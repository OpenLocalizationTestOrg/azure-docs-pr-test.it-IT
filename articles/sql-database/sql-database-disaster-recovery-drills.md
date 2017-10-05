---
title: Esercitazioni per il ripristino di emergenza del database SQL | Documentazione Microsoft
description: Istruzioni e procedure consigliate relative all'uso del database SQL di Azure per eseguire esercitazioni per il ripristino di emergenza che consentono di mantenere la resilienza delle applicazioni aziendali cruciali in caso di errori e interruzioni del servizio.
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
ms.openlocfilehash: 1b1d65a41a794a566287dcffe3581ac58e2a965f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="performing-disaster-recovery-drill"></a><span data-ttu-id="0aec9-103">Esercitazione per il ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="0aec9-103">Performing Disaster Recovery Drill</span></span>
<span data-ttu-id="0aec9-104">È consigliabile verificare periodicamente la conformità delle applicazioni per il flusso di lavoro di ripristino.</span><span class="sxs-lookup"><span data-stu-id="0aec9-104">It is recommended that validation of application readiness for recovery workflow is performed periodically.</span></span> <span data-ttu-id="0aec9-105">La verifica del comportamento di un'applicazione e delle implicazioni legate alla perdita di dati e/o all'interruzione del servizio che comporta il failover è una buona norma di progettazione.</span><span class="sxs-lookup"><span data-stu-id="0aec9-105">Verifying the application behavior and implications of data loss and/or the disruption that failover involves is a good engineering practice.</span></span> <span data-ttu-id="0aec9-106">Inoltre, questa verifica è richiesta dalla maggior parte degli standard del settore come parte della certificazione di continuità aziendale.</span><span class="sxs-lookup"><span data-stu-id="0aec9-106">It is also a requirement by most industry standards as part of business continuity certification.</span></span>

<span data-ttu-id="0aec9-107">L'esercitazione per il ripristino di emergenza prevede l'esecuzione delle attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="0aec9-107">Performing a disaster recovery drill consists of:</span></span>

* <span data-ttu-id="0aec9-108">Simulazione dell'interruzione del livello dati</span><span class="sxs-lookup"><span data-stu-id="0aec9-108">Simulating data tier outage</span></span>
* <span data-ttu-id="0aec9-109">Ripristino</span><span class="sxs-lookup"><span data-stu-id="0aec9-109">Recovering</span></span>
* <span data-ttu-id="0aec9-110">Convalida dell'integrità dell'applicazione dopo il ripristino</span><span class="sxs-lookup"><span data-stu-id="0aec9-110">Validate application integrity post recovery</span></span>

<span data-ttu-id="0aec9-111">A seconda della modalità di [progettazione dell’applicazione per la continuità aziendale](sql-database-business-continuity.md), il flusso di lavoro dell'esercitazione può variare.</span><span class="sxs-lookup"><span data-stu-id="0aec9-111">Depending on how you [designed your application for business continuity](sql-database-business-continuity.md), the workflow to execute the drill can vary.</span></span> <span data-ttu-id="0aec9-112">Di seguito sono descritte le procedure consigliate per eseguire un'esercitazione per il ripristino di emergenza nel contesto del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="0aec9-112">Below we describe the best practices conducting a disaster recovery drill in the context of Azure SQL Database.</span></span>

## <a name="geo-restore"></a><span data-ttu-id="0aec9-113">Ripristino geografico</span><span class="sxs-lookup"><span data-stu-id="0aec9-113">Geo-restore</span></span>
<span data-ttu-id="0aec9-114">Per evitare il rischio di perdita di dati durante l'esecuzione di un'esercitazione per il ripristino di emergenza, è consigliabile usare un ambiente di test creando una copia dell'ambiente di produzione e usandolo per verificare il flusso di lavoro di failover dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0aec9-114">To prevent the potential data loss when conducting a disaster recovery drill, we recommend performing the drill using a test environment by creating a copy of the production environment and using it to verify the application’s failover workflow.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="0aec9-115">Simulazione dell'interruzione del servizio</span><span class="sxs-lookup"><span data-stu-id="0aec9-115">Outage simulation</span></span>
<span data-ttu-id="0aec9-116">Per simulare l'interruzione è possibile eliminare o rinominare il database di origine.</span><span class="sxs-lookup"><span data-stu-id="0aec9-116">To simulate the outage, you can delete or rename the source database.</span></span> <span data-ttu-id="0aec9-117">Ciò causa un errore di connettività dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0aec9-117">This causes application connectivity failures.</span></span>

#### <a name="recovery"></a><span data-ttu-id="0aec9-118">Ripristino</span><span class="sxs-lookup"><span data-stu-id="0aec9-118">Recovery</span></span>
* <span data-ttu-id="0aec9-119">Eseguire il ripristino geografico del database in un server diverso, come descritto [qui](sql-database-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="0aec9-119">Perform the geo-restore of the database into a different server as described [here](sql-database-disaster-recovery.md).</span></span>
* <span data-ttu-id="0aec9-120">Modificare la configurazione dell'applicazione per connettersi ai database ripristinati e seguire la guida [Configurare un database dopo il ripristino](sql-database-disaster-recovery.md) per completare il ripristino.</span><span class="sxs-lookup"><span data-stu-id="0aec9-120">Change the application configuration to connect to the recovered database and follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="0aec9-121">Convalida</span><span class="sxs-lookup"><span data-stu-id="0aec9-121">Validation</span></span>
* <span data-ttu-id="0aec9-122">Completare l'esercitazione verificando l'integrità dell'applicazione dopo il ripristino (inclusi stringhe di connessione, account di accesso, test di funzionalità di base o altre verifiche correlate alle procedure standard di convalida delle applicazioni).</span><span class="sxs-lookup"><span data-stu-id="0aec9-122">Complete the drill by verifying the application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="geo-replication"></a><span data-ttu-id="0aec9-123">Replica geografica</span><span class="sxs-lookup"><span data-stu-id="0aec9-123">Geo-replication</span></span>
<span data-ttu-id="0aec9-124">Per un database protetto mediante la replica geografica l'esercitazione comporta un failover pianificato per il database secondario.</span><span class="sxs-lookup"><span data-stu-id="0aec9-124">For a database that is protected using geo-replication the drill exercise involves planned failover to the secondary database.</span></span> <span data-ttu-id="0aec9-125">Il failover pianificato assicura che i database primario e secondario restino sincronizzati quando si invertono i ruoli.</span><span class="sxs-lookup"><span data-stu-id="0aec9-125">The planned failover ensures that the primary and the secondary databases remain in sync when the roles are switched.</span></span> <span data-ttu-id="0aec9-126">A differenza del failover non pianificato, questa operazione non comporta la perdita di dati, quindi l'esercitazione può essere realizzata nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="0aec9-126">Unlike the unplanned failover, this operation does not result in data loss, so the drill can be performed in the production environment.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="0aec9-127">Simulazione dell'interruzione del servizio</span><span class="sxs-lookup"><span data-stu-id="0aec9-127">Outage simulation</span></span>
<span data-ttu-id="0aec9-128">Per simulare l'interruzione è possibile disabilitare l'applicazione web o la macchina virtuale connessa al database.</span><span class="sxs-lookup"><span data-stu-id="0aec9-128">To simulate the outage, you can disable the web application or virtual machine connected to the database.</span></span> <span data-ttu-id="0aec9-129">Ciò genera errori di connessione per i client web.</span><span class="sxs-lookup"><span data-stu-id="0aec9-129">This results in the connectivity failures for the web clients.</span></span>

#### <a name="recovery"></a><span data-ttu-id="0aec9-130">Ripristino</span><span class="sxs-lookup"><span data-stu-id="0aec9-130">Recovery</span></span>
* <span data-ttu-id="0aec9-131">Assicurarsi che la configurazione dell'applicazione nell'area DR punti al database secondario precedente, che diventa un nuovo database primario completamente accessibile.</span><span class="sxs-lookup"><span data-stu-id="0aec9-131">Make sure the application configuration in the DR region points to the former secondary which becomes the fully accessible new primary.</span></span>
* <span data-ttu-id="0aec9-132">Eseguire [failover pianificato](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) per rendere il database secondario un nuovo database primario</span><span class="sxs-lookup"><span data-stu-id="0aec9-132">Perform [planned failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) to make the secondary database a new primary</span></span>
* <span data-ttu-id="0aec9-133">Seguire la guida [Configurare un database dopo il ripristino](sql-database-disaster-recovery.md) per completare il ripristino.</span><span class="sxs-lookup"><span data-stu-id="0aec9-133">Follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="0aec9-134">Convalida</span><span class="sxs-lookup"><span data-stu-id="0aec9-134">Validation</span></span>
* <span data-ttu-id="0aec9-135">Completare l'esercitazione verificando l'integrità dell'applicazione dopo il ripristino (inclusi stringhe di connessione, account di accesso, test di funzionalità di base o altre verifiche correlate alle procedure standard di convalida delle applicazioni).</span><span class="sxs-lookup"><span data-stu-id="0aec9-135">Complete the drill by verifying the application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0aec9-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0aec9-136">Next steps</span></span>
* <span data-ttu-id="0aec9-137">Per informazioni sugli scenari di continuità aziendale, vedere l'articolo relativo agli [scenari di continuità](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="0aec9-137">To learn about business continuity scenarios, see [Continuity scenarios](sql-database-business-continuity.md)</span></span>
* <span data-ttu-id="0aec9-138">Per informazioni sui backup automatici del database SQL di Azure, vedere [Backup automatici del database SQL](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="0aec9-138">To learn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span></span>
* <span data-ttu-id="0aec9-139">Per altre informazioni sull'uso dei backup automatici per il ripristino, vedere l'articolo relativo al [ripristino di un database dai backup avviati dal servizio](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="0aec9-139">To learn about using automated backups for recovery, see [restore a database from the service-initiated backups](sql-database-recovery-using-backups.md)</span></span>
* <span data-ttu-id="0aec9-140">Per altre informazioni sulle opzioni di ripristino più veloci, vedere [Panoramica: Replica geografica attiva per il database SQL di Azure](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0aec9-140">To learn about faster recovery options, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>  
