---
title: 'Dispositivo simulato e gateway Azure IoT: lezione 1: Configurare NUC | Documentazione Microsoft'
description: Impostare toowork Intel NUC come gateway tra un sensore e informazioni di sensore toocollect Azure IoT Hub IoT e inviarla tooIoT Hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: yjianfeng
tags: 
keywords: gateway iot, intel nuc, computer nuc, DE3815TYKE
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f41d6b2e-9b00-40df-90eb-17d824bea883
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c2146c7cd8ca54adbd0af279364ec8484be1b45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="1e384-104">Configurare Intel NUC come gateway IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="1e384-104">Set up Intel NUC as an IoT gateway</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="1e384-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="1e384-105">What you will do</span></span>

- <span data-ttu-id="1e384-106">Configurare Intel NUC come gateway IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="1e384-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="1e384-107">Installare il pacchetto di Azure IoT Edge hello in NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="1e384-107">Install hello Azure IoT Edge package on Intel NUC.</span></span>
- <span data-ttu-id="1e384-108">Eseguire un'applicazione di esempio "hello_world" funzionalità di gateway di Intel NUC tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="1e384-108">Run a "hello_world" sample application on Intel NUC tooverify hello gateway functionality.</span></span>
<span data-ttu-id="1e384-109">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="1e384-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="1e384-110">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="1e384-110">What you will learn</span></span>

<span data-ttu-id="1e384-111">In questa lezione si apprenderà:</span><span class="sxs-lookup"><span data-stu-id="1e384-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="1e384-112">Come tooconnect Intel NUC con le periferiche.</span><span class="sxs-lookup"><span data-stu-id="1e384-112">How tooconnect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="1e384-113">Come tooinstall e aggiornare i pacchetti hello necessarie sull'uso di Intel NUC hello Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="1e384-113">How tooinstall and update hello required packages on Intel NUC using hello Smart Package Manager.</span></span>
- <span data-ttu-id="1e384-114">Modalità di esempio funzionalità di gateway applicazione tooverify hello hello_world"toorun hello".</span><span class="sxs-lookup"><span data-stu-id="1e384-114">How toorun hello "hello_world" sample application tooverify hello gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1e384-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="1e384-115">What you need</span></span>

- <span data-ttu-id="1e384-116">Un Intel NUC Kit DE3815TYKE con hello Suite Software Gateway IoT di Intel (vento distretto Linux * 7.0.0.13) preinstallato.</span><span class="sxs-lookup"><span data-stu-id="1e384-116">An Intel NUC Kit DE3815TYKE with hello Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span>
- <span data-ttu-id="1e384-117">Un cavo Ethernet.</span><span class="sxs-lookup"><span data-stu-id="1e384-117">An Ethernet cable.</span></span>
- <span data-ttu-id="1e384-118">Una tastiera.</span><span class="sxs-lookup"><span data-stu-id="1e384-118">A keyboard.</span></span>
- <span data-ttu-id="1e384-119">Un cavo HDMI o VGA.</span><span class="sxs-lookup"><span data-stu-id="1e384-119">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="1e384-120">Un monitor con porta HDMI o VGA.</span><span class="sxs-lookup"><span data-stu-id="1e384-120">A monitor with an HDMI or VGA port.</span></span>

![Kit gateway](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a><span data-ttu-id="1e384-122">La connessione di Intel NUC con le periferiche hello</span><span class="sxs-lookup"><span data-stu-id="1e384-122">Connect Intel NUC with hello peripherals</span></span>

<span data-ttu-id="1e384-123">immagine di Hello riportata di seguito è riportato un esempio di Intel NUC connesso con le periferiche diverse:</span><span class="sxs-lookup"><span data-stu-id="1e384-123">hello image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="1e384-124">Tastiera tooa connesso.</span><span class="sxs-lookup"><span data-stu-id="1e384-124">Connected tooa keyboard.</span></span>
2. <span data-ttu-id="1e384-125">Connesso toohello monitoraggio da un cavo o un cavo HDMI.</span><span class="sxs-lookup"><span data-stu-id="1e384-125">Connected toohello monitor by a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="1e384-126">Connesso tooa rete cablata tramite un cavo Ethernet.</span><span class="sxs-lookup"><span data-stu-id="1e384-126">Connected tooa wired network by an Ethernet cable.</span></span>
4. <span data-ttu-id="1e384-127">Alimentatore toohello connessi con un cavo di alimentazione.</span><span class="sxs-lookup"><span data-stu-id="1e384-127">Connected toohello power supply with a power cable.</span></span>

![Tooperipherals NUC Intel connesso](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="1e384-129">Connettere il sistema di Intel NUC toohello dal computer host tramite Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="1e384-129">Connect toohello Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="1e384-130">In questo caso, è necessario tastiera monitor tooget hello indirizzo IP e del dispositivo NUC.</span><span class="sxs-lookup"><span data-stu-id="1e384-130">Here you need keyboard and monitor tooget hello IP address of your NUC device.</span></span> <span data-ttu-id="1e384-131">Se si conosce già hello IP indirizzo, è possibile ignorare toostep 3 di questa sezione.</span><span class="sxs-lookup"><span data-stu-id="1e384-131">If you already know hello IP address, you can skip toostep 3 in this section.</span></span>

1. <span data-ttu-id="1e384-132">Attivare Intel NUC premendo il pulsante di alimentazione hello e di log nel sistema hello.</span><span class="sxs-lookup"><span data-stu-id="1e384-132">Turn on Intel NUC by pressing hello Power button and log in hello system.</span></span>

   <span data-ttu-id="1e384-133">nome Hello predefinito dell'utente e password sono entrambi `root`.</span><span class="sxs-lookup"><span data-stu-id="1e384-133">hello default user name and password are both `root`.</span></span>

2. <span data-ttu-id="1e384-134">Ottenere l'indirizzo IP hello del NUC eseguendo hello `ifconfig` comando.</span><span class="sxs-lookup"><span data-stu-id="1e384-134">Get hello IP address of NUC by running hello `ifconfig` command.</span></span> <span data-ttu-id="1e384-135">Questo passaggio viene eseguito sul dispositivo NUC hello.</span><span class="sxs-lookup"><span data-stu-id="1e384-135">This step is done on hello NUC device.</span></span>

   <span data-ttu-id="1e384-136">Di seguito è riportato un esempio di output del comando hello.</span><span class="sxs-lookup"><span data-stu-id="1e384-136">Here is an example of hello command output.</span></span>

   ![Output di ifconfig che indica l'IP NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="1e384-138">In questo esempio hello che segue `inet addr:` è l'indirizzo IP hello che è necessario quando si pianifica tooconnect in modalità remota da un tooIntel computer host NUC.</span><span class="sxs-lookup"><span data-stu-id="1e384-138">In this example, hello value that follows `inet addr:` is hello IP address that you need when you plan tooconnect remotely from a host computer tooIntel NUC.</span></span>

3. <span data-ttu-id="1e384-139">Utilizzare uno dei seguenti client SSH dagli tooIntel di tooconnect computer host NUC hello.</span><span class="sxs-lookup"><span data-stu-id="1e384-139">Use one of hello following SSH clients from your host machine tooconnect tooIntel NUC.</span></span>

   - <span data-ttu-id="1e384-140">[PuTTY](http://www.putty.org/) per Windows.</span><span class="sxs-lookup"><span data-stu-id="1e384-140">[PuTTY](http://www.putty.org/) for Windows.</span></span>
   - <span data-ttu-id="1e384-141">Hello compilazione SSH client Ubuntu o macOS.</span><span class="sxs-lookup"><span data-stu-id="1e384-141">hello build-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="1e384-142">È più efficiente e produttivo toooperate su Intel NUC da un computer host.</span><span class="sxs-lookup"><span data-stu-id="1e384-142">It is more efficient and productive toooperate on Intel NUC from a host computer.</span></span> <span data-ttu-id="1e384-143">È necessario l'indirizzo IP hello hello, nome utente e password tooconnect hello NUC tramite client SSH.</span><span class="sxs-lookup"><span data-stu-id="1e384-143">You need hello hello IP address, user name and password tooconnect hello NUC via SSH client.</span></span> <span data-ttu-id="1e384-144">Ecco client SSH utilizzo di esempio hello in macOS.</span><span class="sxs-lookup"><span data-stu-id="1e384-144">Here is hello example use SSH client on macOS.</span></span>
   <span data-ttu-id="1e384-145">![Client SSH eseguito su macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="1e384-145">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-hello-azure-iot-edge-package"></a><span data-ttu-id="1e384-146">Installare il pacchetto di hello Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="1e384-146">Install hello Azure IoT Edge package</span></span>

<span data-ttu-id="1e384-147">pacchetto di Azure IoT Edge Hello contiene i file binari precompilati hello di hello SDK e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="1e384-147">hello Azure IoT Edge package contains hello pre-compiled binaries of hello SDK and its dependencies.</span></span> <span data-ttu-id="1e384-148">Questi binari sono Azure IoT Edge, hello Azure IoT SDK e strumenti corrispondenti hello.</span><span class="sxs-lookup"><span data-stu-id="1e384-148">These binaries are Azure IoT Edge, hello Azure IoT SDK and hello corresponding tools.</span></span> <span data-ttu-id="1e384-149">pacchetto di Hello contiene anche un'applicazione di esempio "hello_world" che è una funzionalità di gateway hello toovalidate utilizzato.</span><span class="sxs-lookup"><span data-stu-id="1e384-149">hello package also contains a "hello_world" sample application that is used toovalidate hello gateway functionality.</span></span> <span data-ttu-id="1e384-150">Bordo di IoT è fondamentale hello del gateway hello.</span><span class="sxs-lookup"><span data-stu-id="1e384-150">IoT Edge is hello core part of hello gateway.</span></span> <span data-ttu-id="1e384-151">tooinstall hello del pacchetto, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="1e384-151">tooinstall hello package, follow these steps:</span></span>

1. <span data-ttu-id="1e384-152">Aggiungi repository di cloud di hello IoT eseguendo i seguenti comandi in una finestra terminale hello:</span><span class="sxs-lookup"><span data-stu-id="1e384-152">Add hello IoT cloud repository by running hello following commands in a terminal window:</span></span>

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   <span data-ttu-id="1e384-153">Hello `rpm` comando importazioni hello chiave rpm.</span><span class="sxs-lookup"><span data-stu-id="1e384-153">hello `rpm` command imports hello rpm key.</span></span> <span data-ttu-id="1e384-154">Hello `smart channel` comando aggiunge rpm hello canale toohello Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="1e384-154">hello `smart channel` command adds hello rpm channel toohello Smart Package Manager.</span></span> <span data-ttu-id="1e384-155">Prima di eseguire hello `smart update` comando, viene visualizzato un output simile di sotto.</span><span class="sxs-lookup"><span data-stu-id="1e384-155">Before you run hello `smart update` command, you see an output like below.</span></span>

   ![output dei comandi di canale rpm e smart](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. <span data-ttu-id="1e384-157">Installare il pacchetto di hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1e384-157">Install hello package by running hello following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="1e384-158">`packagegroup-cloud-azure`è il nome di hello del pacchetto di hello.</span><span class="sxs-lookup"><span data-stu-id="1e384-158">`packagegroup-cloud-azure` is hello name of hello package.</span></span> <span data-ttu-id="1e384-159">Hello `smart install` comando è il pacchetto di hello tooinstall utilizzato.</span><span class="sxs-lookup"><span data-stu-id="1e384-159">hello `smart install` command is used tooinstall hello package.</span></span>

   <span data-ttu-id="1e384-160">Dopo aver installato il pacchetto di hello, Intel NUC è toowork previsto come gateway.</span><span class="sxs-lookup"><span data-stu-id="1e384-160">After hello package is installed, Intel NUC is expected toowork as a gateway.</span></span>

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="1e384-161">Eseguire l'applicazione di esempio "hello_world" hello Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="1e384-161">Run hello Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="1e384-162">Andare troppo`azureiotgatewaysdk/samples` ed eseguire l'applicazione di esempio "hello_world" esempio hello.</span><span class="sxs-lookup"><span data-stu-id="1e384-162">Go too`azureiotgatewaysdk/samples` and run hello sample "hello_world" sample application.</span></span> <span data-ttu-id="1e384-163">Questa applicazione di esempio crea un gateway da hello `hello_world.json` file e utilizza i componenti fondamentali di hello di hello Azure IoT Edge architettura toolog un file di hello world messaggio tooa ogni 5 secondi.</span><span class="sxs-lookup"><span data-stu-id="1e384-163">This sample application creates a gateway from hello `hello_world.json` file and uses hello fundamental components of hello Azure IoT Edge architecture toolog a hello world message tooa file every 5 seconds.</span></span>

<span data-ttu-id="1e384-164">È possibile eseguire l'applicazione di esempio "hello_world" esempio hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1e384-164">You can run hello sample "hello_world" sample application by running hello following command:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="1e384-165">applicazione di esempio Hello produce output se la funzionalità di gateway hello funziona correttamente seguente di hello:</span><span class="sxs-lookup"><span data-stu-id="1e384-165">hello sample application produces hello following output if hello gateway functionality is working correctly:</span></span>

![output dell'applicazione](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

<span data-ttu-id="1e384-167">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="1e384-167">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="1e384-168">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="1e384-168">Summary</span></span>

<span data-ttu-id="1e384-169">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="1e384-169">Congratulations!</span></span> <span data-ttu-id="1e384-170">La configurazione di Intel NUC come gateway è completata.</span><span class="sxs-lookup"><span data-stu-id="1e384-170">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="1e384-171">Si è pronti toomove su toohello tooset lezione al successivo backup del computer host, creare un hub IoT di Azure e registrare il dispositivo logico di hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="1e384-171">Now you're ready toomove on toohello next lesson tooset up your host computer, create an Azure IoT hub and register your Azure IoT hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e384-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1e384-172">Next steps</span></span>
[<span data-ttu-id="1e384-173">Preparare il computer host e l'hub IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="1e384-173">Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
