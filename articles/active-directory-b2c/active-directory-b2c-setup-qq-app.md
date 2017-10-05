---
title: 'Azure Active Directory B2C: configurazione di QQ | Documentazione Microsoft'
description: Fornire l'iscrizione e l'accesso agli utenti con account QQ nelle applicazioni protette da Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 18c2cf94-8004-4de1-81c2-e45be65ce12d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: b32e81494b8c84799485f154ae43ad30af394caa
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-qq-accounts"></a><span data-ttu-id="2fa24-103">Azure Active Directory B2C: fornire l'iscrizione e l'accesso agli utenti con account QQ</span><span class="sxs-lookup"><span data-stu-id="2fa24-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with QQ accounts</span></span>

> [!NOTE]
> <span data-ttu-id="2fa24-104">Questa funzionalità è in anteprima.</span><span class="sxs-lookup"><span data-stu-id="2fa24-104">This feature is in preview.</span></span>
> 

## <a name="create-a-qq-application"></a><span data-ttu-id="2fa24-105">Creare un'applicazione QQ</span><span class="sxs-lookup"><span data-stu-id="2fa24-105">Create a QQ application</span></span>

<span data-ttu-id="2fa24-106">Per usare QQ come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario creare un'applicazione QQ e inserire i parametri corretti.</span><span class="sxs-lookup"><span data-stu-id="2fa24-106">To use QQ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a QQ application and supply it with the right parameters.</span></span> <span data-ttu-id="2fa24-107">Per eseguire questa operazione è necessario disporre di un account QQ.</span><span class="sxs-lookup"><span data-stu-id="2fa24-107">You need a QQ account to do this.</span></span> <span data-ttu-id="2fa24-108">Se non si ha un account, è possibile ottenerne uno nel sito [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span><span class="sxs-lookup"><span data-stu-id="2fa24-108">If you don’t have one, you can get one at [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span></span>

### <a name="register-for-the-qq-developer-program"></a><span data-ttu-id="2fa24-109">Registrazione per il programma per sviluppatori QQ</span><span class="sxs-lookup"><span data-stu-id="2fa24-109">Register for the QQ developer program</span></span>

1. <span data-ttu-id="2fa24-110">Passare al [portale per sviluppatori QQ](http://open.qq.com) e accedere con le credenziali dell'account QQ.</span><span class="sxs-lookup"><span data-stu-id="2fa24-110">Go to the [QQ developer portal](http://open.qq.com) and sign in with your QQ account credentials.</span></span>
2. <span data-ttu-id="2fa24-111">Dopo l'accesso, passare a [http://open.qq.com/reg](http://open.qq.com/reg) per registrarsi come sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="2fa24-111">After signing in, go to [http://open.qq.com/reg](http://open.qq.com/reg) to register yourself as a developer.</span></span>
3. <span data-ttu-id="2fa24-112">Nel menu selezionare**个人** (Singolo sviluppatore).</span><span class="sxs-lookup"><span data-stu-id="2fa24-112">In the menu, select **个人** (individual developer).</span></span>
4. <span data-ttu-id="2fa24-113">Immettere le informazioni necessarie nel modulo e fare clic su**下一步** (Passaggio successivo).</span><span class="sxs-lookup"><span data-stu-id="2fa24-113">Enter the required information into the form and click **下一步** (next step).</span></span>
5. <span data-ttu-id="2fa24-114">Questa operazione completerà il processo di verifica email.</span><span class="sxs-lookup"><span data-stu-id="2fa24-114">Complete the email verification process.</span></span>

> [!NOTE]
> <span data-ttu-id="2fa24-115">È necessario attendere l'approvazione per alcuni giorni dopo la registrazione come sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="2fa24-115">You will need to wait a few days to be approved after registering as a developer.</span></span> 

### <a name="register-a-qq-application"></a><span data-ttu-id="2fa24-116">Registrare un'applicazione QQ</span><span class="sxs-lookup"><span data-stu-id="2fa24-116">Register a QQ application</span></span>

1. <span data-ttu-id="2fa24-117">Passare a [https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span><span class="sxs-lookup"><span data-stu-id="2fa24-117">Go to [https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span></span>
2. <span data-ttu-id="2fa24-118">Fare clic su **应用管理** (Gestione app).</span><span class="sxs-lookup"><span data-stu-id="2fa24-118">Click on **应用管理** (app management).</span></span>
3. <span data-ttu-id="2fa24-119">Fare clic su **创建应用** (Crea app).</span><span class="sxs-lookup"><span data-stu-id="2fa24-119">Click on **创建应用** (create app).</span></span>
4. <span data-ttu-id="2fa24-120">Immettere le informazioni di connessione necessarie.</span><span class="sxs-lookup"><span data-stu-id="2fa24-120">Enter the necessary app information.</span></span>
5. <span data-ttu-id="2fa24-121">Fare clic su **创建应用** (Crea app).</span><span class="sxs-lookup"><span data-stu-id="2fa24-121">Click on **创建应用** (create app).</span></span>
6. <span data-ttu-id="2fa24-122">Immettere le informazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="2fa24-122">Enter the required information.</span></span>
7. <span data-ttu-id="2fa24-123">Per il campo **授权回调域** (URL di callback) immettere `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="2fa24-123">For the **授权回调域** (callback URL) field, enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="2fa24-124">Ad esempio, se `tenant_name` è contoso.onmicrosoft.com, impostare l'URL a `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="2fa24-124">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
8. <span data-ttu-id="2fa24-125">Fare clic su **创建应用** (Crea app).</span><span class="sxs-lookup"><span data-stu-id="2fa24-125">Click on **创建应用** (create app).</span></span>
9. <span data-ttu-id="2fa24-126">Nella pagina di conferma fare clic su**应用管理** (Gestione app) per tornare alla pagina di gestione delle app.</span><span class="sxs-lookup"><span data-stu-id="2fa24-126">On the confirmation page, click on **应用管理** (app management) to return to the app management page.</span></span>
10. <span data-ttu-id="2fa24-127">Fare clic su **查看**(Visualizza) accanto all'app appena creata.</span><span class="sxs-lookup"><span data-stu-id="2fa24-127">Click on **查看** (view) next to the app you just created.</span></span>
11. <span data-ttu-id="2fa24-128">Fare clic su **修改** (Modifica).</span><span class="sxs-lookup"><span data-stu-id="2fa24-128">Click on **修改** (edit).</span></span>
12. <span data-ttu-id="2fa24-129">Nella parte superiore della pagina copiare l'**ID APP** e la **CHIAVE APP**.</span><span class="sxs-lookup"><span data-stu-id="2fa24-129">From the top of the page, copy the **APP ID** and **APP KEY**.</span></span>

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="2fa24-130">Configurare QQ come provider di identità nel tenant</span><span class="sxs-lookup"><span data-stu-id="2fa24-130">Configure QQ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="2fa24-131">Seguire questa procedura per [passare al pannello delle funzionalità B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2fa24-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="2fa24-132">Nel pannello delle funzionalità di B2C, fare clic su **Provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="2fa24-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="2fa24-133">Fare clic su **+Aggiungi** nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="2fa24-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="2fa24-134">Fornire un **Nome** per la configurazione del provider di identità.</span><span class="sxs-lookup"><span data-stu-id="2fa24-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="2fa24-135">Ad esempio, immettere "QQ".</span><span class="sxs-lookup"><span data-stu-id="2fa24-135">For example, enter "QQ".</span></span>
5. <span data-ttu-id="2fa24-136">Fare clic su **Tipo di provider di identità**, selezionare **QQ** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2fa24-136">Click **Identity provider type**, select **QQ**, and click **OK**.</span></span>
6. <span data-ttu-id="2fa24-137">Fare clic su **Configura questo provider di identità**</span><span class="sxs-lookup"><span data-stu-id="2fa24-137">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="2fa24-138">Immettere la **chiave app** copiata in precedenza come **ID client**.</span><span class="sxs-lookup"><span data-stu-id="2fa24-138">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="2fa24-139">Immettere il **segreto app** copiato in precedenza come **segreto client**.</span><span class="sxs-lookup"><span data-stu-id="2fa24-139">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="2fa24-140">Fare clic su **OK** e su **Crea** per salvare la configurazione di QQ.</span><span class="sxs-lookup"><span data-stu-id="2fa24-140">Click **OK** and then click **Create** to save your QQ configuration.</span></span>

