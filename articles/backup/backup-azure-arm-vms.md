---
title: aaaBack le macchine virtuali di Azure | Documenti Microsoft
description: Individuare, registrare e il backup dell'insieme di credenziali di macchine virtuali di Azure tooa recovery services.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: backup della macchina virtuale; eseguire il backup della macchina virtuale; backup e ripristino di emergenza; backup di vm di ARM
ms.assetid: 5c68481d-7be3-4e68-b87c-0961c267053e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: trinadhk;jimpark;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a204a42726450a7fd89b5563a786b5070578b113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-tooa-recovery-services-vault"></a><span data-ttu-id="28c48-104">Eseguire il backup di macchine virtuali di Azure insieme di credenziali di servizi di ripristino tooa</span><span class="sxs-lookup"><span data-stu-id="28c48-104">Back up Azure virtual machines tooa Recovery Services vault</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="28c48-105">Eseguire il backup dell'insieme di credenziali di macchine virtuali tooRecovery servizi</span><span class="sxs-lookup"><span data-stu-id="28c48-105">Back up VMs tooRecovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="28c48-106">Eseguire il backup dell'insieme di credenziali tooBackup macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="28c48-106">Back up VMs tooBackup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="28c48-107">In questo articolo illustra in dettaglio come insieme di credenziali tooback backup di macchine virtuali di Azure (distribuzione di gestione risorse e distribuito classica) tooa servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="28c48-107">This article details how tooback up Azure VMs (both Resource Manager-deployed and Classic-deployed) tooa Recovery Services vault.</span></span> <span data-ttu-id="28c48-108">La maggior parte del lavoro hello per il backup di macchine virtuali è preparazione hello.</span><span class="sxs-lookup"><span data-stu-id="28c48-108">Most of hello work for backing up VMs is hello preparation.</span></span> <span data-ttu-id="28c48-109">Prima di poter eseguire il backup o proteggere una macchina virtuale, è necessario completare hello [prerequisiti](backup-azure-arm-vms-prepare.md) tooprepare l'ambiente per la protezione delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="28c48-109">Before you can back up or protect a VM, you must complete hello [prerequisites](backup-azure-arm-vms-prepare.md) tooprepare your environment for protecting your VMs.</span></span> <span data-ttu-id="28c48-110">Dopo aver completato i prerequisiti di hello, è possibile avviare gli snapshot tootake di hello operazione di backup della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="28c48-110">Once you have completed hello prerequisites, then you can initiate hello backup operation tootake snapshots of your VM.</span></span>


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

<span data-ttu-id="28c48-111">Per ulteriori informazioni, vedere gli articoli di hello in [pianificazione dell'infrastruttura di backup di VM in Azure](backup-azure-vms-introduction.md) e [macchine virtuali di Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="28c48-111">For more information, see hello articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

## <a name="triggering-hello-backup-job"></a><span data-ttu-id="28c48-112">Attivazione hello processo di backup</span><span class="sxs-lookup"><span data-stu-id="28c48-112">Triggering hello backup job</span></span>
<span data-ttu-id="28c48-113">i criteri di backup Hello associato hello che insieme di credenziali di servizi di ripristino definiscono la frequenza e quando viene eseguito l'operazione di backup hello.</span><span class="sxs-lookup"><span data-stu-id="28c48-113">hello backup policy associated with hello Recovery Services vault defines how often and when hello backup operation runs.</span></span> <span data-ttu-id="28c48-114">Per impostazione predefinita, hello prima pianificati backup corrisponde hello iniziale.</span><span class="sxs-lookup"><span data-stu-id="28c48-114">By default, hello first scheduled backup is hello initial backup.</span></span> <span data-ttu-id="28c48-115">Fino a quando non si verifica il backup iniziale hello, hello ultimo stato di Backup su hello **i processi di Backup** pannello viene visualizzato come **avviso (backup iniziale in sospeso)**.</span><span class="sxs-lookup"><span data-stu-id="28c48-115">Until hello initial backup occurs, hello Last Backup Status on hello **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span></span>

![Backup in sospeso](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

<span data-ttu-id="28c48-117">A meno che il backup iniziale è scadenza toobegin imminente, è consigliabile eseguire **Esegui backup**.</span><span class="sxs-lookup"><span data-stu-id="28c48-117">Unless your initial backup is due toobegin soon, it is recommended that you run **Back up Now**.</span></span> <span data-ttu-id="28c48-118">Hello procedura riportata di seguito viene avviato dal dashboard di hello insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="28c48-118">hello following procedure starts from hello vault dashboard.</span></span> <span data-ttu-id="28c48-119">Questa procedura viene utilizzato per l'esecuzione di processo di backup iniziale hello dopo aver completato tutti i prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="28c48-119">This procedure serves for running hello initial backup job after you have completed all prerequisites.</span></span> <span data-ttu-id="28c48-120">Se è già stato eseguito il processo di backup iniziale di hello, questa procedura non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="28c48-120">If hello initial backup job has already been run, this procedure is not available.</span></span> <span data-ttu-id="28c48-121">Hello associati criteri di backup determinano il processo di backup successivo di hello.</span><span class="sxs-lookup"><span data-stu-id="28c48-121">hello associated backup policy determines hello next backup job.</span></span>  

<span data-ttu-id="28c48-122">toorun hello iniziale processo di backup:</span><span class="sxs-lookup"><span data-stu-id="28c48-122">toorun hello initial backup job:</span></span>

1. <span data-ttu-id="28c48-123">Nel dashboard dell'insieme di credenziali hello, fare clic sul numero hello in **elementi Backup**, oppure fare clic su hello **elementi Backup** riquadro.</span><span class="sxs-lookup"><span data-stu-id="28c48-123">On hello vault dashboard, click hello number under **Backup Items**, or click hello **Backup Items** tile.</span></span> <br/><span data-ttu-id="28c48-124">
  ![Icona Impostazioni](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span><span class="sxs-lookup"><span data-stu-id="28c48-124">
![Settings icon](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span></span>

  <span data-ttu-id="28c48-125">Hello **elementi Backup** apre blade.</span><span class="sxs-lookup"><span data-stu-id="28c48-125">hello **Backup Items** blade opens.</span></span>

  ![Elementi di backup](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. <span data-ttu-id="28c48-127">In hello **elementi Backup** blade, elemento selezionare hello.</span><span class="sxs-lookup"><span data-stu-id="28c48-127">On hello **Backup Items** blade, select hello item.</span></span>

  ![Icona Impostazioni](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  <span data-ttu-id="28c48-129">Hello **elementi Backup** viene aperto l'elenco.</span><span class="sxs-lookup"><span data-stu-id="28c48-129">hello **Backup Items** list opens.</span></span> <br/>

  ![Processo di backup attivato](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. <span data-ttu-id="28c48-131">In hello **elementi Backup** fare clic sui puntini di sospensione hello **...**  menu di scelta rapida tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="28c48-131">On hello **Backup Items** list, click hello ellipses **...** tooopen hello Context menu.</span></span>

  ![Menu di scelta rapida](./media/backup-azure-vms-first-look-arm/context-menu.png)

  <span data-ttu-id="28c48-133">viene visualizzato il menu di scelta rapida Hello.</span><span class="sxs-lookup"><span data-stu-id="28c48-133">hello Context menu appears.</span></span>

  ![Menu di scelta rapida](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. <span data-ttu-id="28c48-135">Nel menu di scelta rapida hello, fare clic su **Backup ora**.</span><span class="sxs-lookup"><span data-stu-id="28c48-135">On hello Context menu, click **Backup now**.</span></span>

  ![Menu di scelta rapida](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  <span data-ttu-id="28c48-137">verrà visualizzata la finestra di Backup ora pannello Hello.</span><span class="sxs-lookup"><span data-stu-id="28c48-137">hello Backup Now blade opens.</span></span>

  ![Mostra pannello hello Esegui Backup](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. <span data-ttu-id="28c48-139">Nel pannello Esegui Backup hello fare clic sull'icona calendario hello, utilizzare hello tooselect di controllo calendario hello ultimo giorno di tale punto di ripristino è stato mantenuto e fare clic su **Backup**.</span><span class="sxs-lookup"><span data-stu-id="28c48-139">On hello Backup Now blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>

  ![impostare hello ultimo giorno hello Esegui Backup viene mantenuto un punto di ripristino](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="28c48-141">Le notifiche di distribuzione consentono di sapere che è possibile monitorare lo stato di avanzamento hello del processo di hello nella pagina processi di Backup hello e processo di backup hello è stato attivato.</span><span class="sxs-lookup"><span data-stu-id="28c48-141">Deployment notifications let you know hello backup job has been triggered, and that you can monitor hello progress of hello job on hello Backup jobs page.</span></span> <span data-ttu-id="28c48-142">A seconda delle dimensioni di hello della macchina virtuale, la creazione di backup iniziale hello potrebbe richiedere qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="28c48-142">Depending on hello size of your VM, creating hello initial backup may take a while.</span></span>

6. <span data-ttu-id="28c48-143">lo stato di hello tooview o di una traccia di backup iniziale hello, nel dashboard dell'insieme di credenziali hello in hello **i processi di Backup** fare clic su riquadro **In corso**.</span><span class="sxs-lookup"><span data-stu-id="28c48-143">tooview or track hello status of hello initial backup, on hello vault dashboard, on hello **Backup Jobs** tile click **In progress**.</span></span>

  ![Riquadro dei processi di backup](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  <span data-ttu-id="28c48-145">Apre il pannello di processi di Backup Hello.</span><span class="sxs-lookup"><span data-stu-id="28c48-145">hello Backup Jobs blade opens.</span></span>

  ![Riquadro dei processi di backup](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  <span data-ttu-id="28c48-147">In hello **i processi di Backup** pannello, è possibile visualizzare lo stato di hello di tutti i processi.</span><span class="sxs-lookup"><span data-stu-id="28c48-147">In hello **Backup jobs** blade, you can see hello status of all jobs.</span></span> <span data-ttu-id="28c48-148">Controllare se il processo di backup hello per la macchina virtuale è ancora in corso o ha terminato.</span><span class="sxs-lookup"><span data-stu-id="28c48-148">Check if hello backup job for your VM is still in progress, or if it has finished.</span></span> <span data-ttu-id="28c48-149">Al termine di un processo di backup, lo stato di hello è *completato*.</span><span class="sxs-lookup"><span data-stu-id="28c48-149">When a backup job is finished, hello status is *Completed*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="28c48-150">Come parte dell'operazione di backup hello, hello servizio Backup di Azure esegue un'estensione di backup toohello comando in ogni macchina virtuale di tooflush tutti scrive e creare uno snapshot coerenza.</span><span class="sxs-lookup"><span data-stu-id="28c48-150">As a part of hello backup operation, hello Azure Backup service issues a command toohello backup extension in each VM tooflush all writes and take a consistent snapshot.</span></span>
  >
  >

## <a name="troubleshooting-errors"></a><span data-ttu-id="28c48-151">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="28c48-151">Troubleshooting errors</span></span>
<span data-ttu-id="28c48-152">Se si verificano problemi durante il backup la macchina virtuale, vedere hello [articolo sulla risoluzione dei problemi di VM](backup-azure-vms-troubleshoot.md) per assistenza.</span><span class="sxs-lookup"><span data-stu-id="28c48-152">If you run into issues while backing up your virtual machine, see hello [VM troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28c48-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="28c48-153">Next steps</span></span>
<span data-ttu-id="28c48-154">Ora che è stato protetto della macchina virtuale, vedere hello seguente toolearn articoli sulle attività di gestione delle macchine Virtuali e come toorestore macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="28c48-154">Now that you have protected your VM, see hello following articles toolearn about VM management tasks, and how toorestore VMs.</span></span>

* [<span data-ttu-id="28c48-155">Gestire e monitorare il backup delle macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="28c48-155">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="28c48-156">Ripristino di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="28c48-156">Restore virtual machines</span></span>](backup-azure-arm-restore-vms.md)
