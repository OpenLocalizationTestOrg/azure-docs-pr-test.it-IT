---
title: Documentazione tecnica sull'accesso condizionale in Azure Active Directory | Documentazione Microsoft
description: Il controllo di accesso condizionale consente ad Azure Active Directory di controllare le condizioni specifiche definite durante l'autenticazione dell'utente e prima di consentire l'accesso all'applicazione. Se tali condizioni vengono soddisfatte, l'utente viene autenticato e gli viene consentito l'accesso all'applicazione.
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
ms.openlocfilehash: ca16a5399f94fd1ab267e0798cade3fd83f75b13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a><span data-ttu-id="cec54-104">Documentazione tecnica sull'accesso condizionale di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cec54-104">Azure Active Directory Conditional Access technical reference</span></span>

## <a name="services-enabled-with-conditional-access"></a><span data-ttu-id="cec54-105">Servizi abilitati con l'accesso condizionale</span><span class="sxs-lookup"><span data-stu-id="cec54-105">Services enabled with conditional access</span></span>

<span data-ttu-id="cec54-106">Le regole di accesso condizionale sono supportate in diversi tipi di applicazioni di Azure AD,</span><span class="sxs-lookup"><span data-stu-id="cec54-106">Conditional Access rules are supported across various Azure AD application types.</span></span> <span data-ttu-id="cec54-107">inclusi i seguenti:</span><span class="sxs-lookup"><span data-stu-id="cec54-107">This list includes:</span></span>


* <span data-ttu-id="cec54-108">Applicazioni registrate con il proxy di applicazione di Azure</span><span class="sxs-lookup"><span data-stu-id="cec54-108">Applications registered with the Azure Application Proxy</span></span>
* <span data-ttu-id="cec54-109">App remote di Azure</span><span class="sxs-lookup"><span data-stu-id="cec54-109">Azure Remote App</span></span>
* <span data-ttu-id="cec54-110">Applicazioni line-of-business e multi-tenant sviluppate registrate con Azure AD</span><span class="sxs-lookup"><span data-stu-id="cec54-110">Developed line of business and multi-tenant applications registered with Azure AD</span></span>
* <span data-ttu-id="cec54-111">Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="cec54-111">Dynamics CRM</span></span>
* <span data-ttu-id="cec54-112">Applicazioni federate dalla raccolta di applicazioni di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cec54-112">Federated applications from the Azure AD application gallery</span></span>
* <span data-ttu-id="cec54-113">Microsoft Office 365 Yammer</span><span class="sxs-lookup"><span data-stu-id="cec54-113">Microsoft Office 365 Yammer</span></span>
* <span data-ttu-id="cec54-114">Microsoft Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="cec54-114">Microsoft Office 365 Exchange Online</span></span>
* <span data-ttu-id="cec54-115">Microsoft Office 365 SharePoint Online (include OneDrive for Business)</span><span class="sxs-lookup"><span data-stu-id="cec54-115">Microsoft Office 365 SharePoint Online (includes OneDrive for Business)</span></span>
* <span data-ttu-id="cec54-116">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="cec54-116">Microsoft Power BI</span></span> 
* <span data-ttu-id="cec54-117">Applicazioni con accesso Single Sign-On basato su password dalla raccolta di applicazioni di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cec54-117">Password SSO applications from the Azure AD application gallery</span></span>
* <span data-ttu-id="cec54-118">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="cec54-118">Visual Studio Team Services</span></span>
* <span data-ttu-id="cec54-119">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="cec54-119">Microsoft Teams</span></span>









## <a name="enable-access-rules"></a><span data-ttu-id="cec54-120">Abilitare le regole di accesso</span><span class="sxs-lookup"><span data-stu-id="cec54-120">Enable access rules</span></span>
<span data-ttu-id="cec54-121">Ogni regola può essere abilitata o disabilitata sulla base delle singole applicazioni.</span><span class="sxs-lookup"><span data-stu-id="cec54-121">Each rule can be enabled or disabled on a per application bases.</span></span> <span data-ttu-id="cec54-122">Quando le regole sono impostate su **ON** , verranno abilitate e applicate per gli utenti che accedono all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cec54-122">When rules are **ON** they will be enabled and enforced for users accessing the application.</span></span> <span data-ttu-id="cec54-123">Quando sono impostate su **OFF** , non verranno usate e non avranno alcun impatto sull'esperienza di accesso degli utenti.</span><span class="sxs-lookup"><span data-stu-id="cec54-123">When they are **OFF** they will not be used and will not impact the users sign in experience.</span></span>

## <a name="applying-rules-to-specific-users"></a><span data-ttu-id="cec54-124">Applicazione di regole a utenti specifici</span><span class="sxs-lookup"><span data-stu-id="cec54-124">Applying rules to specific users</span></span>
<span data-ttu-id="cec54-125">Le regole possono essere applicate a specifici set di utenti in base al gruppo di sicurezza impostando **Applica a**.</span><span class="sxs-lookup"><span data-stu-id="cec54-125">Rules can be applied to specific sets of users based on security group by setting **Apply To**.</span></span> <span data-ttu-id="cec54-126">L'opzione **Applica a** può essere impostata su **Tutti gli utenti** o su **Gruppi**.</span><span class="sxs-lookup"><span data-stu-id="cec54-126">**Apply To** can be set to **All Users** or **Groups**.</span></span> <span data-ttu-id="cec54-127">Se è impostata su **Tutti gli utenti**, le regole verranno applicate a qualsiasi utente autorizzato ad accedere all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cec54-127">When set to **All Users** the rules will apply to any user with access to the application.</span></span> <span data-ttu-id="cec54-128">L'opzione **Gruppi** consente di selezionare specifici gruppi di sicurezza e distribuzione. Le regole verranno applicate solo a questi gruppi.</span><span class="sxs-lookup"><span data-stu-id="cec54-128">The **Groups** option allows specific security and distribution groups to be selected, rules will only be enforced for these groups.</span></span>

<span data-ttu-id="cec54-129">Quando si distribuisce una regola, tale regola viene in genere applicata inizialmente a un set limitato di utenti appartenenti a gruppi pilota.</span><span class="sxs-lookup"><span data-stu-id="cec54-129">When deploying a rule,  it is common to first apply it a limited set of users, that are members of a piloting groups.</span></span> <span data-ttu-id="cec54-130">Una volta completata, la regola può essere applicata a **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="cec54-130">Once complete the rule can be applied to **All Users**.</span></span> <span data-ttu-id="cec54-131">In questo modo la regola verrà applicata a tutti gli utenti dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="cec54-131">This will cause the rule to be enforced for all users in the organization.</span></span>

<span data-ttu-id="cec54-132">È anche possibile escludere gruppi selezionati dai criteri usando l'opzione **Escludi** .</span><span class="sxs-lookup"><span data-stu-id="cec54-132">Select groups may also be exempted from policy using the **Except** option.</span></span> <span data-ttu-id="cec54-133">I membri di questi gruppi saranno esentati, anche se appartengono a un gruppo incluso.</span><span class="sxs-lookup"><span data-stu-id="cec54-133">Any members of these groups will be exempted even if they appear in an included group.</span></span>

## <a name="at-work-networks"></a><span data-ttu-id="cec54-134">Reti di tipo "ufficio"</span><span class="sxs-lookup"><span data-stu-id="cec54-134">“At work” networks</span></span>
<span data-ttu-id="cec54-135">Le regole di accesso condizionale che utilizzano una rete di tipo "ufficio" si basano su intervalli di indirizzi IP attendibili configurati in Azure AD oppure utilizzano l'attestazione "rete aziendale".</span><span class="sxs-lookup"><span data-stu-id="cec54-135">Conditional access rules that use an “At work” network, rely on trusted IP address ranges that have been configured in Azure AD, or use of the "inside corpnet" claim from AD FS.</span></span> <span data-ttu-id="cec54-136">Queste regole includono:</span><span class="sxs-lookup"><span data-stu-id="cec54-136">These rules include:</span></span>

* <span data-ttu-id="cec54-137">Richiedi autenticazione a più fattori quando non al lavoro</span><span class="sxs-lookup"><span data-stu-id="cec54-137">Require multi-factor authentication when not at work</span></span>
* <span data-ttu-id="cec54-138">Blocca l'accesso quando non al lavoro</span><span class="sxs-lookup"><span data-stu-id="cec54-138">Block access when not at work</span></span>

<span data-ttu-id="cec54-139">Opzioni per specificare le reti di tipo "ufficio"</span><span class="sxs-lookup"><span data-stu-id="cec54-139">Options for specifiying “at work” networks</span></span>

1. <span data-ttu-id="cec54-140">Configurare gli intervalli IP attendibili nella [pagina di configurazione dell'autenticazione Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span><span class="sxs-lookup"><span data-stu-id="cec54-140">Configure trusted IP address ranges in the [multi-factor authentication configuration page](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span></span> <span data-ttu-id="cec54-141">I criteri di accesso condizionale useranno gli intervalli configurati in ogni richiesta di autenticazione e in ogni emissione di token per valutare le regole.</span><span class="sxs-lookup"><span data-stu-id="cec54-141">Conditional Access policy will use the configured ranges on each authentication request and token issuance to evaluate rules.</span></span> 
2. <span data-ttu-id="cec54-142">Configurare l'utilizzo dell'attestazione "rete aziendale" con AD FS; questa opzione può essere utilizzata con la directory federata.</span><span class="sxs-lookup"><span data-stu-id="cec54-142">Configure use of the inside corpnet claim, this option can be used with federated directories, using AD FS.</span></span> <span data-ttu-id="cec54-143">Per altre informazioni sulle attestazioni "rete aziendale", vedere [Indirizzi IP attendibili](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="cec54-143">To learn more about the inside corpnet claims, see [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="rules-based-on-application-sensitivity"></a><span data-ttu-id="cec54-144">Regole basate sulla sensibilità dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="cec54-144">Rules based on application sensitivity</span></span>
<span data-ttu-id="cec54-145">Le regole vengono configurate per le singole applicazioni, consentendo la protezione di servizi ad alto valore, senza alcun impatto sull'accesso ad altri servizi.</span><span class="sxs-lookup"><span data-stu-id="cec54-145">Rules are configured per application allowing the high value services to be secured without impacting access to other services.</span></span> <span data-ttu-id="cec54-146">Le regole di accesso condizionale possono essere configurate nella scheda **Configura** dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cec54-146">Conditional access rules can be configured on the  **Configure** tab of the application.</span></span> 

<span data-ttu-id="cec54-147">Le regole attualmente disponibili sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="cec54-147">Rules currently offered:</span></span>

* <span data-ttu-id="cec54-148">**Richiedi autenticazione a più fattori**</span><span class="sxs-lookup"><span data-stu-id="cec54-148">**Require multi-factor authentication**</span></span>
  
  * <span data-ttu-id="cec54-149">Tutti gli utenti a cui viene applicato questo criterio devono effettuare almeno una volta l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="cec54-149">All users that this policy is applied to will be required to authenticate via multi-factor authentication at least once.</span></span>
* <span data-ttu-id="cec54-150">**Richiedi autenticazione a più fattori quando non al lavoro**</span><span class="sxs-lookup"><span data-stu-id="cec54-150">**Require multi-factor authentication when not at work**</span></span>
  
  * <span data-ttu-id="cec54-151">Se viene applicato questo criterio, tutti gli utenti devono aver effettuato almeno una volta l'autenticazione a più fattori in caso di accesso al servizio da una posizione remota non lavorativa.</span><span class="sxs-lookup"><span data-stu-id="cec54-151">If this policy is applied, all users will be required to have performed multi-factor authentication at least once if they access the service from a non-work remote location.</span></span> <span data-ttu-id="cec54-152">Se si spostano da una posizione in sede a una posizione remota, dovranno effettuare l'autenticazione a più fattori all'accesso al servizio.</span><span class="sxs-lookup"><span data-stu-id="cec54-152">If they move from a work to remote location, they will be required to perform multifactor authentication when accessing the service.</span></span>
* <span data-ttu-id="cec54-153">**Blocca l'accesso quando non al lavoro**</span><span class="sxs-lookup"><span data-stu-id="cec54-153">**Block access when not at work**</span></span> 
  
  * <span data-ttu-id="cec54-154">Quando gli utenti si spostano dalla posizione in sede a una posizione remota, verranno bloccati se viene applicato il criterio "Blocca l'accesso quando non al lavoro".</span><span class="sxs-lookup"><span data-stu-id="cec54-154">When users move from work to a remote location, they will be blocked if the "Block access when not at work" policy is applied to them.</span></span>  <span data-ttu-id="cec54-155">Nella posizione in sede, saranno nuovamente autorizzati ad accedere.</span><span class="sxs-lookup"><span data-stu-id="cec54-155">They will be re-allowed access when at a work location.</span></span>

## <a name="related-topics"></a><span data-ttu-id="cec54-156">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="cec54-156">Related topics</span></span>
* [<span data-ttu-id="cec54-157">Protezione dell'accesso a Office 365 e ad altre app connesse ad Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cec54-157">Securing access to Office 365 and other apps connected to Azure Active Directory</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="cec54-158">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cec54-158">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

