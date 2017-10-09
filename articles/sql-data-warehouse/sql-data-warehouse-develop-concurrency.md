---
title: gestione aaaConcurrency e carico di lavoro in SQL Data Warehouse | Documenti Microsoft
description: Informazioni sulla gestione della concorrenza e del carico di lavoro nel Data Warehouse di SQL Azure per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 08/23/2017
ms.author: joeyong;barbkess;kavithaj
ms.openlocfilehash: 7f7e77aa687760252aed16573b609817ed9111c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a><span data-ttu-id="ed59c-103">Gestione della concorrenza e del carico di lavoro in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ed59c-103">Concurrency and workload management in SQL Data Warehouse</span></span>
<span data-ttu-id="ed59c-104">toodeliver prestazioni prevedibili su larga scala, Microsoft Azure SQL Data Warehouse consentono di controllare i livelli di concorrenza e allocazioni di risorse come la memoria e assegnazione di priorità di CPU.</span><span class="sxs-lookup"><span data-stu-id="ed59c-104">toodeliver predictable performance at scale, Microsoft Azure SQL Data Warehouse helps you control concurrency levels and resource allocations like memory and CPU prioritization.</span></span> <span data-ttu-id="ed59c-105">Questo articolo illustra i concetti di toohello della gestione della concorrenza e carico di lavoro, che spiega come entrambe le funzionalità sono state implementate e come sia possibile controllare in data warehouse.</span><span class="sxs-lookup"><span data-stu-id="ed59c-105">This article introduces you toohello concepts of concurrency and workload management, explaining how both features have been implemented and how you can control them in your data warehouse.</span></span> <span data-ttu-id="ed59c-106">La gestione del carico di lavoro di SQL Data Warehouse è toohelp previsto è supportare ambienti con più utenti.</span><span class="sxs-lookup"><span data-stu-id="ed59c-106">SQL Data Warehouse workload management is intended toohelp you support multi-user environments.</span></span> <span data-ttu-id="ed59c-107">Non è concepita per i carichi di lavoro multi-tenant.</span><span class="sxs-lookup"><span data-stu-id="ed59c-107">It is not intended for multi-tenant workloads.</span></span>

## <a name="concurrency-limits"></a><span data-ttu-id="ed59c-108">Limiti di concorrenza</span><span class="sxs-lookup"><span data-stu-id="ed59c-108">Concurrency limits</span></span>
<span data-ttu-id="ed59c-109">SQL Data Warehouse consente di too1, 024 connessioni simultanee.</span><span class="sxs-lookup"><span data-stu-id="ed59c-109">SQL Data Warehouse allows up too1,024 concurrent connections.</span></span> <span data-ttu-id="ed59c-110">Tutte le 1.024 connessioni possono inviare query contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="ed59c-110">All 1,024 connections can submit queries concurrently.</span></span> <span data-ttu-id="ed59c-111">Tuttavia, toooptimize una velocità effettiva, SQL Data Warehouse può accodare tooensure alcune query che una concessione di memoria minima assegnata a ogni query.</span><span class="sxs-lookup"><span data-stu-id="ed59c-111">However, toooptimize throughput, SQL Data Warehouse may queue some queries tooensure that each query receives a minimal memory grant.</span></span> <span data-ttu-id="ed59c-112">L'accodamento avviene in fase di esecuzione della query.</span><span class="sxs-lookup"><span data-stu-id="ed59c-112">Queuing occurs at query execution time.</span></span> <span data-ttu-id="ed59c-113">Dalle query di accodamento dei messaggi quando vengono raggiunti i limiti, concorrenza SQL Data Warehouse è possibile aumentare velocità effettiva totale per garantire che query attive toocritically di accesso necessarie risorse di memoria.</span><span class="sxs-lookup"><span data-stu-id="ed59c-113">By queuing queries when concurrency limits are reached, SQL Data Warehouse can increase total throughput by ensuring that active queries get access toocritically needed memory resources.</span></span>  

<span data-ttu-id="ed59c-114">I limiti di concorrenza sono regolati da due concetti, *query simultanee* e *slot di concorrenza*.</span><span class="sxs-lookup"><span data-stu-id="ed59c-114">Concurrency limits are governed by two concepts: *concurrent queries* and *concurrency slots*.</span></span> <span data-ttu-id="ed59c-115">Per tooexecute una query, deve essere eseguito entro il limite di concorrenza delle query hello sia allocazione slot di concorrenza hello.</span><span class="sxs-lookup"><span data-stu-id="ed59c-115">For a query tooexecute, it must execute within both hello query concurrency limit and hello concurrency slot allocation.</span></span>

* <span data-ttu-id="ed59c-116">Le query simultanee sono query hello in esecuzione in hello stesso tempo.</span><span class="sxs-lookup"><span data-stu-id="ed59c-116">Concurrent queries are hello queries executing at hello same time.</span></span> <span data-ttu-id="ed59c-117">SQL Data Warehouse supporta le query simultanee di too32 su dimensioni maggiori del numero di DWU hello.</span><span class="sxs-lookup"><span data-stu-id="ed59c-117">SQL Data Warehouse supports up too32 concurrent queries on hello larger DWU sizes.</span></span>
* <span data-ttu-id="ed59c-118">In base alle Unità Data Warehouse (DWU), vengono allocati slot di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="ed59c-118">Concurrency slots are allocated based on DWU.</span></span> <span data-ttu-id="ed59c-119">Ogni 100 DWU, vengono forniti 4 slot di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="ed59c-119">Each 100 DWU provides 4 concurrency slots.</span></span> <span data-ttu-id="ed59c-120">Ad esempio, per DW100 vengono allocati 4 slot di concorrenza e per DW1000 ne vengono allocati 40.</span><span class="sxs-lookup"><span data-stu-id="ed59c-120">For example, a DW100 allocates 4 concurrency slots and DW1000 allocates 40.</span></span> <span data-ttu-id="ed59c-121">Ogni query utilizza uno o più concorrenza slot, dipende hello [classe di risorse](#resource-classes) di query hello.</span><span class="sxs-lookup"><span data-stu-id="ed59c-121">Each query consumes one or more concurrency slots, dependent on hello [resource class](#resource-classes) of hello query.</span></span> <span data-ttu-id="ed59c-122">Query in esecuzione in una classe di risorse smallrc hello utilizzano uno slot di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="ed59c-122">Queries running in hello smallrc resource class consume one concurrency slot.</span></span> <span data-ttu-id="ed59c-123">Le query in esecuzione in una classe di risorse superiore usano più slot di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="ed59c-123">Queries running in a higher resource class consume more concurrency slots.</span></span>

<span data-ttu-id="ed59c-124">Hello nella tabella seguente descrive i limiti di hello per le query simultanee e slot di concorrenza in hello diverse dimensioni DWU.</span><span class="sxs-lookup"><span data-stu-id="ed59c-124">hello following table describes hello limits for both concurrent queries and concurrency slots at hello various DWU sizes.</span></span>

### <a name="concurrency-limits"></a><span data-ttu-id="ed59c-125">Limiti di concorrenza</span><span class="sxs-lookup"><span data-stu-id="ed59c-125">Concurrency limits</span></span>
| <span data-ttu-id="ed59c-126">DWU</span><span class="sxs-lookup"><span data-stu-id="ed59c-126">DWU</span></span> | <span data-ttu-id="ed59c-127">Numero massimo di query simultanee</span><span class="sxs-lookup"><span data-stu-id="ed59c-127">Max concurrent queries</span></span> | <span data-ttu-id="ed59c-128">Numero di slot di concorrenza allocati</span><span class="sxs-lookup"><span data-stu-id="ed59c-128">Concurrency slots allocated</span></span> |
|:--- |:---:|:---:|
| <span data-ttu-id="ed59c-129">DW100</span><span class="sxs-lookup"><span data-stu-id="ed59c-129">DW100</span></span> |<span data-ttu-id="ed59c-130">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-130">4</span></span> |<span data-ttu-id="ed59c-131">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-131">4</span></span> |
| <span data-ttu-id="ed59c-132">DW200</span><span class="sxs-lookup"><span data-stu-id="ed59c-132">DW200</span></span> |<span data-ttu-id="ed59c-133">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-133">8</span></span> |<span data-ttu-id="ed59c-134">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-134">8</span></span> |
| <span data-ttu-id="ed59c-135">DW300</span><span class="sxs-lookup"><span data-stu-id="ed59c-135">DW300</span></span> |<span data-ttu-id="ed59c-136">12</span><span class="sxs-lookup"><span data-stu-id="ed59c-136">12</span></span> |<span data-ttu-id="ed59c-137">12</span><span class="sxs-lookup"><span data-stu-id="ed59c-137">12</span></span> |
| <span data-ttu-id="ed59c-138">DW400</span><span class="sxs-lookup"><span data-stu-id="ed59c-138">DW400</span></span> |<span data-ttu-id="ed59c-139">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-139">16</span></span> |<span data-ttu-id="ed59c-140">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-140">16</span></span> |
| <span data-ttu-id="ed59c-141">DW500</span><span class="sxs-lookup"><span data-stu-id="ed59c-141">DW500</span></span> |<span data-ttu-id="ed59c-142">20</span><span class="sxs-lookup"><span data-stu-id="ed59c-142">20</span></span> |<span data-ttu-id="ed59c-143">20</span><span class="sxs-lookup"><span data-stu-id="ed59c-143">20</span></span> |
| <span data-ttu-id="ed59c-144">DW600</span><span class="sxs-lookup"><span data-stu-id="ed59c-144">DW600</span></span> |<span data-ttu-id="ed59c-145">24</span><span class="sxs-lookup"><span data-stu-id="ed59c-145">24</span></span> |<span data-ttu-id="ed59c-146">24</span><span class="sxs-lookup"><span data-stu-id="ed59c-146">24</span></span> |
| <span data-ttu-id="ed59c-147">DW1000</span><span class="sxs-lookup"><span data-stu-id="ed59c-147">DW1000</span></span> |<span data-ttu-id="ed59c-148">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-148">32</span></span> |<span data-ttu-id="ed59c-149">40</span><span class="sxs-lookup"><span data-stu-id="ed59c-149">40</span></span> |
| <span data-ttu-id="ed59c-150">DW1200</span><span class="sxs-lookup"><span data-stu-id="ed59c-150">DW1200</span></span> |<span data-ttu-id="ed59c-151">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-151">32</span></span> |<span data-ttu-id="ed59c-152">48</span><span class="sxs-lookup"><span data-stu-id="ed59c-152">48</span></span> |
| <span data-ttu-id="ed59c-153">DW1500</span><span class="sxs-lookup"><span data-stu-id="ed59c-153">DW1500</span></span> |<span data-ttu-id="ed59c-154">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-154">32</span></span> |<span data-ttu-id="ed59c-155">60</span><span class="sxs-lookup"><span data-stu-id="ed59c-155">60</span></span> |
| <span data-ttu-id="ed59c-156">DW2000</span><span class="sxs-lookup"><span data-stu-id="ed59c-156">DW2000</span></span> |<span data-ttu-id="ed59c-157">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-157">32</span></span> |<span data-ttu-id="ed59c-158">80</span><span class="sxs-lookup"><span data-stu-id="ed59c-158">80</span></span> |
| <span data-ttu-id="ed59c-159">DW3000</span><span class="sxs-lookup"><span data-stu-id="ed59c-159">DW3000</span></span> |<span data-ttu-id="ed59c-160">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-160">32</span></span> |<span data-ttu-id="ed59c-161">120</span><span class="sxs-lookup"><span data-stu-id="ed59c-161">120</span></span> |
| <span data-ttu-id="ed59c-162">DW6000</span><span class="sxs-lookup"><span data-stu-id="ed59c-162">DW6000</span></span> |<span data-ttu-id="ed59c-163">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-163">32</span></span> |<span data-ttu-id="ed59c-164">240</span><span class="sxs-lookup"><span data-stu-id="ed59c-164">240</span></span> |

<span data-ttu-id="ed59c-165">Quando viene raggiunta una di queste soglie, le nuove query vengono accodate e vengono eseguite in base al principio FIFO (First-In-First-Out).</span><span class="sxs-lookup"><span data-stu-id="ed59c-165">When one of these thresholds is met, new queries are queued and executed on a first-in, first-out basis.</span></span>  <span data-ttu-id="ed59c-166">Come al termine di una query e hello query e slot scende di sotto dei limiti di hello, vengono rilasciate le query in coda.</span><span class="sxs-lookup"><span data-stu-id="ed59c-166">As a queries finishes and hello number of queries and slots falls below hello limits, queued queries are released.</span></span> 

> [!NOTE]  
> <span data-ttu-id="ed59c-167">*Selezionare* query esecuzione esclusivamente su viste a gestione dinamica (DMV) o viste del catalogo non dipendono da uno qualsiasi dei limiti di concorrenza hello.</span><span class="sxs-lookup"><span data-stu-id="ed59c-167">*Select* queries executing exclusively on dynamic management views (DMVs) or catalog views are not governed by any of hello concurrency limits.</span></span> <span data-ttu-id="ed59c-168">È possibile monitorare il sistema hello indipendentemente dal numero di hello di query in esecuzione su di esso.</span><span class="sxs-lookup"><span data-stu-id="ed59c-168">You can monitor hello system regardless of hello number of queries executing on it.</span></span>
> 
> 

## <a name="resource-classes"></a><span data-ttu-id="ed59c-169">Classi di risorse</span><span class="sxs-lookup"><span data-stu-id="ed59c-169">Resource classes</span></span>
<span data-ttu-id="ed59c-170">Risorsa classi consente di controllare l'allocazione della memoria e cicli di CPU tooa query specificati.</span><span class="sxs-lookup"><span data-stu-id="ed59c-170">Resource classes help you control memory allocation and CPU cycles given tooa query.</span></span> <span data-ttu-id="ed59c-171">È possibile assegnare due tipi di risorsa classi tooa utente nel formato hello dei ruoli predefiniti del database.</span><span class="sxs-lookup"><span data-stu-id="ed59c-171">You can assign two types of resource classes tooa user in hello form of database roles.</span></span> <span data-ttu-id="ed59c-172">Hello due tipi di classi di risorse sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="ed59c-172">hello two types of resource classes are as follows:</span></span>
1. <span data-ttu-id="ed59c-173">Classi di risorse dinamiche (**smallrc, mediumrc, largerc, xlargerc**) allocare una quantità di memoria a seconda di hello variabile DWU corrente.</span><span class="sxs-lookup"><span data-stu-id="ed59c-173">Dynamic Resource Classes (**smallrc, mediumrc, largerc, xlargerc**) allocate a variable amount of memory depending on hello current DWU.</span></span> <span data-ttu-id="ed59c-174">Ciò significa che quando si aumenta il backup tooa DWU più grandi, le query ottengono automaticamente maggiore quantità di memoria.</span><span class="sxs-lookup"><span data-stu-id="ed59c-174">This means that when you scale up tooa larger DWU, your queries automatically get more memory.</span></span> 
2. <span data-ttu-id="ed59c-175">Le classi di risorse statiche (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) allocare hello stessa quantità di memoria indipendentemente dal valore hello DWU corrente (purché hello DWU stesso disponga di sufficiente memoria).</span><span class="sxs-lookup"><span data-stu-id="ed59c-175">Static Resource Classes (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) allocate hello same amount of memory regardless of hello current DWU (provided that hello DWU itself has enough memory).</span></span> <span data-ttu-id="ed59c-176">Ciò significa che nelle DWU più grandi è possibile eseguire più query in ogni classe di risorse contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="ed59c-176">This means that on larger DWUs, you can run more queries in each resource class concurrently.</span></span>

<span data-ttu-id="ed59c-177">Agli utenti delle classi **smallrc** e **staticrc10** viene assegnata una quantità di memoria più piccola e ciò permette di sfruttare una concorrenza maggiore.</span><span class="sxs-lookup"><span data-stu-id="ed59c-177">Users in **smallrc** and **staticrc10** are given a smaller amount of memory and can take advantage of higher concurrency.</span></span> <span data-ttu-id="ed59c-178">Al contrario, gli utenti assegnati troppo**xlargerc** o **staticrc80** figurano grandi quantità di memoria, e pertanto meno le query possono essere eseguiti contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="ed59c-178">In contrast, users assigned too**xlargerc** or **staticrc80** are given large amounts of memory, and therefore fewer of their queries can run concurrently.</span></span>

<span data-ttu-id="ed59c-179">Per impostazione predefinita, ogni utente è un membro di classe di risorse ridotto hello, **smallrc**.</span><span class="sxs-lookup"><span data-stu-id="ed59c-179">By default, each user is a member of hello small resource class, **smallrc**.</span></span> <span data-ttu-id="ed59c-180">Hello procedure `sp_addrolemember` è utilizzata una classe di risorse tooincrease hello e `sp_droprolemember` viene utilizzata una classe di risorse toodecrease hello.</span><span class="sxs-lookup"><span data-stu-id="ed59c-180">hello procedure `sp_addrolemember` is used tooincrease hello resource class, and `sp_droprolemember` is used toodecrease hello resource class.</span></span> <span data-ttu-id="ed59c-181">Ad esempio, questo comando potrebbe aumentare la classe di risorse hello di loaduser troppo**largerc**:</span><span class="sxs-lookup"><span data-stu-id="ed59c-181">For example, this command would increase hello resource class of loaduser too**largerc**:</span></span>

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a><span data-ttu-id="ed59c-182">Query che non rispettano le classi di risorse</span><span class="sxs-lookup"><span data-stu-id="ed59c-182">Queries that do not honor resource classes</span></span>

<span data-ttu-id="ed59c-183">Esistono alcuni tipi di query che non traggono vantaggio da un'allocazione di memoria maggiore.</span><span class="sxs-lookup"><span data-stu-id="ed59c-183">There are a few types of queries that do not benefit from a larger memory allocation.</span></span> <span data-ttu-id="ed59c-184">sistema Hello ignora l'allocazione di classe di risorse e sempre esecuzione queste query nella classe di risorse ridotto hello invece.</span><span class="sxs-lookup"><span data-stu-id="ed59c-184">hello system ignores their resource class allocation and always run these queries in hello small resource class instead.</span></span> <span data-ttu-id="ed59c-185">Se tali query vengono eseguite sempre nella classe di risorse ridotto hello, essi possono verificarsi quando gli slot di concorrenza sono sotto pressione e non utilizzano più slot quelle necessarie.</span><span class="sxs-lookup"><span data-stu-id="ed59c-185">If these queries always run in hello small resource class, they can run when concurrency slots are under pressure and they won't consume more slots than needed.</span></span> <span data-ttu-id="ed59c-186">Vedere [Eccezioni della classe di risorse](#query-exceptions-to-concurrency-limits) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="ed59c-186">See [Resource class exceptions](#query-exceptions-to-concurrency-limits) for more information.</span></span>

## <a name="details-on-resource-class-assignment"></a><span data-ttu-id="ed59c-187">Dettagli sull'assegnazione della classe di risorse</span><span class="sxs-lookup"><span data-stu-id="ed59c-187">Details on resource class assignment</span></span>


<span data-ttu-id="ed59c-188">Altri dettagli sulla classe di risorse:</span><span class="sxs-lookup"><span data-stu-id="ed59c-188">A few more details on resource class:</span></span>

* <span data-ttu-id="ed59c-189">*Modificare ruolo* è necessaria l'autorizzazione classe di risorse toochange hello di un utente.</span><span class="sxs-lookup"><span data-stu-id="ed59c-189">*Alter role* permission is required toochange hello resource class of a user.</span></span>
* <span data-ttu-id="ed59c-190">Sebbene sia possibile aggiungere un utente tooone o più classi di risorse superiore hello, classi di risorse dinamiche hanno la precedenza sulle classi di risorse statiche.</span><span class="sxs-lookup"><span data-stu-id="ed59c-190">Although you can add a user tooone or more of hello higher resource classes, dynamic resource classes take precedence over static resource classes.</span></span> <span data-ttu-id="ed59c-191">Ovvero, se un utente è assegnato tooboth **mediumrc**(dinamico) e **staticrc80**(statico), **mediumrc** è una classe di risorse hello che viene rispettato.</span><span class="sxs-lookup"><span data-stu-id="ed59c-191">That is, if a user is assigned tooboth **mediumrc**(dynamic) and **staticrc80**(static), **mediumrc** is hello resource class that is honored.</span></span>
 * <span data-ttu-id="ed59c-192">Quando un utente viene assegnato toomore classe di una risorsa in un tipo di classe di risorse (più di una classe di risorse dinamiche o più di una classe di risorse statiche), classe di risorse massimo hello viene rispettata.</span><span class="sxs-lookup"><span data-stu-id="ed59c-192">When a user is assigned toomore than one resource class in a specific resource class type (more than one dynamic resource class or more than one static resource class), hello highest resource class is honored.</span></span> <span data-ttu-id="ed59c-193">Ovvero, se un utente è assegnato largerc e tooboth mediumrc, classe di risorse superiore hello (largerc) viene rispettata.</span><span class="sxs-lookup"><span data-stu-id="ed59c-193">That is, if a user is assigned tooboth mediumrc and largerc, hello higher resource class (largerc) is honored.</span></span> <span data-ttu-id="ed59c-194">E se un utente è assegnato tooboth **staticrc20** e **statirc80**, **staticrc80** viene tenuto in considerazione.</span><span class="sxs-lookup"><span data-stu-id="ed59c-194">And if a user is assigned tooboth **staticrc20** and **statirc80**, **staticrc80** is honored.</span></span>
* <span data-ttu-id="ed59c-195">Impossibile modificare la classe di risorse Hello di utente amministratore di sistema hello.</span><span class="sxs-lookup"><span data-stu-id="ed59c-195">hello resource class of hello system administrative user cannot be changed.</span></span>

<span data-ttu-id="ed59c-196">Per un esempio dettagliato, vedere [Esempio di modifica della classe di risorse di un utente](#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="ed59c-196">For a detailed example, see [Changing user resource class example](#changing-user-resource-class-example).</span></span>

## <a name="memory-allocation"></a><span data-ttu-id="ed59c-197">Allocazione della memoria</span><span class="sxs-lookup"><span data-stu-id="ed59c-197">Memory allocation</span></span>
<span data-ttu-id="ed59c-198">Esistono vantaggi e svantaggi tooincreasing classe di risorse dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ed59c-198">There are pros and cons tooincreasing a user's resource class.</span></span> <span data-ttu-id="ed59c-199">Sebbene l'aumento di una classe di risorse per un utente, le query offre memoria toomore di accesso, che può indicare le query eseguite più velocemente.</span><span class="sxs-lookup"><span data-stu-id="ed59c-199">Increasing a resource class for a user, gives their queries access toomore memory, which may mean queries execute faster.</span></span>  <span data-ttu-id="ed59c-200">Tuttavia, le classi di risorse superiore riducono il numero di hello di query simultanee che è possibile eseguire.</span><span class="sxs-lookup"><span data-stu-id="ed59c-200">However, higher resource classes also reduce hello number of concurrent queries that can run.</span></span> <span data-ttu-id="ed59c-201">Si tratta di compromesso hello tra allocare grandi quantità di singola query di memoria tooa o consentire altre query, nonché le allocazioni di memoria, toorun contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="ed59c-201">This is hello trade-off between allocating large amounts of memory tooa single query or allowing other queries, which also need memory allocations, toorun concurrently.</span></span> <span data-ttu-id="ed59c-202">Se un utente di elevata allocazioni di memoria per una query, gli altri utenti non potranno toothat accesso stesso memoria toorun una query.</span><span class="sxs-lookup"><span data-stu-id="ed59c-202">If one user is given high allocations of memory for a query, other users will not have access toothat same memory toorun a query.</span></span>

<span data-ttu-id="ed59c-203">Hello nella tabella seguente viene eseguito il mapping hello memoria distribuzione tooeach dalla classe DWU e risorse.</span><span class="sxs-lookup"><span data-stu-id="ed59c-203">hello following table maps hello memory allocated tooeach distribution by DWU and resource class.</span></span>

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a><span data-ttu-id="ed59c-204">Allocazioni di memoria per ogni distribuzione per le classi di risorse dinamiche (MB)</span><span class="sxs-lookup"><span data-stu-id="ed59c-204">Memory allocations per distribution for dynamic resource classes (MB)</span></span>
| <span data-ttu-id="ed59c-205">DWU</span><span class="sxs-lookup"><span data-stu-id="ed59c-205">DWU</span></span> | <span data-ttu-id="ed59c-206">smallrc</span><span class="sxs-lookup"><span data-stu-id="ed59c-206">smallrc</span></span> | <span data-ttu-id="ed59c-207">mediumrc</span><span class="sxs-lookup"><span data-stu-id="ed59c-207">mediumrc</span></span> | <span data-ttu-id="ed59c-208">largerc</span><span class="sxs-lookup"><span data-stu-id="ed59c-208">largerc</span></span> | <span data-ttu-id="ed59c-209">xlargerc</span><span class="sxs-lookup"><span data-stu-id="ed59c-209">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="ed59c-210">DW100</span><span class="sxs-lookup"><span data-stu-id="ed59c-210">DW100</span></span> |<span data-ttu-id="ed59c-211">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-211">100</span></span> |<span data-ttu-id="ed59c-212">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-212">100</span></span> |<span data-ttu-id="ed59c-213">200</span><span class="sxs-lookup"><span data-stu-id="ed59c-213">200</span></span> |<span data-ttu-id="ed59c-214">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-214">400</span></span> |
| <span data-ttu-id="ed59c-215">DW200</span><span class="sxs-lookup"><span data-stu-id="ed59c-215">DW200</span></span> |<span data-ttu-id="ed59c-216">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-216">100</span></span> |<span data-ttu-id="ed59c-217">200</span><span class="sxs-lookup"><span data-stu-id="ed59c-217">200</span></span> |<span data-ttu-id="ed59c-218">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-218">400</span></span> |<span data-ttu-id="ed59c-219">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-219">800</span></span> |
| <span data-ttu-id="ed59c-220">DW300</span><span class="sxs-lookup"><span data-stu-id="ed59c-220">DW300</span></span> |<span data-ttu-id="ed59c-221">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-221">100</span></span> |<span data-ttu-id="ed59c-222">200</span><span class="sxs-lookup"><span data-stu-id="ed59c-222">200</span></span> |<span data-ttu-id="ed59c-223">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-223">400</span></span> |<span data-ttu-id="ed59c-224">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-224">800</span></span> |
| <span data-ttu-id="ed59c-225">DW400</span><span class="sxs-lookup"><span data-stu-id="ed59c-225">DW400</span></span> |<span data-ttu-id="ed59c-226">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-226">100</span></span> |<span data-ttu-id="ed59c-227">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-227">400</span></span> |<span data-ttu-id="ed59c-228">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-228">800</span></span> |<span data-ttu-id="ed59c-229">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-229">1,600</span></span> |
| <span data-ttu-id="ed59c-230">DW500</span><span class="sxs-lookup"><span data-stu-id="ed59c-230">DW500</span></span> |<span data-ttu-id="ed59c-231">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-231">100</span></span> |<span data-ttu-id="ed59c-232">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-232">400</span></span> |<span data-ttu-id="ed59c-233">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-233">800</span></span> |<span data-ttu-id="ed59c-234">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-234">1,600</span></span> |
| <span data-ttu-id="ed59c-235">DW600</span><span class="sxs-lookup"><span data-stu-id="ed59c-235">DW600</span></span> |<span data-ttu-id="ed59c-236">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-236">100</span></span> |<span data-ttu-id="ed59c-237">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-237">400</span></span> |<span data-ttu-id="ed59c-238">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-238">800</span></span> |<span data-ttu-id="ed59c-239">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-239">1,600</span></span> |
| <span data-ttu-id="ed59c-240">DW1000</span><span class="sxs-lookup"><span data-stu-id="ed59c-240">DW1000</span></span> |<span data-ttu-id="ed59c-241">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-241">100</span></span> |<span data-ttu-id="ed59c-242">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-242">800</span></span> |<span data-ttu-id="ed59c-243">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-243">1,600</span></span> |<span data-ttu-id="ed59c-244">3.200</span><span class="sxs-lookup"><span data-stu-id="ed59c-244">3,200</span></span> |
| <span data-ttu-id="ed59c-245">DW1200</span><span class="sxs-lookup"><span data-stu-id="ed59c-245">DW1200</span></span> |<span data-ttu-id="ed59c-246">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-246">100</span></span> |<span data-ttu-id="ed59c-247">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-247">800</span></span> |<span data-ttu-id="ed59c-248">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-248">1,600</span></span> |<span data-ttu-id="ed59c-249">3.200</span><span class="sxs-lookup"><span data-stu-id="ed59c-249">3,200</span></span> |
| <span data-ttu-id="ed59c-250">DW1500</span><span class="sxs-lookup"><span data-stu-id="ed59c-250">DW1500</span></span> |<span data-ttu-id="ed59c-251">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-251">100</span></span> |<span data-ttu-id="ed59c-252">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-252">800</span></span> |<span data-ttu-id="ed59c-253">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-253">1,600</span></span> |<span data-ttu-id="ed59c-254">3.200</span><span class="sxs-lookup"><span data-stu-id="ed59c-254">3,200</span></span> |
| <span data-ttu-id="ed59c-255">DW2000</span><span class="sxs-lookup"><span data-stu-id="ed59c-255">DW2000</span></span> |<span data-ttu-id="ed59c-256">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-256">100</span></span> |<span data-ttu-id="ed59c-257">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-257">1,600</span></span> |<span data-ttu-id="ed59c-258">3.200</span><span class="sxs-lookup"><span data-stu-id="ed59c-258">3,200</span></span> |<span data-ttu-id="ed59c-259">6.400</span><span class="sxs-lookup"><span data-stu-id="ed59c-259">6,400</span></span> |
| <span data-ttu-id="ed59c-260">DW3000</span><span class="sxs-lookup"><span data-stu-id="ed59c-260">DW3000</span></span> |<span data-ttu-id="ed59c-261">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-261">100</span></span> |<span data-ttu-id="ed59c-262">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-262">1,600</span></span> |<span data-ttu-id="ed59c-263">3.200</span><span class="sxs-lookup"><span data-stu-id="ed59c-263">3,200</span></span> |<span data-ttu-id="ed59c-264">6.400</span><span class="sxs-lookup"><span data-stu-id="ed59c-264">6,400</span></span> |
| <span data-ttu-id="ed59c-265">DW6000</span><span class="sxs-lookup"><span data-stu-id="ed59c-265">DW6000</span></span> |<span data-ttu-id="ed59c-266">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-266">100</span></span> |<span data-ttu-id="ed59c-267">3.200</span><span class="sxs-lookup"><span data-stu-id="ed59c-267">3,200</span></span> |<span data-ttu-id="ed59c-268">6.400</span><span class="sxs-lookup"><span data-stu-id="ed59c-268">6,400</span></span> |<span data-ttu-id="ed59c-269">12.800</span><span class="sxs-lookup"><span data-stu-id="ed59c-269">12,800</span></span> |

<span data-ttu-id="ed59c-270">Hello nella tabella seguente viene eseguito il mapping hello memoria distribuzione tooeach DWU e classe di risorse statiche.</span><span class="sxs-lookup"><span data-stu-id="ed59c-270">hello following table maps hello memory allocated tooeach distribution by DWU and static resource class.</span></span> <span data-ttu-id="ed59c-271">Si noti che le classi di risorse superiore hello abbiano la memoria ridotti i limiti DWU toohonor hello globali.</span><span class="sxs-lookup"><span data-stu-id="ed59c-271">Note that hello higher resource classes have their memory reduced toohonor hello global DWU limits.</span></span>

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a><span data-ttu-id="ed59c-272">Allocazioni di memoria per ogni distribuzione per le classi di risorse statiche (MB)</span><span class="sxs-lookup"><span data-stu-id="ed59c-272">Memory allocations per distribution for static resource classes (MB)</span></span>
| <span data-ttu-id="ed59c-273">DWU</span><span class="sxs-lookup"><span data-stu-id="ed59c-273">DWU</span></span> | <span data-ttu-id="ed59c-274">staticrc10</span><span class="sxs-lookup"><span data-stu-id="ed59c-274">staticrc10</span></span> | <span data-ttu-id="ed59c-275">staticrc20</span><span class="sxs-lookup"><span data-stu-id="ed59c-275">staticrc20</span></span> | <span data-ttu-id="ed59c-276">staticrc30</span><span class="sxs-lookup"><span data-stu-id="ed59c-276">staticrc30</span></span> | <span data-ttu-id="ed59c-277">staticrc40</span><span class="sxs-lookup"><span data-stu-id="ed59c-277">staticrc40</span></span> | <span data-ttu-id="ed59c-278">staticrc50</span><span class="sxs-lookup"><span data-stu-id="ed59c-278">staticrc50</span></span> | <span data-ttu-id="ed59c-279">staticrc60</span><span class="sxs-lookup"><span data-stu-id="ed59c-279">staticrc60</span></span> | <span data-ttu-id="ed59c-280">staticrc70</span><span class="sxs-lookup"><span data-stu-id="ed59c-280">staticrc70</span></span> | <span data-ttu-id="ed59c-281">staticrc80</span><span class="sxs-lookup"><span data-stu-id="ed59c-281">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="ed59c-282">DW100</span><span class="sxs-lookup"><span data-stu-id="ed59c-282">DW100</span></span> |<span data-ttu-id="ed59c-283">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-283">100</span></span> |<span data-ttu-id="ed59c-284">200</span><span class="sxs-lookup"><span data-stu-id="ed59c-284">200</span></span> |<span data-ttu-id="ed59c-285">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-285">400</span></span> |<span data-ttu-id="ed59c-286">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-286">400</span></span> |<span data-ttu-id="ed59c-287">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-287">400</span></span> |<span data-ttu-id="ed59c-288">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-288">400</span></span> |<span data-ttu-id="ed59c-289">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-289">400</span></span> |<span data-ttu-id="ed59c-290">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-290">400</span></span> |
| <span data-ttu-id="ed59c-291">DW200</span><span class="sxs-lookup"><span data-stu-id="ed59c-291">DW200</span></span> |<span data-ttu-id="ed59c-292">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-292">100</span></span> |<span data-ttu-id="ed59c-293">200</span><span class="sxs-lookup"><span data-stu-id="ed59c-293">200</span></span> |<span data-ttu-id="ed59c-294">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-294">400</span></span> |<span data-ttu-id="ed59c-295">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-295">800</span></span> |<span data-ttu-id="ed59c-296">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-296">800</span></span> |<span data-ttu-id="ed59c-297">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-297">800</span></span> |<span data-ttu-id="ed59c-298">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-298">800</span></span> |<span data-ttu-id="ed59c-299">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-299">800</span></span> |
| <span data-ttu-id="ed59c-300">DW300</span><span class="sxs-lookup"><span data-stu-id="ed59c-300">DW300</span></span> |<span data-ttu-id="ed59c-301">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-301">100</span></span> |<span data-ttu-id="ed59c-302">200</span><span class="sxs-lookup"><span data-stu-id="ed59c-302">200</span></span> |<span data-ttu-id="ed59c-303">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-303">400</span></span> |<span data-ttu-id="ed59c-304">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-304">800</span></span> |<span data-ttu-id="ed59c-305">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-305">800</span></span> |<span data-ttu-id="ed59c-306">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-306">800</span></span> |<span data-ttu-id="ed59c-307">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-307">800</span></span> |<span data-ttu-id="ed59c-308">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-308">800</span></span> |
| <span data-ttu-id="ed59c-309">DW400</span><span class="sxs-lookup"><span data-stu-id="ed59c-309">DW400</span></span> |<span data-ttu-id="ed59c-310">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-310">100</span></span> |<span data-ttu-id="ed59c-311">200</span><span class="sxs-lookup"><span data-stu-id="ed59c-311">200</span></span> |<span data-ttu-id="ed59c-312">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-312">400</span></span> |<span data-ttu-id="ed59c-313">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-313">800</span></span> |<span data-ttu-id="ed59c-314">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-314">1,600</span></span> |<span data-ttu-id="ed59c-315">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-315">1,600</span></span> |<span data-ttu-id="ed59c-316">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-316">1,600</span></span> |<span data-ttu-id="ed59c-317">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-317">1,600</span></span> |
| <span data-ttu-id="ed59c-318">DW500</span><span class="sxs-lookup"><span data-stu-id="ed59c-318">DW500</span></span> |<span data-ttu-id="ed59c-319">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-319">100</span></span> |<span data-ttu-id="ed59c-320">200</span><span class="sxs-lookup"><span data-stu-id="ed59c-320">200</span></span> |<span data-ttu-id="ed59c-321">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-321">400</span></span> |<span data-ttu-id="ed59c-322">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-322">800</span></span> |<span data-ttu-id="ed59c-323">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-323">1,600</span></span> |<span data-ttu-id="ed59c-324">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-324">1,600</span></span> |<span data-ttu-id="ed59c-325">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-325">1,600</span></span> |<span data-ttu-id="ed59c-326">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-326">1,600</span></span> |
| <span data-ttu-id="ed59c-327">DW600</span><span class="sxs-lookup"><span data-stu-id="ed59c-327">DW600</span></span> |<span data-ttu-id="ed59c-328">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-328">100</span></span> |<span data-ttu-id="ed59c-329">200</span><span class="sxs-lookup"><span data-stu-id="ed59c-329">200</span></span> |<span data-ttu-id="ed59c-330">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-330">400</span></span> |<span data-ttu-id="ed59c-331">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-331">800</span></span> |<span data-ttu-id="ed59c-332">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-332">1,600</span></span> |<span data-ttu-id="ed59c-333">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-333">1,600</span></span> |<span data-ttu-id="ed59c-334">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-334">1,600</span></span> |<span data-ttu-id="ed59c-335">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-335">1,600</span></span> |
| <span data-ttu-id="ed59c-336">DW1000</span><span class="sxs-lookup"><span data-stu-id="ed59c-336">DW1000</span></span> |<span data-ttu-id="ed59c-337">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-337">100</span></span> |<span data-ttu-id="ed59c-338">200</span><span class="sxs-lookup"><span data-stu-id="ed59c-338">200</span></span> |<span data-ttu-id="ed59c-339">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-339">400</span></span> |<span data-ttu-id="ed59c-340">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-340">800</span></span> |<span data-ttu-id="ed59c-341">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-341">1,600</span></span> |<span data-ttu-id="ed59c-342">3.200</span><span class="sxs-lookup"><span data-stu-id="ed59c-342">3,200</span></span> |<span data-ttu-id="ed59c-343">3.200</span><span class="sxs-lookup"><span data-stu-id="ed59c-343">3,200</span></span> |<span data-ttu-id="ed59c-344">3.200</span><span class="sxs-lookup"><span data-stu-id="ed59c-344">3,200</span></span> |
| <span data-ttu-id="ed59c-345">DW1200</span><span class="sxs-lookup"><span data-stu-id="ed59c-345">DW1200</span></span> |<span data-ttu-id="ed59c-346">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-346">100</span></span> |<span data-ttu-id="ed59c-347">200</span><span class="sxs-lookup"><span data-stu-id="ed59c-347">200</span></span> |<span data-ttu-id="ed59c-348">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-348">400</span></span> |<span data-ttu-id="ed59c-349">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-349">800</span></span> |<span data-ttu-id="ed59c-350">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-350">1,600</span></span> |<span data-ttu-id="ed59c-351">3.200</span><span class="sxs-lookup"><span data-stu-id="ed59c-351">3,200</span></span> |<span data-ttu-id="ed59c-352">3.200</span><span class="sxs-lookup"><span data-stu-id="ed59c-352">3,200</span></span> |<span data-ttu-id="ed59c-353">3.200</span><span class="sxs-lookup"><span data-stu-id="ed59c-353">3,200</span></span> |
| <span data-ttu-id="ed59c-354">DW1500</span><span class="sxs-lookup"><span data-stu-id="ed59c-354">DW1500</span></span> |<span data-ttu-id="ed59c-355">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-355">100</span></span> |<span data-ttu-id="ed59c-356">200</span><span class="sxs-lookup"><span data-stu-id="ed59c-356">200</span></span> |<span data-ttu-id="ed59c-357">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-357">400</span></span> |<span data-ttu-id="ed59c-358">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-358">800</span></span> |<span data-ttu-id="ed59c-359">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-359">1,600</span></span> |<span data-ttu-id="ed59c-360">3.200</span><span class="sxs-lookup"><span data-stu-id="ed59c-360">3,200</span></span> |<span data-ttu-id="ed59c-361">3.200</span><span class="sxs-lookup"><span data-stu-id="ed59c-361">3,200</span></span> |<span data-ttu-id="ed59c-362">3.200</span><span class="sxs-lookup"><span data-stu-id="ed59c-362">3,200</span></span> |
| <span data-ttu-id="ed59c-363">DW2000</span><span class="sxs-lookup"><span data-stu-id="ed59c-363">DW2000</span></span> |<span data-ttu-id="ed59c-364">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-364">100</span></span> |<span data-ttu-id="ed59c-365">200</span><span class="sxs-lookup"><span data-stu-id="ed59c-365">200</span></span> |<span data-ttu-id="ed59c-366">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-366">400</span></span> |<span data-ttu-id="ed59c-367">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-367">800</span></span> |<span data-ttu-id="ed59c-368">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-368">1,600</span></span> |<span data-ttu-id="ed59c-369">3.200</span><span class="sxs-lookup"><span data-stu-id="ed59c-369">3,200</span></span> |<span data-ttu-id="ed59c-370">6.400</span><span class="sxs-lookup"><span data-stu-id="ed59c-370">6,400</span></span> |<span data-ttu-id="ed59c-371">6.400</span><span class="sxs-lookup"><span data-stu-id="ed59c-371">6,400</span></span> |
| <span data-ttu-id="ed59c-372">DW3000</span><span class="sxs-lookup"><span data-stu-id="ed59c-372">DW3000</span></span> |<span data-ttu-id="ed59c-373">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-373">100</span></span> |<span data-ttu-id="ed59c-374">200</span><span class="sxs-lookup"><span data-stu-id="ed59c-374">200</span></span> |<span data-ttu-id="ed59c-375">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-375">400</span></span> |<span data-ttu-id="ed59c-376">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-376">800</span></span> |<span data-ttu-id="ed59c-377">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-377">1,600</span></span> |<span data-ttu-id="ed59c-378">3.200</span><span class="sxs-lookup"><span data-stu-id="ed59c-378">3,200</span></span> |<span data-ttu-id="ed59c-379">6.400</span><span class="sxs-lookup"><span data-stu-id="ed59c-379">6,400</span></span> |<span data-ttu-id="ed59c-380">6.400</span><span class="sxs-lookup"><span data-stu-id="ed59c-380">6,400</span></span> |
| <span data-ttu-id="ed59c-381">DW6000</span><span class="sxs-lookup"><span data-stu-id="ed59c-381">DW6000</span></span> |<span data-ttu-id="ed59c-382">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-382">100</span></span> |<span data-ttu-id="ed59c-383">200</span><span class="sxs-lookup"><span data-stu-id="ed59c-383">200</span></span> |<span data-ttu-id="ed59c-384">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-384">400</span></span> |<span data-ttu-id="ed59c-385">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-385">800</span></span> |<span data-ttu-id="ed59c-386">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-386">1,600</span></span> |<span data-ttu-id="ed59c-387">3.200</span><span class="sxs-lookup"><span data-stu-id="ed59c-387">3,200</span></span> |<span data-ttu-id="ed59c-388">6.400</span><span class="sxs-lookup"><span data-stu-id="ed59c-388">6,400</span></span> |<span data-ttu-id="ed59c-389">12.800</span><span class="sxs-lookup"><span data-stu-id="ed59c-389">12,800</span></span> |

<span data-ttu-id="ed59c-390">Da hello nella tabella precedente, è possibile vedere che una query in esecuzione in un DW2000 in hello **xlargerc** classe di risorse avrebbe accesso too6, 400 MB di memoria all'interno di ogni database distribuiti 60 hello.</span><span class="sxs-lookup"><span data-stu-id="ed59c-390">From hello preceding table, you can see that a query running on a DW2000 in hello **xlargerc** resource class would have access too6,400 MB of memory within each of hello 60 distributed databases.</span></span>  <span data-ttu-id="ed59c-391">In SQL Data Warehouse sono presenti 60 distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="ed59c-391">In SQL Data Warehouse, there are 60 distributions.</span></span> <span data-ttu-id="ed59c-392">Allocazione di memoria totale hello toocalculate per una query in una classe di risorse specifico, hello sopra i valori, pertanto, deve essere moltiplicata per 60.</span><span class="sxs-lookup"><span data-stu-id="ed59c-392">Therefore, toocalculate hello total memory allocation for a query in a given resource class, hello above values should be multiplied by 60.</span></span>

### <a name="memory-allocations-system-wide-gb"></a><span data-ttu-id="ed59c-393">Allocazioni di memoria a livello di sistema (GB)</span><span class="sxs-lookup"><span data-stu-id="ed59c-393">Memory allocations system-wide (GB)</span></span>
| <span data-ttu-id="ed59c-394">DWU</span><span class="sxs-lookup"><span data-stu-id="ed59c-394">DWU</span></span> | <span data-ttu-id="ed59c-395">smallrc</span><span class="sxs-lookup"><span data-stu-id="ed59c-395">smallrc</span></span> | <span data-ttu-id="ed59c-396">mediumrc</span><span class="sxs-lookup"><span data-stu-id="ed59c-396">mediumrc</span></span> | <span data-ttu-id="ed59c-397">largerc</span><span class="sxs-lookup"><span data-stu-id="ed59c-397">largerc</span></span> | <span data-ttu-id="ed59c-398">xlargerc</span><span class="sxs-lookup"><span data-stu-id="ed59c-398">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="ed59c-399">DW100</span><span class="sxs-lookup"><span data-stu-id="ed59c-399">DW100</span></span> |<span data-ttu-id="ed59c-400">6</span><span class="sxs-lookup"><span data-stu-id="ed59c-400">6</span></span> |<span data-ttu-id="ed59c-401">6</span><span class="sxs-lookup"><span data-stu-id="ed59c-401">6</span></span> |<span data-ttu-id="ed59c-402">12</span><span class="sxs-lookup"><span data-stu-id="ed59c-402">12</span></span> |<span data-ttu-id="ed59c-403">23</span><span class="sxs-lookup"><span data-stu-id="ed59c-403">23</span></span> |
| <span data-ttu-id="ed59c-404">DW200</span><span class="sxs-lookup"><span data-stu-id="ed59c-404">DW200</span></span> |<span data-ttu-id="ed59c-405">6</span><span class="sxs-lookup"><span data-stu-id="ed59c-405">6</span></span> |<span data-ttu-id="ed59c-406">12</span><span class="sxs-lookup"><span data-stu-id="ed59c-406">12</span></span> |<span data-ttu-id="ed59c-407">23</span><span class="sxs-lookup"><span data-stu-id="ed59c-407">23</span></span> |<span data-ttu-id="ed59c-408">47</span><span class="sxs-lookup"><span data-stu-id="ed59c-408">47</span></span> |
| <span data-ttu-id="ed59c-409">DW300</span><span class="sxs-lookup"><span data-stu-id="ed59c-409">DW300</span></span> |<span data-ttu-id="ed59c-410">6</span><span class="sxs-lookup"><span data-stu-id="ed59c-410">6</span></span> |<span data-ttu-id="ed59c-411">12</span><span class="sxs-lookup"><span data-stu-id="ed59c-411">12</span></span> |<span data-ttu-id="ed59c-412">23</span><span class="sxs-lookup"><span data-stu-id="ed59c-412">23</span></span> |<span data-ttu-id="ed59c-413">47</span><span class="sxs-lookup"><span data-stu-id="ed59c-413">47</span></span> |
| <span data-ttu-id="ed59c-414">DW400</span><span class="sxs-lookup"><span data-stu-id="ed59c-414">DW400</span></span> |<span data-ttu-id="ed59c-415">6</span><span class="sxs-lookup"><span data-stu-id="ed59c-415">6</span></span> |<span data-ttu-id="ed59c-416">23</span><span class="sxs-lookup"><span data-stu-id="ed59c-416">23</span></span> |<span data-ttu-id="ed59c-417">47</span><span class="sxs-lookup"><span data-stu-id="ed59c-417">47</span></span> |<span data-ttu-id="ed59c-418">94</span><span class="sxs-lookup"><span data-stu-id="ed59c-418">94</span></span> |
| <span data-ttu-id="ed59c-419">DW500</span><span class="sxs-lookup"><span data-stu-id="ed59c-419">DW500</span></span> |<span data-ttu-id="ed59c-420">6</span><span class="sxs-lookup"><span data-stu-id="ed59c-420">6</span></span> |<span data-ttu-id="ed59c-421">23</span><span class="sxs-lookup"><span data-stu-id="ed59c-421">23</span></span> |<span data-ttu-id="ed59c-422">47</span><span class="sxs-lookup"><span data-stu-id="ed59c-422">47</span></span> |<span data-ttu-id="ed59c-423">94</span><span class="sxs-lookup"><span data-stu-id="ed59c-423">94</span></span> |
| <span data-ttu-id="ed59c-424">DW600</span><span class="sxs-lookup"><span data-stu-id="ed59c-424">DW600</span></span> |<span data-ttu-id="ed59c-425">6</span><span class="sxs-lookup"><span data-stu-id="ed59c-425">6</span></span> |<span data-ttu-id="ed59c-426">23</span><span class="sxs-lookup"><span data-stu-id="ed59c-426">23</span></span> |<span data-ttu-id="ed59c-427">47</span><span class="sxs-lookup"><span data-stu-id="ed59c-427">47</span></span> |<span data-ttu-id="ed59c-428">94</span><span class="sxs-lookup"><span data-stu-id="ed59c-428">94</span></span> |
| <span data-ttu-id="ed59c-429">DW1000</span><span class="sxs-lookup"><span data-stu-id="ed59c-429">DW1000</span></span> |<span data-ttu-id="ed59c-430">6</span><span class="sxs-lookup"><span data-stu-id="ed59c-430">6</span></span> |<span data-ttu-id="ed59c-431">47</span><span class="sxs-lookup"><span data-stu-id="ed59c-431">47</span></span> |<span data-ttu-id="ed59c-432">94</span><span class="sxs-lookup"><span data-stu-id="ed59c-432">94</span></span> |<span data-ttu-id="ed59c-433">188</span><span class="sxs-lookup"><span data-stu-id="ed59c-433">188</span></span> |
| <span data-ttu-id="ed59c-434">DW1200</span><span class="sxs-lookup"><span data-stu-id="ed59c-434">DW1200</span></span> |<span data-ttu-id="ed59c-435">6</span><span class="sxs-lookup"><span data-stu-id="ed59c-435">6</span></span> |<span data-ttu-id="ed59c-436">47</span><span class="sxs-lookup"><span data-stu-id="ed59c-436">47</span></span> |<span data-ttu-id="ed59c-437">94</span><span class="sxs-lookup"><span data-stu-id="ed59c-437">94</span></span> |<span data-ttu-id="ed59c-438">188</span><span class="sxs-lookup"><span data-stu-id="ed59c-438">188</span></span> |
| <span data-ttu-id="ed59c-439">DW1500</span><span class="sxs-lookup"><span data-stu-id="ed59c-439">DW1500</span></span> |<span data-ttu-id="ed59c-440">6</span><span class="sxs-lookup"><span data-stu-id="ed59c-440">6</span></span> |<span data-ttu-id="ed59c-441">47</span><span class="sxs-lookup"><span data-stu-id="ed59c-441">47</span></span> |<span data-ttu-id="ed59c-442">94</span><span class="sxs-lookup"><span data-stu-id="ed59c-442">94</span></span> |<span data-ttu-id="ed59c-443">188</span><span class="sxs-lookup"><span data-stu-id="ed59c-443">188</span></span> |
| <span data-ttu-id="ed59c-444">DW2000</span><span class="sxs-lookup"><span data-stu-id="ed59c-444">DW2000</span></span> |<span data-ttu-id="ed59c-445">6</span><span class="sxs-lookup"><span data-stu-id="ed59c-445">6</span></span> |<span data-ttu-id="ed59c-446">94</span><span class="sxs-lookup"><span data-stu-id="ed59c-446">94</span></span> |<span data-ttu-id="ed59c-447">188</span><span class="sxs-lookup"><span data-stu-id="ed59c-447">188</span></span> |<span data-ttu-id="ed59c-448">375</span><span class="sxs-lookup"><span data-stu-id="ed59c-448">375</span></span> |
| <span data-ttu-id="ed59c-449">DW3000</span><span class="sxs-lookup"><span data-stu-id="ed59c-449">DW3000</span></span> |<span data-ttu-id="ed59c-450">6</span><span class="sxs-lookup"><span data-stu-id="ed59c-450">6</span></span> |<span data-ttu-id="ed59c-451">94</span><span class="sxs-lookup"><span data-stu-id="ed59c-451">94</span></span> |<span data-ttu-id="ed59c-452">188</span><span class="sxs-lookup"><span data-stu-id="ed59c-452">188</span></span> |<span data-ttu-id="ed59c-453">375</span><span class="sxs-lookup"><span data-stu-id="ed59c-453">375</span></span> |
| <span data-ttu-id="ed59c-454">DW6000</span><span class="sxs-lookup"><span data-stu-id="ed59c-454">DW6000</span></span> |<span data-ttu-id="ed59c-455">6</span><span class="sxs-lookup"><span data-stu-id="ed59c-455">6</span></span> |<span data-ttu-id="ed59c-456">188</span><span class="sxs-lookup"><span data-stu-id="ed59c-456">188</span></span> |<span data-ttu-id="ed59c-457">375</span><span class="sxs-lookup"><span data-stu-id="ed59c-457">375</span></span> |<span data-ttu-id="ed59c-458">750</span><span class="sxs-lookup"><span data-stu-id="ed59c-458">750</span></span> |

<span data-ttu-id="ed59c-459">Da questa tabella delle allocazioni di memoria a livello di sistema, è possibile notare che una query in esecuzione in un DW2000 nella classe della risorsa xlargerc hello viene allocata un totale di 375 GB di memoria (MB * 60 6.400 distribuzioni / 1.024 tooconvert tooGB) su interamente hello del proprio SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ed59c-459">From this table of system-wide memory allocations, you can see that a query running on a DW2000 in hello xlargerc resource class is allocated a total of 375 GB of memory (6,400 MB * 60 distributions / 1,024 tooconvert tooGB) over hello entirety of your SQL Data Warehouse.</span></span>

<span data-ttu-id="ed59c-460">Hello stesso calcolo si applica toostatic classi di risorse.</span><span class="sxs-lookup"><span data-stu-id="ed59c-460">hello same calculation applies toostatic resource classes.</span></span>
 
## <a name="concurrency-slot-consumption"></a><span data-ttu-id="ed59c-461">Utilizzo di slot di concorrenza</span><span class="sxs-lookup"><span data-stu-id="ed59c-461">Concurrency slot consumption</span></span>  
<span data-ttu-id="ed59c-462">SQL Data Warehouse concede tooqueries di memoria più in esecuzione in più classi di risorse.</span><span class="sxs-lookup"><span data-stu-id="ed59c-462">SQL Data Warehouse grants more memory tooqueries running in higher resource classes.</span></span> <span data-ttu-id="ed59c-463">La memoria è una risorsa fissa.</span><span class="sxs-lookup"><span data-stu-id="ed59c-463">Memory is a fixed resource.</span></span>  <span data-ttu-id="ed59c-464">Pertanto, hello maggiore quantità di memoria allocata per ogni query, hello possono eseguire un minor numero di query simultanee.</span><span class="sxs-lookup"><span data-stu-id="ed59c-464">Therefore, hello more memory allocated per query, hello fewer concurrent queries can execute.</span></span> <span data-ttu-id="ed59c-465">Hello nella tabella seguente sono reiterates tutti hello concetti precedente in una singola visualizzazione che mostra il numero di hello di slot di concorrenza disponibili da DWU e slot hello utilizzato da ogni classe di risorse.</span><span class="sxs-lookup"><span data-stu-id="ed59c-465">hello following table reiterates all of hello previous concepts in a single view that shows hello number of concurrency slots available by DWU and hello slots consumed by each resource class.</span></span>  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a><span data-ttu-id="ed59c-466">Allocazione e consumo degli slot di concorrenza per le classi di risorse dinamiche</span><span class="sxs-lookup"><span data-stu-id="ed59c-466">Allocation and consumption of concurrency slots for dynamic resource classes</span></span>  
| <span data-ttu-id="ed59c-467">DWU</span><span class="sxs-lookup"><span data-stu-id="ed59c-467">DWU</span></span> | <span data-ttu-id="ed59c-468">Numero massimo di query simultanee</span><span class="sxs-lookup"><span data-stu-id="ed59c-468">Maximum concurrent queries</span></span> | <span data-ttu-id="ed59c-469">Numero di slot di concorrenza allocati</span><span class="sxs-lookup"><span data-stu-id="ed59c-469">Concurrency slots allocated</span></span> | <span data-ttu-id="ed59c-470">Slot utilizzati da smallrc</span><span class="sxs-lookup"><span data-stu-id="ed59c-470">Slots used by smallrc</span></span> | <span data-ttu-id="ed59c-471">Slot utilizzati da mediumrc</span><span class="sxs-lookup"><span data-stu-id="ed59c-471">Slots used by mediumrc</span></span> | <span data-ttu-id="ed59c-472">Slot utilizzati da largerc</span><span class="sxs-lookup"><span data-stu-id="ed59c-472">Slots used by largerc</span></span> | <span data-ttu-id="ed59c-473">Slot utilizzati da xlargerc</span><span class="sxs-lookup"><span data-stu-id="ed59c-473">Slots used by xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="ed59c-474">DW100</span><span class="sxs-lookup"><span data-stu-id="ed59c-474">DW100</span></span> |<span data-ttu-id="ed59c-475">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-475">4</span></span> |<span data-ttu-id="ed59c-476">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-476">4</span></span> |<span data-ttu-id="ed59c-477">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-477">1</span></span> |<span data-ttu-id="ed59c-478">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-478">1</span></span> |<span data-ttu-id="ed59c-479">2</span><span class="sxs-lookup"><span data-stu-id="ed59c-479">2</span></span> |<span data-ttu-id="ed59c-480">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-480">4</span></span> |
| <span data-ttu-id="ed59c-481">DW200</span><span class="sxs-lookup"><span data-stu-id="ed59c-481">DW200</span></span> |<span data-ttu-id="ed59c-482">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-482">8</span></span> |<span data-ttu-id="ed59c-483">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-483">8</span></span> |<span data-ttu-id="ed59c-484">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-484">1</span></span> |<span data-ttu-id="ed59c-485">2</span><span class="sxs-lookup"><span data-stu-id="ed59c-485">2</span></span> |<span data-ttu-id="ed59c-486">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-486">4</span></span> |<span data-ttu-id="ed59c-487">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-487">8</span></span> |
| <span data-ttu-id="ed59c-488">DW300</span><span class="sxs-lookup"><span data-stu-id="ed59c-488">DW300</span></span> |<span data-ttu-id="ed59c-489">12</span><span class="sxs-lookup"><span data-stu-id="ed59c-489">12</span></span> |<span data-ttu-id="ed59c-490">12</span><span class="sxs-lookup"><span data-stu-id="ed59c-490">12</span></span> |<span data-ttu-id="ed59c-491">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-491">1</span></span> |<span data-ttu-id="ed59c-492">2</span><span class="sxs-lookup"><span data-stu-id="ed59c-492">2</span></span> |<span data-ttu-id="ed59c-493">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-493">4</span></span> |<span data-ttu-id="ed59c-494">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-494">8</span></span> |
| <span data-ttu-id="ed59c-495">DW400</span><span class="sxs-lookup"><span data-stu-id="ed59c-495">DW400</span></span> |<span data-ttu-id="ed59c-496">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-496">16</span></span> |<span data-ttu-id="ed59c-497">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-497">16</span></span> |<span data-ttu-id="ed59c-498">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-498">1</span></span> |<span data-ttu-id="ed59c-499">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-499">4</span></span> |<span data-ttu-id="ed59c-500">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-500">8</span></span> |<span data-ttu-id="ed59c-501">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-501">16</span></span> |
| <span data-ttu-id="ed59c-502">DW500</span><span class="sxs-lookup"><span data-stu-id="ed59c-502">DW500</span></span> |<span data-ttu-id="ed59c-503">20</span><span class="sxs-lookup"><span data-stu-id="ed59c-503">20</span></span> |<span data-ttu-id="ed59c-504">20</span><span class="sxs-lookup"><span data-stu-id="ed59c-504">20</span></span> |<span data-ttu-id="ed59c-505">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-505">1</span></span> |<span data-ttu-id="ed59c-506">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-506">4</span></span> |<span data-ttu-id="ed59c-507">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-507">8</span></span> |<span data-ttu-id="ed59c-508">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-508">16</span></span> |
| <span data-ttu-id="ed59c-509">DW600</span><span class="sxs-lookup"><span data-stu-id="ed59c-509">DW600</span></span> |<span data-ttu-id="ed59c-510">24</span><span class="sxs-lookup"><span data-stu-id="ed59c-510">24</span></span> |<span data-ttu-id="ed59c-511">24</span><span class="sxs-lookup"><span data-stu-id="ed59c-511">24</span></span> |<span data-ttu-id="ed59c-512">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-512">1</span></span> |<span data-ttu-id="ed59c-513">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-513">4</span></span> |<span data-ttu-id="ed59c-514">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-514">8</span></span> |<span data-ttu-id="ed59c-515">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-515">16</span></span> |
| <span data-ttu-id="ed59c-516">DW1000</span><span class="sxs-lookup"><span data-stu-id="ed59c-516">DW1000</span></span> |<span data-ttu-id="ed59c-517">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-517">32</span></span> |<span data-ttu-id="ed59c-518">40</span><span class="sxs-lookup"><span data-stu-id="ed59c-518">40</span></span> |<span data-ttu-id="ed59c-519">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-519">1</span></span> |<span data-ttu-id="ed59c-520">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-520">8</span></span> |<span data-ttu-id="ed59c-521">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-521">16</span></span> |<span data-ttu-id="ed59c-522">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-522">32</span></span> |
| <span data-ttu-id="ed59c-523">DW1200</span><span class="sxs-lookup"><span data-stu-id="ed59c-523">DW1200</span></span> |<span data-ttu-id="ed59c-524">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-524">32</span></span> |<span data-ttu-id="ed59c-525">48</span><span class="sxs-lookup"><span data-stu-id="ed59c-525">48</span></span> |<span data-ttu-id="ed59c-526">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-526">1</span></span> |<span data-ttu-id="ed59c-527">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-527">8</span></span> |<span data-ttu-id="ed59c-528">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-528">16</span></span> |<span data-ttu-id="ed59c-529">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-529">32</span></span> |
| <span data-ttu-id="ed59c-530">DW1500</span><span class="sxs-lookup"><span data-stu-id="ed59c-530">DW1500</span></span> |<span data-ttu-id="ed59c-531">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-531">32</span></span> |<span data-ttu-id="ed59c-532">60</span><span class="sxs-lookup"><span data-stu-id="ed59c-532">60</span></span> |<span data-ttu-id="ed59c-533">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-533">1</span></span> |<span data-ttu-id="ed59c-534">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-534">8</span></span> |<span data-ttu-id="ed59c-535">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-535">16</span></span> |<span data-ttu-id="ed59c-536">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-536">32</span></span> |
| <span data-ttu-id="ed59c-537">DW2000</span><span class="sxs-lookup"><span data-stu-id="ed59c-537">DW2000</span></span> |<span data-ttu-id="ed59c-538">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-538">32</span></span> |<span data-ttu-id="ed59c-539">80</span><span class="sxs-lookup"><span data-stu-id="ed59c-539">80</span></span> |<span data-ttu-id="ed59c-540">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-540">1</span></span> |<span data-ttu-id="ed59c-541">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-541">16</span></span> |<span data-ttu-id="ed59c-542">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-542">32</span></span> |<span data-ttu-id="ed59c-543">64</span><span class="sxs-lookup"><span data-stu-id="ed59c-543">64</span></span> |
| <span data-ttu-id="ed59c-544">DW3000</span><span class="sxs-lookup"><span data-stu-id="ed59c-544">DW3000</span></span> |<span data-ttu-id="ed59c-545">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-545">32</span></span> |<span data-ttu-id="ed59c-546">120</span><span class="sxs-lookup"><span data-stu-id="ed59c-546">120</span></span> |<span data-ttu-id="ed59c-547">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-547">1</span></span> |<span data-ttu-id="ed59c-548">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-548">16</span></span> |<span data-ttu-id="ed59c-549">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-549">32</span></span> |<span data-ttu-id="ed59c-550">64</span><span class="sxs-lookup"><span data-stu-id="ed59c-550">64</span></span> |
| <span data-ttu-id="ed59c-551">DW6000</span><span class="sxs-lookup"><span data-stu-id="ed59c-551">DW6000</span></span> |<span data-ttu-id="ed59c-552">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-552">32</span></span> |<span data-ttu-id="ed59c-553">240</span><span class="sxs-lookup"><span data-stu-id="ed59c-553">240</span></span> |<span data-ttu-id="ed59c-554">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-554">1</span></span> |<span data-ttu-id="ed59c-555">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-555">32</span></span> |<span data-ttu-id="ed59c-556">64</span><span class="sxs-lookup"><span data-stu-id="ed59c-556">64</span></span> |<span data-ttu-id="ed59c-557">128</span><span class="sxs-lookup"><span data-stu-id="ed59c-557">128</span></span> |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a><span data-ttu-id="ed59c-558">Allocazione e consumo degli slot di concorrenza per le classi di risorse statiche</span><span class="sxs-lookup"><span data-stu-id="ed59c-558">Allocation and consumption of concurrency slots for static resource classes</span></span>  
| <span data-ttu-id="ed59c-559">DWU</span><span class="sxs-lookup"><span data-stu-id="ed59c-559">DWU</span></span> | <span data-ttu-id="ed59c-560">Numero massimo di query simultanee</span><span class="sxs-lookup"><span data-stu-id="ed59c-560">Maximum concurrent queries</span></span> | <span data-ttu-id="ed59c-561">Numero di slot di concorrenza allocati</span><span class="sxs-lookup"><span data-stu-id="ed59c-561">Concurrency slots allocated</span></span> |<span data-ttu-id="ed59c-562">staticrc10</span><span class="sxs-lookup"><span data-stu-id="ed59c-562">staticrc10</span></span> | <span data-ttu-id="ed59c-563">staticrc20</span><span class="sxs-lookup"><span data-stu-id="ed59c-563">staticrc20</span></span> | <span data-ttu-id="ed59c-564">staticrc30</span><span class="sxs-lookup"><span data-stu-id="ed59c-564">staticrc30</span></span> | <span data-ttu-id="ed59c-565">staticrc40</span><span class="sxs-lookup"><span data-stu-id="ed59c-565">staticrc40</span></span> | <span data-ttu-id="ed59c-566">staticrc50</span><span class="sxs-lookup"><span data-stu-id="ed59c-566">staticrc50</span></span> | <span data-ttu-id="ed59c-567">staticrc60</span><span class="sxs-lookup"><span data-stu-id="ed59c-567">staticrc60</span></span> | <span data-ttu-id="ed59c-568">staticrc70</span><span class="sxs-lookup"><span data-stu-id="ed59c-568">staticrc70</span></span> | <span data-ttu-id="ed59c-569">staticrc80</span><span class="sxs-lookup"><span data-stu-id="ed59c-569">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="ed59c-570">DW100</span><span class="sxs-lookup"><span data-stu-id="ed59c-570">DW100</span></span> |<span data-ttu-id="ed59c-571">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-571">4</span></span> |<span data-ttu-id="ed59c-572">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-572">4</span></span> |<span data-ttu-id="ed59c-573">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-573">1</span></span> |<span data-ttu-id="ed59c-574">2</span><span class="sxs-lookup"><span data-stu-id="ed59c-574">2</span></span> |<span data-ttu-id="ed59c-575">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-575">4</span></span> |<span data-ttu-id="ed59c-576">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-576">4</span></span> |<span data-ttu-id="ed59c-577">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-577">4</span></span> |<span data-ttu-id="ed59c-578">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-578">4</span></span> |<span data-ttu-id="ed59c-579">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-579">4</span></span> |<span data-ttu-id="ed59c-580">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-580">4</span></span> |
| <span data-ttu-id="ed59c-581">DW200</span><span class="sxs-lookup"><span data-stu-id="ed59c-581">DW200</span></span> |<span data-ttu-id="ed59c-582">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-582">8</span></span> |<span data-ttu-id="ed59c-583">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-583">8</span></span> |<span data-ttu-id="ed59c-584">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-584">1</span></span> |<span data-ttu-id="ed59c-585">2</span><span class="sxs-lookup"><span data-stu-id="ed59c-585">2</span></span> |<span data-ttu-id="ed59c-586">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-586">4</span></span> |<span data-ttu-id="ed59c-587">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-587">8</span></span> |<span data-ttu-id="ed59c-588">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-588">8</span></span> |<span data-ttu-id="ed59c-589">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-589">8</span></span> |<span data-ttu-id="ed59c-590">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-590">8</span></span> |<span data-ttu-id="ed59c-591">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-591">8</span></span> |
| <span data-ttu-id="ed59c-592">DW300</span><span class="sxs-lookup"><span data-stu-id="ed59c-592">DW300</span></span> |<span data-ttu-id="ed59c-593">12</span><span class="sxs-lookup"><span data-stu-id="ed59c-593">12</span></span> |<span data-ttu-id="ed59c-594">12</span><span class="sxs-lookup"><span data-stu-id="ed59c-594">12</span></span> |<span data-ttu-id="ed59c-595">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-595">1</span></span> |<span data-ttu-id="ed59c-596">2</span><span class="sxs-lookup"><span data-stu-id="ed59c-596">2</span></span> |<span data-ttu-id="ed59c-597">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-597">4</span></span> |<span data-ttu-id="ed59c-598">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-598">8</span></span> |<span data-ttu-id="ed59c-599">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-599">8</span></span> |<span data-ttu-id="ed59c-600">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-600">8</span></span> |<span data-ttu-id="ed59c-601">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-601">8</span></span> |<span data-ttu-id="ed59c-602">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-602">8</span></span> |
| <span data-ttu-id="ed59c-603">DW400</span><span class="sxs-lookup"><span data-stu-id="ed59c-603">DW400</span></span> |<span data-ttu-id="ed59c-604">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-604">16</span></span> |<span data-ttu-id="ed59c-605">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-605">16</span></span> |<span data-ttu-id="ed59c-606">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-606">1</span></span> |<span data-ttu-id="ed59c-607">2</span><span class="sxs-lookup"><span data-stu-id="ed59c-607">2</span></span> |<span data-ttu-id="ed59c-608">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-608">4</span></span> |<span data-ttu-id="ed59c-609">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-609">8</span></span> |<span data-ttu-id="ed59c-610">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-610">16</span></span> |<span data-ttu-id="ed59c-611">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-611">16</span></span> |<span data-ttu-id="ed59c-612">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-612">16</span></span> |<span data-ttu-id="ed59c-613">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-613">16</span></span> |
| <span data-ttu-id="ed59c-614">DW500</span><span class="sxs-lookup"><span data-stu-id="ed59c-614">DW500</span></span> | <span data-ttu-id="ed59c-615">20</span><span class="sxs-lookup"><span data-stu-id="ed59c-615">20</span></span>| <span data-ttu-id="ed59c-616">20</span><span class="sxs-lookup"><span data-stu-id="ed59c-616">20</span></span>| <span data-ttu-id="ed59c-617">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-617">1</span></span>| <span data-ttu-id="ed59c-618">2</span><span class="sxs-lookup"><span data-stu-id="ed59c-618">2</span></span>| <span data-ttu-id="ed59c-619">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-619">4</span></span>| <span data-ttu-id="ed59c-620">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-620">8</span></span>| <span data-ttu-id="ed59c-621">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-621">16</span></span>| <span data-ttu-id="ed59c-622">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-622">16</span></span>| <span data-ttu-id="ed59c-623">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-623">16</span></span>| <span data-ttu-id="ed59c-624">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-624">16</span></span>|
| <span data-ttu-id="ed59c-625">DW600</span><span class="sxs-lookup"><span data-stu-id="ed59c-625">DW600</span></span> | <span data-ttu-id="ed59c-626">24</span><span class="sxs-lookup"><span data-stu-id="ed59c-626">24</span></span>| <span data-ttu-id="ed59c-627">24</span><span class="sxs-lookup"><span data-stu-id="ed59c-627">24</span></span>| <span data-ttu-id="ed59c-628">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-628">1</span></span>| <span data-ttu-id="ed59c-629">2</span><span class="sxs-lookup"><span data-stu-id="ed59c-629">2</span></span>| <span data-ttu-id="ed59c-630">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-630">4</span></span>| <span data-ttu-id="ed59c-631">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-631">8</span></span>| <span data-ttu-id="ed59c-632">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-632">16</span></span>| <span data-ttu-id="ed59c-633">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-633">16</span></span>| <span data-ttu-id="ed59c-634">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-634">16</span></span>| <span data-ttu-id="ed59c-635">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-635">16</span></span>|
| <span data-ttu-id="ed59c-636">DW1000</span><span class="sxs-lookup"><span data-stu-id="ed59c-636">DW1000</span></span> | <span data-ttu-id="ed59c-637">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-637">32</span></span>| <span data-ttu-id="ed59c-638">40</span><span class="sxs-lookup"><span data-stu-id="ed59c-638">40</span></span>| <span data-ttu-id="ed59c-639">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-639">1</span></span>| <span data-ttu-id="ed59c-640">2</span><span class="sxs-lookup"><span data-stu-id="ed59c-640">2</span></span>| <span data-ttu-id="ed59c-641">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-641">4</span></span>| <span data-ttu-id="ed59c-642">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-642">8</span></span>| <span data-ttu-id="ed59c-643">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-643">16</span></span>| <span data-ttu-id="ed59c-644">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-644">32</span></span>| <span data-ttu-id="ed59c-645">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-645">32</span></span>| <span data-ttu-id="ed59c-646">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-646">32</span></span>|
| <span data-ttu-id="ed59c-647">DW1200</span><span class="sxs-lookup"><span data-stu-id="ed59c-647">DW1200</span></span> | <span data-ttu-id="ed59c-648">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-648">32</span></span>| <span data-ttu-id="ed59c-649">48</span><span class="sxs-lookup"><span data-stu-id="ed59c-649">48</span></span>| <span data-ttu-id="ed59c-650">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-650">1</span></span>| <span data-ttu-id="ed59c-651">2</span><span class="sxs-lookup"><span data-stu-id="ed59c-651">2</span></span>| <span data-ttu-id="ed59c-652">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-652">4</span></span>| <span data-ttu-id="ed59c-653">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-653">8</span></span>| <span data-ttu-id="ed59c-654">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-654">16</span></span>| <span data-ttu-id="ed59c-655">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-655">32</span></span>| <span data-ttu-id="ed59c-656">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-656">32</span></span>| <span data-ttu-id="ed59c-657">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-657">32</span></span>|
| <span data-ttu-id="ed59c-658">DW1500</span><span class="sxs-lookup"><span data-stu-id="ed59c-658">DW1500</span></span> | <span data-ttu-id="ed59c-659">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-659">32</span></span>| <span data-ttu-id="ed59c-660">60</span><span class="sxs-lookup"><span data-stu-id="ed59c-660">60</span></span>| <span data-ttu-id="ed59c-661">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-661">1</span></span>| <span data-ttu-id="ed59c-662">2</span><span class="sxs-lookup"><span data-stu-id="ed59c-662">2</span></span>| <span data-ttu-id="ed59c-663">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-663">4</span></span>| <span data-ttu-id="ed59c-664">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-664">8</span></span>| <span data-ttu-id="ed59c-665">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-665">16</span></span>| <span data-ttu-id="ed59c-666">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-666">32</span></span>| <span data-ttu-id="ed59c-667">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-667">32</span></span>| <span data-ttu-id="ed59c-668">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-668">32</span></span>|
| <span data-ttu-id="ed59c-669">DW2000</span><span class="sxs-lookup"><span data-stu-id="ed59c-669">DW2000</span></span> | <span data-ttu-id="ed59c-670">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-670">32</span></span>| <span data-ttu-id="ed59c-671">80</span><span class="sxs-lookup"><span data-stu-id="ed59c-671">80</span></span>| <span data-ttu-id="ed59c-672">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-672">1</span></span>| <span data-ttu-id="ed59c-673">2</span><span class="sxs-lookup"><span data-stu-id="ed59c-673">2</span></span>| <span data-ttu-id="ed59c-674">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-674">4</span></span>| <span data-ttu-id="ed59c-675">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-675">8</span></span>| <span data-ttu-id="ed59c-676">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-676">16</span></span>| <span data-ttu-id="ed59c-677">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-677">32</span></span>| <span data-ttu-id="ed59c-678">64</span><span class="sxs-lookup"><span data-stu-id="ed59c-678">64</span></span>| <span data-ttu-id="ed59c-679">64</span><span class="sxs-lookup"><span data-stu-id="ed59c-679">64</span></span>|
| <span data-ttu-id="ed59c-680">DW3000</span><span class="sxs-lookup"><span data-stu-id="ed59c-680">DW3000</span></span> | <span data-ttu-id="ed59c-681">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-681">32</span></span>| <span data-ttu-id="ed59c-682">120</span><span class="sxs-lookup"><span data-stu-id="ed59c-682">120</span></span>| <span data-ttu-id="ed59c-683">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-683">1</span></span>| <span data-ttu-id="ed59c-684">2</span><span class="sxs-lookup"><span data-stu-id="ed59c-684">2</span></span>| <span data-ttu-id="ed59c-685">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-685">4</span></span>| <span data-ttu-id="ed59c-686">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-686">8</span></span>| <span data-ttu-id="ed59c-687">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-687">16</span></span>| <span data-ttu-id="ed59c-688">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-688">32</span></span>| <span data-ttu-id="ed59c-689">64</span><span class="sxs-lookup"><span data-stu-id="ed59c-689">64</span></span>| <span data-ttu-id="ed59c-690">64</span><span class="sxs-lookup"><span data-stu-id="ed59c-690">64</span></span>|
| <span data-ttu-id="ed59c-691">DW6000</span><span class="sxs-lookup"><span data-stu-id="ed59c-691">DW6000</span></span> | <span data-ttu-id="ed59c-692">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-692">32</span></span>| <span data-ttu-id="ed59c-693">240</span><span class="sxs-lookup"><span data-stu-id="ed59c-693">240</span></span>| <span data-ttu-id="ed59c-694">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-694">1</span></span>| <span data-ttu-id="ed59c-695">2</span><span class="sxs-lookup"><span data-stu-id="ed59c-695">2</span></span>| <span data-ttu-id="ed59c-696">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-696">4</span></span>| <span data-ttu-id="ed59c-697">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-697">8</span></span>| <span data-ttu-id="ed59c-698">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-698">16</span></span>| <span data-ttu-id="ed59c-699">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-699">32</span></span>| <span data-ttu-id="ed59c-700">64</span><span class="sxs-lookup"><span data-stu-id="ed59c-700">64</span></span>| <span data-ttu-id="ed59c-701">128</span><span class="sxs-lookup"><span data-stu-id="ed59c-701">128</span></span>|

<span data-ttu-id="ed59c-702">Come si può notare da queste tabelle, l'esecuzione di SQL Data Warehouse come DW1000 alloca un massimo di 32 query simultanee e un totale di 40 slot di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="ed59c-702">From these tables, you can see that SQL Data Warehouse running as DW1000 allocates a maximum of 32 concurrent queries and a total of 40 concurrency slots.</span></span> <span data-ttu-id="ed59c-703">Se l'esecuzione avviene da parte di tutti gli utenti nella classe smallrc, vengono consentite 32 query simultanee, poiché ognuna richiede 1 slot di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="ed59c-703">If all users are running in smallrc, 32 concurrent queries would be allowed because each query would consume 1 concurrency slot.</span></span> <span data-ttu-id="ed59c-704">Se tutti gli utenti di un DW1000 erano in esecuzione in mediumrc, ogni query viene allocata 800 MB per ogni distribuzione di un'allocazione di memoria totale di 47 GB per ogni query e concorrenza sarebbe utenti too5 limitato (40 slot concorrenza slot 8 per ogni utente mediumrc /).</span><span class="sxs-lookup"><span data-stu-id="ed59c-704">If all users on a DW1000 were running in mediumrc, each query would be allocated 800 MB per distribution for a total memory allocation of 47 GB per query, and concurrency would be limited too5 users (40 concurrency slots / 8 slots per mediumrc user).</span></span>

## <a name="selecting-proper-resource-class"></a><span data-ttu-id="ed59c-705">Scelta della classe di risorse appropriata</span><span class="sxs-lookup"><span data-stu-id="ed59c-705">Selecting proper resource class</span></span>  
<span data-ttu-id="ed59c-706">Una buona norma è una classe di risorse tooa toopermanently assegnare gli utenti, anziché modificare le classi di risorse.</span><span class="sxs-lookup"><span data-stu-id="ed59c-706">A good practice is toopermanently assign users tooa resource class rather than changing their resource classes.</span></span> <span data-ttu-id="ed59c-707">Ad esempio, le tabelle columnstore tooclustered di carichi di creare gli indici di qualità superiore quando allocata più memoria.</span><span class="sxs-lookup"><span data-stu-id="ed59c-707">For example, loads tooclustered columnstore tables create higher-quality indexes when allocated more memory.</span></span> <span data-ttu-id="ed59c-708">tooensure che dispongono di accesso toohigher memoria carichi, creare un utente in modo specifico per il caricamento dei dati e assegnata in modo permanente questa classe di risorse utente tooa superiore.</span><span class="sxs-lookup"><span data-stu-id="ed59c-708">tooensure that loads have access toohigher memory, create a user specifically for loading data and permanently assign this user tooa higher resource class.</span></span>
<span data-ttu-id="ed59c-709">Esistono un paio di procedure consigliate, toofollow qui.</span><span class="sxs-lookup"><span data-stu-id="ed59c-709">There are a couple of best practices toofollow here.</span></span> <span data-ttu-id="ed59c-710">Come indicato in precedenza, SQL Data Warehouse supporta due tipi di classi di risorse: le classi di risorse statiche e quelle dinamiche.</span><span class="sxs-lookup"><span data-stu-id="ed59c-710">As mentioned above, SQL DW supports two kinds of resource class types: static resource classes and dynamic resource classes.</span></span>
### <a name="loading-best-practices"></a><span data-ttu-id="ed59c-711">Procedure consigliate per il caricamento</span><span class="sxs-lookup"><span data-stu-id="ed59c-711">Loading best practices</span></span>
1.  <span data-ttu-id="ed59c-712">Se le aspettative hello caricamenti regolari quantità di dati, una classe di risorse statiche è una scelta ottimale.</span><span class="sxs-lookup"><span data-stu-id="ed59c-712">If hello expectations are loads with regular amount of data, a static resource class is a good choice.</span></span> <span data-ttu-id="ed59c-713">In un secondo momento, quando la scalabilità verticale tooget ulteriori capacità di calcolo, data warehouse di hello sarà in grado di toorun simultanea di più query out-of-the-box, come l'utente hello non utilizzata più memoria.</span><span class="sxs-lookup"><span data-stu-id="ed59c-713">Later, when scaling up tooget more computational power, hello data warehouse will be able toorun more concurrent queries out-of-the-box, as hello load user does not consume more memory.</span></span>
2.  <span data-ttu-id="ed59c-714">Se le aspettative hello Carica più grande in alcuni casi, una classe di risorse dinamiche è una scelta ottimale.</span><span class="sxs-lookup"><span data-stu-id="ed59c-714">If hello expectations are bigger loads in some occasions, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="ed59c-715">In un secondo momento, nel caso di aumento tooget maggiore potenza di calcolo, hello carico utente riceverà più memoria out-of-the-box, pertanto consentendo hello carico tooperform più velocemente.</span><span class="sxs-lookup"><span data-stu-id="ed59c-715">Later, when scaling up tooget more computational power, hello load user will get more memory out-of-the-box, hence allowing hello load tooperform faster.</span></span>

<span data-ttu-id="ed59c-716">Hello carichi tooprocess memoria necessaria in modo efficiente dipende dalla natura hello della tabella hello caricata e quantità hello dei dati elaborati.</span><span class="sxs-lookup"><span data-stu-id="ed59c-716">hello memory needed tooprocess loads efficiently depends on hello nature of hello table loaded and hello amount of data processed.</span></span> <span data-ttu-id="ed59c-717">Ad esempio, il caricamento di dati nelle tabelle CCI richiede che alcuni gruppi di righe di memoria toolet CCI raggiungere validità.</span><span class="sxs-lookup"><span data-stu-id="ed59c-717">For instance, loading data into CCI tables requires some memory toolet CCI rowgroups reach optimality.</span></span> <span data-ttu-id="ed59c-718">Per ulteriori informazioni, vedere gli indici Columnstore hello - Guida di caricamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="ed59c-718">For more details, see hello Columnstore indexes - data loading guidance.</span></span>

<span data-ttu-id="ed59c-719">Come procedura consigliata, si consiglia di toouse almeno 200MB di memoria per i caricamenti.</span><span class="sxs-lookup"><span data-stu-id="ed59c-719">As a best practice, we advise you toouse at least 200MB of memory for loads.</span></span>

### <a name="querying-best-practices"></a><span data-ttu-id="ed59c-720">Procedure consigliate per le query</span><span class="sxs-lookup"><span data-stu-id="ed59c-720">Querying best practices</span></span>
<span data-ttu-id="ed59c-721">Le query hanno diversi requisiti a seconda della complessità.</span><span class="sxs-lookup"><span data-stu-id="ed59c-721">Queries have different requirements depending on their complexity.</span></span> <span data-ttu-id="ed59c-722">Aumentare la memoria per ogni query o ad aumentare la concorrenza hello sono entrambi tooaugment validi velocità effettiva globale a seconda delle esigenze di query hello.</span><span class="sxs-lookup"><span data-stu-id="ed59c-722">Increasing memory per query or increasing hello concurrency are both valid ways tooaugment overall throughput depending on hello query needs.</span></span>
1.  <span data-ttu-id="ed59c-723">Se le aspettative hello sono query complesse, regolare (ad esempio, toogenerate report giornaliero e settimanale) e non richiedono alcun vantaggio tootake di concorrenza, una classe di risorse dinamiche è una scelta ottimale.</span><span class="sxs-lookup"><span data-stu-id="ed59c-723">If hello expectations are regular, complex queries (for instance, toogenerate daily and weekly reports) and do not need tootake advantage of concurrency, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="ed59c-724">Se hello sistema dispone di ulteriori dati tooprocess, l'aumento di data warehouse di hello verrà pertanto automaticamente fornire più memoria toohello utente che esegue query hello.</span><span class="sxs-lookup"><span data-stu-id="ed59c-724">If hello system has more data tooprocess, scaling up hello data warehouse will therefore automatically provide more memory toohello user running hello query.</span></span>
2.  <span data-ttu-id="ed59c-725">Se le aspettative hello sono modelli di concorrenza diurna o variabile (ad esempio se viene eseguita una query di database hello tramite un web su vasta scala accessibile dell'interfaccia utente), una classe di risorse statiche è una scelta ottimale.</span><span class="sxs-lookup"><span data-stu-id="ed59c-725">If hello expectations are variable or diurnal concurrency patterns (for instance if hello database is queried through a web UI broadly accessible), a static resource class is a good choice.</span></span> <span data-ttu-id="ed59c-726">In un secondo momento, nel caso di aumento warehouse toodata utente hello associata alla classe di risorse statiche hello verrà automaticamente essere in grado di toorun simultanea di più query.</span><span class="sxs-lookup"><span data-stu-id="ed59c-726">Later, when scaling up toodata warehouse, hello user associated with hello static resource class will automatically be able toorun more concurrent queries.</span></span>

<span data-ttu-id="ed59c-727">Selezionando concessione di memoria appropriata a seconda delle necessità di hello della query è considerevole, in quanto dipende molti fattori, ad esempio quantità hello di dati sottoposti a query, natura hello gli schemi di tabella hello e vari join, selezione e predicati di gruppo.</span><span class="sxs-lookup"><span data-stu-id="ed59c-727">Selecting proper memory grant depending on hello need of your query is non-trivial, as it depends on many factors, such as hello amount of data queried, hello nature of hello table schemas, and various join, selection, and group predicates.</span></span> <span data-ttu-id="ed59c-728">Dal punto di vista generale, allocazione di ulteriore memoria consentirà toocomplete query più veloce, ma consentirebbe di ridurre hello concorrenza complessiva.</span><span class="sxs-lookup"><span data-stu-id="ed59c-728">From a general standpoint, allocating more memory will allow queries toocomplete faster, but would reduce hello overall concurrency.</span></span> <span data-ttu-id="ed59c-729">Se la concorrenza non è un problema, un'allocazione eccessiva di memoria non causa alcun danno.</span><span class="sxs-lookup"><span data-stu-id="ed59c-729">If concurrency is not an issue, over-allocating memory does not harm.</span></span> <span data-ttu-id="ed59c-730">velocità effettiva toofine ottimizzazione, durante il tentativo varie caratteristiche di classi di risorse potrebbe essere necessario.</span><span class="sxs-lookup"><span data-stu-id="ed59c-730">toofine-tune throughput, trying various flavors of resource classes may be required.</span></span>

<span data-ttu-id="ed59c-731">È possibile utilizzare hello seguente stored procedure toofigure out concessione di memoria e concorrenza per ogni classe di risorse in corrispondenza di una determinata SLO e hello più vicino migliore classe di risorse per operazioni CCI con uso intensivo della memoria nella tabella non partizionata di CCI in una classe di risorse specificato:</span><span class="sxs-lookup"><span data-stu-id="ed59c-731">You can use hello following stored procedure toofigure out concurrency and memory grant per resource class at a given SLO and hello closest best resource class for memory intensive CCI operations on non-partitioned CCI table at a given resource class:</span></span>

#### <a name="description"></a><span data-ttu-id="ed59c-732">Descrizione:</span><span class="sxs-lookup"><span data-stu-id="ed59c-732">Description:</span></span>  
<span data-ttu-id="ed59c-733">Ecco scopo hello della stored procedure:</span><span class="sxs-lookup"><span data-stu-id="ed59c-733">Here's hello purpose of this stored procedure:</span></span>  
1. <span data-ttu-id="ed59c-734">toohelp utente individuare concessione di memoria e concorrenza per ogni classe di risorse in un determinato SLO.</span><span class="sxs-lookup"><span data-stu-id="ed59c-734">toohelp user figure out concurrency and memory grant per resource class at a given SLO.</span></span> <span data-ttu-id="ed59c-735">Utente deve tooprovide NULL per lo schema e tablename per questo oggetto, come illustrato nel seguente esempio hello.</span><span class="sxs-lookup"><span data-stu-id="ed59c-735">User needs tooprovide NULL for both schema and tablename for this as shown in hello example below.</span></span>  
2. <span data-ttu-id="ed59c-736">utente toohelp scoprire hello più vicino migliore classe di risorse per hello memoria intensed operazioni CCI (caricamento, la tabella di copia, ricompilazione dell'indice e così via) nella tabella non partizionata di CCI in una classe di risorse specificato.</span><span class="sxs-lookup"><span data-stu-id="ed59c-736">toohelp user figure out hello closest best resource class for hello memory intensed CCI operations (load, copy table, rebuild index, etc.) on non partitioned CCI table at a given resource class.</span></span> <span data-ttu-id="ed59c-737">Hello stored procedure utilizza toofind dello schema di tabella out hello concessione di memoria necessaria per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="ed59c-737">hello stored proc uses table schema toofind out hello required memory grant for this.</span></span>

#### <a name="dependencies--restrictions"></a><span data-ttu-id="ed59c-738">Dipendenze e restrizioni:</span><span class="sxs-lookup"><span data-stu-id="ed59c-738">Dependencies & Restrictions:</span></span>
- <span data-ttu-id="ed59c-739">Questa stored procedure non è il requisito di memoria toocalculate progettato per la tabella partizionata indice ColumnStore cluster.</span><span class="sxs-lookup"><span data-stu-id="ed59c-739">This stored proc is not designed toocalculate memory requirement for partitioned-cci table.</span></span>    
- <span data-ttu-id="ed59c-740">Questa stored procedure non accetta requisito di memoria in considerazione per hello della parte SELECT di un'istruzione CTAS/INSERT-SELECT e presume che sia toobe un'istruzione SELECT semplice.</span><span class="sxs-lookup"><span data-stu-id="ed59c-740">This stored proc doesn't take memory requirement into account for hello SELECT part of CTAS/INSERT-SELECT and assumes it toobe a simple SELECT.</span></span>
- <span data-ttu-id="ed59c-741">Questa stored procedure utilizza una tabella temporanea in modo utilizzabile nella sessione hello in cui è stata creata questa stored procedure.</span><span class="sxs-lookup"><span data-stu-id="ed59c-741">This stored proc uses a temp table so this can be used in hello session where this stored proc was created.</span></span>    
- <span data-ttu-id="ed59c-742">Questa stored procedure dipende da hello attuali offerte (ad esempio, la configurazione hardware, configurazione DMS) e se uno qualsiasi di tale modifica quindi questa stored procedure non funzionerà correttamente.</span><span class="sxs-lookup"><span data-stu-id="ed59c-742">This stored proc depends on hello current offerings (e.g. hardware configuration, DMS config) and if any of that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="ed59c-743">Questa stored procedure dipende dal limite di concorrenza esistente e in caso di modifiche non funziona più correttamente.</span><span class="sxs-lookup"><span data-stu-id="ed59c-743">This stored proc depends on existing offered concurrency limit and if that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="ed59c-744">Questa stored procedure dipende dalle classi di risorse esistenti e in caso di modifiche non funziona più correttamente.</span><span class="sxs-lookup"><span data-stu-id="ed59c-744">This stored proc depends on existing resource class offerings and if that changes then this stored proc wuold not work correctly.</span></span>  

>  [!NOTE]  
>  <span data-ttu-id="ed59c-745">Se non si ottiene alcun output dopo l'esecuzione della stored procedure con i parametri forniti, i motivi potrebbero essere due.</span><span class="sxs-lookup"><span data-stu-id="ed59c-745">If you are not getting output after executing stored procedure with parameters provided then there could be two cases.</span></span> <br /><span data-ttu-id="ed59c-746">1. Uno dei parametri di Data Warehouse contiene un valore SLO non valido</span><span class="sxs-lookup"><span data-stu-id="ed59c-746">1. Either DW Parameter contains invalid SLO value</span></span> <br /><span data-ttu-id="ed59c-747">2. OPPURE non ci sono classi di risorse corrispondenti per l'operazione CCI se è stato fornito il nome della tabella.</span><span class="sxs-lookup"><span data-stu-id="ed59c-747">2. OR there are no matching resource class for CCI operation if table name was provided.</span></span> <br /><span data-ttu-id="ed59c-748">Ad esempio, DW100, concessione di memoria massima disponibile è 400MB e se lo schema della tabella è di tipo wide sufficiente toocross hello requisito di 400MB.</span><span class="sxs-lookup"><span data-stu-id="ed59c-748">For example, at DW100, highest memory grant available is 400MB and if table schema is wide enough toocross hello requirement of 400MB.</span></span>
      
#### <a name="usage-example"></a><span data-ttu-id="ed59c-749">Esempio d'uso:</span><span class="sxs-lookup"><span data-stu-id="ed59c-749">Usage example:</span></span>
<span data-ttu-id="ed59c-750">Sintassi:</span><span class="sxs-lookup"><span data-stu-id="ed59c-750">Syntax:</span></span>  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. <span data-ttu-id="ed59c-751">@DWU:Fornire un tooextract di parametro NULL hello DWU corrente dal database di data Warehouse hello o fornire qualsiasi supportato DWU sotto forma di hello di 'DW100'</span><span class="sxs-lookup"><span data-stu-id="ed59c-751">@DWU: Either provide a NULL parameter tooextract hello current DWU from hello DW DB or provide any supported DWU in hello form of 'DW100'</span></span>
2. <span data-ttu-id="ed59c-752">@SCHEMA_NAME:Specificare un nome di schema della tabella hello</span><span class="sxs-lookup"><span data-stu-id="ed59c-752">@SCHEMA_NAME: Provide a schema name of hello table</span></span>
3. <span data-ttu-id="ed59c-753">@TABLE_NAME:Specificare un nome di tabella di interesse hello</span><span class="sxs-lookup"><span data-stu-id="ed59c-753">@TABLE_NAME: Provide a table name of hello interest</span></span>

<span data-ttu-id="ed59c-754">Esempi di esecuzione di questa stored procedure:</span><span class="sxs-lookup"><span data-stu-id="ed59c-754">Examples executing this stored proc:</span></span>  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

<span data-ttu-id="ed59c-755">È stato possibile creare Table1 utilizzato in hello esempi sopra riportati come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="ed59c-755">Table1 used in hello above examples could be created as below:</span></span>  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-hello-stored-procedure-definition"></a><span data-ttu-id="ed59c-756">Ecco hello stored procedure definizione:</span><span class="sxs-lookup"><span data-stu-id="ed59c-756">Here's hello stored procedure definition:</span></span>
```sql  
-------------------------------------------------------------------------------
-- Dropping prc_workload_management_by_DWU procedure if it exists.
-------------------------------------------------------------------------------
IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'prc_workload_management_by_DWU')
DROP PROCEDURE dbo.prc_workload_management_by_DWU
GO

-------------------------------------------------------------------------------
-- Creating prc_workload_management_by_DWU.
-------------------------------------------------------------------------------
CREATE PROCEDURE dbo.prc_workload_management_by_DWU
(   @DWU VARCHAR(7),
      @SCHEMA_NAME VARCHAR(128),
       @TABLE_NAME VARCHAR(128)
)
AS
IF @DWU IS NULL
BEGIN
-- Selecting proper DWU for hello current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need toosupply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) toohold mapping info.
-- CREATE TABLE #ref
CREATE TABLE #ref
WITH (DISTRIBUTION = ROUND_ROBIN)
AS 
WITH
-- Creating concurrency slots mapping for various DWUs.
alloc
AS
(
  SELECT 'DW100' AS DWU, 4 AS max_queries, 4 AS max_slots, 1 AS slots_used_smallrc, 1 AS slots_used_mediumrc,
        2 AS slots_used_largerc, 4 AS slots_used_xlargerc, 1 AS slots_used_staticrc10, 2 AS slots_used_staticrc20,
        4 AS slots_used_staticrc30, 4 AS slots_used_staticrc40, 4 AS slots_used_staticrc50,
        4 AS slots_used_staticrc60, 4 AS slots_used_staticrc70, 4 AS slots_used_staticrc80
  UNION ALL
    SELECT 'DW200', 8, 8, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW300', 12, 12, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW400', 16, 16, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
     SELECT 'DW500', 20, 20, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW600', 24, 24, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW1000', 32, 40, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1200', 32, 48, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1500', 32, 60, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW2000', 32, 80, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
   SELECT 'DW3000', 32, 120, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
    SELECT 'DW6000', 32, 240, 1, 32, 64, 128, 1, 2, 4, 8, 16, 32, 64, 128
)
-- Creating workload mapping tootheir corresponding slot consumption and default memory grant.
,map
AS
(
  SELECT 'SloDWGroupC00' AS wg_name,1 AS slots_used,100 AS tgt_mem_grant_MB
  UNION ALL
    SELECT 'SloDWGroupC01',2,200
  UNION ALL
    SELECT 'SloDWGroupC02',4,400
  UNION ALL
    SELECT 'SloDWGroupC03',8,800
  UNION ALL
    SELECT 'SloDWGroupC04',16,1600
  UNION ALL
    SELECT 'SloDWGroupC05',32,3200
  UNION ALL
    SELECT 'SloDWGroupC06',64,6400
  UNION ALL
    SELECT 'SloDWGroupC07',128,12800
)
-- Creating ref based on current / asked DWU.
, ref
AS
(
  SELECT  a1.*
  ,       m1.wg_name          AS wg_name_smallrc
  ,       m1.tgt_mem_grant_MB AS tgt_mem_grant_MB_smallrc
  ,       m2.wg_name          AS wg_name_mediumrc
  ,       m2.tgt_mem_grant_MB AS tgt_mem_grant_MB_mediumrc
  ,       m3.wg_name          AS wg_name_largerc
  ,       m3.tgt_mem_grant_MB AS tgt_mem_grant_MB_largerc
  ,       m4.wg_name          AS wg_name_xlargerc
  ,       m4.tgt_mem_grant_MB AS tgt_mem_grant_MB_xlargerc
  ,       m5.wg_name          AS wg_name_staticrc10
  ,       m5.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc10
  ,       m6.wg_name          AS wg_name_staticrc20
  ,       m6.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc20
  ,       m7.wg_name          AS wg_name_staticrc30
  ,       m7.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc30
  ,       m8.wg_name          AS wg_name_staticrc40
  ,       m8.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc40
  ,       m9.wg_name          AS wg_name_staticrc50
  ,       m9.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc50
  ,       m10.wg_name          AS wg_name_staticrc60
  ,       m10.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc60
  ,       m11.wg_name          AS wg_name_staticrc70
  ,       m11.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc70
  ,       m12.wg_name          AS wg_name_staticrc80
  ,       m12.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc80
  FROM alloc a1
  JOIN map   m1  ON a1.slots_used_smallrc     = m1.slots_used
  JOIN map   m2  ON a1.slots_used_mediumrc    = m2.slots_used
  JOIN map   m3  ON a1.slots_used_largerc     = m3.slots_used
  JOIN map   m4  ON a1.slots_used_xlargerc    = m4.slots_used
  JOIN map   m5  ON a1.slots_used_staticrc10    = m5.slots_used
  JOIN map   m6  ON a1.slots_used_staticrc20    = m6.slots_used
  JOIN map   m7  ON a1.slots_used_staticrc30    = m7.slots_used
  JOIN map   m8  ON a1.slots_used_staticrc40    = m8.slots_used
  JOIN map   m9  ON a1.slots_used_staticrc50    = m9.slots_used
  JOIN map   m10  ON a1.slots_used_staticrc60    = m10.slots_used
  JOIN map   m11  ON a1.slots_used_staticrc70    = m11.slots_used
  JOIN map   m12  ON a1.slots_used_staticrc80    = m12.slots_used
-- WHERE   a1.DWU = @DWU
  WHERE   a1.DWU = UPPER(@DWU)
)
SELECT  DWU
,       max_queries
,       max_slots
,       slots_used
,       wg_name
,       tgt_mem_grant_MB
,       up1 as rc
,       (ROW_NUMBER() OVER(PARTITION BY DWU ORDER BY DWU)) as rc_id
FROM
(
    SELECT  DWU
    ,       max_queries
    ,       max_slots
    ,       slots_used
    ,       wg_name
    ,       tgt_mem_grant_MB
    ,       REVERSE(SUBSTRING(REVERSE(wg_names),1,CHARINDEX('_',REVERSE(wg_names),1)-1)) as up1
    ,       REVERSE(SUBSTRING(REVERSE(tgt_mem_grant_MBs),1,CHARINDEX('_',REVERSE(tgt_mem_grant_MBs),1)-1)) as up2
    ,       REVERSE(SUBSTRING(REVERSE(slots_used_all),1,CHARINDEX('_',REVERSE(slots_used_all),1)-1)) as up3
    FROM    ref AS r1
    UNPIVOT
    (
        wg_name FOR wg_names IN (wg_name_smallrc,wg_name_mediumrc,wg_name_largerc,wg_name_xlargerc,
        wg_name_staticrc10, wg_name_staticrc20, wg_name_staticrc30, wg_name_staticrc40, wg_name_staticrc50,
        wg_name_staticrc60, wg_name_staticrc70, wg_name_staticrc80)
    ) AS r2
    UNPIVOT
    (
        tgt_mem_grant_MB FOR tgt_mem_grant_MBs IN (tgt_mem_grant_MB_smallrc,tgt_mem_grant_MB_mediumrc,
        tgt_mem_grant_MB_largerc,tgt_mem_grant_MB_xlargerc, tgt_mem_grant_MB_staticrc10, tgt_mem_grant_MB_staticrc20,
        tgt_mem_grant_MB_staticrc30, tgt_mem_grant_MB_staticrc40, tgt_mem_grant_MB_staticrc50,
        tgt_mem_grant_MB_staticrc60, tgt_mem_grant_MB_staticrc70, tgt_mem_grant_MB_staticrc80)
    ) AS r3
    UNPIVOT
    (
        slots_used FOR slots_used_all IN (slots_used_smallrc,slots_used_mediumrc,slots_used_largerc,
        slots_used_xlargerc, slots_used_staticrc10, slots_used_staticrc20, slots_used_staticrc30,
        slots_used_staticrc40, slots_used_staticrc50, slots_used_staticrc60, slots_used_staticrc70,
        slots_used_staticrc80)
    ) AS r4
) a
WHERE   up1 = up2
AND     up1 = up3
;
-- Getting current info about workload groups.
WITH  
dmv  
AS  
(
  SELECT
          rp.name                                           AS rp_name
  ,       rp.max_memory_kb*1.0/1048576                      AS rp_max_mem_GB
  ,       (rp.max_memory_kb*1.0/1024)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_MB
  ,       (rp.max_memory_kb*1.0/1048576)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_GB
  ,       wg.name                                           AS wg_name
  ,       wg.importance                                     AS importance
  ,       wg.request_max_memory_grant_percent               AS request_max_memory_grant_percent
  FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
  JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    ON  wg.pdw_node_id  = rp.pdw_node_id
                                                                  AND wg.pool_id      = rp.pool_id
  WHERE   rp.name = 'SloDWPool'
  GROUP BY
          rp.name
  ,       rp.max_memory_kb
  ,       wg.name
  ,       wg.importance
  ,       wg.request_max_memory_grant_percent
)
-- Creating resource class name mapping.
,names
AS
(
  SELECT 'smallrc' as resource_class, 1 as rc_id
  UNION ALL
    SELECT 'mediumrc', 2
  UNION ALL
    SELECT 'largerc', 3
  UNION ALL
    SELECT 'xlargerc', 4
  UNION ALL
    SELECT 'staticrc10', 5
  UNION ALL
    SELECT 'staticrc20', 6
  UNION ALL
    SELECT 'staticrc30', 7
  UNION ALL
    SELECT 'staticrc40', 8
  UNION ALL
    SELECT 'staticrc50', 9
  UNION ALL
    SELECT 'staticrc60', 10
  UNION ALL
    SELECT 'staticrc70', 11
  UNION ALL
    SELECT 'staticrc80', 12
)
,base AS
(   SELECT  schema_name
    ,       table_name
    ,       SUM(column_count)                   AS column_count
    ,       ISNULL(SUM(short_string_column_count),0)   AS short_string_column_count
    ,       ISNULL(SUM(long_string_column_count),0)    AS long_string_column_count
    FROM    (   SELECT  sm.name                                             AS schema_name
                ,       tb.name                                             AS table_name
                ,       COUNT(co.column_id)                                 AS column_count
                           ,       CASE    WHEN co.system_type_id IN (36,43,106,108,165,167,173,175,231,239) 
                                AND  co.max_length <= 32 
                                THEN COUNT(co.column_id) 
                        END                                                 AS short_string_column_count
                ,       CASE    WHEN co.system_type_id IN (165,167,173,175,231,239) 
                                AND  co.max_length > 32 and co.max_length <=8000
                                THEN COUNT(co.column_id) 
                        END                                                 AS long_string_column_count
                FROM    sys.schemas AS sm
                JOIN    sys.tables  AS tb   on sm.[schema_id] = tb.[schema_id]
                JOIN    sys.columns AS co   ON tb.[object_id] = co.[object_id]
                           WHERE tb.name = @TABLE_NAME AND sm.name = @SCHEMA_NAME
                GROUP BY sm.name
                ,        tb.name
                ,        co.system_type_id
                ,        co.max_length            ) a
GROUP BY schema_name
,        table_name
)
, size AS
(
SELECT  schema_name
,       table_name
,       75497472                                            AS table_overhead

,       column_count*1048576*8                              AS column_size
,       short_string_column_count*1048576*32                       AS short_string_size,       (long_string_column_count*16777216) AS long_string_size
FROM    base
UNION
SELECT CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as schema_name
         ,CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as table_name
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as table_overhead
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as column_size
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as short_string_size

,CASE WHEN COUNT(*) = 0 THEN 0 END as long_string_size
FROM   base
)
, load_multiplier as 
(
SELECT  CASE 
                     WHEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) > 0 THEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) 
                     ELSE 1 
              END AS multipliplication_factor
) 
       SELECT  r1.DWU
       , schema_name
       , table_name
       , rc.resource_class as closest_rc_in_increasing_order
       , max_queries_at_this_rc = CASE
             WHEN (r1.max_slots / r1.slots_used > r1.max_queries)
                  THEN r1.max_queries
             ELSE r1.max_slots / r1.slots_used
                  END
       , r1.max_slots as max_concurrency_slots
       , r1.slots_used as required_slots_for_the_rc
       , r1.tgt_mem_grant_MB  as rc_mem_grant_MB
       , CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) AS est_mem_grant_required_for_cci_operation_MB       
       FROM    size, load_multiplier, #ref r1, names  rc
       WHERE r1.rc_id=rc.rc_id
                     AND CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) < r1.tgt_mem_grant_MB
       ORDER BY ABS(CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) - r1.tgt_mem_grant_MB)
GO
```

## <a name="query-importance"></a><span data-ttu-id="ed59c-757">Priorità delle query</span><span class="sxs-lookup"><span data-stu-id="ed59c-757">Query importance</span></span>
<span data-ttu-id="ed59c-758">SQL Data Warehouse implementa le classi di risorse utilizzando i gruppi del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ed59c-758">SQL Data Warehouse implements resource classes by using workload groups.</span></span> <span data-ttu-id="ed59c-759">Sono disponibili un totale di otto gruppi di carico di lavoro che controllano il comportamento di hello delle classi di risorse hello hello diverse dimensioni DWU.</span><span class="sxs-lookup"><span data-stu-id="ed59c-759">There are a total of eight workload groups that control hello behavior of hello resource classes across hello various DWU sizes.</span></span> <span data-ttu-id="ed59c-760">Per qualsiasi numero di DWU SQL Data Warehouse viene utilizzato solo quattro delle otto gruppi di carico di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="ed59c-760">For any DWU, SQL Data Warehouse uses only four of hello eight workload groups.</span></span> <span data-ttu-id="ed59c-761">Ciò è utile perché ogni gruppo di carico di lavoro viene assegnato tooone di quattro classi di risorse: smallrc mediumrc, largerc, o xlargerc.</span><span class="sxs-lookup"><span data-stu-id="ed59c-761">This makes sense because each workload group is assigned tooone of four resource classes: smallrc, mediumrc, largerc, or xlargerc.</span></span> <span data-ttu-id="ed59c-762">Hello importanza delle informazioni sui gruppi del carico di lavoro hello è che alcuni di questi gruppi di carico di lavoro siano impostate toohigher *importanza*.</span><span class="sxs-lookup"><span data-stu-id="ed59c-762">hello importance of understanding hello workload groups is that some of these workload groups are set toohigher *importance*.</span></span> <span data-ttu-id="ed59c-763">La priorità viene usata per la pianificazione della CPU.</span><span class="sxs-lookup"><span data-stu-id="ed59c-763">Importance is used for CPU scheduling.</span></span> <span data-ttu-id="ed59c-764">Le query eseguite con priorità alta otterranno tre volte più cicli della CPU rispetto a quelle con priorità media.</span><span class="sxs-lookup"><span data-stu-id="ed59c-764">Queries run with high importance will get three times more CPU cycles than those with medium importance.</span></span> <span data-ttu-id="ed59c-765">Di conseguenza, i mapping degli slot della concorrenza determinano anche la priorità della CPU.</span><span class="sxs-lookup"><span data-stu-id="ed59c-765">Therefore, concurrency slot mappings also determine CPU priority.</span></span> <span data-ttu-id="ed59c-766">Quando una query utilizza 16 o più slot, viene eseguita con priorità alta.</span><span class="sxs-lookup"><span data-stu-id="ed59c-766">When a query consumes 16 or more slots, it runs as high importance.</span></span>

<span data-ttu-id="ed59c-767">Hello nella tabella seguente sono illustrati i mapping di importanza hello per ogni gruppo di carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ed59c-767">hello following table shows hello importance mappings for each workload group.</span></span>

### <a name="workload-group-mappings-tooconcurrency-slots-and-importance"></a><span data-ttu-id="ed59c-768">Importanza e slot tooconcurrency mapping di gruppo del carico di lavoro</span><span class="sxs-lookup"><span data-stu-id="ed59c-768">Workload group mappings tooconcurrency slots and importance</span></span>
| <span data-ttu-id="ed59c-769">Gruppi di carichi di lavoro</span><span class="sxs-lookup"><span data-stu-id="ed59c-769">Workload groups</span></span> | <span data-ttu-id="ed59c-770">Mapping degli slot di concorrenza</span><span class="sxs-lookup"><span data-stu-id="ed59c-770">Concurrency slot mapping</span></span> | <span data-ttu-id="ed59c-771">MB/Distribuzione</span><span class="sxs-lookup"><span data-stu-id="ed59c-771">MB / Distribution</span></span> | <span data-ttu-id="ed59c-772">Mapping delle priorità</span><span class="sxs-lookup"><span data-stu-id="ed59c-772">Importance mapping</span></span> |
|:--- |:---:|:---:|:--- |
| <span data-ttu-id="ed59c-773">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="ed59c-773">SloDWGroupC00</span></span> |<span data-ttu-id="ed59c-774">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-774">1</span></span> |<span data-ttu-id="ed59c-775">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-775">100</span></span> |<span data-ttu-id="ed59c-776">Media</span><span class="sxs-lookup"><span data-stu-id="ed59c-776">Medium</span></span> |
| <span data-ttu-id="ed59c-777">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="ed59c-777">SloDWGroupC01</span></span> |<span data-ttu-id="ed59c-778">2</span><span class="sxs-lookup"><span data-stu-id="ed59c-778">2</span></span> |<span data-ttu-id="ed59c-779">200</span><span class="sxs-lookup"><span data-stu-id="ed59c-779">200</span></span> |<span data-ttu-id="ed59c-780">Media</span><span class="sxs-lookup"><span data-stu-id="ed59c-780">Medium</span></span> |
| <span data-ttu-id="ed59c-781">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="ed59c-781">SloDWGroupC02</span></span> |<span data-ttu-id="ed59c-782">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-782">4</span></span> |<span data-ttu-id="ed59c-783">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-783">400</span></span> |<span data-ttu-id="ed59c-784">Media</span><span class="sxs-lookup"><span data-stu-id="ed59c-784">Medium</span></span> |
| <span data-ttu-id="ed59c-785">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="ed59c-785">SloDWGroupC03</span></span> |<span data-ttu-id="ed59c-786">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-786">8</span></span> |<span data-ttu-id="ed59c-787">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-787">800</span></span> |<span data-ttu-id="ed59c-788">Media</span><span class="sxs-lookup"><span data-stu-id="ed59c-788">Medium</span></span> |
| <span data-ttu-id="ed59c-789">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="ed59c-789">SloDWGroupC04</span></span> |<span data-ttu-id="ed59c-790">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-790">16</span></span> |<span data-ttu-id="ed59c-791">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-791">1,600</span></span> |<span data-ttu-id="ed59c-792">Alto</span><span class="sxs-lookup"><span data-stu-id="ed59c-792">High</span></span> |
| <span data-ttu-id="ed59c-793">SloDWGroupC05</span><span class="sxs-lookup"><span data-stu-id="ed59c-793">SloDWGroupC05</span></span> |<span data-ttu-id="ed59c-794">32</span><span class="sxs-lookup"><span data-stu-id="ed59c-794">32</span></span> |<span data-ttu-id="ed59c-795">3.200</span><span class="sxs-lookup"><span data-stu-id="ed59c-795">3,200</span></span> |<span data-ttu-id="ed59c-796">Alto</span><span class="sxs-lookup"><span data-stu-id="ed59c-796">High</span></span> |
| <span data-ttu-id="ed59c-797">SloDWGroupC06</span><span class="sxs-lookup"><span data-stu-id="ed59c-797">SloDWGroupC06</span></span> |<span data-ttu-id="ed59c-798">64</span><span class="sxs-lookup"><span data-stu-id="ed59c-798">64</span></span> |<span data-ttu-id="ed59c-799">6.400</span><span class="sxs-lookup"><span data-stu-id="ed59c-799">6,400</span></span> |<span data-ttu-id="ed59c-800">Alto</span><span class="sxs-lookup"><span data-stu-id="ed59c-800">High</span></span> |
| <span data-ttu-id="ed59c-801">SloDWGroupC07</span><span class="sxs-lookup"><span data-stu-id="ed59c-801">SloDWGroupC07</span></span> |<span data-ttu-id="ed59c-802">128</span><span class="sxs-lookup"><span data-stu-id="ed59c-802">128</span></span> |<span data-ttu-id="ed59c-803">12.800</span><span class="sxs-lookup"><span data-stu-id="ed59c-803">12,800</span></span> |<span data-ttu-id="ed59c-804">Alto</span><span class="sxs-lookup"><span data-stu-id="ed59c-804">High</span></span> |

<span data-ttu-id="ed59c-805">Da hello **allocazione e utilizzo di slot concorrenza** grafico, è possibile verificare che un DW500 Usa 1, 4, 8 o slot di concorrenza 16 per smallrc, mediumrc, largerc e xlargerc, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="ed59c-805">From hello **Allocation and consumption of concurrency slots** chart, you can see that a DW500 uses 1, 4, 8 or 16 concurrency slots for smallrc, mediumrc, largerc, and xlargerc, respectively.</span></span> <span data-ttu-id="ed59c-806">È possibile cercare i valori in hello precede l'importanza di hello toofind grafico per ogni classe di risorse.</span><span class="sxs-lookup"><span data-stu-id="ed59c-806">You can look those values up in hello preceding chart toofind hello importance for each resource class.</span></span>

### <a name="dw500-mapping-of-resource-classes-tooimportance"></a><span data-ttu-id="ed59c-807">Mapping di DW500 di tooimportance classi di risorse</span><span class="sxs-lookup"><span data-stu-id="ed59c-807">DW500 mapping of resource classes tooimportance</span></span>
| <span data-ttu-id="ed59c-808">classe di risorse</span><span class="sxs-lookup"><span data-stu-id="ed59c-808">Resource class</span></span> | <span data-ttu-id="ed59c-809">Gruppo del carico di lavoro</span><span class="sxs-lookup"><span data-stu-id="ed59c-809">Workload group</span></span> | <span data-ttu-id="ed59c-810">Numero di slot di concorrenza usati</span><span class="sxs-lookup"><span data-stu-id="ed59c-810">Concurrency slots used</span></span> | <span data-ttu-id="ed59c-811">MB/Distribuzione</span><span class="sxs-lookup"><span data-stu-id="ed59c-811">MB / Distribution</span></span> | <span data-ttu-id="ed59c-812">priorità</span><span class="sxs-lookup"><span data-stu-id="ed59c-812">Importance</span></span> |
|:--- |:--- |:---:|:---:|:--- |
| <span data-ttu-id="ed59c-813">smallrc</span><span class="sxs-lookup"><span data-stu-id="ed59c-813">smallrc</span></span> |<span data-ttu-id="ed59c-814">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="ed59c-814">SloDWGroupC00</span></span> |<span data-ttu-id="ed59c-815">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-815">1</span></span> |<span data-ttu-id="ed59c-816">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-816">100</span></span> |<span data-ttu-id="ed59c-817">Media</span><span class="sxs-lookup"><span data-stu-id="ed59c-817">Medium</span></span> |
| <span data-ttu-id="ed59c-818">mediumrc</span><span class="sxs-lookup"><span data-stu-id="ed59c-818">mediumrc</span></span> |<span data-ttu-id="ed59c-819">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="ed59c-819">SloDWGroupC02</span></span> |<span data-ttu-id="ed59c-820">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-820">4</span></span> |<span data-ttu-id="ed59c-821">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-821">400</span></span> |<span data-ttu-id="ed59c-822">Media</span><span class="sxs-lookup"><span data-stu-id="ed59c-822">Medium</span></span> |
| <span data-ttu-id="ed59c-823">largerc</span><span class="sxs-lookup"><span data-stu-id="ed59c-823">largerc</span></span> |<span data-ttu-id="ed59c-824">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="ed59c-824">SloDWGroupC03</span></span> |<span data-ttu-id="ed59c-825">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-825">8</span></span> |<span data-ttu-id="ed59c-826">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-826">800</span></span> |<span data-ttu-id="ed59c-827">Media</span><span class="sxs-lookup"><span data-stu-id="ed59c-827">Medium</span></span> |
| <span data-ttu-id="ed59c-828">xlargerc</span><span class="sxs-lookup"><span data-stu-id="ed59c-828">xlargerc</span></span> |<span data-ttu-id="ed59c-829">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="ed59c-829">SloDWGroupC04</span></span> |<span data-ttu-id="ed59c-830">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-830">16</span></span> |<span data-ttu-id="ed59c-831">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-831">1,600</span></span> |<span data-ttu-id="ed59c-832">Alto</span><span class="sxs-lookup"><span data-stu-id="ed59c-832">High</span></span> |
| <span data-ttu-id="ed59c-833">staticrc10</span><span class="sxs-lookup"><span data-stu-id="ed59c-833">staticrc10</span></span> |<span data-ttu-id="ed59c-834">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="ed59c-834">SloDWGroupC00</span></span> |<span data-ttu-id="ed59c-835">1</span><span class="sxs-lookup"><span data-stu-id="ed59c-835">1</span></span> |<span data-ttu-id="ed59c-836">100</span><span class="sxs-lookup"><span data-stu-id="ed59c-836">100</span></span> |<span data-ttu-id="ed59c-837">Media</span><span class="sxs-lookup"><span data-stu-id="ed59c-837">Medium</span></span> |
| <span data-ttu-id="ed59c-838">staticrc20</span><span class="sxs-lookup"><span data-stu-id="ed59c-838">staticrc20</span></span> |<span data-ttu-id="ed59c-839">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="ed59c-839">SloDWGroupC01</span></span> |<span data-ttu-id="ed59c-840">2</span><span class="sxs-lookup"><span data-stu-id="ed59c-840">2</span></span> |<span data-ttu-id="ed59c-841">200</span><span class="sxs-lookup"><span data-stu-id="ed59c-841">200</span></span> |<span data-ttu-id="ed59c-842">Media</span><span class="sxs-lookup"><span data-stu-id="ed59c-842">Medium</span></span> |
| <span data-ttu-id="ed59c-843">staticrc30</span><span class="sxs-lookup"><span data-stu-id="ed59c-843">staticrc30</span></span> |<span data-ttu-id="ed59c-844">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="ed59c-844">SloDWGroupC02</span></span> |<span data-ttu-id="ed59c-845">4</span><span class="sxs-lookup"><span data-stu-id="ed59c-845">4</span></span> |<span data-ttu-id="ed59c-846">400</span><span class="sxs-lookup"><span data-stu-id="ed59c-846">400</span></span> |<span data-ttu-id="ed59c-847">Media</span><span class="sxs-lookup"><span data-stu-id="ed59c-847">Medium</span></span> |
| <span data-ttu-id="ed59c-848">staticrc40</span><span class="sxs-lookup"><span data-stu-id="ed59c-848">staticrc40</span></span> |<span data-ttu-id="ed59c-849">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="ed59c-849">SloDWGroupC03</span></span> |<span data-ttu-id="ed59c-850">8</span><span class="sxs-lookup"><span data-stu-id="ed59c-850">8</span></span> |<span data-ttu-id="ed59c-851">800</span><span class="sxs-lookup"><span data-stu-id="ed59c-851">800</span></span> |<span data-ttu-id="ed59c-852">Media</span><span class="sxs-lookup"><span data-stu-id="ed59c-852">Medium</span></span> |
| <span data-ttu-id="ed59c-853">staticrc50</span><span class="sxs-lookup"><span data-stu-id="ed59c-853">staticrc50</span></span> |<span data-ttu-id="ed59c-854">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="ed59c-854">SloDWGroupC03</span></span> |<span data-ttu-id="ed59c-855">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-855">16</span></span> |<span data-ttu-id="ed59c-856">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-856">1,600</span></span> |<span data-ttu-id="ed59c-857">Alto</span><span class="sxs-lookup"><span data-stu-id="ed59c-857">High</span></span> |
| <span data-ttu-id="ed59c-858">staticrc60</span><span class="sxs-lookup"><span data-stu-id="ed59c-858">staticrc60</span></span> |<span data-ttu-id="ed59c-859">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="ed59c-859">SloDWGroupC03</span></span> |<span data-ttu-id="ed59c-860">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-860">16</span></span> |<span data-ttu-id="ed59c-861">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-861">1,600</span></span> |<span data-ttu-id="ed59c-862">Alto</span><span class="sxs-lookup"><span data-stu-id="ed59c-862">High</span></span> |
| <span data-ttu-id="ed59c-863">staticrc70</span><span class="sxs-lookup"><span data-stu-id="ed59c-863">staticrc70</span></span> |<span data-ttu-id="ed59c-864">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="ed59c-864">SloDWGroupC03</span></span> |<span data-ttu-id="ed59c-865">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-865">16</span></span> |<span data-ttu-id="ed59c-866">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-866">1,600</span></span> |<span data-ttu-id="ed59c-867">Alto</span><span class="sxs-lookup"><span data-stu-id="ed59c-867">High</span></span> |
| <span data-ttu-id="ed59c-868">staticrc80</span><span class="sxs-lookup"><span data-stu-id="ed59c-868">staticrc80</span></span> |<span data-ttu-id="ed59c-869">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="ed59c-869">SloDWGroupC03</span></span> |<span data-ttu-id="ed59c-870">16</span><span class="sxs-lookup"><span data-stu-id="ed59c-870">16</span></span> |<span data-ttu-id="ed59c-871">1.600</span><span class="sxs-lookup"><span data-stu-id="ed59c-871">1,600</span></span> |<span data-ttu-id="ed59c-872">Alto</span><span class="sxs-lookup"><span data-stu-id="ed59c-872">High</span></span> |

<span data-ttu-id="ed59c-873">È possibile utilizzare hello seguenti toolook query DMV in differenze hello nell'allocazione di risorse di memoria in modo dettagliato da prospettiva hello di carichi hello o tooanalyze active e cronologici l'utilizzo di gruppi di carico di lavoro hello. risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="ed59c-873">You can use hello following DMV query toolook at hello differences in memory resource allocation in detail from hello perspective of hello resource governor, or tooanalyze active and historic usage of hello workload groups when troubleshooting.</span></span>

```sql
WITH rg
AS
(   SELECT  
     pn.name                        AS node_name
    ,pn.[type]                        AS node_type
    ,pn.pdw_node_id                    AS node_id
    ,rp.name                        AS pool_name
    ,rp.max_memory_kb*1.0/1024                AS pool_max_mem_MB
    ,wg.name                        AS group_name
    ,wg.importance                    AS group_importance
    ,wg.request_max_memory_grant_percent        AS group_request_max_memory_grant_pcnt
    ,wg.max_dop                        AS group_max_dop
    ,wg.effective_max_dop                AS group_effective_max_dop
    ,wg.total_request_count                AS group_total_request_count
    ,wg.total_queued_request_count            AS group_total_queued_request_count
    ,wg.active_request_count                AS group_active_request_count
    ,wg.queued_request_count                AS group_queued_request_count
    FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
    JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    
            ON  wg.pdw_node_id  = rp.pdw_node_id
            AND wg.pool_id      = rp.pool_id
    JOIN    sys.dm_pdw_nodes pn
            ON    wg.pdw_node_id    = pn.pdw_node_id
    WHERE   wg.name like 'SloDWGroup%'
        AND     rp.name = 'SloDWPool'
)
SELECT    pool_name
,        pool_max_mem_MB
,        group_name
,        group_importance
,        (pool_max_mem_MB/100)*group_request_max_memory_grant_pcnt AS max_memory_grant_MB
,        node_name
,        node_type
,       group_total_request_count
,       group_total_queued_request_count
,       group_active_request_count
,       group_queued_request_count
FROM    rg
ORDER BY
    node_name
,    group_request_max_memory_grant_pcnt
,    group_importance
;
```

## <a name="queries-that-honor-concurrency-limits"></a><span data-ttu-id="ed59c-874">Query che rispettano i limiti di concorrenza</span><span class="sxs-lookup"><span data-stu-id="ed59c-874">Queries that honor concurrency limits</span></span>
<span data-ttu-id="ed59c-875">La maggior parte delle query è regolata da classi di risorse.</span><span class="sxs-lookup"><span data-stu-id="ed59c-875">Most queries are governed by resource classes.</span></span> <span data-ttu-id="ed59c-876">Queste query devono adattarsi all'interno di query simultanee hello e le soglie dello slot di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="ed59c-876">These queries must fit inside both hello concurrent query and concurrency slot thresholds.</span></span> <span data-ttu-id="ed59c-877">L'utente non è possibile scegliere tooexclude una query dal modello di hello concorrenza slot.</span><span class="sxs-lookup"><span data-stu-id="ed59c-877">A user cannot choose tooexclude a query from hello concurrency slot model.</span></span>

<span data-ttu-id="ed59c-878">tooreiterate, hello istruzioni seguenti rispettano le classi di risorse:</span><span class="sxs-lookup"><span data-stu-id="ed59c-878">tooreiterate, hello following statements honor resource classes:</span></span>

* <span data-ttu-id="ed59c-879">INSERT SELECT</span><span class="sxs-lookup"><span data-stu-id="ed59c-879">INSERT-SELECT</span></span>
* <span data-ttu-id="ed59c-880">AGGIORNAMENTO</span><span class="sxs-lookup"><span data-stu-id="ed59c-880">UPDATE</span></span>
* <span data-ttu-id="ed59c-881">DELETE</span><span class="sxs-lookup"><span data-stu-id="ed59c-881">DELETE</span></span>
* <span data-ttu-id="ed59c-882">SELEZIONARE (quando si esegue una query sulle tabelle utente)</span><span class="sxs-lookup"><span data-stu-id="ed59c-882">SELECT (when querying user tables)</span></span>
* <span data-ttu-id="ed59c-883">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="ed59c-883">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="ed59c-884">ALTER INDEX REORGANIZE</span><span class="sxs-lookup"><span data-stu-id="ed59c-884">ALTER INDEX REORGANIZE</span></span>
* <span data-ttu-id="ed59c-885">MODIFICA TABELLA RICOMPILAZIONE</span><span class="sxs-lookup"><span data-stu-id="ed59c-885">ALTER TABLE REBUILD</span></span>
* <span data-ttu-id="ed59c-886">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="ed59c-886">CREATE INDEX</span></span>
* <span data-ttu-id="ed59c-887">CREARE L'INDICE COLUMNSTORE CLUSTER</span><span class="sxs-lookup"><span data-stu-id="ed59c-887">CREATE CLUSTERED COLUMNSTORE INDEX</span></span>
* <span data-ttu-id="ed59c-888">CREATE TABLE AS SELECT (CTAS)</span><span class="sxs-lookup"><span data-stu-id="ed59c-888">CREATE TABLE AS SELECT (CTAS)</span></span>
* <span data-ttu-id="ed59c-889">Caricamento dei dati</span><span class="sxs-lookup"><span data-stu-id="ed59c-889">Data loading</span></span>
* <span data-ttu-id="ed59c-890">Operazioni di spostamento dei dati eseguite dal servizio lo spostamento dei dati (DMS) hello</span><span class="sxs-lookup"><span data-stu-id="ed59c-890">Data movement operations conducted by hello Data Movement Service (DMS)</span></span>

## <a name="query-exceptions-tooconcurrency-limits"></a><span data-ttu-id="ed59c-891">Limiti tooconcurrency eccezioni di query</span><span class="sxs-lookup"><span data-stu-id="ed59c-891">Query exceptions tooconcurrency limits</span></span>
<span data-ttu-id="ed59c-892">Alcune query non rispettano risorse hello classe toowhich hello utente è assegnato.</span><span class="sxs-lookup"><span data-stu-id="ed59c-892">Some queries do not honor hello resource class toowhich hello user is assigned.</span></span> <span data-ttu-id="ed59c-893">Questi limiti di concorrenza toohello le eccezioni vengono effettuati quando le risorse di memoria hello necessari per un particolare comando sono ridotte, spesso perché il comando hello è un'operazione di metadati.</span><span class="sxs-lookup"><span data-stu-id="ed59c-893">These exceptions toohello concurrency limits are made when hello memory resources needed for a particular command are low, often because hello command is a metadata operation.</span></span> <span data-ttu-id="ed59c-894">obiettivo di Hello di queste eccezioni è tooavoid maggiori delle allocazioni di memoria per le query che non saranno mai necessario.</span><span class="sxs-lookup"><span data-stu-id="ed59c-894">hello goal of these exceptions is tooavoid larger memory allocations for queries that will never need them.</span></span> <span data-ttu-id="ed59c-895">In questi casi, classe di risorse ridotto (smallrc) viene sempre utilizzata indipendentemente dalla classe di risorsa effettiva hello predefinito di hello assegnato toohello utente.</span><span class="sxs-lookup"><span data-stu-id="ed59c-895">In these cases, hello default small resource class (smallrc) is always used regardless of hello actual resource class assigned toohello user.</span></span> <span data-ttu-id="ed59c-896">Ad esempio, in smallrc verrà sempre eseguita `CREATE LOGIN` .</span><span class="sxs-lookup"><span data-stu-id="ed59c-896">For example, `CREATE LOGIN` will always run in smallrc.</span></span> <span data-ttu-id="ed59c-897">Hello risorse richieste toofulfill questa operazione sono molto bassa, pertanto non rende la query di hello tooinclude senso nel modello di hello concorrenza slot.</span><span class="sxs-lookup"><span data-stu-id="ed59c-897">hello resources required toofulfill this operation are very low, so it does not make sense tooinclude hello query in hello concurrency slot model.</span></span>  <span data-ttu-id="ed59c-898">Queste query non dipendono anche dal limite di 32 hello utente concorrenza, un numero illimitato di tali query è possibile eseguire backup toohello limite di sessioni di 1.024 sessioni.</span><span class="sxs-lookup"><span data-stu-id="ed59c-898">These queries are also not limited by hello 32 user concurrency limit, an unlimited number of these queries can run up toohello session limit of 1,024 sessions.</span></span>

<span data-ttu-id="ed59c-899">Hello seguendo le istruzioni non rispetta le classi di risorse:</span><span class="sxs-lookup"><span data-stu-id="ed59c-899">hello following statements do not honor resource classes:</span></span>

* <span data-ttu-id="ed59c-900">CREATE o DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="ed59c-900">CREATE or DROP TABLE</span></span>
* <span data-ttu-id="ed59c-901">ALTER TABLE... SWITCH, SPLIT o MERGE PARTITION</span><span class="sxs-lookup"><span data-stu-id="ed59c-901">ALTER TABLE ... SWITCH, SPLIT, or MERGE PARTITION</span></span>
* <span data-ttu-id="ed59c-902">ALTER INDEX DISABLE</span><span class="sxs-lookup"><span data-stu-id="ed59c-902">ALTER INDEX DISABLE</span></span>
* <span data-ttu-id="ed59c-903">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="ed59c-903">DROP INDEX</span></span>
* <span data-ttu-id="ed59c-904">CREATE, UPDATE o DROP STATISTICS</span><span class="sxs-lookup"><span data-stu-id="ed59c-904">CREATE, UPDATE, or DROP STATISTICS</span></span>
* <span data-ttu-id="ed59c-905">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="ed59c-905">TRUNCATE TABLE</span></span>
* <span data-ttu-id="ed59c-906">ALTER AUTHORIZATION</span><span class="sxs-lookup"><span data-stu-id="ed59c-906">ALTER AUTHORIZATION</span></span>
* <span data-ttu-id="ed59c-907">CREATE LOGIN</span><span class="sxs-lookup"><span data-stu-id="ed59c-907">CREATE LOGIN</span></span>
* <span data-ttu-id="ed59c-908">CREATE, ALTER o DROP USER</span><span class="sxs-lookup"><span data-stu-id="ed59c-908">CREATE, ALTER or DROP USER</span></span>
* <span data-ttu-id="ed59c-909">CREATE, ALTER o DROP PROCEDURE</span><span class="sxs-lookup"><span data-stu-id="ed59c-909">CREATE, ALTER or DROP PROCEDURE</span></span>
* <span data-ttu-id="ed59c-910">CREATE o DROP VIEW</span><span class="sxs-lookup"><span data-stu-id="ed59c-910">CREATE or DROP VIEW</span></span>
* <span data-ttu-id="ed59c-911">INSERT VALUES</span><span class="sxs-lookup"><span data-stu-id="ed59c-911">INSERT VALUES</span></span>
* <span data-ttu-id="ed59c-912">SELECT da viste di sistema e DMV</span><span class="sxs-lookup"><span data-stu-id="ed59c-912">SELECT from system views and DMVs</span></span>
* <span data-ttu-id="ed59c-913">EXPLAIN</span><span class="sxs-lookup"><span data-stu-id="ed59c-913">EXPLAIN</span></span>
* <span data-ttu-id="ed59c-914">DBCC</span><span class="sxs-lookup"><span data-stu-id="ed59c-914">DBCC</span></span>

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <span data-ttu-id="ed59c-915"><a name="changing-user-resource-class-example"></a> Esempio di modifica della classe di risorse di un utente</span><span class="sxs-lookup"><span data-stu-id="ed59c-915"><a name="changing-user-resource-class-example"></a> Change a user resource class example</span></span>
1. <span data-ttu-id="ed59c-916">**Creare account di accesso:** aprire una connessione tooyour **master** database hello SQL server che ospita il database di SQL Data Warehouse ed eseguire i seguenti comandi hello.</span><span class="sxs-lookup"><span data-stu-id="ed59c-916">**Create login:** Open a connection tooyour **master** database on hello SQL server hosting your SQL Data Warehouse database and execute hello following commands.</span></span>
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > <span data-ttu-id="ed59c-917">È un toocreate buona un utente nel database master di hello per gli utenti di Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ed59c-917">It is a good idea toocreate a user in hello master database for Azure SQL Data Warehouse users.</span></span> <span data-ttu-id="ed59c-918">Creazione di un utente nel database master consente a un utente toologin usando strumenti come SQL Server Management Studio senza specificare un nome di database.</span><span class="sxs-lookup"><span data-stu-id="ed59c-918">Creating a user in master allows a user toologin using tools like SSMS without specifying a database name.</span></span>  <span data-ttu-id="ed59c-919">Inoltre, consente loro toouse hello oggetto explorer tooview tutti i database in SQL server.</span><span class="sxs-lookup"><span data-stu-id="ed59c-919">It also allows them toouse hello object explorer tooview all databases on a SQL server.</span></span>  <span data-ttu-id="ed59c-920">Per altre informazioni su creazione e gestione degli utenti, vedere [Proteggere un database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="ed59c-920">For more details about creating and managing users, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>
   > 
   > 
2. <span data-ttu-id="ed59c-921">**Creare l'utente di SQL Data Warehouse:** aprire una connessione toohello **SQL Data Warehouse** database ed eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="ed59c-921">**Create SQL Data Warehouse user:** Open a connection toohello **SQL Data Warehouse** database and execute hello following command.</span></span>
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. <span data-ttu-id="ed59c-922">**Concedere le autorizzazioni:** hello seguenti concessioni di esempio `CONTROL` su hello **SQL Data Warehouse** database.</span><span class="sxs-lookup"><span data-stu-id="ed59c-922">**Grant permissions:** hello following example grants `CONTROL` on hello **SQL Data Warehouse** database.</span></span> <span data-ttu-id="ed59c-923">`CONTROL`in hello livello di database è hello equivalente del ruolo db_owner in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ed59c-923">`CONTROL` at hello database level is hello equivalent of db_owner in SQL Server.</span></span>
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW toonewperson;
    ```
4. <span data-ttu-id="ed59c-924">**Aumentare la classe di risorse:** tooadd di query seguente hello di utilizzare un ruolo utente tooa maggiore carico di lavoro gestione.</span><span class="sxs-lookup"><span data-stu-id="ed59c-924">**Increase resource class:** Use hello following query tooadd a user tooa higher workload management role.</span></span>
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. <span data-ttu-id="ed59c-925">**Classe di risorse di diminuire:** tooremove di query seguente hello di usare un utente a un ruolo di gestione del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ed59c-925">**Decrease resource class:** Use hello following query tooremove a user from a workload management role.</span></span>
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="ed59c-926">Non è possibile tooremove smallrc di un utente.</span><span class="sxs-lookup"><span data-stu-id="ed59c-926">It is not possible tooremove a user from smallrc.</span></span>
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a><span data-ttu-id="ed59c-927">Rilevamento di query in coda e altre viste a gestione dinamica</span><span class="sxs-lookup"><span data-stu-id="ed59c-927">Queued query detection and other DMVs</span></span>
<span data-ttu-id="ed59c-928">È possibile utilizzare hello `sys.dm_pdw_exec_requests` query DMV tooidentify che sono in attesa in una coda di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="ed59c-928">You can use hello `sys.dm_pdw_exec_requests` DMV tooidentify queries that are waiting in a concurrency queue.</span></span> <span data-ttu-id="ed59c-929">Le query in attesa di uno slot di concorrenza saranno in stato **sospeso**.</span><span class="sxs-lookup"><span data-stu-id="ed59c-929">Queries waiting for a concurrency slot will have a status of **suspended**.</span></span>

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

<span data-ttu-id="ed59c-930">I ruoli di gestione del carico di lavoro possono essere visualizzati con `sys.database_principals`.</span><span class="sxs-lookup"><span data-stu-id="ed59c-930">Workload management roles can be viewed with `sys.database_principals`.</span></span>

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

<span data-ttu-id="ed59c-931">Hello query seguente viene illustrato il ruolo di cui ogni utente è assegnato.</span><span class="sxs-lookup"><span data-stu-id="ed59c-931">hello following query shows which role each user is assigned to.</span></span>

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

<span data-ttu-id="ed59c-932">SQL Data Warehouse è hello seguenti tipi di attesa:</span><span class="sxs-lookup"><span data-stu-id="ed59c-932">SQL Data Warehouse has hello following wait types:</span></span>

* <span data-ttu-id="ed59c-933">**LocalQueriesConcurrencyResourceType**: le query che si trovano di fuori di framework di hello concorrenza slot.</span><span class="sxs-lookup"><span data-stu-id="ed59c-933">**LocalQueriesConcurrencyResourceType**: Queries that sit outside of hello concurrency slot framework.</span></span> <span data-ttu-id="ed59c-934">Le query DMV e le funzioni di sistema  come `SELECT @@VERSION` sono esempi di query locali.</span><span class="sxs-lookup"><span data-stu-id="ed59c-934">DMV queries and system functions such as `SELECT @@VERSION` are examples of local queries.</span></span>
* <span data-ttu-id="ed59c-935">**UserConcurrencyResourceType**: le query che si trovano all'interno di hello concorrenza slot framework.</span><span class="sxs-lookup"><span data-stu-id="ed59c-935">**UserConcurrencyResourceType**: Queries that sit inside hello concurrency slot framework.</span></span> <span data-ttu-id="ed59c-936">Le query sulle tabelle dell'utente finale rappresentano esempi in cui si usa questo tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="ed59c-936">Queries against end-user tables represent examples that would use this resource type.</span></span>
* <span data-ttu-id="ed59c-937">**DmsConcurrencyResourceType**: attese risultanti dalle operazioni di spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="ed59c-937">**DmsConcurrencyResourceType**: Waits resulting from data movement operations.</span></span>
* <span data-ttu-id="ed59c-938">**BackupConcurrencyResourceType**: indica che è in esecuzione il backup di un database.</span><span class="sxs-lookup"><span data-stu-id="ed59c-938">**BackupConcurrencyResourceType**: This wait indicates that a database is being backed up.</span></span> <span data-ttu-id="ed59c-939">valore massimo di Hello per questo tipo di risorsa è 1.</span><span class="sxs-lookup"><span data-stu-id="ed59c-939">hello maximum value for this resource type is 1.</span></span> <span data-ttu-id="ed59c-940">Se più copie di backup sono stati richiesti in hello contemporaneamente, hello ad altri utenti verranno inseriti nella coda.</span><span class="sxs-lookup"><span data-stu-id="ed59c-940">If multiple backups have been requested at hello same time, hello others will queue.</span></span>

<span data-ttu-id="ed59c-941">Hello `sys.dm_pdw_waits` DMV può essere utilizzato toosee quali risorse di una richiesta è in attesa di.</span><span class="sxs-lookup"><span data-stu-id="ed59c-941">hello `sys.dm_pdw_waits` DMV can be used toosee which resources a request is waiting for.</span></span>

```sql
SELECT  w.[wait_id]
,       w.[session_id]
,       w.[type]            AS Wait_type
,       w.[object_type]
,       w.[object_name]
,       w.[request_id]
,       w.[request_time]
,       w.[acquire_time]
,       w.[state]
,       w.[priority]
,    SESSION_ID()            AS Current_session
,    s.[status]            AS Session_status
,    s.[login_name]
,    s.[query_count]
,    s.[client_id]
,    s.[sql_spid]
,    r.[command]            AS Request_command
,    r.[label]
,    r.[status]            AS Request_status
,    r.[submit_time]
,    r.[start_time]
,    r.[end_compile_time]
,    r.[end_time]
,    DATEDIFF(ms,r.[submit_time],r.[start_time])        AS Request_queue_time_ms
,    DATEDIFF(ms,r.[start_time],r.[end_compile_time])    AS Request_compile_time_ms
,    DATEDIFF(ms,r.[end_compile_time],r.[end_time])        AS Request_execution_time_ms
,    r.[total_elapsed_time]
FROM    sys.dm_pdw_waits w
JOIN    sys.dm_pdw_exec_sessions s  ON w.[session_id] = s.[session_id]
JOIN    sys.dm_pdw_exec_requests r  ON w.[request_id] = r.[request_id]
WHERE    w.[session_id] <> SESSION_ID();
```

<span data-ttu-id="ed59c-942">Hello `sys.dm_pdw_resource_waits` DMV Mostra solo le attese risorse hello utilizzate da una determinata query.</span><span class="sxs-lookup"><span data-stu-id="ed59c-942">hello `sys.dm_pdw_resource_waits` DMV shows only hello resource waits consumed by a given query.</span></span> <span data-ttu-id="ed59c-943">Tempo di attesa di risorse solo misura il tempo di hello in attesa di risorse toobe fornito, come toosignal anziché di attesa, ovvero hello tempo impiegato per hello sottostante una query SQL Server tooschedule hello nella CPU hello.</span><span class="sxs-lookup"><span data-stu-id="ed59c-943">Resource wait time only measures hello time waiting for resources toobe provided, as opposed toosignal wait time, which is hello time it takes for hello underlying SQL servers tooschedule hello query onto hello CPU.</span></span>

```sql
SELECT  [session_id]
,       [type]
,       [object_type]
,       [object_name]
,       [request_id]
,       [request_time]
,       [acquire_time]
,       DATEDIFF(ms,[request_time],[acquire_time])  AS acquire_duration_ms
,       [concurrency_slots_used]                    AS concurrency_slots_reserved
,       [resource_class]
,       [wait_id]                                   AS queue_position
FROM    sys.dm_pdw_resource_waits
WHERE    [session_id] <> SESSION_ID();
```

<span data-ttu-id="ed59c-944">Hello `sys.dm_pdw_wait_stats` può essere utilizzata per l'analisi delle tendenze cronologiche di attese.</span><span class="sxs-lookup"><span data-stu-id="ed59c-944">hello `sys.dm_pdw_wait_stats` DMV can be used for historic trend analysis of waits.</span></span>

```sql
SELECT    w.[pdw_node_id]
,        w.[wait_name]
,        w.[max_wait_time]
,        w.[request_count]
,        w.[signal_time]
,        w.[completed_count]
,        w.[wait_time]
FROM    sys.dm_pdw_wait_stats w;
```

## <a name="next-steps"></a><span data-ttu-id="ed59c-945">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ed59c-945">Next steps</span></span>
<span data-ttu-id="ed59c-946">Per altre informazioni sulla gestione degli utenti e della sicurezza del database, vedere [Proteggere un database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="ed59c-946">For more information about managing database users and security, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span> <span data-ttu-id="ed59c-947">Per ulteriori informazioni sulle classi di risorse come dimensioni maggiori possono migliorare la qualità di indice columnstore cluster, vedere [la ricompilazione di indici tooimprove segmento di qualità].</span><span class="sxs-lookup"><span data-stu-id="ed59c-947">For more information about how larger resource classes can improve clustered columnstore index quality, see [Rebuilding indexes tooimprove segment quality].</span></span>

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[la ricompilazione di indici tooimprove segmento di qualità]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->
