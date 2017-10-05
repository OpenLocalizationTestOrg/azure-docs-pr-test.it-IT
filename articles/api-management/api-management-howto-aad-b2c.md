---
title: Autorizzare gli account per sviluppatore usando Azure Active Directory B2C - Gestione API di Azure | Documentazione Microsoft
description: Informazioni su come autorizzare gli utenti usando Azure Active Directory B2C in Gestione API.
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
ms.openlocfilehash: eb7deb1a79d9db9ac5cfbea69b8d3c564eb55577
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-authorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a><span data-ttu-id="71772-103">Come autorizzare gli account per sviluppatore usando Azure Active Directory B2C in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="71772-103">How to authorize developer accounts by using Azure Active Directory B2C in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="71772-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="71772-104">Overview</span></span>
<span data-ttu-id="71772-105">Azure Active Directory B2C è una soluzione di gestione delle identità cloud per applicazioni per dispositivi mobili e Web rivolte agli utenti.</span><span class="sxs-lookup"><span data-stu-id="71772-105">Azure Active Directory B2C is a cloud identity management solution for consumer-facing web and mobile applications.</span></span> <span data-ttu-id="71772-106">Può essere usato per gestire l'accesso a un portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="71772-106">You can use it to manage access to your developer portal.</span></span> <span data-ttu-id="71772-107">Questa guida illustra la configurazione necessaria nel servizio Gestione API per l'integrazione con Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="71772-107">This guide shows you the configuration that's required in your API Management service to integrate with Azure Active Directory B2C.</span></span> <span data-ttu-id="71772-108">Per informazioni su come abilitare l'accesso al portale per sviluppatori con la versione classica di Azure Active Directory, vedere [Come autorizzare gli account per sviluppatore usando Azure Active Directory].</span><span class="sxs-lookup"><span data-stu-id="71772-108">For information about enabling access to the developer portal by using classic Azure Active Directory, see [How to authorize developer accounts using Azure Active Directory].</span></span>

> [!NOTE]
> <span data-ttu-id="71772-109">Per completare i passaggi di questa guida, è necessario un tenant di Azure Active Directory B2C in cui creare un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="71772-109">To complete the steps in this guide, you must first have an Azure Active Directory B2C tenant to create an application in.</span></span> <span data-ttu-id="71772-110">È necessario anche che siano pronti i criteri di iscrizione e accesso.</span><span class="sxs-lookup"><span data-stu-id="71772-110">Also, you need to have signup and signin policies ready.</span></span> <span data-ttu-id="71772-111">Per altre informazioni, vedere la [panoramica di Azure Active Directory B2C].</span><span class="sxs-lookup"><span data-stu-id="71772-111">For more information, see [Azure Active Directory B2C overview].</span></span>

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a><span data-ttu-id="71772-112">Autorizzare gli account per sviluppatore usando Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="71772-112">Authorize developer accounts by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="71772-113">Per iniziare, fare clic su **Portale di pubblicazione** nel portale di Azure per il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="71772-113">To get started, click **Publisher portal** in the Azure portal for your API Management service.</span></span> <span data-ttu-id="71772-114">Verrà visualizzato il portale di pubblicazione di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="71772-114">This takes you to the API Management publisher portal.</span></span>

   ![Portale di pubblicazione][api-management-management-console]

   > [!NOTE]
   > <span data-ttu-id="71772-116">Se non è stata ancora creata un'istanza del servizio Gestione API, vedere [Creare un'istanza del servizio Gestione API][Create an API Management service instance] nell'esercitazione [Introduzione a Gestione API di Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="71772-116">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management tutorial][Get started with Azure API Management].</span></span>

2. <span data-ttu-id="71772-117">Fare clic su **Sicurezza** nel menu **Gestione API**.</span><span class="sxs-lookup"><span data-stu-id="71772-117">On the **API Management** menu, click **Security**.</span></span> <span data-ttu-id="71772-118">Nella scheda **Identità** scegliere **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="71772-118">On the **Identities** tab, choose **Azure Active Directory B2C**.</span></span>

  ![Identità esterne 1][api-management-howto-aad-b2c-security-tab]

3. <span data-ttu-id="71772-120">Prendere nota dell'**URL di reindirizzamento** e passare ad Azure Active Directory B2C nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="71772-120">Make a note of the **Redirect URL** and switch over to Azure Active Directory B2C in the Azure portal.</span></span>

  ![Identità esterne 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. <span data-ttu-id="71772-122">Fare clic sul pulsante **Applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="71772-122">Click the **Applications** button.</span></span>

  ![Registrare una nuova applicazione 1][api-management-howto-aad-b2c-portal-menu]

5. <span data-ttu-id="71772-124">Fare clic sul pulsante **Aggiungi** per creare una nuova applicazione Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="71772-124">Click the **Add** button to create a new Azure Active Directory B2C application.</span></span>

  ![Registrare una nuova applicazione 2][api-management-howto-aad-b2c-add-button]

6. <span data-ttu-id="71772-126">Nel pannello **Nuova applicazione** immettere un nome per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="71772-126">In the **New application** blade, enter a name for the application.</span></span> <span data-ttu-id="71772-127">Scegliere **Sì** in **App Web/API Web** e quindi **Sì** in **Consenti flusso implicito**.</span><span class="sxs-lookup"><span data-stu-id="71772-127">Choose **Yes** under **Web App/Web API**, and choose **Yes** under **Allow implicit flow**.</span></span> <span data-ttu-id="71772-128">Copiare quindi l'**URL di reindirizzamento** dalla sezione **Azure Active Directory B2C** della scheda **Identità** del portale di pubblicazione e incollarlo nella casella di testo **URL di risposta**.</span><span class="sxs-lookup"><span data-stu-id="71772-128">Then copy the **Redirect URL** from the **Azure Active Directory B2C** section of the **Identities** tab in the publisher portal, and paste it into the **Reply URL** text box.</span></span>

  ![Registrare una nuova applicazione 3][api-management-howto-aad-b2c-app-details]

7. <span data-ttu-id="71772-130">Selezionare il pulsante **Create** .</span><span class="sxs-lookup"><span data-stu-id="71772-130">Click the **Create** button.</span></span> <span data-ttu-id="71772-131">Dopo che è stata creata, l'applicazione viene visualizzata nel pannello **Applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="71772-131">When the application is created, it appears in the **Applications** blade.</span></span> <span data-ttu-id="71772-132">Fare clic sul nome dell'applicazione per visualizzarne i dettagli.</span><span class="sxs-lookup"><span data-stu-id="71772-132">Click the application name to see its details.</span></span>

  ![Registrare una nuova applicazione 4][api-management-howto-aad-b2c-app-created]

8. <span data-ttu-id="71772-134">Dal pannello **Proprietà** copiare l'**ID applicazione** negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="71772-134">From the **Properties** blade, copy the **Application ID** to the clipboard.</span></span>

  ![ID applicazione 1][api-management-howto-aad-b2c-app-id]

9. <span data-ttu-id="71772-136">Tornare al portale di pubblicazione e incollare l'ID nella casella di testo **ID client**.</span><span class="sxs-lookup"><span data-stu-id="71772-136">Switch back to the publisher portal and paste the ID into the **Client Id** text box.</span></span>

  ![ID applicazione 2][api-management-howto-aad-b2c-client-id]

10. <span data-ttu-id="71772-138">Tornare al portale di Azure, fare clic sul pulsante **Chiavi** e quindi su **Genera chiave**.</span><span class="sxs-lookup"><span data-stu-id="71772-138">Switch back to the Azure portal, click the **Keys** button, and then click **Generate key**.</span></span> <span data-ttu-id="71772-139">Fare clic su **Salva** per salvare la configurazione e visualizzare la **chiave dell'app**.</span><span class="sxs-lookup"><span data-stu-id="71772-139">Click **Save** to save the configuration and display the **App key**.</span></span> <span data-ttu-id="71772-140">Copiare la chiave negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="71772-140">Copy the key to the clipboard.</span></span>

  ![Chiave dell'app 1][api-management-howto-aad-b2c-app-key]

11. <span data-ttu-id="71772-142">Tornare al portale di pubblicazione e incollare la chiave nella casella di testo **Segreto client** .</span><span class="sxs-lookup"><span data-stu-id="71772-142">Switch back to the publisher portal and paste the key into the **Client Secret** text box.</span></span>

  ![Chiave dell'app 2][api-management-howto-aad-b2c-client-secret]

12. <span data-ttu-id="71772-144">Specificare il nome di dominio del tenant di Azure Active Directory B2C nel campo **Tenant consentito**.</span><span class="sxs-lookup"><span data-stu-id="71772-144">Specify the domain name of the Azure Active Directory B2C tenant in **Allowed Tenant**.</span></span>

  ![Tenant consentito][api-management-howto-aad-b2c-allowed-tenant]

13. <span data-ttu-id="71772-146">Specificare **Criterio di iscrizione** e **Criterio di accesso**.</span><span class="sxs-lookup"><span data-stu-id="71772-146">Specify the **Signup Policy** and **Signin Policy**.</span></span> <span data-ttu-id="71772-147">Facoltativamente è possibile specificare anche **Criteri di modifica del profilo** e **Criteri di reimpostazione password**.</span><span class="sxs-lookup"><span data-stu-id="71772-147">Optionally, you can also provide the **Profile Editing Policy** and **Password Reset Policy**.</span></span>

  ![Criteri][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > <span data-ttu-id="71772-149">Per altre informazioni sui criteri, vedere [Azure Active Directory B2C: framework di criteri estendibile].</span><span class="sxs-lookup"><span data-stu-id="71772-149">For more information on policies, see [Azure Active Directory B2C: Extensible policy framework].</span></span>

14. <span data-ttu-id="71772-150">Dopo avere specificato la configurazione desiderata, fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="71772-150">After you've specified the desired configuration, click **Save**.</span></span>

  <span data-ttu-id="71772-151">Dopo il salvataggio delle modifiche, gli sviluppatori potranno creare nuovi account e accedere al portale per sviluppatori con Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="71772-151">After the changes are saved, developers will be able to create new accounts and sign in to the developer portal by using Azure Active Directory B2C.</span></span>

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a><span data-ttu-id="71772-152">Eseguire l'iscrizione per un account per sviluppatore usando Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="71772-152">Sign up for a developer account by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="71772-153">Per eseguire l'iscrizione per un account per sviluppatore usando Azure Active Directory B2C, aprire una nuova finestra del browser e andare al portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="71772-153">To sign up for a developer account by using Azure Active Directory B2C, open a new browser window and go to the developer portal.</span></span> <span data-ttu-id="71772-154">Fare clic sul pulsante **Iscriviti**.</span><span class="sxs-lookup"><span data-stu-id="71772-154">Click the **Sign up** button.</span></span>

   ![Portale per sviluppatori 1][api-management-howto-aad-b2c-dev-portal]

2. <span data-ttu-id="71772-156">Scegliere quindi di iscriversi con **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="71772-156">Choose to sign up with **Azure Active Directory B2C**.</span></span>

   ![Portale per sviluppatori 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. <span data-ttu-id="71772-158">Si verrà reindirizzati ai criteri di iscrizione configurati nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="71772-158">You're redirected to the signup policy that you configured in the previous section.</span></span> <span data-ttu-id="71772-159">Scegliere di eseguire l'iscrizione usando l'indirizzo di posta elettronica o uno degli account di social networking esistenti.</span><span class="sxs-lookup"><span data-stu-id="71772-159">Choose to sign up by using your email address or one of your existing social accounts.</span></span>

   > [!NOTE]
   > <span data-ttu-id="71772-160">Se Azure Active Directory B2C è l'unica opzione abilitata nella scheda **Identità** del portale di pubblicazione, si verrà reindirizzati direttamente ai criteri di iscrizione.</span><span class="sxs-lookup"><span data-stu-id="71772-160">If Azure Active Directory B2C is the only option that's enabled on the **Identities** tab in the publisher portal, you'll be redirected to the signup policy directly.</span></span>

   ![Portale per sviluppatori][api-management-howto-aad-b2c-dev-portal-b2c-options]

   <span data-ttu-id="71772-162">Al termine dell'iscrizione si verrà reindirizzati al portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="71772-162">When the signup is complete, you're redirected back to the developer portal.</span></span> <span data-ttu-id="71772-163">Si è ora connessi al portale per sviluppatori per l'istanza del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="71772-163">You're now signed in to the developer portal for your API Management service instance.</span></span>

    ![Registrazione completata][api-management-registration-complete]

## <a name="next-steps"></a><span data-ttu-id="71772-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="71772-165">Next steps</span></span>

*  <span data-ttu-id="71772-166">[panoramica di Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="71772-166">[Azure Active Directory B2C overview]</span></span>
*  <span data-ttu-id="71772-167">[Azure Active Directory B2C: framework di criteri estendibile]</span><span class="sxs-lookup"><span data-stu-id="71772-167">[Azure Active Directory B2C: Extensible policy framework]</span></span>
*  <span data-ttu-id="71772-168">[Usare un account Microsoft come provider di identità in Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="71772-168">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="71772-169">[Usare un account Google come provider di identità in Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="71772-169">[Use a Google account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="71772-170">[Usare un account LinkedIn come provider di identità in Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="71772-170">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="71772-171">[Usare un account Facebook come provider di identità in Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="71772-171">[Use a Facebook account as an identity provider in Azure Active Directory B2C]</span></span>




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

[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing the Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph
<span data-ttu-id="71772-172">[panoramica di Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview</span><span class="sxs-lookup"><span data-stu-id="71772-172">[Azure Active Directory B2C overview]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview</span></span>
<span data-ttu-id="71772-173">[Come autorizzare gli account per sviluppatore usando Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad</span><span class="sxs-lookup"><span data-stu-id="71772-173">[How to authorize developer accounts using Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad</span></span>
<span data-ttu-id="71772-174">[Azure Active Directory B2C: framework di criteri estendibile]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies</span><span class="sxs-lookup"><span data-stu-id="71772-174">[Azure Active Directory B2C: Extensible policy framework]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies</span></span>
<span data-ttu-id="71772-175">[Usare un account Microsoft come provider di identità in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app</span><span class="sxs-lookup"><span data-stu-id="71772-175">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app</span></span>
<span data-ttu-id="71772-176">[Usare un account Google come provider di identità in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app</span><span class="sxs-lookup"><span data-stu-id="71772-176">[Use a Google account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app</span></span>
<span data-ttu-id="71772-177">[Usare un account Facebook come provider di identità in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app</span><span class="sxs-lookup"><span data-stu-id="71772-177">[Use a Facebook account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app</span></span>
<span data-ttu-id="71772-178">[Usare un account LinkedIn come provider di identità in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app</span><span class="sxs-lookup"><span data-stu-id="71772-178">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app</span></span>

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

[Log in to the Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account
