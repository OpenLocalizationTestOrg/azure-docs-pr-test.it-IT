---
title: 'Connettersi Arduino tooAzure IoT - lezione 2: registrazione del dispositivo | Documenti Microsoft'
description: Creare un gruppo di risorse, creare un hub IoT di Azure e registrare Adafruit sfumatura M0 WiFi nell'hub IoT Azure hello utilizzando hello CLI di Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: connessione arduino toocloud, hub iot di azure, internet del cloud di operazioni, l'hub iot azure creare un dispositivo, arduino cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 5edc690b-7a1d-4ebc-b011-ff27bfffe6e8
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ca362f9c143dd3a98bf47a66b63a9725a0ffc2d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-your-adafruit-feather-m0-wifi-arduino-board"></a>Creare l'hub IoT e registrare la scheda Adafruit Feather M0 WiFi Arduino

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
* Creare un gruppo di risorse.
* Creare l'hub IoT di Azure nel gruppo di risorse hello.
* Aggiungere l'hub IoT di Azure di Arduino Lavagna toohello utilizzando hello Azure interfaccia della riga di comando (CLI di Azure).

Quando si usa hello Azure CLI tooadd l'hub IoT di Arduino Lavagna tooyour, servizio hello genera una chiave per il tooauthenticate Lavagna Arduino con servizio hello. Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshoot].

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
Contenuto dell'articolo:
* Come un hub IoT toouse hello toocreate CLI di Azure.
* Come un'identità del dispositivo per il Arduino toocreate board nell'hub IoT.

## <a name="what-you-need"></a>Elementi necessari
* Un account Azure
* Un computer con hello Azure CLI installato

## <a name="create-your-iot-hub"></a>Creare l'hub IoT
L'hub IoT di Azure consente di connettersi a milioni di asset IoT, monitorarli e gestirli. toocreate l'hub IoT, seguire questi passaggi:

1. Accedi tooyour account Azure eseguendo hello comando seguente:

   ```bash
   az login
   ```

   Dopo l'accesso vengono elencate tutte le sottoscrizioni disponibili.

2. Impostare la sottoscrizione predefinita hello che si desidera toouse eseguendo hello comando seguente:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`possono essere trovati nell'output di hello di hello `az login` o hello `az account list` comando.

3. Registrare il provider di hello eseguendo hello comando seguente. I provider di risorse sono servizi che forniscono risorse per l'applicazione. Prima di poter distribuire hello risorsa di Azure che hello offerte di provider, è necessario registrare il provider di hello.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. Creare un gruppo di risorse denominato iot-esempio nell'area Stati Uniti occidentali hello eseguendo hello comando seguente:

   ```bash
   az group create --name iot-sample --location westus
   ```

   `westus`è il percorso di hello creare il gruppo di risorse. Se si desidera toouse un'altra posizione, è possibile eseguire `az account list-locations -o table` toosee tutti hello Azure supporta percorsi.

5. Creare un hub IoT nel gruppo di risorse di esempio di iot hello eseguendo hello comando seguente:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

Per impostazione predefinita, lo strumento hello crea un IoT Hub nel piano tariffario gratuito hello. Per altre informazioni, vedere [Prezzi dell'hub Iot di Azure](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE]
> nome Hello dell'hub IoT deve essere globalmente univoco.
> È possibile creare una sola edizione F1 dell'hub IoT di Azure nella sottoscrizione di Azure.

## <a name="register-your-arduino-board-in-your-iot-hub"></a>Registrare la scheda Arduino nell'hub IoT
Ogni dispositivo che invia l'hub IoT tooyour messaggi e riceve messaggi dall'hub IoT deve essere registrato con un ID univoco.

Registrare la scheda Arduino nell'hub IoT con il comando seguente:

```bash
az iot device create --device-id mym0wifi --hub-name {my hub name}
```

## <a name="summary"></a>Riepilogo
È stato creato un hub IoT ed è stata registrata una scheda Arduino con un'identità di dispositivo nell'hub IoT. Si è pronti toolearn come toosend messaggi dall'hub IoT tooyour di Arduino Lavagna.

## <a name="next-steps"></a>Passaggi successivi
[Creare un'app di Azure (funzione) e un hub IoT tooprocess e l'archivio del account di archiviazione di Azure messaggi][process-and-store-iot-hub-messages].


<!-- Images and links -->

[troubleshoot]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md