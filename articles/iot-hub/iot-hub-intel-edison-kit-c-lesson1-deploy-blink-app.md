---
title: 'Connettere Intel Edison (C) ad Azure IoT: lezione 1: Distribuire l''applicazione | Documentazione Microsoft'
description: Clonare l'applicazione C di esempio da GitHub ed eseguire gulp per distribuirla nella scheda Intel Edison. Questa applicazione di esempio fa lampeggiare il LED connesso alla scheda ogni due secondi.
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
ms.openlocfilehash: c45ff5f41bdbc78da8532ffdcaaeec15c695f531
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="36b04-105">Creare e distribuire l'applicazione per il lampeggiamento</span><span class="sxs-lookup"><span data-stu-id="36b04-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="36b04-106">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="36b04-106">What you will do</span></span>
<span data-ttu-id="36b04-107">Clonare l'applicazione C di esempio da GitHub e usare lo strumento gulp per distribuire l'applicazione di esempio in Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="36b04-107">Clone the sample C application from GitHub, and use the gulp tool to deploy the sample application to Intel Edison.</span></span> <span data-ttu-id="36b04-108">L'applicazione di esempio fa lampeggiare il LED connesso alla scheda ogni due secondi.</span><span class="sxs-lookup"><span data-stu-id="36b04-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="36b04-109">In caso di problemi, cercare le soluzioni nella [pagina sulla risoluzione dei problemi][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="36b04-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="36b04-110">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="36b04-110">What you will learn</span></span>
* <span data-ttu-id="36b04-111">Come distribuire ed eseguire l'applicazione di esempio in Edison.</span><span class="sxs-lookup"><span data-stu-id="36b04-111">How to deploy and run the sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="36b04-112">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="36b04-112">What you need</span></span>
<span data-ttu-id="36b04-113">È necessario aver completato le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="36b04-113">You must have successfully completed the following operations:</span></span>

* <span data-ttu-id="36b04-114">[Configurare il dispositivo][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="36b04-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="36b04-115">[Ottenere gli strumenti][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="36b04-115">[Get the tools][get-the-tools]</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="36b04-116">Aprire l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="36b04-116">Open the sample application</span></span>
<span data-ttu-id="36b04-117">Per aprire l'applicazione di esempio, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="36b04-117">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="36b04-118">Clonare il repository di esempio da GitHub eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="36b04-118">Clone the sample repository from GitHub by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-edison-getting-started.git
   ```
2. <span data-ttu-id="36b04-119">Aprire l'applicazione di esempio in Visual Studio Code usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="36b04-119">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Struttura del repository][repo-structure]

<span data-ttu-id="36b04-121">Il file nella sottocartella `app` è il file di origine chiave contenente il codice per controllare il LED.</span><span class="sxs-lookup"><span data-stu-id="36b04-121">The file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="36b04-122">Installare le dipendenze dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="36b04-122">Install application dependencies</span></span>
<span data-ttu-id="36b04-123">Installare le librerie e gli altri moduli necessari per l'applicazione di esempio eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="36b04-123">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="36b04-124">Configurare la connessione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="36b04-124">Configure the device connection</span></span>
<span data-ttu-id="36b04-125">Per configurare la connessione al dispositivo, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="36b04-125">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="36b04-126">Generare il file di configurazione del dispositivo eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="36b04-126">Generate the device configuration file by running the following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="36b04-127">Il file di configurazione `config-edison.json` contiene le credenziali utente usate per accedere a Edison.</span><span class="sxs-lookup"><span data-stu-id="36b04-127">The configuration file `config-edison.json` contains the user credentials you use to log in to Edison.</span></span> <span data-ttu-id="36b04-128">Per evitare la perdita delle credenziali utente, il file di configurazione viene generato nella sottocartella `.iot-hub-getting-started` della home directory del computer.</span><span class="sxs-lookup"><span data-stu-id="36b04-128">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="36b04-129">Aprire il file di configurazione del dispositivo in Visual Studio Code eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="36b04-129">Open the device configuration file in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="36b04-130">Sostituire i segnaposto `[device hostname or IP address]` e `[device password]` con l'indirizzo IP e la password annotati nella lezione precedente.</span><span class="sxs-lookup"><span data-stu-id="36b04-130">Replace the placeholder `[device hostname or IP address]` and `[device password]` with the IP address and password that you marked down in previous lesson.</span></span>

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="36b04-132">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="36b04-132">Congratulations!</span></span> <span data-ttu-id="36b04-133">La creazione della prima applicazione di esempio per Edison è completata.</span><span class="sxs-lookup"><span data-stu-id="36b04-133">You've successfully created the first sample application for Edison.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="36b04-134">Distribuire ed eseguire l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="36b04-134">Deploy and run the sample application</span></span>
### <a name="install-the-azure-iot-hub-sdk-on-edison"></a><span data-ttu-id="36b04-135">Installare Azure IoT SDK per hub in Edison</span><span class="sxs-lookup"><span data-stu-id="36b04-135">Install the Azure IoT Hub SDK on Edison</span></span>
<span data-ttu-id="36b04-136">Installare Azure IoT SDK per hub in Edison eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="36b04-136">Install the Azure IoT Hub SDK on Edison by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="36b04-137">A seconda della connessione di rete, l'operazione potrebbe richiedere molto tempo.</span><span class="sxs-lookup"><span data-stu-id="36b04-137">This task might take a long time to complete, depending on your network connection.</span></span> <span data-ttu-id="36b04-138">Per Edison, è necessario eseguirlo solo una volta.</span><span class="sxs-lookup"><span data-stu-id="36b04-138">It needs to be run only once for one Edison.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="36b04-139">Distribuire ed eseguire l'app di esempio</span><span class="sxs-lookup"><span data-stu-id="36b04-139">Deploy and run the sample app</span></span>
<span data-ttu-id="36b04-140">Distribuire ed eseguire l'applicazione di esempio eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="36b04-140">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="36b04-141">Verificare il funzionamento dell'app</span><span class="sxs-lookup"><span data-stu-id="36b04-141">Verify the app works</span></span>
<span data-ttu-id="36b04-142">L'applicazione di esempio termina automaticamente dopo 20 lampeggiamenti del LED.</span><span class="sxs-lookup"><span data-stu-id="36b04-142">The sample application terminates automatically after the LED blinks for 20 times.</span></span> <span data-ttu-id="36b04-143">Se il LED non lampeggia, vedere la [guida alla risoluzione dei problemi][troubleshooting] per trovare le soluzioni ai problemi comuni.</span><span class="sxs-lookup"><span data-stu-id="36b04-143">If you don’t see the LED blinking, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

![LED lampeggiante][led-blinking]

## <a name="summary"></a><span data-ttu-id="36b04-145">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="36b04-145">Summary</span></span>
<span data-ttu-id="36b04-146">Sono stati installati gli strumenti necessari per usare Edison ed è stata distribuita un'applicazione di esempio che consente a Edison di far lampeggiare il LED.</span><span class="sxs-lookup"><span data-stu-id="36b04-146">You've installed the required tools to work with Edison and deployed a sample application to Edison to blink the LED.</span></span> <span data-ttu-id="36b04-147">È ora possibile creare, distribuire ed eseguire un'altra applicazione di esempio che connette Edison all'hub IoT di Azure per inviare e ricevere messaggi.</span><span class="sxs-lookup"><span data-stu-id="36b04-147">You can now create, deploy, and run another sample application that connects Edison to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36b04-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="36b04-148">Next steps</span></span>
<span data-ttu-id="36b04-149">[Ottenere gli strumenti di Azure][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="36b04-149">[Get the Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure_c.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking_c.jpg
[get-the-azure-tools]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
