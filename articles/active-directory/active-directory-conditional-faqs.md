---
title: Domande frequenti sull'accesso condizionale di Azure Active Directory | Microsoft Docs
description: Ottenere risposte alle domande frequenti sull'accesso condizionale in Azure Active Directory.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: e9a5af41b08b593e4d97475f29da4e5fe8df7042
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a><span data-ttu-id="f6ac9-103">Domande frequenti sull'accesso condizionale di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6ac9-103">Azure Active Directory conditional access FAQs</span></span>

## <a name="which-applications-work-with-conditional-access-policies"></a><span data-ttu-id="f6ac9-104">Quali applicazioni funzionano con i criteri di accesso condizionale?</span><span class="sxs-lookup"><span data-stu-id="f6ac9-104">Which applications work with conditional access policies?</span></span>

<span data-ttu-id="f6ac9-105">Per informazioni sulle applicazioni che usano i criteri di accesso condizionale, vedere [Applicazioni e browser che usano regole di accesso condizionale in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span><span class="sxs-lookup"><span data-stu-id="f6ac9-105">For information about applications that work with conditional access policies, see [Applications and browsers that use conditional access rules in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span></span>

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a><span data-ttu-id="f6ac9-106">I criteri di accesso condizionale vengono applicati a Collaborazione B2B e agli utenti guest?</span><span class="sxs-lookup"><span data-stu-id="f6ac9-106">Are conditional access policies enforced for B2B collaboration and guest users?</span></span>

<span data-ttu-id="f6ac9-107">I criteri vengono applicati agli utenti di Collaborazione business-to-business (B2B).</span><span class="sxs-lookup"><span data-stu-id="f6ac9-107">Policies are enforced for business-to-business (B2B) collaboration users.</span></span> <span data-ttu-id="f6ac9-108">In alcuni casi, tuttavia, è possibile che un utente non sia in grado di soddisfare i requisiti dei criteri.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-108">However, in some cases, a user might not be able to satisfy the policy requirements.</span></span> <span data-ttu-id="f6ac9-109">È possibile, ad esempio, che l'organizzazione di un utente guest non supporti l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-109">For example, a guest user's organization might not support multi-factor authentication.</span></span> 



## <a name="does-a-sharepoint-online-policy-also-apply-to-onedrive-for-business"></a><span data-ttu-id="f6ac9-110">I criteri di SharePoint Online si applicano anche a OneDrive for Business?</span><span class="sxs-lookup"><span data-stu-id="f6ac9-110">Does a SharePoint Online policy also apply to OneDrive for Business?</span></span>

<span data-ttu-id="f6ac9-111">Sì.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-111">Yes.</span></span> <span data-ttu-id="f6ac9-112">I criteri di SharePoint Online si applicano anche a OneDrive for Business.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-112">A SharePoint Online policy also applies to OneDrive for Business.</span></span>


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a><span data-ttu-id="f6ac9-113">Perché non è possibile impostare criteri nelle app client, ad esempio Word o Outlook?</span><span class="sxs-lookup"><span data-stu-id="f6ac9-113">Why can’t I set a policy on client apps, like Word or Outlook?</span></span>

<span data-ttu-id="f6ac9-114">I criteri di accesso condizionale impostano i requisiti per l'accesso a un servizio</span><span class="sxs-lookup"><span data-stu-id="f6ac9-114">A conditional access policy sets requirements for accessing a service.</span></span> <span data-ttu-id="f6ac9-115">e vengono applicati nel momento in cui viene eseguita l'autenticazione al servizio.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-115">It's enforced when authentication to that service occurs.</span></span> <span data-ttu-id="f6ac9-116">I criteri non vengono impostati direttamente su un'applicazione client,</span><span class="sxs-lookup"><span data-stu-id="f6ac9-116">The policy is not set directly on a client application.</span></span> <span data-ttu-id="f6ac9-117">ma vengono applicati quando un client chiama un servizio.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-117">Instead, it is applied when a client calls a service.</span></span> <span data-ttu-id="f6ac9-118">I criteri impostati in SharePoint, ad esempio, vengono applicati ai client che chiamano SharePoint</span><span class="sxs-lookup"><span data-stu-id="f6ac9-118">For example, a policy set on SharePoint applies to clients calling SharePoint.</span></span> <span data-ttu-id="f6ac9-119">e i criteri impostati in Exchange vengono applicati ad Outlook.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-119">A policy set on Exchange applies to Outlook.</span></span>

## <a name="does-a-conditional-access-policy-apply-to-service-accounts"></a><span data-ttu-id="f6ac9-120">Un criterio di accesso condizionale è applicabile agli account del servizio?</span><span class="sxs-lookup"><span data-stu-id="f6ac9-120">Does a conditional access policy apply to service accounts?</span></span>

<span data-ttu-id="f6ac9-121">I criteri di accesso condizionale vengono applicati a tutti gli account utente,</span><span class="sxs-lookup"><span data-stu-id="f6ac9-121">Conditional access policies apply to all user accounts.</span></span> <span data-ttu-id="f6ac9-122">inclusi gli account utente usati come account del servizio.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-122">This includes user accounts that are used as service accounts.</span></span> <span data-ttu-id="f6ac9-123">In molti casi, un account del servizio in esecuzione automatica non è in grado di soddisfare i criteri di accesso condizionale.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-123">Often, a service account that runs unattended can't satisfy the requirements of a conditional access policy.</span></span> <span data-ttu-id="f6ac9-124">È possibile, ad esempio, che sia richiesta l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-124">For example, multi-factor authentication might be required.</span></span> <span data-ttu-id="f6ac9-125">Gli account del servizio possono essere esclusi dai criteri usando le impostazioni di gestione dei criteri di accesso condizionale.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-125">Service accounts can be excluded from a policy by using conditional access policy management settings.</span></span> 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a><span data-ttu-id="f6ac9-126">Sono disponibili API Graph per configurare i criteri di accesso condizionale?</span><span class="sxs-lookup"><span data-stu-id="f6ac9-126">Are Graph APIs available for configuring conditional access policies?</span></span>

<span data-ttu-id="f6ac9-127">Attualmente no.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-127">Currently, no.</span></span> 

## <a name="what-is-the-default-exclusion-policy-for-unsupported-device-platforms"></a><span data-ttu-id="f6ac9-128">Quali sono i criteri di esclusione predefiniti per le piattaforme per dispositivi non supportate?</span><span class="sxs-lookup"><span data-stu-id="f6ac9-128">What is the default exclusion policy for unsupported device platforms?</span></span>

<span data-ttu-id="f6ac9-129">Attualmente i criteri di accesso condizionale sono applicati in modo selettivo per gli utenti che usano dispositivi iOS e Android.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-129">Currently, conditional access policies are selectively enforced on users of iOS and Android devices.</span></span> <span data-ttu-id="f6ac9-130">Per impostazione predefinita, i criteri di accesso condizionale per dispositivi iOS e Android non incidono sulle applicazioni in altre piattaforme per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-130">Applications on other device platforms are, by default, not affected by the conditional access policy for iOS and Android devices.</span></span> <span data-ttu-id="f6ac9-131">Un amministratore tenant può decidere di ignorare i criteri globali per disabilitare l'accesso per gli utenti su piattaforme non supportate.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-131">A tenant admin can choose to override the global policy to disallow access to users on platforms that are not supported.</span></span>


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a><span data-ttu-id="f6ac9-132">Come funzionano i criteri di accesso condizionale per Microsoft Teams?</span><span class="sxs-lookup"><span data-stu-id="f6ac9-132">How do conditional access policies work for Microsoft Teams?</span></span>  

<span data-ttu-id="f6ac9-133">Microsoft Teams si basa principalmente su Exchange Online e SharePoint Online per gli scenari di produttività di base, come riunioni, calendari e condivisione di file.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-133">Microsoft Teams relies heavily on Exchange Online and SharePoint Online for core productivity scenarios, like meetings, calendars, and file sharing.</span></span> <span data-ttu-id="f6ac9-134">I criteri di accesso condizionale impostati per queste app cloud si applicano a Microsoft Teams quando un utente esegue l'accesso.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-134">Conditional access policies that are set for these cloud apps apply to Microsoft Teams when a user signs in.</span></span>

<span data-ttu-id="f6ac9-135">Microsoft Teams è supportato anche separatamente come app cloud nei criteri di accesso condizionale di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-135">Microsoft Teams also is supported separately as a cloud app in Azure Active Directory conditional access policies.</span></span> <span data-ttu-id="f6ac9-136">I criteri dell'autorità di certificazione impostati per un'app cloud si applicano a Microsoft Teams quando un utente esegue l'accesso.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-136">Certificate authority policies that are set for a cloud app apply to Microsoft Teams when a user signs in.</span></span>

<span data-ttu-id="f6ac9-137">I client desktop di Microsoft Teams per Windows e Mac supportano l'autenticazione moderna.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-137">Microsoft Teams desktop clients for Windows and Mac support modern authentication.</span></span> <span data-ttu-id="f6ac9-138">Con l'autenticazione moderna, l'accesso basato su Azure Active Directory Authentication Library (ADAL) viene integrato in applicazioni client Microsoft Office su più piattaforme.</span><span class="sxs-lookup"><span data-stu-id="f6ac9-138">Modern authentication brings sign-in based on the Azure Active Directory Authentication Library (ADAL) to Microsoft Office client applications across platforms.</span></span> 