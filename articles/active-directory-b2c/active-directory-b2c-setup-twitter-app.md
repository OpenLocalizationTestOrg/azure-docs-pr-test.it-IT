---
title: 'Azure Active Directory B2C: configurazione di Twitter | Documentazione Microsoft'
description: Fornire l'iscrizione e l'accesso agli utenti con account Twitter nelle applicazioni protette da Azure Active Directory B2C.
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
ms.openlocfilehash: 82a001dd53cdddcf3b360090f3250af593c96fbb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-twitter-accounts"></a><span data-ttu-id="096f9-103">Azure Active Directory B2C: fornire l'iscrizione e l'accesso agli utenti con account Twitter</span><span class="sxs-lookup"><span data-stu-id="096f9-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Twitter accounts</span></span>

> [!NOTE]
> <span data-ttu-id="096f9-104">Questa funzionalità è in anteprima.</span><span class="sxs-lookup"><span data-stu-id="096f9-104">This feature is in preview.</span></span>
> 

## <a name="create-a-twitter-application"></a><span data-ttu-id="096f9-105">Creare un'applicazione Twitter</span><span class="sxs-lookup"><span data-stu-id="096f9-105">Create a Twitter application</span></span>
<span data-ttu-id="096f9-106">Per usare Twitter come provider di identità in Azure Active Directory (Azure AD) B2C, si deve creare un'applicazione Twitter e inserire i parametri corretti.</span><span class="sxs-lookup"><span data-stu-id="096f9-106">To use Twitter as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Twitter application and supply it with the right parameters.</span></span> <span data-ttu-id="096f9-107">Per eseguire questa operazione è necessario un account sviluppatore di Twitter.</span><span class="sxs-lookup"><span data-stu-id="096f9-107">You need a Twitter developer account to do this.</span></span> <span data-ttu-id="096f9-108">Se non si ha un account, è possibile crearlo sul sito [https://dev.twitter.com/](https://dev.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="096f9-108">If you don’t have one, you can get it at [https://dev.twitter.com/](https://dev.twitter.com/).</span></span>

1. <span data-ttu-id="096f9-109">Passare al [sito Web per sviluppatori di Twitter](https://dev.twitter.com/) e accedere con le proprie credenziali.</span><span class="sxs-lookup"><span data-stu-id="096f9-109">Go to the [Twitter developer's website](https://dev.twitter.com/) and sign in with your credentials.</span></span>
2. <span data-ttu-id="096f9-110">Fare clic su **My apps** (App personali) in **Tools & Support** (Strumenti e supporto) e quindi fare clic su **Create New App** (Crea nuova app).</span><span class="sxs-lookup"><span data-stu-id="096f9-110">Click **My apps** under **Tools & Support** and then click **Create New App**.</span></span> 
3. <span data-ttu-id="096f9-111">Nel modulo immettere i valori desiderati per **Nome**, **Descrizione** e **Sito Web**.</span><span class="sxs-lookup"><span data-stu-id="096f9-111">In the form, provide a value for the **Name**, **Description**, and **Website**.</span></span>
4. <span data-ttu-id="096f9-112">Per **URL callback** immettere `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="096f9-112">For the **Callback URL**, enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span></span> <span data-ttu-id="096f9-113">Accertarsi di sostituire **{tenant}** con il nome del tenant, ad esempio contosob2c.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="096f9-113">Make sure to replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
5. <span data-ttu-id="096f9-114">Selezionare la casella per accettare il **contratto per gli sviluppatori** e fare clic su **Create your Twitter application** (Crea applicazione Twitter).</span><span class="sxs-lookup"><span data-stu-id="096f9-114">Check the box to agree to the **Developer Agreement** and click **Create your Twitter application**.</span></span>
6. <span data-ttu-id="096f9-115">Quando l'app viene creata, fare clic su **Keys and Access Tokens** (Chiavi e token di accesso).</span><span class="sxs-lookup"><span data-stu-id="096f9-115">Once the app is created, click **Keys and Access Tokens**.</span></span>
7. <span data-ttu-id="096f9-116">Copiare il valore di **Chiave utente** e **Segreto consumer**.</span><span class="sxs-lookup"><span data-stu-id="096f9-116">Copy the value of **Consumer Key** and **Consumer Secret**.</span></span> <span data-ttu-id="096f9-117">Sono necessari entrambi per configurare Twitter come provider di identità nel tenant.</span><span class="sxs-lookup"><span data-stu-id="096f9-117">You will need both of them to configure Twitter as an identity provider in your tenant.</span></span>

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="096f9-118">Configurare Twitter come provider di identità nel tenant,</span><span class="sxs-lookup"><span data-stu-id="096f9-118">Configure Twitter as an identity provider in your tenant</span></span>
1. <span data-ttu-id="096f9-119">Seguire questa procedura per [passare al pannello delle funzionalità B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="096f9-119">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="096f9-120">Nel pannello delle funzionalità di B2C, fare clic su **Provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="096f9-120">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="096f9-121">Fare clic su **+Aggiungi** nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="096f9-121">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="096f9-122">Fornire un **Nome** per la configurazione del provider di identità.</span><span class="sxs-lookup"><span data-stu-id="096f9-122">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="096f9-123">ad esempio, immettere "Twitter".</span><span class="sxs-lookup"><span data-stu-id="096f9-123">For example, enter "Twitter".</span></span>
5. <span data-ttu-id="096f9-124">Fare clic su **Tipo di provider di identità**, selezionare **Twitter** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="096f9-124">Click **Identity provider type**, select **Twitter**, and click **OK**.</span></span>
6. <span data-ttu-id="096f9-125">Fare clic su **Configura questo provider di identità** e immettere la **Chiave utente** di Twitter per **ID client** e il **Segreto consumer** di Twitter per **Segreto client**.</span><span class="sxs-lookup"><span data-stu-id="096f9-125">Click **Set up this identity provider** and enter the Twitter **Consumer Key** for the **Client id** and the Twitter **Consumer Secret** for the **Client secret**.</span></span>
7. <span data-ttu-id="096f9-126">Fare clic su **OK** e su **Crea** per salvare la configurazione di Twitter.</span><span class="sxs-lookup"><span data-stu-id="096f9-126">Click **OK**, and then click **Create** to save your Twitter configuration.</span></span>

