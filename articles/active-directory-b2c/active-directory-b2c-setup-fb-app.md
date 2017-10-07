---
title: 'Azure Active Directory B2C: configurazione di Facebook | Documentazione Microsoft'
description: Fornire tooconsumers iscrizione e Accedi con Facebook account nelle applicazioni che sono protetti da Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: sromeroz
manager: krassk
editor: sromeroz
ms.assetid: b875f235-a1d2-4abb-b9f0-b89beac38a32
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/7/2017
ms.author: sromeroz
ms.openlocfilehash: 4c3b79c7248bd1e789bf33fc467abb27d0170edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-facebook-accounts"></a><span data-ttu-id="3056d-103">Azure Active B2C di Directory: Fornire tooconsumers iscrizione e Accedi con account Facebook</span><span class="sxs-lookup"><span data-stu-id="3056d-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Facebook accounts</span></span>
## <a name="create-a-facebook-application"></a><span data-ttu-id="3056d-104">Creare un'applicazione Facebook</span><span class="sxs-lookup"><span data-stu-id="3056d-104">Create a Facebook application</span></span>
<span data-ttu-id="3056d-105">toouse Facebook come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un'applicazione Facebook e fornirlo con i parametri corretti hello.</span><span class="sxs-lookup"><span data-stu-id="3056d-105">toouse Facebook as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Facebook application and supply it with hello right parameters.</span></span> <span data-ttu-id="3056d-106">Necessaria una toodo account Facebook.</span><span class="sxs-lookup"><span data-stu-id="3056d-106">You need a Facebook account toodo this.</span></span> <span data-ttu-id="3056d-107">Se non si ha un account, è possibile crearlo nel sito [https://www.facebook.com/](https://www.facebook.com/).</span><span class="sxs-lookup"><span data-stu-id="3056d-107">If you don’t have one, you can get it at [https://www.facebook.com/](https://www.facebook.com/).</span></span>

1. <span data-ttu-id="3056d-108">Passare toohello [Facebook per gli sviluppatori](https://developers.facebook.com/) sito Web e accedere con il Facebook delle credenziali dell'account.</span><span class="sxs-lookup"><span data-stu-id="3056d-108">Go toohello [Facebook for developers](https://developers.facebook.com/) website and sign in with your Facebook account credentials.</span></span>
2. <span data-ttu-id="3056d-109">Se non è già stato fatto, è necessario tooregister gli sviluppatori Facebook.</span><span class="sxs-lookup"><span data-stu-id="3056d-109">If you have not already done so, you need tooregister as a Facebook developer.</span></span> <span data-ttu-id="3056d-110">toodo, fare clic su **registrare** (su hello angolo superiore destro della pagina hello), accettare i criteri di Facebook e completare i passaggi di registrazione hello.</span><span class="sxs-lookup"><span data-stu-id="3056d-110">toodo this, click **Register** (on hello upper-right corner of hello page), accept Facebook's policies, and complete hello registration steps.</span></span>
3. <span data-ttu-id="3056d-111">Fare clic su **My Apps** (App personali) e quindi su **Add a new App** (Aggiungi una nuova app).</span><span class="sxs-lookup"><span data-stu-id="3056d-111">Click **My Apps** and then click **Add a New App**.</span></span> 
4. <span data-ttu-id="3056d-112">Nel modulo hello, fornire un **nome visualizzato** e valido **Contact Email**.</span><span class="sxs-lookup"><span data-stu-id="3056d-112">In hello form, provide a **Display Name** and a valid **Contact Email**.</span></span>
5. <span data-ttu-id="3056d-113">Fare clic su **Crea ID app**.</span><span class="sxs-lookup"><span data-stu-id="3056d-113">Click **Create App ID**.</span></span> <span data-ttu-id="3056d-114">Questo potrebbe richiede i criteri della piattaforma Facebook tooaccept e completare una verifica di protezione in linea.</span><span class="sxs-lookup"><span data-stu-id="3056d-114">This may require you tooaccept Facebook platform policies and complete an online security check.</span></span>
6. <span data-ttu-id="3056d-115">Nella colonna sinistra hello, fare clic su **impostazioni** e quindi selezionare **base** se non è già selezionata.</span><span class="sxs-lookup"><span data-stu-id="3056d-115">In hello left column, click **Settings** and then select **Basic** if not selected already.</span></span>
7. <span data-ttu-id="3056d-116">Selezionare una **categoria**.</span><span class="sxs-lookup"><span data-stu-id="3056d-116">Select a **Category**.</span></span> 
8. <span data-ttu-id="3056d-117">Fare clic su **+Add Platform** (+Aggiungi piattaforma) e selezionare **Website** (Sito Web).</span><span class="sxs-lookup"><span data-stu-id="3056d-117">Click **+ Add Platform** and select **Website**.</span></span>
   
    ![Facebook - Impostazioni](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - Impostazioni - sito Web](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. <span data-ttu-id="3056d-120">Immettere `https://login.microsoftonline.com/` in hello **URL del sito** campo e quindi fare clic su **Salva modifiche** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="3056d-120">Enter `https://login.microsoftonline.com/` in hello **Site URL** field and then click **Save Changes** at hello bottom of hello page.</span></span>
   
    ![Facebook - URL del sito](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. <span data-ttu-id="3056d-122">Copiare il valore di hello di **ID App**.</span><span class="sxs-lookup"><span data-stu-id="3056d-122">Copy hello value of **App ID**.</span></span> <span data-ttu-id="3056d-123">Fare clic su **Mostra** e copiare il valore di hello di **segreto dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="3056d-123">Click **Show** and copy hello value of **App Secret**.</span></span> <span data-ttu-id="3056d-124">Sarà necessario entrambi tooconfigure Facebook come provider di identità nel tenant.</span><span class="sxs-lookup"><span data-stu-id="3056d-124">You will need both of them tooconfigure Facebook as an identity provider in your tenant.</span></span> <span data-ttu-id="3056d-125">**App Segreta** è una credenziale di sicurezza importante.</span><span class="sxs-lookup"><span data-stu-id="3056d-125">**App Secret** is an important security credential.</span></span>
   
    ![Facebook - ID app e segreto app](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. <span data-ttu-id="3056d-127">Fare clic su **+ Aggiungi prodotto** hello spostamento a sinistra e quindi hello **Set Up** pulsante **account Facebook**.</span><span class="sxs-lookup"><span data-stu-id="3056d-127">Click **+ Add Product** on hello left navigation and then hello **Set Up** button for **Facebook Login**.</span></span>
   
    ![Facebook - Accesso a Facebook](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. <span data-ttu-id="3056d-129">Fare clic su **impostazioni** in esplorazione hello in **account Facebook**</span><span class="sxs-lookup"><span data-stu-id="3056d-129">Click **Settings** on hello right nav under **Facebook Login**</span></span>

    ![Facebook - Impostazioni Account di accesso di Facebook](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. <span data-ttu-id="3056d-131">Immettere `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **URI di reindirizzamento di OAuth valido** campo hello **impostazioni OAuth Client** sezione.</span><span class="sxs-lookup"><span data-stu-id="3056d-131">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Valid OAuth redirect URIs** field in hello **Client OAuth Settings** section.</span></span> <span data-ttu-id="3056d-132">Sostituire **{tenant}** con il nome del tenant, ad esempio contosob2c.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="3056d-132">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="3056d-133">Fare clic su **Salva modifiche** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="3056d-133">Click **Save Changes** at hello bottom of hello page.</span></span>
    
    ![Facebook - URI di reindirizzamento OAuth](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. <span data-ttu-id="3056d-135">toomake applicazione Facebook utilizzabile da Azure Active Directory B2C, è necessario toomake pubblicamente disponibile.</span><span class="sxs-lookup"><span data-stu-id="3056d-135">toomake your Facebook application usable by Azure AD B2C, you need toomake it publicly available.</span></span> <span data-ttu-id="3056d-136">È possibile farlo facendo **revisione di App** nel riquadro di spostamento sinistro hello e attivazione hello passare nella parte superiore di hello della pagina hello troppo**Sì** e facendo clic su **conferma**.</span><span class="sxs-lookup"><span data-stu-id="3056d-136">You can do this by clicking **App Review** on hello left navigation and by turning hello switch at hello top of hello page too**YES** and clicking **Confirm**.</span></span>
    
    ![Facebook - App pubblica](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="3056d-138">Configurare Facebook come provider di identità nel tenant</span><span class="sxs-lookup"><span data-stu-id="3056d-138">Configure Facebook as an identity provider in your tenant</span></span>
1. <span data-ttu-id="3056d-139">Seguire questi passaggi troppo[passare pannello funzionalità toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) su hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3056d-139">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="3056d-140">Nel Pannello di hello B2C funzionalità, fare clic su **provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="3056d-140">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="3056d-141">Fare clic su **+ Aggiungi** nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="3056d-141">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="3056d-142">Fornire un nome **nome** per la configurazione del provider di identità hello.</span><span class="sxs-lookup"><span data-stu-id="3056d-142">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="3056d-143">Ad esempio, immettere "Facebook".</span><span class="sxs-lookup"><span data-stu-id="3056d-143">For example, enter "Facebook".</span></span>
5. <span data-ttu-id="3056d-144">Fare clic su **Identity provider type** (Tipo di provider di identità), selezionare **Facebook** e scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="3056d-144">Click **Identity provider type**, select **Facebook**, and click **OK**.</span></span>
6. <span data-ttu-id="3056d-145">Fare clic su **impostare il provider di identità** e immettere hello ID e app segreto dell'applicazione (di hello applicazione Facebook creato in precedenza) in hello **ID Client** e **segreto Client**campi rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="3056d-145">Click **Set up this identity provider** and enter hello app ID and app secret (of hello Facebook application that you created earlier) in hello **Client ID** and **Client secret** fields respectively.</span></span>
7. <span data-ttu-id="3056d-146">Fare clic su **OK**, quindi fare clic su **crea** toosave la configurazione di Facebook.</span><span class="sxs-lookup"><span data-stu-id="3056d-146">Click **OK**, and then click **Create** toosave your Facebook configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="3056d-147">Aggiunta di un **provider di identità** tooyour tenant non modifica i criteri esistenti.</span><span class="sxs-lookup"><span data-stu-id="3056d-147">Adding an **Identity provider** tooyour tenant does not modify your existing policies.</span></span> <span data-ttu-id="3056d-148">Tenere presente tooupdate i criteri includendo i provider di identità hello che appena creato.</span><span class="sxs-lookup"><span data-stu-id="3056d-148">Remember tooupdate your policies by including hello identity provider you just created.</span></span>
>