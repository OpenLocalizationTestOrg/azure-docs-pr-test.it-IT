---
title: Active Directory PoC Playbook ingredienti aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: 0a7f5cd659b9d62ac86e3c27e5727294d481f4a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a><span data-ttu-id="7dd3b-104">Ingredienti del playbook dei modelli di verifica di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7dd3b-104">Azure Active Directory Proof of Concept Playbook Ingredients</span></span> 

## <a name="theme"></a><span data-ttu-id="7dd3b-105">Tema</span><span class="sxs-lookup"><span data-stu-id="7dd3b-105">Theme</span></span>
<span data-ttu-id="7dd3b-106">Azure AD fornisce soluzioni di identità e degli accessi in più aree in enterprise hello.</span><span class="sxs-lookup"><span data-stu-id="7dd3b-106">Azure AD provides identity and access solutions across multiple areas in hello enterprise.</span></span> <span data-ttu-id="7dd3b-107">Si classifica gli scenari di hello in hello seguenti aree:</span><span class="sxs-lookup"><span data-stu-id="7dd3b-107">We classify hello scenarios in hello following areas:</span></span> 

* [<span data-ttu-id="7dd3b-108">Molte app, una sola identità</span><span class="sxs-lookup"><span data-stu-id="7dd3b-108">Lots of apps, one identity</span></span>](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [<span data-ttu-id="7dd3b-109">Aumentare la sicurezza</span><span class="sxs-lookup"><span data-stu-id="7dd3b-109">Increase your security</span></span>](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [<span data-ttu-id="7dd3b-110">Scalabilità self-service</span><span class="sxs-lookup"><span data-stu-id="7dd3b-110">Scale with Self Service</span></span>](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

<span data-ttu-id="7dd3b-111">Definisce un tema tooframe hello che POC consente gli sforzi hello toofocus definita adatta alle esigenze agli obiettivi aziendali, che spesso sono trigger hello di interesse hello in un modello di prova in primo luogo hello.</span><span class="sxs-lookup"><span data-stu-id="7dd3b-111">Defining a theme tooframe hello PoC helps toofocus hello efforts that resonates with business goals, which oftentimes are hello triggers of hello interest in a proof of concept in hello first place.</span></span> 

## <a name="environment"></a><span data-ttu-id="7dd3b-112">Environment</span><span class="sxs-lookup"><span data-stu-id="7dd3b-112">Environment</span></span>

<span data-ttu-id="7dd3b-113">È importante toodetermine i dettagli di hello dell'ambiente hello in cui si installerà hello PoC.</span><span class="sxs-lookup"><span data-stu-id="7dd3b-113">It is important toodetermine hello details of hello environment where you will deliver hello PoC.</span></span> <span data-ttu-id="7dd3b-114">In teoria è possibile creare su di esso dopo hello che POC viene completata.</span><span class="sxs-lookup"><span data-stu-id="7dd3b-114">Ideally you can build upon it after hello PoC is completed.</span></span> <span data-ttu-id="7dd3b-115">ambiente di destinazione Hello è essenziale e si deve trovare hello giusto equilibrio tra rendendo l'oggetto e reale come possibili e overhead di hello di vincoli o considerazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="7dd3b-115">hello target environment is crucial and you should find hello right balance between making it as real as possible and hello overhead of constraints or extra considerations.</span></span> <span data-ttu-id="7dd3b-116">ambienti Hello per PoCs sono:</span><span class="sxs-lookup"><span data-stu-id="7dd3b-116">hello typical environments for PoCs are:</span></span>
* <span data-ttu-id="7dd3b-117">**Produzione:** scenari hello verrà implementati nell'ambiente in tempo reale e già stati distribuiti servizi Cloud Microsoft (soluzione di produzione AD, Office 365, Azure AD/SSO tenant).</span><span class="sxs-lookup"><span data-stu-id="7dd3b-117">**Production:** hello scenarios will be implemented in your live environment and already deployed Microsoft Cloud services (production AD, Office 365, Azure AD tenant/SSO solution).</span></span> 
* <span data-ttu-id="7dd3b-118">**Test accettazione utente / ambiente di sviluppo:** è disponibile un’infrastruttura di test (AD parallelo e potenziale tenant di Azure AD/soluzione SSO) con dati di test analoghi alla produzione.</span><span class="sxs-lookup"><span data-stu-id="7dd3b-118">**User Acceptance Test (UAT)/Dev environment:** You have test infrastructure (parallel AD and potentially Azure AD tenant/SSO solution) with test data that resembles production.</span></span> <span data-ttu-id="7dd3b-119">In genere, ambiente di test hello è condiviso tra più progetti in enterprise hello.</span><span class="sxs-lookup"><span data-stu-id="7dd3b-119">Typically, hello test environment is shared across multiple projects in hello enterprise.</span></span>

<span data-ttu-id="7dd3b-120">Nella maggior parte dei casi, gli scenari in questa guida sono additivi in natura.</span><span class="sxs-lookup"><span data-stu-id="7dd3b-120">Most scenarios in this guide are additive in nature.</span></span> <span data-ttu-id="7dd3b-121">Di conseguenza, possano essere distribuiti nel tenant di produzione hello senza modificare gli utenti all'esterno di hello in ambiente di prova.</span><span class="sxs-lookup"><span data-stu-id="7dd3b-121">As a result, they can be deployed in hello production tenant without affecting users outside hello PoC.</span></span> <span data-ttu-id="7dd3b-122">In questo documento, verranno esclusi gli scenari che avrebbero un impatto globale a livello di tenant.</span><span class="sxs-lookup"><span data-stu-id="7dd3b-122">Throughout this document, we will be calling out which scenarios would have tenant-wide effect.</span></span> <span data-ttu-id="7dd3b-123">In questi casi, è possibile tooconsider un ambiente non di produzione.</span><span class="sxs-lookup"><span data-stu-id="7dd3b-123">In those cases, you might want tooconsider a non-production environment.</span></span> 


## <a name="target-users"></a><span data-ttu-id="7dd3b-124">Utenti di destinazione</span><span class="sxs-lookup"><span data-stu-id="7dd3b-124">Target Users</span></span>

<span data-ttu-id="7dd3b-125">È importante toodetermine hello riferimento impostato per gli utenti che verranno esercitare scenari hello, in particolar modo quando ambiente hello produzione o test.</span><span class="sxs-lookup"><span data-stu-id="7dd3b-125">It is important toodetermine hello target set of users that will exercise hello scenarios, especially when hello environment is production or test.</span></span> <span data-ttu-id="7dd3b-126">categorie di Hello degli utenti di destinazione di prova sono:</span><span class="sxs-lookup"><span data-stu-id="7dd3b-126">hello categories of target users for PoC are:</span></span>
* <span data-ttu-id="7dd3b-127">**Utenti della fase pilota:** utenti reali nell'ambiente di hello che utilizzerà la soluzione hello con hello l'account utilizzato per la loro tooday giorno processo funzioni</span><span class="sxs-lookup"><span data-stu-id="7dd3b-127">**Pilot Users:** Real users in hello environment that will be using hello solution with hello account they use for their day tooday job functions</span></span>
* <span data-ttu-id="7dd3b-128">**Gli utenti di test:** account creati in hello ambiente di Test</span><span class="sxs-lookup"><span data-stu-id="7dd3b-128">**Test Users:** Test accounts created in hello environment</span></span> 

<span data-ttu-id="7dd3b-129">La maggior parte degli scenari contemplati in questa guida può essere usata dagli utenti pilota.</span><span class="sxs-lookup"><span data-stu-id="7dd3b-129">Most scenarios in this guide can be exercised by pilot users.</span></span> <span data-ttu-id="7dd3b-130">In questo documento verranno escluse se necessario le considerazioni in merito agli utenti di destinazione.</span><span class="sxs-lookup"><span data-stu-id="7dd3b-130">Throughout this document, we will be calling out target user considerations if needed.</span></span>


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]