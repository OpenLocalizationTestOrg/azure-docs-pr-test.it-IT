---
title: Gestione della concorrenza e del carico di lavoro in SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: eaf2d43286dbaa52ada1430fbb7ce1e37f41c0d4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a><span data-ttu-id="dcdd9-103">Gestione della concorrenza e del carico di lavoro in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="dcdd9-103">Concurrency and workload management in SQL Data Warehouse</span></span>
<span data-ttu-id="dcdd9-104">Per fornire prestazioni stimabili e scalabili, Microsoft Azure SQL Data Warehouse consente di controllare i livelli di concorrenza e le allocazioni di risorse, come la memoria e la classificazione in ordine di priorità della CPU.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-104">To deliver predictable performance at scale, Microsoft Azure SQL Data Warehouse helps you control concurrency levels and resource allocations like memory and CPU prioritization.</span></span> <span data-ttu-id="dcdd9-105">Questo articolo introduce i concetti di gestione della concorrenza e del carico di lavoro, spiegando in che modo entrambe le funzionalità sono state implementate e come vengono controllate nel data warehouse.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-105">This article introduces you to the concepts of concurrency and workload management, explaining how both features have been implemented and how you can control them in your data warehouse.</span></span> <span data-ttu-id="dcdd9-106">La gestione del carico di lavoro di SQL Data Warehouse è concepita per facilitare il supporto di ambienti multiutente.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-106">SQL Data Warehouse workload management is intended to help you support multi-user environments.</span></span> <span data-ttu-id="dcdd9-107">Non è concepita per i carichi di lavoro multi-tenant.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-107">It is not intended for multi-tenant workloads.</span></span>

## <a name="concurrency-limits"></a><span data-ttu-id="dcdd9-108">Limiti di concorrenza</span><span class="sxs-lookup"><span data-stu-id="dcdd9-108">Concurrency limits</span></span>
<span data-ttu-id="dcdd9-109">SQL Data Warehouse consente un massimo di 1.024 connessioni simultanee.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-109">SQL Data Warehouse allows up to 1,024 concurrent connections.</span></span> <span data-ttu-id="dcdd9-110">Tutte le 1.024 connessioni possono inviare query contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-110">All 1,024 connections can submit queries concurrently.</span></span> <span data-ttu-id="dcdd9-111">Tuttavia, per ottimizzare la velocità effettiva, SQL Data Warehouse può accodare alcune query per garantire che a ognuna venga assegnata una concessione di memoria minima.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-111">However, to optimize throughput, SQL Data Warehouse may queue some queries to ensure that each query receives a minimal memory grant.</span></span> <span data-ttu-id="dcdd9-112">L'accodamento avviene in fase di esecuzione della query.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-112">Queuing occurs at query execution time.</span></span> <span data-ttu-id="dcdd9-113">Accodando le query quando vengono raggiunti i limiti di concorrenza, SQL Data Warehouse è in grado di aumentare la velocità effettiva totale, assicurando che le query attive ottengano l'accesso alle risorse di memoria critiche necessarie.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-113">By queuing queries when concurrency limits are reached, SQL Data Warehouse can increase total throughput by ensuring that active queries get access to critically needed memory resources.</span></span>  

<span data-ttu-id="dcdd9-114">I limiti di concorrenza sono regolati da due concetti, *query simultanee* e *slot di concorrenza*.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-114">Concurrency limits are governed by two concepts: *concurrent queries* and *concurrency slots*.</span></span> <span data-ttu-id="dcdd9-115">Perché una query venga eseguita, è necessario che rientri nel limite di concorrenza delle query e nell'allocazione di slot di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-115">For a query to execute, it must execute within both the query concurrency limit and the concurrency slot allocation.</span></span>

* <span data-ttu-id="dcdd9-116">Le query simultanee sono le query in esecuzione contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-116">Concurrent queries are the queries executing at the same time.</span></span> <span data-ttu-id="dcdd9-117">SQL Data Warehouse supporta fino a 32 query simultanee nelle DWU di dimensioni maggiori.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-117">SQL Data Warehouse supports up to 32 concurrent queries on the larger DWU sizes.</span></span>
* <span data-ttu-id="dcdd9-118">In base alle Unità Data Warehouse (DWU), vengono allocati slot di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-118">Concurrency slots are allocated based on DWU.</span></span> <span data-ttu-id="dcdd9-119">Ogni 100 DWU, vengono forniti 4 slot di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-119">Each 100 DWU provides 4 concurrency slots.</span></span> <span data-ttu-id="dcdd9-120">Ad esempio, per DW100 vengono allocati 4 slot di concorrenza e per DW1000 ne vengono allocati 40.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-120">For example, a DW100 allocates 4 concurrency slots and DW1000 allocates 40.</span></span> <span data-ttu-id="dcdd9-121">Ogni query utilizza uno o più slot di concorrenza, a seconda della [classe di risorse](#resource-classes) della query.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-121">Each query consumes one or more concurrency slots, dependent on the [resource class](#resource-classes) of the query.</span></span> <span data-ttu-id="dcdd9-122">Le query in esecuzione nella classe di risorse smallrc utilizzano uno slot di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-122">Queries running in the smallrc resource class consume one concurrency slot.</span></span> <span data-ttu-id="dcdd9-123">Le query in esecuzione in una classe di risorse superiore usano più slot di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-123">Queries running in a higher resource class consume more concurrency slots.</span></span>

<span data-ttu-id="dcdd9-124">La tabella seguente descrive i limiti sia per le query simultanee che per gli slot di concorrenza a seconda delle dimensioni della DWU.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-124">The following table describes the limits for both concurrent queries and concurrency slots at the various DWU sizes.</span></span>

### <a name="concurrency-limits"></a><span data-ttu-id="dcdd9-125">Limiti di concorrenza</span><span class="sxs-lookup"><span data-stu-id="dcdd9-125">Concurrency limits</span></span>
| <span data-ttu-id="dcdd9-126">DWU</span><span class="sxs-lookup"><span data-stu-id="dcdd9-126">DWU</span></span> | <span data-ttu-id="dcdd9-127">Numero massimo di query simultanee</span><span class="sxs-lookup"><span data-stu-id="dcdd9-127">Max concurrent queries</span></span> | <span data-ttu-id="dcdd9-128">Numero di slot di concorrenza allocati</span><span class="sxs-lookup"><span data-stu-id="dcdd9-128">Concurrency slots allocated</span></span> |
|:--- |:---:|:---:|
| <span data-ttu-id="dcdd9-129">DW100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-129">DW100</span></span> |<span data-ttu-id="dcdd9-130">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-130">4</span></span> |<span data-ttu-id="dcdd9-131">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-131">4</span></span> |
| <span data-ttu-id="dcdd9-132">DW200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-132">DW200</span></span> |<span data-ttu-id="dcdd9-133">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-133">8</span></span> |<span data-ttu-id="dcdd9-134">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-134">8</span></span> |
| <span data-ttu-id="dcdd9-135">DW300</span><span class="sxs-lookup"><span data-stu-id="dcdd9-135">DW300</span></span> |<span data-ttu-id="dcdd9-136">12</span><span class="sxs-lookup"><span data-stu-id="dcdd9-136">12</span></span> |<span data-ttu-id="dcdd9-137">12</span><span class="sxs-lookup"><span data-stu-id="dcdd9-137">12</span></span> |
| <span data-ttu-id="dcdd9-138">DW400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-138">DW400</span></span> |<span data-ttu-id="dcdd9-139">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-139">16</span></span> |<span data-ttu-id="dcdd9-140">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-140">16</span></span> |
| <span data-ttu-id="dcdd9-141">DW500</span><span class="sxs-lookup"><span data-stu-id="dcdd9-141">DW500</span></span> |<span data-ttu-id="dcdd9-142">20</span><span class="sxs-lookup"><span data-stu-id="dcdd9-142">20</span></span> |<span data-ttu-id="dcdd9-143">20</span><span class="sxs-lookup"><span data-stu-id="dcdd9-143">20</span></span> |
| <span data-ttu-id="dcdd9-144">DW600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-144">DW600</span></span> |<span data-ttu-id="dcdd9-145">24</span><span class="sxs-lookup"><span data-stu-id="dcdd9-145">24</span></span> |<span data-ttu-id="dcdd9-146">24</span><span class="sxs-lookup"><span data-stu-id="dcdd9-146">24</span></span> |
| <span data-ttu-id="dcdd9-147">DW1000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-147">DW1000</span></span> |<span data-ttu-id="dcdd9-148">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-148">32</span></span> |<span data-ttu-id="dcdd9-149">40</span><span class="sxs-lookup"><span data-stu-id="dcdd9-149">40</span></span> |
| <span data-ttu-id="dcdd9-150">DW1200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-150">DW1200</span></span> |<span data-ttu-id="dcdd9-151">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-151">32</span></span> |<span data-ttu-id="dcdd9-152">48</span><span class="sxs-lookup"><span data-stu-id="dcdd9-152">48</span></span> |
| <span data-ttu-id="dcdd9-153">DW1500</span><span class="sxs-lookup"><span data-stu-id="dcdd9-153">DW1500</span></span> |<span data-ttu-id="dcdd9-154">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-154">32</span></span> |<span data-ttu-id="dcdd9-155">60</span><span class="sxs-lookup"><span data-stu-id="dcdd9-155">60</span></span> |
| <span data-ttu-id="dcdd9-156">DW2000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-156">DW2000</span></span> |<span data-ttu-id="dcdd9-157">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-157">32</span></span> |<span data-ttu-id="dcdd9-158">80</span><span class="sxs-lookup"><span data-stu-id="dcdd9-158">80</span></span> |
| <span data-ttu-id="dcdd9-159">DW3000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-159">DW3000</span></span> |<span data-ttu-id="dcdd9-160">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-160">32</span></span> |<span data-ttu-id="dcdd9-161">120</span><span class="sxs-lookup"><span data-stu-id="dcdd9-161">120</span></span> |
| <span data-ttu-id="dcdd9-162">DW6000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-162">DW6000</span></span> |<span data-ttu-id="dcdd9-163">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-163">32</span></span> |<span data-ttu-id="dcdd9-164">240</span><span class="sxs-lookup"><span data-stu-id="dcdd9-164">240</span></span> |

<span data-ttu-id="dcdd9-165">Quando viene raggiunta una di queste soglie, le nuove query vengono accodate e vengono eseguite in base al principio FIFO (First-In-First-Out).</span><span class="sxs-lookup"><span data-stu-id="dcdd9-165">When one of these thresholds is met, new queries are queued and executed on a first-in, first-out basis.</span></span>  <span data-ttu-id="dcdd9-166">Al termine dell'esecuzione delle query e quando il numero di query e di slot risulta inferiore ai limiti, le code accodate vengono rilasciate.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-166">As a queries finishes and the number of queries and slots falls below the limits, queued queries are released.</span></span> 

> [!NOTE]  
> <span data-ttu-id="dcdd9-167">*selezione* eseguite esclusivamente sulle viste del catalogo o sulle viste a gestione dinamica (DMV) non sono disciplinate da nessuno dei limiti di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-167">*Select* queries executing exclusively on dynamic management views (DMVs) or catalog views are not governed by any of the concurrency limits.</span></span> <span data-ttu-id="dcdd9-168">È possibile monitorare il sistema indipendentemente dal numero di query in esecuzione nel sistema.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-168">You can monitor the system regardless of the number of queries executing on it.</span></span>
> 
> 

## <a name="resource-classes"></a><span data-ttu-id="dcdd9-169">Classi di risorse</span><span class="sxs-lookup"><span data-stu-id="dcdd9-169">Resource classes</span></span>
<span data-ttu-id="dcdd9-170">Attraverso le classi di risorse è possibile controllare l'allocazione di memoria e cicli di CPU assegnati a una query.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-170">Resource classes help you control memory allocation and CPU cycles given to a query.</span></span> <span data-ttu-id="dcdd9-171">È possibile assegnare due tipi di classi di risorse a un utente sotto forma di ruoli del database.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-171">You can assign two types of resource classes to a user in the form of database roles.</span></span> <span data-ttu-id="dcdd9-172">I due tipi di classi di risorse sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="dcdd9-172">The two types of resource classes are as follows:</span></span>
1. <span data-ttu-id="dcdd9-173">Classi di risorse dinamiche (**smallrc, mediumrc, largerc, xlargerc**), che allocano una quantità variabile di memoria a seconda della DWU corrente.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-173">Dynamic Resource Classes (**smallrc, mediumrc, largerc, xlargerc**) allocate a variable amount of memory depending on the current DWU.</span></span> <span data-ttu-id="dcdd9-174">Ciò significa che quando si passa a una DWU più grande, le query ottengono automaticamente più memoria.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-174">This means that when you scale up to a larger DWU, your queries automatically get more memory.</span></span> 
2. <span data-ttu-id="dcdd9-175">Classi di risorse statiche (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**), che allocano la stessa quantità di memoria indipendentemente dalla DWU corrente (a condizione che la DWU stessa abbia memoria sufficiente).</span><span class="sxs-lookup"><span data-stu-id="dcdd9-175">Static Resource Classes (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) allocate the same amount of memory regardless of the current DWU (provided that the DWU itself has enough memory).</span></span> <span data-ttu-id="dcdd9-176">Ciò significa che nelle DWU più grandi è possibile eseguire più query in ogni classe di risorse contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-176">This means that on larger DWUs, you can run more queries in each resource class concurrently.</span></span>

<span data-ttu-id="dcdd9-177">Agli utenti delle classi **smallrc** e **staticrc10** viene assegnata una quantità di memoria più piccola e ciò permette di sfruttare una concorrenza maggiore.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-177">Users in **smallrc** and **staticrc10** are given a smaller amount of memory and can take advantage of higher concurrency.</span></span> <span data-ttu-id="dcdd9-178">Al contrario, agli utenti delle classi **xlargerc** e **staticrc80** vengono assegnate grandi quantità di memoria e quindi è possibile eseguire contemporaneamente un numero minore di query.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-178">In contrast, users assigned to **xlargerc** or **staticrc80** are given large amounts of memory, and therefore fewer of their queries can run concurrently.</span></span>

<span data-ttu-id="dcdd9-179">Per impostazione predefinita, ogni utente è membro della classe di risorse piccola **smallrc**.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-179">By default, each user is a member of the small resource class, **smallrc**.</span></span> <span data-ttu-id="dcdd9-180">Per aumentare la classe di risorse viene usata la procedura `sp_addrolemember`, mentre per diminuirla viene usata la procedura `sp_droprolemember`.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-180">The procedure `sp_addrolemember` is used to increase the resource class, and `sp_droprolemember` is used to decrease the resource class.</span></span> <span data-ttu-id="dcdd9-181">Questo comando, ad esempio, assegna a loaduser una classe di risorse superiore, **largerc**:</span><span class="sxs-lookup"><span data-stu-id="dcdd9-181">For example, this command would increase the resource class of loaduser to **largerc**:</span></span>

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a><span data-ttu-id="dcdd9-182">Query che non rispettano le classi di risorse</span><span class="sxs-lookup"><span data-stu-id="dcdd9-182">Queries that do not honor resource classes</span></span>

<span data-ttu-id="dcdd9-183">Esistono alcuni tipi di query che non traggono vantaggio da un'allocazione di memoria maggiore.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-183">There are a few types of queries that do not benefit from a larger memory allocation.</span></span> <span data-ttu-id="dcdd9-184">Il sistema ignora l'allocazione della classe di risorse ed esegue sempre queste query nella classe di risorse piccola.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-184">The system ignores their resource class allocation and always run these queries in the small resource class instead.</span></span> <span data-ttu-id="dcdd9-185">Se queste query vengono eseguite sempre nella classe di risorse piccola, è possibile eseguirle quando gli slot di concorrenza sono sotto pressione, per non consumare più slot del necessario.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-185">If these queries always run in the small resource class, they can run when concurrency slots are under pressure and they won't consume more slots than needed.</span></span> <span data-ttu-id="dcdd9-186">Vedere [Eccezioni della classe di risorse](#query-exceptions-to-concurrency-limits) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-186">See [Resource class exceptions](#query-exceptions-to-concurrency-limits) for more information.</span></span>

## <a name="details-on-resource-class-assignment"></a><span data-ttu-id="dcdd9-187">Dettagli sull'assegnazione della classe di risorse</span><span class="sxs-lookup"><span data-stu-id="dcdd9-187">Details on resource class assignment</span></span>


<span data-ttu-id="dcdd9-188">Altri dettagli sulla classe di risorse:</span><span class="sxs-lookup"><span data-stu-id="dcdd9-188">A few more details on resource class:</span></span>

* <span data-ttu-id="dcdd9-189">*Ruolo Alter* è obbligatoria per modificare la classe di risorse di un utente.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-189">*Alter role* permission is required to change the resource class of a user.</span></span>
* <span data-ttu-id="dcdd9-190">Anche se è possibile aggiungere un utente a una o più classi di risorse superiori, le classi di risorse dinamiche hanno la precedenza su quelle statiche.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-190">Although you can add a user to one or more of the higher resource classes, dynamic resource classes take precedence over static resource classes.</span></span> <span data-ttu-id="dcdd9-191">Ciò significa che se un utente viene assegnato a entrambe le classi **mediumrc**(dinamica) e **staticrc80**(statica), la precedenza va a **mediumrc**.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-191">That is, if a user is assigned to both **mediumrc**(dynamic) and **staticrc80**(static), **mediumrc** is the resource class that is honored.</span></span>
 * <span data-ttu-id="dcdd9-192">Quando un utente è assegnato a più di una classe di risorse in un tipo di classe di risorse specifico (più classi di risorse dinamiche o più classi di risorse statiche), la precedenza va alla classe di risorse superiore.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-192">When a user is assigned to more than one resource class in a specific resource class type (more than one dynamic resource class or more than one static resource class), the highest resource class is honored.</span></span> <span data-ttu-id="dcdd9-193">Ciò significa che se un utente viene assegnato a entrambe le classi mediumrc e largerc, la precedenza va alla classe di risorse superiore (largerc).</span><span class="sxs-lookup"><span data-stu-id="dcdd9-193">That is, if a user is assigned to both mediumrc and largerc, the higher resource class (largerc) is honored.</span></span> <span data-ttu-id="dcdd9-194">Se un utente viene assegnato a entrambe le classi **staticrc20** e **statirc80**, la precedenza va a **staticrc80**.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-194">And if a user is assigned to both **staticrc20** and **statirc80**, **staticrc80** is honored.</span></span>
* <span data-ttu-id="dcdd9-195">La classe di risorse dell'utente amministratore di sistema non può essere modificata.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-195">The resource class of the system administrative user cannot be changed.</span></span>

<span data-ttu-id="dcdd9-196">Per un esempio dettagliato, vedere [Esempio di modifica della classe di risorse di un utente](#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="dcdd9-196">For a detailed example, see [Changing user resource class example](#changing-user-resource-class-example).</span></span>

## <a name="memory-allocation"></a><span data-ttu-id="dcdd9-197">Allocazione della memoria</span><span class="sxs-lookup"><span data-stu-id="dcdd9-197">Memory allocation</span></span>
<span data-ttu-id="dcdd9-198">Esistono vantaggi e svantaggi legati all'incremento della classe di risorse dell'utente.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-198">There are pros and cons to increasing a user's resource class.</span></span> <span data-ttu-id="dcdd9-199">Spostando un utente a una classe di risorse superiore, si consente alle rispettive query di accedere a una quantità maggiore di memoria e quindi l'esecuzione delle query è più rapida.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-199">Increasing a resource class for a user, gives their queries access to more memory, which may mean queries execute faster.</span></span>  <span data-ttu-id="dcdd9-200">Una quantità maggiore di classi di risorse, tuttavia, riduce anche il numero di query simultanee che è possibile eseguire.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-200">However, higher resource classes also reduce the number of concurrent queries that can run.</span></span> <span data-ttu-id="dcdd9-201">Questo è il compromesso tra il fatto di allocare grandi quantità di memoria a una singola query o consentire l'esecuzione simultanea di altre query che necessitano di allocazioni di memoria.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-201">This is the trade-off between allocating large amounts of memory to a single query or allowing other queries, which also need memory allocations, to run concurrently.</span></span> <span data-ttu-id="dcdd9-202">Se a un utente vengono allocate grandi quantità di memoria per una query, gli altri utenti non potranno accedere alla stessa memoria per eseguire una query.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-202">If one user is given high allocations of memory for a query, other users will not have access to that same memory to run a query.</span></span>

<span data-ttu-id="dcdd9-203">Nella tabella seguente la memoria allocata è associata a ogni distribuzione per classe DWU e classe di risorse.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-203">The following table maps the memory allocated to each distribution by DWU and resource class.</span></span>

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a><span data-ttu-id="dcdd9-204">Allocazioni di memoria per ogni distribuzione per le classi di risorse dinamiche (MB)</span><span class="sxs-lookup"><span data-stu-id="dcdd9-204">Memory allocations per distribution for dynamic resource classes (MB)</span></span>
| <span data-ttu-id="dcdd9-205">DWU</span><span class="sxs-lookup"><span data-stu-id="dcdd9-205">DWU</span></span> | <span data-ttu-id="dcdd9-206">smallrc</span><span class="sxs-lookup"><span data-stu-id="dcdd9-206">smallrc</span></span> | <span data-ttu-id="dcdd9-207">mediumrc</span><span class="sxs-lookup"><span data-stu-id="dcdd9-207">mediumrc</span></span> | <span data-ttu-id="dcdd9-208">largerc</span><span class="sxs-lookup"><span data-stu-id="dcdd9-208">largerc</span></span> | <span data-ttu-id="dcdd9-209">xlargerc</span><span class="sxs-lookup"><span data-stu-id="dcdd9-209">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="dcdd9-210">DW100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-210">DW100</span></span> |<span data-ttu-id="dcdd9-211">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-211">100</span></span> |<span data-ttu-id="dcdd9-212">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-212">100</span></span> |<span data-ttu-id="dcdd9-213">200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-213">200</span></span> |<span data-ttu-id="dcdd9-214">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-214">400</span></span> |
| <span data-ttu-id="dcdd9-215">DW200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-215">DW200</span></span> |<span data-ttu-id="dcdd9-216">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-216">100</span></span> |<span data-ttu-id="dcdd9-217">200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-217">200</span></span> |<span data-ttu-id="dcdd9-218">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-218">400</span></span> |<span data-ttu-id="dcdd9-219">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-219">800</span></span> |
| <span data-ttu-id="dcdd9-220">DW300</span><span class="sxs-lookup"><span data-stu-id="dcdd9-220">DW300</span></span> |<span data-ttu-id="dcdd9-221">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-221">100</span></span> |<span data-ttu-id="dcdd9-222">200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-222">200</span></span> |<span data-ttu-id="dcdd9-223">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-223">400</span></span> |<span data-ttu-id="dcdd9-224">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-224">800</span></span> |
| <span data-ttu-id="dcdd9-225">DW400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-225">DW400</span></span> |<span data-ttu-id="dcdd9-226">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-226">100</span></span> |<span data-ttu-id="dcdd9-227">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-227">400</span></span> |<span data-ttu-id="dcdd9-228">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-228">800</span></span> |<span data-ttu-id="dcdd9-229">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-229">1,600</span></span> |
| <span data-ttu-id="dcdd9-230">DW500</span><span class="sxs-lookup"><span data-stu-id="dcdd9-230">DW500</span></span> |<span data-ttu-id="dcdd9-231">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-231">100</span></span> |<span data-ttu-id="dcdd9-232">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-232">400</span></span> |<span data-ttu-id="dcdd9-233">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-233">800</span></span> |<span data-ttu-id="dcdd9-234">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-234">1,600</span></span> |
| <span data-ttu-id="dcdd9-235">DW600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-235">DW600</span></span> |<span data-ttu-id="dcdd9-236">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-236">100</span></span> |<span data-ttu-id="dcdd9-237">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-237">400</span></span> |<span data-ttu-id="dcdd9-238">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-238">800</span></span> |<span data-ttu-id="dcdd9-239">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-239">1,600</span></span> |
| <span data-ttu-id="dcdd9-240">DW1000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-240">DW1000</span></span> |<span data-ttu-id="dcdd9-241">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-241">100</span></span> |<span data-ttu-id="dcdd9-242">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-242">800</span></span> |<span data-ttu-id="dcdd9-243">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-243">1,600</span></span> |<span data-ttu-id="dcdd9-244">3.200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-244">3,200</span></span> |
| <span data-ttu-id="dcdd9-245">DW1200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-245">DW1200</span></span> |<span data-ttu-id="dcdd9-246">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-246">100</span></span> |<span data-ttu-id="dcdd9-247">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-247">800</span></span> |<span data-ttu-id="dcdd9-248">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-248">1,600</span></span> |<span data-ttu-id="dcdd9-249">3.200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-249">3,200</span></span> |
| <span data-ttu-id="dcdd9-250">DW1500</span><span class="sxs-lookup"><span data-stu-id="dcdd9-250">DW1500</span></span> |<span data-ttu-id="dcdd9-251">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-251">100</span></span> |<span data-ttu-id="dcdd9-252">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-252">800</span></span> |<span data-ttu-id="dcdd9-253">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-253">1,600</span></span> |<span data-ttu-id="dcdd9-254">3.200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-254">3,200</span></span> |
| <span data-ttu-id="dcdd9-255">DW2000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-255">DW2000</span></span> |<span data-ttu-id="dcdd9-256">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-256">100</span></span> |<span data-ttu-id="dcdd9-257">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-257">1,600</span></span> |<span data-ttu-id="dcdd9-258">3.200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-258">3,200</span></span> |<span data-ttu-id="dcdd9-259">6.400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-259">6,400</span></span> |
| <span data-ttu-id="dcdd9-260">DW3000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-260">DW3000</span></span> |<span data-ttu-id="dcdd9-261">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-261">100</span></span> |<span data-ttu-id="dcdd9-262">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-262">1,600</span></span> |<span data-ttu-id="dcdd9-263">3.200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-263">3,200</span></span> |<span data-ttu-id="dcdd9-264">6.400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-264">6,400</span></span> |
| <span data-ttu-id="dcdd9-265">DW6000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-265">DW6000</span></span> |<span data-ttu-id="dcdd9-266">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-266">100</span></span> |<span data-ttu-id="dcdd9-267">3.200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-267">3,200</span></span> |<span data-ttu-id="dcdd9-268">6.400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-268">6,400</span></span> |<span data-ttu-id="dcdd9-269">12.800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-269">12,800</span></span> |

<span data-ttu-id="dcdd9-270">La tabella seguente indica la memoria allocata a ogni distribuzione in base alla DWU e alla classe di risorse statica.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-270">The following table maps the memory allocated to each distribution by DWU and static resource class.</span></span> <span data-ttu-id="dcdd9-271">Si noti che le classi di risorse superiori hanno memoria ridotta per rispettare i limiti delle DWU globali.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-271">Note that the higher resource classes have their memory reduced to honor the global DWU limits.</span></span>

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a><span data-ttu-id="dcdd9-272">Allocazioni di memoria per ogni distribuzione per le classi di risorse statiche (MB)</span><span class="sxs-lookup"><span data-stu-id="dcdd9-272">Memory allocations per distribution for static resource classes (MB)</span></span>
| <span data-ttu-id="dcdd9-273">DWU</span><span class="sxs-lookup"><span data-stu-id="dcdd9-273">DWU</span></span> | <span data-ttu-id="dcdd9-274">staticrc10</span><span class="sxs-lookup"><span data-stu-id="dcdd9-274">staticrc10</span></span> | <span data-ttu-id="dcdd9-275">staticrc20</span><span class="sxs-lookup"><span data-stu-id="dcdd9-275">staticrc20</span></span> | <span data-ttu-id="dcdd9-276">staticrc30</span><span class="sxs-lookup"><span data-stu-id="dcdd9-276">staticrc30</span></span> | <span data-ttu-id="dcdd9-277">staticrc40</span><span class="sxs-lookup"><span data-stu-id="dcdd9-277">staticrc40</span></span> | <span data-ttu-id="dcdd9-278">staticrc50</span><span class="sxs-lookup"><span data-stu-id="dcdd9-278">staticrc50</span></span> | <span data-ttu-id="dcdd9-279">staticrc60</span><span class="sxs-lookup"><span data-stu-id="dcdd9-279">staticrc60</span></span> | <span data-ttu-id="dcdd9-280">staticrc70</span><span class="sxs-lookup"><span data-stu-id="dcdd9-280">staticrc70</span></span> | <span data-ttu-id="dcdd9-281">staticrc80</span><span class="sxs-lookup"><span data-stu-id="dcdd9-281">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="dcdd9-282">DW100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-282">DW100</span></span> |<span data-ttu-id="dcdd9-283">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-283">100</span></span> |<span data-ttu-id="dcdd9-284">200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-284">200</span></span> |<span data-ttu-id="dcdd9-285">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-285">400</span></span> |<span data-ttu-id="dcdd9-286">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-286">400</span></span> |<span data-ttu-id="dcdd9-287">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-287">400</span></span> |<span data-ttu-id="dcdd9-288">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-288">400</span></span> |<span data-ttu-id="dcdd9-289">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-289">400</span></span> |<span data-ttu-id="dcdd9-290">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-290">400</span></span> |
| <span data-ttu-id="dcdd9-291">DW200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-291">DW200</span></span> |<span data-ttu-id="dcdd9-292">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-292">100</span></span> |<span data-ttu-id="dcdd9-293">200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-293">200</span></span> |<span data-ttu-id="dcdd9-294">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-294">400</span></span> |<span data-ttu-id="dcdd9-295">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-295">800</span></span> |<span data-ttu-id="dcdd9-296">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-296">800</span></span> |<span data-ttu-id="dcdd9-297">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-297">800</span></span> |<span data-ttu-id="dcdd9-298">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-298">800</span></span> |<span data-ttu-id="dcdd9-299">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-299">800</span></span> |
| <span data-ttu-id="dcdd9-300">DW300</span><span class="sxs-lookup"><span data-stu-id="dcdd9-300">DW300</span></span> |<span data-ttu-id="dcdd9-301">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-301">100</span></span> |<span data-ttu-id="dcdd9-302">200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-302">200</span></span> |<span data-ttu-id="dcdd9-303">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-303">400</span></span> |<span data-ttu-id="dcdd9-304">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-304">800</span></span> |<span data-ttu-id="dcdd9-305">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-305">800</span></span> |<span data-ttu-id="dcdd9-306">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-306">800</span></span> |<span data-ttu-id="dcdd9-307">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-307">800</span></span> |<span data-ttu-id="dcdd9-308">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-308">800</span></span> |
| <span data-ttu-id="dcdd9-309">DW400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-309">DW400</span></span> |<span data-ttu-id="dcdd9-310">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-310">100</span></span> |<span data-ttu-id="dcdd9-311">200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-311">200</span></span> |<span data-ttu-id="dcdd9-312">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-312">400</span></span> |<span data-ttu-id="dcdd9-313">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-313">800</span></span> |<span data-ttu-id="dcdd9-314">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-314">1,600</span></span> |<span data-ttu-id="dcdd9-315">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-315">1,600</span></span> |<span data-ttu-id="dcdd9-316">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-316">1,600</span></span> |<span data-ttu-id="dcdd9-317">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-317">1,600</span></span> |
| <span data-ttu-id="dcdd9-318">DW500</span><span class="sxs-lookup"><span data-stu-id="dcdd9-318">DW500</span></span> |<span data-ttu-id="dcdd9-319">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-319">100</span></span> |<span data-ttu-id="dcdd9-320">200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-320">200</span></span> |<span data-ttu-id="dcdd9-321">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-321">400</span></span> |<span data-ttu-id="dcdd9-322">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-322">800</span></span> |<span data-ttu-id="dcdd9-323">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-323">1,600</span></span> |<span data-ttu-id="dcdd9-324">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-324">1,600</span></span> |<span data-ttu-id="dcdd9-325">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-325">1,600</span></span> |<span data-ttu-id="dcdd9-326">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-326">1,600</span></span> |
| <span data-ttu-id="dcdd9-327">DW600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-327">DW600</span></span> |<span data-ttu-id="dcdd9-328">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-328">100</span></span> |<span data-ttu-id="dcdd9-329">200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-329">200</span></span> |<span data-ttu-id="dcdd9-330">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-330">400</span></span> |<span data-ttu-id="dcdd9-331">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-331">800</span></span> |<span data-ttu-id="dcdd9-332">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-332">1,600</span></span> |<span data-ttu-id="dcdd9-333">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-333">1,600</span></span> |<span data-ttu-id="dcdd9-334">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-334">1,600</span></span> |<span data-ttu-id="dcdd9-335">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-335">1,600</span></span> |
| <span data-ttu-id="dcdd9-336">DW1000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-336">DW1000</span></span> |<span data-ttu-id="dcdd9-337">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-337">100</span></span> |<span data-ttu-id="dcdd9-338">200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-338">200</span></span> |<span data-ttu-id="dcdd9-339">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-339">400</span></span> |<span data-ttu-id="dcdd9-340">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-340">800</span></span> |<span data-ttu-id="dcdd9-341">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-341">1,600</span></span> |<span data-ttu-id="dcdd9-342">3.200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-342">3,200</span></span> |<span data-ttu-id="dcdd9-343">3.200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-343">3,200</span></span> |<span data-ttu-id="dcdd9-344">3.200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-344">3,200</span></span> |
| <span data-ttu-id="dcdd9-345">DW1200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-345">DW1200</span></span> |<span data-ttu-id="dcdd9-346">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-346">100</span></span> |<span data-ttu-id="dcdd9-347">200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-347">200</span></span> |<span data-ttu-id="dcdd9-348">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-348">400</span></span> |<span data-ttu-id="dcdd9-349">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-349">800</span></span> |<span data-ttu-id="dcdd9-350">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-350">1,600</span></span> |<span data-ttu-id="dcdd9-351">3.200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-351">3,200</span></span> |<span data-ttu-id="dcdd9-352">3.200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-352">3,200</span></span> |<span data-ttu-id="dcdd9-353">3.200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-353">3,200</span></span> |
| <span data-ttu-id="dcdd9-354">DW1500</span><span class="sxs-lookup"><span data-stu-id="dcdd9-354">DW1500</span></span> |<span data-ttu-id="dcdd9-355">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-355">100</span></span> |<span data-ttu-id="dcdd9-356">200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-356">200</span></span> |<span data-ttu-id="dcdd9-357">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-357">400</span></span> |<span data-ttu-id="dcdd9-358">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-358">800</span></span> |<span data-ttu-id="dcdd9-359">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-359">1,600</span></span> |<span data-ttu-id="dcdd9-360">3.200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-360">3,200</span></span> |<span data-ttu-id="dcdd9-361">3.200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-361">3,200</span></span> |<span data-ttu-id="dcdd9-362">3.200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-362">3,200</span></span> |
| <span data-ttu-id="dcdd9-363">DW2000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-363">DW2000</span></span> |<span data-ttu-id="dcdd9-364">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-364">100</span></span> |<span data-ttu-id="dcdd9-365">200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-365">200</span></span> |<span data-ttu-id="dcdd9-366">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-366">400</span></span> |<span data-ttu-id="dcdd9-367">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-367">800</span></span> |<span data-ttu-id="dcdd9-368">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-368">1,600</span></span> |<span data-ttu-id="dcdd9-369">3.200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-369">3,200</span></span> |<span data-ttu-id="dcdd9-370">6.400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-370">6,400</span></span> |<span data-ttu-id="dcdd9-371">6.400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-371">6,400</span></span> |
| <span data-ttu-id="dcdd9-372">DW3000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-372">DW3000</span></span> |<span data-ttu-id="dcdd9-373">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-373">100</span></span> |<span data-ttu-id="dcdd9-374">200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-374">200</span></span> |<span data-ttu-id="dcdd9-375">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-375">400</span></span> |<span data-ttu-id="dcdd9-376">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-376">800</span></span> |<span data-ttu-id="dcdd9-377">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-377">1,600</span></span> |<span data-ttu-id="dcdd9-378">3.200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-378">3,200</span></span> |<span data-ttu-id="dcdd9-379">6.400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-379">6,400</span></span> |<span data-ttu-id="dcdd9-380">6.400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-380">6,400</span></span> |
| <span data-ttu-id="dcdd9-381">DW6000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-381">DW6000</span></span> |<span data-ttu-id="dcdd9-382">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-382">100</span></span> |<span data-ttu-id="dcdd9-383">200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-383">200</span></span> |<span data-ttu-id="dcdd9-384">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-384">400</span></span> |<span data-ttu-id="dcdd9-385">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-385">800</span></span> |<span data-ttu-id="dcdd9-386">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-386">1,600</span></span> |<span data-ttu-id="dcdd9-387">3.200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-387">3,200</span></span> |<span data-ttu-id="dcdd9-388">6.400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-388">6,400</span></span> |<span data-ttu-id="dcdd9-389">12.800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-389">12,800</span></span> |

<span data-ttu-id="dcdd9-390">Come si può notare nella tabella precedente, una query in esecuzione in DW2000 nella classe di risorse **xlargerc** avrà accesso a 6.400 MB di memoria in ognuno dei 60 database distribuiti.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-390">From the preceding table, you can see that a query running on a DW2000 in the **xlargerc** resource class would have access to 6,400 MB of memory within each of the 60 distributed databases.</span></span>  <span data-ttu-id="dcdd9-391">In SQL Data Warehouse sono presenti 60 distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-391">In SQL Data Warehouse, there are 60 distributions.</span></span> <span data-ttu-id="dcdd9-392">Per calcolare quindi l'allocazione totale di memoria per una query in una classe di risorse specifica, è necessario moltiplicare per 60 i valori precedenti.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-392">Therefore, to calculate the total memory allocation for a query in a given resource class, the above values should be multiplied by 60.</span></span>

### <a name="memory-allocations-system-wide-gb"></a><span data-ttu-id="dcdd9-393">Allocazioni di memoria a livello di sistema (GB)</span><span class="sxs-lookup"><span data-stu-id="dcdd9-393">Memory allocations system-wide (GB)</span></span>
| <span data-ttu-id="dcdd9-394">DWU</span><span class="sxs-lookup"><span data-stu-id="dcdd9-394">DWU</span></span> | <span data-ttu-id="dcdd9-395">smallrc</span><span class="sxs-lookup"><span data-stu-id="dcdd9-395">smallrc</span></span> | <span data-ttu-id="dcdd9-396">mediumrc</span><span class="sxs-lookup"><span data-stu-id="dcdd9-396">mediumrc</span></span> | <span data-ttu-id="dcdd9-397">largerc</span><span class="sxs-lookup"><span data-stu-id="dcdd9-397">largerc</span></span> | <span data-ttu-id="dcdd9-398">xlargerc</span><span class="sxs-lookup"><span data-stu-id="dcdd9-398">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="dcdd9-399">DW100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-399">DW100</span></span> |<span data-ttu-id="dcdd9-400">6</span><span class="sxs-lookup"><span data-stu-id="dcdd9-400">6</span></span> |<span data-ttu-id="dcdd9-401">6</span><span class="sxs-lookup"><span data-stu-id="dcdd9-401">6</span></span> |<span data-ttu-id="dcdd9-402">12</span><span class="sxs-lookup"><span data-stu-id="dcdd9-402">12</span></span> |<span data-ttu-id="dcdd9-403">23</span><span class="sxs-lookup"><span data-stu-id="dcdd9-403">23</span></span> |
| <span data-ttu-id="dcdd9-404">DW200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-404">DW200</span></span> |<span data-ttu-id="dcdd9-405">6</span><span class="sxs-lookup"><span data-stu-id="dcdd9-405">6</span></span> |<span data-ttu-id="dcdd9-406">12</span><span class="sxs-lookup"><span data-stu-id="dcdd9-406">12</span></span> |<span data-ttu-id="dcdd9-407">23</span><span class="sxs-lookup"><span data-stu-id="dcdd9-407">23</span></span> |<span data-ttu-id="dcdd9-408">47</span><span class="sxs-lookup"><span data-stu-id="dcdd9-408">47</span></span> |
| <span data-ttu-id="dcdd9-409">DW300</span><span class="sxs-lookup"><span data-stu-id="dcdd9-409">DW300</span></span> |<span data-ttu-id="dcdd9-410">6</span><span class="sxs-lookup"><span data-stu-id="dcdd9-410">6</span></span> |<span data-ttu-id="dcdd9-411">12</span><span class="sxs-lookup"><span data-stu-id="dcdd9-411">12</span></span> |<span data-ttu-id="dcdd9-412">23</span><span class="sxs-lookup"><span data-stu-id="dcdd9-412">23</span></span> |<span data-ttu-id="dcdd9-413">47</span><span class="sxs-lookup"><span data-stu-id="dcdd9-413">47</span></span> |
| <span data-ttu-id="dcdd9-414">DW400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-414">DW400</span></span> |<span data-ttu-id="dcdd9-415">6</span><span class="sxs-lookup"><span data-stu-id="dcdd9-415">6</span></span> |<span data-ttu-id="dcdd9-416">23</span><span class="sxs-lookup"><span data-stu-id="dcdd9-416">23</span></span> |<span data-ttu-id="dcdd9-417">47</span><span class="sxs-lookup"><span data-stu-id="dcdd9-417">47</span></span> |<span data-ttu-id="dcdd9-418">94</span><span class="sxs-lookup"><span data-stu-id="dcdd9-418">94</span></span> |
| <span data-ttu-id="dcdd9-419">DW500</span><span class="sxs-lookup"><span data-stu-id="dcdd9-419">DW500</span></span> |<span data-ttu-id="dcdd9-420">6</span><span class="sxs-lookup"><span data-stu-id="dcdd9-420">6</span></span> |<span data-ttu-id="dcdd9-421">23</span><span class="sxs-lookup"><span data-stu-id="dcdd9-421">23</span></span> |<span data-ttu-id="dcdd9-422">47</span><span class="sxs-lookup"><span data-stu-id="dcdd9-422">47</span></span> |<span data-ttu-id="dcdd9-423">94</span><span class="sxs-lookup"><span data-stu-id="dcdd9-423">94</span></span> |
| <span data-ttu-id="dcdd9-424">DW600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-424">DW600</span></span> |<span data-ttu-id="dcdd9-425">6</span><span class="sxs-lookup"><span data-stu-id="dcdd9-425">6</span></span> |<span data-ttu-id="dcdd9-426">23</span><span class="sxs-lookup"><span data-stu-id="dcdd9-426">23</span></span> |<span data-ttu-id="dcdd9-427">47</span><span class="sxs-lookup"><span data-stu-id="dcdd9-427">47</span></span> |<span data-ttu-id="dcdd9-428">94</span><span class="sxs-lookup"><span data-stu-id="dcdd9-428">94</span></span> |
| <span data-ttu-id="dcdd9-429">DW1000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-429">DW1000</span></span> |<span data-ttu-id="dcdd9-430">6</span><span class="sxs-lookup"><span data-stu-id="dcdd9-430">6</span></span> |<span data-ttu-id="dcdd9-431">47</span><span class="sxs-lookup"><span data-stu-id="dcdd9-431">47</span></span> |<span data-ttu-id="dcdd9-432">94</span><span class="sxs-lookup"><span data-stu-id="dcdd9-432">94</span></span> |<span data-ttu-id="dcdd9-433">188</span><span class="sxs-lookup"><span data-stu-id="dcdd9-433">188</span></span> |
| <span data-ttu-id="dcdd9-434">DW1200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-434">DW1200</span></span> |<span data-ttu-id="dcdd9-435">6</span><span class="sxs-lookup"><span data-stu-id="dcdd9-435">6</span></span> |<span data-ttu-id="dcdd9-436">47</span><span class="sxs-lookup"><span data-stu-id="dcdd9-436">47</span></span> |<span data-ttu-id="dcdd9-437">94</span><span class="sxs-lookup"><span data-stu-id="dcdd9-437">94</span></span> |<span data-ttu-id="dcdd9-438">188</span><span class="sxs-lookup"><span data-stu-id="dcdd9-438">188</span></span> |
| <span data-ttu-id="dcdd9-439">DW1500</span><span class="sxs-lookup"><span data-stu-id="dcdd9-439">DW1500</span></span> |<span data-ttu-id="dcdd9-440">6</span><span class="sxs-lookup"><span data-stu-id="dcdd9-440">6</span></span> |<span data-ttu-id="dcdd9-441">47</span><span class="sxs-lookup"><span data-stu-id="dcdd9-441">47</span></span> |<span data-ttu-id="dcdd9-442">94</span><span class="sxs-lookup"><span data-stu-id="dcdd9-442">94</span></span> |<span data-ttu-id="dcdd9-443">188</span><span class="sxs-lookup"><span data-stu-id="dcdd9-443">188</span></span> |
| <span data-ttu-id="dcdd9-444">DW2000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-444">DW2000</span></span> |<span data-ttu-id="dcdd9-445">6</span><span class="sxs-lookup"><span data-stu-id="dcdd9-445">6</span></span> |<span data-ttu-id="dcdd9-446">94</span><span class="sxs-lookup"><span data-stu-id="dcdd9-446">94</span></span> |<span data-ttu-id="dcdd9-447">188</span><span class="sxs-lookup"><span data-stu-id="dcdd9-447">188</span></span> |<span data-ttu-id="dcdd9-448">375</span><span class="sxs-lookup"><span data-stu-id="dcdd9-448">375</span></span> |
| <span data-ttu-id="dcdd9-449">DW3000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-449">DW3000</span></span> |<span data-ttu-id="dcdd9-450">6</span><span class="sxs-lookup"><span data-stu-id="dcdd9-450">6</span></span> |<span data-ttu-id="dcdd9-451">94</span><span class="sxs-lookup"><span data-stu-id="dcdd9-451">94</span></span> |<span data-ttu-id="dcdd9-452">188</span><span class="sxs-lookup"><span data-stu-id="dcdd9-452">188</span></span> |<span data-ttu-id="dcdd9-453">375</span><span class="sxs-lookup"><span data-stu-id="dcdd9-453">375</span></span> |
| <span data-ttu-id="dcdd9-454">DW6000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-454">DW6000</span></span> |<span data-ttu-id="dcdd9-455">6</span><span class="sxs-lookup"><span data-stu-id="dcdd9-455">6</span></span> |<span data-ttu-id="dcdd9-456">188</span><span class="sxs-lookup"><span data-stu-id="dcdd9-456">188</span></span> |<span data-ttu-id="dcdd9-457">375</span><span class="sxs-lookup"><span data-stu-id="dcdd9-457">375</span></span> |<span data-ttu-id="dcdd9-458">750</span><span class="sxs-lookup"><span data-stu-id="dcdd9-458">750</span></span> |

<span data-ttu-id="dcdd9-459">Come si può notare in questa tabella di allocazioni di memoria a livello di sistema, a una query in esecuzione in DW2000 nella classe di risorse xlargerc viene allocato un totale di 375 GB di memoria (6.400 MB * 60 distribuzioni/1.024 per la conversione in GB) nell'intero SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-459">From this table of system-wide memory allocations, you can see that a query running on a DW2000 in the xlargerc resource class is allocated a total of 375 GB of memory (6,400 MB * 60 distributions / 1,024 to convert to GB) over the entirety of your SQL Data Warehouse.</span></span>

<span data-ttu-id="dcdd9-460">Lo stesso calcolo si applica alle classi di risorse statiche.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-460">The same calculation applies to static resource classes.</span></span>
 
## <a name="concurrency-slot-consumption"></a><span data-ttu-id="dcdd9-461">Utilizzo di slot di concorrenza</span><span class="sxs-lookup"><span data-stu-id="dcdd9-461">Concurrency slot consumption</span></span>  
<span data-ttu-id="dcdd9-462">SQL Data Warehouse concede più memoria alle query in esecuzione nelle classi di risorse più grandi.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-462">SQL Data Warehouse grants more memory to queries running in higher resource classes.</span></span> <span data-ttu-id="dcdd9-463">La memoria è una risorsa fissa.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-463">Memory is a fixed resource.</span></span>  <span data-ttu-id="dcdd9-464">Maggiore sarà la quantità di memoria allocata per ogni query, quindi, minore sarà il numero di richieste simultanee che è possibile eseguire.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-464">Therefore, the more memory allocated per query, the fewer concurrent queries can execute.</span></span> <span data-ttu-id="dcdd9-465">La tabella seguente riprende tutti i concetti descritti finora in un'unica rappresentazione che mostra il numero di slot di concorrenza disponibili per DWU e gli slot usati da ogni classe di risorse.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-465">The following table reiterates all of the previous concepts in a single view that shows the number of concurrency slots available by DWU and the slots consumed by each resource class.</span></span>  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a><span data-ttu-id="dcdd9-466">Allocazione e consumo degli slot di concorrenza per le classi di risorse dinamiche</span><span class="sxs-lookup"><span data-stu-id="dcdd9-466">Allocation and consumption of concurrency slots for dynamic resource classes</span></span>  
| <span data-ttu-id="dcdd9-467">DWU</span><span class="sxs-lookup"><span data-stu-id="dcdd9-467">DWU</span></span> | <span data-ttu-id="dcdd9-468">Numero massimo di query simultanee</span><span class="sxs-lookup"><span data-stu-id="dcdd9-468">Maximum concurrent queries</span></span> | <span data-ttu-id="dcdd9-469">Numero di slot di concorrenza allocati</span><span class="sxs-lookup"><span data-stu-id="dcdd9-469">Concurrency slots allocated</span></span> | <span data-ttu-id="dcdd9-470">Slot utilizzati da smallrc</span><span class="sxs-lookup"><span data-stu-id="dcdd9-470">Slots used by smallrc</span></span> | <span data-ttu-id="dcdd9-471">Slot utilizzati da mediumrc</span><span class="sxs-lookup"><span data-stu-id="dcdd9-471">Slots used by mediumrc</span></span> | <span data-ttu-id="dcdd9-472">Slot utilizzati da largerc</span><span class="sxs-lookup"><span data-stu-id="dcdd9-472">Slots used by largerc</span></span> | <span data-ttu-id="dcdd9-473">Slot utilizzati da xlargerc</span><span class="sxs-lookup"><span data-stu-id="dcdd9-473">Slots used by xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="dcdd9-474">DW100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-474">DW100</span></span> |<span data-ttu-id="dcdd9-475">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-475">4</span></span> |<span data-ttu-id="dcdd9-476">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-476">4</span></span> |<span data-ttu-id="dcdd9-477">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-477">1</span></span> |<span data-ttu-id="dcdd9-478">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-478">1</span></span> |<span data-ttu-id="dcdd9-479">2</span><span class="sxs-lookup"><span data-stu-id="dcdd9-479">2</span></span> |<span data-ttu-id="dcdd9-480">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-480">4</span></span> |
| <span data-ttu-id="dcdd9-481">DW200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-481">DW200</span></span> |<span data-ttu-id="dcdd9-482">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-482">8</span></span> |<span data-ttu-id="dcdd9-483">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-483">8</span></span> |<span data-ttu-id="dcdd9-484">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-484">1</span></span> |<span data-ttu-id="dcdd9-485">2</span><span class="sxs-lookup"><span data-stu-id="dcdd9-485">2</span></span> |<span data-ttu-id="dcdd9-486">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-486">4</span></span> |<span data-ttu-id="dcdd9-487">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-487">8</span></span> |
| <span data-ttu-id="dcdd9-488">DW300</span><span class="sxs-lookup"><span data-stu-id="dcdd9-488">DW300</span></span> |<span data-ttu-id="dcdd9-489">12</span><span class="sxs-lookup"><span data-stu-id="dcdd9-489">12</span></span> |<span data-ttu-id="dcdd9-490">12</span><span class="sxs-lookup"><span data-stu-id="dcdd9-490">12</span></span> |<span data-ttu-id="dcdd9-491">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-491">1</span></span> |<span data-ttu-id="dcdd9-492">2</span><span class="sxs-lookup"><span data-stu-id="dcdd9-492">2</span></span> |<span data-ttu-id="dcdd9-493">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-493">4</span></span> |<span data-ttu-id="dcdd9-494">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-494">8</span></span> |
| <span data-ttu-id="dcdd9-495">DW400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-495">DW400</span></span> |<span data-ttu-id="dcdd9-496">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-496">16</span></span> |<span data-ttu-id="dcdd9-497">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-497">16</span></span> |<span data-ttu-id="dcdd9-498">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-498">1</span></span> |<span data-ttu-id="dcdd9-499">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-499">4</span></span> |<span data-ttu-id="dcdd9-500">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-500">8</span></span> |<span data-ttu-id="dcdd9-501">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-501">16</span></span> |
| <span data-ttu-id="dcdd9-502">DW500</span><span class="sxs-lookup"><span data-stu-id="dcdd9-502">DW500</span></span> |<span data-ttu-id="dcdd9-503">20</span><span class="sxs-lookup"><span data-stu-id="dcdd9-503">20</span></span> |<span data-ttu-id="dcdd9-504">20</span><span class="sxs-lookup"><span data-stu-id="dcdd9-504">20</span></span> |<span data-ttu-id="dcdd9-505">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-505">1</span></span> |<span data-ttu-id="dcdd9-506">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-506">4</span></span> |<span data-ttu-id="dcdd9-507">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-507">8</span></span> |<span data-ttu-id="dcdd9-508">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-508">16</span></span> |
| <span data-ttu-id="dcdd9-509">DW600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-509">DW600</span></span> |<span data-ttu-id="dcdd9-510">24</span><span class="sxs-lookup"><span data-stu-id="dcdd9-510">24</span></span> |<span data-ttu-id="dcdd9-511">24</span><span class="sxs-lookup"><span data-stu-id="dcdd9-511">24</span></span> |<span data-ttu-id="dcdd9-512">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-512">1</span></span> |<span data-ttu-id="dcdd9-513">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-513">4</span></span> |<span data-ttu-id="dcdd9-514">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-514">8</span></span> |<span data-ttu-id="dcdd9-515">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-515">16</span></span> |
| <span data-ttu-id="dcdd9-516">DW1000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-516">DW1000</span></span> |<span data-ttu-id="dcdd9-517">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-517">32</span></span> |<span data-ttu-id="dcdd9-518">40</span><span class="sxs-lookup"><span data-stu-id="dcdd9-518">40</span></span> |<span data-ttu-id="dcdd9-519">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-519">1</span></span> |<span data-ttu-id="dcdd9-520">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-520">8</span></span> |<span data-ttu-id="dcdd9-521">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-521">16</span></span> |<span data-ttu-id="dcdd9-522">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-522">32</span></span> |
| <span data-ttu-id="dcdd9-523">DW1200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-523">DW1200</span></span> |<span data-ttu-id="dcdd9-524">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-524">32</span></span> |<span data-ttu-id="dcdd9-525">48</span><span class="sxs-lookup"><span data-stu-id="dcdd9-525">48</span></span> |<span data-ttu-id="dcdd9-526">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-526">1</span></span> |<span data-ttu-id="dcdd9-527">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-527">8</span></span> |<span data-ttu-id="dcdd9-528">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-528">16</span></span> |<span data-ttu-id="dcdd9-529">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-529">32</span></span> |
| <span data-ttu-id="dcdd9-530">DW1500</span><span class="sxs-lookup"><span data-stu-id="dcdd9-530">DW1500</span></span> |<span data-ttu-id="dcdd9-531">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-531">32</span></span> |<span data-ttu-id="dcdd9-532">60</span><span class="sxs-lookup"><span data-stu-id="dcdd9-532">60</span></span> |<span data-ttu-id="dcdd9-533">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-533">1</span></span> |<span data-ttu-id="dcdd9-534">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-534">8</span></span> |<span data-ttu-id="dcdd9-535">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-535">16</span></span> |<span data-ttu-id="dcdd9-536">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-536">32</span></span> |
| <span data-ttu-id="dcdd9-537">DW2000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-537">DW2000</span></span> |<span data-ttu-id="dcdd9-538">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-538">32</span></span> |<span data-ttu-id="dcdd9-539">80</span><span class="sxs-lookup"><span data-stu-id="dcdd9-539">80</span></span> |<span data-ttu-id="dcdd9-540">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-540">1</span></span> |<span data-ttu-id="dcdd9-541">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-541">16</span></span> |<span data-ttu-id="dcdd9-542">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-542">32</span></span> |<span data-ttu-id="dcdd9-543">64</span><span class="sxs-lookup"><span data-stu-id="dcdd9-543">64</span></span> |
| <span data-ttu-id="dcdd9-544">DW3000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-544">DW3000</span></span> |<span data-ttu-id="dcdd9-545">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-545">32</span></span> |<span data-ttu-id="dcdd9-546">120</span><span class="sxs-lookup"><span data-stu-id="dcdd9-546">120</span></span> |<span data-ttu-id="dcdd9-547">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-547">1</span></span> |<span data-ttu-id="dcdd9-548">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-548">16</span></span> |<span data-ttu-id="dcdd9-549">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-549">32</span></span> |<span data-ttu-id="dcdd9-550">64</span><span class="sxs-lookup"><span data-stu-id="dcdd9-550">64</span></span> |
| <span data-ttu-id="dcdd9-551">DW6000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-551">DW6000</span></span> |<span data-ttu-id="dcdd9-552">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-552">32</span></span> |<span data-ttu-id="dcdd9-553">240</span><span class="sxs-lookup"><span data-stu-id="dcdd9-553">240</span></span> |<span data-ttu-id="dcdd9-554">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-554">1</span></span> |<span data-ttu-id="dcdd9-555">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-555">32</span></span> |<span data-ttu-id="dcdd9-556">64</span><span class="sxs-lookup"><span data-stu-id="dcdd9-556">64</span></span> |<span data-ttu-id="dcdd9-557">128</span><span class="sxs-lookup"><span data-stu-id="dcdd9-557">128</span></span> |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a><span data-ttu-id="dcdd9-558">Allocazione e consumo degli slot di concorrenza per le classi di risorse statiche</span><span class="sxs-lookup"><span data-stu-id="dcdd9-558">Allocation and consumption of concurrency slots for static resource classes</span></span>  
| <span data-ttu-id="dcdd9-559">DWU</span><span class="sxs-lookup"><span data-stu-id="dcdd9-559">DWU</span></span> | <span data-ttu-id="dcdd9-560">Numero massimo di query simultanee</span><span class="sxs-lookup"><span data-stu-id="dcdd9-560">Maximum concurrent queries</span></span> | <span data-ttu-id="dcdd9-561">Numero di slot di concorrenza allocati</span><span class="sxs-lookup"><span data-stu-id="dcdd9-561">Concurrency slots allocated</span></span> |<span data-ttu-id="dcdd9-562">staticrc10</span><span class="sxs-lookup"><span data-stu-id="dcdd9-562">staticrc10</span></span> | <span data-ttu-id="dcdd9-563">staticrc20</span><span class="sxs-lookup"><span data-stu-id="dcdd9-563">staticrc20</span></span> | <span data-ttu-id="dcdd9-564">staticrc30</span><span class="sxs-lookup"><span data-stu-id="dcdd9-564">staticrc30</span></span> | <span data-ttu-id="dcdd9-565">staticrc40</span><span class="sxs-lookup"><span data-stu-id="dcdd9-565">staticrc40</span></span> | <span data-ttu-id="dcdd9-566">staticrc50</span><span class="sxs-lookup"><span data-stu-id="dcdd9-566">staticrc50</span></span> | <span data-ttu-id="dcdd9-567">staticrc60</span><span class="sxs-lookup"><span data-stu-id="dcdd9-567">staticrc60</span></span> | <span data-ttu-id="dcdd9-568">staticrc70</span><span class="sxs-lookup"><span data-stu-id="dcdd9-568">staticrc70</span></span> | <span data-ttu-id="dcdd9-569">staticrc80</span><span class="sxs-lookup"><span data-stu-id="dcdd9-569">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="dcdd9-570">DW100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-570">DW100</span></span> |<span data-ttu-id="dcdd9-571">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-571">4</span></span> |<span data-ttu-id="dcdd9-572">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-572">4</span></span> |<span data-ttu-id="dcdd9-573">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-573">1</span></span> |<span data-ttu-id="dcdd9-574">2</span><span class="sxs-lookup"><span data-stu-id="dcdd9-574">2</span></span> |<span data-ttu-id="dcdd9-575">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-575">4</span></span> |<span data-ttu-id="dcdd9-576">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-576">4</span></span> |<span data-ttu-id="dcdd9-577">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-577">4</span></span> |<span data-ttu-id="dcdd9-578">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-578">4</span></span> |<span data-ttu-id="dcdd9-579">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-579">4</span></span> |<span data-ttu-id="dcdd9-580">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-580">4</span></span> |
| <span data-ttu-id="dcdd9-581">DW200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-581">DW200</span></span> |<span data-ttu-id="dcdd9-582">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-582">8</span></span> |<span data-ttu-id="dcdd9-583">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-583">8</span></span> |<span data-ttu-id="dcdd9-584">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-584">1</span></span> |<span data-ttu-id="dcdd9-585">2</span><span class="sxs-lookup"><span data-stu-id="dcdd9-585">2</span></span> |<span data-ttu-id="dcdd9-586">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-586">4</span></span> |<span data-ttu-id="dcdd9-587">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-587">8</span></span> |<span data-ttu-id="dcdd9-588">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-588">8</span></span> |<span data-ttu-id="dcdd9-589">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-589">8</span></span> |<span data-ttu-id="dcdd9-590">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-590">8</span></span> |<span data-ttu-id="dcdd9-591">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-591">8</span></span> |
| <span data-ttu-id="dcdd9-592">DW300</span><span class="sxs-lookup"><span data-stu-id="dcdd9-592">DW300</span></span> |<span data-ttu-id="dcdd9-593">12</span><span class="sxs-lookup"><span data-stu-id="dcdd9-593">12</span></span> |<span data-ttu-id="dcdd9-594">12</span><span class="sxs-lookup"><span data-stu-id="dcdd9-594">12</span></span> |<span data-ttu-id="dcdd9-595">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-595">1</span></span> |<span data-ttu-id="dcdd9-596">2</span><span class="sxs-lookup"><span data-stu-id="dcdd9-596">2</span></span> |<span data-ttu-id="dcdd9-597">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-597">4</span></span> |<span data-ttu-id="dcdd9-598">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-598">8</span></span> |<span data-ttu-id="dcdd9-599">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-599">8</span></span> |<span data-ttu-id="dcdd9-600">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-600">8</span></span> |<span data-ttu-id="dcdd9-601">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-601">8</span></span> |<span data-ttu-id="dcdd9-602">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-602">8</span></span> |
| <span data-ttu-id="dcdd9-603">DW400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-603">DW400</span></span> |<span data-ttu-id="dcdd9-604">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-604">16</span></span> |<span data-ttu-id="dcdd9-605">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-605">16</span></span> |<span data-ttu-id="dcdd9-606">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-606">1</span></span> |<span data-ttu-id="dcdd9-607">2</span><span class="sxs-lookup"><span data-stu-id="dcdd9-607">2</span></span> |<span data-ttu-id="dcdd9-608">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-608">4</span></span> |<span data-ttu-id="dcdd9-609">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-609">8</span></span> |<span data-ttu-id="dcdd9-610">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-610">16</span></span> |<span data-ttu-id="dcdd9-611">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-611">16</span></span> |<span data-ttu-id="dcdd9-612">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-612">16</span></span> |<span data-ttu-id="dcdd9-613">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-613">16</span></span> |
| <span data-ttu-id="dcdd9-614">DW500</span><span class="sxs-lookup"><span data-stu-id="dcdd9-614">DW500</span></span> | <span data-ttu-id="dcdd9-615">20</span><span class="sxs-lookup"><span data-stu-id="dcdd9-615">20</span></span>| <span data-ttu-id="dcdd9-616">20</span><span class="sxs-lookup"><span data-stu-id="dcdd9-616">20</span></span>| <span data-ttu-id="dcdd9-617">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-617">1</span></span>| <span data-ttu-id="dcdd9-618">2</span><span class="sxs-lookup"><span data-stu-id="dcdd9-618">2</span></span>| <span data-ttu-id="dcdd9-619">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-619">4</span></span>| <span data-ttu-id="dcdd9-620">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-620">8</span></span>| <span data-ttu-id="dcdd9-621">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-621">16</span></span>| <span data-ttu-id="dcdd9-622">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-622">16</span></span>| <span data-ttu-id="dcdd9-623">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-623">16</span></span>| <span data-ttu-id="dcdd9-624">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-624">16</span></span>|
| <span data-ttu-id="dcdd9-625">DW600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-625">DW600</span></span> | <span data-ttu-id="dcdd9-626">24</span><span class="sxs-lookup"><span data-stu-id="dcdd9-626">24</span></span>| <span data-ttu-id="dcdd9-627">24</span><span class="sxs-lookup"><span data-stu-id="dcdd9-627">24</span></span>| <span data-ttu-id="dcdd9-628">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-628">1</span></span>| <span data-ttu-id="dcdd9-629">2</span><span class="sxs-lookup"><span data-stu-id="dcdd9-629">2</span></span>| <span data-ttu-id="dcdd9-630">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-630">4</span></span>| <span data-ttu-id="dcdd9-631">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-631">8</span></span>| <span data-ttu-id="dcdd9-632">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-632">16</span></span>| <span data-ttu-id="dcdd9-633">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-633">16</span></span>| <span data-ttu-id="dcdd9-634">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-634">16</span></span>| <span data-ttu-id="dcdd9-635">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-635">16</span></span>|
| <span data-ttu-id="dcdd9-636">DW1000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-636">DW1000</span></span> | <span data-ttu-id="dcdd9-637">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-637">32</span></span>| <span data-ttu-id="dcdd9-638">40</span><span class="sxs-lookup"><span data-stu-id="dcdd9-638">40</span></span>| <span data-ttu-id="dcdd9-639">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-639">1</span></span>| <span data-ttu-id="dcdd9-640">2</span><span class="sxs-lookup"><span data-stu-id="dcdd9-640">2</span></span>| <span data-ttu-id="dcdd9-641">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-641">4</span></span>| <span data-ttu-id="dcdd9-642">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-642">8</span></span>| <span data-ttu-id="dcdd9-643">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-643">16</span></span>| <span data-ttu-id="dcdd9-644">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-644">32</span></span>| <span data-ttu-id="dcdd9-645">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-645">32</span></span>| <span data-ttu-id="dcdd9-646">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-646">32</span></span>|
| <span data-ttu-id="dcdd9-647">DW1200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-647">DW1200</span></span> | <span data-ttu-id="dcdd9-648">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-648">32</span></span>| <span data-ttu-id="dcdd9-649">48</span><span class="sxs-lookup"><span data-stu-id="dcdd9-649">48</span></span>| <span data-ttu-id="dcdd9-650">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-650">1</span></span>| <span data-ttu-id="dcdd9-651">2</span><span class="sxs-lookup"><span data-stu-id="dcdd9-651">2</span></span>| <span data-ttu-id="dcdd9-652">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-652">4</span></span>| <span data-ttu-id="dcdd9-653">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-653">8</span></span>| <span data-ttu-id="dcdd9-654">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-654">16</span></span>| <span data-ttu-id="dcdd9-655">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-655">32</span></span>| <span data-ttu-id="dcdd9-656">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-656">32</span></span>| <span data-ttu-id="dcdd9-657">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-657">32</span></span>|
| <span data-ttu-id="dcdd9-658">DW1500</span><span class="sxs-lookup"><span data-stu-id="dcdd9-658">DW1500</span></span> | <span data-ttu-id="dcdd9-659">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-659">32</span></span>| <span data-ttu-id="dcdd9-660">60</span><span class="sxs-lookup"><span data-stu-id="dcdd9-660">60</span></span>| <span data-ttu-id="dcdd9-661">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-661">1</span></span>| <span data-ttu-id="dcdd9-662">2</span><span class="sxs-lookup"><span data-stu-id="dcdd9-662">2</span></span>| <span data-ttu-id="dcdd9-663">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-663">4</span></span>| <span data-ttu-id="dcdd9-664">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-664">8</span></span>| <span data-ttu-id="dcdd9-665">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-665">16</span></span>| <span data-ttu-id="dcdd9-666">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-666">32</span></span>| <span data-ttu-id="dcdd9-667">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-667">32</span></span>| <span data-ttu-id="dcdd9-668">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-668">32</span></span>|
| <span data-ttu-id="dcdd9-669">DW2000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-669">DW2000</span></span> | <span data-ttu-id="dcdd9-670">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-670">32</span></span>| <span data-ttu-id="dcdd9-671">80</span><span class="sxs-lookup"><span data-stu-id="dcdd9-671">80</span></span>| <span data-ttu-id="dcdd9-672">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-672">1</span></span>| <span data-ttu-id="dcdd9-673">2</span><span class="sxs-lookup"><span data-stu-id="dcdd9-673">2</span></span>| <span data-ttu-id="dcdd9-674">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-674">4</span></span>| <span data-ttu-id="dcdd9-675">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-675">8</span></span>| <span data-ttu-id="dcdd9-676">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-676">16</span></span>| <span data-ttu-id="dcdd9-677">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-677">32</span></span>| <span data-ttu-id="dcdd9-678">64</span><span class="sxs-lookup"><span data-stu-id="dcdd9-678">64</span></span>| <span data-ttu-id="dcdd9-679">64</span><span class="sxs-lookup"><span data-stu-id="dcdd9-679">64</span></span>|
| <span data-ttu-id="dcdd9-680">DW3000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-680">DW3000</span></span> | <span data-ttu-id="dcdd9-681">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-681">32</span></span>| <span data-ttu-id="dcdd9-682">120</span><span class="sxs-lookup"><span data-stu-id="dcdd9-682">120</span></span>| <span data-ttu-id="dcdd9-683">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-683">1</span></span>| <span data-ttu-id="dcdd9-684">2</span><span class="sxs-lookup"><span data-stu-id="dcdd9-684">2</span></span>| <span data-ttu-id="dcdd9-685">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-685">4</span></span>| <span data-ttu-id="dcdd9-686">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-686">8</span></span>| <span data-ttu-id="dcdd9-687">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-687">16</span></span>| <span data-ttu-id="dcdd9-688">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-688">32</span></span>| <span data-ttu-id="dcdd9-689">64</span><span class="sxs-lookup"><span data-stu-id="dcdd9-689">64</span></span>| <span data-ttu-id="dcdd9-690">64</span><span class="sxs-lookup"><span data-stu-id="dcdd9-690">64</span></span>|
| <span data-ttu-id="dcdd9-691">DW6000</span><span class="sxs-lookup"><span data-stu-id="dcdd9-691">DW6000</span></span> | <span data-ttu-id="dcdd9-692">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-692">32</span></span>| <span data-ttu-id="dcdd9-693">240</span><span class="sxs-lookup"><span data-stu-id="dcdd9-693">240</span></span>| <span data-ttu-id="dcdd9-694">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-694">1</span></span>| <span data-ttu-id="dcdd9-695">2</span><span class="sxs-lookup"><span data-stu-id="dcdd9-695">2</span></span>| <span data-ttu-id="dcdd9-696">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-696">4</span></span>| <span data-ttu-id="dcdd9-697">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-697">8</span></span>| <span data-ttu-id="dcdd9-698">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-698">16</span></span>| <span data-ttu-id="dcdd9-699">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-699">32</span></span>| <span data-ttu-id="dcdd9-700">64</span><span class="sxs-lookup"><span data-stu-id="dcdd9-700">64</span></span>| <span data-ttu-id="dcdd9-701">128</span><span class="sxs-lookup"><span data-stu-id="dcdd9-701">128</span></span>|

<span data-ttu-id="dcdd9-702">Come si può notare da queste tabelle, l'esecuzione di SQL Data Warehouse come DW1000 alloca un massimo di 32 query simultanee e un totale di 40 slot di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-702">From these tables, you can see that SQL Data Warehouse running as DW1000 allocates a maximum of 32 concurrent queries and a total of 40 concurrency slots.</span></span> <span data-ttu-id="dcdd9-703">Se l'esecuzione avviene da parte di tutti gli utenti nella classe smallrc, vengono consentite 32 query simultanee, poiché ognuna richiede 1 slot di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-703">If all users are running in smallrc, 32 concurrent queries would be allowed because each query would consume 1 concurrency slot.</span></span> <span data-ttu-id="dcdd9-704">Se l'esecuzione avviene da parte di tutti gli utenti di un DW1000 in una classe mediumrc, per ogni query vengono allocati 800 MB a distribuzione, per un'allocazione di memoria totale pari a 47 GB per query, mentre il numero degli utenti simultanei viene limitato a 5 (40 slot di concorrenza, 8 per ogni utente mediumrc).</span><span class="sxs-lookup"><span data-stu-id="dcdd9-704">If all users on a DW1000 were running in mediumrc, each query would be allocated 800 MB per distribution for a total memory allocation of 47 GB per query, and concurrency would be limited to 5 users (40 concurrency slots / 8 slots per mediumrc user).</span></span>

## <a name="selecting-proper-resource-class"></a><span data-ttu-id="dcdd9-705">Scelta della classe di risorse appropriata</span><span class="sxs-lookup"><span data-stu-id="dcdd9-705">Selecting proper resource class</span></span>  
<span data-ttu-id="dcdd9-706">È buona norma assegnare in modo permanente gli utenti a una classe di risorse invece di modificare la classe di risorse degli utenti.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-706">A good practice is to permanently assign users to a resource class rather than changing their resource classes.</span></span> <span data-ttu-id="dcdd9-707">I caricamenti in tabelle columnstore cluster, ad esempio, creano indici di qualità superiore quando viene allocata una quantità di memoria maggiore.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-707">For example, loads to clustered columnstore tables create higher-quality indexes when allocated more memory.</span></span> <span data-ttu-id="dcdd9-708">Per assicurarsi che caricamenti abbiano accesso alla memoria superiore, creare un utente specifico per il caricamento dei dati e assegnare permanentemente a questo utente una classe di risorse superiore.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-708">To ensure that loads have access to higher memory, create a user specifically for loading data and permanently assign this user to a higher resource class.</span></span>
<span data-ttu-id="dcdd9-709">Ci sono alcune procedure consigliate da seguire.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-709">There are a couple of best practices to follow here.</span></span> <span data-ttu-id="dcdd9-710">Come indicato in precedenza, SQL Data Warehouse supporta due tipi di classi di risorse: le classi di risorse statiche e quelle dinamiche.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-710">As mentioned above, SQL DW supports two kinds of resource class types: static resource classes and dynamic resource classes.</span></span>
### <a name="loading-best-practices"></a><span data-ttu-id="dcdd9-711">Procedure consigliate per il caricamento</span><span class="sxs-lookup"><span data-stu-id="dcdd9-711">Loading best practices</span></span>
1.  <span data-ttu-id="dcdd9-712">Se si prevedono caricamenti con quantità di dati regolari, una classe di risorse statica è una scelta appropriata.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-712">If the expectations are loads with regular amount of data, a static resource class is a good choice.</span></span> <span data-ttu-id="dcdd9-713">In un secondo momento, quando si aumenteranno le prestazioni per ottenere maggiore potenza di calcolo, il data warehouse potrà eseguire più query simultanee per impostazione predefinita, in quanto l'utente che esegue il caricamento non utilizza più memoria.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-713">Later, when scaling up to get more computational power, the data warehouse will be able to run more concurrent queries out-of-the-box, as the load user does not consume more memory.</span></span>
2.  <span data-ttu-id="dcdd9-714">Se si prevedono caricamenti di entità più grande in alcune occasioni, una classe di risorse dinamica è una scelta appropriata.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-714">If the expectations are bigger loads in some occasions, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="dcdd9-715">In un secondo momento, quando si aumenteranno le prestazioni per ottenere maggiore potenza di calcolo, l'utente che esegue il caricamento riceverà più memoria per impostazione predefinita, pertanto i tempi di caricamento saranno più rapidi.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-715">Later, when scaling up to get more computational power, the load user will get more memory out-of-the-box, hence allowing the load to perform faster.</span></span>

<span data-ttu-id="dcdd9-716">La memoria necessaria per elaborare in modo efficiente i caricamenti dipende dalla natura della tabella caricata e dalla quantità di dati elaborati.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-716">The memory needed to process loads efficiently depends on the nature of the table loaded and the amount of data processed.</span></span> <span data-ttu-id="dcdd9-717">Ad esempio, il caricamento di dati nelle tabelle CCI richiede una determinata quantità di memoria per consentire l'ottimizzazione per i rowgroup CCI.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-717">For instance, loading data into CCI tables requires some memory to let CCI rowgroups reach optimality.</span></span> <span data-ttu-id="dcdd9-718">Per altre informazioni, vedere le indicazioni relative a indici columnstore e caricamento di dati.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-718">For more details, see the Columnstore indexes - data loading guidance.</span></span>

<span data-ttu-id="dcdd9-719">Come procedura consigliata, si consiglia di usare almeno 200 MB di memoria per i caricamenti.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-719">As a best practice, we advise you to use at least 200MB of memory for loads.</span></span>

### <a name="querying-best-practices"></a><span data-ttu-id="dcdd9-720">Procedure consigliate per le query</span><span class="sxs-lookup"><span data-stu-id="dcdd9-720">Querying best practices</span></span>
<span data-ttu-id="dcdd9-721">Le query hanno diversi requisiti a seconda della complessità.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-721">Queries have different requirements depending on their complexity.</span></span> <span data-ttu-id="dcdd9-722">L'aumento della memoria per ogni query o l'aumento della concorrenza sono entrambi metodi validi per aumentare la velocità effettiva globale a seconda delle esigenze di query.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-722">Increasing memory per query or increasing the concurrency are both valid ways to augment overall throughput depending on the query needs.</span></span>
1.  <span data-ttu-id="dcdd9-723">Se si prevedono query regolari complesse (ad esempio per generare report giornalieri e settimanali) e non è necessario sfruttare la concorrenza, una classe di risorse dinamica è una scelta appropriata.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-723">If the expectations are regular, complex queries (for instance, to generate daily and weekly reports) and do not need to take advantage of concurrency, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="dcdd9-724">Se il sistema ha più dati da elaborare, un aumento delle prestazioni del data warehouse fornisce automaticamente più memoria per l'utente che esegue la query.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-724">If the system has more data to process, scaling up the data warehouse will therefore automatically provide more memory to the user running the query.</span></span>
2.  <span data-ttu-id="dcdd9-725">Se si prevedono modelli di concorrenza variabili o giornalieri (ad esempio se vengono eseguite query sul database tramite un'interfaccia utente Web accessibile su vasta scala), una classe di risorse statica è una scelta appropriata.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-725">If the expectations are variable or diurnal concurrency patterns (for instance if the database is queried through a web UI broadly accessible), a static resource class is a good choice.</span></span> <span data-ttu-id="dcdd9-726">In un secondo momento, quando si aumenteranno le prestazioni del data warehouse, l'utente associato alla classe di risorse statica potrà eseguire automaticamente un numero maggiore di query simultanee.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-726">Later, when scaling up to data warehouse, the user associated with the static resource class will automatically be able to run more concurrent queries.</span></span>

<span data-ttu-id="dcdd9-727">La selezione di una concessione di memoria appropriata a seconda delle esigenze della query non è semplice, perché dipende da molti fattori, come la quantità di dati sottoposti a query, la natura degli schemi di tabella e i vari predicati di gruppo, selezione e join.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-727">Selecting proper memory grant depending on the need of your query is non-trivial, as it depends on many factors, such as the amount of data queried, the nature of the table schemas, and various join, selection, and group predicates.</span></span> <span data-ttu-id="dcdd9-728">Dal punto di vista generale, l'allocazione di più memoria consente tempi più rapidi per il completamento delle query, ma riduce la concorrenza complessiva.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-728">From a general standpoint, allocating more memory will allow queries to complete faster, but would reduce the overall concurrency.</span></span> <span data-ttu-id="dcdd9-729">Se la concorrenza non è un problema, un'allocazione eccessiva di memoria non causa alcun danno.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-729">If concurrency is not an issue, over-allocating memory does not harm.</span></span> <span data-ttu-id="dcdd9-730">Per ottimizzare la velocità effettiva, potrebbe essere necessario provare diversi tipi di classi di risorse.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-730">To fine-tune throughput, trying various flavors of resource classes may be required.</span></span>

<span data-ttu-id="dcdd9-731">È possibile usare la stored procedure seguente per ottenere informazioni sulla concorrenza e sulla concessione di memoria per ogni classe di risorse in un determinato SLO e sulla classe di risorse migliore possibile per operazioni CCI a elevato utilizzo di memoria su una tabella CCI non partizionata con una classe di risorse specifica:</span><span class="sxs-lookup"><span data-stu-id="dcdd9-731">You can use the following stored procedure to figure out concurrency and memory grant per resource class at a given SLO and the closest best resource class for memory intensive CCI operations on non-partitioned CCI table at a given resource class:</span></span>

#### <a name="description"></a><span data-ttu-id="dcdd9-732">Descrizione:</span><span class="sxs-lookup"><span data-stu-id="dcdd9-732">Description:</span></span>  
<span data-ttu-id="dcdd9-733">Ecco lo scopo della stored procedure:</span><span class="sxs-lookup"><span data-stu-id="dcdd9-733">Here's the purpose of this stored procedure:</span></span>  
1. <span data-ttu-id="dcdd9-734">Aiutare l'utente a ottenere informazioni sulla concorrenza e sulla concessione di memoria per ogni classe di risorse in un determinato SLO.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-734">To help user figure out concurrency and memory grant per resource class at a given SLO.</span></span> <span data-ttu-id="dcdd9-735">L'utente deve specificare NULL sia per lo schema che per il nome di tabella, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-735">User needs to provide NULL for both schema and tablename for this as shown in the example below.</span></span>  
2. <span data-ttu-id="dcdd9-736">Aiutare l'utente a ottenere informazioni sulla classe di risorse migliore possibile per operazioni CCI a elevato utilizzo di memoria (caricamento, copia di tabelle, ricompilazione dell'indice e così via) su una tabella CCI non partizionata con una classe di risorse specifica.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-736">To help user figure out the closest best resource class for the memory intensed CCI operations (load, copy table, rebuild index, etc.) on non partitioned CCI table at a given resource class.</span></span> <span data-ttu-id="dcdd9-737">La stored procedure usa lo schema di tabella per individuare la concessione di memoria necessaria.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-737">The stored proc uses table schema to find out the required memory grant for this.</span></span>

#### <a name="dependencies--restrictions"></a><span data-ttu-id="dcdd9-738">Dipendenze e restrizioni:</span><span class="sxs-lookup"><span data-stu-id="dcdd9-738">Dependencies & Restrictions:</span></span>
- <span data-ttu-id="dcdd9-739">Questa stored procedure non è progettata per calcolare i requisiti di memoria per una tabella CCI partizionata.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-739">This stored proc is not designed to calculate memory requirement for partitioned-cci table.</span></span>    
- <span data-ttu-id="dcdd9-740">Questa stored procedure non prende in considerazione i requisiti di memoria per la parte SELECT di un'istruzione CTAS/INSERT-SELECT e presuppone che si tratti di un'istruzione SELECT semplice.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-740">This stored proc doesn't take memory requirement into account for the SELECT part of CTAS/INSERT-SELECT and assumes it to be a simple SELECT.</span></span>
- <span data-ttu-id="dcdd9-741">Questa stored procedure usa una tabella temporanea che quindi può essere usata nella sessione in cui è stata creata la stored procedure.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-741">This stored proc uses a temp table so this can be used in the session where this stored proc was created.</span></span>    
- <span data-ttu-id="dcdd9-742">Questa stored procedure dipende dalle risorse correnti (ad esempio, configurazione hardware e configurazione DMS) e in caso di modifiche non funziona più correttamente.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-742">This stored proc depends on the current offerings (e.g. hardware configuration, DMS config) and if any of that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="dcdd9-743">Questa stored procedure dipende dal limite di concorrenza esistente e in caso di modifiche non funziona più correttamente.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-743">This stored proc depends on existing offered concurrency limit and if that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="dcdd9-744">Questa stored procedure dipende dalle classi di risorse esistenti e in caso di modifiche non funziona più correttamente.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-744">This stored proc depends on existing resource class offerings and if that changes then this stored proc wuold not work correctly.</span></span>  

>  [!NOTE]  
>  <span data-ttu-id="dcdd9-745">Se non si ottiene alcun output dopo l'esecuzione della stored procedure con i parametri forniti, i motivi potrebbero essere due.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-745">If you are not getting output after executing stored procedure with parameters provided then there could be two cases.</span></span> <br /><span data-ttu-id="dcdd9-746">1. Uno dei parametri di Data Warehouse contiene un valore SLO non valido</span><span class="sxs-lookup"><span data-stu-id="dcdd9-746">1. Either DW Parameter contains invalid SLO value</span></span> <br /><span data-ttu-id="dcdd9-747">2. OPPURE non ci sono classi di risorse corrispondenti per l'operazione CCI se è stato fornito il nome della tabella.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-747">2. OR there are no matching resource class for CCI operation if table name was provided.</span></span> <br /><span data-ttu-id="dcdd9-748">Ad esempio, con DW100, la concessione di memoria massima disponibile è 400 MB e lo schema di tabella è sufficientemente ampio per soddisfare il requisito di 400 MB.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-748">For example, at DW100, highest memory grant available is 400MB and if table schema is wide enough to cross the requirement of 400MB.</span></span>
      
#### <a name="usage-example"></a><span data-ttu-id="dcdd9-749">Esempio d'uso:</span><span class="sxs-lookup"><span data-stu-id="dcdd9-749">Usage example:</span></span>
<span data-ttu-id="dcdd9-750">Sintassi:</span><span class="sxs-lookup"><span data-stu-id="dcdd9-750">Syntax:</span></span>  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. <span data-ttu-id="dcdd9-751">@DWU: Fornire un parametro NULL per estrarre la DWU corrente dal database di Data Warehouse oppure fornire una DWU supportata nel formato "DW100"</span><span class="sxs-lookup"><span data-stu-id="dcdd9-751">@DWU: Either provide a NULL parameter to extract the current DWU from the DW DB or provide any supported DWU in the form of 'DW100'</span></span>
2. <span data-ttu-id="dcdd9-752">@SCHEMA_NAME: Fornire un nome di schema della tabella</span><span class="sxs-lookup"><span data-stu-id="dcdd9-752">@SCHEMA_NAME: Provide a schema name of the table</span></span>
3. <span data-ttu-id="dcdd9-753">@TABLE_NAME: Fornire un nome di tabella</span><span class="sxs-lookup"><span data-stu-id="dcdd9-753">@TABLE_NAME: Provide a table name of the interest</span></span>

<span data-ttu-id="dcdd9-754">Esempi di esecuzione di questa stored procedure:</span><span class="sxs-lookup"><span data-stu-id="dcdd9-754">Examples executing this stored proc:</span></span>  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

<span data-ttu-id="dcdd9-755">La tabella Table1 usata negli esempi precedenti può venire creata come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="dcdd9-755">Table1 used in the above examples could be created as below:</span></span>  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-the-stored-procedure-definition"></a><span data-ttu-id="dcdd9-756">Ecco la definizione della stored procedure:</span><span class="sxs-lookup"><span data-stu-id="dcdd9-756">Here's the stored procedure definition:</span></span>
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
-- Selecting proper DWU for the current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need to supply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) to hold mapping info.
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
-- Creating workload mapping to their corresponding slot consumption and default memory grant.
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

## <a name="query-importance"></a><span data-ttu-id="dcdd9-757">Priorità delle query</span><span class="sxs-lookup"><span data-stu-id="dcdd9-757">Query importance</span></span>
<span data-ttu-id="dcdd9-758">SQL Data Warehouse implementa le classi di risorse utilizzando i gruppi del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-758">SQL Data Warehouse implements resource classes by using workload groups.</span></span> <span data-ttu-id="dcdd9-759">Esistono in totale otto gruppi di carichi di lavoro che controllano il comportamento delle classi di risorse nelle DWU di varie dimensioni.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-759">There are a total of eight workload groups that control the behavior of the resource classes across the various DWU sizes.</span></span> <span data-ttu-id="dcdd9-760">Per qualsiasi DWU, SQL Data Warehouse usa solo quattro degli otto gruppi del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-760">For any DWU, SQL Data Warehouse uses only four of the eight workload groups.</span></span> <span data-ttu-id="dcdd9-761">Il senso di questo approccio è assegnare a ogni gruppo di carichi di lavoro una delle quattro classi di risorse, tra smallrc, mediumrc, largerc o xlargerc.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-761">This makes sense because each workload group is assigned to one of four resource classes: smallrc, mediumrc, largerc, or xlargerc.</span></span> <span data-ttu-id="dcdd9-762">È importante comprendere per alcuni gruppi di carichi di lavoro viene impostato il livello di *priorità*più elevato.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-762">The importance of understanding the workload groups is that some of these workload groups are set to higher *importance*.</span></span> <span data-ttu-id="dcdd9-763">La priorità viene usata per la pianificazione della CPU.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-763">Importance is used for CPU scheduling.</span></span> <span data-ttu-id="dcdd9-764">Le query eseguite con priorità alta otterranno tre volte più cicli della CPU rispetto a quelle con priorità media.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-764">Queries run with high importance will get three times more CPU cycles than those with medium importance.</span></span> <span data-ttu-id="dcdd9-765">Di conseguenza, i mapping degli slot della concorrenza determinano anche la priorità della CPU.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-765">Therefore, concurrency slot mappings also determine CPU priority.</span></span> <span data-ttu-id="dcdd9-766">Quando una query utilizza 16 o più slot, viene eseguita con priorità alta.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-766">When a query consumes 16 or more slots, it runs as high importance.</span></span>

<span data-ttu-id="dcdd9-767">Nella tabella seguente vengono riportati i mapping di priorità per ogni gruppo di carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-767">The following table shows the importance mappings for each workload group.</span></span>

### <a name="workload-group-mappings-to-concurrency-slots-and-importance"></a><span data-ttu-id="dcdd9-768">Mapping dei gruppi di carichi di lavoro agli slot di concorrenza e relativa importanza</span><span class="sxs-lookup"><span data-stu-id="dcdd9-768">Workload group mappings to concurrency slots and importance</span></span>
| <span data-ttu-id="dcdd9-769">Gruppi di carichi di lavoro</span><span class="sxs-lookup"><span data-stu-id="dcdd9-769">Workload groups</span></span> | <span data-ttu-id="dcdd9-770">Mapping degli slot di concorrenza</span><span class="sxs-lookup"><span data-stu-id="dcdd9-770">Concurrency slot mapping</span></span> | <span data-ttu-id="dcdd9-771">MB/Distribuzione</span><span class="sxs-lookup"><span data-stu-id="dcdd9-771">MB / Distribution</span></span> | <span data-ttu-id="dcdd9-772">Mapping delle priorità</span><span class="sxs-lookup"><span data-stu-id="dcdd9-772">Importance mapping</span></span> |
|:--- |:---:|:---:|:--- |
| <span data-ttu-id="dcdd9-773">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="dcdd9-773">SloDWGroupC00</span></span> |<span data-ttu-id="dcdd9-774">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-774">1</span></span> |<span data-ttu-id="dcdd9-775">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-775">100</span></span> |<span data-ttu-id="dcdd9-776">Media</span><span class="sxs-lookup"><span data-stu-id="dcdd9-776">Medium</span></span> |
| <span data-ttu-id="dcdd9-777">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="dcdd9-777">SloDWGroupC01</span></span> |<span data-ttu-id="dcdd9-778">2</span><span class="sxs-lookup"><span data-stu-id="dcdd9-778">2</span></span> |<span data-ttu-id="dcdd9-779">200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-779">200</span></span> |<span data-ttu-id="dcdd9-780">Media</span><span class="sxs-lookup"><span data-stu-id="dcdd9-780">Medium</span></span> |
| <span data-ttu-id="dcdd9-781">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="dcdd9-781">SloDWGroupC02</span></span> |<span data-ttu-id="dcdd9-782">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-782">4</span></span> |<span data-ttu-id="dcdd9-783">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-783">400</span></span> |<span data-ttu-id="dcdd9-784">Media</span><span class="sxs-lookup"><span data-stu-id="dcdd9-784">Medium</span></span> |
| <span data-ttu-id="dcdd9-785">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="dcdd9-785">SloDWGroupC03</span></span> |<span data-ttu-id="dcdd9-786">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-786">8</span></span> |<span data-ttu-id="dcdd9-787">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-787">800</span></span> |<span data-ttu-id="dcdd9-788">Media</span><span class="sxs-lookup"><span data-stu-id="dcdd9-788">Medium</span></span> |
| <span data-ttu-id="dcdd9-789">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="dcdd9-789">SloDWGroupC04</span></span> |<span data-ttu-id="dcdd9-790">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-790">16</span></span> |<span data-ttu-id="dcdd9-791">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-791">1,600</span></span> |<span data-ttu-id="dcdd9-792">Alto</span><span class="sxs-lookup"><span data-stu-id="dcdd9-792">High</span></span> |
| <span data-ttu-id="dcdd9-793">SloDWGroupC05</span><span class="sxs-lookup"><span data-stu-id="dcdd9-793">SloDWGroupC05</span></span> |<span data-ttu-id="dcdd9-794">32</span><span class="sxs-lookup"><span data-stu-id="dcdd9-794">32</span></span> |<span data-ttu-id="dcdd9-795">3.200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-795">3,200</span></span> |<span data-ttu-id="dcdd9-796">Alto</span><span class="sxs-lookup"><span data-stu-id="dcdd9-796">High</span></span> |
| <span data-ttu-id="dcdd9-797">SloDWGroupC06</span><span class="sxs-lookup"><span data-stu-id="dcdd9-797">SloDWGroupC06</span></span> |<span data-ttu-id="dcdd9-798">64</span><span class="sxs-lookup"><span data-stu-id="dcdd9-798">64</span></span> |<span data-ttu-id="dcdd9-799">6.400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-799">6,400</span></span> |<span data-ttu-id="dcdd9-800">Alto</span><span class="sxs-lookup"><span data-stu-id="dcdd9-800">High</span></span> |
| <span data-ttu-id="dcdd9-801">SloDWGroupC07</span><span class="sxs-lookup"><span data-stu-id="dcdd9-801">SloDWGroupC07</span></span> |<span data-ttu-id="dcdd9-802">128</span><span class="sxs-lookup"><span data-stu-id="dcdd9-802">128</span></span> |<span data-ttu-id="dcdd9-803">12.800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-803">12,800</span></span> |<span data-ttu-id="dcdd9-804">Alto</span><span class="sxs-lookup"><span data-stu-id="dcdd9-804">High</span></span> |

<span data-ttu-id="dcdd9-805">Come illustrato nel grafico **Allocation and consumption of concurrency slots** (Allocazione e utilizzo degli slot di concorrenza), DW500 utilizza 1, 4, 8 o 16 slot di concorrenza per smallrc, mediumrc, largerc e xlargerc rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-805">From the **Allocation and consumption of concurrency slots** chart, you can see that a DW500 uses 1, 4, 8 or 16 concurrency slots for smallrc, mediumrc, largerc, and xlargerc, respectively.</span></span> <span data-ttu-id="dcdd9-806">È possibile cercare questi valori nel grafico precedente per identificare la priorità di ciascuna classe di risorse.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-806">You can look those values up in the preceding chart to find the importance for each resource class.</span></span>

### <a name="dw500-mapping-of-resource-classes-to-importance"></a><span data-ttu-id="dcdd9-807">Mapping dell'importanza delle classi di risorse in DW500</span><span class="sxs-lookup"><span data-stu-id="dcdd9-807">DW500 mapping of resource classes to importance</span></span>
| <span data-ttu-id="dcdd9-808">classe di risorse</span><span class="sxs-lookup"><span data-stu-id="dcdd9-808">Resource class</span></span> | <span data-ttu-id="dcdd9-809">Gruppo del carico di lavoro</span><span class="sxs-lookup"><span data-stu-id="dcdd9-809">Workload group</span></span> | <span data-ttu-id="dcdd9-810">Numero di slot di concorrenza usati</span><span class="sxs-lookup"><span data-stu-id="dcdd9-810">Concurrency slots used</span></span> | <span data-ttu-id="dcdd9-811">MB/Distribuzione</span><span class="sxs-lookup"><span data-stu-id="dcdd9-811">MB / Distribution</span></span> | <span data-ttu-id="dcdd9-812">priorità</span><span class="sxs-lookup"><span data-stu-id="dcdd9-812">Importance</span></span> |
|:--- |:--- |:---:|:---:|:--- |
| <span data-ttu-id="dcdd9-813">smallrc</span><span class="sxs-lookup"><span data-stu-id="dcdd9-813">smallrc</span></span> |<span data-ttu-id="dcdd9-814">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="dcdd9-814">SloDWGroupC00</span></span> |<span data-ttu-id="dcdd9-815">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-815">1</span></span> |<span data-ttu-id="dcdd9-816">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-816">100</span></span> |<span data-ttu-id="dcdd9-817">Media</span><span class="sxs-lookup"><span data-stu-id="dcdd9-817">Medium</span></span> |
| <span data-ttu-id="dcdd9-818">mediumrc</span><span class="sxs-lookup"><span data-stu-id="dcdd9-818">mediumrc</span></span> |<span data-ttu-id="dcdd9-819">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="dcdd9-819">SloDWGroupC02</span></span> |<span data-ttu-id="dcdd9-820">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-820">4</span></span> |<span data-ttu-id="dcdd9-821">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-821">400</span></span> |<span data-ttu-id="dcdd9-822">Media</span><span class="sxs-lookup"><span data-stu-id="dcdd9-822">Medium</span></span> |
| <span data-ttu-id="dcdd9-823">largerc</span><span class="sxs-lookup"><span data-stu-id="dcdd9-823">largerc</span></span> |<span data-ttu-id="dcdd9-824">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="dcdd9-824">SloDWGroupC03</span></span> |<span data-ttu-id="dcdd9-825">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-825">8</span></span> |<span data-ttu-id="dcdd9-826">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-826">800</span></span> |<span data-ttu-id="dcdd9-827">Media</span><span class="sxs-lookup"><span data-stu-id="dcdd9-827">Medium</span></span> |
| <span data-ttu-id="dcdd9-828">xlargerc</span><span class="sxs-lookup"><span data-stu-id="dcdd9-828">xlargerc</span></span> |<span data-ttu-id="dcdd9-829">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="dcdd9-829">SloDWGroupC04</span></span> |<span data-ttu-id="dcdd9-830">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-830">16</span></span> |<span data-ttu-id="dcdd9-831">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-831">1,600</span></span> |<span data-ttu-id="dcdd9-832">Alto</span><span class="sxs-lookup"><span data-stu-id="dcdd9-832">High</span></span> |
| <span data-ttu-id="dcdd9-833">staticrc10</span><span class="sxs-lookup"><span data-stu-id="dcdd9-833">staticrc10</span></span> |<span data-ttu-id="dcdd9-834">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="dcdd9-834">SloDWGroupC00</span></span> |<span data-ttu-id="dcdd9-835">1</span><span class="sxs-lookup"><span data-stu-id="dcdd9-835">1</span></span> |<span data-ttu-id="dcdd9-836">100</span><span class="sxs-lookup"><span data-stu-id="dcdd9-836">100</span></span> |<span data-ttu-id="dcdd9-837">Media</span><span class="sxs-lookup"><span data-stu-id="dcdd9-837">Medium</span></span> |
| <span data-ttu-id="dcdd9-838">staticrc20</span><span class="sxs-lookup"><span data-stu-id="dcdd9-838">staticrc20</span></span> |<span data-ttu-id="dcdd9-839">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="dcdd9-839">SloDWGroupC01</span></span> |<span data-ttu-id="dcdd9-840">2</span><span class="sxs-lookup"><span data-stu-id="dcdd9-840">2</span></span> |<span data-ttu-id="dcdd9-841">200</span><span class="sxs-lookup"><span data-stu-id="dcdd9-841">200</span></span> |<span data-ttu-id="dcdd9-842">Media</span><span class="sxs-lookup"><span data-stu-id="dcdd9-842">Medium</span></span> |
| <span data-ttu-id="dcdd9-843">staticrc30</span><span class="sxs-lookup"><span data-stu-id="dcdd9-843">staticrc30</span></span> |<span data-ttu-id="dcdd9-844">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="dcdd9-844">SloDWGroupC02</span></span> |<span data-ttu-id="dcdd9-845">4</span><span class="sxs-lookup"><span data-stu-id="dcdd9-845">4</span></span> |<span data-ttu-id="dcdd9-846">400</span><span class="sxs-lookup"><span data-stu-id="dcdd9-846">400</span></span> |<span data-ttu-id="dcdd9-847">Media</span><span class="sxs-lookup"><span data-stu-id="dcdd9-847">Medium</span></span> |
| <span data-ttu-id="dcdd9-848">staticrc40</span><span class="sxs-lookup"><span data-stu-id="dcdd9-848">staticrc40</span></span> |<span data-ttu-id="dcdd9-849">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="dcdd9-849">SloDWGroupC03</span></span> |<span data-ttu-id="dcdd9-850">8</span><span class="sxs-lookup"><span data-stu-id="dcdd9-850">8</span></span> |<span data-ttu-id="dcdd9-851">800</span><span class="sxs-lookup"><span data-stu-id="dcdd9-851">800</span></span> |<span data-ttu-id="dcdd9-852">Media</span><span class="sxs-lookup"><span data-stu-id="dcdd9-852">Medium</span></span> |
| <span data-ttu-id="dcdd9-853">staticrc50</span><span class="sxs-lookup"><span data-stu-id="dcdd9-853">staticrc50</span></span> |<span data-ttu-id="dcdd9-854">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="dcdd9-854">SloDWGroupC03</span></span> |<span data-ttu-id="dcdd9-855">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-855">16</span></span> |<span data-ttu-id="dcdd9-856">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-856">1,600</span></span> |<span data-ttu-id="dcdd9-857">Alto</span><span class="sxs-lookup"><span data-stu-id="dcdd9-857">High</span></span> |
| <span data-ttu-id="dcdd9-858">staticrc60</span><span class="sxs-lookup"><span data-stu-id="dcdd9-858">staticrc60</span></span> |<span data-ttu-id="dcdd9-859">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="dcdd9-859">SloDWGroupC03</span></span> |<span data-ttu-id="dcdd9-860">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-860">16</span></span> |<span data-ttu-id="dcdd9-861">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-861">1,600</span></span> |<span data-ttu-id="dcdd9-862">Alto</span><span class="sxs-lookup"><span data-stu-id="dcdd9-862">High</span></span> |
| <span data-ttu-id="dcdd9-863">staticrc70</span><span class="sxs-lookup"><span data-stu-id="dcdd9-863">staticrc70</span></span> |<span data-ttu-id="dcdd9-864">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="dcdd9-864">SloDWGroupC03</span></span> |<span data-ttu-id="dcdd9-865">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-865">16</span></span> |<span data-ttu-id="dcdd9-866">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-866">1,600</span></span> |<span data-ttu-id="dcdd9-867">Alto</span><span class="sxs-lookup"><span data-stu-id="dcdd9-867">High</span></span> |
| <span data-ttu-id="dcdd9-868">staticrc80</span><span class="sxs-lookup"><span data-stu-id="dcdd9-868">staticrc80</span></span> |<span data-ttu-id="dcdd9-869">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="dcdd9-869">SloDWGroupC03</span></span> |<span data-ttu-id="dcdd9-870">16</span><span class="sxs-lookup"><span data-stu-id="dcdd9-870">16</span></span> |<span data-ttu-id="dcdd9-871">1.600</span><span class="sxs-lookup"><span data-stu-id="dcdd9-871">1,600</span></span> |<span data-ttu-id="dcdd9-872">Alto</span><span class="sxs-lookup"><span data-stu-id="dcdd9-872">High</span></span> |

<span data-ttu-id="dcdd9-873">Per esaminare in dettaglio le differenze nell'allocazione delle risorse di memoria dal punto di vista di resource governor o per analizzare l'utilizzo attivo e cronologico dei gruppi di carichi di lavoro in caso di risoluzione dei problemi, è possibile usare la query DMV seguente:</span><span class="sxs-lookup"><span data-stu-id="dcdd9-873">You can use the following DMV query to look at the differences in memory resource allocation in detail from the perspective of the resource governor, or to analyze active and historic usage of the workload groups when troubleshooting.</span></span>

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

## <a name="queries-that-honor-concurrency-limits"></a><span data-ttu-id="dcdd9-874">Query che rispettano i limiti di concorrenza</span><span class="sxs-lookup"><span data-stu-id="dcdd9-874">Queries that honor concurrency limits</span></span>
<span data-ttu-id="dcdd9-875">La maggior parte delle query è regolata da classi di risorse.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-875">Most queries are governed by resource classes.</span></span> <span data-ttu-id="dcdd9-876">Queste query devono rientrare in entrambe le soglie delle query simultanee e degli slot di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-876">These queries must fit inside both the concurrent query and concurrency slot thresholds.</span></span> <span data-ttu-id="dcdd9-877">Un utente può scegliere di escludere una query dal modello di slot di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-877">A user cannot choose to exclude a query from the concurrency slot model.</span></span>

<span data-ttu-id="dcdd9-878">Le istruzioni seguenti rispettano le classi di risorse:</span><span class="sxs-lookup"><span data-stu-id="dcdd9-878">To reiterate, the following statements honor resource classes:</span></span>

* <span data-ttu-id="dcdd9-879">INSERT SELECT</span><span class="sxs-lookup"><span data-stu-id="dcdd9-879">INSERT-SELECT</span></span>
* <span data-ttu-id="dcdd9-880">AGGIORNAMENTO</span><span class="sxs-lookup"><span data-stu-id="dcdd9-880">UPDATE</span></span>
* <span data-ttu-id="dcdd9-881">DELETE</span><span class="sxs-lookup"><span data-stu-id="dcdd9-881">DELETE</span></span>
* <span data-ttu-id="dcdd9-882">SELEZIONARE (quando si esegue una query sulle tabelle utente)</span><span class="sxs-lookup"><span data-stu-id="dcdd9-882">SELECT (when querying user tables)</span></span>
* <span data-ttu-id="dcdd9-883">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="dcdd9-883">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="dcdd9-884">ALTER INDEX REORGANIZE</span><span class="sxs-lookup"><span data-stu-id="dcdd9-884">ALTER INDEX REORGANIZE</span></span>
* <span data-ttu-id="dcdd9-885">MODIFICA TABELLA RICOMPILAZIONE</span><span class="sxs-lookup"><span data-stu-id="dcdd9-885">ALTER TABLE REBUILD</span></span>
* <span data-ttu-id="dcdd9-886">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="dcdd9-886">CREATE INDEX</span></span>
* <span data-ttu-id="dcdd9-887">CREARE L'INDICE COLUMNSTORE CLUSTER</span><span class="sxs-lookup"><span data-stu-id="dcdd9-887">CREATE CLUSTERED COLUMNSTORE INDEX</span></span>
* <span data-ttu-id="dcdd9-888">CREATE TABLE AS SELECT (CTAS)</span><span class="sxs-lookup"><span data-stu-id="dcdd9-888">CREATE TABLE AS SELECT (CTAS)</span></span>
* <span data-ttu-id="dcdd9-889">Caricamento dei dati</span><span class="sxs-lookup"><span data-stu-id="dcdd9-889">Data loading</span></span>
* <span data-ttu-id="dcdd9-890">Operazioni di spostamento dati condotte dal Servizio di spostamento dati (DMS)</span><span class="sxs-lookup"><span data-stu-id="dcdd9-890">Data movement operations conducted by the Data Movement Service (DMS)</span></span>

## <a name="query-exceptions-to-concurrency-limits"></a><span data-ttu-id="dcdd9-891">Eccezioni query ai limiti di concorrenza</span><span class="sxs-lookup"><span data-stu-id="dcdd9-891">Query exceptions to concurrency limits</span></span>
<span data-ttu-id="dcdd9-892">Alcune query non rispettano la classe di risorse alla quale è assegnato l'utente.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-892">Some queries do not honor the resource class to which the user is assigned.</span></span> <span data-ttu-id="dcdd9-893">Queste eccezioni ai limiti di concorrenza vengono effettuate quando le risorse di memoria necessarie per un particolare comando sono basse, spesso perché il comando è un'operazione dei metadati.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-893">These exceptions to the concurrency limits are made when the memory resources needed for a particular command are low, often because the command is a metadata operation.</span></span> <span data-ttu-id="dcdd9-894">Con queste eccezioni, si intende evitare l'allocazione di più memoria alle query che non ne hanno bisogno.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-894">The goal of these exceptions is to avoid larger memory allocations for queries that will never need them.</span></span> <span data-ttu-id="dcdd9-895">In questi casi, viene sempre usata la classe di risorse piccola predefinita (smallrc), indipendentemente dalla classe di risorse effettivamente assegnata all'utente.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-895">In these cases, the default small resource class (smallrc) is always used regardless of the actual resource class assigned to the user.</span></span> <span data-ttu-id="dcdd9-896">Ad esempio, in smallrc verrà sempre eseguita `CREATE LOGIN` .</span><span class="sxs-lookup"><span data-stu-id="dcdd9-896">For example, `CREATE LOGIN` will always run in smallrc.</span></span> <span data-ttu-id="dcdd9-897">Le risorse necessarie per svolgere questa operazione sono molto ridotte e non avrebbe senso includere la query nel modello di slot di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-897">The resources required to fulfill this operation are very low, so it does not make sense to include the query in the concurrency slot model.</span></span>  <span data-ttu-id="dcdd9-898">Per queste query non è previsto il limite di 32 utenti simultanei; è possibile eseguire un numero illimitato di queste query fino al limite di 1.024 sessioni.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-898">These queries are also not limited by the 32 user concurrency limit, an unlimited number of these queries can run up to the session limit of 1,024 sessions.</span></span>

<span data-ttu-id="dcdd9-899">Le istruzioni seguenti non rispettano le classi di risorse:</span><span class="sxs-lookup"><span data-stu-id="dcdd9-899">The following statements do not honor resource classes:</span></span>

* <span data-ttu-id="dcdd9-900">CREATE o DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="dcdd9-900">CREATE or DROP TABLE</span></span>
* <span data-ttu-id="dcdd9-901">ALTER TABLE... SWITCH, SPLIT o MERGE PARTITION</span><span class="sxs-lookup"><span data-stu-id="dcdd9-901">ALTER TABLE ... SWITCH, SPLIT, or MERGE PARTITION</span></span>
* <span data-ttu-id="dcdd9-902">ALTER INDEX DISABLE</span><span class="sxs-lookup"><span data-stu-id="dcdd9-902">ALTER INDEX DISABLE</span></span>
* <span data-ttu-id="dcdd9-903">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="dcdd9-903">DROP INDEX</span></span>
* <span data-ttu-id="dcdd9-904">CREATE, UPDATE o DROP STATISTICS</span><span class="sxs-lookup"><span data-stu-id="dcdd9-904">CREATE, UPDATE, or DROP STATISTICS</span></span>
* <span data-ttu-id="dcdd9-905">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="dcdd9-905">TRUNCATE TABLE</span></span>
* <span data-ttu-id="dcdd9-906">ALTER AUTHORIZATION</span><span class="sxs-lookup"><span data-stu-id="dcdd9-906">ALTER AUTHORIZATION</span></span>
* <span data-ttu-id="dcdd9-907">CREATE LOGIN</span><span class="sxs-lookup"><span data-stu-id="dcdd9-907">CREATE LOGIN</span></span>
* <span data-ttu-id="dcdd9-908">CREATE, ALTER o DROP USER</span><span class="sxs-lookup"><span data-stu-id="dcdd9-908">CREATE, ALTER or DROP USER</span></span>
* <span data-ttu-id="dcdd9-909">CREATE, ALTER o DROP PROCEDURE</span><span class="sxs-lookup"><span data-stu-id="dcdd9-909">CREATE, ALTER or DROP PROCEDURE</span></span>
* <span data-ttu-id="dcdd9-910">CREATE o DROP VIEW</span><span class="sxs-lookup"><span data-stu-id="dcdd9-910">CREATE or DROP VIEW</span></span>
* <span data-ttu-id="dcdd9-911">INSERT VALUES</span><span class="sxs-lookup"><span data-stu-id="dcdd9-911">INSERT VALUES</span></span>
* <span data-ttu-id="dcdd9-912">SELECT da viste di sistema e DMV</span><span class="sxs-lookup"><span data-stu-id="dcdd9-912">SELECT from system views and DMVs</span></span>
* <span data-ttu-id="dcdd9-913">EXPLAIN</span><span class="sxs-lookup"><span data-stu-id="dcdd9-913">EXPLAIN</span></span>
* <span data-ttu-id="dcdd9-914">DBCC</span><span class="sxs-lookup"><span data-stu-id="dcdd9-914">DBCC</span></span>

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <span data-ttu-id="dcdd9-915"><a name="changing-user-resource-class-example"></a> Esempio di modifica della classe di risorse di un utente</span><span class="sxs-lookup"><span data-stu-id="dcdd9-915"><a name="changing-user-resource-class-example"></a> Change a user resource class example</span></span>
1. <span data-ttu-id="dcdd9-916">**Creare un account di accesso:** aprire una connessione al database **master** nel server SQL che ospita il database SQL Data Warehouse ed eseguire i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-916">**Create login:** Open a connection to your **master** database on the SQL server hosting your SQL Data Warehouse database and execute the following commands.</span></span>
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > <span data-ttu-id="dcdd9-917">È consigliabile creare un utente nel database master per gli utenti di SQL Data Warehouse di Azure.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-917">It is a good idea to create a user in the master database for Azure SQL Data Warehouse users.</span></span> <span data-ttu-id="dcdd9-918">La creazione di un utente nel database master consente all'utente di accedere tramite strumenti come SSMS senza specificare un nome di database.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-918">Creating a user in master allows a user to login using tools like SSMS without specifying a database name.</span></span>  <span data-ttu-id="dcdd9-919">Consente inoltre di usare Esplora oggetti per visualizzare tutti i database in SQL server.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-919">It also allows them to use the object explorer to view all databases on a SQL server.</span></span>  <span data-ttu-id="dcdd9-920">Per altre informazioni su creazione e gestione degli utenti, vedere [Proteggere un database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="dcdd9-920">For more details about creating and managing users, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>
   > 
   > 
2. <span data-ttu-id="dcdd9-921">**Creare un utente di SQL Data Warehouse:** aprire una connessione al database di **SQL Data Warehouse** ed eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-921">**Create SQL Data Warehouse user:** Open a connection to the **SQL Data Warehouse** database and execute the following command.</span></span>
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. <span data-ttu-id="dcdd9-922">**Concedere le autorizzazioni:** nell'esempio seguente viene concessa l'autorizzazione `CONTROL` nel database **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-922">**Grant permissions:** The following example grants `CONTROL` on the **SQL Data Warehouse** database.</span></span> <span data-ttu-id="dcdd9-923">`CONTROL` a livello di database corrisponde a db_owner in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-923">`CONTROL` at the database level is the equivalent of db_owner in SQL Server.</span></span>
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW to newperson;
    ```
4. <span data-ttu-id="dcdd9-924">**Aumentare la classe di risorse:** per aggiungere un utente a un ruolo di gestione del carico di lavoro più elevato, usare la query seguente.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-924">**Increase resource class:** Use the following query to add a user to a higher workload management role.</span></span>
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. <span data-ttu-id="dcdd9-925">**Diminuire la classe di risorse:** per rimuovere un utente da un ruolo di gestione del carico di lavoro, usare la query seguente.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-925">**Decrease resource class:** Use the following query to remove a user from a workload management role.</span></span>
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="dcdd9-926">Non è possibile rimuovere un utente da smallrc.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-926">It is not possible to remove a user from smallrc.</span></span>
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a><span data-ttu-id="dcdd9-927">Rilevamento di query in coda e altre viste a gestione dinamica</span><span class="sxs-lookup"><span data-stu-id="dcdd9-927">Queued query detection and other DMVs</span></span>
<span data-ttu-id="dcdd9-928">È possibile utilizzare la DMV `sys.dm_pdw_exec_requests` per identificare le query in attesa in una coda di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-928">You can use the `sys.dm_pdw_exec_requests` DMV to identify queries that are waiting in a concurrency queue.</span></span> <span data-ttu-id="dcdd9-929">Le query in attesa di uno slot di concorrenza saranno in stato **sospeso**.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-929">Queries waiting for a concurrency slot will have a status of **suspended**.</span></span>

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

<span data-ttu-id="dcdd9-930">I ruoli di gestione del carico di lavoro possono essere visualizzati con `sys.database_principals`.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-930">Workload management roles can be viewed with `sys.database_principals`.</span></span>

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

<span data-ttu-id="dcdd9-931">La query seguente mostra il ruolo a cui è assegnato ogni utente.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-931">The following query shows which role each user is assigned to.</span></span>

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

<span data-ttu-id="dcdd9-932">SQL Data Warehouse prevede i tipi di attesa seguenti.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-932">SQL Data Warehouse has the following wait types:</span></span>

* <span data-ttu-id="dcdd9-933">**LocalQueriesConcurrencyResourceType**: query che si trovano all'esterno del framework di slot di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-933">**LocalQueriesConcurrencyResourceType**: Queries that sit outside of the concurrency slot framework.</span></span> <span data-ttu-id="dcdd9-934">Le query DMV e le funzioni di sistema  come `SELECT @@VERSION` sono esempi di query locali.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-934">DMV queries and system functions such as `SELECT @@VERSION` are examples of local queries.</span></span>
* <span data-ttu-id="dcdd9-935">**UserConcurrencyResourceType**: query che si trovano all'interno del framework di slot di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-935">**UserConcurrencyResourceType**: Queries that sit inside the concurrency slot framework.</span></span> <span data-ttu-id="dcdd9-936">Le query sulle tabelle dell'utente finale rappresentano esempi in cui si usa questo tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-936">Queries against end-user tables represent examples that would use this resource type.</span></span>
* <span data-ttu-id="dcdd9-937">**DmsConcurrencyResourceType**: attese risultanti dalle operazioni di spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-937">**DmsConcurrencyResourceType**: Waits resulting from data movement operations.</span></span>
* <span data-ttu-id="dcdd9-938">**BackupConcurrencyResourceType**: indica che è in esecuzione il backup di un database.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-938">**BackupConcurrencyResourceType**: This wait indicates that a database is being backed up.</span></span> <span data-ttu-id="dcdd9-939">Il valore massimo per questo tipo di risorsa è 1.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-939">The maximum value for this resource type is 1.</span></span> <span data-ttu-id="dcdd9-940">Se più copie di backup sono stati richieste contemporaneamente, le altre verranno accodate.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-940">If multiple backups have been requested at the same time, the others will queue.</span></span>

<span data-ttu-id="dcdd9-941">La DMV `sys.dm_pdw_waits` può essere usata per visualizzare le risorse per cui una richiesta è in attesa.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-941">The `sys.dm_pdw_waits` DMV can be used to see which resources a request is waiting for.</span></span>

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

<span data-ttu-id="dcdd9-942">La DMV `sys.dm_pdw_resource_waits` mostra solo le attese di risorse utilizzate da una determinata query.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-942">The `sys.dm_pdw_resource_waits` DMV shows only the resource waits consumed by a given query.</span></span> <span data-ttu-id="dcdd9-943">Il tempo in attesa delle risorse misura solo il tempo richiesto per fornire le risorse, a differenza del tempo di attesa del segnale che rappresenta il tempo impiegato dal server SQL Server sottostante per pianificare la query sulla CPU.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-943">Resource wait time only measures the time waiting for resources to be provided, as opposed to signal wait time, which is the time it takes for the underlying SQL servers to schedule the query onto the CPU.</span></span>

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

<span data-ttu-id="dcdd9-944">L DMV `sys.dm_pdw_wait_stats` può essere usata per l'analisi della tendenza cronologica delle attese.</span><span class="sxs-lookup"><span data-stu-id="dcdd9-944">The `sys.dm_pdw_wait_stats` DMV can be used for historic trend analysis of waits.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="dcdd9-945">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dcdd9-945">Next steps</span></span>
<span data-ttu-id="dcdd9-946">Per altre informazioni sulla gestione degli utenti e della sicurezza del database, vedere [Proteggere un database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="dcdd9-946">For more information about managing database users and security, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span> <span data-ttu-id="dcdd9-947">Per ulteriori informazioni sulle classi di risorse più grandi che possono migliorare le qualità degli indici indice columnstore cluster, vedere [Ricompilazione degli indici per migliorare la qualità del segmento].</span><span class="sxs-lookup"><span data-stu-id="dcdd9-947">For more information about how larger resource classes can improve clustered columnstore index quality, see [Rebuilding indexes to improve segment quality].</span></span>

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Ricompilazione degli indici per migliorare la qualità del segmento]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->
