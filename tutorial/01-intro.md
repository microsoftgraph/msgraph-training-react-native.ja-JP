<!-- markdownlint-disable MD002 MD041 -->

このチュートリアルでは、Microsoft Graph API を使用してユーザーの予定表情報を取得する、反応するネイティブアプリを構築する方法について説明します。

> [!TIP]
> 完成したチュートリアルをダウンロードするだけで済む場合は、 [GitHub リポジトリ](https://github.com/microsoftgraph/msgraph-training-react-native)をダウンロードするか、クローンを作成できます。

## <a name="prerequisites"></a>前提条件

このチュートリアルを開始する前に、開発用のコンピューターに次のものがインストールされている必要があります。

- 次のうち少なくとも1つ。
  - [Android Studio](https://developer.android.com/studio/) **および** [Java 開発キット](https://jdk.java.net) (android でサンプルを実行するために必要)
  - [Xcode](https://developer.apple.com/xcode/) (iOS でサンプルを実行するために必要)
- [Node.js](https://nodejs.org)

また、Outlook.com 上のメールボックスを持つ個人の Microsoft アカウント、または Microsoft 職場または学校のアカウントを所有している必要があります。 Microsoft アカウントを持っていない場合は、無料のアカウントを取得するためのオプションがいくつかあります。

- [新しい個人用 Microsoft アカウントにサインアップ](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)することができます。
- [Office 365 開発者プログラムにサインアップ](https://developer.microsoft.com/office/dev-program)して、無料の office 365 サブスクリプションを取得することができます。

> [!NOTE]
> このチュートリアルは、対応するネイティブ CLI を使用して記述されています。これは、オペレーティングシステムとターゲットプラットフォームによって固有の前提条件を備えています。 開発用コンピューターを構成する方法については、「基本的な操作を [開始](https://reactnative.dev/docs/environment-setup) する」を参照してください。 このチュートリアルで使用されているバージョンを以下に示します。 このガイドの手順は、他のバージョンでは動作しますが、テストされていません。
>
> - Android Studio バージョン4.1 と Android 9.0 SDK
> - Java 開発キットバージョン12.0.2
> - Xcode version 12.1
> - Node.js バージョン14.15.0

## <a name="feedback"></a>フィードバック

このチュートリアルに関するフィードバックは、 [GitHub リポジトリ](https://github.com/microsoftgraph/msgraph-training-react-native)に記入してください。
