---
title: Limitazioni di Collaborazione B2B di Azure Active Directory | Documentazione Microsoft
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
ms.openlocfilehash: 581e5d1fb5fb08d0dc89ed2c85edcb5f0005650b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a><span data-ttu-id="2de08-103">Limitazioni di Collaborazione B2B di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2de08-103">Limitations of Azure AD B2B collaboration</span></span>
<span data-ttu-id="2de08-104">Collaborazione B2B di Azure Active Directory (Azure AD) è soggetta alle limitazioni descritte in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="2de08-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject to the limitations described in this article.</span></span>

## <a name="possible-double-multi-factor-authentication"></a><span data-ttu-id="2de08-105">Possibile autenticazione a più fattori doppia</span><span class="sxs-lookup"><span data-stu-id="2de08-105">Possible double multi-factor authentication</span></span>
<span data-ttu-id="2de08-106">Con B2B di Azure AD è possibile imporre l'autenticazione a più fattori dell'organizzazione delle risorse (l'organizzazione che invita).</span><span class="sxs-lookup"><span data-stu-id="2de08-106">With Azure AD B2B, you can enforce multi-factor authentication at the resource organization (the inviting organization).</span></span> <span data-ttu-id="2de08-107">I motivi di questo approccio vengono descritti nel dettaglio in [Accesso condizionale per gli utenti di Collaborazione B2B](active-directory-b2b-mfa-instructions.md).</span><span class="sxs-lookup"><span data-stu-id="2de08-107">The reasons for this approach are detailed in [Conditional access for B2B collaboration users](active-directory-b2b-mfa-instructions.md).</span></span> <span data-ttu-id="2de08-108">Se un partner ha già configurato e applicato l'autenticazione a più fattori, è possibile che i rispettivi utenti debbano eseguire l'autenticazione una volta nella propria organizzazione e di nuovo nell'organizzazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="2de08-108">If a partner already has multi-factor authentication set up and enforced, their users might have to perform the authentication once in their home organization and then again in yours.</span></span>

## <a name="instant-on"></a><span data-ttu-id="2de08-109">Immediatezza</span><span class="sxs-lookup"><span data-stu-id="2de08-109">Instant-on</span></span>
<span data-ttu-id="2de08-110">Nei flussi di Collaborazione B2B gli utenti vengono aggiunti alla directory e aggiornati in modo dinamico durante il riscatto dell'invito, l'assegnazione di app e così via.</span><span class="sxs-lookup"><span data-stu-id="2de08-110">In the B2B collaboration flows, we add users to the directory and dynamically update them during invitation redemption, app assignment, and so on.</span></span> <span data-ttu-id="2de08-111">Le operazioni di aggiornamento e scrittura vengono eseguite generalmente in un'istanza della directory e devono essere replicate in tutte le istanze.</span><span class="sxs-lookup"><span data-stu-id="2de08-111">The updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span></span> <span data-ttu-id="2de08-112">La replica viene completata quando tutte le istanze sono state aggiornate.</span><span class="sxs-lookup"><span data-stu-id="2de08-112">Replication is completed once all instances are updated.</span></span> <span data-ttu-id="2de08-113">In alcuni casi, quando un oggetto viene scritto o aggiornato in un'istanza e la chiamata per il recupero dell'oggetto viene effettuata a un'altra istanza, è possibile che si verifichino latenze della replica.</span><span class="sxs-lookup"><span data-stu-id="2de08-113">Sometimes when the object is written or updated in one instance and the call to retrieve this object is to another instance, replication latencies can occur.</span></span> <span data-ttu-id="2de08-114">In tal caso, aggiornare o riprovare.</span><span class="sxs-lookup"><span data-stu-id="2de08-114">If that happens, refresh or retry to help.</span></span> <span data-ttu-id="2de08-115">Se si sta scrivendo un'app usando l'API, è consigliabile riprovare, interrompendo temporaneamente, per risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="2de08-115">If you are writing an app using our API, then retries with some back-off is a good, defensive practice to alleviate this issue.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2de08-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2de08-116">Next steps</span></span>

<span data-ttu-id="2de08-117">Vedere gli altri articoli su Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="2de08-117">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="2de08-118">Che cos'è Azure AD B2B Collaboration?</span><span class="sxs-lookup"><span data-stu-id="2de08-118">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="2de08-119">Proprietà dell'utente di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="2de08-119">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="2de08-120">Aggiunta di un utente di Collaborazione B2B a un ruolo</span><span class="sxs-lookup"><span data-stu-id="2de08-120">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="2de08-121">Delegare gli inviti a Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="2de08-121">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="2de08-122">Gruppi dinamici e Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="2de08-122">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="2de08-123">Codici ed esempi di PowerShell per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="2de08-123">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="2de08-124">Configurare app SaaS per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="2de08-124">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="2de08-125">Token utente in Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="2de08-125">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="2de08-126">Mapping delle attestazioni utente per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="2de08-126">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="2de08-127">Condivisione esterna di Office 365</span><span class="sxs-lookup"><span data-stu-id="2de08-127">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
