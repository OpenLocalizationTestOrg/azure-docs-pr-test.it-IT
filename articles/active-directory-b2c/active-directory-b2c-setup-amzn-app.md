---
title: 'Azure Active Directory B2C: configurazione di Amazon | Documentazione Microsoft'
description: "Fornire la registrazione e l’accesso agli utenti con account Amazon nelle applicazioni protette da Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 77c099bb-a005-4d75-87f9-f61e3de48725
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: dcc97e1b7f6287bd7692c52bf068950065a26572
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-amazon-accounts"></a><span data-ttu-id="fccc9-103">Azure Active Directory B2C: fornire l'iscrizione e l'accesso agli utenti con account Amazon</span><span class="sxs-lookup"><span data-stu-id="fccc9-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Amazon accounts</span></span>
## <a name="create-an-amazon-application"></a><span data-ttu-id="fccc9-104">Creare un'applicazione Amazon</span><span class="sxs-lookup"><span data-stu-id="fccc9-104">Create an Amazon application</span></span>
<span data-ttu-id="fccc9-105">Per usare Amazon come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario creare un'applicazione Amazon e inserire i parametri corretti.</span><span class="sxs-lookup"><span data-stu-id="fccc9-105">To use Amazon as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an Amazon application and supply it with the right parameters.</span></span> <span data-ttu-id="fccc9-106">Per eseguire questa operazione è necessario disporre di un account Amazon.</span><span class="sxs-lookup"><span data-stu-id="fccc9-106">You need an Amazon account to do this.</span></span> <span data-ttu-id="fccc9-107">Se non si ha un account, è possibile crearlo nel sito [http://www.amazon.com/](http://www.amazon.com/).</span><span class="sxs-lookup"><span data-stu-id="fccc9-107">If you don’t have one, you can get it at [http://www.amazon.com/](http://www.amazon.com/).</span></span>

1. <span data-ttu-id="fccc9-108">Visitare il [Centro sviluppatori Amazon](https://login.amazon.com/) e accedere con le credenziali dell'account Amazon.</span><span class="sxs-lookup"><span data-stu-id="fccc9-108">Go to the [Amazon Developer Center](https://login.amazon.com/) and sign in with your Amazon account credentials.</span></span>
2. <span data-ttu-id="fccc9-109">Se non è già stato fatto, fare clic su **Sign Up**(Iscrizione), seguire la procedura di registrazione per sviluppatori e accettare le condizioni.</span><span class="sxs-lookup"><span data-stu-id="fccc9-109">If you have not already done so, click **Sign Up**, follow the developer registration steps, and accept the policy.</span></span>
3. <span data-ttu-id="fccc9-110">Fare clic su **Registra nuova applicazione**.</span><span class="sxs-lookup"><span data-stu-id="fccc9-110">Click **Register new application**.</span></span>
   
    ![Registrazione di una nuova applicazione nel sito Web di Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. <span data-ttu-id="fccc9-112">Fornire informazioni sull'applicazione, come **Name** (Nome), **Description** (Descrizione) e **Privacy Notice URL** (URL informativa sulla privacy) e fare clic su **Save** (Salva).</span><span class="sxs-lookup"><span data-stu-id="fccc9-112">Provide application information (**Name**, **Description**, and **Privacy Notice URL**) and click **Save**.</span></span>
   
    ![Inserimento delle informazioni sull'applicazione per la registrazione di una nuova applicazione in Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. <span data-ttu-id="fccc9-114">Nella sezione **Web Settings** (Impostazioni Web) copiare i valori di **Client ID** (ID Client) e **Client Secret** (Segreto client).</span><span class="sxs-lookup"><span data-stu-id="fccc9-114">In the **Web Settings** section, copy the values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="fccc9-115">Sarà necessario fare clic sul pulsante **Show Secret** (Mostra segreto) per visualizzarlo. Sono necessari entrambi per configurare Amazon come provider di identità nel tenant.</span><span class="sxs-lookup"><span data-stu-id="fccc9-115">(You need to click the **Show Secret** button to see this.) You need both of them to configure Amazon as an identity provider in your tenant.</span></span> <span data-ttu-id="fccc9-116">Fare clic su **Modifica** nella parte inferiore della sezione.</span><span class="sxs-lookup"><span data-stu-id="fccc9-116">Click **Edit** at the bottom of the section.</span></span> <span data-ttu-id="fccc9-117">**Client Segreto** è un'importante credenziale di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="fccc9-117">**Client Secret** is an important security credential.</span></span>
   
    ![Inserimento dell'ID Client e del Segreto client per la nuova applicazione in Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. <span data-ttu-id="fccc9-119">Immettere `https://login.microsoftonline.com` nel campo **Allowed JavaScript Origins** (Origini JavaScript consentite) e `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` nel campo **Allowed Return URLs** (URL restituiti consentiti).</span><span class="sxs-lookup"><span data-stu-id="fccc9-119">Enter `https://login.microsoftonline.com` in the **Allowed JavaScript Origins** field and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Allowed Return URLs** field.</span></span> <span data-ttu-id="fccc9-120">Sostituire **{tenant}** con il nome del tenant, ad esempio contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="fccc9-120">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="fccc9-121">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="fccc9-121">Click **Save**.</span></span> <span data-ttu-id="fccc9-122">Il valore **{tenant}** distingue tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="fccc9-122">The **{tenant}** value is case-sensitive.</span></span>
   
    ![Inserimento delle origini JavaScript e degli URL restituiti per la nuova applicazione in Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="fccc9-124">Configurare Amazon come provider di identità nel tenant</span><span class="sxs-lookup"><span data-stu-id="fccc9-124">Configure Amazon as an identity provider in your tenant</span></span>
1. <span data-ttu-id="fccc9-125">Seguire questa procedura per [passare al pannello delle funzionalità B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fccc9-125">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="fccc9-126">Nel pannello delle funzionalità di B2C, fare clic su **Provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="fccc9-126">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="fccc9-127">Fare clic su **+Aggiungi** nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="fccc9-127">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="fccc9-128">Fornire un **Nome** per la configurazione del provider di identità.</span><span class="sxs-lookup"><span data-stu-id="fccc9-128">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="fccc9-129">Ad esempio, immettere "Amzn".</span><span class="sxs-lookup"><span data-stu-id="fccc9-129">For example, enter "Amzn".</span></span>
5. <span data-ttu-id="fccc9-130">Fare clic su **Identity provider type** (Tipo di provider di identità), selezionare **Amazon** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="fccc9-130">Click **Identity provider type**, select **Amazon**, and click **OK**.</span></span>
6. <span data-ttu-id="fccc9-131">Fare clic su **Configura questo provider di identità** e immettere l'ID client e il segreto client dell'applicazione Amazon creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="fccc9-131">Click **Set up this identity provider** and enter the client ID and client secret of the Amazon application that you created earlier.</span></span>
7. <span data-ttu-id="fccc9-132">Fare clic su **OK** e quindi su **Crea** per salvare la configurazione di Amazon.</span><span class="sxs-lookup"><span data-stu-id="fccc9-132">Click **OK** and then click **Create** to save your Amazon configuration.</span></span>

