---
title: aaaUse un tooconnect di gateway tooAzure un dispositivo IoT Hub IoT | Documenti Microsoft
description: Informazioni su come toouse NUC Intel come un tooconnect gateway IoT un SensorTag TI e trasmissione sensore dati tooAzure IoT Hub in hello cloud.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: gateway IOT connettersi toocloud dispositivo
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 418af34bf29992d46b76ae59ef548744808664c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-tooconnect-things-toohello-cloud---sensortag-tooazure-iot-hub"></a><span data-ttu-id="5e041-104">Utilizzare il cloud IoT gateway tooconnect operazioni toohello - SensorTag tooAzure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="5e041-104">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>

> [!NOTE]
> <span data-ttu-id="5e041-105">Prima di iniziare questa esercitazione, assicurarsi di aver completato [Configurare Intel NUC come gateway IoT di Azure](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span><span class="sxs-lookup"><span data-stu-id="5e041-105">Before you start this tutorial, make sure you’ve completed [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span></span> <span data-ttu-id="5e041-106">In [impostare NUC Intel come gateway IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), si configura il dispositivo Intel NUC hello come gateway IoT.</span><span class="sxs-lookup"><span data-stu-id="5e041-106">In [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), you set up hello Intel NUC device as an IoT gateway.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5e041-107">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="5e041-107">What you will learn</span></span>

<span data-ttu-id="5e041-108">Si apprenderà come toouse un tooconnect gateway IoT un IoT Hub di tooAzure Texas strumenti SensorTag (CC2650STK).</span><span class="sxs-lookup"><span data-stu-id="5e041-108">You learn how toouse an IoT gateway tooconnect a Texas Instruments SensorTag (CC2650STK) tooAzure IoT Hub.</span></span> <span data-ttu-id="5e041-109">gateway IoT Hello invia temperatura e umidità raccolti da hello SensorTag tooAzure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5e041-109">hello IoT gateway sends temperature and humidity data collected from hello SensorTag tooAzure IoT Hub.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5e041-110">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="5e041-110">What you will do</span></span>

- <span data-ttu-id="5e041-111">Creare un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5e041-111">Create an IoT hub.</span></span>
- <span data-ttu-id="5e041-112">Registrare un dispositivo nell'hub IoT hello per hello SensorTag.</span><span class="sxs-lookup"><span data-stu-id="5e041-112">Register a device in hello IoT hub for hello SensorTag.</span></span>
- <span data-ttu-id="5e041-113">Abilitare la connessione di hello tra gateway IoT hello e hello SensorTag.</span><span class="sxs-lookup"><span data-stu-id="5e041-113">Enable hello connection between hello IoT gateway and hello SensorTag.</span></span>
- <span data-ttu-id="5e041-114">Eseguire un BILITA esempio applicazione toosend SensorTag dati tooyour hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5e041-114">Run a BLE sample application toosend SensorTag data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5e041-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="5e041-115">What you need</span></span>

- <span data-ttu-id="5e041-116">Completare l'esercitazione [Configurare Intel NUC come gateway IoT di Azure](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) in cui si configura il dispositivo Intel NUC come gateway IoT.</span><span class="sxs-lookup"><span data-stu-id="5e041-116">Tutorial [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) completed in which you set up Intel NUC as an IoT gateway.</span></span>
- * <span data-ttu-id="5e041-117">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="5e041-117">An active Azure subscription.</span></span> <span data-ttu-id="5e041-118">Se non si ha un account Azure, [creare un account Azure gratuito](https://azure.microsoft.com/free/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="5e041-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
- <span data-ttu-id="5e041-119">Un client SSH in esecuzione nel computer host.</span><span class="sxs-lookup"><span data-stu-id="5e041-119">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="5e041-120">Si consiglia l'uso di PuTTY in Windows.</span><span class="sxs-lookup"><span data-stu-id="5e041-120">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="5e041-121">Linux e macOS sono già dotati di un client SSH.</span><span class="sxs-lookup"><span data-stu-id="5e041-121">Linux and macOS already come with an SSH client.</span></span>
- <span data-ttu-id="5e041-122">indirizzo IP Hello e hello nome utente e password tooaccess hello gateway dal client SSH hello.</span><span class="sxs-lookup"><span data-stu-id="5e041-122">hello IP address and hello username and password tooaccess hello gateway from hello SSH client.</span></span>
- <span data-ttu-id="5e041-123">Una connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="5e041-123">An Internet connection.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> <span data-ttu-id="5e041-124">Qui è possibile registrare questo nuovo dispositivo per SensorTag</span><span class="sxs-lookup"><span data-stu-id="5e041-124">Here you register this new device for your SensorTag</span></span>

## <a name="enable-hello-connection-between-hello-iot-gateway-and-hello-sensortag"></a><span data-ttu-id="5e041-125">Abilitare hello connessione tra gateway IoT hello e hello SensorTag</span><span class="sxs-lookup"><span data-stu-id="5e041-125">Enable hello connection between hello IoT gateway and hello SensorTag</span></span>

<span data-ttu-id="5e041-126">In questa sezione è eseguire hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="5e041-126">In this section, you perform hello following tasks:</span></span>

- <span data-ttu-id="5e041-127">Ottenere l'indirizzo MAC hello di hello SensorTag per connessione Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="5e041-127">Get hello MAC address of hello SensorTag for Bluetooth connection.</span></span>
- <span data-ttu-id="5e041-128">Avviare una connessione Bluetooth da hello IoT gateway toohello SensorTag.</span><span class="sxs-lookup"><span data-stu-id="5e041-128">Initiate a Bluetooth connection from hello IoT gateway toohello SensorTag.</span></span>

### <a name="get-hello-mac-address-of-hello-sensortag-for-bluetooth-connection"></a><span data-ttu-id="5e041-129">Ottenere l'indirizzo MAC hello di hello SensorTag per connessione Bluetooth</span><span class="sxs-lookup"><span data-stu-id="5e041-129">Get hello MAC address of hello SensorTag for Bluetooth connection</span></span>

1. <span data-ttu-id="5e041-130">Nel computer host hello, eseguire client SSH hello e toohello IoT gateway di connessione.</span><span class="sxs-lookup"><span data-stu-id="5e041-130">On hello host computer, run hello SSH client and connect toohello IoT gateway.</span></span>
1. <span data-ttu-id="5e041-131">Sbloccare Bluetooth eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5e041-131">Unblock Bluetooth by running hello following command:</span></span>

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. <span data-ttu-id="5e041-132">Avviare il servizio di Bluetooth hello sul gateway IoT hello e immettere un tooconfigure shell Bluetooth Bluetooth eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="5e041-132">Start hello Bluetooth service on hello IoT gateway and enter a Bluetooth shell tooconfigure Bluetooth by running hello following commands:</span></span>

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. <span data-ttu-id="5e041-133">Accendere il controller Bluetooth hello eseguendo hello comando in hello Bluetooth shell seguente:</span><span class="sxs-lookup"><span data-stu-id="5e041-133">Power on hello Bluetooth controller by running hello following command at hello Bluetooth shell:</span></span>

   ```bash
   power on
   ```

   ![alimentazione sul controller Bluetooth hello gateway IoT hello con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="5e041-135">Avvia l'analisi per i dispositivi Bluetooth circostanti eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5e041-135">Start scanning for nearby Bluetooth devices by running hello following command:</span></span>

   ```bash
   scan on
   ```

   ![Analizzare i dispositivi Bluetooth citcostanti con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="5e041-137">Premere hello pulsante hello SensorTag l'associazione.</span><span class="sxs-lookup"><span data-stu-id="5e041-137">Press hello pairing button on hello SensorTag.</span></span> <span data-ttu-id="5e041-138">Hello verde LED sul hello SensorTag lampeggia.</span><span class="sxs-lookup"><span data-stu-id="5e041-138">hello green LED on hello SensorTag flashes.</span></span>
1. <span data-ttu-id="5e041-139">In hello shell Bluetooth, dovrebbe essere hello che sensortag viene trovato.</span><span class="sxs-lookup"><span data-stu-id="5e041-139">At hello Bluetooth shell, you should see hello SensorTag is found.</span></span> <span data-ttu-id="5e041-140">Prendere nota dell'indirizzo MAC di hello SensorTag hello.</span><span class="sxs-lookup"><span data-stu-id="5e041-140">Make a note of hello MAC address of hello SensorTag.</span></span> <span data-ttu-id="5e041-141">In questo esempio, è l'indirizzo MAC di hello SensorTag hello `24:71:89:C0:7F:82`.</span><span class="sxs-lookup"><span data-stu-id="5e041-141">In this example, hello MAC address of hello SensorTag is `24:71:89:C0:7F:82`.</span></span>
1. <span data-ttu-id="5e041-142">Disattiva analisi hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5e041-142">Turn off hello scan by running hello following command:</span></span>

   ```bash
   scan off
   ```

   ![Interrompere l'analisi dei dispositivi Bluetooth circostanti con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-hello-iot-gateway-toohello-sensortag"></a><span data-ttu-id="5e041-144">Avviare una connessione Bluetooth da hello IoT gateway toohello SensorTag</span><span class="sxs-lookup"><span data-stu-id="5e041-144">Initiate a Bluetooth connection from hello IoT gateway toohello SensorTag</span></span>

1. <span data-ttu-id="5e041-145">Connettersi toohello SensorTag eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5e041-145">Connect toohello SensorTag by running hello following command:</span></span>

   ```bash
   connect <MAC address>
   ```

   ![Connettersi toohello SensorTag con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="5e041-147">Disconnettersi hello SensorTag e uscire dalla shell Bluetooth hello eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="5e041-147">Disconnect from hello SensorTag and exit hello Bluetooth shell by running hello following commands:</span></span>

   ```bash
   disconnect
   exit
   ```

   ![Disconnettersi da hello SensorTag con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

<span data-ttu-id="5e041-149">Connessione hello tra hello SensorTag e gateway IoT hello abilitato.</span><span class="sxs-lookup"><span data-stu-id="5e041-149">You've successfully enabled hello connection between hello SensorTag and hello IoT gateway.</span></span>

## <a name="run-a-ble-sample-application-toosend-sensortag-data-tooyour-iot-hub"></a><span data-ttu-id="5e041-150">Eseguire un BILITA esempio applicazione toosend SensorTag dati tooyour hub IoT</span><span class="sxs-lookup"><span data-stu-id="5e041-150">Run a BLE sample application toosend SensorTag data tooyour IoT hub</span></span>

<span data-ttu-id="5e041-151">applicazione di esempio Bluetooth bassa energia (disattiva) Hello viene fornito da Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="5e041-151">hello Bluetooth Low Energy (BLE) sample application is provided by Azure IoT Edge.</span></span> <span data-ttu-id="5e041-152">applicazione di esempio Hello raccoglie i dati dalla connessione attiva e inviare l'hub IoT tooyou dati hello.</span><span class="sxs-lookup"><span data-stu-id="5e041-152">hello sample application collects data from BLE connection and send hello data tooyou IoT hub.</span></span> <span data-ttu-id="5e041-153">applicazione di esempio hello toorun, è necessario:</span><span class="sxs-lookup"><span data-stu-id="5e041-153">toorun hello sample application, you need to:</span></span>

1. <span data-ttu-id="5e041-154">Configurare l'applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="5e041-154">Configure hello sample application.</span></span>
1. <span data-ttu-id="5e041-155">Eseguire l'applicazione di esempio hello gateway IoT hello.</span><span class="sxs-lookup"><span data-stu-id="5e041-155">Run hello sample application on hello IoT gateway.</span></span>

### <a name="configure-hello-sample-application"></a><span data-ttu-id="5e041-156">Configurare l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="5e041-156">Configure hello sample application</span></span>

1. <span data-ttu-id="5e041-157">Consente di passare toohello cartella dell'applicazione di esempio hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5e041-157">Go toohello folder of hello sample application by running hello following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. <span data-ttu-id="5e041-158">Aprire il file di configurazione di hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5e041-158">Open hello configuration file by running hello following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="5e041-159">Nel file di configurazione hello compilare hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="5e041-159">In hello configuration file, fill in hello following values:</span></span>

   <span data-ttu-id="5e041-160">**IoTHubName**: nome hello dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5e041-160">**IoTHubName**: hello name of your IoT hub.</span></span>

   <span data-ttu-id="5e041-161">**IoTHubSuffix**: IoTHubSuffix ottenere dalla chiave primaria di hello come hello dispositivo della stringa di connessione che si è preso nota verso il basso.</span><span class="sxs-lookup"><span data-stu-id="5e041-161">**IoTHubSuffix**: Get IoTHubSuffix from hello primary key of hello device connection string that you noted down.</span></span> <span data-ttu-id="5e041-162">Assicurarsi di ottenere la chiave primaria di hello hello dispositivo della stringa di connessione, non hello chiave primaria della stringa di connessione hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5e041-162">Ensure that you get hello primary key of hello device connection string, not hello primary key of your IoT hub connection string.</span></span> <span data-ttu-id="5e041-163">chiave primaria di Hello della stringa di connessione del dispositivo hello è nel formato hello `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span><span class="sxs-lookup"><span data-stu-id="5e041-163">hello primary key of hello device connection string is in hello format of `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span></span>

   <span data-ttu-id="5e041-164">**Trasporto**: valore predefinito di hello è `amqp`.</span><span class="sxs-lookup"><span data-stu-id="5e041-164">**Transport**: hello default value is `amqp`.</span></span> <span data-ttu-id="5e041-165">Questo valore Mostra protocollo hello durante transpotation.</span><span class="sxs-lookup"><span data-stu-id="5e041-165">This value shows hello protocol during transpotation.</span></span> <span data-ttu-id="5e041-166">Potrebbe essere `http`, `amqp` o `mqtt`.</span><span class="sxs-lookup"><span data-stu-id="5e041-166">It could be `http`, `amqp`, or `mqtt`.</span></span>

   <span data-ttu-id="5e041-167">**macAddress**: hello indirizzo MAC di hello SensorTag annotato verso il basso.</span><span class="sxs-lookup"><span data-stu-id="5e041-167">**macAddress**: hello MAC address of hello SensorTag that you noted down.</span></span>

   <span data-ttu-id="5e041-168">**deviceID**: ID del dispositivo hello creato nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5e041-168">**deviceID**: ID of hello device that you created in your IoT hub.</span></span>

   <span data-ttu-id="5e041-169">**deviceKey**: chiave primaria di hello hello dispositivo della stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="5e041-169">**deviceKey**: hello primary key of hello device connection string.</span></span>

   ![File di configurazione hello completa dell'applicazione di esempio BILITA hello](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. <span data-ttu-id="5e041-171">Premere `ESC` e tipo `:wq` file hello toosave.</span><span class="sxs-lookup"><span data-stu-id="5e041-171">Press `ESC` and type `:wq` toosave hello file.</span></span>

### <a name="run-hello-sample-application"></a><span data-ttu-id="5e041-172">Eseguire l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="5e041-172">Run hello sample application</span></span>

1. <span data-ttu-id="5e041-173">Verificare che hello che sensortag viene acceso.</span><span class="sxs-lookup"><span data-stu-id="5e041-173">Make sure hello SensorTag is powered on.</span></span>
1. <span data-ttu-id="5e041-174">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5e041-174">Run hello following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="5e041-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5e041-175">Next steps</span></span>

[<span data-ttu-id="5e041-176">Usare il gateway IoT per la trasformazione dei dati del sensore con Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="5e041-176">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
