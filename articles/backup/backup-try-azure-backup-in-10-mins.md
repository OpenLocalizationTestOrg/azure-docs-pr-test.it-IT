---
title: Eseguire il backup di file e cartelle da Windows in Azure (Resource Manager) | Microsoft Docs
description: Informazioni su come eseguire il backup di file e cartelle di Windows in Azure in una distribuzione Resource Manager.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: come eseguire il backup; procedura di backup; backup di file e cartelle
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 8/15/2017
ms.author: markgal;
ms.openlocfilehash: b21edb70eca3ec9552dc157ee3bb658d243b8fcd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="first-look-back-up-files-and-folders-in-resource-manager-deployment"></a><span data-ttu-id="ab823-104">Primi passi: eseguire il backup di file e cartelle in una distribuzione Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ab823-104">First look: back up files and folders in Resource Manager deployment</span></span>
<span data-ttu-id="ab823-105">Questo articolo illustra come eseguire il backup di file e cartelle di Windows Server o di un computer Windows in Azure usando una distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ab823-105">This article explains how to back up your Windows Server (or Windows computer) files and folders to Azure using a Resource Manager deployment.</span></span> <span data-ttu-id="ab823-106">Si tratta di un'esercitazione che illustra le informazioni di base,</span><span class="sxs-lookup"><span data-stu-id="ab823-106">It's a tutorial intended to walk you through the basics.</span></span> <span data-ttu-id="ab823-107">l'ideale per iniziare a usare Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab823-107">If you want to get started using Azure Backup, you're in the right place.</span></span>

<span data-ttu-id="ab823-108">Per altre informazioni su Backup di Azure, vedere questa [panoramica](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="ab823-108">If you want to know more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="ab823-109">Se non è disponibile una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/) che consente di accedere a qualsiasi servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab823-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="ab823-110">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="ab823-110">Create a recovery services vault</span></span>
<span data-ttu-id="ab823-111">Per eseguire il backup dei file e delle cartelle, è necessario creare un insieme di credenziali di Servizi di ripristino nell'area in cui archiviare i dati.</span><span class="sxs-lookup"><span data-stu-id="ab823-111">To back up your files and folders, you need to create a Recovery Services vault in the region where you want to store the data.</span></span> <span data-ttu-id="ab823-112">È anche necessario determinare la modalità di replica di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ab823-112">You also need to determine how you want your storage replicated.</span></span>

### <a name="to-create-a-recovery-services-vault"></a><span data-ttu-id="ab823-113">Per creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="ab823-113">To create a Recovery Services vault</span></span>
1. <span data-ttu-id="ab823-114">Se questa operazione non è già stata eseguita, accedere al [portale di Azure](https://portal.azure.com/) , tramite la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab823-114">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="ab823-115">Scegliere **Altri servizi** dal menu Hub e nell'elenco di risorse digitare **Servizi di ripristino**, quindi fare clic su **Insiemi di credenziali dei servizi di ripristino**.</span><span class="sxs-lookup"><span data-stu-id="ab823-115">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="ab823-117">Se presenti nella sottoscrizione, gli insiemi di credenziali dei servizi di ripristino vengono elencati.</span><span class="sxs-lookup"><span data-stu-id="ab823-117">If there are recovery services vaults in the subscription, the vaults are listed.</span></span>
3. <span data-ttu-id="ab823-118">Scegliere **Aggiungi** dal menu **Insiemi di credenziali dei servizi di ripristino**.</span><span class="sxs-lookup"><span data-stu-id="ab823-118">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="ab823-120">Verrà visualizzato il pannello degli insiemi di credenziali dei servizi di ripristino, in cui viene richiesto di specificare **Nome**, **Sottoscrizione**, **Gruppo di risorse** e **Località**.</span><span class="sxs-lookup"><span data-stu-id="ab823-120">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="ab823-122">Nel campo **Nome**digitare un nome descrittivo per identificare l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="ab823-122">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="ab823-123">Il nome deve essere univoco per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab823-123">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="ab823-124">Digitare un nome che contenga tra i 2 e i 50 caratteri.</span><span class="sxs-lookup"><span data-stu-id="ab823-124">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="ab823-125">Deve iniziare con una lettera e può contenere solo lettere, numeri e trattini.</span><span class="sxs-lookup"><span data-stu-id="ab823-125">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="ab823-126">Nella sezione **Sottoscrizione** usare il menu a discesa per scegliere la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab823-126">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="ab823-127">Se si usa una sola sottoscrizione, questa verrà visualizzata e sarà possibile andare al passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="ab823-127">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="ab823-128">Se non si è certi di quale sottoscrizione usare, usare la sottoscrizione predefinita (o suggerita).</span><span class="sxs-lookup"><span data-stu-id="ab823-128">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="ab823-129">Sono disponibili più scelte solo se l'account dell'organizzazione è associato a più sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab823-129">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="ab823-130">Nella sezione **Gruppo di risorse**:</span><span class="sxs-lookup"><span data-stu-id="ab823-130">In the **Resource group** section:</span></span>

    * <span data-ttu-id="ab823-131">Selezionare **Crea nuovo** per creare un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ab823-131">select **Create new** if you want to create a new Resource group.</span></span>
    <span data-ttu-id="ab823-132">Or</span><span class="sxs-lookup"><span data-stu-id="ab823-132">Or</span></span>
    * <span data-ttu-id="ab823-133">Selezionare **Usa esistente** e fare clic sul menu a discesa per visualizzare l'elenco di gruppi di risorse disponibili.</span><span class="sxs-lookup"><span data-stu-id="ab823-133">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="ab823-134">Per informazioni complete sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ab823-134">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="ab823-135">Fare clic su **Località** per selezionare l'area geografica per l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="ab823-135">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="ab823-136">La scelta determina l'area geografica in cui vengono inviati i dati di backup.</span><span class="sxs-lookup"><span data-stu-id="ab823-136">This choice determines the geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="ab823-137">Nella parte inferiore del pannello Insieme di credenziali dei servizi di ripristino fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ab823-137">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="ab823-138">La creazione dell'insieme di credenziali dei servizi di ripristino può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="ab823-138">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="ab823-139">Monitorare le notifiche di stato nell'area superiore destra del portale.</span><span class="sxs-lookup"><span data-stu-id="ab823-139">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="ab823-140">L'insieme di credenziali, dopo essere stato creato, viene visualizzato negli insiemi di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="ab823-140">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="ab823-141">Se l'insieme di credenziali non viene visualizzato dopo qualche minuto, fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="ab823-141">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Fare clic sul pulsante Aggiorna](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="ab823-143">Dopo la visualizzazione dell'insieme di credenziali nell'elenco corrispondente per i Servizi di ripristino, è possibile configurare la ridondanza di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ab823-143">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-the-vault"></a><span data-ttu-id="ab823-144">Impostare la ridondanza di archiviazione dell'insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="ab823-144">Set storage redundancy for the vault</span></span>
<span data-ttu-id="ab823-145">Quando si crea un insieme di credenziali dei Servizi di ripristino, assicurarsi che la ridondanza di archiviazione sia configurata in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="ab823-145">When you create a Recovery Services vault, make sure storage redundancy is configured the way you want.</span></span>

1. <span data-ttu-id="ab823-146">Nel pannello **Insieme di credenziali dei servizi di ripristino** fare clic sul nuovo insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="ab823-146">From the **Recovery Services vaults** blade, click the new vault.</span></span>

    ![Selezionare il nuovo insieme di credenziali dall'elenco corrispondente per Servizi di ripristino](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="ab823-148">Quando si seleziona l'insieme di credenziali, il pannello **Insieme di credenziali dei servizi di ripristino** si restringe e vengono aperti il pannello Impostazioni,*con il nome dell'insieme di credenziali nella parte superiore*, e il pannello dei dettagli dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="ab823-148">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span></span>

    ![Visualizzare la configurazione dell'archiviazione per il nuovo insieme di credenziali](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="ab823-150">Nel pannello Impostazioni del nuovo insieme di credenziali usare il dispositivo di scorrimento verticale per passare alla sezione Gestisci e fare clic su **Infrastruttura di backup**.</span><span class="sxs-lookup"><span data-stu-id="ab823-150">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="ab823-151">Verrà visualizzato il pannello Infrastruttura di backup.</span><span class="sxs-lookup"><span data-stu-id="ab823-151">The Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="ab823-152">Nel pannello Infrastruttura di backup fare clic su **Configurazione backup** per aprire il pannello **Configurazione backup**.</span><span class="sxs-lookup"><span data-stu-id="ab823-152">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

    ![Impostare la configurazione dell'archiviazione per il nuovo insieme di credenziali](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="ab823-154">Scegliere l'opzione di replica di archiviazione appropriata per l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="ab823-154">Choose the appropriate storage replication option for your vault.</span></span>

    ![opzioni di configurazione dell'archiviazione](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="ab823-156">Per impostazione predefinita, l'insieme di credenziali prevede l'archiviazione con ridondanza geografica.</span><span class="sxs-lookup"><span data-stu-id="ab823-156">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="ab823-157">Se si usa Azure come endpoint di archiviazione di backup primario, continuare a usare l'opzione **Con ridondanza geografica**.</span><span class="sxs-lookup"><span data-stu-id="ab823-157">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="ab823-158">Se non si usa Azure come endpoint di archiviazione di backup primario, scegliere l'opzione **Con ridondanza locale**, che riduce i costi di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab823-158">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="ab823-159">Per altre informazioni sulle opzioni di archiviazione [con ridondanza geografica](../storage/common/storage-redundancy.md#geo-redundant-storage) e [con ridondanza locale](../storage/common/storage-redundancy.md#locally-redundant-storage), vedere [Panoramica della ridondanza di archiviazione](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="ab823-159">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="ab823-160">Dopo aver creato un insieme di credenziali, configurarlo per il backup di file e cartelle.</span><span class="sxs-lookup"><span data-stu-id="ab823-160">Now that you've created a vault, configure it for backing up files and folders.</span></span>

## <a name="configure-the-vault"></a><span data-ttu-id="ab823-161">Configurare l'insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="ab823-161">Configure the vault</span></span>
1. <span data-ttu-id="ab823-162">Nel pannello dell'insieme di credenziali dei servizi di ripristino appena creato, nella sezione Attività iniziali fare clic su **Backup** e nel pannello **Introduzione al backup** selezionare **Obiettivo del backup**.</span><span class="sxs-lookup"><span data-stu-id="ab823-162">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Aprire il Pannello Obiettivo di backup](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="ab823-164">Verrà visualizzato il pannello **Obiettivo del backup**.</span><span class="sxs-lookup"><span data-stu-id="ab823-164">The **Backup Goal** blade opens.</span></span>

    ![Aprire il Pannello Obiettivo di backup](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="ab823-166">Scegliere **Locale** dal menu a discesa **Posizione di esecuzione del carico di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="ab823-166">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="ab823-167">Si sceglie **Locale** perché il server di Windows o il computer Windows è un computer fisico che non si trova in Azure.</span><span class="sxs-lookup"><span data-stu-id="ab823-167">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="ab823-168">Scegliere **File e cartelle** dal menu **Elementi di cui eseguire il backup**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ab823-168">From the **What do you want to backup?** menu, select **Files and folders**, and click **OK**.</span></span>

    ![Configurazione di file e cartelle](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

    <span data-ttu-id="ab823-170">Dopo aver fatto clic su OK verrà visualizzato un segno di spunta accanto a **Obiettivo del backup** e si aprirà il pannello **Preparare l'infrastruttura**.</span><span class="sxs-lookup"><span data-stu-id="ab823-170">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span></span>

    ![Preparare l'infrastruttura dopo aver configurato l'obiettivo del backup](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="ab823-172">Nel pannello **Preparare l'infrastruttura** fare clic su **Scaricare l'agente per Windows Server o Windows Client**.</span><span class="sxs-lookup"><span data-stu-id="ab823-172">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![Preparare l'infrastruttura](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="ab823-174">Se si usa Windows Server Essentials, scegliere di scaricare l'agente per Windows Server Essentials.</span><span class="sxs-lookup"><span data-stu-id="ab823-174">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span></span> <span data-ttu-id="ab823-175">Un menu a comparsa chiederà di eseguire o salvare MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="ab823-175">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span></span>

    ![Finestra di dialogo di MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="ab823-177">Fare clic su **Salva** nel menu a comparsa del download.</span><span class="sxs-lookup"><span data-stu-id="ab823-177">In the download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="ab823-178">Per impostazione predefinita, il file **MARSagentinstaller.exe** viene salvato nella cartella Downloads.</span><span class="sxs-lookup"><span data-stu-id="ab823-178">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span></span> <span data-ttu-id="ab823-179">Al termine del programma di installazione verrà visualizzato un messaggio popup che chiede se eseguire il programma di installazione o aprire la cartella.</span><span class="sxs-lookup"><span data-stu-id="ab823-179">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span></span>

    ![Preparare l'infrastruttura](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="ab823-181">Non è ancora necessario installare l'agente.</span><span class="sxs-lookup"><span data-stu-id="ab823-181">You don't need to install the agent yet.</span></span> <span data-ttu-id="ab823-182">È possibile installare l'agente al termine del download delle credenziali dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="ab823-182">You can install the agent after you have downloaded the vault credentials.</span></span>

6. <span data-ttu-id="ab823-183">Fare clic su **Scarica** nel pannello **Preparare l'infrastruttura**.</span><span class="sxs-lookup"><span data-stu-id="ab823-183">On the **Prepare infrastructure** blade, click **Download**.</span></span>

    ![Scaricare le credenziali dell'insieme di credenziali](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="ab823-185">Le credenziali dell'insieme di credenziali verranno scaricate nella cartella Download locale.</span><span class="sxs-lookup"><span data-stu-id="ab823-185">The vault credentials download to your Downloads folder.</span></span> <span data-ttu-id="ab823-186">Al termine del download delle credenziali dell'insieme di credenziali verrà visualizzato un messaggio popup che chiede se aprire o salvare le credenziali.</span><span class="sxs-lookup"><span data-stu-id="ab823-186">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span></span> <span data-ttu-id="ab823-187">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="ab823-187">Click **Save**.</span></span> <span data-ttu-id="ab823-188">Se si fa clic accidentalmente su **Apri**, attendere che il tentativo di apertura delle credenziali termini con un errore.</span><span class="sxs-lookup"><span data-stu-id="ab823-188">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span></span> <span data-ttu-id="ab823-189">Non è possibile aprire le credenziali dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="ab823-189">You cannot open the vault credentials.</span></span> <span data-ttu-id="ab823-190">Procedere con il passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="ab823-190">Proceed to the next step.</span></span> <span data-ttu-id="ab823-191">Le credenziali dell'insieme di credenziali si trovano nella cartella Downloads.</span><span class="sxs-lookup"><span data-stu-id="ab823-191">The vault credentials are in the Downloads folder.</span></span>   

    ![Il download delle credenziali dell'insieme di credenziali è terminato](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-the-agent"></a><span data-ttu-id="ab823-193">Installare e registrare l'agente</span><span class="sxs-lookup"><span data-stu-id="ab823-193">Install and register the agent</span></span>

> [!NOTE]
> <span data-ttu-id="ab823-194">L'abilitazione del backup tramite il portale di Azure non è ancora disponibile.</span><span class="sxs-lookup"><span data-stu-id="ab823-194">Enabling backup through the Azure portal is not available, yet.</span></span> <span data-ttu-id="ab823-195">Usare l'agente di Servizi di ripristino di Microsoft Azure per eseguire il backup di file e cartelle.</span><span class="sxs-lookup"><span data-stu-id="ab823-195">Use the Microsoft Azure Recovery Services Agent to back up your files and folders.</span></span>
>

1. <span data-ttu-id="ab823-196">Cercare e fare doppio clic sul file **MARSagentinstaller.exe** nella cartella Downloads o nella cartella in cui è stato salvato.</span><span class="sxs-lookup"><span data-stu-id="ab823-196">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="ab823-197">Il programma di installazione visualizzerà una serie di messaggi durante l'estrazione, l'installazione e la registrazione dell'agente di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="ab823-197">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span></span>

    ![Eseguire il programma di installazione dell'agente di Servizi di ripristino](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="ab823-199">Completare l'Installazione guidata di Agente servizi di ripristino di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ab823-199">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="ab823-200">Per completare la procedura guidata, è necessario:</span><span class="sxs-lookup"><span data-stu-id="ab823-200">To complete the wizard, you need to:</span></span>

   * <span data-ttu-id="ab823-201">Scegliere un percorso per la cartella di installazione e della cache.</span><span class="sxs-lookup"><span data-stu-id="ab823-201">Choose a location for the installation and cache folder.</span></span>
   * <span data-ttu-id="ab823-202">Fornire le informazioni sul server proxy se si usa un server proxy per connettersi a Internet.</span><span class="sxs-lookup"><span data-stu-id="ab823-202">Provide your proxy server info if you use a proxy server to connect to the internet.</span></span>
   * <span data-ttu-id="ab823-203">Se si usa un proxy autenticato, immettere il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="ab823-203">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="ab823-204">Fornire le credenziali dell'insieme di credenziali scaricate.</span><span class="sxs-lookup"><span data-stu-id="ab823-204">Provide the downloaded vault credentials</span></span>
   * <span data-ttu-id="ab823-205">Salvare la passphrase di crittografia in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="ab823-205">Save the encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="ab823-206">Se la passphrase viene persa o dimenticata, Microsoft non potrà offrire assistenza per il recupero dei dati di backup.</span><span class="sxs-lookup"><span data-stu-id="ab823-206">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span></span> <span data-ttu-id="ab823-207">Salvare il file in una posizione sicura.</span><span class="sxs-lookup"><span data-stu-id="ab823-207">Save the file in a secure location.</span></span> <span data-ttu-id="ab823-208">È necessario per ripristinare un backup.</span><span class="sxs-lookup"><span data-stu-id="ab823-208">It is required to restore a backup.</span></span>
     >
     >

<span data-ttu-id="ab823-209">L'agente ora è installato e il computer è registrato nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="ab823-209">The agent is now installed and your machine is registered to the vault.</span></span> <span data-ttu-id="ab823-210">Ora è possibile configurare e pianificare il backup.</span><span class="sxs-lookup"><span data-stu-id="ab823-210">You're ready to configure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="ab823-211">Requisiti di rete e connettività</span><span class="sxs-lookup"><span data-stu-id="ab823-211">Network and Connectivity Requirements</span></span>

<span data-ttu-id="ab823-212">Se il computer/proxy ha un accesso a Internet limitato, verificare che le impostazioni del firewall nel computer/proxy siano configurate per consentire gli URL seguenti:</span><span class="sxs-lookup"><span data-stu-id="ab823-212">If your machine/proxy has limited internet access, ensure that firewall settings on the mcahine/proxy are configured to allow the following URLs:</span></span> <br>
    1. <span data-ttu-id="ab823-213">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="ab823-213">www.msftncsi.com</span></span>
    2. <span data-ttu-id="ab823-214">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="ab823-214">*.Microsoft.com</span></span>
    3. <span data-ttu-id="ab823-215">windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="ab823-215">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="ab823-216">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="ab823-216">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="ab823-217">*. windows.ne</span><span class="sxs-lookup"><span data-stu-id="ab823-217">*.windows.ne</span></span>

## <a name="back-up-your-files-and-folders"></a><span data-ttu-id="ab823-218">Eseguire il backup di file e cartelle</span><span class="sxs-lookup"><span data-stu-id="ab823-218">Back up your files and folders</span></span>
<span data-ttu-id="ab823-219">Il backup iniziale comprende due attività fondamentali:</span><span class="sxs-lookup"><span data-stu-id="ab823-219">The initial backup includes two key tasks:</span></span>

* <span data-ttu-id="ab823-220">Pianificare il backup</span><span class="sxs-lookup"><span data-stu-id="ab823-220">Schedule the backup</span></span>
* <span data-ttu-id="ab823-221">Eseguire il backup di file e cartelle per la prima volta</span><span class="sxs-lookup"><span data-stu-id="ab823-221">Back up files and folders for the first time</span></span>

<span data-ttu-id="ab823-222">Per completare il backup iniziale, usare l'agente di Servizi di ripristino di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ab823-222">To complete the initial backup, use the Microsoft Azure Recovery Services agent.</span></span>

### <a name="to-schedule-the-backup-job"></a><span data-ttu-id="ab823-223">Per pianificare il processo di backup</span><span class="sxs-lookup"><span data-stu-id="ab823-223">To schedule the backup job</span></span>
1. <span data-ttu-id="ab823-224">Aprire l'agente di Servizi di ripristino di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ab823-224">Open the Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="ab823-225">È possibile trovarlo se si cerca **Backup di Microsoft Azure**nel computer.</span><span class="sxs-lookup"><span data-stu-id="ab823-225">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Avviare l'agente di Servizi di ripristino di Azure](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)
2. <span data-ttu-id="ab823-227">Nell'agente di Servizi di ripristino fare clic su **Pianifica backup**.</span><span class="sxs-lookup"><span data-stu-id="ab823-227">In the Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)
3. <span data-ttu-id="ab823-229">Nella pagina Guida introduttiva della Pianificazione guidata backup fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="ab823-229">On the Getting started page of the Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="ab823-230">Nella pagina Seleziona elementi per backup fare clic su **Aggiungi elementi**.</span><span class="sxs-lookup"><span data-stu-id="ab823-230">On the Select Items to Backup page, click **Add Items**.</span></span>
5. <span data-ttu-id="ab823-231">Selezionare i file e le cartelle di cui si vuole eseguire il backup e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ab823-231">Select the files and folders that you want to back up, and then click **Okay**.</span></span>
6. <span data-ttu-id="ab823-232">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="ab823-232">Click **Next**.</span></span>
7. <span data-ttu-id="ab823-233">Nella pagina **Specificare la pianificazione del backup** specificare la **pianificazione del backup** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="ab823-233">On the **Specify Backup Schedule** page, specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="ab823-234">È possibile pianificare backup giornalieri, da eseguire non più di tre volte al giorno, o settimanali.</span><span class="sxs-lookup"><span data-stu-id="ab823-234">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Elementi per il backup di Windows Server](./media/backup-try-azure-backup-in-10-mins/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="ab823-236">Per altre informazioni su come specificare la pianificazione del backup vedere l'articolo [Usare Backup di Azure per sostituire l'infrastruttura basata su nastro](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="ab823-236">For more information about how to specify the backup schedule, see the article [Use Azure Backup to replace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

8. <span data-ttu-id="ab823-237">Nella pagina **Seleziona criteri di conservazione** selezionare i **criteri di conservazione** per la copia di backup.</span><span class="sxs-lookup"><span data-stu-id="ab823-237">On the **Select Retention Policy** page, select the **Retention Policy** for the backup copy.</span></span>

    <span data-ttu-id="ab823-238">I criteri di conservazione specificano la durata dell'archiviazione dei dati di backup.</span><span class="sxs-lookup"><span data-stu-id="ab823-238">The retention policy specifies how long the backup data is stored.</span></span> <span data-ttu-id="ab823-239">Anziché specificare un "criterio semplice" per tutti i punti di backup, è possibile specificare criteri di conservazione diversi in base al momento in cui viene eseguito il backup.</span><span class="sxs-lookup"><span data-stu-id="ab823-239">Rather than specifying a “flat policy” for all backup points, you can specify different retention policies based on when the backup occurs.</span></span> <span data-ttu-id="ab823-240">È possibile modificare i criteri di conservazione giornalieri, settimanali, mensili e annuali in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="ab823-240">You can modify the daily, weekly, monthly, and yearly retention policies to meet your needs.</span></span>
9. <span data-ttu-id="ab823-241">Nella pagina Scegliere il tipo di backup iniziale selezionare il tipo di backup iniziale.</span><span class="sxs-lookup"><span data-stu-id="ab823-241">On the Choose Initial Backup Type page, choose the initial backup type.</span></span> <span data-ttu-id="ab823-242">Lasciare selezionata l'opzione **Automaticamente tramite la rete** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="ab823-242">Leave the option **Automatically over the network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="ab823-243">È possibile eseguire il backup automaticamente in rete oppure offline.</span><span class="sxs-lookup"><span data-stu-id="ab823-243">You can back up automatically over the network, or you can back up offline.</span></span> <span data-ttu-id="ab823-244">Il resto di questo articolo descrive il processo di backup automatico.</span><span class="sxs-lookup"><span data-stu-id="ab823-244">The remainder of this article describes the process for backing up automatically.</span></span> <span data-ttu-id="ab823-245">Se si preferisce eseguire un backup offline, vedere l'articolo [Flusso di lavoro di backup offline in Backup di Azure](backup-azure-backup-import-export.md) per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="ab823-245">If you prefer to do an offline backup, review the article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="ab823-246">Nella pagina Conferma esaminare le informazioni e fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="ab823-246">On the Confirmation page, review the information, and then click **Finish**.</span></span>
11. <span data-ttu-id="ab823-247">Dopo aver creato la pianificazione del backup tramite la procedura guidata, fare clic su **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="ab823-247">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="to-back-up-files-and-folders-for-the-first-time"></a><span data-ttu-id="ab823-248">Per eseguire il backup di file e cartelle per la prima volta</span><span class="sxs-lookup"><span data-stu-id="ab823-248">To back up files and folders for the first time</span></span>
1. <span data-ttu-id="ab823-249">Nell'agente di Servizi di ripristino fare clic su **Esegui backup** per completare il seeding iniziale sulla rete.</span><span class="sxs-lookup"><span data-stu-id="ab823-249">In the Recovery Services agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Eseguire ora il backup di Windows Server](./media/backup-try-azure-backup-in-10-mins/backup-now.png)
2. <span data-ttu-id="ab823-251">Nella pagina Conferma riesaminare le impostazioni che l'Esecuzione guidata backup userà per il backup del computer.</span><span class="sxs-lookup"><span data-stu-id="ab823-251">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="ab823-252">Fare clic su **Backup**.</span><span class="sxs-lookup"><span data-stu-id="ab823-252">Then click **Back Up**.</span></span>
3. <span data-ttu-id="ab823-253">Fare clic su **Chiudi** per chiudere la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="ab823-253">Click **Close** to close the wizard.</span></span> <span data-ttu-id="ab823-254">Se si chiude la procedura guidata prima che venga completato il processo di backup, l'esecuzione guidata proseguirà in background.</span><span class="sxs-lookup"><span data-stu-id="ab823-254">If you close the wizard before the backup process finishes, the wizard continues to run in the background.</span></span>

<span data-ttu-id="ab823-255">Al termine del backup iniziale, nella console Backup comparirà lo stato **Processo completato** .</span><span class="sxs-lookup"><span data-stu-id="ab823-255">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

![Completamento infrarossi](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="ab823-257">Domande?</span><span class="sxs-lookup"><span data-stu-id="ab823-257">Questions?</span></span>
<span data-ttu-id="ab823-258">In caso di domande o se si vuole che venga inclusa una funzionalità, è possibile [inviare commenti e suggerimenti](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="ab823-258">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab823-259">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ab823-259">Next steps</span></span>
* <span data-ttu-id="ab823-260">Sono disponibili altre informazioni sul [backup di computer Windows](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="ab823-260">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="ab823-261">Ora che si è eseguito il backup dei file e delle cartelle, è possibile [gestire l'insieme di credenziali e i server](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="ab823-261">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="ab823-262">Se è necessario ripristinare un backup, usare questo articolo per [ripristinare i file in un computer Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="ab823-262">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span></span>
