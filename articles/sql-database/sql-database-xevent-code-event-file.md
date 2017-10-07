---
title: codice di File di eventi per il Database SQL aaaXEvent | Documenti Microsoft
description: "Fornisce PowerShell e Transact-SQL per un esempio di codice a due fasi di destinazione di File di evento hello in un evento esteso nel Database SQL Azure. Archiviazione di Azure è una parte necessaria di questo scenario."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: bbb10ecc-739f-4159-b844-12b4be161231
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: genemi
ms.openlocfilehash: 4457bd3250f4644b54da2f7daddb9da12070e93a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-file-target-code-for-extended-events-in-sql-database"></a>Codice di destinazione del file evento per eventi estesi nel database SQL

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

Si desidera un esempio di codice completo per una modo efficiente toocapture e segnalare le informazioni per un evento esteso.

In Microsoft SQL Server, hello [destinazione File evento](http://msdn.microsoft.com/library/ff878115.aspx) è output evento toostore utilizzati in un file di disco rigido locale. Tuttavia, tali file non sono disponibili tooAzure Database SQL. Invece utilizziamo destinazione di archiviazione di Azure servizio toosupport hello evento File hello.

Questo argomento presenta un esempio di codice in due fasi:

* PowerShell toocreate un contenitore di archiviazione di Azure nel cloud hello.
* Transact-SQL:
  
  * tooassign hello Azure Storage contenitore tooan evento destinazione File.
  * avvio e toocreate hello event session e così via.

## <a name="prerequisites"></a>Prerequisiti

* Un account e una sottoscrizione di Azure. È possibile iscriversi per una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Qualsiasi database in cui è possibile creare una tabella.
  
  * Facoltativamente, è possibile [creare un database dimostrativo **AdventureWorksLT**](sql-database-get-started.md) in pochi minuti.
* SQL Server Management Studio (ssms.exe), idealmente l'ultima versione di aggiornamento mensile. 
  È possibile scaricare hello ssms.exe più recenti da:
  
  * Argomento intitolato [SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).
  * [Download di toohello un collegamento diretto.](http://go.microsoft.com/fwlink/?linkid=616025)
* È necessario disporre di hello [moduli di Azure PowerShell](http://go.microsoft.com/?linkid=9811175) installato.
  
  * i moduli di Hello forniscono i comandi, ad esempio - **New AzureStorageAccount**.

## <a name="phase-1-powershell-code-for-azure-storage-container"></a>Fase 1: Codice di PowerShell per il contenitore di archiviazione di Azure

Questo PowerShell è la fase 1 dell'esempio di codice in due fasi hello.

script Hello viene avviato con i comandi tooclean dopo un precedente possibile eseguire e rerunnable.

1. Incollare uno script di PowerShell hello in un semplice editor di testo, ad esempio Notepad.exe e salvare script hello come un file con estensione hello **ps1**.
2. Avviare PowerShell ISE come amministratore.
3. Al prompt dei comandi hello, digitare<br/>`Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`<br/>e quindi premere INVIO.
4. In PowerShell ISE, aprire il file **.ps1** . Eseguire script hello.
5. script Hello primo avvio di una nuova finestra in cui si accede tooAzure.
   
   * Se si esegue nuovamente script hello senza interrompere la sessione, è possibile hello pratico commento hello **Add-AzureAccount** comando.

![PowerShell ISE, con il modulo Azure installato, script toorun pronto.][30_powershell_ise]


### <a name="powershell-code"></a>Codice PowerShell

```powershell
## TODO: Before running, find all 'TODO' and make each edit!!

#--------------- 1 -----------------------


# You can comment out or skip this Add-AzureAccount
# command after hello first run.
# Current PowerShell environment retains hello successful outcome.

'Expect a pop-up window in which you log in tooAzure.'


Add-AzureAccount

#-------------- 2 ------------------------


'
TODO: Edit hello values assigned toothese variables, especially hello first few!
'

# Ensure hello current date is between
# hello Expiry and Start time values that you edit here.

$subscriptionName    = 'YOUR_SUBSCRIPTION_NAME'
$policySasExpiryTime = '2016-01-28T23:44:56Z'
$policySasStartTime  = '2015-08-01'


$storageAccountName     = 'gmstorageaccountxevent'
$storageAccountLocation = 'West US'
$contextName            = 'gmcontext'
$containerName          = 'gmcontainerxevent'
$policySasToken         = 'gmpolicysastoken'


# Leave this value alone, as 'rwl'.
$policySasPermission = 'rwl'

#--------------- 3 -----------------------


# hello ending display lists your Azure subscriptions.
# One should match hello $subscriptionName value you assigned
#   earlier in this PowerShell script. 

'Choose an existing subscription for hello current PowerShell environment.'


Select-AzureSubscription -SubscriptionName $subscriptionName


#-------------- 4 ------------------------


'
Clean up hello old Azure Storage Account after any previous run, 
before continuing this new run.'


If ($storageAccountName)
{
    Remove-AzureStorageAccount -StorageAccountName $storageAccountName
}

#--------------- 5 -----------------------

[System.DateTime]::Now.ToString()

'
Create a storage account. 
This might take several minutes, will beep when ready.
  ...PLEASE WAIT...'

New-AzureStorageAccount `
    -StorageAccountName $storageAccountName `
    -Location           $storageAccountLocation

[System.DateTime]::Now.ToString()

[System.Media.SystemSounds]::Beep.Play()


'
Get hello primary access key for your storage account.
'


$primaryAccessKey_ForStorageAccount = `
    (Get-AzureStorageKey `
        -StorageAccountName $storageAccountName).Primary

"`$primaryAccessKey_ForStorageAccount = $primaryAccessKey_ForStorageAccount"

'Azure Storage Account cmdlet completed.
Remainder of PowerShell .ps1 script continues.
'

#--------------- 6 -----------------------


# hello context will be needed toocreate a container within hello storage account.

'Create a context object from hello storage account and its primary access key.
'

$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey  $primaryAccessKey_ForStorageAccount


'Create a container within hello storage account.
'


$containerObjectInStorageAccount = New-AzureStorageContainer `
    -Name    $containerName `
    -Context $context


'Create a security policy toobe applied toohello SAS token.
'

New-AzureStorageContainerStoredAccessPolicy `
    -Container  $containerName `
    -Context    $context `
    -Policy     $policySasToken `
    -Permission $policySasPermission `
    -ExpiryTime $policySasExpiryTime `
    -StartTime  $policySasStartTime 

'
Generate a SAS token for hello container.
'
Try
{
    $sasTokenWithPolicy = New-AzureStorageContainerSASToken `
        -Name    $containerName `
        -Context $context `
        -Policy  $policySasToken
}
Catch 
{
    $Error[0].Exception.ToString()
}

#-------------- 7 ------------------------


'Display hello values that YOU must edit into hello Transact-SQL script next!:
'

"storageAccountName: $storageAccountName"
"containerName:      $containerName"
"sasTokenWithPolicy: $sasTokenWithPolicy"

'
REMINDER: sasTokenWithPolicy here might start with "?" character, which you must exclude from Transact-SQL.
'

'
(Later, return here toodelete your Azure Storage account. See hello preceding - Remove-AzureStorageAccount -StorageAccountName $storageAccountName)'

'
Now shift toohello Transact-SQL portion of hello two-part code sample!'

# EOFile
```


Prendere nota di hello alcuni valori denominati che uno script di PowerShell hello stampa la fine. È necessario modificare tali valori in hello script Transact-SQL che segue come fase 2.

## <a name="phase-2-transact-sql-code-that-uses-azure-storage-container"></a>Fase 2: Codice Transact-SQL che utilizza il contenitore di Archiviazione di Azure

* Nella fase 1 di questo esempio di codice è stato eseguito un toocreate di script di PowerShell un contenitore di archiviazione di Azure.
* Successivamente nella fase 2, hello script Transact-SQL seguente è necessario utilizzare hello contenitore.

script Hello viene avviato con i comandi tooclean dopo un precedente possibile eseguire e rerunnable.

script di PowerShell Hello stampati alcuni valori denominati quando è terminato. È necessario modificare hello Transact-SQL script toouse tali valori. Trovare **TODO** in hello toolocate di script Transact-SQL hello punti di montaggio.

1. Aprire SQL Server Management Studio (ssms.exe).
2. La connessione a database di Database SQL di Azure tooyour.
3. Fare clic su tooopen un nuovo riquadro query.
4. Incollare lo script di Transact-SQL seguente nel riquadro query hello hello.
5. Trovare ogni **TODO** in hello script e apportare le modifiche appropriate hello.
6. Salvare e quindi eseguire script hello.


> [!WARNING]
> valore di chiave di firma di accesso condiviso generato da hello precedente script di PowerShell Hello potrebbe iniziare con un '?' (punto interrogativo). Quando si utilizza una chiave SAS hello in hello lo script T-SQL seguente, è necessario *rimuovere iniziali hello '?'* . Le attività in caso contrario potrebbero essere bloccate dalla protezione.


### <a name="transact-sql-code"></a>Codice Transact-SQL

```sql
---- TODO: First, run hello PowerShell portion of this two-part code sample.
---- TODO: Second, find every 'TODO' in this Transact-SQL file, and edit each.

---- Transact-SQL code for Event File target on Azure SQL Database.


SET NOCOUNT ON;
GO


----  Step 1.  Establish one little table, and  ---------
----  insert one row of data.


IF EXISTS
    (SELECT * FROM sys.objects
        WHERE type = 'U' and name = 'gmTabEmployee')
BEGIN
    DROP TABLE gmTabEmployee;
END
GO


CREATE TABLE gmTabEmployee
(
    EmployeeGuid         uniqueIdentifier   not null  default newid()  primary key,
    EmployeeId           int                not null  identity(1,1),
    EmployeeKudosCount   int                not null  default 0,
    EmployeeDescr        nvarchar(256)          null
);
GO


INSERT INTO gmTabEmployee ( EmployeeDescr )
    VALUES ( 'Jane Doe' );
GO


------  Step 2.  Create key, and  ------------
------  Create credential (your Azure Storage container must already exist).


IF NOT EXISTS
    (SELECT * FROM sys.symmetric_keys
        WHERE symmetric_key_id = 101)
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '0C34C960-6621-4682-A123-C7EA08E3FC46' -- Or any newid().
END
GO


IF EXISTS
    (SELECT * FROM sys.database_scoped_credentials
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        WHERE name = 'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent')
BEGIN
    DROP DATABASE SCOPED CREDENTIAL
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent] ;
END
GO


CREATE
    DATABASE SCOPED
    CREDENTIAL
        -- use '.blob.',   and not '.queue.' or '.table.' etc.
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    WITH
        IDENTITY = 'SHARED ACCESS SIGNATURE',  -- "SAS" token.
        -- TODO: Paste in hello long SasToken string here for Secret, but exclude any leading '?'.
        SECRET = 'sv=2014-02-14&sr=c&si=gmpolicysastoken&sig=EjAqjo6Nu5xMLEZEkMkLbeF7TD9v1J8DNB2t8gOKTts%3D'
    ;
GO


------  Step 3.  Create (define) an event session.  --------
------  hello event session has an event with an action,
------  and a has a target.

IF EXISTS
    (SELECT * from sys.database_event_sessions
        WHERE name = 'gmeventsessionname240b')
BEGIN
    DROP
        EVENT SESSION
            gmeventsessionname240b
        ON DATABASE;
END
GO


CREATE
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE

    ADD EVENT
        sqlserver.sql_statement_starting
            (
            ACTION (sqlserver.sql_text)
            WHERE statement LIKE 'UPDATE gmTabEmployee%'
            )
    ADD TARGET
        package0.event_file
            (
            -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
            -- Also, tweak hello .xel file name at end, if you like.
            SET filename =
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b.xel'
            )
    WITH
        (MAX_MEMORY = 10 MB,
        MAX_DISPATCH_LATENCY = 3 SECONDS)
    ;
GO


------  Step 4.  Start hello event session.  ----------------
------  Issue hello SQL Update statements that will be traced.
------  Then stop hello session.

------  Note: If hello target fails tooattach,
------  hello session must be stopped and restarted.

ALTER
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE
    STATE = START;
GO


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM gmTabEmployee;

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe';

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 13
    WHERE EmployeeDescr = 'Jane Doe';

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM gmTabEmployee;
GO


ALTER
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE
    STATE = STOP;
GO


-------------- Step 5.  Select hello results. ----------

SELECT
        *, 'CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS!' as [CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS],
        CAST(event_data AS XML) AS [event_data_XML]  -- TODO: In ssms.exe results grid, double-click this cell!
    FROM
        sys.fn_xe_file_target_read_file
            (
                -- TODO: Fill in Storage Account name, and hello associated Container name.
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b',
                null, null, null
            );
GO


-------------- Step 6.  Clean up. ----------

DROP
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE;
GO

DROP DATABASE SCOPED CREDENTIAL
    -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
    [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    ;
GO

DROP TABLE gmTabEmployee;
GO

PRINT 'Use PowerShell Remove-AzureStorageAccount toodelete your Azure Storage account!';
GO
```


Se la destinazione hello non riesce tooattach quando si esegue, è necessario arrestare e riavviare la sessione di eventi hello:

```sql
ALTER EVENT SESSION ... STATE = STOP;
GO
ALTER EVENT SESSION ... STATE = START;
GO
```


## <a name="output"></a>Output

Al termine dell'esecuzione hello script Transact-SQL, fare clic su una cella in hello **event_data_XML** intestazione di colonna. Viene visualizzato un elemento **<event>** che mostra un'istruzione UPDATE.

Di seguito è riportato un elemento **<event>** generato durante il test:


```xml
<event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T19:18:45.420Z">
  <data name="state">
    <value>0</value>
    <text>Normal</text>
  </data>
  <data name="line_number">
    <value>5</value>
  </data>
  <data name="offset">
    <value>148</value>
  </data>
  <data name="offset_end">
    <value>368</value>
  </data>
  <data name="statement">
    <value>UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe'</value>
  </data>
  <action name="sql_text" package="sqlserver">
    <value>

SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM gmTabEmployee;

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe';

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 13
    WHERE EmployeeDescr = 'Jane Doe';

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM gmTabEmployee;
</value>
  </action>
</event>
```


Hello precedente hello utilizzati script Transact-SQL seguente event_file hello tooread funzione di sistema:

* [sys.fn_xe_file_target_read_file (Transact-SQL)](http://msdn.microsoft.com/library/cc280743.aspx)

Una spiegazione delle opzioni avanzate per la visualizzazione di hello dei dati da eventi estesi è disponibile in:

* [Visualizzazione avanzata dei dati di destinazione da eventi estesi](http://msdn.microsoft.com/library/mt752502.aspx)


## <a name="converting-hello-code-sample-toorun-on-sql-server"></a>Conversione toorun di esempio di codice hello in SQL Server

Si supponga che si desiderava hello toorun precedente esempio di Transact-SQL in Microsoft SQL Server.

* Per semplicità, desiderata utilizzare replace toocompletely del contenitore di archiviazione di Azure hello con un semplice file, ad esempio **C:\myeventdata.xel**. file Hello verrebbero toohello unità disco rigido locale del computer hello che ospita SQL Server.
* Non è necessaria alcuna tipologia di istruzioni di Transact-SQL per **CREATE MASTER KEY** e **CREATE CREDENTIAL**.
* In hello **CREATE EVENT SESSION** istruzione, nel relativo **Aggiungi destinazione** clausola, sostituire il valore di Http hello assegnato apportate troppo**filename =** con una stringa di percorso completo come  **C:\MyFile.xel**.
  
  * Nessun account di Archiviazione di Azure deve essere coinvolto.

## <a name="more-information"></a>Altre informazioni

Per ulteriori informazioni sull'account e i contenitori di hello servizio di archiviazione di Azure, vedere:

* [Come toouse archiviazione Blob da .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [Denominazione e riferimento a contenitori, BLOB e metadati](http://msdn.microsoft.com/library/azure/dd135715.aspx)
* [Utilizzo di hello contenitore radice](http://msdn.microsoft.com/library/azure/ee395424.aspx)
* [Lezione 1: Creare criteri di accesso archiviati e la firma di accesso condiviso in un contenitore di Azure](http://msdn.microsoft.com/library/dn466430.aspx)
  * [Lezione 2: Creare una credenziale di SQL Server usando una firma di accesso condiviso](http://msdn.microsoft.com/library/dn466435.aspx)

<!--
Image references.
-->

[30_powershell_ise]: ./media/sql-database-xevent-code-event-file/event-file-powershell-ise-b30.png

