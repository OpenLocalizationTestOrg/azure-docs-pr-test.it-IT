---
title: gli account sviluppatore aaaAuthorize tramite Azure Active Directory B2C - gestione API di Azure | Documenti Microsoft
description: Informazioni su come gli utenti di tooauthorize usando Azure Active Directory B2C in Gestione API.
services: api-management
documentationcenter: API Management
author: miaojiang
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 28f7cae53138938dbbc848b4afcbf08b72690e37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a><span data-ttu-id="ddc5f-103">La modalità sviluppatore tooauthorize degli account con Azure Active Directory B2C in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="ddc5f-103">How tooauthorize developer accounts by using Azure Active Directory B2C in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="ddc5f-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ddc5f-104">Overview</span></span>
<span data-ttu-id="ddc5f-105">Azure Active Directory B2C è una soluzione di gestione delle identità cloud per applicazioni per dispositivi mobili e Web rivolte agli utenti.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-105">Azure Active Directory B2C is a cloud identity management solution for consumer-facing web and mobile applications.</span></span> <span data-ttu-id="ddc5f-106">È possibile utilizzare il portale per sviluppatori di toomanage accesso tooyour.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-106">You can use it toomanage access tooyour developer portal.</span></span> <span data-ttu-id="ddc5f-107">Questa guida viene illustrata hello configurazione necessarie nel toointegrate servizio Gestione API con Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-107">This guide shows you hello configuration that's required in your API Management service toointegrate with Azure Active Directory B2C.</span></span> <span data-ttu-id="ddc5f-108">Per informazioni sull'abilitazione di portale per sviluppatori di accesso toohello utilizzando Active Directory di Azure classico, vedere [modalità sviluppatore tooauthorize degli account con Azure Active Directory].</span><span class="sxs-lookup"><span data-stu-id="ddc5f-108">For information about enabling access toohello developer portal by using classic Azure Active Directory, see [How tooauthorize developer accounts using Azure Active Directory].</span></span>

> [!NOTE]
> <span data-ttu-id="ddc5f-109">passaggi di hello toocomplete in questa Guida, è innanzitutto necessario un toocreate tenant Azure Active Directory B2C un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-109">toocomplete hello steps in this guide, you must first have an Azure Active Directory B2C tenant toocreate an application in.</span></span> <span data-ttu-id="ddc5f-110">Inoltre, è necessario criteri di iscrizione e signin toohave pronto.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-110">Also, you need toohave signup and signin policies ready.</span></span> <span data-ttu-id="ddc5f-111">Per altre informazioni, vedere la [panoramica di Azure Active Directory B2C].</span><span class="sxs-lookup"><span data-stu-id="ddc5f-111">For more information, see [Azure Active Directory B2C overview].</span></span>

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a><span data-ttu-id="ddc5f-112">Autorizzare gli account per sviluppatore usando Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="ddc5f-112">Authorize developer accounts by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="ddc5f-113">tooget avviato, fare clic su **portale di pubblicazione** nel portale di Azure per il servizio Gestione API hello.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-113">tooget started, click **Publisher portal** in hello Azure portal for your API Management service.</span></span> <span data-ttu-id="ddc5f-114">Consente di procedere toohello portale di pubblicazione di gestione API.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-114">This takes you toohello API Management publisher portal.</span></span>

   ![Portale di pubblicazione][api-management-management-console]

   > [!NOTE]
   > <span data-ttu-id="ddc5f-116">Se è ancora stata creata un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [iniziare con gestione API di Azure esercitazione][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="ddc5f-116">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management tutorial][Get started with Azure API Management].</span></span>

2. <span data-ttu-id="ddc5f-117">In hello **gestione API** menu, fare clic su **sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-117">On hello **API Management** menu, click **Security**.</span></span> <span data-ttu-id="ddc5f-118">In hello **identità** scegliere **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-118">On hello **Identities** tab, choose **Azure Active Directory B2C**.</span></span>

  ![Identità esterne 1][api-management-howto-aad-b2c-security-tab]

3. <span data-ttu-id="ddc5f-120">Prendere nota di hello **l'URL di reindirizzamento** e passare tooAzure Active Directory B2C in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-120">Make a note of hello **Redirect URL** and switch over tooAzure Active Directory B2C in hello Azure portal.</span></span>

  ![Identità esterne 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. <span data-ttu-id="ddc5f-122">Fare clic su hello **applicazioni** pulsante.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-122">Click hello **Applications** button.</span></span>

  ![Registrare una nuova applicazione 1][api-management-howto-aad-b2c-portal-menu]

5. <span data-ttu-id="ddc5f-124">Fare clic su hello **Aggiungi** pulsante applicazione toocreate un nuovo B2C Directory Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-124">Click hello **Add** button toocreate a new Azure Active Directory B2C application.</span></span>

  ![Registrare una nuova applicazione 2][api-management-howto-aad-b2c-add-button]

6. <span data-ttu-id="ddc5f-126">In hello **nuova applicazione** pannello, immettere un nome per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-126">In hello **New application** blade, enter a name for hello application.</span></span> <span data-ttu-id="ddc5f-127">Scegliere **Sì** in **App Web/API Web** e quindi **Sì** in **Consenti flusso implicito**.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-127">Choose **Yes** under **Web App/Web API**, and choose **Yes** under **Allow implicit flow**.</span></span> <span data-ttu-id="ddc5f-128">Quindi hello copia **l'URL di reindirizzamento** da hello **Azure Active Directory B2C** sezione di hello **identità** scheda nel portale di pubblicazione hello e incollarla hello **URL di risposta** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-128">Then copy hello **Redirect URL** from hello **Azure Active Directory B2C** section of hello **Identities** tab in hello publisher portal, and paste it into hello **Reply URL** text box.</span></span>

  ![Registrare una nuova applicazione 3][api-management-howto-aad-b2c-app-details]

7. <span data-ttu-id="ddc5f-130">Fare clic su hello **crea** pulsante.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-130">Click hello **Create** button.</span></span> <span data-ttu-id="ddc5f-131">Quando viene creata un'applicazione hello, viene visualizzata in hello **applicazioni** blade.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-131">When hello application is created, it appears in hello **Applications** blade.</span></span> <span data-ttu-id="ddc5f-132">Fare clic su hello applicazione nome toosee i dettagli.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-132">Click hello application name toosee its details.</span></span>

  ![Registrare una nuova applicazione 4][api-management-howto-aad-b2c-app-created]

8. <span data-ttu-id="ddc5f-134">Da hello **proprietà** blade, hello copia **ID applicazione** toohello Appunti.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-134">From hello **Properties** blade, copy hello **Application ID** toohello clipboard.</span></span>

  ![ID applicazione 1][api-management-howto-aad-b2c-app-id]

9. <span data-ttu-id="ddc5f-136">Passa indietro toohello portale di pubblicazione e incollare hello ID hello **Id Client** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-136">Switch back toohello publisher portal and paste hello ID into hello **Client Id** text box.</span></span>

  ![ID applicazione 2][api-management-howto-aad-b2c-client-id]

10. <span data-ttu-id="ddc5f-138">Passa indietro toohello portale di Azure, fare clic su hello **chiavi** pulsante e quindi fare clic su **Genera chiave**.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-138">Switch back toohello Azure portal, click hello **Keys** button, and then click **Generate key**.</span></span> <span data-ttu-id="ddc5f-139">Fare clic su **salvare** hello di configurazione e la visualizzazione di hello toosave **chiave App**.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-139">Click **Save** toosave hello configuration and display hello **App key**.</span></span> <span data-ttu-id="ddc5f-140">Copiare negli Appunti toohello chiave hello.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-140">Copy hello key toohello clipboard.</span></span>

  ![Chiave dell'app 1][api-management-howto-aad-b2c-app-key]

11. <span data-ttu-id="ddc5f-142">Commutatore toohello back-portale e Incolla hello chiave editore in hello **segreto Client** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-142">Switch back toohello publisher portal and paste hello key into hello **Client Secret** text box.</span></span>

  ![Chiave dell'app 2][api-management-howto-aad-b2c-client-secret]

12. <span data-ttu-id="ddc5f-144">Specificare il nome di dominio hello del tenant di Azure Active Directory B2C hello in **consentito Tenant**.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-144">Specify hello domain name of hello Azure Active Directory B2C tenant in **Allowed Tenant**.</span></span>

  ![Tenant consentito][api-management-howto-aad-b2c-allowed-tenant]

13. <span data-ttu-id="ddc5f-146">Specificare hello **criteri iscrizione** e **criteri Signin**.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-146">Specify hello **Signup Policy** and **Signin Policy**.</span></span> <span data-ttu-id="ddc5f-147">Facoltativamente, è anche possibile fornire hello **profilo criteri di modifica** e **criteri di reimpostazione Password**.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-147">Optionally, you can also provide hello **Profile Editing Policy** and **Password Reset Policy**.</span></span>

  ![Criteri][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > <span data-ttu-id="ddc5f-149">Per altre informazioni sui criteri, vedere [Azure Active Directory B2C: framework di criteri estendibile].</span><span class="sxs-lookup"><span data-stu-id="ddc5f-149">For more information on policies, see [Azure Active Directory B2C: Extensible policy framework].</span></span>

14. <span data-ttu-id="ddc5f-150">Dopo aver specificato la configurazione desiderata di hello, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-150">After you've specified hello desired configuration, click **Save**.</span></span>

  <span data-ttu-id="ddc5f-151">Dopo aver salvate le modifiche di hello, gli sviluppatori verranno toocreate in grado di nuovi account e accedere nel portale per sviluppatori toohello usando Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-151">After hello changes are saved, developers will be able toocreate new accounts and sign in toohello developer portal by using Azure Active Directory B2C.</span></span>

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a><span data-ttu-id="ddc5f-152">Eseguire l'iscrizione per un account per sviluppatore usando Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="ddc5f-152">Sign up for a developer account by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="ddc5f-153">toosign a un account sviluppatore utilizzando Active B2C Directory di Azure, aprire una nuova finestra del browser e passare il portale per sviluppatori di toohello.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-153">toosign up for a developer account by using Azure Active Directory B2C, open a new browser window and go toohello developer portal.</span></span> <span data-ttu-id="ddc5f-154">Fare clic su hello **iscriversi** pulsante.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-154">Click hello **Sign up** button.</span></span>

   ![Portale per sviluppatori 1][api-management-howto-aad-b2c-dev-portal]

2. <span data-ttu-id="ddc5f-156">Scegliere toosign con **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-156">Choose toosign up with **Azure Active Directory B2C**.</span></span>

   ![Portale per sviluppatori 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. <span data-ttu-id="ddc5f-158">Si è reindirizzato toohello iscrizione criteri configurato nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-158">You're redirected toohello signup policy that you configured in hello previous section.</span></span> <span data-ttu-id="ddc5f-159">Scegliere toosign utilizzando l'indirizzo di posta elettronica o uno degli account di social networking esistente.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-159">Choose toosign up by using your email address or one of your existing social accounts.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ddc5f-160">Se Azure Active Directory B2C hello unica opzione che è stato attivato hello **identità** scheda nel portale di pubblicazione hello, sarà reindirizzato toohello iscrizione criteri direttamente.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-160">If Azure Active Directory B2C is hello only option that's enabled on hello **Identities** tab in hello publisher portal, you'll be redirected toohello signup policy directly.</span></span>

   ![Portale per sviluppatori][api-management-howto-aad-b2c-dev-portal-b2c-options]

   <span data-ttu-id="ddc5f-162">Una volta completato hello iscrizione, si è portale per sviluppatori toohello indietro reindirizzato.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-162">When hello signup is complete, you're redirected back toohello developer portal.</span></span> <span data-ttu-id="ddc5f-163">È ora effettuata nel portale per sviluppatori toohello per l'istanza del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="ddc5f-163">You're now signed in toohello developer portal for your API Management service instance.</span></span>

    ![Registrazione completata][api-management-registration-complete]

## <a name="next-steps"></a><span data-ttu-id="ddc5f-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ddc5f-165">Next steps</span></span>

*  <span data-ttu-id="ddc5f-166">[panoramica di Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="ddc5f-166">[Azure Active Directory B2C overview]</span></span>
*  <span data-ttu-id="ddc5f-167">[Azure Active Directory B2C: framework di criteri estendibile]</span><span class="sxs-lookup"><span data-stu-id="ddc5f-167">[Azure Active Directory B2C: Extensible policy framework]</span></span>
*  <span data-ttu-id="ddc5f-168">[Usare un account Microsoft come provider di identità in Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="ddc5f-168">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="ddc5f-169">[Usare un account Google come provider di identità in Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="ddc5f-169">[Use a Google account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="ddc5f-170">[Usare un account LinkedIn come provider di identità in Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="ddc5f-170">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="ddc5f-171">[Usare un account Facebook come provider di identità in Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="ddc5f-171">[Use a Facebook account as an identity provider in Azure Active Directory B2C]</span></span>




[api-management-howto-aad-b2c-security-tab]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab.PNG
[api-management-howto-aad-b2c-security-tab-reply-url]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab-reply-url.PNG
[api-management-howto-aad-b2c-portal-menu]: ./media/api-management-howto-aad-b2c/api-management-b2c-portal-menu.PNG
[api-management-howto-aad-b2c-add-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-add-button.PNG
[api-management-howto-aad-b2c-app-details]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-details.PNG
[api-management-howto-aad-b2c-app-created]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-created.PNG
[api-management-howto-aad-b2c-app-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-id.PNG
[api-management-howto-aad-b2c-client-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-id.PNG
[api-management-howto-aad-b2c-app-key]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key.PNG
[api-management-howto-aad-b2c-app-key-saved]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key-saved.PNG
[api-management-howto-aad-b2c-client-secret]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-secret.PNG
[api-management-howto-aad-b2c-allowed-tenant]: ./media/api-management-howto-aad-b2c/api-management-b2c-allowed-tenant.PNG
[api-management-howto-aad-b2c-policies]: ./media/api-management-howto-aad-b2c/api-management-b2c-policies.PNG
[api-management-howto-aad-b2c-dev-portal]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-button.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-options]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-options.PNG
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.PNG
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-b2c-security-tab.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing hello Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph
[panoramica di Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview
[modalità sviluppatore tooauthorize degli account con Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad
[Azure Active Directory B2C: framework di criteri estendibile]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies
[Usare un account Microsoft come provider di identità in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app
[Usare un account Google come provider di identità in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app
[Usare un account Facebook come provider di identità in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app
[Usare un account LinkedIn come provider di identità in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account
