---
title: Usare l'agente di Azure Backup per eseguire il backup di file e cartelle | Documentazione Microsoft
description: Usare l'agente di Backup di Microsoft Azure per eseguire il backup di file e cartelle Windows in Azure. Creare un insieme di credenziali di Servizi di ripristino, installare l'agente di Backup, definire i criteri di backup ed eseguire il backup iniziale di file e cartelle.
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
ms.openlocfilehash: b95dc0a83d8e5618effb573353f419e1837d30c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-a-windows-server-or-client-to-azure-using-the-resource-manager-deployment-model"></a><span data-ttu-id="d470d-105">Eseguire il backup di un client o server Windows in Azure con Backup di Azure usando il modello di distribuzione Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d470d-105">Back up a Windows Server or client to Azure using the Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d470d-106">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d470d-106">Azure portal</span></span>](backup-configure-vault.md)
> * [<span data-ttu-id="d470d-107">Portale classico</span><span class="sxs-lookup"><span data-stu-id="d470d-107">Classic portal</span></span>](backup-configure-vault-classic.md)
>
>

<span data-ttu-id="d470d-108">Questo articolo illustra come eseguire il backup di file e cartelle di Windows Server o di un client Windows in Azure con Backup di Azure tramite il modello di distribuzione di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d470d-108">This article explains how to back up your Windows Server (or Windows client) files and folders to Azure with Azure Backup using the Resource Manager deployment model.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![Passaggi del processo di backup](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a><span data-ttu-id="d470d-110">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="d470d-110">Before you start</span></span>
<span data-ttu-id="d470d-111">Per eseguire il backup di un server o un client in Azure, è necessario un account Azure.</span><span class="sxs-lookup"><span data-stu-id="d470d-111">To back up a server or client to Azure, you need an Azure account.</span></span> <span data-ttu-id="d470d-112">Se non si ha un account, è possibile crearne uno [gratuito](https://azure.microsoft.com/free/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="d470d-112">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="d470d-113">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="d470d-113">Create a Recovery Services vault</span></span>
<span data-ttu-id="d470d-114">Un insieme di credenziali dei servizi di ripristino è un'entità che archivia tutti i backup e i punti di ripristino che sono stati creati nel corso del tempo.</span><span class="sxs-lookup"><span data-stu-id="d470d-114">A Recovery Services vault is an entity that stores all the backups and recovery points you create over time.</span></span> <span data-ttu-id="d470d-115">L'insieme di credenziali dei servizi di ripristino contiene anche i criteri di backup applicati ai file e alle cartelle protette.</span><span class="sxs-lookup"><span data-stu-id="d470d-115">The Recovery Services vault also contains the backup policy applied to the protected files and folders.</span></span> <span data-ttu-id="d470d-116">Quando si crea un insieme di credenziali dei servizi di ripristino, è necessario selezionare anche l'opzione di ridondanza di archiviazione appropriata.</span><span class="sxs-lookup"><span data-stu-id="d470d-116">When you create a Recovery Services vault, you should also select the appropriate storage redundancy option.</span></span>

### <a name="to-create-a-recovery-services-vault"></a><span data-ttu-id="d470d-117">Per creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="d470d-117">To create a Recovery Services vault</span></span>
1. <span data-ttu-id="d470d-118">Se questa operazione non è già stata eseguita, accedere al [portale di Azure](https://portal.azure.com/) , tramite la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d470d-118">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="d470d-119">Scegliere **Altri servizi** dal menu Hub e nell'elenco di risorse digitare **Servizi di ripristino**, quindi fare clic su **Insiemi di credenziali dei servizi di ripristino**.</span><span class="sxs-lookup"><span data-stu-id="d470d-119">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="d470d-121">Se presenti nella sottoscrizione, gli insiemi di credenziali dei servizi di ripristino vengono elencati.</span><span class="sxs-lookup"><span data-stu-id="d470d-121">If there are recovery services vaults in the subscription, the vaults are listed.</span></span>

3. <span data-ttu-id="d470d-122">Scegliere **Aggiungi** dal menu **Insiemi di credenziali dei servizi di ripristino**.</span><span class="sxs-lookup"><span data-stu-id="d470d-122">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="d470d-124">Verrà visualizzato il pannello degli insiemi di credenziali dei servizi di ripristino, in cui viene richiesto di specificare **Nome**, **Sottoscrizione**, **Gruppo di risorse** e **Località**.</span><span class="sxs-lookup"><span data-stu-id="d470d-124">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="d470d-126">Nel campo **Nome**digitare un nome descrittivo per identificare l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="d470d-126">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="d470d-127">Il nome deve essere univoco per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d470d-127">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="d470d-128">Digitare un nome che contenga tra i 2 e i 50 caratteri.</span><span class="sxs-lookup"><span data-stu-id="d470d-128">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="d470d-129">Deve iniziare con una lettera e può contenere solo lettere, numeri e trattini.</span><span class="sxs-lookup"><span data-stu-id="d470d-129">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="d470d-130">Nella sezione **Sottoscrizione** usare il menu a discesa per scegliere la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d470d-130">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="d470d-131">Se si usa una sola sottoscrizione, questa verrà visualizzata e sarà possibile andare al passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="d470d-131">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="d470d-132">Se non si è certi di quale sottoscrizione usare, usare la sottoscrizione predefinita (o suggerita).</span><span class="sxs-lookup"><span data-stu-id="d470d-132">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="d470d-133">Sono disponibili più scelte solo se l'account dell'organizzazione è associato a più sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="d470d-133">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="d470d-134">Nella sezione **Gruppo di risorse**:</span><span class="sxs-lookup"><span data-stu-id="d470d-134">In the **Resource group** section:</span></span>

    * <span data-ttu-id="d470d-135">Selezionare **Crea nuovo** per creare un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="d470d-135">select **Create new** if you want to create a new Resource group.</span></span>
    <span data-ttu-id="d470d-136">Or</span><span class="sxs-lookup"><span data-stu-id="d470d-136">Or</span></span>
    * <span data-ttu-id="d470d-137">Selezionare **Usa esistente** e fare clic sul menu a discesa per visualizzare l'elenco di gruppi di risorse disponibili.</span><span class="sxs-lookup"><span data-stu-id="d470d-137">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="d470d-138">Per informazioni complete sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d470d-138">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="d470d-139">Fare clic su **Località** per selezionare l'area geografica per l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="d470d-139">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="d470d-140">La scelta determina l'area geografica in cui vengono inviati i dati di backup.</span><span class="sxs-lookup"><span data-stu-id="d470d-140">This choice determines the geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="d470d-141">Nella parte inferiore del pannello Insieme di credenziali dei servizi di ripristino fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d470d-141">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

  <span data-ttu-id="d470d-142">La creazione dell'insieme di credenziali dei servizi di ripristino può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="d470d-142">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="d470d-143">Monitorare le notifiche di stato nell'area superiore destra del portale.</span><span class="sxs-lookup"><span data-stu-id="d470d-143">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="d470d-144">L'insieme di credenziali, dopo essere stato creato, viene visualizzato negli insiemi di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="d470d-144">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="d470d-145">Se l'insieme di credenziali non viene visualizzato dopo qualche minuto, fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="d470d-145">If after several minutes you don't see your vault, click **Refresh**.</span></span>

  ![Fare clic sul pulsante Aggiorna](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  <span data-ttu-id="d470d-147">Dopo la visualizzazione dell'insieme di credenziali nell'elenco corrispondente per i Servizi di ripristino, è possibile configurare la ridondanza di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d470d-147">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>


### <a name="set-storage-redundancy"></a><span data-ttu-id="d470d-148">Impostare la ridondanza di archiviazione</span><span class="sxs-lookup"><span data-stu-id="d470d-148">Set storage redundancy</span></span>
<span data-ttu-id="d470d-149">Quando si crea per la prima volta un insieme di credenziali di Servizi di ripristino, si determina come replicare lo spazio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d470d-149">When you first create a Recovery Services vault you determine how storage is replicated.</span></span>

1. <span data-ttu-id="d470d-150">Nel pannello **Insieme di credenziali dei servizi di ripristino** fare clic sul nuovo insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="d470d-150">From the **Recovery Services vaults** blade, click the new vault.</span></span>

    ![Selezionare il nuovo insieme di credenziali dall'elenco corrispondente per Servizi di ripristino](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="d470d-152">Quando si seleziona l'insieme di credenziali, il pannello **Insieme di credenziali dei servizi di ripristino** si restringe e vengono aperti il pannello Impostazioni,*con il nome dell'insieme di credenziali nella parte superiore*, e il pannello dei dettagli dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="d470d-152">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span></span>

    ![Visualizzare la configurazione dell'archiviazione per il nuovo insieme di credenziali](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. <span data-ttu-id="d470d-154">Nel pannello Impostazioni del nuovo insieme di credenziali usare il dispositivo di scorrimento verticale per passare alla sezione Gestisci e fare clic su **Infrastruttura di backup**.</span><span class="sxs-lookup"><span data-stu-id="d470d-154">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>

  <span data-ttu-id="d470d-155">Verrà visualizzato il pannello Infrastruttura di backup.</span><span class="sxs-lookup"><span data-stu-id="d470d-155">The Backup Infrastructure blade opens.</span></span>

3. <span data-ttu-id="d470d-156">Nel pannello Infrastruttura di backup fare clic su **Configurazione backup** per aprire il pannello **Configurazione backup**.</span><span class="sxs-lookup"><span data-stu-id="d470d-156">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

  ![Impostare la configurazione dell'archiviazione per il nuovo insieme di credenziali](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)

4. <span data-ttu-id="d470d-158">Scegliere l'opzione di replica di archiviazione appropriata per l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="d470d-158">Choose the appropriate storage replication option for your vault.</span></span>

  ![opzioni di configurazione dell'archiviazione](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

  <span data-ttu-id="d470d-160">Per impostazione predefinita, l'insieme di credenziali prevede l'archiviazione con ridondanza geografica.</span><span class="sxs-lookup"><span data-stu-id="d470d-160">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="d470d-161">Se si usa Azure come endpoint di archiviazione di backup primario, continuare a usare l'opzione **Con ridondanza geografica**.</span><span class="sxs-lookup"><span data-stu-id="d470d-161">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="d470d-162">Se non si usa Azure come endpoint di archiviazione di backup primario, scegliere l'opzione **Con ridondanza locale**, che riduce i costi di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d470d-162">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="d470d-163">Per altre informazioni sulle opzioni di archiviazione [con ridondanza geografica](../storage/common/storage-redundancy.md#geo-redundant-storage) e [con ridondanza locale](../storage/common/storage-redundancy.md#locally-redundant-storage), vedere [Panoramica della ridondanza di archiviazione](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="d470d-163">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="d470d-164">Dopo avere creato un insieme di credenziali, preparare l'infrastruttura per il backup di file e cartelle scaricando e installando l'agente di Servizi di ripristino di Microsoft Azure, scaricando le credenziali dell'insieme di credenziali e usandole per registrare l'agente con l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="d470d-164">Now that you've created a vault, prepare your infrastructure to back up files and folders by downloading and installing the Microsoft Azure Recovery Services agent, downloading vault credentials, and then using those credentials to register the agent with the vault.</span></span>

## <a name="configure-the-vault"></a><span data-ttu-id="d470d-165">Configurare l'insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="d470d-165">Configure the vault</span></span>

1. <span data-ttu-id="d470d-166">Nel pannello dell'insieme di credenziali dei servizi di ripristino appena creato, nella sezione Attività iniziali fare clic su **Backup** e nel pannello **Introduzione al backup** selezionare **Obiettivo del backup**.</span><span class="sxs-lookup"><span data-stu-id="d470d-166">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span></span>

  ![Aprire il Pannello Obiettivo di backup](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  <span data-ttu-id="d470d-168">Verrà visualizzato il pannello **Obiettivo del backup**.</span><span class="sxs-lookup"><span data-stu-id="d470d-168">The **Backup Goal** blade opens.</span></span> <span data-ttu-id="d470d-169">Se l'insieme di credenziali di Servizi di ripristino è stato configurato in precedenza, viene visualizzato il pannello **Obiettivo del backup** quando si fa clic su **Backup** nel pannello dell'insieme di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="d470d-169">If the Recovery Services vault has been previously configured, then the **Backup Goal** blades opens when you click **Backup** on the Recovery Services vault blade.</span></span>

  ![Aprire il Pannello Obiettivo di backup](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="d470d-171">Scegliere **Locale** dal menu a discesa **Posizione di esecuzione del carico di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="d470d-171">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

  <span data-ttu-id="d470d-172">Si sceglie **Locale** perché il server di Windows o il computer Windows è un computer fisico che non si trova in Azure.</span><span class="sxs-lookup"><span data-stu-id="d470d-172">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="d470d-173">Scegliere **File e cartelle** dal menu **Elementi di cui eseguire il backup**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d470d-173">From the **What do you want to backup?** menu, select **Files and folders**, and click **OK**.</span></span>

  ![Configurazione di file e cartelle](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

  <span data-ttu-id="d470d-175">Dopo aver fatto clic su OK verrà visualizzato un segno di spunta accanto a **Obiettivo del backup** e si aprirà il pannello **Preparare l'infrastruttura**.</span><span class="sxs-lookup"><span data-stu-id="d470d-175">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span></span>

  ![Preparare l'infrastruttura dopo aver configurato l'obiettivo del backup](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="d470d-177">Nel pannello **Preparare l'infrastruttura** fare clic su **Scaricare l'agente per Windows Server o Windows Client**.</span><span class="sxs-lookup"><span data-stu-id="d470d-177">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

  ![Preparare l'infrastruttura](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

  <span data-ttu-id="d470d-179">Se si usa Windows Server Essentials, scegliere di scaricare l'agente per Windows Server Essentials.</span><span class="sxs-lookup"><span data-stu-id="d470d-179">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span></span> <span data-ttu-id="d470d-180">Un menu a comparsa chiederà di eseguire o salvare MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="d470d-180">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span></span>

  ![Finestra di dialogo di MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="d470d-182">Fare clic su **Salva** nel menu a comparsa del download.</span><span class="sxs-lookup"><span data-stu-id="d470d-182">In the download pop-up menu, click **Save**.</span></span>

  <span data-ttu-id="d470d-183">Per impostazione predefinita, il file **MARSagentinstaller.exe** viene salvato nella cartella Downloads.</span><span class="sxs-lookup"><span data-stu-id="d470d-183">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span></span> <span data-ttu-id="d470d-184">Al termine del programma di installazione verrà visualizzato un messaggio popup che chiede se eseguire il programma di installazione o aprire la cartella.</span><span class="sxs-lookup"><span data-stu-id="d470d-184">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span></span>

  ![Preparare l'infrastruttura](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

  <span data-ttu-id="d470d-186">Non è ancora necessario installare l'agente.</span><span class="sxs-lookup"><span data-stu-id="d470d-186">You don't need to install the agent yet.</span></span> <span data-ttu-id="d470d-187">È possibile installare l'agente al termine del download delle credenziali dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="d470d-187">You can install the agent after you have downloaded the vault credentials.</span></span>

6. <span data-ttu-id="d470d-188">Fare clic su **Scarica** nel pannello **Preparare l'infrastruttura**.</span><span class="sxs-lookup"><span data-stu-id="d470d-188">On the **Prepare infrastructure** blade, click **Download**.</span></span>

  ![Scaricare le credenziali dell'insieme di credenziali](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

  <span data-ttu-id="d470d-190">Le credenziali dell'insieme di credenziali verranno scaricate nella cartella Download locale.</span><span class="sxs-lookup"><span data-stu-id="d470d-190">The vault credentials download to your Downloads folder.</span></span> <span data-ttu-id="d470d-191">Al termine del download delle credenziali dell'insieme di credenziali verrà visualizzato un messaggio popup che chiede se aprire o salvare le credenziali.</span><span class="sxs-lookup"><span data-stu-id="d470d-191">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span></span> <span data-ttu-id="d470d-192">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="d470d-192">Click **Save**.</span></span> <span data-ttu-id="d470d-193">Se si fa clic accidentalmente su **Apri**, attendere che il tentativo di apertura delle credenziali termini con un errore.</span><span class="sxs-lookup"><span data-stu-id="d470d-193">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span></span> <span data-ttu-id="d470d-194">Non è possibile aprire le credenziali dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="d470d-194">You cannot open the vault credentials.</span></span> <span data-ttu-id="d470d-195">Procedere con il passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="d470d-195">Proceed to the next step.</span></span> <span data-ttu-id="d470d-196">Le credenziali dell'insieme di credenziali si trovano nella cartella Downloads.</span><span class="sxs-lookup"><span data-stu-id="d470d-196">The vault credentials are in the Downloads folder.</span></span>   

  ![Il download delle credenziali dell'insieme di credenziali è terminato](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-the-agent"></a><span data-ttu-id="d470d-198">Installare e registrare l'agente</span><span class="sxs-lookup"><span data-stu-id="d470d-198">Install and register the agent</span></span>

> [!NOTE]
> <span data-ttu-id="d470d-199">L'abilitazione del backup tramite il portale di Azure non è ancora disponibile.</span><span class="sxs-lookup"><span data-stu-id="d470d-199">Enabling backup through the Azure portal is not available, yet.</span></span> <span data-ttu-id="d470d-200">Usare l'agente di Servizi di ripristino di Microsoft Azure per eseguire il backup di file e cartelle.</span><span class="sxs-lookup"><span data-stu-id="d470d-200">Use the Microsoft Azure Recovery Services Agent to back up your files and folders.</span></span>
>

1. <span data-ttu-id="d470d-201">Cercare e fare doppio clic sul file **MARSagentinstaller.exe** nella cartella Downloads o nella cartella in cui è stato salvato.</span><span class="sxs-lookup"><span data-stu-id="d470d-201">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span></span>

  <span data-ttu-id="d470d-202">Il programma di installazione visualizzerà una serie di messaggi durante l'estrazione, l'installazione e la registrazione dell'agente di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="d470d-202">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span></span>

  ![Eseguire il programma di installazione dell'agente di Servizi di ripristino](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="d470d-204">Completare l'Installazione guidata di Agente servizi di ripristino di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d470d-204">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="d470d-205">Per completare la procedura guidata, è necessario:</span><span class="sxs-lookup"><span data-stu-id="d470d-205">To complete the wizard, you need to:</span></span>

  * <span data-ttu-id="d470d-206">Scegliere un percorso per la cartella di installazione e della cache.</span><span class="sxs-lookup"><span data-stu-id="d470d-206">Choose a location for the installation and cache folder.</span></span>
  * <span data-ttu-id="d470d-207">Fornire le informazioni sul server proxy se si usa un server proxy per connettersi a Internet.</span><span class="sxs-lookup"><span data-stu-id="d470d-207">Provide your proxy server info if you use a proxy server to connect to the internet.</span></span>
  * <span data-ttu-id="d470d-208">Se si usa un proxy autenticato, immettere il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="d470d-208">Provide your user name and password details if you use an authenticated proxy.</span></span>
  * <span data-ttu-id="d470d-209">Fornire le credenziali dell'insieme di credenziali scaricate.</span><span class="sxs-lookup"><span data-stu-id="d470d-209">Provide the downloaded vault credentials</span></span>
  * <span data-ttu-id="d470d-210">Salvare la passphrase di crittografia in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="d470d-210">Save the encryption passphrase in a secure location.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d470d-211">Se la passphrase viene persa o dimenticata, Microsoft non potrà offrire assistenza per il recupero dei dati di backup.</span><span class="sxs-lookup"><span data-stu-id="d470d-211">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span></span> <span data-ttu-id="d470d-212">Salvare il file in una posizione sicura.</span><span class="sxs-lookup"><span data-stu-id="d470d-212">Save the file in a secure location.</span></span> <span data-ttu-id="d470d-213">È necessario per ripristinare un backup.</span><span class="sxs-lookup"><span data-stu-id="d470d-213">It is required to restore a backup.</span></span>
  >
  >

<span data-ttu-id="d470d-214">L'agente ora è installato e il computer è registrato nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="d470d-214">The agent is now installed and your machine is registered to the vault.</span></span> <span data-ttu-id="d470d-215">Ora è possibile configurare e pianificare il backup.</span><span class="sxs-lookup"><span data-stu-id="d470d-215">You're ready to configure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="d470d-216">Requisiti di rete e connettività</span><span class="sxs-lookup"><span data-stu-id="d470d-216">Network and Connectivity Requirements</span></span>

<span data-ttu-id="d470d-217">Se il computer/proxy ha un accesso a Internet limitato, verificare che le impostazioni del firewall sul computer/proxy siano configurate per consentire gli URL seguenti:</span><span class="sxs-lookup"><span data-stu-id="d470d-217">If your machine/proxy has limited internet access, ensure that firewall settings on the machine/proxy are configured to allow the following URLs:</span></span> <br>
    1. <span data-ttu-id="d470d-218">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="d470d-218">www.msftncsi.com</span></span>
    2. <span data-ttu-id="d470d-219">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="d470d-219">*.Microsoft.com</span></span>
    3. <span data-ttu-id="d470d-220">windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="d470d-220">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="d470d-221">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="d470d-221">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="d470d-222">*. windows.ne</span><span class="sxs-lookup"><span data-stu-id="d470d-222">*.windows.ne</span></span>


## <a name="create-the-backup-policy"></a><span data-ttu-id="d470d-223">Creare i criteri di backup</span><span class="sxs-lookup"><span data-stu-id="d470d-223">Create the backup policy</span></span>
<span data-ttu-id="d470d-224">I criteri di backup costituiscono la pianificazione per l'acquisizione degli snapshot di backup e la durata di conservazione di questi snapshot.</span><span class="sxs-lookup"><span data-stu-id="d470d-224">The backup policy is the schedule when recovery points are taken, and the length of time the recovery points are retained.</span></span> <span data-ttu-id="d470d-225">Usare l'agente di Backup di Microsoft Azure per creare il criterio di backup di file e cartelle.</span><span class="sxs-lookup"><span data-stu-id="d470d-225">Use the Microsoft Azure Backup agent to create the backup policy for files and folders.</span></span>

### <a name="to-create-a-backup-schedule"></a><span data-ttu-id="d470d-226">Per creare una pianificazione di backup</span><span class="sxs-lookup"><span data-stu-id="d470d-226">To create a backup schedule</span></span>
1. <span data-ttu-id="d470d-227">Aprire l'agente Backup di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d470d-227">Open the Microsoft Azure Backup agent.</span></span> <span data-ttu-id="d470d-228">È possibile trovarlo se si cerca **Backup di Microsoft Azure**nel computer.</span><span class="sxs-lookup"><span data-stu-id="d470d-228">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Avviare Azure Backup Agent](./media/backup-configure-vault/snap-in-search.png)
2. <span data-ttu-id="d470d-230">Nel riquadro **Azioni** dell'agente di Backup fare clic su **Pianifica backup** per avviare la Pianificazione guidata backup.</span><span class="sxs-lookup"><span data-stu-id="d470d-230">In the Backup agent's **Actions** pane, click **Schedule Backup** to launch the Schedule Backup Wizard.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-configure-vault/schedule-first-backup.png)

3. <span data-ttu-id="d470d-232">Nella pagina **Attività iniziali** della Pianificazione guidata backup fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d470d-232">On the **Getting started** page of the Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="d470d-233">Nella pagina **Seleziona elementi per backup** fare clic su **Aggiungi elementi**.</span><span class="sxs-lookup"><span data-stu-id="d470d-233">On the **Select Items to Backup** page, click **Add Items**.</span></span>

  <span data-ttu-id="d470d-234">Verrà visualizzata la finestra di dialogo Seleziona elementi.</span><span class="sxs-lookup"><span data-stu-id="d470d-234">The Select Items dialog opens.</span></span>

5. <span data-ttu-id="d470d-235">Selezionare i file e le cartelle da proteggere e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d470d-235">Select the files and folders that you want to protect, and then click **OK**.</span></span>
6. <span data-ttu-id="d470d-236">Nella pagina **Seleziona elementi per backup** fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d470d-236">In the **Select Items to Backup** page, click **Next**.</span></span>
7. <span data-ttu-id="d470d-237">Nella pagina **Specificare la pianificazione del backup** specificare la pianificazione del backup e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d470d-237">On the **Specify Backup Schedule** page, specify the backup schedule and click **Next**.</span></span>

    <span data-ttu-id="d470d-238">È possibile pianificare backup giornalieri, da eseguire non più di tre volte al giorno, o settimanali.</span><span class="sxs-lookup"><span data-stu-id="d470d-238">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Elementi per il backup di Windows Server](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="d470d-240">Per altre informazioni su come specificare la pianificazione del backup vedere l'articolo [Usare Backup di Azure per sostituire l'infrastruttura basata su nastro](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="d470d-240">For more information about how to specify the backup schedule, see the article [Use Azure Backup to replace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >

8. <span data-ttu-id="d470d-241">Nella pagina **Seleziona i criteri di conservazione** selezionare i criteri di conservazione specifici per la copia di backup e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d470d-241">On the **Select Retention Policy** page, choose the specific retention policies the for the backup copy and click **Next**.</span></span>

    <span data-ttu-id="d470d-242">I criteri di conservazione specificano il periodo di tempo per cui il backup verrà archiviato.</span><span class="sxs-lookup"><span data-stu-id="d470d-242">The retention policy specifies the duration which the backup is stored.</span></span> <span data-ttu-id="d470d-243">Anziché specificare solo un "criterio semplice" per tutti i punti di backup, è possibile specificare criteri di conservazione diversi in base al momento in cui viene eseguito il backup.</span><span class="sxs-lookup"><span data-stu-id="d470d-243">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when the backup occurs.</span></span> <span data-ttu-id="d470d-244">È possibile modificare i criteri di conservazione giornalieri, settimanali, mensili e annuali in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="d470d-244">You can modify the daily, weekly, monthly, and yearly retention policies to meet your needs.</span></span>
9. <span data-ttu-id="d470d-245">Nella pagina Scegliere il tipo di backup iniziale selezionare il tipo di backup iniziale.</span><span class="sxs-lookup"><span data-stu-id="d470d-245">On the Choose Initial Backup Type page, choose the initial backup type.</span></span> <span data-ttu-id="d470d-246">Lasciare selezionata l'opzione **Automaticamente tramite la rete** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d470d-246">Leave the option **Automatically over the network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="d470d-247">È possibile eseguire il backup automaticamente in rete oppure offline.</span><span class="sxs-lookup"><span data-stu-id="d470d-247">You can back up automatically over the network, or you can back up offline.</span></span> <span data-ttu-id="d470d-248">Il resto di questo articolo descrive il processo di backup automatico.</span><span class="sxs-lookup"><span data-stu-id="d470d-248">The remainder of this article describes the process for backing up automatically.</span></span> <span data-ttu-id="d470d-249">Se si preferisce eseguire un backup offline, vedere l'articolo [Flusso di lavoro di backup offline in Backup di Azure](backup-azure-backup-import-export.md) per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="d470d-249">If you prefer to do an offline backup, review the article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="d470d-250">Nella pagina Conferma esaminare le informazioni e fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="d470d-250">On the Confirmation page, review the information, and then click **Finish**.</span></span>
11. <span data-ttu-id="d470d-251">Dopo aver creato la pianificazione del backup tramite la procedura guidata, fare clic su **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="d470d-251">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="d470d-252">Abilitare la limitazione della larghezza di banda</span><span class="sxs-lookup"><span data-stu-id="d470d-252">Enable network throttling</span></span>
<span data-ttu-id="d470d-253">L'agente di Microsoft Backup di Azure consente di limitare la larghezza di banda della rete.</span><span class="sxs-lookup"><span data-stu-id="d470d-253">The Microsoft Azure Backup agent provides network throttling.</span></span> <span data-ttu-id="d470d-254">La limitazione controlla l'uso della larghezza di banda della rete durante il trasferimento dati.</span><span class="sxs-lookup"><span data-stu-id="d470d-254">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="d470d-255">Questo controllo può essere utile se è necessario eseguire il backup dei dati durante l'orario di lavoro, ma senza che il processo di backup interferisca con il resto del traffico Internet.</span><span class="sxs-lookup"><span data-stu-id="d470d-255">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other Internet traffic.</span></span> <span data-ttu-id="d470d-256">La limitazione si applica alle attività di backup e ripristino.</span><span class="sxs-lookup"><span data-stu-id="d470d-256">Throttling applies to back up and restore activities.</span></span>

> [!NOTE]
> <span data-ttu-id="d470d-257">La limitazione di rete non è disponibile su Windows Server 2008 R2 SP1, Windows Server 2008 SP2 o Windows 7 (con i pacchetti di servizio).</span><span class="sxs-lookup"><span data-stu-id="d470d-257">Network throttling is not available on Windows Server 2008 R2 SP1, Windows Server 2008 SP2, or Windows 7 (with service packs).</span></span> <span data-ttu-id="d470d-258">La funzione di limitazione della rete di Backup di Azure attiva il QoS ( Quality of Service) sul sistema operativo locale.</span><span class="sxs-lookup"><span data-stu-id="d470d-258">The Azure Backup network throttling feature engages Quality of Service (QoS) on the local operating system.</span></span> <span data-ttu-id="d470d-259">Anche se il Backup di Azure è in grado di proteggere questi sistemi operativi, la versione del QoS disponibile su queste piattaforme non funziona con la limitazione di rete di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="d470d-259">Though Azure Backup can protect these operating systems, the version of QoS available on these platforms doesn't work with Azure Backup network throttling.</span></span> <span data-ttu-id="d470d-260">La limitazione di rete può essere utilizzata in tutti gli altri [sistemi operativi supportati](backup-azure-backup-faq.md).</span><span class="sxs-lookup"><span data-stu-id="d470d-260">Network throttling can be used on all other [supported operating systems](backup-azure-backup-faq.md).</span></span>
>
>

<span data-ttu-id="d470d-261">**Per abilitare la limitazione larghezza di banda**</span><span class="sxs-lookup"><span data-stu-id="d470d-261">**To enable network throttling**</span></span>

1. <span data-ttu-id="d470d-262">Nell'agente di Backup di Microsoft Azure fare clic su **Modifica proprietà**.</span><span class="sxs-lookup"><span data-stu-id="d470d-262">In the Microsoft Azure Backup agent, click **Change Properties**.</span></span>

    ![Modifica proprietà](./media/backup-configure-vault/change-properties.png)
2. <span data-ttu-id="d470d-264">Nella scheda **Limitazione larghezza di banda rete** selezionare la casella di controllo **Abilita la limitazione all'utilizzo della larghezza di banda Internet per le operazioni di backup**.</span><span class="sxs-lookup"><span data-stu-id="d470d-264">On the **Throttling** tab, select the **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![Limitazione della larghezza di banda della rete](./media/backup-configure-vault/throttling-dialog.png)
3. <span data-ttu-id="d470d-266">Dopo aver abilitato la limitazione, specificare la larghezza di banda consentita per trasferire i dati di backup durante le **ore lavorative** e le **ore non lavorative**.</span><span class="sxs-lookup"><span data-stu-id="d470d-266">After you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="d470d-267">I valori della larghezza di banda partono da 512 kilobit al secondo (Kbps) e possono arrivare fino a 1.023 megabyte al secondo (Mbps).</span><span class="sxs-lookup"><span data-stu-id="d470d-267">The bandwidth values begin at 512 kilobits per second (Kbps) and can go up to 1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="d470d-268">È anche possibile definire l'inizio e la fine delle **ore lavorative**e i giorni della settimana da considerare come giorni lavorativi.</span><span class="sxs-lookup"><span data-stu-id="d470d-268">You can also designate the start and finish for **Work hours**, and which days of the week are considered work days.</span></span> <span data-ttu-id="d470d-269">Gli orari al di fuori delle ore lavorative definite vengono considerati ore non lavorative.</span><span class="sxs-lookup"><span data-stu-id="d470d-269">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="d470d-270">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d470d-270">Click **OK**.</span></span>

### <a name="to-back-up-files-and-folders-for-the-first-time"></a><span data-ttu-id="d470d-271">Per eseguire il backup di file e cartelle per la prima volta</span><span class="sxs-lookup"><span data-stu-id="d470d-271">To back up files and folders for the first time</span></span>
1. <span data-ttu-id="d470d-272">Nell'agente di Backup fare clic su **Esegui backup** per completare il seeding iniziale sulla rete.</span><span class="sxs-lookup"><span data-stu-id="d470d-272">In the backup agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Eseguire ora il backup di Windows Server](./media/backup-configure-vault/backup-now.png)
2. <span data-ttu-id="d470d-274">Nella pagina Conferma riesaminare le impostazioni che l'Esecuzione guidata backup userà per il backup del computer.</span><span class="sxs-lookup"><span data-stu-id="d470d-274">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="d470d-275">Fare clic su **Backup**.</span><span class="sxs-lookup"><span data-stu-id="d470d-275">Then click **Back Up**.</span></span>
3. <span data-ttu-id="d470d-276">Fare clic su **Chiudi** per chiudere la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="d470d-276">Click **Close** to close the wizard.</span></span> <span data-ttu-id="d470d-277">Se quest'operazione viene svolta prima che venga completato il processo di backup, l'esecuzione guidata proseguirà in background.</span><span class="sxs-lookup"><span data-stu-id="d470d-277">If you do this before the backup process finishes, the wizard continues to run in the background.</span></span>

<span data-ttu-id="d470d-278">Al termine del backup iniziale, nella console Backup comparirà lo stato **Processo completato** .</span><span class="sxs-lookup"><span data-stu-id="d470d-278">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

![Completamento infrarossi](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="d470d-280">Domande?</span><span class="sxs-lookup"><span data-stu-id="d470d-280">Questions?</span></span>
<span data-ttu-id="d470d-281">In caso di domande o se si vuole che venga inclusa una funzionalità, è possibile [inviare commenti e suggerimenti](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="d470d-281">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d470d-282">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d470d-282">Next steps</span></span>
<span data-ttu-id="d470d-283">Per altre informazioni sul backup di macchine virtuali o altri carichi di lavoro, vedere:</span><span class="sxs-lookup"><span data-stu-id="d470d-283">For additional information about backing up VMs or other workloads, see:</span></span>

* <span data-ttu-id="d470d-284">Ora che si è eseguito il backup dei file e delle cartelle, è possibile [gestire l'insieme di credenziali e i server](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="d470d-284">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="d470d-285">Se è necessario ripristinare un backup, usare questo articolo per [ripristinare i file in un computer Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="d470d-285">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span></span>
