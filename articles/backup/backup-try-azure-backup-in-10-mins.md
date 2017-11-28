---
title: aaaBack backup Windows tooAzure di file e cartelle (gestione delle risorse) | Documenti Microsoft
description: Informazioni su tooback backup tooAzure file e cartelle di Windows in una distribuzione di gestione risorse.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "modalità toobackup; modalità tooback; backup di file e cartelle"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 8/15/2017
ms.author: markgal;
ms.openlocfilehash: 07d6580a84d5092ed2c61bf86ff5fcb148423ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-back-up-files-and-folders-in-resource-manager-deployment"></a><span data-ttu-id="1fb88-104">Primi passi: eseguire il backup di file e cartelle in una distribuzione Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1fb88-104">First look: back up files and folders in Resource Manager deployment</span></span>
<span data-ttu-id="1fb88-105">Questo articolo viene illustrato come tooAzure tooback backup del Server di Windows (o un computer Windows) file e cartelle, utilizzando una distribuzione di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="1fb88-105">This article explains how tooback up your Windows Server (or Windows computer) files and folders tooAzure using a Resource Manager deployment.</span></span> <span data-ttu-id="1fb88-106">Si tratta di un'esercitazione toowalk previsto di nozioni di base hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-106">It's a tutorial intended toowalk you through hello basics.</span></span> <span data-ttu-id="1fb88-107">Se si desidera tooget avviato tramite Backup di Azure, si è nel posto giusto hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-107">If you want tooget started using Azure Backup, you're in hello right place.</span></span>

<span data-ttu-id="1fb88-108">Se si desidera tooknow ulteriori informazioni su Backup di Azure, leggere questo [Panoramica](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="1fb88-108">If you want tooknow more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="1fb88-109">Se non è disponibile una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/) che consente di accedere a qualsiasi servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="1fb88-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="1fb88-110">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="1fb88-110">Create a recovery services vault</span></span>
<span data-ttu-id="1fb88-111">tooback backup di file e cartelle, è necessario un insieme di credenziali di servizi di ripristino nell'area di hello in cui si desidera dati hello toostore toocreate.</span><span class="sxs-lookup"><span data-stu-id="1fb88-111">tooback up your files and folders, you need toocreate a Recovery Services vault in hello region where you want toostore hello data.</span></span> <span data-ttu-id="1fb88-112">È inoltre necessario toodetermine la modalità di archiviazione replicata.</span><span class="sxs-lookup"><span data-stu-id="1fb88-112">You also need toodetermine how you want your storage replicated.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="1fb88-113">toocreate un insieme di credenziali di servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="1fb88-113">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="1fb88-114">Se non già stato fatto, accedere toohello [portale Azure](https://portal.azure.com/) tramite la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1fb88-114">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="1fb88-115">Nel menu Hub hello, fare clic su **più servizi** e nell'elenco di hello delle risorse, digitare **servizi di ripristino** e fare clic su **insiemi di credenziali di servizi di ripristino**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-115">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="1fb88-117">Se sono presenti archivi di servizi di ripristino nella sottoscrizione hello, vengono elencati gli insiemi di credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-117">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>
3. <span data-ttu-id="1fb88-118">In hello **insiemi di credenziali di servizi di ripristino** menu, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-118">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="1fb88-120">Servizi di ripristino Hello insieme di credenziali si apre Pannello chiesto tooprovide un **nome**, **sottoscrizione**, **gruppo di risorse**, e **percorso**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-120">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="1fb88-122">Per **nome**, immettere un insieme di credenziali di nome descrittivo tooidentify hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-122">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="1fb88-123">nome di Hello deve toobe univoco per la sottoscrizione di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-123">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="1fb88-124">Digitare un nome che contenga tra i 2 e i 50 caratteri.</span><span class="sxs-lookup"><span data-stu-id="1fb88-124">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="1fb88-125">Deve iniziare con una lettera e può contenere solo lettere, numeri e trattini.</span><span class="sxs-lookup"><span data-stu-id="1fb88-125">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="1fb88-126">In hello **sottoscrizione** sezione, utilizzare hello toochoose di menu a discesa hello sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1fb88-126">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="1fb88-127">Se si utilizza una sola sottoscrizione, che viene visualizzato di sottoscrizione ed è possibile ignorare toohello successivo passaggio.</span><span class="sxs-lookup"><span data-stu-id="1fb88-127">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="1fb88-128">Se non sei sicuro che toouse di sottoscrizione, utilizzare predefinito hello (o suggerito) sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="1fb88-128">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="1fb88-129">Sono disponibili più scelte solo se l'account dell'organizzazione è associato a più sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="1fb88-129">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="1fb88-130">In hello **gruppo di risorse** sezione:</span><span class="sxs-lookup"><span data-stu-id="1fb88-130">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="1fb88-131">Selezionare **Crea nuovo** se si desidera toocreate un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="1fb88-131">select **Create new** if you want toocreate a new Resource group.</span></span>
    <span data-ttu-id="1fb88-132">Or</span><span class="sxs-lookup"><span data-stu-id="1fb88-132">Or</span></span>
    * <span data-ttu-id="1fb88-133">Selezionare **utilizzare esistente** e fare clic su hello dal menu a discesa toosee hello disponibili elenco di gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="1fb88-133">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="1fb88-134">Per informazioni complete su gruppi di risorse, vedere hello [Panoramica di gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1fb88-134">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="1fb88-135">Fare clic su **percorso** tooselect hello località geografica per l'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-135">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="1fb88-136">Questa opzione determina l'area geografica di hello in cui viene inviati ai dati di backup.</span><span class="sxs-lookup"><span data-stu-id="1fb88-136">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="1fb88-137">Nella parte inferiore di hello del pannello dell'insieme di credenziali di servizi di ripristino hello, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-137">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="1fb88-138">Può richiedere alcuni minuti per hello che toobe creato insieme di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="1fb88-138">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="1fb88-139">Monitorare le notifiche di stato hello in area destra superiore hello del portale hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-139">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="1fb88-140">Una volta creato l'insieme di credenziali, viene visualizzato nell'elenco hello degli insiemi di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="1fb88-140">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="1fb88-141">Se l'insieme di credenziali non viene visualizzato dopo qualche minuto, fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-141">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Fare clic sul pulsante Aggiorna](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="1fb88-143">Dopo aver visualizzato l'insieme di credenziali nell'elenco di hello degli insiemi di credenziali di servizi di ripristino, si è pronti tooset ridondanza dell'archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-143">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-hello-vault"></a><span data-ttu-id="1fb88-144">Impostare la ridondanza di archiviazione per l'insieme di credenziali hello</span><span class="sxs-lookup"><span data-stu-id="1fb88-144">Set storage redundancy for hello vault</span></span>
<span data-ttu-id="1fb88-145">Quando si crea un insieme di credenziali di servizi di ripristino, verificare che la ridondanza dell'archiviazione è configurata hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="1fb88-145">When you create a Recovery Services vault, make sure storage redundancy is configured hello way you want.</span></span>

1. <span data-ttu-id="1fb88-146">Da hello **insiemi di credenziali di servizi di ripristino** pannello, fare clic su nuovo insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-146">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Selezionare nuovo insieme di credenziali hello hello elenco dell'insieme di credenziali di servizi di ripristino](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="1fb88-148">Quando si seleziona l'insieme di credenziali hello, hello **insieme di credenziali di servizi di ripristino** consente di restringere blade e pannello impostazioni hello (*che ha il nome di hello dell'insieme di credenziali hello nella parte superiore di hello*) e pannello Dettagli insieme di credenziali hello aperto.</span><span class="sxs-lookup"><span data-stu-id="1fb88-148">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Configurazione dell'archiviazione hello vista per nuovo insieme di credenziali](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="1fb88-150">Nel pannello impostazioni di hello nuovo insieme di credenziali, utilizzare hello tooscroll di scorrimento verticale verso il basso toohello sezione gestione e fare clic su **infrastruttura Backup**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-150">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="1fb88-151">verrà visualizzata la finestra di blade Backup infrastruttura Hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-151">hello Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="1fb88-152">Nel Pannello di hello infrastruttura di Backup, fare clic su **la configurazione del Backup** tooopen hello **la configurazione del Backup** blade.</span><span class="sxs-lookup"><span data-stu-id="1fb88-152">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

    ![Set di configurazione dell'archiviazione hello per nuovo insieme di credenziali](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="1fb88-154">Scegliere l'opzione di replica di archiviazione appropriato hello per l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="1fb88-154">Choose hello appropriate storage replication option for your vault.</span></span>

    ![opzioni di configurazione dell'archiviazione](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="1fb88-156">Per impostazione predefinita, l'insieme di credenziali prevede l'archiviazione con ridondanza geografica.</span><span class="sxs-lookup"><span data-stu-id="1fb88-156">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="1fb88-157">Se si usa Azure come un endpoint di archiviazione di backup primario, continuare toouse **con ridondanza geografica**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-157">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="1fb88-158">Se non si utilizza Azure come un endpoint di archiviazione di backup primario, quindi scegliere **ridondanza locale**, che consente di ridurre i costi di archiviazione di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-158">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="1fb88-159">Per altre informazioni sulle opzioni di archiviazione [con ridondanza geografica](../storage/common/storage-redundancy.md#geo-redundant-storage) e [con ridondanza locale](../storage/common/storage-redundancy.md#locally-redundant-storage), vedere [Panoramica della ridondanza di archiviazione](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="1fb88-159">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="1fb88-160">Dopo aver creato un insieme di credenziali, configurarlo per il backup di file e cartelle.</span><span class="sxs-lookup"><span data-stu-id="1fb88-160">Now that you've created a vault, configure it for backing up files and folders.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="1fb88-161">Configurare l'insieme di credenziali hello</span><span class="sxs-lookup"><span data-stu-id="1fb88-161">Configure hello vault</span></span>
1. <span data-ttu-id="1fb88-162">In hello pannello dell'insieme di credenziali di servizi di ripristino (per hello insieme di credenziali appena creato), nella sezione Guida introduttiva hello, fare clic su **Backup**, quindi su hello **Introduzione a Backup** pannello seleziona ** Obiettivo di backup**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-162">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Aprire il Pannello Obiettivo di backup](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="1fb88-164">Hello **Backup obiettivo** apre blade.</span><span class="sxs-lookup"><span data-stu-id="1fb88-164">hello **Backup Goal** blade opens.</span></span>

    ![Aprire il Pannello Obiettivo di backup](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="1fb88-166">Da hello **in cui viene eseguito il carico di lavoro?** menu a discesa, seleziona **locale**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-166">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="1fb88-167">Si sceglie **Locale** perché il server di Windows o il computer Windows è un computer fisico che non si trova in Azure.</span><span class="sxs-lookup"><span data-stu-id="1fb88-167">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="1fb88-168">Da hello **cosa si desidera toobackup?** dal menu **file e cartelle**, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-168">From hello **What do you want toobackup?** menu, select **Files and folders**, and click **OK**.</span></span>

    ![Configurazione di file e cartelle](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

    <span data-ttu-id="1fb88-170">Fare clic su OK, un segno di spunta accanto troppo**obiettivo Backup**, hello e **Prepare infrastruttura** apre blade.</span><span class="sxs-lookup"><span data-stu-id="1fb88-170">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

    ![Preparare l'infrastruttura dopo aver configurato l'obiettivo del backup](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="1fb88-172">In hello **Prepare infrastruttura** pannello, fare clic su **Scarica agente per Windows Server o Client Windows**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-172">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![Preparare l'infrastruttura](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="1fb88-174">Se si utilizza Windows Server essenziali, quindi scegliere agente hello toodownload per Windows Server essenziali.</span><span class="sxs-lookup"><span data-stu-id="1fb88-174">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="1fb88-175">Un menu a comparsa chiede toorun o salvare MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="1fb88-175">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

    ![Finestra di dialogo di MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="1fb88-177">Nel menu a comparsa download hello, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-177">In hello download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="1fb88-178">Per impostazione predefinita, hello **MARSagentinstaller.exe** tooyour cartella di download viene salvato.</span><span class="sxs-lookup"><span data-stu-id="1fb88-178">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="1fb88-179">Al termine dell'installazione guidata di hello, verrà visualizzato un messaggio popup che chiede se si desidera che il programma di installazione di toorun hello o aprire la cartella hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-179">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

    ![Preparare l'infrastruttura](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="1fb88-181">È necessario ancora agente hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="1fb88-181">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="1fb88-182">È possibile installare l'agente di hello dopo avere scaricato l'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-182">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="1fb88-183">In hello **Prepare infrastruttura** pannello, fare clic su **scaricare**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-183">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

    ![Scaricare le credenziali dell'insieme di credenziali](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="1fb88-185">insieme di credenziali Hello scaricare tooyour cartella di download.</span><span class="sxs-lookup"><span data-stu-id="1fb88-185">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="1fb88-186">Dopo l'insieme di credenziali hello completare il download, vengono visualizzati una finestra popup che chiede se si desidera tooopen o salvare le credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-186">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="1fb88-187">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-187">Click **Save**.</span></span> <span data-ttu-id="1fb88-188">Se si sceglie accidentalmente **aprire**, consentono di finestra di dialogo hello tenta tooopen hello insieme di credenziali, l'esito negativo.</span><span class="sxs-lookup"><span data-stu-id="1fb88-188">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="1fb88-189">È possibile aprire l'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-189">You cannot open hello vault credentials.</span></span> <span data-ttu-id="1fb88-190">Passaggio successivo toohello di procedere.</span><span class="sxs-lookup"><span data-stu-id="1fb88-190">Proceed toohello next step.</span></span> <span data-ttu-id="1fb88-191">insieme di credenziali Hello sono nella cartella di download di hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-191">hello vault credentials are in hello Downloads folder.</span></span>   

    ![Il download delle credenziali dell'insieme di credenziali è terminato](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="1fb88-193">Installare e registrare agente hello</span><span class="sxs-lookup"><span data-stu-id="1fb88-193">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="1fb88-194">Non è ancora disponibile, l'abilitazione backup tramite il portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-194">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="1fb88-195">Utilizzare hello tooback di agente servizi di ripristino di Microsoft Azure backup di file e cartelle.</span><span class="sxs-lookup"><span data-stu-id="1fb88-195">Use hello Microsoft Azure Recovery Services Agent tooback up your files and folders.</span></span>
>

1. <span data-ttu-id="1fb88-196">Individuare e fare doppio clic su hello **MARSagentinstaller.exe** dalla cartella download di hello (o altro percorso di salvataggio).</span><span class="sxs-lookup"><span data-stu-id="1fb88-196">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="1fb88-197">programma di installazione Hello fornisce una serie di messaggi durante l'estrazione, installa e registra l'agente di servizi di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-197">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

    ![Eseguire il programma di installazione dell'agente di Servizi di ripristino](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="1fb88-199">Completare l'installazione guidata di Microsoft Azure Recovery Services Agent hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-199">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="1fb88-200">procedura guidata hello toocomplete, è necessario:</span><span class="sxs-lookup"><span data-stu-id="1fb88-200">toocomplete hello wizard, you need to:</span></span>

   * <span data-ttu-id="1fb88-201">Scegliere il percorso della cartella di installazione e la cache di hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-201">Choose a location for hello installation and cache folder.</span></span>
   * <span data-ttu-id="1fb88-202">Fornire il proprio proxy informazioni sul server se si utilizza un toohello tooconnect di server proxy internet.</span><span class="sxs-lookup"><span data-stu-id="1fb88-202">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
   * <span data-ttu-id="1fb88-203">Se si usa un proxy autenticato, immettere il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="1fb88-203">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="1fb88-204">Fornire le credenziali dell'insieme di credenziali scaricato hello</span><span class="sxs-lookup"><span data-stu-id="1fb88-204">Provide hello downloaded vault credentials</span></span>
   * <span data-ttu-id="1fb88-205">Salvare la passphrase di crittografia hello in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="1fb88-205">Save hello encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="1fb88-206">Se si perde o dimentica passphrase hello, Microsoft non consente di ripristinare i dati di backup hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-206">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="1fb88-207">Salvare il file hello in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="1fb88-207">Save hello file in a secure location.</span></span> <span data-ttu-id="1fb88-208">È necessario toorestore una copia di backup.</span><span class="sxs-lookup"><span data-stu-id="1fb88-208">It is required toorestore a backup.</span></span>
     >
     >

<span data-ttu-id="1fb88-209">agente Hello è ora installato e il computer è registrato toohello insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="1fb88-209">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="1fb88-210">È possibile tooconfigure e pianificare il backup.</span><span class="sxs-lookup"><span data-stu-id="1fb88-210">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="1fb88-211">Requisiti di rete e connettività</span><span class="sxs-lookup"><span data-stu-id="1fb88-211">Network and Connectivity Requirements</span></span>

<span data-ttu-id="1fb88-212">Se il computer/proxy ha limitato l'accesso a internet, assicurarsi che le impostazioni del firewall su hello mcahine/proxy siano configurati tooallow hello URL seguenti:</span><span class="sxs-lookup"><span data-stu-id="1fb88-212">If your machine/proxy has limited internet access, ensure that firewall settings on hello mcahine/proxy are configured tooallow hello following URLs:</span></span> <br>
    1. <span data-ttu-id="1fb88-213">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="1fb88-213">www.msftncsi.com</span></span>
    2. <span data-ttu-id="1fb88-214">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="1fb88-214">*.Microsoft.com</span></span>
    3. <span data-ttu-id="1fb88-215">windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="1fb88-215">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="1fb88-216">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="1fb88-216">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="1fb88-217">*. windows.ne</span><span class="sxs-lookup"><span data-stu-id="1fb88-217">*.windows.ne</span></span>

## <a name="back-up-your-files-and-folders"></a><span data-ttu-id="1fb88-218">Eseguire il backup di file e cartelle</span><span class="sxs-lookup"><span data-stu-id="1fb88-218">Back up your files and folders</span></span>
<span data-ttu-id="1fb88-219">backup iniziale Hello include due attività principali:</span><span class="sxs-lookup"><span data-stu-id="1fb88-219">hello initial backup includes two key tasks:</span></span>

* <span data-ttu-id="1fb88-220">Pianifica backup hello</span><span class="sxs-lookup"><span data-stu-id="1fb88-220">Schedule hello backup</span></span>
* <span data-ttu-id="1fb88-221">Eseguire il backup di file e cartelle per hello prima volta</span><span class="sxs-lookup"><span data-stu-id="1fb88-221">Back up files and folders for hello first time</span></span>

<span data-ttu-id="1fb88-222">toocomplete hello primo backup, agente di servizi di ripristino di Microsoft Azure Usa hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-222">toocomplete hello initial backup, use hello Microsoft Azure Recovery Services agent.</span></span>

### <a name="tooschedule-hello-backup-job"></a><span data-ttu-id="1fb88-223">processo di backup hello tooschedule</span><span class="sxs-lookup"><span data-stu-id="1fb88-223">tooschedule hello backup job</span></span>
1. <span data-ttu-id="1fb88-224">Aprire l'agente di servizi di ripristino di Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-224">Open hello Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="1fb88-225">È possibile trovarlo se si cerca **Backup di Microsoft Azure**nel computer.</span><span class="sxs-lookup"><span data-stu-id="1fb88-225">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Avviare l'agente di servizi di ripristino di Azure hello](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)
2. <span data-ttu-id="1fb88-227">Nell'agente di servizi di ripristino hello, fare clic su **pianifica Backup**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-227">In hello Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)
3. <span data-ttu-id="1fb88-229">Pagina di pianificazione guidata Backup hello introduzione su hello, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-229">On hello Getting started page of hello Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="1fb88-230">Nella pagina di tooBackup selezionare elementi hello, fare clic su **Aggiungi elementi**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-230">On hello Select Items tooBackup page, click **Add Items**.</span></span>
5. <span data-ttu-id="1fb88-231">Selezionare le cartelle che si desidera tooback e quindi fare clic su file hello **OK**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-231">Select hello files and folders that you want tooback up, and then click **Okay**.</span></span>
6. <span data-ttu-id="1fb88-232">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-232">Click **Next**.</span></span>
7. <span data-ttu-id="1fb88-233">In hello **specificare pianificazione Backup** specificare hello **pianificazione del backup** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-233">On hello **Specify Backup Schedule** page, specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="1fb88-234">È possibile pianificare backup giornalieri, da eseguire non più di tre volte al giorno, o settimanali.</span><span class="sxs-lookup"><span data-stu-id="1fb88-234">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Elementi per il backup di Windows Server](./media/backup-try-azure-backup-in-10-mins/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="1fb88-236">Per ulteriori informazioni su come toospecify hello pianificazione del backup, vedere l'articolo hello [tooreplace utilizzare Azure Backup infrastruttura nastro](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="1fb88-236">For more information about how toospecify hello backup schedule, see hello article [Use Azure Backup tooreplace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

8. <span data-ttu-id="1fb88-237">In hello **selezionare criteri di conservazione** pagina, seleziona hello **criteri di conservazione** hello copia di backup.</span><span class="sxs-lookup"><span data-stu-id="1fb88-237">On hello **Select Retention Policy** page, select hello **Retention Policy** for hello backup copy.</span></span>

    <span data-ttu-id="1fb88-238">criteri di conservazione Hello specificano quanto tempo hello backup vengono archiviati.</span><span class="sxs-lookup"><span data-stu-id="1fb88-238">hello retention policy specifies how long hello backup data is stored.</span></span> <span data-ttu-id="1fb88-239">Anziché specificare un criterio"semplice" per tutti i punti di backup, è possibile specificare i criteri di conservazione diversi in base a quando viene eseguito il backup di hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-239">Rather than specifying a “flat policy” for all backup points, you can specify different retention policies based on when hello backup occurs.</span></span> <span data-ttu-id="1fb88-240">È possibile modificare toomeet criteri di conservazione giornaliero, settimanale, mensile e annuale hello le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="1fb88-240">You can modify hello daily, weekly, monthly, and yearly retention policies toomeet your needs.</span></span>
9. <span data-ttu-id="1fb88-241">Nella pagina tipo di Backup iniziale scegliere hello, scegliere il tipo di backup iniziale di hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-241">On hello Choose Initial Backup Type page, choose hello initial backup type.</span></span> <span data-ttu-id="1fb88-242">Lasciare l'opzione hello **automaticamente tramite rete hello** selezionata e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-242">Leave hello option **Automatically over hello network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="1fb88-243">È possibile eseguire il backup automaticamente tramite rete hello oppure è possibile eseguire il backup non in linea.</span><span class="sxs-lookup"><span data-stu-id="1fb88-243">You can back up automatically over hello network, or you can back up offline.</span></span> <span data-ttu-id="1fb88-244">resto Hello di questo articolo descrive il processo di hello per il backup automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1fb88-244">hello remainder of this article describes hello process for backing up automatically.</span></span> <span data-ttu-id="1fb88-245">Se si preferisce toodo un backup offline, vedere l'articolo di hello [Offline backup flusso di lavoro in Backup di Azure](backup-azure-backup-import-export.md) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="1fb88-245">If you prefer toodo an offline backup, review hello article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="1fb88-246">Nella pagina di conferma hello, esaminare le informazioni di hello e quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-246">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>
11. <span data-ttu-id="1fb88-247">Al termine la procedura guidata hello creazione pianificazione backup hello, fare clic su **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-247">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a><span data-ttu-id="1fb88-248">tooback backup di file e cartelle per la prima volta hello</span><span class="sxs-lookup"><span data-stu-id="1fb88-248">tooback up files and folders for hello first time</span></span>
1. <span data-ttu-id="1fb88-249">Nell'agente di servizi di ripristino hello, fare clic su **Effettua backup** hello toocomplete iniziale tramite rete hello il seeding.</span><span class="sxs-lookup"><span data-stu-id="1fb88-249">In hello Recovery Services agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Eseguire ora il backup di Windows Server](./media/backup-try-azure-backup-in-10-mins/backup-now.png)
2. <span data-ttu-id="1fb88-251">Nella pagina di conferma hello, rivedere le impostazioni di hello che hello backup guidato immediato utilizzerà tooback macchina hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-251">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="1fb88-252">Fare clic su **Backup**.</span><span class="sxs-lookup"><span data-stu-id="1fb88-252">Then click **Back Up**.</span></span>
3. <span data-ttu-id="1fb88-253">Fare clic su **Chiudi** guidata hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="1fb88-253">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="1fb88-254">Se si chiude la procedura guidata hello prima al termine del processo di backup hello, toorun guidata hello continua in background hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-254">If you close hello wizard before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

<span data-ttu-id="1fb88-255">Al termine dell'operazione backup iniziale hello, hello **processo completato** stato viene visualizzato nella console Backup hello.</span><span class="sxs-lookup"><span data-stu-id="1fb88-255">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

![Completamento infrarossi](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="1fb88-257">Domande?</span><span class="sxs-lookup"><span data-stu-id="1fb88-257">Questions?</span></span>
<span data-ttu-id="1fb88-258">Se si hanno domande o se è presente una funzionalità che si desidera toosee incluso, [inviare commenti e suggerimenti](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="1fb88-258">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1fb88-259">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1fb88-259">Next steps</span></span>
* <span data-ttu-id="1fb88-260">Sono disponibili altre informazioni sul [backup di computer Windows](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="1fb88-260">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="1fb88-261">Ora che si è eseguito il backup dei file e delle cartelle, è possibile [gestire l'insieme di credenziali e i server](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="1fb88-261">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="1fb88-262">Se è necessario toorestore una copia di backup, utilizzare anche in questo articolo[ripristinare i file tooa Windows macchina](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="1fb88-262">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
