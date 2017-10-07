---
title: aaaConnect tooAzure un gateway IoT Suite utilizzando un NUC Intel | Documenti Microsoft
description: Utilizzare hello Microsoft IoT commerciale Gateway Kit e hello preconfigurato soluzione di monitoraggio remoto. Hello utilizzare Azure IoT Edge gateway tooconnect toohello soluzione di monitoraggio remoto, inviare i dati di telemetria simulato toohello cloud e rispondere toomethods richiamato dal dashboard di soluzione hello.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 46b545fc21b054191c8f78ace20fc628f839a819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a>Connettere il preconfigurati soluzione di monitoraggio remoto di Azure IoT Edge gateway toohello e inviare dati di telemetria simulata

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

Questa esercitazione viene illustrato come toouse Azure IoT Edge toosimulate temperatura e l'umidità dati toosend toohello monitoraggio remoto preconfigurato soluzione. esercitazione Hello utilizza:

- Azure IoT Edge tooimplement un gateway di esempio.
- monitoraggio remoto IoT Suite Hello preconfigurato soluzione come hello basato su cloud back-end.

## <a name="overview"></a>Panoramica

In questa esercitazione è completare hello alla procedura seguente:

- Distribuire un'istanza di hello remoto monitoraggio soluzione preconfigurata tooyour sottoscrizione di Azure. Questo passaggio distribuisce e configura automaticamente più servizi di Azure.
- Consente di impostare il toocommunicate dispositivo gateway di Intel NUC con il computer e una soluzione di monitoraggio remoto hello.
- Configurare hello IoT Edge gateway toosend simulato telemetria che è possibile visualizzare nel dashboard di soluzione hello.

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Hello remoto disposizioni soluzione monitoraggio di un set di servizi di Azure nella sottoscrizione di Azure. distribuzione di Hello riflette un'architettura aziendale reale. tooavoid addebiti di consumo di Azure, eliminare l'istanza di soluzione hello preconfigurato azureiotsuite.com dopo aver con esso. Se è necessario hello nuovamente la soluzione preconfigurata, è possibile ricrearla facilmente. Per ulteriori informazioni sulla riduzione del consumo durante l'esecuzione di soluzioni di monitoraggio remoto hello, vedere [configurazione Azure IoT Suite preconfigurato soluzioni per scopi dimostrativi][lnk-demo-config].

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

Ripetere hello precedenti passaggi tooadd un secondo dispositivo con un ID di dispositivo, ad esempio **device02**. esempio Hello invia dati da due dispositivi simulati in hello gateway toohello soluzione di monitoraggio remoto.

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a>Compilazione del modulo IoT bordo personalizzato hello

È ora possibile compilare moduli IoT Edge personalizzata hello che consente di hello gateway toosend messaggi toohello soluzione di monitoraggio remoto. Per altre informazioni sulla configurazione di un gateway e sui moduli IoT Edge, vedere [Concetti di Azure IoT Edge][lnk-gateway-concepts].

Scaricare il codice sorgente di hello per i moduli di IoT bordo personalizzati hello da GitHub utilizzando hello seguenti comandi:

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

Compilazione del modulo IoT bordo personalizzato hello utilizzando hello seguenti comandi:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

script di compilazione Hello inserisce modulo IoT Edge di hello libsimulator.so personalizzato nella cartella di compilazione hello.

## <a name="configure-and-run-hello-iot-edge-gateway"></a>Configurare ed eseguire hello gateway perimetrale IoT

È ora possibile configurare hello IoT Edge gateway toosend telemetria simulato tooyour remoto dashboard di monitoraggio. Per altre informazioni sulla configurazione di un gateway e sui moduli IoT Edge, vedere [Concetti di Azure IoT Edge][lnk-gateway-concepts].

> [!TIP]
> In questa esercitazione è utilizzare standard di hello `vi` editor di testo in hello NUC Intel. Se non è stato utilizzato `vi` prima, si consiglia di completare un'esercitazione introduttiva, ad esempio [Unix - hello vi Editor esercitazione] [ lnk-vi-tutorial] toofamiliarize familiarità con questo editor. In alternativa, è possibile installare più semplice hello [nano](https://www.nano-editor.org/) editor utilizzando il comando hello `smart install nano -y`.

File di configurazione di esempio hello Open in hello **vi** editor utilizzando hello comando seguente:

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
```

Individuare hello seguendo le linee nella configurazione di hello per il modulo di hub IOT hello:

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

Sostituire i segnaposto hello valori con informazioni di IoT Hub è stato creato e salvato in hello hello inizino di questa esercitazione. il valore di Hello per IoTHubName simile **yourrmsolution37e08**, e il valore di hello per IoTSuffix è in genere **azure devices.net**.

Individuare hello seguendo le linee nella configurazione di hello per il modulo di mapping hello:

```json
args": [
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  },
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

Sostituire hello **deviceID** e **deviceKey** segnaposto con ID hello e le chiavi per i dispositivi hello due creato in precedenza nella soluzione di monitoraggio remoto hello.

Salvare le modifiche.

È ora possibile eseguire hello gateway IoT Edge utilizzando hello seguenti comandi:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

gateway Hello inizia hello NUC Intel e invia una soluzione di monitoraggio remoto toohello telemetria simulato:

![Il gateway IoT Edge genera dati di telemetria simulati][img-simulated telemetry]

Premere **Ctrl-C** programma hello tooexit in qualsiasi momento.

## <a name="view-hello-telemetry"></a>Visualizzazione hello telemetria

soluzione di monitoraggio remoto di telemetria simulato toohello ora invia Hello gateway perimetrale IoT. È possibile visualizzare i dati di telemetria hello nel dashboard di soluzione hello.

- Passare il dashboard di soluzione toohello.
- Selezionare uno dei dispositivi hello due configurato nel gateway hello in hello **tooView dispositivo** elenco a discesa.
- Consente di visualizzare dati di telemetria Hello dai dispositivi gateway hello nel dashboard di hello.

![Visualizzare i dati di telemetria dai dispositivi gateway hello simulata][img-telemetry-display]

> [!WARNING]
> Se si lascia in esecuzione nell'account di Azure di soluzione di monitoraggio remoto hello, verrà addebitato per volta hello che è in esecuzione. Per ulteriori informazioni sulla riduzione del consumo durante l'esecuzione di soluzioni di monitoraggio remoto hello, vedere [configurazione Azure IoT Suite preconfigurato soluzioni per scopi dimostrativi][lnk-demo-config]. Eliminare la soluzione hello preconfigurato dall'account di Azure al termine dell'utilizzo.

## <a name="next-steps"></a>Passaggi successivi

Visitare hello [Centro per sviluppatori Azure IoT](https://azure.microsoft.com/develop/iot/) per ulteriori esempi e documentazione su Azure IoT.

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started