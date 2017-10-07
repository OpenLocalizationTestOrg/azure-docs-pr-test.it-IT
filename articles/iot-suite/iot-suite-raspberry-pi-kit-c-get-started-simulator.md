---
title: aaaConnect un tooAzure Raspberry Pi IoT Suite utilizzando C con dati di telemetria simulato | Documenti Microsoft
description: Utilizzare hello Starter Kit di Microsoft Azure IoT per hello Raspberry Pi 3 e Azure IoT Suite. Utilizzare tooconnect C toohello le Pi Raspberry soluzione di monitoraggio remoto, inviare i dati di telemetria simulato toohello cloud e rispondere toomethods richiamato dal dashboard di soluzione hello.
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
ms.openlocfilehash: 3c4fa43b381385d1a7896cada34aa3aa0b8e5fb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-simulated-telemetry-using-c"></a><span data-ttu-id="531c8-104">Connettere il toohello Raspberry Pi 3 soluzione di monitoraggio remoto e inviare dati di telemetria simulata utilizzando C</span><span class="sxs-lookup"><span data-stu-id="531c8-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send simulated telemetry using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="531c8-105">Questa esercitazione viene illustrato come toouse hello Raspberry Pi 3 toosimulate temperatura e umidità dati toosend toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="531c8-105">This tutorial shows you how toouse hello Raspberry Pi 3 toosimulate temperature and humidity data toosend toohello cloud.</span></span> <span data-ttu-id="531c8-106">esercitazione Hello utilizza:</span><span class="sxs-lookup"><span data-stu-id="531c8-106">hello tutorial uses:</span></span>

- <span data-ttu-id="531c8-107">Sistema operativo Raspbian, linguaggio di programmazione C hello e hello Microsoft Azure IoT SDK per C tooimplement un dispositivo di esempio.</span><span class="sxs-lookup"><span data-stu-id="531c8-107">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
- <span data-ttu-id="531c8-108">monitoraggio remoto IoT Suite Hello preconfigurato soluzione come hello basato su cloud back-end.</span><span class="sxs-lookup"><span data-stu-id="531c8-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="531c8-109">Hello remoto disposizioni soluzione monitoraggio di un set di servizi di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="531c8-109">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="531c8-110">distribuzione di Hello riflette un'architettura aziendale reale.</span><span class="sxs-lookup"><span data-stu-id="531c8-110">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="531c8-111">tooavoid addebiti di consumo di Azure, eliminare l'istanza di soluzione hello preconfigurato azureiotsuite.com dopo aver con esso.</span><span class="sxs-lookup"><span data-stu-id="531c8-111">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="531c8-112">Se è necessario hello nuovamente la soluzione preconfigurata, è possibile ricrearla facilmente.</span><span class="sxs-lookup"><span data-stu-id="531c8-112">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="531c8-113">Per ulteriori informazioni sulla riduzione del consumo durante l'esecuzione di soluzioni di monitoraggio remoto hello, vedere [configurazione Azure IoT Suite preconfigurato soluzioni per scopi dimostrativi][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="531c8-113">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="531c8-114">Scaricare e configurare l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="531c8-114">Download and configure hello sample</span></span>

<span data-ttu-id="531c8-115">È ora possibile scaricare e configurare l'applicazione client per il monitoraggio remoto di hello nelle Pi Raspberry.</span><span class="sxs-lookup"><span data-stu-id="531c8-115">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="531c8-116">Clonare il repository hello</span><span class="sxs-lookup"><span data-stu-id="531c8-116">Clone hello repositories</span></span>

<span data-ttu-id="531c8-117">Se non già stato fatto, hello clone richiesto repository eseguendo hello seguendo i comandi di un terminale il Pi:</span><span class="sxs-lookup"><span data-stu-id="531c8-117">If you haven't already done so, clone hello required repositories by running hello following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="531c8-118">Aggiornare la stringa di connessione dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="531c8-118">Update hello device connection string</span></span>

<span data-ttu-id="531c8-119">File di origine di esempio hello Open in hello **nano** editor utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="531c8-119">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="531c8-120">Individuare hello seguenti righe:</span><span class="sxs-lookup"><span data-stu-id="531c8-120">Locate hello following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="531c8-121">Sostituire i valori segnaposto hello con dispositivo hello e informazioni di IoT Hub è stato creato e salvato all'inizio di hello di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="531c8-121">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="531c8-122">Salvare le modifiche (**Ctrl O**, **invio**) e uscire dall'editor hello (**Ctrl + X**).</span><span class="sxs-lookup"><span data-stu-id="531c8-122">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="531c8-123">Compilare l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="531c8-123">Build hello sample</span></span>

<span data-ttu-id="531c8-124">Installare i pacchetti dei prerequisiti per Microsoft Azure IoT dispositivo SDK hello hello per C eseguendo hello seguendo i comandi in un terminal hello Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="531c8-124">Install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="531c8-125">È ora possibile compilare la soluzione di esempio hello aggiornato su hello Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="531c8-125">You can now build hello updated sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
```

<span data-ttu-id="531c8-126">È ora possibile eseguire il programma di esempio hello in hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="531c8-126">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="531c8-127">Immettere il comando hello:</span><span class="sxs-lookup"><span data-stu-id="531c8-127">Enter hello command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="531c8-128">Hello riportato di seguito è riportato un esempio di output di hello visualizzato al prompt dei comandi di hello in hello Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="531c8-128">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Output dell'app Raspberry Pi][img-raspberry-output]

<span data-ttu-id="531c8-130">Premere **Ctrl-C** programma hello tooexit in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="531c8-130">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="531c8-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="531c8-131">Next steps</span></span>

<span data-ttu-id="531c8-132">Visitare hello [Centro per sviluppatori Azure IoT](https://azure.microsoft.com/develop/iot/) per ulteriori esempi e documentazione su Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="531c8-132">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-simulator/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
