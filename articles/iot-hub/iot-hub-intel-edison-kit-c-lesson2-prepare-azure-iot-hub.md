---
title: 'Connect Intel Edison (C) tooAzure IoT - lezione 2: registrazione del dispositivo | Documenti Microsoft'
description: Creare un gruppo di risorse, creare un hub IoT di Azure e registrare Edison nell'hub IoT Azure hello utilizzando hello CLI di Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 80bfc3cd-a1fc-4775-8994-d8033381dd3d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9635e916425883d65793d0ed46843ab49b3f35ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a><span data-ttu-id="43545-103">Creare l'hub IoT e registrare Intel Edison</span><span class="sxs-lookup"><span data-stu-id="43545-103">Create your IoT hub and register Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="43545-104">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="43545-104">What you will do</span></span>
* <span data-ttu-id="43545-105">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="43545-105">Create a resource group.</span></span>
* <span data-ttu-id="43545-106">Creare l'hub IoT di Azure nel gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="43545-106">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="43545-107">Aggiungere l'hub IoT di Azure toohello Edison Intel utilizzando hello Azure interfaccia della riga di comando (CLI di Azure).</span><span class="sxs-lookup"><span data-stu-id="43545-107">Add Intel Edison toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="43545-108">Quando si usa hello Azure CLI tooadd l'hub IoT tooyour Edison, servizio hello genera una chiave per tooauthenticate Edison con servizio hello.</span><span class="sxs-lookup"><span data-stu-id="43545-108">When you use hello Azure CLI tooadd Edison tooyour IoT hub, hello service generates a key for Edison tooauthenticate with hello service.</span></span> <span data-ttu-id="43545-109">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="43545-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="43545-110">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="43545-110">What you will learn</span></span>
<span data-ttu-id="43545-111">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="43545-111">In this article, you will learn:</span></span>
* <span data-ttu-id="43545-112">Come un hub IoT toouse hello toocreate CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="43545-112">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
* <span data-ttu-id="43545-113">Come toocreate un'identità del dispositivo per Edison nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="43545-113">How toocreate a device identity for Edison in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="43545-114">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="43545-114">What you need</span></span>
* <span data-ttu-id="43545-115">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="43545-115">An Azure account.</span></span> <span data-ttu-id="43545-116">Se non si ha un account Azure, creare un [account Azure gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="43545-116">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
* <span data-ttu-id="43545-117">È necessario hello che Azure CLI installato.</span><span class="sxs-lookup"><span data-stu-id="43545-117">You should have hello Azure CLI installed.</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="43545-118">Creare l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="43545-118">Create your IoT hub</span></span>
<span data-ttu-id="43545-119">L'hub IoT di Azure consente di connettersi a milioni di asset IoT, monitorarli e gestirli.</span><span class="sxs-lookup"><span data-stu-id="43545-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="43545-120">toocreate l'hub IoT, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="43545-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="43545-121">Accedi tooyour account Azure eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="43545-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="43545-122">Dopo l'accesso vengono elencate tutte le sottoscrizioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="43545-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="43545-123">Impostare la sottoscrizione predefinita hello che si desidera toouse eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="43545-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="43545-124">`subscription ID or name`possono essere trovati nell'output di hello di hello `az login` o hello `az account list` comando.</span><span class="sxs-lookup"><span data-stu-id="43545-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="43545-125">Registrare il provider di hello eseguendo hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="43545-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="43545-126">I provider di risorse sono servizi che forniscono risorse per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="43545-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="43545-127">Prima di poter distribuire hello risorsa di Azure che hello offerte di provider, è necessario registrare il provider di hello.</span><span class="sxs-lookup"><span data-stu-id="43545-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="43545-128">Creare un gruppo di risorse denominato iot-esempio nell'area Stati Uniti occidentali hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="43545-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="43545-129">`westus`è il percorso di hello creare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="43545-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="43545-130">Se si desidera toouse un'altra posizione, è possibile eseguire `az account list-locations -o table` toosee tutti hello Azure supporta percorsi.</span><span class="sxs-lookup"><span data-stu-id="43545-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="43545-131">Creare un hub IoT nel gruppo di risorse di esempio di iot hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="43545-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="43545-132">Per impostazione predefinita, lo strumento hello crea un IoT Hub nel piano tariffario gratuito hello.</span><span class="sxs-lookup"><span data-stu-id="43545-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="43545-133">Per altre informazioni, vedere [Prezzi dell'hub Iot di Azure](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="43545-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="43545-134">nome Hello dell'hub IoT deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="43545-134">hello name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="43545-135">È possibile creare una sola edizione F1 dell'hub IoT di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="43545-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>


## <a name="register-edison-in-your-iot-hub"></a><span data-ttu-id="43545-136">Registrare Edison nell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="43545-136">Register Edison in your IoT hub</span></span>
<span data-ttu-id="43545-137">Ogni dispositivo che invia l'hub IoT tooyour messaggi e riceve messaggi dall'hub IoT deve essere registrato con un ID univoco.</span><span class="sxs-lookup"><span data-stu-id="43545-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="43545-138">Registrare Edison nell'hub IoT eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="43545-138">Register Edison in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="43545-139">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="43545-139">Summary</span></span>
<span data-ttu-id="43545-140">È stato creato un hub IoT ed Edison è stato registrato con un'identità del dispositivo nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="43545-140">You've created an IoT hub and registered Edison with a device identity in your IoT hub.</span></span> <span data-ttu-id="43545-141">Si è pronti toolearn come toosend messaggi dall'hub IoT di tooyour Edison.</span><span class="sxs-lookup"><span data-stu-id="43545-141">You're ready toolearn how toosend messages from Edison tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43545-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="43545-142">Next steps</span></span>
<span data-ttu-id="43545-143">[Creare un'app di Azure (funzione) e un hub IoT tooprocess e l'archivio del account di archiviazione di Azure messaggi][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="43545-143">[Create an Azure function app and an Azure Storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md