---
title: aaaConnect un tooAzure Raspberry Pi IoT Suite utilizzando C con dati di telemetria simulato | Documenti Microsoft
description: Utilizzare hello Starter Kit di Microsoft Azure IoT per hello Raspberry Pi 3 e Azure IoT Suite. Utilizzare tooconnect C toohello le Pi Raspberry soluzione di monitoraggio remoto, inviare i dati di telemetria simulato toohello cloud e rispondere toomethods richiamato dal dashboard di soluzione hello.
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
ms.openlocfilehash: 3c4fa43b381385d1a7896cada34aa3aa0b8e5fb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-simulated-telemetry-using-c"></a>Connettere il toohello Raspberry Pi 3 soluzione di monitoraggio remoto e inviare dati di telemetria simulata utilizzando C

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Questa esercitazione viene illustrato come toouse hello Raspberry Pi 3 toosimulate temperatura e umidità dati toosend toohello cloud. esercitazione Hello utilizza:

- Sistema operativo Raspbian, linguaggio di programmazione C hello e hello Microsoft Azure IoT SDK per C tooimplement un dispositivo di esempio.
- monitoraggio remoto IoT Suite Hello preconfigurato soluzione come hello basato su cloud back-end.

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Hello remoto disposizioni soluzione monitoraggio di un set di servizi di Azure nella sottoscrizione di Azure. distribuzione di Hello riflette un'architettura aziendale reale. tooavoid addebiti di consumo di Azure, eliminare l'istanza di soluzione hello preconfigurato azureiotsuite.com dopo aver con esso. Se è necessario hello nuovamente la soluzione preconfigurata, è possibile ricrearla facilmente. Per ulteriori informazioni sulla riduzione del consumo durante l'esecuzione di soluzioni di monitoraggio remoto hello, vedere [configurazione Azure IoT Suite preconfigurato soluzioni per scopi dimostrativi][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-hello-sample"></a>Scaricare e configurare l'esempio hello

È ora possibile scaricare e configurare l'applicazione client per il monitoraggio remoto di hello nelle Pi Raspberry.

### <a name="clone-hello-repositories"></a>Clonare il repository hello

Se non già stato fatto, hello clone richiesto repository eseguendo hello seguendo i comandi di un terminale il Pi:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a>Aggiornare la stringa di connessione dispositivo hello

File di origine di esempio hello Open in hello **nano** editor utilizzando hello comando seguente:

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/remote_monitoring/remote_monitoring.c
```

Individuare hello seguenti righe:

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

Sostituire i valori segnaposto hello con dispositivo hello e informazioni di IoT Hub è stato creato e salvato all'inizio di hello di questa esercitazione. Salvare le modifiche (**Ctrl O**, **invio**) e uscire dall'editor hello (**Ctrl + X**).

## <a name="build-hello-sample"></a>Compilare l'esempio hello

Installare i pacchetti dei prerequisiti per Microsoft Azure IoT dispositivo SDK hello hello per C eseguendo hello seguendo i comandi in un terminal hello Raspberry Pi:

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

È ora possibile compilare la soluzione di esempio hello aggiornato su hello Raspberry Pi:

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
```

È ora possibile eseguire il programma di esempio hello in hello Raspberry Pi. Immettere il comando hello:

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

Hello riportato di seguito è riportato un esempio di output di hello visualizzato al prompt dei comandi di hello in hello Raspberry Pi:

![Output dell'app Raspberry Pi][img-raspberry-output]

Premere **Ctrl-C** programma hello tooexit in qualsiasi momento.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a>Passaggi successivi

Visitare hello [Centro per sviluppatori Azure IoT](https://azure.microsoft.com/develop/iot/) per ulteriori esempi e documentazione su Azure IoT.

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-simulator/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
