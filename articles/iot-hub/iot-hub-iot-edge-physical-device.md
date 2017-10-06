---
title: un dispositivo fisico con Azure IoT Edge aaaUse | Documenti Microsoft
description: Come toouse un hub IoT tooan di Texas strumenti SensorTag dispositivo toosend dati tramite un gateway perimetrale IoT in esecuzione in un dispositivo Raspberry Pi 3. gateway Hello viene creato utilizzando Azure IoT Edge.
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 212dacbf-e5e9-48b2-9c8a-1c14d9e7b913
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: andbuc
ms.openlocfilehash: a2385accdbd99012ad094232653ee47d4e5c7839
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-tooforward-device-to-cloud-messages-tooiot-hub"></a>Utilizzare Azure IoT Edge su un tooIoT di messaggi da dispositivo a cloud tooforward Pi Raspberry Hub

Questa procedura dettagliata di hello [esempio consumo energetico Bluetooth] [ lnk-ble-samplecode] illustra come toouse [Azure IoT Edge] [ lnk-sdk] per:

* Inoltrare i dati di telemetria da dispositivo a cloud tooIoT Hub da un dispositivo fisico.
* Inviare i comandi dal dispositivo fisico tooa di IoT Hub.

In questa procedura dettagliata verranno trattati i seguenti argomenti:

* **Architettura**: importanti informazioni architetturale: esempio hello Bluetooth consumo energetico.
* **Compilare ed eseguire**: esempio di esecuzione hello e toobuild necessari passaggi di hello.

## <a name="architecture"></a>Architettura

Hello dettagliata mostra come toobuild ed eseguire un gateway esterno IoT su 3 Pi Raspberry che esegue Raspbian Linux. gateway Hello viene compilato utilizzando IoT Edge. esempio Hello utilizza una data di temperatura toocollect dispositivo Texas strumenti SensorTag Bluetooth bassa energia (disattiva).

Quando si esegue hello gateway perimetrale IoT è:

* Connette il dispositivo di SensorTag tooa utilizzando il protocollo di energia bassa Bluetooth (disattiva) hello.
* Si connette tooIoT Hub utilizzando il protocollo HTTP hello.
* Inoltra i dati di telemetria da hello SensorTag dispositivo tooIoT Hub.
* Invia i comandi dal dispositivo di SensorTag toohello IoT Hub.

gateway Hello contiene i seguenti moduli IoT Edge hello:

* Oggetto *modulo BILITA* che interagisce con i dati di temperatura tooreceive dispositivo un BILITA da dispositivi hello e invia i comandi toohello.
* Oggetto *modulo toodevice di cloud BILITA* che converte i messaggi JSON inviati dall'IoT Hub in istruzioni BILE per hello *modulo BILITA*.
* Oggetto *modulo logger* che registra tutti i gateway messaggi tooa file locale.
* Un *modulo di mapping delle identità* che esegue la conversione tra gli indirizzi MAC del dispositivo BLE e le identità dispositivo dell'hub IoT di Azure.
* Un *modulo IoT Hub* che consente di caricare hub IoT tooan dati di telemetria e riceve i comandi di dispositivo da un hub IoT.
* Oggetto *modulo stampante BILITA* che viene interpretata la telemetria dal dispositivo BILITA hello e stampa dati formattati toohello console tooenable risoluzione e il debug.

### <a name="how-data-flows-through-hello-gateway"></a>Il flusso dei dati tramite il gateway hello

Hello seguente diagramma a blocchi di seguito viene illustrato come pipeline di flusso dati di caricamento di hello telemetria.

![Pipeline di caricamento dei dati di telemetria attraverso il gateway](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

passaggi di Hello che un elemento di dati di telemetria accetta gli spostamenti da un tooIoT dispositivo BILITA Hub sono:

1. dispositivo BILITA Hello genera un campione di temperatura e lo invia tramite Bluetooth toohello BILITA modulo gateway hello.
1. modulo BILITA Hello riceve l'esempio hello e pubblica broker toohello con indirizzo MAC hello del dispositivo hello.
1. modulo di mapping identità Hello preleva il messaggio e utilizza un hello tootranslate tabella interna indirizzo MAC del dispositivo hello in un'identità del dispositivo IoT Hub. Un'identità dispositivo dell'hub IoT è costituita da un ID di dispositivo e una chiave del dispositivo.
1. modulo di mapping identità Hello pubblica un nuovo messaggio che contiene dati di esempio hello temperatura, l'indirizzo MAC di hello del dispositivo hello e ID dispositivo hello chiave hello del dispositivo.
1. modulo di IoT Hub Hello riceve questo messaggio nuovo (generato dal modulo di mapping identità hello) e pubblica tooIoT Hub.
1. modulo di logger Hello registra tutti i messaggi da file di hello broker tooa locale.

Hello seguente diagramma a blocchi di seguito viene illustrato come pipeline di flusso dati di hello dispositivo comando:

![Pipeline dell'invio dei comandi del dispositivo attraverso il gateway](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. IoT Hub modulo esegue periodicamente il polling di Hello hello hub IoT per i nuovi messaggi di comando.
1. Quando il modulo di IoT Hub hello riceve un nuovo messaggio di comando, vengono pubblicati toohello broker.
1. modulo di mapping identità Hello preleva il messaggio di comando hello e utilizza un hello tootranslate tabella interna IoT Hub ID tooa dispositivo indirizzo MAC. Quindi, vengono pubblicati un nuovo messaggio che include l'indirizzo MAC di hello hello per dispositivo di destinazione nel mapping di proprietà hello del messaggio hello.
1. modulo BILITA Cloud a dispositivo Hello preleva il messaggio e lo converte in istruzione BILITA corretta di hello per il modulo BILITA hello. Dopodiché pubblica un nuovo messaggio.
1. modulo BILITA Hello preleva il messaggio ed esegue istruzioni dei / o hello comunicando con dispositivo BILITA hello.
1. modulo di logger Hello registra tutti i messaggi dal file di disco tooa broker hello.

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa esercitazione, è necessaria una sottoscrizione di Azure attiva.

> [!NOTE]
> Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk-free-trial].

È necessario client SSH nel tooenable computer desktop è tooremotely accesso hello della riga di comando in hello Raspberry Pi.

- Windows non include un client SSH. È consigliabile usare [PuTTY](http://www.putty.org/).
- La maggior parte delle distribuzioni di Linux e Mac OS includono hello della riga di comando SSH utilità. Per altre informazioni, vedere [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (SSH con Linux o Mac OS).

## <a name="prepare-your-hardware"></a>Preparare l'hardware

In questa esercitazione si presuppone l'uso un [SensorTag strumenti Texas](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) dispositivo connesso tooa Raspberry Pi 3 Raspbian di esecuzione.

### <a name="install-raspbian"></a>Installare Raspbian

È possibile utilizzare una delle seguenti opzioni tooinstall Raspbian sul dispositivo Raspberry Pi 3 hello.

* versione più recente di hello tooinstall di Raspbian, utilizzare hello [NOOBS] [ lnk-noobs] interfaccia utente grafica.
* Manualmente [scaricare] [ lnk-raspbian] e scrivere hello immagine più recente della scheda hello Raspbian del sistema operativo tooan SD.

### <a name="sign-in-and-access-hello-terminal"></a>Accesso e terminal hello

Sono presenti due opzioni tooaccess un ambiente terminal le Pi Raspberry:

* Se si dispone di una tastiera e monitorare connesso tooyour Raspberry Pi, è possibile utilizzare hello GUI Raspbian tooaccess una finestra terminale.

* Riga di comando hello accesso con le pi greco Raspberry tramite SSH nel computer desktop.

#### <a name="use-a-terminal-window-in-hello-gui"></a>Utilizzare una finestra terminal in hello GUI

le credenziali predefinite Hello per Raspbian sono username **pi** e la password **raspberry**. Nella barra delle applicazioni hello in hello GUI, è possibile avviare hello **Terminal** utilità utilizzando l'icona di hello simile a un monitoraggio.

#### <a name="sign-in-with-ssh"></a>Accedere con SSH

È possibile utilizzare SSH per l'accesso da riga di comando tooyour Raspberry Pi. articolo Hello [SSH (Secure Shell)] [ lnk-pi-ssh] viene descritto come tooconfigure SSH sul pi greco Raspberry e come tooconnect da [Windows] [ lnk-ssh-windows] o [Linux e Mac OS][lnk-ssh-linux].

Accedere con il nome utente **pi** e la password **raspberry**.

### <a name="install-bluez-537"></a>Installare BlueZ 5.37

i moduli BILITA Hello comunicare toohello Bluetooth hardware tramite stack BlueZ hello. È necessario versione 5.37 di BlueZ per hello moduli toowork correttamente. Queste istruzioni assicurarsi che sia installata hello versione corretta di BlueZ.

1. Arrestare il daemon bluetooth corrente di hello:

    ```sh
    sudo systemctl stop bluetooth
    ```

1. Installare le dipendenze BlueZ hello:

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. Scaricare il codice sorgente di hello BlueZ da bluez.org:

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. Decomprimere il codice sorgente hello:

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. Cambia cartella toohello appena creato di directory:

    ```sh
    cd bluez-5.37
    ```

1. Configurare hello BlueZ codice toobe compilato:

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. Compilare BlueZ:

    ```sh
    make
    ```

1. Al termine, installare BlueZ:

    ```sh
    sudo make install
    ```

1. Modificare la configurazione di servizio per bluetooth in modo che punti toohello nuovo daemon bluetooth nel file hello systemd `/lib/systemd/system/bluetooth.service`. Sostituire riga 'ExecStart' hello con hello seguente testo:

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-toohello-sensortag-device-from-your-raspberry-pi-3-device"></a>Abilitazione del dispositivo SensorTag toohello connettività dal dispositivo Raspberry Pi 3

Prima di esempio hello in esecuzione, è necessario che il Pi 3 Raspberry possano connettersi dispositivo SensorTag toohello tooverify.

1. Assicurarsi di hello `rfkill` utilità è installata:

    ```sh
    sudo apt-get install rfkill
    ```

1. Sbloccare bluetooth su hello Raspberry Pi 3, verificare che il numero di versione di hello **5.37**:

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. shell interattiva bluetooth di hello tooenter, avviare il servizio bluetooth hello ed eseguire hello **bluetoothctl** comando:

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. Immettere il comando hello **accensione** toopower controller bluetooth hello. comando Hello restituisce seguente toohello simili di output:

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. Nella shell interattiva bluetooth hello, immettere il comando hello **analisi** tooscan per i dispositivi bluetooth. comando Hello restituisce seguente toohello simili di output:

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. Rendere individuabile un dispositivo SensorTag hello premendo hello piccolo pulsante (Buongiorno lampeggiamento LED verde). Hello Raspberry Pi 3 deve individuare dispositivi SensorTag hello:

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    In questo esempio, è possibile visualizzare tale indirizzo MAC di hello SensorTag dispositivo hello **A0:E6:F8:B5:F6:00**.

1. Disattivare l'analisi immettendo hello **analisi** comando:

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. Connettere il dispositivo di SensorTag tooyour tramite il relativo indirizzo MAC immettendo **connettersi \<indirizzo MAC\>**. Per maggiore chiarezza, è abbreviato Hello seguente esempio di output:

    ```sh
    Attempting tooconnect tooA0:E6:F8:B5:F6:00
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: yes
    Connection successful
    [CHG] Device A0:E6:F8:B5:F6:00 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
    ...
    [NEW] Primary Service
            /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
            Device Information
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 GattServices: /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 Name: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Alias: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Modalias: bluetooth:v000Dp0000d0110
    ```

    > È possibile elencare le caratteristiche di GATT hello del dispositivo hello utilizzando hello **elenco attributi** comando.

1. È ora possibile disconnettersi dal dispositivo hello utilizzando hello **disconnettere** comando e uscire dalla shell bluetooth hello utilizzando hello **chiudere** comando:

    ```sh
    Attempting toodisconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

A questo punto è pronto toorun: esempio hello IoT Edge disattiva il 3 Pi Raspberry.

## <a name="run-hello-iot-edge-ble-sample"></a>Eseguire l'esempio IoT Edge BILITA hello

esempio di IoT Edge BILITA toorun hello, è necessario toocomplete tre attività:

* Configurare due dispositivi di esempio nell'hub IoT.
* Compilare IoT Edge sul dispositivo Raspberry Pi 3.
* Configurare ed eseguire l'esempio BILITA hello sul dispositivo Raspberry Pi 3.

Al momento della scrittura hello IoT Edge supporta solo i moduli BILITA gateway su Linux.

### <a name="configure-two-sample-devices-in-your-iot-hub"></a>Configurare due dispositivi di esempio nell'hub IoT

* [Creazione di un hub IoT] [ lnk-create-hub] nella sottoscrizione di Azure, è necessario il nome di hello di toocomplete l'hub in questa procedura dettagliata. Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.
* Aggiungere un dispositivo chiamato **SensorTag_01** tooyour IoT hub e prendere nota della chiave id e dispositivo. È possibile utilizzare hello [Esplora dispositivo o l'hub IOT-Esplora] [ lnk-explorer-tools] strumenti tooadd l'hub IoT toohello di dispositivi creata nel passaggio precedente hello e tooretrieve la relativa chiave. Eseguire il mapping in questo dispositivo toohello SensorTag dispositivo quando si configura gateway hello.

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a>Compilare Azure IoT Edge su Raspberry Pi 3

Installare le dipendenze per Azure IoT Edge:

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

I comandi seguenti di hello utilizzare, tooclone IoT Edge e tutti i relativi dei Sottomoduli tooyour home directory:

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

Quando si dispone di una copia completa di hello repository IoT bordo il 3 Pi Raspberry, è possibile compilare utilizzando hello comando seguente dalla cartella hello contenente hello SDK:

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-hello-ble-sample-on-your-raspberry-pi-3"></a>Configurare ed eseguire l'esempio BILITA hello il 3 Pi Raspberry

toobootstrap e l'esempio hello esecuzione, è necessario configurare ogni modulo IoT Edge che partecipa nel gateway hello. La configurazione viene definita in un file JSON ed è necessario configurare tutti e cinque i moduli IoT Edge coinvolti. È un file JSON di esempio in repository hello denominato **gateway\_sample.json** che è possibile utilizzare come punto di partenza per la creazione di un file di configurazione hello. Questo file è hello **ble_gateway/samples/src** cartella nella copia locale di hello repository IoT Edge.

Hello nelle sezioni seguenti descrivono come tooedit questa configurazione del file di esempio BILITA hello e si presuppone che hello repository IoT Edge è hello **/home/pi/iot-edge /** cartella il Raspberry Pi 3. Se il repository di hello è altrove, regolare i percorsi di hello.

#### <a name="logger-configuration"></a>Configurazione del modulo logger

Presupponendo che si trova il repository di gateway hello in hello **/home/pi/iot-edge /** cartella, configurare il modulo di logger hello come segue:

```json
{
  "name": "Logger",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path" : "build/modules/logger/liblogger.so"
    }
  },
  "args":
  {
    "filename": "<</path/to/log-file.log>>"
  }
}
```

#### <a name="ble-module-configuration"></a>Configurazione del modulo BLE

configurazione di esempio Hello per dispositivo BILITA hello presuppone un dispositivo SensorTag strumenti Texas. Qualsiasi dispositivo BILITA standard che può operare come un GATT periferiche dovrebbero funzionare, ma potrebbe essere necessario tooupdate hello GATT caratteristica ID e dati. Aggiungere l'indirizzo MAC hello del dispositivo SensorTag:

```json
{
  "name": "SensorTag",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble.so"
    }
  },
  "args": {
    "controller_index": 0,
    "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
    "instructions": [
      {
        "type": "read_once",
        "characteristic_uuid": "00002A24-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A25-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A26-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A27-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A28-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A29-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "write_at_init",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AQ=="
      },
      {
        "type": "read_periodic",
        "characteristic_uuid": "F000AA01-0451-4000-B000-000000000000",
        "interval_in_ms": 1000
      },
      {
        "type": "write_at_exit",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AA=="
      }
    ]
  }
}
```

Se non si utilizza un dispositivo SensorTag, vedere documentazione di hello per le toodetermine dispositivo BILITA se è necessario tooupdate hello GATT caratteristica ID e i valori dei dati.

#### <a name="iot-hub-module"></a>modulo dell'hub IoT

Aggiungere il nome di hello dell'IoT Hub. valore suffisso Hello è in genere **azure devices.net**:

```json
{
  "name": "IoTHub",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/iothub/libiothub.so"
    }
  },
  "args": {
    "IoTHubName": "<<Azure IoT Hub Name>>",
    "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
    "Transport" : "amqp"
  }
}
```

#### <a name="identity-mapping-module-configuration"></a>Configurazione del modulo di mapping delle identità

Aggiungere l'indirizzo MAC di hello del dispositivo SensorTag e hello dispositivo chiave e ID di hello **SensorTag_01** dispositivo tooyour IoT Hub è stato aggiunto:

```json
{
  "name": "mapping",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/identitymap/libidentity_map.so"
    }
  },
  "args": [
    {
      "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
      "deviceId": "<<Azure IoT Hub Device ID>>",
      "deviceKey": "<<Azure IoT Hub Device Key>>"
    }
  ]
}
```

#### <a name="ble-printer-module-configuration"></a>Configurazione del modulo di stampa BLE

```json
{
  "name": "BLE Printer",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/samples/ble_gateway/ble_printer/libble_printer.so"
    }
  },
  "args": null
}
```

#### <a name="blec2d-module-configuration"></a>Configurazione del modulo BLEC2D

```json
{
  "name": "BLEC2D",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble_c2d.so"
    }
  },
  "args": null
}
```

#### <a name="routing-configuration"></a>Configurazione di routing

la configurazione seguente Hello assicura seguente hello routing tra i moduli di IoT Edge:

* Hello **Logger** modulo riceve e registra tutti i messaggi.
* Hello **SensorTag** modulo Invia hello tooboth messaggi **mapping** e **stampante BILITA** moduli.
* Hello **mapping** modulo Invia messaggi toohello **l'hub IOT** toobe modulo inviato tooyour IoT Hub.
* Hello **l'hub IOT** modulo Invia messaggi di risposta toohello **mapping** modulo.
* Hello **mapping** modulo Invia messaggi toohello **BLEC2D** modulo.
* Hello **BLEC2D** modulo Invia messaggi di risposta toohello **Tag sensore** modulo.

```json
"links" : [
    {"source" : "*", "sink" : "Logger" },
    {"source" : "SensorTag", "sink" : "mapping" },
    {"source" : "SensorTag", "sink" : "BLE Printer" },
    {"source" : "mapping", "sink" : "IoTHub" },
    {"source" : "IoTHub", "sink" : "mapping" },
    {"source" : "mapping", "sink" : "BLEC2D" },
    {"source" : "BLEC2D", "sink" : "SensorTag"}
 ]
```

esempio hello toorun, file di configurazione JSON per la toohello percorso pass hello come un parametro di toohello **bilita\_gateway** binario. Hello comando riportato di seguito si presuppone l'uso hello **gateway_sample.json** file di configurazione. Eseguire il comando seguente da hello **iot edge** cartella hello Raspberry Pi:

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

Potrebbe essere necessario toopress hello piccolo pulsante hello SensorTag dispositivo toomake è individuabile prima di eseguire l'esempio hello.

Quando si esegue l'esempio hello, è possibile utilizzare hello [Esplora dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) o hello [l'hub IOT Esplora](https://github.com/Azure/iothub-explorer) hello messaggi hello toomonitor di strumento gateway perimetrale IoT inoltra dal dispositivo SensorTag hello. Ad esempio, tramite l'hub IOT explorer è possibile monitorare i messaggi da dispositivo a cloud utilizzando hello comando seguente:

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a>Inviare messaggi da cloud a dispositivo

modulo BILITA Hello supporta anche l'invio di comandi dal dispositivo toohello IoT Hub. È possibile utilizzare hello [Esplora dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) o hello [l'hub IOT Esplora](https://github.com/Azure/iothub-explorer) i messaggi JSON di strumento toosend modulo hello BILITA gateway inoltra sul dispositivo BILITA toohello.

Se si usa hello Texas strumenti SensorTag dispositivo, è possibile attivare il LED di colore rosso hello, LED verde o cicalino inviando i comandi da IoT Hub. Prima di inviare comandi dall'IoT Hub, inviare innanzitutto hello due messaggi JSON nell'ordine seguente. È quindi possibile inviare qualsiasi hello comandi tooturn luci hello o cicalino.

1. Reimposta tutti i LED e cicalino hello (spegnerli):

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. Configurare l'I/O come "remote":

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

È ora possibile inviare uno qualsiasi dei seguenti comandi tooturn luci hello o cicalino sul dispositivo SensorTag hello hello:

* Attiva il LED di colore rosso hello:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* Attiva il LED verde hello:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* Attivare cicalino hello:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a>Passaggi successivi

Se si desidera toogain conoscenze più avanzate del bordo IoT e sperimentare alcuni esempi di codice, visitare hello esercitazioni per sviluppatori e risorse:

* [Azure IoT Edge][lnk-sdk]

toofurther esplorare le funzionalità di hello di IoT Hub, vedere:

* [Guida per gli sviluppatori dell'hub IoT][lnk-devguide]

<!-- Links -->
[lnk-ble-samplecode]: https://github.com/Azure/iot-edge/tree/master/samples/ble_gateway
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-explorer-tools]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/manage_iot_hub.md
[lnk-sdk]: https://github.com/Azure/iot-edge/
[lnk-noobs]: https://www.raspberrypi.org/documentation/installation/noobs.md
[lnk-raspbian]: https://www.raspberrypi.org/downloads/raspbian/
[lnk-devguide]: iot-hub-devguide.md
[lnk-create-hub]: iot-hub-create-through-portal.md 
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
