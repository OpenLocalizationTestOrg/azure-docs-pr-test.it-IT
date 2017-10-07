---
title: aaaIoT Kit toocloud - tooAzure connettersi AZ3166 Kit di IoT IoT Hub | Documenti Microsoft
description: Informazioni su come toosetup e connettersi tooAzure AZ3166 Kit IoT IoT Hub per tale piattaforma cloud di Azure di toosend dati toohello in questa esercitazione.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: xshi
ms.openlocfilehash: fd36abaed1fd9f73028b84312bca9e900fb9c004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-iot-devkit-az3166-tooazure-iot-hub-in-hello-cloud"></a>Connettersi tooAzure AZ3166 Kit IoT IoT Hub nel cloud hello

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Hello [MXChip IoT Kit](https://microsoft.github.io/azure-iot-developer-kit/) può essere utilizzato toodevelop e prototipo soluzioni Internet delle cose (IoT) sfruttando i servizi di Microsoft Azure. Include una scheda compatibile Arduino con periferiche avanzate e sensori, un pacchetto della scheda open source e un aumento delle dimensioni del [catalogo progetti](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).

## <a name="what-you-do"></a>Operazioni da fare
Connettersi [Kit](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IoT hub di creare, dati di temperatura e umidità hello raccogliere da sensori e inviare l'hub di tooIoT dati hello.

Non hai ancora DevKit? Ricevine uno nuovo [qui](https://aka.ms/iot-devkit-purchase).

## <a name="what-you-learn"></a>Contenuto dell'esercitazione

* La modalità tooconnect IoT DevKit tooWireless accesso scegliere e preparare l'ambiente di sviluppo.
* Come toocreate un hub IoT e registrare un dispositivo per MXChip IoT Kit.
* Come dati del sensore toocollect mediante l'esecuzione di un'applicazione di esempio su MXChip IoT Kit.
* Come toosend hello hub IoT tooyour di dati del sensore.

## <a name="what-you-need"></a>Elementi necessari

* Una scheda DevKit di IoT MXChip con un cavo USB micro. [Ottienila adesso](https://aka.ms/iot-devkit-purchase)
* Un computer che esegue Windows 10 o macOS 10.10+
* Una sottoscrizione di Azure attiva
  * Attivare una [versione di prova gratuita di 30 giorni dell'account di Microsoft Azure](https://azureinfo.microsoft.com/us-freetrial.html)

## <a name="prepare-your-hardware"></a>Preparare l'hardware

Collegare il computer di tooyour hello hardware.

### <a name="hardware-you-need"></a>Hardware necessario

* Scheda DevKit
* Micro cavo USB

![getting-started-hardware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-tooyour-computer"></a>Connettere computer tooyour Kit

1. La connessione USB fine tooyour PC
2. La connessione USB Micro fine toohello Kit
3. Hello verde LED Avanti toopower Conferma connessione

![getting-started-connect](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a>Configurare il WiFi

I progetti IoT si basano sulla connettività Internet. Utilizzare hello seguendo le istruzioni tooconfigure hello Kit tooconnect tooWiFi.

### <a name="enter-ap-mode"></a>Passare alla modalità AP

Tenere premuto il pulsante B, quindi si reimposta hello push e la versione, quindi il tasto versione B. Il kit passerà alla modalità punto di accesso per la configurazione Wi-Fi. schermata Ciao visualizzerà hello servizio impostare Identifier(SSID) di hello Kit, così come indirizzo IP del portale di hello configurazione:

![getting-started-wifi-ap](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-toodevkit-ap"></a>Asia Pacifico tooDevKit connettersi

A questo punto, usare un altro Wi-Fi abilitato dispositivi (PC o telefono cellulare) tooconnect toohello DevKit SSID (evidenziato nella schermata di hello precedente), lasciare vuota la password hello.

![getting-started-ssid](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a>Configurare il WiFi per DevKit

Indirizzo IP hello aprire visualizzato sullo schermo Kit hello sul proprio PC o un browser di telefono cellulare, selezionare hello Wi-Fi rete hello Kit tooconnect per, quindi digitare la password di hello. Fare clic su **Connetti** toocomplete:

![getting-started-wifi-portal](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

Al termine della connessione di hello, hello Kit verrà riavviato in pochi secondi. Se ha avuto esito positivo, verrà visualizzato hello Wi-Fi nome e indirizzo IP nella schermata di hello:

![getting-started-wifi-ip](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
l'indirizzo IP Hello foto hello potrebbe non corrispondere hello IP effettivo assegnato e visualizzati sullo schermo Kit hello. Questo è normale come Wi-Fi utilizza DHCP toodynamically assegnare indirizzi IP.

Dopo la configurazione Wi-Fi, le credenziali verranno rese persistenti nel dispositivo hello per tale connessione, anche se scollegato. Ad esempio, se configurato hello Kit per Wi-Fi in casa e ha quindi office toohello Kit di hello, occorrerà modalità tooreconfigure PA (a partire dal passaggio **immettere modalità PA**) tooconnect hello Kit tooyour office Wi-Fi. 

## <a name="start-using-devkit"></a>Iniziare a usare DevKit

applicazione predefinita Hello in esecuzione nel Kit verrà controllare hello la versione più recente del firmware hello e visualizzare alcuni dati di diagnostica sensore automaticamente.

### <a name="upgrade-toohello-latest-firmware"></a>Aggiornare il firmware più recente di toohello

Verrà richiesto nella schermata di hello che entrambi hello versione più recente del firmware se è presente un aggiornamento Necessito. Seguire [aggiornare il firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) tooupgrade della Guida è.

![getting-started-firmware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
Si tratta di un impegno monouso, dopo aver iniziato lo sviluppo di hello Kit e caricare l'app, sarà necessario firmware più recente di hello forniti con l'app.

### <a name="test-various-sensors"></a>Testare i diversi sensori

Premere sensori tootest pulsante B, continuare premendo e rilasciando toocycle pulsante hello B tramite ogni sensore.

![getting-started-sensors](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a>Preparare l'ambiente di sviluppo

Ora è ora tooset hello ambiente di sviluppo: strumenti e i pacchetti per toobuild IoT applicazioni sorprendenti. È possibile scegliere una versione Windows o macOS tooyour del sistema operativo di base.


### <a name="windows"></a>Windows

Invita i clienti si toouse hello installazione pacchetto tooprepare hello ambiente di sviluppo. Se si verificano problemi, è possibile seguire hello [passaggi manuali](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget eseguito.

#### <a name="download-latest-package"></a>Scaricare il pacchetto più recente

Hello `.zip` file scaricato contiene tutti i pacchetti necessari per lo sviluppo di Kit e strumenti necessari.

> [!div class="button"]
[Scaricare](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> Hello `.zip` hello siano contenuti file strumenti e i pacchetti. Se si dispone già di alcuni componenti installati, script hello rileverà e ignorarli.
> * Node.js e Yarn: Runtime per lo script di installazione di hello e attività automatizzate
> * [Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -multipiattaforma esperienza della riga di comando per la gestione delle risorse di Azure, hello MSI contiene Python e pip dipendenti.
> * [Visual Studio Code](https://code.visualstudio.com/): editor del codice semplice per lo sviluppo di DevKit
> * [Estensione di Visual Studio Code per Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): abilita lo sviluppo di Arduino in Visual Studio Code
> * [IDE Arduino](https://www.arduino.cc/en/Main/Software): estensione hello per Arduino si basa su questo strumento
> * Pacchetto Kit Lavagna: Strumento catene, librerie e progetti per hello Kit
> * Utilità ST-Link: utilità essenziali e driver

#### <a name="run-installation-script"></a>Eseguire lo script di installazione

In Esplora File individuare hello `.zip` e decomprimerlo, trovare `install.cmd`del mouse e scegliere **"Esegui come amministratore"** toostart.

![getting-started-run-admin](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

Durante l'installazione, verrà visualizzato lo stato di avanzamento hello di ogni strumento o un pacchetto.

![getting-started-install](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-tooinstall-drivers"></a>Verificare i driver tooinstall

Hello Visual Studio Code per l'estensione Arduino si basa su hello Arduino IDE. Se si tratta di hello prima volta che si sta installando hello Arduino IDE, sarà richiesta tooinstall rilevanti driver:

![getting-started-driver](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

Occorrere installazione toofinish circa 10 minuti a seconda della velocità di Internet. Al termine dell'installazione di hello, dovrebbe essere codice e Visual Studio IDE Arduino collegamenti sul desktop.

> [!NOTE] 
In alcuni casi, quando si avvia Visual Studio Code, verrà visualizzato un errore che non è possibile trovare nell'IDE di Arduino o in un pacchetto di scheda correlati. toosolve chiudere Visual Studio Code, avviare una volta Arduino IDE e Visual Studio Code deve individuare il percorso di IDE Arduino correttamente.


### <a name="macos-preview"></a>macOS (anteprima)

Seguire questi ambiente di sviluppo tooprepare passaggi macOS.

#### <a name="install-azure-cli-20"></a>Installare l'interfaccia della riga di comando di Azure 2.0

Seguire hello [guida ufficiale](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall CLI di Azure 2.0:

Installare l'interfaccia della riga di comando di Azure 2.0 con il solo comando `curl`:

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

E riavviare la shell dei comandi per effetto di tootake modifiche:

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a>Installare l'IDE di Arduino

estensione di Visual Studio codice Arduino Hello si basa su hello Arduino IDE. Scaricare e installare hello [Arduino IDE per macOS](https://www.arduino.cc/en/Main/Software).

#### <a name="install-visual-studio-code"></a>Installare Visual Studio Code

Scaricar e installare [Visual Studio Code per macOS](https://code.visualstudio.com/). Questo sarà lo strumento di sviluppo primario hello per la creazione di applicazioni DevKit IoT.

####  <a name="download-latest-package"></a>Scaricare il pacchetto più recente

1. Installare Node.js. È possibile usare Gestione pacchetti macOS diffusi [Homebrew](https://brew.sh/) o [pre-compilato installazione](https://nodejs.org/en/download/) tooinstall è.

2. Scaricare il file `.zip` che contiene gli script delle attività necessari per lo sviluppo di DevKit in Visual Studio Code.

   > [!div class="button"]
   [Scaricare](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   Individuare hello `.zip` ed estrarre i file. Avviare quindi **Terminal** app e l'esecuzione hello tooconfigure i comandi seguenti:

   Spostare estratti tooyour macOS utente una cartella:
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   Installare i pacchetti `npm`:
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a>Installare l'estensione di Visual Studio Code per Arduino

Codice di Visual Studio consente le estensioni di Marketplace tooinstall direttamente nello strumento di hello, semplicemente fare clic sull'icona di estensioni hello nel riquadro di hello menu a sinistra e quindi cercare `Arduino` tooinstall:

![installation-extensions](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a>Installare il pacchetto della scheda DevKit

Sarà necessario Lavagna Kit di hello tooadd utilizzando hello Manager scheda in Visual Studio Code.

1. Utilizzare `Cmd+Shift+P` tooinvoke comando tavolozza e digitare **Arduino** quindi individuare e selezionare **Arduino: scheda Gestione**.

2. Fare clic su **'URL aggiuntivi'** in basso a destra hello.
   ![installation-additional-urls](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)

3. In hello `settings.json` file, aggiungere una riga in fondo hello `USER SETTINGS` riquadro e salvare.
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![installation-settings-json](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. Ora cercare 'az3166' hello Lavagna Manager e installare la versione più recente di hello.
   ![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)

È ora tutti i pacchetti installati per macOS e gli strumenti necessari hello.


## <a name="open-project-folder"></a>Aprire la cartella del progetto

### <a name="launch-vs-code"></a>Avviare Visual Studio Code

Assicurarsi che DevKit non sia connesso. Avviare innanzitutto il codice di Visual Studio e connettere hello Kit tooyour computer. Visual Studio Code lo troverà automaticamente e mostrerà una pagina di introduzione:

![mini-solution-vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
In alcuni casi, quando si avvia Visual Studio Code, verrà visualizzato un errore che non è possibile trovare nell'IDE di Arduino o in un pacchetto di scheda correlati. toosolve chiudere Visual Studio Code, avviare nuovamente Arduino IDE e Visual Studio Code deve individuare il percorso di IDE Arduino correttamente.

### <a name="open-arduino-examples-folder"></a>Aprire la cartella degli esempi di Arduino

Opzione troppo**'Arduino esempi'** scheda, passare troppo`Examples for MXCHIP AZ3166 > AzureIoT` e fare clic su `GetStarted`.

![mini-solution-examples](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

Se si è verificata riquadro hello tooclose tooreload, utilizzare `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tavolozza e il tipo di comando tooinvoke **Arduino** toofind e selezionare **Arduino: esempi**.

## <a name="provision-azure-services"></a>Eseguire il provisioning dei servizi di Azure

Nella finestra di soluzione hello, eseguire le attività `Ctrl+P` (macOS: `Cmd+P`) digitando 'task il provisioning di cloud':

In hello Visual Studio Code terminale, che una riga di comando interattiva guiderà hello provisioning necessari servizi di Azure:

![mini-solution-cloud-provision](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a>Compilare e caricare la definizione di Arduino

### <a name="install-required-library"></a>Installare la raccolta richiesta

1. Premere `F1` o `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tavolozza e il tipo di comando tooinvoke **Arduino** quindi individuare e selezionare **Arduino: Gestione librerie**.

2. Cercare la raccolta `ArduinoJson` e fare clic su **Install** (Installa)

### <a name="build-and-upload-hello-device-code"></a>Creare e caricare codice dispositivo hello

Utilizzare `Ctrl+P` (macOS: `Cmd+P`) toorun 'attività di dispositivo upload'. Hello terminal richiederà si tooenter modalità di configurazione. toodo in tal caso, tenere premuto un pulsante, quindi push e la versione di hello pulsante Reimposta. schermata Ciao visualizzerà 'Configuration'. Si tratta di stringa di connessione hello tooset che recupera dal passaggio di 'cloud-provisioning di attività'.

Quindi è possibile avviare la verifica e caricamento sketch Arduino hello:

![mini-solution-device-upload](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

Hello Kit verrà riavviato e avviarne l'esecuzione di codice hello.

## <a name="test-hello-project"></a>Progetto di test hello

Nel codice di Visual Studio, fare clic sul hello power plug sulla barra tooopen hello seriale di monitoraggio di stato hello.

applicazione di esempio Hello è in esecuzione correttamente quando viene visualizzato hello seguenti risultati:

* Hello Visualizza monitoraggio seriale hello stesse informazioni di contenuto di hello hello schermata seguente.
* LED sul kit IoT MXChip Hello è lampeggiante.

![Output finale in Visual Studio Code](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a>Problemi e commenti

È possibile trovare [FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) se si verificano problemi o raggiungere toous dai canali hello riportato di seguito.

## <a name="next-steps"></a>Passaggi successivi

Si è connessi un tooyour MXChip Kit di IoT IoT Hub e hello inviato acquisita l'hub IoT sensore dati tooyour.

Guida introduttiva toocontinue con IoT Hub e tooexplore altri scenari IoT, vedere:

- [Gestire la messaggistica dei dispositivi cloud con iothub-explorer](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [Salvare i messaggi di IoT Hub tooAzure archiviazione dei dati](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [Usare Power BI toovisualize sensore in tempo reale dati provenienti dall'IoT Hub Azure](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [Utilizzare le app Web di Azure toovisualize sensore in tempo reale dati provenienti dall'IoT Hub Azure](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [Previsioni meteorologiche utilizzando i dati del sensore hello dall'hub IoT in Azure Machine Learning](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [Gestione dei dispositivi con iothub-explorer](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [Monitoraggio remoto e notifiche con App per la logica](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)