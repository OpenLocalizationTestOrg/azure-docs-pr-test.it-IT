---
title: Ripristinare i dati in Windows Server o in un client di Windows da Azure con il modello di distribuzione classica | Documentazione Microsoft
description: Informazioni su come eseguire operazioni di ripristino da un computer che esegue Windows Server o un client Windows.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 85585dfc-c764-4e8c-8f0e-40b969640ac2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 300b2b17b44e21ed446fd63d572a2461e2fc1343
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="restore-files-to-a-windows-server-or-windows-client-machine-using-the-classic-deployment-model"></a><span data-ttu-id="8e167-103">Ripristinare file in un computer di Windows Server o in un client di Windows con il modello di distribuzione classica</span><span class="sxs-lookup"><span data-stu-id="8e167-103">Restore files to a Windows server or Windows client machine using the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8e167-104">Portale classico</span><span class="sxs-lookup"><span data-stu-id="8e167-104">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
> * [<span data-ttu-id="8e167-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8e167-105">Azure portal</span></span>](backup-azure-restore-windows-server.md)
>
>

<span data-ttu-id="8e167-106">Questo articolo spiega come recuperare i dati da un insieme di credenziali di backup e ripristinarli in un server o in un computer.</span><span class="sxs-lookup"><span data-stu-id="8e167-106">This article explains how to recover data from a backup vault and restore it to a server or computer.</span></span> <span data-ttu-id="8e167-107">A partire da marzo 2017 non è più possibile creare insiemi di credenziali di backup nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="8e167-107">Starting in March 2017, you can no longer create backup vaults in the classic portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e167-108">È ora possibile aggiornare gli insiemi di credenziali di Backup ad insiemi di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="8e167-108">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="8e167-109">Per altre informazioni, vedere l'articolo [Aggiornare un insieme di credenziali di Backup a un insieme di credenziali di Servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="8e167-109">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="8e167-110">Microsoft consiglia di aggiornare gli insiemi di credenziali di Backup a insiemi di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="8e167-110">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="8e167-111">Dopo il **15 ottobre 2017** non sarà più possibile usare PowerShell per creare insiemi di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="8e167-111">**October 15, 2017**, you will no longer be able to use PowerShell to create Backup vaults.</span></span> <br/> <span data-ttu-id="8e167-112">**A partire dal 1° novembre 2017**:</span><span class="sxs-lookup"><span data-stu-id="8e167-112">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="8e167-113">Eventuali insiemi di credenziali di Backup rimanenti verranno automaticamente aggiornati a insiemi di credenziali di servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="8e167-113">Any remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="8e167-114">e non sarà più possibile accedere ai dati di backup nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="8e167-114">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="8e167-115">Sarà possibile invece usare il portale di Azure per accedere ai dati di backup negli insiemi di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="8e167-115">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

<span data-ttu-id="8e167-116">Per ripristinare i dati, usare la procedura di ripristino guidato dei dati nell'agente di Servizi di ripristino di Microsoft Azure (MARS).</span><span class="sxs-lookup"><span data-stu-id="8e167-116">To restore data, you use the Recover Data wizard in the Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="8e167-117">Quando si ripristinano dati, è possibile:</span><span class="sxs-lookup"><span data-stu-id="8e167-117">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="8e167-118">Ripristinare i dati nello stesso computer in cui sono stati eseguiti i backup.</span><span class="sxs-lookup"><span data-stu-id="8e167-118">Restore data to the same machine from which the backups were taken.</span></span>
* <span data-ttu-id="8e167-119">Ripristinare i dati in un'altra macchina.</span><span class="sxs-lookup"><span data-stu-id="8e167-119">Restore data to an alternate machine.</span></span>

<span data-ttu-id="8e167-120">A gennaio 2017 Microsoft ha rilasciato un aggiornamento in anteprima all'agente MARS.</span><span class="sxs-lookup"><span data-stu-id="8e167-120">In January 2017, Microsoft released a Preview update to the MARS agent.</span></span> <span data-ttu-id="8e167-121">Insieme alle correzioni di bug, questo aggiornamento abilita la funzione di ripristino istantaneo, che consente di montare uno snapshot del punto di ripristino scrivibile come volume di ripristino.</span><span class="sxs-lookup"><span data-stu-id="8e167-121">Along with bug fixes, this update enables Instant Restore, which allows you to mount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="8e167-122">È quindi possibile esplorare il volume di ripristino e i file di copia in un computer locale, ripristinando quindi i file in modo selettivo.</span><span class="sxs-lookup"><span data-stu-id="8e167-122">You can then explore the recovery volume and copy files to a local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="8e167-123">Se si vuole usare questa funzione per ripristinare i dati, è necessario l'[aggiornamento di Backup di Azure di gennaio 2017](https://support.microsoft.com/en-us/help/3216528?preview).</span><span class="sxs-lookup"><span data-stu-id="8e167-123">The [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want to use Instant Restore to restore data.</span></span> <span data-ttu-id="8e167-124">È necessario anche che i dati di backup siano protetti in insiemi di credenziali nelle impostazioni locali elencate nell'articolo del supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="8e167-124">Also the backup data must be protected in vaults in locales listed in the support article.</span></span> <span data-ttu-id="8e167-125">Consultare l'[aggiornamento di Azure Backup di gennaio 2017](https://support.microsoft.com/en-us/help/3216528?preview) per un elenco aggiornato delle impostazioni locali che supportano la funzione di ripristino istantaneo.</span><span class="sxs-lookup"><span data-stu-id="8e167-125">Consult the [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for the latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="8e167-126">Il ripristino istantaneo **non** è attualmente disponibile in tutte le impostazioni locali.</span><span class="sxs-lookup"><span data-stu-id="8e167-126">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="8e167-127">È disponibile per l'uso negli insiemi di credenziali di Servizi di ripristino nel portale di Azure e negli insiemi di credenziali di Backup nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="8e167-127">Instant Restore is available for use in Recovery Services vaults in the Azure portal and Backup vaults in the classic portal.</span></span> <span data-ttu-id="8e167-128">Se si vuole usare la funzione di ripristino istantaneo, scaricare l'aggiornamento di MARS e seguire le procedure relative al ripristino istantaneo.</span><span class="sxs-lookup"><span data-stu-id="8e167-128">If you want to use Instant Restore, download the MARS update, and follow the procedures that mention Instant Restore.</span></span>


## <a name="use-instant-restore-to-recover-data-to-the-same-machine"></a><span data-ttu-id="8e167-129">Usare la funzione di ripristino istantaneo per ripristinare i dati sullo stesso computer</span><span class="sxs-lookup"><span data-stu-id="8e167-129">Use Instant Restore to recover data to the same machine</span></span>

<span data-ttu-id="8e167-130">Se un file è stato eliminato accidentalmente e lo si vuole ripristinare nello stesso computer in cui è stato eseguito il backup, la seguente procedura permette di recuperarlo.</span><span class="sxs-lookup"><span data-stu-id="8e167-130">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span></span>

1. <span data-ttu-id="8e167-131">Aprire lo snap-in di **Backup di Microsoft Azure** .</span><span class="sxs-lookup"><span data-stu-id="8e167-131">Open the **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="8e167-132">Se non si sa dove è stato installato lo snap-in, cercare **Backup di Microsoft Azure** nel computer o nel server.</span><span class="sxs-lookup"><span data-stu-id="8e167-132">If you don't know where the snap in was installed, search the computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="8e167-133">L'applicazione desktop dovrebbe essere visualizzata nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="8e167-133">The desktop app should appear in the search results.</span></span>

2. <span data-ttu-id="8e167-134">Fare clic su **Ripristina dati** per avviare la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="8e167-134">Click **Recover Data** to start the wizard.</span></span>

    ![Ripristina dati](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="8e167-136">Nel riquadro **Guida introduttiva** selezionare l'opzione **This server (Questo server) (`<server name>`)** e fare clic su **Avanti** per ripristinare i dati nello stesso server o computer.</span><span class="sxs-lookup"><span data-stu-id="8e167-136">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Scegliere l'opzione This server (Questo server) per ripristinare i dati nello stesso computer](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="8e167-138">Nel riquadro **Seleziona modalità di ripristino** selezionare **Singoli file e cartelle** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8e167-138">On the **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Ricerca dei file](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="8e167-140">Nel riquadro **Seleziona volume e data** selezionare il volume che contiene i file e/o le cartelle da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="8e167-140">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="8e167-141">Nel calendario selezionare un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="8e167-141">On the calendar, select a recovery point.</span></span> <span data-ttu-id="8e167-142">È possibile ripristinare da qualsiasi punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="8e167-142">You can restore from any recovery point in time.</span></span> <span data-ttu-id="8e167-143">Le date in **grassetto** indicano la disponibilità di almeno un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="8e167-143">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="8e167-144">Dopo aver selezionato una data, se sono disponibili più punti di ripristino, scegliere quello appropriato dall'elenco a discesa **Ora**.</span><span class="sxs-lookup"><span data-stu-id="8e167-144">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Volume e dati](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="8e167-146">Dopo aver selezionato il punto di ripristino, fare clic su **Monta**.</span><span class="sxs-lookup"><span data-stu-id="8e167-146">Once you have chosen the recovery point to restore, click **Mount**.</span></span>

    <span data-ttu-id="8e167-147">Backup di Azure monta il punto di ripristino locale e lo usa come volume di ripristino.</span><span class="sxs-lookup"><span data-stu-id="8e167-147">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="8e167-148">Nel riquadro **Cerca e ripristina file** fare clic su **Sfoglia** per aprire Esplora risorse e individuare i file e le cartelle desiderati.</span><span class="sxs-lookup"><span data-stu-id="8e167-148">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Opzioni di ripristino](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="8e167-150">In Esplora risorse copiare i file e/o le cartelle che si desidera ripristinare e incollarle in qualsiasi posizione locale nel server o nel computer.</span><span class="sxs-lookup"><span data-stu-id="8e167-150">In Windows Explorer, copy the files and/or folders you want to restore and paste them to any location local to the server or computer.</span></span> <span data-ttu-id="8e167-151">È possibile aprire o trasmettere i file direttamente dal volume di ripristino e verificare che vengano ripristinate le versioni corrette.</span><span class="sxs-lookup"><span data-stu-id="8e167-151">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Copiare e incollare file e cartelle dal volume montato alla posizione locale](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="8e167-153">Dopo aver terminato il ripristino di file e/o cartelle, fare clic su **Smonta** nel riquadro **Cerca e ripristina file**.</span><span class="sxs-lookup"><span data-stu-id="8e167-153">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="8e167-154">Fare clic su **Sì** per confermare che si desidera smontare il volume.</span><span class="sxs-lookup"><span data-stu-id="8e167-154">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Smontare il volume e confermare](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="8e167-156">Se non si fa clic su Smonta, il volume di ripristino resterà montato per sei ore.</span><span class="sxs-lookup"><span data-stu-id="8e167-156">If you do not click Unmount, the Recovery Volume will remain mounted for six hours from the time when it was mounted.</span></span> <span data-ttu-id="8e167-157">Mentre il volume è montato, non vengono eseguite operazioni di backup.</span><span class="sxs-lookup"><span data-stu-id="8e167-157">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="8e167-158">Qualsiasi operazione di backup pianificata durante il periodo in cui il volume è montato verrà eseguita dopo lo smontaggio del volume di ripristino.</span><span class="sxs-lookup"><span data-stu-id="8e167-158">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >


## <a name="recover-data-to-the-same-machine"></a><span data-ttu-id="8e167-159">Recuperare i dati nello stesso computer</span><span class="sxs-lookup"><span data-stu-id="8e167-159">Recover data to the same machine</span></span>
<span data-ttu-id="8e167-160">Se un file è stato eliminato accidentalmente e lo si vuole ripristinare nello stesso computer in cui è stato eseguito il backup, la seguente procedura permette di recuperarlo.</span><span class="sxs-lookup"><span data-stu-id="8e167-160">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span></span>

1. <span data-ttu-id="8e167-161">Aprire lo snap-in di **Backup di Microsoft Azure** .</span><span class="sxs-lookup"><span data-stu-id="8e167-161">Open the **Microsoft Azure Backup** snap in.</span></span>
2. <span data-ttu-id="8e167-162">Fare clic su **Ripristina dati** per avviare il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8e167-162">Click **Recover Data** to initiate the workflow.</span></span>

    ![Ripristina dati](./media/backup-azure-restore-windows-server-classic/recover.png)
3. <span data-ttu-id="8e167-164">Selezionare l'opzione **Questo server (*nomecomputer*)** per ripristinare il file di backup nello stesso computer.</span><span class="sxs-lookup"><span data-stu-id="8e167-164">Select the **This server (*yourmachinename*)** option to restore the backed up file on the same machine.</span></span>

    ![Nello stesso computer](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. <span data-ttu-id="8e167-166">È possibile scegliere **Sfoglia elenco file** o **Cerca file**.</span><span class="sxs-lookup"><span data-stu-id="8e167-166">Choose to **Browse for files** or **Search for files**.</span></span>

    <span data-ttu-id="8e167-167">Se si intende ripristinare uno o più file con un percorso noto, lasciare l'opzione predefinita.</span><span class="sxs-lookup"><span data-stu-id="8e167-167">Leave the default option if you plan to restore one or more files whose path is known.</span></span> <span data-ttu-id="8e167-168">Se non si è certi della struttura di cartelle, ma si vuole cercare un file, selezionare l'opzione **Cerca file** .</span><span class="sxs-lookup"><span data-stu-id="8e167-168">If you are not sure about the folder structure but would like to search for a file, pick the **Search for files** option.</span></span> <span data-ttu-id="8e167-169">Ai fini di questa sezione, si procede con l'opzione predefinita.</span><span class="sxs-lookup"><span data-stu-id="8e167-169">For the purpose of this section, we will proceed with the default option.</span></span>

    ![Ricerca dei file](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. <span data-ttu-id="8e167-171">Nella schermata successiva selezionare il volume da cui si vuole ripristinare il file.</span><span class="sxs-lookup"><span data-stu-id="8e167-171">Select the volume from which you wish to restore the file.</span></span>

    <span data-ttu-id="8e167-172">È possibile ripristinare da qualsiasi data.</span><span class="sxs-lookup"><span data-stu-id="8e167-172">You can restore from any point in time.</span></span> <span data-ttu-id="8e167-173">Le date visualizzate in **grassetto** nel controllo calendario indicano la disponibilità di un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="8e167-173">Dates which appear in **bold** in the calendar control indicate the availability of a restore point.</span></span> <span data-ttu-id="8e167-174">Dopo aver selezionato una data, in base alla pianificazione del backup (e alla riuscita di un'operazione di backup), è possibile selezionare un orario dall'elenco a discesa **Ora** .</span><span class="sxs-lookup"><span data-stu-id="8e167-174">Once a date is selected, based on your backup schedule (and the success of a backup operation), you can select a point in time from the **Time** drop down.</span></span>

    ![Volume e dati](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. <span data-ttu-id="8e167-176">Selezionare gli elementi da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="8e167-176">Select the items to recover.</span></span> <span data-ttu-id="8e167-177">È possibile selezionare più cartelle e file per il ripristino.</span><span class="sxs-lookup"><span data-stu-id="8e167-177">You can multi-select folders/files you wish to restore.</span></span>

    ![Selezione dei file](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. <span data-ttu-id="8e167-179">Specificare i parametri di ripristino.</span><span class="sxs-lookup"><span data-stu-id="8e167-179">Specify the recovery parameters.</span></span>

    ![Opzioni di ripristino](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * <span data-ttu-id="8e167-181">È possibile scegliere di ripristinare i file nel percorso originale (in cui il file o la cartella verrà sovrascritta) o in un altro percorso nello stesso computer.</span><span class="sxs-lookup"><span data-stu-id="8e167-181">You have an option of restoring to the original location (in which the file/folder would be overwritten) or to another location in the same machine.</span></span>
   * <span data-ttu-id="8e167-182">Se il file o la cartella da ripristinare esiste nel percorso di destinazione, è possibile creare copie (due versioni dello stesso file), sovrascrivere i file nel percorso di destinazione oppure ignorare il ripristino dei file esistenti nel database di destinazione.</span><span class="sxs-lookup"><span data-stu-id="8e167-182">If the file/folder you wish to restore exists in the target location, you can create copies (two versions of the same file), overwrite the files in the target location, or skip the recovery of the files which exist in the target.</span></span>
   * <span data-ttu-id="8e167-183">È consigliabile lasciare l'opzione predefinita che prevede il ripristino degli elenchi di controllo di accesso sui file che vengono recuperati.</span><span class="sxs-lookup"><span data-stu-id="8e167-183">It is highly recommended that you leave the default option of restoring the ACLs on the files which are being recovered.</span></span>
8. <span data-ttu-id="8e167-184">Una volta forniti i dati di input, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8e167-184">Once these inputs are provided, click **Next**.</span></span> <span data-ttu-id="8e167-185">Il flusso di lavoro di ripristino, che consente di ripristinare i file in questo computer, verrà avviato.</span><span class="sxs-lookup"><span data-stu-id="8e167-185">The recovery workflow, which restores the files to this machine, will begin.</span></span>

## <a name="recover-to-an-alternate-machine"></a><span data-ttu-id="8e167-186">Recuperare i dati in un altro computer</span><span class="sxs-lookup"><span data-stu-id="8e167-186">Recover to an alternate machine</span></span>
<span data-ttu-id="8e167-187">Se l'intero server viene perso, è comunque possibile recuperare dati da Backup di Azure in un computer diverso.</span><span class="sxs-lookup"><span data-stu-id="8e167-187">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span></span> <span data-ttu-id="8e167-188">I passaggi seguenti illustrano il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8e167-188">The following steps illustrate the workflow.</span></span>  

<span data-ttu-id="8e167-189">Include la terminologia utilizzata in questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="8e167-189">The terminology used in these steps includes:</span></span>

* <span data-ttu-id="8e167-190">*Computer di origine* : il computer di origine da cui è stato eseguito il backup e che non è attualmente disponibile.</span><span class="sxs-lookup"><span data-stu-id="8e167-190">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="8e167-191">*Computer di destinazione* : il computer in cui i dati vengono ripristinati.</span><span class="sxs-lookup"><span data-stu-id="8e167-191">*Target machine* – The machine to which the data is being recovered.</span></span>
* <span data-ttu-id="8e167-192">*Insieme di credenziali di esempio*: insieme di credenziali di backup in cui *computer di origine* e *computer di destinazione* sono registrati.</span><span class="sxs-lookup"><span data-stu-id="8e167-192">*Sample vault* – The Backup vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="8e167-193">I backup eseguiti da un determinato computer non possono essere ripristinati in un computer che esegue una versione precedente del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="8e167-193">Backups taken from a machine cannot be restored on a machine which is running an earlier version of the operating system.</span></span> <span data-ttu-id="8e167-194">Ad esempio, se i backup vengono eseguiti da un computer che esegue Windows 7, è possibile ripristinare i dati in un computer con Windows 8 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="8e167-194">For example, if backups are taken from a Windows 7 machine, it can be restored on a Windows 8 or above machine.</span></span> <span data-ttu-id="8e167-195">Tuttavia non è possibile eseguire l'operazione inversa.</span><span class="sxs-lookup"><span data-stu-id="8e167-195">However, the vice-versa does not hold true.</span></span>
>
>

1. <span data-ttu-id="8e167-196">Aprire lo snap-in di **Backup di Microsoft Azure** nel *Computer di destinazione*.</span><span class="sxs-lookup"><span data-stu-id="8e167-196">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span></span>
2. <span data-ttu-id="8e167-197">Verificare che il *computer di destinazione* e il *computer di origine* siano registrati nello stesso insieme di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="8e167-197">Ensure that the *Target machine* and the *Source machine* are registered to the same backup vault.</span></span>
3. <span data-ttu-id="8e167-198">Fare clic su **Ripristina dati** per avviare il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8e167-198">Click **Recover Data** to initiate the workflow.</span></span>

    ![Ripristina dati](./media/backup-azure-restore-windows-server-classic/recover.png)
4. <span data-ttu-id="8e167-200">Selezionare **Un altro server**</span><span class="sxs-lookup"><span data-stu-id="8e167-200">Select **Another server**</span></span>

    ![Un altro server](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. <span data-ttu-id="8e167-202">Specificare il file dell'insieme di credenziali che corrisponde all' *Insieme di credenziali di esempio*.</span><span class="sxs-lookup"><span data-stu-id="8e167-202">Provide the vault credential file that corresponds to the *Sample vault*.</span></span> <span data-ttu-id="8e167-203">Se il file dell'insieme di credenziali non è valido (o è scaduto), scaricarne uno nuovo dall' *Insieme di credenziali di esempio* nel portale classico di Azure.</span><span class="sxs-lookup"><span data-stu-id="8e167-203">If the vault credential file is invalid (or expired) download a new vault credential file from the *Sample vault* in the Azure classic portal.</span></span> <span data-ttu-id="8e167-204">Dopo aver specificato il file delle credenziali dell'insieme di credenziali, in quest'ultimo viene visualizzato l'insieme di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="8e167-204">Once the vault credential file is provided, the backup vault against the vault credential file is displayed.</span></span>
6. <span data-ttu-id="8e167-205">Selezionare il *computer di origine* dall'elenco dei computer visualizzati.</span><span class="sxs-lookup"><span data-stu-id="8e167-205">Select the *Source machine* from the list of displayed machines.</span></span>

    ![Elenco di computer](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. <span data-ttu-id="8e167-207">Selezionare l'opzione **Cerca file** o **Sfoglia elenco file**.</span><span class="sxs-lookup"><span data-stu-id="8e167-207">Select either the **Search for files** or **Browse for files** option.</span></span> <span data-ttu-id="8e167-208">Ai fini di questa sezione, si userà l'opzione **Cerca file** .</span><span class="sxs-lookup"><span data-stu-id="8e167-208">For the purpose of this section, we will use the **Search for files** option.</span></span>

    ![Search](./media/backup-azure-restore-windows-server-classic/search.png)
8. <span data-ttu-id="8e167-210">Nella schermata successiva selezionare la data e il volume.</span><span class="sxs-lookup"><span data-stu-id="8e167-210">Select the volume and date in the next screen.</span></span> <span data-ttu-id="8e167-211">Cercare il nome delle cartelle e dei file da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="8e167-211">Search for the folder/file name you want to restore.</span></span>

    ![Ricerca di elementi](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. <span data-ttu-id="8e167-213">Selezionare il percorso in cui devono essere ripristinati i file.</span><span class="sxs-lookup"><span data-stu-id="8e167-213">Select the location where the files need to be restored.</span></span>

    ![Percorso di ripristino](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. <span data-ttu-id="8e167-215">Specificare la passphrase di crittografia indicata durante la registrazione del *computer di origine* all'*insieme di credenziali di esempio*.</span><span class="sxs-lookup"><span data-stu-id="8e167-215">Provide the encryption passphrase that was provided during *Source machine’s* registration to *Sample vault*.</span></span>

    ![Crittografia](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. <span data-ttu-id="8e167-217">Dopo aver specificato i dati di input, fare clic sul pulsante **Ripristina**che attiva le operazioni di ripristino dei file di backup nella destinazione specificata.</span><span class="sxs-lookup"><span data-stu-id="8e167-217">Once the input is provided, click **Recover**, which triggers the restore of the backed up files to the destination provided.</span></span>

## <a name="use-instant-restore-to-restore-data-to-an-alternate-machine"></a><span data-ttu-id="8e167-218">Usare il ripristino immediato per ripristinare i dati in un altro computer</span><span class="sxs-lookup"><span data-stu-id="8e167-218">Use Instant Restore to restore data to an alternate machine</span></span>
<span data-ttu-id="8e167-219">Se l'intero server viene perso, è comunque possibile recuperare dati da Backup di Azure in un computer diverso.</span><span class="sxs-lookup"><span data-stu-id="8e167-219">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span></span> <span data-ttu-id="8e167-220">I passaggi seguenti illustrano il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8e167-220">The following steps illustrate the workflow.</span></span>

<span data-ttu-id="8e167-221">Include la terminologia utilizzata in questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="8e167-221">The terminology used in these steps includes:</span></span>

* <span data-ttu-id="8e167-222">*Computer di origine* : il computer di origine da cui è stato eseguito il backup e che non è attualmente disponibile.</span><span class="sxs-lookup"><span data-stu-id="8e167-222">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="8e167-223">*Computer di destinazione* : il computer in cui i dati vengono ripristinati.</span><span class="sxs-lookup"><span data-stu-id="8e167-223">*Target machine* – The machine to which the data is being recovered.</span></span>
* <span data-ttu-id="8e167-224">*Insieme di credenziali di esempio*: l'insieme di credenziali dei servizi di ripristino in cui il *computer di origine* e il *computer di destinazione* sono registrati.</span><span class="sxs-lookup"><span data-stu-id="8e167-224">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="8e167-225">Non è possibile ripristinare i backup in un computer di destinazione che esegue una versione precedente del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="8e167-225">Backups can't be restored to a target machine running an earlier version of the operating system.</span></span> <span data-ttu-id="8e167-226">Ad esempio, un backup eseguito su un computer con Windows 7 può essere ripristinato in un computer con Windows 8 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="8e167-226">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="8e167-227">Un backup eseguito su un computer con Windows 8 non può essere ripristinato in un computer con Windows 7.</span><span class="sxs-lookup"><span data-stu-id="8e167-227">A backup taken from a Windows 8 computer cannot be restored to a Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="8e167-228">Aprire lo snap-in di **Backup di Microsoft Azure** nel *Computer di destinazione*.</span><span class="sxs-lookup"><span data-stu-id="8e167-228">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span></span>

2. <span data-ttu-id="8e167-229">Assicurarsi che il *computer di destinazione* e il *computer di origine* siano registrati nello stesso insieme di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="8e167-229">Ensure the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span></span>

3. <span data-ttu-id="8e167-230">Fare clic su **Ripristina dati** per aprire il **ripristino guidato dei dati**.</span><span class="sxs-lookup"><span data-stu-id="8e167-230">Click **Recover Data** to open the **Recover Data wizard**.</span></span>

    ![Ripristina dati](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="8e167-232">Nel riquadro **Guida introduttiva** selezionare **Another server** (Un altro server)</span><span class="sxs-lookup"><span data-stu-id="8e167-232">On the **Getting Started** pane, select **Another server**</span></span>

    ![Un altro server](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="8e167-234">Specificare il file dell'insieme di credenziali che corrisponde all'*insieme di credenziali di esempio*, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8e167-234">Provide the vault credential file that corresponds to the *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="8e167-235">Se il file dell'insieme di credenziali non è valido (o è scaduto), è necessario scaricarne uno nuovo dall'*insieme di credenziali di esempio* nel Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8e167-235">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span></span> <span data-ttu-id="8e167-236">Dopo aver specificato un insieme di credenziali valido, viene visualizzato il nome dell'insieme di credenziali di backup corrispondente.</span><span class="sxs-lookup"><span data-stu-id="8e167-236">Once you provide a valid vault credential, the name of the corresponding Backup Vault appears.</span></span>

6. <span data-ttu-id="8e167-237">Nel riquadro **Seleziona server di backup** selezionare il *computer di origine* dall'elenco dei computer visualizzati e specificare la passphrase.</span><span class="sxs-lookup"><span data-stu-id="8e167-237">On the **Select Backup Server** pane, select the *Source machine* from the list of displayed machines and provide the passphrase.</span></span> <span data-ttu-id="8e167-238">Quindi fare clic su **Next**.</span><span class="sxs-lookup"><span data-stu-id="8e167-238">Then click **Next**.</span></span>

    ![Elenco di computer](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="8e167-240">Nel riquadro **Seleziona modalità di ripristino** selezionare **Singoli file e cartelle** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8e167-240">On the **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Search](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="8e167-242">Nel riquadro **Seleziona volume e data** selezionare il volume che contiene i file e/o le cartelle da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="8e167-242">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="8e167-243">Nel calendario selezionare un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="8e167-243">On the calendar, select a recovery point.</span></span> <span data-ttu-id="8e167-244">È possibile ripristinare da qualsiasi punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="8e167-244">You can restore from any recovery point in time.</span></span> <span data-ttu-id="8e167-245">Le date in **grassetto** indicano la disponibilità di almeno un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="8e167-245">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="8e167-246">Dopo aver selezionato una data, se sono disponibili più punti di ripristino, scegliere quello appropriato dall'elenco a discesa **Ora**.</span><span class="sxs-lookup"><span data-stu-id="8e167-246">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Ricerca di elementi](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="8e167-248">Fare clic su **Monta** per montare localmente il punto di ripristino come volume di ripristino sul *computer di destinazione*.</span><span class="sxs-lookup"><span data-stu-id="8e167-248">Click **Mount** to locally mount the recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="8e167-249">Nel riquadro **Cerca e ripristina file** fare clic su **Sfoglia** per aprire Esplora risorse e individuare i file e le cartelle desiderati.</span><span class="sxs-lookup"><span data-stu-id="8e167-249">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Crittografia](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="8e167-251">In Esplora risorse copiare i file e/o le cartelle dal volume di ripristino e incollarli nella posizione del *computer di destinazione*.</span><span class="sxs-lookup"><span data-stu-id="8e167-251">In Windows Explorer, copy the files and/or folders from the recovery volume and paste them to your *Target machine* location.</span></span> <span data-ttu-id="8e167-252">È possibile aprire o trasmettere i file direttamente dal volume di ripristino e verificare che vengano ripristinate le versioni corrette.</span><span class="sxs-lookup"><span data-stu-id="8e167-252">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Crittografia](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="8e167-254">Dopo aver terminato il ripristino di file e/o cartelle, fare clic su **Smonta** nel riquadro **Cerca e ripristina file**.</span><span class="sxs-lookup"><span data-stu-id="8e167-254">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="8e167-255">Fare clic su **Sì** per confermare che si desidera smontare il volume.</span><span class="sxs-lookup"><span data-stu-id="8e167-255">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Crittografia](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="8e167-257">Se non si fa clic su Smonta, il volume di ripristino resterà montato per sei ore.</span><span class="sxs-lookup"><span data-stu-id="8e167-257">If you do not click Unmount, the Recovery Volume will remain mounted for six hours from the time when it was mounted.</span></span> <span data-ttu-id="8e167-258">Mentre il volume è montato, non vengono eseguite operazioni di backup.</span><span class="sxs-lookup"><span data-stu-id="8e167-258">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="8e167-259">Qualsiasi operazione di backup pianificata durante il periodo in cui il volume è montato verrà eseguita dopo lo smontaggio del volume di ripristino.</span><span class="sxs-lookup"><span data-stu-id="8e167-259">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >


## <a name="next-steps"></a><span data-ttu-id="8e167-260">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8e167-260">Next steps</span></span>
* [<span data-ttu-id="8e167-261">Backup di Azure - Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="8e167-261">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
* <span data-ttu-id="8e167-262">Visitare il [Forum su Backup di Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span><span class="sxs-lookup"><span data-stu-id="8e167-262">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span></span>

## <a name="learn-more"></a><span data-ttu-id="8e167-263">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="8e167-263">Learn more</span></span>
* [<span data-ttu-id="8e167-264">Panoramica di Azure Backup</span><span class="sxs-lookup"><span data-stu-id="8e167-264">Azure Backup Overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [<span data-ttu-id="8e167-265">Eseguire il backup di macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="8e167-265">Backup Azure virtual machines</span></span>](backup-azure-vms-introduction.md)
* [<span data-ttu-id="8e167-266">Eseguire il backup dei carichi di lavoro di Microsoft</span><span class="sxs-lookup"><span data-stu-id="8e167-266">Backup up Microsoft workloads</span></span>](backup-azure-dpm-introduction.md)
