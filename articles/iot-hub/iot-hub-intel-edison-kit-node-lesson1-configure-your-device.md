---
title: 'Connettere Intel Edison (Node) ad Azure IoT: lezione 1: Configurare il dispositivo | Documentazione Microsoft'
description: Configurare Intel Edison per il primo uso.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: configurazione arduino, connessione di arduino al pc, configurazione di arduino, scheda arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 372c9b6d-e701-4ff6-8151-d262aa76aa55
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 87bf3a917af096e43a43a2143afa4bf43a72d7fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-intel-edison"></a>Configurare Intel Edison
## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
Configurare Intel Edison per il primo utilizzo assemblando la scheda, fornendo l'alimentazione e installando lo strumento di configurazione nel sistema operativo desktop per eseguire il flashing del firmware Edison, impostarne la password e connetterlo al Wi-Fi. In caso di problemi, cercare le soluzioni nella [pagina sulla risoluzione dei problemi][troubleshooting].

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
Contenuto dell'articolo:

* Come assemblare la scheda Edison e fornire l'alimentazione.
* Come eseguire il flashing del firmware di Edison, impostare la password e connettere il Wi-Fi.

## <a name="what-you-need"></a>Elementi necessari
Per completare questa operazione, è necessario disporre dei componenti seguenti dello starter kit di Intel Edison:

* Modulo Intel® Edison
* Scheda di espansione Arduino
* Elementi distanziali o viti contenuti nel pacchetto, inclusi quattro set di viti ed elementi distanziali in plastica e due viti per fissare il modulo alla scheda di espansione.
* Cavo USB Micro B/Tipo A
* Alimentatore in corrente continua (CC). I valori nominali dell'alimentatore devono essere i seguenti:
  - 7-15 V CC
  - Almeno 1500 mA
  - Il pin centrale deve essere il polo positivo dell'alimentatore

  ![Contenuto dello starter kit](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

Altri elementi necessari:

* Computer Windows, Mac o Linux.
* Connessione wireless per Edison.
* Connessione Internet per scaricare lo strumento di configurazione.

## <a name="assemble-your-board"></a>Assemblare la scheda

Questa sezione contiene i passaggi per connettere il modulo Intel® Edison alla scheda di espansione.

1. Posizionare il modulo Intel® Edison all'interno del bordo bianco della scheda di espansione, allineando i fori del modulo con le viti della scheda di espansione.

2. Premere verso il basso il modulo sotto le parole `What will you make?` fino a quando non si sente uno scatto.

   ![assemblare la scheda 2](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. Usare i due dadi esagonali (inclusi nel pacchetto) per fissare il modulo alla scheda di espansione.

   ![assemblare la scheda 3](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. Inserire una vite in uno dei quattro fori negli angoli della scheda di espansione. Avvitare e fissare uno dei due elementi distanziali in plastica alla vite.

   ![assemblare la scheda 4](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. Ripetere l'operazione per gli altri tre elementi distanziali angolari.

   ![assemblare la scheda 5](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

A questo punto la scheda è assemblata.

   ![scheda assemblata](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a>Alimentare Edison

1. Collegare l'alimentatore.

   ![Collegare l'alimentatore](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. Un LED verde (con etichetta DS1 sulla scheda di espansione Arduino*) dovrebbe accendersi e rimanere acceso.

3. Attendere un minuto per il completamento dell'avvio della scheda.

   > [!NOTE]
   > Se non si dispone di un alimentatore CC, è comunque possibile alimentare la scheda tramite una porta USB. Per informazioni dettagliate, vedere la sezione `Connect Edison to your computer`. Questo modo di alimentare la scheda può causarne un comportamento non prevedibile, soprattutto quando si usa il Wi-Fi o si comandano motori.

## <a name="connect-edison-to-your-computer"></a>Connettere Edison al computer

1. Spostare i microinterruttori verso le due porte micro-USB in modo che Edison si trovi in modalità dispositivo. Per informazioni sulle differenze tra la modalità dispositivo e la modalità host, vedere [qui](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).

   ![Spostare verso il basso il microinterruttore](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. Collegare il cavo micro-USB alla porta micro-USB superiore.

   ![Porta micro-USB superiore](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. Collegare l'altra estremità del cavo USB al computer.

   ![USB computer](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. La scheda è completamente inizializzata quando il computer consente di montare una nuova unità (ad esempio inserendo una scheda SD).

## <a name="download-and-run-the-configuration-tool"></a>Scaricare ed eseguire lo strumento di configurazione
Scaricare lo strumento di configurazione più recente presente in [questo collegamento](https://software.intel.com/en-us/iot/hardware/edison/downloads) sotto l'intestazione `Installers`. Eseguire lo strumento e attenersi alle istruzioni visualizzate. Fare clic su Avanti quando necessario.

### <a name="flash-firmware"></a>Eseguire il flashing del firmware
1. Nella pagina `Set up options` fare clic su `Flash Firmware`.
2. Selezionare l'immagine per eseguire il flashing sulla scheda tramite una delle operazioni seguenti:
   - Per scaricare ed eseguire il flashing della scheda con l'immagine del firmware più recente disponibile in Intel, selezionare `Download the latest image version xxxx`.
   - Per eseguire il flashing della scheda con un'immagine già salvata nel computer, selezionare `Select the local image`. Individuare e selezionare l'immagine di cui si desidera eseguire il flashing nella scheda.
3. Lo strumento di installazione tenterà di eseguire il flashing della scheda. L'intero processo di esecuzione del flashing può richiedere fino a 10 minuti.

### <a name="set-password"></a>Impostare la password
1. Nella pagina `Set up options` fare clic su `Enable Security`.
2. Per la scheda Intel® Edison è possibile impostare un nome personalizzato. Facoltativo.
3. Digitare una password per la scheda e quindi fare clic su `Set password`.
4. Annotare la password per usarla in seguito.

### <a name="connect-wi-fi"></a>Connettere il Wi-Fi
1. Nella pagina `Set up options` fare clic su `Connect Wi-Fi`. Attendere fino a un minuto per la ricerca delle reti Wi-Fi disponibili.
2. Nell'elenco a discesa `Detected Networks` selezionare la rete.
3. Nell'elenco a discesa `Security` selezionare il tipo di sicurezza della rete.
4. Specificare le informazioni di accesso e la password, quindi fare clic su `Configure Wi-Fi`.
5. Annotare l'indirizzo IP per usarlo in seguito.

> [!NOTE]
> Verificare che Edison sia connesso alla stessa rete del computer. Il computer si connette a Edison tramite l'indirizzo IP.

Congratulazioni. Edison è stato configurato.

## <a name="summary"></a>Riepilogo
Questo articolo ha illustrato come assemblare la scheda Edison, eseguire il flashing del firmware, impostare la password e connetterla al Wi-Fi usando lo strumento di configurazione. Si noti che il LED non si illumina ancora. L'attività successiva consiste nell'installazione del software e degli strumenti necessari per preparare l'esecuzione di un'applicazione di esempio in Edison.

## <a name="next-steps"></a>Passaggi successivi
[Ottenere gli strumenti][get-the-tools]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md