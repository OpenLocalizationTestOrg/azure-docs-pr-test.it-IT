---
title: Importare un file BACPAC per creare un database SQL di Azure | Microsoft Docs
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
ms.openlocfilehash: 285e17ed6d0ce700cb518864df7a3b5f5e55bee5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="import-a-bacpac-file-to-a-new-azure-sql-database"></a><span data-ttu-id="fe21d-103">Importare un file BACPAC in un nuovo database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="fe21d-103">Import a BACPAC file to a new Azure SQL Database</span></span>

<span data-ttu-id="fe21d-104">Quando è necessario importare un database da un archivio o eseguire la migrazione da un'altra piattaforma, è possibile importare lo schema e i dati del database da un file [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4).</span><span class="sxs-lookup"><span data-stu-id="fe21d-104">When you need to import a database from an archive or when migrating from another platform, you can import the database schema and data from a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span></span> <span data-ttu-id="fe21d-105">Un file BACPAC è un file ZIP con un'estensione bacpac contenente i metadati e dati da un database di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fe21d-105">A BACPAC file is a ZIP file with an extension of BACPAC containing the metadata and data from a SQL Server database.</span></span> <span data-ttu-id="fe21d-106">È possibile importare un file BACPAC dall'archiviazione BLOB di Azure (solo archiviazione standard) o dall'archiviazione locale in un percorso locale.</span><span class="sxs-lookup"><span data-stu-id="fe21d-106">A BACPAC file can be imported from Azure blob storage (standard storage only) or from local storage in an on-premises location.</span></span> <span data-ttu-id="fe21d-107">Per ottimizzare la velocità di importazione, è consigliabile specificare un livello di servizio e prestazioni superiore, ad esempio un P6, e quindi applicare la scalabilità verso il basso in base alle esigenze dopo che l'importazione ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="fe21d-107">To maximize the import speed, we recommend that you specify a higher service tier and performance level, such as a P6, and then scale to down as appropriate after the import is successful.</span></span> <span data-ttu-id="fe21d-108">Il livello di compatibilità del database dopo l'importazione si basa anche sul livello di compatibilità del database di origine.</span><span class="sxs-lookup"><span data-stu-id="fe21d-108">Also, the database compatibility level after the import is based on the compatibility level of the source database.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="fe21d-109">Dopo la migrazione del database al database SQL di Azure, è possibile scegliere per il funzionamento del database al livello di compatibilità corrente (livello 100 per il database AdventureWorks2008R2) o a un livello superiore.</span><span class="sxs-lookup"><span data-stu-id="fe21d-109">After you migrate your database to Azure SQL Database, you can choose to operate the database at its current compatibility level (level 100 for the AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="fe21d-110">Per altre informazioni sulle implicazioni e le opzioni per il funzionamento di un database a un livello di compatibilità specifico, vedere [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level) (Livello di compatibilità ALTER DATABASE).</span><span class="sxs-lookup"><span data-stu-id="fe21d-110">For more information on the implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="fe21d-111">Vedere anche [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) per informazioni sulle impostazioni a livello di database aggiuntive relative ai livelli di compatibilità.</span><span class="sxs-lookup"><span data-stu-id="fe21d-111">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related to compatibility levels.</span></span>   >

> [!NOTE]
> <span data-ttu-id="fe21d-112">Per importare un file BACPAC in un nuovo database, è necessario prima creare un server logico di database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="fe21d-112">To import a BACPAC to a new database, you must first create an Azure SQL Database logical server.</span></span> <span data-ttu-id="fe21d-113">Per un'esercitazione che spiega come eseguire la migrazione di un database SQL Server al database SQL di Azure tramite SQLPackage, vedere [Migrate a SQL Server Database](sql-database-migrate-your-sql-server-database.md) (Eseguire la migrazione di un database SQL Server)</span><span class="sxs-lookup"><span data-stu-id="fe21d-113">For a tutorial showing you how to migrate a SQL Server database to Azure SQL Database using SQLPackage, see [Migrate a SQL Server Database](sql-database-migrate-your-sql-server-database.md)</span></span>
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a><span data-ttu-id="fe21d-114">Importare da un file BACPAC tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="fe21d-114">Import from a BACPAC file using Azure portal</span></span>

<span data-ttu-id="fe21d-115">Questo articolo illustra come usare il [portale di Azure](https://portal.azure.com) per creare un database SQL di Azure a partire da un file BACPAC archiviato nell'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="fe21d-115">This article provides directions for creating an Azure SQL database from a BACPAC file stored in Azure blob storage using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fe21d-116">L'importazione tramite il portale di Azure supporta solo l'importazione di un file BACPAC dall'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="fe21d-116">Import using the Azure portal only supports importing a BACPAC file from Azure blob storage.</span></span>

<span data-ttu-id="fe21d-117">Per importare un database tramite il portale di Azure, aprire la pagina per il database e fare clic su **Importa** sulla barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="fe21d-117">To import a database using the Azure portal, open the page for your database and click **Import** on the toolbar.</span></span> <span data-ttu-id="fe21d-118">Specificare l'account di archiviazione e il contenitore e quindi selezionare il file BACPAC che si vuole importare.</span><span class="sxs-lookup"><span data-stu-id="fe21d-118">Specify the storage account and container, and select the BACPAC file you want to import.</span></span> <span data-ttu-id="fe21d-119">Selezionare la dimensione del nuovo database (in genere lo stesso dell'origine) e specificare le credenziali di SQL Server di destinazione.</span><span class="sxs-lookup"><span data-stu-id="fe21d-119">Select the size of the new database (usually the same as origin) and provide the destination SQL Server credentials.</span></span>  

   ![Importazione di database](./media/sql-database-import/import.png)

<span data-ttu-id="fe21d-121">Per monitorare lo stato di avanzamento dell'operazione di importazione, aprire la pagina per il server logico contenente il database importato.</span><span class="sxs-lookup"><span data-stu-id="fe21d-121">To monitor the progress of the import operation, open the page for the logical server containing the database being imported.</span></span> <span data-ttu-id="fe21d-122">Scorrere fino a **Operazioni** e quindi fare clic sulla cronologia di **Importazione/Esportazione**.</span><span class="sxs-lookup"><span data-stu-id="fe21d-122">Scroll down to **Operations** and then click **Import/Export** history.</span></span>

### <a name="monitor-the-progress-of-an-import-operation"></a><span data-ttu-id="fe21d-123">Monitorare lo stato di un'operazione di importazione</span><span class="sxs-lookup"><span data-stu-id="fe21d-123">Monitor the progress of an import operation</span></span>

<span data-ttu-id="fe21d-124">Per monitorare lo stato di avanzamento dell'operazione di importazione, aprire la pagina per il server logico in cui viene importato il database.</span><span class="sxs-lookup"><span data-stu-id="fe21d-124">To monitor the progress of the import operation, open the page for the logical server into which the database is being imported imported.</span></span> <span data-ttu-id="fe21d-125">Scorrere fino a **Operazioni** e quindi fare clic sulla cronologia di **Importazione/Esportazione**.</span><span class="sxs-lookup"><span data-stu-id="fe21d-125">Scroll down to **Operations** and then click **Import/Export** history.</span></span>
   
   <span data-ttu-id="fe21d-126">![importazione](./media/sql-database-import/import-history.png) ![stato importazione](./media/sql-database-import/import-status.png)</span><span class="sxs-lookup"><span data-stu-id="fe21d-126">![import](./media/sql-database-import/import-history.png) ![import status](./media/sql-database-import/import-status.png)</span></span>

<span data-ttu-id="fe21d-127">Per verificare che il database sia attivo nel server, fare clic su **Database SQL** e verificare che il nuovo database sia **Online**.</span><span class="sxs-lookup"><span data-stu-id="fe21d-127">To verify the database is live on the server, click **SQL databases** and verify the new database is **Online**.</span></span>

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a><span data-ttu-id="fe21d-128">Importare da un file BACPAC tramite SQLPackage</span><span class="sxs-lookup"><span data-stu-id="fe21d-128">Import from a BACPAC file using SQLPackage</span></span>

<span data-ttu-id="fe21d-129">Per importare un database SQL tramite l'utilità della riga di comando [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx), vedere la sezione relativa ai [parametri e proprietà dell'importazione](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span><span class="sxs-lookup"><span data-stu-id="fe21d-129">To import a SQL database using the [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Import parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span></span> <span data-ttu-id="fe21d-130">L'utilità SQLPackage viene offerta con le versioni più recenti di [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) e [SQL Server Data Tools per Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), oppure è possibile scaricare la versione più recente di [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) direttamente dall'area download Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fe21d-130">The SQLPackage utility ships with the latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download the latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from the Microsoft download center.</span></span>

<span data-ttu-id="fe21d-131">È consigliabile usare l'utilità SQLPackage per la scalabilità e le prestazioni nella maggior parte degli ambienti di produzione.</span><span class="sxs-lookup"><span data-stu-id="fe21d-131">We recommend the use of the SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="fe21d-132">Per informazioni sull'uso di file BACPAC per la migrazione, vedere l'articolo [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/) (Migrazione da SQL Server al database SQL di Azure con file BACPAC) del blog del Customer Advisory Team di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fe21d-132">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

<span data-ttu-id="fe21d-133">Vedere il comando SQLPackage seguente per uno script di esempio che illustra come importare il database **AdventureWorks2008R2** dalla risorsa di archiviazione locale a un server logico del database SQL di Azure, chiamato **mynewserver20170403** in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="fe21d-133">See the following SQLPackage command for a script example for how to import the **AdventureWorks2008R2** database from local storage to an Azure SQL Database logical server, called **mynewserver20170403** in this example.</span></span> <span data-ttu-id="fe21d-134">Questo script illustra la creazione di un nuovo database denominato **myMigratedDatabase**, con un livello di servizio **Premium** e un obiettivo di servizio **P6**.</span><span class="sxs-lookup"><span data-stu-id="fe21d-134">This script shows the creation of a new database called **myMigratedDatabase**, with a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="fe21d-135">Sostituire i valori in base alle esigenze specifiche dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="fe21d-135">Change these values as appropriate to your environment.</span></span>

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![importazione sqlpackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="fe21d-137">Il server logico del database SQL di Azure è in ascolto sulla porta 1433.</span><span class="sxs-lookup"><span data-stu-id="fe21d-137">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="fe21d-138">Se si sta tentando di connettersi a un server logico del database SQL di Azure dall'interno di un firewall aziendale, questa porta deve essere aperta.</span><span class="sxs-lookup"><span data-stu-id="fe21d-138">If you are attempting to connect to an Azure SQL Database logical server from within a corporate firewall, this port must be open in the corporate firewall for you to successfully connect.</span></span>
>

<span data-ttu-id="fe21d-139">Questo esempio illustra come importare un database usando SqlPackage.exe con l'autenticazione universale di Active Directory:</span><span class="sxs-lookup"><span data-stu-id="fe21d-139">This example shows how to import a database using SqlPackage.exe with Active Directory Universal Authentication:</span></span>

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a><span data-ttu-id="fe21d-140">Importare da un file BACPAC tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe21d-140">Import from a BACPAC file using PowerShell</span></span>

<span data-ttu-id="fe21d-141">Usare il cmdlet [AzureRmSqlDatabaseImport New](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) per inviare una richiesta di importazione database al servizio database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="fe21d-141">Use the [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet to submit an import database request to the Azure SQL Database service.</span></span> <span data-ttu-id="fe21d-142">A seconda delle dimensioni del database, l'operazione di esportazione potrebbe richiedere diverso tempo.</span><span class="sxs-lookup"><span data-stu-id="fe21d-142">Depending on the size of your database, the import operation may take some time to complete.</span></span>

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

<span data-ttu-id="fe21d-143">Per verificare lo stato della richiesta di importazione, usare il cmdlet [AzureRmSqlDatabaseImportExportStatus Get](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus).</span><span class="sxs-lookup"><span data-stu-id="fe21d-143">To check the status of the import request, use the [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="fe21d-144">L'esecuzione di questo cmdlet subito dopo la richiesta restituisce in genere **Status: InProgress**.</span><span class="sxs-lookup"><span data-stu-id="fe21d-144">Running this immediately after the request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="fe21d-145">Al termine dell'esportazione, il messaggio restituito è **Status: Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="fe21d-145">When you see **Status: Succeeded** the import is complete.</span></span>

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
<span data-ttu-id="fe21d-146">Per un altro esempio di script, vedere [Importare un database da un file BACPAC](scripts/sql-database-import-from-bacpac-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fe21d-146">For another script example, see [Import a database from a BACPAC file](scripts/sql-database-import-from-bacpac-powershell.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe21d-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fe21d-147">Next steps</span></span>
* <span data-ttu-id="fe21d-148">Per informazioni su come connettersi ed eseguire query su un database SQL importato, vedere [Connettersi al database SQL con SQL Server Management Studio ed eseguire una query T-SQL di esempio](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="fe21d-148">To learn how to connect to and query an imported SQL Database, see [Connect to SQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>
* <span data-ttu-id="fe21d-149">Per informazioni sull'uso di file BACPAC per la migrazione, vedere l'articolo [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/) (Migrazione da SQL Server al database SQL di Azure con file BACPAC) del blog del Customer Advisory Team di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fe21d-149">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="fe21d-150">Per una descrizione dell'intero processo di migrazione del database SQL Server, tra cui raccomandazioni sulle prestazioni, vedere [Migrare un database SQL Server nel database SQL di Azure](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="fe21d-150">For a discussion of the entire SQL Server database migration process, including performance recommendations, see [Migrate a SQL Server database to Azure SQL Database](sql-database-cloud-migrate.md).</span></span>



