---
featureFlags: usabilla
title: 'Connettere Raspberry Pi (Node) ad Azure IoT: lezione 2: Registrare il dispositivo | Documentazione Microsoft'
description: "Creare un gruppo di risorse, creare un hub IoT di Azure e registrare il dispositivo Pi nel registro delle identità dell'hub IoT tramite l'interfaccia della riga di comando di Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: cloud raspberry pi, connessione cloud pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 736215b6-e7e4-46f9-af30-0ded9ffa5204
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 774f9356d7a11b2c61905ada75bed92d44e5fc0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="0d54d-104">Creare l'hub IoT e registrare Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="0d54d-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="0d54d-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="0d54d-105">What you will do</span></span>
* <span data-ttu-id="0d54d-106">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="0d54d-106">Create a resource group.</span></span>
* <span data-ttu-id="0d54d-107">Creare l'hub IoT di Azure nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="0d54d-107">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="0d54d-108">Aggiungere Raspberry Pi 3 all'hub IoT di Azure usando l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d54d-108">Add Raspberry Pi 3 to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="0d54d-109">Quando si usa l'interfaccia della riga di comando di Azure per aggiungere il dispositivo Pi all'hub IoT, il servizio genera una chiave per l'autenticazione del dispositivo Pi con il servizio.</span><span class="sxs-lookup"><span data-stu-id="0d54d-109">When you use Azure CLI to add Pi to your IoT hub, the service generates a key for Pi to authenticate with the service.</span></span> <span data-ttu-id="0d54d-110">In caso di problemi cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="0d54d-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0d54d-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="0d54d-111">What you will learn</span></span>
<span data-ttu-id="0d54d-112">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="0d54d-112">In this article, you will learn:</span></span>
* <span data-ttu-id="0d54d-113">Come usare l'interfaccia della riga di comando di Azure per creare un hub IoT</span><span class="sxs-lookup"><span data-stu-id="0d54d-113">How to use Azure CLI to create an IoT hub</span></span>
* <span data-ttu-id="0d54d-114">Come creare un'identità per il dispositivo Pi nell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="0d54d-114">How to create a device identity for Pi in your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0d54d-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="0d54d-115">What you need</span></span>
* <span data-ttu-id="0d54d-116">Un account Azure</span><span class="sxs-lookup"><span data-stu-id="0d54d-116">An Azure account</span></span>
* <span data-ttu-id="0d54d-117">Un computer Mac o Windows con l'interfaccia della riga di comando di Azure installata</span><span class="sxs-lookup"><span data-stu-id="0d54d-117">A Mac or a Windows computer with the Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="0d54d-118">Creare l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="0d54d-118">Create your IoT hub</span></span>
<span data-ttu-id="0d54d-119">L'hub IoT di Azure consente di connettersi a milioni di asset IoT, monitorarli e gestirli.</span><span class="sxs-lookup"><span data-stu-id="0d54d-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="0d54d-120">Per creare l'hub IoT, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0d54d-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="0d54d-121">Accedere al proprio account di Azure usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0d54d-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="0d54d-122">Dopo l'accesso vengono elencate tutte le sottoscrizioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="0d54d-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="0d54d-123">Impostare la sottoscrizione predefinita che si vuole usare tramite il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0d54d-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="0d54d-124">`subscription ID or name` si trova nell'output del comando `az login` o `az account list`.</span><span class="sxs-lookup"><span data-stu-id="0d54d-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="0d54d-125">Registrare il provider usando il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="0d54d-125">Register the provider by running the following command.</span></span> <span data-ttu-id="0d54d-126">I provider di risorse sono servizi che forniscono risorse per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0d54d-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="0d54d-127">Prima di poter distribuire la risorsa di Azure fornita dal provider, è necessario registrare il provider.</span><span class="sxs-lookup"><span data-stu-id="0d54d-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="0d54d-128">Creare un gruppo di risorse denominato iot-sample nell'area Stati Uniti occidentali usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0d54d-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="0d54d-129">`westus` è la località in cui si crea il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="0d54d-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="0d54d-130">Per usare un'altra località è possibile eseguire `az account list-locations -o table` per visualizzare tutte le località supportate da Azure.</span><span class="sxs-lookup"><span data-stu-id="0d54d-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>
 
5. <span data-ttu-id="0d54d-131">Creare un hub IoT nel gruppo di risorse iot-sample usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0d54d-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="0d54d-132">Per impostazione predefinita, lo strumento crea un hub IoT nel piano tariffario gratuito.</span><span class="sxs-lookup"><span data-stu-id="0d54d-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="0d54d-133">Per altre informazioni, vedere [Prezzi dell'hub Iot di Azure](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="0d54d-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="0d54d-134">Il nome dell'hub IoT deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="0d54d-134">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="0d54d-135">È possibile creare una sola edizione F1 dell'hub IoT di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d54d-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="0d54d-136">Registrare il dispositivo Pi nell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="0d54d-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="0d54d-137">Ogni dispositivo che invia o riceve messaggi da e verso l'hub IoT deve essere registrato con un ID univoco.</span><span class="sxs-lookup"><span data-stu-id="0d54d-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span> <span data-ttu-id="0d54d-138">Si userà l'interfaccia della riga di comando di Azure per registrare il dispositivo Pi e creare un certificato X.509 autofirmato per l'autenticazione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0d54d-138">You will use Azure CLI to register your Pi and create a self-signed X.509 certificate for device authentication.</span></span>

<span data-ttu-id="0d54d-139">Eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0d54d-139">Run the following command:</span></span>

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a><span data-ttu-id="0d54d-140">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="0d54d-140">Summary</span></span>
<span data-ttu-id="0d54d-141">È stato creato un hub IoT e il dispositivo Pi è stato registrato con un'identità del dispositivo nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0d54d-141">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="0d54d-142">È ora possibile apprendere come inviare messaggi dal dispositivo Pi all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0d54d-142">You're ready to learn how to send messages from Pi to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d54d-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0d54d-143">Next steps</span></span>
[<span data-ttu-id="0d54d-144">Creare un'app per le funzioni di Azure e un account di archiviazione di Azure per elaborare e archiviare i messaggi dell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="0d54d-144">Create an Azure function app and an Azure storage account to process and store IoT hub messages</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)

