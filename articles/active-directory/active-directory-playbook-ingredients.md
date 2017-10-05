---
title: Ingredienti del playbook dei modelli di verifica di Azure Active Directory | Microsoft Docs
description: "Esplorare e implementare rapidamente gli scenari di Gestione delle identità e degli accessi"
services: active-directory
keywords: azure active directory, playbook, modello di verifica, PoC
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: d2a0fe280f143d390f5e4ba40e0ebe92d8a4a837
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a><span data-ttu-id="fdcee-104">Ingredienti del playbook dei modelli di verifica di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fdcee-104">Azure Active Directory Proof of Concept Playbook Ingredients</span></span> 

## <a name="theme"></a><span data-ttu-id="fdcee-105">Tema</span><span class="sxs-lookup"><span data-stu-id="fdcee-105">Theme</span></span>
<span data-ttu-id="fdcee-106">Azure AD offre soluzioni per la gestione di identità e accessi in più aree dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="fdcee-106">Azure AD provides identity and access solutions across multiple areas in the enterprise.</span></span> <span data-ttu-id="fdcee-107">Gli scenari vengono classificati in base alle aree seguenti:</span><span class="sxs-lookup"><span data-stu-id="fdcee-107">We classify the scenarios in the following areas:</span></span> 

* [<span data-ttu-id="fdcee-108">Molte app, una sola identità</span><span class="sxs-lookup"><span data-stu-id="fdcee-108">Lots of apps, one identity</span></span>](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [<span data-ttu-id="fdcee-109">Aumentare la sicurezza</span><span class="sxs-lookup"><span data-stu-id="fdcee-109">Increase your security</span></span>](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [<span data-ttu-id="fdcee-110">Scalabilità self-service</span><span class="sxs-lookup"><span data-stu-id="fdcee-110">Scale with Self Service</span></span>](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

<span data-ttu-id="fdcee-111">La definizione di un tema ai fini dell’impostazione di un modello di verifica aiuta a mettere in evidenza gli sforzi necessari per raggiungere gli obiettivi aziendali, che rappresentano spesso il primo motivo di interesse nella creazione di un modello di verifica.</span><span class="sxs-lookup"><span data-stu-id="fdcee-111">Defining a theme to frame the PoC helps to focus the efforts that resonates with business goals, which oftentimes are the triggers of the interest in a proof of concept in the first place.</span></span> 

## <a name="environment"></a><span data-ttu-id="fdcee-112">Environment</span><span class="sxs-lookup"><span data-stu-id="fdcee-112">Environment</span></span>

<span data-ttu-id="fdcee-113">È importante determinare i dettagli dell'ambiente in cui verrà distribuito il modello di verifica</span><span class="sxs-lookup"><span data-stu-id="fdcee-113">It is important to determine the details of the environment where you will deliver the PoC.</span></span> <span data-ttu-id="fdcee-114">che idealmente, una volta completato, dovrebbe costituire la base su cui costruire l’ambiente.</span><span class="sxs-lookup"><span data-stu-id="fdcee-114">Ideally you can build upon it after the PoC is completed.</span></span> <span data-ttu-id="fdcee-115">L'ambiente di destinazione è fondamentale ed è consigliabile trovare il giusto equilibrio tra l’obiettivo di renderlo il più reale possibile e il numero totale di vincoli o considerazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="fdcee-115">The target environment is crucial and you should find the right balance between making it as real as possible and the overhead of constraints or extra considerations.</span></span> <span data-ttu-id="fdcee-116">Gli ambienti tipici per i modelli di verifica sono:</span><span class="sxs-lookup"><span data-stu-id="fdcee-116">The typical environments for PoCs are:</span></span>
* <span data-ttu-id="fdcee-117">**Produzione:** gli scenari verranno implementati nell'ambiente live e nei servizi Microsoft Cloud già distribuiti (Active Directory di produzione, Office 365, tenant di Azure AD/soluzione SSO).</span><span class="sxs-lookup"><span data-stu-id="fdcee-117">**Production:** The scenarios will be implemented in your live environment and already deployed Microsoft Cloud services (production AD, Office 365, Azure AD tenant/SSO solution).</span></span> 
* <span data-ttu-id="fdcee-118">**Test accettazione utente / ambiente di sviluppo:** è disponibile un’infrastruttura di test (AD parallelo e potenziale tenant di Azure AD/soluzione SSO) con dati di test analoghi alla produzione.</span><span class="sxs-lookup"><span data-stu-id="fdcee-118">**User Acceptance Test (UAT)/Dev environment:** You have test infrastructure (parallel AD and potentially Azure AD tenant/SSO solution) with test data that resembles production.</span></span> <span data-ttu-id="fdcee-119">In genere, l'ambiente di test viene condiviso tra più progetti dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="fdcee-119">Typically, the test environment is shared across multiple projects in the enterprise.</span></span>

<span data-ttu-id="fdcee-120">Nella maggior parte dei casi, gli scenari in questa guida sono additivi in natura.</span><span class="sxs-lookup"><span data-stu-id="fdcee-120">Most scenarios in this guide are additive in nature.</span></span> <span data-ttu-id="fdcee-121">Pertanto, possono essere distribuiti nel tenant di produzione senza impatto sugli utenti esterni al modello di verifica.</span><span class="sxs-lookup"><span data-stu-id="fdcee-121">As a result, they can be deployed in the production tenant without affecting users outside the PoC.</span></span> <span data-ttu-id="fdcee-122">In questo documento, verranno esclusi gli scenari che avrebbero un impatto globale a livello di tenant.</span><span class="sxs-lookup"><span data-stu-id="fdcee-122">Throughout this document, we will be calling out which scenarios would have tenant-wide effect.</span></span> <span data-ttu-id="fdcee-123">In questi casi, è consigliabile prendere in considerazione un ambiente non di produzione.</span><span class="sxs-lookup"><span data-stu-id="fdcee-123">In those cases, you might want to consider a non-production environment.</span></span> 


## <a name="target-users"></a><span data-ttu-id="fdcee-124">Utenti di destinazione</span><span class="sxs-lookup"><span data-stu-id="fdcee-124">Target Users</span></span>

<span data-ttu-id="fdcee-125">È importante determinare il set di destinazione degli utenti che faranno pratica nell’ambito di questi scenari, in particolar modo quando l'ambiente è di produzione o di test.</span><span class="sxs-lookup"><span data-stu-id="fdcee-125">It is important to determine the target set of users that will exercise the scenarios, especially when the environment is production or test.</span></span> <span data-ttu-id="fdcee-126">Le categorie di utenti di destinazione per i modelli di verifica sono:</span><span class="sxs-lookup"><span data-stu-id="fdcee-126">The categories of target users for PoC are:</span></span>
* <span data-ttu-id="fdcee-127">**Utenti pilota:** utenti reali nell'ambiente che utilizzeranno la soluzione con l'account usato per le normali attività quotidiane</span><span class="sxs-lookup"><span data-stu-id="fdcee-127">**Pilot Users:** Real users in the environment that will be using the solution with the account they use for their day to day job functions</span></span>
* <span data-ttu-id="fdcee-128">**Utenti test:** account di prova creati nell'ambiente</span><span class="sxs-lookup"><span data-stu-id="fdcee-128">**Test Users:** Test accounts created in the environment</span></span> 

<span data-ttu-id="fdcee-129">La maggior parte degli scenari contemplati in questa guida può essere usata dagli utenti pilota.</span><span class="sxs-lookup"><span data-stu-id="fdcee-129">Most scenarios in this guide can be exercised by pilot users.</span></span> <span data-ttu-id="fdcee-130">In questo documento verranno escluse se necessario le considerazioni in merito agli utenti di destinazione.</span><span class="sxs-lookup"><span data-stu-id="fdcee-130">Throughout this document, we will be calling out target user considerations if needed.</span></span>


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]