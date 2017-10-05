---
title: Connettere un gateway ad Azure IoT Suite con un Intel NUC | Microsoft Docs
description: Usare il kit gateway commerciale di Microsoft IoT e la soluzione di monitoraggio remoto preconfigurato. Usare il gateway Azure IoT Edge per abilitare un dispositivo SensorTag da connettere alla soluzione di monitoraggio remoto, inviare dati di telemetria al cloud e rispondere ai metodi richiamati dal dashboard della soluzione.
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
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: bda16be1094276fcecef1e708f9d7db307d94a89
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-azure-iot-edge-gateway-to-the-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a><span data-ttu-id="d4ab7-104">Collegare il gateway Azure IoT Edge alla soluzione preconfigurata di monitoraggio remoto e inviare dati di telemetria da un SensorTag</span><span class="sxs-lookup"><span data-stu-id="d4ab7-104">Connect your Azure IoT Edge gateway to the remote monitoring preconfigured solution and send telemetry from a SensorTag</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="d4ab7-105">In questa esercitazione viene illustrato come usare Azure IoT Edge per inviare dati relativi alla temperatura e all'umidità dal dispositivo SensorTag alla soluzione preconfigurata di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-105">This tutorial shows you how to use Azure IoT Edge to send temperature and humidity data from SensorTag device to the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="d4ab7-106">Il SensorTag si connette al gateway Intel NUC tramite Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-106">The SensorTag connects to the Intel NUC gateway using Bluetooth.</span></span> <span data-ttu-id="d4ab7-107">L'esercitazione usa:</span><span class="sxs-lookup"><span data-stu-id="d4ab7-107">The tutorial uses:</span></span>

- <span data-ttu-id="d4ab7-108">Azure IoT Edge per implementare un gateway di esempio.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-108">Azure IoT Edge to implement a sample gateway.</span></span>
- <span data-ttu-id="d4ab7-109">La soluzione preconfigurata di monitoraggio remoto IoT Suite come back-end basato su cloud.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-109">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="d4ab7-110">Panoramica</span><span class="sxs-lookup"><span data-stu-id="d4ab7-110">Overview</span></span>

<span data-ttu-id="d4ab7-111">In questa esercitazione si completa la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d4ab7-111">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="d4ab7-112">Distribuire un'istanza della soluzione preconfigurata di monitoraggio remoto nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-112">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="d4ab7-113">Questo passaggio distribuisce e configura automaticamente più servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-113">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="d4ab7-114">Configurare il dispositivo di gateway Intel NUC per la comunicazione con il computer e la soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-114">Set up your Intel NUC gateway device to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="d4ab7-115">Configurare il gateway Intel NUC per ricevere i dati di telemetria da un dispositivo SensorTag e inviarli al dashboard di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-115">Set up your Intel NUC gateway to receive telemetry from a SensorTag device and send it to the remote monitoring dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

<span data-ttu-id="d4ab7-116">[SensorTag BLE di Texas Instruments][lnk-sensortag].</span><span class="sxs-lookup"><span data-stu-id="d4ab7-116">[Texas Instruments BLE SensorTag][lnk-sensortag].</span></span> <span data-ttu-id="d4ab7-117">Questa esercitazione consente di recuperare i dati di telemetria sul Bluetooth dal dispositivo SensorTag.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-117">This tutorial retrieves telemetry data over Bluetooth from the SensorTag device.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="d4ab7-118">La soluzione di monitoraggio remoto esegue il provisioning di un set di servizi di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="d4ab7-119">La distribuzione riflette un'architettura enterprise reale.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-119">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="d4ab7-120">Per evitare costi di consumo di Azure non necessari, eliminare l'istanza della soluzione preconfigurata in azureiotsuite.com al completamento.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="d4ab7-121">Se la soluzione preconfigurata occorre nuovamente, è possibile ricrearla facilmente.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-121">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="d4ab7-122">Per altre informazioni sulla riduzione del consumo durante l'esecuzione della soluzione di monitoraggio remoto, vedere [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configurazione di soluzioni preconfigurate di Azure IoT Suite per scopi dimostrativi).</span><span class="sxs-lookup"><span data-stu-id="d4ab7-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a><span data-ttu-id="d4ab7-123">Configurare la connettività Bluetooth</span><span class="sxs-lookup"><span data-stu-id="d4ab7-123">Configure Bluetooth connectivity</span></span>

<span data-ttu-id="d4ab7-124">Configurare Bluetooth in Intel NUC per abilitare il dispositivo SensorTag a connettersi e a inviare dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-124">Configure Bluetooth on the Intel NUC to enable the SensorTag device to connect and send telemetry.</span></span>

### <a name="find-the-mac-address-of-the-sensortag"></a><span data-ttu-id="d4ab7-125">Trovare l'indirizzo MAC del SensorTag</span><span class="sxs-lookup"><span data-stu-id="d4ab7-125">Find the MAC address of the SensorTag</span></span>

1. <span data-ttu-id="d4ab7-126">Nella shell su Intel NUC, eseguire il comando seguente per sbloccare il servizio Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="d4ab7-126">In the shell on the Intel NUC, run the following command to unblock the Bluetooth service:</span></span>

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. <span data-ttu-id="d4ab7-127">Eseguire i comandi seguenti per avviare il servizio Bluetooth su Intel NUC e immettere la shell di Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="d4ab7-127">Run the following commands to start the Bluetooth service on the Intel NUC and enter the Bluetooth shell:</span></span>

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="d4ab7-128">Eseguire il comando seguente per accendere il controller Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="d4ab7-128">Run the following command to power on the Bluetooth controller:</span></span>

    ```bash
    power on
    ```

    <span data-ttu-id="d4ab7-129">Quando il controller è attivo, viene visualizzato un messaggio **Changing power on succeeded** (La modifica dell'accensione ha avuto esito positivo).</span><span class="sxs-lookup"><span data-stu-id="d4ab7-129">When the controller is on, you see a message **Changing power on succeeded**.</span></span>

1. <span data-ttu-id="d4ab7-130">Eseguire il comando seguente per avviare l'analisi per i dispositivi Bluetooth circostanti:</span><span class="sxs-lookup"><span data-stu-id="d4ab7-130">Run the following command to scan for nearby Bluetooth devices:</span></span>

    ```bash
    scan on
    ```

1. <span data-ttu-id="d4ab7-131">Premere il pulsante di accensione di SensorTag per renderlo individuabile.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-131">Press the power button on the SensorTag to make it discoverable.</span></span> <span data-ttu-id="d4ab7-132">Il LED verde lampeggia.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-132">The green LED flashes.</span></span>

1. <span data-ttu-id="d4ab7-133">Quando viene visualizzato un messaggio nella shell in base al quale il controller ha individuato il SensorTag, prendere nota dell'indirizzo MAC del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-133">When you see a message in the shell that the controller has discovered the SensorTag, make a note of the MAC address of the device.</span></span> <span data-ttu-id="d4ab7-134">L'indirizzo MAC è simile a **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-134">The MAC address looks like **A0:E6:F8:B5:F6:00**.</span></span> <span data-ttu-id="d4ab7-135">Quando si configura il gateway, più avanti nell'esercitazione, è necessario l'indirizzo MAC.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-135">You need the MAC address later in the tutorial when you configure the gateway.</span></span>

1. <span data-ttu-id="d4ab7-136">Eseguire il comando seguente per disattivare l'analisi del Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="d4ab7-136">Run the following command to turn off Bluetooth scanning:</span></span>

    ```bash
    scan off
    ```

1. <span data-ttu-id="d4ab7-137">Eseguire il comando seguente per verificare che è possibile connettersi al dispositivo SensorTag:</span><span class="sxs-lookup"><span data-stu-id="d4ab7-137">Run the following command to verify that you can connect to the SensorTag device:</span></span>

    ```bash
    connect <SensorTag MAC address>
    ```

    <span data-ttu-id="d4ab7-138">Se ci si connette correttamente, la shell visualizzerà il messaggio **Connessione riuscita** e stamperà informazioni sul dispositivo SensorTag.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-138">If you connect successfully, the shell shows the message **Connection successful** and prints information about the SensorTag device.</span></span> <span data-ttu-id="d4ab7-139">Se non è possibile connettersi, controllare che il SensorTag sia ancora acceso.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-139">If you cannot connect, check the SensorTag is still powered on.</span></span>

1. <span data-ttu-id="d4ab7-140">Ora è possibile disconnettersi da SensorTag e chiudere la shell del Bluetooth eseguendo i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d4ab7-140">You can now disconnect from the SensorTag and exit the Bluetooth shell by running the following commands:</span></span>

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-the-custom-iot-edge-module"></a><span data-ttu-id="d4ab7-141">Compilare il modulo IoT Edge personalizzato</span><span class="sxs-lookup"><span data-stu-id="d4ab7-141">Build the custom IoT Edge module</span></span>

<span data-ttu-id="d4ab7-142">È ora possibile compilare il modulo IoT Edge personalizzato che consente al gateway di inviare messaggi alla soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-142">You can now build the custom IoT Edge module that enables the gateway to send messages to the remote monitoring solution.</span></span> <span data-ttu-id="d4ab7-143">Per altre informazioni sulla configurazione di un gateway e sui moduli IoT Edge, vedere [Concetti di Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="d4ab7-143">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="d4ab7-144">Scaricare il codice sorgente per i moduli personalizzati di IoT Edge da GitHub tramite i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d4ab7-144">Download the source code for the custom IoT Edge modules from GitHub using the following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="d4ab7-145">Compilare il modulo personalizzato IoT Edge tramite i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d4ab7-145">Build the custom IoT Edge module using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="d4ab7-146">Lo script di compilazione inserisce il modulo di IoT Edge libsensor2remotemonitoring.so personalizzato nella cartella di compilazione.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-146">The build script places the libsensor2remotemonitoring.so custom IoT Edge module in the build folder.</span></span>

## <a name="configure-and-run-the-iot-edge-gateway"></a><span data-ttu-id="d4ab7-147">Configurare ed eseguire il gateway IoT Edge</span><span class="sxs-lookup"><span data-stu-id="d4ab7-147">Configure and run the IoT Edge gateway</span></span>

<span data-ttu-id="d4ab7-148">È ora possibile configurare il gateway IoT Edge per inviare dati di telemetria dal dispositivo SensorTag al dashboard di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-148">You can now configure the IoT Edge gateway to send telemetry from your SensorTag device to your remote monitoring dashboard.</span></span> <span data-ttu-id="d4ab7-149">Per altre informazioni sulla configurazione di un gateway e sui moduli IoT Edge, vedere [Concetti di Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="d4ab7-149">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="d4ab7-150">In questa esercitazione, si usa l'editor di testo standard `vi` in Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-150">In this tutorial, you use the standard `vi` text editor on the Intel NUC.</span></span> <span data-ttu-id="d4ab7-151">Se non è stato usato `vi` in precedenza, è necessario completare un'esercitazione introduttiva, ad esempio [Unix - The vi Editor Tutorial][lnk-vi-tutorial] per familiarizzare con questo editor.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-151">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - The vi Editor Tutorial][lnk-vi-tutorial] to familiarize yourself with this editor.</span></span> <span data-ttu-id="d4ab7-152">In alternativa, è possibile installare l'editor [nano](https://www.nano-editor.org/) più semplice tramite il comando `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-152">Alternatively, you can install the more user-friendly [nano](https://www.nano-editor.org/) editor using the command `smart install nano -y`.</span></span>

<span data-ttu-id="d4ab7-153">Aprire il file di configurazione di esempio nell'editor **vi** usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d4ab7-153">Open the sample configuration file in the **vi** editor using the following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

<span data-ttu-id="d4ab7-154">Individuare le righe seguenti nella configurazione per il modulo IoTHub:</span><span class="sxs-lookup"><span data-stu-id="d4ab7-154">Locate the following lines in the configuration for the IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="d4ab7-155">Sostituire i valori segnaposto con le informazioni dell'hub IoT create e salvate all'inizio di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-155">Replace the placeholder values with the IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="d4ab7-156">Il valore per IoTHubName è simile a **yourrmsolution37e08** e il valore per IoTSuffix è in genere **azure-devices.net**.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-156">The value for IoTHubName looks like **yourrmsolution37e08**, and the value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="d4ab7-157">Individuare le righe seguenti nella configurazione per il modulo di mapping:</span><span class="sxs-lookup"><span data-stu-id="d4ab7-157">Locate the following lines in the configuration for the mapping module:</span></span>

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="d4ab7-158">Sostituire il segnaposto **macAddress** con l'indirizzo MAC del SensorTag di cui si è preso nota in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-158">Replace the **macAddress** placeholder with the MAC address of your SensorTag you noted previously.</span></span> <span data-ttu-id="d4ab7-159">Sostituire i segnaposti **deviceID** e **deviceKey** con gli ID e le chiavi per i due dispositivi creati in precedenza nella soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-159">Replace the **deviceID** and **deviceKey** placeholders with the IDs and keys for the two devices you created in the remote monitoring solution previously.</span></span>

<span data-ttu-id="d4ab7-160">Individuare le righe seguenti nella configurazione per il modulo di SensorTag:</span><span class="sxs-lookup"><span data-stu-id="d4ab7-160">Locate the following lines in the configuration for the SensorTag module:</span></span>

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

<span data-ttu-id="d4ab7-161">Sostituire il segnaposto **device\_mac\_address** con l'indirizzo MAC del SensorTag di cui si è preso nota in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-161">Replace the **device\_mac\_address** placeholder  with the MAC address of your SensorTag you noted previously.</span></span>

<span data-ttu-id="d4ab7-162">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-162">Save your changes.</span></span>

<span data-ttu-id="d4ab7-163">Ora è possibile eseguire il gateway usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d4ab7-163">You can now run the gateway using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

<span data-ttu-id="d4ab7-164">Il gateway IoT Edge avvia Intel NUC e invia i dati di telemetria dal SensorTag alla soluzione di monitoraggio remoto:</span><span class="sxs-lookup"><span data-stu-id="d4ab7-164">The IoT Edge gateway starts on the Intel NUC and sends telemetry from the SensorTag to the remote monitoring solution:</span></span>

![Il gateway IoT Edge invia i dati di telemetria dal SensorTag][img-telemetry]

<span data-ttu-id="d4ab7-166">Premere **CTRL-C** per uscire dal programma in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-166">Press **Ctrl-C** to exit the program at any time.</span></span>

## <a name="view-the-telemetry"></a><span data-ttu-id="d4ab7-167">Visualizzare i dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="d4ab7-167">View the telemetry</span></span>

<span data-ttu-id="d4ab7-168">Ora il gateway invia i dati di telemetria dal dispositivo SensorTag alla soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-168">The gateway is now sending telemetry from the SensorTag device to the remote monitoring solution.</span></span> <span data-ttu-id="d4ab7-169">È possibile visualizzare i dati di telemetria nel dashboard della soluzione.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-169">You can view the telemetry on the solution dashboard.</span></span> <span data-ttu-id="d4ab7-170">È anche possibile inviare comandi al dispositivo SensorTag tramite il gateway dal dashboard della soluzione.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-170">You can also send commands to your SensorTag device through the gateway from the solution dashboard.</span></span>

- <span data-ttu-id="d4ab7-171">Passare al dashboard della soluzione.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-171">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="d4ab7-172">Selezionare il dispositivo configurato nel gateway che rappresenta il SensorTag nell'elenco a discesa **Dispositivo da visualizzare**.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-172">Select the device you configured in the gateway that represents the SensorTag in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="d4ab7-173">I dati di telemetria dal dispositivo SensorTag vengono visualizzati nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-173">The telemetry from the SensorTag device displays on the dashboard.</span></span>

![Visualizzare i dati di telemetria dai dispositivi SensorTag][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="d4ab7-175">Se si lascia la soluzione di monitoraggio remoto in esecuzione nell'account Azure, verrà addebitato il tempo dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-175">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="d4ab7-176">Per altre informazioni sulla riduzione del consumo durante l'esecuzione della soluzione di monitoraggio remoto, vedere [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configurazione di soluzioni preconfigurate di Azure IoT Suite per scopi dimostrativi).</span><span class="sxs-lookup"><span data-stu-id="d4ab7-176">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="d4ab7-177">Al termine, eliminare la soluzione preconfigurata dall'account Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-177">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d4ab7-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d4ab7-178">Next steps</span></span>

<span data-ttu-id="d4ab7-179">Visitare il [Centro per sviluppatori Azure IoT](https://azure.microsoft.com/develop/iot/) per altri esempi e documentazione su Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="d4ab7-179">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started