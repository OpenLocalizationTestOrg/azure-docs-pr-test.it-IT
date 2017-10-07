---
title: aaaCreate un IoT Hub di Azure utilizzando un modello (PowerShell) | Documenti Microsoft
description: Come toouse un toocreate modello di gestione risorse di Azure un IoT Hub con PowerShell.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7eade855-c289-4ffb-b5ef-02be8c5f670f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: e98ff5e898200cd727b9326fb3df393e43b021e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a>Creare un hub IoT usando un modello di Azure Resource Manager (PowerShell)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

È possibile utilizzare Gestione risorse di Azure toocreate e gestire hub IoT di Azure a livello di codice. In questa esercitazione illustra come toouse un toocreate modello di gestione risorse di Azure un hub IoT con PowerShell.

> [!NOTE]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager e classico](../azure-resource-manager/resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione Azure Resource Manager hello.

toocomplete questa esercitazione, è necessario hello seguenti:

* Un account Azure attivo. <br/>Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.
* [Azure PowerShell 1.0][lnk-powershell-install] o versione successiva.

> [!TIP]
> articolo Hello [tramite Azure PowerShell con Gestione risorse di Azure] [ lnk-powershell-arm] fornisce ulteriori informazioni su come toouse PowerShell e Azure Resource Manager modelli toocreate Azure le risorse.

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

È possibile utilizzare hello toodiscover comandi in cui è possibile distribuire un hub IoT e hello attualmente supportate le versioni dell'API seguente:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

Creare un toocontain gruppo di risorse hub IoT utilizzando hello comando in uno dei percorsi di hello è supportato per l'IoT Hub seguente. In questo esempio viene creato un gruppo di risorse denominato **MyIoTRG1**:

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-toocreate-an-iot-hub"></a>Inviare un toocreate modello un hub IoT

Utilizzare un toocreate modello JSON un hub IoT nel gruppo di risorse. È anche possibile utilizzare un Azure Resource Manager modello toomake modifiche tooan IoT hub esistente.

1. Utilizzare un toocreate editor di testo un modello di gestione risorse di Azure denominato **template.json** con hello in seguito toocreate definizione di risorsa di un nuovo hub IoT standard. Questo esempio aggiunge hello IoT Hub hello **Stati Uniti orientali** area, consente di creare due gruppi di consumer (**cg1** e **cg2**) su endpoint compatibili con Hub eventi hello e utilizza hello **2016-02-03** versione API. Questo modello prevede inoltre si toopass nel nome dell'hub IoT hello come un parametro denominato **hubName**. Per l'elenco corrente di hello di percorsi che supportano IoT Hub vedere [stato Azure][lnk-status].

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg1')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg2')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

2. Salvare file di modello hello Azure Resource Manager nel computer locale. Questo esempio presuppone che il file venga salvato in una cartella denominata **c:\templates**.

3. Eseguire hello toodeploy comando dopo il nuovo hub IoT, passando il nome di hello dell'hub IoT come parametro. In questo esempio, è il nome di hello dell'hub IoT hello `abcmyiothub`. nome Hello dell'hub IoT deve essere globalmente univoco:

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. output di Hello Visualizza chiavi di hello per l'hub IoT hello che è stato creato.

5. l'applicazione aggiunta tooverify hello nuovo hub IoT, visitare hello [portale di Azure] [ lnk-azure-portal] e visualizzare l'elenco delle risorse. In alternativa, utilizzare hello **Get-AzureRmResource** cmdlet di PowerShell.

> [!NOTE]
> Questa applicazione di esempio aggiunge un hub IoT Standard S1 che viene addebitato. È possibile eliminare l'hub IoT hello tramite hello [portale di Azure] [ lnk-azure-portal] o utilizzando hello **Remove-AzureRmResource** cmdlet PowerShell dopo aver terminato.

## <a name="next-steps"></a>Passaggi successivi

Dopo aver distribuito un hub IoT con un modello di gestione risorse di Azure PowerShell, è opportuno tooexplore ulteriormente:

* Leggere informazioni sulle funzionalità di hello di hello [il provider di risorse IoT Hub API REST][lnk-rest-api].
* Lettura [Panoramica di gestione risorse di Azure] [ lnk-azure-rm-overview] toolearn ulteriori informazioni sulla funzionalità hello di gestione risorse di Azure.

toolearn più sullo sviluppo per l'IoT Hub, vedere hello seguenti articoli:

* [Introduzione tooC SDK][lnk-c-sdk]
* [Azure IoT SDKs][lnk-sdks] (SDK di IoT di Azure)

toofurther esplorare le funzionalità di hello di IoT Hub, vedere:

* [Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: /powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-powershell-arm]: ../azure-resource-manager/powershell-azure-resource-manager.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
