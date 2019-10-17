<!-- markdownlint-disable MD002 MD041 -->

最初に、新しい反応するネイティブプロジェクトを作成します。

1. プロジェクトを作成するディレクトリで、コマンドラインインターフェイス (CLI) を開きます。 次のコマンドを実行して、[対応するネイティブな cli](https://github.com/facebook/react-native)ツールをインストールし、新しい反応するネイティブプロジェクトを作成します。

    ```Shell
    npm install -g react-native-cli
    react-native init GraphTutorial
    ```

1. **省略可能:** プロジェクトを実行して、開発環境が正しく構成されていることを確認します。 CLI で、作成したばかりの**Graphtutorial**ディレクトリにディレクトリを変更し、次のいずれかのコマンドを実行します。

    - IOS の場合:`react-native run-ios`
    - Android の場合: Android エミュレーターのインスタンスを起動し、を実行します。`react-native run-android`

## <a name="install-dependencies"></a>依存関係のインストール

に進む前に、後で使用する追加の依存関係をインストールします。

- アプリ内のビュー間のナビゲーションを処理するための[ナビゲーションの反応](https://reactnavigation.org)。
- [ネイティブのジェスチャハンドラー](https://github.com/kmagiera/react-native-gesture-handler)を処理し、[ネイティブの復元](https://github.com/kmagiera/react-native-reanimated)に対応します。これは、ナビゲーションの反応によって必要になります。
- UI のアイコンを提供する[ネイティブ要素](https://react-native-training.github.io/react-native-elements/docs/getting_started.html)と、[ネイティブベクトルアイコン](https://github.com/oblador/react-native-vector-icons)を反応させる。
- 認証とトークンの管理を処理する[ネイティブアプリ](https://github.com/FormidableLabs/react-native-app-auth)認証を処理します。
- 日付と時刻の解析と比較を処理するには、[しばらくお待ち](https://momentjs.com)ください。
- [microsoft graph-](https://github.com/microsoftgraph/msgraph-sdk-javascript) microsoft graph に電話をかけるためのクライアントです。

1. 応答するネイティブプロジェクトのルートディレクトリで、CLI を開きます。
1. 次のコマンドを実行します。

    ```Shell
    npm install react-navigation@3.11.1 react-native-gesture-handler@1.3.0 react-native-reanimated@1.1.0
    npm install react-native-elements@1.1.0 react-native-vector-icons@6.6.0 moment@2.24.0
    npm install react-native-app-auth@4.4.0 @microsoft/microsoft-graph-client@1.7.0
    react-native link react-native-vector-icons
    ```

### <a name="link-and-configure-dependencies-for-ios"></a>IOS の依存関係をリンクおよび構成する

> [!NOTE]
> IOS を対象としていない場合は、このセクションを省略できます。

1. **Graphtutorial/ios**ディレクトリで CLI を開きます。
1. 次のコマンドを実行します。

    ```Shell
    pod install
    ```

1. テキストエディターで、 **graphtutorial/ios/GraphTutorial/AppDelegate. .h**ファイルを開きます。 その内容を次のように置き換えます。

    ```obj-c
    #import <React/RCTBridgeDelegate.h>
    #import <UIKit/UIKit.h>
    #import "RNAppAuthAuthorizationFlowManager.h"

    @interface AppDelegate : UIResponder <UIApplicationDelegate, RCTBridgeDelegate, RNAppAuthAuthorizationFlowManager>

    @property (nonatomic, strong) UIWindow *window;
    @property (nonatomic, weak) id<RNAppAuthAuthorizationFlowManagerDelegate> authorizationFlowManagerDelegate;

    @end
    ```

### <a name="configure-dependencies-for-android"></a>Android の依存関係を構成する

> [!NOTE]
> Android を対象としていない場合は、このセクションを省略できます。

1. エディターで**Graphtutorial/android/app/gradle**ファイルを開きます。
1. `defaultConfig`エントリを検索し、その中`defaultConfig`に次のプロパティを追加します。

    ```Gradle
    manifestPlaceholders = [
        appAuthRedirectScheme: 'graph-tutorial'
    ]
    ```

1. ファイルを保存します。 この`defaultConfig`エントリは、次のようになります。

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

## <a name="design-the-app"></a>アプリを設計する

アプリケーションは、[ナビゲーションドロアー](https://reactnavigation.org/docs/drawer-based-navigation.html)を使用して、さまざまなビュー間を移動します。 この手順では、アプリで使用される基本的なビューを作成し、ナビゲーションドロアーを実装します。

### <a name="create-views"></a>ビューを作成する

このセクションでは、[認証フロー](https://reactnavigation.org/docs/auth-flow.html)をサポートするためのアプリのビューを作成します。

1. **Graphtutorial**の「 **views**」という名前の新しいディレクトリを作成します。
1. **HomeScreen**という名前の新しいファイルを**graphtutorial/views**ディレクトリに作成します。 このファイルに次のコードを追加します。

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

1. **Graphtutorial .js**という名前の**graphtutorial/views**ディレクトリに新しいファイルを作成します。 このファイルに次のコードを追加します。

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

1. **SignInScreen**という名前の新しいファイルを**graphtutorial/views**ディレクトリに作成します。 このファイルに次のコードを追加します。

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

1. 「 **Authload Ingscreen**」という名前の**graphtutorial または views**ディレクトリに新しいファイルを作成します。 このファイルに次のコードを追加します。

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

### <a name="create-a-navigation-drawer"></a>ナビゲーションドロアーを作成する

このセクションでは、アプリケーションのメニューを作成し、画面間を移動するために反応するナビゲーションを使用するようにアプリケーションを更新します。

1. 「**メニュー**という名前の**graphtutorial**ディレクトリ」に新しいディレクトリを作成します。
1. 「 **Drawermenu**」という名前の**graphermenu**ディレクトリに新しいファイルを作成します。 このファイルに次のコードを追加します。

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

1. **Graphtutorial/app.config**ファイルを開き、内容全体を次のように置き換えます。

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
    ```

1. すべての変更を保存します。

1. エミュレーターにアプリケーションを再読み込みします。

アプリのメニューは、2つのフラグメント間を移動し、[**サインイン**] または [**サインアウト**] ボタンをタップすると、変更されます。

![Android 上のアプリケーションのスクリーンショット](./images/android-app-screens.png)

![IOS 上のアプリケーションのスクリーンショット](./images/ios-app-screens.png)

> [!NOTE]
> アプリケーションを非同期ストレージまたはコンポーネントの更新に関して実行するときに、警告が表示される場合があります。 このチュートリアルの目的のために、これらの警告を閉じることができます。
