---
title: aaaESP8266 toocloud - connettersi sfumatura HUZZAH ESP8266 tooAzure IoT Hub | Documenti Microsoft
description: Informazioni su come toosetup e connettersi Adafruit sfumatura HUZZAH ESP8266 tooAzure IoT Hub per tale piattaforma cloud di Azure di toosend dati toohello in questa esercitazione.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: c505aacf-89a8-40ed-a853-493b75bec524
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: xshi
ms.openlocfilehash: 44fd47232488948d21c7aa71bdd865397e41e63e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-tooazure-iot-hub-in-hello-cloud"></a>Connettersi Adafruit sfumatura HUZZAH ESP8266 tooAzure IoT Hub nel cloud hello

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Connessione tra DHT22, Feather HUZZAH ESP8266 e l'hub IoT](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a>Operazioni da fare


Connettersi Adafruit sfumatura HUZZAH ESP8266 tooan IoT hub creato. Quindi eseguire un'applicazione di esempio in ESP8266 toocollect hello temperatura e umidità dati da un sensore DHT22. Infine, si invia l'hub IoT hello sensore dati tooyour.

> [!NOTE]
> Se si utilizzano altre schede ESP8266, è comunque possibile eseguire questi passaggi tooconnect è tooyour IoT hub. A seconda della Lavagna hello ESP8266 in uso, potrebbe essere necessario hello tooreconfigure `LED_PIN`. Ad esempio, se si utilizza ESP8266 da AI Thinker, è possibile modificarlo da `0` troppo`2`. Se non si ha ancora un kit, Scaricare il pacchetto hello [sito Web di Azure](http://azure.com/iotstarterkits).




## <a name="what-you-learn"></a>Contenuto dell'esercitazione

* Come toocreate un hub IoT e registrare un dispositivo per sfumatura HUZZAH ESP8266
* Come tooconnect ESP8266 HUZZAH sfumatura con sensore hello e il computer
* Come dati del sensore toocollect mediante l'esecuzione di un'applicazione di esempio su ESP8266 HUZZAH sfumatura
* Come toosend hello hub IoT tooyour di sensore dati

## <a name="what-you-need"></a>Elementi necessari

![Parti necessarie per l'esercitazione hello](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete questa operazione, è necessario hello dallo Starter Kit di sfumatura HUZZAH ESP8266 le seguenti parti:

* Hello sfumatura HUZZAH ESP8266 Lavagna
* Un cavo USB A di tooType Micro USB

È inoltre necessario hello seguenti operazioni per l'ambiente di sviluppo:

* Una sottoscrizione di Azure attiva. Se non si ha un account Azure, [creare un account Azure gratuito](https://azure.microsoft.com/free/) in pochi minuti.
* Mac o PC che esegue Windows o Ubuntu.
* Rete wireless per sfumatura HUZZAH ESP8266 tooconnect per.
* Strumento di configurazione hello toodownload connessione Internet.
* [IDE Arduino](https://www.arduino.cc/en/main/software) 1.6.8 o versione successiva. Le versioni precedenti non funzionano con libreria AzureIoT hello.

Hello gli elementi seguenti sono facoltativi nel caso in cui non si dispone di un sensore. È anche possibile hello utilizzando i dati del sensore simulato.

* Sensore di temperatura e umidità Adafruit DHT22
* Basetta sperimentale
* Cavi ponticello M/M


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-hello-sensor-and-your-computer"></a>Connessione ESP8266 HUZZAH sfumatura con sensore hello e il computer
In questa sezione è connettersi Lavagna tooyour sensori di hello. Quindi si collega il computer tooyour dispositivo per l'ulteriore utilizzo.
### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-huzzah-esp8266"></a>Connettersi a un DHT22 temperatura e umidità sensore tooFeather HUZZAH ESP8266

Utilizzare hello breadboard e ponticelli cavi toomake hello connessione come indicato di seguito. Se non si dispone di un sensore, ignorare questa sezione in quanto è possibile usare i dati di sensori simulati.

![Riferimento per le connessioni](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


Per i codici PIN sensore, utilizzare hello seguente collegamento:


| Inizio (sensore)           | Fine (scheda)           | Colore del cavo   |
| -----------------------  | ---------------------- | ------------: |
| VDD (Pin 31F)            | 3V (Pin 58H)           | Cavo rosso     |
| DATI (Pin 32F)           | GPIO 2 (Pin 46A)       | Cavo blu    |
| GND (Pin 34F)            | GND (PIn 56I)          | Cavo nero   |

Per altre informazioni, vedere la [configurazione del sensore Adafruit DHT22](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) e la [piedinatura di Adafruit Feather HUZZAH Esp8266](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).



Ora Feather Huzzah ESP8266 è connesso con un sensore funzionante.

![Connettere DHT22 a Feather HUZZAH](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-tooyour-computer"></a>Connettere computer tooyour ESP8266 HUZZAH sfumatura

Come illustrato nella figura, utilizzare hello USB Micro tooType A USB cable tooconnect sfumatura HUZZAH ESP8266 tooyour computer.

![Connettere computer tooyour Huzzah sfumatura](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a>Aggiungere le autorizzazioni per la porta seriale (solo Ubuntu)


Se si utilizza Ubuntu, verificare di che aver toooperate autorizzazioni hello in hello USB porta della sfumatura HUZZAH ESP8266. le autorizzazioni della porta seriale tooadd, seguire questi passaggi:


1. Eseguire hello seguenti comandi in un terminal:

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Viene visualizzato uno dei hello seguente output:

   * crw-rw---- 1 root uucp xxxxxxxx
   * crw-rw---- 1 root dialout xxxxxxxx

   Nell'output di hello, si noti che `uucp` o `dialout` è nome del proprietario del gruppo hello di hello porta USB.

1. Aggiungi gruppo toohello hello eseguendo hello comando seguente:

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   `<group-owner-name>`è nome del proprietario del gruppo hello ottenuto nel passaggio precedente hello. `<username>` è il nome utente di Ubuntu.

1. Disconnettersi da Ubuntu e quindi accedere di nuovo per hello tooappear di modifica.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Raccogliere dati del sensore e inviarle tooyour IoT hub

In questa sezione si distribuisce un'applicazione di esempio in Feather HUZZAH ESP8266. applicazione di esempio Hello lampeggia hello LED su ESP8266 HUZZAH sfumatura e invia la temperatura hello e umidità raccolti da hello DHT22 sensore tooyour hub IoT.

### <a name="get-hello-sample-application-from-github"></a>Ottenere l'applicazione di esempio hello da GitHub

applicazione di esempio Hello è ospitata in GitHub. Clonare il repository di esempio hello che contiene l'applicazione di esempio hello da GitHub. repository di esempio hello tooclone, seguire questi passaggi:

1. Aprire un prompt dei comandi o una finestra del terminale.
1. Passare tooa cartella in cui si desidera toobe applicazione di esempio hello archiviati.
1. Eseguire hello comando seguente:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

Installare il pacchetto di hello per sfumatura HUZZAH ESP8266 in hello Arduino IDE:

1. Aprire hello cartella dove si trova l'applicazione di esempio hello.
1. Aprire il file di app.ino hello nella cartella dell'applicazione hello in hello Arduino IDE.

   ![Aprire l'applicazione di esempio hello in Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. In hello Arduino IDE, fare clic su **File** > **preferenze**.
1. In hello **preferenze** finestra di dialogo fare clic su hello icona Avanti toohello **URL di gestione aggiuntivi lavagne** casella.
1. Nella finestra popup hello immettere hello URL seguente e quindi fare clic su **OK**.

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Url del pacchetto nell'IDE Arduino tooa punto](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. In hello **preferenza** la finestra di dialogo, fare clic su **OK**.
1. Fare clic su **Strumenti** > **Bacheca** > **Boards Manager** (Gestione bacheche) e quindi cercare esp8266.

   Boards Manager indica che è installata ESP8266 con una versione 2.2.0 o successiva.

   ![installazione del pacchetto esp8266 Hello](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. Fare clic su **Strumenti** > **Bacheca** > **Adafruit HUZZAH ESP8266**.

### <a name="install-necessary-libraries"></a>Installare le librerie necessarie

1. In hello Arduino IDE, fare clic su **Sketch** > **libreria includono** > **Gestisci raccolte**.
1. Ricerca di hello seguente i nomi delle librerie uno alla volta. Per ogni libreria trovata fare clic su **Install** (Installa).
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a>Non si dispone di un sensore DHT22 reale?

applicazione di esempio Hello possibile simulare la temperatura e umidità dati nel caso in cui non si dispone di un sensore DHT22 reale. tooset dei dati di toouse simulate dell'applicazione di esempio hello, seguire questi passaggi:

1. Aprire hello `config.h` file hello `app` cartella.
1. Individuare hello successiva riga di codice e modificare il valore di hello da `false` troppo`true`:
   ```c
   define SIMULATED_DATA true
   ```
   ![Configurare i dati simulati toouse dell'applicazione di esempio hello](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. Salvare file con estensione hello `Control-s`.

### <a name="deploy-hello-sample-application-toofeather-huzzah-esp8266"></a>Distribuire tooFeather applicazione di esempio hello HUZZAH ESP8266

1. In hello Arduino IDE, fare clic su **strumento** > **porta**, quindi fare clic su porta seriale hello per sfumatura HUZZAH ESP8266.
1. Fare clic su **Sketch** > **caricare** toobuild e distribuire tooFeather applicazione di esempio hello HUZZAH ESP8266.

### <a name="enter-your-credentials"></a>Immettere le credenziali

Dopo aver completato il caricamento di hello, seguire questi passaggi tooenter le credenziali:

1. In hello Arduino IDE, fare clic su **strumenti** > **monitoraggio seriale**.
1. Nella finestra di monitoraggio seriale hello, noti elenchi a discesa hello due nell'angolo inferiore destro hello.
1. Selezionare **alcuna terminazione di riga** per l'elenco a discesa sinistra hello.
1. Selezionare **115200 baud** per l'elenco a discesa a destra hello.
1. Nella casella di input hello nella parte superiore di hello della finestra di monitoraggio seriale hello, immettere le seguenti informazioni se viene chiesto tooprovide hello, quindi fare clic su **inviare**.
   * Wi-Fi SSID
   * Password Wi-Fi
   * Stringa di connessione del dispositivo

> [!Note]
> informazioni sulle credenziali Hello viene archiviati in hello EEPROM di sfumatura HUZZAH ESP8266. Se si fa clic su pulsante Reimposta hello in hello Lavagna ESP8266 HUZZAH sfumatura, applicazione di esempio hello chiede se si desiderano informazioni hello tooerase. Immettere `Y` informazioni hello toohave cancellate. Verrà chiesto informazioni hello tooprovide una seconda volta.

### <a name="verify-hello-sample-application-is-running-successfully"></a>Verificare l'applicazione di esempio hello venga eseguita correttamente

Se viene visualizzato seguito hello output della finestra di monitoraggio seriale hello e hello lampeggiante LED su ESP8266 HUZZAH sfumatura, applicazione di esempio hello venga eseguita correttamente.

![Output finale nell'IDE Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a>Passaggi successivi

Aver connesso un hub IoT di sfumatura HUZZAH ESP8266 tooyour e inviato hello acquisito sensore dati tooyour IoT hub. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

