---
title: un file BACPAC di SQL Azure database tooa aaaExport | Documenti Microsoft
description: Esportare un file BACPAC di SQL Azure database tooa utilizzando hello portale di Azure
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 41d63a97-37db-4e40-b652-77c2fd1c09b7
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: cb3b4227318e0fd2114529c86c9792615fe7fd1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-sql-database-tooa-bacpac-file"></a>Esportare un file BACPAC tooa database di SQL Azure

Quando è necessario tooexport un database di archiviazione o per la piattaforma tooanother mobile, è possibile esportare tooa schema e i dati del database hello [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file. Un file BACPAC è un file ZIP con un'estensione di file BACPAC che contiene metadati hello e i dati da un database di SQL Server. È possibile memorizzare questo tipo di file in un'archiviazione BLOB di Azure o in un'archiviazione locale e successivamente importarlo nuovamente nel database SQL di Azure o in un'installazione locale di SQL Server. 

> [!IMPORTANT] 
> La funzionalità di esportazione automatizzata di database SQL di Azure è stata ritirata il 1° marzo 2017. È possibile utilizzare [conservazione dei backup a lungo termine](sql-database-long-term-retention.md
) o [automazione di Azure](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md) tooperiodically database SQL di archiviazione usando PowerShell in base a pianificazione tooa di propria scelta. Per un esempio, scaricare hello [script PowerShell di esempio](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export) da Github.
>

## <a name="considerations-when-exporting-an-azure-sql-database"></a>Considerazioni relative all'esportazione di un database SQL di Azure

* Per un'esportazione toobe consistente, è necessario assicurarsi che si verifichi alcuna attività di scrittura durante l'esportazione di hello, o che si desidera esportare i dati un [copia consistente](sql-database-copy.md) del database SQL di Azure.
* Se si sta esportando archiviazione tooblob, hello massima di un file BACPAC è 200 GB. un file BACPAC più grande, tooarchive esportare toolocal archiviazione.
* L'esportazione di un'archiviazione premium BACPAC file tooAzure hello metodi descritti in questo articolo non è supportata.
* Se l'operazione di esportazione hello dal Database SQL di Azure è superiore a 20 ore, potrebbero essere annullato. prestazioni tooincrease durante l'esportazione, è possibile:
  * Aumentare temporaneamente il livello di servizio.
  * Cessare tutte lettura e scrittura di attività durante l'esportazione di hello.
  * Utilizzare un [indice cluster](https://msdn.microsoft.com/library/ms190457.aspx) con valori non null in tutte le tabelle di grandi dimensioni. Senza indici cluster, l'esportazione potrebbe non riuscire se dovesse durare più di 6 - 12 ore. Questo avviene perché il servizio di esportazione hello necessita di una tabella intera tabella analisi tootry tooexport toocomplete. Un toodetermine efficace se le tabelle sono ottimizzate per l'esportazione è toorun **DBCC SHOW_STATISTICS** e assicurarsi che tale hello *RANGE_HI_KEY* non è null e il relativo valore ha una distribuzione ottima. Per i dettagli, vedere [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/ms174384.aspx).

> [!NOTE]
> File Bacpac non sono previsti toobe utilizzato per le operazioni di backup e ripristino. Il database SQL di Azure crea automaticamente i backup per ogni database dell'utente. Per altre informazioni, vedere [Panoramica sulla continuità aziendale](sql-database-business-continuity.md) e [Backup del database SQL](sql-database-automated-backups.md).  
> 

## <a name="export-tooa-bacpac-file-using-hello-azure-portal"></a>Esportare file BACPAC tooa utilizzando hello portale di Azure

un database utilizzando tooexport hello [portale di Azure](https://portal.azure.com), aprire la pagina hello per il database e fare clic su **esportare** sulla barra degli strumenti hello. Specificare nome del file BACPAC hello, fornire hello account di archiviazione di Azure e il contenitore per l'esportazione di hello e fornire i database di origine toohello tooconnect credenziali hello.  

![Esportazione di un database](./media/sql-database-export/database-export.png)

lo stato di hello toomonitor di hello operazione di esportazione, aprire la pagina hello per hello server logico contenente hello il database da esportare. Scorrere verso il basso troppo**operazioni** e quindi fare clic su **importazione/esportazione** cronologia.

![Cronologia delle esportazioni](./media/sql-database-export/export-history.png)
![Stato nella cronologia delle esportazioni](./media/sql-database-export/export-history2.png)

## <a name="export-tooa-bacpac-file-using-hello-sqlpackage-utility"></a>Esportare file BACPAC tooa utilità SQLPackage hello

tooexport un SQL database utilizzando hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) utilità della riga di comando, vedere [esportare parametri e proprietà](https://msdn.microsoft.com/library/hh550080.aspx#Export Parameters and Properties). SQLPackage utilità Hello viene fornito con le versioni più recenti di hello [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) e [SQL Server Data Tools per Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), oppure è possibile scaricare una versione più recente di hello di [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) direttamente da hello Microsoft download center.

È consigliabile utilizzare hello di hello SQLPackage utilità per la scalabilità e prestazioni nella maggior parte degli ambienti di produzione. Per un Team di consulenza clienti di SQL Server tramite file BACPAC, vedere i blog sulla migrazione [la migrazione da SQL Server tooAzure Database SQL tramite file BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

Questo esempio viene illustrato come tooexport un database tramite SqlPackage.exe con autenticazione universale di Active Directory:

```cmd
SqlPackage.exe /a:Export /tf:testExport.bacpac /scs:"Data Source=apptestserver.database.windows.net;Initial Catalog=MyDB;" /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="export-tooa-bacpac-file-using-sql-server-management-studio-ssms"></a>Esportare file BACPAC tooa utilizzando SQL Server Management Studio (SSMS)

versioni più recenti di Hello di SQL Server Management Studio forniscono anche un tooexport guidata un file BACPAC tooa di Database SQL di Azure. Vedere hello [esportare un'applicazione livello dati](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application).

## <a name="export-tooa-bacpac-file-using-powershell"></a>Esportare file BACPAC tooa tramite PowerShell

Hello utilizzare [New AzureRmSqlDatabaseExport](/powershell/module/azurerm.sql/new-azurermsqldatabaseexport) cmdlet toosubmit un toohello richiesta di esportazione del database del servizio di Database SQL di Azure. A seconda delle dimensioni di hello del database, l'operazione di esportazione hello potrebbe richiedere alcuni toocomplete ora.

 ```powershell
 $exportRequest = New-AzureRmSqlDatabaseExport -ResourceGroupName $ResourceGroupName -ServerName $ServerName `
   -DatabaseName $DatabaseName -StorageKeytype $StorageKeytype -StorageKey $StorageKey -StorageUri $BacpacUri `
   -AdministratorLogin $creds.UserName -AdministratorLoginPassword $creds.Password
 ```

stato di hello toocheck di hello richiesta di esportazione, utilizzare hello [Get AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet. L'esecuzione di questo hello subito dopo la richiesta in genere restituisce **stato: InProgress**. Quando viene visualizzato **stato: ha avuto esito positivo** esportazione hello è stata completata.

```powershell
$exportStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $exportRequest.OperationStatusLink
[Console]::Write("Exporting")
while ($exportStatus.Status -eq "InProgress")
{
    $exportStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $exportRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$exportStatus
```

## <a name="next-steps"></a>Passaggi successivi

* toolearn sulla conservazione dei backup a lungo termine di un backup di database SQL di Azure come un tooexported alternativo di un database per scopi di archiviazione, vedere [conservazione dei backup a lungo termine](sql-database-long-term-retention.md).
- Per un Team di consulenza clienti di SQL Server tramite file BACPAC, vedere i blog sulla migrazione [la migrazione da SQL Server tooAzure Database SQL tramite file BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* toolearn sull'importazione di un database di SQL Server tooa BACPAC, vedere [Importa un database di SQL Server tooa BACPCAC](https://msdn.microsoft.com/library/hh710052.aspx).
* toolearn sull'esportazione di un file BACPAC da un database di SQL Server, vedere [esportare un'applicazione livello dati](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) e [eseguire la migrazione di un database](sql-database-migrate-your-sql-server-database.md).
* Se si sta esportando da SQL Server come un tooAzure toomigration preludio Database SQL, vedere [eseguire la migrazione di un tooAzure di database di SQL Server Database SQL](sql-database-cloud-migrate.md).
