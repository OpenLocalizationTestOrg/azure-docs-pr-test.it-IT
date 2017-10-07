---
title: Panoramica di Azure IoT Suite aaaMicrosoft | Documenti Microsoft
description: Panoramica di come Azure IoT Suite offre internet delle cose soluzioni preconfigurate toocollect, analizzare e archiviare i dati, fornire visualizzazioni e integrazione con altri sistemi.
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
ms.openlocfilehash: 385025c5ec0d37c74689a928bc09e85b33439634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-iot-suite"></a><span data-ttu-id="872e5-103">Panoramica di Azure IoT Suite</span><span class="sxs-lookup"><span data-stu-id="872e5-103">Overview of Azure IoT Suite</span></span>

<span data-ttu-id="872e5-104">Hello Azure internet dei servizi di cose (IoT) offre un'ampia gamma di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="872e5-104">hello Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="872e5-105">Questi servizi di livello aziendale consentono di:</span><span class="sxs-lookup"><span data-stu-id="872e5-105">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="872e5-106">Raccogliere dati dai dispositivi</span><span class="sxs-lookup"><span data-stu-id="872e5-106">Collect data from devices</span></span>
* <span data-ttu-id="872e5-107">Analizzare i flussi dei dati in movimento</span><span class="sxs-lookup"><span data-stu-id="872e5-107">Analyze data streams in-motion</span></span>
* <span data-ttu-id="872e5-108">Archiviare ed eseguire query su set di dati di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="872e5-108">Store and query large data sets</span></span>
* <span data-ttu-id="872e5-109">Visualizzare i dati in tempo reale e cronologici</span><span class="sxs-lookup"><span data-stu-id="872e5-109">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="872e5-110">Eseguire l'integrazione con i sistemi back-office</span><span class="sxs-lookup"><span data-stu-id="872e5-110">Integrate with back-office systems</span></span>
* <span data-ttu-id="872e5-111">Gestire i dispositivi</span><span class="sxs-lookup"><span data-stu-id="872e5-111">Manage your devices</span></span>

<span data-ttu-id="872e5-112">toodeliver queste funzionalità, Azure IoT Suite insieme pacchetti più servizi di Azure con le estensioni personalizzate come *preconfigurato soluzioni*.</span><span class="sxs-lookup"><span data-stu-id="872e5-112">toodeliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as *preconfigured solutions*.</span></span> <span data-ttu-id="872e5-113">Queste soluzioni preconfigurate sono implementazioni di base di modelli di soluzione IoT comuni che consentono di tooreduce hello tempo si toodeliver soluzioni IoT.</span><span class="sxs-lookup"><span data-stu-id="872e5-113">These preconfigured solutions are base implementations of common IoT solution patterns that help tooreduce hello time you take toodeliver your IoT solutions.</span></span> <span data-ttu-id="872e5-114">Utilizzo di hello [IoT software development kit][lnk-sdks], è possibile personalizzare ed estendere questi toomeet soluzioni i propri requisiti.</span><span class="sxs-lookup"><span data-stu-id="872e5-114">Using hello [IoT software development kits][lnk-sdks], you can customize and extend these solutions toomeet your own requirements.</span></span> <span data-ttu-id="872e5-115">È anche possibile usare queste soluzioni come esempi o modelli durante lo sviluppo di nuove soluzioni IoT.</span><span class="sxs-lookup"><span data-stu-id="872e5-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="872e5-116">Hello video seguente fornisce un tooAzure introduzione IoT Suite:</span><span class="sxs-lookup"><span data-stu-id="872e5-116">hello following video provides an introduction tooAzure IoT Suite:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a><span data-ttu-id="872e5-117">Servizi di Azure IoT in Azure IoT Suite</span><span class="sxs-lookup"><span data-stu-id="872e5-117">Azure IoT services in Azure IoT Suite</span></span>
<span data-ttu-id="872e5-118">le soluzioni di Hello preconfigurato utilizzano in genere hello seguenti servizi:</span><span class="sxs-lookup"><span data-stu-id="872e5-118">hello preconfigured solutions typically use hello following services:</span></span>

* <span data-ttu-id="872e5-119">Core tooAzure IoT Suite è hello [IoT Hub Azure] [ lnk-iot-hub] servizio.</span><span class="sxs-lookup"><span data-stu-id="872e5-119">Core tooAzure IoT Suite is hello [Azure IoT Hub][lnk-iot-hub] service.</span></span> <span data-ttu-id="872e5-120">Questo servizio fornisce hello dispositivo a cloud e le funzionalità di messaggistica cloud a dispositivo e agisce come gateway toohello hello cloud e altri servizi IoT Suite chiave hello.</span><span class="sxs-lookup"><span data-stu-id="872e5-120">This service provides hello device-to-cloud and cloud-to-device messaging capabilities and acts as hello gateway toohello cloud and hello other key IoT Suite services.</span></span> <span data-ttu-id="872e5-121">servizio Hello consente tooreceive messaggi dai dispositivi su larga scala e inviare comandi tooyour dispositivi.</span><span class="sxs-lookup"><span data-stu-id="872e5-121">hello service enables you tooreceive messages from your devices at scale, and send commands tooyour devices.</span></span> <span data-ttu-id="872e5-122">servizio Hello consente inoltre troppo[gestire i dispositivi][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="872e5-122">hello service also enables you too[manage your devices][lnk-device-management].</span></span> <span data-ttu-id="872e5-123">Ad esempio, è possibile configurare, riavviare o eseguire impostazioni di fabbrica hub di toohello connessi uno o più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="872e5-123">For example, you can configure, reboot, or perform a factory reset on one or more devices connected toohello hub.</span></span>
* <span data-ttu-id="872e5-124">[Analisi di flusso di Azure][lnk-asa] offre l'analisi dei dati in movimento.</span><span class="sxs-lookup"><span data-stu-id="872e5-124">[Azure Stream Analytics][lnk-asa] provides in-motion data analysis.</span></span> <span data-ttu-id="872e5-125">IoT Suite utilizza questi dati di telemetria in ingresso di servizio tooprocess, eseguire l'aggregazione e rilevare gli eventi.</span><span class="sxs-lookup"><span data-stu-id="872e5-125">IoT Suite uses this service tooprocess incoming telemetry, perform aggregation, and detect events.</span></span> <span data-ttu-id="872e5-126">soluzioni Hello preconfigurato inoltre utilizzano analitica tooprocess informativi i messaggi del flusso che contengono dati, ad esempio le risposte di metadati o un comando dai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="872e5-126">hello preconfigured solutions also use stream analytics tooprocess informational messages that contain data such as metadata or command responses from devices.</span></span> <span data-ttu-id="872e5-127">soluzioni Hello Analitica flusso tooprocess hello messaggi i dispositivi usati e recapitare i messaggi tooother servizi.</span><span class="sxs-lookup"><span data-stu-id="872e5-127">hello solutions use Stream Analytics tooprocess hello messages from your devices and deliver those messages tooother services.</span></span>
* <span data-ttu-id="872e5-128">[Archiviazione di Azure] [ lnk-azure-storage] e [Azure Cosmos DB] [ lnk-document-db] forniscono funzionalità di archiviazione dati hello.</span><span class="sxs-lookup"><span data-stu-id="872e5-128">[Azure Storage][lnk-azure-storage] and [Azure Cosmos DB][lnk-document-db] provide hello data storage capabilities.</span></span> <span data-ttu-id="872e5-129">Hello soluzioni preconfigurate utilizzano dati di telemetria toostore archiviazione blob e toomake disponibile per l'analisi.</span><span class="sxs-lookup"><span data-stu-id="872e5-129">hello preconfigured solutions use blob storage toostore telemetry and toomake it available for analysis.</span></span> <span data-ttu-id="872e5-130">soluzioni Hello utilizzano Cosmos DB toostore metadati del dispositivo e abilitano la funzionalità di gestione di dispositivi hello di soluzioni di hello.</span><span class="sxs-lookup"><span data-stu-id="872e5-130">hello solutions use Cosmos DB toostore device metadata and enable hello device management capabilities of hello solutions.</span></span>
* <span data-ttu-id="872e5-131">[Le app Web di Azure] [ lnk-web-apps] e [Microsoft Power BI] [ lnk-power-bi] forniscono le funzionalità di visualizzazione dati hello.</span><span class="sxs-lookup"><span data-stu-id="872e5-131">[Azure Web Apps][lnk-web-apps] and [Microsoft Power BI][lnk-power-bi] provide hello data visualization capabilities.</span></span> <span data-ttu-id="872e5-132">flessibilità di Hello di Power BI consente tooquickly compilare i propri dashboard interattivi che utilizzano dati IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="872e5-132">hello flexibility of Power BI enables you tooquickly build your own interactive dashboards that use IoT Suite data.</span></span>

<span data-ttu-id="872e5-133">Per una panoramica dell'architettura di hello di una tipica soluzione IoT, vedere [Microsoft Azure e hello Internet delle cose (IoT)][iot-suite-what-is-azure-iot].</span><span class="sxs-lookup"><span data-stu-id="872e5-133">For an overview of hello architecture of a typical IoT solution, see [Microsoft Azure and hello Internet of Things (IoT)][iot-suite-what-is-azure-iot].</span></span>

## <a name="preconfigured-solutions"></a><span data-ttu-id="872e5-134">soluzioni preconfigurate</span><span class="sxs-lookup"><span data-stu-id="872e5-134">Preconfigured solutions</span></span>

<span data-ttu-id="872e5-135">IoT Suite include soluzioni preconfigurate che abilita Guida introduttiva è tooquickly e tooexplore hello scenari IoT comuni, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="872e5-135">IoT Suite includes preconfigured solutions that enable you tooquickly get started with and tooexplore hello common IoT scenarios, such as:</span></span>

* <span data-ttu-id="872e5-136">Monitoraggio remoto</span><span class="sxs-lookup"><span data-stu-id="872e5-136">Remote monitoring</span></span>
* <span data-ttu-id="872e5-137">Manutenzione predittiva</span><span class="sxs-lookup"><span data-stu-id="872e5-137">Predictive maintenance</span></span>
* <span data-ttu-id="872e5-138">Connected factory</span><span class="sxs-lookup"><span data-stu-id="872e5-138">Connected factory</span></span>

<span data-ttu-id="872e5-139">È possibile distribuire queste tooyour soluzioni sottoscrizione di Azure e quindi eseguire uno scenario di IoT completato, end-to-end.</span><span class="sxs-lookup"><span data-stu-id="872e5-139">You can deploy these solutions tooyour Azure subscription and then run a complete, end-to-end IoT scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="872e5-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="872e5-140">Next steps</span></span>

<span data-ttu-id="872e5-141">Dopo aver creato una panoramica delle operazioni che è possibile eseguire IoT Suite e quali sono i componenti principali, informazioni sulle soluzioni hello preconfigurato in IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="872e5-141">Now that you have an overview of what IoT Suite can do and what are its main components, you can learn more about hello preconfigured solutions in IoT Suite.</span></span> <span data-ttu-id="872e5-142">Per ulteriori informazioni, vedere [quali sono hello Azure IoT preconfigurato soluzioni?][lnk-what-are-preconfig]</span><span class="sxs-lookup"><span data-stu-id="872e5-142">For more information, see [What are hello Azure IoT preconfigured solutions?][lnk-what-are-preconfig]</span></span>

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
