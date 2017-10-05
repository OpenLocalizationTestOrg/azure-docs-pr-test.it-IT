---
title: 'Azure Active Directory B2C: Configurazione dell''account Microsoft | Documentazione Microsoft'
description: Fornire la registrazione e l'accesso agli utenti con account Microsoft nelle applicazioni protette da Azure Active Directory B2C
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
ms.openlocfilehash: 59879dc0b3fc1d7af3e2a1f67f1701f451de9126
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-microsoft-accounts"></a><span data-ttu-id="6dde7-103">Azure Active Directory B2C: Fornire la registrazione e l'accesso agli utenti con account Microsoft</span><span class="sxs-lookup"><span data-stu-id="6dde7-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Microsoft accounts</span></span>
## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="6dde7-104">Creare un'applicazione di account Microsoft</span><span class="sxs-lookup"><span data-stu-id="6dde7-104">Create a Microsoft account application</span></span>
<span data-ttu-id="6dde7-105">Per usare un account Microsoft come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario creare un'applicazione di account Microsoft e inserire i parametri corretti.</span><span class="sxs-lookup"><span data-stu-id="6dde7-105">To use Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Microsoft account application and supply it with the right parameters.</span></span> <span data-ttu-id="6dde7-106">Per eseguire questa operazione è necessario disporre di un account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6dde7-106">You need a Microsoft account to do this.</span></span> <span data-ttu-id="6dde7-107">Se non si ha un account, è possibile crearlo nel sito [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="6dde7-107">If you don’t have one, you can get it at [https://www.live.com/](https://www.live.com/).</span></span>

1. <span data-ttu-id="6dde7-108">Entrare nel [portale di registrazione delle applicazioni Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) e accedere con le credenziali del proprio account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6dde7-108">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2. <span data-ttu-id="6dde7-109">Fare clic su **Aggiungi un'app**.</span><span class="sxs-lookup"><span data-stu-id="6dde7-109">Click **Add an app**.</span></span>
   
    ![Account Microsoft - Aggiungere una nuova app](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. <span data-ttu-id="6dde7-111">Specificare un **Nome** per l'applicazione e fare clic su **Crea applicazione**.</span><span class="sxs-lookup"><span data-stu-id="6dde7-111">Provide a **Name** for your application and click **Create application**.</span></span>
   
    ![Account Microsoft - Nome applicazione](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. <span data-ttu-id="6dde7-113">Copiare il valore di **ID applicazione**. Sarà necessario per configurare un account Microsoft come provider di identità nel tenant.</span><span class="sxs-lookup"><span data-stu-id="6dde7-113">Copy the value of **Application Id**. You will need it to configure Microsoft account as an identity provider in your tenant.</span></span>
   
    ![Account Microsoft - ID applicazione](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. <span data-ttu-id="6dde7-115">Fare clic su **Aggiungi piattaforma** e scegliere **Web**.</span><span class="sxs-lookup"><span data-stu-id="6dde7-115">Click on **Add platform** and choose **Web**.</span></span>
   
    ![Account Microsoft - Aggiungi piattaforma](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Account Microsoft - Web](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. <span data-ttu-id="6dde7-118">Immettere `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` nel campo **URI di reindirizzamento** .</span><span class="sxs-lookup"><span data-stu-id="6dde7-118">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Redirect URIs** field.</span></span> <span data-ttu-id="6dde7-119">Sostituire **{tenant}** con il nome del tenant, ad esempio contosob2c.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="6dde7-119">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
   
    ![Account Microsoft - URL di reindirizzamento](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. <span data-ttu-id="6dde7-121">Fare clic su **Genera nuova password** nella sezione **Segreti applicazione**.</span><span class="sxs-lookup"><span data-stu-id="6dde7-121">Click on **Generate New Password** under the **Application Secrets** section.</span></span> <span data-ttu-id="6dde7-122">Copiare la nuova password visualizzata sullo schermo.</span><span class="sxs-lookup"><span data-stu-id="6dde7-122">Copy the new password displayed on screen.</span></span> <span data-ttu-id="6dde7-123">Sarà necessario per configurare un account Microsoft come provider di identità nel tenant.</span><span class="sxs-lookup"><span data-stu-id="6dde7-123">You will need it to configure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="6dde7-124">La password è una credenziale di sicurezza importante.</span><span class="sxs-lookup"><span data-stu-id="6dde7-124">This password is an important security credential.</span></span>
   
    ![Account Microsoft - Genera nuova password](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Account Microsoft - Nuova password](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. <span data-ttu-id="6dde7-127">Selezionare la casella **Supporto Live SDK** nella sezione **Opzioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="6dde7-127">Check the box that says **Live SDK support** under the **Advanced Options** section.</span></span> <span data-ttu-id="6dde7-128">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="6dde7-128">Click **Save**.</span></span>
   
    ![Account Microsoft - Supporto Live SDK](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="6dde7-130">Configurare un account Microsoft come provider di identità nel tenant</span><span class="sxs-lookup"><span data-stu-id="6dde7-130">Configure Microsoft account as an identity provider in your tenant</span></span>
1. <span data-ttu-id="6dde7-131">Seguire questa procedura per [passare al pannello delle funzionalità B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6dde7-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="6dde7-132">Nel pannello delle funzionalità di B2C, fare clic su **Provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="6dde7-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="6dde7-133">Fare clic su **+Aggiungi** nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="6dde7-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="6dde7-134">Fornire un **Nome** per la configurazione del provider di identità.</span><span class="sxs-lookup"><span data-stu-id="6dde7-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="6dde7-135">Ad esempio, immettere "MSA".</span><span class="sxs-lookup"><span data-stu-id="6dde7-135">For example, enter "MSA".</span></span>
5. <span data-ttu-id="6dde7-136">Fare clic su **Tipo di provider di identità**, selezionare **Account Microsoft** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6dde7-136">Click **Identity provider type**, select **Microsoft account**, and click **OK**.</span></span>
6. <span data-ttu-id="6dde7-137">Fare clic su **Set up this identity provider** (Configura il provider di identità) e immettere l'ID applicazione e la password dell'applicazione dell'account Microsoft creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6dde7-137">Click **Set up this identity provider** and enter the Application Id and password of the Microsoft account application that you created earlier.</span></span>
7. <span data-ttu-id="6dde7-138">Fare clic su **OK** e quindi su **Crea** per salvare la configurazione dell'account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6dde7-138">Click **OK** and then click **Create** to save your Microsoft account configuration.</span></span>

