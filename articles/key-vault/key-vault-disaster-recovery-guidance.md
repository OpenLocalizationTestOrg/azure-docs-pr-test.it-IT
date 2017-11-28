---
title: toodo aaaWhat nell'evento hello di un'interruzione del servizio Azure che interessa l'insieme di credenziali chiave di Azure | Documenti Microsoft
description: Informazioni su quali toodo nell'evento hello di un'interruzione del servizio Azure che interessa l'insieme di credenziali chiave di Azure.
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
ms.openlocfilehash: 88eec82ada401a28323b3eea126168185ba4cdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a><span data-ttu-id="259a6-103">Disponibilità e ridondanza dell'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="259a6-103">Azure Key Vault availability and redundancy</span></span>
<span data-ttu-id="259a6-104">Insieme di credenziali chiave di Azure offre più livelli di ridondanza toomake assicurarsi che le chiavi e segreti rimangono disponibili tooyour applicazione anche se i singoli componenti di hello del servizio hanno esito negativo.</span><span class="sxs-lookup"><span data-stu-id="259a6-104">Azure Key Vault features multiple layers of redundancy toomake sure that your keys and secrets remain available tooyour application even if individual components of hello service fail.</span></span>

<span data-ttu-id="259a6-105">Hello contenuto di credenziali delle chiavi viene replicati all'interno di area hello e area secondaria tooa almeno 150 miglia immediatamente, ma all'interno di hello geography stesso.</span><span class="sxs-lookup"><span data-stu-id="259a6-105">hello contents of your key vault are replicated within hello region and tooa secondary region at least 150 miles away but within hello same geography.</span></span> <span data-ttu-id="259a6-106">Questo garantisce un'elevata durabilità delle chiavi e dei segreti.</span><span class="sxs-lookup"><span data-stu-id="259a6-106">This maintains high durability of your keys and secrets.</span></span> <span data-ttu-id="259a6-107">Vedere hello [Azure abbinato aree](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) per informazioni dettagliate su una coppia di area specifico.</span><span class="sxs-lookup"><span data-stu-id="259a6-107">See hello [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document for details on specific region pairs.</span></span>

<span data-ttu-id="259a6-108">Se i singoli componenti all'interno del servizio dell'insieme di credenziali chiave hello hanno esito negativo, componenti alternativi all'interno di area hello passaggio tooserve toomake la richiesta che vi sia alcuna riduzione delle funzionalità.</span><span class="sxs-lookup"><span data-stu-id="259a6-108">If individual components within hello key vault service fail, alternate components within hello region step in tooserve your request toomake sure that there is no degradation of functionality.</span></span> <span data-ttu-id="259a6-109">Non è necessario tootake tootrigger qualsiasi azione questo.</span><span class="sxs-lookup"><span data-stu-id="259a6-109">You do not need tootake any action tootrigger this.</span></span> <span data-ttu-id="259a6-110">Viene eseguita automaticamente e sarà tooyou trasparente.</span><span class="sxs-lookup"><span data-stu-id="259a6-110">It happens automatically and will be transparent tooyou.</span></span>

<span data-ttu-id="259a6-111">In evento raro hello che non è disponibile un'intera regione di Azure, le richieste di hello apportate dell'insieme di credenziali chiave di Azure in tale area vengono indirizzate automaticamente (*failover*) area secondaria tooa.</span><span class="sxs-lookup"><span data-stu-id="259a6-111">In hello rare event that an entire Azure region is unavailable, hello requests that you make of Azure Key Vault in that region are automatically routed (*failed over*) tooa secondary region.</span></span> <span data-ttu-id="259a6-112">Quando l'area primaria hello è nuovamente disponibile, le richieste vengono indirizzate nuovamente (*non è stato possibile eseguire il*) area primaria toohello.</span><span class="sxs-lookup"><span data-stu-id="259a6-112">When hello primary region is available again, requests are routed back (*failed back*) toohello primary region.</span></span> <span data-ttu-id="259a6-113">Nuovamente, non è necessario tootake alcuna azione perché ciò avviene automaticamente.</span><span class="sxs-lookup"><span data-stu-id="259a6-113">Again, you do not need tootake any action because this happens automatically.</span></span>

<span data-ttu-id="259a6-114">Esistono alcuni aspetti toobe conoscere:</span><span class="sxs-lookup"><span data-stu-id="259a6-114">There are a few caveats toobe aware of:</span></span>

* <span data-ttu-id="259a6-115">Nell'evento hello di un failover di area, potrebbe richiedere alcuni minuti per hello servizio toofail.</span><span class="sxs-lookup"><span data-stu-id="259a6-115">In hello event of a region failover, it may take a few minutes for hello service toofail over.</span></span> <span data-ttu-id="259a6-116">Le richieste effettuate durante questo periodo potrebbero non riuscire finché non viene completato il failover hello.</span><span class="sxs-lookup"><span data-stu-id="259a6-116">Requests that are made during this time may fail until hello failover completes.</span></span>
* <span data-ttu-id="259a6-117">Dopo il completamento del failover, l'insieme di credenziali delle chiavi è in modalità di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="259a6-117">After a failover is complete, your key vault is in read-only mode.</span></span> <span data-ttu-id="259a6-118">Le richieste supportate in questa modalità sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="259a6-118">Requests that are supported in this mode are:</span></span>
  * <span data-ttu-id="259a6-119">List key vaults</span><span class="sxs-lookup"><span data-stu-id="259a6-119">List key vaults</span></span>
  * <span data-ttu-id="259a6-120">Get properties of key vaults</span><span class="sxs-lookup"><span data-stu-id="259a6-120">Get properties of key vaults</span></span>
  * <span data-ttu-id="259a6-121">List secrets</span><span class="sxs-lookup"><span data-stu-id="259a6-121">List secrets</span></span>
  * <span data-ttu-id="259a6-122">Get secrets</span><span class="sxs-lookup"><span data-stu-id="259a6-122">Get secrets</span></span>
  * <span data-ttu-id="259a6-123">List keys</span><span class="sxs-lookup"><span data-stu-id="259a6-123">List keys</span></span>
  * <span data-ttu-id="259a6-124">Get (properties of) keys</span><span class="sxs-lookup"><span data-stu-id="259a6-124">Get (properties of) keys</span></span>
  * <span data-ttu-id="259a6-125">Crittografare il contenuto</span><span class="sxs-lookup"><span data-stu-id="259a6-125">Encrypt</span></span>
  * <span data-ttu-id="259a6-126">Decrypt</span><span class="sxs-lookup"><span data-stu-id="259a6-126">Decrypt</span></span>
  * <span data-ttu-id="259a6-127">Wrap</span><span class="sxs-lookup"><span data-stu-id="259a6-127">Wrap</span></span>
  * <span data-ttu-id="259a6-128">Unwrap</span><span class="sxs-lookup"><span data-stu-id="259a6-128">Unwrap</span></span>
  * <span data-ttu-id="259a6-129">Verificare</span><span class="sxs-lookup"><span data-stu-id="259a6-129">Verify</span></span>
  * <span data-ttu-id="259a6-130">Sign</span><span class="sxs-lookup"><span data-stu-id="259a6-130">Sign</span></span>
  * <span data-ttu-id="259a6-131">Backup</span><span class="sxs-lookup"><span data-stu-id="259a6-131">Backup</span></span>
* <span data-ttu-id="259a6-132">Dopo il failback di un failover, tutti i tipi di richiesta, ad esempio le richieste di lettura *e* scrittura, risultano disponibili.</span><span class="sxs-lookup"><span data-stu-id="259a6-132">After a failover is failed back, all request types (including read *and* write requests) are available.</span></span>

