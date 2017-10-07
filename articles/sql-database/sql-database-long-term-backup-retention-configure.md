---
title: Configurare la conservazione dei backup a lungo termine - Database SQL di Azure | Microsoft Docs
description: Informazioni su come toostore automatizzare i backup nell'insieme di credenziali di servizi di ripristino di Azure hello e toorestore da hello insieme di credenziali di servizi di ripristino di Azure
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: carlrab
ms.openlocfilehash: 603f4dd21cee4407d46f749655aba8f9ef3322c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a>Configurare e ripristinare dalla conservazione dei backup a lungo termine del database SQL di Azure

È possibile configurare i backup del database SQL di Azure dell'insieme di credenziali toostore hello servizi di ripristino di Azure e quindi ripristina un database tramite backup conservato con insieme di credenziali hello hello portale di Azure o PowerShell.

## <a name="azure-portal"></a>Portale di Azure

Hello seguente mostra le sezioni è come hello tooconfigure portale di Azure tramite hello toouse servizi di ripristino di Azure dell'insieme di credenziali, visualizzare i backup nell'insieme di credenziali hello e ripristinare dall'insieme di credenziali hello.

### <a name="configure-hello-vault-register-hello-server-and-select-databases"></a>Configurare hello insieme di credenziali, registrare il server di hello e selezionare i database

Si [configurare un backup di servizi di ripristino di Azure dell'insieme di credenziali tooretain automatizzata](sql-database-long-term-retention.md) per un periodo più lungo hello periodo di memorizzazione per il livello di servizio. 

1. Aprire hello **SQL Server** pagina per il server.

   ![pagina sql server](./media/sql-database-get-started-portal/sql-server-blade.png)

2. Fare clic su **Conservazione backup a lungo termine**.

   ![collegamento conservazione backup a lungo termine](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. In hello **conservazione dei backup a lungo termine** pagina per il server, leggere e accettare le condizioni di anteprima di hello (a meno che non si è ancora stato fatto - o questa funzionalità non è più in anteprima).

   ![accettare i termini di anteprima hello](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. tooconfigure memorizzazione del backup a lungo termine, selezionare tale database nella griglia di hello e quindi fare clic su **configura** sulla barra degli strumenti hello.

   ![selezione del database per la conservazione backup a lungo termine](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. In hello **configura** pagina, fare clic su **Configura le impostazioni obbligatorie** in **insieme di credenziali servizio Recovery**.

   ![collegamento configurazione dell'insieme di credenziali](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. In hello **insieme di credenziali di Recovery services** pagina, selezionare un insieme di credenziali esistente, se presente. In caso contrario, se nessun recupero servizi insieme di credenziali trovato per la sottoscrizione, fare clic tooexit hello flusso e creare un insieme di credenziali di servizi di ripristino.

   ![collegamento crea insieme di credenziali](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. In hello **insiemi di credenziali di servizi di ripristino** pagina, fare clic su **Aggiungi**.

   ![collegamento aggiungi insieme di credenziali](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. In hello **insieme di credenziali di servizi di ripristino** pagina, fornire un nome valido per l'insieme di credenziali di servizi di ripristino hello.

   ![nome nuovo insieme di credenziali](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. Selezionare la sottoscrizione e il gruppo di risorse e quindi selezionare il percorso di hello per insieme di credenziali hello. Al termine, fare clic su **Crea**.

   ![crea insieme di credenziali](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > insieme di credenziali Hello deve trovarsi nella stessa area server logico SQL Azure di hello hello e deve utilizzare hello stesso gruppo di risorse server logico hello.
   >

10. Dopo la creazione di nuovo insieme di credenziali hello eseguire hello necessarie tooreturn toohello **insieme di credenziali di Recovery services** pagina.

11. In hello **insieme di credenziali di Recovery services** pagina, fare clic su insieme di credenziali hello e quindi fare clic su **selezionare**.

   ![selezione insieme di credenziali esistente](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. In hello **configura** pagina, fornire un nome valido per il nuovo criterio di conservazione hello, modificare i criteri di conservazione predefiniti hello come appropriato e quindi fare clic su **OK**.

   ![definizione dei criteri di conservazione](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. In hello **conservazione dei backup a lungo termine** pagina per il database, fare clic su **salvare** e quindi fare clic su **OK** tooapply hello a lungo termine tooall di criteri di conservazione dei backup selezionato database.

   ![definizione dei criteri di conservazione](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. Fare clic su **salvare** tooenable conservazione backup a lungo termine con questo nuovo criterio toohello servizi di ripristino di Azure insieme di credenziali configurato.

   ![definizione dei criteri di conservazione](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> Una volta configurato, i backup visualizzati nell'insieme di credenziali hello entro sette giorni successivi. Per proseguire questa esercitazione backup visualizzati nell'insieme di credenziali hello.
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a>Visualizzare i backup nella conservazione a lungo termine con il portale di Azure

Visualizzare informazioni sui backup del database nella [conservazione backup a lungo termine](sql-database-long-term-retention.md). 

1. In hello portale di Azure, aprire l'insieme di credenziali di servizi di ripristino di Azure per i backup dei database (andare troppo**tutte le risorse** e selezionarlo dall'elenco di hello delle risorse per la sottoscrizione) quantità hello tooview di archiviazione utilizzato dal database backup nell'insieme di credenziali hello.

   ![visualizzazione dell'insieme di credenziali dei servizi di ripristino con i backup](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. Aprire hello **database SQL** pagina per il database.

   ![nuova pagina del database di esempio](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. Sulla barra degli strumenti hello, fare clic su **ripristinare**.

   ![barra degli strumenti di ripristino](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. Nella pagina di ripristino hello, fare clic su **a lungo termine**.

5. In backup di Azure dell'insieme di credenziali, fare clic su **selezionare un backup** tooview i backup di database disponibili hello in conservazione dei backup a lungo termine.

   ![backup nell'insieme di credenziali](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-hello-azure-portal"></a>Ripristinare un database da un backup di conservazione del backup a lungo termine tramite hello portale di Azure

Ripristinare hello tooa nuovo il database da un backup in hello che insieme di credenziali di servizi di ripristino di Azure.

1. In hello **i backup di Azure dell'insieme di credenziali** pagina, fare clic su toorestore backup hello e quindi fare clic su **selezionare**.

   ![selezione del backup dell'insieme di credenziali](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. In hello **nome del Database** testo specificare hello nome per il database ripristinato hello.

   ![nuovo nome database](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. Fare clic su **OK** toorestore del database dal backup hello in database nuovi toohello di hello insieme di credenziali.

4. Sulla barra degli strumenti hello, fare clic sullo stato hello notifica icona tooview hello hello del processo di ripristino.

   ![avanzamento del processo di ripristino dall'insieme di credenziali](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. Quando viene completato il processo di ripristino di hello, aprire hello **database SQL** database appena ripristinato hello tooview di pagina.

   ![database ripristinato dall'insieme di credenziali](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> Da qui è possibile connettersi a database toohello ripristinato tramite attività di SQL Server Management Studio tooperform necessita, ad esempio troppo[estrarre un bit di dati da toocopy database hello ripristinato nel database esistente di hello o toodelete hello esistente nome del database del database e ridenominazione hello ripristinata database toohello esistente](sql-database-recovery-using-backups.md#point-in-time-restore).
>

## <a name="powershell"></a>PowerShell

Hello le sezioni seguenti Mostra come toouse PowerShell tooconfigure hello servizi di ripristino di Azure dell'insieme di credenziali, visualizzare i backup nell'insieme di credenziali hello e ripristinare dall'insieme di credenziali hello.

### <a name="create-a-recovery-services-vault"></a>Creare un insieme di credenziali di Servizi di ripristino

Hello utilizzare [New AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate ripristino di un insieme di credenziali dei servizi.

> [!IMPORTANT]
> insieme di credenziali Hello deve trovarsi nella stessa area server logico SQL Azure di hello hello e deve utilizzare hello stesso gruppo di risorse server logico hello.

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-toouse-hello-recovery-vault-for-its-long-term-retention-backups"></a>Impostare le credenziali di ripristino server hello toouse per i backup di conservazione a lungo termine

Hello utilizzare [Set AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) tooassociate cmdlet creato in precedenza con un server SQL di Azure specifico insieme di credenziali di servizi di ripristino.

```PowerShell
# Set your server toouse hello vault toofor long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a>Creare un criterio di conservazione

Criteri di conservazione sono dove impostare tookeep quanto tempo un backup del database. Hello utilizzare [Get AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet tooget hello predefinito memorizzazione criteri toouse come modello hello per la creazione di criteri. In questo modello, il periodo di memorizzazione hello è impostato su 2 anni. Successivamente, eseguire hello [New AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally creare criteri di hello. 

> [!NOTE]
> Alcuni cmdlet richiedono l'impostazione di contesto dell'insieme di credenziali hello prima dell'esecuzione ([Set AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) in modo che questo cmdlet in alcuni frammenti di codice correlate. Impostare il contesto di hello perché hello criteri fanno parte dell'insieme di credenziali hello. È possibile creare più criteri di conservazione per ogni insieme di credenziali e quindi applicare i database di toospecific criteri hello desiderato. 


```PowerShell
# Retrieve hello default retention policy for hello AzureSQLDatabase workload type
$retentionPolicy = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType AzureSQLDatabase

# Set hello retention value tootwo years (you can set tooany time between 1 week and 10 years)
$retentionPolicy.RetentionDurationType = "Years"
$retentionPolicy.RetentionCount = 2
$retentionPolicyName = "my2YearRetentionPolicy"

# Set hello vault context toohello vault you are creating hello policy for
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# Create hello new policy
$policy = New-AzureRmRecoveryServicesBackupProtectionPolicy -name $retentionPolicyName -WorkloadType AzureSQLDatabase -retentionPolicy $retentionPolicy
$policy
```

### <a name="configure-a-database-toouse-hello-previously-defined-retention-policy"></a>Configurare un criterio di conservazione database toouse hello definito in precedenza

Hello utilizzare [Set AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet tooapply hello nuovi criteri tooa database specifico.

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a>Visualizzare le informazioni sui backup e i backup nella conservazione a lungo termine

Visualizzare informazioni sui backup del database nella [conservazione backup a lungo termine](sql-database-long-term-retention.md). 

Utilizzare le seguenti informazioni di backup tooview cmdlet hello:

- [Get-AzureRmRecoveryServicesBackupContainer](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [Get-AzureRmRecoveryServicesBackupItem](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [Get-AzureRmRecoveryServicesBackupRecoveryPoint](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

```PowerShell
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$databaseNeedingRestore = $databaseName

# Set hello vault context toohello vault we want toorestore from
#$vault = Get-AzureRmRecoveryServicesVault -ResourceGroupName $resourceGroupName
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# hello following commands find hello container associated with hello server 'myserver' under resource group 'myresourcegroup'
$container = Get-AzureRmRecoveryServicesBackupContainer -ContainerType AzureSQL -FriendlyName $vault.Name

# Get hello long-term retention metadata associated with a specific database
$item = Get-AzureRmRecoveryServicesBackupItem -Container $container -WorkloadType AzureSQLDatabase -Name $databaseNeedingRestore

# Get all available backups for hello previously indicated database
# Optionally, set hello -StartDate and -EndDate parameters tooreturn backups within a specific time period
$availableBackups = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $item
$availableBackups
```

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a>Ripristinare un database da un backup nella conservazione dei backup a lungo termine

Ripristino di conservazione dei backup a lungo termine utilizza hello [ripristino AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.

```PowerShell
# Restore hello most recent backup: $availableBackups[0]
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$restoredDatabaseName = "{new-database-name}"
$edition = "Basic"
$performanceLevel = "Basic"

$restoredDb = Restore-AzureRmSqlDatabase -FromLongTermRetentionBackup -ResourceId $availableBackups[0].Id -ResourceGroupName $resourceGroupName `
 -ServerName $serverName -TargetDatabaseName $restoredDatabaseName -Edition $edition -ServiceObjectiveName $performanceLevel
$restoredDb
```


> [!NOTE]
> Da qui è possibile connettersi a database toohello ripristinato tramite SQL Server Management Studio tooperform necessarie operazioni, ad esempio tooextract un bit di dati da hello ripristinate toocopy database nel database esistente di hello o database esistente di toodelete hello e ridenominazione Hello database ripristinato toohello nome del database esistente. Vedere [ripristino temporizzato](sql-database-recovery-using-backups.md#point-in-time-restore).

## <a name="next-steps"></a>Passaggi successivi

- toolearn sul servizio generato i backup automatici, vedere [backup automatici](sql-database-automated-backups.md)
- toolearn sulla conservazione dei backup a lungo termine, vedere [conservazione dei backup a lungo termine](sql-database-long-term-retention.md)
- toolearn sul ripristino da backup, vedere [ripristinare dal backup](sql-database-recovery-using-backups.md)
