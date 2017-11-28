---
title: Eseguire il backup di macchine virtuali Linux in Azure | Microsoft Docs
description: Proteggere le macchine virtuali Linux eseguendo il backup con Backup di Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 7c00392d5185a2f067f2ee2717529dcbde1e71f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a><span data-ttu-id="fb74e-103">Eseguire il backup di macchine virtuali Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="fb74e-103">Back up Linux  virtual machines in Azure</span></span>

<span data-ttu-id="fb74e-104">È possibile proteggere i dati eseguendo backup a intervalli regolari.</span><span class="sxs-lookup"><span data-stu-id="fb74e-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="fb74e-105">Backup di Azure crea punti di recupero che vengono archiviati negli insiemi di credenziali di ripristino con ridondanza geografica.</span><span class="sxs-lookup"><span data-stu-id="fb74e-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="fb74e-106">Quando si ripristina da un punto di ripristino, è possibile ripristinare hello intera macchina virtuale o a specifici file.</span><span class="sxs-lookup"><span data-stu-id="fb74e-106">When you restore from a recovery point, you can restore hello whole VM or just specific files.</span></span> <span data-ttu-id="fb74e-107">Questo articolo spiega come toorestore un singolo file tooa nginx in esecuzione Linux VM.</span><span class="sxs-lookup"><span data-stu-id="fb74e-107">This article explains how toorestore a single file tooa Linux VM running nginx.</span></span> <span data-ttu-id="fb74e-108">Se si dispone già di un toouse VM, è possibile crearne uno utilizzando hello [delle Guide rapide Linux](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="fb74e-108">If you don't already have a VM toouse, you can create one using hello [Linux quickstart](quick-create-cli.md).</span></span> <span data-ttu-id="fb74e-109">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="fb74e-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fb74e-110">Creare un backup di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="fb74e-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="fb74e-111">Pianificare un backup giornaliero</span><span class="sxs-lookup"><span data-stu-id="fb74e-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="fb74e-112">Ripristinare un file da un backup</span><span class="sxs-lookup"><span data-stu-id="fb74e-112">Restore a file from a backup</span></span>



## <a name="backup-overview"></a><span data-ttu-id="fb74e-113">Panoramica del servizio Backup</span><span class="sxs-lookup"><span data-stu-id="fb74e-113">Backup overview</span></span>

<span data-ttu-id="fb74e-114">Quando hello servizio Backup di Azure avvia un backup, attiva hello estensione backup tootake uno snapshot del punto nel tempo.</span><span class="sxs-lookup"><span data-stu-id="fb74e-114">When hello Azure Backup service initiates a backup, it triggers hello backup extension tootake a point-in-time snapshot.</span></span> <span data-ttu-id="fb74e-115">Hello servizio Azure Backup utilizza hello _VMSnapshotLinux_ estensione in Linux.</span><span class="sxs-lookup"><span data-stu-id="fb74e-115">hello Azure Backup service uses hello _VMSnapshotLinux_ extension in Linux.</span></span> <span data-ttu-id="fb74e-116">estensione Hello viene installato durante il backup di VM prima hello se hello macchina virtuale è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fb74e-116">hello extension is installed during hello first VM backup if hello VM is running.</span></span> <span data-ttu-id="fb74e-117">Se hello VM non è in esecuzione, il servizio di Backup hello crea uno snapshot di hello archiviazione sottostante (poiché non scritte dall'applicazione si verificano durante hello che macchina virtuale è stato arrestato).</span><span class="sxs-lookup"><span data-stu-id="fb74e-117">If hello VM is not running, hello Backup service takes a snapshot of hello underlying storage (since no application writes occur while hello VM is stopped).</span></span>

<span data-ttu-id="fb74e-118">Per impostazione predefinita, Backup di Azure richiede un backup coerente del file system per VM Linux ma può essere configurato tootake [backup coerente dell'applicazione tramite pre- script di e post-framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span><span class="sxs-lookup"><span data-stu-id="fb74e-118">By default, Azure Backup takes a file system consistent backup for Linux VM but it can be configured tootake [application consistent backup using pre-script and post-script framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span></span> <span data-ttu-id="fb74e-119">Una volta hello servizio Azure Backup istantanea hello, dati hello sono toohello trasferite insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="fb74e-119">Once hello Azure Backup service takes hello snapshot, hello data is transferred toohello vault.</span></span> <span data-ttu-id="fb74e-120">l'efficienza toomaximize servizio hello identifica e i trasferimenti di dati che sono stati modificati dal backup precedente hello solo i blocchi hello.</span><span class="sxs-lookup"><span data-stu-id="fb74e-120">toomaximize efficiency, hello service identifies and transfers only hello blocks of data that have changed since hello previous backup.</span></span>

<span data-ttu-id="fb74e-121">Una volta completato il trasferimento dei dati di hello, snapshot hello viene rimosso e viene creato un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="fb74e-121">When hello data transfer is complete, hello snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="fb74e-122">Creare un backup</span><span class="sxs-lookup"><span data-stu-id="fb74e-122">Create a backup</span></span>
<span data-ttu-id="fb74e-123">Creare un semplice pianificata giornaliera backup tooa insieme di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="fb74e-123">Create a simple scheduled daily backup tooa Recovery Services Vault.</span></span> 

1. <span data-ttu-id="fb74e-124">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fb74e-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="fb74e-125">Dal menu hello hello sinistra, selezionare **macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="fb74e-125">In hello menu on hello left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="fb74e-126">Dall'elenco di hello, selezionare una macchina virtuale tooback backup.</span><span class="sxs-lookup"><span data-stu-id="fb74e-126">From hello list, select a VM tooback up.</span></span>
4. <span data-ttu-id="fb74e-127">Nel pannello VM hello in hello **impostazioni** fare clic su **Backup**.</span><span class="sxs-lookup"><span data-stu-id="fb74e-127">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="fb74e-128">Hello **Abilita backup** apre blade.</span><span class="sxs-lookup"><span data-stu-id="fb74e-128">hello **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="fb74e-129">In **insieme di credenziali di servizi di ripristino**, fare clic su **Crea nuovo** e specificare il nome di hello per nuovo insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="fb74e-129">In **Recovery Services vault**, click **Create new** and provide hello name for hello new vault.</span></span> <span data-ttu-id="fb74e-130">Viene creato un nuovo insieme di credenziali in hello stesso gruppo di risorse e il percorso come macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="fb74e-130">A new vault is created in hello same Resource Group and location as hello virtual machine.</span></span>
6. <span data-ttu-id="fb74e-131">Fare clic su **Criterio di Backup**.</span><span class="sxs-lookup"><span data-stu-id="fb74e-131">Click **Backup policy**.</span></span> <span data-ttu-id="fb74e-132">Per questo esempio, mantenere i valori predefiniti di hello e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="fb74e-132">For this example, keep hello defaults and click **OK**.</span></span>
7. <span data-ttu-id="fb74e-133">In hello **Abilita backup** pannello, fare clic su **Abilita Backup**.</span><span class="sxs-lookup"><span data-stu-id="fb74e-133">On hello **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="fb74e-134">Verrà creato un backup giornaliero in base alla pianificazione predefinita hello.</span><span class="sxs-lookup"><span data-stu-id="fb74e-134">This creates a daily backup based on hello default schedule.</span></span>
10. <span data-ttu-id="fb74e-135">un punto di ripristino iniziale, su hello toocreate **Backup** fare clic su pannello **Backup ora**.</span><span class="sxs-lookup"><span data-stu-id="fb74e-135">toocreate an initial recovery point, on hello **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="fb74e-136">In hello **Esegui Backup** pannello, fare clic sull'icona calendario hello, utilizzare hello tooselect di controllo calendario hello ultimo giorno di tale punto di ripristino è stato mantenuto e fare clic su **Backup**.</span><span class="sxs-lookup"><span data-stu-id="fb74e-136">On hello **Backup Now** blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="fb74e-137">In hello **Backup** pannello per la macchina virtuale, viene visualizzato un numero di punti di ripristino che sono state completate hello.</span><span class="sxs-lookup"><span data-stu-id="fb74e-137">In hello **Backup** blade for your VM, you will see hello number of recovery points that are complete.</span></span>

    ![Punti di ripristino](./media/tutorial-backup-vms/backup-complete.png)

<span data-ttu-id="fb74e-139">il primo backup di Hello richiede circa 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="fb74e-139">hello first backup takes about 20 minutes.</span></span> <span data-ttu-id="fb74e-140">Al termine del backup, procedere toohello parte successiva di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="fb74e-140">Proceed toohello next part of this tutorial after your backup is finished.</span></span>

## <a name="restore-a-file"></a><span data-ttu-id="fb74e-141">Ripristinare un file</span><span class="sxs-lookup"><span data-stu-id="fb74e-141">Restore a file</span></span>

<span data-ttu-id="fb74e-142">Se accidentalmente si elimina o si apporta modifiche tooa file, è possibile utilizzare file di ripristino di File toorecover hello dall'insieme di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="fb74e-142">If you accidentally delete or make changes tooa file, you can use File Recovery toorecover hello file from your backup vault.</span></span> <span data-ttu-id="fb74e-143">Ripristino di file usa uno script eseguito nella macchina virtuale, hello toomount hello di punto di ripristino come unità locale.</span><span class="sxs-lookup"><span data-stu-id="fb74e-143">File Recovery uses a script that runs on hello VM, toomount hello recovery point as local drive.</span></span> <span data-ttu-id="fb74e-144">Queste unità rimarrà montate per 12 ore in modo che è possibile copiare i file dal punto di ripristino hello e ripristinarli toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fb74e-144">These drives will remain mounted for 12 hours so that you can copy files from hello recovery point and restore them toohello VM.</span></span>  

<span data-ttu-id="fb74e-145">In questo esempio, ecco come toorecover hello predefinito nginx pagina web /var/www/html/index.nginx-debian.html.</span><span class="sxs-lookup"><span data-stu-id="fb74e-145">In this example, we show how toorecover hello default nginx web page /var/www/html/index.nginx-debian.html.</span></span> <span data-ttu-id="fb74e-146">indirizzo IP pubblico Hello della macchina virtuale in questo esempio è *13.69.75.209*.</span><span class="sxs-lookup"><span data-stu-id="fb74e-146">hello public IP address of our VM in this example is *13.69.75.209*.</span></span> <span data-ttu-id="fb74e-147">È possibile trovare l'indirizzo IP hello di macchina virtuale utilizzando:</span><span class="sxs-lookup"><span data-stu-id="fb74e-147">You can find hello IP address of your vm using:</span></span>

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. <span data-ttu-id="fb74e-148">Nel computer locale, aprire un browser e digitare in indirizzo IP pubblico hello della VM toosee hello predefinito nginx pagina web.</span><span class="sxs-lookup"><span data-stu-id="fb74e-148">On your local computer, open a browser and type in hello public IP address of your VM toosee hello default nginx web page.</span></span>

    ![Pagina Web di nginx predefinita](./media/tutorial-backup-vms/nginx-working.png)

1. <span data-ttu-id="fb74e-150">Stabilire una connessione SSH alla VM.</span><span class="sxs-lookup"><span data-stu-id="fb74e-150">SSH into your VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
2. <span data-ttu-id="fb74e-151">Eliminare /var/www/html/index.nginx-debian.html.</span><span class="sxs-lookup"><span data-stu-id="fb74e-151">Delete /var/www/html/index.nginx-debian.html.</span></span>

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. <span data-ttu-id="fb74e-152">Nel computer locale, aggiornare il browser di hello premendo CTRL + F5 toosee che nginx pagina predefinita non viene più visualizzato.</span><span class="sxs-lookup"><span data-stu-id="fb74e-152">On your local computer, refresh hello browser by hitting CTRL + F5 toosee that default nginx page is gone.</span></span>

    ![Pagina Web di nginx predefinita](./media/tutorial-backup-vms/nginx-broken.png)
    
1. <span data-ttu-id="fb74e-154">Nel computer locale, accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fb74e-154">On your local computer, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
6. <span data-ttu-id="fb74e-155">Dal menu hello hello sinistra, selezionare **macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="fb74e-155">In hello menu on hello left, select **Virtual machines**.</span></span> 
7. <span data-ttu-id="fb74e-156">Elenco hello selezionare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fb74e-156">From hello list, select hello VM.</span></span>
8. <span data-ttu-id="fb74e-157">Nel pannello VM hello in hello **impostazioni** fare clic su **Backup**.</span><span class="sxs-lookup"><span data-stu-id="fb74e-157">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="fb74e-158">Hello **Backup** apre blade.</span><span class="sxs-lookup"><span data-stu-id="fb74e-158">hello **Backup** blade opens.</span></span> 
9. <span data-ttu-id="fb74e-159">Nel menu di hello nella parte superiore di hello del pannello hello, selezionare **ripristino File**.</span><span class="sxs-lookup"><span data-stu-id="fb74e-159">In hello menu at hello top of hello blade, select **File Recovery**.</span></span> <span data-ttu-id="fb74e-160">Hello **ripristino File** apre blade.</span><span class="sxs-lookup"><span data-stu-id="fb74e-160">hello **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="fb74e-161">In **passaggio 1: selezionare il punto di ripristino**, selezionare un punto di ripristino dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="fb74e-161">In **Step 1: Select recovery point**, select a recovery point from hello drop-down.</span></span>
11. <span data-ttu-id="fb74e-162">In **passaggio 2: scaricare script toobrowse e recuperare i file**, fare clic su hello **scaricare eseguibile** pulsante.</span><span class="sxs-lookup"><span data-stu-id="fb74e-162">In **Step 2: Download script toobrowse and recover files**, click hello **Download Executable** button.</span></span> <span data-ttu-id="fb74e-163">Salvare computer locale tooyour di hello file scaricato.</span><span class="sxs-lookup"><span data-stu-id="fb74e-163">Save hello downloaded file tooyour local computer.</span></span>
7. <span data-ttu-id="fb74e-164">Fare clic su **scaricare script** locale file di script hello toodownload.</span><span class="sxs-lookup"><span data-stu-id="fb74e-164">Click **Download script** toodownload hello script file locally.</span></span>
8. <span data-ttu-id="fb74e-165">Aprire un hello di prompt dei comandi e il tipo del Bash seguente, sostituendo *Linux_myVM_05-05-2017.sh* con hello correggere percorso e il nome di script hello scaricato, *azureuser* con il nome utente di hello per hello VM e *13.69.75.209* con indirizzo IP pubblico hello per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fb74e-165">Open a Bash prompt and type hello following, replacing *Linux_myVM_05-05-2017.sh* with hello correct path and filename for hello script that you downloaded, *azureuser* with hello username for hello VM and *13.69.75.209* with hello public IP address for your VM.</span></span>
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. <span data-ttu-id="fb74e-166">Nel computer locale, aprire un toohello connessione SSH macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fb74e-166">On your local computer, open an SSH connection toohello VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
    
10. <span data-ttu-id="fb74e-167">Aggiungere la macchina virtuale, eseguire il file di script toohello autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="fb74e-167">On your VM, add execute permissions toohello script file.</span></span>

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. <span data-ttu-id="fb74e-168">Nella macchina virtuale, eseguire un punto di ripristino hello toomount hello script come un file System.</span><span class="sxs-lookup"><span data-stu-id="fb74e-168">On your VM, run hello script toomount hello recovery point as a filesystem.</span></span>

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. <span data-ttu-id="fb74e-169">Hello output di hello script offre che Hello percorso per il punto di montaggio hello.</span><span class="sxs-lookup"><span data-stu-id="fb74e-169">hello output from hello script gives you hello path for hello mount point.</span></span> <span data-ttu-id="fb74e-170">output di Hello è toothis simile:</span><span class="sxs-lookup"><span data-stu-id="fb74e-170">hello output looks similar toothis:</span></span>

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting toorecovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of hello recovery point toothis machine...
                         
    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

12. <span data-ttu-id="fb74e-171">Nella macchina virtuale, copiare pagina web predefinita di hello nginx da toowhere indietro punto di montaggio hello eliminato file hello.</span><span class="sxs-lookup"><span data-stu-id="fb74e-171">On your VM, copy hello nginx default web page from hello mount point back toowhere you deleted hello file.</span></span>

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. <span data-ttu-id="fb74e-172">Nel computer locale, aprire scheda del browser hello in cui si è connessi toohello l'indirizzo IP del hello VM la visualizzazione hello nginx predefinito della pagina.</span><span class="sxs-lookup"><span data-stu-id="fb74e-172">On your local computer, open hello browser tab where you are connected toohello IP address of hello VM showing hello nginx default page.</span></span> <span data-ttu-id="fb74e-173">Premere CTRL + F5 pagina nel browser toorefresh hello.</span><span class="sxs-lookup"><span data-stu-id="fb74e-173">Press CTRL + F5 toorefresh hello browser page.</span></span> <span data-ttu-id="fb74e-174">Si noterà ora che hello funziona di nuovo la pagina predefinita.</span><span class="sxs-lookup"><span data-stu-id="fb74e-174">You should now see that hello default page is working again.</span></span>

    ![Pagina Web di nginx predefinita](./media/tutorial-backup-vms/nginx-working.png)

18. <span data-ttu-id="fb74e-176">Nel computer locale, tornare indietro toohello per hello portale di Azure e nella scheda del browser **passaggio 3: smontare dischi hello dopo il ripristino** fare clic su hello **smontare dischi** pulsante.</span><span class="sxs-lookup"><span data-stu-id="fb74e-176">On your local computer, go back toohello browser tab for hello Azure portal and in **Step 3: Unmount hello disks after recovery** click hello **Unmount Disks** button.</span></span> <span data-ttu-id="fb74e-177">Se si dimentica toodo questo passaggio, punto di montaggio toohello hello connessione è chiusa automaticamente dopo 12 ore.</span><span class="sxs-lookup"><span data-stu-id="fb74e-177">If you forget toodo this step, hello connection toohello mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="fb74e-178">Dopo queste 12 ore, è necessario toodownload un nuovo toocreate script un nuovo punto di montaggio.</span><span class="sxs-lookup"><span data-stu-id="fb74e-178">After those 12 hours, you need toodownload a new script toocreate a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fb74e-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fb74e-179">Next steps</span></span>

<span data-ttu-id="fb74e-180">In questa esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="fb74e-180">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fb74e-181">Creare un backup di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="fb74e-181">Create a backup of a VM</span></span>
> * <span data-ttu-id="fb74e-182">Pianificare un backup giornaliero</span><span class="sxs-lookup"><span data-stu-id="fb74e-182">Schedule a daily backup</span></span>
> * <span data-ttu-id="fb74e-183">Ripristinare un file da un backup</span><span class="sxs-lookup"><span data-stu-id="fb74e-183">Restore a file from a backup</span></span>

<span data-ttu-id="fb74e-184">Spostare toohello toolearn esercitazione successiva sul monitoraggio delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="fb74e-184">Advance toohello next tutorial toolearn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fb74e-185">Monitorare le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="fb74e-185">Monitor virtual machines</span></span>](tutorial-monitoring.md)

