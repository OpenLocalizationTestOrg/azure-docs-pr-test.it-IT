---
title: 'Dispositivo simulato e gateway Azure IoT: lezione 2: Registrare il dispositivo | Documentazione Microsoft'
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: hub iot di azure, cloud internet delle cose, hub iot di azure creare dispositivo, sensortag ti, ble ti
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 23cfbe21-22c6-4fe1-ae41-63714a897f12
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d1052ed2fa9e022966e6e71fa2c7d4f18c333b2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a><span data-ttu-id="e65e3-103">Creare un hub IoT di Azure e registrare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="e65e3-103">Create your Azure IoT hub and register your device</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="e65e3-104">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="e65e3-104">What you will do</span></span>

- <span data-ttu-id="e65e3-105">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="e65e3-105">Create a resource group</span></span>
- <span data-ttu-id="e65e3-106">Creare il primo hub IoT</span><span class="sxs-lookup"><span data-stu-id="e65e3-106">Create your first IoT hub</span></span>
- <span data-ttu-id="e65e3-107">Registrare il dispositivo nell'hub IoT utilizzando hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="e65e3-107">Register your device in your IoT hub by using hello Azure CLI.</span></span> 

<span data-ttu-id="e65e3-108">Quando si registra il dispositivo nell'hub IoT, hello servizio IoT Hub Azure genera una chiave per il tooauthenticate toouse dispositivo con il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="e65e3-108">When you register your device in your IoT hub, hello Azure IoT Hub service generates a key for your device toouse tooauthenticate with hello service.</span></span> 

<span data-ttu-id="e65e3-109">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e65e3-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e65e3-110">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="e65e3-110">What you will learn</span></span>

<span data-ttu-id="e65e3-111">In questa lezione si apprenderà:</span><span class="sxs-lookup"><span data-stu-id="e65e3-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="e65e3-112">Come un hub IoT toouse hello toocreate CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="e65e3-112">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
- <span data-ttu-id="e65e3-113">Come tooregister un dispositivo in un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e65e3-113">How tooregister a device in an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e65e3-114">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="e65e3-114">What you need</span></span>

- <span data-ttu-id="e65e3-115">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="e65e3-115">An active Azure subscription.</span></span> <span data-ttu-id="e65e3-116">Se non si ha un account Azure, è possibile [creare un account Azure gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="e65e3-116">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
- <span data-ttu-id="e65e3-117">È necessario hello che Azure CLI installato.</span><span class="sxs-lookup"><span data-stu-id="e65e3-117">You should have hello Azure CLI installed.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="e65e3-118">Creare un hub IoT</span><span class="sxs-lookup"><span data-stu-id="e65e3-118">Create an IoT hub</span></span>

<span data-ttu-id="e65e3-119">toocreate un hub IoT, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="e65e3-119">toocreate an IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="e65e3-120">Accedi tooyour account Azure eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e65e3-120">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="e65e3-121">Dopo l'accesso verranno elencate tutte le sottoscrizioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="e65e3-121">All your available subscriptions will be listed after a successful sign-in.</span></span>

2. <span data-ttu-id="e65e3-122">Impostare il valore predefinito di hello sottoscrizione di Azure che si desidera toouse eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e65e3-122">Set hello default Azure subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="e65e3-123">`subscription ID or name`possono essere trovati nell'output di hello di hello `az login` o hello `az account list` comando.</span><span class="sxs-lookup"><span data-stu-id="e65e3-123">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="e65e3-124">Registrare il provider di hello eseguendo hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="e65e3-124">Register hello provider by running hello following command.</span></span> <span data-ttu-id="e65e3-125">I provider di risorse sono servizi che forniscono risorse per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e65e3-125">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="e65e3-126">Prima di poter distribuire hello risorsa di Azure che hello offerte di provider, è necessario registrare il provider di hello.</span><span class="sxs-lookup"><span data-stu-id="e65e3-126">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. <span data-ttu-id="e65e3-127">Creare un gruppo di risorse denominato `iot-gateway` nell'area Stati Uniti occidentali hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e65e3-127">Create a resource group named `iot-gateway` in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   <span data-ttu-id="e65e3-128">`westus`è il percorso di hello creare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e65e3-128">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="e65e3-129">Se si desidera toouse un'altra posizione, è possibile eseguire `az account list-locations -o table` toosee tutti hello Azure supporta percorsi.</span><span class="sxs-lookup"><span data-stu-id="e65e3-129">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="e65e3-130">Creare un hub IoT in hello `iot-gateway` gruppo di risorse eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e65e3-130">Create an IoT hub in hello `iot-gateway` resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

<span data-ttu-id="e65e3-131">Per impostazione predefinita, lo strumento hello crea un IoT Hub nel piano tariffario gratuito hello.</span><span class="sxs-lookup"><span data-stu-id="e65e3-131">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="e65e3-132">Per altre informazioni, vedere [Prezzi dell'hub Iot di Azure](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="e65e3-132">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="e65e3-133">nome Hello dell'hub IoT deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="e65e3-133">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="e65e3-134">È possibile creare una sola edizione F1 dell'hub IoT di Azure nell'ambito della propria sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e65e3-134">You can create only one F1 edition of Azure Iot Hub under your Azure subscription.</span></span>

## <a name="register-your-device-in-your-iot-hub"></a><span data-ttu-id="e65e3-135">Registrare il dispositivo nell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="e65e3-135">Register your device in your IoT hub</span></span>

<span data-ttu-id="e65e3-136">Ogni dispositivo che invia l'hub IoT tooyour messaggi e riceve messaggi dall'hub IoT deve essere registrato con un ID univoco.</span><span class="sxs-lookup"><span data-stu-id="e65e3-136">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>
<span data-ttu-id="e65e3-137">Registrare il dispositivo nell'hub IoT eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="e65e3-137">Register your device in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a><span data-ttu-id="e65e3-138">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="e65e3-138">Summary</span></span>

<span data-ttu-id="e65e3-139">È stato creato un hub IoT e il dispositivo logico è stato registrato con un'identità del dispositivo nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e65e3-139">You've created an IoT hub and registered your logical device with a device identity in your IoT hub.</span></span> <span data-ttu-id="e65e3-140">Si è pronti toolearn tooconfigure ed eseguire un gateway applicazione toosend campionamento dall'hub IoT tooyour dispositivo fisico hello di cloud.</span><span class="sxs-lookup"><span data-stu-id="e65e3-140">You're ready toolearn how tooconfigure and run a gateway sample application toosend data from your physical device tooyour IoT hub in hello cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e65e3-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e65e3-141">Next steps</span></span>
[<span data-ttu-id="e65e3-142">Configurare ed eseguire un'applicazione di esempio per il caricamento nel cloud del dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="e65e3-142">Configure and run a simulated device cloud upload sample application</span></span>](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)