---
title: in Azure SQL Data Warehouse aaaAuditing | Documenti Microsoft
description: Introduzione al servizio di controllo di Azure SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 0e6af148-b218-4b43-bb5f-907917d20330
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 08/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 948de74fa052ef206cf1aa65c0d81f084b18cb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a><span data-ttu-id="05c0b-103">Servizio di controllo di Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="05c0b-103">Auditing in Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="05c0b-104">Controllo</span><span class="sxs-lookup"><span data-stu-id="05c0b-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="05c0b-105">Introduzione al rilevamento delle minacce</span><span class="sxs-lookup"><span data-stu-id="05c0b-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

<span data-ttu-id="05c0b-106">Il controllo di SQL Data Warehouse consente toorecord eventi nel Registro di controllo tooan database nell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="05c0b-106">SQL Data Warehouse auditing allows you toorecord events in your database tooan audit log in your Azure Storage account.</span></span> <span data-ttu-id="05c0b-107">Il controllo consente di agevolare la conformità alle normative, comprendere le attività del database e ottenere informazioni su eventuali discrepanze e anomalie che potrebbero indicare problemi aziendali o sospette violazioni della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="05c0b-107">Auditing can help you maintain regulatory compliance, understand  database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span> <span data-ttu-id="05c0b-108">La funzionalità di controllo di SQL Data Warehouse si integra inoltre con Microsoft Power BI per l'esecuzione di analisi e report drill-down.</span><span class="sxs-lookup"><span data-stu-id="05c0b-108">SQL Data Warehouse auditing also integrates with Microsoft Power BI for drill-down reporting and analysis.</span></span>

<span data-ttu-id="05c0b-109">Gli strumenti di controllo abilitano e semplificare la conformità toocompliance standard, ma non garantiscono la conformità.</span><span class="sxs-lookup"><span data-stu-id="05c0b-109">Auditing tools enable and facilitate adherence toocompliance standards but don't guarantee compliance.</span></span> <span data-ttu-id="05c0b-110">Per ulteriori informazioni su Azure programmi tale conformità agli standard di supporto, vedere hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span><span class="sxs-lookup"><span data-stu-id="05c0b-110">For more information about Azure programs that support standards compliance, see hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span></span>

* <span data-ttu-id="05c0b-111">[Nozioni di base sul controllo del database]</span><span class="sxs-lookup"><span data-stu-id="05c0b-111">[Database Auditing basics]</span></span>
* <span data-ttu-id="05c0b-112">[Configurare il controllo per il database]</span><span class="sxs-lookup"><span data-stu-id="05c0b-112">[Set up auditing for your database]</span></span>
* <span data-ttu-id="05c0b-113">[Analizzare i log di controllo e i report]</span><span class="sxs-lookup"><span data-stu-id="05c0b-113">[Analyze audit logs and reports]</span></span>

## <span data-ttu-id="05c0b-114"><a id="subheading-1"></a>Nozioni di base sul controllo del database di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="05c0b-114"><a id="subheading-1"></a>Azure SQL Data Warehouse Database Auditing basics</span></span>
<span data-ttu-id="05c0b-115">Il controllo del database SQL Data Warehouse consente di:</span><span class="sxs-lookup"><span data-stu-id="05c0b-115">SQL Data Warehouse database auditing allows you to:</span></span>

* <span data-ttu-id="05c0b-116">**Conservare** un audit trail di eventi selezionati.</span><span class="sxs-lookup"><span data-stu-id="05c0b-116">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="05c0b-117">È possibile definire le categorie di database azioni toobe controllato.</span><span class="sxs-lookup"><span data-stu-id="05c0b-117">You can define categories of database actions  toobe audited.</span></span>
* <span data-ttu-id="05c0b-118">**Creare report** sulle attività del database.</span><span class="sxs-lookup"><span data-stu-id="05c0b-118">**Report** on database activity.</span></span> <span data-ttu-id="05c0b-119">È possibile utilizzare i report preconfigurati e tooget un dashboard iniziare rapidamente con attività e la notifica degli eventi.</span><span class="sxs-lookup"><span data-stu-id="05c0b-119">You can use preconfigured reports and a dashboard tooget started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="05c0b-120">**Analizzare** i report.</span><span class="sxs-lookup"><span data-stu-id="05c0b-120">**Analyze** reports.</span></span> <span data-ttu-id="05c0b-121">È possibile individuare eventi sospetti, attività insolite e tendenze.</span><span class="sxs-lookup"><span data-stu-id="05c0b-121">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="05c0b-122">È possibile configurare il controllo per hello seguenti categorie di eventi:</span><span class="sxs-lookup"><span data-stu-id="05c0b-122">You can configure auditing for hello following event categories:</span></span>

<span data-ttu-id="05c0b-123">**Normale SQL** e **SQL con parametri** per cui hello i log di controllo raccolti sono classificati come</span><span class="sxs-lookup"><span data-stu-id="05c0b-123">**Plain SQL** and **Parameterized SQL** for which hello collected audit logs are classified as</span></span>  

* <span data-ttu-id="05c0b-124">**Accesso toodata**</span><span class="sxs-lookup"><span data-stu-id="05c0b-124">**Access toodata**</span></span>
* <span data-ttu-id="05c0b-125">**Modifiche dello schema (DDL)**</span><span class="sxs-lookup"><span data-stu-id="05c0b-125">**Schema changes (DDL)**</span></span>
* <span data-ttu-id="05c0b-126">**Modifiche dei dati (DML)**</span><span class="sxs-lookup"><span data-stu-id="05c0b-126">**Data changes (DML)**</span></span>
* <span data-ttu-id="05c0b-127">**Account, ruoli e autorizzazioni (DCL)**</span><span class="sxs-lookup"><span data-stu-id="05c0b-127">**Accounts, roles, and permissions (DCL)**</span></span>
* <span data-ttu-id="05c0b-128">**Stored procedure**, **accesso** e **gestione delle transazioni**.</span><span class="sxs-lookup"><span data-stu-id="05c0b-128">**Stored Procedure**, **Login** and, **Transaction Management**.</span></span>

<span data-ttu-id="05c0b-129">Per ogni categoria di eventi, il controllo delle operazioni **riuscite** e **non riuscite** viene configurato separatamente.</span><span class="sxs-lookup"><span data-stu-id="05c0b-129">For each Event Category, Auditing of **Success** and **Failure** operations are configured separately.</span></span>

<span data-ttu-id="05c0b-130">Per ulteriori informazioni sulle attività di hello e gli eventi controllati, vedere hello <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">riferimento di formato di Log di controllo (download di file doc)</a>.</span><span class="sxs-lookup"><span data-stu-id="05c0b-130">For more information about hello activities and events audited, see hello <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Audit Log Format Reference (doc file download)</a>.</span></span>

<span data-ttu-id="05c0b-131">I log di controllo vengono archiviati nell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="05c0b-131">Audit logs are stored in your Azure storage account.</span></span> <span data-ttu-id="05c0b-132">È possibile definire un periodo di conservazione del log di controllo.</span><span class="sxs-lookup"><span data-stu-id="05c0b-132">You can define an audit log retention period.</span></span>

<span data-ttu-id="05c0b-133">Un criterio di controllo può essere definito per un database specifico o come criterio server predefinito.</span><span class="sxs-lookup"><span data-stu-id="05c0b-133">An auditing policy can be defined for a specific database or as a default server policy.</span></span> <span data-ttu-id="05c0b-134">Un criterio di controllo del server predefinito si applica tooall database in un server, che non dispongono di un override database controllo definiti criteri specifici.</span><span class="sxs-lookup"><span data-stu-id="05c0b-134">A default server auditing policy applies tooall databases on a server, which do not have a specific overriding database auditing policy defined.</span></span>

<span data-ttu-id="05c0b-135">Prima di impostare il controllo, verificare che si stia usando un [client di livello inferiore](sql-data-warehouse-auditing-downlevel-clients.md).</span><span class="sxs-lookup"><span data-stu-id="05c0b-135">Before setting up audit auditing check if you are using a ["Downlevel Client."](sql-data-warehouse-auditing-downlevel-clients.md)</span></span>

## <span data-ttu-id="05c0b-136"><a id="subheading-2"></a>Configurare il controllo per il database</span><span class="sxs-lookup"><span data-stu-id="05c0b-136"><a id="subheading-2"></a>Set up auditing for your database</span></span>
1. <span data-ttu-id="05c0b-137">Avviare hello <a href="https://portal.azure.com" target="_blank">portale di Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="05c0b-137">Launch hello <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span></span>
2. <span data-ttu-id="05c0b-138">Passare toohello **impostazioni** blade di hello desiderato tooaudit SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="05c0b-138">Go toohello **Settings** blade of hello SQL Data Warehouse you want tooaudit.</span></span> <span data-ttu-id="05c0b-139">In hello **impostazioni** pannello seleziona **rilevamento controllo & minaccia**.</span><span class="sxs-lookup"><span data-stu-id="05c0b-139">In hello **Settings** blade, select **Auditing & Threat detection**.</span></span>
   
    ![][1]
3. <span data-ttu-id="05c0b-140">Successivamente, abilitare il controllo, fare clic su hello **ON** pulsante.</span><span class="sxs-lookup"><span data-stu-id="05c0b-140">Next, enable auditing by clicking hello **ON** button.</span></span>
   
    ![][3]
4. <span data-ttu-id="05c0b-141">Nel Pannello di configurazione di controllo di hello, selezionare **dettagli archiviazione** Pannello di controllo log archiviazione tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="05c0b-141">In hello auditing configuration blade, select **STORAGE DETAILS** tooopen hello Audit Logs Storage blade.</span></span> <span data-ttu-id="05c0b-142">Selezionare account di archiviazione di Azure in cui verranno salvati i log hello e hello periodo di memorizzazione.</span><span class="sxs-lookup"><span data-stu-id="05c0b-142">Select hello Azure storage account where logs will be saved and, hello retention period.</span></span> 
>[!TIP]
><span data-ttu-id="05c0b-143">Hello utilizzare stesso account di archiviazione per tutti i hello tooget database controllati meglio hello preconfigurato report modelli.</span><span class="sxs-lookup"><span data-stu-id="05c0b-143">Use hello same storage account for all audited databases tooget hello most out of hello pre-configured reports templates.</span></span>
   
    ![][4]
5. <span data-ttu-id="05c0b-144">Fare clic su hello **OK** configurazione di pulsante toosave hello archiviazione dei dettagli.</span><span class="sxs-lookup"><span data-stu-id="05c0b-144">Click hello **OK** button toosave hello storage details configuration.</span></span>
6. <span data-ttu-id="05c0b-145">In **registrazione dall'evento**, fare clic su **successo** e **errore** toolog tutti gli eventi, oppure scegliere singole categorie di eventi.</span><span class="sxs-lookup"><span data-stu-id="05c0b-145">Under **LOGGING BY EVENT**, click **SUCCESS** and **FAILURE** toolog all events, or choose individual event categories.</span></span>
7. <span data-ttu-id="05c0b-146">Se si configura servizio di controllo per un database, potrebbe essere una stringa di connessione hello tooalter di tooensure il client controllo dei dati viene acquisito in modo corretto.</span><span class="sxs-lookup"><span data-stu-id="05c0b-146">If you are configuring Auditing for a database, you may need tooalter hello connection string of your client tooensure data auditing is correctly captured.</span></span> <span data-ttu-id="05c0b-147">Controllare hello [modificare nome FDQN di Server nella stringa di connessione hello](sql-data-warehouse-auditing-downlevel-clients.md) argomento per le connessioni client di livello inferiore.</span><span class="sxs-lookup"><span data-stu-id="05c0b-147">Check hello [Modify Server FDQN in hello connection string](sql-data-warehouse-auditing-downlevel-clients.md) topic for downlevel client connections.</span></span>
8. <span data-ttu-id="05c0b-148">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="05c0b-148">Click **OK**.</span></span>

## <span data-ttu-id="05c0b-149"><a id="subheading-3"></a>Analizzare i log di controllo e i report</span><span class="sxs-lookup"><span data-stu-id="05c0b-149"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="05c0b-150">I log di controllo vengono aggregati in una raccolta di tabelle di archivio con un **SQLDBAuditLogs** prefisso in hello account di archiviazione di Azure si è scelto durante l'installazione.</span><span class="sxs-lookup"><span data-stu-id="05c0b-150">Audit logs are aggregated in a collection of Store Tables with a **SQLDBAuditLogs** prefix in hello Azure storage account you chose during setup.</span></span> <span data-ttu-id="05c0b-151">È possibile visualizzare i file di log con uno strumento come <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Esplora archivi di Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="05c0b-151">You can view log files using a tool such as <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Storage Explorer</a>.</span></span>

<span data-ttu-id="05c0b-152">Un modello di report preconfigurati dashboard è disponibile come una <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">scaricabile foglio di calcolo Excel</a> toohelp per analizzare rapidamente i dati di log.</span><span class="sxs-lookup"><span data-stu-id="05c0b-152">A preconfigured dashboard report template is available as a <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadable Excel spreadsheet</a> toohelp you quickly analyze log data.</span></span> <span data-ttu-id="05c0b-153">toouse hello modello sul seguente modello i log di controllo, è necessario in Excel 2013 o versioni successive e Power Query, che è possibile scaricare <a href="http://www.microsoft.com/download/details.aspx?id=39379">qui</a>.</span><span class="sxs-lookup"><span data-stu-id="05c0b-153">toouse hello template on your audit logs, you need Excel 2013 or later and Power Query, which you can download <a href="http://www.microsoft.com/download/details.aspx?id=39379">here</a>.</span></span>

<span data-ttu-id="05c0b-154">modello Hello contiene dati di esempio fittizio ed è possibile impostare Power Query tooimport il log di controllo direttamente dall'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="05c0b-154">hello template has fictional sample data in it, and you can set up Power Query tooimport your audit log directly from your Azure storage account.</span></span>

## <span data-ttu-id="05c0b-155"><a id="subheading-4"></a>Rigenerazione delle chiavi di archiviazione</span><span class="sxs-lookup"><span data-stu-id="05c0b-155"><a id="subheading-4"></a>Storage key regeneration</span></span>
<span data-ttu-id="05c0b-156">Nell'ambiente di produzione, si è probabilmente toorefresh lo spazio di archiviazione chiavi periodicamente.</span><span class="sxs-lookup"><span data-stu-id="05c0b-156">In production, you are likely toorefresh your storage keys periodically.</span></span> <span data-ttu-id="05c0b-157">Durante l'aggiornamento delle chiavi, è necessario criteri hello toosave.</span><span class="sxs-lookup"><span data-stu-id="05c0b-157">When refreshing your keys, you need toosave hello policy.</span></span> <span data-ttu-id="05c0b-158">il processo di Hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="05c0b-158">hello process is as follows:</span></span>

1. <span data-ttu-id="05c0b-159">In hello controllo pannello configurazione (descritto in precedenza nel programma di installazione hello controllo sezione) passare hello **chiave di accesso di archiviazione** da *primario* troppo*secondario* e  **SALVARE**.</span><span class="sxs-lookup"><span data-stu-id="05c0b-159">In hello auditing configuration blade (described above in hello setup auditing section) switch hello **Storage Access Key** from *Primary* too*Secondary* and **SAVE**.</span></span>

   ![][4]
2. <span data-ttu-id="05c0b-160">Pannello di configurazione di archiviazione di passare toohello e **rigenerare** hello *chiave di accesso primaria*.</span><span class="sxs-lookup"><span data-stu-id="05c0b-160">Go toohello storage configuration blade and **regenerate** hello *Primary Access Key*.</span></span>
3. <span data-ttu-id="05c0b-161">Tornare indietro toohello controllo pannello configurazione hello commutatore **chiave di accesso di archiviazione** da *secondario* troppo*primario* e premere **salvare**.</span><span class="sxs-lookup"><span data-stu-id="05c0b-161">Go back toohello auditing configuration blade, switch hello **Storage Access Key** from *Secondary* too*Primary* and press **SAVE**.</span></span>
4. <span data-ttu-id="05c0b-162">Tornare indietro archiviazione toohello dell'interfaccia utente e **rigenerare** hello *chiave di accesso secondaria* (per la preparazione di hello chiavi successive ciclo di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="05c0b-162">Go back toohello storage UI and **regenerate** hello *Secondary Access Key* (as preparation for hello next keys refresh cycle.</span></span>

## <span data-ttu-id="05c0b-163"><a id="subheading-5"></a>Automazione (API REST/PowerShell)</span><span class="sxs-lookup"><span data-stu-id="05c0b-163"><a id="subheading-5"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="05c0b-164">È inoltre possibile configurare il controllo in Azure SQL Data Warehouse utilizzando i seguenti strumenti di automazione hello:</span><span class="sxs-lookup"><span data-stu-id="05c0b-164">You can also configure auditing in Azure SQL Data Warehouse by using hello following automation tools:</span></span>

* <span data-ttu-id="05c0b-165">**Cmdlet di PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="05c0b-165">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="05c0b-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="05c0b-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="05c0b-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="05c0b-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="05c0b-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="05c0b-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="05c0b-169">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="05c0b-169">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="05c0b-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="05c0b-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="05c0b-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="05c0b-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="05c0b-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="05c0b-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

<!--Anchors-->
[Nozioni di base sul controllo del database]: #subheading-1
[Configurare il controllo per il database]: #subheading-2
[Analizzare i log di controllo e i report]: #subheading-3


<!--Image references-->
[1]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing.png
[2]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-inherit.png
[3]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-enable.png
[4]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-storage-account.png
[5]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-dashboard.png


<!--Link references-->
[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy