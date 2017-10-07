---
title: un IoT Hub di Azure mediante un cmdlet PowerShell aaaCreate | Documenti Microsoft
description: Come toouse un toocreate di cmdlet di PowerShell un hub IoT.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 005cd8d48eb39d2e8b1bfb9ef84330d4aae4658f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-new-azurermiothub-cmdlet"></a>Creazione di un hub IoT utilizzando il cmdlet New-AzureRmIotHub hello

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Introduzione

È possibile utilizzare toocreate cmdlet PowerShell di Azure e gestire hub IoT di Azure. In questa esercitazione illustra come toocreate un hub IoT con PowerShell.

> [!NOTE]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager e classico](../azure-resource-manager/resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione Azure Resource Manager hello.

toocomplete questa esercitazione, è necessario hello seguenti:

* Un account Azure attivo. <br/>Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.
* [Cmdlet di Azure PowerShell][lnk-powershell-install].

## <a name="connect-tooyour-azure-subscription"></a>Connettersi tooyour sottoscrizione di Azure
In un prompt dei comandi di PowerShell, immettere hello successivo comando toosign in tooyour sottoscrizione di Azure:

```powershell
Login-AzureRmAccount
```

Se si dispone di più sottoscrizioni di Azure, consente l'accesso tooall accesso tooAzure hello le sottoscrizioni di Azure associate con le credenziali. Utilizzare hello toolist hello Azure sottoscrizioni disponibili per l'utente toouse comando seguente:

```powershell
Get-AzureRMSubscription
```

Utilizzare hello seguente sottoscrizione tooselect comando che si desidera toouse toorun hello comandi toocreate l'hub IoT. È possibile utilizzare il nome di sottoscrizione hello o ID dall'output di hello del comando precedente hello:

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

## <a name="create-resource-group"></a>Creare un gruppo di risorse

È necessario un toodeploy gruppo di risorse un hub IoT. È possibile usare un gruppo di risorse esistente o crearne uno nuovo.

È possibile utilizzare hello comando toodiscover hello posizioni in cui è possibile distribuire un hub IoT seguenti:

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

toocreate un gruppo di risorse per l'hub IoT in uno dei percorsi di hello è supportato per l'IoT Hub, utilizzare hello comando seguente. In questo esempio viene creato un gruppo di risorse denominato **MyIoTRG1** in hello **Stati Uniti orientali** area:

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a>Creare un hub IoT

toocreate un hub IoT nel gruppo di risorse hello creato nel passaggio precedente hello, utilizzare hello comando seguente. Questo esempio viene creato un **S1** hub chiamato **MyTestIoTHub** in hello **Stati Uniti orientali** area:

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

nome Hello dell'hub IoT hello deve essere univoco.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


È possibile elencare tutti gli hub IoT di hello nella sottoscrizione tramite hello comando seguente:

```powershell
Get-AzureRmIotHub
```

Nell'esempio precedente Hello aggiunta S1 Standard IoT Hub per il quale verrà addebitato. È possibile eliminare l'hub IoT hello utilizzando hello comando seguente:

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

In alternativa, è possibile rimuovere un gruppo di risorse e tutti hello risorse contenute utilizzando hello comando seguente:

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a>Passaggi successivi

Dopo aver distribuito un hub IoT utilizzando un cmdlet di PowerShell, è opportuno tooexplore ulteriormente:

* Individuare altri [cmdlet di PowerShell da usare con l'hub IoT][lnk-iothub-cmdlets].
* Leggere informazioni sulle funzionalità di hello di hello [il provider di risorse IoT Hub API REST][lnk-rest-api].

toolearn più sullo sviluppo per l'IoT Hub, vedere hello seguenti articoli:

* [Introduzione tooC SDK][lnk-c-sdk]
* [Azure IoT SDKs][lnk-sdks] (SDK di IoT di Azure)

toofurther esplorare le funzionalità di hello di IoT Hub, vedere:

* [Simulazione di un dispositivo con IoT Edge][lnk-iotedge]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
