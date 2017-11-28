---
title: aaaConnect tooAzure un gateway IoT Suite utilizzando un NUC Intel | Documenti Microsoft
description: Utilizzare hello Microsoft IoT commerciale Gateway Kit e hello preconfigurato soluzione di monitoraggio remoto. Hello utilizzare Azure IoT Edge gateway tooconnect toohello soluzione di monitoraggio remoto, inviare i dati di telemetria simulato toohello cloud e rispondere toomethods richiamato dal dashboard di soluzione hello.
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
ms.openlocfilehash: 46b545fc21b054191c8f78ace20fc628f839a819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a><span data-ttu-id="2846e-104">Connettere il preconfigurati soluzione di monitoraggio remoto di Azure IoT Edge gateway toohello e inviare dati di telemetria simulata</span><span class="sxs-lookup"><span data-stu-id="2846e-104">Connect your Azure IoT Edge gateway toohello remote monitoring preconfigured solution and send simulated telemetry</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="2846e-105">Questa esercitazione viene illustrato come toouse Azure IoT Edge toosimulate temperatura e l'umidità dati toosend toohello monitoraggio remoto preconfigurato soluzione.</span><span class="sxs-lookup"><span data-stu-id="2846e-105">This tutorial shows you how toouse Azure IoT Edge toosimulate temperature and humidity data toosend toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="2846e-106">esercitazione Hello utilizza:</span><span class="sxs-lookup"><span data-stu-id="2846e-106">hello tutorial uses:</span></span>

- <span data-ttu-id="2846e-107">Azure IoT Edge tooimplement un gateway di esempio.</span><span class="sxs-lookup"><span data-stu-id="2846e-107">Azure IoT Edge tooimplement a sample gateway.</span></span>
- <span data-ttu-id="2846e-108">monitoraggio remoto IoT Suite Hello preconfigurato soluzione come hello basato su cloud back-end.</span><span class="sxs-lookup"><span data-stu-id="2846e-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="2846e-109">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2846e-109">Overview</span></span>

<span data-ttu-id="2846e-110">In questa esercitazione è completare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2846e-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="2846e-111">Distribuire un'istanza di hello remoto monitoraggio soluzione preconfigurata tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2846e-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="2846e-112">Questo passaggio distribuisce e configura automaticamente più servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="2846e-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="2846e-113">Consente di impostare il toocommunicate dispositivo gateway di Intel NUC con il computer e una soluzione di monitoraggio remoto hello.</span><span class="sxs-lookup"><span data-stu-id="2846e-113">Set up your Intel NUC gateway device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="2846e-114">Configurare hello IoT Edge gateway toosend simulato telemetria che è possibile visualizzare nel dashboard di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="2846e-114">Configure hello IoT Edge gateway toosend simulated telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="2846e-115">Hello remoto disposizioni soluzione monitoraggio di un set di servizi di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2846e-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="2846e-116">distribuzione di Hello riflette un'architettura aziendale reale.</span><span class="sxs-lookup"><span data-stu-id="2846e-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="2846e-117">tooavoid addebiti di consumo di Azure, eliminare l'istanza di soluzione hello preconfigurato azureiotsuite.com dopo aver con esso.</span><span class="sxs-lookup"><span data-stu-id="2846e-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="2846e-118">Se è necessario hello nuovamente la soluzione preconfigurata, è possibile ricrearla facilmente.</span><span class="sxs-lookup"><span data-stu-id="2846e-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="2846e-119">Per ulteriori informazioni sulla riduzione del consumo durante l'esecuzione di soluzioni di monitoraggio remoto hello, vedere [configurazione Azure IoT Suite preconfigurato soluzioni per scopi dimostrativi][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="2846e-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

<span data-ttu-id="2846e-120">Ripetere hello precedenti passaggi tooadd un secondo dispositivo con un ID di dispositivo, ad esempio **device02**.</span><span class="sxs-lookup"><span data-stu-id="2846e-120">Repeat hello previous steps tooadd a second device using a Device ID such as **device02**.</span></span> <span data-ttu-id="2846e-121">esempio Hello invia dati da due dispositivi simulati in hello gateway toohello soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="2846e-121">hello sample sends data from two simulated devices in hello gateway toohello remote monitoring solution.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a><span data-ttu-id="2846e-122">Compilazione del modulo IoT bordo personalizzato hello</span><span class="sxs-lookup"><span data-stu-id="2846e-122">Build hello custom IoT Edge module</span></span>

<span data-ttu-id="2846e-123">È ora possibile compilare moduli IoT Edge personalizzata hello che consente di hello gateway toosend messaggi toohello soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="2846e-123">You can now build hello custom IoT Edge module that enables hello gateway toosend messages toohello remote monitoring solution.</span></span> <span data-ttu-id="2846e-124">Per altre informazioni sulla configurazione di un gateway e sui moduli IoT Edge, vedere [Concetti di Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="2846e-124">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="2846e-125">Scaricare il codice sorgente di hello per i moduli di IoT bordo personalizzati hello da GitHub utilizzando hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="2846e-125">Download hello source code for hello custom IoT Edge modules from GitHub using hello following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="2846e-126">Compilazione del modulo IoT bordo personalizzato hello utilizzando hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="2846e-126">Build hello custom IoT Edge module using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="2846e-127">script di compilazione Hello inserisce modulo IoT Edge di hello libsimulator.so personalizzato nella cartella di compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="2846e-127">hello build script places hello libsimulator.so custom IoT Edge module in hello build folder.</span></span>

## <a name="configure-and-run-hello-iot-edge-gateway"></a><span data-ttu-id="2846e-128">Configurare ed eseguire hello gateway perimetrale IoT</span><span class="sxs-lookup"><span data-stu-id="2846e-128">Configure and run hello IoT Edge gateway</span></span>

<span data-ttu-id="2846e-129">È ora possibile configurare hello IoT Edge gateway toosend telemetria simulato tooyour remoto dashboard di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="2846e-129">You can now configure hello IoT Edge gateway toosend simulated telemetry tooyour remote monitoring dashboard.</span></span> <span data-ttu-id="2846e-130">Per altre informazioni sulla configurazione di un gateway e sui moduli IoT Edge, vedere [Concetti di Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="2846e-130">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="2846e-131">In questa esercitazione è utilizzare standard di hello `vi` editor di testo in hello NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="2846e-131">In this tutorial, you use hello standard `vi` text editor on hello Intel NUC.</span></span> <span data-ttu-id="2846e-132">Se non è stato utilizzato `vi` prima, si consiglia di completare un'esercitazione introduttiva, ad esempio [Unix - hello vi Editor esercitazione] [ lnk-vi-tutorial] toofamiliarize familiarità con questo editor.</span><span class="sxs-lookup"><span data-stu-id="2846e-132">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - hello vi Editor Tutorial][lnk-vi-tutorial] toofamiliarize yourself with this editor.</span></span> <span data-ttu-id="2846e-133">In alternativa, è possibile installare più semplice hello [nano](https://www.nano-editor.org/) editor utilizzando il comando hello `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="2846e-133">Alternatively, you can install hello more user-friendly [nano](https://www.nano-editor.org/) editor using hello command `smart install nano -y`.</span></span>

<span data-ttu-id="2846e-134">File di configurazione di esempio hello Open in hello **vi** editor utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2846e-134">Open hello sample configuration file in hello **vi** editor using hello following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
```

<span data-ttu-id="2846e-135">Individuare hello seguendo le linee nella configurazione di hello per il modulo di hub IOT hello:</span><span class="sxs-lookup"><span data-stu-id="2846e-135">Locate hello following lines in hello configuration for hello IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="2846e-136">Sostituire i segnaposto hello valori con informazioni di IoT Hub è stato creato e salvato in hello hello inizino di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2846e-136">Replace hello placeholder values with hello IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="2846e-137">il valore di Hello per IoTHubName simile **yourrmsolution37e08**, e il valore di hello per IoTSuffix è in genere **azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="2846e-137">hello value for IoTHubName looks like **yourrmsolution37e08**, and hello value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="2846e-138">Individuare hello seguendo le linee nella configurazione di hello per il modulo di mapping hello:</span><span class="sxs-lookup"><span data-stu-id="2846e-138">Locate hello following lines in hello configuration for hello mapping module:</span></span>

```json
args": [
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  },
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="2846e-139">Sostituire hello **deviceID** e **deviceKey** segnaposto con ID hello e le chiavi per i dispositivi hello due creato in precedenza nella soluzione di monitoraggio remoto hello.</span><span class="sxs-lookup"><span data-stu-id="2846e-139">Replace hello **deviceID** and **deviceKey** placeholders with hello IDs and keys for hello two devices you created in hello remote monitoring solution previously.</span></span>

<span data-ttu-id="2846e-140">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="2846e-140">Save your changes.</span></span>

<span data-ttu-id="2846e-141">È ora possibile eseguire hello gateway IoT Edge utilizzando hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="2846e-141">You can now run hello IoT Edge gateway using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

<span data-ttu-id="2846e-142">gateway Hello inizia hello NUC Intel e invia una soluzione di monitoraggio remoto toohello telemetria simulato:</span><span class="sxs-lookup"><span data-stu-id="2846e-142">hello gateway starts on hello Intel NUC and sends simulated telemetry toohello remote monitoring solution:</span></span>

![Il gateway IoT Edge genera dati di telemetria simulati][img-simulated telemetry]

<span data-ttu-id="2846e-144">Premere **Ctrl-C** programma hello tooexit in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="2846e-144">Press **Ctrl-C** tooexit hello program at any time.</span></span>

## <a name="view-hello-telemetry"></a><span data-ttu-id="2846e-145">Visualizzazione hello telemetria</span><span class="sxs-lookup"><span data-stu-id="2846e-145">View hello telemetry</span></span>

<span data-ttu-id="2846e-146">soluzione di monitoraggio remoto di telemetria simulato toohello ora invia Hello gateway perimetrale IoT.</span><span class="sxs-lookup"><span data-stu-id="2846e-146">hello IoT Edge gateway is now sending simulated telemetry toohello remote monitoring solution.</span></span> <span data-ttu-id="2846e-147">È possibile visualizzare i dati di telemetria hello nel dashboard di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="2846e-147">You can view hello telemetry on hello solution dashboard.</span></span>

- <span data-ttu-id="2846e-148">Passare il dashboard di soluzione toohello.</span><span class="sxs-lookup"><span data-stu-id="2846e-148">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="2846e-149">Selezionare uno dei dispositivi hello due configurato nel gateway hello in hello **tooView dispositivo** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="2846e-149">Select one of hello two devices you configured in hello gateway in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="2846e-150">Consente di visualizzare dati di telemetria Hello dai dispositivi gateway hello nel dashboard di hello.</span><span class="sxs-lookup"><span data-stu-id="2846e-150">hello telemetry from hello gateway devices displays on hello dashboard.</span></span>

![Visualizzare i dati di telemetria dai dispositivi gateway hello simulata][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="2846e-152">Se si lascia in esecuzione nell'account di Azure di soluzione di monitoraggio remoto hello, verrà addebitato per volta hello che è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2846e-152">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="2846e-153">Per ulteriori informazioni sulla riduzione del consumo durante l'esecuzione di soluzioni di monitoraggio remoto hello, vedere [configurazione Azure IoT Suite preconfigurato soluzioni per scopi dimostrativi][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="2846e-153">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="2846e-154">Eliminare la soluzione hello preconfigurato dall'account di Azure al termine dell'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="2846e-154">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2846e-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2846e-155">Next steps</span></span>

<span data-ttu-id="2846e-156">Visitare hello [Centro per sviluppatori Azure IoT](https://azure.microsoft.com/develop/iot/) per ulteriori esempi e documentazione su Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="2846e-156">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started