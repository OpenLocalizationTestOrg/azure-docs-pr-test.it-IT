---
title: Soluzione Wire Data in Log Analytics | Documentazione Microsoft
description: I dati in transito sono dati consolidati di rete e sulle prestazioni provenienti da computer con agenti OMS, inclusi Operations Manager e gli agenti connessi a Windows. I dati di rete vengono combinati con i dati dei log per poter correlare i dati.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: fc3d7127-0baa-4772-858a-5ba995d1519b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: banders
ms.openlocfilehash: eb8ae80f91b9ecad666ab7a2257d99e5669f5b88
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="wire-data-20-preview-solution-in-log-analytics"></a><span data-ttu-id="883ab-104">Soluzione Wire Data 2.0 (anteprima) in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="883ab-104">Wire Data 2.0 (Preview) solution in Log Analytics</span></span>

![Simbolo di Wire Data](./media/log-analytics-wire-data/wire-data2-symbol.png)

<span data-ttu-id="883ab-106">I dati in transito sono dati di rete e sulle prestazioni consolidati provenienti da computer con agenti OMS, tra cui agenti Operations Manager, connessi a Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="883ab-106">Wire data is consolidated network and performance data from computers with OMS agents, including Operations Manager, Windows-connected, and Linux agents.</span></span> <span data-ttu-id="883ab-107">I dati di rete vengono combinati con altri dati di log per consentire la correlazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="883ab-107">Network data is combined with your other log data to help you correlate data.</span></span>

<span data-ttu-id="883ab-108">Oltre agli agenti OMS, la soluzione Wire Data usa le istanze di Microsoft Dependency Agent installate nell'infrastruttura IT.</span><span class="sxs-lookup"><span data-stu-id="883ab-108">In addition to OMS agents, the Wire Data solution uses Microsoft Dependency agents that you install on computers in your IT infrastructure.</span></span> <span data-ttu-id="883ab-109">Le istanze di Dependency Agent monitorano i dati di rete inviati da e verso i computer per i livelli di rete 2-3 del [modello OSI](https://en.wikipedia.org/wiki/OSI_model), che includono le diverse porte e i vari protocolli usati.</span><span class="sxs-lookup"><span data-stu-id="883ab-109">Dependency Agents monitor network data sent to and from your computers for network levels 2-3 in the [OSI model](https://en.wikipedia.org/wiki/OSI_model), including the various protocols and ports used.</span></span> <span data-ttu-id="883ab-110">I dati vengono quindi inviati a Log Analytics usando gli agenti.</span><span class="sxs-lookup"><span data-stu-id="883ab-110">Data is then sent to Log Analytics using agents.</span></span>

> [!NOTE]
> <span data-ttu-id="883ab-111">Non è possibile aggiungere la versione precedente della soluzione Wire Data a nuove aree di lavoro.</span><span class="sxs-lookup"><span data-stu-id="883ab-111">You cannot add the previous version of the Wire Data solution to new workspaces.</span></span> <span data-ttu-id="883ab-112">Se è stata abilitata la soluzione Wire Data originale, è possibile continuare a usarla.</span><span class="sxs-lookup"><span data-stu-id="883ab-112">If you have the original Wire Data solution enabled, you can continue to use it.</span></span> <span data-ttu-id="883ab-113">Per usare Wire Data 2.0, tuttavia, è prima necessario rimuovere la versione originale.</span><span class="sxs-lookup"><span data-stu-id="883ab-113">However, to use Wire Data 2.0, you must first remove the original version.</span></span>

<span data-ttu-id="883ab-114">Per impostazione predefinita, Log Analytics raccoglie i dati registrati sulle prestazioni di CPU, memoria, dischi e rete dai contatori integrati in Windows.</span><span class="sxs-lookup"><span data-stu-id="883ab-114">By default, Log Analytics collects logged data for CPU, memory, disk, and network performance data from counters built into Windows.</span></span> <span data-ttu-id="883ab-115">La raccolta dei dati di rete e di altro tipo viene eseguita in tempo reale per ogni agente, inclusi subnet e protocolli a livello di applicazione usati dal computer.</span><span class="sxs-lookup"><span data-stu-id="883ab-115">Network and other data collection is done in real-time for each agent, including subnets and application-level protocols being used by the computer.</span></span> <span data-ttu-id="883ab-116">È possibile aggiungere altri contatori delle prestazioni nella pagina Settings della scheda Logs.</span><span class="sxs-lookup"><span data-stu-id="883ab-116">You can add other performance counters on the Settings page on the Logs tab.</span></span>

<span data-ttu-id="883ab-117">Se si è usato [sFlow](http://www.sflow.org/) o un altro software con il [protocollo NetFlow di Cisco](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), le statistiche e i dati visualizzati dai dati in transito risulteranno familiari.</span><span class="sxs-lookup"><span data-stu-id="883ab-117">If you've used [sFlow](http://www.sflow.org/) or other software with [Cisco's NetFlow protocol](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), then the statistics and data you see from wire data will be familiar to you.</span></span>

<span data-ttu-id="883ab-118">Alcuni tipi di query di ricerca nei log predefinite includono:</span><span class="sxs-lookup"><span data-stu-id="883ab-118">Some of the types of built-in Log search queries include:</span></span>

- <span data-ttu-id="883ab-119">Agenti che forniscono dati in transito</span><span class="sxs-lookup"><span data-stu-id="883ab-119">Agents that provide wire data</span></span>
- <span data-ttu-id="883ab-120">Indirizzo IP degli agenti che forniscono dati in transito</span><span class="sxs-lookup"><span data-stu-id="883ab-120">IP address of agents providing wire data</span></span>
- <span data-ttu-id="883ab-121">Comunicazioni in uscita da parte degli indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="883ab-121">Outbound communications by IP addresses</span></span>
- <span data-ttu-id="883ab-122">Numero di byte inviati dai protocolli applicativi</span><span class="sxs-lookup"><span data-stu-id="883ab-122">Number of bytes sent by application protocols</span></span>
- <span data-ttu-id="883ab-123">Numero di byte inviati da un servizio dell’applicazione</span><span class="sxs-lookup"><span data-stu-id="883ab-123">Number of bytes sent by an application service</span></span>
- <span data-ttu-id="883ab-124">Byte ricevuti da protocolli diversi</span><span class="sxs-lookup"><span data-stu-id="883ab-124">Bytes received by different protocols</span></span>
- <span data-ttu-id="883ab-125">Byte totali inviati e ricevuti per versione IP</span><span class="sxs-lookup"><span data-stu-id="883ab-125">Total bytes sent and received by IP version</span></span>
- <span data-ttu-id="883ab-126">Latenza media per le connessioni misurate in modo affidabile</span><span class="sxs-lookup"><span data-stu-id="883ab-126">Average latency for connections that were measured reliably</span></span>
- <span data-ttu-id="883ab-127">Processi dei computer che hanno avviato o ricevuto traffico di rete</span><span class="sxs-lookup"><span data-stu-id="883ab-127">Computer processes that initiated or received network traffic</span></span>
- <span data-ttu-id="883ab-128">Quantità di traffico di rete per un processo</span><span class="sxs-lookup"><span data-stu-id="883ab-128">Amount of network traffic for a process</span></span>

<span data-ttu-id="883ab-129">Quando si esegue una ricerca usando i dati in transito, è possibile filtrare e raggruppare i dati per visualizzare le informazioni su agenti e protocolli principali.</span><span class="sxs-lookup"><span data-stu-id="883ab-129">When you search using wire data, you can filter and group data to view information about the top agents and top protocols.</span></span> <span data-ttu-id="883ab-130">In alternativa, è possibile visualizzare quando determinati computer (indirizzi IP/indirizzi MAC) hanno comunicato tra loro, per quanto tempo e quanti dati sono stati inviati, visualizzando essenzialmente metadati relativi al traffico di rete basati sulla ricerca.</span><span class="sxs-lookup"><span data-stu-id="883ab-130">Or you can view when certain computers (IP addresses/MAC addresses) communicated with each other, for how long, and how much data was sent—basically, you view metadata about network traffic, which is search-based.</span></span>

<span data-ttu-id="883ab-131">La visualizzazione di metadati, tuttavia, non è necessariamente utile per una risoluzione dei problemi approfondita.</span><span class="sxs-lookup"><span data-stu-id="883ab-131">However, since you're viewing metadata, it's not necessarily useful for in-depth troubleshooting.</span></span> <span data-ttu-id="883ab-132">I dati in transito in Log Analytics non sono un'acquisizione completa dei dati di rete</span><span class="sxs-lookup"><span data-stu-id="883ab-132">Wire data in Log Analytics is not a full capture of network data.</span></span> <span data-ttu-id="883ab-133">e non sono quindi destinati a una risoluzione dei problemi approfondita a livello di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="883ab-133">So, it's not intended for deep packet-level troubleshooting.</span></span> <span data-ttu-id="883ab-134">Il vantaggio di usare l'agente, rispetto ad altri metodi di raccolta, è che non è necessario installare appliance, riconfigurare i commutatori di rete o eseguire configurazioni complesse.</span><span class="sxs-lookup"><span data-stu-id="883ab-134">The advantage of using the agent, compared to other collection methods, is that you don't have to install appliances, reconfigure your network switches, or preform complicated configurations.</span></span> <span data-ttu-id="883ab-135">I dati in transito sono basati semplicemente sull'agente, che viene installato in un computer e monitora il proprio traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="883ab-135">Wire data is simply agent-based—you install the agent on a computer and it will monitor its own network traffic.</span></span> <span data-ttu-id="883ab-136">Un altro vantaggio si riscontra quando si vogliono monitorare carichi di lavoro in esecuzione in provider di servizi cloud, provider di servizi di hosting o Microsoft Azure, in cui l'utente non è proprietario del livello infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="883ab-136">Another advantage is when you want to monitor workloads running in cloud providers or hosting service provider or Microsoft Azure, where the user doesn't own the fabric layer.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="883ab-137">Origini connesse</span><span class="sxs-lookup"><span data-stu-id="883ab-137">Connected sources</span></span>

<span data-ttu-id="883ab-138">Wire Data ottiene i dati da Microsoft Dependency Agent.</span><span class="sxs-lookup"><span data-stu-id="883ab-138">Wire Data gets its data from the Microsoft Dependency Agent.</span></span> <span data-ttu-id="883ab-139">Dependency Agent dipende dall'agente OMS per le connessioni a Log Analytics,</span><span class="sxs-lookup"><span data-stu-id="883ab-139">The Dependency Agent depends on the OMS Agent for its connections to Log Analytics.</span></span> <span data-ttu-id="883ab-140">quindi prima di installare Dependency Agent è necessario che in un server sia installato e configurato l'agente OMS.</span><span class="sxs-lookup"><span data-stu-id="883ab-140">This means that a server must have the OMS Agent installed and configured first, and then you install the Dependency Agent.</span></span> <span data-ttu-id="883ab-141">La tabella seguente descrive le origini connesse supportate dalla soluzione Wire Data.</span><span class="sxs-lookup"><span data-stu-id="883ab-141">The following table describes the connected sources that the Wire Data solution supports.</span></span>

| <span data-ttu-id="883ab-142">**Origine connessa**</span><span class="sxs-lookup"><span data-stu-id="883ab-142">**Connected source**</span></span> | <span data-ttu-id="883ab-143">**Supportato**</span><span class="sxs-lookup"><span data-stu-id="883ab-143">**Supported**</span></span> | <span data-ttu-id="883ab-144">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="883ab-144">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="883ab-145">Agenti di Windows</span><span class="sxs-lookup"><span data-stu-id="883ab-145">Windows agents</span></span> | <span data-ttu-id="883ab-146">Sì</span><span class="sxs-lookup"><span data-stu-id="883ab-146">Yes</span></span> | <span data-ttu-id="883ab-147">Wire Data analizza e raccoglie i dati da computer agente Windows.</span><span class="sxs-lookup"><span data-stu-id="883ab-147">Wire Data analyzes and collects data from Windows agent computers.</span></span> <br><br> <span data-ttu-id="883ab-148">Oltre a [OMS Agent](log-analytics-windows-agents.md), gli agenti Windows richiedono Microsoft Dependency Agent.</span><span class="sxs-lookup"><span data-stu-id="883ab-148">In addition to the [OMS Agent](log-analytics-windows-agents.md), Windows agents require the Microsoft Dependency Agent.</span></span> <span data-ttu-id="883ab-149">Per un elenco completo delle versioni del sistema operativo, vedere [Sistemi operativi supportati](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems).</span><span class="sxs-lookup"><span data-stu-id="883ab-149">See the [supported operating systems](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="883ab-150">Agenti Linux</span><span class="sxs-lookup"><span data-stu-id="883ab-150">Linux agents</span></span> | <span data-ttu-id="883ab-151">Sì</span><span class="sxs-lookup"><span data-stu-id="883ab-151">Yes</span></span> | <span data-ttu-id="883ab-152">Wire Data analizza e raccoglie i dati da computer agente Linux.</span><span class="sxs-lookup"><span data-stu-id="883ab-152">Wire Data analyzes and collects data from Linux agent computers.</span></span><br><br> <span data-ttu-id="883ab-153">Oltre a [OMS Agent](log-analytics-linux-agents.md), gli agenti Linux richiedono Microsoft Dependency Agent.</span><span class="sxs-lookup"><span data-stu-id="883ab-153">In addition to the [OMS Agent](log-analytics-linux-agents.md), Linux agents require the Microsoft Dependency Agent.</span></span> <span data-ttu-id="883ab-154">Per un elenco completo delle versioni del sistema operativo, vedere [Sistemi operativi supportati](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems).</span><span class="sxs-lookup"><span data-stu-id="883ab-154">See the [supported operating systems](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="883ab-155">Gruppo di gestione di System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="883ab-155">System Center Operations Manager management group</span></span> | <span data-ttu-id="883ab-156">Sì</span><span class="sxs-lookup"><span data-stu-id="883ab-156">Yes</span></span> | <span data-ttu-id="883ab-157">Wire Data analizza e raccoglie i dati dagli agenti Windows e Linux in un [gruppo di gestione di System Center Operations Manager](log-analytics-om-agents.md) connesso.</span><span class="sxs-lookup"><span data-stu-id="883ab-157">Wire Data analyzes and collects data from Windows and Linux agents in a connected [System Center Operations Manager management group](log-analytics-om-agents.md).</span></span> <br><br> <span data-ttu-id="883ab-158">È necessaria una connessione diretta dal computer agente System Center Operations Manager a Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="883ab-158">A direct connection from the System Center Operations Manager agent computer to Log Analytics is required.</span></span> <span data-ttu-id="883ab-159">I dati vengono inoltrati dal gruppo di gestione a Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="883ab-159">Data is forwarded from the management group to Log Analytics.</span></span> |
| <span data-ttu-id="883ab-160">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="883ab-160">Azure storage account</span></span> | <span data-ttu-id="883ab-161">No</span><span class="sxs-lookup"><span data-stu-id="883ab-161">No</span></span> | <span data-ttu-id="883ab-162">Wire Data raccoglie i dati dai computer agente, quindi non devono essere raccolti dati da Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="883ab-162">Wire Data collects data from agent computers, so there is no data from it to collect from Azure Storage.</span></span> |

<span data-ttu-id="883ab-163">In Windows, Microsoft Monitoring Agent (MMA) viene usato sia da System Center Operations Manager che da Log Analytics per raccogliere e inviare dati.</span><span class="sxs-lookup"><span data-stu-id="883ab-163">On Windows, the Microsoft Monitoring Agent (MMA) is used by both System Center Operations Manager and Log Analytics to gather and send data.</span></span> <span data-ttu-id="883ab-164">A seconda del contesto, l'agente viene chiamato agente System Center Operations Manager, agente OMS, agente Log Analytics, agente MMA o agente diretto.</span><span class="sxs-lookup"><span data-stu-id="883ab-164">Depending on the context, the agent is called the System Center Operations Manager Agent, OMS Agent, Log Analytics Agent, MMA, or Direct Agent.</span></span> <span data-ttu-id="883ab-165">System Center Operations Manager e Log Analytics offrono versioni leggermente diverse dell'agente MMA.</span><span class="sxs-lookup"><span data-stu-id="883ab-165">System Center Operations Manager and Log Analytics provide slightly different versions of the MMA.</span></span> <span data-ttu-id="883ab-166">Ognuna di queste versioni può inviare segnalazioni a System Center Operations Manager, Log Analytics o entrambi.</span><span class="sxs-lookup"><span data-stu-id="883ab-166">These versions can each report to System Center Operations Manager, to Log Analytics, or to both.</span></span>

<span data-ttu-id="883ab-167">In Linux, l'agente OMS per Linux raccoglie e invia i dati a Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="883ab-167">On Linux, the OMS Agent for Linux gathers and sends data to Log Analytics.</span></span> <span data-ttu-id="883ab-168">È possibile usare Wire Data in server con agenti OMS diretti o in server collegati a Log Analytics tramite gruppi di gestione di System Center Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="883ab-168">You can use Wire Data on servers with OMS Direct Agents or on servers that are attached to Log Analytics via System Center Operations Manager management groups.</span></span>

<span data-ttu-id="883ab-169">In questo articolo, il termine _agente OMS_ viene usato per fare riferimento a tutti gli agenti, sia Linux che Windows e sia connessi a un gruppo di gestione di System Center Operations Manager che direttamente a Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="883ab-169">In this article, references to all agents, whether Linux or Windows, whether connected to a System Center Operations Manager management group or directly to Log Analytics are termed the _OMS agent_.</span></span> <span data-ttu-id="883ab-170">Il nome della distribuzione specifica dell'agente verrà usato solo se necessario per il contesto.</span><span class="sxs-lookup"><span data-stu-id="883ab-170">We'll use the specific deployment name of the agent only if it's needed for context.</span></span>

<span data-ttu-id="883ab-171">L'istanza di Dependency Agent non trasmette dati e non richiede modifiche ai firewall o alle porte.</span><span class="sxs-lookup"><span data-stu-id="883ab-171">The Dependency Agent does not transmit any data itself, and it does not require any changes to firewalls or ports.</span></span> <span data-ttu-id="883ab-172">I dati in Wire Data vengono sempre trasmessi dall'agente OMS a Log Analytics, direttamente o con il gateway OMS.</span><span class="sxs-lookup"><span data-stu-id="883ab-172">The data in Wire Data is always transmitted by the OMS agent to Log Analytics, either directly or using the OMS Gateway.</span></span>

![Diagramma degli agenti](./media/log-analytics-wire-data/agents.png)

<span data-ttu-id="883ab-174">Per un utente di System Center Operations Manager con un gruppo di gestione connesso a Log Analytics:</span><span class="sxs-lookup"><span data-stu-id="883ab-174">If you are a System Center Operations Manager user with a management group connected to Log Analytics:</span></span>

- <span data-ttu-id="883ab-175">Non è necessaria alcuna configurazione aggiuntiva se gli agenti System Center Operations Manager possono accedere a Internet per connettersi a Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="883ab-175">No additional configuration is required when your System Center Operations Manager agents can access the Internet to connect to Log Analytics.</span></span>
- <span data-ttu-id="883ab-176">È necessario configurare il gateway OMS in modo da usare System Center Operations Manager quando gli agenti System Center Operations Manager non possono connettersi a Log Analytics tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="883ab-176">You need to configure the OMS Gateway to work with System Center Operations Manager when your System Center Operations Manager agents cannot access Log Analytics over the Internet.</span></span>

<span data-ttu-id="883ab-177">Se si usa l'agente diretto, è necessario configurare l'agente OMS in modo che si connetta a Log Analytics o al gateway OMS.</span><span class="sxs-lookup"><span data-stu-id="883ab-177">If you are using the Direct Agent, you need to configure the OMS agent itself to connect to Log Analytics or to your OMS Gateway.</span></span> <span data-ttu-id="883ab-178">È possibile scaricare il gateway OMS dall'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=52666).</span><span class="sxs-lookup"><span data-stu-id="883ab-178">You can download the OMS Gateway from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="883ab-179">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="883ab-179">Prerequisites</span></span>

- <span data-ttu-id="883ab-180">È necessaria la soluzione [Insight & Analytics](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) offerta.</span><span class="sxs-lookup"><span data-stu-id="883ab-180">Requires the [Insight and Analytics](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) solution offer.</span></span>
- <span data-ttu-id="883ab-181">Se si usa la versione precedente della soluzione Wire Data, prima di tutto è necessario rimuoverla.</span><span class="sxs-lookup"><span data-stu-id="883ab-181">If you're using the previous version of the Wire Data solution, you must first remove it.</span></span> <span data-ttu-id="883ab-182">Tutti i dati acquisiti tramite la soluzione Wire Data originale, tuttavia, saranno ancora disponibili in Wire Data 2.0 e nella ricerca log.</span><span class="sxs-lookup"><span data-stu-id="883ab-182">However, all data captured through the original Wire Data solution is still available in Wire Data 2.0 and log search.</span></span>
- <span data-ttu-id="883ab-183">Per installare o disinstallare Dependency Agent sono necessari privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="883ab-183">Administrator privileges are required to install or uninstall the Dependency Agent.</span></span>
- <span data-ttu-id="883ab-184">Dependency Agent deve essere installato in un computer con un sistema operativo a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="883ab-184">The Dependency Agent must be installed on a computer with a 64-bit operating system.</span></span>

### <a name="operating-systems"></a><span data-ttu-id="883ab-185">Sistemi operativi</span><span class="sxs-lookup"><span data-stu-id="883ab-185">Operating systems</span></span>

<span data-ttu-id="883ab-186">Le sezioni seguenti elencano i sistemi operativi supportati per l'agente di dipendenza.</span><span class="sxs-lookup"><span data-stu-id="883ab-186">The following sections list the supported operating systems for the Dependency Agent.</span></span> <span data-ttu-id="883ab-187">Wire Data non supporta architetture a 32 bit per i sistemi operativi.</span><span class="sxs-lookup"><span data-stu-id="883ab-187">Wire Data doesn't support 32-bit architectures for any operating system.</span></span>

#### <a name="windows-server"></a><span data-ttu-id="883ab-188">Windows Server</span><span class="sxs-lookup"><span data-stu-id="883ab-188">Windows Server</span></span>

- <span data-ttu-id="883ab-189">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="883ab-189">Windows Server 2016</span></span>
- <span data-ttu-id="883ab-190">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="883ab-190">Windows Server 2012 R2</span></span>
- <span data-ttu-id="883ab-191">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="883ab-191">Windows Server 2012</span></span>
- <span data-ttu-id="883ab-192">Windows Server 2008 R2 SP1,</span><span class="sxs-lookup"><span data-stu-id="883ab-192">Windows Server 2008 R2 SP1</span></span>

#### <a name="windows-desktop"></a><span data-ttu-id="883ab-193">Desktop di Windows</span><span class="sxs-lookup"><span data-stu-id="883ab-193">Windows desktop</span></span>

- <span data-ttu-id="883ab-194">Windows 10</span><span class="sxs-lookup"><span data-stu-id="883ab-194">Windows 10</span></span>
- <span data-ttu-id="883ab-195">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="883ab-195">Windows 8.1</span></span>
- <span data-ttu-id="883ab-196">Windows 8</span><span class="sxs-lookup"><span data-stu-id="883ab-196">Windows 8</span></span>
- <span data-ttu-id="883ab-197">Windows 7</span><span class="sxs-lookup"><span data-stu-id="883ab-197">Windows 7</span></span>

#### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a><span data-ttu-id="883ab-198">Red Hat Enterprise Linux, CentOS Linux e Oracle Linux (con il kernel RHEL)</span><span class="sxs-lookup"><span data-stu-id="883ab-198">Red Hat Enterprise Linux, CentOS Linux, and Oracle Linux (with RHEL Kernel)</span></span>

- <span data-ttu-id="883ab-199">Sono supportate solo versioni predefinita e SMP del kernel Linux.</span><span class="sxs-lookup"><span data-stu-id="883ab-199">Only default and SMP Linux kernel releases are supported.</span></span>
- <span data-ttu-id="883ab-200">Le versioni del kernel non standard, ad esempio PAE e Xen, non sono supportate per le distribuzioni Linux.</span><span class="sxs-lookup"><span data-stu-id="883ab-200">Nonstandard kernel releases, such as PAE and Xen, are not supported for any Linux distribution.</span></span> <span data-ttu-id="883ab-201">Un sistema con stringa di versione _2.6.16.21-0.8-xen_, ad esempio, non è supportato.</span><span class="sxs-lookup"><span data-stu-id="883ab-201">For example, a system with the release string of _2.6.16.21-0.8-xen_ is not supported.</span></span>
- <span data-ttu-id="883ab-202">I kernel personalizzati, tra cui le ricompilazioni dei kernel standard, non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="883ab-202">Custom kernels, including recompiles of standard kernels, are not supported.</span></span>
- <span data-ttu-id="883ab-203">Il kernel CentOSPlus non è supportato.</span><span class="sxs-lookup"><span data-stu-id="883ab-203">CentOSPlus kernel is not supported.</span></span>
- <span data-ttu-id="883ab-204">Unbreakable Enterprise Kernel (UEK) di Oracle è illustrato in una sezione successiva di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="883ab-204">Oracle Unbreakable Enterprise Kernel (UEK) is covered in a later section of this article.</span></span>

#### <a name="red-hat-linux-7"></a><span data-ttu-id="883ab-205">Red Hat Linux 7</span><span class="sxs-lookup"><span data-stu-id="883ab-205">Red Hat Linux 7</span></span>

| <span data-ttu-id="883ab-206">**Versione del sistema operativo**</span><span class="sxs-lookup"><span data-stu-id="883ab-206">**OS version**</span></span> | <span data-ttu-id="883ab-207">**Versione del kernel**</span><span class="sxs-lookup"><span data-stu-id="883ab-207">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="883ab-208">7.0</span><span class="sxs-lookup"><span data-stu-id="883ab-208">7.0</span></span> | <span data-ttu-id="883ab-209">3.10.0-123</span><span class="sxs-lookup"><span data-stu-id="883ab-209">3.10.0-123</span></span> |
| <span data-ttu-id="883ab-210">7.1</span><span class="sxs-lookup"><span data-stu-id="883ab-210">7.1</span></span> | <span data-ttu-id="883ab-211">3.10.0-229</span><span class="sxs-lookup"><span data-stu-id="883ab-211">3.10.0-229</span></span> |
| <span data-ttu-id="883ab-212">7,2</span><span class="sxs-lookup"><span data-stu-id="883ab-212">7.2</span></span> | <span data-ttu-id="883ab-213">3.10.0-327</span><span class="sxs-lookup"><span data-stu-id="883ab-213">3.10.0-327</span></span> |
| <span data-ttu-id="883ab-214">7.3</span><span class="sxs-lookup"><span data-stu-id="883ab-214">7.3</span></span> | <span data-ttu-id="883ab-215">3.10.0-514</span><span class="sxs-lookup"><span data-stu-id="883ab-215">3.10.0-514</span></span> |

#### <a name="red-hat-linux-6"></a><span data-ttu-id="883ab-216">Red Hat Linux 6</span><span class="sxs-lookup"><span data-stu-id="883ab-216">Red Hat Linux 6</span></span>

| <span data-ttu-id="883ab-217">**Versione del sistema operativo**</span><span class="sxs-lookup"><span data-stu-id="883ab-217">**OS version**</span></span> | <span data-ttu-id="883ab-218">**Versione del kernel**</span><span class="sxs-lookup"><span data-stu-id="883ab-218">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="883ab-219">6.0</span><span class="sxs-lookup"><span data-stu-id="883ab-219">6.0</span></span> | <span data-ttu-id="883ab-220">2.6.32-71</span><span class="sxs-lookup"><span data-stu-id="883ab-220">2.6.32-71</span></span> |
| <span data-ttu-id="883ab-221">6.1</span><span class="sxs-lookup"><span data-stu-id="883ab-221">6.1</span></span> | <span data-ttu-id="883ab-222">2.6.32-131</span><span class="sxs-lookup"><span data-stu-id="883ab-222">2.6.32-131</span></span> |
| <span data-ttu-id="883ab-223">6.2</span><span class="sxs-lookup"><span data-stu-id="883ab-223">6.2</span></span> | <span data-ttu-id="883ab-224">2.6.32-220</span><span class="sxs-lookup"><span data-stu-id="883ab-224">2.6.32-220</span></span> |
| <span data-ttu-id="883ab-225">6.3</span><span class="sxs-lookup"><span data-stu-id="883ab-225">6.3</span></span> | <span data-ttu-id="883ab-226">2.6.32-279</span><span class="sxs-lookup"><span data-stu-id="883ab-226">2.6.32-279</span></span> |
| <span data-ttu-id="883ab-227">6.4</span><span class="sxs-lookup"><span data-stu-id="883ab-227">6.4</span></span> | <span data-ttu-id="883ab-228">2.6.32-358</span><span class="sxs-lookup"><span data-stu-id="883ab-228">2.6.32-358</span></span> |
| <span data-ttu-id="883ab-229">6,5</span><span class="sxs-lookup"><span data-stu-id="883ab-229">6.5</span></span> | <span data-ttu-id="883ab-230">2.6.32-431</span><span class="sxs-lookup"><span data-stu-id="883ab-230">2.6.32-431</span></span> |
| <span data-ttu-id="883ab-231">6.6</span><span class="sxs-lookup"><span data-stu-id="883ab-231">6.6</span></span> | <span data-ttu-id="883ab-232">2.6.32-504</span><span class="sxs-lookup"><span data-stu-id="883ab-232">2.6.32-504</span></span> |
| <span data-ttu-id="883ab-233">6.7</span><span class="sxs-lookup"><span data-stu-id="883ab-233">6.7</span></span> | <span data-ttu-id="883ab-234">2.6.32-573</span><span class="sxs-lookup"><span data-stu-id="883ab-234">2.6.32-573</span></span> |
| <span data-ttu-id="883ab-235">6.8</span><span class="sxs-lookup"><span data-stu-id="883ab-235">6.8</span></span> | <span data-ttu-id="883ab-236">2.6.32-642</span><span class="sxs-lookup"><span data-stu-id="883ab-236">2.6.32-642</span></span> |

#### <a name="red-hat-linux-5"></a><span data-ttu-id="883ab-237">Red Hat Linux 5</span><span class="sxs-lookup"><span data-stu-id="883ab-237">Red Hat Linux 5</span></span>

| <span data-ttu-id="883ab-238">**Versione del sistema operativo**</span><span class="sxs-lookup"><span data-stu-id="883ab-238">**OS version**</span></span> | <span data-ttu-id="883ab-239">**Versione del kernel**</span><span class="sxs-lookup"><span data-stu-id="883ab-239">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="883ab-240">5.8</span><span class="sxs-lookup"><span data-stu-id="883ab-240">5.8</span></span> | <span data-ttu-id="883ab-241">2.6.18-308</span><span class="sxs-lookup"><span data-stu-id="883ab-241">2.6.18-308</span></span> |
| <span data-ttu-id="883ab-242">5.9</span><span class="sxs-lookup"><span data-stu-id="883ab-242">5.9</span></span> | <span data-ttu-id="883ab-243">2.6.18-348</span><span class="sxs-lookup"><span data-stu-id="883ab-243">2.6.18-348</span></span> |
| <span data-ttu-id="883ab-244">5.10</span><span class="sxs-lookup"><span data-stu-id="883ab-244">5.10</span></span> | <span data-ttu-id="883ab-245">2.6.18-371</span><span class="sxs-lookup"><span data-stu-id="883ab-245">2.6.18-371</span></span> |
| <span data-ttu-id="883ab-246">5.11</span><span class="sxs-lookup"><span data-stu-id="883ab-246">5.11</span></span> | <span data-ttu-id="883ab-247">2.6.18-398</span><span class="sxs-lookup"><span data-stu-id="883ab-247">2.6.18-398</span></span> <br> <span data-ttu-id="883ab-248">2.6.18-400</span><span class="sxs-lookup"><span data-stu-id="883ab-248">2.6.18-400</span></span> <br><span data-ttu-id="883ab-249">2.6.18-402</span><span class="sxs-lookup"><span data-stu-id="883ab-249">2.6.18-402</span></span> <br><span data-ttu-id="883ab-250">2.6.18-404</span><span class="sxs-lookup"><span data-stu-id="883ab-250">2.6.18-404</span></span> <br><span data-ttu-id="883ab-251">2.6.18-406</span><span class="sxs-lookup"><span data-stu-id="883ab-251">2.6.18-406</span></span> <br> <span data-ttu-id="883ab-252">2.6.18-407</span><span class="sxs-lookup"><span data-stu-id="883ab-252">2.6.18-407</span></span> <br> <span data-ttu-id="883ab-253">2.6.18-408</span><span class="sxs-lookup"><span data-stu-id="883ab-253">2.6.18-408</span></span> <br> <span data-ttu-id="883ab-254">2.6.18-409</span><span class="sxs-lookup"><span data-stu-id="883ab-254">2.6.18-409</span></span> <br> <span data-ttu-id="883ab-255">2.6.18-410</span><span class="sxs-lookup"><span data-stu-id="883ab-255">2.6.18-410</span></span> <br> <span data-ttu-id="883ab-256">2.6.18-411</span><span class="sxs-lookup"><span data-stu-id="883ab-256">2.6.18-411</span></span> <br> <span data-ttu-id="883ab-257">2.6.18-412</span><span class="sxs-lookup"><span data-stu-id="883ab-257">2.6.18-412</span></span> <br> <span data-ttu-id="883ab-258">2.6.18-416</span><span class="sxs-lookup"><span data-stu-id="883ab-258">2.6.18-416</span></span> <br> <span data-ttu-id="883ab-259">2.6.18-417</span><span class="sxs-lookup"><span data-stu-id="883ab-259">2.6.18-417</span></span> <br> <span data-ttu-id="883ab-260">2.6.18-419</span><span class="sxs-lookup"><span data-stu-id="883ab-260">2.6.18-419</span></span> |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a><span data-ttu-id="883ab-261">Oracle Enterprise Linux con Unbreakable Enterprise Kernel</span><span class="sxs-lookup"><span data-stu-id="883ab-261">Oracle Enterprise Linux with Unbreakable Enterprise Kernel</span></span>

#### <a name="oracle-linux-6"></a><span data-ttu-id="883ab-262">Oracle Linux 6</span><span class="sxs-lookup"><span data-stu-id="883ab-262">Oracle Linux 6</span></span>

| <span data-ttu-id="883ab-263">**Versione del sistema operativo**</span><span class="sxs-lookup"><span data-stu-id="883ab-263">**OS version**</span></span> | <span data-ttu-id="883ab-264">**Versione del kernel**</span><span class="sxs-lookup"><span data-stu-id="883ab-264">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="883ab-265">6.2</span><span class="sxs-lookup"><span data-stu-id="883ab-265">6.2</span></span> | <span data-ttu-id="883ab-266">Oracle 2.6.32-300 (UEK R1)</span><span class="sxs-lookup"><span data-stu-id="883ab-266">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="883ab-267">6.3</span><span class="sxs-lookup"><span data-stu-id="883ab-267">6.3</span></span> | <span data-ttu-id="883ab-268">Oracle 2.6.39-200 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="883ab-268">Oracle 2.6.39-200 (UEK R2)</span></span> |
| <span data-ttu-id="883ab-269">6.4</span><span class="sxs-lookup"><span data-stu-id="883ab-269">6.4</span></span> | <span data-ttu-id="883ab-270">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="883ab-270">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="883ab-271">6,5</span><span class="sxs-lookup"><span data-stu-id="883ab-271">6.5</span></span> | <span data-ttu-id="883ab-272">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="883ab-272">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |
| <span data-ttu-id="883ab-273">6.6</span><span class="sxs-lookup"><span data-stu-id="883ab-273">6.6</span></span> | <span data-ttu-id="883ab-274">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="883ab-274">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |

#### <a name="oracle-linux-5"></a><span data-ttu-id="883ab-275">Oracle Linux 5</span><span class="sxs-lookup"><span data-stu-id="883ab-275">Oracle Linux 5</span></span>

| <span data-ttu-id="883ab-276">**Versione del sistema operativo**</span><span class="sxs-lookup"><span data-stu-id="883ab-276">**OS version**</span></span> | <span data-ttu-id="883ab-277">**Versione del kernel**</span><span class="sxs-lookup"><span data-stu-id="883ab-277">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="883ab-278">5.8</span><span class="sxs-lookup"><span data-stu-id="883ab-278">5.8</span></span> | <span data-ttu-id="883ab-279">Oracle 2.6.32-300 (UEK R1)</span><span class="sxs-lookup"><span data-stu-id="883ab-279">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="883ab-280">5.9</span><span class="sxs-lookup"><span data-stu-id="883ab-280">5.9</span></span> | <span data-ttu-id="883ab-281">Oracle 2.6.39-300 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="883ab-281">Oracle 2.6.39-300 (UEK R2)</span></span> |
| <span data-ttu-id="883ab-282">5.10</span><span class="sxs-lookup"><span data-stu-id="883ab-282">5.10</span></span> | <span data-ttu-id="883ab-283">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="883ab-283">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="883ab-284">5.11</span><span class="sxs-lookup"><span data-stu-id="883ab-284">5.11</span></span> | <span data-ttu-id="883ab-285">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="883ab-285">Oracle 2.6.39-400 (UEK R2)</span></span> |

#### <a name="suse-linux-enterprise-server"></a><span data-ttu-id="883ab-286">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="883ab-286">SUSE Linux Enterprise Server</span></span>

#### <a name="suse-linux-11"></a><span data-ttu-id="883ab-287">SUSE Linux 11</span><span class="sxs-lookup"><span data-stu-id="883ab-287">SUSE Linux 11</span></span>

| <span data-ttu-id="883ab-288">**Versione del sistema operativo**</span><span class="sxs-lookup"><span data-stu-id="883ab-288">**OS version**</span></span> | <span data-ttu-id="883ab-289">**Versione del kernel**</span><span class="sxs-lookup"><span data-stu-id="883ab-289">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="883ab-290">11</span><span class="sxs-lookup"><span data-stu-id="883ab-290">11</span></span> | <span data-ttu-id="883ab-291">2.6.27</span><span class="sxs-lookup"><span data-stu-id="883ab-291">2.6.27</span></span> |
| <span data-ttu-id="883ab-292">11 SP1</span><span class="sxs-lookup"><span data-stu-id="883ab-292">11 SP1</span></span> | <span data-ttu-id="883ab-293">2.6.32</span><span class="sxs-lookup"><span data-stu-id="883ab-293">2.6.32</span></span> |
| <span data-ttu-id="883ab-294">11 SP2</span><span class="sxs-lookup"><span data-stu-id="883ab-294">11 SP2</span></span> | <span data-ttu-id="883ab-295">3.0.13</span><span class="sxs-lookup"><span data-stu-id="883ab-295">3.0.13</span></span> |
| <span data-ttu-id="883ab-296">11 SP3</span><span class="sxs-lookup"><span data-stu-id="883ab-296">11 SP3</span></span> | <span data-ttu-id="883ab-297">3.0.76</span><span class="sxs-lookup"><span data-stu-id="883ab-297">3.0.76</span></span> |
| <span data-ttu-id="883ab-298">11 SP4</span><span class="sxs-lookup"><span data-stu-id="883ab-298">11 SP4</span></span> | <span data-ttu-id="883ab-299">3.0.101</span><span class="sxs-lookup"><span data-stu-id="883ab-299">3.0.101</span></span> |

#### <a name="suse-linux-10"></a><span data-ttu-id="883ab-300">SUSE Linux 10</span><span class="sxs-lookup"><span data-stu-id="883ab-300">SUSE Linux 10</span></span>

| <span data-ttu-id="883ab-301">**Versione del sistema operativo**</span><span class="sxs-lookup"><span data-stu-id="883ab-301">**OS version**</span></span> | <span data-ttu-id="883ab-302">**Versione del kernel**</span><span class="sxs-lookup"><span data-stu-id="883ab-302">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="883ab-303">10 SP4</span><span class="sxs-lookup"><span data-stu-id="883ab-303">10 SP4</span></span> | <span data-ttu-id="883ab-304">2.6.16.60</span><span class="sxs-lookup"><span data-stu-id="883ab-304">2.6.16.60</span></span> |

#### <a name="dependency-agent-downloads"></a><span data-ttu-id="883ab-305">Download di Dependency Agent</span><span class="sxs-lookup"><span data-stu-id="883ab-305">Dependency Agent downloads</span></span>

| <span data-ttu-id="883ab-306">**File**</span><span class="sxs-lookup"><span data-stu-id="883ab-306">**File**</span></span> | <span data-ttu-id="883ab-307">**Sistema operativo**</span><span class="sxs-lookup"><span data-stu-id="883ab-307">**OS**</span></span> | <span data-ttu-id="883ab-308">**Versione**</span><span class="sxs-lookup"><span data-stu-id="883ab-308">**Version**</span></span> | <span data-ttu-id="883ab-309">**SHA-256**</span><span class="sxs-lookup"><span data-stu-id="883ab-309">**SHA-256**</span></span> |
| --- | --- | --- | --- |
| [<span data-ttu-id="883ab-310">InstallDependencyAgent-Windows.exe</span><span class="sxs-lookup"><span data-stu-id="883ab-310">InstallDependencyAgent-Windows.exe</span></span>](https://aka.ms/dependencyagentwindows) | <span data-ttu-id="883ab-311">Windows</span><span class="sxs-lookup"><span data-stu-id="883ab-311">Windows</span></span> | <span data-ttu-id="883ab-312">9.0.5</span><span class="sxs-lookup"><span data-stu-id="883ab-312">9.0.5</span></span> | <span data-ttu-id="883ab-313">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span><span class="sxs-lookup"><span data-stu-id="883ab-313">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span></span> |
| [<span data-ttu-id="883ab-314">InstallDependencyAgent-Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="883ab-314">InstallDependencyAgent-Linux64.bin</span></span>](https://aka.ms/dependencyagentlinux) | <span data-ttu-id="883ab-315">Linux</span><span class="sxs-lookup"><span data-stu-id="883ab-315">Linux</span></span> | <span data-ttu-id="883ab-316">9.0.5</span><span class="sxs-lookup"><span data-stu-id="883ab-316">9.0.5</span></span> | <span data-ttu-id="883ab-317">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span><span class="sxs-lookup"><span data-stu-id="883ab-317">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span></span> |



## <a name="configuration"></a><span data-ttu-id="883ab-318">Configurazione</span><span class="sxs-lookup"><span data-stu-id="883ab-318">Configuration</span></span>

<span data-ttu-id="883ab-319">Per configurare la soluzione Wire Data per le proprie aree di lavoro, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="883ab-319">Perform the following steps to configure the Wire Data solution for your workspaces.</span></span>

1. <span data-ttu-id="883ab-320">Abilitare la soluzione Log Analytics attività da [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) o seguendo la procedura illustrata in [Aggiungere soluzioni di Log Analytics dalla Raccolta soluzioni](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="883ab-320">Enable the Activity Log Analytics solution from the [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="883ab-321">Installare Dependency Agent in ogni computer in cui si vogliono ottenere i dati.</span><span class="sxs-lookup"><span data-stu-id="883ab-321">Install the Dependency Agent on each computer where you want to get data.</span></span> <span data-ttu-id="883ab-322">Dependency Agent può monitorare le connessioni con i vicini immediati e potrebbe quindi non essere necessario un agente in ogni computer.</span><span class="sxs-lookup"><span data-stu-id="883ab-322">The Dependency Agent can monitor connections to immediate neighbors, so you might not need an agent on every computer.</span></span>

### <a name="install-the-dependency-agent-on-windows"></a><span data-ttu-id="883ab-323">Installare Dependency Agent in Windows</span><span class="sxs-lookup"><span data-stu-id="883ab-323">Install the Dependency Agent on Windows</span></span>

<span data-ttu-id="883ab-324">Per installare o disinstallare l'agente sono necessari i privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="883ab-324">Administrator privileges are required to install or uninstall the agent.</span></span>

<span data-ttu-id="883ab-325">Dependency Agent viene installato nei computer che eseguono Windows con InstallDependencyAgent-Windows.exe.</span><span class="sxs-lookup"><span data-stu-id="883ab-325">The Dependency Agent is installed on computers running Windows through InstallDependencyAgent-Windows.exe.</span></span> <span data-ttu-id="883ab-326">Se si esegue questo file eseguibile senza opzioni, avvia una procedura guidata che consente di completare l'installazione in modo interattivo.</span><span class="sxs-lookup"><span data-stu-id="883ab-326">If you run this executable file without any options, it starts a wizard that you can follow to install interactively.</span></span>

<span data-ttu-id="883ab-327">Per installare Dependency Agent in ogni computer che esegue Windows, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="883ab-327">Use the following steps to install the Dependency Agent on each computer running Windows:</span></span>

1. <span data-ttu-id="883ab-328">Installare l'agente OMS seguendo le istruzioni riportate in [Connettere computer Windows al servizio Log Analytics in Azure](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="883ab-328">Install the OMS Agent by using the instructions at [Connect Windows computers to the Log Analytics service in Azure](log-analytics-windows-agents.md).</span></span>
2. <span data-ttu-id="883ab-329">Scaricare l'agente Windows usando il collegamento riportato nella sezione precedente e quindi eseguirlo con questo comando: InstallDependencyAgent-Windows.exe</span><span class="sxs-lookup"><span data-stu-id="883ab-329">Download the Windows agent using the link in the previous section and then run it by using the following command: InstallDependencyAgent-Windows.exe</span></span>
3. <span data-ttu-id="883ab-330">Seguire la procedura guidata per installare l'agente.</span><span class="sxs-lookup"><span data-stu-id="883ab-330">Follow the wizard to install the agent.</span></span>
4. <span data-ttu-id="883ab-331">Se l'agente di dipendenza non si avvia, controllare i registri per vedere le informazioni dettagliate sull'errore.</span><span class="sxs-lookup"><span data-stu-id="883ab-331">If the Dependency Agent fails to start, check the logs for detailed error information.</span></span> <span data-ttu-id="883ab-332">Per gli agenti Windows, la directory di log è %Programfiles%\Microsoft Dependency Agent\logs.</span><span class="sxs-lookup"><span data-stu-id="883ab-332">On Windows agents, the log directory is %Programfiles%\Microsoft Dependency Agent\logs.</span></span>

#### <a name="windows-command-line"></a><span data-ttu-id="883ab-333">Riga di comando di Windows</span><span class="sxs-lookup"><span data-stu-id="883ab-333">Windows command line</span></span>

<span data-ttu-id="883ab-334">Usare le opzioni della tabella seguente per eseguire l'installazione dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="883ab-334">Use options from the following table to install from a command line.</span></span> <span data-ttu-id="883ab-335">Per visualizzare un elenco dei flag di installazione, eseguire il programma di installazione con il flag /?</span><span class="sxs-lookup"><span data-stu-id="883ab-335">To see a list of the installation flags, run the installer by using the /?</span></span> <span data-ttu-id="883ab-336">come segue.</span><span class="sxs-lookup"><span data-stu-id="883ab-336">flag as follows.</span></span>

<span data-ttu-id="883ab-337">InstallDependencyAgent-Windows.exe /?</span><span class="sxs-lookup"><span data-stu-id="883ab-337">InstallDependencyAgent-Windows.exe /?</span></span>

| <span data-ttu-id="883ab-338">**Flag**</span><span class="sxs-lookup"><span data-stu-id="883ab-338">**Flag**</span></span> | <span data-ttu-id="883ab-339">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="883ab-339">**Description**</span></span> |
| --- | --- |
| <code>/?</code> | <span data-ttu-id="883ab-340">Ottenere un elenco delle opzioni della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="883ab-340">Get a list of the command-line options.</span></span> |
| <code>/S</code> | <span data-ttu-id="883ab-341">Eseguire un'installazione invisibile all'utente senza prompt per l'utente.</span><span class="sxs-lookup"><span data-stu-id="883ab-341">Perform a silent installation with no user prompts.</span></span> |

<span data-ttu-id="883ab-342">Per impostazione predefinita, i file di Dependency Agent per Windows si trovano in C:\Program Files\Microsoft Dependency Agent.</span><span class="sxs-lookup"><span data-stu-id="883ab-342">Files for the Windows Dependency Agent are placed in C:\Program Files\Microsoft Dependency Agent by default.</span></span>

### <a name="install-the-dependency-agent-on-linux"></a><span data-ttu-id="883ab-343">Installare Dependency Agent in Linux</span><span class="sxs-lookup"><span data-stu-id="883ab-343">Install the Dependency Agent on Linux</span></span>

<span data-ttu-id="883ab-344">Per installare o configurare l'agente è necessario l'accesso alla radice.</span><span class="sxs-lookup"><span data-stu-id="883ab-344">Root access is required to install or configure the agent.</span></span>

<span data-ttu-id="883ab-345">Dependency Agent viene installato nei computer Linux con InstallDependencyAgent-Linux64.bin, uno script della shell con un file binario autoestraente.</span><span class="sxs-lookup"><span data-stu-id="883ab-345">The Dependency Agent is installed on Linux computers through InstallDependencyAgent-Linux64.bin, a shell script with a self-extracting binary.</span></span> <span data-ttu-id="883ab-346">È possibile eseguire il file con _sh_ oppure aggiungere autorizzazioni di esecuzione al file stesso.</span><span class="sxs-lookup"><span data-stu-id="883ab-346">You can run the file by using _sh_ or add execute permissions to the file itself.</span></span>

<span data-ttu-id="883ab-347">Per installare Dependency Agent in ogni computer Linux, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="883ab-347">Use the following steps to install the Dependency Agent on each Linux computer:</span></span>

1. <span data-ttu-id="883ab-348">Installare l'agente OMS seguendo le istruzioni per [raccogliere e gestire i dati da computer Linux](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="883ab-348">Install the OMS Agent by using the instructions at [Collect and manage data from Linux computers](log-analytics-agent-linux.md).</span></span>
2. <span data-ttu-id="883ab-349">Scaricare Dependency Agent per Linux usando il collegamento riportato nella sezione precedente e quindi installarlo come radice con questo comando: sh InstallDependencyAgent-Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="883ab-349">Download the Linux Dependency agent using the link in the previous section and then install it as root by using the following command: sh InstallDependencyAgent-Linux64.bin</span></span>
3. <span data-ttu-id="883ab-350">Se l'agente di dipendenza non si avvia, controllare i registri per vedere le informazioni dettagliate sull'errore.</span><span class="sxs-lookup"><span data-stu-id="883ab-350">If the Dependency Agent fails to start, check the logs for detailed error information.</span></span> <span data-ttu-id="883ab-351">Per gli agenti Linux, la directory di log è /var/opt/microsoft/dependency-agent/log.</span><span class="sxs-lookup"><span data-stu-id="883ab-351">On Linux agents, the log directory is: /var/opt/microsoft/dependency-agent/log.</span></span>

<span data-ttu-id="883ab-352">Per visualizzare un elenco dei flag di installazione, eseguire il programma di installazione con il flag `-help` come segue.</span><span class="sxs-lookup"><span data-stu-id="883ab-352">To see a list of the installation flags, run the installation program with the `-help` flag as follows.</span></span>

```
InstallDependencyAgent-Linux64.bin -help
```

| <span data-ttu-id="883ab-353">**Flag**</span><span class="sxs-lookup"><span data-stu-id="883ab-353">**Flag**</span></span> | <span data-ttu-id="883ab-354">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="883ab-354">**Description**</span></span> |
| --- | --- |
| <code>-help</code> | <span data-ttu-id="883ab-355">Ottenere un elenco delle opzioni della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="883ab-355">Get a list of the command-line options.</span></span> |
| <code>-s</code> | <span data-ttu-id="883ab-356">Eseguire un'installazione invisibile all'utente senza prompt per l'utente.</span><span class="sxs-lookup"><span data-stu-id="883ab-356">Perform a silent installation with no user prompts.</span></span> |
| <code>--check</code> | <span data-ttu-id="883ab-357">Controllare le autorizzazioni e il sistema operativo senza installare l'agente.</span><span class="sxs-lookup"><span data-stu-id="883ab-357">Check permissions and the operating system but do not install the agent.</span></span> |

<span data-ttu-id="883ab-358">I file relativi a Dependency Agent sono memorizzati nelle directory seguenti.</span><span class="sxs-lookup"><span data-stu-id="883ab-358">Files for the Dependency Agent are placed in the following directories:</span></span>

| <span data-ttu-id="883ab-359">**File**</span><span class="sxs-lookup"><span data-stu-id="883ab-359">**Files**</span></span> | <span data-ttu-id="883ab-360">**Posizione**</span><span class="sxs-lookup"><span data-stu-id="883ab-360">**Location**</span></span> |
| --- | --- |
| <span data-ttu-id="883ab-361">File core</span><span class="sxs-lookup"><span data-stu-id="883ab-361">Core files</span></span> | <span data-ttu-id="883ab-362">/opt/microsoft/dependency-agent</span><span class="sxs-lookup"><span data-stu-id="883ab-362">/opt/microsoft/dependency-agent</span></span> |
| <span data-ttu-id="883ab-363">File di log</span><span class="sxs-lookup"><span data-stu-id="883ab-363">Log files</span></span> | <span data-ttu-id="883ab-364">/var/opt/microsoft/dependency-agent/log</span><span class="sxs-lookup"><span data-stu-id="883ab-364">/var/opt/microsoft/dependency-agent/log</span></span> |
| <span data-ttu-id="883ab-365">File di configurazione</span><span class="sxs-lookup"><span data-stu-id="883ab-365">Config files</span></span> | <span data-ttu-id="883ab-366">/etc/opt/microsoft/dependency-agent/config</span><span class="sxs-lookup"><span data-stu-id="883ab-366">/etc/opt/microsoft/dependency-agent/config</span></span> |
| <span data-ttu-id="883ab-367">File eseguibili del servizio</span><span class="sxs-lookup"><span data-stu-id="883ab-367">Service executable files</span></span> | <span data-ttu-id="883ab-368">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span><span class="sxs-lookup"><span data-stu-id="883ab-368">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span></span><br><br><span data-ttu-id="883ab-369">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span><span class="sxs-lookup"><span data-stu-id="883ab-369">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span></span> |
| <span data-ttu-id="883ab-370">File binary di archiviazione</span><span class="sxs-lookup"><span data-stu-id="883ab-370">Binary storage files</span></span> | <span data-ttu-id="883ab-371">/var/opt/microsoft/dependency-agent/storage</span><span class="sxs-lookup"><span data-stu-id="883ab-371">/var/opt/microsoft/dependency-agent/storage</span></span> |

### <a name="installation-script-examples"></a><span data-ttu-id="883ab-372">Esempi di script di installazione</span><span class="sxs-lookup"><span data-stu-id="883ab-372">Installation script examples</span></span>

<span data-ttu-id="883ab-373">Per distribuire facilmente Dependency Agent in più server contemporaneamente, è utile usare uno script.</span><span class="sxs-lookup"><span data-stu-id="883ab-373">To easily deploy the Dependency Agent on many servers at once, it helps to use a script.</span></span> <span data-ttu-id="883ab-374">È possibile usare gli esempi di script seguenti per scaricare e installare Dependency Agent in Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="883ab-374">You can use the following script examples to download and install the Dependency Agent on either Windows or Linux.</span></span>

#### <a name="powershell-script-for-windows"></a><span data-ttu-id="883ab-375">Script di PowerShell per Windows</span><span class="sxs-lookup"><span data-stu-id="883ab-375">PowerShell script for Windows</span></span>

```PowerShell

Invoke-WebRequest &quot;https://aka.ms/dependencyagentwindows&quot; -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S

```

#### <a name="shell-script-for-linux"></a><span data-ttu-id="883ab-376">Script della shell per Linux</span><span class="sxs-lookup"><span data-stu-id="883ab-376">Shell script for Linux</span></span>

```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
```

```
sh InstallDependencyAgent-Linux64.bin -s
```

### <a name="desired-state-configuration"></a><span data-ttu-id="883ab-377">Configurazione dello stato desiderato</span><span class="sxs-lookup"><span data-stu-id="883ab-377">Desired State Configuration</span></span>

<span data-ttu-id="883ab-378">Per distribuire Dependency Agent tramite Desired State Configuration, è possibile usare il modulo xPSDesiredStateConfiguration e un frammento di codice come il seguente:</span><span class="sxs-lookup"><span data-stu-id="883ab-378">To deploy the Dependency Agent via Desired State Configuration, you can use the xPSDesiredStateConfiguration module and a bit of code like the following:</span></span>

```
Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = &quot;C:\InstallDependencyAgent-Windows.exe&quot;



Node $NodeName

{

    # Download and install the Dependency Agent

    xRemoteFile DAPackage

    {

        Uri = &quot;https://aka.ms/dependencyagentwindows&quot;

        DestinationPath = $DAPackageLocalPath

        DependsOn = &quot;[Package]OI&quot;

    }

    xPackage DA

    {

        Ensure=&quot;Present&quot;

        Name = &quot;Dependency Agent&quot;

        Path = $DAPackageLocalPath

        Arguments = '/S'

        ProductId = &quot;&quot;

        InstalledCheckRegKey = &quot;HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent&quot;

        InstalledCheckRegValueName = &quot;DisplayName&quot;

        InstalledCheckRegValueData = &quot;Dependency Agent&quot;

    }

}

```
### <a name="uninstall-the-dependency-agent"></a><span data-ttu-id="883ab-379">Disinstallare Dependency Agent</span><span class="sxs-lookup"><span data-stu-id="883ab-379">Uninstall the Dependency Agent</span></span>

<span data-ttu-id="883ab-380">Per rimuovere Dependency Agent, usare le sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="883ab-380">Use the following sections to help you remove the Dependency Agent.</span></span>

#### <a name="uninstall-the-dependency-agent-on-windows"></a><span data-ttu-id="883ab-381">Disinstallare Dependency Agent in Windows</span><span class="sxs-lookup"><span data-stu-id="883ab-381">Uninstall the Dependency Agent on Windows</span></span>

<span data-ttu-id="883ab-382">Dependency Agent per Windows può essere disinstallato da un amministratore tramite il Pannello di controllo.</span><span class="sxs-lookup"><span data-stu-id="883ab-382">An administrator can uninstall the Dependency Agent for Windows through Control Panel.</span></span>

<span data-ttu-id="883ab-383">Per disinstallare Dependency Agent, un amministratore può anche eseguire %Programfiles%\Microsoft Dependency Agent\Uninstall.exe.</span><span class="sxs-lookup"><span data-stu-id="883ab-383">An administrator can also run %Programfiles%\Microsoft Dependency Agent\Uninstall.exe to uninstall the Dependency Agent.</span></span>

#### <a name="uninstall-the-dependency-agent-on-linux"></a><span data-ttu-id="883ab-384">Disinstallare Dependency Agent in Linux</span><span class="sxs-lookup"><span data-stu-id="883ab-384">Uninstall the Dependency Agent on Linux</span></span>

<span data-ttu-id="883ab-385">Per disinstallare completamente Dependency Agent da Linux, è necessario rimuovere l'agente stesso e il connettore che viene installato automaticamente con l'agente.</span><span class="sxs-lookup"><span data-stu-id="883ab-385">To completely uninstall the Dependency Agent from Linux, you must remove the agent itself and the connector, which is installed automatically with the agent.</span></span> <span data-ttu-id="883ab-386">È possibile disinstallare entrambi con il singolo comando seguente:</span><span class="sxs-lookup"><span data-stu-id="883ab-386">You can uninstall both by using the following single command:</span></span>

```
rpm -e dependency-agent dependency-agent-connector
```

## <a name="management-packs"></a><span data-ttu-id="883ab-387">Management Pack</span><span class="sxs-lookup"><span data-stu-id="883ab-387">Management packs</span></span>

<span data-ttu-id="883ab-388">Quando viene attivato Wire Data in un'area di lavoro di Log Analytics, a tutti i server Windows nell'area di lavoro viene inviato un Management Pack di 300 KB.</span><span class="sxs-lookup"><span data-stu-id="883ab-388">When Wire Data is activated in a Log Analytics workspace, a 300-KB management pack is sent to all the Windows servers in that workspace.</span></span> <span data-ttu-id="883ab-389">Se si usano agenti System Center Operations Manager in un [gruppo di gestione connesso](log-analytics-om-agents.md), il Management Pack di Dependency Monitor viene distribuito da System Center Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="883ab-389">If you are using System Center Operations Manager agents in a [connected management group](log-analytics-om-agents.md), the Dependency Monitor management pack is deployed from System Center Operations Manager.</span></span> <span data-ttu-id="883ab-390">Se gli agenti sono connessi direttamente, il Management Pack viene fornito da Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="883ab-390">If the agents are directly connected, Log Analytics delivers the management pack.</span></span>

<span data-ttu-id="883ab-391">Il Management Pack è denominato Microsoft.IntelligencePacks.ApplicationDependencyMonitor</span><span class="sxs-lookup"><span data-stu-id="883ab-391">The management pack is named Microsoft.IntelligencePacks.ApplicationDependencyMonitor.</span></span> <span data-ttu-id="883ab-392">e viene inserito in %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs\.</span><span class="sxs-lookup"><span data-stu-id="883ab-392">It's written to: %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs.</span></span> <span data-ttu-id="883ab-393">L'origine dati usata dal Management Pack è %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;IDGeneratoAutomaticamente&gt;\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.</span><span class="sxs-lookup"><span data-stu-id="883ab-393">The data source that the management pack uses is: %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.</span></span>

## <a name="using-the-solution"></a><span data-ttu-id="883ab-394">Uso della soluzione</span><span class="sxs-lookup"><span data-stu-id="883ab-394">Using the solution</span></span>

<span data-ttu-id="883ab-395">**Installazione e configurazione della soluzione**</span><span class="sxs-lookup"><span data-stu-id="883ab-395">**Installing and configuring the solution**</span></span>

<span data-ttu-id="883ab-396">Usare le informazioni seguenti per installare e configurare la soluzione.</span><span class="sxs-lookup"><span data-stu-id="883ab-396">Use the following information to install and configure the solution.</span></span>

- <span data-ttu-id="883ab-397">La soluzione Wire Data acquisisce i dati dai computer che eseguono Windows Server 2012 R2, Windows 8.1 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="883ab-397">The Wire Data solution acquires data from computers running Windows Server 2012 R2, Windows 8.1, and later operating systems.</span></span>
- <span data-ttu-id="883ab-398">Nei computer da cui si desidera acquisire i dati in transito è necessario che sia installato Microsoft .NET Framework 4.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="883ab-398">Microsoft .NET Framework 4.0 or later is required on computers where you want to acquire wire data from.</span></span>
- <span data-ttu-id="883ab-399">Aggiungere la soluzione Wire Data all'area di lavoro di Log Analytics usando la procedura descritta nell'articolo su come [aggiungere soluzioni di Log Analytics dalla raccolta soluzioni](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="883ab-399">Add the Wire Data solution to your Log Analytics workspace using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="883ab-400">Non è richiesta alcuna ulteriore configurazione.</span><span class="sxs-lookup"><span data-stu-id="883ab-400">There is no further configuration required.</span></span>
- <span data-ttu-id="883ab-401">Se si vogliono visualizzare i dati in transito per una soluzione specifica, è necessario che la soluzione sia già stata aggiunta all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="883ab-401">If you want to view wire data for a specific solution, you need to have the solution already added to your workspace.</span></span>

<span data-ttu-id="883ab-402">Dopo l'installazione degli agenti e della soluzione, nell'area di lavoro verrà visualizzato il riquadro Wire Data 2.0.</span><span class="sxs-lookup"><span data-stu-id="883ab-402">After you have agents installed and you install the solution, the Wire Data 2.0 tile appears in your workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="883ab-403">Attualmente, per visualizzare i dati in transito è necessario usare il portale di OMS.</span><span class="sxs-lookup"><span data-stu-id="883ab-403">Currently, you must use the OMS portal to view wire data.</span></span> <span data-ttu-id="883ab-404">Non è possibile usare il portale di Azure a tale scopo.</span><span class="sxs-lookup"><span data-stu-id="883ab-404">You cannot use the Azure portal to view wire data.</span></span>

![Riquadro Wire Data](./media/log-analytics-wire-data/wire-data-tile.png)

## <a name="using-the-wire-data-20-solution"></a><span data-ttu-id="883ab-406">Uso della soluzione Wire Data 2.0</span><span class="sxs-lookup"><span data-stu-id="883ab-406">Using the Wire Data 2.0 solution</span></span>

<span data-ttu-id="883ab-407">Nel portale di OMS fare clic sul riquadro **Wire Data 2.0** per aprire il dashboard di Wire Data.</span><span class="sxs-lookup"><span data-stu-id="883ab-407">In the OMS portal, click the **Wire Data 2.0** tile to open the Wire Data dashboard.</span></span> <span data-ttu-id="883ab-408">Il dashboard include i pannelli nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="883ab-408">The dashboard includes the blades in the following table.</span></span> <span data-ttu-id="883ab-409">Ogni panello elenca fino a 10 elementi corrispondenti ai criteri del pannello per lo scope e l'intervallo di tempo specificati.</span><span class="sxs-lookup"><span data-stu-id="883ab-409">Each blade lists up to 10 items matching that blade's criteria for the specified scope and time range.</span></span> <span data-ttu-id="883ab-410">È possibile eseguire una ricerca log per ottenere tutti i record facendo clic su **Vedi tutto** nella parte inferiore del pannello o facendo clic sull'intestazione del pannello.</span><span class="sxs-lookup"><span data-stu-id="883ab-410">You can run a log search that returns all records by clicking **See all** at the bottom of the blade or by clicking the blade header.</span></span>

| <span data-ttu-id="883ab-411">**Pannello**</span><span class="sxs-lookup"><span data-stu-id="883ab-411">**Blade**</span></span> | <span data-ttu-id="883ab-412">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="883ab-412">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="883ab-413">Agenti che acquisiscono il traffico di rete</span><span class="sxs-lookup"><span data-stu-id="883ab-413">Agents capturing network traffic</span></span> | <span data-ttu-id="883ab-414">Mostra il numero degli agenti che acquisiscono il traffico di rete e un elenco dei primi 10 computer che acquisiscono il traffico.</span><span class="sxs-lookup"><span data-stu-id="883ab-414">Shows the number of agents that are capturing network traffic and lists the top 10 computers that are capturing traffic.</span></span> <span data-ttu-id="883ab-415">Fare clic sul numero per eseguire una ricerca nei log per <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>.</span><span class="sxs-lookup"><span data-stu-id="883ab-415">Click the number to run a log search for <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>.</span></span> <span data-ttu-id="883ab-416">Fare clic su un computer nell'elenco per eseguire una ricerca nei log che restituisca il numero totale dei byte acquisiti.</span><span class="sxs-lookup"><span data-stu-id="883ab-416">Click a computer in the list to run a log search returning the total number of bytes captured.</span></span> |
| <span data-ttu-id="883ab-417">Subnet locali</span><span class="sxs-lookup"><span data-stu-id="883ab-417">Local Subnets</span></span> | <span data-ttu-id="883ab-418">Mostra il numero delle subnet locali individuate dagli agenti.</span><span class="sxs-lookup"><span data-stu-id="883ab-418">Shows the number of local subnets that agents have discovered.</span></span>  <span data-ttu-id="883ab-419">Fare clic sul numero per eseguire una ricerca nei log per <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> e ottenere un elenco di tutte le subnet con il numero dei byte inviati tramite ognuna.</span><span class="sxs-lookup"><span data-stu-id="883ab-419">Click the number to run a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> that lists all subnets with the number of bytes sent over each one.</span></span> <span data-ttu-id="883ab-420">Fare clic su una subnet nell'elenco per eseguire una ricerca nei log che restituisca il numero totale dei byte inviati tramite la subnet.</span><span class="sxs-lookup"><span data-stu-id="883ab-420">Click a subnet in the list to run a log search returning the total number of bytes sent over the subnet.</span></span> |
| <span data-ttu-id="883ab-421">Protocolli a livello dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="883ab-421">Application-level Protocols</span></span> | <span data-ttu-id="883ab-422">Mostra il numero di protocolli a livello di applicazione in uso, in base a quanto individuato dagli agenti.</span><span class="sxs-lookup"><span data-stu-id="883ab-422">Shows the number of application-level protocols in use, as discovered by agents.</span></span> <span data-ttu-id="883ab-423">Fare clic sul numero per eseguire una ricerca nei log per <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>.</span><span class="sxs-lookup"><span data-stu-id="883ab-423">Click the number to run a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>.</span></span> <span data-ttu-id="883ab-424">Fare clic su un protocollo per eseguire una ricerca nei log che restituisca il numero totale dei byte inviati usando il protocollo.</span><span class="sxs-lookup"><span data-stu-id="883ab-424">Click a protocol to run a log search returning the total number of bytes sent using the protocol.</span></span> |

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Dashboard di Wire Data](./media/log-analytics-wire-data/wire-data-dash.png)

<span data-ttu-id="883ab-426">È possibile usare il pannello **Agenti che acquisiscono il traffico di rete** per determinare la quantità di larghezza di banda utilizzata dai computer.</span><span class="sxs-lookup"><span data-stu-id="883ab-426">You can use the **Agents capturing network traffic** blade to determine how much network bandwidth is being consumed by computers.</span></span> <span data-ttu-id="883ab-427">Questo pannello consente di trovare facilmente il computer _più comunicativo_ nel proprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="883ab-427">This blade can help you easily find the _chattiest_ computer in your environment.</span></span> <span data-ttu-id="883ab-428">Tali computer potrebbero essere sovraccaricati, presentare un funzionamento anomalo o usare una quantità di risorse di rete superiore alla norma.</span><span class="sxs-lookup"><span data-stu-id="883ab-428">Such computers could be overloaded, acting abnormally, or using more network resources than normal.</span></span>

![Esempio di ricerca log](./media/log-analytics-wire-data/log-search-example01.png)

<span data-ttu-id="883ab-430">Analogamente, è possibile usare il pannello **Subnet locali** per determinare la quantità di traffico di rete sulle subnet.</span><span class="sxs-lookup"><span data-stu-id="883ab-430">Similarly, you can use the **Local Subnets** blade to determine how much network traffic is moving through your subnets.</span></span> <span data-ttu-id="883ab-431">Gli utenti spesso definiscono le subnet per aree critiche per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="883ab-431">Users often define subnets around critical areas for their applications.</span></span> <span data-ttu-id="883ab-432">Questo pannello offre un quadro di tali aree.</span><span class="sxs-lookup"><span data-stu-id="883ab-432">This blade offers a view into those areas.</span></span>

![Esempio di ricerca log](./media/log-analytics-wire-data/log-search-example02.png)

<span data-ttu-id="883ab-434">Il pannello **Protocolli a livello dell'applicazione** è utile perché è opportuno sapere quali protocolli vengono usati.</span><span class="sxs-lookup"><span data-stu-id="883ab-434">The **Application-level Protocols** blade is useful because it's helpful know what protocols are in use.</span></span> <span data-ttu-id="883ab-435">Se ad esempio si prevede che SSH non venga usato nel proprio ambiente di rete,</span><span class="sxs-lookup"><span data-stu-id="883ab-435">For example, you might expect SSH to not be in use in your network environment.</span></span> <span data-ttu-id="883ab-436">visualizzando le informazioni disponibili nel pannello è possibile ottenere rapidamente conferma o smentita di tale previsione.</span><span class="sxs-lookup"><span data-stu-id="883ab-436">Viewing information available in the blade can quickly confirm or disprove your expectation.</span></span>

![Esempio di ricerca log](./media/log-analytics-wire-data/log-search-example03.png)

<span data-ttu-id="883ab-438">In questo esempio si potrebbero esaminare i dettagli su SSH per scoprire quali computer usano SSH e molti altri dettagli relativi alle comunicazioni.</span><span class="sxs-lookup"><span data-stu-id="883ab-438">In this example, you could drill-into SSH details to see which computers are using SSH and many other communication details.</span></span>

![Risultati della ricerca su SSH](./media/log-analytics-wire-data/ssh-details.png)

<span data-ttu-id="883ab-440">È anche utile sapere se il traffico dei protocolli aumenta o diminuisce nel tempo.</span><span class="sxs-lookup"><span data-stu-id="883ab-440">It's also useful to know if protocol traffic is increasing or decreasing over time.</span></span> <span data-ttu-id="883ab-441">L'aumento della quantità di dati trasmessa da un'applicazione, ad esempio, può essere un aspetto di cui è consigliabile essere a conoscenza o che si potrebbe trovare degno di nota.</span><span class="sxs-lookup"><span data-stu-id="883ab-441">For example, if the amount of data being transmitted by an application is increasing, that might be something you should be aware of, or that you might find noteworthy.</span></span>

## <a name="input-data"></a><span data-ttu-id="883ab-442">Dati di input</span><span class="sxs-lookup"><span data-stu-id="883ab-442">Input data</span></span>

<span data-ttu-id="883ab-443">Wire Data raccoglie i metadati sul traffico di rete tramite gli agenti abilitati.</span><span class="sxs-lookup"><span data-stu-id="883ab-443">Wire data collects metadata about network traffic using the agents that you have enabled.</span></span> <span data-ttu-id="883ab-444">Ogni agente invia dati ogni 15 secondi circa.</span><span class="sxs-lookup"><span data-stu-id="883ab-444">Each agent sends data about every 15 seconds.</span></span>

## <a name="output-data"></a><span data-ttu-id="883ab-445">Dati di output</span><span class="sxs-lookup"><span data-stu-id="883ab-445">Output data</span></span>

<span data-ttu-id="883ab-446">Per ogni tipo di dati di input vene creato un record con tipo _WireData_.</span><span class="sxs-lookup"><span data-stu-id="883ab-446">A record with a type of _WireData_ is created for each type of input data.</span></span> <span data-ttu-id="883ab-447">I record WireData includono le proprietà elencate nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="883ab-447">WireData records have properties shown in the following table:</span></span>

| <span data-ttu-id="883ab-448">Proprietà</span><span class="sxs-lookup"><span data-stu-id="883ab-448">Property</span></span> | <span data-ttu-id="883ab-449">Descrizione</span><span class="sxs-lookup"><span data-stu-id="883ab-449">Description</span></span> |
|---|---|
| <span data-ttu-id="883ab-450">Computer</span><span class="sxs-lookup"><span data-stu-id="883ab-450">Computer</span></span> | <span data-ttu-id="883ab-451">Nome del computer in cui sono stati raccolti i dati</span><span class="sxs-lookup"><span data-stu-id="883ab-451">Computer name where data was collected</span></span> |
| <span data-ttu-id="883ab-452">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="883ab-452">TimeGenerated</span></span> | <span data-ttu-id="883ab-453">Ora del record</span><span class="sxs-lookup"><span data-stu-id="883ab-453">Time of the record</span></span> |
| <span data-ttu-id="883ab-454">LocalIP</span><span class="sxs-lookup"><span data-stu-id="883ab-454">LocalIP</span></span> | <span data-ttu-id="883ab-455">Indirizzo IP del computer locale</span><span class="sxs-lookup"><span data-stu-id="883ab-455">IP address of the local computer</span></span> |
| <span data-ttu-id="883ab-456">SessionState</span><span class="sxs-lookup"><span data-stu-id="883ab-456">SessionState</span></span> | <span data-ttu-id="883ab-457">Sessione connessa o disconnessa</span><span class="sxs-lookup"><span data-stu-id="883ab-457">Connected or disconnected</span></span> |
| <span data-ttu-id="883ab-458">ReceivedBytes</span><span class="sxs-lookup"><span data-stu-id="883ab-458">ReceivedBytes</span></span> | <span data-ttu-id="883ab-459">Quantità di byte ricevuta</span><span class="sxs-lookup"><span data-stu-id="883ab-459">Amount of bytes received</span></span> |
| <span data-ttu-id="883ab-460">ProtocolName</span><span class="sxs-lookup"><span data-stu-id="883ab-460">ProtocolName</span></span> | <span data-ttu-id="883ab-461">Nome del protocollo di rete usato</span><span class="sxs-lookup"><span data-stu-id="883ab-461">Name of the network protocol used</span></span> |
| <span data-ttu-id="883ab-462">IPVersion</span><span class="sxs-lookup"><span data-stu-id="883ab-462">IPVersion</span></span> | <span data-ttu-id="883ab-463">Versione IP</span><span class="sxs-lookup"><span data-stu-id="883ab-463">IP version</span></span> |
| <span data-ttu-id="883ab-464">Direzione</span><span class="sxs-lookup"><span data-stu-id="883ab-464">Direction</span></span> | <span data-ttu-id="883ab-465">In ingresso o in uscita</span><span class="sxs-lookup"><span data-stu-id="883ab-465">Inbound or outbound</span></span> |
| <span data-ttu-id="883ab-466">MaliciousIP</span><span class="sxs-lookup"><span data-stu-id="883ab-466">MaliciousIP</span></span> | <span data-ttu-id="883ab-467">Indirizzo IP di un'origine dannosa nota</span><span class="sxs-lookup"><span data-stu-id="883ab-467">IP address of a known malicious source</span></span> |
| <span data-ttu-id="883ab-468">Severity</span><span class="sxs-lookup"><span data-stu-id="883ab-468">Severity</span></span> | <span data-ttu-id="883ab-469">Gravità del software dannoso sospetto</span><span class="sxs-lookup"><span data-stu-id="883ab-469">Suspected malware severity</span></span> |
| <span data-ttu-id="883ab-470">RemoteIPCountry</span><span class="sxs-lookup"><span data-stu-id="883ab-470">RemoteIPCountry</span></span> | <span data-ttu-id="883ab-471">Paese dell'indirizzo IP remoto</span><span class="sxs-lookup"><span data-stu-id="883ab-471">Country of the remote IP address</span></span> |
| <span data-ttu-id="883ab-472">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="883ab-472">ManagementGroupName</span></span> | <span data-ttu-id="883ab-473">Nome del gruppo di gestione di Operations Manager</span><span class="sxs-lookup"><span data-stu-id="883ab-473">Name of the Operations Manager management group</span></span> |
| <span data-ttu-id="883ab-474">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="883ab-474">SourceSystem</span></span> | <span data-ttu-id="883ab-475">Origine in cui sono stati raccolti i dati</span><span class="sxs-lookup"><span data-stu-id="883ab-475">Source where data was collected</span></span> |
| <span data-ttu-id="883ab-476">SessionStartTime</span><span class="sxs-lookup"><span data-stu-id="883ab-476">SessionStartTime</span></span> | <span data-ttu-id="883ab-477">Data e ora di inizio della sessione</span><span class="sxs-lookup"><span data-stu-id="883ab-477">Start time of session</span></span> |
| <span data-ttu-id="883ab-478">SessionEndTime</span><span class="sxs-lookup"><span data-stu-id="883ab-478">SessionEndTime</span></span> | <span data-ttu-id="883ab-479">Data e ora di fine della sessione</span><span class="sxs-lookup"><span data-stu-id="883ab-479">End time of session</span></span> |
| <span data-ttu-id="883ab-480">LocalSubnet</span><span class="sxs-lookup"><span data-stu-id="883ab-480">LocalSubnet</span></span> | <span data-ttu-id="883ab-481">Subnet in cui sono stati raccolti i dati</span><span class="sxs-lookup"><span data-stu-id="883ab-481">Subnet where data was collected</span></span> |
| <span data-ttu-id="883ab-482">LocalPortNumber</span><span class="sxs-lookup"><span data-stu-id="883ab-482">LocalPortNumber</span></span> | <span data-ttu-id="883ab-483">Numero di porta locale</span><span class="sxs-lookup"><span data-stu-id="883ab-483">Local port number</span></span> |
| <span data-ttu-id="883ab-484">RemoteIP</span><span class="sxs-lookup"><span data-stu-id="883ab-484">RemoteIP</span></span> | <span data-ttu-id="883ab-485">Indirizzo IP remoto usato dal computer remoto</span><span class="sxs-lookup"><span data-stu-id="883ab-485">Remote IP address used by the remote computer</span></span> |
| <span data-ttu-id="883ab-486">RemotePortNumber</span><span class="sxs-lookup"><span data-stu-id="883ab-486">RemotePortNumber</span></span> | <span data-ttu-id="883ab-487">Numero di porta usato dall'indirizzo IP remoto</span><span class="sxs-lookup"><span data-stu-id="883ab-487">Port number used by the remote IP address</span></span> |
| <span data-ttu-id="883ab-488">SessionID</span><span class="sxs-lookup"><span data-stu-id="883ab-488">SessionID</span></span> | <span data-ttu-id="883ab-489">Valore univoco che identifica la sessione di comunicazione tra due indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="883ab-489">A unique value that identifies communication session between two IP addresses</span></span> |
| <span data-ttu-id="883ab-490">SentBytes</span><span class="sxs-lookup"><span data-stu-id="883ab-490">SentBytes</span></span> | <span data-ttu-id="883ab-491">Numero di byte inviati</span><span class="sxs-lookup"><span data-stu-id="883ab-491">Number of bytes sent</span></span> |
| <span data-ttu-id="883ab-492">TotalBytes</span><span class="sxs-lookup"><span data-stu-id="883ab-492">TotalBytes</span></span> | <span data-ttu-id="883ab-493">Numero totale dei byte inviati durante la sessione</span><span class="sxs-lookup"><span data-stu-id="883ab-493">Total number of bytes sent during session</span></span> |
| <span data-ttu-id="883ab-494">ApplicationProtocol</span><span class="sxs-lookup"><span data-stu-id="883ab-494">ApplicationProtocol</span></span> | <span data-ttu-id="883ab-495">Tipo di protocollo di rete usato</span><span class="sxs-lookup"><span data-stu-id="883ab-495">Type of network protocol used</span></span>   |
| <span data-ttu-id="883ab-496">ProcessID</span><span class="sxs-lookup"><span data-stu-id="883ab-496">ProcessID</span></span> | <span data-ttu-id="883ab-497">ID processo Windows</span><span class="sxs-lookup"><span data-stu-id="883ab-497">Windows process ID</span></span> |
| <span data-ttu-id="883ab-498">ProcessName</span><span class="sxs-lookup"><span data-stu-id="883ab-498">ProcessName</span></span> | <span data-ttu-id="883ab-499">Percorso e nome file del processo</span><span class="sxs-lookup"><span data-stu-id="883ab-499">Path and file name of the process</span></span> |
| <span data-ttu-id="883ab-500">RemoteIPLongitude</span><span class="sxs-lookup"><span data-stu-id="883ab-500">RemoteIPLongitude</span></span> | <span data-ttu-id="883ab-501">Valore di longitudine dell'indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="883ab-501">IP longitude value</span></span> |
| <span data-ttu-id="883ab-502">RemoteIPLatitude</span><span class="sxs-lookup"><span data-stu-id="883ab-502">RemoteIPLatitude</span></span> | <span data-ttu-id="883ab-503">Valore di latitudine dell'indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="883ab-503">IP latitude value</span></span> |


## <a name="next-steps"></a><span data-ttu-id="883ab-504">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="883ab-504">Next steps</span></span>

- <span data-ttu-id="883ab-505">[Ricerche nei log](log-analytics-log-searches.md) per visualizzare i record di ricerca dettagliati su Wire Data.</span><span class="sxs-lookup"><span data-stu-id="883ab-505">[Search logs](log-analytics-log-searches.md) to view detailed wire data search records.</span></span>
