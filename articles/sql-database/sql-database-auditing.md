---
title: aaaGet avviato al controllo del database SQL di Azure | Documenti Microsoft
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
ms.openlocfilehash: 5494c602d702ac41992520f900c393a98cc7c989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-auditing"></a><span data-ttu-id="9a5f7-103">Introduzione al controllo del database SQL</span><span class="sxs-lookup"><span data-stu-id="9a5f7-103">Get started with SQL database auditing</span></span>
<span data-ttu-id="9a5f7-104">Controllo del database SQL Azure tiene traccia degli eventi di database e li scrive i log di controllo tooan nell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-104">Azure SQL database auditing tracks database events and writes them tooan audit log in your Azure storage account.</span></span> <span data-ttu-id="9a5f7-105">Inoltre, il servizio di controllo:</span><span class="sxs-lookup"><span data-stu-id="9a5f7-105">Auditing also:</span></span>

* <span data-ttu-id="9a5f7-106">Consente di gestire la conformità alle normative, ottenere informazioni sull'attività del database e rilevare discrepanze e anomalie che potrebbero indicare problemi aziendali o possibili violazioni della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-106">Helps you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

* <span data-ttu-id="9a5f7-107">Abilita e facilita norme toocompliance la conformità, anche se non garantisce la conformità.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-107">Enables and facilitates adherence toocompliance standards, although it doesn't guarantee compliance.</span></span> <span data-ttu-id="9a5f7-108">Per ulteriori informazioni su Azure programmi tale conformità agli standard di supporto, vedere hello [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span><span class="sxs-lookup"><span data-stu-id="9a5f7-108">For more information about Azure programs that support standards compliance, see hello [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span></span>


## <span data-ttu-id="9a5f7-109"><a id="subheading-1"></a>Panoramica del servizio di controllo del database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="9a5f7-109"><a id="subheading-1"></a>Azure SQL database auditing overview</span></span>
<span data-ttu-id="9a5f7-110">È possibile usare il servizio di controllo del database SQL per eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="9a5f7-110">You can use SQL database auditing to:</span></span>


* <span data-ttu-id="9a5f7-111">**Conservare** un audit trail di eventi selezionati.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-111">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="9a5f7-112">È possibile definire le categorie di database azioni toobe controllato.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-112">You can define categories of database actions toobe audited.</span></span>
* <span data-ttu-id="9a5f7-113">**Creare report** sulle attività del database.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-113">**Report** on database activity.</span></span> <span data-ttu-id="9a5f7-114">È possibile utilizzare i report preconfigurati e tooget un dashboard iniziare rapidamente con attività e la notifica degli eventi.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-114">You can use preconfigured reports and a dashboard tooget started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="9a5f7-115">**Analizzare** i report.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-115">**Analyze** reports.</span></span> <span data-ttu-id="9a5f7-116">È possibile individuare eventi sospetti, attività insolite e tendenze.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-116">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="9a5f7-117">È possibile configurare il controllo per diversi tipi di categorie di eventi, come illustrato in hello [impostare il controllo per il database](#subheading-2) sezione.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-117">You can configure auditing for different types of event categories, as explained in hello [Set up auditing for your database](#subheading-2) section.</span></span>

<span data-ttu-id="9a5f7-118">I log di controllo vengono scritti nell'archiviazione Blob tooAzure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-118">Audit logs are written tooAzure Blob storage on your Azure subscription.</span></span>


## <span data-ttu-id="9a5f7-119"><a id="subheading-8"></a>Definire criteri di controllo a livello di server o a livello di database</span><span class="sxs-lookup"><span data-stu-id="9a5f7-119"><a id="subheading-8"></a>Define server-level vs. database-level auditing policy</span></span>

<span data-ttu-id="9a5f7-120">I criteri di controllo possono essere definiti per un database specifico o come criteri server predefiniti:</span><span class="sxs-lookup"><span data-stu-id="9a5f7-120">An auditing policy can be defined for a specific database or as a default server policy:</span></span>

* <span data-ttu-id="9a5f7-121">Un criterio server applica tooall esistenti e nuovi database creati nel server di hello.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-121">A server policy applies tooall existing and newly created databases on hello server.</span></span>

* <span data-ttu-id="9a5f7-122">Se *è abilitato il controllo blob server*, si *applica sempre toohello database* (vale a dire database hello verrà controllati), indipendentemente dal database hello le impostazioni di controllo.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-122">If *server blob auditing is enabled*, it *always applies toohello database* (that is, hello database will be audited), regardless of hello database auditing settings.</span></span>

* <span data-ttu-id="9a5f7-123">Abilitare il controllo sul database hello, in aggiunta tooenabling nel server di hello, blob verrà *non* eseguire l'override o modificare le impostazioni di hello del controllo di hello server blob.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-123">Enabling blob auditing on hello database, in addition tooenabling it on hello server, will *not* override or change any of hello settings of hello server blob auditing.</span></span> <span data-ttu-id="9a5f7-124">I due controlli coesisteranno.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-124">Both audits will exist side by side.</span></span> <span data-ttu-id="9a5f7-125">In altre parole, il database di hello verrà controllato due volte in parallelo (una volta dal criterio di server hello e una volta dai criteri database hello).</span><span class="sxs-lookup"><span data-stu-id="9a5f7-125">In other words, hello database will be audited twice in parallel (once by hello server policy and once by hello database policy).</span></span>

   > [!NOTE]
   > <span data-ttu-id="9a5f7-126">È consigliabile evitare di abilitare contemporaneamente il controllo BLOB del server e il controllo BLOB del database ad eccezione dei casi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9a5f7-126">You should avoid enabling both server blob auditing and database blob auditing together, unless:</span></span>
    > * <span data-ttu-id="9a5f7-127">Si desidera un altro toouse *account di archiviazione* o *periodo di memorizzazione* per un database specifico.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-127">You want toouse a different *storage account* or *retention period* for a specific database.</span></span>
    > * <span data-ttu-id="9a5f7-128">Si desidera tooaudit evento tipi o categorie per un database specifico che differiscono dai tipi di evento o alle categorie che vengono controllate per rest hello database hello hello server.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-128">You want tooaudit event types or categories for a specific database that differ from event types or categories that are being audited for hello rest of hello databases on hello server.</span></span> <span data-ttu-id="9a5f7-129">Ad esempio, potrebbe essere inserimenti nella tabella che devono toobe controllati solo per un database specifico.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-129">For example, you might have table inserts that need toobe audited only for a specific database.</span></span>
   > 
   > <span data-ttu-id="9a5f7-130">In caso contrario, è consigliabile abilitare il servizio controllo blob solo a livello di server e lasciare controllo a livello di database hello disabilitato per tutti i database.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-130">Otherwise, we recommended that you enable only server-level blob auditing and leave hello database-level auditing disabled for all databases.</span></span>


## <span data-ttu-id="9a5f7-131"><a id="subheading-2"></a>Configurare il controllo per il database</span><span class="sxs-lookup"><span data-stu-id="9a5f7-131"><a id="subheading-2"></a>Set up auditing for your database</span></span>
<span data-ttu-id="9a5f7-132">Hello nella sezione seguente descrive hello configurazione di controllo utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-132">hello following section describes hello configuration of auditing using hello Azure portal.</span></span>

1. <span data-ttu-id="9a5f7-133">Passare toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9a5f7-133">Go toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9a5f7-134">Passare toohello **impostazioni** blade di hello SQL database di SQL server si desidera tooaudit.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-134">Go toohello **Settings** blade of hello SQL database/SQL server you want tooaudit.</span></span> <span data-ttu-id="9a5f7-135">In hello **impostazioni** pannello seleziona **rilevamento controllo & minaccia**.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-135">In hello **Settings** blade, select **Auditing & Threat detection**.</span></span>

    <span data-ttu-id="9a5f7-136"><a id="auditing-screenshot"></a>![Riquadro di spostamento][1]</span><span class="sxs-lookup"><span data-stu-id="9a5f7-136"><a id="auditing-screenshot"></a> ![Navigation pane][1]</span></span>
3. <span data-ttu-id="9a5f7-137">Se si preferisce tooset un criterio di controllo server (che verranno applicati tooall esistenti e nuovi database creati in questo server), è possibile selezionare hello **visualizzare impostazioni del server** collegamento nel Pannello di controllo database hello.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-137">If you prefer tooset up a server auditing policy (which will apply tooall existing and newly created databases on this server), you can select hello **View server settings** link in hello database auditing blade.</span></span> <span data-ttu-id="9a5f7-138">È possibile visualizzare o modificare le impostazioni di controllo server hello.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-138">You can then view or modify hello server auditing settings.</span></span>

    ![Riquadro di spostamento][2]
4. <span data-ttu-id="9a5f7-140">Se si preferisce tooenable blob controllo a livello di database hello (in aggiunta tooor anziché il controllo a livello di server), per **controllo**selezionare **ON**e per **il controllo tipo** , selezionare **Blob**.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-140">If you prefer tooenable blob auditing on hello database level (in addition tooor instead of server-level auditing), for **Auditing**, select **ON**, and for **Auditing type**, select  **Blob**.</span></span>

    <span data-ttu-id="9a5f7-141">Se il servizio controllo blob server è abilitato, controllo database configurato hello esisterà in modo affiancato con controllo del blob hello server.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-141">If server blob auditing is enabled, hello database-configured audit will exist side by side with hello server blob audit.</span></span>  

    ![Riquadro di spostamento][3]
5. <span data-ttu-id="9a5f7-143">hello tooopen **Audit Log archiviazione** pannello seleziona **dettagli archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-143">tooopen hello **Audit Logs Storage** blade, select **Storage Details**.</span></span> <span data-ttu-id="9a5f7-144">Selezionare l'account di archiviazione di Azure hello in cui verranno salvati i log e quindi selezionare il periodo di memorizzazione hello, dopo il quale hello verranno eliminati i log precedenti.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-144">Select hello Azure storage account where logs will be saved, and then select hello retention period, after which hello old logs will be deleted.</span></span> <span data-ttu-id="9a5f7-145">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-145">Then click **OK**.</span></span> 
   >[!TIP] 
   ><span data-ttu-id="9a5f7-146">hello tooget meglio modelli report controllo hello, utilizzare hello stesso account di archiviazione per tutti i database controllati.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-146">tooget hello most out of hello auditing reports templates, use hello same storage account for all audited databases.</span></span> 

    <span data-ttu-id="9a5f7-147"><a id="storage-screenshot"></a>![Riquadro di spostamento][4]</span><span class="sxs-lookup"><span data-stu-id="9a5f7-147"><a id="storage-screenshot"></a> ![Navigation pane][4]</span></span>
6. <span data-ttu-id="9a5f7-148">Se si desidera che gli eventi controllato hello toocustomize, è possibile eseguire questa operazione tramite PowerShell o hello API REST.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-148">If you want toocustomize hello audited events, you can do this via PowerShell or hello REST API.</span></span> <span data-ttu-id="9a5f7-149">Per ulteriori informazioni, vedere hello [automazione (API REST di PowerShell /)](#subheading-7) sezione.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-149">For more details, see hello [Automation (PowerShell/REST API)](#subheading-7) section.</span></span>
7. <span data-ttu-id="9a5f7-150">Dopo aver configurato le impostazioni di controllo, è possibile attivare la nuova funzionalità di rilevamento minacce hello e configurare gli avvisi di sicurezza tooreceive messaggi di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-150">After you've configured your auditing settings, you can turn on hello new threat detection feature and configure emails tooreceive security alerts.</span></span> <span data-ttu-id="9a5f7-151">Quando si usa il rilevamento delle minacce, si ricevono avvisi proattivi sulle attività di database anomale che possono indicare potenziali minacce per la sicurezza.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-151">When you use threat detection, you receive proactive alerts on anomalous database activities that can indicate potential security threats.</span></span> <span data-ttu-id="9a5f7-152">Per altri dettagli, vedere l'[introduzione al rilevamento delle minacce](sql-database-threat-detection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9a5f7-152">For more details, see [Getting started with threat detection](sql-database-threat-detection-get-started.md).</span></span>
8. <span data-ttu-id="9a5f7-153">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-153">Click **Save**.</span></span>





## <span data-ttu-id="9a5f7-154"><a id="subheading-3"></a>Analizzare i log di controllo e i report</span><span class="sxs-lookup"><span data-stu-id="9a5f7-154"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="9a5f7-155">I log di controllo vengono aggregati in hello account di archiviazione di Azure si è scelto durante l'installazione.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-155">Audit logs are aggregated in hello Azure storage account you chose during setup.</span></span> <span data-ttu-id="9a5f7-156">È possibile esplorare i log di controllo con uno strumento come [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="9a5f7-156">You can explore audit logs by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="9a5f7-157">I log del controllo BLOB vengono salvati come raccolta di file BLOB in un contenitore denominato **sqldbauditlogs**.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-157">Blob auditing logs are saved as a collection of blob files within a container named **sqldbauditlogs**.</span></span>

<span data-ttu-id="9a5f7-158">Per ulteriori informazioni sulla gerarchia hello della cartella di archiviazione dei registri di controllo di hello blob, convenzioni di denominazione dei blob e il formato di log, vedere hello [Blob Audit Log formato riferimento (download di file con estensione docx)](https://go.microsoft.com/fwlink/?linkid=829599).</span><span class="sxs-lookup"><span data-stu-id="9a5f7-158">For further details about hello hierarchy of hello blob audit logs storage folder, blob naming conventions, and log format, see hello [Blob Audit Log Format Reference (.docx file download)](https://go.microsoft.com/fwlink/?linkid=829599).</span></span>

<span data-ttu-id="9a5f7-159">Esistono diversi metodi che è possibile utilizzare i blob tooview i registri di controllo:</span><span class="sxs-lookup"><span data-stu-id="9a5f7-159">There are several methods you can use tooview blob auditing logs:</span></span>

* <span data-ttu-id="9a5f7-160">Hello utilizzare [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9a5f7-160">Use hello [Azure portal](https://portal.azure.com).</span></span>  <span data-ttu-id="9a5f7-161">Database rilevanti hello aperto.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-161">Open hello relevant database.</span></span> <span data-ttu-id="9a5f7-162">Hello in cima del database hello **rilevamento controllo & minaccia** pannello, fare clic su **Visualizza log di controllo**.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-162">At hello top of hello database's **Auditing & Threat detection** blade, click **View audit logs**.</span></span>

    ![Riquadro di spostamento][7]

    <span data-ttu-id="9a5f7-164">Un **record di controllo** apre pannello, da cui sarà in grado di tooview hello registri.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-164">An **Audit records** blade opens, from which you'll be able tooview hello logs.</span></span>

    - <span data-ttu-id="9a5f7-165">È possibile visualizzare date specifiche facendo clic su **filtro** nella parte superiore di hello di hello **record di controllo** blade.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-165">You can view specific dates by clicking **Filter** at hello top of hello **Audit records** blade.</span></span>
    - <span data-ttu-id="9a5f7-166">È possibile passare dai record di controllo creati dai criteri del server a quelli creati dai criteri del database e viceversa.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-166">You can switch between audit records that were created by a server policy or database policy audit.</span></span>

       ![Riquadro di spostamento][8]

* <span data-ttu-id="9a5f7-168">Utilizzare la funzione di sistema hello **Sys. fn_get_audit_file** (T-SQL) tooreturn hello controllo dati di log in formato tabulare.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-168">Use hello system function **sys.fn_get_audit_file** (T-SQL) tooreturn hello audit log data in tabular format.</span></span> <span data-ttu-id="9a5f7-169">Per ulteriori informazioni sull'utilizzo di questa funzione, vedere hello [documentazione Sys. fn_get_audit_file](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="9a5f7-169">For more information on using this function, see hello [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span></span>


* <span data-ttu-id="9a5f7-170">Usare **Unisci file di controllo** in SQL Server Management Studio (a partire da SSMS 17):</span><span class="sxs-lookup"><span data-stu-id="9a5f7-170">Use **Merge Audit Files** in SQL Server Management Studio (starting with SSMS 17):</span></span>  
    1. <span data-ttu-id="9a5f7-171">Scegliere dal menu SSMS hello **File** > **aprire** > **i file di controllo di tipo Merge**.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-171">From hello SSMS menu, select **File** > **Open** > **Merge Audit Files**.</span></span>

        ![Riquadro di spostamento][9]
    2. <span data-ttu-id="9a5f7-173">Hello **aggiungere i file di controllo** verrà visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-173">hello **Add Audit Files** dialog box opens.</span></span> <span data-ttu-id="9a5f7-174">Selezionare una delle hello **Aggiungi** opzioni per scegliere se i file di controllo toomerge da una variabile locale del disco o importarli da archiviazione di Azure (si sarà necessario tooprovide i chiave dell'account e i dettagli di archiviazione di Azure).</span><span class="sxs-lookup"><span data-stu-id="9a5f7-174">Select one of hello **Add** options to choose whether toomerge audit files from a local disk or import them from Azure Storage (you will be required tooprovide your Azure Storage details and account key).</span></span>

    3. <span data-ttu-id="9a5f7-175">Dopo essere stati aggiunti tutti i file toomerge, fare clic su **OK** toocomplete l'operazione di unione hello.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-175">After all files toomerge have been added, click **OK** toocomplete hello merge operation.</span></span>

    4. <span data-ttu-id="9a5f7-176">Consente di aprire file sottoposto a merge Hello in SSMS, in cui è possibile visualizzare e analizzarli, nonché di esportazione è tooan XEL o CSV file o tooa della tabella.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-176">hello merged file opens in SSMS, where you can view and analyze it, as well as export it tooan XEL or CSV file or tooa table.</span></span>

* <span data-ttu-id="9a5f7-177">Hello utilizzare [sincronizzazione applicazione](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) che è stata creata.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-177">Use hello [sync application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) that we have created.</span></span> <span data-ttu-id="9a5f7-178">In esecuzione in Azure e prevede l'utilizzo di Operations Management Suite (OMS) Log Analitica pubblica API toopush SQL i log di controllo in OMS.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-178">It runs in Azure and utilizes Operations Management Suite (OMS) Log Analytics public APIs toopush SQL audit logs into OMS.</span></span> <span data-ttu-id="9a5f7-179">applicazione di sincronizzazione Hello indirizza i log di controllo SQL nel Analitica di Log di OMS per l'utilizzo tramite il dashboard di OMS Log Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-179">hello sync application pushes SQL audit logs into OMS Log Analytics for consumption via hello OMS Log Analytics dashboard.</span></span> 

* <span data-ttu-id="9a5f7-180">Usare Power BI.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-180">Use Power BI.</span></span> <span data-ttu-id="9a5f7-181">È possibile visualizzare e analizzare i dati dei log di controllo in Power BI.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-181">You can view and analyze audit log data in Power BI.</span></span> <span data-ttu-id="9a5f7-182">Per altre informazioni, vedere il post di blog su [Power BI e l'accesso a un modello scaricabile](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span><span class="sxs-lookup"><span data-stu-id="9a5f7-182">Learn more about [Power BI, and access a downloadable template](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span></span>

* <span data-ttu-id="9a5f7-183">Scaricare i file di log dal contenitore blob di archiviazione di Azure tramite il portale di hello o tramite uno strumento come [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="9a5f7-183">Download log files from your Azure Storage blob container via hello portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
    * <span data-ttu-id="9a5f7-184">Dopo avere scaricato un file di log in locale, è possibile fare doppio clic su tooopen file hello, visualizzare e analizzare i log di hello in SSMS.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-184">After you have downloaded a log file locally, you can double-click hello file tooopen, view, and analyze hello logs in SSMS.</span></span>
    * <span data-ttu-id="9a5f7-185">È anche possibile scaricare più file contemporaneamente tramite Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-185">You can also download multiple files simultaneously via Azure Storage Explorer.</span></span> <span data-ttu-id="9a5f7-186">Fare doppio clic su una sottocartella specifica (ad esempio, una sottocartella che include tutti i file di log per una data specifica) e selezionare **salvare come** toosave in una cartella locale.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-186">Right-click a specific subfolder (for example, a subfolder that includes all log files for a specific date) and select **Save as** toosave in a local folder.</span></span>

* <span data-ttu-id="9a5f7-187">Altri metodi:</span><span class="sxs-lookup"><span data-stu-id="9a5f7-187">Additional methods:</span></span>
   * <span data-ttu-id="9a5f7-188">Dopo aver scaricato diversi file (o una sottocartella che include i file di log per un giorno intero, come descritto nella precedente hello in questo elenco), è possibile unirli in locale come descritto nelle istruzioni di file di controllo Merge SQL Server Management Studio hello descritte in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-188">After downloading several files (or a subfolder that includes log files for an entire day, as described in hello previous item in this list), you can merge them locally as described in hello SSMS Merge Audit Files instructions described earlier.</span></span>

   * <span data-ttu-id="9a5f7-189">Visualizzare i log del controllo BLOB a livello di codice:</span><span class="sxs-lookup"><span data-stu-id="9a5f7-189">View blob auditing logs programmatically:</span></span>

     * <span data-ttu-id="9a5f7-190">Hello utilizzare [lettore di eventi estesi](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) libreria c#.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-190">Use hello [Extended Events Reader](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# library.</span></span>
     * <span data-ttu-id="9a5f7-191">[Eseguire query sui file di eventi estesi](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-191">[Query Extended Events Files](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) by using PowerShell.</span></span>




## <span data-ttu-id="9a5f7-192"><a id="subheading-5"></a>Procedure nell'ambiente di produzione</span><span class="sxs-lookup"><span data-stu-id="9a5f7-192"><a id="subheading-5"></a>Production practices</span></span>
<!--hello description in this section refers toopreceding screen captures.-->

### <span data-ttu-id="9a5f7-193"><a id="subheading-6">Controllo dei database con replica geografica</a></span><span class="sxs-lookup"><span data-stu-id="9a5f7-193"><a id="subheading-6">Auditing geo-replicated databases</a></span></span>
<span data-ttu-id="9a5f7-194">Quando si utilizzano il database di replica geografica, è possibile tooset il controllo sul database primario hello, database secondario hello o entrambi, in base al tipo di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-194">When you use geo-replicated databases, it is possible tooset up auditing on either hello primary database, hello secondary database, or both, depending on hello audit type.</span></span>

<span data-ttu-id="9a5f7-195">Seguire queste istruzioni (tenere presente che il servizio controllo blob può essere attivato o disattivata solo dal database primario di hello le impostazioni di controllo):</span><span class="sxs-lookup"><span data-stu-id="9a5f7-195">Follow these instructions (remember that blob auditing can be turned on or off only from hello primary database auditing settings):</span></span>

* <span data-ttu-id="9a5f7-196">**Database primario**.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-196">**Primary database**.</span></span> <span data-ttu-id="9a5f7-197">Attivare il controllo di blob, nel server di hello o per hello database, come descritto in hello [impostare il controllo per il database](#subheading-2) sezione.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-197">Turn on blob auditing, either on hello server or on hello database itself, as described in hello [Set up auditing for your database](#subheading-2) section.</span></span>
* <span data-ttu-id="9a5f7-198">**Database secondario**.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-198">**Secondary database**.</span></span> <span data-ttu-id="9a5f7-199">Attivare il controllo di blob nel database primario hello, come descritto in hello [impostare il controllo per il database](#subheading-2) sezione.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-199">Turn on blob auditing on hello primary database, as described in hello [Set up auditing for your database](#subheading-2) section.</span></span> 
   * <span data-ttu-id="9a5f7-200">BLOB deve essere abilitato il controllo su hello *database primario stesso*, non il server hello.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-200">Blob auditing must be enabled on hello *primary database itself*, not hello server.</span></span>
   * <span data-ttu-id="9a5f7-201">Dopo che il servizio controllo blob è abilitato sul database primario hello, anche diventare abilitato nel database secondario hello.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-201">After blob auditing is enabled on hello primary database, it will also become enabled on hello secondary database.</span></span>

     >[!IMPORTANT]
     ><span data-ttu-id="9a5f7-202">Per impostazione predefinita, le impostazioni di archiviazione hello per database secondario hello sarà toothose identici del database primario hello, causando il traffico tra internazionali.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-202">By default, hello storage settings for hello secondary database will be identical toothose of hello primary database, causing cross-regional traffic.</span></span> <span data-ttu-id="9a5f7-203">È possibile evitare questo problema abilitando il servizio controllo blob nel server secondario hello e configurazione dell'archiviazione locale nelle impostazioni di archiviazione di hello server secondario.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-203">You can avoid this by enabling blob auditing on hello secondary server and configuring local storage in hello secondary server storage settings.</span></span> <span data-ttu-id="9a5f7-204">Questo percorso sostituirà il percorso di archiviazione hello per database secondario hello e il risultato in ogni database in cui salvare l'archiviazione toolocal i registri di controllo.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-204">This will override hello storage location for hello secondary database and result in each database saving its audit logs toolocal storage.</span></span>  
<br>

### <span data-ttu-id="9a5f7-205"><a id="subheading-6">Rigenerazione delle chiavi di archiviazione</a></span><span class="sxs-lookup"><span data-stu-id="9a5f7-205"><a id="subheading-6">Storage key regeneration</a></span></span>
<span data-ttu-id="9a5f7-206">Nell'ambiente di produzione, si è probabilmente toorefresh lo spazio di archiviazione chiavi periodicamente.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-206">In production, you are likely toorefresh your storage keys periodically.</span></span> <span data-ttu-id="9a5f7-207">Durante l'aggiornamento delle chiavi, è necessario il criterio di controllo hello tooresave.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-207">When refreshing your keys, you need tooresave hello auditing policy.</span></span> <span data-ttu-id="9a5f7-208">il processo di Hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="9a5f7-208">hello process is as follows:</span></span>

1. <span data-ttu-id="9a5f7-209">Aprire hello **dettagli archiviazione** blade.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-209">Open hello **Storage Details** blade.</span></span> <span data-ttu-id="9a5f7-210">In hello **chiave di accesso di archiviazione** , quindi selezionare **secondario**, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-210">In hello **Storage Access Key** box, select **Secondary**, and click **OK**.</span></span> <span data-ttu-id="9a5f7-211">Quindi fare clic su **salvare** nella parte superiore di hello di hello controllo pannello di configurazione.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-211">Then click **Save** at hello top of hello auditing configuration blade.</span></span>

    ![Riquadro di spostamento][5]
2. <span data-ttu-id="9a5f7-213">Andare a pannello di configurazione di archiviazione toohello e rigenerare la chiave di accesso primaria hello.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-213">Go toohello storage configuration blade and regenerate hello primary access key.</span></span>

    ![Riquadro di spostamento][6]
3. <span data-ttu-id="9a5f7-215">Tornare indietro toohello Pannello di configurazione di controllo, passare hello archiviazione chiave di accesso secondario tooprimary e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-215">Go back toohello auditing configuration blade, switch hello storage access key from secondary tooprimary, and then click **OK**.</span></span> <span data-ttu-id="9a5f7-216">Quindi fare clic su **salvare** nella parte superiore di hello di hello controllo pannello di configurazione.</span><span class="sxs-lookup"><span data-stu-id="9a5f7-216">Then click **Save** at hello top of hello auditing configuration blade.</span></span>
4. <span data-ttu-id="9a5f7-217">Tornare al pannello di configurazione di archiviazione toohello e chiave di accesso secondaria hello rigenerare (in preparazione per il ciclo di aggiornamento della chiave di hello Avanti).</span><span class="sxs-lookup"><span data-stu-id="9a5f7-217">Go back toohello storage configuration blade and regenerate hello secondary access key (in preparation for hello next key's refresh cycle).</span></span>

## <span data-ttu-id="9a5f7-218"><a id="subheading-7"></a>Automazione (API REST/PowerShell)</span><span class="sxs-lookup"><span data-stu-id="9a5f7-218"><a id="subheading-7"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="9a5f7-219">È inoltre possibile configurare il controllo nel Database di SQL Azure utilizzando i seguenti strumenti di automazione hello:</span><span class="sxs-lookup"><span data-stu-id="9a5f7-219">You can also configure auditing in Azure SQL Database by using hello following automation tools:</span></span>

* <span data-ttu-id="9a5f7-220">**Cmdlet di PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="9a5f7-220">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="9a5f7-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="9a5f7-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="9a5f7-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="9a5f7-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="9a5f7-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="9a5f7-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="9a5f7-224">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="9a5f7-224">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="9a5f7-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="9a5f7-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="9a5f7-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="9a5f7-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="9a5f7-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="9a5f7-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

   <span data-ttu-id="9a5f7-228">Per un esempio di script, vedere [Configurare il controllo del database SQL e il rilevamento delle minacce usando PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9a5f7-228">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

* <span data-ttu-id="9a5f7-229">**API REST per il controllo BLOB**:</span><span class="sxs-lookup"><span data-stu-id="9a5f7-229">**REST API - Blob auditing**:</span></span>

   * [<span data-ttu-id="9a5f7-230">Creare o aggiornare i criteri controllo BLOB del database</span><span class="sxs-lookup"><span data-stu-id="9a5f7-230">Create or Update Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [<span data-ttu-id="9a5f7-231">Creare o aggiornare i criteri controllo BLOB del server</span><span class="sxs-lookup"><span data-stu-id="9a5f7-231">Create or Update Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [<span data-ttu-id="9a5f7-232">Ottenere i criteri controllo BLOB del database</span><span class="sxs-lookup"><span data-stu-id="9a5f7-232">Get Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [<span data-ttu-id="9a5f7-233">Ottenere i criteri controllo BLOB del server</span><span class="sxs-lookup"><span data-stu-id="9a5f7-233">Get Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [<span data-ttu-id="9a5f7-234">Ottenere il risultato dell'operazione di controllo BLOB del server</span><span class="sxs-lookup"><span data-stu-id="9a5f7-234">Get Server Blob Auditing Operation Result</span></span>](https://msdn.microsoft.com/library/azure/mt771862.aspx)


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
