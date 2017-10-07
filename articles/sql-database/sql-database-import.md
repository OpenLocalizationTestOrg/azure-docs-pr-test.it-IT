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
# <a name="import-a-bacpac-file-tooa-new-azure-sql-database"></a>Importare un tooa file BACPAC Nuovo Database SQL di Azure

Quando è necessario un database da un archivio tooimport o durante la migrazione da un'altra piattaforma, è possibile importare lo schema del database hello e dati da un [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file. Un file BACPAC è un file ZIP con un'estensione di file BACPAC che contiene metadati hello e i dati da un database di SQL Server. È possibile importare un file BACPAC dall'archiviazione BLOB di Azure (solo archiviazione standard) o dall'archiviazione locale in un percorso locale. velocità di importazione toomaximize hello, si consiglia di specificare un servizio prestazioni e livello superiore, ad esempio un P6 e quindi ridimensionare toodown esigenze dopo l'importazione di hello ha esito positivo. Hello, inoltre, il livello di compatibilità del database dopo l'importazione di hello è basato sul livello di compatibilità hello hello del database di origine. 

> [!IMPORTANT] 
> Dopo la migrazione del Database SQL di tooAzure database, è possibile scegliere il database hello toooperate al livello corrente compatibilità (livello 100 per il database AdventureWorks2008R2 hello) o a un livello superiore. Per ulteriori informazioni sulle opzioni per l'uso di un database a un livello di compatibilità e le implicazioni di hello, vedere [del livello di compatibilità di ALTER DATABASE](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level). Vedere anche [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) per informazioni sulle impostazioni a livello di database aggiuntive correlate toocompatibility livelli.   >

> [!NOTE]
> tooimport un nuovo database tooa BACPAC, è innanzitutto necessario creare un server logico di Database SQL di Azure. Per un'esercitazione che mostra come toomigrate un Server SQL database tooAzure Database SQL utilizzando SQLPackage, vedere [eseguire la migrazione di un Database di SQL Server](sql-database-migrate-your-sql-server-database.md)
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a>Importare da un file BACPAC tramite il portale di Azure

In questo articolo vengono fornite istruzioni per la creazione di un database SQL di Azure da un file BACPAC archiviato nell'archiviazione blob di Azure utilizzando hello [portale di Azure](https://portal.azure.com). Importazione tramite hello solo portale di Azure supporta l'importazione di un file BACPAC dall'archiviazione blob di Azure.

un database utilizzando tooimport hello portale di Azure, pagina hello open per il database e fare clic su **importazione** sulla barra degli strumenti hello. Specificare contenitore e account di archiviazione hello e selezionare file BACPAC di hello da tooimport. Selezionare dimensioni hello del nuovo database hello (in genere hello stesso come origine) e fornire le credenziali SQL Server di destinazione hello.  

   ![Importazione di database](./media/sql-database-import/import.png)

lo stato di hello toomonitor di hello operazione di importazione, aprire la pagina hello per hello server logico contenente hello il database importato. Scorrere verso il basso troppo**operazioni** e quindi fare clic su **importazione/esportazione** cronologia.

### <a name="monitor-hello-progress-of-an-import-operation"></a>Monitorare l'avanzamento di un'operazione di importazione hello

lo stato di hello toomonitor di hello operazione di importazione, aprire la pagina hello per hello server logico in cui hello viene importato database importato. Scorrere verso il basso troppo**operazioni** e quindi fare clic su **importazione/esportazione** cronologia.
   
   ![importazione](./media/sql-database-import/import-history.png) ![stato importazione](./media/sql-database-import/import-status.png)

database hello tooverify in tempo reale sul server hello, fare clic su **database SQL** e verificare che sia di nuovo database hello **Online**.

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a>Importare da un file BACPAC tramite SQLPackage

tooimport un SQL database utilizzando hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) utilità della riga di comando, vedere [importare parametri e proprietà](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties). SQLPackage utilità Hello viene fornito con le versioni più recenti di hello [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) e [SQL Server Data Tools per Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), oppure è possibile scaricare una versione più recente di hello di [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) direttamente da hello Microsoft download center.

È consigliabile utilizzare hello di hello SQLPackage utilità per la scalabilità e prestazioni nella maggior parte degli ambienti di produzione. Per un Team di consulenza clienti di SQL Server tramite file BACPAC, vedere i blog sulla migrazione [la migrazione da SQL Server tooAzure Database SQL tramite file BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

Vedere hello comando SQLPackage per un esempio di script per la procedura seguente hello tooimport **AdventureWorks2008R2** database dall'archiviazione locale tooan Database SQL di Azure server logico, chiamato **mynewserver20170403** in questo esempio. Questo script illustra la creazione di hello di un nuovo database denominato **myMigratedDatabase**, con un livello di servizio di **Premium**e un obiettivo di servizio di **P6**. Modificare questi valori come ambiente tooyour appropriato.

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![importazione sqlpackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> Il server logico del database SQL di Azure è in ascolto sulla porta 1433. Se si sta tentando di tooconnect tooan Database SQL di Azure server logico all'interno di un firewall aziendale, questa porta deve essere aperta nel firewall aziendale hello per la connessione è toosuccessfully.
>

Questo esempio viene illustrato come tooimport un database tramite SqlPackage.exe con autenticazione universale di Active Directory:

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a>Importare da un file BACPAC tramite PowerShell

Hello utilizzare [New AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit un toohello di richiesta di importazione database servizio di Database SQL di Azure. A seconda delle dimensioni di hello del database, hello importazione può richiedere alcuni toocomplete ora.

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

stato di hello toocheck di hello della richiesta di importazione, utilizzare hello [Get AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet. L'esecuzione di questo hello subito dopo la richiesta in genere restituisce **stato: InProgress**. Quando viene visualizzato **stato: ha avuto esito positivo** importazione hello è stata completata.

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
Per un altro esempio di script, vedere [Importare un database da un file BACPAC](scripts/sql-database-import-from-bacpac-powershell.md).

## <a name="next-steps"></a>Passaggi successivi
* toolearn come tooconnect tooand query a un Database SQL importati, vedere [connettersi tooSQL Database con SQL Server Management Studio ed eseguire una query T-SQL di esempio](sql-database-connect-query-ssms.md).
* Per un Team di consulenza clienti di SQL Server tramite file BACPAC, vedere i blog sulla migrazione [la migrazione da SQL Server tooAzure Database SQL tramite file BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* Per una discussione di hello intero database migrazione processo di SQL Server, inclusi i consigli relativi alle prestazioni, vedere [eseguire la migrazione di un tooAzure di database di SQL Server Database SQL](sql-database-cloud-migrate.md).



