---
title: codice di Buffer circolare per il Database SQL aaaXEvent | Documenti Microsoft
description: Fornisce un esempio di codice Transact-SQL che viene eseguito in modo semplice e rapido mediante l'utilizzo di destinazione Buffer circolare hello, nel Database di SQL Azure.
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: 2510fb3f-c8f2-437a-8f49-9d5f6c96e75b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genemi
ms.openlocfilehash: 21df748d9999d6837d2b5bbe4a3f47fb351b4633
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="ring-buffer-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="40b77-103">Codice di destinazione del buffer circolare per gli eventi estesi nel database SQL</span><span class="sxs-lookup"><span data-stu-id="40b77-103">Ring Buffer target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="40b77-104">Si desidera un esempio di codice completo per hello più semplice rapidamente toocapture e segnalare le informazioni per un evento esteso durante un test.</span><span class="sxs-lookup"><span data-stu-id="40b77-104">You want a complete code sample for hello easiest quick way toocapture and report information for an extended event during a test.</span></span> <span data-ttu-id="40b77-105">destinazione più semplice di Hello per i dati degli eventi estesi è hello [destinazione Buffer circolare](http://msdn.microsoft.com/library/ff878182.aspx).</span><span class="sxs-lookup"><span data-stu-id="40b77-105">hello easiest target for extended event data is hello [Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx).</span></span>

<span data-ttu-id="40b77-106">In questo argomento viene presentato un esempio di codice Transact-SQL che:</span><span class="sxs-lookup"><span data-stu-id="40b77-106">This topic presents a Transact-SQL code sample that:</span></span>

1. <span data-ttu-id="40b77-107">Crea una tabella con dati toodemonstrate con.</span><span class="sxs-lookup"><span data-stu-id="40b77-107">Creates a table with data toodemonstrate with.</span></span>
2. <span data-ttu-id="40b77-108">Crea una sessione per un evento esteso esistente, ovvero **sqlserver.sql_statement_starting**.</span><span class="sxs-lookup"><span data-stu-id="40b77-108">Creates a session for an existing extended event, namely **sqlserver.sql_statement_starting**.</span></span>
   
   * <span data-ttu-id="40b77-109">evento Hello è limitato tooSQL istruzioni contenenti una determinata stringa di aggiornamento: **istruzione come '% aggiornamento tabEmployee %'**.</span><span class="sxs-lookup"><span data-stu-id="40b77-109">hello event is limited tooSQL statements that contain a particular Update string: **statement LIKE '%UPDATE tabEmployee%'**.</span></span>
   * <span data-ttu-id="40b77-110">Sceglie output di hello toosend della destinazione di tooa hello evento di tipo Buffer circolare, vale a dire **package0.ring_buffer**.</span><span class="sxs-lookup"><span data-stu-id="40b77-110">Chooses toosend hello output of hello event tooa target of type Ring Buffer, namely  **package0.ring_buffer**.</span></span>
3. <span data-ttu-id="40b77-111">Avvia una sessione di eventi hello.</span><span class="sxs-lookup"><span data-stu-id="40b77-111">Starts hello event session.</span></span>
4. <span data-ttu-id="40b77-112">Esegue un paio di semplici istruzioni SQL UPDATE.</span><span class="sxs-lookup"><span data-stu-id="40b77-112">Issues a couple of simple SQL UPDATE statements.</span></span>
5. <span data-ttu-id="40b77-113">Rilascia un SQL SELECT istruzione tooretrieve evento output di hello Buffer circolare.</span><span class="sxs-lookup"><span data-stu-id="40b77-113">Issues a SQL SELECT statement tooretrieve event output from hello Ring Buffer.</span></span>
   
   * <span data-ttu-id="40b77-114">**sys.dm_xe_database_session_targets** e altre viste a gestione dinamica (DMV) sono unite.</span><span class="sxs-lookup"><span data-stu-id="40b77-114">**sys.dm_xe_database_session_targets** and other dynamic management views (DMVs) are joined.</span></span>
6. <span data-ttu-id="40b77-115">Arresta sessione dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="40b77-115">Stops hello event session.</span></span>
7. <span data-ttu-id="40b77-116">Elimina hello destinazione Buffer circolare, toorelease relative risorse.</span><span class="sxs-lookup"><span data-stu-id="40b77-116">Drops hello Ring Buffer target, toorelease its resources.</span></span>
8. <span data-ttu-id="40b77-117">Elimina la sessione di eventi hello e tabella demo hello.</span><span class="sxs-lookup"><span data-stu-id="40b77-117">Drops hello event session and hello demo table.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40b77-118">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="40b77-118">Prerequisites</span></span>

* <span data-ttu-id="40b77-119">Un account e una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="40b77-119">An Azure account and subscription.</span></span> <span data-ttu-id="40b77-120">È possibile iscriversi per una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="40b77-120">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="40b77-121">Qualsiasi database in cui è possibile creare una tabella.</span><span class="sxs-lookup"><span data-stu-id="40b77-121">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="40b77-122">Facoltativamente, è possibile [creare un database dimostrativo **AdventureWorksLT**](sql-database-get-started.md) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="40b77-122">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="40b77-123">SQL Server Management Studio (ssms.exe), idealmente l'ultima versione di aggiornamento mensile.</span><span class="sxs-lookup"><span data-stu-id="40b77-123">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="40b77-124">È possibile scaricare hello ssms.exe più recenti da:</span><span class="sxs-lookup"><span data-stu-id="40b77-124">You can download hello latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="40b77-125">Argomento intitolato [SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="40b77-125">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="40b77-126">Download di toohello un collegamento diretto.</span><span class="sxs-lookup"><span data-stu-id="40b77-126">A direct link toohello download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)

## <a name="code-sample"></a><span data-ttu-id="40b77-127">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="40b77-127">Code sample</span></span>

<span data-ttu-id="40b77-128">Con molto piccola modifica, hello nell'esempio di codice seguente Buffer circolare può avvenire in Database SQL di Azure o Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="40b77-128">With very minor modification, hello following Ring Buffer code sample can be run on either Azure SQL Database or Microsoft SQL Server.</span></span> <span data-ttu-id="40b77-129">differenza Hello è la presenza di hello del nodo hello nel nome hello di alcune viste a gestione dinamica (DMV), "database" utilizzata nella clausola FROM hello nel passaggio 5.</span><span class="sxs-lookup"><span data-stu-id="40b77-129">hello difference is hello presence of hello node '_database' in hello name of some dynamic management views (DMVs), used in hello FROM clause in Step 5.</span></span> <span data-ttu-id="40b77-130">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="40b77-130">For example:</span></span>

* <span data-ttu-id="40b77-131">sys.dm_xe**_database**_session_targets</span><span class="sxs-lookup"><span data-stu-id="40b77-131">sys.dm_xe**_database**_session_targets</span></span>
* <span data-ttu-id="40b77-132">sys.dm_xe_session_targets</span><span class="sxs-lookup"><span data-stu-id="40b77-132">sys.dm_xe_session_targets</span></span>

&nbsp;

```sql
GO
----  Transact-SQL.
---- Step set 1.

SET NOCOUNT ON;
GO


IF EXISTS
    (SELECT * FROM sys.objects
        WHERE type = 'U' and name = 'tabEmployee')
BEGIN
    DROP TABLE tabEmployee;
END
GO


CREATE TABLE tabEmployee
(
    EmployeeGuid         uniqueIdentifier   not null  default newid()  primary key,
    EmployeeId           int                not null  identity(1,1),
    EmployeeKudosCount   int                not null  default 0,
    EmployeeDescr        nvarchar(256)          null
);
GO


INSERT INTO tabEmployee ( EmployeeDescr )
    VALUES ( 'Jane Doe' );
GO

---- Step set 2.


IF EXISTS
    (SELECT * from sys.database_event_sessions
        WHERE name = 'eventsession_gm_azuresqldb51')
BEGIN
    DROP EVENT SESSION eventsession_gm_azuresqldb51
        ON DATABASE;
END
GO


CREATE
    EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD EVENT
        sqlserver.sql_statement_starting
            (
            ACTION (sqlserver.sql_text)
            WHERE statement LIKE '%UPDATE tabEmployee%'
            )
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
GO

---- Step set 3.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = START;
GO

---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
GO

---- Step set 5.


SELECT
    se.name                      AS [session-name],
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source,
    st.target_data,
    CAST(st.target_data AS XML)  AS [target_data_XML]
FROM
               sys.dm_xe_database_session_event_actions  AS ac

    INNER JOIN sys.dm_xe_database_session_events         AS ev  ON ev.event_name = ac.event_name
        AND CAST(ev.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_object_columns AS oc
         ON CAST(oc.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_targets        AS st
         ON CAST(st.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_sessions               AS se
         ON CAST(ac.event_session_address AS BINARY(8)) = CAST(se.address AS BINARY(8))
WHERE
        oc.column_name = 'occurrence_number'
    AND
        se.name        = 'eventsession_gm_azuresqldb51'
    AND
        ac.action_name = 'sql_text'
ORDER BY
    se.name,
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source
;
GO

---- Step set 6.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = STOP;
GO

---- Step set 7.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO

---- Step set 8.


DROP EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE;
GO

DROP TABLE tabEmployee;
GO
```


&nbsp;

## <a name="ring-buffer-contents"></a><span data-ttu-id="40b77-133">Contenuto del buffer circolare</span><span class="sxs-lookup"><span data-stu-id="40b77-133">Ring Buffer contents</span></span>

<span data-ttu-id="40b77-134">Nell'esempio di codice hello ssms.exe toorun è stato utilizzato.</span><span class="sxs-lookup"><span data-stu-id="40b77-134">We used ssms.exe toorun hello code sample.</span></span>

<span data-ttu-id="40b77-135">risultati di hello tooview, si fa clic su cella hello sotto l'intestazione di colonna hello **target_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="40b77-135">tooview hello results, we clicked hello cell under hello column header **target_data_XML**.</span></span>

<span data-ttu-id="40b77-136">Quindi nel riquadro dei risultati di hello è fatto clic su cella hello sotto l'intestazione di colonna hello **target_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="40b77-136">Then in hello results pane we clicked hello cell under hello column header **target_data_XML**.</span></span> <span data-ttu-id="40b77-137">Fare clic su Create un'altra scheda di file in ssms.exe in cui hello è stato visualizzato il contenuto della cella risultato hello, come XML.</span><span class="sxs-lookup"><span data-stu-id="40b77-137">This click created another file tab in ssms.exe in which hello content of hello result cell was displayed, as XML.</span></span>

<span data-ttu-id="40b77-138">output di Hello è illustrato nella seguente blocco hello.</span><span class="sxs-lookup"><span data-stu-id="40b77-138">hello output is shown in hello following block.</span></span> <span data-ttu-id="40b77-139">Sembra lungo, ma è composto solo da due elementi **<event>** .</span><span class="sxs-lookup"><span data-stu-id="40b77-139">It looks long, but it is just two **<event>** elements.</span></span>

&nbsp;

```
<RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="2" eventCount="2" droppedCount="0" memoryUsed="1728">
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.317Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>7</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>184</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>328</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.327Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>10</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>340</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>486</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
</RingBufferTarget>
```


#### <a name="release-resources-held-by-your-ring-buffer"></a><span data-ttu-id="40b77-140">Rilasciare le risorse usate dal buffer circolare</span><span class="sxs-lookup"><span data-stu-id="40b77-140">Release resources held by your Ring Buffer</span></span>

<span data-ttu-id="40b77-141">Una volta con il Buffer circolare, è possibile rimuoverla e rilasciare le risorse di emissione di un **ALTER** simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="40b77-141">When you are done with your Ring Buffer, you can remove it and release its resources issuing an **ALTER** like hello following:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO
```


<span data-ttu-id="40b77-142">definizione di Hello della sessione di eventi è aggiornato, ma non è stato eliminato.</span><span class="sxs-lookup"><span data-stu-id="40b77-142">hello definition of your event session is updated, but not dropped.</span></span> <span data-ttu-id="40b77-143">Successivamente è possibile aggiungere un'altra istanza di una sessione di eventi tooyour Buffer circolare hello:</span><span class="sxs-lookup"><span data-stu-id="40b77-143">Later you can add another instance of hello Ring Buffer tooyour event session:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
```


## <a name="more-information"></a><span data-ttu-id="40b77-144">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="40b77-144">More information</span></span>

<span data-ttu-id="40b77-145">Hello argomento principale per gli eventi estesi nel Database SQL Azure sono:</span><span class="sxs-lookup"><span data-stu-id="40b77-145">hello primary topic for extended events on Azure SQL Database is:</span></span>

* <span data-ttu-id="40b77-146">[Considerazioni sugli eventi estesi nel database SQL](sql-database-xevent-db-diff-from-svr.md), che illustra alcuni aspetti degli eventi estesi che presentano differenze tra il database SQL di Azure e Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="40b77-146">[Extended event considerations in SQL Database](sql-database-xevent-db-diff-from-svr.md), which contrasts some aspects of extended events that differ between Azure SQL Database versus Microsoft SQL Server.</span></span>

<span data-ttu-id="40b77-147">Altri argomenti di esempio di codice per gli eventi estesi sono disponibili in hello seguenti collegamenti.</span><span class="sxs-lookup"><span data-stu-id="40b77-147">Other code sample topics for extended events are available at hello following links.</span></span> <span data-ttu-id="40b77-148">Tuttavia, è necessario controllare regolarmente toosee qualsiasi esempio se l'esempio hello è destinato a Microsoft SQL Server e Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="40b77-148">However, you must routinely check any sample toosee whether hello sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="40b77-149">È possibile quindi decidere se modifiche di lieve entità sono: esempio hello toorun necessari.</span><span class="sxs-lookup"><span data-stu-id="40b77-149">Then you can decide whether minor changes are needed toorun hello sample.</span></span>

* <span data-ttu-id="40b77-150">Esempio di codice per il database SQL di Azure: [codice di destinazione del file evento per gli eventi estesi nel database SQL](sql-database-xevent-code-event-file.md)</span><span class="sxs-lookup"><span data-stu-id="40b77-150">Code sample for Azure SQL Database: [Event File target code for extended events in SQL Database](sql-database-xevent-code-event-file.md)</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
