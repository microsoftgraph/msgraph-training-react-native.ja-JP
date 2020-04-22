<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="c3618-101">最初に、新しい反応するネイティブプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="c3618-101">Begin by creating a new React Native project.</span></span>

1. <span data-ttu-id="c3618-102">プロジェクトを作成するディレクトリで、コマンドラインインターフェイス (CLI) を開きます。</span><span class="sxs-lookup"><span data-stu-id="c3618-102">Open your command line interface (CLI) in a directory where you want to create the project.</span></span> <span data-ttu-id="c3618-103">次のコマンドを実行して、[ネイティブ cli](https://github.com/facebook/react-native)ツールを実行し、新しい反応するネイティブプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="c3618-103">Run the following command to run the [react-native-cli](https://github.com/facebook/react-native) tool and create a new React Native project.</span></span>

    ```Shell
    npx react-native init GraphTutorial --template react-native-template-typescript
    ```

1. <span data-ttu-id="c3618-104">**省略可能:** プロジェクトを実行して、開発環境が正しく構成されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c3618-104">**Optional:** Verify that your development environment is configured correctly by running the project.</span></span> <span data-ttu-id="c3618-105">CLI で、作成したばかりの**Graphtutorial**ディレクトリにディレクトリを変更し、次のいずれかのコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="c3618-105">In your CLI, change the directory to the **GraphTutorial** directory you just created, and run one of the following commands.</span></span>

    - <span data-ttu-id="c3618-106">IOS の場合:`npx react-native run-ios`</span><span class="sxs-lookup"><span data-stu-id="c3618-106">For iOS: `npx react-native run-ios`</span></span>
    - <span data-ttu-id="c3618-107">Android の場合: Android エミュレーターのインスタンスを起動し、を実行します。`npx react-native run-android`</span><span class="sxs-lookup"><span data-stu-id="c3618-107">For Android: Launch an Android emulator instance and run `npx react-native run-android`</span></span>

## <a name="install-dependencies"></a><span data-ttu-id="c3618-108">依存関係のインストール</span><span class="sxs-lookup"><span data-stu-id="c3618-108">Install dependencies</span></span>

<span data-ttu-id="c3618-109">に進む前に、後で使用する追加の依存関係をインストールします。</span><span class="sxs-lookup"><span data-stu-id="c3618-109">Before moving on, install some additional dependencies that you will use later.</span></span>

- <span data-ttu-id="c3618-110">アプリ内のビュー間のナビゲーションを処理するための[ナビゲーションの反応](https://reactnavigation.org)。</span><span class="sxs-lookup"><span data-stu-id="c3618-110">[react-navigation](https://reactnavigation.org) to handle navigation between views in the app.</span></span>
- <span data-ttu-id="c3618-111">ネイティブの[ジェスチャ](https://github.com/kmagiera/react-native-gesture-handler)処理に対応した、ネイティブの[安全な領域コンテキスト](https://github.com/th3rdwave/react-native-safe-area-context)、反応したネイティブ[画面](https://github.com/kmagiera/react-native-screens)、[反応-ネイティブの復元](https://github.com/kmagiera/react-native-reanimated)、およびマスクされた[表示](https://github.com/react-native-community/react-native-masked-view)に必要な操作を行います。</span><span class="sxs-lookup"><span data-stu-id="c3618-111">[react-native-gesture-handler](https://github.com/kmagiera/react-native-gesture-handler), [react-native-safe-area-context](https://github.com/th3rdwave/react-native-safe-area-context), [react-native-screens](https://github.com/kmagiera/react-native-screens), [react-native-reanimate](https://github.com/kmagiera/react-native-reanimated), and [masked-view](https://github.com/react-native-community/react-native-masked-view) required by react-navigation.</span></span>
- <span data-ttu-id="c3618-112">UI のアイコンを提供する[ネイティブ要素](https://react-native-training.github.io/react-native-elements/docs/getting_started.html)と、[ネイティブベクトルアイコン](https://github.com/oblador/react-native-vector-icons)を反応させる。</span><span class="sxs-lookup"><span data-stu-id="c3618-112">[react-native-elements](https://react-native-training.github.io/react-native-elements/docs/getting_started.html) and [react-native-vector-icons](https://github.com/oblador/react-native-vector-icons) to provide icons for the UI.</span></span>
- <span data-ttu-id="c3618-113">認証とトークンの管理を処理する[ネイティブアプリ](https://github.com/FormidableLabs/react-native-app-auth)認証を処理します。</span><span class="sxs-lookup"><span data-stu-id="c3618-113">[react-native-app-auth](https://github.com/FormidableLabs/react-native-app-auth) to handle authentication and token management.</span></span>
- <span data-ttu-id="c3618-114">トークン用のストレージを提供するための[非同期ストレージ](https://github.com/react-native-community/react-native-async-storage)。</span><span class="sxs-lookup"><span data-stu-id="c3618-114">[async-storage](https://github.com/react-native-community/react-native-async-storage) to provide storage for tokens.</span></span>
- <span data-ttu-id="c3618-115">日付と時刻の解析と比較を処理するには、[しばらくお待ち](https://momentjs.com)ください。</span><span class="sxs-lookup"><span data-stu-id="c3618-115">[moment](https://momentjs.com) to handle parsing and comparison of dates and times.</span></span>
- <span data-ttu-id="c3618-116">[microsoft graph-](https://github.com/microsoftgraph/msgraph-sdk-javascript) microsoft graph に電話をかけるためのクライアントです。</span><span class="sxs-lookup"><span data-stu-id="c3618-116">[microsoft-graph-client](https://github.com/microsoftgraph/msgraph-sdk-javascript) for making calls to the Microsoft Graph.</span></span>

1. <span data-ttu-id="c3618-117">応答するネイティブプロジェクトのルートディレクトリで、CLI を開きます。</span><span class="sxs-lookup"><span data-stu-id="c3618-117">Open your CLI in the root directory of your React Native project.</span></span>
1. <span data-ttu-id="c3618-118">次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="c3618-118">Run the following command.</span></span>

    ```Shell
    npm install @react-navigation/native@5.1.5 @react-navigation/drawer@5.4.1 @react-navigation/stack@5.2.10
    npm install @react-native-community/masked-view@0.1.7 react-native-safe-area-context@0.7.3
    npm install react-native-reanimated@1.8.0 react-native-screens@2.4.0 @react-native-community/async-storage@1.9.0
    npm install react-native-elements@1.2.7 react-native-vector-icons@6.6.0 react-native-gesture-handler@1.6.1
    npm install react-native-app-auth@5.1.1 moment@2.24.0 @microsoft/microsoft-graph-client@2.0.0
    ```

### <a name="link-and-configure-dependencies-for-ios"></a><span data-ttu-id="c3618-119">IOS の依存関係をリンクおよび構成する</span><span class="sxs-lookup"><span data-stu-id="c3618-119">Link and configure dependencies for iOS</span></span>

> [!NOTE]
> <span data-ttu-id="c3618-120">IOS を対象としていない場合は、このセクションを省略できます。</span><span class="sxs-lookup"><span data-stu-id="c3618-120">If you are not targeting iOS, you can skip this section.</span></span>

1. <span data-ttu-id="c3618-121">**Graphtutorial/ios**ディレクトリで CLI を開きます。</span><span class="sxs-lookup"><span data-stu-id="c3618-121">Open your CLI in the **GraphTutorial/ios** directory.</span></span>
1. <span data-ttu-id="c3618-122">次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="c3618-122">Run the following command.</span></span>

    ```Shell
    pod install
    ```

1. <span data-ttu-id="c3618-123">テキストエディターで**Graphtutorial/ios/graphtutorial/情報**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="c3618-123">Open the **GraphTutorial/ios/GraphTutorial/Info.plist** file in a text editor.</span></span> <span data-ttu-id="c3618-124">ファイルの最終`</dict>`行の直前に次の行を追加します。</span><span class="sxs-lookup"><span data-stu-id="c3618-124">Add the following just before the last `</dict>` line in the file.</span></span>

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

1. <span data-ttu-id="c3618-125">テキストエディターで、 **graphtutorial/ios/GraphTutorial/AppDelegate. .h**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="c3618-125">Open the **GraphTutorial/ios/GraphTutorial/AppDelegate.h** file in a text editor.</span></span> <span data-ttu-id="c3618-126">その内容を次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c3618-126">Replace its contents with the following.</span></span>

    :::code language="objc" source="../demo/GraphTutorial/ios/GraphTutorial/AppDelegate.h":::

### <a name="configure-dependencies-for-android"></a><span data-ttu-id="c3618-127">Android の依存関係を構成する</span><span class="sxs-lookup"><span data-stu-id="c3618-127">Configure dependencies for Android</span></span>

> [!NOTE]
> <span data-ttu-id="c3618-128">Android を対象としていない場合は、このセクションを省略できます。</span><span class="sxs-lookup"><span data-stu-id="c3618-128">If you are not targeting Android, you can skip this section.</span></span>

1. <span data-ttu-id="c3618-129">エディターで**Graphtutorial/android/app/gradle**ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="c3618-129">Open the **GraphTutorial/android/app/build.gradle** file in an editor.</span></span>
1. <span data-ttu-id="c3618-130">`defaultConfig`エントリを検索し、その中`defaultConfig`に次のプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="c3618-130">Locate the `defaultConfig` entry and add the following property inside `defaultConfig`.</span></span>

    ```Gradle
    manifestPlaceholders = [
        appAuthRedirectScheme: 'graph-tutorial'
    ]
    ```

    <span data-ttu-id="c3618-131">この`defaultConfig`エントリは、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="c3618-131">The `defaultConfig` entry should look similar to the following.</span></span>

    :::code language="gradle" source="../demo/GraphTutorial/android/app/build.gradle" id="DefaultConfigSnippet":::

1. <span data-ttu-id="c3618-132">ファイルの末尾に次の行を追加します。</span><span class="sxs-lookup"><span data-stu-id="c3618-132">Add the following line to the end of the file.</span></span>

    ```Gradle
    apply from: "../../node_modules/react-native-vector-icons/fonts.gradle"
    ```

1. <span data-ttu-id="c3618-133">ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="c3618-133">Save the file.</span></span>

## <a name="design-the-app"></a><span data-ttu-id="c3618-134">アプリを設計する</span><span class="sxs-lookup"><span data-stu-id="c3618-134">Design the app</span></span>

<span data-ttu-id="c3618-135">アプリケーションは、[ナビゲーションドロアー](https://reactnavigation.org/docs/drawer-based-navigation.html)を使用して、さまざまなビュー間を移動します。</span><span class="sxs-lookup"><span data-stu-id="c3618-135">The application will use a [navigation drawer](https://reactnavigation.org/docs/drawer-based-navigation.html) to navigate between different views.</span></span> <span data-ttu-id="c3618-136">この手順では、アプリで使用される基本的なビューを作成し、ナビゲーションドロアーを実装します。</span><span class="sxs-lookup"><span data-stu-id="c3618-136">In this step you will create the basic views used by the app and implement the navigation drawer.</span></span>

### <a name="create-views"></a><span data-ttu-id="c3618-137">ビューを作成する</span><span class="sxs-lookup"><span data-stu-id="c3618-137">Create views</span></span>

<span data-ttu-id="c3618-138">このセクションでは、[認証フロー](https://reactnavigation.org/docs/auth-flow)をサポートするためのアプリのビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="c3618-138">In this section you will create the views for the app to support an [authentication flow](https://reactnavigation.org/docs/auth-flow).</span></span>

1. <span data-ttu-id="c3618-139">**Graphtutorial または index .js**を開き、ファイルの先頭に次の`import`ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="c3618-139">Open **GraphTutorial/index.js** and add the following to the top of the file, before any other `import` statements.</span></span>

    ```javascript
    import 'react-native-gesture-handler';
    ```

1. <span data-ttu-id="c3618-140">「**画面**」という名前の「 **graphtutorial** 」ディレクトリに新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="c3618-140">Create a new directory in the **GraphTutorial** directory named **screens**.</span></span>
1. <span data-ttu-id="c3618-141">**HomeScreen**という名前の**graphtutorial または画面**ディレクトリに新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="c3618-141">Create a new file in the **GraphTutorial/screens** directory named **HomeScreen.tsx**.</span></span> <span data-ttu-id="c3618-142">このファイルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="c3618-142">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="c3618-143">**Calendarscreen**という名前の**graphtutorial/画面**ディレクトリに新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="c3618-143">Create a new file in the **GraphTutorial/screens** directory named **CalendarScreen.tsx**.</span></span> <span data-ttu-id="c3618-144">このファイルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="c3618-144">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="c3618-145">**SignInScreen**という名前の**graphtutorial または画面**ディレクトリに新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="c3618-145">Create a new file in the **GraphTutorial/screens** directory named **SignInScreen.tsx**.</span></span> <span data-ttu-id="c3618-146">このファイルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="c3618-146">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="c3618-147">「 **Authload Ingscreen**」という名前の**graphtutorial または画面**ディレクトリに新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="c3618-147">Create a new file in the **GraphTutorial/screens** directory named **AuthLoadingScreen.tsx**.</span></span> <span data-ttu-id="c3618-148">このファイルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="c3618-148">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/AuthLoadingScreen.tsx" id="AuthLoadingScreenSnippet":::

### <a name="create-a-navigation-drawer"></a><span data-ttu-id="c3618-149">ナビゲーションドロアーを作成する</span><span class="sxs-lookup"><span data-stu-id="c3618-149">Create a navigation drawer</span></span>

<span data-ttu-id="c3618-150">このセクションでは、アプリケーションのメニューを作成し、画面間を移動するために反応するナビゲーションを使用するようにアプリケーションを更新します。</span><span class="sxs-lookup"><span data-stu-id="c3618-150">In this section you will create a menu for the application, and update the application to use react-navigation to move between screens.</span></span>

1. <span data-ttu-id="c3618-151">「**メニュー**という名前の**graphtutorial**ディレクトリ」に新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="c3618-151">Create a new directory in the **GraphTutorial** directory named **menus**.</span></span>
1. <span data-ttu-id="c3618-152">「 **Headercomponents**」という名前の**graphtutorial/メニュー**ディレクトリに、新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="c3618-152">Create a new file in the **GraphTutorial/menus** directory named **HeaderComponents.tsx**.</span></span> <span data-ttu-id="c3618-153">このファイルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="c3618-153">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/menus/HeaderComponents.tsx" id="HeaderComponentSnippet":::

1. <span data-ttu-id="c3618-154">「 **Drawermenu**」という名前の**graphermenu**ディレクトリに新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="c3618-154">Create a new file in the **GraphTutorial/menus** directory named **DrawerMenu.tsx**.</span></span> <span data-ttu-id="c3618-155">このファイルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="c3618-155">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="c3618-156">**Graphtutorial**の「 **images**」という名前の新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="c3618-156">Create a new directory in the **GraphTutorial** directory named **images**.</span></span>
1. <span data-ttu-id="c3618-157">このディレクトリに**no-profile-pic**という名前の既定のプロファイルイメージを追加します。</span><span class="sxs-lookup"><span data-stu-id="c3618-157">Add a default profile image named **no-profile-pic.png** in this directory.</span></span> <span data-ttu-id="c3618-158">好みのイメージを使用することも、[このサンプルの](https://github.com/microsoftgraph/msgraph-training-react-native/blob/master/demo/GraphTutorial/images/no-profile-pic.png)イメージを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="c3618-158">You can use any image you like, or use [the one from this sample](https://github.com/microsoftgraph/msgraph-training-react-native/blob/master/demo/GraphTutorial/images/no-profile-pic.png).</span></span>

1. <span data-ttu-id="c3618-159">**Graphtutorial またはアプリケーション tsx**ファイルを開き、内容全体を次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c3618-159">Open the **GraphTutorial/App.tsx** file and replace the entire contents with the following.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/App.tsx" id="AppSnippet":::

1. <span data-ttu-id="c3618-160">すべての変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="c3618-160">Save all of your changes.</span></span>

1. <span data-ttu-id="c3618-161">エミュレーターにアプリケーションを再読み込みします。</span><span class="sxs-lookup"><span data-stu-id="c3618-161">Reload the application in your emulator.</span></span>

<span data-ttu-id="c3618-162">アプリのメニューは、2つのフラグメント間を移動し、[**サインイン**] または [**サインアウト**] ボタンをタップすると、変更されます。</span><span class="sxs-lookup"><span data-stu-id="c3618-162">The app's menu should work to navigate between the two fragments and change when you tap the **Sign in** or **Sign out** buttons.</span></span>

![Android 上のアプリケーションのスクリーンショット](./images/android-app-screens.png)

![IOS 上のアプリケーションのスクリーンショット](./images/ios-app-screens.png)
