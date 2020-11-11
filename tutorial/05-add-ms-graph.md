<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="b2050-101">この演習では、Microsoft Graph をアプリケーションに組み込みます。</span><span class="sxs-lookup"><span data-stu-id="b2050-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="b2050-102">このアプリケーションでは、microsoft graph [JavaScript クライアントライブラリ](https://github.com/microsoftgraph/msgraph-sdk-javascript) を使用して microsoft graph への呼び出しを行います。</span><span class="sxs-lookup"><span data-stu-id="b2050-102">For this application, you will use the [Microsoft Graph JavaScript Client Library](https://github.com/microsoftgraph/msgraph-sdk-javascript) to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="b2050-103">Outlook からカレンダー イベントを取得する</span><span class="sxs-lookup"><span data-stu-id="b2050-103">Get calendar events from Outlook</span></span>

<span data-ttu-id="b2050-104">このセクションでは、クラスを拡張して、 `GraphManager` 現在の週のユーザーイベントを取得する関数を追加し、新しい関数を使用するように更新し `CalendarScreen` ます。</span><span class="sxs-lookup"><span data-stu-id="b2050-104">In this section you will extend the `GraphManager` class to add a function to get the user's events for the current week and update `CalendarScreen` to use these new functions.</span></span>

1. <span data-ttu-id="b2050-105">**Graphtutorial/graph/Graphtutorial tsx** ファイルを開き、次のメソッドをクラスに追加し `GraphManager` ます。</span><span class="sxs-lookup"><span data-stu-id="b2050-105">Open the **GraphTutorial/graph/GraphManager.tsx** file and add the following method to the `GraphManager` class.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphManager.ts" id="GetCalendarViewSnippet":::

    > [!NOTE]
    > <span data-ttu-id="b2050-106">のコードについて検討 `getCalendarView` します。</span><span class="sxs-lookup"><span data-stu-id="b2050-106">Consider what the code in `getCalendarView` is doing.</span></span>
    >
    > - <span data-ttu-id="b2050-107">呼び出される URL は `/v1.0/me/calendarView` です。</span><span class="sxs-lookup"><span data-stu-id="b2050-107">The URL that will be called is `/v1.0/me/calendarView`.</span></span>
    > - <span data-ttu-id="b2050-108">この `header` 関数は、 `Prefer: outlook.timezone` 要求にヘッダーを追加して、応答内の時間をユーザーの優先タイムゾーンに追加します。</span><span class="sxs-lookup"><span data-stu-id="b2050-108">The `header` function adds the `Prefer: outlook.timezone` header to the request, causing the times in the response to be in the user's preferred time zone.</span></span>
    > - <span data-ttu-id="b2050-109">関数は、 `query` `startDateTime` および `endDateTime` カレンダービューの時間のウィンドウを定義するパラメーターを追加します。</span><span class="sxs-lookup"><span data-stu-id="b2050-109">The `query` function adds the `startDateTime` and `endDateTime` parameters, defining the window of time for the calendar view.</span></span>
    > - <span data-ttu-id="b2050-110">関数は、 `select` 各イベントに対して返されるフィールドを、アプリが実際に使用するものだけに制限します。</span><span class="sxs-lookup"><span data-stu-id="b2050-110">The `select` function limits the fields returned for each events to just those the app will actually use.</span></span>
    > - <span data-ttu-id="b2050-111">関数は、 `orderby` 開始時刻で結果を並べ替えます。</span><span class="sxs-lookup"><span data-stu-id="b2050-111">The `orderby` function sorts the results by the start time.</span></span>
    > - <span data-ttu-id="b2050-112">この `top` 関数は、結果を最初の50イベントに制限します。</span><span class="sxs-lookup"><span data-stu-id="b2050-112">The `top` function limits the results to the first 50 events.</span></span>

1. <span data-ttu-id="b2050-113">**Graphtutorial/ビュー/CalendarScreen** を開き、その内容全体を次のコードで置き換えます。</span><span class="sxs-lookup"><span data-stu-id="b2050-113">Open the **GraphTutorial/views/CalendarScreen.tsx** and replace its entire contents with the following code.</span></span>

    ```typescript
    import React from 'react';
    import {
      ActivityIndicator,
      Alert,
      FlatList,
      Modal,
      Platform,
      ScrollView,
      StyleSheet,
      Text,
      View,
    } from 'react-native';
    import { createStackNavigator } from '@react-navigation/stack';
    import * as MicrosoftGraph from '@microsoft/microsoft-graph-types';
    import moment from 'moment-timezone';
    import { findOneIana } from 'windows-iana';

    import { UserContext } from '../UserContext';
    import { GraphManager } from '../graph/GraphManager';

    const Stack = createStackNavigator();
    const CalendarState = React.createContext<CalendarScreenState>({
      loadingEvents: true,
      events: []
    });

    type CalendarScreenState = {
      loadingEvents: boolean;
      events: MicrosoftGraph.Event[];
    }

    // Temporary JSON view
    const CalendarComponent = () => {
      const calendarState = React.useContext(CalendarState);

      return (
        <View style={styles.container}>
          <Modal visible={calendarState.loadingEvents}>
            <View style={styles.loading}>
              <ActivityIndicator
                color={Platform.OS === 'android' ? '#276b80' : undefined}
                animating={calendarState.loadingEvents}
                size='large' />
            </View>
          </Modal>
          <ScrollView>
            <Text>{JSON.stringify(calendarState.events, null, 2)}</Text>
          </ScrollView>
        </View>
      );
    }

    export default class CalendarScreen extends React.Component {
      static contextType = UserContext;

      state: CalendarScreenState = {
        loadingEvents: true,
        events: []
      };

      async componentDidMount() {
        try {
          const tz = this.context.userTimeZone || 'UTC';
          // Convert user's Windows time zone ("Pacific Standard Time")
          // to IANA format ("America/Los_Angeles")
          // Moment.js needs IANA format
          const ianaTimeZone = findOneIana(tz);

          // Get midnight on the start of the current week in the user's
          // time zone, but in UTC. For example, for PST, the time value
          // would be 07:00:00Z
          const startOfWeek = moment
            .tz(ianaTimeZone!.valueOf())
            .startOf('week')
            .utc();

          const endOfWeek = moment(startOfWeek)
            .add(7, 'day');

          const events = await GraphManager.getCalendarView(
            startOfWeek.format(),
            endOfWeek.format(),
            tz);

          this.setState({
            loadingEvents: false,
            events: events.value
          });
        } catch(error) {
          Alert.alert(
            'Error getting events',
            JSON.stringify(error),
            [
              {
                text: 'OK'
              }
            ],
            { cancelable: false }
          );

        }
      }

      render() {
        return (
          <CalendarState.Provider value={this.state}>
            <Stack.Navigator>
              <Stack.Screen name='Calendar'
                component={ CalendarComponent }
                options={{
                  headerShown: false
                }} />
            </Stack.Navigator>
          </CalendarState.Provider>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1
      },
      loading: {
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center'
      },
      eventItem: {
        padding: 10
      },
      eventSubject: {
        fontWeight: '700',
        fontSize: 18
      },
      eventOrganizer: {
        fontWeight: '200'
      },
      eventDuration: {
        fontWeight: '200'
      }
    });
    ```

<span data-ttu-id="b2050-114">これで、アプリを実行し、サインインすると、メニューの [ **予定表** ] ナビゲーション項目をタップできるようになります。</span><span class="sxs-lookup"><span data-stu-id="b2050-114">You can now run the app, sign in, and tap the **Calendar** navigation item in the menu.</span></span> <span data-ttu-id="b2050-115">アプリ内のイベントの JSON ダンプが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b2050-115">You should see a JSON dump of the events in the app.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="b2050-116">結果の表示</span><span class="sxs-lookup"><span data-stu-id="b2050-116">Display the results</span></span>

<span data-ttu-id="b2050-117">これで、JSON ダンプを、ユーザーにわかりやすい方法で結果を表示するためのものに置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="b2050-117">Now you can replace the JSON dump with something to display the results in a user-friendly manner.</span></span> <span data-ttu-id="b2050-118">このセクションでは、を `FlatList` カレンダー画面に追加して、イベントを表示します。</span><span class="sxs-lookup"><span data-stu-id="b2050-118">In this section, you will add a `FlatList` to the calendar screen to render the events.</span></span>

1. <span data-ttu-id="b2050-119">次のメソッドをクラス宣言の **上** に追加し `CalendarScreen` ます。</span><span class="sxs-lookup"><span data-stu-id="b2050-119">Add the following method **above** the `CalendarScreen` class declaration.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/CalendarScreen.tsx" id="ConvertDateSnippet":::

1. <span data-ttu-id="b2050-120">メソッドのを次のように置き換え `ScrollView` `CalendarComponent` ます。</span><span class="sxs-lookup"><span data-stu-id="b2050-120">Replace the `ScrollView` in the `CalendarComponent` method with the following.</span></span>

    ```typescript
    <FlatList data={calendarState.events}
      renderItem={({item}) =>
        <View style={styles.eventItem}>
          <Text style={styles.eventSubject}>{item.subject}</Text>
          <Text style={styles.eventOrganizer}>{item.organizer.emailAddress.name}</Text>
          <Text style={styles.eventDuration}>
            {convertDateTime(item.start.dateTime)} - {convertDateTime(item.end.dateTime)}
          </Text>
        </View>
      } />
    ```

1. <span data-ttu-id="b2050-121">アプリを実行し、サインインして、 **予定表** のナビゲーションアイテムをタップします。</span><span class="sxs-lookup"><span data-stu-id="b2050-121">Run the app, sign in, and tap the **Calendar** navigation item.</span></span> <span data-ttu-id="b2050-122">イベントの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b2050-122">You should see the list of events.</span></span>

    ![イベント表のスクリーンショット](./images/calendar-list.png)
