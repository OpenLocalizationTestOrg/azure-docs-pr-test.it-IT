---
title: 'Dispositivo simulato e gateway Azure IoT: lezione 1: Configurare NUC | Documentazione Microsoft'
description: Impostare toowork Intel NUC come gateway tra un sensore e informazioni di sensore toocollect Azure IoT Hub IoT e inviarla tooIoT Hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: yjianfeng
tags: 
keywords: gateway iot, intel nuc, computer nuc, DE3815TYKE
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f41d6b2e-9b00-40df-90eb-17d824bea883
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c2146c7cd8ca54adbd0af279364ec8484be1b45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a>Configurare Intel NUC come gateway IoT di Azure

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione

- Configurare Intel NUC come gateway IoT di Azure.
- Installare il pacchetto di Azure IoT Edge hello in NUC Intel.
- Eseguire un'applicazione di esempio "hello_world" funzionalità di gateway di Intel NUC tooverify hello.
Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione

In questa lezione si apprenderà:

- Come tooconnect Intel NUC con le periferiche.
- Come tooinstall e aggiornare i pacchetti hello necessarie sull'uso di Intel NUC hello Smart Package Manager.
- Modalità di esempio funzionalità di gateway applicazione tooverify hello hello_world"toorun hello".

## <a name="what-you-need"></a>Elementi necessari

- Un Intel NUC Kit DE3815TYKE con hello Suite Software Gateway IoT di Intel (vento distretto Linux * 7.0.0.13) preinstallato.
- Un cavo Ethernet.
- Una tastiera.
- Un cavo HDMI o VGA.
- Un monitor con porta HDMI o VGA.

![Kit gateway](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a>La connessione di Intel NUC con le periferiche hello

immagine di Hello riportata di seguito è riportato un esempio di Intel NUC connesso con le periferiche diverse:

1. Tastiera tooa connesso.
2. Connesso toohello monitoraggio da un cavo o un cavo HDMI.
3. Connesso tooa rete cablata tramite un cavo Ethernet.
4. Alimentatore toohello connessi con un cavo di alimentazione.

![Tooperipherals NUC Intel connesso](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a>Connettere il sistema di Intel NUC toohello dal computer host tramite Secure Shell (SSH)

In questo caso, è necessario tastiera monitor tooget hello indirizzo IP e del dispositivo NUC. Se si conosce già hello IP indirizzo, è possibile ignorare toostep 3 di questa sezione.

1. Attivare Intel NUC premendo il pulsante di alimentazione hello e di log nel sistema hello.

   nome Hello predefinito dell'utente e password sono entrambi `root`.

2. Ottenere l'indirizzo IP hello del NUC eseguendo hello `ifconfig` comando. Questo passaggio viene eseguito sul dispositivo NUC hello.

   Di seguito è riportato un esempio di output del comando hello.

   ![Output di ifconfig che indica l'IP NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   In questo esempio hello che segue `inet addr:` è l'indirizzo IP hello che è necessario quando si pianifica tooconnect in modalità remota da un tooIntel computer host NUC.

3. Utilizzare uno dei seguenti client SSH dagli tooIntel di tooconnect computer host NUC hello.

   - [PuTTY](http://www.putty.org/) per Windows.
   - Hello compilazione SSH client Ubuntu o macOS.

   È più efficiente e produttivo toooperate su Intel NUC da un computer host. È necessario l'indirizzo IP hello hello, nome utente e password tooconnect hello NUC tramite client SSH. Ecco client SSH utilizzo di esempio hello in macOS.
   ![Client SSH eseguito su macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)

## <a name="install-hello-azure-iot-edge-package"></a>Installare il pacchetto di hello Azure IoT Edge

pacchetto di Azure IoT Edge Hello contiene i file binari precompilati hello di hello SDK e le relative dipendenze. Questi binari sono Azure IoT Edge, hello Azure IoT SDK e strumenti corrispondenti hello. pacchetto di Hello contiene anche un'applicazione di esempio "hello_world" che è una funzionalità di gateway hello toovalidate utilizzato. Bordo di IoT è fondamentale hello del gateway hello. tooinstall hello del pacchetto, seguire questi passaggi:

1. Aggiungi repository di cloud di hello IoT eseguendo i seguenti comandi in una finestra terminale hello:

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   Hello `rpm` comando importazioni hello chiave rpm. Hello `smart channel` comando aggiunge rpm hello canale toohello Smart Package Manager. Prima di eseguire hello `smart update` comando, viene visualizzato un output simile di sotto.

   ![output dei comandi di canale rpm e smart](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. Installare il pacchetto di hello eseguendo hello comando seguente:

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   `packagegroup-cloud-azure`è il nome di hello del pacchetto di hello. Hello `smart install` comando è il pacchetto di hello tooinstall utilizzato.

   Dopo aver installato il pacchetto di hello, Intel NUC è toowork previsto come gateway.

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a>Eseguire l'applicazione di esempio "hello_world" hello Azure IoT Edge

Andare troppo`azureiotgatewaysdk/samples` ed eseguire l'applicazione di esempio "hello_world" esempio hello. Questa applicazione di esempio crea un gateway da hello `hello_world.json` file e utilizza i componenti fondamentali di hello di hello Azure IoT Edge architettura toolog un file di hello world messaggio tooa ogni 5 secondi.

È possibile eseguire l'applicazione di esempio "hello_world" esempio hello eseguendo hello comando seguente:

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

applicazione di esempio Hello produce output se la funzionalità di gateway hello funziona correttamente seguente di hello:

![output dell'applicazione](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="summary"></a>Riepilogo

Congratulazioni. La configurazione di Intel NUC come gateway è completata. Si è pronti toomove su toohello tooset lezione al successivo backup del computer host, creare un hub IoT di Azure e registrare il dispositivo logico di hub IoT di Azure.

## <a name="next-steps"></a>Passaggi successivi
[Preparare il computer host e l'hub IoT di Azure](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
