---
title: 'Primo approccio: Eseguire il backup di VM di Azure con un insieme di credenziali di backup | Microsoft Docs'
description: Utilizzare hello tooback portale classico di insieme di credenziali Backup tooa macchine virtuali di Azure. In questa esercitazione illustra tutte le fasi, tra cui la creazione di credenziali di Backup hello, la registrazione delle macchine virtuali di hello, creazione di criteri di backup e in esecuzione il processo di backup iniziale di hello.
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
ms.openlocfilehash: 77700e69eab9faccbc7ef923e1eb4e1f97be75d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a><span data-ttu-id="f73fe-104">Primo approccio: Backup di macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="f73fe-104">First look: Backing up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f73fe-105">Proteggere le VM con un insieme di credenziali dei servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="f73fe-105">Protect VMs with a recovery services vault</span></span>](backup-azure-vms-first-look-arm.md)
> * [<span data-ttu-id="f73fe-106">Proteggere le VM di Azure con un insieme di credenziali per il backup</span><span class="sxs-lookup"><span data-stu-id="f73fe-106">Protect Azure VMs with a backup vault</span></span>](backup-azure-vms-first-look.md)
>
>

<span data-ttu-id="f73fe-107">In questa esercitazione illustra i passaggi di hello per il backup di un archivio di backup tooa macchina virtuale di Azure (VM) in Azure.</span><span class="sxs-lookup"><span data-stu-id="f73fe-107">This tutorial takes you through hello steps for backing up an Azure virtual machine (VM) tooa backup vault in Azure.</span></span> <span data-ttu-id="f73fe-108">Questo articolo descrive il modello classico di hello o modello di distribuzione di Service Manager, per il backup di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="f73fe-108">This article describes hello classic model or Service Manager deployment model, for backing up VMs.</span></span> <span data-ttu-id="f73fe-109">Hello passaggi seguenti si applicano solo tooBackup gli insiemi di credenziali creati nel portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="f73fe-109">hello following steps apply only tooBackup vaults created in hello classic portal.</span></span> <span data-ttu-id="f73fe-110">Si consiglia di utilizzare il modello di gestione risorse hello per le nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="f73fe-110">Microsoft recommends using hello Resource Manager model for new deployments.</span></span>

<span data-ttu-id="f73fe-111">Se si desidera eseguire il backup di un archivio di servizi di ripristino tooa VM appartenente tooa gruppo di risorse, vedere [innanzitutto: proteggere macchine virtuali con un insieme di credenziali di servizi di ripristino](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="f73fe-111">If you are interested in backing up a VM tooa Recovery Services vault that belongs tooa Resource Group, see [First look: Protect VMs with a recovery services vault](backup-azure-vms-first-look-arm.md).</span></span>

<span data-ttu-id="f73fe-112">toosuccessfully completare seguente hello esercitazione devono essere presente questi prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="f73fe-112">toosuccessfully complete hello following tutorial, these prerequisites must exist:</span></span>

* <span data-ttu-id="f73fe-113">È stata creata una VM nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f73fe-113">You have created a VM in your Azure subscription.</span></span>
* <span data-ttu-id="f73fe-114">Hello macchina virtuale dispone di connettività tooAzure indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="f73fe-114">hello VM has connectivity tooAzure public IP addresses.</span></span> <span data-ttu-id="f73fe-115">Per altre informazioni, vedere [Connettività di rete](backup-azure-vms-prepare.md#network-connectivity).</span><span class="sxs-lookup"><span data-stu-id="f73fe-115">For additional information, see [Network connectivity](backup-azure-vms-prepare.md#network-connectivity).</span></span>


> [!NOTE]
> <span data-ttu-id="f73fe-116">Azure offre due modelli di distribuzione per creare e usare le risorse: [Resource Manager e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f73fe-116">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f73fe-117">In questa esercitazione viene utilizzato con le macchine virtuali create nel portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="f73fe-117">This tutorial is for use with virtual machines created in hello classic portal.</span></span>
>
>

## <a name="create-a-backup-vault"></a><span data-ttu-id="f73fe-118">Creare un insieme di credenziali per il backup</span><span class="sxs-lookup"><span data-stu-id="f73fe-118">Create a backup vault</span></span>
<span data-ttu-id="f73fe-119">Un insieme di credenziali di backup è un'entità contenente tutti i backup di hello e i punti di ripristino che sono stati creati nel corso del tempo.</span><span class="sxs-lookup"><span data-stu-id="f73fe-119">A backup vault is an entity that stores all hello backups and recovery points that have been created over time.</span></span> <span data-ttu-id="f73fe-120">insieme di credenziali backup Hello contiene anche i criteri di backup hello che vengono applicati toohello le macchine virtuali viene eseguito il backup.</span><span class="sxs-lookup"><span data-stu-id="f73fe-120">hello backup vault also contains hello backup policies that are applied toohello virtual machines being backed up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f73fe-121">A partire da marzo 2017, è possibile utilizzare non è più insiemi di credenziali Backup hello toocreate portale classico.</span><span class="sxs-lookup"><span data-stu-id="f73fe-121">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
> <span data-ttu-id="f73fe-122">È possibile aggiornare i servizi archivi di Backup gli insiemi di credenziali tooRecovery.</span><span class="sxs-lookup"><span data-stu-id="f73fe-122">You can upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="f73fe-123">Per informazioni dettagliate, vedere l'articolo hello [aggiornare un tooa insieme di credenziali di Backup dell'insieme di credenziali di servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="f73fe-123">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="f73fe-124">Microsoft incoraggia gli utenti tooupgrade insiemi di credenziali di servizi tooRecovery insiemi di credenziali di Backup.</span><span class="sxs-lookup"><span data-stu-id="f73fe-124">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="f73fe-125">Dopo 15 ottobre 2017, è possibile utilizzare gli insiemi di credenziali di PowerShell toocreate Backup.</span><span class="sxs-lookup"><span data-stu-id="f73fe-125">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="f73fe-126">**Entro il 1° novembre 2017**:</span><span class="sxs-lookup"><span data-stu-id="f73fe-126">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="f73fe-127">Tutti gli archivi di Backup rimanenti verrà automaticamente aggiornato tooRecovery servizi insiemi di credenziali.</span><span class="sxs-lookup"><span data-stu-id="f73fe-127">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="f73fe-128">Si sarà in grado di tooaccess ai dati di backup nel portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="f73fe-128">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="f73fe-129">Utilizzare invece hello Azure tooaccess portale i dati di backup in insiemi di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="f73fe-129">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="discover-and-register-azure-virtual-machines"></a><span data-ttu-id="f73fe-130">Individuare e registrare le macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="f73fe-130">Discover and Register Azure virtual machines</span></span>
<span data-ttu-id="f73fe-131">Prima di registrare hello macchina virtuale con un insieme di credenziali, eseguire tooidentify processo di individuazione hello nuove macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="f73fe-131">Before registering hello VM with a vault, run hello discovery process tooidentify any new VMs.</span></span> <span data-ttu-id="f73fe-132">Viene restituito un elenco di macchine virtuali nella sottoscrizione di hello, insieme a informazioni aggiuntive come nome del servizio cloud hello e area hello.</span><span class="sxs-lookup"><span data-stu-id="f73fe-132">This returns a list of virtual machines in hello subscription, along with additional information like hello cloud service name and hello region.</span></span>

1. <span data-ttu-id="f73fe-133">Accedi toohello [portale di Azure classico](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="f73fe-133">Sign in toohello [Azure Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="f73fe-134">Nel portale di Azure classico hello, fare clic su **servizi di ripristino** elenco hello tooopen degli insiemi di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="f73fe-134">In hello Azure classic portal, click **Recovery Services** tooopen hello list of Recovery Services vaults.</span></span>
    <span data-ttu-id="f73fe-135">![Selezionare il carico di lavoro](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span><span class="sxs-lookup"><span data-stu-id="f73fe-135">![Select workload](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span></span>
3. <span data-ttu-id="f73fe-136">Hello l'elenco degli insiemi di credenziali, selezionare hello insieme di credenziali tooback una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f73fe-136">From hello list of vaults, select hello vault tooback up a VM.</span></span>

    <span data-ttu-id="f73fe-137">Quando si seleziona l'insieme di credenziali, aprirla in hello **avvio rapido** pagina</span><span class="sxs-lookup"><span data-stu-id="f73fe-137">When you select your vault, it opens in hello **Quick Start** page</span></span>
4. <span data-ttu-id="f73fe-138">Dal menu di hello insieme di credenziali, fare clic su **elementi registrati**.</span><span class="sxs-lookup"><span data-stu-id="f73fe-138">From hello vault menu, click **Registered Items**.</span></span>

    ![Selezionare il carico di lavoro](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. <span data-ttu-id="f73fe-140">Da hello **tipo** dal menu **macchina virtuale di Azure**.</span><span class="sxs-lookup"><span data-stu-id="f73fe-140">From hello **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Selezionare il carico di lavoro](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="f73fe-142">Fare clic su **DISCOVER** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="f73fe-142">Click **DISCOVER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="f73fe-143">![Pulsante Individua](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="f73fe-143">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="f73fe-144">il processo di individuazione Hello potrebbe richiedere alcuni minuti hello le macchine virtuali sono in elencati in formato tabulare.</span><span class="sxs-lookup"><span data-stu-id="f73fe-144">hello discovery process may take a few minutes while hello virtual machines are being tabulated.</span></span> <span data-ttu-id="f73fe-145">Vi è una notifica nella parte inferiore di hello della schermata Ciao che informa che il processo di hello sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f73fe-145">There is a notification at hello bottom of hello screen that lets you know that hello process is running.</span></span>

    ![Individuare le VM](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="f73fe-147">notifica Hello cambia quando il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="f73fe-147">hello notification changes when hello process is complete.</span></span>

    ![Individuazione completata](./media/backup-azure-vms-first-look/discovery-complete.png)
7. <span data-ttu-id="f73fe-149">Fare clic su **registrare** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="f73fe-149">Click **REGISTER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="f73fe-150">![Pulsante Registra](./media/backup-azure-vms-first-look/register-icon.png)</span><span class="sxs-lookup"><span data-stu-id="f73fe-150">![Register button](./media/backup-azure-vms-first-look/register-icon.png)</span></span>
8. <span data-ttu-id="f73fe-151">In hello **registrare elementi** menu di scelta rapida, hello selezionare le macchine virtuali che si desidera tooregister.</span><span class="sxs-lookup"><span data-stu-id="f73fe-151">In hello **Register Items** shortcut menu, select hello virtual machines that you want tooregister.</span></span>

   > [!TIP]
   > <span data-ttu-id="f73fe-152">È possibile registrare più macchine virtuali contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="f73fe-152">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="f73fe-153">Viene creato un processo per ogni macchina virtuale selezionata.</span><span class="sxs-lookup"><span data-stu-id="f73fe-153">A job is created for each virtual machine that you've selected.</span></span>
9. <span data-ttu-id="f73fe-154">Fare clic su **Visualizza processo** in hello notifica toogo toohello **processi** pagina.</span><span class="sxs-lookup"><span data-stu-id="f73fe-154">Click **View Job** in hello notification toogo toohello **Jobs** page.</span></span>

    ![Registrare il processo](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="f73fe-156">macchina virtuale Hello viene visualizzato anche nell'elenco di hello degli elementi registrati, insieme allo stato di hello dell'operazione di registrazione hello.</span><span class="sxs-lookup"><span data-stu-id="f73fe-156">hello virtual machine also appears in hello list of registered items, along with hello status of hello registration operation.</span></span>

    ![Registering status 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="f73fe-158">Al termine dell'operazione di hello, lo stato di hello cambia hello tooreflect *registrato* stato.</span><span class="sxs-lookup"><span data-stu-id="f73fe-158">When hello operation completes, hello status changes tooreflect hello *registered* state.</span></span>

    ![Registration status 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a><span data-ttu-id="f73fe-160">Installare hello agente della macchina virtuale nella macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="f73fe-160">Install hello VM Agent on hello virtual machine</span></span>
<span data-ttu-id="f73fe-161">Hello agente VM di Azure deve essere installato nella macchina virtuale di Azure per hello Backup estensione toowork hello.</span><span class="sxs-lookup"><span data-stu-id="f73fe-161">hello Azure VM Agent must be installed on hello Azure virtual machine for hello Backup extension toowork.</span></span> <span data-ttu-id="f73fe-162">Se la macchina virtuale è stata creata da una raccolta di Azure hello, hello agente VM è già presente nella macchina virtuale; hello è possibile ignorare troppo[protegge le macchine virtuali](backup-azure-vms-first-look.md#create-the-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="f73fe-162">If your VM was created from hello Azure gallery, hello VM Agent is already present on hello VM; you can skip too[protecting your VMs](backup-azure-vms-first-look.md#create-the-backup-policy).</span></span>

<span data-ttu-id="f73fe-163">Se la macchina virtuale eseguita la migrazione da un data center locale, hello VM probabilmente non dispone di hello che agente VM installato.</span><span class="sxs-lookup"><span data-stu-id="f73fe-163">If your VM migrated from an on-premises datacenter, hello VM probably does not have hello VM Agent installed.</span></span> <span data-ttu-id="f73fe-164">È necessario installare hello agente della macchina virtuale nella macchina virtuale hello hello tooprotect procedere macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f73fe-164">You must install hello VM Agent on hello virtual machine before proceeding tooprotect hello VM.</span></span> <span data-ttu-id="f73fe-165">Per i passaggi dettagliati per l'installazione di hello agente VM, vedere hello [sezione agente di macchine Virtuali dell'articolo di macchine virtuali Backup hello](backup-azure-vms-prepare.md#vm-agent).</span><span class="sxs-lookup"><span data-stu-id="f73fe-165">For detailed steps on installing hello VM Agent, see hello [VM Agent section of hello Backup VMs article](backup-azure-vms-prepare.md#vm-agent).</span></span>

## <a name="create-hello-backup-policy"></a><span data-ttu-id="f73fe-166">Creare criteri di backup hello</span><span class="sxs-lookup"><span data-stu-id="f73fe-166">Create hello backup policy</span></span>
<span data-ttu-id="f73fe-167">Prima attivare il processo di backup iniziale di hello, pianificare hello quando vengono eseguiti gli snapshot di backup.</span><span class="sxs-lookup"><span data-stu-id="f73fe-167">Before you trigger hello initial backup job, set hello schedule when backup snapshots are taken.</span></span> <span data-ttu-id="f73fe-168">Hello pianificare gli snapshot di backup vengono eseguiti e hello di questi snapshot del periodo di tempo vengono mantenute, è criteri di backup hello.</span><span class="sxs-lookup"><span data-stu-id="f73fe-168">hello schedule when backup snapshots are taken, and hello length of time those snapshots are retained, is hello backup policy.</span></span> <span data-ttu-id="f73fe-169">informazioni di memorizzazione Hello si basano sullo schema di rotazione dei backup nonno-padre-figlio.</span><span class="sxs-lookup"><span data-stu-id="f73fe-169">hello retention information is based on Grandfather-father-son backup rotation scheme.</span></span>

1. <span data-ttu-id="f73fe-170">Passare l'insieme di credenziali backup toohello in **servizi di ripristino** in hello portale di Azure classico, quindi fare clic su **elementi registrati**.</span><span class="sxs-lookup"><span data-stu-id="f73fe-170">Navigate toohello backup vault under **Recovery Services** in hello Azure Classic portal, and  click **Registered Items**.</span></span>
2. <span data-ttu-id="f73fe-171">Selezionare **macchina virtuale di Azure** dal menu a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="f73fe-171">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![Select workload in portal](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="f73fe-173">Fare clic su **PROTEGGI** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="f73fe-173">Click **PROTECT** at hello bottom of hello page.</span></span>
    <span data-ttu-id="f73fe-174">![Fare clic su Protezione](./media/backup-azure-vms-first-look/protect-icon.png)</span><span class="sxs-lookup"><span data-stu-id="f73fe-174">![Click Protect](./media/backup-azure-vms-first-look/protect-icon.png)</span></span>

    <span data-ttu-id="f73fe-175">Hello **guidata proteggere elementi** sono elencati *solo* macchine virtuali che vengono registrate e non protetti.</span><span class="sxs-lookup"><span data-stu-id="f73fe-175">hello **Protect Items wizard** appears and lists *only* virtual machines that are registered and not protected.</span></span>

    ![Configurare la protezione su vasta scala](./media/backup-azure-vms/protect-at-scale.png)
4. <span data-ttu-id="f73fe-177">Selezionare le macchine virtuali hello che si desidera tooprotect.</span><span class="sxs-lookup"><span data-stu-id="f73fe-177">Select hello virtual machines that you want tooprotect.</span></span>

    <span data-ttu-id="f73fe-178">Se sono presenti due o più macchine virtuali con hello stesso nome, utilizzare hello servizio Cloud toodistinguish tra le macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="f73fe-178">If there are two or more virtual machines with hello same name, use hello Cloud Service toodistinguish between hello virtual machines.</span></span>
5. <span data-ttu-id="f73fe-179">In hello **configurare la protezione** menu selezionare un criterio esistente o creare un nuovo tooprotect criteri macchine virtuali hello identificato.</span><span class="sxs-lookup"><span data-stu-id="f73fe-179">On hello **Configure protection** menu select an existing policy or create a new policy tooprotect hello virtual machines that you identified.</span></span>

    <span data-ttu-id="f73fe-180">Nuovi archivi di Backup dispone di un criterio predefinito associato all'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="f73fe-180">New Backup vaults have a default policy associated with hello vault.</span></span> <span data-ttu-id="f73fe-181">Questo criterio ha quotidianamente snapshot ogni sera e snapshot giornaliero hello vengono mantenuti per 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="f73fe-181">This policy takes a daily snapshot each evening, and hello daily snapshot is retained for 30 days.</span></span> <span data-ttu-id="f73fe-182">Ai singoli criteri di backup possono essere associate più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="f73fe-182">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="f73fe-183">Tuttavia, hello macchina virtuale può essere solo associata a un criterio alla volta.</span><span class="sxs-lookup"><span data-stu-id="f73fe-183">However, hello virtual machine can only be associated with one policy at a time.</span></span>

    ![Proteggere con nuovi criteri](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="f73fe-185">Un criterio di backup include uno schema di memorizzazione per i backup pianificato hello.</span><span class="sxs-lookup"><span data-stu-id="f73fe-185">A backup policy includes a retention scheme for hello scheduled backups.</span></span> <span data-ttu-id="f73fe-186">Se si seleziona un criterio di backup, le opzioni di memorizzazione hello toomodify Impossibile sarà nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="f73fe-186">If you select an existing backup policy, you will be unable toomodify hello retention options in hello next step.</span></span>
   >
   >
6. <span data-ttu-id="f73fe-187">In **mantenimento** definire hello giornaliera, settimanale, mensile e annuo ambito per i punti di backup specifico hello.</span><span class="sxs-lookup"><span data-stu-id="f73fe-187">On **Retention Range** define hello daily, weekly, monthly, and yearly scope for hello specific backup points.</span></span>

    ![Virtual machine is backed up with recovery point](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="f73fe-189">Criteri di conservazione specificano durata hello per archiviare un backup.</span><span class="sxs-lookup"><span data-stu-id="f73fe-189">Retention policy specifies hello length of time for storing a backup.</span></span> <span data-ttu-id="f73fe-190">È possibile specificare i criteri di conservazione diversi in base a quando viene eseguito il backup di hello.</span><span class="sxs-lookup"><span data-stu-id="f73fe-190">You can specify different retention policies based on when hello backup is taken.</span></span>
7. <span data-ttu-id="f73fe-191">Fare clic su **processi** tooview hello elenco **configurazione della protezione** processi.</span><span class="sxs-lookup"><span data-stu-id="f73fe-191">Click **Jobs** tooview hello list of **Configure Protection** jobs.</span></span>

    ![Configure protection job](./media/backup-azure-vms/protect-configureprotection.png)

    <span data-ttu-id="f73fe-193">Ora che è stato stabilito criteri hello, passare passaggio successivo toohello ed eseguire il backup iniziale hello.</span><span class="sxs-lookup"><span data-stu-id="f73fe-193">Now that you've established hello policy, go toohello next step and run hello initial backup.</span></span>

## <a name="initial-backup"></a><span data-ttu-id="f73fe-194">Backup iniziale</span><span class="sxs-lookup"><span data-stu-id="f73fe-194">Initial backup</span></span>
<span data-ttu-id="f73fe-195">Una volta che una macchina virtuale è stata protetta con un criterio, è possibile visualizzare tale relazione nella hello **elementi protetti** scheda. Fino a quando non hello iniziale backup viene eseguito, hello **lo stato di protezione** viene illustrato come **Protected - (in sospeso il backup iniziale)**.</span><span class="sxs-lookup"><span data-stu-id="f73fe-195">Once a virtual machine has been protected with a policy, you can view that relationship on hello **Protected Items** tab. Until hello initial backup occurs, hello **Protection Status** shows as **Protected - (pending initial backup)**.</span></span> <span data-ttu-id="f73fe-196">Per impostazione predefinita, backup pianificato prima hello è hello *backup iniziale*.</span><span class="sxs-lookup"><span data-stu-id="f73fe-196">By default, hello first scheduled backup is hello *initial backup*.</span></span>

![Backup in sospeso](./media/backup-azure-vms-first-look/protection-pending-border.png)

<span data-ttu-id="f73fe-198">toostart hello backup iniziale ora:</span><span class="sxs-lookup"><span data-stu-id="f73fe-198">toostart hello initial backup now:</span></span>

1. <span data-ttu-id="f73fe-199">In hello **elementi protetti** pagina, fare clic su **Esegui Backup** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="f73fe-199">On hello **Protected Items** page, click **Backup Now** at hello bottom of hello page.</span></span>
    <span data-ttu-id="f73fe-200">![Icona Esegui backup ora](./media/backup-azure-vms-first-look/backup-now-icon.png)</span><span class="sxs-lookup"><span data-stu-id="f73fe-200">![Backup Now icon](./media/backup-azure-vms-first-look/backup-now-icon.png)</span></span>

    <span data-ttu-id="f73fe-201">Hello servizio Backup di Azure crea un processo di backup per l'operazione di backup iniziale hello.</span><span class="sxs-lookup"><span data-stu-id="f73fe-201">hello Azure Backup service creates a backup job for hello initial backup operation.</span></span>
2. <span data-ttu-id="f73fe-202">Fare clic su hello **processi** elenco della scheda tooview hello dei processi.</span><span class="sxs-lookup"><span data-stu-id="f73fe-202">Click hello **Jobs** tab tooview hello list of jobs.</span></span>

    ![Backup in progress](./media/backup-azure-vms-first-look/protect-inprogress.png)

    <span data-ttu-id="f73fe-204">Quando il backup iniziale è stato completato, lo stato di hello della macchina virtuale hello in hello **elementi protetti** scheda *Protected*.</span><span class="sxs-lookup"><span data-stu-id="f73fe-204">When initial backup is complete, hello status of hello virtual machine in hello **Protected Items** tab is *Protected*.</span></span>

    ![Virtual machine is backed up with recovery point](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > <span data-ttu-id="f73fe-206">Il backup di macchine virtuali è un processo locale.</span><span class="sxs-lookup"><span data-stu-id="f73fe-206">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="f73fe-207">È possibile eseguire il backup di macchine virtuali da una regione tooa insieme di credenziali backup in un'altra area.</span><span class="sxs-lookup"><span data-stu-id="f73fe-207">You cannot back up virtual machines from one region tooa backup vault in another region.</span></span> <span data-ttu-id="f73fe-208">In tal caso, per ogni area di Azure con macchine virtuali che devono toobe eseguito il backup, è necessario creare almeno un insieme di credenziali di backup in tale area.</span><span class="sxs-lookup"><span data-stu-id="f73fe-208">So, for every Azure region that has VMs that need toobe backed up, at least one backup vault must be created in that region.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="f73fe-209">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f73fe-209">Next steps</span></span>
<span data-ttu-id="f73fe-210">Ora che è stato eseguito il backup di una macchina virtuale, sono disponibili diversi passaggi successivi interessanti.</span><span class="sxs-lookup"><span data-stu-id="f73fe-210">Now that you have successfully backed up a VM, there are several next steps that could be of interest.</span></span> <span data-ttu-id="f73fe-211">passaggio più logica Hello è toofamiliarize manualmente con il ripristino di dati tooa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f73fe-211">hello most logical step is toofamiliarize yourself with restoring data tooa VM.</span></span> <span data-ttu-id="f73fe-212">Tuttavia, vi sono attività di gestione che consentono di comprendere come tookeep dati sicuri e ridurre al minimo i costi.</span><span class="sxs-lookup"><span data-stu-id="f73fe-212">However, there are management tasks that will help you understand how tookeep your data safe and minimize costs.</span></span>

* [<span data-ttu-id="f73fe-213">Gestire e monitorare il backup delle macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="f73fe-213">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="f73fe-214">Ripristino di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="f73fe-214">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
* [<span data-ttu-id="f73fe-215">Guida alla risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="f73fe-215">Troubleshooting guidance</span></span>](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a><span data-ttu-id="f73fe-216">Domande?</span><span class="sxs-lookup"><span data-stu-id="f73fe-216">Questions?</span></span>
<span data-ttu-id="f73fe-217">Se si hanno domande o se è presente una funzionalità che si desidera toosee incluso, [inviare commenti e suggerimenti](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="f73fe-217">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>
