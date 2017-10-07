---
title: un file BACPAC aaaImport file toocreate un database SQL di Azure | Documenti Microsoft
description: Creare un nuovo database SQL di Azure importando un file BACPAC.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: cf9a9631-56aa-4985-a565-1cacc297871d
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/26/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 0d5fc93acf27b79502969fcd6199d11161915b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="import-a-bacpac-file-tooa-new-azure-sql-database"></a><span data-ttu-id="f41d5-103">Importare un tooa file BACPAC Nuovo Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="f41d5-103">Import a BACPAC file tooa new Azure SQL Database</span></span>

<span data-ttu-id="f41d5-104">Quando è necessario un database da un archivio tooimport o durante la migrazione da un'altra piattaforma, è possibile importare lo schema del database hello e dati da un [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span><span class="sxs-lookup"><span data-stu-id="f41d5-104">When you need tooimport a database from an archive or when migrating from another platform, you can import hello database schema and data from a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span></span> <span data-ttu-id="f41d5-105">Un file BACPAC è un file ZIP con un'estensione di file BACPAC che contiene metadati hello e i dati da un database di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f41d5-105">A BACPAC file is a ZIP file with an extension of BACPAC containing hello metadata and data from a SQL Server database.</span></span> <span data-ttu-id="f41d5-106">È possibile importare un file BACPAC dall'archiviazione BLOB di Azure (solo archiviazione standard) o dall'archiviazione locale in un percorso locale.</span><span class="sxs-lookup"><span data-stu-id="f41d5-106">A BACPAC file can be imported from Azure blob storage (standard storage only) or from local storage in an on-premises location.</span></span> <span data-ttu-id="f41d5-107">velocità di importazione toomaximize hello, si consiglia di specificare un servizio prestazioni e livello superiore, ad esempio un P6 e quindi ridimensionare toodown esigenze dopo l'importazione di hello ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="f41d5-107">toomaximize hello import speed, we recommend that you specify a higher service tier and performance level, such as a P6, and then scale toodown as appropriate after hello import is successful.</span></span> <span data-ttu-id="f41d5-108">Hello, inoltre, il livello di compatibilità del database dopo l'importazione di hello è basato sul livello di compatibilità hello hello del database di origine.</span><span class="sxs-lookup"><span data-stu-id="f41d5-108">Also, hello database compatibility level after hello import is based on hello compatibility level of hello source database.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="f41d5-109">Dopo la migrazione del Database SQL di tooAzure database, è possibile scegliere il database hello toooperate al livello corrente compatibilità (livello 100 per il database AdventureWorks2008R2 hello) o a un livello superiore.</span><span class="sxs-lookup"><span data-stu-id="f41d5-109">After you migrate your database tooAzure SQL Database, you can choose toooperate hello database at its current compatibility level (level 100 for hello AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="f41d5-110">Per ulteriori informazioni sulle opzioni per l'uso di un database a un livello di compatibilità e le implicazioni di hello, vedere [del livello di compatibilità di ALTER DATABASE](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span><span class="sxs-lookup"><span data-stu-id="f41d5-110">For more information on hello implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="f41d5-111">Vedere anche [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) per informazioni sulle impostazioni a livello di database aggiuntive correlate toocompatibility livelli.</span><span class="sxs-lookup"><span data-stu-id="f41d5-111">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related toocompatibility levels.</span></span>   >

> [!NOTE]
> <span data-ttu-id="f41d5-112">tooimport un nuovo database tooa BACPAC, è innanzitutto necessario creare un server logico di Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="f41d5-112">tooimport a BACPAC tooa new database, you must first create an Azure SQL Database logical server.</span></span> <span data-ttu-id="f41d5-113">Per un'esercitazione che mostra come toomigrate un Server SQL database tooAzure Database SQL utilizzando SQLPackage, vedere [eseguire la migrazione di un Database di SQL Server](sql-database-migrate-your-sql-server-database.md)</span><span class="sxs-lookup"><span data-stu-id="f41d5-113">For a tutorial showing you how toomigrate a SQL Server database tooAzure SQL Database using SQLPackage, see [Migrate a SQL Server Database](sql-database-migrate-your-sql-server-database.md)</span></span>
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a><span data-ttu-id="f41d5-114">Importare da un file BACPAC tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f41d5-114">Import from a BACPAC file using Azure portal</span></span>

<span data-ttu-id="f41d5-115">In questo articolo vengono fornite istruzioni per la creazione di un database SQL di Azure da un file BACPAC archiviato nell'archiviazione blob di Azure utilizzando hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f41d5-115">This article provides directions for creating an Azure SQL database from a BACPAC file stored in Azure blob storage using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f41d5-116">Importazione tramite hello solo portale di Azure supporta l'importazione di un file BACPAC dall'archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="f41d5-116">Import using hello Azure portal only supports importing a BACPAC file from Azure blob storage.</span></span>

<span data-ttu-id="f41d5-117">un database utilizzando tooimport hello portale di Azure, pagina hello open per il database e fare clic su **importazione** sulla barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="f41d5-117">tooimport a database using hello Azure portal, open hello page for your database and click **Import** on hello toolbar.</span></span> <span data-ttu-id="f41d5-118">Specificare contenitore e account di archiviazione hello e selezionare file BACPAC di hello da tooimport.</span><span class="sxs-lookup"><span data-stu-id="f41d5-118">Specify hello storage account and container, and select hello BACPAC file you want tooimport.</span></span> <span data-ttu-id="f41d5-119">Selezionare dimensioni hello del nuovo database hello (in genere hello stesso come origine) e fornire le credenziali SQL Server di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="f41d5-119">Select hello size of hello new database (usually hello same as origin) and provide hello destination SQL Server credentials.</span></span>  

   ![Importazione di database](./media/sql-database-import/import.png)

<span data-ttu-id="f41d5-121">lo stato di hello toomonitor di hello operazione di importazione, aprire la pagina hello per hello server logico contenente hello il database importato.</span><span class="sxs-lookup"><span data-stu-id="f41d5-121">toomonitor hello progress of hello import operation, open hello page for hello logical server containing hello database being imported.</span></span> <span data-ttu-id="f41d5-122">Scorrere verso il basso troppo**operazioni** e quindi fare clic su **importazione/esportazione** cronologia.</span><span class="sxs-lookup"><span data-stu-id="f41d5-122">Scroll down too**Operations** and then click **Import/Export** history.</span></span>

### <a name="monitor-hello-progress-of-an-import-operation"></a><span data-ttu-id="f41d5-123">Monitorare l'avanzamento di un'operazione di importazione hello</span><span class="sxs-lookup"><span data-stu-id="f41d5-123">Monitor hello progress of an import operation</span></span>

<span data-ttu-id="f41d5-124">lo stato di hello toomonitor di hello operazione di importazione, aprire la pagina hello per hello server logico in cui hello viene importato database importato.</span><span class="sxs-lookup"><span data-stu-id="f41d5-124">toomonitor hello progress of hello import operation, open hello page for hello logical server into which hello database is being imported imported.</span></span> <span data-ttu-id="f41d5-125">Scorrere verso il basso troppo**operazioni** e quindi fare clic su **importazione/esportazione** cronologia.</span><span class="sxs-lookup"><span data-stu-id="f41d5-125">Scroll down too**Operations** and then click **Import/Export** history.</span></span>
   
   <span data-ttu-id="f41d5-126">![importazione](./media/sql-database-import/import-history.png) ![stato importazione](./media/sql-database-import/import-status.png)</span><span class="sxs-lookup"><span data-stu-id="f41d5-126">![import](./media/sql-database-import/import-history.png) ![import status](./media/sql-database-import/import-status.png)</span></span>

<span data-ttu-id="f41d5-127">database hello tooverify in tempo reale sul server hello, fare clic su **database SQL** e verificare che sia di nuovo database hello **Online**.</span><span class="sxs-lookup"><span data-stu-id="f41d5-127">tooverify hello database is live on hello server, click **SQL databases** and verify hello new database is **Online**.</span></span>

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a><span data-ttu-id="f41d5-128">Importare da un file BACPAC tramite SQLPackage</span><span class="sxs-lookup"><span data-stu-id="f41d5-128">Import from a BACPAC file using SQLPackage</span></span>

<span data-ttu-id="f41d5-129">tooimport un SQL database utilizzando hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) utilità della riga di comando, vedere [importare parametri e proprietà](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span><span class="sxs-lookup"><span data-stu-id="f41d5-129">tooimport a SQL database using hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Import parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span></span> <span data-ttu-id="f41d5-130">SQLPackage utilità Hello viene fornito con le versioni più recenti di hello [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) e [SQL Server Data Tools per Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), oppure è possibile scaricare una versione più recente di hello di [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) direttamente da hello Microsoft download center.</span><span class="sxs-lookup"><span data-stu-id="f41d5-130">hello SQLPackage utility ships with hello latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download hello latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from hello Microsoft download center.</span></span>

<span data-ttu-id="f41d5-131">È consigliabile utilizzare hello di hello SQLPackage utilità per la scalabilità e prestazioni nella maggior parte degli ambienti di produzione.</span><span class="sxs-lookup"><span data-stu-id="f41d5-131">We recommend hello use of hello SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="f41d5-132">Per un Team di consulenza clienti di SQL Server tramite file BACPAC, vedere i blog sulla migrazione [la migrazione da SQL Server tooAzure Database SQL tramite file BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="f41d5-132">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

<span data-ttu-id="f41d5-133">Vedere hello comando SQLPackage per un esempio di script per la procedura seguente hello tooimport **AdventureWorks2008R2** database dall'archiviazione locale tooan Database SQL di Azure server logico, chiamato **mynewserver20170403** in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="f41d5-133">See hello following SQLPackage command for a script example for how tooimport hello **AdventureWorks2008R2** database from local storage tooan Azure SQL Database logical server, called **mynewserver20170403** in this example.</span></span> <span data-ttu-id="f41d5-134">Questo script illustra la creazione di hello di un nuovo database denominato **myMigratedDatabase**, con un livello di servizio di **Premium**e un obiettivo di servizio di **P6**.</span><span class="sxs-lookup"><span data-stu-id="f41d5-134">This script shows hello creation of a new database called **myMigratedDatabase**, with a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="f41d5-135">Modificare questi valori come ambiente tooyour appropriato.</span><span class="sxs-lookup"><span data-stu-id="f41d5-135">Change these values as appropriate tooyour environment.</span></span>

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![importazione sqlpackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="f41d5-137">Il server logico del database SQL di Azure è in ascolto sulla porta 1433.</span><span class="sxs-lookup"><span data-stu-id="f41d5-137">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="f41d5-138">Se si sta tentando di tooconnect tooan Database SQL di Azure server logico all'interno di un firewall aziendale, questa porta deve essere aperta nel firewall aziendale hello per la connessione è toosuccessfully.</span><span class="sxs-lookup"><span data-stu-id="f41d5-138">If you are attempting tooconnect tooan Azure SQL Database logical server from within a corporate firewall, this port must be open in hello corporate firewall for you toosuccessfully connect.</span></span>
>

<span data-ttu-id="f41d5-139">Questo esempio viene illustrato come tooimport un database tramite SqlPackage.exe con autenticazione universale di Active Directory:</span><span class="sxs-lookup"><span data-stu-id="f41d5-139">This example shows how tooimport a database using SqlPackage.exe with Active Directory Universal Authentication:</span></span>

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a><span data-ttu-id="f41d5-140">Importare da un file BACPAC tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="f41d5-140">Import from a BACPAC file using PowerShell</span></span>

<span data-ttu-id="f41d5-141">Hello utilizzare [New AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit un toohello di richiesta di importazione database servizio di Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="f41d5-141">Use hello [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit an import database request toohello Azure SQL Database service.</span></span> <span data-ttu-id="f41d5-142">A seconda delle dimensioni di hello del database, hello importazione può richiedere alcuni toocomplete ora.</span><span class="sxs-lookup"><span data-stu-id="f41d5-142">Depending on hello size of your database, hello import operation may take some time toocomplete.</span></span>

 ```powershell
 $importRequest = New-AzureRmSqlDatabaseImport -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "MyImportSample" `
    -DatabaseMaxSizeBytes "262144000" `
    -StorageKeyType "StorageAccessKey" `
    -StorageKey $(Get-AzureRmStorageAccountKey -ResourceGroupName "myResourceGroup" -StorageAccountName $storageaccountname).Value[0] `
    -StorageUri "http://$storageaccountname.blob.core.windows.net/importsample/sample.bacpac" `
    -Edition "Standard" `
    -ServiceObjectiveName "P6" `
    -AdministratorLogin "ServerAdmin" `
    -AdministratorLoginPassword $(ConvertTo-SecureString -String "ASecureP@assw0rd" -AsPlainText -Force)

 ```

<span data-ttu-id="f41d5-143">stato di hello toocheck di hello della richiesta di importazione, utilizzare hello [Get AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f41d5-143">toocheck hello status of hello import request, use hello [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="f41d5-144">L'esecuzione di questo hello subito dopo la richiesta in genere restituisce **stato: InProgress**.</span><span class="sxs-lookup"><span data-stu-id="f41d5-144">Running this immediately after hello request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="f41d5-145">Quando viene visualizzato **stato: ha avuto esito positivo** importazione hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="f41d5-145">When you see **Status: Succeeded** hello import is complete.</span></span>

```powershell
$importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
[Console]::Write("Importing")
while ($importStatus.Status -eq "InProgress")
{
    $importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$importStatus
```

> [!TIP]
<span data-ttu-id="f41d5-146">Per un altro esempio di script, vedere [Importare un database da un file BACPAC](scripts/sql-database-import-from-bacpac-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f41d5-146">For another script example, see [Import a database from a BACPAC file](scripts/sql-database-import-from-bacpac-powershell.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f41d5-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f41d5-147">Next steps</span></span>
* <span data-ttu-id="f41d5-148">toolearn come tooconnect tooand query a un Database SQL importati, vedere [connettersi tooSQL Database con SQL Server Management Studio ed eseguire una query T-SQL di esempio](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="f41d5-148">toolearn how tooconnect tooand query an imported SQL Database, see [Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>
* <span data-ttu-id="f41d5-149">Per un Team di consulenza clienti di SQL Server tramite file BACPAC, vedere i blog sulla migrazione [la migrazione da SQL Server tooAzure Database SQL tramite file BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="f41d5-149">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="f41d5-150">Per una discussione di hello intero database migrazione processo di SQL Server, inclusi i consigli relativi alle prestazioni, vedere [eseguire la migrazione di un tooAzure di database di SQL Server Database SQL](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="f41d5-150">For a discussion of hello entire SQL Server database migration process, including performance recommendations, see [Migrate a SQL Server database tooAzure SQL Database](sql-database-cloud-migrate.md).</span></span>



