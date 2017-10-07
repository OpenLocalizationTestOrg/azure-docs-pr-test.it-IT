---
title: 'Connect Arduino (C) tooAzure IoT - lezione 3: distribuzione del modello | Documenti Microsoft'
description: "app di Azure funzione Hello è in ascolto di eventi di hub IoT tooAzure, elabora i messaggi in arrivo e li scrive archiviazione tabella tooAzure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: l'archiviazione dei dati nel cloud hello, dati archiviati nel cloud, iot servizio cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9c8f4cd1-9511-4601-ad7e-51761a986753
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 6a84a6d3c5263a85c8997cf69fe446d73ab7a5fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>Creare un'app per le funzioni di Azure e un account di archiviazione di Azure
[Funzioni di Azure](../../articles/azure-functions/functions-overview.md) è una soluzione per l'esecuzione di facilmente *funzioni* (frammenti di codice) nel cloud hello. Un'app di Azure funzione ospita esecuzione hello delle funzioni in Azure.

## <a name="what-will-you-do"></a>Contenuto dell'esercitazione
Utilizzare un toocreate modello di gestione risorse di Azure un'app di Azure (funzione) e un account di archiviazione di Azure. app di Azure funzione Hello è in ascolto di eventi di hub IoT tooAzure, elabora i messaggi in arrivo e li scrive archiviazione tabella tooAzure.

Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina per la scheda Adafruit sfumatura M0 Wi-Fi Arduino](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).

## <a name="what-will-you-learn"></a>Concetti legati all'esercitazione
Contenuto dell'articolo:
* Come toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure le risorse.
* Toouse di Azure come funzione app tooprocess messaggi hub IoT e per scriverli tooa tabella nell'archiviazione tabelle di Azure.

## <a name="what-do-you-need"></a>Elementi necessari
È necessario aver completato:
- [Introduzione alla scheda Arduino][get-started]
- [Creare l'hub IoT di Azure][create-iot-hub]

## <a name="open-hello-sample-app"></a>App di esempio hello aperto
Aprire il progetto di esempio hello in Visual Studio Code eseguendo hello seguenti comandi:

```bash
cd Lesson3
code .
```

![Struttura del repository][repo-structure]

* Hello `app.ino` file hello `app` sottocartella è il file di origine della chiave hello. Questo file di origine contiene toosend codice hello un messaggio di 20 volte tooyour IoT hub e blink hello LED per ogni messaggio inviato.
* Hello `config.json` contiene le impostazioni di configurazione necessarie.
* Hello `arm-template.json` file è hello Azure Resource Manager modello contenente un'app di Azure (funzione) e un account di archiviazione di Azure.
* Hello `arm-template-param.json` tratta i file di configurazione hello utilizzato dal modello di gestione risorse di Azure hello.
* Hello `ReceiveDeviceMessages` sottocartella contiene codice Node.js hello hello Azure (funzione).

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Configurare i modelli di Azure Resource Manager e creare risorse in Azure
Hello aggiornamento `arm-template-param.json` file in Visual Studio Code.

![Parametri del modello di Azure Resource Manager][arm-template-params]

* Sostituire **[your IoT Hub name]** con il valore di **{my hub name}** specificato quando [è stato creato l'hub IoT ed è stata registrata la scheda Arduino][created-iot-hub-and-registered-arduino-board].
* Sostituire **[prefix string for new resources]** con il prefisso desiderato. prefisso Hello assicura che il nome risorsa hello sia globalmente univoco tooavoid conflitto. Non usare un trattino o un numero iniziale nel prefisso hello.

Dopo l'aggiornamento hello `arm-template-param.json` file, distribuire hello risorse tooAzure eseguendo hello comando seguente:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

Sono necessari circa cinque minuti toocreate queste risorse. Durante la creazione di risorse hello è in corso, è possibile spostare toohello Avanti articolo.

## <a name="summary"></a>Riepilogo
Aver creato il tooprocess app Azure funzione messaggi hub IoT e un'archiviazione di Azure account toostore questi messaggi. È ora possibile distribuire ed eseguire i messaggi da dispositivo a cloud toosend di esempio hello sulla Lavagna Arduino.

## <a name="next-steps"></a>Passaggi successivi
[Eseguire un toosend di applicazione di esempio, i messaggi da dispositivo a cloud sulla Lavagna Arduino][send-device-to-cloud-messages]

<!-- Images and links -->

[get-started]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[create-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/repo_structure_c.png
[arm-template-params]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/arm_para_arduino.png
[created-iot-hub-and-registered-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md