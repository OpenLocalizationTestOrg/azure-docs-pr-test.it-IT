---
title: procedura dettagliata sulla soluzione di Azure IoT Suite factory aaaConnected | Documenti Microsoft
description: Una descrizione di hello Azure IoT preconfigurato soluzione connesso factory e dalla relativa architettura.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 7fd55c51351659401349cfde91a20fce1045b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a><span data-ttu-id="33aa3-103">Procedura dettagliata per la soluzione preconfigurata di connected factory</span><span class="sxs-lookup"><span data-stu-id="33aa3-103">Connected factory preconfigured solution walkthrough</span></span>

<span data-ttu-id="33aa3-104">Hello IoT Suite connesso factory [preconfigurato soluzione] [ lnk-preconfigured-solutions] è un'implementazione di una soluzione industriale end-to-end che:</span><span class="sxs-lookup"><span data-stu-id="33aa3-104">hello IoT Suite connected factory [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end industrial solution that:</span></span>

* <span data-ttu-id="33aa3-105">Consente di connettere i dispositivi di settore tooboth simulato server in esecuzione OPC UA nelle righe di produzione simulato factory e dispositivi server UA OPC.</span><span class="sxs-lookup"><span data-stu-id="33aa3-105">Connects tooboth simulated industrial devices running OPC UA servers in simulated factory production lines, and real OPC UA server devices.</span></span> <span data-ttu-id="33aa3-106">Per ulteriori informazioni su OPC UA, vedere hello [connesso domande frequenti sulla factory](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="33aa3-106">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="33aa3-107">Visualizza KPI e OEE di tali dispositivi e delle linee di produzione.</span><span class="sxs-lookup"><span data-stu-id="33aa3-107">Shows operational KPIs and OEE of those devices and production lines.</span></span>
* <span data-ttu-id="33aa3-108">Viene illustrato come un'applicazione basata su cloud potrebbe essere toointeract utilizzati con i sistemi server UA OPC.</span><span class="sxs-lookup"><span data-stu-id="33aa3-108">Demonstrates how a cloud-based application could be used toointeract with OPC UA server systems.</span></span>
* <span data-ttu-id="33aa3-109">Consente di tooconnect dispositivi server UA OPC.</span><span class="sxs-lookup"><span data-stu-id="33aa3-109">Enables you tooconnect your own OPC UA server devices.</span></span>
* <span data-ttu-id="33aa3-110">Consente di toobrowse e modificare i dati del server OPC UA hello.</span><span class="sxs-lookup"><span data-stu-id="33aa3-110">Enables you toobrowse and modify hello OPC UA server data.</span></span>
* <span data-ttu-id="33aa3-111">Si integra con hello Azure ora serie Insights (STI) servizio tooprovide visualizzazioni personalizzate dei dati di hello dai server UA OPC.</span><span class="sxs-lookup"><span data-stu-id="33aa3-111">Integrates with hello Azure Time Series Insights (TSI) service tooprovide customized views of hello data from your OPC UA servers.</span></span>

<span data-ttu-id="33aa3-112">È possibile utilizzare la soluzione hello come punto di partenza per la propria implementazione e [personalizzare] [ lnk-customize] è toomeet i requisiti aziendali specifici.</span><span class="sxs-lookup"><span data-stu-id="33aa3-112">You can use hello solution as a starting point for your own implementation and [customize][lnk-customize] it toomeet your own specific business requirements.</span></span>

<span data-ttu-id="33aa3-113">Questo articolo vengono illustrati alcuni elementi chiave hello, di hello connesso factory soluzione tooenable toounderstand il funzionamento.</span><span class="sxs-lookup"><span data-stu-id="33aa3-113">This article walks you through some of hello key elements of hello connected factory solution tooenable you toounderstand how it works.</span></span> <span data-ttu-id="33aa3-114">Queste informazioni consentono di:</span><span class="sxs-lookup"><span data-stu-id="33aa3-114">This knowledge helps you to:</span></span>

* <span data-ttu-id="33aa3-115">Risolvere i problemi nella soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="33aa3-115">Troubleshoot issues in hello solution.</span></span>
* <span data-ttu-id="33aa3-116">Pianificare la modalità toocustomize toohello soluzione toomeet esigenze specifiche.</span><span class="sxs-lookup"><span data-stu-id="33aa3-116">Plan how toocustomize toohello solution toomeet your own specific requirements.</span></span>
* <span data-ttu-id="33aa3-117">Progettare la propria soluzione IoT che usa i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="33aa3-117">Design your own IoT solution that uses Azure services.</span></span>

<span data-ttu-id="33aa3-118">Per ulteriori informazioni, vedere hello [connesso domande frequenti sulla factory](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="33aa3-118">For more information, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="33aa3-119">Architettura logica</span><span class="sxs-lookup"><span data-stu-id="33aa3-119">Logical architecture</span></span>

<span data-ttu-id="33aa3-120">Hello seguente diagramma illustra i componenti logici hello della soluzione preconfigurata hello:</span><span class="sxs-lookup"><span data-stu-id="33aa3-120">hello following diagram outlines hello logical components of hello preconfigured solution:</span></span>

![Architettura logica di connected factory][connected-factory-logical]

## <a name="communication-patterns"></a><span data-ttu-id="33aa3-122">Modelli di comunicazione</span><span class="sxs-lookup"><span data-stu-id="33aa3-122">Communication patterns</span></span>

<span data-ttu-id="33aa3-123">soluzione Hello utilizza hello [specifica OPC UA Pub/Sub](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend OPC UA telemetria dati tooIoT Hub in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="33aa3-123">hello solution uses hello [OPC UA Pub/Sub specification](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend OPC UA telemetry data tooIoT Hub in JSON format.</span></span> <span data-ttu-id="33aa3-124">soluzione Hello utilizza hello [Publisher OPC](https://github.com/Azure/iot-edge-opc-publisher) modulo IoT Edge per questo scopo.</span><span class="sxs-lookup"><span data-stu-id="33aa3-124">hello solution uses hello [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) IoT Edge module for this purpose.</span></span>

<span data-ttu-id="33aa3-125">soluzione Hello ha anche un client di OPC UA integrato in un'applicazione web in grado di stabilire connessioni con server OPC UA locali.</span><span class="sxs-lookup"><span data-stu-id="33aa3-125">hello solution also has an OPC UA client integrated into a web application that can establish connections with on-premises OPC UA servers.</span></span> <span data-ttu-id="33aa3-126">Hello client utilizza un [proxy inverso](https://wikipedia.org/wiki/Reverse_proxy) e riceve la Guida dalla connessione di IoT Hub toomake hello senza che sia necessario aprire le porte nel firewall locale hello.</span><span class="sxs-lookup"><span data-stu-id="33aa3-126">hello client uses a [reverse-proxy](https://wikipedia.org/wiki/Reverse_proxy) and receives help from IoT Hub toomake hello connection without requiring open ports in hello on-premises firewall.</span></span> <span data-ttu-id="33aa3-127">Questo modello di comunicazione è denominato [modello di comunicazione assistita con servizi](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span><span class="sxs-lookup"><span data-stu-id="33aa3-127">This communication pattern is called [service-assisted communication](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span></span> <span data-ttu-id="33aa3-128">soluzione Hello utilizza hello [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) modulo IoT Edge per questo scopo.</span><span class="sxs-lookup"><span data-stu-id="33aa3-128">hello solution uses hello [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) IoT Edge module for this purpose.</span></span>


## <a name="simulation"></a><span data-ttu-id="33aa3-129">Simulazione</span><span class="sxs-lookup"><span data-stu-id="33aa3-129">Simulation</span></span>

<span data-ttu-id="33aa3-130">Hello simulati stazioni e l'esecuzione di produzione hello simulato sistemi (MES) costituiscono una linea di produzione di factory.</span><span class="sxs-lookup"><span data-stu-id="33aa3-130">hello simulated stations and hello simulated manufacturing execution systems (MES) make up a factory production line.</span></span> <span data-ttu-id="33aa3-131">Hello dispositivi simulati e hello OPC Publisher modulo sono basati su hello [OPC UA .NET Standard] [ lnk-OPC-UA-NET-Standard] pubblicati da hello Foundation OPC.</span><span class="sxs-lookup"><span data-stu-id="33aa3-131">hello simulated devices and hello OPC Publisher Module are based on hello [OPC UA .NET Standard][lnk-OPC-UA-NET-Standard] published by hello OPC Foundation.</span></span>

<span data-ttu-id="33aa3-132">Hello OPC Proxy e server di pubblicazione OPC vengono implementati come moduli basati su [Azure IoT Edge][lnk-Azure-IoT-Gateway].</span><span class="sxs-lookup"><span data-stu-id="33aa3-132">hello OPC Proxy and OPC Publisher are implemented as modules based on [Azure IoT Edge][lnk-Azure-IoT-Gateway].</span></span> <span data-ttu-id="33aa3-133">Ogni linea di produzione simulata ha un gateway designato collegato.</span><span class="sxs-lookup"><span data-stu-id="33aa3-133">Each simulated production line has a designated gateway attached.</span></span>

<span data-ttu-id="33aa3-134">Tutti i componenti di simulazione vengono eseguiti in contenitori Docker ospitati in una macchina virtuale Linux di Azure.</span><span class="sxs-lookup"><span data-stu-id="33aa3-134">All simulation components run in Docker containers  hosted in an Azure Linux VM.</span></span> <span data-ttu-id="33aa3-135">simulazione di Hello è configurato toorun otto simulato le righe di produzione per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="33aa3-135">hello simulation is configured toorun eight simulated production lines by default.</span></span>

## <a name="simulated-production-line"></a><span data-ttu-id="33aa3-136">Linea di produzione simulata</span><span class="sxs-lookup"><span data-stu-id="33aa3-136">Simulated production line</span></span>

<span data-ttu-id="33aa3-137">Una linea di produzione produce parti.</span><span class="sxs-lookup"><span data-stu-id="33aa3-137">A production line manufactures parts.</span></span> <span data-ttu-id="33aa3-138">È composta da postazioni diverse, ovvero montaggio, collaudo e imballaggio.</span><span class="sxs-lookup"><span data-stu-id="33aa3-138">It is composed of different stations: an assembly station, a test station, and a packaging station.</span></span>

<span data-ttu-id="33aa3-139">simulazione di Hello viene eseguito e aggiorna i dati di hello esposto tramite nodi OPC UA hello.</span><span class="sxs-lookup"><span data-stu-id="33aa3-139">hello simulation runs and updates hello data that is exposed through hello OPC UA nodes.</span></span> <span data-ttu-id="33aa3-140">Tutte le stazioni line simulato di produzione vengono orchestrate da hello MES tramite UA OPC.</span><span class="sxs-lookup"><span data-stu-id="33aa3-140">All simulated production line stations are orchestrated by hello MES through OPC UA.</span></span>

## <a name="simulated-manufacturing-execution-system"></a><span data-ttu-id="33aa3-141">MES (Manufacturing Execution System) simulato</span><span class="sxs-lookup"><span data-stu-id="33aa3-141">Simulated manufacturing execution system</span></span>

<span data-ttu-id="33aa3-142">Hello MES controlla ogni stazione in linea di produzione hello tramite modifiche dello stato di OPC UA toodetect stazione.</span><span class="sxs-lookup"><span data-stu-id="33aa3-142">hello MES monitors each station in hello production line through OPC UA toodetect station status changes.</span></span> <span data-ttu-id="33aa3-143">Chiama OPC UA stazioni di metodi toocontrol hello e passa un prodotto da una postazione toohello Avanti fino al completamento.</span><span class="sxs-lookup"><span data-stu-id="33aa3-143">It calls OPC UA methods toocontrol hello stations and passes a product from one station toohello next until it is complete.</span></span>

## <a name="gateway-opc-publisher-module"></a><span data-ttu-id="33aa3-144">Modulo di pubblicazione OPC del gateway</span><span class="sxs-lookup"><span data-stu-id="33aa3-144">Gateway OPC publisher module</span></span>

<span data-ttu-id="33aa3-145">Modulo di server di pubblicazione OPC connette toohello stazione OPC UA server e sottoscrive toohello OPC nodi toobe pubblicato.</span><span class="sxs-lookup"><span data-stu-id="33aa3-145">OPC Publisher Module connects toohello station OPC UA servers and subscribes toohello OPC nodes toobe published.</span></span> <span data-ttu-id="33aa3-146">modulo Hello converte i dati del nodo hello in formato JSON, crittografa e invia tooIoT Hub come messaggi OPC UA pubblicazione/sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="33aa3-146">hello module converts hello node data into JSON format, encrypts it, and sends it tooIoT Hub as OPC UA Pub/Sub messages.</span></span>

<span data-ttu-id="33aa3-147">modulo server di pubblicazione OPC Hello solo richiede una porta in uscita https (443) e può funzionare con un'infrastruttura aziendale esistente.</span><span class="sxs-lookup"><span data-stu-id="33aa3-147">hello OPC Publisher module only requires an outbound https port (443) and can work with existing enterprise infrastructure.</span></span>

## <a name="gateway-opc-proxy-module"></a><span data-ttu-id="33aa3-148">Modulo proxy OPC del gateway</span><span class="sxs-lookup"><span data-stu-id="33aa3-148">Gateway OPC proxy module</span></span>

<span data-ttu-id="33aa3-149">Hello Gateway OPC UA Proxy modulo tunnel messaggi di comando e controllo UA OPC binari e richiede solo una porta in uscita https (443).</span><span class="sxs-lookup"><span data-stu-id="33aa3-149">hello Gateway OPC UA Proxy Module tunnels binary OPC UA command and control messages and only requires an outbound https port (443).</span></span> <span data-ttu-id="33aa3-150">Può funzionare con l'infrastruttura aziendale esistente, inclusi i proxy Web.</span><span class="sxs-lookup"><span data-stu-id="33aa3-150">It can work with existing enterprise infrastructure, including Web Proxies.</span></span>

<span data-ttu-id="33aa3-151">Utilizza dispositivo Hub IoT metodi tootransfer delicate TCP/IP dati a livello di applicazione hello e garantisce pertanto trust endpoint, la crittografia dei dati e l'integrità mediante SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="33aa3-151">It uses IoT Hub Device methods tootransfer packetized TCP/IP data at hello application layer and thus ensures endpoint trust, data encryption, and integrity using SSL/TLS.</span></span>

<span data-ttu-id="33aa3-152">protocollo binario di OPC UA inoltrato tramite proxy hello Hello Usa la crittografia e autenticazione agente utente.</span><span class="sxs-lookup"><span data-stu-id="33aa3-152">hello OPC UA binary protocol relayed through hello proxy itself uses UA authentication and encryption.</span></span>

## <a name="azure-time-series-insights"></a><span data-ttu-id="33aa3-153">Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="33aa3-153">Azure Time Series Insights</span></span>

<span data-ttu-id="33aa3-154">Hello Gateway OPC Publisher modulo sottoscrive tooOPC UA server nodi toodetect modifica i valori dei dati hello.</span><span class="sxs-lookup"><span data-stu-id="33aa3-154">hello Gateway OPC Publisher Module subscribes tooOPC UA server nodes toodetect change in hello data values.</span></span> <span data-ttu-id="33aa3-155">Se viene rilevata una modifica di dati in uno dei nodi di hello, questo modulo Invia messaggi tooAzure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="33aa3-155">If a data change is detected in one of hello nodes, this module then sends messages tooAzure IoT Hub.</span></span>

<span data-ttu-id="33aa3-156">IoT Hub fornisce un tooAzure origine evento STI.</span><span class="sxs-lookup"><span data-stu-id="33aa3-156">IoT Hub provides an event source tooAzure TSI.</span></span> <span data-ttu-id="33aa3-157">STI archivia i dati per 30 giorni basate sui timestamp associato toohello messaggi.</span><span class="sxs-lookup"><span data-stu-id="33aa3-157">TSI stores data for 30 days based on timestamps attached toohello messages.</span></span> <span data-ttu-id="33aa3-158">Questi dati includono:</span><span class="sxs-lookup"><span data-stu-id="33aa3-158">This data includes:</span></span>

* <span data-ttu-id="33aa3-159">ApplicationUri OPC UA</span><span class="sxs-lookup"><span data-stu-id="33aa3-159">OPC UA ApplicationUri</span></span>
* <span data-ttu-id="33aa3-160">NodeId OPC UA</span><span class="sxs-lookup"><span data-stu-id="33aa3-160">OPC UA NodeId</span></span>
* <span data-ttu-id="33aa3-161">Valore del nodo hello</span><span class="sxs-lookup"><span data-stu-id="33aa3-161">Value of hello node</span></span>
* <span data-ttu-id="33aa3-162">Timestamp di origine</span><span class="sxs-lookup"><span data-stu-id="33aa3-162">Source timestamp</span></span>
* <span data-ttu-id="33aa3-163">DisplayName OPC UA</span><span class="sxs-lookup"><span data-stu-id="33aa3-163">OPC UA DisplayName</span></span>

<span data-ttu-id="33aa3-164">Attualmente, STI non consentono i clienti desiderano dati hello tookeep per quanto tempo toocustomize.</span><span class="sxs-lookup"><span data-stu-id="33aa3-164">Currently, TSI does not allow customers toocustomize how long they wish tookeep hello data for.</span></span>

<span data-ttu-id="33aa3-165">Time Series Insights esegue query sui dati del nodo usando una funzione SearchSpan (Time.From, Time.To) ed esegue l'aggregazione in base ad ApplicationUri OPC UA, NodeId OPC UA oppure DisplayName OPC UA.</span><span class="sxs-lookup"><span data-stu-id="33aa3-165">TSI queries against node data using a SearchSpan (Time.From, Time.To) and aggregates by OPC UA ApplicationUri or OPC UA NodeId or OPC UA DisplayName.</span></span>

<span data-ttu-id="33aa3-166">dati di hello tooretrieve per hello OEE e indicatori KPI misuratori e grafici di serie temporali hello, i dati vengono aggregati per numero di eventi, Sum, Avg, Min e Max.</span><span class="sxs-lookup"><span data-stu-id="33aa3-166">tooretrieve hello data for hello OEE and KPI gauges, and hello time series charts, data is aggregated by count of events, Sum, Avg, Min, and Max.</span></span>

<span data-ttu-id="33aa3-167">serie temporale Hello vengono compilate mediante un processo diverso.</span><span class="sxs-lookup"><span data-stu-id="33aa3-167">hello time series are built using a different process.</span></span> <span data-ttu-id="33aa3-168">OEE e indicatori KPI vengono calcolati dai dati di base di stazione e trasmessi a topologia hello (righe di produzione, le factory, enterprise) in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="33aa3-168">OEE and KPIs are calculated from station base data and bubbled up for hello topology (production lines, factories, enterprise) in hello application.</span></span>

<span data-ttu-id="33aa3-169">Inoltre, serie temporale per topologia OEE e un indicatore KPI viene calcolato in app hello, ogni volta che un intervallo di tempo visualizzato è pronto.</span><span class="sxs-lookup"><span data-stu-id="33aa3-169">Additionally, time series for OEE and KPI topology is calculated in hello app, whenever a displayed timespan is ready.</span></span> <span data-ttu-id="33aa3-170">Ad esempio, visualizzazione giorno hello viene aggiornato ogni ora completa.</span><span class="sxs-lookup"><span data-stu-id="33aa3-170">For example, hello day view is updated every full hour.</span></span>

<span data-ttu-id="33aa3-171">visualizzazione di Hello time serie di dati del nodo provenienti direttamente da STI utilizzando un'aggregazione per timespan.</span><span class="sxs-lookup"><span data-stu-id="33aa3-171">hello time series view of node data comes directly from TSI using an aggregation for timespan.</span></span>

## <a name="iot-hub"></a><span data-ttu-id="33aa3-172">Hub IoT</span><span class="sxs-lookup"><span data-stu-id="33aa3-172">IoT Hub</span></span>
<span data-ttu-id="33aa3-173">Hello [hub IoT] [ lnk-IoT Hub] riceve i dati inviati da hello OPC Publisher modulo in cloud hello e rende il servizio di Azure STI toohello disponibili.</span><span class="sxs-lookup"><span data-stu-id="33aa3-173">hello [IoT hub][lnk-IoT Hub] receives data sent from hello OPC Publisher Module into hello cloud and makes it available toohello Azure TSI service.</span></span> 

<span data-ttu-id="33aa3-174">Hello IoT Hub nella soluzione hello inoltre:</span><span class="sxs-lookup"><span data-stu-id="33aa3-174">hello IoT Hub in hello solution also:</span></span>
- <span data-ttu-id="33aa3-175">Gestisce un registro di sistema di identità che archivia gli ID hello per tutti OPC Publisher modulo e tutti i moduli di Proxy OPC.</span><span class="sxs-lookup"><span data-stu-id="33aa3-175">Maintains an identity registry that stores hello IDs for all OPC Publisher Module and all OPC Proxy Modules.</span></span>
- <span data-ttu-id="33aa3-176">Viene utilizzato come canale di trasporto per la comunicazione bidirezionale di hello modulo Proxy OPC.</span><span class="sxs-lookup"><span data-stu-id="33aa3-176">Is used as transport channel for bidirectional communication of hello OPC Proxy Module.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="33aa3-177">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="33aa3-177">Azure Storage</span></span>
<span data-ttu-id="33aa3-178">soluzione Hello utilizza l'archiviazione blob di Azure come archiviazione su disco per i dati di distribuzione di macchina virtuale e toostore hello.</span><span class="sxs-lookup"><span data-stu-id="33aa3-178">hello solution uses Azure blob storage as disk storage for hello VM and toostore deployment data.</span></span>

## <a name="web-app"></a><span data-ttu-id="33aa3-179">App Web</span><span class="sxs-lookup"><span data-stu-id="33aa3-179">Web app</span></span>
<span data-ttu-id="33aa3-180">app web Hello distribuita come parte della soluzione hello preconfigurato è costituito da un client OPC UA integrato, di elaborazione degli avvisi e visualizzazione di dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="33aa3-180">hello web app deployed as part of hello preconfigured solution comprises of an integrated OPC UA client, alerts processing and telemetry visualization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33aa3-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="33aa3-181">Next steps</span></span>

<span data-ttu-id="33aa3-182">È possibile continuare introduzione IoT Suite leggendo hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="33aa3-182">You can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="33aa3-183">[Autorizzazioni nel sito azureiotsuite.com hello][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="33aa3-183">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="33aa3-184">Distribuire un gateway in Windows o Linux per la soluzione factory preconfigurato hello connesso</span><span class="sxs-lookup"><span data-stu-id="33aa3-184">Deploy a gateway on Windows or Linux for hello connected factory preconfigured solution</span></span>](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
