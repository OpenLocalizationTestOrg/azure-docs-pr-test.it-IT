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
# <a name="extended-events-in-sql-database"></a>Eventi estesi nel database SQL
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

In questo argomento viene illustrato come implementazione di hello degli eventi estesi nel Database di SQL Azure è leggermente diverso tooextended confrontati gli eventi in Microsoft SQL Server.

- Database SQL V12 acquisita funzionalità di eventi estesi hello hello seconda metà del calendario 2015.
- SQL Server ha gli eventi estesi dal 2008.
- set di funzionalità Hello degli eventi estesi nel Database SQL è un subset affidabile di funzionalità hello in SQL Server.

*XEvent* è un nome alternativo informale utilizzato talvolta per "eventi estesi" in blog e altri percorsi informali.

Per altre informazioni sugli eventi estesi, per il database SQL di Azure e Microsoft SQL Server, vedere l'articolo:

- [Quick Start: Extended events in SQL Server](http://msdn.microsoft.com/library/mt733217.aspx)
- [Eventi estesi](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a>Prerequisiti

In questo argomento si presuppone che si dispone già di una conoscenza di:

- [Servizio Azure SQL Database](https://azure.microsoft.com/services/sql-database/)
- [Eventi estesi](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.

- bulk Hello di documentazione sugli eventi estesi applica tooboth SQL Server e Database SQL.

Esposizione precedente toohello elementi è utile quando si scelgono i File di eventi come hello hello [destinazione](#AzureXEventsTargets):

- [Servizio di Archiviazione di Azure](https://azure.microsoft.com/services/storage/)


- PowerShell
    - [Con Azure PowerShell con l'archiviazione di Azure](../storage/common/storage-powershell-guide-full.md) -include informazioni complete su PowerShell e hello servizio di archiviazione di Azure.

## <a name="code-samples"></a>Esempi di codice

Gli argomenti correlati forniscono due esempi di codice:


- [Codice di destinazione del buffer circolare per eventi estesi nel database SQL](sql-database-xevent-code-ring-buffer.md)
    - Breve script Transact-SQL semplice.
    - Lo sottolineiamo in argomento di esempio di codice hello che, una volta con una destinazione Buffer circolare, è necessario rilasciare le risorse eseguendo un rilascio alter `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` istruzione. Successivamente è possibile aggiungere un'altra istanza del buffer circolare da `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.


- [Codice di destinazione del file evento per eventi estesi nel database SQL](sql-database-xevent-code-event-file.md)
    - Fase 1 è PowerShell toocreate un contenitore di archiviazione di Azure.
    - Fase 2 è Transact-SQL che utilizza il contenitore di archiviazione di Azure hello.

## <a name="transact-sql-differences"></a>Differenze di Transact-SQL


- Quando si esegue hello [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) comando in SQL Server, utilizzare hello **ON SERVER** clausola. Ma nel Database SQL è utilizzare hello **ON DATABASE** clausola invece.


- Hello **ON DATABASE** clausola si applica anche toohello [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) e [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) comandi Transact-SQL.


- Una procedura consigliata è l'opzione della sessione eventi hello tooinclude di **STARTUP_STATE = ON** nel **CREATE EVENT SESSION** o **ALTER EVENT SESSION** istruzioni.
    - Hello **= ON** valore supporta un riavvio automatico dopo una riconfigurazione del database logico di hello scadenza tooa failover.

## <a name="new-catalog-views"></a>Nuove viste del catalogo

Hello funzionalità eventi estesi è supportato da molti [viste del catalogo](http://msdn.microsoft.com/library/ms174365.aspx). Viste del catalogo forniscono informazioni sul *metadati o definizioni di* di sessioni eventi creati dall'utente nel database corrente hello. viste di Hello non restituiscono informazioni sulle istanze di sessioni eventi attivi.

| Nome della<br/>vista del catalogo | Descrizione |
|:--- |:--- |
| **sys.database_event_session_actions** |Restituisce una riga per ogni azione su ogni evento di una sessione di eventi. |
| **sys.database_event_session_events** |Restituisce una riga per ogni evento in una sessione di eventi. |
| **sys.database_event_session_fields** |Restituisce una riga per ogni colonna personalizzabile impostata in modo esplicito su eventi e destinazioni. |
| **sys.database_event_session_targets** |Restituisce una riga per ogni destinazione di evento per una sessione di eventi. |
| **sys.database_event_sessions** |Restituisce una riga per ogni sessione di eventi nel database di SQL Database hello. |

In Microsoft SQL Server le viste del catalogo simili hanno nomi che includono *.server\_* anziché *.database\_*. modello di nome Hello è ad esempio **sys.server_event_%**.

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a>[DMV](http://msdn.microsoft.com/library/ms188754.aspx)

Il database SQL di Azure include [viste a gestione dinamica (DMV)](http://msdn.microsoft.com/library/bb677293.aspx) che supportano gli eventi estesi. Le DMV indicano le sessioni di eventi *attive* .

| Nome della DMV | Descrizione |
|:--- |:--- |
| **sys.dm_xe_database_session_event_actions** |Restituisce informazioni sulle azioni della sessione di eventi. |
| **sys.dm_xe_database_session_events** |Restituisce informazioni sugli eventi della sessione. |
| **sys.dm_xe_database_session_object_columns** |Mostra i valori di configurazione hello per gli oggetti sessione tooa associato. |
| **sys.dm_xe_database_session_targets** |Restituisce informazioni sulle destinazioni della sessione. |
| **sys.dm_xe_database_sessions** |Restituisce una riga per ogni sessione di eventi che è toohello con ambito di database corrente. |

In Microsoft SQL Server, sono denominate simile viste del catalogo senza hello  *\_database* parte hello nome, ad esempio:

- **sys.dm_xe_sessions**, anziché il nome<br/>**sys.dm_xe_database_sessions**.

### <a name="dmvs-common-tooboth"></a>Tooboth comuni viste a gestione dinamica
Per gli eventi estesi sono disponibili le DMV aggiuntive che sono comuni tooboth Database SQL di Azure e Microsoft SQL Server:

- **sys.dm_xe_map_values**
- **sys.dm_xe_object_columns**
- **sys.dm_xe_objects**
- **sys.dm_xe_packages**

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-hello-available-extended-events-actions-and-targets"></a>Trovare gli eventi estesi disponibili hello, azioni e destinazioni

È possibile eseguire un semplice database SQL **selezionare** tooobtain un elenco di eventi disponibili hello, azioni e di destinazione.

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


<a name="AzureXEventsTargets" id="AzureXEventsTargets"></a>&nbsp;

## <a name="targets-for-your-sql-database-event-sessions"></a>Destinazioni per le sessioni di eventi del database SQL

Di seguito si trovano le destinazioni che possono acquisire i risultati dalle sessioni di eventi nel database SQL:

- [Destinazione buffer circolare](http://msdn.microsoft.com/library/ff878182.aspx) : contiene per un tempo breve i dati degli eventi nella memoria.
- [Destinazione contatore eventi](http://msdn.microsoft.com/library/ff878025.aspx) : conta tutti gli eventi che si verificano durante una sessione di eventi estesi.
- [Destinazione File di eventi](http://msdn.microsoft.com/library/ff878115.aspx) -contenitore di archiviazione di Azure tooan di buffer completi scritture.

Hello [traccia eventi per Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API non è disponibile per gli eventi estesi nel Database SQL.

## <a name="restrictions"></a>Restrizioni

Esistono alcune differenze relative alla sicurezza befitting ambiente cloud hello del Database SQL:

- Eventi estesi sono fondati sul modello di isolamento single-tenant hello. Una sessione di eventi in un database non può accedere a dati o eventi da un altro database.
- Non è possibile eseguire un **CREATE EVENT SESSION** istruzione nel contesto di hello di hello **master** database.

## <a name="permission-model"></a>Modello di autorizzazione

È necessario disporre di **controllo** tooissue database hello l'autorizzazione per un **CREATE EVENT SESSION** istruzione. Hello proprietario del database (dbo) dispone **controllo** autorizzazione.

### <a name="storage-container-authorizations"></a>Autorizzazioni del contenitore di archiviazione

token SAS Hello generare per il contenitore di archiviazione di Azure è necessario specificare **rwl** per le autorizzazioni di hello. Hello **rwl** valore fornisce hello queste autorizzazioni:

- Lettura
- Scrittura
- Elenco

## <a name="performance-considerations"></a>Considerazioni sulle prestazioni

Esistono scenari in cui un uso intensivo di eventi estesi può accumularsi più attivi di memoria maggiore di quella integro per hello generali del sistema. Pertanto hello sistema di Database SQL di Azure in modo dinamico imposta e consente di regolare i limiti di memoria attiva che può essere accumulata da una sessione eventi all'ammontare hello. Diversi fattori contribuiscono a calcolo dinamico hello.

Se si riceve un messaggio di errore che indica che è stato applicato un massimo di memoria, alcune azioni correttive da eseguire sono:

- Eseguire meno sessioni di eventi simultanee.
- Tramite il **crea** e **ALTER** istruzioni per le sessioni di eventi, è possibile ridurre hello di memoria specificate su hello **MAX\_memoria** clausola.

### <a name="network-latency"></a>Latenza di rete

Hello **File evento** destinazione potrebbe riscontrare latenza di rete o errori durante la persistenza dei dati tooAzure, archiviazione BLOB. Altri eventi nel Database SQL potrebbero essere ritardati in quanto in attesa per toocomplete di comunicazione di rete hello. Questo ritardo può rallentare il carico di lavoro.

- toomitigate questo prestazioni dei rischi, evitare di impostare hello **EVENT_RETENTION_MODE** opzione troppo**NO_EVENT_LOSS** nelle definizioni di sessione di eventi.

## <a name="related-links"></a>Collegamenti correlati

- [Uso di Azure PowerShell con Archiviazione di Azure](../storage/common/storage-powershell-guide-full.md)
- [Cmdlet di Archiviazione di Azure](http://msdn.microsoft.com/library/dn806401.aspx)
- [Con Azure PowerShell con l'archiviazione di Azure](../storage/common/storage-powershell-guide-full.md) -include informazioni complete su PowerShell e hello servizio di archiviazione di Azure.
- [Come toouse archiviazione Blob da .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [CREATE CREDENTIAL (Transact-SQL)](http://msdn.microsoft.com/library/ms189522.aspx)
- [CREARE LA SESSIONE DI EVENTI (Transact-SQL)](http://msdn.microsoft.com/library/bb677289.aspx)
- [Post del blog di Jonathan Kehayias sugli eventi estesi in Microsoft SQL Server](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- Hello Azure *gli aggiornamenti del servizio* pagina Web, circoscritta con parametro tooAzure Database SQL:
    - [https://azure.microsoft.com/updates/?service=sql-database](https://azure.microsoft.com/updates/?service=sql-database)


Altri argomenti di esempio di codice per gli eventi estesi sono disponibili in hello seguenti collegamenti. Tuttavia, è necessario controllare regolarmente toosee qualsiasi esempio se l'esempio hello è destinato a Microsoft SQL Server e Database SQL di Azure. È possibile quindi decidere se modifiche di lieve entità sono: esempio hello toorun necessari.

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
