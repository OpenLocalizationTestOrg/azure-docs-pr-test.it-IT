---
title: aaaBack backup tooAzure lo stato del sistema di Windows | Documenti Microsoft
description: Informazioni su tooback backup dello stato del sistema di Windows Server e/o tooAzure computer Windows hello.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: "modalità toobackup; modalità tooback; backup di file e cartelle"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: be5d4be81af981c10de82add9fe962a730753cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a><span data-ttu-id="25eac-104">Eseguire il backup dello stato del sistema Windows in una distribuzione Resource Manager</span><span class="sxs-lookup"><span data-stu-id="25eac-104">Back up Windows system state in Resource Manager deployment</span></span>
<span data-ttu-id="25eac-105">Questo articolo illustra la modalità di stato tooAzure tooback il sistema di Windows Server.</span><span class="sxs-lookup"><span data-stu-id="25eac-105">This article explains how tooback up your Windows Server system state tooAzure.</span></span> <span data-ttu-id="25eac-106">Si tratta di un'esercitazione toowalk previsto di nozioni di base hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-106">It's a tutorial intended toowalk you through hello basics.</span></span>

<span data-ttu-id="25eac-107">Se si desidera tooknow ulteriori informazioni su Backup di Azure, leggere questo [Panoramica](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="25eac-107">If you want tooknow more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="25eac-108">Se non è disponibile una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/) che consente di accedere a qualsiasi servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="25eac-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="25eac-109">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="25eac-109">Create a recovery services vault</span></span>
<span data-ttu-id="25eac-110">tooback backup di file e cartelle, è necessario un insieme di credenziali di servizi di ripristino nell'area di hello in cui si desidera dati hello toostore toocreate.</span><span class="sxs-lookup"><span data-stu-id="25eac-110">tooback up your files and folders, you need toocreate a Recovery Services vault in hello region where you want toostore hello data.</span></span> <span data-ttu-id="25eac-111">È inoltre necessario toodetermine la modalità di archiviazione replicata.</span><span class="sxs-lookup"><span data-stu-id="25eac-111">You also need toodetermine how you want your storage replicated.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="25eac-112">toocreate un insieme di credenziali di servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="25eac-112">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="25eac-113">Se non già stato fatto, accedere toohello [portale Azure](https://portal.azure.com/) tramite la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="25eac-113">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="25eac-114">Nel menu Hub hello, fare clic su **più servizi** e nell'elenco di hello delle risorse, digitare **servizi di ripristino** e fare clic su **insiemi di credenziali di servizi di ripristino**.</span><span class="sxs-lookup"><span data-stu-id="25eac-114">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="25eac-116">Se sono presenti archivi di servizi di ripristino nella sottoscrizione hello, vengono elencati gli insiemi di credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-116">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>
3. <span data-ttu-id="25eac-117">In hello **insiemi di credenziali di servizi di ripristino** menu, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="25eac-117">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="25eac-119">Servizi di ripristino Hello insieme di credenziali si apre Pannello chiesto tooprovide un **nome**, **sottoscrizione**, **gruppo di risorse**, e **percorso**.</span><span class="sxs-lookup"><span data-stu-id="25eac-119">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="25eac-121">Per **nome**, immettere un insieme di credenziali di nome descrittivo tooidentify hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-121">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="25eac-122">nome di Hello deve toobe univoco per la sottoscrizione di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-122">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="25eac-123">Digitare un nome che contenga tra i 2 e i 50 caratteri.</span><span class="sxs-lookup"><span data-stu-id="25eac-123">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="25eac-124">Deve iniziare con una lettera e può contenere solo lettere, numeri e trattini.</span><span class="sxs-lookup"><span data-stu-id="25eac-124">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="25eac-125">In hello **sottoscrizione** sezione, utilizzare hello toochoose di menu a discesa hello sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="25eac-125">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="25eac-126">Se si utilizza una sola sottoscrizione, che viene visualizzato di sottoscrizione ed è possibile ignorare toohello successivo passaggio.</span><span class="sxs-lookup"><span data-stu-id="25eac-126">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="25eac-127">Se non sei sicuro che toouse di sottoscrizione, utilizzare predefinito hello (o suggerito) sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="25eac-127">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="25eac-128">Sono disponibili più scelte solo se l'account dell'organizzazione è associato a più sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="25eac-128">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="25eac-129">In hello **gruppo di risorse** sezione:</span><span class="sxs-lookup"><span data-stu-id="25eac-129">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="25eac-130">Selezionare **Crea nuovo** se si desidera toocreate un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="25eac-130">select **Create new** if you want toocreate a Resource group.</span></span>
    <span data-ttu-id="25eac-131">Or</span><span class="sxs-lookup"><span data-stu-id="25eac-131">Or</span></span>
    * <span data-ttu-id="25eac-132">Selezionare **utilizzare esistente** e fare clic su hello dal menu a discesa toosee hello disponibili elenco di gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="25eac-132">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="25eac-133">Per informazioni complete su gruppi di risorse, vedere hello [Panoramica di gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="25eac-133">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="25eac-134">Fare clic su **percorso** tooselect hello località geografica per l'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-134">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="25eac-135">Questa opzione determina l'area geografica di hello in cui viene inviati ai dati di backup.</span><span class="sxs-lookup"><span data-stu-id="25eac-135">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="25eac-136">Nella parte inferiore di hello del pannello dell'insieme di credenziali di servizi di ripristino hello, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="25eac-136">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="25eac-137">Può richiedere alcuni minuti per hello che toobe creato insieme di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="25eac-137">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="25eac-138">Monitorare le notifiche di stato hello in area destra superiore hello del portale hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-138">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="25eac-139">Una volta creato l'insieme di credenziali, viene visualizzato nell'elenco hello degli insiemi di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="25eac-139">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="25eac-140">Se l'insieme di credenziali non viene visualizzato dopo qualche minuto, fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="25eac-140">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Fare clic sul pulsante Aggiorna](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="25eac-142">Dopo aver visualizzato l'insieme di credenziali nell'elenco di hello degli insiemi di credenziali di servizi di ripristino, si è pronti tooset ridondanza dell'archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-142">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-hello-vault"></a><span data-ttu-id="25eac-143">Impostare la ridondanza di archiviazione per l'insieme di credenziali hello</span><span class="sxs-lookup"><span data-stu-id="25eac-143">Set storage redundancy for hello vault</span></span>
<span data-ttu-id="25eac-144">Quando si crea un insieme di credenziali di servizi di ripristino, verificare che la ridondanza dell'archiviazione è configurata hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="25eac-144">When you create a Recovery Services vault, make sure storage redundancy is configured hello way you want.</span></span>

1. <span data-ttu-id="25eac-145">Da hello **insiemi di credenziali di servizi di ripristino** pannello, fare clic su nuovo insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-145">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Selezionare nuovo insieme di credenziali hello hello elenco dell'insieme di credenziali di servizi di ripristino](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="25eac-147">Quando si seleziona l'insieme di credenziali hello, hello **insieme di credenziali di servizi di ripristino** consente di restringere blade e pannello impostazioni hello (*che ha il nome di hello dell'insieme di credenziali hello nella parte superiore di hello*) e pannello Dettagli insieme di credenziali hello aperto.</span><span class="sxs-lookup"><span data-stu-id="25eac-147">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Configurazione dell'archiviazione hello vista per nuovo insieme di credenziali](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="25eac-149">Nel pannello impostazioni di hello nuovo insieme di credenziali, utilizzare hello tooscroll di scorrimento verticale verso il basso toohello sezione gestione e fare clic su **infrastruttura Backup**.</span><span class="sxs-lookup"><span data-stu-id="25eac-149">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="25eac-150">verrà visualizzata la finestra di blade Backup infrastruttura Hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-150">hello Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="25eac-151">Nel Pannello di hello infrastruttura di Backup, fare clic su **la configurazione del Backup** tooopen hello **la configurazione del Backup** blade.</span><span class="sxs-lookup"><span data-stu-id="25eac-151">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

    ![Set di configurazione dell'archiviazione hello per nuovo insieme di credenziali](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="25eac-153">Scegliere l'opzione di replica di archiviazione appropriato hello per l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="25eac-153">Choose hello appropriate storage replication option for your vault.</span></span>

    ![opzioni di configurazione dell'archiviazione](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="25eac-155">Per impostazione predefinita, l'insieme di credenziali prevede l'archiviazione con ridondanza geografica.</span><span class="sxs-lookup"><span data-stu-id="25eac-155">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="25eac-156">Se si usa Azure come un endpoint di archiviazione di backup primario, continuare toouse **con ridondanza geografica**.</span><span class="sxs-lookup"><span data-stu-id="25eac-156">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="25eac-157">Se non si utilizza Azure come un endpoint di archiviazione di backup primario, quindi scegliere **ridondanza locale**, che consente di ridurre i costi di archiviazione di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-157">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="25eac-158">Per altre informazioni sulle opzioni di archiviazione [con ridondanza geografica](../storage/common/storage-redundancy.md#geo-redundant-storage) e [con ridondanza locale](../storage/common/storage-redundancy.md#locally-redundant-storage), vedere [Panoramica della ridondanza di archiviazione](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="25eac-158">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="25eac-159">Dopo aver creato un insieme di credenziali, configurarlo per il backup dello stato del sistema Windows.</span><span class="sxs-lookup"><span data-stu-id="25eac-159">Now that you've created a vault, configure it for backing up Windows System State.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="25eac-160">Configurare l'insieme di credenziali hello</span><span class="sxs-lookup"><span data-stu-id="25eac-160">Configure hello vault</span></span>
1. <span data-ttu-id="25eac-161">In hello pannello dell'insieme di credenziali di servizi di ripristino (per hello insieme di credenziali appena creato), nella sezione Guida introduttiva hello, fare clic su **Backup**, quindi su hello **Introduzione a Backup** pannello seleziona  **Obiettivo di backup**.</span><span class="sxs-lookup"><span data-stu-id="25eac-161">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Aprire il Pannello Obiettivo di backup](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="25eac-163">Hello **Backup obiettivo** apre blade.</span><span class="sxs-lookup"><span data-stu-id="25eac-163">hello **Backup Goal** blade opens.</span></span>

    ![Aprire il Pannello Obiettivo di backup](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="25eac-165">Da hello **in cui viene eseguito il carico di lavoro?** menu a discesa, seleziona **locale**.</span><span class="sxs-lookup"><span data-stu-id="25eac-165">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="25eac-166">Si sceglie **Locale** perché il server di Windows o il computer Windows è un computer fisico che non si trova in Azure.</span><span class="sxs-lookup"><span data-stu-id="25eac-166">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="25eac-167">Da hello **cosa si desidera toobackup?** dal menu **dello stato del sistema**, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="25eac-167">From hello **What do you want toobackup?** menu, select **System State**, and click **OK**.</span></span>

    ![Configurazione di file e cartelle](./media/backup-azure-system-state/backup-goal-system-state.png)

    <span data-ttu-id="25eac-169">Fare clic su OK, un segno di spunta accanto troppo**obiettivo Backup**, hello e **Prepare infrastruttura** apre blade.</span><span class="sxs-lookup"><span data-stu-id="25eac-169">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

    ![Preparare l'infrastruttura dopo aver configurato l'obiettivo del backup](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="25eac-171">In hello **Prepare infrastruttura** pannello, fare clic su **Scarica agente per Windows Server o Client Windows**.</span><span class="sxs-lookup"><span data-stu-id="25eac-171">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![Preparare l'infrastruttura](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="25eac-173">Se si utilizza Windows Server essenziali, quindi scegliere agente hello toodownload per Windows Server essenziali.</span><span class="sxs-lookup"><span data-stu-id="25eac-173">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="25eac-174">Un menu a comparsa chiede toorun o salvare MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="25eac-174">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

    ![Finestra di dialogo di MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="25eac-176">Nel menu a comparsa download hello, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="25eac-176">In hello download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="25eac-177">Per impostazione predefinita, hello **MARSagentinstaller.exe** tooyour cartella di download viene salvato.</span><span class="sxs-lookup"><span data-stu-id="25eac-177">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="25eac-178">Al termine dell'installazione guidata di hello, verrà visualizzato un messaggio popup che chiede se si desidera che il programma di installazione di toorun hello o aprire la cartella hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-178">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

    ![Preparare l'infrastruttura](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="25eac-180">È necessario ancora agente hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="25eac-180">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="25eac-181">È possibile installare l'agente di hello dopo avere scaricato l'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-181">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="25eac-182">In hello **Prepare infrastruttura** pannello, fare clic su **scaricare**.</span><span class="sxs-lookup"><span data-stu-id="25eac-182">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

    ![Scaricare le credenziali dell'insieme di credenziali](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="25eac-184">insieme di credenziali Hello scaricare tooyour cartella di download.</span><span class="sxs-lookup"><span data-stu-id="25eac-184">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="25eac-185">Dopo l'insieme di credenziali hello completare il download, vengono visualizzati una finestra popup che chiede se si desidera tooopen o salvare le credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-185">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="25eac-186">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="25eac-186">Click **Save**.</span></span> <span data-ttu-id="25eac-187">Se si sceglie accidentalmente **aprire**, consentono di finestra di dialogo hello tenta tooopen hello insieme di credenziali, l'esito negativo.</span><span class="sxs-lookup"><span data-stu-id="25eac-187">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="25eac-188">È possibile aprire l'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-188">You cannot open hello vault credentials.</span></span> <span data-ttu-id="25eac-189">Passaggio successivo toohello di procedere.</span><span class="sxs-lookup"><span data-stu-id="25eac-189">Proceed toohello next step.</span></span> <span data-ttu-id="25eac-190">insieme di credenziali Hello sono nella cartella di download di hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-190">hello vault credentials are in hello Downloads folder.</span></span>   

    ![Il download delle credenziali dell'insieme di credenziali è terminato](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="25eac-192">Installare e registrare agente hello</span><span class="sxs-lookup"><span data-stu-id="25eac-192">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="25eac-193">Non è ancora disponibile, l'abilitazione backup tramite il portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-193">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="25eac-194">Utilizzare hello tooback di agente servizi di ripristino di Microsoft Azure backup dello stato di sistema di Windows Server.</span><span class="sxs-lookup"><span data-stu-id="25eac-194">Use hello Microsoft Azure Recovery Services Agent tooback up Windows Server System State.</span></span>
>

1. <span data-ttu-id="25eac-195">Individuare e fare doppio clic su hello **MARSagentinstaller.exe** dalla cartella download di hello (o altro percorso di salvataggio).</span><span class="sxs-lookup"><span data-stu-id="25eac-195">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="25eac-196">programma di installazione Hello fornisce una serie di messaggi durante l'estrazione, installa e registra l'agente di servizi di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-196">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

    ![Eseguire il programma di installazione dell'agente di Servizi di ripristino](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="25eac-198">Completare l'installazione guidata di Microsoft Azure Recovery Services Agent hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-198">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="25eac-199">procedura guidata hello toocomplete, è necessario:</span><span class="sxs-lookup"><span data-stu-id="25eac-199">toocomplete hello wizard, you need to:</span></span>

   * <span data-ttu-id="25eac-200">Scegliere il percorso della cartella di installazione e la cache di hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-200">Choose a location for hello installation and cache folder.</span></span>
   * <span data-ttu-id="25eac-201">Fornire il proprio proxy informazioni sul server se si utilizza un toohello tooconnect di server proxy internet.</span><span class="sxs-lookup"><span data-stu-id="25eac-201">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
   * <span data-ttu-id="25eac-202">Se si usa un proxy autenticato, immettere il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="25eac-202">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="25eac-203">Fornire le credenziali dell'insieme di credenziali scaricato hello</span><span class="sxs-lookup"><span data-stu-id="25eac-203">Provide hello downloaded vault credentials</span></span>
   * <span data-ttu-id="25eac-204">Salvare la passphrase di crittografia hello in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="25eac-204">Save hello encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="25eac-205">Se si perde o dimentica passphrase hello, Microsoft non consente di ripristinare i dati di backup hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-205">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="25eac-206">Salvare il file hello in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="25eac-206">Save hello file in a secure location.</span></span> <span data-ttu-id="25eac-207">È necessario toorestore una copia di backup.</span><span class="sxs-lookup"><span data-stu-id="25eac-207">It is required toorestore a backup.</span></span>
     >
     >

<span data-ttu-id="25eac-208">agente Hello è ora installato e il computer è registrato toohello insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="25eac-208">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="25eac-209">È possibile tooconfigure e pianificare il backup.</span><span class="sxs-lookup"><span data-stu-id="25eac-209">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="back-up-windows-server-system-state-preview"></a><span data-ttu-id="25eac-210">Eseguire il backup dello stato del sistema Windows Server (anteprima)</span><span class="sxs-lookup"><span data-stu-id="25eac-210">Back up Windows Server System State (Preview)</span></span>
<span data-ttu-id="25eac-211">backup iniziale Hello include tre attività:</span><span class="sxs-lookup"><span data-stu-id="25eac-211">hello initial backup includes three tasks:</span></span>

* <span data-ttu-id="25eac-212">Abilitare i Backup dello stato del sistema tramite hello Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="25eac-212">Enable System State Backup using hello Azure Backup agent</span></span>
* <span data-ttu-id="25eac-213">Pianifica backup hello</span><span class="sxs-lookup"><span data-stu-id="25eac-213">Schedule hello backup</span></span>
* <span data-ttu-id="25eac-214">Eseguire il backup di file e cartelle per hello prima volta</span><span class="sxs-lookup"><span data-stu-id="25eac-214">Back up files and folders for hello first time</span></span>

<span data-ttu-id="25eac-215">toocomplete hello primo backup, agente di servizi di ripristino di Microsoft Azure Usa hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-215">toocomplete hello initial backup, use hello Microsoft Azure Recovery Services agent.</span></span>

### <a name="tooenable-system-state-backup-using-hello-azure-backup-agent"></a><span data-ttu-id="25eac-216">backup dello stato del sistema tooenable utilizzando hello Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="25eac-216">tooenable System State backup using hello Azure Backup agent</span></span>

1. <span data-ttu-id="25eac-217">In una sessione di PowerShell, eseguire hello seguente motore di comando toostop hello Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="25eac-217">In a PowerShell session, run hello following command toostop hello Azure Backup engine.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="25eac-218">Aprire hello del Registro di sistema di Windows.</span><span class="sxs-lookup"><span data-stu-id="25eac-218">Open hello Windows Registry.</span></span>

  ```
  PS C:\> regedit.exe
  ```

3. <span data-ttu-id="25eac-219">Aggiungere la seguente chiave del Registro di sistema con hello hello specificato valore DWord.</span><span class="sxs-lookup"><span data-stu-id="25eac-219">Add hello following registry key with hello specified DWord Value.</span></span>

  | <span data-ttu-id="25eac-220">Percorso del Registro</span><span class="sxs-lookup"><span data-stu-id="25eac-220">Registry path</span></span> | <span data-ttu-id="25eac-221">Chiave del Registro di sistema</span><span class="sxs-lookup"><span data-stu-id="25eac-221">Registry key</span></span> | <span data-ttu-id="25eac-222">Valore DWORD</span><span class="sxs-lookup"><span data-stu-id="25eac-222">DWord value</span></span> |
  |---------------|--------------|-------------|
  | <span data-ttu-id="25eac-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="25eac-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="25eac-224">TurnOffSSBFeature</span><span class="sxs-lookup"><span data-stu-id="25eac-224">TurnOffSSBFeature</span></span> | <span data-ttu-id="25eac-225">2</span><span class="sxs-lookup"><span data-stu-id="25eac-225">2</span></span> |

4. <span data-ttu-id="25eac-226">Riavviare il motore di Backup hello eseguendo hello seguente comando in un prompt dei comandi con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="25eac-226">Restart hello Backup engine by executing hello following command in an elevated command prompt.</span></span>

  ```
  PS C:\> Net start obengine
  ```

### <a name="tooschedule-hello-backup-job"></a><span data-ttu-id="25eac-227">processo di backup hello tooschedule</span><span class="sxs-lookup"><span data-stu-id="25eac-227">tooschedule hello backup job</span></span>

1. <span data-ttu-id="25eac-228">Aprire l'agente di servizi di ripristino di Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-228">Open hello Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="25eac-229">È possibile trovarlo se si cerca **Backup di Microsoft Azure**nel computer.</span><span class="sxs-lookup"><span data-stu-id="25eac-229">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Avviare l'agente di servizi di ripristino di Azure hello](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. <span data-ttu-id="25eac-231">Nell'agente di servizi di ripristino hello, fare clic su **pianifica Backup**.</span><span class="sxs-lookup"><span data-stu-id="25eac-231">In hello Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. <span data-ttu-id="25eac-233">Pagina di pianificazione guidata Backup hello introduzione su hello, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="25eac-233">On hello Getting started page of hello Schedule Backup Wizard, click **Next**.</span></span>

4. <span data-ttu-id="25eac-234">Nella pagina di tooBackup selezionare elementi hello, fare clic su **Aggiungi elementi**.</span><span class="sxs-lookup"><span data-stu-id="25eac-234">On hello Select Items tooBackup page, click **Add Items**.</span></span>

5. <span data-ttu-id="25eac-235">Selezionare **Stato del sistema** e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="25eac-235">Select **System State** and then click **OK**.</span></span>

6. <span data-ttu-id="25eac-236">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="25eac-236">Click **Next**.</span></span>

7. <span data-ttu-id="25eac-237">Hello pianificazione di Backup dello stato del sistema e alla conservazione dei verrà automaticamente impostata tooback backup ogni domenica ora locale 9:00 PM, e il periodo di conservazione hello è too60 giorni.</span><span class="sxs-lookup"><span data-stu-id="25eac-237">hello System State Backup and Retention schedule is automatically set tooback up every Sunday at 9:00 PM local time, and hello retention period is set too60 days.</span></span>

   > [!NOTE]
   > <span data-ttu-id="25eac-238">I criteri di backup e di conservazione dello stato del sistema vengono configurati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="25eac-238">System State backup and retention policy is automatically configured.</span></span> <span data-ttu-id="25eac-239">Se si esegue il backup di file e cartelle inoltre toohello dello stato del sistema Windows Server, specificare solo hello Backup e criteri di memorizzazione per i backup di file dalla procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-239">If you back up Files and Folders in addition toohello Windows Server System State, specify only hello Backup and Retention policy for file backups from hello wizard.</span></span> 
   >

8. <span data-ttu-id="25eac-240">Nella pagina di conferma hello, esaminare le informazioni di hello e quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="25eac-240">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>

9. <span data-ttu-id="25eac-241">Al termine la procedura guidata hello creazione pianificazione backup hello, fare clic su **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="25eac-241">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="tooback-up-windows-server-system-state-for-hello-first-time"></a><span data-ttu-id="25eac-242">tooback backup dello stato di sistema di Windows Server per la prima volta hello</span><span class="sxs-lookup"><span data-stu-id="25eac-242">tooback up Windows Server System State for hello first time</span></span>

1. <span data-ttu-id="25eac-243">Verificare che non siano presenti aggiornamenti in sospeso di Windows Server che richiedono un riavvio.</span><span class="sxs-lookup"><span data-stu-id="25eac-243">Make sure there are no pending updates for Windows Server that require a reboot.</span></span>

2. <span data-ttu-id="25eac-244">Nell'agente di servizi di ripristino hello, fare clic su **Effettua backup** hello toocomplete iniziale tramite rete hello il seeding.</span><span class="sxs-lookup"><span data-stu-id="25eac-244">In hello Recovery Services agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Eseguire ora il backup di Windows Server](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. <span data-ttu-id="25eac-246">Nella pagina di conferma hello, rivedere le impostazioni di hello che hello backup guidato immediato utilizzerà tooback macchina hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-246">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="25eac-247">Fare clic su **Backup**.</span><span class="sxs-lookup"><span data-stu-id="25eac-247">Then click **Back Up**.</span></span>

4. <span data-ttu-id="25eac-248">Fare clic su **Chiudi** guidata hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="25eac-248">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="25eac-249">Se si chiude la procedura guidata hello prima al termine del processo di backup hello, toorun guidata hello continua in background hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-249">If you close hello wizard before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

5. <span data-ttu-id="25eac-250">Se si esegue il backup di file e cartelle sul server, inoltre toohello dello stato del sistema Server Windows, hello Esegui Backup verrà solo eseguito il backup dei file.</span><span class="sxs-lookup"><span data-stu-id="25eac-250">If you back up Files and Folders on your server, in addition toohello Windows Server System State, hello Backup Now wizard will only back up files.</span></span> <span data-ttu-id="25eac-251">uno stato di sistema ad hoc tooperform eseguire il backup, usare hello comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="25eac-251">tooperform an ad hoc System State back up, use hello following PowerShell command:</span></span>

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  <span data-ttu-id="25eac-252">Al termine dell'operazione backup iniziale hello, hello **processo completato** stato viene visualizzato nella console Backup hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-252">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

  ![Completamento infrarossi](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="25eac-254">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="25eac-254">Frequently asked questions</span></span>

<span data-ttu-id="25eac-255">Hello domande e risposte seguenti forniscono informazioni supplementari.</span><span class="sxs-lookup"><span data-stu-id="25eac-255">hello following questions and answers provide supplementary information.</span></span>

### <a name="what-is-hello-staging-volume"></a><span data-ttu-id="25eac-256">Che cos'è il Volume di gestione temporanea hello?</span><span class="sxs-lookup"><span data-stu-id="25eac-256">What is hello Staging Volume?</span></span>

<span data-ttu-id="25eac-257">Volume di gestione temporanea Hello rappresenta posizione intermedia di hello in hello disponibile in modo nativo, Windows Server Backup fasi hello Backup dello stato del sistema.</span><span class="sxs-lookup"><span data-stu-id="25eac-257">hello Staging Volume represents hello intermediate location where hello natively available, Windows Server Backup stages hello System State Backup.</span></span> <span data-ttu-id="25eac-258">Agente di Backup di Azure quindi comprime e crittografa il backup intermedio e invia che tramite toohello il protocollo HTTPS protetta configurato l'insieme di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="25eac-258">Azure Backup agent then compresses and encrypts this intermediate backup and sends it via secure HTTPS Protocol toohello configured Recovery Services Vault.</span></span> <span data-ttu-id="25eac-259">**È consigliabile che stabilire hello Volume di gestione temporanea in un volume di sistema operativo Windows. Se si osservano problemi con i backup dello stato di sistema, la verifica percorso hello del Volume di gestione temporanea è hello primo passaggio di risoluzione dei problemi.**</span><span class="sxs-lookup"><span data-stu-id="25eac-259">**We strongly recommended you establish hello Staging Volume in a non-Windows-OS volume. If you observe problems with System State Backups, checking hello location of your Staging Volume is hello first troubleshooting step.**</span></span> 

### <a name="how-can-i-change-hello-staging-volume-path-specified-in-hello-azure-backup-agent"></a><span data-ttu-id="25eac-260">Come è possibile modificare hello percorso del Volume di gestione temporanea specificata nell'agente di Backup di Azure hello?</span><span class="sxs-lookup"><span data-stu-id="25eac-260">How can I change hello Staging Volume Path specified in hello Azure Backup agent?</span></span>

<span data-ttu-id="25eac-261">Per impostazione predefinita, Hello Volume di gestione temporanea si trova nella cartella della cache di hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-261">hello Staging Volume is located in hello cache folder by default.</span></span> 

1. <span data-ttu-id="25eac-262">toochange questo percorso, utilizzare hello comando (in un prompt dei comandi con privilegi elevati) seguente:</span><span class="sxs-lookup"><span data-stu-id="25eac-262">toochange this location, use hello following command (in an elevated command prompt):</span></span>
  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="25eac-263">Aggiornare quindi hello seguenti voci del registro con hello percorso toohello nuova Volume di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="25eac-263">Then update hello following registry entries with hello path toohello new Staging Volume folder.</span></span>

  |<span data-ttu-id="25eac-264">Percorso del Registro</span><span class="sxs-lookup"><span data-stu-id="25eac-264">Registry path</span></span>|<span data-ttu-id="25eac-265">Chiave del Registro di sistema</span><span class="sxs-lookup"><span data-stu-id="25eac-265">Registry key</span></span>|<span data-ttu-id="25eac-266">Valore</span><span class="sxs-lookup"><span data-stu-id="25eac-266">Value</span></span>|
  |-------------|------------|-----|
  |<span data-ttu-id="25eac-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="25eac-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="25eac-268">SSBStagingPath</span><span class="sxs-lookup"><span data-stu-id="25eac-268">SSBStagingPath</span></span> | <span data-ttu-id="25eac-269">Nuovo percorso del volume di staging</span><span class="sxs-lookup"><span data-stu-id="25eac-269">new staging volume location</span></span> |

<span data-ttu-id="25eac-270">Hello percorso gestione temporanea viene fatta distinzione tra maiuscole e minuscole e deve essere hello esatta stesso maiuscole e minuscole come ciò che esiste nel server di hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-270">hello Staging Path is case sensitive and must be hello exact same casing as what exists on hello server.</span></span> 

3. <span data-ttu-id="25eac-271">Dopo aver modificato percorso del volume di gestione temporanea hello, riavviare il motore di Backup hello:</span><span class="sxs-lookup"><span data-stu-id="25eac-271">Once you change hello Staging volume path, restart hello Backup engine:</span></span>
  ```
  PS C:\> Net start obengine
  ```
4. <span data-ttu-id="25eac-272">toopick percorso hello modificato, agente di servizi di ripristino di Microsoft Azure aprire hello e trigger di un backup dello stato del sistema ad hoc.</span><span class="sxs-lookup"><span data-stu-id="25eac-272">toopick up hello changed path, open hello Microsoft Azure Recovery Services agent and trigger an ad hoc backup of System State.</span></span>

### <a name="why-is-hello-system-state-default-retention-set-too60-days"></a><span data-ttu-id="25eac-273">Motivo per cui è stato del sistema hello periodo di memorizzazione predefinito impostato too60 giorni?</span><span class="sxs-lookup"><span data-stu-id="25eac-273">Why is hello System State default retention set too60 days?</span></span>

<span data-ttu-id="25eac-274">ciclo di vita utile Hello di un backup dello stato del sistema è hello stesso come impostazione di hello "tombstone lifetime" per il ruolo di Windows Server Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-274">hello useful life of a system state backup is hello same as hello "tombstone lifetime" setting for hello Windows Server Active Directory role.</span></span> <span data-ttu-id="25eac-275">il valore predefinito Hello per la voce di durata oggetto contrassegnato per rimozione hello è 60 giorni.</span><span class="sxs-lookup"><span data-stu-id="25eac-275">hello default value for hello tombstone lifetime entry is 60 days.</span></span> <span data-ttu-id="25eac-276">Questo valore può essere impostato sull'oggetto di configurazione del servizio Directory (NTDS) hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-276">This value can be set on hello Directory Service (NTDS) config object.</span></span>

### <a name="how-do-i-change-hello-default-backup-and-retention-policy-for-system-state"></a><span data-ttu-id="25eac-277">Come modificare predefinito hello Backup e criteri di conservazione per lo stato del sistema?</span><span class="sxs-lookup"><span data-stu-id="25eac-277">How do I change hello default Backup and Retention Policy for System State?</span></span>

<span data-ttu-id="25eac-278">valore predefinito di hello toochange Backup e criteri di conservazione per lo stato del sistema:</span><span class="sxs-lookup"><span data-stu-id="25eac-278">toochange hello default Backup and Retention Policy for System State:</span></span>
1. <span data-ttu-id="25eac-279">Arrestare il motore di Backup hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-279">Stop hello Backup engine.</span></span> <span data-ttu-id="25eac-280">Eseguire hello comando seguente da un prompt dei comandi con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="25eac-280">Run hello following command from an elevated command prompt.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="25eac-281">Aggiungere o aggiornare hello seguenti voci chiave del Registro di sistema HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Backup\Config\CloudBackupProvider di Azure.</span><span class="sxs-lookup"><span data-stu-id="25eac-281">Add or update hello following registry key entries in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.</span></span>

  |<span data-ttu-id="25eac-282">Nome nel Registro di sistema</span><span class="sxs-lookup"><span data-stu-id="25eac-282">Registry Name</span></span>|<span data-ttu-id="25eac-283">Descrizione</span><span class="sxs-lookup"><span data-stu-id="25eac-283">Description</span></span>|<span data-ttu-id="25eac-284">Valore</span><span class="sxs-lookup"><span data-stu-id="25eac-284">Value</span></span>|
  |-------------|-----------|-----|
  |<span data-ttu-id="25eac-285">SSBScheduleTime</span><span class="sxs-lookup"><span data-stu-id="25eac-285">SSBScheduleTime</span></span>|<span data-ttu-id="25eac-286">Tooconfigure usato hello ora del backup hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-286">Used tooconfigure hello time of hello backup.</span></span> <span data-ttu-id="25eac-287">L'impostazione predefinita sono le 21 ora locale.</span><span class="sxs-lookup"><span data-stu-id="25eac-287">Default is 9PM local time.</span></span>|<span data-ttu-id="25eac-288">DWORD: formato HHMM (numero decimale), ad esempio 2130 per le 21:30 ora locale</span><span class="sxs-lookup"><span data-stu-id="25eac-288">DWord: Format HHMM (Decimal) for example 2130 for 9:30PM local time</span></span>|
  |<span data-ttu-id="25eac-289">SSBScheduleDays</span><span class="sxs-lookup"><span data-stu-id="25eac-289">SSBScheduleDays</span></span>|<span data-ttu-id="25eac-290">Giorni di hello tooconfigure utilizzato quando i Backup dello stato del sistema deve essere eseguito a hello specificati ora.</span><span class="sxs-lookup"><span data-stu-id="25eac-290">Used tooconfigure hello days when System State Backup must be performed at hello specified time.</span></span> <span data-ttu-id="25eac-291">Singole cifre specificano i giorni della settimana hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-291">Individual digits specify days of hello week.</span></span> <span data-ttu-id="25eac-292">0 rappresenta domenica, 1 lunedì e così via.</span><span class="sxs-lookup"><span data-stu-id="25eac-292">0 represents Sunday, 1 is Monday, and so on.</span></span> <span data-ttu-id="25eac-293">Il giorno predefinito per il backup è domenica.</span><span class="sxs-lookup"><span data-stu-id="25eac-293">Default day for backup is Sunday.</span></span>|<span data-ttu-id="25eac-294">DWord: giorni di backup di toorun settimana hello (decimale), ad esempio 1230 pianifica backup su lunedì, martedì, mercoledì e domenica.</span><span class="sxs-lookup"><span data-stu-id="25eac-294">DWord: days of hello week toorun backup (decimal) for example 1230 schedules backups on Monday, Tuesday, Wednesday, and Sunday.</span></span>|
  |<span data-ttu-id="25eac-295">SSBRetentionDays</span><span class="sxs-lookup"><span data-stu-id="25eac-295">SSBRetentionDays</span></span>|<span data-ttu-id="25eac-296">Backup di tooretain giorni hello tooconfigure utilizzato.</span><span class="sxs-lookup"><span data-stu-id="25eac-296">Used tooconfigure hello days tooretain backup.</span></span> <span data-ttu-id="25eac-297">Il valore predefinito è 60.</span><span class="sxs-lookup"><span data-stu-id="25eac-297">Default value is 60.</span></span> <span data-ttu-id="25eac-298">Il massimo consentito è 180.</span><span class="sxs-lookup"><span data-stu-id="25eac-298">Maximum allowed value is 180.</span></span>|<span data-ttu-id="25eac-299">DWord: Backup di tooretain giorni (decimale).</span><span class="sxs-lookup"><span data-stu-id="25eac-299">DWord: Days tooretain backup (decimal).</span></span>|

3. <span data-ttu-id="25eac-300">Modulo di backup hello toorestart comando che segue hello di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="25eac-300">Use hello following command toorestart hello backup engine.</span></span>
    ```
    PS C:\> Net start obengine
    ```

4. <span data-ttu-id="25eac-301">Aprire l'agente di servizi di ripristino di Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-301">Open hello Microsoft Recovery Services agent.</span></span>

5. <span data-ttu-id="25eac-302">Fare clic su **pianifica Backup** e quindi fare clic su **Avanti** fino a visualizzare modifiche hello.</span><span class="sxs-lookup"><span data-stu-id="25eac-302">Click **Schedule Backup** and then click **Next** until you see hello changes reflected.</span></span>

6. <span data-ttu-id="25eac-303">Fare clic su **fine** modifiche hello tooapply.</span><span class="sxs-lookup"><span data-stu-id="25eac-303">Click **Finish** tooapply hello changes.</span></span>


## <a name="questions"></a><span data-ttu-id="25eac-304">Domande?</span><span class="sxs-lookup"><span data-stu-id="25eac-304">Questions?</span></span>
<span data-ttu-id="25eac-305">Se si hanno domande o se è presente una funzionalità che si desidera toosee incluso, [inviare commenti e suggerimenti](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="25eac-305">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="25eac-306">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25eac-306">Next steps</span></span>
* <span data-ttu-id="25eac-307">Sono disponibili altre informazioni sul [backup di computer Windows](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="25eac-307">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="25eac-308">Ora che si è eseguito il backup dei file e delle cartelle, è possibile [gestire l'insieme di credenziali e i server](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="25eac-308">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="25eac-309">Se è necessario toorestore una copia di backup, utilizzare anche in questo articolo[ripristinare i file tooa Windows macchina](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="25eac-309">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
