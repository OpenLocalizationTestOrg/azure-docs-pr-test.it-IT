---
title: 'Dispositivo SensorTag e gateway Azure IoT: lezione 1: Configurare Intel NUC | Microsoft Docs'
description: Impostare toowork Intel NUC come gateway tra un sensore e informazioni di sensore toocollect Azure IoT Hub IoT e inviarla tooIoT Hub.
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
ms.openlocfilehash: 7c3ab3b014713c7facb86b8e8622d70e60a960e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="b8479-104">Configurare Intel NUC come gateway IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="b8479-104">Set up Intel NUC as an IoT gateway</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a><span data-ttu-id="b8479-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="b8479-105">What you will do</span></span>

- <span data-ttu-id="b8479-106">Configurare Intel NUC come gateway IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="b8479-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="b8479-107">Installare il pacchetto di Azure IoT Edge hello in hello NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="b8479-107">Install hello Azure IoT Edge package on hello Intel NUC.</span></span>
- <span data-ttu-id="b8479-108">Eseguire un'applicazione di esempio "hello_world" in funzionalità del gateway di Intel NUC tooverify hello hello.</span><span class="sxs-lookup"><span data-stu-id="b8479-108">Run a "hello_world" sample application on hello Intel NUC tooverify hello gateway functionality.</span></span>

  > <span data-ttu-id="b8479-109">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="b8479-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b8479-110">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="b8479-110">What you will learn</span></span>

<span data-ttu-id="b8479-111">In questa lezione si apprenderà:</span><span class="sxs-lookup"><span data-stu-id="b8479-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="b8479-112">Come tooconnect Intel NUC con le periferiche.</span><span class="sxs-lookup"><span data-stu-id="b8479-112">How tooconnect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="b8479-113">Come tooinstall e aggiornare i pacchetti hello necessarie sull'uso di Intel NUC hello Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="b8479-113">How tooinstall and update hello required packages on Intel NUC using hello Smart Package Manager.</span></span>
- <span data-ttu-id="b8479-114">Modalità di esempio funzionalità di gateway applicazione tooverify hello hello_world"toorun hello".</span><span class="sxs-lookup"><span data-stu-id="b8479-114">How toorun hello "hello_world" sample application tooverify hello gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b8479-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="b8479-115">What you need</span></span>

- <span data-ttu-id="b8479-116">Un Intel NUC Kit DE3815TYKE con hello Suite Software Gateway IoT di Intel (vento distretto Linux * 7.0.0.13) preinstallato.</span><span class="sxs-lookup"><span data-stu-id="b8479-116">An Intel NUC Kit DE3815TYKE with hello Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span> <span data-ttu-id="b8479-117">[Fare clic qui toopurchase Groove IoT commerciale Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span><span class="sxs-lookup"><span data-stu-id="b8479-117">[Click here toopurchase Grove IoT Commercial Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span></span>
- <span data-ttu-id="b8479-118">Un cavo Ethernet.</span><span class="sxs-lookup"><span data-stu-id="b8479-118">An Ethernet cable.</span></span>
- <span data-ttu-id="b8479-119">Una tastiera.</span><span class="sxs-lookup"><span data-stu-id="b8479-119">A keyboard.</span></span>
- <span data-ttu-id="b8479-120">Un cavo HDMI o VGA.</span><span class="sxs-lookup"><span data-stu-id="b8479-120">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="b8479-121">Un monitor con porta HDMI o VGA.</span><span class="sxs-lookup"><span data-stu-id="b8479-121">A monitor with an HDMI or VGA port.</span></span>
- <span data-ttu-id="b8479-122">Facoltativo: [SensorTag di Texas Instruments (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span><span class="sxs-lookup"><span data-stu-id="b8479-122">Optional: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span></span>

![Kit gateway](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a><span data-ttu-id="b8479-124">La connessione di Intel NUC con le periferiche hello</span><span class="sxs-lookup"><span data-stu-id="b8479-124">Connect Intel NUC with hello peripherals</span></span>

<span data-ttu-id="b8479-125">immagine di Hello riportata di seguito è riportato un esempio di Intel NUC connesso con le periferiche diverse:</span><span class="sxs-lookup"><span data-stu-id="b8479-125">hello image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="b8479-126">Tastiera tooa connesso.</span><span class="sxs-lookup"><span data-stu-id="b8479-126">Connected tooa keyboard.</span></span>
2. <span data-ttu-id="b8479-127">Monitoraggio tooa la connessione con un cavo o un cavo HDMI.</span><span class="sxs-lookup"><span data-stu-id="b8479-127">Connected tooa monitor with a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="b8479-128">Connesso tooa rete tramite un cavo Ethernet cablata.</span><span class="sxs-lookup"><span data-stu-id="b8479-128">Connected tooa wired network with an Ethernet cable.</span></span>
4. <span data-ttu-id="b8479-129">Alimentatore tooa connessi con un cavo di alimentazione.</span><span class="sxs-lookup"><span data-stu-id="b8479-129">Connected tooa power supply with a power cable.</span></span>

![Tooperipherals NUC Intel connesso](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="b8479-131">Connettere il sistema di Intel NUC toohello dal computer host tramite Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="b8479-131">Connect toohello Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="b8479-132">È necessario una tastiera e un indirizzo IP di monitoraggio tooget hello del dispositivo NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="b8479-132">You will need a keyboard and a monitor tooget hello IP address of your Intel NUC device.</span></span> <span data-ttu-id="b8479-133">Se si conosce già hello IP indirizzo, è possibile ignorare toostep ahead 3 di questa sezione.</span><span class="sxs-lookup"><span data-stu-id="b8479-133">If you already know hello IP address, you can skip ahead toostep 3 in this section.</span></span>

1. <span data-ttu-id="b8479-134">Attivare hello Intel NUC premendo il pulsante di alimentazione hello e l'accesso.</span><span class="sxs-lookup"><span data-stu-id="b8479-134">Turn on hello Intel NUC by pressing hello power button and then log in.</span></span>

   <span data-ttu-id="b8479-135">nome Hello predefinito dell'utente e password sono entrambi `root`.</span><span class="sxs-lookup"><span data-stu-id="b8479-135">hello default user name and password are both `root`.</span></span>

       > Hit hello enter key on your keyboard if you see either of hello following errors when you boot: 'A TPM error (7) occurred attempting tooread a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. <span data-ttu-id="b8479-136">Ottenere l'indirizzo IP hello di hello Intel NUC eseguendo hello `ifconfig` comando sul dispositivo Intel NUC hello.</span><span class="sxs-lookup"><span data-stu-id="b8479-136">Get hello IP address of hello Intel NUC by running hello `ifconfig` command on hello Intel NUC device.</span></span>

   <span data-ttu-id="b8479-137">Di seguito è riportato un esempio di output del comando hello.</span><span class="sxs-lookup"><span data-stu-id="b8479-137">Here is an example of hello command output.</span></span>

   ![Output di ifconfig che indica l'IP di Intel NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="b8479-139">In questo esempio hello che segue `inet addr:` è l'indirizzo IP hello che è necessario connettersi quando toohello Intel NUC da un computer host.</span><span class="sxs-lookup"><span data-stu-id="b8479-139">In this example, hello value that follows `inet addr:` is hello IP address that you need when connect toohello Intel NUC from a host computer.</span></span>

3. <span data-ttu-id="b8479-140">Utilizzare uno dei seguenti client SSH dagli tooIntel di tooconnect computer host NUC hello.</span><span class="sxs-lookup"><span data-stu-id="b8479-140">Use one of hello following SSH clients from your host computer tooconnect tooIntel NUC.</span></span>

    - <span data-ttu-id="b8479-141">[PuTTY](http://www.putty.org/) per Windows.</span><span class="sxs-lookup"><span data-stu-id="b8479-141">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="b8479-142">client SSH incorporato Hello in Ubuntu o macOS.</span><span class="sxs-lookup"><span data-stu-id="b8479-142">hello built-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="b8479-143">È più efficiente e produttivo toooperate un NUC Intel da un computer host.</span><span class="sxs-lookup"><span data-stu-id="b8479-143">It is more efficient and productive toooperate an Intel NUC from a host computer.</span></span> <span data-ttu-id="b8479-144">Si sarà necessario hello indirizzo IP del NUC Intel, tooit di tooconnect di nome e una password utente tramite un client SSH.</span><span class="sxs-lookup"><span data-stu-id="b8479-144">You'll need hello Intel NUC's IP address, user name and password tooconnect tooit via an SSH client.</span></span> <span data-ttu-id="b8479-145">Di seguito è riportato un esempio che usa un client SSH in macOS.</span><span class="sxs-lookup"><span data-stu-id="b8479-145">Here is an example that uses an SSH client on macOS.</span></span>
   <span data-ttu-id="b8479-146">![Client SSH eseguito su macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="b8479-146">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-hello-azure-iot-edge-package"></a><span data-ttu-id="b8479-147">Installare il pacchetto di hello Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="b8479-147">Install hello Azure IoT Edge package</span></span>

<span data-ttu-id="b8479-148">pacchetto di Azure IoT Edge Hello contiene i file binari precompilati hello di IoT Edge e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="b8479-148">hello Azure IoT Edge package contains hello pre-compiled binaries of IoT Edge and its dependencies.</span></span> <span data-ttu-id="b8479-149">Questi binari sono Azure IoT Edge, hello Azure IoT SDK e strumenti corrispondenti hello.</span><span class="sxs-lookup"><span data-stu-id="b8479-149">These binaries are Azure IoT Edge, hello Azure IoT SDK and hello corresponding tools.</span></span> <span data-ttu-id="b8479-150">Hello pacchetto contiene anche un "hello_world" applicazione di esempio è una funzionalità di gateway hello toovalidate utilizzato.</span><span class="sxs-lookup"><span data-stu-id="b8479-150">hello package also contains a "hello_world" sample application is used toovalidate hello gateway functionality.</span></span> <span data-ttu-id="b8479-151">Bordo di IoT è fondamentale hello del gateway hello.</span><span class="sxs-lookup"><span data-stu-id="b8479-151">IoT Edge is hello core part of hello gateway.</span></span> 

<span data-ttu-id="b8479-152">Seguire questi pacchetti hello tooinstall di passaggi.</span><span class="sxs-lookup"><span data-stu-id="b8479-152">Follow these steps tooinstall hello package.</span></span>

1. <span data-ttu-id="b8479-153">Aggiungere hello repository IoT Cloud eseguendo i seguenti comandi in una finestra terminale hello:</span><span class="sxs-lookup"><span data-stu-id="b8479-153">Add hello IoT Cloud repository by running hello following commands in a terminal window:</span></span>

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > <span data-ttu-id="b8479-154">Immettere 'y', quando viene richiesto too'Include questo canale?'</span><span class="sxs-lookup"><span data-stu-id="b8479-154">Enter 'y', when it prompts you too'Include this channel?'</span></span>
   
   <span data-ttu-id="b8479-155">Se si riceve un `import read failed(-1)` errore, utilizzare hello problema di hello tooresolve i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b8479-155">If you receive an `import read failed(-1)` error, use hello following commands tooresolve hello issue:</span></span>
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   <span data-ttu-id="b8479-156">Hello `rpm` comando importazioni hello chiave rpm.</span><span class="sxs-lookup"><span data-stu-id="b8479-156">hello `rpm` command imports hello rpm key.</span></span> <span data-ttu-id="b8479-157">Hello `smart channel` comando aggiunge rpm hello canale toohello Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="b8479-157">hello `smart channel` command adds hello rpm channel toohello Smart Package Manager.</span></span> <span data-ttu-id="b8479-158">Prima di eseguire hello `smart update` comando, verrà visualizzato un output come il seguente.</span><span class="sxs-lookup"><span data-stu-id="b8479-158">Before you run hello `smart update` command, you will see an output like below.</span></span>

   ![output dei comandi di canale rpm e smart](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. <span data-ttu-id="b8479-160">Eseguire il comando di aggiornamento smart hello:</span><span class="sxs-lookup"><span data-stu-id="b8479-160">Execute hello smart update command:</span></span>

   ```bash
   smart update
   ```

3. <span data-ttu-id="b8479-161">Installare il pacchetto di Azure IoT Gateway hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b8479-161">Install hello Azure IoT Gateway package by running hello following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="b8479-162">`packagegroup-cloud-azure`è il nome di hello del pacchetto di hello.</span><span class="sxs-lookup"><span data-stu-id="b8479-162">`packagegroup-cloud-azure` is hello name of hello package.</span></span> <span data-ttu-id="b8479-163">Hello `smart install` comando è il pacchetto di hello tooinstall utilizzato.</span><span class="sxs-lookup"><span data-stu-id="b8479-163">hello `smart install` command is used tooinstall hello package.</span></span>

    > <span data-ttu-id="b8479-164">Comando che segue hello esecuzione se viene visualizzato questo errore: "chiave pubblica non disponibile"</span><span class="sxs-lookup"><span data-stu-id="b8479-164">Run hello following command if you see this error: 'public key not available'</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > <span data-ttu-id="b8479-165">Riavviare hello Intel NUC se viene visualizzato questo errore: 'alcun pacchetto non fornisce util-linux-dev'</span><span class="sxs-lookup"><span data-stu-id="b8479-165">Reboot hello Intel NUC if you see this error: 'no package provides util-linux-dev'</span></span>

   <span data-ttu-id="b8479-166">Dopo aver installato il pacchetto di hello, Intel NUC è pronto toofunction come gateway.</span><span class="sxs-lookup"><span data-stu-id="b8479-166">After hello package is installed, Intel NUC is ready toofunction as a gateway.</span></span>

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="b8479-167">Eseguire l'applicazione di esempio "hello_world" hello Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="b8479-167">Run hello Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="b8479-168">Hello dopo l'applicazione di esempio crea un gateway da un `hello_world.json` file e utilizza i componenti fondamentali di hello del bordo di Azure IoT architettura toolog un file di hello world messaggio tooa (txt) ogni 5 secondi.</span><span class="sxs-lookup"><span data-stu-id="b8479-168">hello following sample application creates a gateway from a `hello_world.json` file and uses hello fundamental components of Azure IoT Edge architecture toolog a hello world message tooa file (log.txt) every 5 seconds.</span></span>

<span data-ttu-id="b8479-169">È possibile eseguire l'esempio hello World Hello eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="b8479-169">You can run hello Hello World sample by executing hello following commands:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="b8479-170">Consente di eseguire per alcuni minuti e quindi premere hello invio chiave toostop applicazione hello World Hello è.</span><span class="sxs-lookup"><span data-stu-id="b8479-170">Let hello Hello World application run for a few minutes and then hit hello Enter key toostop it.</span></span>
<span data-ttu-id="b8479-171">![output dell'applicazione](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span><span class="sxs-lookup"><span data-stu-id="b8479-171">![application output](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span></span>

> <span data-ttu-id="b8479-172">È possibile ignorare eventuali errori "invalid argument handle(NULL)" (handle argomento non valido(NULL)" visualizzati dopo aver premuto INVIO. </span><span class="sxs-lookup"><span data-stu-id="b8479-172">You can ignore any 'invalid argument handle(NULL)' errors that appear after you hit Enter.</span></span>

<span data-ttu-id="b8479-173">È possibile verificare tale gateway hello è stato eseguito correttamente, aprire i file di log. txt hello che si trova ora nella cartella hello_world ![visualizzazione directory >.log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span><span class="sxs-lookup"><span data-stu-id="b8479-173">You can verify that hello gateway ran successfully by opening hello log.txt file that is now in your hello_world folder ![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span></span>

<span data-ttu-id="b8479-174">Aprire i log. txt utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b8479-174">Open log.txt using hello following command:</span></span>

```bash
vim log.txt
```

<span data-ttu-id="b8479-175">Verrà quindi visualizzato il contenuto di hello del log. txt, sarà un output in formato JSON di hello la registrazione dei messaggi che sono stati scritti ogni 5 secondi dal modulo di Hello World hello gateway.</span><span class="sxs-lookup"><span data-stu-id="b8479-175">You will then see hello contents of log.txt, which will be a JSON formatted output of hello logging messages that were written every 5 seconds by hello gateway Hello World module.</span></span>
<span data-ttu-id="b8479-176">![vista della directory log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span><span class="sxs-lookup"><span data-stu-id="b8479-176">![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span></span>

<span data-ttu-id="b8479-177">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="b8479-177">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="b8479-178">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="b8479-178">Summary</span></span>

<span data-ttu-id="b8479-179">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="b8479-179">Congratulations!</span></span> <span data-ttu-id="b8479-180">La configurazione di Intel NUC come gateway è completata.</span><span class="sxs-lookup"><span data-stu-id="b8479-180">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="b8479-181">Si è pronti toomove su toohello tooset lezione al successivo backup del computer host, creare un IoT Hub di Azure e registrare il dispositivo logico IoT Hub di Azure.</span><span class="sxs-lookup"><span data-stu-id="b8479-181">Now you're ready toomove on toohello next lesson tooset up your host computer, create an Azure IoT Hub and register your Azure IoT Hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8479-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b8479-182">Next steps</span></span>
[<span data-ttu-id="b8479-183">Utilizzare un tooconnect di gateway tooAzure un dispositivo IoT Hub IoT</span><span class="sxs-lookup"><span data-stu-id="b8479-183">Use an IoT gateway tooconnect a device tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

