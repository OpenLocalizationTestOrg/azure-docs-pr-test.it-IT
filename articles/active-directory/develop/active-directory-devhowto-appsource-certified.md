---
title: aaaHow tooget AppSource certificate per Azure Active Directory | Documenti Microsoft
description: Informazioni dettagliate su come tooget applicazione AppSource certificate per Azure Active Directory.
services: active-directory
documentationcenter: 
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 21206407-49f8-4c0b-84d1-c25e17cd4183
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/03/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: e9f07e9220afcba1120b987122fe770fe5225eed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-appsource-certified-for-azure-active-directory"></a><span data-ttu-id="71521-103">Come tooget AppSource certificate per Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="71521-103">How tooget AppSource Certified for Azure Active Directory</span></span>
<span data-ttu-id="71521-104">[Microsoft AppSource](https://appsource.microsoft.com/) è una destinazione per toodiscover agli utenti di business, provare e gestire le applicazioni line-of-business SaaS (autonomo SaaS e componente aggiuntivo tooexisting SaaS Microsoft prodotti).</span><span class="sxs-lookup"><span data-stu-id="71521-104">[Microsoft AppSource](https://appsource.microsoft.com/) is a destination for business users toodiscover, try, and manage line-of-business SaaS applications (standalone SaaS and add-on tooexisting Microsoft SaaS products).</span></span>

<span data-ttu-id="71521-105">toolist un'applicazione SaaS in AppSource autonoma, è necessario accettare l'applicazione single sign-on dall'account aziendale da qualsiasi società o organizzazione con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="71521-105">toolist a standalone SaaS application on AppSource, your application must accept single sign-on from work accounts from any company or organization that has Azure Active Directory.</span></span> <span data-ttu-id="71521-106">processo di accesso Hello deve utilizzare hello [OpenID Connect](./active-directory-protocols-openid-connect-code.md) o [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocolli.</span><span class="sxs-lookup"><span data-stu-id="71521-106">hello sign-in process must use hello [OpenID Connect](./active-directory-protocols-openid-connect-code.md) or [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocols.</span></span> <span data-ttu-id="71521-107">L'integrazione SAML non è accettata per la certificazione AppSource.</span><span class="sxs-lookup"><span data-stu-id="71521-107">SAML integration is not accepted for AppSource certification.</span></span>

## <a name="guides-and-code-samples"></a><span data-ttu-id="71521-108">Guide ed esempi di codice</span><span class="sxs-lookup"><span data-stu-id="71521-108">Guides and code samples</span></span>
<span data-ttu-id="71521-109">Se si desidera toolearn sulla modalità di connessione dell'applicazione con Azure Active Directory tramite Openid di toointegrate, seguire le guide e scrivere il codice negli esempi di hello [Guida per gli sviluppatori di Azure Active Directory](./active-directory-developers-guide.md#get-started "introduzione Azure AD per gli sviluppatori").</span><span class="sxs-lookup"><span data-stu-id="71521-109">If you want toolearn about how toointegrate your application with Azure Active Directory using Open ID connect, follow our guides and code samples in hello [Azure Active Directory developer's guide](./active-directory-developers-guide.md#get-started "Get Started with Azure AD for developers").</span></span>

## <a name="multi-tenant-applications"></a><span data-ttu-id="71521-110">Applicazioni multi-tenant</span><span class="sxs-lookup"><span data-stu-id="71521-110">Multi-tenant applications</span></span>

<span data-ttu-id="71521-111">Un'applicazione che accetta l'accesso degli utenti da qualsiasi società o organizzazione con Azure Active Directory senza richiedere un'istanza, una configurazione o una distribuzione separata è nota come *applicazione multi-tenant*.</span><span class="sxs-lookup"><span data-stu-id="71521-111">An application that accepts sign-ins from users from any company or organization that have Azure Active Directory without requiring a separate instance, configuration, or deployment is known as a *multi-tenant application*.</span></span> <span data-ttu-id="71521-112">AppSource consiglia che le applicazioni implementano hello multi-tenancy tooenable *con clic singolo* esperienza di valutazione gratuita.</span><span class="sxs-lookup"><span data-stu-id="71521-112">AppSource recommends that applications implement multi-tenancy tooenable hello *single-click* free trial experience.</span></span>

<span data-ttu-id="71521-113">In ordine tooenable multi-tenancy sull'applicazione:</span><span class="sxs-lookup"><span data-stu-id="71521-113">In order tooenable multi-tenancy on your application:</span></span>
- <span data-ttu-id="71521-114">Impostare `Multi-Tenanted` proprietà troppo`Yes` sulle informazioni della registrazione applicazione in hello [portale Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (per impostazione predefinita, le applicazioni create in hello portale di Azure sono configurate come *single-tenant*)</span><span class="sxs-lookup"><span data-stu-id="71521-114">Set `Multi-Tenanted` property too`Yes` on your application registration's information in hello [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (by default, applications created in hello Azure Portal are configured as *single-tenant*)</span></span>
- <span data-ttu-id="71521-115">Aggiornare il toohello le richieste di codice toosend '`common`' endpoint (aggiornare l'endpoint di hello da *https://login.microsoftonline.com/ {yourtenant}* troppo*https://login.microsoftonline.com/common*)</span><span class="sxs-lookup"><span data-stu-id="71521-115">Update your code toosend requests toohello '`common`' endpoint (update hello endpoint from *https://login.microsoftonline.com/{yourtenant}* too*https://login.microsoftonline.com/common*)</span></span>
- <span data-ttu-id="71521-116">Per alcune piattaforme, ad esempio ASP.NET, è necessario anche tooupdate tooaccept il codice più emittenti</span><span class="sxs-lookup"><span data-stu-id="71521-116">For some platforms, like ASP.NET, you need also tooupdate your code tooaccept multiple issuers</span></span>

<span data-ttu-id="71521-117">Per ulteriori informazioni su multi-tenancy, vedere: [come toosign in qualsiasi utente di Azure Active Directory (AD) usando hello modello di applicazione multi-tenant](./active-directory-devhowto-multi-tenant-overview.md).</span><span class="sxs-lookup"><span data-stu-id="71521-117">For more information about multi-tenancy, see: [How toosign in any Azure Active Directory (AD) user using hello multi-tenant application pattern](./active-directory-devhowto-multi-tenant-overview.md).</span></span>

### <a name="single-tenant-applications"></a><span data-ttu-id="71521-118">Applicazioni a tenant singolo</span><span class="sxs-lookup"><span data-stu-id="71521-118">Single-tenant applications</span></span>
<span data-ttu-id="71521-119">Le applicazioni che accettano solo l'accesso degli utenti di un'istanza di Azure Active Directory definita sono note come *applicazioni a tenant singolo*.</span><span class="sxs-lookup"><span data-stu-id="71521-119">Applications that only accept sign-ins from users of a defined Azure Active Directory instance are known as *single-tenant application*.</span></span> <span data-ttu-id="71521-120">Gli utenti esterni, inclusi gli account aziendale o dell'istituto di istruzione da altre organizzazioni o account personale, possono accedere in applicazione single-tenant tooa dopo l'aggiunta di ogni utente come *account guest* istanza toohello Azure Active Directory un'applicazione Hello è registrata.</span><span class="sxs-lookup"><span data-stu-id="71521-120">External users (including Work or School accounts from other organizations, or personal account) can sign in tooa single-tenant application after adding each user as *guest account* toohello Azure Active Directory instance that hello application is registered.</span></span> <span data-ttu-id="71521-121">È possibile aggiungere utenti come guest tooan di account Azure Active Directory tramite hello [ *collaborazione B2B di Azure AD* ](../active-directory-b2b-what-is-azure-ad-b2b.md) - e può essere eseguita [a livello di programmazione](../active-directory-b2b-code-samples.md).</span><span class="sxs-lookup"><span data-stu-id="71521-121">You can add users as guest accounts tooan Azure Active Directory via hello [*Azure AD B2B collaboration*](../active-directory-b2b-what-is-azure-ad-b2b.md) - and it can be done [programatically](../active-directory-b2b-code-samples.md).</span></span> <span data-ttu-id="71521-122">Quando si aggiunge un utente come tooan account guest Azure Active Directory, un messaggio di posta elettronica di invito viene inviato toohello utente, con invito hello tooaccept facendo clic sul collegamento hello nel messaggio di posta elettronica di invito hello.</span><span class="sxs-lookup"><span data-stu-id="71521-122">When you add a user as guest account tooan Azure Active Directory, an invitation email is sent toohello user, who has tooaccept hello invitation by clicking on hello link in hello invitation email.</span></span> <span data-ttu-id="71521-123">Inviti inviati tooan utente in un'organizzazione invitando che sia anche membro dell'organizzazione partner hello sono tooaccept non è necessario un invito toosign in.</span><span class="sxs-lookup"><span data-stu-id="71521-123">Invitations that are sent tooan additional user in an inviting organization that is also a member of hello partner organization are not required tooaccept an invitation toosign in.</span></span>

<span data-ttu-id="71521-124">Le applicazioni single-tenant possono abilitare hello *Contact Me* esperienza, ma se si desidera tooenable hello con clic singolo / libero valutazione AppSource consigliato, abilitare multi-tenancy all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="71521-124">Single-tenant applications can enable hello *Contact Me* experience, but if you want tooenable hello single-click/ free trial experience that AppSource recommends, enable multi-tenancy on your application instead.</span></span>


## <a name="appsource-trial-experiences"></a><span data-ttu-id="71521-125">Esperienze di valutazione di AppSource</span><span class="sxs-lookup"><span data-stu-id="71521-125">AppSource trial experiences</span></span>

### <a name="free-trial-customer-led-trial-experience"></a><span data-ttu-id="71521-126">Versione di valutazione gratuita (esperienza di valutazione gestita dal cliente)</span><span class="sxs-lookup"><span data-stu-id="71521-126">Free Trial (Customer-led trial experience)</span></span> 
<span data-ttu-id="71521-127">Hello *lock-versione di valutazione* esperienza hello AppSource consigliato, poiché offre un'applicazione tooyour accesso con clic singolo.</span><span class="sxs-lookup"><span data-stu-id="71521-127">hello *customer-led trial* is hello experience that AppSource recommends as it offers a single-click access tooyour application.</span></span> <span data-ttu-id="71521-128">Di seguito è illustrata questa esperienza:</span><span class="sxs-lookup"><span data-stu-id="71521-128">Below an illustration of how this experience looks like:</span></span><br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="71521-129">L'utente trova l'applicazione nel sito Web AppSource</span><span class="sxs-lookup"><span data-stu-id="71521-129">User finds your application in AppSource Web Site</span></span></li><li><span data-ttu-id="71521-130">Seleziona l'opzione "Versione di valutazione gratuita"</span><span class="sxs-lookup"><span data-stu-id="71521-130">Selects ‘Free trial’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li><span data-ttu-id="71521-131">AppSource reindirizza l'utente tooa URL del sito web</span><span class="sxs-lookup"><span data-stu-id="71521-131">AppSource redirects user tooa URL in your web site</span></span></li><li><span data-ttu-id="71521-132">Il sito web avvia hello <i>single sign-on</i> processo automaticamente (al caricamento della pagina)</span><span class="sxs-lookup"><span data-stu-id="71521-132">Your web site starts hello <i>single-sign-on</i> process automatically (on page load)</span></span></li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="71521-133">Utente viene reindirizzato tooMicrosoft Accedi pagina</span><span class="sxs-lookup"><span data-stu-id="71521-133">User is redirected tooMicrosoft Sign-in page</span></span></li><li><span data-ttu-id="71521-134">Utente fornisce credenziali toosign in</span><span class="sxs-lookup"><span data-stu-id="71521-134">User provides credentials toosign in</span></span></li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="71521-135">L'utente dà il consenso per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="71521-135">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="71521-136">Accedi completa e l'utente viene reindirizzato tooyour indietro sito</span><span class="sxs-lookup"><span data-stu-id="71521-136">Sign-in completes and user is redirected back tooyour web site</span></span></li><li><span data-ttu-id="71521-137">Utente avvia versione di valutazione gratuita di hello</span><span class="sxs-lookup"><span data-stu-id="71521-137">User starts hello free trial</span></span></li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a><span data-ttu-id="71521-138">Desidero essere contattato (esperienza di valutazione gestita dal partner)</span><span class="sxs-lookup"><span data-stu-id="71521-138">Contact Me (Partner-led trial experience)</span></span>
<span data-ttu-id="71521-139">Hello *partner valutazione* può essere utilizzata quando un manuale o un'operazione a lungo termine deve utente di hello tooprovision toohappen /Company: ad esempio, l'applicazione deve tooprovision le macchine virtuali, istanze di database, o operazioni che richiedono toocomplete molto tempo.</span><span class="sxs-lookup"><span data-stu-id="71521-139">hello *partner trial experience* can be used when a manual or a long-term operation needs toohappen tooprovision hello user/ company: for example, your application needs tooprovision virtual machines, database instances, or operations that take much time toocomplete.</span></span> <span data-ttu-id="71521-140">In questo caso, dopo l'utente seleziona hello *'Richiesta versione di valutazione'* pulsante e compila un modulo, AppSource invia hello informazioni di contatto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="71521-140">In this case, after user selects hello *'Request Trial'* button and fills out a form, AppSource sends you hello user's contact information.</span></span> <span data-ttu-id="71521-141">Dopo aver ricevuto queste informazioni, quindi eseguire il provisioning di ambiente hello e invia all'utente di toohello hello istruzioni su come tooaccess hello esperienza di valutazione:</span><span class="sxs-lookup"><span data-stu-id="71521-141">Upon receiving this information, you then provision hello environment and send hello instructions toohello user on how tooaccess hello trial experience:</span></span><br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="71521-142">L'utente trova l'applicazione nel sito Web AppSource</span><span class="sxs-lookup"><span data-stu-id="71521-142">User finds your application in AppSource web site</span></span></li><li><span data-ttu-id="71521-143">Seleziona l'opzione "Desidero essere contattato"</span><span class="sxs-lookup"><span data-stu-id="71521-143">Selects ‘Contact Me’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li><span data-ttu-id="71521-144">Compila un modulo con le informazioni di contatto</span><span class="sxs-lookup"><span data-stu-id="71521-144">Fills out a form with contact information</span></span></li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td><span data-ttu-id="71521-145">Le informazioni dell'utente vengono ricevute</span><span class="sxs-lookup"><span data-stu-id="71521-145">You receive user information</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td><span data-ttu-id="71521-146">L'ambiente viene configurato</span><span class="sxs-lookup"><span data-stu-id="71521-146">Setup environment</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td><span data-ttu-id="71521-147">L'utente viene contattato con le informazioni sulla versione di valutazione</span><span class="sxs-lookup"><span data-stu-id="71521-147">Contact user with trial info</span></span></td>
        </tr>
        </table><br/><br/>
        <ul><li><span data-ttu-id="71521-148">Le informazioni dell'utente vengono ricevute e viene configurata l'istanza di valutazione</span><span class="sxs-lookup"><span data-stu-id="71521-148">You receive user's information and setup trial instance</span></span></li><li><span data-ttu-id="71521-149">Si invia hello collegamento ipertestuale tooaccess utenti toohello dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="71521-149">You send hello hyperlink tooaccess your application toohello user</span></span></li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="71521-150">Utente accede l'applicazione e il processo single sign-on di hello completo</span><span class="sxs-lookup"><span data-stu-id="71521-150">User accesses your application and complete hello single-sign-on process</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="71521-151">L'utente dà il consenso per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="71521-151">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="71521-152">Accedi completa e l'utente viene reindirizzato tooyour indietro sito</span><span class="sxs-lookup"><span data-stu-id="71521-152">Sign-in completes and user is redirected back tooyour web site</span></span></li><li><span data-ttu-id="71521-153">Utente avvia versione di valutazione gratuita di hello</span><span class="sxs-lookup"><span data-stu-id="71521-153">User starts hello free trial</span></span></li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a><span data-ttu-id="71521-154">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="71521-154">More information</span></span>
<span data-ttu-id="71521-155">Per ulteriori informazioni sull'esperienza di valutazione AppSource hello, vedere [questo video](https://aka.ms/trialexperienceforwebapps).</span><span class="sxs-lookup"><span data-stu-id="71521-155">For more information about hello AppSource trial experience, see [this video](https://aka.ms/trialexperienceforwebapps).</span></span> 
 
## <a name="next-steps"></a><span data-ttu-id="71521-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="71521-156">Next Steps</span></span>

- <span data-ttu-id="71521-157">Per altre informazioni sulla creazione di applicazioni che supportano gli accessi di Azure Active Directory, vedere [Scenari di autenticazione per Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span><span class="sxs-lookup"><span data-stu-id="71521-157">For more information on building applications that support Azure Active Directory sign-ins, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span></span> 

- <span data-ttu-id="71521-158">Per informazioni su come toolist applicazione SaaS in AppSource, Vai vedere [AppSource informazioni per i Partner](https://appsource.microsoft.com/partners)</span><span class="sxs-lookup"><span data-stu-id="71521-158">For information on how toolist your SaaS application in AppSource, go see [AppSource Partner Information](https://appsource.microsoft.com/partners)</span></span>


## <a name="get-support"></a><span data-ttu-id="71521-159">Ottenere supporto</span><span class="sxs-lookup"><span data-stu-id="71521-159">Get Support</span></span>
<span data-ttu-id="71521-160">Per l'integrazione di Azure Active Directory, utilizziamo [Overflow dello Stack](http://stackoverflow.com/questions/tagged/azure-active-directory) con supporto di tooprovide hello della community.</span><span class="sxs-lookup"><span data-stu-id="71521-160">For Azure Active Directory integration, we use [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory) with hello community tooprovide support.</span></span> 

<span data-ttu-id="71521-161">Si consiglia di è possibile porre domande su Stack Overflow prima e individuare toosee problemi esistenti se un utente ha richiesto la domanda prima.</span><span class="sxs-lookup"><span data-stu-id="71521-161">We highly recommend you ask your questions on Stack Overflow first and browse existing issues toosee if someone has asked your question before.</span></span> <span data-ttu-id="71521-162">Assicurarsi di aggiungere alle domande o ai commenti il tag `[azure-active-directory]`.</span><span class="sxs-lookup"><span data-stu-id="71521-162">Make sure that your questions or comments are tagged with `[azure-active-directory]`.</span></span>

<span data-ttu-id="71521-163">Utilizzare hello seguendo i commenti e suggerimenti tooprovide di sezione commenti e consentono di ridefinire e definire il contenuto.</span><span class="sxs-lookup"><span data-stu-id="71521-163">Use hello following comments section tooprovide feedback and help us refine and shape our content.</span></span>

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->