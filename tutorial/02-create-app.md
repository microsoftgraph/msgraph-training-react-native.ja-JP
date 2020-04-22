<!-- markdownlint-disable MD002 MD041 -->

最初に、新しい反応するネイティブプロジェクトを作成します。

1. プロジェクトを作成するディレクトリで、コマンドラインインターフェイス (CLI) を開きます。 次のコマンドを実行して、[ネイティブ cli](https://github.com/facebook/react-native)ツールを実行し、新しい反応するネイティブプロジェクトを作成します。

    ```Shell
    npx react-native init GraphTutorial --template react-native-template-typescript
    ```

1. **省略可能:** プロジェクトを実行して、開発環境が正しく構成されていることを確認します。 CLI で、作成したばかりの**Graphtutorial**ディレクトリにディレクトリを変更し、次のいずれかのコマンドを実行します。

    - IOS の場合:`npx react-native run-ios`
    - Android の場合: Android エミュレーターのインスタンスを起動し、を実行します。`npx react-native run-android`

## <a name="install-dependencies"></a>依存関係のインストール

に進む前に、後で使用する追加の依存関係をインストールします。

- アプリ内のビュー間のナビゲーションを処理するための[ナビゲーションの反応](https://reactnavigation.org)。
- ネイティブの[ジェスチャ](https://github.com/kmagiera/react-native-gesture-handler)処理に対応した、ネイティブの[安全な領域コンテキスト](https://github.com/th3rdwave/react-native-safe-area-context)、反応したネイティブ[画面](https://github.com/kmagiera/react-native-screens)、[反応-ネイティブの復元](https://github.com/kmagiera/react-native-reanimated)、およびマスクされた[表示](https://github.com/react-native-community/react-native-masked-view)に必要な操作を行います。
- UI のアイコンを提供する[ネイティブ要素](https://react-native-training.github.io/react-native-elements/docs/getting_started.html)と、[ネイティブベクトルアイコン](https://github.com/oblador/react-native-vector-icons)を反応させる。
- 認証とトークンの管理を処理する[ネイティブアプリ](https://github.com/FormidableLabs/react-native-app-auth)認証を処理します。
- トークン用のストレージを提供するための[非同期ストレージ](https://github.com/react-native-community/react-native-async-storage)。
- 日付と時刻の解析と比較を処理するには、[しばらくお待ち](https://momentjs.com)ください。
- [microsoft graph-](https://github.com/microsoftgraph/msgraph-sdk-javascript) microsoft graph に電話をかけるためのクライアントです。

1. 応答するネイティブプロジェクトのルートディレクトリで、CLI を開きます。
1. 次のコマンドを実行します。

    ```Shell
    npm install @react-navigation/native@5.1.5 @react-navigation/drawer@5.4.1 @react-navigation/stack@5.2.10
    npm install @react-native-community/masked-view@0.1.7 react-native-safe-area-context@0.7.3
    npm install react-native-reanimated@1.8.0 react-native-screens@2.4.0 @react-native-community/async-storage@1.9.0
    npm install react-native-elements@1.2.7 react-native-vector-icons@6.6.0 react-native-gesture-handler@1.6.1
    npm install react-native-app-auth@5.1.1 moment@2.24.0 @microsoft/microsoft-graph-client@2.0.0
    ```

### <a name="link-and-configure-dependencies-for-ios"></a>IOS の依存関係をリンクおよび構成する

> [!NOTE]
> IOS を対象としていない場合は、このセクションを省略できます。

1. **Graphtutorial/ios**ディレクトリで CLI を開きます。
1. 次のコマンドを実行します。

    ```Shell
    pod install
    ```

1. テキストエディターで**Graphtutorial/ios/graphtutorial/情報**ファイルを開きます。 ファイルの最終`</dict>`行の直前に次の行を追加します。

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

1. テキストエディターで、 **graphtutorial/ios/GraphTutorial/AppDelegate. .h**ファイルを開きます。 その内容を次のように置き換えます。

    :::code language="objc" source="../demo/GraphTutorial/ios/GraphTutorial/AppDelegate.h":::

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

    この`defaultConfig`エントリは、次のようになります。

    :::code language="gradle" source="../demo/GraphTutorial/android/app/build.gradle" id="DefaultConfigSnippet":::

1. ファイルの末尾に次の行を追加します。

    ```Gradle
    apply from: "../../node_modules/react-native-vector-icons/fonts.gradle"
    ```

1. ファイルを保存します。

## <a name="design-the-app"></a>アプリを設計する

アプリケーションは、[ナビゲーションドロアー](https://reactnavigation.org/docs/drawer-based-navigation.html)を使用して、さまざまなビュー間を移動します。 この手順では、アプリで使用される基本的なビューを作成し、ナビゲーションドロアーを実装します。

### <a name="create-views"></a>ビューを作成する

このセクションでは、[認証フロー](https://reactnavigation.org/docs/auth-flow)をサポートするためのアプリのビューを作成します。

1. **Graphtutorial または index .js**を開き、ファイルの先頭に次の`import`ステートメントを追加します。

    ```javascript
    import 'react-native-gesture-handler';
    ```

1. 「**画面**」という名前の「 **graphtutorial** 」ディレクトリに新しいディレクトリを作成します。
1. **HomeScreen**という名前の**graphtutorial または画面**ディレクトリに新しいファイルを作成します。 このファイルに次のコードを追加します。

    ```typescript
    import React from 'react';
    import {
      ActivityIndicator,
      Alert,
      StyleSheet,
      Text,
      View,
    } from 'react-native';
    import { createStackNavigator } from '@react-navigation/stack';
    import { DrawerToggle, headerOptions } from '../menus/HeaderComponents';

    const Stack = createStackNavigator();
    const UserState = React.createContext({userLoading: true, userName: ''});

    type HomeScreenState = {
      userLoading: boolean;
      userName: string;
    }

    const HomeComponent = () => {
      const userState = React.useContext(UserState);

      return (
        <View style={styles.container}>
          <ActivityIndicator animating={userState.userLoading} size='large' />
          {userState.userLoading ? null: <Text>Hello {userState.userName}!</Text>}
        </View>
      );
    }

    export default class HomeScreen extends React.Component {

      state: HomeScreenState = {
        userLoading: true,
        userName: ''
      };

      render() {
        return (
          <UserState.Provider value={this.state}>
              <Stack.Navigator screenOptions={headerOptions}>
                <Stack.Screen name='Home'
                  component={HomeComponent}
                  options={{
                    title: 'Welcome',
                    headerLeft: () => <DrawerToggle/>
                  }} />
              </Stack.Navigator>
          </UserState.Provider>
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

1. **Calendarscreen**という名前の**graphtutorial/画面**ディレクトリに新しいファイルを作成します。 このファイルに次のコードを追加します。

    ```typescript
    import React from 'react';
    import {
      Text,
      StyleSheet,
      View,
    } from 'react-native';
    import { createStackNavigator } from '@react-navigation/stack';
    import { DrawerToggle, headerOptions } from '../menus/HeaderComponents';

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
          <Stack.Navigator screenOptions={ headerOptions }>
            <Stack.Screen name='Calendar'
              component={ CalendarComponent }
              options={{
                title: 'Calendar',
                headerLeft: () => <DrawerToggle/>
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

1. **SignInScreen**という名前の**graphtutorial または画面**ディレクトリに新しいファイルを作成します。 このファイルに次のコードを追加します。

    ```typescript
    // Adapted from https://reactnavigation.org/docs/auth-flow
    import React from 'react';
    import {
      Alert,
      Button,
      StyleSheet,
      View,
    } from 'react-native';
    import { NavigationContext } from '@react-navigation/native';

    export default class SignInScreen extends React.Component {
      static contextType = NavigationContext;

      static navigationOptions = {
        title: 'Please sign in',
      };

      _signInAsync = async () => {
        const navigation = this.context;

        // TEMPORARY
        navigation.reset({
          index: 0,
          routes: [ { name: 'Main' } ]
        });
      };

      render() {
        const navigation = this.context;
        navigation.setOptions({
          title: 'Please sign in',
          headerShown: true
        });

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

1. 「 **Authload Ingscreen**」という名前の**graphtutorial または画面**ディレクトリに新しいファイルを作成します。 このファイルに次のコードを追加します。

    :::code language="typescript" source="../demo/GraphTutorial/screens/AuthLoadingScreen.tsx" id="AuthLoadingScreenSnippet":::

### <a name="create-a-navigation-drawer"></a>ナビゲーションドロアーを作成する

このセクションでは、アプリケーションのメニューを作成し、画面間を移動するために反応するナビゲーションを使用するようにアプリケーションを更新します。

1. 「**メニュー**という名前の**graphtutorial**ディレクトリ」に新しいディレクトリを作成します。
1. 「 **Headercomponents**」という名前の**graphtutorial/メニュー**ディレクトリに、新しいファイルを作成します。 このファイルに次のコードを追加します。

    :::code language="typescript" source="../demo/GraphTutorial/menus/HeaderComponents.tsx" id="HeaderComponentSnippet":::

1. 「 **Drawermenu**」という名前の**graphermenu**ディレクトリに新しいファイルを作成します。 このファイルに次のコードを追加します。

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
    import { NavigationContext } from '@react-navigation/native';

    import HomeScreen from '../screens/HomeScreen';
    import CalendarScreen from '../screens/CalendarScreen';

    const Drawer = createDrawerNavigator();

    type CustomDrawerContentProps = DrawerContentComponentProps & {
      userName: string;
      userEmail: string;
      userPhoto: ImageSourcePropType;
      signOut: () => void;
    }

    type DrawerMenuState = {
      userName: string;
      userEmail: string;
      userPhoto: ImageSourcePropType;
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

    export default class DrawerMenuContent extends React.Component {
      static contextType = NavigationContext;

      state: DrawerMenuState = {
        // TEMPORARY
        userName: 'Adele Vance',
        userEmail: 'adelev@contoso.com',
        userPhoto: require('../images/no-profile-pic.png')
      }

      _signOut = async () => {
        const navigation = this.context;
        // Sign out
        // TEMPORARY
        navigation.reset({
          index: 0,
          routes: [{ name: 'SignIn' }]
        });
      }

      render() {
        const navigation = this.context;
        navigation.setOptions({
          headerShown: false,
        });

        return (
          <Drawer.Navigator
            drawerType='front'
            drawerContent={props => (
              <CustomDrawerContent {...props}
                userName={this.state.userName}
                userEmail={this.state.userEmail}
                userPhoto={this.state.userPhoto}
                signOut={this._signOut} />
            )}>
            <Drawer.Screen name='Home'
              component={HomeScreen}
              options={{drawerLabel: 'Home'}} />
            <Drawer.Screen name='Calendar'
              component={CalendarScreen}
              options={{drawerLabel: 'Calendar'}} />
          </Drawer.Navigator>
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

1. **Graphtutorial**の「 **images**」という名前の新しいディレクトリを作成します。
1. このディレクトリに**no-profile-pic**という名前の既定のプロファイルイメージを追加します。 好みのイメージを使用することも、[このサンプルの](https://github.com/microsoftgraph/msgraph-training-react-native/blob/master/demo/GraphTutorial/images/no-profile-pic.png)イメージを使用することもできます。

1. **Graphtutorial またはアプリケーション tsx**ファイルを開き、内容全体を次のように置き換えます。

    :::code language="typescript" source="../demo/GraphTutorial/App.tsx" id="AppSnippet":::

1. すべての変更を保存します。

1. エミュレーターにアプリケーションを再読み込みします。

アプリのメニューは、2つのフラグメント間を移動し、[**サインイン**] または [**サインアウト**] ボタンをタップすると、変更されます。

![Android 上のアプリケーションのスクリーンショット](./images/android-app-screens.png)

![IOS 上のアプリケーションのスクリーンショット](./images/ios-app-screens.png)
