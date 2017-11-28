---
title: riferimento tecnico di Active Directory l'accesso condizionale aaaAzure | Documenti Microsoft
description: "Con il controllo di accesso condizionale, Azure Active Directory verifica specifiche condizioni hello selezionate per l'autenticazione utente hello e prima di consentire l'accesso toohello applicazione. Quando queste condizioni sono soddisfatte, l'utente di hello è autenticato e accesso toohello applicazione consentita."
services: active-directory.
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 56a5bade-7dcc-4dcf-8092-a7d4bf5df3c1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ee201405d1d17f130607a95bf455b60cd222dd0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a><span data-ttu-id="cefe8-104">Documentazione tecnica sull'accesso condizionale di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cefe8-104">Azure Active Directory Conditional Access technical reference</span></span>

## <a name="services-enabled-with-conditional-access"></a><span data-ttu-id="cefe8-105">Servizi abilitati con l'accesso condizionale</span><span class="sxs-lookup"><span data-stu-id="cefe8-105">Services enabled with conditional access</span></span>

<span data-ttu-id="cefe8-106">Le regole di accesso condizionale sono supportate in diversi tipi di applicazioni di Azure AD,</span><span class="sxs-lookup"><span data-stu-id="cefe8-106">Conditional Access rules are supported across various Azure AD application types.</span></span> <span data-ttu-id="cefe8-107">inclusi i seguenti:</span><span class="sxs-lookup"><span data-stu-id="cefe8-107">This list includes:</span></span>


* <span data-ttu-id="cefe8-108">Applicazioni registrate con hello Proxy dell'applicazione Azure</span><span class="sxs-lookup"><span data-stu-id="cefe8-108">Applications registered with hello Azure Application Proxy</span></span>
* <span data-ttu-id="cefe8-109">App remote di Azure</span><span class="sxs-lookup"><span data-stu-id="cefe8-109">Azure Remote App</span></span>
* <span data-ttu-id="cefe8-110">Applicazioni line-of-business e multi-tenant sviluppate registrate con Azure AD</span><span class="sxs-lookup"><span data-stu-id="cefe8-110">Developed line of business and multi-tenant applications registered with Azure AD</span></span>
* <span data-ttu-id="cefe8-111">Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="cefe8-111">Dynamics CRM</span></span>
* <span data-ttu-id="cefe8-112">Alle applicazioni federate dalla raccolta di applicazione hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cefe8-112">Federated applications from hello Azure AD application gallery</span></span>
* <span data-ttu-id="cefe8-113">Microsoft Office 365 Yammer</span><span class="sxs-lookup"><span data-stu-id="cefe8-113">Microsoft Office 365 Yammer</span></span>
* <span data-ttu-id="cefe8-114">Microsoft Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="cefe8-114">Microsoft Office 365 Exchange Online</span></span>
* <span data-ttu-id="cefe8-115">Microsoft Office 365 SharePoint Online (include OneDrive for Business)</span><span class="sxs-lookup"><span data-stu-id="cefe8-115">Microsoft Office 365 SharePoint Online (includes OneDrive for Business)</span></span>
* <span data-ttu-id="cefe8-116">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="cefe8-116">Microsoft Power BI</span></span> 
* <span data-ttu-id="cefe8-117">Applicazioni SSO password dalla raccolta applicazione hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cefe8-117">Password SSO applications from hello Azure AD application gallery</span></span>
* <span data-ttu-id="cefe8-118">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="cefe8-118">Visual Studio Team Services</span></span>
* <span data-ttu-id="cefe8-119">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="cefe8-119">Microsoft Teams</span></span>









## <a name="enable-access-rules"></a><span data-ttu-id="cefe8-120">Abilitare le regole di accesso</span><span class="sxs-lookup"><span data-stu-id="cefe8-120">Enable access rules</span></span>
<span data-ttu-id="cefe8-121">Ogni regola può essere abilitata o disabilitata sulla base delle singole applicazioni.</span><span class="sxs-lookup"><span data-stu-id="cefe8-121">Each rule can be enabled or disabled on a per application bases.</span></span> <span data-ttu-id="cefe8-122">Quando le regole sono **ON** verrà abilitate e applicate per gli utenti l'accesso a un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="cefe8-122">When rules are **ON** they will be enabled and enforced for users accessing hello application.</span></span> <span data-ttu-id="cefe8-123">Quando si trovano **OFF** non verrà utilizzate e non agli utenti di hello impatto firmerà nell'esperienza.</span><span class="sxs-lookup"><span data-stu-id="cefe8-123">When they are **OFF** they will not be used and will not impact hello users sign in experience.</span></span>

## <a name="applying-rules-toospecific-users"></a><span data-ttu-id="cefe8-124">Utenti di applicare regole toospecific</span><span class="sxs-lookup"><span data-stu-id="cefe8-124">Applying rules toospecific users</span></span>
<span data-ttu-id="cefe8-125">Le regole possono essere applicati toospecific a insiemi di utenti in base a gruppo di sicurezza impostando **applica a**.</span><span class="sxs-lookup"><span data-stu-id="cefe8-125">Rules can be applied toospecific sets of users based on security group by setting **Apply To**.</span></span> <span data-ttu-id="cefe8-126">**Applica a** può essere impostato troppo**tutti gli utenti** o **gruppi**.</span><span class="sxs-lookup"><span data-stu-id="cefe8-126">**Apply To** can be set too**All Users** or **Groups**.</span></span> <span data-ttu-id="cefe8-127">Quando impostato troppo**tutti gli utenti** regole hello applicherà tooany utente con l'applicazione toohello di accesso.</span><span class="sxs-lookup"><span data-stu-id="cefe8-127">When set too**All Users** hello rules will apply tooany user with access toohello application.</span></span> <span data-ttu-id="cefe8-128">Hello **gruppi** opzione consente di sicurezza specifici e toobe di gruppi di distribuzione selezionato, verranno applicate le regole solo per questi gruppi.</span><span class="sxs-lookup"><span data-stu-id="cefe8-128">hello **Groups** option allows specific security and distribution groups toobe selected, rules will only be enforced for these groups.</span></span>

<span data-ttu-id="cefe8-129">Quando si distribuisce una regola, è comune toofirst applica un set limitato di utenti, che sono membri di gruppi di distribuzione pilota.</span><span class="sxs-lookup"><span data-stu-id="cefe8-129">When deploying a rule,  it is common toofirst apply it a limited set of users, that are members of a piloting groups.</span></span> <span data-ttu-id="cefe8-130">Una volta regola hello completo può essere applicato troppo**tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="cefe8-130">Once complete hello rule can be applied too**All Users**.</span></span> <span data-ttu-id="cefe8-131">In questo modo regola hello toobe applicata per tutti gli utenti dell'organizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="cefe8-131">This will cause hello rule toobe enforced for all users in hello organization.</span></span>

<span data-ttu-id="cefe8-132">Selezionare i gruppi possono anche essere esentati dai criteri di utilizzo hello **tranne** opzione.</span><span class="sxs-lookup"><span data-stu-id="cefe8-132">Select groups may also be exempted from policy using hello **Except** option.</span></span> <span data-ttu-id="cefe8-133">I membri di questi gruppi saranno esentati, anche se appartengono a un gruppo incluso.</span><span class="sxs-lookup"><span data-stu-id="cefe8-133">Any members of these groups will be exempted even if they appear in an included group.</span></span>

## <a name="at-work-networks"></a><span data-ttu-id="cefe8-134">Reti di tipo "ufficio"</span><span class="sxs-lookup"><span data-stu-id="cefe8-134">“At work” networks</span></span>
<span data-ttu-id="cefe8-135">Le regole di accesso condizionale che utilizzano una rete "al lavoro", si basano su intervalli di indirizzi IP attendibili che sono stati configurati in Azure AD, o l'utilizzo di hello "all'interno della rete aziendale" attestazione da ADFS.</span><span class="sxs-lookup"><span data-stu-id="cefe8-135">Conditional access rules that use an “At work” network, rely on trusted IP address ranges that have been configured in Azure AD, or use of hello "inside corpnet" claim from AD FS.</span></span> <span data-ttu-id="cefe8-136">Queste regole includono:</span><span class="sxs-lookup"><span data-stu-id="cefe8-136">These rules include:</span></span>

* <span data-ttu-id="cefe8-137">Richiedi autenticazione a più fattori quando non al lavoro</span><span class="sxs-lookup"><span data-stu-id="cefe8-137">Require multi-factor authentication when not at work</span></span>
* <span data-ttu-id="cefe8-138">Blocca l'accesso quando non al lavoro</span><span class="sxs-lookup"><span data-stu-id="cefe8-138">Block access when not at work</span></span>

<span data-ttu-id="cefe8-139">Opzioni per specificare le reti di tipo "ufficio"</span><span class="sxs-lookup"><span data-stu-id="cefe8-139">Options for specifiying “at work” networks</span></span>

1. <span data-ttu-id="cefe8-140">Configurare intervalli di indirizzi IP attendibili in hello [pagina di configurazione di multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span><span class="sxs-lookup"><span data-stu-id="cefe8-140">Configure trusted IP address ranges in hello [multi-factor authentication configuration page](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span></span> <span data-ttu-id="cefe8-141">Criteri di accesso condizionale utilizzerà gli intervalli hello configurato in ogni richiesta e token di rilascio tooevaluate le regole di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="cefe8-141">Conditional Access policy will use hello configured ranges on each authentication request and token issuance tooevaluate rules.</span></span> 
2. <span data-ttu-id="cefe8-142">Configura l'utilizzo di hello all'interno della rete aziendale attestazione, questa opzione può essere utilizzata con le directory federativa, tramite ADFS.</span><span class="sxs-lookup"><span data-stu-id="cefe8-142">Configure use of hello inside corpnet claim, this option can be used with federated directories, using AD FS.</span></span> <span data-ttu-id="cefe8-143">toolearn ulteriori informazioni su hello all'interno della rete aziendale attestazioni, vedere [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="cefe8-143">toolearn more about hello inside corpnet claims, see [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="rules-based-on-application-sensitivity"></a><span data-ttu-id="cefe8-144">Regole basate sulla sensibilità dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="cefe8-144">Rules based on application sensitivity</span></span>
<span data-ttu-id="cefe8-145">Le regole sono configurate per ogni applicazione consentendo toobe di servizi di valore elevato hello protetta senza conseguenze per servizi di accesso tooother.</span><span class="sxs-lookup"><span data-stu-id="cefe8-145">Rules are configured per application allowing hello high value services toobe secured without impacting access tooother services.</span></span> <span data-ttu-id="cefe8-146">Regole di accesso condizionale possono essere configurate in hello **configura** scheda dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="cefe8-146">Conditional access rules can be configured on hello  **Configure** tab of hello application.</span></span> 

<span data-ttu-id="cefe8-147">Le regole attualmente disponibili sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="cefe8-147">Rules currently offered:</span></span>

* <span data-ttu-id="cefe8-148">**Richiedi autenticazione a più fattori**</span><span class="sxs-lookup"><span data-stu-id="cefe8-148">**Require multi-factor authentication**</span></span>
  
  * <span data-ttu-id="cefe8-149">Tutti gli utenti che questo criterio viene applicato toowill essere tooauthenticate richiesto tramite l'autenticazione a più fattori almeno una volta.</span><span class="sxs-lookup"><span data-stu-id="cefe8-149">All users that this policy is applied toowill be required tooauthenticate via multi-factor authentication at least once.</span></span>
* <span data-ttu-id="cefe8-150">**Richiedi autenticazione a più fattori quando non al lavoro**</span><span class="sxs-lookup"><span data-stu-id="cefe8-150">**Require multi-factor authentication when not at work**</span></span>
  
  * <span data-ttu-id="cefe8-151">Se viene applicato il criterio, tutti gli utenti sarà richiesto toohave eseguita almeno una volta autenticazione a più fattori se accedono servizio hello da una postazione remota non lavorative.</span><span class="sxs-lookup"><span data-stu-id="cefe8-151">If this policy is applied, all users will be required toohave performed multi-factor authentication at least once if they access hello service from a non-work remote location.</span></span> <span data-ttu-id="cefe8-152">Se si sposta da un percorso di lavoro tooremote, saranno tooperform richiesto l'autenticazione a più fattori quando si accede hello servizio.</span><span class="sxs-lookup"><span data-stu-id="cefe8-152">If they move from a work tooremote location, they will be required tooperform multifactor authentication when accessing hello service.</span></span>
* <span data-ttu-id="cefe8-153">**Blocca l'accesso quando non al lavoro**</span><span class="sxs-lookup"><span data-stu-id="cefe8-153">**Block access when not at work**</span></span> 
  
  * <span data-ttu-id="cefe8-154">Quando gli utenti di passare da postazione remota tooa di lavoro, verrà bloccati se il criterio di "Bloccare l'accesso quando non al lavoro" hello è toothem applicato.</span><span class="sxs-lookup"><span data-stu-id="cefe8-154">When users move from work tooa remote location, they will be blocked if hello "Block access when not at work" policy is applied toothem.</span></span>  <span data-ttu-id="cefe8-155">Nella posizione in sede, saranno nuovamente autorizzati ad accedere.</span><span class="sxs-lookup"><span data-stu-id="cefe8-155">They will be re-allowed access when at a work location.</span></span>

## <a name="related-topics"></a><span data-ttu-id="cefe8-156">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="cefe8-156">Related topics</span></span>
* [<span data-ttu-id="cefe8-157">Protezione dell'accesso tooOffice 365 e altre App connessa tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cefe8-157">Securing access tooOffice 365 and other apps connected tooAzure Active Directory</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="cefe8-158">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cefe8-158">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

