---
title: Creare e ripristinare un backup in Servizi BizTalk | Documentazione Microsoft
description: "I Servizi BizTalk includono funzionalità di backup e ripristino. Informazioni su come creare e ripristinare un backup e determinare gli elementi di cui eseguire il backup. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 59f91173-4683-48df-abd5-41262bfce6df
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c55d1ab124441c42101b4ad60924a9ea28231408
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-backup-and-restore"></a><span data-ttu-id="ced12-105">Servizi BizTalk: backup e ripristino</span><span class="sxs-lookup"><span data-stu-id="ced12-105">BizTalk Services: Backup and Restore</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="ced12-106">I Servizi BizTalk di Azure includono funzioni di backup e ripristino.</span><span class="sxs-lookup"><span data-stu-id="ced12-106">Azure BizTalk Services includes Backup and Restore capabilities.</span></span> <span data-ttu-id="ced12-107">Questo argomento descrive come eseguire il backup e il ripristino dei Servizi BizTalk usando il portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="ced12-107">This topic describes how to backup and restore BizTalk Services using the Azure classic portal.</span></span>

<span data-ttu-id="ced12-108">È anche possibile eseguire il backup dei Servizi BizTalk mediante l' [API REST](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span><span class="sxs-lookup"><span data-stu-id="ced12-108">You can also back up BizTalk Services using the [BizTalk Services REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span></span> 

> [!NOTE]
> <span data-ttu-id="ced12-109">Il backup delle connessioni ibride NON viene eseguito, indipendentemente dall'edizione.</span><span class="sxs-lookup"><span data-stu-id="ced12-109">Hybrid Connections are NOT backed up, regardless of the Edition.</span></span> <span data-ttu-id="ced12-110">È necessario ricreare le connessioni ibride.</span><span class="sxs-lookup"><span data-stu-id="ced12-110">You must recreate your hybrid connections.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="ced12-111">Operazioni preliminari</span><span class="sxs-lookup"><span data-stu-id="ced12-111">Before you Begin</span></span>
* <span data-ttu-id="ced12-112">Le funzionalità di backup e ripristino potrebbero non essere disponibili per tutte le edizioni.</span><span class="sxs-lookup"><span data-stu-id="ced12-112">Backup and Restore may not be available for all editions.</span></span> <span data-ttu-id="ced12-113">Vedere [Servizi BizTalk: Grafico edizioni](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="ced12-113">See [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>
* <span data-ttu-id="ced12-114">Tramite il portale di Azure classico è possibile creare un backup su richiesta o backup pianificati.</span><span class="sxs-lookup"><span data-stu-id="ced12-114">Using the Azure classic portal, you can create an On Demand backup or create a scheduled backup.</span></span> 
* <span data-ttu-id="ced12-115">È possibile ripristinare il contenuto del backup nello stesso servizio BizTalk oppure in nuovo Servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="ced12-115">Backup content can be restored to the same BizTalk Service or to a new BizTalk Service.</span></span> <span data-ttu-id="ced12-116">Per ripristinare il Servizio BizTalk usando lo stesso nome è necessario eliminare il Servizio BizTalk esistente e il nome deve essere disponibile.</span><span class="sxs-lookup"><span data-stu-id="ced12-116">To restore the BizTalk Service using the same name, the existing BizTalk Service must be deleted and the name must be available.</span></span> <span data-ttu-id="ced12-117">Dopo aver eliminato un Servizio BizTalk, potrebbe essere necessario un certo periodo di tempo affinché lo stesso nome sia disponibile.</span><span class="sxs-lookup"><span data-stu-id="ced12-117">After you delete a BizTalk Service, it can take longer time than wanted for the same name to be available.</span></span> <span data-ttu-id="ced12-118">Se non è possibile attendere che lo stesso nome sia disponibile, ripristinare un nuovo Servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="ced12-118">If you cannot wait for the same name to be available, then restore to a new BizTalk Service.</span></span>
* <span data-ttu-id="ced12-119">È possibile ripristinare la stessa edizione oppure un'edizione successiva dei Servizi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="ced12-119">BizTalk Services can be restored to the same edition or a higher edition.</span></span> <span data-ttu-id="ced12-120">Il ripristino di una versione precedente di Servizi BizTalk, risalente al momento in cui è stato creato il backup, non è supportato.</span><span class="sxs-lookup"><span data-stu-id="ced12-120">Restoring BizTalk Services to a lower edition, from when the backup was taken, is not supported.</span></span>
  
    <span data-ttu-id="ced12-121">Ad esempio, è possibile ripristinare un backup creato con l'edizione Basic nell'edizione Premium,</span><span class="sxs-lookup"><span data-stu-id="ced12-121">For example, a backup using the Basic Edition can be restored to the Premium Edition.</span></span> <span data-ttu-id="ced12-122">ma non è possibile ripristinare un backup creato con l'edizione Premium nell'edizione Standard.</span><span class="sxs-lookup"><span data-stu-id="ced12-122">A backup using the Premium Edition cannot be restored to the Standard Edition.</span></span>
* <span data-ttu-id="ced12-123">Il backup dei numeri di controllo consente di mantenere la continuità dei numeri di controllo.</span><span class="sxs-lookup"><span data-stu-id="ced12-123">The EDI Control numbers are backed up to maintain continuity of the control numbers.</span></span> <span data-ttu-id="ced12-124">Se dopo l'ultimo backup si elaborano dei messaggi, il ripristino del contenuto di questo backup può causare la generazione di numeri di controllo duplicati.</span><span class="sxs-lookup"><span data-stu-id="ced12-124">If messages are processed after the last backup, restoring this backup content can cause duplicate control numbers.</span></span>
* <span data-ttu-id="ced12-125">Se un batch contiene messaggi attivi, elaborare il batch **prima** di eseguire un backup.</span><span class="sxs-lookup"><span data-stu-id="ced12-125">If a batch has active messages, process the batch **before** running a backup.</span></span> <span data-ttu-id="ced12-126">Quando si crea un backup (secondo le esigenze o pianificato), i messaggi in batch non vengono mai archiviati.</span><span class="sxs-lookup"><span data-stu-id="ced12-126">When creating a backup (as needed or scheduled), messages in batches are never stored.</span></span> 
  
    <span data-ttu-id="ced12-127">**Se si crea un backup con la presenza di messaggi attivi in un batch, non verrà eseguito il backup di questi messaggi, che andranno pertanto perduti.**</span><span class="sxs-lookup"><span data-stu-id="ced12-127">**If a backup is taken with active messages in a batch, these messages are not backed up and are therefore lost.**</span></span>
* <span data-ttu-id="ced12-128">Facoltativo: nel portale di Servizi BizTalk arrestare qualsiasi operazione di gestione.</span><span class="sxs-lookup"><span data-stu-id="ced12-128">Optional: In the BizTalk Services Portal, stop any management operations.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="ced12-129">Creare un backup</span><span class="sxs-lookup"><span data-stu-id="ced12-129">Create a backup</span></span>
<span data-ttu-id="ced12-130">È possibile creare in qualsiasi momento un backup controllato interamente dall'utente.</span><span class="sxs-lookup"><span data-stu-id="ced12-130">A backup can be taken at any time and is completely controlled by you.</span></span> <span data-ttu-id="ced12-131">In questa sezione sono elencati i passaggi per creare backup tramite il portale di Azure classico, inclusi:</span><span class="sxs-lookup"><span data-stu-id="ced12-131">This section lists the steps to create backups using the Azure classic portal, including:</span></span>

[<span data-ttu-id="ced12-132">Backup su richiesta</span><span class="sxs-lookup"><span data-stu-id="ced12-132">On Demand backup</span></span>](#backupnow)

[<span data-ttu-id="ced12-133">Pianificare un backup</span><span class="sxs-lookup"><span data-stu-id="ced12-133">Schedule a backup</span></span>](#backupschedule)

#### <span data-ttu-id="ced12-134"><a name="backupnow"></a>Backup su richiesta</span><span class="sxs-lookup"><span data-stu-id="ced12-134"><a name="backupnow"></a>On Demand backup</span></span>
1. <span data-ttu-id="ced12-135">Nel portale di Azure classico, selezionare **Servizi BizTalk**e quindi selezionare il servizio di cui si desidera eseguire il backup.</span><span class="sxs-lookup"><span data-stu-id="ced12-135">In the Azure classic portal, select **BizTalk Services**, and then select the BizTalk Service you want to backup.</span></span>
2. <span data-ttu-id="ced12-136">Nella scheda **Dashboard** selezionare **Backup** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="ced12-136">In the **Dashboard** tab, select **Back up** at the bottom of the page.</span></span>
3. <span data-ttu-id="ced12-137">Indicare un nome per il backup.</span><span class="sxs-lookup"><span data-stu-id="ced12-137">Enter a backup name.</span></span> <span data-ttu-id="ced12-138">Ad esempio, immettere *ServizioBizTalk*BU*Data*.</span><span class="sxs-lookup"><span data-stu-id="ced12-138">For example, enter *myBizTalkService*BU*Date*.</span></span>
4. <span data-ttu-id="ced12-139">Scegliere un account di archiviazione BLOB e selezionare il segno di spunta per avviare il backup.</span><span class="sxs-lookup"><span data-stu-id="ced12-139">Choose a blob storage account and select the checkmark to start the backup.</span></span>

<span data-ttu-id="ced12-140">Al termine del backup verrà creato un contenitore con il nome di backup indicato nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ced12-140">Once the backup completes, a container with the backup name you enter is created in the storage account.</span></span> <span data-ttu-id="ced12-141">Questo contenitore include la configurazione del backup del proprio servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="ced12-141">This container contains your BizTalk Service backup configuration.</span></span>

#### <span data-ttu-id="ced12-142"><a name="backupschedule"></a>Pianificare un backup</span><span class="sxs-lookup"><span data-stu-id="ced12-142"><a name="backupschedule"></a>Schedule a backup</span></span>
1. <span data-ttu-id="ced12-143">Nel portale di Azure classico selezionare **Servizi BizTalk**, il nome del servizio di cui si vuole pianificare il backup e quindi la scheda **Configura**.</span><span class="sxs-lookup"><span data-stu-id="ced12-143">In the Azure classic portal, select **BizTalk Services**, select the BizTalk Service name you want to schedule the backup, and then select the **Configure** tab.</span></span>
2. <span data-ttu-id="ced12-144">Impostare **Stato backup** su **Automatico**.</span><span class="sxs-lookup"><span data-stu-id="ced12-144">Set the **Backup Status** to **Automatic**.</span></span> 
3. <span data-ttu-id="ced12-145">Selezionare **Account di archiviazione** per archiviare il backup, immettere un valore in **Frequenza** per la creazione dei backup e specificare la durata di mantenimento dei backup (**Giorni di conservazione**):</span><span class="sxs-lookup"><span data-stu-id="ced12-145">Select the **Storage Account** to store the backup, enter the **Frequency** to create the backups, and how long to keep the backups (**Retention Days**):</span></span>
   
    ![][AutomaticBU]
   
    <span data-ttu-id="ced12-146">**Note**</span><span class="sxs-lookup"><span data-stu-id="ced12-146">**Notes**</span></span>     
   
   * <span data-ttu-id="ced12-147">In **Giorni di conservazione**, il periodo di conservazione deve essere maggiore della frequenza di backup.</span><span class="sxs-lookup"><span data-stu-id="ced12-147">In **Retention Days**, the retention period must be greater than the backup frequency.</span></span>
   * <span data-ttu-id="ced12-148">Selezionare **Mantieni sempre almeno un backup**, anche se è stato superato il periodo di conservazione.</span><span class="sxs-lookup"><span data-stu-id="ced12-148">Select **Always keep at least one backup**, even if it is past the retention period.</span></span>
4. <span data-ttu-id="ced12-149">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ced12-149">Select **Save**.</span></span>

<span data-ttu-id="ced12-150">Quando si esegue un processo di backup pianificato, viene creato un contenitore (in cui archiviare i dati di backup) nell'account di archiviazione specificato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="ced12-150">When a scheduled backup job runs, it creates a container (to store backup data) in the storage account you entered.</span></span> <span data-ttu-id="ced12-151">Il nome del contenitore è indicato come *Servizio BizTalk nome-data-ora*.</span><span class="sxs-lookup"><span data-stu-id="ced12-151">The name of the container is named *BizTalk Service Name-date-time*.</span></span> 

<span data-ttu-id="ced12-152">Se nel dashboard del servizio BizTalk Service è indicato uno stato **Non riuscito** :</span><span class="sxs-lookup"><span data-stu-id="ced12-152">If the BizTalk Service dashboard shows a **Failed** status:</span></span>

![Last scheduled backup status][BackupStatus] 

<span data-ttu-id="ced12-154">Il collegamento apre i log operazioni dei servizi di gestione per semplificare la risoluzione.</span><span class="sxs-lookup"><span data-stu-id="ced12-154">The link opens the Management Services Operation Logs to help troubleshoot.</span></span> <span data-ttu-id="ced12-155">Vedere [Servizi BizTalk: Risoluzione dei problemi mediante i log operazioni](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span><span class="sxs-lookup"><span data-stu-id="ced12-155">See [BizTalk Services: Troubleshoot using operation logs](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span></span>

## <a name="restore"></a><span data-ttu-id="ced12-156">Restore</span><span class="sxs-lookup"><span data-stu-id="ced12-156">Restore</span></span>
<span data-ttu-id="ced12-157">È possibile ripristinare i backup dal portale di Azure classico oppure da [Ripristino dei servizi BizTalk di Azure da un backup](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span><span class="sxs-lookup"><span data-stu-id="ced12-157">You can restore backups from the Azure classic portal or from the [Restore BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span></span> <span data-ttu-id="ced12-158">In questa sezione sono elencati i passaggi per eseguire il ripristino tramite il portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="ced12-158">This section lists the steps to restore using the classic portal.</span></span>

#### <a name="before-restoring-a-backup"></a><span data-ttu-id="ced12-159">Prima di ripristinare un backup</span><span class="sxs-lookup"><span data-stu-id="ced12-159">Before restoring a backup</span></span>
* <span data-ttu-id="ced12-160">Durante il ripristino di un Servizio BizTalk è possibile immettere nuovi archivi di rilevamento, archiviazione e monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="ced12-160">New tracking, archiving, and monitoring stores can be entered while restoring a BizTalk Service.</span></span>
* <span data-ttu-id="ced12-161">Verranno ripristinati gli stessi dati di runtime EDI.</span><span class="sxs-lookup"><span data-stu-id="ced12-161">The same EDI Runtime data is restored.</span></span> <span data-ttu-id="ced12-162">Il backup del runtime EDI consente di archiviare i numeri di controllo.</span><span class="sxs-lookup"><span data-stu-id="ced12-162">The EDI Runtime backup stores the control numbers.</span></span> <span data-ttu-id="ced12-163">I numeri di controllo ripristinati sono indicati in sequenza a partire dal momento del backup.</span><span class="sxs-lookup"><span data-stu-id="ced12-163">The restored control numbers are in sequence from the time of the backup.</span></span> <span data-ttu-id="ced12-164">Se dopo l'ultimo backup si elaborano dei messaggi, il ripristino del contenuto di questo backup può causare la generazione di numeri di controllo duplicati.</span><span class="sxs-lookup"><span data-stu-id="ced12-164">If messages are processed after the last backup, restoring this backup content can cause duplicate control numbers.</span></span>

#### <a name="restore-a-backup"></a><span data-ttu-id="ced12-165">Ripristino di un backup</span><span class="sxs-lookup"><span data-stu-id="ced12-165">Restore a backup</span></span>
1. <span data-ttu-id="ced12-166">Nel portale di Azure classico selezionare **Nuovo** > **Servizi app** > **Servizio BizTalk** > **Ripristina**:</span><span class="sxs-lookup"><span data-stu-id="ced12-166">In the Azure classic portal, select **New** > **App Services** > **BizTalk Service** > **Restore**:</span></span>
   
    ![Ripristino di un backup][Restore]
2. <span data-ttu-id="ced12-168">In **URL backup**selezionare l'icona della cartella ed espandere l'account di archiviazione di Azure che contiene il backup di configurazione del servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="ced12-168">In **Backup URL**, select the folder icon and expand the Azure storage account that stores the BizTalk Service configuration backup.</span></span> <span data-ttu-id="ced12-169">Espandere il contenitore e nel riquadro sinistro selezionare il file di backup corrispondente con estensione txt.</span><span class="sxs-lookup"><span data-stu-id="ced12-169">Expand the container and in the right pane, select the corresponding back up .txt file.</span></span> 
   <br/><br/>
   <span data-ttu-id="ced12-170">Scegliere **Open**(Apri).</span><span class="sxs-lookup"><span data-stu-id="ced12-170">Select **Open**.</span></span>
3. <span data-ttu-id="ced12-171">Nella pagina **Ripristina servizio BizTalk** specificare un **Nome servizio BizTalk** e verificare le voci in **URL di dominio**, **Edizione** e **Area** per il servizio BizTalk ripristinato.</span><span class="sxs-lookup"><span data-stu-id="ced12-171">On the **Restore BizTalk Service** page, enter a **BizTalk Service Name** and verify the **Domain URL**, **Edition**, and **Region** for the restored BizTalk Service.</span></span> <span data-ttu-id="ced12-172">**Selezionare** Crea nuova istanza di database SQL per il database di rilevamento:</span><span class="sxs-lookup"><span data-stu-id="ced12-172">**Create a new SQL database instance** for the tracking database:</span></span>
   
    ![][RestoreBizTalkService]
   
    <span data-ttu-id="ced12-173">Fare clic sulla freccia Avanti.</span><span class="sxs-lookup"><span data-stu-id="ced12-173">Select the next arrow.</span></span>
4. <span data-ttu-id="ced12-174">Verificare il nome del database SQL, specificare il server fisico sul quale verrà creato il database SQL e un nome utente/una password relativi a tale server.</span><span class="sxs-lookup"><span data-stu-id="ced12-174">Verify the name of the SQL database, enter the physical server where the SQL database will be created, and a username/password for that server.</span></span>

    <span data-ttu-id="ced12-175">Per configurare l'edizione, le dimensioni e altre proprietà del database SQL, selezionare **Configura impostazioni di database avanzate**.</span><span class="sxs-lookup"><span data-stu-id="ced12-175">If you want to configure the SQL database edition, size, and other properties, select  **Configure Advanced Database Settings**.</span></span> 

    <span data-ttu-id="ced12-176">Fare clic sulla freccia Avanti.</span><span class="sxs-lookup"><span data-stu-id="ced12-176">Select the next arrow.</span></span>

1. <span data-ttu-id="ced12-177">Creare un nuovo account di archiviazione o immetterne uno esistente per il servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="ced12-177">Create a new storage account or enter an existing storage account for the BizTalk Service.</span></span>
2. <span data-ttu-id="ced12-178">Selezionare il segno di spunta per avviare il ripristino.</span><span class="sxs-lookup"><span data-stu-id="ced12-178">Select the checkmark to start the restore.</span></span>

<span data-ttu-id="ced12-179">Quando il ripristino sarà stato completato correttamente verrà elencato un nuovo servizio BizTalk con stato sospeso nella pagina dei Servizi BizTalk del portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="ced12-179">Once the restoration successfully completes, a new BizTalk Service is listed in a suspended state on the BizTalk Services page in the Azure classic portal.</span></span>

### <span data-ttu-id="ced12-180"><a name="postrestore"></a>Dopo aver ripristinato un backup</span><span class="sxs-lookup"><span data-stu-id="ced12-180"><a name="postrestore"></a>After restoring a backup</span></span>
<span data-ttu-id="ced12-181">Lo stato di un servizio BizTalk ripristinato è sempre **Sospeso** .</span><span class="sxs-lookup"><span data-stu-id="ced12-181">The BizTalk Service is always restored in a **Suspended** state.</span></span> <span data-ttu-id="ced12-182">In questo stato è possibile apportare qualsiasi modifica alla configurazione prima che il nuovo ambiente diventi funzionale, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ced12-182">In this state, you can make any configuration changes before the new environment is functional, including:</span></span>

* <span data-ttu-id="ced12-183">Se le applicazioni del Servizio BizTalk sono state create mediante l'SDK di Servizi BizTalk di Azure, potrebbe essere necessario aggiornare le credenziali ACS in tali applicazioni, in modo che funzionino nell'ambiente ripristinato.</span><span class="sxs-lookup"><span data-stu-id="ced12-183">If you created BizTalk Service applications using the Azure BizTalk Services SDK, you may need to to update the Access Control (ACS) credentials in those applications to work with the restored environment.</span></span>
* <span data-ttu-id="ced12-184">Un servizio BizTalk viene ripristinato per replicare un ambiente di un servizio BizTalk esistente.</span><span class="sxs-lookup"><span data-stu-id="ced12-184">You restore a BizTalk Service to replicate an existing BizTalk Service environment.</span></span> <span data-ttu-id="ced12-185">In una situazione simile, se nel portale di Servizi BizTalk originale sono stati configurati contratti che usano una cartella FTP come origine, può essere necessario aggiornare tali contratti nell'ambiente appena ripristinato in modo da usare una cartella FTP di origine diversa.</span><span class="sxs-lookup"><span data-stu-id="ced12-185">In this situation, if there are agreements configured in the original BizTalk Services portal that use a source FTP folder, you may need to update the agreements in the newly restored environment to use a different source FTP folder.</span></span> <span data-ttu-id="ced12-186">In caso contrario, è possibile che due diversi contratti tentino di eseguire il pull dello stesso messaggio.</span><span class="sxs-lookup"><span data-stu-id="ced12-186">Otherwise, there may be two different agreements trying to pull the same message.</span></span>
* <span data-ttu-id="ced12-187">Se il ripristino è stato eseguito per ottenere più ambienti di servizi BizTalk, assicurarsi di individuare l'ambiente corretto mediante le applicazioni di Visual Studio, i cmdlet di PowerShell, le API REST oppure le API del modello a oggetti per la gestione dei partner commerciali.</span><span class="sxs-lookup"><span data-stu-id="ced12-187">If you restored to have multiple BizTalk Service environments, make sure you target the correct environment in the Visual Studio applications, PowerShell cmdlets, REST APIs, or Trading Partner Management OM APIs.</span></span>
* <span data-ttu-id="ced12-188">È buona norma configurare i backup automatizzati nell'ambiente del servizio BizTalk appena ripristinato.</span><span class="sxs-lookup"><span data-stu-id="ced12-188">It's a good practice to configure automated backups on the newly restored BizTalk Service environment.</span></span>

<span data-ttu-id="ced12-189">Per avviare il servizio BizTalk nel portale di Azure classico, selezionare il servizio BizTalk ripristinato e quindi **Riprendi** sulla barra delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="ced12-189">To start the BizTalk Service in the Azure classic portal, select the restored BizTalk Service and select **Resume** in the task bar.</span></span> 

## <a name="what-gets-backed-up"></a><span data-ttu-id="ced12-190">Elementi di cui viene eseguito il backup</span><span class="sxs-lookup"><span data-stu-id="ced12-190">What gets backed up</span></span>
<span data-ttu-id="ced12-191">Viene eseguito il backup degli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ced12-191">When a backup is created, the following items are backed up:</span></span>

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH><span data-ttu-id="ced12-192">Elementi di backup</span><span class="sxs-lookup"><span data-stu-id="ced12-192">Items backed up</span></span></TH> 
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="ced12-193">
 <strong>Portale Servizi BizTalk di Azure</strong></span><span class="sxs-lookup"><span data-stu-id="ced12-193">
 <strong>Azure BizTalk Services Portal</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="ced12-194">Configurazione e runtime</span><span class="sxs-lookup"><span data-stu-id="ced12-194">Configuration and Runtime</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="ced12-195">Dettagli su partner e profilo</span><span class="sxs-lookup"><span data-stu-id="ced12-195">Partner and profile details</span></span></li>
<li><span data-ttu-id="ced12-196">Contratti con il partner</span><span class="sxs-lookup"><span data-stu-id="ced12-196">Partner Agreements</span></span></li>
<li><span data-ttu-id="ced12-197">Assembly personalizzati distribuiti</span><span class="sxs-lookup"><span data-stu-id="ced12-197">Custom assemblies deployed</span></span></li>
<li><span data-ttu-id="ced12-198">Bridge distribuiti</span><span class="sxs-lookup"><span data-stu-id="ced12-198">Bridges deployed</span></span></li>
<li><span data-ttu-id="ced12-199">Certificati</span><span class="sxs-lookup"><span data-stu-id="ced12-199">Certificates</span></span></li>
<li><span data-ttu-id="ced12-200">Trasformazioni distribuite</span><span class="sxs-lookup"><span data-stu-id="ced12-200">Transforms deployed</span></span></li>
<li><span data-ttu-id="ced12-201">Pipeline</span><span class="sxs-lookup"><span data-stu-id="ced12-201">Pipelines</span></span></li>
<li><span data-ttu-id="ced12-202">Modelli creati e salvati nel portale Servizi BizTalk</span><span class="sxs-lookup"><span data-stu-id="ced12-202">Templates created and saved in the BizTalk Services Portal</span></span></li>
<li><span data-ttu-id="ced12-203">Mapping X12 ST01 e GS01</span><span class="sxs-lookup"><span data-stu-id="ced12-203">X12 ST01 and GS01 mappings</span></span></li>
<li><span data-ttu-id="ced12-204">Numeri di controllo (EDI)</span><span class="sxs-lookup"><span data-stu-id="ced12-204">Control numbers (EDI)</span></span></li>
<li><span data-ttu-id="ced12-205">Valori MIC del messaggio AS2</span><span class="sxs-lookup"><span data-stu-id="ced12-205">AS2 Message MIC values</span></span></li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2"><span data-ttu-id="ced12-206">
 <strong>Servizio BizTalk di Azure</strong></span><span class="sxs-lookup"><span data-stu-id="ced12-206">
 <strong>Azure BizTalk Service</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="ced12-207">Certificato SSL</span><span class="sxs-lookup"><span data-stu-id="ced12-207">SSL Certificate</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="ced12-208">Dati certificato SSL</span><span class="sxs-lookup"><span data-stu-id="ced12-208">SSL Certificate Data</span></span></li>
<li><span data-ttu-id="ced12-209">Password certificato SSL</span><span class="sxs-lookup"><span data-stu-id="ced12-209">SSL Certificate Password</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td><span data-ttu-id="ced12-210">Impostazioni del servizio BizTalk</span><span class="sxs-lookup"><span data-stu-id="ced12-210">BizTalk Service Settings</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="ced12-211">Conteggio dell'unità di scala</span><span class="sxs-lookup"><span data-stu-id="ced12-211">Scale unit count</span></span></li>
<li><span data-ttu-id="ced12-212">Edizione</span><span class="sxs-lookup"><span data-stu-id="ced12-212">Edition</span></span></li>
<li><span data-ttu-id="ced12-213">Versione prodotto</span><span class="sxs-lookup"><span data-stu-id="ced12-213">Product Version</span></span></li>
<li><span data-ttu-id="ced12-214">Area/data center</span><span class="sxs-lookup"><span data-stu-id="ced12-214">Region/Datacenter</span></span></li>
<li><span data-ttu-id="ced12-215">Spazio dei nomi e chiave del Servizio di controllo di accesso (ACS)</span><span class="sxs-lookup"><span data-stu-id="ced12-215">Access Control Service (ACS) namespace and key</span></span></li>
<li><span data-ttu-id="ced12-216">Rilevamento della stringa di connessione al database</span><span class="sxs-lookup"><span data-stu-id="ced12-216">Tracking database connection string</span></span></li>
<li><span data-ttu-id="ced12-217">Archiviazione della stringa di connessione all'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="ced12-217">Archiving Storage account connection string</span></span></li>
<li><span data-ttu-id="ced12-218">Monitoraggio della stringa di connessione all'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="ced12-218">Monitoring storage account connection string</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="ced12-219">
 <strong>Elementi aggiuntivi</strong></span><span class="sxs-lookup"><span data-stu-id="ced12-219">
 <strong>Additional Items</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="ced12-220">Database di rilevamento</span><span class="sxs-lookup"><span data-stu-id="ced12-220">Tracking Database</span></span></td> 
<td><span data-ttu-id="ced12-221">Quando viene creato il servizio BizTalk, vengono immessi i dettagli relativi al database di rilevamento, tra cui il server di database SQL di Azure e il nome del database di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="ced12-221">When the BizTalk Service is created, the Tracking Database details are entered, including the Azure SQL Database Server and the Tracking Database name.</span></span> <span data-ttu-id="ced12-222">Non viene eseguito il backup automatico del database di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="ced12-222">The Tracking Database is not automatically backed up.</span></span>
<br/><br/><span data-ttu-id="ced12-223">
<strong>Importante</strong></span><span class="sxs-lookup"><span data-stu-id="ced12-223">
<strong>Important</strong></span></span><br/>
<span data-ttu-id="ced12-224">Se il database di rilevamento viene eliminato ed è necessario ripristinarlo, è necessario disporre di un backup precedente.</span><span class="sxs-lookup"><span data-stu-id="ced12-224">If the Tracking Database is deleted and the database needs recovered, a previous backup must exist.</span></span> <span data-ttu-id="ced12-225">Se non è disponibile un backup, non sarà possibile recuperare il database di rilevamento e i relativi dati.</span><span class="sxs-lookup"><span data-stu-id="ced12-225">If a backup does not exist, the Tracking Database and its data are not recoverable.</span></span> <span data-ttu-id="ced12-226">In questo caso, creare un nuovo database di rilevamento con lo stesso nome.</span><span class="sxs-lookup"><span data-stu-id="ced12-226">In this situation, create a new Tracking Database with the same database name.</span></span> <span data-ttu-id="ced12-227">È consigliata la replica geografica.</span><span class="sxs-lookup"><span data-stu-id="ced12-227">Geo-Replication is recommended.</span></span></td>
</tr> 
</table>

## <a name="next"></a><span data-ttu-id="ced12-228">Avanti</span><span class="sxs-lookup"><span data-stu-id="ced12-228">Next</span></span>
<span data-ttu-id="ced12-229">Per creare Servizi BizTalk di Azure nel portale di Azure classico, passare a [Servizi BizTalk: Provisioning mediante il portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span><span class="sxs-lookup"><span data-stu-id="ced12-229">To create Azure BizTalk Services in the Azure classic portal, go to [BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span></span> <span data-ttu-id="ced12-230">Per iniziare a creare applicazioni, vedere [Servizi BizTalk di Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="ced12-230">To start creating applications, go to [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="ced12-231">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ced12-231">See Also</span></span>
* [<span data-ttu-id="ced12-232">Backup del servizio BizTalk</span><span class="sxs-lookup"><span data-stu-id="ced12-232">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="ced12-233">Ripristino del servizio BizTalk da un backup</span><span class="sxs-lookup"><span data-stu-id="ced12-233">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="ced12-234">Servizi BizTalk: Grafico edizioni Developer, Basic, Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="ced12-234">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="ced12-235">Servizi BizTalk: effettuare il provisioning di un servizio BizTalk mediante il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="ced12-235">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="ced12-236">Servizi BizTalk: Tabella degli stati del servizio</span><span class="sxs-lookup"><span data-stu-id="ced12-236">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="ced12-237">Servizi BizTalk: Schede Dashboard, Monitoraggio, Scalabilità</span><span class="sxs-lookup"><span data-stu-id="ced12-237">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="ced12-238">Servizi BizTalk: limitazione</span><span class="sxs-lookup"><span data-stu-id="ced12-238">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="ced12-239">Servizi BizTalk: nome e chiave dell'autorità emittente</span><span class="sxs-lookup"><span data-stu-id="ced12-239">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="ced12-240">Come iniziare a usare l'SDK di Servizi BizTalk di Azure</span><span class="sxs-lookup"><span data-stu-id="ced12-240">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

