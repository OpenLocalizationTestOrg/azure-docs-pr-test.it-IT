---
title: aaaManage calcolo power in Azure SQL Data Warehouse (panoramica) | Documenti Microsoft
description: "Funzionalità relative alla scalabilità orizzontale delle prestazioni in Azure SQL Data Warehouse. Scalabilità orizzontale grazie alla regolazione Dwu o sospendere e riprendere toosave risorse di calcolo dei costi."
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
ms.openlocfilehash: 1ffbe8d694ac181eaeb6f585a2cee87a570ed7d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a><span data-ttu-id="ab677-104">Gestire la potenza di calcolo in Azure SQL Data Warehouse (Panoramica)</span><span class="sxs-lookup"><span data-stu-id="ab677-104">Manage compute power in Azure SQL Data Warehouse (Overview)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ab677-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ab677-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="ab677-106">Portale</span><span class="sxs-lookup"><span data-stu-id="ab677-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="ab677-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab677-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="ab677-108">REST</span><span class="sxs-lookup"><span data-stu-id="ab677-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="ab677-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="ab677-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<span data-ttu-id="ab677-110">architettura di SQL Data Warehouse di Hello separa l'archiviazione e calcolo, consentendo di ogni tooscale in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="ab677-110">hello architecture of SQL Data Warehouse separates storage and compute, allowing each tooscale independently.</span></span> <span data-ttu-id="ab677-111">Di conseguenza, calcolo può essere scalato toomeet prestazioni richieste indipendente della quantità di hello di dati.</span><span class="sxs-lookup"><span data-stu-id="ab677-111">As a result, compute can be scaled toomeet performance demands independent of hello amount of data.</span></span> <span data-ttu-id="ab677-112">Come conseguenza logica di questa architettura, la [fatturazione][billed] è separata per calcolo e archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ab677-112">A natural consequence of this architecture is that [billing][billed] for compute and storage is separate.</span></span> 

<span data-ttu-id="ab677-113">Questa panoramica descrive la scalabilità orizzontale con SQL Data Warehouse e come tooutilize hello sospendere, riprendere e funzionalità di scalabilità di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ab677-113">This overview describes how scale out works with SQL Data Warehouse and how tooutilize hello pause, resume, and scale capabilities of SQL Data Warehouse.</span></span> <span data-ttu-id="ab677-114">Consultare hello [del data warehouse di unità (Dwu)] [ data warehouse units (DWUs)] toolearn pagina correlazione Dwu e prestazioni.</span><span class="sxs-lookup"><span data-stu-id="ab677-114">Consult hello [data warehouse units (DWUs)][data warehouse units (DWUs)] page toolearn how DWUs and performance are related.</span></span> 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a><span data-ttu-id="ab677-115">Funzionamento delle operazioni di gestione del calcolo in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ab677-115">How compute management operations work in SQL Data Warehouse</span></span>
<span data-ttu-id="ab677-116">architettura di Hello per SQL Data Warehouse è costituita da un nodo del controllo, nodi di calcolo e hello a livello di archiviazione distribuiti tra le distribuzioni di 60.</span><span class="sxs-lookup"><span data-stu-id="ab677-116">hello architecture for SQL Data Warehouse consists of a control node, compute nodes, and hello storage layer spread across 60 distributions.</span></span> 

<span data-ttu-id="ab677-117">Durante una sessione attiva normale in SQL Data Warehouse, nodo head del sistema gestisce i metadati di hello e contiene query optimizer di hello distribuita.</span><span class="sxs-lookup"><span data-stu-id="ab677-117">During a normal active session in SQL Data Warehouse, your system's head node manages hello metadata and contains hello distributed query optimizer.</span></span> <span data-ttu-id="ab677-118">Al di sotto del nodo head si trovano i nodi di calcolo e il livello di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ab677-118">Beneath this head node are your compute nodes and your storage layer.</span></span> <span data-ttu-id="ab677-119">Per un numero di DWU di 400, il sistema dispone di un nodo head, quattro nodi di calcolo e il livello di archiviazione hello, composta da 60 distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="ab677-119">For a DWU 400, your system has one head node, four compute nodes, and hello storage layer, consisting of 60 distributions.</span></span> 

<span data-ttu-id="ab677-120">Quando si essere sottoposto a una scala o sospesa l'operazione, sistema hello innanzitutto termina tutte le query in ingresso e quindi eseguire il rollback delle transazioni tooensure uno stato coerente.</span><span class="sxs-lookup"><span data-stu-id="ab677-120">When you undergo a scale or pause operation, hello system first kills all incoming queries and then rolls back transactions tooensure a consistent state.</span></span> <span data-ttu-id="ab677-121">Per le operazioni di scalabilità, quest'ultima si verificherà solamente al completamento del rollback di transazione.</span><span class="sxs-lookup"><span data-stu-id="ab677-121">For scale operations, scaling will only occur once this transactional rollback has completed.</span></span> <span data-ttu-id="ab677-122">Per un'operazione di scalabilità verticale, disposizioni sistema hello hello numero di nodi di calcolo molto desiderato e quindi inizia a livello di archiviazione toohello nodi calcolo hello ricollegamento.</span><span class="sxs-lookup"><span data-stu-id="ab677-122">For a scale-up operation, hello system provisions hello extra desired number of compute nodes, and then begins reattaching hello compute nodes toohello storage layer.</span></span> <span data-ttu-id="ab677-123">Per un'operazione di scalabilità orizzontale, hello nodi non necessari vengono rilasciati e nodi di calcolo rimanenti hello ricollegare stessi toohello numero appropriato di distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="ab677-123">For a scale-down operation, hello unneeded nodes are released and hello remaining compute nodes reattach themselves toohello appropriate number of distributions.</span></span> <span data-ttu-id="ab677-124">Per un'operazione di sospensione, tutte di calcolo vengono rilasciati i nodi e il sistema verrà sottoposta ad un'ampia gamma di metadati operazioni tooleave sistema finale in uno stato stabile.</span><span class="sxs-lookup"><span data-stu-id="ab677-124">For a pause operation, all compute nodes are released and your system will undergo a variety of metadata operations tooleave your final system in a stable state.</span></span>

| <span data-ttu-id="ab677-125">DWU</span><span class="sxs-lookup"><span data-stu-id="ab677-125">DWU</span></span>  | <span data-ttu-id="ab677-126">\# di nodi di calcolo</span><span class="sxs-lookup"><span data-stu-id="ab677-126">\#of compute nodes</span></span> | <span data-ttu-id="ab677-127">\# di distribuzioni per nodo</span><span class="sxs-lookup"><span data-stu-id="ab677-127">\# of distributions per node</span></span> |
| ---- | ------------------ | ---------------------------- |
| <span data-ttu-id="ab677-128">100</span><span class="sxs-lookup"><span data-stu-id="ab677-128">100</span></span>  | <span data-ttu-id="ab677-129">1</span><span class="sxs-lookup"><span data-stu-id="ab677-129">1</span></span>                  | <span data-ttu-id="ab677-130">60</span><span class="sxs-lookup"><span data-stu-id="ab677-130">60</span></span>                           |
| <span data-ttu-id="ab677-131">200</span><span class="sxs-lookup"><span data-stu-id="ab677-131">200</span></span>  | <span data-ttu-id="ab677-132">2</span><span class="sxs-lookup"><span data-stu-id="ab677-132">2</span></span>                  | <span data-ttu-id="ab677-133">30</span><span class="sxs-lookup"><span data-stu-id="ab677-133">30</span></span>                           |
| <span data-ttu-id="ab677-134">300</span><span class="sxs-lookup"><span data-stu-id="ab677-134">300</span></span>  | <span data-ttu-id="ab677-135">3</span><span class="sxs-lookup"><span data-stu-id="ab677-135">3</span></span>                  | <span data-ttu-id="ab677-136">20</span><span class="sxs-lookup"><span data-stu-id="ab677-136">20</span></span>                           |
| <span data-ttu-id="ab677-137">400</span><span class="sxs-lookup"><span data-stu-id="ab677-137">400</span></span>  | <span data-ttu-id="ab677-138">4</span><span class="sxs-lookup"><span data-stu-id="ab677-138">4</span></span>                  | <span data-ttu-id="ab677-139">15</span><span class="sxs-lookup"><span data-stu-id="ab677-139">15</span></span>                           |
| <span data-ttu-id="ab677-140">500</span><span class="sxs-lookup"><span data-stu-id="ab677-140">500</span></span>  | <span data-ttu-id="ab677-141">5</span><span class="sxs-lookup"><span data-stu-id="ab677-141">5</span></span>                  | <span data-ttu-id="ab677-142">12</span><span class="sxs-lookup"><span data-stu-id="ab677-142">12</span></span>                           |
| <span data-ttu-id="ab677-143">600</span><span class="sxs-lookup"><span data-stu-id="ab677-143">600</span></span>  | <span data-ttu-id="ab677-144">6</span><span class="sxs-lookup"><span data-stu-id="ab677-144">6</span></span>                  | <span data-ttu-id="ab677-145">10</span><span class="sxs-lookup"><span data-stu-id="ab677-145">10</span></span>                           |
| <span data-ttu-id="ab677-146">1000</span><span class="sxs-lookup"><span data-stu-id="ab677-146">1000</span></span> | <span data-ttu-id="ab677-147">10</span><span class="sxs-lookup"><span data-stu-id="ab677-147">10</span></span>                 | <span data-ttu-id="ab677-148">6</span><span class="sxs-lookup"><span data-stu-id="ab677-148">6</span></span>                            |
| <span data-ttu-id="ab677-149">1200</span><span class="sxs-lookup"><span data-stu-id="ab677-149">1200</span></span> | <span data-ttu-id="ab677-150">12</span><span class="sxs-lookup"><span data-stu-id="ab677-150">12</span></span>                 | <span data-ttu-id="ab677-151">5</span><span class="sxs-lookup"><span data-stu-id="ab677-151">5</span></span>                            |
| <span data-ttu-id="ab677-152">1500</span><span class="sxs-lookup"><span data-stu-id="ab677-152">1500</span></span> | <span data-ttu-id="ab677-153">15</span><span class="sxs-lookup"><span data-stu-id="ab677-153">15</span></span>                 | <span data-ttu-id="ab677-154">4</span><span class="sxs-lookup"><span data-stu-id="ab677-154">4</span></span>                            |
| <span data-ttu-id="ab677-155">2000</span><span class="sxs-lookup"><span data-stu-id="ab677-155">2000</span></span> | <span data-ttu-id="ab677-156">20</span><span class="sxs-lookup"><span data-stu-id="ab677-156">20</span></span>                 | <span data-ttu-id="ab677-157">3</span><span class="sxs-lookup"><span data-stu-id="ab677-157">3</span></span>                            |
| <span data-ttu-id="ab677-158">3000</span><span class="sxs-lookup"><span data-stu-id="ab677-158">3000</span></span> | <span data-ttu-id="ab677-159">30</span><span class="sxs-lookup"><span data-stu-id="ab677-159">30</span></span>                 | <span data-ttu-id="ab677-160">2</span><span class="sxs-lookup"><span data-stu-id="ab677-160">2</span></span>                            |
| <span data-ttu-id="ab677-161">6000</span><span class="sxs-lookup"><span data-stu-id="ab677-161">6000</span></span> | <span data-ttu-id="ab677-162">60</span><span class="sxs-lookup"><span data-stu-id="ab677-162">60</span></span>                 | <span data-ttu-id="ab677-163">1</span><span class="sxs-lookup"><span data-stu-id="ab677-163">1</span></span>                            |

<span data-ttu-id="ab677-164">sono tre funzioni principali di Hello per la gestione di calcolo:</span><span class="sxs-lookup"><span data-stu-id="ab677-164">hello three primary functions for managing compute are:</span></span>

1. <span data-ttu-id="ab677-165">Sospendi</span><span class="sxs-lookup"><span data-stu-id="ab677-165">Pause</span></span>
2. <span data-ttu-id="ab677-166">Riprendi</span><span class="sxs-lookup"><span data-stu-id="ab677-166">Resume</span></span>
3. <span data-ttu-id="ab677-167">Scalabilità</span><span class="sxs-lookup"><span data-stu-id="ab677-167">Scale</span></span>

<span data-ttu-id="ab677-168">Ognuna di queste operazioni potrebbe richiedere diversi minuti toocomplete.</span><span class="sxs-lookup"><span data-stu-id="ab677-168">Each of these operations may take several minutes toocomplete.</span></span> <span data-ttu-id="ab677-169">Se si scala, sospensione/ripresa automaticamente, è consigliabile tooimplement logica tooensure determinate operazioni completate prima di procedere con un'altra azione.</span><span class="sxs-lookup"><span data-stu-id="ab677-169">If you are scaling/pausing/resuming automatically, you may want tooimplement logic tooensure that certain operations have been completed before proceeding with another action.</span></span> 

<span data-ttu-id="ab677-170">Verifica dello stato del database hello tramite vari endpoint consentirà toocorrectly implementare automazione di tali operazioni.</span><span class="sxs-lookup"><span data-stu-id="ab677-170">Checking hello database state through various endpoints will allow you toocorrectly implement automation of such operations.</span></span> <span data-ttu-id="ab677-171">portale Hello invierà una notifica al completamento di un'operazione e hello database corrente dello stato, ma non per il controllo a livello di codice di stato.</span><span class="sxs-lookup"><span data-stu-id="ab677-171">hello portal will provide notification upon completion of an operation and hello databases current state but does not allow for programmatic checking of state.</span></span> 

>  [!NOTE]
>
>  <span data-ttu-id="ab677-172">La funzionalità di gestione del calcolo non è presente in tutti gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="ab677-172">Compute management functionality does not exist across all endpoints.</span></span>
>
>  

|              | <span data-ttu-id="ab677-173">Sospensione/ripresa</span><span class="sxs-lookup"><span data-stu-id="ab677-173">Pause/Resume</span></span> | <span data-ttu-id="ab677-174">Scalabilità</span><span class="sxs-lookup"><span data-stu-id="ab677-174">Scale</span></span> | <span data-ttu-id="ab677-175">Controllare lo stato del database</span><span class="sxs-lookup"><span data-stu-id="ab677-175">Check database state</span></span> |
| ------------ | ------------ | ----- | -------------------- |
| <span data-ttu-id="ab677-176">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ab677-176">Azure portal</span></span> | <span data-ttu-id="ab677-177">Sì</span><span class="sxs-lookup"><span data-stu-id="ab677-177">Yes</span></span>          | <span data-ttu-id="ab677-178">Sì</span><span class="sxs-lookup"><span data-stu-id="ab677-178">Yes</span></span>   | <span data-ttu-id="ab677-179">**No**</span><span class="sxs-lookup"><span data-stu-id="ab677-179">**No**</span></span>               |
| <span data-ttu-id="ab677-180">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab677-180">PowerShell</span></span>   | <span data-ttu-id="ab677-181">Sì</span><span class="sxs-lookup"><span data-stu-id="ab677-181">Yes</span></span>          | <span data-ttu-id="ab677-182">Sì</span><span class="sxs-lookup"><span data-stu-id="ab677-182">Yes</span></span>   | <span data-ttu-id="ab677-183">Sì</span><span class="sxs-lookup"><span data-stu-id="ab677-183">Yes</span></span>                  |
| <span data-ttu-id="ab677-184">API REST</span><span class="sxs-lookup"><span data-stu-id="ab677-184">REST API</span></span>     | <span data-ttu-id="ab677-185">Sì</span><span class="sxs-lookup"><span data-stu-id="ab677-185">Yes</span></span>          | <span data-ttu-id="ab677-186">Sì</span><span class="sxs-lookup"><span data-stu-id="ab677-186">Yes</span></span>   | <span data-ttu-id="ab677-187">Sì</span><span class="sxs-lookup"><span data-stu-id="ab677-187">Yes</span></span>                  |
| <span data-ttu-id="ab677-188">T-SQL</span><span class="sxs-lookup"><span data-stu-id="ab677-188">T-SQL</span></span>        | <span data-ttu-id="ab677-189">**No**</span><span class="sxs-lookup"><span data-stu-id="ab677-189">**No**</span></span>       | <span data-ttu-id="ab677-190">Sì</span><span class="sxs-lookup"><span data-stu-id="ab677-190">Yes</span></span>   | <span data-ttu-id="ab677-191">Sì</span><span class="sxs-lookup"><span data-stu-id="ab677-191">Yes</span></span>                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="ab677-192">Ridimensionare le risorse di calcolo</span><span class="sxs-lookup"><span data-stu-id="ab677-192">Scale compute</span></span>

<span data-ttu-id="ab677-193">Le prestazioni in SQL Data Warehouse vengono misurate in [Unità Data Warehouse (DWU)][data warehouse units (DWUs)], una misura astratta delle risorse di calcolo come CPU, memoria e larghezza di banda I/O.</span><span class="sxs-lookup"><span data-stu-id="ab677-193">Performance in SQL Data Warehouse is measured in [data warehouse units (DWUs)][data warehouse units (DWUs)] which is an abstracted measure of compute resources such as CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="ab677-194">Un utente che desidera tooscale le prestazioni del sistema relativi a tale scopo in vari modi, ad esempio tramite il portale di hello, T-SQL e le API REST.</span><span class="sxs-lookup"><span data-stu-id="ab677-194">A user who wishes tooscale their system's performance can do so through various means, such as through hello portal, T-SQL, and REST APIs.</span></span> 

### <a name="how-do-i-scale-compute"></a><span data-ttu-id="ab677-195">In che modo è possibile ridimensionare le risorse di calcolo?</span><span class="sxs-lookup"><span data-stu-id="ab677-195">How do I scale compute?</span></span>
<span data-ttu-id="ab677-196">Potenza di calcolo viene gestita SQL Data Warehouse modificando l'impostazione DWU hello.</span><span class="sxs-lookup"><span data-stu-id="ab677-196">Compute power is managed for you SQL Data Warehouse by changing hello DWU setting.</span></span> <span data-ttu-id="ab677-197">Le prestazioni aumentano in modo [lineare][linearly] man mano che si aggiungono più DWU per determinate operazioni.</span><span class="sxs-lookup"><span data-stu-id="ab677-197">Performance increases [linearly][linearly] as you add more DWU for certain operations.</span></span>  <span data-ttu-id="ab677-198">Esistono varie offerte di DWU per assicurare un cambiamento netto delle prestazioni durante il ridimensionamento verticale del sistema.</span><span class="sxs-lookup"><span data-stu-id="ab677-198">We offer DWU offerings that ensure that your performance will change noticeably when you scale your system up or down.</span></span> 

<span data-ttu-id="ab677-199">tooadjust Dwu, è possibile utilizzare uno di questi singoli metodi.</span><span class="sxs-lookup"><span data-stu-id="ab677-199">tooadjust DWUs, you can use any of these individual methods.</span></span>

* <span data-ttu-id="ab677-200">[Ridimensionare la potenza di calcolo con il portale di Azure][Scale compute power with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="ab677-200">[Scale compute power with Azure portal][Scale compute power with Azure portal]</span></span>
* <span data-ttu-id="ab677-201">[Ridimensionare la potenza di calcolo con PowerShell][Scale compute power with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="ab677-201">[Scale compute power with PowerShell][Scale compute power with PowerShell]</span></span>
* <span data-ttu-id="ab677-202">[Ridimensionare la potenza di calcolo con le API REST][Scale compute power with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="ab677-202">[Scale compute power with REST APIs][Scale compute power with REST APIs]</span></span>
* <span data-ttu-id="ab677-203">[Ridimensionare la potenza di calcolo con TSQL][Scale compute power with TSQL]</span><span class="sxs-lookup"><span data-stu-id="ab677-203">[Scale compute power with TSQL][Scale compute power with TSQL]</span></span>

### <a name="how-many-dwus-should-i-use"></a><span data-ttu-id="ab677-204">Quante DWU è consigliabile usare?</span><span class="sxs-lookup"><span data-stu-id="ab677-204">How many DWUs should I use?</span></span>

<span data-ttu-id="ab677-205">toounderstand è il valore DWU ideale, provare a scalabilità verticale e l'esecuzione di alcune query dopo il caricamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="ab677-205">toounderstand what your ideal DWU value is, try scaling up and down, and running a few queries after loading your data.</span></span> <span data-ttu-id="ab677-206">Poiché il ridimensionamento è rapido, è possibile provare diversi livelli di prestazioni in un'ora o meno.</span><span class="sxs-lookup"><span data-stu-id="ab677-206">Since scaling is quick, you can try various performance levels in an hour or less.</span></span> 

> [!Note] 
> <span data-ttu-id="ab677-207">SQL Data Warehouse è progettata tooprocess grandi quantità di dati.</span><span class="sxs-lookup"><span data-stu-id="ab677-207">SQL Data Warehouse is designed tooprocess large amounts of data.</span></span> <span data-ttu-id="ab677-208">toosee capacità true per la scalabilità, soprattutto in più grande Dwu, si desidera toouse grandi set di dati che si avvicina o supera 1 TB.</span><span class="sxs-lookup"><span data-stu-id="ab677-208">toosee its true capabilities for scaling, especially at larger DWUs, you want toouse a large data set which approaches or exceeds 1 TB.</span></span>

<span data-ttu-id="ab677-209">Indicazioni per la ricerca hello DWU migliore per il carico di lavoro:</span><span class="sxs-lookup"><span data-stu-id="ab677-209">Recommendations for finding hello best DWU for your workload:</span></span>

1. <span data-ttu-id="ab677-210">Per un data warehouse in sviluppo, iniziare con un numero più limitato di prestazioni DWU.</span><span class="sxs-lookup"><span data-stu-id="ab677-210">For a data warehouse in development, begin by selecting a smaller DWU performance level.</span></span>  <span data-ttu-id="ab677-211">Un buon punto di partenza è DW400 o DW200.</span><span class="sxs-lookup"><span data-stu-id="ab677-211">A good starting point is DW400 or DW200.</span></span>
2. <span data-ttu-id="ab677-212">Monitorare le prestazioni dell'applicazione, osservare il numero di hello di Dwu selezionato confrontato prestazioni toohello che è osservare.</span><span class="sxs-lookup"><span data-stu-id="ab677-212">Monitor your application performance, observing hello number of DWUs selected compared toohello performance you observe.</span></span>
3. <span data-ttu-id="ab677-213">Determinare la quantità delle prestazioni di velocità superiore o inferiore devono essere per si tooreach hello ottimale livello di prestazioni per le proprie esigenze, presupponendo una scala lineare.</span><span class="sxs-lookup"><span data-stu-id="ab677-213">Determine how much faster or slower performance should be for you tooreach hello optimum performance level for your requirements by assuming linear scale.</span></span>
4. <span data-ttu-id="ab677-214">Aumentare o diminuire il numero di hello di Dwu in proporzione toohow molto più veloce o lenta desiderato tooperform il carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ab677-214">Increase or decrease hello number of DWUs in proportion toohow much faster or slower you want your workload tooperform.</span></span> 
5. <span data-ttu-id="ab677-215">Continuare ad apportare modifiche finché non si raggiunge un livello di prestazioni ottimale per i propri requisiti aziendali.</span><span class="sxs-lookup"><span data-stu-id="ab677-215">Continue making adjustments until you reach an optimum performance level for your business requirements.</span></span>

> [!NOTE]
>
> <span data-ttu-id="ab677-216">Le prestazioni delle query aumentano solo con la parallelizzazione ulteriori se lavoro hello può essere suddivise tra nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="ab677-216">Query performance only increases with more parallelization if hello work can be split between compute nodes.</span></span> <span data-ttu-id="ab677-217">Se si ritiene che il ridimensionamento non sta cambiando le prestazioni, estrarre il nostro toocheck articoli se i dati non viene distribuiti o se si stanno introducendo una grande quantità di spostamento dei dati di ottimizzazione delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="ab677-217">If you find that scaling is not changing your performance, please check out our performance tuning articles toocheck whether your data is unevenly distributed or if you are introducing a large amount of data movement.</span></span> 

### <a name="when-should-i-scale-dwus"></a><span data-ttu-id="ab677-218">Quando è necessario ridimensionare le DWU?</span><span class="sxs-lookup"><span data-stu-id="ab677-218">When should I scale DWUs?</span></span>
<span data-ttu-id="ab677-219">Scalabilità Dwu modifica hello scenari importanti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ab677-219">Scaling DWUs alters hello following important scenarios:</span></span>

1. <span data-ttu-id="ab677-220">Modifica in modo lineare delle prestazioni del sistema hello per le analisi, le aggregazioni e un'istruzione CTAS istruzioni</span><span class="sxs-lookup"><span data-stu-id="ab677-220">Linearly changing performance of hello system for scans, aggregations, and CTAS statements</span></span>
2. <span data-ttu-id="ab677-221">Aumentare il numero di hello di reader e writer durante il caricamento con PolyBase</span><span class="sxs-lookup"><span data-stu-id="ab677-221">Increasing hello number of readers and writers when loading with PolyBase</span></span>
3. <span data-ttu-id="ab677-222">Numero massimo di query simultanee e slot di concorrenza</span><span class="sxs-lookup"><span data-stu-id="ab677-222">Maximum number of concurrent queries and concurrency slots</span></span>

<span data-ttu-id="ab677-223">Indicazioni relative al tooscale Dwu:</span><span class="sxs-lookup"><span data-stu-id="ab677-223">Recommendations for when tooscale DWUs:</span></span>

1. <span data-ttu-id="ab677-224">Prima di eseguire un'operazione di caricamento o trasformazione di quantità di dati elevate, ridimensionare le DWU in modo che i dati siano disponibili più rapidamente.</span><span class="sxs-lookup"><span data-stu-id="ab677-224">Before you perform a heavy data loading or transformation operation, scale up DWUs so that your data is available more quickly.</span></span>
2. <span data-ttu-id="ab677-225">Durante le ore, la scalabilità tooaccommodate un numero maggiore di query simultanee.</span><span class="sxs-lookup"><span data-stu-id="ab677-225">During peak business hours, scale tooaccommodate larger numbers of concurrent queries.</span></span> 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="ab677-226">Sospendere le risorse di calcolo</span><span class="sxs-lookup"><span data-stu-id="ab677-226">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="ab677-227">toopause un database, utilizzare uno di questi singoli metodi.</span><span class="sxs-lookup"><span data-stu-id="ab677-227">toopause a database, use any of these individual methods.</span></span>

* <span data-ttu-id="ab677-228">[Sospendere le risorse di calcolo con il portale di Azure][Pause compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="ab677-228">[Pause compute with Azure portal][Pause compute with Azure portal]</span></span>
* <span data-ttu-id="ab677-229">[Sospendere le risorse di calcolo con PowerShell][Pause compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="ab677-229">[Pause compute with PowerShell][Pause compute with PowerShell]</span></span>
* <span data-ttu-id="ab677-230">[Sospendere le risorse di calcolo con le API REST][Pause compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="ab677-230">[Pause compute with REST APIs][Pause compute with REST APIs]</span></span>

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="ab677-231">Riavviare le risorse di calcolo</span><span class="sxs-lookup"><span data-stu-id="ab677-231">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="ab677-232">tooresume un database, utilizzare uno di questi singoli metodi.</span><span class="sxs-lookup"><span data-stu-id="ab677-232">tooresume a database, use any of these individual methods.</span></span>

* <span data-ttu-id="ab677-233">[Riavviare le risorse di calcolo con il portale di Azure][Resume compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="ab677-233">[Resume compute with Azure portal][Resume compute with Azure portal]</span></span>
* <span data-ttu-id="ab677-234">[Riavviare le risorse di calcolo con PowerShell][Resume compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="ab677-234">[Resume compute with PowerShell][Resume compute with PowerShell]</span></span>
* <span data-ttu-id="ab677-235">[Riavviare le risorse di calcolo con le API REST][Resume compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="ab677-235">[Resume compute with REST APIs][Resume compute with REST APIs]</span></span>

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="ab677-236">Controllare lo stato del database</span><span class="sxs-lookup"><span data-stu-id="ab677-236">Check database state</span></span> 

<span data-ttu-id="ab677-237">tooresume un database, utilizzare uno di questi singoli metodi.</span><span class="sxs-lookup"><span data-stu-id="ab677-237">tooresume a database, use any of these individual methods.</span></span>

- <span data-ttu-id="ab677-238">[Controllare lo stato del database con T-SQL][Check database state with T-SQL]</span><span class="sxs-lookup"><span data-stu-id="ab677-238">[Check database state with T-SQL][Check database state with T-SQL]</span></span>
- <span data-ttu-id="ab677-239">[Controllare lo stato del database con PowerShell][Check database state with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="ab677-239">[Check database state with PowerShell][Check database state with PowerShell]</span></span>
- <span data-ttu-id="ab677-240">[Controllare lo stato del database con le API REST][Check database state with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="ab677-240">[Check database state with REST APIs][Check database state with REST APIs]</span></span>

## <a name="permissions"></a><span data-ttu-id="ab677-241">Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="ab677-241">Permissions</span></span>

<span data-ttu-id="ab677-242">Scala database hello richiede autorizzazioni hello descritte in [ALTER DATABASE][ALTER DATABASE].</span><span class="sxs-lookup"><span data-stu-id="ab677-242">Scaling hello database requires hello permissions described in [ALTER DATABASE][ALTER DATABASE].</span></span>  <span data-ttu-id="ab677-243">Sospendere e riprendere richiedono hello [collaboratore DB SQL] [ SQL DB Contributor] autorizzazione, in particolare Microsoft.Sql/servers/databases/action.</span><span class="sxs-lookup"><span data-stu-id="ab677-243">Pause and Resume require hello [SQL DB Contributor][SQL DB Contributor] permission, specifically Microsoft.Sql/servers/databases/action.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="ab677-244">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ab677-244">Next steps</span></span>
<span data-ttu-id="ab677-245">Fare riferimento toohello toohelp articoli è comprendere alcuni concetti di prestazioni chiave aggiuntive seguenti:</span><span class="sxs-lookup"><span data-stu-id="ab677-245">Refer toohello following articles toohelp you understand some additional key performance concepts:</span></span>

* <span data-ttu-id="ab677-246">[Gestione della concorrenza e del carico di lavoro][Workload and concurrency management]</span><span class="sxs-lookup"><span data-stu-id="ab677-246">[Workload and concurrency management][Workload and concurrency management]</span></span>
* <span data-ttu-id="ab677-247">[Panoramica delle tabelle][Table design overview]</span><span class="sxs-lookup"><span data-stu-id="ab677-247">[Table design overview][Table design overview]</span></span>
* <span data-ttu-id="ab677-248">[Distribuzione di tabelle][Table distribution]</span><span class="sxs-lookup"><span data-stu-id="ab677-248">[Table distribution][Table distribution]</span></span>
* <span data-ttu-id="ab677-249">[Indicizzazione di tabelle][Table indexing]</span><span class="sxs-lookup"><span data-stu-id="ab677-249">[Table indexing][Table indexing]</span></span>
* <span data-ttu-id="ab677-250">[Partizionamento di tabelle][Table partitioning]</span><span class="sxs-lookup"><span data-stu-id="ab677-250">[Table partitioning][Table partitioning]</span></span>
* <span data-ttu-id="ab677-251">[Statistiche delle tabelle][Table statistics]</span><span class="sxs-lookup"><span data-stu-id="ab677-251">[Table statistics][Table statistics]</span></span>
* <span data-ttu-id="ab677-252">[Procedure consigliate][Best practices]</span><span class="sxs-lookup"><span data-stu-id="ab677-252">[Best practices][Best practices]</span></span>

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
