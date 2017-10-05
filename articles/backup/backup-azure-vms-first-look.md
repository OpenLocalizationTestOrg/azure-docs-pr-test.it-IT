---
title: 'Primo approccio: Eseguire il backup di VM di Azure con un insieme di credenziali di backup | Microsoft Docs'
description: Usare il portale classico per eseguire il backup di VM di Azure in un insieme di credenziali di backup. Questa esercitazione illustra tutte le fasi, che includono la creazione dell'insieme di credenziali di backup, la registrazione delle VM, la creazione dei criteri di backup e l'esecuzione del processo di backup iniziale.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 722820dc-b65f-425c-a9e5-c1946e896a87
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;
ms.openlocfilehash: fc31d7654e455ec5b4e4bb9af4cf1a166f1661ee
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a><span data-ttu-id="13b72-104">Primo approccio: Backup di macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="13b72-104">First look: Backing up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="13b72-105">Proteggere le VM con un insieme di credenziali dei servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="13b72-105">Protect VMs with a recovery services vault</span></span>](backup-azure-vms-first-look-arm.md)
> * [<span data-ttu-id="13b72-106">Proteggere le VM di Azure con un insieme di credenziali per il backup</span><span class="sxs-lookup"><span data-stu-id="13b72-106">Protect Azure VMs with a backup vault</span></span>](backup-azure-vms-first-look.md)
>
>

<span data-ttu-id="13b72-107">Questa esercitazione illustra i passaggi per eseguire il backup di una macchina virtuale di Azure in un insieme di credenziali di backup in Azure.</span><span class="sxs-lookup"><span data-stu-id="13b72-107">This tutorial takes you through the steps for backing up an Azure virtual machine (VM) to a backup vault in Azure.</span></span> <span data-ttu-id="13b72-108">Questo articolo descrive il modello di distribuzione classica o Service Manager per il backup di VM.</span><span class="sxs-lookup"><span data-stu-id="13b72-108">This article describes the classic model or Service Manager deployment model, for backing up VMs.</span></span> <span data-ttu-id="13b72-109">I passaggi seguenti si applicano solo agli insiemi di credenziali di backup creati nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="13b72-109">The following steps apply only to Backup vaults created in the classic portal.</span></span> <span data-ttu-id="13b72-110">Per le nuove distribuzioni è consigliabile usare il modello Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="13b72-110">Microsoft recommends using the Resource Manager model for new deployments.</span></span>

<span data-ttu-id="13b72-111">Per informazioni sul backup di una VM in un insieme di credenziali dei servizi di ripristino appartenente a un gruppo di risorse, vedere [Primo approccio: Proteggere le VM di Azure con un insieme di credenziali dei servizi di ripristino](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="13b72-111">If you are interested in backing up a VM to a Recovery Services vault that belongs to a Resource Group, see [First look: Protect VMs with a recovery services vault](backup-azure-vms-first-look-arm.md).</span></span>

<span data-ttu-id="13b72-112">Per completare l'esercitazione seguente, è necessario rispettare questi prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="13b72-112">To successfully complete the following tutorial, these prerequisites must exist:</span></span>

* <span data-ttu-id="13b72-113">È stata creata una VM nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="13b72-113">You have created a VM in your Azure subscription.</span></span>
* <span data-ttu-id="13b72-114">La VM può connettersi agli indirizzi IP pubblici di Azure.</span><span class="sxs-lookup"><span data-stu-id="13b72-114">The VM has connectivity to Azure public IP addresses.</span></span> <span data-ttu-id="13b72-115">Per altre informazioni, vedere [Connettività di rete](backup-azure-vms-prepare.md#network-connectivity).</span><span class="sxs-lookup"><span data-stu-id="13b72-115">For additional information, see [Network connectivity](backup-azure-vms-prepare.md#network-connectivity).</span></span>


> [!NOTE]
> <span data-ttu-id="13b72-116">Azure offre due modelli di distribuzione per creare e usare le risorse: [Resource Manager e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="13b72-116">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="13b72-117">Questa esercitazione si applica alle macchine virtuali create nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="13b72-117">This tutorial is for use with virtual machines created in the classic portal.</span></span>
>
>

## <a name="create-a-backup-vault"></a><span data-ttu-id="13b72-118">Creare un insieme di credenziali per il backup</span><span class="sxs-lookup"><span data-stu-id="13b72-118">Create a backup vault</span></span>
<span data-ttu-id="13b72-119">Un insieme di credenziali di backup è un'entità che archivia tutti i backup e i punti di ripristino che sono stati creati nel corso del tempo.</span><span class="sxs-lookup"><span data-stu-id="13b72-119">A backup vault is an entity that stores all the backups and recovery points that have been created over time.</span></span> <span data-ttu-id="13b72-120">L'insieme di credenziali di backup contiene anche i criteri di backup applicati alle macchine virtuali di cui viene eseguito il backup.</span><span class="sxs-lookup"><span data-stu-id="13b72-120">The backup vault also contains the backup policies that are applied to the virtual machines being backed up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="13b72-121">A partire da marzo 2017, non è più possibile usare il portale classico per creare insiemi di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="13b72-121">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
> <span data-ttu-id="13b72-122">È possibile aggiornare gli insiemi di credenziali di backup a insiemi di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="13b72-122">You can upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="13b72-123">Per altre informazioni, vedere l'articolo [Aggiornare un insieme di credenziali di Backup a un insieme di credenziali di Servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="13b72-123">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="13b72-124">Microsoft consiglia di aggiornare gli insiemi di credenziali di Backup a insiemi di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="13b72-124">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="13b72-125">Dopo il 15 ottobre 2017 non sarà possibile usare PowerShell per creare insiemi di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="13b72-125">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="13b72-126">**Entro il 1° novembre 2017**:</span><span class="sxs-lookup"><span data-stu-id="13b72-126">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="13b72-127">Tutti gli insiemi di credenziali di backup rimanenti verranno aggiornati automaticamente a insiemi di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="13b72-127">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="13b72-128">e non sarà più possibile accedere ai dati di backup nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="13b72-128">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="13b72-129">Sarà possibile invece usare il portale di Azure per accedere ai dati di backup negli insiemi di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="13b72-129">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="discover-and-register-azure-virtual-machines"></a><span data-ttu-id="13b72-130">Individuare e registrare le macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="13b72-130">Discover and Register Azure virtual machines</span></span>
<span data-ttu-id="13b72-131">Prima di registrare la VM con un insieme di credenziali, eseguire il processo di individuazione per identificare eventuali VM nuove.</span><span class="sxs-lookup"><span data-stu-id="13b72-131">Before registering the VM with a vault, run the discovery process to identify any new VMs.</span></span> <span data-ttu-id="13b72-132">Verrà restituito un elenco delle macchine virtuali disponibili nella sottoscrizione, insieme ad altre informazioni come il nome del servizio cloud e l'area.</span><span class="sxs-lookup"><span data-stu-id="13b72-132">This returns a list of virtual machines in the subscription, along with additional information like the cloud service name and the region.</span></span>

1. <span data-ttu-id="13b72-133">Accedere al [portale di Azure classico](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="13b72-133">Sign in to the [Azure Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="13b72-134">Nel portale di Azure classico fare clic su **Servizi di ripristino** per aprire l'elenco degli insiemi di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="13b72-134">In the Azure classic portal, click **Recovery Services** to open the list of Recovery Services vaults.</span></span>
    <span data-ttu-id="13b72-135">![Selezionare il carico di lavoro](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span><span class="sxs-lookup"><span data-stu-id="13b72-135">![Select workload](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span></span>
3. <span data-ttu-id="13b72-136">Nell'elenco di insiemi di credenziali selezionare quello da usare per il backup di una VM.</span><span class="sxs-lookup"><span data-stu-id="13b72-136">From the list of vaults, select the vault to back up a VM.</span></span>

    <span data-ttu-id="13b72-137">Quando si seleziona l'insieme di credenziali, viene visualizzata la pagina **Avvio rapido** .</span><span class="sxs-lookup"><span data-stu-id="13b72-137">When you select your vault, it opens in the **Quick Start** page</span></span>
4. <span data-ttu-id="13b72-138">Nel menu dell'insieme di credenziali fare clic su **Elementi registrati**.</span><span class="sxs-lookup"><span data-stu-id="13b72-138">From the vault menu, click **Registered Items**.</span></span>

    ![Selezionare il carico di lavoro](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. <span data-ttu-id="13b72-140">Scegliere **Macchina virtuale di Azure** dal menu **Tipo**.</span><span class="sxs-lookup"><span data-stu-id="13b72-140">From the **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Selezionare il carico di lavoro](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="13b72-142">Fare clic su **INDIVIDUA** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="13b72-142">Click **DISCOVER** at the bottom of the page.</span></span>
    <span data-ttu-id="13b72-143">![Pulsante Individua](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="13b72-143">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="13b72-144">Il processo di individuazione può richiedere alcuni minuti mentre le macchine virtuali vengono elencate in formato tabulare.</span><span class="sxs-lookup"><span data-stu-id="13b72-144">The discovery process may take a few minutes while the virtual machines are being tabulated.</span></span> <span data-ttu-id="13b72-145">Nella parte inferiore della schermata è presente una notifica che indica che il processo è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="13b72-145">There is a notification at the bottom of the screen that lets you know that the process is running.</span></span>

    ![Individuare le VM](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="13b72-147">Al termine del processo, la notifica cambia.</span><span class="sxs-lookup"><span data-stu-id="13b72-147">The notification changes when the process is complete.</span></span>

    ![Individuazione completata](./media/backup-azure-vms-first-look/discovery-complete.png)
7. <span data-ttu-id="13b72-149">Fare clic su **REGISTRA** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="13b72-149">Click **REGISTER** at the bottom of the page.</span></span>
    <span data-ttu-id="13b72-150">![Pulsante Registra](./media/backup-azure-vms-first-look/register-icon.png)</span><span class="sxs-lookup"><span data-stu-id="13b72-150">![Register button](./media/backup-azure-vms-first-look/register-icon.png)</span></span>
8. <span data-ttu-id="13b72-151">Nel menu di scelta rapida **Registra elementi** selezionare le macchine virtuali da registrare.</span><span class="sxs-lookup"><span data-stu-id="13b72-151">In the **Register Items** shortcut menu, select the virtual machines that you want to register.</span></span>

   > [!TIP]
   > <span data-ttu-id="13b72-152">È possibile registrare più macchine virtuali contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="13b72-152">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="13b72-153">Viene creato un processo per ogni macchina virtuale selezionata.</span><span class="sxs-lookup"><span data-stu-id="13b72-153">A job is created for each virtual machine that you've selected.</span></span>
9. <span data-ttu-id="13b72-154">Fare clic su **Visualizza processo** nella notifica per passare alla pagina **Processi**.</span><span class="sxs-lookup"><span data-stu-id="13b72-154">Click **View Job** in the notification to go to the **Jobs** page.</span></span>

    ![Registrare il processo](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="13b72-156">La macchina virtuale viene visualizzata anche nell'elenco di elementi registrati insieme allo stato dell'operazione di registrazione.</span><span class="sxs-lookup"><span data-stu-id="13b72-156">The virtual machine also appears in the list of registered items, along with the status of the registration operation.</span></span>

    ![Registering status 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="13b72-158">Al termine dell'operazione, lo stato diventerà *Registrazione completata* per riflettere la modifica.</span><span class="sxs-lookup"><span data-stu-id="13b72-158">When the operation completes, the status changes to reflect the *registered* state.</span></span>

    ![Registration status 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-the-vm-agent-on-the-virtual-machine"></a><span data-ttu-id="13b72-160">Installare l'agente di macchine virtuali nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="13b72-160">Install the VM Agent on the virtual machine</span></span>
<span data-ttu-id="13b72-161">Per il funzionamento dell'estensione di backup, l'agente di macchine virtuali deve essere installato nella macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="13b72-161">The Azure VM Agent must be installed on the Azure virtual machine for the Backup extension to work.</span></span> <span data-ttu-id="13b72-162">Se la VM è stata creata dalla raccolta di Azure, l'agente di macchine virtuali è già presente nella VM ed è possibile passare alla [protezione delle VM](backup-azure-vms-first-look.md#create-the-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="13b72-162">If your VM was created from the Azure gallery, the VM Agent is already present on the VM; you can skip to [protecting your VMs](backup-azure-vms-first-look.md#create-the-backup-policy).</span></span>

<span data-ttu-id="13b72-163">Se la migrazione della VM è stata eseguita da un data center locale, l'agente di macchine virtuali non è probabilmente installato nella VM.</span><span class="sxs-lookup"><span data-stu-id="13b72-163">If your VM migrated from an on-premises datacenter, the VM probably does not have the VM Agent installed.</span></span> <span data-ttu-id="13b72-164">Prima di procedere alla protezione della VM, è necessario installare l'agente di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="13b72-164">You must install the VM Agent on the virtual machine before proceeding to protect the VM.</span></span> <span data-ttu-id="13b72-165">Per informazioni dettagliate sull'installazione dell'agente di macchine virtuali, vedere la [sezione Agente di macchine virtuali dell'articolo sul backup di macchine virtuali](backup-azure-vms-prepare.md#vm-agent).</span><span class="sxs-lookup"><span data-stu-id="13b72-165">For detailed steps on installing the VM Agent, see the [VM Agent section of the Backup VMs article](backup-azure-vms-prepare.md#vm-agent).</span></span>

## <a name="create-the-backup-policy"></a><span data-ttu-id="13b72-166">Creare i criteri di backup</span><span class="sxs-lookup"><span data-stu-id="13b72-166">Create the backup policy</span></span>
<span data-ttu-id="13b72-167">Prima attivare il processo di backup iniziale, impostare la pianificazione per l'acquisizione degli snapshot di backup.</span><span class="sxs-lookup"><span data-stu-id="13b72-167">Before you trigger the initial backup job, set the schedule when backup snapshots are taken.</span></span> <span data-ttu-id="13b72-168">La pianificazione per l'acquisizione degli snapshot di backup e la durata di conservazione di questi snapshot costituiscono i criteri di backup.</span><span class="sxs-lookup"><span data-stu-id="13b72-168">The schedule when backup snapshots are taken, and the length of time those snapshots are retained, is the backup policy.</span></span> <span data-ttu-id="13b72-169">Le informazioni sul periodo di conservazione si basano sullo schema di rotazione dei backup GFS (Grandfather-Father-Son).</span><span class="sxs-lookup"><span data-stu-id="13b72-169">The retention information is based on Grandfather-father-son backup rotation scheme.</span></span>

1. <span data-ttu-id="13b72-170">Passare all'insieme di credenziali per il backup disponibile in **Servizi di ripristino** nel portale di Azure classico e fare clic su **Elementi registrati**.</span><span class="sxs-lookup"><span data-stu-id="13b72-170">Navigate to the backup vault under **Recovery Services** in the Azure Classic portal, and  click **Registered Items**.</span></span>
2. <span data-ttu-id="13b72-171">Selezionare **Macchina virtuale di Azure** dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="13b72-171">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![Select workload in portal](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="13b72-173">Fare clic su **PROTEGGI** in basso nella pagina.</span><span class="sxs-lookup"><span data-stu-id="13b72-173">Click **PROTECT** at the bottom of the page.</span></span>
    <span data-ttu-id="13b72-174">![Fare clic su Proteggi](./media/backup-azure-vms-first-look/protect-icon.png)</span><span class="sxs-lookup"><span data-stu-id="13b72-174">![Click Protect](./media/backup-azure-vms-first-look/protect-icon.png)</span></span>

    <span data-ttu-id="13b72-175">Verrà visualizzata la procedura guidata **Proteggi elementi** , che elenca *solo* le macchine virtuali registrate e non protette.</span><span class="sxs-lookup"><span data-stu-id="13b72-175">The **Protect Items wizard** appears and lists *only* virtual machines that are registered and not protected.</span></span>

    ![Configurare la protezione su vasta scala](./media/backup-azure-vms/protect-at-scale.png)
4. <span data-ttu-id="13b72-177">Selezionare le macchine virtuali da proteggere.</span><span class="sxs-lookup"><span data-stu-id="13b72-177">Select the virtual machines that you want to protect.</span></span>

    <span data-ttu-id="13b72-178">Se sono presenti due o più macchine virtuali con lo stesso nome, usare il servizio cloud per distinguerle.</span><span class="sxs-lookup"><span data-stu-id="13b72-178">If there are two or more virtual machines with the same name, use the Cloud Service to distinguish between the virtual machines.</span></span>
5. <span data-ttu-id="13b72-179">Nel menu **Configura protezione** selezionare i criteri esistenti o crearne di nuovi per proteggere le macchine virtuali identificate.</span><span class="sxs-lookup"><span data-stu-id="13b72-179">On the **Configure protection** menu select an existing policy or create a new policy to protect the virtual machines that you identified.</span></span>

    <span data-ttu-id="13b72-180">Ai nuovi insiemi di credenziali di backup sono associati criteri predefiniti.</span><span class="sxs-lookup"><span data-stu-id="13b72-180">New Backup vaults have a default policy associated with the vault.</span></span> <span data-ttu-id="13b72-181">Questi criteri acquisiscono uno snapshot giornaliero ogni sera, che viene mantenuto per 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="13b72-181">This policy takes a daily snapshot each evening, and the daily snapshot is retained for 30 days.</span></span> <span data-ttu-id="13b72-182">Ai singoli criteri di backup possono essere associate più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="13b72-182">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="13b72-183">Una macchina virtuale può tuttavia essere associata a un solo criterio alla volta.</span><span class="sxs-lookup"><span data-stu-id="13b72-183">However, the virtual machine can only be associated with one policy at a time.</span></span>

    ![Proteggere con nuovi criteri](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="13b72-185">I criteri di backup includono uno schema di conservazione per i backup pianificati.</span><span class="sxs-lookup"><span data-stu-id="13b72-185">A backup policy includes a retention scheme for the scheduled backups.</span></span> <span data-ttu-id="13b72-186">Se sono stati selezionati criteri di backup esistenti, non sarà possibile modificare le opzioni di conservazione nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="13b72-186">If you select an existing backup policy, you will be unable to modify the retention options in the next step.</span></span>
   >
   >
6. <span data-ttu-id="13b72-187">In **Intervallo conservazione** definire l'ambito giornaliero, settimanale, mensile e annuale per i punti di backup specifici.</span><span class="sxs-lookup"><span data-stu-id="13b72-187">On **Retention Range** define the daily, weekly, monthly, and yearly scope for the specific backup points.</span></span>

    ![Virtual machine is backed up with recovery point](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="13b72-189">I criteri di conservazione specificano il periodo di tempo per l'archiviazione di una copia di backup.</span><span class="sxs-lookup"><span data-stu-id="13b72-189">Retention policy specifies the length of time for storing a backup.</span></span> <span data-ttu-id="13b72-190">È possibile specificare criteri di conservazione diversi in base alla momento in cui viene eseguito il backup.</span><span class="sxs-lookup"><span data-stu-id="13b72-190">You can specify different retention policies based on when the backup is taken.</span></span>
7. <span data-ttu-id="13b72-191">Fare clic su **Processi** per visualizzare l'elenco dei processi in **Configura protezione**.</span><span class="sxs-lookup"><span data-stu-id="13b72-191">Click **Jobs** to view the list of **Configure Protection** jobs.</span></span>

    ![Configure protection job](./media/backup-azure-vms/protect-configureprotection.png)

    <span data-ttu-id="13b72-193">Dopo aver stabilito i criteri, andare al passaggio successivo ed eseguire il backup iniziale.</span><span class="sxs-lookup"><span data-stu-id="13b72-193">Now that you've established the policy, go to the next step and run the initial backup.</span></span>

## <a name="initial-backup"></a><span data-ttu-id="13b72-194">Backup iniziale</span><span class="sxs-lookup"><span data-stu-id="13b72-194">Initial backup</span></span>
<span data-ttu-id="13b72-195">Dopo aver protetto la macchina virtuale con i criteri specificati, è possibile visualizzare la relazione nella scheda **Elementi protetti** . Finché non viene eseguito il backup iniziale, **Stato di protezione** indica **Protetto (backup iniziale in sospeso)**.</span><span class="sxs-lookup"><span data-stu-id="13b72-195">Once a virtual machine has been protected with a policy, you can view that relationship on the **Protected Items** tab. Until the initial backup occurs, the **Protection Status** shows as **Protected - (pending initial backup)**.</span></span> <span data-ttu-id="13b72-196">Per impostazione predefinita, il primo backup pianificato è il *backup iniziale*.</span><span class="sxs-lookup"><span data-stu-id="13b72-196">By default, the first scheduled backup is the *initial backup*.</span></span>

![Backup in sospeso](./media/backup-azure-vms-first-look/protection-pending-border.png)

<span data-ttu-id="13b72-198">Per avviare il backup iniziale:</span><span class="sxs-lookup"><span data-stu-id="13b72-198">To start the initial backup now:</span></span>

1. <span data-ttu-id="13b72-199">In basso nella pagina **Elementi protetti** fare clic su **Esegui backup ora**.</span><span class="sxs-lookup"><span data-stu-id="13b72-199">On the **Protected Items** page, click **Backup Now** at the bottom of the page.</span></span>
    <span data-ttu-id="13b72-200">![Icona Esegui backup ora](./media/backup-azure-vms-first-look/backup-now-icon.png)</span><span class="sxs-lookup"><span data-stu-id="13b72-200">![Backup Now icon](./media/backup-azure-vms-first-look/backup-now-icon.png)</span></span>

    <span data-ttu-id="13b72-201">Il servizio Backup di Azure crea un processo di backup per l'operazione di backup iniziale.</span><span class="sxs-lookup"><span data-stu-id="13b72-201">The Azure Backup service creates a backup job for the initial backup operation.</span></span>
2. <span data-ttu-id="13b72-202">Fare clic sulla scheda **Processi** per visualizzare l'elenco dei processi.</span><span class="sxs-lookup"><span data-stu-id="13b72-202">Click the **Jobs** tab to view the list of jobs.</span></span>

    ![Backup in progress](./media/backup-azure-vms-first-look/protect-inprogress.png)

    <span data-ttu-id="13b72-204">Al termine del backup iniziale, lo stato della macchina virtuale nella scheda **Elementi protetti** sarà *Protetto*.</span><span class="sxs-lookup"><span data-stu-id="13b72-204">When initial backup is complete, the status of the virtual machine in the **Protected Items** tab is *Protected*.</span></span>

    ![Virtual machine is backed up with recovery point](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > <span data-ttu-id="13b72-206">Il backup di macchine virtuali è un processo locale.</span><span class="sxs-lookup"><span data-stu-id="13b72-206">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="13b72-207">Non è possibile eseguire il backup di macchine virtuali di un'area in un insieme di credenziali per il backup in un'altra area.</span><span class="sxs-lookup"><span data-stu-id="13b72-207">You cannot back up virtual machines from one region to a backup vault in another region.</span></span> <span data-ttu-id="13b72-208">Di conseguenza, per ogni area di Azure in cui sono presenti VM per cui deve essere eseguito il backup, è necessario creare almeno un insieme di credenziali per il backup in quell'area.</span><span class="sxs-lookup"><span data-stu-id="13b72-208">So, for every Azure region that has VMs that need to be backed up, at least one backup vault must be created in that region.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="13b72-209">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="13b72-209">Next steps</span></span>
<span data-ttu-id="13b72-210">Ora che è stato eseguito il backup di una macchina virtuale, sono disponibili diversi passaggi successivi interessanti.</span><span class="sxs-lookup"><span data-stu-id="13b72-210">Now that you have successfully backed up a VM, there are several next steps that could be of interest.</span></span> <span data-ttu-id="13b72-211">Il passaggio più logico consiste nell'acquisire familiarità con il ripristino dei dati in una VM.</span><span class="sxs-lookup"><span data-stu-id="13b72-211">The most logical step is to familiarize yourself with restoring data to a VM.</span></span> <span data-ttu-id="13b72-212">Esistono tuttavia attività di gestione che aiutano a comprendere come proteggere i dati e ridurre al minimo i costi.</span><span class="sxs-lookup"><span data-stu-id="13b72-212">However, there are management tasks that will help you understand how to keep your data safe and minimize costs.</span></span>

* [<span data-ttu-id="13b72-213">Gestire e monitorare il backup delle macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="13b72-213">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="13b72-214">Ripristino di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="13b72-214">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
* [<span data-ttu-id="13b72-215">Guida alla risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="13b72-215">Troubleshooting guidance</span></span>](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a><span data-ttu-id="13b72-216">Domande?</span><span class="sxs-lookup"><span data-stu-id="13b72-216">Questions?</span></span>
<span data-ttu-id="13b72-217">In caso di domande o se si vuole che venga inclusa una funzionalità, è possibile [inviare commenti e suggerimenti](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="13b72-217">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>
