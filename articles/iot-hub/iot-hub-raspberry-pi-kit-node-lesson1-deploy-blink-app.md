---
featureFlags: usabilla
title: 'Connettere Raspberry Pi (Node) ad Azure IoT: lezione 1: Distribuire l''app | Documentazione Microsoft'
description: Clonare l'applicazione Node.js di esempio da GitHub e usare gulp per distribuire l'applicazione sulla scheda di Raspberry Pi 3. Questa applicazione di esempio fa lampeggiare il LED connesso alla scheda ogni due secondi.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: lampeggiamento led raspberry pi, far lampeggiare il led con raspberry pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: a5a03a57-fe86-416f-90ff-6eca17775842
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8b73000c166950172c07b8e188025dc9da5bc011
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="f32a0-105">Creare e distribuire l'applicazione per il lampeggiamento</span><span class="sxs-lookup"><span data-stu-id="f32a0-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="f32a0-106">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="f32a0-106">What you will do</span></span>
<span data-ttu-id="f32a0-107">Clonare l'applicazione Node.js di esempio da GitHub e usare lo strumento gulp per distribuire l'applicazione di esempio in Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="f32a0-107">Clone the sample Node.js application from GitHub and use the gulp tool to deploy the sample application to your Raspberry Pi 3.</span></span> <span data-ttu-id="f32a0-108">L'applicazione di esempio fa lampeggiare il LED connesso alla scheda ogni due secondi.</span><span class="sxs-lookup"><span data-stu-id="f32a0-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="f32a0-109">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f32a0-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f32a0-110">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="f32a0-110">What you will learn</span></span>
<span data-ttu-id="f32a0-111">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="f32a0-111">In this article, you will learn:</span></span>

* <span data-ttu-id="f32a0-112">Come usare `device-discover-cli` per recuperare le informazioni di rete relative al dispositivo Pi.</span><span class="sxs-lookup"><span data-stu-id="f32a0-112">How to use the `device-discover-cli` tool to retrieve networking information about Pi.</span></span>
* <span data-ttu-id="f32a0-113">Come distribuire ed eseguire l'applicazione di esempio nel dispositivo Pi.</span><span class="sxs-lookup"><span data-stu-id="f32a0-113">How to deploy and run the sample application on Pi.</span></span>
* <span data-ttu-id="f32a0-114">Come effettuare la distribuzione e il debug di applicazioni eseguite in remoto in Pi.</span><span class="sxs-lookup"><span data-stu-id="f32a0-114">How to deploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f32a0-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="f32a0-115">What you need</span></span>
<span data-ttu-id="f32a0-116">È necessario aver completato le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f32a0-116">You must have successfully completed the following operations:</span></span>

* [<span data-ttu-id="f32a0-117">Configurare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="f32a0-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md)
* [<span data-ttu-id="f32a0-118">Ottenere gli strumenti</span><span class="sxs-lookup"><span data-stu-id="f32a0-118">Get the tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

## <a name="obtain-the-ip-address-and-host-name-of-pi"></a><span data-ttu-id="f32a0-119">Ottenere l'indirizzo IP e il nome host del dispositivo Pi</span><span class="sxs-lookup"><span data-stu-id="f32a0-119">Obtain the IP address and host name of Pi</span></span>
<span data-ttu-id="f32a0-120">Aprire il prompt dei comandi in Windows o una finestra del terminale in macOS o Ubuntu e quindi eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="f32a0-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run the following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="f32a0-121">L'output visualizzato dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f32a0-121">You should see an output that is similar to the following:</span></span>

![Individuazione del dispositivo](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="f32a0-123">Prendere nota di `IP address` e `hostname` del dispositivo Pi.</span><span class="sxs-lookup"><span data-stu-id="f32a0-123">Take note of the `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="f32a0-124">Queste informazioni saranno necessarie più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="f32a0-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="f32a0-125">Verificare che Pi sia connesso alla stessa rete del computer.</span><span class="sxs-lookup"><span data-stu-id="f32a0-125">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="f32a0-126">Se il computer è connesso a una rete wireless mentre il dispositivo Pi è connesso a una rete cablata, ad esempio, l'indirizzo IP potrebbe non essere incluso nell'output di devdisco.</span><span class="sxs-lookup"><span data-stu-id="f32a0-126">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="f32a0-127">Clonare l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="f32a0-127">Clone the sample application</span></span>
<span data-ttu-id="f32a0-128">Per aprire il codice di esempio, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f32a0-128">To open the sample code, follow these steps:</span></span>

1. <span data-ttu-id="f32a0-129">Clonare il repository di esempio da GitHub eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="f32a0-129">Clone the sample repository from GitHub by running the following command:</span></span>
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started.git
   ```
2. <span data-ttu-id="f32a0-130">Aprire l'applicazione di esempio in Visual Studio Code usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f32a0-130">Open the sample application in Visual Studio Code by running the following commands:</span></span>
   
   ```bash
   cd iot-hub-node-raspberrypi-getting-started
   cd Lesson1
   code .
   ```

![Struttura del repository](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-mac.png)

<span data-ttu-id="f32a0-132">Il file `app.js` nella sottocartella `app` è il file di origine chiave contenente il codice per controllare il LED.</span><span class="sxs-lookup"><span data-stu-id="f32a0-132">The `app.js` file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="f32a0-133">Installare le dipendenze dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f32a0-133">Install application dependencies</span></span>
<span data-ttu-id="f32a0-134">Installare le librerie e gli altri moduli necessari per l'applicazione di esempio eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="f32a0-134">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="f32a0-135">Configurare la connessione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="f32a0-135">Configure the device connection</span></span>
<span data-ttu-id="f32a0-136">Per configurare la connessione al dispositivo, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="f32a0-136">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="f32a0-137">Generare il file di configurazione del dispositivo eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="f32a0-137">Generate the device configuration file by running the following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="f32a0-138">Il file di configurazione `config-raspberrypi.json` contiene le credenziali utente usate per accedere al dispositivo Pi.</span><span class="sxs-lookup"><span data-stu-id="f32a0-138">The configuration file `config-raspberrypi.json` contains the user credentials you use to log in to Pi.</span></span> <span data-ttu-id="f32a0-139">Per evitare la perdita delle credenziali utente, il file di configurazione viene generato nella sottocartella `.iot-hub-getting-started` della home directory del computer.</span><span class="sxs-lookup"><span data-stu-id="f32a0-139">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="f32a0-140">Aprire il file di configurazione del dispositivo in Visual Studio Code eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="f32a0-140">Open the device configuration file in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
3. <span data-ttu-id="f32a0-141">Sostituire il segnaposto `[device hostname or IP address]` con l'indirizzo IP o il nome host ottenuto nella sezione "Ottenere l'indirizzo IP e il nome host del dispositivo Pi".</span><span class="sxs-lookup"><span data-stu-id="f32a0-141">Replace the placeholder `[device hostname or IP address]` with the IP address or the host name that you got previously in "Obtain the IP address and host name of Pi."</span></span>
   
   ![Config.json](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="f32a0-143">È possibile usare una chiave SSH al posto di nome utente e password quando ci si connette a Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="f32a0-143">You can use SSH key instead of user name and password when connecting to Raspberry Pi.</span></span> <span data-ttu-id="f32a0-144">Per eseguire questa operazione è necessario generare la chiave usando **ssh-keygen** e **pi ssh-copy-id @\<indirizzo dispositivo\>**.</span><span class="sxs-lookup"><span data-stu-id="f32a0-144">In order to do this you will have to generate the key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="f32a0-145">In Windows, questi comandi sono disponibili in **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="f32a0-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="f32a0-146">In MacOS è necessario eseguire **brew install ssh-copy-id**.</span><span class="sxs-lookup"><span data-stu-id="f32a0-146">On MacOS you need to run **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="f32a0-147">Dopo aver caricato correttamente la chiave in Raspberry Pi, sostituire **device_password** con la proprietà **device_key_path** in **config raspberrypi.json**.</span><span class="sxs-lookup"><span data-stu-id="f32a0-147">After successfully uploading the key to the Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="f32a0-148">Le righe aggiornate saranno simili alle seguenti:</span><span class="sxs-lookup"><span data-stu-id="f32a0-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="f32a0-149">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="f32a0-149">Congratulations!</span></span> <span data-ttu-id="f32a0-150">La creazione della prima applicazione di esempio per Pi è completata.</span><span class="sxs-lookup"><span data-stu-id="f32a0-150">You've successfully created the first sample application for Pi.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="f32a0-151">Distribuire ed eseguire l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="f32a0-151">Deploy and run the sample application</span></span>
### <a name="install-nodejs-and-npm-on-pi"></a><span data-ttu-id="f32a0-152">Installare Node.js e NPM in Pi</span><span class="sxs-lookup"><span data-stu-id="f32a0-152">Install Node.js and NPM on Pi</span></span>
<span data-ttu-id="f32a0-153">Installare Node.js e NPM in Pi eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="f32a0-153">Install Node.js and NPM on Pi by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="f32a0-154">Per completare questa attività, la prima volta che viene eseguita potrebbero essere necessari 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="f32a0-154">This task might take 10 minutes to complete the first time you run it.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="f32a0-155">Distribuire ed eseguire l'app di esempio</span><span class="sxs-lookup"><span data-stu-id="f32a0-155">Deploy and run the sample app</span></span>
<span data-ttu-id="f32a0-156">Distribuire ed eseguire l'applicazione di esempio eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="f32a0-156">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="f32a0-157">Verificare il funzionamento dell'app</span><span class="sxs-lookup"><span data-stu-id="f32a0-157">Verify the app works</span></span>
<span data-ttu-id="f32a0-158">Il LED sul dispositivo Pi dovrebbe ora lampeggiare ogni due secondi.</span><span class="sxs-lookup"><span data-stu-id="f32a0-158">You should now see the LED on Pi blinking every two seconds.</span></span>  <span data-ttu-id="f32a0-159">In caso contrario, vedere la [guida alla risoluzione dei problemi](iot-hub-raspberry-pi-kit-node-troubleshooting.md) per le soluzioni alle problematiche comuni.</span><span class="sxs-lookup"><span data-stu-id="f32a0-159">If you don’t see the LED blinking, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions to common problems.</span></span>
<span data-ttu-id="f32a0-160">![LED lampeggiante](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="f32a0-160">![LED blinking](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="f32a0-161">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="f32a0-161">Summary</span></span>
<span data-ttu-id="f32a0-162">Sono stati installati gli strumenti necessari per usare Pi ed è stata distribuita un'applicazione di esempio che consente al dispositivo Pi di far lampeggiare il LED.</span><span class="sxs-lookup"><span data-stu-id="f32a0-162">You've installed the required tools to work with Pi and deployed a sample application to Pi to blink the LED.</span></span> <span data-ttu-id="f32a0-163">È ora possibile creare, distribuire ed eseguire un'altra applicazione di esempio che connette Pi all'hub IoT di Azure per inviare e ricevere messaggi.</span><span class="sxs-lookup"><span data-stu-id="f32a0-163">You can now create, deploy, and run another sample application that connects Pi to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f32a0-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f32a0-164">Next steps</span></span>
[<span data-ttu-id="f32a0-165">Ottenere gli strumenti di Azure</span><span class="sxs-lookup"><span data-stu-id="f32a0-165">Get the Azure tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)

