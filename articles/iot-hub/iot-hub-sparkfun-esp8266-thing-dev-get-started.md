---
title: aaaESP8266 toocloud - connettersi Sparkfun ESP8266 cosa Dev tooAzure IoT Hub | Documenti Microsoft
description: Informazioni su come toosetup e connettersi tooAzure Sparkfun ESP8266 cosa Dev IoT Hub per tale piattaforma cloud di Azure di toosend dati toohello in questa esercitazione.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 587fe292-9602-45b4-95ee-f39bba10e716
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 19b249df23b6df516634853521c6d532f51014da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-tooazure-iot-hub-in-hello-cloud"></a>Connettersi tooAzure Sparkfun ESP8266 cosa Dev IoT Hub nel cloud hello

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![connessione tra DHT22, Thing Dev e hub IoT](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione

La connessione verrà creato l'hub IoT tooan Sparkfun ESP8266 cosa Dev. Quindi eseguire un'applicazione di esempio sui dati di temperatura e umidità toocollect ESP8266 da un sensore DHT22. Infine, inviare l'hub IoT hello sensore dati tooyour.

> [!NOTE]
> Se si usano altri lavagne ESP8266, è comunque possibile eseguire questi passaggi tooconnect è tooyour IoT hub. A seconda della Lavagna hello ESP8266 in uso, potrebbe essere necessario hello tooreconfigure `LED_PIN`. Ad esempio, se si utilizza ESP8266 da AI Thinker, è possibile modificare tale da `0` troppo`2`. Non si dispone ancora di un kit? Fare clic [qui](http://azure.com/iotstarterkits)

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione

* Come toocreate un hub IoT e registrare un dispositivo per scopi di sviluppo cosa
* Come tooconnect cosa Dev con sensore hello e il computer.
* Come dati del sensore toocollect mediante l'esecuzione di un'applicazione di esempio su cosa scopi di sviluppo
* Come toosend hello hub IoT tooyour di dati del sensore.

## <a name="what-you-will-need"></a>Prerequisiti

![Parti necessarie per l'esercitazione hello](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete questa operazione, è necessario hello dallo Starter Kit di sviluppo cosa le seguenti parti:

* Hello Sparkfun ESP8266 cosa Dev Lavagna.
* Un tooType USB Micro cavo USB A.

Esempio hello è inoltre necessario per l'ambiente di sviluppo:

* Una sottoscrizione di Azure attiva. Se non si ha un account Azure, [creare un account Azure gratuito](https://azure.microsoft.com/free/) in pochi minuti.
* Mac o PC che esegue Windows o Ubuntu.
* Rete wireless per tooconnect Sparkfun ESP8266 cosa Dev per.
* Strumento di configurazione hello toodownload connessione Internet.
* [IDE Arduino](https://www.arduino.cc/en/main/software) versione 1.6.8 (o versione successiva), le versioni precedenti non funzioneranno con libreria AzureIoT hello.

Hello gli elementi seguenti sono facoltativi nel caso in cui non si dispone di un sensore. È anche possibile hello utilizzando i dati del sensore simulato.

* Un sensore di temperatura e umidità Adafruit DHT22.
* Una basetta sperimentale.
* Cavi ponticello M/M.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-hello-sensor-and-your-computer"></a>Connessione ESP8266 cosa Dev con sensore hello e il computer

### <a name="connect-a-dht22-temperature-and-humidity-sensor-tooesp8266-thing-dev"></a>Connettersi a un sensore di temperatura e umidità DHT22 tooESP8266 cosa Dev

Utilizzare hello breadboard e ponticelli cavi toomake hello connessione come indicato di seguito. Se non si dispone di un sensore, ignorare questa sezione in quanto è possibile usare i dati di sensori simulati.

![Riferimento per le connessioni](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

Per i codici PIN sensore, verrà utilizzato hello seguente collegamento:

| Inizio (sensore)           | Fine (scheda)           | Colore del cavo   |
| -----------------------  | ---------------------- | ------------: |
| VDD (Pin 27F)            | 3V (Pin 8A)           | Cavo rosso     |
| DATA (Pin 28F)           | GPIO 2 (Pin 9A)       | Cavo bianco    |
| GND (Pin 30F)            | GND (Pin 7J)          | Cavo nero   |


- Per altre informazioni, vedere: [installazione del sensore DHT22](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) e [specifiche di Sparkfun ESP8266 Thing Dev](https://www.sparkfun.com/products/13711)

Ora Sparkfun ESP8266 Thing Dev è connesso con un sensore funzionante.

![collegare DHT22 con ESP8266 Thing Dev](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-tooyour-computer"></a>Connettere computer tooyour Sparkfun ESP8266 cosa Dev

Utilizzare hello USB Micro tooType A USB cable tooconnect Sparkfun ESP8266 cosa Dev tooyour computer come indicato di seguito.

![connettere computer tooyour huzzah di sfumatura](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a>Aggiungere le autorizzazioni per la porta seriale: solo in Ubuntu

Se si utilizza Ubuntu, assicurarsi che un utente normale ha toooperate autorizzazioni hello in hello USB porta di Sparkfun ESP8266 cosa scopi di sviluppo autorizzazioni di porta seriale tooadd per un utente normale, seguire questi passaggi:

1. Eseguire hello seguenti comandi in un terminal:

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Viene visualizzato uno dei hello seguente output:

   * crw-rw---- 1 root uucp xxxxxxxx
   * crw-rw---- 1 root dialout xxxxxxxx

   Si noti nell'output di hello, `uucp` o `dialout` ovvero hello proprietario nome del gruppo di hello porta USB.

1. Aggiungi gruppo toohello hello eseguendo hello comando seguente:

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   `<group-owner-name>`è nome del proprietario del gruppo hello ottenuto nel passaggio precedente hello. `<username>` è il nome utente di Ubuntu.

1. Disconnettersi Ubuntu e ripetere l'accesso, per effetto di tootake modifica hello.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Raccogliere dati del sensore e inviarle tooyour IoT hub

In questa sezione si distribuisce e si esegue un'applicazione di esempio in Sparkfun ESP8266 Thing Dev. applicazione di esempio Hello lampeggia hello LED su Sparkfun ESP8266 cosa Dev e invia la temperatura hello e umidità raccolti da hello DHT22 sensore tooyour hub IoT.

### <a name="get-hello-sample-application-from-github"></a>Ottenere l'applicazione di esempio hello da GitHub

applicazione di esempio Hello è ospitata in GitHub. Clonare il repository di esempio hello che contiene l'applicazione di esempio hello da GitHub. repository di esempio hello tooclone, seguire questi passaggi:

1. Aprire un prompt dei comandi o una finestra del terminale.
1. Passare tooa cartella in cui si desidera toobe applicazione di esempio hello archiviati.
1. Eseguire hello comando seguente:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

Installare il pacchetto di hello per Sparkfun ESP8266 cosa Dev nell'IDE Arduino:

1. Aprire hello cartella dove si trova l'applicazione di esempio hello.
1. Aprire il file di app.ino hello nella cartella dell'applicazione hello Arduino IDE.

   ![Aprire l'applicazione di esempio hello in arduino ide](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. In hello Arduino IDE, fare clic su **File** > **preferenze**.
1. In hello **preferenze** finestra di dialogo fare clic su hello icona Avanti toohello **URL di gestione aggiuntivi lavagne** casella di testo.
1. Nella finestra popup hello immettere hello URL seguente e quindi fare clic su **OK**.

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![url del pacchetto nell'ide arduino tooa punto](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. In hello **preferenza** la finestra di dialogo, fare clic su **OK**.
1. Fare clic su **Strumenti** > **Bacheca** > **Boards Manager** (Gestione bacheche) e quindi cercare esp8266.
   Deve essere installato ESP8266 versione 2.2.0 o successiva.

   ![installazione del pacchetto esp8266 Hello](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. Fare clic su **Strumenti** > **Scheda** > **Sparkfun ESP8266 Thing Dev**.

### <a name="install-necessary-libraries"></a>Installare le librerie necessarie

1. In hello Arduino IDE, fare clic su **Sketch** > **libreria includono** > **Gestisci raccolte**.
1. Ricerca di hello seguente i nomi delle librerie uno alla volta. Per ogni libreria hello desiderati, fare clic su **installare**.
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a>Non si dispone di un sensore DHT22 reale?

applicazione di esempio Hello possibile simulare la temperatura e umidità dati nel caso in cui non si dispone di un sensore DHT22 reale. dati toouse simulate dell'applicazione di esempio hello di tooenable, seguire questi passaggi:

1. Aprire hello `config.h` file hello `app` cartella.
1. Individuare hello successiva riga di codice e modificare il valore di hello da `false` troppo`true`:
   ```c
   define SIMULATED_DATA true
   ```
   ![Configurare i dati simulati toouse dell'applicazione di esempio hello](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. Salvare con `Control-s`.

### <a name="deploy-hello-sample-application-toosparkfun-esp8266-thing-dev"></a>Distribuire tooSparkfun applicazione di esempio hello ESP8266 cosa Dev

1. In hello Arduino IDE, fare clic su **strumento** > **porta**, quindi fare clic su porta seriale hello per scopi di sviluppo cosa ESP8266 Sparkfun
1. Fare clic su **Sketch** > **caricare** toobuild e distribuire tooSparkfun applicazione di esempio hello ESP8266 cosa scopi di sviluppo

> [!Note]
> Se si utilizza macOS che è probabilmente possibile vedere hello seguendo i messaggi durante il caricamento. `warning: espcomm_sync failed`,`error: espcomm_open failed`. Aprire la finestra ternimal e fine toosolve azioni di sotto di questo problema.
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a>Immettere le credenziali

Dopo aver completato il caricamento di hello, seguire le credenziali tooenter passaggi hello:

1. In hello Arduino IDE, fare clic su **strumenti** > **monitoraggio seriale**.
1. Nella finestra di monitoraggio seriale hello, noti elenchi a discesa hello due su hello nell'angolo inferiore destro.
1. Selezionare **alcuna terminazione di riga** per l'elenco a discesa sinistra hello.
1. Selezionare **115200 baud** per l'elenco a discesa a destra hello.
1. Nella casella di input hello nella parte superiore di hello della finestra di monitoraggio seriale hello, immettere le seguenti informazioni se viene chiesto tooprovide hello, quindi fare clic su **inviare**.
   * Wi-Fi SSID
   * Password Wi-Fi
   * Stringa di connessione del dispositivo

> [!Note]
> informazioni sulle credenziali Hello viene archiviati in hello EEPROM di Sparkfun ESP8266 cosa scopi di sviluppo Se si fa clic su pulsante Reimposta hello in hello Lavagna Sparkfun ESP8266 cosa Dev, applicazione di esempio hello viene chiesto se si desiderano che le informazioni di hello tooerase. Immettere `Y` informazioni hello toohave cancellati e viene richiesto di informazioni di hello tooprovide nuovamente.

### <a name="verify-hello-sample-application-is-running-successfully"></a>Verificare l'applicazione di esempio hello venga eseguita correttamente

Se viene visualizzato seguito hello output della finestra di monitoraggio seriale hello e hello lampeggiante LED su Sparkfun ESP8266 cosa Dev, applicazione di esempio hello venga eseguita correttamente.

![Output finale nell'IDE di Arduino](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a>Passaggi successivi

Connesso a un hub IoT di tooyour Sparkfun ESP8266 cosa Dev e inviati hello acquisita l'hub IoT tooyour sensore dati completata. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
