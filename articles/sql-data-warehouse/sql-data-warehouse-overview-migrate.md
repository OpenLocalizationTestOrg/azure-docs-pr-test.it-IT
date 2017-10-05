---
title: Eseguire la migrazione della soluzione in SQL Data Warehouse | Microsoft Docs
description: Indicazioni sulla migrazione per spostare la soluzione nella piattaforma Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 198365eb-7451-4222-b99c-d1d9ef687f1b
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/27/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 771b9456e66b8a1e41f72340b695b19e2adaf793
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-solution-to-azure-sql-data-warehouse"></a><span data-ttu-id="14fa9-103">Eseguire la migrazione della soluzione in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="14fa9-103">Migrate your solution to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="14fa9-104">Scoprire cosa comporta la migrazione di una soluzione di database esistente ad Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="14fa9-104">See what's involved in migrating an existing database solution to Azure SQL Data Warehouse.</span></span> 

## <a name="profile-your-workload"></a><span data-ttu-id="14fa9-105">Profilatura del carico di lavoro</span><span class="sxs-lookup"><span data-stu-id="14fa9-105">Profile your workload</span></span>
<span data-ttu-id="14fa9-106">Prima di eseguire la migrazione, è opportuno assicurarsi che SQL Data Warehouse sia la soluzione ideale per il carico di lavoro specifico.</span><span class="sxs-lookup"><span data-stu-id="14fa9-106">Before migrating, you want to be certain SQL Data Warehouse is the right solution for your workload.</span></span> <span data-ttu-id="14fa9-107">SQL Data Warehouse è un sistema distribuito progettato per eseguire analisi su dati di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="14fa9-107">SQL Data Warehouse is a distributed system designed to perform analytics on large data.</span></span>  <span data-ttu-id="14fa9-108">La migrazione a SQL Data Warehouse richiede alcune modifiche di progettazione non troppo difficili da comprendere, ma la cui implementazione potrebbe richiedere del tempo.</span><span class="sxs-lookup"><span data-stu-id="14fa9-108">Migrating to SQL Data Warehouse requires some design changes that are not too hard to understand but might take some time to implement.</span></span> <span data-ttu-id="14fa9-109">Se l'azienda richiede un data warehouse di classe enterprise, i vantaggi valgono la pena.</span><span class="sxs-lookup"><span data-stu-id="14fa9-109">If your business requires an enterprise-class data warehouse, the benefits are worth the effort.</span></span> <span data-ttu-id="14fa9-110">Tuttavia, se non è necessaria la potenza di SQL Data Warehouse, è più conveniente usare SQL Server o il database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="14fa9-110">However, if you don't need the power of SQL Data Warehouse, it is more cost-effective to use SQL Server or Azure SQL Database.</span></span>

<span data-ttu-id="14fa9-111">Prendere in considerazione l'uso di SQL Data Warehouse nei casi seguenti:</span><span class="sxs-lookup"><span data-stu-id="14fa9-111">Consider using SQL Data Warehouse when you:</span></span>
- <span data-ttu-id="14fa9-112">Si devono gestire uno o più terabyte di dati</span><span class="sxs-lookup"><span data-stu-id="14fa9-112">Have one or more Terabytes of data</span></span>
- <span data-ttu-id="14fa9-113">Si prevede di eseguire operazioni di analisi su grandi quantità di dati</span><span class="sxs-lookup"><span data-stu-id="14fa9-113">Plan to run analytics on large amounts of data</span></span>
- <span data-ttu-id="14fa9-114">È necessario avere la possibilità di ridimensionare le capacità di calcolo e archiviazione</span><span class="sxs-lookup"><span data-stu-id="14fa9-114">Need the ability to scale compute and storage</span></span> 
- <span data-ttu-id="14fa9-115">Si vuole risparmiare sui costi tramite la sospensione delle risorse di calcolo quando non sono necessarie.</span><span class="sxs-lookup"><span data-stu-id="14fa9-115">Want to save costs by pausing compute resources when you don't need them.</span></span>

<span data-ttu-id="14fa9-116">Non usare SQL Data Warehouse per carichi di lavoro operativi (OLTP) con queste esigenze:</span><span class="sxs-lookup"><span data-stu-id="14fa9-116">Don't use SQL Data Warehouse for operational (OLTP) workloads that have:</span></span>
- <span data-ttu-id="14fa9-117">Operazioni di lettura e scrittura molto frequenti</span><span class="sxs-lookup"><span data-stu-id="14fa9-117">High frequency reads and writes</span></span>
- <span data-ttu-id="14fa9-118">Numeri elevati di selezioni singleton</span><span class="sxs-lookup"><span data-stu-id="14fa9-118">Large numbers of singleton selects</span></span>
- <span data-ttu-id="14fa9-119">Volumi elevati di inserimenti di righe singole</span><span class="sxs-lookup"><span data-stu-id="14fa9-119">High volumes of single row inserts</span></span>
- <span data-ttu-id="14fa9-120">Elaborazioni riga per riga</span><span class="sxs-lookup"><span data-stu-id="14fa9-120">Row by row processing needs</span></span>
- <span data-ttu-id="14fa9-121">Formati non compatibili (JSON, XML)</span><span class="sxs-lookup"><span data-stu-id="14fa9-121">Incompatible formats (JSON, XML)</span></span>


## <a name="plan-the-migration"></a><span data-ttu-id="14fa9-122">Pianificare la migrazione</span><span class="sxs-lookup"><span data-stu-id="14fa9-122">Plan the migration</span></span>

<span data-ttu-id="14fa9-123">Dopo aver deciso di eseguire la migrazione di una soluzione esistente a SQL Data Warehouse, è importante pianificare la migrazione prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="14fa9-123">Once you have decided to migrate an existing solution to SQL Data Warehouse, it is important to plan the migration before getting started.</span></span> 

<span data-ttu-id="14fa9-124">Uno degli obiettivi di pianificazione è assicurarsi che i dati, gli schemi di tabella e il codice siano compatibili con SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="14fa9-124">One goal of planning is to ensure your data, your table schemas, and your code are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="14fa9-125">Esistono alcune differenze di compatibilità da risolvere tra il sistema corrente e SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="14fa9-125">There are some compatibility differences to work around between your current system and SQL Data Warehouse.</span></span> <span data-ttu-id="14fa9-126">Inoltre, la migrazione di grandi quantità di dati in Azure richiede del tempo.</span><span class="sxs-lookup"><span data-stu-id="14fa9-126">Plus, migrating large amounts of data to Azure takes time.</span></span> <span data-ttu-id="14fa9-127">Una pianificazione attenta consente di velocizzare il trasferimento dei dati in Azure.</span><span class="sxs-lookup"><span data-stu-id="14fa9-127">Careful planning expedites getting your data to Azure.</span></span> 

<span data-ttu-id="14fa9-128">Un altro obiettivo della pianificazione è apportare alcune modifiche di progettazione per garantire che la soluzione possa sfruttare le prestazioni elevate per le query per cui è progettato SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="14fa9-128">Another goal of planning is to make design adjustments to ensure your solution takes advantage of the high query performance SQL Data Warehouse is designed to provide.</span></span> <span data-ttu-id="14fa9-129">La progettazione di data warehouse ai fini della scalabilità introduce modelli di progettazione diversi, pertanto gli approcci tradizionali non si rivelano sempre ottimali.</span><span class="sxs-lookup"><span data-stu-id="14fa9-129">Designing data warehouses for scale introduces different design patterns and so traditional approaches aren't always the best.</span></span> <span data-ttu-id="14fa9-130">Anche se è possibile apportare alcune modifiche di progettazione dopo la migrazione, introdurre le modifiche il prima possibile nel processo consentirà di risparmiare tempo in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="14fa9-130">Although you can make some design adjustments after migration, making changes sooner in the process will save time later.</span></span>

<span data-ttu-id="14fa9-131">Per eseguire correttamente una migrazione, è necessario eseguire la migrazione di schemi di tabella, codice e dati.</span><span class="sxs-lookup"><span data-stu-id="14fa9-131">To perform a successful migration, you need to migrate your table schemas, your code, and your data.</span></span> <span data-ttu-id="14fa9-132">Per linee guida su questi aspetti della migrazione, vedere:</span><span class="sxs-lookup"><span data-stu-id="14fa9-132">For guidance on these migration topics, see:</span></span>

-  [<span data-ttu-id="14fa9-133">Eseguire la migrazione degli schemi</span><span class="sxs-lookup"><span data-stu-id="14fa9-133">Migrate your schemas</span></span>](sql-data-warehouse-migrate-schema.md)
-  [<span data-ttu-id="14fa9-134">Eseguire la migrazione del codice</span><span class="sxs-lookup"><span data-stu-id="14fa9-134">Migrate your code</span></span>](sql-data-warehouse-migrate-code.md)
-  <span data-ttu-id="14fa9-135">[Eseguire la migrazione dei dati](sql-data-warehouse-migrate-data.md).</span><span class="sxs-lookup"><span data-stu-id="14fa9-135">[Migrate your data](sql-data-warehouse-migrate-data.md).</span></span> 

<!--
## Perform the migration


## Deploy the solution


## Validate the migration

-->

## <a name="next-steps"></a><span data-ttu-id="14fa9-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="14fa9-136">Next steps</span></span>
<span data-ttu-id="14fa9-137">Anche il team CAT (Customer Advisory Team) offre indicazioni molto utili per SQL Data Warehouse, pubblicate tramite blog.</span><span class="sxs-lookup"><span data-stu-id="14fa9-137">The CAT (Customer Advisory Team) also has some great SQL Data Warehouse guidance, which they publish through blogs.</span></span>  <span data-ttu-id="14fa9-138">Per altre istruzioni sulla migrazione, vedere l'articolo [Migrating data to Azure SQL Data Warehouse in practice][Migrating data to Azure SQL Data Warehouse in practice] (Migrazione dei dati in Azure SQL Data Warehouse in pratica).</span><span class="sxs-lookup"><span data-stu-id="14fa9-138">Take a look at their article, [Migrating data to Azure SQL Data Warehouse in practice][Migrating data to Azure SQL Data Warehouse in practice] for additional guidance on migration.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data to Azure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
