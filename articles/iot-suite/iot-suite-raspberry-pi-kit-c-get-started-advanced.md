---
title: Aggiorna IoT Suite utilizzando C toosupport firmware aaaConnect un tooAzure Pi Raspberry | Documenti Microsoft
description: Utilizzare hello Starter Kit di Microsoft Azure IoT per hello Raspberry Pi 3 e Azure IoT Suite. Utilizzare tooconnect C toohello le Pi Raspberry soluzione di monitoraggio remoto, inviare i dati di telemetria da sensori toohello cloud ed eseguire un aggiornamento remoto del firmware.
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
ms.openlocfilehash: 36d39c6d754ddb025fd3f6b74d7795ed907b754c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-c"></a>Connettere il toohello Raspberry Pi 3 soluzione di monitoraggio remoto e abilitare gli aggiornamenti del firmware remoto utilizzando C

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Questa esercitazione viene illustrato come toouse hello IoT Starter Kit di Microsoft Azure per 3 Pi Raspberry per:

* Sviluppare un lettore di temperatura e umidità in grado di comunicare con il cloud hello.
* Abilitare ed eseguire un'applicazione client di firmware remote update tooupdate hello in hello Raspberry Pi.

esercitazione Hello utilizza:

* Sistema operativo Raspbian, linguaggio di programmazione C hello e hello Microsoft Azure IoT SDK per C tooimplement un dispositivo di esempio.
* monitoraggio remoto IoT Suite Hello preconfigurato soluzione come hello basato su cloud back-end.

## <a name="overview"></a>Panoramica

In questa esercitazione è completare hello alla procedura seguente:

* Distribuire un'istanza di hello remoto monitoraggio soluzione preconfigurata tooyour sottoscrizione di Azure. Questo passaggio distribuisce e configura automaticamente più servizi di Azure.
* Consente di impostare il dispositivo e sensori di toocommunicate con il computer e hello soluzione di monitoraggio remoto.
* Aggiornare hello esempio dispositivo codice tooconnect toohello soluzione di monitoraggio remoto e inviare dati di telemetria che è possibile visualizzare nel dashboard di soluzione hello.
* Utilizzare l'esempio dispositivo codice tooupdate hello client un'applicazione hello.

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Hello remoto disposizioni soluzione monitoraggio di un set di servizi di Azure nella sottoscrizione di Azure. distribuzione di Hello riflette un'architettura aziendale reale. tooavoid addebiti di consumo di Azure, eliminare l'istanza di soluzione hello preconfigurato azureiotsuite.com dopo aver con esso. Se è necessario hello nuovamente la soluzione preconfigurata, è possibile ricrearla facilmente. Per ulteriori informazioni sulla riduzione del consumo durante l'esecuzione di soluzioni di monitoraggio remoto hello, vedere [configurazione Azure IoT Suite preconfigurato soluzioni per scopi dimostrativi][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a>Scaricare e configurare l'esempio hello

È ora possibile scaricare e configurare l'applicazione client per il monitoraggio remoto di hello nelle Pi Raspberry.

### <a name="clone-hello-repositories"></a>Clonare il repository hello

Se non è già fatto, hello clone richiesto repository eseguendo hello seguendo i comandi del Pi:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a>Aggiornare la stringa di connessione dispositivo hello

File di configurazione di esempio hello Open in hello **nano** editor utilizzando hello comando seguente:

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

Sostituire i valori segnaposto hello con hello ID e l'IoT Hub informazioni sul dispositivo è stato creato e salvato all'inizio di hello di questa esercitazione.

Al termine, il contenuto di hello del file di deviceinfo hello dovrebbe essere simile hello di esempio seguente:

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

Salvare le modifiche (**Ctrl O**, **invio**) e uscire dall'editor hello (**Ctrl + X**).

## <a name="build-hello-sample"></a>Compilare l'esempio hello

Se non è già stato fatto, installare i pacchetti dei prerequisiti per Microsoft Azure IoT dispositivo SDK hello hello per C eseguendo hello seguendo i comandi in un terminal hello Raspberry Pi:

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

È ora possibile compilare la soluzione di esempio hello su hello Raspberry Pi:

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
```

È ora possibile eseguire il programma di esempio hello in hello Raspberry Pi. Immettere il comando hello:

  ```sh
  sudo ~/cmake/remote_monitoring/remote_monitoring
  ```

Hello riportato di seguito è riportato un esempio di output di hello visualizzato al prompt dei comandi di hello in hello Raspberry Pi:

![Output dell'app Raspberry Pi][img-raspberry-output]

Premere **Ctrl-C** programma hello tooexit in qualsiasi momento.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. Nel dashboard di soluzione hello, fare clic su **dispositivi** toovisit hello **dispositivi** pagina. Selezionare le Pi Raspberry hello **elenco dei dispositivi**. Quindi scegliere **Metodi**:

    ![Elencare i dispositivi nel dashboard][img-list-devices]

1. In hello **Richiama metodo** pagina, scegliere **InitiateFirmwareUpdate** in hello **metodo** elenco a discesa.

1. In hello **FWPackageURI** immettere **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**. Questo file di archivio contiene l'implementazione di hello della versione 2.0 del firmware hello.

1. Scegliere **InvokeMethod**. app Hello in hello Pi Raspberry invia un dashboard di soluzione toohello indietro di riconoscimento. Quindi Avvia processo di aggiornamento del firmware hello download hello della nuova versione del firmware hello:

    ![Visualizzare la cronologia del metodo][img-method-history]

## <a name="observe-hello-firmware-update-process"></a>Processo di aggiornamento del firmware hello osservare

È possibile osservare processo di aggiornamento del firmware hello mentre è in esecuzione sul dispositivo hello e visualizzando hello segnalati proprietà nel dashboard di soluzione hello:

1. È possibile visualizzare l'avanzamento di hello del processo di aggiornamento hello in hello Raspberry Pi:

    ![Mostra l'avanzamento dell'aggiornamento][img-update-progress]

    > [!NOTE]
    > applicazione di monitoraggio remoto Hello viene riavviato automaticamente al termine dell'aggiornamento hello. Utilizzare il comando hello `ps -ef` tooverify è in esecuzione. Se si desidera che il processo di hello tooterminate, utilizzare hello `kill` comando con id processo hello.

1. È possibile visualizzare lo stato di hello di aggiornamento del firmware hello, come segnalato dal dispositivo hello, nel portale di soluzione hello. Hello schermata seguente mostra lo stato di hello e la durata di ogni fase del processo di aggiornamento hello e la nuova versione del firmware di hello:

    ![Mostra lo stato del processo][img-job-status]

    Se si passa indietro toohello dashboard, è possibile verificare dispositivo hello sta ancora inviando dati di telemetria dopo l'aggiornamento del firmware hello.

> [!WARNING]
> Se si lascia in esecuzione nell'account di Azure di soluzione di monitoraggio remoto hello, verrà addebitato per volta hello che è in esecuzione. Per ulteriori informazioni sulla riduzione del consumo durante l'esecuzione di soluzioni di monitoraggio remoto hello, vedere [configurazione Azure IoT Suite preconfigurato soluzioni per scopi dimostrativi][lnk-demo-config]. Eliminare la soluzione hello preconfigurato dall'account di Azure al termine dell'utilizzo.

## <a name="next-steps"></a>Passaggi successivi

Visitare hello [Centro per sviluppatori Azure IoT](https://azure.microsoft.com/develop/iot/) per ulteriori esempi e documentazione su Azure IoT.


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md