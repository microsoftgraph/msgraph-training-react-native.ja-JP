<!-- markdownlint-disable MD002 MD041 -->

この演習では、Azure AD での認証をサポートするために、前の手順で作成したアプリケーションを拡張します。 これは、Microsoft Graph を呼び出すために必要な OAuth アクセストークンを取得するために必要です。 これを行うには、アプリケーションに対して、[ネイティブなアプリケーション認証](https://github.com/FormidableLabs/react-native-app-auth)の調整ライブラリを統合します。

1. 「 **Auth**」という名前を持つ「 **graphtutorial** 」ディレクトリに新しいディレクトリを作成します。
1. 「 **Authconfig .js**」という名前の新しいファイルを**graphtutorial または auth**ディレクトリに作成します。 このファイルに次のコードを追加します。

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

    を`YOUR_APP_ID_HERE`アプリ登録のアプリ ID に置き換えます。

> [!IMPORTANT]
> Git などのソース管理を使用している場合は、この時点で**Authconfig .js**ファイルをソース管理から除外して、アプリ ID が誤ってリークしないようにすることをお勧めします。

## <a name="implement-sign-in"></a>サインインの実装

このセクションでは、認証ヘルパークラスを作成し、サインインしてサインアウトするためにアプリを更新します。

1. 「 **AuthManager**」という名前の**graphtutorial/auth**ディレクトリに新しいファイルを作成します。 このファイルに次のコードを追加します。

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

1. **Graphtutorial/views/SignInScreen**ファイルを開き、次`import`のステートメントをファイルの先頭に追加します。

    ```js
    import { AuthManager } from '../auth/AuthManager';
    ```

1. 既存`_signInAsync`のメソッドを次のように置き換えます。

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

1. 次に示すメソッドを `HomeScreen` クラスに追加します。

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

1. **Graphtutorial/menu/DrawerMenu**ファイルを開き、次`import`のステートメントをファイルの先頭に追加します。

    ```js
    import { AuthManager } from '../auth/AuthManager';
    ```

1. で`_onItemPressed`、 `// TEMPORARY`行を次のように置き換えます。

    ```js
    await AuthManager.signOutAsync();
    ```

1. 変更を保存し、エミュレーターでアプリケーションを再読み込みします。

アプリにサインインすると、[**ようこそ**] 画面にアクセストークンが表示されます。

## <a name="get-user-details"></a>ユーザーの詳細を取得する

このセクションでは、Graph クライアントライブラリ用のカスタム認証プロバイダを作成し、Microsoft Graph へのすべての呼び出しを保持するヘルパークラスを作成し`HomeScreen` 、 `DrawerMenuContent`この新しいクラスを使用してログインユーザーを取得するためのクラスとクラスを更新します。

1. **Graph**という名前の**graphtutorial**ディレクトリに新しいディレクトリを作成します。
1. **Graphauthprovider**という名前の**graphtutorial または graph**ディレクトリに、新しいファイルを作成します。 このファイルに次のコードを追加します。

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

1. **Graphtutorial .js**という名前の**graphtutorial または graph**ディレクトリに、新しいファイルを作成します。 このファイルに次のコードを追加します。

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

1. **Graphtutorial/views/HomeScreen**ファイルを開き、次`import`のステートメントをファイルの先頭に追加します。

    ```js
    import { GraphManager } from '../graph/GraphManager';
    ```

1. `componentDidMount`メソッドを次のように置き換えます。

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

1. **Graphtutorial/views/DrawerMenu .js**ファイルを開き、次`import`のステートメントをファイルの先頭に追加します。

    ```js
    import { GraphManager } from '../graph/GraphManager';
    ```

1. 次`componentDidMount`のメソッドを`DrawerMenuContent`クラスに追加します。

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

変更を保存してすぐにアプリを再読み込みすると、ユーザーの表示名と電子メールアドレスで UI が更新されます。
