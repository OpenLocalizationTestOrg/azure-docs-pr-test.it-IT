---
title: Creare un hub IoT usando l'interfaccia della riga di comando di Azure (az.py) | Documentazione Microsoft
description: Come creare un hub IoT di Azure usando l'interfaccia della riga di comando di Azure 2.0 multipiattaforma (az.py).
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-hub
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 161089159999a4a63a39b059e69a08b7a9297445
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-iot-hub-using-the-azure-cli-20"></a><span data-ttu-id="93ddf-103">Creare un hub IoT usando l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="93ddf-103">Create an IoT hub using the Azure CLI 2.0</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="93ddf-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="93ddf-104">Introduction</span></span>

<span data-ttu-id="93ddf-105">È possibile usare l'interfaccia della riga di comando di Azure 2.0 (az.py) per creare e gestire hub IoT di Azure a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="93ddf-105">You can use Azure CLI 2.0 (az.py) to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="93ddf-106">Questo articolo illustra come usare l'interfaccia della riga di comando di Azure 2.0 (az.py) per creare un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="93ddf-106">This article shows you how to use the Azure CLI 2.0 (az.py) to create an IoT hub.</span></span>

<span data-ttu-id="93ddf-107">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="93ddf-107">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="93ddf-108">[Interfaccia della riga di comando di Azure (azure.js)](iot-hub-create-using-cli-nodejs.md): l'interfaccia della riga di comando per i modelli di distribuzione classica e di gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="93ddf-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – the CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="93ddf-109">Interfaccia della riga di comando di Azure 2.0 (az.py): interfaccia avanzata per il modello di distribuzione di gestione delle risorse, come descritto in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="93ddf-109">Azure CLI 2.0 (az.py) - the next generation CLI for the resource management deployment model as described in this article.</span></span>

<span data-ttu-id="93ddf-110">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="93ddf-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="93ddf-111">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="93ddf-111">An active Azure account.</span></span> <span data-ttu-id="93ddf-112">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="93ddf-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="93ddf-113">[Interfaccia della riga di comando di Azure 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="93ddf-113">[Azure CLI 2.0][lnk-CLI-install].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="93ddf-114">Accedere all'account Azure e impostarlo</span><span class="sxs-lookup"><span data-stu-id="93ddf-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="93ddf-115">Accedere al proprio account Azure e selezionare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="93ddf-115">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="93ddf-116">Al prompt dei comandi eseguire il [comando per l'accesso][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="93ddf-116">At the command prompt, run the [login command][lnk-login-command]:</span></span>
    
    ```azurecli
    az login
    ```

    <span data-ttu-id="93ddf-117">Seguire le istruzioni per l'autenticazione tramite il codice e accedere all'account Azure con un Web browser.</span><span class="sxs-lookup"><span data-stu-id="93ddf-117">Follow the instructions to authenticate using the code and sign in to your Azure account through a web browser.</span></span>

2. <span data-ttu-id="93ddf-118">Se si usano più sottoscrizioni di Azure, effettuando l'accesso ad Azure è possibile accedere a tutti gli account Azure associati alle credenziali.</span><span class="sxs-lookup"><span data-stu-id="93ddf-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure accounts associated with your credentials.</span></span> <span data-ttu-id="93ddf-119">Usare il seguente [comando per elencare gli account Azure][lnk-az-account-command] che è possibile usare:</span><span class="sxs-lookup"><span data-stu-id="93ddf-119">Use the following [command to list the Azure accounts][lnk-az-account-command] available for you to use:</span></span>
    
    ```azurecli
    az account list 
    ```

    <span data-ttu-id="93ddf-120">Usare il comando seguente per selezionare la sottoscrizione che si vuole usare per eseguire i comandi per creare l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="93ddf-120">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="93ddf-121">È possibile usare il nome o l'ID della sottoscrizione dall'output del comando precedente:</span><span class="sxs-lookup"><span data-stu-id="93ddf-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a><span data-ttu-id="93ddf-122">Creare un hub IoT</span><span class="sxs-lookup"><span data-stu-id="93ddf-122">Create an IoT Hub</span></span>

<span data-ttu-id="93ddf-123">Usare l'interfaccia della riga di comando di Azure per creare un gruppo di risorse e quindi aggiungere un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="93ddf-123">Use the Azure CLI to create a resource group and then add an IoT hub.</span></span>

1. <span data-ttu-id="93ddf-124">Quando si crea un hub IoT, è necessario crearlo in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="93ddf-124">When you create an IoT hub, you must create it in a resource group.</span></span> <span data-ttu-id="93ddf-125">Usare un gruppo di risorse esistente o eseguire questo [comando per creare un gruppo di risorse][lnk-az-resource-command]:</span><span class="sxs-lookup"><span data-stu-id="93ddf-125">Either use an existing resource group, or run the following [command to create a resource group][lnk-az-resource-command]:</span></span>
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > <span data-ttu-id="93ddf-126">L'esempio precedente crea il gruppo di risorse nella località Stati Uniti occidentali.</span><span class="sxs-lookup"><span data-stu-id="93ddf-126">The previous example creates the resource group in the West US location.</span></span> <span data-ttu-id="93ddf-127">È possibile visualizzare un elenco di località disponibili eseguendo il comando `az account list-locations -o table`.</span><span class="sxs-lookup"><span data-stu-id="93ddf-127">You can view a list of available locations by running the command `az account list-locations -o table`.</span></span>
    >
    >

2. <span data-ttu-id="93ddf-128">Eseguire il seguente [comando per creare un hub IoT][lnk-az-iot-command] nel gruppo di risorse, usando un nome globalmente univoco per l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="93ddf-128">Run the following [command to create an IoT hub][lnk-az-iot-command] in your resource group, using a globally unique name for your IoT hub:</span></span>
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> <span data-ttu-id="93ddf-129">Il comando precedente crea un hub IoT nel piano tariffario S1 che viene fatturato.</span><span class="sxs-lookup"><span data-stu-id="93ddf-129">The previous command creates an IoT hub in the S1 pricing tier for which you are billed.</span></span> <span data-ttu-id="93ddf-130">Per altre informazioni, vedere [Azure IoT Hub Prezzi][lnk-iot-pricing].</span><span class="sxs-lookup"><span data-stu-id="93ddf-130">For more information, see [Azure IoT Hub pricing][lnk-iot-pricing].</span></span>
>
>

## <a name="remove-an-iot-hub"></a><span data-ttu-id="93ddf-131">Rimuovere un hub IoT</span><span class="sxs-lookup"><span data-stu-id="93ddf-131">Remove an IoT Hub</span></span>

<span data-ttu-id="93ddf-132">È possibile usare l'interfaccia della riga di comando di Azure per [eliminare una singola risorsa][lnk-az-resource-command], ad esempio un hub IoT, o eliminare un gruppo di risorse e tutte le risorse, inclusi gli hub IoT.</span><span class="sxs-lookup"><span data-stu-id="93ddf-132">You can use the Azure CLI to [delete an individual resource][lnk-az-resource-command], such as an IoT hub, or delete a resource group and all its resources, including any IoT hubs.</span></span>

<span data-ttu-id="93ddf-133">Per eliminare un hub IoT, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="93ddf-133">To delete an IoT hub, run the following command:</span></span>

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

<span data-ttu-id="93ddf-134">Per eliminare un gruppo di risorse e tutte le risorse, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="93ddf-134">To delete a resource group and all its resources, run the following command:</span></span>

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a><span data-ttu-id="93ddf-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="93ddf-135">Next steps</span></span>
<span data-ttu-id="93ddf-136">Per altre informazioni sulle attività di sviluppo per l'hub IoT, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="93ddf-136">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="93ddf-137">[Guida per gli sviluppatori dell'hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="93ddf-137">[IoT Hub developer guide][lnk-devguide]</span></span>

<span data-ttu-id="93ddf-138">Per altre informazioni sulle funzionalità dell'hub IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="93ddf-138">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="93ddf-139">[Uso del portale di Azure per gestire l'hub IoT][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="93ddf-139">[Using the Azure portal to manage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-devguide]: iot-hub-devguide.md
[lnk-portal]: iot-hub-create-through-portal.md 
