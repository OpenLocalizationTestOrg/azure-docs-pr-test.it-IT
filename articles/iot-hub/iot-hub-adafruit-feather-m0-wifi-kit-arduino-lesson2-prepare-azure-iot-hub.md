---
title: 'Connettersi Arduino tooAzure IoT - lezione 2: registrazione del dispositivo | Documenti Microsoft'
description: Creare un gruppo di risorse, creare un hub IoT di Azure e registrare Adafruit sfumatura M0 WiFi nell'hub IoT Azure hello utilizzando hello CLI di Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: connessione arduino toocloud, hub iot di azure, internet del cloud di operazioni, l'hub iot azure creare un dispositivo, arduino cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 5edc690b-7a1d-4ebc-b011-ff27bfffe6e8
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ca362f9c143dd3a98bf47a66b63a9725a0ffc2d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-your-adafruit-feather-m0-wifi-arduino-board"></a><span data-ttu-id="ffcf1-104">Creare l'hub IoT e registrare la scheda Adafruit Feather M0 WiFi Arduino</span><span class="sxs-lookup"><span data-stu-id="ffcf1-104">Create your IoT hub and register your Adafruit Feather M0 WiFi Arduino board</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="ffcf1-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="ffcf1-105">What you will do</span></span>
* <span data-ttu-id="ffcf1-106">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ffcf1-106">Create a resource group.</span></span>
* <span data-ttu-id="ffcf1-107">Creare l'hub IoT di Azure nel gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="ffcf1-107">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="ffcf1-108">Aggiungere l'hub IoT di Azure di Arduino Lavagna toohello utilizzando hello Azure interfaccia della riga di comando (CLI di Azure).</span><span class="sxs-lookup"><span data-stu-id="ffcf1-108">Add your Arduino board toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="ffcf1-109">Quando si usa hello Azure CLI tooadd l'hub IoT di Arduino Lavagna tooyour, servizio hello genera una chiave per il tooauthenticate Lavagna Arduino con servizio hello.</span><span class="sxs-lookup"><span data-stu-id="ffcf1-109">When you use hello Azure CLI tooadd your Arduino board tooyour IoT hub, hello service generates a key for your Arduino board tooauthenticate with hello service.</span></span> <span data-ttu-id="ffcf1-110">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshoot].</span><span class="sxs-lookup"><span data-stu-id="ffcf1-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshoot].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ffcf1-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="ffcf1-111">What you will learn</span></span>
<span data-ttu-id="ffcf1-112">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="ffcf1-112">In this article, you will learn:</span></span>
* <span data-ttu-id="ffcf1-113">Come un hub IoT toouse hello toocreate CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="ffcf1-113">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
* <span data-ttu-id="ffcf1-114">Come un'identità del dispositivo per il Arduino toocreate board nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ffcf1-114">How toocreate a device identity for your Arduino board in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ffcf1-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="ffcf1-115">What you need</span></span>
* <span data-ttu-id="ffcf1-116">Un account Azure</span><span class="sxs-lookup"><span data-stu-id="ffcf1-116">An Azure account</span></span>
* <span data-ttu-id="ffcf1-117">Un computer con hello Azure CLI installato</span><span class="sxs-lookup"><span data-stu-id="ffcf1-117">A computer with hello Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="ffcf1-118">Creare l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="ffcf1-118">Create your IoT hub</span></span>
<span data-ttu-id="ffcf1-119">L'hub IoT di Azure consente di connettersi a milioni di asset IoT, monitorarli e gestirli.</span><span class="sxs-lookup"><span data-stu-id="ffcf1-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="ffcf1-120">toocreate l'hub IoT, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="ffcf1-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="ffcf1-121">Accedi tooyour account Azure eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ffcf1-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="ffcf1-122">Dopo l'accesso vengono elencate tutte le sottoscrizioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="ffcf1-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="ffcf1-123">Impostare la sottoscrizione predefinita hello che si desidera toouse eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ffcf1-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="ffcf1-124">`subscription ID or name`possono essere trovati nell'output di hello di hello `az login` o hello `az account list` comando.</span><span class="sxs-lookup"><span data-stu-id="ffcf1-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="ffcf1-125">Registrare il provider di hello eseguendo hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="ffcf1-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="ffcf1-126">I provider di risorse sono servizi che forniscono risorse per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ffcf1-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="ffcf1-127">Prima di poter distribuire hello risorsa di Azure che hello offerte di provider, è necessario registrare il provider di hello.</span><span class="sxs-lookup"><span data-stu-id="ffcf1-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="ffcf1-128">Creare un gruppo di risorse denominato iot-esempio nell'area Stati Uniti occidentali hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ffcf1-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="ffcf1-129">`westus`è il percorso di hello creare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ffcf1-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="ffcf1-130">Se si desidera toouse un'altra posizione, è possibile eseguire `az account list-locations -o table` toosee tutti hello Azure supporta percorsi.</span><span class="sxs-lookup"><span data-stu-id="ffcf1-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="ffcf1-131">Creare un hub IoT nel gruppo di risorse di esempio di iot hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ffcf1-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="ffcf1-132">Per impostazione predefinita, lo strumento hello crea un IoT Hub nel piano tariffario gratuito hello.</span><span class="sxs-lookup"><span data-stu-id="ffcf1-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="ffcf1-133">Per altre informazioni, vedere [Prezzi dell'hub Iot di Azure](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="ffcf1-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="ffcf1-134">nome Hello dell'hub IoT deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="ffcf1-134">hello name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="ffcf1-135">È possibile creare una sola edizione F1 dell'hub IoT di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ffcf1-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-your-arduino-board-in-your-iot-hub"></a><span data-ttu-id="ffcf1-136">Registrare la scheda Arduino nell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="ffcf1-136">Register your Arduino board in your IoT hub</span></span>
<span data-ttu-id="ffcf1-137">Ogni dispositivo che invia l'hub IoT tooyour messaggi e riceve messaggi dall'hub IoT deve essere registrato con un ID univoco.</span><span class="sxs-lookup"><span data-stu-id="ffcf1-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="ffcf1-138">Registrare la scheda Arduino nell'hub IoT con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ffcf1-138">Register your Arduino board in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mym0wifi --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="ffcf1-139">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="ffcf1-139">Summary</span></span>
<span data-ttu-id="ffcf1-140">È stato creato un hub IoT ed è stata registrata una scheda Arduino con un'identità di dispositivo nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ffcf1-140">You've created an IoT hub and registered your Arduino board with a device identity in your IoT hub.</span></span> <span data-ttu-id="ffcf1-141">Si è pronti toolearn come toosend messaggi dall'hub IoT tooyour di Arduino Lavagna.</span><span class="sxs-lookup"><span data-stu-id="ffcf1-141">You're ready toolearn how toosend messages from your Arduino board tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffcf1-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ffcf1-142">Next steps</span></span>
<span data-ttu-id="ffcf1-143">[Creare un'app di Azure (funzione) e un hub IoT tooprocess e l'archivio del account di archiviazione di Azure messaggi][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="ffcf1-143">[Create an Azure function app and an Azure Storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshoot]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md