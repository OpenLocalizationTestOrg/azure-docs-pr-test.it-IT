---
title: 'Azure Active Directory B2C: Configurazione di LinkedIn | Documentazione Microsoft'
description: "Fornire la registrazione e l’accesso agli utenti con account su LinkedIn nelle applicazioni protette da Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: fa51a16b-9ce9-4e27-9eff-0869b4c4f0ef
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 1a6c4b19261aa34e668554ccad2b6340cddf9bf5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-linkedin-accounts"></a><span data-ttu-id="c2a75-103">Azure Active Directory B2C: fornire l'iscrizione e l'accesso agli utenti con account LinkedIn</span><span class="sxs-lookup"><span data-stu-id="c2a75-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with LinkedIn accounts</span></span>
## <a name="create-a-linkedin-application"></a><span data-ttu-id="c2a75-104">Creare un'applicazione su LinkedIn</span><span class="sxs-lookup"><span data-stu-id="c2a75-104">Create a LinkedIn application</span></span>
<span data-ttu-id="c2a75-105">Per utilizzare LinkedIn come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario creare un'applicazione LinkedIn e inserire i parametri corretti.</span><span class="sxs-lookup"><span data-stu-id="c2a75-105">To use LinkedIn as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a LinkedIn application and supply it with the right parameters.</span></span> <span data-ttu-id="c2a75-106">Per eseguire questa operazione è necessario disporre di un account di LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="c2a75-106">You need a LinkedIn account to do this.</span></span> <span data-ttu-id="c2a75-107">Se non si ha un account, è possibile crearlo nel sito [https://www.linkedin.com/](https://www.linkedin.com/).</span><span class="sxs-lookup"><span data-stu-id="c2a75-107">If you don’t have one, you can get it at [https://www.linkedin.com/](https://www.linkedin.com/).</span></span>

1. <span data-ttu-id="c2a75-108">Visitare il [sito Web di sviluppatori LinkedIn](https://www.developer.linkedin.com/) e accedere con le credenziali dell'account LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="c2a75-108">Go to the [LinkedIn Developers website](https://www.developer.linkedin.com/) and sign in with your LinkedIn account credentials.</span></span>
2. <span data-ttu-id="c2a75-109">Fare clic su **My Apps** (App personali) sulla barra dei menu superiore e quindi fare clic su **Create application** (Crea applicazione).</span><span class="sxs-lookup"><span data-stu-id="c2a75-109">Click **My Apps** in the top menu bar and then click **Create Application**.</span></span>
   
    ![LinkedIn - Nuova app](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. <span data-ttu-id="c2a75-111">Nel modulo **Create a New Application** (Creazione di una nuova applicazione), immettere le informazioni pertinenti (**nome azienda**, **nome**, **descrizione**, **URL del logo dell'applicazione**, **utilizzo dell'applicazione**, **URL del sito Web**, **e-mail aziendale** e **telefono ufficio**).</span><span class="sxs-lookup"><span data-stu-id="c2a75-111">In the **Create a New Application** form, fill in the relevant information (**Company Name**, **Name**, **Description**, **Application Logo URL**, **Application Use**, **Website URL**, **Business Email** and **Business Phone**).</span></span>
4. <span data-ttu-id="c2a75-112">Accettare il documento **LinkedIn API Terms of Use** (Condizioni d'uso dell'API LinkedIn) e fare clic su **Submit** (Invia).</span><span class="sxs-lookup"><span data-stu-id="c2a75-112">Agree to the **LinkedIn API Terms of Use** and click **Submit**.</span></span>
   
    ![LinkedIn - Registro app](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. <span data-ttu-id="c2a75-114">Copiare i valori **ID client** e **Segreto client**.</span><span class="sxs-lookup"><span data-stu-id="c2a75-114">Copy the values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="c2a75-115">che si trovano nella sezione **Authentication Keys** (Chiavi di autenticazione). Sono necessari entrambi per configurare LinkedIn come provider di identità nel tenant.</span><span class="sxs-lookup"><span data-stu-id="c2a75-115">(You can find them under **Authentication Keys**.) You will need both of them to configure LinkedIn as an identity provider in your tenant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c2a75-116">**Client Segreto** è un'importante credenziale di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="c2a75-116">**Client Secret** is an important security credential.</span></span>
   > 
   > 
6. <span data-ttu-id="c2a75-117">Immettere `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` nel campo **Authorized Redirect URLs** (URL di reindirizzamento autorizzati) in **OAuth 2.0**.</span><span class="sxs-lookup"><span data-stu-id="c2a75-117">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized Redirect URLs** field (under **OAuth 2.0**).</span></span> <span data-ttu-id="c2a75-118">Sostituire **{tenant}** con il nome del tenant, ad esempio contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="c2a75-118">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="c2a75-119">Fare clic su **Add** (Aggiungi) e quindi su **Update** (Aggiorna).</span><span class="sxs-lookup"><span data-stu-id="c2a75-119">Click **Add**, and then click **Update**.</span></span> <span data-ttu-id="c2a75-120">Il valore **{tenant}** distingue tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="c2a75-120">The **{tenant}** value is case-sensitive.</span></span>
   
    ![LinkedIn - Installazione app](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="c2a75-122">Configurare LinkedIn come provider di identità nel tenant</span><span class="sxs-lookup"><span data-stu-id="c2a75-122">Configure LinkedIn as an identity provider in your tenant</span></span>
1. <span data-ttu-id="c2a75-123">Seguire questa procedura per [passare al pannello delle funzionalità B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c2a75-123">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="c2a75-124">Nel pannello delle funzionalità di B2C, fare clic su **Provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="c2a75-124">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="c2a75-125">Fare clic su **+Aggiungi** nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="c2a75-125">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="c2a75-126">Fornire un **Nome** per la configurazione del provider di identità.</span><span class="sxs-lookup"><span data-stu-id="c2a75-126">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="c2a75-127">Ad esempio, immettere "LI".</span><span class="sxs-lookup"><span data-stu-id="c2a75-127">For example, enter "LI".</span></span>
5. <span data-ttu-id="c2a75-128">Fare clic su **Identity provider type** (Tipo di provider di identità), selezionare **LinkedIn** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c2a75-128">Click **Identity provider type**, select **LinkedIn**, and click **OK**.</span></span>
6. <span data-ttu-id="c2a75-129">Fare clic su **Impostare il provider di identità** e immettere l'ID client e il segreto client dell'applicazione LinkedIn creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c2a75-129">Click **Set up this identity provider** and enter the client ID and client secret of the LinkedIn application that you created earlier.</span></span>
7. <span data-ttu-id="c2a75-130">Fare clic su **OK** e quindi su **Create** (Crea) per salvare la configurazione di LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="c2a75-130">Click **OK** and then click **Create** to save your LinkedIn configuration.</span></span>

