---
title: Aggiorna IoT Suite utilizzando C toosupport firmware aaaConnect un tooAzure Pi Raspberry | Documenti Microsoft
description: Utilizzare hello Starter Kit di Microsoft Azure IoT per hello Raspberry Pi 3 e Azure IoT Suite. Utilizzare tooconnect C toohello le Pi Raspberry soluzione di monitoraggio remoto, inviare i dati di telemetria da sensori toohello cloud ed eseguire un aggiornamento remoto del firmware.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 36d39c6d754ddb025fd3f6b74d7795ed907b754c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-c"></a><span data-ttu-id="6fd17-104">Connettere il toohello Raspberry Pi 3 soluzione di monitoraggio remoto e abilitare gli aggiornamenti del firmware remoto utilizzando C</span><span class="sxs-lookup"><span data-stu-id="6fd17-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and enable remote firmware updates using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="6fd17-105">Questa esercitazione viene illustrato come toouse hello IoT Starter Kit di Microsoft Azure per 3 Pi Raspberry per:</span><span class="sxs-lookup"><span data-stu-id="6fd17-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="6fd17-106">Sviluppare un lettore di temperatura e umidità in grado di comunicare con il cloud hello.</span><span class="sxs-lookup"><span data-stu-id="6fd17-106">Develop a temperature and humidity reader that can communicate with hello cloud.</span></span>
* <span data-ttu-id="6fd17-107">Abilitare ed eseguire un'applicazione client di firmware remote update tooupdate hello in hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6fd17-107">Enable and perform a remote firmware update tooupdate hello client application on hello Raspberry Pi.</span></span>

<span data-ttu-id="6fd17-108">esercitazione Hello utilizza:</span><span class="sxs-lookup"><span data-stu-id="6fd17-108">hello tutorial uses:</span></span>

* <span data-ttu-id="6fd17-109">Sistema operativo Raspbian, linguaggio di programmazione C hello e hello Microsoft Azure IoT SDK per C tooimplement un dispositivo di esempio.</span><span class="sxs-lookup"><span data-stu-id="6fd17-109">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
* <span data-ttu-id="6fd17-110">monitoraggio remoto IoT Suite Hello preconfigurato soluzione come hello basato su cloud back-end.</span><span class="sxs-lookup"><span data-stu-id="6fd17-110">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="6fd17-111">Panoramica</span><span class="sxs-lookup"><span data-stu-id="6fd17-111">Overview</span></span>

<span data-ttu-id="6fd17-112">In questa esercitazione è completare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6fd17-112">In this tutorial, you complete hello following steps:</span></span>

* <span data-ttu-id="6fd17-113">Distribuire un'istanza di hello remoto monitoraggio soluzione preconfigurata tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6fd17-113">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="6fd17-114">Questo passaggio distribuisce e configura automaticamente più servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="6fd17-114">This step automatically deploys and configures multiple Azure services.</span></span>
* <span data-ttu-id="6fd17-115">Consente di impostare il dispositivo e sensori di toocommunicate con il computer e hello soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="6fd17-115">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
* <span data-ttu-id="6fd17-116">Aggiornare hello esempio dispositivo codice tooconnect toohello soluzione di monitoraggio remoto e inviare dati di telemetria che è possibile visualizzare nel dashboard di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="6fd17-116">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>
* <span data-ttu-id="6fd17-117">Utilizzare l'esempio dispositivo codice tooupdate hello client un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="6fd17-117">Use hello sample device code tooupdate hello client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="6fd17-118">Hello remoto disposizioni soluzione monitoraggio di un set di servizi di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6fd17-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="6fd17-119">distribuzione di Hello riflette un'architettura aziendale reale.</span><span class="sxs-lookup"><span data-stu-id="6fd17-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="6fd17-120">tooavoid addebiti di consumo di Azure, eliminare l'istanza di soluzione hello preconfigurato azureiotsuite.com dopo aver con esso.</span><span class="sxs-lookup"><span data-stu-id="6fd17-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="6fd17-121">Se è necessario hello nuovamente la soluzione preconfigurata, è possibile ricrearla facilmente.</span><span class="sxs-lookup"><span data-stu-id="6fd17-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="6fd17-122">Per ulteriori informazioni sulla riduzione del consumo durante l'esecuzione di soluzioni di monitoraggio remoto hello, vedere [configurazione Azure IoT Suite preconfigurato soluzioni per scopi dimostrativi][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="6fd17-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="6fd17-123">Scaricare e configurare l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="6fd17-123">Download and configure hello sample</span></span>

<span data-ttu-id="6fd17-124">È ora possibile scaricare e configurare l'applicazione client per il monitoraggio remoto di hello nelle Pi Raspberry.</span><span class="sxs-lookup"><span data-stu-id="6fd17-124">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="6fd17-125">Clonare il repository hello</span><span class="sxs-lookup"><span data-stu-id="6fd17-125">Clone hello repositories</span></span>

<span data-ttu-id="6fd17-126">Se non è già fatto, hello clone richiesto repository eseguendo hello seguendo i comandi del Pi:</span><span class="sxs-lookup"><span data-stu-id="6fd17-126">If you haven't done so already, clone hello required repositories by running hello following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="6fd17-127">Aggiornare la stringa di connessione dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="6fd17-127">Update hello device connection string</span></span>

<span data-ttu-id="6fd17-128">File di configurazione di esempio hello Open in hello **nano** editor utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6fd17-128">Open hello sample configuration file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="6fd17-129">Sostituire i valori segnaposto hello con hello ID e l'IoT Hub informazioni sul dispositivo è stato creato e salvato all'inizio di hello di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="6fd17-129">Replace hello placeholder values with hello device ID and IoT Hub information you created and saved at hello start of this tutorial.</span></span>

<span data-ttu-id="6fd17-130">Al termine, il contenuto di hello del file di deviceinfo hello dovrebbe essere simile hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="6fd17-130">When you are done, hello contents of hello deviceinfo file should look like hello following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="6fd17-131">Salvare le modifiche (**Ctrl O**, **invio**) e uscire dall'editor hello (**Ctrl + X**).</span><span class="sxs-lookup"><span data-stu-id="6fd17-131">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="6fd17-132">Compilare l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="6fd17-132">Build hello sample</span></span>

<span data-ttu-id="6fd17-133">Se non è già stato fatto, installare i pacchetti dei prerequisiti per Microsoft Azure IoT dispositivo SDK hello hello per C eseguendo hello seguendo i comandi in un terminal hello Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="6fd17-133">If you have not already done so, install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="6fd17-134">È ora possibile compilare la soluzione di esempio hello su hello Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="6fd17-134">You can now build hello sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
```

<span data-ttu-id="6fd17-135">È ora possibile eseguire il programma di esempio hello in hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6fd17-135">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="6fd17-136">Immettere il comando hello:</span><span class="sxs-lookup"><span data-stu-id="6fd17-136">Enter hello command:</span></span>

  ```sh
  sudo ~/cmake/remote_monitoring/remote_monitoring
  ```

<span data-ttu-id="6fd17-137">Hello riportato di seguito è riportato un esempio di output di hello visualizzato al prompt dei comandi di hello in hello Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="6fd17-137">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Output dell'app Raspberry Pi][img-raspberry-output]

<span data-ttu-id="6fd17-139">Premere **Ctrl-C** programma hello tooexit in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="6fd17-139">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="6fd17-140">Nel dashboard di soluzione hello, fare clic su **dispositivi** toovisit hello **dispositivi** pagina.</span><span class="sxs-lookup"><span data-stu-id="6fd17-140">In hello solution dashboard, click **Devices** toovisit hello **Devices** page.</span></span> <span data-ttu-id="6fd17-141">Selezionare le Pi Raspberry hello **elenco dei dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="6fd17-141">Select your Raspberry Pi in hello **Device List**.</span></span> <span data-ttu-id="6fd17-142">Quindi scegliere **Metodi**:</span><span class="sxs-lookup"><span data-stu-id="6fd17-142">Then choose **Methods**:</span></span>

    ![Elencare i dispositivi nel dashboard][img-list-devices]

1. <span data-ttu-id="6fd17-144">In hello **Richiama metodo** pagina, scegliere **InitiateFirmwareUpdate** in hello **metodo** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="6fd17-144">On hello **Invoke Method** page, choose **InitiateFirmwareUpdate** in hello **Method** dropdown.</span></span>

1. <span data-ttu-id="6fd17-145">In hello **FWPackageURI** immettere **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span><span class="sxs-lookup"><span data-stu-id="6fd17-145">In hello **FWPackageURI** field, enter **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span></span> <span data-ttu-id="6fd17-146">Questo file di archivio contiene l'implementazione di hello della versione 2.0 del firmware hello.</span><span class="sxs-lookup"><span data-stu-id="6fd17-146">This archive file contains hello implementation of version 2.0 of hello firmware.</span></span>

1. <span data-ttu-id="6fd17-147">Scegliere **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="6fd17-147">Choose **InvokeMethod**.</span></span> <span data-ttu-id="6fd17-148">app Hello in hello Pi Raspberry invia un dashboard di soluzione toohello indietro di riconoscimento.</span><span class="sxs-lookup"><span data-stu-id="6fd17-148">hello app on hello Raspberry Pi sends an acknowledgment back toohello solution dashboard.</span></span> <span data-ttu-id="6fd17-149">Quindi Avvia processo di aggiornamento del firmware hello download hello della nuova versione del firmware hello:</span><span class="sxs-lookup"><span data-stu-id="6fd17-149">It then starts hello firmware update process by downloading hello new version of hello firmware:</span></span>

    ![Visualizzare la cronologia del metodo][img-method-history]

## <a name="observe-hello-firmware-update-process"></a><span data-ttu-id="6fd17-151">Processo di aggiornamento del firmware hello osservare</span><span class="sxs-lookup"><span data-stu-id="6fd17-151">Observe hello firmware update process</span></span>

<span data-ttu-id="6fd17-152">È possibile osservare processo di aggiornamento del firmware hello mentre è in esecuzione sul dispositivo hello e visualizzando hello segnalati proprietà nel dashboard di soluzione hello:</span><span class="sxs-lookup"><span data-stu-id="6fd17-152">You can observe hello firmware update process as it runs on hello device and by viewing hello reported properties in hello solution dashboard:</span></span>

1. <span data-ttu-id="6fd17-153">È possibile visualizzare l'avanzamento di hello del processo di aggiornamento hello in hello Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="6fd17-153">You can view hello progress in of hello update process on hello Raspberry Pi:</span></span>

    ![Mostra l'avanzamento dell'aggiornamento][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="6fd17-155">applicazione di monitoraggio remoto Hello viene riavviato automaticamente al termine dell'aggiornamento hello.</span><span class="sxs-lookup"><span data-stu-id="6fd17-155">hello remote monitoring app restarts silently when hello update completes.</span></span> <span data-ttu-id="6fd17-156">Utilizzare il comando hello `ps -ef` tooverify è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6fd17-156">Use hello command `ps -ef` tooverify it is running.</span></span> <span data-ttu-id="6fd17-157">Se si desidera che il processo di hello tooterminate, utilizzare hello `kill` comando con id processo hello.</span><span class="sxs-lookup"><span data-stu-id="6fd17-157">If you want tooterminate hello process, use hello `kill` command with hello process id.</span></span>

1. <span data-ttu-id="6fd17-158">È possibile visualizzare lo stato di hello di aggiornamento del firmware hello, come segnalato dal dispositivo hello, nel portale di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="6fd17-158">You can view hello status of hello firmware update, as reported by hello device, in hello solution portal.</span></span> <span data-ttu-id="6fd17-159">Hello schermata seguente mostra lo stato di hello e la durata di ogni fase del processo di aggiornamento hello e la nuova versione del firmware di hello:</span><span class="sxs-lookup"><span data-stu-id="6fd17-159">hello following screenshot shows hello status and duration of each stage of hello update process, and hello new firmware version:</span></span>

    ![Mostra lo stato del processo][img-job-status]

    <span data-ttu-id="6fd17-161">Se si passa indietro toohello dashboard, è possibile verificare dispositivo hello sta ancora inviando dati di telemetria dopo l'aggiornamento del firmware hello.</span><span class="sxs-lookup"><span data-stu-id="6fd17-161">If you navigate back toohello dashboard, you can verify hello device is still sending telemetry following hello firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="6fd17-162">Se si lascia in esecuzione nell'account di Azure di soluzione di monitoraggio remoto hello, verrà addebitato per volta hello che è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6fd17-162">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="6fd17-163">Per ulteriori informazioni sulla riduzione del consumo durante l'esecuzione di soluzioni di monitoraggio remoto hello, vedere [configurazione Azure IoT Suite preconfigurato soluzioni per scopi dimostrativi][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="6fd17-163">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="6fd17-164">Eliminare la soluzione hello preconfigurato dall'account di Azure al termine dell'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="6fd17-164">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6fd17-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6fd17-165">Next steps</span></span>

<span data-ttu-id="6fd17-166">Visitare hello [Centro per sviluppatori Azure IoT](https://azure.microsoft.com/develop/iot/) per ulteriori esempi e documentazione su Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="6fd17-166">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md