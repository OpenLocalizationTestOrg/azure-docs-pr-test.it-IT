---
title: 'Azure Active Directory B2C: configurazione di WeChat | Documentazione Microsoft'
description: Fornire tooconsumers iscrizione e Accedi con account WeChat nelle applicazioni che sono protetti da Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d2424c66-ba68-4d82-847e-d137683527b0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 92cc3579d818d2379a503ccc695138b33a34466d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-wechat-accounts"></a><span data-ttu-id="95781-103">Azure B2C di Directory Active: Fornire tooconsumers iscrizione e Accedi con account WeChat</span><span class="sxs-lookup"><span data-stu-id="95781-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with WeChat accounts</span></span>

> [!NOTE]
> <span data-ttu-id="95781-104">Questa funzionalità è in anteprima.</span><span class="sxs-lookup"><span data-stu-id="95781-104">This feature is in preview.</span></span>
> 

## <a name="create-a-wechat-application"></a><span data-ttu-id="95781-105">Creare un'applicazione WeChat</span><span class="sxs-lookup"><span data-stu-id="95781-105">Create a WeChat application</span></span>

<span data-ttu-id="95781-106">toouse WeChat come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un'applicazione WeChat e fornirlo con i parametri corretti hello.</span><span class="sxs-lookup"><span data-stu-id="95781-106">toouse WeChat as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a WeChat application and supply it with hello right parameters.</span></span> <span data-ttu-id="95781-107">È necessario un toodo account WeChat questo.</span><span class="sxs-lookup"><span data-stu-id="95781-107">You need a WeChat account toodo this.</span></span> <span data-ttu-id="95781-108">Se non si dispone di un account, è possibile ottenerne uno eseguendo l'iscrizione tramite una delle App per dispositivi mobili o usano il numero QQ.</span><span class="sxs-lookup"><span data-stu-id="95781-108">If you don’t have one, you can get one by signing up through one of their mobile apps or by using your QQ number.</span></span> <span data-ttu-id="95781-109">Successivamente, ottenere l'account registrato con programma per sviluppatori di hello WeChat.</span><span class="sxs-lookup"><span data-stu-id="95781-109">After that, get your account registered with hello WeChat developer program.</span></span> <span data-ttu-id="95781-110">Altre informazioni sono disponibili [qui](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span><span class="sxs-lookup"><span data-stu-id="95781-110">You can find more information [here](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span></span>

### <a name="register-a-wechat-application"></a><span data-ttu-id="95781-111">Registrare un'applicazione WeChat</span><span class="sxs-lookup"><span data-stu-id="95781-111">Register a WeChat application</span></span>

1. <span data-ttu-id="95781-112">Andare troppo[https://open.weixin.qq.com/](https://open.weixin.qq.com/) ed effettuare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="95781-112">Go too[https://open.weixin.qq.com/](https://open.weixin.qq.com/) and log in.</span></span>
2. <span data-ttu-id="95781-113">Fare clic su **管理中心** (Centro di gestione).</span><span class="sxs-lookup"><span data-stu-id="95781-113">Click on **管理中心** (management center).</span></span>
3. <span data-ttu-id="95781-114">Seguire hello necessarie tooregister una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="95781-114">Follow hello necessary steps tooregister a new application.</span></span>
4. <span data-ttu-id="95781-115">Per **授权回调域** (URL di callback) immettere `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="95781-115">For **授权回调域** (callback URL), enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="95781-116">Ad esempio, se il `tenant_name` è contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="95781-116">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
5. <span data-ttu-id="95781-117">Trovare e copiare hello **ID APP** e **chiave APP**.</span><span class="sxs-lookup"><span data-stu-id="95781-117">Find and copy hello **APP ID** and **APP KEY**.</span></span> <span data-ttu-id="95781-118">che verranno usati in seguito.</span><span class="sxs-lookup"><span data-stu-id="95781-118">You will need these later.</span></span>

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="95781-119">Configurare WeChat come provider di identità nel tenant,</span><span class="sxs-lookup"><span data-stu-id="95781-119">Configure WeChat as an identity provider in your tenant</span></span>
1. <span data-ttu-id="95781-120">Seguire questi passaggi troppo[passare pannello funzionalità toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) su hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="95781-120">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="95781-121">Nel Pannello di hello B2C funzionalità, fare clic su **provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="95781-121">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="95781-122">Fare clic su **+ Aggiungi** nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="95781-122">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="95781-123">Fornire un nome **nome** per la configurazione del provider di identità hello.</span><span class="sxs-lookup"><span data-stu-id="95781-123">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="95781-124">ad esempio, immettere "WeChat".</span><span class="sxs-lookup"><span data-stu-id="95781-124">For example, enter "WeChat".</span></span>
5. <span data-ttu-id="95781-125">Fare clic su **Tipo di provider di identità**, selezionare **WeChat** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="95781-125">Click **Identity provider type**, select **WeChat**, and click **OK**.</span></span>
6. <span data-ttu-id="95781-126">Fare clic su **Configura questo provider di identità**</span><span class="sxs-lookup"><span data-stu-id="95781-126">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="95781-127">Immettere hello **chiave App** copiato in precedenza come hello **ID Client**.</span><span class="sxs-lookup"><span data-stu-id="95781-127">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="95781-128">Immettere hello **segreto dell'App** copiato in precedenza come hello **segreto Client**.</span><span class="sxs-lookup"><span data-stu-id="95781-128">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="95781-129">Fare clic su **OK** e quindi fare clic su **crea** toosave configurazione WeChat.</span><span class="sxs-lookup"><span data-stu-id="95781-129">Click **OK** and then click **Create** toosave your WeChat configuration.</span></span>

