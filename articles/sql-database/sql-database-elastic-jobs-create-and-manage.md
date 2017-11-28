---
title: gruppi aaaManage di database SQL di Azure | Documenti Microsoft
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
ms.openlocfilehash: a73c4fb24c332fae0e917c18272724cccd56f29a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a><span data-ttu-id="5ed94-103">Creare e gestire database SQL di Azure con scalabilità orizzontale tramite processi elastici (anteprima)</span><span class="sxs-lookup"><span data-stu-id="5ed94-103">Create and manage scaled out Azure SQL Databases using elastic jobs (preview)</span></span>


<span data-ttu-id="5ed94-104">**processi di database elastico** semplificano la gestione dei gruppi di database con l'esecuzione di operazioni amministrative, come le modifiche dello schema, la gestione delle credenziali, gli aggiornamenti dei dati di riferimento, la raccolta dei dati sulle prestazioni o la raccolta dei dati di telemetria dei tenant (clienti).</span><span class="sxs-lookup"><span data-stu-id="5ed94-104">**Elastic Database jobs** simplify management of groups of databases by executing administrative operations such as schema changes, credentials management, reference data updates, performance data collection or tenant (customer) telemetry collection.</span></span> <span data-ttu-id="5ed94-105">I processi di Database elastici è attualmente disponibile tramite hello portale di Azure e i cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5ed94-105">Elastic Database jobs is currently available through hello Azure portal and PowerShell cmdlets.</span></span> <span data-ttu-id="5ed94-106">Tuttavia, hello aree del portale di Azure con funzionalità ridotte limitate tooexecution in tutti i database in un [pool elastico (anteprima)](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="5ed94-106">However, hello Azure portal surfaces reduced functionality limited tooexecution across all databases in an [elastic pool (preview)](sql-database-elastic-pool.md).</span></span> <span data-ttu-id="5ed94-107">set di funzionalità aggiuntive di tooaccess e l'esecuzione di script in un gruppo di database tra un insieme personalizzato o una partizione (creato utilizzando [libreria client di Database elastico](sql-database-elastic-scale-introduction.md)), vedere [creazione e gestione i processi tramite PowerShell](sql-database-elastic-jobs-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5ed94-107">tooaccess additional features and execution of scripts across a group of databases including a custom-defined collection or a shard set (created using [Elastic Database client library](sql-database-elastic-scale-introduction.md)), see [Creating and managing jobs using PowerShell](sql-database-elastic-jobs-powershell.md).</span></span> <span data-ttu-id="5ed94-108">Per ulteriori informazioni sui processi, vedere [Panoramica dei processi di database elastici](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5ed94-108">For more information about jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5ed94-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5ed94-109">Prerequisites</span></span>
* <span data-ttu-id="5ed94-110">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5ed94-110">An Azure subscription.</span></span> <span data-ttu-id="5ed94-111">Per una versione di valutazione gratuita, vedere [Versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5ed94-111">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5ed94-112">Un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="5ed94-112">An elastic pool.</span></span> <span data-ttu-id="5ed94-113">Vedere l'articolo sui [pool elastici](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="5ed94-113">See [About elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="5ed94-114">Installazione dei componenti del servizio relativo ai processi elastici di database.</span><span class="sxs-lookup"><span data-stu-id="5ed94-114">Installation of elastic database job service components.</span></span> <span data-ttu-id="5ed94-115">Vedere [installazione del servizio processo di database elastico hello](sql-database-elastic-jobs-service-installation.md).</span><span class="sxs-lookup"><span data-stu-id="5ed94-115">See [Installing hello elastic database job service](sql-database-elastic-jobs-service-installation.md).</span></span>

## <a name="creating-jobs"></a><span data-ttu-id="5ed94-116">Creazione di processi</span><span class="sxs-lookup"><span data-stu-id="5ed94-116">Creating jobs</span></span>
1. <span data-ttu-id="5ed94-117">Utilizzo di hello [portale di Azure](https://portal.azure.com), da un pool di processi di database elastici esistente, fare clic su **processo di creazione**.</span><span class="sxs-lookup"><span data-stu-id="5ed94-117">Using hello [Azure portal](https://portal.azure.com), from an existing elastic database job pool, click **Create job**.</span></span>
2. <span data-ttu-id="5ed94-118">Digitare nome utente hello e la password dell'amministratore del database hello (creato al momento dell'installazione dei processi) per il database di controllo processi hello (archiviazione di metadati per i processi).</span><span class="sxs-lookup"><span data-stu-id="5ed94-118">Type in hello username and password of hello database administrator (created at installation of Jobs) for hello jobs control database (metadata storage for jobs).</span></span>
   
    ![Nome del processo hello, digitare o incollare nel codice e fare clic su Esegui][1]
3. <span data-ttu-id="5ed94-120">In hello **Crea processo** pannello, digitare un nome per il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="5ed94-120">In hello **Create Job** blade, type a name for hello job.</span></span>
4. <span data-ttu-id="5ed94-121">Digitare hello nome e la password tooconnect toohello destinazione database utente con autorizzazioni sufficienti per toosucceed di esecuzione di script.</span><span class="sxs-lookup"><span data-stu-id="5ed94-121">Type hello user name and password tooconnect toohello target databases with sufficient permissions for script execution toosucceed.</span></span>
5. <span data-ttu-id="5ed94-122">Incollare o digitare nello script T-SQL hello.</span><span class="sxs-lookup"><span data-stu-id="5ed94-122">Paste or type in hello T-SQL script.</span></span>
6. <span data-ttu-id="5ed94-123">Fare clic su **Salva** e quindi su **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="5ed94-123">Click **Save** and then click **Run**.</span></span>
   
    ![Creare processi ed eseguirli][5]

## <a name="run-idempotent-jobs"></a><span data-ttu-id="5ed94-125">Eseguire processi idempotenti</span><span class="sxs-lookup"><span data-stu-id="5ed94-125">Run idempotent jobs</span></span>
<span data-ttu-id="5ed94-126">Quando si esegue uno script con un set di database, è necessario assicurarsi che script hello è idempotente.</span><span class="sxs-lookup"><span data-stu-id="5ed94-126">When you run a script against a set of databases, you must be sure that hello script is idempotent.</span></span> <span data-ttu-id="5ed94-127">Vale a dire hello script deve essere in grado di toorun più volte, anche se non è riuscito prima in uno stato incompleto.</span><span class="sxs-lookup"><span data-stu-id="5ed94-127">That is, hello script must be able toorun multiple times, even if it has failed before in an incomplete state.</span></span> <span data-ttu-id="5ed94-128">Ad esempio, quando uno script non riesce, il processo di hello verrà automaticamente ritentato fino al completamento (entro i limiti, come ripetere hello logica infine smetteranno hello ritentare).</span><span class="sxs-lookup"><span data-stu-id="5ed94-128">For example, when a script fails, hello job will be automatically retried until it succeeds (within limits, as hello retry logic will eventually cease hello retrying).</span></span> <span data-ttu-id="5ed94-129">Hello modo toodo questo è hello toouse una clausola "IF EXISTS" e l'eliminazione di qualsiasi istanza presente prima di creare un nuovo oggetto.</span><span class="sxs-lookup"><span data-stu-id="5ed94-129">hello way toodo this is toouse hello an "IF EXISTS" clause and delete any found instance before creating a new object.</span></span> <span data-ttu-id="5ed94-130">Di seguito è riportato un esempio:</span><span class="sxs-lookup"><span data-stu-id="5ed94-130">An example is shown here:</span></span>

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

<span data-ttu-id="5ed94-131">In alternativa, usare una clausola "IF NOT EXISTS" prima di creare una nuova istanza:</span><span class="sxs-lookup"><span data-stu-id="5ed94-131">Alternatively, use an "IF NOT EXISTS" clause before creating a new instance:</span></span>

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

<span data-ttu-id="5ed94-132">Questo script Aggiorna tabella hello creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5ed94-132">This script then updates hello table created previously.</span></span>

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a><span data-ttu-id="5ed94-133">Verifica dello stato del processo</span><span class="sxs-lookup"><span data-stu-id="5ed94-133">Checking job status</span></span>
<span data-ttu-id="5ed94-134">Dopo aver iniziato un processo, è possibile controllarne lo stato di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="5ed94-134">After a job has begun, you can check on its progress.</span></span>

1. <span data-ttu-id="5ed94-135">Dalla pagina di pool elastico hello, fare clic su **gestire processi**.</span><span class="sxs-lookup"><span data-stu-id="5ed94-135">From hello elastic pool page, click **Manage jobs**.</span></span>
   
    ![Fare clic su "Gestione processi"][2]
2. <span data-ttu-id="5ed94-137">Fare clic su hello Nome (a) di un processo.</span><span class="sxs-lookup"><span data-stu-id="5ed94-137">Click on hello name (a) of a job.</span></span> <span data-ttu-id="5ed94-138">Hello **stato** può essere "Completed" o "Failed".</span><span class="sxs-lookup"><span data-stu-id="5ed94-138">hello **STATUS** can be "Completed" or "Failed."</span></span> <span data-ttu-id="5ed94-139">dettagli del processo di Hello vengono visualizzate (b) con data e ora di creazione e l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="5ed94-139">hello job's details appear (b) with its date and time of creation and running.</span></span> <span data-ttu-id="5ed94-140">elenco di Hello (c) seguito hello che mostra lo stato di avanzamento hello dello script hello in tutti i database nel pool di hello, fornendo i dettagli di data e ora.</span><span class="sxs-lookup"><span data-stu-id="5ed94-140">hello list (c) below hello that shows hello progress of hello script against each database in hello pool, giving its date and time details.</span></span>
   
    ![Controllo di un processo completato][3]

## <a name="checking-failed-jobs"></a><span data-ttu-id="5ed94-142">Controllo dei processi non riusciti</span><span class="sxs-lookup"><span data-stu-id="5ed94-142">Checking failed jobs</span></span>
<span data-ttu-id="5ed94-143">Se un processo ha esito negativo, è disponibile un log dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="5ed94-143">If a job fails, a log of its execution can found.</span></span> <span data-ttu-id="5ed94-144">Fare clic su nome hello di hello non è stato possibile processo toosee i dettagli.</span><span class="sxs-lookup"><span data-stu-id="5ed94-144">Click hello name of hello failed job toosee its details.</span></span>

![Controllo di un processo non riuscito][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


