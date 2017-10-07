---
title: 'Connettersi Raspberry Pi (nodo) tooAzure IoT - lezione 3: distribuzione del modello | Documenti Microsoft'
description: "app di Azure funzione Hello è in ascolto di eventi di hub IoT tooAzure, elabora i messaggi in arrivo e li scrive archiviazione tabella tooAzure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: l'archiviazione dei dati nel cloud hello, dati archiviati nel cloud, iot servizio cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6c58de85-c5c4-4989-bb5e-08c45c549966
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b6c0a9530cb80e3f78c0e96037f6f3942b602aea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>Creare un'app per le funzioni di Azure e un account di archiviazione di Azure
[Funzioni di Azure](../azure-functions/functions-overview.md) è una soluzione per l'esecuzione di facilmente *funzioni* (frammenti di codice) nel cloud hello. Un'app di Azure funzione ospita esecuzione hello delle funzioni in Azure.

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
Utilizzare un toocreate modello di gestione risorse di Azure un'app di Azure (funzione) e un account di archiviazione di Azure. app di Azure funzione Hello è in ascolto di eventi di hub IoT tooAzure, elabora i messaggi in arrivo e li scrive archiviazione tabella tooAzure. Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
Contenuto dell'articolo:

* Come toouse [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) toodeploy Azure le risorse.
* Toouse di Azure come funzione app tooprocess messaggi hub IoT e per scriverli tooa tabella nell'archiviazione tabelle di Azure.

## <a name="what-you-need"></a>Elementi necessari
È necessario aver completato:
* [Introduzione a Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-get-started.md)
* [Creare l'hub IoT di Azure](iot-hub-raspberry-pi-kit-node-get-started.md)

## <a name="open-hello-sample-app"></a>App di esempio hello aperto
Aprire il progetto di esempio hello in Visual Studio Code eseguendo hello seguenti comandi:

```bash
cd Lesson3
code .
```

![Struttura del repository](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure.png)

* Hello `app.js` file hello `app` sottocartella è il file di origine della chiave hello. Questo file di origine contiene toosend codice hello un messaggio di 20 volte tooyour IoT hub e blink hello LED per ogni messaggio inviato.
* Hello `arm-template.json` file è hello Azure Resource Manager modello contenente un'app di Azure (funzione) e un account di archiviazione di Azure.
* Hello `arm-template-param.json` tratta i file di configurazione hello utilizzato dal modello di gestione risorse di Azure hello.
* Hello `ReceiveDeviceMessages` sottocartella contiene codice Node.js hello hello Azure (funzione).

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Configurare i modelli di Azure Resource Manager e creare risorse in Azure
Hello aggiornamento `arm-template-param.json` file in Visual Studio Code.

![Parametri del modello di Azure Resource Manager](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para.png)

* Sostituire **[your IoT Hub name]** con il valore di **{my hub name}** specificato quando [è stato creato l'hub IoT ed è stato registrato il dispositivo Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).
* Sostituire **[prefix string for new resources]** con il prefisso desiderato. prefisso Hello assicura che il nome risorsa hello sia globalmente univoco tooavoid conflitto. Non usare un trattino o un numero iniziale nel prefisso hello.

Dopo l'aggiornamento hello `arm-template-param.json` file, distribuire hello risorse tooAzure eseguendo hello comando seguente:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

Sono necessari circa cinque minuti toocreate queste risorse. Durante la creazione di risorse hello è in corso, è possibile spostare toohello Avanti articolo.

## <a name="summary"></a>Riepilogo
Aver creato il tooprocess app Azure funzione messaggi hub IoT e un'archiviazione di Azure account toostore questi messaggi. È ora possibile distribuire ed eseguire messaggi da dispositivo a cloud toosend di esempio hello in Pi.

## <a name="next-steps"></a>Passaggi successivi
[Eseguire un toosend di applicazione di esempio, i messaggi da dispositivo a cloud Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md)

