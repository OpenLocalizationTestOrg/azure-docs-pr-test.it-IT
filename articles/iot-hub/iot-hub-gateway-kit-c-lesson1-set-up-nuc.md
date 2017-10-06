---
title: 'Dispositivo SensorTag e gateway Azure IoT: lezione 1: Configurare Intel NUC | Microsoft Docs'
description: Impostare toowork Intel NUC come gateway tra un sensore e informazioni di sensore toocollect Azure IoT Hub IoT e inviarla tooIoT Hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: gateway iot, intel nuc, computer nuc, DE3815TYKE
ms.assetid: 917090d6-35c2-495b-a620-ca6f9c02b317
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7c3ab3b014713c7facb86b8e8622d70e60a960e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a>Configurare Intel NUC come gateway IoT di Azure
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione

- Configurare Intel NUC come gateway IoT di Azure.
- Installare il pacchetto di Azure IoT Edge hello in hello NUC Intel.
- Eseguire un'applicazione di esempio "hello_world" in funzionalità del gateway di Intel NUC tooverify hello hello.

  > Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione

In questa lezione si apprenderà:

- Come tooconnect Intel NUC con le periferiche.
- Come tooinstall e aggiornare i pacchetti hello necessarie sull'uso di Intel NUC hello Smart Package Manager.
- Modalità di esempio funzionalità di gateway applicazione tooverify hello hello_world"toorun hello".

## <a name="what-you-need"></a>Elementi necessari

- Un Intel NUC Kit DE3815TYKE con hello Suite Software Gateway IoT di Intel (vento distretto Linux * 7.0.0.13) preinstallato. [Fare clic qui toopurchase Groove IoT commerciale Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).
- Un cavo Ethernet.
- Una tastiera.
- Un cavo HDMI o VGA.
- Un monitor con porta HDMI o VGA.
- Facoltativo: [SensorTag di Texas Instruments (CC2650STK)](http://www.ti.com/tool/cc2650stk)

![Kit gateway](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a>La connessione di Intel NUC con le periferiche hello

immagine di Hello riportata di seguito è riportato un esempio di Intel NUC connesso con le periferiche diverse:

1. Tastiera tooa connesso.
2. Monitoraggio tooa la connessione con un cavo o un cavo HDMI.
3. Connesso tooa rete tramite un cavo Ethernet cablata.
4. Alimentatore tooa connessi con un cavo di alimentazione.

![Tooperipherals NUC Intel connesso](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a>Connettere il sistema di Intel NUC toohello dal computer host tramite Secure Shell (SSH)

È necessario una tastiera e un indirizzo IP di monitoraggio tooget hello del dispositivo NUC Intel. Se si conosce già hello IP indirizzo, è possibile ignorare toostep ahead 3 di questa sezione.

1. Attivare hello Intel NUC premendo il pulsante di alimentazione hello e l'accesso.

   nome Hello predefinito dell'utente e password sono entrambi `root`.

       > Hit hello enter key on your keyboard if you see either of hello following errors when you boot: 'A TPM error (7) occurred attempting tooread a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. Ottenere l'indirizzo IP hello di hello Intel NUC eseguendo hello `ifconfig` comando sul dispositivo Intel NUC hello.

   Di seguito è riportato un esempio di output del comando hello.

   ![Output di ifconfig che indica l'IP di Intel NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   In questo esempio hello che segue `inet addr:` è l'indirizzo IP hello che è necessario connettersi quando toohello Intel NUC da un computer host.

3. Utilizzare uno dei seguenti client SSH dagli tooIntel di tooconnect computer host NUC hello.

    - [PuTTY](http://www.putty.org/) per Windows.
    - client SSH incorporato Hello in Ubuntu o macOS.

   È più efficiente e produttivo toooperate un NUC Intel da un computer host. Si sarà necessario hello indirizzo IP del NUC Intel, tooit di tooconnect di nome e una password utente tramite un client SSH. Di seguito è riportato un esempio che usa un client SSH in macOS.
   ![Client SSH eseguito su macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)

## <a name="install-hello-azure-iot-edge-package"></a>Installare il pacchetto di hello Azure IoT Edge

pacchetto di Azure IoT Edge Hello contiene i file binari precompilati hello di IoT Edge e le relative dipendenze. Questi binari sono Azure IoT Edge, hello Azure IoT SDK e strumenti corrispondenti hello. Hello pacchetto contiene anche un "hello_world" applicazione di esempio è una funzionalità di gateway hello toovalidate utilizzato. Bordo di IoT è fondamentale hello del gateway hello. 

Seguire questi pacchetti hello tooinstall di passaggi.

1. Aggiungere hello repository IoT Cloud eseguendo i seguenti comandi in una finestra terminale hello:

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > Immettere 'y', quando viene richiesto too'Include questo canale?'
   
   Se si riceve un `import read failed(-1)` errore, utilizzare hello problema di hello tooresolve i comandi seguenti:
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   Hello `rpm` comando importazioni hello chiave rpm. Hello `smart channel` comando aggiunge rpm hello canale toohello Smart Package Manager. Prima di eseguire hello `smart update` comando, verrà visualizzato un output come il seguente.

   ![output dei comandi di canale rpm e smart](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. Eseguire il comando di aggiornamento smart hello:

   ```bash
   smart update
   ```

3. Installare il pacchetto di Azure IoT Gateway hello eseguendo hello comando seguente:

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   `packagegroup-cloud-azure`è il nome di hello del pacchetto di hello. Hello `smart install` comando è il pacchetto di hello tooinstall utilizzato.

    > Comando che segue hello esecuzione se viene visualizzato questo errore: "chiave pubblica non disponibile"

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > Riavviare hello Intel NUC se viene visualizzato questo errore: 'alcun pacchetto non fornisce util-linux-dev'

   Dopo aver installato il pacchetto di hello, Intel NUC è pronto toofunction come gateway.

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a>Eseguire l'applicazione di esempio "hello_world" hello Azure IoT Edge

Hello dopo l'applicazione di esempio crea un gateway da un `hello_world.json` file e utilizza i componenti fondamentali di hello del bordo di Azure IoT architettura toolog un file di hello world messaggio tooa (txt) ogni 5 secondi.

È possibile eseguire l'esempio hello World Hello eseguendo hello seguenti comandi:

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

Consente di eseguire per alcuni minuti e quindi premere hello invio chiave toostop applicazione hello World Hello è.
![output dell'applicazione](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

> È possibile ignorare eventuali errori "invalid argument handle(NULL)" (handle argomento non valido(NULL)" visualizzati dopo aver premuto INVIO. 

È possibile verificare tale gateway hello è stato eseguito correttamente, aprire i file di log. txt hello che si trova ora nella cartella hello_world ![visualizzazione directory >.log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)

Aprire i log. txt utilizzando hello comando seguente:

```bash
vim log.txt
```

Verrà quindi visualizzato il contenuto di hello del log. txt, sarà un output in formato JSON di hello la registrazione dei messaggi che sono stati scritti ogni 5 secondi dal modulo di Hello World hello gateway.
![vista della directory log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)

Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="summary"></a>Riepilogo

Congratulazioni. La configurazione di Intel NUC come gateway è completata. Si è pronti toomove su toohello tooset lezione al successivo backup del computer host, creare un IoT Hub di Azure e registrare il dispositivo logico IoT Hub di Azure.

## <a name="next-steps"></a>Passaggi successivi
[Utilizzare un tooconnect di gateway tooAzure un dispositivo IoT Hub IoT](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

