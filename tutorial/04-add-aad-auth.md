<!-- markdownlint-disable MD002 MD041 -->

この演習では、Azure AD での認証をサポートするために、前の手順で作成したアプリケーションを拡張します。 これは、Microsoft Graph を呼び出すために必要な OAuth アクセストークンを取得するために必要です。 これを行うには、アプリケーションに対して、 [ネイティブなアプリケーション認証](https://github.com/FormidableLabs/react-native-app-auth) の調整ライブラリを統合します。

1. 「 **Auth** 」という名前を持つ「 **graphtutorial** 」ディレクトリに新しいディレクトリを作成します。
1. 「 **Authconfig. ts** 」という名前の **graphtutorial または auth** ディレクトリに新しいファイルを作成します。 次のコードをファイルに追加します。

    :::code language="typescript" source="../demo/GraphTutorial/auth/AuthConfig.example.ts":::

    `YOUR_APP_ID_HERE`をアプリ登録のアプリ ID に置き換えます。

> [!IMPORTANT]
> Git などのソース管理を使用している場合は、アプリ ID を誤ってリークしないように、ソース管理から **Authconfig. ts** ファイルを除外することをお勧めします。

## <a name="implement-sign-in"></a>サインインの実装

このセクションでは、認証ヘルパークラスを作成し、サインインしてサインアウトするためにアプリを更新します。

1. 「 **AuthManager. ts** 」という名前の新しいファイルを **graphtutorial/auth** ディレクトリに作成します。 次のコードをファイルに追加します。

    :::code language="typescript" source="../demo/GraphTutorial/auth/AuthManager.ts" id="AuthManagerSnippet":::

1. **Graphtutorial またはアプリケーション tsx** ファイルを開き、次の `import` ステートメントをファイルの先頭に追加します。

    ```typescript
    import { AuthManager } from './auth/AuthManager';
    ```

1. 既存の `authContext` 宣言を次のように置き換えます。

    :::code language="typescript" source="../demo/GraphTutorial/App.tsx" id="AuthContextSnippet" highlight="4-6,9":::

1. **Graphtutorial/menu/DrawerMenu. tsx** ファイルを開き、次の `import` ステートメントをファイルの先頭に追加します。

    ```typescript
    import { AuthManager } from '../auth/AuthManager';
    ```

1. 次のコードを関数に追加し `componentDidMount` ます。

    ```typescript
    try {
      const accessToken = await AuthManager.getAccessTokenAsync();

      // TEMPORARY
      this.setState({userFirstName: accessToken, userLoading: false});
    } catch (error) {
      Alert.alert(
        'Error getting token',
        JSON.stringify(error),
        [
          {
            text: 'OK'
          }
        ],
        { cancelable: false }
      );
    }
    ```

1. 変更を保存し、エミュレーターでアプリケーションを再読み込みします。

アプリにサインインすると、[ **ようこそ** ] 画面にアクセストークンが表示されます。

## <a name="get-user-details"></a>ユーザーの詳細情報を取得する

このセクションでは、Graph クライアントライブラリ用のカスタム認証プロバイダを作成し、Microsoft Graph へのすべての呼び出しを保持するヘルパークラスを作成し、 `DrawerMenuContent` この新しいクラスを使用してログインユーザーを取得するようにクラスを更新します。

1. **Graph** という名前の **graphtutorial** ディレクトリに新しいディレクトリを作成します。
1. **Graphauthprovider** という名前の **graphtutorial または graph** ディレクトリに新しいファイルを作成します。 次のコードをファイルに追加します。

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphAuthProvider.ts" id="AuthProviderSnippet":::

1. Graphtutorial という名前の **Graphtutorial または graph** ディレクトリ **GraphManager.ts** に新しいファイルを作成します。 次のコードをファイルに追加します。

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
        return await graphClient
          .api('/me')
          .select('displayName,givenName,mail,mailboxSettings,userPrincipalName')
          .get();
      }
    }
    ```

1. **Graphtutorial/views/DrawerMenu** ファイルを開き、次の `import` ステートメントをファイルの先頭に追加します。

    ```typescript
    import { GraphManager } from '../graph/GraphManager';
    ```

1. メソッドを `componentDidMount` 次のように置き換えます。

    :::code language="typescript" source="../demo/GraphTutorial/menus/DrawerMenu.tsx" id="ComponentDidMountSnippet":::

変更を保存してすぐにアプリを再読み込みすると、ユーザーの表示名と電子メールアドレスで UI が更新されます。
