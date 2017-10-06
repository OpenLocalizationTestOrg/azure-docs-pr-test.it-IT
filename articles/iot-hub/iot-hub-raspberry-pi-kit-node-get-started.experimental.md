---
title: aaaRaspberry Pi toocloud (Node.js) - connessione Pi Raspberry tooAzure IoT Hub | Documenti Microsoft
description: Connettersi Pi Raspberry tooAzure IoT Hub per Pi Raspberry toosend dati toohello cloud di Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure iot al lampone pi greco, al lampone pi iot hub, al lampone pi trasmissione dati toocloud, al lampone pi toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.openlocfilehash: 07bc66983c427eab8118be18d91abb25deb03ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-nodejs"></a>Connettersi Pi Raspberry tooAzure IoT Hub (Node.js)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

In questa esercitazione, è necessario innanzitutto apprendimento hello nozioni fondamentali sulle operazioni con Pi Raspberry Raspbian in esecuzione. Si apprenderà quindi la modalità di connessione cloud toohello dispositivi utilizzando tooseamlessly [IoT Hub Azure](iot-hub-what-is-iot-hub.md). Per esempi di Windows 10 IoT Core, vedere toohello [Windows Dev Center](http://www.windowsondevices.com/).

Se non si ha ancora un kit, Provare a hello [Raspberry Pi 3 emulatore](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/). In alternativa, acquistare un nuovo kit [qui](https://azure.microsoft.com/develop/iot/starter-kits).

## <a name="what-you-do"></a>Operazioni da fare

* Installare Raspberry Pi.
* Creare un hub IoT.
* Registrare un dispositivo per Pi nel proprio hub IoT.
* Eseguire un'applicazione di esempio nell'hub IoT di pi greco toosend sensore dati tooyour.

Connettersi Pi Raspberry tooan l'hub IoT creati. Quindi eseguire un'applicazione di esempio in dati di temperatura e umidità toocollect Pi da un sensore BME280. Infine, si invia l'hub IoT hello sensore dati tooyour.

## <a name="what-you-learn"></a>Contenuto dell'esercitazione

* Come toocreate un hub IoT di Azure e ottenere la stringa di connessione nuovo dispositivo.
* Come tooconnect Pi con un sensore BME280.
* Come dati del sensore toocollect mediante l'esecuzione di un'applicazione di esempio su Pi.
* Come l'hub IoT toosend sensore dati tooyour.

## <a name="what-you-need"></a>Elementi necessari

![Elementi necessari](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

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

## <a name="setup-raspberry-pi"></a>Installare Raspberry Pi

### <a name="install-hello-raspbian-operating-system-for-pi"></a>Installazione del sistema operativo di hello Raspbian per Pi

Preparare una scheda microSD hello per l'installazione dell'immagine Raspbian hello.

1. Scaricare Raspbian.
   1. [Scaricare Raspbian Jessie con Pixel](https://www.raspberrypi.org/downloads/raspbian/) (file con estensione zip hello).
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

   ![menu Preferenze Raspbian Hello](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. In hello **interfacce** scheda, impostare **I2C** e **SSH** troppo**abilitare**, quindi fare clic su **OK**. Se non hai sensori fisici e desidera toouse simulato sensore dati, questo passaggio è facoltativo.

   ![Abilitare I2C e SSH su Raspberry Pi](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
tooenable SSH e I2C, è possibile trovare più documenti di riferimento su [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) e [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).

### <a name="connect-hello-sensor-toopi"></a>Connettersi hello sensore tooPi

Utilizzare hello breadboard e ponticelli cavi tooconnect un LED e un tooPi BME280 come indicato di seguito. Se non si dispone di sensore hello, ignorare questa sezione.

![Hello Raspberry Pi e sensore connessione](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

sensore Hello BME280 possibile raccogliere dati di temperatura e umidità. E hello LED lampeggia se esiste una comunicazione tra i dispositivi e hello cloud. 

Per i codici PIN sensore, utilizzare hello seguente collegamento:

| Inizio (sensore e LED)     | Fine (scheda)            | Colore del cavo   |
| -----------------------  | ---------------------- | ------------: |
| VDD (Pin 5G)             | 3,3 V PWR (Pin 1)       | Cavo bianco   |
| GND (Pin 7G)             | GND (Pin 6)            | Cavo marrone   |
| SCK (Pin 8G)             | I2C1 SDA (Pin 3)       | Cavo arancione  |
| SDI (Pin 10G)            | I2C1 SCL (Pin 5)       | Cavo rosso     |
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

### <a name="clone-sample-application-and-install-hello-prerequisite-packages"></a>Clonare l'applicazione di esempio e installare i pacchetti dei prerequisiti hello

1. Utilizzare uno dei seguenti client SSH dagli tooyour di tooconnect computer host Pi Raspberry hello.
    - [PuTTY](http://www.putty.org/) per Windows. È necessario l'indirizzo IP hello del tooconnect Pi tramite SSH.
    - client SSH incorporato Hello in Ubuntu o macOS. Potrebbe essere necessario eseguire `ssh pi@<ip address of pi>` tooconnect Pi via SSH.

   > [!NOTE] 
   nome utente predefinito Hello `pi` , e la password di hello è `raspberry`.

1. Installazione di Node.js e NPM tooyour Pi.
   
   Verificare innanzitutto la versione di Node. js con hello comando seguente. 
   
   ```bash
   node -v
   ```

   Se la versione di hello è inferiore a 4. x o non è presente alcun Node.js sul pi greco, eseguire hello successivo comando tooinstall o aggiornare Node.js.

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. Clonare l'applicazione di esempio hello eseguendo hello comando seguente:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. Installare tutti i pacchetti hello comando seguente. Include Azure IoT SDK per dispositivi, la libreria del sensore BME280 e libreria di Pi per i collegamenti.

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   Potrebbe richiedere diversi minuti toofinish questo denpening processo di installazione per la connessione di rete.

### <a name="configure-hello-sample-application"></a>Configurare l'applicazione di esempio hello

1. Aprire il file di configurazione hello eseguendo hello seguenti comandi:

   ```bash
   nano config.json
   ```

   ![File di configurazione](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   Questo file contiene due elementi configurabili. Hello prima uno è `interval`, che definisce l'intervallo di tempo hello tra due messaggi che inviano toocloud. Hello secondo `simulatedData`, ovvero un valore booleano per se toouse sensore dati simulati o non.

   Se si **non dispone di sensore hello**, hello impostare `simulatedData` valore troppo`true` applicazione di esempio hello toomake creare e utilizzare dati del sensore simulato.

1. Salvare e uscire premendo CTRL-O > Invio > CTRL-X.

### <a name="run-hello-sample-application"></a>Eseguire l'applicazione di esempio hello

1. Eseguire l'applicazione di esempio hello eseguendo hello comando seguente:

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   Assicurarsi copiare e incollare stringa di connessione del dispositivo hello in virgolette hello.


Verrà visualizzato l'output seguente hello che mostra hello sensore dati e hello i messaggi vengono inviati tooyour IoT hub.

![Output - sensore dati vengono inviati da tooyour Raspberry Pi hub IoT](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a>Passaggi successivi

È stato eseguito dati sensore toocollect di applicazione di esempio e inviarlo tooyour IoT hub.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]