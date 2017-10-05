---
title: 'Connettere Intel Edison (Node) ad Azure IoT: lezione 1: Distribuire l''app | Documentazione Microsoft'
description: Clonare l'applicazione C di esempio da GitHub ed eseguire gulp per distribuirla nella scheda Intel Edison. Questa applicazione di esempio fa lampeggiare il LED connesso alla scheda ogni due secondi.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: progetti led arduino, lampeggiamento led arduino, codice di lampeggiamento led arduino, programma di lampeggiamento arduino, esempio di lampeggiamento arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: ed2c21d0-c72c-4ac2-9e70-347e9a0711c0
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8490fbbf14183432c665165412f00955d6323580
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="4dbe9-105">Creare e distribuire l'applicazione per il lampeggiamento</span><span class="sxs-lookup"><span data-stu-id="4dbe9-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="4dbe9-106">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="4dbe9-106">What you will do</span></span>
<span data-ttu-id="4dbe9-107">Clonare l'applicazione C di esempio da GitHub e usare lo strumento gulp per distribuire l'applicazione di esempio in Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="4dbe9-107">Clone the sample C application from GitHub, and use the gulp tool to deploy the sample application to Intel Edison.</span></span> <span data-ttu-id="4dbe9-108">L'applicazione di esempio fa lampeggiare il LED connesso alla scheda ogni due secondi.</span><span class="sxs-lookup"><span data-stu-id="4dbe9-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="4dbe9-109">In caso di problemi, cercare le soluzioni nella [pagina sulla risoluzione dei problemi][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="4dbe9-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4dbe9-110">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="4dbe9-110">What you will learn</span></span>
* <span data-ttu-id="4dbe9-111">Come distribuire ed eseguire l'applicazione di esempio in Edison.</span><span class="sxs-lookup"><span data-stu-id="4dbe9-111">How to deploy and run the sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4dbe9-112">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="4dbe9-112">What you need</span></span>
<span data-ttu-id="4dbe9-113">È necessario aver completato le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="4dbe9-113">You must have successfully completed the following operations:</span></span>

* <span data-ttu-id="4dbe9-114">[Configurare il dispositivo][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="4dbe9-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="4dbe9-115">[Ottenere gli strumenti][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="4dbe9-115">[Get the tools][get-the-tools]</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="4dbe9-116">Aprire l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="4dbe9-116">Open the sample application</span></span>
<span data-ttu-id="4dbe9-117">Per aprire l'applicazione di esempio, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4dbe9-117">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="4dbe9-118">Clonare il repository di esempio da GitHub eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="4dbe9-118">Clone the sample repository from GitHub by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-edison-getting-started.git
   ```
2. <span data-ttu-id="4dbe9-119">Aprire l'applicazione di esempio in Visual Studio Code usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4dbe9-119">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd iot-hub-node-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Struttura del repository][repo-structure]

<span data-ttu-id="4dbe9-121">Il file nella sottocartella `app` è il file di origine chiave contenente il codice per controllare il LED.</span><span class="sxs-lookup"><span data-stu-id="4dbe9-121">The file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="4dbe9-122">Installare le dipendenze dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="4dbe9-122">Install application dependencies</span></span>
<span data-ttu-id="4dbe9-123">Installare le librerie e gli altri moduli necessari per l'applicazione di esempio eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="4dbe9-123">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="4dbe9-124">Configurare la connessione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="4dbe9-124">Configure the device connection</span></span>
<span data-ttu-id="4dbe9-125">Per configurare la connessione al dispositivo, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="4dbe9-125">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="4dbe9-126">Generare il file di configurazione del dispositivo eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="4dbe9-126">Generate the device configuration file by running the following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="4dbe9-127">Il file di configurazione `config-edison.json` contiene le credenziali utente usate per accedere a Edison.</span><span class="sxs-lookup"><span data-stu-id="4dbe9-127">The configuration file `config-edison.json` contains the user credentials you use to log in to Edison.</span></span> <span data-ttu-id="4dbe9-128">Per evitare la perdita delle credenziali utente, il file di configurazione viene generato nella sottocartella `.iot-hub-getting-started` della home directory del computer.</span><span class="sxs-lookup"><span data-stu-id="4dbe9-128">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="4dbe9-129">Aprire il file di configurazione del dispositivo in Visual Studio Code eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="4dbe9-129">Open the device configuration file in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="4dbe9-130">Sostituire i segnaposto `[device hostname or IP address]` e `[device password]` con l'indirizzo IP e la password annotati nella lezione precedente.</span><span class="sxs-lookup"><span data-stu-id="4dbe9-130">Replace the placeholder `[device hostname or IP address]` and `[device password]` with the IP address and password that you marked down in previous lesson.</span></span>

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="4dbe9-132">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="4dbe9-132">Congratulations!</span></span> <span data-ttu-id="4dbe9-133">La creazione della prima applicazione di esempio per Edison è completata.</span><span class="sxs-lookup"><span data-stu-id="4dbe9-133">You've successfully created the first sample application for Edison.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="4dbe9-134">Distribuire ed eseguire l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="4dbe9-134">Deploy and run the sample application</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="4dbe9-135">Distribuire ed eseguire l'app di esempio</span><span class="sxs-lookup"><span data-stu-id="4dbe9-135">Deploy and run the sample app</span></span>
<span data-ttu-id="4dbe9-136">Distribuire ed eseguire l'applicazione di esempio eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="4dbe9-136">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="4dbe9-137">Verificare il funzionamento dell'app</span><span class="sxs-lookup"><span data-stu-id="4dbe9-137">Verify the app works</span></span>
<span data-ttu-id="4dbe9-138">L'applicazione di esempio termina automaticamente dopo 20 lampeggiamenti del LED.</span><span class="sxs-lookup"><span data-stu-id="4dbe9-138">The sample application terminates automatically after the LED blinks for 20 times.</span></span> <span data-ttu-id="4dbe9-139">Se il LED non lampeggia, vedere la [guida alla risoluzione dei problemi][troubleshooting] per trovare le soluzioni ai problemi comuni.</span><span class="sxs-lookup"><span data-stu-id="4dbe9-139">If you don’t see the LED blinking, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

![LED lampeggiante][led-blinking]

## <a name="summary"></a><span data-ttu-id="4dbe9-141">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="4dbe9-141">Summary</span></span>
<span data-ttu-id="4dbe9-142">Sono stati installati gli strumenti necessari per usare Edison ed è stata distribuita un'applicazione di esempio che consente a Edison di far lampeggiare il LED.</span><span class="sxs-lookup"><span data-stu-id="4dbe9-142">You've installed the required tools to work with Edison and deployed a sample application to Edison to blink the LED.</span></span> <span data-ttu-id="4dbe9-143">È ora possibile creare, distribuire ed eseguire un'altra applicazione di esempio che connette Edison all'hub IoT di Azure per inviare e ricevere messaggi.</span><span class="sxs-lookup"><span data-stu-id="4dbe9-143">You can now create, deploy, and run another sample application that connects Edison to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4dbe9-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4dbe9-144">Next steps</span></span>
<span data-ttu-id="4dbe9-145">[Ottenere gli strumenti di Azure][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="4dbe9-145">[Get the Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
