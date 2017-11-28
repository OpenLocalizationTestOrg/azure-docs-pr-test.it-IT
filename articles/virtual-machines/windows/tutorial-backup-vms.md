---
title: Eseguire il backup di macchine virtuali Windows in Azure | Microsoft Docs
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
ms.openlocfilehash: 8e58a2290e5034ef393f65cbcddb86e18cf4a6ec
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="back-up-windows-virtual-machines-in-azure"></a><span data-ttu-id="b46cf-103">Eseguire il backup di macchine virtuali Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="b46cf-103">Back up Windows virtual machines in Azure</span></span>

<span data-ttu-id="b46cf-104">È possibile proteggere i dati eseguendo backup a intervalli regolari.</span><span class="sxs-lookup"><span data-stu-id="b46cf-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="b46cf-105">Backup di Azure crea punti di recupero che vengono archiviati negli insiemi di credenziali di ripristino con ridondanza geografica.</span><span class="sxs-lookup"><span data-stu-id="b46cf-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="b46cf-106">Quando si ripristina da un punto di recupero, è possibile ripristinare la macchina virtuale intera o parziale.</span><span class="sxs-lookup"><span data-stu-id="b46cf-106">When you restore from a recovery point, you can restore the whole VM or just specific files.</span></span> <span data-ttu-id="b46cf-107">Questo articolo spiega come ripristinare un singolo file in una macchina virtuale che esegue Windows Server e IIS.</span><span class="sxs-lookup"><span data-stu-id="b46cf-107">This article explains how to restore a single file to a VM running Windows Server and IIS.</span></span> <span data-ttu-id="b46cf-108">Se non si dispone già di una macchina virtuale da usare, è possibile crearne una usando la [guida introduttiva di Windows](quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b46cf-108">If you don't already have a VM to use, you can create one using the [Windows quickstart](quick-create-portal.md).</span></span> <span data-ttu-id="b46cf-109">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="b46cf-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b46cf-110">Creare un backup di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b46cf-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="b46cf-111">Pianificare un backup giornaliero</span><span class="sxs-lookup"><span data-stu-id="b46cf-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="b46cf-112">Ripristinare un file da un backup</span><span class="sxs-lookup"><span data-stu-id="b46cf-112">Restore a file from a backup</span></span>




## <a name="backup-overview"></a><span data-ttu-id="b46cf-113">Panoramica del servizio Backup</span><span class="sxs-lookup"><span data-stu-id="b46cf-113">Backup overview</span></span>

<span data-ttu-id="b46cf-114">Quando il servizio Backup di Azure avvia un processo di backup, attiva l'estensione per il backup per acquisire uno snapshot temporizzato.</span><span class="sxs-lookup"><span data-stu-id="b46cf-114">When the Azure Backup service initiates a backup job, it triggers the backup extension to take a point-in-time snapshot.</span></span> <span data-ttu-id="b46cf-115">Il servizio Backup di Azure usa l'estensione _VMSnapshot_.</span><span class="sxs-lookup"><span data-stu-id="b46cf-115">The Azure Backup service uses the _VMSnapshot_ extension.</span></span> <span data-ttu-id="b46cf-116">L'estensione viene installata durante il primo backup della macchina virtuale se la macchina virtuale è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b46cf-116">The extension is installed during the first VM backup if the VM is running.</span></span> <span data-ttu-id="b46cf-117">Se la macchina virtuale non è in esecuzione, il servizio Backup crea uno snapshot dell'archivio sottostante (poiché non si verifica alcuna scrittura di applicazione durante l'arresto della macchina virtuale).</span><span class="sxs-lookup"><span data-stu-id="b46cf-117">If the VM is not running, the Backup service takes a snapshot of the underlying storage (since no application writes occur while the VM is stopped).</span></span>

<span data-ttu-id="b46cf-118">Quando crea uno snapshot delle macchine virtuali di Windows, il servizio Backup si coordina con il servizio Copia Shadow del volume (VSS) per ottenere uno snapshot coerente dei dischi delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="b46cf-118">When taking a snapshot of Windows VMs, the Backup service coordinates with the Volume Shadow Copy Service (VSS) to get a consistent snapshot of the virtual machine's disks.</span></span> <span data-ttu-id="b46cf-119">Dopo che il servizio Backup di Azure crea lo snapshot, i data vengono trasferiti nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="b46cf-119">Once the Azure Backup service takes the snapshot, the data is transferred to the vault.</span></span> <span data-ttu-id="b46cf-120">Per offrire la massima efficienza, il servizio identifica e trasferisce solo i blocchi di dati che sono stati modificati dall'ultimo backup.</span><span class="sxs-lookup"><span data-stu-id="b46cf-120">To maximize efficiency, the service identifies and transfers only the blocks of data that have changed since the previous backup.</span></span>

<span data-ttu-id="b46cf-121">Quando il trasferimento dei dati è completato, lo snapshot viene rimosso e viene creato un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="b46cf-121">When the data transfer is complete, the snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="b46cf-122">Creare un backup</span><span class="sxs-lookup"><span data-stu-id="b46cf-122">Create a backup</span></span>
<span data-ttu-id="b46cf-123">Creare un semplice backup giornaliero pianificato per un insieme di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="b46cf-123">Create a simple scheduled daily backup to a Recovery Services Vault.</span></span> 

1. <span data-ttu-id="b46cf-124">Accedere al [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b46cf-124">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b46cf-125">Nel menu a sinistra selezionare **Macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="b46cf-125">In the menu on the left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="b46cf-126">Dall'elenco selezionare la macchina virtuale di cui eseguire il backup.</span><span class="sxs-lookup"><span data-stu-id="b46cf-126">From the list, select a VM to back up.</span></span>
4. <span data-ttu-id="b46cf-127">Nel pannello della macchina virtuale, nella sezione **Impostazioni** fare clic su **Backup**.</span><span class="sxs-lookup"><span data-stu-id="b46cf-127">On the VM blade, in the **Settings** section, click **Backup**.</span></span> <span data-ttu-id="b46cf-128">Verrà aperto il pannello **Abilita backup**.</span><span class="sxs-lookup"><span data-stu-id="b46cf-128">The **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="b46cf-129">In **Insieme di credenziali dei servizi di ripristino** fare clic su **Crea nuovo** e inserire un nome per il nuovo insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="b46cf-129">In **Recovery Services vault**, click **Create new** and provide the name for the new vault.</span></span> <span data-ttu-id="b46cf-130">Viene creato un nuovo insieme di credenziali nello stesso gruppo di risorse e nello stesso percorso della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b46cf-130">A new vault is created in the same Resource Group and location as the virtual machine.</span></span>
6. <span data-ttu-id="b46cf-131">Fare clic su **Criterio di Backup**.</span><span class="sxs-lookup"><span data-stu-id="b46cf-131">Click **Backup policy**.</span></span> <span data-ttu-id="b46cf-132">Per questo esempio, mantenere le impostazioni predefinite e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b46cf-132">For this example, keep the defaults and click **OK**.</span></span>
7. <span data-ttu-id="b46cf-133">Nel pannello **Abilita backup** fare clic su **Abilita backup**.</span><span class="sxs-lookup"><span data-stu-id="b46cf-133">On the **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="b46cf-134">Verrà creato un backup giornaliero in base alla pianificazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b46cf-134">This creates a daily backup based on the default schedule.</span></span>
10. <span data-ttu-id="b46cf-135">Per creare un punto di recupero iniziale, nel pannello **Backup** fare clic su **Esegui backup ora**.</span><span class="sxs-lookup"><span data-stu-id="b46cf-135">To create an initial recovery point, on the **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="b46cf-136">Nel pannello **Esegui backup ora** fare clic sull'icona del calendario, usare il comando del calendario per selezionare l'ultimo giorno di conservazione di tale punto di recupero e fare clic su **Backup**.</span><span class="sxs-lookup"><span data-stu-id="b46cf-136">On the **Backup Now** blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="b46cf-137">Nel pannello **Backup** per la macchina virtuale in uso verrà visualizzato il numero di punti di recupero completati.</span><span class="sxs-lookup"><span data-stu-id="b46cf-137">In the **Backup** blade for your VM, you will see the number of recovery points that are complete.</span></span>

    ![Punti di ripristino](./media/tutorial-backup-vms/backup-complete.png)
    
<span data-ttu-id="b46cf-139">Il primo backup richiede circa 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="b46cf-139">The first backup takes about 20 minutes.</span></span> <span data-ttu-id="b46cf-140">Al termine del backup, procedere con la parte successiva di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b46cf-140">Proceed to the next part of this tutorial after your backup is finished.</span></span>

## <a name="recover-a-file"></a><span data-ttu-id="b46cf-141">Recupero di un file</span><span class="sxs-lookup"><span data-stu-id="b46cf-141">Recover a file</span></span>

<span data-ttu-id="b46cf-142">Se accidentalmente si elimina o si apportano modifiche a un file, è possibile usare Ripristino file per ripristinare il file dall'insieme di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="b46cf-142">If you accidentally delete or make changes to a file, you can use File Recovery to recover the file from your backup vault.</span></span> <span data-ttu-id="b46cf-143">Ripristino file usa uno script eseguito nella macchina virtuale, per montare il punto di recupero come unità locale.</span><span class="sxs-lookup"><span data-stu-id="b46cf-143">File Recovery uses a script that runs on the VM, to mount the recovery point as local drive.</span></span> <span data-ttu-id="b46cf-144">Queste unità rimarranno montate per 12 ore in modo che sia possibile copiare i file dal punto di recupero e ripristinarli nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b46cf-144">These drives will remain mounted for 12 hours so that you can copy files from the recovery point and restore them to the VM.</span></span>  

<span data-ttu-id="b46cf-145">Questo esempio spiega come ripristinare il file di immagine usato nella pagina Web predefinita per IIS.</span><span class="sxs-lookup"><span data-stu-id="b46cf-145">In this example, we show how to recover the image file that is used in the default web page for IIS.</span></span> 

1. <span data-ttu-id="b46cf-146">Aprire un browser e connettersi all'indirizzo IP della macchina virtuale per visualizzare la pagina IIS predefinita.</span><span class="sxs-lookup"><span data-stu-id="b46cf-146">Open a browser and connect to the IP address of the VM to show the default IIS page.</span></span>

    ![Pagina Web IIS predefinita](./media/tutorial-backup-vms/iis-working.png)

2. <span data-ttu-id="b46cf-148">Connettersi alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b46cf-148">Connect to the VM.</span></span>
3. <span data-ttu-id="b46cf-149">Nella macchina virtuale aprire **Esplora file**, passare a \inetpub\wwwroot ed eliminare il file **iisstart.png**.</span><span class="sxs-lookup"><span data-stu-id="b46cf-149">On the VM, open **File Explorer** and navigate to \inetpub\wwwroot and delete the file **iisstart.png**.</span></span>
4. <span data-ttu-id="b46cf-150">Nel computer locale aggiornare il browser per verificare che l'immagine nella pagina IIS predefinita non sia più presente.</span><span class="sxs-lookup"><span data-stu-id="b46cf-150">On your local computer, refresh the browser to see that the image on the default IIS page is gone.</span></span>

    ![Pagina Web IIS predefinita](./media/tutorial-backup-vms/iis-broken.png)

5. <span data-ttu-id="b46cf-152">Nel computer locale aprire una nuova scheda e passare al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b46cf-152">On your local computer, open a new tab and go the the [Azure portal](https://portal.azure.com).</span></span>
6. <span data-ttu-id="b46cf-153">Nel menu a sinistra selezionare **Macchine virtuali** e selezionare la macchina virtuale dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="b46cf-153">In the menu on the left, select **Virtual machines** and select the VM form the list.</span></span>
8. <span data-ttu-id="b46cf-154">Nel pannello della macchina virtuale, nella sezione **Impostazioni** fare clic su **Backup**.</span><span class="sxs-lookup"><span data-stu-id="b46cf-154">On the VM blade, in the **Settings** section, click **Backup**.</span></span> <span data-ttu-id="b46cf-155">Verrà visualizzato il pannello **Backup**.</span><span class="sxs-lookup"><span data-stu-id="b46cf-155">The **Backup** blade opens.</span></span> 
9. <span data-ttu-id="b46cf-156">Dal menu nella parte superiore del pannello scegliere **Ripristino file**.</span><span class="sxs-lookup"><span data-stu-id="b46cf-156">In the menu at the top of the blade, select **File Recovery**.</span></span> <span data-ttu-id="b46cf-157">Verrà aperto il pannello **Ripristino file**.</span><span class="sxs-lookup"><span data-stu-id="b46cf-157">The **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="b46cf-158">In **Passaggio 1: Selezionare il punto di recupero** selezionare un punto di recupero dall'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="b46cf-158">In **Step 1: Select recovery point**, select a recovery point from the drop-down.</span></span>
11. <span data-ttu-id="b46cf-159">In **Passaggio 2: Scaricare lo script per cercare e ripristinare i file** fare clic sul pulsante **Scarica eseguibile**.</span><span class="sxs-lookup"><span data-stu-id="b46cf-159">In **Step 2: Download script to browse and recover files**, click the **Download Executable** button.</span></span> <span data-ttu-id="b46cf-160">Salvare il file nella cartella **Downloads**.</span><span class="sxs-lookup"><span data-stu-id="b46cf-160">Save the file to your **Downloads** folder.</span></span>
12. <span data-ttu-id="b46cf-161">Nel computer locale aprire **Esplora file**, andare alla cartella **Downloads** e copiare il file con estensione exe scaricato.</span><span class="sxs-lookup"><span data-stu-id="b46cf-161">On your local computer, open **File Explorer** and navigate to your **Downloads** folder and copy the downloaded .exe file.</span></span> <span data-ttu-id="b46cf-162">Il nome del file verrà preceduto dal nome della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b46cf-162">The filename will be prefixed by your VM name.</span></span> 
13. <span data-ttu-id="b46cf-163">Incollare il file con estensione exe sul desktop della macchina virtuale (tramite la connessione RDP).</span><span class="sxs-lookup"><span data-stu-id="b46cf-163">On your VM (over the RDP connection) paste the .exe file to the Desktop of your VM.</span></span> 
14. <span data-ttu-id="b46cf-164">Passare al desktop della macchina virtuale e fare doppio clic sul file con estensione exe.</span><span class="sxs-lookup"><span data-stu-id="b46cf-164">Navigate to the desktop of your VM and double-click on the .exe.</span></span> <span data-ttu-id="b46cf-165">Verrà aperto un prompt dei comandi e il punto di recupero sarà montato come condivisione di file a cui è possibile accedere.</span><span class="sxs-lookup"><span data-stu-id="b46cf-165">This will launch a command prompt and then mount the recovery point as a file share that you can access.</span></span> <span data-ttu-id="b46cf-166">Al termine della creazione della condivisione, digitare **q** per chiudere il prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="b46cf-166">When it is finished creating the share, type **q** to close the command prompt.</span></span>
15. <span data-ttu-id="b46cf-167">Nella macchina virtuale aprire **Esplora file** e passare alla lettera di unità usata per la condivisione file.</span><span class="sxs-lookup"><span data-stu-id="b46cf-167">On your VM, open **File Explorer** and navigate to the drive letter that was used for the file share.</span></span>
16. <span data-ttu-id="b46cf-168">Passare a \inetpub\wwwroot e copiare **iisstart.png** dalla condivisione file e incollarlo in \inetpub\wwwroot.</span><span class="sxs-lookup"><span data-stu-id="b46cf-168">Navigate to \inetpub\wwwroot and copy **iisstart.png** from the file share and paste it into \inetpub\wwwroot.</span></span> <span data-ttu-id="b46cf-169">Ad esempio, copiare F:\inetpub\wwwroot\iisstart.png e incollarlo in c:\inetpub\wwwroot per ripristinare il file.</span><span class="sxs-lookup"><span data-stu-id="b46cf-169">For example, copy F:\inetpub\wwwroot\iisstart.png and paste it into c:\inetpub\wwwroot to recover the file.</span></span>
17. <span data-ttu-id="b46cf-170">Nel computer locale aprire la scheda del browser in cui si è connessi all'indirizzo IP della macchina virtuale che mostra la pagina IIS predefinita.</span><span class="sxs-lookup"><span data-stu-id="b46cf-170">On your local computer, open the browser tab where you are connected to the IP address of the VM showing the IIS default page.</span></span> <span data-ttu-id="b46cf-171">Premere CTRL + F5 per aggiornare la pagina del browser.</span><span class="sxs-lookup"><span data-stu-id="b46cf-171">Press CTRL + F5 to refresh the browser page.</span></span> <span data-ttu-id="b46cf-172">Si noterà ora che l'immagine è stata ripristinata.</span><span class="sxs-lookup"><span data-stu-id="b46cf-172">You should now see that the image has been restored.</span></span>
18. <span data-ttu-id="b46cf-173">Nel computer locale tornare alla scheda del browser per il portale di Azure e in **Passaggio 3: Smontare i dischi dopo il ripristino** fare clic sul pulsante **Smontare i dischi**.</span><span class="sxs-lookup"><span data-stu-id="b46cf-173">On your local computer, go back to the browser tab for the Azure portal and in **Step 3: Unmount the disks after recovery** click the **Unmount Disks** button.</span></span> <span data-ttu-id="b46cf-174">Se si dimentica di eseguire questo passaggio, la connessione per il punto di montaggio viene chiusa automaticamente dopo 12 ore.</span><span class="sxs-lookup"><span data-stu-id="b46cf-174">If you forget to do this step, the connection to the mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="b46cf-175">Trascorse le 12 ore, è necessario scaricare un nuovo script per creare un nuovo punto di montaggio.</span><span class="sxs-lookup"><span data-stu-id="b46cf-175">After those 12 hours, you need to download a new script to create a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b46cf-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b46cf-176">Next steps</span></span>

<span data-ttu-id="b46cf-177">In questa esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="b46cf-177">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b46cf-178">Creare un backup di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b46cf-178">Create a backup of a VM</span></span>
> * <span data-ttu-id="b46cf-179">Pianificare un backup giornaliero</span><span class="sxs-lookup"><span data-stu-id="b46cf-179">Schedule a daily backup</span></span>
> * <span data-ttu-id="b46cf-180">Ripristinare un file da un backup</span><span class="sxs-lookup"><span data-stu-id="b46cf-180">Restore a file from a backup</span></span>

<span data-ttu-id="b46cf-181">Passare all'esercitazione successiva per informazioni sul monitoraggio di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="b46cf-181">Advance to the next tutorial to learn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b46cf-182">Monitorare le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="b46cf-182">Monitor virtual machines</span></span>](tutorial-monitoring.md)









