<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="37375-101">このチュートリアルでは、Microsoft Graph API を使用してユーザーの予定表情報を取得する、反応するネイティブアプリを構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="37375-101">This tutorial teaches you how to build an React Native app that uses the Microsoft Graph API to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="37375-102">完成したチュートリアルをダウンロードするだけで済む場合は、 [GitHub リポジトリ](https://github.com/microsoftgraph/msgraph-training-react-native)をダウンロードするか、クローンを作成できます。</span><span class="sxs-lookup"><span data-stu-id="37375-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-react-native).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37375-103">前提条件</span><span class="sxs-lookup"><span data-stu-id="37375-103">Prerequisites</span></span>

<span data-ttu-id="37375-104">このチュートリアルを開始する前に、開発用のコンピューターに次のものがインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="37375-104">Before you start this tutorial, you should have the following installed on your development machine.</span></span>

- <span data-ttu-id="37375-105">次のうち少なくとも1つ。</span><span class="sxs-lookup"><span data-stu-id="37375-105">At least one of the following:</span></span>
  - <span data-ttu-id="37375-106">[Android Studio](https://developer.android.com/studio/) **および** [Java 開発キット](https://jdk.java.net)(android でサンプルを実行するために必要)</span><span class="sxs-lookup"><span data-stu-id="37375-106">[Android Studio](https://developer.android.com/studio/) **and** [Java Development Kit](https://jdk.java.net) (required to run the sample on Android)</span></span>
  - <span data-ttu-id="37375-107">[Xcode](https://developer.apple.com/xcode/) (iOS でサンプルを実行するために必要)</span><span class="sxs-lookup"><span data-stu-id="37375-107">[Xcode](https://developer.apple.com/xcode/) (required to run the sample on iOS)</span></span>
- [<span data-ttu-id="37375-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="37375-108">Node.js</span></span>](https://nodejs.org)

<span data-ttu-id="37375-109">また、Outlook.com 上のメールボックスを持つ個人の Microsoft アカウント、または Microsoft 職場または学校のアカウントを所有している必要があります。</span><span class="sxs-lookup"><span data-stu-id="37375-109">You should also have either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span> <span data-ttu-id="37375-110">Microsoft アカウントを持っていない場合は、無料のアカウントを取得するためのオプションがいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="37375-110">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="37375-111">[新しい個人用 Microsoft アカウントにサインアップ](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)することができます。</span><span class="sxs-lookup"><span data-stu-id="37375-111">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="37375-112">[Office 365 開発者プログラムにサインアップ](https://developer.microsoft.com/office/dev-program)して、無料の office 365 サブスクリプションを取得することができます。</span><span class="sxs-lookup"><span data-stu-id="37375-112">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="37375-113">このチュートリアルは、対応するネイティブ CLI を使用して記述されています。これは、オペレーティングシステムとターゲットプラットフォームによって固有の前提条件を備えています。</span><span class="sxs-lookup"><span data-stu-id="37375-113">This tutorial was written using the React Native CLI, which has specific prerequisites depending on your operating system and target platforms.</span></span> <span data-ttu-id="37375-114">開発用コンピューターを構成する方法については、「基本的な操作を[開始](https://reactnative.dev/docs/environment-setup)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="37375-114">See [React Native Getting Started](https://reactnative.dev/docs/environment-setup) for instructions on configuring your development machine.</span></span> <span data-ttu-id="37375-115">このチュートリアルで使用されているバージョンを以下に示します。</span><span class="sxs-lookup"><span data-stu-id="37375-115">The versions used for this tutorial are listed below.</span></span> <span data-ttu-id="37375-116">このガイドの手順は、他のバージョンでは動作しますが、テストされていません。</span><span class="sxs-lookup"><span data-stu-id="37375-116">The steps in this guide may work with other versions, but that has not been tested.</span></span>
>
> - <span data-ttu-id="37375-117">Android Studio バージョン 3.6.2 with Android 9.0 SDK</span><span class="sxs-lookup"><span data-stu-id="37375-117">Android Studio version 3.6.2 with the Android 9.0 SDK</span></span>
> - <span data-ttu-id="37375-118">Java 開発キットバージョン12.0.2</span><span class="sxs-lookup"><span data-stu-id="37375-118">Java Development Kit version 12.0.2</span></span>
> - <span data-ttu-id="37375-119">Xcode version 11.4</span><span class="sxs-lookup"><span data-stu-id="37375-119">Xcode version 11.4</span></span>
> - <span data-ttu-id="37375-120">Node.js バージョン12.16.2</span><span class="sxs-lookup"><span data-stu-id="37375-120">Node.js version 12.16.2</span></span>

## <a name="feedback"></a><span data-ttu-id="37375-121">フィードバック</span><span class="sxs-lookup"><span data-stu-id="37375-121">Feedback</span></span>

<span data-ttu-id="37375-122">このチュートリアルに関するフィードバックは、 [GitHub リポジトリ](https://github.com/microsoftgraph/msgraph-training-react-native)に記入してください。</span><span class="sxs-lookup"><span data-stu-id="37375-122">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-react-native).</span></span>
