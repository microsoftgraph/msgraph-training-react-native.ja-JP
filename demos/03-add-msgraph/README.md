# <a name="how-to-run-the-completed-project"></a>完了したプロジェクトを実行する方法

## <a name="prerequisites"></a>前提条件

このフォルダーで完了したプロジェクトを実行するには、次のものが必要です。

- 次のうち少なくとも1つ。
  - [Android Studio](https://developer.android.com/studio/) **および** [Java 開発キット](https://jdk.java.net)(android でサンプルを実行するために必要)
  - [Xcode](https://developer.apple.com/xcode/) (iOS でサンプルを実行するために必要)
- [Node.js](https://nodejs.org)
- Outlook.com 上のメールボックスを持つ個人の Microsoft アカウント、または Microsoft 職場または学校のアカウントのいずれか。

> **注:** このチュートリアルは、対応するネイティブ CLI を使用して記述されています。これは、オペレーティングシステムとターゲットプラットフォームによって固有の前提条件を備えています。 開発用コンピューターを構成する方法については、「基本的な操作を[開始](https://facebook.github.io/react-native/docs/getting-started)する」を参照してください。 このチュートリアルで使用されているバージョンを以下に示します。 このガイドの手順は、他のバージョンでは動作しますが、テストされていません。
>
> - Android Studio バージョン 3.4.2 with 1.8.0 JRE および Android 9.0 SDK
> - Java 開発キットバージョン12.0.2
> - Xcode version 10.3
> - Node.js バージョン10.16.0

Microsoft アカウントを持っていない場合は、無料のアカウントを取得するためのオプションがいくつかあります。

- [新しい個人用 Microsoft アカウントにサインアップ](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)することができます。
- [Office 365 開発者プログラムにサインアップ](https://developer.microsoft.com/office/dev-program)して、無料の office 365 サブスクリプションを取得することができます。

## <a name="register-an-application-with-the-azure-active-directory-admin-center"></a>Azure Active Directory 管理センターにアプリケーションを登録する

1. ブラウザーを開き、[Azure Active Directory 管理センター](https://aad.portal.azure.com)へ移動して、**個人用アカウント** (別名: Microsoft アカウント)、または**職場/学校アカウント**を使用してログインします。

1. 左側のナビゲーションで [ **Azure Active Directory** ] を選択し、[**管理**] の下にある [**アプリの登録**] を選択します。

    ![アプリの登録のスクリーンショット ](/tutorial/images/aad-portal-app-registrations.png)

1. **[新規登録]** を選択します。 **[アプリケーションを登録]** ページで、次のように値を設定します。

    - `React Native Graph Tutorial` に **[名前]** を設定します。
    - **[サポートされているアカウントの種類]** を **[任意の組織のディレクトリ内のアカウントと個人用の Microsoft アカウント]** に設定します。
    - [**リダイレクト URI**] で、ドロップダウンを [**パブリッククライアント (モバイル & デスクトップ)**] に変更し`graph-tutorial://react-native-auth`、値をに設定します。

    ![[アプリケーションの登録] ページのスクリーンショット](/tutorial/images/aad-register-an-app.png)

1. [**登録**] を選択します。 [**ネイティブグラフの応答] チュートリアル**ページで、**アプリケーション (クライアント) ID**の値をコピーして保存します。そのためには、次の手順を実行する必要があります。

    ![新しいアプリの登録のアプリケーション ID のスクリーンショット](/tutorial/images/aad-application-id.png)

1. [**管理**] で、[**認証**] を選択します。 [**リダイレクト uri** ] ページで、uri `urn:ietf:wg:oauth:2.0:oob`を使用して、**パブリッククライアント (モバイル & デスクトップ)** 型の別のリダイレクト URI を追加します。 [**保存**] を選択します。

    ![リダイレクト Uri ページのスクリーンショット](/tutorial/images/aad-redirect-uris.png)

## <a name="configure-the-sample"></a>サンプルを構成する

1. **Graphtutorial/auth/AuthConfig .js**ファイルの名前を**authconfig**に変更します。
1. **Authconfig .js**ファイルを編集し、次のように変更します。
    1. を`YOUR_APP_ID_HERE`アプリ登録ポータルで取得した**アプリケーション Id**に置き換えます。

1. コマンドラインインターフェイス (CLI) で、 **Graphtutorial**ディレクトリに移動し、次のコマンドを実行して要件をインストールします。

    ```Shell
    npm install
    ```

## <a name="run-the-sample"></a>サンプルを実行する

### <a name="run-on-ios-simulator"></a>IOS シミュレータで実行する

CLI で次のコマンドを実行して、iOS シミュレータでアプリケーションを起動します。

```Shell
react-native run-ios
```

### <a name="run-on-android-emulator"></a>Android エミュレーターで実行する

を起動し、android エミュレーターで次のコマンドを実行して、Android エミュレーターでアプリケーションを起動します。

```Shell
react-native run-android
```
