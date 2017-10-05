---
title: 'Azure Active Directory B2C: configurazione di Facebook | Documentazione Microsoft'
description: "Fornire la registrazione e l’accesso agli utenti con account su Facebook nelle applicazioni protette da Azure Active Directory B2C."
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
ms.openlocfilehash: 8c2154fcf33537358b549395d15b4ba937371cd0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-facebook-accounts"></a><span data-ttu-id="9be80-103">Azure Active Directory B2C: fornire l'iscrizione e l'accesso agli utenti con account Facebook</span><span class="sxs-lookup"><span data-stu-id="9be80-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Facebook accounts</span></span>
## <a name="create-a-facebook-application"></a><span data-ttu-id="9be80-104">Creare un'applicazione Facebook</span><span class="sxs-lookup"><span data-stu-id="9be80-104">Create a Facebook application</span></span>
<span data-ttu-id="9be80-105">Per utilizzare Facebook come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario creare un'applicazione Facebook e inserire i parametri corretti.</span><span class="sxs-lookup"><span data-stu-id="9be80-105">To use Facebook as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Facebook application and supply it with the right parameters.</span></span> <span data-ttu-id="9be80-106">Per eseguire questa operazione è necessario disporre di un account Facebook.</span><span class="sxs-lookup"><span data-stu-id="9be80-106">You need a Facebook account to do this.</span></span> <span data-ttu-id="9be80-107">Se non si ha un account, è possibile crearlo nel sito [https://www.facebook.com/](https://www.facebook.com/).</span><span class="sxs-lookup"><span data-stu-id="9be80-107">If you don’t have one, you can get it at [https://www.facebook.com/](https://www.facebook.com/).</span></span>

1. <span data-ttu-id="9be80-108">Passare al [sito Web Facebook for developers](https://developers.facebook.com/) e accedere con le credenziali dell'account Facebook.</span><span class="sxs-lookup"><span data-stu-id="9be80-108">Go to the [Facebook for developers](https://developers.facebook.com/) website and sign in with your Facebook account credentials.</span></span>
2. <span data-ttu-id="9be80-109">Se non è ancora stato fatto, è necessario registrarsi come sviluppatore Facebook.</span><span class="sxs-lookup"><span data-stu-id="9be80-109">If you have not already done so, you need to register as a Facebook developer.</span></span> <span data-ttu-id="9be80-110">A tale scopo, fare clic su **Registrati** nell'angolo in alto a destra della pagina, accettare le condizioni di Facebook e completare la procedura di registrazione.</span><span class="sxs-lookup"><span data-stu-id="9be80-110">To do this, click **Register** (on the upper-right corner of the page), accept Facebook's policies, and complete the registration steps.</span></span>
3. <span data-ttu-id="9be80-111">Fare clic su **My Apps** (App personali) e quindi su **Add a new App** (Aggiungi una nuova app).</span><span class="sxs-lookup"><span data-stu-id="9be80-111">Click **My Apps** and then click **Add a New App**.</span></span> 
4. <span data-ttu-id="9be80-112">Nel modulo fornire un **nome visualizzato** e una **email di contatto** valida.</span><span class="sxs-lookup"><span data-stu-id="9be80-112">In the form, provide a **Display Name** and a valid **Contact Email**.</span></span>
5. <span data-ttu-id="9be80-113">Fare clic su **Crea ID app**.</span><span class="sxs-lookup"><span data-stu-id="9be80-113">Click **Create App ID**.</span></span> <span data-ttu-id="9be80-114">Potrebbe essere necessario accettare i criteri della piattaforma Facebook e completare un controllo di sicurezza online.</span><span class="sxs-lookup"><span data-stu-id="9be80-114">This may require you to accept Facebook platform policies and complete an online security check.</span></span>
6. <span data-ttu-id="9be80-115">Nella colonna di sinistra fare clic su **Impostazioni** e quindi selezionare **Base**, se non è già selezionata.</span><span class="sxs-lookup"><span data-stu-id="9be80-115">In the left column, click **Settings** and then select **Basic** if not selected already.</span></span>
7. <span data-ttu-id="9be80-116">Selezionare una **categoria**.</span><span class="sxs-lookup"><span data-stu-id="9be80-116">Select a **Category**.</span></span> 
8. <span data-ttu-id="9be80-117">Fare clic su **+Add Platform** (+Aggiungi piattaforma) e selezionare **Website** (Sito Web).</span><span class="sxs-lookup"><span data-stu-id="9be80-117">Click **+ Add Platform** and select **Website**.</span></span>
   
    ![Facebook - Impostazioni](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - Impostazioni - sito Web](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. <span data-ttu-id="9be80-120">Immettere `https://login.microsoftonline.com/` nel campo **URL sito** e quindi fare clic su **Salva modifiche** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="9be80-120">Enter `https://login.microsoftonline.com/` in the **Site URL** field and then click **Save Changes** at the bottom of the page.</span></span>
   
    ![Facebook - URL del sito](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. <span data-ttu-id="9be80-122">Copiare il valore di **ID App**.</span><span class="sxs-lookup"><span data-stu-id="9be80-122">Copy the value of **App ID**.</span></span> <span data-ttu-id="9be80-123">Fare clic su **Show** (Mostra) e copiare il valore **App Secret** (Segreto app).</span><span class="sxs-lookup"><span data-stu-id="9be80-123">Click **Show** and copy the value of **App Secret**.</span></span> <span data-ttu-id="9be80-124">Sono necessari entrambi per configurare Facebook come provider di identità nel tenant.</span><span class="sxs-lookup"><span data-stu-id="9be80-124">You will need both of them to configure Facebook as an identity provider in your tenant.</span></span> <span data-ttu-id="9be80-125">**App Segreta** è una credenziale di sicurezza importante.</span><span class="sxs-lookup"><span data-stu-id="9be80-125">**App Secret** is an important security credential.</span></span>
   
    ![Facebook - ID app e segreto app](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. <span data-ttu-id="9be80-127">Fare clic su **Aggiungi prodotto** nel riquadro di spostamento sinistro, quindi fare clic sul pulsante **Configurazione** per **Account di accesso di Facebook**.</span><span class="sxs-lookup"><span data-stu-id="9be80-127">Click **+ Add Product** on the left navigation and then the **Set Up** button for **Facebook Login**.</span></span>
   
    ![Facebook - Accesso a Facebook](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. <span data-ttu-id="9be80-129">Fare clic su **Impostazioni** nel riquadro di spostamento destro in **Account di accesso di Facebook**</span><span class="sxs-lookup"><span data-stu-id="9be80-129">Click **Settings** on the right nav under **Facebook Login**</span></span>

    ![Facebook - Impostazioni Account di accesso di Facebook](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. <span data-ttu-id="9be80-131">Immettere `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` nel campo **Valid OAuth redirect URIs** (URI di reindirizzamento OAuth validi) nella sezione **Client OAuth Settings** (Impostazioni OAuth client).</span><span class="sxs-lookup"><span data-stu-id="9be80-131">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Valid OAuth redirect URIs** field in the **Client OAuth Settings** section.</span></span> <span data-ttu-id="9be80-132">Sostituire **{tenant}** con il nome del tenant, ad esempio contosob2c.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="9be80-132">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="9be80-133">Fare clic su **Salva le modifiche** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="9be80-133">Click **Save Changes** at the bottom of the page.</span></span>
    
    ![Facebook - URI di reindirizzamento OAuth](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. <span data-ttu-id="9be80-135">Per rendere l'applicazione Facebook utilizzabile da AD B2C di Azure, è necessario renderla pubblicamente disponibile.</span><span class="sxs-lookup"><span data-stu-id="9be80-135">To make your Facebook application usable by Azure AD B2C, you need to make it publicly available.</span></span> <span data-ttu-id="9be80-136">A questo scopo, fare clic su **App Review** (Controllo app) nel riquadro di spostamento sinistro, impostare l'opzione nella parte superiore della pagina su **SÌ** e quindi fare clic su **Confirm** (Conferma).</span><span class="sxs-lookup"><span data-stu-id="9be80-136">You can do this by clicking **App Review** on the left navigation and by turning the switch at the top of the page to **YES** and clicking **Confirm**.</span></span>
    
    ![Facebook - App pubblica](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="9be80-138">Configurare Facebook come provider di identità nel tenant</span><span class="sxs-lookup"><span data-stu-id="9be80-138">Configure Facebook as an identity provider in your tenant</span></span>
1. <span data-ttu-id="9be80-139">Seguire questa procedura per [passare al pannello delle funzionalità B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9be80-139">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="9be80-140">Nel pannello delle funzionalità di B2C, fare clic su **Provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="9be80-140">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="9be80-141">Fare clic su **+Aggiungi** nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="9be80-141">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="9be80-142">Fornire un **Nome** per la configurazione del provider di identità.</span><span class="sxs-lookup"><span data-stu-id="9be80-142">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="9be80-143">Ad esempio, immettere "Facebook".</span><span class="sxs-lookup"><span data-stu-id="9be80-143">For example, enter "Facebook".</span></span>
5. <span data-ttu-id="9be80-144">Fare clic su **Identity provider type** (Tipo di provider di identità), selezionare **Facebook** e scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="9be80-144">Click **Identity provider type**, select **Facebook**, and click **OK**.</span></span>
6. <span data-ttu-id="9be80-145">Fare clic su **Set up this identity provider** (Configura questo provider di identità), immettere l'ID app e il segreto app dell'applicazione Facebook creata in precedenza rispettivamente nei campi **ID client** e **Segreto client**.</span><span class="sxs-lookup"><span data-stu-id="9be80-145">Click **Set up this identity provider** and enter the app ID and app secret (of the Facebook application that you created earlier) in the **Client ID** and **Client secret** fields respectively.</span></span>
7. <span data-ttu-id="9be80-146">Fare clic su **OK** e quindi su **Create** (Crea) per salvare la configurazione di Facebook.</span><span class="sxs-lookup"><span data-stu-id="9be80-146">Click **OK**, and then click **Create** to save your Facebook configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="9be80-147">L'aggiunta di un **provider di identità** al tenant non modifica i criteri esistenti.</span><span class="sxs-lookup"><span data-stu-id="9be80-147">Adding an **Identity provider** to your tenant does not modify your existing policies.</span></span> <span data-ttu-id="9be80-148">Ricordare di aggiornare i criteri includendo il provider di identità appena creato.</span><span class="sxs-lookup"><span data-stu-id="9be80-148">Remember to update your policies by including the identity provider you just created.</span></span>
>