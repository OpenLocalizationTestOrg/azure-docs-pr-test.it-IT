---
title: gli account sviluppatore aaaAuthorize tramite Azure Active Directory - gestione API di Azure | Documenti Microsoft
description: Informazioni su come gli utenti tooauthorize tramite Azure Active Directory in Gestione API.
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
ms.openlocfilehash: ebf5447a509a47df35e4262138bfcf423cb1dd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a><span data-ttu-id="7d03f-103">La modalità sviluppatore tooauthorize degli account con Azure Active Directory in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="7d03f-103">How tooauthorize developer accounts using Azure Active Directory in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="7d03f-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="7d03f-104">Overview</span></span>
<span data-ttu-id="7d03f-105">Questa guida viene spiegato come tooenable accedere portale per sviluppatori toohello per gli utenti da Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7d03f-105">This guide shows you how tooenable access toohello developer portal for users from Azure Active Directory.</span></span> <span data-ttu-id="7d03f-106">Questa guida illustra anche come toomanage gruppi di utenti di Azure Active Directory tramite l'aggiunta di gruppi esterni che contengono hello agli utenti di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7d03f-106">This guide also shows you how toomanage groups of Azure Active Directory users by adding external groups that contain hello users of an Azure Active Directory.</span></span>

> <span data-ttu-id="7d03f-107">hello toocomplete i passaggi in questa guida è necessario prima disporre di Azure Active Directory in cui toocreate un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7d03f-107">toocomplete hello steps in this guide you must first have an Azure Active Directory in which toocreate an application.</span></span>
> 
> 

## <a name="how-tooauthorize-developer-accounts-using-azure-active-directory"></a><span data-ttu-id="7d03f-108">La modalità sviluppatore tooauthorize degli account con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7d03f-108">How tooauthorize developer accounts using Azure Active Directory</span></span>
<span data-ttu-id="7d03f-109">tooget avviato, fare clic su **portale di pubblicazione** nel portale di Azure per il servizio Gestione API hello.</span><span class="sxs-lookup"><span data-stu-id="7d03f-109">tooget started, click **Publisher portal** in hello Azure portal for your API Management service.</span></span> <span data-ttu-id="7d03f-110">Consente di procedere toohello portale di pubblicazione di gestione API.</span><span class="sxs-lookup"><span data-stu-id="7d03f-110">This takes you toohello API Management publisher portal.</span></span>

![Portale di pubblicazione][api-management-management-console]

> <span data-ttu-id="7d03f-112">Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="7d03f-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="7d03f-113">Fare clic su **sicurezza** da hello **gestione API** menu a sinistra di hello e fare clic su **le identità esterne**.</span><span class="sxs-lookup"><span data-stu-id="7d03f-113">Click **Security** from hello **API Management** menu on hello left and click **External Identities**.</span></span>

![Identità esterne][api-management-security-external-identities]

<span data-ttu-id="7d03f-115">Fare clic su **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7d03f-115">Click **Azure Active Directory**.</span></span> <span data-ttu-id="7d03f-116">Prendere nota di hello **l'URL di reindirizzamento** e passare tooyour Azure Active Directory nel portale di Azure classico hello.</span><span class="sxs-lookup"><span data-stu-id="7d03f-116">Make a note of hello **Redirect URL** and switch over tooyour Azure Active Directory in hello Azure Classic Portal.</span></span>

![Identità esterne][api-management-security-aad-new]

<span data-ttu-id="7d03f-118">Fare clic su hello **Aggiungi** toocreate una nuova applicazione Azure Active Directory e scegliere **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.</span><span class="sxs-lookup"><span data-stu-id="7d03f-118">Click hello **Add** button toocreate a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Aggiungere una nuova applicazione Azure Active Directory][api-management-new-aad-application-menu]

<span data-ttu-id="7d03f-120">Immettere un nome per l'applicazione hello, selezionare **Web dell'applicazione e/o API Web**e fare clic sul pulsante Avanti hello.</span><span class="sxs-lookup"><span data-stu-id="7d03f-120">Enter a name for hello application, select **Web application and/or Web API**, and click hello next button.</span></span>

![Nuova applicazione Azure Active Directory][api-management-new-aad-application-1]

<span data-ttu-id="7d03f-122">Per **Sign-on URL**, immettere hello sign-on URL del portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="7d03f-122">For **Sign-on URL**, enter hello sign-on URL of your developer portal.</span></span> <span data-ttu-id="7d03f-123">In questo esempio hello **Sign-on URL** è `https://aad03.portal.current.int-azure-api.net/signin`.</span><span class="sxs-lookup"><span data-stu-id="7d03f-123">In this example, hello **Sign-on URL** is `https://aad03.portal.current.int-azure-api.net/signin`.</span></span> 

<span data-ttu-id="7d03f-124">Per hello **URL ID App**, immettere il dominio predefinito hello o un dominio personalizzato per hello Azure Active Directory e aggiungere tooit una stringa univoca.</span><span class="sxs-lookup"><span data-stu-id="7d03f-124">For hello **App ID URL**, enter either hello default domain or a custom domain for hello Azure Active Directory, and append a unique string tooit.</span></span> <span data-ttu-id="7d03f-125">In questo esempio hello dominio predefinito di **https://contoso5api.onmicrosoft.com** viene utilizzato con il suffisso hello **/api** specificato.</span><span class="sxs-lookup"><span data-stu-id="7d03f-125">In this example, hello default domain of **https://contoso5api.onmicrosoft.com** is used with hello suffix of **/api** specified.</span></span>

![Proprietà della nuova applicazione Azure Active Directory][api-management-new-aad-application-2]

<span data-ttu-id="7d03f-127">Fare clic su hello controllo pulsante toosave e creare un'applicazione hello e passa toohello **configura** tooconfigure un'applicazione hello nuova scheda.</span><span class="sxs-lookup"><span data-stu-id="7d03f-127">Click hello check button toosave and create hello application, and switch toohello **Configure** tab tooconfigure hello new application.</span></span>

![Nuova applicazione Azure Active Directory creata][api-management-new-aad-app-created]

<span data-ttu-id="7d03f-129">Se più Azure Active Directory prevede toobe utilizzato per questa applicazione, fare clic su **Sì** per **applicazione è multi-tenant**.</span><span class="sxs-lookup"><span data-stu-id="7d03f-129">If multiple Azure Active Directories are going toobe used for this application, click **Yes** for **Application is multi-tenant**.</span></span> <span data-ttu-id="7d03f-130">valore predefinito di Hello è **n**.</span><span class="sxs-lookup"><span data-stu-id="7d03f-130">hello default is **No**.</span></span>

![L'applicazione è multi-tenant][api-management-aad-app-multi-tenant]

<span data-ttu-id="7d03f-132">Hello copia **l'URL di reindirizzamento** da hello **Azure Active Directory** sezione di hello **le identità esterne** scheda nel portale di pubblicazione hello e incollarla hello **URL di risposta** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="7d03f-132">Copy hello **Redirect URL** from hello **Azure Active Directory** section of hello **External Identities** tab in hello publisher portal and paste it into hello **Reply URL** text box.</span></span> 

![URL di risposta][api-management-aad-reply-url]

<span data-ttu-id="7d03f-134">Scorri toohello alla fine di hello configurare della scheda Seleziona hello **autorizzazioni applicazione** elenco a discesa e selezionare **lettura dati directory**.</span><span class="sxs-lookup"><span data-stu-id="7d03f-134">Scroll toohello bottom of hello configure tab, select hello **Application Permissions** drop-down, and check **Read directory data**.</span></span>

![Autorizzazioni applicazione][api-management-aad-app-permissions]

<span data-ttu-id="7d03f-136">Seleziona hello **delegare le autorizzazioni** elenco a discesa e selezionare **attivare l'accesso e leggere i profili degli utenti**.</span><span class="sxs-lookup"><span data-stu-id="7d03f-136">Select hello **Delegate Permissions** drop-down, and check **Enable sign-on and read users' profiles**.</span></span>

![Autorizzazioni delegate][api-management-aad-delegated-permissions]

> <span data-ttu-id="7d03f-138">Per ulteriori informazioni sull'applicazione e le autorizzazioni delegate, vedere [hello accesso API Graph][Accessing hello Graph API].</span><span class="sxs-lookup"><span data-stu-id="7d03f-138">For more information about application and delegated permissions, see [Accessing hello Graph API][Accessing hello Graph API].</span></span>
> 
> 

<span data-ttu-id="7d03f-139">Hello copia **Id Client** toohello Appunti.</span><span class="sxs-lookup"><span data-stu-id="7d03f-139">Copy hello **Client Id** toohello clipboard.</span></span>

![Client Id][api-management-aad-app-client-id]

<span data-ttu-id="7d03f-141">Passare il portale di pubblicazione toohello indietro e incollare in hello **Id Client** copiati dalla configurazione dell'applicazione hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7d03f-141">Switch back toohello publisher portal and paste in hello **Client Id** copied from hello Azure Active Directory application configuration.</span></span>

![Client Id][api-management-client-id]

<span data-ttu-id="7d03f-143">Configurazione di Azure Active Directory toohello nascosto e fare clic su hello **Seleziona durata** menu a discesa hello **chiavi** sezione e specificare un intervallo.</span><span class="sxs-lookup"><span data-stu-id="7d03f-143">Switch back toohello Azure Active Directory configuration, and click hello **Select duration** drop-down in hello **Keys** section and specify an interval.</span></span> <span data-ttu-id="7d03f-144">In questo esempio viene usato **1 anno** .</span><span class="sxs-lookup"><span data-stu-id="7d03f-144">In this example, **1 year** is used.</span></span>

![Chiave][api-management-aad-key-before-save]

<span data-ttu-id="7d03f-146">Fare clic su **salvare** chiave hello configurazione e la visualizzazione toosave hello.</span><span class="sxs-lookup"><span data-stu-id="7d03f-146">Click **Save** toosave hello configuration and display hello key.</span></span> <span data-ttu-id="7d03f-147">Copiare negli Appunti toohello chiave hello.</span><span class="sxs-lookup"><span data-stu-id="7d03f-147">Copy hello key toohello clipboard.</span></span>

> <span data-ttu-id="7d03f-148">Annotare il valore relativo alla chiave.</span><span class="sxs-lookup"><span data-stu-id="7d03f-148">Make a note of this key.</span></span> <span data-ttu-id="7d03f-149">Quando si chiude una finestra di configurazione di hello Azure Active Directory, non è più visualizzata chiave hello.</span><span class="sxs-lookup"><span data-stu-id="7d03f-149">Once you close hello Azure Active Directory configuration window, hello key cannot be displayed again.</span></span>
> 
> 

![Chiave][api-management-aad-key-after-save]

<span data-ttu-id="7d03f-151">Commutatore toohello back-portale e Incolla hello chiave editore in hello **segreto Client** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="7d03f-151">Switch back toohello publisher portal and paste hello key into hello **Client Secret** text box.</span></span>

![Client Secret][api-management-client-secret]

<span data-ttu-id="7d03f-153">**Consentito tenant** specifica le directory hanno accesso toohello API dell'istanza del servizio Gestione API hello.</span><span class="sxs-lookup"><span data-stu-id="7d03f-153">**Allowed Tenants** specifies which directories have access toohello APIs of hello API Management service instance.</span></span> <span data-ttu-id="7d03f-154">Specificare i domini hello di hello toowhich di istanze di Azure Active Directory si desidera accedere toogrant.</span><span class="sxs-lookup"><span data-stu-id="7d03f-154">Specify hello domains of hello Azure Active Directory instances toowhich you want toogrant access.</span></span> <span data-ttu-id="7d03f-155">È possibile separare più domini con virgole, spazi o caratteri di nuova riga.</span><span class="sxs-lookup"><span data-stu-id="7d03f-155">You can separate multiple domains with newlines, spaces, or commas.</span></span>

![Tenant consentiti][api-management-client-allowed-tenants]


<span data-ttu-id="7d03f-157">Una volta hello lo si desidera che la configurazione viene specificata, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="7d03f-157">Once hello desired configuration is specified, click **Save**.</span></span>

![Salva][api-management-client-allowed-tenants-save]

<span data-ttu-id="7d03f-159">Una volta che vengono salvate le modifiche di hello, gli utenti di hello in hello specificati possono accedere Azure Active Directory nel portale per sviluppatori toohello seguendo i passaggi di hello in [Accedi al portale per sviluppatori toohello utilizzando un account Azure Active Directory] [Log in toohello Developer portal using an Azure Active Directory account].</span><span class="sxs-lookup"><span data-stu-id="7d03f-159">Once hello changes are saved, hello users in hello specified Azure Active Directory can sign in toohello Developer portal by following hello steps in [Log in toohello Developer portal using an Azure Active Directory account][Log in toohello Developer portal using an Azure Active Directory account].</span></span>

<span data-ttu-id="7d03f-160">È possibile specificare più domini in hello **consentito tenant** sezione.</span><span class="sxs-lookup"><span data-stu-id="7d03f-160">Multiple domains can be specified in hello **Allowed Tenants** section.</span></span> <span data-ttu-id="7d03f-161">Prima di qualsiasi utente può accedere da un dominio diverso da quello hello originale in cui è stata registrata un'applicazione hello, un amministratore globale di dominio diverso hello deve concedere l'autorizzazione per tooaccess applicazione hello dati della directory.</span><span class="sxs-lookup"><span data-stu-id="7d03f-161">Before any user can log in from a different domain than hello original domain where hello application was registered, a global administrator of hello different domain must grant permission for hello application tooaccess directory data.</span></span> <span data-ttu-id="7d03f-162">autorizzazione toogrant, amministratore globale di hello deve andare troppo`https://<URL of your developer portal>/aadadminconsent` (ad esempio, https://contoso.portal.azure-api.net/aadadminconsent), digitare il nome di dominio hello di hello desiderano toogive accesso tooand tenant di Active Directory fare clic su Invia.</span><span class="sxs-lookup"><span data-stu-id="7d03f-162">toogrant permission, hello global administrator should go too`https://<URL of your developer portal>/aadadminconsent` (for example, https://contoso.portal.azure-api.net/aadadminconsent), type in hello domain name of hello Active Directory tenant they want toogive access tooand click Submit.</span></span> <span data-ttu-id="7d03f-163">In seguito hello esempio, da un amministratore globale `miaoaad.onmicrosoft.com` tenta toogive autorizzazione toothis particolare portale.</span><span class="sxs-lookup"><span data-stu-id="7d03f-163">In hello following example, a global administrator from `miaoaad.onmicrosoft.com` is trying toogive permission toothis particular developer portal.</span></span> 

![Autorizzazioni][api-management-aad-consent]

<span data-ttu-id="7d03f-165">Nella schermata successiva hello, amministratore globale di hello sarà richiesta tooconfirm concesse le autorizzazioni hello.</span><span class="sxs-lookup"><span data-stu-id="7d03f-165">In hello next screen, hello global administrator will be prompted tooconfirm giving hello permission.</span></span> 

![Autorizzazioni][api-management-permissions-form]

> <span data-ttu-id="7d03f-167">Se un amministratore non globali tenta toolog nella prima le autorizzazioni vengono concesse da un amministratore globale, hello account di accesso non riesce e verrà visualizzato un errore.</span><span class="sxs-lookup"><span data-stu-id="7d03f-167">If a non-global administrator tries toolog in before permissions are granted by a global administrator, hello login attempt fails and an error screen is displayed.</span></span>
> 
> 

## <a name="how-tooadd-an-external-azure-active-directory-group"></a><span data-ttu-id="7d03f-168">Modo tooadd esterna Azure Active Directory in cui raggruppare</span><span class="sxs-lookup"><span data-stu-id="7d03f-168">How tooadd an external Azure Active Directory Group</span></span>
<span data-ttu-id="7d03f-169">Dopo l'abilitazione dell'accesso per gli utenti in Azure Active Directory, è possibile aggiungere gruppi di Azure Active Directory in Gestione API toomore gestire facilmente l'associazione di hello di sviluppatori hello gruppo hello con prodotti hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="7d03f-169">After enabling access for users in an Azure Active Directory, you can add Azure Active Directory groups into API Management toomore easily manage hello association of hello developers in hello group with hello desired products.</span></span>

> <span data-ttu-id="7d03f-170">tooconfigure un gruppo esterno di Azure Active Directory, hello Azure Active Directory deve essere prima configurate nella scheda identità hello seguendo la procedura hello nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="7d03f-170">tooconfigure an external Azure Active Directory group, hello Azure Active Directory must first be configured in hello Identities tab by following hello procedure in hello previous section.</span></span> 
> 
> 

<span data-ttu-id="7d03f-171">I gruppi esterni di Azure Active Directory vengono aggiunti da hello **visibilità** scheda del prodotto hello per i quali gruppo di toohello toogrant accesso.</span><span class="sxs-lookup"><span data-stu-id="7d03f-171">External Azure Active Directory groups are added from hello **Visibility** tab of hello product for which you wish toogrant access toohello group.</span></span> <span data-ttu-id="7d03f-172">Fare clic su **prodotti**, quindi fare clic su nome hello del prodotto desiderate hello.</span><span class="sxs-lookup"><span data-stu-id="7d03f-172">Click **Products**, and then click hello name of hello desired product.</span></span>

![Configure product][api-management-configure-product]

<span data-ttu-id="7d03f-174">Passare toohello **visibilità** scheda e fare clic su **Aggiungi gruppi da Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7d03f-174">Switch toohello **Visibility** tab, and click **Add Groups from Azure Active Directory**.</span></span>

![Aggiungere i gruppi][api-management-add-groups]

<span data-ttu-id="7d03f-176">Seleziona hello **Tenant di Azure Active Directory** dall'elenco a discesa hello, quindi nome hello del tipo di gruppo desiderato di hello in hello **gruppi** toobe aggiunto casella di testo.</span><span class="sxs-lookup"><span data-stu-id="7d03f-176">Select hello **Azure Active Directory Tenant** from hello drop-down list, and then type hello name of hello desired group in hello **Groups** toobe added text box.</span></span>

![Selezionare un gruppo][api-management-select-group]

<span data-ttu-id="7d03f-178">Nome di questo gruppo è reperibile in hello **gruppi** elenco per Azure Active Directory, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="7d03f-178">This group name can be found in hello **Groups** list for your Azure Active Directory, as shown in hello following example.</span></span>

![Elenco di gruppi di Azure Active Directory][api-management-aad-groups-list]

<span data-ttu-id="7d03f-180">Fare clic su **Aggiungi** toovalidate hello nome del gruppo e aggiungere il gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="7d03f-180">Click **Add** toovalidate hello group name and add hello group.</span></span> <span data-ttu-id="7d03f-181">In questo esempio hello **agli sviluppatori di Contoso 5** viene aggiunto un gruppo esterno.</span><span class="sxs-lookup"><span data-stu-id="7d03f-181">In this example, hello **Contoso 5 Developers** external group is added.</span></span> 

![Gruppo aggiunto][api-management-aad-group-added]

<span data-ttu-id="7d03f-183">Fare clic su **salvare** toosave hello nuova selezione gruppo.</span><span class="sxs-lookup"><span data-stu-id="7d03f-183">Click **Save** toosave hello new group selection.</span></span>

<span data-ttu-id="7d03f-184">Una volta che un gruppo di Azure Active Directory è stato configurato da un prodotto, è disponibile toobe controllate hello **visibilità** scheda hello altri prodotti nell'istanza del servizio Gestione API hello.</span><span class="sxs-lookup"><span data-stu-id="7d03f-184">Once an Azure Active Directory group has been configured from one product, it is available toobe checked on hello **Visibility** tab for hello other products in hello API Management service instance.</span></span>

<span data-ttu-id="7d03f-185">tooreview e configurare le proprietà di hello per gruppi esterni dopo che sono stati aggiunti, fare clic sul nome hello del gruppo hello hello **gruppi** scheda.</span><span class="sxs-lookup"><span data-stu-id="7d03f-185">tooreview and configure hello properties for external groups once they have been added, click hello name of hello group from hello **Groups** tab.</span></span>

![Gestire i gruppi][api-management-groups]

<span data-ttu-id="7d03f-187">Da qui è possibile modificare hello **nome** hello e **descrizione** del gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="7d03f-187">From here you can edit hello **Name** and hello **Description** of hello group.</span></span>

![Modificare un gruppo][api-management-edit-group]

<span data-ttu-id="7d03f-189">Gli utenti da hello configurato Azure Active Directory possono Accedi al portale per sviluppatori toohello e di visualizzazione e sottoscrizione tooany gruppi per cui dispongono di visibilità seguendo le istruzioni di hello nella seguente sezione hello.</span><span class="sxs-lookup"><span data-stu-id="7d03f-189">Users from hello configured Azure Active Directory can sign in toohello Developer portal and view and subscribe tooany groups for which they have visibility by following hello instructions in hello following section.</span></span>

## <a name="how-toolog-in-toohello-developer-portal-using-an-azure-active-directory-account"></a><span data-ttu-id="7d03f-190">Come toolog nel portale per sviluppatori toohello utilizzando un account Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7d03f-190">How toolog in toohello Developer portal using an Azure Active Directory account</span></span>
<span data-ttu-id="7d03f-191">toolog portale per sviluppatori hello utilizzando un account di Azure Active Directory configurato nelle sezioni precedenti hello, aprire una nuova finestra del browser utilizzando hello **Sign-on URL** dalla configurazione dell'applicazione hello Active Directory e fare clic su **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7d03f-191">toolog into hello Developer portal using an Azure Active Directory account configured in hello previous sections, open a new browser window using hello **Sign-on URL** from hello Active Directory application configuration, and click **Azure Active Directory**.</span></span>

![Portale per sviluppatori][api-management-dev-portal-signin]

<span data-ttu-id="7d03f-193">Immettere le credenziali di hello di uno degli utenti hello in Azure Active Directory e fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="7d03f-193">Enter hello credentials of one of hello users in your Azure Active Directory, and click **Sign in**.</span></span>

![pagina di accesso][api-management-aad-signin]

<span data-ttu-id="7d03f-195">È possibile che venga richiesto di compilare un modulo di registrazione se sono necessarie altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="7d03f-195">You may be prompted with a registration form if any additional information is required.</span></span> <span data-ttu-id="7d03f-196">Completare il modulo di registrazione hello e fare clic su **iscriversi**.</span><span class="sxs-lookup"><span data-stu-id="7d03f-196">Complete hello registration form and click **Sign up**.</span></span>

![Registrazione][api-management-complete-registration]

<span data-ttu-id="7d03f-198">L'utente viene ora registrato nel portale per sviluppatori di hello per l'istanza del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="7d03f-198">Your user is now logged into hello developer portal for your API Management service instance.</span></span>

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

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

