---
title: eventi aaaExtended nel Database SQL | Documenti Microsoft
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
ms.openlocfilehash: 8c966a84412aa561c92b16e5c6902102483eb1bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="extended-events-in-sql-database"></a><span data-ttu-id="f9c21-103">Eventi estesi nel database SQL</span><span class="sxs-lookup"><span data-stu-id="f9c21-103">Extended events in SQL Database</span></span>
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="f9c21-104">In questo argomento viene illustrato come implementazione di hello degli eventi estesi nel Database di SQL Azure è leggermente diverso tooextended confrontati gli eventi in Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f9c21-104">This topic explains how hello implementation of extended events in Azure SQL Database is slightly different compared tooextended events in Microsoft SQL Server.</span></span>

- <span data-ttu-id="f9c21-105">Database SQL V12 acquisita funzionalità di eventi estesi hello hello seconda metà del calendario 2015.</span><span class="sxs-lookup"><span data-stu-id="f9c21-105">SQL Database V12 gained hello extended events feature in hello second half of calendar 2015.</span></span>
- <span data-ttu-id="f9c21-106">SQL Server ha gli eventi estesi dal 2008.</span><span class="sxs-lookup"><span data-stu-id="f9c21-106">SQL Server has had extended events since 2008.</span></span>
- <span data-ttu-id="f9c21-107">set di funzionalità Hello degli eventi estesi nel Database SQL è un subset affidabile di funzionalità hello in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f9c21-107">hello feature set of extended events on SQL Database is a robust subset of hello features on SQL Server.</span></span>

<span data-ttu-id="f9c21-108">*XEvent* è un nome alternativo informale utilizzato talvolta per "eventi estesi" in blog e altri percorsi informali.</span><span class="sxs-lookup"><span data-stu-id="f9c21-108">*XEvents* is an informal nickname that is sometimes used for 'extended events' in blogs and other informal locations.</span></span>

<span data-ttu-id="f9c21-109">Per altre informazioni sugli eventi estesi, per il database SQL di Azure e Microsoft SQL Server, vedere l'articolo:</span><span class="sxs-lookup"><span data-stu-id="f9c21-109">Additional information about extended events, for Azure SQL Database and Microsoft SQL Server, is available at:</span></span>

- [<span data-ttu-id="f9c21-110">Quick Start: Extended events in SQL Server</span><span class="sxs-lookup"><span data-stu-id="f9c21-110">Quick Start: Extended events in SQL Server</span></span>](http://msdn.microsoft.com/library/mt733217.aspx)
- [<span data-ttu-id="f9c21-111">Eventi estesi</span><span class="sxs-lookup"><span data-stu-id="f9c21-111">Extended Events</span></span>](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a><span data-ttu-id="f9c21-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f9c21-112">Prerequisites</span></span>

<span data-ttu-id="f9c21-113">In questo argomento si presuppone che si dispone già di una conoscenza di:</span><span class="sxs-lookup"><span data-stu-id="f9c21-113">This topic assumes you already have some knowledge of:</span></span>

- <span data-ttu-id="f9c21-114">[Servizio Azure SQL Database](https://azure.microsoft.com/services/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="f9c21-114">[Azure SQL Database service](https://azure.microsoft.com/services/sql-database/).</span></span>
- <span data-ttu-id="f9c21-115">[Eventi estesi](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f9c21-115">[Extended events](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.</span></span>

- <span data-ttu-id="f9c21-116">bulk Hello di documentazione sugli eventi estesi applica tooboth SQL Server e Database SQL.</span><span class="sxs-lookup"><span data-stu-id="f9c21-116">hello bulk of our documentation about extended events applies tooboth SQL Server and SQL Database.</span></span>

<span data-ttu-id="f9c21-117">Esposizione precedente toohello elementi è utile quando si scelgono i File di eventi come hello hello [destinazione](#AzureXEventsTargets):</span><span class="sxs-lookup"><span data-stu-id="f9c21-117">Prior exposure toohello following items is helpful when choosing hello Event File as hello [target](#AzureXEventsTargets):</span></span>

- [<span data-ttu-id="f9c21-118">Servizio di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="f9c21-118">Azure Storage service</span></span>](https://azure.microsoft.com/services/storage/)


- <span data-ttu-id="f9c21-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9c21-119">PowerShell</span></span>
    - <span data-ttu-id="f9c21-120">[Con Azure PowerShell con l'archiviazione di Azure](../storage/common/storage-powershell-guide-full.md) -include informazioni complete su PowerShell e hello servizio di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c21-120">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and hello Azure Storage service.</span></span>

## <a name="code-samples"></a><span data-ttu-id="f9c21-121">Esempi di codice</span><span class="sxs-lookup"><span data-stu-id="f9c21-121">Code samples</span></span>

<span data-ttu-id="f9c21-122">Gli argomenti correlati forniscono due esempi di codice:</span><span class="sxs-lookup"><span data-stu-id="f9c21-122">Related topics provide two code samples:</span></span>


- [<span data-ttu-id="f9c21-123">Codice di destinazione del buffer circolare per eventi estesi nel database SQL</span><span class="sxs-lookup"><span data-stu-id="f9c21-123">Ring Buffer target code for extended events in SQL Database</span></span>](sql-database-xevent-code-ring-buffer.md)
    - <span data-ttu-id="f9c21-124">Breve script Transact-SQL semplice.</span><span class="sxs-lookup"><span data-stu-id="f9c21-124">Short simple Transact-SQL script.</span></span>
    - <span data-ttu-id="f9c21-125">Lo sottolineiamo in argomento di esempio di codice hello che, una volta con una destinazione Buffer circolare, è necessario rilasciare le risorse eseguendo un rilascio alter `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` istruzione.</span><span class="sxs-lookup"><span data-stu-id="f9c21-125">We emphasize in hello code sample topic that, when you are done with a Ring Buffer target, you should release its resources by executing an alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` statement.</span></span> <span data-ttu-id="f9c21-126">Successivamente è possibile aggiungere un'altra istanza del buffer circolare da `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span><span class="sxs-lookup"><span data-stu-id="f9c21-126">Later you can add another instance of Ring Buffer by `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span></span>


- [<span data-ttu-id="f9c21-127">Codice di destinazione del file evento per eventi estesi nel database SQL</span><span class="sxs-lookup"><span data-stu-id="f9c21-127">Event File target code for extended events in SQL Database</span></span>](sql-database-xevent-code-event-file.md)
    - <span data-ttu-id="f9c21-128">Fase 1 è PowerShell toocreate un contenitore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c21-128">Phase 1 is PowerShell toocreate an Azure Storage container.</span></span>
    - <span data-ttu-id="f9c21-129">Fase 2 è Transact-SQL che utilizza il contenitore di archiviazione di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f9c21-129">Phase 2 is Transact-SQL that uses hello Azure Storage container.</span></span>

## <a name="transact-sql-differences"></a><span data-ttu-id="f9c21-130">Differenze di Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="f9c21-130">Transact-SQL differences</span></span>


- <span data-ttu-id="f9c21-131">Quando si esegue hello [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) comando in SQL Server, utilizzare hello **ON SERVER** clausola.</span><span class="sxs-lookup"><span data-stu-id="f9c21-131">When you execute hello [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) command on SQL Server, you use hello **ON SERVER** clause.</span></span> <span data-ttu-id="f9c21-132">Ma nel Database SQL è utilizzare hello **ON DATABASE** clausola invece.</span><span class="sxs-lookup"><span data-stu-id="f9c21-132">But on SQL Database you use hello **ON DATABASE** clause instead.</span></span>


- <span data-ttu-id="f9c21-133">Hello **ON DATABASE** clausola si applica anche toohello [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) e [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) comandi Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="f9c21-133">hello **ON DATABASE** clause also applies toohello [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) and [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL commands.</span></span>


- <span data-ttu-id="f9c21-134">Una procedura consigliata è l'opzione della sessione eventi hello tooinclude di **STARTUP_STATE = ON** nel **CREATE EVENT SESSION** o **ALTER EVENT SESSION** istruzioni.</span><span class="sxs-lookup"><span data-stu-id="f9c21-134">A best practice is tooinclude hello event session option of **STARTUP_STATE = ON** in your **CREATE EVENT SESSION**  or **ALTER EVENT SESSION** statements.</span></span>
    - <span data-ttu-id="f9c21-135">Hello **= ON** valore supporta un riavvio automatico dopo una riconfigurazione del database logico di hello scadenza tooa failover.</span><span class="sxs-lookup"><span data-stu-id="f9c21-135">hello **= ON** value supports an automatic restart after a reconfiguration of hello logical database due tooa failover.</span></span>

## <a name="new-catalog-views"></a><span data-ttu-id="f9c21-136">Nuove viste del catalogo</span><span class="sxs-lookup"><span data-stu-id="f9c21-136">New catalog views</span></span>

<span data-ttu-id="f9c21-137">Hello funzionalità eventi estesi è supportato da molti [viste del catalogo](http://msdn.microsoft.com/library/ms174365.aspx).</span><span class="sxs-lookup"><span data-stu-id="f9c21-137">hello extended events feature is supported by several [catalog views](http://msdn.microsoft.com/library/ms174365.aspx).</span></span> <span data-ttu-id="f9c21-138">Viste del catalogo forniscono informazioni sul *metadati o definizioni di* di sessioni eventi creati dall'utente nel database corrente hello.</span><span class="sxs-lookup"><span data-stu-id="f9c21-138">Catalog views tell you about *metadata or definitions* of user-created event sessions in hello current database.</span></span> <span data-ttu-id="f9c21-139">viste di Hello non restituiscono informazioni sulle istanze di sessioni eventi attivi.</span><span class="sxs-lookup"><span data-stu-id="f9c21-139">hello views do not return information about instances of active event sessions.</span></span>

| <span data-ttu-id="f9c21-140">Nome della</span><span class="sxs-lookup"><span data-stu-id="f9c21-140">Name of</span></span><br/><span data-ttu-id="f9c21-141">vista del catalogo</span><span class="sxs-lookup"><span data-stu-id="f9c21-141">catalog view</span></span> | <span data-ttu-id="f9c21-142">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f9c21-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f9c21-143">**sys.database_event_session_actions**</span><span class="sxs-lookup"><span data-stu-id="f9c21-143">**sys.database_event_session_actions**</span></span> |<span data-ttu-id="f9c21-144">Restituisce una riga per ogni azione su ogni evento di una sessione di eventi.</span><span class="sxs-lookup"><span data-stu-id="f9c21-144">Returns a row for each action on each event of an event session.</span></span> |
| <span data-ttu-id="f9c21-145">**sys.database_event_session_events**</span><span class="sxs-lookup"><span data-stu-id="f9c21-145">**sys.database_event_session_events**</span></span> |<span data-ttu-id="f9c21-146">Restituisce una riga per ogni evento in una sessione di eventi.</span><span class="sxs-lookup"><span data-stu-id="f9c21-146">Returns a row for each event in an event session.</span></span> |
| <span data-ttu-id="f9c21-147">**sys.database_event_session_fields**</span><span class="sxs-lookup"><span data-stu-id="f9c21-147">**sys.database_event_session_fields**</span></span> |<span data-ttu-id="f9c21-148">Restituisce una riga per ogni colonna personalizzabile impostata in modo esplicito su eventi e destinazioni.</span><span class="sxs-lookup"><span data-stu-id="f9c21-148">Returns a row for each customize-able column that was explicitly set on events and targets.</span></span> |
| <span data-ttu-id="f9c21-149">**sys.database_event_session_targets**</span><span class="sxs-lookup"><span data-stu-id="f9c21-149">**sys.database_event_session_targets**</span></span> |<span data-ttu-id="f9c21-150">Restituisce una riga per ogni destinazione di evento per una sessione di eventi.</span><span class="sxs-lookup"><span data-stu-id="f9c21-150">Returns a row for each event target for an event session.</span></span> |
| <span data-ttu-id="f9c21-151">**sys.database_event_sessions**</span><span class="sxs-lookup"><span data-stu-id="f9c21-151">**sys.database_event_sessions**</span></span> |<span data-ttu-id="f9c21-152">Restituisce una riga per ogni sessione di eventi nel database di SQL Database hello.</span><span class="sxs-lookup"><span data-stu-id="f9c21-152">Returns a row for each event session in hello SQL Database database.</span></span> |

<span data-ttu-id="f9c21-153">In Microsoft SQL Server le viste del catalogo simili hanno nomi che includono *.server\_* anziché *.database\_*.</span><span class="sxs-lookup"><span data-stu-id="f9c21-153">In Microsoft SQL Server, similar catalog views have names that include *.server\_* instead of *.database\_*.</span></span> <span data-ttu-id="f9c21-154">modello di nome Hello è ad esempio **sys.server_event_%**.</span><span class="sxs-lookup"><span data-stu-id="f9c21-154">hello name pattern is like **sys.server_event_%**.</span></span>

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a><span data-ttu-id="f9c21-155">[DMV](http://msdn.microsoft.com/library/ms188754.aspx)</span><span class="sxs-lookup"><span data-stu-id="f9c21-155">New dynamic management views [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)</span></span>

<span data-ttu-id="f9c21-156">Il database SQL di Azure include [viste a gestione dinamica (DMV)](http://msdn.microsoft.com/library/bb677293.aspx) che supportano gli eventi estesi.</span><span class="sxs-lookup"><span data-stu-id="f9c21-156">Azure SQL Database has [dynamic management views (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) that support extended events.</span></span> <span data-ttu-id="f9c21-157">Le DMV indicano le sessioni di eventi *attive* .</span><span class="sxs-lookup"><span data-stu-id="f9c21-157">DMVs tell you about *active* event sessions.</span></span>

| <span data-ttu-id="f9c21-158">Nome della DMV</span><span class="sxs-lookup"><span data-stu-id="f9c21-158">Name of DMV</span></span> | <span data-ttu-id="f9c21-159">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f9c21-159">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f9c21-160">**sys.dm_xe_database_session_event_actions**</span><span class="sxs-lookup"><span data-stu-id="f9c21-160">**sys.dm_xe_database_session_event_actions**</span></span> |<span data-ttu-id="f9c21-161">Restituisce informazioni sulle azioni della sessione di eventi.</span><span class="sxs-lookup"><span data-stu-id="f9c21-161">Returns information about event session actions.</span></span> |
| <span data-ttu-id="f9c21-162">**sys.dm_xe_database_session_events**</span><span class="sxs-lookup"><span data-stu-id="f9c21-162">**sys.dm_xe_database_session_events**</span></span> |<span data-ttu-id="f9c21-163">Restituisce informazioni sugli eventi della sessione.</span><span class="sxs-lookup"><span data-stu-id="f9c21-163">Returns information about session events.</span></span> |
| <span data-ttu-id="f9c21-164">**sys.dm_xe_database_session_object_columns**</span><span class="sxs-lookup"><span data-stu-id="f9c21-164">**sys.dm_xe_database_session_object_columns**</span></span> |<span data-ttu-id="f9c21-165">Mostra i valori di configurazione hello per gli oggetti sessione tooa associato.</span><span class="sxs-lookup"><span data-stu-id="f9c21-165">Shows hello configuration values for objects that are bound tooa session.</span></span> |
| <span data-ttu-id="f9c21-166">**sys.dm_xe_database_session_targets**</span><span class="sxs-lookup"><span data-stu-id="f9c21-166">**sys.dm_xe_database_session_targets**</span></span> |<span data-ttu-id="f9c21-167">Restituisce informazioni sulle destinazioni della sessione.</span><span class="sxs-lookup"><span data-stu-id="f9c21-167">Returns information about session targets.</span></span> |
| <span data-ttu-id="f9c21-168">**sys.dm_xe_database_sessions**</span><span class="sxs-lookup"><span data-stu-id="f9c21-168">**sys.dm_xe_database_sessions**</span></span> |<span data-ttu-id="f9c21-169">Restituisce una riga per ogni sessione di eventi che è toohello con ambito di database corrente.</span><span class="sxs-lookup"><span data-stu-id="f9c21-169">Returns a row for each event session that is scoped toohello current database.</span></span> |

<span data-ttu-id="f9c21-170">In Microsoft SQL Server, sono denominate simile viste del catalogo senza hello  *\_database* parte hello nome, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="f9c21-170">In Microsoft SQL Server, similar catalog views are named without hello *\_database* portion of hello name, such as:</span></span>

- <span data-ttu-id="f9c21-171">**sys.dm_xe_sessions**, anziché il nome</span><span class="sxs-lookup"><span data-stu-id="f9c21-171">**sys.dm_xe_sessions**, instead of name</span></span><br/><span data-ttu-id="f9c21-172">**sys.dm_xe_database_sessions**.</span><span class="sxs-lookup"><span data-stu-id="f9c21-172">**sys.dm_xe_database_sessions**.</span></span>

### <a name="dmvs-common-tooboth"></a><span data-ttu-id="f9c21-173">Tooboth comuni viste a gestione dinamica</span><span class="sxs-lookup"><span data-stu-id="f9c21-173">DMVs common tooboth</span></span>
<span data-ttu-id="f9c21-174">Per gli eventi estesi sono disponibili le DMV aggiuntive che sono comuni tooboth Database SQL di Azure e Microsoft SQL Server:</span><span class="sxs-lookup"><span data-stu-id="f9c21-174">For extended events there are additional DMVs that are common tooboth Azure SQL Database and Microsoft SQL Server:</span></span>

- <span data-ttu-id="f9c21-175">**sys.dm_xe_map_values**</span><span class="sxs-lookup"><span data-stu-id="f9c21-175">**sys.dm_xe_map_values**</span></span>
- <span data-ttu-id="f9c21-176">**sys.dm_xe_object_columns**</span><span class="sxs-lookup"><span data-stu-id="f9c21-176">**sys.dm_xe_object_columns**</span></span>
- <span data-ttu-id="f9c21-177">**sys.dm_xe_objects**</span><span class="sxs-lookup"><span data-stu-id="f9c21-177">**sys.dm_xe_objects**</span></span>
- <span data-ttu-id="f9c21-178">**sys.dm_xe_packages**</span><span class="sxs-lookup"><span data-stu-id="f9c21-178">**sys.dm_xe_packages**</span></span>

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-hello-available-extended-events-actions-and-targets"></a><span data-ttu-id="f9c21-179">Trovare gli eventi estesi disponibili hello, azioni e destinazioni</span><span class="sxs-lookup"><span data-stu-id="f9c21-179">Find hello available extended events, actions, and targets</span></span>

<span data-ttu-id="f9c21-180">È possibile eseguire un semplice database SQL **selezionare** tooobtain un elenco di eventi disponibili hello, azioni e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="f9c21-180">You can run a simple SQL **SELECT** tooobtain a list of hello available events, actions, and target.</span></span>

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


<span data-ttu-id="f9c21-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a>&nbsp;</span><span class="sxs-lookup"><span data-stu-id="f9c21-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span></span>

## <a name="targets-for-your-sql-database-event-sessions"></a><span data-ttu-id="f9c21-182">Destinazioni per le sessioni di eventi del database SQL</span><span class="sxs-lookup"><span data-stu-id="f9c21-182">Targets for your SQL Database event sessions</span></span>

<span data-ttu-id="f9c21-183">Di seguito si trovano le destinazioni che possono acquisire i risultati dalle sessioni di eventi nel database SQL:</span><span class="sxs-lookup"><span data-stu-id="f9c21-183">Here are targets that can capture results from your event sessions on SQL Database:</span></span>

- <span data-ttu-id="f9c21-184">[Destinazione buffer circolare](http://msdn.microsoft.com/library/ff878182.aspx) : contiene per un tempo breve i dati degli eventi nella memoria.</span><span class="sxs-lookup"><span data-stu-id="f9c21-184">[Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx) - Briefly holds event data in memory.</span></span>
- <span data-ttu-id="f9c21-185">[Destinazione contatore eventi](http://msdn.microsoft.com/library/ff878025.aspx) : conta tutti gli eventi che si verificano durante una sessione di eventi estesi.</span><span class="sxs-lookup"><span data-stu-id="f9c21-185">[Event Counter target](http://msdn.microsoft.com/library/ff878025.aspx) - Counts all events that occur during an extended events session.</span></span>
- <span data-ttu-id="f9c21-186">[Destinazione File di eventi](http://msdn.microsoft.com/library/ff878115.aspx) -contenitore di archiviazione di Azure tooan di buffer completi scritture.</span><span class="sxs-lookup"><span data-stu-id="f9c21-186">[Event File target](http://msdn.microsoft.com/library/ff878115.aspx) - Writes complete buffers tooan Azure Storage container.</span></span>

<span data-ttu-id="f9c21-187">Hello [traccia eventi per Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API non è disponibile per gli eventi estesi nel Database SQL.</span><span class="sxs-lookup"><span data-stu-id="f9c21-187">hello [Event Tracing for Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API is not available for extended events on SQL Database.</span></span>

## <a name="restrictions"></a><span data-ttu-id="f9c21-188">Restrizioni</span><span class="sxs-lookup"><span data-stu-id="f9c21-188">Restrictions</span></span>

<span data-ttu-id="f9c21-189">Esistono alcune differenze relative alla sicurezza befitting ambiente cloud hello del Database SQL:</span><span class="sxs-lookup"><span data-stu-id="f9c21-189">There are a couple of security-related differences befitting hello cloud environment of SQL Database:</span></span>

- <span data-ttu-id="f9c21-190">Eventi estesi sono fondati sul modello di isolamento single-tenant hello.</span><span class="sxs-lookup"><span data-stu-id="f9c21-190">Extended events are founded on hello single-tenant isolation model.</span></span> <span data-ttu-id="f9c21-191">Una sessione di eventi in un database non può accedere a dati o eventi da un altro database.</span><span class="sxs-lookup"><span data-stu-id="f9c21-191">An event session in one database cannot access data or events from another database.</span></span>
- <span data-ttu-id="f9c21-192">Non è possibile eseguire un **CREATE EVENT SESSION** istruzione nel contesto di hello di hello **master** database.</span><span class="sxs-lookup"><span data-stu-id="f9c21-192">You cannot issue a **CREATE EVENT SESSION** statement in hello context of hello **master** database.</span></span>

## <a name="permission-model"></a><span data-ttu-id="f9c21-193">Modello di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="f9c21-193">Permission model</span></span>

<span data-ttu-id="f9c21-194">È necessario disporre di **controllo** tooissue database hello l'autorizzazione per un **CREATE EVENT SESSION** istruzione.</span><span class="sxs-lookup"><span data-stu-id="f9c21-194">You must have **Control** permission on hello database tooissue a **CREATE EVENT SESSION** statement.</span></span> <span data-ttu-id="f9c21-195">Hello proprietario del database (dbo) dispone **controllo** autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="f9c21-195">hello database owner (dbo) has **Control** permission.</span></span>

### <a name="storage-container-authorizations"></a><span data-ttu-id="f9c21-196">Autorizzazioni del contenitore di archiviazione</span><span class="sxs-lookup"><span data-stu-id="f9c21-196">Storage container authorizations</span></span>

<span data-ttu-id="f9c21-197">token SAS Hello generare per il contenitore di archiviazione di Azure è necessario specificare **rwl** per le autorizzazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="f9c21-197">hello SAS token you generate for your Azure Storage container must specify **rwl** for hello permissions.</span></span> <span data-ttu-id="f9c21-198">Hello **rwl** valore fornisce hello queste autorizzazioni:</span><span class="sxs-lookup"><span data-stu-id="f9c21-198">hello **rwl** value provides hello following permissions:</span></span>

- <span data-ttu-id="f9c21-199">Lettura</span><span class="sxs-lookup"><span data-stu-id="f9c21-199">Read</span></span>
- <span data-ttu-id="f9c21-200">Scrittura</span><span class="sxs-lookup"><span data-stu-id="f9c21-200">Write</span></span>
- <span data-ttu-id="f9c21-201">Elenco</span><span class="sxs-lookup"><span data-stu-id="f9c21-201">List</span></span>

## <a name="performance-considerations"></a><span data-ttu-id="f9c21-202">Considerazioni sulle prestazioni</span><span class="sxs-lookup"><span data-stu-id="f9c21-202">Performance considerations</span></span>

<span data-ttu-id="f9c21-203">Esistono scenari in cui un uso intensivo di eventi estesi può accumularsi più attivi di memoria maggiore di quella integro per hello generali del sistema.</span><span class="sxs-lookup"><span data-stu-id="f9c21-203">There are scenarios where intensive use of extended events can accumulate more active memory than is healthy for hello overall system.</span></span> <span data-ttu-id="f9c21-204">Pertanto hello sistema di Database SQL di Azure in modo dinamico imposta e consente di regolare i limiti di memoria attiva che può essere accumulata da una sessione eventi all'ammontare hello.</span><span class="sxs-lookup"><span data-stu-id="f9c21-204">Therefore hello Azure SQL Database system dynamically sets and adjusts limits on hello amount of active memory that can be accumulated by an event session.</span></span> <span data-ttu-id="f9c21-205">Diversi fattori contribuiscono a calcolo dinamico hello.</span><span class="sxs-lookup"><span data-stu-id="f9c21-205">Many factors go into hello dynamic calculation.</span></span>

<span data-ttu-id="f9c21-206">Se si riceve un messaggio di errore che indica che è stato applicato un massimo di memoria, alcune azioni correttive da eseguire sono:</span><span class="sxs-lookup"><span data-stu-id="f9c21-206">If you receive an error message that says a memory maximum was enforced, some corrective actions you can take are:</span></span>

- <span data-ttu-id="f9c21-207">Eseguire meno sessioni di eventi simultanee.</span><span class="sxs-lookup"><span data-stu-id="f9c21-207">Run fewer concurrent event sessions.</span></span>
- <span data-ttu-id="f9c21-208">Tramite il **crea** e **ALTER** istruzioni per le sessioni di eventi, è possibile ridurre hello di memoria specificate su hello **MAX\_memoria** clausola.</span><span class="sxs-lookup"><span data-stu-id="f9c21-208">Through your **CREATE** and **ALTER** statements for event sessions, reduce hello amount of memory you specify on hello **MAX\_MEMORY** clause.</span></span>

### <a name="network-latency"></a><span data-ttu-id="f9c21-209">Latenza di rete</span><span class="sxs-lookup"><span data-stu-id="f9c21-209">Network latency</span></span>

<span data-ttu-id="f9c21-210">Hello **File evento** destinazione potrebbe riscontrare latenza di rete o errori durante la persistenza dei dati tooAzure, archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="f9c21-210">hello **Event File** target might experience network latency or failures while persisting data tooAzure Storage blobs.</span></span> <span data-ttu-id="f9c21-211">Altri eventi nel Database SQL potrebbero essere ritardati in quanto in attesa per toocomplete di comunicazione di rete hello.</span><span class="sxs-lookup"><span data-stu-id="f9c21-211">Other events in SQL Database might be delayed while they wait for hello network communication toocomplete.</span></span> <span data-ttu-id="f9c21-212">Questo ritardo può rallentare il carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f9c21-212">This delay can slow your workload.</span></span>

- <span data-ttu-id="f9c21-213">toomitigate questo prestazioni dei rischi, evitare di impostare hello **EVENT_RETENTION_MODE** opzione troppo**NO_EVENT_LOSS** nelle definizioni di sessione di eventi.</span><span class="sxs-lookup"><span data-stu-id="f9c21-213">toomitigate this performance risk, avoid setting hello **EVENT_RETENTION_MODE** option too**NO_EVENT_LOSS** in your event session definitions.</span></span>

## <a name="related-links"></a><span data-ttu-id="f9c21-214">Collegamenti correlati</span><span class="sxs-lookup"><span data-stu-id="f9c21-214">Related links</span></span>

- <span data-ttu-id="f9c21-215">[Uso di Azure PowerShell con Archiviazione di Azure](../storage/common/storage-powershell-guide-full.md)</span><span class="sxs-lookup"><span data-stu-id="f9c21-215">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span>
- [<span data-ttu-id="f9c21-216">Cmdlet di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="f9c21-216">Azure Storage Cmdlets</span></span>](http://msdn.microsoft.com/library/dn806401.aspx)
- <span data-ttu-id="f9c21-217">[Con Azure PowerShell con l'archiviazione di Azure](../storage/common/storage-powershell-guide-full.md) -include informazioni complete su PowerShell e hello servizio di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c21-217">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and hello Azure Storage service.</span></span>
- [<span data-ttu-id="f9c21-218">Come toouse archiviazione Blob da .NET</span><span class="sxs-lookup"><span data-stu-id="f9c21-218">How toouse Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [<span data-ttu-id="f9c21-219">CREATE CREDENTIAL (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="f9c21-219">CREATE CREDENTIAL (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/ms189522.aspx)
- [<span data-ttu-id="f9c21-220">CREARE LA SESSIONE DI EVENTI (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="f9c21-220">CREATE EVENT SESSION (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/bb677289.aspx)
- [<span data-ttu-id="f9c21-221">Post del blog di Jonathan Kehayias sugli eventi estesi in Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="f9c21-221">Jonathan Kehayias' blog posts about extended events in Microsoft SQL Server</span></span>](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- <span data-ttu-id="f9c21-222">Hello Azure *gli aggiornamenti del servizio* pagina Web, circoscritta con parametro tooAzure Database SQL:</span><span class="sxs-lookup"><span data-stu-id="f9c21-222">hello Azure *Service Updates* webpage, narrowed by parameter tooAzure SQL Database:</span></span>
    - [<span data-ttu-id="f9c21-223">https://azure.microsoft.com/updates/?service=sql-database</span><span class="sxs-lookup"><span data-stu-id="f9c21-223">https://azure.microsoft.com/updates/?service=sql-database</span></span>](https://azure.microsoft.com/updates/?service=sql-database)


<span data-ttu-id="f9c21-224">Altri argomenti di esempio di codice per gli eventi estesi sono disponibili in hello seguenti collegamenti.</span><span class="sxs-lookup"><span data-stu-id="f9c21-224">Other code sample topics for extended events are available at hello following links.</span></span> <span data-ttu-id="f9c21-225">Tuttavia, è necessario controllare regolarmente toosee qualsiasi esempio se l'esempio hello è destinato a Microsoft SQL Server e Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c21-225">However, you must routinely check any sample toosee whether hello sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="f9c21-226">È possibile quindi decidere se modifiche di lieve entità sono: esempio hello toorun necessari.</span><span class="sxs-lookup"><span data-stu-id="f9c21-226">Then you can decide whether minor changes are needed toorun hello sample.</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
