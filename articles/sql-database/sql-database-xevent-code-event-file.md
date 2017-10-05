---
title: Codice del file evento XEvent per il database SQL | Documentazione Microsoft
description: "Fornisce PowerShell e Transact-SQL per un esempio di codice in due fasi che illustra la destinazione del file evento in un evento esteso in Azure SQL Database. Archiviazione di Azure è una parte necessaria di questo scenario."
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
ms.openlocfilehash: e8c7a9af11ac4c22be00426337ab7c8b8ff0860f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="event-file-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="038e6-104">Codice di destinazione del file evento per eventi estesi nel database SQL</span><span class="sxs-lookup"><span data-stu-id="038e6-104">Event File target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="038e6-105">Si desidera un esempio di codice completo per un modo affidabile per acquisire e segnalare informazioni per un evento esteso.</span><span class="sxs-lookup"><span data-stu-id="038e6-105">You want a complete code sample for a robust way to capture and report information for an extended event.</span></span>

<span data-ttu-id="038e6-106">In Microsoft SQL Server la [destinazione del file evento](http://msdn.microsoft.com/library/ff878115.aspx) viene utilizzata per archiviare l'output di eventi in un file di disco rigido locale.</span><span class="sxs-lookup"><span data-stu-id="038e6-106">In Microsoft SQL Server, the [Event File target](http://msdn.microsoft.com/library/ff878115.aspx) is used to store event outputs into a local hard drive file.</span></span> <span data-ttu-id="038e6-107">Tuttavia, tali file non sono disponibili per il Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="038e6-107">But such files are not available to Azure SQL Database.</span></span> <span data-ttu-id="038e6-108">Invece, utilizziamo il servizio Archiviazione di Azure per supportare la destinazione del file evento.</span><span class="sxs-lookup"><span data-stu-id="038e6-108">Instead we use the Azure Storage service to support the Event File target.</span></span>

<span data-ttu-id="038e6-109">Questo argomento presenta un esempio di codice in due fasi:</span><span class="sxs-lookup"><span data-stu-id="038e6-109">This topic presents a two-phase code sample:</span></span>

* <span data-ttu-id="038e6-110">PowerShell, per creare un contenitore di Archiviazione di Azure nel cloud.</span><span class="sxs-lookup"><span data-stu-id="038e6-110">PowerShell, to create an Azure Storage container in the cloud.</span></span>
* <span data-ttu-id="038e6-111">Transact-SQL:</span><span class="sxs-lookup"><span data-stu-id="038e6-111">Transact-SQL:</span></span>
  
  * <span data-ttu-id="038e6-112">per assegnare il contenitore di Archiviazione di Azure a una destinazione del file evento.</span><span class="sxs-lookup"><span data-stu-id="038e6-112">To assign the Azure Storage container to an Event File target.</span></span>
  * <span data-ttu-id="038e6-113">Per creare e avviare la sessione dell'evento e così via.</span><span class="sxs-lookup"><span data-stu-id="038e6-113">To create and start the event session, and so on.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="038e6-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="038e6-114">Prerequisites</span></span>

* <span data-ttu-id="038e6-115">Un account e una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="038e6-115">An Azure account and subscription.</span></span> <span data-ttu-id="038e6-116">È possibile iscriversi per una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="038e6-116">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="038e6-117">Qualsiasi database in cui è possibile creare una tabella.</span><span class="sxs-lookup"><span data-stu-id="038e6-117">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="038e6-118">Facoltativamente, è possibile [creare un database dimostrativo **AdventureWorksLT**](sql-database-get-started.md) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="038e6-118">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="038e6-119">SQL Server Management Studio (ssms.exe), idealmente l'ultima versione di aggiornamento mensile.</span><span class="sxs-lookup"><span data-stu-id="038e6-119">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="038e6-120">È possibile scaricare la versione più recente di ssms.exe da:</span><span class="sxs-lookup"><span data-stu-id="038e6-120">You can download the latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="038e6-121">Argomento intitolato [SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="038e6-121">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="038e6-122">Un collegamento diretto al download.</span><span class="sxs-lookup"><span data-stu-id="038e6-122">A direct link to the download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)
* <span data-ttu-id="038e6-123">È necessario che i [moduli di Azure PowerShell](http://go.microsoft.com/?linkid=9811175) siano installati.</span><span class="sxs-lookup"><span data-stu-id="038e6-123">You must have the [Azure PowerShell modules](http://go.microsoft.com/?linkid=9811175) installed.</span></span>
  
  * <span data-ttu-id="038e6-124">I moduli forniscono comandi come **New-AzureStorageAccount**.</span><span class="sxs-lookup"><span data-stu-id="038e6-124">The modules provide commands such as - **New-AzureStorageAccount**.</span></span>

## <a name="phase-1-powershell-code-for-azure-storage-container"></a><span data-ttu-id="038e6-125">Fase 1: Codice di PowerShell per il contenitore di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="038e6-125">Phase 1: PowerShell code for Azure Storage container</span></span>

<span data-ttu-id="038e6-126">Questo PowerShell è la fase 1 dell'esempio di codice in due fasi.</span><span class="sxs-lookup"><span data-stu-id="038e6-126">This PowerShell is phase 1 of the two-phase code sample.</span></span>

<span data-ttu-id="038e6-127">Lo script inizia con comandi di pulitura dopo un'eventuale esecuzione precedente ed è eseguibile di nuovo.</span><span class="sxs-lookup"><span data-stu-id="038e6-127">The script starts with commands to clean up after a possible previous run, and is rerunnable.</span></span>

1. <span data-ttu-id="038e6-128">Incollare lo script di PowerShell in un editor di testo semplice, ad esempio Notepad.exe e salvare lo script come file con estensione **.ps1**.</span><span class="sxs-lookup"><span data-stu-id="038e6-128">Paste the PowerShell script into a simple text editor such as Notepad.exe, and save the script as a file with the extension **.ps1**.</span></span>
2. <span data-ttu-id="038e6-129">Avviare PowerShell ISE come amministratore.</span><span class="sxs-lookup"><span data-stu-id="038e6-129">Start PowerShell ISE as an Administrator.</span></span>
3. <span data-ttu-id="038e6-130">Al prompt dei comandi, digitare</span><span class="sxs-lookup"><span data-stu-id="038e6-130">At the prompt, type</span></span><br/>`Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`<br/><span data-ttu-id="038e6-131">e quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="038e6-131">and then press Enter.</span></span>
4. <span data-ttu-id="038e6-132">In PowerShell ISE, aprire il file **.ps1** .</span><span class="sxs-lookup"><span data-stu-id="038e6-132">In PowerShell ISE, open your **.ps1** file.</span></span> <span data-ttu-id="038e6-133">Eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="038e6-133">Run the script.</span></span>
5. <span data-ttu-id="038e6-134">Innanzitutto, lo script avvia una nuova finestra in cui si accede ad Azure.</span><span class="sxs-lookup"><span data-stu-id="038e6-134">The script first starts a new window in which you log in to Azure.</span></span>
   
   * <span data-ttu-id="038e6-135">Se si esegue nuovamente lo script senza interrompere la sessione, è possibile pratico decommentare il comando **Add-AzureAccount** .</span><span class="sxs-lookup"><span data-stu-id="038e6-135">If you rerun the script without disrupting your session, you have the convenient option of commenting out the **Add-AzureAccount** command.</span></span>

![PowerShell ISE, con il modulo Azure installato, pronto per l'esecuzione di script.][30_powershell_ise]


### <a name="powershell-code"></a><span data-ttu-id="038e6-137">Codice PowerShell</span><span class="sxs-lookup"><span data-stu-id="038e6-137">PowerShell code</span></span>

```powershell
## TODO: Before running, find all 'TODO' and make each edit!!

#--------------- 1 -----------------------


# You can comment out or skip this Add-AzureAccount
# command after the first run.
# Current PowerShell environment retains the successful outcome.

'Expect a pop-up window in which you log in to Azure.'


Add-AzureAccount

#-------------- 2 ------------------------


'
TODO: Edit the values assigned to these variables, especially the first few!
'

# Ensure the current date is between
# the Expiry and Start time values that you edit here.

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


# The ending display lists your Azure subscriptions.
# One should match the $subscriptionName value you assigned
#   earlier in this PowerShell script. 

'Choose an existing subscription for the current PowerShell environment.'


Select-AzureSubscription -SubscriptionName $subscriptionName


#-------------- 4 ------------------------


'
Clean up the old Azure Storage Account after any previous run, 
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
Get the primary access key for your storage account.
'


$primaryAccessKey_ForStorageAccount = `
    (Get-AzureStorageKey `
        -StorageAccountName $storageAccountName).Primary

"`$primaryAccessKey_ForStorageAccount = $primaryAccessKey_ForStorageAccount"

'Azure Storage Account cmdlet completed.
Remainder of PowerShell .ps1 script continues.
'

#--------------- 6 -----------------------


# The context will be needed to create a container within the storage account.

'Create a context object from the storage account and its primary access key.
'

$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey  $primaryAccessKey_ForStorageAccount


'Create a container within the storage account.
'


$containerObjectInStorageAccount = New-AzureStorageContainer `
    -Name    $containerName `
    -Context $context


'Create a security policy to be applied to the SAS token.
'

New-AzureStorageContainerStoredAccessPolicy `
    -Container  $containerName `
    -Context    $context `
    -Policy     $policySasToken `
    -Permission $policySasPermission `
    -ExpiryTime $policySasExpiryTime `
    -StartTime  $policySasStartTime 

'
Generate a SAS token for the container.
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


'Display the values that YOU must edit into the Transact-SQL script next!:
'

"storageAccountName: $storageAccountName"
"containerName:      $containerName"
"sasTokenWithPolicy: $sasTokenWithPolicy"

'
REMINDER: sasTokenWithPolicy here might start with "?" character, which you must exclude from Transact-SQL.
'

'
(Later, return here to delete your Azure Storage account. See the preceding - Remove-AzureStorageAccount -StorageAccountName $storageAccountName)'

'
Now shift to the Transact-SQL portion of the two-part code sample!'

# EOFile
```


<span data-ttu-id="038e6-138">Prendere nota dei valori nominati che lo script di PowerShell stampa alla fine.</span><span class="sxs-lookup"><span data-stu-id="038e6-138">Take note of the few named values that the PowerShell script prints when it ends.</span></span> <span data-ttu-id="038e6-139">È necessario modificare tali valori nello script Transact-SQL che segue come fase 2.</span><span class="sxs-lookup"><span data-stu-id="038e6-139">You must edit those values into the Transact-SQL script that follows as phase 2.</span></span>

## <a name="phase-2-transact-sql-code-that-uses-azure-storage-container"></a><span data-ttu-id="038e6-140">Fase 2: Codice Transact-SQL che utilizza il contenitore di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="038e6-140">Phase 2: Transact-SQL code that uses Azure Storage container</span></span>

* <span data-ttu-id="038e6-141">Nella fase 1 di questo esempio di codice è stato eseguito uno script di PowerShell per creare un contenitore di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="038e6-141">In phase 1 of this code sample, you ran a PowerShell script to create an Azure Storage container.</span></span>
* <span data-ttu-id="038e6-142">Successivamente nella fase 2, lo script Transact-SQL deve utilizzare il contenitore.</span><span class="sxs-lookup"><span data-stu-id="038e6-142">Next in phase 2, the following Transact-SQL script must use the container.</span></span>

<span data-ttu-id="038e6-143">Lo script inizia con comandi di pulitura dopo un'eventuale esecuzione precedente ed è eseguibile di nuovo.</span><span class="sxs-lookup"><span data-stu-id="038e6-143">The script starts with commands to clean up after a possible previous run, and is rerunnable.</span></span>

<span data-ttu-id="038e6-144">Lo script di PowerShell stampa alcuni valori denominati quando è terminato.</span><span class="sxs-lookup"><span data-stu-id="038e6-144">The PowerShell script printed a few named values when it ended.</span></span> <span data-ttu-id="038e6-145">È necessario modificare lo script di Transact-SQL per utilizzare tali valori.</span><span class="sxs-lookup"><span data-stu-id="038e6-145">You must edit the Transact-SQL script to use those values.</span></span> <span data-ttu-id="038e6-146">Trovare **TODO** nello script di Transact-SQL per individuare i punti di modifica.</span><span class="sxs-lookup"><span data-stu-id="038e6-146">Find **TODO** in the Transact-SQL script to locate the edit points.</span></span>

1. <span data-ttu-id="038e6-147">Aprire SQL Server Management Studio (ssms.exe).</span><span class="sxs-lookup"><span data-stu-id="038e6-147">Open SQL Server Management Studio (ssms.exe).</span></span>
2. <span data-ttu-id="038e6-148">Connettersi al database di Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="038e6-148">Connect to your Azure SQL Database database.</span></span>
3. <span data-ttu-id="038e6-149">Fare clic per aprire un nuovo riquadro di query.</span><span class="sxs-lookup"><span data-stu-id="038e6-149">Click to open a new query pane.</span></span>
4. <span data-ttu-id="038e6-150">Incollare il seguente script di Transact-SQL nel riquadro della query.</span><span class="sxs-lookup"><span data-stu-id="038e6-150">Paste the following Transact-SQL script into the query pane.</span></span>
5. <span data-ttu-id="038e6-151">Trovare ogni **TODO** nello script e apportare le modifiche appropriate.</span><span class="sxs-lookup"><span data-stu-id="038e6-151">Find every **TODO** in the script and make the appropriate edits.</span></span>
6. <span data-ttu-id="038e6-152">Salvare e quindi eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="038e6-152">Save, and then run the script.</span></span>


> [!WARNING]
> <span data-ttu-id="038e6-153">Il valore della chiave di firma di accesso condiviso generata dallo script di PowerShell precedente potrebbe iniziare con un "?" (punto interrogativo).</span><span class="sxs-lookup"><span data-stu-id="038e6-153">The SAS key value generated by the preceding PowerShell script might begin with a '?' (question mark).</span></span> <span data-ttu-id="038e6-154">Quando si usa la chiave di firma di accesso condiviso nello script T-SQL seguente, è necessario *rimuovere il prefisso "?"*.</span><span class="sxs-lookup"><span data-stu-id="038e6-154">When you use the SAS key in the following T-SQL script, you must *remove the leading '?'*.</span></span> <span data-ttu-id="038e6-155">Le attività in caso contrario potrebbero essere bloccate dalla protezione.</span><span class="sxs-lookup"><span data-stu-id="038e6-155">Otherwise your efforts might be blocked by security.</span></span>


### <a name="transact-sql-code"></a><span data-ttu-id="038e6-156">Codice Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="038e6-156">Transact-SQL code</span></span>

```sql
---- TODO: First, run the PowerShell portion of this two-part code sample.
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
        -- TODO: Assign AzureStorageAccount name, and the associated Container name.
        WHERE name = 'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent')
BEGIN
    DROP DATABASE SCOPED CREDENTIAL
        -- TODO: Assign AzureStorageAccount name, and the associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent] ;
END
GO


CREATE
    DATABASE SCOPED
    CREDENTIAL
        -- use '.blob.',   and not '.queue.' or '.table.' etc.
        -- TODO: Assign AzureStorageAccount name, and the associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    WITH
        IDENTITY = 'SHARED ACCESS SIGNATURE',  -- "SAS" token.
        -- TODO: Paste in the long SasToken string here for Secret, but exclude any leading '?'.
        SECRET = 'sv=2014-02-14&sr=c&si=gmpolicysastoken&sig=EjAqjo6Nu5xMLEZEkMkLbeF7TD9v1J8DNB2t8gOKTts%3D'
    ;
GO


------  Step 3.  Create (define) an event session.  --------
------  The event session has an event with an action,
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
            -- TODO: Assign AzureStorageAccount name, and the associated Container name.
            -- Also, tweak the .xel file name at end, if you like.
            SET filename =
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b.xel'
            )
    WITH
        (MAX_MEMORY = 10 MB,
        MAX_DISPATCH_LATENCY = 3 SECONDS)
    ;
GO


------  Step 4.  Start the event session.  ----------------
------  Issue the SQL Update statements that will be traced.
------  Then stop the session.

------  Note: If the target fails to attach,
------  the session must be stopped and restarted.

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


-------------- Step 5.  Select the results. ----------

SELECT
        *, 'CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS!' as [CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS],
        CAST(event_data AS XML) AS [event_data_XML]  -- TODO: In ssms.exe results grid, double-click this cell!
    FROM
        sys.fn_xe_file_target_read_file
            (
                -- TODO: Fill in Storage Account name, and the associated Container name.
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
    -- TODO: Assign AzureStorageAccount name, and the associated Container name.
    [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    ;
GO

DROP TABLE gmTabEmployee;
GO

PRINT 'Use PowerShell Remove-AzureStorageAccount to delete your Azure Storage account!';
GO
```


<span data-ttu-id="038e6-157">Se la destinazione non può essere collegata durante l’esecuzione, è necessario arrestare e riavviare la sessione dell'evento:</span><span class="sxs-lookup"><span data-stu-id="038e6-157">If the target fails to attach when you run, you must stop and restart the event session:</span></span>

```sql
ALTER EVENT SESSION ... STATE = STOP;
GO
ALTER EVENT SESSION ... STATE = START;
GO
```


## <a name="output"></a><span data-ttu-id="038e6-158">Output</span><span class="sxs-lookup"><span data-stu-id="038e6-158">Output</span></span>

<span data-ttu-id="038e6-159">Al termine dell'esecuzione dello script Transact-SQL, fare clic su una cella sotto l'intestazione della colonna **event_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="038e6-159">When the Transact-SQL script completes, click a cell under the **event_data_XML** column header.</span></span> <span data-ttu-id="038e6-160">Viene visualizzato un elemento **<event>** che mostra un'istruzione UPDATE.</span><span class="sxs-lookup"><span data-stu-id="038e6-160">One **<event>** element is displayed which shows one UPDATE statement.</span></span>

<span data-ttu-id="038e6-161">Di seguito è riportato un elemento **<event>** generato durante il test:</span><span class="sxs-lookup"><span data-stu-id="038e6-161">Here is one **<event>** element that was generated during testing:</span></span>


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


<span data-ttu-id="038e6-162">Lo script Transact-SQL precedente ha usato la funzione di sistema seguente per leggere l'event_file:</span><span class="sxs-lookup"><span data-stu-id="038e6-162">The preceding Transact-SQL script used the following system function to read the event_file:</span></span>

* [<span data-ttu-id="038e6-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="038e6-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/cc280743.aspx)

<span data-ttu-id="038e6-164">Le opzioni avanzate per la visualizzazione di dati da eventi estesi sono illustrate all'indirizzo:</span><span class="sxs-lookup"><span data-stu-id="038e6-164">An explanation of advanced options for the viewing of data from extended events is available at:</span></span>

* [<span data-ttu-id="038e6-165">Visualizzazione avanzata dei dati di destinazione da eventi estesi</span><span class="sxs-lookup"><span data-stu-id="038e6-165">Advanced Viewing of Target Data from Extended Events</span></span>](http://msdn.microsoft.com/library/mt752502.aspx)


## <a name="converting-the-code-sample-to-run-on-sql-server"></a><span data-ttu-id="038e6-166">Conversione dell’esempio di codice da eseguire in SQL Server</span><span class="sxs-lookup"><span data-stu-id="038e6-166">Converting the code sample to run on SQL Server</span></span>

<span data-ttu-id="038e6-167">Si supponga di voler eseguire l'esempio di Transact-SQL precedente in Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="038e6-167">Suppose you wanted to run the preceding Transact-SQL sample on Microsoft SQL Server.</span></span>

* <span data-ttu-id="038e6-168">Per semplicità, si desidera sostituire completamente l'uso del contenitore di Archiviazione di Azure con un semplice file, come **C:\myeventdata.xel**.</span><span class="sxs-lookup"><span data-stu-id="038e6-168">For simplicity, you would want to completely replace use of the Azure Storage container with a simple file such as **C:\myeventdata.xel**.</span></span> <span data-ttu-id="038e6-169">Il file verrebbe scritto sul disco rigido locale del computer che ospita SQL Server.</span><span class="sxs-lookup"><span data-stu-id="038e6-169">The file would be written to the local hard drive of the computer that hosts SQL Server.</span></span>
* <span data-ttu-id="038e6-170">Non è necessaria alcuna tipologia di istruzioni di Transact-SQL per **CREATE MASTER KEY** e **CREATE CREDENTIAL**.</span><span class="sxs-lookup"><span data-stu-id="038e6-170">You would not need any kind of Transact-SQL statements for **CREATE MASTER KEY** and **CREATE CREDENTIAL**.</span></span>
* <span data-ttu-id="038e6-171">Nell'istruzione **CREATE EVENT SESSION**, nella relativa clausola **ADD TARGET**, sostituire il valore di Http assegnato a **filename =** con una stringa di percorso completo **C:\myfile.xel**.</span><span class="sxs-lookup"><span data-stu-id="038e6-171">In the **CREATE EVENT SESSION** statement, in its **ADD TARGET** clause, you would replace the Http value assigned made to **filename=** with a full path string like **C:\myfile.xel**.</span></span>
  
  * <span data-ttu-id="038e6-172">Nessun account di Archiviazione di Azure deve essere coinvolto.</span><span class="sxs-lookup"><span data-stu-id="038e6-172">No Azure Storage account need be involved.</span></span>

## <a name="more-information"></a><span data-ttu-id="038e6-173">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="038e6-173">More information</span></span>

<span data-ttu-id="038e6-174">Per ulteriori informazioni sugli account e i contenitori nel servizio Archiviazione di Azure, vedere:</span><span class="sxs-lookup"><span data-stu-id="038e6-174">For more info about accounts and containers in the Azure Storage service, see:</span></span>

* [<span data-ttu-id="038e6-175">Come usare l'archiviazione BLOB da .NET</span><span class="sxs-lookup"><span data-stu-id="038e6-175">How to use Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="038e6-176">Denominazione e riferimento a contenitori, BLOB e metadati</span><span class="sxs-lookup"><span data-stu-id="038e6-176">Naming and Referencing Containers, Blobs, and Metadata</span></span>](http://msdn.microsoft.com/library/azure/dd135715.aspx)
* [<span data-ttu-id="038e6-177">Lavorare con il contenitore radice</span><span class="sxs-lookup"><span data-stu-id="038e6-177">Working with the Root Container</span></span>](http://msdn.microsoft.com/library/azure/ee395424.aspx)
* [<span data-ttu-id="038e6-178">Lezione 1: Creare criteri di accesso archiviati e la firma di accesso condiviso in un contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="038e6-178">Lesson 1: Create a stored access policy and a shared access signature on an Azure container</span></span>](http://msdn.microsoft.com/library/dn466430.aspx)
  * [<span data-ttu-id="038e6-179">Lezione 2: Creare una credenziale di SQL Server usando una firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="038e6-179">Lesson 2: Create a SQL Server credential using a shared access signature</span></span>](http://msdn.microsoft.com/library/dn466435.aspx)

<!--
Image references.
-->

[30_powershell_ise]: ./media/sql-database-xevent-code-event-file/event-file-powershell-ise-b30.png

