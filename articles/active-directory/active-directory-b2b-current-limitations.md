---
title: aaaLimitations di collaborazione B2B di Azure Active Directory | Documenti Microsoft
description: Limitazioni correnti di Collaborazione B2B di Azure Active Directory
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 322081f32fbacfe67ee1300993c7df1870e498bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a><span data-ttu-id="dc6e9-103">Limitazioni di Collaborazione B2B di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc6e9-103">Limitations of Azure AD B2B collaboration</span></span>
<span data-ttu-id="dc6e9-104">Collaborazione B2B di Active Directory (Azure AD) di Azure è attualmente limitazioni toohello soggetto descritte in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="dc6e9-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject toohello limitations described in this article.</span></span>

## <a name="possible-double-multi-factor-authentication"></a><span data-ttu-id="dc6e9-105">Possibile autenticazione a più fattori doppia</span><span class="sxs-lookup"><span data-stu-id="dc6e9-105">Possible double multi-factor authentication</span></span>
<span data-ttu-id="dc6e9-106">Con Azure AD B2B, è possibile applicare multi-factor authentication all'organizzazione risorse hello (Buongiorno si invitano organizzazione).</span><span class="sxs-lookup"><span data-stu-id="dc6e9-106">With Azure AD B2B, you can enforce multi-factor authentication at hello resource organization (hello inviting organization).</span></span> <span data-ttu-id="dc6e9-107">vengono descritti in dettaglio i motivi Hello per questo approccio [accesso condizionale per gli utenti di collaborazione B2B](active-directory-b2b-mfa-instructions.md).</span><span class="sxs-lookup"><span data-stu-id="dc6e9-107">hello reasons for this approach are detailed in [Conditional access for B2B collaboration users](active-directory-b2b-mfa-instructions.md).</span></span> <span data-ttu-id="dc6e9-108">Se un partner dispone già di multi-factor authentication consente di impostare e applicati, gli utenti necessario autenticazione hello tooperform una volta all'interno dell'organizzazione principale e quindi nuovamente in quelle in uso.</span><span class="sxs-lookup"><span data-stu-id="dc6e9-108">If a partner already has multi-factor authentication set up and enforced, their users might have tooperform hello authentication once in their home organization and then again in yours.</span></span>

## <a name="instant-on"></a><span data-ttu-id="dc6e9-109">Immediatezza</span><span class="sxs-lookup"><span data-stu-id="dc6e9-109">Instant-on</span></span>
<span data-ttu-id="dc6e9-110">Nei flussi di collaborazione B2B di hello, aggiungiamo directory toohello users e aggiornarli in modo dinamico durante il riscatto di invito, assegnazione di app e così via.</span><span class="sxs-lookup"><span data-stu-id="dc6e9-110">In hello B2B collaboration flows, we add users toohello directory and dynamically update them during invitation redemption, app assignment, and so on.</span></span> <span data-ttu-id="dc6e9-111">gli aggiornamenti di Hello e scritture in genere avvengono nell'istanza di una directory e devono essere replicate in tutte le istanze.</span><span class="sxs-lookup"><span data-stu-id="dc6e9-111">hello updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span></span> <span data-ttu-id="dc6e9-112">La replica viene completata quando tutte le istanze sono state aggiornate.</span><span class="sxs-lookup"><span data-stu-id="dc6e9-112">Replication is completed once all instances are updated.</span></span> <span data-ttu-id="dc6e9-113">A volte quando oggetto hello viene scritto o aggiornato in un'istanza e hello chiamare tooretrieve questo oggetto è tooanother istanza, possono verificarsi le latenze di replica.</span><span class="sxs-lookup"><span data-stu-id="dc6e9-113">Sometimes when hello object is written or updated in one instance and hello call tooretrieve this object is tooanother instance, replication latencies can occur.</span></span> <span data-ttu-id="dc6e9-114">In tal caso, aggiornare o riprovare toohelp.</span><span class="sxs-lookup"><span data-stu-id="dc6e9-114">If that happens, refresh or retry toohelp.</span></span> <span data-ttu-id="dc6e9-115">Se si scrive un'app usando l'API, quindi tentativi con backoff è un tooalleviate difensivo, buona pratica questo problema.</span><span class="sxs-lookup"><span data-stu-id="dc6e9-115">If you are writing an app using our API, then retries with some back-off is a good, defensive practice tooalleviate this issue.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc6e9-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dc6e9-116">Next steps</span></span>

<span data-ttu-id="dc6e9-117">Vedere gli altri articoli su Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="dc6e9-117">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="dc6e9-118">Che cos'è Azure AD B2B Collaboration?</span><span class="sxs-lookup"><span data-stu-id="dc6e9-118">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="dc6e9-119">Proprietà dell'utente di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="dc6e9-119">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="dc6e9-120">Aggiunta di un ruolo di tooa utente collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="dc6e9-120">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="dc6e9-121">Delegare gli inviti a Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="dc6e9-121">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="dc6e9-122">Gruppi dinamici e Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="dc6e9-122">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="dc6e9-123">Codici ed esempi di PowerShell per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="dc6e9-123">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="dc6e9-124">Configurare app SaaS per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="dc6e9-124">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="dc6e9-125">Token utente in Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="dc6e9-125">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="dc6e9-126">Mapping delle attestazioni utente per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="dc6e9-126">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="dc6e9-127">Condivisione esterna di Office 365</span><span class="sxs-lookup"><span data-stu-id="dc6e9-127">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
