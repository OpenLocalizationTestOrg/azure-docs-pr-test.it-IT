---
title: macchine virtuali di Windows Azure aaaBackup | Microsoft documenti
description: Proteggere le macchine virtuali Windows eseguendo il backup con Backup di Azure.
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 1cd3e1940a83aacd160cba3c8613b63b6f3c11d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-virtual-machines-in-azure"></a><span data-ttu-id="848b8-103">Eseguire il backup di macchine virtuali Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="848b8-103">Back up Windows virtual machines in Azure</span></span>

<span data-ttu-id="848b8-104">È possibile proteggere i dati eseguendo backup a intervalli regolari.</span><span class="sxs-lookup"><span data-stu-id="848b8-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="848b8-105">Backup di Azure crea punti di recupero che vengono archiviati negli insiemi di credenziali di ripristino con ridondanza geografica.</span><span class="sxs-lookup"><span data-stu-id="848b8-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="848b8-106">Quando si ripristina da un punto di ripristino, è possibile ripristinare hello intera macchina virtuale o a specifici file.</span><span class="sxs-lookup"><span data-stu-id="848b8-106">When you restore from a recovery point, you can restore hello whole VM or just specific files.</span></span> <span data-ttu-id="848b8-107">Questo articolo viene illustrato come toorestore un singolo file tooa macchina virtuale che esegue Windows Server e IIS.</span><span class="sxs-lookup"><span data-stu-id="848b8-107">This article explains how toorestore a single file tooa VM running Windows Server and IIS.</span></span> <span data-ttu-id="848b8-108">Se si dispone già di un toouse VM, è possibile crearne uno utilizzando hello [Guida introduttiva a Windows](quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="848b8-108">If you don't already have a VM toouse, you can create one using hello [Windows quickstart](quick-create-portal.md).</span></span> <span data-ttu-id="848b8-109">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="848b8-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="848b8-110">Creare un backup di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="848b8-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="848b8-111">Pianificare un backup giornaliero</span><span class="sxs-lookup"><span data-stu-id="848b8-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="848b8-112">Ripristinare un file da un backup</span><span class="sxs-lookup"><span data-stu-id="848b8-112">Restore a file from a backup</span></span>




## <a name="backup-overview"></a><span data-ttu-id="848b8-113">Panoramica del servizio Backup</span><span class="sxs-lookup"><span data-stu-id="848b8-113">Backup overview</span></span>

<span data-ttu-id="848b8-114">Quando hello servizio Backup di Azure avvia un processo di backup, attiva hello estensione backup tootake uno snapshot del punto nel tempo.</span><span class="sxs-lookup"><span data-stu-id="848b8-114">When hello Azure Backup service initiates a backup job, it triggers hello backup extension tootake a point-in-time snapshot.</span></span> <span data-ttu-id="848b8-115">Hello servizio Azure Backup utilizza hello _VMSnapshot_ estensione.</span><span class="sxs-lookup"><span data-stu-id="848b8-115">hello Azure Backup service uses hello _VMSnapshot_ extension.</span></span> <span data-ttu-id="848b8-116">estensione Hello viene installato durante il backup di VM prima hello se hello macchina virtuale è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="848b8-116">hello extension is installed during hello first VM backup if hello VM is running.</span></span> <span data-ttu-id="848b8-117">Se hello VM non è in esecuzione, il servizio di Backup hello crea uno snapshot di hello archiviazione sottostante (poiché non scritte dall'applicazione si verificano durante hello che macchina virtuale è stato arrestato).</span><span class="sxs-lookup"><span data-stu-id="848b8-117">If hello VM is not running, hello Backup service takes a snapshot of hello underlying storage (since no application writes occur while hello VM is stopped).</span></span>

<span data-ttu-id="848b8-118">Quando si acquisisce uno snapshot delle macchine virtuali di Windows, il servizio di Backup hello interagisce con hello del servizio Copia Shadow del Volume (VSS) tooget uno snapshot coerenza dei dischi della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="848b8-118">When taking a snapshot of Windows VMs, hello Backup service coordinates with hello Volume Shadow Copy Service (VSS) tooget a consistent snapshot of hello virtual machine's disks.</span></span> <span data-ttu-id="848b8-119">Una volta hello servizio Azure Backup istantanea hello, dati hello sono toohello trasferite insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="848b8-119">Once hello Azure Backup service takes hello snapshot, hello data is transferred toohello vault.</span></span> <span data-ttu-id="848b8-120">l'efficienza toomaximize servizio hello identifica e i trasferimenti di dati che sono stati modificati dal backup precedente hello solo i blocchi hello.</span><span class="sxs-lookup"><span data-stu-id="848b8-120">toomaximize efficiency, hello service identifies and transfers only hello blocks of data that have changed since hello previous backup.</span></span>

<span data-ttu-id="848b8-121">Una volta completato il trasferimento dei dati di hello, snapshot hello viene rimosso e viene creato un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="848b8-121">When hello data transfer is complete, hello snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="848b8-122">Creare un backup</span><span class="sxs-lookup"><span data-stu-id="848b8-122">Create a backup</span></span>
<span data-ttu-id="848b8-123">Creare un semplice pianificata giornaliera backup tooa insieme di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="848b8-123">Create a simple scheduled daily backup tooa Recovery Services Vault.</span></span> 

1. <span data-ttu-id="848b8-124">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="848b8-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="848b8-125">Dal menu hello hello sinistra, selezionare **macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="848b8-125">In hello menu on hello left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="848b8-126">Dall'elenco di hello, selezionare una macchina virtuale tooback backup.</span><span class="sxs-lookup"><span data-stu-id="848b8-126">From hello list, select a VM tooback up.</span></span>
4. <span data-ttu-id="848b8-127">Nel pannello VM hello in hello **impostazioni** fare clic su **Backup**.</span><span class="sxs-lookup"><span data-stu-id="848b8-127">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="848b8-128">Hello **Abilita backup** apre blade.</span><span class="sxs-lookup"><span data-stu-id="848b8-128">hello **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="848b8-129">In **insieme di credenziali di servizi di ripristino**, fare clic su **Crea nuovo** e specificare il nome di hello per nuovo insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="848b8-129">In **Recovery Services vault**, click **Create new** and provide hello name for hello new vault.</span></span> <span data-ttu-id="848b8-130">Viene creato un nuovo insieme di credenziali in hello stesso gruppo di risorse e il percorso come macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="848b8-130">A new vault is created in hello same Resource Group and location as hello virtual machine.</span></span>
6. <span data-ttu-id="848b8-131">Fare clic su **Criterio di Backup**.</span><span class="sxs-lookup"><span data-stu-id="848b8-131">Click **Backup policy**.</span></span> <span data-ttu-id="848b8-132">Per questo esempio, mantenere i valori predefiniti di hello e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="848b8-132">For this example, keep hello defaults and click **OK**.</span></span>
7. <span data-ttu-id="848b8-133">In hello **Abilita backup** pannello, fare clic su **Abilita Backup**.</span><span class="sxs-lookup"><span data-stu-id="848b8-133">On hello **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="848b8-134">Verrà creato un backup giornaliero in base alla pianificazione predefinita hello.</span><span class="sxs-lookup"><span data-stu-id="848b8-134">This creates a daily backup based on hello default schedule.</span></span>
10. <span data-ttu-id="848b8-135">un punto di ripristino iniziale, su hello toocreate **Backup** fare clic su pannello **Backup ora**.</span><span class="sxs-lookup"><span data-stu-id="848b8-135">toocreate an initial recovery point, on hello **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="848b8-136">In hello **Esegui Backup** pannello, fare clic sull'icona calendario hello, utilizzare hello tooselect di controllo calendario hello ultimo giorno di tale punto di ripristino è stato mantenuto e fare clic su **Backup**.</span><span class="sxs-lookup"><span data-stu-id="848b8-136">On hello **Backup Now** blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="848b8-137">In hello **Backup** pannello per la macchina virtuale, viene visualizzato un numero di punti di ripristino che sono state completate hello.</span><span class="sxs-lookup"><span data-stu-id="848b8-137">In hello **Backup** blade for your VM, you will see hello number of recovery points that are complete.</span></span>

    ![Punti di ripristino](./media/tutorial-backup-vms/backup-complete.png)
    
<span data-ttu-id="848b8-139">il primo backup di Hello richiede circa 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="848b8-139">hello first backup takes about 20 minutes.</span></span> <span data-ttu-id="848b8-140">Al termine del backup, procedere toohello parte successiva di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="848b8-140">Proceed toohello next part of this tutorial after your backup is finished.</span></span>

## <a name="recover-a-file"></a><span data-ttu-id="848b8-141">Recupero di un file</span><span class="sxs-lookup"><span data-stu-id="848b8-141">Recover a file</span></span>

<span data-ttu-id="848b8-142">Se accidentalmente si elimina o si apporta modifiche tooa file, è possibile utilizzare file di ripristino di File toorecover hello dall'insieme di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="848b8-142">If you accidentally delete or make changes tooa file, you can use File Recovery toorecover hello file from your backup vault.</span></span> <span data-ttu-id="848b8-143">Ripristino di file usa uno script eseguito nella macchina virtuale, hello toomount hello di punto di ripristino come unità locale.</span><span class="sxs-lookup"><span data-stu-id="848b8-143">File Recovery uses a script that runs on hello VM, toomount hello recovery point as local drive.</span></span> <span data-ttu-id="848b8-144">Queste unità rimarrà montate per 12 ore in modo che è possibile copiare i file dal punto di ripristino hello e ripristinarli toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="848b8-144">These drives will remain mounted for 12 hours so that you can copy files from hello recovery point and restore them toohello VM.</span></span>  

<span data-ttu-id="848b8-145">In questo esempio, ecco come toorecover hello file di immagine che viene utilizzata nella pagina web predefinita di hello per IIS.</span><span class="sxs-lookup"><span data-stu-id="848b8-145">In this example, we show how toorecover hello image file that is used in hello default web page for IIS.</span></span> 

1. <span data-ttu-id="848b8-146">Aprire un browser e connettersi toohello di indirizzo IP della pagina di hello VM tooshow hello predefinita IIS.</span><span class="sxs-lookup"><span data-stu-id="848b8-146">Open a browser and connect toohello IP address of hello VM tooshow hello default IIS page.</span></span>

    ![Pagina Web IIS predefinita](./media/tutorial-backup-vms/iis-working.png)

2. <span data-ttu-id="848b8-148">Connettersi toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="848b8-148">Connect toohello VM.</span></span>
3. <span data-ttu-id="848b8-149">In hello macchina virtuale, aprire **Esplora File** e passare too\inetpub\wwwroot ed eliminare file hello **iisstart.png**.</span><span class="sxs-lookup"><span data-stu-id="848b8-149">On hello VM, open **File Explorer** and navigate too\inetpub\wwwroot and delete hello file **iisstart.png**.</span></span>
4. <span data-ttu-id="848b8-150">Nel computer locale, l'aggiornamento hello browser toosee che hello immagine nella pagina IIS predefinita hello venga rimossa.</span><span class="sxs-lookup"><span data-stu-id="848b8-150">On your local computer, refresh hello browser toosee that hello image on hello default IIS page is gone.</span></span>

    ![Pagina Web IIS predefinita](./media/tutorial-backup-vms/iis-broken.png)

5. <span data-ttu-id="848b8-152">Nel computer locale, aprire una nuova scheda e hello hello passare [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="848b8-152">On your local computer, open a new tab and go hello hello [Azure portal](https://portal.azure.com).</span></span>
6. <span data-ttu-id="848b8-153">Dal menu hello hello sinistra, selezionare **macchine virtuali** e selezionare hello VM modulo hello elenco.</span><span class="sxs-lookup"><span data-stu-id="848b8-153">In hello menu on hello left, select **Virtual machines** and select hello VM form hello list.</span></span>
8. <span data-ttu-id="848b8-154">Nel pannello VM hello in hello **impostazioni** fare clic su **Backup**.</span><span class="sxs-lookup"><span data-stu-id="848b8-154">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="848b8-155">Hello **Backup** apre blade.</span><span class="sxs-lookup"><span data-stu-id="848b8-155">hello **Backup** blade opens.</span></span> 
9. <span data-ttu-id="848b8-156">Nel menu di hello nella parte superiore di hello del pannello hello, selezionare **ripristino File**.</span><span class="sxs-lookup"><span data-stu-id="848b8-156">In hello menu at hello top of hello blade, select **File Recovery**.</span></span> <span data-ttu-id="848b8-157">Hello **ripristino File** apre blade.</span><span class="sxs-lookup"><span data-stu-id="848b8-157">hello **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="848b8-158">In **passaggio 1: selezionare il punto di ripristino**, selezionare un punto di ripristino dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="848b8-158">In **Step 1: Select recovery point**, select a recovery point from hello drop-down.</span></span>
11. <span data-ttu-id="848b8-159">In **passaggio 2: scaricare script toobrowse e recuperare i file**, fare clic su hello **scaricare eseguibile** pulsante.</span><span class="sxs-lookup"><span data-stu-id="848b8-159">In **Step 2: Download script toobrowse and recover files**, click hello **Download Executable** button.</span></span> <span data-ttu-id="848b8-160">Salvare hello file tooyour **Scarica** cartella.</span><span class="sxs-lookup"><span data-stu-id="848b8-160">Save hello file tooyour **Downloads** folder.</span></span>
12. <span data-ttu-id="848b8-161">Nel computer locale, aprire **Esplora File** e passare tooyour **Scarica** hello cartella e copia scaricato file .exe.</span><span class="sxs-lookup"><span data-stu-id="848b8-161">On your local computer, open **File Explorer** and navigate tooyour **Downloads** folder and copy hello downloaded .exe file.</span></span> <span data-ttu-id="848b8-162">nome file Hello è preceduto dal nome macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="848b8-162">hello filename will be prefixed by your VM name.</span></span> 
13. <span data-ttu-id="848b8-163">La macchina virtuale (sulla connessione RDP hello) incollare hello .exe file toohello Desktop della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="848b8-163">On your VM (over hello RDP connection) paste hello .exe file toohello Desktop of your VM.</span></span> 
14. <span data-ttu-id="848b8-164">Passare toohello desktop della macchina virtuale e fare doppio clic su .exe hello.</span><span class="sxs-lookup"><span data-stu-id="848b8-164">Navigate toohello desktop of your VM and double-click on hello .exe.</span></span> <span data-ttu-id="848b8-165">Verrà avviato un prompt dei comandi e quindi montare il punto di ripristino hello come condivisione file che è possibile accedere.</span><span class="sxs-lookup"><span data-stu-id="848b8-165">This will launch a command prompt and then mount hello recovery point as a file share that you can access.</span></span> <span data-ttu-id="848b8-166">Al termine Crea condivisione hello, digitare **q** tooclose hello il prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="848b8-166">When it is finished creating hello share, type **q** tooclose hello command prompt.</span></span>
15. <span data-ttu-id="848b8-167">Nella macchina virtuale, aprire **Esplora File** e passare toohello lettera di unità utilizzata per la condivisione di file hello.</span><span class="sxs-lookup"><span data-stu-id="848b8-167">On your VM, open **File Explorer** and navigate toohello drive letter that was used for hello file share.</span></span>
16. <span data-ttu-id="848b8-168">Passare too\inetpub\wwwroot e copia **iisstart.png** dal file hello condividere e incollarlo in \Inetpub\Wwwroot..</span><span class="sxs-lookup"><span data-stu-id="848b8-168">Navigate too\inetpub\wwwroot and copy **iisstart.png** from hello file share and paste it into \inetpub\wwwroot.</span></span> <span data-ttu-id="848b8-169">Ad esempio, copiare F:\inetpub\wwwroot\iisstart.png e incollarlo nel file di c:\inetpub\wwwroot toorecover hello.</span><span class="sxs-lookup"><span data-stu-id="848b8-169">For example, copy F:\inetpub\wwwroot\iisstart.png and paste it into c:\inetpub\wwwroot toorecover hello file.</span></span>
17. <span data-ttu-id="848b8-170">Nel computer locale, aprire scheda del browser hello in cui si è connessi toohello di indirizzo IP della pagina predefinita di hello VM con hello IIS.</span><span class="sxs-lookup"><span data-stu-id="848b8-170">On your local computer, open hello browser tab where you are connected toohello IP address of hello VM showing hello IIS default page.</span></span> <span data-ttu-id="848b8-171">Premere CTRL + F5 pagina nel browser toorefresh hello.</span><span class="sxs-lookup"><span data-stu-id="848b8-171">Press CTRL + F5 toorefresh hello browser page.</span></span> <span data-ttu-id="848b8-172">Si noterà ora che hello immagine è stata ripristinata.</span><span class="sxs-lookup"><span data-stu-id="848b8-172">You should now see that hello image has been restored.</span></span>
18. <span data-ttu-id="848b8-173">Nel computer locale, tornare indietro toohello per hello portale di Azure e nella scheda del browser **passaggio 3: smontare dischi hello dopo il ripristino** fare clic su hello **smontare dischi** pulsante.</span><span class="sxs-lookup"><span data-stu-id="848b8-173">On your local computer, go back toohello browser tab for hello Azure portal and in **Step 3: Unmount hello disks after recovery** click hello **Unmount Disks** button.</span></span> <span data-ttu-id="848b8-174">Se si dimentica toodo questo passaggio, punto di montaggio toohello hello connessione è chiusa automaticamente dopo 12 ore.</span><span class="sxs-lookup"><span data-stu-id="848b8-174">If you forget toodo this step, hello connection toohello mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="848b8-175">Dopo queste 12 ore, è necessario toodownload un nuovo toocreate script un nuovo punto di montaggio.</span><span class="sxs-lookup"><span data-stu-id="848b8-175">After those 12 hours, you need toodownload a new script toocreate a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="848b8-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="848b8-176">Next steps</span></span>

<span data-ttu-id="848b8-177">In questa esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="848b8-177">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="848b8-178">Creare un backup di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="848b8-178">Create a backup of a VM</span></span>
> * <span data-ttu-id="848b8-179">Pianificare un backup giornaliero</span><span class="sxs-lookup"><span data-stu-id="848b8-179">Schedule a daily backup</span></span>
> * <span data-ttu-id="848b8-180">Ripristinare un file da un backup</span><span class="sxs-lookup"><span data-stu-id="848b8-180">Restore a file from a backup</span></span>

<span data-ttu-id="848b8-181">Spostare toohello toolearn esercitazione successiva sul monitoraggio delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="848b8-181">Advance toohello next tutorial toolearn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="848b8-182">Monitorare le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="848b8-182">Monitor virtual machines</span></span>](tutorial-monitoring.md)









