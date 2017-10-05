---
title: Configurare la conservazione dei backup a lungo termine - Database SQL di Azure | Microsoft Docs
description: Informazioni su come archiviare i backup automatici nell'insieme di credenziali di Servizi di ripristino di Azure e su come eseguire il ripristino dall'insieme di credenziali di Servizi di ripristino di Azure
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
ms.openlocfilehash: ed9f74a59f0ca512e2758c6db4c5c9075030f859
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a><span data-ttu-id="e2221-103">Configurare e ripristinare dalla conservazione dei backup a lungo termine del database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="e2221-103">Configure and restore from Azure SQL Database long-term backup retention</span></span>

<span data-ttu-id="e2221-104">È possibile configurare l'insieme di credenziali di Servizi di ripristino di Azure per archiviare i backup del database SQL di Azure e quindi ripristinare un database tramite backup conservati nell'insieme di credenziali usando il portale di Azure o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e2221-104">You can configure the Azure Recovery Services vault to store Azure SQL database backups and then recover a database using backups retained in the vault using the Azure portal or PowerShell.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="e2221-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e2221-105">Azure portal</span></span>

<span data-ttu-id="e2221-106">Nelle sezioni seguenti viene illustrato come usare il portale di Azure per configurare l'insieme di credenziali di Servizi di ripristino di Azure, visualizzare i backup nell'insieme di credenziali ed eseguire il ripristino dall'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="e2221-106">The following sections show you how to use the Azure portal to configure the Azure Recovery Services vault, view backups in the vault, and restore from the vault.</span></span>

### <a name="configure-the-vault-register-the-server-and-select-databases"></a><span data-ttu-id="e2221-107">Configurare l'insieme di credenziali, registrare il server e selezionare i database</span><span class="sxs-lookup"><span data-stu-id="e2221-107">Configure the vault, register the server, and select databases</span></span>

<span data-ttu-id="e2221-108">Si [configurerà un insieme di credenziali di Servizi di ripristino di Azure per conservare i backup automatici](sql-database-long-term-retention.md) per un periodo più lungo rispetto al periodo di conservazione associato al livello di servizio.</span><span class="sxs-lookup"><span data-stu-id="e2221-108">You [configure an Azure Recovery Services vault to retain automated backups](sql-database-long-term-retention.md) for a period longer than the retention period for your service tier.</span></span> 

1. <span data-ttu-id="e2221-109">Aprire la pagina **SQL Server** per il server in uso.</span><span class="sxs-lookup"><span data-stu-id="e2221-109">Open the **SQL Server** page for your server.</span></span>

   ![pagina sql server](./media/sql-database-get-started-portal/sql-server-blade.png)

2. <span data-ttu-id="e2221-111">Fare clic su **Conservazione backup a lungo termine**.</span><span class="sxs-lookup"><span data-stu-id="e2221-111">Click **Long-term backup retention**.</span></span>

   ![collegamento conservazione backup a lungo termine](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. <span data-ttu-id="e2221-113">Nella pagina **Conservazione backup a lungo termine** del server in uso leggere e accettare le condizioni preliminari (se non sono già state accettate o se questa funzionalità non è più in versione di anteprima).</span><span class="sxs-lookup"><span data-stu-id="e2221-113">On the **Long-term backup retention** page for your server, review and accept the preview terms (unless you have already done so - or this feature is no longer in preview).</span></span>

   ![accettare le condizioni preliminari](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. <span data-ttu-id="e2221-115">Per configurare la conservazione a lungo termine dei backup, selezionare il database nella griglia e quindi fare clic su **Configura** sulla barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="e2221-115">To configure long-term backup retention, select that database in the grid and then click **Configure** on the toolbar.</span></span>

   ![selezione del database per la conservazione backup a lungo termine](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. <span data-ttu-id="e2221-117">Nella pagina **Configura** fare clic su **Configurare le impostazioni necessarie** in **Insieme di credenziali di Servizi di ripristino**.</span><span class="sxs-lookup"><span data-stu-id="e2221-117">On the **Configure** page, click **Configure required settings** under **Recovery service vault**.</span></span>

   ![collegamento configurazione dell'insieme di credenziali](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. <span data-ttu-id="e2221-119">Nella pagina **Insieme di credenziali di Servizi di ripristino** selezionare un insieme di credenziali esistente, se disponibile.</span><span class="sxs-lookup"><span data-stu-id="e2221-119">On the **Recovery services vault** page, select an existing vault, if any.</span></span> <span data-ttu-id="e2221-120">In caso contrario, se per la propria sottoscrizione non è presente alcun insieme di credenziali dei servizi di ripristino, fare clic per chiudere il flusso e creare un insieme di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e2221-120">Otherwise, if no recovery services vault found for your subscription, click to exit the flow and create a recovery services vault.</span></span>

   ![collegamento crea insieme di credenziali](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. <span data-ttu-id="e2221-122">Nella pagina **Insiemi di credenziali dei servizi di ripristino** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e2221-122">On the **Recovery Services vaults** page, click **Add**.</span></span>

   ![collegamento aggiungi insieme di credenziali](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. <span data-ttu-id="e2221-124">Nella pagina **Insieme di credenziali di Servizi di ripristino** specificare un nome valido per l'insieme di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e2221-124">On the **Recovery Services vault** page, provide a valid name for the Recovery Services vault.</span></span>

   ![nome nuovo insieme di credenziali](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. <span data-ttu-id="e2221-126">Selezionare la propria sottoscrizione e il relativo gruppo di risorse e quindi specificare il percorso per l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="e2221-126">Select your subscription and resource group, and then select the location for the vault.</span></span> <span data-ttu-id="e2221-127">Al termine, fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e2221-127">When done, click **Create**.</span></span>

   ![crea insieme di credenziali](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > <span data-ttu-id="e2221-129">L'insieme di credenziali deve trovarsi nella stessa area del server logico di Azure SQL e deve usare lo stesso gruppo di risorse del server logico.</span><span class="sxs-lookup"><span data-stu-id="e2221-129">The vault must be located in the same region as the Azure SQL logical server, and must use the same resource group as the logical server.</span></span>
   >

10. <span data-ttu-id="e2221-130">Dopo aver creato il nuovo insieme di credenziali, eseguire i passaggi necessari per tornare alla pagina **Insieme di credenziali di Servizi di ripristino**.</span><span class="sxs-lookup"><span data-stu-id="e2221-130">After the new vault is created, execute the necessary steps to return to the **Recovery services vault** page.</span></span>

11. <span data-ttu-id="e2221-131">Nella pagina **Insieme di credenziali di Servizi di ripristino** fare clic sull'insieme di credenziali e quindi su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="e2221-131">On the **Recovery services vault** page, click the vault and then click **Select**.</span></span>

   ![selezione insieme di credenziali esistente](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. <span data-ttu-id="e2221-133">Nella pagina **Configura** specificare un nome valido per i nuovi criteri di conservazione, modificare i criteri di conservazione predefiniti in base alle esigenze e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e2221-133">On the **Configure** page, provide a valid name for the new retention policy, modify the default retention policy as appropriate, and then click **OK**.</span></span>

   ![definizione dei criteri di conservazione](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. <span data-ttu-id="e2221-135">Nella pagina **Conservazione backup a lungo termine** del database in uso fare clic su **Salva** e quindi su **OK** per applicare i criteri di conservazione dei backup a lungo termine a tutti i database selezionati.</span><span class="sxs-lookup"><span data-stu-id="e2221-135">On the **Long-term backup retention** page for your database, click **Save** and then click **OK** to apply the long-term backup retention policy to all selected databases.</span></span>

   ![definizione dei criteri di conservazione](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. <span data-ttu-id="e2221-137">Fare clic su **Salva** per abilitare la conservazione dei backup a lungo termine usando i nuovi criteri per l'insieme di credenziali di Servizi di ripristino di Azure appena configurato.</span><span class="sxs-lookup"><span data-stu-id="e2221-137">Click **Save** to enable long-term backup retention using this new policy to the Azure Recovery Services vault that you configured.</span></span>

   ![definizione dei criteri di conservazione](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> <span data-ttu-id="e2221-139">Dopo essere stati configurati, i backup verranno visualizzati nell'insieme di credenziali entro i successivi sette giorni.</span><span class="sxs-lookup"><span data-stu-id="e2221-139">Once configured, backups show up in the vault within next seven days.</span></span> <span data-ttu-id="e2221-140">Non continuare questa esercitazione finché i backup non verranno visualizzati nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="e2221-140">Do not continue this tutorial until backups show up in the vault.</span></span>
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a><span data-ttu-id="e2221-141">Visualizzare i backup nella conservazione a lungo termine con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e2221-141">View backups in long-term retention using Azure portal</span></span>

<span data-ttu-id="e2221-142">Visualizzare informazioni sui backup del database nella [conservazione backup a lungo termine](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="e2221-142">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

1. <span data-ttu-id="e2221-143">Nel portale di Azure aprire l'insieme di credenziali di Servizi di ripristino di Azure per i backup del database (andare a **Tutte le risorse** e selezionarlo dall'elenco delle risorse correlate alla sottoscrizione) per visualizzare la quantità di spazio di archiviazione usata dai backup del database nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="e2221-143">In the Azure portal, open your Azure Recovery Services vault for your database backups (go to **All resources** and select it from the list of resources for your subscription) to view the amount of storage used by your database backups in the vault.</span></span>

   ![visualizzazione dell'insieme di credenziali dei servizi di ripristino con i backup](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. <span data-ttu-id="e2221-145">Aprire la pagina **Database SQL** per il database.</span><span class="sxs-lookup"><span data-stu-id="e2221-145">Open the **SQL database** page for your database.</span></span>

   ![nuova pagina del database di esempio](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. <span data-ttu-id="e2221-147">Sulla barra degli strumenti fare clic su **Ripristina**.</span><span class="sxs-lookup"><span data-stu-id="e2221-147">On the toolbar, click **Restore**.</span></span>

   ![barra degli strumenti di ripristino](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. <span data-ttu-id="e2221-149">Nella pagina Ripristina fare clic su **A lungo termine**.</span><span class="sxs-lookup"><span data-stu-id="e2221-149">On the Restore page, click **Long-term**.</span></span>

5. <span data-ttu-id="e2221-150">Nei backup dell'insieme di credenziali di Azure fare clic su **Selezionare un backup** per visualizzare i backup di database disponibili nella conservazione dei backup a lungo termine.</span><span class="sxs-lookup"><span data-stu-id="e2221-150">Under Azure vault backups, click **Select a backup** to view the available database backups in long-term backup retention.</span></span>

   ![backup nell'insieme di credenziali](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-the-azure-portal"></a><span data-ttu-id="e2221-152">Ripristinare un database da un backup nella conservazione backup a lungo termine con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e2221-152">Restore a database from a backup in long-term backup retention using the Azure portal</span></span>

<span data-ttu-id="e2221-153">È possibile ripristinare il database a un nuovo database ricavato da un backup nell'insieme di credenziali di Servizi di ripristino di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2221-153">You restore the database to a new database from a backup in the Azure Recovery Services vault.</span></span>

1. <span data-ttu-id="e2221-154">Nella pagina **Backup degli insiemi di credenziali di Azure** fare clic sul backup da ripristinare e quindi su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="e2221-154">On the **Azure vault backups** page, click the backup to restore and then click **Select**.</span></span>

   ![selezione del backup dell'insieme di credenziali](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. <span data-ttu-id="e2221-156">Nella casella di testo **Nome database** immettere un nome per il database ripristinato.</span><span class="sxs-lookup"><span data-stu-id="e2221-156">In the **Database name** text box, provide the name for the restored database.</span></span>

   ![nuovo nome database](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. <span data-ttu-id="e2221-158">Fare clic su **OK** per ripristinare il database dal backup presente nell'insieme di credenziali al nuovo database.</span><span class="sxs-lookup"><span data-stu-id="e2221-158">Click **OK** to restore your database from the backup in the vault to the new database.</span></span>

4. <span data-ttu-id="e2221-159">Sulla barra degli strumenti fare clic sull'icona di notifica per visualizzare lo stato del processo di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e2221-159">On the toolbar, click the notification icon to view the status of the restore job.</span></span>

   ![avanzamento del processo di ripristino dall'insieme di credenziali](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. <span data-ttu-id="e2221-161">Al termine del processo di ripristino, aprire la pagina **Database SQL** per visualizzare il database appena ripristinato.</span><span class="sxs-lookup"><span data-stu-id="e2221-161">When the restore job is completed, open the **SQL databases** page to view the newly restored database.</span></span>

   ![database ripristinato dall'insieme di credenziali](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> <span data-ttu-id="e2221-163">A questo punto è possibile connettersi al database ripristinato usando SQL Server Management Studio per eseguire le attività necessarie, ad esempio per [estrarre un bit di dati dal database ripristinato da copiare nel database esistente o per eliminare il database esistente e rinominare il database ripristinato con il nome del database esistente](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="e2221-163">From here, you can connect to the restored database using SQL Server Management Studio to perform needed tasks, such as to [extract a bit of data from the restored database to copy into the existing database or to delete the existing database and rename the restored database to the existing database name](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>
>

## <a name="powershell"></a><span data-ttu-id="e2221-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2221-164">PowerShell</span></span>

<span data-ttu-id="e2221-165">Nelle sezioni seguenti viene illustrato come usare PowerShell per configurare l'insieme di credenziali di Servizi di ripristino di Azure, visualizzare i backup nell'insieme di credenziali ed eseguire il ripristino dall'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="e2221-165">The following sections show you how to use PowerShell to configure the Azure Recovery Services vault, view backups in the vault, and restore from the vault.</span></span>

### <a name="create-a-recovery-services-vault"></a><span data-ttu-id="e2221-166">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="e2221-166">Create a recovery services vault</span></span>

<span data-ttu-id="e2221-167">Usare [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) per creare un nuovo insieme di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e2221-167">Use the [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) to create a recovery services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e2221-168">L'insieme di credenziali deve trovarsi nella stessa area del server logico di Azure SQL e deve usare lo stesso gruppo di risorse del server logico.</span><span class="sxs-lookup"><span data-stu-id="e2221-168">The vault must be located in the same region as the Azure SQL logical server, and must use the same resource group as the logical server.</span></span>

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-to-use-the-recovery-vault-for-its-long-term-retention-backups"></a><span data-ttu-id="e2221-169">Impostare il server per usare l'insieme di credenziali di ripristino per i backup con conservazione a lungo termine</span><span class="sxs-lookup"><span data-stu-id="e2221-169">Set your server to use the recovery vault for its long-term retention backups</span></span>

<span data-ttu-id="e2221-170">Usare il cmdlet [Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) per associare un insieme di credenziali dei servizi di ripristino creato in precedenza a un server di Azure SQL specifico.</span><span class="sxs-lookup"><span data-stu-id="e2221-170">Use the [Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet to associate a previously created recovery services vault with a specific Azure SQL server.</span></span>

```PowerShell
# Set your server to use the vault to for long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a><span data-ttu-id="e2221-171">Creare un criterio di conservazione</span><span class="sxs-lookup"><span data-stu-id="e2221-171">Create a retention policy</span></span>

<span data-ttu-id="e2221-172">Un criterio di conservazione consente di impostare per quanto tempo mantenere il backup di un database.</span><span class="sxs-lookup"><span data-stu-id="e2221-172">A retention policy is where you set how long to keep a database backup.</span></span> <span data-ttu-id="e2221-173">Usare il cmdlet [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) per ottenere il criterio di conservazione predefinito usato come modello per la creazione di criteri.</span><span class="sxs-lookup"><span data-stu-id="e2221-173">Use the [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet to get the default retention policy to use as the template for creating policies.</span></span> <span data-ttu-id="e2221-174">In questo modello il periodo di conservazione è di 2 anni.</span><span class="sxs-lookup"><span data-stu-id="e2221-174">In this template, the retention period is set for 2 years.</span></span> <span data-ttu-id="e2221-175">Eseguire quindi [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) per creare i criteri.</span><span class="sxs-lookup"><span data-stu-id="e2221-175">Next, run the [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) to finally create the policy.</span></span> 

> [!NOTE]
> <span data-ttu-id="e2221-176">Per alcuni cmdlet è necessario impostare il contesto dell'insieme di credenziali prima dell'esecuzione ([Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)), pertanto questo cmdlet è presente in alcuni frammenti correlati.</span><span class="sxs-lookup"><span data-stu-id="e2221-176">Some cmdlets require that you set the vault context before running ([Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) so you see this cmdlet in a few related snippets.</span></span> <span data-ttu-id="e2221-177">Il contesto viene impostato perché i criteri fanno parte dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="e2221-177">You set the context because the policy is part of the vault.</span></span> <span data-ttu-id="e2221-178">È possibile creare più criteri di conservazione per ogni insieme di credenziali e quindi applicare il criterio desiderato a database specifici.</span><span class="sxs-lookup"><span data-stu-id="e2221-178">You can create multiple retention policies for each vault and then apply the desired policy to specific databases.</span></span> 


```PowerShell
# Retrieve the default retention policy for the AzureSQLDatabase workload type
$retentionPolicy = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType AzureSQLDatabase

# Set the retention value to two years (you can set to any time between 1 week and 10 years)
$retentionPolicy.RetentionDurationType = "Years"
$retentionPolicy.RetentionCount = 2
$retentionPolicyName = "my2YearRetentionPolicy"

# Set the vault context to the vault you are creating the policy for
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# Create the new policy
$policy = New-AzureRmRecoveryServicesBackupProtectionPolicy -name $retentionPolicyName -WorkloadType AzureSQLDatabase -retentionPolicy $retentionPolicy
$policy
```

### <a name="configure-a-database-to-use-the-previously-defined-retention-policy"></a><span data-ttu-id="e2221-179">Configurare un database per usare il criterio di conservazione definito prima</span><span class="sxs-lookup"><span data-stu-id="e2221-179">Configure a database to use the previously defined retention policy</span></span>

<span data-ttu-id="e2221-180">Usare il cmdlet [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) per applicare i nuovi criteri a un database specifico.</span><span class="sxs-lookup"><span data-stu-id="e2221-180">Use the [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet to apply the new policy to a specific database.</span></span>

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a><span data-ttu-id="e2221-181">Visualizzare le informazioni sui backup e i backup nella conservazione a lungo termine</span><span class="sxs-lookup"><span data-stu-id="e2221-181">View backup info, and backups in long-term retention</span></span>

<span data-ttu-id="e2221-182">Visualizzare informazioni sui backup del database nella [conservazione backup a lungo termine](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="e2221-182">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

<span data-ttu-id="e2221-183">Usare i cmdlet seguenti per visualizzare le informazioni di backup:</span><span class="sxs-lookup"><span data-stu-id="e2221-183">Use the following cmdlets to view backup information:</span></span>

- [<span data-ttu-id="e2221-184">Get-AzureRmRecoveryServicesBackupContainer</span><span class="sxs-lookup"><span data-stu-id="e2221-184">Get-AzureRmRecoveryServicesBackupContainer</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [<span data-ttu-id="e2221-185">Get-AzureRmRecoveryServicesBackupItem</span><span class="sxs-lookup"><span data-stu-id="e2221-185">Get-AzureRmRecoveryServicesBackupItem</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [<span data-ttu-id="e2221-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="e2221-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

```PowerShell
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$databaseNeedingRestore = $databaseName

# Set the vault context to the vault we want to restore from
#$vault = Get-AzureRmRecoveryServicesVault -ResourceGroupName $resourceGroupName
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# the following commands find the container associated with the server 'myserver' under resource group 'myresourcegroup'
$container = Get-AzureRmRecoveryServicesBackupContainer -ContainerType AzureSQL -FriendlyName $vault.Name

# Get the long-term retention metadata associated with a specific database
$item = Get-AzureRmRecoveryServicesBackupItem -Container $container -WorkloadType AzureSQLDatabase -Name $databaseNeedingRestore

# Get all available backups for the previously indicated database
# Optionally, set the -StartDate and -EndDate parameters to return backups within a specific time period
$availableBackups = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $item
$availableBackups
```

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a><span data-ttu-id="e2221-187">Ripristinare un database da un backup nella conservazione dei backup a lungo termine</span><span class="sxs-lookup"><span data-stu-id="e2221-187">Restore a database from a backup in long-term backup retention</span></span>

<span data-ttu-id="e2221-188">Il ripristino dalla conservazione backup a lungo termine usa il cmdlet [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase).</span><span class="sxs-lookup"><span data-stu-id="e2221-188">Restoring from long-term backup retention uses the [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.</span></span>

```PowerShell
# Restore the most recent backup: $availableBackups[0]
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
> <span data-ttu-id="e2221-189">A questo punto è possibile connettersi al database ripristinato usando SQL Server Management Studio per eseguire le attività necessarie, ad esempio per estrarre un bit di dati dal database ripristinato da copiare nel database esistente o per eliminare il database esistente e rinominare il database ripristinato con il nome del database esistente.</span><span class="sxs-lookup"><span data-stu-id="e2221-189">From here, you can connect to the restored database using SQL Server Management Studio to perform needed tasks, such as to extract a bit of data from the restored database to copy into the existing database or to delete the existing database and rename the restored database to the existing database name.</span></span> <span data-ttu-id="e2221-190">Vedere [ripristino temporizzato](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="e2221-190">See [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2221-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e2221-191">Next steps</span></span>

- <span data-ttu-id="e2221-192">Per informazioni sui backup automatici generati dal servizio, vedere l'articolo relativo ai [backup automatici](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="e2221-192">To learn about service-generated automatic backups, see [automatic backups](sql-database-automated-backups.md)</span></span>
- <span data-ttu-id="e2221-193">Per altre informazioni sulla conservazione dei backup a lungo termine, vedere [conservazione dei backup a lungo termine](sql-database-long-term-retention.md)</span><span class="sxs-lookup"><span data-stu-id="e2221-193">To learn about long-term backup retention, see [long-term backup retention](sql-database-long-term-retention.md)</span></span>
- <span data-ttu-id="e2221-194">Per altre informazioni sul ripristino da backup, vedere [ripristino dal backup](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="e2221-194">To learn about restoring from backups, see [restore from backup](sql-database-recovery-using-backups.md)</span></span>
