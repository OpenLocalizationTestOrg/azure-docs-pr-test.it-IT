---
title: aaaIntel Edison toocloud (C) - connessione Edison Intel tooAzure IoT Hub | Documenti Microsoft
description: Informazioni su come toosetup e connettersi Edison Intel tooAzure IoT Hub per la piattaforma cloud di Azure Edison Intel toosend dati toohello in questa esercitazione.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Azure iot intel edison, intel hub iot edison, intel edison invia dati toocloud, intel toocloud edison
ms.assetid: 4885fa2c-c2ee-4253-b37f-ccd55f92b006
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/17/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0928e6c7870d724ff2044280937a45a9e032c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-intel-edison-tooazure-iot-hub-c"></a>Connettersi Edison Intel tooAzure IoT Hub (C)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

In questa esercitazione, è necessario innanzitutto hello nozioni fondamentali sulle operazioni con Intel Edison di apprendimento. Si apprenderà quindi la modalità di connessione cloud toohello dispositivi utilizzando tooseamlessly [IoT Hub Azure](iot-hub-what-is-iot-hub.md).

Se non si ha ancora un kit, iniziare da [qui](https://azure.microsoft.com/develop/iot/starter-kits)

## <a name="what-you-do"></a>Operazioni da fare

* Configurare i moduli Intel Edison e Grove.
* Creare un hub IoT.
* Registrare un dispositivo per Edison nel proprio hub IoT.
* Eseguire un'applicazione di esempio nell'hub IoT di Edison toosend sensore dati tooyour.

Connettersi Edison Intel tooan l'hub IoT creati. Quindi eseguire un'applicazione di esempio in Edison toocollect temperatura e umidità dati da un sensore di temperatura Groove. Infine, si invia l'hub IoT hello sensore dati tooyour.

## <a name="what-you-learn"></a>Contenuto dell'esercitazione

* Come toocreate un hub IoT di Azure e ottenere la stringa di connessione nuovo dispositivo.
* Come tooconnect Edison con un sensore di temperatura Groove.
* Come dati del sensore toocollect mediante l'esecuzione di un'applicazione di esempio su Edison.
* Come l'hub IoT toosend sensore dati tooyour.

## <a name="what-you-need"></a>Elementi necessari

![Elementi necessari](media/iot-hub-intel-edison-kit-c-get-started/0_kit.png)

* Hello Lavagna Edison Intel
* Scheda di espansione Arduino
* Una sottoscrizione di Azure attiva. Se non si ha un account Azure, [creare un account Azure gratuito](https://azure.microsoft.com/free/) in pochi minuti.
* Un Mac o PC che esegue Windows o Linux.
* Una connessione Internet.
* Un cavo USB A di tooType Micro B
* Alimentatore in corrente continua (CC). I valori nominali dell'alimentatore devono essere i seguenti:
  - 7-15 V CC
  - Almeno 1500 mA
  - pin center/interna Hello devono essere polo positivo hello di alimentatore hello

Hello seguenti elementi è facoltativo:

* Grove Base Shield V2
* Sensore temperatura Grove
* Cavo Grove
* Le barre dello spaziatore né viti incluse nel pacchetto di hello, tra cui scheda di espansione toohello modulo hello toofasten due viti e quattro set di viti e spaziatore plastica.

> [!NOTE] 
Poiché il supporto di esempio di codice hello simulati i dati del sensore, questi elementi sono facoltativi.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a>Configurare Intel Edison

### <a name="assemble-your-board"></a>Assemblare la scheda

In questa sezione contiene passaggi tooattach la scheda di espansione Intel® Edison tooyour modulo.

1. Modulo di Intel® Edison hello sul posto all'interno di struttura hello bianca sulla Lavagna espansione, allineare fori hello sul modulo hello con viti hello nella scheda di espansione hello.

2. Premere sul modulo hello subito dopo le parole hello `What will you make?` fino a quando non si ritiene un gioco da ragazzi.

   ![assemblare la scheda 2](media/iot-hub-intel-edison-kit-c-get-started/1_assemble_board2.jpg)

3. Utilizzare una scheda di espansione di hello due dadi esadecimale (inclusi nel pacchetto hello) toosecure hello modulo toohello.

   ![assemblare la scheda 3](media/iot-hub-intel-edison-kit-c-get-started/2_assemble_board3.jpg)

4. Inserire una vite in uno dei quattro fori angolo hello nella scheda di espansione hello. Torsione e stringere uno spaziatore plastica di hello bianco su vite hello.

   ![assemblare la scheda 4](media/iot-hub-intel-edison-kit-c-get-started/3_assemble_board4.jpg)

5. Ripetere l'operazione per hello spaziatore altri tre angolo.

   ![assemblare la scheda 5](media/iot-hub-intel-edison-kit-c-get-started/4_assemble_board5.jpg)

A questo punto la scheda è assemblata.

   ![scheda assemblata](media/iot-hub-intel-edison-kit-c-get-started/5_assembled_board.jpg)

### <a name="connect-hello-grove-base-shield-and-hello-temperature-sensor"></a>Connettere hello dello scudo di Base di Groove e sensore di temperatura hello

1. Inserire hello dello scudo di Base di Groove nella Lavagna tooyour. e assicurarsi che sia inserito correttamente nella scheda.
   
   ![Grove Base Shield](media/iot-hub-intel-edison-kit-c-get-started/6_grove_base_sheild.jpg)

2. Sensore di temperatura utilizzare Groove cavo tooconnect Groove su hello dello scudo di Base di Groove **A0** porta.

   ![Connettersi sensore tootemperature](media/iot-hub-intel-edison-kit-c-get-started/7_temperature_sensor.jpg)
   
   ![Edison e connessione al sensore](media/iot-hub-intel-edison-kit-c-get-started/16_edion_sensor.png)

Il sensore è pronto.

### <a name="power-up-edison"></a>Alimentare Edison

1. Plug-in dell'alimentatore hello.

   ![Collegare l'alimentatore](media/iot-hub-intel-edison-kit-c-get-started/8_plug_power.jpg)

2. Un LED verde (nella scheda di espansione Arduino * hello con etichettato DS1) dovrebbe accendersi e rimanere acceso.

3. Attendere un minuto per hello Lavagna toofinish l'avvio.

   > [!NOTE]
   > Se non si dispone di un alimentatore controller di dominio, è comunque possibile Lavagna hello power attraverso una porta USB. Per informazioni dettagliate, vedere la sezione `Connect Edison tooyour computer`. Questo modo di alimentare la scheda può causarne un comportamento non prevedibile, soprattutto quando si usa il Wi-Fi o si comandano motori.

### <a name="connect-edison-tooyour-computer"></a>Connettere computer tooyour Edison

1. Attiva o disattiva verso il basso microinterruttore hello verso hello due micro porte USB, in modo che Edison è in modalità di dispositivo. Per informazioni sulle differenze tra la modalità dispositivo e la modalità host, vedere [qui](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).

   ![Attivare o disattivare verso il basso microinterruttore hello](media/iot-hub-intel-edison-kit-c-get-started/9_toggle_down_microswitch.jpg)

2. Collegare il cavo USB micro di hello superiore porta USB micro hello.

   ![Porta micro-USB superiore](media/iot-hub-intel-edison-kit-c-get-started/10_top_usbport.jpg)

3. Plug hello altra estremità del cavo USB nel computer.

   ![USB computer](media/iot-hub-intel-edison-kit-c-get-started/11_computer_usb.jpg)

4. La scheda è completamente inizializzata quando il computer consente di montare una nuova unità (ad esempio inserendo una scheda SD).

## <a name="download-and-run-hello-configuration-tool"></a>Scaricare ed eseguire lo strumento di configurazione hello
Strumento di configurazione più recente di hello da ottenere [questo collegamento](https://software.intel.com/en-us/iot/hardware/edison/downloads) sotto hello `Installers` intestazione. Esecuzione dello strumento hello e seguire il visualizzate le istruzioni, fare clic su Avanti dove necessario

### <a name="flash-firmware"></a>Eseguire il flashing del firmware
1. In hello `Set up options` pagina, fare clic su `Flash Firmware`.
2. Selezionare tooflash immagine hello nella scheda effettuando una delle seguenti hello:
   - toodownload e flash la Lavagna con hello più recente del firmware immagine disponibile da Intel, selezionare `Download hello latest image version xxxx`.
   - Selezionare la scheda con un'immagine è già stato salvato nel computer in uso, tooflash `Select hello local image`. Sfoglia tooand hello selezionare l'immagine tooflash tooyour Lavagna.
3. strumento di configurazione Hello tenterà tooflash la Lavagna. processo lampeggiante Hello potrebbe richiedere too10 minuti.

### <a name="set-password"></a>Impostare la password
1. In hello `Set up options` pagina, fare clic su `Enable Security`.
2. Per la scheda Intel® Edison è possibile impostare un nome personalizzato. Facoltativo.
3. Digitare una password per la scheda e quindi fare clic su `Set password`.
4. Contrassegnare come inattivo password hello, che viene utilizzata in un secondo momento.

### <a name="connect-wi-fi"></a>Connettere il Wi-Fi
1. In hello `Set up options` pagina, fare clic su `Connect Wi-Fi`. Attesa di minuto tooone come l'analisi del computer per reti Wi-Fi disponibili.
2. Da hello `Detected Networks` elenco a discesa, selezionare la rete.
3. Da hello `Security` elenco a discesa, il tipo di sicurezza della rete selezionare hello.
4. Specificare le informazioni di accesso e la password, quindi fare clic su `Configure Wi-Fi`.
5. Contrassegnare come inattivo hello indirizzo IP, che viene utilizzato in un secondo momento.

> [!NOTE]
> Assicurarsi che Edison sia connesso toohello stessa rete del computer. Il computer si connette tooyour Edison utilizzando l'indirizzo IP hello.

   ![Connettersi sensore tootemperature](media/iot-hub-intel-edison-kit-c-get-started/12_configuration_tool.png)

Congratulazioni. Edison è stato configurato.

## <a name="run-a-sample-application-on-intel-edison"></a>Eseguire un'applicazione di esempio in Intel Edison

### <a name="prepare-hello-azure-iot-device-sdk"></a>Preparare hello dispositivo IoT di Azure SDK

1. Utilizzare uno dei seguenti client SSH dagli tooyour di tooconnect computer host Intel Edison hello. indirizzo IP Hello è dallo strumento di configurazione hello e password di hello è hello uno impostate in questo strumento.
    - [PuTTY](http://www.putty.org/) per Windows.
    - client SSH incorporato Hello in Ubuntu o macOS (eseguire `ssh root@"hello IP address"`).

2. Clone hello esempio app tooyour dispositivo client. 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-edison-client-app.git
   ```

3. Passare quindi hello toorun cartella repository di toohello successivo comando toobuild IoT di Azure SDK

   ```bash
   cd iot-hub-c-intel-edison-client-app
   sed -i -e 's/\r$//' buildSDK.sh
   chmod 755 buildSDK.sh
   ./buildSDK.sh
   ```

### <a name="configure-hello-sample-application"></a>Configurare l'applicazione di esempio hello

1. Aprire il file di configurazione hello eseguendo hello seguenti comandi:

   ```bash
   nano config.h
   ```

   ![File di configurazione](media/iot-hub-intel-edison-kit-c-get-started/13_configure_file.png)

   Questo file contiene due macro configurabili. Hello prima uno è `INTERVAL`, che definisce l'intervallo di tempo hello tra due messaggi che inviano toocloud. Hello secondo `SIMULATED_DATA`, ovvero un valore booleano per se toouse sensore dati simulati o non.

   Se si **non dispone di sensore hello**, hello impostare `SIMULATED_DATA` valore troppo`1` applicazione di esempio hello toomake creare e utilizzare dati del sensore simulato.

2. Salvare e uscire premendo CTRL-O > Invio > CTRL-X.

### <a name="build-and-run-hello-sample-application"></a>Compilare ed eseguire l'applicazione di esempio hello

1. Compilare l'applicazione di esempio hello eseguendo hello comando seguente:

   ```bash
   cmake . && make
   ```
   ![Output della compilazione](media/iot-hub-intel-edison-kit-c-get-started/14_build_output.png)

1. Eseguire l'applicazione di esempio hello eseguendo hello comando seguente:

   ```bash
   sudo ./app '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   Assicurarsi copiare e incollare stringa di connessione del dispositivo hello in virgolette hello.

Verrà visualizzato l'output seguente hello che mostra hello sensore dati e hello i messaggi vengono inviati tooyour IoT hub.

![Output - sensore dati vengono inviati da Intel Edison tooyour hub IoT](media/iot-hub-intel-edison-kit-c-get-started/15_message_sent.png)

## <a name="next-steps"></a>Passaggi successivi

È stato eseguito dati sensore toocollect di applicazione di esempio e inviarlo tooyour IoT hub.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
