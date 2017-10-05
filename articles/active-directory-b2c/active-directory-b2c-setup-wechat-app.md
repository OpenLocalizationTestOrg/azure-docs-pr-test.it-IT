---
title: 'Azure Active Directory B2C: configurazione di WeChat | Documentazione Microsoft'
description: Fornire l'iscrizione e l'accesso agli utenti con account WeChat nelle applicazioni protette da Azure Active Directory B2C.
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
ms.openlocfilehash: a54aec23d951610118246e9f70cdd27752ef39a6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-wechat-accounts"></a><span data-ttu-id="41ceb-103">Azure Active Directory B2C: fornire l'iscrizione e l'accesso agli utenti con account WeChat</span><span class="sxs-lookup"><span data-stu-id="41ceb-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with WeChat accounts</span></span>

> [!NOTE]
> <span data-ttu-id="41ceb-104">Questa funzionalità è in anteprima.</span><span class="sxs-lookup"><span data-stu-id="41ceb-104">This feature is in preview.</span></span>
> 

## <a name="create-a-wechat-application"></a><span data-ttu-id="41ceb-105">Creare un'applicazione WeChat</span><span class="sxs-lookup"><span data-stu-id="41ceb-105">Create a WeChat application</span></span>

<span data-ttu-id="41ceb-106">Per usare WeChat come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario creare un'applicazione WeChat e inserire i parametri corretti.</span><span class="sxs-lookup"><span data-stu-id="41ceb-106">To use WeChat as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a WeChat application and supply it with the right parameters.</span></span> <span data-ttu-id="41ceb-107">Per eseguire questa operazione è necessario un account WeChat.</span><span class="sxs-lookup"><span data-stu-id="41ceb-107">You need a WeChat account to do this.</span></span> <span data-ttu-id="41ceb-108">Se non si dispone di un account, è possibile ottenerne uno eseguendo l'iscrizione tramite una delle App per dispositivi mobili o usano il numero QQ.</span><span class="sxs-lookup"><span data-stu-id="41ceb-108">If you don’t have one, you can get one by signing up through one of their mobile apps or by using your QQ number.</span></span> <span data-ttu-id="41ceb-109">Ottenere quindi l'account registrato con il programma per sviluppatori WeChat.</span><span class="sxs-lookup"><span data-stu-id="41ceb-109">After that, get your account registered with the WeChat developer program.</span></span> <span data-ttu-id="41ceb-110">Altre informazioni sono disponibili [qui](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span><span class="sxs-lookup"><span data-stu-id="41ceb-110">You can find more information [here](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span></span>

### <a name="register-a-wechat-application"></a><span data-ttu-id="41ceb-111">Registrare un'applicazione WeChat</span><span class="sxs-lookup"><span data-stu-id="41ceb-111">Register a WeChat application</span></span>

1. <span data-ttu-id="41ceb-112">Passare a [https://open.weixin.qq.com/](https://open.weixin.qq.com/) ed eseguire l'accesso.</span><span class="sxs-lookup"><span data-stu-id="41ceb-112">Go to [https://open.weixin.qq.com/](https://open.weixin.qq.com/) and log in.</span></span>
2. <span data-ttu-id="41ceb-113">Fare clic su **管理中心** (Centro di gestione).</span><span class="sxs-lookup"><span data-stu-id="41ceb-113">Click on **管理中心** (management center).</span></span>
3. <span data-ttu-id="41ceb-114">Seguire i passaggi necessari per registrare una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="41ceb-114">Follow the necessary steps to register a new application.</span></span>
4. <span data-ttu-id="41ceb-115">Per **授权回调域** (URL di callback) immettere `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="41ceb-115">For **授权回调域** (callback URL), enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="41ceb-116">Ad esempio, se `tenant_name` è contoso.onmicrosoft.com, impostare l'URL a `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="41ceb-116">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
5. <span data-ttu-id="41ceb-117">Trovare e copiare l'**ID APP** e la **CHIAVE APP**,</span><span class="sxs-lookup"><span data-stu-id="41ceb-117">Find and copy the **APP ID** and **APP KEY**.</span></span> <span data-ttu-id="41ceb-118">che verranno usati in seguito.</span><span class="sxs-lookup"><span data-stu-id="41ceb-118">You will need these later.</span></span>

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="41ceb-119">Configurare WeChat come provider di identità nel tenant,</span><span class="sxs-lookup"><span data-stu-id="41ceb-119">Configure WeChat as an identity provider in your tenant</span></span>
1. <span data-ttu-id="41ceb-120">Seguire questa procedura per [passare al pannello delle funzionalità B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="41ceb-120">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="41ceb-121">Nel pannello delle funzionalità di B2C, fare clic su **Provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="41ceb-121">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="41ceb-122">Fare clic su **+Aggiungi** nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="41ceb-122">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="41ceb-123">Fornire un **Nome** per la configurazione del provider di identità.</span><span class="sxs-lookup"><span data-stu-id="41ceb-123">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="41ceb-124">ad esempio, immettere "WeChat".</span><span class="sxs-lookup"><span data-stu-id="41ceb-124">For example, enter "WeChat".</span></span>
5. <span data-ttu-id="41ceb-125">Fare clic su **Tipo di provider di identità**, selezionare **WeChat** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="41ceb-125">Click **Identity provider type**, select **WeChat**, and click **OK**.</span></span>
6. <span data-ttu-id="41ceb-126">Fare clic su **Configura questo provider di identità**</span><span class="sxs-lookup"><span data-stu-id="41ceb-126">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="41ceb-127">Immettere la **chiave app** copiata in precedenza come **ID client**.</span><span class="sxs-lookup"><span data-stu-id="41ceb-127">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="41ceb-128">Immettere il **segreto app** copiato in precedenza come **segreto client**.</span><span class="sxs-lookup"><span data-stu-id="41ceb-128">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="41ceb-129">Fare clic su **OK** e su **Crea** per salvare la configurazione di WeChat.</span><span class="sxs-lookup"><span data-stu-id="41ceb-129">Click **OK** and then click **Create** to save your WeChat configuration.</span></span>

