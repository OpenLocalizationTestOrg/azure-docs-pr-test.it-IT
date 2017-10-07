---
title: 'Azure Active Directory B2C: configurazione di Twitter | Documentazione Microsoft'
description: Fornire tooconsumers iscrizione e Accedi con Twitter account nelle applicazioni che sono protetti da Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 579a6841-9329-45b8-a351-da4315a6634e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/06/2017
ms.author: parakhj
ms.openlocfilehash: 275c5c73fd5e8e5075e77fee942cbc1b5e1586cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-twitter-accounts"></a><span data-ttu-id="0dec3-103">Azure Active B2C di Directory: Fornire tooconsumers iscrizione e Accedi con account Twitter</span><span class="sxs-lookup"><span data-stu-id="0dec3-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Twitter accounts</span></span>

> [!NOTE]
> <span data-ttu-id="0dec3-104">Questa funzionalità è in anteprima.</span><span class="sxs-lookup"><span data-stu-id="0dec3-104">This feature is in preview.</span></span>
> 

## <a name="create-a-twitter-application"></a><span data-ttu-id="0dec3-105">Creare un'applicazione Twitter</span><span class="sxs-lookup"><span data-stu-id="0dec3-105">Create a Twitter application</span></span>
<span data-ttu-id="0dec3-106">toouse Twitter come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un'applicazione di Twitter e fornirlo con i parametri corretti hello.</span><span class="sxs-lookup"><span data-stu-id="0dec3-106">toouse Twitter as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Twitter application and supply it with hello right parameters.</span></span> <span data-ttu-id="0dec3-107">Necessaria una toodo account sviluppatore di Twitter.</span><span class="sxs-lookup"><span data-stu-id="0dec3-107">You need a Twitter developer account toodo this.</span></span> <span data-ttu-id="0dec3-108">Se non si ha un account, è possibile crearlo sul sito [https://dev.twitter.com/](https://dev.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="0dec3-108">If you don’t have one, you can get it at [https://dev.twitter.com/](https://dev.twitter.com/).</span></span>

1. <span data-ttu-id="0dec3-109">Passare toohello [sito Web per gli sviluppatori di Twitter](https://dev.twitter.com/) e accedere con le credenziali.</span><span class="sxs-lookup"><span data-stu-id="0dec3-109">Go toohello [Twitter developer's website](https://dev.twitter.com/) and sign in with your credentials.</span></span>
2. <span data-ttu-id="0dec3-110">Fare clic su **My apps** (App personali) in **Tools & Support** (Strumenti e supporto) e quindi fare clic su **Create New App** (Crea nuova app).</span><span class="sxs-lookup"><span data-stu-id="0dec3-110">Click **My apps** under **Tools & Support** and then click **Create New App**.</span></span> 
3. <span data-ttu-id="0dec3-111">Nel modulo hello, fornire un valore per hello **nome**, **descrizione**, e **sito Web**.</span><span class="sxs-lookup"><span data-stu-id="0dec3-111">In hello form, provide a value for hello **Name**, **Description**, and **Website**.</span></span>
4. <span data-ttu-id="0dec3-112">Per hello **URL Callback**, immettere `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="0dec3-112">For hello **Callback URL**, enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span></span> <span data-ttu-id="0dec3-113">Verificare che tooreplace **{tenant}** con il nome del tenant (ad esempio, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="0dec3-113">Make sure tooreplace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
5. <span data-ttu-id="0dec3-114">Controllare hello casella tooagree toohello **contratto per gli sviluppatori** e fare clic su **creare un'applicazione Twitter**.</span><span class="sxs-lookup"><span data-stu-id="0dec3-114">Check hello box tooagree toohello **Developer Agreement** and click **Create your Twitter application**.</span></span>
6. <span data-ttu-id="0dec3-115">Una volta creato l'applicazione hello, fare clic su **chiavi e i token di accesso**.</span><span class="sxs-lookup"><span data-stu-id="0dec3-115">Once hello app is created, click **Keys and Access Tokens**.</span></span>
7. <span data-ttu-id="0dec3-116">Copiare il valore di hello di **chiave Consumer** e **segreto del cliente**.</span><span class="sxs-lookup"><span data-stu-id="0dec3-116">Copy hello value of **Consumer Key** and **Consumer Secret**.</span></span> <span data-ttu-id="0dec3-117">Sarà necessario entrambi tooconfigure Twitter come provider di identità nel tenant.</span><span class="sxs-lookup"><span data-stu-id="0dec3-117">You will need both of them tooconfigure Twitter as an identity provider in your tenant.</span></span>

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="0dec3-118">Configurare Twitter come provider di identità nel tenant,</span><span class="sxs-lookup"><span data-stu-id="0dec3-118">Configure Twitter as an identity provider in your tenant</span></span>
1. <span data-ttu-id="0dec3-119">Seguire questi passaggi troppo[passare pannello funzionalità toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) su hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0dec3-119">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="0dec3-120">Nel Pannello di hello B2C funzionalità, fare clic su **provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="0dec3-120">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="0dec3-121">Fare clic su **+ Aggiungi** nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="0dec3-121">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="0dec3-122">Fornire un nome **nome** per la configurazione del provider di identità hello.</span><span class="sxs-lookup"><span data-stu-id="0dec3-122">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="0dec3-123">ad esempio, immettere "Twitter".</span><span class="sxs-lookup"><span data-stu-id="0dec3-123">For example, enter "Twitter".</span></span>
5. <span data-ttu-id="0dec3-124">Fare clic su **Tipo di provider di identità**, selezionare **Twitter** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0dec3-124">Click **Identity provider type**, select **Twitter**, and click **OK**.</span></span>
6. <span data-ttu-id="0dec3-125">Fare clic su **impostare il provider di identità** e immettere hello Twitter **chiave Consumer** per hello **id Client** e hello Twitter **segreto del cliente**per hello **segreto Client**.</span><span class="sxs-lookup"><span data-stu-id="0dec3-125">Click **Set up this identity provider** and enter hello Twitter **Consumer Key** for hello **Client id** and hello Twitter **Consumer Secret** for hello **Client secret**.</span></span>
7. <span data-ttu-id="0dec3-126">Fare clic su **OK**, quindi fare clic su **crea** toosave la configurazione di Twitter.</span><span class="sxs-lookup"><span data-stu-id="0dec3-126">Click **OK**, and then click **Create** toosave your Twitter configuration.</span></span>

