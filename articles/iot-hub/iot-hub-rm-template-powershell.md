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
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a><span data-ttu-id="030d8-103">Creare un hub IoT usando un modello di Azure Resource Manager (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="030d8-103">Create an IoT hub using Azure Resource Manager template (PowerShell)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="030d8-104">È possibile utilizzare Gestione risorse di Azure toocreate e gestire hub IoT di Azure a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="030d8-104">You can use Azure Resource Manager toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="030d8-105">In questa esercitazione illustra come toouse un toocreate modello di gestione risorse di Azure un hub IoT con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="030d8-105">This tutorial shows you how toouse an Azure Resource Manager template toocreate an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="030d8-106">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager e classico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="030d8-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="030d8-107">In questo articolo viene illustrato l'utilizzo del modello di distribuzione Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="030d8-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="030d8-108">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="030d8-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="030d8-109">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="030d8-109">An active Azure account.</span></span> <br/><span data-ttu-id="030d8-110">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="030d8-110">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="030d8-111">[Azure PowerShell 1.0][lnk-powershell-install] o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="030d8-111">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

> [!TIP]
> <span data-ttu-id="030d8-112">articolo Hello [tramite Azure PowerShell con Gestione risorse di Azure] [ lnk-powershell-arm] fornisce ulteriori informazioni su come toouse PowerShell e Azure Resource Manager modelli toocreate Azure le risorse.</span><span class="sxs-lookup"><span data-stu-id="030d8-112">hello article [Using Azure PowerShell with Azure Resource Manager][lnk-powershell-arm] provides more information about how toouse PowerShell and Azure Resource Manager templates toocreate Azure resources.</span></span>

## <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="030d8-113">Connettersi tooyour sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="030d8-113">Connect tooyour Azure subscription</span></span>

<span data-ttu-id="030d8-114">In un prompt dei comandi di PowerShell, immettere hello successivo comando toosign in tooyour sottoscrizione di Azure:</span><span class="sxs-lookup"><span data-stu-id="030d8-114">In a PowerShell command prompt, enter hello following command toosign in tooyour Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="030d8-115">Se si dispone di più sottoscrizioni di Azure, consente l'accesso tooall accesso tooAzure hello le sottoscrizioni di Azure associate con le credenziali.</span><span class="sxs-lookup"><span data-stu-id="030d8-115">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="030d8-116">Utilizzare hello toolist hello Azure sottoscrizioni disponibili per l'utente toouse comando seguente:</span><span class="sxs-lookup"><span data-stu-id="030d8-116">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="030d8-117">Utilizzare hello seguente sottoscrizione tooselect comando che si desidera toouse toorun hello comandi toocreate l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="030d8-117">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="030d8-118">È possibile utilizzare il nome di sottoscrizione hello o ID dall'output di hello del comando precedente hello:</span><span class="sxs-lookup"><span data-stu-id="030d8-118">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

<span data-ttu-id="030d8-119">È possibile utilizzare hello toodiscover comandi in cui è possibile distribuire un hub IoT e hello attualmente supportate le versioni dell'API seguente:</span><span class="sxs-lookup"><span data-stu-id="030d8-119">You can use hello following commands toodiscover where you can deploy an IoT hub and hello currently supported API versions:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

<span data-ttu-id="030d8-120">Creare un toocontain gruppo di risorse hub IoT utilizzando hello comando in uno dei percorsi di hello è supportato per l'IoT Hub seguente.</span><span class="sxs-lookup"><span data-stu-id="030d8-120">Create a resource group toocontain your IoT hub using hello following command in one of hello supported locations for IoT Hub.</span></span> <span data-ttu-id="030d8-121">In questo esempio viene creato un gruppo di risorse denominato **MyIoTRG1**:</span><span class="sxs-lookup"><span data-stu-id="030d8-121">This example creates a resource group called **MyIoTRG1**:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-toocreate-an-iot-hub"></a><span data-ttu-id="030d8-122">Inviare un toocreate modello un hub IoT</span><span class="sxs-lookup"><span data-stu-id="030d8-122">Submit a template toocreate an IoT hub</span></span>

<span data-ttu-id="030d8-123">Utilizzare un toocreate modello JSON un hub IoT nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="030d8-123">Use a JSON template toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="030d8-124">È anche possibile utilizzare un Azure Resource Manager modello toomake modifiche tooan IoT hub esistente.</span><span class="sxs-lookup"><span data-stu-id="030d8-124">You can also use an Azure Resource Manager template toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="030d8-125">Utilizzare un toocreate editor di testo un modello di gestione risorse di Azure denominato **template.json** con hello in seguito toocreate definizione di risorsa di un nuovo hub IoT standard.</span><span class="sxs-lookup"><span data-stu-id="030d8-125">Use a text editor toocreate an Azure Resource Manager template called **template.json** with hello following resource definition toocreate a new standard IoT hub.</span></span> <span data-ttu-id="030d8-126">Questo esempio aggiunge hello IoT Hub hello **Stati Uniti orientali** area, consente di creare due gruppi di consumer (**cg1** e **cg2**) su endpoint compatibili con Hub eventi hello e utilizza hello **2016-02-03** versione API.</span><span class="sxs-lookup"><span data-stu-id="030d8-126">This example adds hello IoT Hub in hello **East US** region, creates two consumer groups (**cg1** and **cg2**) on hello Event Hub-compatible endpoint, and uses hello **2016-02-03** API version.</span></span> <span data-ttu-id="030d8-127">Questo modello prevede inoltre si toopass nel nome dell'hub IoT hello come un parametro denominato **hubName**.</span><span class="sxs-lookup"><span data-stu-id="030d8-127">This template also expects you toopass in hello IoT hub name as a parameter called **hubName**.</span></span> <span data-ttu-id="030d8-128">Per l'elenco corrente di hello di percorsi che supportano IoT Hub vedere [stato Azure][lnk-status].</span><span class="sxs-lookup"><span data-stu-id="030d8-128">For hello current list of locations that support IoT Hub see [Azure Status][lnk-status].</span></span>

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

2. <span data-ttu-id="030d8-129">Salvare file di modello hello Azure Resource Manager nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="030d8-129">Save hello Azure Resource Manager template file on your local machine.</span></span> <span data-ttu-id="030d8-130">Questo esempio presuppone che il file venga salvato in una cartella denominata **c:\templates**.</span><span class="sxs-lookup"><span data-stu-id="030d8-130">This example assumes you save it in a folder called **c:\templates**.</span></span>

3. <span data-ttu-id="030d8-131">Eseguire hello toodeploy comando dopo il nuovo hub IoT, passando il nome di hello dell'hub IoT come parametro.</span><span class="sxs-lookup"><span data-stu-id="030d8-131">Run hello following command toodeploy your new IoT hub, passing hello name of your IoT hub as a parameter.</span></span> <span data-ttu-id="030d8-132">In questo esempio, è il nome di hello dell'hub IoT hello `abcmyiothub`.</span><span class="sxs-lookup"><span data-stu-id="030d8-132">In this example, hello name of hello IoT hub is `abcmyiothub`.</span></span> <span data-ttu-id="030d8-133">nome Hello dell'hub IoT deve essere globalmente univoco:</span><span class="sxs-lookup"><span data-stu-id="030d8-133">hello name of your IoT hub must be globally unique:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. <span data-ttu-id="030d8-134">output di Hello Visualizza chiavi di hello per l'hub IoT hello che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="030d8-134">hello output displays hello keys for hello IoT hub you created.</span></span>

5. <span data-ttu-id="030d8-135">l'applicazione aggiunta tooverify hello nuovo hub IoT, visitare hello [portale di Azure] [ lnk-azure-portal] e visualizzare l'elenco delle risorse.</span><span class="sxs-lookup"><span data-stu-id="030d8-135">tooverify your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="030d8-136">In alternativa, utilizzare hello **Get-AzureRmResource** cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="030d8-136">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="030d8-137">Questa applicazione di esempio aggiunge un hub IoT Standard S1 che viene addebitato.</span><span class="sxs-lookup"><span data-stu-id="030d8-137">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="030d8-138">È possibile eliminare l'hub IoT hello tramite hello [portale di Azure] [ lnk-azure-portal] o utilizzando hello **Remove-AzureRmResource** cmdlet PowerShell dopo aver terminato.</span><span class="sxs-lookup"><span data-stu-id="030d8-138">You can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="030d8-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="030d8-139">Next steps</span></span>

<span data-ttu-id="030d8-140">Dopo aver distribuito un hub IoT con un modello di gestione risorse di Azure PowerShell, è opportuno tooexplore ulteriormente:</span><span class="sxs-lookup"><span data-stu-id="030d8-140">Now you have deployed an IoT hub using an Azure Resource Manager template with PowerShell, you may want tooexplore further:</span></span>

* <span data-ttu-id="030d8-141">Leggere informazioni sulle funzionalità di hello di hello [il provider di risorse IoT Hub API REST][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="030d8-141">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="030d8-142">Lettura [Panoramica di gestione risorse di Azure] [ lnk-azure-rm-overview] toolearn ulteriori informazioni sulla funzionalità hello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="030d8-142">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="030d8-143">toolearn più sullo sviluppo per l'IoT Hub, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="030d8-143">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="030d8-144">[Introduzione tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="030d8-144">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="030d8-145">[Azure IoT SDKs][lnk-sdks] (SDK di IoT di Azure)</span><span class="sxs-lookup"><span data-stu-id="030d8-145">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="030d8-146">toofurther esplorare le funzionalità di hello di IoT Hub, vedere:</span><span class="sxs-lookup"><span data-stu-id="030d8-146">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="030d8-147">[Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="030d8-147">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
