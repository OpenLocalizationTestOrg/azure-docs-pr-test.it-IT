---
title: modello di distribuzione classica di hello aaaRestore tooa di dati di Windows Server o Client Windows dall'utilizzo di Azure | Documenti Microsoft
description: Informazioni su come toorestore da Windows Server o Client Windows.
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
ms.openlocfilehash: 4d1458d5233c4f55004ecfa95cbf7b3b18a03dde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-hello-classic-deployment-model"></a><span data-ttu-id="e9409-103">Ripristinare i file tooa Windows server o computer client Windows utilizzando il modello di distribuzione classica hello</span><span class="sxs-lookup"><span data-stu-id="e9409-103">Restore files tooa Windows server or Windows client machine using hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e9409-104">Portale classico</span><span class="sxs-lookup"><span data-stu-id="e9409-104">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
> * [<span data-ttu-id="e9409-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e9409-105">Azure portal</span></span>](backup-azure-restore-windows-server.md)
>
>

<span data-ttu-id="e9409-106">Questo articolo spiega come toorecover dati da un backup dell'insieme di credenziali e ripristino tooa server o computer.</span><span class="sxs-lookup"><span data-stu-id="e9409-106">This article explains how toorecover data from a backup vault and restore it tooa server or computer.</span></span> <span data-ttu-id="e9409-107">A partire da marzo 2017, è possibile creare non più insiemi di credenziali di backup nel portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="e9409-107">Starting in March 2017, you can no longer create backup vaults in hello classic portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e9409-108">È ora possibile aggiornare i servizi archivi di Backup gli insiemi di credenziali tooRecovery.</span><span class="sxs-lookup"><span data-stu-id="e9409-108">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="e9409-109">Per informazioni dettagliate, vedere l'articolo hello [aggiornare un tooa insieme di credenziali di Backup dell'insieme di credenziali di servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="e9409-109">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="e9409-110">Microsoft incoraggia gli utenti tooupgrade insiemi di credenziali di servizi tooRecovery insiemi di credenziali di Backup.</span><span class="sxs-lookup"><span data-stu-id="e9409-110">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="e9409-111">**15 ottobre 2017**, non potrà più insiemi di credenziali Backup a toocreate toouse in grado di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e9409-111">**October 15, 2017**, you will no longer be able toouse PowerShell toocreate Backup vaults.</span></span> <br/> <span data-ttu-id="e9409-112">**A partire dal 1° novembre 2017**:</span><span class="sxs-lookup"><span data-stu-id="e9409-112">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="e9409-113">Gli insiemi di credenziali di Backup rimanenti verrà automaticamente aggiornato tooRecovery servizi insiemi di credenziali.</span><span class="sxs-lookup"><span data-stu-id="e9409-113">Any remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="e9409-114">Si sarà in grado di tooaccess ai dati di backup nel portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="e9409-114">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="e9409-115">Utilizzare invece hello Azure tooaccess portale i dati di backup in insiemi di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e9409-115">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

<span data-ttu-id="e9409-116">dati toorestore, guidata hello Ripristina dati nell'agente di Microsoft Azure Recovery Services (MARS) hello.</span><span class="sxs-lookup"><span data-stu-id="e9409-116">toorestore data, you use hello Recover Data wizard in hello Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="e9409-117">Quando si ripristinano dati, è possibile:</span><span class="sxs-lookup"><span data-stu-id="e9409-117">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="e9409-118">Ripristino dati toohello stesso computer dai quali backup hello sono stati eseguiti.</span><span class="sxs-lookup"><span data-stu-id="e9409-118">Restore data toohello same machine from which hello backups were taken.</span></span>
* <span data-ttu-id="e9409-119">Ripristinare dati tooan alternativo macchina.</span><span class="sxs-lookup"><span data-stu-id="e9409-119">Restore data tooan alternate machine.</span></span>

<span data-ttu-id="e9409-120">Gennaio January 2017, Microsoft ha rilasciato un agente di anteprima aggiornamento toohello MARS.</span><span class="sxs-lookup"><span data-stu-id="e9409-120">In January 2017, Microsoft released a Preview update toohello MARS agent.</span></span> <span data-ttu-id="e9409-121">Insieme a correzioni di bug, questo aggiornamento consente a ripristinare immediata, che consente di toomount uno snapshot del punto di ripristino scrivibile come volume di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e9409-121">Along with bug fixes, this update enables Instant Restore, which allows you toomount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="e9409-122">È quindi possibile esplorare hello ripristino volume e copia i file tooa computer locale in modo selettivo il ripristino dei file.</span><span class="sxs-lookup"><span data-stu-id="e9409-122">You can then explore hello recovery volume and copy files tooa local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="e9409-123">Hello [gennaio January 2017 aggiornamento di Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview) è obbligatorio se si desidera toouse ripristino immediato toorestore dati.</span><span class="sxs-lookup"><span data-stu-id="e9409-123">hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want toouse Instant Restore toorestore data.</span></span> <span data-ttu-id="e9409-124">Dati di backup hello devono inoltre essere protetti in insiemi di credenziali in impostazioni locali elencate nell'articolo di supporto tecnico hello.</span><span class="sxs-lookup"><span data-stu-id="e9409-124">Also hello backup data must be protected in vaults in locales listed in hello support article.</span></span> <span data-ttu-id="e9409-125">Consultare hello [gennaio January 2017 aggiornamento di Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview) per l'elenco più recente di hello delle impostazioni locali che supportano il ripristino immediato.</span><span class="sxs-lookup"><span data-stu-id="e9409-125">Consult hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for hello latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="e9409-126">Il ripristino istantaneo **non** è attualmente disponibile in tutte le impostazioni locali.</span><span class="sxs-lookup"><span data-stu-id="e9409-126">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="e9409-127">Ripristino immediato è disponibile per l'uso di insiemi di credenziali di servizi di ripristino in hello portale di Azure e gli insiemi di credenziali di Backup nel portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="e9409-127">Instant Restore is available for use in Recovery Services vaults in hello Azure portal and Backup vaults in hello classic portal.</span></span> <span data-ttu-id="e9409-128">Se si desidera ripristinare immediata toouse, scaricare l'aggiornamento di MARS hello e seguire le procedure hello che menzionano il ripristino immediato.</span><span class="sxs-lookup"><span data-stu-id="e9409-128">If you want toouse Instant Restore, download hello MARS update, and follow hello procedures that mention Instant Restore.</span></span>


## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a><span data-ttu-id="e9409-129">Utilizzare il ripristino immediato toorecover dati toohello nello stesso computer</span><span class="sxs-lookup"><span data-stu-id="e9409-129">Use Instant Restore toorecover data toohello same machine</span></span>

<span data-ttu-id="e9409-130">Se è stato eliminato accidentalmente un file e preferenze di toorestore è toohello stessa macchina (da cui hello backup viene eseguito), hello seguendo i passaggi consentono di ripristinare i dati di hello.</span><span class="sxs-lookup"><span data-stu-id="e9409-130">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="e9409-131">Aprire hello **Backup di Microsoft Azure** allineamento in.</span><span class="sxs-lookup"><span data-stu-id="e9409-131">Open hello **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="e9409-132">Se non si conosce in cui è stato installato hello snap-in, eseguire la ricerca computer hello o un server per **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="e9409-132">If you don't know where hello snap in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="e9409-133">app desktop Hello dovrebbe essere visualizzato nei risultati della ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="e9409-133">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="e9409-134">Fare clic su **Ripristina dati** guidata hello toostart.</span><span class="sxs-lookup"><span data-stu-id="e9409-134">Click **Recover Data** toostart hello wizard.</span></span>

    ![Ripristina dati](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="e9409-136">In hello **Introduzione** riquadro, toorestore hello dati toohello stesso server o computer, selezionare **server (`<server name>`)** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="e9409-136">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Scegliere questo toohello di dati server opzione toorestore hello nello stesso computer](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="e9409-138">In hello **selezionare la modalità di ripristino** riquadro scegliere **singoli file e cartelle** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="e9409-138">On hello **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Ricerca dei file](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="e9409-140">In hello **seleziona Volume e data** riquadro, volume hello select che contiene i file hello e/o le cartelle da toorestore.</span><span class="sxs-lookup"><span data-stu-id="e9409-140">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="e9409-141">Calendario hello, selezionare un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e9409-141">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="e9409-142">È possibile ripristinare da qualsiasi punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e9409-142">You can restore from any recovery point in time.</span></span> <span data-ttu-id="e9409-143">Le date in **grassetto** indicare hello la disponibilità di almeno un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e9409-143">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="e9409-144">Dopo aver selezionato una data, se sono disponibili più punti di ripristino, scegliere il punto di ripristino specifico di hello da hello **ora** dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="e9409-144">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Volume e dati](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="e9409-146">Dopo aver scelto toorestore punto di ripristino hello, fare clic su **montare**.</span><span class="sxs-lookup"><span data-stu-id="e9409-146">Once you have chosen hello recovery point toorestore, click **Mount**.</span></span>

    <span data-ttu-id="e9409-147">Backup di Azure monta il punto di ripristino locali hello che viene utilizzato come un volume di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e9409-147">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="e9409-148">In hello **Sfoglia e ripristinare i file** riquadro, fare clic su **Sfoglia** tooopen in Esplora risorse e individuare i file hello e le cartelle desiderate.</span><span class="sxs-lookup"><span data-stu-id="e9409-148">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Opzioni di ripristino](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="e9409-150">In Esplora risorse, la copia di file hello e/o le cartelle si toorestore e incollarlo tooany percorso locale toohello server o computer.</span><span class="sxs-lookup"><span data-stu-id="e9409-150">In Windows Explorer, copy hello files and/or folders you want toorestore and paste them tooany location local toohello server or computer.</span></span> <span data-ttu-id="e9409-151">È possibile aprire o flusso di file hello direttamente dal volume di ripristino hello e verificare hello corretto versioni vengono ripristinate.</span><span class="sxs-lookup"><span data-stu-id="e9409-151">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Copiare e incollare i file e cartelle dal percorso toolocal volume montato](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="e9409-153">Al termine il ripristino file hello e/o cartelle, hello **Sfoglia e i file di ripristino** riquadro, fare clic su **Smonta**.</span><span class="sxs-lookup"><span data-stu-id="e9409-153">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="e9409-154">Quindi fare clic su **Sì** tooconfirm che si desidera volume hello toounmount.</span><span class="sxs-lookup"><span data-stu-id="e9409-154">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Smontare il volume di hello e verificare](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="e9409-156">Se non si sceglie Smonta, hello ripristino Volume rimarrà montata per sei ore dall'ora di hello quando è stato montato.</span><span class="sxs-lookup"><span data-stu-id="e9409-156">If you do not click Unmount, hello Recovery Volume will remain mounted for six hours from hello time when it was mounted.</span></span> <span data-ttu-id="e9409-157">Nessuna operazione di backup verranno eseguito mentre hello volume montato.</span><span class="sxs-lookup"><span data-stu-id="e9409-157">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="e9409-158">Toorun qualsiasi operazione di backup pianificato durante la fase di hello quando hello volume montato, verrà eseguito dopo il volume di ripristino hello viene disinstallato.</span><span class="sxs-lookup"><span data-stu-id="e9409-158">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="recover-data-toohello-same-machine"></a><span data-ttu-id="e9409-159">Ripristinare i dati toohello nello stesso computer</span><span class="sxs-lookup"><span data-stu-id="e9409-159">Recover data toohello same machine</span></span>
<span data-ttu-id="e9409-160">Se è stato eliminato accidentalmente un file e preferenze di toorestore è toohello stessa macchina (da cui hello backup viene eseguito), hello seguendo i passaggi consentono di ripristinare i dati di hello.</span><span class="sxs-lookup"><span data-stu-id="e9409-160">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="e9409-161">Aprire hello **Backup di Microsoft Azure** allineamento in.</span><span class="sxs-lookup"><span data-stu-id="e9409-161">Open hello **Microsoft Azure Backup** snap in.</span></span>
2. <span data-ttu-id="e9409-162">Fare clic su **Ripristina dati** flusso di lavoro tooinitiate hello.</span><span class="sxs-lookup"><span data-stu-id="e9409-162">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Ripristina dati](./media/backup-azure-restore-windows-server-classic/recover.png)
3. <span data-ttu-id="e9409-164">Seleziona hello * *server (*yourmachinename*) * * hello toorestore opzione file di backup su hello stesso computer.</span><span class="sxs-lookup"><span data-stu-id="e9409-164">Select hello **This server (*yourmachinename*)** option toorestore hello backed up file on hello same machine.</span></span>

    ![Nello stesso computer](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. <span data-ttu-id="e9409-166">Scegliere troppo**Sfoglia file** o **Cerca file**.</span><span class="sxs-lookup"><span data-stu-id="e9409-166">Choose too**Browse for files** or **Search for files**.</span></span>

    <span data-ttu-id="e9409-167">Lasciare opzione predefinita hello se si prevede di toorestore uno o più file il cui percorso è noto.</span><span class="sxs-lookup"><span data-stu-id="e9409-167">Leave hello default option if you plan toorestore one or more files whose path is known.</span></span> <span data-ttu-id="e9409-168">Se si desidera toosearch per un file dubbi sulla struttura di cartelle hello, selezionare hello **Cerca file** opzione.</span><span class="sxs-lookup"><span data-stu-id="e9409-168">If you are not sure about hello folder structure but would like toosearch for a file, pick hello **Search for files** option.</span></span> <span data-ttu-id="e9409-169">A scopo di hello in questa sezione, si procederà con l'opzione predefinita di hello.</span><span class="sxs-lookup"><span data-stu-id="e9409-169">For hello purpose of this section, we will proceed with hello default option.</span></span>

    ![Ricerca dei file](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. <span data-ttu-id="e9409-171">Selezionare il volume di hello da cui si desidera file hello toorestore.</span><span class="sxs-lookup"><span data-stu-id="e9409-171">Select hello volume from which you wish toorestore hello file.</span></span>

    <span data-ttu-id="e9409-172">È possibile ripristinare da qualsiasi data.</span><span class="sxs-lookup"><span data-stu-id="e9409-172">You can restore from any point in time.</span></span> <span data-ttu-id="e9409-173">Date visualizzate in **grassetto** nel controllo di calendario hello indicare la disponibilità di hello di un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e9409-173">Dates which appear in **bold** in hello calendar control indicate hello availability of a restore point.</span></span> <span data-ttu-id="e9409-174">Dopo aver selezionata una data, in base alla pianificazione di backup (e successo hello di un'operazione di backup), è possibile selezionare un punto nel tempo da hello **ora** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="e9409-174">Once a date is selected, based on your backup schedule (and hello success of a backup operation), you can select a point in time from hello **Time** drop down.</span></span>

    ![Volume e dati](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. <span data-ttu-id="e9409-176">Selezionare toorecover elementi hello.</span><span class="sxs-lookup"><span data-stu-id="e9409-176">Select hello items toorecover.</span></span> <span data-ttu-id="e9409-177">È possibile selezioni più cartelle/file desiderato toorestore.</span><span class="sxs-lookup"><span data-stu-id="e9409-177">You can multi-select folders/files you wish toorestore.</span></span>

    ![Selezione dei file](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. <span data-ttu-id="e9409-179">Specificare parametri per il ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="e9409-179">Specify hello recovery parameters.</span></span>

    ![Opzioni di ripristino](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * <span data-ttu-id="e9409-181">È disponibile un'opzione di ripristino nel percorso originale toohello (in cui hello file/cartella verrebbe sovrascritto) o una posizione tooanother in hello nello stesso computer.</span><span class="sxs-lookup"><span data-stu-id="e9409-181">You have an option of restoring toohello original location (in which hello file/folder would be overwritten) or tooanother location in hello same machine.</span></span>
   * <span data-ttu-id="e9409-182">Se hello file/cartella in cui è presente nel percorso di destinazione hello toorestore, è possibile creare copie (due versioni di hello stesso file), sovrascrivere i file nel percorso di destinazione hello hello o ignorare il ripristino del file hello che esistono nella destinazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="e9409-182">If hello file/folder you wish toorestore exists in hello target location, you can create copies (two versions of hello same file), overwrite hello files in hello target location, or skip hello recovery of hello files which exist in hello target.</span></span>
   * <span data-ttu-id="e9409-183">Si consiglia di lasciare l'opzione predefinita hello ripristino hello ACL nel file hello che verrà eseguito il ripristino.</span><span class="sxs-lookup"><span data-stu-id="e9409-183">It is highly recommended that you leave hello default option of restoring hello ACLs on hello files which are being recovered.</span></span>
8. <span data-ttu-id="e9409-184">Una volta forniti i dati di input, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="e9409-184">Once these inputs are provided, click **Next**.</span></span> <span data-ttu-id="e9409-185">Hello ripristino flusso di lavoro che ripristina hello file toothis macchina, verrà avviato.</span><span class="sxs-lookup"><span data-stu-id="e9409-185">hello recovery workflow, which restores hello files toothis machine, will begin.</span></span>

## <a name="recover-tooan-alternate-machine"></a><span data-ttu-id="e9409-186">Ripristinare tooan alternativo macchina</span><span class="sxs-lookup"><span data-stu-id="e9409-186">Recover tooan alternate machine</span></span>
<span data-ttu-id="e9409-187">Se l'intero server viene perso, è comunque possibile ripristinare dati da computer diversi tooa di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="e9409-187">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="e9409-188">Hello alla procedura seguente viene illustrato del flusso di lavoro di hello.</span><span class="sxs-lookup"><span data-stu-id="e9409-188">hello following steps illustrate hello workflow.</span></span>  

<span data-ttu-id="e9409-189">terminologia di Hello utilizzata in questa procedura include:</span><span class="sxs-lookup"><span data-stu-id="e9409-189">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="e9409-190">*Computer di origine* : macchina originale di hello dal backup hello è stato eseguito e non è attualmente disponibile.</span><span class="sxs-lookup"><span data-stu-id="e9409-190">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="e9409-191">*Computer di destinazione* : dati di hello macchina toowhich hello viene ripristinati.</span><span class="sxs-lookup"><span data-stu-id="e9409-191">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="e9409-192">*Insieme di credenziali di esempio* : hello toowhich insieme di credenziali di hello Backup *macchina di origine* e *nel computer di destinazione* registrati.</span><span class="sxs-lookup"><span data-stu-id="e9409-192">*Sample vault* – hello Backup vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="e9409-193">Impossibile ripristinare i backup eseguiti da un computer in un computer in cui è in esecuzione una versione precedente del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="e9409-193">Backups taken from a machine cannot be restored on a machine which is running an earlier version of hello operating system.</span></span> <span data-ttu-id="e9409-194">Ad esempio, se i backup vengono eseguiti da un computer che esegue Windows 7, è possibile ripristinare i dati in un computer con Windows 8 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="e9409-194">For example, if backups are taken from a Windows 7 machine, it can be restored on a Windows 8 or above machine.</span></span> <span data-ttu-id="e9409-195">Tuttavia, hello viceversa non ha valore true.</span><span class="sxs-lookup"><span data-stu-id="e9409-195">However, hello vice-versa does not hold true.</span></span>
>
>

1. <span data-ttu-id="e9409-196">Aprire hello **Backup di Microsoft Azure** allineamento in su hello *nel computer di destinazione*.</span><span class="sxs-lookup"><span data-stu-id="e9409-196">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>
2. <span data-ttu-id="e9409-197">Verificare che hello *inviala* hello e *macchina di origine* sono registrato toohello stesso insieme di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="e9409-197">Ensure that hello *Target machine* and hello *Source machine* are registered toohello same backup vault.</span></span>
3. <span data-ttu-id="e9409-198">Fare clic su **Ripristina dati** flusso di lavoro tooinitiate hello.</span><span class="sxs-lookup"><span data-stu-id="e9409-198">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Ripristina dati](./media/backup-azure-restore-windows-server-classic/recover.png)
4. <span data-ttu-id="e9409-200">Selezionare **Un altro server**</span><span class="sxs-lookup"><span data-stu-id="e9409-200">Select **Another server**</span></span>

    ![Un altro server](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. <span data-ttu-id="e9409-202">Fornire file delle credenziali dell'insieme di credenziali hello corrispondente toohello *insieme di credenziali di esempio*.</span><span class="sxs-lookup"><span data-stu-id="e9409-202">Provide hello vault credential file that corresponds toohello *Sample vault*.</span></span> <span data-ttu-id="e9409-203">Se file di credenziali dell'insieme di credenziali hello (scaduti o non validi) scaricare un nuovo file delle credenziali dell'insieme di credenziali da hello *insieme di credenziali di esempio* nel portale di Azure classico hello.</span><span class="sxs-lookup"><span data-stu-id="e9409-203">If hello vault credential file is invalid (or expired) download a new vault credential file from hello *Sample vault* in hello Azure classic portal.</span></span> <span data-ttu-id="e9409-204">Una volta file delle credenziali dell'insieme di credenziali hello viene fornito, viene visualizzato insieme di credenziali backup hello su file delle credenziali dell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="e9409-204">Once hello vault credential file is provided, hello backup vault against hello vault credential file is displayed.</span></span>
6. <span data-ttu-id="e9409-205">Seleziona hello *macchina di origine* dall'elenco di hello macchine visualizzato.</span><span class="sxs-lookup"><span data-stu-id="e9409-205">Select hello *Source machine* from hello list of displayed machines.</span></span>

    ![Elenco di computer](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. <span data-ttu-id="e9409-207">Selezionare entrambi hello **Cerca file** o **Sfoglia file** opzione.</span><span class="sxs-lookup"><span data-stu-id="e9409-207">Select either hello **Search for files** or **Browse for files** option.</span></span> <span data-ttu-id="e9409-208">A scopo di hello in questa sezione, si utilizzerà hello **Cerca file** opzione.</span><span class="sxs-lookup"><span data-stu-id="e9409-208">For hello purpose of this section, we will use hello **Search for files** option.</span></span>

    ![Ricerca](./media/backup-azure-restore-windows-server-classic/search.png)
8. <span data-ttu-id="e9409-210">Selezionare il volume di hello e alla data nella schermata successiva hello.</span><span class="sxs-lookup"><span data-stu-id="e9409-210">Select hello volume and date in hello next screen.</span></span> <span data-ttu-id="e9409-211">Ricerca per nome di cartella/file hello desiderato toorestore.</span><span class="sxs-lookup"><span data-stu-id="e9409-211">Search for hello folder/file name you want toorestore.</span></span>

    ![Ricerca di elementi](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. <span data-ttu-id="e9409-213">Selezionare il percorso di hello in cui è necessario ripristinare toobe hello file.</span><span class="sxs-lookup"><span data-stu-id="e9409-213">Select hello location where hello files need toobe restored.</span></span>

    ![Percorso di ripristino](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. <span data-ttu-id="e9409-215">Fornire una passphrase di crittografia hello fornita durante *macchina di origine* registrazione troppo*insieme di credenziali di esempio*.</span><span class="sxs-lookup"><span data-stu-id="e9409-215">Provide hello encryption passphrase that was provided during *Source machine’s* registration too*Sample vault*.</span></span>

    ![Crittografia](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. <span data-ttu-id="e9409-217">Una volta hello input viene fornito, fare clic su **ripristinare**, che i trigger hello ripristino del backup del file di destinazione toohello fornito hello.</span><span class="sxs-lookup"><span data-stu-id="e9409-217">Once hello input is provided, click **Recover**, which triggers hello restore of hello backed up files toohello destination provided.</span></span>

## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a><span data-ttu-id="e9409-218">Utilizzare il ripristino immediato toorestore dati tooan macchina alternativo</span><span class="sxs-lookup"><span data-stu-id="e9409-218">Use Instant Restore toorestore data tooan alternate machine</span></span>
<span data-ttu-id="e9409-219">Se l'intero server viene perso, è comunque possibile ripristinare dati da computer diversi tooa di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="e9409-219">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="e9409-220">Hello alla procedura seguente viene illustrato del flusso di lavoro di hello.</span><span class="sxs-lookup"><span data-stu-id="e9409-220">hello following steps illustrate hello workflow.</span></span>

<span data-ttu-id="e9409-221">terminologia di Hello utilizzata in questa procedura include:</span><span class="sxs-lookup"><span data-stu-id="e9409-221">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="e9409-222">*Computer di origine* : macchina originale di hello dal backup hello è stato eseguito e non è attualmente disponibile.</span><span class="sxs-lookup"><span data-stu-id="e9409-222">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="e9409-223">*Computer di destinazione* : dati di hello macchina toowhich hello viene ripristinati.</span><span class="sxs-lookup"><span data-stu-id="e9409-223">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="e9409-224">*Insieme di credenziali di esempio* : hello toowhich insieme di credenziali per servizi di ripristino di hello *macchina di origine* e *nel computer di destinazione* registrati.</span><span class="sxs-lookup"><span data-stu-id="e9409-224">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="e9409-225">I backup non possono essere ripristinato tooa computer di destinazione esegue una versione precedente del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="e9409-225">Backups can't be restored tooa target machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="e9409-226">Ad esempio, un backup eseguito su un computer con Windows 7 può essere ripristinato in un computer con Windows 8 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="e9409-226">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="e9409-227">Un backup eseguito da un computer Windows 8 non può essere ripristinato tooa Windows 7 computer.</span><span class="sxs-lookup"><span data-stu-id="e9409-227">A backup taken from a Windows 8 computer cannot be restored tooa Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="e9409-228">Aprire hello **Backup di Microsoft Azure** allineamento in su hello *nel computer di destinazione*.</span><span class="sxs-lookup"><span data-stu-id="e9409-228">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>

2. <span data-ttu-id="e9409-229">Assicurarsi di hello *nel computer di destinazione* hello e *macchina di origine* sono registrato toohello servizi di ripristino stesso insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="e9409-229">Ensure hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>

3. <span data-ttu-id="e9409-230">Fare clic su **Ripristina dati** tooopen hello **procedura guidata Ripristina dati**.</span><span class="sxs-lookup"><span data-stu-id="e9409-230">Click **Recover Data** tooopen hello **Recover Data wizard**.</span></span>

    ![Ripristina dati](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="e9409-232">In hello **Introduzione** riquadro, selezionare **un altro server**</span><span class="sxs-lookup"><span data-stu-id="e9409-232">On hello **Getting Started** pane, select **Another server**</span></span>

    ![Un altro server](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="e9409-234">Fornire file delle credenziali dell'insieme di credenziali hello corrispondente toohello *insieme di credenziali di esempio*, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="e9409-234">Provide hello vault credential file that corresponds toohello *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="e9409-235">Caso di file delle credenziali dell'insieme di credenziali hello (scaduti o non validi), è possibile scaricare un nuovo file delle credenziali dell'insieme di credenziali da hello *insieme di credenziali di esempio* in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e9409-235">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="e9409-236">Dopo aver specificato un insieme valido di credenziali, nome hello di hello corrispondente dell'insieme di credenziali di Backup.</span><span class="sxs-lookup"><span data-stu-id="e9409-236">Once you provide a valid vault credential, hello name of hello corresponding Backup Vault appears.</span></span>

6. <span data-ttu-id="e9409-237">In hello **selezione Server di Backup** riquadro, seleziona hello *macchina di origine* dall'elenco di hello macchine visualizzati e fornire la passphrase hello.</span><span class="sxs-lookup"><span data-stu-id="e9409-237">On hello **Select Backup Server** pane, select hello *Source machine* from hello list of displayed machines and provide hello passphrase.</span></span> <span data-ttu-id="e9409-238">Quindi fare clic su **Next**.</span><span class="sxs-lookup"><span data-stu-id="e9409-238">Then click **Next**.</span></span>

    ![Elenco di computer](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="e9409-240">In hello **selezionare la modalità di ripristino** riquadro **singoli file e cartelle** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="e9409-240">On hello **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Ricerca](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="e9409-242">In hello **seleziona Volume e data** riquadro, volume hello select che contiene i file hello e/o le cartelle da toorestore.</span><span class="sxs-lookup"><span data-stu-id="e9409-242">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="e9409-243">Calendario hello, selezionare un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e9409-243">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="e9409-244">È possibile ripristinare da qualsiasi punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e9409-244">You can restore from any recovery point in time.</span></span> <span data-ttu-id="e9409-245">Le date in **grassetto** indicare hello la disponibilità di almeno un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e9409-245">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="e9409-246">Dopo aver selezionato una data, se sono disponibili più punti di ripristino, scegliere il punto di ripristino specifico di hello da hello **ora** dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="e9409-246">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Ricerca di elementi](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="e9409-248">Fare clic su **montare** toolocally montaggio hello punto di ripristino come in un volume di ripristino del *nel computer di destinazione*.</span><span class="sxs-lookup"><span data-stu-id="e9409-248">Click **Mount** toolocally mount hello recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="e9409-249">In hello **Sfoglia e ripristinare i file** riquadro, fare clic su **Sfoglia** tooopen in Esplora risorse e individuare i file hello e le cartelle desiderate.</span><span class="sxs-lookup"><span data-stu-id="e9409-249">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Crittografia](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="e9409-251">In Esplora risorse, copiare i file hello o le cartelle dal volume di ripristino hello e incollarli tooyour *inviala* percorso.</span><span class="sxs-lookup"><span data-stu-id="e9409-251">In Windows Explorer, copy hello files and/or folders from hello recovery volume and paste them tooyour *Target machine* location.</span></span> <span data-ttu-id="e9409-252">È possibile aprire o flusso di file hello direttamente dal volume di ripristino hello e verificare hello corretto versioni vengono ripristinate.</span><span class="sxs-lookup"><span data-stu-id="e9409-252">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Crittografia](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="e9409-254">Al termine il ripristino file hello e/o cartelle, hello **Sfoglia e i file di ripristino** riquadro, fare clic su **Smonta**.</span><span class="sxs-lookup"><span data-stu-id="e9409-254">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="e9409-255">Quindi fare clic su **Sì** tooconfirm che si desidera volume hello toounmount.</span><span class="sxs-lookup"><span data-stu-id="e9409-255">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Crittografia](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="e9409-257">Se non si sceglie Smonta, hello ripristino Volume rimarrà montata per sei ore dall'ora di hello quando è stato montato.</span><span class="sxs-lookup"><span data-stu-id="e9409-257">If you do not click Unmount, hello Recovery Volume will remain mounted for six hours from hello time when it was mounted.</span></span> <span data-ttu-id="e9409-258">Nessuna operazione di backup verranno eseguito mentre hello volume montato.</span><span class="sxs-lookup"><span data-stu-id="e9409-258">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="e9409-259">Toorun qualsiasi operazione di backup pianificato durante la fase di hello quando hello volume montato, verrà eseguito dopo il volume di ripristino hello viene disinstallato.</span><span class="sxs-lookup"><span data-stu-id="e9409-259">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="next-steps"></a><span data-ttu-id="e9409-260">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e9409-260">Next steps</span></span>
* [<span data-ttu-id="e9409-261">Backup di Azure - Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="e9409-261">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
* <span data-ttu-id="e9409-262">Visitare hello [Forum di Azure Backup](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span><span class="sxs-lookup"><span data-stu-id="e9409-262">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span></span>

## <a name="learn-more"></a><span data-ttu-id="e9409-263">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="e9409-263">Learn more</span></span>
* [<span data-ttu-id="e9409-264">Panoramica di Azure Backup</span><span class="sxs-lookup"><span data-stu-id="e9409-264">Azure Backup Overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [<span data-ttu-id="e9409-265">Eseguire il backup di macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="e9409-265">Backup Azure virtual machines</span></span>](backup-azure-vms-introduction.md)
* [<span data-ttu-id="e9409-266">Eseguire il backup dei carichi di lavoro di Microsoft</span><span class="sxs-lookup"><span data-stu-id="e9409-266">Backup up Microsoft workloads</span></span>](backup-azure-dpm-introduction.md)
