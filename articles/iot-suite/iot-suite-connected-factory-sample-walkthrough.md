---
title: Procedura dettagliata per la soluzione di connected factory di Azure IoT Suite | Microsoft Docs
description: Descrizione della soluzione preconfigurata di connected factory di Azure IoT e della relativa architettura.
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
ms.openlocfilehash: 517e908a744734139ed0aeee314a4f3b9eda86cc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a><span data-ttu-id="c2da9-103">Procedura dettagliata per la soluzione preconfigurata di connected factory</span><span class="sxs-lookup"><span data-stu-id="c2da9-103">Connected factory preconfigured solution walkthrough</span></span>

<span data-ttu-id="c2da9-104">La [soluzione preconfigurata ][lnk-preconfigured-solutions] di connected factory di IoT Suite rappresenta l'implementazione di una soluzione industriale end-to-end che:</span><span class="sxs-lookup"><span data-stu-id="c2da9-104">The IoT Suite connected factory [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end industrial solution that:</span></span>

* <span data-ttu-id="c2da9-105">Si connette sia a dispositivi industriali simulati che eseguono server OPC UA in linee di produzione simulate degli stabilimenti, sia a dispositivi server OPC UA reali.</span><span class="sxs-lookup"><span data-stu-id="c2da9-105">Connects to both simulated industrial devices running OPC UA servers in simulated factory production lines, and real OPC UA server devices.</span></span> <span data-ttu-id="c2da9-106">Per altre informazioni su OPC UA, vedere le [domande frequenti sulla soluzione di connected factory](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="c2da9-106">For more information about OPC UA, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="c2da9-107">Visualizza KPI e OEE di tali dispositivi e delle linee di produzione.</span><span class="sxs-lookup"><span data-stu-id="c2da9-107">Shows operational KPIs and OEE of those devices and production lines.</span></span>
* <span data-ttu-id="c2da9-108">Dimostra come usare un'applicazione basata sul cloud per interagire con i sistemi server OPC UA.</span><span class="sxs-lookup"><span data-stu-id="c2da9-108">Demonstrates how a cloud-based application could be used to interact with OPC UA server systems.</span></span>
* <span data-ttu-id="c2da9-109">Consente di connettere i propri dispositivi server OPC UA.</span><span class="sxs-lookup"><span data-stu-id="c2da9-109">Enables you to connect your own OPC UA server devices.</span></span>
* <span data-ttu-id="c2da9-110">Consente di esplorare e modificare i dati dei server OPC UA.</span><span class="sxs-lookup"><span data-stu-id="c2da9-110">Enables you to browse and modify the OPC UA server data.</span></span>
* <span data-ttu-id="c2da9-111">Si integra con il servizio Azure Time Series Insights (TSI) per fornire visualizzazioni personalizzate dei dati dei server OPC UA.</span><span class="sxs-lookup"><span data-stu-id="c2da9-111">Integrates with the Azure Time Series Insights (TSI) service to provide customized views of the data from your OPC UA servers.</span></span>

<span data-ttu-id="c2da9-112">È possibile usare la soluzione come punto di partenza per l'implementazione e [personalizzarla][lnk-customize] in base ai requisiti aziendali specifici.</span><span class="sxs-lookup"><span data-stu-id="c2da9-112">You can use the solution as a starting point for your own implementation and [customize][lnk-customize] it to meet your own specific business requirements.</span></span>

<span data-ttu-id="c2da9-113">Questo articolo illustra alcuni degli elementi principali della soluzione di connected factory per comprenderne il funzionamento.</span><span class="sxs-lookup"><span data-stu-id="c2da9-113">This article walks you through some of the key elements of the connected factory solution to enable you to understand how it works.</span></span> <span data-ttu-id="c2da9-114">Queste informazioni consentono di:</span><span class="sxs-lookup"><span data-stu-id="c2da9-114">This knowledge helps you to:</span></span>

* <span data-ttu-id="c2da9-115">Risolvere i problemi nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="c2da9-115">Troubleshoot issues in the solution.</span></span>
* <span data-ttu-id="c2da9-116">Pianificare come personalizzare la soluzione per soddisfare requisiti specifici.</span><span class="sxs-lookup"><span data-stu-id="c2da9-116">Plan how to customize to the solution to meet your own specific requirements.</span></span>
* <span data-ttu-id="c2da9-117">Progettare la propria soluzione IoT che usa i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="c2da9-117">Design your own IoT solution that uses Azure services.</span></span>

<span data-ttu-id="c2da9-118">Per altre informazioni, vedere le [domande frequenti sulla soluzione di connected factory](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="c2da9-118">For more information, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="c2da9-119">Architettura logica</span><span class="sxs-lookup"><span data-stu-id="c2da9-119">Logical architecture</span></span>

<span data-ttu-id="c2da9-120">Il diagramma seguente illustra i componenti logici della soluzione preconfigurata:</span><span class="sxs-lookup"><span data-stu-id="c2da9-120">The following diagram outlines the logical components of the preconfigured solution:</span></span>

![Architettura logica di connected factory][connected-factory-logical]

## <a name="communication-patterns"></a><span data-ttu-id="c2da9-122">Modelli di comunicazione</span><span class="sxs-lookup"><span data-stu-id="c2da9-122">Communication patterns</span></span>

<span data-ttu-id="c2da9-123">La soluzione usa la [specifica OPC UA Pub/Sub](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) per inviare i dati di telemetria OPC UA all'hub IoT in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="c2da9-123">The solution uses the [OPC UA Pub/Sub specification](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) to send OPC UA telemetry data to IoT Hub in JSON format.</span></span> <span data-ttu-id="c2da9-124">La soluzione usa il [modulo di pubblicazione OPC](https://github.com/Azure/iot-edge-opc-publisher) IoT Edge per questo scopo.</span><span class="sxs-lookup"><span data-stu-id="c2da9-124">The solution uses the [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) IoT Edge module for this purpose.</span></span>

<span data-ttu-id="c2da9-125">La soluzione ha anche un client OPC UA integrato in un'applicazione Web che può stabilire connessioni con server OPC UA locali.</span><span class="sxs-lookup"><span data-stu-id="c2da9-125">The solution also has an OPC UA client integrated into a web application that can establish connections with on-premises OPC UA servers.</span></span> <span data-ttu-id="c2da9-126">Il client usa un [proxy inverso](https://wikipedia.org/wiki/Reverse_proxy) e riceve assistenza dall'hub IoT per stabilire la connessione senza che sia necessario aprire le porte nel firewall locale.</span><span class="sxs-lookup"><span data-stu-id="c2da9-126">The client uses a [reverse-proxy](https://wikipedia.org/wiki/Reverse_proxy) and receives help from IoT Hub to make the connection without requiring open ports in the on-premises firewall.</span></span> <span data-ttu-id="c2da9-127">Questo modello di comunicazione è denominato [modello di comunicazione assistita con servizi](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span><span class="sxs-lookup"><span data-stu-id="c2da9-127">This communication pattern is called [service-assisted communication](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span></span> <span data-ttu-id="c2da9-128">La soluzione usa il modulo [proxy OPC](https://github.com/Azure/iot-edge-opc-proxy/) IoT Edge per questo scopo.</span><span class="sxs-lookup"><span data-stu-id="c2da9-128">The solution uses the [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) IoT Edge module for this purpose.</span></span>


## <a name="simulation"></a><span data-ttu-id="c2da9-129">Simulazione</span><span class="sxs-lookup"><span data-stu-id="c2da9-129">Simulation</span></span>

<span data-ttu-id="c2da9-130">Le postazioni simulate e i sistemi MES (Manufacturing Execution Systems) simulati costituiscono una linea di produzione dello stabilimento.</span><span class="sxs-lookup"><span data-stu-id="c2da9-130">The simulated stations and the simulated manufacturing execution systems (MES) make up a factory production line.</span></span> <span data-ttu-id="c2da9-131">I dispositivi simulati e il modulo di pubblicazione OPC si basano sullo [standard OPC UA .NET][lnk-OPC-UA-NET-Standard] pubblicato dalla OPC Foundation.</span><span class="sxs-lookup"><span data-stu-id="c2da9-131">The simulated devices and the OPC Publisher Module are based on the [OPC UA .NET Standard][lnk-OPC-UA-NET-Standard] published by the OPC Foundation.</span></span>

<span data-ttu-id="c2da9-132">Il proxy OPC e il modulo di pubblicazione OPC vengono implementati come moduli basati su [Azure IoT Edge][lnk-Azure-IoT-Gateway].</span><span class="sxs-lookup"><span data-stu-id="c2da9-132">The OPC Proxy and OPC Publisher are implemented as modules based on [Azure IoT Edge][lnk-Azure-IoT-Gateway].</span></span> <span data-ttu-id="c2da9-133">Ogni linea di produzione simulata ha un gateway designato collegato.</span><span class="sxs-lookup"><span data-stu-id="c2da9-133">Each simulated production line has a designated gateway attached.</span></span>

<span data-ttu-id="c2da9-134">Tutti i componenti di simulazione vengono eseguiti in contenitori Docker ospitati in una macchina virtuale Linux di Azure.</span><span class="sxs-lookup"><span data-stu-id="c2da9-134">All simulation components run in Docker containers  hosted in an Azure Linux VM.</span></span> <span data-ttu-id="c2da9-135">Per impostazione predefinita, la simulazione è configurata per l'esecuzione di otto linee di produzione simulate.</span><span class="sxs-lookup"><span data-stu-id="c2da9-135">The simulation is configured to run eight simulated production lines by default.</span></span>

## <a name="simulated-production-line"></a><span data-ttu-id="c2da9-136">Linea di produzione simulata</span><span class="sxs-lookup"><span data-stu-id="c2da9-136">Simulated production line</span></span>

<span data-ttu-id="c2da9-137">Una linea di produzione produce parti.</span><span class="sxs-lookup"><span data-stu-id="c2da9-137">A production line manufactures parts.</span></span> <span data-ttu-id="c2da9-138">È composta da postazioni diverse, ovvero montaggio, collaudo e imballaggio.</span><span class="sxs-lookup"><span data-stu-id="c2da9-138">It is composed of different stations: an assembly station, a test station, and a packaging station.</span></span>

<span data-ttu-id="c2da9-139">La simulazione viene eseguita e aggiorna i dati esposti tramite i nodi OPC UA.</span><span class="sxs-lookup"><span data-stu-id="c2da9-139">The simulation runs and updates the data that is exposed through the OPC UA nodes.</span></span> <span data-ttu-id="c2da9-140">Tutte le postazioni della linea di produzione simulata sono coordinate dal sistema MES tramite OPC UA.</span><span class="sxs-lookup"><span data-stu-id="c2da9-140">All simulated production line stations are orchestrated by the MES through OPC UA.</span></span>

## <a name="simulated-manufacturing-execution-system"></a><span data-ttu-id="c2da9-141">MES (Manufacturing Execution System) simulato</span><span class="sxs-lookup"><span data-stu-id="c2da9-141">Simulated manufacturing execution system</span></span>

<span data-ttu-id="c2da9-142">Il MES monitora ogni postazione nella linea di produzione tramite OPC UA per rilevare le modifiche di stato della postazione stessa.</span><span class="sxs-lookup"><span data-stu-id="c2da9-142">The MES monitors each station in the production line through OPC UA to detect station status changes.</span></span> <span data-ttu-id="c2da9-143">Chiama metodi OPC UA per controllare le postazioni e trasferisce un prodotto da una postazione all'altra finché non è completo.</span><span class="sxs-lookup"><span data-stu-id="c2da9-143">It calls OPC UA methods to control the stations and passes a product from one station to the next until it is complete.</span></span>

## <a name="gateway-opc-publisher-module"></a><span data-ttu-id="c2da9-144">Modulo di pubblicazione OPC del gateway</span><span class="sxs-lookup"><span data-stu-id="c2da9-144">Gateway OPC publisher module</span></span>

<span data-ttu-id="c2da9-145">Il modulo di pubblicazione OPC si connette ai server OPC UA della postazione ed effettua la sottoscrizione ai nodi OPC da pubblicare.</span><span class="sxs-lookup"><span data-stu-id="c2da9-145">OPC Publisher Module connects to the station OPC UA servers and subscribes to the OPC nodes to be published.</span></span> <span data-ttu-id="c2da9-146">Il modulo converte i dati del nodo in formato JSON, li crittografa e li invia all'hub IoT come messaggi di pubblicazione/sottoscrizione OPC UA.</span><span class="sxs-lookup"><span data-stu-id="c2da9-146">The module converts the node data into JSON format, encrypts it, and sends it to IoT Hub as OPC UA Pub/Sub messages.</span></span>

<span data-ttu-id="c2da9-147">Il modulo di pubblicazione OPC richiede solo una porta HTTPS in uscita (443) e può funzionare con l'infrastruttura aziendale esistente.</span><span class="sxs-lookup"><span data-stu-id="c2da9-147">The OPC Publisher module only requires an outbound https port (443) and can work with existing enterprise infrastructure.</span></span>

## <a name="gateway-opc-proxy-module"></a><span data-ttu-id="c2da9-148">Modulo proxy OPC del gateway</span><span class="sxs-lookup"><span data-stu-id="c2da9-148">Gateway OPC proxy module</span></span>

<span data-ttu-id="c2da9-149">Il modulo proxy OPC UA del gateway effettua il tunnel dei messaggi di comando e controllo OPC UA binari e richiede solo una porta HTTPS in uscita (443).</span><span class="sxs-lookup"><span data-stu-id="c2da9-149">The Gateway OPC UA Proxy Module tunnels binary OPC UA command and control messages and only requires an outbound https port (443).</span></span> <span data-ttu-id="c2da9-150">Può funzionare con l'infrastruttura aziendale esistente, inclusi i proxy Web.</span><span class="sxs-lookup"><span data-stu-id="c2da9-150">It can work with existing enterprise infrastructure, including Web Proxies.</span></span>

<span data-ttu-id="c2da9-151">Usa metodi di dispositivo hub IoT per trasferire pacchetti di dati TCP/IP a livello di applicazione e garantisce quindi l'attendibilità degli endpoint, la crittografia dei dati e l'integrità tramite SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="c2da9-151">It uses IoT Hub Device methods to transfer packetized TCP/IP data at the application layer and thus ensures endpoint trust, data encryption, and integrity using SSL/TLS.</span></span>

<span data-ttu-id="c2da9-152">Il protocollo binario OPC UA inoltrato attraverso il proxy stesso usa la crittografia e l'autenticazione UA.</span><span class="sxs-lookup"><span data-stu-id="c2da9-152">The OPC UA binary protocol relayed through the proxy itself uses UA authentication and encryption.</span></span>

## <a name="azure-time-series-insights"></a><span data-ttu-id="c2da9-153">Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="c2da9-153">Azure Time Series Insights</span></span>

<span data-ttu-id="c2da9-154">Il modulo di pubblicazione OPC del gateway effettua la sottoscrizione ai nodi del server OPC UA per rilevare le modifiche ai valori dei dati.</span><span class="sxs-lookup"><span data-stu-id="c2da9-154">The Gateway OPC Publisher Module subscribes to OPC UA server nodes to detect change in the data values.</span></span> <span data-ttu-id="c2da9-155">Se viene rilevata una modifica dei dati in uno dei nodi, questo modulo invia messaggi all'hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="c2da9-155">If a data change is detected in one of the nodes, this module then sends messages to Azure IoT Hub.</span></span>

<span data-ttu-id="c2da9-156">L'hub IoT fornisce un'origine evento ad Azure Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="c2da9-156">IoT Hub provides an event source to Azure TSI.</span></span> <span data-ttu-id="c2da9-157">Time Series Insights archivia i dati per 30 giorni in base ai timestamp associati ai messaggi.</span><span class="sxs-lookup"><span data-stu-id="c2da9-157">TSI stores data for 30 days based on timestamps attached to the messages.</span></span> <span data-ttu-id="c2da9-158">Questi dati includono:</span><span class="sxs-lookup"><span data-stu-id="c2da9-158">This data includes:</span></span>

* <span data-ttu-id="c2da9-159">ApplicationUri OPC UA</span><span class="sxs-lookup"><span data-stu-id="c2da9-159">OPC UA ApplicationUri</span></span>
* <span data-ttu-id="c2da9-160">NodeId OPC UA</span><span class="sxs-lookup"><span data-stu-id="c2da9-160">OPC UA NodeId</span></span>
* <span data-ttu-id="c2da9-161">Valore del nodo</span><span class="sxs-lookup"><span data-stu-id="c2da9-161">Value of the node</span></span>
* <span data-ttu-id="c2da9-162">Timestamp di origine</span><span class="sxs-lookup"><span data-stu-id="c2da9-162">Source timestamp</span></span>
* <span data-ttu-id="c2da9-163">DisplayName OPC UA</span><span class="sxs-lookup"><span data-stu-id="c2da9-163">OPC UA DisplayName</span></span>

<span data-ttu-id="c2da9-164">Time Series Insights non consente attualmente ai clienti di definire il periodo di conservazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="c2da9-164">Currently, TSI does not allow customers to customize how long they wish to keep the data for.</span></span>

<span data-ttu-id="c2da9-165">Time Series Insights esegue query sui dati del nodo usando una funzione SearchSpan (Time.From, Time.To) ed esegue l'aggregazione in base ad ApplicationUri OPC UA, NodeId OPC UA oppure DisplayName OPC UA.</span><span class="sxs-lookup"><span data-stu-id="c2da9-165">TSI queries against node data using a SearchSpan (Time.From, Time.To) and aggregates by OPC UA ApplicationUri or OPC UA NodeId or OPC UA DisplayName.</span></span>

<span data-ttu-id="c2da9-166">Per recuperare i dati per i misuratori OEE e KPI e i grafici di serie temporali, i dati vengono aggregati per numero di eventi, Sum, Avg, Min e Max.</span><span class="sxs-lookup"><span data-stu-id="c2da9-166">To retrieve the data for the OEE and KPI gauges, and the time series charts, data is aggregated by count of events, Sum, Avg, Min, and Max.</span></span>

<span data-ttu-id="c2da9-167">Le serie temporali vengono compilate usando un processo differente.</span><span class="sxs-lookup"><span data-stu-id="c2da9-167">The time series are built using a different process.</span></span> <span data-ttu-id="c2da9-168">OEE e KPI vengono calcolati dai dati di base della postazione e propagati alla topologia (linee di produzione, stabilimento, azienda) nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c2da9-168">OEE and KPIs are calculated from station base data and bubbled up for the topology (production lines, factories, enterprise) in the application.</span></span>

<span data-ttu-id="c2da9-169">La serie temporale per la topologia OEE e KPI viene calcolata nell'app ogni volta che un intervallo di tempo visualizzato è pronto,</span><span class="sxs-lookup"><span data-stu-id="c2da9-169">Additionally, time series for OEE and KPI topology is calculated in the app, whenever a displayed timespan is ready.</span></span> <span data-ttu-id="c2da9-170">ad esempio la visualizzazione giornaliera viene aggiornata ogni ora.</span><span class="sxs-lookup"><span data-stu-id="c2da9-170">For example, the day view is updated every full hour.</span></span>

<span data-ttu-id="c2da9-171">La visualizzazione della serie temporale dei dati del nodo proviene direttamente da Time Series Insights tramite un'aggregazione per timespan.</span><span class="sxs-lookup"><span data-stu-id="c2da9-171">The time series view of node data comes directly from TSI using an aggregation for timespan.</span></span>

## <a name="iot-hub"></a><span data-ttu-id="c2da9-172">Hub IoT</span><span class="sxs-lookup"><span data-stu-id="c2da9-172">IoT Hub</span></span>
<span data-ttu-id="c2da9-173">L'[hub IoT][lnk-IoT Hub] riceve i dati inviati dal modulo di pubblicazione OPC nel cloud e li mette a disposizione del servizio di Azure Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="c2da9-173">The [IoT hub][lnk-IoT Hub] receives data sent from the OPC Publisher Module into the cloud and makes it available to the Azure TSI service.</span></span> 

<span data-ttu-id="c2da9-174">L'hub IoT nella soluzione esegue anche le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c2da9-174">The IoT Hub in the solution also:</span></span>
- <span data-ttu-id="c2da9-175">Gestisce un registro delle identità che archivia gli ID per tutti i moduli di pubblicazione OPC e tutti i moduli proxy OPC.</span><span class="sxs-lookup"><span data-stu-id="c2da9-175">Maintains an identity registry that stores the IDs for all OPC Publisher Module and all OPC Proxy Modules.</span></span>
- <span data-ttu-id="c2da9-176">Viene usato come canale di trasporto per la comunicazione bidirezionale del modulo proxy OPC.</span><span class="sxs-lookup"><span data-stu-id="c2da9-176">Is used as transport channel for bidirectional communication of the OPC Proxy Module.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="c2da9-177">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c2da9-177">Azure Storage</span></span>
<span data-ttu-id="c2da9-178">La soluzione usa Archiviazione BLOB di Azure come spazio di archiviazione su disco per la macchina virtuale e per i dati di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c2da9-178">The solution uses Azure blob storage as disk storage for the VM and to store deployment data.</span></span>

## <a name="web-app"></a><span data-ttu-id="c2da9-179">App Web</span><span class="sxs-lookup"><span data-stu-id="c2da9-179">Web app</span></span>
<span data-ttu-id="c2da9-180">L'app Web distribuita nell'ambito della soluzione preconfigurata è costituita da un client OPC UA integrato, elaborazione degli avvisi e visualizzazione dei dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="c2da9-180">The web app deployed as part of the preconfigured solution comprises of an integrated OPC UA client, alerts processing and telemetry visualization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2da9-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c2da9-181">Next steps</span></span>

<span data-ttu-id="c2da9-182">È possibile proseguire con l'introduzione a IoT Suite vedendo gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="c2da9-182">You can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="c2da9-183">[Autorizzazioni per il sito azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="c2da9-183">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="c2da9-184">Distribuire un gateway in Windows o Linux per la soluzione preconfigurata di connected factory</span><span class="sxs-lookup"><span data-stu-id="c2da9-184">Deploy a gateway on Windows or Linux for the connected factory preconfigured solution</span></span>](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
