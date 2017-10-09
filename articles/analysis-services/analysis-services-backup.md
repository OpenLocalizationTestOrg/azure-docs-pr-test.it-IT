---
title: database di Analysis Services aaaAzure di backup e ripristino | Documenti Microsoft
description: Viene descritto come toobackup e ripristino di un Azure Analysis Services database.
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
ms.openlocfilehash: cf0a782d237a95fdfa5ef628f998bd053aac0d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore"></a><span data-ttu-id="daddc-103">Backup e ripristino</span><span class="sxs-lookup"><span data-stu-id="daddc-103">Backup and restore</span></span>

<span data-ttu-id="daddc-104">Il backup dei database modello tabulare in Analysis Services di Azure è molto hello uguale a quello locale di Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="daddc-104">Backing up tabular model databases in Azure Analysis Services is much hello same as for on-premises Analysis Services.</span></span> <span data-ttu-id="daddc-105">la differenza principale Hello è dove memorizzare i file di backup.</span><span class="sxs-lookup"><span data-stu-id="daddc-105">hello primary difference is where you store your backup files.</span></span> <span data-ttu-id="daddc-106">I file di backup devono essere salvati tooa contenitore in un [account di archiviazione Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="daddc-106">Backup files must be saved tooa container in an [Azure storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="daddc-107">È possibile usare un account di archiviazione e un contenitore già esistenti, o è possibile crearne di nuovi durante la configurazione delle impostazioni di archiviazione per il server.</span><span class="sxs-lookup"><span data-stu-id="daddc-107">You can use a storage account and container you already have, or they can be created when configuring storage settings for your server.</span></span>

> [!NOTE]
> <span data-ttu-id="daddc-108">La creazione di un account di archiviazione può dare luogo a un nuovo servizio fatturabile.</span><span class="sxs-lookup"><span data-stu-id="daddc-108">Creating a storage account can result in a new billable service.</span></span> <span data-ttu-id="daddc-109">vedere, più toolearn [prezzi di archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/blobs/).</span><span class="sxs-lookup"><span data-stu-id="daddc-109">toolearn more, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span>
> 
> 

<span data-ttu-id="daddc-110">I backup vengono salvati con estensione abf.</span><span class="sxs-lookup"><span data-stu-id="daddc-110">Backups are saved with an abf extension.</span></span> <span data-ttu-id="daddc-111">Per i modelli tabulari in memoria, vengono archiviati sia i dati del modello che i metadati.</span><span class="sxs-lookup"><span data-stu-id="daddc-111">For in-memory tabular models, both model data and metadata are stored.</span></span> <span data-ttu-id="daddc-112">Per i modelli tabulari DirectQuery, vengono archiviati solo i metadati del modello.</span><span class="sxs-lookup"><span data-stu-id="daddc-112">For DirectQuery tabular models, only model metadata is stored.</span></span> <span data-ttu-id="daddc-113">I backup possono essere compressi e crittografati, a seconda delle opzioni di hello che prescelto.</span><span class="sxs-lookup"><span data-stu-id="daddc-113">Backups can be compressed and encrypted, depending on hello options you choose.</span></span> 



## <a name="configure-storage-settings"></a><span data-ttu-id="daddc-114">Configurare le impostazioni di archiviazione</span><span class="sxs-lookup"><span data-stu-id="daddc-114">Configure storage settings</span></span>
<span data-ttu-id="daddc-115">Prima del backup, è necessario tooconfigure le impostazioni di archiviazione per il server.</span><span class="sxs-lookup"><span data-stu-id="daddc-115">Before backing up, you need tooconfigure storage settings for your server.</span></span>


### <a name="tooconfigure-storage-settings"></a><span data-ttu-id="daddc-116">impostazioni di archiviazione tooconfigure</span><span class="sxs-lookup"><span data-stu-id="daddc-116">tooconfigure storage settings</span></span>
1.  <span data-ttu-id="daddc-117">Nel portale di Azure > **Impostazioni**, fare clic su **Backup**.</span><span class="sxs-lookup"><span data-stu-id="daddc-117">In Azure portal > **Settings**, click **Backup**.</span></span>

    ![Backup in Impostazioni](./media/analysis-services-backup/aas-backup-backups.png)

2.  <span data-ttu-id="daddc-119">Fare clic su **Abilitata** e quindi su **Impostazioni di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="daddc-119">Click **Enabled**, then click **Storage Settings**.</span></span>

    ![Abilita](./media/analysis-services-backup/aas-backup-enable.png)

3. <span data-ttu-id="daddc-121">Selezionare l'account di archiviazione o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="daddc-121">Select your storage account or create a new one.</span></span>

4. <span data-ttu-id="daddc-122">Selezionare un contenitore o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="daddc-122">Select a container or create a new one.</span></span>

    ![Selezionare un contenitore](./media/analysis-services-backup/aas-backup-container.png)

5. <span data-ttu-id="daddc-124">Salvare le impostazioni di backup.</span><span class="sxs-lookup"><span data-stu-id="daddc-124">Save your backup settings.</span></span>

    ![Salvare le impostazioni di backup](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a><span data-ttu-id="daddc-126">Backup</span><span class="sxs-lookup"><span data-stu-id="daddc-126">Backup</span></span>

### <a name="toobackup-by-using-ssms"></a><span data-ttu-id="daddc-127">toobackup utilizzando SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="daddc-127">toobackup by using SSMS</span></span>

1. <span data-ttu-id="daddc-128">In SSMS fare clic con il pulsante destro del mouse su un database > **Backup**.</span><span class="sxs-lookup"><span data-stu-id="daddc-128">In SSMS, right-click a database > **Back Up**.</span></span>

2. <span data-ttu-id="daddc-129">In **Backup database** > **File di backup** fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="daddc-129">In **Backup Database** > **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="daddc-130">In hello **Salva file con nome** finestra di dialogo, verificare il percorso di cartella hello e quindi digitare un nome per il file di backup hello.</span><span class="sxs-lookup"><span data-stu-id="daddc-130">In hello **Save file as** dialog, verify hello folder path, and then type a name for hello backup file.</span></span> 

4. <span data-ttu-id="daddc-131">In hello **Backup Database** finestra di dialogo, selezionare le opzioni.</span><span class="sxs-lookup"><span data-stu-id="daddc-131">In hello **Backup Database** dialog, select options.</span></span>

    <span data-ttu-id="daddc-132">**Consenti file sovrascrivere** -selezionare questa opzione toooverwrite i file di backup di hello stesso nome.</span><span class="sxs-lookup"><span data-stu-id="daddc-132">**Allow file overwrite** - Select this option toooverwrite backup files of hello same name.</span></span> <span data-ttu-id="daddc-133">Se questa opzione non è selezionata, il file hello da salvare non può avere hello stesso nome come un file già esistente in hello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="daddc-133">If this option is not selected, hello file you are saving cannot have hello same name as a file that already exists in hello same location.</span></span>

    <span data-ttu-id="daddc-134">**Applicare la compressione** -selezionare l'opzione toocompress hello del file di backup.</span><span class="sxs-lookup"><span data-stu-id="daddc-134">**Apply compression** - Select this option toocompress hello backup file.</span></span> <span data-ttu-id="daddc-135">I file di backup compressi consentono di risparmiare spazio su disco, ma richiedono un utilizzo della CPU leggermente più elevato.</span><span class="sxs-lookup"><span data-stu-id="daddc-135">Compressed backup files save disk space, but require slightly higher CPU utilization.</span></span> 

    <span data-ttu-id="daddc-136">**Crittografare i file di backup** -selezionare l'opzione tooencrypt hello del file di backup.</span><span class="sxs-lookup"><span data-stu-id="daddc-136">**Encrypt backup file** - Select this option tooencrypt hello backup file.</span></span> <span data-ttu-id="daddc-137">Questa opzione richiede un file di backup hello toosecure password fornita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="daddc-137">This option requires a user-supplied password toosecure hello backup file.</span></span> <span data-ttu-id="daddc-138">password Hello impedisce la lettura dei dati di backup hello qualsiasi altro mezzo di un'operazione di ripristino.</span><span class="sxs-lookup"><span data-stu-id="daddc-138">hello password prevents reading of hello backup data any other means than a restore operation.</span></span> <span data-ttu-id="daddc-139">Se si sceglie tooencrypt backup, archiviare password hello in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="daddc-139">If you choose tooencrypt backups, store hello password in a safe location.</span></span>

5. <span data-ttu-id="daddc-140">Fare clic su **OK** toocreate e salvare i file di backup hello.</span><span class="sxs-lookup"><span data-stu-id="daddc-140">Click **OK** toocreate and save hello backup file.</span></span>


### <a name="powershell"></a><span data-ttu-id="daddc-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="daddc-141">PowerShell</span></span>
<span data-ttu-id="daddc-142">Usare il cmdlet [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="daddc-142">Use [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.</span></span>

## <a name="restore"></a><span data-ttu-id="daddc-143">Ripristino</span><span class="sxs-lookup"><span data-stu-id="daddc-143">Restore</span></span>
<span data-ttu-id="daddc-144">Durante il ripristino, il file di backup deve essere nell'account di archiviazione hello configurate per il server.</span><span class="sxs-lookup"><span data-stu-id="daddc-144">When restoring, your backup file must be in hello storage account you've configured for your server.</span></span> <span data-ttu-id="daddc-145">Se è necessario un file di backup da un account di archiviazione locale percorso tooyour toomove, utilizzare [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) o hello [AzCopy](../storage/common/storage-use-azcopy.md) utilità della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="daddc-145">If you need toomove a backup file from an on-premises location tooyour storage account, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) or hello [AzCopy](../storage/common/storage-use-azcopy.md) command-line utility.</span></span> 



> [!NOTE]
> <span data-ttu-id="daddc-146">Se si esegue il ripristino da un server locale, è necessario rimuovere tutti gli utenti di dominio di hello dai ruoli del modello hello e aggiungerli nuovamente ruoli toohello come utenti di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="daddc-146">If you're restoring from an on-premises server, you must remove all hello domain users from hello model's roles and add them back toohello roles as Azure Active Directory users.</span></span>
> 
> 

### <a name="toorestore-by-using-ssms"></a><span data-ttu-id="daddc-147">toorestore utilizzando SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="daddc-147">toorestore by using SSMS</span></span>

1. <span data-ttu-id="daddc-148">In SSMS fare clic con il pulsante destro del mouse su un database > **Ripristina**.</span><span class="sxs-lookup"><span data-stu-id="daddc-148">In SSMS, right-click a database > **Restore**.</span></span>

2. <span data-ttu-id="daddc-149">In hello **Backup Database** finestra di dialogo, nella **file di Backup**, fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="daddc-149">In hello **Backup Database** dialog, in **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="daddc-150">In hello **Individua file di Database** finestra di dialogo, selezionare hello desiderata toorestore.</span><span class="sxs-lookup"><span data-stu-id="daddc-150">In hello **Locate Database Files** dialog, select hello file you want toorestore.</span></span>

4. <span data-ttu-id="daddc-151">In **ripristinare il database**, selezionare il database di hello.</span><span class="sxs-lookup"><span data-stu-id="daddc-151">In **Restore database**, select hello database.</span></span>

5. <span data-ttu-id="daddc-152">Specificare le opzioni.</span><span class="sxs-lookup"><span data-stu-id="daddc-152">Specify options.</span></span> <span data-ttu-id="daddc-153">Opzioni di sicurezza devono corrispondere le opzioni di backup hello che è utilizzato per eseguire il backup.</span><span class="sxs-lookup"><span data-stu-id="daddc-153">Security options must match hello backup options you used when backing up.</span></span>


### <a name="powershell"></a><span data-ttu-id="daddc-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="daddc-154">PowerShell</span></span>

<span data-ttu-id="daddc-155">Usare il cmdlet [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="daddc-155">Use [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.</span></span>


## <a name="related-information"></a><span data-ttu-id="daddc-156">Informazioni correlate</span><span class="sxs-lookup"><span data-stu-id="daddc-156">Related information</span></span>

[<span data-ttu-id="daddc-157">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="daddc-157">Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)  
<span data-ttu-id="daddc-158">[Disponibilità elevata](analysis-services-bcdr.md)   </span><span class="sxs-lookup"><span data-stu-id="daddc-158">[High availability](analysis-services-bcdr.md)   </span></span>  
[<span data-ttu-id="daddc-159">Gestire Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="daddc-159">Manage Azure Analysis Services</span></span>](analysis-services-manage.md)
