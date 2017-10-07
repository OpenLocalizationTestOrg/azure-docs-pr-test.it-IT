---
featureFlags: usabilla
title: 'Connettersi Raspberry Pi (nodo) tooAzure IoT - lezione 2: registrazione del dispositivo | Documenti Microsoft'
description: "Creare un gruppo di risorse, creare un hub IoT di Azure e registrare Pi in hello del Registro di sistema di IoT Hub identità tramite l'interfaccia CLI di Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: cloud raspberry pi, connessione cloud pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 736215b6-e7e4-46f9-af30-0ded9ffa5204
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 97533298d52d1187c49a4c35ddda922d6e45c87d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a>Creare l'hub IoT e registrare Raspberry Pi 3
## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
* Creare un gruppo di risorse.
* Creare l'hub IoT di Azure nel gruppo di risorse hello.
* Aggiungere Raspberry Pi 3 toohello Azure IoT hub utilizzando hello Azure interfaccia della riga di comando (CLI di Azure).

Quando si usa l'hub IoT Azure CLI tooadd Pi tooyour, servizio hello genera una chiave per Pi tooauthenticate con servizio hello. Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
Contenuto dell'articolo:
* Come toouse CLI di Azure toocreate un hub IoT
* Come toocreate un'identità del dispositivo per Pi nell'hub IoT

## <a name="what-you-need"></a>Elementi necessari
* Un account Azure
* Un Mac o in un computer Windows con hello Azure CLI installato

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
> nome Hello dell'hub IoT deve essere globalmente univoco. È possibile creare una sola edizione F1 dell'hub IoT di Azure nella sottoscrizione di Azure.

## <a name="register-pi-in-your-iot-hub"></a>Registrare il dispositivo Pi nell'hub IoT
Ogni dispositivo che invia l'hub IoT tooyour messaggi e riceve messaggi dall'hub IoT deve essere registrato con un ID univoco. Si verrà utilizzata tooregister CLI di Azure il Pi e creare un certificato autofirmato x. 509 per l'autenticazione del dispositivo.

Eseguire hello comando seguente:

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a>Riepilogo
È stato creato un hub IoT e il dispositivo Pi è stato registrato con un'identità del dispositivo nell'hub IoT. Si è pronti toolearn come toosend messaggi dall'hub IoT tooyour di pi greco.

## <a name="next-steps"></a>Passaggi successivi
[Creare un'app di Azure (funzione) e un tooprocess di account di archiviazione di Azure e archiviare i messaggi di hub IoT](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)

