---
title: nel Database di Azure per MySQL aaaLimitations | Documenti Microsoft
description: Descrive i limiti dell'anteprima del Database di Azure per MySQL.
services: mysql
author: jasonh
ms.author: kamathsun
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 9c877c592bf640f62182d8761c9c51363882d706
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-in-azure-database-for-mysql-preview"></a><span data-ttu-id="38516-103">Limiti del Database di Azure per MySQL (anteprima)</span><span class="sxs-lookup"><span data-stu-id="38516-103">Limitations in Azure Database for MySQL (Preview)</span></span>
<span data-ttu-id="38516-104">Hello Azure Database per il servizio MySQL è in anteprima pubblica.</span><span class="sxs-lookup"><span data-stu-id="38516-104">hello Azure Database for MySQL service is in public preview.</span></span> <span data-ttu-id="38516-105">Hello nelle sezioni seguenti vengono descritti la capacità e i limiti funzionali nel servizio di database hello.</span><span class="sxs-lookup"><span data-stu-id="38516-105">hello following sections describe capacity and functional limits in hello database service.</span></span>

## <a name="service-tier-maximums"></a><span data-ttu-id="38516-106">Valori massimi del livello di servizio</span><span class="sxs-lookup"><span data-stu-id="38516-106">Service Tier Maximums</span></span>
<span data-ttu-id="38516-107">Il Database di Azure per MySQL dispone di più livelli di servizio tra cui è possibile scegliere durante la creazione di un server.</span><span class="sxs-lookup"><span data-stu-id="38516-107">Azure Database for MySQL has multiple service tiers you can choose from when creating a server.</span></span> <span data-ttu-id="38516-108">Per altre informazioni vedere [Opzioni e prestazioni disponibili in ogni livello di servizio](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="38516-108">For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).</span></span>  

<span data-ttu-id="38516-109">È un numero massimo di connessioni, unità di calcolo e archiviazione in ogni livello di servizio durante l'anteprima del servizio hello, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="38516-109">There is a maximum number of connections, compute units, and storage in each service tier during hello service preview, as follows:</span></span> 

|                            |                   |
| :------------------------- | :---------------- |
| <span data-ttu-id="38516-110">**Numero massimo di connessioni**</span><span class="sxs-lookup"><span data-stu-id="38516-110">**Max connections**</span></span>        |                   |
| <span data-ttu-id="38516-111">Base con 50 unità di calcolo</span><span class="sxs-lookup"><span data-stu-id="38516-111">Basic 50 Compute Units</span></span>     | <span data-ttu-id="38516-112">50 connessioni</span><span class="sxs-lookup"><span data-stu-id="38516-112">50 connections</span></span>    |
| <span data-ttu-id="38516-113">Base con 100 unità di calcolo</span><span class="sxs-lookup"><span data-stu-id="38516-113">Basic 100 Compute Units</span></span>    | <span data-ttu-id="38516-114">100 connessioni</span><span class="sxs-lookup"><span data-stu-id="38516-114">100 connections</span></span>   |
| <span data-ttu-id="38516-115">Standard con 100 unità di calcolo</span><span class="sxs-lookup"><span data-stu-id="38516-115">Standard 100 Compute Units</span></span> | <span data-ttu-id="38516-116">200 connessioni</span><span class="sxs-lookup"><span data-stu-id="38516-116">200 connections</span></span>   |
| <span data-ttu-id="38516-117">Standard con 200 unità di calcolo</span><span class="sxs-lookup"><span data-stu-id="38516-117">Standard 200 Compute Units</span></span> | <span data-ttu-id="38516-118">300 connessioni</span><span class="sxs-lookup"><span data-stu-id="38516-118">300 connections</span></span>   |
| <span data-ttu-id="38516-119">Standard con 400 unità di calcolo</span><span class="sxs-lookup"><span data-stu-id="38516-119">Standard 400 Compute Units</span></span> | <span data-ttu-id="38516-120">400 connessioni</span><span class="sxs-lookup"><span data-stu-id="38516-120">400 connections</span></span>   |
| <span data-ttu-id="38516-121">Standard con 800 unità di calcolo</span><span class="sxs-lookup"><span data-stu-id="38516-121">Standard 800 Compute Units</span></span> | <span data-ttu-id="38516-122">500 connessioni</span><span class="sxs-lookup"><span data-stu-id="38516-122">500 connections</span></span>   |
| <span data-ttu-id="38516-123">**Unità di calcolo massime**</span><span class="sxs-lookup"><span data-stu-id="38516-123">**Max Compute Units**</span></span>      |                   |
| <span data-ttu-id="38516-124">Livello di servizio Basic</span><span class="sxs-lookup"><span data-stu-id="38516-124">Basic service tier</span></span>         | <span data-ttu-id="38516-125">100 unità di calcolo</span><span class="sxs-lookup"><span data-stu-id="38516-125">100 Compute Units</span></span> |
| <span data-ttu-id="38516-126">Livello di servizio Standard</span><span class="sxs-lookup"><span data-stu-id="38516-126">Standard service tier</span></span>      | <span data-ttu-id="38516-127">800 unità di calcolo</span><span class="sxs-lookup"><span data-stu-id="38516-127">800 Compute Units</span></span> |
| <span data-ttu-id="38516-128">**Spazio di archiviazione massimo**</span><span class="sxs-lookup"><span data-stu-id="38516-128">**Max storage**</span></span>            |                   |
| <span data-ttu-id="38516-129">Livello di servizio Basic</span><span class="sxs-lookup"><span data-stu-id="38516-129">Basic service tier</span></span>         | <span data-ttu-id="38516-130">1 TB</span><span class="sxs-lookup"><span data-stu-id="38516-130">1 TB</span></span>              |
| <span data-ttu-id="38516-131">Livello di servizio Standard</span><span class="sxs-lookup"><span data-stu-id="38516-131">Standard service tier</span></span>      | <span data-ttu-id="38516-132">1 TB</span><span class="sxs-lookup"><span data-stu-id="38516-132">1 TB</span></span>              |

<span data-ttu-id="38516-133">Quando vengono raggiunte numero eccessivo di connessioni, potrebbe essere visualizzato il seguente errore hello:</span><span class="sxs-lookup"><span data-stu-id="38516-133">When too many connections are reached, you may receive hello following error:</span></span>
> <span data-ttu-id="38516-134">ERROR 1040 (08004): Too many connections (ERRORE 1040 (08004): numero eccessivo di connessioni)</span><span class="sxs-lookup"><span data-stu-id="38516-134">ERROR 1040 (08004): Too many connections</span></span>

## <a name="preview-functional-limitations"></a><span data-ttu-id="38516-135">Limiti funzionali dell'anteprima:</span><span class="sxs-lookup"><span data-stu-id="38516-135">Preview functional limitations:</span></span>
### <a name="scale-operations"></a><span data-ttu-id="38516-136">Operazioni di scalabilità:</span><span class="sxs-lookup"><span data-stu-id="38516-136">Scale operations:</span></span>
1.  <span data-ttu-id="38516-137">La scalabilità dinamica dei server tra i livelli di servizio non è attualmente supportata,</span><span class="sxs-lookup"><span data-stu-id="38516-137">Dynamic scaling of servers across service tiers is currently not supported.</span></span> <span data-ttu-id="38516-138">vale a dire il passaggio tra i livelli di servizio Base e Standard.</span><span class="sxs-lookup"><span data-stu-id="38516-138">That is, switching between Basic and Standard service tiers.</span></span>
2.  <span data-ttu-id="38516-139">L'aumento dinamico su richiesta dell'archiviazione sul server creato in precedenza non è attualmente supportato.</span><span class="sxs-lookup"><span data-stu-id="38516-139">Dynamic on-demand increase of storage on pre-created server is currently not supported.</span></span>
3.  <span data-ttu-id="38516-140">La riduzione delle dimensioni di archiviazione del server non è supportato.</span><span class="sxs-lookup"><span data-stu-id="38516-140">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="38516-141">Aggiornamenti della versione dei server:</span><span class="sxs-lookup"><span data-stu-id="38516-141">Server version upgrades:</span></span>
- <span data-ttu-id="38516-142">La migrazione automatica tra le versioni del motore del database principale non è attualmente supportata.</span><span class="sxs-lookup"><span data-stu-id="38516-142">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="38516-143">Gestione sottoscrizioni:</span><span class="sxs-lookup"><span data-stu-id="38516-143">Subscription management:</span></span>
- <span data-ttu-id="38516-144">Lo spostamento dinamico di server creati in precedenza tra le sottoscrizioni e il gruppo di risorse non è attualmente supportato.</span><span class="sxs-lookup"><span data-stu-id="38516-144">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="38516-145">Ripristino temporizzato:</span><span class="sxs-lookup"><span data-stu-id="38516-145">Point-in-time-restore:</span></span>
1.  <span data-ttu-id="38516-146">Non è consentito il ripristino a livello di servizio toodifferent e/o dimensioni unità di calcolo e archiviazione.</span><span class="sxs-lookup"><span data-stu-id="38516-146">Restoring toodifferent service tier and/or Compute Units and Storage size is not allowed.</span></span>
2.  <span data-ttu-id="38516-147">Il ripristino di un server eliminato non è supportato.</span><span class="sxs-lookup"><span data-stu-id="38516-147">Restoring a dropped server is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38516-148">Passaggi successivi:</span><span class="sxs-lookup"><span data-stu-id="38516-148">Next Steps:</span></span>
<span data-ttu-id="38516-149">[Opzioni disponibili in ogni livello di servizio](concepts-service-tiers.md)
[Versioni del Database MySQL supportate](concepts-supported-versions.md)</span><span class="sxs-lookup"><span data-stu-id="38516-149">[What’s available in each service tier](concepts-service-tiers.md)
[Supported MySQL Database Versions](concepts-supported-versions.md)</span></span>
