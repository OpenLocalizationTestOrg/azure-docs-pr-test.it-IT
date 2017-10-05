---
title: Connettere Raspberry Pi ad Azure IoT Suite usando Node.js con telemetria simulata | Microsoft Docs
description: Usare lo Starter Kit di Microsoft Azure IoT per Raspberry Pi 3 e Azure IoT Suite. Usare Node.js per la connessione di Raspberry Pi alla soluzione di monitoraggio remoto, per inviare dati di telemetria simulata al cloud e per rispondere ai metodi richiamati dal dashboard della soluzione.
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
ms.openlocfilehash: 43fbfe2f2c5fb86e496c4419f9565365cf89830a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-simulated-telemetry-using-nodejs"></a><span data-ttu-id="8a22d-104">Connettere Raspberry Pi 3 alla soluzione di monitoraggio remoto e inviare la telemetria simulata usando Node.js</span><span class="sxs-lookup"><span data-stu-id="8a22d-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send simulated telemetry using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="8a22d-105">Questa esercitazione illustra come usare Raspberry Pi 3 per simulare i dati relativi alla temperatura e all'umidità dati da inviare al cloud.</span><span class="sxs-lookup"><span data-stu-id="8a22d-105">This tutorial shows you how to use the Raspberry Pi 3 to simulate temperature and humidity data to send to the cloud.</span></span> <span data-ttu-id="8a22d-106">L'esercitazione usa:</span><span class="sxs-lookup"><span data-stu-id="8a22d-106">The tutorial uses:</span></span>

- <span data-ttu-id="8a22d-107">Il sistema operativo Raspbian, il linguaggio di programmazione Node.js e Microsoft Azure IoT SDK per Node.js per implementare un dispositivo di esempio.</span><span class="sxs-lookup"><span data-stu-id="8a22d-107">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span></span>
- <span data-ttu-id="8a22d-108">La soluzione preconfigurata di monitoraggio remoto IoT Suite come back-end basato su cloud.</span><span class="sxs-lookup"><span data-stu-id="8a22d-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="8a22d-109">La soluzione di monitoraggio remoto esegue il provisioning di un set di servizi di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8a22d-109">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="8a22d-110">La distribuzione riflette un'architettura enterprise reale.</span><span class="sxs-lookup"><span data-stu-id="8a22d-110">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="8a22d-111">Per evitare costi di consumo di Azure non necessari, eliminare l'istanza della soluzione preconfigurata in azureiotsuite.com al completamento.</span><span class="sxs-lookup"><span data-stu-id="8a22d-111">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="8a22d-112">Se la soluzione preconfigurata occorre nuovamente, è possibile ricrearla facilmente.</span><span class="sxs-lookup"><span data-stu-id="8a22d-112">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="8a22d-113">Per altre informazioni sulla riduzione del consumo durante l'esecuzione della soluzione di monitoraggio remoto, vedere [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configurazione di soluzioni preconfigurate di Azure IoT Suite per scopi dimostrativi).</span><span class="sxs-lookup"><span data-stu-id="8a22d-113">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="8a22d-114">Scaricare e configurare l'esempio</span><span class="sxs-lookup"><span data-stu-id="8a22d-114">Download and configure the sample</span></span>

<span data-ttu-id="8a22d-115">È ora possibile scaricare e configurare l'applicazione client di monitoraggio remoto su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="8a22d-115">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="8a22d-116">Installare Node.js</span><span class="sxs-lookup"><span data-stu-id="8a22d-116">Install Node.js</span></span>

<span data-ttu-id="8a22d-117">Se non è già stato fatto, installare Node.js in Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="8a22d-117">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="8a22d-118">IoT SDK per Node.js richiede la versione 0.11.5 o successiva di Node.js.</span><span class="sxs-lookup"><span data-stu-id="8a22d-118">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="8a22d-119">I passaggi seguenti mostrano come installare Node.js v6.10.2 su Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="8a22d-119">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="8a22d-120">Usare il comando seguente per aggiornare Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="8a22d-120">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="8a22d-121">Usare il comando seguente per scaricare i file binari di Node.js su Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="8a22d-121">Use the following command to download the Node.js binaries to your Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="8a22d-122">Usare il comando seguente per installare i file binari:</span><span class="sxs-lookup"><span data-stu-id="8a22d-122">Use the following command to install the binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="8a22d-123">Usare il comando seguente per verificare di aver installato correttamente Node.js v6.10.2:</span><span class="sxs-lookup"><span data-stu-id="8a22d-123">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a><span data-ttu-id="8a22d-124">Clonare i repository</span><span class="sxs-lookup"><span data-stu-id="8a22d-124">Clone the repositories</span></span>

<span data-ttu-id="8a22d-125">Se non è già stato fatto, clonare i repository necessari eseguendo i comandi seguenti in un terminale in Pi:</span><span class="sxs-lookup"><span data-stu-id="8a22d-125">If you haven't already done so, clone the required repositories by running the following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="8a22d-126">Aggiornare la stringa di connessione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="8a22d-126">Update the device connection string</span></span>

<span data-ttu-id="8a22d-127">Aprire il file origine di esempio nell'editor **nano** usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8a22d-127">Open the sample source file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="8a22d-128">Trovare la riga:</span><span class="sxs-lookup"><span data-stu-id="8a22d-128">Find the line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="8a22d-129">Sostituire i valori segnaposto con il dispositivo e le informazioni dell'hub IoT creati e salvati all'inizio di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="8a22d-129">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="8a22d-130">Salvare le modifiche (**Ctrl+O**, **INVIO**) e chiudere l'editor (**Ctrl+X**).</span><span class="sxs-lookup"><span data-stu-id="8a22d-130">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="8a22d-131">Eseguire l'esempio</span><span class="sxs-lookup"><span data-stu-id="8a22d-131">Run the sample</span></span>

<span data-ttu-id="8a22d-132">Eseguire i comandi seguenti per installare i pacchetti prerequisiti per l'esempio:</span><span class="sxs-lookup"><span data-stu-id="8a22d-132">Run the following commands to install the prerequisite packages for the sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator
npm install
```

<span data-ttu-id="8a22d-133">È ora possibile eseguire il programma di esempio su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="8a22d-133">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="8a22d-134">Immettere il comando:</span><span class="sxs-lookup"><span data-stu-id="8a22d-134">Enter the command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="8a22d-135">L'output seguente riporta un esempio dell'output visualizzato al prompt dei comandi su Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="8a22d-135">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Output dell'app Raspberry Pi][img-raspberry-output]

<span data-ttu-id="8a22d-137">Premere **CTRL-C** per uscire dal programma in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="8a22d-137">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="8a22d-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8a22d-138">Next steps</span></span>

<span data-ttu-id="8a22d-139">Visitare il [Centro per sviluppatori Azure IoT](https://azure.microsoft.com/develop/iot/) per altri esempi e documentazione su Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="8a22d-139">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-simulator/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
