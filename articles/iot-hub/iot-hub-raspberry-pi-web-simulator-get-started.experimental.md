---
title: aaaSimulated Raspberry Pi toocloud (Node.js) - connessione Raspberry l'installazione guidata piattaforma web simulatore tooAzure IoT Hub | Documenti Microsoft
description: Connettersi Raspberry Pi web simulatore tooAzure IoT Hub per Pi Raspberry toosend dati toohello cloud di Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: pi al lampone simulatore, azure al lampone pi greco, al lampone pi iot hub iot, pi al lampone invia dati toocloud, al lampone pi toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/7/2017
ms.author: xshi
ms.openlocfilehash: 0ebe1004e96ff4e64fdd1b05b7e35192ec42f7d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-online-simulator-tooazure-iot-hub-nodejs"></a>Connettersi Pi Raspberry simulatore online tooAzure IoT Hub (Node.js)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

In questa esercitazione, è necessario innanzitutto apprendimento hello nozioni fondamentali sulle operazioni con simulatore online Raspberry Pi. Si apprenderà quindi la modalità di connessione cloud toohello di hello Pi simulatore utilizzando tooseamlessly [IoT Hub Azure](iot-hub-what-is-iot-hub.md). 

Se si dispone di dispositivi fisici, visitare [tooAzure connettersi Pi Raspberry IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) tooget avviato. 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator tooAzure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a>Operazioni da fare

* Nozioni di base hello del simulatore online Raspberry Pi.
* Creare un hub IoT.
* Registrare un dispositivo per Pi nel proprio hub IoT.
* Eseguire un'applicazione di esempio Pi toosend simulato sensore dati tooyour IoT hub.

Connettere hub IoT tooan simulato Pi Raspberry creati. Quindi si esegue un'applicazione di esempio con i dati del sensore toogenerate hello simulatore. Infine, si invia l'hub IoT hello sensore dati tooyour.

## <a name="what-you-learn"></a>Contenuto dell'esercitazione

* Come toocreate un hub IoT di Azure e ottenere la stringa di connessione nuovo dispositivo. Se non si ha un account Azure, [creare un account Azure gratuito](https://azure.microsoft.com/free/) in pochi minuti.
* Come toowork con simulatore online Raspberry Pi.
* Come l'hub IoT toosend sensore dati tooyour.

## <a name="overview-of-raspberry-pi-web-simulator"></a>Panoramica del simulatore Web Raspberry Pi

Fare clic su simulatore online Pi Raspberry hello pulsante toolaunch.

> [!div class="button"]
[Avviare il simulatore Raspberry Pi](https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted)

Esistono tre aree nel simulatore di hello web.
* Area di assembly: circuito predefinito hello è che un Pi si connette con un sensore BME280 e un LED. area Hello è bloccata nella versione di anteprima così attualmente non è possibile eseguire la personalizzazione.
* Per la codifica - un editor di codice in linea per toocode con Raspberry Pi. applicazione di esempio Hello predefinita consente di dati del sensore toocollect dal sensore BME280 e invia tooyour IoT Hub di Azure. un'applicazione Hello è completamente compatibile con dispositivi Pi. 
* Finestra di console integrata - Mostra output di hello del codice. Nella parte superiore di hello di questa finestra, sono disponibili tre pulsanti.
   * **Eseguire** -esecuzione di un'applicazione hello in hello per la codifica.
   * **Reimpostare** -hello la reimpostazione della codifica di applicazione di esempio di area toohello predefinito.
   * **Riduzione o espansione** - in hello destra lato vi è un pulsante per si toofold/espandere hello finestra della console.

> [!NOTE] 
simulatore di web Pi Raspberry Hello è ora disponibile nella versione di anteprima. Desideriamo toohear il tono di voce hello [Gitter chat](https://gitter.im/Microsoft/raspberry-pi-web-simulator). codice sorgente Hello è public su [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).

![Panoramica del simulatore online Pi](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a>Eseguire un'applicazione di esempio nel simulatore Web Pi

1. Nell'area di codifica, assicurarsi che si lavora sull'applicazione di esempio hello predefinito. Sostituire i segnaposto hello nella riga 15 con hello stringa di connessione di Azure IoT hub dispositivo.
   ![Sostituire una stringa di connessione del dispositivo hello](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)

2. Fare clic su **eseguire** o tipo `npm start` toorun un'applicazione hello.


Verrà visualizzato l'output di hello seguente che mostra i dati del sensore hello e i messaggi hello inviati hub IoT tooyour ![Output - i dati del sensore inviati dall'hub IoT di pi greco Raspberry tooyour](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)


## <a name="next-steps"></a>Passaggi successivi

È stato eseguito dati sensore toocollect di applicazione di esempio e inviarlo tooyour IoT hub.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
