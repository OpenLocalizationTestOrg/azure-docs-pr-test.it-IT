---
title: Connettere un gateway ad Azure IoT Suite con un Intel NUC | Microsoft Docs
description: Usare il kit gateway commerciale di Microsoft IoT e la soluzione di monitoraggio remoto preconfigurato. Usare il gateway Azure IoT Edge per connettersi alla soluzione di monitoraggio remoto, inviare dati di telemetria simulati al cloud e rispondere ai metodi richiamati dal dashboard della soluzione.
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
ms.openlocfilehash: 9ed57d3c23e2adbd42c054f33c8ed46e3d6c9792
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-azure-iot-edge-gateway-to-the-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a><span data-ttu-id="2d854-104">Collegare il gateway Azure IoT Edge alla soluzione preconfigurata di monitoraggio remoto e inviare dati di telemetria simulati</span><span class="sxs-lookup"><span data-stu-id="2d854-104">Connect your Azure IoT Edge gateway to the remote monitoring preconfigured solution and send simulated telemetry</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="2d854-105">In questa esercitazione viene illustrato come usare Azure IoT Edge per simulare dati relativi alla temperatura e all'umidità da inviare alla soluzione preconfigurata di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="2d854-105">This tutorial shows you how to use Azure IoT Edge to simulate temperature and humidity data to send to the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="2d854-106">L'esercitazione usa:</span><span class="sxs-lookup"><span data-stu-id="2d854-106">The tutorial uses:</span></span>

- <span data-ttu-id="2d854-107">Azure IoT Edge per implementare un gateway di esempio.</span><span class="sxs-lookup"><span data-stu-id="2d854-107">Azure IoT Edge to implement a sample gateway.</span></span>
- <span data-ttu-id="2d854-108">La soluzione preconfigurata di monitoraggio remoto IoT Suite come back-end basato su cloud.</span><span class="sxs-lookup"><span data-stu-id="2d854-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="2d854-109">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2d854-109">Overview</span></span>

<span data-ttu-id="2d854-110">In questa esercitazione si completa la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2d854-110">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="2d854-111">Distribuire un'istanza della soluzione preconfigurata di monitoraggio remoto nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d854-111">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="2d854-112">Questo passaggio distribuisce e configura automaticamente più servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d854-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="2d854-113">Configurare il dispositivo di gateway Intel NUC per la comunicazione con il computer e la soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="2d854-113">Set up your Intel NUC gateway device to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="2d854-114">Configurare il gateway IoT Edge per inviare dati di telemetria simulati che è possibile visualizzare nel dashboard della soluzione.</span><span class="sxs-lookup"><span data-stu-id="2d854-114">Configure the IoT Edge gateway to send simulated telemetry that you can view on the solution dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="2d854-115">La soluzione di monitoraggio remoto esegue il provisioning di un set di servizi di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d854-115">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="2d854-116">La distribuzione riflette un'architettura enterprise reale.</span><span class="sxs-lookup"><span data-stu-id="2d854-116">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="2d854-117">Per evitare costi di consumo di Azure non necessari, eliminare l'istanza della soluzione preconfigurata in azureiotsuite.com al completamento.</span><span class="sxs-lookup"><span data-stu-id="2d854-117">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="2d854-118">Se la soluzione preconfigurata occorre nuovamente, è possibile ricrearla facilmente.</span><span class="sxs-lookup"><span data-stu-id="2d854-118">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="2d854-119">Per altre informazioni sulla riduzione del consumo durante l'esecuzione della soluzione di monitoraggio remoto, vedere [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configurazione di soluzioni preconfigurate di Azure IoT Suite per scopi dimostrativi).</span><span class="sxs-lookup"><span data-stu-id="2d854-119">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

<span data-ttu-id="2d854-120">Ripetere i passaggi precedenti per aggiungere un secondo dispositivo tramite un ID di dispositivo, ad esempio **device02**.</span><span class="sxs-lookup"><span data-stu-id="2d854-120">Repeat the previous steps to add a second device using a Device ID such as **device02**.</span></span> <span data-ttu-id="2d854-121">Nell'esempio vengono inviati dati da due dispositivi simulati nel gateway alla soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="2d854-121">The sample sends data from two simulated devices in the gateway to the remote monitoring solution.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-the-custom-iot-edge-module"></a><span data-ttu-id="2d854-122">Compilare il modulo IoT Edge personalizzato</span><span class="sxs-lookup"><span data-stu-id="2d854-122">Build the custom IoT Edge module</span></span>

<span data-ttu-id="2d854-123">È ora possibile compilare il modulo IoT Edge personalizzato che consente al gateway di inviare messaggi alla soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="2d854-123">You can now build the custom IoT Edge module that enables the gateway to send messages to the remote monitoring solution.</span></span> <span data-ttu-id="2d854-124">Per altre informazioni sulla configurazione di un gateway e sui moduli IoT Edge, vedere [Concetti di Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="2d854-124">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="2d854-125">Scaricare il codice sorgente per i moduli personalizzati di IoT Edge da GitHub tramite i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2d854-125">Download the source code for the custom IoT Edge modules from GitHub using the following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="2d854-126">Compilare il modulo personalizzato IoT Edge tramite i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2d854-126">Build the custom IoT Edge module using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="2d854-127">Lo script di compilazione inserisce il modulo di IoT Edge libsimulator.so personalizzato nella cartella di compilazione.</span><span class="sxs-lookup"><span data-stu-id="2d854-127">The build script places the libsimulator.so custom IoT Edge module in the build folder.</span></span>

## <a name="configure-and-run-the-iot-edge-gateway"></a><span data-ttu-id="2d854-128">Configurare ed eseguire il gateway IoT Edge</span><span class="sxs-lookup"><span data-stu-id="2d854-128">Configure and run the IoT Edge gateway</span></span>

<span data-ttu-id="2d854-129">È ora possibile configurare il gateway IoT Edge per inviare dati di telemetria simulati al dashboard di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="2d854-129">You can now configure the IoT Edge gateway to send simulated telemetry to your remote monitoring dashboard.</span></span> <span data-ttu-id="2d854-130">Per altre informazioni sulla configurazione di un gateway e sui moduli IoT Edge, vedere [Concetti di Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="2d854-130">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="2d854-131">In questa esercitazione, si usa l'editor di testo standard `vi` in Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="2d854-131">In this tutorial, you use the standard `vi` text editor on the Intel NUC.</span></span> <span data-ttu-id="2d854-132">Se non è stato usato `vi` in precedenza, è necessario completare un'esercitazione introduttiva, ad esempio [Unix - The vi Editor Tutorial][lnk-vi-tutorial] per familiarizzare con questo editor.</span><span class="sxs-lookup"><span data-stu-id="2d854-132">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - The vi Editor Tutorial][lnk-vi-tutorial] to familiarize yourself with this editor.</span></span> <span data-ttu-id="2d854-133">In alternativa, è possibile installare l'editor [nano](https://www.nano-editor.org/) più semplice tramite il comando `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="2d854-133">Alternatively, you can install the more user-friendly [nano](https://www.nano-editor.org/) editor using the command `smart install nano -y`.</span></span>

<span data-ttu-id="2d854-134">Aprire il file di configurazione di esempio nell'editor **vi** usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2d854-134">Open the sample configuration file in the **vi** editor using the following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
```

<span data-ttu-id="2d854-135">Individuare le righe seguenti nella configurazione per il modulo IoTHub:</span><span class="sxs-lookup"><span data-stu-id="2d854-135">Locate the following lines in the configuration for the IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="2d854-136">Sostituire i valori segnaposto con le informazioni dell'hub IoT create e salvate all'inizio di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2d854-136">Replace the placeholder values with the IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="2d854-137">Il valore per IoTHubName è simile a **yourrmsolution37e08** e il valore per IoTSuffix è in genere **azure-devices.net**.</span><span class="sxs-lookup"><span data-stu-id="2d854-137">The value for IoTHubName looks like **yourrmsolution37e08**, and the value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="2d854-138">Individuare le righe seguenti nella configurazione per il modulo di mapping:</span><span class="sxs-lookup"><span data-stu-id="2d854-138">Locate the following lines in the configuration for the mapping module:</span></span>

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

<span data-ttu-id="2d854-139">Sostituire i segnaposti **deviceID** e **deviceKey** con gli ID e le chiavi per i due dispositivi creati in precedenza nella soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="2d854-139">Replace the **deviceID** and **deviceKey** placeholders with the IDs and keys for the two devices you created in the remote monitoring solution previously.</span></span>

<span data-ttu-id="2d854-140">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="2d854-140">Save your changes.</span></span>

<span data-ttu-id="2d854-141">Ora è possibile eseguire il gateway IoT Edge usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2d854-141">You can now run the IoT Edge gateway using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

<span data-ttu-id="2d854-142">Il gateway avvia Intel NUC e invia i dati di telemetria simulati alla soluzione di monitoraggio remoto:</span><span class="sxs-lookup"><span data-stu-id="2d854-142">The gateway starts on the Intel NUC and sends simulated telemetry to the remote monitoring solution:</span></span>

![Il gateway IoT Edge genera dati di telemetria simulati][img-simulated telemetry]

<span data-ttu-id="2d854-144">Premere **CTRL-C** per uscire dal programma in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="2d854-144">Press **Ctrl-C** to exit the program at any time.</span></span>

## <a name="view-the-telemetry"></a><span data-ttu-id="2d854-145">Visualizzare i dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="2d854-145">View the telemetry</span></span>

<span data-ttu-id="2d854-146">Il gateway IoT Edge ora invia dati di telemetria simulati alla soluzione di monitoraggio remota.</span><span class="sxs-lookup"><span data-stu-id="2d854-146">The IoT Edge gateway is now sending simulated telemetry to the remote monitoring solution.</span></span> <span data-ttu-id="2d854-147">È possibile visualizzare i dati di telemetria nel dashboard della soluzione.</span><span class="sxs-lookup"><span data-stu-id="2d854-147">You can view the telemetry on the solution dashboard.</span></span>

- <span data-ttu-id="2d854-148">Passare al dashboard della soluzione.</span><span class="sxs-lookup"><span data-stu-id="2d854-148">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="2d854-149">Selezionare uno dei due dispositivi configurati nel gateway nell'elenco a discesa **Dispositivo da visualizzare**.</span><span class="sxs-lookup"><span data-stu-id="2d854-149">Select one of the two devices you configured in the gateway in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="2d854-150">I dati di telemetria dai dispositivi di gateway vengono visualizzati nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="2d854-150">The telemetry from the gateway devices displays on the dashboard.</span></span>

![Visualizzare i dati di telemetria dai dispositivi di gateway simulati][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="2d854-152">Se si lascia la soluzione di monitoraggio remoto in esecuzione nell'account Azure, verrà addebitato il tempo dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2d854-152">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="2d854-153">Per altre informazioni sulla riduzione del consumo durante l'esecuzione della soluzione di monitoraggio remoto, vedere [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configurazione di soluzioni preconfigurate di Azure IoT Suite per scopi dimostrativi).</span><span class="sxs-lookup"><span data-stu-id="2d854-153">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="2d854-154">Al termine, eliminare la soluzione preconfigurata dall'account Azure.</span><span class="sxs-lookup"><span data-stu-id="2d854-154">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d854-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2d854-155">Next steps</span></span>

<span data-ttu-id="2d854-156">Visitare il [Centro per sviluppatori Azure IoT](https://azure.microsoft.com/develop/iot/) per altri esempi e documentazione su Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="2d854-156">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started