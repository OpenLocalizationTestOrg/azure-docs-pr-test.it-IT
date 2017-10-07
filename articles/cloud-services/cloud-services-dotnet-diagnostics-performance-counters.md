---
title: contatori delle prestazioni in diagnostica Azure aaaUse | Documenti Microsoft
description: Utilizzare i contatori delle prestazioni in servizi cloud di Azure o i colli di bottiglia toofind macchina virtuale e ottimizzare le prestazioni.
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
ms.openlocfilehash: f3250816c01fc6e164a6aae48da5035845e6d2b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a><span data-ttu-id="b9e97-103">Creare e usare contatori di prestazioni in un'applicazione Azure</span><span class="sxs-lookup"><span data-stu-id="b9e97-103">Create and use performance counters in an Azure application</span></span>
<span data-ttu-id="b9e97-104">Questo articolo descrive i vantaggi hello e come i contatori delle prestazioni tooput nell'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="b9e97-104">This article describes hello benefits of and how tooput performance counters into your Azure application.</span></span> <span data-ttu-id="b9e97-105">È possibile utilizzarli come dati toocollect, individuare i colli di bottiglia e ottimizzare le prestazioni del sistema e dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b9e97-105">You can use them toocollect data, find bottlenecks, and tune system and application performance.</span></span>

<span data-ttu-id="b9e97-106">Contatori delle prestazioni disponibili per Windows Server, IIS e ASP.NET possono anche essere raccolti e utilizzato integrità hello toodetermine di ruoli web di Azure e i ruoli di lavoro, le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="b9e97-106">Performance counters available for Windows Server, IIS, and ASP.NET can also be collected and used toodetermine hello health of your Azure web roles, worker roles, and Virtual Machines.</span></span> <span data-ttu-id="b9e97-107">È anche possibile creare e usare contatori delle prestazioni personalizzati.</span><span class="sxs-lookup"><span data-stu-id="b9e97-107">You can also create and use custom performance counters.</span></span>  

<span data-ttu-id="b9e97-108">È possibile esaminare i dati dei contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="b9e97-108">You can examine performance counter data</span></span>

1. <span data-ttu-id="b9e97-109">Direttamente nell'host di applicazioni hello con lo strumento Performance Monitor hello accesso tramite Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="b9e97-109">Directly on hello application host with hello Performance Monitor tool accessed using Remote Desktop</span></span>
2. <span data-ttu-id="b9e97-110">Con System Center Operations Manager hello Azure Management Pack</span><span class="sxs-lookup"><span data-stu-id="b9e97-110">With System Center Operations Manager using hello Azure Management Pack</span></span>
3. <span data-ttu-id="b9e97-111">Con altri strumenti di monitoraggio che accedono a hello tooAzure archiviazione trasferire i dati di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="b9e97-111">With other monitoring tools that access hello diagnostic data transferred tooAzure storage.</span></span> <span data-ttu-id="b9e97-112">Per altre informazioni, vedere [Archiviare e visualizzare i dati di diagnostica nell'account di archiviazione Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b9e97-112">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for more information.</span></span>  

<span data-ttu-id="b9e97-113">Per ulteriori informazioni sul monitoraggio delle prestazioni di hello dell'applicazione in hello [portale di Azure](http://portal.azure.com/), vedere [come servizi Cloud tooMonitor](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span><span class="sxs-lookup"><span data-stu-id="b9e97-113">For more information on monitoring hello performance of your application in hello [Azure portal](http://portal.azure.com/), see [How tooMonitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span></span>

<span data-ttu-id="b9e97-114">Per altre informazioni dettagliate sulla creazione di una registrazione e traccia strategia e sull'uso della diagnostica e altri problemi tootroubleshoot tecniche e ottimizzare le applicazioni Azure, vedere [risoluzione dei problemi di procedure consigliate per lo sviluppo di Azure Applicazioni](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="b9e97-114">For additional in-depth guidance on creating a logging and tracing strategy and using diagnostics and other techniques tootroubleshoot problems and optimize Azure applications, see [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span></span>

## <a name="enable-performance-counter-monitoring"></a><span data-ttu-id="b9e97-115">Abilitare il monitoraggio del contatore delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="b9e97-115">Enable performance counter monitoring</span></span>
<span data-ttu-id="b9e97-116">Per impostazione predefinita, i contatori delle prestazioni non sono abilitati.</span><span class="sxs-lookup"><span data-stu-id="b9e97-116">Performance counters are not enabled by default.</span></span> <span data-ttu-id="b9e97-117">L'applicazione o un'attività di avvio deve modificare diagnostica predefinito hello prestazioni specifici di agente configurazione tooinclude hello contatori che si desidera toomonitor per ogni istanza del ruolo.</span><span class="sxs-lookup"><span data-stu-id="b9e97-117">Your application or a startup task must modify hello default diagnostics agent configuration tooinclude hello specific performance counters that you wish toomonitor for each role instance.</span></span>

### <a name="performance-counters-available-for-microsoft-azure"></a><span data-ttu-id="b9e97-118">Contatori delle prestazioni disponibili per Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b9e97-118">Performance counters available for Microsoft Azure</span></span>
<span data-ttu-id="b9e97-119">Azure fornisce un subset di contatori delle prestazioni di hello disponibili per Windows Server, IIS e ASP.NET stack hello.</span><span class="sxs-lookup"><span data-stu-id="b9e97-119">Azure provides a subset of hello performance counters available for Windows Server, IIS and hello ASP.NET stack.</span></span> <span data-ttu-id="b9e97-120">Hello nella tabella seguente sono elencati alcuni dei contatori delle prestazioni di hello di particolare interesse per le applicazioni Azure.</span><span class="sxs-lookup"><span data-stu-id="b9e97-120">hello following table lists some of hello performance counters of particular interest for Azure applications.</span></span>

| <span data-ttu-id="b9e97-121">Categoria contatore: oggetto (istanza)</span><span class="sxs-lookup"><span data-stu-id="b9e97-121">Counter Category: Object (Instance)</span></span> | <span data-ttu-id="b9e97-122">Nome contatore</span><span class="sxs-lookup"><span data-stu-id="b9e97-122">Counter Name</span></span> | <span data-ttu-id="b9e97-123">Riferimento</span><span class="sxs-lookup"><span data-stu-id="b9e97-123">Reference</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b9e97-124">Eccezioni CLR .NET (*globale*)</span><span class="sxs-lookup"><span data-stu-id="b9e97-124">.NET CLR Exceptions(*Global*)</span></span> |<span data-ttu-id="b9e97-125">N. eccezioni/sec</span><span class="sxs-lookup"><span data-stu-id="b9e97-125"># Exceps Thrown / sec</span></span> |<span data-ttu-id="b9e97-126">Contatori delle prestazioni delle eccezioni</span><span class="sxs-lookup"><span data-stu-id="b9e97-126">Exception Performance Counters</span></span> |
| <span data-ttu-id="b9e97-127">Memoria CLR .NET (*globale*)</span><span class="sxs-lookup"><span data-stu-id="b9e97-127">.NET CLR Memory(*Global*)</span></span> |<span data-ttu-id="b9e97-128">Percentuale tempo in GC</span><span class="sxs-lookup"><span data-stu-id="b9e97-128">% Time in GC</span></span> |<span data-ttu-id="b9e97-129">Contatori delle prestazioni di memoria</span><span class="sxs-lookup"><span data-stu-id="b9e97-129">Memory Performance Counters</span></span> |
| <span data-ttu-id="b9e97-130">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b9e97-130">ASP.NET</span></span> |<span data-ttu-id="b9e97-131">Riavvii applicazione</span><span class="sxs-lookup"><span data-stu-id="b9e97-131">Application Restarts</span></span> |<span data-ttu-id="b9e97-132">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b9e97-132">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="b9e97-133">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b9e97-133">ASP.NET</span></span> |<span data-ttu-id="b9e97-134">Tempo di esecuzione della richiesta</span><span class="sxs-lookup"><span data-stu-id="b9e97-134">Request Execution Time</span></span> |<span data-ttu-id="b9e97-135">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b9e97-135">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="b9e97-136">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b9e97-136">ASP.NET</span></span> |<span data-ttu-id="b9e97-137">Richieste disconnesse</span><span class="sxs-lookup"><span data-stu-id="b9e97-137">Requests Disconnected</span></span> |<span data-ttu-id="b9e97-138">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b9e97-138">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="b9e97-139">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b9e97-139">ASP.NET</span></span> |<span data-ttu-id="b9e97-140">Riavvii processo di lavoro</span><span class="sxs-lookup"><span data-stu-id="b9e97-140">Worker Process Restarts</span></span> |<span data-ttu-id="b9e97-141">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b9e97-141">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="b9e97-142">Applicazioni ASP.NET (**totale**)</span><span class="sxs-lookup"><span data-stu-id="b9e97-142">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="b9e97-143">Totale richieste</span><span class="sxs-lookup"><span data-stu-id="b9e97-143">Requests Total</span></span> |<span data-ttu-id="b9e97-144">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b9e97-144">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="b9e97-145">Applicazioni ASP.NET (**totale**)</span><span class="sxs-lookup"><span data-stu-id="b9e97-145">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="b9e97-146">Richieste/sec</span><span class="sxs-lookup"><span data-stu-id="b9e97-146">Requests/Sec</span></span> |<span data-ttu-id="b9e97-147">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b9e97-147">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="b9e97-148">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="b9e97-148">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="b9e97-149">Tempo di esecuzione della richiesta</span><span class="sxs-lookup"><span data-stu-id="b9e97-149">Request Execution Time</span></span> |<span data-ttu-id="b9e97-150">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b9e97-150">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="b9e97-151">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="b9e97-151">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="b9e97-152">Tempo di attesa richiesta</span><span class="sxs-lookup"><span data-stu-id="b9e97-152">Request Wait Time</span></span> |<span data-ttu-id="b9e97-153">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b9e97-153">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="b9e97-154">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="b9e97-154">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="b9e97-155">Richieste correnti</span><span class="sxs-lookup"><span data-stu-id="b9e97-155">Requests Current</span></span> |<span data-ttu-id="b9e97-156">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b9e97-156">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="b9e97-157">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="b9e97-157">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="b9e97-158">Richieste in coda</span><span class="sxs-lookup"><span data-stu-id="b9e97-158">Requests Queued</span></span> |<span data-ttu-id="b9e97-159">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b9e97-159">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="b9e97-160">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="b9e97-160">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="b9e97-161">Richieste respinte</span><span class="sxs-lookup"><span data-stu-id="b9e97-161">Requests Rejected</span></span> |<span data-ttu-id="b9e97-162">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b9e97-162">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="b9e97-163">Memoria</span><span class="sxs-lookup"><span data-stu-id="b9e97-163">Memory</span></span> |<span data-ttu-id="b9e97-164">MByte disponibili</span><span class="sxs-lookup"><span data-stu-id="b9e97-164">Available MBytes</span></span> |<span data-ttu-id="b9e97-165">Contatori delle prestazioni di memoria</span><span class="sxs-lookup"><span data-stu-id="b9e97-165">Memory Performance Counters</span></span> |
| <span data-ttu-id="b9e97-166">Memoria</span><span class="sxs-lookup"><span data-stu-id="b9e97-166">Memory</span></span> |<span data-ttu-id="b9e97-167">Byte vincolati</span><span class="sxs-lookup"><span data-stu-id="b9e97-167">Committed Bytes</span></span> |<span data-ttu-id="b9e97-168">Contatori delle prestazioni di memoria</span><span class="sxs-lookup"><span data-stu-id="b9e97-168">Memory Performance Counters</span></span> |
| <span data-ttu-id="b9e97-169">Processor(_Total)</span><span class="sxs-lookup"><span data-stu-id="b9e97-169">Processor(_Total)</span></span> |<span data-ttu-id="b9e97-170">% di tempo processore</span><span class="sxs-lookup"><span data-stu-id="b9e97-170">% Processor Time</span></span> |<span data-ttu-id="b9e97-171">Contatori delle prestazioni per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b9e97-171">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="b9e97-172">TCPv4</span><span class="sxs-lookup"><span data-stu-id="b9e97-172">TCPv4</span></span> |<span data-ttu-id="b9e97-173">Errori di connessione</span><span class="sxs-lookup"><span data-stu-id="b9e97-173">Connection Failures</span></span> |<span data-ttu-id="b9e97-174">Oggetto TCP</span><span class="sxs-lookup"><span data-stu-id="b9e97-174">TCP Object</span></span> |
| <span data-ttu-id="b9e97-175">TCPv4</span><span class="sxs-lookup"><span data-stu-id="b9e97-175">TCPv4</span></span> |<span data-ttu-id="b9e97-176">Connessioni stabilite</span><span class="sxs-lookup"><span data-stu-id="b9e97-176">Connections Established</span></span> |<span data-ttu-id="b9e97-177">Oggetto TCP</span><span class="sxs-lookup"><span data-stu-id="b9e97-177">TCP Object</span></span> |
| <span data-ttu-id="b9e97-178">TCPv4</span><span class="sxs-lookup"><span data-stu-id="b9e97-178">TCPv4</span></span> |<span data-ttu-id="b9e97-179">Connessioni ripristinate</span><span class="sxs-lookup"><span data-stu-id="b9e97-179">Connections Reset</span></span> |<span data-ttu-id="b9e97-180">Oggetto TCP</span><span class="sxs-lookup"><span data-stu-id="b9e97-180">TCP Object</span></span> |
| <span data-ttu-id="b9e97-181">TCPv4</span><span class="sxs-lookup"><span data-stu-id="b9e97-181">TCPv4</span></span> |<span data-ttu-id="b9e97-182">Segmenti inviati/sec</span><span class="sxs-lookup"><span data-stu-id="b9e97-182">Segments Sent/sec</span></span> |<span data-ttu-id="b9e97-183">Oggetto TCP</span><span class="sxs-lookup"><span data-stu-id="b9e97-183">TCP Object</span></span> |
| <span data-ttu-id="b9e97-184">Interfaccia di rete (*)</span><span class="sxs-lookup"><span data-stu-id="b9e97-184">Network Interface(*)</span></span> |<span data-ttu-id="b9e97-185">Byte ricevuti/sec</span><span class="sxs-lookup"><span data-stu-id="b9e97-185">Bytes Received/sec</span></span> |<span data-ttu-id="b9e97-186">Oggetto interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="b9e97-186">Network Interface Object</span></span> |
| <span data-ttu-id="b9e97-187">Interfaccia di rete (*)</span><span class="sxs-lookup"><span data-stu-id="b9e97-187">Network Interface(*)</span></span> |<span data-ttu-id="b9e97-188">Byte inviati/sec</span><span class="sxs-lookup"><span data-stu-id="b9e97-188">Bytes Sent/sec</span></span> |<span data-ttu-id="b9e97-189">Oggetto interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="b9e97-189">Network Interface Object</span></span> |
| <span data-ttu-id="b9e97-190">Interfaccia di rete (Scheda di rete per il bus delle macchine virtuali Microsoft _2)</span><span class="sxs-lookup"><span data-stu-id="b9e97-190">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="b9e97-191">Byte ricevuti/sec</span><span class="sxs-lookup"><span data-stu-id="b9e97-191">Bytes Received/sec</span></span> |<span data-ttu-id="b9e97-192">Oggetto interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="b9e97-192">Network Interface Object</span></span> |
| <span data-ttu-id="b9e97-193">Interfaccia di rete (Scheda di rete per il bus delle macchine virtuali Microsoft _2)</span><span class="sxs-lookup"><span data-stu-id="b9e97-193">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="b9e97-194">Byte inviati/sec</span><span class="sxs-lookup"><span data-stu-id="b9e97-194">Bytes Sent/sec</span></span> |<span data-ttu-id="b9e97-195">Oggetto interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="b9e97-195">Network Interface Object</span></span> |
| <span data-ttu-id="b9e97-196">Interfaccia di rete (Scheda di rete per il bus delle macchine virtuali Microsoft _2)</span><span class="sxs-lookup"><span data-stu-id="b9e97-196">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="b9e97-197">Totale byte/sec</span><span class="sxs-lookup"><span data-stu-id="b9e97-197">Bytes Total/sec</span></span> |<span data-ttu-id="b9e97-198">Oggetto interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="b9e97-198">Network Interface Object</span></span> |

## <a name="create-and-add-custom-performance-counters-tooyour-application"></a><span data-ttu-id="b9e97-199">Creare e aggiungere l'applicazione di tooyour i contatori delle prestazioni personalizzati</span><span class="sxs-lookup"><span data-stu-id="b9e97-199">Create and add custom performance counters tooyour application</span></span>
<span data-ttu-id="b9e97-200">Azure dispone di supporto toocreate e modificare i contatori delle prestazioni personalizzati per i ruoli web e ruoli di lavoro.</span><span class="sxs-lookup"><span data-stu-id="b9e97-200">Azure has support toocreate and modify custom performance counters for web roles and worker roles.</span></span> <span data-ttu-id="b9e97-201">contatori di Hello possono essere utilizzato il comportamento di specifiche dell'applicazione tootrack e monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="b9e97-201">hello counters may be used tootrack and monitor application-specific behavior.</span></span> <span data-ttu-id="b9e97-202">È possibile creare ed eliminare categorie e identificatori dei contatori delle prestazioni personalizzati da un'attività di avvio, un ruolo Web o un ruolo di lavoro con autorizzazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="b9e97-202">You can create and delete custom performance counter categories and specifiers from a startup task, web role, or worker role with elevated permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="b9e97-203">Codice che modifica i contatori delle prestazioni toocustom deve elevate toorun autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="b9e97-203">Code that makes changes toocustom performance counters must have elevated permissions toorun.</span></span> <span data-ttu-id="b9e97-204">Se il codice hello è in un ruolo web o un ruolo di lavoro, il ruolo di hello deve includere tag hello <Runtime executionContext="elevated" /> in hello servicedefinition. Csdef del file per hello ruolo tooinitialize correttamente.</span><span class="sxs-lookup"><span data-stu-id="b9e97-204">If hello code is in a web role or worker role, hello role must include hello tag <Runtime executionContext="elevated" /> in hello ServiceDefinition.csdef file for hello role tooinitialize properly.</span></span>
>
>

<span data-ttu-id="b9e97-205">È possibile inviare archiviazione tooAzure dati contatore di prestazioni personalizzati utilizzando hello diagnostica agente.</span><span class="sxs-lookup"><span data-stu-id="b9e97-205">You can send custom performance counter data tooAzure storage using hello diagnostics agent.</span></span>

<span data-ttu-id="b9e97-206">i dati dei contatori delle prestazioni standard Hello viene generati da hello che Azure elabora.</span><span class="sxs-lookup"><span data-stu-id="b9e97-206">hello standard performance counter data is generated by hello Azure processes.</span></span> <span data-ttu-id="b9e97-207">I dati dei contatori delle prestazioni personalizzati devono essere creati dall'applicazione ruolo Web o ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="b9e97-207">Custom performance counter data must be created by your web role or worker role application.</span></span> <span data-ttu-id="b9e97-208">Vedere [tipi di contatori delle prestazioni](https://msdn.microsoft.com/library/z573042h.aspx) per informazioni sui tipi di hello di dati che possono essere archiviati in contatori delle prestazioni personalizzati.</span><span class="sxs-lookup"><span data-stu-id="b9e97-208">See [Performance Counter Types](https://msdn.microsoft.com/library/z573042h.aspx) for information on hello types of data that can be stored in custom performance counters.</span></span> <span data-ttu-id="b9e97-209">Per un esempio di creazione e impostazione dei dati dei contatori delle prestazioni personalizzati in un ruolo Web, vedere [Esempio PerformanceCounters](http://code.msdn.microsoft.com/azure/) .</span><span class="sxs-lookup"><span data-stu-id="b9e97-209">See [PerformanceCounters Sample](http://code.msdn.microsoft.com/azure/) for an example that creates and sets custom performance counter data in a web role.</span></span>

## <a name="store-and-view-performance-counter-data"></a><span data-ttu-id="b9e97-210">Archiviare e visualizzare i dati dei contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="b9e97-210">Store and view performance counter data</span></span>
<span data-ttu-id="b9e97-211">Azure memorizza nella cache i dati dei contatori delle prestazioni con altre informazioni di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="b9e97-211">Azure caches performance counter data with other diagnostic information.</span></span> <span data-ttu-id="b9e97-212">Questi dati sono disponibili per il monitoraggio remoto durante l'esecuzione di istanza del ruolo hello utilizzando gli strumenti tooview accesso desktop remoto, ad esempio Performance Monitor.</span><span class="sxs-lookup"><span data-stu-id="b9e97-212">This data is available for remote monitoring while hello role instance is running using remote desktop access tooview tools such as Performance Monitor.</span></span> <span data-ttu-id="b9e97-213">toopersist hello trasferimento dei dati all'esterno di istanza del ruolo hello, agente di diagnostica hello deve archiviazione tooAzure dei dati hello.</span><span class="sxs-lookup"><span data-stu-id="b9e97-213">toopersist hello data outside of hello role instance, hello diagnostics agent must transfer hello data tooAzure storage.</span></span> <span data-ttu-id="b9e97-214">limite delle dimensioni dei dati dei contatori delle prestazioni memorizzati nella cache di hello Hello può essere configurato nell'agente di diagnostica hello o può essere configurato toobe parte di un limite condiviso per tutti i dati di diagnostica di hello.</span><span class="sxs-lookup"><span data-stu-id="b9e97-214">hello size limit of hello cached performance counter data can be configured in hello diagnostics agent, or it may be configured toobe part of a shared limit for all hello diagnostic data.</span></span> <span data-ttu-id="b9e97-215">Per ulteriori informazioni sull'impostazione delle dimensioni del buffer hello, vedere [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) e [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span><span class="sxs-lookup"><span data-stu-id="b9e97-215">For more information about setting hello buffer size, see [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) and [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span></span> <span data-ttu-id="b9e97-216">Vedere [archivio e visualizza i dati di diagnostica in archiviazione di Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx) per una panoramica dell'impostazione di account di archiviazione di hello diagnostica agente tootransfer dati tooa.</span><span class="sxs-lookup"><span data-stu-id="b9e97-216">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for an overview of setting up hello diagnostics agent tootransfer data tooa storage account.</span></span>

<span data-ttu-id="b9e97-217">Ogni istanza del contatore delle prestazioni configurati viene registrata con una frequenza di campionamento specificata e trasferimento dei dati campionato hello toohello account di archiviazione tramite una richiesta di trasferimento pianificato o di una richiesta di trasferimento su richiesta.</span><span class="sxs-lookup"><span data-stu-id="b9e97-217">Each configured performance counter instance is recorded at a specified sampling rate, and hello sampled data is transferred toohello storage account either by a scheduled transfer request or an on-demand transfer request.</span></span> <span data-ttu-id="b9e97-218">I trasferimenti automatici possono essere pianificati con una frequenza di una volta ogni minuto.</span><span class="sxs-lookup"><span data-stu-id="b9e97-218">Automatic transfers may be scheduled as often as once per minute.</span></span> <span data-ttu-id="b9e97-219">Dati del contatore di prestazioni trasferiti dall'agente di diagnostica hello sono archiviati in una tabella, WADPerformanceCountersTable, nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="b9e97-219">Performance counter data transferred by hello diagnostics agent is stored in a table, WADPerformanceCountersTable, in hello storage account.</span></span> <span data-ttu-id="b9e97-220">Questa tabella è accessibile e può essere sottoposta a query con i metodi API di archiviazione standard di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9e97-220">This table may be accessed and queried with standard Azure storage API methods.</span></span> <span data-ttu-id="b9e97-221">Vedere [esempio PerformanceCounters di Microsoft Azure](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) per un esempio di query e visualizzazione di dati del contatore delle prestazioni dalla tabella WADPerformanceCountersTable hello.</span><span class="sxs-lookup"><span data-stu-id="b9e97-221">See [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) for an example of querying and displaying performance counter data from hello WADPerformanceCountersTable table.</span></span>

> [!NOTE]
> <span data-ttu-id="b9e97-222">A seconda della frequenza di trasferimento dell'agente di diagnostica hello e latenza della coda, hello dati più recente del contatore delle prestazioni nell'account di archiviazione hello sia aggiornata alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="b9e97-222">Depending on hello diagnostics agent transfer frequency and queue latency, hello most recent performance counter data in hello storage account may be several minutes out of date.</span></span>
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a><span data-ttu-id="b9e97-223">Abilitare i contatori delle prestazioni con il file di configurazione della diagnostica</span><span class="sxs-lookup"><span data-stu-id="b9e97-223">Enable performance counters using diagnostics configuration file</span></span>
<span data-ttu-id="b9e97-224">Utilizzare i seguenti contatori delle prestazioni di stored procedure tooenable nell'applicazione Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b9e97-224">Use hello following procedure tooenable performance counters in your Azure application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9e97-225">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b9e97-225">Prerequisites</span></span>
<span data-ttu-id="b9e97-226">In questa sezione si presuppone di aver importato monitor di diagnostica hello nell'applicazione e aggiunto hello diagnostica configurazione file tooyour soluzione di Visual Studio (Diagnostics. wadcfg in SDK 2.4 e di sotto o wadcfgx in SDK 2.5 e versioni successive).</span><span class="sxs-lookup"><span data-stu-id="b9e97-226">This section assumes that you have imported hello Diagnostics monitor into your application and added hello diagnostics configuration file tooyour Visual Studio solution (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above).</span></span> <span data-ttu-id="b9e97-227">Per altre informazioni, vedere i passaggi 1 e 2 in [Abilitazione della diagnostica nei servizi cloud e nelle macchine virtuali di Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="b9e97-227">See steps 1 and 2 in [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md)) for more information.</span></span>

## <a name="step-1-collect-and-store-data-from-performance-counters"></a><span data-ttu-id="b9e97-228">Passaggio 1: Raccogliere e archiviare i dati dei contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="b9e97-228">Step 1: Collect and store data from performance counters</span></span>
<span data-ttu-id="b9e97-229">Dopo aver aggiunto la diagnostica hello file tooyour soluzione di Visual Studio, è possibile configurare hello raccolta e l'archiviazione dei dati dei contatori delle prestazioni in un'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="b9e97-229">After you have added hello diagnostics file tooyour Visual Studio solution, you can configure hello collection and storage of performance counter data in an Azure application.</span></span> <span data-ttu-id="b9e97-230">Questa operazione viene eseguita mediante l'aggiunta di file di diagnostica toohello dei contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="b9e97-230">This is done by adding performance counters toohello diagnostics file.</span></span> <span data-ttu-id="b9e97-231">Dati di diagnostica, inclusi i contatori delle prestazioni, vengono prima raccolti nell'istanza di hello.</span><span class="sxs-lookup"><span data-stu-id="b9e97-231">Diagnostics data, including performance counters, is first collected on hello instance.</span></span> <span data-ttu-id="b9e97-232">dati Hello sono persistente toohello WADPerformanceCountersTable tabella hello servizio tabelle di Azure, pertanto sarà anche necessario toospecify hello account di archiviazione nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b9e97-232">hello data is then persisted toohello WADPerformanceCountersTable table in hello Azure Table service, so you will also need toospecify hello storage account in your application.</span></span> <span data-ttu-id="b9e97-233">Se si sta testando l'applicazione localmente nell'emulatore di calcolo di hello, è anche possibile archiviare i dati di diagnostica a livello locale in hello emulatore di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b9e97-233">If you're testing your application locally in hello Compute Emulator, you can also store diagnostics data locally in hello Storage Emulator.</span></span> <span data-ttu-id="b9e97-234">Prima di archiviare dati di diagnostica, è necessario passare toohello [portale di Azure](http://portal.azure.com/) e creare un account di archiviazione classico.</span><span class="sxs-lookup"><span data-stu-id="b9e97-234">Before you store diagnostics data, you must first go toohello [Azure portal](http://portal.azure.com/) and create a classic storage account.</span></span> <span data-ttu-id="b9e97-235">È consigliabile toolocate account di archiviazione nella stessa posizione geografica dell'applicazione Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b9e97-235">A best practice is toolocate your storage account in hello same geo-location as your Azure application.</span></span> <span data-ttu-id="b9e97-236">Da mantenere hello Azure account di archiviazione e di applicazione sono in hello stessa località geografica, evitare di sostenere costi di larghezza di banda esterna e ridurre la latenza.</span><span class="sxs-lookup"><span data-stu-id="b9e97-236">By keeping hello Azure application and storage account are in hello same geo-location, you avoid paying external bandwidth costs and reduce latency.</span></span>

### <a name="add-performance-counters-toohello-diagnostics-file"></a><span data-ttu-id="b9e97-237">Aggiungere file di diagnostica toohello dei contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="b9e97-237">Add performance counters toohello diagnostics file</span></span>
<span data-ttu-id="b9e97-238">È possibile usare diversi contatori.</span><span class="sxs-lookup"><span data-stu-id="b9e97-238">There are many counters you can use.</span></span> <span data-ttu-id="b9e97-239">Hello riportato di seguito diversi contatori delle prestazioni consigliati per il web e ruolo di lavoro monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="b9e97-239">hello following example shows several performance counters that are recommended for web and worker role monitoring.</span></span>

<span data-ttu-id="b9e97-240">Aprire il file di hello diagnostica (Diagnostics. wadcfg in SDK 2.4 e versioni precedenti o wadcfgx in SDK 2.5 e versioni successive) e aggiungere hello successivo elemento DiagnosticMonitorConfiguration toohello:</span><span class="sxs-lookup"><span data-stu-id="b9e97-240">Open hello diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add hello following toohello DiagnosticMonitorConfiguration element:</span></span>

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use hello Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use hello Process(WaWorkerHost) category counters in a worker role.
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

<span data-ttu-id="b9e97-241">attributo di bufferQuotaInMB Hello, che specifica hello quantità massima di archiviazione nel file system disponibile per il tipo di raccolta dati hello (log di Azure, i log di IIS e così via).</span><span class="sxs-lookup"><span data-stu-id="b9e97-241">hello bufferQuotaInMB attribute, which specifies hello maximum amount of file system storage that is available for hello data collection type (Azure logs, IIS logs, etc.).</span></span> <span data-ttu-id="b9e97-242">valore predefinito di Hello è 0.</span><span class="sxs-lookup"><span data-stu-id="b9e97-242">hello default is 0.</span></span> <span data-ttu-id="b9e97-243">Quando viene raggiunta la quota hello, dati meno recenti di hello vengono eliminati man mano che vengono aggiunti nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="b9e97-243">When hello quota is reached, hello oldest data is deleted as new data is added.</span></span> <span data-ttu-id="b9e97-244">somma di Hello di tutte le proprietà di bufferQuotaInMB hello deve essere maggiore del valore di hello dell'attributo OverallQuotaInMB hello.</span><span class="sxs-lookup"><span data-stu-id="b9e97-244">hello sum of all hello bufferQuotaInMB properties must be greater than hello value of hello OverallQuotaInMB attribute.</span></span> <span data-ttu-id="b9e97-245">Per una discussione più dettagliata di determinare la quantità di archiviazione richiesta per la raccolta di hello dei dati di diagnostica, vedere hello sezione WAD il programma di installazione di [risoluzione dei problemi di procedure consigliate per lo sviluppo di applicazioni Azure](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="b9e97-245">For a more detailed discussion of determining how much storage will be required for hello collection of diagnostics data, see hello Setup WAD section of [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span></span>

<span data-ttu-id="b9e97-246">l'attributo scheduledTransferPeriod Hello, che specifica l'intervallo di hello tra i trasferimenti di dati pianificati, arrotondato per eccesso toohello più vicino al minuto.</span><span class="sxs-lookup"><span data-stu-id="b9e97-246">hello scheduledTransferPeriod attribute, which specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span> <span data-ttu-id="b9e97-247">In hello seguono esempi, è impostato tooPT30M (30 minuti).</span><span class="sxs-lookup"><span data-stu-id="b9e97-247">In hello following examples, it is set tooPT30M (30 minutes).</span></span> <span data-ttu-id="b9e97-248">Impostazione hello trasferimento tooa periodo valore basso, ad esempio 1 minuto, influisce negativamente sulle prestazioni dell'applicazione nell'ambiente di produzione, ma può essere utile per visualizzare l'esecuzione rapida, quando si esegue il test della diagnostica.</span><span class="sxs-lookup"><span data-stu-id="b9e97-248">Setting hello transfer period tooa small value, such as 1 minute, will adversely impact your application's performance in production but can be useful for seeing diagnostics working quickly when you are testing.</span></span> <span data-ttu-id="b9e97-249">periodo di trasferimento pianificato Hello deve essere sufficientemente piccole tooensure che i dati di diagnostica non viene sovrascritti nell'istanza di hello, ma sufficientemente elevato che non influirà hello delle prestazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b9e97-249">hello scheduled transfer period should be small enough tooensure that diagnostic data is not overwritten on hello instance, but large enough that it will not impact hello performance of your application.</span></span>

<span data-ttu-id="b9e97-250">attributo counterSpecifier Hello specifica toocollect contatore delle prestazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="b9e97-250">hello counterSpecifier attribute specifies hello performance counter toocollect.</span></span> <span data-ttu-id="b9e97-251">attributo sampleRate Hello specifica velocità hello in corrispondenza del quale hello delle prestazioni del contatore, in questo caso 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="b9e97-251">hello sampleRate attribute specifies hello rate at which hello performance counter should be sampled, in this case 30 seconds.</span></span>

<span data-ttu-id="b9e97-252">Una volta aggiunti i contatori delle prestazioni di hello che si desidera toocollect, salvare il file di diagnostica toohello di modifiche.</span><span class="sxs-lookup"><span data-stu-id="b9e97-252">Once you've added hello performance counters that you want toocollect, save your changes toohello diagnostics file.</span></span> <span data-ttu-id="b9e97-253">Successivamente, è necessario l'account di archiviazione hello toospecify che verranno mantenuti per i dati di diagnostica hello.</span><span class="sxs-lookup"><span data-stu-id="b9e97-253">Next, you need toospecify hello storage account that hello diagnostics data will be persisted to.</span></span>

### <a name="specify-hello-storage-account"></a><span data-ttu-id="b9e97-254">Specificare l'account di archiviazione hello</span><span class="sxs-lookup"><span data-stu-id="b9e97-254">Specify hello storage account</span></span>
<span data-ttu-id="b9e97-255">toopersist il tooyour informazioni di diagnostica Azure Storage account, è necessario specificare una stringa di connessione nel file di configurazione (ServiceConfiguration. cscfg) del servizio.</span><span class="sxs-lookup"><span data-stu-id="b9e97-255">toopersist your diagnostics information tooyour Azure Storage account, you must specify a connection string in your service configuration (ServiceConfiguration.cscfg) file.</span></span>

<span data-ttu-id="b9e97-256">Per Azure SDK 2.5, hello Account di archiviazione può essere specificato nel file Diagnostics. wadcfgx hello.</span><span class="sxs-lookup"><span data-stu-id="b9e97-256">For Azure SDK 2.5, hello Storage Account can be specified in hello diagnostics.wadcfgx file.</span></span>

> [!NOTE]
> <span data-ttu-id="b9e97-257">Queste istruzioni si applicano solo tooAzure SDK 2.4 e versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="b9e97-257">These instructions only apply tooAzure SDK 2.4 and below.</span></span> <span data-ttu-id="b9e97-258">Per Azure SDK 2.5, hello Account di archiviazione può essere specificato nel file Diagnostics. wadcfgx hello.</span><span class="sxs-lookup"><span data-stu-id="b9e97-258">For Azure SDK 2.5, hello Storage Account can be specified in hello diagnostics.wadcfgx file.</span></span>
>
>

<span data-ttu-id="b9e97-259">stringhe di connessione tooset hello:</span><span class="sxs-lookup"><span data-stu-id="b9e97-259">tooset hello connection strings:</span></span>

1. <span data-ttu-id="b9e97-260">Aprire il file ServiceConfiguration hello utilizzando l'editor di testo preferito e stringa di connessione hello set per l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b9e97-260">Open hello ServiceConfiguration.Cloud.cscfg file using your favorite text editor and set hello connection string for your storage.</span></span> <span data-ttu-id="b9e97-261">Hello *AccountName* e *AccountKey* i valori sono disponibili in hello portale Azure nel dashboard dell'account di archiviazione hello, in corrispondenza delle chiavi di accesso.</span><span class="sxs-lookup"><span data-stu-id="b9e97-261">hello *AccountName* and *AccountKey* values are found in hello Azure portal in hello storage account dashboard, under Access keys.</span></span>

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. <span data-ttu-id="b9e97-262">Salvare file ServiceConfiguration hello.</span><span class="sxs-lookup"><span data-stu-id="b9e97-262">Save hello ServiceConfiguration.Cloud.cscfg file.</span></span>
3. <span data-ttu-id="b9e97-263">Aprire il file local. cscfg hello e verificare che UseDevelopmentStorage sia impostato tootrue.</span><span class="sxs-lookup"><span data-stu-id="b9e97-263">Open hello ServiceConfiguration.Local.cscfg file and verify that UseDevelopmentStorage is set tootrue.</span></span>

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   <span data-ttu-id="b9e97-264">Ora che sono impostate le stringhe di connessione hello, quando l'applicazione viene distribuita l'applicazione viene mantenuto account di archiviazione tooyour dati di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="b9e97-264">Now that hello connection strings are set, your application will persist diagnostics data tooyour storage account when your application is deployed.</span></span>
4. <span data-ttu-id="b9e97-265">Salvare e compilare il progetto, quindi distribuire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b9e97-265">Save and build your project, then deploy your application.</span></span>

## <a name="step-2-optional-create-custom-performance-counters"></a><span data-ttu-id="b9e97-266">Passaggio 2: (Facoltativo) Creare contatori delle prestazioni personalizzati</span><span class="sxs-lookup"><span data-stu-id="b9e97-266">Step 2: (Optional) Create custom performance counters</span></span>
<span data-ttu-id="b9e97-267">Inoltre toohello predefiniti i contatori delle prestazioni, è possibile aggiungere che i ruoli web o di lavoro toomonitor contatori delle proprie prestazioni personalizzati.</span><span class="sxs-lookup"><span data-stu-id="b9e97-267">In addition toohello pre-defined performance counters, you can add your own custom performance counters toomonitor web or worker roles.</span></span> <span data-ttu-id="b9e97-268">Contatori delle prestazioni personalizzati possono modo utilizzati tootrack e monitoraggio specifici dell'applicazione e può essere creati o eliminati in un'attività di avvio, un ruolo web o un ruolo di lavoro con autorizzazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="b9e97-268">Custom performance counters may be used tootrack and monitor application-specific behavior and can be created or deleted in a startup task, web role, or worker role with elevated permissions.</span></span>

<span data-ttu-id="b9e97-269">agente di diagnostica di Azure Hello Aggiorna hello configurazione contatori di prestazioni dal file con estensione wadcfg hello un minuto dopo l'avvio.</span><span class="sxs-lookup"><span data-stu-id="b9e97-269">hello Azure diagnostics agent refreshes hello performance counter configuration from hello .wadcfg file one minute after starting.</span></span>  <span data-ttu-id="b9e97-270">Se si creano i contatori delle prestazioni personalizzati nel metodo OnStart hello e le attività di avvio richiedono più di un minuto tooexecute, i contatori delle prestazioni personalizzati non è state create quando l'agente diagnostica Azure hello tenta tooload li.</span><span class="sxs-lookup"><span data-stu-id="b9e97-270">If you create custom performance counters in hello OnStart method and your startup tasks take longer than one minute tooexecute, your custom performance counters will not have been created when hello Azure Diagnostics agent tries tooload them.</span></span>  <span data-ttu-id="b9e97-271">In questo scenario Diagnostica di Azure acquisirà correttamente tutti i dati di diagnostica tranne i contatori delle prestazioni personalizzati.</span><span class="sxs-lookup"><span data-stu-id="b9e97-271">In this scenario, you will see that Azure Diagnostics correctly captures all diagnostics data except your custom performance counters.</span></span>  <span data-ttu-id="b9e97-272">tooresolve questo problema, creare hello contatori delle prestazioni in un'attività di avvio o spostare alcune delle attività di avvio funziona metodo OnStart toohello dopo la creazione di contatori delle prestazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="b9e97-272">tooresolve this issue, create hello performance counters in a startup task or move some of your startup task work toohello OnStart method after creating hello performance counters.</span></span>

<span data-ttu-id="b9e97-273">Eseguire i seguenti passaggi toocreate una semplice personalizzata contatore delle prestazioni "\MyCustomCounterCategory\MyButton1Counter" hello:</span><span class="sxs-lookup"><span data-stu-id="b9e97-273">Perform hello following steps toocreate a simple custom performance counter named "\MyCustomCounterCategory\MyButton1Counter":</span></span>

1. <span data-ttu-id="b9e97-274">Aprire hello file di definizione del servizio (CSDEF) per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b9e97-274">Open hello service definition file (CSDEF) for your application.</span></span>
2. <span data-ttu-id="b9e97-275">Aggiungere hello elemento toohello WebRole o WorkerRole elemento tooallow esecuzione con privilegi elevati:</span><span class="sxs-lookup"><span data-stu-id="b9e97-275">Add hello Runtime element toohello WebRole or WorkerRole element tooallow execution with elevated privileges:</span></span>

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. <span data-ttu-id="b9e97-276">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="b9e97-276">Save hello file.</span></span>
4. <span data-ttu-id="b9e97-277">Aprire il file di hello diagnostica (Diagnostics. wadcfg in SDK 2.4 e versioni precedenti o wadcfgx in SDK 2.5 e versioni successive) e aggiungere hello seguente toohello DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="b9e97-277">Open hello diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add hello following toohello DiagnosticMonitorConfiguration</span></span>

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. <span data-ttu-id="b9e97-278">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="b9e97-278">Save hello file.</span></span>
6. <span data-ttu-id="b9e97-279">Creare categoria del contatore delle prestazioni personalizzati hello nel metodo OnStart hello del ruolo, prima di chiamare base. OnStart.</span><span class="sxs-lookup"><span data-stu-id="b9e97-279">Create hello custom performance counter category in hello OnStart method of your role, before invoking base.OnStart.</span></span> <span data-ttu-id="b9e97-280">Hello esempio c# seguente viene creata una categoria personalizzata, se non esiste già:</span><span class="sxs-lookup"><span data-stu-id="b9e97-280">hello following C# example creates a custom category, if it does not already exist:</span></span>

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
7. <span data-ttu-id="b9e97-281">Aggiornare i contatori di hello all'interno dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b9e97-281">Update hello counters within your application.</span></span> <span data-ttu-id="b9e97-282">Hello di esempio seguente aggiorna un contatore delle prestazioni personalizzato in eventi Button1_Click:</span><span class="sxs-lookup"><span data-stu-id="b9e97-282">hello following example updates a custom performance counter on Button1_Click events:</span></span>

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
8. <span data-ttu-id="b9e97-283">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="b9e97-283">Save hello file.</span></span>  

<span data-ttu-id="b9e97-284">I dati dei contatori delle prestazioni personalizzati verranno ora raccolti dal monitor di diagnostica di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b9e97-284">Custom performance counter data will now be collected by hello Azure diagnostics monitor.</span></span>

## <a name="step-3-query-performance-counter-data"></a><span data-ttu-id="b9e97-285">Passaggio 3: Eseguire query sui dati dei contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="b9e97-285">Step 3: Query performance counter data</span></span>
<span data-ttu-id="b9e97-286">Dopo l'applicazione viene distribuita e in esecuzione, il monitor di diagnostica hello inizierà a raccogliere i contatori delle prestazioni e che tooAzure l'archiviazione dei dati di persistenza.</span><span class="sxs-lookup"><span data-stu-id="b9e97-286">Once your application is deployed and running, hello Diagnostics monitor will begin collecting performance counters and persisting that data tooAzure storage.</span></span> <span data-ttu-id="b9e97-287">Utilizzare gli strumenti, ad esempio Esplora Server in Visual Studio, [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), o [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) di Cerebrata in hello dati dei contatori delle prestazioni di hello tooview Tabella WADPerformanceCountersTable.</span><span class="sxs-lookup"><span data-stu-id="b9e97-287">You use tools such as Server Explorer in Visual Studio,  [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), or [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) by Cerebrata tooview hello performance counters data in hello WADPerformanceCountersTable table.</span></span> <span data-ttu-id="b9e97-288">È possibile eseguire una query anche a livello di codice hello tabella servizio tramite [c#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), o [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span><span class="sxs-lookup"><span data-stu-id="b9e97-288">You can also programmatically query hello Table service using [C#](../cosmos-db/table-storage-how-to-use-dotnet.md),  [Java](../cosmos-db/table-storage-how-to-use-java.md),  [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), or [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span></span>

<span data-ttu-id="b9e97-289">Hello esempio c# seguente viene illustrata una query di base sulla tabella WADPerformanceCountersTable hello e Salva il file CSV tooa di hello diagnostica dei dati.</span><span class="sxs-lookup"><span data-stu-id="b9e97-289">hello following C# example shows a basic query against hello WADPerformanceCountersTable table and saves hello diagnostics data tooa CSV file.</span></span> <span data-ttu-id="b9e97-290">Dopo che i contatori delle prestazioni di hello vengono salvati i file CSV tooa, è possibile utilizzare le funzionalità di Microsoft Excel o alcuni altri dati hello toovisualize dello strumento di creazione di grafi hello.</span><span class="sxs-lookup"><span data-stu-id="b9e97-290">Once hello performance counters are saved tooa CSV file, you can use hello graphing capabilities in Microsoft Excel or some other tool toovisualize hello data.</span></span> <span data-ttu-id="b9e97-291">Impossibile verificare tooadd tooMicrosoft.WindowsAzure.Storage.dll un riferimento, incluso in hello Azure SDK per .NET ottobre 2012 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="b9e97-291">Be sure tooadd a reference tooMicrosoft.WindowsAzure.Storage.dll, which is included in hello Azure SDK for .NET October 2012 and later.</span></span> <span data-ttu-id="b9e97-292">assembly Hello è installato toohello % programma Files%\Microsoft SDKs\Microsoft Azure.NET sdk\version-num\ref\. directory.</span><span class="sxs-lookup"><span data-stu-id="b9e97-292">hello assembly is installed toohello %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ directory.</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get hello connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using hello Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use hello CloudConfigurationManager type
// tooretrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store hello connection string in your web.config or app.config file.
// Use hello ConfigurationManager type tooretrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference toohello storage account using hello connection string.  You can also use hello development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create hello table query, filter on a specific CounterName, DeploymentId and RoleInstance.
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

// Execute hello table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process hello query results and build a CSV file.
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

<span data-ttu-id="b9e97-293">Eseguire il mapping di entità tooC # oggetti usando una classe personalizzata derivata da **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="b9e97-293">Entities map tooC# objects using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="b9e97-294">il codice seguente Hello definisce una classe di entità che rappresenta un contatore delle prestazioni in hello **WADPerformanceCountersTable** tabella.</span><span class="sxs-lookup"><span data-stu-id="b9e97-294">hello following code defines an entity class that represents a performance counter in hello **WADPerformanceCountersTable** table.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b9e97-295">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b9e97-295">Next Steps</span></span>
[<span data-ttu-id="b9e97-296">Visualizzare altri articoli sulla diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="b9e97-296">View additional articles on Azure Diagnostics</span></span>](../azure-diagnostics.md)
