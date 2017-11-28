---
title: i database in Azure SQL Data Warehouse aaaManage | Documenti Microsoft
description: "Panoramica della gestione dei database di SQL Data Warehouse. Include strumenti di gestione, prestazioni di DWU e di scalabilità orizzontale, risoluzione dei problemi di prestazioni delle query, definizione dei criteri di protezione e ripristino di un database da un danneggiamento dei dati o da un'interruzione dell'alimentazione locale."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 8576fdb3-71fe-4b3b-a4e0-5e8a7f148acf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: caec6572c4ab395107c3b095adc69a53eae8bd88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-databases-in-azure-sql-data-warehouse"></a><span data-ttu-id="035fa-104">Gestire i database in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="035fa-104">Manage databases in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="035fa-105">SQL Data Warehouse automatizza molti aspetti della gestione dei database.</span><span class="sxs-lookup"><span data-stu-id="035fa-105">SQL Data Warehouse automates many aspects of managing your databases.</span></span> <span data-ttu-id="035fa-106">Ad esempio, prestazioni tooscale sufficiente tooadjust e pagare hello livello a destra delle risorse di calcolo e quindi consentire SQL Data Warehouse eseguire tutto il lavoro hello di scalabilità orizzontale e scalabilità back.</span><span class="sxs-lookup"><span data-stu-id="035fa-106">For example, tooscale performance you only need tooadjust and pay for hello right level of compute resources, and then let SQL Data Warehouse do all hello work of scaling out and scaling back.</span></span>

<span data-ttu-id="035fa-107">È sicuramente consigliabile toomonitor tooidentify il carico di lavoro, le prestazioni è necessario, nonché risolvere i problemi relativi a query con esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="035fa-107">You will undoubtedly want toomonitor your workload tooidentify your performance needs as well as troubleshoot long-running queries.</span></span> <span data-ttu-id="035fa-108">È inoltre necessario tooperform alcune autorizzazioni toomanage attività di protezione per gli utenti e account di accesso.</span><span class="sxs-lookup"><span data-stu-id="035fa-108">You will also need tooperform a few security tasks toomanage permissions for users and logins.</span></span>

<span data-ttu-id="035fa-109">Questa panoramica illustra questi aspetti della gestione di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="035fa-109">This overview covers these aspects of managing SQL Data Warehouse.</span></span>

* <span data-ttu-id="035fa-110">Strumenti di gestione</span><span class="sxs-lookup"><span data-stu-id="035fa-110">Management tools</span></span>
* <span data-ttu-id="035fa-111">Ridimensionare le risorse di calcolo</span><span class="sxs-lookup"><span data-stu-id="035fa-111">Scale Compute</span></span>
* <span data-ttu-id="035fa-112">Sospendere e riprendere</span><span class="sxs-lookup"><span data-stu-id="035fa-112">Pause and Resume</span></span>
* <span data-ttu-id="035fa-113">Procedure consigliate per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="035fa-113">Performance Best Practices</span></span>
* <span data-ttu-id="035fa-114">Monitoraggio delle query</span><span class="sxs-lookup"><span data-stu-id="035fa-114">Query Monitoring</span></span>
* <span data-ttu-id="035fa-115">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="035fa-115">Security</span></span>
* <span data-ttu-id="035fa-116">Backup e ripristino</span><span class="sxs-lookup"><span data-stu-id="035fa-116">Backup and restore</span></span>

## <a name="management-tools"></a><span data-ttu-id="035fa-117">Strumenti di gestione</span><span class="sxs-lookup"><span data-stu-id="035fa-117">Management tools</span></span>
<span data-ttu-id="035fa-118">È possibile utilizzare vari strumenti toomanage database in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="035fa-118">You can use a variety of tools toomanage databases in SQL Data Warehouse.</span></span> <span data-ttu-id="035fa-119">Per la gestione di database, si svilupperà preferenze dello strumento per ogni tipo di attività è necessario tooperform.</span><span class="sxs-lookup"><span data-stu-id="035fa-119">As you manage databases, you will develop tool preferences for each type of task you need tooperform.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="035fa-120">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="035fa-120">Azure portal</span></span>
<span data-ttu-id="035fa-121">Hello [portale di Azure] [ Azure portal] è un portale basato sul web in cui è possibile creare, aggiornare ed eliminare i database e monitorare le risorse del database.</span><span class="sxs-lookup"><span data-stu-id="035fa-121">hello [Azure portal][Azure portal] is a web-based portal where you can create, update, and delete databases and monitor database resources.</span></span> <span data-ttu-id="035fa-122">Questo strumento è molto utile se sta semplicemente Introduzione a Azure, gestisce un numero ridotto di database del data warehouse o necessario tooquickly eseguire un'operazione.</span><span class="sxs-lookup"><span data-stu-id="035fa-122">This tool is great is if you're just getting started with Azure, managing a small number of data warehouse databases, or need tooquickly do something.</span></span>

<span data-ttu-id="035fa-123">tooget introduttiva hello portale di Azure, vedere [creare un Data Warehouse di SQL (portale di Azure)][Create a SQL Data Warehouse (Azure portal)].</span><span class="sxs-lookup"><span data-stu-id="035fa-123">tooget started with hello Azure portal, see [Create a SQL Data Warehouse (Azure portal)][Create a SQL Data Warehouse (Azure portal)].</span></span>

### <a name="sql-server-data-tools-in-visual-studio"></a><span data-ttu-id="035fa-124">SQL Server Data Tools in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="035fa-124">SQL Server Data Tools in Visual Studio</span></span>
<span data-ttu-id="035fa-125">[SQL Server Data Tools] [ SQL Server Data Tools] (SSDT) in Visual Studio consente tooconnect gestire e sviluppare i database.</span><span class="sxs-lookup"><span data-stu-id="035fa-125">[SQL Server Data Tools][SQL Server Data Tools] (SSDT) in Visual Studio allows you tooconnect to, manage, and develop your databases.</span></span> <span data-ttu-id="035fa-126">È opportuno che gli sviluppatori di applicazioni con una certa familiarità con Visual Studio o altri ambienti di sviluppo integrato (IDE), provino a usare SSDT in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="035fa-126">If you're an application developer familiar with Visual Studio or other integrated development environments (IDEs), try using SSDT in Visual Studio.</span></span>

<span data-ttu-id="035fa-127">SSDT include hello Esplora oggetti SQL Server che consentono di toovisualize, connettersi ed eseguire gli script nei database di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="035fa-127">SSDT includes hello SQL Server Object Explorer which enables you toovisualize, connect, and execute scripts against SQL Data Warehouse databases.</span></span> <span data-ttu-id="035fa-128">tooquickly connettersi tooSQL Data Warehouse, è possibile scegliere semplicemente hello **aperta in Visual Studio** pulsante nella barra dei comandi di hello quando si visualizzano i dettagli del database hello in hello portale classico di Azure.</span><span class="sxs-lookup"><span data-stu-id="035fa-128">tooquickly connect tooSQL Data Warehouse, you can simply click hello **Open in Visual Studio** button in hello command bar when viewing hello database details in hello Azure Classic Portal.</span></span>  

<span data-ttu-id="035fa-129">tooget introduttivi di SSDT in Visual Studio, vedere [Query Azure SQL Data Warehouse con Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="035fa-129">tooget started with SSDT in Visual Studio, see [Query Azure SQL Data Warehouse with Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].</span></span>

### <a name="command-line-tools"></a><span data-ttu-id="035fa-130">Strumenti da riga di comando</span><span class="sxs-lookup"><span data-stu-id="035fa-130">Command-line tools</span></span>
<span data-ttu-id="035fa-131">Gli strumenti da riga di comando sono ideali per l'automazione dei carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="035fa-131">Command line tools are ideal for automating your workloads.</span></span>  <span data-ttu-id="035fa-132">PowerShell e sqlcmd sono due modi tooautomate dei processi.</span><span class="sxs-lookup"><span data-stu-id="035fa-132">PowerShell and sqlcmd are two great ways tooautomate your processes.</span></span>  <span data-ttu-id="035fa-133">Si consiglia di questi strumenti per gestire un numero elevato di server logici e distribuire le modifiche di risorsa in un ambiente di produzione come attività hello necessarie possono essere inseriti nello script e quindi automatizzata.</span><span class="sxs-lookup"><span data-stu-id="035fa-133">We recommend these tools for managing a large number of logical servers and deploying resource changes in a production environment as hello tasks necessary can be scripted and then automated.</span></span>

### <a name="dynamic-management-views"></a><span data-ttu-id="035fa-134">Viste a gestione dinamica</span><span class="sxs-lookup"><span data-stu-id="035fa-134">Dynamic management views</span></span>
<span data-ttu-id="035fa-135">Viste a gestione dinamica sono hello Pane and burro della gestione di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="035fa-135">DMVs are hello bread and butter of managing SQL Data Warehouse.</span></span> <span data-ttu-id="035fa-136">Quasi tutte le informazioni che rende visibili nel portale di hello si basano su viste a gestione dinamica.</span><span class="sxs-lookup"><span data-stu-id="035fa-136">Almost all information that surfaces in hello portal relies on DMVs.</span></span> <span data-ttu-id="035fa-137">vedere un elenco di SQL Data Warehouse DMV, toosee [viste di sistema di SQL Data Warehouse][SQL Data Warehouse system views].</span><span class="sxs-lookup"><span data-stu-id="035fa-137">toosee a list of SQL Data Warehouse DMVs, see [SQL Data Warehouse system views][SQL Data Warehouse system views].</span></span>

<span data-ttu-id="035fa-138">tooget introduzione, vedere [Connect e query con sqlcmd][Connect and query with sqlcmd], e [creare un database (PowerShell)][Create a database (PowerShell)].</span><span class="sxs-lookup"><span data-stu-id="035fa-138">tooget started, see [Connect and query with sqlcmd][Connect and query with sqlcmd], and [Create a database (PowerShell)][Create a database (PowerShell)].</span></span>

## <a name="scale-compute"></a><span data-ttu-id="035fa-139">Ridimensionare le risorse di calcolo</span><span class="sxs-lookup"><span data-stu-id="035fa-139">Scale compute</span></span>
<span data-ttu-id="035fa-140">In SQL Data Warehouse, è possibile aumentare o ridurre rapidamente le prestazioni aumentando o riducendo le risorse di calcolo di CPU, memoria e larghezza di banda di I/O.</span><span class="sxs-lookup"><span data-stu-id="035fa-140">In SQL Data Warehouse, you can quickly scale performance out or back by increasing or decreasing compute resources of CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="035fa-141">prestazioni tooscale, toodo è sufficiente modificare il numero di hello warehouse delle unità di dati (Dwu) in cui SQL Data Warehouse alloca tooyour database.</span><span class="sxs-lookup"><span data-stu-id="035fa-141">tooscale performance, all you need toodo is adjust hello number of data warehouse units (DWUs) that SQL Data Warehouse allocates tooyour database.</span></span> <span data-ttu-id="035fa-142">SQL Data Warehouse rapidamente hello apportata la modifica e gestisce tutti hello sottostante modifiche toohardware o software.</span><span class="sxs-lookup"><span data-stu-id="035fa-142">SQL Data Warehouse quickly makes hello change and handles all hello underlying changes toohardware or software.</span></span>

<span data-ttu-id="035fa-143">vedere toolearn più sulla scalabilità Dwu, [scalare prestazioni].</span><span class="sxs-lookup"><span data-stu-id="035fa-143">toolearn more about scaling DWUs, see [Scale performance].</span></span>

## <a name="pause-and-resume"></a><span data-ttu-id="035fa-144">Sospendere e riprendere</span><span class="sxs-lookup"><span data-stu-id="035fa-144">Pause and resume</span></span>
<span data-ttu-id="035fa-145">toosave costi, è possibile sospendere e riprendere calcolo risorse su richiesta.</span><span class="sxs-lookup"><span data-stu-id="035fa-145">toosave costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="035fa-146">Ad esempio, se si prevede di usare database hello durante la notte hello e i fine settimana, è possibile sospenderla durante le ore e riprenderlo giornata hello.</span><span class="sxs-lookup"><span data-stu-id="035fa-146">For example, if you won't be using hello database during hello night and on weekends, you can pause it during those times, and resume it during hello day.</span></span> <span data-ttu-id="035fa-147">È non verrà addebitato Dwu mentre hello database resta sospesa.</span><span class="sxs-lookup"><span data-stu-id="035fa-147">You won't be charged for DWUs while hello database is paused.</span></span>

<span data-ttu-id="035fa-148">Per altre informazioni, vedere le sezioni [Sospendere il calcolo][Pause compute] e [Riprendere il calcolo][Resume compute].</span><span class="sxs-lookup"><span data-stu-id="035fa-148">For more information, see [Pause compute][Pause compute], and [Resume compute][Resume compute].</span></span>

## <a name="performance-best-practices"></a><span data-ttu-id="035fa-149">Procedure consigliate per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="035fa-149">Performance Best Practices</span></span>
<span data-ttu-id="035fa-150">Attività iniziali con una nuova tecnologia, individuazione hello suggerimenti e consigli che funzionano migliore destra dall'inizio hello può consentire di risparmiare molto tempo.</span><span class="sxs-lookup"><span data-stu-id="035fa-150">When getting started with a new technology, discovering hello tips and tricks that work best right from hello start can save you lots of time.</span></span>  <span data-ttu-id="035fa-151">Sono disponibili procedure consigliate in molti di questi argomenti.</span><span class="sxs-lookup"><span data-stu-id="035fa-151">You will find best practices throughout many of our topics.</span></span>

<span data-ttu-id="035fa-152">toosee molti un riepilogo delle considerazioni più importanti di hello quando si sviluppa il carico di lavoro, vedere [procedure consigliate di SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="035fa-152">toosee many a summary of hello most important considerations when developing your workload, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

## <a name="query-monitoring"></a><span data-ttu-id="035fa-153">Monitoraggio delle query</span><span class="sxs-lookup"><span data-stu-id="035fa-153">Query Monitoring</span></span>
<span data-ttu-id="035fa-154">Talvolta una query è in esecuzione troppo lungo, ma non si è certi di quale è provocato da hello.</span><span class="sxs-lookup"><span data-stu-id="035fa-154">Sometimes a query is running too long, but you aren't sure of which one is hello culprit.</span></span> <span data-ttu-id="035fa-155">SQL Data Warehouse con viste a gestione dinamica (DMV) che è possibile utilizzare toofigure timeout query in cui sta richiedendo troppo tempo.</span><span class="sxs-lookup"><span data-stu-id="035fa-155">SQL Data Warehouse has dynamic management views (DMVs) that you can use toofigure out which query is taking too long.</span></span>

<span data-ttu-id="035fa-156">query con esecuzione prolungata toofind, vedere [monitorare il carico di lavoro mediante DMV][Monitor your workload using DMVs].</span><span class="sxs-lookup"><span data-stu-id="035fa-156">toofind long-running queries, see [Monitor your workload using DMVs][Monitor your workload using DMVs].</span></span>

## <a name="security"></a><span data-ttu-id="035fa-157">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="035fa-157">Security</span></span>
<span data-ttu-id="035fa-158">toomaintain un sistema sicuro, è necessario essere su avviso hello e proteggersi da qualsiasi tipo di accesso non autorizzato.</span><span class="sxs-lookup"><span data-stu-id="035fa-158">toomaintain a secure system, you must be on hello alert and guard against any type of unauthorized access.</span></span> <span data-ttu-id="035fa-159">Un sistema di sicurezza deve toomake che le regole del firewall siano soddisfatti autorizzato in modo che solo gli indirizzi IP possono connettersi.</span><span class="sxs-lookup"><span data-stu-id="035fa-159">A security system needs toomake sure firewall rules are in place so only authorized IP addresses can connect.</span></span> <span data-ttu-id="035fa-160">È necessaria l'autenticazione corretta delle credenziali dell'utente.</span><span class="sxs-lookup"><span data-stu-id="035fa-160">It needs proper authentication of user credentials.</span></span> <span data-ttu-id="035fa-161">Dopo che un utente è connesso toohello database, hello utente deve solo disporre delle autorizzazioni tooperform un numero minimo di azioni.</span><span class="sxs-lookup"><span data-stu-id="035fa-161">After a user has connected toohello database, hello user should only have permissions tooperform a minimal number of actions.</span></span> <span data-ttu-id="035fa-162">toosecure dati, è possibile utilizzare la crittografia.</span><span class="sxs-lookup"><span data-stu-id="035fa-162">toosecure data, you can use encryption.</span></span> <span data-ttu-id="035fa-163">È inoltre importante toohave controllo e di rilevamento in modo è possibile ripercorrere eventi nel caso di eventuali attività sospette.</span><span class="sxs-lookup"><span data-stu-id="035fa-163">It's also important toohave auditing and tracking so you can retrace events if there is any suspicious activity.</span></span>

<span data-ttu-id="035fa-164">toolearn sulla gestione della sicurezza, head su toohello [Cenni preliminari sulla sicurezza][Security overview].</span><span class="sxs-lookup"><span data-stu-id="035fa-164">toolearn about managing security, head over toohello [Security overview][Security overview].</span></span>

## <a name="backup-and-restore"></a><span data-ttu-id="035fa-165">Backup e ripristino</span><span class="sxs-lookup"><span data-stu-id="035fa-165">Backup and restore</span></span>
<span data-ttu-id="035fa-166">Eseguire backup affidabili dei dati è una parte fondamentale di qualsiasi database di produzione.</span><span class="sxs-lookup"><span data-stu-id="035fa-166">Having reliable backps of your data is an essential part of any production database.</span></span> <span data-ttu-id="035fa-167">SQL Data Warehouse tiene al sicuro i dati eseguendo automaticamente il backup dei database attivi a intervalli regolari.</span><span class="sxs-lookup"><span data-stu-id="035fa-167">SQL Data Warehouse keeps your data safe by automatically backing up your active databases at regular intervals.</span></span> <span data-ttu-id="035fa-168">Questi backup consentono toorecover dagli scenari in cui è stato danneggiato i dati o l'eliminazione accidentale dei dati o database.</span><span class="sxs-lookup"><span data-stu-id="035fa-168">These backups allow you toorecover from scenarios where you've corrupted your data or accidentally dropped your data or database.</span></span>  <span data-ttu-id="035fa-169">Per hello dati pianificazione del backup, criteri di conservazione e toorestore un database, vedere [ripristino da snapshot][Restore from snapshot].</span><span class="sxs-lookup"><span data-stu-id="035fa-169">For hello data backup schedule, retention policy and how toorestore a database, see [Restore from snapshot][Restore from snapshot].</span></span>

## <a name="next-steps"></a><span data-ttu-id="035fa-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="035fa-170">Next steps</span></span>
<span data-ttu-id="035fa-171">Principi di progettazione di database appropriata utilizzando renderà più facile toomanage i database in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="035fa-171">Using good database design principles will make it easier toomanage your databases in SQL Data Warehouse.</span></span> <span data-ttu-id="035fa-172">altre, toolearn head su toohello [Cenni preliminari sullo sviluppo][Development overview].</span><span class="sxs-lookup"><span data-stu-id="035fa-172">toolearn more, head over toohello [Development overview][Development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse (Azure Portal)]: sql-data-warehouse-get-started-provision.md
[Create a database (PowerShell)]: sql-data-warehouse-get-started-provision-powershell.md
[connection]: sql-data-warehouse-develop-connections.md
[Query Azure SQL Data Warehouse with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[Connect and query with sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md
[Development overview]: sql-data-warehouse-overview-develop.md
[Monitor your workload using DMVs]: sql-data-warehouse-manage-monitor.md
[Pause compute]: sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Restore from snapshot]: sql-data-warehouse-restore-database-overview.md
[Resume compute]: sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[scalare prestazioni]: sql-data-warehouse-manage-compute-overview.md#scale-compute
[Security overview]: sql-data-warehouse-overview-manage-security.md
[SQL Data Warehouse Best Practices]: sql-data-warehouse-best-practices.md
[SQL Data Warehouse system views]: sql-data-warehouse-reference-tsql-system-views.md

<!--MSDN references-->
[SQL Server Data Tools]: https://msdn.microsoft.com/library/mt204009.aspx

<!--Other web references-->
[Azure portal]: http://portal.azure.com/
