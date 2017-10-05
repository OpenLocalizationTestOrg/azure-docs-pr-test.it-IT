---
title: Eseguire il backup dello stato del sistema Windows in Azure | Microsoft Docs
description: Informazioni su come eseguire il backup dello stato del sistema di computer Windows Server e/o Windows in Azure.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: come eseguire il backup; procedura di backup; backup di file e cartelle
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: 6fbd96935f444d8b0c6d068ebd0d28e612f19816
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a><span data-ttu-id="e01f3-104">Eseguire il backup dello stato del sistema Windows in una distribuzione Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e01f3-104">Back up Windows system state in Resource Manager deployment</span></span>
<span data-ttu-id="e01f3-105">Questo articolo illustra come eseguire il backup dello stato del sistema Windows Server in Azure.</span><span class="sxs-lookup"><span data-stu-id="e01f3-105">This article explains how to back up your Windows Server system state to Azure.</span></span> <span data-ttu-id="e01f3-106">Si tratta di un'esercitazione che illustra le informazioni di base,</span><span class="sxs-lookup"><span data-stu-id="e01f3-106">It's a tutorial intended to walk you through the basics.</span></span>

<span data-ttu-id="e01f3-107">Per altre informazioni su Backup di Azure, vedere questa [panoramica](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="e01f3-107">If you want to know more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="e01f3-108">Se non è disponibile una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/) che consente di accedere a qualsiasi servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="e01f3-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="e01f3-109">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="e01f3-109">Create a recovery services vault</span></span>
<span data-ttu-id="e01f3-110">Per eseguire il backup dei file e delle cartelle, è necessario creare un insieme di credenziali di Servizi di ripristino nell'area in cui archiviare i dati.</span><span class="sxs-lookup"><span data-stu-id="e01f3-110">To back up your files and folders, you need to create a Recovery Services vault in the region where you want to store the data.</span></span> <span data-ttu-id="e01f3-111">È anche necessario determinare la modalità di replica di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e01f3-111">You also need to determine how you want your storage replicated.</span></span>

### <a name="to-create-a-recovery-services-vault"></a><span data-ttu-id="e01f3-112">Per creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="e01f3-112">To create a Recovery Services vault</span></span>
1. <span data-ttu-id="e01f3-113">Se questa operazione non è già stata eseguita, accedere al [portale di Azure](https://portal.azure.com/) , tramite la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e01f3-113">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="e01f3-114">Scegliere **Altri servizi** dal menu Hub e nell'elenco di risorse digitare **Servizi di ripristino**, quindi fare clic su **Insiemi di credenziali dei servizi di ripristino**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-114">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="e01f3-116">Se presenti nella sottoscrizione, gli insiemi di credenziali dei servizi di ripristino vengono elencati.</span><span class="sxs-lookup"><span data-stu-id="e01f3-116">If there are recovery services vaults in the subscription, the vaults are listed.</span></span>
3. <span data-ttu-id="e01f3-117">Scegliere **Aggiungi** dal menu **Insiemi di credenziali dei servizi di ripristino**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-117">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="e01f3-119">Verrà visualizzato il pannello degli insiemi di credenziali dei servizi di ripristino, in cui viene richiesto di specificare **Nome**, **Sottoscrizione**, **Gruppo di risorse** e **Località**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-119">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="e01f3-121">Nel campo **Nome**digitare un nome descrittivo per identificare l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="e01f3-121">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="e01f3-122">Il nome deve essere univoco per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e01f3-122">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="e01f3-123">Digitare un nome che contenga tra i 2 e i 50 caratteri.</span><span class="sxs-lookup"><span data-stu-id="e01f3-123">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="e01f3-124">Deve iniziare con una lettera e può contenere solo lettere, numeri e trattini.</span><span class="sxs-lookup"><span data-stu-id="e01f3-124">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="e01f3-125">Nella sezione **Sottoscrizione** usare il menu a discesa per scegliere la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e01f3-125">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="e01f3-126">Se si usa una sola sottoscrizione, questa verrà visualizzata e sarà possibile andare al passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="e01f3-126">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="e01f3-127">Se non si è certi di quale sottoscrizione usare, usare la sottoscrizione predefinita (o suggerita).</span><span class="sxs-lookup"><span data-stu-id="e01f3-127">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="e01f3-128">Sono disponibili più scelte solo se l'account dell'organizzazione è associato a più sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="e01f3-128">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="e01f3-129">Nella sezione **Gruppo di risorse**:</span><span class="sxs-lookup"><span data-stu-id="e01f3-129">In the **Resource group** section:</span></span>

    * <span data-ttu-id="e01f3-130">Selezionare **Crea nuovo** se si vuole creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e01f3-130">select **Create new** if you want to create a Resource group.</span></span>
    <span data-ttu-id="e01f3-131">Or</span><span class="sxs-lookup"><span data-stu-id="e01f3-131">Or</span></span>
    * <span data-ttu-id="e01f3-132">Selezionare **Usa esistente** e fare clic sul menu a discesa per visualizzare l'elenco di gruppi di risorse disponibili.</span><span class="sxs-lookup"><span data-stu-id="e01f3-132">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="e01f3-133">Per informazioni complete sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e01f3-133">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="e01f3-134">Fare clic su **Località** per selezionare l'area geografica per l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="e01f3-134">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="e01f3-135">La scelta determina l'area geografica in cui vengono inviati i dati di backup.</span><span class="sxs-lookup"><span data-stu-id="e01f3-135">This choice determines the geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="e01f3-136">Nella parte inferiore del pannello Insieme di credenziali dei servizi di ripristino fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-136">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="e01f3-137">La creazione dell'insieme di credenziali dei servizi di ripristino può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="e01f3-137">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="e01f3-138">Monitorare le notifiche di stato nell'area superiore destra del portale.</span><span class="sxs-lookup"><span data-stu-id="e01f3-138">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="e01f3-139">L'insieme di credenziali, dopo essere stato creato, viene visualizzato negli insiemi di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e01f3-139">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="e01f3-140">Se l'insieme di credenziali non viene visualizzato dopo qualche minuto, fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-140">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Fare clic sul pulsante Aggiorna](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="e01f3-142">Dopo la visualizzazione dell'insieme di credenziali nell'elenco corrispondente per i Servizi di ripristino, è possibile configurare la ridondanza di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e01f3-142">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-the-vault"></a><span data-ttu-id="e01f3-143">Impostare la ridondanza di archiviazione dell'insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="e01f3-143">Set storage redundancy for the vault</span></span>
<span data-ttu-id="e01f3-144">Quando si crea un insieme di credenziali dei Servizi di ripristino, assicurarsi che la ridondanza di archiviazione sia configurata in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="e01f3-144">When you create a Recovery Services vault, make sure storage redundancy is configured the way you want.</span></span>

1. <span data-ttu-id="e01f3-145">Nel pannello **Insieme di credenziali dei servizi di ripristino** fare clic sul nuovo insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="e01f3-145">From the **Recovery Services vaults** blade, click the new vault.</span></span>

    ![Selezionare il nuovo insieme di credenziali dall'elenco corrispondente per Servizi di ripristino](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="e01f3-147">Quando si seleziona l'insieme di credenziali, il pannello **Insieme di credenziali dei servizi di ripristino** si restringe e vengono aperti il pannello Impostazioni,*con il nome dell'insieme di credenziali nella parte superiore*, e il pannello dei dettagli dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="e01f3-147">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span></span>

    ![Visualizzare la configurazione dell'archiviazione per il nuovo insieme di credenziali](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="e01f3-149">Nel pannello Impostazioni del nuovo insieme di credenziali usare il dispositivo di scorrimento verticale per passare alla sezione Gestisci e fare clic su **Infrastruttura di backup**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-149">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="e01f3-150">Verrà visualizzato il pannello Infrastruttura di backup.</span><span class="sxs-lookup"><span data-stu-id="e01f3-150">The Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="e01f3-151">Nel pannello Infrastruttura di backup fare clic su **Configurazione backup** per aprire il pannello **Configurazione backup**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-151">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

    ![Impostare la configurazione dell'archiviazione per il nuovo insieme di credenziali](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="e01f3-153">Scegliere l'opzione di replica di archiviazione appropriata per l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="e01f3-153">Choose the appropriate storage replication option for your vault.</span></span>

    ![opzioni di configurazione dell'archiviazione](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="e01f3-155">Per impostazione predefinita, l'insieme di credenziali prevede l'archiviazione con ridondanza geografica.</span><span class="sxs-lookup"><span data-stu-id="e01f3-155">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="e01f3-156">Se si usa Azure come endpoint di archiviazione di backup primario, continuare a usare l'opzione **Con ridondanza geografica**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-156">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="e01f3-157">Se non si usa Azure come endpoint di archiviazione di backup primario, scegliere l'opzione **Con ridondanza locale**, che riduce i costi di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e01f3-157">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="e01f3-158">Per altre informazioni sulle opzioni di archiviazione [con ridondanza geografica](../storage/common/storage-redundancy.md#geo-redundant-storage) e [con ridondanza locale](../storage/common/storage-redundancy.md#locally-redundant-storage), vedere [Panoramica della ridondanza di archiviazione](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="e01f3-158">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="e01f3-159">Dopo aver creato un insieme di credenziali, configurarlo per il backup dello stato del sistema Windows.</span><span class="sxs-lookup"><span data-stu-id="e01f3-159">Now that you've created a vault, configure it for backing up Windows System State.</span></span>

## <a name="configure-the-vault"></a><span data-ttu-id="e01f3-160">Configurare l'insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="e01f3-160">Configure the vault</span></span>
1. <span data-ttu-id="e01f3-161">Nel pannello dell'insieme di credenziali dei servizi di ripristino appena creato, nella sezione Attività iniziali fare clic su **Backup** e nel pannello **Introduzione al backup** selezionare **Obiettivo del backup**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-161">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Aprire il Pannello Obiettivo di backup](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="e01f3-163">Verrà visualizzato il pannello **Obiettivo del backup**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-163">The **Backup Goal** blade opens.</span></span>

    ![Aprire il Pannello Obiettivo di backup](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="e01f3-165">Scegliere **Locale** dal menu a discesa **Posizione di esecuzione del carico di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-165">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="e01f3-166">Si sceglie **Locale** perché il server di Windows o il computer Windows è un computer fisico che non si trova in Azure.</span><span class="sxs-lookup"><span data-stu-id="e01f3-166">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="e01f3-167">Scegliere **Stato del sistema** dal menu **Elementi di cui eseguire il backup** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-167">From the **What do you want to backup?** menu, select **System State**, and click **OK**.</span></span>

    ![Configurazione di file e cartelle](./media/backup-azure-system-state/backup-goal-system-state.png)

    <span data-ttu-id="e01f3-169">Dopo aver fatto clic su OK verrà visualizzato un segno di spunta accanto a **Obiettivo del backup** e si aprirà il pannello **Preparare l'infrastruttura**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-169">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span></span>

    ![Preparare l'infrastruttura dopo aver configurato l'obiettivo del backup](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="e01f3-171">Nel pannello **Preparare l'infrastruttura** fare clic su **Scaricare l'agente per Windows Server o Windows Client**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-171">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![Preparare l'infrastruttura](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="e01f3-173">Se si usa Windows Server Essentials, scegliere di scaricare l'agente per Windows Server Essentials.</span><span class="sxs-lookup"><span data-stu-id="e01f3-173">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span></span> <span data-ttu-id="e01f3-174">Un menu a comparsa chiederà di eseguire o salvare MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="e01f3-174">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span></span>

    ![Finestra di dialogo di MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="e01f3-176">Fare clic su **Salva** nel menu a comparsa del download.</span><span class="sxs-lookup"><span data-stu-id="e01f3-176">In the download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="e01f3-177">Per impostazione predefinita, il file **MARSagentinstaller.exe** viene salvato nella cartella Downloads.</span><span class="sxs-lookup"><span data-stu-id="e01f3-177">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span></span> <span data-ttu-id="e01f3-178">Al termine del programma di installazione verrà visualizzato un messaggio popup che chiede se eseguire il programma di installazione o aprire la cartella.</span><span class="sxs-lookup"><span data-stu-id="e01f3-178">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span></span>

    ![Preparare l'infrastruttura](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="e01f3-180">Non è ancora necessario installare l'agente.</span><span class="sxs-lookup"><span data-stu-id="e01f3-180">You don't need to install the agent yet.</span></span> <span data-ttu-id="e01f3-181">È possibile installare l'agente al termine del download delle credenziali dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="e01f3-181">You can install the agent after you have downloaded the vault credentials.</span></span>

6. <span data-ttu-id="e01f3-182">Fare clic su **Scarica** nel pannello **Preparare l'infrastruttura**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-182">On the **Prepare infrastructure** blade, click **Download**.</span></span>

    ![Scaricare le credenziali dell'insieme di credenziali](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="e01f3-184">Le credenziali dell'insieme di credenziali verranno scaricate nella cartella Download locale.</span><span class="sxs-lookup"><span data-stu-id="e01f3-184">The vault credentials download to your Downloads folder.</span></span> <span data-ttu-id="e01f3-185">Al termine del download delle credenziali dell'insieme di credenziali verrà visualizzato un messaggio popup che chiede se aprire o salvare le credenziali.</span><span class="sxs-lookup"><span data-stu-id="e01f3-185">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span></span> <span data-ttu-id="e01f3-186">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-186">Click **Save**.</span></span> <span data-ttu-id="e01f3-187">Se si fa clic accidentalmente su **Apri**, attendere che il tentativo di apertura delle credenziali termini con un errore.</span><span class="sxs-lookup"><span data-stu-id="e01f3-187">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span></span> <span data-ttu-id="e01f3-188">Non è possibile aprire le credenziali dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="e01f3-188">You cannot open the vault credentials.</span></span> <span data-ttu-id="e01f3-189">Procedere con il passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="e01f3-189">Proceed to the next step.</span></span> <span data-ttu-id="e01f3-190">Le credenziali dell'insieme di credenziali si trovano nella cartella Downloads.</span><span class="sxs-lookup"><span data-stu-id="e01f3-190">The vault credentials are in the Downloads folder.</span></span>   

    ![Il download delle credenziali dell'insieme di credenziali è terminato](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-the-agent"></a><span data-ttu-id="e01f3-192">Installare e registrare l'agente</span><span class="sxs-lookup"><span data-stu-id="e01f3-192">Install and register the agent</span></span>

> [!NOTE]
> <span data-ttu-id="e01f3-193">L'abilitazione del backup tramite il portale di Azure non è ancora disponibile.</span><span class="sxs-lookup"><span data-stu-id="e01f3-193">Enabling backup through the Azure portal is not available, yet.</span></span> <span data-ttu-id="e01f3-194">Usare l'agente di Servizi di ripristino di Microsoft Azure per eseguire il backup dello stato del sistema Windows Server.</span><span class="sxs-lookup"><span data-stu-id="e01f3-194">Use the Microsoft Azure Recovery Services Agent to back up Windows Server System State.</span></span>
>

1. <span data-ttu-id="e01f3-195">Cercare e fare doppio clic sul file **MARSagentinstaller.exe** nella cartella Downloads o nella cartella in cui è stato salvato.</span><span class="sxs-lookup"><span data-stu-id="e01f3-195">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="e01f3-196">Il programma di installazione visualizzerà una serie di messaggi durante l'estrazione, l'installazione e la registrazione dell'agente di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e01f3-196">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span></span>

    ![Eseguire il programma di installazione dell'agente di Servizi di ripristino](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="e01f3-198">Completare l'Installazione guidata di Agente servizi di ripristino di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e01f3-198">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="e01f3-199">Per completare la procedura guidata, è necessario:</span><span class="sxs-lookup"><span data-stu-id="e01f3-199">To complete the wizard, you need to:</span></span>

   * <span data-ttu-id="e01f3-200">Scegliere un percorso per la cartella di installazione e della cache.</span><span class="sxs-lookup"><span data-stu-id="e01f3-200">Choose a location for the installation and cache folder.</span></span>
   * <span data-ttu-id="e01f3-201">Fornire le informazioni sul server proxy se si usa un server proxy per connettersi a Internet.</span><span class="sxs-lookup"><span data-stu-id="e01f3-201">Provide your proxy server info if you use a proxy server to connect to the internet.</span></span>
   * <span data-ttu-id="e01f3-202">Se si usa un proxy autenticato, immettere il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="e01f3-202">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="e01f3-203">Fornire le credenziali dell'insieme di credenziali scaricate.</span><span class="sxs-lookup"><span data-stu-id="e01f3-203">Provide the downloaded vault credentials</span></span>
   * <span data-ttu-id="e01f3-204">Salvare la passphrase di crittografia in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="e01f3-204">Save the encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="e01f3-205">Se la passphrase viene persa o dimenticata, Microsoft non potrà offrire assistenza per il recupero dei dati di backup.</span><span class="sxs-lookup"><span data-stu-id="e01f3-205">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span></span> <span data-ttu-id="e01f3-206">Salvare il file in una posizione sicura.</span><span class="sxs-lookup"><span data-stu-id="e01f3-206">Save the file in a secure location.</span></span> <span data-ttu-id="e01f3-207">È necessario per ripristinare un backup.</span><span class="sxs-lookup"><span data-stu-id="e01f3-207">It is required to restore a backup.</span></span>
     >
     >

<span data-ttu-id="e01f3-208">L'agente ora è installato e il computer è registrato nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="e01f3-208">The agent is now installed and your machine is registered to the vault.</span></span> <span data-ttu-id="e01f3-209">Ora è possibile configurare e pianificare il backup.</span><span class="sxs-lookup"><span data-stu-id="e01f3-209">You're ready to configure and schedule your backup.</span></span>

## <a name="back-up-windows-server-system-state-preview"></a><span data-ttu-id="e01f3-210">Eseguire il backup dello stato del sistema Windows Server (anteprima)</span><span class="sxs-lookup"><span data-stu-id="e01f3-210">Back up Windows Server System State (Preview)</span></span>
<span data-ttu-id="e01f3-211">Il backup iniziale include tre attività:</span><span class="sxs-lookup"><span data-stu-id="e01f3-211">The initial backup includes three tasks:</span></span>

* <span data-ttu-id="e01f3-212">Abilitare il backup dello stato del sistema con l'agente di Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="e01f3-212">Enable System State Backup using the Azure Backup agent</span></span>
* <span data-ttu-id="e01f3-213">Pianificare il backup</span><span class="sxs-lookup"><span data-stu-id="e01f3-213">Schedule the backup</span></span>
* <span data-ttu-id="e01f3-214">Eseguire il backup di file e cartelle per la prima volta</span><span class="sxs-lookup"><span data-stu-id="e01f3-214">Back up files and folders for the first time</span></span>

<span data-ttu-id="e01f3-215">Per completare il backup iniziale, usare l'agente di Servizi di ripristino di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e01f3-215">To complete the initial backup, use the Microsoft Azure Recovery Services agent.</span></span>

### <a name="to-enable-system-state-backup-using-the-azure-backup-agent"></a><span data-ttu-id="e01f3-216">Per abilitare il backup dello stato del sistema con l'agente di Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="e01f3-216">To enable System State backup using the Azure Backup agent</span></span>

1. <span data-ttu-id="e01f3-217">In una sessione di PowerShell eseguire questo comando per arrestare il motore di backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="e01f3-217">In a PowerShell session, run the following command to stop the Azure Backup engine.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="e01f3-218">Aprire il Registro di sistema di Windows.</span><span class="sxs-lookup"><span data-stu-id="e01f3-218">Open the Windows Registry.</span></span>

  ```
  PS C:\> regedit.exe
  ```

3. <span data-ttu-id="e01f3-219">Aggiungere la chiave del Registro di sistema seguente con il valore DWORD specificato.</span><span class="sxs-lookup"><span data-stu-id="e01f3-219">Add the following registry key with the specified DWord Value.</span></span>

  | <span data-ttu-id="e01f3-220">Percorso del Registro</span><span class="sxs-lookup"><span data-stu-id="e01f3-220">Registry path</span></span> | <span data-ttu-id="e01f3-221">Chiave del Registro di sistema</span><span class="sxs-lookup"><span data-stu-id="e01f3-221">Registry key</span></span> | <span data-ttu-id="e01f3-222">Valore DWORD</span><span class="sxs-lookup"><span data-stu-id="e01f3-222">DWord value</span></span> |
  |---------------|--------------|-------------|
  | <span data-ttu-id="e01f3-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="e01f3-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="e01f3-224">TurnOffSSBFeature</span><span class="sxs-lookup"><span data-stu-id="e01f3-224">TurnOffSSBFeature</span></span> | <span data-ttu-id="e01f3-225">2</span><span class="sxs-lookup"><span data-stu-id="e01f3-225">2</span></span> |

4. <span data-ttu-id="e01f3-226">Riavviare il motore di backup eseguendo questo comando in un prompt dei comandi con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="e01f3-226">Restart the Backup engine by executing the following command in an elevated command prompt.</span></span>

  ```
  PS C:\> Net start obengine
  ```

### <a name="to-schedule-the-backup-job"></a><span data-ttu-id="e01f3-227">Per pianificare il processo di backup</span><span class="sxs-lookup"><span data-stu-id="e01f3-227">To schedule the backup job</span></span>

1. <span data-ttu-id="e01f3-228">Aprire l'agente di Servizi di ripristino di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e01f3-228">Open the Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="e01f3-229">È possibile trovarlo se si cerca **Backup di Microsoft Azure**nel computer.</span><span class="sxs-lookup"><span data-stu-id="e01f3-229">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Avviare l'agente di Servizi di ripristino di Azure](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. <span data-ttu-id="e01f3-231">Nell'agente di Servizi di ripristino fare clic su **Pianifica backup**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-231">In the Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. <span data-ttu-id="e01f3-233">Nella pagina Guida introduttiva della Pianificazione guidata backup fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-233">On the Getting started page of the Schedule Backup Wizard, click **Next**.</span></span>

4. <span data-ttu-id="e01f3-234">Nella pagina Seleziona elementi per backup fare clic su **Aggiungi elementi**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-234">On the Select Items to Backup page, click **Add Items**.</span></span>

5. <span data-ttu-id="e01f3-235">Selezionare **Stato del sistema** e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-235">Select **System State** and then click **OK**.</span></span>

6. <span data-ttu-id="e01f3-236">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-236">Click **Next**.</span></span>

7. <span data-ttu-id="e01f3-237">La pianificazione del backup e della conservazione dello stato del sistema viene impostata automaticamente su un backup ogni domenica alle 21:00 ora locale e su un periodo di conservazione di 60 giorni.</span><span class="sxs-lookup"><span data-stu-id="e01f3-237">The System State Backup and Retention schedule is automatically set to back up every Sunday at 9:00 PM local time, and the retention period is set to 60 days.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e01f3-238">I criteri di backup e di conservazione dello stato del sistema vengono configurati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e01f3-238">System State backup and retention policy is automatically configured.</span></span> <span data-ttu-id="e01f3-239">Se si vuole eseguire il backup di file e cartelle oltre che dello stato del sistema Windows Server, nella procedura guidata specificare solo i criteri di backup e di conservazione per i backup dei file.</span><span class="sxs-lookup"><span data-stu-id="e01f3-239">If you back up Files and Folders in addition to the Windows Server System State, specify only the Backup and Retention policy for file backups from the wizard.</span></span> 
   >

8. <span data-ttu-id="e01f3-240">Nella pagina Conferma esaminare le informazioni e fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-240">On the Confirmation page, review the information, and then click **Finish**.</span></span>

9. <span data-ttu-id="e01f3-241">Dopo aver creato la pianificazione del backup tramite la procedura guidata, fare clic su **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-241">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="to-back-up-windows-server-system-state-for-the-first-time"></a><span data-ttu-id="e01f3-242">Eseguire il backup dello stato del sistema Windows Server per la prima volta</span><span class="sxs-lookup"><span data-stu-id="e01f3-242">To back up Windows Server System State for the first time</span></span>

1. <span data-ttu-id="e01f3-243">Verificare che non siano presenti aggiornamenti in sospeso di Windows Server che richiedono un riavvio.</span><span class="sxs-lookup"><span data-stu-id="e01f3-243">Make sure there are no pending updates for Windows Server that require a reboot.</span></span>

2. <span data-ttu-id="e01f3-244">Nell'agente di Servizi di ripristino fare clic su **Esegui backup** per completare il seeding iniziale sulla rete.</span><span class="sxs-lookup"><span data-stu-id="e01f3-244">In the Recovery Services agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Eseguire ora il backup di Windows Server](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. <span data-ttu-id="e01f3-246">Nella pagina Conferma riesaminare le impostazioni che l'Esecuzione guidata backup userà per il backup del computer.</span><span class="sxs-lookup"><span data-stu-id="e01f3-246">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="e01f3-247">Fare clic su **Backup**.</span><span class="sxs-lookup"><span data-stu-id="e01f3-247">Then click **Back Up**.</span></span>

4. <span data-ttu-id="e01f3-248">Fare clic su **Chiudi** per chiudere la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="e01f3-248">Click **Close** to close the wizard.</span></span> <span data-ttu-id="e01f3-249">Se si chiude la procedura guidata prima che venga completato il processo di backup, l'esecuzione guidata proseguirà in background.</span><span class="sxs-lookup"><span data-stu-id="e01f3-249">If you close the wizard before the backup process finishes, the wizard continues to run in the background.</span></span>

5. <span data-ttu-id="e01f3-250">Se si esegue il backup di file e cartelle oltre che dello stato del sistema Windows Server, la procedura guidata Esegui backup ora eseguirà il backup solo dei file.</span><span class="sxs-lookup"><span data-stu-id="e01f3-250">If you back up Files and Folders on your server, in addition to the Windows Server System State, the Backup Now wizard will only back up files.</span></span> <span data-ttu-id="e01f3-251">Per eseguire un backup dello stato del sistema ad hoc, usare questo comando di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e01f3-251">To perform an ad hoc System State back up, use the following PowerShell command:</span></span>

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  <span data-ttu-id="e01f3-252">Al termine del backup iniziale, nella console Backup comparirà lo stato **Processo completato** .</span><span class="sxs-lookup"><span data-stu-id="e01f3-252">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

  ![Completamento infrarossi](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="e01f3-254">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="e01f3-254">Frequently asked questions</span></span>

<span data-ttu-id="e01f3-255">Le domande e le risposte seguenti offrono informazioni supplementari.</span><span class="sxs-lookup"><span data-stu-id="e01f3-255">The following questions and answers provide supplementary information.</span></span>

### <a name="what-is-the-staging-volume"></a><span data-ttu-id="e01f3-256">Che cos'è il volume di staging?</span><span class="sxs-lookup"><span data-stu-id="e01f3-256">What is the Staging Volume?</span></span>

<span data-ttu-id="e01f3-257">Il volume di staging rappresenta la posizione intermedia in cui Windows Server Backup, disponibile in modo nativo, inserisce temporaneamente il backup dello stato del sistema.</span><span class="sxs-lookup"><span data-stu-id="e01f3-257">The Staging Volume represents the intermediate location where the natively available, Windows Server Backup stages the System State Backup.</span></span> <span data-ttu-id="e01f3-258">L'agente di Backup di Azure quindi comprime e crittografa questo backup intermedio e lo invia tramite il protocollo HTTPS sicuro all'insieme di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e01f3-258">Azure Backup agent then compresses and encrypts this intermediate backup and sends it via secure HTTPS Protocol to the configured Recovery Services Vault.</span></span> <span data-ttu-id="e01f3-259">**È consigliabile definire il volume di staging in una posizione che non sia un volume del sistema operativo Windows. Se si riscontrano problemi con i backup dello stato del sistema, il primo passaggio per risolverli è controllare la posizione del volume di staging.**</span><span class="sxs-lookup"><span data-stu-id="e01f3-259">**We strongly recommended you establish the Staging Volume in a non-Windows-OS volume. If you observe problems with System State Backups, checking the location of your Staging Volume is the first troubleshooting step.**</span></span> 

### <a name="how-can-i-change-the-staging-volume-path-specified-in-the-azure-backup-agent"></a><span data-ttu-id="e01f3-260">Come si può modificare il percorso del volume di staging specificato nell'agente di Backup di Azure?</span><span class="sxs-lookup"><span data-stu-id="e01f3-260">How can I change the Staging Volume Path specified in the Azure Backup agent?</span></span>

<span data-ttu-id="e01f3-261">Per impostazione predefinita, il volume di staging si trova nella cartella della cache.</span><span class="sxs-lookup"><span data-stu-id="e01f3-261">The Staging Volume is located in the cache folder by default.</span></span> 

1. <span data-ttu-id="e01f3-262">Per modificare tale posizione, usare il comando seguente in un prompt dei comandi con privilegi elevati:</span><span class="sxs-lookup"><span data-stu-id="e01f3-262">To change this location, use the following command (in an elevated command prompt):</span></span>
  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="e01f3-263">Aggiornare quindi la voce del Registro di sistema seguente con il percorso della nuova cartella del volume di staging.</span><span class="sxs-lookup"><span data-stu-id="e01f3-263">Then update the following registry entries with the path to the new Staging Volume folder.</span></span>

  |<span data-ttu-id="e01f3-264">Percorso del Registro</span><span class="sxs-lookup"><span data-stu-id="e01f3-264">Registry path</span></span>|<span data-ttu-id="e01f3-265">Chiave del Registro di sistema</span><span class="sxs-lookup"><span data-stu-id="e01f3-265">Registry key</span></span>|<span data-ttu-id="e01f3-266">Valore</span><span class="sxs-lookup"><span data-stu-id="e01f3-266">Value</span></span>|
  |-------------|------------|-----|
  |<span data-ttu-id="e01f3-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="e01f3-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="e01f3-268">SSBStagingPath</span><span class="sxs-lookup"><span data-stu-id="e01f3-268">SSBStagingPath</span></span> | <span data-ttu-id="e01f3-269">Nuovo percorso del volume di staging</span><span class="sxs-lookup"><span data-stu-id="e01f3-269">new staging volume location</span></span> |

<span data-ttu-id="e01f3-270">Per il percorso di staging viene fatta distinzione tra maiuscole e minuscole e l'uso di maiuscole e minuscole deve corrispondere esattamente a quello esistente nel server.</span><span class="sxs-lookup"><span data-stu-id="e01f3-270">The Staging Path is case sensitive and must be the exact same casing as what exists on the server.</span></span> 

3. <span data-ttu-id="e01f3-271">Dopo aver modificato il percorso del volume di staging, riavviare il motore di backup:</span><span class="sxs-lookup"><span data-stu-id="e01f3-271">Once you change the Staging volume path, restart the Backup engine:</span></span>
  ```
  PS C:\> Net start obengine
  ```
4. <span data-ttu-id="e01f3-272">Per acquisire il percorso modificato, aprire l'agente di Servizi di ripristino di Microsoft Azure e attivare un backup ad hoc dello stato del sistema.</span><span class="sxs-lookup"><span data-stu-id="e01f3-272">To pick up the changed path, open the Microsoft Azure Recovery Services agent and trigger an ad hoc backup of System State.</span></span>

### <a name="why-is-the-system-state-default-retention-set-to-60-days"></a><span data-ttu-id="e01f3-273">Perché l'impostazione predefinita della conservazione dello stato del sistema è 60 giorni?</span><span class="sxs-lookup"><span data-stu-id="e01f3-273">Why is the System State default retention set to 60 days?</span></span>

<span data-ttu-id="e01f3-274">La vita utile di un backup dello stato del sistema è uguale all'impostazione della "durata di rimozione definitiva" del ruolo Active Directory di Windows Server.</span><span class="sxs-lookup"><span data-stu-id="e01f3-274">The useful life of a system state backup is the same as the "tombstone lifetime" setting for the Windows Server Active Directory role.</span></span> <span data-ttu-id="e01f3-275">Il valore predefinito della voce relativa alla durata di rimozione definitiva è 60 giorni.</span><span class="sxs-lookup"><span data-stu-id="e01f3-275">The default value for the tombstone lifetime entry is 60 days.</span></span> <span data-ttu-id="e01f3-276">Questo valore può essere impostato nell'oggetto di configurazione del servizio directory (NTDS).</span><span class="sxs-lookup"><span data-stu-id="e01f3-276">This value can be set on the Directory Service (NTDS) config object.</span></span>

### <a name="how-do-i-change-the-default-backup-and-retention-policy-for-system-state"></a><span data-ttu-id="e01f3-277">Come si modificano i criteri di backup e di conservazione predefiniti per lo stato del sistema?</span><span class="sxs-lookup"><span data-stu-id="e01f3-277">How do I change the default Backup and Retention Policy for System State?</span></span>

<span data-ttu-id="e01f3-278">Per modificare i criteri di backup e di conservazione predefiniti per lo stato del sistema:</span><span class="sxs-lookup"><span data-stu-id="e01f3-278">To change the default Backup and Retention Policy for System State:</span></span>
1. <span data-ttu-id="e01f3-279">Arrestare il motore di backup.</span><span class="sxs-lookup"><span data-stu-id="e01f3-279">Stop the Backup engine.</span></span> <span data-ttu-id="e01f3-280">Eseguire questo comando da un prompt dei comandi con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="e01f3-280">Run the following command from an elevated command prompt.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="e01f3-281">Aggiungere o aggiornare le voci di chiave del Registro di sistema seguenti in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.</span><span class="sxs-lookup"><span data-stu-id="e01f3-281">Add or update the following registry key entries in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.</span></span>

  |<span data-ttu-id="e01f3-282">Nome nel Registro di sistema</span><span class="sxs-lookup"><span data-stu-id="e01f3-282">Registry Name</span></span>|<span data-ttu-id="e01f3-283">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e01f3-283">Description</span></span>|<span data-ttu-id="e01f3-284">Valore</span><span class="sxs-lookup"><span data-stu-id="e01f3-284">Value</span></span>|
  |-------------|-----------|-----|
  |<span data-ttu-id="e01f3-285">SSBScheduleTime</span><span class="sxs-lookup"><span data-stu-id="e01f3-285">SSBScheduleTime</span></span>|<span data-ttu-id="e01f3-286">Consente di configurare l'ora di backup.</span><span class="sxs-lookup"><span data-stu-id="e01f3-286">Used to configure the time of the backup.</span></span> <span data-ttu-id="e01f3-287">L'impostazione predefinita sono le 21 ora locale.</span><span class="sxs-lookup"><span data-stu-id="e01f3-287">Default is 9PM local time.</span></span>|<span data-ttu-id="e01f3-288">DWORD: formato HHMM (numero decimale), ad esempio 2130 per le 21:30 ora locale</span><span class="sxs-lookup"><span data-stu-id="e01f3-288">DWord: Format HHMM (Decimal) for example 2130 for 9:30PM local time</span></span>|
  |<span data-ttu-id="e01f3-289">SSBScheduleDays</span><span class="sxs-lookup"><span data-stu-id="e01f3-289">SSBScheduleDays</span></span>|<span data-ttu-id="e01f3-290">Consente di configurare i giorni in cui il backup dello stato del sistema deve essere eseguito all'ora specificata.</span><span class="sxs-lookup"><span data-stu-id="e01f3-290">Used to configure the days when System State Backup must be performed at the specified time.</span></span> <span data-ttu-id="e01f3-291">I giorni della settimana sono specificati da singole cifre.</span><span class="sxs-lookup"><span data-stu-id="e01f3-291">Individual digits specify days of the week.</span></span> <span data-ttu-id="e01f3-292">0 rappresenta domenica, 1 lunedì e così via.</span><span class="sxs-lookup"><span data-stu-id="e01f3-292">0 represents Sunday, 1 is Monday, and so on.</span></span> <span data-ttu-id="e01f3-293">Il giorno predefinito per il backup è domenica.</span><span class="sxs-lookup"><span data-stu-id="e01f3-293">Default day for backup is Sunday.</span></span>|<span data-ttu-id="e01f3-294">DWORD: giorni della settimana in cui eseguire il backup (numero decimale). Ad esempio, 1230 pianifica i backup di lunedì, martedì, mercoledì e domenica.</span><span class="sxs-lookup"><span data-stu-id="e01f3-294">DWord: days of the week to run backup (decimal) for example 1230 schedules backups on Monday, Tuesday, Wednesday, and Sunday.</span></span>|
  |<span data-ttu-id="e01f3-295">SSBRetentionDays</span><span class="sxs-lookup"><span data-stu-id="e01f3-295">SSBRetentionDays</span></span>|<span data-ttu-id="e01f3-296">Consente di configurare i giorni di conservazione del backup.</span><span class="sxs-lookup"><span data-stu-id="e01f3-296">Used to configure the days to retain backup.</span></span> <span data-ttu-id="e01f3-297">Il valore predefinito è 60.</span><span class="sxs-lookup"><span data-stu-id="e01f3-297">Default value is 60.</span></span> <span data-ttu-id="e01f3-298">Il massimo consentito è 180.</span><span class="sxs-lookup"><span data-stu-id="e01f3-298">Maximum allowed value is 180.</span></span>|<span data-ttu-id="e01f3-299">DWORD: giorni di conservazione del backup (numero decimale).</span><span class="sxs-lookup"><span data-stu-id="e01f3-299">DWord: Days to retain backup (decimal).</span></span>|

3. <span data-ttu-id="e01f3-300">Usare il comando seguente per riavviare il motore di backup.</span><span class="sxs-lookup"><span data-stu-id="e01f3-300">Use the following command to restart the backup engine.</span></span>
    ```
    PS C:\> Net start obengine
    ```

4. <span data-ttu-id="e01f3-301">Aprire l'agente di Servizi di ripristino di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e01f3-301">Open the Microsoft Recovery Services agent.</span></span>

5. <span data-ttu-id="e01f3-302">Fare clic su **Pianifica backup** e quindi su **Avanti** finché non vengono visualizzate le modifiche.</span><span class="sxs-lookup"><span data-stu-id="e01f3-302">Click **Schedule Backup** and then click **Next** until you see the changes reflected.</span></span>

6. <span data-ttu-id="e01f3-303">Fare clic su **Fine** per applicare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="e01f3-303">Click **Finish** to apply the changes.</span></span>


## <a name="questions"></a><span data-ttu-id="e01f3-304">Domande?</span><span class="sxs-lookup"><span data-stu-id="e01f3-304">Questions?</span></span>
<span data-ttu-id="e01f3-305">In caso di domande o se si vuole che venga inclusa una funzionalità, è possibile [inviare commenti e suggerimenti](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="e01f3-305">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e01f3-306">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e01f3-306">Next steps</span></span>
* <span data-ttu-id="e01f3-307">Sono disponibili altre informazioni sul [backup di computer Windows](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="e01f3-307">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="e01f3-308">Ora che si è eseguito il backup dei file e delle cartelle, è possibile [gestire l'insieme di credenziali e i server](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="e01f3-308">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="e01f3-309">Se è necessario ripristinare un backup, usare questo articolo per [ripristinare i file in un computer Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="e01f3-309">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span></span>
