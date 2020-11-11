<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="cf887-101">最初に、新しい反応するネイティブプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="cf887-101">Begin by creating a new React Native project.</span></span>

1. <span data-ttu-id="cf887-102">プロジェクトを作成するディレクトリで、コマンドラインインターフェイス (CLI) を開きます。</span><span class="sxs-lookup"><span data-stu-id="cf887-102">Open your command line interface (CLI) in a directory where you want to create the project.</span></span> <span data-ttu-id="cf887-103">次のコマンドを実行して、 [ネイティブ cli](https://github.com/facebook/react-native) ツールを実行し、新しい反応するネイティブプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="cf887-103">Run the following command to run the [react-native-cli](https://github.com/facebook/react-native) tool and create a new React Native project.</span></span>

    ```Shell
    npx react-native init GraphTutorial --template react-native-template-typescript
    ```

1. <span data-ttu-id="cf887-104">**省略可能:** プロジェクトを実行して、開発環境が正しく構成されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="cf887-104">**Optional:** Verify that your development environment is configured correctly by running the project.</span></span> <span data-ttu-id="cf887-105">CLI で、作成したばかりの **Graphtutorial** ディレクトリにディレクトリを変更し、次のいずれかのコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="cf887-105">In your CLI, change the directory to the **GraphTutorial** directory you just created, and run one of the following commands.</span></span>

    - <span data-ttu-id="cf887-106">IOS の場合: `npx react-native run-ios`</span><span class="sxs-lookup"><span data-stu-id="cf887-106">For iOS: `npx react-native run-ios`</span></span>
    - <span data-ttu-id="cf887-107">Android の場合: Android エミュレーターのインスタンスを起動し、を実行します。 `npx react-native run-android`</span><span class="sxs-lookup"><span data-stu-id="cf887-107">For Android: Launch an Android emulator instance and run `npx react-native run-android`</span></span>

## <a name="install-dependencies"></a><span data-ttu-id="cf887-108">依存関係のインストール</span><span class="sxs-lookup"><span data-stu-id="cf887-108">Install dependencies</span></span>

<span data-ttu-id="cf887-109">に進む前に、後で使用する追加の依存関係をインストールします。</span><span class="sxs-lookup"><span data-stu-id="cf887-109">Before moving on, install some additional dependencies that you will use later.</span></span>

- <span data-ttu-id="cf887-110">アプリ内のビュー間のナビゲーションを処理するための[ナビゲーションの反応](https://reactnavigation.org)。</span><span class="sxs-lookup"><span data-stu-id="cf887-110">[react-navigation](https://reactnavigation.org) to handle navigation between views in the app.</span></span>
- <span data-ttu-id="cf887-111">ネイティブの[ジェスチャ](https://github.com/kmagiera/react-native-gesture-handler)処理に対応した、ネイティブの[安全な領域コンテキスト](https://github.com/th3rdwave/react-native-safe-area-context)、反応したネイティブ[画面](https://github.com/kmagiera/react-native-screens)、[反応-ネイティブの復元](https://github.com/kmagiera/react-native-reanimated)、およびマスクされた[表示](https://github.com/react-native-community/react-native-masked-view)に必要な操作を行います。</span><span class="sxs-lookup"><span data-stu-id="cf887-111">[react-native-gesture-handler](https://github.com/kmagiera/react-native-gesture-handler), [react-native-safe-area-context](https://github.com/th3rdwave/react-native-safe-area-context), [react-native-screens](https://github.com/kmagiera/react-native-screens), [react-native-reanimate](https://github.com/kmagiera/react-native-reanimated), and [masked-view](https://github.com/react-native-community/react-native-masked-view) required by react-navigation.</span></span>
- <span data-ttu-id="cf887-112">UI のアイコンを提供する[ネイティブ要素](https://reactnativeelements.com/docs/)と、[ネイティブベクトルアイコン](https://github.com/oblador/react-native-vector-icons)を反応させる。</span><span class="sxs-lookup"><span data-stu-id="cf887-112">[react-native-elements](https://reactnativeelements.com/docs/) and [react-native-vector-icons](https://github.com/oblador/react-native-vector-icons) to provide icons for the UI.</span></span>
- <span data-ttu-id="cf887-113">認証とトークンの管理を処理する[ネイティブアプリ](https://github.com/FormidableLabs/react-native-app-auth)認証を処理します。</span><span class="sxs-lookup"><span data-stu-id="cf887-113">[react-native-app-auth](https://github.com/FormidableLabs/react-native-app-auth) to handle authentication and token management.</span></span>
- <span data-ttu-id="cf887-114">トークン用のストレージを提供するための[非同期ストレージ](https://react-native-async-storage.github.io/async-storage/docs/install)。</span><span class="sxs-lookup"><span data-stu-id="cf887-114">[async-storage](https://react-native-async-storage.github.io/async-storage/docs/install) to provide storage for tokens.</span></span>
- <span data-ttu-id="cf887-115">[datetimepicker](https://github.com/react-native-datetimepicker/datetimepicker) は、日付と時刻の選択を UI に追加します。</span><span class="sxs-lookup"><span data-stu-id="cf887-115">[datetimepicker](https://github.com/react-native-datetimepicker/datetimepicker) to add date and time pickers to the UI.</span></span>
- <span data-ttu-id="cf887-116">日付と時刻の解析と比較を処理するには、[しばらくお待ち](https://momentjs.com)ください。</span><span class="sxs-lookup"><span data-stu-id="cf887-116">[moment](https://momentjs.com) to handle parsing and comparison of dates and times.</span></span>
- <span data-ttu-id="cf887-117">windows のタイムゾーンを IANA 形式に変換するための[windows の iana](https://github.com/rubenillodo/windows-iana) 。</span><span class="sxs-lookup"><span data-stu-id="cf887-117">[windows-iana](https://github.com/rubenillodo/windows-iana) for translating Windows time zones to IANA format.</span></span>
- <span data-ttu-id="cf887-118">[microsoft graph-](https://github.com/microsoftgraph/msgraph-sdk-javascript) microsoft graph に電話をかけるためのクライアントです。</span><span class="sxs-lookup"><span data-stu-id="cf887-118">[microsoft-graph-client](https://github.com/microsoftgraph/msgraph-sdk-javascript) for making calls to the Microsoft Graph.</span></span>

1. <span data-ttu-id="cf887-119">応答するネイティブプロジェクトのルートディレクトリで、CLI を開きます。</span><span class="sxs-lookup"><span data-stu-id="cf887-119">Open your CLI in the root directory of your React Native project.</span></span>
1. <span data-ttu-id="cf887-120">次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="cf887-120">Run the following command.</span></span>

    ```Shell
    npm install @react-navigation/native@5.8.8 @react-navigation/drawer@5.11.1 @react-navigation/stack@5.12.5
    npm install @react-native-community/masked-view@0.1.10 react-native-safe-area-context@3.1.8 windows-iana
    npm install react-native-reanimated@1.13.1 react-native-screens@2.14.0 @react-native-async-storage/async-storage@1.13.2
    npm install react-native-elements@2.3.2 react-native-vector-icons@7.1.0 react-native-gesture-handler@1.8.0
    npm install react-native-app-auth@6.0.1 moment@2.29.1 moment-timezone @microsoft/microsoft-graph-client@2.1.1
    npm install @react-native-community/datetimepicker@3.0.4
    npm install @microsoft/microsoft-graph-types --save-dev
    ```

### <a name="link-and-configure-dependencies-for-ios"></a><span data-ttu-id="cf887-121">IOS の依存関係をリンクおよび構成する</span><span class="sxs-lookup"><span data-stu-id="cf887-121">Link and configure dependencies for iOS</span></span>

> [!NOTE]
> <span data-ttu-id="cf887-122">IOS を対象としていない場合は、このセクションを省略できます。</span><span class="sxs-lookup"><span data-stu-id="cf887-122">If you are not targeting iOS, you can skip this section.</span></span>

1. <span data-ttu-id="cf887-123">**Graphtutorial/ios** ディレクトリで CLI を開きます。</span><span class="sxs-lookup"><span data-stu-id="cf887-123">Open your CLI in the **GraphTutorial/ios** directory.</span></span>
1. <span data-ttu-id="cf887-124">次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="cf887-124">Run the following command.</span></span>

    ```Shell
    pod install
    ```

1. <span data-ttu-id="cf887-125">テキストエディターで **Graphtutorial/ios/graphtutorial/情報** ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="cf887-125">Open the **GraphTutorial/ios/GraphTutorial/Info.plist** file in a text editor.</span></span> <span data-ttu-id="cf887-126">ファイルの最終行の直前に次の行を追加し `</dict>` ます。</span><span class="sxs-lookup"><span data-stu-id="cf887-126">Add the following just before the last `</dict>` line in the file.</span></span>

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

1. <span data-ttu-id="cf887-127">テキストエディターで、 **graphtutorial/ios/GraphTutorial/AppDelegate. .h** ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="cf887-127">Open the **GraphTutorial/ios/GraphTutorial/AppDelegate.h** file in a text editor.</span></span> <span data-ttu-id="cf887-128">その内容を次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="cf887-128">Replace its contents with the following.</span></span>

    :::code language="objc" source="../demo/GraphTutorial/ios/GraphTutorial/AppDelegate.h":::

### <a name="configure-dependencies-for-android"></a><span data-ttu-id="cf887-129">Android の依存関係を構成する</span><span class="sxs-lookup"><span data-stu-id="cf887-129">Configure dependencies for Android</span></span>

> [!NOTE]
> <span data-ttu-id="cf887-130">Android を対象としていない場合は、このセクションを省略できます。</span><span class="sxs-lookup"><span data-stu-id="cf887-130">If you are not targeting Android, you can skip this section.</span></span>

1. <span data-ttu-id="cf887-131">エディターで **Graphtutorial/android/app/gradle** ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="cf887-131">Open the **GraphTutorial/android/app/build.gradle** file in an editor.</span></span>
1. <span data-ttu-id="cf887-132">エントリを検索し、その `defaultConfig` 中に次のプロパティを追加し `defaultConfig` ます。</span><span class="sxs-lookup"><span data-stu-id="cf887-132">Locate the `defaultConfig` entry and add the following property inside `defaultConfig`.</span></span>

    ```Gradle
    manifestPlaceholders = [
        appAuthRedirectScheme: 'graph-tutorial'
    ]
    ```

    <span data-ttu-id="cf887-133">この `defaultConfig` エントリは、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="cf887-133">The `defaultConfig` entry should look similar to the following.</span></span>

    :::code language="gradle" source="../demo/GraphTutorial/android/app/build.gradle" id="DefaultConfigSnippet":::

1. <span data-ttu-id="cf887-134">ファイルの末尾に次の行を追加します。</span><span class="sxs-lookup"><span data-stu-id="cf887-134">Add the following line to the end of the file.</span></span>

    ```Gradle
    apply from: "../../node_modules/react-native-vector-icons/fonts.gradle"
    ```

1. <span data-ttu-id="cf887-135">ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="cf887-135">Save the file.</span></span>

## <a name="design-the-app"></a><span data-ttu-id="cf887-136">アプリを設計する</span><span class="sxs-lookup"><span data-stu-id="cf887-136">Design the app</span></span>

<span data-ttu-id="cf887-137">アプリケーションは、 [ナビゲーションドロアー](https://reactnavigation.org/docs/drawer-based-navigation.html) を使用して、さまざまなビュー間を移動します。</span><span class="sxs-lookup"><span data-stu-id="cf887-137">The application will use a [navigation drawer](https://reactnavigation.org/docs/drawer-based-navigation.html) to navigate between different views.</span></span> <span data-ttu-id="cf887-138">この手順では、アプリで使用される基本的なビューを作成し、ナビゲーションドロアーを実装します。</span><span class="sxs-lookup"><span data-stu-id="cf887-138">In this step you will create the basic views used by the app and implement the navigation drawer.</span></span>

### <a name="create-views"></a><span data-ttu-id="cf887-139">ビューを作成する</span><span class="sxs-lookup"><span data-stu-id="cf887-139">Create views</span></span>

<span data-ttu-id="cf887-140">このセクションでは、 [認証フロー](https://reactnavigation.org/docs/auth-flow)をサポートするためのアプリのビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="cf887-140">In this section you will create the views for the app to support an [authentication flow](https://reactnavigation.org/docs/auth-flow).</span></span>

1. <span data-ttu-id="cf887-141">**Graphtutorial チュートリアル/index.js** を開いて、その他のステートメントの前に、次をファイルの先頭に追加し `import` ます。</span><span class="sxs-lookup"><span data-stu-id="cf887-141">Open **GraphTutorial/index.js** and add the following to the top of the file, before any other `import` statements.</span></span>

    ```javascript
    import 'react-native-gesture-handler';
    ```

1. <span data-ttu-id="cf887-142">「 **Authcontext** 」という名前の **graphtutorial** ディレクトリに新しいファイルを作成し、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="cf887-142">Create a new file in the **GraphTutorial** directory named **AuthContext.tsx** and add the following code.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/AuthContext.tsx" id="AuthContextSnippet":::

1. <span data-ttu-id="cf887-143">**UserContext** という名前の **graphtutorial** ディレクトリに新しいファイルを作成し、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="cf887-143">Create a new file in the **GraphTutorial** directory named **UserContext.tsx** and add the following code.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/UserContext.tsx" id="UserContextSnippet":::

1. <span data-ttu-id="cf887-144">「 **画面** 」という名前の「 **graphtutorial** 」ディレクトリに新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="cf887-144">Create a new directory in the **GraphTutorial** directory named **screens**.</span></span>
1. <span data-ttu-id="cf887-145">**HomeScreen** という名前の **graphtutorial または画面** ディレクトリに新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="cf887-145">Create a new file in the **GraphTutorial/screens** directory named **HomeScreen.tsx**.</span></span> <span data-ttu-id="cf887-146">次のコードをファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="cf887-146">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/HomeScreen.tsx" id="HomeScreenSnippet":::

1. <span data-ttu-id="cf887-147">**Calendarscreen** という名前の **graphtutorial/画面** ディレクトリに新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="cf887-147">Create a new file in the **GraphTutorial/screens** directory named **CalendarScreen.tsx**.</span></span> <span data-ttu-id="cf887-148">次のコードをファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="cf887-148">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="cf887-149">**SignInScreen** という名前の **graphtutorial または画面** ディレクトリに新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="cf887-149">Create a new file in the **GraphTutorial/screens** directory named **SignInScreen.tsx**.</span></span> <span data-ttu-id="cf887-150">次のコードをファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="cf887-150">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="cf887-151">「 **Authload Ingscreen** 」という名前の **graphtutorial または画面** ディレクトリに新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="cf887-151">Create a new file in the **GraphTutorial/screens** directory named **AuthLoadingScreen.tsx**.</span></span> <span data-ttu-id="cf887-152">次のコードをファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="cf887-152">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/AuthLoadingScreen.tsx" id="AuthLoadingScreenSnippet":::

### <a name="create-a-navigation-drawer"></a><span data-ttu-id="cf887-153">ナビゲーションドロアーを作成する</span><span class="sxs-lookup"><span data-stu-id="cf887-153">Create a navigation drawer</span></span>

<span data-ttu-id="cf887-154">このセクションでは、アプリケーションのメニューを作成し、画面間を移動するために反応するナビゲーションを使用するようにアプリケーションを更新します。</span><span class="sxs-lookup"><span data-stu-id="cf887-154">In this section you will create a menu for the application, and update the application to use react-navigation to move between screens.</span></span>

1. <span data-ttu-id="cf887-155">「 **メニュー** という名前の **graphtutorial** ディレクトリ」に新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="cf887-155">Create a new directory in the **GraphTutorial** directory named **menus**.</span></span>

1. <span data-ttu-id="cf887-156">「 **Drawermenu** 」という名前の **graphermenu** ディレクトリに新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="cf887-156">Create a new file in the **GraphTutorial/menus** directory named **DrawerMenu.tsx**.</span></span> <span data-ttu-id="cf887-157">次のコードをファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="cf887-157">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="cf887-158">**Graphtutorial** の「 **images** 」という名前の新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="cf887-158">Create a new directory in the **GraphTutorial** directory named **images**.</span></span>
1. <span data-ttu-id="cf887-159">このディレクトリに **no-profile-pic.png** という名前の既定のプロファイルイメージを追加します。</span><span class="sxs-lookup"><span data-stu-id="cf887-159">Add a default profile image named **no-profile-pic.png** in this directory.</span></span> <span data-ttu-id="cf887-160">好みのイメージを使用することも、 [このサンプルの](https://github.com/microsoftgraph/msgraph-training-react-native/blob/master/demo/GraphTutorial/images/no-profile-pic.png)イメージを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="cf887-160">You can use any image you like, or use [the one from this sample](https://github.com/microsoftgraph/msgraph-training-react-native/blob/master/demo/GraphTutorial/images/no-profile-pic.png).</span></span>

1. <span data-ttu-id="cf887-161">**Graphtutorial またはアプリケーション tsx** ファイルを開き、内容全体を次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="cf887-161">Open the **GraphTutorial/App.tsx** file and replace the entire contents with the following.</span></span>

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

1. <span data-ttu-id="cf887-162">すべての変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="cf887-162">Save all of your changes.</span></span>

1. <span data-ttu-id="cf887-163">エミュレーターにアプリケーションを再読み込みします。</span><span class="sxs-lookup"><span data-stu-id="cf887-163">Reload the application in your emulator.</span></span>

<span data-ttu-id="cf887-164">アプリのメニューは、2つのフラグメント間を移動し、[ **サインイン** ] または [ **サインアウト** ] ボタンをタップすると、変更されます。</span><span class="sxs-lookup"><span data-stu-id="cf887-164">The app's menu should work to navigate between the two fragments and change when you tap the **Sign in** or **Sign out** buttons.</span></span>

![Android 上のアプリケーションのスクリーンショット](./images/android-app-screens.png)

![IOS 上のアプリケーションのスクリーンショット](./images/ios-app-screens.png)
