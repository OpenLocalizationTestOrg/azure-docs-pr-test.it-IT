---
title: 'Connettersi Edison Intel (nodo) tooAzure IoT - lezione 4: ricezione messaggi | Documenti Microsoft'
description: "Un'applicazione di esempio viene eseguita in Edison e monitora i messaggi in ingresso dall'hub IoT. Una nuova attività gulp invia messaggi tooEdison da hello di tooblink l'hub IoT LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: led di controllo arduino dal web, led di controllo arduino tramite web
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: bc738bf6-e38d-4024-82d7-39b6c2d4bacb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: aab0ced4810dd3d4f5ba636940b06563f1db9241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="15db0-105">Eseguire un tooreceive di applicazione di esempio i messaggi da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="15db0-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="15db0-106">Questo articolo illustra come distribuire un'applicazione di esempio in Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="15db0-106">In this article, you deploy a sample application on Intel Edison.</span></span> <span data-ttu-id="15db0-107">applicazione di esempio Hello controlla i messaggi in ingresso dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="15db0-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="15db0-108">Inoltre si esegue un'attività gulp su tooEdison di messaggi toosend il computer dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="15db0-108">You also run a gulp task on your computer toosend messages tooEdison from your IoT hub.</span></span> <span data-ttu-id="15db0-109">Quando l'applicazione di esempio hello riceve messaggi hello, lampeggia hello LED.</span><span class="sxs-lookup"><span data-stu-id="15db0-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="15db0-110">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="15db0-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="15db0-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="15db0-111">What you will do</span></span>
* <span data-ttu-id="15db0-112">Connettere l'hub IoT hello esempio applicazione tooyour.</span><span class="sxs-lookup"><span data-stu-id="15db0-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="15db0-113">Distribuire ed eseguire l'applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="15db0-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="15db0-114">Invio di messaggi dal hello di IoT hub tooEdison tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="15db0-114">Send messages from your IoT hub tooEdison tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="15db0-115">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="15db0-115">What you will learn</span></span>
<span data-ttu-id="15db0-116">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="15db0-116">In this article, you will learn:</span></span>
* <span data-ttu-id="15db0-117">La modalità in ingresso toomonitor dei messaggi dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="15db0-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="15db0-118">La modalità toosend cloud a dispositivo dei messaggi dal tooEdison hub IoT.</span><span class="sxs-lookup"><span data-stu-id="15db0-118">How toosend cloud-to-device messages from your IoT hub tooEdison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="15db0-119">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="15db0-119">What you need</span></span>
* <span data-ttu-id="15db0-120">Intel Edison, impostato per l'uso.</span><span class="sxs-lookup"><span data-stu-id="15db0-120">Intel Edison, set up for use.</span></span> <span data-ttu-id="15db0-121">toolearn tooset backup Edison, vedere [configurare il dispositivo][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="15db0-121">toolearn how tooset up Edison, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="15db0-122">Un hub IoT creato nella propria sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="15db0-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="15db0-123">toolearn come toocreate l'hub IoT, vedere [creare l'IoT Hub Azure][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="15db0-123">toolearn how toocreate your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="15db0-124">Collegare hello esempio applicazione tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="15db0-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="15db0-125">Assicurarsi che si è nella cartella repository hello `iot-hub-node-edison-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="15db0-125">Make sure that you're in hello repo folder `iot-hub-node-edison-getting-started`.</span></span> <span data-ttu-id="15db0-126">Aprire l'applicazione di esempio hello in Visual Studio Code eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="15db0-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="15db0-127">file Hello in hello `app` sottocartella è hello i file di origine della chiave che contiene i messaggi in ingresso hello codice toomonitor dall'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="15db0-127">hello file in hello `app` subfolder is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="15db0-128">Hello `blinkLED` funzione lampeggia hello LED.</span><span class="sxs-lookup"><span data-stu-id="15db0-128">hello `blinkLED` function blinks hello LED.</span></span>

   ![Struttura repository nell'applicazione di esempio hello][repo-structure]
2. <span data-ttu-id="15db0-130">Inizializzare i file di configurazione hello eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="15db0-130">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="15db0-131">Se è stato completato i passaggi di hello in [creare un account di archiviazione e l'app Azure funzione] [ create-an-azure-function-app-and-storage-account] su questo computer, tutte le configurazioni di hello vengono ereditate, pertanto è possibile ignorare hello passaggio toohello attività di distribuzione e in esecuzione l'applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="15db0-131">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all hello configurations are inherited, so you can skip hello step toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="15db0-132">Se è stato completato i passaggi di hello in [creare un account di archiviazione e l'app Azure funzione] [ create-an-azure-function-app-and-storage-account] in un computer diverso, è necessario segnaposto hello tooreplace hello `config-edison.json` file.</span><span class="sxs-lookup"><span data-stu-id="15db0-132">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need tooreplace hello placeholders in hello `config-edison.json` file.</span></span> <span data-ttu-id="15db0-133">Hello `config-edison.json` file si trova nella sottocartella hello della cartella principale.</span><span class="sxs-lookup"><span data-stu-id="15db0-133">hello `config-edison.json` file is in hello subfolder of your home folder.</span></span>

   ![Contenuto del file di configurazione edison.json hello](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * <span data-ttu-id="15db0-135">Sostituire **[nome host di dispositivo o indirizzo IP]** con indirizzo IP del dispositivo hello è contrassegnato come inattivo quando è stato configurato il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="15db0-135">Replace **[device hostname or IP address]** with hello device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="15db0-136">Sostituire **[stringa di connessione dispositivo IoT]** con stringa di connessione hello dispositivo che si ottiene eseguendo hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` comando.</span><span class="sxs-lookup"><span data-stu-id="15db0-136">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="15db0-137">Sostituire **[stringa di connessione hub IoT]** con stringa di connessione hub IoT che si ottiene eseguendo hello hello `az iot hub show-connection-string --name {my hub name}` comando.</span><span class="sxs-lookup"><span data-stu-id="15db0-137">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="15db0-138">Distribuire ed eseguire l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="15db0-138">Deploy and run hello sample application</span></span>
<span data-ttu-id="15db0-139">Distribuire ed eseguire l'applicazione di esempio hello Edison eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="15db0-139">Deploy and run hello sample application on Edison by running hello following commands:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="15db0-140">comando gulp Hello distribuisce tooEdison applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="15db0-140">hello gulp command deploys hello sample application tooEdison.</span></span> <span data-ttu-id="15db0-141">Quindi, viene eseguita un'applicazione hello Edison e un'attività separata nell'host computer toosend 20 blink messaggi tooEdison dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="15db0-141">Then, it runs hello application on Edison and a separate task on your host computer toosend 20 blink messages tooEdison from your IoT hub.</span></span>

<span data-ttu-id="15db0-142">Quando si esegue l'applicazione di esempio hello, avvia l'ascolto toomessages dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="15db0-142">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="15db0-143">Nel frattempo, attività gulp hello invia messaggi di "blink" diversi dai tooEdison hub IoT.</span><span class="sxs-lookup"><span data-stu-id="15db0-143">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooEdison.</span></span> <span data-ttu-id="15db0-144">Per ogni messaggio blink Edison riceve, applicazione di esempio hello chiama hello `blinkLED` hello tooblink funzione LED.</span><span class="sxs-lookup"><span data-stu-id="15db0-144">For each blink message that Edison receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="15db0-145">Dovrebbe essere blink LED hello ogni due secondi come hello gulp attività inviati 20 messaggi dal tooEdison hub IoT.</span><span class="sxs-lookup"><span data-stu-id="15db0-145">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooEdison.</span></span> <span data-ttu-id="15db0-146">Hello ultimo uno è un messaggio "stop" che interrompe l'esecuzione di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="15db0-146">hello last one is a "stop" message that stops hello application from running.</span></span>

![Applicazione di esempio con comando gulp e messaggi di lampeggiamento][gulp-command-and-blink-messages]

## <a name="summary"></a><span data-ttu-id="15db0-148">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="15db0-148">Summary</span></span>
<span data-ttu-id="15db0-149">I messaggi inviati correttamente dal hello di IoT hub tooEdison tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="15db0-149">You’ve successfully sent messages from your IoT hub tooEdison tooblink hello LED.</span></span> <span data-ttu-id="15db0-150">attività successiva Hello è facoltativo: modificare hello e disattivare il comportamento di hello LED.</span><span class="sxs-lookup"><span data-stu-id="15db0-150">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15db0-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="15db0-151">Next steps</span></span>
<span data-ttu-id="15db0-152">[Modificare hello e disattivare il comportamento di hello LED][change-the-on-and-off-behavior-of-the-led]</span><span class="sxs-lookup"><span data-stu-id="15db0-152">[Change hello on and off behavior of hello LED][change-the-on-and-off-behavior-of-the-led]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md