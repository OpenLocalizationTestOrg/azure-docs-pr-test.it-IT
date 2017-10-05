---
title: 'Dispositivo simulato e gateway Azure IoT: lezione 1: Configurare NUC | Documentazione Microsoft'
description: Impostare Intel NUC come un gateway IoT di Azure tra un sensore e l'hub IoT di Azure, per raccogliere informazioni sul sensore e inviarle a IoT Hub.
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
ms.openlocfilehash: b87974be9570f7d03fe84ae0a1d1fa7e346ff189
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="af358-104">Configurare Intel NUC come gateway IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="af358-104">Set up Intel NUC as an IoT gateway</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="af358-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="af358-105">What you will do</span></span>

- <span data-ttu-id="af358-106">Configurare Intel NUC come gateway IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="af358-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="af358-107">Installare il pacchetto Azure IoT Edge in Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="af358-107">Install the Azure IoT Edge package on Intel NUC.</span></span>
- <span data-ttu-id="af358-108">Eseguire un'applicazione di esempio "hello_world" in Intel NUC per verificare la funzionalità del gateway.</span><span class="sxs-lookup"><span data-stu-id="af358-108">Run a "hello_world" sample application on Intel NUC to verify the gateway functionality.</span></span>
<span data-ttu-id="af358-109">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="af358-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="af358-110">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="af358-110">What you will learn</span></span>

<span data-ttu-id="af358-111">In questa lezione si apprenderà:</span><span class="sxs-lookup"><span data-stu-id="af358-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="af358-112">Come collegare Intel NUC alle periferiche.</span><span class="sxs-lookup"><span data-stu-id="af358-112">How to connect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="af358-113">Come installare e aggiornare i pacchetti richiesti su Intel NUC tramite Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="af358-113">How to install and update the required packages on Intel NUC using the Smart Package Manager.</span></span>
- <span data-ttu-id="af358-114">Come eseguire l'applicazione di esempio "hello_world" per verificare la funzionalità del gateway.</span><span class="sxs-lookup"><span data-stu-id="af358-114">How to run the "hello_world" sample application to verify the gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="af358-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="af358-115">What you need</span></span>

- <span data-ttu-id="af358-116">Intel NUC Kit DE3815TYKE con Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstallata.</span><span class="sxs-lookup"><span data-stu-id="af358-116">An Intel NUC Kit DE3815TYKE with the Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span>
- <span data-ttu-id="af358-117">Un cavo Ethernet.</span><span class="sxs-lookup"><span data-stu-id="af358-117">An Ethernet cable.</span></span>
- <span data-ttu-id="af358-118">Una tastiera.</span><span class="sxs-lookup"><span data-stu-id="af358-118">A keyboard.</span></span>
- <span data-ttu-id="af358-119">Un cavo HDMI o VGA.</span><span class="sxs-lookup"><span data-stu-id="af358-119">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="af358-120">Un monitor con porta HDMI o VGA.</span><span class="sxs-lookup"><span data-stu-id="af358-120">A monitor with an HDMI or VGA port.</span></span>

![Kit gateway](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-the-peripherals"></a><span data-ttu-id="af358-122">Come connettere Intel NUC con le periferiche</span><span class="sxs-lookup"><span data-stu-id="af358-122">Connect Intel NUC with the peripherals</span></span>

<span data-ttu-id="af358-123">Nell'immagine seguente è riportato un esempio di dispositivo Intel NUC collegato a diverse periferiche:</span><span class="sxs-lookup"><span data-stu-id="af358-123">The image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="af358-124">A una tastiera.</span><span class="sxs-lookup"><span data-stu-id="af358-124">Connected to a keyboard.</span></span>
2. <span data-ttu-id="af358-125">A un monitor tramite un cavo VGA o HDMI.</span><span class="sxs-lookup"><span data-stu-id="af358-125">Connected to the monitor by a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="af358-126">A una rete cablata tramite cavo Ethernet.</span><span class="sxs-lookup"><span data-stu-id="af358-126">Connected to a wired network by an Ethernet cable.</span></span>
4. <span data-ttu-id="af358-127">All'alimentatore tramite un cavo di alimentazione.</span><span class="sxs-lookup"><span data-stu-id="af358-127">Connected to the power supply with a power cable.</span></span>

![Dispositivo Intel NUC collegato a periferiche](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-to-the-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="af358-129">Connettere il sistema Intel NUC dal computer host tramite Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="af358-129">Connect to the Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="af358-130">In questo caso sono necessari una tastiera e un monitor per ottenere l'indirizzo IP del dispositivo NUC.</span><span class="sxs-lookup"><span data-stu-id="af358-130">Here you need keyboard and monitor to get the IP address of your NUC device.</span></span> <span data-ttu-id="af358-131">Se si conosce già l'indirizzo IP, è possibile andare al passaggio 3 di questa sezione.</span><span class="sxs-lookup"><span data-stu-id="af358-131">If you already know the IP address, you can skip to step 3 in this section.</span></span>

1. <span data-ttu-id="af358-132">Accendere il dispositivo Intel NUC premendo l'apposito tasto e accedere al sistema.</span><span class="sxs-lookup"><span data-stu-id="af358-132">Turn on Intel NUC by pressing the Power button and log in the system.</span></span>

   <span data-ttu-id="af358-133">Il nome utente e la password predefiniti sono entrambi `root`.</span><span class="sxs-lookup"><span data-stu-id="af358-133">The default user name and password are both `root`.</span></span>

2. <span data-ttu-id="af358-134">Ottenere l'indirizzo IP del dispositivo NUC eseguendo il comando `ifconfig`.</span><span class="sxs-lookup"><span data-stu-id="af358-134">Get the IP address of NUC by running the `ifconfig` command.</span></span> <span data-ttu-id="af358-135">Questo passaggio viene eseguito sul dispositivo NUC.</span><span class="sxs-lookup"><span data-stu-id="af358-135">This step is done on the NUC device.</span></span>

   <span data-ttu-id="af358-136">Di seguito è riportato un esempio dell'output del comando.</span><span class="sxs-lookup"><span data-stu-id="af358-136">Here is an example of the command output.</span></span>

   ![Output di ifconfig che indica l'IP NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="af358-138">In questo esempio, il valore che segue `inet addr:` è l'indirizzo IP necessario se si prevede di connettersi in remoto da un computer host a Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="af358-138">In this example, the value that follows `inet addr:` is the IP address that you need when you plan to connect remotely from a host computer to Intel NUC.</span></span>

3. <span data-ttu-id="af358-139">Per connettersi a Intel NUC, usare uno dei client SSH seguenti dal computer host.</span><span class="sxs-lookup"><span data-stu-id="af358-139">Use one of the following SSH clients from your host machine to connect to Intel NUC.</span></span>

   - <span data-ttu-id="af358-140">[PuTTY](http://www.putty.org/) per Windows.</span><span class="sxs-lookup"><span data-stu-id="af358-140">[PuTTY](http://www.putty.org/) for Windows.</span></span>
   - <span data-ttu-id="af358-141">Il client SSH incorporato in Ubuntu o macOS.</span><span class="sxs-lookup"><span data-stu-id="af358-141">The build-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="af358-142">È più efficiente e produttivo lavorare su un dispositivo Intel NUC da un computer host.</span><span class="sxs-lookup"><span data-stu-id="af358-142">It is more efficient and productive to operate on Intel NUC from a host computer.</span></span> <span data-ttu-id="af358-143">Per connettersi al dispositivo NUC tramite il client SSH, sono necessari indirizzo IP, nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="af358-143">You need the the IP address, user name and password to connect the NUC via SSH client.</span></span> <span data-ttu-id="af358-144">Di seguito è riportato un esempio di utilizzo del client SSH su macOS.</span><span class="sxs-lookup"><span data-stu-id="af358-144">Here is the example use SSH client on macOS.</span></span>
   <span data-ttu-id="af358-145">![Client SSH eseguito su macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="af358-145">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-the-azure-iot-edge-package"></a><span data-ttu-id="af358-146">Installare il pacchetto Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="af358-146">Install the Azure IoT Edge package</span></span>

<span data-ttu-id="af358-147">Il pacchetto Azure IoT Edge contiene i file binari precompilati dell'SDK e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="af358-147">The Azure IoT Edge package contains the pre-compiled binaries of the SDK and its dependencies.</span></span> <span data-ttu-id="af358-148">I file binari sono costituiti da Azure IoT Edge, Azure IoT SDK e gli strumenti corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="af358-148">These binaries are Azure IoT Edge, the Azure IoT SDK and the corresponding tools.</span></span> <span data-ttu-id="af358-149">Il pacchetto contiene anche un'applicazione di esempio "hello_world" usata per convalidare la funzionalità del gateway.</span><span class="sxs-lookup"><span data-stu-id="af358-149">The package also contains a "hello_world" sample application that is used to validate the gateway functionality.</span></span> <span data-ttu-id="af358-150">IoT Edge è la parte principale del gateway.</span><span class="sxs-lookup"><span data-stu-id="af358-150">IoT Edge is the core part of the gateway.</span></span> <span data-ttu-id="af358-151">Per installare il pacchetto, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="af358-151">To install the package, follow these steps:</span></span>

1. <span data-ttu-id="af358-152">Aggiungere il repository cloud IoT eseguendo questi comandi nella finestra del terminale:</span><span class="sxs-lookup"><span data-stu-id="af358-152">Add the IoT cloud repository by running the following commands in a terminal window:</span></span>

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   <span data-ttu-id="af358-153">Il comando `rpm` consente di importare la chiave rpm.</span><span class="sxs-lookup"><span data-stu-id="af358-153">The `rpm` command imports the rpm key.</span></span> <span data-ttu-id="af358-154">Il comando `smart channel` consente di aggiungere il canale rpm a Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="af358-154">The `smart channel` command adds the rpm channel to the Smart Package Manager.</span></span> <span data-ttu-id="af358-155">Prima dell'esecuzione del comando `smart update`, viene visualizzato un output come quello seguente.</span><span class="sxs-lookup"><span data-stu-id="af358-155">Before you run the `smart update` command, you see an output like below.</span></span>

   ![output dei comandi di canale rpm e smart](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. <span data-ttu-id="af358-157">Installare il pacchetto eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="af358-157">Install the package by running the following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="af358-158">`packagegroup-cloud-azure` è il nome del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="af358-158">`packagegroup-cloud-azure` is the name of the package.</span></span> <span data-ttu-id="af358-159">Il comando `smart install` consente di installare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="af358-159">The `smart install` command is used to install the package.</span></span>

   <span data-ttu-id="af358-160">Dopo l'installazione del pacchetto, Intel NUC dovrebbe funzionare come gateway.</span><span class="sxs-lookup"><span data-stu-id="af358-160">After the package is installed, Intel NUC is expected to work as a gateway.</span></span>

## <a name="run-the-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="af358-161">Eseguire l'applicazione di esempio "hello_world" di Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="af358-161">Run the Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="af358-162">Passare a `azureiotgatewaysdk/samples` ed eseguire l'applicazione di esempio "hello_world"</span><span class="sxs-lookup"><span data-stu-id="af358-162">Go to `azureiotgatewaysdk/samples` and run the sample "hello_world" sample application.</span></span> <span data-ttu-id="af358-163">che crea un gateway dal file `hello_world.json` e usa i componenti principali dell'architettura di Azure IoT Edge per registrare un messaggio di "hello world" in un file ogni 5 secondi.</span><span class="sxs-lookup"><span data-stu-id="af358-163">This sample application creates a gateway from the `hello_world.json` file and uses the fundamental components of the Azure IoT Edge architecture to log a hello world message to a file every 5 seconds.</span></span>

<span data-ttu-id="af358-164">È possibile eseguire l'applicazione di esempio "hello_world" con questo comando:</span><span class="sxs-lookup"><span data-stu-id="af358-164">You can run the sample "hello_world" sample application by running the following command:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="af358-165">L'applicazione di esempio restituisce l'output seguente se la funzionalità del gateway viene eseguita correttamente:</span><span class="sxs-lookup"><span data-stu-id="af358-165">The sample application produces the following output if the gateway functionality is working correctly:</span></span>

![output dell'applicazione](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

<span data-ttu-id="af358-167">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="af358-167">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="af358-168">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="af358-168">Summary</span></span>

<span data-ttu-id="af358-169">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="af358-169">Congratulations!</span></span> <span data-ttu-id="af358-170">La configurazione di Intel NUC come gateway è completata.</span><span class="sxs-lookup"><span data-stu-id="af358-170">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="af358-171">È ora possibile passare alla lezione successiva per configurare il computer host, creare un hub IoT di Azure e registrare il dispositivo logico dell'hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="af358-171">Now you're ready to move on to the next lesson to set up your host computer, create an Azure IoT hub and register your Azure IoT hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af358-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="af358-172">Next steps</span></span>
[<span data-ttu-id="af358-173">Preparare il computer host e l'hub IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="af358-173">Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
