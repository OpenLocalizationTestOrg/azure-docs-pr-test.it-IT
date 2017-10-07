---
title: aaaConnect un tooAzure Raspberry Pi IoT Suite con C sensori reali | Documenti Microsoft
description: Utilizzare hello Starter Kit di Microsoft Azure IoT per hello Raspberry Pi 3 e Azure IoT Suite. Utilizzare tooconnect C toohello le Pi Raspberry soluzione di monitoraggio remoto, inviare i dati di telemetria da sensori toohello cloud e rispondere toomethods richiamato dal dashboard di soluzione hello.
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
ms.openlocfilehash: 7dac55ae5fde4c6f8e3ea6a7debf9a6822dc07ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-c"></a><span data-ttu-id="5c1cf-104">Connettere il toohello Raspberry Pi 3 soluzione di monitoraggio remoto e inviare dati di telemetria da un sensore reale utilizzando C</span><span class="sxs-lookup"><span data-stu-id="5c1cf-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send telemetry from a real sensor using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="5c1cf-105">Questa esercitazione viene illustrato come toouse hello IoT Starter Kit di Microsoft Azure per 3 Pi Raspberry toodevelop un lettore di temperatura e umidità in grado di comunicare con il cloud hello.</span><span class="sxs-lookup"><span data-stu-id="5c1cf-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 toodevelop a temperature and humidity reader that can communicate with hello cloud.</span></span> <span data-ttu-id="5c1cf-106">esercitazione Hello utilizza:</span><span class="sxs-lookup"><span data-stu-id="5c1cf-106">hello tutorial uses:</span></span>

- <span data-ttu-id="5c1cf-107">Sistema operativo Raspbian, linguaggio di programmazione C hello e hello Microsoft Azure IoT SDK per C tooimplement un dispositivo di esempio.</span><span class="sxs-lookup"><span data-stu-id="5c1cf-107">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
- <span data-ttu-id="5c1cf-108">monitoraggio remoto IoT Suite Hello preconfigurato soluzione come hello basato su cloud back-end.</span><span class="sxs-lookup"><span data-stu-id="5c1cf-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="5c1cf-109">Panoramica</span><span class="sxs-lookup"><span data-stu-id="5c1cf-109">Overview</span></span>

<span data-ttu-id="5c1cf-110">In questa esercitazione è completare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5c1cf-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="5c1cf-111">Distribuire un'istanza di hello remoto monitoraggio soluzione preconfigurata tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5c1cf-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="5c1cf-112">Questo passaggio distribuisce e configura automaticamente più servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="5c1cf-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="5c1cf-113">Consente di impostare il dispositivo e sensori di toocommunicate con il computer e hello soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="5c1cf-113">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="5c1cf-114">Aggiornare hello esempio dispositivo codice tooconnect toohello soluzione di monitoraggio remoto e inviare dati di telemetria che è possibile visualizzare nel dashboard di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="5c1cf-114">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="5c1cf-115">Hello remoto disposizioni soluzione monitoraggio di un set di servizi di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5c1cf-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="5c1cf-116">distribuzione di Hello riflette un'architettura aziendale reale.</span><span class="sxs-lookup"><span data-stu-id="5c1cf-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="5c1cf-117">tooavoid addebiti di consumo di Azure, eliminare l'istanza di soluzione hello preconfigurato azureiotsuite.com dopo aver con esso.</span><span class="sxs-lookup"><span data-stu-id="5c1cf-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="5c1cf-118">Se è necessario hello nuovamente la soluzione preconfigurata, è possibile ricrearla facilmente.</span><span class="sxs-lookup"><span data-stu-id="5c1cf-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="5c1cf-119">Per ulteriori informazioni sulla riduzione del consumo durante l'esecuzione di soluzioni di monitoraggio remoto hello, vedere [configurazione Azure IoT Suite preconfigurato soluzioni per scopi dimostrativi][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="5c1cf-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="5c1cf-120">Scaricare e configurare l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="5c1cf-120">Download and configure hello sample</span></span>

<span data-ttu-id="5c1cf-121">È ora possibile scaricare e configurare l'applicazione client per il monitoraggio remoto di hello nelle Pi Raspberry.</span><span class="sxs-lookup"><span data-stu-id="5c1cf-121">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="5c1cf-122">Clonare il repository hello</span><span class="sxs-lookup"><span data-stu-id="5c1cf-122">Clone hello repositories</span></span>

<span data-ttu-id="5c1cf-123">Se non già stato fatto, hello clone richiesto repository eseguendo hello seguendo i comandi di un terminale il Pi:</span><span class="sxs-lookup"><span data-stu-id="5c1cf-123">If you haven't already done so, clone hello required repositories by running hello following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
git clone --recursive https://github.com/WiringPi/WiringPi.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="5c1cf-124">Aggiornare la stringa di connessione dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="5c1cf-124">Update hello device connection string</span></span>

<span data-ttu-id="5c1cf-125">File di origine di esempio hello Open in hello **nano** editor utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5c1cf-125">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="5c1cf-126">Individuare hello seguenti righe:</span><span class="sxs-lookup"><span data-stu-id="5c1cf-126">Locate hello following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="5c1cf-127">Sostituire i valori segnaposto hello con dispositivo hello e informazioni di IoT Hub è stato creato e salvato all'inizio di hello di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="5c1cf-127">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="5c1cf-128">Salvare le modifiche (**Ctrl O**, **invio**) e uscire dall'editor hello (**Ctrl + X**).</span><span class="sxs-lookup"><span data-stu-id="5c1cf-128">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="5c1cf-129">Compilare l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="5c1cf-129">Build hello sample</span></span>

<span data-ttu-id="5c1cf-130">Installare i pacchetti dei prerequisiti per Microsoft Azure IoT dispositivo SDK hello hello per C eseguendo hello seguendo i comandi in un terminal hello Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="5c1cf-130">Install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="5c1cf-131">È ora possibile compilare la soluzione di esempio hello aggiornato su hello Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="5c1cf-131">You can now build hello updated sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
```

<span data-ttu-id="5c1cf-132">È ora possibile eseguire il programma di esempio hello in hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="5c1cf-132">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="5c1cf-133">Immettere il comando hello:</span><span class="sxs-lookup"><span data-stu-id="5c1cf-133">Enter hello command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="5c1cf-134">Hello riportato di seguito è riportato un esempio di output di hello visualizzato al prompt dei comandi di hello in hello Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="5c1cf-134">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Output dell'app Raspberry Pi][img-raspberry-output]

<span data-ttu-id="5c1cf-136">Premere **Ctrl-C** programma hello tooexit in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="5c1cf-136">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="5c1cf-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5c1cf-137">Next steps</span></span>

<span data-ttu-id="5c1cf-138">Visitare hello [Centro per sviluppatori Azure IoT](https://azure.microsoft.com/develop/iot/) per ulteriori esempi e documentazione su Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="5c1cf-138">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-basic/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
