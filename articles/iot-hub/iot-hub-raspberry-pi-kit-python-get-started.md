---
title: aaaRaspberry Pi toocloud (Python) - connessione Pi Raspberry tooAzure IoT Hub | Documenti Microsoft
description: Informazioni su come toosetup e connettersi Pi Raspberry tooAzure IoT Hub per la piattaforma cloud di Azure Pi Raspberry toosend dati toohello in questa esercitazione.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Azure iot al lampone pi greco, al lampone pi iot hub, al lampone pi trasmissione dati toocloud, al lampone pi toocloud
ms.service: iot-hub
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/31/2017
ms.author: xshi
ms.openlocfilehash: 86f5c91ab9dd4e23c563437827fb7d2d06916d2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-python"></a>Connettersi Pi Raspberry tooAzure IoT Hub (Python)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

In questa esercitazione, è necessario innanzitutto apprendimento hello nozioni fondamentali sulle operazioni con Pi Raspberry Raspbian in esecuzione. Si apprenderà quindi la modalità di connessione cloud toohello dispositivi utilizzando tooseamlessly [IoT Hub Azure](iot-hub-what-is-iot-hub.md). Per esempi di Windows 10 IoT Core, vedere toohello [Windows Dev Center](http://www.windowsondevices.com/).

Se non si ha ancora un kit, Provare il [simulatore online Raspberry Pi](iot-hub-raspberry-pi-web-simulator-get-started.md). In alternativa, acquistare un nuovo kit [qui](https://azure.microsoft.com/develop/iot/starter-kits).

## <a name="what-you-do"></a>Operazioni da fare

* Creare un hub IoT.
* Registrare un dispositivo per Pi nel proprio hub IoT.
* Installare Raspberry Pi.
* Eseguire un'applicazione di esempio nell'hub IoT di pi greco toosend sensore dati tooyour.

Connettersi Pi Raspberry tooan l'hub IoT creati. Quindi eseguire un'applicazione di esempio in dati di temperatura e umidità toocollect Pi da un sensore BME280. Infine, si invia l'hub IoT hello sensore dati tooyour.

## <a name="what-you-learn"></a>Contenuto dell'esercitazione

* Come toocreate un hub IoT di Azure e ottenere la stringa di connessione nuovo dispositivo.
* Come tooconnect Pi con un sensore BME280.
* Come dati del sensore toocollect mediante l'esecuzione di un'applicazione di esempio su Pi.
* Come l'hub IoT toosend sensore dati tooyour.

## <a name="what-you-need"></a>Elementi necessari

![Elementi necessari](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* Hello Raspberry Pi 2 o 3 Pi Raspberry Lavagna.
* Una sottoscrizione di Azure attiva. Se non si ha un account Azure, [creare un account Azure gratuito](https://azure.microsoft.com/free/) in pochi minuti.
* Un monitoraggio, una tastiera e mouse che si connettono tooPi.
* Un Mac o PC che esegue Windows o Linux.
* Una connessione Internet.
* Una scheda microSD da 16 GB o più.
* Un USB SD adapter o microSD card tooburn hello immagine del sistema operativo nella scheda microSD hello.
* Alimentatore di 2 amp 5 volt con il cavo USB micro di hello 6 piedi.

Hello seguenti elementi è facoltativo:

* Un sensore Adafruit BME280 assemblato per rilevare umidità, temperatura e pressione.
* Una basetta sperimentale.
* 6 cavi ponticello F/M.
* Un LED da 10 mm a luce diffusa.


> [!NOTE] 
Poiché il supporto di esempio di codice hello simulati i dati del sensore, questi elementi sono facoltativi.


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="set-up-raspberry-pi"></a>Installare Raspberry Pi

### <a name="install-hello-raspbian-operating-system-for-pi"></a>Installazione del sistema operativo di hello Raspbian per Pi

Preparare una scheda microSD hello per l'installazione dell'immagine Raspbian hello.

1. Scaricare Raspbian.
   1. [Scaricare Raspbian Jessie con Desktop](https://www.raspberrypi.org/downloads/raspbian/) (file con estensione zip hello).
   1. Estrarre la cartella di hello Raspbian immagine tooa nel computer in uso.
1. Installare una scheda microSD di Raspbian toohello.
   1. [Scaricare e installare hello Etcher SD card masterizzatore utilità](https://etcher.io/).
   1. Eseguire Etcher e selezionare l'immagine Raspbian hello estratta nel passaggio 1.
   1. Selezionare un'unità scheda microSD hello. Si noti che Etcher potrebbe essere stata già selezionata unità corretta hello.
   1. Fare clic sulla scheda microSD toohello Raspbian di tooinstall Flash.
   1. Rimuovi scheda microSD hello dal computer al termine dell'installazione. Scheda microSD di hello tooremove provvisoria è direttamente perché Etcher Smonta scheda microSD hello dopo il completamento o rimuove automaticamente.
   1. Inserire scheda microSD hello Pi.

### <a name="enable-ssh-and-i2c"></a>Abilitare SSH e I2C

1. Collegare monitor toohello Pi, tastiera e mouse, avviare l'installazione guidata piattaforma e l'accesso Raspbian utilizzando `pi` come nome utente hello e `raspberry` come password hello.
1. Fare clic sull'icona al lampone hello > **preferenze** > **Raspberry Pi configurazione**.

   ![menu Preferenze Raspbian Hello](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. In hello **interfacce** scheda, impostare **I2C** e **SSH** troppo**abilitare**, quindi fare clic su **OK**. Se non hai sensori fisici e desidera toouse simulato sensore dati, questo passaggio è facoltativo.

   ![Abilitare I2C e SSH su Raspberry Pi](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
tooenable SSH e I2C, è possibile trovare più documenti di riferimento su [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) e [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).

### <a name="connect-hello-sensor-toopi"></a>Connettersi hello sensore tooPi

Utilizzare hello breadboard e ponticelli cavi tooconnect un LED e un tooPi BME280 come indicato di seguito. Se non si dispone di sensore hello, [ignorare questa sezione](#connect-pi-to-the-network).

![Hello Raspberry Pi e sensore connessione](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

sensore Hello BME280 possibile raccogliere dati di temperatura e umidità. E hello LED lampeggia se esiste una comunicazione tra i dispositivi e hello cloud. 

Per i codici PIN sensore, utilizzare hello seguente collegamento:

| Inizio (sensore e LED)     | Fine (scheda)            | Colore del cavo   |
| -----------------------  | ---------------------- | ------------: |
| VDD (Pin 5G)             | 3,3 V PWR (Pin 1)       | Cavo bianco   |
| GND (Pin 7G)             | GND (Pin 6)            | Cavo marrone   |
| SDI (Pin 10G)            | I2C1 SDA (Pin 3)       | Cavo rosso     |
| SCK (Pin 8G)             | I2C1 SCL (Pin 5)       | Cavo arancione  |
| LED VDD (Pin 18F)        | GPIO 24 (Pin 18)       | Cavo bianco   |
| LED GND (Pin 17F)        | GND (Pin 20)           | Cavo nero   |

Fare clic su tooview [Raspberry Pi 2 e 3 mapping Pin](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) per riferimento.

Dopo aver collegato correttamente BME280 tooyour Raspberry Pi, dovrebbe essere sotto l'immagine.

![Pi e BME280 connessi](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a>Connessione di rete toohello Pi

Attivare Pi tramite cavo USB micro hello e alimentatore hello. Utilizzare hello Ethernet via cavo tooconnect Pi tooyour cablate di rete o seguire hello [istruzioni hello Foundation Pi Raspberry](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour rete. Dopo l'installazione guidata piattaforma toohello connessione rete, è necessario annotare hello tootake [indirizzo IP del pi greco](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).

![Rete toowired connesso](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> Assicurarsi che l'installazione guidata piattaforma sia connesso toohello stessa rete del computer. Ad esempio, se il computer è connesso tooa rete wireless mentre Pi è connesso tooa rete cablata, si potrebbe visualizzare non hello IP indirizzo nell'output di hello devdisco.

## <a name="run-a-sample-application-on-pi"></a>Eseguire un'applicazione di esempio in Pi

### <a name="install-hello-prerequisite-packages"></a>Installare i pacchetti dei prerequisiti hello

Utilizzare uno dei seguenti client SSH dagli tooyour di tooconnect computer host Pi Raspberry hello.
   
   **Utenti Windows**
   1. Scaricare e installare [PuTTY](http://www.putty.org/) per Windows. 
   1. Copiare l'indirizzo IP hello della sezione Pi in nome Host di hello (o indirizzo IP) e selezionare il tipo di connessione hello SSH.
   
   
   **Utenti Mac e Ubuntu**
   
   Utilizzare client SSH incorporato hello in Ubuntu o macOS. Potrebbe essere necessario toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.
   > [!NOTE] 
   nome utente predefinito Hello `pi` , e la password di hello è `raspberry`.


### <a name="configure-hello-sample-application"></a>Configurare l'applicazione di esempio hello

1. Clonare l'applicazione di esempio hello eseguendo hello comando seguente:

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-python-raspberrypi-client-app.git
   ```
1. Aprire il file di configurazione hello eseguendo hello seguenti comandi:

   ```bash
   cd iot-hub-python-raspberrypi-client-app
   nano config.py
   ```

   Questo file contiene 5 macro configurabili. Hello prima uno è `MESSAGE_TIMESPAN`, che definisce l'intervallo di tempo hello (in millisecondi) tra i due messaggi che inviano toocloud. Hello secondo `SIMULATED_DATA`, ovvero un valore booleano per se toouse sensore dati simulati o non. `I2C_ADDRESS`è in indirizzo hello I2C che è connesso il sensore BME280. `GPIO_PIN_ADDRESS`è l'indirizzo GPIO hello per il LED. Hello ultimo uno è `BLINK_TIMESPAN`, cui definito timespan hello quando il LED è attivata in millisecondi.

   Se si **non dispone di sensore hello**, hello impostare `SIMULATED_DATA` valore troppo`True` applicazione di esempio hello toomake creare e utilizzare dati del sensore simulato.

1. Salvare e uscire premendo CTRL-O > Invio > CTRL-X.

### <a name="build-and-run-hello-sample-application"></a>Compilare ed eseguire l'applicazione di esempio hello

1. Compilare l'applicazione di esempio hello eseguendo hello comando seguente. Poiché hello Azure IoT SDK per Python sono wrapper su hello Azure IoT dispositivo C SDK, sarà necessario librerie hello C toocompile se è preferibile o necessario toogenerate hello Python di librerie da codice sorgente.

   ```bash
   sudo chmod u+x setup.sh
   sudo ./setup.sh
   ```
   > [!NOTE] 
   È inoltre possibile specificare la versione di hello da eseguendo `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`. Se si esegue uno script senza parametri, script hello rileverà automaticamente versione hello di python installato (sequenza di ricerca 2.7 -> 3.4 -> 3.5). Assicurarsi che la versione di Python rimanga coerente durante la compilazione e l'esecuzione. 
   
   > [!NOTE] 
   Sulla compilazione libreria client Python di hello (iothub_client.so) nei dispositivi Linux con meno di 1GB di RAM, può vedere compilare accumulano durante la compilazione iothub_client_python.cpp, come illustrato di seguito al 98% `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`. Se si esegue questo problema, controllare il consumo di memoria hello di hello dispositivo utilizzando `free -m command` in un'altra finestra terminal questo periodo di tempo. Se si utilizza memoria insufficiente durante la compilazione di file iothub_client_python.cpp, potrebbe essere tootemporarily aumentare tooget spazio di swapping hello è più disponibile memoria toosuccessfully compilare libreria SDK del dispositivo hello del client Python.
   
1. Eseguire l'applicazione di esempio hello eseguendo hello comando seguente:

   ```bash
   python app.py '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   Assicurarsi copiare e incollare stringa di connessione del dispositivo hello in virgolette hello. E, se si usa python hello 3, è possibile utilizzare hello comando `python3 app.py '<your Azure IoT hub device connection string>'`.


   Verrà visualizzato l'output seguente hello che mostra hello sensore dati e hello i messaggi vengono inviati tooyour IoT hub.

   ![Output - sensore dati vengono inviati da tooyour Raspberry Pi hub IoT](media/iot-hub-raspberry-pi-kit-c-get-started/success.png
)

## <a name="next-steps"></a>Passaggi successivi

È stato eseguito dati sensore toocollect di applicazione di esempio e inviarlo tooyour IoT hub. messaggi hello toosee che l'installazione guidata piattaforma Raspberry ha inviato IoT tooyour hub o trasmissione tooyour messaggi Pi Raspberry in un'interfaccia della riga di comando, vedere hello [dispositivo cloud Gestione messaggistica esercitazione hub IOT Esplora](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
