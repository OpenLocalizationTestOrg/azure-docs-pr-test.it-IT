---
title: Usare i contatori delle prestazioni in Diagnostica di Azure Diagnostics | Documentazione Microsoft
description: Usare i contatori delle prestazioni nei servizi cloud o nelle macchine virtuali di Azure per trovare i colli di bottiglia e ottimizzare le prestazioni.
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: fc4c61e9-d49d-4ed9-a32c-b91cdf851909
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/29/2016
ms.author: robb
ms.openlocfilehash: 2cf765cb034725199127c547a9b8b997a4a6089c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a><span data-ttu-id="57f79-103">Creare e usare contatori di prestazioni in un'applicazione Azure</span><span class="sxs-lookup"><span data-stu-id="57f79-103">Create and use performance counters in an Azure application</span></span>
<span data-ttu-id="57f79-104">Questo articolo descrive i vantaggi dei contatori delle prestazioni e come inserirli nell'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="57f79-104">This article describes the benefits of and how to put performance counters into your Azure application.</span></span> <span data-ttu-id="57f79-105">È possibile usarli per raccogliere dati, trovare colli di bottiglia e ottimizzare le prestazioni del sistema e dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="57f79-105">You can use them to collect data, find bottlenecks, and tune system and application performance.</span></span>

<span data-ttu-id="57f79-106">I contatori delle prestazioni disponibili per Windows Server, IIS e ASP.NET possono essere raccolti e usati anche per determinare l'integrità di ruoli Web, ruoli di lavoro e macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="57f79-106">Performance counters available for Windows Server, IIS, and ASP.NET can also be collected and used to determine the health of your Azure web roles, worker roles, and Virtual Machines.</span></span> <span data-ttu-id="57f79-107">È anche possibile creare e usare contatori delle prestazioni personalizzati.</span><span class="sxs-lookup"><span data-stu-id="57f79-107">You can also create and use custom performance counters.</span></span>  

<span data-ttu-id="57f79-108">È possibile esaminare i dati dei contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="57f79-108">You can examine performance counter data</span></span>

1. <span data-ttu-id="57f79-109">Direttamente nell'host applicazione con lo strumento Performance Monitor accessibile da Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="57f79-109">Directly on the application host with the Performance Monitor tool accessed using Remote Desktop</span></span>
2. <span data-ttu-id="57f79-110">Con System Center Operations Manager con Azure Management Pack</span><span class="sxs-lookup"><span data-stu-id="57f79-110">With System Center Operations Manager using the Azure Management Pack</span></span>
3. <span data-ttu-id="57f79-111">Con altri strumenti di monitoraggio che accedono ai dati di diagnostica trasferiti ad Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="57f79-111">With other monitoring tools that access the diagnostic data transferred to Azure storage.</span></span> <span data-ttu-id="57f79-112">Per altre informazioni, vedere [Archiviare e visualizzare i dati di diagnostica nell'account di archiviazione Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx) .</span><span class="sxs-lookup"><span data-stu-id="57f79-112">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for more information.</span></span>  

<span data-ttu-id="57f79-113">Per altre informazioni sul monitoraggio delle prestazioni dell'applicazione nel [portale di Azure](http://portal.azure.com/), vedere [Come monitorare i servizi cloud](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span><span class="sxs-lookup"><span data-stu-id="57f79-113">For more information on monitoring the performance of your application in the [Azure portal](http://portal.azure.com/), see [How to Monitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span></span>

<span data-ttu-id="57f79-114">Per ulteriori indicazioni dettagliate sulla creazione di una strategia di registrazione e traccia e sull'utilizzo della diagnostica e di altre tecniche per risolvere i problemi e ottimizzare le applicazioni Azure, vedere le [procedure consigliate di risoluzione dei problemi per lo sviluppo di applicazioni Azure](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="57f79-114">For additional in-depth guidance on creating a logging and tracing strategy and using diagnostics and other techniques to troubleshoot problems and optimize Azure applications, see [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span></span>

## <a name="enable-performance-counter-monitoring"></a><span data-ttu-id="57f79-115">Abilitare il monitoraggio del contatore delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="57f79-115">Enable performance counter monitoring</span></span>
<span data-ttu-id="57f79-116">Per impostazione predefinita, i contatori delle prestazioni non sono abilitati.</span><span class="sxs-lookup"><span data-stu-id="57f79-116">Performance counters are not enabled by default.</span></span> <span data-ttu-id="57f79-117">L'applicazione o un'attività di avvio deve modificare la configurazione predefinita dell'agente di diagnostica in modo che includa i contatori delle prestazioni specifici da monitorare per ogni istanza del ruolo.</span><span class="sxs-lookup"><span data-stu-id="57f79-117">Your application or a startup task must modify the default diagnostics agent configuration to include the specific performance counters that you wish to monitor for each role instance.</span></span>

### <a name="performance-counters-available-for-microsoft-azure"></a><span data-ttu-id="57f79-118">Contatori delle prestazioni disponibili per Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="57f79-118">Performance counters available for Microsoft Azure</span></span>
<span data-ttu-id="57f79-119">Azure fornisce un subset dei contatori delle prestazioni disponibili per Windows Server, IIS e lo stack ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="57f79-119">Azure provides a subset of the performance counters available for Windows Server, IIS and the ASP.NET stack.</span></span> <span data-ttu-id="57f79-120">La tabella seguente elenca alcuni contatori delle prestazioni particolarmente interessanti per le applicazioni Azure.</span><span class="sxs-lookup"><span data-stu-id="57f79-120">The following table lists some of the performance counters of particular interest for Azure applications.</span></span>

| <span data-ttu-id="57f79-121">Categoria contatore: oggetto (istanza)</span><span class="sxs-lookup"><span data-stu-id="57f79-121">Counter Category: Object (Instance)</span></span> | <span data-ttu-id="57f79-122">Nome contatore</span><span class="sxs-lookup"><span data-stu-id="57f79-122">Counter Name</span></span> | <span data-ttu-id="57f79-123">Riferimento</span><span class="sxs-lookup"><span data-stu-id="57f79-123">Reference</span></span> |
| --- | --- | --- |
| <span data-ttu-id="57f79-124">Eccezioni CLR .NET (*globale*)</span><span class="sxs-lookup"><span data-stu-id="57f79-124">.NET CLR Exceptions(*Global*)</span></span> |<span data-ttu-id="57f79-125">N. eccezioni/sec</span><span class="sxs-lookup"><span data-stu-id="57f79-125"># Exceps Thrown / sec</span></span> |<span data-ttu-id="57f79-126">Contatori delle prestazioni delle eccezioni</span><span class="sxs-lookup"><span data-stu-id="57f79-126">Exception Performance Counters</span></span> |
| <span data-ttu-id="57f79-127">Memoria CLR .NET (*globale*)</span><span class="sxs-lookup"><span data-stu-id="57f79-127">.NET CLR Memory(*Global*)</span></span> |<span data-ttu-id="57f79-128">Percentuale tempo in GC</span><span class="sxs-lookup"><span data-stu-id="57f79-128">% Time in GC</span></span> |<span data-ttu-id="57f79-129">Contatori delle prestazioni di memoria</span><span class="sxs-lookup"><span data-stu-id="57f79-129">Memory Performance Counters</span></span> |
| <span data-ttu-id="57f79-130">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="57f79-130">ASP.NET</span></span> |<span data-ttu-id="57f79-131">Riavvii applicazione</span><span class="sxs-lookup"><span data-stu-id="57f79-131">Application Restarts</span></span> |<span data-ttu-id="57f79-132">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="57f79-132">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="57f79-133">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="57f79-133">ASP.NET</span></span> |<span data-ttu-id="57f79-134">Tempo di esecuzione della richiesta</span><span class="sxs-lookup"><span data-stu-id="57f79-134">Request Execution Time</span></span> |<span data-ttu-id="57f79-135">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="57f79-135">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="57f79-136">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="57f79-136">ASP.NET</span></span> |<span data-ttu-id="57f79-137">Richieste disconnesse</span><span class="sxs-lookup"><span data-stu-id="57f79-137">Requests Disconnected</span></span> |<span data-ttu-id="57f79-138">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="57f79-138">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="57f79-139">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="57f79-139">ASP.NET</span></span> |<span data-ttu-id="57f79-140">Riavvii processo di lavoro</span><span class="sxs-lookup"><span data-stu-id="57f79-140">Worker Process Restarts</span></span> |<span data-ttu-id="57f79-141">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="57f79-141">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="57f79-142">Applicazioni ASP.NET (**totale**)</span><span class="sxs-lookup"><span data-stu-id="57f79-142">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="57f79-143">Totale richieste</span><span class="sxs-lookup"><span data-stu-id="57f79-143">Requests Total</span></span> |<span data-ttu-id="57f79-144">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="57f79-144">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="57f79-145">Applicazioni ASP.NET (**totale**)</span><span class="sxs-lookup"><span data-stu-id="57f79-145">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="57f79-146">Richieste/sec</span><span class="sxs-lookup"><span data-stu-id="57f79-146">Requests/Sec</span></span> |<span data-ttu-id="57f79-147">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="57f79-147">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="57f79-148">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="57f79-148">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="57f79-149">Tempo di esecuzione della richiesta</span><span class="sxs-lookup"><span data-stu-id="57f79-149">Request Execution Time</span></span> |<span data-ttu-id="57f79-150">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="57f79-150">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="57f79-151">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="57f79-151">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="57f79-152">Tempo di attesa richiesta</span><span class="sxs-lookup"><span data-stu-id="57f79-152">Request Wait Time</span></span> |<span data-ttu-id="57f79-153">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="57f79-153">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="57f79-154">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="57f79-154">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="57f79-155">Richieste correnti</span><span class="sxs-lookup"><span data-stu-id="57f79-155">Requests Current</span></span> |<span data-ttu-id="57f79-156">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="57f79-156">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="57f79-157">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="57f79-157">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="57f79-158">Richieste in coda</span><span class="sxs-lookup"><span data-stu-id="57f79-158">Requests Queued</span></span> |<span data-ttu-id="57f79-159">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="57f79-159">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="57f79-160">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="57f79-160">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="57f79-161">Richieste respinte</span><span class="sxs-lookup"><span data-stu-id="57f79-161">Requests Rejected</span></span> |<span data-ttu-id="57f79-162">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="57f79-162">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="57f79-163">Memoria</span><span class="sxs-lookup"><span data-stu-id="57f79-163">Memory</span></span> |<span data-ttu-id="57f79-164">MByte disponibili</span><span class="sxs-lookup"><span data-stu-id="57f79-164">Available MBytes</span></span> |<span data-ttu-id="57f79-165">Contatori delle prestazioni di memoria</span><span class="sxs-lookup"><span data-stu-id="57f79-165">Memory Performance Counters</span></span> |
| <span data-ttu-id="57f79-166">Memoria</span><span class="sxs-lookup"><span data-stu-id="57f79-166">Memory</span></span> |<span data-ttu-id="57f79-167">Byte vincolati</span><span class="sxs-lookup"><span data-stu-id="57f79-167">Committed Bytes</span></span> |<span data-ttu-id="57f79-168">Contatori delle prestazioni di memoria</span><span class="sxs-lookup"><span data-stu-id="57f79-168">Memory Performance Counters</span></span> |
| <span data-ttu-id="57f79-169">Processor(_Total)</span><span class="sxs-lookup"><span data-stu-id="57f79-169">Processor(_Total)</span></span> |<span data-ttu-id="57f79-170">% di tempo processore</span><span class="sxs-lookup"><span data-stu-id="57f79-170">% Processor Time</span></span> |<span data-ttu-id="57f79-171">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="57f79-171">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="57f79-172">TCPv4</span><span class="sxs-lookup"><span data-stu-id="57f79-172">TCPv4</span></span> |<span data-ttu-id="57f79-173">Errori di connessione</span><span class="sxs-lookup"><span data-stu-id="57f79-173">Connection Failures</span></span> |<span data-ttu-id="57f79-174">Oggetto TCP</span><span class="sxs-lookup"><span data-stu-id="57f79-174">TCP Object</span></span> |
| <span data-ttu-id="57f79-175">TCPv4</span><span class="sxs-lookup"><span data-stu-id="57f79-175">TCPv4</span></span> |<span data-ttu-id="57f79-176">Connessioni stabilite</span><span class="sxs-lookup"><span data-stu-id="57f79-176">Connections Established</span></span> |<span data-ttu-id="57f79-177">Oggetto TCP</span><span class="sxs-lookup"><span data-stu-id="57f79-177">TCP Object</span></span> |
| <span data-ttu-id="57f79-178">TCPv4</span><span class="sxs-lookup"><span data-stu-id="57f79-178">TCPv4</span></span> |<span data-ttu-id="57f79-179">Connessioni ripristinate</span><span class="sxs-lookup"><span data-stu-id="57f79-179">Connections Reset</span></span> |<span data-ttu-id="57f79-180">Oggetto TCP</span><span class="sxs-lookup"><span data-stu-id="57f79-180">TCP Object</span></span> |
| <span data-ttu-id="57f79-181">TCPv4</span><span class="sxs-lookup"><span data-stu-id="57f79-181">TCPv4</span></span> |<span data-ttu-id="57f79-182">Segmenti inviati/sec</span><span class="sxs-lookup"><span data-stu-id="57f79-182">Segments Sent/sec</span></span> |<span data-ttu-id="57f79-183">Oggetto TCP</span><span class="sxs-lookup"><span data-stu-id="57f79-183">TCP Object</span></span> |
| <span data-ttu-id="57f79-184">Interfaccia di rete (*)</span><span class="sxs-lookup"><span data-stu-id="57f79-184">Network Interface(*)</span></span> |<span data-ttu-id="57f79-185">Byte ricevuti/sec</span><span class="sxs-lookup"><span data-stu-id="57f79-185">Bytes Received/sec</span></span> |<span data-ttu-id="57f79-186">Oggetto interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="57f79-186">Network Interface Object</span></span> |
| <span data-ttu-id="57f79-187">Interfaccia di rete (*)</span><span class="sxs-lookup"><span data-stu-id="57f79-187">Network Interface(*)</span></span> |<span data-ttu-id="57f79-188">Byte inviati/sec</span><span class="sxs-lookup"><span data-stu-id="57f79-188">Bytes Sent/sec</span></span> |<span data-ttu-id="57f79-189">Oggetto interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="57f79-189">Network Interface Object</span></span> |
| <span data-ttu-id="57f79-190">Interfaccia di rete (Scheda di rete per il bus delle macchine virtuali Microsoft _2)</span><span class="sxs-lookup"><span data-stu-id="57f79-190">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="57f79-191">Byte ricevuti/sec</span><span class="sxs-lookup"><span data-stu-id="57f79-191">Bytes Received/sec</span></span> |<span data-ttu-id="57f79-192">Oggetto interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="57f79-192">Network Interface Object</span></span> |
| <span data-ttu-id="57f79-193">Interfaccia di rete (Scheda di rete per il bus delle macchine virtuali Microsoft _2)</span><span class="sxs-lookup"><span data-stu-id="57f79-193">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="57f79-194">Byte inviati/sec</span><span class="sxs-lookup"><span data-stu-id="57f79-194">Bytes Sent/sec</span></span> |<span data-ttu-id="57f79-195">Oggetto interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="57f79-195">Network Interface Object</span></span> |
| <span data-ttu-id="57f79-196">Interfaccia di rete (Scheda di rete per il bus delle macchine virtuali Microsoft _2)</span><span class="sxs-lookup"><span data-stu-id="57f79-196">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="57f79-197">Totale byte/sec</span><span class="sxs-lookup"><span data-stu-id="57f79-197">Bytes Total/sec</span></span> |<span data-ttu-id="57f79-198">Oggetto interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="57f79-198">Network Interface Object</span></span> |

## <a name="create-and-add-custom-performance-counters-to-your-application"></a><span data-ttu-id="57f79-199">Creare e aggiungere contatori delle prestazioni personalizzati all'applicazione</span><span class="sxs-lookup"><span data-stu-id="57f79-199">Create and add custom performance counters to your application</span></span>
<span data-ttu-id="57f79-200">Azure include il supporto per creare e modificare contatori delle prestazioni personalizzati per ruoli Web e ruoli di lavoro.</span><span class="sxs-lookup"><span data-stu-id="57f79-200">Azure has support to create and modify custom performance counters for web roles and worker roles.</span></span> <span data-ttu-id="57f79-201">I contatori possono essere usati per tenere traccia del comportamento specifico dell'applicazione e per monitorarlo.</span><span class="sxs-lookup"><span data-stu-id="57f79-201">The counters may be used to track and monitor application-specific behavior.</span></span> <span data-ttu-id="57f79-202">È possibile creare ed eliminare categorie e identificatori dei contatori delle prestazioni personalizzati da un'attività di avvio, un ruolo Web o un ruolo di lavoro con autorizzazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="57f79-202">You can create and delete custom performance counter categories and specifiers from a startup task, web role, or worker role with elevated permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="57f79-203">Il codice che apporta le modifiche ai contatori delle prestazioni personalizzati deve avere autorizzazioni di esecuzione elevate.</span><span class="sxs-lookup"><span data-stu-id="57f79-203">Code that makes changes to custom performance counters must have elevated permissions to run.</span></span> <span data-ttu-id="57f79-204">Se il codice è in un ruolo Web o in un ruolo di lavoro, il ruolo deve includere il tag <Runtime executionContext="elevated" /> nel file ServiceDefinition.csdef per la corretta inizializzazione del ruolo.</span><span class="sxs-lookup"><span data-stu-id="57f79-204">If the code is in a web role or worker role, the role must include the tag <Runtime executionContext="elevated" /> in the ServiceDefinition.csdef file for the role to initialize properly.</span></span>
>
>

<span data-ttu-id="57f79-205">È possibile inviare i dati dei contatori delle prestazioni personalizzati alla risorsa di archiviazione di Azure con l'agente di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="57f79-205">You can send custom performance counter data to Azure storage using the diagnostics agent.</span></span>

<span data-ttu-id="57f79-206">I dati dei contatori delle prestazioni standard vengono generati dai processi di Azure.</span><span class="sxs-lookup"><span data-stu-id="57f79-206">The standard performance counter data is generated by the Azure processes.</span></span> <span data-ttu-id="57f79-207">I dati dei contatori delle prestazioni personalizzati devono essere creati dall'applicazione ruolo Web o ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="57f79-207">Custom performance counter data must be created by your web role or worker role application.</span></span> <span data-ttu-id="57f79-208">Per informazioni sui tipi di dati che possono essere archiviati nei contatori delle prestazioni personalizzati, vedere [Tipi di contatori delle prestazioni](https://msdn.microsoft.com/library/z573042h.aspx) .</span><span class="sxs-lookup"><span data-stu-id="57f79-208">See [Performance Counter Types](https://msdn.microsoft.com/library/z573042h.aspx) for information on the types of data that can be stored in custom performance counters.</span></span> <span data-ttu-id="57f79-209">Per un esempio di creazione e impostazione dei dati dei contatori delle prestazioni personalizzati in un ruolo Web, vedere [Esempio PerformanceCounters](http://code.msdn.microsoft.com/azure/) .</span><span class="sxs-lookup"><span data-stu-id="57f79-209">See [PerformanceCounters Sample](http://code.msdn.microsoft.com/azure/) for an example that creates and sets custom performance counter data in a web role.</span></span>

## <a name="store-and-view-performance-counter-data"></a><span data-ttu-id="57f79-210">Archiviare e visualizzare i dati dei contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="57f79-210">Store and view performance counter data</span></span>
<span data-ttu-id="57f79-211">Azure memorizza nella cache i dati dei contatori delle prestazioni con altre informazioni di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="57f79-211">Azure caches performance counter data with other diagnostic information.</span></span> <span data-ttu-id="57f79-212">Questi dati sono disponibili per il monitoraggio remoto mentre l'istanza del ruolo è in esecuzione con l'accesso desktop remoto per visualizzare strumenti come Performance Monitor.</span><span class="sxs-lookup"><span data-stu-id="57f79-212">This data is available for remote monitoring while the role instance is running using remote desktop access to view tools such as Performance Monitor.</span></span> <span data-ttu-id="57f79-213">Per rendere i dati persistenti al di fuori dell'istanza del ruolo, l'agente di diagnostica deve trasferire i dati nell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="57f79-213">To persist the data outside of the role instance, the diagnostics agent must transfer the data to Azure storage.</span></span> <span data-ttu-id="57f79-214">Il limite di dimensioni dei dati dei contatori delle prestazioni memorizzati nella cache può essere configurato nell'agente di diagnostica oppure come parte di un limite condiviso per tutti i dati di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="57f79-214">The size limit of the cached performance counter data can be configured in the diagnostics agent, or it may be configured to be part of a shared limit for all the diagnostic data.</span></span> <span data-ttu-id="57f79-215">Per altre informazioni sull'impostazione delle dimensioni del buffer, vedere [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) e [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span><span class="sxs-lookup"><span data-stu-id="57f79-215">For more information about setting the buffer size, see [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) and [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span></span> <span data-ttu-id="57f79-216">Per una panoramica della configurazione dell'agente di diagnostica per i trasferire i dati in un account di archiviazione, vedere [Archiviare e visualizzare i dati di diagnostica nell'account di archiviazione Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx)</span><span class="sxs-lookup"><span data-stu-id="57f79-216">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for an overview of setting up the diagnostics agent to transfer data to a storage account.</span></span>

<span data-ttu-id="57f79-217">Ogni istanza dei contatori delle prestazioni configurati viene registrata con una frequenza di campionamento specificata e i dati campionati vengono trasferiti nell'account di archiviazione in base a una richiesta di trasferimento pianificato o a una richiesta di trasferimento su richiesta.</span><span class="sxs-lookup"><span data-stu-id="57f79-217">Each configured performance counter instance is recorded at a specified sampling rate, and the sampled data is transferred to the storage account either by a scheduled transfer request or an on-demand transfer request.</span></span> <span data-ttu-id="57f79-218">I trasferimenti automatici possono essere pianificati con una frequenza di una volta ogni minuto.</span><span class="sxs-lookup"><span data-stu-id="57f79-218">Automatic transfers may be scheduled as often as once per minute.</span></span> <span data-ttu-id="57f79-219">I dati dei contatori delle prestazioni trasferiti dall'agente di diagnostica vengono archiviati in una tabella, WADPerformanceCountersTable, nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="57f79-219">Performance counter data transferred by the diagnostics agent is stored in a table, WADPerformanceCountersTable, in the storage account.</span></span> <span data-ttu-id="57f79-220">Questa tabella è accessibile e può essere sottoposta a query con i metodi API di archiviazione standard di Azure.</span><span class="sxs-lookup"><span data-stu-id="57f79-220">This table may be accessed and queried with standard Azure storage API methods.</span></span> <span data-ttu-id="57f79-221">Per un esempio di query e di visualizzazione dei dati dei contatori delle prestazioni dalla tabella WADPerformanceCountersTable, vedere l' [esempio PerformanceCounters per Microsoft Azure](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) .</span><span class="sxs-lookup"><span data-stu-id="57f79-221">See [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) for an example of querying and displaying performance counter data from the WADPerformanceCountersTable table.</span></span>

> [!NOTE]
> <span data-ttu-id="57f79-222">A seconda della latenza della coda e della frequenza di trasferimento dell'agente di diagnostica, i dati dei contatori delle prestazioni più recenti nell'account di archiviazione potrebbero essere scaduti da alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="57f79-222">Depending on the diagnostics agent transfer frequency and queue latency, the most recent performance counter data in the storage account may be several minutes out of date.</span></span>
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a><span data-ttu-id="57f79-223">Abilitare i contatori delle prestazioni con il file di configurazione della diagnostica</span><span class="sxs-lookup"><span data-stu-id="57f79-223">Enable performance counters using diagnostics configuration file</span></span>
<span data-ttu-id="57f79-224">Usare la procedura seguente per abilitare i contatori delle prestazioni nell'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="57f79-224">Use the following procedure to enable performance counters in your Azure application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57f79-225">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="57f79-225">Prerequisites</span></span>
<span data-ttu-id="57f79-226">Questa sezione presuppone che il monitor di diagnostica sia stato importato nell'applicazione e che il file di configurazione della diagnostica sia stato aggiunto alla soluzione Visual Studio (diagnostics.wadcfg in SDK 2.4 e versioni precedenti o diagnostics.wadcfgx in SDK 2.5 e versioni successive).</span><span class="sxs-lookup"><span data-stu-id="57f79-226">This section assumes that you have imported the Diagnostics monitor into your application and added the diagnostics configuration file to your Visual Studio solution (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above).</span></span> <span data-ttu-id="57f79-227">Per altre informazioni, vedere i passaggi 1 e 2 in [Abilitazione della diagnostica nei servizi cloud e nelle macchine virtuali di Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="57f79-227">See steps 1 and 2 in [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md)) for more information.</span></span>

## <a name="step-1-collect-and-store-data-from-performance-counters"></a><span data-ttu-id="57f79-228">Passaggio 1: Raccogliere e archiviare i dati dei contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="57f79-228">Step 1: Collect and store data from performance counters</span></span>
<span data-ttu-id="57f79-229">Dopo avere aggiunto il file della diagnostica alla soluzione Visual Studio, è possibile configurare la raccolta e l'archiviazione dei dati dei contatori delle prestazioni in un'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="57f79-229">After you have added the diagnostics file to your Visual Studio solution, you can configure the collection and storage of performance counter data in an Azure application.</span></span> <span data-ttu-id="57f79-230">Questa operazione viene eseguita tramite l'aggiunta di contatori delle prestazioni nel file della diagnostica.</span><span class="sxs-lookup"><span data-stu-id="57f79-230">This is done by adding performance counters to the diagnostics file.</span></span> <span data-ttu-id="57f79-231">I dati di diagnostica, inclusi i dati dei contatori delle prestazioni, vengono innanzitutto raccolti nell'istanza</span><span class="sxs-lookup"><span data-stu-id="57f79-231">Diagnostics data, including performance counters, is first collected on the instance.</span></span> <span data-ttu-id="57f79-232">e quindi salvati in modo permanente nella tabella WADPerformanceCountersTable del servizio tabelle di Azure, pertanto è necessario specificare l'account di archiviazione nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="57f79-232">The data is then persisted to the WADPerformanceCountersTable table in the Azure Table service, so you will also need to specify the storage account in your application.</span></span> <span data-ttu-id="57f79-233">Se si esegue il test dell'applicazione in locale nell'emulatore di calcolo, è anche possibile archiviare i dati di diagnostica in locale nell'emulatore di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="57f79-233">If you're testing your application locally in the Compute Emulator, you can also store diagnostics data locally in the Storage Emulator.</span></span> <span data-ttu-id="57f79-234">Prima di archiviare i dati di diagnostica è necessario passare al [portale di Azure](http://portal.azure.com/) e creare un account di archiviazione classico.</span><span class="sxs-lookup"><span data-stu-id="57f79-234">Before you store diagnostics data, you must first go to the [Azure portal](http://portal.azure.com/) and create a classic storage account.</span></span> <span data-ttu-id="57f79-235">È consigliabile creare l'account di archiviazione nella stessa area geografica in cui si trova l'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="57f79-235">A best practice is to locate your storage account in the same geo-location as your Azure application.</span></span> <span data-ttu-id="57f79-236">Mantenendo l'applicazione e l'account di archiviazione di Azure nella stessa area geografica, si evita il pagamento di costi per la larghezza di banda esterna e si riduce la latenza.</span><span class="sxs-lookup"><span data-stu-id="57f79-236">By keeping the Azure application and storage account are in the same geo-location, you avoid paying external bandwidth costs and reduce latency.</span></span>

### <a name="add-performance-counters-to-the-diagnostics-file"></a><span data-ttu-id="57f79-237">Aggiungere i contatori delle prestazioni nel file della diagnostica</span><span class="sxs-lookup"><span data-stu-id="57f79-237">Add performance counters to the diagnostics file</span></span>
<span data-ttu-id="57f79-238">È possibile usare diversi contatori.</span><span class="sxs-lookup"><span data-stu-id="57f79-238">There are many counters you can use.</span></span> <span data-ttu-id="57f79-239">L'esempio seguente comprende diversi contatori delle prestazioni consigliati per il monitoraggio dei ruoli Web e di lavoro.</span><span class="sxs-lookup"><span data-stu-id="57f79-239">The following example shows several performance counters that are recommended for web and worker role monitoring.</span></span>

<span data-ttu-id="57f79-240">Aprire il file della diagnostica (diagnostics.wadcfg in SDK 2.4 e versioni precedenti o diagnostics.wadcfgx in SDK 2.5 e versioni successive) e aggiungere quanto segue all'elemento DiagnosticMonitorConfiguration:</span><span class="sxs-lookup"><span data-stu-id="57f79-240">Open the diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add the following to the DiagnosticMonitorConfiguration element:</span></span>

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use the Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use the Process(WaWorkerHost) category counters in a worker role.
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\% Processor Time" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Private Bytes" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Thread Count" sampleRate="PT30S" />
    -->

    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Interop(_Global_)\# of marshalling" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Loading(_Global_)\% Time Loading" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR LocksAndThreads(_Global_)\Contention Rate / sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Memory(_Global_)\# Bytes in all Heaps" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Networking(_Global_)\Connections Established" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Remoting(_Global_)\Remote Calls/sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Jit(_Global_)\% Time in Jit" sampleRate="PT30S" />
</PerformanceCounters>
```

<span data-ttu-id="57f79-241">L'attributo bufferQuotaInMB, che specifica la quantità massima di spazio di archiviazione disponibile nel file system per il tipo di raccolta dati (log di Azure, log di IIS ecc.).</span><span class="sxs-lookup"><span data-stu-id="57f79-241">The bufferQuotaInMB attribute, which specifies the maximum amount of file system storage that is available for the data collection type (Azure logs, IIS logs, etc.).</span></span> <span data-ttu-id="57f79-242">Il valore predefinito è 0.</span><span class="sxs-lookup"><span data-stu-id="57f79-242">The default is 0.</span></span> <span data-ttu-id="57f79-243">Quando viene raggiunta la quota massima, i dati meno recenti vengono eliminati man mano che vengono aggiunti nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="57f79-243">When the quota is reached, the oldest data is deleted as new data is added.</span></span> <span data-ttu-id="57f79-244">La somma di tutte le proprietà di bufferQuotaInMB deve essere maggiore del valore dell'attributo OverallQuotaInMB.</span><span class="sxs-lookup"><span data-stu-id="57f79-244">The sum of all the bufferQuotaInMB properties must be greater than the value of the OverallQuotaInMB attribute.</span></span> <span data-ttu-id="57f79-245">Per informazioni dettagliate su come determinare la quantità di archiviazione necessaria per la raccolta dei dati di diagnostica, vedere la sezione relativa alla configurazione di WAD in [Procedure consigliate di risoluzione dei problemi per lo sviluppo di applicazioni Azure](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="57f79-245">For a more detailed discussion of determining how much storage will be required for the collection of diagnostics data, see the Setup WAD section of [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span></span>

<span data-ttu-id="57f79-246">L'attributo scheduledTransferPeriod, che specifica l'intervallo tra i trasferimenti di dati pianificati, arrotondato per eccesso al minuto più vicino.</span><span class="sxs-lookup"><span data-stu-id="57f79-246">The scheduledTransferPeriod attribute, which specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span> <span data-ttu-id="57f79-247">Negli esempi seguenti è impostato su PT30M (30 minuti).</span><span class="sxs-lookup"><span data-stu-id="57f79-247">In the following examples, it is set to PT30M (30 minutes).</span></span> <span data-ttu-id="57f79-248">Un valore di impostazione troppo basso, ad esempio 1 minuto, del periodo di trasferimento influisce negativamente sulle prestazioni dell'applicazione in produzione, ma può risultare utile per l'esecuzione rapida della diagnostica in fase di test.</span><span class="sxs-lookup"><span data-stu-id="57f79-248">Setting the transfer period to a small value, such as 1 minute, will adversely impact your application's performance in production but can be useful for seeing diagnostics working quickly when you are testing.</span></span> <span data-ttu-id="57f79-249">Il periodo di trasferimento pianificato deve essere sufficientemente basso da garantire che i dati di diagnostica non vengano sovrascritti nell'istanza, ma anche sufficientemente alto da non influire sulle prestazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="57f79-249">The scheduled transfer period should be small enough to ensure that diagnostic data is not overwritten on the instance, but large enough that it will not impact the performance of your application.</span></span>

<span data-ttu-id="57f79-250">L'attributo counterSpecifier specifica il contatore delle prestazioni di cui raccogliere i dati.</span><span class="sxs-lookup"><span data-stu-id="57f79-250">The counterSpecifier attribute specifies the performance counter to collect.</span></span> <span data-ttu-id="57f79-251">L'attributo sampleRate specifica la frequenza con cui raccogliere i dati del contatore delle prestazioni, in questo caso 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="57f79-251">The sampleRate attribute specifies the rate at which the performance counter should be sampled, in this case 30 seconds.</span></span>

<span data-ttu-id="57f79-252">Una volta aggiunti i contatori delle prestazioni di cui raccogliere i dati, salvare le modifiche nel file diagnostica.</span><span class="sxs-lookup"><span data-stu-id="57f79-252">Once you've added the performance counters that you want to collect, save your changes to the diagnostics file.</span></span> <span data-ttu-id="57f79-253">Sarà quindi necessario specificare l'account di archiviazione nel quale verranno salvati in modo permanente i dati di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="57f79-253">Next, you need to specify the storage account that the diagnostics data will be persisted to.</span></span>

### <a name="specify-the-storage-account"></a><span data-ttu-id="57f79-254">Specificare l'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="57f79-254">Specify the storage account</span></span>
<span data-ttu-id="57f79-255">Per salvare in modo permanente le informazioni di diagnostica nell'account di archiviazione di Azure, è necessario specificare una stringa di connessione nel file di configurazione del servizio (ServiceConfiguration.cscfg).</span><span class="sxs-lookup"><span data-stu-id="57f79-255">To persist your diagnostics information to your Azure Storage account, you must specify a connection string in your service configuration (ServiceConfiguration.cscfg) file.</span></span>

<span data-ttu-id="57f79-256">Per Azure SDK 2.5 l'account di archiviazione può essere specificato nel file diagnostics.wadcfgx.</span><span class="sxs-lookup"><span data-stu-id="57f79-256">For Azure SDK 2.5, the Storage Account can be specified in the diagnostics.wadcfgx file.</span></span>

> [!NOTE]
> <span data-ttu-id="57f79-257">Queste istruzioni si applicano solo ad Azure SDK 2.4 e versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="57f79-257">These instructions only apply to Azure SDK 2.4 and below.</span></span> <span data-ttu-id="57f79-258">Per Azure SDK 2.5 l'account di archiviazione può essere specificato nel file diagnostics.wadcfgx.</span><span class="sxs-lookup"><span data-stu-id="57f79-258">For Azure SDK 2.5, the Storage Account can be specified in the diagnostics.wadcfgx file.</span></span>
>
>

<span data-ttu-id="57f79-259">Per impostare le stringhe di connessione:</span><span class="sxs-lookup"><span data-stu-id="57f79-259">To set the connection strings:</span></span>

1. <span data-ttu-id="57f79-260">Aprire il file ServiceConfiguration.Cloud.cscfg usando l'editor di testo preferito e impostare la stringa di connessione per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="57f79-260">Open the ServiceConfiguration.Cloud.cscfg file using your favorite text editor and set the connection string for your storage.</span></span> <span data-ttu-id="57f79-261">I valori *AccountName* e *AccountKey* sono disponibili nel dashboard dell'account di archiviazione del portale di Azure, in Chiavi di accesso.</span><span class="sxs-lookup"><span data-stu-id="57f79-261">The *AccountName* and *AccountKey* values are found in the Azure portal in the storage account dashboard, under Access keys.</span></span>

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. <span data-ttu-id="57f79-262">Salvare il file ServiceConfiguration.Cloud.cscfg.</span><span class="sxs-lookup"><span data-stu-id="57f79-262">Save the ServiceConfiguration.Cloud.cscfg file.</span></span>
3. <span data-ttu-id="57f79-263">Aprire il file ServiceConfiguration.Local.cscfg e verificare che UseDevelopmentStorage sia impostato su true.</span><span class="sxs-lookup"><span data-stu-id="57f79-263">Open the ServiceConfiguration.Local.cscfg file and verify that UseDevelopmentStorage is set to true.</span></span>

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   <span data-ttu-id="57f79-264">Ora che le stringhe di connessione sono impostate, i dati di diagnostica verranno salvati in modo permanente nell'account di archiviazione al momento della distribuzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="57f79-264">Now that the connection strings are set, your application will persist diagnostics data to your storage account when your application is deployed.</span></span>
4. <span data-ttu-id="57f79-265">Salvare e compilare il progetto, quindi distribuire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="57f79-265">Save and build your project, then deploy your application.</span></span>

## <a name="step-2-optional-create-custom-performance-counters"></a><span data-ttu-id="57f79-266">Passaggio 2: (Facoltativo) Creare contatori delle prestazioni personalizzati</span><span class="sxs-lookup"><span data-stu-id="57f79-266">Step 2: (Optional) Create custom performance counters</span></span>
<span data-ttu-id="57f79-267">Oltre ai contatori delle prestazioni predefiniti, è possibile aggiungere contatori delle prestazioni personalizzati per monitorare i ruoli Web o di lavoro.</span><span class="sxs-lookup"><span data-stu-id="57f79-267">In addition to the pre-defined performance counters, you can add your own custom performance counters to monitor web or worker roles.</span></span> <span data-ttu-id="57f79-268">I contatori delle prestazioni personalizzati possono essere utilizzati per tenere traccia e monitorare il funzionamento specifico dell'applicazione e possono essere creati o eliminati in un'attività di avvio, in un ruolo Web o in un ruolo di lavoro con autorizzazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="57f79-268">Custom performance counters may be used to track and monitor application-specific behavior and can be created or deleted in a startup task, web role, or worker role with elevated permissions.</span></span>

<span data-ttu-id="57f79-269">L'agente Diagnostica di Azure aggiorna la configurazione dei contatori delle prestazioni dal file con estensione wadcfg un minuto dopo l'avvio.</span><span class="sxs-lookup"><span data-stu-id="57f79-269">The Azure diagnostics agent refreshes the performance counter configuration from the .wadcfg file one minute after starting.</span></span>  <span data-ttu-id="57f79-270">Se si creano contatori delle prestazioni personalizzati nel metodo OnStart e l'esecuzione delle attività di avvio dura più di un minuto, i contatori delle prestazioni personalizzati non risulteranno creati quando l'agente Diagnostica di Azure cercherà di caricarli.</span><span class="sxs-lookup"><span data-stu-id="57f79-270">If you create custom performance counters in the OnStart method and your startup tasks take longer than one minute to execute, your custom performance counters will not have been created when the Azure Diagnostics agent tries to load them.</span></span>  <span data-ttu-id="57f79-271">In questo scenario Diagnostica di Azure acquisirà correttamente tutti i dati di diagnostica tranne i contatori delle prestazioni personalizzati.</span><span class="sxs-lookup"><span data-stu-id="57f79-271">In this scenario, you will see that Azure Diagnostics correctly captures all diagnostics data except your custom performance counters.</span></span>  <span data-ttu-id="57f79-272">Per risolvere questo problema, creare i contatori delle prestazioni in un'attività di avvio o spostare parte delle operazioni delle attività di avvio al metodo OnStart dopo avere creato i contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="57f79-272">To resolve this issue, create the performance counters in a startup task or move some of your startup task work to the OnStart method after creating the performance counters.</span></span>

<span data-ttu-id="57f79-273">Per creare un semplice contatore delle prestazioni personalizzato denominato "\MyCustomCounterCategory\MyButton1Counter", effettuare i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="57f79-273">Perform the following steps to create a simple custom performance counter named "\MyCustomCounterCategory\MyButton1Counter":</span></span>

1. <span data-ttu-id="57f79-274">Aprire il file di definizione del servizio (CSDEF) dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="57f79-274">Open the service definition file (CSDEF) for your application.</span></span>
2. <span data-ttu-id="57f79-275">Aggiungere l'elemento Runtime all'elemento WebRole o WorkerRole per consentire l'esecuzione con privilegi elevati:</span><span class="sxs-lookup"><span data-stu-id="57f79-275">Add the Runtime element to the WebRole or WorkerRole element to allow execution with elevated privileges:</span></span>

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. <span data-ttu-id="57f79-276">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="57f79-276">Save the file.</span></span>
4. <span data-ttu-id="57f79-277">Aprire il file della diagnostica (diagnostics.wadcfg in SDK 2.4 e versioni precedenti o diagnostics.wadcfgx in SDK 2.5 e versioni successive) e aggiungere quanto segue a DiagnosticMonitorConfiguration:</span><span class="sxs-lookup"><span data-stu-id="57f79-277">Open the diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add the following to the DiagnosticMonitorConfiguration</span></span>

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. <span data-ttu-id="57f79-278">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="57f79-278">Save the file.</span></span>
6. <span data-ttu-id="57f79-279">Creare la categoria dei contatori delle prestazioni personalizzati nel metodo OnStart del ruolo prima di richiamare base.OnStart.</span><span class="sxs-lookup"><span data-stu-id="57f79-279">Create the custom performance counter category in the OnStart method of your role, before invoking base.OnStart.</span></span> <span data-ttu-id="57f79-280">Nell'esempio C# seguente viene creata una categoria personalizzata, nel caso in cui non esista già:</span><span class="sxs-lookup"><span data-stu-id="57f79-280">The following C# example creates a custom category, if it does not already exist:</span></span>

    ```csharp
    public override bool OnStart()
    {
      if (!PerformanceCounterCategory.Exists("MyCustomCounterCategory"))
      {
         CounterCreationDataCollection counterCollection = new CounterCreationDataCollection();

         // add a counter tracking user button1 clicks
         CounterCreationData operationTotal1 = new CounterCreationData();
         operationTotal1.CounterName = "MyButton1Counter";
         operationTotal1.CounterHelp = "My Custom Counter for Button1";
         operationTotal1.CounterType = PerformanceCounterType.NumberOfItems32;
         counterCollection.Add(operationTotal1);

         PerformanceCounterCategory.Create(
           "MyCustomCounterCategory",
           "My Custom Counter Category",
           PerformanceCounterCategoryType.SingleInstance, counterCollection);

         Trace.WriteLine("Custom counter category created.");
      }
      else {
        Trace.WriteLine("Custom counter category already exists.");
      }

    return base.OnStart();
    }
    ```
7. <span data-ttu-id="57f79-281">Aggiornare i contatori all'interno dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="57f79-281">Update the counters within your application.</span></span> <span data-ttu-id="57f79-282">Nell'esempio seguente viene aggiornato un contatore delle prestazioni personalizzato per gli eventi Button1_Click:</span><span class="sxs-lookup"><span data-stu-id="57f79-282">The following example updates a custom performance counter on Button1_Click events:</span></span>

    ```csharp
    protected void Button1_Click(object sender, EventArgs e)
    {
      PerformanceCounter button1Counter = new PerformanceCounter(
        "MyCustomCounterCategory",
        "MyButton1Counter",
        string.Empty,
        false);
      button1Counter.Increment();
      this.Button1.Text = "Button 1 count: " +
        button1Counter.RawValue.ToString();
    }
    ```
8. <span data-ttu-id="57f79-283">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="57f79-283">Save the file.</span></span>  

<span data-ttu-id="57f79-284">I dati dei contatori delle prestazioni personalizzati verranno ora raccolti dal monitoraggio di diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="57f79-284">Custom performance counter data will now be collected by the Azure diagnostics monitor.</span></span>

## <a name="step-3-query-performance-counter-data"></a><span data-ttu-id="57f79-285">Passaggio 3: Eseguire query sui dati dei contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="57f79-285">Step 3: Query performance counter data</span></span>
<span data-ttu-id="57f79-286">Dopo che l'applicazione è stata distribuita ed è in esecuzione, il monitoraggio diagnostica inizierà a raccogliere i dati dei contatori delle prestazioni e a salvarli in modo permanente nell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="57f79-286">Once your application is deployed and running, the Diagnostics monitor will begin collecting performance counters and persisting that data to Azure storage.</span></span> <span data-ttu-id="57f79-287">Usare strumenti come Esplora server in Visual Studio, [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/) o [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) di Cerebrata per visualizzare i dati dei contatori delle prestazioni nella tabella WADPerformanceCountersTable.</span><span class="sxs-lookup"><span data-stu-id="57f79-287">You use tools such as Server Explorer in Visual Studio,  [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), or [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) by Cerebrata to view the performance counters data in the WADPerformanceCountersTable table.</span></span> <span data-ttu-id="57f79-288">A livello di codice è anche possibile eseguire una query sul servizio tabelle usando [C#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md) o [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span><span class="sxs-lookup"><span data-stu-id="57f79-288">You can also programmatically query the Table service using [C#](../cosmos-db/table-storage-how-to-use-dotnet.md),  [Java](../cosmos-db/table-storage-how-to-use-java.md),  [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), or [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span></span>

<span data-ttu-id="57f79-289">Nell'esempio C# seguente viene illustrato come eseguire una query di base sulla tabella WADPerformanceCountersTable e come salvare i dati di diagnostica in un file CSV.</span><span class="sxs-lookup"><span data-stu-id="57f79-289">The following C# example shows a basic query against the WADPerformanceCountersTable table and saves the diagnostics data to a CSV file.</span></span> <span data-ttu-id="57f79-290">Dopo aver salvato i contatori delle prestazioni in un file CSV, è possibile usare le funzionalità grafiche di Microsoft Excel o altri strumenti per visualizzare i dati.</span><span class="sxs-lookup"><span data-stu-id="57f79-290">Once the performance counters are saved to a CSV file, you can use the graphing capabilities in Microsoft Excel or some other tool to visualize the data.</span></span> <span data-ttu-id="57f79-291">Ricordarsi di aggiungere un riferimento a Microsoft.WindowsAzure.Storage.dll, che è stato incluso in Azure SDK per .NET a partire dalla versione di ottobre 2012.</span><span class="sxs-lookup"><span data-stu-id="57f79-291">Be sure to add a reference to Microsoft.WindowsAzure.Storage.dll, which is included in the Azure SDK for .NET October 2012 and later.</span></span> <span data-ttu-id="57f79-292">L'assembly viene installato nella directory %Programmi%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\.</span><span class="sxs-lookup"><span data-stu-id="57f79-292">The assembly is installed to the %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ directory.</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get the connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using the Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use the CloudConfigurationManager type
// to retrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store the connection string in your web.config or app.config file.
// Use the ConfigurationManager type to retrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference to the storage account using the connection string.  You can also use the development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create the table query, filter on a specific CounterName, DeploymentId and RoleInstance.
TableQuery<PerformanceCountersEntity> query = new TableQuery<PerformanceCountersEntity>()
  .Where(
    TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("CounterName", QueryComparisons.Equal, @"\Processor(_Total)\% Processor Time"),
      TableOperators.And,
      TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("DeploymentId", QueryComparisons.Equal, "ec26b7a1720447e1bcdeefc41c4892a3"),
      TableOperators.And,
      TableQuery.GenerateFilterCondition("RoleInstance", QueryComparisons.Equal, "WebRole1_IN_0")
    )
  )
);

// Execute the table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process the query results and build a CSV file.
StringBuilder sb = new StringBuilder("TimeStamp,EventTickCount,DeploymentId,Role,RoleInstance,CounterName,CounterValue\n");

foreach (PerformanceCountersEntity entity in result)
{
  sb.Append(entity.Timestamp + "," + entity.EventTickCount + "," + entity.DeploymentId + ","
    + entity.Role + "," + entity.RoleInstance + "," + entity.CounterName + "," + entity.CounterValue+"\n");
}

StreamWriter sw = File.CreateText(@"C:\temp\PerfCounters.csv");
sw.Write(sb.ToString());
sw.Close();
```

<span data-ttu-id="57f79-293">Per eseguire il mapping di entità a oggetti C#, viene utilizzata una classe personalizzata derivata da **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="57f79-293">Entities map to C# objects using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="57f79-294">Il codice seguente definisce una classe dell'entità che rappresenta un contatore delle prestazioni nella tabella **WADPerformanceCountersTable** .</span><span class="sxs-lookup"><span data-stu-id="57f79-294">The following code defines an entity class that represents a performance counter in the **WADPerformanceCountersTable** table.</span></span>

```csharp
public class PerformanceCountersEntity : TableEntity
{
  public long EventTickCount { get; set; }
  public string DeploymentId { get; set; }
  public string Role { get; set; }
  public string RoleInstance { get; set; }
  public string CounterName { get; set; }
  public double CounterValue { get; set; }
}
```

## <a name="next-steps"></a><span data-ttu-id="57f79-295">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="57f79-295">Next Steps</span></span>
[<span data-ttu-id="57f79-296">Visualizzare altri articoli sulla diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="57f79-296">View additional articles on Azure Diagnostics</span></span>](../azure-diagnostics.md)
