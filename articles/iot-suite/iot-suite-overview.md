---
title: Panoramica di Microsoft Azure IoT Suite | Documentazione Microsoft
description: Panoramica di come Azure IoT Suite offra soluzioni preconfigurate Internet delle cose per raccogliere, analizzare e archiviare dati, fornire visualizzazioni ed eseguire l'integrazione con altri sistemi.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2d38d08a-4133-4e5c-8b28-f93cadb5df05
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfa8dbbd0b1d943a9eb7a042df0bac25189d9ac9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-azure-iot-suite"></a><span data-ttu-id="2604e-103">Panoramica di Azure IoT Suite</span><span class="sxs-lookup"><span data-stu-id="2604e-103">Overview of Azure IoT Suite</span></span>

<span data-ttu-id="2604e-104">I servizi di Azure IoT (Internet delle cose) offrono una vasta gamma di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2604e-104">The Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="2604e-105">Questi servizi di livello aziendale consentono di:</span><span class="sxs-lookup"><span data-stu-id="2604e-105">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="2604e-106">Raccogliere dati dai dispositivi</span><span class="sxs-lookup"><span data-stu-id="2604e-106">Collect data from devices</span></span>
* <span data-ttu-id="2604e-107">Analizzare i flussi dei dati in movimento</span><span class="sxs-lookup"><span data-stu-id="2604e-107">Analyze data streams in-motion</span></span>
* <span data-ttu-id="2604e-108">Archiviare ed eseguire query su set di dati di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="2604e-108">Store and query large data sets</span></span>
* <span data-ttu-id="2604e-109">Visualizzare i dati in tempo reale e cronologici</span><span class="sxs-lookup"><span data-stu-id="2604e-109">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="2604e-110">Eseguire l'integrazione con i sistemi back-office</span><span class="sxs-lookup"><span data-stu-id="2604e-110">Integrate with back-office systems</span></span>
* <span data-ttu-id="2604e-111">Gestire i dispositivi</span><span class="sxs-lookup"><span data-stu-id="2604e-111">Manage your devices</span></span>

<span data-ttu-id="2604e-112">Per offrire queste funzionalità, Azure IoT Suite include più servizi di Azure con estensioni personalizzate come *soluzioni preconfigurate*.</span><span class="sxs-lookup"><span data-stu-id="2604e-112">To deliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as *preconfigured solutions*.</span></span> <span data-ttu-id="2604e-113">Queste soluzioni preconfigurate sono implementazioni di base dei modelli di soluzione IoT comuni che contribuiscono a ridurre i tempi di distribuzione delle soluzioni IoT.</span><span class="sxs-lookup"><span data-stu-id="2604e-113">These preconfigured solutions are base implementations of common IoT solution patterns that help to reduce the time you take to deliver your IoT solutions.</span></span> <span data-ttu-id="2604e-114">I [Software Development Kit IoT][lnk-sdks] consentono di personalizzare ed estendere queste soluzioni per soddisfare le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="2604e-114">Using the [IoT software development kits][lnk-sdks], you can customize and extend these solutions to meet your own requirements.</span></span> <span data-ttu-id="2604e-115">È anche possibile usare queste soluzioni come esempi o modelli durante lo sviluppo di nuove soluzioni IoT.</span><span class="sxs-lookup"><span data-stu-id="2604e-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="2604e-116">Nel video seguente viene fornita un'introduzione ad Azure IoT Suite:</span><span class="sxs-lookup"><span data-stu-id="2604e-116">The following video provides an introduction to Azure IoT Suite:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a><span data-ttu-id="2604e-117">Servizi di Azure IoT in Azure IoT Suite</span><span class="sxs-lookup"><span data-stu-id="2604e-117">Azure IoT services in Azure IoT Suite</span></span>
<span data-ttu-id="2604e-118">Le soluzioni preconfigurate usano in genere i servizi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2604e-118">The preconfigured solutions typically use the following services:</span></span>

* <span data-ttu-id="2604e-119">Il servizio principale di Azure IoT Suite è [Hub IoT di Azure][lnk-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="2604e-119">Core to Azure IoT Suite is the [Azure IoT Hub][lnk-iot-hub] service.</span></span> <span data-ttu-id="2604e-120">Questo servizio fornisce funzionalità di messaggistica da dispositivo a cloud e da cloud a dispositivo e funge da gateway per il cloud e gli altri servizi chiave di IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="2604e-120">This service provides the device-to-cloud and cloud-to-device messaging capabilities and acts as the gateway to the cloud and the other key IoT Suite services.</span></span> <span data-ttu-id="2604e-121">Il servizio consente di ricevere messaggi dai dispositivi su vasta scala e inviare i comandi ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="2604e-121">The service enables you to receive messages from your devices at scale, and send commands to your devices.</span></span> <span data-ttu-id="2604e-122">Il servizio consente inoltre di [gestire i dispositivi][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="2604e-122">The service also enables you to [manage your devices][lnk-device-management].</span></span> <span data-ttu-id="2604e-123">È possibile, ad esempio, configurare, riavviare o eseguire un ripristino delle impostazioni predefinite per uno o più dispositivi connessi all'hub.</span><span class="sxs-lookup"><span data-stu-id="2604e-123">For example, you can configure, reboot, or perform a factory reset on one or more devices connected to the hub.</span></span>
* <span data-ttu-id="2604e-124">[Analisi di flusso di Azure][lnk-asa] offre l'analisi dei dati in movimento.</span><span class="sxs-lookup"><span data-stu-id="2604e-124">[Azure Stream Analytics][lnk-asa] provides in-motion data analysis.</span></span> <span data-ttu-id="2604e-125">IoT Suite usa questo servizio per elaborare i dati di telemetria in entrata, eseguire operazioni di aggregazione e rilevare gli eventi.</span><span class="sxs-lookup"><span data-stu-id="2604e-125">IoT Suite uses this service to process incoming telemetry, perform aggregation, and detect events.</span></span> <span data-ttu-id="2604e-126">Le soluzioni preconfigurate usando anche l'analisi di flusso per elaborare i messaggi informativi che contengono dati, ad esempio i metadati o le risposte ai comandi dai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="2604e-126">The preconfigured solutions also use stream analytics to process informational messages that contain data such as metadata or command responses from devices.</span></span> <span data-ttu-id="2604e-127">Le soluzioni usano Analisi di flusso per elaborare i messaggi dei dispositivi e inviare i messaggi ad altri servizi.</span><span class="sxs-lookup"><span data-stu-id="2604e-127">The solutions use Stream Analytics to process the messages from your devices and deliver those messages to other services.</span></span>
* <span data-ttu-id="2604e-128">[Archiviazione di Azure][lnk-azure-storage] e [Azure Cosmos DB][lnk-document-db] offrono le funzionalità di archiviazione dati.</span><span class="sxs-lookup"><span data-stu-id="2604e-128">[Azure Storage][lnk-azure-storage] and [Azure Cosmos DB][lnk-document-db] provide the data storage capabilities.</span></span> <span data-ttu-id="2604e-129">Le soluzioni preconfigurate usano l'archivio BLOB per archiviare i dati di telemetria e renderli disponibili per l'analisi.</span><span class="sxs-lookup"><span data-stu-id="2604e-129">The preconfigured solutions use blob storage to store telemetry and to make it available for analysis.</span></span> <span data-ttu-id="2604e-130">Le soluzioni usano Cosmos DB per archiviare i metadati dei dispositivi e abilitare le funzionalità di gestione dispositivi delle soluzioni.</span><span class="sxs-lookup"><span data-stu-id="2604e-130">The solutions use Cosmos DB to store device metadata and enable the device management capabilities of the solutions.</span></span>
* <span data-ttu-id="2604e-131">[App Web di Azure][lnk-web-apps] e [Microsoft Power BI][lnk-power-bi] offrono le funzionalità di visualizzazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="2604e-131">[Azure Web Apps][lnk-web-apps] and [Microsoft Power BI][lnk-power-bi] provide the data visualization capabilities.</span></span> <span data-ttu-id="2604e-132">La flessibilità di Power BI consente di creare rapidamente i propri dashboard interattivi che usano i dati di IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="2604e-132">The flexibility of Power BI enables you to quickly build your own interactive dashboards that use IoT Suite data.</span></span>

<span data-ttu-id="2604e-133">Per una panoramica dell'architettura di una tipica soluzione IoT, vedere [Microsoft Azure e Internet of Things (IoT)][iot-suite-what-is-azure-iot].</span><span class="sxs-lookup"><span data-stu-id="2604e-133">For an overview of the architecture of a typical IoT solution, see [Microsoft Azure and the Internet of Things (IoT)][iot-suite-what-is-azure-iot].</span></span>

## <a name="preconfigured-solutions"></a><span data-ttu-id="2604e-134">soluzioni preconfigurate</span><span class="sxs-lookup"><span data-stu-id="2604e-134">Preconfigured solutions</span></span>

<span data-ttu-id="2604e-135">IoT Suite include soluzioni preconfigurate che consentono di iniziare rapidamente e di esplorare gli scenari comuni di IoT, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="2604e-135">IoT Suite includes preconfigured solutions that enable you to quickly get started with and to explore the common IoT scenarios, such as:</span></span>

* <span data-ttu-id="2604e-136">Monitoraggio remoto</span><span class="sxs-lookup"><span data-stu-id="2604e-136">Remote monitoring</span></span>
* <span data-ttu-id="2604e-137">Manutenzione predittiva</span><span class="sxs-lookup"><span data-stu-id="2604e-137">Predictive maintenance</span></span>
* <span data-ttu-id="2604e-138">Connected factory</span><span class="sxs-lookup"><span data-stu-id="2604e-138">Connected factory</span></span>

<span data-ttu-id="2604e-139">È possibile distribuire queste soluzioni nella sottoscrizione di Azure e quindi eseguire uno scenario IoT end-to-end completo.</span><span class="sxs-lookup"><span data-stu-id="2604e-139">You can deploy these solutions to your Azure subscription and then run a complete, end-to-end IoT scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2604e-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2604e-140">Next steps</span></span>

<span data-ttu-id="2604e-141">Dopo aver acquisito una panoramica di IoT Suite e dei suoi componenti, è possibile ottenere maggiori informazioni sulle soluzioni preconfigurate in IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="2604e-141">Now that you have an overview of what IoT Suite can do and what are its main components, you can learn more about the preconfigured solutions in IoT Suite.</span></span> <span data-ttu-id="2604e-142">Per altre informazioni vedere [Informazioni sulle soluzioni preconfigurate di Azure IoT Suite][lnk-what-are-preconfig]</span><span class="sxs-lookup"><span data-stu-id="2604e-142">For more information, see [What are the Azure IoT preconfigured solutions?][lnk-what-are-preconfig]</span></span>

[lnk-sdks]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-azure-storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-document-db]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-power-bi]: https://powerbi.microsoft.com/
[lnk-web-apps]: https://azure.microsoft.com/documentation/services/app-service/web/
[iot-suite-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-what-are-preconfig]: iot-suite-what-are-preconfigured-solutions.md
[lnk-device-management]: ../iot-hub/iot-hub-device-management-overview.md
