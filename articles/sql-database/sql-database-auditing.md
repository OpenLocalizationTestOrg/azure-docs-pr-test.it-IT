---
title: Introduzione al controllo del database SQL di Azure | Microsoft Docs
description: Introduzione al servizio di controllo del database SQL di Azure
services: sql-database
documentationcenter: 
author: giladm
manager: jhubbard
editor: giladm
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: giladm
ms.openlocfilehash: f4324a59b5fa4c2e1ab5b1d7fc7e5fe986ea80f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-sql-database-auditing"></a><span data-ttu-id="06249-103">Introduzione al controllo del database SQL</span><span class="sxs-lookup"><span data-stu-id="06249-103">Get started with SQL database auditing</span></span>
<span data-ttu-id="06249-104">Il servizio di controllo del database SQL di Azure tiene traccia degli eventi di database e li registra in un log di controllo nell'account di archiviazione di Azure dell'utente.</span><span class="sxs-lookup"><span data-stu-id="06249-104">Azure SQL database auditing tracks database events and writes them to an audit log in your Azure storage account.</span></span> <span data-ttu-id="06249-105">Inoltre, il servizio di controllo:</span><span class="sxs-lookup"><span data-stu-id="06249-105">Auditing also:</span></span>

* <span data-ttu-id="06249-106">Consente di gestire la conformità alle normative, ottenere informazioni sull'attività del database e rilevare discrepanze e anomalie che potrebbero indicare problemi aziendali o possibili violazioni della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="06249-106">Helps you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

* <span data-ttu-id="06249-107">Supporta e facilita il rispetto degli standard di conformità, pur non garantendo la conformità.</span><span class="sxs-lookup"><span data-stu-id="06249-107">Enables and facilitates adherence to compliance standards, although it doesn't guarantee compliance.</span></span> <span data-ttu-id="06249-108">Per altre informazioni sui programmi di Azure che supportano la conformità agli standard, vedere il [Centro protezione Azure](https://azure.microsoft.com/support/trust-center/compliance/).</span><span class="sxs-lookup"><span data-stu-id="06249-108">For more information about Azure programs that support standards compliance, see the [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span></span>


## <span data-ttu-id="06249-109"><a id="subheading-1"></a>Panoramica del servizio di controllo del database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="06249-109"><a id="subheading-1"></a>Azure SQL database auditing overview</span></span>
<span data-ttu-id="06249-110">È possibile usare il servizio di controllo del database SQL per eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="06249-110">You can use SQL database auditing to:</span></span>


* <span data-ttu-id="06249-111">**Conservare** un audit trail di eventi selezionati.</span><span class="sxs-lookup"><span data-stu-id="06249-111">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="06249-112">È possibile definire categorie di azioni di database da controllare.</span><span class="sxs-lookup"><span data-stu-id="06249-112">You can define categories of database actions to be audited.</span></span>
* <span data-ttu-id="06249-113">**Creare report** sulle attività del database.</span><span class="sxs-lookup"><span data-stu-id="06249-113">**Report** on database activity.</span></span> <span data-ttu-id="06249-114">È possibile usare i report preconfigurati e un dashboard per iniziare rapidamente a usare l’attività e la segnalazione di eventi.</span><span class="sxs-lookup"><span data-stu-id="06249-114">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="06249-115">**Analizzare** i report.</span><span class="sxs-lookup"><span data-stu-id="06249-115">**Analyze** reports.</span></span> <span data-ttu-id="06249-116">È possibile individuare eventi sospetti, attività insolite e tendenze.</span><span class="sxs-lookup"><span data-stu-id="06249-116">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="06249-117">È possibile configurare il controllo per diversi tipi di categorie di eventi, come spiegato nella sezione [Configurare il controllo per il database](#subheading-2).</span><span class="sxs-lookup"><span data-stu-id="06249-117">You can configure auditing for different types of event categories, as explained in the [Set up auditing for your database](#subheading-2) section.</span></span>

<span data-ttu-id="06249-118">I log di controllo vengono scritti nell'archivio BLOB di Azure della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="06249-118">Audit logs are written to Azure Blob storage on your Azure subscription.</span></span>


## <span data-ttu-id="06249-119"><a id="subheading-8"></a>Definire criteri di controllo a livello di server o a livello di database</span><span class="sxs-lookup"><span data-stu-id="06249-119"><a id="subheading-8"></a>Define server-level vs. database-level auditing policy</span></span>

<span data-ttu-id="06249-120">I criteri di controllo possono essere definiti per un database specifico o come criteri server predefiniti:</span><span class="sxs-lookup"><span data-stu-id="06249-120">An auditing policy can be defined for a specific database or as a default server policy:</span></span>

* <span data-ttu-id="06249-121">I criteri server si applicano a tutti i database nuovi ed esistenti in un server.</span><span class="sxs-lookup"><span data-stu-id="06249-121">A server policy applies to all existing and newly created databases on the server.</span></span>

* <span data-ttu-id="06249-122">Se abilitato, il *controllo BLOB del server* *si applica sempre al database*. Il controllo verrà quindi eseguito sul database indipendentemente dalle impostazioni di controllo del database.</span><span class="sxs-lookup"><span data-stu-id="06249-122">If *server blob auditing is enabled*, it *always applies to the database* (that is, the database will be audited), regardless of the database auditing settings.</span></span>

* <span data-ttu-id="06249-123">L'abilitazione del controllo BLOB nel database in aggiunta all'abilitazione nel server *non* sostituisce o modifica le impostazioni del controllo BLOB del server.</span><span class="sxs-lookup"><span data-stu-id="06249-123">Enabling blob auditing on the database, in addition to enabling it on the server, will *not* override or change any of the settings of the server blob auditing.</span></span> <span data-ttu-id="06249-124">I due controlli coesisteranno.</span><span class="sxs-lookup"><span data-stu-id="06249-124">Both audits will exist side by side.</span></span> <span data-ttu-id="06249-125">In altre parole, il database verrà controllato due volte in parallelo, una volta con i criteri del server e una volta con i criteri del database.</span><span class="sxs-lookup"><span data-stu-id="06249-125">In other words, the database will be audited twice in parallel (once by the server policy and once by the database policy).</span></span>

   > [!NOTE]
   > <span data-ttu-id="06249-126">È consigliabile evitare di abilitare contemporaneamente il controllo BLOB del server e il controllo BLOB del database ad eccezione dei casi seguenti:</span><span class="sxs-lookup"><span data-stu-id="06249-126">You should avoid enabling both server blob auditing and database blob auditing together, unless:</span></span>
    > * <span data-ttu-id="06249-127">Si vuole usare un *account di archiviazione* o un *periodo di conservazione* diverso per un database specifico.</span><span class="sxs-lookup"><span data-stu-id="06249-127">You want to use a different *storage account* or *retention period* for a specific database.</span></span>
    > * <span data-ttu-id="06249-128">Per un database specifico si vogliono controllare tipi o categorie di eventi diversi da quelli controllati per gli altri database nel server.</span><span class="sxs-lookup"><span data-stu-id="06249-128">You want to audit event types or categories for a specific database that differ from event types or categories that are being audited for the rest of the databases on the server.</span></span> <span data-ttu-id="06249-129">Ad esempio, potrebbe essere necessario controllare gli inserimenti di tabella solo per un database specifico.</span><span class="sxs-lookup"><span data-stu-id="06249-129">For example, you might have table inserts that need to be audited only for a specific database.</span></span>
   > 
   > <span data-ttu-id="06249-130">Negli altri casi, è consigliabile abilitare solo il controllo BLOB a livello di server e lasciare disabilitato il controllo a livello di database per tutti i database.</span><span class="sxs-lookup"><span data-stu-id="06249-130">Otherwise, we recommended that you enable only server-level blob auditing and leave the database-level auditing disabled for all databases.</span></span>


## <span data-ttu-id="06249-131"><a id="subheading-2"></a>Configurare il controllo per il database</span><span class="sxs-lookup"><span data-stu-id="06249-131"><a id="subheading-2"></a>Set up auditing for your database</span></span>
<span data-ttu-id="06249-132">Nella sezione seguente è descritta la configurazione del controllo mediante il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="06249-132">The following section describes the configuration of auditing using the Azure portal.</span></span>

1. <span data-ttu-id="06249-133">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="06249-133">Go to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="06249-134">Passare al pannello **Impostazioni** del database o del server SQL che si vuole controllare.</span><span class="sxs-lookup"><span data-stu-id="06249-134">Go to the **Settings** blade of the SQL database/SQL server you want to audit.</span></span> <span data-ttu-id="06249-135">Nel pannello **Impostazioni** selezionare **Controllo e rilevamento minacce**.</span><span class="sxs-lookup"><span data-stu-id="06249-135">In the **Settings** blade, select **Auditing & Threat detection**.</span></span>

    <span data-ttu-id="06249-136"><a id="auditing-screenshot"></a> ![Riquadro di spostamento][1]</span><span class="sxs-lookup"><span data-stu-id="06249-136"><a id="auditing-screenshot"></a> ![Navigation pane][1]</span></span>
3. <span data-ttu-id="06249-137">Se si preferisce configurare criteri di controllo del server, che verranno applicati a tutti i database nuovi ed esistenti nel server, è possibile selezionare il collegamento **Visualizza impostazioni del server** nel pannello relativo al controllo del database.</span><span class="sxs-lookup"><span data-stu-id="06249-137">If you prefer to set up a server auditing policy (which will apply to all existing and newly created databases on this server), you can select the **View server settings** link in the database auditing blade.</span></span> <span data-ttu-id="06249-138">Si possono quindi visualizzare o modificare le impostazioni di controllo del server.</span><span class="sxs-lookup"><span data-stu-id="06249-138">You can then view or modify the server auditing settings.</span></span>

    ![Riquadro di spostamento][2]
4. <span data-ttu-id="06249-140">Se si preferisce abilitare il controllo BLOB a livello di database, in aggiunta o in sostituzione del controllo a livello di server, selezionare **SÌ** per **Controllo** e **BLOB** per **Tipo di controllo**.</span><span class="sxs-lookup"><span data-stu-id="06249-140">If you prefer to enable blob auditing on the database level (in addition to or instead of server-level auditing), for **Auditing**, select **ON**, and for **Auditing type**, select  **Blob**.</span></span>

    <span data-ttu-id="06249-141">Se il controllo BLOB del server è abilitato, il controllo configurato del database coesisterà con il controllo BLOB del server.</span><span class="sxs-lookup"><span data-stu-id="06249-141">If server blob auditing is enabled, the database-configured audit will exist side by side with the server blob audit.</span></span>  

    ![Riquadro di spostamento][3]
5. <span data-ttu-id="06249-143">Per aprire il pannello **Archiviazione dei log di controllo** selezionare **Dettagli archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="06249-143">To open the **Audit Logs Storage** blade, select **Storage Details**.</span></span> <span data-ttu-id="06249-144">Selezionare l'account di archiviazione di Azure in cui verranno salvati i log e quindi il periodo di conservazione al termine del quale verranno eliminati i log meno recenti.</span><span class="sxs-lookup"><span data-stu-id="06249-144">Select the Azure storage account where logs will be saved, and then select the retention period, after which the old logs will be deleted.</span></span> <span data-ttu-id="06249-145">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="06249-145">Then click **OK**.</span></span> 
   >[!TIP] 
   ><span data-ttu-id="06249-146">Per sfruttare al massimo i modelli di report di controllo, usare lo stesso account di archiviazione per tutti i database controllati.</span><span class="sxs-lookup"><span data-stu-id="06249-146">To get the most out of the auditing reports templates, use the same storage account for all audited databases.</span></span> 

    <span data-ttu-id="06249-147"><a id="storage-screenshot"></a> ![Riquadro di spostamento][4]</span><span class="sxs-lookup"><span data-stu-id="06249-147"><a id="storage-screenshot"></a> ![Navigation pane][4]</span></span>
6. <span data-ttu-id="06249-148">Per personalizzare gli eventi controllati, è possibile usare PowerShell o l'API REST.</span><span class="sxs-lookup"><span data-stu-id="06249-148">If you want to customize the audited events, you can do this via PowerShell or the REST API.</span></span> <span data-ttu-id="06249-149">Per altre informazioni, vedere la sezione [Automazione (API REST/PowerShell)](#subheading-7).</span><span class="sxs-lookup"><span data-stu-id="06249-149">For more details, see the [Automation (PowerShell/REST API)](#subheading-7) section.</span></span>
7. <span data-ttu-id="06249-150">Dopo aver configurato le impostazioni di controllo, è possibile attivare la nuova funzionalità di rilevamento delle minacce e configurare gli indirizzi di posta elettronica per ricevere gli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="06249-150">After you've configured your auditing settings, you can turn on the new threat detection feature and configure emails to receive security alerts.</span></span> <span data-ttu-id="06249-151">Quando si usa il rilevamento delle minacce, si ricevono avvisi proattivi sulle attività di database anomale che possono indicare potenziali minacce per la sicurezza.</span><span class="sxs-lookup"><span data-stu-id="06249-151">When you use threat detection, you receive proactive alerts on anomalous database activities that can indicate potential security threats.</span></span> <span data-ttu-id="06249-152">Per altri dettagli, vedere l'[introduzione al rilevamento delle minacce](sql-database-threat-detection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="06249-152">For more details, see [Getting started with threat detection](sql-database-threat-detection-get-started.md).</span></span>
8. <span data-ttu-id="06249-153">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="06249-153">Click **Save**.</span></span>





## <span data-ttu-id="06249-154"><a id="subheading-3"></a>Analizzare i log di controllo e i report</span><span class="sxs-lookup"><span data-stu-id="06249-154"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="06249-155">I log di controllo vengono aggregati nell'account di archiviazione di Azure selezionato durante la configurazione.</span><span class="sxs-lookup"><span data-stu-id="06249-155">Audit logs are aggregated in the Azure storage account you chose during setup.</span></span> <span data-ttu-id="06249-156">È possibile esplorare i log di controllo con uno strumento come [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="06249-156">You can explore audit logs by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="06249-157">I log del controllo BLOB vengono salvati come raccolta di file BLOB in un contenitore denominato **sqldbauditlogs**.</span><span class="sxs-lookup"><span data-stu-id="06249-157">Blob auditing logs are saved as a collection of blob files within a container named **sqldbauditlogs**.</span></span>

<span data-ttu-id="06249-158">Per altri dettagli sulla gerarchia della cartella di archiviazione dei log del controllo BLOB, le convenzioni di denominazione dei BLOB e il formato dei log, vedere le [informazioni di riferimento sul formato dei log del controllo BLOB (download di file con estensione docx)](https://go.microsoft.com/fwlink/?linkid=829599).</span><span class="sxs-lookup"><span data-stu-id="06249-158">For further details about the hierarchy of the blob audit logs storage folder, blob naming conventions, and log format, see the [Blob Audit Log Format Reference (.docx file download)](https://go.microsoft.com/fwlink/?linkid=829599).</span></span>

<span data-ttu-id="06249-159">Per visualizzare i log del controllo BLOB sono disponibili diversi metodi:</span><span class="sxs-lookup"><span data-stu-id="06249-159">There are several methods you can use to view blob auditing logs:</span></span>

* <span data-ttu-id="06249-160">Usare il [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="06249-160">Use the [Azure portal](https://portal.azure.com).</span></span>  <span data-ttu-id="06249-161">Aprire il database corrispondente.</span><span class="sxs-lookup"><span data-stu-id="06249-161">Open the relevant database.</span></span> <span data-ttu-id="06249-162">Nella parte superiore del pannello **Controllo e rilevamento minacce** del database fare clic su **Visualizza log di controllo**.</span><span class="sxs-lookup"><span data-stu-id="06249-162">At the top of the database's **Auditing & Threat detection** blade, click **View audit logs**.</span></span>

    ![Riquadro di spostamento][7]

    <span data-ttu-id="06249-164">Verrà aperto il pannello **Record di controllo**, da cui sarà possibile visualizzare i log.</span><span class="sxs-lookup"><span data-stu-id="06249-164">An **Audit records** blade opens, from which you'll be able to view the logs.</span></span>

    - <span data-ttu-id="06249-165">È possibile visualizzare date specifiche facendo clic su **Filtro** nella parte superiore del pannello **Record di controllo**.</span><span class="sxs-lookup"><span data-stu-id="06249-165">You can view specific dates by clicking **Filter** at the top of the **Audit records** blade.</span></span>
    - <span data-ttu-id="06249-166">È possibile passare dai record di controllo creati dai criteri del server a quelli creati dai criteri del database e viceversa.</span><span class="sxs-lookup"><span data-stu-id="06249-166">You can switch between audit records that were created by a server policy or database policy audit.</span></span>

       ![Riquadro di spostamento][8]

* <span data-ttu-id="06249-168">Usare la funzione di sistema **sys.fn_get_audit_file** (T-SQL) per tornare ai dati dei log di controllo in formato tabulare.</span><span class="sxs-lookup"><span data-stu-id="06249-168">Use the system function **sys.fn_get_audit_file** (T-SQL) to return the audit log data in tabular format.</span></span> <span data-ttu-id="06249-169">Per altre informazioni su questa funzione, vedere la [documentazione su sys.fn_get_audit_file](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="06249-169">For more information on using this function, see the [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span></span>


* <span data-ttu-id="06249-170">Usare **Unisci file di controllo** in SQL Server Management Studio (a partire da SSMS 17):</span><span class="sxs-lookup"><span data-stu-id="06249-170">Use **Merge Audit Files** in SQL Server Management Studio (starting with SSMS 17):</span></span>  
    1. <span data-ttu-id="06249-171">Dalla barra dei menu di SSMS selezionare **File** > **Apri** > **Unisci file di controllo**.</span><span class="sxs-lookup"><span data-stu-id="06249-171">From the SSMS menu, select **File** > **Open** > **Merge Audit Files**.</span></span>

        ![Riquadro di spostamento][9]
    2. <span data-ttu-id="06249-173">Verrà visualizzata la finestra di dialogo **Aggiunti file di controllo**.</span><span class="sxs-lookup"><span data-stu-id="06249-173">The **Add Audit Files** dialog box opens.</span></span> <span data-ttu-id="06249-174">Selezionare una delle opzioni **Aggiungi** per scegliere se unire i file di controllo da un disco locale oppure importarli da Archiviazione di Azure (sarà necessario specificare i dettagli e la chiave dell'account di archiviazione di Azure).</span><span class="sxs-lookup"><span data-stu-id="06249-174">Select one of the **Add** options to choose whether to merge audit files from a local disk or import them from Azure Storage (you will be required to provide your Azure Storage details and account key).</span></span>

    3. <span data-ttu-id="06249-175">Dopo aver aggiunto tutti i file da unire, fare clic su **OK** per completare l'operazione di unione.</span><span class="sxs-lookup"><span data-stu-id="06249-175">After all files to merge have been added, click **OK** to complete the merge operation.</span></span>

    4. <span data-ttu-id="06249-176">Il file unito verrà aperto in SSMS, dove potrà essere visualizzato, analizzato ed esportato in un file XEL o CSV o in una tabella.</span><span class="sxs-lookup"><span data-stu-id="06249-176">The merged file opens in SSMS, where you can view and analyze it, as well as export it to an XEL or CSV file or to a table.</span></span>

* <span data-ttu-id="06249-177">Usare l'[applicazione di sincronizzazione](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) che è stata creata.</span><span class="sxs-lookup"><span data-stu-id="06249-177">Use the [sync application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) that we have created.</span></span> <span data-ttu-id="06249-178">L'applicazione viene eseguita in Azure e utilizza le API pubbliche di Operations Management Suite (OMS) Log Analytics per effettuare il push dei log di controllo SQL in OMS,</span><span class="sxs-lookup"><span data-stu-id="06249-178">It runs in Azure and utilizes Operations Management Suite (OMS) Log Analytics public APIs to push SQL audit logs into OMS.</span></span> <span data-ttu-id="06249-179">per l'utilizzo tramite il dashboard di OMS Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="06249-179">The sync application pushes SQL audit logs into OMS Log Analytics for consumption via the OMS Log Analytics dashboard.</span></span> 

* <span data-ttu-id="06249-180">Usare Power BI.</span><span class="sxs-lookup"><span data-stu-id="06249-180">Use Power BI.</span></span> <span data-ttu-id="06249-181">È possibile visualizzare e analizzare i dati dei log di controllo in Power BI.</span><span class="sxs-lookup"><span data-stu-id="06249-181">You can view and analyze audit log data in Power BI.</span></span> <span data-ttu-id="06249-182">Per altre informazioni, vedere il post di blog su [Power BI e l'accesso a un modello scaricabile](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span><span class="sxs-lookup"><span data-stu-id="06249-182">Learn more about [Power BI, and access a downloadable template](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span></span>

* <span data-ttu-id="06249-183">Scaricare i file di log dal contenitore BLOB del servizio di archiviazione di Azure tramite il portale o con uno strumento come [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="06249-183">Download log files from your Azure Storage blob container via the portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
    * <span data-ttu-id="06249-184">Dopo aver scaricato un file di log in locale, è possibile fare doppio clic sul file per aprire, visualizzare e analizzare i log in SSMS.</span><span class="sxs-lookup"><span data-stu-id="06249-184">After you have downloaded a log file locally, you can double-click the file to open, view, and analyze the logs in SSMS.</span></span>
    * <span data-ttu-id="06249-185">È anche possibile scaricare più file contemporaneamente tramite Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="06249-185">You can also download multiple files simultaneously via Azure Storage Explorer.</span></span> <span data-ttu-id="06249-186">Fare clic con il pulsante destro del mouse su una sottocartella specifica, ad esempio una sottocartella contenente tutti i file di log per una determinata data, e scegliere **Salva con nome** per salvarla in una cartella locale.</span><span class="sxs-lookup"><span data-stu-id="06249-186">Right-click a specific subfolder (for example, a subfolder that includes all log files for a specific date) and select **Save as** to save in a local folder.</span></span>

* <span data-ttu-id="06249-187">Altri metodi:</span><span class="sxs-lookup"><span data-stu-id="06249-187">Additional methods:</span></span>
   * <span data-ttu-id="06249-188">Dopo aver scaricato diversi file (o una sottocartella contenente i file di log per un intero giorno, come descritto nella voce precedente di questo elenco), è possibile unirli in locale come descritto nelle istruzioni relative all'unione di file di controllo in SSMS riportate sopra.</span><span class="sxs-lookup"><span data-stu-id="06249-188">After downloading several files (or a subfolder that includes log files for an entire day, as described in the previous item in this list), you can merge them locally as described in the SSMS Merge Audit Files instructions described earlier.</span></span>

   * <span data-ttu-id="06249-189">Visualizzare i log del controllo BLOB a livello di codice:</span><span class="sxs-lookup"><span data-stu-id="06249-189">View blob auditing logs programmatically:</span></span>

     * <span data-ttu-id="06249-190">Usare la libreria C# del [lettore di eventi estesi](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/).</span><span class="sxs-lookup"><span data-stu-id="06249-190">Use the [Extended Events Reader](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# library.</span></span>
     * <span data-ttu-id="06249-191">[Eseguire query sui file di eventi estesi](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06249-191">[Query Extended Events Files](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) by using PowerShell.</span></span>




## <span data-ttu-id="06249-192"><a id="subheading-5"></a>Procedure nell'ambiente di produzione</span><span class="sxs-lookup"><span data-stu-id="06249-192"><a id="subheading-5"></a>Production practices</span></span>
<!--The description in this section refers to preceding screen captures.-->

### <span data-ttu-id="06249-193"><a id="subheading-6">Controllo dei database con replica geografica</a></span><span class="sxs-lookup"><span data-stu-id="06249-193"><a id="subheading-6">Auditing geo-replicated databases</a></span></span>
<span data-ttu-id="06249-194">Se si usano database con replica geografica, è possibile configurare il controllo nel database primario, nel database secondario o in entrambi, a seconda del tipo di controllo.</span><span class="sxs-lookup"><span data-stu-id="06249-194">When you use geo-replicated databases, it is possible to set up auditing on either the primary database, the secondary database, or both, depending on the audit type.</span></span>

<span data-ttu-id="06249-195">Seguire le istruzioni di seguito, tenendo presente che il controllo BLOB può essere attivato o disattivato solo dalle impostazioni di controllo del database primario:</span><span class="sxs-lookup"><span data-stu-id="06249-195">Follow these instructions (remember that blob auditing can be turned on or off only from the primary database auditing settings):</span></span>

* <span data-ttu-id="06249-196">**Database primario**.</span><span class="sxs-lookup"><span data-stu-id="06249-196">**Primary database**.</span></span> <span data-ttu-id="06249-197">Attivare il controllo BLOB nel server o nel database stesso, come descritto nella sezione [Configurare il controllo per il database](#subheading-2).</span><span class="sxs-lookup"><span data-stu-id="06249-197">Turn on blob auditing, either on the server or on the database itself, as described in the [Set up auditing for your database](#subheading-2) section.</span></span>
* <span data-ttu-id="06249-198">**Database secondario**.</span><span class="sxs-lookup"><span data-stu-id="06249-198">**Secondary database**.</span></span> <span data-ttu-id="06249-199">Attivare il controllo BLOB nel database primario, come descritto nella sezione [Configurare il controllo per il database](#subheading-2).</span><span class="sxs-lookup"><span data-stu-id="06249-199">Turn on blob auditing on the primary database, as described in the [Set up auditing for your database](#subheading-2) section.</span></span> 
   * <span data-ttu-id="06249-200">Il controllo BLOB deve essere abilitato nello *stesso database primario* e non nel server.</span><span class="sxs-lookup"><span data-stu-id="06249-200">Blob auditing must be enabled on the *primary database itself*, not the server.</span></span>
   * <span data-ttu-id="06249-201">Dopo che il controllo BLOB è stato abilitato nel database primario, verrà abilitato anche nel database secondario.</span><span class="sxs-lookup"><span data-stu-id="06249-201">After blob auditing is enabled on the primary database, it will also become enabled on the secondary database.</span></span>

     >[!IMPORTANT]
     ><span data-ttu-id="06249-202">Per impostazione predefinita, le impostazioni di archiviazione per il database secondario sono identiche a quelle del database primario, e causano traffico tra le aree.</span><span class="sxs-lookup"><span data-stu-id="06249-202">By default, the storage settings for the secondary database will be identical to those of the primary database, causing cross-regional traffic.</span></span> <span data-ttu-id="06249-203">È possibile evitare questo problema abilitando il controllo BLOB nel server secondario e configurando una risorsa di archiviazione locale nelle impostazioni di archiviazione del server secondario.</span><span class="sxs-lookup"><span data-stu-id="06249-203">You can avoid this by enabling blob auditing on the secondary server and configuring local storage in the secondary server storage settings.</span></span> <span data-ttu-id="06249-204">In questo modo verrà ignorato il percorso di archiviazione per il database secondario e di conseguenza ogni database salverà i propri log di controllo in una risorsa di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="06249-204">This will override the storage location for the secondary database and result in each database saving its audit logs to local storage.</span></span>  
<br>

### <span data-ttu-id="06249-205"><a id="subheading-6">Rigenerazione delle chiavi di archiviazione</a></span><span class="sxs-lookup"><span data-stu-id="06249-205"><a id="subheading-6">Storage key regeneration</a></span></span>
<span data-ttu-id="06249-206">Durante la produzione è probabile che periodicamente vengano aggiornate le chiavi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="06249-206">In production, you are likely to refresh your storage keys periodically.</span></span> <span data-ttu-id="06249-207">Quando si aggiornano le chiavi, è necessario salvare nuovamente i criteri di controllo.</span><span class="sxs-lookup"><span data-stu-id="06249-207">When refreshing your keys, you need to resave the auditing policy.</span></span> <span data-ttu-id="06249-208">Il processo è il seguente:</span><span class="sxs-lookup"><span data-stu-id="06249-208">The process is as follows:</span></span>

1. <span data-ttu-id="06249-209">Aprire il pannello **Dettagli archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="06249-209">Open the **Storage Details** blade.</span></span> <span data-ttu-id="06249-210">Nella casella **Chiave di accesso alle risorse di archiviazione** selezionare **Secondaria** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="06249-210">In the **Storage Access Key** box, select **Secondary**, and click **OK**.</span></span> <span data-ttu-id="06249-211">Fare quindi clic su **Salva** nella parte superiore del pannello di configurazione del controllo.</span><span class="sxs-lookup"><span data-stu-id="06249-211">Then click **Save** at the top of the auditing configuration blade.</span></span>

    ![Riquadro di spostamento][5]
2. <span data-ttu-id="06249-213">Passare al pannello di configurazione dell'archiviazione e rigenerare la chiave di accesso primaria.</span><span class="sxs-lookup"><span data-stu-id="06249-213">Go to the storage configuration blade and regenerate the primary access key.</span></span>

    ![Riquadro di spostamento][6]
3. <span data-ttu-id="06249-215">Tornare al pannello di configurazione del controllo, modificare la chiave di accesso alle risorse di archiviazione da secondaria a primaria e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="06249-215">Go back to the auditing configuration blade, switch the storage access key from secondary to primary, and then click **OK**.</span></span> <span data-ttu-id="06249-216">Fare quindi clic su **Salva** nella parte superiore del pannello di configurazione del controllo.</span><span class="sxs-lookup"><span data-stu-id="06249-216">Then click **Save** at the top of the auditing configuration blade.</span></span>
4. <span data-ttu-id="06249-217">Tornare al pannello di configurazione dell'archiviazione e rigenerare la chiave di accesso secondaria, in preparazione al successivo ciclo di aggiornamento della chiave.</span><span class="sxs-lookup"><span data-stu-id="06249-217">Go back to the storage configuration blade and regenerate the secondary access key (in preparation for the next key's refresh cycle).</span></span>

## <span data-ttu-id="06249-218"><a id="subheading-7"></a>Automazione (API REST/PowerShell)</span><span class="sxs-lookup"><span data-stu-id="06249-218"><a id="subheading-7"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="06249-219">È possibile configurare il controllo nel database SQL di Azure anche con gli strumenti di automazione seguenti.</span><span class="sxs-lookup"><span data-stu-id="06249-219">You can also configure auditing in Azure SQL Database by using the following automation tools:</span></span>

* <span data-ttu-id="06249-220">**Cmdlet di PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="06249-220">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="06249-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="06249-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="06249-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="06249-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="06249-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="06249-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="06249-224">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="06249-224">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="06249-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="06249-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="06249-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="06249-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="06249-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="06249-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

   <span data-ttu-id="06249-228">Per un esempio di script, vedere [Configurare il controllo del database SQL e il rilevamento delle minacce usando PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="06249-228">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

* <span data-ttu-id="06249-229">**API REST per il controllo BLOB**:</span><span class="sxs-lookup"><span data-stu-id="06249-229">**REST API - Blob auditing**:</span></span>

   * [<span data-ttu-id="06249-230">Creare o aggiornare i criteri controllo BLOB del database</span><span class="sxs-lookup"><span data-stu-id="06249-230">Create or Update Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [<span data-ttu-id="06249-231">Creare o aggiornare i criteri controllo BLOB del server</span><span class="sxs-lookup"><span data-stu-id="06249-231">Create or Update Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [<span data-ttu-id="06249-232">Ottenere i criteri controllo BLOB del database</span><span class="sxs-lookup"><span data-stu-id="06249-232">Get Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [<span data-ttu-id="06249-233">Ottenere i criteri controllo BLOB del server</span><span class="sxs-lookup"><span data-stu-id="06249-233">Get Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [<span data-ttu-id="06249-234">Ottenere il risultato dell'operazione di controllo BLOB del server</span><span class="sxs-lookup"><span data-stu-id="06249-234">Get Server Blob Auditing Operation Result</span></span>](https://msdn.microsoft.com/library/azure/mt771862.aspx)


<!--Anchors-->
[Azure SQL Database Auditing overview]: #subheading-1
[Set up auditing for your database]: #subheading-2
[Analyze audit logs and reports]: #subheading-3
[Practices for usage in production]: #subheading-5
[Storage Key Regeneration]: #subheading-6
[Automation (PowerShell / REST API)]: #subheading-7
[Blob/Table differences in Server auditing policy inheritance]: (#subheading-8)  

<!--Image references-->
[1]: ./media/sql-database-auditing-get-started/1_auditing_get_started_settings.png
[2]: ./media/sql-database-auditing-get-started/2_auditing_get_started_server_inherit.png
[3]: ./media/sql-database-auditing-get-started/3_auditing_get_started_turn_on.png
[4]: ./media/sql-database-auditing-get-started/4_auditing_get_started_storage_details.png
[5]: ./media/sql-database-auditing-get-started/5_auditing_get_started_storage_key_regeneration.png
[6]: ./media/sql-database-auditing-get-started/6_auditing_get_started_regenerate_key.png
[7]: ./media/sql-database-auditing-get-started/7_auditing_get_started_blob_view_audit_logs.png
[8]: ./media/sql-database-auditing-get-started/8_auditing_get_started_blob_audit_records.png
[9]: ./media/sql-database-auditing-get-started/9_auditing_get_started_ssms_1.png
[10]: ./media/sql-database-auditing-get-started/10_auditing_get_started_ssms_2.png

[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy
