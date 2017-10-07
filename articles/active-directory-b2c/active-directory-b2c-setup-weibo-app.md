---
title: 'Azure Active Directory B2C: configurazione di Weibo | Documentazione Microsoft'
description: Fornire tooconsumers iscrizione e Accedi con account Weibo nelle applicazioni che sono protetti da Azure Active Directory B2C.
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
ms.openlocfilehash: c0648620f318046c1d9d24feb92a0c5f19c6a91a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-weibo-accounts"></a><span data-ttu-id="80411-103">Azure B2C di Directory Active: Fornire tooconsumers iscrizione e Accedi con account Weibo</span><span class="sxs-lookup"><span data-stu-id="80411-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Weibo accounts</span></span>

> [!NOTE]
> <span data-ttu-id="80411-104">Questa funzionalità è in anteprima.</span><span class="sxs-lookup"><span data-stu-id="80411-104">This feature is in preview.</span></span> <span data-ttu-id="80411-105">Non usare questo provider di identità nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="80411-105">Do not use this identity provider in your production environment.</span></span>
> 

## <a name="create-a-weibo-application"></a><span data-ttu-id="80411-106">Creare un'applicazione Weibo</span><span class="sxs-lookup"><span data-stu-id="80411-106">Create a Weibo application</span></span>

<span data-ttu-id="80411-107">toouse Weibo come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un'applicazione Weibo e fornirlo con i parametri corretti hello.</span><span class="sxs-lookup"><span data-stu-id="80411-107">toouse Weibo as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Weibo application and supply it with hello right parameters.</span></span> <span data-ttu-id="80411-108">È necessario un toodo account Weibo questo.</span><span class="sxs-lookup"><span data-stu-id="80411-108">You need a Weibo account toodo this.</span></span> <span data-ttu-id="80411-109">Se non si ha un account, è possibile ottenerne uno nel sito [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span><span class="sxs-lookup"><span data-stu-id="80411-109">If you don’t have one, you can get one at [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span></span>

### <a name="register-for-hello-weibo-developer-program"></a><span data-ttu-id="80411-110">Registrarsi al programma per sviluppatori di hello Weibo</span><span class="sxs-lookup"><span data-stu-id="80411-110">Register for hello Weibo developer program</span></span>

1. <span data-ttu-id="80411-111">Passare toohello [portale per sviluppatori Weibo](http://open.weibo.com/) e accedere con le credenziali dell'account Weibo.</span><span class="sxs-lookup"><span data-stu-id="80411-111">Go toohello [Weibo developer portal](http://open.weibo.com/) and sign in with your Weibo account credentials.</span></span>
2. <span data-ttu-id="80411-112">Dopo aver effettuato l'accesso, fare clic sul nome visualizzato nell'angolo superiore destro di hello.</span><span class="sxs-lookup"><span data-stu-id="80411-112">After signing in, click on your display name in hello top-right corner.</span></span>
3. <span data-ttu-id="80411-113">Nell'elenco a discesa hello, selezionare**编辑开发者信息**(informazioni per gli sviluppatori di modifica).</span><span class="sxs-lookup"><span data-stu-id="80411-113">In hello dropdown, select **编辑开发者信息** (edit developer information).</span></span>
4. <span data-ttu-id="80411-114">Immettere le informazioni necessarie hello nel modulo di hello e fare clic su**提交**(Invia).</span><span class="sxs-lookup"><span data-stu-id="80411-114">Enter hello required information into hello form and click **提交** (submit).</span></span>
5. <span data-ttu-id="80411-115">Completamento del processo di verifica tramite posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="80411-115">Complete hello email verification process.</span></span>
6. <span data-ttu-id="80411-116">Passare toohello [pagina Verifica identità](http://open.weibo.com/developers/identity/edit).</span><span class="sxs-lookup"><span data-stu-id="80411-116">Go toohello [identity verification page](http://open.weibo.com/developers/identity/edit).</span></span>
7. <span data-ttu-id="80411-117">Immettere le informazioni necessarie hello nel modulo di hello e fare clic su**提交**(Invia).</span><span class="sxs-lookup"><span data-stu-id="80411-117">Enter hello required information into hello form and click **提交** (submit).</span></span>

### <a name="register-a-weibo-application"></a><span data-ttu-id="80411-118">Registrare un'applicazione Weibo</span><span class="sxs-lookup"><span data-stu-id="80411-118">Register a Weibo application</span></span>

1. <span data-ttu-id="80411-119">Passare toohello [nuova pagina di registrazione app Weibo](http://open.weibo.com/apps/new).</span><span class="sxs-lookup"><span data-stu-id="80411-119">Go toohello [new Weibo app registration page](http://open.weibo.com/apps/new).</span></span>
2. <span data-ttu-id="80411-120">Immettere le informazioni necessarie applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="80411-120">Enter hello necessary application information.</span></span>
3. <span data-ttu-id="80411-121">Fare clic su **创建** (Crea).</span><span class="sxs-lookup"><span data-stu-id="80411-121">Click **创建** (create).</span></span>
4. <span data-ttu-id="80411-122">Copiare i valori hello di **chiave App** e **segreto dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="80411-122">Copy hello values of **App Key** and **App Secret**.</span></span> <span data-ttu-id="80411-123">che sarà necessario più avanti.</span><span class="sxs-lookup"><span data-stu-id="80411-123">You will need this later.</span></span>
5. <span data-ttu-id="80411-124">Caricare le foto hello necessarie e immettere le informazioni necessarie hello.</span><span class="sxs-lookup"><span data-stu-id="80411-124">Upload hello required photos and enter hello necessary information.</span></span>
6. <span data-ttu-id="80411-125">Fare clic su **保存以上信息** (Salva).</span><span class="sxs-lookup"><span data-stu-id="80411-125">Click **保存以上信息** (save).</span></span>
7. <span data-ttu-id="80411-126">Fare clic su **高级信息** (Informazioni avanzate).</span><span class="sxs-lookup"><span data-stu-id="80411-126">Click **高级信息** (advanced information).</span></span>
8. <span data-ttu-id="80411-127">Fare clic su**编辑**campo successivo toohello (modifica) per OAuth 2.0**授权设置**(URL di reindirizzamento).</span><span class="sxs-lookup"><span data-stu-id="80411-127">Click **编辑** (edit) next toohello field for OAuth2.0 **授权设置** (redirect URL).</span></span>
9. <span data-ttu-id="80411-128">Immettere `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` per OAuth 2.0**授权设置** (URL di reindirizzamento).</span><span class="sxs-lookup"><span data-stu-id="80411-128">Enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` for OAuth2.0 **授权设置** (redirect URL).</span></span> <span data-ttu-id="80411-129">Ad esempio, se il `tenant_name` è contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="80411-129">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
10. <span data-ttu-id="80411-130">Fare clic su **提交** (Invia).</span><span class="sxs-lookup"><span data-stu-id="80411-130">Click **提交** (submit).</span></span>  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="80411-131">Configurare Weibo come provider di identità nel tenant</span><span class="sxs-lookup"><span data-stu-id="80411-131">Configure Weibo as an identity provider in your tenant</span></span>
1. <span data-ttu-id="80411-132">Seguire questi passaggi troppo[passare pannello funzionalità toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) su hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="80411-132">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="80411-133">Nel Pannello di hello B2C funzionalità, fare clic su **provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="80411-133">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="80411-134">Fare clic su **+ Aggiungi** nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="80411-134">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="80411-135">Fornire un nome **nome** per la configurazione del provider di identità hello.</span><span class="sxs-lookup"><span data-stu-id="80411-135">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="80411-136">ad esempio, immettere "Weibo".</span><span class="sxs-lookup"><span data-stu-id="80411-136">For example, enter "Weibo".</span></span>
5. <span data-ttu-id="80411-137">Fare clic su **Tipo di provider di identità**, selezionare **Weibo** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="80411-137">Click **Identity provider type**, select **Weibo**, and click **OK**.</span></span>
6. <span data-ttu-id="80411-138">Fare clic su **Configura questo provider di identità**</span><span class="sxs-lookup"><span data-stu-id="80411-138">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="80411-139">Immettere hello **chiave App** copiato in precedenza come hello **ID Client**.</span><span class="sxs-lookup"><span data-stu-id="80411-139">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="80411-140">Immettere hello **segreto dell'App** copiato in precedenza come hello **segreto Client**.</span><span class="sxs-lookup"><span data-stu-id="80411-140">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="80411-141">Fare clic su **OK** e quindi fare clic su **crea** toosave configurazione Weibo.</span><span class="sxs-lookup"><span data-stu-id="80411-141">Click **OK** and then click **Create** toosave your Weibo configuration.</span></span>

