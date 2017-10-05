---
title: Autorizzare gli account per sviluppatori usando Azure Active Directory - Gestione API di Azure | Documentazione Microsoft
description: Informazioni su come autorizzare gli utenti usando Azure Active Directory in Gestione API.
services: api-management
documentationcenter: API Management
author: steved0x
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
ms.openlocfilehash: 7637e6419d17a2d75904fbe63df5f27d4be4bbe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-authorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a><span data-ttu-id="46b1c-103">Come autorizzare gli account per sviluppatori usando Azure Active Directory in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="46b1c-103">How to authorize developer accounts using Azure Active Directory in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="46b1c-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="46b1c-104">Overview</span></span>
<span data-ttu-id="46b1c-105">Questa guida illustra come abilitare l'accesso al portale per sviluppatori per gli utenti da Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="46b1c-105">This guide shows you how to enable access to the developer portal for users from Azure Active Directory.</span></span> <span data-ttu-id="46b1c-106">Questa guida illustra anche come gestire gruppi di utenti di Azure Active Directory aggiungendo gruppi esterni contenenti gli utenti di una directory di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="46b1c-106">This guide also shows you how to manage groups of Azure Active Directory users by adding external groups that contain the users of an Azure Active Directory.</span></span>

> <span data-ttu-id="46b1c-107">Per completare i passaggi di questa guida, è necessaria una directory di Azure Active Directory in cui creare un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="46b1c-107">To complete the steps in this guide you must first have an Azure Active Directory in which to create an application.</span></span>
> 
> 

## <a name="how-to-authorize-developer-accounts-using-azure-active-directory"></a><span data-ttu-id="46b1c-108">Come autorizzare gli account per sviluppatori usando Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="46b1c-108">How to authorize developer accounts using Azure Active Directory</span></span>
<span data-ttu-id="46b1c-109">Per iniziare, fare clic su **Portale di pubblicazione** nel portale di Azure relativo al servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="46b1c-109">To get started, click **Publisher portal** in the Azure portal for your API Management service.</span></span> <span data-ttu-id="46b1c-110">Verrà visualizzato il portale di pubblicazione di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="46b1c-110">This takes you to the API Management publisher portal.</span></span>

![Portale di pubblicazione][api-management-management-console]

> <span data-ttu-id="46b1c-112">Se non è stata creata un'istanza del servizio Gestione API, vedere [Creare un'istanza di Gestione API][Create an API Management service instance] nell'esercitazione [Introduzione a Gestione API di Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="46b1c-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="46b1c-113">Fare clic su **Security** (Sicurezza) nel menu **API Management** (Gestione API) a sinistra e quindi su **External Identities** (Identità esterne).</span><span class="sxs-lookup"><span data-stu-id="46b1c-113">Click **Security** from the **API Management** menu on the left and click **External Identities**.</span></span>

![Identità esterne][api-management-security-external-identities]

<span data-ttu-id="46b1c-115">Fare clic su **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46b1c-115">Click **Azure Active Directory**.</span></span> <span data-ttu-id="46b1c-116">Prendere nota dell' **URL di reindirizzamento** e passare alla directory di Azure Active Directory nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="46b1c-116">Make a note of the **Redirect URL** and switch over to your Azure Active Directory in the Azure Classic Portal.</span></span>

![Identità esterne][api-management-security-aad-new]

<span data-ttu-id="46b1c-118">Fare clic sul pulsante **Aggiungi** per creare una nuova applicazione Azure Active Directory e scegliere **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.</span><span class="sxs-lookup"><span data-stu-id="46b1c-118">Click the **Add** button to create a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Aggiungere una nuova applicazione Azure Active Directory][api-management-new-aad-application-menu]

<span data-ttu-id="46b1c-120">Immettere un nome per l'applicazione, selezionare **Applicazione Web e/o API Web**, quindi fare clic sul pulsante Avanti.</span><span class="sxs-lookup"><span data-stu-id="46b1c-120">Enter a name for the application, select **Web application and/or Web API**, and click the next button.</span></span>

![Nuova applicazione Azure Active Directory][api-management-new-aad-application-1]

<span data-ttu-id="46b1c-122">In **URL accesso**immettere l'URL di accesso del portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="46b1c-122">For **Sign-on URL**, enter the sign-on URL of your developer portal.</span></span> <span data-ttu-id="46b1c-123">In questo esempio, il valore di **URL accesso** è `https://aad03.portal.current.int-azure-api.net/signin`.</span><span class="sxs-lookup"><span data-stu-id="46b1c-123">In this example, the **Sign-on URL** is `https://aad03.portal.current.int-azure-api.net/signin`.</span></span> 

<span data-ttu-id="46b1c-124">In **URL ID app**immettere il dominio predefinito un dominio personalizzato per Azure Active Directory e aggiungervi una stringa univoca.</span><span class="sxs-lookup"><span data-stu-id="46b1c-124">For the **App ID URL**, enter either the default domain or a custom domain for the Azure Active Directory, and append a unique string to it.</span></span> <span data-ttu-id="46b1c-125">In questo esempio, il dominio predefinito di **https://contoso5api.onmicrosoft.com** viene usato con il suffisso **/api** specificato.</span><span class="sxs-lookup"><span data-stu-id="46b1c-125">In this example, the default domain of **https://contoso5api.onmicrosoft.com** is used with the suffix of **/api** specified.</span></span>

![Proprietà della nuova applicazione Azure Active Directory][api-management-new-aad-application-2]

<span data-ttu-id="46b1c-127">Fare clic sul pulsante con il segno di spunta per salvare e creare l'applicazione e passare alla scheda **Configura** per configurare la nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="46b1c-127">Click the check button to save and create the application, and switch to the **Configure** tab to configure the new application.</span></span>

![Nuova applicazione Azure Active Directory creata][api-management-new-aad-app-created]

<span data-ttu-id="46b1c-129">Se per questa applicazione verranno usate più directory di Azure Active Directory, fare clic su **Sì** per **L'applicazione è multi-tenant**.</span><span class="sxs-lookup"><span data-stu-id="46b1c-129">If multiple Azure Active Directories are going to be used for this application, click **Yes** for **Application is multi-tenant**.</span></span> <span data-ttu-id="46b1c-130">Il valore predefinito è **No**.</span><span class="sxs-lookup"><span data-stu-id="46b1c-130">The default is **No**.</span></span>

![L'applicazione è multi-tenant][api-management-aad-app-multi-tenant]

<span data-ttu-id="46b1c-132">Copiare l'**URL di reindirizzamento** dalla sezione **Azure Active Directory** della scheda **External Identities** (Identità esterne) del portale di pubblicazione e incollarlo nella casella di testo **URL di risposta**.</span><span class="sxs-lookup"><span data-stu-id="46b1c-132">Copy the **Redirect URL** from the **Azure Active Directory** section of the **External Identities** tab in the publisher portal and paste it into the **Reply URL** text box.</span></span> 

![URL di risposta][api-management-aad-reply-url]

<span data-ttu-id="46b1c-134">Scorrere fino alla parte inferiore della scheda Configura e selezionare l'elenco a discesa **Autorizzazioni applicazione** e quindi **Lettura dati directory**.</span><span class="sxs-lookup"><span data-stu-id="46b1c-134">Scroll to the bottom of the configure tab, select the **Application Permissions** drop-down, and check **Read directory data**.</span></span>

![Autorizzazioni applicazione][api-management-aad-app-permissions]

<span data-ttu-id="46b1c-136">Selezionare l'elenco a discesa **Autorizzazioni delegate** e quindi **Abilita l'accesso e la lettura del profilo utente**.</span><span class="sxs-lookup"><span data-stu-id="46b1c-136">Select the **Delegate Permissions** drop-down, and check **Enable sign-on and read users' profiles**.</span></span>

![Autorizzazioni delegate][api-management-aad-delegated-permissions]

> <span data-ttu-id="46b1c-138">Per altre informazioni sulle autorizzazioni applicazione e delegate, vedere [Accesso all'API Graph][Accessing the Graph API].</span><span class="sxs-lookup"><span data-stu-id="46b1c-138">For more information about application and delegated permissions, see [Accessing the Graph API][Accessing the Graph API].</span></span>
> 
> 

<span data-ttu-id="46b1c-139">Copiare l' **ID client** negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="46b1c-139">Copy the **Client Id** to the clipboard.</span></span>

![ID client][api-management-aad-app-client-id]

<span data-ttu-id="46b1c-141">Tornare al portale di pubblicazione e incollare l' **ID client** copiato dalla configurazione dell'applicazione di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="46b1c-141">Switch back to the publisher portal and paste in the **Client Id** copied from the Azure Active Directory application configuration.</span></span>

![Client Id][api-management-client-id]

<span data-ttu-id="46b1c-143">Tornare alla configurazione di Azure Active Directory e fare clic sull'elenco a discesa **Seleziona durata** nella sezione **Chiavi** e specificare un intervallo.</span><span class="sxs-lookup"><span data-stu-id="46b1c-143">Switch back to the Azure Active Directory configuration, and click the **Select duration** drop-down in the **Keys** section and specify an interval.</span></span> <span data-ttu-id="46b1c-144">In questo esempio viene usato **1 anno** .</span><span class="sxs-lookup"><span data-stu-id="46b1c-144">In this example, **1 year** is used.</span></span>

![Chiave][api-management-aad-key-before-save]

<span data-ttu-id="46b1c-146">Fare clic su **Salva** per salvare la configurazione e visualizzare la chiave.</span><span class="sxs-lookup"><span data-stu-id="46b1c-146">Click **Save** to save the configuration and display the key.</span></span> <span data-ttu-id="46b1c-147">Copiare la chiave negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="46b1c-147">Copy the key to the clipboard.</span></span>

> <span data-ttu-id="46b1c-148">Annotare il valore relativo alla chiave.</span><span class="sxs-lookup"><span data-stu-id="46b1c-148">Make a note of this key.</span></span> <span data-ttu-id="46b1c-149">Una volta chiusa la finestra di configurazione di Azure Active Directory, la chiave non potrà più essere visualizzata.</span><span class="sxs-lookup"><span data-stu-id="46b1c-149">Once you close the Azure Active Directory configuration window, the key cannot be displayed again.</span></span>
> 
> 

![Chiave][api-management-aad-key-after-save]

<span data-ttu-id="46b1c-151">Tornare al portale di pubblicazione e incollare la chiave nella casella di testo **Segreto client** .</span><span class="sxs-lookup"><span data-stu-id="46b1c-151">Switch back to the publisher portal and paste the key into the **Client Secret** text box.</span></span>

![Segreto client][api-management-client-secret]

<span data-ttu-id="46b1c-153">**Tenant consentiti** specifica le directory che hanno accesso alle API dell'istanza del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="46b1c-153">**Allowed Tenants** specifies which directories have access to the APIs of the API Management service instance.</span></span> <span data-ttu-id="46b1c-154">Specificare i domini delle istanze di Azure Active Directory a cui si vuole concedere l'accesso.</span><span class="sxs-lookup"><span data-stu-id="46b1c-154">Specify the domains of the Azure Active Directory instances to which you want to grant access.</span></span> <span data-ttu-id="46b1c-155">È possibile separare più domini con virgole, spazi o caratteri di nuova riga.</span><span class="sxs-lookup"><span data-stu-id="46b1c-155">You can separate multiple domains with newlines, spaces, or commas.</span></span>

![Tenant consentiti][api-management-client-allowed-tenants]


<span data-ttu-id="46b1c-157">Una volta specificata la configurazione desiderata, fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="46b1c-157">Once the desired configuration is specified, click **Save**.</span></span>

![Salva][api-management-client-allowed-tenants-save]

<span data-ttu-id="46b1c-159">Al termine del salvataggio delle modifiche, gli utenti nell'istanza di Azure Active Directory specificata possono accedere al portale per sviluppatori seguendo i passaggi in [Accedere al portale per sviluppatori con un account Azure Active Directory][Log in to the Developer portal using an Azure Active Directory account].</span><span class="sxs-lookup"><span data-stu-id="46b1c-159">Once the changes are saved, the users in the specified Azure Active Directory can sign in to the Developer portal by following the steps in [Log in to the Developer portal using an Azure Active Directory account][Log in to the Developer portal using an Azure Active Directory account].</span></span>

<span data-ttu-id="46b1c-160">Nella sezione **Tenant consentiti** si possono specificare più domini.</span><span class="sxs-lookup"><span data-stu-id="46b1c-160">Multiple domains can be specified in the **Allowed Tenants** section.</span></span> <span data-ttu-id="46b1c-161">Per consentire a un utente di accedere da un dominio diverso da quello originale in cui è stata registrata l'applicazione, un amministratore globale dell'altro dominio deve concedere l'autorizzazione che permette all'applicazione di accedere ai dati della directory.</span><span class="sxs-lookup"><span data-stu-id="46b1c-161">Before any user can log in from a different domain than the original domain where the application was registered, a global administrator of the different domain must grant permission for the application to access directory data.</span></span> <span data-ttu-id="46b1c-162">Per concedere l'autorizzazione, l'amministratore globale deve accedere all'`https://<URL of your developer portal>/aadadminconsent`, ad esempio https://contoso.portal.azure-api.net/aadadminconsent, digitare il nome di dominio del tenant di Active Directory a cui consentire l'accesso e fare clic su Invia.</span><span class="sxs-lookup"><span data-stu-id="46b1c-162">To grant permission, the global administrator should go to `https://<URL of your developer portal>/aadadminconsent` (for example, https://contoso.portal.azure-api.net/aadadminconsent), type in the domain name of the Active Directory tenant they want to give access to and click Submit.</span></span> <span data-ttu-id="46b1c-163">Nell'esempio seguente, un amministratore globale di `miaoaad.onmicrosoft.com` tenta di concedere l'autorizzazione a questo portale per sviluppatori specifico.</span><span class="sxs-lookup"><span data-stu-id="46b1c-163">In the following example, a global administrator from `miaoaad.onmicrosoft.com` is trying to give permission to this particular developer portal.</span></span> 

![autorizzazioni][api-management-aad-consent]

<span data-ttu-id="46b1c-165">Nella schermata successiva all'amministratore globale verrà richiesto di confermare l'autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="46b1c-165">In the next screen, the global administrator will be prompted to confirm giving the permission.</span></span> 

![autorizzazioni][api-management-permissions-form]

> <span data-ttu-id="46b1c-167">Se un amministratore non globale cerca di accedere prima che vengano concesse le autorizzazioni da un amministratore globale, il tentativo di accesso non riesce e viene visualizzata una schermata di errore.</span><span class="sxs-lookup"><span data-stu-id="46b1c-167">If a non-global administrator tries to log in before permissions are granted by a global administrator, the login attempt fails and an error screen is displayed.</span></span>
> 
> 

## <a name="how-to-add-an-external-azure-active-directory-group"></a><span data-ttu-id="46b1c-168">Come aggiungere un gruppo di Azure Active Directory esterno</span><span class="sxs-lookup"><span data-stu-id="46b1c-168">How to add an external Azure Active Directory Group</span></span>
<span data-ttu-id="46b1c-169">Dopo avere abilitato l'accesso per gli utenti in Azure Active Directory, è possibile aggiungere gruppi di Azure Active Directory in Gestione API per gestire più facilmente l'associazione degli sviluppatori del gruppo ai prodotti desiderati.</span><span class="sxs-lookup"><span data-stu-id="46b1c-169">After enabling access for users in an Azure Active Directory, you can add Azure Active Directory groups into API Management to more easily manage the association of the developers in the group with the desired products.</span></span>

> <span data-ttu-id="46b1c-170">Prima di configurare un gruppo esterno di Azure Active Directory, è necessario configurare Azure Active Directory nella scheda Identità seguendo la procedura della sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="46b1c-170">To configure an external Azure Active Directory group, the Azure Active Directory must first be configured in the Identities tab by following the procedure in the previous section.</span></span> 
> 
> 

<span data-ttu-id="46b1c-171">I gruppi esterni di Azure Active Directory vengono aggiunti dalla scheda **Visibilità** del prodotto per cui si desidera concedere l'accesso al gruppo.</span><span class="sxs-lookup"><span data-stu-id="46b1c-171">External Azure Active Directory groups are added from the **Visibility** tab of the product for which you wish to grant access to the group.</span></span> <span data-ttu-id="46b1c-172">Fare clic su **Prodotti**e quindi fare clic sul nome del prodotto desiderato.</span><span class="sxs-lookup"><span data-stu-id="46b1c-172">Click **Products**, and then click the name of the desired product.</span></span>

![Configure product][api-management-configure-product]

<span data-ttu-id="46b1c-174">Passare alla scheda **Visibility** (Visibilità) e fare clic su **Add Groups from Azure Active Directory** (Aggiungi gruppi da Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="46b1c-174">Switch to the **Visibility** tab, and click **Add Groups from Azure Active Directory**.</span></span>

![Aggiungere i gruppi][api-management-add-groups]

<span data-ttu-id="46b1c-176">Selezionare il **tenant di Azure Active Directory** nell'elenco a discesa e quindi digitare il nome del gruppo desiderato nella casella di testo **Groups to be added** (Gruppi da aggiungere).</span><span class="sxs-lookup"><span data-stu-id="46b1c-176">Select the **Azure Active Directory Tenant** from the drop-down list, and then type the name of the desired group in the **Groups** to be added text box.</span></span>

![Selezionare un gruppo][api-management-select-group]

<span data-ttu-id="46b1c-178">Questo nome di gruppo è presente nell'elenco **Gruppi** di Azure Active Directory, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="46b1c-178">This group name can be found in the **Groups** list for your Azure Active Directory, as shown in the following example.</span></span>

![Elenco di gruppi di Azure Active Directory][api-management-aad-groups-list]

<span data-ttu-id="46b1c-180">Fare clic su **Aggiungi** per convalidare il nome del gruppo e aggiungere il gruppo.</span><span class="sxs-lookup"><span data-stu-id="46b1c-180">Click **Add** to validate the group name and add the group.</span></span> <span data-ttu-id="46b1c-181">In questo esempio viene aggiunto il gruppo esterno **Contoso 5 Developers** .</span><span class="sxs-lookup"><span data-stu-id="46b1c-181">In this example, the **Contoso 5 Developers** external group is added.</span></span> 

![Gruppo aggiunto][api-management-aad-group-added]

<span data-ttu-id="46b1c-183">Fare clic su **Salva** per salvare la nuova selezione di gruppi.</span><span class="sxs-lookup"><span data-stu-id="46b1c-183">Click **Save** to save the new group selection.</span></span>

<span data-ttu-id="46b1c-184">Una volta che un gruppo di Azure Active Directory è stato configurato da un prodotto, può essere selezionato nella scheda **Visibilità** di altri prodotti nell'istanza del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="46b1c-184">Once an Azure Active Directory group has been configured from one product, it is available to be checked on the **Visibility** tab for the other products in the API Management service instance.</span></span>

<span data-ttu-id="46b1c-185">Per rivedere e configurare le proprietà per i gruppi esterni dopo che sono stati aggiunti, fare clic sul nome del gruppo nella scheda **Gruppi**.</span><span class="sxs-lookup"><span data-stu-id="46b1c-185">To review and configure the properties for external groups once they have been added, click the name of the group from the **Groups** tab.</span></span>

![Gestire i gruppi][api-management-groups]

<span data-ttu-id="46b1c-187">Da qui è possibile modificare il **nome** e la **descrizione** del gruppo.</span><span class="sxs-lookup"><span data-stu-id="46b1c-187">From here you can edit the **Name** and the **Description** of the group.</span></span>

![Modificare un gruppo][api-management-edit-group]

<span data-ttu-id="46b1c-189">Gli utenti dell'istanza di Azure Active Directory configurata possono accedere al portale per sviluppatori e visualizzare e sottoscrivere qualsiasi gruppo su cui hanno visibilità, seguendo le istruzioni della sezione seguente.</span><span class="sxs-lookup"><span data-stu-id="46b1c-189">Users from the configured Azure Active Directory can sign in to the Developer portal and view and subscribe to any groups for which they have visibility by following the instructions in the following section.</span></span>

## <a name="how-to-log-in-to-the-developer-portal-using-an-azure-active-directory-account"></a><span data-ttu-id="46b1c-190">Come accedere al portale per sviluppatori con un account Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="46b1c-190">How to log in to the Developer portal using an Azure Active Directory account</span></span>
<span data-ttu-id="46b1c-191">Per accedere al portale per sviluppatori con un account Azure Active Directory configurato nelle sezioni precedenti, aprire una nuova finestra del browser con l'**URL accesso** della configurazione dell'applicazione Active Directory e fare clic su **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46b1c-191">To log into the Developer portal using an Azure Active Directory account configured in the previous sections, open a new browser window using the **Sign-on URL** from the Active Directory application configuration, and click **Azure Active Directory**.</span></span>

![Portale per sviluppatori][api-management-dev-portal-signin]

<span data-ttu-id="46b1c-193">Immettere le credenziali di uno degli utenti in Azure Active Directory e fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="46b1c-193">Enter the credentials of one of the users in your Azure Active Directory, and click **Sign in**.</span></span>

![Accedi][api-management-aad-signin]

<span data-ttu-id="46b1c-195">È possibile che venga richiesto di compilare un modulo di registrazione se sono necessarie altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="46b1c-195">You may be prompted with a registration form if any additional information is required.</span></span> <span data-ttu-id="46b1c-196">Compilare il modulo di registrazione e fare clic su **Iscrizione**.</span><span class="sxs-lookup"><span data-stu-id="46b1c-196">Complete the registration form and click **Sign up**.</span></span>

![Registrazione][api-management-complete-registration]

<span data-ttu-id="46b1c-198">L'utente ora è connesso al portale per sviluppatori per l'istanza del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="46b1c-198">Your user is now logged into the developer portal for your API Management service instance.</span></span>

![Registrazione completata][api-management-registration-complete]

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-security-external-identities.png
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
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.png
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-aad-consent]: ./media/api-management-howto-aad/api-management-aad-consent.png
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

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

[Log in to the Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

