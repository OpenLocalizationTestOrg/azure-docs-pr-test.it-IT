---
title: 'Connect Raspberry PI (C) tooAzure IoT - lezione 1: configurare i dispositivi | Documenti Microsoft'
description: "Installare hello Raspbian del sistema operativo, un sistema operativo gratuito che è ottimizzato per hello hardware Pi Raspberry configurare Raspberry Pi 3 per il primo utilizzo."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "installazione raspbian, raspbian download, la connettività di pi greco, al lampone tooraspberry connettersi come raspbian tooinstall, raspbian l'installazione, al lampone pi installazione raspbian, al lampone pi installazione del sistema operativo, al lampone pi sd card installazione, al lampone pi connect,"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8ee9b23c-93f7-43ff-8ea1-e7761eb87a6f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ba3466f6d5d46352326a2a63eb011e117da5aca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a>Configurare il dispositivo
## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
Configurare Pi per il primo utilizzo e installare hello Raspbian del sistema operativo. Raspbian è un sistema operativo gratuito che è ottimizzato per hello hardware Raspberry Pi. Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
Contenuto dell'articolo:

* Come tooinstall Raspbian su Pi.
* Come toopower backup Pi tramite un cavo USB.
* Come tooconnect Pi toohello rete tramite un cavo Ethernet o una rete wireless.
* Come tooadd toohello un LED breadboard e connetterla tooPi.

## <a name="what-you-need"></a>Elementi necessari
toocomplete questa operazione, è necessario hello dallo Starter Kit di Raspberry Pi 3 le seguenti parti:

* Hello Lavagna Raspberry Pi 3
* scheda microSD 16 GB Hello
* Hello 5 volt 2 amp alimentatore con il cavo USB micro di hello 6-ft
* breadboard Hello
* Cavi del connettore
* Resistore da 560 Ohm
* LED da 10 mm a luce diffusa
* Hello cavo Ethernet

![Contenuto dello starter kit](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

Altri elementi necessari:

* Una connessione cablata o wireless per Pi tooconnect per.
* Un USB SD adapter o mini SD card tooburn hello del sistema operativo immagine nella scheda microSD hello.
* Computer Windows, Mac o Linux. computer Hello è usato tooinstall Raspbian scheda microSD hello.
* Un toodownload connessione Internet hello software e gli strumenti necessari.

## <a name="install-raspbian-on-hello-microsd-card"></a>Installare Raspbian scheda MicroSD hello
Preparare una scheda microSD hello per l'installazione dell'immagine Raspbian hello.

1. Scaricare Raspbian.
   1. [Scaricare](https://www.raspberrypi.org/downloads/raspbian/) file con estensione zip hello per Raspbian Jessie con Pixel.
   2. Estrarre la cartella di hello Raspbian immagine tooa nel computer in uso.
2. Installare una scheda microSD di Raspbian toohello.
   1. [Scaricare](https://www.etcher.io) e installare hello Etcher SD card masterizzatore utilità.
   2. Eseguire Etcher e selezionare l'immagine Raspbian hello estratta nel passaggio 1.
   3. Selezionare un'unità scheda microSD hello.
      Si noti che Etcher potrebbe essere stata già selezionata unità corretta hello.
   4. Fare clic su **Flash** tooinstall Raspbian toohello microSD scheda.
   5. Rimuovi scheda microSD hello dal computer al termine dell'installazione.
      Scheda microSD di hello tooremove provvisoria è direttamente perché Etcher Smonta scheda microSD hello dopo il completamento o rimuove automaticamente.
   6. Inserire il Pi scheda microSD hello.

![Inserire hello SD card](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a>Accendere Pi
Attivare Pi tramite cavo USB micro hello e alimentatore hello.

![Accendere](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> È importante toouse hello alimentatore nel kit di hello almeno toomake 2A che sia il Raspberry sufficiente toowork power correttamente.

## <a name="enable-ssh"></a>Abilitare SSH
A partire dalla versione di novembre 2016 hello, Raspbian ha server SSH hello disabilitato per impostazione predefinita. È necessario tooenable è manualmente. È possibile fare riferimento toohello [istruzioni ufficiale](https://www.raspberrypi.org/documentation/remote-access/ssh/) o collegare un monitor e andare troppo**Preferenze -> configurazione Pi Raspberry** tooenable SSH.

## <a name="connect-raspberry-pi-3-toohello-network"></a>Connessione di rete toohello Raspberry Pi 3
È possibile connettersi tooa Pi cablata tooa di rete wireless o di rete. Assicurarsi che l'installazione guidata piattaforma sia connesso toohello stessa rete del computer. Ad esempio, è possibile connettersi toohello Pi che stesso commutatore che il computer è connesso.

### <a name="connect-tooa-wired-network"></a>La connessione di rete cablata tooa
Utilizzare hello Ethernet via cavo tooconnect tooyour Pi rete cablata. Hello due LED Pi accendere se hello connessione viene stabilita.

![Connettersi tramite cavo Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-tooa-wireless-network"></a>Connessione rete wireless tooa
Seguire hello [istruzioni](https://www.raspberrypi.org/learning/software-guide/wifi/) dalla rete wireless di hello Raspberry Pi Foundation tooconnect Pi tooyour. Queste istruzioni richiedono toofirst connettere un monitoraggio e tooPi una tastiera.

## <a name="connect-hello-led-toopi"></a>Connettersi tooPi hello LED
toocomplete questa attività, utilizzare hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), hello cavi connettore, hello LED e hello resistenza. Connetterle toohello [input/output generico](https://www.raspberrypi.org/documentation/usage/gpio/) porte (GPIO) di pi greco.

![Basetta sperimentale, LED e resistore](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. Connettersi segmento più breve di hello del LED hello troppo**GPIO GND (6 Pin)**.
2. Connettersi segmento più lungo di hello del segmento tooone LED di resistenza hello hello.
3. Connettersi hello altro segmento di resistenza hello troppo**GPIO 4 (7 Pin)**.

Si noti che è importante polarità hello LED. generalmente impostata come attiva bassa.

![Piedinatura](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

Congratulazioni. Il dispositivo Raspberry Pi è stato configurato.

## <a name="summary"></a>Riepilogo
In questo articolo, si è appreso come tooconfigure pi greco, installando Raspbian, connessione rete tooa di pi greco, e la connessione a un tooPi LED. Si noti che hello che LED non ancora accendersi. attività successiva Hello è tooinstall hello strumenti e necessari software in preparazione per l'esecuzione di un'applicazione di esempio in Pi.

![L'hardware è pronto](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a>Passaggi successivi
[Ottenere strumenti hello](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

