---
title: 'Azure Active Directory B2C: configurazione di Google+ | Documentazione Microsoft'
description: Fornire tooconsumers iscrizione e Accedi con Google + account nelle applicazioni che sono protetti da Azure Active Directory B2C.
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
ms.openlocfilehash: 6ef66eb17777acd95b5f4745ed6097c77e37663b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-google-accounts"></a><span data-ttu-id="d491e-103">Azure Active B2C di Directory: Fornire tooconsumers iscrizione e Accedi con account di Google +</span><span class="sxs-lookup"><span data-stu-id="d491e-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Google+ accounts</span></span>
## <a name="create-a-google-application"></a><span data-ttu-id="d491e-104">Creazione di un'applicazione Google+</span><span class="sxs-lookup"><span data-stu-id="d491e-104">Create a Google+ application</span></span>
<span data-ttu-id="d491e-105">toouse Google + come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un'applicazione Google + e fornirlo con i parametri corretti hello.</span><span class="sxs-lookup"><span data-stu-id="d491e-105">toouse Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Google+ application and supply it with hello right parameters.</span></span> <span data-ttu-id="d491e-106">È necessario questo toodo un account Google +.</span><span class="sxs-lookup"><span data-stu-id="d491e-106">You need a Google+ account toodo this.</span></span> <span data-ttu-id="d491e-107">Se non è disponibile un account, è possibile crearlo nel sito [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span><span class="sxs-lookup"><span data-stu-id="d491e-107">If you don’t have one, you can get it at [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span></span>

1. <span data-ttu-id="d491e-108">Passare toohello [Google Developers Console](https://console.developers.google.com/) e accedere con le credenziali dell'account Google +.</span><span class="sxs-lookup"><span data-stu-id="d491e-108">Go toohello [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2. <span data-ttu-id="d491e-109">Fare clic su **Crea progetto**, immettere un nome in **Nome progetto**e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d491e-109">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>
   
    ![Google+ - Introduzione](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google+ - Nuovo progetto](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. <span data-ttu-id="d491e-112">Fare clic su **API Manager** e quindi fare clic su **credenziali** nel riquadro di spostamento sinistro hello.</span><span class="sxs-lookup"><span data-stu-id="d491e-112">Click **API Manager** and then click **Credentials** in hello left navigation.</span></span>
4. <span data-ttu-id="d491e-113">Fare clic su hello **schermata consenso OAuth** scheda nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="d491e-113">Click hello **OAuth consent screen** tab at hello top.</span></span>
   
    ![Google+ - Credenziali](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. <span data-ttu-id="d491e-115">Selezionare o specificare un **Indirizzo e-mail** valido, fornire un **Nome prodotto** e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d491e-115">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>
   
    ![Google+ - Schermata consenso OAuth](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. <span data-ttu-id="d491e-117">Fare clic su **Nuove credenziali** e scegliere **ID client OAuth**.</span><span class="sxs-lookup"><span data-stu-id="d491e-117">Click **New credentials** and then choose **OAuth client ID**.</span></span>
   
    ![Google+ - Schermata consenso OAuth](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. <span data-ttu-id="d491e-119">In **Tipo di applicazione** selezionare **Applicazione Web**.</span><span class="sxs-lookup"><span data-stu-id="d491e-119">Under **Application type**, select **Web application**.</span></span>
   
    ![Google+ - Schermata consenso OAuth](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. <span data-ttu-id="d491e-121">Fornire un **nome** per l'applicazione, immettere `https://login.microsoftonline.com` in hello **autorizzato JavaScript origins** , campo e `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized redirect URI**campo.</span><span class="sxs-lookup"><span data-stu-id="d491e-121">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in hello **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized redirect URIs** field.</span></span> <span data-ttu-id="d491e-122">Sostituire **{tenant}** con il nome del tenant, ad esempio contosob2c.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="d491e-122">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="d491e-123">Hello **{tenant}** valore è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="d491e-123">hello **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="d491e-124">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d491e-124">Click **Create**.</span></span>
   
    ![Google+ - Creare ID client](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. <span data-ttu-id="d491e-126">Copiare i valori hello di **ID Client** e **segreto Client**.</span><span class="sxs-lookup"><span data-stu-id="d491e-126">Copy hello values of **Client ID** and **Client secret**.</span></span> <span data-ttu-id="d491e-127">Sarà necessario entrambi tooconfigure Google + come provider di identità nel tenant.</span><span class="sxs-lookup"><span data-stu-id="d491e-127">You will need both of them tooconfigure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="d491e-128">**Segreto client** è una credenziale di sicurezza importante.</span><span class="sxs-lookup"><span data-stu-id="d491e-128">**Client secret** is an important security credential.</span></span>
   
    ![Google+ - Segreto client](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="d491e-130">Configurare Google+ come provider di identità nel tenant</span><span class="sxs-lookup"><span data-stu-id="d491e-130">Configure Google+ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="d491e-131">Seguire questi passaggi troppo[passare pannello funzionalità toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) su hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d491e-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="d491e-132">Nel Pannello di hello B2C funzionalità, fare clic su **provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="d491e-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="d491e-133">Fare clic su **+ Aggiungi** nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="d491e-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="d491e-134">Fornire un nome **nome** per la configurazione del provider di identità hello.</span><span class="sxs-lookup"><span data-stu-id="d491e-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="d491e-135">Ad esempio, immettere "G+".</span><span class="sxs-lookup"><span data-stu-id="d491e-135">For example, enter "G+".</span></span>
5. <span data-ttu-id="d491e-136">Fare clic su **Tipo di provider di identità**, selezionare **Google** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d491e-136">Click **Identity provider type**, select **Google**, and click **OK**.</span></span>
6. <span data-ttu-id="d491e-137">Fare clic su **impostare il provider di identità** e immettere privata hello client ID e il client di hello applicazione Google + creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d491e-137">Click **Set up this identity provider** and enter hello client ID and client secret of hello Google+ application that you created earlier.</span></span>
7. <span data-ttu-id="d491e-138">Fare clic su **OK** e quindi fare clic su **crea** toosave configurazione Google +.</span><span class="sxs-lookup"><span data-stu-id="d491e-138">Click **OK** and then click **Create** toosave your Google+ configuration.</span></span>

