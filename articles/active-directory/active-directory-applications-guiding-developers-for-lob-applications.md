---
title: Sviluppare app per Azure AD | Documentazione Microsoft
description: Scritto per i professionisti IT, questo articolo include linee guida per l'integrazione delle applicazioni di Azure in Active Directory.
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
ms.openlocfilehash: 6b119be9c06d8c1ccc8e747168429e6c2d2e7a8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a><span data-ttu-id="1957c-103">Sviluppare app line-of-business per Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1957c-103">Develop line-of-business apps for Azure Active Directory</span></span>
<span data-ttu-id="1957c-104">Questa guida offre una panoramica dello sviluppo di applicazioni line-of-business (LoB) per Azure Active Directory (AD) ed è rivolta agli amministratori globali di Active Directory/Office 365.</span><span class="sxs-lookup"><span data-stu-id="1957c-104">This guide provides an overview of developing line-of-business (LoB) applications for Azure Active Directory (AD).The intended audience is Active Directory/Office 365 global administrators.</span></span>

## <a name="overview"></a><span data-ttu-id="1957c-105">Overview</span><span class="sxs-lookup"><span data-stu-id="1957c-105">Overview</span></span>
<span data-ttu-id="1957c-106">La creazione di applicazioni integrate con Azure AD offre agli utenti dell'organizzazione servizi Single Sign-On per Office 365.</span><span class="sxs-lookup"><span data-stu-id="1957c-106">Building applications integrated with Azure AD gives users in your organization single sign-on with Office 365.</span></span> <span data-ttu-id="1957c-107">La disponibilità dell'applicazione in Azure AD consente di avere il controllo dei criteri di autenticazione impostati per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1957c-107">Having the application in Azure AD gives you control over the authentication policy for the application.</span></span> <span data-ttu-id="1957c-108">Per altre informazioni sull'accesso condizionale e su come proteggere le applicazioni con l'autenticazione a più fattori (MFA), vedere [Configurare le regole di accesso](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="1957c-108">To learn more about conditional access and how to protect apps with multi-factor authentication (MFA) see [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

<span data-ttu-id="1957c-109">Registrare l'applicazione per l'uso di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1957c-109">Register your application to use Azure Active Directory.</span></span> <span data-ttu-id="1957c-110">Registrando l'applicazione, gli sviluppatori possono usare Azure AD per autenticare gli utenti e richiedere l'accesso a risorse degli utenti come posta elettronica, calendario e documenti.</span><span class="sxs-lookup"><span data-stu-id="1957c-110">Registering the application means that your developers can use Azure AD to authenticate users and request access to user resources such as email, calendar, and documents.</span></span>

<span data-ttu-id="1957c-111">Qualsiasi membro della directory (non guest) può registrare un'applicazione, operazione nota anche come *creazione di un oggetto applicazione*.</span><span class="sxs-lookup"><span data-stu-id="1957c-111">Any member of your directory (not guests) can register an application, otherwise known as *creating an application object*.</span></span>

<span data-ttu-id="1957c-112">La registrazione di un'applicazione consente a qualsiasi utente di eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="1957c-112">Registering an application allows any user to do the following:</span></span>

* <span data-ttu-id="1957c-113">Ottenere un'identità per l'applicazione riconosciuta da Azure AD</span><span class="sxs-lookup"><span data-stu-id="1957c-113">Get an identity for their application that Azure AD recognizes</span></span>
* <span data-ttu-id="1957c-114">Ottenere uno o più segreti/chiavi utilizzabili dall'applicazione per l'autenticazione in AD</span><span class="sxs-lookup"><span data-stu-id="1957c-114">Get one or more secrets/keys that the application can use to authenticate itself to AD</span></span>
* <span data-ttu-id="1957c-115">Personalizzare l'applicazione con nome, logo e altri elementi nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1957c-115">Brand the application in the Azure portal with a custom name, logo, etc.</span></span>
* <span data-ttu-id="1957c-116">Applicare le funzionalità di autorizzazione di Azure AD per la propria app, tra cui:</span><span class="sxs-lookup"><span data-stu-id="1957c-116">Apply Azure AD authorization features to their app, including:</span></span>

  * <span data-ttu-id="1957c-117">Controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="1957c-117">Role-Based Access Control (RBAC)</span></span>
  * <span data-ttu-id="1957c-118">Azure Active Directory come server di autorizzazione oAuth (proteggere un'API esposta dall'applicazione)</span><span class="sxs-lookup"><span data-stu-id="1957c-118">Azure Active Directory as oAuth authorization server (secure an API exposed by the application)</span></span>
* <span data-ttu-id="1957c-119">Dichiarare le autorizzazioni necessarie per il funzionamento dell'applicazione nel modo previsto, tra cui:</span><span class="sxs-lookup"><span data-stu-id="1957c-119">Declare required permissions necessary for the application to function as expected, including:</span></span>

      - <span data-ttu-id="1957c-120">Autorizzazioni per l'app (solo amministratori globali).</span><span class="sxs-lookup"><span data-stu-id="1957c-120">App permissions (global administrators only).</span></span> <span data-ttu-id="1957c-121">Ad esempio: appartenenza ai ruoli in un'altra appartenenza di ruolo o applicazione Azure AD relativa a una risorsa, un gruppo di risorse o una sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="1957c-121">For example: Role membership in another Azure AD application or role membership relative to an Azure Resource, Resource Group, or Subscription</span></span>
      - <span data-ttu-id="1957c-122">Autorizzazioni delegate (qualsiasi utente).</span><span class="sxs-lookup"><span data-stu-id="1957c-122">Delegated permissions (any user).</span></span> <span data-ttu-id="1957c-123">Ad esempio: Azure AD, Profilo di accesso e lettura</span><span class="sxs-lookup"><span data-stu-id="1957c-123">For example: Azure AD, Sign-in, and Read Profile</span></span>

> [!NOTE]
> <span data-ttu-id="1957c-124">Per impostazione predefinita, qualsiasi membro può registrare un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1957c-124">By default, any member can register an application.</span></span> <span data-ttu-id="1957c-125">Per informazioni su come limitare le autorizzazioni per la registrazione delle applicazioni per membri specifici, vedere [Procedura per l'aggiunta delle applicazioni ad Azure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span><span class="sxs-lookup"><span data-stu-id="1957c-125">To learn how to restrict permissions for registering applications to specific members, see [How applications are added to Azure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span></span>
>
>

<span data-ttu-id="1957c-126">Ecco cosa deve fare l'amministratore globale per aiutare gli sviluppatori a rendere le loro applicazioni pronte per la produzione:</span><span class="sxs-lookup"><span data-stu-id="1957c-126">Here’s what you, the global administrator, need to do to help developers make their application ready for production:</span></span>

* <span data-ttu-id="1957c-127">Configurare regole di accesso (criteri di accesso/autenticazione a più fattori)</span><span class="sxs-lookup"><span data-stu-id="1957c-127">Configure access rules (access policy/MFA)</span></span>
* <span data-ttu-id="1957c-128">Configurare l'app per richiedere l'assegnazione di utenti e assegnare gli utenti</span><span class="sxs-lookup"><span data-stu-id="1957c-128">Configure the app to require user assignment and assign users</span></span>
* <span data-ttu-id="1957c-129">Evitare l'esperienza di autorizzazione utente predefinita</span><span class="sxs-lookup"><span data-stu-id="1957c-129">Suppress the default user consent experience</span></span>

## <a name="configure-access-rules"></a><span data-ttu-id="1957c-130">Configurare regole di accesso</span><span class="sxs-lookup"><span data-stu-id="1957c-130">Configure access rules</span></span>
<span data-ttu-id="1957c-131">Configurare regole di accesso per ogni applicazione nelle app SaaS.</span><span class="sxs-lookup"><span data-stu-id="1957c-131">Configure per-application access rules to your SaaS apps.</span></span> <span data-ttu-id="1957c-132">Ad esempio, è possibile richiedere l'autenticazione a più fattori oppure solo di consentire l'accesso agli utenti connessi a reti attendibili.</span><span class="sxs-lookup"><span data-stu-id="1957c-132">For example, you can require MFA or only allow access to users on trusted networks.</span></span> <span data-ttu-id="1957c-133">I dettagli a questo scopo sono disponibili nel documento [Configurazione di regole di accesso](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="1957c-133">The details for this are available in the document [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

## <a name="configure-the-app-to-require-user-assignment-and-assign-users"></a><span data-ttu-id="1957c-134">Configurare l'app per richiedere l'assegnazione di utenti e assegnare gli utenti</span><span class="sxs-lookup"><span data-stu-id="1957c-134">Configure the app to require user assignment and assign users</span></span>
<span data-ttu-id="1957c-135">Per impostazione predefinita, gli utenti possono accedere alle applicazioni senza esservi assegnati.</span><span class="sxs-lookup"><span data-stu-id="1957c-135">By default, users can access applications without being assigned.</span></span> <span data-ttu-id="1957c-136">Tuttavia, se l'applicazione espone ruoli o si desidera che venga visualizzata nel pannello di accesso dell'utente, l'assegnazione degli utenti dovrebbe essere richiesta.</span><span class="sxs-lookup"><span data-stu-id="1957c-136">However, if the application exposes roles or if you want the application to appear on a user’s access panel, you should require user assignment.</span></span>

[<span data-ttu-id="1957c-137">Richiedere l'assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="1957c-137">Requiring user assignment</span></span>](active-directory-applications-guiding-developers-requiring-user-assignment.md)

<span data-ttu-id="1957c-138">Per gli abbonati ad Azure AD Premium o Enterprise Mobility Suite (EMS), è consigliabile usare i gruppi.</span><span class="sxs-lookup"><span data-stu-id="1957c-138">If you’re an Azure AD Premium or Enterprise Mobility Suite (EMS) subscriber, we strongly recommend using groups.</span></span> <span data-ttu-id="1957c-139">L'assegnazione di gruppi per l'applicazione consente di delegare le attività di gestione continuativa degli accessi al proprietario del gruppo.</span><span class="sxs-lookup"><span data-stu-id="1957c-139">Assigning groups to the application allows you to delegate ongoing access management to the owner of the group.</span></span> <span data-ttu-id="1957c-140">È possibile creare il gruppo oppure richiedere al responsabile dell'organizzazione di creare il gruppo con gli strumenti per la gestione dei gruppi.</span><span class="sxs-lookup"><span data-stu-id="1957c-140">You can create the group or ask the responsible party in your organization to create the group using your group management facility.</span></span>

[<span data-ttu-id="1957c-141">Assegnazione di utenti a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="1957c-141">Assigning users to an application</span></span>](active-directory-applications-guiding-developers-assigning-users.md)  
[<span data-ttu-id="1957c-142">Assegnazione di gruppi a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="1957c-142">Assigning groups to an application</span></span>](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a><span data-ttu-id="1957c-143">Rimuovere l'esperienza di consenso dell'utente</span><span class="sxs-lookup"><span data-stu-id="1957c-143">Suppress user consent</span></span>
<span data-ttu-id="1957c-144">Per impostazione predefinita, ogni utente è sottoposto a un'esperienza di consenso per poter accedere.</span><span class="sxs-lookup"><span data-stu-id="1957c-144">By default, each user goes through a consent experience to sign in.</span></span> <span data-ttu-id="1957c-145">L'esperienza di consenso, in cui viene chiesto di concedere le autorizzazioni per un'applicazione, può creare confusione per gli utenti che non hanno familiarità con questo tipo di decisioni.</span><span class="sxs-lookup"><span data-stu-id="1957c-145">The consent experience, asking users to grant permissions to an application, can be disconcerting for users who are unfamiliar with making such decisions.</span></span>

<span data-ttu-id="1957c-146">Per le applicazioni attendibili, è possibile semplificare l'esperienza utente dando il consenso per l'applicazione per conto dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="1957c-146">For applications that you trust, you can simplify the user experience by consenting to the application on behalf of your organization.</span></span>

<span data-ttu-id="1957c-147">Per altre informazioni sul consenso dell'utente e l'esperienza di consenso in Azure, vedere [Integrazione di applicazioni con Azure Active Directory](active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="1957c-147">For more information about user consent and the consent experience in Azure, see [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="1957c-148">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="1957c-148">Related Articles</span></span>
* [<span data-ttu-id="1957c-149">Consentire l'accesso remoto sicuro ad applicazioni locali con il proxy di applicazione di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1957c-149">Enable secure remote access to on-premises applications with Azure AD Application Proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="1957c-150">Anteprima dell'accesso condizionale di Azure per app SaaS</span><span class="sxs-lookup"><span data-stu-id="1957c-150">Azure Conditional Access Preview for SaaS Apps</span></span>](active-directory-conditional-access-azuread-connected-apps.md)
* [<span data-ttu-id="1957c-151">Gestione dell'accesso alle app tramite Azure AD</span><span class="sxs-lookup"><span data-stu-id="1957c-151">Managing access to apps with Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* [<span data-ttu-id="1957c-152">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1957c-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
