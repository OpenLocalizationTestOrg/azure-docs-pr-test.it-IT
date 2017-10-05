---
title: Servizio di controllo di Azure SQL Data Warehouse | Documentazione Microsoft
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
ms.openlocfilehash: f851c82ebeaa647f663d499a4d327c3479e36121
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a><span data-ttu-id="8ba4e-103">Servizio di controllo di Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="8ba4e-103">Auditing in Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8ba4e-104">Controllo</span><span class="sxs-lookup"><span data-stu-id="8ba4e-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="8ba4e-105">Introduzione al rilevamento delle minacce</span><span class="sxs-lookup"><span data-stu-id="8ba4e-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

<span data-ttu-id="8ba4e-106">La funzionalità di controllo di SQL Data Warehouse consente di registrare gli eventi nel database in un log di controllo nell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-106">SQL Data Warehouse auditing allows you to record events in your database to an audit log in your Azure Storage account.</span></span> <span data-ttu-id="8ba4e-107">Il controllo consente di agevolare la conformità alle normative, comprendere le attività del database e ottenere informazioni su eventuali discrepanze e anomalie che potrebbero indicare problemi aziendali o sospette violazioni della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-107">Auditing can help you maintain regulatory compliance, understand  database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span> <span data-ttu-id="8ba4e-108">La funzionalità di controllo di SQL Data Warehouse si integra inoltre con Microsoft Power BI per l'esecuzione di analisi e report drill-down.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-108">SQL Data Warehouse auditing also integrates with Microsoft Power BI for drill-down reporting and analysis.</span></span>

<span data-ttu-id="8ba4e-109">Gli strumenti di controllo abilitano e facilitano il rispetto degli standard di conformità, ma non garantiscono la conformità.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-109">Auditing tools enable and facilitate adherence to compliance standards but don't guarantee compliance.</span></span> <span data-ttu-id="8ba4e-110">Per altre informazioni sui programmi di Azure che supportano la conformità agli standard, vedere il <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Centro protezione Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-110">For more information about Azure programs that support standards compliance, see the <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span></span>

* <span data-ttu-id="8ba4e-111">[Nozioni di base sul controllo del database]</span><span class="sxs-lookup"><span data-stu-id="8ba4e-111">[Database Auditing basics]</span></span>
* <span data-ttu-id="8ba4e-112">[Configurare il controllo per il database]</span><span class="sxs-lookup"><span data-stu-id="8ba4e-112">[Set up auditing for your database]</span></span>
* <span data-ttu-id="8ba4e-113">[Analizzare i log di controllo e i report]</span><span class="sxs-lookup"><span data-stu-id="8ba4e-113">[Analyze audit logs and reports]</span></span>

## <span data-ttu-id="8ba4e-114"><a id="subheading-1"></a>Nozioni di base sul controllo del database di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="8ba4e-114"><a id="subheading-1"></a>Azure SQL Data Warehouse Database Auditing basics</span></span>
<span data-ttu-id="8ba4e-115">Il controllo del database SQL Data Warehouse consente di:</span><span class="sxs-lookup"><span data-stu-id="8ba4e-115">SQL Data Warehouse database auditing allows you to:</span></span>

* <span data-ttu-id="8ba4e-116">**Conservare** un audit trail di eventi selezionati.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-116">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="8ba4e-117">È possibile definire categorie di azioni di database da controllare.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-117">You can define categories of database actions  to be audited.</span></span>
* <span data-ttu-id="8ba4e-118">**Creare report** sulle attività del database.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-118">**Report** on database activity.</span></span> <span data-ttu-id="8ba4e-119">È possibile usare i report preconfigurati e un dashboard per iniziare rapidamente a usare l’attività e la segnalazione di eventi.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-119">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="8ba4e-120">**Analizzare** i report.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-120">**Analyze** reports.</span></span> <span data-ttu-id="8ba4e-121">È possibile individuare eventi sospetti, attività insolite e tendenze.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-121">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="8ba4e-122">È possibile configurare il controllo per le seguenti categorie di eventi:</span><span class="sxs-lookup"><span data-stu-id="8ba4e-122">You can configure auditing for the following event categories:</span></span>

<span data-ttu-id="8ba4e-123">**SQL normale** e **SQL con parametri** per cui i log di controllo raccolti sono classificati come</span><span class="sxs-lookup"><span data-stu-id="8ba4e-123">**Plain SQL** and **Parameterized SQL** for which the collected audit logs are classified as</span></span>  

* <span data-ttu-id="8ba4e-124">**Accesso ai dati**</span><span class="sxs-lookup"><span data-stu-id="8ba4e-124">**Access to data**</span></span>
* <span data-ttu-id="8ba4e-125">**Modifiche dello schema (DDL)**</span><span class="sxs-lookup"><span data-stu-id="8ba4e-125">**Schema changes (DDL)**</span></span>
* <span data-ttu-id="8ba4e-126">**Modifiche dei dati (DML)**</span><span class="sxs-lookup"><span data-stu-id="8ba4e-126">**Data changes (DML)**</span></span>
* <span data-ttu-id="8ba4e-127">**Account, ruoli e autorizzazioni (DCL)**</span><span class="sxs-lookup"><span data-stu-id="8ba4e-127">**Accounts, roles, and permissions (DCL)**</span></span>
* <span data-ttu-id="8ba4e-128">**Stored procedure**, **accesso** e **gestione delle transazioni**.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-128">**Stored Procedure**, **Login** and, **Transaction Management**.</span></span>

<span data-ttu-id="8ba4e-129">Per ogni categoria di eventi, il controllo delle operazioni **riuscite** e **non riuscite** viene configurato separatamente.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-129">For each Event Category, Auditing of **Success** and **Failure** operations are configured separately.</span></span>

<span data-ttu-id="8ba4e-130">Per altre informazioni sulle attività e sugli eventi controllati, vedere il <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">documento di riferimento sul formato dei log di controllo (download di file DOC)</a>.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-130">For more information about the activities and events audited, see the <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Audit Log Format Reference (doc file download)</a>.</span></span>

<span data-ttu-id="8ba4e-131">I log di controllo vengono archiviati nell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-131">Audit logs are stored in your Azure storage account.</span></span> <span data-ttu-id="8ba4e-132">È possibile definire un periodo di conservazione del log di controllo.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-132">You can define an audit log retention period.</span></span>

<span data-ttu-id="8ba4e-133">Un criterio di controllo può essere definito per un database specifico o come criterio server predefinito.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-133">An auditing policy can be defined for a specific database or as a default server policy.</span></span> <span data-ttu-id="8ba4e-134">I criteri di controllo del server predefiniti si applicano a tutti i database di un server per i quali non sono definiti specifici criteri di controllo del database che hanno la precedenza.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-134">A default server auditing policy applies to all databases on a server, which do not have a specific overriding database auditing policy defined.</span></span>

<span data-ttu-id="8ba4e-135">Prima di impostare il controllo, verificare che si stia usando un [client di livello inferiore](sql-data-warehouse-auditing-downlevel-clients.md).</span><span class="sxs-lookup"><span data-stu-id="8ba4e-135">Before setting up audit auditing check if you are using a ["Downlevel Client."](sql-data-warehouse-auditing-downlevel-clients.md)</span></span>

## <span data-ttu-id="8ba4e-136"><a id="subheading-2"></a>Configurare il controllo per il database</span><span class="sxs-lookup"><span data-stu-id="8ba4e-136"><a id="subheading-2"></a>Set up auditing for your database</span></span>
1. <span data-ttu-id="8ba4e-137">Avviare il <a href="https://portal.azure.com" target="_blank">portale di Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-137">Launch the <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span></span>
2. <span data-ttu-id="8ba4e-138">Passare al pannello **Impostazioni** dell'istanza di SQL Data Warehouse che si vuole controllare.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-138">Go to the **Settings** blade of the SQL Data Warehouse you want to audit.</span></span> <span data-ttu-id="8ba4e-139">Nel pannello **Impostazioni** selezionare **Controllo e rilevamento minacce**.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-139">In the **Settings** blade, select **Auditing & Threat detection**.</span></span>
   
    ![][1]
3. <span data-ttu-id="8ba4e-140">Successivamente, abilitare il controllo facendo clic sul pulsante **ON** .</span><span class="sxs-lookup"><span data-stu-id="8ba4e-140">Next, enable auditing by clicking the **ON** button.</span></span>
   
    ![][3]
4. <span data-ttu-id="8ba4e-141">Nel pannello di configurazione del controllo selezionare **DETTAGLI ARCHIVIAZIONE** per aprire il pannello Archiviazione dei log di controllo.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-141">In the auditing configuration blade, select **STORAGE DETAILS** to open the Audit Logs Storage blade.</span></span> <span data-ttu-id="8ba4e-142">Selezionare l'account di archiviazione di Azure in cui verranno salvati i log e il periodo di conservazione.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-142">Select the Azure storage account where logs will be saved and, the retention period.</span></span> 
>[!TIP]
><span data-ttu-id="8ba4e-143">Per sfruttare al massimo i modelli di report preconfigurati, usare lo stesso account di archiviazione per tutti i database controllati.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-143">Use the same storage account for all audited databases to get the most out of the pre-configured reports templates.</span></span>
   
    ![][4]
5. <span data-ttu-id="8ba4e-144">Fare clic sul pulsante **OK** per salvare la configurazione dei dettagli di archiviazione .</span><span class="sxs-lookup"><span data-stu-id="8ba4e-144">Click the **OK** button to save the storage details configuration.</span></span>
6. <span data-ttu-id="8ba4e-145">In **REGISTRAZIONE PER EVENTO** fare clic su **OPERAZIONE RIUSCITA** e **OPERAZIONE NON RIUSCITA** per registrare tutti gli eventi oppure scegliere singole categorie di eventi.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-145">Under **LOGGING BY EVENT**, click **SUCCESS** and **FAILURE** to log all events, or choose individual event categories.</span></span>
7. <span data-ttu-id="8ba4e-146">Se si sta configurando il controllo per un database, è necessario modificare la stringa di connessione del client per garantire che il controllo dei dati venga acquisito correttamente.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-146">If you are configuring Auditing for a database, you may need to alter the connection string of your client to ensure data auditing is correctly captured.</span></span> <span data-ttu-id="8ba4e-147">Controllare l’argomento [Modificare il nome di dominio di Server completo nella stringa di connessione](sql-data-warehouse-auditing-downlevel-clients.md) per le connessioni di client di livello inferiore.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-147">Check the [Modify Server FDQN in the connection string](sql-data-warehouse-auditing-downlevel-clients.md) topic for downlevel client connections.</span></span>
8. <span data-ttu-id="8ba4e-148">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-148">Click **OK**.</span></span>

## <span data-ttu-id="8ba4e-149"><a id="subheading-3"></a>Analizzare i log di controllo e i report</span><span class="sxs-lookup"><span data-stu-id="8ba4e-149"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="8ba4e-150">I log di controllo vengono aggregati in una raccolta di tabelle di archiviazione con il prefisso **SQLDBAuditLogs** nell'account di archiviazione di Azure scelto durante l'installazione.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-150">Audit logs are aggregated in a collection of Store Tables with a **SQLDBAuditLogs** prefix in the Azure storage account you chose during setup.</span></span> <span data-ttu-id="8ba4e-151">È possibile visualizzare i file di log con uno strumento come <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Esplora archivi di Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-151">You can view log files using a tool such as <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Storage Explorer</a>.</span></span>

<span data-ttu-id="8ba4e-152">È possibile scaricare un modello di report dashboard preconfigurato in formato <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">foglio di calcolo di Excel</a>, che consente di analizzare rapidamente i dati di log.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-152">A preconfigured dashboard report template is available as a <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadable Excel spreadsheet</a> to help you quickly analyze log data.</span></span> <span data-ttu-id="8ba4e-153">Per usare il modello nei log di controllo sono necessari Excel 2013 o versione successiva e Power Query, disponibile per il download <a href="http://www.microsoft.com/download/details.aspx?id=39379">qui</a>.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-153">To use the template on your audit logs, you need Excel 2013 or later and Power Query, which you can download <a href="http://www.microsoft.com/download/details.aspx?id=39379">here</a>.</span></span>

<span data-ttu-id="8ba4e-154">Il modello contiene dati di esempio fittizi ed è possibile configurare Power Query per l'importazione diretta del log di controllo dall'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-154">The template has fictional sample data in it, and you can set up Power Query to import your audit log directly from your Azure storage account.</span></span>

## <span data-ttu-id="8ba4e-155"><a id="subheading-4"></a>Rigenerazione delle chiavi di archiviazione</span><span class="sxs-lookup"><span data-stu-id="8ba4e-155"><a id="subheading-4"></a>Storage key regeneration</span></span>
<span data-ttu-id="8ba4e-156">Durante la produzione è probabile che periodicamente vengano aggiornate le chiavi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-156">In production, you are likely to refresh your storage keys periodically.</span></span> <span data-ttu-id="8ba4e-157">Quando si aggiornano le chiavi, è necessario salvare i criteri.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-157">When refreshing your keys, you need to save the policy.</span></span> <span data-ttu-id="8ba4e-158">Il processo è il seguente:</span><span class="sxs-lookup"><span data-stu-id="8ba4e-158">The process is as follows:</span></span>

1. <span data-ttu-id="8ba4e-159">Nel pannello di configurazione del controllo (descritto in precedenza nella sezione sulla configurazione del controllo) cambiare **Chiave di accesso alle risorse di archiviazione** da *Primaria* a *Secondaria* e fare clic su **SALVA**.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-159">In the auditing configuration blade (described above in the setup auditing section) switch the **Storage Access Key** from *Primary* to *Secondary* and **SAVE**.</span></span>

   ![][4]
2. <span data-ttu-id="8ba4e-160">Passare al pannello di configurazione di archiviazione e **rigenerare** la *Chiave di accesso primaria*.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-160">Go to the storage configuration blade and **regenerate** the *Primary Access Key*.</span></span>
3. <span data-ttu-id="8ba4e-161">Tornare al pannello di configurazione del controllo, cambiare **Chiave di accesso alle risorse di archiviazione** da *Secondaria* a *Primaria* e fare clic su **SALVA**.</span><span class="sxs-lookup"><span data-stu-id="8ba4e-161">Go back to the auditing configuration blade, switch the **Storage Access Key** from *Secondary* to *Primary* and press **SAVE**.</span></span>
4. <span data-ttu-id="8ba4e-162">Tornare all'interfaccia utente di archiviazione e **rigenerare** la *Chiave di accesso secondaria* (in preparazione al successivo ciclo di aggiornamento delle chiavi).</span><span class="sxs-lookup"><span data-stu-id="8ba4e-162">Go back to the storage UI and **regenerate** the *Secondary Access Key* (as preparation for the next keys refresh cycle.</span></span>

## <span data-ttu-id="8ba4e-163"><a id="subheading-5"></a>Automazione (API REST/PowerShell)</span><span class="sxs-lookup"><span data-stu-id="8ba4e-163"><a id="subheading-5"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="8ba4e-164">È possibile configurare il controllo in Azure SQL Data Warehouse anche con gli strumenti di automazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="8ba4e-164">You can also configure auditing in Azure SQL Data Warehouse by using the following automation tools:</span></span>

* <span data-ttu-id="8ba4e-165">**Cmdlet di PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="8ba4e-165">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="8ba4e-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="8ba4e-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="8ba4e-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="8ba4e-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="8ba4e-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="8ba4e-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="8ba4e-169">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="8ba4e-169">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="8ba4e-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="8ba4e-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="8ba4e-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="8ba4e-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="8ba4e-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="8ba4e-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

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