---
featureFlags: usabilla
title: 'Connettersi Raspberry Pi (nodo) tooAzure IoT - lezione 2: registrazione del dispositivo | Documenti Microsoft'
description: "Creare un gruppo di risorse, creare un hub IoT di Azure e registrare Pi in hello del Registro di sistema di IoT Hub identità tramite l'interfaccia CLI di Azure."
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
ms.openlocfilehash: 97533298d52d1187c49a4c35ddda922d6e45c87d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="83a88-104">Creare l'hub IoT e registrare Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="83a88-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="83a88-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="83a88-105">What you will do</span></span>
* <span data-ttu-id="83a88-106">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="83a88-106">Create a resource group.</span></span>
* <span data-ttu-id="83a88-107">Creare l'hub IoT di Azure nel gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="83a88-107">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="83a88-108">Aggiungere Raspberry Pi 3 toohello Azure IoT hub utilizzando hello Azure interfaccia della riga di comando (CLI di Azure).</span><span class="sxs-lookup"><span data-stu-id="83a88-108">Add Raspberry Pi 3 toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="83a88-109">Quando si usa l'hub IoT Azure CLI tooadd Pi tooyour, servizio hello genera una chiave per Pi tooauthenticate con servizio hello.</span><span class="sxs-lookup"><span data-stu-id="83a88-109">When you use Azure CLI tooadd Pi tooyour IoT hub, hello service generates a key for Pi tooauthenticate with hello service.</span></span> <span data-ttu-id="83a88-110">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="83a88-110">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="83a88-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="83a88-111">What you will learn</span></span>
<span data-ttu-id="83a88-112">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="83a88-112">In this article, you will learn:</span></span>
* <span data-ttu-id="83a88-113">Come toouse CLI di Azure toocreate un hub IoT</span><span class="sxs-lookup"><span data-stu-id="83a88-113">How toouse Azure CLI toocreate an IoT hub</span></span>
* <span data-ttu-id="83a88-114">Come toocreate un'identità del dispositivo per Pi nell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="83a88-114">How toocreate a device identity for Pi in your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="83a88-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="83a88-115">What you need</span></span>
* <span data-ttu-id="83a88-116">Un account Azure</span><span class="sxs-lookup"><span data-stu-id="83a88-116">An Azure account</span></span>
* <span data-ttu-id="83a88-117">Un Mac o in un computer Windows con hello Azure CLI installato</span><span class="sxs-lookup"><span data-stu-id="83a88-117">A Mac or a Windows computer with hello Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="83a88-118">Creare l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="83a88-118">Create your IoT hub</span></span>
<span data-ttu-id="83a88-119">L'hub IoT di Azure consente di connettersi a milioni di asset IoT, monitorarli e gestirli.</span><span class="sxs-lookup"><span data-stu-id="83a88-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="83a88-120">toocreate l'hub IoT, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="83a88-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="83a88-121">Accedi tooyour account Azure eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="83a88-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="83a88-122">Dopo l'accesso vengono elencate tutte le sottoscrizioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="83a88-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="83a88-123">Impostare la sottoscrizione predefinita hello che si desidera toouse eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="83a88-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="83a88-124">`subscription ID or name`possono essere trovati nell'output di hello di hello `az login` o hello `az account list` comando.</span><span class="sxs-lookup"><span data-stu-id="83a88-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="83a88-125">Registrare il provider di hello eseguendo hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="83a88-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="83a88-126">I provider di risorse sono servizi che forniscono risorse per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="83a88-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="83a88-127">Prima di poter distribuire hello risorsa di Azure che hello offerte di provider, è necessario registrare il provider di hello.</span><span class="sxs-lookup"><span data-stu-id="83a88-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="83a88-128">Creare un gruppo di risorse denominato iot-esempio nell'area Stati Uniti occidentali hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="83a88-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="83a88-129">`westus`è il percorso di hello creare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="83a88-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="83a88-130">Se si desidera toouse un'altra posizione, è possibile eseguire `az account list-locations -o table` toosee tutti hello Azure supporta percorsi.</span><span class="sxs-lookup"><span data-stu-id="83a88-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>
 
5. <span data-ttu-id="83a88-131">Creare un hub IoT nel gruppo di risorse di esempio di iot hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="83a88-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="83a88-132">Per impostazione predefinita, lo strumento hello crea un IoT Hub nel piano tariffario gratuito hello.</span><span class="sxs-lookup"><span data-stu-id="83a88-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="83a88-133">Per altre informazioni, vedere [Prezzi dell'hub Iot di Azure](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="83a88-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="83a88-134">nome Hello dell'hub IoT deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="83a88-134">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="83a88-135">È possibile creare una sola edizione F1 dell'hub IoT di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="83a88-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="83a88-136">Registrare il dispositivo Pi nell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="83a88-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="83a88-137">Ogni dispositivo che invia l'hub IoT tooyour messaggi e riceve messaggi dall'hub IoT deve essere registrato con un ID univoco.</span><span class="sxs-lookup"><span data-stu-id="83a88-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span> <span data-ttu-id="83a88-138">Si verrà utilizzata tooregister CLI di Azure il Pi e creare un certificato autofirmato x. 509 per l'autenticazione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="83a88-138">You will use Azure CLI tooregister your Pi and create a self-signed X.509 certificate for device authentication.</span></span>

<span data-ttu-id="83a88-139">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="83a88-139">Run hello following command:</span></span>

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a><span data-ttu-id="83a88-140">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="83a88-140">Summary</span></span>
<span data-ttu-id="83a88-141">È stato creato un hub IoT e il dispositivo Pi è stato registrato con un'identità del dispositivo nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="83a88-141">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="83a88-142">Si è pronti toolearn come toosend messaggi dall'hub IoT tooyour di pi greco.</span><span class="sxs-lookup"><span data-stu-id="83a88-142">You're ready toolearn how toosend messages from Pi tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83a88-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="83a88-143">Next steps</span></span>
[<span data-ttu-id="83a88-144">Creare un'app di Azure (funzione) e un tooprocess di account di archiviazione di Azure e archiviare i messaggi di hub IoT</span><span class="sxs-lookup"><span data-stu-id="83a88-144">Create an Azure function app and an Azure storage account tooprocess and store IoT hub messages</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)

