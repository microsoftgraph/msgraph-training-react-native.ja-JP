<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="5e996-101">この演習では、Microsoft Graph をアプリケーションに組み込みます。</span><span class="sxs-lookup"><span data-stu-id="5e996-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="5e996-102">このアプリケーションでは、microsoft graph [JavaScript クライアントライブラリ](https://github.com/microsoftgraph/msgraph-sdk-javascript)を使用して microsoft graph への呼び出しを行います。</span><span class="sxs-lookup"><span data-stu-id="5e996-102">For this application, you will use the [Microsoft Graph JavaScript Client Library](https://github.com/microsoftgraph/msgraph-sdk-javascript) to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="5e996-103">Outlook からカレンダー イベントを取得する</span><span class="sxs-lookup"><span data-stu-id="5e996-103">Get calendar events from Outlook</span></span>

<span data-ttu-id="5e996-104">このセクションでは、 `GraphManager`クラスを拡張して、ユーザーのイベントを取得する関数を追加`CalendarScreen`し、これらの新しい関数を使用するように更新します。</span><span class="sxs-lookup"><span data-stu-id="5e996-104">In this section you will extend the `GraphManager` class to add a function to get the user's events and update `CalendarScreen` to use these new functions.</span></span>

1. <span data-ttu-id="5e996-105">**Graphtutorial/graph/Graphtutorial tsx**ファイルを開き、次のメソッドを`GraphManager`クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="5e996-105">Open the **GraphTutorial/graph/GraphManager.tsx** file and add the following method to the `GraphManager` class.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphManager.ts" id="GetEventsSnippet":::

    > [!NOTE]
    > <span data-ttu-id="5e996-106">のコードに`getEvents`ついて検討します。</span><span class="sxs-lookup"><span data-stu-id="5e996-106">Consider what the code in `getEvents` is doing.</span></span>
    >
    > - <span data-ttu-id="5e996-107">呼び出される URL は `/v1.0/me/events` です。</span><span class="sxs-lookup"><span data-stu-id="5e996-107">The URL that will be called is `/v1.0/me/events`.</span></span>
    > - <span data-ttu-id="5e996-108">関数`select`は、各イベントに対して返されるフィールドを、アプリが実際に使用するものだけに制限します。</span><span class="sxs-lookup"><span data-stu-id="5e996-108">The `select` function limits the fields returned for each events to just those the app will actually use.</span></span>
    > - <span data-ttu-id="5e996-109">`orderby` 関数は、作成された日時で結果を並べ替えます。最新のアイテムが最初に表示されます。</span><span class="sxs-lookup"><span data-stu-id="5e996-109">The `orderby` function sorts the results by the date and time they were created, with the most recent item being first.</span></span>

1. <span data-ttu-id="5e996-110">**Graphtutorial/ビュー/CalendarScreen**を開き、その内容全体を次のコードで置き換えます。</span><span class="sxs-lookup"><span data-stu-id="5e996-110">Open the **GraphTutorial/views/CalendarScreen.tsx** and replace its entire contents with the following code.</span></span>

    ```typescript
    import React from 'react';
    import {
      ActivityIndicator,
      Alert,
      FlatList,
      Modal,
      ScrollView,
      StyleSheet,
      Text,
      View,
    } from 'react-native';
    import { createStackNavigator } from '@react-navigation/stack';

    import { DrawerToggle, headerOptions } from '../menus/HeaderComponents';
    import { GraphManager } from '../graph/GraphManager';

    const Stack = createStackNavigator();
    const initialState: CalendarScreenState = { loadingEvents: true, events: []};
    const CalendarState = React.createContext(initialState);

    type CalendarScreenState = {
      loadingEvents: boolean;
      events: any[];
    }

    // Temporary JSON view
    const CalendarComponent = () => {
      const calendarState = React.useContext(CalendarState);

      return (
        <View style={styles.container}>
          <Modal visible={calendarState.loadingEvents}>
            <View style={styles.loading}>
              <ActivityIndicator animating={calendarState.loadingEvents} size='large' />
            </View>
          </Modal>
          <ScrollView>
            <Text>{JSON.stringify(calendarState.events, null, 2)}</Text>
          </ScrollView>
        </View>
      );
    }

    export default class CalendarScreen extends React.Component {

      state: CalendarScreenState = {
        loadingEvents: true,
        events: []
      };

      async componentDidMount() {
        try {
          const events = await GraphManager.getEvents();

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
            <Stack.Navigator screenOptions={ headerOptions }>
              <Stack.Screen name='Calendar'
                component={ CalendarComponent }
                options={{
                  title: 'Calendar',
                  headerLeft: () => <DrawerToggle/>
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

<span data-ttu-id="5e996-111">これで、アプリを実行し、サインインすると、メニューの [**予定表**] ナビゲーション項目をタップできるようになります。</span><span class="sxs-lookup"><span data-stu-id="5e996-111">You can now run the app, sign in, and tap the **Calendar** navigation item in the menu.</span></span> <span data-ttu-id="5e996-112">アプリ内のイベントの JSON ダンプが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5e996-112">You should see a JSON dump of the events in the app.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="5e996-113">結果の表示</span><span class="sxs-lookup"><span data-stu-id="5e996-113">Display the results</span></span>

<span data-ttu-id="5e996-114">これで、JSON ダンプを、ユーザーにわかりやすい方法で結果を表示するためのものに置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="5e996-114">Now you can replace the JSON dump with something to display the results in a user-friendly manner.</span></span> <span data-ttu-id="5e996-115">このセクションでは、をカレンダー画面`FlatList`に追加して、イベントを表示します。</span><span class="sxs-lookup"><span data-stu-id="5e996-115">In this section, you will add a `FlatList` to the calendar screen to render the events.</span></span>

1. <span data-ttu-id="5e996-116">**Graphtutorial/graph/screen/calendarscreen. tsx**ファイルを開き、次`import`のステートメントをファイルの先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="5e996-116">Open the **GraphTutorial/graph/screens/CalendarScreen.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import moment from 'moment';
    ```

1. <span data-ttu-id="5e996-117">次のメソッドを**above**クラス宣言`CalendarScreen`の上に追加します。</span><span class="sxs-lookup"><span data-stu-id="5e996-117">Add the following method **above** the `CalendarScreen` class declaration.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/CalendarScreen.tsx" id="ConvertDateSnippet":::

1. <span data-ttu-id="5e996-118">`ScrollView`メソッドのを次のように置き換え`CalendarComponent`ます。</span><span class="sxs-lookup"><span data-stu-id="5e996-118">Replace the `ScrollView` in the `CalendarComponent` method with the following.</span></span>

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

1. <span data-ttu-id="5e996-119">アプリを実行し、サインインして、**予定表**のナビゲーションアイテムをタップします。</span><span class="sxs-lookup"><span data-stu-id="5e996-119">Run the app, sign in, and tap the **Calendar** navigation item.</span></span> <span data-ttu-id="5e996-120">イベントの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="5e996-120">You should see the list of events.</span></span>

    ![イベント表のスクリーンショット](./images/calendar-list.png)
