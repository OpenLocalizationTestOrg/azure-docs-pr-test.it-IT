---
title: App aaaDevelop per Azure AD | Microsoft documenti
description: Scritto per professionisti IT di hello, questo articolo fornisce le linee guida per l'integrazione di applicazioni Azure con Active Directory.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: dd69f2bc-37c5-457c-857d-27acb84267fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2924be752af0be2843b1d9b74d9ec446d3fe1ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a><span data-ttu-id="ed1b4-103">Sviluppare app line-of-business per Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ed1b4-103">Develop line-of-business apps for Azure Active Directory</span></span>
<span data-ttu-id="ed1b4-104">Questa guida fornisce una panoramica dello sviluppo di applicazioni di line-of-business (LoB) per Azure Active Directory (AD) .hello destinati destinatari sono gli amministratori globali di Active Directory o Office 365.</span><span class="sxs-lookup"><span data-stu-id="ed1b4-104">This guide provides an overview of developing line-of-business (LoB) applications for Azure Active Directory (AD).hello intended audience is Active Directory/Office 365 global administrators.</span></span>

## <a name="overview"></a><span data-ttu-id="ed1b4-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ed1b4-105">Overview</span></span>
<span data-ttu-id="ed1b4-106">La creazione di applicazioni integrate con Azure AD offre agli utenti dell'organizzazione servizi Single Sign-On per Office 365.</span><span class="sxs-lookup"><span data-stu-id="ed1b4-106">Building applications integrated with Azure AD gives users in your organization single sign-on with Office 365.</span></span> <span data-ttu-id="ed1b4-107">Con un'applicazione hello in consente di Azure AD, che controllare i criteri di autenticazione hello per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ed1b4-107">Having hello application in Azure AD gives you control over hello authentication policy for hello application.</span></span> <span data-ttu-id="ed1b4-108">altre informazioni sull'accesso condizionale e vedere App tooprotect con multi-factor authentication (MFA) toolearn [le regole di accesso di configurazione](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="ed1b4-108">toolearn more about conditional access and how tooprotect apps with multi-factor authentication (MFA) see [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

<span data-ttu-id="ed1b4-109">Registrare il toouse applicazione Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ed1b4-109">Register your application toouse Azure Active Directory.</span></span> <span data-ttu-id="ed1b4-110">Registrazione di un'applicazione hello significa che gli sviluppatori possono utilizzare Azure AD tooauthenticate utenti e richiedere toouser di accedere alle risorse, ad esempio posta elettronica, calendario e documenti.</span><span class="sxs-lookup"><span data-stu-id="ed1b4-110">Registering hello application means that your developers can use Azure AD tooauthenticate users and request access toouser resources such as email, calendar, and documents.</span></span>

<span data-ttu-id="ed1b4-111">Qualsiasi membro della directory (non guest) può registrare un'applicazione, operazione nota anche come *creazione di un oggetto applicazione*.</span><span class="sxs-lookup"><span data-stu-id="ed1b4-111">Any member of your directory (not guests) can register an application, otherwise known as *creating an application object*.</span></span>

<span data-ttu-id="ed1b4-112">Registrazione di un'applicazione consente qualsiasi esempio di hello toodo utente:</span><span class="sxs-lookup"><span data-stu-id="ed1b4-112">Registering an application allows any user toodo hello following:</span></span>

* <span data-ttu-id="ed1b4-113">Ottenere un'identità per l'applicazione riconosciuta da Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed1b4-113">Get an identity for their application that Azure AD recognizes</span></span>
* <span data-ttu-id="ed1b4-114">Ottenere uno o più segreti/tasti hello applicazione può utilizzare tooauthenticate stesso tooAD</span><span class="sxs-lookup"><span data-stu-id="ed1b4-114">Get one or more secrets/keys that hello application can use tooauthenticate itself tooAD</span></span>
* <span data-ttu-id="ed1b4-115">Applicazione hello del marchio in hello portale di Azure con un nome personalizzato, logo, e così via.</span><span class="sxs-lookup"><span data-stu-id="ed1b4-115">Brand hello application in hello Azure portal with a custom name, logo, etc.</span></span>
* <span data-ttu-id="ed1b4-116">Applicare app tootheir funzionalità di Azure AD autorizzazioni, tra cui:</span><span class="sxs-lookup"><span data-stu-id="ed1b4-116">Apply Azure AD authorization features tootheir app, including:</span></span>

  * <span data-ttu-id="ed1b4-117">Controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="ed1b4-117">Role-Based Access Control (RBAC)</span></span>
  * <span data-ttu-id="ed1b4-118">Azure Active Directory come server di autorizzazione oAuth (un'API esposta da un'applicazione hello protetto)</span><span class="sxs-lookup"><span data-stu-id="ed1b4-118">Azure Active Directory as oAuth authorization server (secure an API exposed by hello application)</span></span>
* <span data-ttu-id="ed1b4-119">Dichiarare necessarie per toofunction applicazione hello delle autorizzazioni necessarie come previsto, tra cui:</span><span class="sxs-lookup"><span data-stu-id="ed1b4-119">Declare required permissions necessary for hello application toofunction as expected, including:</span></span>

      - <span data-ttu-id="ed1b4-120">Autorizzazioni per l'app (solo amministratori globali).</span><span class="sxs-lookup"><span data-stu-id="ed1b4-120">App permissions (global administrators only).</span></span> <span data-ttu-id="ed1b4-121">Ad esempio: un altro Azure AD applicazione o un ruolo di appartenenza relativo tooan Azure, risorsa gruppo di risorse, l'appartenenza al ruolo o una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="ed1b4-121">For example: Role membership in another Azure AD application or role membership relative tooan Azure Resource, Resource Group, or Subscription</span></span>
      - <span data-ttu-id="ed1b4-122">Autorizzazioni delegate (qualsiasi utente).</span><span class="sxs-lookup"><span data-stu-id="ed1b4-122">Delegated permissions (any user).</span></span> <span data-ttu-id="ed1b4-123">Ad esempio: Azure AD, Profilo di accesso e lettura</span><span class="sxs-lookup"><span data-stu-id="ed1b4-123">For example: Azure AD, Sign-in, and Read Profile</span></span>

> [!NOTE]
> <span data-ttu-id="ed1b4-124">Per impostazione predefinita, qualsiasi membro può registrare un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ed1b4-124">By default, any member can register an application.</span></span> <span data-ttu-id="ed1b4-125">toolearn toorestrict le autorizzazioni per la registrazione di membri toospecific applicazioni, vedere [come le applicazioni vengono aggiunti AD tooAzure](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span><span class="sxs-lookup"><span data-stu-id="ed1b4-125">toolearn how toorestrict permissions for registering applications toospecific members, see [How applications are added tooAzure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span></span>
>
>

<span data-ttu-id="ed1b4-126">Ecco cosa ne, amministratore globale di hello, è necessario toodo toohelp gli sviluppatori effettuano le applicazioni di produzione:</span><span class="sxs-lookup"><span data-stu-id="ed1b4-126">Here’s what you, hello global administrator, need toodo toohelp developers make their application ready for production:</span></span>

* <span data-ttu-id="ed1b4-127">Configurare regole di accesso (criteri di accesso/autenticazione a più fattori)</span><span class="sxs-lookup"><span data-stu-id="ed1b4-127">Configure access rules (access policy/MFA)</span></span>
* <span data-ttu-id="ed1b4-128">Configurare l'assegnazione di hello app toorequire utente e assegnare gli utenti</span><span class="sxs-lookup"><span data-stu-id="ed1b4-128">Configure hello app toorequire user assignment and assign users</span></span>
* <span data-ttu-id="ed1b4-129">Esclusione di esperienza di consenso utente hello predefinito</span><span class="sxs-lookup"><span data-stu-id="ed1b4-129">Suppress hello default user consent experience</span></span>

## <a name="configure-access-rules"></a><span data-ttu-id="ed1b4-130">Configurare regole di accesso</span><span class="sxs-lookup"><span data-stu-id="ed1b4-130">Configure access rules</span></span>
<span data-ttu-id="ed1b4-131">Configurare App SaaS tooyour regole di accesso per applicazione.</span><span class="sxs-lookup"><span data-stu-id="ed1b4-131">Configure per-application access rules tooyour SaaS apps.</span></span> <span data-ttu-id="ed1b4-132">Ad esempio, è possibile richiedere l'autenticazione a più fattori o consentire solo l'accesso toousers su reti attendibili.</span><span class="sxs-lookup"><span data-stu-id="ed1b4-132">For example, you can require MFA or only allow access toousers on trusted networks.</span></span> <span data-ttu-id="ed1b4-133">Dettagli Hello per questo sono disponibili nel documento hello [le regole di accesso di configurazione](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="ed1b4-133">hello details for this are available in hello document [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

## <a name="configure-hello-app-toorequire-user-assignment-and-assign-users"></a><span data-ttu-id="ed1b4-134">Configurare l'assegnazione di hello app toorequire utente e assegnare gli utenti</span><span class="sxs-lookup"><span data-stu-id="ed1b4-134">Configure hello app toorequire user assignment and assign users</span></span>
<span data-ttu-id="ed1b4-135">Per impostazione predefinita, gli utenti possono accedere alle applicazioni senza esservi assegnati.</span><span class="sxs-lookup"><span data-stu-id="ed1b4-135">By default, users can access applications without being assigned.</span></span> <span data-ttu-id="ed1b4-136">Tuttavia, se un'applicazione hello espone i ruoli o se si desidera tooappear applicazione hello nel Pannello di accesso dell'utente, è necessario che l'assegnazione utente.</span><span class="sxs-lookup"><span data-stu-id="ed1b4-136">However, if hello application exposes roles or if you want hello application tooappear on a user’s access panel, you should require user assignment.</span></span>

[<span data-ttu-id="ed1b4-137">Richiedere l'assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="ed1b4-137">Requiring user assignment</span></span>](active-directory-applications-guiding-developers-requiring-user-assignment.md)

<span data-ttu-id="ed1b4-138">Per gli abbonati ad Azure AD Premium o Enterprise Mobility Suite (EMS), è consigliabile usare i gruppi.</span><span class="sxs-lookup"><span data-stu-id="ed1b4-138">If you’re an Azure AD Premium or Enterprise Mobility Suite (EMS) subscriber, we strongly recommend using groups.</span></span> <span data-ttu-id="ed1b4-139">Assegnazione di gruppi di applicazioni toohello consente toodelegate accesso continuativo gestione toohello proprietario hello del gruppo di.</span><span class="sxs-lookup"><span data-stu-id="ed1b4-139">Assigning groups toohello application allows you toodelegate ongoing access management toohello owner of hello group.</span></span> <span data-ttu-id="ed1b4-140">È possibile creare il gruppo di hello o chiedere responsabile hello del gruppo di hello toocreate organizzazione utilizzando le funzionalità di gestione di gruppo.</span><span class="sxs-lookup"><span data-stu-id="ed1b4-140">You can create hello group or ask hello responsible party in your organization toocreate hello group using your group management facility.</span></span>

[<span data-ttu-id="ed1b4-141">Assegnazione di utenti applicazione tooan</span><span class="sxs-lookup"><span data-stu-id="ed1b4-141">Assigning users tooan application</span></span>](active-directory-applications-guiding-developers-assigning-users.md)  
[<span data-ttu-id="ed1b4-142">Assegnazione di gruppi di applicazioni tooan</span><span class="sxs-lookup"><span data-stu-id="ed1b4-142">Assigning groups tooan application</span></span>](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a><span data-ttu-id="ed1b4-143">Rimuovere l'esperienza di consenso dell'utente</span><span class="sxs-lookup"><span data-stu-id="ed1b4-143">Suppress user consent</span></span>
<span data-ttu-id="ed1b4-144">Per impostazione predefinita, ogni utente passa attraverso un toosign esperienza di consenso in.</span><span class="sxs-lookup"><span data-stu-id="ed1b4-144">By default, each user goes through a consent experience toosign in.</span></span> <span data-ttu-id="ed1b4-145">esperienza di consenso Hello, che richiede agli utenti le autorizzazioni di toogrant tooan applicazione, può essere aggiunto agli utenti che hanno familiarità con tali decisioni.</span><span class="sxs-lookup"><span data-stu-id="ed1b4-145">hello consent experience, asking users toogrant permissions tooan application, can be disconcerting for users who are unfamiliar with making such decisions.</span></span>

<span data-ttu-id="ed1b4-146">Per le applicazioni attendibili, è possibile semplificare esperienza utente hello applicando toohello il consenso per conto dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="ed1b4-146">For applications that you trust, you can simplify hello user experience by consenting toohello application on behalf of your organization.</span></span>

<span data-ttu-id="ed1b4-147">Per ulteriori informazioni sul consenso dell'utente e consenso hello in Azure, vedere [integrazione di applicazioni con Azure Active Directory](active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="ed1b4-147">For more information about user consent and hello consent experience in Azure, see [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="ed1b4-148">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="ed1b4-148">Related Articles</span></span>
* [<span data-ttu-id="ed1b4-149">Consentire alle applicazioni di accesso remoto sicuro tooon locale con Proxy dell'applicazione Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed1b4-149">Enable secure remote access tooon-premises applications with Azure AD Application Proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="ed1b4-150">Anteprima dell'accesso condizionale di Azure per app SaaS</span><span class="sxs-lookup"><span data-stu-id="ed1b4-150">Azure Conditional Access Preview for SaaS Apps</span></span>](active-directory-conditional-access-azuread-connected-apps.md)
* [<span data-ttu-id="ed1b4-151">La gestione di accesso tooapps con Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed1b4-151">Managing access tooapps with Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* [<span data-ttu-id="ed1b4-152">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ed1b4-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
