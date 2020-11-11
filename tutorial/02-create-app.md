<!-- markdownlint-disable MD002 MD041 -->

最初に、新しい反応するネイティブプロジェクトを作成します。

1. プロジェクトを作成するディレクトリで、コマンドラインインターフェイス (CLI) を開きます。 次のコマンドを実行して、 [ネイティブ cli](https://github.com/facebook/react-native) ツールを実行し、新しい反応するネイティブプロジェクトを作成します。

    ```Shell
    npx react-native init GraphTutorial --template react-native-template-typescript
    ```

1. **省略可能:** プロジェクトを実行して、開発環境が正しく構成されていることを確認します。 CLI で、作成したばかりの **Graphtutorial** ディレクトリにディレクトリを変更し、次のいずれかのコマンドを実行します。

    - IOS の場合: `npx react-native run-ios`
    - Android の場合: Android エミュレーターのインスタンスを起動し、を実行します。 `npx react-native run-android`

## <a name="install-dependencies"></a>依存関係のインストール

に進む前に、後で使用する追加の依存関係をインストールします。

- アプリ内のビュー間のナビゲーションを処理するための[ナビゲーションの反応](https://reactnavigation.org)。
- ネイティブの[ジェスチャ](https://github.com/kmagiera/react-native-gesture-handler)処理に対応した、ネイティブの[安全な領域コンテキスト](https://github.com/th3rdwave/react-native-safe-area-context)、反応したネイティブ[画面](https://github.com/kmagiera/react-native-screens)、[反応-ネイティブの復元](https://github.com/kmagiera/react-native-reanimated)、およびマスクされた[表示](https://github.com/react-native-community/react-native-masked-view)に必要な操作を行います。
- UI のアイコンを提供する[ネイティブ要素](https://reactnativeelements.com/docs/)と、[ネイティブベクトルアイコン](https://github.com/oblador/react-native-vector-icons)を反応させる。
- 認証とトークンの管理を処理する[ネイティブアプリ](https://github.com/FormidableLabs/react-native-app-auth)認証を処理します。
- トークン用のストレージを提供するための[非同期ストレージ](https://react-native-async-storage.github.io/async-storage/docs/install)。
- [datetimepicker](https://github.com/react-native-datetimepicker/datetimepicker) は、日付と時刻の選択を UI に追加します。
- 日付と時刻の解析と比較を処理するには、[しばらくお待ち](https://momentjs.com)ください。
- windows のタイムゾーンを IANA 形式に変換するための[windows の iana](https://github.com/rubenillodo/windows-iana) 。
- [microsoft graph-](https://github.com/microsoftgraph/msgraph-sdk-javascript) microsoft graph に電話をかけるためのクライアントです。

1. 応答するネイティブプロジェクトのルートディレクトリで、CLI を開きます。
1. 次のコマンドを実行します。

    ```Shell
    npm install @react-navigation/native@5.8.8 @react-navigation/drawer@5.11.1 @react-navigation/stack@5.12.5
    npm install @react-native-community/masked-view@0.1.10 react-native-safe-area-context@3.1.8 windows-iana
    npm install react-native-reanimated@1.13.1 react-native-screens@2.14.0 @react-native-async-storage/async-storage@1.13.2
    npm install react-native-elements@2.3.2 react-native-vector-icons@7.1.0 react-native-gesture-handler@1.8.0
    npm install react-native-app-auth@6.0.1 moment@2.29.1 moment-timezone @microsoft/microsoft-graph-client@2.1.1
    npm install @react-native-community/datetimepicker@3.0.4
    npm install @microsoft/microsoft-graph-types --save-dev
    ```

### <a name="link-and-configure-dependencies-for-ios"></a>IOS の依存関係をリンクおよび構成する

> [!NOTE]
> IOS を対象としていない場合は、このセクションを省略できます。

1. **Graphtutorial/ios** ディレクトリで CLI を開きます。
1. 次のコマンドを実行します。

    ```Shell
    pod install
    ```

1. テキストエディターで **Graphtutorial/ios/graphtutorial/情報** ファイルを開きます。 ファイルの最終行の直前に次の行を追加し `</dict>` ます。

    ```xml
    <key>UIAppFonts</key>
    <array>
      <string>AntDesign.ttf</string>
      <string>Entypo.ttf</string>
      <string>EvilIcons.ttf</string>
      <string>Feather.ttf</string>
      <string>FontAwesome.ttf</string>
      <string>FontAwesome5_Brands.ttf</string>
      <string>FontAwesome5_Regular.ttf</string>
      <string>FontAwesome5_Solid.ttf</string>
      <string>Foundation.ttf</string>
      <string>Ionicons.ttf</string>
      <string>MaterialIcons.ttf</string>
      <string>MaterialCommunityIcons.ttf</string>
      <string>SimpleLineIcons.ttf</string>
      <string>Octicons.ttf</string>
      <string>Zocial.ttf</string>
    </array>
    ```

1. テキストエディターで、 **graphtutorial/ios/GraphTutorial/AppDelegate. .h** ファイルを開きます。 その内容を次のように置き換えます。

    :::code language="objc" source="../demo/GraphTutorial/ios/GraphTutorial/AppDelegate.h":::

### <a name="configure-dependencies-for-android"></a>Android の依存関係を構成する

> [!NOTE]
> Android を対象としていない場合は、このセクションを省略できます。

1. エディターで **Graphtutorial/android/app/gradle** ファイルを開きます。
1. エントリを検索し、その `defaultConfig` 中に次のプロパティを追加し `defaultConfig` ます。

    ```Gradle
    manifestPlaceholders = [
        appAuthRedirectScheme: 'graph-tutorial'
    ]
    ```

    この `defaultConfig` エントリは、次のようになります。

    :::code language="gradle" source="../demo/GraphTutorial/android/app/build.gradle" id="DefaultConfigSnippet":::

1. ファイルの末尾に次の行を追加します。

    ```Gradle
    apply from: "../../node_modules/react-native-vector-icons/fonts.gradle"
    ```

1. ファイルを保存します。

## <a name="design-the-app"></a>アプリを設計する

アプリケーションは、 [ナビゲーションドロアー](https://reactnavigation.org/docs/drawer-based-navigation.html) を使用して、さまざまなビュー間を移動します。 この手順では、アプリで使用される基本的なビューを作成し、ナビゲーションドロアーを実装します。

### <a name="create-views"></a>ビューを作成する

このセクションでは、 [認証フロー](https://reactnavigation.org/docs/auth-flow)をサポートするためのアプリのビューを作成します。

1. **Graphtutorial チュートリアル/index.js** を開いて、その他のステートメントの前に、次をファイルの先頭に追加し `import` ます。

    ```javascript
    import 'react-native-gesture-handler';
    ```

1. 「 **Authcontext** 」という名前の **graphtutorial** ディレクトリに新しいファイルを作成し、次のコードを追加します。

    :::code language="typescript" source="../demo/GraphTutorial/AuthContext.tsx" id="AuthContextSnippet":::

1. **UserContext** という名前の **graphtutorial** ディレクトリに新しいファイルを作成し、次のコードを追加します。

    :::code language="typescript" source="../demo/GraphTutorial/UserContext.tsx" id="UserContextSnippet":::

1. 「 **画面** 」という名前の「 **graphtutorial** 」ディレクトリに新しいディレクトリを作成します。
1. **HomeScreen** という名前の **graphtutorial または画面** ディレクトリに新しいファイルを作成します。 次のコードをファイルに追加します。

    :::code language="typescript" source="../demo/GraphTutorial/screens/HomeScreen.tsx" id="HomeScreenSnippet":::

1. **Calendarscreen** という名前の **graphtutorial/画面** ディレクトリに新しいファイルを作成します。 次のコードをファイルに追加します。

    ```typescript
    import React from 'react';
    import {
      Text,
      StyleSheet,
      View,
    } from 'react-native';
    import { createStackNavigator } from '@react-navigation/stack';

    const Stack = createStackNavigator();

    // Temporary placeholder view
    const CalendarComponent = () => (
      <View style={styles.container}>
        <Text>Calendar</Text>
      </View>
    );

    export default class CalendarScreen extends React.Component {

      render() {
        return (
          <Stack.Navigator>
            <Stack.Screen name='Calendar'
              component={ CalendarComponent }
              options={{
                headerShown: false
              }} />
          </Stack.Navigator>
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

1. **SignInScreen** という名前の **graphtutorial または画面** ディレクトリに新しいファイルを作成します。 次のコードをファイルに追加します。

    ```typescript
    // Adapted from https://reactnavigation.org/docs/auth-flow
    import React from 'react';
    import {
      Alert,
      Button,
      StyleSheet,
      View,
    } from 'react-native';
    import { ParamListBase } from '@react-navigation/native';
    import { StackNavigationProp } from '@react-navigation/stack'

    import { AuthContext } from '../AuthContext';

    type SignInProps = {
      navigation: StackNavigationProp<ParamListBase>;
    };

    export default class SignInScreen extends React.Component<SignInProps> {
      static contextType = AuthContext;

      _signInAsync = async () => {
        await this.context.signIn();
      };

      componentDidMount() {
        this.props.navigation.setOptions({
          title: 'Please sign in',
          headerShown: true
        });
      }

      render() {
        return (
          <View style={styles.container}>
            <Button title='Sign In' onPress={this._signInAsync}/>
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

1. 「 **Authload Ingscreen** 」という名前の **graphtutorial または画面** ディレクトリに新しいファイルを作成します。 次のコードをファイルに追加します。

    :::code language="typescript" source="../demo/GraphTutorial/screens/AuthLoadingScreen.tsx" id="AuthLoadingScreenSnippet":::

### <a name="create-a-navigation-drawer"></a>ナビゲーションドロアーを作成する

このセクションでは、アプリケーションのメニューを作成し、画面間を移動するために反応するナビゲーションを使用するようにアプリケーションを更新します。

1. 「 **メニュー** という名前の **graphtutorial** ディレクトリ」に新しいディレクトリを作成します。

1. 「 **Drawermenu** 」という名前の **graphermenu** ディレクトリに新しいファイルを作成します。 次のコードをファイルに追加します。

    ```typescript
    import React, { FC } from 'react';
    import {
      Alert,
      Image,
      StyleSheet,
      Text,
      View,
      ImageSourcePropType
    } from 'react-native';
    import {
      createDrawerNavigator,
      DrawerContentScrollView,
      DrawerItem,
      DrawerItemList,
      DrawerContentComponentProps
    } from '@react-navigation/drawer';
    import { ParamListBase } from '@react-navigation/native';
    import { StackNavigationProp } from '@react-navigation/stack'

    import { AuthContext } from '../AuthContext';
    import { UserContext } from '../UserContext';
    import HomeScreen from '../screens/HomeScreen';
    import CalendarScreen from '../screens/CalendarScreen';

    const Drawer = createDrawerNavigator();

    type CustomDrawerContentProps = DrawerContentComponentProps & {
      userName: string;
      userEmail: string;
      userPhoto: ImageSourcePropType;
      signOut: () => void;
    }

    type DrawerMenuProps = {
      navigation: StackNavigationProp<ParamListBase>;
    }

    const CustomDrawerContent: FC<CustomDrawerContentProps> = props => (
      <DrawerContentScrollView {...props}>
          <View style={styles.profileView}>
            <Image source={props.userPhoto}
              resizeMode='contain'
              style={styles.profilePhoto} />
            <Text style={styles.profileUserName}>{props.userName}</Text>
            <Text style={styles.profileEmail}>{props.userEmail}</Text>
          </View>
          <DrawerItemList {...props} />
          <DrawerItem label='Sign Out' onPress={props.signOut}/>
      </DrawerContentScrollView>
    );

    export default class DrawerMenuContent extends React.Component<DrawerMenuProps> {
      static contextType = AuthContext;

      state = {
        // TEMPORARY
        userLoading: true,
        userFirstName: 'Adele',
        userFullName: 'Adele Vance',
        userEmail: 'adelev@contoso.com',
        userTimeZone: 'UTC',
        userPhoto: require('../images/no-profile-pic.png')
      }

      _signOut = async () => {
        this.context.signOut();
      }

      async componentDidMount() {
        this.props.navigation.setOptions({
          headerShown: false,
        });
      }

      render() {
        const userLoaded = !this.state.userLoading;

        return (
          <UserContext.Provider value={this.state}>
            <Drawer.Navigator
              drawerType='front'
              screenOptions={{
                headerStyle: {
                  backgroundColor: '#276b80'
                },
                headerTintColor: 'white'
              }}
              drawerContent={props => (
                <CustomDrawerContent {...props}
                  userName={this.state.userFullName}
                  userEmail={this.state.userEmail}
                  userPhoto={this.state.userPhoto}
                  signOut={this._signOut} />
              )}>
              <Drawer.Screen name='Home'
                component={HomeScreen}
                options={{drawerLabel: 'Home', headerTitle: 'Welcome'}} />
              { userLoaded &&
                <Drawer.Screen name='Calendar'
                  component={CalendarScreen}
                  options={{drawerLabel: 'Calendar'}} />
              }
            </Drawer.Navigator>
          </UserContext.Provider>
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

1. **Graphtutorial** の「 **images** 」という名前の新しいディレクトリを作成します。
1. このディレクトリに **no-profile-pic.png** という名前の既定のプロファイルイメージを追加します。 好みのイメージを使用することも、 [このサンプルの](https://github.com/microsoftgraph/msgraph-training-react-native/blob/master/demo/GraphTutorial/images/no-profile-pic.png)イメージを使用することもできます。

1. **Graphtutorial またはアプリケーション tsx** ファイルを開き、内容全体を次のように置き換えます。

    ```typescript
    // Adapted from https://reactnavigation.org/docs/auth-flow
    import * as React from 'react';
    import { NavigationContainer, ParamListBase } from '@react-navigation/native';
    import { createStackNavigator, StackNavigationProp } from '@react-navigation/stack'

    import { AuthContext } from './AuthContext';
    import SignInScreen from './screens/SignInScreen';
    import DrawerMenuContent from './menus/DrawerMenu'
    import AuthLoadingScreen from './screens/AuthLoadingScreen';

    const Stack = createStackNavigator();

    type Props = {
      navigation: StackNavigationProp<ParamListBase>;
    };

    export default function App({ navigation }: Props) {
      const [state, dispatch] = React.useReducer(
        (prevState: any, action: any) => {
          switch (action.type) {
            case 'RESTORE_TOKEN':
              return {
                ...prevState,
                userToken: action.token,
                isLoading: false
              };
            case 'SIGN_IN':
              return {
                ...prevState,
                isSignOut: false,
                userToken: action.token
              }
            case 'SIGN_OUT':
              return {
                ...prevState,
                isSignOut: true,
                userToken: null
              }
          }
        },
        {
          isLoading: true,
          isSignOut: false,
          userToken: null
        }
      );

      React.useEffect(() => {
        const bootstrapAsync = async () => {
          let userToken = null;
          // TEMPORARY
          dispatch({ type: 'RESTORE_TOKEN', token: userToken });
        };

        bootstrapAsync();
      }, []);

      const authContext = React.useMemo(
        () => ({
          signIn: async () => {
            dispatch({ type: 'SIGN_IN', token: 'placeholder-token' });
          },
          signOut: async () => {
            dispatch({ type: 'SIGN_OUT' });
          }
        }),
        []
      );

      return (
        <AuthContext.Provider value={authContext}>
          <NavigationContainer>
            <Stack.Navigator>
              {state.isLoading ? (
                <Stack.Screen name="Loading" component={AuthLoadingScreen} />
              ) : state.userToken == null ? (
                <Stack.Screen name="SignIn" component={SignInScreen} />
              ) : (
                <Stack.Screen name="Main" component={DrawerMenuContent} />
              )}
            </Stack.Navigator>
          </NavigationContainer>
        </AuthContext.Provider>
      );
    }
    ```

1. すべての変更を保存します。

1. エミュレーターにアプリケーションを再読み込みします。

アプリのメニューは、2つのフラグメント間を移動し、[ **サインイン** ] または [ **サインアウト** ] ボタンをタップすると、変更されます。

![Android 上のアプリケーションのスクリーンショット](./images/android-app-screens.png)

![IOS 上のアプリケーションのスクリーンショット](./images/ios-app-screens.png)
