---
title: 'Connect Raspberry PI (C) tooAzure IoT - lezione 1: distribuire app | Documenti Microsoft'
description: Clonazione di un'applicazione hello esempio C da GitHub e gulp toodeploy questa scheda tooyour Raspberry Pi 3 dell'applicazione. Questa applicazione di esempio lampeggia hello LED connesso toohello Lavagna ogni due secondi.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: lampeggiamento led raspberry pi, far lampeggiare il led con raspberry pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f601d1e1-2bc3-4cc5-a6b1-0467e5304dcf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: e90c3360c4de1873313db19561c781eb21dbf1d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="66746-105">Creare e distribuire un'applicazione hello blink</span><span class="sxs-lookup"><span data-stu-id="66746-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="66746-106">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="66746-106">What you will do</span></span>
<span data-ttu-id="66746-107">Clonazione di un'applicazione hello esempio C da GitHub e utilizzare hello gulp strumento toodeploy hello esempio applicazione tooRaspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="66746-107">Clone hello sample C application from GitHub, and use hello gulp tool toodeploy hello sample application tooRaspberry Pi 3.</span></span> <span data-ttu-id="66746-108">applicazione di esempio Hello lampeggia hello LED connesso toohello Lavagna ogni due secondi.</span><span class="sxs-lookup"><span data-stu-id="66746-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="66746-109">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="66746-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="66746-110">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="66746-110">What you will learn</span></span>
<span data-ttu-id="66746-111">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="66746-111">In this article, you will learn:</span></span>

* <span data-ttu-id="66746-112">Come hello toouse `device-discover-cli` tooretrieve strumento rete informazioni Pi.</span><span class="sxs-lookup"><span data-stu-id="66746-112">How toouse hello `device-discover-cli` tool tooretrieve networking information about Pi.</span></span>
* <span data-ttu-id="66746-113">Toodeploy e hello esecuzione esempio come applicazione in Installazione guidata piattaforma.</span><span class="sxs-lookup"><span data-stu-id="66746-113">How toodeploy and run hello sample application on Pi.</span></span>
* <span data-ttu-id="66746-114">Come toodeploy ed eseguire il debug di applicazioni in esecuzione in modalità remota in Pi.</span><span class="sxs-lookup"><span data-stu-id="66746-114">How toodeploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="66746-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="66746-115">What you need</span></span>
<span data-ttu-id="66746-116">È necessario che sia completata hello seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="66746-116">You must have successfully completed hello following operations:</span></span>

* [<span data-ttu-id="66746-117">Configurare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="66746-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md)
* [<span data-ttu-id="66746-118">Ottenere strumenti hello</span><span class="sxs-lookup"><span data-stu-id="66746-118">Get hello tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

## <a name="obtain-hello-ip-address-and-host-name-of-pi"></a><span data-ttu-id="66746-119">Ottenere hello IP indirizzo e il nome host di pi greco</span><span class="sxs-lookup"><span data-stu-id="66746-119">Obtain hello IP address and host name of Pi</span></span>
<span data-ttu-id="66746-120">Aprire un prompt dei comandi in Windows o un terminale macOS o Ubuntu e quindi eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="66746-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run hello following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="66746-121">Verrà visualizzato un output simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="66746-121">You should see an output that is similar toohello following:</span></span>

![Individuazione del dispositivo](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="66746-123">Prendere nota di hello `IP address` e `hostname` di pi greco.</span><span class="sxs-lookup"><span data-stu-id="66746-123">Take note of hello `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="66746-124">Queste informazioni saranno necessarie più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="66746-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="66746-125">Assicurarsi che l'installazione guidata piattaforma sia connesso toohello stessa rete del computer.</span><span class="sxs-lookup"><span data-stu-id="66746-125">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="66746-126">Ad esempio, se il computer è connesso tooa rete wireless mentre Pi è connesso tooa rete cablata, si potrebbe visualizzare non hello IP indirizzo nell'output di hello devdisco.</span><span class="sxs-lookup"><span data-stu-id="66746-126">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="66746-127">Applicazione di esempio hello aperto</span><span class="sxs-lookup"><span data-stu-id="66746-127">Open hello sample application</span></span>
<span data-ttu-id="66746-128">hello tooopen applicazione di esempio, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="66746-128">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="66746-129">Clonare il repository di esempio hello da GitHub eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="66746-129">Clone hello sample repository from GitHub by running hello following command:</span></span>
   
    ```bash
    git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started.git
    ```
2. <span data-ttu-id="66746-130">Aprire l'applicazione di esempio hello in Visual Studio Code eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="66746-130">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>
   
    ```bash
    cd iot-hub-c-raspberrypi-getting-started
    cd Lesson1
    code .
    ```

![Struttura del repository](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-c-mac.png)

<span data-ttu-id="66746-132">Hello `main.c` file hello `app` sottocartella è hello i file di origine della chiave che contiene hello codice toocontrol hello LED.</span><span class="sxs-lookup"><span data-stu-id="66746-132">hello `main.c` file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="66746-133">Installare le dipendenze dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="66746-133">Install application dependencies</span></span>
<span data-ttu-id="66746-134">Installare le librerie di hello e altri moduli, che è necessario per l'applicazione di esempio hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="66746-134">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="66746-135">Configurare una connessione al dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="66746-135">Configure hello device connection</span></span>
<span data-ttu-id="66746-136">tooconfigure hello connessione al dispositivo, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="66746-136">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="66746-137">Generare file di configurazione dispositivo hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="66746-137">Generate hello device configuration file by running hello following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="66746-138">file di configurazione Hello `config-raspberrypi.json` contiene credenziali utente hello è utilizzare toolog tooPi.</span><span class="sxs-lookup"><span data-stu-id="66746-138">hello configuration file `config-raspberrypi.json` contains hello user credentials you use toolog in tooPi.</span></span> <span data-ttu-id="66746-139">perdita di hello tooavoid delle credenziali dell'utente, viene generato il file di configurazione di hello nella sottocartella hello `.iot-hub-getting-started` della cartella principale di hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="66746-139">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="66746-140">Aprire il file di configurazione dispositivo hello in Visual Studio Code eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="66746-140">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```

3. <span data-ttu-id="66746-141">Sostituire il segnaposto hello `[device hostname or IP address]` con indirizzo IP hello o il nome host hello che è stato ottenuto in precedenza in "Ottenere hello IP indirizzo e nome host di pi greco."</span><span class="sxs-lookup"><span data-stu-id="66746-141">Replace hello placeholder `[device hostname or IP address]` with hello IP address or hello host name that you got previously in "Obtain hello IP address and host name of Pi."</span></span>
   
   ![Config.json](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="66746-143">È possibile utilizzare la chiave SSH anziché nome utente e password quando ci si connette tooRaspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="66746-143">You can use SSH key instead of user name and password when connecting tooRaspberry Pi.</span></span> <span data-ttu-id="66746-144">In ordine toodo questo sarà necessario toogenerate hello chiave usando **ssh-keygen** e **pi ssh-copy-id @\<indirizzo dispositivo\>**.</span><span class="sxs-lookup"><span data-stu-id="66746-144">In order toodo this you will have toogenerate hello key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="66746-145">In Windows, questi comandi sono disponibili in **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="66746-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="66746-146">MacOS è necessario toorun **brew installare ssh-copy-id**.</span><span class="sxs-lookup"><span data-stu-id="66746-146">On MacOS you need toorun **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="66746-147">Dopo aver caricato correttamente hello chiave toohello Raspberry Pi, sostituire **device_password** con **device_key_path** proprietà **config raspberrypi.json**.</span><span class="sxs-lookup"><span data-stu-id="66746-147">After successfully uploading hello key toohello Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="66746-148">Le righe aggiornate saranno simili alle seguenti:</span><span class="sxs-lookup"><span data-stu-id="66746-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="66746-149">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="66746-149">Congratulations!</span></span> <span data-ttu-id="66746-150">È stato creato correttamente l'applicazione di esempio prima di hello per Pi.</span><span class="sxs-lookup"><span data-stu-id="66746-150">You've successfully created hello first sample application for Pi.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="66746-151">Distribuire ed eseguire l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="66746-151">Deploy and run hello sample application</span></span>
### <a name="install-hello-azure-iot-hub-sdk-on-pi"></a><span data-ttu-id="66746-152">Installare hello Azure IoT Hub SDK in Pi</span><span class="sxs-lookup"><span data-stu-id="66746-152">Install hello Azure IoT Hub SDK on Pi</span></span>
<span data-ttu-id="66746-153">Installare hello Azure IoT Hub SDK in Pi eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="66746-153">Install hello Azure IoT Hub SDK on Pi by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="66746-154">Questa operazione potrebbe richiedere qualche hello toocomplete di minuti alla prima esecuzione.</span><span class="sxs-lookup"><span data-stu-id="66746-154">This task might take a few minutes toocomplete hello first time you run it.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="66746-155">Distribuire ed eseguire app di esempio hello</span><span class="sxs-lookup"><span data-stu-id="66746-155">Deploy and run hello sample app</span></span>
<span data-ttu-id="66746-156">Distribuire ed eseguire l'applicazione di esempio hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="66746-156">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="66746-157">Verificare il funzionamento dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="66746-157">Verify hello app works</span></span>
<span data-ttu-id="66746-158">applicazione di esempio Hello termina automaticamente dopo hello LED lampeggia per 20 volte.</span><span class="sxs-lookup"><span data-stu-id="66746-158">hello sample application terminates automatically after hello LED blinks for 20 times.</span></span> <span data-ttu-id="66746-159">Se non viene visualizzato hello LED è lampeggiante, vedere hello [risoluzione dei problemi guida](iot-hub-raspberry-pi-kit-c-troubleshooting.md) per soluzioni ai problemi di toocommon.</span><span class="sxs-lookup"><span data-stu-id="66746-159">If you don’t see hello LED blinking, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>
<span data-ttu-id="66746-160">![LED lampeggiante](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="66746-160">![LED blinking](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="66746-161">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="66746-161">Summary</span></span>
<span data-ttu-id="66746-162">È stato installato hello necessario strumenti toowork con Pi e distribuito un hello tooblink di tooPi dall'applicazione di esempio LED.</span><span class="sxs-lookup"><span data-stu-id="66746-162">You've installed hello required tools toowork with Pi and deployed a sample application tooPi tooblink hello LED.</span></span> <span data-ttu-id="66746-163">È ora possibile creare, distribuire e l'esecuzione di un'altra applicazione di esempio che si connette Pi tooAzure toosend IoT Hub e ricevere messaggi.</span><span class="sxs-lookup"><span data-stu-id="66746-163">You can now create, deploy, and run another sample application that connects Pi tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66746-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="66746-164">Next steps</span></span>
[<span data-ttu-id="66746-165">Ottenere gli strumenti di Azure</span><span class="sxs-lookup"><span data-stu-id="66746-165">Get Azure tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)

