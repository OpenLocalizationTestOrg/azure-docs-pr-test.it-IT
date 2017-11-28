---
title: "query di analitica aaaRun su più database SQL di Azure | Documenti Microsoft"
description: Estrarre i dati dai database tenant in un database di analisi per l'analisi offline
keywords: esercitazione database SQL
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: billgib; sstein
ms.openlocfilehash: f2664e4aafd2fecc98d20d229342bca19b0b08c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a><span data-ttu-id="ec977-104">Estrarre i dati dai database tenant in un database di analisi per l'analisi offline</span><span class="sxs-lookup"><span data-stu-id="ec977-104">Extract data from tenant databases into an analytics database for offline analysis</span></span>

<span data-ttu-id="ec977-105">In questa esercitazione è utilizzare una query di toorun processo elastico in tutti i database tenant.</span><span class="sxs-lookup"><span data-stu-id="ec977-105">In this tutorial, you use an elastic job toorun queries against each tenant database.</span></span> <span data-ttu-id="ec977-106">il processo di Hello estrae i dati di vendita di ticket e li carica in un database analitica (o del data warehouse) per l'analisi.</span><span class="sxs-lookup"><span data-stu-id="ec977-106">hello job extracts ticket sales data and loads it into an analytics database (or data warehouse) for analysis.</span></span> <span data-ttu-id="ec977-107">Hello database analitica viene quindi eseguita una query tooextract informazioni approfondite sui dati operativi quotidiane di tutti i tenant.</span><span class="sxs-lookup"><span data-stu-id="ec977-107">hello analytics database is then queried tooextract insights from this day-to-day operational data of all tenants.</span></span>


<span data-ttu-id="ec977-108">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="ec977-108">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ec977-109">Creare database analitica di hello tenant</span><span class="sxs-lookup"><span data-stu-id="ec977-109">Create hello tenant analytics database</span></span>
> * <span data-ttu-id="ec977-110">Creare un processo pianificato tooretrieve dati e popolare il database di analitica hello</span><span class="sxs-lookup"><span data-stu-id="ec977-110">Create a scheduled job tooretrieve data and populate hello analytics database</span></span>

<span data-ttu-id="ec977-111">toocomplete questa esercitazione, assicurarsi che i hello seguenti prerequisiti siano soddisfatti:</span><span class="sxs-lookup"><span data-stu-id="ec977-111">toocomplete this tutorial, make sure hello following prerequisites are met:</span></span>

* <span data-ttu-id="ec977-112">app SaaS Wingtip Hello viene distribuita.</span><span class="sxs-lookup"><span data-stu-id="ec977-112">hello Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="ec977-113">toodeploy in meno di cinque minuti, vedere [Distribuisci ed esplorare l'applicazione SaaS Wingtip hello](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="ec977-113">toodeploy in less than five minutes, see [Deploy and explore hello Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="ec977-114">Azure PowerShell è installato.</span><span class="sxs-lookup"><span data-stu-id="ec977-114">Azure PowerShell is installed.</span></span> <span data-ttu-id="ec977-115">Per informazioni dettagliate, vedere [Introduzione ad Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span><span class="sxs-lookup"><span data-stu-id="ec977-115">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="ec977-116">è installata la versione più recente Hello di SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="ec977-116">hello latest version of SQL Server Management Studio (SSMS) is installed.</span></span> [<span data-ttu-id="ec977-117">Scaricare e installare SSMS</span><span class="sxs-lookup"><span data-stu-id="ec977-117">Download and Install SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a><span data-ttu-id="ec977-118">Modello di analisi operativa del tenant</span><span class="sxs-lookup"><span data-stu-id="ec977-118">Tenant Operational Analytics pattern</span></span>

<span data-ttu-id="ec977-119">Uno dei hello delle opportunità con applicazioni SaaS è toouse hello tenant avanzato i dati archiviati nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="ec977-119">One of hello great opportunities with SaaS applications is toouse hello rich tenant data that is stored in hello cloud.</span></span> <span data-ttu-id="ec977-120">Utilizzare questo dati toogain approfondite operazione hello e l'utilizzo dell'applicazione e i tenant.</span><span class="sxs-lookup"><span data-stu-id="ec977-120">Use this data toogain insights into hello operation and usage of your application, and your tenants.</span></span> <span data-ttu-id="ec977-121">Questi dati possono assistere lo sviluppo di funzionalità e miglioramenti altri investimenti in app hello e piattaforma.</span><span class="sxs-lookup"><span data-stu-id="ec977-121">This data can guide feature development, usability improvements, and other investments in hello app and platform.</span></span> <span data-ttu-id="ec977-122">L'accesso a questi dati è semplice quando sono raccolti in un singolo database multi-tenant, ma non è altrettanto semplice in una distribuzione su larga scala potenzialmente in migliaia di database.</span><span class="sxs-lookup"><span data-stu-id="ec977-122">Accessing this data when it's in a single multi-tenant database is easy, but not so easy when distributed at scale across potentially thousands of databases.</span></span> <span data-ttu-id="ec977-123">Un approccio tooaccessing questi dati sono processi toouse elastico, abilitare i risultati della query che restituiscono risultati dal processo esecuzione toobe acquisiti in un database di output e una tabella.</span><span class="sxs-lookup"><span data-stu-id="ec977-123">One approach tooaccessing this data is toouse Elastic jobs, which enable result-returning query results from job execution toobe captured in an output database and table.</span></span>

## <a name="get-hello-wingtip-application-scripts"></a><span data-ttu-id="ec977-124">Ottenere script per l'applicazione hello Wingtip</span><span class="sxs-lookup"><span data-stu-id="ec977-124">Get hello Wingtip application scripts</span></span>

<span data-ttu-id="ec977-125">Hello Wingtip SaaS script e codice sorgente dell'applicazione sono disponibili in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repository github.</span><span class="sxs-lookup"><span data-stu-id="ec977-125">hello Wingtip SaaS scripts and application source code are available in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="ec977-126">[I passaggi di script di SaaS Wingtip hello toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span><span class="sxs-lookup"><span data-stu-id="ec977-126">[Steps toodownload hello Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="deploy-a-database-for-tenant-analytics-results"></a><span data-ttu-id="ec977-127">Distribuire un database per i risultati di analisi dei tenant</span><span class="sxs-lookup"><span data-stu-id="ec977-127">Deploy a database for tenant analytics results</span></span>

<span data-ttu-id="ec977-128">In questa esercitazione è necessario toohave che Hello di toocapture distribuito un database risultante dall'esecuzione del processo di script, che contengono query che restituiscono risultati.</span><span class="sxs-lookup"><span data-stu-id="ec977-128">This tutorial requires you toohave a database deployed toocapture hello results from job execution of scripts, which contain results-returning queries.</span></span> <span data-ttu-id="ec977-129">Per iniziare verrà creato un database denominato tenantanalytics a questo scopo.</span><span class="sxs-lookup"><span data-stu-id="ec977-129">Let's create a database called tenantanalytics for this purpose.</span></span>

1. <span data-ttu-id="ec977-130">Apri... \\Moduli learning\\Analitica Operational\\Tenant Analitica\\*Demo TenantAnalyticsDB.ps1* in hello *PowerShell ISE* e impostare Hello il valore seguente:</span><span class="sxs-lookup"><span data-stu-id="ec977-130">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in hello *PowerShell ISE* and set hello following value:</span></span>
   * <span data-ttu-id="ec977-131">**$DemoScenario** = **2***Distribuire il database di analisi operativo*</span><span class="sxs-lookup"><span data-stu-id="ec977-131">**$DemoScenario** = **2** *Deploy operational analytics database*</span></span>
1. <span data-ttu-id="ec977-132">Premere **F5** script dimostrativo di hello toorun (hello che chiama *Distribuisci TenantAnalyticsDB.ps1* script) che consente di creare database analitica di hello tenant.</span><span class="sxs-lookup"><span data-stu-id="ec977-132">Press **F5** toorun hello demo script (that calls hello *Deploy-TenantAnalyticsDB.ps1* script) which creates hello tenant analytics database.</span></span>

## <a name="create-some-data-for-hello-demo"></a><span data-ttu-id="ec977-133">Creare alcuni dati per la demo hello</span><span class="sxs-lookup"><span data-stu-id="ec977-133">Create some data for hello demo</span></span>

1. <span data-ttu-id="ec977-134">Apri... \\Moduli learning\\Analitica Operational\\Tenant Analitica\\*Demo TenantAnalyticsDB.ps1* in hello *PowerShell ISE* e impostare Hello il valore seguente:</span><span class="sxs-lookup"><span data-stu-id="ec977-134">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in hello *PowerShell ISE* and set hello following value:</span></span>
   * <span data-ttu-id="ec977-135">**$DemoScenario** = **1***Acquistare biglietti per gli eventi in tutte le sedi*</span><span class="sxs-lookup"><span data-stu-id="ec977-135">**$DemoScenario** = **1** *Purchase tickets for events at all venues*</span></span>
1. <span data-ttu-id="ec977-136">Premere **F5** toorun hello script e creare ticket di cronologia di acquisto.</span><span class="sxs-lookup"><span data-stu-id="ec977-136">Press **F5** toorun hello script and create ticket purchasing history.</span></span>


## <a name="create-a-scheduled-job-tooretrieve-tenant-analytics-about-ticket-purchases"></a><span data-ttu-id="ec977-137">Creare un analitica di tenant ScheduledJob tooretrieve sugli acquisti di ticket</span><span class="sxs-lookup"><span data-stu-id="ec977-137">Create a scheduled job tooretrieve tenant analytics about ticket purchases</span></span>

<span data-ttu-id="ec977-138">Questo script crea informazioni di acquisto un processo tooretrieve ticket da tutti i tenant.</span><span class="sxs-lookup"><span data-stu-id="ec977-138">This script creates a job tooretrieve ticket purchase information from all tenants.</span></span> <span data-ttu-id="ec977-139">Una volta aggregato in una singola tabella, è possibile ottenere metriche dettagliate sull'acquisto di modelli tra tenant hello ticket.</span><span class="sxs-lookup"><span data-stu-id="ec977-139">Once aggregated into a single table, you can gain rich insightful metrics about ticket purchasing patterns across hello tenants.</span></span>

1. <span data-ttu-id="ec977-140">Aprire SQL Server Management Studio e connettersi toohello catalogo -&lt;utente&gt;. database.windows.net server</span><span class="sxs-lookup"><span data-stu-id="ec977-140">Open SSMS and connect toohello catalog-&lt;user&gt;.database.windows.net server</span></span>
1. <span data-ttu-id="ec977-141">Aprire ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*</span><span class="sxs-lookup"><span data-stu-id="ec977-141">Open ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="ec977-142">Modificare &lt;utente&gt;, utilizza hello utente il nome utilizzato per la distribuzione di app SaaS Wingtip hello nella parte superiore di hello dello script hello **sp\_aggiungere\_destinazione\_gruppo\_membro** e **sp\_aggiungere\_jobstep**</span><span class="sxs-lookup"><span data-stu-id="ec977-142">Modify &lt;User&gt;, use hello user name used when you deployed hello Wingtip SaaS app at hello top of hello script, **sp\_add\_target\_group\_member** and **sp\_add\_jobstep**</span></span>
1. <span data-ttu-id="ec977-143">Fare clic destro, selezionare **connessione**e collegare il catalogo toohello -&lt;utente&gt;. database.windows.net server, se non è già connesso.</span><span class="sxs-lookup"><span data-stu-id="ec977-143">Right click, select **Connection**, and connect toohello catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="ec977-144">Verificare di essere connesso toohello **jobaccount** database e premere **F5** per eseguire script hello</span><span class="sxs-lookup"><span data-stu-id="ec977-144">Ensure you are connected toohello **jobaccount** database and press **F5** to run hello script</span></span>

* <span data-ttu-id="ec977-145">**SP\_aggiungere\_destinazione\_gruppo** crea nome gruppo di destinazione hello *TenantGroup*, ora è necessario tooadd membri di destinazione.</span><span class="sxs-lookup"><span data-stu-id="ec977-145">**sp\_add\_target\_group** creates hello target group name *TenantGroup*, now we need tooadd target members.</span></span>
* <span data-ttu-id="ec977-146">**SP\_aggiungere\_destinazione\_gruppo\_membro** aggiunge un *server* che considera tutti i database in tale server (nota hello customer1 - tipo di membro di destinazione &lt;Utente&gt; server che contiene i database tenant hello) fase del processo di esecuzione deve essere inclusi nel processo di hello.</span><span class="sxs-lookup"><span data-stu-id="ec977-146">**sp\_add\_target\_group\_member** adds a *server* target member type, which deems all databases within that server (note this is hello customer1-&lt;User&gt; server containing hello tenant databases) at time of job execution should be included in hello job.</span></span>
* <span data-ttu-id="ec977-147">**sp\_add\_job** crea un nuovo processo pianificato settimanale denominato "Ticket Purchases from all Tenants" (Acquisti di biglietti da tutti i tenant)</span><span class="sxs-lookup"><span data-stu-id="ec977-147">**sp\_add\_job** creates a new weekly scheduled job called “Ticket Purchases from all Tenants”</span></span>
* <span data-ttu-id="ec977-148">**SP\_aggiungere\_jobstep** crea il passaggio di processo hello tooretrieve testo di comando T-SQL contenente tutte le informazioni di acquisto di hello ticket da tutti i tenant e hello copia la restituzione di set di risultati in una tabella denominata  *AllTicketsPurchasesfromAllTenants*</span><span class="sxs-lookup"><span data-stu-id="ec977-148">**sp\_add\_jobstep** creates hello job step containing T-SQL command text tooretrieve all hello ticket purchase information from all tenants and copy hello returning result set into a table called *AllTicketsPurchasesfromAllTenants*</span></span>
* <span data-ttu-id="ec977-149">Hello rimanenti nello script hello visualizzazioni esistenza hello di oggetti hello e l'esecuzione del processo di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="ec977-149">hello remaining views in hello script display hello existence of hello objects and monitor job execution.</span></span> <span data-ttu-id="ec977-150">Esaminare il valore di stato hello da hello **ciclo di vita** stato hello toomonitor della colonna.</span><span class="sxs-lookup"><span data-stu-id="ec977-150">Review hello status value from hello **lifecycle** column toomonitor hello status.</span></span> <span data-ttu-id="ec977-151">Una volta, ha avuto esito positivo, il processo di hello è stata completata in tutti i database tenant e hello due altri database contenenti hello fare riferimento a tabella.</span><span class="sxs-lookup"><span data-stu-id="ec977-151">Once, Succeeded, hello job has successfully finished on all tenant databases and hello two additional databases containing hello reference table.</span></span>

<span data-ttu-id="ec977-152">In esecuzione script hello dovrebbe restituire risultati simili:</span><span class="sxs-lookup"><span data-stu-id="ec977-152">Successfully running hello script should result in similar results:</span></span>

![results](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-tooretrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a><span data-ttu-id="ec977-154">Creare un processo tooretrieve un numero di ticket di riepilogo acquista da tutti i tenant</span><span class="sxs-lookup"><span data-stu-id="ec977-154">Create a job tooretrieve a summary count of ticket purchases from all tenants</span></span>

<span data-ttu-id="ec977-155">Questo script crea una somma tooretrieve processo di tutti gli acquisti di ticket da tutti i tenant.</span><span class="sxs-lookup"><span data-stu-id="ec977-155">This script creates a job tooretrieve sum of all ticket purchases from all tenants.</span></span>

1. <span data-ttu-id="ec977-156">Aprire SQL Server Management Studio e connettersi toohello *catalogo -&lt;utente&gt;. database.windows.net* server</span><span class="sxs-lookup"><span data-stu-id="ec977-156">Open SSMS and connect toohello *catalog-&lt;User&gt;.database.windows.net* server</span></span>
1. <span data-ttu-id="ec977-157">File aperti hello... \\Moduli di formazione\\il provisioning e catalogo\\Analitica Operational\\Tenant Analitica\\*risultati TicketPurchasesfromAllTenants.sql*</span><span class="sxs-lookup"><span data-stu-id="ec977-157">Open hello file …\\Learning Modules\\Provision and Catalog\\Operational Analytics\\Tenant Analytics\\*Results-TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="ec977-158">Modificare &lt;utente&gt;, utilizza hello utente il nome utilizzato per la distribuzione di app SaaS Wingtip hello nello script hello, hello **sp\_aggiungere\_jobstep** stored procedure</span><span class="sxs-lookup"><span data-stu-id="ec977-158">Modify &lt;User&gt;, use hello user name used when you deployed hello Wingtip SaaS app in hello script, in hello **sp\_add\_jobstep** stored procedure</span></span>
1. <span data-ttu-id="ec977-159">Fare clic destro, selezionare **connessione**e collegare il catalogo toohello -&lt;utente&gt;. database.windows.net server, se non è già connesso.</span><span class="sxs-lookup"><span data-stu-id="ec977-159">Right click, select **Connection**, and connect toohello catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="ec977-160">Verificare di essere connesso toohello **tenantanalytics** database e premere **F5** per eseguire script hello</span><span class="sxs-lookup"><span data-stu-id="ec977-160">Ensure you are connected toohello **tenantanalytics** database and press **F5** to run hello script</span></span>

<span data-ttu-id="ec977-161">In esecuzione script hello dovrebbe restituire risultati simili:</span><span class="sxs-lookup"><span data-stu-id="ec977-161">Successfully running hello script should result in similar results:</span></span>

![results](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* <span data-ttu-id="ec977-163">**sp\_add\_job** crea un nuovo processo pianificato settimanale denominato "ResultsTicketsOrders"</span><span class="sxs-lookup"><span data-stu-id="ec977-163">**sp\_add\_job** creates a new weekly scheduled job called “ResultsTicketsOrders”</span></span>

* <span data-ttu-id="ec977-164">**SP\_aggiungere\_jobstep** crea il passaggio di processo hello tooretrieve testo di comando T-SQL contenente tutte le informazioni di acquisto di hello ticket da tutti i tenant e la restituzione di set di risultati in una tabella denominata CountofTicketOrders hello di copia</span><span class="sxs-lookup"><span data-stu-id="ec977-164">**sp\_add\_jobstep** creates hello job step containing T-SQL command text tooretrieve all hello ticket purchase information from all tenants and copy hello returning result set into a table called CountofTicketOrders</span></span>

* <span data-ttu-id="ec977-165">Hello rimanenti nello script hello visualizzazioni esistenza hello di oggetti hello e l'esecuzione del processo di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="ec977-165">hello remaining views in hello script display hello existence of hello objects and monitor job execution.</span></span> <span data-ttu-id="ec977-166">Esaminare il valore di stato hello da hello **ciclo di vita** stato hello toomonitor della colonna.</span><span class="sxs-lookup"><span data-stu-id="ec977-166">Review hello status value from hello **lifecycle** column toomonitor hello status.</span></span> <span data-ttu-id="ec977-167">Una volta, ha avuto esito positivo, il processo di hello è stata completata in tutti i database tenant e hello due altri database contenenti hello fare riferimento a tabella.</span><span class="sxs-lookup"><span data-stu-id="ec977-167">Once, Succeeded, hello job has successfully finished on all tenant databases and hello two additional databases containing hello reference table.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ec977-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ec977-168">Next steps</span></span>

<span data-ttu-id="ec977-169">In questa esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="ec977-169">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ec977-170">Distribuire un database di analisi dei tenant</span><span class="sxs-lookup"><span data-stu-id="ec977-170">Deploy a tenant analytics database</span></span>
> * <span data-ttu-id="ec977-171">Creare un processo pianificato tooretrieve analitiche di dati tra i tenant</span><span class="sxs-lookup"><span data-stu-id="ec977-171">Create a scheduled job tooretrieve analytical data across tenants</span></span>

<span data-ttu-id="ec977-172">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="ec977-172">Congratulations!</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ec977-173">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ec977-173">Additional resources</span></span>

* <span data-ttu-id="ec977-174">Ulteriori [esercitazioni in cui si basano su hello applicazione SaaS Wingtip](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="ec977-174">Additional [tutorials that build upon hello Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="ec977-175">Processi elastici</span><span class="sxs-lookup"><span data-stu-id="ec977-175">Elastic Jobs</span></span>](sql-database-elastic-jobs-overview.md)
