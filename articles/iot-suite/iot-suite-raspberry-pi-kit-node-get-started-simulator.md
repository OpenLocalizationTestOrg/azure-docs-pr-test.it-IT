---
title: aaaConnect un tooAzure Raspberry Pi IoT Suite con Node.js simulato telemetria | Documenti Microsoft
description: Utilizzare hello Starter Kit di Microsoft Azure IoT per hello Raspberry Pi 3 e Azure IoT Suite. Usare Node.js tooconnect toohello le Pi Raspberry soluzione di monitoraggio remoto, inviare i dati di telemetria simulato toohello cloud e rispondere toomethods richiamato dal dashboard di soluzione hello.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: node.js
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: f65eeaa6e83fd89cdedae8fa8386a3e9ef8417d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-simulated-telemetry-using-nodejs"></a><span data-ttu-id="a1965-104">Connettere il toohello Raspberry Pi 3 soluzione di monitoraggio remoto e inviare la telemetria simulato con Node.js</span><span class="sxs-lookup"><span data-stu-id="a1965-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send simulated telemetry using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="a1965-105">Questa esercitazione viene illustrato come toouse hello Raspberry Pi 3 toosimulate temperatura e umidità dati toosend toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="a1965-105">This tutorial shows you how toouse hello Raspberry Pi 3 toosimulate temperature and humidity data toosend toohello cloud.</span></span> <span data-ttu-id="a1965-106">esercitazione Hello utilizza:</span><span class="sxs-lookup"><span data-stu-id="a1965-106">hello tutorial uses:</span></span>

- <span data-ttu-id="a1965-107">Sistema operativo Raspbian, hello Node.js linguaggio di programmazione e hello Microsoft Azure IoT SDK per Node.js tooimplement un dispositivo di esempio.</span><span class="sxs-lookup"><span data-stu-id="a1965-107">Raspbian OS, hello Node.js programming language, and hello Microsoft Azure IoT SDK for Node.js tooimplement a sample device.</span></span>
- <span data-ttu-id="a1965-108">monitoraggio remoto IoT Suite Hello preconfigurato soluzione come hello basato su cloud back-end.</span><span class="sxs-lookup"><span data-stu-id="a1965-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="a1965-109">Hello remoto disposizioni soluzione monitoraggio di un set di servizi di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a1965-109">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="a1965-110">distribuzione di Hello riflette un'architettura aziendale reale.</span><span class="sxs-lookup"><span data-stu-id="a1965-110">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="a1965-111">tooavoid addebiti di consumo di Azure, eliminare l'istanza di soluzione hello preconfigurato azureiotsuite.com dopo aver con esso.</span><span class="sxs-lookup"><span data-stu-id="a1965-111">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="a1965-112">Se è necessario hello nuovamente la soluzione preconfigurata, è possibile ricrearla facilmente.</span><span class="sxs-lookup"><span data-stu-id="a1965-112">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="a1965-113">Per ulteriori informazioni sulla riduzione del consumo durante l'esecuzione di soluzioni di monitoraggio remoto hello, vedere [configurazione Azure IoT Suite preconfigurato soluzioni per scopi dimostrativi][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="a1965-113">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="a1965-114">Scaricare e configurare l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="a1965-114">Download and configure hello sample</span></span>

<span data-ttu-id="a1965-115">È ora possibile scaricare e configurare l'applicazione client per il monitoraggio remoto di hello nelle Pi Raspberry.</span><span class="sxs-lookup"><span data-stu-id="a1965-115">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="a1965-116">Installare Node.js</span><span class="sxs-lookup"><span data-stu-id="a1965-116">Install Node.js</span></span>

<span data-ttu-id="a1965-117">Se non è già stato fatto, installare Node.js in Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="a1965-117">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="a1965-118">Hello IoT SDK per Node.js richiede la versione 0.11.5 di Node.js o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="a1965-118">hello IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="a1965-119">Hello passaggi seguenti viene illustrato come tooinstall Node.js v6.10.2 sulle Pi Raspberry:</span><span class="sxs-lookup"><span data-stu-id="a1965-119">hello following steps show you how tooinstall Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="a1965-120">Utilizzare hello comando che segue tooupdate le Pi Raspberry:</span><span class="sxs-lookup"><span data-stu-id="a1965-120">Use hello following command tooupdate your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="a1965-121">Utilizzare hello comando toodownload hello Node.js i file binari tooyour Pi Raspberry seguenti:</span><span class="sxs-lookup"><span data-stu-id="a1965-121">Use hello following command toodownload hello Node.js binaries tooyour Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="a1965-122">Utilizzare hello file binari di hello tooinstall di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a1965-122">Use hello following command tooinstall hello binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="a1965-123">Utilizzare hello tooverify comando è stato installato correttamente Node.js v6.10.2 seguente:</span><span class="sxs-lookup"><span data-stu-id="a1965-123">Use hello following command tooverify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a><span data-ttu-id="a1965-124">Clonare il repository hello</span><span class="sxs-lookup"><span data-stu-id="a1965-124">Clone hello repositories</span></span>

<span data-ttu-id="a1965-125">Se non già stato fatto, hello clone richiesto repository eseguendo hello seguendo i comandi di un terminale il Pi:</span><span class="sxs-lookup"><span data-stu-id="a1965-125">If you haven't already done so, clone hello required repositories by running hello following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="a1965-126">Aggiornare la stringa di connessione dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="a1965-126">Update hello device connection string</span></span>

<span data-ttu-id="a1965-127">File di origine di esempio hello Open in hello **nano** editor utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a1965-127">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="a1965-128">Individuare la riga hello:</span><span class="sxs-lookup"><span data-stu-id="a1965-128">Find hello line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="a1965-129">Sostituire i valori segnaposto hello con dispositivo hello e informazioni di IoT Hub è stato creato e salvato all'inizio di hello di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a1965-129">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="a1965-130">Salvare le modifiche (**Ctrl O**, **invio**) e uscire dall'editor hello (**Ctrl + X**).</span><span class="sxs-lookup"><span data-stu-id="a1965-130">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="run-hello-sample"></a><span data-ttu-id="a1965-131">Eseguire l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="a1965-131">Run hello sample</span></span>

<span data-ttu-id="a1965-132">La seguente esecuzione hello comandi tooinstall hello i pacchetti dei prerequisiti per l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="a1965-132">Run hello following commands tooinstall hello prerequisite packages for hello sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator
npm install
```

<span data-ttu-id="a1965-133">È ora possibile eseguire il programma di esempio hello in hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="a1965-133">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="a1965-134">Immettere il comando hello:</span><span class="sxs-lookup"><span data-stu-id="a1965-134">Enter hello command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="a1965-135">Hello riportato di seguito è riportato un esempio di output di hello visualizzato al prompt dei comandi di hello in hello Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="a1965-135">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Output dell'app Raspberry Pi][img-raspberry-output]

<span data-ttu-id="a1965-137">Premere **Ctrl-C** programma hello tooexit in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="a1965-137">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="a1965-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a1965-138">Next steps</span></span>

<span data-ttu-id="a1965-139">Visitare hello [Centro per sviluppatori Azure IoT](https://azure.microsoft.com/develop/iot/) per ulteriori esempi e documentazione su Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="a1965-139">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-simulator/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
