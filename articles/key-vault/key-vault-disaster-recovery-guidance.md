---
title: Operazioni da eseguire in caso di interruzione di un servizio Azure con impatto sull'insieme di credenziali delle chiavi di Azure | Microsoft Docs
description: Informazioni sulle operazioni da eseguire in caso di un'interruzione del servizio Azure con impatto sull'insieme di credenziali delle chiavi di Azure.
services: key-vault
documentationcenter: 
author: adamglick
manager: mbaldwin
editor: 
ms.assetid: 19a9af63-3032-447b-9d1a-b0125f384edb
ms.service: key-vault
ms.workload: key-vault
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: sumedhb;aglick
ms.openlocfilehash: 6419d54c54e7d19103419262b79e7a5268b2268c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a><span data-ttu-id="0199f-103">Disponibilità e ridondanza dell'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="0199f-103">Azure Key Vault availability and redundancy</span></span>
<span data-ttu-id="0199f-104">L'insieme di credenziali delle chiavi di Azure dispone di più livelli di ridondanza, per garantire che le chiavi e i segreti rimangano disponibili per l'applicazione anche quando si verificano errori di singoli componenti del servizio.</span><span class="sxs-lookup"><span data-stu-id="0199f-104">Azure Key Vault features multiple layers of redundancy to make sure that your keys and secrets remain available to your application even if individual components of the service fail.</span></span>

<span data-ttu-id="0199f-105">I contenuti dell'insieme di credenziali delle chiavi vengono replicati all'interno dell'area e in un'area secondaria distante almeno 250 chilometri, ma all'interno della stessa area geografica.</span><span class="sxs-lookup"><span data-stu-id="0199f-105">The contents of your key vault are replicated within the region and to a secondary region at least 150 miles away but within the same geography.</span></span> <span data-ttu-id="0199f-106">Questo garantisce un'elevata durabilità delle chiavi e dei segreti.</span><span class="sxs-lookup"><span data-stu-id="0199f-106">This maintains high durability of your keys and secrets.</span></span> <span data-ttu-id="0199f-107">Per informazioni dettagliate su coppie di aree specifiche, vedere il documento [Aree abbinate di Azure](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions).</span><span class="sxs-lookup"><span data-stu-id="0199f-107">See the [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document for details on specific region pairs.</span></span>

<span data-ttu-id="0199f-108">Se si verificano errori di singoli componenti del servizio dell'insieme di credenziali delle chiavi, per gestire la richiesta subentrano componenti alternativi all'interno dell'area in modo che non si verifichi alcuna riduzione delle prestazioni delle funzionalità.</span><span class="sxs-lookup"><span data-stu-id="0199f-108">If individual components within the key vault service fail, alternate components within the region step in to serve your request to make sure that there is no degradation of functionality.</span></span> <span data-ttu-id="0199f-109">A tale scopo, non è necessario alcun intervento</span><span class="sxs-lookup"><span data-stu-id="0199f-109">You do not need to take any action to trigger this.</span></span> <span data-ttu-id="0199f-110">in quanto l'azione viene eseguita automaticamente e in modo trasparente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="0199f-110">It happens automatically and will be transparent to you.</span></span>

<span data-ttu-id="0199f-111">Nella rara eventualità che l'intera area di Azure risulti non disponibile, le richieste eseguite all'insieme di credenziali delle chiavi di tale area vengono indirizzate automaticamente a un'area secondaria (*failover*).</span><span class="sxs-lookup"><span data-stu-id="0199f-111">In the rare event that an entire Azure region is unavailable, the requests that you make of Azure Key Vault in that region are automatically routed (*failed over*) to a secondary region.</span></span> <span data-ttu-id="0199f-112">Quando l'area primaria diventa di nuovo disponibile, le richieste vengono reindirizzate a tale area (*failback*).</span><span class="sxs-lookup"><span data-stu-id="0199f-112">When the primary region is available again, requests are routed back (*failed back*) to the primary region.</span></span> <span data-ttu-id="0199f-113">Anche in questo caso non è richiesta alcuna azione, poiché questa operazione viene eseguita in modo automatico.</span><span class="sxs-lookup"><span data-stu-id="0199f-113">Again, you do not need to take any action because this happens automatically.</span></span>

<span data-ttu-id="0199f-114">Esistono alcune limitazioni che è necessario tenere presenti:</span><span class="sxs-lookup"><span data-stu-id="0199f-114">There are a few caveats to be aware of:</span></span>

* <span data-ttu-id="0199f-115">Nel caso del failover di un'area, il failover del servizio può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="0199f-115">In the event of a region failover, it may take a few minutes for the service to fail over.</span></span> <span data-ttu-id="0199f-116">È possibile che le richieste eseguite durante questo periodo abbiano esito negativo fino al completamento del failover.</span><span class="sxs-lookup"><span data-stu-id="0199f-116">Requests that are made during this time may fail until the failover completes.</span></span>
* <span data-ttu-id="0199f-117">Dopo il completamento del failover, l'insieme di credenziali delle chiavi è in modalità di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="0199f-117">After a failover is complete, your key vault is in read-only mode.</span></span> <span data-ttu-id="0199f-118">Le richieste supportate in questa modalità sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="0199f-118">Requests that are supported in this mode are:</span></span>
  * <span data-ttu-id="0199f-119">List key vaults</span><span class="sxs-lookup"><span data-stu-id="0199f-119">List key vaults</span></span>
  * <span data-ttu-id="0199f-120">Get properties of key vaults</span><span class="sxs-lookup"><span data-stu-id="0199f-120">Get properties of key vaults</span></span>
  * <span data-ttu-id="0199f-121">List secrets</span><span class="sxs-lookup"><span data-stu-id="0199f-121">List secrets</span></span>
  * <span data-ttu-id="0199f-122">Get secrets</span><span class="sxs-lookup"><span data-stu-id="0199f-122">Get secrets</span></span>
  * <span data-ttu-id="0199f-123">List keys</span><span class="sxs-lookup"><span data-stu-id="0199f-123">List keys</span></span>
  * <span data-ttu-id="0199f-124">Get (properties of) keys</span><span class="sxs-lookup"><span data-stu-id="0199f-124">Get (properties of) keys</span></span>
  * <span data-ttu-id="0199f-125">Crittografare il contenuto</span><span class="sxs-lookup"><span data-stu-id="0199f-125">Encrypt</span></span>
  * <span data-ttu-id="0199f-126">Decrypt</span><span class="sxs-lookup"><span data-stu-id="0199f-126">Decrypt</span></span>
  * <span data-ttu-id="0199f-127">Wrap</span><span class="sxs-lookup"><span data-stu-id="0199f-127">Wrap</span></span>
  * <span data-ttu-id="0199f-128">Unwrap</span><span class="sxs-lookup"><span data-stu-id="0199f-128">Unwrap</span></span>
  * <span data-ttu-id="0199f-129">Verificare</span><span class="sxs-lookup"><span data-stu-id="0199f-129">Verify</span></span>
  * <span data-ttu-id="0199f-130">Sign</span><span class="sxs-lookup"><span data-stu-id="0199f-130">Sign</span></span>
  * <span data-ttu-id="0199f-131">Backup</span><span class="sxs-lookup"><span data-stu-id="0199f-131">Backup</span></span>
* <span data-ttu-id="0199f-132">Dopo il failback di un failover, tutti i tipi di richiesta, ad esempio le richieste di lettura *e* scrittura, risultano disponibili.</span><span class="sxs-lookup"><span data-stu-id="0199f-132">After a failover is failed back, all request types (including read *and* write requests) are available.</span></span>

