<!-- markdownlint-disable MD002 MD041 -->

このチュートリアルでは、Microsoft Graph API を使用してユーザーの予定表情報を取得する、反応するネイティブアプリを構築する方法について説明します。

> [!TIP]
> 完成したチュートリアルをダウンロードするだけで済む場合は、 [GitHub リポジトリ](https://github.com/microsoftgraph/msgraph-training-react-native)をダウンロードするか、クローンを作成できます。

## <a name="prerequisites"></a>前提条件

このチュートリアルを開始する前に、開発用のコンピューターに次のものがインストールされている必要があります。

- 次のうち少なくとも1つ。
  - [Android Studio](https://developer.android.com/studio/) **および** [Java 開発キット](https://jdk.java.net)(android でサンプルを実行するために必要)
  - [Xcode](https://developer.apple.com/xcode/) (iOS でサンプルを実行するために必要)
- [Node.js](https://nodejs.org)

> [!NOTE]
> このチュートリアルは、対応するネイティブ CLI を使用して記述されています。これは、オペレーティングシステムとターゲットプラットフォームによって固有の前提条件を備えています。 開発用コンピューターを構成する方法については、「基本的な操作を[開始](https://facebook.github.io/react-native/docs/getting-started)する」を参照してください。 このチュートリアルで使用されているバージョンを以下に示します。 このガイドの手順は、他のバージョンでは動作しますが、テストされていません。
>
> - Android Studio バージョン 3.4.2 with 1.8.0 JRE および Android 9.0 SDK
> - Java 開発キットバージョン12.0.2
> - Xcode version 10.3
> - Node.js バージョン10.16.0

## <a name="feedback"></a>フィードバック

このチュートリアルに関するフィードバックは、 [GitHub リポジトリ](https://github.com/microsoftgraph/msgraph-training-react-native)に記入してください。
