---
title: Connettere Raspberry Pi ad Azure IoT Suite con sensori reali C | Microsoft Docs
description: Usare lo Starter Kit di Microsoft Azure IoT per Raspberry Pi 3 e Azure IoT Suite. Usare C per la connessione di Raspberry Pi alla soluzione di monitoraggio remoto, inviare dati di telemetria simulata al cloud e rispondere ai metodi richiamati dal dashboard della soluzione.
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
ms.openlocfilehash: 418108e8236518d2671abca0f06f1ae8159d6442
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-c"></a><span data-ttu-id="f5062-104">Connettere Raspberry Pi 3 alla soluzione di monitoraggio remoto e inviare la telemetria da un sensore reale usando C</span><span class="sxs-lookup"><span data-stu-id="f5062-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send telemetry from a real sensor using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="f5062-105">Questa esercitazione illustra come usare lo Starter Kit di Microsoft Azure IoT per Raspberry Pi 3 per sviluppare un lettore di temperatura e di umidità in grado di comunicare con il cloud.</span><span class="sxs-lookup"><span data-stu-id="f5062-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to develop a temperature and humidity reader that can communicate with the cloud.</span></span> <span data-ttu-id="f5062-106">L'esercitazione usa:</span><span class="sxs-lookup"><span data-stu-id="f5062-106">The tutorial uses:</span></span>

- <span data-ttu-id="f5062-107">Il sistema operativo Raspbian, il linguaggio di programmazione C e Microsoft Azure IoT SDK per C per implementare un dispositivo di esempio.</span><span class="sxs-lookup"><span data-stu-id="f5062-107">Raspbian OS, the C programming language, and the Microsoft Azure IoT SDK for C to implement a sample device.</span></span>
- <span data-ttu-id="f5062-108">La soluzione preconfigurata di monitoraggio remoto IoT Suite come back-end basato su cloud.</span><span class="sxs-lookup"><span data-stu-id="f5062-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="f5062-109">Panoramica</span><span class="sxs-lookup"><span data-stu-id="f5062-109">Overview</span></span>

<span data-ttu-id="f5062-110">In questa esercitazione si completa la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f5062-110">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="f5062-111">Distribuire un'istanza della soluzione preconfigurata di monitoraggio remoto nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5062-111">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="f5062-112">Questo passaggio distribuisce e configura automaticamente più servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5062-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="f5062-113">Configurare il dispositivo e i sensori per la comunicazione con il computer e la soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="f5062-113">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="f5062-114">Aggiornare il codice del dispositivo di esempio per eseguire la connessione alla soluzione di monitoraggio remoto e inviare i dati di telemetria che è possibile visualizzare nel dashboard della soluzione.</span><span class="sxs-lookup"><span data-stu-id="f5062-114">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="f5062-115">La soluzione di monitoraggio remoto esegue il provisioning di un set di servizi di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5062-115">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="f5062-116">La distribuzione riflette un'architettura enterprise reale.</span><span class="sxs-lookup"><span data-stu-id="f5062-116">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="f5062-117">Per evitare costi di consumo di Azure non necessari, eliminare l'istanza della soluzione preconfigurata in azureiotsuite.com al completamento.</span><span class="sxs-lookup"><span data-stu-id="f5062-117">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="f5062-118">Se la soluzione preconfigurata occorre nuovamente, è possibile ricrearla facilmente.</span><span class="sxs-lookup"><span data-stu-id="f5062-118">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="f5062-119">Per altre informazioni sulla riduzione del consumo durante l'esecuzione della soluzione di monitoraggio remoto, vedere [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configurazione di soluzioni preconfigurate di Azure IoT Suite per scopi dimostrativi).</span><span class="sxs-lookup"><span data-stu-id="f5062-119">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="f5062-120">Scaricare e configurare l'esempio</span><span class="sxs-lookup"><span data-stu-id="f5062-120">Download and configure the sample</span></span>

<span data-ttu-id="f5062-121">È ora possibile scaricare e configurare l'applicazione client di monitoraggio remoto su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="f5062-121">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-the-repositories"></a><span data-ttu-id="f5062-122">Clonare i repository</span><span class="sxs-lookup"><span data-stu-id="f5062-122">Clone the repositories</span></span>

<span data-ttu-id="f5062-123">Se non è già stato fatto, clonare i repository necessari eseguendo i comandi seguenti in un terminale in Pi:</span><span class="sxs-lookup"><span data-stu-id="f5062-123">If you haven't already done so, clone the required repositories by running the following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
git clone --recursive https://github.com/WiringPi/WiringPi.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="f5062-124">Aggiornare la stringa di connessione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="f5062-124">Update the device connection string</span></span>

<span data-ttu-id="f5062-125">Aprire il file origine di esempio nell'editor **nano** usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f5062-125">Open the sample source file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="f5062-126">Individuare le righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5062-126">Locate the following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="f5062-127">Sostituire i valori segnaposto con il dispositivo e le informazioni dell'hub IoT creati e salvati all'inizio di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f5062-127">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="f5062-128">Salvare le modifiche (**CTRL+O**, **INVIO**) e chiudere l'editor (**CTRL+X**).</span><span class="sxs-lookup"><span data-stu-id="f5062-128">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="build-the-sample"></a><span data-ttu-id="f5062-129">Compilare l'esempio</span><span class="sxs-lookup"><span data-stu-id="f5062-129">Build the sample</span></span>

<span data-ttu-id="f5062-130">Installare i pacchetti di prerequisiti per Microsoft Azure IoT SDK per dispositivi di Microsoft per C eseguendo i comandi seguenti in un terminale di Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="f5062-130">Install the prerequisite packages for the Microsoft Azure IoT Device SDK for C by running the following commands in a terminal on the Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="f5062-131">È ora possibile compilare la soluzione di esempio aggiornata su Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="f5062-131">You can now build the updated sample solution on the Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
```

<span data-ttu-id="f5062-132">È ora possibile eseguire il programma di esempio su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="f5062-132">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="f5062-133">Immettere il comando:</span><span class="sxs-lookup"><span data-stu-id="f5062-133">Enter the command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="f5062-134">L'output seguente riporta un esempio dell'output visualizzato al prompt dei comandi su Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="f5062-134">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Output dell'app Raspberry Pi][img-raspberry-output]

<span data-ttu-id="f5062-136">Premere **CTRL-C** per uscire dal programma in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="f5062-136">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="f5062-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f5062-137">Next steps</span></span>

<span data-ttu-id="f5062-138">Visitare il [Centro per sviluppatori Azure IoT](https://azure.microsoft.com/develop/iot/) per altri esempi e documentazione su Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="f5062-138">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-basic/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
