---
title: 'Dispositivo SensorTag e gateway Azure IoT: lezione 1: Configurare Intel NUC | Microsoft Docs'
description: Configurare Intel NUC come gateway IoT di Azure tra un sensore e l'hub IoT di Azure, per raccogliere informazioni sul sensore e inviarle a IoT Hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: gateway iot, intel nuc, computer nuc, DE3815TYKE
ms.assetid: 917090d6-35c2-495b-a620-ca6f9c02b317
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1a3a92ab8d08c6ed6f047208217c46022027157e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="b99f4-104">Configurare Intel NUC come gateway IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="b99f4-104">Set up Intel NUC as an IoT gateway</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a><span data-ttu-id="b99f4-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="b99f4-105">What you will do</span></span>

- <span data-ttu-id="b99f4-106">Configurare Intel NUC come gateway IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="b99f4-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="b99f4-107">Installare il pacchetto Azure IoT Edge in Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="b99f4-107">Install the Azure IoT Edge package on the Intel NUC.</span></span>
- <span data-ttu-id="b99f4-108">Eseguire un'applicazione di esempio "hello_world" in Intel NUC per verificare la funzionalità del gateway.</span><span class="sxs-lookup"><span data-stu-id="b99f4-108">Run a "hello_world" sample application on the Intel NUC to verify the gateway functionality.</span></span>

  > <span data-ttu-id="b99f4-109">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="b99f4-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b99f4-110">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="b99f4-110">What you will learn</span></span>

<span data-ttu-id="b99f4-111">In questa lezione si apprenderà:</span><span class="sxs-lookup"><span data-stu-id="b99f4-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="b99f4-112">Come collegare Intel NUC alle periferiche.</span><span class="sxs-lookup"><span data-stu-id="b99f4-112">How to connect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="b99f4-113">Come installare e aggiornare i pacchetti richiesti su Intel NUC tramite Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="b99f4-113">How to install and update the required packages on Intel NUC using the Smart Package Manager.</span></span>
- <span data-ttu-id="b99f4-114">Come eseguire l'applicazione di esempio "hello_world" per verificare la funzionalità del gateway.</span><span class="sxs-lookup"><span data-stu-id="b99f4-114">How to run the "hello_world" sample application to verify the gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b99f4-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="b99f4-115">What you need</span></span>

- <span data-ttu-id="b99f4-116">Intel NUC Kit DE3815TYKE con Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstallata.</span><span class="sxs-lookup"><span data-stu-id="b99f4-116">An Intel NUC Kit DE3815TYKE with the Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span> <span data-ttu-id="b99f4-117">[Fare clic qui per acquistare il Kit gateway commerciale Grove IoT](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span><span class="sxs-lookup"><span data-stu-id="b99f4-117">[Click here to purchase Grove IoT Commercial Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span></span>
- <span data-ttu-id="b99f4-118">Un cavo Ethernet.</span><span class="sxs-lookup"><span data-stu-id="b99f4-118">An Ethernet cable.</span></span>
- <span data-ttu-id="b99f4-119">Una tastiera.</span><span class="sxs-lookup"><span data-stu-id="b99f4-119">A keyboard.</span></span>
- <span data-ttu-id="b99f4-120">Un cavo HDMI o VGA.</span><span class="sxs-lookup"><span data-stu-id="b99f4-120">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="b99f4-121">Un monitor con porta HDMI o VGA.</span><span class="sxs-lookup"><span data-stu-id="b99f4-121">A monitor with an HDMI or VGA port.</span></span>
- <span data-ttu-id="b99f4-122">Facoltativo: [SensorTag di Texas Instruments (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span><span class="sxs-lookup"><span data-stu-id="b99f4-122">Optional: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span></span>

![Kit gateway](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-the-peripherals"></a><span data-ttu-id="b99f4-124">Come connettere Intel NUC con le periferiche</span><span class="sxs-lookup"><span data-stu-id="b99f4-124">Connect Intel NUC with the peripherals</span></span>

<span data-ttu-id="b99f4-125">Nell'immagine seguente è riportato un esempio di dispositivo Intel NUC collegato a diverse periferiche:</span><span class="sxs-lookup"><span data-stu-id="b99f4-125">The image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="b99f4-126">A una tastiera.</span><span class="sxs-lookup"><span data-stu-id="b99f4-126">Connected to a keyboard.</span></span>
2. <span data-ttu-id="b99f4-127">A un monitor tramite un cavo VGA o HDMI.</span><span class="sxs-lookup"><span data-stu-id="b99f4-127">Connected to a monitor with a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="b99f4-128">A una rete cablata tramite cavo Ethernet.</span><span class="sxs-lookup"><span data-stu-id="b99f4-128">Connected to a wired network with an Ethernet cable.</span></span>
4. <span data-ttu-id="b99f4-129">A un alimentatore tramite un cavo di alimentazione.</span><span class="sxs-lookup"><span data-stu-id="b99f4-129">Connected to a power supply with a power cable.</span></span>

![Dispositivo Intel NUC collegato a periferiche](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-to-the-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="b99f4-131">Connettere il sistema Intel NUC dal computer host tramite Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="b99f4-131">Connect to the Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="b99f4-132">Sono necessari una tastiera e un monitor per ottenere l'indirizzo IP del dispositivo Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="b99f4-132">You will need a keyboard and a monitor to get the IP address of your Intel NUC device.</span></span> <span data-ttu-id="b99f4-133">Se si conosce già l'indirizzo IP, è possibile andare al passaggio 3 di questa sezione.</span><span class="sxs-lookup"><span data-stu-id="b99f4-133">If you already know the IP address, you can skip ahead to step 3 in this section.</span></span>

1. <span data-ttu-id="b99f4-134">Accendere il dispositivo Intel NUC premendo l'apposito tasto ed eseguire l'accesso.</span><span class="sxs-lookup"><span data-stu-id="b99f4-134">Turn on the Intel NUC by pressing the power button and then log in.</span></span>

   <span data-ttu-id="b99f4-135">Il nome utente e la password predefiniti sono entrambi `root`.</span><span class="sxs-lookup"><span data-stu-id="b99f4-135">The default user name and password are both `root`.</span></span>

       > Hit the enter key on your keyboard if you see either of the following errors when you boot: 'A TPM error (7) occurred attempting to read a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. <span data-ttu-id="b99f4-136">Ottenere l'indirizzo IP del dispositivo Intel NUC eseguendo da esso il comando `ifconfig`. </span><span class="sxs-lookup"><span data-stu-id="b99f4-136">Get the IP address of the Intel NUC by running the `ifconfig` command on the Intel NUC device.</span></span>

   <span data-ttu-id="b99f4-137">Di seguito è riportato un esempio dell'output del comando.</span><span class="sxs-lookup"><span data-stu-id="b99f4-137">Here is an example of the command output.</span></span>

   ![Output di ifconfig che indica l'IP di Intel NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="b99f4-139">In questo esempio, il valore che segue `inet addr:` è l'indirizzo IP necessario per connettersi da un computer host a Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="b99f4-139">In this example, the value that follows `inet addr:` is the IP address that you need when connect to the Intel NUC from a host computer.</span></span>

3. <span data-ttu-id="b99f4-140">Per connettersi a Intel NUC, usare uno dei client SSH seguenti dal computer host.</span><span class="sxs-lookup"><span data-stu-id="b99f4-140">Use one of the following SSH clients from your host computer to connect to Intel NUC.</span></span>

    - <span data-ttu-id="b99f4-141">[PuTTY](http://www.putty.org/) per Windows.</span><span class="sxs-lookup"><span data-stu-id="b99f4-141">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="b99f4-142">Il client SSH incorporato in Ubuntu o macOS.</span><span class="sxs-lookup"><span data-stu-id="b99f4-142">The built-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="b99f4-143">È più efficiente e produttivo lavorare su un dispositivo Intel NUC da un computer host.</span><span class="sxs-lookup"><span data-stu-id="b99f4-143">It is more efficient and productive to operate an Intel NUC from a host computer.</span></span> <span data-ttu-id="b99f4-144">Per connettersi al dispositivo Intel NUC tramite il client SSH, sono necessari indirizzo IP, nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="b99f4-144">You'll need the Intel NUC's IP address, user name and password to connect to it via an SSH client.</span></span> <span data-ttu-id="b99f4-145">Di seguito è riportato un esempio che usa un client SSH in macOS.</span><span class="sxs-lookup"><span data-stu-id="b99f4-145">Here is an example that uses an SSH client on macOS.</span></span>
   <span data-ttu-id="b99f4-146">![Client SSH eseguito su macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="b99f4-146">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-the-azure-iot-edge-package"></a><span data-ttu-id="b99f4-147">Installare il pacchetto Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="b99f4-147">Install the Azure IoT Edge package</span></span>

<span data-ttu-id="b99f4-148">Il pacchetto Azure IoT Edge contiene i file binari precompilati di IoT Edge e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="b99f4-148">The Azure IoT Edge package contains the pre-compiled binaries of IoT Edge and its dependencies.</span></span> <span data-ttu-id="b99f4-149">I file binari sono Azure IoT Edge, l'SDK Azure IoT e gli strumenti corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="b99f4-149">These binaries are Azure IoT Edge, the Azure IoT SDK and the corresponding tools.</span></span> <span data-ttu-id="b99f4-150">Il pacchetto contiene anche un'applicazione di esempio "hello_world" utilizzata per convalidare la funzionalità del gateway.</span><span class="sxs-lookup"><span data-stu-id="b99f4-150">The package also contains a "hello_world" sample application is used to validate the gateway functionality.</span></span> <span data-ttu-id="b99f4-151">IoT Edge è il componente principale del gateway.</span><span class="sxs-lookup"><span data-stu-id="b99f4-151">IoT Edge is the core part of the gateway.</span></span> 

<span data-ttu-id="b99f4-152">Per installare il pacchetto, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="b99f4-152">Follow these steps to install the package.</span></span>

1. <span data-ttu-id="b99f4-153">Aggiungere il repository cloud IoT eseguendo questi comandi nella finestra del terminale:</span><span class="sxs-lookup"><span data-stu-id="b99f4-153">Add the IoT Cloud repository by running the following commands in a terminal window:</span></span>

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > <span data-ttu-id="b99f4-154">Digitare "y", quando viene richiesto se includere questo canale.</span><span class="sxs-lookup"><span data-stu-id="b99f4-154">Enter 'y', when it prompts you to 'Include this channel?'</span></span>
   
   <span data-ttu-id="b99f4-155">Se si riceve un errore `import read failed(-1)` usare i comandi seguenti per risolvere il problema:</span><span class="sxs-lookup"><span data-stu-id="b99f4-155">If you receive an `import read failed(-1)` error, use the following commands to resolve the issue:</span></span>
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   <span data-ttu-id="b99f4-156">Il comando `rpm` consente di importare la chiave rpm.</span><span class="sxs-lookup"><span data-stu-id="b99f4-156">The `rpm` command imports the rpm key.</span></span> <span data-ttu-id="b99f4-157">Il comando `smart channel` consente di aggiungere il canale rpm a Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="b99f4-157">The `smart channel` command adds the rpm channel to the Smart Package Manager.</span></span> <span data-ttu-id="b99f4-158">Prima dell'esecuzione del comando `smart update`, viene visualizzato un output come quello seguente.</span><span class="sxs-lookup"><span data-stu-id="b99f4-158">Before you run the `smart update` command, you will see an output like below.</span></span>

   ![output dei comandi di canale rpm e smart](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. <span data-ttu-id="b99f4-160">Eseguire il comando di aggiornamento smart:</span><span class="sxs-lookup"><span data-stu-id="b99f4-160">Execute the smart update command:</span></span>

   ```bash
   smart update
   ```

3. <span data-ttu-id="b99f4-161">Installare il pacchetto del gateway IoT di Azure eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="b99f4-161">Install the Azure IoT Gateway package by running the following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="b99f4-162">`packagegroup-cloud-azure` è il nome del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="b99f4-162">`packagegroup-cloud-azure` is the name of the package.</span></span> <span data-ttu-id="b99f4-163">Il comando `smart install` consente di installare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="b99f4-163">The `smart install` command is used to install the package.</span></span>

    > <span data-ttu-id="b99f4-164">Eseguire il comando seguente se viene visualizzato l'errore "public key not available" (chiave pubblica non disponibile)</span><span class="sxs-lookup"><span data-stu-id="b99f4-164">Run the following command if you see this error: 'public key not available'</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > <span data-ttu-id="b99f4-165">Riavviare Intel NUC se viene visualizzato l'errore: "no package provides util-linux-dev" (nessun pacchetto fornisce util-linux-dev)</span><span class="sxs-lookup"><span data-stu-id="b99f4-165">Reboot the Intel NUC if you see this error: 'no package provides util-linux-dev'</span></span>

   <span data-ttu-id="b99f4-166">Dopo l'installazione del pacchetto, Intel NUC è pronto per funzionare come gateway.</span><span class="sxs-lookup"><span data-stu-id="b99f4-166">After the package is installed, Intel NUC is ready to function as a gateway.</span></span>

## <a name="run-the-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="b99f4-167">Eseguire l'applicazione di esempio "hello_world" di Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="b99f4-167">Run the Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="b99f4-168">L'applicazione di esempio seguente crea un gateway dal file `hello_world.json` e usa i componenti principali dell'architettura di Azure IoT Edge per registrare un messaggio "hello world" in un file (log.txt) ogni 5 secondi.</span><span class="sxs-lookup"><span data-stu-id="b99f4-168">The following sample application creates a gateway from a `hello_world.json` file and uses the fundamental components of Azure IoT Edge architecture to log a hello world message to a file (log.txt) every 5 seconds.</span></span>

<span data-ttu-id="b99f4-169">È possibile eseguire l'esempio Hello World tramite i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b99f4-169">You can run the Hello World sample by executing the following commands:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="b99f4-170">Lasciare in esecuzione l'applicazione Hello World per alcuni minuti, quindi premere il tasto INVIO per arrestarla.</span><span class="sxs-lookup"><span data-stu-id="b99f4-170">Let the Hello World application run for a few minutes and then hit the Enter key to stop it.</span></span>
<span data-ttu-id="b99f4-171">![output dell'applicazione](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span><span class="sxs-lookup"><span data-stu-id="b99f4-171">![application output](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span></span>

> <span data-ttu-id="b99f4-172">È possibile ignorare eventuali errori "invalid argument handle(NULL)" (handle argomento non valido(NULL)" visualizzati dopo aver premuto INVIO. </span><span class="sxs-lookup"><span data-stu-id="b99f4-172">You can ignore any 'invalid argument handle(NULL)' errors that appear after you hit Enter.</span></span>

<span data-ttu-id="b99f4-173">È possibile verificare l'esecuzione corretta del gateway aprendo il file log.txt che ora si trova nella cartella hello_world: ![vista della directory log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span><span class="sxs-lookup"><span data-stu-id="b99f4-173">You can verify that the gateway ran successfully by opening the log.txt file that is now in your hello_world folder ![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span></span>

<span data-ttu-id="b99f4-174">Aprire il file log.txt con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b99f4-174">Open log.txt using the following command:</span></span>

```bash
vim log.txt
```

<span data-ttu-id="b99f4-175">Verranno visualizzati i contenuti del file log.txt, ovvero un output in formato JSON dei messaggi di log scritti ogni 5 secondi dal modulo Hello World del gateway.</span><span class="sxs-lookup"><span data-stu-id="b99f4-175">You will then see the contents of log.txt, which will be a JSON formatted output of the logging messages that were written every 5 seconds by the gateway Hello World module.</span></span>
<span data-ttu-id="b99f4-176">![vista della directory log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span><span class="sxs-lookup"><span data-stu-id="b99f4-176">![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span></span>

<span data-ttu-id="b99f4-177">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="b99f4-177">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="b99f4-178">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="b99f4-178">Summary</span></span>

<span data-ttu-id="b99f4-179">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="b99f4-179">Congratulations!</span></span> <span data-ttu-id="b99f4-180">La configurazione di Intel NUC come gateway è completata.</span><span class="sxs-lookup"><span data-stu-id="b99f4-180">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="b99f4-181">È ora possibile passare alla lezione successiva per configurare il computer host, creare un hub IoT di Azure e registrare il dispositivo logico dell'hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="b99f4-181">Now you're ready to move on to the next lesson to set up your host computer, create an Azure IoT Hub and register your Azure IoT Hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b99f4-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b99f4-182">Next steps</span></span>
<span data-ttu-id="b99f4-183">[Use an IoT gateway to connect a device to Azure IoT Hub](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md) (Usare un gateway IoT per connettere un dispositivo all'hub IoT di Azure)</span><span class="sxs-lookup"><span data-stu-id="b99f4-183">[Use an IoT gateway to connect a device to Azure IoT Hub](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)</span></span>

