---
title: 'Backup di Azure: Ripristino dello stato del sistema tooa Windows Server | Documenti Microsoft'
description: Procedura dettagliata per il ripristino dello stato del sistema di Windows Server da un backup in Azure.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/18/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: a45506507f53e2744350d3b6b2e52f1db415de4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-system-state-toowindows-server"></a><span data-ttu-id="68ae2-103">Ripristino dello stato del sistema tooWindows Server</span><span class="sxs-lookup"><span data-stu-id="68ae2-103">Restore System State tooWindows Server</span></span>

<span data-ttu-id="68ae2-104">Questo articolo illustra come insieme di credenziali di backup dello stato del sistema di Windows Server toorestore da un ripristino di servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="68ae2-104">This article explains how toorestore Windows Server System State backups from an Azure Recovery Services vault.</span></span> <span data-ttu-id="68ae2-105">toorestore dello stato del sistema, è necessario eseguire il backup dello stato del sistema (create utilizzando le istruzioni di hello in [eseguire il backup dello stato del sistema](backup-azure-system-state.md#back-up-windows-server-system-state-preview)) e assicurarsi di aver installato hello [versione più recente di Microsoft Azure Recovery hello L'agente di servizi (MARS)](http://aka.ms/azurebackup_agent).</span><span class="sxs-lookup"><span data-stu-id="68ae2-105">toorestore System State, you must have a System State backup (created using hello instructions in [Back up System State](backup-azure-system-state.md#back-up-windows-server-system-state-preview)), and make sure you have installed hello [latest version of hello Microsoft Azure Recovery Services (MARS) agent](http://aka.ms/azurebackup_agent).</span></span> <span data-ttu-id="68ae2-106">Il ripristino dei dati dello stato del sistema di Windows Server da un insieme di credenziali di Servizi di ripristino di Azure è un processo in due passaggi:</span><span class="sxs-lookup"><span data-stu-id="68ae2-106">Recovering Windows Server System State data from an Azure Recovery Services vault is a two-step process:</span></span>

1. <span data-ttu-id="68ae2-107">Ripristinare lo stato del sistema sotto forma di file da Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="68ae2-107">Restore System State as files from Azure Backup.</span></span> <span data-ttu-id="68ae2-108">Quando si ripristina lo stato del sistema sotto forma di file da Backup di Azure, è possibile eseguire una di queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="68ae2-108">When restoring System State as files from Azure Backup, you can either:</span></span>
  * <span data-ttu-id="68ae2-109">Ripristino dello stato del sistema toohello nello stesso server in cui sono stati eseguiti backup hello, o</span><span class="sxs-lookup"><span data-stu-id="68ae2-109">Restore System State toohello same server where hello backups were taken, or</span></span>
  * <span data-ttu-id="68ae2-110">Server alternativo tooan file ripristino dello stato del sistema.</span><span class="sxs-lookup"><span data-stu-id="68ae2-110">Restore System State file tooan alternate server.</span></span>

2. <span data-ttu-id="68ae2-111">Applicare tooa di file hello ripristinato lo stato del sistema Windows Server.</span><span class="sxs-lookup"><span data-stu-id="68ae2-111">Apply hello restored System State files tooa Windows Server.</span></span>


## <a name="recover-system-state-files-toohello-same-server"></a><span data-ttu-id="68ae2-112">Ripristinare lo stato del sistema file toohello nello stesso server</span><span class="sxs-lookup"><span data-stu-id="68ae2-112">Recover System State files toohello same server</span></span>
<span data-ttu-id="68ae2-113">Hello alla procedura seguente viene illustrato come tooroll eseguire il backup di stato precedente tooa configurazione del Server di Windows.</span><span class="sxs-lookup"><span data-stu-id="68ae2-113">hello following steps explain how tooroll back your Windows Server configuration tooa previous state.</span></span> <span data-ttu-id="68ae2-114">Tooa indietro di configurazione noto, lo stato stabile, il server in sequenza può essere molto utile.</span><span class="sxs-lookup"><span data-stu-id="68ae2-114">Rolling your server configuration back tooa known, stable state, can be extremely valuable.</span></span> <span data-ttu-id="68ae2-115">Hello successivo dello stato del sistema del server di passaggi restore hello da un insieme di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="68ae2-115">hello following steps restore hello server's System State from a Recovery Services vault.</span></span> 

1. <span data-ttu-id="68ae2-116">Aprire hello **Backup di Microsoft Azure** snap-in.</span><span class="sxs-lookup"><span data-stu-id="68ae2-116">Open hello **Microsoft Azure Backup** snap-in.</span></span> <span data-ttu-id="68ae2-117">Se non si conosce in hello snap-in è stato installato, eseguire la ricerca computer hello o un server per **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="68ae2-117">If you don't know where hello snap-in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="68ae2-118">app desktop Hello dovrebbe essere visualizzato nei risultati della ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="68ae2-118">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="68ae2-119">Fare clic su **Ripristina dati** guidata hello toostart.</span><span class="sxs-lookup"><span data-stu-id="68ae2-119">Click **Recover Data** toostart hello wizard.</span></span>

    ![Ripristina dati](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="68ae2-121">In hello **Introduzione** riquadro, toorestore hello dati toohello stesso server o computer, selezionare **server (`<server name>`)** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="68ae2-121">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Scegliere questo toohello di dati server opzione toorestore hello nello stesso computer](./media/backup-azure-restore-system-state/samemachine.png)

4. <span data-ttu-id="68ae2-123">In hello **selezionare la modalità di ripristino** riquadro scegliere **dello stato del sistema** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="68ae2-123">On hello **Select Recovery Mode** pane, choose **System State** and then click **Next**.</span></span>

    ![Ricerca dei file](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. <span data-ttu-id="68ae2-125">Nel calendario hello in **seleziona Volume e data** punto riquadro, selezionare un ripristino.</span><span class="sxs-lookup"><span data-stu-id="68ae2-125">On hello calendar in **Select Volume and Date** pane, select a recovery point.</span></span> 

    <span data-ttu-id="68ae2-126">È possibile ripristinare da qualsiasi punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="68ae2-126">You can restore from any recovery point in time.</span></span> <span data-ttu-id="68ae2-127">Le date in **grassetto** indicare hello la disponibilità di almeno un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="68ae2-127">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="68ae2-128">Dopo aver selezionato una data, se sono disponibili più punti di ripristino, scegliere il punto di ripristino specifico di hello da hello **ora** dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="68ae2-128">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Volume e dati](./media/backup-azure-restore-system-state/select-date.png)

6. <span data-ttu-id="68ae2-130">Dopo aver scelto toorestore punto di ripristino hello, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="68ae2-130">Once you have chosen hello recovery point toorestore, click **Next**.</span></span>

    <span data-ttu-id="68ae2-131">Backup di Azure monta il punto di ripristino locali hello che viene utilizzato come un volume di ripristino.</span><span class="sxs-lookup"><span data-stu-id="68ae2-131">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="68ae2-132">Nel riquadro successivo di hello, specificare una destinazione hello per hello ripristinati i file di stato del sistema e fare clic su **Sfoglia** tooopen in Esplora risorse e individuare i file hello e le cartelle desiderate.</span><span class="sxs-lookup"><span data-stu-id="68ae2-132">On hello next pane, specify hello destination for hello recovered System State files and click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span> <span data-ttu-id="68ae2-133">opzione Hello **crea copie in modo da mantenere entrambe le versioni**, crea le copie dei singoli file in un archivio di file di stato del sistema esistente anziché creare una copia di hello dell'intero archivio dello stato del sistema di hello.</span><span class="sxs-lookup"><span data-stu-id="68ae2-133">hello option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating hello copy of hello entire System State archive.</span></span>

    ![Opzioni di ripristino](./media/backup-azure-restore-system-state/recover-as-files.png)

8. <span data-ttu-id="68ae2-135">Verificare i dettagli di hello di ripristino su hello **conferma** riquadro e fare clic su **ripristinare**.</span><span class="sxs-lookup"><span data-stu-id="68ae2-135">Verify hello details of recovery on hello **Confirmation** pane and click **Recover**.</span></span>

   ![Fare clic su Ripristina tooacknowledge hello Ripristina azione](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. <span data-ttu-id="68ae2-137">Hello copia *WindowsImageBackup* directory hello volume non critici tooa destinazione di ripristino del server di hello.</span><span class="sxs-lookup"><span data-stu-id="68ae2-137">Copy hello *WindowsImageBackup* directory in hello Recovery destination tooa non-critical volume of hello server.</span></span> <span data-ttu-id="68ae2-138">In genere, il volume del sistema operativo Windows hello è volume critico hello.</span><span class="sxs-lookup"><span data-stu-id="68ae2-138">Usually, hello Windows OS volume is hello critical volume.</span></span>

10. <span data-ttu-id="68ae2-139">Dopo il ripristino di hello ha esito positivo, seguire i passaggi di hello nella sezione hello [applica ripristinato lo stato del sistema toohello di file Server Windows](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), hello toocomplete il processo di ripristino dello stato del sistema.</span><span class="sxs-lookup"><span data-stu-id="68ae2-139">Once hello recovery is successful, follow hello steps in hello section, [Apply restored System State files toohello Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), toocomplete hello System State recovery process.</span></span>

## <a name="recover-system-state-files-tooan-alternate-server"></a><span data-ttu-id="68ae2-140">Ripristinare lo stato del sistema file server alternativo tooan</span><span class="sxs-lookup"><span data-stu-id="68ae2-140">Recover System State files tooan alternate server</span></span>

<span data-ttu-id="68ae2-141">Se il Server di Windows è danneggiato o non è accessibile e che si desidera toorestore è stabile tooa recuperando hello dello stato del sistema di Windows Server, è possibile ripristinare lo stato del sistema del server di hello danneggiato da un altro server.</span><span class="sxs-lookup"><span data-stu-id="68ae2-141">If your Windows Server is corrupted or inaccessible, and you want toorestore it tooa stable state by recovering hello Windows Server System State, you can restore hello corrupted server's System State from another server.</span></span> <span data-ttu-id="68ae2-142">Utilizzare hello seguendo i passaggi toohello ripristino dello stato del sistema in un server distinto.</span><span class="sxs-lookup"><span data-stu-id="68ae2-142">Use hello following steps toohello restore System State on a separate server.</span></span>  

<span data-ttu-id="68ae2-143">terminologia di Hello utilizzata in questa procedura include:</span><span class="sxs-lookup"><span data-stu-id="68ae2-143">hello terminology used in these steps includes:</span></span>

- <span data-ttu-id="68ae2-144">*Computer di origine* : macchina originale di hello dal backup hello è stato eseguito e non è attualmente disponibile.</span><span class="sxs-lookup"><span data-stu-id="68ae2-144">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
- <span data-ttu-id="68ae2-145">*Computer di destinazione* : dati di hello macchina toowhich hello viene ripristinati.</span><span class="sxs-lookup"><span data-stu-id="68ae2-145">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
- <span data-ttu-id="68ae2-146">*Insieme di credenziali di esempio* : hello toowhich insieme di credenziali per servizi di ripristino di hello *macchina di origine* e *nel computer di destinazione* registrati.</span><span class="sxs-lookup"><span data-stu-id="68ae2-146">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="68ae2-147">I backup eseguiti da un computer non possono essere ripristinato tooa macchina esegue una versione precedente del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="68ae2-147">Backups taken from one machine cannot be restored tooa machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="68ae2-148">Ad esempio, i backup eseguiti da Windows Server 2016 non può essere ripristino tooWindows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="68ae2-148">For example, backups taken from a Windows Server 2016 machine can't be restored tooWindows Server 2012 R2.</span></span> <span data-ttu-id="68ae2-149">È tuttavia possibile inverso hello.</span><span class="sxs-lookup"><span data-stu-id="68ae2-149">However, hello inverse is possible.</span></span> <span data-ttu-id="68ae2-150">È possibile utilizzare i backup di Windows Server 2012 R2 toorestore Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="68ae2-150">You can use backups from Windows Server 2012 R2 toorestore Windows Server 2016.</span></span>
>

1. <span data-ttu-id="68ae2-151">Aprire hello **Backup di Microsoft Azure** snap-in hello *nel computer di destinazione*.</span><span class="sxs-lookup"><span data-stu-id="68ae2-151">Open hello **Microsoft Azure Backup** snap-in on hello *Target machine*.</span></span>
2. <span data-ttu-id="68ae2-152">Verificare che hello *inviala* hello e *macchina di origine* sono registrato toohello servizi di ripristino stesso insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="68ae2-152">Ensure that hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>
3. <span data-ttu-id="68ae2-153">Fare clic su **Ripristina dati** flusso di lavoro tooinitiate hello.</span><span class="sxs-lookup"><span data-stu-id="68ae2-153">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Ripristina dati](./media/backup-azure-restore-windows-server-classic/recover.png)

4. <span data-ttu-id="68ae2-155">Selezionare **Un altro server**</span><span class="sxs-lookup"><span data-stu-id="68ae2-155">Select **Another server**</span></span>

    ![Un altro server](./media/backup-azure-restore-system-state/anotherserver.png)

5. <span data-ttu-id="68ae2-157">Fornire file delle credenziali dell'insieme di credenziali hello corrispondente toohello *insieme di credenziali di esempio*.</span><span class="sxs-lookup"><span data-stu-id="68ae2-157">Provide hello vault credential file that corresponds toohello *Sample vault*.</span></span> <span data-ttu-id="68ae2-158">Caso di file delle credenziali dell'insieme di credenziali hello (scaduti o non validi), è possibile scaricare un nuovo file delle credenziali dell'insieme di credenziali da hello *insieme di credenziali di esempio* in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="68ae2-158">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="68ae2-159">Una volta file delle credenziali dell'insieme di credenziali hello viene fornito, viene visualizzata insieme di credenziali di servizi di ripristino hello associata al file delle credenziali dell'insieme di credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="68ae2-159">Once hello vault credential file is provided, hello Recovery Services vault associated with hello vault credential file appears.</span></span>

6. <span data-ttu-id="68ae2-160">Nel riquadro di selezione Server di Backup hello selezionare hello *macchina di origine* dall'elenco di hello macchine visualizzato.</span><span class="sxs-lookup"><span data-stu-id="68ae2-160">On hello Select Backup Server pane, select hello *Source machine* from hello list of displayed machines.</span></span>

    ![Elenco di computer](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. <span data-ttu-id="68ae2-162">Nel riquadro di selezione modalità ripristino hello, scegliere **dello stato del sistema** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="68ae2-162">On hello Select Recovery Mode pane, choose **System State** and click **Next**.</span></span> 

    ![Ricerca](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. <span data-ttu-id="68ae2-164">Nel calendario Ciao hello **seleziona Volume e data** punto riquadro, selezionare un ripristino.</span><span class="sxs-lookup"><span data-stu-id="68ae2-164">On hello Calendar in hello **Select Volume and Date** pane, select a recovery point.</span></span> <span data-ttu-id="68ae2-165">È possibile ripristinare da qualsiasi punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="68ae2-165">You can restore from any recovery point in time.</span></span> <span data-ttu-id="68ae2-166">Le date in **grassetto** indicare hello la disponibilità di almeno un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="68ae2-166">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="68ae2-167">Dopo aver selezionato una data, se sono disponibili più punti di ripristino, scegliere il punto di ripristino specifico di hello da hello **ora** dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="68ae2-167">Once  you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span> 

    ![Ricerca di elementi](./media/backup-azure-restore-system-state/select-date.png)

9. <span data-ttu-id="68ae2-169">Dopo aver scelto toorestore punto di ripristino hello, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="68ae2-169">Once you have chosen hello recovery point toorestore, click **Next**.</span></span>

10. <span data-ttu-id="68ae2-170">In hello **selezionare modalità di ripristino dello stato sistema** riquadro specificare hello destinazione in cui si desidera toobe ripristinati i file dello stato del sistema, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="68ae2-170">On hello **Select System State Recovery Mode** pane, specify hello destination where you want System State files toobe recovered, then click **Next**.</span></span>

    ![Crittografia](./media/backup-azure-restore-system-state/recover-as-files.png)

    <span data-ttu-id="68ae2-172">opzione Hello **crea copie in modo da mantenere entrambe le versioni**, crea le copie dei singoli file in un archivio di file di stato del sistema esistente anziché creare una copia di hello dell'intero archivio dello stato del sistema di hello.</span><span class="sxs-lookup"><span data-stu-id="68ae2-172">hello option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating hello copy of hello entire System State archive.</span></span>

11. <span data-ttu-id="68ae2-173">Verificare i dettagli di hello di ripristino nel riquadro di conferma hello e fare clic su **ripristinare**.</span><span class="sxs-lookup"><span data-stu-id="68ae2-173">Verify hello details of recovery on hello Confirmation pane, and click **Recover**.</span></span> 

    ![Fare clic su processo di ripristino hello tooconfirm pulsante Ripristina hello](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. <span data-ttu-id="68ae2-175">Hello copia *WindowsImageBackup* volume non critici tooa di directory di server hello (ad esempio d:\).</span><span class="sxs-lookup"><span data-stu-id="68ae2-175">Copy hello *WindowsImageBackup* directory tooa non-critical volume of hello server (for example D:\).</span></span> <span data-ttu-id="68ae2-176">Volume del sistema operativo Windows hello è in genere volume critico hello.</span><span class="sxs-lookup"><span data-stu-id="68ae2-176">Usually hello Windows OS volume is hello critical volume.</span></span>

13. <span data-ttu-id="68ae2-177">processo di ripristino hello toocomplete, sezione troppo seguente hello utilizzare[applicare i file di stato del sistema hello ripristinato in un Server Windows](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span><span class="sxs-lookup"><span data-stu-id="68ae2-177">toocomplete hello recovery process, use hello following section too[apply hello restored System State files on a Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span></span>




## <a name="apply-restored-system-state-on-a-windows-server"></a><span data-ttu-id="68ae2-178">Applicare lo stato del sistema ripristinato a un'istanza di Windows Server</span><span class="sxs-lookup"><span data-stu-id="68ae2-178">Apply restored System State on a Windows Server</span></span>

<span data-ttu-id="68ae2-179">Dopo aver ripristinato lo stato del sistema come file con l'agente di servizi di ripristino di Azure, utilizzare hello Windows Server Backup Utilità tooapply hello recuperato tooWindows dello stato del sistema Server.</span><span class="sxs-lookup"><span data-stu-id="68ae2-179">Once you have recovered System State as files using Azure Recovery Services Agent, use hello Windows Server Backup utility tooapply hello recovered System State tooWindows Server.</span></span> <span data-ttu-id="68ae2-180">Hello utilità di Windows Server Backup è già disponibile nel server di hello.</span><span class="sxs-lookup"><span data-stu-id="68ae2-180">hello Windows Server Backup utility is already available on hello server.</span></span> <span data-ttu-id="68ae2-181">Hello alla procedura seguente viene illustrato come tooapply hello ripristinato lo stato del sistema.</span><span class="sxs-lookup"><span data-stu-id="68ae2-181">hello following steps explain how tooapply hello recovered System State.</span></span>

1. <span data-ttu-id="68ae2-182">Seguente hello utilizzare comandi tooreboot server *modalità ripristino servizi Directory*.</span><span class="sxs-lookup"><span data-stu-id="68ae2-182">Use hello following commands tooreboot your server in *Directory Services Repair Mode*.</span></span> <span data-ttu-id="68ae2-183">In un prompt dei comandi con privilegi elevati:</span><span class="sxs-lookup"><span data-stu-id="68ae2-183">In an elevated command prompt:</span></span>

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. <span data-ttu-id="68ae2-184">Dopo il riavvio di hello, aprire lo snap-in Windows Server Backup hello.</span><span class="sxs-lookup"><span data-stu-id="68ae2-184">After hello reboot, open hello Windows Server Backup snap-in.</span></span> <span data-ttu-id="68ae2-185">Se non si conosce in hello snap-in è stato installato, eseguire la ricerca computer hello o un server per **Windows Server Backup**.</span><span class="sxs-lookup"><span data-stu-id="68ae2-185">If you don't know where hello snap-in was installed, search hello computer or server for **Windows Server Backup**.</span></span>

    <span data-ttu-id="68ae2-186">app desktop Hello viene visualizzato nei risultati della ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="68ae2-186">hello desktop app appears in hello search results.</span></span>

3. <span data-ttu-id="68ae2-187">Hello nello snap-in, selezionare **Backup locale**.</span><span class="sxs-lookup"><span data-stu-id="68ae2-187">In hello snap-in, select **Local Backup**.</span></span>

    ![Selezionare i Backup locale toorestore da qui](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. <span data-ttu-id="68ae2-189">Nella console di Backup locale hello in hello **riquadro azioni**, fare clic su **ripristinare** tooopen hello ripristino guidato.</span><span class="sxs-lookup"><span data-stu-id="68ae2-189">On hello Local Backup console, in hello **Actions Pane**, click **Recover** tooopen hello Recovery Wizard.</span></span>

5. <span data-ttu-id="68ae2-190">Selezionare l'opzione di hello, **un backup archiviato in un'altra posizione**, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="68ae2-190">Select hello option, **A backup stored in another location**, and click **Next**.</span></span>

   ![Scegliere toorecover tooa diversi server](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. <span data-ttu-id="68ae2-192">Quando si specifica il tipo di posizione hello, selezionare **cartella condivisa remota** se il backup dello stato del sistema è stato ripristinato tooanother server.</span><span class="sxs-lookup"><span data-stu-id="68ae2-192">When specifying hello location type, select **Remote shared folder** if your System State backup was recovered tooanother server.</span></span> <span data-ttu-id="68ae2-193">Se lo stato del sistema è stato ripristinato localmente, selezionare **Unità locali**.</span><span class="sxs-lookup"><span data-stu-id="68ae2-193">If your System State was recovered locally, then select **Local drives**.</span></span> 

    ![Selezionare se toorecovery dal server locale o in un altro](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. <span data-ttu-id="68ae2-195">Immettere hello percorso toohello *WindowsImageBackup* directory, oppure scegliere unità di hello locale contenente la directory (ad esempio, D:\WindowsImageBackup), ripristinata come parte del ripristino di file hello dello stato del sistema mediante il ripristino di Azure L'agente e fare clic su servizi **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="68ae2-195">Enter hello path toohello *WindowsImageBackup* directory, or choose hello local drive containing this directory (for example, D:\WindowsImageBackup), recovered as part of hello System State files recovery using Azure Recovery Services Agent and click **Next**.</span></span>

    ![percorso file condiviso toohello](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. <span data-ttu-id="68ae2-197">Versione di hello selezionare lo stato del sistema che desidera toorestore e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="68ae2-197">Select hello System State version that you want toorestore, and click **Next**.</span></span>

9. <span data-ttu-id="68ae2-198">Nel riquadro di selezione tipo di ripristino hello, selezionare **dello stato del sistema** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="68ae2-198">In hello Select Recovery Type pane, select **System State** and click **Next**.</span></span>

10. <span data-ttu-id="68ae2-199">Per la posizione di hello di hello ripristino dello stato del sistema, selezionare **nel percorso originale**, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="68ae2-199">For hello location of hello System State Recovery, select **Original Location**, and click **Next**.</span></span>

11. <span data-ttu-id="68ae2-200">Rivedere i dettagli di conferma hello, verificare le impostazioni di riavvio hello e fare clic su **ripristinare** tooapplly hello ripristino dei file di stato del sistema.</span><span class="sxs-lookup"><span data-stu-id="68ae2-200">Review hello confirmation details, verify hello reboot settings, and click **Recover** tooapplly hello restored System State files.</span></span>

    ![avvio hello ripristinare i file di stato del sistema](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a><span data-ttu-id="68ae2-202">Considerazioni speciali per il ripristino dello stato del sistema nel server di Active Directory</span><span class="sxs-lookup"><span data-stu-id="68ae2-202">Special considerations for System State recovery on Active Directory server</span></span>

<span data-ttu-id="68ae2-203">Il backup dello stato del sistema include i dati di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="68ae2-203">System State backup includes Active Directory data.</span></span> <span data-ttu-id="68ae2-204">Utilizzare hello seguendo i passaggi toorestore servizi di dominio Active Directory (AD DS) dallo stato tooa precedente stato corrente.</span><span class="sxs-lookup"><span data-stu-id="68ae2-204">Use hello following steps toorestore Active Directory Domain Service (AD DS) from its current state tooa previous state.</span></span>

1. <span data-ttu-id="68ae2-205">Riavviare il controller di dominio di hello in Directory Services in modalità ripristino.</span><span class="sxs-lookup"><span data-stu-id="68ae2-205">Restart hello domain controller in Directory Services Restore Mode (DSRM).</span></span>
2. <span data-ttu-id="68ae2-206">Seguire i passaggi di hello [qui](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toorecover i cmdlet di Windows Server Backup toouse di dominio Active Directory.</span><span class="sxs-lookup"><span data-stu-id="68ae2-206">Follow hello steps [here](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toouse Windows Server Backup cmdlets toorecover AD DS.</span></span>


## <a name="troubleshoot-failed-system-state-restore"></a><span data-ttu-id="68ae2-207">Risolvere i problemi relativi a un ripristino non riuscito dello stato del sistema</span><span class="sxs-lookup"><span data-stu-id="68ae2-207">Troubleshoot failed System State restore</span></span>

<span data-ttu-id="68ae2-208">Se il processo precedente di hello dell'applicazione dello stato del sistema non viene completata correttamente, utilizzare hello ambiente ripristino (Win) toorecover di Windows Server.</span><span class="sxs-lookup"><span data-stu-id="68ae2-208">If hello previous process of applying System State does not complete successfully, use hello Windows Recovery Environment (Win RE) toorecover your Windows Server.</span></span> <span data-ttu-id="68ae2-209">Hello passaggi seguenti illustrano come toorecover tramite ambiente ripristino Windows.</span><span class="sxs-lookup"><span data-stu-id="68ae2-209">hello following steps explain how toorecover using Win RE.</span></span> <span data-ttu-id="68ae2-210">Usare questa opzione solo se Windows Server non viene avviato normalmente dopo un ripristino dello stato del sistema.</span><span class="sxs-lookup"><span data-stu-id="68ae2-210">Use This option only if Windows Server does not boot normally after a System State restore.</span></span> <span data-ttu-id="68ae2-211">processo Hello Cancella i dati non di sistema, prestare attenzione.</span><span class="sxs-lookup"><span data-stu-id="68ae2-211">hello following process erases non-system data, use caution.</span></span> 

1. <span data-ttu-id="68ae2-212">Avvio di Windows Server in ambiente ripristino (Win) hello.</span><span class="sxs-lookup"><span data-stu-id="68ae2-212">Boot your Windows Server into hello Windows Recovery Environment (Win RE).</span></span>

2. <span data-ttu-id="68ae2-213">Selezionare hello disponibili tre opzioni di risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="68ae2-213">Select Troubleshoot from hello three available options.</span></span>

    ![Menu iniziale](./media/backup-azure-restore-system-state/winre-1.png)

3. <span data-ttu-id="68ae2-215">Da hello **opzioni avanzate** selezionare **prompt dei comandi** e fornire nome utente amministratore di server hello e una password.</span><span class="sxs-lookup"><span data-stu-id="68ae2-215">From hello **Advanced Options** screen, select **Command Prompt** and provide hello server administrator username and password.</span></span>

   ![Menu iniziale](./media/backup-azure-restore-system-state/winre-2.png)

4. <span data-ttu-id="68ae2-217">Specificare nome utente amministratore di server hello e la password.</span><span class="sxs-lookup"><span data-stu-id="68ae2-217">Provide hello server administrator username and password.</span></span>

    ![Menu iniziale](./media/backup-azure-restore-system-state/winre-3.png)

5. <span data-ttu-id="68ae2-219">Quando si apre il prompt di comandi hello in modalità amministratore, eseguire versioni dello stato del sistema di hello tooget comando backup successivo.</span><span class="sxs-lookup"><span data-stu-id="68ae2-219">When you open hello command prompt in administrator mode, run following command tooget hello System State backup versions.</span></span>

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![Ottenere le versioni del backup dello stato del sistema](./media/backup-azure-restore-system-state/winre-4.png)

6. <span data-ttu-id="68ae2-221">Eseguire hello successivo comando tooget tutti i volumi nel backup hello.</span><span class="sxs-lookup"><span data-stu-id="68ae2-221">Run hello following command tooget all volumes available in hello backup.</span></span>

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![Ottenere le versioni del backup dello stato del sistema](./media/backup-azure-restore-system-state/winre-5.png)

7. <span data-ttu-id="68ae2-223">Hello comando che segue recupera tutti i volumi che fanno parte di hello Backup dello stato del sistema.</span><span class="sxs-lookup"><span data-stu-id="68ae2-223">hello following command recovers all volumes that are part of hello System State Backup.</span></span> <span data-ttu-id="68ae2-224">Si noti che questo passaggio consente di ripristinare solo hello volumi critici che fanno parte dello stato del sistema hello.</span><span class="sxs-lookup"><span data-stu-id="68ae2-224">Note that this step recovers only hello critical volumes that are part of hello System State.</span></span> <span data-ttu-id="68ae2-225">Tutti i dati non di sistema vengono cancellati.</span><span class="sxs-lookup"><span data-stu-id="68ae2-225">All non-System data is erased.</span></span>

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![Ottenere le versioni del backup dello stato del sistema](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a><span data-ttu-id="68ae2-227">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="68ae2-227">Next steps</span></span>
* <span data-ttu-id="68ae2-228">Dopo aver ripristinato i file e le cartelle, è possibile [gestire i backup](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="68ae2-228">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
