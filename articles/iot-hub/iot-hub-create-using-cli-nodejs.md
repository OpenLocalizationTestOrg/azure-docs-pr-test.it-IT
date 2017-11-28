---
title: un hub IoT mediante Azure CLI (azure.js) aaaCreate | Documenti Microsoft
description: Come un hub IoT di Azure mediante toocreate hello multipiattaforma CLI di Azure (azure.js).
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
ms.openlocfilehash: c2a7ea98500b0a0e55a39f4cdfea4605c92add94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli"></a><span data-ttu-id="81b7a-103">Creazione di un hub IoT utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="81b7a-103">Create an IoT hub using hello Azure CLI</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="81b7a-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="81b7a-104">Introduction</span></span>

<span data-ttu-id="81b7a-105">È possibile utilizzare toocreate CLI di Azure (azure.js) e gestire hub IoT di Azure a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="81b7a-105">You can use Azure CLI (azure.js) toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="81b7a-106">Questo articolo illustra come toouse hello toocreate CLI di Azure (azure.js) un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="81b7a-106">This article shows you how toouse hello Azure CLI (azure.js) toocreate an IoT hub.</span></span>

<span data-ttu-id="81b7a-107">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="81b7a-107">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="81b7a-108">CLI di Azure (azure.js): hello CLI per hello classic e modelli di distribuzione di gestione di risorse come descritto in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="81b7a-108">Azure CLI (azure.js) – hello CLI for hello classic and resource management deployment models as described in this article.</span></span>
* <span data-ttu-id="81b7a-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) -hello prossima generazione CLI per modello di distribuzione di gestione risorse hello.</span><span class="sxs-lookup"><span data-stu-id="81b7a-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) - hello next generation CLI for hello resource management deployment model.</span></span>

<span data-ttu-id="81b7a-110">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="81b7a-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="81b7a-111">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="81b7a-111">An active Azure account.</span></span> <span data-ttu-id="81b7a-112">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="81b7a-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="81b7a-113">[Interfaccia della riga di comando di Azure 0.10.4][lnk-CLI-install] o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="81b7a-113">[Azure CLI 0.10.4][lnk-CLI-install] or later.</span></span> <span data-ttu-id="81b7a-114">Se si dispone già di hello Azure CLI installato, è possibile convalidare una versione corrente di hello al prompt dei comandi di hello con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="81b7a-114">If you already have hello Azure CLI installed, you can validate hello current version at hello command prompt with hello following command:</span></span>

```azurecli
azure --version
```

> [!NOTE]
> <span data-ttu-id="81b7a-115">Azure offre due modelli di distribuzione per creare e usare le risorse: [modello di distribuzione classica e Azure Resource Manager](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="81b7a-115">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="81b7a-116">Hello CLI di Azure deve essere in modalità di gestione risorse di Azure:</span><span class="sxs-lookup"><span data-stu-id="81b7a-116">hello Azure CLI must be in Azure Resource Manager mode:</span></span>
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="81b7a-117">Impostare l'account e la sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="81b7a-117">Set your Azure account and subscription</span></span>

1. <span data-ttu-id="81b7a-118">Al prompt dei comandi di hello, account di accesso digitando hello il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="81b7a-118">At hello command prompt, login by typing hello following command:</span></span>

   ```azurecli
    azure login
   ```

   <span data-ttu-id="81b7a-119">Utilizzare hello suggeriti i web browser e tooauthenticate di codice.</span><span class="sxs-lookup"><span data-stu-id="81b7a-119">Use hello suggested web browser and code tooauthenticate.</span></span>
1. <span data-ttu-id="81b7a-120">Se si dispone di più sottoscrizioni di Azure, la connessione tooAzure consenta l'accesso tooall hello le sottoscrizioni di Azure associate con le credenziali.</span><span class="sxs-lookup"><span data-stu-id="81b7a-120">If you have multiple Azure subscriptions, connecting tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="81b7a-121">È possibile visualizzare le sottoscrizioni di Azure hello e consente di identificare quello predefinito di hello, utilizzando il comando di hello:</span><span class="sxs-lookup"><span data-stu-id="81b7a-121">You can view hello Azure subscriptions, and identify which one is hello default, using hello command:</span></span>

   ```azurecli
    azure account list
   ```

   <span data-ttu-id="81b7a-122">contesto di tooset hello sottoscrizione in cui si desidera utilizzare comandi hello restanti hello toorun:</span><span class="sxs-lookup"><span data-stu-id="81b7a-122">tooset hello subscription context under which you want toorun hello rest of hello commands use:</span></span>

   ```azurecli
    azure account set <subscription name>
   ```

1. <span data-ttu-id="81b7a-123">Se non si dispone di un gruppo di risorse, è possibile crearne uno denominato **exampleResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="81b7a-123">If you do not have a resource group, you can create one named **exampleResourceGroup**:</span></span>

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> <span data-ttu-id="81b7a-124">articolo Hello [toomanage CLI di Azure hello Azure usare risorse e gruppi di risorse] [ lnk-CLI-arm] fornisce ulteriori informazioni su come toouse hello Azure CLI toomanage Azure le risorse.</span><span class="sxs-lookup"><span data-stu-id="81b7a-124">hello article [Use hello Azure CLI toomanage Azure resources and resource groups][lnk-CLI-arm] provides more information about how toouse hello Azure CLI toomanage Azure resources.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="81b7a-125">Creare un hub IoT</span><span class="sxs-lookup"><span data-stu-id="81b7a-125">Create an IoT Hub</span></span>

<span data-ttu-id="81b7a-126">Parametri obbligatori:</span><span class="sxs-lookup"><span data-stu-id="81b7a-126">Required parameters:</span></span>

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* <span data-ttu-id="81b7a-127">**resource-group**.</span><span class="sxs-lookup"><span data-stu-id="81b7a-127">**resource-group**.</span></span> <span data-ttu-id="81b7a-128">nome del gruppo di risorse Hello.</span><span class="sxs-lookup"><span data-stu-id="81b7a-128">hello resource group name.</span></span> <span data-ttu-id="81b7a-129">formato Hello viene fatta distinzione tra maiuscole e minuscole caratteri alfanumerici, caratteri di sottolineatura e trattini, lunghezza di 1 a 64.</span><span class="sxs-lookup"><span data-stu-id="81b7a-129">hello format is case insensitive alphanumeric, underscore, and hyphen, 1-64 length.</span></span>
* <span data-ttu-id="81b7a-130">**name**.</span><span class="sxs-lookup"><span data-stu-id="81b7a-130">**name**.</span></span> <span data-ttu-id="81b7a-131">nome Hello di hello IoT hub toobe creato.</span><span class="sxs-lookup"><span data-stu-id="81b7a-131">hello name of hello IoT hub toobe created.</span></span> <span data-ttu-id="81b7a-132">formato Hello viene fatta distinzione tra maiuscole e minuscole caratteri alfanumerici, caratteri di sottolineatura e trattino, lunghezza 3-50.</span><span class="sxs-lookup"><span data-stu-id="81b7a-132">hello format is case insensitive alphanumeric, underscore, and hyphen, 3-50 length.</span></span>
* <span data-ttu-id="81b7a-133">**location**.</span><span class="sxs-lookup"><span data-stu-id="81b7a-133">**location**.</span></span> <span data-ttu-id="81b7a-134">Hello percorso (area o Data Center di azure) tooprovision hello hub IoT.</span><span class="sxs-lookup"><span data-stu-id="81b7a-134">hello location (azure region/datacenter) tooprovision hello IoT hub.</span></span>
* <span data-ttu-id="81b7a-135">**sku-name**.</span><span class="sxs-lookup"><span data-stu-id="81b7a-135">**sku-name**.</span></span> <span data-ttu-id="81b7a-136">nome Hello dello sku di hello, uno di: [F1, S1, S2, S3].</span><span class="sxs-lookup"><span data-stu-id="81b7a-136">hello name of hello sku, one of: [F1, S1, S2, S3].</span></span> <span data-ttu-id="81b7a-137">Per l'elenco completo più recente hello, consultare toohello pagina dei prezzi per l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="81b7a-137">For hello latest full list, refer toohello pricing page for IoT Hub.</span></span>
* <span data-ttu-id="81b7a-138">**units**.</span><span class="sxs-lookup"><span data-stu-id="81b7a-138">**units**.</span></span> <span data-ttu-id="81b7a-139">numero di Hello di unità sottoposte a provisioning.</span><span class="sxs-lookup"><span data-stu-id="81b7a-139">hello number of provisioned units.</span></span> <span data-ttu-id="81b7a-140">Intervallo: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span><span class="sxs-lookup"><span data-stu-id="81b7a-140">Range: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span></span> <span data-ttu-id="81b7a-141">Unità di IoT Hub sono basate sul numero totale di messaggi hello e di conteggio dei dispositivi desiderato tooconnect.</span><span class="sxs-lookup"><span data-stu-id="81b7a-141">IoT Hub units are based on your total message count and hello number of devices you want tooconnect.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

<span data-ttu-id="81b7a-142">toosee tutti hello parametri disponibili per la creazione, è possibile utilizzare il comando di help hello nel prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="81b7a-142">toosee all hello parameters available for creation, you can use hello help command in command prompt:</span></span>

```azurecli
azure iothub create -h
```

<span data-ttu-id="81b7a-143">Esempio semplice: chiamato di un IoT Hub toocreate **exampleIoTHubName** nel gruppo di risorse hello **exampleResourceGroup**, eseguire hello il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="81b7a-143">Quick example: toocreate an IoT Hub called **exampleIoTHubName** in hello resource group **exampleResourceGroup**, run hello following command:</span></span>

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> <span data-ttu-id="81b7a-144">Attraverso questo comando dell'interfaccia della riga di comando di Azure viene creato un hub IoT S1 Standard che viene addebitato.</span><span class="sxs-lookup"><span data-stu-id="81b7a-144">This Azure CLI command creates an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="81b7a-145">È possibile eliminare l'hub IoT hello **exampleIoTHubName** tramite il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="81b7a-145">You can delete hello IoT hub **exampleIoTHubName** using following command:</span></span>
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a><span data-ttu-id="81b7a-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="81b7a-146">Next steps</span></span>

<span data-ttu-id="81b7a-147">toolearn più sullo sviluppo per l'IoT Hub, vedere l'articolo seguente hello:</span><span class="sxs-lookup"><span data-stu-id="81b7a-147">toolearn more about developing for IoT Hub, see hello following article:</span></span>

* <span data-ttu-id="81b7a-148">[IoT SDKs][lnk-sdks] (SDK di IoT)</span><span class="sxs-lookup"><span data-stu-id="81b7a-148">[IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="81b7a-149">toofurther esplorare le funzionalità di hello di IoT Hub, vedere:</span><span class="sxs-lookup"><span data-stu-id="81b7a-149">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="81b7a-150">[Utilizzo di hello toomanage portale Azure IoT Hub][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="81b7a-150">[Using hello Azure portal toomanage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
