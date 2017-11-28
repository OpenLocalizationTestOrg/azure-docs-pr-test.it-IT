---
title: Esercitazioni di ripristino di emergenza Database aaaSQL | Documenti Microsoft
description: Altre informazioni e procedure consigliate per l'utilizzo di keep toohelp di Database SQL di Azure tooperform disaster recovery drill le interruzioni toofailures resilienti applicazioni aziendali critiche di importanza.
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: b44a269c-fe2a-404f-b013-290030860bd1
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/31/2016
ms.author: sashan
ms.openlocfilehash: bf17857a19fdebddf0d4f55e4db3a1b33efb4e8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="performing-disaster-recovery-drill"></a><span data-ttu-id="33174-103">Esercitazione per il ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="33174-103">Performing Disaster Recovery Drill</span></span>
<span data-ttu-id="33174-104">È consigliabile verificare periodicamente la conformità delle applicazioni per il flusso di lavoro di ripristino.</span><span class="sxs-lookup"><span data-stu-id="33174-104">It is recommended that validation of application readiness for recovery workflow is performed periodically.</span></span> <span data-ttu-id="33174-105">Comportamento dell'applicazione hello verifica e le implicazioni dell'interruzione di perdite e/o hello dati prevede che il failover è buona norma engineering.</span><span class="sxs-lookup"><span data-stu-id="33174-105">Verifying hello application behavior and implications of data loss and/or hello disruption that failover involves is a good engineering practice.</span></span> <span data-ttu-id="33174-106">Inoltre, questa verifica è richiesta dalla maggior parte degli standard del settore come parte della certificazione di continuità aziendale.</span><span class="sxs-lookup"><span data-stu-id="33174-106">It is also a requirement by most industry standards as part of business continuity certification.</span></span>

<span data-ttu-id="33174-107">L'esercitazione per il ripristino di emergenza prevede l'esecuzione delle attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="33174-107">Performing a disaster recovery drill consists of:</span></span>

* <span data-ttu-id="33174-108">Simulazione dell'interruzione del livello dati</span><span class="sxs-lookup"><span data-stu-id="33174-108">Simulating data tier outage</span></span>
* <span data-ttu-id="33174-109">Ripristino</span><span class="sxs-lookup"><span data-stu-id="33174-109">Recovering</span></span>
* <span data-ttu-id="33174-110">Convalida dell'integrità dell'applicazione dopo il ripristino</span><span class="sxs-lookup"><span data-stu-id="33174-110">Validate application integrity post recovery</span></span>

<span data-ttu-id="33174-111">A seconda di come si [progettato l'applicazione per la continuità aziendale](sql-database-business-continuity.md), drill hello tooexecute di hello del flusso di lavoro può variare.</span><span class="sxs-lookup"><span data-stu-id="33174-111">Depending on how you [designed your application for business continuity](sql-database-business-continuity.md), hello workflow tooexecute hello drill can vary.</span></span> <span data-ttu-id="33174-112">Di seguito sono riportati alcuni suggerimenti hello condurre un'analisi di ripristino di emergenza nel contesto di hello del Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="33174-112">Below we describe hello best practices conducting a disaster recovery drill in hello context of Azure SQL Database.</span></span>

## <a name="geo-restore"></a><span data-ttu-id="33174-113">Ripristino geografico</span><span class="sxs-lookup"><span data-stu-id="33174-113">Geo-restore</span></span>
<span data-ttu-id="33174-114">tooprevent hello potenziale perdita di dati durante l'esecuzione di un'analisi di ripristino di emergenza, è consigliabile eseguire drill hello usando un ambiente di test mediante la creazione di una copia dell'ambiente di produzione hello e l'uso del flusso di lavoro failover dell'applicazione hello tooverify.</span><span class="sxs-lookup"><span data-stu-id="33174-114">tooprevent hello potential data loss when conducting a disaster recovery drill, we recommend performing hello drill using a test environment by creating a copy of hello production environment and using it tooverify hello application’s failover workflow.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="33174-115">Simulazione dell'interruzione del servizio</span><span class="sxs-lookup"><span data-stu-id="33174-115">Outage simulation</span></span>
<span data-ttu-id="33174-116">toosimulate hello interruzione, è possibile eliminare o rinominare il database di origine hello.</span><span class="sxs-lookup"><span data-stu-id="33174-116">toosimulate hello outage, you can delete or rename hello source database.</span></span> <span data-ttu-id="33174-117">Ciò causa un errore di connettività dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="33174-117">This causes application connectivity failures.</span></span>

#### <a name="recovery"></a><span data-ttu-id="33174-118">Ripristino</span><span class="sxs-lookup"><span data-stu-id="33174-118">Recovery</span></span>
* <span data-ttu-id="33174-119">Eseguire ripristino a livello geografico hello del database hello in un server diverso, come descritto [qui](sql-database-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="33174-119">Perform hello geo-restore of hello database into a different server as described [here](sql-database-disaster-recovery.md).</span></span>
* <span data-ttu-id="33174-120">Modifica hello applicazione configurazione tooconnect toohello ripristinato del database e seguire hello [configurare un database dopo il ripristino](sql-database-disaster-recovery.md) ripristino hello toocomplete della Guida.</span><span class="sxs-lookup"><span data-stu-id="33174-120">Change hello application configuration tooconnect toohello recovered database and follow hello [Configure a database after recovery](sql-database-disaster-recovery.md) guide toocomplete hello recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="33174-121">Convalida</span><span class="sxs-lookup"><span data-stu-id="33174-121">Validation</span></span>
* <span data-ttu-id="33174-122">Hello completo drill verificando il ripristino post integrità applicazione hello (incluse le stringhe di connessione, gli account di accesso, il test delle funzionalità di base o altra parte le convalide delle procedure conclusioni standard dell'applicazione).</span><span class="sxs-lookup"><span data-stu-id="33174-122">Complete hello drill by verifying hello application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="geo-replication"></a><span data-ttu-id="33174-123">Replica geografica</span><span class="sxs-lookup"><span data-stu-id="33174-123">Geo-replication</span></span>
<span data-ttu-id="33174-124">Per un database che è protetta tramite drill di replica geografica hello esercizio prevede toohello il failover pianificato del database secondario.</span><span class="sxs-lookup"><span data-stu-id="33174-124">For a database that is protected using geo-replication hello drill exercise involves planned failover toohello secondary database.</span></span> <span data-ttu-id="33174-125">Hello failover pianificato assicura che hello primario e i database secondari hello rimangano sincronizzati quando il cambio di ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="33174-125">hello planned failover ensures that hello primary and hello secondary databases remain in sync when hello roles are switched.</span></span> <span data-ttu-id="33174-126">A differenza di hello failover non pianificato, questa operazione non produce una perdita di dati, in modo drill hello possono essere eseguite nell'ambiente di produzione hello.</span><span class="sxs-lookup"><span data-stu-id="33174-126">Unlike hello unplanned failover, this operation does not result in data loss, so hello drill can be performed in hello production environment.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="33174-127">Simulazione dell'interruzione del servizio</span><span class="sxs-lookup"><span data-stu-id="33174-127">Outage simulation</span></span>
<span data-ttu-id="33174-128">interruzione di hello toosimulate, è possibile disabilitare l'applicazione web hello o macchina virtuale connessa toohello database.</span><span class="sxs-lookup"><span data-stu-id="33174-128">toosimulate hello outage, you can disable hello web application or virtual machine connected toohello database.</span></span> <span data-ttu-id="33174-129">Di conseguenza gli errori di connettività hello per i client web hello.</span><span class="sxs-lookup"><span data-stu-id="33174-129">This results in hello connectivity failures for hello web clients.</span></span>

#### <a name="recovery"></a><span data-ttu-id="33174-130">Ripristino</span><span class="sxs-lookup"><span data-stu-id="33174-130">Recovery</span></span>
* <span data-ttu-id="33174-131">Assicurarsi che configurazione dell'applicazione hello in hello ripristino di emergenza area punti toohello ex secondario che diventa hello accessibile completamente nuovo database primario.</span><span class="sxs-lookup"><span data-stu-id="33174-131">Make sure hello application configuration in hello DR region points toohello former secondary which becomes hello fully accessible new primary.</span></span>
* <span data-ttu-id="33174-132">Eseguire [failover pianificato](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) un nuovo database primario del database secondario hello toomake</span><span class="sxs-lookup"><span data-stu-id="33174-132">Perform [planned failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) toomake hello secondary database a new primary</span></span>
* <span data-ttu-id="33174-133">Seguire hello [configurare un database dopo il ripristino](sql-database-disaster-recovery.md) ripristino hello toocomplete della Guida.</span><span class="sxs-lookup"><span data-stu-id="33174-133">Follow hello [Configure a database after recovery](sql-database-disaster-recovery.md) guide toocomplete hello recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="33174-134">Convalida</span><span class="sxs-lookup"><span data-stu-id="33174-134">Validation</span></span>
* <span data-ttu-id="33174-135">Hello completo drill verificando il ripristino post integrità applicazione hello (incluse le stringhe di connessione, gli account di accesso, il test delle funzionalità di base o altra parte le convalide delle procedure conclusioni standard dell'applicazione).</span><span class="sxs-lookup"><span data-stu-id="33174-135">Complete hello drill by verifying hello application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="next-steps"></a><span data-ttu-id="33174-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="33174-136">Next steps</span></span>
* <span data-ttu-id="33174-137">toolearn sugli scenari di continuità aziendale, vedere [gli scenari di continuità](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="33174-137">toolearn about business continuity scenarios, see [Continuity scenarios](sql-database-business-continuity.md)</span></span>
* <span data-ttu-id="33174-138">toolearn sui backup di Database di SQL Azure automatizzati, vedere [backup automatici di Database SQL](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="33174-138">toolearn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span></span>
* <span data-ttu-id="33174-139">toolearn sull'utilizzo di backup automatico per il ripristino, vedere [ripristinare un database dai backup avviate dal servizio hello](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="33174-139">toolearn about using automated backups for recovery, see [restore a database from hello service-initiated backups](sql-database-recovery-using-backups.md)</span></span>
* <span data-ttu-id="33174-140">toolearn sulle opzioni di ripristino più veloce, vedere [replica geografica attiva](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="33174-140">toolearn about faster recovery options, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>  
