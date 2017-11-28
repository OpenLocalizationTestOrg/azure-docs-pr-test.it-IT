---
title: 'Azure Active Directory B2C: Configurazione di LinkedIn | Documentazione Microsoft'
description: Fornire tooconsumers iscrizione e Accedi con l'account di LinkedIn nelle applicazioni che sono protetti da Azure Active Directory B2C
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
ms.openlocfilehash: 6c5233ef48b24968fd6383f470b5d8a969a78ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-linkedin-accounts"></a><span data-ttu-id="4b5f0-103">Azure Active B2C di Directory: Fornire tooconsumers iscrizione e Accedi con gli account di LinkedIn</span><span class="sxs-lookup"><span data-stu-id="4b5f0-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with LinkedIn accounts</span></span>
## <a name="create-a-linkedin-application"></a><span data-ttu-id="4b5f0-104">Creare un'applicazione su LinkedIn</span><span class="sxs-lookup"><span data-stu-id="4b5f0-104">Create a LinkedIn application</span></span>
<span data-ttu-id="4b5f0-105">toouse LinkedIn come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un'applicazione di LinkedIn e fornirlo con i parametri corretti hello.</span><span class="sxs-lookup"><span data-stu-id="4b5f0-105">toouse LinkedIn as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a LinkedIn application and supply it with hello right parameters.</span></span> <span data-ttu-id="4b5f0-106">Necessaria una toodo account LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="4b5f0-106">You need a LinkedIn account toodo this.</span></span> <span data-ttu-id="4b5f0-107">Se non si ha un account, è possibile crearlo nel sito [https://www.linkedin.com/](https://www.linkedin.com/).</span><span class="sxs-lookup"><span data-stu-id="4b5f0-107">If you don’t have one, you can get it at [https://www.linkedin.com/](https://www.linkedin.com/).</span></span>

1. <span data-ttu-id="4b5f0-108">Passare toohello [sito Web gli sviluppatori di LinkedIn](https://www.developer.linkedin.com/) e accedere con le credenziali dell'account LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="4b5f0-108">Go toohello [LinkedIn Developers website](https://www.developer.linkedin.com/) and sign in with your LinkedIn account credentials.</span></span>
2. <span data-ttu-id="4b5f0-109">Fare clic su **My Apps** in hello barra dei menu superiore e quindi fare clic su **Crea applicazione**.</span><span class="sxs-lookup"><span data-stu-id="4b5f0-109">Click **My Apps** in hello top menu bar and then click **Create Application**.</span></span>
   
    ![LinkedIn - Nuova app](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. <span data-ttu-id="4b5f0-111">In hello **creare una nuova applicazione** modulo, inserire le informazioni pertinenti hello (**nome società**, **nome**, **descrizione**, **URL del Logo dell'applicazione**, **l'utilizzo dell'applicazione**, **URL del sito Web**, **posta elettronica aziendali** e **telefono ufficio**).</span><span class="sxs-lookup"><span data-stu-id="4b5f0-111">In hello **Create a New Application** form, fill in hello relevant information (**Company Name**, **Name**, **Description**, **Application Logo URL**, **Application Use**, **Website URL**, **Business Email** and **Business Phone**).</span></span>
4. <span data-ttu-id="4b5f0-112">Accettare toohello **condizioni di utilizzo dell'API di LinkedIn** e fare clic su **Invia**.</span><span class="sxs-lookup"><span data-stu-id="4b5f0-112">Agree toohello **LinkedIn API Terms of Use** and click **Submit**.</span></span>
   
    ![LinkedIn - Registro app](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. <span data-ttu-id="4b5f0-114">Copiare i valori hello di **ID Client** e **segreto Client**.</span><span class="sxs-lookup"><span data-stu-id="4b5f0-114">Copy hello values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="4b5f0-115">che si trovano nella sezione **Authentication Keys** (Chiavi di autenticazione). Sarà necessario entrambi tooconfigure LinkedIn come provider di identità nel tenant.</span><span class="sxs-lookup"><span data-stu-id="4b5f0-115">(You can find them under **Authentication Keys**.) You will need both of them tooconfigure LinkedIn as an identity provider in your tenant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4b5f0-116">**Client Segreto** è un'importante credenziale di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="4b5f0-116">**Client Secret** is an important security credential.</span></span>
   > 
   > 
6. <span data-ttu-id="4b5f0-117">Immettere `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **autorizzato URL di reindirizzamento** campo (in **OAuth 2.0**).</span><span class="sxs-lookup"><span data-stu-id="4b5f0-117">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized Redirect URLs** field (under **OAuth 2.0**).</span></span> <span data-ttu-id="4b5f0-118">Sostituire **{tenant}** con il nome del tenant, ad esempio contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="4b5f0-118">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="4b5f0-119">Fare clic su **Add** (Aggiungi) e quindi su **Update** (Aggiorna).</span><span class="sxs-lookup"><span data-stu-id="4b5f0-119">Click **Add**, and then click **Update**.</span></span> <span data-ttu-id="4b5f0-120">Hello **{tenant}** valore è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="4b5f0-120">hello **{tenant}** value is case-sensitive.</span></span>
   
    ![LinkedIn - Installazione app](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="4b5f0-122">Configurare LinkedIn come provider di identità nel tenant</span><span class="sxs-lookup"><span data-stu-id="4b5f0-122">Configure LinkedIn as an identity provider in your tenant</span></span>
1. <span data-ttu-id="4b5f0-123">Seguire questi passaggi troppo[passare pannello funzionalità toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) su hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4b5f0-123">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="4b5f0-124">Nel Pannello di hello B2C funzionalità, fare clic su **provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="4b5f0-124">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="4b5f0-125">Fare clic su **+ Aggiungi** nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="4b5f0-125">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="4b5f0-126">Fornire un nome **nome** per la configurazione del provider di identità hello.</span><span class="sxs-lookup"><span data-stu-id="4b5f0-126">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="4b5f0-127">Ad esempio, immettere "LI".</span><span class="sxs-lookup"><span data-stu-id="4b5f0-127">For example, enter "LI".</span></span>
5. <span data-ttu-id="4b5f0-128">Fare clic su **Identity provider type** (Tipo di provider di identità), selezionare **LinkedIn** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b5f0-128">Click **Identity provider type**, select **LinkedIn**, and click **OK**.</span></span>
6. <span data-ttu-id="4b5f0-129">Fare clic su **impostare il provider di identità** e immettere privata hello client ID e il client di hello LinkedIn applicazione creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4b5f0-129">Click **Set up this identity provider** and enter hello client ID and client secret of hello LinkedIn application that you created earlier.</span></span>
7. <span data-ttu-id="4b5f0-130">Fare clic su **OK** e quindi fare clic su **crea** toosave la configurazione di LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="4b5f0-130">Click **OK** and then click **Create** toosave your LinkedIn configuration.</span></span>

