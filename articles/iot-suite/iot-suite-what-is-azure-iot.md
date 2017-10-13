---
title: Soluzioni di Azure per Internet delle cose (IoT Suite) | Documentazione Microsoft
description: Una panoramica di IoT in Azure, inclusa un'architettura della soluzione di esempio e la sua relazione con Azure IoT Suite e le soluzioni preconfigurate.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 437d2655-896f-4a9e-a4a8-b864790d3ef8
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 320190488bb4c7b8192421f9dd50a5264f558584
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="azure-iot-suite"></a>Azure IoT Suite
Microsoft Azure IoT Suite è una soluzione di livello aziendale che consente di iniziare rapidamente a usare un set di soluzioni preconfigurate estendibili per gestire scenari IoT comuni, come il [monitoraggio remoto][lnk-preconfigured-solutions], la [manutenzione predittiva][lnk-predictive-maintenance] e [connected factory][lnk-connected-factory]. Tali soluzioni sono implementazioni dell'architettura di una soluzione IoT illustrata in questo articolo.

Si tratta di soluzioni preconfigurate complete e funzionanti di tipo end-to-end che includono:

- Dispositivi simulati per iniziare.
- Servizi di Azure preconfigurati come [Hub IoT di Azure][Azure IoT Hub], [Hub eventi di Azure][Azure Event Hubs], [Analisi di flusso di Azure][Azure Stream Analytics], [Azure Machine Learning][Azure Machine Learning] e [Archiviazione di Azure][Azure storage].
- Console di gestione specifiche per la soluzione.

Le soluzioni preconfigurate contengono codice consolidato, pronto per la produzione, che è possibile personalizzare ed estendere per implementare scenari IoT specifici.

Vedere anche il servizio [Hub IoT di Azure][Azure IoT Hub], usato da molte soluzioni preconfigurate. [Hub IoT di Azure][Azure IoT Hub] garantisce comunicazioni bidirezionali sicure e affidabili tra i dispositivi e il cloud usati nell'architettura delle soluzioni preconfigurate.

## <a name="next-steps"></a>Passaggi successivi
Esplorare queste risorse per altre informazioni su IoT Suite e sulle soluzioni preconfigurate:

* [Informazioni su Azure IoT Suite][lnk-whatissuite]
* [Informazioni sulle soluzioni preconfigurate di Azure IoT Suite][lnk-whatarepreconfigured]

[lnk-whatissuite]: iot-suite-overview.md
[lnk-whatarepreconfigured]: iot-suite-what-are-preconfigured-solutions.md

[lnk-preconfigured-solutions]: iot-suite-getstarted-preconfigured-solutions.md
[Azure IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[Azure Event Hubs]: https://azure.microsoft.com/documentation/services/event-hubs/
[Azure Stream Analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[Azure Machine Learning]: https://azure.microsoft.com/documentation/services/machine-learning/
[Azure storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-predictive-maintenance]: iot-suite-predictive-overview.md
[lnk-connected-factory]: iot-suite-connected-factory-overview.md