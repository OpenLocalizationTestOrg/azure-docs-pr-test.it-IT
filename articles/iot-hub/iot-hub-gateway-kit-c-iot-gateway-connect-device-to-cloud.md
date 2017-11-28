---
title: Usare un gateway IoT per connettere un dispositivo all'hub IoT di Azure | Microsoft Docs
description: Informazioni su come usare Intel NUC come gateway IoT per connettere un SensorTag TI e inviare i dati del sensore all'hub IoT di Azure nel cloud.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: connessione del dispositivo al cloud tramite gateway IoT
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 4fb77ed0241d15338c2574fd22828507c3e40cb3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-iot-gateway-to-connect-things-to-the-cloud---sensortag-to-azure-iot-hub"></a><span data-ttu-id="3d47c-104">Usare il gateway IoT per connettere oggetti al cloud: SensorTag ad Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="3d47c-104">Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub</span></span>

> [!NOTE]
> <span data-ttu-id="3d47c-105">Prima di iniziare questa esercitazione, assicurarsi di aver completato [Configurare Intel NUC come gateway IoT di Azure](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span><span class="sxs-lookup"><span data-stu-id="3d47c-105">Before you start this tutorial, make sure you’ve completed [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span></span> <span data-ttu-id="3d47c-106">In [Configurare Intel NUC come gateway IoT di Azure](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) si configura il dispositivo Intel NUC come gateway IoT.</span><span class="sxs-lookup"><span data-stu-id="3d47c-106">In [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), you set up the Intel NUC device as an IoT gateway.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3d47c-107">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="3d47c-107">What you will learn</span></span>

<span data-ttu-id="3d47c-108">Informazioni su come usare un gateway IoT per connettere un SensorTag di Texas Instruments (CC2650STK) ad Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3d47c-108">You learn how to use an IoT gateway to connect a Texas Instruments SensorTag (CC2650STK) to Azure IoT Hub.</span></span> <span data-ttu-id="3d47c-109">Il gateway IoT invia dati di temperatura e umidità raccolti dal SensorTag ad Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3d47c-109">The IoT gateway sends temperature and humidity data collected from the SensorTag to Azure IoT Hub.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="3d47c-110">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="3d47c-110">What you will do</span></span>

- <span data-ttu-id="3d47c-111">Creare un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3d47c-111">Create an IoT hub.</span></span>
- <span data-ttu-id="3d47c-112">Registrare un dispositivo nell'hub IoT per SensorTag.</span><span class="sxs-lookup"><span data-stu-id="3d47c-112">Register a device in the IoT hub for the SensorTag.</span></span>
- <span data-ttu-id="3d47c-113">Abilitare la connessione tra il gateway IoT e il SensorTag.</span><span class="sxs-lookup"><span data-stu-id="3d47c-113">Enable the connection between the IoT gateway and the SensorTag.</span></span>
- <span data-ttu-id="3d47c-114">Eseguire un'applicazione di esempio BLE per inviare i dati del sensore SensorTag all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3d47c-114">Run a BLE sample application to send SensorTag data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3d47c-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="3d47c-115">What you need</span></span>

- <span data-ttu-id="3d47c-116">Completare l'esercitazione [Configurare Intel NUC come gateway IoT di Azure](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) in cui si configura il dispositivo Intel NUC come gateway IoT.</span><span class="sxs-lookup"><span data-stu-id="3d47c-116">Tutorial [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) completed in which you set up Intel NUC as an IoT gateway.</span></span>
- * <span data-ttu-id="3d47c-117">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="3d47c-117">An active Azure subscription.</span></span> <span data-ttu-id="3d47c-118">Se non si ha un account Azure, [creare un account Azure gratuito](https://azure.microsoft.com/free/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="3d47c-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
- <span data-ttu-id="3d47c-119">Un client SSH in esecuzione nel computer host.</span><span class="sxs-lookup"><span data-stu-id="3d47c-119">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="3d47c-120">Si consiglia l'uso di PuTTY in Windows.</span><span class="sxs-lookup"><span data-stu-id="3d47c-120">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="3d47c-121">Linux e macOS sono già dotati di un client SSH.</span><span class="sxs-lookup"><span data-stu-id="3d47c-121">Linux and macOS already come with an SSH client.</span></span>
- <span data-ttu-id="3d47c-122">L'indirizzo IP, il nome utente e la password per accedere al gateway dal client SSH.</span><span class="sxs-lookup"><span data-stu-id="3d47c-122">The IP address and the username and password to access the gateway from the SSH client.</span></span>
- <span data-ttu-id="3d47c-123">Una connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="3d47c-123">An Internet connection.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> <span data-ttu-id="3d47c-124">Qui è possibile registrare questo nuovo dispositivo per SensorTag</span><span class="sxs-lookup"><span data-stu-id="3d47c-124">Here you register this new device for your SensorTag</span></span>

## <a name="enable-the-connection-between-the-iot-gateway-and-the-sensortag"></a><span data-ttu-id="3d47c-125">Abilitare la connessione tra il gateway IoT e SensorTag</span><span class="sxs-lookup"><span data-stu-id="3d47c-125">Enable the connection between the IoT gateway and the SensorTag</span></span>

<span data-ttu-id="3d47c-126">In questa sezione vengono eseguite le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="3d47c-126">In this section, you perform the following tasks:</span></span>

- <span data-ttu-id="3d47c-127">Ottenere l'indirizzo MAC di SensorTag per la connessione Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="3d47c-127">Get the MAC address of the SensorTag for Bluetooth connection.</span></span>
- <span data-ttu-id="3d47c-128">Avviare una connessione Bluetooth dal gateway IoT per SensorTag.</span><span class="sxs-lookup"><span data-stu-id="3d47c-128">Initiate a Bluetooth connection from the IoT gateway to the SensorTag.</span></span>

### <a name="get-the-mac-address-of-the-sensortag-for-bluetooth-connection"></a><span data-ttu-id="3d47c-129">Ottenere l'indirizzo MAC di SensorTag per la connessione Bluetooth</span><span class="sxs-lookup"><span data-stu-id="3d47c-129">Get the MAC address of the SensorTag for Bluetooth connection</span></span>

1. <span data-ttu-id="3d47c-130">Nel computer host eseguire il client SSH e connettersi al gateway IoT.</span><span class="sxs-lookup"><span data-stu-id="3d47c-130">On the host computer, run the SSH client and connect to the IoT gateway.</span></span>
1. <span data-ttu-id="3d47c-131">Sbloccare il Bluetooth eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3d47c-131">Unblock Bluetooth by running the following command:</span></span>

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. <span data-ttu-id="3d47c-132">Avviare il servizio Bluetooth sul gateway IoT e immettere una shell Bluetooth per configurare il Bluetooth eseguendo i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3d47c-132">Start the Bluetooth service on the IoT gateway and enter a Bluetooth shell to configure Bluetooth by running the following commands:</span></span>

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. <span data-ttu-id="3d47c-133">Accendere il controller Bluetooth eseguendo il comando seguente nella shell del Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="3d47c-133">Power on the Bluetooth controller by running the following command at the Bluetooth shell:</span></span>

   ```bash
   power on
   ```

   ![accendere il controller Bluetooth sul gateway IoT con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="3d47c-135">Avviare l'analisi per dispositivi Bluetooth circostanti eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3d47c-135">Start scanning for nearby Bluetooth devices by running the following command:</span></span>

   ```bash
   scan on
   ```

   ![Analizzare i dispositivi Bluetooth citcostanti con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="3d47c-137">Premere il pulsante di associazione su SensorTag.</span><span class="sxs-lookup"><span data-stu-id="3d47c-137">Press the pairing button on the SensorTag.</span></span> <span data-ttu-id="3d47c-138">Il LED verde su SensorTag lampeggia.</span><span class="sxs-lookup"><span data-stu-id="3d47c-138">The green LED on the SensorTag flashes.</span></span>
1. <span data-ttu-id="3d47c-139">Nella shell del Bluetooth viene visualizzato il SensorTag rilevato.</span><span class="sxs-lookup"><span data-stu-id="3d47c-139">At the Bluetooth shell, you should see the SensorTag is found.</span></span> <span data-ttu-id="3d47c-140">Prendere nota dell'indirizzo MAC di SensorTag.</span><span class="sxs-lookup"><span data-stu-id="3d47c-140">Make a note of the MAC address of the SensorTag.</span></span> <span data-ttu-id="3d47c-141">In questo esempio l'indirizzo MAC di SensorTag è `24:71:89:C0:7F:82`.</span><span class="sxs-lookup"><span data-stu-id="3d47c-141">In this example, the MAC address of the SensorTag is `24:71:89:C0:7F:82`.</span></span>
1. <span data-ttu-id="3d47c-142">Arrestare l'analisi eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3d47c-142">Turn off the scan by running the following command:</span></span>

   ```bash
   scan off
   ```

   ![Interrompere l'analisi dei dispositivi Bluetooth circostanti con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-the-iot-gateway-to-the-sensortag"></a><span data-ttu-id="3d47c-144">Avviare una connessione Bluetooth dal gateway IoT per SensorTag</span><span class="sxs-lookup"><span data-stu-id="3d47c-144">Initiate a Bluetooth connection from the IoT gateway to the SensorTag</span></span>

1. <span data-ttu-id="3d47c-145">Connettersi a SensorTag eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3d47c-145">Connect to the SensorTag by running the following command:</span></span>

   ```bash
   connect <MAC address>
   ```

   ![Connettersi a SensorTag con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="3d47c-147">Disconnettersi da SensorTag e chiudere la shell del Bluetooth eseguendo i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3d47c-147">Disconnect from the SensorTag and exit the Bluetooth shell by running the following commands:</span></span>

   ```bash
   disconnect
   exit
   ```

   ![Disconnettersi da SensorTag con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

<span data-ttu-id="3d47c-149">La connessione tra il gateway IoT e SensorTag è stata abilitata correttamente.</span><span class="sxs-lookup"><span data-stu-id="3d47c-149">You've successfully enabled the connection between the SensorTag and the IoT gateway.</span></span>

## <a name="run-a-ble-sample-application-to-send-sensortag-data-to-your-iot-hub"></a><span data-ttu-id="3d47c-150">Eseguire un'applicazione di esempio BLE per inviare i dati del sensore SensorTag all'hub IoT</span><span class="sxs-lookup"><span data-stu-id="3d47c-150">Run a BLE sample application to send SensorTag data to your IoT hub</span></span>

<span data-ttu-id="3d47c-151">L'applicazione di esempio Bluetooth Low Energy (BLE) viene offerta da Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="3d47c-151">The Bluetooth Low Energy (BLE) sample application is provided by Azure IoT Edge.</span></span> <span data-ttu-id="3d47c-152">L'applicazione di esempio raccoglie i dati dalla connessione BLE e li invia all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3d47c-152">The sample application collects data from BLE connection and send the data to you IoT hub.</span></span> <span data-ttu-id="3d47c-153">Per eseguire l'applicazione di esempio è necessario:</span><span class="sxs-lookup"><span data-stu-id="3d47c-153">To run the sample application, you need to:</span></span>

1. <span data-ttu-id="3d47c-154">Configurare l'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="3d47c-154">Configure the sample application.</span></span>
1. <span data-ttu-id="3d47c-155">Eseguire l'applicazione di esempio nel gateway IoT.</span><span class="sxs-lookup"><span data-stu-id="3d47c-155">Run the sample application on the IoT gateway.</span></span>

### <a name="configure-the-sample-application"></a><span data-ttu-id="3d47c-156">Configurare l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="3d47c-156">Configure the sample application</span></span>

1. <span data-ttu-id="3d47c-157">Passare alla cartella dell'applicazione di esempio eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3d47c-157">Go to the folder of the sample application by running the following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. <span data-ttu-id="3d47c-158">Aprire il file di configurazione usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3d47c-158">Open the configuration file by running the following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="3d47c-159">Nel file di configurazione, inserire i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="3d47c-159">In the configuration file, fill in the following values:</span></span>

   <span data-ttu-id="3d47c-160">**IoTHubName**: il nome dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3d47c-160">**IoTHubName**: The name of your IoT hub.</span></span>

   <span data-ttu-id="3d47c-161">**IoTHubSuffix**: ottenere IoTHubSuffix dalla chiave primaria della stringa di connessione del dispositivo di cui si è preso nota.</span><span class="sxs-lookup"><span data-stu-id="3d47c-161">**IoTHubSuffix**: Get IoTHubSuffix from the primary key of the device connection string that you noted down.</span></span> <span data-ttu-id="3d47c-162">Assicurarsi di ottenere la chiave primaria della stringa di connessione del dispositivo, non la chiave primaria della stringa di connessione dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3d47c-162">Ensure that you get the primary key of the device connection string, not the primary key of your IoT hub connection string.</span></span> <span data-ttu-id="3d47c-163">La chiave primaria della stringa di connessione del dispositivo ha il formato `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span><span class="sxs-lookup"><span data-stu-id="3d47c-163">The primary key of the device connection string is in the format of `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span></span>

   <span data-ttu-id="3d47c-164">**Transport**: il valore predefinito è `amqp`.</span><span class="sxs-lookup"><span data-stu-id="3d47c-164">**Transport**: The default value is `amqp`.</span></span> <span data-ttu-id="3d47c-165">Questo valore mostra il protocollo durante il trasporto.</span><span class="sxs-lookup"><span data-stu-id="3d47c-165">This value shows the protocol during transpotation.</span></span> <span data-ttu-id="3d47c-166">Potrebbe essere `http`, `amqp` o `mqtt`.</span><span class="sxs-lookup"><span data-stu-id="3d47c-166">It could be `http`, `amqp`, or `mqtt`.</span></span>

   <span data-ttu-id="3d47c-167">**macAddress**: l'indirizzo MAC di SensorTag di cui si è preso nota.</span><span class="sxs-lookup"><span data-stu-id="3d47c-167">**macAddress**: The MAC address of the SensorTag that you noted down.</span></span>

   <span data-ttu-id="3d47c-168">**deviceID**: ID del dispositivo creato nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3d47c-168">**deviceID**: ID of the device that you created in your IoT hub.</span></span>

   <span data-ttu-id="3d47c-169">**deviceKey**: la chiave primaria della stringa di connessione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3d47c-169">**deviceKey**: The primary key of the device connection string.</span></span>

   ![Completare il file di configurazione dell'applicazione di esempio BLE](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. <span data-ttu-id="3d47c-171">Premere `ESC` e digitare `:wq` per salvare il file.</span><span class="sxs-lookup"><span data-stu-id="3d47c-171">Press `ESC` and type `:wq` to save the file.</span></span>

### <a name="run-the-sample-application"></a><span data-ttu-id="3d47c-172">Eseguire l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="3d47c-172">Run the sample application</span></span>

1. <span data-ttu-id="3d47c-173">Assicurarsi che SensorTag sia acceso.</span><span class="sxs-lookup"><span data-stu-id="3d47c-173">Make sure the SensorTag is powered on.</span></span>
1. <span data-ttu-id="3d47c-174">Eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3d47c-174">Run the following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="3d47c-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3d47c-175">Next steps</span></span>

[<span data-ttu-id="3d47c-176">Usare il gateway IoT per la trasformazione dei dati del sensore con Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="3d47c-176">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
