---
title: Backup e ripristino del database di Azure Analysis Services | Microsoft Docs
description: Viene descritto come eseguire backup e ripristino di un database di Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: bffa481a498b130ef1f2388a5ba856da5d164ee0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="backup-and-restore"></a><span data-ttu-id="023f3-103">Backup e ripristino</span><span class="sxs-lookup"><span data-stu-id="023f3-103">Backup and restore</span></span>

<span data-ttu-id="023f3-104">Il backup dei database modello tabulare in Azure Analysis Services è molto simile a quello di Analysis Services in locale.</span><span class="sxs-lookup"><span data-stu-id="023f3-104">Backing up tabular model databases in Azure Analysis Services is much the same as for on-premises Analysis Services.</span></span> <span data-ttu-id="023f3-105">La differenza principale è dove vengono archiviati i file di backup.</span><span class="sxs-lookup"><span data-stu-id="023f3-105">The primary difference is where you store your backup files.</span></span> <span data-ttu-id="023f3-106">I file di backup devono essere salvati in un contenitore in un [account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="023f3-106">Backup files must be saved to a container in an [Azure storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="023f3-107">È possibile usare un account di archiviazione e un contenitore già esistenti, o è possibile crearne di nuovi durante la configurazione delle impostazioni di archiviazione per il server.</span><span class="sxs-lookup"><span data-stu-id="023f3-107">You can use a storage account and container you already have, or they can be created when configuring storage settings for your server.</span></span>

> [!NOTE]
> <span data-ttu-id="023f3-108">La creazione di un account di archiviazione può dare luogo a un nuovo servizio fatturabile.</span><span class="sxs-lookup"><span data-stu-id="023f3-108">Creating a storage account can result in a new billable service.</span></span> <span data-ttu-id="023f3-109">Per altre informazioni, vedere [Prezzi di Archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/blobs/).</span><span class="sxs-lookup"><span data-stu-id="023f3-109">To learn more, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span>
> 
> 

<span data-ttu-id="023f3-110">I backup vengono salvati con estensione abf.</span><span class="sxs-lookup"><span data-stu-id="023f3-110">Backups are saved with an abf extension.</span></span> <span data-ttu-id="023f3-111">Per i modelli tabulari in memoria, vengono archiviati sia i dati del modello che i metadati.</span><span class="sxs-lookup"><span data-stu-id="023f3-111">For in-memory tabular models, both model data and metadata are stored.</span></span> <span data-ttu-id="023f3-112">Per i modelli tabulari DirectQuery, vengono archiviati solo i metadati del modello.</span><span class="sxs-lookup"><span data-stu-id="023f3-112">For DirectQuery tabular models, only model metadata is stored.</span></span> <span data-ttu-id="023f3-113">I backup possono essere compressi e crittografati, a seconda delle opzioni scelte.</span><span class="sxs-lookup"><span data-stu-id="023f3-113">Backups can be compressed and encrypted, depending on the options you choose.</span></span> 



## <a name="configure-storage-settings"></a><span data-ttu-id="023f3-114">Configurare le impostazioni di archiviazione</span><span class="sxs-lookup"><span data-stu-id="023f3-114">Configure storage settings</span></span>
<span data-ttu-id="023f3-115">Prima di eseguire il backup, è necessario configurare le impostazioni di archiviazione per il server.</span><span class="sxs-lookup"><span data-stu-id="023f3-115">Before backing up, you need to configure storage settings for your server.</span></span>


### <a name="to-configure-storage-settings"></a><span data-ttu-id="023f3-116">Per configurare le impostazioni di archiviazione</span><span class="sxs-lookup"><span data-stu-id="023f3-116">To configure storage settings</span></span>
1.  <span data-ttu-id="023f3-117">Nel portale di Azure > **Impostazioni**, fare clic su **Backup**.</span><span class="sxs-lookup"><span data-stu-id="023f3-117">In Azure portal > **Settings**, click **Backup**.</span></span>

    ![Backup in Impostazioni](./media/analysis-services-backup/aas-backup-backups.png)

2.  <span data-ttu-id="023f3-119">Fare clic su **Abilitata** e quindi su **Impostazioni di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="023f3-119">Click **Enabled**, then click **Storage Settings**.</span></span>

    ![Abilita](./media/analysis-services-backup/aas-backup-enable.png)

3. <span data-ttu-id="023f3-121">Selezionare l'account di archiviazione o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="023f3-121">Select your storage account or create a new one.</span></span>

4. <span data-ttu-id="023f3-122">Selezionare un contenitore o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="023f3-122">Select a container or create a new one.</span></span>

    ![Selezionare un contenitore](./media/analysis-services-backup/aas-backup-container.png)

5. <span data-ttu-id="023f3-124">Salvare le impostazioni di backup.</span><span class="sxs-lookup"><span data-stu-id="023f3-124">Save your backup settings.</span></span>

    ![Salvare le impostazioni di backup](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a><span data-ttu-id="023f3-126">Backup</span><span class="sxs-lookup"><span data-stu-id="023f3-126">Backup</span></span>

### <a name="to-backup-by-using-ssms"></a><span data-ttu-id="023f3-127">Per eseguire il backup tramite SSMS</span><span class="sxs-lookup"><span data-stu-id="023f3-127">To backup by using SSMS</span></span>

1. <span data-ttu-id="023f3-128">In SSMS fare clic con il pulsante destro del mouse su un database > **Backup**.</span><span class="sxs-lookup"><span data-stu-id="023f3-128">In SSMS, right-click a database > **Back Up**.</span></span>

2. <span data-ttu-id="023f3-129">In **Backup database** > **File di backup** fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="023f3-129">In **Backup Database** > **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="023f3-130">Nella finestra di dialogo **Salva file con nome** verificare il percorso della cartella e quindi digitare un nome per il file di backup.</span><span class="sxs-lookup"><span data-stu-id="023f3-130">In the **Save file as** dialog, verify the folder path, and then type a name for the backup file.</span></span> 

4. <span data-ttu-id="023f3-131">Nella finestra di dialogo **Backup database** selezionare le opzioni.</span><span class="sxs-lookup"><span data-stu-id="023f3-131">In the **Backup Database** dialog, select options.</span></span>

    <span data-ttu-id="023f3-132">**Consenti sostituzione file**: selezionare questa opzione per sovrascrivere i file di backup con lo stesso nome.</span><span class="sxs-lookup"><span data-stu-id="023f3-132">**Allow file overwrite** - Select this option to overwrite backup files of the same name.</span></span> <span data-ttu-id="023f3-133">Se questa opzione non è selezionata, il file da salvare non può avere lo stesso nome di un file già esistente nello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="023f3-133">If this option is not selected, the file you are saving cannot have the same name as a file that already exists in the same location.</span></span>

    <span data-ttu-id="023f3-134">**Applica compressione**: selezionare questa opzione per comprimere il file di backup.</span><span class="sxs-lookup"><span data-stu-id="023f3-134">**Apply compression** - Select this option to compress the backup file.</span></span> <span data-ttu-id="023f3-135">I file di backup compressi consentono di risparmiare spazio su disco, ma richiedono un utilizzo della CPU leggermente più elevato.</span><span class="sxs-lookup"><span data-stu-id="023f3-135">Compressed backup files save disk space, but require slightly higher CPU utilization.</span></span> 

    <span data-ttu-id="023f3-136">**Crittografa file di backup**: selezionare questa opzione per crittografare il file di backup.</span><span class="sxs-lookup"><span data-stu-id="023f3-136">**Encrypt backup file** - Select this option to encrypt the backup file.</span></span> <span data-ttu-id="023f3-137">Questa opzione richiede una password specificata dall'utente per proteggere il file di backup.</span><span class="sxs-lookup"><span data-stu-id="023f3-137">This option requires a user-supplied password to secure the backup file.</span></span> <span data-ttu-id="023f3-138">La password impedisce la lettura dei dati di backup con qualsiasi mezzo che non sia un'operazione di ripristino.</span><span class="sxs-lookup"><span data-stu-id="023f3-138">The password prevents reading of the backup data any other means than a restore operation.</span></span> <span data-ttu-id="023f3-139">Se si sceglie di crittografare i backup, archiviare la password in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="023f3-139">If you choose to encrypt backups, store the password in a safe location.</span></span>

5. <span data-ttu-id="023f3-140">Fare clic su **OK** per creare e salvare il file di backup.</span><span class="sxs-lookup"><span data-stu-id="023f3-140">Click **OK** to create and save the backup file.</span></span>


### <a name="powershell"></a><span data-ttu-id="023f3-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="023f3-141">PowerShell</span></span>
<span data-ttu-id="023f3-142">Usare il cmdlet [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="023f3-142">Use [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.</span></span>

## <a name="restore"></a><span data-ttu-id="023f3-143">Ripristino</span><span class="sxs-lookup"><span data-stu-id="023f3-143">Restore</span></span>
<span data-ttu-id="023f3-144">Durante il ripristino, il file di backup deve essere nell'account di archiviazione configurato per il server.</span><span class="sxs-lookup"><span data-stu-id="023f3-144">When restoring, your backup file must be in the storage account you've configured for your server.</span></span> <span data-ttu-id="023f3-145">Se è necessario spostare un file di backup da un percorso locale all'account di archiviazione, usare [Archiviazione di Microsoft Azure](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) o l'utilità della riga di comando [AzCopy](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="023f3-145">If you need to move a backup file from an on-premises location to your storage account, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) or the [AzCopy](../storage/common/storage-use-azcopy.md) command-line utility.</span></span> 



> [!NOTE]
> <span data-ttu-id="023f3-146">Se si sta eseguendo il ripristino da un server locale, è necessario rimuovere tutti gli utenti di dominio dai ruoli del modello e aggiungerli nuovamente ai ruoli come utenti di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="023f3-146">If you're restoring from an on-premises server, you must remove all the domain users from the model's roles and add them back to the roles as Azure Active Directory users.</span></span>
> 
> 

### <a name="to-restore-by-using-ssms"></a><span data-ttu-id="023f3-147">Per eseguire il ripristino usando SSMS</span><span class="sxs-lookup"><span data-stu-id="023f3-147">To restore by using SSMS</span></span>

1. <span data-ttu-id="023f3-148">In SSMS fare clic con il pulsante destro del mouse su un database > **Ripristina**.</span><span class="sxs-lookup"><span data-stu-id="023f3-148">In SSMS, right-click a database > **Restore**.</span></span>

2. <span data-ttu-id="023f3-149">Nella finestra di dialogo **Backup database** in **File di backup** fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="023f3-149">In the **Backup Database** dialog, in **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="023f3-150">Nella finestra di dialogo **Trova file di database** selezionare il file da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="023f3-150">In the **Locate Database Files** dialog, select the file you want to restore.</span></span>

4. <span data-ttu-id="023f3-151">In **Ripristina database** selezionare il database.</span><span class="sxs-lookup"><span data-stu-id="023f3-151">In **Restore database**, select the database.</span></span>

5. <span data-ttu-id="023f3-152">Specificare le opzioni.</span><span class="sxs-lookup"><span data-stu-id="023f3-152">Specify options.</span></span> <span data-ttu-id="023f3-153">Le opzioni di sicurezza devono corrispondere alle opzioni di backup usate per eseguire il backup.</span><span class="sxs-lookup"><span data-stu-id="023f3-153">Security options must match the backup options you used when backing up.</span></span>


### <a name="powershell"></a><span data-ttu-id="023f3-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="023f3-154">PowerShell</span></span>

<span data-ttu-id="023f3-155">Usare il cmdlet [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="023f3-155">Use [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.</span></span>


## <a name="related-information"></a><span data-ttu-id="023f3-156">Informazioni correlate</span><span class="sxs-lookup"><span data-stu-id="023f3-156">Related information</span></span>

[<span data-ttu-id="023f3-157">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="023f3-157">Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)  
<span data-ttu-id="023f3-158">[Disponibilità elevata](analysis-services-bcdr.md)   </span><span class="sxs-lookup"><span data-stu-id="023f3-158">[High availability](analysis-services-bcdr.md)   </span></span>  
[<span data-ttu-id="023f3-159">Gestire Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="023f3-159">Manage Azure Analysis Services</span></span>](analysis-services-manage.md)
