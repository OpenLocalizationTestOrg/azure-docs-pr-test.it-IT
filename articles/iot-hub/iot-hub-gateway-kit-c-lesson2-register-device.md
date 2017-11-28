---
title: 'Dispositivo SensorTag e gateway Azure IoT: lezione 2: Registrare il dispositivo | Documentazione Microsoft'
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: hub iot di azure, cloud internet delle cose, hub iot di azure creare dispositivo, sensortag ti, ble ti
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 2c18f5ae-e39a-48ae-a9fe-04bb595740a0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 685a479583f5f11f57bef22dc5881285bb1f70d0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a><span data-ttu-id="7cfaf-103">Creare un hub IoT di Azure e registrare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="7cfaf-103">Create your Azure IoT hub and register your device</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="7cfaf-104">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="7cfaf-104">What you will do</span></span>

- <span data-ttu-id="7cfaf-105">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="7cfaf-105">Create a resource group</span></span>
- <span data-ttu-id="7cfaf-106">Creare il primo hub IoT</span><span class="sxs-lookup"><span data-stu-id="7cfaf-106">Create your first IoT hub</span></span>
- <span data-ttu-id="7cfaf-107">Registrare il dispositivo nell'hub IoT usando l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="7cfaf-107">Register your device in your IoT hub by using the Azure CLI.</span></span> 

<span data-ttu-id="7cfaf-108">Quando si registra il dispositivo nell'hub IoT, il servizio hub IoT di Azure genera una chiave che il dispositivo deve usare per l'autenticazione con il servizio.</span><span class="sxs-lookup"><span data-stu-id="7cfaf-108">When you register your device in your IoT hub, the Azure IoT Hub service generates a key for your device to use to authenticate with the service.</span></span> 

<span data-ttu-id="7cfaf-109">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="7cfaf-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7cfaf-110">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="7cfaf-110">What you will learn</span></span>

<span data-ttu-id="7cfaf-111">In questa lezione si apprenderà:</span><span class="sxs-lookup"><span data-stu-id="7cfaf-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="7cfaf-112">Come usare l'interfaccia della riga di comando di Azure per creare un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7cfaf-112">How to use the Azure CLI to create an IoT hub.</span></span>
- <span data-ttu-id="7cfaf-113">Come registrare un dispositivo in un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7cfaf-113">How to register a device in an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7cfaf-114">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="7cfaf-114">What you need</span></span>

- <span data-ttu-id="7cfaf-115">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="7cfaf-115">An active Azure subscription.</span></span> <span data-ttu-id="7cfaf-116">Se non si ha un account Azure, è possibile [creare un account Azure gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="7cfaf-116">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
- <span data-ttu-id="7cfaf-117">È necessario che sia installata l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="7cfaf-117">You should have the Azure CLI installed.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="7cfaf-118">Creare un hub IoT</span><span class="sxs-lookup"><span data-stu-id="7cfaf-118">Create an IoT hub</span></span>

<span data-ttu-id="7cfaf-119">Per creare un hub IoT, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7cfaf-119">To create an IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="7cfaf-120">Accedere al proprio account di Azure usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7cfaf-120">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="7cfaf-121">Dopo l'accesso verranno elencate tutte le sottoscrizioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="7cfaf-121">All your available subscriptions will be listed after a successful sign-in.</span></span>

2. <span data-ttu-id="7cfaf-122">Impostare la sottoscrizione di Azure predefinita che si vuole usare mediante il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7cfaf-122">Set the default Azure subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="7cfaf-123">`subscription ID or name` si trova nell'output del comando `az login` o `az account list`.</span><span class="sxs-lookup"><span data-stu-id="7cfaf-123">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="7cfaf-124">Registrare il provider usando il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="7cfaf-124">Register the provider by running the following command.</span></span> <span data-ttu-id="7cfaf-125">I provider di risorse sono servizi che forniscono risorse per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7cfaf-125">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="7cfaf-126">Prima di poter distribuire la risorsa di Azure fornita dal provider, è necessario registrare il provider.</span><span class="sxs-lookup"><span data-stu-id="7cfaf-126">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. <span data-ttu-id="7cfaf-127">Creare un gruppo di risorse denominato `iot-gateway` nell'area Stati Uniti occidentali usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7cfaf-127">Create a resource group named `iot-gateway` in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   <span data-ttu-id="7cfaf-128">`westus` è la località in cui si crea il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="7cfaf-128">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="7cfaf-129">Per usare un'altra località è possibile eseguire `az account list-locations -o table` per visualizzare tutte le località supportate da Azure.</span><span class="sxs-lookup"><span data-stu-id="7cfaf-129">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>

5. <span data-ttu-id="7cfaf-130">Creare un hub IoT nel gruppo di risorse `iot-gateway` usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7cfaf-130">Create an IoT hub in the `iot-gateway` resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

<span data-ttu-id="7cfaf-131">Per impostazione predefinita, lo strumento crea un hub IoT nel piano tariffario gratuito.</span><span class="sxs-lookup"><span data-stu-id="7cfaf-131">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="7cfaf-132">Per altre informazioni, vedere [Prezzi dell'hub Iot di Azure](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="7cfaf-132">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="7cfaf-133">Il nome dell'hub IoT deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="7cfaf-133">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="7cfaf-134">È possibile creare una sola edizione F1 dell'hub IoT di Azure nell'ambito della propria sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7cfaf-134">You can create only one F1 edition of Azure Iot Hub under your Azure subscription.</span></span>

## <a name="register-your-device-in-your-iot-hub"></a><span data-ttu-id="7cfaf-135">Registrare il dispositivo nell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="7cfaf-135">Register your device in your IoT hub</span></span>

<span data-ttu-id="7cfaf-136">Ogni dispositivo che invia o riceve messaggi da e verso l'hub IoT deve essere registrato con un ID univoco.</span><span class="sxs-lookup"><span data-stu-id="7cfaf-136">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>
<span data-ttu-id="7cfaf-137">Registrare il dispositivo nell'hub IoT eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="7cfaf-137">Register your device in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a><span data-ttu-id="7cfaf-138">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="7cfaf-138">Summary</span></span>

<span data-ttu-id="7cfaf-139">È stato creato un hub IoT e il dispositivo logico è stato registrato con un'identità del dispositivo nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7cfaf-139">You've created an IoT hub and registered your logical device with a device identity in your IoT hub.</span></span> <span data-ttu-id="7cfaf-140">Si è già appreso come configurare ed eseguire un'applicazione gateway di esempio per inviare dati dal dispositivo fisico all'hub IoT nel cloud.</span><span class="sxs-lookup"><span data-stu-id="7cfaf-140">You're ready to learn how to configure and run a gateway sample application to send data from your physical device to your IoT hub in the cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7cfaf-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7cfaf-141">Next steps</span></span>
[<span data-ttu-id="7cfaf-142">Configurare ed eseguire un'app di esempio BLE</span><span class="sxs-lookup"><span data-stu-id="7cfaf-142">Configure and run a BLE sample app</span></span>](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)