# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="f421d-101">完了したプロジェクトを実行する方法</span><span class="sxs-lookup"><span data-stu-id="f421d-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f421d-102">前提条件</span><span class="sxs-lookup"><span data-stu-id="f421d-102">Prerequisites</span></span>

<span data-ttu-id="f421d-103">このフォルダーで完了したプロジェクトを実行するには、次のものが必要です。</span><span class="sxs-lookup"><span data-stu-id="f421d-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="f421d-104">次のうち少なくとも1つ。</span><span class="sxs-lookup"><span data-stu-id="f421d-104">At least one of the following:</span></span>
  - <span data-ttu-id="f421d-105">[Android Studio](https://developer.android.com/studio/) **および** [Java 開発キット](https://jdk.java.net)(android でサンプルを実行するために必要)</span><span class="sxs-lookup"><span data-stu-id="f421d-105">[Android Studio](https://developer.android.com/studio/) **and** [Java Development Kit](https://jdk.java.net) (required to run the sample on Android)</span></span>
  - <span data-ttu-id="f421d-106">[Xcode](https://developer.apple.com/xcode/) (iOS でサンプルを実行するために必要)</span><span class="sxs-lookup"><span data-stu-id="f421d-106">[Xcode](https://developer.apple.com/xcode/) (required to run the sample on iOS)</span></span>
- [<span data-ttu-id="f421d-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="f421d-107">Node.js</span></span>](https://nodejs.org)
- <span data-ttu-id="f421d-108">Outlook.com 上のメールボックスを持つ個人の Microsoft アカウント、または Microsoft 職場または学校のアカウントのいずれか。</span><span class="sxs-lookup"><span data-stu-id="f421d-108">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

> <span data-ttu-id="f421d-109">**注:** このチュートリアルは、対応するネイティブ CLI を使用して記述されています。これは、オペレーティングシステムとターゲットプラットフォームによって固有の前提条件を備えています。</span><span class="sxs-lookup"><span data-stu-id="f421d-109">**Note:** This tutorial was written using the React Native CLI, which has specific prerequisites depending on your operating system and target platforms.</span></span> <span data-ttu-id="f421d-110">開発用コンピューターを構成する方法については、「基本的な操作を[開始](https://facebook.github.io/react-native/docs/getting-started)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f421d-110">See [React Native Getting Started](https://facebook.github.io/react-native/docs/getting-started) for instructions on configuring your development machine.</span></span> <span data-ttu-id="f421d-111">このチュートリアルで使用されているバージョンを以下に示します。</span><span class="sxs-lookup"><span data-stu-id="f421d-111">The versions used for this tutorial are listed below.</span></span> <span data-ttu-id="f421d-112">このガイドの手順は、他のバージョンでは動作しますが、テストされていません。</span><span class="sxs-lookup"><span data-stu-id="f421d-112">The steps in this guide may work with other versions, but that has not been tested.</span></span>
>
> - <span data-ttu-id="f421d-113">Android Studio バージョン 3.4.2 with 1.8.0 JRE および Android 9.0 SDK</span><span class="sxs-lookup"><span data-stu-id="f421d-113">Android Studio version 3.4.2 with the 1.8.0 JRE and the Android 9.0 SDK</span></span>
> - <span data-ttu-id="f421d-114">Java 開発キットバージョン12.0.2</span><span class="sxs-lookup"><span data-stu-id="f421d-114">Java Development Kit version 12.0.2</span></span>
> - <span data-ttu-id="f421d-115">Xcode version 10.3</span><span class="sxs-lookup"><span data-stu-id="f421d-115">Xcode version 10.3</span></span>
> - <span data-ttu-id="f421d-116">Node.js バージョン10.16.0</span><span class="sxs-lookup"><span data-stu-id="f421d-116">Node.js version 10.16.0</span></span>

<span data-ttu-id="f421d-117">Microsoft アカウントを持っていない場合は、無料のアカウントを取得するためのオプションがいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="f421d-117">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="f421d-118">[新しい個人用 Microsoft アカウントにサインアップ](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)することができます。</span><span class="sxs-lookup"><span data-stu-id="f421d-118">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="f421d-119">[Office 365 開発者プログラムにサインアップ](https://developer.microsoft.com/office/dev-program)して、無料の office 365 サブスクリプションを取得することができます。</span><span class="sxs-lookup"><span data-stu-id="f421d-119">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-an-application-with-the-azure-active-directory-admin-center"></a><span data-ttu-id="f421d-120">Azure Active Directory 管理センターにアプリケーションを登録する</span><span class="sxs-lookup"><span data-stu-id="f421d-120">Register an application with the Azure Active Directory admin center</span></span>

1. <span data-ttu-id="f421d-121">ブラウザーを開き、[Azure Active Directory 管理センター](https://aad.portal.azure.com)へ移動して、**個人用アカウント** (別名: Microsoft アカウント)、または**職場/学校アカウント**を使用してログインします。</span><span class="sxs-lookup"><span data-stu-id="f421d-121">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com) and login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="f421d-122">左側のナビゲーションで [ **Azure Active Directory** ] を選択し、[**管理**] の下にある [**アプリの登録**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="f421d-122">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="f421d-123">アプリの登録のスクリーンショット</span><span class="sxs-lookup"><span data-stu-id="f421d-123">A screenshot of the App registrations</span></span> ](/tutorial/images/aad-portal-app-registrations.png)

1. <span data-ttu-id="f421d-124">**[新規登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="f421d-124">Select **New registration**.</span></span> <span data-ttu-id="f421d-125">**[アプリケーションを登録]** ページで、次のように値を設定します。</span><span class="sxs-lookup"><span data-stu-id="f421d-125">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="f421d-126">`React Native Graph Tutorial` に **[名前]** を設定します。</span><span class="sxs-lookup"><span data-stu-id="f421d-126">Set **Name** to `React Native Graph Tutorial`.</span></span>
    - <span data-ttu-id="f421d-127">**[サポートされているアカウントの種類]** を **[任意の組織のディレクトリ内のアカウントと個人用の Microsoft アカウント]** に設定します。</span><span class="sxs-lookup"><span data-stu-id="f421d-127">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="f421d-128">[**リダイレクト URI**] で、ドロップダウンを [**パブリッククライアント (モバイル & デスクトップ)**] に変更し`graph-tutorial://react-native-auth`、値をに設定します。</span><span class="sxs-lookup"><span data-stu-id="f421d-128">Under **Redirect URI**, change the dropdown to **Public client (mobile & desktop)**, and set the value to `graph-tutorial://react-native-auth`.</span></span>

    ![[アプリケーションの登録] ページのスクリーンショット](/tutorial/images/aad-register-an-app.png)

1. <span data-ttu-id="f421d-130">[**登録**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="f421d-130">Select **Register**.</span></span> <span data-ttu-id="f421d-131">[**ネイティブグラフの応答] チュートリアル**ページで、**アプリケーション (クライアント) ID**の値をコピーして保存します。そのためには、次の手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f421d-131">On the **React Native Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![新しいアプリの登録のアプリケーション ID のスクリーンショット](/tutorial/images/aad-application-id.png)

1. <span data-ttu-id="f421d-133">[**管理**] で、[**認証**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="f421d-133">Under **Manage**, select **Authentication**.</span></span> <span data-ttu-id="f421d-134">[**リダイレクト uri** ] ページで、uri `urn:ietf:wg:oauth:2.0:oob`を使用して、**パブリッククライアント (モバイル & デスクトップ)** 型の別のリダイレクト URI を追加します。</span><span class="sxs-lookup"><span data-stu-id="f421d-134">On the **Redirect URIs** page, add another redirect URI of type **Public client (mobile & desktop)**, with the URI `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="f421d-135">[**保存**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="f421d-135">Select **Save**.</span></span>

    ![リダイレクト Uri ページのスクリーンショット](/tutorial/images/aad-redirect-uris.png)

## <a name="configure-the-sample"></a><span data-ttu-id="f421d-137">サンプルを構成する</span><span class="sxs-lookup"><span data-stu-id="f421d-137">Configure the sample</span></span>

1. <span data-ttu-id="f421d-138">**Graphtutorial/auth/AuthConfig .js**ファイルの名前を**authconfig**に変更します。</span><span class="sxs-lookup"><span data-stu-id="f421d-138">Rename the **GraphTutorial/auth/AuthConfig.js.example** file to **AuthConfig.js**.</span></span>
1. <span data-ttu-id="f421d-139">**Authconfig .js**ファイルを編集し、次のように変更します。</span><span class="sxs-lookup"><span data-stu-id="f421d-139">Edit the **AuthConfig.js** file and make the following changes.</span></span>
    1. <span data-ttu-id="f421d-140">を`YOUR_APP_ID_HERE`アプリ登録ポータルで取得した**アプリケーション Id**に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="f421d-140">Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the App Registration Portal.</span></span>

1. <span data-ttu-id="f421d-141">コマンドラインインターフェイス (CLI) で、 **Graphtutorial**ディレクトリに移動し、次のコマンドを実行して要件をインストールします。</span><span class="sxs-lookup"><span data-stu-id="f421d-141">In your command-line interface (CLI), navigate to the **GraphTutorial** directory and run the following command to install requirements.</span></span>

    ```Shell
    npm install
    ```

## <a name="run-the-sample"></a><span data-ttu-id="f421d-142">サンプルを実行する</span><span class="sxs-lookup"><span data-stu-id="f421d-142">Run the sample</span></span>

### <a name="run-on-ios-simulator"></a><span data-ttu-id="f421d-143">IOS シミュレータで実行する</span><span class="sxs-lookup"><span data-stu-id="f421d-143">Run on iOS Simulator</span></span>

<span data-ttu-id="f421d-144">CLI で次のコマンドを実行して、iOS シミュレータでアプリケーションを起動します。</span><span class="sxs-lookup"><span data-stu-id="f421d-144">Run the following command in your CLI to start the application in an iOS Simulator.</span></span>

```Shell
react-native run-ios
```

### <a name="run-on-android-emulator"></a><span data-ttu-id="f421d-145">Android エミュレーターで実行する</span><span class="sxs-lookup"><span data-stu-id="f421d-145">Run on Android emulator</span></span>

<span data-ttu-id="f421d-146">を起動し、android エミュレーターで次のコマンドを実行して、Android エミュレーターでアプリケーションを起動します。</span><span class="sxs-lookup"><span data-stu-id="f421d-146">Launch and Android emulator instance and run the following command in your CLI to start the application in an Android emulator.</span></span>

```Shell
react-native run-android
```
