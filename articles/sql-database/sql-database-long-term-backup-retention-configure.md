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
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a><span data-ttu-id="e087f-103">Configurare e ripristinare dalla conservazione dei backup a lungo termine del database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="e087f-103">Configure and restore from Azure SQL Database long-term backup retention</span></span>

<span data-ttu-id="e087f-104">È possibile configurare i backup del database SQL di Azure dell'insieme di credenziali toostore hello servizi di ripristino di Azure e quindi ripristina un database tramite backup conservato con insieme di credenziali hello hello portale di Azure o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e087f-104">You can configure hello Azure Recovery Services vault toostore Azure SQL database backups and then recover a database using backups retained in hello vault using hello Azure portal or PowerShell.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="e087f-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e087f-105">Azure portal</span></span>

<span data-ttu-id="e087f-106">Hello seguente mostra le sezioni è come hello tooconfigure portale di Azure tramite hello toouse servizi di ripristino di Azure dell'insieme di credenziali, visualizzare i backup nell'insieme di credenziali hello e ripristinare dall'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="e087f-106">hello following sections show you how toouse hello Azure portal tooconfigure hello Azure Recovery Services vault, view backups in hello vault, and restore from hello vault.</span></span>

### <a name="configure-hello-vault-register-hello-server-and-select-databases"></a><span data-ttu-id="e087f-107">Configurare hello insieme di credenziali, registrare il server di hello e selezionare i database</span><span class="sxs-lookup"><span data-stu-id="e087f-107">Configure hello vault, register hello server, and select databases</span></span>

<span data-ttu-id="e087f-108">Si [configurare un backup di servizi di ripristino di Azure dell'insieme di credenziali tooretain automatizzata](sql-database-long-term-retention.md) per un periodo più lungo hello periodo di memorizzazione per il livello di servizio.</span><span class="sxs-lookup"><span data-stu-id="e087f-108">You [configure an Azure Recovery Services vault tooretain automated backups](sql-database-long-term-retention.md) for a period longer than hello retention period for your service tier.</span></span> 

1. <span data-ttu-id="e087f-109">Aprire hello **SQL Server** pagina per il server.</span><span class="sxs-lookup"><span data-stu-id="e087f-109">Open hello **SQL Server** page for your server.</span></span>

   ![pagina sql server](./media/sql-database-get-started-portal/sql-server-blade.png)

2. <span data-ttu-id="e087f-111">Fare clic su **Conservazione backup a lungo termine**.</span><span class="sxs-lookup"><span data-stu-id="e087f-111">Click **Long-term backup retention**.</span></span>

   ![collegamento conservazione backup a lungo termine](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. <span data-ttu-id="e087f-113">In hello **conservazione dei backup a lungo termine** pagina per il server, leggere e accettare le condizioni di anteprima di hello (a meno che non si è ancora stato fatto - o questa funzionalità non è più in anteprima).</span><span class="sxs-lookup"><span data-stu-id="e087f-113">On hello **Long-term backup retention** page for your server, review and accept hello preview terms (unless you have already done so - or this feature is no longer in preview).</span></span>

   ![accettare i termini di anteprima hello](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. <span data-ttu-id="e087f-115">tooconfigure memorizzazione del backup a lungo termine, selezionare tale database nella griglia di hello e quindi fare clic su **configura** sulla barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="e087f-115">tooconfigure long-term backup retention, select that database in hello grid and then click **Configure** on hello toolbar.</span></span>

   ![selezione del database per la conservazione backup a lungo termine](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. <span data-ttu-id="e087f-117">In hello **configura** pagina, fare clic su **Configura le impostazioni obbligatorie** in **insieme di credenziali servizio Recovery**.</span><span class="sxs-lookup"><span data-stu-id="e087f-117">On hello **Configure** page, click **Configure required settings** under **Recovery service vault**.</span></span>

   ![collegamento configurazione dell'insieme di credenziali](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. <span data-ttu-id="e087f-119">In hello **insieme di credenziali di Recovery services** pagina, selezionare un insieme di credenziali esistente, se presente.</span><span class="sxs-lookup"><span data-stu-id="e087f-119">On hello **Recovery services vault** page, select an existing vault, if any.</span></span> <span data-ttu-id="e087f-120">In caso contrario, se nessun recupero servizi insieme di credenziali trovato per la sottoscrizione, fare clic tooexit hello flusso e creare un insieme di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e087f-120">Otherwise, if no recovery services vault found for your subscription, click tooexit hello flow and create a recovery services vault.</span></span>

   ![collegamento crea insieme di credenziali](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. <span data-ttu-id="e087f-122">In hello **insiemi di credenziali di servizi di ripristino** pagina, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e087f-122">On hello **Recovery Services vaults** page, click **Add**.</span></span>

   ![collegamento aggiungi insieme di credenziali](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. <span data-ttu-id="e087f-124">In hello **insieme di credenziali di servizi di ripristino** pagina, fornire un nome valido per l'insieme di credenziali di servizi di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="e087f-124">On hello **Recovery Services vault** page, provide a valid name for hello Recovery Services vault.</span></span>

   ![nome nuovo insieme di credenziali](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. <span data-ttu-id="e087f-126">Selezionare la sottoscrizione e il gruppo di risorse e quindi selezionare il percorso di hello per insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="e087f-126">Select your subscription and resource group, and then select hello location for hello vault.</span></span> <span data-ttu-id="e087f-127">Al termine, fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e087f-127">When done, click **Create**.</span></span>

   ![crea insieme di credenziali](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > <span data-ttu-id="e087f-129">insieme di credenziali Hello deve trovarsi nella stessa area server logico SQL Azure di hello hello e deve utilizzare hello stesso gruppo di risorse server logico hello.</span><span class="sxs-lookup"><span data-stu-id="e087f-129">hello vault must be located in hello same region as hello Azure SQL logical server, and must use hello same resource group as hello logical server.</span></span>
   >

10. <span data-ttu-id="e087f-130">Dopo la creazione di nuovo insieme di credenziali hello eseguire hello necessarie tooreturn toohello **insieme di credenziali di Recovery services** pagina.</span><span class="sxs-lookup"><span data-stu-id="e087f-130">After hello new vault is created, execute hello necessary steps tooreturn toohello **Recovery services vault** page.</span></span>

11. <span data-ttu-id="e087f-131">In hello **insieme di credenziali di Recovery services** pagina, fare clic su insieme di credenziali hello e quindi fare clic su **selezionare**.</span><span class="sxs-lookup"><span data-stu-id="e087f-131">On hello **Recovery services vault** page, click hello vault and then click **Select**.</span></span>

   ![selezione insieme di credenziali esistente](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. <span data-ttu-id="e087f-133">In hello **configura** pagina, fornire un nome valido per il nuovo criterio di conservazione hello, modificare i criteri di conservazione predefiniti hello come appropriato e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e087f-133">On hello **Configure** page, provide a valid name for hello new retention policy, modify hello default retention policy as appropriate, and then click **OK**.</span></span>

   ![definizione dei criteri di conservazione](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. <span data-ttu-id="e087f-135">In hello **conservazione dei backup a lungo termine** pagina per il database, fare clic su **salvare** e quindi fare clic su **OK** tooapply hello a lungo termine tooall di criteri di conservazione dei backup selezionato database.</span><span class="sxs-lookup"><span data-stu-id="e087f-135">On hello **Long-term backup retention** page for your database, click **Save** and then click **OK** tooapply hello long-term backup retention policy tooall selected databases.</span></span>

   ![definizione dei criteri di conservazione](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. <span data-ttu-id="e087f-137">Fare clic su **salvare** tooenable conservazione backup a lungo termine con questo nuovo criterio toohello servizi di ripristino di Azure insieme di credenziali configurato.</span><span class="sxs-lookup"><span data-stu-id="e087f-137">Click **Save** tooenable long-term backup retention using this new policy toohello Azure Recovery Services vault that you configured.</span></span>

   ![definizione dei criteri di conservazione](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> <span data-ttu-id="e087f-139">Una volta configurato, i backup visualizzati nell'insieme di credenziali hello entro sette giorni successivi.</span><span class="sxs-lookup"><span data-stu-id="e087f-139">Once configured, backups show up in hello vault within next seven days.</span></span> <span data-ttu-id="e087f-140">Per proseguire questa esercitazione backup visualizzati nell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="e087f-140">Do not continue this tutorial until backups show up in hello vault.</span></span>
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a><span data-ttu-id="e087f-141">Visualizzare i backup nella conservazione a lungo termine con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e087f-141">View backups in long-term retention using Azure portal</span></span>

<span data-ttu-id="e087f-142">Visualizzare informazioni sui backup del database nella [conservazione backup a lungo termine](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="e087f-142">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

1. <span data-ttu-id="e087f-143">In hello portale di Azure, aprire l'insieme di credenziali di servizi di ripristino di Azure per i backup dei database (andare troppo**tutte le risorse** e selezionarlo dall'elenco di hello delle risorse per la sottoscrizione) quantità hello tooview di archiviazione utilizzato dal database backup nell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="e087f-143">In hello Azure portal, open your Azure Recovery Services vault for your database backups (go too**All resources** and select it from hello list of resources for your subscription) tooview hello amount of storage used by your database backups in hello vault.</span></span>

   ![visualizzazione dell'insieme di credenziali dei servizi di ripristino con i backup](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. <span data-ttu-id="e087f-145">Aprire hello **database SQL** pagina per il database.</span><span class="sxs-lookup"><span data-stu-id="e087f-145">Open hello **SQL database** page for your database.</span></span>

   ![nuova pagina del database di esempio](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. <span data-ttu-id="e087f-147">Sulla barra degli strumenti hello, fare clic su **ripristinare**.</span><span class="sxs-lookup"><span data-stu-id="e087f-147">On hello toolbar, click **Restore**.</span></span>

   ![barra degli strumenti di ripristino](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. <span data-ttu-id="e087f-149">Nella pagina di ripristino hello, fare clic su **a lungo termine**.</span><span class="sxs-lookup"><span data-stu-id="e087f-149">On hello Restore page, click **Long-term**.</span></span>

5. <span data-ttu-id="e087f-150">In backup di Azure dell'insieme di credenziali, fare clic su **selezionare un backup** tooview i backup di database disponibili hello in conservazione dei backup a lungo termine.</span><span class="sxs-lookup"><span data-stu-id="e087f-150">Under Azure vault backups, click **Select a backup** tooview hello available database backups in long-term backup retention.</span></span>

   ![backup nell'insieme di credenziali](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-hello-azure-portal"></a><span data-ttu-id="e087f-152">Ripristinare un database da un backup di conservazione del backup a lungo termine tramite hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e087f-152">Restore a database from a backup in long-term backup retention using hello Azure portal</span></span>

<span data-ttu-id="e087f-153">Ripristinare hello tooa nuovo il database da un backup in hello che insieme di credenziali di servizi di ripristino di Azure.</span><span class="sxs-lookup"><span data-stu-id="e087f-153">You restore hello database tooa new database from a backup in hello Azure Recovery Services vault.</span></span>

1. <span data-ttu-id="e087f-154">In hello **i backup di Azure dell'insieme di credenziali** pagina, fare clic su toorestore backup hello e quindi fare clic su **selezionare**.</span><span class="sxs-lookup"><span data-stu-id="e087f-154">On hello **Azure vault backups** page, click hello backup toorestore and then click **Select**.</span></span>

   ![selezione del backup dell'insieme di credenziali](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. <span data-ttu-id="e087f-156">In hello **nome del Database** testo specificare hello nome per il database ripristinato hello.</span><span class="sxs-lookup"><span data-stu-id="e087f-156">In hello **Database name** text box, provide hello name for hello restored database.</span></span>

   ![nuovo nome database](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. <span data-ttu-id="e087f-158">Fare clic su **OK** toorestore del database dal backup hello in database nuovi toohello di hello insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="e087f-158">Click **OK** toorestore your database from hello backup in hello vault toohello new database.</span></span>

4. <span data-ttu-id="e087f-159">Sulla barra degli strumenti hello, fare clic sullo stato hello notifica icona tooview hello hello del processo di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e087f-159">On hello toolbar, click hello notification icon tooview hello status of hello restore job.</span></span>

   ![avanzamento del processo di ripristino dall'insieme di credenziali](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. <span data-ttu-id="e087f-161">Quando viene completato il processo di ripristino di hello, aprire hello **database SQL** database appena ripristinato hello tooview di pagina.</span><span class="sxs-lookup"><span data-stu-id="e087f-161">When hello restore job is completed, open hello **SQL databases** page tooview hello newly restored database.</span></span>

   ![database ripristinato dall'insieme di credenziali](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> <span data-ttu-id="e087f-163">Da qui è possibile connettersi a database toohello ripristinato tramite attività di SQL Server Management Studio tooperform necessita, ad esempio troppo[estrarre un bit di dati da toocopy database hello ripristinato nel database esistente di hello o toodelete hello esistente nome del database del database e ridenominazione hello ripristinata database toohello esistente](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="e087f-163">From here, you can connect toohello restored database using SQL Server Management Studio tooperform needed tasks, such as too[extract a bit of data from hello restored database toocopy into hello existing database or toodelete hello existing database and rename hello restored database toohello existing database name](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>
>

## <a name="powershell"></a><span data-ttu-id="e087f-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e087f-164">PowerShell</span></span>

<span data-ttu-id="e087f-165">Hello le sezioni seguenti Mostra come toouse PowerShell tooconfigure hello servizi di ripristino di Azure dell'insieme di credenziali, visualizzare i backup nell'insieme di credenziali hello e ripristinare dall'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="e087f-165">hello following sections show you how toouse PowerShell tooconfigure hello Azure Recovery Services vault, view backups in hello vault, and restore from hello vault.</span></span>

### <a name="create-a-recovery-services-vault"></a><span data-ttu-id="e087f-166">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="e087f-166">Create a recovery services vault</span></span>

<span data-ttu-id="e087f-167">Hello utilizzare [New AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate ripristino di un insieme di credenziali dei servizi.</span><span class="sxs-lookup"><span data-stu-id="e087f-167">Use hello [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate a recovery services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e087f-168">insieme di credenziali Hello deve trovarsi nella stessa area server logico SQL Azure di hello hello e deve utilizzare hello stesso gruppo di risorse server logico hello.</span><span class="sxs-lookup"><span data-stu-id="e087f-168">hello vault must be located in hello same region as hello Azure SQL logical server, and must use hello same resource group as hello logical server.</span></span>

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-toouse-hello-recovery-vault-for-its-long-term-retention-backups"></a><span data-ttu-id="e087f-169">Impostare le credenziali di ripristino server hello toouse per i backup di conservazione a lungo termine</span><span class="sxs-lookup"><span data-stu-id="e087f-169">Set your server toouse hello recovery vault for its long-term retention backups</span></span>

<span data-ttu-id="e087f-170">Hello utilizzare [Set AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) tooassociate cmdlet creato in precedenza con un server SQL di Azure specifico insieme di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e087f-170">Use hello [Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet tooassociate a previously created recovery services vault with a specific Azure SQL server.</span></span>

```PowerShell
# Set your server toouse hello vault toofor long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a><span data-ttu-id="e087f-171">Creare un criterio di conservazione</span><span class="sxs-lookup"><span data-stu-id="e087f-171">Create a retention policy</span></span>

<span data-ttu-id="e087f-172">Criteri di conservazione sono dove impostare tookeep quanto tempo un backup del database.</span><span class="sxs-lookup"><span data-stu-id="e087f-172">A retention policy is where you set how long tookeep a database backup.</span></span> <span data-ttu-id="e087f-173">Hello utilizzare [Get AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet tooget hello predefinito memorizzazione criteri toouse come modello hello per la creazione di criteri.</span><span class="sxs-lookup"><span data-stu-id="e087f-173">Use hello [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet tooget hello default retention policy toouse as hello template for creating policies.</span></span> <span data-ttu-id="e087f-174">In questo modello, il periodo di memorizzazione hello è impostato su 2 anni.</span><span class="sxs-lookup"><span data-stu-id="e087f-174">In this template, hello retention period is set for 2 years.</span></span> <span data-ttu-id="e087f-175">Successivamente, eseguire hello [New AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally creare criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="e087f-175">Next, run hello [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally create hello policy.</span></span> 

> [!NOTE]
> <span data-ttu-id="e087f-176">Alcuni cmdlet richiedono l'impostazione di contesto dell'insieme di credenziali hello prima dell'esecuzione ([Set AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) in modo che questo cmdlet in alcuni frammenti di codice correlate.</span><span class="sxs-lookup"><span data-stu-id="e087f-176">Some cmdlets require that you set hello vault context before running ([Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) so you see this cmdlet in a few related snippets.</span></span> <span data-ttu-id="e087f-177">Impostare il contesto di hello perché hello criteri fanno parte dell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="e087f-177">You set hello context because hello policy is part of hello vault.</span></span> <span data-ttu-id="e087f-178">È possibile creare più criteri di conservazione per ogni insieme di credenziali e quindi applicare i database di toospecific criteri hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="e087f-178">You can create multiple retention policies for each vault and then apply hello desired policy toospecific databases.</span></span> 


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

### <a name="configure-a-database-toouse-hello-previously-defined-retention-policy"></a><span data-ttu-id="e087f-179">Configurare un criterio di conservazione database toouse hello definito in precedenza</span><span class="sxs-lookup"><span data-stu-id="e087f-179">Configure a database toouse hello previously defined retention policy</span></span>

<span data-ttu-id="e087f-180">Hello utilizzare [Set AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet tooapply hello nuovi criteri tooa database specifico.</span><span class="sxs-lookup"><span data-stu-id="e087f-180">Use hello [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet tooapply hello new policy tooa specific database.</span></span>

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a><span data-ttu-id="e087f-181">Visualizzare le informazioni sui backup e i backup nella conservazione a lungo termine</span><span class="sxs-lookup"><span data-stu-id="e087f-181">View backup info, and backups in long-term retention</span></span>

<span data-ttu-id="e087f-182">Visualizzare informazioni sui backup del database nella [conservazione backup a lungo termine](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="e087f-182">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

<span data-ttu-id="e087f-183">Utilizzare le seguenti informazioni di backup tooview cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="e087f-183">Use hello following cmdlets tooview backup information:</span></span>

- [<span data-ttu-id="e087f-184">Get-AzureRmRecoveryServicesBackupContainer</span><span class="sxs-lookup"><span data-stu-id="e087f-184">Get-AzureRmRecoveryServicesBackupContainer</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [<span data-ttu-id="e087f-185">Get-AzureRmRecoveryServicesBackupItem</span><span class="sxs-lookup"><span data-stu-id="e087f-185">Get-AzureRmRecoveryServicesBackupItem</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [<span data-ttu-id="e087f-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="e087f-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

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

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a><span data-ttu-id="e087f-187">Ripristinare un database da un backup nella conservazione dei backup a lungo termine</span><span class="sxs-lookup"><span data-stu-id="e087f-187">Restore a database from a backup in long-term backup retention</span></span>

<span data-ttu-id="e087f-188">Ripristino di conservazione dei backup a lungo termine utilizza hello [ripristino AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e087f-188">Restoring from long-term backup retention uses hello [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.</span></span>

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
> <span data-ttu-id="e087f-189">Da qui è possibile connettersi a database toohello ripristinato tramite SQL Server Management Studio tooperform necessarie operazioni, ad esempio tooextract un bit di dati da hello ripristinate toocopy database nel database esistente di hello o database esistente di toodelete hello e ridenominazione Hello database ripristinato toohello nome del database esistente.</span><span class="sxs-lookup"><span data-stu-id="e087f-189">From here, you can connect toohello restored database using SQL Server Management Studio tooperform needed tasks, such as tooextract a bit of data from hello restored database toocopy into hello existing database or toodelete hello existing database and rename hello restored database toohello existing database name.</span></span> <span data-ttu-id="e087f-190">Vedere [ripristino temporizzato](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="e087f-190">See [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e087f-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e087f-191">Next steps</span></span>

- <span data-ttu-id="e087f-192">toolearn sul servizio generato i backup automatici, vedere [backup automatici](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="e087f-192">toolearn about service-generated automatic backups, see [automatic backups](sql-database-automated-backups.md)</span></span>
- <span data-ttu-id="e087f-193">toolearn sulla conservazione dei backup a lungo termine, vedere [conservazione dei backup a lungo termine](sql-database-long-term-retention.md)</span><span class="sxs-lookup"><span data-stu-id="e087f-193">toolearn about long-term backup retention, see [long-term backup retention](sql-database-long-term-retention.md)</span></span>
- <span data-ttu-id="e087f-194">toolearn sul ripristino da backup, vedere [ripristinare dal backup](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="e087f-194">toolearn about restoring from backups, see [restore from backup](sql-database-recovery-using-backups.md)</span></span>
