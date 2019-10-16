<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="30ce9-101">この演習では、Azure AD での認証をサポートするために、前の手順で作成したアプリケーションを拡張します。</span><span class="sxs-lookup"><span data-stu-id="30ce9-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="30ce9-102">これは、Microsoft Graph を呼び出すために必要な OAuth アクセストークンを取得するために必要です。</span><span class="sxs-lookup"><span data-stu-id="30ce9-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="30ce9-103">これを行うには、アプリケーションに対して、[ネイティブなアプリケーション認証](https://github.com/FormidableLabs/react-native-app-auth)の調整ライブラリを統合します。</span><span class="sxs-lookup"><span data-stu-id="30ce9-103">To do this, you will integrate the [react-native-app-auth](https://github.com/FormidableLabs/react-native-app-auth) library into the application.</span></span>

1. <span data-ttu-id="30ce9-104">「 **Auth**」という名前を持つ「 **graphtutorial** 」ディレクトリに新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="30ce9-104">Create a new directory in the **GraphTutorial** directory named **auth**.</span></span>
1. <span data-ttu-id="30ce9-105">「 **Authconfig .js**」という名前の新しいファイルを**graphtutorial または auth**ディレクトリに作成します。</span><span class="sxs-lookup"><span data-stu-id="30ce9-105">Create a new file in the **GraphTutorial/auth** directory named **AuthConfig.js**.</span></span> <span data-ttu-id="30ce9-106">このファイルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="30ce9-106">Add the following code to the file.</span></span>

    ```js
    export const AuthConfig = {
      appId = 'YOUR_APP_ID_HERE',
      appScopes = [
        'openid',
        'offline_access',
        'profile',
        'User.Read',
        'Calendars.Read'
      ]
    };
    ```

    <span data-ttu-id="30ce9-107">を`YOUR_APP_ID_HERE`アプリ登録のアプリ ID に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="30ce9-107">Replace `YOUR_APP_ID_HERE` with the app ID from your app registration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="30ce9-108">Git などのソース管理を使用している場合は、この時点で**Authconfig .js**ファイルをソース管理から除外して、アプリ ID が誤ってリークしないようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="30ce9-108">If you're using source control such as git, now would be a good time to exclude the **AuthConfig.js** file from source control to avoid inadvertently leaking your app ID.</span></span>

## <a name="implement-sign-in"></a><span data-ttu-id="30ce9-109">サインインの実装</span><span class="sxs-lookup"><span data-stu-id="30ce9-109">Implement sign-in</span></span>

<span data-ttu-id="30ce9-110">このセクションでは、認証ヘルパークラスを作成し、サインインしてサインアウトするためにアプリを更新します。</span><span class="sxs-lookup"><span data-stu-id="30ce9-110">In this section you will create an authentication helper class, and update the app to sign in and sign out.</span></span>

1. <span data-ttu-id="30ce9-111">「 **AuthManager**」という名前の**graphtutorial/auth**ディレクトリに新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="30ce9-111">Create a new file in the **GraphTutorial/auth** directory named **AuthManager.js**.</span></span> <span data-ttu-id="30ce9-112">このファイルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="30ce9-112">Add the following code to the file.</span></span>

    ```js
    import { AuthConfig } from './AuthConfig';
    import { AsyncStorage } from 'react-native';
    import { authorize, refresh } from 'react-native-app-auth';
    import moment from 'moment';

    const config = {
      clientId: AuthConfig.appId,
      redirectUrl: Platform.OS === 'ios' ? 'urn:ietf:wg:oauth:2.0:oob' : 'graph-tutorial://react-native-auth',
      scopes: AuthConfig.appScopes,
      additionalParameters: { prompt: 'select_account' },
      serviceConfiguration: {
        authorizationEndpoint: 'https://login.microsoftonline.com/common/oauth2/v2.0/authorize',
        tokenEndpoint: 'https://login.microsoftonline.com/common/oauth2/v2.0/token',
      }
    };

    export class AuthManager {

      static signInAsync = async () => {
        const result = await authorize(config);

        // Store the access token, refresh token, and expiration time in storage
        await AsyncStorage.setItem('userToken', result.accessToken);
        await AsyncStorage.setItem('refreshToken', result.refreshToken);
        await AsyncStorage.setItem('expireTime', result.accessTokenExpirationDate);
      }

      static signOutAsync = async () => {
        // Clear storage
        await AsyncStorage.removeItem('userToken');
        await AsyncStorage.removeItem('refreshToken');
        await AsyncStorage.removeItem('expireTime');
      }

      static getAccessTokenAsync = async() => {
        const expireTime = await AsyncStorage.getItem('expireTime');

        if (expireTime !== null) {
          // Get expiration time - 5 minutes
          // If it's <= 5 minutes before expiration, then refresh
          const expire = moment(expireTime).subtract(5, 'minutes');
          const now = moment();

          if (now.isSameOrAfter(expire)) {
            // Expired, refresh
            const refreshToken = await AsyncStorage.getItem('refreshToken');

            const result = await refresh(config, {refreshToken: refreshToken});

            // Store the new access token, refresh token, and expiration time in storage
            await AsyncStorage.setItem('userToken', result.accessToken);
            await AsyncStorage.setItem('refreshToken', result.refreshToken);
            await AsyncStorage.setItem('expireTime', result.accessTokenExpirationDate);

            return result.accessToken;
          }

          // Not expired, just return saved access token
          const accessToken = await AsyncStorage.getItem('userToken');
          return accessToken;
        }

        return null;
      }
    }
    ```

1. <span data-ttu-id="30ce9-113">**Graphtutorial/views/SignInScreen**ファイルを開き、次`import`のステートメントをファイルの先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="30ce9-113">Open the **GraphTutorial/views/SignInScreen.js** file and add the following `import` statement to the top of the file.</span></span>

    ```js
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="30ce9-114">既存`_signInAsync`のメソッドを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="30ce9-114">Replace the existing `_signInAsync` method with the following.</span></span>

    ```js
    _signInAsync = async () => {
      try {
        await AuthManager.signInAsync();
        this.props.navigation.navigate('App');
      } catch (error) {
        alert(error);
      }
    };

1. Open the **GraphTutorial/views/HomeScreen.js** file and add the following `import` statement to the top of the file.

    ```js
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="30ce9-115">次に示すメソッドを `HomeScreen` クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="30ce9-115">Add the following method to the `HomeScreen` class.</span></span>

    ```js
    async componentDidMount() {
      try {
        const accessToken = await AuthManager.getAccessTokenAsync();

        // TEMPORARY
        this.setState({userName: accessToken, userLoading: false});
      } catch (error) {
        alert(error);
      }
    }
    ```

1. <span data-ttu-id="30ce9-116">**Graphtutorial/menu/DrawerMenu**ファイルを開き、次`import`のステートメントをファイルの先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="30ce9-116">Open the **GraphTutorial/menus/DrawerMenu.js** file and add the following `import` statement to the top of the file.</span></span>

    ```js
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="30ce9-117">で`_onItemPressed`、 `// TEMPORARY`行を次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="30ce9-117">In `_onItemPressed`, replace the `// TEMPORARY` line with the following.</span></span>

    ```js
    await AuthManager.signOutAsync();
    ```

1. <span data-ttu-id="30ce9-118">変更を保存し、エミュレーターでアプリケーションを再読み込みします。</span><span class="sxs-lookup"><span data-stu-id="30ce9-118">Save your changes and reload the application in your emulator.</span></span>

<span data-ttu-id="30ce9-119">アプリにサインインすると、[**ようこそ**] 画面にアクセストークンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="30ce9-119">If you sign in to the app, you should see an access token displayed on the **Welcome** screen.</span></span>

## <a name="get-user-details"></a><span data-ttu-id="30ce9-120">ユーザーの詳細を取得する</span><span class="sxs-lookup"><span data-stu-id="30ce9-120">Get user details</span></span>

<span data-ttu-id="30ce9-121">このセクションでは、Graph クライアントライブラリ用のカスタム認証プロバイダを作成し、Microsoft Graph へのすべての呼び出しを保持するヘルパークラスを作成し`HomeScreen` 、 `DrawerMenuContent`この新しいクラスを使用してログインユーザーを取得するためのクラスとクラスを更新します。</span><span class="sxs-lookup"><span data-stu-id="30ce9-121">In this section you will create a custom authentication provider for the Graph client library, create a helper class to hold all of the calls to Microsoft Graph and update the `HomeScreen` and `DrawerMenuContent` classes to use this new class to get the logged-in user.</span></span>

1. <span data-ttu-id="30ce9-122">**Graph**という名前の**graphtutorial**ディレクトリに新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="30ce9-122">Create a new directory in the **GraphTutorial** directory named **graph**.</span></span>
1. <span data-ttu-id="30ce9-123">**Graphauthprovider**という名前の**graphtutorial または graph**ディレクトリに、新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="30ce9-123">Create a new file in the **GraphTutorial/graph** directory named **GraphAuthProvider.js**.</span></span> <span data-ttu-id="30ce9-124">このファイルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="30ce9-124">Add the following code to the file.</span></span>

    ```js
    import { AuthManager } from '../auth/AuthManager';

    // Used by Graph client to get access tokens
    // See https://github.com/microsoftgraph/msgraph-sdk-javascript/blob/dev/docs/CustomAuthenticationProvider.md
    export class GraphAuthProvider {
      getAccessToken = async() => {
        return await AuthManager.getAccessTokenAsync();
      }
    }
    ```

1. <span data-ttu-id="30ce9-125">**Graphtutorial .js**という名前の**graphtutorial または graph**ディレクトリに、新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="30ce9-125">Create a new file in the **GraphTutorial/graph** directory named **GraphManager.js**.</span></span> <span data-ttu-id="30ce9-126">このファイルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="30ce9-126">Add the following code to the file.</span></span>

    ```js
    import { Client } from '@microsoft/microsoft-graph-client';
    import { GraphAuthProvider } from './GraphAuthProvider';

    // Set the authProvider to an instance
    // of GraphAuthProvider
    const clientOptions = {
      authProvider: new GraphAuthProvider()
    };

    // Initialize the client
    const graphClient = Client.initWithMiddleware(clientOptions);

    export class GraphManager {
      static getUserAsync = async() => {
        // GET /me
        return graphClient.api('/me').get();
      }
    }
    ```

1. <span data-ttu-id="30ce9-127">**Graphtutorial/views/HomeScreen**ファイルを開き、次`import`のステートメントをファイルの先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="30ce9-127">Open the **GraphTutorial/views/HomeScreen.js** file and add the following `import` statement to the top of the file.</span></span>

    ```js
    import { GraphManager } from '../graph/GraphManager';
    ```

1. <span data-ttu-id="30ce9-128">`componentDidMount`メソッドを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="30ce9-128">Replace the `componentDidMount` method with the following.</span></span>

    ```js
    async componentDidMount() {
      try {
        // Get the signed-in user from Graph
        const user = await GraphManager.getUserAsync();
        // Set the user name to the user's given name
        this.setState({userName: user.givenName, userLoading: false});
      } catch (error) {
        alert(error);
      }
    }
    ```

1. <span data-ttu-id="30ce9-129">**Graphtutorial/views/DrawerMenu .js**ファイルを開き、次`import`のステートメントをファイルの先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="30ce9-129">Open the **GraphTutorial/views/DrawerMenu.js** file and add the following `import` statement to the top of the file.</span></span>

    ```js
    import { GraphManager } from '../graph/GraphManager';
    ```

1. <span data-ttu-id="30ce9-130">次`componentDidMount`のメソッドを`DrawerMenuContent`クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="30ce9-130">Add the following `componentDidMount` method to the `DrawerMenuContent` class.</span></span>

    ```js
    async componentDidMount() {
      try {
        // Get the signed-in user from Graph
        const user = await GraphManager.getUserAsync();

        // Update UI with display name and email
        this.setState({
          userName: user.displayName,
          // Work/School accounts have email address in mail attribute
          // Personal accounts have it in userPrincipalName
          userEmail: user.mail !== null ? user.mail : user.userPrincipalName,
        });
      } catch(error) {
        alert(error);
      }
    }
    ```

<span data-ttu-id="30ce9-131">変更を保存してすぐにアプリを再読み込みすると、ユーザーの表示名と電子メールアドレスで UI が更新されます。</span><span class="sxs-lookup"><span data-stu-id="30ce9-131">If you save your changes and reload the app now, after sign-in the UI is updated with the user's display name and email address.</span></span>
