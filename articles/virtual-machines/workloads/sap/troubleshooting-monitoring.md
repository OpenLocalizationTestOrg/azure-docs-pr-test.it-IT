---
title: aaaTroubleshooting e monitoraggio di SAP HANA in Azure (istanze di grandi dimensioni) | Documenti Microsoft
description: Risolvere i problemi e monitorare SAP HANA in Azure (istanze di grandi dimensioni).
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1f1cd35820e227fd99af495431cd4b826aa53600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a><span data-ttu-id="bb8a9-103">Come tootroubleshoot e monitoraggio SAP HANA (istanze di grandi dimensioni) in Azure</span><span class="sxs-lookup"><span data-stu-id="bb8a9-103">How tootroubleshoot and monitor SAP HANA (large instances) on Azure</span></span>


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a><span data-ttu-id="bb8a9-104">Monitoraggio in SAP HANA in Azure (istanze di grandi dimensioni)</span><span class="sxs-lookup"><span data-stu-id="bb8a9-104">Monitoring in SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="bb8a9-105">SAP HANA in Azure (istanze di grandi dimensioni) non è diverso da qualsiasi altra distribuzione IaaS, è necessario toomonitor cosa hello del sistema operativo e un'applicazione hello procedere e come questi utilizzare hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="bb8a9-105">SAP HANA on Azure (Large Instances) is no different from any other IaaS deployment — you need toomonitor what hello OS and hello application is doing and how these consume hello following resources:</span></span>

- <span data-ttu-id="bb8a9-106">CPU</span><span class="sxs-lookup"><span data-stu-id="bb8a9-106">CPU</span></span>
- <span data-ttu-id="bb8a9-107">Memoria</span><span class="sxs-lookup"><span data-stu-id="bb8a9-107">Memory</span></span>
- <span data-ttu-id="bb8a9-108">Larghezza di banda della rete</span><span class="sxs-lookup"><span data-stu-id="bb8a9-108">Network bandwidth</span></span>
- <span data-ttu-id="bb8a9-109">Spazio su disco</span><span class="sxs-lookup"><span data-stu-id="bb8a9-109">Disk space</span></span>

<span data-ttu-id="bb8a9-110">Come con macchine virtuali di Azure è necessario toofigure se le classi di risorse hello sopra sono sufficienti o se queste ottenere esaurite.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-110">As with Azure Virtual Machines you need toofigure out whether hello resource classes named above are sufficient, or whether these get depleted.</span></span> <span data-ttu-id="bb8a9-111">Ecco ulteriori dettagli su ciascuna delle classi diverse hello:</span><span class="sxs-lookup"><span data-stu-id="bb8a9-111">Here is more detail on each of hello different classes:</span></span>

<span data-ttu-id="bb8a9-112">**Utilizzo delle risorse della CPU:** rapporto hello definite SAP per determinati HANA carico di lavoro è imposto toomake che deve essere sufficiente toowork disponibili risorse di CPU tramite hello i dati archiviati in memoria.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-112">**CPU resource consumption:** hello ratio that SAP defined for certain workload against HANA is enforced toomake sure that there should be enough CPU resources available toowork through hello data that is stored in memory.</span></span> <span data-ttu-id="bb8a9-113">Tuttavia, potrebbe essere casi in cui HANA richiede una maggiore quantità di CPU, l'esecuzione di query a causa di problemi simili o toomissing indici.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-113">Nevertheless, there might be cases where HANA consumes a lot of CPU executing queries due toomissing indexes or similar issues.</span></span> <span data-ttu-id="bb8a9-114">Ciò significa che è necessario monitorare il consumo di risorse della CPU di unità di grandi dimensioni istanza HANA hello, nonché le risorse della CPU utilizzate da servizi HANA specifici hello.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-114">This means you should monitor CPU resource consumption of hello HANA large instance unit as well as CPU resources consumed by hello specific HANA services.</span></span>

<span data-ttu-id="bb8a9-115">**Utilizzo della memoria:** è importante toomonitor all'interno di HANA, nonché di fuori di HANA unità hello.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-115">**Memory consumption:** Is important toomonitor from within HANA, as well as outside of HANA on hello unit.</span></span> <span data-ttu-id="bb8a9-116">All'interno di HANA, monitorare come dati hello sta consumando memoria in toostay ordine all'interno di hello richiesto il ridimensionamento delle linee guida di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-116">Within HANA, monitor how hello data is consuming HANA allocated memory in order toostay within hello required sizing guidelines of SAP.</span></span> <span data-ttu-id="bb8a9-117">È anche opportuno toomonitor utilizzo della memoria su hello istanza grande livello toomake che il software aggiuntivo HANA-non installato non usano troppa memoria e pertanto si contendono HANA per la memoria.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-117">You also want toomonitor memory consumption on hello Large Instance level toomake sure that additional installed non-HANA software does not consume too much memory, and therefore compete with HANA for memory.</span></span>

<span data-ttu-id="bb8a9-118">**Larghezza di banda di rete:** gateway di rete virtuale di Azure hello è limitata di dati trasferiti in rete virtuale di Azure hello la larghezza di banda, è utile ricevuti da tutti i dati di hello toomonitor hello macchine virtuali di Azure all'interno di un toofigure di rete virtuale come chiudere sono toohello limiti di hello Azure lo SKU selezionato del gateway.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-118">**Network bandwidth:** hello Azure VNet gateway is limited in bandwidth of data moving into hello Azure VNet, so it is helpful toomonitor hello data received by all hello Azure VMs within a VNet toofigure out how close you are toohello limits of hello Azure gateway SKU you selected.</span></span> <span data-ttu-id="bb8a9-119">Nell'unità di istanza di grandi dimensioni HANA hello, rende senso toomonitor in ingresso e in uscita del traffico di rete nonché e tenere traccia di tookeep dei volumi hello che vengono gestiti nel tempo.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-119">On hello HANA Large Instance unit, it does make sense toomonitor incoming and outgoing network traffic as well, and tookeep track of hello volumes that are handled over time.</span></span>

<span data-ttu-id="bb8a9-120">**Spazio su disco**: l'utilizzo dello spazio su disco in genere aumenta nel tempo.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-120">**Disk space:** Disk space consumption usually increases over time.</span></span> <span data-ttu-id="bb8a9-121">Ciò è dovuto a diversi motivi, in particolare l'aumento di volume dei dati, l'esecuzione di backup del log delle transazioni, l'archiviazione dei file di traccia e l'esecuzione di snapshot di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-121">There are many reasons for this, but most of all are: data volume increases, execution of transaction log backups, storing trace files, and performing storage snapshots.</span></span> <span data-ttu-id="bb8a9-122">Pertanto, è importante toomonitor spazio su disco e gestire lo spazio su disco hello associato hello istanza grande HANA unità.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-122">Therefore, it is important toomonitor disk space usage and manage hello disk space associated with hello HANA Large Instance unit.</span></span>

## <a name="monitoring-and-troubleshooting-from-hana-side"></a><span data-ttu-id="bb8a9-123">Monitoraggio e risoluzione dei problemi dal lato HANA</span><span class="sxs-lookup"><span data-stu-id="bb8a9-123">Monitoring and troubleshooting from HANA side</span></span>

<span data-ttu-id="bb8a9-124">In ordine tooeffectively analizzare i problemi correlati tooSAP HANA in Azure (istanze di grandi dimensioni), è utile toonarrow verso il basso della causa radice hello del problema.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-124">In order tooeffectively analyze problems related tooSAP HANA on Azure (Large Instances), it is useful toonarrow down hello root cause of a problem.</span></span> <span data-ttu-id="bb8a9-125">SAP ha pubblicato una grande quantità di documentazione toohelp è.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-125">SAP has published a large amount of documentation toohelp you.</span></span>

<span data-ttu-id="bb8a9-126">Applicabile FAQ tooSAP correlati HANA prestazioni sono reperibile in hello note su SAP seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb8a9-126">Applicable FAQs related tooSAP HANA performance can be found in hello following SAP Notes:</span></span>

- [<span data-ttu-id="bb8a9-127">Nota SAP #2222200 – FAQ: rete e SAP HANA</span><span class="sxs-lookup"><span data-stu-id="bb8a9-127">SAP Note #2222200 – FAQ: SAP HANA Network</span></span>](https://launchpad.support.sap.com/#/notes/2222200)
- [<span data-ttu-id="bb8a9-128">Nota SAP #2100040 – FAQ: CPU e SAP HANA</span><span class="sxs-lookup"><span data-stu-id="bb8a9-128">SAP Note #2100040 – FAQ: SAP HANA CPU</span></span>](https://launchpad.support.sap.com/#/notes/0002100040)
- [<span data-ttu-id="bb8a9-129">Nota SAP #199997 – FAQ: memoria e SAP HANA</span><span class="sxs-lookup"><span data-stu-id="bb8a9-129">SAP Note #199997 – FAQ: SAP HANA Memory</span></span>](https://launchpad.support.sap.com/#/notes/2177064)
- [<span data-ttu-id="bb8a9-130">Nota SAP #200000 – FAQ: ottimizzazione delle prestazioni di SAP HANA</span><span class="sxs-lookup"><span data-stu-id="bb8a9-130">SAP Note #200000 – FAQ: SAP HANA Performance Optimization</span></span>](https://launchpad.support.sap.com/#/notes/2000000)
- [<span data-ttu-id="bb8a9-131">Nota SAP #199930 – FAQ: analisi dell'I/O di SAP HANA</span><span class="sxs-lookup"><span data-stu-id="bb8a9-131">SAP Note #199930 – FAQ: SAP HANA I/O Analysis</span></span>](https://launchpad.support.sap.com/#/notes/1999930)
- [<span data-ttu-id="bb8a9-132">Nota SAP #2177064 – FAQ: riavvio del servizio e interruzioni inaspettate di SAP HANA</span><span class="sxs-lookup"><span data-stu-id="bb8a9-132">SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes</span></span>](https://launchpad.support.sap.com/#/notes/2177064)

<span data-ttu-id="bb8a9-133">**Avvisi SAP HANA**</span><span class="sxs-lookup"><span data-stu-id="bb8a9-133">**SAP HANA Alerts**</span></span>

<span data-ttu-id="bb8a9-134">Come primo passaggio, verificare hello corrente SAP HANA avviso log.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-134">As a first step, check hello current SAP HANA alert logs.</span></span> <span data-ttu-id="bb8a9-135">In SAP HANA Studio andare troppo**Console di amministrazione: gli avvisi: Mostra: tutti gli avvisi**.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-135">In SAP HANA Studio, go too**Administration Console: Alerts: Show: all alerts**.</span></span> <span data-ttu-id="bb8a9-136">Questa scheda visualizzerà tutti gli avvisi di SAP HANA per valori specifici (memoria fisica disponibile, l'utilizzo della CPU e così via) che rientrano nella hello impostare minimo e massimo delle soglie.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-136">This tab will show all SAP HANA alerts for specific values (free physical memory, CPU utilization, etc.) that fall outside of hello set minimum and maximum thresholds.</span></span> <span data-ttu-id="bb8a9-137">Per impostazione predefinita i controlli vengono aggiornati automaticamente ogni 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-137">By default, checks are auto-refreshed every 15 minutes.</span></span>

![In SAP HANA Studio andare tooAdministration Console: gli avvisi: Mostra: tutti gli avvisi](./media/troubleshooting-monitoring/image1-show-alerts.png)

<span data-ttu-id="bb8a9-139">**CPU**</span><span class="sxs-lookup"><span data-stu-id="bb8a9-139">**CPU**</span></span>

<span data-ttu-id="bb8a9-140">Per un avviso generato a causa di impostazione della soglia tooimproper, valore predefinito di tooreset toohello o un valore di soglia più ragionevole è una soluzione.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-140">For an alert triggered due tooimproper threshold setting, a resolution is tooreset toohello default value or a more reasonable threshold value.</span></span>

![Valore predefinito di reimpostazione toohello o un valore di soglia accettabile](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

<span data-ttu-id="bb8a9-142">Hello seguendo gli avvisi può indicare problemi di risorse della CPU:</span><span class="sxs-lookup"><span data-stu-id="bb8a9-142">hello following alerts may indicate CPU resource problems:</span></span>

- <span data-ttu-id="bb8a9-143">Utilizzo della CPU dell'host (avviso 5)</span><span class="sxs-lookup"><span data-stu-id="bb8a9-143">Host CPU Usage (Alert 5)</span></span>
- <span data-ttu-id="bb8a9-144">Funzionamento del punto di salvataggio più recente (avviso 28)</span><span class="sxs-lookup"><span data-stu-id="bb8a9-144">Most recent savepoint operation (Alert 28)</span></span>
- <span data-ttu-id="bb8a9-145">Durata del punto di salvataggio (avviso 54)</span><span class="sxs-lookup"><span data-stu-id="bb8a9-145">Savepoint duration (Alert 54)</span></span>

<span data-ttu-id="bb8a9-146">È possibile notare elevato della CPU sul database SAP HANA da uno dei seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="bb8a9-146">You may notice high CPU consumption on your SAP HANA database from one of hello following:</span></span>

- <span data-ttu-id="bb8a9-147">L'avviso 5 (utilizzo della CPU dell'host) viene generato per l'utilizzo della CPU corrente o precedente</span><span class="sxs-lookup"><span data-stu-id="bb8a9-147">Alert 5 (Host CPU usage) is raised for current or past CPU usage</span></span>
- <span data-ttu-id="bb8a9-148">Hello visualizzato l'utilizzo della CPU nella schermata introduttiva hello</span><span class="sxs-lookup"><span data-stu-id="bb8a9-148">hello displayed CPU usage on hello overview screen</span></span>

![Visualizzato l'utilizzo della CPU nella schermata introduttiva hello](./media/troubleshooting-monitoring/image3-cpu-usage.png)

<span data-ttu-id="bb8a9-150">grafico del carico Hello potrebbe mostrare elevato della CPU, o consumo elevato nelle ultime hello:</span><span class="sxs-lookup"><span data-stu-id="bb8a9-150">hello Load graph might show high CPU consumption, or high consumption in hello past:</span></span>

![grafico del carico Hello potrebbe mostrare elevato della CPU, o consumo elevato nelle ultime hello](./media/troubleshooting-monitoring/image4-load-graph.png)

<span data-ttu-id="bb8a9-152">Un avviso generato a causa di utilizzo della CPU toohigh potrebbe essere causato da diversi motivi, ad esempio, a titolo esemplificativo: esecuzione di determinate transazioni, il caricamento dei dati, blocco di processi a esecuzione prolungata istruzioni SQL e le prestazioni delle query non valida (ad esempio, con BW su HANA cubi).</span><span class="sxs-lookup"><span data-stu-id="bb8a9-152">An alert triggered due toohigh CPU utilization could be caused by several reasons, including, but not limited to: execution of certain transactions, data loading, hanging of jobs, long running SQL statements, and bad query performance (for example, with BW on HANA cubes).</span></span>

<span data-ttu-id="bb8a9-153">Fare riferimento toohello [risoluzione dei problemi di SAP HANA: provoca correlati della CPU e le soluzioni](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) sito per i passaggi di risoluzione dei problemi dettagliata.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-153">Refer toohello [SAP HANA Troubleshooting: CPU Related Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="bb8a9-154">**Sistema operativo**</span><span class="sxs-lookup"><span data-stu-id="bb8a9-154">**Operating System**</span></span>

<span data-ttu-id="bb8a9-155">Uno dei più importante hello verifica la presenza di SAP HANA in Linux è toomake assicurarsi che le pagine di grandi dimensioni trasparente sono disabilitate, vedere [SAP nota #2131662 – trasparente enorme pagine (THP) nei server di SAP HANA](https://launchpad.support.sap.com/#/notes/2131662).</span><span class="sxs-lookup"><span data-stu-id="bb8a9-155">One of hello most important checks for SAP HANA on Linux is toomake sure that Transparent Huge Pages are disabled, see [SAP Note #2131662 – Transparent Huge Pages (THP) on SAP HANA Servers](https://launchpad.support.sap.com/#/notes/2131662).</span></span>

- <span data-ttu-id="bb8a9-156">È possibile controllare se le pagine di grandi dimensioni trasparente sono abilitate tramite hello Linux comando seguente: **cat /sys/kernel/mm/transparent\_hugepage abilitato**</span><span class="sxs-lookup"><span data-stu-id="bb8a9-156">You can check if Transparent Huge Pages are enabled through hello following Linux command: **cat /sys/kernel/mm/transparent\_hugepage/enabled**</span></span>
- <span data-ttu-id="bb8a9-157">Se _sempre_ è racchiuso tra parentesi quadre, come indicato di seguito, significa che sono abilitate le pagine di grandi dimensioni trasparente hello: [sempre] madvise mai; se _mai_ è racchiuso tra parentesi quadre, come indicato di seguito, significa che hello trasparente Pagine di grandi dimensioni sono disabilitate: sempre madvise [mai]</span><span class="sxs-lookup"><span data-stu-id="bb8a9-157">If _always_ is enclosed in brackets as below, it means that hello Transparent Huge Pages are enabled: [always] madvise never; if _never_ is enclosed in brackets as below, it means that hello Transparent Huge Pages are disabled: always madvise [never]</span></span>

<span data-ttu-id="bb8a9-158">comando Linux seguente Hello deve restituire nothing: **rpm - qa | grep ulimit.**</span><span class="sxs-lookup"><span data-stu-id="bb8a9-158">hello following Linux command should return nothing: **rpm -qa | grep ulimit.**</span></span> <span data-ttu-id="bb8a9-159">Nel caso sembrasse che _ulimit_ è installato, disinstallarlo immediatamente.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-159">If it appears _ulimit_ is installed, uninstall it immediately.</span></span>

<span data-ttu-id="bb8a9-160">**Memoria**</span><span class="sxs-lookup"><span data-stu-id="bb8a9-160">**Memory**</span></span>

<span data-ttu-id="bb8a9-161">È possibile osservare tale quantità hello della memoria allocata dall'hello SAP HANA database è supera al previsto.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-161">You may observe that hello amount of memory allocated by hello SAP HANA database is higher than expected.</span></span> <span data-ttu-id="bb8a9-162">Hello seguendo gli avvisi indica problemi con utilizzo elevato della memoria:</span><span class="sxs-lookup"><span data-stu-id="bb8a9-162">hello following alerts indicate issues with high memory usage:</span></span>

- <span data-ttu-id="bb8a9-163">Utilizzo di memoria fisica dell'host (avviso 1)</span><span class="sxs-lookup"><span data-stu-id="bb8a9-163">Host physical memory usage (Alert 1)</span></span>
- <span data-ttu-id="bb8a9-164">Utilizzo di memoria del server dei nomi (avviso 12)</span><span class="sxs-lookup"><span data-stu-id="bb8a9-164">Memory usage of name server (Alert 12)</span></span>
- <span data-ttu-id="bb8a9-165">Utilizzo di memoria totale delle tabelle columnstore (avviso 40)</span><span class="sxs-lookup"><span data-stu-id="bb8a9-165">Total memory usage of Column Store tables (Alert 40)</span></span>
- <span data-ttu-id="bb8a9-166">Utilizzo di memoria dei servizi (avviso 43)</span><span class="sxs-lookup"><span data-stu-id="bb8a9-166">Memory usage of services (Alert 43)</span></span>
- <span data-ttu-id="bb8a9-167">Utilizzo di memoria totale della risorsa di archiviazione principale delle tabelle columnstore (avviso 45)</span><span class="sxs-lookup"><span data-stu-id="bb8a9-167">Memory usage of main storage of Column Store tables (Alert 45)</span></span>
- <span data-ttu-id="bb8a9-168">File di dump di runtime (avviso 46)</span><span class="sxs-lookup"><span data-stu-id="bb8a9-168">Runtime dump files (Alert 46)</span></span>

<span data-ttu-id="bb8a9-169">Fare riferimento toohello [risoluzione dei problemi di SAP HANA: problemi di memoria](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) sito per i passaggi di risoluzione dei problemi dettagliata.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-169">Refer toohello [SAP HANA Troubleshooting: Memory Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="bb8a9-170">**Rete**</span><span class="sxs-lookup"><span data-stu-id="bb8a9-170">**Network**</span></span>

<span data-ttu-id="bb8a9-171">Fare riferimento troppo[SAP nota #2081065: risoluzione dei problemi di rete di SAP HANA](https://launchpad.support.sap.com/#/notes/2081065) ed eseguire i passaggi descritti in questa nota SAP risoluzione dei problemi di rete di hello.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-171">Refer too[SAP Note #2081065 – Troubleshooting SAP HANA Network](https://launchpad.support.sap.com/#/notes/2081065) and perform hello network troubleshooting steps in this SAP Note.</span></span>

1. <span data-ttu-id="bb8a9-172">Analisi del tempo di round trip tra client e server.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-172">Analyzing round-trip time between server and client.</span></span>
  <span data-ttu-id="bb8a9-173">R.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-173">A.</span></span> <span data-ttu-id="bb8a9-174">Esecuzione dello script SQL hello [ _HANA\_rete\_client_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="bb8a9-174">Run hello SQL script [_HANA\_Network\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>
  
2. <span data-ttu-id="bb8a9-175">Analizzare le comunicazioni internodo.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-175">Analyze internode communication.</span></span>
  <span data-ttu-id="bb8a9-176">R.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-176">A.</span></span> <span data-ttu-id="bb8a9-177">Eseguire lo script SQL [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="bb8a9-177">Run SQL script [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>

3. <span data-ttu-id="bb8a9-178">Eseguire il comando Linux **ifconfig** (output di hello Mostra se si verificano perdite di pacchetti).</span><span class="sxs-lookup"><span data-stu-id="bb8a9-178">Run Linux command **ifconfig** (hello output shows if any packet losses are occurring).</span></span>
4. <span data-ttu-id="bb8a9-179">Eseguire il comando di Linux **tcpdump**.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-179">Run Linux command **tcpdump**.</span></span>

<span data-ttu-id="bb8a9-180">Inoltre, utilizzare open source di hello [IPERF](https://iperf.fr/) strumento (o simile) toomeasure prestazioni di rete reali dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-180">Also, use hello open source [IPERF](https://iperf.fr/) tool (or similar) toomeasure real application network performance.</span></span>

<span data-ttu-id="bb8a9-181">Fare riferimento toohello [risoluzione dei problemi di SAP HANA: prestazioni di rete e problemi di connettività](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) sito per i passaggi di risoluzione dei problemi dettagliata.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-181">Refer toohello [SAP HANA Troubleshooting: Networking Performance and Connectivity Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="bb8a9-182">**Archiviazione**</span><span class="sxs-lookup"><span data-stu-id="bb8a9-182">**Storage**</span></span>

<span data-ttu-id="bb8a9-183">Dal punto di vista dell'utente finale, un'applicazione (o l'intero sistema hello) esegue risultano ridotte, non risponde o può anche sembrare toohang se esistono problemi di prestazioni dei / o.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-183">From an end-user perspective, an application (or hello system as a whole) runs sluggishly, is unresponsive, or can even seem toohang if there are issues with I/O performance.</span></span> <span data-ttu-id="bb8a9-184">In hello **volumi** scheda in SAP HANA Studio, è possibile visualizzare hello collegato volumi e i volumi sono utilizzati da ogni servizio.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-184">In hello **Volumes** tab in SAP HANA Studio, you can see hello attached volumes, and what volumes are used by each service.</span></span>

![Nella scheda di volumi hello in SAP HANA Studio, è possibile visualizzare hello collegato volumi e i volumi sono utilizzati da ogni servizio](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

<span data-ttu-id="bb8a9-186">I volumi collegati nella parte inferiore di hello della schermata di hello di che è possibile visualizzare i dettagli hello volumi, ad esempio file e le statistiche dei / o.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-186">Attached volumes in hello lower part of hello screen you can see details of hello volumes, such as files and I/O statistics.</span></span>

![I volumi collegati nella parte inferiore di hello della schermata di hello di che è possibile visualizzare i dettagli hello volumi, ad esempio file e le statistiche dei / o](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

<span data-ttu-id="bb8a9-188">Fare riferimento toohello [risoluzione dei problemi di SAP HANA: i/o relative cause e soluzioni](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) e [risoluzione dei problemi di SAP HANA: disco relative cause e soluzioni](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) sito per i passaggi di risoluzione dei problemi dettagliata.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-188">Refer toohello [SAP HANA Troubleshooting: I/O Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) and [SAP HANA Troubleshooting: Disk Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="bb8a9-189">**Strumenti di diagnostica**</span><span class="sxs-lookup"><span data-stu-id="bb8a9-189">**Diagnostic Tools**</span></span>

<span data-ttu-id="bb8a9-190">Eseguire un controllo di integrità di SAP HANA tramite HANA\_Configuration\_Minichecks.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-190">Perform an SAP HANA Health Check through HANA\_Configuration\_Minichecks.</span></span> <span data-ttu-id="bb8a9-191">Questo strumento restituisce problemi tecnici critici che dovrebbero essere già stati notificati mediante avvisi in SAP HANA Studio.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-191">This tool returns potentially critical technical issues that should have already been raised as alerts in SAP HANA Studio.</span></span>

<span data-ttu-id="bb8a9-192">Fare riferimento troppo[SAP nota #1969700 – insieme di istruzioni SQL per SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) e scaricare nota di hello SQL Statements.zip file toothat associata.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-192">Refer too[SAP Note #1969700 – SQL statement collection for SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) and download hello SQL Statements.zip file attached toothat note.</span></span> <span data-ttu-id="bb8a9-193">Archiviare il file con estensione zip sul disco rigido locale hello.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-193">Store this .zip file on hello local hard drive.</span></span>

<span data-ttu-id="bb8a9-194">In SAP HANA Studio scegliere hello **informazioni di sistema** scheda, fare doppio clic nella hello **nome** colonna e selezionare **le istruzioni SQL Import**.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-194">In SAP HANA Studio, on hello **System Information** tab, right-click in hello **Name** column and select **Import SQL Statements**.</span></span>

![In SAP HANA Studio, nella scheda informazioni di sistema hello, fare clic nella colonna nome hello e selezionare le istruzioni Import in SQL](./media/troubleshooting-monitoring/image7-import-statements-a.png)

<span data-ttu-id="bb8a9-196">Selezionare hello SQL Statements.zip file archiviato in locale e una cartella con istruzioni SQL corrispondenti hello verrà importata.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-196">Select hello SQL Statements.zip file stored locally, and a folder with hello corresponding SQL statements will be imported.</span></span> <span data-ttu-id="bb8a9-197">A questo punto, hello che molti diversi controlli di diagnostica possono essere eseguiti con queste istruzioni SQL.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-197">At this point, hello many different diagnostic checks can be run with these SQL statements.</span></span>

<span data-ttu-id="bb8a9-198">Ad esempio, requisiti di larghezza di banda replica DFS di SAP HANA tootest, fare doppio clic su hello **della larghezza di banda** istruzione in **replica: la larghezza di banda** e selezionare **aprire** Nella Console SQL.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-198">For example, tootest SAP HANA System Replication bandwidth requirements, right-click hello **Bandwidth** statement under **Replication: Bandwidth** and select **Open** in SQL Console.</span></span>

<span data-ttu-id="bb8a9-199">istruzione SQL completa Hello apre toobe consentendo di parametri di input (sezione di modifica) modificato e quindi eseguita.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-199">hello complete SQL statement opens allowing input parameters (modification section) toobe changed and then executed.</span></span>

![istruzione SQL completa Hello apre toobe consentendo di parametri di input (sezione di modifica) modificato e quindi eseguita](./media/troubleshooting-monitoring/image8-import-statements-b.png)

<span data-ttu-id="bb8a9-201">Un altro esempio è il pulsante destro su istruzioni hello in **replica: Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-201">Another example is right-clicking on hello statements under **Replication: Overview**.</span></span> <span data-ttu-id="bb8a9-202">Selezionare **Execute** dal menu di scelta rapida hello:</span><span class="sxs-lookup"><span data-stu-id="bb8a9-202">Select **Execute** from hello context menu:</span></span>

![Un altro esempio è il pulsante destro su istruzioni hello in replica: Panoramica.](./media/troubleshooting-monitoring/image9-import-statements-c.png)

<span data-ttu-id="bb8a9-205">Vengono visualizzate informazioni utili per la risoluzione dei problemi:</span><span class="sxs-lookup"><span data-stu-id="bb8a9-205">This results in information that helps with troubleshooting:</span></span>

![Vengono visualizzate informazioni utili per la risoluzione dei problemi](./media/troubleshooting-monitoring/image10-import-statements-d.png)

<span data-ttu-id="bb8a9-207">Hello stesso per HANA\_configurazione\_Minichecks e cercare eventuali _X_ segni di hello _C_ colonna (Critical).</span><span class="sxs-lookup"><span data-stu-id="bb8a9-207">Do hello same for HANA\_Configuration\_Minichecks and check for any _X_ marks in hello _C_ (Critical) column.</span></span>

<span data-ttu-id="bb8a9-208">Output di esempio:</span><span class="sxs-lookup"><span data-stu-id="bb8a9-208">Sample outputs:</span></span>

<span data-ttu-id="bb8a9-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** per controlli SAP HANA generali.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** for general SAP HANA checks.</span></span>

![HANA\_Configuration\_MiniChecks\_Rev102.01+1 per controlli SAP HANA generali](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

<span data-ttu-id="bb8a9-211">**HANA\_Services\_Overview** per una panoramica di quanto stanno eseguendo attualmente i servizi SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-211">**HANA\_Services\_Overview** for an overview of what SAP HANA services are currently running.</span></span>

![HANA\_Services\_Overview per una panoramica di quanto stanno eseguendo attualmente i servizi SAP HANA](./media/troubleshooting-monitoring/image12-services-overview.png)

<span data-ttu-id="bb8a9-213">**HANA\_Services\_Statistics** per informazioni sul servizio SAP HANA (CPU, memoria, ecc.).</span><span class="sxs-lookup"><span data-stu-id="bb8a9-213">**HANA\_Services\_Statistics** for SAP HANA service information (CPU, memory, etc.).</span></span>

![<span data-ttu-id="bb8a9-214">HANA\_Services\_Statistics per informazioni sul servizio SAP HANA</span><span class="sxs-lookup"><span data-stu-id="bb8a9-214">HANA\_Services\_Statistics for SAP HANA service information</span></span> ](./media/troubleshooting-monitoring/image13-services-statistics.png)

<span data-ttu-id="bb8a9-215">**HANA\_configurazione\_Panoramica\_Rev110 +** per informazioni generali sull'istanza di SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-215">**HANA\_Configuration\_Overview\_Rev110+** for general information on hello SAP HANA instance.</span></span>

![HANA\_configurazione\_Panoramica\_Rev110 + per informazioni generali sull'istanza di SAP HANA hello](./media/troubleshooting-monitoring/image14-configuration-overview.png)

<span data-ttu-id="bb8a9-217">**HANA\_configurazione\_parametri\_Rev70 +** toocheck i parametri di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="bb8a9-217">**HANA\_Configuration\_Parameters\_Rev70+** toocheck SAP HANA parameters.</span></span>

![HANA\_configurazione\_parametri\_i parametri di SAP HANA toocheck Rev70 +](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

