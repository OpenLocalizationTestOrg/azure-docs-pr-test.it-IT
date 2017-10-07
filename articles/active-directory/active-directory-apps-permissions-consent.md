---
title: App, autorizzazioni e consenso in Azure Active Directory | Documentazione Microsoft
description: "Azure AD Connect integra le directory locali con Azure Active Directory. In questo modo tooprovide un'identità comune per le applicazioni di Office 365, Azure e SaaS integrata con Azure AD."
keywords: "tooAzure introduzione AD App, che cos'è Azure AD Connect, installare active directory"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 25897cc4-7687-49b6-b0d5-71f51302b6b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/31/2017
ms.author: billmath
ms.reviewer: jesakowi
ms.custom: oldportal;it-pro;
ms.openlocfilehash: af0c2669199736fdb41e85876a7e3a7064e80770
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a><span data-ttu-id="a0824-105">App, autorizzazioni e consenso in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a0824-105">Apps, permissions, and consent in Azure Active Directory</span></span>
<span data-ttu-id="a0824-106">All'interno di Azure Active Directory, è possibile aggiungere directory tooyour delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="a0824-106">Within Azure Active Directory, you can add applications tooyour directory.</span></span>  <span data-ttu-id="a0824-107">applicazioni Hello possono variare a seconda di tipo hello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a0824-107">hello applications can vary depending on hello type of application.</span></span>  <span data-ttu-id="a0824-108">applicazioni tooview nel portale classico hello, selezionare una directory e scegliere le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="a0824-108">tooview applications in hello classic portal, select a directory and choose applications.</span></span>

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> <span data-ttu-id="a0824-109">Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a0824-109">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

## <a name="types-of-apps"></a><span data-ttu-id="a0824-110">Tipi di app</span><span class="sxs-lookup"><span data-stu-id="a0824-110">Types of apps</span></span>

1. <span data-ttu-id="a0824-111">**App a tenant singolo**</span><span class="sxs-lookup"><span data-stu-id="a0824-111">**Single-tenant apps**</span></span> </br>
    - <span data-ttu-id="a0824-112">**App single-tenant** -noto anche delle App line-of-business (LOB) tooas.</span><span class="sxs-lookup"><span data-stu-id="a0824-112">**Single-tenant apps** - Often referred tooas line-of-business (LOB) apps.</span></span> <span data-ttu-id="a0824-113">Ciò avviene hello in cui un utente all'interno dell'organizzazione sviluppa l'app e si desidera che gli utenti in toosign in grado di hello organizzazione toobe nell'app toohello.</span><span class="sxs-lookup"><span data-stu-id="a0824-113">This is hello case where someone within your organization develops their own app, and would like users in hello organization toobe able toosign in toohello app.</span></span>
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - <span data-ttu-id="a0824-114">**App Proxy app** - quando si espone un'applicazione locale con Azure AD App Proxy, un'applicazione single-tenant è registrata nel tenant (in aggiunta toohello servizio Proxy di applicazione).</span><span class="sxs-lookup"><span data-stu-id="a0824-114">**App Proxy apps** - When you expose an on-prem application with Azure AD App Proxy, a single-tenant app is registered in your tenant (in addition toohello App Proxy service).</span></span> <span data-ttu-id="a0824-115">Questa app è ciò che rappresenta l'applicazione locale per tutte le interazioni cloud (ad esempio, autenticazione).</span><span class="sxs-lookup"><span data-stu-id="a0824-115">This app is what represents your on-prem application for all cloud interactions (for example, authentication).</span></span> <span data-ttu-id="a0824-116">L'app proxy richiede Azure AD Basic o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="a0824-116">(App Proxy requires Azure AD Basic or higher.)</span></span>


2. <span data-ttu-id="a0824-117">**App multi-tenant**</span><span class="sxs-lookup"><span data-stu-id="a0824-117">**Multi-tenant apps**</span></span>
    - <span data-ttu-id="a0824-118">**App multi-tenant che altri possano accettare** - simile troppo "app single-tenant che sviluppa organizzazione".</span><span class="sxs-lookup"><span data-stu-id="a0824-118">**Multi-tenant apps which others can consent to** - similar too“single-tenant apps that your organization develops”.</span></span> <span data-ttu-id="a0824-119">Hello differenza principale (oltre alla logica di hello in app hello stessa) è che gli utenti di altri tenant possono anche fornire il consenso tooand Accedi toohello app.</span><span class="sxs-lookup"><span data-stu-id="a0824-119">hello main difference (besides hello logic in hello app itself) is that users from other tenants can also consent tooand sign in toohello app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - <span data-ttu-id="a0824-120">**App multi-tenant sviluppate da terzi per cui Contoso ha ottenuto il consenso**,</span><span class="sxs-lookup"><span data-stu-id="a0824-120">**Multi-tenant apps others develop, which Contoso can consent to**.</span></span> <span data-ttu-id="a0824-121">o, in breve, "app con consenso". Questo è il lato capovolto hello di "multi-tenant App che sviluppate dall'organizzazione".</span><span class="sxs-lookup"><span data-stu-id="a0824-121">(Or “consented apps”, for short.) This is hello flip side of “multi-tenant apps your organization develops”.</span></span> <span data-ttu-id="a0824-122">Quando un'altra organizzazione sviluppa un'applicazione multi-tenant, gli utenti dell'organizzazione possono fornire il consenso toohello app e accedere tooit.</span><span class="sxs-lookup"><span data-stu-id="a0824-122">When another organization develops a multi-tenant app, users of your organization can consent toohello app and sign in tooit.</span></span>
    - <span data-ttu-id="a0824-123">**App proprietarie di Microsoft**: app che rappresentano i servizi Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a0824-123">**Microsoft first-party apps** - Apps that represent Microsoft services.</span></span> <span data-ttu-id="a0824-124">Consenso viene gestito dal fatto di hello che si esegue l'iscrizione per il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="a0824-124">Consent is driven by hello fact that you sign up for hello service.</span></span> <span data-ttu-id="a0824-125">È talvolta speciale dell'esperienza utente e la logica per determinate applicazioni prima parte che viene spesso utilizzata per la definizione dei criteri sull'accesso toohello app.</span><span class="sxs-lookup"><span data-stu-id="a0824-125">There is sometimes special UX and logic for certain first-party apps that is often used when establishing policies around access toohello app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - <span data-ttu-id="a0824-126">**Le app preintegrate** -App disponibili nella raccolta di App di Azure AD, è possibile aggiungere hello tooyour directory tooprovide single sign-on (e in alcuni casi, il provisioning) App SaaS toopopular.</span><span class="sxs-lookup"><span data-stu-id="a0824-126">**Pre-integrated apps** - Apps available in hello Azure AD App Gallery, which you can add tooyour directory tooprovide single sign-on (and in some cases, provisioning) toopopular SaaS apps.</span></span>
    - <span data-ttu-id="a0824-127">**Accesso Single Sign-On di Azure AD**: SSO "reale", per le app che possono essere integrate con Azure AD, tramite un protocollo di accesso supportato, ad esempio SAML 2.0 oppure OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="a0824-127">**Azure AD single sign-on**: “Real” SSO, for apps that can be integrated with Azure AD, through a supported sign-in protocol such as SAML 2.0 or OpenID Connect.</span></span> <span data-ttu-id="a0824-128">procedura guidata Hello illustra la configurazione.</span><span class="sxs-lookup"><span data-stu-id="a0824-128">hello wizard walks you through setting it up.</span></span>
    - <span data-ttu-id="a0824-129">**Password single sign-on**: Azure AD archivia in modo sicuro le credenziali dell'utente hello per app di hello e credenziali hello "inserite" nel modulo di accesso hello dal hello estensione browser di accedere all'App Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0824-129">**Password single sign-on**: Azure AD securely stores hello user’s credentials for hello app, and hello credentials are “injected” into hello sign-in form by hello Azure AD App Access browser extension.</span></span> <span data-ttu-id="a0824-130">Scenario noto anche come "insieme di credenziali delle password".</span><span class="sxs-lookup"><span data-stu-id="a0824-130">Also known as “password vaulting”.</span></span>

## <a name="permissions"></a><span data-ttu-id="a0824-131">Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="a0824-131">Permissions</span></span>

<span data-ttu-id="a0824-132">Quando si registra un'app, utente hello che esegue hello app registrazione (ovvero, lo sviluppatore hello) definisce quale app hello autorizzazioni deve accedere a e le risorse.</span><span class="sxs-lookup"><span data-stu-id="a0824-132">When an app is registered, hello user performing hello app registration (that is, hello developer) defines which permissions hello app needs access to, and which resources.</span></span> <span data-ttu-id="a0824-133">le risorse hello sono, autonomamente, definito come le altre app. Ad esempio, un utente la creazione di un'applicazione lettore di posta elettronica, sarebbe stato che la propria applicazione richiede l'autorizzazione "Accesso alle cassette postali come utente connesso di hello" hello "Office 365 Exchange risorsa in linea" hello:</span><span class="sxs-lookup"><span data-stu-id="a0824-133">(hello resources are, themselves, defined as other apps.) For example, someone building a mail reader app, would state that their app requires hello “Access mailboxes as hello signed-in user” permission in hello “Office 365 Exchange Online” resource:</span></span>
    
![](media/active-directory-apps-permissions-consent/apps6.png)

<span data-ttu-id="a0824-134">Affinché un'applicazione (client hello) toorequest determinate autorizzazioni da un'altra applicazione (risorse hello), gli sviluppatori di hello di hello risorsa app definisce le autorizzazioni di hello esistenti.</span><span class="sxs-lookup"><span data-stu-id="a0824-134">In order for one app (hello client) toorequest a certain permission from another app (hello resource), hello developer of hello resource app defines hello permissions that exist.</span></span> <span data-ttu-id="a0824-135">In questo esempio, Microsoft, il proprietario di hello di app di risorsa "Office 365 Exchange Online" hello, hanno definito un'autorizzazione denominata "Accedere alle cassette postali come utente connesso di hello".</span><span class="sxs-lookup"><span data-stu-id="a0824-135">In our example, Microsoft, hello owner of hello “Office 365 Exchange Online” resource app, have defined a permission named “Access mailboxes as hello signed-in user”.</span></span>

<span data-ttu-id="a0824-136">Quando si definiscono le autorizzazioni, è necessario definire per sviluppatori di app hello se può essere concessa autorizzazione hello, o se è necessario consenso dell'amministratore.</span><span class="sxs-lookup"><span data-stu-id="a0824-136">When defining permissions, hello app developer must define if hello permission can be consented to, or if it requires admin consent.</span></span> <span data-ttu-id="a0824-137">In questo modo gli sviluppatori tooallow utenti tooconsent i propri tooapps richiedono solo le autorizzazioni di sensibilità bassa, ma richiedono autorizzazioni di amministratori tooconsent toomore sensibili.</span><span class="sxs-lookup"><span data-stu-id="a0824-137">This allows developers tooallow users tooconsent on their own tooapps requesting only low-sensitivity permissions, but require admins tooconsent toomore sensitive permissions.</span></span> <span data-ttu-id="a0824-138">Salve, ad esempio, "Azure Active Directory" risorse app, è stato definito, pertanto gli utenti possono fornire il consenso tooapps, richiedono le autorizzazioni di sola lettura limitate.</span><span class="sxs-lookup"><span data-stu-id="a0824-138">For example, hello “Azure Active Directory” resource app, has been defined, so users can consent tooapps, requesting limited read-only permissions.</span></span>  <span data-ttu-id="a0824-139">Tuttavia, il consenso dell'amministratore è obbligatorio per le autorizzazioni di lettura complete e tutte le autorizzazioni di scrittura.</span><span class="sxs-lookup"><span data-stu-id="a0824-139">However, admin consent is required for full read permissions, and all write permissions.</span></span>

<span data-ttu-id="a0824-140">Poiché i client nativi non sono autenticati, un'app definita come app client nativa può richiedere solo autorizzazioni delegate.</span><span class="sxs-lookup"><span data-stu-id="a0824-140">Because native clients are not authenticated, an app defined as a native client app can only request delegated permissions.</span></span> <span data-ttu-id="a0824-141">Ciò significa che deve essere sempre presente un utente effettivo quando si ottiene un token.</span><span class="sxs-lookup"><span data-stu-id="a0824-141">This means that there must always be an actual user involved when obtaining a token.</span></span> <span data-ttu-id="a0824-142">Le app e le API Web (client riservati) devono sempre eseguire l'autenticazione con Azure AD quando ottengono un token di accesso.</span><span class="sxs-lookup"><span data-stu-id="a0824-142">Web apps and web APIs (confidential clients), must always authenticate with Azure AD when getting an access token.</span></span> <span data-ttu-id="a0824-143">Ovvero devono avere anche il possibilità hello che richiedono le autorizzazioni solo per app.</span><span class="sxs-lookup"><span data-stu-id="a0824-143">Meaning they also have hello possibility of requesting app-only permissions.</span></span> <span data-ttu-id="a0824-144">Ad esempio, se un servizio back-end è necessario il servizio back-end di tooauthenticate tooanother.</span><span class="sxs-lookup"><span data-stu-id="a0824-144">For example, if one back-end service needs tooauthenticate tooanother back-end service.</span></span> <span data-ttu-id="a0824-145">Le autorizzazioni che richiedono autorizzazioni di sola app richiedono sempre il consenso dell'amministratore.</span><span class="sxs-lookup"><span data-stu-id="a0824-145">Applications requesting app-only permissions always require administrator consent.</span></span>

<span data-ttu-id="a0824-146">Riepilogo:</span><span class="sxs-lookup"><span data-stu-id="a0824-146">Summarizing:</span></span>



- <span data-ttu-id="a0824-147">Un'applicazione (client) stati autorizzazioni hello che necessarie per altre applicazioni (risorse).</span><span class="sxs-lookup"><span data-stu-id="a0824-147">An app (client) states hello permissions it needs for other apps (resources).</span></span>
- <span data-ttu-id="a0824-148">Un'app (risorsa) indica quali autorizzazioni sono esposti tooother App (client).</span><span class="sxs-lookup"><span data-stu-id="a0824-148">An app (resource) states what permissions are exposed tooother apps (clients).</span></span>
- <span data-ttu-id="a0824-149">Un'autorizzazione può essere di tipo sola app o delegata.</span><span class="sxs-lookup"><span data-stu-id="a0824-149">A permission can be an app-only permission, or a delegated permission.</span></span>
- <span data-ttu-id="a0824-150">Un'autorizzazione delegata può essere contrassegnata come "consente il consenso dell'utente," o "richiede il consenso dell'amministratore".</span><span class="sxs-lookup"><span data-stu-id="a0824-150">A delegated permission can be marked as “allows user consent”, or “requires admin consent”.</span></span>
- <span data-ttu-id="a0824-151">Un'app può funzionare come client (dichiarando che deve risorsa tooa autorizzazioni), come una risorsa (dichiarando le autorizzazioni che espone) o come entrambe.</span><span class="sxs-lookup"><span data-stu-id="a0824-151">An app can behave as a client (by declaring that it needs permissions tooa resource), as a resource (by declaring which permissions it exposes), or as both.</span></span>

## <a name="controls"></a><span data-ttu-id="a0824-152">Controlli</span><span class="sxs-lookup"><span data-stu-id="a0824-152">Controls</span></span>

<span data-ttu-id="a0824-153">di seguito Hello è un elenco di hello admin diversi controlli disponibili per tutti i questo comportamento.</span><span class="sxs-lookup"><span data-stu-id="a0824-153">hello following is a list of hello different admin controls available for all this behavior.</span></span> <span data-ttu-id="a0824-154">salve controlli accessibili nel portale classico di hello da configurare nella directory hello.</span><span class="sxs-lookup"><span data-stu-id="a0824-154">hello admin controls can be accessed in hello classic portal from configure under hello directory.</span></span>

![](media/active-directory-apps-permissions-consent/apps7.png)

<span data-ttu-id="a0824-155">In hello Azure portale, in **gestire**, **impostazioni utente**.</span><span class="sxs-lookup"><span data-stu-id="a0824-155">In hello Azure portal, under **manage**, **user settings**.</span></span>

![](media/active-directory-apps-permissions-consent/apps11.png)



- <span data-ttu-id="a0824-156">È possibile controllare se gli utenti possono fornire il consenso tooapps:</span><span class="sxs-lookup"><span data-stu-id="a0824-156">You can control whether users can consent tooapps:</span></span>

<span data-ttu-id="a0824-157">Nel portale classico di hello selezionare **gli utenti possono concedere applicazioni autorizzazioni tooaccess i propri dati.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span><span class="sxs-lookup"><span data-stu-id="a0824-157">In hello classic portal, select **Users may give applications permissions tooaccess their data.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span></span>

<span data-ttu-id="a0824-158">Nel portale di Azure hello, selezionare **gli utenti possono consentire App tooaccess i propri dati**.</span><span class="sxs-lookup"><span data-stu-id="a0824-158">In hello Azure portal, select **users can allow apps tooaccess their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps12.png)



- <span data-ttu-id="a0824-159">È possibile controllare se gli utenti possono registrare le proprie App LOB single-tenant: nella finestra Seleziona portale classico hello **gli utenti possono aggiungere applicazioni integrate.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span><span class="sxs-lookup"><span data-stu-id="a0824-159">You can control whether users can register their own single-tenant LOB apps: In hello classic portal select **Users may add integrated applications.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span></span>

<span data-ttu-id="a0824-160">Nel portale di Azure hello, selezionare **gli utenti possono consentire App tooaccess i propri dati**.</span><span class="sxs-lookup"><span data-stu-id="a0824-160">In hello Azure portal, select **users can allow apps tooaccess their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
><span data-ttu-id="a0824-161">Anche se si consente agli utenti le app LOB di tooregister single-tenant, vi sono limiti toowhat possono essere registrati.</span><span class="sxs-lookup"><span data-stu-id="a0824-161">Even if you do allow users tooregister single-tenant LOB apps, there are limits toowhat can be registered.</span></span>  
><span data-ttu-id="a0824-162">Ad esempio, per gli sviluppatori che non sono amministratori della directory.</span><span class="sxs-lookup"><span data-stu-id="a0824-162">For example, developers who are not directory admins.</span></span>
>
>- <span data-ttu-id="a0824-163">Gli utenti non possono rendere un'app a tenant singolo un'app multi-tenant.</span><span class="sxs-lookup"><span data-stu-id="a0824-163">Users cannot make a single-tenant app a multi-tenant app.</span></span>
>- <span data-ttu-id="a0824-164">Quando si registra App LOB single-tenant, gli utenti possono richiedere le autorizzazioni solo app tooother app.</span><span class="sxs-lookup"><span data-stu-id="a0824-164">When registering single-tenant LOB apps, users cannot request app-only permissions tooother apps.</span></span>
>- <span data-ttu-id="a0824-165">Quando si registra App LOB single-tenant, gli utenti possono richiedere le autorizzazioni delegate tooother App se tali autorizzazioni richiedono consenso dell'amministratore.</span><span class="sxs-lookup"><span data-stu-id="a0824-165">When registering single-tenant LOB apps, users cannot request delegated permissions tooother apps if those permissions require admin consent.</span></span>
>- <span data-ttu-id="a0824-166">Gli utenti non possono apportare modifiche tooapps che non sono proprietari del.</span><span class="sxs-lookup"><span data-stu-id="a0824-166">Users cannot make changes tooapps that they are not owners of.</span></span>



- <span data-ttu-id="a0824-167">È possibile controllare se gli utenti possono aggiungere app preintegrate che usano password SSO (ossia "insieme di credenziali delle password") ![](media/active-directory-apps-permissions-consent/apps10.png)</span><span class="sxs-lookup"><span data-stu-id="a0824-167">You can control whether users can themselves add pre-integrated apps that use password SSO (aka “password vaulting”) ![](media/active-directory-apps-permissions-consent/apps10.png)</span></span>



- <span data-ttu-id="a0824-168">È possibile controllare le condizioni in base alle quali è possibile accedere alle applicazioni (ovvero, accesso condizionale).</span><span class="sxs-lookup"><span data-stu-id="a0824-168">You can control under which conditions applications can be accessed (that is, conditional access).</span></span> <span data-ttu-id="a0824-169">Tenere presente che questo vale sia app client toohello e toohello risorsa app.</span><span class="sxs-lookup"><span data-stu-id="a0824-169">Be aware this applies both toohello client app and toohello resource app.</span></span> <span data-ttu-id="a0824-170">In tal caso, si supponga di che impostare un criterio di accesso condizionale che afferma che app "Office 365 Exchange Online" hello è accessibile solo da computer che sono conformi.</span><span class="sxs-lookup"><span data-stu-id="a0824-170">So, say you set a conditional access policy that says that hello “Office 365 Exchange Online” app can only be accessed from machines, which are compliant.</span></span>  <span data-ttu-id="a0824-171">Questo criterio verrà attivato anche quando un utente tenta di toouse un'app client che richiede autorizzazioni tooExchange Online.</span><span class="sxs-lookup"><span data-stu-id="a0824-171">This policy will also kick in when a user attempts toouse a client app which requests permissions tooExchange Online.</span></span>



- <span data-ttu-id="a0824-172">Si ha la visibilità in cui le app sono state tooand stato fornito il consenso, quelle che sono in uso.</span><span class="sxs-lookup"><span data-stu-id="a0824-172">You have visibility into which apps have been consented tooand which ones are being used.</span></span>

1.  <span data-ttu-id="a0824-173">Quando un utente acconsente tooan app, viene creato un oggetto entità servizio nel tenant di hello.</span><span class="sxs-lookup"><span data-stu-id="a0824-173">When a user consents tooan app, a ServicePrincipal object is created in hello tenant.</span></span> <span data-ttu-id="a0824-174">Creazione di entità servizio è incluso nel report di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="a0824-174">ServicePrincipal creation is included in hello audit report.</span></span>
2.  <span data-ttu-id="a0824-175">Report attività di accesso utente indicano quale utente hello app accesso a.</span><span class="sxs-lookup"><span data-stu-id="a0824-175">User sign-in activity reports tell you which app hello user is signing in to.</span></span> 

## <a name="example"></a><span data-ttu-id="a0824-176">Esempio</span><span class="sxs-lookup"><span data-stu-id="a0824-176">Example</span></span>

<span data-ttu-id="a0824-177">Ad esempio, è opportuno app "FabrikamMail per Office 365" hello, che si notato accedono gli utenti nel tenant di a.</span><span class="sxs-lookup"><span data-stu-id="a0824-177">As an example, let’s take hello “FabrikamMail for Office 365” app, which you’ve noticed users in your tenant are signing in to.</span></span> <span data-ttu-id="a0824-178">"FabrikamMail" è un'app di lettura della posta elettronica per Android pubblicata da "Fabrikam, Inc.".</span><span class="sxs-lookup"><span data-stu-id="a0824-178">“FabrikamMail” is a mail reader app for Android, published by “Fabrikam, Inc.”.</span></span> <span data-ttu-id="a0824-179">Questo può essere suddiviso in hello "app multi-tenant altri sviluppare, che è possibile fornire il consenso per Contoso".</span><span class="sxs-lookup"><span data-stu-id="a0824-179">This falls into hello “multi-tenant apps other develop, which Contoso can consent to”.</span></span>

<span data-ttu-id="a0824-180">Se gli utenti sono autorizzati tooconsent, ricevono un hello dei messaggi di richiesta di consenso i prima volta, che effettuano l'accesso:![](media/active-directory-apps-permissions-consent/apps14.png)</span><span class="sxs-lookup"><span data-stu-id="a0824-180">If users are allowed tooconsent, they get a consent prompt hello first time they sign in: ![](media/active-directory-apps-permissions-consent/apps14.png)</span></span>

<span data-ttu-id="a0824-181">"Accedere le cassette postali" è una stringa di consenso hello rivolta all'utente l'autorizzazione "Accesso alle cassette postali come utente connesso di hello" hello esposti da "Office 365 Exchange Online" (ovvero, Exchange).</span><span class="sxs-lookup"><span data-stu-id="a0824-181">“Access your mailboxes” is hello user-facing consent string for hello “Access mailboxes as hello signed-in user” permission exposed by “Office 365 Exchange Online” (that is, Exchange).</span></span>

<span data-ttu-id="a0824-182">È possibile visualizzare le autorizzazioni di hello cercando oggetto entità servizio hello per Exchange (risorsa hello), che è stato aggiunto al momento dell'iscrizione per Office 365.</span><span class="sxs-lookup"><span data-stu-id="a0824-182">You can see hello permissions by looking up hello ServicePrincipal object for Exchange (hello resource), which was added when you signed up for Office 365.</span></span> <span data-ttu-id="a0824-183">È possibile pensare oggetto entità servizio hello di un' "istanza" hello app nel tenant di cui viene utilizzato per la registrazione di configurazioni e le diverse opzioni.</span><span class="sxs-lookup"><span data-stu-id="a0824-183">You can think of hello ServicePrincipal object of an “instance” of hello app in your tenant, which is used for recording different options and configurations.</span></span>  <span data-ttu-id="a0824-184">È possibile vedere questo utilizzando hello `Get-AzureADServicePrincipal` in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0824-184">You can see this by using hello `Get-AzureADServicePrincipal` in PowerShell.</span></span>

    PS C:\> Get-AzureADServicePrincipal -ObjectId 383f7b97-6754-4d3d-9474-3908ebcba1c6 | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : Office 365 Exchange Online
    AppId                     : 00000002-0000-0ff1-ce00-000000000000
    AppOwnerTenantId          : 
    AppRoleAssignmentRequired : False
    AppRoles                  : {...}
    DisplayName               : Microsoft.Exchange
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {...
                                , class OAuth2Permission {
                                  AdminConsentDescription : Allows hello app toohave hello same access toomailboxes as hello signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as hello signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows hello app full access tooyour mailboxes on your behalf.
                                  UserConsentDisplayName  : Access your mailboxes
                                  Value                   : full_access_as_user
                                },
                                ...}
    PasswordCredentials       : {}
    PublisherName             : 
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {00000002-0000-0ff1-ce00-000000000000/outlook.office365.com, 00000002-0000-0ff1-ce00-000000000000/mail.office365.com, 00000002-0000-0ff1-ce00-000000000000/outlook.com, 
                                00000002-0000-0ff1-ce00-000000000000/*.outlook.com...}
    Tags                      : {}

<span data-ttu-id="a0824-185">Consenso viene avviato quando l'utente hello fa clic su "Accetto".</span><span class="sxs-lookup"><span data-stu-id="a0824-185">Consent is initiated when hello user clicks “Accept”.</span></span> <span data-ttu-id="a0824-186">Innanzitutto, un oggetto entità servizio per "FabrikamMail per Office 365" viene creato nel tenant di hello.</span><span class="sxs-lookup"><span data-stu-id="a0824-186">First, a ServicePrincipal object for “FabrikamMail for Office 365” is created in hello tenant.</span></span> <span data-ttu-id="a0824-187">Hello ServicePrincipal simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a0824-187">hello ServicePrincipal looks something like this:</span></span>

    PS C:\> Get-AzureADServicePrincipal -SearchString "FabrikamMail for Office 365" | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : a8b16333-851d-42e8-acd2-eac155849b37
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : FabrikamMail for Office 365
    AppId                     : aba7c072-2267-4031-8960-e7a2db6e0590
    AppOwnerTenantId          : 4a4076e0-a70f-41c6-b819-6f9c4a86df89
    AppRoleAssignmentRequired : False
    AppRoles                  : {}
    DisplayName               : FabrikamMail for Office 365
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {}
    PasswordCredentials       : {}
    PublisherName             : Fabrikam, Inc.
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {aba7c072-2267-4031-8960-e7a2db6e0590}
    Tags                      : {WindowsAzureActiveDirectoryIntegratedApp}

<span data-ttu-id="a0824-188">Consenso app tooan crea un collegamento Oauth2PermissionGrant tra segue hello:</span><span class="sxs-lookup"><span data-stu-id="a0824-188">Consenting tooan app creates an Oauth2PermissionGrant link between hello following:</span></span>
  
- <span data-ttu-id="a0824-189">oggetto utente Hello</span><span class="sxs-lookup"><span data-stu-id="a0824-189">hello user object</span></span>
- <span data-ttu-id="a0824-190">applicazioni client Hello ServicePrincipalName (SPN)</span><span class="sxs-lookup"><span data-stu-id="a0824-190">hello client apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="a0824-191">Hello risorsa App ServicePrincipalName (SPN)</span><span class="sxs-lookup"><span data-stu-id="a0824-191">hello resource apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="a0824-192">autorizzazioni in app risorse hello.</span><span class="sxs-lookup"><span data-stu-id="a0824-192">permissions in hello resource app.</span></span>  

<span data-ttu-id="a0824-193">Nel caso di hello di FabrikamMail, simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a0824-193">In hello case of FabrikamMail, it looks something like this:</span></span>

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

<span data-ttu-id="a0824-194">(**ClientId** ID di oggetto principal del FabrikamMail servizio (Buongiorno quello appena creato), **PrincipalId** è l'ID di oggetto utente hello (di hello utente che ha concesso il consenso), **ResourceId**è servizio di Exchange ID oggetto dell'entità, l'ambito è l'autorizzazione di hello in Exchange che è stato concesso il consenso).</span><span class="sxs-lookup"><span data-stu-id="a0824-194">(**ClientId** is FabrikamMail’s service principal object ID (hello one that just got created), **PrincipalId** is hello user object ID (of hello user who consented), **ResourceId** is Exchange’s service principal object ID, Scope is hello permission in Exchange that was consented to).</span></span>

<span data-ttu-id="a0824-195">Se gli utenti non sono consentiti tooconsent, visualizzeranno una schermata in cui è indicato l'autorizzazione è necessaria.</span><span class="sxs-lookup"><span data-stu-id="a0824-195">If users are not allowed tooconsent, they will see a screen that says that permission is required.</span></span>

