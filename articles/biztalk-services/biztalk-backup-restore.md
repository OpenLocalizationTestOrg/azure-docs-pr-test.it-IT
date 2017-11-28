---
title: aaaCreate e ripristinare un backup nei servizi BizTalk | Documenti Microsoft
description: "I Servizi BizTalk includono funzionalità di backup e ripristino. Informazioni su come toocreate determinare quali backup e ripristinare un backup. MABS, WABS"
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
ms.openlocfilehash: 32356ad870678fa5fd5bbbbf13d9377188f770a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-backup-and-restore"></a><span data-ttu-id="3ce5f-105">Servizi BizTalk: backup e ripristino</span><span class="sxs-lookup"><span data-stu-id="3ce5f-105">BizTalk Services: Backup and Restore</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="3ce5f-106">I Servizi BizTalk di Azure includono funzioni di backup e ripristino.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-106">Azure BizTalk Services includes Backup and Restore capabilities.</span></span> <span data-ttu-id="3ce5f-107">In questo argomento viene descritto come toobackup e ripristino di servizi di BizTalk utilizzando hello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-107">This topic describes how toobackup and restore BizTalk Services using hello Azure classic portal.</span></span>

<span data-ttu-id="3ce5f-108">È inoltre possibile eseguire i servizi di BizTalk utilizzando hello [API REST di servizi BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span><span class="sxs-lookup"><span data-stu-id="3ce5f-108">You can also back up BizTalk Services using hello [BizTalk Services REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span></span> 

> [!NOTE]
> <span data-ttu-id="3ce5f-109">Le connessioni ibride non sottoposti a backup, indipendentemente dall'edizione hello.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-109">Hybrid Connections are NOT backed up, regardless of hello Edition.</span></span> <span data-ttu-id="3ce5f-110">È necessario ricreare le connessioni ibride.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-110">You must recreate your hybrid connections.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="3ce5f-111">Operazioni preliminari</span><span class="sxs-lookup"><span data-stu-id="3ce5f-111">Before you Begin</span></span>
* <span data-ttu-id="3ce5f-112">Le funzionalità di backup e ripristino potrebbero non essere disponibili per tutte le edizioni.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-112">Backup and Restore may not be available for all editions.</span></span> <span data-ttu-id="3ce5f-113">Vedere [Servizi BizTalk: Grafico edizioni](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="3ce5f-113">See [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>
* <span data-ttu-id="3ce5f-114">Utilizza hello portale di Azure classico, è possibile creare un backup su richiesta o creare un backup pianificato.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-114">Using hello Azure classic portal, you can create an On Demand backup or create a scheduled backup.</span></span> 
* <span data-ttu-id="3ce5f-115">Contenuto di backup può essere ripristinato toohello stesso BizTalk Service o tooa nuovo BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-115">Backup content can be restored toohello same BizTalk Service or tooa new BizTalk Service.</span></span> <span data-ttu-id="3ce5f-116">toorestore hello BizTalk Service utilizzando hello stesso nome, hello esistente BizTalk Service deve essere eliminato e il nome di hello deve essere disponibile.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-116">toorestore hello BizTalk Service using hello same name, hello existing BizTalk Service must be deleted and hello name must be available.</span></span> <span data-ttu-id="3ce5f-117">Dopo aver eliminato un BizTalk Service, può richiedere più tempo desiderato per hello stesso nome toobe disponibili.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-117">After you delete a BizTalk Service, it can take longer time than wanted for hello same name toobe available.</span></span> <span data-ttu-id="3ce5f-118">Se non è possibile attendere hello stesso nome toobe disponibili, quindi ripristinare tooa nuovo BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-118">If you cannot wait for hello same name toobe available, then restore tooa new BizTalk Service.</span></span>
* <span data-ttu-id="3ce5f-119">Servizi BizTalk può essere ripristinato toohello stessa versione o una versione successiva.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-119">BizTalk Services can be restored toohello same edition or a higher edition.</span></span> <span data-ttu-id="3ce5f-120">Ripristino dei servizi BizTalk tooa edizione inferiore, da quando è stato eseguito il backup di hello, non è supportata.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-120">Restoring BizTalk Services tooa lower edition, from when hello backup was taken, is not supported.</span></span>
  
    <span data-ttu-id="3ce5f-121">Ad esempio, un backup utilizzando hello che Edizione Basic può essere ripristinato toohello Premium Edition.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-121">For example, a backup using hello Basic Edition can be restored toohello Premium Edition.</span></span> <span data-ttu-id="3ce5f-122">Un backup utilizzando hello che edizione Premium non può essere ripristinato toohello Standard Edition.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-122">A backup using hello Premium Edition cannot be restored toohello Standard Edition.</span></span>
* <span data-ttu-id="3ce5f-123">numeri di controllo EDI Hello sottoposti a backup continuità toomaintain hello dei numeri di controllo.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-123">hello EDI Control numbers are backed up toomaintain continuity of hello control numbers.</span></span> <span data-ttu-id="3ce5f-124">Se i messaggi vengono elaborati dopo l'ultimo backup hello, ripristinare il contenuto di backup può provocare numeri di controllo duplicati.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-124">If messages are processed after hello last backup, restoring this backup content can cause duplicate control numbers.</span></span>
* <span data-ttu-id="3ce5f-125">Se dispone di un batch di messaggi attivi, elabora il batch di hello **prima** in esecuzione un backup.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-125">If a batch has active messages, process hello batch **before** running a backup.</span></span> <span data-ttu-id="3ce5f-126">Quando si crea un backup (secondo le esigenze o pianificato), i messaggi in batch non vengono mai archiviati.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-126">When creating a backup (as needed or scheduled), messages in batches are never stored.</span></span> 
  
    <span data-ttu-id="3ce5f-127">**Se si crea un backup con la presenza di messaggi attivi in un batch, non verrà eseguito il backup di questi messaggi, che andranno pertanto perduti.**</span><span class="sxs-lookup"><span data-stu-id="3ce5f-127">**If a backup is taken with active messages in a batch, these messages are not backed up and are therefore lost.**</span></span>
* <span data-ttu-id="3ce5f-128">Facoltativo: Nel portale dei servizi BizTalk di hello, arrestare eventuali operazioni di gestione.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-128">Optional: In hello BizTalk Services Portal, stop any management operations.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="3ce5f-129">Creare un backup</span><span class="sxs-lookup"><span data-stu-id="3ce5f-129">Create a backup</span></span>
<span data-ttu-id="3ce5f-130">È possibile creare in qualsiasi momento un backup controllato interamente dall'utente.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-130">A backup can be taken at any time and is completely controlled by you.</span></span> <span data-ttu-id="3ce5f-131">Questa sezione sono elencati i backup di toocreate passaggi hello utilizzando hello Azure classico portale, tra cui:</span><span class="sxs-lookup"><span data-stu-id="3ce5f-131">This section lists hello steps toocreate backups using hello Azure classic portal, including:</span></span>

[<span data-ttu-id="3ce5f-132">Backup su richiesta</span><span class="sxs-lookup"><span data-stu-id="3ce5f-132">On Demand backup</span></span>](#backupnow)

[<span data-ttu-id="3ce5f-133">Pianificare un backup</span><span class="sxs-lookup"><span data-stu-id="3ce5f-133">Schedule a backup</span></span>](#backupschedule)

#### <span data-ttu-id="3ce5f-134"><a name="backupnow"></a>Backup su richiesta</span><span class="sxs-lookup"><span data-stu-id="3ce5f-134"><a name="backupnow"></a>On Demand backup</span></span>
1. <span data-ttu-id="3ce5f-135">Nel portale di Azure classico hello, selezionare **servizi BizTalk**, e quindi selezionare hello BizTalk Service desiderato toobackup.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-135">In hello Azure classic portal, select **BizTalk Services**, and then select hello BizTalk Service you want toobackup.</span></span>
2. <span data-ttu-id="3ce5f-136">In hello **Dashboard** , selezionare **backup** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-136">In hello **Dashboard** tab, select **Back up** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="3ce5f-137">Indicare un nome per il backup.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-137">Enter a backup name.</span></span> <span data-ttu-id="3ce5f-138">Ad esempio, immettere *ServizioBizTalk*BU*Data*.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-138">For example, enter *myBizTalkService*BU*Date*.</span></span>
4. <span data-ttu-id="3ce5f-139">Scegliere un account di archiviazione blob di backup e selezionare hello segno di spunta toostart hello.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-139">Choose a blob storage account and select hello checkmark toostart hello backup.</span></span>

<span data-ttu-id="3ce5f-140">Al termine del backup hello, viene creato un contenitore con nome del backup hello che immesso nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-140">Once hello backup completes, a container with hello backup name you enter is created in hello storage account.</span></span> <span data-ttu-id="3ce5f-141">Questo contenitore include la configurazione del backup del proprio servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-141">This container contains your BizTalk Service backup configuration.</span></span>

#### <span data-ttu-id="3ce5f-142"><a name="backupschedule"></a>Pianificare un backup</span><span class="sxs-lookup"><span data-stu-id="3ce5f-142"><a name="backupschedule"></a>Schedule a backup</span></span>
1. <span data-ttu-id="3ce5f-143">Nel portale di Azure classico hello, selezionare **servizi BizTalk**, selezionare hello Nome BizTalk Service backup hello tooschedule desiderato e quindi selezionare hello **configura** scheda.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-143">In hello Azure classic portal, select **BizTalk Services**, select hello BizTalk Service name you want tooschedule hello backup, and then select hello **Configure** tab.</span></span>
2. <span data-ttu-id="3ce5f-144">Set hello **stato Backup** troppo**automatica**.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-144">Set hello **Backup Status** too**Automatic**.</span></span> 
3. <span data-ttu-id="3ce5f-145">Seleziona hello **Account di archiviazione** toostore hello backup, immettere hello **frequenza** toocreate hello backup e il tempo tookeep hello backup (**giorni di conservazione**):</span><span class="sxs-lookup"><span data-stu-id="3ce5f-145">Select hello **Storage Account** toostore hello backup, enter hello **Frequency** toocreate hello backups, and how long tookeep hello backups (**Retention Days**):</span></span>
   
    ![][AutomaticBU]
   
    <span data-ttu-id="3ce5f-146">**Note**</span><span class="sxs-lookup"><span data-stu-id="3ce5f-146">**Notes**</span></span>     
   
   * <span data-ttu-id="3ce5f-147">In **giorni di conservazione**, il periodo di memorizzazione hello deve essere maggiore della frequenza di backup hello.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-147">In **Retention Days**, hello retention period must be greater than hello backup frequency.</span></span>
   * <span data-ttu-id="3ce5f-148">Selezionare **mantenere sempre almeno un backup**, anche se è stata superata hello periodo di memorizzazione.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-148">Select **Always keep at least one backup**, even if it is past hello retention period.</span></span>
4. <span data-ttu-id="3ce5f-149">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-149">Select **Save**.</span></span>

<span data-ttu-id="3ce5f-150">Quando viene eseguito un processo di backup pianificato, viene creato un contenitore (dati di backup toostore) nell'account di archiviazione hello immesso.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-150">When a scheduled backup job runs, it creates a container (toostore backup data) in hello storage account you entered.</span></span> <span data-ttu-id="3ce5f-151">nome Hello del contenitore di hello è denominata *BizTalk Service Name-data-ora*.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-151">hello name of hello container is named *BizTalk Service Name-date-time*.</span></span> 

<span data-ttu-id="3ce5f-152">Se viene visualizzato il dashboard di BizTalk Service hello un **Failed** stato:</span><span class="sxs-lookup"><span data-stu-id="3ce5f-152">If hello BizTalk Service dashboard shows a **Failed** status:</span></span>

![Last scheduled backup status][BackupStatus] 

<span data-ttu-id="3ce5f-154">collegamento Hello apre hello registri operazioni di Gestione servizi toohelp risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-154">hello link opens hello Management Services Operation Logs toohelp troubleshoot.</span></span> <span data-ttu-id="3ce5f-155">Vedere [Servizi BizTalk: Risoluzione dei problemi mediante i log operazioni](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span><span class="sxs-lookup"><span data-stu-id="3ce5f-155">See [BizTalk Services: Troubleshoot using operation logs](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span></span>

## <a name="restore"></a><span data-ttu-id="3ce5f-156">Ripristino</span><span class="sxs-lookup"><span data-stu-id="3ce5f-156">Restore</span></span>
<span data-ttu-id="3ce5f-157">È possibile ripristinare i backup dal portale di Azure classico hello o da hello [ripristinare API REST dei servizi BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span><span class="sxs-lookup"><span data-stu-id="3ce5f-157">You can restore backups from hello Azure classic portal or from hello [Restore BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span></span> <span data-ttu-id="3ce5f-158">Questa sezione elenca hello passaggi toorestore utilizzando portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-158">This section lists hello steps toorestore using hello classic portal.</span></span>

#### <a name="before-restoring-a-backup"></a><span data-ttu-id="3ce5f-159">Prima di ripristinare un backup</span><span class="sxs-lookup"><span data-stu-id="3ce5f-159">Before restoring a backup</span></span>
* <span data-ttu-id="3ce5f-160">Durante il ripristino di un Servizio BizTalk è possibile immettere nuovi archivi di rilevamento, archiviazione e monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-160">New tracking, archiving, and monitoring stores can be entered while restoring a BizTalk Service.</span></span>
* <span data-ttu-id="3ce5f-161">Hello stessi dati di Runtime EDI viene ripristinati.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-161">hello same EDI Runtime data is restored.</span></span> <span data-ttu-id="3ce5f-162">backup di Runtime EDI Hello archivia numeri di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-162">hello EDI Runtime backup stores hello control numbers.</span></span> <span data-ttu-id="3ce5f-163">numeri di controllo Hello ripristinato sono in sequenza dall'ora hello del backup hello.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-163">hello restored control numbers are in sequence from hello time of hello backup.</span></span> <span data-ttu-id="3ce5f-164">Se i messaggi vengono elaborati dopo l'ultimo backup hello, ripristinare il contenuto di backup può provocare numeri di controllo duplicati.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-164">If messages are processed after hello last backup, restoring this backup content can cause duplicate control numbers.</span></span>

#### <a name="restore-a-backup"></a><span data-ttu-id="3ce5f-165">Ripristino di un backup</span><span class="sxs-lookup"><span data-stu-id="3ce5f-165">Restore a backup</span></span>
1. <span data-ttu-id="3ce5f-166">Nel portale di Azure classico hello, selezionare **New** > **servizi App** > **BizTalk Service** > **ripristino** :</span><span class="sxs-lookup"><span data-stu-id="3ce5f-166">In hello Azure classic portal, select **New** > **App Services** > **BizTalk Service** > **Restore**:</span></span>
   
    ![Ripristino di un backup][Restore]
2. <span data-ttu-id="3ce5f-168">In **Backup URL**, selezionare l'icona della cartella hello ed espandere hello account di archiviazione Azure che archivi hello backup della configurazione di BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-168">In **Backup URL**, select hello folder icon and expand hello Azure storage account that stores hello BizTalk Service configuration backup.</span></span> <span data-ttu-id="3ce5f-169">Espandere il contenitore di hello e nel riquadro di destra hello, selezionare hello corrispondente, eseguire il backup dei file con estensione txt.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-169">Expand hello container and in hello right pane, select hello corresponding back up .txt file.</span></span> 
   <br/><br/>
   <span data-ttu-id="3ce5f-170">Scegliere **Open**(Apri).</span><span class="sxs-lookup"><span data-stu-id="3ce5f-170">Select **Open**.</span></span>
3. <span data-ttu-id="3ce5f-171">In hello **servizio Ripristino configurazione di BizTalk** pagina, immettere un **nome del servizio BizTalk** e verificare hello **URL di dominio**, **Edition**e **Area** per hello ripristinato BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-171">On hello **Restore BizTalk Service** page, enter a **BizTalk Service Name** and verify hello **Domain URL**, **Edition**, and **Region** for hello restored BizTalk Service.</span></span> <span data-ttu-id="3ce5f-172">**Creare una nuova istanza di database SQL** per database di rilevamento hello:</span><span class="sxs-lookup"><span data-stu-id="3ce5f-172">**Create a new SQL database instance** for hello tracking database:</span></span>
   
    ![][RestoreBizTalkService]
   
    <span data-ttu-id="3ce5f-173">Selezionare sulla freccia avanti hello.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-173">Select hello next arrow.</span></span>
4. <span data-ttu-id="3ce5f-174">Verificare il nome di hello del database SQL di hello, immettere hello server fisici in cui verrà creato il database SQL hello e un nome utente e password per il server.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-174">Verify hello name of hello SQL database, enter hello physical server where hello SQL database will be created, and a username/password for that server.</span></span>

    <span data-ttu-id="3ce5f-175">Se si desidera l'edizione del database SQL tooconfigure hello, dimensioni e altre proprietà, selezionare **Configure Advanced Settings Database**.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-175">If you want tooconfigure hello SQL database edition, size, and other properties, select  **Configure Advanced Database Settings**.</span></span> 

    <span data-ttu-id="3ce5f-176">Selezionare sulla freccia avanti hello.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-176">Select hello next arrow.</span></span>

1. <span data-ttu-id="3ce5f-177">Creare un nuovo account di archiviazione o immettere un account di archiviazione esistente per hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-177">Create a new storage account or enter an existing storage account for hello BizTalk Service.</span></span>
2. <span data-ttu-id="3ce5f-178">Selezionare Ripristina hello toostart di hello segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-178">Select hello checkmark toostart hello restore.</span></span>

<span data-ttu-id="3ce5f-179">Dopo il ripristino di hello è stata completata correttamente, è elencato un nuovo di BizTalk Service in uno stato sospeso, nella pagina servizi BizTalk hello hello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-179">Once hello restoration successfully completes, a new BizTalk Service is listed in a suspended state on hello BizTalk Services page in hello Azure classic portal.</span></span>

### <span data-ttu-id="3ce5f-180"><a name="postrestore"></a>Dopo aver ripristinato un backup</span><span class="sxs-lookup"><span data-stu-id="3ce5f-180"><a name="postrestore"></a>After restoring a backup</span></span>
<span data-ttu-id="3ce5f-181">Hello BizTalk Service viene sempre ripristinato un **Suspended** stato.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-181">hello BizTalk Service is always restored in a **Suspended** state.</span></span> <span data-ttu-id="3ce5f-182">In questo stato, può essere modifiche alla configurazione prima nuovo ambiente hello è funzionale, tra cui:</span><span class="sxs-lookup"><span data-stu-id="3ce5f-182">In this state, you can make any configuration changes before hello new environment is functional, including:</span></span>

* <span data-ttu-id="3ce5f-183">Se le applicazioni di BizTalk Service utilizzando hello Azure BizTalk Services SDK è stato creato, potrebbe essere credenziali di controllo di accesso (ACS) tootooupdate hello in toowork tali applicazioni con ambiente hello ripristinato.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-183">If you created BizTalk Service applications using hello Azure BizTalk Services SDK, you may need tootooupdate hello Access Control (ACS) credentials in those applications toowork with hello restored environment.</span></span>
* <span data-ttu-id="3ce5f-184">Ripristinare un tooreplicate BizTalk Service un ambiente BizTalk Service esistente.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-184">You restore a BizTalk Service tooreplicate an existing BizTalk Service environment.</span></span> <span data-ttu-id="3ce5f-185">In questo caso, se sono presenti contratti configurati nel portale di servizi BizTalk originale hello che utilizzano una cartella di origine FTP, potrebbe essere contratti hello tooupdate in toouse ambiente hello appena ripristinato una cartella FTP di origine diversa.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-185">In this situation, if there are agreements configured in hello original BizTalk Services portal that use a source FTP folder, you may need tooupdate hello agreements in hello newly restored environment toouse a different source FTP folder.</span></span> <span data-ttu-id="3ce5f-186">In caso contrario, potrebbero essere presenti due contratti diversi durante il tentativo toopull hello stesso messaggio.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-186">Otherwise, there may be two different agreements trying toopull hello same message.</span></span>
* <span data-ttu-id="3ce5f-187">Se è stato ripristinato toohave più ambienti BizTalk Service, assicurarsi che la destinazione è ambiente corretto di hello in applicazioni di Visual Studio hello, i cmdlet di PowerShell, API REST o API del modello a oggetti gestione dei Partner commerciali.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-187">If you restored toohave multiple BizTalk Service environments, make sure you target hello correct environment in hello Visual Studio applications, PowerShell cmdlets, REST APIs, or Trading Partner Management OM APIs.</span></span>
* <span data-ttu-id="3ce5f-188">Si tratta di un backup di tooconfigure automatizzata buona norma in ambiente del servizio BizTalk hello appena ripristinato.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-188">It's a good practice tooconfigure automated backups on hello newly restored BizTalk Service environment.</span></span>

<span data-ttu-id="3ce5f-189">Ciao toostart BizTalk Service hello portale di Azure classico, hello seleziona ripristinato BizTalk Service e selezionare **Resume** nella barra delle applicazioni hello.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-189">toostart hello BizTalk Service in hello Azure classic portal, select hello restored BizTalk Service and select **Resume** in hello task bar.</span></span> 

## <a name="what-gets-backed-up"></a><span data-ttu-id="3ce5f-190">Elementi di cui viene eseguito il backup</span><span class="sxs-lookup"><span data-stu-id="3ce5f-190">What gets backed up</span></span>
<span data-ttu-id="3ce5f-191">Quando viene creato un backup, hello seguenti elementi vengono eseguito il backup:</span><span class="sxs-lookup"><span data-stu-id="3ce5f-191">When a backup is created, hello following items are backed up:</span></span>

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH><span data-ttu-id="3ce5f-192">Elementi di backup</span><span class="sxs-lookup"><span data-stu-id="3ce5f-192">Items backed up</span></span></TH> 
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="3ce5f-193">
 <strong>Portale Servizi BizTalk di Azure</strong></span><span class="sxs-lookup"><span data-stu-id="3ce5f-193">
 <strong>Azure BizTalk Services Portal</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="3ce5f-194">Configurazione e runtime</span><span class="sxs-lookup"><span data-stu-id="3ce5f-194">Configuration and Runtime</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="3ce5f-195">Dettagli su partner e profilo</span><span class="sxs-lookup"><span data-stu-id="3ce5f-195">Partner and profile details</span></span></li>
<li><span data-ttu-id="3ce5f-196">Contratti con il partner</span><span class="sxs-lookup"><span data-stu-id="3ce5f-196">Partner Agreements</span></span></li>
<li><span data-ttu-id="3ce5f-197">Assembly personalizzati distribuiti</span><span class="sxs-lookup"><span data-stu-id="3ce5f-197">Custom assemblies deployed</span></span></li>
<li><span data-ttu-id="3ce5f-198">Bridge distribuiti</span><span class="sxs-lookup"><span data-stu-id="3ce5f-198">Bridges deployed</span></span></li>
<li><span data-ttu-id="3ce5f-199">Certificati</span><span class="sxs-lookup"><span data-stu-id="3ce5f-199">Certificates</span></span></li>
<li><span data-ttu-id="3ce5f-200">Trasformazioni distribuite</span><span class="sxs-lookup"><span data-stu-id="3ce5f-200">Transforms deployed</span></span></li>
<li><span data-ttu-id="3ce5f-201">Pipeline</span><span class="sxs-lookup"><span data-stu-id="3ce5f-201">Pipelines</span></span></li>
<li><span data-ttu-id="3ce5f-202">I modelli creati e salvati in hello portale dei servizi BizTalk</span><span class="sxs-lookup"><span data-stu-id="3ce5f-202">Templates created and saved in hello BizTalk Services Portal</span></span></li>
<li><span data-ttu-id="3ce5f-203">Mapping X12 ST01 e GS01</span><span class="sxs-lookup"><span data-stu-id="3ce5f-203">X12 ST01 and GS01 mappings</span></span></li>
<li><span data-ttu-id="3ce5f-204">Numeri di controllo (EDI)</span><span class="sxs-lookup"><span data-stu-id="3ce5f-204">Control numbers (EDI)</span></span></li>
<li><span data-ttu-id="3ce5f-205">Valori MIC del messaggio AS2</span><span class="sxs-lookup"><span data-stu-id="3ce5f-205">AS2 Message MIC values</span></span></li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2"><span data-ttu-id="3ce5f-206">
 <strong>Servizio BizTalk di Azure</strong></span><span class="sxs-lookup"><span data-stu-id="3ce5f-206">
 <strong>Azure BizTalk Service</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="3ce5f-207">Certificato SSL</span><span class="sxs-lookup"><span data-stu-id="3ce5f-207">SSL Certificate</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="3ce5f-208">Dati certificato SSL</span><span class="sxs-lookup"><span data-stu-id="3ce5f-208">SSL Certificate Data</span></span></li>
<li><span data-ttu-id="3ce5f-209">Password certificato SSL</span><span class="sxs-lookup"><span data-stu-id="3ce5f-209">SSL Certificate Password</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td><span data-ttu-id="3ce5f-210">Impostazioni del servizio BizTalk</span><span class="sxs-lookup"><span data-stu-id="3ce5f-210">BizTalk Service Settings</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="3ce5f-211">Conteggio dell'unità di scala</span><span class="sxs-lookup"><span data-stu-id="3ce5f-211">Scale unit count</span></span></li>
<li><span data-ttu-id="3ce5f-212">Edizione</span><span class="sxs-lookup"><span data-stu-id="3ce5f-212">Edition</span></span></li>
<li><span data-ttu-id="3ce5f-213">Versione prodotto</span><span class="sxs-lookup"><span data-stu-id="3ce5f-213">Product Version</span></span></li>
<li><span data-ttu-id="3ce5f-214">Area/data center</span><span class="sxs-lookup"><span data-stu-id="3ce5f-214">Region/Datacenter</span></span></li>
<li><span data-ttu-id="3ce5f-215">Spazio dei nomi e chiave del Servizio di controllo di accesso (ACS)</span><span class="sxs-lookup"><span data-stu-id="3ce5f-215">Access Control Service (ACS) namespace and key</span></span></li>
<li><span data-ttu-id="3ce5f-216">Rilevamento della stringa di connessione al database</span><span class="sxs-lookup"><span data-stu-id="3ce5f-216">Tracking database connection string</span></span></li>
<li><span data-ttu-id="3ce5f-217">Archiviazione della stringa di connessione all'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="3ce5f-217">Archiving Storage account connection string</span></span></li>
<li><span data-ttu-id="3ce5f-218">Monitoraggio della stringa di connessione all'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="3ce5f-218">Monitoring storage account connection string</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="3ce5f-219">
 <strong>Elementi aggiuntivi</strong></span><span class="sxs-lookup"><span data-stu-id="3ce5f-219">
 <strong>Additional Items</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="3ce5f-220">Database di rilevamento</span><span class="sxs-lookup"><span data-stu-id="3ce5f-220">Tracking Database</span></span></td> 
<td><span data-ttu-id="3ce5f-221">Quando viene creato hello BizTalk Service, vengono immessi i dettagli del Database di rilevamento hello inclusi hello Server di Database SQL di Azure e il nome di Database di rilevamento hello.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-221">When hello BizTalk Service is created, hello Tracking Database details are entered, including hello Azure SQL Database Server and hello Tracking Database name.</span></span> <span data-ttu-id="3ce5f-222">Hello Database di rilevamento non viene automaticamente eseguito il backup.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-222">hello Tracking Database is not automatically backed up.</span></span>
<br/><br/><span data-ttu-id="3ce5f-223">
<strong>Importante</strong></span><span class="sxs-lookup"><span data-stu-id="3ce5f-223">
<strong>Important</strong></span></span><br/>
<span data-ttu-id="3ce5f-224">Se hello Database di rilevamento viene eliminata e hello esigenze database ripristinate, deve esistere un backup precedente.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-224">If hello Tracking Database is deleted and hello database needs recovered, a previous backup must exist.</span></span> <span data-ttu-id="3ce5f-225">Se non esiste un backup, i Database di rilevamento hello e i relativi dati non sono recuperabili.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-225">If a backup does not exist, hello Tracking Database and its data are not recoverable.</span></span> <span data-ttu-id="3ce5f-226">In questo caso, creare un nuovo Database di rilevamento con hello stesso nome di database.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-226">In this situation, create a new Tracking Database with hello same database name.</span></span> <span data-ttu-id="3ce5f-227">È consigliata la replica geografica.</span><span class="sxs-lookup"><span data-stu-id="3ce5f-227">Geo-Replication is recommended.</span></span></td>
</tr> 
</table>

## <a name="next"></a><span data-ttu-id="3ce5f-228">Avanti</span><span class="sxs-lookup"><span data-stu-id="3ce5f-228">Next</span></span>
<span data-ttu-id="3ce5f-229">Servizi BizTalk di Azure toocreate in hello Azure classico, andare troppo[servizi BizTalk: portale classico di Provisioning tramite Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span><span class="sxs-lookup"><span data-stu-id="3ce5f-229">toocreate Azure BizTalk Services in hello Azure classic portal, go too[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span></span> <span data-ttu-id="3ce5f-230">creazione di applicazioni, andare troppo toostart[servizi BizTalk di Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="3ce5f-230">toostart creating applications, go too[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="3ce5f-231">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="3ce5f-231">See Also</span></span>
* [<span data-ttu-id="3ce5f-232">Backup del servizio BizTalk</span><span class="sxs-lookup"><span data-stu-id="3ce5f-232">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="3ce5f-233">Ripristino del servizio BizTalk da un backup</span><span class="sxs-lookup"><span data-stu-id="3ce5f-233">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="3ce5f-234">Servizi BizTalk: Grafico edizioni Developer, Basic, Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="3ce5f-234">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="3ce5f-235">Servizi BizTalk: effettuare il provisioning di un servizio BizTalk mediante il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="3ce5f-235">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="3ce5f-236">Servizi BizTalk: Tabella degli stati del servizio</span><span class="sxs-lookup"><span data-stu-id="3ce5f-236">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="3ce5f-237">Servizi BizTalk: Schede Dashboard, Monitoraggio, Scalabilità</span><span class="sxs-lookup"><span data-stu-id="3ce5f-237">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="3ce5f-238">Servizi BizTalk: limitazione</span><span class="sxs-lookup"><span data-stu-id="3ce5f-238">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="3ce5f-239">Servizi BizTalk: nome e chiave dell'autorità emittente</span><span class="sxs-lookup"><span data-stu-id="3ce5f-239">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="3ce5f-240">Come è possibile utilizzare hello Azure BizTalk Services SDK</span><span class="sxs-lookup"><span data-stu-id="3ce5f-240">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

