---
title: aaaUse Azure Backup agent tooback backup di file e cartelle | Documenti Microsoft
description: Utilizzare hello Microsoft Azure Backup agent tooback backup tooAzure file e cartelle di Windows. Creare un insieme di credenziali di servizi di ripristino, installare l'agente di Backup hello, definire i criteri di backup hello ed eseguire backup iniziale hello in cartelle e file hello.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: insieme di credenziali di backup; backup di un server Windows; backup di Windows;
ms.assetid: 7f5b1943-b3c1-4ddb-8fb7-3560533c68d5
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: be203c24841971872b5c6e7cf260a2fa5c58ac47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-client-tooazure-using-hello-resource-manager-deployment-model"></a><span data-ttu-id="070c7-105">Eseguire il backup di un tooAzure di Windows Server o client utilizzando hello modello di distribuzione di gestione risorse</span><span class="sxs-lookup"><span data-stu-id="070c7-105">Back up a Windows Server or client tooAzure using hello Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="070c7-106">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="070c7-106">Azure portal</span></span>](backup-configure-vault.md)
> * [<span data-ttu-id="070c7-107">Portale classico</span><span class="sxs-lookup"><span data-stu-id="070c7-107">Classic portal</span></span>](backup-configure-vault-classic.md)
>
>

<span data-ttu-id="070c7-108">Questo articolo spiega come tooAzure tooback backup del Server di Windows (o un client di Windows) di file e cartelle con Azure Backup tramite hello il modello di distribuzione di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="070c7-108">This article explains how tooback up your Windows Server (or Windows client) files and folders tooAzure with Azure Backup using hello Resource Manager deployment model.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![Passaggi del processo di backup](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a><span data-ttu-id="070c7-110">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="070c7-110">Before you start</span></span>
<span data-ttu-id="070c7-111">tooback backup di un server o client tooAzure, è necessario un account di Azure.</span><span class="sxs-lookup"><span data-stu-id="070c7-111">tooback up a server or client tooAzure, you need an Azure account.</span></span> <span data-ttu-id="070c7-112">Se non si ha un account, è possibile crearne uno [gratuito](https://azure.microsoft.com/free/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="070c7-112">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="070c7-113">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="070c7-113">Create a Recovery Services vault</span></span>
<span data-ttu-id="070c7-114">Un insieme di credenziali di servizi di ripristino è un'entità contenente tutti i backup di hello e i punti di ripristino creati nel corso del tempo.</span><span class="sxs-lookup"><span data-stu-id="070c7-114">A Recovery Services vault is an entity that stores all hello backups and recovery points you create over time.</span></span> <span data-ttu-id="070c7-115">insieme di credenziali di servizi di ripristino Hello contiene inoltre hello applicato criteri di backup protetti toohello file e cartelle.</span><span class="sxs-lookup"><span data-stu-id="070c7-115">hello Recovery Services vault also contains hello backup policy applied toohello protected files and folders.</span></span> <span data-ttu-id="070c7-116">Quando si crea un insieme di credenziali di servizi di ripristino, è necessario inoltre selezionare opzione di ridondanza di archiviazione appropriato hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-116">When you create a Recovery Services vault, you should also select hello appropriate storage redundancy option.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="070c7-117">toocreate un insieme di credenziali di servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="070c7-117">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="070c7-118">Se non già stato fatto, accedere toohello [portale Azure](https://portal.azure.com/) tramite la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="070c7-118">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="070c7-119">Nel menu Hub hello, fare clic su **più servizi** e nell'elenco di hello delle risorse, digitare **servizi di ripristino** e fare clic su **insiemi di credenziali di servizi di ripristino**.</span><span class="sxs-lookup"><span data-stu-id="070c7-119">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="070c7-121">Se sono presenti archivi di servizi di ripristino nella sottoscrizione hello, vengono elencati gli insiemi di credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-121">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>

3. <span data-ttu-id="070c7-122">In hello **insiemi di credenziali di servizi di ripristino** menu, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="070c7-122">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="070c7-124">Servizi di ripristino Hello insieme di credenziali si apre Pannello chiesto tooprovide un **nome**, **sottoscrizione**, **gruppo di risorse**, e **percorso**.</span><span class="sxs-lookup"><span data-stu-id="070c7-124">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="070c7-126">Per **nome**, immettere un insieme di credenziali di nome descrittivo tooidentify hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-126">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="070c7-127">nome di Hello deve toobe univoco per la sottoscrizione di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-127">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="070c7-128">Digitare un nome che contenga tra i 2 e i 50 caratteri.</span><span class="sxs-lookup"><span data-stu-id="070c7-128">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="070c7-129">Deve iniziare con una lettera e può contenere solo lettere, numeri e trattini.</span><span class="sxs-lookup"><span data-stu-id="070c7-129">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="070c7-130">In hello **sottoscrizione** sezione, utilizzare hello toochoose di menu a discesa hello sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="070c7-130">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="070c7-131">Se si utilizza una sola sottoscrizione, che viene visualizzato di sottoscrizione ed è possibile ignorare toohello successivo passaggio.</span><span class="sxs-lookup"><span data-stu-id="070c7-131">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="070c7-132">Se non sei sicuro che toouse di sottoscrizione, utilizzare predefinito hello (o suggerito) sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="070c7-132">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="070c7-133">Sono disponibili più scelte solo se l'account dell'organizzazione è associato a più sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="070c7-133">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="070c7-134">In hello **gruppo di risorse** sezione:</span><span class="sxs-lookup"><span data-stu-id="070c7-134">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="070c7-135">Selezionare **Crea nuovo** se si desidera toocreate un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="070c7-135">select **Create new** if you want toocreate a new Resource group.</span></span>
    <span data-ttu-id="070c7-136">Or</span><span class="sxs-lookup"><span data-stu-id="070c7-136">Or</span></span>
    * <span data-ttu-id="070c7-137">Selezionare **utilizzare esistente** e fare clic su hello dal menu a discesa toosee hello disponibili elenco di gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="070c7-137">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="070c7-138">Per informazioni complete su gruppi di risorse, vedere hello [Panoramica di gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="070c7-138">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="070c7-139">Fare clic su **percorso** tooselect hello località geografica per l'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-139">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="070c7-140">Questa opzione determina l'area geografica di hello in cui viene inviati ai dati di backup.</span><span class="sxs-lookup"><span data-stu-id="070c7-140">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="070c7-141">Nella parte inferiore di hello del pannello dell'insieme di credenziali di servizi di ripristino hello, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="070c7-141">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

  <span data-ttu-id="070c7-142">Può richiedere alcuni minuti per hello che toobe creato insieme di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="070c7-142">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="070c7-143">Monitorare le notifiche di stato hello in area destra superiore hello del portale hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-143">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="070c7-144">Una volta creato l'insieme di credenziali, viene visualizzato nell'elenco hello degli insiemi di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="070c7-144">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="070c7-145">Se l'insieme di credenziali non viene visualizzato dopo qualche minuto, fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="070c7-145">If after several minutes you don't see your vault, click **Refresh**.</span></span>

  ![Fare clic sul pulsante Aggiorna](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  <span data-ttu-id="070c7-147">Dopo aver visualizzato l'insieme di credenziali nell'elenco di hello degli insiemi di credenziali di servizi di ripristino, si è pronti tooset ridondanza dell'archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-147">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>


### <a name="set-storage-redundancy"></a><span data-ttu-id="070c7-148">Impostare la ridondanza di archiviazione</span><span class="sxs-lookup"><span data-stu-id="070c7-148">Set storage redundancy</span></span>
<span data-ttu-id="070c7-149">Quando si crea per la prima volta un insieme di credenziali di Servizi di ripristino, si determina come replicare lo spazio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="070c7-149">When you first create a Recovery Services vault you determine how storage is replicated.</span></span>

1. <span data-ttu-id="070c7-150">Da hello **insiemi di credenziali di servizi di ripristino** pannello, fare clic su nuovo insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-150">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Selezionare nuovo insieme di credenziali hello hello elenco dell'insieme di credenziali di servizi di ripristino](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="070c7-152">Quando si seleziona l'insieme di credenziali hello, hello **insieme di credenziali di servizi di ripristino** consente di restringere blade e pannello impostazioni hello (*che ha il nome di hello dell'insieme di credenziali hello nella parte superiore di hello*) e pannello Dettagli insieme di credenziali hello aperto.</span><span class="sxs-lookup"><span data-stu-id="070c7-152">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Configurazione dell'archiviazione hello vista per nuovo insieme di credenziali](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. <span data-ttu-id="070c7-154">Nel pannello impostazioni di hello nuovo insieme di credenziali, utilizzare hello tooscroll di scorrimento verticale verso il basso toohello sezione gestione e fare clic su **infrastruttura Backup**.</span><span class="sxs-lookup"><span data-stu-id="070c7-154">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>

  <span data-ttu-id="070c7-155">verrà visualizzata la finestra di blade Backup infrastruttura Hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-155">hello Backup Infrastructure blade opens.</span></span>

3. <span data-ttu-id="070c7-156">Nel Pannello di hello infrastruttura di Backup, fare clic su **la configurazione del Backup** tooopen hello **la configurazione del Backup** blade.</span><span class="sxs-lookup"><span data-stu-id="070c7-156">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

  ![Set di configurazione dell'archiviazione hello per nuovo insieme di credenziali](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)

4. <span data-ttu-id="070c7-158">Scegliere l'opzione di replica di archiviazione appropriato hello per l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="070c7-158">Choose hello appropriate storage replication option for your vault.</span></span>

  ![opzioni di configurazione dell'archiviazione](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

  <span data-ttu-id="070c7-160">Per impostazione predefinita, l'insieme di credenziali prevede l'archiviazione con ridondanza geografica.</span><span class="sxs-lookup"><span data-stu-id="070c7-160">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="070c7-161">Se si usa Azure come un endpoint di archiviazione di backup primario, continuare toouse **con ridondanza geografica**.</span><span class="sxs-lookup"><span data-stu-id="070c7-161">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="070c7-162">Se non si utilizza Azure come un endpoint di archiviazione di backup primario, quindi scegliere **ridondanza locale**, che consente di ridurre i costi di archiviazione di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-162">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="070c7-163">Per altre informazioni sulle opzioni di archiviazione [con ridondanza geografica](../storage/common/storage-redundancy.md#geo-redundant-storage) e [con ridondanza locale](../storage/common/storage-redundancy.md#locally-redundant-storage), vedere [Panoramica della ridondanza di archiviazione](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="070c7-163">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="070c7-164">Dopo aver creato un insieme di credenziali, preparare l'infrastruttura tooback backup di file e cartelle dal download e installazione agente servizi di ripristino di Microsoft Azure hello, scaricare l'insieme di credenziali e quindi utilizzare tali credenziali tooregister hello agente insieme di credenziali Hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-164">Now that you've created a vault, prepare your infrastructure tooback up files and folders by downloading and installing hello Microsoft Azure Recovery Services agent, downloading vault credentials, and then using those credentials tooregister hello agent with hello vault.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="070c7-165">Configurare l'insieme di credenziali hello</span><span class="sxs-lookup"><span data-stu-id="070c7-165">Configure hello vault</span></span>

1. <span data-ttu-id="070c7-166">In hello pannello dell'insieme di credenziali di servizi di ripristino (per hello insieme di credenziali appena creato), nella sezione Guida introduttiva hello, fare clic su **Backup**, quindi su hello **Introduzione a Backup** pannello seleziona  **Obiettivo di backup**.</span><span class="sxs-lookup"><span data-stu-id="070c7-166">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

  ![Aprire il Pannello Obiettivo di backup](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  <span data-ttu-id="070c7-168">Hello **Backup obiettivo** apre blade.</span><span class="sxs-lookup"><span data-stu-id="070c7-168">hello **Backup Goal** blade opens.</span></span> <span data-ttu-id="070c7-169">Se hello insieme di credenziali di servizi di ripristino è stata configurata in precedenza, hello **Backup obiettivo** pannelli viene visualizzata quando si fa clic su **Backup** in servizi di ripristino hello credenziali blade.</span><span class="sxs-lookup"><span data-stu-id="070c7-169">If hello Recovery Services vault has been previously configured, then hello **Backup Goal** blades opens when you click **Backup** on hello Recovery Services vault blade.</span></span>

  ![Aprire il Pannello Obiettivo di backup](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="070c7-171">Da hello **in cui viene eseguito il carico di lavoro?** menu a discesa, seleziona **locale**.</span><span class="sxs-lookup"><span data-stu-id="070c7-171">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

  <span data-ttu-id="070c7-172">Si sceglie **Locale** perché il server di Windows o il computer Windows è un computer fisico che non si trova in Azure.</span><span class="sxs-lookup"><span data-stu-id="070c7-172">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="070c7-173">Da hello **cosa si desidera toobackup?** dal menu **file e cartelle**, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="070c7-173">From hello **What do you want toobackup?** menu, select **Files and folders**, and click **OK**.</span></span>

  ![Configurazione di file e cartelle](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

  <span data-ttu-id="070c7-175">Fare clic su OK, un segno di spunta accanto troppo**obiettivo Backup**, hello e **Prepare infrastruttura** apre blade.</span><span class="sxs-lookup"><span data-stu-id="070c7-175">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

  ![Preparare l'infrastruttura dopo aver configurato l'obiettivo del backup](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="070c7-177">In hello **Prepare infrastruttura** pannello, fare clic su **Scarica agente per Windows Server o Client Windows**.</span><span class="sxs-lookup"><span data-stu-id="070c7-177">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

  ![Preparare l'infrastruttura](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

  <span data-ttu-id="070c7-179">Se si utilizza Windows Server essenziali, quindi scegliere agente hello toodownload per Windows Server essenziali.</span><span class="sxs-lookup"><span data-stu-id="070c7-179">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="070c7-180">Un menu a comparsa chiede toorun o salvare MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="070c7-180">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

  ![Finestra di dialogo di MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="070c7-182">Nel menu a comparsa download hello, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="070c7-182">In hello download pop-up menu, click **Save**.</span></span>

  <span data-ttu-id="070c7-183">Per impostazione predefinita, hello **MARSagentinstaller.exe** tooyour cartella di download viene salvato.</span><span class="sxs-lookup"><span data-stu-id="070c7-183">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="070c7-184">Al termine dell'installazione guidata di hello, verrà visualizzato un messaggio popup che chiede se si desidera che il programma di installazione di toorun hello o aprire la cartella hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-184">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

  ![Preparare l'infrastruttura](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

  <span data-ttu-id="070c7-186">È necessario ancora agente hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="070c7-186">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="070c7-187">È possibile installare l'agente di hello dopo avere scaricato l'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-187">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="070c7-188">In hello **Prepare infrastruttura** pannello, fare clic su **scaricare**.</span><span class="sxs-lookup"><span data-stu-id="070c7-188">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

  ![Scaricare le credenziali dell'insieme di credenziali](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

  <span data-ttu-id="070c7-190">insieme di credenziali Hello scaricare tooyour cartella di download.</span><span class="sxs-lookup"><span data-stu-id="070c7-190">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="070c7-191">Dopo l'insieme di credenziali hello completare il download, vengono visualizzati una finestra popup che chiede se si desidera tooopen o salvare le credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-191">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="070c7-192">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="070c7-192">Click **Save**.</span></span> <span data-ttu-id="070c7-193">Se si sceglie accidentalmente **aprire**, consentono di finestra di dialogo hello tenta tooopen hello insieme di credenziali, l'esito negativo.</span><span class="sxs-lookup"><span data-stu-id="070c7-193">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="070c7-194">È possibile aprire l'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-194">You cannot open hello vault credentials.</span></span> <span data-ttu-id="070c7-195">Passaggio successivo toohello di procedere.</span><span class="sxs-lookup"><span data-stu-id="070c7-195">Proceed toohello next step.</span></span> <span data-ttu-id="070c7-196">insieme di credenziali Hello sono nella cartella di download di hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-196">hello vault credentials are in hello Downloads folder.</span></span>   

  ![Il download delle credenziali dell'insieme di credenziali è terminato](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="070c7-198">Installare e registrare agente hello</span><span class="sxs-lookup"><span data-stu-id="070c7-198">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="070c7-199">Non è ancora disponibile, l'abilitazione backup tramite il portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-199">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="070c7-200">Utilizzare hello tooback di agente servizi di ripristino di Microsoft Azure backup di file e cartelle.</span><span class="sxs-lookup"><span data-stu-id="070c7-200">Use hello Microsoft Azure Recovery Services Agent tooback up your files and folders.</span></span>
>

1. <span data-ttu-id="070c7-201">Individuare e fare doppio clic su hello **MARSagentinstaller.exe** dalla cartella download di hello (o altro percorso di salvataggio).</span><span class="sxs-lookup"><span data-stu-id="070c7-201">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

  <span data-ttu-id="070c7-202">programma di installazione Hello fornisce una serie di messaggi durante l'estrazione, installa e registra l'agente di servizi di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-202">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

  ![Eseguire il programma di installazione dell'agente di Servizi di ripristino](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="070c7-204">Completare l'installazione guidata di Microsoft Azure Recovery Services Agent hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-204">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="070c7-205">procedura guidata hello toocomplete, è necessario:</span><span class="sxs-lookup"><span data-stu-id="070c7-205">toocomplete hello wizard, you need to:</span></span>

  * <span data-ttu-id="070c7-206">Scegliere il percorso della cartella di installazione e la cache di hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-206">Choose a location for hello installation and cache folder.</span></span>
  * <span data-ttu-id="070c7-207">Fornire il proprio proxy informazioni sul server se si utilizza un toohello tooconnect di server proxy internet.</span><span class="sxs-lookup"><span data-stu-id="070c7-207">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
  * <span data-ttu-id="070c7-208">Se si usa un proxy autenticato, immettere il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="070c7-208">Provide your user name and password details if you use an authenticated proxy.</span></span>
  * <span data-ttu-id="070c7-209">Fornire le credenziali dell'insieme di credenziali scaricato hello</span><span class="sxs-lookup"><span data-stu-id="070c7-209">Provide hello downloaded vault credentials</span></span>
  * <span data-ttu-id="070c7-210">Salvare la passphrase di crittografia hello in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="070c7-210">Save hello encryption passphrase in a secure location.</span></span>

  > [!NOTE]
  > <span data-ttu-id="070c7-211">Se si perde o dimentica passphrase hello, Microsoft non consente di ripristinare i dati di backup hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-211">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="070c7-212">Salvare il file hello in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="070c7-212">Save hello file in a secure location.</span></span> <span data-ttu-id="070c7-213">È necessario toorestore una copia di backup.</span><span class="sxs-lookup"><span data-stu-id="070c7-213">It is required toorestore a backup.</span></span>
  >
  >

<span data-ttu-id="070c7-214">agente Hello è ora installato e il computer è registrato toohello insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="070c7-214">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="070c7-215">È possibile tooconfigure e pianificare il backup.</span><span class="sxs-lookup"><span data-stu-id="070c7-215">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="070c7-216">Requisiti di rete e connettività</span><span class="sxs-lookup"><span data-stu-id="070c7-216">Network and Connectivity Requirements</span></span>

<span data-ttu-id="070c7-217">Se il computer/proxy ha limitato l'accesso a internet, assicurarsi che le impostazioni del firewall nel computer di hello/proxy siano configurati tooallow hello URL seguenti:</span><span class="sxs-lookup"><span data-stu-id="070c7-217">If your machine/proxy has limited internet access, ensure that firewall settings on hello machine/proxy are configured tooallow hello following URLs:</span></span> <br>
    1. <span data-ttu-id="070c7-218">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="070c7-218">www.msftncsi.com</span></span>
    2. <span data-ttu-id="070c7-219">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="070c7-219">*.Microsoft.com</span></span>
    3. <span data-ttu-id="070c7-220">windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="070c7-220">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="070c7-221">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="070c7-221">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="070c7-222">*. windows.ne</span><span class="sxs-lookup"><span data-stu-id="070c7-222">*.windows.ne</span></span>


## <a name="create-hello-backup-policy"></a><span data-ttu-id="070c7-223">Creare criteri di backup hello</span><span class="sxs-lookup"><span data-stu-id="070c7-223">Create hello backup policy</span></span>
<span data-ttu-id="070c7-224">criterio di backup Hello è pianificazione hello quando i punti di ripristino vengono eseguiti e hello periodo di tempo sono mantenuti i punti di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-224">hello backup policy is hello schedule when recovery points are taken, and hello length of time hello recovery points are retained.</span></span> <span data-ttu-id="070c7-225">Usare hello Microsoft Azure Backup agent toocreate hello criterio di backup di file e cartelle.</span><span class="sxs-lookup"><span data-stu-id="070c7-225">Use hello Microsoft Azure Backup agent toocreate hello backup policy for files and folders.</span></span>

### <a name="toocreate-a-backup-schedule"></a><span data-ttu-id="070c7-226">toocreate una pianificazione di backup</span><span class="sxs-lookup"><span data-stu-id="070c7-226">toocreate a backup schedule</span></span>
1. <span data-ttu-id="070c7-227">Aprire l'agente di Backup di Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-227">Open hello Microsoft Azure Backup agent.</span></span> <span data-ttu-id="070c7-228">È possibile trovarlo se si cerca **Backup di Microsoft Azure**nel computer.</span><span class="sxs-lookup"><span data-stu-id="070c7-228">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Avviare l'agente Azure Backup hello](./media/backup-configure-vault/snap-in-search.png)
2. <span data-ttu-id="070c7-230">Nell'agente hello Backup **azioni** riquadro, fare clic su **pianifica Backup** toolaunch hello pianificazione guidata Backup.</span><span class="sxs-lookup"><span data-stu-id="070c7-230">In hello Backup agent's **Actions** pane, click **Schedule Backup** toolaunch hello Schedule Backup Wizard.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-configure-vault/schedule-first-backup.png)

3. <span data-ttu-id="070c7-232">In hello **Introduzione** di hello pianificazione guidata Backup fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="070c7-232">On hello **Getting started** page of hello Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="070c7-233">In hello **selezionare elementi tooBackup** pagina, fare clic su **Aggiungi elementi**.</span><span class="sxs-lookup"><span data-stu-id="070c7-233">On hello **Select Items tooBackup** page, click **Add Items**.</span></span>

  <span data-ttu-id="070c7-234">verrà visualizzata la finestra di dialogo Seleziona elementi Hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-234">hello Select Items dialog opens.</span></span>

5. <span data-ttu-id="070c7-235">Selezionare il file hello e le cartelle che desidera tooprotect e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="070c7-235">Select hello files and folders that you want tooprotect, and then click **OK**.</span></span>
6. <span data-ttu-id="070c7-236">In hello **selezionare elementi tooBackup** pagina, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="070c7-236">In hello **Select Items tooBackup** page, click **Next**.</span></span>
7. <span data-ttu-id="070c7-237">In hello **specificare pianificazione Backup** specificare pianificazione backup hello e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="070c7-237">On hello **Specify Backup Schedule** page, specify hello backup schedule and click **Next**.</span></span>

    <span data-ttu-id="070c7-238">È possibile pianificare backup giornalieri, da eseguire non più di tre volte al giorno, o settimanali.</span><span class="sxs-lookup"><span data-stu-id="070c7-238">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Elementi per il backup di Windows Server](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="070c7-240">Per ulteriori informazioni su come toospecify hello pianificazione del backup, vedere l'articolo hello [tooreplace utilizzare Azure Backup infrastruttura nastro](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="070c7-240">For more information about how toospecify hello backup schedule, see hello article [Use Azure Backup tooreplace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >

8. <span data-ttu-id="070c7-241">In hello **selezionare criteri di conservazione** pagina, scegliere hello di criteri di memorizzazione specifico hello hello copia di backup e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="070c7-241">On hello **Select Retention Policy** page, choose hello specific retention policies hello for hello backup copy and click **Next**.</span></span>

    <span data-ttu-id="070c7-242">criteri di conservazione Hello specificano durata hello viene archiviato il backup di hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-242">hello retention policy specifies hello duration which hello backup is stored.</span></span> <span data-ttu-id="070c7-243">Anziché specificare solo un criterio"semplice" per tutti i punti di backup, è possibile specificare i criteri di conservazione diversi in base a quando viene eseguito il backup di hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-243">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when hello backup occurs.</span></span> <span data-ttu-id="070c7-244">È possibile modificare toomeet criteri di conservazione giornaliero, settimanale, mensile e annuale hello le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="070c7-244">You can modify hello daily, weekly, monthly, and yearly retention policies toomeet your needs.</span></span>
9. <span data-ttu-id="070c7-245">Nella pagina tipo di Backup iniziale scegliere hello, scegliere il tipo di backup iniziale di hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-245">On hello Choose Initial Backup Type page, choose hello initial backup type.</span></span> <span data-ttu-id="070c7-246">Lasciare l'opzione hello **automaticamente tramite rete hello** selezionata e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="070c7-246">Leave hello option **Automatically over hello network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="070c7-247">È possibile eseguire il backup automaticamente tramite rete hello oppure è possibile eseguire il backup non in linea.</span><span class="sxs-lookup"><span data-stu-id="070c7-247">You can back up automatically over hello network, or you can back up offline.</span></span> <span data-ttu-id="070c7-248">resto Hello di questo articolo descrive il processo di hello per il backup automaticamente.</span><span class="sxs-lookup"><span data-stu-id="070c7-248">hello remainder of this article describes hello process for backing up automatically.</span></span> <span data-ttu-id="070c7-249">Se si preferisce toodo un backup offline, vedere l'articolo di hello [Offline backup flusso di lavoro in Backup di Azure](backup-azure-backup-import-export.md) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="070c7-249">If you prefer toodo an offline backup, review hello article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="070c7-250">Nella pagina di conferma hello, esaminare le informazioni di hello e quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="070c7-250">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>
11. <span data-ttu-id="070c7-251">Al termine la procedura guidata hello creazione pianificazione backup hello, fare clic su **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="070c7-251">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="070c7-252">Abilitare la limitazione della larghezza di banda</span><span class="sxs-lookup"><span data-stu-id="070c7-252">Enable network throttling</span></span>
<span data-ttu-id="070c7-253">agente di Backup di Microsoft Azure Hello fornisce la limitazione delle richieste di rete.</span><span class="sxs-lookup"><span data-stu-id="070c7-253">hello Microsoft Azure Backup agent provides network throttling.</span></span> <span data-ttu-id="070c7-254">La limitazione controlla l'uso della larghezza di banda della rete durante il trasferimento dati.</span><span class="sxs-lookup"><span data-stu-id="070c7-254">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="070c7-255">Questo controllo può essere utile se è necessario tooback dei dati durante le ore lavorative, ma non si desidera hello toointerfere di processo di backup con il traffico Internet.</span><span class="sxs-lookup"><span data-stu-id="070c7-255">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other Internet traffic.</span></span> <span data-ttu-id="070c7-256">La limitazione si applica tooback backup e ripristino.</span><span class="sxs-lookup"><span data-stu-id="070c7-256">Throttling applies tooback up and restore activities.</span></span>

> [!NOTE]
> <span data-ttu-id="070c7-257">La limitazione di rete non è disponibile su Windows Server 2008 R2 SP1, Windows Server 2008 SP2 o Windows 7 (con i pacchetti di servizio).</span><span class="sxs-lookup"><span data-stu-id="070c7-257">Network throttling is not available on Windows Server 2008 R2 SP1, Windows Server 2008 SP2, or Windows 7 (with service packs).</span></span> <span data-ttu-id="070c7-258">rete di Backup di Azure Hello limitazione funzionalità coinvolge Quality of Service (QoS) nel sistema operativo locale hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-258">hello Azure Backup network throttling feature engages Quality of Service (QoS) on hello local operating system.</span></span> <span data-ttu-id="070c7-259">Se il Backup di Azure per poter proteggere questi sistemi operativi, versione di hello QoS disponibile in queste piattaforme non funziona con la limitazione della rete di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="070c7-259">Though Azure Backup can protect these operating systems, hello version of QoS available on these platforms doesn't work with Azure Backup network throttling.</span></span> <span data-ttu-id="070c7-260">La limitazione di rete può essere utilizzata in tutti gli altri [sistemi operativi supportati](backup-azure-backup-faq.md).</span><span class="sxs-lookup"><span data-stu-id="070c7-260">Network throttling can be used on all other [supported operating systems](backup-azure-backup-faq.md).</span></span>
>
>

<span data-ttu-id="070c7-261">**la limitazione delle richieste di rete tooenable**</span><span class="sxs-lookup"><span data-stu-id="070c7-261">**tooenable network throttling**</span></span>

1. <span data-ttu-id="070c7-262">Nell'agente di Backup di Microsoft Azure hello, fare clic su **Modifica proprietà**.</span><span class="sxs-lookup"><span data-stu-id="070c7-262">In hello Microsoft Azure Backup agent, click **Change Properties**.</span></span>

    ![Modifica proprietà](./media/backup-configure-vault/change-properties.png)
2. <span data-ttu-id="070c7-264">In hello **limitazione** scheda, seleziona hello **abilitare la limitazione per le operazioni di backup all'utilizzo della larghezza di banda di internet** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="070c7-264">On hello **Throttling** tab, select hello **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![Limitazione della larghezza di banda della rete](./media/backup-configure-vault/throttling-dialog.png)
3. <span data-ttu-id="070c7-266">Dopo avere abilitato la limitazione delle richieste, specificare hello consentito della larghezza di banda per trasferire i dati di backup durante **ore lavorative** e **ore Non lavorative**.</span><span class="sxs-lookup"><span data-stu-id="070c7-266">After you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="070c7-267">i valori di larghezza di banda Hello iniziano 512 kilobit al secondo (Kbps) e possono aumentare fino a too1, 023 megabyte al secondo (MBps).</span><span class="sxs-lookup"><span data-stu-id="070c7-267">hello bandwidth values begin at 512 kilobits per second (Kbps) and can go up too1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="070c7-268">È anche possibile designare inizio hello e di fine per **ore lavorative**, e i giorni della settimana hello sono considerate giorni.</span><span class="sxs-lookup"><span data-stu-id="070c7-268">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered work days.</span></span> <span data-ttu-id="070c7-269">Gli orari al di fuori delle ore lavorative definite vengono considerati ore non lavorative.</span><span class="sxs-lookup"><span data-stu-id="070c7-269">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="070c7-270">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="070c7-270">Click **OK**.</span></span>

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a><span data-ttu-id="070c7-271">tooback backup di file e cartelle per la prima volta hello</span><span class="sxs-lookup"><span data-stu-id="070c7-271">tooback up files and folders for hello first time</span></span>
1. <span data-ttu-id="070c7-272">Nell'agente di backup hello, fare clic su **Effettua backup** hello toocomplete iniziale tramite rete hello il seeding.</span><span class="sxs-lookup"><span data-stu-id="070c7-272">In hello backup agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Eseguire ora il backup di Windows Server](./media/backup-configure-vault/backup-now.png)
2. <span data-ttu-id="070c7-274">Nella pagina di conferma hello, rivedere le impostazioni di hello che hello backup guidato immediato utilizzerà tooback macchina hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-274">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="070c7-275">Fare clic su **Backup**.</span><span class="sxs-lookup"><span data-stu-id="070c7-275">Then click **Back Up**.</span></span>
3. <span data-ttu-id="070c7-276">Fare clic su **Chiudi** guidata hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="070c7-276">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="070c7-277">Se si esegue questa operazione prima al termine del processo di backup hello, toorun guidata hello continua in background hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-277">If you do this before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

<span data-ttu-id="070c7-278">Al termine dell'operazione backup iniziale hello, hello **processo completato** stato viene visualizzato nella console Backup hello.</span><span class="sxs-lookup"><span data-stu-id="070c7-278">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

![Completamento infrarossi](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="070c7-280">Domande?</span><span class="sxs-lookup"><span data-stu-id="070c7-280">Questions?</span></span>
<span data-ttu-id="070c7-281">Se si hanno domande o se è presente una funzionalità che si desidera toosee incluso, [inviare commenti e suggerimenti](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="070c7-281">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="070c7-282">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="070c7-282">Next steps</span></span>
<span data-ttu-id="070c7-283">Per altre informazioni sul backup di macchine virtuali o altri carichi di lavoro, vedere:</span><span class="sxs-lookup"><span data-stu-id="070c7-283">For additional information about backing up VMs or other workloads, see:</span></span>

* <span data-ttu-id="070c7-284">Ora che si è eseguito il backup dei file e delle cartelle, è possibile [gestire l'insieme di credenziali e i server](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="070c7-284">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="070c7-285">Se è necessario toorestore una copia di backup, utilizzare anche in questo articolo[ripristinare i file tooa Windows macchina](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="070c7-285">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
