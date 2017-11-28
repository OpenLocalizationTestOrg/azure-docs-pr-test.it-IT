---
title: 'Connect Intel Edison (C) tooAzure IoT - lezione 1: distribuire l''applicazione | Documenti Microsoft'
description: Clonazione di un'applicazione hello esempio C da GitHub ed eseguire gulp toodeploy questo tooyour applicazione Lavagna Edison Intel. Questa applicazione di esempio lampeggia hello LED connesso toohello Lavagna ogni due secondi.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: progetti led arduino, lampeggiamento led arduino, codice di lampeggiamento led arduino, programma di lampeggiamento arduino, esempio di lampeggiamento arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: b02dfd3f-28fd-4b52-8775-eb0eaf74d707
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: fa84fae812dd742a2ad4997a5e213c8e40e6fcf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="95420-105">Creare e distribuire un'applicazione hello blink</span><span class="sxs-lookup"><span data-stu-id="95420-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="95420-106">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="95420-106">What you will do</span></span>
<span data-ttu-id="95420-107">Applicazione di esempio C hello da GitHub clonare e usare hello gulp strumento toodeploy hello esempio applicazione tooIntel Edison.</span><span class="sxs-lookup"><span data-stu-id="95420-107">Clone hello sample C application from GitHub, and use hello gulp tool toodeploy hello sample application tooIntel Edison.</span></span> <span data-ttu-id="95420-108">applicazione di esempio Hello lampeggia hello LED connesso toohello Lavagna ogni due secondi.</span><span class="sxs-lookup"><span data-stu-id="95420-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="95420-109">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="95420-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="95420-110">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="95420-110">What you will learn</span></span>
* <span data-ttu-id="95420-111">Come applicazione in Edison esempio toodeploy e hello esecuzione.</span><span class="sxs-lookup"><span data-stu-id="95420-111">How toodeploy and run hello sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="95420-112">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="95420-112">What you need</span></span>
<span data-ttu-id="95420-113">È necessario che sia completata hello seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="95420-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="95420-114">[Configurare il dispositivo][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="95420-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="95420-115">[Ottenere strumenti hello][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="95420-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="95420-116">Applicazione di esempio hello aperto</span><span class="sxs-lookup"><span data-stu-id="95420-116">Open hello sample application</span></span>
<span data-ttu-id="95420-117">hello tooopen applicazione di esempio, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="95420-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="95420-118">Clonare il repository di esempio hello da GitHub eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="95420-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-edison-getting-started.git
   ```
2. <span data-ttu-id="95420-119">Aprire l'applicazione di esempio hello in Visual Studio Code eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="95420-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Struttura del repository][repo-structure]

<span data-ttu-id="95420-121">file Hello in hello `app` sottocartella è hello i file di origine della chiave che contiene hello codice toocontrol hello LED.</span><span class="sxs-lookup"><span data-stu-id="95420-121">hello file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="95420-122">Installare le dipendenze dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="95420-122">Install application dependencies</span></span>
<span data-ttu-id="95420-123">Installare le librerie di hello e altri moduli, che è necessario per l'applicazione di esempio hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="95420-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="95420-124">Configurare una connessione al dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="95420-124">Configure hello device connection</span></span>
<span data-ttu-id="95420-125">tooconfigure hello connessione al dispositivo, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="95420-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="95420-126">Generare file di configurazione dispositivo hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="95420-126">Generate hello device configuration file by running hello following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="95420-127">file di configurazione Hello `config-edison.json` contiene credenziali utente hello è utilizzare toolog tooEdison.</span><span class="sxs-lookup"><span data-stu-id="95420-127">hello configuration file `config-edison.json` contains hello user credentials you use toolog in tooEdison.</span></span> <span data-ttu-id="95420-128">perdita di hello tooavoid delle credenziali dell'utente, viene generato il file di configurazione di hello nella sottocartella hello `.iot-hub-getting-started` della cartella principale di hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="95420-128">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="95420-129">Aprire il file di configurazione dispositivo hello in Visual Studio Code eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="95420-129">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="95420-130">Sostituire il segnaposto hello `[device hostname or IP address]` e `[device password]` con indirizzo IP hello e una password che è contrassegnato come inattivo nella lezione precedente.</span><span class="sxs-lookup"><span data-stu-id="95420-130">Replace hello placeholder `[device hostname or IP address]` and `[device password]` with hello IP address and password that you marked down in previous lesson.</span></span>

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="95420-132">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="95420-132">Congratulations!</span></span> <span data-ttu-id="95420-133">È stato creato correttamente l'applicazione di esempio per Edison prima hello.</span><span class="sxs-lookup"><span data-stu-id="95420-133">You've successfully created hello first sample application for Edison.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="95420-134">Distribuire ed eseguire l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="95420-134">Deploy and run hello sample application</span></span>
### <a name="install-hello-azure-iot-hub-sdk-on-edison"></a><span data-ttu-id="95420-135">Installare hello Azure IoT Hub SDK in Edison</span><span class="sxs-lookup"><span data-stu-id="95420-135">Install hello Azure IoT Hub SDK on Edison</span></span>
<span data-ttu-id="95420-136">Installare hello Azure IoT Hub SDK in Edison eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="95420-136">Install hello Azure IoT Hub SDK on Edison by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="95420-137">Questa operazione potrebbe richiedere un toocomplete molto tempo, a seconda della connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="95420-137">This task might take a long time toocomplete, depending on your network connection.</span></span> <span data-ttu-id="95420-138">È necessario toobe eseguirlo una sola volta per uno Edison.</span><span class="sxs-lookup"><span data-stu-id="95420-138">It needs toobe run only once for one Edison.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="95420-139">Distribuire ed eseguire app di esempio hello</span><span class="sxs-lookup"><span data-stu-id="95420-139">Deploy and run hello sample app</span></span>
<span data-ttu-id="95420-140">Distribuire ed eseguire l'applicazione di esempio hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="95420-140">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="95420-141">Verificare il funzionamento dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="95420-141">Verify hello app works</span></span>
<span data-ttu-id="95420-142">applicazione di esempio Hello termina automaticamente dopo hello LED lampeggia per 20 volte.</span><span class="sxs-lookup"><span data-stu-id="95420-142">hello sample application terminates automatically after hello LED blinks for 20 times.</span></span> <span data-ttu-id="95420-143">Se non viene visualizzato hello LED è lampeggiante, vedere hello [risoluzione dei problemi guida] [ troubleshooting] per soluzioni ai problemi di toocommon.</span><span class="sxs-lookup"><span data-stu-id="95420-143">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

![LED lampeggiante][led-blinking]

## <a name="summary"></a><span data-ttu-id="95420-145">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="95420-145">Summary</span></span>
<span data-ttu-id="95420-146">È stato installato hello necessario strumenti toowork con Edison e distribuito un hello tooblink di tooEdison dall'applicazione di esempio LED.</span><span class="sxs-lookup"><span data-stu-id="95420-146">You've installed hello required tools toowork with Edison and deployed a sample application tooEdison tooblink hello LED.</span></span> <span data-ttu-id="95420-147">È ora possibile creare, distribuire e l'esecuzione di un'altra applicazione di esempio che si connette Edison tooAzure toosend IoT Hub e ricevere messaggi.</span><span class="sxs-lookup"><span data-stu-id="95420-147">You can now create, deploy, and run another sample application that connects Edison tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95420-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="95420-148">Next steps</span></span>
<span data-ttu-id="95420-149">[Ottenere hello gli strumenti di Azure][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="95420-149">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure_c.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking_c.jpg
[get-the-azure-tools]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
