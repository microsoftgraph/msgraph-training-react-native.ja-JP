<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="9789e-101">この手順では、Azure Active Directory 管理センターを使用して、新しい Azure AD ネイティブアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="9789e-101">In this exercise you will create a new Azure AD native application using the Azure Active Directory admin center.</span></span>

1. <span data-ttu-id="9789e-102">ブラウザーを開き、[Azure Active Directory 管理センター](https://aad.portal.azure.com)へ移動して、**個人用アカウント** (別名: Microsoft アカウント)、または**職場/学校アカウント**を使用してログインします。</span><span class="sxs-lookup"><span data-stu-id="9789e-102">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com) and login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="9789e-103">左側のナビゲーションで [ **Azure Active Directory** ] を選択し、[**管理**] の下にある [**アプリの登録**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="9789e-103">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="9789e-104">アプリの登録のスクリーンショット</span><span class="sxs-lookup"><span data-stu-id="9789e-104">A screenshot of the App registrations</span></span> ](./images/aad-portal-app-registrations.png)

1. <span data-ttu-id="9789e-105">**[新規登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="9789e-105">Select **New registration**.</span></span> <span data-ttu-id="9789e-106">**[アプリケーションを登録]** ページで、次のように値を設定します。</span><span class="sxs-lookup"><span data-stu-id="9789e-106">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="9789e-107">`React Native Graph Tutorial` に **[名前]** を設定します。</span><span class="sxs-lookup"><span data-stu-id="9789e-107">Set **Name** to `React Native Graph Tutorial`.</span></span>
    - <span data-ttu-id="9789e-108">**[サポートされているアカウントの種類]** を **[任意の組織のディレクトリ内のアカウントと個人用の Microsoft アカウント]** に設定します。</span><span class="sxs-lookup"><span data-stu-id="9789e-108">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="9789e-109">[**リダイレクト URI**] で、ドロップダウンを [**パブリッククライアント (モバイル & デスクトップ)**] に変更し`graph-tutorial://react-native-auth`、値をに設定します。</span><span class="sxs-lookup"><span data-stu-id="9789e-109">Under **Redirect URI**, change the dropdown to **Public client (mobile & desktop)**, and set the value to `graph-tutorial://react-native-auth`.</span></span>

    ![[アプリケーションの登録] ページのスクリーンショット](./images/aad-register-an-app.png)

1. <span data-ttu-id="9789e-111">[**登録**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="9789e-111">Select **Register**.</span></span> <span data-ttu-id="9789e-112">[**ネイティブグラフの応答] チュートリアル**ページで、**アプリケーション (クライアント) ID**の値をコピーして保存します。そのためには、次の手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9789e-112">On the **React Native Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![新しいアプリの登録のアプリケーション ID のスクリーンショット](./images/aad-application-id.png)

1. <span data-ttu-id="9789e-114">[**管理**] で、[**認証**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="9789e-114">Under **Manage**, select **Authentication**.</span></span> <span data-ttu-id="9789e-115">[**リダイレクト uri** ] ページで、uri `urn:ietf:wg:oauth:2.0:oob`を使用して、**パブリッククライアント (モバイル & デスクトップ)** 型の別のリダイレクト URI を追加します。</span><span class="sxs-lookup"><span data-stu-id="9789e-115">On the **Redirect URIs** page, add another redirect URI of type **Public client (mobile & desktop)**, with the URI `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="9789e-116">[**保存**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="9789e-116">Select **Save**.</span></span>

    ![リダイレクト Uri ページのスクリーンショット](./images/aad-redirect-uris.png)
