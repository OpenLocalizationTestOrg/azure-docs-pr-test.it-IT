---
title: Ripristinare dati in Azure in un computer di Windows Server o in un client Windows | Microsoft Docs
description: Informazioni su come ripristinare i dati archiviati in Azure in un computer di Windows Server o in un client Windows.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 742f4b9e-c0ab-4eeb-8e22-ee29b83c22c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/16/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 231dd61f95267b3a504ed70e9b3a5abc470b69b2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="restore-files-to-a-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a><span data-ttu-id="0fd2d-103">Ripristinare file in un computer di Windows Server o in un client Windows con il modello di distribuzione di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0fd2d-103">Restore files to a Windows server or Windows client machine using Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0fd2d-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0fd2d-104">Azure portal</span></span>](backup-azure-restore-windows-server.md)
> * [<span data-ttu-id="0fd2d-105">Portale classico</span><span class="sxs-lookup"><span data-stu-id="0fd2d-105">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
>
>

<span data-ttu-id="0fd2d-106">Questo articolo illustra come ripristinare i dati da un insieme di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-106">This article explains how to restore data from a backup vault.</span></span> <span data-ttu-id="0fd2d-107">Per ripristinare i dati, usare la procedura di ripristino guidato dei dati nell'agente di Servizi di ripristino di Microsoft Azure (MARS).</span><span class="sxs-lookup"><span data-stu-id="0fd2d-107">To restore data, you use the Recover Data wizard in the Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="0fd2d-108">Quando si ripristinano dati, è possibile:</span><span class="sxs-lookup"><span data-stu-id="0fd2d-108">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="0fd2d-109">Ripristinare i dati nello stesso computer in cui sono stati eseguiti i backup.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-109">Restore data to the same machine from which the backups were taken.</span></span>
* <span data-ttu-id="0fd2d-110">Ripristinare i dati in un'altra macchina.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-110">Restore data to an alternate machine.</span></span>

<span data-ttu-id="0fd2d-111">A gennaio 2017 Microsoft ha rilasciato un aggiornamento in anteprima all'agente MARS.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-111">In January 2017, Microsoft released a Preview update to the MARS agent.</span></span> <span data-ttu-id="0fd2d-112">Insieme alle correzioni di bug, questo aggiornamento abilita la funzione di ripristino istantaneo, che consente di montare uno snapshot del punto di ripristino scrivibile come volume di ripristino.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-112">Along with bug fixes, this update enables Instant Restore, which allows you to mount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="0fd2d-113">È quindi possibile esplorare il volume di ripristino e i file di copia in un computer locale, ripristinando quindi i file in modo selettivo.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-113">You can then explore the recovery volume and copy files to a local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="0fd2d-114">Se si vuole usare questa funzione per ripristinare i dati, è necessario l'[aggiornamento di Backup di Azure di gennaio 2017](https://support.microsoft.com/en-us/help/3216528?preview).</span><span class="sxs-lookup"><span data-stu-id="0fd2d-114">The [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want to use Instant Restore to restore data.</span></span> <span data-ttu-id="0fd2d-115">È necessario anche che i dati di backup siano protetti in insiemi di credenziali nelle impostazioni locali elencate nell'articolo del supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-115">Also the backup data must be protected in vaults in locales listed in the support article.</span></span> <span data-ttu-id="0fd2d-116">Consultare l'[aggiornamento di Azure Backup di gennaio 2017](https://support.microsoft.com/en-us/help/3216528?preview) per un elenco aggiornato delle impostazioni locali che supportano la funzione di ripristino istantaneo.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-116">Consult the [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for the latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="0fd2d-117">Il ripristino istantaneo **non** è attualmente disponibile in tutte le impostazioni locali.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-117">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="0fd2d-118">È disponibile per l'uso negli insiemi di credenziali di Servizi di ripristino nel portale di Azure e negli insiemi di credenziali di Backup nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-118">Instant Restore is available for use in Recovery Services vaults in the Azure portal and Backup vaults in the classic portal.</span></span> <span data-ttu-id="0fd2d-119">Se si vuole usare la funzione di ripristino istantaneo, scaricare l'aggiornamento di MARS e seguire le procedure relative al ripristino istantaneo.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-119">If you want to use Instant Restore, download the MARS update, and follow the procedures that mention Instant Restore.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="use-instant-restore-to-recover-data-to-the-same-machine"></a><span data-ttu-id="0fd2d-120">Usare la funzione di ripristino istantaneo per ripristinare i dati sullo stesso computer</span><span class="sxs-lookup"><span data-stu-id="0fd2d-120">Use Instant Restore to recover data to the same machine</span></span>

<span data-ttu-id="0fd2d-121">Se un file è stato eliminato accidentalmente e lo si vuole ripristinare nello stesso computer in cui è stato eseguito il backup, la seguente procedura permette di recuperarlo.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-121">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span></span>

1. <span data-ttu-id="0fd2d-122">Aprire lo snap-in di **Backup di Microsoft Azure** .</span><span class="sxs-lookup"><span data-stu-id="0fd2d-122">Open the **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="0fd2d-123">Se non si sa dove è stato installato lo snap-in, cercare **Backup di Microsoft Azure** nel computer o nel server.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-123">If you don't know where the snap in was installed, search the computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="0fd2d-124">L'applicazione desktop dovrebbe essere visualizzata nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-124">The desktop app should appear in the search results.</span></span>

2. <span data-ttu-id="0fd2d-125">Fare clic su **Ripristina dati** per avviare la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-125">Click **Recover Data** to start the wizard.</span></span>

    ![Ripristina dati](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="0fd2d-127">Nel riquadro **Guida introduttiva** selezionare l'opzione **This server (Questo server) (`<server name>`)** e fare clic su **Avanti** per ripristinare i dati nello stesso server o computer.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-127">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Scegliere l'opzione This server (Questo server) per ripristinare i dati nello stesso computer](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="0fd2d-129">Nel riquadro **Seleziona modalità di ripristino** selezionare **Singoli file e cartelle** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-129">On the **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Ricerca dei file](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="0fd2d-131">Nel riquadro **Seleziona volume e data** selezionare il volume che contiene i file e/o le cartelle da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-131">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="0fd2d-132">Nel calendario selezionare un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-132">On the calendar, select a recovery point.</span></span> <span data-ttu-id="0fd2d-133">È possibile ripristinare da qualsiasi punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-133">You can restore from any recovery point in time.</span></span> <span data-ttu-id="0fd2d-134">Le date in **grassetto** indicano la disponibilità di almeno un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-134">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="0fd2d-135">Dopo aver selezionato una data, se sono disponibili più punti di ripristino, scegliere quello appropriato dall'elenco a discesa **Ora**.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-135">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Volume e dati](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="0fd2d-137">Dopo aver selezionato il punto di ripristino, fare clic su **Monta**.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-137">Once you have chosen the recovery point to restore, click **Mount**.</span></span>

    <span data-ttu-id="0fd2d-138">Backup di Azure monta il punto di ripristino locale e lo usa come volume di ripristino.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-138">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="0fd2d-139">Nel riquadro **Cerca e ripristina file** fare clic su **Sfoglia** per aprire Esplora risorse e individuare i file e le cartelle desiderati.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-139">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Opzioni di ripristino](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="0fd2d-141">In Esplora risorse copiare i file e/o le cartelle che si desidera ripristinare e incollarle in qualsiasi posizione locale nel server o nel computer.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-141">In Windows Explorer, copy the files and/or folders you want to restore and paste them to any location local to the server or computer.</span></span> <span data-ttu-id="0fd2d-142">È possibile aprire o trasmettere i file direttamente dal volume di ripristino e verificare che vengano ripristinate le versioni corrette.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-142">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Copiare e incollare file e cartelle dal volume montato alla posizione locale](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="0fd2d-144">Dopo aver terminato il ripristino di file e/o cartelle, fare clic su **Smonta** nel riquadro **Cerca e ripristina file**.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-144">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="0fd2d-145">Fare clic su **Sì** per confermare che si desidera smontare il volume.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-145">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Smontare il volume e confermare](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="0fd2d-147">Se non si fa clic su Smonta, il volume di ripristino resterà montato per 6 ore.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-147">If you do not click Unmount, the Recovery Volume will remain mounted for 6 hours from the time when it was mounted.</span></span> <span data-ttu-id="0fd2d-148">Il tempo di montaggio viene tuttavia esteso fino a un massimo di 24 ore in caso di copia dei file in corso.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-148">However, the mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="0fd2d-149">Mentre il volume è montato, non vengono eseguite operazioni di backup.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-149">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="0fd2d-150">Qualsiasi operazione di backup pianificata durante il periodo in cui il volume è montato verrà eseguita dopo lo smontaggio del volume di ripristino.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-150">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >


## <a name="use-instant-restore-to-restore-data-to-an-alternate-machine"></a><span data-ttu-id="0fd2d-151">Usare il ripristino immediato per ripristinare i dati in un altro computer</span><span class="sxs-lookup"><span data-stu-id="0fd2d-151">Use Instant Restore to restore data to an alternate machine</span></span>
<span data-ttu-id="0fd2d-152">Se l'intero server viene perso, è comunque possibile recuperare dati da Backup di Azure in un computer diverso.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-152">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span></span> <span data-ttu-id="0fd2d-153">I passaggi seguenti illustrano il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-153">The following steps illustrate the workflow.</span></span>


<span data-ttu-id="0fd2d-154">Include la terminologia utilizzata in questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="0fd2d-154">The terminology used in these steps includes:</span></span>

* <span data-ttu-id="0fd2d-155">*Computer di origine* : il computer di origine da cui è stato eseguito il backup e che non è attualmente disponibile.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-155">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="0fd2d-156">*Computer di destinazione* : il computer in cui i dati vengono ripristinati.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-156">*Target machine* – The machine to which the data is being recovered.</span></span>
* <span data-ttu-id="0fd2d-157">*Insieme di credenziali di esempio*: l'insieme di credenziali dei servizi di ripristino in cui il *computer di origine* e il *computer di destinazione* sono registrati.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-157">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="0fd2d-158">Non è possibile ripristinare i backup in un computer di destinazione che esegue una versione precedente del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-158">Backups can't be restored to a target machine running an earlier version of the operating system.</span></span> <span data-ttu-id="0fd2d-159">Ad esempio, un backup eseguito su un computer con Windows 7 può essere ripristinato in un computer con Windows 8 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-159">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="0fd2d-160">Un backup eseguito su un computer con Windows 8 non può essere ripristinato in un computer con Windows 7.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-160">A backup taken from a Windows 8 computer cannot be restored to a Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="0fd2d-161">Aprire lo snap-in di **Backup di Microsoft Azure** nel *Computer di destinazione*.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-161">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span></span>

2. <span data-ttu-id="0fd2d-162">Assicurarsi che il *computer di destinazione* e il *computer di origine* siano registrati nello stesso insieme di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-162">Ensure the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span></span>

3. <span data-ttu-id="0fd2d-163">Fare clic su **Ripristina dati** per aprire il **ripristino guidato dei dati**.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-163">Click **Recover Data** to open the **Recover Data wizard**.</span></span>

    ![Ripristina dati](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="0fd2d-165">Nel riquadro **Guida introduttiva** selezionare **Another server** (Un altro server)</span><span class="sxs-lookup"><span data-stu-id="0fd2d-165">On the **Getting Started** pane, select **Another server**</span></span>

    ![Un altro server](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="0fd2d-167">Specificare il file dell'insieme di credenziali che corrisponde all'*insieme di credenziali di esempio*, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-167">Provide the vault credential file that corresponds to the *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="0fd2d-168">Se il file dell'insieme di credenziali non è valido (o è scaduto), è necessario scaricarne uno nuovo dall'*insieme di credenziali di esempio* nel Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-168">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span></span> <span data-ttu-id="0fd2d-169">Dopo aver specificato un insieme di credenziali valido, viene visualizzato il nome dell'insieme di credenziali di backup corrispondente.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-169">Once you provide a valid vault credential, the name of the corresponding Backup Vault appears.</span></span>


6. <span data-ttu-id="0fd2d-170">Nel riquadro **Seleziona server di backup** selezionare il *computer di origine* dall'elenco dei computer visualizzati e specificare la passphrase.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-170">On the **Select Backup Server** pane, select the *Source machine* from the list of displayed machines and provide the passphrase.</span></span> <span data-ttu-id="0fd2d-171">Quindi fare clic su **Next**.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-171">Then click **Next**.</span></span>

    ![Elenco di computer](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="0fd2d-173">Nel riquadro **Seleziona modalità di ripristino** selezionare **Singoli file e cartelle** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-173">On the **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Search](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="0fd2d-175">Nel riquadro **Seleziona volume e data** selezionare il volume che contiene i file e/o le cartelle da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-175">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="0fd2d-176">Nel calendario selezionare un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-176">On the calendar, select a recovery point.</span></span> <span data-ttu-id="0fd2d-177">È possibile ripristinare da qualsiasi punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-177">You can restore from any recovery point in time.</span></span> <span data-ttu-id="0fd2d-178">Le date in **grassetto** indicano la disponibilità di almeno un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-178">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="0fd2d-179">Dopo aver selezionato una data, se sono disponibili più punti di ripristino, scegliere quello appropriato dall'elenco a discesa **Ora**.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-179">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Ricerca di elementi](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="0fd2d-181">Fare clic su **Monta** per montare localmente il punto di ripristino come volume di ripristino sul *computer di destinazione*.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-181">Click **Mount** to locally mount the recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="0fd2d-182">Nel riquadro **Cerca e ripristina file** fare clic su **Sfoglia** per aprire Esplora risorse e individuare i file e le cartelle desiderati.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-182">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Crittografia](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="0fd2d-184">In Esplora risorse copiare i file e/o le cartelle dal volume di ripristino e incollarli nella posizione del *computer di destinazione*.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-184">In Windows Explorer, copy the files and/or folders from the recovery volume and paste them to your *Target machine* location.</span></span> <span data-ttu-id="0fd2d-185">È possibile aprire o trasmettere i file direttamente dal volume di ripristino e verificare che vengano ripristinate le versioni corrette.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-185">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Crittografia](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="0fd2d-187">Dopo aver terminato il ripristino di file e/o cartelle, fare clic su **Smonta** nel riquadro **Cerca e ripristina file**.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-187">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="0fd2d-188">Fare clic su **Sì** per confermare che si desidera smontare il volume.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-188">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Crittografia](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="0fd2d-190">Se non si fa clic su Smonta, il volume di ripristino resterà montato per 6 ore.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-190">If you do not click Unmount, the Recovery Volume will remain mounted for 6 hours from the time when it was mounted.</span></span> <span data-ttu-id="0fd2d-191">Il tempo di montaggio viene tuttavia esteso fino a un massimo di 24 ore in caso di copia dei file in corso.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-191">However, the mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="0fd2d-192">Mentre il volume è montato, non vengono eseguite operazioni di backup.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-192">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="0fd2d-193">Qualsiasi operazione di backup pianificata durante il periodo in cui il volume è montato verrà eseguita dopo lo smontaggio del volume di ripristino.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-193">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >

## <a name="troubleshooting"></a><span data-ttu-id="0fd2d-194">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="0fd2d-194">Troubleshooting</span></span>
<span data-ttu-id="0fd2d-195">Se il montaggio del volume di ripristino non è stato completato da Backup di Azure diversi minuti dopo il clic su **Monta** o ha esito negativo con uno o più errori, seguire questa procedura per avviare normalmente il ripristino.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-195">If Azure Backup does not successfully mount the recovery volume even after several minutes of clicking **Mount** or fails to mount the recovery volume with one or more errors, follow the steps below to begin recovering normally.</span></span>

1.  <span data-ttu-id="0fd2d-196">Annullare il processo di montaggio in corso se è in esecuzione da diversi minuti.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-196">Cancel the ongoing mount process in case it has been running for several minutes.</span></span>

2.  <span data-ttu-id="0fd2d-197">Verificare di usare l'ultima versione dell'agente di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-197">Ensure that you are on the latest version of the Azure Backup agent.</span></span> <span data-ttu-id="0fd2d-198">Per trovare le informazioni relative alla versione dell'agente di Backup di Azure, fare clic su **Informazioni su Agente di Servizi di ripristino di Microsoft Azure** nel riquadro **Azioni** della console di Backup di Microsoft Azure e verificare che il numero in **Versione** sia uguale o superiore alla versione indicata in [questo articolo](https://go.microsoft.com/fwlink/?linkid=229525).</span><span class="sxs-lookup"><span data-stu-id="0fd2d-198">To find out the version information of Azure Backup agent, click on **About Microsoft Azure Recovery Services Agent** on the **Actions** pane of Microsoft Azure Backup console and ensure that the **Version** number is equal to or higher than the version mentioned in [this article](https://go.microsoft.com/fwlink/?linkid=229525).</span></span> <span data-ttu-id="0fd2d-199">È possibile scaricare l'ultima versione da [qui](https://go.microsoft.com/fwLink/?LinkID=288905).</span><span class="sxs-lookup"><span data-stu-id="0fd2d-199">You can download the latest version from [here](https://go.microsoft.com/fwLink/?LinkID=288905)</span></span>

3.  <span data-ttu-id="0fd2d-200">Passare a **Gestione dispositivi** -> **Controller di archiviazione** e verificare di poter individuare **Iniziatore iSCSI Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-200">Go to **Device Manager** -> **Storage Controllers** and ensure that you can locate **Microsoft iSCSI Initiator**.</span></span> <span data-ttu-id="0fd2d-201">Se si riesce a individuarlo, andare direttamente al passaggio 7 seguente.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-201">If you can locate it, directly go to step 7 below.</span></span> 

4.  <span data-ttu-id="0fd2d-202">Se non si riesce a individuare il servizio iniziatore iSCSI Microsoft come illustrato nel passaggio 3, verificare se in **Gestione dispositivi** -> **Controller di archiviazione** è presente una voce **Dispositivo sconosciuto** con ID hardware **ROOT\ISCSIPRT**.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-202">If you cannot locate Microsoft iSCSI Initiator service as mentioned in step 3, check to see if you can find an entry under **Device Manager** -> **Storage Controllers** called **Unknown Device** with Hardware ID **ROOT\ISCSIPRT**.</span></span>

5.  <span data-ttu-id="0fd2d-203">Fare clic con il pulsante destro del mouse su **Dispositivo sconosciuto** e scegliere **Aggiornamento software driver**.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-203">Right click on **Unknown Device** and select **Update Driver Software**.</span></span>

6.  <span data-ttu-id="0fd2d-204">Aggiornare il driver selezionando l'opzione **Cerca automaticamente un driver aggiornato**.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-204">Update the driver by selecting the option to  **Search automatically for updated driver software**.</span></span> <span data-ttu-id="0fd2d-205">Al termine dell'aggiornamento, **Dispositivo sconosciuto** verrà modificato in **Iniziatore iSCSI Microsoft**, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-205">Completion of the update should change **Unknown Device** to **Microsoft iSCSI Initiator** as shown below.</span></span> 

    ![Crittografia](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  <span data-ttu-id="0fd2d-207">Passare a **Gestione attività** -> **Servizi (computer locale)** -> **Servizio iniziatore iSCSI Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-207">Go to **Task Manager** -> **Services (Local)** -> **Microsoft iSCSI Initiator Service**.</span></span> 

    ![Crittografia](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  <span data-ttu-id="0fd2d-209">Riavviare il servizio iniziatore iSCSI Microsoft. A tale scopo, fare clic con il pulsante destro del mouse sul servizio e scegliere **Arresta**, quindi fare di nuovo clic con il pulsante destro del mouse e scegliere **Avvia**.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-209">Restart the Microsoft iSCSI Initiator service by right-clicking on the service, clicking on **Stop** and further right clicking again and clicking on **Start**.</span></span>

9.  <span data-ttu-id="0fd2d-210">Riprovare il ripristino istantaneo.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-210">Retry recovering using Instant Restore.</span></span> 

<span data-ttu-id="0fd2d-211">Se il ripristino ha ancora esito negativo, riavviare il server o il client.</span><span class="sxs-lookup"><span data-stu-id="0fd2d-211">If the recovery still fails, reboot your server/client.</span></span> <span data-ttu-id="0fd2d-212">Se un riavvio non è auspicabile o il ripristino non riesce anche dopo il riavvio del server, provare a eseguire il ripristino da un altro computer e contattare il supporto di Azure inviando una richiesta di supporto dal [portale di Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="0fd2d-212">If a reboot is not desirable or the recovery still fails even after rebooting the server, try recovering from an Alternate Machine, and contact Azure Support by going to [Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and submitting a support request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fd2d-213">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0fd2d-213">Next steps</span></span>
* <span data-ttu-id="0fd2d-214">Dopo aver ripristinato i file e le cartelle, è possibile [gestire i backup](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="0fd2d-214">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
