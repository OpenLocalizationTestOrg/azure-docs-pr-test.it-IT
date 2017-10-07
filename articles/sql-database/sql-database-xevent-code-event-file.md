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
# <a name="event-file-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="35311-104">Codice di destinazione del file evento per eventi estesi nel database SQL</span><span class="sxs-lookup"><span data-stu-id="35311-104">Event File target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="35311-105">Si desidera un esempio di codice completo per una modo efficiente toocapture e segnalare le informazioni per un evento esteso.</span><span class="sxs-lookup"><span data-stu-id="35311-105">You want a complete code sample for a robust way toocapture and report information for an extended event.</span></span>

<span data-ttu-id="35311-106">In Microsoft SQL Server, hello [destinazione File evento](http://msdn.microsoft.com/library/ff878115.aspx) è output evento toostore utilizzati in un file di disco rigido locale.</span><span class="sxs-lookup"><span data-stu-id="35311-106">In Microsoft SQL Server, hello [Event File target](http://msdn.microsoft.com/library/ff878115.aspx) is used toostore event outputs into a local hard drive file.</span></span> <span data-ttu-id="35311-107">Tuttavia, tali file non sono disponibili tooAzure Database SQL.</span><span class="sxs-lookup"><span data-stu-id="35311-107">But such files are not available tooAzure SQL Database.</span></span> <span data-ttu-id="35311-108">Invece utilizziamo destinazione di archiviazione di Azure servizio toosupport hello evento File hello.</span><span class="sxs-lookup"><span data-stu-id="35311-108">Instead we use hello Azure Storage service toosupport hello Event File target.</span></span>

<span data-ttu-id="35311-109">Questo argomento presenta un esempio di codice in due fasi:</span><span class="sxs-lookup"><span data-stu-id="35311-109">This topic presents a two-phase code sample:</span></span>

* <span data-ttu-id="35311-110">PowerShell toocreate un contenitore di archiviazione di Azure nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="35311-110">PowerShell, toocreate an Azure Storage container in hello cloud.</span></span>
* <span data-ttu-id="35311-111">Transact-SQL:</span><span class="sxs-lookup"><span data-stu-id="35311-111">Transact-SQL:</span></span>
  
  * <span data-ttu-id="35311-112">tooassign hello Azure Storage contenitore tooan evento destinazione File.</span><span class="sxs-lookup"><span data-stu-id="35311-112">tooassign hello Azure Storage container tooan Event File target.</span></span>
  * <span data-ttu-id="35311-113">avvio e toocreate hello event session e così via.</span><span class="sxs-lookup"><span data-stu-id="35311-113">toocreate and start hello event session, and so on.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35311-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="35311-114">Prerequisites</span></span>

* <span data-ttu-id="35311-115">Un account e una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="35311-115">An Azure account and subscription.</span></span> <span data-ttu-id="35311-116">È possibile iscriversi per una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="35311-116">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="35311-117">Qualsiasi database in cui è possibile creare una tabella.</span><span class="sxs-lookup"><span data-stu-id="35311-117">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="35311-118">Facoltativamente, è possibile [creare un database dimostrativo **AdventureWorksLT**](sql-database-get-started.md) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="35311-118">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="35311-119">SQL Server Management Studio (ssms.exe), idealmente l'ultima versione di aggiornamento mensile.</span><span class="sxs-lookup"><span data-stu-id="35311-119">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="35311-120">È possibile scaricare hello ssms.exe più recenti da:</span><span class="sxs-lookup"><span data-stu-id="35311-120">You can download hello latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="35311-121">Argomento intitolato [SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="35311-121">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="35311-122">Download di toohello un collegamento diretto.</span><span class="sxs-lookup"><span data-stu-id="35311-122">A direct link toohello download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)
* <span data-ttu-id="35311-123">È necessario disporre di hello [moduli di Azure PowerShell](http://go.microsoft.com/?linkid=9811175) installato.</span><span class="sxs-lookup"><span data-stu-id="35311-123">You must have hello [Azure PowerShell modules](http://go.microsoft.com/?linkid=9811175) installed.</span></span>
  
  * <span data-ttu-id="35311-124">i moduli di Hello forniscono i comandi, ad esempio - **New AzureStorageAccount**.</span><span class="sxs-lookup"><span data-stu-id="35311-124">hello modules provide commands such as - **New-AzureStorageAccount**.</span></span>

## <a name="phase-1-powershell-code-for-azure-storage-container"></a><span data-ttu-id="35311-125">Fase 1: Codice di PowerShell per il contenitore di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="35311-125">Phase 1: PowerShell code for Azure Storage container</span></span>

<span data-ttu-id="35311-126">Questo PowerShell è la fase 1 dell'esempio di codice in due fasi hello.</span><span class="sxs-lookup"><span data-stu-id="35311-126">This PowerShell is phase 1 of hello two-phase code sample.</span></span>

<span data-ttu-id="35311-127">script Hello viene avviato con i comandi tooclean dopo un precedente possibile eseguire e rerunnable.</span><span class="sxs-lookup"><span data-stu-id="35311-127">hello script starts with commands tooclean up after a possible previous run, and is rerunnable.</span></span>

1. <span data-ttu-id="35311-128">Incollare uno script di PowerShell hello in un semplice editor di testo, ad esempio Notepad.exe e salvare script hello come un file con estensione hello **ps1**.</span><span class="sxs-lookup"><span data-stu-id="35311-128">Paste hello PowerShell script into a simple text editor such as Notepad.exe, and save hello script as a file with hello extension **.ps1**.</span></span>
2. <span data-ttu-id="35311-129">Avviare PowerShell ISE come amministratore.</span><span class="sxs-lookup"><span data-stu-id="35311-129">Start PowerShell ISE as an Administrator.</span></span>
3. <span data-ttu-id="35311-130">Al prompt dei comandi hello, digitare</span><span class="sxs-lookup"><span data-stu-id="35311-130">At hello prompt, type</span></span><br/>`Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`<br/><span data-ttu-id="35311-131">e quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="35311-131">and then press Enter.</span></span>
4. <span data-ttu-id="35311-132">In PowerShell ISE, aprire il file **.ps1** .</span><span class="sxs-lookup"><span data-stu-id="35311-132">In PowerShell ISE, open your **.ps1** file.</span></span> <span data-ttu-id="35311-133">Eseguire script hello.</span><span class="sxs-lookup"><span data-stu-id="35311-133">Run hello script.</span></span>
5. <span data-ttu-id="35311-134">script Hello primo avvio di una nuova finestra in cui si accede tooAzure.</span><span class="sxs-lookup"><span data-stu-id="35311-134">hello script first starts a new window in which you log in tooAzure.</span></span>
   
   * <span data-ttu-id="35311-135">Se si esegue nuovamente script hello senza interrompere la sessione, è possibile hello pratico commento hello **Add-AzureAccount** comando.</span><span class="sxs-lookup"><span data-stu-id="35311-135">If you rerun hello script without disrupting your session, you have hello convenient option of commenting out hello **Add-AzureAccount** command.</span></span>

![PowerShell ISE, con il modulo Azure installato, script toorun pronto.][30_powershell_ise]


### <a name="powershell-code"></a><span data-ttu-id="35311-137">Codice PowerShell</span><span class="sxs-lookup"><span data-stu-id="35311-137">PowerShell code</span></span>

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


<span data-ttu-id="35311-138">Prendere nota di hello alcuni valori denominati che uno script di PowerShell hello stampa la fine.</span><span class="sxs-lookup"><span data-stu-id="35311-138">Take note of hello few named values that hello PowerShell script prints when it ends.</span></span> <span data-ttu-id="35311-139">È necessario modificare tali valori in hello script Transact-SQL che segue come fase 2.</span><span class="sxs-lookup"><span data-stu-id="35311-139">You must edit those values into hello Transact-SQL script that follows as phase 2.</span></span>

## <a name="phase-2-transact-sql-code-that-uses-azure-storage-container"></a><span data-ttu-id="35311-140">Fase 2: Codice Transact-SQL che utilizza il contenitore di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="35311-140">Phase 2: Transact-SQL code that uses Azure Storage container</span></span>

* <span data-ttu-id="35311-141">Nella fase 1 di questo esempio di codice è stato eseguito un toocreate di script di PowerShell un contenitore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="35311-141">In phase 1 of this code sample, you ran a PowerShell script toocreate an Azure Storage container.</span></span>
* <span data-ttu-id="35311-142">Successivamente nella fase 2, hello script Transact-SQL seguente è necessario utilizzare hello contenitore.</span><span class="sxs-lookup"><span data-stu-id="35311-142">Next in phase 2, hello following Transact-SQL script must use hello container.</span></span>

<span data-ttu-id="35311-143">script Hello viene avviato con i comandi tooclean dopo un precedente possibile eseguire e rerunnable.</span><span class="sxs-lookup"><span data-stu-id="35311-143">hello script starts with commands tooclean up after a possible previous run, and is rerunnable.</span></span>

<span data-ttu-id="35311-144">script di PowerShell Hello stampati alcuni valori denominati quando è terminato.</span><span class="sxs-lookup"><span data-stu-id="35311-144">hello PowerShell script printed a few named values when it ended.</span></span> <span data-ttu-id="35311-145">È necessario modificare hello Transact-SQL script toouse tali valori.</span><span class="sxs-lookup"><span data-stu-id="35311-145">You must edit hello Transact-SQL script toouse those values.</span></span> <span data-ttu-id="35311-146">Trovare **TODO** in hello toolocate di script Transact-SQL hello punti di montaggio.</span><span class="sxs-lookup"><span data-stu-id="35311-146">Find **TODO** in hello Transact-SQL script toolocate hello edit points.</span></span>

1. <span data-ttu-id="35311-147">Aprire SQL Server Management Studio (ssms.exe).</span><span class="sxs-lookup"><span data-stu-id="35311-147">Open SQL Server Management Studio (ssms.exe).</span></span>
2. <span data-ttu-id="35311-148">La connessione a database di Database SQL di Azure tooyour.</span><span class="sxs-lookup"><span data-stu-id="35311-148">Connect tooyour Azure SQL Database database.</span></span>
3. <span data-ttu-id="35311-149">Fare clic su tooopen un nuovo riquadro query.</span><span class="sxs-lookup"><span data-stu-id="35311-149">Click tooopen a new query pane.</span></span>
4. <span data-ttu-id="35311-150">Incollare lo script di Transact-SQL seguente nel riquadro query hello hello.</span><span class="sxs-lookup"><span data-stu-id="35311-150">Paste hello following Transact-SQL script into hello query pane.</span></span>
5. <span data-ttu-id="35311-151">Trovare ogni **TODO** in hello script e apportare le modifiche appropriate hello.</span><span class="sxs-lookup"><span data-stu-id="35311-151">Find every **TODO** in hello script and make hello appropriate edits.</span></span>
6. <span data-ttu-id="35311-152">Salvare e quindi eseguire script hello.</span><span class="sxs-lookup"><span data-stu-id="35311-152">Save, and then run hello script.</span></span>


> [!WARNING]
> <span data-ttu-id="35311-153">valore di chiave di firma di accesso condiviso generato da hello precedente script di PowerShell Hello potrebbe iniziare con un '?' (punto interrogativo).</span><span class="sxs-lookup"><span data-stu-id="35311-153">hello SAS key value generated by hello preceding PowerShell script might begin with a '?' (question mark).</span></span> <span data-ttu-id="35311-154">Quando si utilizza una chiave SAS hello in hello lo script T-SQL seguente, è necessario *rimuovere iniziali hello '?'* .</span><span class="sxs-lookup"><span data-stu-id="35311-154">When you use hello SAS key in hello following T-SQL script, you must *remove hello leading '?'*.</span></span> <span data-ttu-id="35311-155">Le attività in caso contrario potrebbero essere bloccate dalla protezione.</span><span class="sxs-lookup"><span data-stu-id="35311-155">Otherwise your efforts might be blocked by security.</span></span>


### <a name="transact-sql-code"></a><span data-ttu-id="35311-156">Codice Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="35311-156">Transact-SQL code</span></span>

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


<span data-ttu-id="35311-157">Se la destinazione hello non riesce tooattach quando si esegue, è necessario arrestare e riavviare la sessione di eventi hello:</span><span class="sxs-lookup"><span data-stu-id="35311-157">If hello target fails tooattach when you run, you must stop and restart hello event session:</span></span>

```sql
ALTER EVENT SESSION ... STATE = STOP;
GO
ALTER EVENT SESSION ... STATE = START;
GO
```


## <a name="output"></a><span data-ttu-id="35311-158">Output</span><span class="sxs-lookup"><span data-stu-id="35311-158">Output</span></span>

<span data-ttu-id="35311-159">Al termine dell'esecuzione hello script Transact-SQL, fare clic su una cella in hello **event_data_XML** intestazione di colonna.</span><span class="sxs-lookup"><span data-stu-id="35311-159">When hello Transact-SQL script completes, click a cell under hello **event_data_XML** column header.</span></span> <span data-ttu-id="35311-160">Viene visualizzato un elemento **<event>** che mostra un'istruzione UPDATE.</span><span class="sxs-lookup"><span data-stu-id="35311-160">One **<event>** element is displayed which shows one UPDATE statement.</span></span>

<span data-ttu-id="35311-161">Di seguito è riportato un elemento **<event>** generato durante il test:</span><span class="sxs-lookup"><span data-stu-id="35311-161">Here is one **<event>** element that was generated during testing:</span></span>


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


<span data-ttu-id="35311-162">Hello precedente hello utilizzati script Transact-SQL seguente event_file hello tooread funzione di sistema:</span><span class="sxs-lookup"><span data-stu-id="35311-162">hello preceding Transact-SQL script used hello following system function tooread hello event_file:</span></span>

* [<span data-ttu-id="35311-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="35311-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/cc280743.aspx)

<span data-ttu-id="35311-164">Una spiegazione delle opzioni avanzate per la visualizzazione di hello dei dati da eventi estesi è disponibile in:</span><span class="sxs-lookup"><span data-stu-id="35311-164">An explanation of advanced options for hello viewing of data from extended events is available at:</span></span>

* [<span data-ttu-id="35311-165">Visualizzazione avanzata dei dati di destinazione da eventi estesi</span><span class="sxs-lookup"><span data-stu-id="35311-165">Advanced Viewing of Target Data from Extended Events</span></span>](http://msdn.microsoft.com/library/mt752502.aspx)


## <a name="converting-hello-code-sample-toorun-on-sql-server"></a><span data-ttu-id="35311-166">Conversione toorun di esempio di codice hello in SQL Server</span><span class="sxs-lookup"><span data-stu-id="35311-166">Converting hello code sample toorun on SQL Server</span></span>

<span data-ttu-id="35311-167">Si supponga che si desiderava hello toorun precedente esempio di Transact-SQL in Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="35311-167">Suppose you wanted toorun hello preceding Transact-SQL sample on Microsoft SQL Server.</span></span>

* <span data-ttu-id="35311-168">Per semplicità, desiderata utilizzare replace toocompletely del contenitore di archiviazione di Azure hello con un semplice file, ad esempio **C:\myeventdata.xel**.</span><span class="sxs-lookup"><span data-stu-id="35311-168">For simplicity, you would want toocompletely replace use of hello Azure Storage container with a simple file such as **C:\myeventdata.xel**.</span></span> <span data-ttu-id="35311-169">file Hello verrebbero toohello unità disco rigido locale del computer hello che ospita SQL Server.</span><span class="sxs-lookup"><span data-stu-id="35311-169">hello file would be written toohello local hard drive of hello computer that hosts SQL Server.</span></span>
* <span data-ttu-id="35311-170">Non è necessaria alcuna tipologia di istruzioni di Transact-SQL per **CREATE MASTER KEY** e **CREATE CREDENTIAL**.</span><span class="sxs-lookup"><span data-stu-id="35311-170">You would not need any kind of Transact-SQL statements for **CREATE MASTER KEY** and **CREATE CREDENTIAL**.</span></span>
* <span data-ttu-id="35311-171">In hello **CREATE EVENT SESSION** istruzione, nel relativo **Aggiungi destinazione** clausola, sostituire il valore di Http hello assegnato apportate troppo**filename =** con una stringa di percorso completo come  **C:\MyFile.xel**.</span><span class="sxs-lookup"><span data-stu-id="35311-171">In hello **CREATE EVENT SESSION** statement, in its **ADD TARGET** clause, you would replace hello Http value assigned made too**filename=** with a full path string like **C:\myfile.xel**.</span></span>
  
  * <span data-ttu-id="35311-172">Nessun account di Archiviazione di Azure deve essere coinvolto.</span><span class="sxs-lookup"><span data-stu-id="35311-172">No Azure Storage account need be involved.</span></span>

## <a name="more-information"></a><span data-ttu-id="35311-173">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="35311-173">More information</span></span>

<span data-ttu-id="35311-174">Per ulteriori informazioni sull'account e i contenitori di hello servizio di archiviazione di Azure, vedere:</span><span class="sxs-lookup"><span data-stu-id="35311-174">For more info about accounts and containers in hello Azure Storage service, see:</span></span>

* [<span data-ttu-id="35311-175">Come toouse archiviazione Blob da .NET</span><span class="sxs-lookup"><span data-stu-id="35311-175">How toouse Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="35311-176">Denominazione e riferimento a contenitori, BLOB e metadati</span><span class="sxs-lookup"><span data-stu-id="35311-176">Naming and Referencing Containers, Blobs, and Metadata</span></span>](http://msdn.microsoft.com/library/azure/dd135715.aspx)
* [<span data-ttu-id="35311-177">Utilizzo di hello contenitore radice</span><span class="sxs-lookup"><span data-stu-id="35311-177">Working with hello Root Container</span></span>](http://msdn.microsoft.com/library/azure/ee395424.aspx)
* [<span data-ttu-id="35311-178">Lezione 1: Creare criteri di accesso archiviati e la firma di accesso condiviso in un contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="35311-178">Lesson 1: Create a stored access policy and a shared access signature on an Azure container</span></span>](http://msdn.microsoft.com/library/dn466430.aspx)
  * [<span data-ttu-id="35311-179">Lezione 2: Creare una credenziale di SQL Server usando una firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="35311-179">Lesson 2: Create a SQL Server credential using a shared access signature</span></span>](http://msdn.microsoft.com/library/dn466435.aspx)

<!--
Image references.
-->

[30_powershell_ise]: ./media/sql-database-xevent-code-event-file/event-file-powershell-ise-b30.png

