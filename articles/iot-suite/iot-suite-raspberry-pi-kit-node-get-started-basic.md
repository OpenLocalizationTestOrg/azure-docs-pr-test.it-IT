---
title: aaaConnect un tooAzure Raspberry Pi IoT Suite con Node.js sensori reali | Documenti Microsoft
description: Utilizzare hello Starter Kit di Microsoft Azure IoT per hello Raspberry Pi 3 e Azure IoT Suite. Usare Node.js tooconnect toohello le Pi Raspberry soluzione di monitoraggio remoto, inviare i dati di telemetria da sensori toohello cloud e rispondere toomethods richiamato dal dashboard di soluzione hello.
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
ms.openlocfilehash: 7ffb4a7a8c04b424a1f29170f4739d89f39a2429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-nodejs"></a><span data-ttu-id="726eb-104">Connettere il toohello Raspberry Pi 3 soluzione di monitoraggio remoto e inviare dati di telemetria da un sensore reale con Node.js</span><span class="sxs-lookup"><span data-stu-id="726eb-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send telemetry from a real sensor using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="726eb-105">Questa esercitazione viene illustrato come toouse hello IoT Starter Kit di Microsoft Azure per 3 Pi Raspberry toodevelop un lettore di temperatura e umidità in grado di comunicare con il cloud hello.</span><span class="sxs-lookup"><span data-stu-id="726eb-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 toodevelop a temperature and humidity reader that can communicate with hello cloud.</span></span> <span data-ttu-id="726eb-106">esercitazione Hello utilizza:</span><span class="sxs-lookup"><span data-stu-id="726eb-106">hello tutorial uses:</span></span>

- <span data-ttu-id="726eb-107">Sistema operativo Raspbian, hello Node.js linguaggio di programmazione e hello Microsoft Azure IoT SDK per Node.js tooimplement un dispositivo di esempio.</span><span class="sxs-lookup"><span data-stu-id="726eb-107">Raspbian OS, hello Node.js programming language, and hello Microsoft Azure IoT SDK for Node.js tooimplement a sample device.</span></span>
- <span data-ttu-id="726eb-108">monitoraggio remoto IoT Suite Hello preconfigurato soluzione come hello basato su cloud back-end.</span><span class="sxs-lookup"><span data-stu-id="726eb-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="726eb-109">Panoramica</span><span class="sxs-lookup"><span data-stu-id="726eb-109">Overview</span></span>

<span data-ttu-id="726eb-110">In questa esercitazione è completare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="726eb-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="726eb-111">Distribuire un'istanza di hello remoto monitoraggio soluzione preconfigurata tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="726eb-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="726eb-112">Questo passaggio distribuisce e configura automaticamente più servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="726eb-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="726eb-113">Consente di impostare il dispositivo e sensori di toocommunicate con il computer e hello soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="726eb-113">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="726eb-114">Aggiornare hello esempio dispositivo codice tooconnect toohello soluzione di monitoraggio remoto e inviare dati di telemetria che è possibile visualizzare nel dashboard di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="726eb-114">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="726eb-115">Hello remoto disposizioni soluzione monitoraggio di un set di servizi di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="726eb-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="726eb-116">distribuzione di Hello riflette un'architettura aziendale reale.</span><span class="sxs-lookup"><span data-stu-id="726eb-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="726eb-117">tooavoid addebiti di consumo di Azure, eliminare l'istanza di soluzione hello preconfigurato azureiotsuite.com dopo aver con esso.</span><span class="sxs-lookup"><span data-stu-id="726eb-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="726eb-118">Se è necessario hello nuovamente la soluzione preconfigurata, è possibile ricrearla facilmente.</span><span class="sxs-lookup"><span data-stu-id="726eb-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="726eb-119">Per ulteriori informazioni sulla riduzione del consumo durante l'esecuzione di soluzioni di monitoraggio remoto hello, vedere [configurazione Azure IoT Suite preconfigurato soluzioni per scopi dimostrativi][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="726eb-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="726eb-120">Scaricare e configurare l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="726eb-120">Download and configure hello sample</span></span>

<span data-ttu-id="726eb-121">È ora possibile scaricare e configurare l'applicazione client per il monitoraggio remoto di hello nelle Pi Raspberry.</span><span class="sxs-lookup"><span data-stu-id="726eb-121">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="726eb-122">Installare Node.js</span><span class="sxs-lookup"><span data-stu-id="726eb-122">Install Node.js</span></span>

<span data-ttu-id="726eb-123">Installare Node. js nel Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="726eb-123">Install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="726eb-124">Hello IoT SDK per Node.js richiede la versione 0.11.5 di Node.js o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="726eb-124">hello IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="726eb-125">Hello passaggi seguenti viene illustrato come tooinstall Node.js v6.10.2 sulle Pi Raspberry:</span><span class="sxs-lookup"><span data-stu-id="726eb-125">hello following steps show you how tooinstall Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="726eb-126">Utilizzare hello comando che segue tooupdate le Pi Raspberry:</span><span class="sxs-lookup"><span data-stu-id="726eb-126">Use hello following command tooupdate your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="726eb-127">Utilizzare hello comando toodownload hello Node.js i file binari tooyour Pi Raspberry seguenti:</span><span class="sxs-lookup"><span data-stu-id="726eb-127">Use hello following command toodownload hello Node.js binaries tooyour Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="726eb-128">Utilizzare hello file binari di hello tooinstall di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="726eb-128">Use hello following command tooinstall hello binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="726eb-129">Utilizzare hello tooverify comando è stato installato correttamente Node.js v6.10.2 seguente:</span><span class="sxs-lookup"><span data-stu-id="726eb-129">Use hello following command tooverify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a><span data-ttu-id="726eb-130">Clonare il repository hello</span><span class="sxs-lookup"><span data-stu-id="726eb-130">Clone hello repositories</span></span>

<span data-ttu-id="726eb-131">Se non già stato fatto, hello clone richiesto repository eseguendo hello seguendo i comandi del Pi:</span><span class="sxs-lookup"><span data-stu-id="726eb-131">If you haven't already done so, clone hello required repositories by running hello following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git`
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="726eb-132">Aggiornare la stringa di connessione dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="726eb-132">Update hello device connection string</span></span>

<span data-ttu-id="726eb-133">File di origine di esempio hello Open in hello **nano** editor utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="726eb-133">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="726eb-134">Individuare la riga hello:</span><span class="sxs-lookup"><span data-stu-id="726eb-134">Find hello line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="726eb-135">Sostituire i valori segnaposto hello con dispositivo hello e informazioni di IoT Hub è stato creato e salvato all'inizio di hello di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="726eb-135">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="726eb-136">Salvare le modifiche (**Ctrl O**, **invio**) e uscire dall'editor hello (**Ctrl + X**).</span><span class="sxs-lookup"><span data-stu-id="726eb-136">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="run-hello-sample"></a><span data-ttu-id="726eb-137">Eseguire l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="726eb-137">Run hello sample</span></span>

<span data-ttu-id="726eb-138">La seguente esecuzione hello comandi tooinstall hello i pacchetti dei prerequisiti per l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="726eb-138">Run hello following commands tooinstall hello prerequisite packages for hello sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic
npm install
```

<span data-ttu-id="726eb-139">È ora possibile eseguire il programma di esempio hello in hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="726eb-139">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="726eb-140">Immettere il comando hello:</span><span class="sxs-lookup"><span data-stu-id="726eb-140">Enter hello command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="726eb-141">Hello riportato di seguito è riportato un esempio di output di hello visualizzato al prompt dei comandi di hello in hello Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="726eb-141">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Output dell'app Raspberry Pi][img-raspberry-output]

<span data-ttu-id="726eb-143">Premere **Ctrl-C** programma hello tooexit in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="726eb-143">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="726eb-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="726eb-144">Next steps</span></span>

<span data-ttu-id="726eb-145">Visitare hello [Centro per sviluppatori Azure IoT](https://azure.microsoft.com/develop/iot/) per ulteriori esempi e documentazione su Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="726eb-145">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-basic/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
