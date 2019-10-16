<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="2b4cd-101">このチュートリアルでは、Microsoft Graph API を使用してユーザーの予定表情報を取得する、反応するネイティブアプリを構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2b4cd-101">This tutorial teaches you how to build an React Native app that uses the Microsoft Graph API to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="2b4cd-102">完成したチュートリアルをダウンロードするだけで済む場合は、 [GitHub リポジトリ](https://github.com/microsoftgraph/msgraph-training-react-native)をダウンロードするか、クローンを作成できます。</span><span class="sxs-lookup"><span data-stu-id="2b4cd-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-react-native).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b4cd-103">前提条件</span><span class="sxs-lookup"><span data-stu-id="2b4cd-103">Prerequisites</span></span>

<span data-ttu-id="2b4cd-104">このチュートリアルを開始する前に、開発用のコンピューターに次のものがインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="2b4cd-104">Before you start this tutorial, you should have the following installed on your development machine.</span></span>

- <span data-ttu-id="2b4cd-105">次のうち少なくとも1つ。</span><span class="sxs-lookup"><span data-stu-id="2b4cd-105">At least one of the following:</span></span>
  - <span data-ttu-id="2b4cd-106">[Android Studio](https://developer.android.com/studio/) **および** [Java 開発キット](https://jdk.java.net)(android でサンプルを実行するために必要)</span><span class="sxs-lookup"><span data-stu-id="2b4cd-106">[Android Studio](https://developer.android.com/studio/) **and** [Java Development Kit](https://jdk.java.net) (required to run the sample on Android)</span></span>
  - <span data-ttu-id="2b4cd-107">[Xcode](https://developer.apple.com/xcode/) (iOS でサンプルを実行するために必要)</span><span class="sxs-lookup"><span data-stu-id="2b4cd-107">[Xcode](https://developer.apple.com/xcode/) (required to run the sample on iOS)</span></span>
- [<span data-ttu-id="2b4cd-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="2b4cd-108">Node.js</span></span>](https://nodejs.org)

> [!NOTE]
> <span data-ttu-id="2b4cd-109">このチュートリアルは、対応するネイティブ CLI を使用して記述されています。これは、オペレーティングシステムとターゲットプラットフォームによって固有の前提条件を備えています。</span><span class="sxs-lookup"><span data-stu-id="2b4cd-109">This tutorial was written using the React Native CLI, which has specific prerequisites depending on your operating system and target platforms.</span></span> <span data-ttu-id="2b4cd-110">開発用コンピューターを構成する方法については、「基本的な操作を[開始](https://facebook.github.io/react-native/docs/getting-started)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2b4cd-110">See [React Native Getting Started](https://facebook.github.io/react-native/docs/getting-started) for instructions on configuring your development machine.</span></span> <span data-ttu-id="2b4cd-111">このチュートリアルで使用されているバージョンを以下に示します。</span><span class="sxs-lookup"><span data-stu-id="2b4cd-111">The versions used for this tutorial are listed below.</span></span> <span data-ttu-id="2b4cd-112">このガイドの手順は、他のバージョンでは動作しますが、テストされていません。</span><span class="sxs-lookup"><span data-stu-id="2b4cd-112">The steps in this guide may work with other versions, but that has not been tested.</span></span>
>
> - <span data-ttu-id="2b4cd-113">Android Studio バージョン 3.4.2 with 1.8.0 JRE および Android 9.0 SDK</span><span class="sxs-lookup"><span data-stu-id="2b4cd-113">Android Studio version 3.4.2 with the 1.8.0 JRE and the Android 9.0 SDK</span></span>
> - <span data-ttu-id="2b4cd-114">Java 開発キットバージョン12.0.2</span><span class="sxs-lookup"><span data-stu-id="2b4cd-114">Java Development Kit version 12.0.2</span></span>
> - <span data-ttu-id="2b4cd-115">Xcode version 10.3</span><span class="sxs-lookup"><span data-stu-id="2b4cd-115">Xcode version 10.3</span></span>
> - <span data-ttu-id="2b4cd-116">Node.js バージョン10.16.0</span><span class="sxs-lookup"><span data-stu-id="2b4cd-116">Node.js version 10.16.0</span></span>

## <a name="feedback"></a><span data-ttu-id="2b4cd-117">フィードバック</span><span class="sxs-lookup"><span data-stu-id="2b4cd-117">Feedback</span></span>

<span data-ttu-id="2b4cd-118">このチュートリアルに関するフィードバックは、 [GitHub リポジトリ](https://github.com/microsoftgraph/msgraph-training-react-native)に記入してください。</span><span class="sxs-lookup"><span data-stu-id="2b4cd-118">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-react-native).</span></span>
