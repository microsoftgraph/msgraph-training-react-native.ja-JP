<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="3e065-101">最初に、新しい反応するネイティブプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="3e065-101">Begin by creating a new React Native project.</span></span>

1. <span data-ttu-id="3e065-102">プロジェクトを作成するディレクトリで、コマンドラインインターフェイス (CLI) を開きます。</span><span class="sxs-lookup"><span data-stu-id="3e065-102">Open your command line interface (CLI) in a directory where you want to create the project.</span></span> <span data-ttu-id="3e065-103">次のコマンドを実行して、[対応するネイティブな cli](https://github.com/facebook/react-native)ツールをインストールし、新しい反応するネイティブプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="3e065-103">Run the following command to install the [react-native-cli](https://github.com/facebook/react-native) tool and create a new React Native project.</span></span>

    ```Shell
    npm install -g react-native-cli
    react-native init GraphTutorial
    ```

1. <span data-ttu-id="3e065-104">**省略可能:** プロジェクトを実行して、開発環境が正しく構成されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="3e065-104">**Optional:** Verify that your development environment is configured correctly by running the project.</span></span> <span data-ttu-id="3e065-105">CLI で、作成したばかりの**Graphtutorial**ディレクトリにディレクトリを変更し、次のいずれかのコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="3e065-105">In your CLI, change the directory to the **GraphTutorial** directory you just created, and run one of the following commands.</span></span>

    - <span data-ttu-id="3e065-106">IOS の場合:`react-native run-ios`</span><span class="sxs-lookup"><span data-stu-id="3e065-106">For iOS: `react-native run-ios`</span></span>
    - <span data-ttu-id="3e065-107">Android の場合: Android エミュレーターのインスタンスを起動し、を実行します。`react-native run-android`</span><span class="sxs-lookup"><span data-stu-id="3e065-107">For Android: Launch an Android emulator instance and run `react-native run-android`</span></span>

## <a name="install-dependencies"></a><span data-ttu-id="3e065-108">依存関係のインストール</span><span class="sxs-lookup"><span data-stu-id="3e065-108">Install dependencies</span></span>

<span data-ttu-id="3e065-109">に進む前に、後で使用する追加の依存関係をインストールします。</span><span class="sxs-lookup"><span data-stu-id="3e065-109">Before moving on, install some additional dependencies that you will use later.</span></span>

- <span data-ttu-id="3e065-110">アプリ内のビュー間のナビゲーションを処理するための[ナビゲーションの反応](https://reactnavigation.org)。</span><span class="sxs-lookup"><span data-stu-id="3e065-110">[react-navigation](https://reactnavigation.org) to handle navigation between views in the app.</span></span>
- <span data-ttu-id="3e065-111">[ネイティブのジェスチャハンドラー](https://github.com/kmagiera/react-native-gesture-handler)を処理し、[ネイティブの復元](https://github.com/kmagiera/react-native-reanimated)に対応します。これは、ナビゲーションの反応によって必要になります。</span><span class="sxs-lookup"><span data-stu-id="3e065-111">[react-native-gesture-handler](https://github.com/kmagiera/react-native-gesture-handler) and [react-native-reanimate](https://github.com/kmagiera/react-native-reanimated), required by react-navigation.</span></span>
- <span data-ttu-id="3e065-112">UI のアイコンを提供する[ネイティブ要素](https://react-native-training.github.io/react-native-elements/docs/getting_started.html)と、[ネイティブベクトルアイコン](https://github.com/oblador/react-native-vector-icons)を反応させる。</span><span class="sxs-lookup"><span data-stu-id="3e065-112">[react-native-elements](https://react-native-training.github.io/react-native-elements/docs/getting_started.html) and [react-native-vector-icons](https://github.com/oblador/react-native-vector-icons) to provide icons for the UI.</span></span>
- <span data-ttu-id="3e065-113">認証とトークンの管理を処理する[ネイティブアプリ](https://github.com/FormidableLabs/react-native-app-auth)認証を処理します。</span><span class="sxs-lookup"><span data-stu-id="3e065-113">[react-native-app-auth](https://github.com/FormidableLabs/react-native-app-auth) to handle authentication and token management.</span></span>
- <span data-ttu-id="3e065-114">日付と時刻の解析と比較を処理するには、[しばらくお待ち](https://momentjs.com)ください。</span><span class="sxs-lookup"><span data-stu-id="3e065-114">[moment](https://momentjs.com) to handle parsing and comparison of dates and times.</span></span>
- <span data-ttu-id="3e065-115">[microsoft graph-](https://github.com/microsoftgraph/msgraph-sdk-javascript) microsoft graph に電話をかけるためのクライアントです。</span><span class="sxs-lookup"><span data-stu-id="3e065-115">[microsoft-graph-client](https://github.com/microsoftgraph/msgraph-sdk-javascript) for making calls to the Microsoft Graph.</span></span>

1. <span data-ttu-id="3e065-116">応答するネイティブプロジェクトのルートディレクトリで、CLI を開きます。</span><span class="sxs-lookup"><span data-stu-id="3e065-116">Open your CLI in the root directory of your React Native project.</span></span>
1. <span data-ttu-id="3e065-117">次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="3e065-117">Run the following command.</span></span>

    ```Shell
    npm install react-navigation@3.11.1 react-native-gesture-handler@1.3.0 react-native-reanimated@1.1.0
    npm install react-native-elements@1.1.0 react-native-vector-icons@6.6.0 moment@2.24.0
    npm install react-native-app-auth@4.4.0 @microsoft/microsoft-graph-client@1.7.0
    react-native link react-native-vector-icons
    ```

### <a name="link-and-configure-dependencies-for-ios"></a><span data-ttu-id="3e065-118">IOS の依存関係をリンクおよび構成する</span><span class="sxs-lookup"><span data-stu-id="3e065-118">Link and configure dependencies for iOS</span></span>

> [!NOTE]
> <span data-ttu-id="3e065-119">IOS を対象としていない場合は、このセクションを省略できます。</span><span class="sxs-lookup"><span data-stu-id="3e065-119">If you are not targeting iOS, you can skip this section.</span></span>

1. <span data-ttu-id="3e065-120">**Graphtutorial/ios**ディレクトリで CLI を開きます。</span><span class="sxs-lookup"><span data-stu-id="3e065-120">Open your CLI in the **GraphTutorial/ios** directory.</span></span>
1. <span data-ttu-id="3e065-121">次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="3e065-121">Run the following command.</span></span>

    ```Shell
    pod install
    ```

1. <span data-ttu-id="3e065-122">テキストエディターで、 **graphtutorial/ios/GraphTutorial/AppDelegate. .h**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="3e065-122">Open the **GraphTutorial/ios/GraphTutorial/AppDelegate.h** file in a text editor.</span></span> <span data-ttu-id="3e065-123">その内容を次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="3e065-123">Replace its contents with the following.</span></span>

    ```obj-c
    #import <React/RCTBridgeDelegate.h>
    #import <UIKit/UIKit.h>
    #import "RNAppAuthAuthorizationFlowManager.h"

    @interface AppDelegate : UIResponder <UIApplicationDelegate, RCTBridgeDelegate, RNAppAuthAuthorizationFlowManager>

    @property (nonatomic, strong) UIWindow *window;
    @property (nonatomic, weak) id<RNAppAuthAuthorizationFlowManagerDelegate> authorizationFlowManagerDelegate;

    @end
    ```

### <a name="configure-dependencies-for-android"></a><span data-ttu-id="3e065-124">Android の依存関係を構成する</span><span class="sxs-lookup"><span data-stu-id="3e065-124">Configure dependencies for Android</span></span>

> [!NOTE]
> <span data-ttu-id="3e065-125">Android を対象としていない場合は、このセクションを省略できます。</span><span class="sxs-lookup"><span data-stu-id="3e065-125">If you are not targeting Android, you can skip this section.</span></span>

1. <span data-ttu-id="3e065-126">エディターで**Graphtutorial/android/app/gradle**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="3e065-126">Open the **GraphTutorial/android/app/build.gradle** file in an editor.</span></span>
1. <span data-ttu-id="3e065-127">`defaultConfig`エントリを検索し、その中`defaultConfig`に次のプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="3e065-127">Locate the `defaultConfig` entry and add the following property inside `defaultConfig`.</span></span>

    ```Gradle
    manifestPlaceholders = [
        appAuthRedirectScheme: 'graph-tutorial'
    ]
    ```

1. <span data-ttu-id="3e065-128">ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="3e065-128">Save the file.</span></span> <span data-ttu-id="3e065-129">この`defaultConfig`エントリは、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="3e065-129">The `defaultConfig` entry should look similar to the following.</span></span>

    ```Gradle
    defaultConfig {
        applicationId "com.graphtutorial"
        minSdkVersion rootProject.ext.minSdkVersion
        targetSdkVersion rootProject.ext.targetSdkVersion
        versionCode 1
        versionName "1.0"
        manifestPlaceholders = [
            appAuthRedirectScheme: 'graphtutorial'
        ]
    }
    ```

## <a name="design-the-app"></a><span data-ttu-id="3e065-130">アプリを設計する</span><span class="sxs-lookup"><span data-stu-id="3e065-130">Design the app</span></span>

<span data-ttu-id="3e065-131">アプリケーションは、[ナビゲーションドロアー](https://reactnavigation.org/docs/drawer-based-navigation.html)を使用して、さまざまなビュー間を移動します。</span><span class="sxs-lookup"><span data-stu-id="3e065-131">The application will use a [navigation drawer](https://reactnavigation.org/docs/drawer-based-navigation.html) to navigate between different views.</span></span> <span data-ttu-id="3e065-132">この手順では、アプリで使用される基本的なビューを作成し、ナビゲーションドロアーを実装します。</span><span class="sxs-lookup"><span data-stu-id="3e065-132">In this step you will create the basic views used by the app and implement the navigation drawer.</span></span>

### <a name="create-views"></a><span data-ttu-id="3e065-133">ビューを作成する</span><span class="sxs-lookup"><span data-stu-id="3e065-133">Create views</span></span>

<span data-ttu-id="3e065-134">このセクションでは、[認証フロー](https://reactnavigation.org/docs/auth-flow.html)をサポートするためのアプリのビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="3e065-134">In this section you will create the views for the app to support an [authentication flow](https://reactnavigation.org/docs/auth-flow.html).</span></span>

1. <span data-ttu-id="3e065-135">**Graphtutorial**の「 **views**」という名前の新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="3e065-135">Create a new directory in the **GraphTutorial** directory named **views**.</span></span>
1. <span data-ttu-id="3e065-136">**HomeScreen**という名前の新しいファイルを**graphtutorial/views**ディレクトリに作成します。</span><span class="sxs-lookup"><span data-stu-id="3e065-136">Create a new file in the **GraphTutorial/views** directory named **HomeScreen.js**.</span></span> <span data-ttu-id="3e065-137">このファイルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="3e065-137">Add the following code to the file.</span></span>

    ```JSX
    import React from 'react';
    import {
      ActivityIndicator,
      Text,
      StyleSheet,
      View,
    } from 'react-native';
    import { Icon } from 'react-native-elements';

    export default class HomeScreen extends React.Component {
      static navigationOptions = ({navigation}) => {
        return {
          title: 'Welcome',
          headerLeft: <Icon iconStyle={{ marginLeft: 10, color: 'white' }} size={30} name="menu" onPress={navigation.toggleDrawer} />
        };
      }

      state = {
        userLoading: true,
        userName: ''
      };

      render() {
        return (
          <View style={styles.container}>
            <ActivityIndicator animating={this.state.userLoading} size='large' />
            {this.state.userLoading ? null: <Text>Hello {this.state.userName}!</Text>}
          </View>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center'
      }
    });
    ```

1. <span data-ttu-id="3e065-138">**Graphtutorial .js**という名前の**graphtutorial/views**ディレクトリに新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="3e065-138">Create a new file in the **GraphTutorial/views** directory named **CalendarScreen.js**.</span></span> <span data-ttu-id="3e065-139">このファイルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="3e065-139">Add the following code to the file.</span></span>

    ```JSX
    import React from 'react';
    import {
      Text,
      StyleSheet,
      View,
    } from 'react-native';
    import { Icon } from 'react-native-elements';

    export default class CalendarScreen extends React.Component {
      static navigationOptions = ({navigation}) => {
        return {
          title: 'Calendar',
          headerLeft: <Icon iconStyle={{ marginLeft: 10, color: 'white' }} size={30} name="menu" onPress={navigation.toggleDrawer} />
        };
      }

      // Temporary placeholder view
      render() {
        return (
          <View style={styles.container}>
            <Text>Calendar</Text>
          </View>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center'
      }
    });
    ```

1. <span data-ttu-id="3e065-140">**SignInScreen**という名前の新しいファイルを**graphtutorial/views**ディレクトリに作成します。</span><span class="sxs-lookup"><span data-stu-id="3e065-140">Create a new file in the **GraphTutorial/views** directory named **SignInScreen.js**.</span></span> <span data-ttu-id="3e065-141">このファイルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="3e065-141">Add the following code to the file.</span></span>

    ```JSX
    // Adapted from https://reactnavigation.org/docs/auth-flow.html
    import React from 'react';
    import {
      Button,
      StyleSheet,
      View,
    } from 'react-native';

    export default class SignInScreen extends React.Component {
      static navigationOptions = {
        title: 'Please sign in',
      };

      _signInAsync = async () => {
        // TEMPORARY
        this.props.navigation.navigate('App');
      };

      render() {
        return (
          <View style={styles.container}>
            <Button title="Sign In" onPress={this._signInAsync}/>
          </View>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center'
      }
    });
    ```

1. <span data-ttu-id="3e065-142">「 **Authload Ingscreen**」という名前の**graphtutorial または views**ディレクトリに新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="3e065-142">Create a new file in the **GraphTutorial/views** directory named **AuthLoadingScreen.js**.</span></span> <span data-ttu-id="3e065-143">このファイルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="3e065-143">Add the following code to the file.</span></span>

    ```JSX
    // Adapted from https://reactnavigation.org/docs/auth-flow.html
    import React from 'react';
    import {
      ActivityIndicator,
      AsyncStorage,
      Text,
      StyleSheet,
      View,
    } from 'react-native';

    export default class AuthLoadingScreen extends React.Component {

      componentDidMount() {
        this._bootstrapAsync();
      }

      // Fetch the token from storage then navigate to our appropriate place
      // NOTE: Production apps should protect user tokens in secure storage.
      _bootstrapAsync = async () => {
        const userToken = await AsyncStorage.getItem('userToken');

        // This will switch to the App screen or Auth screen and this loading
        // screen will be unmounted and thrown away.
        this.props.navigation.navigate(userToken ? 'App' : 'Auth');
      };

      render() {
        return (
          <View style={styles.container}>
            <ActivityIndicator size='large' />
            <Text style={styles.statusText}>Logging in...</Text>
          </View>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center'
      },
      statusText: {
        marginTop: 10
      }
    });
    ```

### <a name="create-a-navigation-drawer"></a><span data-ttu-id="3e065-144">ナビゲーションドロアーを作成する</span><span class="sxs-lookup"><span data-stu-id="3e065-144">Create a navigation drawer</span></span>

<span data-ttu-id="3e065-145">このセクションでは、アプリケーションのメニューを作成し、画面間を移動するために反応するナビゲーションを使用するようにアプリケーションを更新します。</span><span class="sxs-lookup"><span data-stu-id="3e065-145">In this section you will create a menu for the application, and update the application to use react-navigation to move between screens.</span></span>

1. <span data-ttu-id="3e065-146">「**メニュー**という名前の**graphtutorial**ディレクトリ」に新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="3e065-146">Create a new directory in the **GraphTutorial** directory named **menus**.</span></span>
1. <span data-ttu-id="3e065-147">「 **Drawermenu**」という名前の**graphermenu**ディレクトリに新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="3e065-147">Create a new file in the **GraphTutorial/menus** directory named **DrawerMenu.js**.</span></span> <span data-ttu-id="3e065-148">このファイルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="3e065-148">Add the following code to the file.</span></span>

    ```JSX
    import React from 'react';
    import {
      Image,
      SafeAreaView,
      ScrollView,
      StyleSheet,
      Text,
      View
    } from 'react-native';
    import { DrawerItems } from 'react-navigation';

    export default class DrawerMenuContent extends React.Component {

      state = {
        // TEMPORARY
        userName: 'Adele Vance',
        userEmail: 'adelev@contoso.com',
        userPhoto: require('../images/no-profile-pic.png')
      }

      // Check if user tapped on the Sign Out button and
      // sign the user out
      _onItemPressed = async (route) => {
        if (route.route.routeName !== 'Sign Out') {
          this.props.onItemPress(route);
          return;
        }

        // Sign out
        // TEMPORARY
        this.props.navigation.navigate('Auth');
      }

      render() {
        return (
          <ScrollView>
            <SafeAreaView style={styles.container}
              forceInset={{ top: 'always', horizontal: 'never' }}>
              <View style={styles.profileView}>
                <Image source={this.state.userPhoto}
                  resizeMode='contain'
                  style={styles.profilePhoto} />
                <Text style={styles.profileUserName}>{this.state.userName}</Text>
                <Text style={styles.profileEmail}>{this.state.userEmail}</Text>
              </View>
              <DrawerItems {...this.props}
                onItemPress={this._onItemPressed}/>
            </SafeAreaView>
          </ScrollView>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1
      },
      profileView: {
        alignItems: 'center',
        padding: 10
      },
      profilePhoto: {
        width: 80,
        height: 80,
        borderRadius: 40
      },
      profileUserName: {
        fontWeight: '700'
      },
      profileEmail: {
        fontWeight: '200',
        fontSize: 10
      }
    });
    ```

1. <span data-ttu-id="3e065-149">**Graphtutorial/app.config**ファイルを開き、内容全体を次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="3e065-149">Open the **GraphTutorial/App.js** file and replace the entire contents with the following.</span></span>

    ```JSX
    // Adapted from https://reactnavigation.org/docs/auth-flow.html
    import {
      createSwitchNavigator,
      createStackNavigator,
      createDrawerNavigator,
      createAppContainer } from "react-navigation";

    import AuthLoadingScreen from './views/AuthLoadingScreen';
    import SignInScreen from './views/SignInScreen';
    import HomeScreen from './views/HomeScreen';
    import CalendarScreen from './views/CalendarScreen';
    import DrawerMenuContent from './menus/DrawerMenu';

    const headerOptions = {
      defaultNavigationOptions: {
        headerStyle: {
          backgroundColor: '#276b80'
        },
        headerTintColor: 'white'
      }
    };

    const AuthStack = createStackNavigator(
      {
        SignIn: SignInScreen
      },
      headerOptions
    );

    const AppDrawer = createDrawerNavigator(
      {
        Home: createStackNavigator({ Home: HomeScreen }, headerOptions),
        Calendar: createStackNavigator({ Calendar: CalendarScreen }, headerOptions),
        'Sign Out': 'SignOut'
      },
      {
        hideStatusBar: false,
        contentComponent: DrawerMenuContent
      }
    );

    export default createAppContainer(createSwitchNavigator(
      {
        AuthLoading: AuthLoadingScreen,
        App: AppDrawer,
        Auth: AuthStack
      },
      {
        initialRouteName: 'AuthLoading'
      }
    ));

1. Save all of your changes.

1. Reload the application in your emulator.

The app's menu should work to navigate between the two fragments and change when you tap the **Sign in** or **Sign out** buttons.

![Screenshots of the application on Android](./images/android-app-screens.png)

![Screenshots of the application on iOS](./images/ios-app-screens.png)

> [!NOTE]
> You may receive warnings when running the app about Async Storage or componentWillUpdate. For the purposes of this tutorial, you can dismiss those warnings.
