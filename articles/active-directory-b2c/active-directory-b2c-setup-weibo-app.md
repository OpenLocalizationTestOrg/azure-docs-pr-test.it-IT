---
title: 'Azure Active Directory B2C: configurazione di Weibo | Documentazione Microsoft'
description: Fornire l'iscrizione e l'accesso agli utenti con account Weibo nelle applicazioni protette da Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1860de34-94cb-4ceb-851e-102f930f7230
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 00c5d3781455c80b33bdbb4c872ae354531baf3e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-weibo-accounts"></a><span data-ttu-id="9090c-103">Azure Active Directory B2C: fornire l'iscrizione e l'accesso agli utenti con account Weibo</span><span class="sxs-lookup"><span data-stu-id="9090c-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Weibo accounts</span></span>

> [!NOTE]
> <span data-ttu-id="9090c-104">Questa funzionalità è in anteprima.</span><span class="sxs-lookup"><span data-stu-id="9090c-104">This feature is in preview.</span></span> <span data-ttu-id="9090c-105">Non usare questo provider di identità nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="9090c-105">Do not use this identity provider in your production environment.</span></span>
> 

## <a name="create-a-weibo-application"></a><span data-ttu-id="9090c-106">Creare un'applicazione Weibo</span><span class="sxs-lookup"><span data-stu-id="9090c-106">Create a Weibo application</span></span>

<span data-ttu-id="9090c-107">Per usare Weibo come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario creare un'applicazione Weibo e inserire i parametri corretti.</span><span class="sxs-lookup"><span data-stu-id="9090c-107">To use Weibo as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Weibo application and supply it with the right parameters.</span></span> <span data-ttu-id="9090c-108">Per eseguire questa operazione è necessario un account Weibo.</span><span class="sxs-lookup"><span data-stu-id="9090c-108">You need a Weibo account to do this.</span></span> <span data-ttu-id="9090c-109">Se non si ha un account, è possibile ottenerne uno nel sito [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span><span class="sxs-lookup"><span data-stu-id="9090c-109">If you don’t have one, you can get one at [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span></span>

### <a name="register-for-the-weibo-developer-program"></a><span data-ttu-id="9090c-110">Registrazione per il programma per sviluppatori Weibo</span><span class="sxs-lookup"><span data-stu-id="9090c-110">Register for the Weibo developer program</span></span>

1. <span data-ttu-id="9090c-111">Passare al [portale per sviluppatori Weibo](http://open.weibo.com/) e accedere con le credenziali dell'account Weibo.</span><span class="sxs-lookup"><span data-stu-id="9090c-111">Go to the [Weibo developer portal](http://open.weibo.com/) and sign in with your Weibo account credentials.</span></span>
2. <span data-ttu-id="9090c-112">Dopo l'accesso, fare clic sul nome visualizzato nell'angolo superiore destro.</span><span class="sxs-lookup"><span data-stu-id="9090c-112">After signing in, click on your display name in the top-right corner.</span></span>
3. <span data-ttu-id="9090c-113">Nell'elenco a discesa selezionare**编辑开发者信息** (Modifica informazioni per gli sviluppatori).</span><span class="sxs-lookup"><span data-stu-id="9090c-113">In the dropdown, select **编辑开发者信息** (edit developer information).</span></span>
4. <span data-ttu-id="9090c-114">Immettere le informazioni necessarie nel modulo e fare clic su **下一步** (Invia).</span><span class="sxs-lookup"><span data-stu-id="9090c-114">Enter the required information into the form and click **提交** (submit).</span></span>
5. <span data-ttu-id="9090c-115">Questa operazione completerà il processo di verifica email.</span><span class="sxs-lookup"><span data-stu-id="9090c-115">Complete the email verification process.</span></span>
6. <span data-ttu-id="9090c-116">Andare alla [pagina di verifica dell'identità](http://open.weibo.com/developers/identity/edit).</span><span class="sxs-lookup"><span data-stu-id="9090c-116">Go to the [identity verification page](http://open.weibo.com/developers/identity/edit).</span></span>
7. <span data-ttu-id="9090c-117">Immettere le informazioni necessarie nel modulo e fare clic su **下一步** (Invia).</span><span class="sxs-lookup"><span data-stu-id="9090c-117">Enter the required information into the form and click **提交** (submit).</span></span>

### <a name="register-a-weibo-application"></a><span data-ttu-id="9090c-118">Registrare un'applicazione Weibo</span><span class="sxs-lookup"><span data-stu-id="9090c-118">Register a Weibo application</span></span>

1. <span data-ttu-id="9090c-119">Accedere alla [pagina per la registrazione di app Weibo](http://open.weibo.com/apps/new).</span><span class="sxs-lookup"><span data-stu-id="9090c-119">Go to the [new Weibo app registration page](http://open.weibo.com/apps/new).</span></span>
2. <span data-ttu-id="9090c-120">Immettere le informazioni sull'applicazione necessarie.</span><span class="sxs-lookup"><span data-stu-id="9090c-120">Enter the necessary application information.</span></span>
3. <span data-ttu-id="9090c-121">Fare clic su **创建** (Crea).</span><span class="sxs-lookup"><span data-stu-id="9090c-121">Click **创建** (create).</span></span>
4. <span data-ttu-id="9090c-122">Copiare i valori della **chiave app** e del **segreto app**.</span><span class="sxs-lookup"><span data-stu-id="9090c-122">Copy the values of **App Key** and **App Secret**.</span></span> <span data-ttu-id="9090c-123">che sarà necessario più avanti.</span><span class="sxs-lookup"><span data-stu-id="9090c-123">You will need this later.</span></span>
5. <span data-ttu-id="9090c-124">Caricare le foto necessarie e immettere le informazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="9090c-124">Upload the required photos and enter the necessary information.</span></span>
6. <span data-ttu-id="9090c-125">Fare clic su **保存以上信息** (Salva).</span><span class="sxs-lookup"><span data-stu-id="9090c-125">Click **保存以上信息** (save).</span></span>
7. <span data-ttu-id="9090c-126">Fare clic su **高级信息** (Informazioni avanzate).</span><span class="sxs-lookup"><span data-stu-id="9090c-126">Click **高级信息** (advanced information).</span></span>
8. <span data-ttu-id="9090c-127">Fare clic su **编辑** (Modifica) accanto al campo per OAuth 2.0**授权设置** (URL di reindirizzamento).</span><span class="sxs-lookup"><span data-stu-id="9090c-127">Click **编辑** (edit) next to the field for OAuth2.0 **授权设置** (redirect URL).</span></span>
9. <span data-ttu-id="9090c-128">Immettere `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` per OAuth 2.0**授权设置** (URL di reindirizzamento).</span><span class="sxs-lookup"><span data-stu-id="9090c-128">Enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` for OAuth2.0 **授权设置** (redirect URL).</span></span> <span data-ttu-id="9090c-129">Ad esempio, se `tenant_name` è contoso.onmicrosoft.com, impostare l'URL a `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="9090c-129">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
10. <span data-ttu-id="9090c-130">Fare clic su **提交** (Invia).</span><span class="sxs-lookup"><span data-stu-id="9090c-130">Click **提交** (submit).</span></span>  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="9090c-131">Configurare Weibo come provider di identità nel tenant</span><span class="sxs-lookup"><span data-stu-id="9090c-131">Configure Weibo as an identity provider in your tenant</span></span>
1. <span data-ttu-id="9090c-132">Seguire questa procedura per [passare al pannello delle funzionalità B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9090c-132">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="9090c-133">Nel pannello delle funzionalità di B2C, fare clic su **Provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="9090c-133">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="9090c-134">Fare clic su **+Aggiungi** nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="9090c-134">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="9090c-135">Fornire un **Nome** per la configurazione del provider di identità.</span><span class="sxs-lookup"><span data-stu-id="9090c-135">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="9090c-136">ad esempio, immettere "Weibo".</span><span class="sxs-lookup"><span data-stu-id="9090c-136">For example, enter "Weibo".</span></span>
5. <span data-ttu-id="9090c-137">Fare clic su **Tipo di provider di identità**, selezionare **Weibo** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9090c-137">Click **Identity provider type**, select **Weibo**, and click **OK**.</span></span>
6. <span data-ttu-id="9090c-138">Fare clic su **Configura questo provider di identità**</span><span class="sxs-lookup"><span data-stu-id="9090c-138">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="9090c-139">Immettere la **chiave app** copiata in precedenza come **ID client**.</span><span class="sxs-lookup"><span data-stu-id="9090c-139">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="9090c-140">Immettere il **segreto app** copiato in precedenza come **segreto client**.</span><span class="sxs-lookup"><span data-stu-id="9090c-140">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="9090c-141">Fare clic su **OK** e su **Crea** per salvare la configurazione di Weibo.</span><span class="sxs-lookup"><span data-stu-id="9090c-141">Click **OK** and then click **Create** to save your Weibo configuration.</span></span>

