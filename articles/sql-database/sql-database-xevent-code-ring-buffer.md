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
# <a name="ring-buffer-target-code-for-extended-events-in-sql-database"></a>Codice di destinazione del buffer circolare per gli eventi estesi nel database SQL

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

Si desidera un esempio di codice completo per hello più semplice rapidamente toocapture e segnalare le informazioni per un evento esteso durante un test. destinazione più semplice di Hello per i dati degli eventi estesi è hello [destinazione Buffer circolare](http://msdn.microsoft.com/library/ff878182.aspx).

In questo argomento viene presentato un esempio di codice Transact-SQL che:

1. Crea una tabella con dati toodemonstrate con.
2. Crea una sessione per un evento esteso esistente, ovvero **sqlserver.sql_statement_starting**.
   
   * evento Hello è limitato tooSQL istruzioni contenenti una determinata stringa di aggiornamento: **istruzione come '% aggiornamento tabEmployee %'**.
   * Sceglie output di hello toosend della destinazione di tooa hello evento di tipo Buffer circolare, vale a dire **package0.ring_buffer**.
3. Avvia una sessione di eventi hello.
4. Esegue un paio di semplici istruzioni SQL UPDATE.
5. Rilascia un SQL SELECT istruzione tooretrieve evento output di hello Buffer circolare.
   
   * **sys.dm_xe_database_session_targets** e altre viste a gestione dinamica (DMV) sono unite.
6. Arresta sessione dell'evento hello.
7. Elimina hello destinazione Buffer circolare, toorelease relative risorse.
8. Elimina la sessione di eventi hello e tabella demo hello.

## <a name="prerequisites"></a>Prerequisiti

* Un account e una sottoscrizione di Azure. È possibile iscriversi per una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Qualsiasi database in cui è possibile creare una tabella.
  
  * Facoltativamente, è possibile [creare un database dimostrativo **AdventureWorksLT**](sql-database-get-started.md) in pochi minuti.
* SQL Server Management Studio (ssms.exe), idealmente l'ultima versione di aggiornamento mensile. 
  È possibile scaricare hello ssms.exe più recenti da:
  
  * Argomento intitolato [SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).
  * [Download di toohello un collegamento diretto.](http://go.microsoft.com/fwlink/?linkid=616025)

## <a name="code-sample"></a>Esempio di codice

Con molto piccola modifica, hello nell'esempio di codice seguente Buffer circolare può avvenire in Database SQL di Azure o Microsoft SQL Server. differenza Hello è la presenza di hello del nodo hello nel nome hello di alcune viste a gestione dinamica (DMV), "database" utilizzata nella clausola FROM hello nel passaggio 5. ad esempio:

* sys.dm_xe**_database**_session_targets
* sys.dm_xe_session_targets

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

## <a name="ring-buffer-contents"></a>Contenuto del buffer circolare

Nell'esempio di codice hello ssms.exe toorun è stato utilizzato.

risultati di hello tooview, si fa clic su cella hello sotto l'intestazione di colonna hello **target_data_XML**.

Quindi nel riquadro dei risultati di hello è fatto clic su cella hello sotto l'intestazione di colonna hello **target_data_XML**. Fare clic su Create un'altra scheda di file in ssms.exe in cui hello è stato visualizzato il contenuto della cella risultato hello, come XML.

output di Hello è illustrato nella seguente blocco hello. Sembra lungo, ma è composto solo da due elementi **<event>** .

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


#### <a name="release-resources-held-by-your-ring-buffer"></a>Rilasciare le risorse usate dal buffer circolare

Una volta con il Buffer circolare, è possibile rimuoverla e rilasciare le risorse di emissione di un **ALTER** simile hello seguente:

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO
```


definizione di Hello della sessione di eventi è aggiornato, ma non è stato eliminato. Successivamente è possibile aggiungere un'altra istanza di una sessione di eventi tooyour Buffer circolare hello:

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
```


## <a name="more-information"></a>Altre informazioni

Hello argomento principale per gli eventi estesi nel Database SQL Azure sono:

* [Considerazioni sugli eventi estesi nel database SQL](sql-database-xevent-db-diff-from-svr.md), che illustra alcuni aspetti degli eventi estesi che presentano differenze tra il database SQL di Azure e Microsoft SQL Server.

Altri argomenti di esempio di codice per gli eventi estesi sono disponibili in hello seguenti collegamenti. Tuttavia, è necessario controllare regolarmente toosee qualsiasi esempio se l'esempio hello è destinato a Microsoft SQL Server e Database SQL di Azure. È possibile quindi decidere se modifiche di lieve entità sono: esempio hello toorun necessari.

* Esempio di codice per il database SQL di Azure: [codice di destinazione del file evento per gli eventi estesi nel database SQL](sql-database-xevent-code-event-file.md)

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
