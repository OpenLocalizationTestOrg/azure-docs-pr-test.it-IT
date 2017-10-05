---
title: 'Azure Active Directory B2C: configurazione di Google+ | Documentazione Microsoft'
description: "Fornire la registrazione e l’accesso agli utenti con account Google+ nelle applicazioni protette da Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 4dcca66f-29e4-4b4d-8840-50baad736bd7
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6ab73e5c79742ab548733f5712dee1e28461db9f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-google-accounts"></a><span data-ttu-id="c472e-103">Azure Active Directory B2C: fornire l'iscrizione e l'accesso agli utenti con account Google+</span><span class="sxs-lookup"><span data-stu-id="c472e-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Google+ accounts</span></span>
## <a name="create-a-google-application"></a><span data-ttu-id="c472e-104">Creazione di un'applicazione Google+</span><span class="sxs-lookup"><span data-stu-id="c472e-104">Create a Google+ application</span></span>
<span data-ttu-id="c472e-105">Per usare Google+ come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario creare un'applicazione Google+ e inserire i parametri corretti.</span><span class="sxs-lookup"><span data-stu-id="c472e-105">To use Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Google+ application and supply it with the right parameters.</span></span> <span data-ttu-id="c472e-106">Per eseguire questa operazione è necessario disporre di un account Google+.</span><span class="sxs-lookup"><span data-stu-id="c472e-106">You need a Google+ account to do this.</span></span> <span data-ttu-id="c472e-107">Se non è disponibile un account, è possibile crearlo nel sito [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span><span class="sxs-lookup"><span data-stu-id="c472e-107">If you don’t have one, you can get it at [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span></span>

1. <span data-ttu-id="c472e-108">Visitare [Google Developers Console](https://console.developers.google.com/) e accedere con le credenziali dell'account Google+.</span><span class="sxs-lookup"><span data-stu-id="c472e-108">Go to the [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2. <span data-ttu-id="c472e-109">Fare clic su **Crea progetto**, immettere un nome in **Nome progetto**e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c472e-109">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>
   
    ![Google+ - Introduzione](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google+ - Nuovo progetto](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. <span data-ttu-id="c472e-112">Fare clic su **Gestione API** e su **Credenziali** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="c472e-112">Click **API Manager** and then click **Credentials** in the left navigation.</span></span>
4. <span data-ttu-id="c472e-113">Fare clic sulla scheda **Schermata consenso OAuth** nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="c472e-113">Click the **OAuth consent screen** tab at the top.</span></span>
   
    ![Google+ - Credenziali](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. <span data-ttu-id="c472e-115">Selezionare o specificare un **Indirizzo e-mail** valido, fornire un **Nome prodotto** e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="c472e-115">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>
   
    ![Google+ - Schermata consenso OAuth](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. <span data-ttu-id="c472e-117">Fare clic su **Nuove credenziali** e scegliere **ID client OAuth**.</span><span class="sxs-lookup"><span data-stu-id="c472e-117">Click **New credentials** and then choose **OAuth client ID**.</span></span>
   
    ![Google+ - Schermata consenso OAuth](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. <span data-ttu-id="c472e-119">In **Tipo di applicazione** selezionare **Applicazione Web**.</span><span class="sxs-lookup"><span data-stu-id="c472e-119">Under **Application type**, select **Web application**.</span></span>
   
    ![Google+ - Schermata consenso OAuth](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. <span data-ttu-id="c472e-121">Fornire un **Nome** per l'applicazione, immettere `https://login.microsoftonline.com` nel campo **Origini JavaScript Autorizzate** e `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` nel campo **URI di reindirizzamento autorizzati**.</span><span class="sxs-lookup"><span data-stu-id="c472e-121">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in the **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized redirect URIs** field.</span></span> <span data-ttu-id="c472e-122">Sostituire **{tenant}** con il nome del tenant, ad esempio contosob2c.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="c472e-122">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="c472e-123">Il valore **{tenant}** distingue tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="c472e-123">The **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="c472e-124">Fare clic su **Create**(Crea).</span><span class="sxs-lookup"><span data-stu-id="c472e-124">Click **Create**.</span></span>
   
    ![Google+ - Creare ID client](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. <span data-ttu-id="c472e-126">Copiare i valori **ID client** e **Segreto client**.</span><span class="sxs-lookup"><span data-stu-id="c472e-126">Copy the values of **Client ID** and **Client secret**.</span></span> <span data-ttu-id="c472e-127">Sono necessari entrambi per configurare Google+ come provider di identità nel tenant.</span><span class="sxs-lookup"><span data-stu-id="c472e-127">You will need both of them to configure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="c472e-128">**Segreto client** è una credenziale di sicurezza importante.</span><span class="sxs-lookup"><span data-stu-id="c472e-128">**Client secret** is an important security credential.</span></span>
   
    ![Google+ - Segreto client](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="c472e-130">Configurare Google+ come provider di identità nel tenant</span><span class="sxs-lookup"><span data-stu-id="c472e-130">Configure Google+ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="c472e-131">Seguire questa procedura per [passare al pannello delle funzionalità B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c472e-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="c472e-132">Nel pannello delle funzionalità di B2C, fare clic su **Provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="c472e-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="c472e-133">Fare clic su **+Aggiungi** nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="c472e-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="c472e-134">Fornire un **Nome** per la configurazione del provider di identità.</span><span class="sxs-lookup"><span data-stu-id="c472e-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="c472e-135">Ad esempio, immettere "G+".</span><span class="sxs-lookup"><span data-stu-id="c472e-135">For example, enter "G+".</span></span>
5. <span data-ttu-id="c472e-136">Fare clic su **Tipo di provider di identità**, selezionare **Google** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c472e-136">Click **Identity provider type**, select **Google**, and click **OK**.</span></span>
6. <span data-ttu-id="c472e-137">Fare clic su **Impostare il provider di identità** e immettere l'ID Client e il segreto client dell'applicazione Google+ creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c472e-137">Click **Set up this identity provider** and enter the client ID and client secret of the Google+ application that you created earlier.</span></span>
7. <span data-ttu-id="c472e-138">Fare clic su **OK** e su **Crea** per salvare la configurazione di Google+.</span><span class="sxs-lookup"><span data-stu-id="c472e-138">Click **OK** and then click **Create** to save your Google+ configuration.</span></span>

