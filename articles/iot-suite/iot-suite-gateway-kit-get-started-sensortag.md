---
title: aaaConnect tooAzure un gateway IoT Suite utilizzando un NUC Intel | Documenti Microsoft
description: Utilizzare hello Microsoft IoT commerciale Gateway Kit e hello preconfigurato soluzione di monitoraggio remoto. Utilizzo di una soluzione di monitoraggio remoto toohello SensorTag dispositivo tooconnect hello Azure IoT Edge gateway tooenable, cloud toohello telemetria di inviare e rispondere toomethods richiamato dal dashboard di soluzione hello.
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
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: 6f98ee3c1e2311a8644da9d72d40e671e7cbcf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a>Connettere la soluzione preconfigurata di monitoraggio remoto di Azure IoT Edge gateway toohello e inviare dati di telemetria da un SensorTag

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

Questa esercitazione viene illustrato come toouse Azure IoT Edge toosend temperatura e umidità dati monitoraggio remoto di SensorTag dispositivo toohello preconfigurato soluzione. Hello SensorTag si connette il gateway di Intel NUC toohello tramite Bluetooth. esercitazione Hello utilizza:

- Azure IoT Edge tooimplement un gateway di esempio.
- monitoraggio remoto IoT Suite Hello preconfigurato soluzione come hello basato su cloud back-end.

## <a name="overview"></a>Panoramica

In questa esercitazione è completare hello alla procedura seguente:

- Distribuire un'istanza di hello remoto monitoraggio soluzione preconfigurata tooyour sottoscrizione di Azure. Questo passaggio distribuisce e configura automaticamente più servizi di Azure.
- Consente di impostare il toocommunicate dispositivo gateway di Intel NUC con il computer e una soluzione di monitoraggio remoto hello.
- Imposta i dati di telemetria Intel NUC tooreceive gateway da un dispositivo SensorTag e inviarla toohello dashboard di monitoraggio remoto.

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[SensorTag BLE di Texas Instruments][lnk-sensortag]. In questa esercitazione consente di recuperare i dati di telemetria tramite Bluetooth dal dispositivo SensorTag hello.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Hello remoto disposizioni soluzione monitoraggio di un set di servizi di Azure nella sottoscrizione di Azure. distribuzione di Hello riflette un'architettura aziendale reale. tooavoid addebiti di consumo di Azure, eliminare l'istanza di soluzione hello preconfigurato azureiotsuite.com dopo aver con esso. Se è necessario hello nuovamente la soluzione preconfigurata, è possibile ricrearla facilmente. Per ulteriori informazioni sulla riduzione del consumo durante l'esecuzione di soluzioni di monitoraggio remoto hello, vedere [configurazione Azure IoT Suite preconfigurato soluzioni per scopi dimostrativi][lnk-demo-config].

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a>Configurare la connettività Bluetooth

Configurare la funzione Bluetooth nel dispositivo tooconnect di hello Intel NUC tooenable hello SensorTag e inviare dati di telemetria.

### <a name="find-hello-mac-address-of-hello-sensortag"></a>Trovare l'indirizzo MAC hello di hello SensorTag

1. Nella shell di hello in hello NUC Intel, eseguire hello comando toounblock hello Bluetooth servizio:

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. La seguente esecuzione hello comandi toostart hello Bluetooth servizio hello NUC Intel e immettere shell Bluetooth hello:

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. Eseguire hello toopower comando sul controller Bluetooth hello seguenti:

    ```bash
    power on
    ```

    Quando il controller hello è attiva, viene visualizzato un messaggio **la modifica di alimentazione in cui ha avuto esito positivo**.

1. Eseguire hello tooscan di comando per i dispositivi Bluetooth circostanti seguenti:

    ```bash
    scan on
    ```

1. Premere hello power pulsante toomake SensorTag hello è individuabile. fa lampeggiare il LED verde Hello.

1. Quando viene visualizzato un messaggio nella shell di hello tale controller hello ha individuato hello SensorTag, prendere nota dell'indirizzo MAC del dispositivo hello hello. Hello indirizzo MAC è simile a **A0:E6:F8:B5:F6:00**. Indirizzo MAC hello è necessario più avanti nell'esercitazione di hello quando si configura gateway hello.

1. Eseguire hello successivo comando tooturn la scansione Bluetooth:

    ```bash
    scan off
    ```

1. Eseguire hello dopo che è possibile collegare il dispositivo di SensorTag toohello tooverify di comando:

    ```bash
    connect <SensorTag MAC address>
    ```

    Se ci si connette correttamente, la shell hello Mostra messaggio hello **connessione riuscita** e Visualizza informazioni sul dispositivo SensorTag hello. Se non è possibile connettersi, controllare hello che sensortag è ancora attiva.

1. È ora possibile disconnettersi dalle hello SensorTag e uscire dalla shell Bluetooth hello eseguendo hello seguenti comandi:

    ```bash
    disconnect
    exit
    ```

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
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

script di compilazione Hello inserisce modulo IoT Edge di hello libsensor2remotemonitoring.so personalizzato nella cartella di compilazione hello.

## <a name="configure-and-run-hello-iot-edge-gateway"></a>Configurare ed eseguire hello gateway perimetrale IoT

È ora possibile configurare hello telemetria di IoT Edge gateway toosend dal dispositivo SensorTag per tooyour dashboard di monitoraggio remoto. Per altre informazioni sulla configurazione di un gateway e sui moduli IoT Edge, vedere [Concetti di Azure IoT Edge][lnk-gateway-concepts].

> [!TIP]
> In questa esercitazione è utilizzare standard di hello `vi` editor di testo in hello NUC Intel. Se non è stato utilizzato `vi` prima, si consiglia di completare un'esercitazione introduttiva, ad esempio [Unix - hello vi Editor esercitazione] [ lnk-vi-tutorial] toofamiliarize familiarità con questo editor. In alternativa, è possibile installare più semplice hello [nano](https://www.nano-editor.org/) editor utilizzando il comando hello `smart install nano -y`.

File di configurazione di esempio hello Open in hello **vi** editor utilizzando hello comando seguente:

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
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
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

Sostituire hello **macAddress** segnaposto con hello indirizzo MAC del SensorTag è indicato in precedenza. Sostituire hello **deviceID** e **deviceKey** segnaposto con ID hello e le chiavi per i dispositivi hello due creato in precedenza nella soluzione di monitoraggio remoto hello.

Individuare hello seguendo le linee nella configurazione di hello per modulo SensorTag hello:

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

Sostituire hello **dispositivo\_mac\_indirizzo** segnaposto con hello indirizzo MAC del SensorTag è indicato in precedenza.

Salvare le modifiche.

È ora possibile eseguire il gateway di hello tramite hello seguenti comandi:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

Hello gateway perimetrale IoT inizia hello NUC Intel e invia i dati di telemetria dalla soluzione di monitoraggio remoto toohello SensorTag hello:

![Gateway di confine IoT invia dati di telemetria da hello SensorTag][img-telemetry]

Premere **Ctrl-C** programma hello tooexit in qualsiasi momento.

## <a name="view-hello-telemetry"></a>Visualizzazione hello telemetria

gateway Hello ora invia dati di telemetria da hello SensorTag dispositivo toohello soluzione di monitoraggio remoto. È possibile visualizzare i dati di telemetria hello nel dashboard di soluzione hello. È anche possibile inviare dispositivo SensorTag tooyour di comandi tramite gateway hello dal dashboard di soluzione hello.

- Passare il dashboard di soluzione toohello.
- Dispositivo hello selezionare configurato nel gateway hello che rappresenta Ciao SensorTag hello **tooView dispositivo** elenco a discesa.
- Consente di visualizzare dati di telemetria Hello dal dispositivo SensorTag hello nel dashboard di hello.

![Visualizzare i dati di telemetria dai dispositivi SensorTag hello][img-telemetry-display]

> [!WARNING]
> Se si lascia in esecuzione nell'account di Azure di soluzione di monitoraggio remoto hello, verrà addebitato per volta hello che è in esecuzione. Per ulteriori informazioni sulla riduzione del consumo durante l'esecuzione di soluzioni di monitoraggio remoto hello, vedere [configurazione Azure IoT Suite preconfigurato soluzioni per scopi dimostrativi][lnk-demo-config]. Eliminare la soluzione hello preconfigurato dall'account di Azure al termine dell'utilizzo.


## <a name="next-steps"></a>Passaggi successivi

Visitare hello [Centro per sviluppatori Azure IoT](https://azure.microsoft.com/develop/iot/) per ulteriori esempi e documentazione su Azure IoT.

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started