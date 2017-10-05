---
title: Eventi estesi nel database SQL | Documentazione Microsoft
description: Vengono descritti gli eventi estesi (XEvent) in Azure SQL Database e come le sessioni di eventi sono leggermente diverse da sessioni di eventi in Microsoft SQL Server.
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: 3b28cf15-f820-4b3c-8310-908d6d5b9d0c
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genemi
ms.openlocfilehash: 7e5da1c32484b0b94d2ad32ead6bb7c28f9744aa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="extended-events-in-sql-database"></a><span data-ttu-id="c8289-103">Eventi estesi nel database SQL</span><span class="sxs-lookup"><span data-stu-id="c8289-103">Extended events in SQL Database</span></span>
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="c8289-104">In questo argomento viene illustrato come l'implementazione di eventi estesi nel database SQL di Azure è leggermente diversa rispetto agli eventi estesi in Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c8289-104">This topic explains how the implementation of extended events in Azure SQL Database is slightly different compared to extended events in Microsoft SQL Server.</span></span>

- <span data-ttu-id="c8289-105">SQL Database V12 ha acquisito la funzionalità degli eventi estesi nella seconda metà del calendario 2015.</span><span class="sxs-lookup"><span data-stu-id="c8289-105">SQL Database V12 gained the extended events feature in the second half of calendar 2015.</span></span>
- <span data-ttu-id="c8289-106">SQL Server ha gli eventi estesi dal 2008.</span><span class="sxs-lookup"><span data-stu-id="c8289-106">SQL Server has had extended events since 2008.</span></span>
- <span data-ttu-id="c8289-107">Il set di funzionalità degli eventi estesi nel database SQL è un subset affidabile delle funzionalità in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c8289-107">The feature set of extended events on SQL Database is a robust subset of the features on SQL Server.</span></span>

<span data-ttu-id="c8289-108">*XEvent* è un nome alternativo informale utilizzato talvolta per "eventi estesi" in blog e altri percorsi informali.</span><span class="sxs-lookup"><span data-stu-id="c8289-108">*XEvents* is an informal nickname that is sometimes used for 'extended events' in blogs and other informal locations.</span></span>

<span data-ttu-id="c8289-109">Per altre informazioni sugli eventi estesi, per il database SQL di Azure e Microsoft SQL Server, vedere l'articolo:</span><span class="sxs-lookup"><span data-stu-id="c8289-109">Additional information about extended events, for Azure SQL Database and Microsoft SQL Server, is available at:</span></span>

- [<span data-ttu-id="c8289-110">Quick Start: Extended events in SQL Server</span><span class="sxs-lookup"><span data-stu-id="c8289-110">Quick Start: Extended events in SQL Server</span></span>](http://msdn.microsoft.com/library/mt733217.aspx)
- [<span data-ttu-id="c8289-111">Eventi estesi</span><span class="sxs-lookup"><span data-stu-id="c8289-111">Extended Events</span></span>](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a><span data-ttu-id="c8289-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c8289-112">Prerequisites</span></span>

<span data-ttu-id="c8289-113">In questo argomento si presuppone che si dispone già di una conoscenza di:</span><span class="sxs-lookup"><span data-stu-id="c8289-113">This topic assumes you already have some knowledge of:</span></span>

- <span data-ttu-id="c8289-114">[Servizio Azure SQL Database](https://azure.microsoft.com/services/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="c8289-114">[Azure SQL Database service](https://azure.microsoft.com/services/sql-database/).</span></span>
- <span data-ttu-id="c8289-115">[Eventi estesi](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c8289-115">[Extended events](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.</span></span>

- <span data-ttu-id="c8289-116">La maggior parte della nostra documentazione sugli eventi estesi si applica sia a SQL Server che al database SQL.</span><span class="sxs-lookup"><span data-stu-id="c8289-116">The bulk of our documentation about extended events applies to both SQL Server and SQL Database.</span></span>

<span data-ttu-id="c8289-117">Un’esposizione precedente a quanto riportato di seguito è utile quando si sceglie il file evento come [destinazione](#AzureXEventsTargets):</span><span class="sxs-lookup"><span data-stu-id="c8289-117">Prior exposure to the following items is helpful when choosing the Event File as the [target](#AzureXEventsTargets):</span></span>

- [<span data-ttu-id="c8289-118">Servizio di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c8289-118">Azure Storage service</span></span>](https://azure.microsoft.com/services/storage/)


- <span data-ttu-id="c8289-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8289-119">PowerShell</span></span>
    - <span data-ttu-id="c8289-120">[Utilizzo di Azure PowerShell con Archiviazione di Azure](../storage/common/storage-powershell-guide-full.md) : fornisce informazioni complete su PowerShell e il servizio Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c8289-120">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and the Azure Storage service.</span></span>

## <a name="code-samples"></a><span data-ttu-id="c8289-121">Esempi di codice</span><span class="sxs-lookup"><span data-stu-id="c8289-121">Code samples</span></span>

<span data-ttu-id="c8289-122">Gli argomenti correlati forniscono due esempi di codice:</span><span class="sxs-lookup"><span data-stu-id="c8289-122">Related topics provide two code samples:</span></span>


- [<span data-ttu-id="c8289-123">Codice di destinazione del buffer circolare per eventi estesi nel database SQL</span><span class="sxs-lookup"><span data-stu-id="c8289-123">Ring Buffer target code for extended events in SQL Database</span></span>](sql-database-xevent-code-ring-buffer.md)
    - <span data-ttu-id="c8289-124">Breve script Transact-SQL semplice.</span><span class="sxs-lookup"><span data-stu-id="c8289-124">Short simple Transact-SQL script.</span></span>
    - <span data-ttu-id="c8289-125">Nell'argomento dell'esempio di codice si evidenzia che, una volta completata la destinazione del buffer circolare, è necessario rilasciarne le risorse tramite l'esecuzione di un'istruzione `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` alter-drop.</span><span class="sxs-lookup"><span data-stu-id="c8289-125">We emphasize in the code sample topic that, when you are done with a Ring Buffer target, you should release its resources by executing an alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` statement.</span></span> <span data-ttu-id="c8289-126">Successivamente è possibile aggiungere un'altra istanza del buffer circolare da `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span><span class="sxs-lookup"><span data-stu-id="c8289-126">Later you can add another instance of Ring Buffer by `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span></span>


- [<span data-ttu-id="c8289-127">Codice di destinazione del file evento per eventi estesi nel database SQL</span><span class="sxs-lookup"><span data-stu-id="c8289-127">Event File target code for extended events in SQL Database</span></span>](sql-database-xevent-code-event-file.md)
    - <span data-ttu-id="c8289-128">Fase 1 è PowerShell per creare un contenitore di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c8289-128">Phase 1 is PowerShell to create an Azure Storage container.</span></span>
    - <span data-ttu-id="c8289-129">Fase 2 è Transact-SQL che utilizza il contenitore di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c8289-129">Phase 2 is Transact-SQL that uses the Azure Storage container.</span></span>

## <a name="transact-sql-differences"></a><span data-ttu-id="c8289-130">Differenze di Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="c8289-130">Transact-SQL differences</span></span>


- <span data-ttu-id="c8289-131">Quando si esegue il comando [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) su SQL Server, si utilizza la clausola **ON SERVER** .</span><span class="sxs-lookup"><span data-stu-id="c8289-131">When you execute the [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) command on SQL Server, you use the **ON SERVER** clause.</span></span> <span data-ttu-id="c8289-132">Ma nel database SQL si utilizza invece la clausola **ON DATABASE** .</span><span class="sxs-lookup"><span data-stu-id="c8289-132">But on SQL Database you use the **ON DATABASE** clause instead.</span></span>


- <span data-ttu-id="c8289-133">La clausola **ON DATABASE** riguarda anche i comandi Transact-SQL [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) e [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx).</span><span class="sxs-lookup"><span data-stu-id="c8289-133">The **ON DATABASE** clause also applies to the [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) and [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL commands.</span></span>


- <span data-ttu-id="c8289-134">Una procedura consigliata consiste nell'includere l'opzione della sessione eventi di **STARTUP_STATE = ON** nelle istruzioni **CREATE EVENT SESSION** o **ALTER EVENT SESSION**.</span><span class="sxs-lookup"><span data-stu-id="c8289-134">A best practice is to include the event session option of **STARTUP_STATE = ON** in your **CREATE EVENT SESSION**  or **ALTER EVENT SESSION** statements.</span></span>
    - <span data-ttu-id="c8289-135">Il valore **= ON** supporta un riavvio automatico dopo una riconfigurazione del database logico a causa di un failover.</span><span class="sxs-lookup"><span data-stu-id="c8289-135">The **= ON** value supports an automatic restart after a reconfiguration of the logical database due to a failover.</span></span>

## <a name="new-catalog-views"></a><span data-ttu-id="c8289-136">Nuove viste del catalogo</span><span class="sxs-lookup"><span data-stu-id="c8289-136">New catalog views</span></span>

<span data-ttu-id="c8289-137">La funzionalità degli eventi estesi è supportata da diverse [viste del catalogo](http://msdn.microsoft.com/library/ms174365.aspx).</span><span class="sxs-lookup"><span data-stu-id="c8289-137">The extended events feature is supported by several [catalog views](http://msdn.microsoft.com/library/ms174365.aspx).</span></span> <span data-ttu-id="c8289-138">Le viste del catalogo indicano i *metadati o le definizioni* di sessioni di eventi create dall'utente nel database corrente.</span><span class="sxs-lookup"><span data-stu-id="c8289-138">Catalog views tell you about *metadata or definitions* of user-created event sessions in the current database.</span></span> <span data-ttu-id="c8289-139">Le viste non restituiscono informazioni sulle istanze delle sessioni di eventi attivi.</span><span class="sxs-lookup"><span data-stu-id="c8289-139">The views do not return information about instances of active event sessions.</span></span>

| <span data-ttu-id="c8289-140">Nome della</span><span class="sxs-lookup"><span data-stu-id="c8289-140">Name of</span></span><br/><span data-ttu-id="c8289-141">vista del catalogo</span><span class="sxs-lookup"><span data-stu-id="c8289-141">catalog view</span></span> | <span data-ttu-id="c8289-142">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8289-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c8289-143">**sys.database_event_session_actions**</span><span class="sxs-lookup"><span data-stu-id="c8289-143">**sys.database_event_session_actions**</span></span> |<span data-ttu-id="c8289-144">Restituisce una riga per ogni azione su ogni evento di una sessione di eventi.</span><span class="sxs-lookup"><span data-stu-id="c8289-144">Returns a row for each action on each event of an event session.</span></span> |
| <span data-ttu-id="c8289-145">**sys.database_event_session_events**</span><span class="sxs-lookup"><span data-stu-id="c8289-145">**sys.database_event_session_events**</span></span> |<span data-ttu-id="c8289-146">Restituisce una riga per ogni evento in una sessione di eventi.</span><span class="sxs-lookup"><span data-stu-id="c8289-146">Returns a row for each event in an event session.</span></span> |
| <span data-ttu-id="c8289-147">**sys.database_event_session_fields**</span><span class="sxs-lookup"><span data-stu-id="c8289-147">**sys.database_event_session_fields**</span></span> |<span data-ttu-id="c8289-148">Restituisce una riga per ogni colonna personalizzabile impostata in modo esplicito su eventi e destinazioni.</span><span class="sxs-lookup"><span data-stu-id="c8289-148">Returns a row for each customize-able column that was explicitly set on events and targets.</span></span> |
| <span data-ttu-id="c8289-149">**sys.database_event_session_targets**</span><span class="sxs-lookup"><span data-stu-id="c8289-149">**sys.database_event_session_targets**</span></span> |<span data-ttu-id="c8289-150">Restituisce una riga per ogni destinazione di evento per una sessione di eventi.</span><span class="sxs-lookup"><span data-stu-id="c8289-150">Returns a row for each event target for an event session.</span></span> |
| <span data-ttu-id="c8289-151">**sys.database_event_sessions**</span><span class="sxs-lookup"><span data-stu-id="c8289-151">**sys.database_event_sessions**</span></span> |<span data-ttu-id="c8289-152">Restituisce una riga per ogni sessione di eventi nel database SQL del database.</span><span class="sxs-lookup"><span data-stu-id="c8289-152">Returns a row for each event session in the SQL Database database.</span></span> |

<span data-ttu-id="c8289-153">In Microsoft SQL Server le viste del catalogo simili hanno nomi che includono *.server\_* anziché *.database\_*.</span><span class="sxs-lookup"><span data-stu-id="c8289-153">In Microsoft SQL Server, similar catalog views have names that include *.server\_* instead of *.database\_*.</span></span> <span data-ttu-id="c8289-154">Il modello del nome è simile a **sys.server_event_%**.</span><span class="sxs-lookup"><span data-stu-id="c8289-154">The name pattern is like **sys.server_event_%**.</span></span>

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a><span data-ttu-id="c8289-155">[DMV](http://msdn.microsoft.com/library/ms188754.aspx)</span><span class="sxs-lookup"><span data-stu-id="c8289-155">New dynamic management views [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)</span></span>

<span data-ttu-id="c8289-156">Il database SQL di Azure include [viste a gestione dinamica (DMV)](http://msdn.microsoft.com/library/bb677293.aspx) che supportano gli eventi estesi.</span><span class="sxs-lookup"><span data-stu-id="c8289-156">Azure SQL Database has [dynamic management views (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) that support extended events.</span></span> <span data-ttu-id="c8289-157">Le DMV indicano le sessioni di eventi *attive* .</span><span class="sxs-lookup"><span data-stu-id="c8289-157">DMVs tell you about *active* event sessions.</span></span>

| <span data-ttu-id="c8289-158">Nome della DMV</span><span class="sxs-lookup"><span data-stu-id="c8289-158">Name of DMV</span></span> | <span data-ttu-id="c8289-159">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8289-159">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c8289-160">**sys.dm_xe_database_session_event_actions**</span><span class="sxs-lookup"><span data-stu-id="c8289-160">**sys.dm_xe_database_session_event_actions**</span></span> |<span data-ttu-id="c8289-161">Restituisce informazioni sulle azioni della sessione di eventi.</span><span class="sxs-lookup"><span data-stu-id="c8289-161">Returns information about event session actions.</span></span> |
| <span data-ttu-id="c8289-162">**sys.dm_xe_database_session_events**</span><span class="sxs-lookup"><span data-stu-id="c8289-162">**sys.dm_xe_database_session_events**</span></span> |<span data-ttu-id="c8289-163">Restituisce informazioni sugli eventi della sessione.</span><span class="sxs-lookup"><span data-stu-id="c8289-163">Returns information about session events.</span></span> |
| <span data-ttu-id="c8289-164">**sys.dm_xe_database_session_object_columns**</span><span class="sxs-lookup"><span data-stu-id="c8289-164">**sys.dm_xe_database_session_object_columns**</span></span> |<span data-ttu-id="c8289-165">Mostra i valori di configurazione per gli oggetti associati a una sessione.</span><span class="sxs-lookup"><span data-stu-id="c8289-165">Shows the configuration values for objects that are bound to a session.</span></span> |
| <span data-ttu-id="c8289-166">**sys.dm_xe_database_session_targets**</span><span class="sxs-lookup"><span data-stu-id="c8289-166">**sys.dm_xe_database_session_targets**</span></span> |<span data-ttu-id="c8289-167">Restituisce informazioni sulle destinazioni della sessione.</span><span class="sxs-lookup"><span data-stu-id="c8289-167">Returns information about session targets.</span></span> |
| <span data-ttu-id="c8289-168">**sys.dm_xe_database_sessions**</span><span class="sxs-lookup"><span data-stu-id="c8289-168">**sys.dm_xe_database_sessions**</span></span> |<span data-ttu-id="c8289-169">Restituisce una riga per ogni sessione di eventi con ambito nel database corrente.</span><span class="sxs-lookup"><span data-stu-id="c8289-169">Returns a row for each event session that is scoped to the current database.</span></span> |

<span data-ttu-id="c8289-170">In Microsoft SQL Server le viste del catalogo simili sono denominate senza la parte del nome *\_database*, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c8289-170">In Microsoft SQL Server, similar catalog views are named without the *\_database* portion of the name, such as:</span></span>

- <span data-ttu-id="c8289-171">**sys.dm_xe_sessions**, anziché il nome</span><span class="sxs-lookup"><span data-stu-id="c8289-171">**sys.dm_xe_sessions**, instead of name</span></span><br/><span data-ttu-id="c8289-172">**sys.dm_xe_database_sessions**.</span><span class="sxs-lookup"><span data-stu-id="c8289-172">**sys.dm_xe_database_sessions**.</span></span>

### <a name="dmvs-common-to-both"></a><span data-ttu-id="c8289-173">DMV comuni a entrambi</span><span class="sxs-lookup"><span data-stu-id="c8289-173">DMVs common to both</span></span>
<span data-ttu-id="c8289-174">Per gli eventi estesi sono disponibili DMV aggiuntive comuni a Microsoft SQL Server e Azure SQL Database:</span><span class="sxs-lookup"><span data-stu-id="c8289-174">For extended events there are additional DMVs that are common to both Azure SQL Database and Microsoft SQL Server:</span></span>

- <span data-ttu-id="c8289-175">**sys.dm_xe_map_values**</span><span class="sxs-lookup"><span data-stu-id="c8289-175">**sys.dm_xe_map_values**</span></span>
- <span data-ttu-id="c8289-176">**sys.dm_xe_object_columns**</span><span class="sxs-lookup"><span data-stu-id="c8289-176">**sys.dm_xe_object_columns**</span></span>
- <span data-ttu-id="c8289-177">**sys.dm_xe_objects**</span><span class="sxs-lookup"><span data-stu-id="c8289-177">**sys.dm_xe_objects**</span></span>
- <span data-ttu-id="c8289-178">**sys.dm_xe_packages**</span><span class="sxs-lookup"><span data-stu-id="c8289-178">**sys.dm_xe_packages**</span></span>

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-the-available-extended-events-actions-and-targets"></a><span data-ttu-id="c8289-179">Trovare gli eventi estesi, le azioni e le destinazioni disponibili</span><span class="sxs-lookup"><span data-stu-id="c8289-179">Find the available extended events, actions, and targets</span></span>

<span data-ttu-id="c8289-180">È possibile eseguire un semplice **SELECT** di SQL per ottenere un elenco di eventi, azioni e destinazioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="c8289-180">You can run a simple SQL **SELECT** to obtain a list of the available events, actions, and target.</span></span>

```sql
SELECT
        o.object_type,
        p.name         AS [package_name],
        o.name         AS [db_object_name],
        o.description  AS [db_obj_description]
    FROM
                   sys.dm_xe_objects  AS o
        INNER JOIN sys.dm_xe_packages AS p  ON p.guid = o.package_guid
    WHERE
        o.object_type in
            (
            'action',  'event',  'target'
            )
    ORDER BY
        o.object_type,
        p.name,
        o.name;
```


<span data-ttu-id="c8289-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span><span class="sxs-lookup"><span data-stu-id="c8289-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span></span>

## <a name="targets-for-your-sql-database-event-sessions"></a><span data-ttu-id="c8289-182">Destinazioni per le sessioni di eventi del database SQL</span><span class="sxs-lookup"><span data-stu-id="c8289-182">Targets for your SQL Database event sessions</span></span>

<span data-ttu-id="c8289-183">Di seguito si trovano le destinazioni che possono acquisire i risultati dalle sessioni di eventi nel database SQL:</span><span class="sxs-lookup"><span data-stu-id="c8289-183">Here are targets that can capture results from your event sessions on SQL Database:</span></span>

- <span data-ttu-id="c8289-184">[Destinazione buffer circolare](http://msdn.microsoft.com/library/ff878182.aspx) : contiene per un tempo breve i dati degli eventi nella memoria.</span><span class="sxs-lookup"><span data-stu-id="c8289-184">[Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx) - Briefly holds event data in memory.</span></span>
- <span data-ttu-id="c8289-185">[Destinazione contatore eventi](http://msdn.microsoft.com/library/ff878025.aspx) : conta tutti gli eventi che si verificano durante una sessione di eventi estesi.</span><span class="sxs-lookup"><span data-stu-id="c8289-185">[Event Counter target](http://msdn.microsoft.com/library/ff878025.aspx) - Counts all events that occur during an extended events session.</span></span>
- <span data-ttu-id="c8289-186">[Destinazione file evento](http://msdn.microsoft.com/library/ff878115.aspx) : scrive buffer completi in un contenitore di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c8289-186">[Event File target](http://msdn.microsoft.com/library/ff878115.aspx) - Writes complete buffers to an Azure Storage container.</span></span>

<span data-ttu-id="c8289-187">L’API [Tracciamento eventi per Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) non è disponibile per gli eventi estesi nel database SQL.</span><span class="sxs-lookup"><span data-stu-id="c8289-187">The [Event Tracing for Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API is not available for extended events on SQL Database.</span></span>

## <a name="restrictions"></a><span data-ttu-id="c8289-188">Restrizioni</span><span class="sxs-lookup"><span data-stu-id="c8289-188">Restrictions</span></span>

<span data-ttu-id="c8289-189">Esistono un paio di differenze relative alla sicurezza adatte all'ambiente cloud del database SQL:</span><span class="sxs-lookup"><span data-stu-id="c8289-189">There are a couple of security-related differences befitting the cloud environment of SQL Database:</span></span>

- <span data-ttu-id="c8289-190">Gli eventi estesi si basano sul modello di isolamento single-tenant.</span><span class="sxs-lookup"><span data-stu-id="c8289-190">Extended events are founded on the single-tenant isolation model.</span></span> <span data-ttu-id="c8289-191">Una sessione di eventi in un database non può accedere a dati o eventi da un altro database.</span><span class="sxs-lookup"><span data-stu-id="c8289-191">An event session in one database cannot access data or events from another database.</span></span>
- <span data-ttu-id="c8289-192">Non è possibile emettere un'istruzione **CREATE EVENT SESSION** nel contesto del database **master**.</span><span class="sxs-lookup"><span data-stu-id="c8289-192">You cannot issue a **CREATE EVENT SESSION** statement in the context of the **master** database.</span></span>

## <a name="permission-model"></a><span data-ttu-id="c8289-193">Modello di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="c8289-193">Permission model</span></span>

<span data-ttu-id="c8289-194">È necessario avere l'autorizzazione **Controllo** nel database per emettere un'istruzione **CREATE EVENT SESSION**.</span><span class="sxs-lookup"><span data-stu-id="c8289-194">You must have **Control** permission on the database to issue a **CREATE EVENT SESSION** statement.</span></span> <span data-ttu-id="c8289-195">Il proprietario del database (dbo) dispone dell’autorizzazione **controllo** .</span><span class="sxs-lookup"><span data-stu-id="c8289-195">The database owner (dbo) has **Control** permission.</span></span>

### <a name="storage-container-authorizations"></a><span data-ttu-id="c8289-196">Autorizzazioni del contenitore di archiviazione</span><span class="sxs-lookup"><span data-stu-id="c8289-196">Storage container authorizations</span></span>

<span data-ttu-id="c8289-197">Il token della firma di accesso condiviso generato per il contenitore di Archiviazione di Azure deve specificare **rwl** per le autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="c8289-197">The SAS token you generate for your Azure Storage container must specify **rwl** for the permissions.</span></span> <span data-ttu-id="c8289-198">Questo valore **rwl** fornisce le autorizzazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c8289-198">The **rwl** value provides the following permissions:</span></span>

- <span data-ttu-id="c8289-199">Lettura</span><span class="sxs-lookup"><span data-stu-id="c8289-199">Read</span></span>
- <span data-ttu-id="c8289-200">Scrittura</span><span class="sxs-lookup"><span data-stu-id="c8289-200">Write</span></span>
- <span data-ttu-id="c8289-201">Elenco</span><span class="sxs-lookup"><span data-stu-id="c8289-201">List</span></span>

## <a name="performance-considerations"></a><span data-ttu-id="c8289-202">Considerazioni sulle prestazioni</span><span class="sxs-lookup"><span data-stu-id="c8289-202">Performance considerations</span></span>

<span data-ttu-id="c8289-203">Esistono scenari in cui un uso intensivo di eventi estesi può accumulare più memoria attiva di quanto è adatto per l'intero sistema.</span><span class="sxs-lookup"><span data-stu-id="c8289-203">There are scenarios where intensive use of extended events can accumulate more active memory than is healthy for the overall system.</span></span> <span data-ttu-id="c8289-204">Pertanto il sistema di Azure SQL Database imposta e regola in modo dinamico i limiti sulla quantità di memoria attiva che può essere accumulata da una sessione di eventi.</span><span class="sxs-lookup"><span data-stu-id="c8289-204">Therefore the Azure SQL Database system dynamically sets and adjusts limits on the amount of active memory that can be accumulated by an event session.</span></span> <span data-ttu-id="c8289-205">Molti fattori vengono utilizzati nel calcolo dinamico.</span><span class="sxs-lookup"><span data-stu-id="c8289-205">Many factors go into the dynamic calculation.</span></span>

<span data-ttu-id="c8289-206">Se si riceve un messaggio di errore che indica che è stato applicato un massimo di memoria, alcune azioni correttive da eseguire sono:</span><span class="sxs-lookup"><span data-stu-id="c8289-206">If you receive an error message that says a memory maximum was enforced, some corrective actions you can take are:</span></span>

- <span data-ttu-id="c8289-207">Eseguire meno sessioni di eventi simultanee.</span><span class="sxs-lookup"><span data-stu-id="c8289-207">Run fewer concurrent event sessions.</span></span>
- <span data-ttu-id="c8289-208">Tramite le istruzioni **CREATE** e **ALTER** per le sessioni di eventi, ridurre la quantità di memoria specificata nella clausola **MAX\_MEMORY**.</span><span class="sxs-lookup"><span data-stu-id="c8289-208">Through your **CREATE** and **ALTER** statements for event sessions, reduce the amount of memory you specify on the **MAX\_MEMORY** clause.</span></span>

### <a name="network-latency"></a><span data-ttu-id="c8289-209">Latenza di rete</span><span class="sxs-lookup"><span data-stu-id="c8289-209">Network latency</span></span>

<span data-ttu-id="c8289-210">La destinazione del **file evento** potrebbe subire una latenza di rete o errori durante il mantenimento dei dati nei BLOB di archiviazione di Azure .</span><span class="sxs-lookup"><span data-stu-id="c8289-210">The **Event File** target might experience network latency or failures while persisting data to Azure Storage blobs.</span></span> <span data-ttu-id="c8289-211">Altri eventi nel database SQL potrebbero subire un ritardo mentre rimangono in attesa del completamento della comunicazione di rete.</span><span class="sxs-lookup"><span data-stu-id="c8289-211">Other events in SQL Database might be delayed while they wait for the network communication to complete.</span></span> <span data-ttu-id="c8289-212">Questo ritardo può rallentare il carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="c8289-212">This delay can slow your workload.</span></span>

- <span data-ttu-id="c8289-213">Per ridurre questo rischio delle prestazioni, evitare di impostare l'opzione **EVENT_RETENTION_MODE** su **NO_EVENT_LOSS** nelle definizioni della sessione di eventi.</span><span class="sxs-lookup"><span data-stu-id="c8289-213">To mitigate this performance risk, avoid setting the **EVENT_RETENTION_MODE** option to **NO_EVENT_LOSS** in your event session definitions.</span></span>

## <a name="related-links"></a><span data-ttu-id="c8289-214">Collegamenti correlati</span><span class="sxs-lookup"><span data-stu-id="c8289-214">Related links</span></span>

- <span data-ttu-id="c8289-215">[Uso di Azure PowerShell con Archiviazione di Azure](../storage/common/storage-powershell-guide-full.md)</span><span class="sxs-lookup"><span data-stu-id="c8289-215">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span>
- [<span data-ttu-id="c8289-216">Cmdlet di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c8289-216">Azure Storage Cmdlets</span></span>](http://msdn.microsoft.com/library/dn806401.aspx)
- <span data-ttu-id="c8289-217">[Utilizzo di Azure PowerShell con Archiviazione di Azure](../storage/common/storage-powershell-guide-full.md) : fornisce informazioni complete su PowerShell e il servizio Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c8289-217">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and the Azure Storage service.</span></span>
- [<span data-ttu-id="c8289-218">Come usare l'archiviazione BLOB da .NET</span><span class="sxs-lookup"><span data-stu-id="c8289-218">How to use Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [<span data-ttu-id="c8289-219">CREARE CREDENZIALI (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="c8289-219">CREATE CREDENTIAL (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/ms189522.aspx)
- [<span data-ttu-id="c8289-220">CREARE LA SESSIONE DI EVENTI (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="c8289-220">CREATE EVENT SESSION (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/bb677289.aspx)
- [<span data-ttu-id="c8289-221">Post del blog di Jonathan Kehayias sugli eventi estesi in Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="c8289-221">Jonathan Kehayias' blog posts about extended events in Microsoft SQL Server</span></span>](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- <span data-ttu-id="c8289-222">La pagina Web *Aggiornamenti di Azure*, con visualizzazione limitata dal parametro ai soli aggiornamenti relativi al database SQL di Azure:</span><span class="sxs-lookup"><span data-stu-id="c8289-222">The Azure *Service Updates* webpage, narrowed by parameter to Azure SQL Database:</span></span>
    - [<span data-ttu-id="c8289-223">https://azure.microsoft.com/updates/?service=sql-database</span><span class="sxs-lookup"><span data-stu-id="c8289-223">https://azure.microsoft.com/updates/?service=sql-database</span></span>](https://azure.microsoft.com/updates/?service=sql-database)


<span data-ttu-id="c8289-224">Altri argomenti con esempi di codice per gli eventi estesi sono disponibili ai collegamenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="c8289-224">Other code sample topics for extended events are available at the following links.</span></span> <span data-ttu-id="c8289-225">È comunque necessario controllare regolarmente qualsiasi esempio per verificare se è destinato a Microsoft SQL Server o al database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="c8289-225">However, you must routinely check any sample to see whether the sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="c8289-226">È quindi possibile decidere se sono necessarie alcune modifiche per eseguire l'esempio.</span><span class="sxs-lookup"><span data-stu-id="c8289-226">Then you can decide whether minor changes are needed to run the sample.</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find the Objects That Have the Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
