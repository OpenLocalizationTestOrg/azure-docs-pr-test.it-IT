---
title: Creare un hub IoT di Azure con un modello (PowerShell) | Documentazione Microsoft
description: Come usare un modello di Azure Resource Manager per creare un hub IoT con PowerShell.
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
ms.openlocfilehash: f83fac6cffc9e58582417324a4348ca3b6220f0c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a><span data-ttu-id="0ab0e-103">Creare un hub IoT usando un modello di Azure Resource Manager (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="0ab0e-103">Create an IoT hub using Azure Resource Manager template (PowerShell)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="0ab0e-104">È possibile utilizzare Gestione risorse di Azure per creare e gestire hub IoT di Azure a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="0ab0e-104">You can use Azure Resource Manager to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="0ab0e-105">In questa esercitazione viene illustrato come usare un modello di Azure Resource Manager per creare un hub IoT con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ab0e-105">This tutorial shows you how to use an Azure Resource Manager template to create an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="0ab0e-106">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager e classico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0ab0e-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0ab0e-107">In questo articolo viene illustrato l'uso del modello di distribuzione Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0ab0e-107">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="0ab0e-108">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0ab0e-108">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="0ab0e-109">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="0ab0e-109">An active Azure account.</span></span> <br/><span data-ttu-id="0ab0e-110">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="0ab0e-110">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="0ab0e-111">[Azure PowerShell 1.0][lnk-powershell-install] o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="0ab0e-111">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

> [!TIP]
> <span data-ttu-id="0ab0e-112">Per altre informazioni su come usare PowerShell e i modelli di Azure Resource Manager per creare risorse di Azure, vedere [Using Azure PowerShell with Azure Resource Manager][lnk-powershell-arm] (Uso di Azure PowerShell con Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="0ab0e-112">The article [Using Azure PowerShell with Azure Resource Manager][lnk-powershell-arm] provides more information about how to use PowerShell and Azure Resource Manager templates to create Azure resources.</span></span>

## <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="0ab0e-113">Connettersi alla sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="0ab0e-113">Connect to your Azure subscription</span></span>

<span data-ttu-id="0ab0e-114">In un prompt dei comandi di PowerShell, immettere il comando seguente per accedere alla sottoscrizione di Azure:</span><span class="sxs-lookup"><span data-stu-id="0ab0e-114">In a PowerShell command prompt, enter the following command to sign in to your Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="0ab0e-115">Se si usano più sottoscrizioni Azure e si esegue l'accesso ad Azure, è possibile accedere a tutte le sottoscrizioni di Azure associate alle credenziali.</span><span class="sxs-lookup"><span data-stu-id="0ab0e-115">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="0ab0e-116">Usare il comando seguente per elencare gli account Azure che è possibile usare:</span><span class="sxs-lookup"><span data-stu-id="0ab0e-116">Use the following command to list the Azure subscriptions available for you to use:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="0ab0e-117">Usare il comando seguente per selezionare la sottoscrizione che si vuole usare per eseguire i comandi per creare l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0ab0e-117">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="0ab0e-118">È possibile usare il nome o l'ID della sottoscrizione dall'output del comando precedente:</span><span class="sxs-lookup"><span data-stu-id="0ab0e-118">You can use either the subscription name or ID from the output of the previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

<span data-ttu-id="0ab0e-119">È possibile usare i comandi seguenti per individuare dove è possibile distribuire un hub IoT e le versioni API attualmente supportate:</span><span class="sxs-lookup"><span data-stu-id="0ab0e-119">You can use the following commands to discover where you can deploy an IoT hub and the currently supported API versions:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

<span data-ttu-id="0ab0e-120">Creare un gruppo di risorse per contenere l'hub IoT usando il comando seguente in una delle località supportate per l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0ab0e-120">Create a resource group to contain your IoT hub using the following command in one of the supported locations for IoT Hub.</span></span> <span data-ttu-id="0ab0e-121">In questo esempio viene creato un gruppo di risorse denominato **MyIoTRG1**:</span><span class="sxs-lookup"><span data-stu-id="0ab0e-121">This example creates a resource group called **MyIoTRG1**:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-to-create-an-iot-hub"></a><span data-ttu-id="0ab0e-122">Inviare un modello per creare un hub IoT</span><span class="sxs-lookup"><span data-stu-id="0ab0e-122">Submit a template to create an IoT hub</span></span>

<span data-ttu-id="0ab0e-123">Utilizzare un modello JSON per creare un hub IoT nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="0ab0e-123">Use a JSON template to create an IoT hub in your resource group.</span></span> <span data-ttu-id="0ab0e-124">È anche possibile usare un modello di Azure Resource Manager per apportare modifiche a un hub IoT esistente.</span><span class="sxs-lookup"><span data-stu-id="0ab0e-124">You can also use an Azure Resource Manager template to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="0ab0e-125">Usare un editor di testo per creare un modello di Azure Resource Manager denominato **template.json** con la definizione di risorsa seguente per creare un nuovo hub IoT standard.</span><span class="sxs-lookup"><span data-stu-id="0ab0e-125">Use a text editor to create an Azure Resource Manager template called **template.json** with the following resource definition to create a new standard IoT hub.</span></span> <span data-ttu-id="0ab0e-126">In questo esempio l'hub IoT viene aggiunto all'area **Stati Uniti orientali**, vengono creati due gruppi di consumer (**cg1** e **cg2**) sull'endpoint compatibile con Hub eventi e viene usata la versione **2016-02-03** dell'API.</span><span class="sxs-lookup"><span data-stu-id="0ab0e-126">This example adds the IoT Hub in the **East US** region, creates two consumer groups (**cg1** and **cg2**) on the Event Hub-compatible endpoint, and uses the **2016-02-03** API version.</span></span> <span data-ttu-id="0ab0e-127">Questo modello prevede anche che il nome dell'hub IoT venga passato come un parametro denominato **hubName**.</span><span class="sxs-lookup"><span data-stu-id="0ab0e-127">This template also expects you to pass in the IoT hub name as a parameter called **hubName**.</span></span> <span data-ttu-id="0ab0e-128">Per un elenco aggiornato delle località in cui è supportato l'hub IoT, vedere lo [Stato di Azure][lnk-status].</span><span class="sxs-lookup"><span data-stu-id="0ab0e-128">For the current list of locations that support IoT Hub see [Azure Status][lnk-status].</span></span>

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

2. <span data-ttu-id="0ab0e-129">Salvare il file del modello di Azure Resource Manager sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="0ab0e-129">Save the Azure Resource Manager template file on your local machine.</span></span> <span data-ttu-id="0ab0e-130">Questo esempio presuppone che il file venga salvato in una cartella denominata **c:\templates**.</span><span class="sxs-lookup"><span data-stu-id="0ab0e-130">This example assumes you save it in a folder called **c:\templates**.</span></span>

3. <span data-ttu-id="0ab0e-131">Eseguire il comando seguente per distribuire il nuovo hub IoT, passando il nome dell'hub IoT come parametro.</span><span class="sxs-lookup"><span data-stu-id="0ab0e-131">Run the following command to deploy your new IoT hub, passing the name of your IoT hub as a parameter.</span></span> <span data-ttu-id="0ab0e-132">In questo esempio, il nome dell'hub IoT è `abcmyiothub`.</span><span class="sxs-lookup"><span data-stu-id="0ab0e-132">In this example, the name of the IoT hub is `abcmyiothub`.</span></span> <span data-ttu-id="0ab0e-133">Il nome dell'hub IoT deve essere globalmente univoco:</span><span class="sxs-lookup"><span data-stu-id="0ab0e-133">The name of your IoT hub must be globally unique:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. <span data-ttu-id="0ab0e-134">L'output visualizza le chiavi per l'hub IoT che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="0ab0e-134">The output displays the keys for the IoT hub you created.</span></span>

5. <span data-ttu-id="0ab0e-135">Per verificare che l'applicazione abbia aggiunto il nuovo hub IoT, visitare il [portale di Azure][lnk-azure-portal] e visualizzare l'elenco delle risorse.</span><span class="sxs-lookup"><span data-stu-id="0ab0e-135">To verify your application added the new IoT hub, visit the [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="0ab0e-136">In alternativa, usare il cmdlet di PowerShell **Get-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="0ab0e-136">Alternatively, use the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="0ab0e-137">Questa applicazione di esempio aggiunge un hub IoT Standard S1 che viene addebitato.</span><span class="sxs-lookup"><span data-stu-id="0ab0e-137">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="0ab0e-138">Al termine è possibile eliminare l'hub IoT usando il [portale di Azure][lnk-azure-portal] o il cmdlet di PowerShell **Remove-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="0ab0e-138">You can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ab0e-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0ab0e-139">Next steps</span></span>

<span data-ttu-id="0ab0e-140">Dopo aver distribuito un hub IoT usando un modello di Azure Resource Manager con PowerShell, può essere opportuno ottenere informazioni più dettagliate:</span><span class="sxs-lookup"><span data-stu-id="0ab0e-140">Now you have deployed an IoT hub using an Azure Resource Manager template with PowerShell, you may want to explore further:</span></span>

* <span data-ttu-id="0ab0e-141">Informazioni sulle funzionalità dell'[API REST del provider di risorse dell'hub IoT][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="0ab0e-141">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="0ab0e-142">Per altre informazioni sulle funzionalità di Azure Resource Manager, vedere la [Panoramica di Azure Resource Manager][lnk-azure-rm-overview].</span><span class="sxs-lookup"><span data-stu-id="0ab0e-142">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="0ab0e-143">Per altre informazioni sulle attività di sviluppo per l'hub IoT, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="0ab0e-143">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="0ab0e-144">[Introduzione a C SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="0ab0e-144">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="0ab0e-145">[Azure IoT SDKs][lnk-sdks] (SDK di IoT di Azure)</span><span class="sxs-lookup"><span data-stu-id="0ab0e-145">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="0ab0e-146">Per altre informazioni sulle funzionalità dell'hub IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="0ab0e-146">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="0ab0e-147">[Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="0ab0e-147">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
