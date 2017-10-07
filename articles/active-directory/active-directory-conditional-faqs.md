---
title: Active Directory l'accesso condizionale FAQ aaaAzure | Documenti Microsoft
description: Ottenere risposte toofrequently domande frequenti sull'accesso condizionale in Azure Active Directory.
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
ms.openlocfilehash: d23acbb01217d7e9717d1a43de1b46a929404118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a><span data-ttu-id="b0bae-103">Domande frequenti sull'accesso condizionale di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0bae-103">Azure Active Directory conditional access FAQs</span></span>

## <a name="which-applications-work-with-conditional-access-policies"></a><span data-ttu-id="b0bae-104">Quali applicazioni funzionano con i criteri di accesso condizionale?</span><span class="sxs-lookup"><span data-stu-id="b0bae-104">Which applications work with conditional access policies?</span></span>

<span data-ttu-id="b0bae-105">Per informazioni sulle applicazioni che usano i criteri di accesso condizionale, vedere [Applicazioni e browser che usano regole di accesso condizionale in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span><span class="sxs-lookup"><span data-stu-id="b0bae-105">For information about applications that work with conditional access policies, see [Applications and browsers that use conditional access rules in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span></span>

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a><span data-ttu-id="b0bae-106">I criteri di accesso condizionale vengono applicati a Collaborazione B2B e agli utenti guest?</span><span class="sxs-lookup"><span data-stu-id="b0bae-106">Are conditional access policies enforced for B2B collaboration and guest users?</span></span>

<span data-ttu-id="b0bae-107">I criteri vengono applicati agli utenti di Collaborazione business-to-business (B2B).</span><span class="sxs-lookup"><span data-stu-id="b0bae-107">Policies are enforced for business-to-business (B2B) collaboration users.</span></span> <span data-ttu-id="b0bae-108">Tuttavia, in alcuni casi, un utente potrebbe non essere i requisiti dei criteri hello toosatisfy in grado di.</span><span class="sxs-lookup"><span data-stu-id="b0bae-108">However, in some cases, a user might not be able toosatisfy hello policy requirements.</span></span> <span data-ttu-id="b0bae-109">È possibile, ad esempio, che l'organizzazione di un utente guest non supporti l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="b0bae-109">For example, a guest user's organization might not support multi-factor authentication.</span></span> 



## <a name="does-a-sharepoint-online-policy-also-apply-tooonedrive-for-business"></a><span data-ttu-id="b0bae-110">Un criterio di SharePoint Online anche applica tooOneDrive for Business?</span><span class="sxs-lookup"><span data-stu-id="b0bae-110">Does a SharePoint Online policy also apply tooOneDrive for Business?</span></span>

<span data-ttu-id="b0bae-111">Sì.</span><span class="sxs-lookup"><span data-stu-id="b0bae-111">Yes.</span></span> <span data-ttu-id="b0bae-112">Un criterio di SharePoint Online tooOneDrive si applica anche per le aziende.</span><span class="sxs-lookup"><span data-stu-id="b0bae-112">A SharePoint Online policy also applies tooOneDrive for Business.</span></span>


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a><span data-ttu-id="b0bae-113">Perché non è possibile impostare criteri nelle app client, ad esempio Word o Outlook?</span><span class="sxs-lookup"><span data-stu-id="b0bae-113">Why can’t I set a policy on client apps, like Word or Outlook?</span></span>

<span data-ttu-id="b0bae-114">I criteri di accesso condizionale impostano i requisiti per l'accesso a un servizio</span><span class="sxs-lookup"><span data-stu-id="b0bae-114">A conditional access policy sets requirements for accessing a service.</span></span> <span data-ttu-id="b0bae-115">Viene applicato quando si verifica servizio toothat di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="b0bae-115">It's enforced when authentication toothat service occurs.</span></span> <span data-ttu-id="b0bae-116">criteri di Hello non sono impostato direttamente su un'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="b0bae-116">hello policy is not set directly on a client application.</span></span> <span data-ttu-id="b0bae-117">ma vengono applicati quando un client chiama un servizio.</span><span class="sxs-lookup"><span data-stu-id="b0bae-117">Instead, it is applied when a client calls a service.</span></span> <span data-ttu-id="b0bae-118">Ad esempio, i criteri impostati in SharePoint applicano tooclients chiamata SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b0bae-118">For example, a policy set on SharePoint applies tooclients calling SharePoint.</span></span> <span data-ttu-id="b0bae-119">Un criterio impostato su Exchange applica tooOutlook.</span><span class="sxs-lookup"><span data-stu-id="b0bae-119">A policy set on Exchange applies tooOutlook.</span></span>

## <a name="does-a-conditional-access-policy-apply-tooservice-accounts"></a><span data-ttu-id="b0bae-120">Criteri di accesso condizionale applica tooservice account?</span><span class="sxs-lookup"><span data-stu-id="b0bae-120">Does a conditional access policy apply tooservice accounts?</span></span>

<span data-ttu-id="b0bae-121">Criteri di accesso condizionale si applicano gli account utente tooall.</span><span class="sxs-lookup"><span data-stu-id="b0bae-121">Conditional access policies apply tooall user accounts.</span></span> <span data-ttu-id="b0bae-122">inclusi gli account utente usati come account del servizio.</span><span class="sxs-lookup"><span data-stu-id="b0bae-122">This includes user accounts that are used as service accounts.</span></span> <span data-ttu-id="b0bae-123">Spesso, un account del servizio che esegue automatico non è possibile soddisfare i requisiti di hello di criteri di accesso condizionale.</span><span class="sxs-lookup"><span data-stu-id="b0bae-123">Often, a service account that runs unattended can't satisfy hello requirements of a conditional access policy.</span></span> <span data-ttu-id="b0bae-124">È possibile, ad esempio, che sia richiesta l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="b0bae-124">For example, multi-factor authentication might be required.</span></span> <span data-ttu-id="b0bae-125">Gli account del servizio possono essere esclusi dai criteri usando le impostazioni di gestione dei criteri di accesso condizionale.</span><span class="sxs-lookup"><span data-stu-id="b0bae-125">Service accounts can be excluded from a policy by using conditional access policy management settings.</span></span> 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a><span data-ttu-id="b0bae-126">Sono disponibili API Graph per configurare i criteri di accesso condizionale?</span><span class="sxs-lookup"><span data-stu-id="b0bae-126">Are Graph APIs available for configuring conditional access policies?</span></span>

<span data-ttu-id="b0bae-127">Attualmente no.</span><span class="sxs-lookup"><span data-stu-id="b0bae-127">Currently, no.</span></span> 

## <a name="what-is-hello-default-exclusion-policy-for-unsupported-device-platforms"></a><span data-ttu-id="b0bae-128">Novità di criteri di esclusione predefiniti hello per le piattaforme di dispositivi non supportate?</span><span class="sxs-lookup"><span data-stu-id="b0bae-128">What is hello default exclusion policy for unsupported device platforms?</span></span>

<span data-ttu-id="b0bae-129">Attualmente i criteri di accesso condizionale sono applicati in modo selettivo per gli utenti che usano dispositivi iOS e Android.</span><span class="sxs-lookup"><span data-stu-id="b0bae-129">Currently, conditional access policies are selectively enforced on users of iOS and Android devices.</span></span> <span data-ttu-id="b0bae-130">Le applicazioni su altre piattaforme di dispositivo, per impostazione predefinita, non sono interessate dal criterio di accesso condizionale hello per dispositivi iOS e Android.</span><span class="sxs-lookup"><span data-stu-id="b0bae-130">Applications on other device platforms are, by default, not affected by hello conditional access policy for iOS and Android devices.</span></span> <span data-ttu-id="b0bae-131">Un amministratore tenant può scegliere toooverride hello criteri globali toodisallow accesso toousers su piattaforme che non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="b0bae-131">A tenant admin can choose toooverride hello global policy toodisallow access toousers on platforms that are not supported.</span></span>


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a><span data-ttu-id="b0bae-132">Come funzionano i criteri di accesso condizionale per Microsoft Teams?</span><span class="sxs-lookup"><span data-stu-id="b0bae-132">How do conditional access policies work for Microsoft Teams?</span></span>  

<span data-ttu-id="b0bae-133">Microsoft Teams si basa principalmente su Exchange Online e SharePoint Online per gli scenari di produttività di base, come riunioni, calendari e condivisione di file.</span><span class="sxs-lookup"><span data-stu-id="b0bae-133">Microsoft Teams relies heavily on Exchange Online and SharePoint Online for core productivity scenarios, like meetings, calendars, and file sharing.</span></span> <span data-ttu-id="b0bae-134">Criteri di accesso condizionale impostati per queste App cloud applicano tooMicrosoft team quando un utente accede.</span><span class="sxs-lookup"><span data-stu-id="b0bae-134">Conditional access policies that are set for these cloud apps apply tooMicrosoft Teams when a user signs in.</span></span>

<span data-ttu-id="b0bae-135">Microsoft Teams è supportato anche separatamente come app cloud nei criteri di accesso condizionale di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b0bae-135">Microsoft Teams also is supported separately as a cloud app in Azure Active Directory conditional access policies.</span></span> <span data-ttu-id="b0bae-136">I criteri di Autorità certificato impostati per un'applicazione cloud applicano tooMicrosoft team quando un utente accede.</span><span class="sxs-lookup"><span data-stu-id="b0bae-136">Certificate authority policies that are set for a cloud app apply tooMicrosoft Teams when a user signs in.</span></span>

<span data-ttu-id="b0bae-137">I client desktop di Microsoft Teams per Windows e Mac supportano l'autenticazione moderna.</span><span class="sxs-lookup"><span data-stu-id="b0bae-137">Microsoft Teams desktop clients for Windows and Mac support modern authentication.</span></span> <span data-ttu-id="b0bae-138">L'autenticazione moderna consente l'accesso in base alle applicazioni client di hello Azure Active Directory Authentication Library (ADAL) tooMicrosoft Office su piattaforme diverse.</span><span class="sxs-lookup"><span data-stu-id="b0bae-138">Modern authentication brings sign-in based on hello Azure Active Directory Authentication Library (ADAL) tooMicrosoft Office client applications across platforms.</span></span> 
