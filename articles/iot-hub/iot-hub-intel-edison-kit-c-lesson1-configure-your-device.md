---
title: 'Connect Intel Edison (C) tooAzure IoT - lezione 1: configurare i dispositivi | Documenti Microsoft'
description: Configurare Intel Edison per il primo utilizzo.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino impostato, connettersi arduino toopc, il programma di installazione arduino, arduino Lavagna
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: bb8aa45b-d3ff-4438-b9d6-a9725a45ade1
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5e06e06f1fcea02086e95742804f82cfcb8e265f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-intel-edison"></a>Configurare Intel Edison
## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
Configurare Edison Intel per primo utilizzo assemblando Lavagna hello, l'accensione e l'installazione dello strumento Configurazione tooyour desktop tooflash OS firmware di Edison, impostare la relativa password e connetterla tooWi-Fi. Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
Contenuto dell'articolo:

* Come tooassemble Edison bordo e il sistema e backup.
* Come firmware di Edison tooflash, impostare la password e la connessione Wi-Fi.

## <a name="what-you-need"></a>Elementi necessari
toocomplete questa operazione, è necessario hello dallo Starter Kit Edison Intel le seguenti parti:

* Modulo Intel® Edison
* Scheda di espansione Arduino
* Le barre dello spaziatore né viti incluse nel pacchetto di hello, tra cui scheda di espansione toohello modulo hello toofasten due viti e quattro set di viti e spaziatore plastica.
* Un cavo USB A di tooType Micro B
* Alimentatore in corrente continua (CC). I valori nominali dell'alimentatore devono essere i seguenti:
  - 7-15 V CC
  - Almeno 1500 mA
  - pin center/interna Hello devono essere polo positivo hello di alimentatore hello

  ![Contenuto dello starter kit](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

Altri elementi necessari:

* Computer Windows, Mac o Linux.
* Una connessione wireless per tooconnect Edison per.
* Strumento di configurazione toodownload connessione Internet.

## <a name="assemble-your-board"></a>Assemblare la scheda

In questa sezione contiene passaggi tooattach la scheda di espansione Intel® Edison tooyour modulo.

1. Modulo di Intel® Edison hello sul posto all'interno di struttura hello bianca sulla Lavagna espansione, allineare fori hello sul modulo hello con viti hello nella scheda di espansione hello.

2. Premere sul modulo hello subito dopo le parole hello `What will you make?` fino a quando non si ritiene un gioco da ragazzi.

   ![assemblare la scheda 2](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. Utilizzare una scheda di espansione di hello due dadi esadecimale (inclusi nel pacchetto hello) toosecure hello modulo toohello.

   ![assemblare la scheda 3](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. Inserire una vite in uno dei quattro fori angolo hello nella scheda di espansione hello. Torsione e stringere uno spaziatore plastica di hello bianco su vite hello.

   ![assemblare la scheda 4](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. Ripetere l'operazione per hello spaziatore altri tre angolo.

   ![assemblare la scheda 5](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

A questo punto la scheda è assemblata.

   ![scheda assemblata](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a>Alimentare Edison

1. Plug-in dell'alimentatore hello.

   ![Collegare l'alimentatore](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. Un LED verde (nella scheda di espansione Arduino * hello con etichettato DS1) dovrebbe accendersi e rimanere acceso.

3. Attendere un minuto per hello Lavagna toofinish l'avvio.

   > [!NOTE]
   > Se non si dispone di un alimentatore controller di dominio, è comunque possibile Lavagna hello power attraverso una porta USB. Per informazioni dettagliate, vedere la sezione `Connect Edison tooyour computer`. Questo modo di alimentare la scheda può causarne un comportamento non prevedibile, soprattutto quando si usa il Wi-Fi o si comandano motori.

## <a name="connect-edison-tooyour-computer"></a>Connettere computer tooyour Edison

1. Attiva o disattiva verso il basso microinterruttore hello verso hello due micro porte USB, in modo che Edison è in modalità di dispositivo. Per informazioni sulle differenze tra la modalità dispositivo e la modalità host, vedere [qui](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).

   ![Attivare o disattivare verso il basso microinterruttore hello](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. Collegare il cavo USB micro di hello superiore porta USB micro hello.

   ![Porta micro-USB superiore](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. Plug hello altra estremità del cavo USB nel computer.

   ![USB computer](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

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

Congratulazioni. Edison è stato configurato.

## <a name="summary"></a>Riepilogo
In questo articolo, si è appreso come tooassemble hello Lavagna Edison, flash relativo firmware, la password di installazione e connetterla tooWi-Fi usando lo strumento di configurazione. Si noti che hello che LED non ancora accendersi. attività successiva Hello è software in preparazione per l'esecuzione di un'applicazione di esempio in Edison e gli strumenti necessari di tooinstall hello.

## <a name="next-steps"></a>Passaggi successivi
[Ottenere strumenti hello][get-the-tools]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md