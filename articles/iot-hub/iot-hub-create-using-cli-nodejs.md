---
title: Creare un hub IoT usando l'interfaccia della riga di comando di Azure (azure.js) | Documentazione Microsoft
description: Come creare un hub IoT di Azure usando l'interfaccia della riga di comando di Azure multipiattaforma (azure.js).
services: iot-hub
documentationcenter: .net
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: 46a17831-650c-41d9-b228-445c5bb423d3
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: boltean
ms.openlocfilehash: 5e37c6c5e8625ce446ab203f19f9a8b2f1cd5a46
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-iot-hub-using-the-azure-cli"></a><span data-ttu-id="9107c-103">Creare un hub IoT usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="9107c-103">Create an IoT hub using the Azure CLI</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="9107c-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="9107c-104">Introduction</span></span>

<span data-ttu-id="9107c-105">È possibile usare l'interfaccia della riga di comando di Azure (azure.js) per creare e gestire hub IoT di Azure a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="9107c-105">You can use Azure CLI (azure.js) to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="9107c-106">Questo articolo illustra come usare l'interfaccia della riga di comando di Azure (azure.js) per creare un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9107c-106">This article shows you how to use the Azure CLI (azure.js) to create an IoT hub.</span></span>

<span data-ttu-id="9107c-107">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="9107c-107">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="9107c-108">Interfaccia della riga di comando di Azure (azure.js): interfaccia della riga di comando per i modelli di distribuzione classica e Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9107c-108">Azure CLI (azure.js) – the CLI for the classic and resource management deployment models as described in this article.</span></span>
* <span data-ttu-id="9107c-109">[Interfaccia della riga di comando di Azure 2.0 (az.py)](iot-hub-create-using-cli.md): interfaccia della riga di comando di nuova generazione per il modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9107c-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) - the next generation CLI for the resource management deployment model.</span></span>

<span data-ttu-id="9107c-110">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9107c-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="9107c-111">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="9107c-111">An active Azure account.</span></span> <span data-ttu-id="9107c-112">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="9107c-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="9107c-113">[Interfaccia della riga di comando di Azure 0.10.4][lnk-CLI-install] o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="9107c-113">[Azure CLI 0.10.4][lnk-CLI-install] or later.</span></span> <span data-ttu-id="9107c-114">Se l'interfaccia della riga di comando di Azure è installata, è possibile convalidare la versione corrente al prompt dei comandi inserendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9107c-114">If you already have the Azure CLI installed, you can validate the current version at the command prompt with the following command:</span></span>

```azurecli
azure --version
```

> [!NOTE]
> <span data-ttu-id="9107c-115">Azure offre due modelli di distribuzione per creare e usare le risorse: [modello di distribuzione classica e Azure Resource Manager](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9107c-115">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9107c-116">L'interfaccia della riga di comando di Azure deve essere impostata obbligatoriamente sulla modalità Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="9107c-116">The Azure CLI must be in Azure Resource Manager mode:</span></span>
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="9107c-117">Impostare l'account e la sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="9107c-117">Set your Azure account and subscription</span></span>

1. <span data-ttu-id="9107c-118">Per accedere, digitare il comando seguente al prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="9107c-118">At the command prompt, login by typing the following command:</span></span>

   ```azurecli
    azure login
   ```

   <span data-ttu-id="9107c-119">Per l'autenticazione, usare il browser e il codice suggeriti.</span><span class="sxs-lookup"><span data-stu-id="9107c-119">Use the suggested web browser and code to authenticate.</span></span>
1. <span data-ttu-id="9107c-120">Se si usano più sottoscrizioni Azure e si esegue l'accesso ad Azure, è possibile accedere a tutte le sottoscrizioni di Azure associate alle credenziali.</span><span class="sxs-lookup"><span data-stu-id="9107c-120">If you have multiple Azure subscriptions, connecting to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="9107c-121">Per visualizzare le sottoscrizioni di Azure e identificare quella predefinita, usare il comando:</span><span class="sxs-lookup"><span data-stu-id="9107c-121">You can view the Azure subscriptions, and identify which one is the default, using the command:</span></span>

   ```azurecli
    azure account list
   ```

   <span data-ttu-id="9107c-122">Per impostare il contesto della sottoscrizione in cui eseguire il resto dei comandi usare:</span><span class="sxs-lookup"><span data-stu-id="9107c-122">To set the subscription context under which you want to run the rest of the commands use:</span></span>

   ```azurecli
    azure account set <subscription name>
   ```

1. <span data-ttu-id="9107c-123">Se non si dispone di un gruppo di risorse, è possibile crearne uno denominato **exampleResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="9107c-123">If you do not have a resource group, you can create one named **exampleResourceGroup**:</span></span>

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> <span data-ttu-id="9107c-124">L'articolo [Usare l'interfaccia della riga di comando di Azure per gestire risorse e gruppi di risorse][lnk-CLI-arm] contiene altre informazioni su come usare l'interfaccia della riga di comando di Azure per gestire risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="9107c-124">The article [Use the Azure CLI to manage Azure resources and resource groups][lnk-CLI-arm] provides more information about how to use the Azure CLI to manage Azure resources.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="9107c-125">Creare un hub IoT</span><span class="sxs-lookup"><span data-stu-id="9107c-125">Create an IoT Hub</span></span>

<span data-ttu-id="9107c-126">Parametri obbligatori:</span><span class="sxs-lookup"><span data-stu-id="9107c-126">Required parameters:</span></span>

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* <span data-ttu-id="9107c-127">**resource-group**.</span><span class="sxs-lookup"><span data-stu-id="9107c-127">**resource-group**.</span></span> <span data-ttu-id="9107c-128">Il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="9107c-128">The resource group name.</span></span> <span data-ttu-id="9107c-129">Il formato non distingue tra maiuscole e minuscole, usa caratteri alfanumerici, caratteri di sottolineatura e trattini e ammette una lunghezza da 1 a 64.</span><span class="sxs-lookup"><span data-stu-id="9107c-129">The format is case insensitive alphanumeric, underscore, and hyphen, 1-64 length.</span></span>
* <span data-ttu-id="9107c-130">**name**.</span><span class="sxs-lookup"><span data-stu-id="9107c-130">**name**.</span></span> <span data-ttu-id="9107c-131">Il nome dell'hub IoT da creare.</span><span class="sxs-lookup"><span data-stu-id="9107c-131">The name of the IoT hub to be created.</span></span> <span data-ttu-id="9107c-132">Il formato non distingue tra maiuscole e minuscole, usa caratteri alfanumerici, caratteri di sottolineatura e trattini e ammette una lunghezza da 3 a 50.</span><span class="sxs-lookup"><span data-stu-id="9107c-132">The format is case insensitive alphanumeric, underscore, and hyphen, 3-50 length.</span></span>
* <span data-ttu-id="9107c-133">**location**.</span><span class="sxs-lookup"><span data-stu-id="9107c-133">**location**.</span></span> <span data-ttu-id="9107c-134">Il percorso (area/data center di Azure) per eseguire il provisioning dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9107c-134">The location (azure region/datacenter) to provision the IoT hub.</span></span>
* <span data-ttu-id="9107c-135">**sku-name**.</span><span class="sxs-lookup"><span data-stu-id="9107c-135">**sku-name**.</span></span> <span data-ttu-id="9107c-136">Il nome dello SKU, uno fra: [F1, S1, S2, S3].</span><span class="sxs-lookup"><span data-stu-id="9107c-136">The name of the sku, one of: [F1, S1, S2, S3].</span></span> <span data-ttu-id="9107c-137">Per l'elenco completo più recente, vedere la pagina relativa ai prezzi di IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9107c-137">For the latest full list, refer to the pricing page for IoT Hub.</span></span>
* <span data-ttu-id="9107c-138">**units**.</span><span class="sxs-lookup"><span data-stu-id="9107c-138">**units**.</span></span> <span data-ttu-id="9107c-139">Il numero di unità fornite.</span><span class="sxs-lookup"><span data-stu-id="9107c-139">The number of provisioned units.</span></span> <span data-ttu-id="9107c-140">Intervallo: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span><span class="sxs-lookup"><span data-stu-id="9107c-140">Range: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span></span> <span data-ttu-id="9107c-141">Le unità IoT Hub sono basate sul numero totale di messaggi e il numero di dispositivi a cui si vuole connettersi.</span><span class="sxs-lookup"><span data-stu-id="9107c-141">IoT Hub units are based on your total message count and the number of devices you want to connect.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

<span data-ttu-id="9107c-142">Per visualizzare tutti i parametri disponibili per la creazione, è possibile usare il comando help nel prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="9107c-142">To see all the parameters available for creation, you can use the help command in command prompt:</span></span>

```azurecli
azure iothub create -h
```

<span data-ttu-id="9107c-143">Esempio rapido: per creare un hub IoT denominato **exampleIoTHubName** nel gruppo di risorse **exampleResourceGroup**, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="9107c-143">Quick example: To create an IoT Hub called **exampleIoTHubName** in the resource group **exampleResourceGroup**, run the following command:</span></span>

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> <span data-ttu-id="9107c-144">Attraverso questo comando dell'interfaccia della riga di comando di Azure viene creato un hub IoT S1 Standard che viene addebitato.</span><span class="sxs-lookup"><span data-stu-id="9107c-144">This Azure CLI command creates an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="9107c-145">Per eliminare l'hub IoT **exampleIoTHubName** eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="9107c-145">You can delete the IoT hub **exampleIoTHubName** using following command:</span></span>
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a><span data-ttu-id="9107c-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9107c-146">Next steps</span></span>

<span data-ttu-id="9107c-147">Per altre informazioni sulle attività di sviluppo per l'hub IoT, vedere l'articolo seguente:</span><span class="sxs-lookup"><span data-stu-id="9107c-147">To learn more about developing for IoT Hub, see the following article:</span></span>

* <span data-ttu-id="9107c-148">[IoT SDKs][lnk-sdks] (SDK di IoT)</span><span class="sxs-lookup"><span data-stu-id="9107c-148">[IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="9107c-149">Per altre informazioni sulle funzionalità dell'hub IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="9107c-149">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="9107c-150">[Uso del portale di Azure per gestire l'hub IoT][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="9107c-150">[Using the Azure portal to manage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
