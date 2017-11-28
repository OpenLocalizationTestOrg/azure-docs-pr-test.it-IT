---
title: Connettere Raspberry Pi ad Azure IoT Suite usando Node.js con sensori reali | Microsoft Docs
description: Usare lo Starter Kit di Microsoft Azure IoT per Raspberry Pi 3 e Azure IoT Suite. Usare Node.js per la connessione di Raspberry Pi alla soluzione di monitoraggio remoto, inviare dati di telemetria simulata al cloud e rispondere ai metodi richiamati dal dashboard della soluzione.
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
ms.openlocfilehash: 91546157cc8eabf68706391ce706038d8dc5f82d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-nodejs"></a><span data-ttu-id="85401-104">Connettere Raspberry Pi 3 alla soluzione di monitoraggio remoto e inviare la telemetria da un sensore reale usando Node.js</span><span class="sxs-lookup"><span data-stu-id="85401-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send telemetry from a real sensor using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="85401-105">Questa esercitazione illustra come usare lo Starter Kit di Microsoft Azure IoT per Raspberry Pi 3 per sviluppare un lettore di temperatura e di umidità in grado di comunicare con il cloud.</span><span class="sxs-lookup"><span data-stu-id="85401-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to develop a temperature and humidity reader that can communicate with the cloud.</span></span> <span data-ttu-id="85401-106">L'esercitazione usa:</span><span class="sxs-lookup"><span data-stu-id="85401-106">The tutorial uses:</span></span>

- <span data-ttu-id="85401-107">Il sistema operativo Raspbian, il linguaggio di programmazione Node.js e Microsoft Azure IoT SDK per Node.js per implementare un dispositivo di esempio.</span><span class="sxs-lookup"><span data-stu-id="85401-107">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span></span>
- <span data-ttu-id="85401-108">La soluzione preconfigurata di monitoraggio remoto IoT Suite come back-end basato su cloud.</span><span class="sxs-lookup"><span data-stu-id="85401-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="85401-109">Panoramica</span><span class="sxs-lookup"><span data-stu-id="85401-109">Overview</span></span>

<span data-ttu-id="85401-110">In questa esercitazione si completa la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="85401-110">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="85401-111">Distribuire un'istanza della soluzione preconfigurata di monitoraggio remoto nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="85401-111">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="85401-112">Questo passaggio distribuisce e configura automaticamente più servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="85401-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="85401-113">Configurare il dispositivo e i sensori per la comunicazione con il computer e la soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="85401-113">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="85401-114">Aggiornare il codice del dispositivo di esempio per eseguire la connessione alla soluzione di monitoraggio remoto e inviare i dati di telemetria che è possibile visualizzare nel dashboard della soluzione.</span><span class="sxs-lookup"><span data-stu-id="85401-114">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="85401-115">La soluzione di monitoraggio remoto esegue il provisioning di un set di servizi di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="85401-115">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="85401-116">La distribuzione riflette un'architettura enterprise reale.</span><span class="sxs-lookup"><span data-stu-id="85401-116">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="85401-117">Per evitare costi di consumo di Azure non necessari, eliminare l'istanza della soluzione preconfigurata in azureiotsuite.com al completamento.</span><span class="sxs-lookup"><span data-stu-id="85401-117">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="85401-118">Se la soluzione preconfigurata occorre nuovamente, è possibile ricrearla facilmente.</span><span class="sxs-lookup"><span data-stu-id="85401-118">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="85401-119">Per altre informazioni sulla riduzione del consumo durante l'esecuzione della soluzione di monitoraggio remoto, vedere [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configurazione di soluzioni preconfigurate di Azure IoT Suite per scopi dimostrativi).</span><span class="sxs-lookup"><span data-stu-id="85401-119">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="85401-120">Scaricare e configurare l'esempio</span><span class="sxs-lookup"><span data-stu-id="85401-120">Download and configure the sample</span></span>

<span data-ttu-id="85401-121">È ora possibile scaricare e configurare l'applicazione client di monitoraggio remoto su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="85401-121">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="85401-122">Installare Node.js</span><span class="sxs-lookup"><span data-stu-id="85401-122">Install Node.js</span></span>

<span data-ttu-id="85401-123">Installare Node. js nel Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="85401-123">Install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="85401-124">IoT SDK per Node.js richiede la versione 0.11.5 o successiva di Node.js.</span><span class="sxs-lookup"><span data-stu-id="85401-124">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="85401-125">I passaggi seguenti mostrano come installare Node.js v6.10.2 su Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="85401-125">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="85401-126">Usare il comando seguente per aggiornare Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="85401-126">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="85401-127">Usare il comando seguente per scaricare i file binari di Node.js su Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="85401-127">Use the following command to download the Node.js binaries to your Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="85401-128">Usare il comando seguente per installare i file binari:</span><span class="sxs-lookup"><span data-stu-id="85401-128">Use the following command to install the binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="85401-129">Usare il comando seguente per verificare di aver installato correttamente Node.js v6.10.2:</span><span class="sxs-lookup"><span data-stu-id="85401-129">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a><span data-ttu-id="85401-130">Clonare i repository</span><span class="sxs-lookup"><span data-stu-id="85401-130">Clone the repositories</span></span>

<span data-ttu-id="85401-131">Se non è già stato fatto, clonare i repository necessari eseguendo i comandi seguenti nel Pi:</span><span class="sxs-lookup"><span data-stu-id="85401-131">If you haven't already done so, clone the required repositories by running the following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git`
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="85401-132">Aggiornare la stringa di connessione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="85401-132">Update the device connection string</span></span>

<span data-ttu-id="85401-133">Aprire il file origine di esempio nell'editor **nano** usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="85401-133">Open the sample source file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="85401-134">Trovare la riga:</span><span class="sxs-lookup"><span data-stu-id="85401-134">Find the line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="85401-135">Sostituire i valori segnaposto con il dispositivo e le informazioni dell'hub IoT creati e salvati all'inizio di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="85401-135">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="85401-136">Salvare le modifiche (**Ctrl+O**, **INVIO**) e chiudere l'editor (**Ctrl+X**).</span><span class="sxs-lookup"><span data-stu-id="85401-136">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="85401-137">Eseguire l'esempio</span><span class="sxs-lookup"><span data-stu-id="85401-137">Run the sample</span></span>

<span data-ttu-id="85401-138">Eseguire i comandi seguenti per installare i pacchetti prerequisiti per l'esempio:</span><span class="sxs-lookup"><span data-stu-id="85401-138">Run the following commands to install the prerequisite packages for the sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic
npm install
```

<span data-ttu-id="85401-139">È ora possibile eseguire il programma di esempio su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="85401-139">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="85401-140">Immettere il comando:</span><span class="sxs-lookup"><span data-stu-id="85401-140">Enter the command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="85401-141">L'output seguente riporta un esempio dell'output visualizzato al prompt dei comandi su Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="85401-141">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Output dell'app Raspberry Pi][img-raspberry-output]

<span data-ttu-id="85401-143">Premere **CTRL-C** per uscire dal programma in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="85401-143">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="85401-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="85401-144">Next steps</span></span>

<span data-ttu-id="85401-145">Visitare il [Centro per sviluppatori Azure IoT](https://azure.microsoft.com/develop/iot/) per altri esempi e documentazione su Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="85401-145">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-basic/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
