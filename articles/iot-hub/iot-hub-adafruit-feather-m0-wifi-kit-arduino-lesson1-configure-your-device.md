---
title: 'Connect Arduino (C) tooAzure IoT - lezione 1: configurare i dispositivi | Documenti Microsoft'
description: Configurare Adafruit Feather M0 WiFi per il primo utilizzo.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino impostato, connettersi arduino toopc, il programma di installazione arduino, arduino Lavagna
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: f5b334f0-a148-41aa-b374-ce7b9f5b305a
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 30b764e8ff6221995456283a226e79f064b2d74e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a>Configurare il dispositivo
## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
Configurare la Lavagna Adafruit sfumatura M0 Wi-Fi Arduino per primo utilizzo assemblando Lavagna hello, l'accensione. Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).

## <a name="what-you-need"></a>Elementi necessari
toocomplete questa operazione, è necessario hello seguenti parti per lo Starter Kit Adafruit sfumatura M0 Wi-Fi:

* Hello Adafruit sfumatura M0 WiFi Lavagna
* Un cavo USB A di tooType Micro B

![kit][kit]

Altri elementi necessari:

* Computer Windows, Mac o Linux.
* Una connessione wireless per i tooconnect Lavagna Arduino per.
* Strumento di configurazione toodownload connessione Internet.

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
Contenuto dell'articolo:

* Come tooassemble la Lavagna Arduino e potenza, per hello seguenti lezioni.
* Come le autorizzazioni di porta seriale tooadd per Ubuntu.

## <a name="connect-your-arduino-board-tooyour-computer"></a>Connettere il computer di tooyour Arduino Lavagna

1. Collegare il cavo USB micro di hello superiore porta USB micro hello.

   ![Porta micro-USB superiore][top-micro-usb-port]

2. Plug hello altra estremità del cavo USB nel computer.

   ![USB computer][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a>Aggiungere autorizzazioni per la porta seriale in Ubuntu

Se si usa Windows o macOS, è possibile ignorare questa sezione. Per Ubuntu, è necessario hello seguendo i passaggi toomake hello linux normale utente che disponga hello autorizzazioni toooperate sulla porta USB hello la Lavagna Arduino.

1. Come utente normale dal terminale:

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   Verrà visualizzata una schermata simile alla seguente:

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   Hello "0" potrebbe essere un numero diverso oppure potrebbero essere restituite più voci. In dati hello case primo hello dobbiamo `uucp`, hello in secondo luogo è `dialout`, che è proprietario del gruppo di hello del file hello.

2. Aggiungi utente toohello toohello gruppo:

   ```bash
   sudo usermod -a -G group-name username
   ```

   Dove `group-name` dati hello trovato nel primo passaggio hello e `username` è il nome utente di linux.

3. È necessario toolog e nuovamente per questo effetto tootake modifica e l'installazione completa di hello.

## <a name="summary"></a>Riepilogo
In questo articolo, si è appreso come tooconfigure la Lavagna Arduino. attività successiva Hello è software in preparazione per l'esecuzione di un'applicazione di esempio sulla Lavagna Arduino e gli strumenti necessari di tooinstall hello.

![L'hardware è pronto][hardware-is-ready]

## <a name="next-steps"></a>Passaggi successivi
[Ottenere strumenti hello][get-the-tools]
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md