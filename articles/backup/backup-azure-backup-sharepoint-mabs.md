---
title: Usare il server di Backup di Azure per eseguire il backup di una farm di SharePoint in Azure | Microsoft Docs
description: "Usare il server di Backup di Azure per eseguire il backup e ripristinare i dati di SharePoint. In questo articolo vengono fornite le informazioni per configurare la farm di SharePoint in modo da archiviare in Azure i dati desiderati. È possibile ripristinare i dati SharePoint protetti dal disco o da Azure."
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: 34ba87a4-91f1-4054-a4a1-272af1e15496
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 3ed000affd326eb1bd7c99773ec021ad6e03cc3b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-a-sharepoint-farm-to-azure"></a><span data-ttu-id="09dae-105">Eseguire il backup di una farm di SharePoint in Azure</span><span class="sxs-lookup"><span data-stu-id="09dae-105">Back up a SharePoint farm to Azure</span></span>
<span data-ttu-id="09dae-106">Il backup di una farm di SharePoint in Azure si esegue tramite il server di Backup di Microsoft Azure (MABS) in modo analogo al backup delle altre origini dati.</span><span class="sxs-lookup"><span data-stu-id="09dae-106">You back up a SharePoint farm to Microsoft Azure by using Microsoft Azure Backup Server (MABS) in much the same way that you back up other data sources.</span></span> <span data-ttu-id="09dae-107">Backup di Azure offre flessibilità nella pianificazione di backup per creare punti di backup quotidiani, settimanali, mensili o annuali e offre diverse opzioni in termini di criteri di conservazione per i vari intervalli di backup.</span><span class="sxs-lookup"><span data-stu-id="09dae-107">Azure Backup provides flexibility in the backup schedule to create daily, weekly, monthly, or yearly backup points and gives you retention policy options for various backup points.</span></span> <span data-ttu-id="09dae-108">Offre inoltre la possibilità di archiviare copie dei dischi locali per obiettivi di tempi di ripristino (RTO) rapidi e di archiviare copie in Azure per una conservazione economicamente conveniente e a lungo termine.</span><span class="sxs-lookup"><span data-stu-id="09dae-108">It also provides the capability to store local disk copies for quick recovery-time objectives (RTO) and to store copies to Azure for economical, long-term retention.</span></span>

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a><span data-ttu-id="09dae-109">Versioni supportate di SharePoint e relativi scenari di protezione</span><span class="sxs-lookup"><span data-stu-id="09dae-109">SharePoint supported versions and related protection scenarios</span></span>
<span data-ttu-id="09dae-110">Backup di Azure per DPM supporta gli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="09dae-110">Azure Backup for DPM supports the following scenarios:</span></span>

| <span data-ttu-id="09dae-111">Carico di lavoro</span><span class="sxs-lookup"><span data-stu-id="09dae-111">Workload</span></span> | <span data-ttu-id="09dae-112">Versione</span><span class="sxs-lookup"><span data-stu-id="09dae-112">Version</span></span> | <span data-ttu-id="09dae-113">Distribuzione di SharePoint</span><span class="sxs-lookup"><span data-stu-id="09dae-113">SharePoint deployment</span></span> | <span data-ttu-id="09dae-114">Protezione e ripristino</span><span class="sxs-lookup"><span data-stu-id="09dae-114">Protection and recovery</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="09dae-115">SharePoint</span><span class="sxs-lookup"><span data-stu-id="09dae-115">SharePoint</span></span> |<span data-ttu-id="09dae-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span><span class="sxs-lookup"><span data-stu-id="09dae-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span></span> |<span data-ttu-id="09dae-117">SharePoint distribuito come un server fisico o macchina virtuale Hyper-V o VmWare</span><span class="sxs-lookup"><span data-stu-id="09dae-117">SharePoint deployed as a physical server or Hyper-V/VMware virtual machine</span></span> <br> -------------- <br> <span data-ttu-id="09dae-118">SQL AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="09dae-118">SQL AlwaysOn</span></span> | <span data-ttu-id="09dae-119">Proteggere le opzioni di ripristino di farm di SharePoint: farm di ripristino, database, e file o voce di elenco dai punti di ripristino del disco.</span><span class="sxs-lookup"><span data-stu-id="09dae-119">Protect SharePoint Farm recovery options: Recovery farm, database, and file or list item from disk recovery points.</span></span>  <span data-ttu-id="09dae-120">Farm e ripristino dei database dai punti di ripristino di Azure.</span><span class="sxs-lookup"><span data-stu-id="09dae-120">Farm and database recovery from Azure recovery points.</span></span> |

## <a name="before-you-start"></a><span data-ttu-id="09dae-121">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="09dae-121">Before you start</span></span>
<span data-ttu-id="09dae-122">È necessario verificare alcuni aspetti prima di eseguire il backup di una farm di SharePoint in Azure.</span><span class="sxs-lookup"><span data-stu-id="09dae-122">There are a few things you need to confirm before you back up a SharePoint farm to Azure.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="09dae-123">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="09dae-123">Prerequisites</span></span>
<span data-ttu-id="09dae-124">Prima di procedere, assicurarsi di avere [installato e preparato il server di Backup di Azure](backup-azure-microsoft-azure-backup.md) per proteggere i carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="09dae-124">Before you proceed, make sure that you have [installed and prepared the Azure Backup Server](backup-azure-microsoft-azure-backup.md) to protect workloads.</span></span>

### <a name="protection-agent"></a><span data-ttu-id="09dae-125">Agente protezione</span><span class="sxs-lookup"><span data-stu-id="09dae-125">Protection agent</span></span>
<span data-ttu-id="09dae-126">L'agente protezione deve essere installato nel server che esegue SharePoint, nei server che eseguono SQL Server e in tutti gli altri server che fanno parte della farm di SharePoint.</span><span class="sxs-lookup"><span data-stu-id="09dae-126">The Protection agent must be installed on the server that's running SharePoint, the servers that are running SQL Server, and all other servers that are part of the SharePoint farm.</span></span> <span data-ttu-id="09dae-127">Per altre informazioni sull'installazione dell'agente di protezione, vedere l'articolo relativo alla [configurazione dell'agente di protezione](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span><span class="sxs-lookup"><span data-stu-id="09dae-127">For more information about how to set up the protection agent, see [Setup Protection Agent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span></span>  <span data-ttu-id="09dae-128">L'unica eccezione è che l'agente viene installato in un server Web front-end (WFE) solo.</span><span class="sxs-lookup"><span data-stu-id="09dae-128">The one exception is that you install the agent only on a single web front end (WFE) server.</span></span> <span data-ttu-id="09dae-129">DPM ha bisogno che l'agente sia installato in un solo server WFE e agisca come punto di ingresso per la protezione.</span><span class="sxs-lookup"><span data-stu-id="09dae-129">DPM needs the agent on one WFE server only to serve as the entry point for protection.</span></span>

### <a name="sharepoint-farm"></a><span data-ttu-id="09dae-130">Una farm di SharePoint</span><span class="sxs-lookup"><span data-stu-id="09dae-130">SharePoint farm</span></span>
<span data-ttu-id="09dae-131">Per ogni 10 milioni di elementi nella farm, deve essere almeno disponibili 2 GB di spazio nel volume in cui si trova la cartella di MABS.</span><span class="sxs-lookup"><span data-stu-id="09dae-131">For every 10 million items in the farm, there must be at least 2 GB of space on the volume where the MABS folder is located.</span></span> <span data-ttu-id="09dae-132">Questo spazio è necessario per la generazione del catalogo.</span><span class="sxs-lookup"><span data-stu-id="09dae-132">This space is required for catalog generation.</span></span> <span data-ttu-id="09dae-133">Affinché MABS ripristini elementi specifici, ad esempio raccolte siti, siti, elenchi, raccolte documenti, cartelle, singoli documenti ed elementi di elenchi, la generazione del catalogo crea un elenco degli URL inclusi in ogni database del contenuto.</span><span class="sxs-lookup"><span data-stu-id="09dae-133">For MABS to recover specific items (site collections, sites, lists, document libraries, folders, individual documents, and list items), catalog generation creates a list of the URLs that are contained within each content database.</span></span> <span data-ttu-id="09dae-134">È possibile visualizzare l'elenco degli URL nel pannello degli elementi ripristinabili dell'area delle attività di **ripristino** della Console amministrazione MABS.</span><span class="sxs-lookup"><span data-stu-id="09dae-134">You can view the list of URLs in the recoverable item pane in the **Recovery** task area of MABS Administrator Console.</span></span>

### <a name="sql-server"></a><span data-ttu-id="09dae-135">SQL Server</span><span class="sxs-lookup"><span data-stu-id="09dae-135">SQL Server</span></span>
<span data-ttu-id="09dae-136">MABS viene eseguito come account LocalSystem.</span><span class="sxs-lookup"><span data-stu-id="09dae-136">MABS runs as a LocalSystem account.</span></span> <span data-ttu-id="09dae-137">Per eseguire il backup dei database di SQL Server, MABS deve avere privilegi sysadmin sull'account per il server che esegue SQL Server.</span><span class="sxs-lookup"><span data-stu-id="09dae-137">To back up SQL Server databases, MABS needs sysadmin privileges on that account for the server that's running SQL Server.</span></span> <span data-ttu-id="09dae-138">Impostare NT AUTHORITY\SYSTEM su *sysadmin* nel server che esegue SQL Server prima di eseguire il backup.</span><span class="sxs-lookup"><span data-stu-id="09dae-138">Set NT AUTHORITY\SYSTEM to *sysadmin* on the server that's running SQL Server before you back it up.</span></span>

<span data-ttu-id="09dae-139">Se la farm di SharePoint ha un database di SQL Server configurato con alias di SQL Server, installare i componenti del client di SQL Server nel server Web front-end da proteggere con MABS.</span><span class="sxs-lookup"><span data-stu-id="09dae-139">If the SharePoint farm has SQL Server databases that are configured with SQL Server aliases, install the SQL Server client components on the front-end Web server that MABS will protect.</span></span>

### <a name="sharepoint-server"></a><span data-ttu-id="09dae-140">SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="09dae-140">SharePoint Server</span></span>
<span data-ttu-id="09dae-141">Mentre le prestazioni dipendono da molti fattori, ad esempio la dimensione della farm di SharePoint, in linea generale un solo MABS può proteggere una farm di SharePoint da 25 TB.</span><span class="sxs-lookup"><span data-stu-id="09dae-141">While performance depends on many factors such as size of SharePoint farm, as general guidance one MABS can protect a 25 TB SharePoint farm.</span></span>

### <a name="whats-not-supported"></a><span data-ttu-id="09dae-142">Attività non supportate</span><span class="sxs-lookup"><span data-stu-id="09dae-142">What's not supported</span></span>
* <span data-ttu-id="09dae-143">MABS protegge una farm di SharePoint, ma non protegge gli indici di ricerca e i database di servizio dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="09dae-143">MABS that protects a SharePoint farm does not protect search indexes or application service databases.</span></span> <span data-ttu-id="09dae-144">Occorre configurare separatamente la protezione di questi database.</span><span class="sxs-lookup"><span data-stu-id="09dae-144">You will need to configure the protection of these databases separately.</span></span>
* <span data-ttu-id="09dae-145">MABS non esegue il backup dei database di SQL Server SharePoint ospitati in condivisioni di file server di scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="09dae-145">MABS does not provide backup of SharePoint SQL Server databases that are hosted on scale-out file server (SOFS) shares.</span></span>

## <a name="configure-sharepoint-protection"></a><span data-ttu-id="09dae-146">Configurare la protezione di SharePoint</span><span class="sxs-lookup"><span data-stu-id="09dae-146">Configure SharePoint protection</span></span>
<span data-ttu-id="09dae-147">Prima di usare MABS per proteggere SharePoint, è necessario configurare il servizio VSS Writer di SharePoint (servizio WSS Writer) tramite **ConfigureSharePoint.exe**.</span><span class="sxs-lookup"><span data-stu-id="09dae-147">Before you can use MABS to protect SharePoint, you must configure the SharePoint VSS Writer service (WSS Writer service) by using **ConfigureSharePoint.exe**.</span></span>

<span data-ttu-id="09dae-148">**ConfigureSharePoint.exe** è disponibile nella cartella [percorso di installazione di MABS]\bin nel server Web front-end.</span><span class="sxs-lookup"><span data-stu-id="09dae-148">You can find **ConfigureSharePoint.exe** in the [MABS Installation Path]\bin folder on the front-end web server.</span></span> <span data-ttu-id="09dae-149">Questo strumento fornisce all'agente protezione le credenziali per la farm di SharePoint.</span><span class="sxs-lookup"><span data-stu-id="09dae-149">This tool provides the protection agent with the credentials for the SharePoint farm.</span></span> <span data-ttu-id="09dae-150">È possibile eseguirlo in un unico server front-end Web.</span><span class="sxs-lookup"><span data-stu-id="09dae-150">You run it on a single WFE server.</span></span> <span data-ttu-id="09dae-151">Se si dispone di più server WFE, selezionarne solo uno quando si configura un gruppo di protezione dati.</span><span class="sxs-lookup"><span data-stu-id="09dae-151">If you have multiple WFE servers, select just one when you configure a protection group.</span></span>

### <a name="to-configure-the-sharepoint-vss-writer-service"></a><span data-ttu-id="09dae-152">Per configurare il servizio Writer VSS di SharePoint</span><span class="sxs-lookup"><span data-stu-id="09dae-152">To configure the SharePoint VSS Writer service</span></span>
1. <span data-ttu-id="09dae-153">Nel server WFE, al prompt dei comandi, passare a [percorso di installazione di MABS]\bin\\</span><span class="sxs-lookup"><span data-stu-id="09dae-153">On the WFE server, at a command prompt, go to [MABS installation location]\bin\\</span></span>
2. <span data-ttu-id="09dae-154">Digitare ConfigureSharePoint -EnableSharePointProtection.</span><span class="sxs-lookup"><span data-stu-id="09dae-154">Enter ConfigureSharePoint -EnableSharePointProtection.</span></span>
3. <span data-ttu-id="09dae-155">Immettere le credenziali di amministratore della farm.</span><span class="sxs-lookup"><span data-stu-id="09dae-155">Enter the farm administrator credentials.</span></span> <span data-ttu-id="09dae-156">Questo account deve essere un membro del gruppo degli amministratori locale nel server front-end Web.</span><span class="sxs-lookup"><span data-stu-id="09dae-156">This account should be a member of the local Administrator group on the WFE server.</span></span> <span data-ttu-id="09dae-157">Se l'amministratore della farm non è un amministratore locale, concedere le autorizzazioni seguenti sul server front-end Web:</span><span class="sxs-lookup"><span data-stu-id="09dae-157">If the farm administrator isn’t a local admin grant the following permissions on the WFE server:</span></span>
   * <span data-ttu-id="09dae-158">Concedere il controllo completo del gruppo WSS_Admin_WPG sulla cartella DPM (% Program Files%\Microsoft Azure Backup\DPM).</span><span class="sxs-lookup"><span data-stu-id="09dae-158">Grant the WSS_Admin_WPG group full control to the DPM folder (%Program Files%\Microsoft Azure Backup\DPM).</span></span>
   * <span data-ttu-id="09dae-159">Concedere l'accesso in lettura al gruppo WSS_Admin_WPG per la chiave del Registro di sistema di DPM (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span><span class="sxs-lookup"><span data-stu-id="09dae-159">Grant the WSS_Admin_WPG group read access to the DPM Registry key (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span></span>

> [!NOTE]
> <span data-ttu-id="09dae-160">È necessario eseguire di nuovo ConfigureSharePoint.exe ogni volta che si verifica un cambiamento nelle credenziali di amministratore di farm SharePoint.</span><span class="sxs-lookup"><span data-stu-id="09dae-160">You’ll need to rerun ConfigureSharePoint.exe whenever there’s a change in the SharePoint farm administrator credentials.</span></span>
>
>

## <a name="back-up-a-sharepoint-farm-by-using-mabs"></a><span data-ttu-id="09dae-161">Eseguire il backup di una farm di SharePoint tramite MABS</span><span class="sxs-lookup"><span data-stu-id="09dae-161">Back up a SharePoint farm by using MABS</span></span>
<span data-ttu-id="09dae-162">Dopo aver configurato MABS e la farm di SharePoint come descritto in precedenza, è possibile proteggere SharePoint con MABS.</span><span class="sxs-lookup"><span data-stu-id="09dae-162">After you have configured MABS and the SharePoint farm as explained previously, SharePoint can be protected by MABS.</span></span>

### <a name="to-protect-a-sharepoint-farm"></a><span data-ttu-id="09dae-163">Per proteggere una farm di SharePoint</span><span class="sxs-lookup"><span data-stu-id="09dae-163">To protect a SharePoint farm</span></span>
1. <span data-ttu-id="09dae-164">Dalla scheda **Protezione** della Console di amministrazione MABS fare clic su **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="09dae-164">From the **Protection** tab of the MABS Administrator Console, click **New**.</span></span>
    <span data-ttu-id="09dae-165">![Nuova scheda Protezione](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span><span class="sxs-lookup"><span data-stu-id="09dae-165">![New Protection Tab](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span></span>
2. <span data-ttu-id="09dae-166">Nella pagina **Seleziona tipo di gruppo protezione dati** della procedura guidata **Crea nuovo gruppo protezione dati** selezionare **Server** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="09dae-166">On the **Select Protection Group Type** page of the **Create New Protection Group** wizard, select **Servers**, and then click **Next**.</span></span>

    ![Seleziona tipo di gruppo di protezione dati](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. <span data-ttu-id="09dae-168">Nella schermata **Seleziona membri del gruppo** selezionare la casella di controllo del server di SharePoint che si vuole proteggere e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="09dae-168">On the **Select Group Members** screen, select the check box for the SharePoint server you want to protect and click **Next**.</span></span>

    ![Seleziona membri del gruppo](./media/backup-azure-backup-sharepoint/select-group-members2.png)

   > [!NOTE]
   > <span data-ttu-id="09dae-170">Con l'agente protezione installato, è possibile visualizzare il server della procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="09dae-170">With the protection agent installed, you can see the server in the wizard.</span></span> <span data-ttu-id="09dae-171">MABS mostra anche la propria struttura.</span><span class="sxs-lookup"><span data-stu-id="09dae-171">MABS also shows its structure.</span></span> <span data-ttu-id="09dae-172">Poiché è stato eseguito ConfigureSharePoint.exe, MABS comunica con il servizio VSS Writer di SharePoint e con i relativi database di SQL Server e riconosce la struttura della farm di SharePoint, i database del contenuto associati e tutti gli elementi corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="09dae-172">Because you ran ConfigureSharePoint.exe, MABS communicates with the SharePoint VSS Writer service and its corresponding SQL Server databases and recognizes the SharePoint farm structure, the associated content databases, and any corresponding items.</span></span>
   >
   >
4. <span data-ttu-id="09dae-173">Nella pagina **Seleziona metodo protezione dati** digitare il nome del **Gruppo protezione dati** e selezionare i *metodi di protezione* preferiti.</span><span class="sxs-lookup"><span data-stu-id="09dae-173">On the **Select Data Protection Method** page, enter the name of the **Protection Group**, and select your preferred *protection methods*.</span></span> <span data-ttu-id="09dae-174">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="09dae-174">Click **Next**.</span></span>

    ![Seleziona metodo protezione dati](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)

   > [!NOTE]
   > <span data-ttu-id="09dae-176">Il metodo di protezione del disco consente di soddisfare obiettivi di tempi di ripristino brevi.</span><span class="sxs-lookup"><span data-stu-id="09dae-176">The disk protection method helps to meet short recovery-time objectives.</span></span>
   >
   >
5. <span data-ttu-id="09dae-177">Nella pagina **Specifica obiettivi a breve termine** selezionare l'**intervallo di conservazione** preferito e specificare la frequenza di esecuzione dei backup.</span><span class="sxs-lookup"><span data-stu-id="09dae-177">On the **Specify Short-Term Goals** page, select your preferred **Retention range** and identify when you want backups to occur.</span></span>

    ![Specifica obiettivi a breve termine](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)

   > [!NOTE]
   > <span data-ttu-id="09dae-179">Poiché è molto spesso richiesto il ripristino di dati con data di creazione inferiore a cinque giorni, in questo esempio è stato selezionato un periodo di conservazione sul disco di cinque giorni ed è stato specificato che il backup non venga eseguito durante orari lavorativi.</span><span class="sxs-lookup"><span data-stu-id="09dae-179">Because recovery is most often required for data that's less than five days old, we selected a retention range of five days on disk and ensured that the backup happens during non-production hours, for this example.</span></span>
   >
   >
6. <span data-ttu-id="09dae-180">Esaminare lo spazio su disco del pool di archiviazione allocato per il gruppo protezione dati e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="09dae-180">Review the storage pool disk space allocated for the protection group, and click then **Next**.</span></span>
7. <span data-ttu-id="09dae-181">Per ogni gruppo protezione dati MABS alloca spazio su disco per archiviare e gestire le repliche.</span><span class="sxs-lookup"><span data-stu-id="09dae-181">For every protection group, MABS allocates disk space to store and manage replicas.</span></span> <span data-ttu-id="09dae-182">A questo punto, MABS deve creare una copia dei dati selezionati.</span><span class="sxs-lookup"><span data-stu-id="09dae-182">At this point, MABS must create a copy of the selected data.</span></span> <span data-ttu-id="09dae-183">Selezionare come e quando si vuole che la replica venga creata, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="09dae-183">Select how and when you want the replica created, and then click **Next**.</span></span>

    ![Scelta del metodo per la creazione della replica](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)

   > [!NOTE]
   > <span data-ttu-id="09dae-185">Per assicurarsi che il traffico di rete non venga influenzato, selezionare un'ora fuori dell'orario di produzione.</span><span class="sxs-lookup"><span data-stu-id="09dae-185">To make sure that network traffic is not effected, select a time outside production hours.</span></span>
   >
   >
8. <span data-ttu-id="09dae-186">MABS garantisce l'integrità dei dati mediante l'esecuzione di verifiche della coerenza sulla replica.</span><span class="sxs-lookup"><span data-stu-id="09dae-186">MABS ensures data integrity by performing consistency checks on the replica.</span></span> <span data-ttu-id="09dae-187">Sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="09dae-187">There are two available options.</span></span> <span data-ttu-id="09dae-188">È possibile definire una pianificazione per eseguire verifiche della coerenza oppure DPM può eseguire automaticamente verifiche di coerenza sulla replica quando diventa incoerente. </span><span class="sxs-lookup"><span data-stu-id="09dae-188">You can define a schedule to run consistency checks, or DPM can run consistency checks automatically on the replica whenever it becomes inconsistent.</span></span> <span data-ttu-id="09dae-189">Selezionare l'opzione preferita e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="09dae-189">Select your preferred option, and then click **Next**.</span></span>

    ![Verifica coerenza](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. <span data-ttu-id="09dae-191">Nella pagina **Specifica i dati da proteggere online** selezionare la farm di SharePoint che si vuole proteggere e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="09dae-191">On the **Specify Online Protection Data** page, select the SharePoint farm that you want to protect, and then click **Next**.</span></span>

    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. <span data-ttu-id="09dae-193">Nella pagina **Specifica la pianificazione dei backup online** selezionare la pianificazione preferita e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="09dae-193">On the **Specify Online Backup Schedule** page, select your preferred schedule, and then click **Next**.</span></span>

    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="09dae-195">MABS fornisce un massimo di due backup giornalieri in Azure dal punto di backup del disco più recente disponibile in quel momento.</span><span class="sxs-lookup"><span data-stu-id="09dae-195">MABS provides a maximum of two daily backups to Azure from the then available latest disk backup point.</span></span> <span data-ttu-id="09dae-196">Backup di Azure può inoltre controllare la quantità di larghezza di banda WAN che può essere usata per i backup in orari normali e di punta tramite la [limitazione della larghezza di bada della rete di Backup di Azure](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span><span class="sxs-lookup"><span data-stu-id="09dae-196">Azure Backup can also control the amount of WAN bandwidth that can be used for backups in peak and off-peak hours by using [Azure Backup Network Throttling](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span></span>
    >
    >
11. <span data-ttu-id="09dae-197">In base alla pianificazione di backup selezionata, nella pagina **Specificare i criteri di mantenimento online** selezionare i criteri di conservazione per i punti di backup giornalieri, settimanali, mensili e annuali.</span><span class="sxs-lookup"><span data-stu-id="09dae-197">Depending on the backup schedule that you selected, on the **Specify Online Retention Policy** page, select the retention policy for daily, weekly, monthly, and yearly backup points.</span></span>

    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)

    > [!NOTE]
    > <span data-ttu-id="09dae-199">MABS usa uno schema di conservazione GFS (Grandfather-Father-Son, nonno-padre-figlio) in cui è possibile scegliere criteri di conservazione diversi per punti di backup diversi.</span><span class="sxs-lookup"><span data-stu-id="09dae-199">MABS uses a grandfather-father-son retention scheme in which a different retention policy can be chosen for different backup points.</span></span>
    >
    >
12. <span data-ttu-id="09dae-200">Analogamente al disco, è necessario creare una replica del punto di riferimento iniziale in Azure.</span><span class="sxs-lookup"><span data-stu-id="09dae-200">Similar to disk, an initial reference point replica needs to be created in Azure.</span></span> <span data-ttu-id="09dae-201">Selezionare l'opzione preferita per creare una copia di backup iniziale in Azure e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="09dae-201">Select your preferred option to create an initial backup copy to Azure, and then click **Next**.</span></span>

    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. <span data-ttu-id="09dae-203">Esaminare le impostazioni selezionate nella pagina di **riepilogo** e fare clic su **Crea gruppo**.</span><span class="sxs-lookup"><span data-stu-id="09dae-203">Review your selected settings on the **Summary** page, and then click **Create Group**.</span></span> <span data-ttu-id="09dae-204">Dopo aver creato il gruppo di protezione dati, viene visualizzato un messaggio di corretto completamento.</span><span class="sxs-lookup"><span data-stu-id="09dae-204">You will see a success message after the protection group has been created.</span></span>

    ![Riepilogo](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-mabs"></a><span data-ttu-id="09dae-206">Ripristinare un elemento di SharePoint dal disco tramite MABS</span><span class="sxs-lookup"><span data-stu-id="09dae-206">Restore a SharePoint item from disk by using MABS</span></span>
<span data-ttu-id="09dae-207">Nell'esempio seguente, l' *elemento di SharePoint da ripristinare* è stato accidentalmente eliminato e deve essere ripristinato.</span><span class="sxs-lookup"><span data-stu-id="09dae-207">In the following example, the *Recovering SharePoint item* has been accidentally deleted and needs to be recovered.</span></span>
<span data-ttu-id="09dae-208">![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span><span class="sxs-lookup"><span data-stu-id="09dae-208">![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span></span>

1. <span data-ttu-id="09dae-209">Aprire la **Console amministrazione DPM**.</span><span class="sxs-lookup"><span data-stu-id="09dae-209">Open the **DPM Administrator Console**.</span></span> <span data-ttu-id="09dae-210">Tutte le farm di SharePoint protette da DPM vengono visualizzate nella scheda **Protezione** .</span><span class="sxs-lookup"><span data-stu-id="09dae-210">All SharePoint farms that are protected by DPM are shown in the **Protection** tab.</span></span>

    ![MABS SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. <span data-ttu-id="09dae-212">Per iniziare a ripristinare l'elemento, selezionare la scheda **Ripristino** .</span><span class="sxs-lookup"><span data-stu-id="09dae-212">To begin to recover the item, select the **Recovery** tab.</span></span>

    ![MABS SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. <span data-ttu-id="09dae-214">È possibile eseguire ricerche in SharePoint relative all' *elemento di SharePoint da ripristinare* tramite una ricerca con caratteri jolly all'interno di un intervallo di punti di ripristino.</span><span class="sxs-lookup"><span data-stu-id="09dae-214">You can search SharePoint for *Recovering SharePoint item* by using a wildcard-based search within a recovery point range.</span></span>

    ![MABS SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. <span data-ttu-id="09dae-216">Selezionare il punto di ripristino appropriato dai risultati della ricerca, fare clic con il pulsante destro del mouse sull'elemento e selezionare **Ripristina**.</span><span class="sxs-lookup"><span data-stu-id="09dae-216">Select the appropriate recovery point from the search results, right-click the item, and then select **Recover**.</span></span>
5. <span data-ttu-id="09dae-217">È inoltre possibile scorrere i vari punti di ripristino e selezionare un database o un elemento da recuperare.</span><span class="sxs-lookup"><span data-stu-id="09dae-217">You can also browse through various recovery points and select a database or item to recover.</span></span> <span data-ttu-id="09dae-218">Selezionare **Data > Tempo di ripristino**, quindi selezionare l'elemento corretto da **Database > Farm SharePoint > Punto di ripristino > Elemento**.</span><span class="sxs-lookup"><span data-stu-id="09dae-218">Select **Date > Recovery time**, and then select the correct **Database > SharePoint farm > Recovery point > Item**.</span></span>

    ![MABS SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. <span data-ttu-id="09dae-220">Fare clic con il pulsante destro del mouse sull'elemento e selezionare **Ripristina** per aprire il **Ripristino guidato**.</span><span class="sxs-lookup"><span data-stu-id="09dae-220">Right-click the item, and then select **Recover** to open the **Recovery Wizard**.</span></span> <span data-ttu-id="09dae-221">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="09dae-221">Click **Next**.</span></span>

    ![Verifica selezione per ripristino](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. <span data-ttu-id="09dae-223">Selezionare il tipo di ripristino che si vuole eseguire, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="09dae-223">Select the type of recovery that you want to perform, and then click **Next**.</span></span>

    ![Tipo di ripristino](./media/backup-azure-backup-sharepoint/select-recovery-type.png)

   > [!NOTE]
   > <span data-ttu-id="09dae-225">In questo esempio, la selezione di **Ripristina originale** ripristina l'elemento nel sito originale di SharePoint.</span><span class="sxs-lookup"><span data-stu-id="09dae-225">The selection of **Recover to original** in the example recovers the item to the original SharePoint site.</span></span>
   >
   >
8. <span data-ttu-id="09dae-226">Selezionare il **processo di ripristino** che si vuole usare.</span><span class="sxs-lookup"><span data-stu-id="09dae-226">Select the **Recovery Process** that you want to use.</span></span>

   * <span data-ttu-id="09dae-227">Selezionare **Ripristina senza utilizzare una farm di ripristino** se la farm di SharePoint non è stata modificata e corrisponde al punto di ripristino eseguito.</span><span class="sxs-lookup"><span data-stu-id="09dae-227">Select **Recover without using a recovery farm** if the SharePoint farm has not changed and is the same as the recovery point that is being restored.</span></span>
   * <span data-ttu-id="09dae-228">Selezionare **Ripristina utilizzando una farm di ripristino** se la farm di SharePoint è stato modificata dopo che il punto di ripristino è stato creato.</span><span class="sxs-lookup"><span data-stu-id="09dae-228">Select **Recover using a recovery farm** if the SharePoint farm has changed since the recovery point was created.</span></span>

     ![processo di ripristino](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. <span data-ttu-id="09dae-230">Specificare un percorso di istanza di gestione temporanea di SQL Server per ripristinare temporaneamente il database e specificare una condivisione di file di gestione temporanea in MABS e nel server che esegue SharePoint per ripristinare l'elemento.</span><span class="sxs-lookup"><span data-stu-id="09dae-230">Provide a staging SQL Server instance location to recover the database temporarily, and provide a staging file share on MABS and the server that's running SharePoint to recover the item.</span></span>

    ![Staging Location1](./media/backup-azure-backup-sharepoint/staging-location1.png)

    <span data-ttu-id="09dae-232">MABS collega il database del contenuto che ospita l'elemento di SharePoint all'istanza di gestione temporanea di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="09dae-232">MABS attaches the content database that is hosting the SharePoint item to the temporary SQL Server instance.</span></span> <span data-ttu-id="09dae-233">MABS ripristina l'elemento dal database del contenuto e lo aggiunge al percorso di file di gestione temporanea di MABS.</span><span class="sxs-lookup"><span data-stu-id="09dae-233">From the content database, it recovers the item and puts it on the staging file location on MABS.</span></span> <span data-ttu-id="09dae-234">L'elemento recuperato che si trova nel percorso di gestione temporanea deve ora essere esportato nel percorso di gestione temporaneo della farm di SharePoint.</span><span class="sxs-lookup"><span data-stu-id="09dae-234">The recovered item that's on the staging location now needs to be exported to the staging location on the SharePoint farm.</span></span>

    ![Gestione temporanea Location2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. <span data-ttu-id="09dae-236">Selezionare **Specifica opzioni di ripristino**e applicare le impostazioni di sicurezza per la farm di SharePoint o applicare le impostazioni di sicurezza del punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="09dae-236">Select **Specify recovery options**, and apply security settings to the SharePoint farm or apply the security settings of the recovery point.</span></span> <span data-ttu-id="09dae-237">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="09dae-237">Click **Next**.</span></span>

    ![Opzioni di ripristino](./media/backup-azure-backup-sharepoint/recovery-options.png)

    > [!NOTE]
    > <span data-ttu-id="09dae-239">È possibile scegliere di limitare l'utilizzo della larghezza di banda di rete.</span><span class="sxs-lookup"><span data-stu-id="09dae-239">You can choose to throttle the network bandwidth usage.</span></span> <span data-ttu-id="09dae-240">Consente di ridurre l'impatto sul server di produzione durante l'orario di produzione.</span><span class="sxs-lookup"><span data-stu-id="09dae-240">This minimizes impact to the production server during production hours.</span></span>
    >
    >
11. <span data-ttu-id="09dae-241">Esaminare le informazioni di riepilogo e fare clic su **Ripristina** per avviare il ripristino del file.</span><span class="sxs-lookup"><span data-stu-id="09dae-241">Review the summary information, and then click **Recover** to begin recovery of the file.</span></span>

    ![Riepilogo di ripristino](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. <span data-ttu-id="09dae-243">Selezionare la scheda **Monitoraggio** nella **Console di amministrazione MABS** per visualizzare lo **Stato** del ripristino.</span><span class="sxs-lookup"><span data-stu-id="09dae-243">Now select the **Monitoring** tab in the **MABS Administrator Console** to view the **Status** of the recovery.</span></span>

    ![Stato di ripristino](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)

    > [!NOTE]
    > <span data-ttu-id="09dae-245">A questo punto è possibile ripristinare il file.</span><span class="sxs-lookup"><span data-stu-id="09dae-245">The file is now restored.</span></span> <span data-ttu-id="09dae-246">È possibile aggiornare il sito di SharePoint per controllare il file ripristinato.</span><span class="sxs-lookup"><span data-stu-id="09dae-246">You can refresh the SharePoint site to check the restored file.</span></span>
    >
    >

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a><span data-ttu-id="09dae-247">Ripristinare un database di SharePoint da Azure tramite DPM</span><span class="sxs-lookup"><span data-stu-id="09dae-247">Restore a SharePoint database from Azure by using DPM</span></span>
1. <span data-ttu-id="09dae-248">Per ripristinare un database del contenuto di SharePoint, scorrere i vari punti di ripristino (come illustrato in precedenza) e selezionare il punto di ripristino che si vuole ripristinare.</span><span class="sxs-lookup"><span data-stu-id="09dae-248">To recover a SharePoint content database, browse through various recovery points (as shown previously), and select the recovery point that you want to restore.</span></span>

    ![MABS SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. <span data-ttu-id="09dae-250">Fare doppio clic sul punto di ripristino di SharePoint per visualizzare le informazioni del catalogo di SharePoint disponibili.</span><span class="sxs-lookup"><span data-stu-id="09dae-250">Double-click the SharePoint recovery point to show the available SharePoint catalog information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="09dae-251">Poiché la farm di SharePoint è protetta per la conservazione a lungo termine in Azure, non è disponibile nessuna informazione sul catalogo (metadati) in MABS.</span><span class="sxs-lookup"><span data-stu-id="09dae-251">Because the SharePoint farm is protected for long-term retention in Azure, no catalog information (metadata) is available on MABS.</span></span> <span data-ttu-id="09dae-252">Di conseguenza, ogni volta che si vuole ripristinare un database del contenuto di SharePoint temporizzato, si deve ricatalogare la farm di SharePoint.</span><span class="sxs-lookup"><span data-stu-id="09dae-252">As a result, whenever a point-in-time SharePoint content database needs to be recovered, you need to catalog the SharePoint farm again.</span></span>
   >
   >
3. <span data-ttu-id="09dae-253">Fare clic su **Ricatalogazione**.</span><span class="sxs-lookup"><span data-stu-id="09dae-253">Click **Re-catalog**.</span></span>

    ![MABS SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)

    <span data-ttu-id="09dae-255">Viene visualizzata la finestra di stato di **Ricatalogazione cloud** .</span><span class="sxs-lookup"><span data-stu-id="09dae-255">The **Cloud Recatalog** status window opens.</span></span>

    ![MABS SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)

    <span data-ttu-id="09dae-257">Dopo aver completato la catalogazione, viene visualizzato lo stato *Operazione completata*.</span><span class="sxs-lookup"><span data-stu-id="09dae-257">After cataloging is finished, the status changes to *Success*.</span></span> <span data-ttu-id="09dae-258">Fare clic su **Close**.</span><span class="sxs-lookup"><span data-stu-id="09dae-258">Click **Close**.</span></span>

    ![MABS SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. <span data-ttu-id="09dae-260">Fare clic sull'oggetto di SharePoint visualizzato nella scheda **Ripristino** di MABS per ottenere la struttura del database del contenuto.</span><span class="sxs-lookup"><span data-stu-id="09dae-260">Click the SharePoint object shown in the MABS **Recovery** tab to get the content database structure.</span></span> <span data-ttu-id="09dae-261">Fare clic con il pulsante destro del mouse sull'elemento e scegliere **Ripristina**.</span><span class="sxs-lookup"><span data-stu-id="09dae-261">Right-click the item, and then click **Recover**.</span></span>

    ![MABS SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. <span data-ttu-id="09dae-263">A questo punto seguire i [passaggi di ripristino illustrati precedentemente in questo articolo](#restore-a-sharepoint-item-from-disk-using-dpm) per ripristinare il database del contenuto di SharePoint dal disco.</span><span class="sxs-lookup"><span data-stu-id="09dae-263">At this point, follow the [recovery steps earlier in this article](#restore-a-sharepoint-item-from-disk-using-dpm) to recover a SharePoint content database from disk.</span></span>

## <a name="faqs"></a><span data-ttu-id="09dae-264">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="09dae-264">FAQs</span></span>
<span data-ttu-id="09dae-265">D: è possibile ripristinare un elemento di SharePoint nel percorso originale se SharePoint è configurato con SQL AlwaysOn (con protezione su disco)?</span><span class="sxs-lookup"><span data-stu-id="09dae-265">Q: Can I recover a SharePoint item to the original location if SharePoint is configured by using SQL AlwaysOn (with protection on disk)?</span></span><br>
<span data-ttu-id="09dae-266">R: Sì, l'elemento può essere ripristinato nel sito originale di SharePoint.</span><span class="sxs-lookup"><span data-stu-id="09dae-266">A: Yes, the item can be recovered to the original SharePoint site.</span></span>

<span data-ttu-id="09dae-267">D: è possibile ripristinare un database di SharePoint nel percorso originale se SharePoint è configurato con SQL AlwaysOn?</span><span class="sxs-lookup"><span data-stu-id="09dae-267">Q: Can I recover a SharePoint database to the original location if SharePoint is configured by using SQL AlwaysOn?</span></span><br>
<span data-ttu-id="09dae-268">R: poiché i database di SharePoint sono configurati con SQL AlwaysOn, non possono essere modificati se non si rimuove il gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="09dae-268">A: Because SharePoint databases are configured in SQL AlwaysOn, they cannot be modified unless the availability group is removed.</span></span> <span data-ttu-id="09dae-269">Di conseguenza MABS non può ripristinare il database nel percorso originale.</span><span class="sxs-lookup"><span data-stu-id="09dae-269">As a result, MABS cannot restore a database to the original location.</span></span> <span data-ttu-id="09dae-270">È possibile ripristinare un database di SQL Server in un'altra istanza di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="09dae-270">You can recover a SQL Server database to another SQL Server instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09dae-271">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="09dae-271">Next steps</span></span>
* <span data-ttu-id="09dae-272">Per altre informazioni su Protezione MABS di SharePoint, vedere [Serie di Video - Protezione DPM di SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span><span class="sxs-lookup"><span data-stu-id="09dae-272">Learn more about MABS Protection of SharePoint - see [Video Series - DPM Protection of SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span></span>
