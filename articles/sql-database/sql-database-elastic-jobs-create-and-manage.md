---
title: Gestire gruppi di database SQL di Azure | Documentazione Microsoft
description: Informazioni sulla creazione e la gestione di un processo elastico.
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: f858344d-085b-4022-935e-1b5fa20adbac
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: d30cc74778e0b36dd632c2f040ce80d1ca8af5a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a><span data-ttu-id="6363a-103">Creare e gestire database SQL di Azure con scalabilità orizzontale tramite processi elastici (anteprima)</span><span class="sxs-lookup"><span data-stu-id="6363a-103">Create and manage scaled out Azure SQL Databases using elastic jobs (preview)</span></span>


<span data-ttu-id="6363a-104">**processi di database elastico** semplificano la gestione dei gruppi di database con l'esecuzione di operazioni amministrative, come le modifiche dello schema, la gestione delle credenziali, gli aggiornamenti dei dati di riferimento, la raccolta dei dati sulle prestazioni o la raccolta dei dati di telemetria dei tenant (clienti).</span><span class="sxs-lookup"><span data-stu-id="6363a-104">**Elastic Database jobs** simplify management of groups of databases by executing administrative operations such as schema changes, credentials management, reference data updates, performance data collection or tenant (customer) telemetry collection.</span></span> <span data-ttu-id="6363a-105">L'opzione relativa ai processi di database elastici è attualmente disponibile tramite il portale di Azure e i cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6363a-105">Elastic Database jobs is currently available through the Azure portal and PowerShell cmdlets.</span></span> <span data-ttu-id="6363a-106">Il portale di Azure presenta tuttavia funzionalità ridotte, limitate all'esecuzione in tutti i database di un [pool elastico (anteprima)](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="6363a-106">However, the Azure portal surfaces reduced functionality limited to execution across all databases in an [elastic pool (preview)](sql-database-elastic-pool.md).</span></span> <span data-ttu-id="6363a-107">Per accedere a funzionalità aggiuntive e all'esecuzione di script in un gruppo di database, compreso un insieme personalizzato o un insieme di partizioni (creato usando la [libreria client dei database elastici](sql-database-elastic-scale-introduction.md)), vedere [Creare e gestire processi di database elastici del database SQL tramite PowerShell](sql-database-elastic-jobs-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6363a-107">To access additional features and execution of scripts across a group of databases including a custom-defined collection or a shard set (created using [Elastic Database client library](sql-database-elastic-scale-introduction.md)), see [Creating and managing jobs using PowerShell](sql-database-elastic-jobs-powershell.md).</span></span> <span data-ttu-id="6363a-108">Per ulteriori informazioni sui processi, vedere [Panoramica dei processi di database elastici](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6363a-108">For more information about jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6363a-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6363a-109">Prerequisites</span></span>
* <span data-ttu-id="6363a-110">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6363a-110">An Azure subscription.</span></span> <span data-ttu-id="6363a-111">Per una versione di valutazione gratuita, vedere [Versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6363a-111">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6363a-112">Un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="6363a-112">An elastic pool.</span></span> <span data-ttu-id="6363a-113">Vedere l'articolo sui [pool elastici](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="6363a-113">See [About elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="6363a-114">Installazione dei componenti del servizio relativo ai processi elastici di database.</span><span class="sxs-lookup"><span data-stu-id="6363a-114">Installation of elastic database job service components.</span></span> <span data-ttu-id="6363a-115">Vedere l'articolo sull' [installazione del servizio relativo ai processi elastici di database](sql-database-elastic-jobs-service-installation.md).</span><span class="sxs-lookup"><span data-stu-id="6363a-115">See [Installing the elastic database job service](sql-database-elastic-jobs-service-installation.md).</span></span>

## <a name="creating-jobs"></a><span data-ttu-id="6363a-116">Creazione di processi</span><span class="sxs-lookup"><span data-stu-id="6363a-116">Creating jobs</span></span>
1. <span data-ttu-id="6363a-117">Mediante il [portale di Azure](https://portal.azure.com), da un pool di processi di database elastici esistente, fare clic su **Crea processo**.</span><span class="sxs-lookup"><span data-stu-id="6363a-117">Using the [Azure portal](https://portal.azure.com), from an existing elastic database job pool, click **Create job**.</span></span>
2. <span data-ttu-id="6363a-118">Digitare il nome utente e la password dell'amministratore del database (creati in fase di installazione) per il database di controllo dei processi (archivio dei metadati relativi ai processi).</span><span class="sxs-lookup"><span data-stu-id="6363a-118">Type in the username and password of the database administrator (created at installation of Jobs) for the jobs control database (metadata storage for jobs).</span></span>
   
    ![Denominare il processo, digitare o incollare il nome nel codice e fare clic su Esegui][1]
3. <span data-ttu-id="6363a-120">Nel pannello **Crea processo** digitare il nome del processo.</span><span class="sxs-lookup"><span data-stu-id="6363a-120">In the **Create Job** blade, type a name for the job.</span></span>
4. <span data-ttu-id="6363a-121">Digitare il nome utente e la password per connettersi ai database di destinazione con autorizzazioni sufficienti per l'esecuzione di script.</span><span class="sxs-lookup"><span data-stu-id="6363a-121">Type the user name and password to connect to the target databases with sufficient permissions for script execution to succeed.</span></span>
5. <span data-ttu-id="6363a-122">Incollare o digitare nello script T-SQL.</span><span class="sxs-lookup"><span data-stu-id="6363a-122">Paste or type in the T-SQL script.</span></span>
6. <span data-ttu-id="6363a-123">Fare clic su **Salva** e quindi su **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="6363a-123">Click **Save** and then click **Run**.</span></span>
   
    ![Creare processi ed eseguirli][5]

## <a name="run-idempotent-jobs"></a><span data-ttu-id="6363a-125">Eseguire processi idempotenti</span><span class="sxs-lookup"><span data-stu-id="6363a-125">Run idempotent jobs</span></span>
<span data-ttu-id="6363a-126">Quando si esegue uno script su un insieme di database, è necessario assicurarsi che tale script sia idempotente.</span><span class="sxs-lookup"><span data-stu-id="6363a-126">When you run a script against a set of databases, you must be sure that the script is idempotent.</span></span> <span data-ttu-id="6363a-127">In altri termini, è necessario che lo script possa essere eseguito più volte anche se in precedenza aveva avuto esito negativo e non era stato completato.</span><span class="sxs-lookup"><span data-stu-id="6363a-127">That is, the script must be able to run multiple times, even if it has failed before in an incomplete state.</span></span> <span data-ttu-id="6363a-128">Se ad esempio uno script non riesce, il processo verrà ripetuto automaticamente fino a quando non avrà esito positivo (all'interno di limiti stabiliti, poiché la logica di ripetizione potrà eventualmente interrompere l'esecuzione di nuovi tentativi).</span><span class="sxs-lookup"><span data-stu-id="6363a-128">For example, when a script fails, the job will be automatically retried until it succeeds (within limits, as the retry logic will eventually cease the retrying).</span></span> <span data-ttu-id="6363a-129">Il metodo per eseguire questa operazione consiste nell'uso della clausola "IF EXISTS" e nell'eliminazione di qualsiasi istanza trovata prima della creazione di un nuovo oggetto.</span><span class="sxs-lookup"><span data-stu-id="6363a-129">The way to do this is to use the an "IF EXISTS" clause and delete any found instance before creating a new object.</span></span> <span data-ttu-id="6363a-130">Di seguito è riportato un esempio:</span><span class="sxs-lookup"><span data-stu-id="6363a-130">An example is shown here:</span></span>

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

<span data-ttu-id="6363a-131">In alternativa, usare una clausola "IF NOT EXISTS" prima di creare una nuova istanza:</span><span class="sxs-lookup"><span data-stu-id="6363a-131">Alternatively, use an "IF NOT EXISTS" clause before creating a new instance:</span></span>

    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
     CREATE TABLE TestTable(
      TestTableId INT PRIMARY KEY IDENTITY,
      InsertionTime DATETIME2
     );
    END
    GO

    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO

<span data-ttu-id="6363a-132">Questo script aggiorna quindi la tabella creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6363a-132">This script then updates the table created previously.</span></span>

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a><span data-ttu-id="6363a-133">Verifica dello stato del processo</span><span class="sxs-lookup"><span data-stu-id="6363a-133">Checking job status</span></span>
<span data-ttu-id="6363a-134">Dopo aver iniziato un processo, è possibile controllarne lo stato di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="6363a-134">After a job has begun, you can check on its progress.</span></span>

1. <span data-ttu-id="6363a-135">Nella pagina del pool elastico fare clic su **Gestione processi**.</span><span class="sxs-lookup"><span data-stu-id="6363a-135">From the elastic pool page, click **Manage jobs**.</span></span>
   
    ![Fare clic su "Gestione processi"][2]
2. <span data-ttu-id="6363a-137">Fare clic sul nome (a) di un processo.</span><span class="sxs-lookup"><span data-stu-id="6363a-137">Click on the name (a) of a job.</span></span> <span data-ttu-id="6363a-138">Lo **STATO** può essere "Completato" o "Non riuscito".</span><span class="sxs-lookup"><span data-stu-id="6363a-138">The **STATUS** can be "Completed" or "Failed."</span></span> <span data-ttu-id="6363a-139">I dettagli del processo vengono visualizzati (b) insieme alla data e all'ora di creazione ed esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6363a-139">The job's details appear (b) with its date and time of creation and running.</span></span> <span data-ttu-id="6363a-140">L'elenco (c) sottostante mostra lo stato di avanzamento dello script su ogni database del pool, fornendo dettagli relativi alla data e all'ora.</span><span class="sxs-lookup"><span data-stu-id="6363a-140">The list (c) below the that shows the progress of the script against each database in the pool, giving its date and time details.</span></span>
   
    ![Controllo di un processo completato][3]

## <a name="checking-failed-jobs"></a><span data-ttu-id="6363a-142">Controllo dei processi non riusciti</span><span class="sxs-lookup"><span data-stu-id="6363a-142">Checking failed jobs</span></span>
<span data-ttu-id="6363a-143">Se un processo ha esito negativo, è disponibile un log dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6363a-143">If a job fails, a log of its execution can found.</span></span> <span data-ttu-id="6363a-144">Fare clic sul nome del processo non riuscito per visualizzarne i dettagli.</span><span class="sxs-lookup"><span data-stu-id="6363a-144">Click the name of the failed job to see its details.</span></span>

![Controllo di un processo non riuscito][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


