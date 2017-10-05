---
title: Creare un hub IoT di Azure con un cmdlet di PowerShell | Microsoft Docs
description: Procedura per usare un cmdlet di PowerShell per creare un hub IoT.
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
ms.openlocfilehash: 02227adeb8a9a7463506efa44ddc2977f8aae65a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-iot-hub-using-the-new-azurermiothub-cmdlet"></a><span data-ttu-id="9d855-103">Creare un hub IoT usando il cmdlet New-AzureRmIotHub</span><span class="sxs-lookup"><span data-stu-id="9d855-103">Create an IoT hub using the New-AzureRmIotHub cmdlet</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="9d855-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="9d855-104">Introduction</span></span>

<span data-ttu-id="9d855-105">È possibile usare i cmdlet di Azure PowerShell per creare e gestire hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="9d855-105">You can use Azure PowerShell cmdlets to create and manage Azure IoT hubs.</span></span> <span data-ttu-id="9d855-106">In questa esercitazione viene illustrato come creare un hub IoT con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9d855-106">This tutorial shows you how to create an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="9d855-107">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager e classico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9d855-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9d855-108">In questo articolo viene illustrato l'uso del modello di distribuzione Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9d855-108">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="9d855-109">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9d855-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="9d855-110">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="9d855-110">An active Azure account.</span></span> <br/><span data-ttu-id="9d855-111">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="9d855-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="9d855-112">[Cmdlet di Azure PowerShell][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="9d855-112">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>

## <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="9d855-113">Connettersi alla sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="9d855-113">Connect to your Azure subscription</span></span>
<span data-ttu-id="9d855-114">In un prompt dei comandi di PowerShell, immettere il comando seguente per accedere alla sottoscrizione di Azure:</span><span class="sxs-lookup"><span data-stu-id="9d855-114">In a PowerShell command prompt, enter the following command to sign in to your Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="9d855-115">Se si usano più sottoscrizioni Azure e si esegue l'accesso ad Azure, è possibile accedere a tutte le sottoscrizioni di Azure associate alle credenziali.</span><span class="sxs-lookup"><span data-stu-id="9d855-115">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="9d855-116">Usare il comando seguente per elencare gli account Azure che è possibile usare:</span><span class="sxs-lookup"><span data-stu-id="9d855-116">Use the following command to list the Azure subscriptions available for you to use:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="9d855-117">Usare il comando seguente per selezionare la sottoscrizione che si vuole usare per eseguire i comandi per creare l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9d855-117">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="9d855-118">È possibile usare il nome o l'ID della sottoscrizione dall'output del comando precedente:</span><span class="sxs-lookup"><span data-stu-id="9d855-118">You can use either the subscription name or ID from the output of the previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

## <a name="create-resource-group"></a><span data-ttu-id="9d855-119">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="9d855-119">Create resource group</span></span>

<span data-ttu-id="9d855-120">Per la distribuzione di un hub IoT è necessario un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="9d855-120">You need a resource group to deploy an IoT hub.</span></span> <span data-ttu-id="9d855-121">È possibile usare un gruppo di risorse esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="9d855-121">You can use an existing resource group or create a new one.</span></span>

<span data-ttu-id="9d855-122">È possibile usare il comando seguente per individuare le località in cui è possibile distribuire un hub IoT:</span><span class="sxs-lookup"><span data-stu-id="9d855-122">You can use the following command to discover the locations where you can deploy an IoT hub:</span></span>

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

<span data-ttu-id="9d855-123">Per creare un gruppo di risorse per l'hub IoT in una delle località supportate per l'hub IoT usare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="9d855-123">To create a resource group for your IoT hub in one of the supported locations for IoT Hub, use the following command.</span></span> <span data-ttu-id="9d855-124">In questo esempio viene creato un gruppo di risorse denominato **MyIoTRG1** nell'area degli **Stati Uniti orientali**:</span><span class="sxs-lookup"><span data-stu-id="9d855-124">This example creates a resource group called **MyIoTRG1** in the **East US** region:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a><span data-ttu-id="9d855-125">Creare un hub IoT</span><span class="sxs-lookup"><span data-stu-id="9d855-125">Create an IoT hub</span></span>

<span data-ttu-id="9d855-126">Per creare un hub IoT nel gruppo di risorse creato nel passaggio precedente, usare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="9d855-126">To create an IoT hub in the resource group you created in the previous step, use the following command.</span></span> <span data-ttu-id="9d855-127">In questo esempio viene creato un hub **S1** denominato **MyTestIoTHub** nell'area degli **Stati Uniti orientali**:</span><span class="sxs-lookup"><span data-stu-id="9d855-127">This example creates an **S1** hub called **MyTestIoTHub** in the **East US** region:</span></span>

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

<span data-ttu-id="9d855-128">Il nome dell'hub IoT deve essere univoco.</span><span class="sxs-lookup"><span data-stu-id="9d855-128">The name of the IoT hub must be unique.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


<span data-ttu-id="9d855-129">È possibile elencare tutti gli hub IoT nella sottoscrizione con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9d855-129">You can list all the IoT hubs in your subscription using the following command:</span></span>

```powershell
Get-AzureRmIotHub
```

<span data-ttu-id="9d855-130">Nell'esempio precedente viene aggiunto un hub IoT Standard S1 che viene addebitato.</span><span class="sxs-lookup"><span data-stu-id="9d855-130">The previous example adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="9d855-131">È possibile eliminare l'hub IoT con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9d855-131">You can delete the IoT hub using the following command:</span></span>

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

<span data-ttu-id="9d855-132">In alternativa, è possibile rimuovere un gruppo di risorse e tutte le risorse che contiene con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9d855-132">Alternatively, you can remove a resource group and all the resources it contains using the following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a><span data-ttu-id="9d855-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9d855-133">Next steps</span></span>

<span data-ttu-id="9d855-134">Dopo aver distribuito un hub IoT mediante il cmdlet di PowerShell, può essere opportuno ottenere informazioni più dettagliate:</span><span class="sxs-lookup"><span data-stu-id="9d855-134">Now you have deployed an IoT hub using a PowerShell cmdlet, you may want to explore further:</span></span>

* <span data-ttu-id="9d855-135">Individuare altri [cmdlet di PowerShell da usare con l'hub IoT][lnk-iothub-cmdlets].</span><span class="sxs-lookup"><span data-stu-id="9d855-135">Discover other [PowerShell cmdlets for working with your IoT hub][lnk-iothub-cmdlets].</span></span>
* <span data-ttu-id="9d855-136">Informazioni sulle funzionalità dell'[API REST del provider di risorse dell'hub IoT][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="9d855-136">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>

<span data-ttu-id="9d855-137">Per altre informazioni sulle attività di sviluppo per l'hub IoT, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="9d855-137">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="9d855-138">[Introduzione a C SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="9d855-138">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="9d855-139">[Azure IoT SDKs][lnk-sdks] (SDK di IoT di Azure)</span><span class="sxs-lookup"><span data-stu-id="9d855-139">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="9d855-140">Per altre informazioni sulle funzionalità dell'hub IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="9d855-140">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="9d855-141">[Simulazione di un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="9d855-141">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
