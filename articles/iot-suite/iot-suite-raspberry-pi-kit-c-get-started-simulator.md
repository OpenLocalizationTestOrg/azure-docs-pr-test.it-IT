---
title: Connect a Raspberry Pi to Azure IoT Suite using C with simulated telemetry (Connettere Raspberry Pi ad Azure IoT Suite usando C con telemetria simulata) | Documentazione Microsoft
description: Usare lo Starter Kit di Microsoft Azure IoT per Raspberry Pi 3 e Azure IoT Suite. Usare C per la connessione di Raspberry Pi alla soluzione di monitoraggio remoto, per inviare dati di telemetria simulata al cloud e per rispondere ai metodi richiamati dal dashboard della soluzione.
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
ms.openlocfilehash: 43b82e5fb6a309283979f23d8c87af600595bc55
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-simulated-telemetry-using-c"></a><span data-ttu-id="f683d-104">Connettere Raspberry Pi 3 alla soluzione di monitoraggio remoto e inviare la telemetria simulata usando C</span><span class="sxs-lookup"><span data-stu-id="f683d-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send simulated telemetry using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="f683d-105">Questa esercitazione illustra come usare Raspberry Pi 3 per simulare i dati relativi alla temperatura e all'umidità da inviare al cloud.</span><span class="sxs-lookup"><span data-stu-id="f683d-105">This tutorial shows you how to use the Raspberry Pi 3 to simulate temperature and humidity data to send to the cloud.</span></span> <span data-ttu-id="f683d-106">L'esercitazione usa:</span><span class="sxs-lookup"><span data-stu-id="f683d-106">The tutorial uses:</span></span>

- <span data-ttu-id="f683d-107">Il sistema operativo Raspbian, il linguaggio di programmazione C e Microsoft Azure IoT SDK per C per implementare un dispositivo di esempio.</span><span class="sxs-lookup"><span data-stu-id="f683d-107">Raspbian OS, the C programming language, and the Microsoft Azure IoT SDK for C to implement a sample device.</span></span>
- <span data-ttu-id="f683d-108">La soluzione preconfigurata di monitoraggio remoto IoT Suite come back-end basato su cloud.</span><span class="sxs-lookup"><span data-stu-id="f683d-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="f683d-109">La soluzione di monitoraggio remoto esegue il provisioning di un set di servizi di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f683d-109">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="f683d-110">La distribuzione riflette un'architettura enterprise reale.</span><span class="sxs-lookup"><span data-stu-id="f683d-110">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="f683d-111">Per evitare costi di consumo di Azure non necessari, eliminare l'istanza della soluzione preconfigurata in azureiotsuite.com al completamento.</span><span class="sxs-lookup"><span data-stu-id="f683d-111">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="f683d-112">Se la soluzione preconfigurata occorre nuovamente, è possibile ricrearla facilmente.</span><span class="sxs-lookup"><span data-stu-id="f683d-112">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="f683d-113">Per altre informazioni sulla riduzione del consumo durante l'esecuzione della soluzione di monitoraggio remoto, vedere [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configurazione di soluzioni preconfigurate di Azure IoT Suite per scopi dimostrativi).</span><span class="sxs-lookup"><span data-stu-id="f683d-113">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="f683d-114">Scaricare e configurare l'esempio</span><span class="sxs-lookup"><span data-stu-id="f683d-114">Download and configure the sample</span></span>

<span data-ttu-id="f683d-115">È ora possibile scaricare e configurare l'applicazione client di monitoraggio remoto su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="f683d-115">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-the-repositories"></a><span data-ttu-id="f683d-116">Clonare i repository</span><span class="sxs-lookup"><span data-stu-id="f683d-116">Clone the repositories</span></span>

<span data-ttu-id="f683d-117">Se non è già stato fatto, clonare i repository necessari eseguendo i comandi seguenti in un terminale in Pi:</span><span class="sxs-lookup"><span data-stu-id="f683d-117">If you haven't already done so, clone the required repositories by running the following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="f683d-118">Aggiornare la stringa di connessione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="f683d-118">Update the device connection string</span></span>

<span data-ttu-id="f683d-119">Aprire il file origine di esempio nell'editor **nano** usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f683d-119">Open the sample source file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="f683d-120">Individuare le righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="f683d-120">Locate the following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="f683d-121">Sostituire i valori segnaposto con il dispositivo e le informazioni dell'hub IoT creati e salvati all'inizio di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f683d-121">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="f683d-122">Salvare le modifiche (**CTRL+O**, **INVIO**) e chiudere l'editor (**CTRL+X**).</span><span class="sxs-lookup"><span data-stu-id="f683d-122">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="build-the-sample"></a><span data-ttu-id="f683d-123">Compilare l'esempio</span><span class="sxs-lookup"><span data-stu-id="f683d-123">Build the sample</span></span>

<span data-ttu-id="f683d-124">Installare i pacchetti di prerequisiti per Microsoft Azure IoT SDK per dispositivi di Microsoft per C eseguendo i comandi seguenti in un terminale di Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="f683d-124">Install the prerequisite packages for the Microsoft Azure IoT Device SDK for C by running the following commands in a terminal on the Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="f683d-125">È ora possibile compilare la soluzione di esempio aggiornata su Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="f683d-125">You can now build the updated sample solution on the Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
```

<span data-ttu-id="f683d-126">È ora possibile eseguire il programma di esempio su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="f683d-126">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="f683d-127">Immettere il comando:</span><span class="sxs-lookup"><span data-stu-id="f683d-127">Enter the command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="f683d-128">L'output seguente riporta un esempio dell'output visualizzato al prompt dei comandi su Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="f683d-128">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Output dell'app Raspberry Pi][img-raspberry-output]

<span data-ttu-id="f683d-130">Premere **CTRL-C** per uscire dal programma in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="f683d-130">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="f683d-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f683d-131">Next steps</span></span>

<span data-ttu-id="f683d-132">Visitare il [Centro per sviluppatori Azure IoT](https://azure.microsoft.com/develop/iot/) per altri esempi e documentazione su Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="f683d-132">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-simulator/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
