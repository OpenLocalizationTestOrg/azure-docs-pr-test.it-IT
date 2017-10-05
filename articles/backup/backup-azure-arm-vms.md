---
title: Eseguire il backup di macchine virtuali di Azure | Documentazione Microsoft
description: Scoprire, registrare ed eseguire il backup di macchine virtuali di Azure in un insieme di credenziali di Servizi di ripristino.
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
ms.openlocfilehash: 40983a3de104238d09b976b5fcf2419da42c1bba
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="back-up-azure-virtual-machines-to-a-recovery-services-vault"></a><span data-ttu-id="ab544-104">Backup di macchine virtuali di Azure in un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="ab544-104">Back up Azure virtual machines to a Recovery Services vault</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ab544-105">Eseguire il backup di macchine virtuali in un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="ab544-105">Back up VMs to Recovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="ab544-106">Eseguire il backup di macchine virtuali in un insieme di credenziali per il backup</span><span class="sxs-lookup"><span data-stu-id="ab544-106">Back up VMs to Backup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="ab544-107">Questo articolo descrive come eseguire il backup di macchine virtuali di Azure, distribuite con il modello di distribuzione classica e con il modello di distribuzione Resource Manager, in un insieme di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="ab544-107">This article details how to back up Azure VMs (both Resource Manager-deployed and Classic-deployed) to a Recovery Services vault.</span></span> <span data-ttu-id="ab544-108">Per eseguire il backup di macchine virtuali, il più del lavoro è dato dalla preparazione.</span><span class="sxs-lookup"><span data-stu-id="ab544-108">Most of the work for backing up VMs is the preparation.</span></span> <span data-ttu-id="ab544-109">Prima di poter eseguire il backup o proteggere una macchina virtuale, è necessario completare i [prerequisiti](backup-azure-arm-vms-prepare.md) per preparare l'ambiente per la protezione delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="ab544-109">Before you can back up or protect a VM, you must complete the [prerequisites](backup-azure-arm-vms-prepare.md) to prepare your environment for protecting your VMs.</span></span> <span data-ttu-id="ab544-110">Dopo aver completato i prerequisiti, è possibile avviare il backup per eseguire snapshot della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ab544-110">Once you have completed the prerequisites, then you can initiate the backup operation to take snapshots of your VM.</span></span>


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

<span data-ttu-id="ab544-111">Per altre informazioni, vedere gli articoli relativi alla [pianificazione dell'infrastruttura di backup delle macchine virtuali in Azure](backup-azure-vms-introduction.md) e alle [macchine virtuali di Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="ab544-111">For more information, see the articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

## <a name="triggering-the-backup-job"></a><span data-ttu-id="ab544-112">Attivazione del processo di backup</span><span class="sxs-lookup"><span data-stu-id="ab544-112">Triggering the backup job</span></span>
<span data-ttu-id="ab544-113">Il criterio di backup associato all'insieme di credenziali di servizi di ripristino definisce quando e con quale frequenza eseguire l'operazione di backup.</span><span class="sxs-lookup"><span data-stu-id="ab544-113">The backup policy associated with the Recovery Services vault defines how often and when the backup operation runs.</span></span> <span data-ttu-id="ab544-114">Per impostazione predefinita, il primo backup pianificato è il backup iniziale.</span><span class="sxs-lookup"><span data-stu-id="ab544-114">By default, the first scheduled backup is the initial backup.</span></span> <span data-ttu-id="ab544-115">Fino all'esecuzione del backup iniziale, lo stato dell'ultimo backup nel pannello **Processi di Backup** è **Avviso (backup iniziale in sospeso)**.</span><span class="sxs-lookup"><span data-stu-id="ab544-115">Until the initial backup occurs, the Last Backup Status on the **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span></span>

![Backup in sospeso](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

<span data-ttu-id="ab544-117">A meno che l'avvio del backup iniziale non sia imminente, è consigliabile scegliere l'opzione **Esegui backup ora**.</span><span class="sxs-lookup"><span data-stu-id="ab544-117">Unless your initial backup is due to begin soon, it is recommended that you run **Back up Now**.</span></span> <span data-ttu-id="ab544-118">La procedura seguente viene avviata dal dashboard dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="ab544-118">The following procedure starts from the vault dashboard.</span></span> <span data-ttu-id="ab544-119">Questa procedura viene usata per l'esecuzione del processo di backup iniziale dopo aver completato tutti i prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="ab544-119">This procedure serves for running the initial backup job after you have completed all prerequisites.</span></span> <span data-ttu-id="ab544-120">Se è già stato eseguito il processo di backup iniziale, questa procedura non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="ab544-120">If the initial backup job has already been run, this procedure is not available.</span></span> <span data-ttu-id="ab544-121">I criteri di backup associati determinano il processo di backup successivo.</span><span class="sxs-lookup"><span data-stu-id="ab544-121">The associated backup policy determines the next backup job.</span></span>  

<span data-ttu-id="ab544-122">Per eseguire il processo di backup iniziale:</span><span class="sxs-lookup"><span data-stu-id="ab544-122">To run the initial backup job:</span></span>

1. <span data-ttu-id="ab544-123">Nel dashboard dell'insieme di credenziali fare clic sul numero sotto **Elementi di backup** oppure fare clic sul riquadro **Elementi di backup**.</span><span class="sxs-lookup"><span data-stu-id="ab544-123">On the vault dashboard, click the number under **Backup Items**, or click the **Backup Items** tile.</span></span> <br/><span data-ttu-id="ab544-124">
  ![Icona Impostazioni](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span><span class="sxs-lookup"><span data-stu-id="ab544-124">
![Settings icon](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span></span>

  <span data-ttu-id="ab544-125">Si apre il pannello **Elementi di backup** .</span><span class="sxs-lookup"><span data-stu-id="ab544-125">The **Backup Items** blade opens.</span></span>

  ![Elementi di backup](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. <span data-ttu-id="ab544-127">Nel pannello **Elementi di backup** selezionare l'elemento.</span><span class="sxs-lookup"><span data-stu-id="ab544-127">On the **Backup Items** blade, select the item.</span></span>

  ![Icona Impostazioni](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  <span data-ttu-id="ab544-129">Si apre l'elenco **Elementi di backup**.</span><span class="sxs-lookup"><span data-stu-id="ab544-129">The **Backup Items** list opens.</span></span> <br/>

  ![Processo di backup attivato](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. <span data-ttu-id="ab544-131">Nell'elenco **Elementi di backup** fare clic sui puntini di sospensione **...** per aprire il menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="ab544-131">On the **Backup Items** list, click the ellipses **...** to open the Context menu.</span></span>

  ![Menu di scelta rapida](./media/backup-azure-vms-first-look-arm/context-menu.png)

  <span data-ttu-id="ab544-133">Si apre il menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="ab544-133">The Context menu appears.</span></span>

  ![Menu di scelta rapida](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. <span data-ttu-id="ab544-135">Nel menu di scelta rapida fare clic su **Esegui backup ora**.</span><span class="sxs-lookup"><span data-stu-id="ab544-135">On the Context menu, click **Backup now**.</span></span>

  ![Menu di scelta rapida](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  <span data-ttu-id="ab544-137">Si apre il pannello Esegui backup ora.</span><span class="sxs-lookup"><span data-stu-id="ab544-137">The Backup Now blade opens.</span></span>

  ![mostra il pannello Esegui backup ora](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. <span data-ttu-id="ab544-139">Nel pannello Esegui backup ora fare clic sull'icona del calendario, usare il comando del calendario per selezionare l'ultimo giorno di conservazione di tale punto di ripristino e fare clic su **Esegui backup**.</span><span class="sxs-lookup"><span data-stu-id="ab544-139">On the Backup Now blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span></span>

  ![impostare l'ultimo giorno di conservazione del punto di ripristino di Esegui backup ora](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="ab544-141">Le notifiche sulla distribuzione consentono di sapere che il processo di backup è stato attivato e che è possibile monitorare lo stato di avanzamento del processo nella pagina Processi di backup.</span><span class="sxs-lookup"><span data-stu-id="ab544-141">Deployment notifications let you know the backup job has been triggered, and that you can monitor the progress of the job on the Backup jobs page.</span></span> <span data-ttu-id="ab544-142">A seconda delle dimensioni della macchina virtuale, la creazione del backup iniziale potrebbe richiedere un po' di tempo.</span><span class="sxs-lookup"><span data-stu-id="ab544-142">Depending on the size of your VM, creating the initial backup may take a while.</span></span>

6. <span data-ttu-id="ab544-143">Per visualizzare o tenere traccia dello stato del backup iniziale, nel dashboard dell'insieme di credenziali, nel riquadro **Processi di backup** fare clic sul riquadro **In corso**.</span><span class="sxs-lookup"><span data-stu-id="ab544-143">To view or track the status of the initial backup, on the vault dashboard, on the **Backup Jobs** tile click **In progress**.</span></span>

  ![Riquadro dei processi di backup](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  <span data-ttu-id="ab544-145">Si apre il pannello dei processi di backup.</span><span class="sxs-lookup"><span data-stu-id="ab544-145">The Backup Jobs blade opens.</span></span>

  ![Riquadro dei processi di backup](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  <span data-ttu-id="ab544-147">Nel pannello **Processi di backup** è possibile visualizzare lo stato di tutti i processi.</span><span class="sxs-lookup"><span data-stu-id="ab544-147">In the **Backup jobs** blade, you can see the status of all jobs.</span></span> <span data-ttu-id="ab544-148">Controllare se il processo di backup per la macchina virtuale è ancora in corso o se è terminato.</span><span class="sxs-lookup"><span data-stu-id="ab544-148">Check if the backup job for your VM is still in progress, or if it has finished.</span></span> <span data-ttu-id="ab544-149">Al termine del processo di backup, lo stato è *Completato*.</span><span class="sxs-lookup"><span data-stu-id="ab544-149">When a backup job is finished, the status is *Completed*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ab544-150">Come parte dell'operazione di backup, il servizio Backup di Azure esegue un comando nell'estensione di backup in ogni VM per scaricare tutte le scritture e creare uno snapshot coerente.</span><span class="sxs-lookup"><span data-stu-id="ab544-150">As a part of the backup operation, the Azure Backup service issues a command to the backup extension in each VM to flush all writes and take a consistent snapshot.</span></span>
  >
  >

## <a name="troubleshooting-errors"></a><span data-ttu-id="ab544-151">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="ab544-151">Troubleshooting errors</span></span>
<span data-ttu-id="ab544-152">Se si riscontrano problemi durante il backup della macchina virtuale, leggere l'[articolo sulla risoluzione dei problemi delle macchine virtuali](backup-azure-vms-troubleshoot.md) per assistenza.</span><span class="sxs-lookup"><span data-stu-id="ab544-152">If you run into issues while backing up your virtual machine, see the [VM troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab544-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ab544-153">Next steps</span></span>
<span data-ttu-id="ab544-154">Dopo aver protetto la macchina virtuale, vedere gli articoli seguenti per ottenere informazioni sulle attività di gestione delle macchine virtuali e su come ripristinare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="ab544-154">Now that you have protected your VM, see the following articles to learn about VM management tasks, and how to restore VMs.</span></span>

* [<span data-ttu-id="ab544-155">Gestire e monitorare il backup delle macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="ab544-155">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="ab544-156">Ripristino di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="ab544-156">Restore virtual machines</span></span>](backup-azure-arm-restore-vms.md)
