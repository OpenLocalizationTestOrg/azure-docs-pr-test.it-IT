---
title: aaaAzure SQL Data Warehouse domande frequenti | Documenti Microsoft
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
ms.openlocfilehash: 09fd3f65d9507b09fcb8f477742c7d020add2755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a><span data-ttu-id="3ccb4-103">Domande frequenti su SQL Data Warehouse di Azure</span><span class="sxs-lookup"><span data-stu-id="3ccb4-103">SQL Data Warehouse Frequently asked questions</span></span>

## <a name="general"></a><span data-ttu-id="3ccb4-104">Generale</span><span class="sxs-lookup"><span data-stu-id="3ccb4-104">General</span></span>

<span data-ttu-id="3ccb4-105">D:</span><span class="sxs-lookup"><span data-stu-id="3ccb4-105">Q.</span></span> <span data-ttu-id="3ccb4-106">Cosa offre SQL DW per la protezione dei dati?</span><span class="sxs-lookup"><span data-stu-id="3ccb4-106">What does SQL DW offer for data security?</span></span>

<span data-ttu-id="3ccb4-107">R.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-107">A.</span></span> <span data-ttu-id="3ccb4-108">SQL DW offre diverse soluzioni per la protezione dei dati, ad esempio TDE e il controllo.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-108">SQL DW offers several solutions for protecting data such as TDE and auditing.</span></span> <span data-ttu-id="3ccb4-109">Per altre informazioni, vedere [Sicurezza].</span><span class="sxs-lookup"><span data-stu-id="3ccb4-109">For more information, see [Security].</span></span>

<span data-ttu-id="3ccb4-110">D:</span><span class="sxs-lookup"><span data-stu-id="3ccb4-110">Q.</span></span> <span data-ttu-id="3ccb4-111">Dove è possibile trovare gli standard legali o aziendali a cui SQL DW è conforme?</span><span class="sxs-lookup"><span data-stu-id="3ccb4-111">Where can I find out what legal or business standards is SQL DW compliant with?</span></span>

<span data-ttu-id="3ccb4-112">R.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-112">A.</span></span> <span data-ttu-id="3ccb4-113">Visitare hello [Microsoft Compliance] pagina per diverse offerte di conformità per prodotto, ad esempio SOC e ISO.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-113">Visit hello [Microsoft Compliance] page for various compliance offerings by product such as SOC and ISO.</span></span> <span data-ttu-id="3ccb4-114">Prima di selezionare il titolo di conformità, quindi espandere Azure hello Microsoft nell'ambito cloud services sezione sul lato destro hello di hello pagina toosee quali servizi sono servizi di Azure è compatibili.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-114">First choose by Compliance title, then expand Azure in hello Microsoft in-scope cloud services section on hello right side of hello page toosee what services are Azure services are compliant.</span></span>

<span data-ttu-id="3ccb4-115">D:</span><span class="sxs-lookup"><span data-stu-id="3ccb4-115">Q.</span></span> <span data-ttu-id="3ccb4-116">È possibile connettersi a PowerBI?</span><span class="sxs-lookup"><span data-stu-id="3ccb4-116">Can I connect PowerBI?</span></span>

<span data-ttu-id="3ccb4-117">R.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-117">A.</span></span> <span data-ttu-id="3ccb4-118">È possibile usarlo.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-118">Yes!</span></span> <span data-ttu-id="3ccb4-119">Anche se PowerBI supporta la query diretta con SQL DW, non è pensato per un numero elevato di utenti o di dati in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-119">Though PowerBI supports direct query with SQL DW, it’s not intended for large number of users or real-time data.</span></span> <span data-ttu-id="3ccb4-120">Per l'uso della produzione di PowerBI, è consigliabile usare PowerBI su Azure Analysis Services o IaaS di Analysis Service.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-120">For production use of PowerBI, we recommend using PowerBI on top of Azure Analysis Services or Analysis Service IaaS.</span></span> 

<span data-ttu-id="3ccb4-121">D:</span><span class="sxs-lookup"><span data-stu-id="3ccb4-121">Q.</span></span> <span data-ttu-id="3ccb4-122">Quali sono i limiti di capacità di SQL Data Warehouse?</span><span class="sxs-lookup"><span data-stu-id="3ccb4-122">What are SQL Data Warehouse Capacity Limits?</span></span>

<span data-ttu-id="3ccb4-123">R.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-123">A.</span></span> <span data-ttu-id="3ccb4-124">Vedere la pagina relativa ai [limiti di capacità] correnti.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-124">See our current [capacity limits] page.</span></span> 

<span data-ttu-id="3ccb4-125">D:</span><span class="sxs-lookup"><span data-stu-id="3ccb4-125">Q.</span></span> <span data-ttu-id="3ccb4-126">Perché le operazioni di ridimensionamento, sospensione o ripresa richiedono così tanto tempo?</span><span class="sxs-lookup"><span data-stu-id="3ccb4-126">Why is my Scale/Pause/Resume taking so long?</span></span>

<span data-ttu-id="3ccb4-127">R.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-127">A.</span></span> <span data-ttu-id="3ccb4-128">Una serie di fattori può influenzare il tempo di hello per le operazioni di gestione di calcolo.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-128">A variety of factors can influence hello time for compute management operations.</span></span> <span data-ttu-id="3ccb4-129">Un caso che si verifica spesso nelle operazioni a esecuzione prolungata è il rollback transazionali.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-129">A common case for  long running operations is transactional rollback.</span></span> <span data-ttu-id="3ccb4-130">Quando viene avviata un'operazione di sospensione o di ridimensionamento, vengono bloccate tutte le sessioni in ingresso e le query vengono svuotate.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-130">When a scale or pause operation is initiated, all incoming sessions are blocked and queries are drained.</span></span> <span data-ttu-id="3ccb4-131">Nel sistema ordini tooleave hello in uno stato stabile, rollback delle transazioni devono essere eseguito prima che inizi un'operazione.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-131">In order tooleave hello system in a stable state, transactions must be rolled back before an operation can commence.</span></span> <span data-ttu-id="3ccb4-132">salve maggiore numero hello e dimensioni hello log delle transazioni, operazione hello più hello verrà bloccato il ripristino dello stato di hello sistema tooa stabile.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-132">hello greater hello number and larger hello log size of transactions, hello longer hello operation will be stalled restoring hello system tooa stable state.</span></span>

## <a name="user-support"></a><span data-ttu-id="3ccb4-133">Supporto per l'utente</span><span class="sxs-lookup"><span data-stu-id="3ccb4-133">User support</span></span>

<span data-ttu-id="3ccb4-134">D:</span><span class="sxs-lookup"><span data-stu-id="3ccb4-134">Q.</span></span> <span data-ttu-id="3ccb4-135">Ho una richiesta di funzionalità, dove posso inviarla?</span><span class="sxs-lookup"><span data-stu-id="3ccb4-135">I have a feature request, where do I submit it?</span></span>

<span data-ttu-id="3ccb4-136">R.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-136">A.</span></span> <span data-ttu-id="3ccb4-137">Se si dispone di una richiesta di funzionalità, inviarla alla pagina [UserVoice]</span><span class="sxs-lookup"><span data-stu-id="3ccb4-137">If you have a feature request, submit it on our [UserVoice] page</span></span>

<span data-ttu-id="3ccb4-138">D:</span><span class="sxs-lookup"><span data-stu-id="3ccb4-138">Q.</span></span> <span data-ttu-id="3ccb4-139">Come posso fare?</span><span class="sxs-lookup"><span data-stu-id="3ccb4-139">How can I do x?</span></span>

<span data-ttu-id="3ccb4-140">R.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-140">A.</span></span> <span data-ttu-id="3ccb4-141">Per assistenza nello sviluppo con SQL Data Warehouse, è possibile porre domande alla pagina [Overflow dello stack].</span><span class="sxs-lookup"><span data-stu-id="3ccb4-141">For help in developing with SQL Data Warehouse, you can ask questions on our [Stack Overflow] page.</span></span> 

<span data-ttu-id="3ccb4-142">D:</span><span class="sxs-lookup"><span data-stu-id="3ccb4-142">Q.</span></span> <span data-ttu-id="3ccb4-143">Come posso inviare un ticket di supporto?</span><span class="sxs-lookup"><span data-stu-id="3ccb4-143">How do I submit a support ticket?</span></span>

<span data-ttu-id="3ccb4-144">R.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-144">A.</span></span> <span data-ttu-id="3ccb4-145">[I ticket di supporto] possono essere inviati tramite il Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-145">[Support Tickets] can be filed through Azure portal.</span></span>

## <a name="sql-languagefeature-support"></a><span data-ttu-id="3ccb4-146">Supporto per le funzionalità/linguaggio SQL</span><span class="sxs-lookup"><span data-stu-id="3ccb4-146">SQL language/feature support</span></span> 

<span data-ttu-id="3ccb4-147">D:</span><span class="sxs-lookup"><span data-stu-id="3ccb4-147">Q.</span></span> <span data-ttu-id="3ccb4-148">Quali tipi di dati sono supportati da SQL Data Warehouse?</span><span class="sxs-lookup"><span data-stu-id="3ccb4-148">What datatypes does SQL Data Warehouse support?</span></span>

<span data-ttu-id="3ccb4-149">R.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-149">A.</span></span> <span data-ttu-id="3ccb4-150">Vedere i [tipi di dati] di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-150">See SQL Data Warehouse [data types].</span></span>

<span data-ttu-id="3ccb4-151">D:</span><span class="sxs-lookup"><span data-stu-id="3ccb4-151">Q.</span></span> <span data-ttu-id="3ccb4-152">Quali funzionalità delle tabelle sono supportate?</span><span class="sxs-lookup"><span data-stu-id="3ccb4-152">What table features do you support?</span></span>

<span data-ttu-id="3ccb4-153">R.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-153">A.</span></span> <span data-ttu-id="3ccb4-154">Sebbene SQL Data Warehouse supporti molte funzionalità, alcune non sono supportate. Queste sono documentate in [Funzionalità non supportate delle tabelle].</span><span class="sxs-lookup"><span data-stu-id="3ccb4-154">While SQL Data Warehouse supports many features, some are not supported and are documented in [Unsupported Table Features].</span></span>

## <a name="tooling-and-administration"></a><span data-ttu-id="3ccb4-155">Strumenti e amministrazione</span><span class="sxs-lookup"><span data-stu-id="3ccb4-155">Tooling and administration</span></span>

<span data-ttu-id="3ccb4-156">D:</span><span class="sxs-lookup"><span data-stu-id="3ccb4-156">Q.</span></span> <span data-ttu-id="3ccb4-157">I progetti di Database sono supportati in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-157">Do you support Database projects in Visual Studio.</span></span>

<span data-ttu-id="3ccb4-158">R.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-158">A.</span></span> <span data-ttu-id="3ccb4-159">Attualmente i progetti di Database non sono supportati in Visual Studio per SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-159">We currently do not support Database projects in Visual Studio for SQL Data Warehouse.</span></span> <span data-ttu-id="3ccb4-160">Se si desidera toocast tooget un voto tale funzionalità, visitare il nostro vocale utente [progetti di Database di funzionalità richiesta].</span><span class="sxs-lookup"><span data-stu-id="3ccb4-160">If you'd like toocast a vote tooget this feature, visit our User Voice [Database projects feature request].</span></span>

<span data-ttu-id="3ccb4-161">D:</span><span class="sxs-lookup"><span data-stu-id="3ccb4-161">Q.</span></span> <span data-ttu-id="3ccb4-162">SQL Data Warehouse supporta le API REST?</span><span class="sxs-lookup"><span data-stu-id="3ccb4-162">Does SQL Data Warehouse support REST APIs?</span></span>

<span data-ttu-id="3ccb4-163">R.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-163">A.</span></span> <span data-ttu-id="3ccb4-164">Sì.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-164">Yes.</span></span> <span data-ttu-id="3ccb4-165">La maggior parte delle funzionalità REST che può essere usata con il Database SQL è disponibile anche con SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-165">Most REST functionality that can be used with SQL Database is also available with SQL Data Warehouse.</span></span> <span data-ttu-id="3ccb4-166">È possibile trovare informazioni sulle API nelle pagine di documentazione REST o in [MSDN].</span><span class="sxs-lookup"><span data-stu-id="3ccb4-166">You can find API information within REST documentation pages or [MSDN].</span></span>


## <a name="loading"></a><span data-ttu-id="3ccb4-167">Caricamento</span><span class="sxs-lookup"><span data-stu-id="3ccb4-167">Loading</span></span>

<span data-ttu-id="3ccb4-168">D:</span><span class="sxs-lookup"><span data-stu-id="3ccb4-168">Q.</span></span> <span data-ttu-id="3ccb4-169">Quali driver client sono supportati?</span><span class="sxs-lookup"><span data-stu-id="3ccb4-169">What client drivers do you support?</span></span>

<span data-ttu-id="3ccb4-170">R.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-170">A.</span></span> <span data-ttu-id="3ccb4-171">Supporto di driver per data Warehouse può trovarsi in hello [le stringhe di connessione] pagina</span><span class="sxs-lookup"><span data-stu-id="3ccb4-171">Driver support for DW can be found on hello [Connection Strings] page</span></span>

<span data-ttu-id="3ccb4-172">D: Quali formati di file sono supportati da PolyBase con SQL Data Warehouse?</span><span class="sxs-lookup"><span data-stu-id="3ccb4-172">Q: What file formats are supported by PolyBase with SQL Data Warehouse?</span></span>

<span data-ttu-id="3ccb4-173">R: Orc, RC, Parquet e testo delimitato semplice</span><span class="sxs-lookup"><span data-stu-id="3ccb4-173">A: Orc, RC, Parquet, and flat delimited text</span></span>

<span data-ttu-id="3ccb4-174">D: cosa è possibile connettersi usando PolyBase toofrom SQL DW?</span><span class="sxs-lookup"><span data-stu-id="3ccb4-174">Q: What can I connect toofrom SQL DW using PolyBase?</span></span> 

<span data-ttu-id="3ccb4-175">R: [Azure Data Lake Store] e [BLOB del servizio di archiviazione di Azure]</span><span class="sxs-lookup"><span data-stu-id="3ccb4-175">A: [Azure Data Lake Store] and [Azure Storage Blobs]</span></span>

<span data-ttu-id="3ccb4-176">D: è possibile la distribuzione del calcolo quando ci si connette tooAzure BLOB di archiviazione o ADLS?</span><span class="sxs-lookup"><span data-stu-id="3ccb4-176">Q: Is computation pushdown possible  when connecting tooAzure Storage Blobs or ADLS?</span></span> 

<span data-ttu-id="3ccb4-177">R: no, SQL Data Warehouse PolyBase interagisce solo i componenti di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-177">A: No, SQL DW PolyBase only interacts hello storage components.</span></span> 

<span data-ttu-id="3ccb4-178">D: è possibile connettere tooHDI?</span><span class="sxs-lookup"><span data-stu-id="3ccb4-178">Q: Can I connect tooHDI?</span></span>

<span data-ttu-id="3ccb4-179">R: HDI è possibile utilizzare ADLS o WASB come livello HDFS hello.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-179">A: HDI can use either ADLS or WASB as hello HDFS layer.</span></span> <span data-ttu-id="3ccb4-180">Se si dispone di un livello HDFS, è possibile caricare i dati in SQL DW.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-180">If you have either as your HDFS layer, then you can load that data into SQL DW.</span></span> <span data-ttu-id="3ccb4-181">Tuttavia, è possibile generare istanza HDI toohello calcolo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-181">However, you cannot generate pushdown computation toohello HDI instance.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3ccb4-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3ccb4-182">Next steps</span></span>
<span data-ttu-id="3ccb4-183">Per altre informazioni su SQL Data Warehouse nel complesso, vedere la pagina [Panoramica].</span><span class="sxs-lookup"><span data-stu-id="3ccb4-183">For more information on SQL Data Warehouse as a whole, see our [Overview] page.</span></span>


<!-- Article references -->
[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[le stringhe di connessione]: ./sql-data-warehouse-connection-strings.md
[Overflow dello stack]: http://stackoverflow.com/questions/tagged/azure-sqldw
[I ticket di supporto]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Sicurezza]: ./sql-data-warehouse-overview-manage-security.md
[Microsoft Compliance]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings
[limiti di capacità]: ./sql-data-warehouse-service-capacity-limits.md
[tipi di dati]: ./sql-data-warehouse-tables-data-types.md
[Funzionalità non supportate delle tabelle]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md
[BLOB del servizio di archiviazione di Azure]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[progetti di Database di funzionalità richiesta]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu
[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx
[Panoramica]: ./sql-data-warehouse-overview-faq.md