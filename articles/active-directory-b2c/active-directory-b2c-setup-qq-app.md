---
title: 'Azure Active Directory B2C: configurazione di QQ | Documentazione Microsoft'
description: Fornire tooconsumers iscrizione e Accedi con account q nelle applicazioni che sono protetti da Azure Active Directory B2C.
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
ms.openlocfilehash: 896d6221e01d15de1652a5717cf1f65619101e0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-qq-accounts"></a><span data-ttu-id="0da6f-103">Azure Active B2C di Directory: Fornire tooconsumers iscrizione e Accedi con account q</span><span class="sxs-lookup"><span data-stu-id="0da6f-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with QQ accounts</span></span>

> [!NOTE]
> <span data-ttu-id="0da6f-104">Questa funzionalità è in anteprima.</span><span class="sxs-lookup"><span data-stu-id="0da6f-104">This feature is in preview.</span></span>
> 

## <a name="create-a-qq-application"></a><span data-ttu-id="0da6f-105">Creare un'applicazione QQ</span><span class="sxs-lookup"><span data-stu-id="0da6f-105">Create a QQ application</span></span>

<span data-ttu-id="0da6f-106">toouse q come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un'applicazione di q e fornirlo con i parametri corretti hello.</span><span class="sxs-lookup"><span data-stu-id="0da6f-106">toouse QQ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a QQ application and supply it with hello right parameters.</span></span> <span data-ttu-id="0da6f-107">Necessaria una toodo account q.</span><span class="sxs-lookup"><span data-stu-id="0da6f-107">You need a QQ account toodo this.</span></span> <span data-ttu-id="0da6f-108">Se non si ha un account, è possibile ottenerne uno nel sito [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span><span class="sxs-lookup"><span data-stu-id="0da6f-108">If you don’t have one, you can get one at [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span></span>

### <a name="register-for-hello-qq-developer-program"></a><span data-ttu-id="0da6f-109">Registrarsi al programma per sviluppatori di hello q</span><span class="sxs-lookup"><span data-stu-id="0da6f-109">Register for hello QQ developer program</span></span>

1. <span data-ttu-id="0da6f-110">Passare toohello [portale per sviluppatori q](http://open.qq.com) e accedere con le credenziali dell'account q.</span><span class="sxs-lookup"><span data-stu-id="0da6f-110">Go toohello [QQ developer portal](http://open.qq.com) and sign in with your QQ account credentials.</span></span>
2. <span data-ttu-id="0da6f-111">Dopo avere effettuato l'accesso, andare troppo[http://open.qq.com/reg](http://open.qq.com/reg) tooregister manualmente gli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="0da6f-111">After signing in, go too[http://open.qq.com/reg](http://open.qq.com/reg) tooregister yourself as a developer.</span></span>
3. <span data-ttu-id="0da6f-112">Selezionare menu hello**个人**(developer singoli).</span><span class="sxs-lookup"><span data-stu-id="0da6f-112">In hello menu, select **个人** (individual developer).</span></span>
4. <span data-ttu-id="0da6f-113">Immettere le informazioni necessarie hello nel modulo di hello e fare clic su**下一步**(passaggio successivo).</span><span class="sxs-lookup"><span data-stu-id="0da6f-113">Enter hello required information into hello form and click **下一步** (next step).</span></span>
5. <span data-ttu-id="0da6f-114">Completamento del processo di verifica tramite posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="0da6f-114">Complete hello email verification process.</span></span>

> [!NOTE]
> <span data-ttu-id="0da6f-115">È necessario toowait alcuni toobe giorni approvato dopo la registrazione come uno sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="0da6f-115">You will need toowait a few days toobe approved after registering as a developer.</span></span> 

### <a name="register-a-qq-application"></a><span data-ttu-id="0da6f-116">Registrare un'applicazione QQ</span><span class="sxs-lookup"><span data-stu-id="0da6f-116">Register a QQ application</span></span>

1. <span data-ttu-id="0da6f-117">Andare troppo[https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span><span class="sxs-lookup"><span data-stu-id="0da6f-117">Go too[https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span></span>
2. <span data-ttu-id="0da6f-118">Fare clic su **应用管理** (Gestione app).</span><span class="sxs-lookup"><span data-stu-id="0da6f-118">Click on **应用管理** (app management).</span></span>
3. <span data-ttu-id="0da6f-119">Fare clic su **创建应用** (Crea app).</span><span class="sxs-lookup"><span data-stu-id="0da6f-119">Click on **创建应用** (create app).</span></span>
4. <span data-ttu-id="0da6f-120">Immettere le informazioni necessarie app hello.</span><span class="sxs-lookup"><span data-stu-id="0da6f-120">Enter hello necessary app information.</span></span>
5. <span data-ttu-id="0da6f-121">Fare clic su **创建应用** (Crea app).</span><span class="sxs-lookup"><span data-stu-id="0da6f-121">Click on **创建应用** (create app).</span></span>
6. <span data-ttu-id="0da6f-122">Immettere le informazioni necessarie hello.</span><span class="sxs-lookup"><span data-stu-id="0da6f-122">Enter hello required information.</span></span>
7. <span data-ttu-id="0da6f-123">Per hello**授权回调域**(URL callback) immettere `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="0da6f-123">For hello **授权回调域** (callback URL) field, enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="0da6f-124">Ad esempio, se il `tenant_name` è contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="0da6f-124">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
8. <span data-ttu-id="0da6f-125">Fare clic su **创建应用** (Crea app).</span><span class="sxs-lookup"><span data-stu-id="0da6f-125">Click on **创建应用** (create app).</span></span>
9. <span data-ttu-id="0da6f-126">Nella pagina di conferma hello, fare clic su**应用管理**pagina di gestione app toohello tooreturn (gestione delle app).</span><span class="sxs-lookup"><span data-stu-id="0da6f-126">On hello confirmation page, click on **应用管理** (app management) tooreturn toohello app management page.</span></span>
10. <span data-ttu-id="0da6f-127">Fare clic su**查看**(visualizzazione) prossima toohello applicazione appena creato.</span><span class="sxs-lookup"><span data-stu-id="0da6f-127">Click on **查看** (view) next toohello app you just created.</span></span>
11. <span data-ttu-id="0da6f-128">Fare clic su **修改** (Modifica).</span><span class="sxs-lookup"><span data-stu-id="0da6f-128">Click on **修改** (edit).</span></span>
12. <span data-ttu-id="0da6f-129">Dall'alto hello della pagina hello, copiare hello **ID APP** e **chiave APP**.</span><span class="sxs-lookup"><span data-stu-id="0da6f-129">From hello top of hello page, copy hello **APP ID** and **APP KEY**.</span></span>

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="0da6f-130">Configurare QQ come provider di identità nel tenant</span><span class="sxs-lookup"><span data-stu-id="0da6f-130">Configure QQ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="0da6f-131">Seguire questi passaggi troppo[passare pannello funzionalità toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) su hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0da6f-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="0da6f-132">Nel Pannello di hello B2C funzionalità, fare clic su **provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="0da6f-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="0da6f-133">Fare clic su **+ Aggiungi** nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="0da6f-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="0da6f-134">Fornire un nome **nome** per la configurazione del provider di identità hello.</span><span class="sxs-lookup"><span data-stu-id="0da6f-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="0da6f-135">Ad esempio, immettere "QQ".</span><span class="sxs-lookup"><span data-stu-id="0da6f-135">For example, enter "QQ".</span></span>
5. <span data-ttu-id="0da6f-136">Fare clic su **Tipo di provider di identità**, selezionare **QQ** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0da6f-136">Click **Identity provider type**, select **QQ**, and click **OK**.</span></span>
6. <span data-ttu-id="0da6f-137">Fare clic su **Configura questo provider di identità**</span><span class="sxs-lookup"><span data-stu-id="0da6f-137">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="0da6f-138">Immettere hello **chiave App** copiato in precedenza come hello **ID Client**.</span><span class="sxs-lookup"><span data-stu-id="0da6f-138">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="0da6f-139">Immettere hello **segreto dell'App** copiato in precedenza come hello **segreto Client**.</span><span class="sxs-lookup"><span data-stu-id="0da6f-139">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="0da6f-140">Fare clic su **OK** e quindi fare clic su **crea** toosave configurazione q.</span><span class="sxs-lookup"><span data-stu-id="0da6f-140">Click **OK** and then click **Create** toosave your QQ configuration.</span></span>

