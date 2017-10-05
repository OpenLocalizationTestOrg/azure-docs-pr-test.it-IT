---
title: Gestire la potenza di calcolo in Azure SQL Data Warehouse (Panoramica) | Documentazione Microsoft
description: "Funzionalità relative alla scalabilità orizzontale delle prestazioni in Azure SQL Data Warehouse. Eseguire il ridimensionamento modificando le impostazioni DWU o sospendendo e riavviando le risorse di calcolo per ridurre i costi."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: e13a82b0-abfe-429f-ac3c-f2b6789a70c6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/22/2017
ms.author: elbutter
ms.openlocfilehash: abe22f542a79714f6e894870872ee6b76ffe7633
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a><span data-ttu-id="2db43-104">Gestire la potenza di calcolo in Azure SQL Data Warehouse (Panoramica)</span><span class="sxs-lookup"><span data-stu-id="2db43-104">Manage compute power in Azure SQL Data Warehouse (Overview)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2db43-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2db43-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="2db43-106">Portale</span><span class="sxs-lookup"><span data-stu-id="2db43-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="2db43-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2db43-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="2db43-108">REST</span><span class="sxs-lookup"><span data-stu-id="2db43-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="2db43-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="2db43-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<span data-ttu-id="2db43-110">L'architettura di SQL Data Warehouse separa le risorse di archiviazione e calcolo consentendo a entrambe di eseguire il ridimensionamento in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="2db43-110">The architecture of SQL Data Warehouse separates storage and compute, allowing each to scale independently.</span></span> <span data-ttu-id="2db43-111">Pertanto, è possibile ridimensionare il calcolo per soddisfare le richieste di prestazioni, a prescindere dalla quantità di dati.</span><span class="sxs-lookup"><span data-stu-id="2db43-111">As a result, compute can be scaled to meet performance demands independent of the amount of data.</span></span> <span data-ttu-id="2db43-112">Come conseguenza logica di questa architettura, la [fatturazione][billed] è separata per calcolo e archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2db43-112">A natural consequence of this architecture is that [billing][billed] for compute and storage is separate.</span></span> 

<span data-ttu-id="2db43-113">Questa panoramica descrive il funzionamento della scalabilità orizzontale con SQL Data Warehouse e come usare le funzionalità di sospensione, ripresa e ridimensionamento di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2db43-113">This overview describes how scale out works with SQL Data Warehouse and how to utilize the pause, resume, and scale capabilities of SQL Data Warehouse.</span></span> <span data-ttu-id="2db43-114">Vedere la pagina sulle [Unità Data Warehouse (DWU)][data warehouse units (DWUs)] per altre informazioni sulla correlazione tra DWU e prestazioni.</span><span class="sxs-lookup"><span data-stu-id="2db43-114">Consult the [data warehouse units (DWUs)][data warehouse units (DWUs)] page to learn how DWUs and performance are related.</span></span> 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a><span data-ttu-id="2db43-115">Funzionamento delle operazioni di gestione del calcolo in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="2db43-115">How compute management operations work in SQL Data Warehouse</span></span>
<span data-ttu-id="2db43-116">L'architettura di SQL Data Warehouse consiste in un nodo di controllo, nodi di calcolo e di un livello di archiviazione suddiviso in 60 distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="2db43-116">The architecture for SQL Data Warehouse consists of a control node, compute nodes, and the storage layer spread across 60 distributions.</span></span> 

<span data-ttu-id="2db43-117">Durante una normale sessione attiva in SQL Data Warehouse, il nodo head del sistema gestisce i metadati e contiene l'ottimizzazione delle query distribuite.</span><span class="sxs-lookup"><span data-stu-id="2db43-117">During a normal active session in SQL Data Warehouse, your system's head node manages the metadata and contains the distributed query optimizer.</span></span> <span data-ttu-id="2db43-118">Al di sotto del nodo head si trovano i nodi di calcolo e il livello di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2db43-118">Beneath this head node are your compute nodes and your storage layer.</span></span> <span data-ttu-id="2db43-119">Considerando 400 DWU, il sistema dispone di un nodo head, di quattro nodi di calcolo e del livello di archiviazione, per 60 distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="2db43-119">For a DWU 400, your system has one head node, four compute nodes, and the storage layer, consisting of 60 distributions.</span></span> 

<span data-ttu-id="2db43-120">Quando si eseguono operazioni di ridimensionamento o sospensione, il sistema termina innanzitutto le query in entrata, quindi esegue il rollback delle transazioni per garantire la coerenza.</span><span class="sxs-lookup"><span data-stu-id="2db43-120">When you undergo a scale or pause operation, the system first kills all incoming queries and then rolls back transactions to ensure a consistent state.</span></span> <span data-ttu-id="2db43-121">Per le operazioni di scalabilità, quest'ultima si verificherà solamente al completamento del rollback di transazione.</span><span class="sxs-lookup"><span data-stu-id="2db43-121">For scale operations, scaling will only occur once this transactional rollback has completed.</span></span> <span data-ttu-id="2db43-122">Per le operazioni di scalabilità verticale con aumento di prestazioni, il sistema esegue il provisioning del numero di nodi di calcolo aggiuntivi desiderati, quindi inizia a ricollegare i nodi di calcolo al livello di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2db43-122">For a scale-up operation, the system provisions the extra desired number of compute nodes, and then begins reattaching the compute nodes to the storage layer.</span></span> <span data-ttu-id="2db43-123">Per un'operazione di scalabilità verticale con diminuzione delle prestazioni, i nodi non più necessari vengono rilasciati e quelli rimanenti si ricollegano al numero appropriato di distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="2db43-123">For a scale-down operation, the unneeded nodes are released and the remaining compute nodes reattach themselves to the appropriate number of distributions.</span></span> <span data-ttu-id="2db43-124">Per un'operazione di sospensione, vengono rilasciati tutti i nodi di calcolo e nel sistema vengono eseguite varie operazioni di metadati per lasciarlo in uno stato stabile.</span><span class="sxs-lookup"><span data-stu-id="2db43-124">For a pause operation, all compute nodes are released and your system will undergo a variety of metadata operations to leave your final system in a stable state.</span></span>

| <span data-ttu-id="2db43-125">DWU</span><span class="sxs-lookup"><span data-stu-id="2db43-125">DWU</span></span>  | <span data-ttu-id="2db43-126">\# di nodi di calcolo</span><span class="sxs-lookup"><span data-stu-id="2db43-126">\#of compute nodes</span></span> | <span data-ttu-id="2db43-127">\# di distribuzioni per nodo</span><span class="sxs-lookup"><span data-stu-id="2db43-127">\# of distributions per node</span></span> |
| ---- | ------------------ | ---------------------------- |
| <span data-ttu-id="2db43-128">100</span><span class="sxs-lookup"><span data-stu-id="2db43-128">100</span></span>  | <span data-ttu-id="2db43-129">1</span><span class="sxs-lookup"><span data-stu-id="2db43-129">1</span></span>                  | <span data-ttu-id="2db43-130">60</span><span class="sxs-lookup"><span data-stu-id="2db43-130">60</span></span>                           |
| <span data-ttu-id="2db43-131">200</span><span class="sxs-lookup"><span data-stu-id="2db43-131">200</span></span>  | <span data-ttu-id="2db43-132">2</span><span class="sxs-lookup"><span data-stu-id="2db43-132">2</span></span>                  | <span data-ttu-id="2db43-133">30</span><span class="sxs-lookup"><span data-stu-id="2db43-133">30</span></span>                           |
| <span data-ttu-id="2db43-134">300</span><span class="sxs-lookup"><span data-stu-id="2db43-134">300</span></span>  | <span data-ttu-id="2db43-135">3</span><span class="sxs-lookup"><span data-stu-id="2db43-135">3</span></span>                  | <span data-ttu-id="2db43-136">20</span><span class="sxs-lookup"><span data-stu-id="2db43-136">20</span></span>                           |
| <span data-ttu-id="2db43-137">400</span><span class="sxs-lookup"><span data-stu-id="2db43-137">400</span></span>  | <span data-ttu-id="2db43-138">4</span><span class="sxs-lookup"><span data-stu-id="2db43-138">4</span></span>                  | <span data-ttu-id="2db43-139">15</span><span class="sxs-lookup"><span data-stu-id="2db43-139">15</span></span>                           |
| <span data-ttu-id="2db43-140">500</span><span class="sxs-lookup"><span data-stu-id="2db43-140">500</span></span>  | <span data-ttu-id="2db43-141">5</span><span class="sxs-lookup"><span data-stu-id="2db43-141">5</span></span>                  | <span data-ttu-id="2db43-142">12</span><span class="sxs-lookup"><span data-stu-id="2db43-142">12</span></span>                           |
| <span data-ttu-id="2db43-143">600</span><span class="sxs-lookup"><span data-stu-id="2db43-143">600</span></span>  | <span data-ttu-id="2db43-144">6</span><span class="sxs-lookup"><span data-stu-id="2db43-144">6</span></span>                  | <span data-ttu-id="2db43-145">10</span><span class="sxs-lookup"><span data-stu-id="2db43-145">10</span></span>                           |
| <span data-ttu-id="2db43-146">1000</span><span class="sxs-lookup"><span data-stu-id="2db43-146">1000</span></span> | <span data-ttu-id="2db43-147">10</span><span class="sxs-lookup"><span data-stu-id="2db43-147">10</span></span>                 | <span data-ttu-id="2db43-148">6</span><span class="sxs-lookup"><span data-stu-id="2db43-148">6</span></span>                            |
| <span data-ttu-id="2db43-149">1200</span><span class="sxs-lookup"><span data-stu-id="2db43-149">1200</span></span> | <span data-ttu-id="2db43-150">12</span><span class="sxs-lookup"><span data-stu-id="2db43-150">12</span></span>                 | <span data-ttu-id="2db43-151">5</span><span class="sxs-lookup"><span data-stu-id="2db43-151">5</span></span>                            |
| <span data-ttu-id="2db43-152">1500</span><span class="sxs-lookup"><span data-stu-id="2db43-152">1500</span></span> | <span data-ttu-id="2db43-153">15</span><span class="sxs-lookup"><span data-stu-id="2db43-153">15</span></span>                 | <span data-ttu-id="2db43-154">4</span><span class="sxs-lookup"><span data-stu-id="2db43-154">4</span></span>                            |
| <span data-ttu-id="2db43-155">2000</span><span class="sxs-lookup"><span data-stu-id="2db43-155">2000</span></span> | <span data-ttu-id="2db43-156">20</span><span class="sxs-lookup"><span data-stu-id="2db43-156">20</span></span>                 | <span data-ttu-id="2db43-157">3</span><span class="sxs-lookup"><span data-stu-id="2db43-157">3</span></span>                            |
| <span data-ttu-id="2db43-158">3000</span><span class="sxs-lookup"><span data-stu-id="2db43-158">3000</span></span> | <span data-ttu-id="2db43-159">30</span><span class="sxs-lookup"><span data-stu-id="2db43-159">30</span></span>                 | <span data-ttu-id="2db43-160">2</span><span class="sxs-lookup"><span data-stu-id="2db43-160">2</span></span>                            |
| <span data-ttu-id="2db43-161">6000</span><span class="sxs-lookup"><span data-stu-id="2db43-161">6000</span></span> | <span data-ttu-id="2db43-162">60</span><span class="sxs-lookup"><span data-stu-id="2db43-162">60</span></span>                 | <span data-ttu-id="2db43-163">1</span><span class="sxs-lookup"><span data-stu-id="2db43-163">1</span></span>                            |

<span data-ttu-id="2db43-164">Le tre funzioni principali per la gestione del calcolo sono:</span><span class="sxs-lookup"><span data-stu-id="2db43-164">The three primary functions for managing compute are:</span></span>

1. <span data-ttu-id="2db43-165">Sospendi</span><span class="sxs-lookup"><span data-stu-id="2db43-165">Pause</span></span>
2. <span data-ttu-id="2db43-166">Riprendi</span><span class="sxs-lookup"><span data-stu-id="2db43-166">Resume</span></span>
3. <span data-ttu-id="2db43-167">Scalabilità</span><span class="sxs-lookup"><span data-stu-id="2db43-167">Scale</span></span>

<span data-ttu-id="2db43-168">Ciascuna di queste operazioni può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="2db43-168">Each of these operations may take several minutes to complete.</span></span> <span data-ttu-id="2db43-169">In caso di operazioni automatiche di ridimensionamento/sospensione/ripresa, si potrebbe voler implementare la logica per assicurare il completamento di determinate operazioni prima di procedere con altre.</span><span class="sxs-lookup"><span data-stu-id="2db43-169">If you are scaling/pausing/resuming automatically, you may want to implement logic to ensure that certain operations have been completed before proceeding with another action.</span></span> 

<span data-ttu-id="2db43-170">Verificando lo stato del database in vari endpoint sarà possibile implementare correttamente l'automazione di tali operazioni.</span><span class="sxs-lookup"><span data-stu-id="2db43-170">Checking the database state through various endpoints will allow you to correctly implement automation of such operations.</span></span> <span data-ttu-id="2db43-171">Il portale invierà notifiche una volta completata un'operazione e indicherà lo stato corrente del database. Tuttavia non è possibile verificare lo stato in maniera programmatica.</span><span class="sxs-lookup"><span data-stu-id="2db43-171">The portal will provide notification upon completion of an operation and the databases current state but does not allow for programmatic checking of state.</span></span> 

>  [!NOTE]
>
>  <span data-ttu-id="2db43-172">La funzionalità di gestione del calcolo non è presente in tutti gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="2db43-172">Compute management functionality does not exist across all endpoints.</span></span>
>
>  

|              | <span data-ttu-id="2db43-173">Sospensione/ripresa</span><span class="sxs-lookup"><span data-stu-id="2db43-173">Pause/Resume</span></span> | <span data-ttu-id="2db43-174">Scalabilità</span><span class="sxs-lookup"><span data-stu-id="2db43-174">Scale</span></span> | <span data-ttu-id="2db43-175">Controllare lo stato del database</span><span class="sxs-lookup"><span data-stu-id="2db43-175">Check database state</span></span> |
| ------------ | ------------ | ----- | -------------------- |
| <span data-ttu-id="2db43-176">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2db43-176">Azure portal</span></span> | <span data-ttu-id="2db43-177">Sì</span><span class="sxs-lookup"><span data-stu-id="2db43-177">Yes</span></span>          | <span data-ttu-id="2db43-178">Sì</span><span class="sxs-lookup"><span data-stu-id="2db43-178">Yes</span></span>   | <span data-ttu-id="2db43-179">**No**</span><span class="sxs-lookup"><span data-stu-id="2db43-179">**No**</span></span>               |
| <span data-ttu-id="2db43-180">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2db43-180">PowerShell</span></span>   | <span data-ttu-id="2db43-181">Sì</span><span class="sxs-lookup"><span data-stu-id="2db43-181">Yes</span></span>          | <span data-ttu-id="2db43-182">Sì</span><span class="sxs-lookup"><span data-stu-id="2db43-182">Yes</span></span>   | <span data-ttu-id="2db43-183">Sì</span><span class="sxs-lookup"><span data-stu-id="2db43-183">Yes</span></span>                  |
| <span data-ttu-id="2db43-184">API REST</span><span class="sxs-lookup"><span data-stu-id="2db43-184">REST API</span></span>     | <span data-ttu-id="2db43-185">Sì</span><span class="sxs-lookup"><span data-stu-id="2db43-185">Yes</span></span>          | <span data-ttu-id="2db43-186">Sì</span><span class="sxs-lookup"><span data-stu-id="2db43-186">Yes</span></span>   | <span data-ttu-id="2db43-187">Sì</span><span class="sxs-lookup"><span data-stu-id="2db43-187">Yes</span></span>                  |
| <span data-ttu-id="2db43-188">T-SQL</span><span class="sxs-lookup"><span data-stu-id="2db43-188">T-SQL</span></span>        | <span data-ttu-id="2db43-189">**No**</span><span class="sxs-lookup"><span data-stu-id="2db43-189">**No**</span></span>       | <span data-ttu-id="2db43-190">Sì</span><span class="sxs-lookup"><span data-stu-id="2db43-190">Yes</span></span>   | <span data-ttu-id="2db43-191">Sì</span><span class="sxs-lookup"><span data-stu-id="2db43-191">Yes</span></span>                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="2db43-192">Ridimensionare le risorse di calcolo</span><span class="sxs-lookup"><span data-stu-id="2db43-192">Scale compute</span></span>

<span data-ttu-id="2db43-193">Le prestazioni in SQL Data Warehouse vengono misurate in [Unità Data Warehouse (DWU)][data warehouse units (DWUs)], una misura astratta delle risorse di calcolo come CPU, memoria e larghezza di banda I/O.</span><span class="sxs-lookup"><span data-stu-id="2db43-193">Performance in SQL Data Warehouse is measured in [data warehouse units (DWUs)][data warehouse units (DWUs)] which is an abstracted measure of compute resources such as CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="2db43-194">Un utente che desidera aumentare le prestazioni del sistema può farlo in vari modi, ad esempio tramite il portale, T-SQL e le API REST.</span><span class="sxs-lookup"><span data-stu-id="2db43-194">A user who wishes to scale their system's performance can do so through various means, such as through the portal, T-SQL, and REST APIs.</span></span> 

### <a name="how-do-i-scale-compute"></a><span data-ttu-id="2db43-195">In che modo è possibile ridimensionare le risorse di calcolo?</span><span class="sxs-lookup"><span data-stu-id="2db43-195">How do I scale compute?</span></span>
<span data-ttu-id="2db43-196">La potenza di calcolo è gestita da SQL Data Warehouse modificando l'impostazione DWU.</span><span class="sxs-lookup"><span data-stu-id="2db43-196">Compute power is managed for you SQL Data Warehouse by changing the DWU setting.</span></span> <span data-ttu-id="2db43-197">Le prestazioni aumentano in modo [lineare][linearly] man mano che si aggiungono più DWU per determinate operazioni.</span><span class="sxs-lookup"><span data-stu-id="2db43-197">Performance increases [linearly][linearly] as you add more DWU for certain operations.</span></span>  <span data-ttu-id="2db43-198">Esistono varie offerte di DWU per assicurare un cambiamento netto delle prestazioni durante il ridimensionamento verticale del sistema.</span><span class="sxs-lookup"><span data-stu-id="2db43-198">We offer DWU offerings that ensure that your performance will change noticeably when you scale your system up or down.</span></span> 

<span data-ttu-id="2db43-199">Per modificare le DWU, è possibile usare uno di questi metodi singoli.</span><span class="sxs-lookup"><span data-stu-id="2db43-199">To adjust DWUs, you can use any of these individual methods.</span></span>

* <span data-ttu-id="2db43-200">[Ridimensionare la potenza di calcolo con il portale di Azure][Scale compute power with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="2db43-200">[Scale compute power with Azure portal][Scale compute power with Azure portal]</span></span>
* <span data-ttu-id="2db43-201">[Ridimensionare la potenza di calcolo con PowerShell][Scale compute power with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="2db43-201">[Scale compute power with PowerShell][Scale compute power with PowerShell]</span></span>
* <span data-ttu-id="2db43-202">[Ridimensionare la potenza di calcolo con le API REST][Scale compute power with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="2db43-202">[Scale compute power with REST APIs][Scale compute power with REST APIs]</span></span>
* <span data-ttu-id="2db43-203">[Ridimensionare la potenza di calcolo con TSQL][Scale compute power with TSQL]</span><span class="sxs-lookup"><span data-stu-id="2db43-203">[Scale compute power with TSQL][Scale compute power with TSQL]</span></span>

### <a name="how-many-dwus-should-i-use"></a><span data-ttu-id="2db43-204">Quante DWU è consigliabile usare?</span><span class="sxs-lookup"><span data-stu-id="2db43-204">How many DWUs should I use?</span></span>

<span data-ttu-id="2db43-205">Per comprendere il valore di DWU ideale, provare ad aumentarlo e diminuirlo ed eseguire alcune query dopo il caricamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="2db43-205">To understand what your ideal DWU value is, try scaling up and down, and running a few queries after loading your data.</span></span> <span data-ttu-id="2db43-206">Poiché il ridimensionamento è rapido, è possibile provare diversi livelli di prestazioni in un'ora o meno.</span><span class="sxs-lookup"><span data-stu-id="2db43-206">Since scaling is quick, you can try various performance levels in an hour or less.</span></span> 

> [!Note] 
> <span data-ttu-id="2db43-207">SQL Data Warehouse è progettato per elaborare grandi quantità di dati.</span><span class="sxs-lookup"><span data-stu-id="2db43-207">SQL Data Warehouse is designed to process large amounts of data.</span></span> <span data-ttu-id="2db43-208">Per constatarne le reali funzionalità di ridimensionamento, specialmente per DWU di dimensioni maggiori, si consiglia di usare un set di dati di grandi dimensioni, possibilmente 1 TB o più.</span><span class="sxs-lookup"><span data-stu-id="2db43-208">To see its true capabilities for scaling, especially at larger DWUs, you want to use a large data set which approaches or exceeds 1 TB.</span></span>

<span data-ttu-id="2db43-209">Raccomandazioni per individuare l'impostazione DWU più adatta al proprio carico di lavoro:</span><span class="sxs-lookup"><span data-stu-id="2db43-209">Recommendations for finding the best DWU for your workload:</span></span>

1. <span data-ttu-id="2db43-210">Per un data warehouse in sviluppo, iniziare con un numero più limitato di prestazioni DWU.</span><span class="sxs-lookup"><span data-stu-id="2db43-210">For a data warehouse in development, begin by selecting a smaller DWU performance level.</span></span>  <span data-ttu-id="2db43-211">Un buon punto di partenza è DW400 o DW200.</span><span class="sxs-lookup"><span data-stu-id="2db43-211">A good starting point is DW400 or DW200.</span></span>
2. <span data-ttu-id="2db43-212">Monitorare le prestazioni dell'applicazione, osservare che il numero di DWUs selezionato in relazione alle prestazioni che si osservano.</span><span class="sxs-lookup"><span data-stu-id="2db43-212">Monitor your application performance, observing the number of DWUs selected compared to the performance you observe.</span></span>
3. <span data-ttu-id="2db43-213">Determinare di quanto si vogliono aumentare o ridurre le prestazioni per raggiungere il livello ottimale per i propri requisiti presupponendo una scalabilità lineare.</span><span class="sxs-lookup"><span data-stu-id="2db43-213">Determine how much faster or slower performance should be for you to reach the optimum performance level for your requirements by assuming linear scale.</span></span>
4. <span data-ttu-id="2db43-214">Aumentare o diminuire il numero di DWU proporzionalmente alla velocità desiderata per le prestazioni del proprio carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="2db43-214">Increase or decrease the number of DWUs in proportion to how much faster or slower you want your workload to perform.</span></span> 
5. <span data-ttu-id="2db43-215">Continuare ad apportare modifiche finché non si raggiunge un livello di prestazioni ottimale per i propri requisiti aziendali.</span><span class="sxs-lookup"><span data-stu-id="2db43-215">Continue making adjustments until you reach an optimum performance level for your business requirements.</span></span>

> [!NOTE]
>
> <span data-ttu-id="2db43-216">Le prestazioni delle query aumentano con maggiore parallelizzazione solo se il lavoro può essere suddivise tra i nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="2db43-216">Query performance only increases with more parallelization if the work can be split between compute nodes.</span></span> <span data-ttu-id="2db43-217">Se si ritiene che la scalabilità non stia modificando le prestazioni, si consiglia di leggere gli articoli sull'ottimizzazione di queste ultime per verificare qualora i dati siano distribuiti in modo ineguale o se si stiano introducendo grandi quantità di movimenti di dati.</span><span class="sxs-lookup"><span data-stu-id="2db43-217">If you find that scaling is not changing your performance, please check out our performance tuning articles to check whether your data is unevenly distributed or if you are introducing a large amount of data movement.</span></span> 

### <a name="when-should-i-scale-dwus"></a><span data-ttu-id="2db43-218">Quando è necessario ridimensionare le DWU?</span><span class="sxs-lookup"><span data-stu-id="2db43-218">When should I scale DWUs?</span></span>
<span data-ttu-id="2db43-219">Il ridimensionamento delle DWU modifica i seguenti scenari importanti:</span><span class="sxs-lookup"><span data-stu-id="2db43-219">Scaling DWUs alters the following important scenarios:</span></span>

1. <span data-ttu-id="2db43-220">Modifica lineare delle prestazioni del sistema per le analisi, l'aggregazione e le istruzioni CTAS</span><span class="sxs-lookup"><span data-stu-id="2db43-220">Linearly changing performance of the system for scans, aggregations, and CTAS statements</span></span>
2. <span data-ttu-id="2db43-221">Aumento del numero di lettori e writer durante il caricamento con PolyBase</span><span class="sxs-lookup"><span data-stu-id="2db43-221">Increasing the number of readers and writers when loading with PolyBase</span></span>
3. <span data-ttu-id="2db43-222">Numero massimo di query simultanee e slot di concorrenza</span><span class="sxs-lookup"><span data-stu-id="2db43-222">Maximum number of concurrent queries and concurrency slots</span></span>

<span data-ttu-id="2db43-223">Raccomandazioni sul momento più indicato per il ridimensionamento delle DWU:</span><span class="sxs-lookup"><span data-stu-id="2db43-223">Recommendations for when to scale DWUs:</span></span>

1. <span data-ttu-id="2db43-224">Prima di eseguire un'operazione di caricamento o trasformazione di quantità di dati elevate, ridimensionare le DWU in modo che i dati siano disponibili più rapidamente.</span><span class="sxs-lookup"><span data-stu-id="2db43-224">Before you perform a heavy data loading or transformation operation, scale up DWUs so that your data is available more quickly.</span></span>
2. <span data-ttu-id="2db43-225">Durante le ore lavorative più intense, eseguire il ridimensionamento per poter ricevere un numero maggiori di query simultanee.</span><span class="sxs-lookup"><span data-stu-id="2db43-225">During peak business hours, scale to accommodate larger numbers of concurrent queries.</span></span> 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="2db43-226">Sospendere il calcolo</span><span class="sxs-lookup"><span data-stu-id="2db43-226">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="2db43-227">Per sospendere un database, usare uno di questi metodi singoli.</span><span class="sxs-lookup"><span data-stu-id="2db43-227">To pause a database, use any of these individual methods.</span></span>

* <span data-ttu-id="2db43-228">[Sospendere le risorse di calcolo con il portale di Azure][Pause compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="2db43-228">[Pause compute with Azure portal][Pause compute with Azure portal]</span></span>
* <span data-ttu-id="2db43-229">[Sospendere le risorse di calcolo con PowerShell][Pause compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="2db43-229">[Pause compute with PowerShell][Pause compute with PowerShell]</span></span>
* <span data-ttu-id="2db43-230">[Sospendere le risorse di calcolo con le API REST][Pause compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="2db43-230">[Pause compute with REST APIs][Pause compute with REST APIs]</span></span>

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="2db43-231">Riavviare le risorse di calcolo</span><span class="sxs-lookup"><span data-stu-id="2db43-231">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="2db43-232">Per riavviare un database, usare uno di questi metodi singoli.</span><span class="sxs-lookup"><span data-stu-id="2db43-232">To resume a database, use any of these individual methods.</span></span>

* <span data-ttu-id="2db43-233">[Riavviare le risorse di calcolo con il portale di Azure][Resume compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="2db43-233">[Resume compute with Azure portal][Resume compute with Azure portal]</span></span>
* <span data-ttu-id="2db43-234">[Riavviare le risorse di calcolo con PowerShell][Resume compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="2db43-234">[Resume compute with PowerShell][Resume compute with PowerShell]</span></span>
* <span data-ttu-id="2db43-235">[Riavviare le risorse di calcolo con le API REST][Resume compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="2db43-235">[Resume compute with REST APIs][Resume compute with REST APIs]</span></span>

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="2db43-236">Controllare lo stato del database</span><span class="sxs-lookup"><span data-stu-id="2db43-236">Check database state</span></span> 

<span data-ttu-id="2db43-237">Per riavviare un database, usare uno di questi metodi singoli.</span><span class="sxs-lookup"><span data-stu-id="2db43-237">To resume a database, use any of these individual methods.</span></span>

- <span data-ttu-id="2db43-238">[Controllare lo stato del database con T-SQL][Check database state with T-SQL]</span><span class="sxs-lookup"><span data-stu-id="2db43-238">[Check database state with T-SQL][Check database state with T-SQL]</span></span>
- <span data-ttu-id="2db43-239">[Controllare lo stato del database con PowerShell][Check database state with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="2db43-239">[Check database state with PowerShell][Check database state with PowerShell]</span></span>
- <span data-ttu-id="2db43-240">[Controllare lo stato del database con le API REST][Check database state with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="2db43-240">[Check database state with REST APIs][Check database state with REST APIs]</span></span>

## <a name="permissions"></a><span data-ttu-id="2db43-241">autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="2db43-241">Permissions</span></span>

<span data-ttu-id="2db43-242">Il ridimensionamento del database richiede le autorizzazioni descritte in [ALTER DATABASE][ALTER DATABASE].</span><span class="sxs-lookup"><span data-stu-id="2db43-242">Scaling the database requires the permissions described in [ALTER DATABASE][ALTER DATABASE].</span></span>  <span data-ttu-id="2db43-243">La sospensione e la ripresa richiedono l'autorizzazione [Collaboratore Database SQL][SQL DB Contributor], in particolare Microsoft.Sql/servers/databases/action.</span><span class="sxs-lookup"><span data-stu-id="2db43-243">Pause and Resume require the [SQL DB Contributor][SQL DB Contributor] permission, specifically Microsoft.Sql/servers/databases/action.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="2db43-244">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2db43-244">Next steps</span></span>
<span data-ttu-id="2db43-245">Per comprendere più facilmente altri concetti importanti sulle prestazioni, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="2db43-245">Refer to the following articles to help you understand some additional key performance concepts:</span></span>

* <span data-ttu-id="2db43-246">[Gestione della concorrenza e del carico di lavoro][Workload and concurrency management]</span><span class="sxs-lookup"><span data-stu-id="2db43-246">[Workload and concurrency management][Workload and concurrency management]</span></span>
* <span data-ttu-id="2db43-247">[Panoramica delle tabelle][Table design overview]</span><span class="sxs-lookup"><span data-stu-id="2db43-247">[Table design overview][Table design overview]</span></span>
* <span data-ttu-id="2db43-248">[Distribuzione di tabelle][Table distribution]</span><span class="sxs-lookup"><span data-stu-id="2db43-248">[Table distribution][Table distribution]</span></span>
* <span data-ttu-id="2db43-249">[Indicizzazione di tabelle][Table indexing]</span><span class="sxs-lookup"><span data-stu-id="2db43-249">[Table indexing][Table indexing]</span></span>
* <span data-ttu-id="2db43-250">[Partizionamento di tabelle][Table partitioning]</span><span class="sxs-lookup"><span data-stu-id="2db43-250">[Table partitioning][Table partitioning]</span></span>
* <span data-ttu-id="2db43-251">[Statistiche delle tabelle][Table statistics]</span><span class="sxs-lookup"><span data-stu-id="2db43-251">[Table statistics][Table statistics]</span></span>
* <span data-ttu-id="2db43-252">[Procedure consigliate][Best practices]</span><span class="sxs-lookup"><span data-stu-id="2db43-252">[Best practices][Best practices]</span></span>

<!--Image reference-->

<!--Article references-->
[data warehouse units (DWUs)]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[billed]: https://azure.microsoft.com/en-us/pricing/details/sql-data-warehouse/
[linearly]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[Scale compute power with Azure portal]: ./sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[Scale compute power with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#scale-compute-bk
[Scale compute power with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#scale-compute-bk
[Scale compute power with TSQL]: ./sql-data-warehouse-manage-compute-tsql.md#scale-compute-bk

[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md

[Pause compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#pause-compute-bk
[Pause compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#pause-compute-bk
[Pause compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#pause-compute-bk

[Resume compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#resume-compute-bk
[Resume compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#resume-compute-bk
[Resume compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#resume-compute-bk

[Check database state with T-SQL]: ./sql-data-warehouse-manage-compute-tsql.md#check-database-state-and-operation-progress
[Check database state with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#check-database-state
[Check database state with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#check-database-state

[Workload and concurrency management]: ./sql-data-warehouse-develop-concurrency.md
[Table design overview]: ./sql-data-warehouse-tables-overview.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexing]: ./sql-data-warehouse-tables-index.md
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Table statistics]: ./sql-data-warehouse-tables-statistics.md
[Best practices]: ./sql-data-warehouse-best-practices.md
[development overview]: ./sql-data-warehouse-overview-develop.md

[SQL DB Contributor]: ../active-directory/role-based-access-built-in-roles.md#sql-db-contributor

<!--MSDN references-->
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx

<!--Other Web references-->
[Azure portal]: http://portal.azure.com/
