---
title: 'Azure Active Directory B2C: Configurazione dell''account Microsoft | Documentazione Microsoft'
description: Fornire tooconsumers iscrizione e Accedi con l'account di Microsoft nelle applicazioni che sono protetti da Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 06407322-142c-4cb3-9106-a8d752c4c853
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: bec4777f003c459030f68c35b24f0e4bcddf84ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-microsoft-accounts"></a><span data-ttu-id="b00db-103">Azure Active B2C di Directory: Fornire tooconsumers iscrizione e Accedi con account Microsoft</span><span class="sxs-lookup"><span data-stu-id="b00db-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Microsoft accounts</span></span>
## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="b00db-104">Creare un'applicazione di account Microsoft</span><span class="sxs-lookup"><span data-stu-id="b00db-104">Create a Microsoft account application</span></span>
<span data-ttu-id="b00db-105">toouse Microsoft account come un provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un'applicazione di account Microsoft e fornirlo con i parametri corretti hello.</span><span class="sxs-lookup"><span data-stu-id="b00db-105">toouse Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Microsoft account application and supply it with hello right parameters.</span></span> <span data-ttu-id="b00db-106">Necessaria una toodo account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b00db-106">You need a Microsoft account toodo this.</span></span> <span data-ttu-id="b00db-107">Se non si ha un account, è possibile crearlo nel sito [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="b00db-107">If you don’t have one, you can get it at [https://www.live.com/](https://www.live.com/).</span></span>

1. <span data-ttu-id="b00db-108">Passare toohello [portale di registrazione dell'applicazione Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) e accedere con le credenziali dell'account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b00db-108">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2. <span data-ttu-id="b00db-109">Fare clic su **Aggiungi un'app**.</span><span class="sxs-lookup"><span data-stu-id="b00db-109">Click **Add an app**.</span></span>
   
    ![Account Microsoft - Aggiungere una nuova app](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. <span data-ttu-id="b00db-111">Specificare un **Nome** per l'applicazione e fare clic su **Crea applicazione**.</span><span class="sxs-lookup"><span data-stu-id="b00db-111">Provide a **Name** for your application and click **Create application**.</span></span>
   
    ![Account Microsoft - Nome applicazione](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. <span data-ttu-id="b00db-113">Copiare il valore di hello di **Id applicazione**. Sarà necessario tooconfigure account Microsoft come provider di identità nel tenant.</span><span class="sxs-lookup"><span data-stu-id="b00db-113">Copy hello value of **Application Id**. You will need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span>
   
    ![Account Microsoft - ID applicazione](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. <span data-ttu-id="b00db-115">Fare clic su **Aggiungi piattaforma** e scegliere **Web**.</span><span class="sxs-lookup"><span data-stu-id="b00db-115">Click on **Add platform** and choose **Web**.</span></span>
   
    ![Account Microsoft - Aggiungi piattaforma](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Account Microsoft - Web](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. <span data-ttu-id="b00db-118">Immettere `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** campo.</span><span class="sxs-lookup"><span data-stu-id="b00db-118">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** field.</span></span> <span data-ttu-id="b00db-119">Sostituire **{tenant}** con il nome del tenant, ad esempio contosob2c.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="b00db-119">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
   
    ![Account Microsoft - URL di reindirizzamento](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. <span data-ttu-id="b00db-121">Fare clic su **generare una nuova Password** in hello **applicazione segreti** sezione.</span><span class="sxs-lookup"><span data-stu-id="b00db-121">Click on **Generate New Password** under hello **Application Secrets** section.</span></span> <span data-ttu-id="b00db-122">Copia hello nuova password visualizzata sullo schermo.</span><span class="sxs-lookup"><span data-stu-id="b00db-122">Copy hello new password displayed on screen.</span></span> <span data-ttu-id="b00db-123">Sarà necessario tooconfigure account Microsoft come provider di identità nel tenant.</span><span class="sxs-lookup"><span data-stu-id="b00db-123">You will need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="b00db-124">La password è una credenziale di sicurezza importante.</span><span class="sxs-lookup"><span data-stu-id="b00db-124">This password is an important security credential.</span></span>
   
    ![Account Microsoft - Genera nuova password](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Account Microsoft - Nuova password](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. <span data-ttu-id="b00db-127">Casella di controllo hello indicante **il supporto di Live SDK** in hello **opzioni avanzate** sezione.</span><span class="sxs-lookup"><span data-stu-id="b00db-127">Check hello box that says **Live SDK support** under hello **Advanced Options** section.</span></span> <span data-ttu-id="b00db-128">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="b00db-128">Click **Save**.</span></span>
   
    ![Account Microsoft - Supporto Live SDK](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="b00db-130">Configurare un account Microsoft come provider di identità nel tenant</span><span class="sxs-lookup"><span data-stu-id="b00db-130">Configure Microsoft account as an identity provider in your tenant</span></span>
1. <span data-ttu-id="b00db-131">Seguire questi passaggi troppo[passare pannello funzionalità toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) su hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b00db-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="b00db-132">Nel Pannello di hello B2C funzionalità, fare clic su **provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="b00db-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="b00db-133">Fare clic su **+ Aggiungi** nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="b00db-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="b00db-134">Fornire un nome **nome** per la configurazione del provider di identità hello.</span><span class="sxs-lookup"><span data-stu-id="b00db-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="b00db-135">Ad esempio, immettere "MSA".</span><span class="sxs-lookup"><span data-stu-id="b00db-135">For example, enter "MSA".</span></span>
5. <span data-ttu-id="b00db-136">Fare clic su **Tipo di provider di identità**, selezionare **Account Microsoft** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b00db-136">Click **Identity provider type**, select **Microsoft account**, and click **OK**.</span></span>
6. <span data-ttu-id="b00db-137">Fare clic su **impostare il provider di identità** e immettere l'Id applicazione hello e la password di hello applicazione Microsoft account creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b00db-137">Click **Set up this identity provider** and enter hello Application Id and password of hello Microsoft account application that you created earlier.</span></span>
7. <span data-ttu-id="b00db-138">Fare clic su **OK** e quindi fare clic su **crea** toosave configurazione dell'account di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b00db-138">Click **OK** and then click **Create** toosave your Microsoft account configuration.</span></span>

