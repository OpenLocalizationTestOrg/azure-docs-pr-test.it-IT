---
title: 'Azure Active Directory B2C: configurazione di Amazon | Documentazione Microsoft'
description: Fornire tooconsumers iscrizione e Accedi con l'account di Amazon nelle applicazioni che sono protetti da Azure Active Directory B2C.
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
ms.openlocfilehash: 60d7c4b76d9d3e86ed535765329abed07f1e5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-amazon-accounts"></a><span data-ttu-id="b1220-103">Azure Active B2C di Directory: Fornire tooconsumers iscrizione e Accedi con account di Amazon</span><span class="sxs-lookup"><span data-stu-id="b1220-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Amazon accounts</span></span>
## <a name="create-an-amazon-application"></a><span data-ttu-id="b1220-104">Creare un'applicazione Amazon</span><span class="sxs-lookup"><span data-stu-id="b1220-104">Create an Amazon application</span></span>
<span data-ttu-id="b1220-105">toouse Amazon come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un'applicazione di Amazon e fornirlo con i parametri corretti hello.</span><span class="sxs-lookup"><span data-stu-id="b1220-105">toouse Amazon as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate an Amazon application and supply it with hello right parameters.</span></span> <span data-ttu-id="b1220-106">È necessario un toodo account Amazon questo.</span><span class="sxs-lookup"><span data-stu-id="b1220-106">You need an Amazon account toodo this.</span></span> <span data-ttu-id="b1220-107">Se non si ha un account, è possibile crearlo nel sito [http://www.amazon.com/](http://www.amazon.com/).</span><span class="sxs-lookup"><span data-stu-id="b1220-107">If you don’t have one, you can get it at [http://www.amazon.com/](http://www.amazon.com/).</span></span>

1. <span data-ttu-id="b1220-108">Passare toohello [Centro per sviluppatori Amazon](https://login.amazon.com/) e accedere con le credenziali dell'account Amazon.</span><span class="sxs-lookup"><span data-stu-id="b1220-108">Go toohello [Amazon Developer Center](https://login.amazon.com/) and sign in with your Amazon account credentials.</span></span>
2. <span data-ttu-id="b1220-109">Se non è già stato fatto, fare clic su **iscrizione**, attenersi alla procedura di registrazione per sviluppatori hello e accettano criteri hello.</span><span class="sxs-lookup"><span data-stu-id="b1220-109">If you have not already done so, click **Sign Up**, follow hello developer registration steps, and accept hello policy.</span></span>
3. <span data-ttu-id="b1220-110">Fare clic su **Registra nuova applicazione**.</span><span class="sxs-lookup"><span data-stu-id="b1220-110">Click **Register new application**.</span></span>
   
    ![Registrazione di una nuova applicazione nel sito Web di Amazon hello](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. <span data-ttu-id="b1220-112">Fornire informazioni sull'applicazione, come **Name** (Nome), **Description** (Descrizione) e **Privacy Notice URL** (URL informativa sulla privacy) e fare clic su **Save** (Salva).</span><span class="sxs-lookup"><span data-stu-id="b1220-112">Provide application information (**Name**, **Description**, and **Privacy Notice URL**) and click **Save**.</span></span>
   
    ![Inserimento delle informazioni sull'applicazione per la registrazione di una nuova applicazione in Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. <span data-ttu-id="b1220-114">In hello **impostazioni Web** sezione valori hello copia di **ID Client** e **segreto Client**.</span><span class="sxs-lookup"><span data-stu-id="b1220-114">In hello **Web Settings** section, copy hello values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="b1220-115">(È necessario hello tooclick **Mostra segreto** pulsante questo toosee.) È necessario che entrambi gli elementi tooconfigure Amazon come provider di identità nel tenant.</span><span class="sxs-lookup"><span data-stu-id="b1220-115">(You need tooclick hello **Show Secret** button toosee this.) You need both of them tooconfigure Amazon as an identity provider in your tenant.</span></span> <span data-ttu-id="b1220-116">Fare clic su **modifica** nella parte inferiore di hello della sezione hello.</span><span class="sxs-lookup"><span data-stu-id="b1220-116">Click **Edit** at hello bottom of hello section.</span></span> <span data-ttu-id="b1220-117">**Client Segreto** è un'importante credenziale di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="b1220-117">**Client Secret** is an important security credential.</span></span>
   
    ![Inserimento dell'ID Client e del Segreto client per la nuova applicazione in Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. <span data-ttu-id="b1220-119">Immettere `https://login.microsoftonline.com` in hello **consentito JavaScript Origins** campo e `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **consentito URL restituiti** campo.</span><span class="sxs-lookup"><span data-stu-id="b1220-119">Enter `https://login.microsoftonline.com` in hello **Allowed JavaScript Origins** field and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Allowed Return URLs** field.</span></span> <span data-ttu-id="b1220-120">Sostituire **{tenant}** con il nome del tenant, ad esempio contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="b1220-120">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="b1220-121">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="b1220-121">Click **Save**.</span></span> <span data-ttu-id="b1220-122">Hello **{tenant}** valore è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="b1220-122">hello **{tenant}** value is case-sensitive.</span></span>
   
    ![Inserimento delle origini JavaScript e degli URL restituiti per la nuova applicazione in Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="b1220-124">Configurare Amazon come provider di identità nel tenant</span><span class="sxs-lookup"><span data-stu-id="b1220-124">Configure Amazon as an identity provider in your tenant</span></span>
1. <span data-ttu-id="b1220-125">Seguire questi passaggi troppo[passare pannello funzionalità toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) su hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b1220-125">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="b1220-126">Nel Pannello di hello B2C funzionalità, fare clic su **provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="b1220-126">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="b1220-127">Fare clic su **+ Aggiungi** nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="b1220-127">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="b1220-128">Fornire un nome **nome** per la configurazione del provider di identità hello.</span><span class="sxs-lookup"><span data-stu-id="b1220-128">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="b1220-129">Ad esempio, immettere "Amzn".</span><span class="sxs-lookup"><span data-stu-id="b1220-129">For example, enter "Amzn".</span></span>
5. <span data-ttu-id="b1220-130">Fare clic su **Identity provider type** (Tipo di provider di identità), selezionare **Amazon** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b1220-130">Click **Identity provider type**, select **Amazon**, and click **OK**.</span></span>
6. <span data-ttu-id="b1220-131">Fare clic su **impostare il provider di identità** e immettere privata hello client ID e il client di hello applicazione Amazon creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b1220-131">Click **Set up this identity provider** and enter hello client ID and client secret of hello Amazon application that you created earlier.</span></span>
7. <span data-ttu-id="b1220-132">Fare clic su **OK** e quindi fare clic su **crea** toosave la configurazione di Amazon.</span><span class="sxs-lookup"><span data-stu-id="b1220-132">Click **OK** and then click **Create** toosave your Amazon configuration.</span></span>

