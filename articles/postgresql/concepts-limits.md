---
title: Limiti del Database di Azure per PostgreSQL | Microsoft Docs
description: Descrive i limiti del Database di Azure per PostgreSQL.
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.topic: article
ms.date: 06/01/2017
ms.openlocfilehash: 38988fc5c0dc05331ea078534cd1a05e9eca2493
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="limitations-in-azure-database-for-postgresql"></a><span data-ttu-id="6f982-103">Limiti del Database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="6f982-103">Limitations in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="6f982-104">Il servizio Database di Azure per PostgreSQL è in anteprima pubblica.</span><span class="sxs-lookup"><span data-stu-id="6f982-104">The Azure Database for PostgreSQL service is in public preview.</span></span> <span data-ttu-id="6f982-105">Nelle sezioni seguenti vengono descritti i limiti delle capacità e funzionali nel servizio del database.</span><span class="sxs-lookup"><span data-stu-id="6f982-105">The following sections describe capacity and functional limits in the database service.</span></span>

## <a name="service-tier-maximums"></a><span data-ttu-id="6f982-106">Valori massimi del livello di servizio</span><span class="sxs-lookup"><span data-stu-id="6f982-106">Service Tier Maximums</span></span>
<span data-ttu-id="6f982-107">Il Database di Azure per PostgreSQL dispone di più livelli di servizio tra cui è possibile scegliere durante la creazione di un server.</span><span class="sxs-lookup"><span data-stu-id="6f982-107">Azure Database for PostgreSQL has multiple service tiers you can choose from when creating a server.</span></span> <span data-ttu-id="6f982-108">Per altre informazioni vedere [Opzioni e prestazioni disponibili in ogni livello di servizio](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="6f982-108">For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).</span></span>  

<span data-ttu-id="6f982-109">Esiste un numero massimo di connessioni, unità di calcolo e archiviazione in ogni livello di servizio durante l'anteprima del servizio, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6f982-109">There is a maximum number of connections, compute units, and storage in each service tier during the service preview, as follows:</span></span> 

|                            |                   |
| :------------------------- | :---------------- |
| <span data-ttu-id="6f982-110">**Numero massimo di connessioni**</span><span class="sxs-lookup"><span data-stu-id="6f982-110">**Max connections**</span></span>        |                   |
| <span data-ttu-id="6f982-111">Base con 50 unità di calcolo</span><span class="sxs-lookup"><span data-stu-id="6f982-111">Basic 50 Compute Units</span></span>     | <span data-ttu-id="6f982-112">50 connessioni</span><span class="sxs-lookup"><span data-stu-id="6f982-112">50 connections</span></span>    |
| <span data-ttu-id="6f982-113">Base con 100 unità di calcolo</span><span class="sxs-lookup"><span data-stu-id="6f982-113">Basic 100 Compute Units</span></span>    | <span data-ttu-id="6f982-114">100 connessioni</span><span class="sxs-lookup"><span data-stu-id="6f982-114">100 connections</span></span>   |
| <span data-ttu-id="6f982-115">Standard con 100 unità di calcolo</span><span class="sxs-lookup"><span data-stu-id="6f982-115">Standard 100 Compute Units</span></span> | <span data-ttu-id="6f982-116">200 connessioni</span><span class="sxs-lookup"><span data-stu-id="6f982-116">200 connections</span></span>   |
| <span data-ttu-id="6f982-117">Standard con 200 unità di calcolo</span><span class="sxs-lookup"><span data-stu-id="6f982-117">Standard 200 Compute Units</span></span> | <span data-ttu-id="6f982-118">300 connessioni</span><span class="sxs-lookup"><span data-stu-id="6f982-118">300 connections</span></span>   |
| <span data-ttu-id="6f982-119">Standard con 400 unità di calcolo</span><span class="sxs-lookup"><span data-stu-id="6f982-119">Standard 400 Compute Units</span></span> | <span data-ttu-id="6f982-120">400 connessioni</span><span class="sxs-lookup"><span data-stu-id="6f982-120">400 connections</span></span>   |
| <span data-ttu-id="6f982-121">Standard con 800 unità di calcolo</span><span class="sxs-lookup"><span data-stu-id="6f982-121">Standard 800 Compute Units</span></span> | <span data-ttu-id="6f982-122">500 connessioni</span><span class="sxs-lookup"><span data-stu-id="6f982-122">500 connections</span></span>   |
| <span data-ttu-id="6f982-123">**Unità di calcolo massime**</span><span class="sxs-lookup"><span data-stu-id="6f982-123">**Max Compute Units**</span></span>      |                   |
| <span data-ttu-id="6f982-124">Livello di servizio Basic</span><span class="sxs-lookup"><span data-stu-id="6f982-124">Basic service tier</span></span>         | <span data-ttu-id="6f982-125">100 unità di calcolo</span><span class="sxs-lookup"><span data-stu-id="6f982-125">100 Compute Units</span></span> |
| <span data-ttu-id="6f982-126">Livello di servizio Standard</span><span class="sxs-lookup"><span data-stu-id="6f982-126">Standard service tier</span></span>      | <span data-ttu-id="6f982-127">800 unità di calcolo</span><span class="sxs-lookup"><span data-stu-id="6f982-127">800 Compute Units</span></span> |
| <span data-ttu-id="6f982-128">**Spazio di archiviazione massimo**</span><span class="sxs-lookup"><span data-stu-id="6f982-128">**Max storage**</span></span>            |                   |
| <span data-ttu-id="6f982-129">Livello di servizio Basic</span><span class="sxs-lookup"><span data-stu-id="6f982-129">Basic service tier</span></span>         | <span data-ttu-id="6f982-130">1 TB</span><span class="sxs-lookup"><span data-stu-id="6f982-130">1 TB</span></span>              |
| <span data-ttu-id="6f982-131">Livello di servizio Standard</span><span class="sxs-lookup"><span data-stu-id="6f982-131">Standard service tier</span></span>      | <span data-ttu-id="6f982-132">1 TB</span><span class="sxs-lookup"><span data-stu-id="6f982-132">1 TB</span></span>              |

<span data-ttu-id="6f982-133">Quando viene raggiunto un numero eccessivo di connessioni, è possibile che si riceva l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="6f982-133">When too many connections are reached, you may receive the following error:</span></span>
> <span data-ttu-id="6f982-134">FATAL: sorry, too many clients already (ERRORE IRREVERSIBILE: ci sono già troppi client)</span><span class="sxs-lookup"><span data-stu-id="6f982-134">FATAL:  sorry, too many clients already</span></span>

## <a name="preview-functional-limitations"></a><span data-ttu-id="6f982-135">Limiti funzionali dell'anteprima</span><span class="sxs-lookup"><span data-stu-id="6f982-135">Preview functional limitations</span></span>
### <a name="scale-operations"></a><span data-ttu-id="6f982-136">Operazioni di scalabilità</span><span class="sxs-lookup"><span data-stu-id="6f982-136">Scale operations</span></span>
1.  <span data-ttu-id="6f982-137">La scalabilità dinamica dei server tra i livelli di servizio non è attualmente supportata,</span><span class="sxs-lookup"><span data-stu-id="6f982-137">Dynamic scaling of servers across service tiers is currently not supported.</span></span> <span data-ttu-id="6f982-138">vale a dire il passaggio tra i livelli di servizio Base e Standard.</span><span class="sxs-lookup"><span data-stu-id="6f982-138">That is, switching between Basic and Standard service tiers.</span></span>
2.  <span data-ttu-id="6f982-139">L'aumento dinamico su richiesta dell'archiviazione sul server creato in precedenza non è attualmente supportato.</span><span class="sxs-lookup"><span data-stu-id="6f982-139">Dynamic on-demand increase of storage on pre-created server is currently not supported.</span></span>
3.  <span data-ttu-id="6f982-140">La riduzione delle dimensioni di archiviazione del server non è supportato.</span><span class="sxs-lookup"><span data-stu-id="6f982-140">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="6f982-141">Aggiornamenti della versione dei server</span><span class="sxs-lookup"><span data-stu-id="6f982-141">Server version upgrades</span></span>
- <span data-ttu-id="6f982-142">La migrazione automatica tra le versioni del motore del database principale non è attualmente supportata.</span><span class="sxs-lookup"><span data-stu-id="6f982-142">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="6f982-143">Gestione sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="6f982-143">Subscription management</span></span>
- <span data-ttu-id="6f982-144">Lo spostamento dinamico di server creati in precedenza tra le sottoscrizioni e il gruppo di risorse non è attualmente supportato.</span><span class="sxs-lookup"><span data-stu-id="6f982-144">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="6f982-145">Ripristino temporizzato</span><span class="sxs-lookup"><span data-stu-id="6f982-145">Point-in-time-restore</span></span>
1.  <span data-ttu-id="6f982-146">Il ripristino a un livello di servizio diverso e/o a dimensioni delle unità di calcolo e di archiviazione diverse non è consentito.</span><span class="sxs-lookup"><span data-stu-id="6f982-146">Restoring to different service tier and/or Compute Units and Storage size is not allowed.</span></span>
2.  <span data-ttu-id="6f982-147">Il ripristino di un server eliminato non è supportato.</span><span class="sxs-lookup"><span data-stu-id="6f982-147">Restoring a dropped server is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f982-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6f982-148">Next steps</span></span>
- <span data-ttu-id="6f982-149">Informazioni sulle [opzioni e prestazioni disponibili in ogni piano tariffario](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="6f982-149">Understand [What’s available in each pricing tier](concepts-service-tiers.md)</span></span>
- <span data-ttu-id="6f982-150">Informazione sulle [Supported PostgreSQL Database Versions](concepts-supported-versions.md) (Versioni supportate del Database PostgreSQL)</span><span class="sxs-lookup"><span data-stu-id="6f982-150">Understand [Supported PostgreSQL Database Versions](concepts-supported-versions.md)</span></span>
- <span data-ttu-id="6f982-151">Rivedere [How To Back up and Restore a server in Azure Database for PostgreSQL using the Azure portal](howto-restore-server-portal.md) (Come eseguire il backup e il ripristino di un server nel Database di Azure per PostgreSQL usando il portale di Azure)</span><span class="sxs-lookup"><span data-stu-id="6f982-151">Review [How To Back up and Restore a server in Azure Database for PostgreSQL using the Azure portal](howto-restore-server-portal.md)</span></span>
