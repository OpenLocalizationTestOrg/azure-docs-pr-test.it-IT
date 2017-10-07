---
title: aaaConnect tooAzure un gateway IoT Suite utilizzando un NUC Intel | Documenti Microsoft
description: Utilizzare hello Microsoft IoT commerciale Gateway Kit e hello preconfigurato soluzione di monitoraggio remoto. Utilizzo di una soluzione di monitoraggio remoto toohello SensorTag dispositivo tooconnect hello Azure IoT Edge gateway tooenable, cloud toohello telemetria di inviare e rispondere toomethods richiamato dal dashboard di soluzione hello.
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
ms.openlocfilehash: 6f98ee3c1e2311a8644da9d72d40e671e7cbcf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a><span data-ttu-id="35e86-104">Connettere la soluzione preconfigurata di monitoraggio remoto di Azure IoT Edge gateway toohello e inviare dati di telemetria da un SensorTag</span><span class="sxs-lookup"><span data-stu-id="35e86-104">Connect your Azure IoT Edge gateway toohello remote monitoring preconfigured solution and send telemetry from a SensorTag</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="35e86-105">Questa esercitazione viene illustrato come toouse Azure IoT Edge toosend temperatura e umidità dati monitoraggio remoto di SensorTag dispositivo toohello preconfigurato soluzione.</span><span class="sxs-lookup"><span data-stu-id="35e86-105">This tutorial shows you how toouse Azure IoT Edge toosend temperature and humidity data from SensorTag device toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="35e86-106">Hello SensorTag si connette il gateway di Intel NUC toohello tramite Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="35e86-106">hello SensorTag connects toohello Intel NUC gateway using Bluetooth.</span></span> <span data-ttu-id="35e86-107">esercitazione Hello utilizza:</span><span class="sxs-lookup"><span data-stu-id="35e86-107">hello tutorial uses:</span></span>

- <span data-ttu-id="35e86-108">Azure IoT Edge tooimplement un gateway di esempio.</span><span class="sxs-lookup"><span data-stu-id="35e86-108">Azure IoT Edge tooimplement a sample gateway.</span></span>
- <span data-ttu-id="35e86-109">monitoraggio remoto IoT Suite Hello preconfigurato soluzione come hello basato su cloud back-end.</span><span class="sxs-lookup"><span data-stu-id="35e86-109">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="35e86-110">Panoramica</span><span class="sxs-lookup"><span data-stu-id="35e86-110">Overview</span></span>

<span data-ttu-id="35e86-111">In questa esercitazione è completare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="35e86-111">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="35e86-112">Distribuire un'istanza di hello remoto monitoraggio soluzione preconfigurata tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="35e86-112">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="35e86-113">Questo passaggio distribuisce e configura automaticamente più servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="35e86-113">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="35e86-114">Consente di impostare il toocommunicate dispositivo gateway di Intel NUC con il computer e una soluzione di monitoraggio remoto hello.</span><span class="sxs-lookup"><span data-stu-id="35e86-114">Set up your Intel NUC gateway device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="35e86-115">Imposta i dati di telemetria Intel NUC tooreceive gateway da un dispositivo SensorTag e inviarla toohello dashboard di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="35e86-115">Set up your Intel NUC gateway tooreceive telemetry from a SensorTag device and send it toohello remote monitoring dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

<span data-ttu-id="35e86-116">[SensorTag BLE di Texas Instruments][lnk-sensortag].</span><span class="sxs-lookup"><span data-stu-id="35e86-116">[Texas Instruments BLE SensorTag][lnk-sensortag].</span></span> <span data-ttu-id="35e86-117">In questa esercitazione consente di recuperare i dati di telemetria tramite Bluetooth dal dispositivo SensorTag hello.</span><span class="sxs-lookup"><span data-stu-id="35e86-117">This tutorial retrieves telemetry data over Bluetooth from hello SensorTag device.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="35e86-118">Hello remoto disposizioni soluzione monitoraggio di un set di servizi di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="35e86-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="35e86-119">distribuzione di Hello riflette un'architettura aziendale reale.</span><span class="sxs-lookup"><span data-stu-id="35e86-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="35e86-120">tooavoid addebiti di consumo di Azure, eliminare l'istanza di soluzione hello preconfigurato azureiotsuite.com dopo aver con esso.</span><span class="sxs-lookup"><span data-stu-id="35e86-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="35e86-121">Se è necessario hello nuovamente la soluzione preconfigurata, è possibile ricrearla facilmente.</span><span class="sxs-lookup"><span data-stu-id="35e86-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="35e86-122">Per ulteriori informazioni sulla riduzione del consumo durante l'esecuzione di soluzioni di monitoraggio remoto hello, vedere [configurazione Azure IoT Suite preconfigurato soluzioni per scopi dimostrativi][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="35e86-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a><span data-ttu-id="35e86-123">Configurare la connettività Bluetooth</span><span class="sxs-lookup"><span data-stu-id="35e86-123">Configure Bluetooth connectivity</span></span>

<span data-ttu-id="35e86-124">Configurare la funzione Bluetooth nel dispositivo tooconnect di hello Intel NUC tooenable hello SensorTag e inviare dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="35e86-124">Configure Bluetooth on hello Intel NUC tooenable hello SensorTag device tooconnect and send telemetry.</span></span>

### <a name="find-hello-mac-address-of-hello-sensortag"></a><span data-ttu-id="35e86-125">Trovare l'indirizzo MAC hello di hello SensorTag</span><span class="sxs-lookup"><span data-stu-id="35e86-125">Find hello MAC address of hello SensorTag</span></span>

1. <span data-ttu-id="35e86-126">Nella shell di hello in hello NUC Intel, eseguire hello comando toounblock hello Bluetooth servizio:</span><span class="sxs-lookup"><span data-stu-id="35e86-126">In hello shell on hello Intel NUC, run hello following command toounblock hello Bluetooth service:</span></span>

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. <span data-ttu-id="35e86-127">La seguente esecuzione hello comandi toostart hello Bluetooth servizio hello NUC Intel e immettere shell Bluetooth hello:</span><span class="sxs-lookup"><span data-stu-id="35e86-127">Run hello following commands toostart hello Bluetooth service on hello Intel NUC and enter hello Bluetooth shell:</span></span>

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="35e86-128">Eseguire hello toopower comando sul controller Bluetooth hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="35e86-128">Run hello following command toopower on hello Bluetooth controller:</span></span>

    ```bash
    power on
    ```

    <span data-ttu-id="35e86-129">Quando il controller hello è attiva, viene visualizzato un messaggio **la modifica di alimentazione in cui ha avuto esito positivo**.</span><span class="sxs-lookup"><span data-stu-id="35e86-129">When hello controller is on, you see a message **Changing power on succeeded**.</span></span>

1. <span data-ttu-id="35e86-130">Eseguire hello tooscan di comando per i dispositivi Bluetooth circostanti seguenti:</span><span class="sxs-lookup"><span data-stu-id="35e86-130">Run hello following command tooscan for nearby Bluetooth devices:</span></span>

    ```bash
    scan on
    ```

1. <span data-ttu-id="35e86-131">Premere hello power pulsante toomake SensorTag hello è individuabile.</span><span class="sxs-lookup"><span data-stu-id="35e86-131">Press hello power button on hello SensorTag toomake it discoverable.</span></span> <span data-ttu-id="35e86-132">fa lampeggiare il LED verde Hello.</span><span class="sxs-lookup"><span data-stu-id="35e86-132">hello green LED flashes.</span></span>

1. <span data-ttu-id="35e86-133">Quando viene visualizzato un messaggio nella shell di hello tale controller hello ha individuato hello SensorTag, prendere nota dell'indirizzo MAC del dispositivo hello hello.</span><span class="sxs-lookup"><span data-stu-id="35e86-133">When you see a message in hello shell that hello controller has discovered hello SensorTag, make a note of hello MAC address of hello device.</span></span> <span data-ttu-id="35e86-134">Hello indirizzo MAC è simile a **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="35e86-134">hello MAC address looks like **A0:E6:F8:B5:F6:00**.</span></span> <span data-ttu-id="35e86-135">Indirizzo MAC hello è necessario più avanti nell'esercitazione di hello quando si configura gateway hello.</span><span class="sxs-lookup"><span data-stu-id="35e86-135">You need hello MAC address later in hello tutorial when you configure hello gateway.</span></span>

1. <span data-ttu-id="35e86-136">Eseguire hello successivo comando tooturn la scansione Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="35e86-136">Run hello following command tooturn off Bluetooth scanning:</span></span>

    ```bash
    scan off
    ```

1. <span data-ttu-id="35e86-137">Eseguire hello dopo che è possibile collegare il dispositivo di SensorTag toohello tooverify di comando:</span><span class="sxs-lookup"><span data-stu-id="35e86-137">Run hello following command tooverify that you can connect toohello SensorTag device:</span></span>

    ```bash
    connect <SensorTag MAC address>
    ```

    <span data-ttu-id="35e86-138">Se ci si connette correttamente, la shell hello Mostra messaggio hello **connessione riuscita** e Visualizza informazioni sul dispositivo SensorTag hello.</span><span class="sxs-lookup"><span data-stu-id="35e86-138">If you connect successfully, hello shell shows hello message **Connection successful** and prints information about hello SensorTag device.</span></span> <span data-ttu-id="35e86-139">Se non è possibile connettersi, controllare hello che sensortag è ancora attiva.</span><span class="sxs-lookup"><span data-stu-id="35e86-139">If you cannot connect, check hello SensorTag is still powered on.</span></span>

1. <span data-ttu-id="35e86-140">È ora possibile disconnettersi dalle hello SensorTag e uscire dalla shell Bluetooth hello eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="35e86-140">You can now disconnect from hello SensorTag and exit hello Bluetooth shell by running hello following commands:</span></span>

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a><span data-ttu-id="35e86-141">Compilazione del modulo IoT bordo personalizzato hello</span><span class="sxs-lookup"><span data-stu-id="35e86-141">Build hello custom IoT Edge module</span></span>

<span data-ttu-id="35e86-142">È ora possibile compilare moduli IoT Edge personalizzata hello che consente di hello gateway toosend messaggi toohello soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="35e86-142">You can now build hello custom IoT Edge module that enables hello gateway toosend messages toohello remote monitoring solution.</span></span> <span data-ttu-id="35e86-143">Per altre informazioni sulla configurazione di un gateway e sui moduli IoT Edge, vedere [Concetti di Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="35e86-143">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="35e86-144">Scaricare il codice sorgente di hello per i moduli di IoT bordo personalizzati hello da GitHub utilizzando hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="35e86-144">Download hello source code for hello custom IoT Edge modules from GitHub using hello following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="35e86-145">Compilazione del modulo IoT bordo personalizzato hello utilizzando hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="35e86-145">Build hello custom IoT Edge module using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="35e86-146">script di compilazione Hello inserisce modulo IoT Edge di hello libsensor2remotemonitoring.so personalizzato nella cartella di compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="35e86-146">hello build script places hello libsensor2remotemonitoring.so custom IoT Edge module in hello build folder.</span></span>

## <a name="configure-and-run-hello-iot-edge-gateway"></a><span data-ttu-id="35e86-147">Configurare ed eseguire hello gateway perimetrale IoT</span><span class="sxs-lookup"><span data-stu-id="35e86-147">Configure and run hello IoT Edge gateway</span></span>

<span data-ttu-id="35e86-148">È ora possibile configurare hello telemetria di IoT Edge gateway toosend dal dispositivo SensorTag per tooyour dashboard di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="35e86-148">You can now configure hello IoT Edge gateway toosend telemetry from your SensorTag device tooyour remote monitoring dashboard.</span></span> <span data-ttu-id="35e86-149">Per altre informazioni sulla configurazione di un gateway e sui moduli IoT Edge, vedere [Concetti di Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="35e86-149">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="35e86-150">In questa esercitazione è utilizzare standard di hello `vi` editor di testo in hello NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="35e86-150">In this tutorial, you use hello standard `vi` text editor on hello Intel NUC.</span></span> <span data-ttu-id="35e86-151">Se non è stato utilizzato `vi` prima, si consiglia di completare un'esercitazione introduttiva, ad esempio [Unix - hello vi Editor esercitazione] [ lnk-vi-tutorial] toofamiliarize familiarità con questo editor.</span><span class="sxs-lookup"><span data-stu-id="35e86-151">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - hello vi Editor Tutorial][lnk-vi-tutorial] toofamiliarize yourself with this editor.</span></span> <span data-ttu-id="35e86-152">In alternativa, è possibile installare più semplice hello [nano](https://www.nano-editor.org/) editor utilizzando il comando hello `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="35e86-152">Alternatively, you can install hello more user-friendly [nano](https://www.nano-editor.org/) editor using hello command `smart install nano -y`.</span></span>

<span data-ttu-id="35e86-153">File di configurazione di esempio hello Open in hello **vi** editor utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="35e86-153">Open hello sample configuration file in hello **vi** editor using hello following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

<span data-ttu-id="35e86-154">Individuare hello seguendo le linee nella configurazione di hello per il modulo di hub IOT hello:</span><span class="sxs-lookup"><span data-stu-id="35e86-154">Locate hello following lines in hello configuration for hello IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="35e86-155">Sostituire i segnaposto hello valori con informazioni di IoT Hub è stato creato e salvato in hello hello inizino di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="35e86-155">Replace hello placeholder values with hello IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="35e86-156">il valore di Hello per IoTHubName simile **yourrmsolution37e08**, e il valore di hello per IoTSuffix è in genere **azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="35e86-156">hello value for IoTHubName looks like **yourrmsolution37e08**, and hello value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="35e86-157">Individuare hello seguendo le linee nella configurazione di hello per il modulo di mapping hello:</span><span class="sxs-lookup"><span data-stu-id="35e86-157">Locate hello following lines in hello configuration for hello mapping module:</span></span>

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="35e86-158">Sostituire hello **macAddress** segnaposto con hello indirizzo MAC del SensorTag è indicato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="35e86-158">Replace hello **macAddress** placeholder with hello MAC address of your SensorTag you noted previously.</span></span> <span data-ttu-id="35e86-159">Sostituire hello **deviceID** e **deviceKey** segnaposto con ID hello e le chiavi per i dispositivi hello due creato in precedenza nella soluzione di monitoraggio remoto hello.</span><span class="sxs-lookup"><span data-stu-id="35e86-159">Replace hello **deviceID** and **deviceKey** placeholders with hello IDs and keys for hello two devices you created in hello remote monitoring solution previously.</span></span>

<span data-ttu-id="35e86-160">Individuare hello seguendo le linee nella configurazione di hello per modulo SensorTag hello:</span><span class="sxs-lookup"><span data-stu-id="35e86-160">Locate hello following lines in hello configuration for hello SensorTag module:</span></span>

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

<span data-ttu-id="35e86-161">Sostituire hello **dispositivo\_mac\_indirizzo** segnaposto con hello indirizzo MAC del SensorTag è indicato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="35e86-161">Replace hello **device\_mac\_address** placeholder  with hello MAC address of your SensorTag you noted previously.</span></span>

<span data-ttu-id="35e86-162">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="35e86-162">Save your changes.</span></span>

<span data-ttu-id="35e86-163">È ora possibile eseguire il gateway di hello tramite hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="35e86-163">You can now run hello gateway using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

<span data-ttu-id="35e86-164">Hello gateway perimetrale IoT inizia hello NUC Intel e invia i dati di telemetria dalla soluzione di monitoraggio remoto toohello SensorTag hello:</span><span class="sxs-lookup"><span data-stu-id="35e86-164">hello IoT Edge gateway starts on hello Intel NUC and sends telemetry from hello SensorTag toohello remote monitoring solution:</span></span>

![Gateway di confine IoT invia dati di telemetria da hello SensorTag][img-telemetry]

<span data-ttu-id="35e86-166">Premere **Ctrl-C** programma hello tooexit in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="35e86-166">Press **Ctrl-C** tooexit hello program at any time.</span></span>

## <a name="view-hello-telemetry"></a><span data-ttu-id="35e86-167">Visualizzazione hello telemetria</span><span class="sxs-lookup"><span data-stu-id="35e86-167">View hello telemetry</span></span>

<span data-ttu-id="35e86-168">gateway Hello ora invia dati di telemetria da hello SensorTag dispositivo toohello soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="35e86-168">hello gateway is now sending telemetry from hello SensorTag device toohello remote monitoring solution.</span></span> <span data-ttu-id="35e86-169">È possibile visualizzare i dati di telemetria hello nel dashboard di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="35e86-169">You can view hello telemetry on hello solution dashboard.</span></span> <span data-ttu-id="35e86-170">È anche possibile inviare dispositivo SensorTag tooyour di comandi tramite gateway hello dal dashboard di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="35e86-170">You can also send commands tooyour SensorTag device through hello gateway from hello solution dashboard.</span></span>

- <span data-ttu-id="35e86-171">Passare il dashboard di soluzione toohello.</span><span class="sxs-lookup"><span data-stu-id="35e86-171">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="35e86-172">Dispositivo hello selezionare configurato nel gateway hello che rappresenta Ciao SensorTag hello **tooView dispositivo** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="35e86-172">Select hello device you configured in hello gateway that represents hello SensorTag in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="35e86-173">Consente di visualizzare dati di telemetria Hello dal dispositivo SensorTag hello nel dashboard di hello.</span><span class="sxs-lookup"><span data-stu-id="35e86-173">hello telemetry from hello SensorTag device displays on hello dashboard.</span></span>

![Visualizzare i dati di telemetria dai dispositivi SensorTag hello][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="35e86-175">Se si lascia in esecuzione nell'account di Azure di soluzione di monitoraggio remoto hello, verrà addebitato per volta hello che è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="35e86-175">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="35e86-176">Per ulteriori informazioni sulla riduzione del consumo durante l'esecuzione di soluzioni di monitoraggio remoto hello, vedere [configurazione Azure IoT Suite preconfigurato soluzioni per scopi dimostrativi][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="35e86-176">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="35e86-177">Eliminare la soluzione hello preconfigurato dall'account di Azure al termine dell'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="35e86-177">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="35e86-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="35e86-178">Next steps</span></span>

<span data-ttu-id="35e86-179">Visitare hello [Centro per sviluppatori Azure IoT](https://azure.microsoft.com/develop/iot/) per ulteriori esempi e documentazione su Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="35e86-179">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started