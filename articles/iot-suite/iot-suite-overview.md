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
# <a name="overview-of-azure-iot-suite"></a>Panoramica di Azure IoT Suite

Hello Azure internet dei servizi di cose (IoT) offre un'ampia gamma di funzionalità. Questi servizi di livello aziendale consentono di:

* Raccogliere dati dai dispositivi
* Analizzare i flussi dei dati in movimento
* Archiviare ed eseguire query su set di dati di grandi dimensioni
* Visualizzare i dati in tempo reale e cronologici
* Eseguire l'integrazione con i sistemi back-office
* Gestire i dispositivi

toodeliver queste funzionalità, Azure IoT Suite insieme pacchetti più servizi di Azure con le estensioni personalizzate come *preconfigurato soluzioni*. Queste soluzioni preconfigurate sono implementazioni di base di modelli di soluzione IoT comuni che consentono di tooreduce hello tempo si toodeliver soluzioni IoT. Utilizzo di hello [IoT software development kit][lnk-sdks], è possibile personalizzare ed estendere questi toomeet soluzioni i propri requisiti. È anche possibile usare queste soluzioni come esempi o modelli durante lo sviluppo di nuove soluzioni IoT.

Hello video seguente fornisce un tooAzure introduzione IoT Suite:

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a>Servizi di Azure IoT in Azure IoT Suite
le soluzioni di Hello preconfigurato utilizzano in genere hello seguenti servizi:

* Core tooAzure IoT Suite è hello [IoT Hub Azure] [ lnk-iot-hub] servizio. Questo servizio fornisce hello dispositivo a cloud e le funzionalità di messaggistica cloud a dispositivo e agisce come gateway toohello hello cloud e altri servizi IoT Suite chiave hello. servizio Hello consente tooreceive messaggi dai dispositivi su larga scala e inviare comandi tooyour dispositivi. servizio Hello consente inoltre troppo[gestire i dispositivi][lnk-device-management]. Ad esempio, è possibile configurare, riavviare o eseguire impostazioni di fabbrica hub di toohello connessi uno o più dispositivi.
* [Analisi di flusso di Azure][lnk-asa] offre l'analisi dei dati in movimento. IoT Suite utilizza questi dati di telemetria in ingresso di servizio tooprocess, eseguire l'aggregazione e rilevare gli eventi. soluzioni Hello preconfigurato inoltre utilizzano analitica tooprocess informativi i messaggi del flusso che contengono dati, ad esempio le risposte di metadati o un comando dai dispositivi. soluzioni Hello Analitica flusso tooprocess hello messaggi i dispositivi usati e recapitare i messaggi tooother servizi.
* [Archiviazione di Azure] [ lnk-azure-storage] e [Azure Cosmos DB] [ lnk-document-db] forniscono funzionalità di archiviazione dati hello. Hello soluzioni preconfigurate utilizzano dati di telemetria toostore archiviazione blob e toomake disponibile per l'analisi. soluzioni Hello utilizzano Cosmos DB toostore metadati del dispositivo e abilitano la funzionalità di gestione di dispositivi hello di soluzioni di hello.
* [Le app Web di Azure] [ lnk-web-apps] e [Microsoft Power BI] [ lnk-power-bi] forniscono le funzionalità di visualizzazione dati hello. flessibilità di Hello di Power BI consente tooquickly compilare i propri dashboard interattivi che utilizzano dati IoT Suite.

Per una panoramica dell'architettura di hello di una tipica soluzione IoT, vedere [Microsoft Azure e hello Internet delle cose (IoT)][iot-suite-what-is-azure-iot].

## <a name="preconfigured-solutions"></a>soluzioni preconfigurate

IoT Suite include soluzioni preconfigurate che abilita Guida introduttiva è tooquickly e tooexplore hello scenari IoT comuni, ad esempio:

* Monitoraggio remoto
* Manutenzione predittiva
* Connected factory

È possibile distribuire queste tooyour soluzioni sottoscrizione di Azure e quindi eseguire uno scenario di IoT completato, end-to-end.

## <a name="next-steps"></a>Passaggi successivi

Dopo aver creato una panoramica delle operazioni che è possibile eseguire IoT Suite e quali sono i componenti principali, informazioni sulle soluzioni hello preconfigurato in IoT Suite. Per ulteriori informazioni, vedere [quali sono hello Azure IoT preconfigurato soluzioni?][lnk-what-are-preconfig]

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
