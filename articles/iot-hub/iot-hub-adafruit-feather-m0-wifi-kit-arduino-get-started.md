---
title: 'M0 toocloud: la connessione Wi-Fi M0 sfumatura tooAzure IoT Hub | Documenti Microsoft'
description: Informazioni su come tooset backup e la connessione Wi-Fi M0 di sfumatura Adafruit tooAzure la piattaforma cloud di Azure IoT Hub toosend dati toohello in questa esercitazione.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 51befcdb-332b-416f-a6a1-8aabdb67f283
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/16/2017
ms.author: xshi
ms.openlocfilehash: 6aabeb961a50ba5d3934f77eb1ccda4af1bf64c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-m0-wifi-tooazure-iot-hub-in-hello-cloud"></a>La connessione Wi-Fi M0 di sfumatura Adafruit tooAzure IoT Hub nel cloud hello
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Connessione tra BME280, Feather M0 Wi-Fi e l'hub IoT](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

In questa esercitazione, è necessario innanzitutto hello nozioni fondamentali sulle operazioni con la scheda Arduino di apprendimento. Si apprenderà quindi la modalità di connessione cloud toohello dispositivi utilizzando tooseamlessly [IoT Hub Azure](iot-hub-what-is-iot-hub.md).

## <a name="what-you-do"></a>Operazioni da fare

La connessione Wi-Fi M0 di sfumatura Adafruit tooan IoT hub creato. Quindi eseguire un'applicazione di esempio in Wi-Fi M0 toocollect hello temperatura e umidità dati da un BME280. Infine, si invia l'hub IoT hello sensore dati tooyour.


## <a name="what-you-learn"></a>Contenuto dell'esercitazione

* Come toocreate un hub IoT e registrare un dispositivo per Wi-Fi M0 sfumatura
* Come tooconnect Wi-Fi M0 sfumatura con sensore hello e il computer
* Come dati del sensore toocollect mediante l'esecuzione di un'applicazione di esempio su Wi-Fi M0 sfumatura
* Come toosend hello hub IoT tooyour di sensore dati

## <a name="what-you-need"></a>Elementi necessari

![Parti necessarie per l'esercitazione hello](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete questa operazione, è necessario hello dallo Starter Kit di sfumatura M0 Wi-Fi le seguenti parti:

* Hello Wi-Fi M0 sfumatura Lavagna
* Un cavo USB A di tooType Micro USB

È inoltre necessario hello seguenti operazioni per l'ambiente di sviluppo:

* Una sottoscrizione di Azure attiva. Se non si ha un account di Azure, [creare un account di Azure gratuito](https://azure.microsoft.com/free/) in pochi minuti.
* Un Mac o un PC che esegue Windows o Ubuntu.
* Una rete wireless per Wi-Fi M0 sfumatura tooconnect per.
* Uno strumento di configurazione hello Internet connessione toodownload.
* [IDE Arduino](https://www.arduino.cc/en/main/software) 1.6.8 o versione successiva. Le versioni precedenti non funzionano con libreria di Azure IoT Hub hello.

Se non si dispone di un sensore, hello seguenti elementi è facoltativo. È anche possibile hello utilizzando i dati del sensore simulato:

* Un sensore di temperatura e umidità BME280
* Basetta sperimentale
* Cavi ponticello M/M

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-hello-sensor-and-your-computer"></a>La connessione Wi-Fi M0 sfumatura con sensore hello e il computer
In questa sezione è connettersi Lavagna tooyour sensori di hello. Quindi si collega il computer tooyour dispositivo per l'ulteriore utilizzo.

### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-m0-wifi"></a>Connettersi a un DHT22 temperatura e umidità sensore tooFeather Wi-Fi M0

Utilizzare hello breadboard e ponticelli cavi toomake hello connessione. Se non si dispone di un sensore, ignorare questa sezione in quanto è possibile usare i dati di sensori simulati.

![Riferimento per le connessioni](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


Per i codici PIN sensore, utilizzare hello seguente collegamento:


| Inizio (sensore)           | Fine (scheda)            | Colore del cavo   |
| -----------------------  | ---------------------- | ------------: |
| VDD (Pin 27A)            | 3 V (Pin 3A)            | Cavo rosso     |
| GND (Pin 29A)            | GND (Pin 6A)           | Cavo nero   |
| SCK (Pin 30A)            | SCK (Pin 12A)          | Cavo giallo  |
| SDO (Pin 31A)            | MI (Pin 14A)           | Cavo bianco   |
| SDI (Pin 32A)            | M0 (Pin 13A)           | Cavo blu    |
| CS (Pin 33A)             | GPIO 5 (Pin 15J)       | Cavo arancione  |

Per altre informazioni, vedere [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) (Informazioni sul sensore di temperatura + pressione barometrica + umidità Adafruit BME280) e la [piedinatura di Adafruit Feather M0 Wi-Fi](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).



Ora Feather M0 Wi-Fi è connesso con un sensore funzionante.

![Connettere DHT22 a Feather HUZZAH](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-tooyour-computer"></a>La connessione Wi-Fi M0 sfumatura tooyour computer

Utilizzare hello USB Micro tooType A USB cable tooconnect Wi-Fi M0 sfumatura tooyour computer, come illustrato:

![Connettere computer tooyour Huzzah sfumatura](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a>Aggiungere le autorizzazioni per la porta seriale (solo Ubuntu)

Se si utilizza Ubuntu, verificare di che aver toooperate autorizzazioni hello in hello USB porta della sfumatura M0 Wi-Fi. le autorizzazioni della porta seriale tooadd, seguire questi passaggi:


1. Un terminale, eseguire hello seguenti comandi:

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Viene visualizzato uno dei hello seguente output:

   * crw-rw---- 1 root uucp xxxxxxxx
   * crw-rw---- 1 root dialout xxxxxxxx

   Nell'output di hello, si noti che `uucp` o `dialout` è nome del proprietario del gruppo hello di hello porta USB.

2. tooadd hello toohello gruppo di utenti, eseguire hello comando seguente:

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   Ottenuto nel passaggio precedente hello, nome del proprietario del gruppo hello `<group-owner-name>`. `<username>` il nome utente di Ubuntu.

3. Per tooappear modifica hello, disconnettersi da Ubuntu e quindi accedere di nuovo.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Raccogliere dati del sensore e inviarle tooyour IoT hub

In questa sezione si distribuisce e si esegue un'applicazione di esempio in Feather M0 Wi-Fi. applicazione di esempio Hello rende hello blink LED sul Wi-Fi M0 sfumatura. Invia quindi temperatura hello e umidità raccolti da hello BME280 sensore tooyour hub IoT.

### <a name="get-hello-sample-application-from-github-and-prepare-hello-arduino-ide"></a>Ottenere l'applicazione di esempio hello da GitHub e preparare hello Arduino IDE

applicazione di esempio Hello è ospitata in GitHub. Clonare il repository di esempio hello che contiene l'applicazione di esempio hello da GitHub. repository di esempio hello tooclone, seguire questi passaggi:

1. Aprire un prompt dei comandi o una finestra del terminale.

2. Passare tooa cartella in cui si desidera toobe applicazione di esempio hello archiviati.
3. Eseguire hello comando seguente:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-hello-package-for-feather-m0-wifi-in-hello-arduino-ide"></a>Installare il pacchetto di hello per Wi-Fi M0 sfumatura in hello Arduino IDE

1. Aprire hello cartella dove si trova l'applicazione di esempio hello.

2. Aprire il file di app.ino hello nella cartella dell'applicazione hello in hello Arduino IDE.

   ![Aprire l'applicazione di esempio hello in Arduino IDE](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. Fare clic su **File** > **preferenze** (Windows/Linux) o **Arduino** > **preferenze** (Mac) e copiare e Incolla collegamento hello sotto in hello **URL di gestione aggiuntivi lavagne** opzione hello preferenze Arduino IDE.
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. Fare clic su **strumenti** > **Lavagna** > **Manager lavagne**e quindi installare hello `Arduino SAMD Boards` versione `1.6.2` o versione successiva. 

1. Quindi nella stessa finestra hello, installare `Adafruit SAMD Boards` definizioni del file tooadd hello Lavagna del pacchetto.

   ![installazione del pacchetto esp8266 Hello](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. Fare clic su **Strumenti** > **Schede** > **Adafruit M0 Wi-Fi**.

5. Installare i driver (solo per Windows). Quando si collega Wi-Fi M0 sfumatura, potrebbe essere necessario tooinstall un driver. Fare clic su [hello collegamento per il download nella pagina Web hello](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) programma di installazione driver toodownload hello. Seguire i driver hello tooinstall passaggi hello desiderato.

### <a name="install-necessary-libraries"></a>Installare le librerie necessarie

1. In hello Arduino IDE, fare clic su **Sketch** > **libreria includono** > **Gestisci raccolte**.

2. Ricerca di hello seguente i nomi delle librerie uno alla volta. Per ogni libreria trovata fare clic su **Install** (Installa):

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. Installare manualmente `Adafruit_WINC1500`. Andare troppo[il sito Web](https://github.com/adafruit/Adafruit_WINC1500) e fare clic su **Clone o download** > **ZIP di Download**. L'IDE Arduino, andare troppo**Sketch** > **libreria includono** > **aggiungere ZIP libreria** e aggiungere i file zip hello.

### <a name="use-hello-sample-application-if-you-dont-have-a-real-bme280-sensor"></a>Utilizzare l'applicazione di esempio hello se non si dispone di un sensore BME280 reale

Se non si dispone di un sensore BME280 reale, l'applicazione di esempio hello possibile simulare la temperatura e umidità dati. tooset dei dati di toouse simulate dell'applicazione di esempio hello, seguire questi passaggi:

1. Aprire hello `config.h` file hello `app` cartella.

2. Individuare hello successiva riga di codice e modificare il valore di hello da `false` troppo`true`:

   ```c
   define SIMULATED_DATA true
   ```
   ![Configurare i dati simulati toouse dell'applicazione di esempio hello](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. Salvare file con estensione hello `Control-s`.

### <a name="deploy-hello-sample-application-toofeather-m0-wifi"></a>Distribuire tooFeather applicazione di esempio hello Wi-Fi M0

1. In hello Arduino IDE, fare clic su **strumento** > **porta**, quindi fare clic su porta seriale hello per Wi-Fi M0 sfumatura.

2. Fare clic su **Sketch** > **caricare** toobuild e distribuire tooFeather applicazione di esempio hello Wi-Fi M0.

### <a name="enter-your-credentials"></a>Immettere le credenziali

Dopo aver completato il caricamento di hello, seguire questi passaggi tooenter le credenziali:

1. In hello Arduino IDE, fare clic su **strumenti** > **monitoraggio seriale**.

2. Nell'angolo inferiore destro hello della finestra di monitoraggio seriale hello selezionare **alcuna terminazione di riga** nell'elenco a discesa hello hello sinistra.
3. Selezionare **115200 baud** nell'elenco a discesa hello hello destra.
4. Nella casella di input hello nella parte superiore di hello, immettere le seguenti informazioni se si è hello frequenti tooprovide e fare clic su **inviare**:

   * Wi-Fi SSID
   * Password Wi-Fi
   * Stringa di connessione del dispositivo

> [!Note]
> informazioni sulle credenziali Hello viene archiviati in hello EEPROM di sfumatura M0 Wi-Fi. Se si fa clic su pulsante Reimposta hello in hello Lavagna Wi-Fi M0 sfumatura, applicazione di esempio hello chiede se si desiderano informazioni hello tooerase. Immettere `Y` informazioni hello tooerase. Verrà chiesto informazioni hello tooprovide una seconda volta.

### <a name="verify-that-hello-sample-application-is-running-successfully"></a>Verificare che l'applicazione di esempio hello venga eseguita correttamente

Se viene visualizzato seguito hello output della finestra di monitoraggio seriale hello e hello lampeggiante LED su Wi-Fi M0 sfumatura, applicazione di esempio hello venga eseguita correttamente:

![Output finale nell'IDE Arduino](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a>Passaggi successivi

Connessione Wi-Fi M0 sfumatura tooyour IoT hub e inviati hello acquisita l'hub IoT tooyour sensore dati completata. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

