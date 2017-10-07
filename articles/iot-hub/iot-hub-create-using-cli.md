---
title: un IoT Hub mediante Azure CLI (az.py) aaaCreate | Documenti Microsoft
description: Come un hub IoT di Azure mediante toocreate hello multipiattaforma CLI di Azure 2.0 (az.py).
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
ms.openlocfilehash: 9c9639235c2ac343e6ceb9578291dafaea26ea24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli-20"></a><span data-ttu-id="5c96f-103">Creazione di un hub IoT utilizzando hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5c96f-103">Create an IoT hub using hello Azure CLI 2.0</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="5c96f-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="5c96f-104">Introduction</span></span>

<span data-ttu-id="5c96f-105">È possibile utilizzare l'interfaccia CLI di Azure 2.0 (az.py) toocreate e gestire hub IoT di Azure a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="5c96f-105">You can use Azure CLI 2.0 (az.py) toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="5c96f-106">Questo articolo illustra come toouse hello toocreate CLI di Azure 2.0 (az.py) un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5c96f-106">This article shows you how toouse hello Azure CLI 2.0 (az.py) toocreate an IoT hub.</span></span>

<span data-ttu-id="5c96f-107">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="5c96f-107">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="5c96f-108">[CLI di Azure (azure.js)](iot-hub-create-using-cli-nodejs.md) : hello CLI per hello classic e risorse Gestione modelli di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="5c96f-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – hello CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="5c96f-109">Azure CLI 2.0 (az.py) - hello prossima generazione CLI per hello risorse Gestione modello di distribuzione come descritto in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="5c96f-109">Azure CLI 2.0 (az.py) - hello next generation CLI for hello resource management deployment model as described in this article.</span></span>

<span data-ttu-id="5c96f-110">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="5c96f-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="5c96f-111">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="5c96f-111">An active Azure account.</span></span> <span data-ttu-id="5c96f-112">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="5c96f-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="5c96f-113">[Interfaccia della riga di comando di Azure 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="5c96f-113">[Azure CLI 2.0][lnk-CLI-install].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="5c96f-114">Accedere all'account Azure e impostarlo</span><span class="sxs-lookup"><span data-stu-id="5c96f-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="5c96f-115">Accedi tooyour account Azure e selezionare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="5c96f-115">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="5c96f-116">Al prompt dei comandi di hello, eseguire hello [comando login][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="5c96f-116">At hello command prompt, run hello [login command][lnk-login-command]:</span></span>
    
    ```azurecli
    az login
    ```

    <span data-ttu-id="5c96f-117">Seguire tooauthenticate istruzioni hello utilizzando codice hello e Accedi tooyour account Azure tramite un web browser.</span><span class="sxs-lookup"><span data-stu-id="5c96f-117">Follow hello instructions tooauthenticate using hello code and sign in tooyour Azure account through a web browser.</span></span>

2. <span data-ttu-id="5c96f-118">Se si dispone di più sottoscrizioni di Azure, consente l'accesso tooall accesso tooAzure hello associato con le credenziali dell'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="5c96f-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure accounts associated with your credentials.</span></span> <span data-ttu-id="5c96f-119">Utilizzare la seguente hello [toolist comando hello account Azure] [ lnk-az-account-command] disponibile per toouse è:</span><span class="sxs-lookup"><span data-stu-id="5c96f-119">Use hello following [command toolist hello Azure accounts][lnk-az-account-command] available for you toouse:</span></span>
    
    ```azurecli
    az account list 
    ```

    <span data-ttu-id="5c96f-120">Utilizzare hello seguente sottoscrizione tooselect comando che si desidera toouse toorun hello comandi toocreate l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5c96f-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="5c96f-121">È possibile utilizzare il nome di sottoscrizione hello o ID dall'output di hello del comando precedente hello:</span><span class="sxs-lookup"><span data-stu-id="5c96f-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a><span data-ttu-id="5c96f-122">Creare un hub IoT</span><span class="sxs-lookup"><span data-stu-id="5c96f-122">Create an IoT Hub</span></span>

<span data-ttu-id="5c96f-123">Utilizzare hello Azure CLI toocreate un gruppo di risorse e quindi aggiungere un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5c96f-123">Use hello Azure CLI toocreate a resource group and then add an IoT hub.</span></span>

1. <span data-ttu-id="5c96f-124">Quando si crea un hub IoT, è necessario crearlo in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="5c96f-124">When you create an IoT hub, you must create it in a resource group.</span></span> <span data-ttu-id="5c96f-125">Utilizzare un gruppo di risorse esistente oppure eseguire l'esempio hello [comando toocreate un gruppo di risorse][lnk-az-resource-command]:</span><span class="sxs-lookup"><span data-stu-id="5c96f-125">Either use an existing resource group, or run hello following [command toocreate a resource group][lnk-az-resource-command]:</span></span>
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > <span data-ttu-id="5c96f-126">Hello precedente esempio Crea gruppo di risorse hello in hello percorso Stati Uniti occidentali.</span><span class="sxs-lookup"><span data-stu-id="5c96f-126">hello previous example creates hello resource group in hello West US location.</span></span> <span data-ttu-id="5c96f-127">È possibile visualizzare un elenco di ubicazioni disponibili eseguendo il comando hello `az account list-locations -o table`.</span><span class="sxs-lookup"><span data-stu-id="5c96f-127">You can view a list of available locations by running hello command `az account list-locations -o table`.</span></span>
    >
    >

2. <span data-ttu-id="5c96f-128">Eseguire il seguente hello [comando toocreate un hub IoT] [ lnk-az-iot-command] nel gruppo di risorse, utilizzando un nome univoco globale per l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="5c96f-128">Run hello following [command toocreate an IoT hub][lnk-az-iot-command] in your resource group, using a globally unique name for your IoT hub:</span></span>
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> <span data-ttu-id="5c96f-129">comando precedente Hello crea un hub IoT in hello S1 piano tariffario per il quale verrà addebitato.</span><span class="sxs-lookup"><span data-stu-id="5c96f-129">hello previous command creates an IoT hub in hello S1 pricing tier for which you are billed.</span></span> <span data-ttu-id="5c96f-130">Per altre informazioni, vedere [Azure IoT Hub Prezzi][lnk-iot-pricing].</span><span class="sxs-lookup"><span data-stu-id="5c96f-130">For more information, see [Azure IoT Hub pricing][lnk-iot-pricing].</span></span>
>
>

## <a name="remove-an-iot-hub"></a><span data-ttu-id="5c96f-131">Rimuovere un hub IoT</span><span class="sxs-lookup"><span data-stu-id="5c96f-131">Remove an IoT Hub</span></span>

<span data-ttu-id="5c96f-132">È possibile utilizzare anche hello Azure CLI[eliminare una singola risorsa][lnk-az-resource-command], ad esempio un hub IoT o elimina un gruppo di risorse e tutte le relative risorse, inclusi tutti gli hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5c96f-132">You can use hello Azure CLI too[delete an individual resource][lnk-az-resource-command], such as an IoT hub, or delete a resource group and all its resources, including any IoT hubs.</span></span>

<span data-ttu-id="5c96f-133">toodelete un hub IoT, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5c96f-133">toodelete an IoT hub, run hello following command:</span></span>

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

<span data-ttu-id="5c96f-134">toodelete un gruppo di risorse e tutte le relative risorse, hello esecuzione seguente comando:</span><span class="sxs-lookup"><span data-stu-id="5c96f-134">toodelete a resource group and all its resources, run hello following command:</span></span>

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a><span data-ttu-id="5c96f-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5c96f-135">Next steps</span></span>
<span data-ttu-id="5c96f-136">toolearn più sullo sviluppo per l'IoT Hub, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="5c96f-136">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="5c96f-137">[Guida per gli sviluppatori dell'hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="5c96f-137">[IoT Hub developer guide][lnk-devguide]</span></span>

<span data-ttu-id="5c96f-138">toofurther esplorare le funzionalità di hello di IoT Hub, vedere:</span><span class="sxs-lookup"><span data-stu-id="5c96f-138">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="5c96f-139">[Utilizzo di hello toomanage portale Azure IoT Hub][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="5c96f-139">[Using hello Azure portal toomanage IoT Hub][lnk-portal]</span></span>

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
