---
title: 'Connettere Intel Edison (C) ad Azure IoT: lezione 2: Registrare il dispositivo | Documentazione Microsoft'
description: Creare un gruppo di risorse, creare un hub IoT di Azure e registrare Edison nell'hub IoT di Azure tramite l'interfaccia della riga di comando di Azure.
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
ms.openlocfilehash: 52e3e4734dfd2b89f79b0c66683163e69b8e5f25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a><span data-ttu-id="18bec-103">Creare l'hub IoT e registrare Intel Edison</span><span class="sxs-lookup"><span data-stu-id="18bec-103">Create your IoT hub and register Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="18bec-104">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="18bec-104">What you will do</span></span>
* <span data-ttu-id="18bec-105">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="18bec-105">Create a resource group.</span></span>
* <span data-ttu-id="18bec-106">Creare l'hub IoT di Azure nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="18bec-106">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="18bec-107">Aggiungere Intel Edison all'hub IoT di Azure usando l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="18bec-107">Add Intel Edison to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="18bec-108">Quando si usa l'interfaccia della riga di comando di Azure per aggiungere Edison all'hub IoT, il servizio genera una chiave per l'autenticazione di Edison con il servizio.</span><span class="sxs-lookup"><span data-stu-id="18bec-108">When you use the Azure CLI to add Edison to your IoT hub, the service generates a key for Edison to authenticate with the service.</span></span> <span data-ttu-id="18bec-109">In caso di problemi, cercare le soluzioni nella [pagina sulla risoluzione dei problemi][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="18bec-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="18bec-110">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="18bec-110">What you will learn</span></span>
<span data-ttu-id="18bec-111">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="18bec-111">In this article, you will learn:</span></span>
* <span data-ttu-id="18bec-112">Come usare l'interfaccia della riga di comando di Azure per creare un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="18bec-112">How to use the Azure CLI to create an IoT hub.</span></span>
* <span data-ttu-id="18bec-113">Come creare un'identità del dispositivo per Edison nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="18bec-113">How to create a device identity for Edison in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="18bec-114">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="18bec-114">What you need</span></span>
* <span data-ttu-id="18bec-115">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="18bec-115">An Azure account.</span></span> <span data-ttu-id="18bec-116">Se non si ha un account Azure, creare un [account Azure gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="18bec-116">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
* <span data-ttu-id="18bec-117">È necessario che sia installata l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="18bec-117">You should have the Azure CLI installed.</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="18bec-118">Creare l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="18bec-118">Create your IoT hub</span></span>
<span data-ttu-id="18bec-119">L'hub IoT di Azure consente di connettersi a milioni di asset IoT, monitorarli e gestirli.</span><span class="sxs-lookup"><span data-stu-id="18bec-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="18bec-120">Per creare l'hub IoT, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="18bec-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="18bec-121">Accedere al proprio account di Azure usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="18bec-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="18bec-122">Dopo l'accesso vengono elencate tutte le sottoscrizioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="18bec-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="18bec-123">Impostare la sottoscrizione predefinita che si vuole usare tramite il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="18bec-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="18bec-124">`subscription ID or name` si trova nell'output del comando `az login` o `az account list`.</span><span class="sxs-lookup"><span data-stu-id="18bec-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="18bec-125">Registrare il provider usando il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="18bec-125">Register the provider by running the following command.</span></span> <span data-ttu-id="18bec-126">I provider di risorse sono servizi che forniscono risorse per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="18bec-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="18bec-127">Prima di poter distribuire la risorsa di Azure fornita dal provider, è necessario registrare il provider.</span><span class="sxs-lookup"><span data-stu-id="18bec-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="18bec-128">Creare un gruppo di risorse denominato iot-sample nell'area Stati Uniti occidentali usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="18bec-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="18bec-129">`westus` è la località in cui si crea il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="18bec-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="18bec-130">Per usare un'altra località è possibile eseguire `az account list-locations -o table` per visualizzare tutte le località supportate da Azure.</span><span class="sxs-lookup"><span data-stu-id="18bec-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>

5. <span data-ttu-id="18bec-131">Creare un hub IoT nel gruppo di risorse iot-sample usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="18bec-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="18bec-132">Per impostazione predefinita, lo strumento crea un hub IoT nel piano tariffario gratuito.</span><span class="sxs-lookup"><span data-stu-id="18bec-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="18bec-133">Per altre informazioni, vedere [Prezzi dell'hub Iot di Azure](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="18bec-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="18bec-134">Il nome dell'hub IoT deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="18bec-134">The name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="18bec-135">È possibile creare una sola edizione F1 dell'hub IoT di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="18bec-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>


## <a name="register-edison-in-your-iot-hub"></a><span data-ttu-id="18bec-136">Registrare Edison nell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="18bec-136">Register Edison in your IoT hub</span></span>
<span data-ttu-id="18bec-137">Ogni dispositivo che invia o riceve messaggi da e verso l'hub IoT deve essere registrato con un ID univoco.</span><span class="sxs-lookup"><span data-stu-id="18bec-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="18bec-138">Registrare Edison nell'hub IoT eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="18bec-138">Register Edison in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="18bec-139">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="18bec-139">Summary</span></span>
<span data-ttu-id="18bec-140">È stato creato un hub IoT ed Edison è stato registrato con un'identità del dispositivo nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="18bec-140">You've created an IoT hub and registered Edison with a device identity in your IoT hub.</span></span> <span data-ttu-id="18bec-141">È ora possibile apprendere come inviare messaggi da Edison all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="18bec-141">You're ready to learn how to send messages from Edison to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18bec-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="18bec-142">Next steps</span></span>
<span data-ttu-id="18bec-143">[Creare un'app per le funzioni di Azure e un account di archiviazione di Azure per elaborare e archiviare i messaggi dell'hub IoT][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="18bec-143">[Create an Azure function app and an Azure Storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md