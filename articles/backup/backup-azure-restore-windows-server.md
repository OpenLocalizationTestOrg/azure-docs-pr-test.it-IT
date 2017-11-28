---
title: dati aaaRestore tooa Azure Windows Server o computer Windows | Documenti Microsoft
description: Informazioni su come i dati toorestore archiviati in Azure tooa Windows Server o computer Windows.
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
ms.openlocfilehash: 11335495e448986a74f1733406f87e04331641d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a><span data-ttu-id="3c5ce-103">Ripristinare i file tooa Windows server o computer client Windows utilizzando il modello di distribuzione di gestione risorse</span><span class="sxs-lookup"><span data-stu-id="3c5ce-103">Restore files tooa Windows server or Windows client machine using Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3c5ce-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3c5ce-104">Azure portal</span></span>](backup-azure-restore-windows-server.md)
> * [<span data-ttu-id="3c5ce-105">Portale classico</span><span class="sxs-lookup"><span data-stu-id="3c5ce-105">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
>
>

<span data-ttu-id="3c5ce-106">Questo articolo viene illustrato come toorestore dati da un insieme di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-106">This article explains how toorestore data from a backup vault.</span></span> <span data-ttu-id="3c5ce-107">dati toorestore, guidata hello Ripristina dati nell'agente di Microsoft Azure Recovery Services (MARS) hello.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-107">toorestore data, you use hello Recover Data wizard in hello Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="3c5ce-108">Quando si ripristinano dati, è possibile:</span><span class="sxs-lookup"><span data-stu-id="3c5ce-108">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="3c5ce-109">Ripristino dati toohello stesso computer dai quali backup hello sono stati eseguiti.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-109">Restore data toohello same machine from which hello backups were taken.</span></span>
* <span data-ttu-id="3c5ce-110">Ripristinare dati tooan alternativo macchina.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-110">Restore data tooan alternate machine.</span></span>

<span data-ttu-id="3c5ce-111">Gennaio January 2017, Microsoft ha rilasciato un agente di anteprima aggiornamento toohello MARS.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-111">In January 2017, Microsoft released a Preview update toohello MARS agent.</span></span> <span data-ttu-id="3c5ce-112">Insieme a correzioni di bug, questo aggiornamento consente a ripristinare immediata, che consente di toomount uno snapshot del punto di ripristino scrivibile come volume di ripristino.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-112">Along with bug fixes, this update enables Instant Restore, which allows you toomount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="3c5ce-113">È quindi possibile esplorare hello ripristino volume e copia i file tooa computer locale in modo selettivo il ripristino dei file.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-113">You can then explore hello recovery volume and copy files tooa local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="3c5ce-114">Hello [gennaio January 2017 aggiornamento di Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview) è obbligatorio se si desidera toouse ripristino immediato toorestore dati.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-114">hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want toouse Instant Restore toorestore data.</span></span> <span data-ttu-id="3c5ce-115">Dati di backup hello devono inoltre essere protetti in insiemi di credenziali in impostazioni locali elencate nell'articolo di supporto tecnico hello.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-115">Also hello backup data must be protected in vaults in locales listed in hello support article.</span></span> <span data-ttu-id="3c5ce-116">Consultare hello [gennaio January 2017 aggiornamento di Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview) per l'elenco più recente di hello delle impostazioni locali che supportano il ripristino immediato.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-116">Consult hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for hello latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="3c5ce-117">Il ripristino istantaneo **non** è attualmente disponibile in tutte le impostazioni locali.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-117">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="3c5ce-118">Ripristino immediato è disponibile per l'uso di insiemi di credenziali di servizi di ripristino in hello portale di Azure e gli insiemi di credenziali di Backup nel portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-118">Instant Restore is available for use in Recovery Services vaults in hello Azure portal and Backup vaults in hello classic portal.</span></span> <span data-ttu-id="3c5ce-119">Se si desidera ripristinare immediata toouse, scaricare l'aggiornamento di MARS hello e seguire le procedure hello che menzionano il ripristino immediato.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-119">If you want toouse Instant Restore, download hello MARS update, and follow hello procedures that mention Instant Restore.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a><span data-ttu-id="3c5ce-120">Utilizzare il ripristino immediato toorecover dati toohello nello stesso computer</span><span class="sxs-lookup"><span data-stu-id="3c5ce-120">Use Instant Restore toorecover data toohello same machine</span></span>

<span data-ttu-id="3c5ce-121">Se è stato eliminato accidentalmente un file e preferenze di toorestore è toohello stessa macchina (da cui hello backup viene eseguito), hello seguendo i passaggi consentono di ripristinare i dati di hello.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-121">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="3c5ce-122">Aprire hello **Backup di Microsoft Azure** allineamento in.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-122">Open hello **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="3c5ce-123">Se non si conosce in cui è stato installato hello snap-in, eseguire la ricerca computer hello o un server per **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-123">If you don't know where hello snap in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="3c5ce-124">app desktop Hello dovrebbe essere visualizzato nei risultati della ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-124">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="3c5ce-125">Fare clic su **Ripristina dati** guidata hello toostart.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-125">Click **Recover Data** toostart hello wizard.</span></span>

    ![Ripristina dati](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="3c5ce-127">In hello **Introduzione** riquadro, toorestore hello dati toohello stesso server o computer, selezionare **server (`<server name>`)** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-127">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Scegliere questo toohello di dati server opzione toorestore hello nello stesso computer](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="3c5ce-129">In hello **selezionare la modalità di ripristino** riquadro scegliere **singoli file e cartelle** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-129">On hello **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Ricerca dei file](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="3c5ce-131">In hello **seleziona Volume e data** riquadro, volume hello select che contiene i file hello e/o le cartelle da toorestore.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-131">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="3c5ce-132">Calendario hello, selezionare un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-132">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="3c5ce-133">È possibile ripristinare da qualsiasi punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-133">You can restore from any recovery point in time.</span></span> <span data-ttu-id="3c5ce-134">Le date in **grassetto** indicare hello la disponibilità di almeno un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-134">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="3c5ce-135">Dopo aver selezionato una data, se sono disponibili più punti di ripristino, scegliere il punto di ripristino specifico di hello da hello **ora** dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-135">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Volume e dati](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="3c5ce-137">Dopo aver scelto toorestore punto di ripristino hello, fare clic su **montare**.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-137">Once you have chosen hello recovery point toorestore, click **Mount**.</span></span>

    <span data-ttu-id="3c5ce-138">Backup di Azure monta il punto di ripristino locali hello che viene utilizzato come un volume di ripristino.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-138">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="3c5ce-139">In hello **Sfoglia e ripristinare i file** riquadro, fare clic su **Sfoglia** tooopen in Esplora risorse e individuare i file hello e le cartelle desiderate.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-139">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Opzioni di ripristino](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="3c5ce-141">In Esplora risorse, la copia di file hello e/o le cartelle si toorestore e incollarlo tooany percorso locale toohello server o computer.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-141">In Windows Explorer, copy hello files and/or folders you want toorestore and paste them tooany location local toohello server or computer.</span></span> <span data-ttu-id="3c5ce-142">È possibile aprire o flusso di file hello direttamente dal volume di ripristino hello e verificare hello corretto versioni vengono ripristinate.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-142">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Copiare e incollare i file e cartelle dal percorso toolocal volume montato](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="3c5ce-144">Al termine il ripristino file hello e/o cartelle, hello **Sfoglia e i file di ripristino** riquadro, fare clic su **Smonta**.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-144">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="3c5ce-145">Quindi fare clic su **Sì** tooconfirm che si desidera volume hello toounmount.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-145">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Smontare il volume di hello e verificare](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="3c5ce-147">Se non si sceglie Smonta, hello ripristino Volume rimarrà montata per 6 ore dall'ora di hello quando è stato montato.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-147">If you do not click Unmount, hello Recovery Volume will remain mounted for 6 hours from hello time when it was mounted.</span></span> <span data-ttu-id="3c5ce-148">Tuttavia, il tempo di montaggio hello è estesa fino a un massimo di 24 ore in caso di una copia di file in corso.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-148">However, hello mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="3c5ce-149">Nessuna operazione di backup verranno eseguito mentre hello volume montato.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-149">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="3c5ce-150">Toorun qualsiasi operazione di backup pianificato durante la fase di hello quando hello volume montato, verrà eseguito dopo il volume di ripristino hello viene disinstallato.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-150">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a><span data-ttu-id="3c5ce-151">Utilizzare il ripristino immediato toorestore dati tooan macchina alternativo</span><span class="sxs-lookup"><span data-stu-id="3c5ce-151">Use Instant Restore toorestore data tooan alternate machine</span></span>
<span data-ttu-id="3c5ce-152">Se l'intero server viene perso, è comunque possibile ripristinare dati da computer diversi tooa di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-152">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="3c5ce-153">Hello alla procedura seguente viene illustrato del flusso di lavoro di hello.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-153">hello following steps illustrate hello workflow.</span></span>


<span data-ttu-id="3c5ce-154">terminologia di Hello utilizzata in questa procedura include:</span><span class="sxs-lookup"><span data-stu-id="3c5ce-154">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="3c5ce-155">*Computer di origine* : macchina originale di hello dal backup hello è stato eseguito e non è attualmente disponibile.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-155">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="3c5ce-156">*Computer di destinazione* : dati di hello macchina toowhich hello viene ripristinati.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-156">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="3c5ce-157">*Insieme di credenziali di esempio* : hello toowhich insieme di credenziali per servizi di ripristino di hello *macchina di origine* e *nel computer di destinazione* registrati.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-157">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="3c5ce-158">I backup non possono essere ripristinato tooa computer di destinazione esegue una versione precedente del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-158">Backups can't be restored tooa target machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="3c5ce-159">Ad esempio, un backup eseguito su un computer con Windows 7 può essere ripristinato in un computer con Windows 8 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-159">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="3c5ce-160">Un backup eseguito da un computer Windows 8 non può essere ripristinato tooa Windows 7 computer.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-160">A backup taken from a Windows 8 computer cannot be restored tooa Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="3c5ce-161">Aprire hello **Backup di Microsoft Azure** allineamento in su hello *nel computer di destinazione*.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-161">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>

2. <span data-ttu-id="3c5ce-162">Assicurarsi di hello *nel computer di destinazione* hello e *macchina di origine* sono registrato toohello servizi di ripristino stesso insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-162">Ensure hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>

3. <span data-ttu-id="3c5ce-163">Fare clic su **Ripristina dati** tooopen hello **procedura guidata Ripristina dati**.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-163">Click **Recover Data** tooopen hello **Recover Data wizard**.</span></span>

    ![Ripristina dati](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="3c5ce-165">In hello **Introduzione** riquadro, selezionare **un altro server**</span><span class="sxs-lookup"><span data-stu-id="3c5ce-165">On hello **Getting Started** pane, select **Another server**</span></span>

    ![Un altro server](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="3c5ce-167">Fornire file delle credenziali dell'insieme di credenziali hello corrispondente toohello *insieme di credenziali di esempio*, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-167">Provide hello vault credential file that corresponds toohello *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="3c5ce-168">Caso di file delle credenziali dell'insieme di credenziali hello (scaduti o non validi), è possibile scaricare un nuovo file delle credenziali dell'insieme di credenziali da hello *insieme di credenziali di esempio* in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-168">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="3c5ce-169">Dopo aver specificato un insieme valido di credenziali, nome hello di hello corrispondente dell'insieme di credenziali di Backup.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-169">Once you provide a valid vault credential, hello name of hello corresponding Backup Vault appears.</span></span>


6. <span data-ttu-id="3c5ce-170">In hello **selezione Server di Backup** riquadro, seleziona hello *macchina di origine* dall'elenco di hello macchine visualizzati e fornire la passphrase hello.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-170">On hello **Select Backup Server** pane, select hello *Source machine* from hello list of displayed machines and provide hello passphrase.</span></span> <span data-ttu-id="3c5ce-171">Quindi fare clic su **Next**.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-171">Then click **Next**.</span></span>

    ![Elenco di computer](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="3c5ce-173">In hello **selezionare la modalità di ripristino** riquadro **singoli file e cartelle** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-173">On hello **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Ricerca](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="3c5ce-175">In hello **seleziona Volume e data** riquadro, volume hello select che contiene i file hello e/o le cartelle da toorestore.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-175">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="3c5ce-176">Calendario hello, selezionare un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-176">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="3c5ce-177">È possibile ripristinare da qualsiasi punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-177">You can restore from any recovery point in time.</span></span> <span data-ttu-id="3c5ce-178">Le date in **grassetto** indicare hello la disponibilità di almeno un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-178">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="3c5ce-179">Dopo aver selezionato una data, se sono disponibili più punti di ripristino, scegliere il punto di ripristino specifico di hello da hello **ora** dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-179">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Ricerca di elementi](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="3c5ce-181">Fare clic su **montare** toolocally montaggio hello punto di ripristino come in un volume di ripristino del *nel computer di destinazione*.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-181">Click **Mount** toolocally mount hello recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="3c5ce-182">In hello **Sfoglia e ripristinare i file** riquadro, fare clic su **Sfoglia** tooopen in Esplora risorse e individuare i file hello e le cartelle desiderate.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-182">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Crittografia](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="3c5ce-184">In Esplora risorse, copiare i file hello o le cartelle dal volume di ripristino hello e incollarli tooyour *inviala* percorso.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-184">In Windows Explorer, copy hello files and/or folders from hello recovery volume and paste them tooyour *Target machine* location.</span></span> <span data-ttu-id="3c5ce-185">È possibile aprire o flusso di file hello direttamente dal volume di ripristino hello e verificare hello corretto versioni vengono ripristinate.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-185">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Crittografia](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="3c5ce-187">Al termine il ripristino file hello e/o cartelle, hello **Sfoglia e i file di ripristino** riquadro, fare clic su **Smonta**.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-187">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="3c5ce-188">Quindi fare clic su **Sì** tooconfirm che si desidera volume hello toounmount.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-188">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Crittografia](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="3c5ce-190">Se non si sceglie Smonta, hello ripristino Volume rimarrà montata per 6 ore dall'ora di hello quando è stato montato.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-190">If you do not click Unmount, hello Recovery Volume will remain mounted for 6 hours from hello time when it was mounted.</span></span> <span data-ttu-id="3c5ce-191">Tuttavia, il tempo di montaggio hello è estesa fino a un massimo di 24 ore in caso di una copia di file in corso.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-191">However, hello mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="3c5ce-192">Nessuna operazione di backup verranno eseguito mentre hello volume montato.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-192">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="3c5ce-193">Toorun qualsiasi operazione di backup pianificato durante la fase di hello quando hello volume montato, verrà eseguito dopo il volume di ripristino hello viene disinstallato.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-193">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >

## <a name="troubleshooting"></a><span data-ttu-id="3c5ce-194">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="3c5ce-194">Troubleshooting</span></span>
<span data-ttu-id="3c5ce-195">Se Azure Backup non correttamente montare il volume di ripristino hello anche dopo diversi minuti di facendo clic su **montare** o volume di ripristino ha esito negativo toomount hello con uno o più errori, seguire i passaggi di hello sotto toobegin ripristino normalmente.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-195">If Azure Backup does not successfully mount hello recovery volume even after several minutes of clicking **Mount** or fails toomount hello recovery volume with one or more errors, follow hello steps below toobegin recovering normally.</span></span>

1.  <span data-ttu-id="3c5ce-196">Annullare il processo di installazione in corso hello nel caso in cui è in esecuzione per diversi minuti.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-196">Cancel hello ongoing mount process in case it has been running for several minutes.</span></span>

2.  <span data-ttu-id="3c5ce-197">Verificare che trovino in più recente dell'agente di Backup di Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-197">Ensure that you are on hello latest version of hello Azure Backup agent.</span></span> <span data-ttu-id="3c5ce-198">toofind le informazioni sulla versione di hello di Azure Backup agent, fare clic su **su Microsoft Azure Recovery Services Agent** su hello **azioni** riquadro di Microsoft Azure Backup console e verificare che hello  **Versione** numero è uguale tooor superiore indicato nella versione di hello [questo articolo](https://go.microsoft.com/fwlink/?linkid=229525).</span><span class="sxs-lookup"><span data-stu-id="3c5ce-198">toofind out hello version information of Azure Backup agent, click on **About Microsoft Azure Recovery Services Agent** on hello **Actions** pane of Microsoft Azure Backup console and ensure that hello **Version** number is equal tooor higher than hello version mentioned in [this article](https://go.microsoft.com/fwlink/?linkid=229525).</span></span> <span data-ttu-id="3c5ce-199">È possibile scaricare una versione più recente di hello dal [qui](https://go.microsoft.com/fwLink/?LinkID=288905)</span><span class="sxs-lookup"><span data-stu-id="3c5ce-199">You can download hello latest version from [here](https://go.microsoft.com/fwLink/?LinkID=288905)</span></span>

3.  <span data-ttu-id="3c5ce-200">Andare troppo**Gestione dispositivi** -> **i controller di archiviazione** e assicurarsi che sia possibile individuare **iniziatore iSCSI Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-200">Go too**Device Manager** -> **Storage Controllers** and ensure that you can locate **Microsoft iSCSI Initiator**.</span></span> <span data-ttu-id="3c5ce-201">Se si desidera trovare, passare direttamente toostep 7 seguente.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-201">If you can locate it, directly go toostep 7 below.</span></span> 

4.  <span data-ttu-id="3c5ce-202">Se è possibile individuare servizio iniziatore iSCSI Microsoft, come indicato nel passaggio 3, controllare toosee se è possibile trovare una voce nella sezione **Gestione dispositivi** -> **i controller di archiviazione** chiamato  **Dispositivo sconosciuto** con l'ID Hardware **ROOT\ISCSIPRT**.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-202">If you cannot locate Microsoft iSCSI Initiator service as mentioned in step 3, check toosee if you can find an entry under **Device Manager** -> **Storage Controllers** called **Unknown Device** with Hardware ID **ROOT\ISCSIPRT**.</span></span>

5.  <span data-ttu-id="3c5ce-203">Fare clic con il pulsante destro del mouse su **Dispositivo sconosciuto** e scegliere **Aggiornamento software driver**.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-203">Right click on **Unknown Device** and select **Update Driver Software**.</span></span>

6.  <span data-ttu-id="3c5ce-204">Aggiorna driver hello selezionando l'opzione hello troppo **cerca automaticamente un driver aggiornato**.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-204">Update hello driver by selecting hello option too **Search automatically for updated driver software**.</span></span> <span data-ttu-id="3c5ce-205">Completamento dell'aggiornamento hello debba modificare **dispositivo sconosciuto** troppo**iniziatore iSCSI Microsoft** come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-205">Completion of hello update should change **Unknown Device** too**Microsoft iSCSI Initiator** as shown below.</span></span> 

    ![Crittografia](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  <span data-ttu-id="3c5ce-207">Andare troppo**Task Manager** -> **servizi (locale)** -> **servizio iniziatore iSCSI Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-207">Go too**Task Manager** -> **Services (Local)** -> **Microsoft iSCSI Initiator Service**.</span></span> 

    ![Crittografia](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  <span data-ttu-id="3c5ce-209">Riavviare servizio iniziatore iSCSI Microsoft di hello facendo clic sul servizio hello, facendo clic su **arrestare** e ulteriormente destro del mouse facendo clic su Nuovo e facendo clic su **avviare**.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-209">Restart hello Microsoft iSCSI Initiator service by right-clicking on hello service, clicking on **Stop** and further right clicking again and clicking on **Start**.</span></span>

9.  <span data-ttu-id="3c5ce-210">Riprovare il ripristino istantaneo.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-210">Retry recovering using Instant Restore.</span></span> 

<span data-ttu-id="3c5ce-211">Se non riesce ripristino hello, riavviare il server e client.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-211">If hello recovery still fails, reboot your server/client.</span></span> <span data-ttu-id="3c5ce-212">Se non è auspicabile il riavvio o recupero hello persistono anche dopo il riavvio hello server, riprovare il ripristino da un computer alternativo e contattare il supporto di Azure passando troppo[portale Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) e l'invio di una richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="3c5ce-212">If a reboot is not desirable or hello recovery still fails even after rebooting hello server, try recovering from an Alternate Machine, and contact Azure Support by going too[Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and submitting a support request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c5ce-213">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3c5ce-213">Next steps</span></span>
* <span data-ttu-id="3c5ce-214">Dopo aver ripristinato i file e le cartelle, è possibile [gestire i backup](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="3c5ce-214">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
