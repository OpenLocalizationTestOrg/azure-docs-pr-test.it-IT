---
title: 'Dispositivo SensorTag e gateway Azure IoT: lezione 4: Creare l''app per le funzioni | Documentazione Microsoft'
description: Salvare i messaggi dall'hub IoT di Intel NUC tooyour, scriverli archiviazione tabelle tooAzure e quindi leggerli dal cloud hello.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: l'archiviazione dei dati nel cloud hello, dati archiviati nel cloud, iot servizio cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f84f9a85-e2c4-4a92-8969-f65eb34c194e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: efee3bdc15ced104651f4a500311a5fe614267c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a>Creare un'app per le funzioni di Azure e un account di archiviazione

Funzioni di Azure è una soluzione per l'esecuzione di facilmente _funzioni_ (frammenti di codice) nel cloud hello. Un'app di Azure funzione ospita esecuzione hello delle funzioni in Azure. 

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione

- Utilizzare un toocreate modello di gestione risorse di Azure un'app di Azure (funzione) e un account di archiviazione di Azure. app di Azure funzione Hello è in ascolto di eventi di hub IoT tooAzure, elabora i messaggi in arrivo e li scrive archiviazione tabella tooAzure.

Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-troubleshooting.md).


## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione

In questa lezione si apprenderà:

- Come toouse toodeploy Gestione risorse di Azure le risorse di Azure.
- Toouse di Azure come funzione app tooprocess messaggi IoT Hub e per scriverli tooa tabella nell'archiviazione tabelle di Azure.

## <a name="what-you-need"></a>Elementi necessari

È necessario avere completata lezioni precedenti hello:

- [Lezione 1: Configurare Intel NUC come gateway IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
- [Lezione 2: Preparare il computer host e l'hub IoT di Azure](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
- [Lezione 3: Ricevere messaggi da SensorTag e leggere i messaggi dall'hub IoT](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

## <a name="open-a-sample-app"></a>Aprire un'app di esempio

Passare tooyour `iot-hub-c-intel-nuc-gateway-getting-started` cartella repository, i file di configurazione di inizializzazione hello e hello quindi aprire un progetto di esempio nel codice di Visual Studio eseguendo hello comando seguente:

```bash
cd Lesson4
npm install
gulp init
code .
```

![Struttura del repository](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- Hello `arm-template.json` file è hello Azure Resource Manager modello contenente un'app di Azure (funzione) e un account di archiviazione di Azure.
- Hello `arm-template-param.json` tratta i file di configurazione hello utilizzato dal modello di gestione risorse di Azure hello.
- Hello `ReceiveDeviceMessages` sottocartella contiene codice Node.js hello hello Azure (funzione).

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Configurare i modelli di Azure Resource Manager e creare risorse in Azure

Hello aggiornamento `arm-template-param.json` file in Visual Studio Code.

![File JSON del modello di Azure Resource Manager](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- Sostituire `[your IoT Hub name]` con il nome `{my hub name}` specificato nella lezione 2.

Dopo l'aggiornamento hello `arm-template-param.json` file, distribuire hello risorse tooAzure eseguendo hello comando seguente:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

Utilizzare `iot-gateway` come valore hello `{resource group name}` se non si sono modificati valore hello nella lezione 2.

## <a name="summary"></a>Riepilogo

Aver creato il tooprocess app Azure funzione messaggi hub IoT e un'archiviazione di Azure account toostore questi messaggi. È ora possibile leggere i messaggi vengono inviati tramite l'hub IoT tooyour di gateway.

## <a name="next-steps"></a>Passaggi successivi
[Leggere i messaggi con salvataggio permanente in Archiviazione di Azure](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).
