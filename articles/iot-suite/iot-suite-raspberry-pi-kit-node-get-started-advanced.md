---
title: Connettere Raspberry Pi ad Azure IoT Suite usando Node.js per supportare gli aggiornamenti del firmware | Microsoft Docs
description: Usare lo Starter Kit di Microsoft Azure IoT per Raspberry Pi 3 e Azure IoT Suite. Usare Node.js per connettere Raspberry Pi alla soluzione di monitoraggio remoto, inviare dati di telemetria dai sensori al cloud ed eseguire un aggiornamento del firmware remoto.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 54503d5d6a636239d240509d7d09cf334234bac7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-enable-remote-firmware-updates-using-nodejs"></a><span data-ttu-id="56dec-104">Connettere Raspberry Pi 3 alla soluzione di monitoraggio remoto e attivare gli aggiornamenti del firmware remoto usando Node.js</span><span class="sxs-lookup"><span data-stu-id="56dec-104">Connect your Raspberry Pi 3 to the remote monitoring solution and enable remote firmware updates using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="56dec-105">Questa esercitazione illustra come usare lo Starter Kit di Microsoft Azure IoT per Raspberry Pi 3 per:</span><span class="sxs-lookup"><span data-stu-id="56dec-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="56dec-106">Sviluppare un lettore di temperatura e umidità in grado di comunicare con il cloud.</span><span class="sxs-lookup"><span data-stu-id="56dec-106">Develop a temperature and humidity reader that can communicate with the cloud.</span></span>
* <span data-ttu-id="56dec-107">Abilitare ed eseguire un aggiornamento del firmware remoto per aggiornare l'applicazione client su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="56dec-107">Enable and perform a remote firmware update to update the client application on the Raspberry Pi.</span></span>

<span data-ttu-id="56dec-108">L'esercitazione usa:</span><span class="sxs-lookup"><span data-stu-id="56dec-108">The tutorial uses:</span></span>

- <span data-ttu-id="56dec-109">Il sistema operativo Raspbian, il linguaggio di programmazione Node.js e Microsoft Azure IoT SDK per Node.js per implementare un dispositivo di esempio.</span><span class="sxs-lookup"><span data-stu-id="56dec-109">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span></span>
- <span data-ttu-id="56dec-110">La soluzione preconfigurata di monitoraggio remoto IoT Suite come back-end basato su cloud.</span><span class="sxs-lookup"><span data-stu-id="56dec-110">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="56dec-111">Panoramica</span><span class="sxs-lookup"><span data-stu-id="56dec-111">Overview</span></span>

<span data-ttu-id="56dec-112">In questa esercitazione si completa la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="56dec-112">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="56dec-113">Distribuire un'istanza della soluzione preconfigurata di monitoraggio remoto nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="56dec-113">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="56dec-114">Questo passaggio distribuisce e configura automaticamente più servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="56dec-114">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="56dec-115">Configurare il dispositivo e i sensori per la comunicazione con il computer e la soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="56dec-115">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="56dec-116">Aggiornare il codice del dispositivo di esempio per eseguire la connessione alla soluzione di monitoraggio remoto e inviare i dati di telemetria che è possibile visualizzare nel dashboard della soluzione.</span><span class="sxs-lookup"><span data-stu-id="56dec-116">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>
- <span data-ttu-id="56dec-117">Usare il codice del dispositivo di esempio per aggiornare l'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="56dec-117">Use the sample device code to update the client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="56dec-118">La soluzione di monitoraggio remota esegue il provisioning di un set di servizi di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="56dec-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="56dec-119">La distribuzione riflette un'architettura enterprise reale.</span><span class="sxs-lookup"><span data-stu-id="56dec-119">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="56dec-120">Per evitare costi di consumo di Azure non necessari, eliminare l'istanza della soluzione preconfigurata in azureiotsuite.com al completamento.</span><span class="sxs-lookup"><span data-stu-id="56dec-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="56dec-121">Se la soluzione preconfigurata occorre nuovamente, è possibile ricrearla facilmente.</span><span class="sxs-lookup"><span data-stu-id="56dec-121">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="56dec-122">Per altre informazioni sulla riduzione del consumo durante l'esecuzione della soluzione di monitoraggio remoto, vedere [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configurazione di soluzioni preconfigurate di Azure IoT Suite per scopi dimostrativi).</span><span class="sxs-lookup"><span data-stu-id="56dec-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="56dec-123">Scaricare e configurare l'esempio</span><span class="sxs-lookup"><span data-stu-id="56dec-123">Download and configure the sample</span></span>

<span data-ttu-id="56dec-124">È ora possibile scaricare e configurare l'applicazione client di monitoraggio remoto su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="56dec-124">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="56dec-125">Installare Node.js</span><span class="sxs-lookup"><span data-stu-id="56dec-125">Install Node.js</span></span>

<span data-ttu-id="56dec-126">Se non è già stato fatto, installare Node.js in Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="56dec-126">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="56dec-127">IoT SDK per Node.js richiede la versione 0.11.5 o successiva di Node.js.</span><span class="sxs-lookup"><span data-stu-id="56dec-127">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="56dec-128">I passaggi seguenti mostrano come installare Node.js v6.10.2 su Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="56dec-128">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="56dec-129">Usare il comando seguente per aggiornare Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="56dec-129">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="56dec-130">Usare il comando seguente per scaricare i file binari di Node.js su Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="56dec-130">Use the following command to download the Node.js binaries to your Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="56dec-131">Usare il comando seguente per installare i file binari:</span><span class="sxs-lookup"><span data-stu-id="56dec-131">Use the following command to install the binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="56dec-132">Usare il comando seguente per verificare di aver installato correttamente Node.js v6.10.2:</span><span class="sxs-lookup"><span data-stu-id="56dec-132">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a><span data-ttu-id="56dec-133">Clonare i repository</span><span class="sxs-lookup"><span data-stu-id="56dec-133">Clone the repositories</span></span>

<span data-ttu-id="56dec-134">Se non è già stato fatto, clonare i repository necessari eseguendo i comandi seguenti nel Pi:</span><span class="sxs-lookup"><span data-stu-id="56dec-134">If you haven't done so already, clone the required repositories by running the following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="56dec-135">Aggiornare la stringa di connessione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="56dec-135">Update the device connection string</span></span>

<span data-ttu-id="56dec-136">Aprire il file di configurazione di esempio nell'editor **nano** usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="56dec-136">Open the sample configuration file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="56dec-137">Sostituire i valori segnaposto con l'id del dispositivo e informazioni dell'hub IoT creati e salvati all'inizio di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="56dec-137">Replace the placeholder values with the device id and IoT Hub information you created and saved at the start of this tutorial.</span></span>

<span data-ttu-id="56dec-138">Al termine, il contenuto del file deviceinfo dovrebbe essere simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="56dec-138">When you are done, the contents of the deviceinfo file should look like the following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="56dec-139">Salvare le modifiche (**Ctrl+O**, **INVIO**) e chiudere l'editor (**Ctrl+X**).</span><span class="sxs-lookup"><span data-stu-id="56dec-139">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="56dec-140">Eseguire l'esempio</span><span class="sxs-lookup"><span data-stu-id="56dec-140">Run the sample</span></span>

<span data-ttu-id="56dec-141">Eseguire i comandi seguenti per installare i pacchetti prerequisiti per l'esempio:</span><span class="sxs-lookup"><span data-stu-id="56dec-141">Run the following commands to install the prerequisite packages for the sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advance/1.0
npm install
```

<span data-ttu-id="56dec-142">È ora possibile eseguire il programma di esempio su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="56dec-142">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="56dec-143">Immettere il comando:</span><span class="sxs-lookup"><span data-stu-id="56dec-143">Enter the command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/1.0/remote_monitoring.js
```

<span data-ttu-id="56dec-144">L'output seguente riporta un esempio dell'output visualizzato al prompt dei comandi su Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="56dec-144">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Output dell'app Raspberry Pi][img-raspberry-output]

<span data-ttu-id="56dec-146">Premere **CTRL+C** per uscire dal programma in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="56dec-146">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="56dec-147">Nel dashboard della soluzione fare clic su **Dispositivi** per passare alla pagina **Dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="56dec-147">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="56dec-148">Selezionare Raspberry Pi in **Elenco dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="56dec-148">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="56dec-149">Quindi scegliere **Metodi**:</span><span class="sxs-lookup"><span data-stu-id="56dec-149">Then choose **Methods**:</span></span>

    ![Elencare i dispositivi nel dashboard][img-list-devices]

1. <span data-ttu-id="56dec-151">Nella pagina **Richiama metodo**, scegliere **InitiateFirmwareUpdate** nell'elenco a discesa **Metodo**.</span><span class="sxs-lookup"><span data-stu-id="56dec-151">On the **Invoke Method** page, choose **InitiateFirmwareUpdate** in the **Method** dropdown.</span></span>

1. <span data-ttu-id="56dec-152">Nel campo **FWPackageURI** immettere **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span><span class="sxs-lookup"><span data-stu-id="56dec-152">In the **FWPackageURI** field, enter **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span></span> <span data-ttu-id="56dec-153">Questo file contiene l'implementazione della versione 2.0 del firmware.</span><span class="sxs-lookup"><span data-stu-id="56dec-153">This file contains the implementation of version 2.0 of the firmware.</span></span>

1. <span data-ttu-id="56dec-154">Scegliere **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="56dec-154">Choose **InvokeMethod**.</span></span> <span data-ttu-id="56dec-155">L'app su Raspberry Pi invia un riconoscimento al dashboard della soluzione.</span><span class="sxs-lookup"><span data-stu-id="56dec-155">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard.</span></span> <span data-ttu-id="56dec-156">Avvia quindi il processo di aggiornamento del firmware scaricando la nuova versione del firmware:</span><span class="sxs-lookup"><span data-stu-id="56dec-156">It then starts the firmware update process by downloading the new version of the firmware:</span></span>

    ![Visualizzare la cronologia del metodo][img-method-history]

## <a name="observe-the-firmware-update-process"></a><span data-ttu-id="56dec-158">Osservare il processo di aggiornamento del firmware</span><span class="sxs-lookup"><span data-stu-id="56dec-158">Observe the firmware update process</span></span>

<span data-ttu-id="56dec-159">È possibile osservare il processo di aggiornamento del firmware durante l'esecuzione nel dispositivo e visualizzando le proprietà dichiarate nel dashboard della soluzione:</span><span class="sxs-lookup"><span data-stu-id="56dec-159">You can observe the firmware update process as it runs on the device and by viewing the reported properties in the solution dashboard:</span></span>

1. <span data-ttu-id="56dec-160">È possibile visualizzare lo stato di avanzamento del processo di aggiornamento su Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="56dec-160">You can view the progress in of the update process on the Raspberry Pi:</span></span>

    ![Mostra l'avanzamento dell'aggiornamento][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="56dec-162">L'applicazione di monitoraggio remoto viene riavviata automaticamente al termine dell'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="56dec-162">The remote monitoring app restarts silently when the update completes.</span></span> <span data-ttu-id="56dec-163">Usare il comando `ps -ef` per verificare che sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="56dec-163">Use the command `ps -ef` to verify it is running.</span></span> <span data-ttu-id="56dec-164">Se si vuole terminare il processo, usare il comando `kill` con l'id del processo.</span><span class="sxs-lookup"><span data-stu-id="56dec-164">If you want to terminate the process, use the `kill` command with the process id.</span></span>

1. <span data-ttu-id="56dec-165">È possibile visualizzare lo stato dell'aggiornamento del firmware, come segnalato dal dispositivo, nel portale della soluzione.</span><span class="sxs-lookup"><span data-stu-id="56dec-165">You can view the status of the firmware update, as reported by the device, in the solution portal.</span></span> <span data-ttu-id="56dec-166">La schermata seguente mostra lo stato e la durata di ogni fase del processo di aggiornamento e la nuova versione del firmware:</span><span class="sxs-lookup"><span data-stu-id="56dec-166">The following screenshot shows the status and duration of each stage of the update process, and the new firmware version:</span></span>

    ![Mostra lo stato del processo][img-job-status]

    <span data-ttu-id="56dec-168">Se si passa nuovamente al dashboard, è possibile verificare che il dispositivo sta ancora inviando i dati di telemetria dopo l'aggiornamento del firmware.</span><span class="sxs-lookup"><span data-stu-id="56dec-168">If you navigate back to the dashboard, you can verify the device is still sending telemetry following the firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="56dec-169">Se si lascia la soluzione di monitoraggio remoto in esecuzione nell'account Azure, verrà addebitato il tempo dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="56dec-169">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="56dec-170">Per altre informazioni sulla riduzione del consumo durante l'esecuzione della soluzione di monitoraggio remoto, vedere [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configurazione di soluzioni preconfigurate di Azure IoT Suite per scopi dimostrativi).</span><span class="sxs-lookup"><span data-stu-id="56dec-170">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="56dec-171">Al termine, eliminare la soluzione preconfigurata dall'account Azure.</span><span class="sxs-lookup"><span data-stu-id="56dec-171">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56dec-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="56dec-172">Next steps</span></span>

<span data-ttu-id="56dec-173">Visitare il [Centro per sviluppatori Azure IoT](https://azure.microsoft.com/develop/iot/) per altri esempi e documentazione su Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="56dec-173">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
