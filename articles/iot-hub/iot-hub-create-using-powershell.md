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
# <a name="create-an-iot-hub-using-hello-new-azurermiothub-cmdlet"></a><span data-ttu-id="7284e-103">Creazione di un hub IoT utilizzando il cmdlet New-AzureRmIotHub hello</span><span class="sxs-lookup"><span data-stu-id="7284e-103">Create an IoT hub using hello New-AzureRmIotHub cmdlet</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="7284e-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="7284e-104">Introduction</span></span>

<span data-ttu-id="7284e-105">È possibile utilizzare toocreate cmdlet PowerShell di Azure e gestire hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="7284e-105">You can use Azure PowerShell cmdlets toocreate and manage Azure IoT hubs.</span></span> <span data-ttu-id="7284e-106">In questa esercitazione illustra come toocreate un hub IoT con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7284e-106">This tutorial shows you how toocreate an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="7284e-107">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager e classico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7284e-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7284e-108">In questo articolo viene illustrato l'utilizzo del modello di distribuzione Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="7284e-108">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="7284e-109">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="7284e-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="7284e-110">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="7284e-110">An active Azure account.</span></span> <br/><span data-ttu-id="7284e-111">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="7284e-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="7284e-112">[Cmdlet di Azure PowerShell][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="7284e-112">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>

## <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="7284e-113">Connettersi tooyour sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="7284e-113">Connect tooyour Azure subscription</span></span>
<span data-ttu-id="7284e-114">In un prompt dei comandi di PowerShell, immettere hello successivo comando toosign in tooyour sottoscrizione di Azure:</span><span class="sxs-lookup"><span data-stu-id="7284e-114">In a PowerShell command prompt, enter hello following command toosign in tooyour Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="7284e-115">Se si dispone di più sottoscrizioni di Azure, consente l'accesso tooall accesso tooAzure hello le sottoscrizioni di Azure associate con le credenziali.</span><span class="sxs-lookup"><span data-stu-id="7284e-115">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="7284e-116">Utilizzare hello toolist hello Azure sottoscrizioni disponibili per l'utente toouse comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7284e-116">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="7284e-117">Utilizzare hello seguente sottoscrizione tooselect comando che si desidera toouse toorun hello comandi toocreate l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7284e-117">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="7284e-118">È possibile utilizzare il nome di sottoscrizione hello o ID dall'output di hello del comando precedente hello:</span><span class="sxs-lookup"><span data-stu-id="7284e-118">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

## <a name="create-resource-group"></a><span data-ttu-id="7284e-119">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="7284e-119">Create resource group</span></span>

<span data-ttu-id="7284e-120">È necessario un toodeploy gruppo di risorse un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7284e-120">You need a resource group toodeploy an IoT hub.</span></span> <span data-ttu-id="7284e-121">È possibile usare un gruppo di risorse esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="7284e-121">You can use an existing resource group or create a new one.</span></span>

<span data-ttu-id="7284e-122">È possibile utilizzare hello comando toodiscover hello posizioni in cui è possibile distribuire un hub IoT seguenti:</span><span class="sxs-lookup"><span data-stu-id="7284e-122">You can use hello following command toodiscover hello locations where you can deploy an IoT hub:</span></span>

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

<span data-ttu-id="7284e-123">toocreate un gruppo di risorse per l'hub IoT in uno dei percorsi di hello è supportato per l'IoT Hub, utilizzare hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="7284e-123">toocreate a resource group for your IoT hub in one of hello supported locations for IoT Hub, use hello following command.</span></span> <span data-ttu-id="7284e-124">In questo esempio viene creato un gruppo di risorse denominato **MyIoTRG1** in hello **Stati Uniti orientali** area:</span><span class="sxs-lookup"><span data-stu-id="7284e-124">This example creates a resource group called **MyIoTRG1** in hello **East US** region:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a><span data-ttu-id="7284e-125">Creare un hub IoT</span><span class="sxs-lookup"><span data-stu-id="7284e-125">Create an IoT hub</span></span>

<span data-ttu-id="7284e-126">toocreate un hub IoT nel gruppo di risorse hello creato nel passaggio precedente hello, utilizzare hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="7284e-126">toocreate an IoT hub in hello resource group you created in hello previous step, use hello following command.</span></span> <span data-ttu-id="7284e-127">Questo esempio viene creato un **S1** hub chiamato **MyTestIoTHub** in hello **Stati Uniti orientali** area:</span><span class="sxs-lookup"><span data-stu-id="7284e-127">This example creates an **S1** hub called **MyTestIoTHub** in hello **East US** region:</span></span>

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

<span data-ttu-id="7284e-128">nome Hello dell'hub IoT hello deve essere univoco.</span><span class="sxs-lookup"><span data-stu-id="7284e-128">hello name of hello IoT hub must be unique.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


<span data-ttu-id="7284e-129">È possibile elencare tutti gli hub IoT di hello nella sottoscrizione tramite hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7284e-129">You can list all hello IoT hubs in your subscription using hello following command:</span></span>

```powershell
Get-AzureRmIotHub
```

<span data-ttu-id="7284e-130">Nell'esempio precedente Hello aggiunta S1 Standard IoT Hub per il quale verrà addebitato.</span><span class="sxs-lookup"><span data-stu-id="7284e-130">hello previous example adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="7284e-131">È possibile eliminare l'hub IoT hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7284e-131">You can delete hello IoT hub using hello following command:</span></span>

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

<span data-ttu-id="7284e-132">In alternativa, è possibile rimuovere un gruppo di risorse e tutti hello risorse contenute utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7284e-132">Alternatively, you can remove a resource group and all hello resources it contains using hello following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a><span data-ttu-id="7284e-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7284e-133">Next steps</span></span>

<span data-ttu-id="7284e-134">Dopo aver distribuito un hub IoT utilizzando un cmdlet di PowerShell, è opportuno tooexplore ulteriormente:</span><span class="sxs-lookup"><span data-stu-id="7284e-134">Now you have deployed an IoT hub using a PowerShell cmdlet, you may want tooexplore further:</span></span>

* <span data-ttu-id="7284e-135">Individuare altri [cmdlet di PowerShell da usare con l'hub IoT][lnk-iothub-cmdlets].</span><span class="sxs-lookup"><span data-stu-id="7284e-135">Discover other [PowerShell cmdlets for working with your IoT hub][lnk-iothub-cmdlets].</span></span>
* <span data-ttu-id="7284e-136">Leggere informazioni sulle funzionalità di hello di hello [il provider di risorse IoT Hub API REST][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="7284e-136">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>

<span data-ttu-id="7284e-137">toolearn più sullo sviluppo per l'IoT Hub, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="7284e-137">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="7284e-138">[Introduzione tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="7284e-138">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="7284e-139">[Azure IoT SDKs][lnk-sdks] (SDK di IoT di Azure)</span><span class="sxs-lookup"><span data-stu-id="7284e-139">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="7284e-140">toofurther esplorare le funzionalità di hello di IoT Hub, vedere:</span><span class="sxs-lookup"><span data-stu-id="7284e-140">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="7284e-141">[Simulazione di un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="7284e-141">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
