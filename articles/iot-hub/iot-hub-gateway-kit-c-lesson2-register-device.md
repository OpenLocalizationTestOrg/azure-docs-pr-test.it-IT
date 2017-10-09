---
title: 'Dispositivo SensorTag e gateway Azure IoT: lezione 2: Registrare il dispositivo | Documentazione Microsoft'
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: hub iot di azure, cloud internet delle cose, hub iot di azure creare dispositivo, sensortag ti, ble ti
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 2c18f5ae-e39a-48ae-a9fe-04bb595740a0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5d2322268aa18f52f60c2833778323773ac4eec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a>Creare un hub IoT di Azure e registrare il dispositivo

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione

- Creare un gruppo di risorse
- Creare il primo hub IoT
- Registrare il dispositivo nell'hub IoT utilizzando hello CLI di Azure. 

Quando si registra il dispositivo nell'hub IoT, hello servizio IoT Hub Azure genera una chiave per il tooauthenticate toouse dispositivo con il servizio di hello. 

Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione

In questa lezione si apprenderà:

- Come un hub IoT toouse hello toocreate CLI di Azure.
- Come tooregister un dispositivo in un hub IoT.

## <a name="what-you-need"></a>Elementi necessari

- Una sottoscrizione di Azure attiva. Se non si ha un account Azure, è possibile [creare un account Azure gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.
- È necessario hello che Azure CLI installato.

## <a name="create-an-iot-hub"></a>Creare un hub IoT

toocreate un hub IoT, seguire questi passaggi:

1. Accedi tooyour account Azure eseguendo hello comando seguente:

   ```bash
   az login
   ```

   Dopo l'accesso verranno elencate tutte le sottoscrizioni disponibili.

2. Impostare il valore predefinito di hello sottoscrizione di Azure che si desidera toouse eseguendo hello comando seguente:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`possono essere trovati nell'output di hello di hello `az login` o hello `az account list` comando.

3. Registrare il provider di hello eseguendo hello comando seguente. I provider di risorse sono servizi che forniscono risorse per l'applicazione. Prima di poter distribuire hello risorsa di Azure che hello offerte di provider, è necessario registrare il provider di hello.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. Creare un gruppo di risorse denominato `iot-gateway` nell'area Stati Uniti occidentali hello eseguendo hello comando seguente:

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   `westus`è il percorso di hello creare il gruppo di risorse. Se si desidera toouse un'altra posizione, è possibile eseguire `az account list-locations -o table` toosee tutti hello Azure supporta percorsi.

5. Creare un hub IoT in hello `iot-gateway` gruppo di risorse eseguendo hello comando seguente:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

Per impostazione predefinita, lo strumento hello crea un IoT Hub nel piano tariffario gratuito hello. Per altre informazioni, vedere [Prezzi dell'hub Iot di Azure](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE]
> nome Hello dell'hub IoT deve essere globalmente univoco. È possibile creare una sola edizione F1 dell'hub IoT di Azure nell'ambito della propria sottoscrizione di Azure.

## <a name="register-your-device-in-your-iot-hub"></a>Registrare il dispositivo nell'hub IoT

Ogni dispositivo che invia l'hub IoT tooyour messaggi e riceve messaggi dall'hub IoT deve essere registrato con un ID univoco.
Registrare il dispositivo nell'hub IoT eseguendo questo comando:

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a>Riepilogo

È stato creato un hub IoT e il dispositivo logico è stato registrato con un'identità del dispositivo nell'hub IoT. Si è pronti toolearn tooconfigure ed eseguire un gateway applicazione toosend campionamento dall'hub IoT tooyour dispositivo fisico hello di cloud.

## <a name="next-steps"></a>Passaggi successivi
[Configurare ed eseguire un'app di esempio BLE](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)