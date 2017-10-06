---
title: aaaMigrate il Data Warehouse di tooSQL soluzione | Documenti Microsoft
description: Materiale sussidiario di migrazione per portare la piattaforma di soluzione tooAzure SQL Data Warehouse.
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
ms.openlocfilehash: 27b51f15247603f054070f360ede7f24541c0288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-solution-tooazure-sql-data-warehouse"></a><span data-ttu-id="6ea1f-103">Eseguire la migrazione del tooAzure soluzione SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="6ea1f-103">Migrate your solution tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="6ea1f-104">Che cosa comporta la migrazione di un tooAzure di soluzioni di database SQL Data Warehouse esistente, vedere.</span><span class="sxs-lookup"><span data-stu-id="6ea1f-104">See what's involved in migrating an existing database solution tooAzure SQL Data Warehouse.</span></span> 

## <a name="profile-your-workload"></a><span data-ttu-id="6ea1f-105">Profilatura del carico di lavoro</span><span class="sxs-lookup"><span data-stu-id="6ea1f-105">Profile your workload</span></span>
<span data-ttu-id="6ea1f-106">Prima della migrazione, si desidera toobe determinati che SQL Data Warehouse è una soluzione più adeguata hello per il carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="6ea1f-106">Before migrating, you want toobe certain SQL Data Warehouse is hello right solution for your workload.</span></span> <span data-ttu-id="6ea1f-107">SQL Data Warehouse è un analitica tooperform sistema distribuito progettato su dati di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="6ea1f-107">SQL Data Warehouse is a distributed system designed tooperform analytics on large data.</span></span>  <span data-ttu-id="6ea1f-108">Migrazione tooSQL Data Warehouse richiede alcune modifiche di progettazione che non sono troppo difficile toounderstand ma potrebbero richiedere alcuni tooimplement ora.</span><span class="sxs-lookup"><span data-stu-id="6ea1f-108">Migrating tooSQL Data Warehouse requires some design changes that are not too hard toounderstand but might take some time tooimplement.</span></span> <span data-ttu-id="6ea1f-109">Se l'azienda richiede un data warehouse di classe enterprise, i vantaggi di hello si ritiene opportuno sforzo hello.</span><span class="sxs-lookup"><span data-stu-id="6ea1f-109">If your business requires an enterprise-class data warehouse, hello benefits are worth hello effort.</span></span> <span data-ttu-id="6ea1f-110">Tuttavia, se non è necessario power hello di SQL Data Warehouse, è più conveniente toouse SQL Server o Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="6ea1f-110">However, if you don't need hello power of SQL Data Warehouse, it is more cost-effective toouse SQL Server or Azure SQL Database.</span></span>

<span data-ttu-id="6ea1f-111">Prendere in considerazione l'uso di SQL Data Warehouse nei casi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6ea1f-111">Consider using SQL Data Warehouse when you:</span></span>
- <span data-ttu-id="6ea1f-112">Si devono gestire uno o più terabyte di dati</span><span class="sxs-lookup"><span data-stu-id="6ea1f-112">Have one or more Terabytes of data</span></span>
- <span data-ttu-id="6ea1f-113">Piano toorun analitica su grandi quantità di dati</span><span class="sxs-lookup"><span data-stu-id="6ea1f-113">Plan toorun analytics on large amounts of data</span></span>
- <span data-ttu-id="6ea1f-114">È necessario hello archiviazione e calcolo tooscale possibilità</span><span class="sxs-lookup"><span data-stu-id="6ea1f-114">Need hello ability tooscale compute and storage</span></span> 
- <span data-ttu-id="6ea1f-115">Desidera toosave costi sospendendo quando non sono necessarie risorse di calcolo.</span><span class="sxs-lookup"><span data-stu-id="6ea1f-115">Want toosave costs by pausing compute resources when you don't need them.</span></span>

<span data-ttu-id="6ea1f-116">Non usare SQL Data Warehouse per carichi di lavoro operativi (OLTP) con queste esigenze:</span><span class="sxs-lookup"><span data-stu-id="6ea1f-116">Don't use SQL Data Warehouse for operational (OLTP) workloads that have:</span></span>
- <span data-ttu-id="6ea1f-117">Operazioni di lettura e scrittura molto frequenti</span><span class="sxs-lookup"><span data-stu-id="6ea1f-117">High frequency reads and writes</span></span>
- <span data-ttu-id="6ea1f-118">Numeri elevati di selezioni singleton</span><span class="sxs-lookup"><span data-stu-id="6ea1f-118">Large numbers of singleton selects</span></span>
- <span data-ttu-id="6ea1f-119">Volumi elevati di inserimenti di righe singole</span><span class="sxs-lookup"><span data-stu-id="6ea1f-119">High volumes of single row inserts</span></span>
- <span data-ttu-id="6ea1f-120">Elaborazioni riga per riga</span><span class="sxs-lookup"><span data-stu-id="6ea1f-120">Row by row processing needs</span></span>
- <span data-ttu-id="6ea1f-121">Formati non compatibili (JSON, XML)</span><span class="sxs-lookup"><span data-stu-id="6ea1f-121">Incompatible formats (JSON, XML)</span></span>


## <a name="plan-hello-migration"></a><span data-ttu-id="6ea1f-122">Migrazione del piano di hello</span><span class="sxs-lookup"><span data-stu-id="6ea1f-122">Plan hello migration</span></span>

<span data-ttu-id="6ea1f-123">Dopo aver scelto toomigrate un tooSQL soluzione esistente, Data Warehouse, è importante tooplan la migrazione di hello prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="6ea1f-123">Once you have decided toomigrate an existing solution tooSQL Data Warehouse, it is important tooplan hello migration before getting started.</span></span> 

<span data-ttu-id="6ea1f-124">Uno degli obiettivi di pianificazione è tooensure dei dati, gli schemi di tabella, e il codice sono compatibili con SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6ea1f-124">One goal of planning is tooensure your data, your table schemas, and your code are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="6ea1f-125">Esistono alcuni toowork differenze compatibilità intorno tra il sistema corrente e SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6ea1f-125">There are some compatibility differences toowork around between your current system and SQL Data Warehouse.</span></span> <span data-ttu-id="6ea1f-126">Inoltre, la migrazione di grandi quantità di dati tooAzure richiede tempo.</span><span class="sxs-lookup"><span data-stu-id="6ea1f-126">Plus, migrating large amounts of data tooAzure takes time.</span></span> <span data-ttu-id="6ea1f-127">Una pianificazione attenta consente di accelerare recupero tooAzure i dati.</span><span class="sxs-lookup"><span data-stu-id="6ea1f-127">Careful planning expedites getting your data tooAzure.</span></span> 

<span data-ttu-id="6ea1f-128">Un altro obiettivo della pianificazione è la progettazione di toomake tooensure regolazioni che la soluzione sfrutta hello prestazioni elevate delle query che SQL Data Warehouse è progettata tooprovide.</span><span class="sxs-lookup"><span data-stu-id="6ea1f-128">Another goal of planning is toomake design adjustments tooensure your solution takes advantage of hello high query performance SQL Data Warehouse is designed tooprovide.</span></span> <span data-ttu-id="6ea1f-129">Progettazione data warehouse per la scala introduce i modelli di progettazione e gli approcci tradizionali pertanto non sono sempre hello meglio.</span><span class="sxs-lookup"><span data-stu-id="6ea1f-129">Designing data warehouses for scale introduces different design patterns and so traditional approaches aren't always hello best.</span></span> <span data-ttu-id="6ea1f-130">Anche se è possibile apportare alcune modifiche di progettazione dopo la migrazione, apportare modifiche prima nel processo di hello consentirà di risparmiare tempo in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="6ea1f-130">Although you can make some design adjustments after migration, making changes sooner in hello process will save time later.</span></span>

<span data-ttu-id="6ea1f-131">tooperform correttamente una migrazione, è necessario toomigrate gli schemi di tabella, il codice e i dati.</span><span class="sxs-lookup"><span data-stu-id="6ea1f-131">tooperform a successful migration, you need toomigrate your table schemas, your code, and your data.</span></span> <span data-ttu-id="6ea1f-132">Per linee guida su questi aspetti della migrazione, vedere:</span><span class="sxs-lookup"><span data-stu-id="6ea1f-132">For guidance on these migration topics, see:</span></span>

-  [<span data-ttu-id="6ea1f-133">Eseguire la migrazione degli schemi</span><span class="sxs-lookup"><span data-stu-id="6ea1f-133">Migrate your schemas</span></span>](sql-data-warehouse-migrate-schema.md)
-  [<span data-ttu-id="6ea1f-134">Eseguire la migrazione del codice</span><span class="sxs-lookup"><span data-stu-id="6ea1f-134">Migrate your code</span></span>](sql-data-warehouse-migrate-code.md)
-  <span data-ttu-id="6ea1f-135">[Eseguire la migrazione dei dati](sql-data-warehouse-migrate-data.md).</span><span class="sxs-lookup"><span data-stu-id="6ea1f-135">[Migrate your data](sql-data-warehouse-migrate-data.md).</span></span> 

<!--
## Perform hello migration


## Deploy hello solution


## Validate hello migration

-->

## <a name="next-steps"></a><span data-ttu-id="6ea1f-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6ea1f-136">Next steps</span></span>
<span data-ttu-id="6ea1f-137">Hello CAT (Customer Advisory Team) dispone anche di alcuni un'ottima guida di SQL Data Warehouse, pubblicano tramite blog.</span><span class="sxs-lookup"><span data-stu-id="6ea1f-137">hello CAT (Customer Advisory Team) also has some great SQL Data Warehouse guidance, which they publish through blogs.</span></span>  <span data-ttu-id="6ea1f-138">Dare un'occhiata loro articolo [tooAzure di migrazione dei dati SQL Data Warehouse in pratica] [ Migrating data tooAzure SQL Data Warehouse in practice] per altro materiale sussidiario sulla migrazione.</span><span class="sxs-lookup"><span data-stu-id="6ea1f-138">Take a look at their article, [Migrating data tooAzure SQL Data Warehouse in practice][Migrating data tooAzure SQL Data Warehouse in practice] for additional guidance on migration.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data tooAzure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
