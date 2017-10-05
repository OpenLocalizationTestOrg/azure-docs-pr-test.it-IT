---
title: Domande frequenti su SQL Data Warehouse di Azure | Microsoft Docs
description: In questo articolo sono elencate le domande frequenti su SQL Data Warehouse di Azure poste dai clienti e dagli sviluppatori
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 812CA525-3BF3-49DF-8DF3-FB4342464F4F
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 3/1/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 4c00710ecc0c91f8407eca81b78176075fcbd6ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a><span data-ttu-id="e35cf-103">Domande frequenti su SQL Data Warehouse di Azure</span><span class="sxs-lookup"><span data-stu-id="e35cf-103">SQL Data Warehouse Frequently asked questions</span></span>

## <a name="general"></a><span data-ttu-id="e35cf-104">Generale</span><span class="sxs-lookup"><span data-stu-id="e35cf-104">General</span></span>

<span data-ttu-id="e35cf-105">D:</span><span class="sxs-lookup"><span data-stu-id="e35cf-105">Q.</span></span> <span data-ttu-id="e35cf-106">Cosa offre SQL DW per la protezione dei dati?</span><span class="sxs-lookup"><span data-stu-id="e35cf-106">What does SQL DW offer for data security?</span></span>

<span data-ttu-id="e35cf-107">R.</span><span class="sxs-lookup"><span data-stu-id="e35cf-107">A.</span></span> <span data-ttu-id="e35cf-108">SQL DW offre diverse soluzioni per la protezione dei dati, ad esempio TDE e il controllo.</span><span class="sxs-lookup"><span data-stu-id="e35cf-108">SQL DW offers several solutions for protecting data such as TDE and auditing.</span></span> <span data-ttu-id="e35cf-109">Per altre informazioni, vedere [Sicurezza].</span><span class="sxs-lookup"><span data-stu-id="e35cf-109">For more information, see [Security].</span></span>

<span data-ttu-id="e35cf-110">D:</span><span class="sxs-lookup"><span data-stu-id="e35cf-110">Q.</span></span> <span data-ttu-id="e35cf-111">Dove è possibile trovare gli standard legali o aziendali a cui SQL DW è conforme?</span><span class="sxs-lookup"><span data-stu-id="e35cf-111">Where can I find out what legal or business standards is SQL DW compliant with?</span></span>

<span data-ttu-id="e35cf-112">R.</span><span class="sxs-lookup"><span data-stu-id="e35cf-112">A.</span></span> <span data-ttu-id="e35cf-113">Visitare la pagina [Conformità di Microsoft] per le diverse offerte di conformità per prodotto, ad esempio SOC e ISO.</span><span class="sxs-lookup"><span data-stu-id="e35cf-113">Visit the [Microsoft Compliance] page for various compliance offerings by product such as SOC and ISO.</span></span> <span data-ttu-id="e35cf-114">Scegliere prima in base al titolo di conformità, quindi espandere Azure nella sezione servizi cloud nell'ambito di Microsoft sul lato destro della pagina per visualizzare i servizi conformi ai servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="e35cf-114">First choose by Compliance title, then expand Azure in the Microsoft in-scope cloud services section on the right side of the page to see what services are Azure services are compliant.</span></span>

<span data-ttu-id="e35cf-115">D:</span><span class="sxs-lookup"><span data-stu-id="e35cf-115">Q.</span></span> <span data-ttu-id="e35cf-116">È possibile connettersi a PowerBI?</span><span class="sxs-lookup"><span data-stu-id="e35cf-116">Can I connect PowerBI?</span></span>

<span data-ttu-id="e35cf-117">R.</span><span class="sxs-lookup"><span data-stu-id="e35cf-117">A.</span></span> <span data-ttu-id="e35cf-118">È possibile usarlo.</span><span class="sxs-lookup"><span data-stu-id="e35cf-118">Yes!</span></span> <span data-ttu-id="e35cf-119">Anche se PowerBI supporta la query diretta con SQL DW, non è pensato per un numero elevato di utenti o di dati in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="e35cf-119">Though PowerBI supports direct query with SQL DW, it’s not intended for large number of users or real-time data.</span></span> <span data-ttu-id="e35cf-120">Per l'uso della produzione di PowerBI, è consigliabile usare PowerBI su Azure Analysis Services o IaaS di Analysis Service.</span><span class="sxs-lookup"><span data-stu-id="e35cf-120">For production use of PowerBI, we recommend using PowerBI on top of Azure Analysis Services or Analysis Service IaaS.</span></span> 

<span data-ttu-id="e35cf-121">D:</span><span class="sxs-lookup"><span data-stu-id="e35cf-121">Q.</span></span> <span data-ttu-id="e35cf-122">Quali sono i limiti di capacità di SQL Data Warehouse?</span><span class="sxs-lookup"><span data-stu-id="e35cf-122">What are SQL Data Warehouse Capacity Limits?</span></span>

<span data-ttu-id="e35cf-123">R.</span><span class="sxs-lookup"><span data-stu-id="e35cf-123">A.</span></span> <span data-ttu-id="e35cf-124">Vedere la pagina relativa ai [limiti di capacità] correnti.</span><span class="sxs-lookup"><span data-stu-id="e35cf-124">See our current [capacity limits] page.</span></span> 

<span data-ttu-id="e35cf-125">D:</span><span class="sxs-lookup"><span data-stu-id="e35cf-125">Q.</span></span> <span data-ttu-id="e35cf-126">Perché le operazioni di ridimensionamento, sospensione o ripresa richiedono così tanto tempo?</span><span class="sxs-lookup"><span data-stu-id="e35cf-126">Why is my Scale/Pause/Resume taking so long?</span></span>

<span data-ttu-id="e35cf-127">R.</span><span class="sxs-lookup"><span data-stu-id="e35cf-127">A.</span></span> <span data-ttu-id="e35cf-128">Le operazioni di gestione di calcolo possono essere influenzate da una serie di fattori.</span><span class="sxs-lookup"><span data-stu-id="e35cf-128">A variety of factors can influence the time for compute management operations.</span></span> <span data-ttu-id="e35cf-129">Un caso che si verifica spesso nelle operazioni a esecuzione prolungata è il rollback transazionali.</span><span class="sxs-lookup"><span data-stu-id="e35cf-129">A common case for  long running operations is transactional rollback.</span></span> <span data-ttu-id="e35cf-130">Quando viene avviata un'operazione di sospensione o di ridimensionamento, vengono bloccate tutte le sessioni in ingresso e le query vengono svuotate.</span><span class="sxs-lookup"><span data-stu-id="e35cf-130">When a scale or pause operation is initiated, all incoming sessions are blocked and queries are drained.</span></span> <span data-ttu-id="e35cf-131">Per lasciare il sistema in uno stato stabile, è necessario eseguire il rollback delle transazioni prima di procedere con un'operazione.</span><span class="sxs-lookup"><span data-stu-id="e35cf-131">In order to leave the system in a stable state, transactions must be rolled back before an operation can commence.</span></span> <span data-ttu-id="e35cf-132">Maggiore è il numero di transazioni e maggiori sono le dimensioni del log delle transazioni, più duraturo sarà lo stallo dell'operazione durante il ripristino del sistema a uno stato stabile.</span><span class="sxs-lookup"><span data-stu-id="e35cf-132">The greater the number and larger the log size of transactions, the longer the operation will be stalled restoring the system to a stable state.</span></span>

## <a name="user-support"></a><span data-ttu-id="e35cf-133">Supporto per l'utente</span><span class="sxs-lookup"><span data-stu-id="e35cf-133">User support</span></span>

<span data-ttu-id="e35cf-134">D:</span><span class="sxs-lookup"><span data-stu-id="e35cf-134">Q.</span></span> <span data-ttu-id="e35cf-135">Ho una richiesta di funzionalità, dove posso inviarla?</span><span class="sxs-lookup"><span data-stu-id="e35cf-135">I have a feature request, where do I submit it?</span></span>

<span data-ttu-id="e35cf-136">R.</span><span class="sxs-lookup"><span data-stu-id="e35cf-136">A.</span></span> <span data-ttu-id="e35cf-137">Se si dispone di una richiesta di funzionalità, inviarla alla pagina [UserVoice]</span><span class="sxs-lookup"><span data-stu-id="e35cf-137">If you have a feature request, submit it on our [UserVoice] page</span></span>

<span data-ttu-id="e35cf-138">D:</span><span class="sxs-lookup"><span data-stu-id="e35cf-138">Q.</span></span> <span data-ttu-id="e35cf-139">Come posso fare?</span><span class="sxs-lookup"><span data-stu-id="e35cf-139">How can I do x?</span></span>

<span data-ttu-id="e35cf-140">R.</span><span class="sxs-lookup"><span data-stu-id="e35cf-140">A.</span></span> <span data-ttu-id="e35cf-141">Per assistenza nello sviluppo con SQL Data Warehouse, è possibile porre domande alla pagina [Overflow dello stack].</span><span class="sxs-lookup"><span data-stu-id="e35cf-141">For help in developing with SQL Data Warehouse, you can ask questions on our [Stack Overflow] page.</span></span> 

<span data-ttu-id="e35cf-142">D:</span><span class="sxs-lookup"><span data-stu-id="e35cf-142">Q.</span></span> <span data-ttu-id="e35cf-143">Come posso inviare un ticket di supporto?</span><span class="sxs-lookup"><span data-stu-id="e35cf-143">How do I submit a support ticket?</span></span>

<span data-ttu-id="e35cf-144">R.</span><span class="sxs-lookup"><span data-stu-id="e35cf-144">A.</span></span> <span data-ttu-id="e35cf-145">[I ticket di supporto] possono essere inviati tramite il Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e35cf-145">[Support Tickets] can be filed through Azure portal.</span></span>

## <a name="sql-languagefeature-support"></a><span data-ttu-id="e35cf-146">Supporto per le funzionalità/linguaggio SQL</span><span class="sxs-lookup"><span data-stu-id="e35cf-146">SQL language/feature support</span></span> 

<span data-ttu-id="e35cf-147">D:</span><span class="sxs-lookup"><span data-stu-id="e35cf-147">Q.</span></span> <span data-ttu-id="e35cf-148">Quali tipi di dati sono supportati da SQL Data Warehouse?</span><span class="sxs-lookup"><span data-stu-id="e35cf-148">What datatypes does SQL Data Warehouse support?</span></span>

<span data-ttu-id="e35cf-149">R.</span><span class="sxs-lookup"><span data-stu-id="e35cf-149">A.</span></span> <span data-ttu-id="e35cf-150">Vedere i [tipi di dati] di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e35cf-150">See SQL Data Warehouse [data types].</span></span>

<span data-ttu-id="e35cf-151">D:</span><span class="sxs-lookup"><span data-stu-id="e35cf-151">Q.</span></span> <span data-ttu-id="e35cf-152">Quali funzionalità delle tabelle sono supportate?</span><span class="sxs-lookup"><span data-stu-id="e35cf-152">What table features do you support?</span></span>

<span data-ttu-id="e35cf-153">R.</span><span class="sxs-lookup"><span data-stu-id="e35cf-153">A.</span></span> <span data-ttu-id="e35cf-154">Sebbene SQL Data Warehouse supporti molte funzionalità, alcune non sono supportate. Queste sono documentate in [Funzionalità non supportate delle tabelle].</span><span class="sxs-lookup"><span data-stu-id="e35cf-154">While SQL Data Warehouse supports many features, some are not supported and are documented in [Unsupported Table Features].</span></span>

## <a name="tooling-and-administration"></a><span data-ttu-id="e35cf-155">Strumenti e amministrazione</span><span class="sxs-lookup"><span data-stu-id="e35cf-155">Tooling and administration</span></span>

<span data-ttu-id="e35cf-156">D:</span><span class="sxs-lookup"><span data-stu-id="e35cf-156">Q.</span></span> <span data-ttu-id="e35cf-157">I progetti di Database sono supportati in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e35cf-157">Do you support Database projects in Visual Studio.</span></span>

<span data-ttu-id="e35cf-158">R.</span><span class="sxs-lookup"><span data-stu-id="e35cf-158">A.</span></span> <span data-ttu-id="e35cf-159">Attualmente i progetti di Database non sono supportati in Visual Studio per SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e35cf-159">We currently do not support Database projects in Visual Studio for SQL Data Warehouse.</span></span> <span data-ttu-id="e35cf-160">Se si desidera eseguire il cast di un voto per ottenere questa funzionalità, visitare il forum [richiesta di funzionalità per progetti di Database].</span><span class="sxs-lookup"><span data-stu-id="e35cf-160">If you'd like to cast a vote to get this feature, visit our User Voice [Database projects feature request].</span></span>

<span data-ttu-id="e35cf-161">D:</span><span class="sxs-lookup"><span data-stu-id="e35cf-161">Q.</span></span> <span data-ttu-id="e35cf-162">SQL Data Warehouse supporta le API REST?</span><span class="sxs-lookup"><span data-stu-id="e35cf-162">Does SQL Data Warehouse support REST APIs?</span></span>

<span data-ttu-id="e35cf-163">R.</span><span class="sxs-lookup"><span data-stu-id="e35cf-163">A.</span></span> <span data-ttu-id="e35cf-164">Sì.</span><span class="sxs-lookup"><span data-stu-id="e35cf-164">Yes.</span></span> <span data-ttu-id="e35cf-165">La maggior parte delle funzionalità REST che può essere usata con il Database SQL è disponibile anche con SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e35cf-165">Most REST functionality that can be used with SQL Database is also available with SQL Data Warehouse.</span></span> <span data-ttu-id="e35cf-166">È possibile trovare informazioni sulle API nelle pagine di documentazione REST o in [MSDN].</span><span class="sxs-lookup"><span data-stu-id="e35cf-166">You can find API information within REST documentation pages or [MSDN].</span></span>


## <a name="loading"></a><span data-ttu-id="e35cf-167">Caricamento</span><span class="sxs-lookup"><span data-stu-id="e35cf-167">Loading</span></span>

<span data-ttu-id="e35cf-168">D:</span><span class="sxs-lookup"><span data-stu-id="e35cf-168">Q.</span></span> <span data-ttu-id="e35cf-169">Quali driver client sono supportati?</span><span class="sxs-lookup"><span data-stu-id="e35cf-169">What client drivers do you support?</span></span>

<span data-ttu-id="e35cf-170">R.</span><span class="sxs-lookup"><span data-stu-id="e35cf-170">A.</span></span> <span data-ttu-id="e35cf-171">Il supporto dei driver per DW è reperibile nella pagina delle[stringhe di connessione]</span><span class="sxs-lookup"><span data-stu-id="e35cf-171">Driver support for DW can be found on the [Connection Strings] page</span></span>

<span data-ttu-id="e35cf-172">D: Quali formati di file sono supportati da PolyBase con SQL Data Warehouse?</span><span class="sxs-lookup"><span data-stu-id="e35cf-172">Q: What file formats are supported by PolyBase with SQL Data Warehouse?</span></span>

<span data-ttu-id="e35cf-173">R: Orc, RC, Parquet e testo delimitato semplice</span><span class="sxs-lookup"><span data-stu-id="e35cf-173">A: Orc, RC, Parquet, and flat delimited text</span></span>

<span data-ttu-id="e35cf-174">D: A cosa è possibile collegarsi da SQL Data Warehouse usando PolyBase?</span><span class="sxs-lookup"><span data-stu-id="e35cf-174">Q: What can I connect to from SQL DW using PolyBase?</span></span> 

<span data-ttu-id="e35cf-175">R: [Azure Data Lake Store] e [BLOB del servizio di archiviazione di Azure]</span><span class="sxs-lookup"><span data-stu-id="e35cf-175">A: [Azure Data Lake Store] and [Azure Storage Blobs]</span></span>

<span data-ttu-id="e35cf-176">D: È possibile impostare il calcolo per la connessione al BLOB del servizio di archiviazione di Azure o ad ADLS?</span><span class="sxs-lookup"><span data-stu-id="e35cf-176">Q: Is computation pushdown possible  when connecting to Azure Storage Blobs or ADLS?</span></span> 

<span data-ttu-id="e35cf-177">R: No, PolyBase di SQL DW interagisce solo con i componenti di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e35cf-177">A: No, SQL DW PolyBase only interacts the storage components.</span></span> 

<span data-ttu-id="e35cf-178">D: È possibile connettersi ad HDI?</span><span class="sxs-lookup"><span data-stu-id="e35cf-178">Q: Can I connect to HDI?</span></span>

<span data-ttu-id="e35cf-179">R: HDI può usare ADLS o WASB come livello HDFS.</span><span class="sxs-lookup"><span data-stu-id="e35cf-179">A: HDI can use either ADLS or WASB as the HDFS layer.</span></span> <span data-ttu-id="e35cf-180">Se si dispone di un livello HDFS, è possibile caricare i dati in SQL DW.</span><span class="sxs-lookup"><span data-stu-id="e35cf-180">If you have either as your HDFS layer, then you can load that data into SQL DW.</span></span> <span data-ttu-id="e35cf-181">Tuttavia, non è possibile generare il calcolo di distribuzione per l'istanza HDI.</span><span class="sxs-lookup"><span data-stu-id="e35cf-181">However, you cannot generate pushdown computation to the HDI instance.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e35cf-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e35cf-182">Next steps</span></span>
<span data-ttu-id="e35cf-183">Per altre informazioni su SQL Data Warehouse nel complesso, vedere la pagina [Panoramica].</span><span class="sxs-lookup"><span data-stu-id="e35cf-183">For more information on SQL Data Warehouse as a whole, see our [Overview] page.</span></span>


<!-- Article references -->
<span data-ttu-id="e35cf-184">[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse</span><span class="sxs-lookup"><span data-stu-id="e35cf-184">[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse</span></span>
<span data-ttu-id="e35cf-185">[stringhe di connessione]: ./sql-data-warehouse-connection-strings.md</span><span class="sxs-lookup"><span data-stu-id="e35cf-185">[Connection Strings]: ./sql-data-warehouse-connection-strings.md</span></span>
<span data-ttu-id="e35cf-186">[Overflow dello stack]: http://stackoverflow.com/questions/tagged/azure-sqldw</span><span class="sxs-lookup"><span data-stu-id="e35cf-186">[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw</span></span>
<span data-ttu-id="e35cf-187">[I ticket di supporto]: ./sql-data-warehouse-get-started-create-support-ticket.md</span><span class="sxs-lookup"><span data-stu-id="e35cf-187">[Support Tickets]: ./sql-data-warehouse-get-started-create-support-ticket.md</span></span>
<span data-ttu-id="e35cf-188">[Sicurezza]: ./sql-data-warehouse-overview-manage-security.md</span><span class="sxs-lookup"><span data-stu-id="e35cf-188">[Security]: ./sql-data-warehouse-overview-manage-security.md</span></span>
<span data-ttu-id="e35cf-189">[Conformità di Microsoft]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings</span><span class="sxs-lookup"><span data-stu-id="e35cf-189">[Microsoft Compliance]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings</span></span>
<span data-ttu-id="e35cf-190">[limiti di capacità]: ./sql-data-warehouse-service-capacity-limits.md</span><span class="sxs-lookup"><span data-stu-id="e35cf-190">[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md</span></span>
<span data-ttu-id="e35cf-191">[tipi di dati]: ./sql-data-warehouse-tables-data-types.md</span><span class="sxs-lookup"><span data-stu-id="e35cf-191">[data types]: ./sql-data-warehouse-tables-data-types.md</span></span>
<span data-ttu-id="e35cf-192">[Funzionalità non supportate delle tabelle]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features</span><span class="sxs-lookup"><span data-stu-id="e35cf-192">[Unsupported Table Features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features</span></span>
<span data-ttu-id="e35cf-193">[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md</span><span class="sxs-lookup"><span data-stu-id="e35cf-193">[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md</span></span>
<span data-ttu-id="e35cf-194">[BLOB del servizio di archiviazione di Azure]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md</span><span class="sxs-lookup"><span data-stu-id="e35cf-194">[Azure Storage Blobs]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md</span></span>
<span data-ttu-id="e35cf-195">[richiesta di funzionalità per progetti di Database]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu</span><span class="sxs-lookup"><span data-stu-id="e35cf-195">[Database projects feature request]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu</span></span>
<span data-ttu-id="e35cf-196">[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx</span><span class="sxs-lookup"><span data-stu-id="e35cf-196">[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx</span></span>
<span data-ttu-id="e35cf-197">[Panoramica]: ./sql-data-warehouse-overview-faq.md</span><span class="sxs-lookup"><span data-stu-id="e35cf-197">[Overview]: ./sql-data-warehouse-overview-faq.md</span></span>