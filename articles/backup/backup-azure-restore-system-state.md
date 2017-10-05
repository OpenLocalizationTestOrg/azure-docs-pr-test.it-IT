---
title: 'Backup di Azure: Ripristinare lo stato del sistema per Windows Server | Microsoft Docs'
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
ms.openlocfilehash: 320c85f8045d9b72cf7f430d2e2736ba8e5ec269
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="restore-system-state-to-windows-server"></a><span data-ttu-id="484bc-103">Ripristinare lo stato del sistema per Windows Server</span><span class="sxs-lookup"><span data-stu-id="484bc-103">Restore System State to Windows Server</span></span>

<span data-ttu-id="484bc-104">Questo articolo illustra come ripristinare i backup dello stato del sistema di Windows Server da un insieme di credenziali di Servizi di ripristino di Azure.</span><span class="sxs-lookup"><span data-stu-id="484bc-104">This article explains how to restore Windows Server System State backups from an Azure Recovery Services vault.</span></span> <span data-ttu-id="484bc-105">Per ripristinare lo stato del sistema, è necessario avere un backup dello stato del sistema, creato usando le istruzioni disponibili in [Eseguire il backup dello stato del sistema](backup-azure-system-state.md#back-up-windows-server-system-state-preview), e assicurarsi di avere installato la [versione più recente dell'agente dei Servizi di ripristino di Microsoft Azure](http://aka.ms/azurebackup_agent).</span><span class="sxs-lookup"><span data-stu-id="484bc-105">To restore System State, you must have a System State backup (created using the instructions in [Back up System State](backup-azure-system-state.md#back-up-windows-server-system-state-preview)), and make sure you have installed the [latest version of the Microsoft Azure Recovery Services (MARS) agent](http://aka.ms/azurebackup_agent).</span></span> <span data-ttu-id="484bc-106">Il ripristino dei dati dello stato del sistema di Windows Server da un insieme di credenziali di Servizi di ripristino di Azure è un processo in due passaggi:</span><span class="sxs-lookup"><span data-stu-id="484bc-106">Recovering Windows Server System State data from an Azure Recovery Services vault is a two-step process:</span></span>

1. <span data-ttu-id="484bc-107">Ripristinare lo stato del sistema sotto forma di file da Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="484bc-107">Restore System State as files from Azure Backup.</span></span> <span data-ttu-id="484bc-108">Quando si ripristina lo stato del sistema sotto forma di file da Backup di Azure, è possibile eseguire una di queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="484bc-108">When restoring System State as files from Azure Backup, you can either:</span></span>
  * <span data-ttu-id="484bc-109">Ripristinare lo stato del sistema nello stesso server in cui è stato creato il backup.</span><span class="sxs-lookup"><span data-stu-id="484bc-109">Restore System State to the same server where the backups were taken, or</span></span>
  * <span data-ttu-id="484bc-110">Ripristinare il file dello stato del sistema in un server alternativo.</span><span class="sxs-lookup"><span data-stu-id="484bc-110">Restore System State file to an alternate server.</span></span>

2. <span data-ttu-id="484bc-111">Applicare i file dello stato del sistema ripristinato in un'istanza di Windows Server.</span><span class="sxs-lookup"><span data-stu-id="484bc-111">Apply the restored System State files to a Windows Server.</span></span>


## <a name="recover-system-state-files-to-the-same-server"></a><span data-ttu-id="484bc-112">Ripristinare i file dello stato del sistema nello stesso server</span><span class="sxs-lookup"><span data-stu-id="484bc-112">Recover System State files to the same server</span></span>
<span data-ttu-id="484bc-113">La procedura seguente illustra come eseguire il rollback della configurazione di Windows Server a uno stato precedente.</span><span class="sxs-lookup"><span data-stu-id="484bc-113">The following steps explain how to roll back your Windows Server configuration to a previous state.</span></span> <span data-ttu-id="484bc-114">Il rollback della configurazione del server a uno stato noto e stabile può essere estremamente utile.</span><span class="sxs-lookup"><span data-stu-id="484bc-114">Rolling your server configuration back to a known, stable state, can be extremely valuable.</span></span> <span data-ttu-id="484bc-115">La procedura seguente consente di ripristinare lo stato del sistema del server da un insieme di credenziali dei Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="484bc-115">The following steps restore the server's System State from a Recovery Services vault.</span></span> 

1. <span data-ttu-id="484bc-116">Aprire lo snap-in di **Backup di Microsoft Azure** .</span><span class="sxs-lookup"><span data-stu-id="484bc-116">Open the **Microsoft Azure Backup** snap-in.</span></span> <span data-ttu-id="484bc-117">Se non si sa dove è stato installato lo snap-in, cercare **Backup di Microsoft Azure** nel computer o nel server.</span><span class="sxs-lookup"><span data-stu-id="484bc-117">If you don't know where the snap-in was installed, search the computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="484bc-118">L'applicazione desktop dovrebbe essere visualizzata nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="484bc-118">The desktop app should appear in the search results.</span></span>

2. <span data-ttu-id="484bc-119">Fare clic su **Ripristina dati** per avviare la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="484bc-119">Click **Recover Data** to start the wizard.</span></span>

    ![Ripristina dati](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="484bc-121">Nel riquadro **Guida introduttiva** selezionare l'opzione **This server (Questo server) (`<server name>`)** e fare clic su **Avanti** per ripristinare i dati nello stesso server o computer.</span><span class="sxs-lookup"><span data-stu-id="484bc-121">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Scegliere l'opzione This server (Questo server) per ripristinare i dati nello stesso computer](./media/backup-azure-restore-system-state/samemachine.png)

4. <span data-ttu-id="484bc-123">Nel riquadro **Seleziona modalità di ripristino** scegliere **Stato del sistema** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="484bc-123">On the **Select Recovery Mode** pane, choose **System State** and then click **Next**.</span></span>

    ![Ricerca dei file](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. <span data-ttu-id="484bc-125">Nel calendario del riquadro **Seleziona volume e data** selezionare un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="484bc-125">On the calendar in **Select Volume and Date** pane, select a recovery point.</span></span> 

    <span data-ttu-id="484bc-126">È possibile ripristinare da qualsiasi punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="484bc-126">You can restore from any recovery point in time.</span></span> <span data-ttu-id="484bc-127">Le date in **grassetto** indicano la disponibilità di almeno un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="484bc-127">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="484bc-128">Dopo aver selezionato una data, se sono disponibili più punti di ripristino, scegliere quello appropriato dall'elenco a discesa **Ora**.</span><span class="sxs-lookup"><span data-stu-id="484bc-128">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Volume e dati](./media/backup-azure-restore-system-state/select-date.png)

6. <span data-ttu-id="484bc-130">Dopo aver selezionato il punto di ripristino, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="484bc-130">Once you have chosen the recovery point to restore, click **Next**.</span></span>

    <span data-ttu-id="484bc-131">Backup di Azure monta il punto di ripristino locale e lo usa come volume di ripristino.</span><span class="sxs-lookup"><span data-stu-id="484bc-131">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="484bc-132">Nel riquadro successivo specificare la destinazione per i file ripristinati dello stato del sistema e quindi fare clic su **Sfoglia** per aprire Esplora risorse e trovare i file e le cartelle necessari.</span><span class="sxs-lookup"><span data-stu-id="484bc-132">On the next pane, specify the destination for the recovered System State files and click **Browse** to open Windows Explorer and find the files and folders you want.</span></span> <span data-ttu-id="484bc-133">L'opzione **Crea copie in modo da mantenere entrambe le versioni** crea copie dei singoli file in un archivio di file dello stato del sistema esistente invece di creare la copia dell'intero archivio dello stato del sistema.</span><span class="sxs-lookup"><span data-stu-id="484bc-133">The option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating the copy of the entire System State archive.</span></span>

    ![Opzioni di ripristino](./media/backup-azure-restore-system-state/recover-as-files.png)

8. <span data-ttu-id="484bc-135">Verificare i dettagli relativi al ripristino nel riquadro **Conferma** e fare clic su **Ripristina**.</span><span class="sxs-lookup"><span data-stu-id="484bc-135">Verify the details of recovery on the **Confirmation** pane and click **Recover**.</span></span>

   ![Fare clic su Ripristina per confermare l'azione di ripristino](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. <span data-ttu-id="484bc-137">Copiare la directory *WindowsImageBackup* nella destinazione di ripristino in un volume non critico del server.</span><span class="sxs-lookup"><span data-stu-id="484bc-137">Copy the *WindowsImageBackup* directory in the Recovery destination to a non-critical volume of the server.</span></span> <span data-ttu-id="484bc-138">Il volume del sistema operativo Windows è in genere il volume critico.</span><span class="sxs-lookup"><span data-stu-id="484bc-138">Usually, the Windows OS volume is the critical volume.</span></span>

10. <span data-ttu-id="484bc-139">Al termine del ripristino, seguire la procedura illustrata nella sezione [Applicare i file ripristinati dello stato del sistema a Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server) per completare il processo di ripristino dello stato del sistema.</span><span class="sxs-lookup"><span data-stu-id="484bc-139">Once the recovery is successful, follow the steps in the section, [Apply restored System State files to the Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), to complete the System State recovery process.</span></span>

## <a name="recover-system-state-files-to-an-alternate-server"></a><span data-ttu-id="484bc-140">Ripristinare il file dello stato del sistema in un server alternativo</span><span class="sxs-lookup"><span data-stu-id="484bc-140">Recover System State files to an alternate server</span></span>

<span data-ttu-id="484bc-141">Se l'istanza di Windows Server è danneggiata o inaccessibile e si vuole ripristinarne uno stato stabile eseguendo il ripristino dello stato del sistema di Windows Server, è possibile ripristinare lo stato del sistema del server danneggiato da un altro server.</span><span class="sxs-lookup"><span data-stu-id="484bc-141">If your Windows Server is corrupted or inaccessible, and you want to restore it to a stable state by recovering the Windows Server System State, you can restore the corrupted server's System State from another server.</span></span> <span data-ttu-id="484bc-142">Seguire questa procedura per ripristinare lo stato del sistema in un server separato.</span><span class="sxs-lookup"><span data-stu-id="484bc-142">Use the following steps to the restore System State on a separate server.</span></span>  

<span data-ttu-id="484bc-143">Include la terminologia utilizzata in questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="484bc-143">The terminology used in these steps includes:</span></span>

- <span data-ttu-id="484bc-144">*Computer di origine* : il computer di origine da cui è stato eseguito il backup e che non è attualmente disponibile.</span><span class="sxs-lookup"><span data-stu-id="484bc-144">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
- <span data-ttu-id="484bc-145">*Computer di destinazione* : il computer in cui i dati vengono ripristinati.</span><span class="sxs-lookup"><span data-stu-id="484bc-145">*Target machine* – The machine to which the data is being recovered.</span></span>
- <span data-ttu-id="484bc-146">*Insieme di credenziali di esempio*: l'insieme di credenziali dei servizi di ripristino in cui il *computer di origine* e il *computer di destinazione* sono registrati.</span><span class="sxs-lookup"><span data-stu-id="484bc-146">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="484bc-147">I backup eseguiti da un computer non possono essere ripristinati in un computer che esegue una versione precedente del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="484bc-147">Backups taken from one machine cannot be restored to a machine running an earlier version of the operating system.</span></span> <span data-ttu-id="484bc-148">Ad esempio, i backup eseguiti da un computer con Windows Server 2016 non possono essere ripristinati in Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="484bc-148">For example, backups taken from a Windows Server 2016 machine can't be restored to Windows Server 2012 R2.</span></span> <span data-ttu-id="484bc-149">È tuttavia possibile eseguire l'operazione inversa.</span><span class="sxs-lookup"><span data-stu-id="484bc-149">However, the inverse is possible.</span></span> <span data-ttu-id="484bc-150">È possibile usare i backup da Windows Server 2012 R2 per ripristinare Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="484bc-150">You can use backups from Windows Server 2012 R2 to restore Windows Server 2016.</span></span>
>

1. <span data-ttu-id="484bc-151">Aprire lo snap-in di **Backup di Microsoft Azure** nel *Computer di destinazione*.</span><span class="sxs-lookup"><span data-stu-id="484bc-151">Open the **Microsoft Azure Backup** snap-in on the *Target machine*.</span></span>
2. <span data-ttu-id="484bc-152">Assicurarsi che il *computer di destinazione* e il *computer di origine* siano registrati nello stesso insieme di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="484bc-152">Ensure that the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span></span>
3. <span data-ttu-id="484bc-153">Fare clic su **Ripristina dati** per avviare il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="484bc-153">Click **Recover Data** to initiate the workflow.</span></span>

    ![Ripristina dati](./media/backup-azure-restore-windows-server-classic/recover.png)

4. <span data-ttu-id="484bc-155">Selezionare **Un altro server**</span><span class="sxs-lookup"><span data-stu-id="484bc-155">Select **Another server**</span></span>

    ![Un altro server](./media/backup-azure-restore-system-state/anotherserver.png)

5. <span data-ttu-id="484bc-157">Specificare il file dell'insieme di credenziali che corrisponde all' *Insieme di credenziali di esempio*.</span><span class="sxs-lookup"><span data-stu-id="484bc-157">Provide the vault credential file that corresponds to the *Sample vault*.</span></span> <span data-ttu-id="484bc-158">Se il file dell'insieme di credenziali non è valido (o è scaduto), è necessario scaricarne uno nuovo dall'*insieme di credenziali di esempio* nel Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="484bc-158">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span></span> <span data-ttu-id="484bc-159">Dopo aver specificato il file dell'insieme di credenziali, viene visualizzato l'insieme di credenziali di Servizi di ripristino associato al file di credenziali dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="484bc-159">Once the vault credential file is provided, the Recovery Services vault associated with the vault credential file appears.</span></span>

6. <span data-ttu-id="484bc-160">Nel riquadro Seleziona server di backup selezionare il *computer di origine* dall'elenco di computer visualizzati.</span><span class="sxs-lookup"><span data-stu-id="484bc-160">On the Select Backup Server pane, select the *Source machine* from the list of displayed machines.</span></span>

    ![Elenco di computer](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. <span data-ttu-id="484bc-162">Nel riquadro Seleziona modalità di ripristino scegliere **Stato del sistema** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="484bc-162">On the Select Recovery Mode pane, choose **System State** and click **Next**.</span></span> 

    ![Search](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. <span data-ttu-id="484bc-164">Nel riquadro **Seleziona volume e data** del Calendario selezionare un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="484bc-164">On the Calendar in the **Select Volume and Date** pane, select a recovery point.</span></span> <span data-ttu-id="484bc-165">È possibile ripristinare da qualsiasi punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="484bc-165">You can restore from any recovery point in time.</span></span> <span data-ttu-id="484bc-166">Le date in **grassetto** indicano la disponibilità di almeno un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="484bc-166">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="484bc-167">Dopo aver selezionato una data, se sono disponibili più punti di ripristino, scegliere quello appropriato dal menu a discesa **Ora**.</span><span class="sxs-lookup"><span data-stu-id="484bc-167">Once  you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span> 

    ![Ricerca di elementi](./media/backup-azure-restore-system-state/select-date.png)

9. <span data-ttu-id="484bc-169">Dopo aver selezionato il punto di ripristino, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="484bc-169">Once you have chosen the recovery point to restore, click **Next**.</span></span>

10. <span data-ttu-id="484bc-170">Nel riquadro **Selezionare la modalità di ripristino dello stato del sistema** specificare la destinazione per il ripristino dei file dello stato del sistema, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="484bc-170">On the **Select System State Recovery Mode** pane, specify the destination where you want System State files to be recovered, then click **Next**.</span></span>

    ![Crittografia](./media/backup-azure-restore-system-state/recover-as-files.png)

    <span data-ttu-id="484bc-172">L'opzione **Crea copie in modo da mantenere entrambe le versioni** crea copie dei singoli file in un archivio di file dello stato del sistema esistente invece di creare la copia dell'intero archivio dello stato del sistema.</span><span class="sxs-lookup"><span data-stu-id="484bc-172">The option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating the copy of the entire System State archive.</span></span>

11. <span data-ttu-id="484bc-173">Verificare i dettagli relativi al ripristino nel riquadro Conferma e fare clic su **Ripristina**.</span><span class="sxs-lookup"><span data-stu-id="484bc-173">Verify the details of recovery on the Confirmation pane, and click **Recover**.</span></span> 

    ![Fare clic sul pulsante Ripristina per confermare il processo di ripristino](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. <span data-ttu-id="484bc-175">Copiare la directory *WindowsImageBackup* in un volume non critico del server, ad esempio D:\).</span><span class="sxs-lookup"><span data-stu-id="484bc-175">Copy the *WindowsImageBackup* directory to a non-critical volume of the server (for example D:\).</span></span> <span data-ttu-id="484bc-176">Il volume del sistema operativo Windows è in genere il volume critico.</span><span class="sxs-lookup"><span data-stu-id="484bc-176">Usually the Windows OS volume is the critical volume.</span></span>

13. <span data-ttu-id="484bc-177">Per completare il processo di ripristino, usare la sezione seguente per [applicare i file ripristinati dello stato del sistema a un'istanza di Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span><span class="sxs-lookup"><span data-stu-id="484bc-177">To complete the recovery process, use the following section to [apply the restored System State files on a Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span></span>




## <a name="apply-restored-system-state-on-a-windows-server"></a><span data-ttu-id="484bc-178">Applicare lo stato del sistema ripristinato a un'istanza di Windows Server</span><span class="sxs-lookup"><span data-stu-id="484bc-178">Apply restored System State on a Windows Server</span></span>

<span data-ttu-id="484bc-179">Dopo avere ripristinato lo stato del sistema sotto forma di file tramite l'agente dei Servizi di ripristino di Microsoft Azure, usare l'utilità Windows Server Backup per applicare lo stato del sistema ripristinato a un'istanza di Windows Server.</span><span class="sxs-lookup"><span data-stu-id="484bc-179">Once you have recovered System State as files using Azure Recovery Services Agent, use the Windows Server Backup utility to apply the recovered System State to Windows Server.</span></span> <span data-ttu-id="484bc-180">L'utilità Windows Server Backup è già disponibile nel server.</span><span class="sxs-lookup"><span data-stu-id="484bc-180">The Windows Server Backup utility is already available on the server.</span></span> <span data-ttu-id="484bc-181">La procedura seguente illustra come applicare lo stato del sistema ripristinato.</span><span class="sxs-lookup"><span data-stu-id="484bc-181">The following steps explain how to apply the recovered System State.</span></span>

1. <span data-ttu-id="484bc-182">Usare i comandi seguenti per riavviare il server in *Modalità di ripristino dei servizi directory*.</span><span class="sxs-lookup"><span data-stu-id="484bc-182">Use the following commands to reboot your server in *Directory Services Repair Mode*.</span></span> <span data-ttu-id="484bc-183">In un prompt dei comandi con privilegi elevati:</span><span class="sxs-lookup"><span data-stu-id="484bc-183">In an elevated command prompt:</span></span>

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. <span data-ttu-id="484bc-184">Dopo il riavvio aprire lo snap-in Windows Server Backup.</span><span class="sxs-lookup"><span data-stu-id="484bc-184">After the reboot, open the Windows Server Backup snap-in.</span></span> <span data-ttu-id="484bc-185">Se non si conosce il percorso di installazione dello snap-in, cercare **Windows Server Backup** nel computer o nel server.</span><span class="sxs-lookup"><span data-stu-id="484bc-185">If you don't know where the snap-in was installed, search the computer or server for **Windows Server Backup**.</span></span>

    <span data-ttu-id="484bc-186">L'applicazione desktop viene visualizzata nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="484bc-186">The desktop app appears in the search results.</span></span>

3. <span data-ttu-id="484bc-187">Nello snap-in selezionare **Backup locale**.</span><span class="sxs-lookup"><span data-stu-id="484bc-187">In the snap-in, select **Local Backup**.</span></span>

    ![Selezionare Backup locale per eseguire il ripristino da tale posizione](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. <span data-ttu-id="484bc-189">Nel **riquadro Azioni** della console Backup locale fare clic su **Ripristina** per aprire il Ripristino guidato.</span><span class="sxs-lookup"><span data-stu-id="484bc-189">On the Local Backup console, in the **Actions Pane**, click **Recover** to open the Recovery Wizard.</span></span>

5. <span data-ttu-id="484bc-190">Selezionare l'opzione **Backup archiviato in un altro percorso** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="484bc-190">Select the option, **A backup stored in another location**, and click **Next**.</span></span>

   ![Scegliere il ripristino in un server diverso](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. <span data-ttu-id="484bc-192">Quando si specifica il tipo di posizione, selezionare **Cartella condivisa remota** se il backup dello stato del sistema è stato ripristinato in un altro server.</span><span class="sxs-lookup"><span data-stu-id="484bc-192">When specifying the location type, select **Remote shared folder** if your System State backup was recovered to another server.</span></span> <span data-ttu-id="484bc-193">Se lo stato del sistema è stato ripristinato localmente, selezionare **Unità locali**.</span><span class="sxs-lookup"><span data-stu-id="484bc-193">If your System State was recovered locally, then select **Local drives**.</span></span> 

    ![Specificare se eseguire il ripristino da un server locale o da un altro server](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. <span data-ttu-id="484bc-195">Immettere il percorso della directory *WindowsImageBackup* oppure scegliere l'unità locale contenente questa directory, ad esempio D:\WindowsImageBackup, ripristinata come parte del ripristino dei file dello stato del sistema tramite l'agente dei Servizi di ripristino di Azure Recovery e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="484bc-195">Enter the path to the *WindowsImageBackup* directory, or choose the local drive containing this directory (for example, D:\WindowsImageBackup), recovered as part of the System State files recovery using Azure Recovery Services Agent and click **Next**.</span></span>

    ![Percorso del file condiviso](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. <span data-ttu-id="484bc-197">Selezionare la versione dello stato del sistema da ripristinare, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="484bc-197">Select the System State version that you want to restore, and click **Next**.</span></span>

9. <span data-ttu-id="484bc-198">Nel riquadro Seleziona tipo di ripristino selezionare**Stato del sistema** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="484bc-198">In the Select Recovery Type pane, select **System State** and click **Next**.</span></span>

10. <span data-ttu-id="484bc-199">Come percorso del ripristino dello stato del sistema selezionare **Percorso originale** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="484bc-199">For the location of the System State Recovery, select **Original Location**, and click **Next**.</span></span>

11. <span data-ttu-id="484bc-200">Verificare i dettagli della conferma e le impostazioni di riavvio, quindi fare clic su **Ripristina** per applicare i file ripristinati dello stato del sistema.</span><span class="sxs-lookup"><span data-stu-id="484bc-200">Review the confirmation details, verify the reboot settings, and click **Recover** to applly the restored System State files.</span></span>

    ![Avviare il ripristino dei file dello stato del sistema](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a><span data-ttu-id="484bc-202">Considerazioni speciali per il ripristino dello stato del sistema nel server di Active Directory</span><span class="sxs-lookup"><span data-stu-id="484bc-202">Special considerations for System State recovery on Active Directory server</span></span>

<span data-ttu-id="484bc-203">Il backup dello stato del sistema include i dati di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="484bc-203">System State backup includes Active Directory data.</span></span> <span data-ttu-id="484bc-204">Seguire questa procedura per ripristinare Active Directory Domain Service (AD DS) dallo stato corrente a uno stato precedente.</span><span class="sxs-lookup"><span data-stu-id="484bc-204">Use the following steps to restore Active Directory Domain Service (AD DS) from its current state to a previous state.</span></span>

1. <span data-ttu-id="484bc-205">Riavviare il controller di dominio in Modalità ripristino servizi directory.</span><span class="sxs-lookup"><span data-stu-id="484bc-205">Restart the domain controller in Directory Services Restore Mode (DSRM).</span></span>
2. <span data-ttu-id="484bc-206">Seguire [questa procedura](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) per usare i cmdlet di Windows Server Backup per ripristinare AD DS.</span><span class="sxs-lookup"><span data-stu-id="484bc-206">Follow the steps [here](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) to use Windows Server Backup cmdlets to recover AD DS.</span></span>


## <a name="troubleshoot-failed-system-state-restore"></a><span data-ttu-id="484bc-207">Risolvere i problemi relativi a un ripristino non riuscito dello stato del sistema</span><span class="sxs-lookup"><span data-stu-id="484bc-207">Troubleshoot failed System State restore</span></span>

<span data-ttu-id="484bc-208">Se il processo precedente di applicazione dello stato del sistema non viene completato correttamente, usare Ambiente ripristino Windows per ripristinare l'istanza di Windows Server.</span><span class="sxs-lookup"><span data-stu-id="484bc-208">If the previous process of applying System State does not complete successfully, use the Windows Recovery Environment (Win RE) to recover your Windows Server.</span></span> <span data-ttu-id="484bc-209">La procedura seguente illustra come eseguire il ripristino con Ambiente ripristino Windows.</span><span class="sxs-lookup"><span data-stu-id="484bc-209">The following steps explain how to recover using Win RE.</span></span> <span data-ttu-id="484bc-210">Usare questa opzione solo se Windows Server non viene avviato normalmente dopo un ripristino dello stato del sistema.</span><span class="sxs-lookup"><span data-stu-id="484bc-210">Use This option only if Windows Server does not boot normally after a System State restore.</span></span> <span data-ttu-id="484bc-211">Il processo seguente cancella i dati non di sistema, quindi occorre eseguirlo con cautela.</span><span class="sxs-lookup"><span data-stu-id="484bc-211">The following process erases non-system data, use caution.</span></span> 

1. <span data-ttu-id="484bc-212">Avviare l'istanza di Windows Server in Ambiente ripristino Windows.</span><span class="sxs-lookup"><span data-stu-id="484bc-212">Boot your Windows Server into the Windows Recovery Environment (Win RE).</span></span>

2. <span data-ttu-id="484bc-213">Selezionare una delle opzioni disponibili per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="484bc-213">Select Troubleshoot from the three available options.</span></span>

    ![Menu iniziale](./media/backup-azure-restore-system-state/winre-1.png)

3. <span data-ttu-id="484bc-215">Dalla schermata **Opzioni avanzate** selezionare **Prompt dei comandi** e specificare il nome utente e la password dell'amministratore del server.</span><span class="sxs-lookup"><span data-stu-id="484bc-215">From the **Advanced Options** screen, select **Command Prompt** and provide the server administrator username and password.</span></span>

   ![Menu iniziale](./media/backup-azure-restore-system-state/winre-2.png)

4. <span data-ttu-id="484bc-217">Specificare il nome utente e la password dell'amministratore del server.</span><span class="sxs-lookup"><span data-stu-id="484bc-217">Provide the server administrator username and password.</span></span>

    ![Menu iniziale](./media/backup-azure-restore-system-state/winre-3.png)

5. <span data-ttu-id="484bc-219">Quando si apre il prompt dei comandi in modalità Amministratore, eseguire questo comando per ottenere le versioni del backup dello stato del sistema.</span><span class="sxs-lookup"><span data-stu-id="484bc-219">When you open the command prompt in administrator mode, run following command to get the System State backup versions.</span></span>

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![Ottenere le versioni del backup dello stato del sistema](./media/backup-azure-restore-system-state/winre-4.png)

6. <span data-ttu-id="484bc-221">Eseguire il comando seguente per ottenere tutti i volumi disponibili nel backup.</span><span class="sxs-lookup"><span data-stu-id="484bc-221">Run the following command to get all volumes available in the backup.</span></span>

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![Ottenere le versioni del backup dello stato del sistema](./media/backup-azure-restore-system-state/winre-5.png)

7. <span data-ttu-id="484bc-223">Il comando seguente ripristina tutti i volumi che fanno parte del backup dello stato del sistema.</span><span class="sxs-lookup"><span data-stu-id="484bc-223">The following command recovers all volumes that are part of the System State Backup.</span></span> <span data-ttu-id="484bc-224">Si noti che questo passaggio ripristina solo i volumi critici che fanno parte dello stato del sistema.</span><span class="sxs-lookup"><span data-stu-id="484bc-224">Note that this step recovers only the critical volumes that are part of the System State.</span></span> <span data-ttu-id="484bc-225">Tutti i dati non di sistema vengono cancellati.</span><span class="sxs-lookup"><span data-stu-id="484bc-225">All non-System data is erased.</span></span>

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![Ottenere le versioni del backup dello stato del sistema](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a><span data-ttu-id="484bc-227">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="484bc-227">Next steps</span></span>
* <span data-ttu-id="484bc-228">Dopo aver ripristinato i file e le cartelle, è possibile [gestire i backup](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="484bc-228">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
