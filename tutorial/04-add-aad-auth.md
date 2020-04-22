<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="f9473-101">この演習では、Azure AD での認証をサポートするために、前の手順で作成したアプリケーションを拡張します。</span><span class="sxs-lookup"><span data-stu-id="f9473-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="f9473-102">これは、Microsoft Graph を呼び出すために必要な OAuth アクセストークンを取得するために必要です。</span><span class="sxs-lookup"><span data-stu-id="f9473-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="f9473-103">これを行うには、アプリケーションに対して、[ネイティブなアプリケーション認証](https://github.com/FormidableLabs/react-native-app-auth)の調整ライブラリを統合します。</span><span class="sxs-lookup"><span data-stu-id="f9473-103">To do this, you will integrate the [react-native-app-auth](https://github.com/FormidableLabs/react-native-app-auth) library into the application.</span></span>

1. <span data-ttu-id="f9473-104">「 **Auth**」という名前を持つ「 **graphtutorial** 」ディレクトリに新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="f9473-104">Create a new directory in the **GraphTutorial** directory named **auth**.</span></span>
1. <span data-ttu-id="f9473-105">「 **Authconfig. ts**」という名前の**graphtutorial または auth**ディレクトリに新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="f9473-105">Create a new file in the **GraphTutorial/auth** directory named **AuthConfig.ts**.</span></span> <span data-ttu-id="f9473-106">このファイルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="f9473-106">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/auth/AuthConfig.ts.example":::

    <span data-ttu-id="f9473-107">を`YOUR_APP_ID_HERE`アプリ登録のアプリ ID に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="f9473-107">Replace `YOUR_APP_ID_HERE` with the app ID from your app registration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f9473-108">Git などのソース管理を使用している場合は、アプリ ID を誤ってリークしないように、ソース管理から**Authconfig. ts**ファイルを除外することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="f9473-108">If you're using source control such as git, now would be a good time to exclude the **AuthConfig.ts** file from source control to avoid inadvertently leaking your app ID.</span></span>

## <a name="implement-sign-in"></a><span data-ttu-id="f9473-109">サインインの実装</span><span class="sxs-lookup"><span data-stu-id="f9473-109">Implement sign-in</span></span>

<span data-ttu-id="f9473-110">このセクションでは、認証ヘルパークラスを作成し、サインインしてサインアウトするためにアプリを更新します。</span><span class="sxs-lookup"><span data-stu-id="f9473-110">In this section you will create an authentication helper class, and update the app to sign in and sign out.</span></span>

1. <span data-ttu-id="f9473-111">「 **AuthManager. ts**」という名前の新しいファイルを**graphtutorial/auth**ディレクトリに作成します。</span><span class="sxs-lookup"><span data-stu-id="f9473-111">Create a new file in the **GraphTutorial/auth** directory named **AuthManager.ts**.</span></span> <span data-ttu-id="f9473-112">このファイルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="f9473-112">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/auth/AuthManager.ts" id="AuthManagerSnippet":::

1. <span data-ttu-id="f9473-113">**Graphtutorial/views/SignInScreen**ファイルを開き、次`import`のステートメントをファイルの先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="f9473-113">Open the **GraphTutorial/views/SignInScreen.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="f9473-114">既存`_signInAsync`のメソッドを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="f9473-114">Replace the existing `_signInAsync` method with the following.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/SignInScreen.tsx" id="SignInAsyncSnippet":::

1. <span data-ttu-id="f9473-115">**Graphtutorial/views/HomeScreen**ファイルを開き、次`import`のステートメントをファイルの先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="f9473-115">Open the **GraphTutorial/views/HomeScreen.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="f9473-116">次のメソッドを `HomeScreen` クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="f9473-116">Add the following method to the `HomeScreen` class.</span></span>

    ```typescript
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

1. <span data-ttu-id="f9473-117">**Graphtutorial/menu/DrawerMenu. tsx**ファイルを開き、次`import`のステートメントをファイルの先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="f9473-117">Open the **GraphTutorial/menus/DrawerMenu.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="f9473-118">既存`_signOut`のメソッドを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="f9473-118">Replace the existing `_signOut` method with the following.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/menus/DrawerMenu.tsx" id="SignOutSnippet" highlight="5":::

1. <span data-ttu-id="f9473-119">変更を保存し、エミュレーターでアプリケーションを再読み込みします。</span><span class="sxs-lookup"><span data-stu-id="f9473-119">Save your changes and reload the application in your emulator.</span></span>

<span data-ttu-id="f9473-120">アプリにサインインすると、[**ようこそ**] 画面にアクセストークンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f9473-120">If you sign in to the app, you should see an access token displayed on the **Welcome** screen.</span></span>

## <a name="get-user-details"></a><span data-ttu-id="f9473-121">ユーザーの詳細情報を取得する</span><span class="sxs-lookup"><span data-stu-id="f9473-121">Get user details</span></span>

<span data-ttu-id="f9473-122">このセクションでは、Graph クライアントライブラリ用のカスタム認証プロバイダを作成し、Microsoft Graph へのすべての呼び出しを保持するヘルパークラスを作成し`HomeScreen` 、 `DrawerMenuContent`この新しいクラスを使用してログインユーザーを取得するためのクラスとクラスを更新します。</span><span class="sxs-lookup"><span data-stu-id="f9473-122">In this section you will create a custom authentication provider for the Graph client library, create a helper class to hold all of the calls to Microsoft Graph and update the `HomeScreen` and `DrawerMenuContent` classes to use this new class to get the logged-in user.</span></span>

1. <span data-ttu-id="f9473-123">**Graph**という名前の**graphtutorial**ディレクトリに新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="f9473-123">Create a new directory in the **GraphTutorial** directory named **graph**.</span></span>
1. <span data-ttu-id="f9473-124">**Graphauthprovider**という名前の**graphtutorial または graph**ディレクトリに新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="f9473-124">Create a new file in the **GraphTutorial/graph** directory named **GraphAuthProvider.ts**.</span></span> <span data-ttu-id="f9473-125">このファイルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="f9473-125">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphAuthProvider.ts" id="AuthProviderSnippet":::

1. <span data-ttu-id="f9473-126">Graphtutorial という名前の**Graphtutorial または graph**ディレクトリ**GraphManager.ts**に新しいファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="f9473-126">Create a new file in the **GraphTutorial/graph** directory named **GraphManager.ts**.</span></span> <span data-ttu-id="f9473-127">このファイルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="f9473-127">Add the following code to the file.</span></span>

    ```typescript
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

1. <span data-ttu-id="f9473-128">**Graphtutorial/views/HomeScreen**ファイルを開き、次`import`のステートメントをファイルの先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="f9473-128">Open the **GraphTutorial/views/HomeScreen.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import { GraphManager } from '../graph/GraphManager';
    ```

1. <span data-ttu-id="f9473-129">`componentDidMount`メソッドを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="f9473-129">Replace the `componentDidMount` method with the following.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/HomeScreen.tsx" id="ComponentDidMountSnippet" highlight="3-6,9":::

1. <span data-ttu-id="f9473-130">**Graphtutorial/views/DrawerMenu**ファイルを開き、次`import`のステートメントをファイルの先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="f9473-130">Open the **GraphTutorial/views/DrawerMenu.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import { GraphManager } from '../graph/GraphManager';
    ```

1. <span data-ttu-id="f9473-131">次の `componentDidMount` メソッドを `DrawerMenuContent` クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="f9473-131">Add the following `componentDidMount` method to the `DrawerMenuContent` class.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/menus/DrawerMenu.tsx" id="ComponentDidMountSnippet":::

<span data-ttu-id="f9473-132">変更を保存してすぐにアプリを再読み込みすると、ユーザーの表示名と電子メールアドレスで UI が更新されます。</span><span class="sxs-lookup"><span data-stu-id="f9473-132">If you save your changes and reload the app now, after sign-in the UI is updated with the user's display name and email address.</span></span>
