<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="0333d-101">この演習では、Microsoft Graph をアプリケーションに組み込みます。</span><span class="sxs-lookup"><span data-stu-id="0333d-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="0333d-102">このアプリケーションでは、microsoft graph [JavaScript クライアントライブラリ](https://github.com/microsoftgraph/msgraph-sdk-javascript)を使用して microsoft graph への呼び出しを行います。</span><span class="sxs-lookup"><span data-stu-id="0333d-102">For this application, you will use the [Microsoft Graph JavaScript Client Library](https://github.com/microsoftgraph/msgraph-sdk-javascript) to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="0333d-103">Outlook から予定表のイベントを取得する</span><span class="sxs-lookup"><span data-stu-id="0333d-103">Get calendar events from Outlook</span></span>

<span data-ttu-id="0333d-104">このセクションでは、 `GraphManager`クラスを拡張して、ユーザーのイベントを取得する関数を追加`CalendarScreen`し、これらの新しい関数を使用するように更新します。</span><span class="sxs-lookup"><span data-stu-id="0333d-104">In this section you will extend the `GraphManager` class to add a function to get the user's events and update `CalendarScreen` to use these new functions.</span></span>

1. <span data-ttu-id="0333d-105">**Graphtutorial/graph/Graphtutorial .js**ファイルを開き、次のメソッドを`GraphManager`クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="0333d-105">Open the **GraphTutorial/graph/GraphManager.js** file and add the following method to the `GraphManager` class.</span></span>

    ```js
    static getEvents = async() => {
      // GET /me/events
      return graphClient.api('/me/events')
        // $select='subject,organizer,start,end'
        // Only return these fields in results
        .select('subject,organizer,start,end')
        // $orderby=createdDateTime DESC
        // Sort results by when they were created, newest first
        .orderby('createdDateTime DESC')
        .get();
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="0333d-106">のコードに`getEvents`ついて検討します。</span><span class="sxs-lookup"><span data-stu-id="0333d-106">Consider what the code in `getEvents` is doing.</span></span>
    >
    > - <span data-ttu-id="0333d-107">呼び出し先の URL は`/v1.0/me/events`になります。</span><span class="sxs-lookup"><span data-stu-id="0333d-107">The URL that will be called is `/v1.0/me/events`.</span></span>
    > - <span data-ttu-id="0333d-108">関数`select`は、各イベントに対して返されるフィールドを、アプリが実際に使用するものだけに制限します。</span><span class="sxs-lookup"><span data-stu-id="0333d-108">The `select` function limits the fields returned for each events to just those the app will actually use.</span></span>
    > - <span data-ttu-id="0333d-109">関数`orderby`は、生成された日付と時刻で結果を並べ替えます。最新のアイテムが最初に表示されます。</span><span class="sxs-lookup"><span data-stu-id="0333d-109">The `orderby` function sorts the results by the date and time they were created, with the most recent item being first.</span></span>

1. <span data-ttu-id="0333d-110">**Graphtutorial/ビュー/CalendarScreen .js**を開き、その内容全体を次のコードで置き換えます。</span><span class="sxs-lookup"><span data-stu-id="0333d-110">Open the **GraphTutorial/views/CalendarScreen.js** and replace its entire contents with the following code.</span></span>

    ```JSX
    import React from 'react';
    import {
      ActivityIndicator,
      FlatList,
      Modal,
      ScrollView,
      StyleSheet,
      Text,
      View,
    } from 'react-native';
    import { Icon } from 'react-native-elements';
    import { GraphManager } from '../graph/GraphManager';

    export default class CalendarScreen extends React.Component {
      static navigationOptions = ({navigation}) => {
        return {
          title: 'Calendar',
          headerLeft: <Icon iconStyle={{ marginLeft: 10, color: 'white' }} size={30} name="menu" onPress={navigation.toggleDrawer} />
        };
      }

      state = {
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
          alert(error);
        }
      }

      // Temporary JSON view
      render() {
        return (
          <View style={styles.container}>
            <Modal visible={this.state.loadingEvents}>
              <View style={styles.loading}>
                <ActivityIndicator animating={this.state.loadingEvents} size='large' />
              </View>
            </Modal>
            <ScrollView>
              <Text>{JSON.stringify(this.state.events, null, 2)}</Text>
            </ScrollView>
          </View>
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

<span data-ttu-id="0333d-111">これで、アプリを実行し、サインインすると、メニューの [**予定表**] ナビゲーション項目をタップできるようになります。</span><span class="sxs-lookup"><span data-stu-id="0333d-111">You can now run the app, sign in, and tap the **Calendar** navigation item in the menu.</span></span> <span data-ttu-id="0333d-112">アプリ内のイベントの JSON ダンプが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0333d-112">You should see a JSON dump of the events in the app.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="0333d-113">結果を表示する</span><span class="sxs-lookup"><span data-stu-id="0333d-113">Display the results</span></span>

<span data-ttu-id="0333d-114">これで、JSON ダンプを、ユーザーにわかりやすい方法で結果を表示するためのものに置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="0333d-114">Now you can replace the JSON dump with something to display the results in a user-friendly manner.</span></span> <span data-ttu-id="0333d-115">このセクションでは、をカレンダー画面`FlatList`に追加して、イベントを表示します。</span><span class="sxs-lookup"><span data-stu-id="0333d-115">In this section, you will add a `FlatList` to the calendar screen to render the events.</span></span>

1. <span data-ttu-id="0333d-116">**Graphtutorial/graph/Graphtutorial .js**ファイルを開き、次`import`のステートメントをファイルの先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="0333d-116">Open the **GraphTutorial/graph/GraphManager.js** file and add the following `import` statement to the top of the file.</span></span>

    ```js
    import moment from 'moment';
    ```

1. <span data-ttu-id="0333d-117">次のメソッドを\*\*\*\* クラス宣言`CalendarScreen`の上に追加します。</span><span class="sxs-lookup"><span data-stu-id="0333d-117">Add the following method **above** the `CalendarScreen` class declaration.</span></span>

    ```js
    convertDateTime = (dateTime) => {
      const utcTime = moment.utc(dateTime);
      return utcTime.local().format('MMM Do H:mm a');
    };
    ```

1. <span data-ttu-id="0333d-118">`ScrollView`メソッドのを次のように置き換え`render`ます。</span><span class="sxs-lookup"><span data-stu-id="0333d-118">Replace the `ScrollView` in the `render` method with the following.</span></span>

    ```JSX
    <FlatList data={this.state.events}
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

1. <span data-ttu-id="0333d-119">アプリを実行し、サインインして、**予定表**のナビゲーションアイテムをタップします。</span><span class="sxs-lookup"><span data-stu-id="0333d-119">Run the app, sign in, and tap the **Calendar** navigation item.</span></span> <span data-ttu-id="0333d-120">イベントの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="0333d-120">You should see the list of events.</span></span>

    ![イベントの表のスクリーンショット](./images/calendar-list.png)
