---
title: Conversione di dati nel gateway IoT con Azure IoT Edge | Microsoft Docs
description: Usare il gateway IoT per convertire il formato dei dati del sensore tramite un modulo personalizzato di Azure IoT Edge.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: conversione dei dati del gateway iot, trasformazione dei dati del gateway iot
ms.assetid: 75f2573d-500b-4405-bff7-61021c4c3500
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: d5c735a4adbc59e9526ec4fd40720c5ec136d63d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a><span data-ttu-id="eee6b-104">Usare il gateway IoT per la trasformazione dei dati del sensore con Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="eee6b-104">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>

> [!NOTE]
> <span data-ttu-id="eee6b-105">Prima di iniziare questa esercitazione, assicurarsi di aver completato le lezioni seguenti in sequenza:</span><span class="sxs-lookup"><span data-stu-id="eee6b-105">Before you start this tutorial, make sure you’ve completed the following lessons in sequence:</span></span>
> * [<span data-ttu-id="eee6b-106">Configurare Intel NUC come gateway IoT</span><span class="sxs-lookup"><span data-stu-id="eee6b-106">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * <span data-ttu-id="eee6b-107">[Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md) (Usare il gateway IoT per connettere oggetti al cloud - SensorTag ad Azure IoT Hub)</span><span class="sxs-lookup"><span data-stu-id="eee6b-107">[Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)</span></span>

<span data-ttu-id="eee6b-108">Uno degli scopi di un gateway IoT consiste nell'elaborare i dati raccolti prima di inviarli al cloud.</span><span class="sxs-lookup"><span data-stu-id="eee6b-108">One purpose of an Iot gateway is to process collected data before sending it to the cloud.</span></span> <span data-ttu-id="eee6b-109">Azure IoT Edge introduce una serie di moduli che possono essere creati e assemblati per formare il flusso di lavoro dell'elaborazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="eee6b-109">Azure IoT Edge introduces modules which can be created and assembled to form the data processing workflow.</span></span> <span data-ttu-id="eee6b-110">Un modulo riceve un messaggio, esegue un'azione su di esso e quindi lo passa ad altri moduli per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="eee6b-110">A module receives a message, performs some action on it, and then move it on for other modules to process.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="eee6b-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="eee6b-111">What you learn</span></span>

<span data-ttu-id="eee6b-112">Informazioni su come creare un modulo per convertire i messaggi del SensorTag in un formato diverso.</span><span class="sxs-lookup"><span data-stu-id="eee6b-112">You learn how to create a module to convert messages from the SensorTag into a different format.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="eee6b-113">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="eee6b-113">What you do</span></span>

* <span data-ttu-id="eee6b-114">Creare un modulo per convertire nel formato JSON un messaggio ricevuto.</span><span class="sxs-lookup"><span data-stu-id="eee6b-114">Create a module to convert a received message into the .json format.</span></span>
* <span data-ttu-id="eee6b-115">Compilare il modulo.</span><span class="sxs-lookup"><span data-stu-id="eee6b-115">Compile the module.</span></span>
* <span data-ttu-id="eee6b-116">Aggiungere il modulo all'applicazione di esempio BLE da Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="eee6b-116">Add the module to the BLE sample application from Azure IoT Edge.</span></span>
* <span data-ttu-id="eee6b-117">Eseguire l'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="eee6b-117">Run the sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="eee6b-118">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="eee6b-118">What you need</span></span>

* <span data-ttu-id="eee6b-119">Le esercitazioni seguenti completate in sequenza:</span><span class="sxs-lookup"><span data-stu-id="eee6b-119">The following tutorials completed in sequence:</span></span>
  * [<span data-ttu-id="eee6b-120">Configurare Intel NUC come gateway IoT</span><span class="sxs-lookup"><span data-stu-id="eee6b-120">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * <span data-ttu-id="eee6b-121">[Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md) (Usare il gateway IoT per connettere oggetti al cloud - SensorTag ad Azure IoT Hub)</span><span class="sxs-lookup"><span data-stu-id="eee6b-121">[Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)</span></span>
* <span data-ttu-id="eee6b-122">Un client SSH in esecuzione nel computer host.</span><span class="sxs-lookup"><span data-stu-id="eee6b-122">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="eee6b-123">Si consiglia l'uso di PuTTY in Windows.</span><span class="sxs-lookup"><span data-stu-id="eee6b-123">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="eee6b-124">Linux e macOS sono già dotati di un client SSH.</span><span class="sxs-lookup"><span data-stu-id="eee6b-124">Linux and macOS already come with an SSH client.</span></span>
* <span data-ttu-id="eee6b-125">L'indirizzo IP, il nome utente e la password per accedere al gateway dal client SSH.</span><span class="sxs-lookup"><span data-stu-id="eee6b-125">The IP address and the username and password to access the gateway from the SSH client.</span></span>
* <span data-ttu-id="eee6b-126">Una connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="eee6b-126">An Internet connection.</span></span>

## <a name="create-a-module"></a><span data-ttu-id="eee6b-127">Creare un modulo</span><span class="sxs-lookup"><span data-stu-id="eee6b-127">Create a module</span></span>

1. <span data-ttu-id="eee6b-128">Nel computer host eseguire il client SSH e connettersi al gateway IoT.</span><span class="sxs-lookup"><span data-stu-id="eee6b-128">On the host computer, run the SSH client and connect to the IoT gateway.</span></span>
1. <span data-ttu-id="eee6b-129">Clonare i file di origine del modulo di conversione da GitHub nella home directory del gateway IoT eseguendo i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="eee6b-129">Clone the source files of the conversion module from GitHub to the home directory of the IoT gateway by running the following commands:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   <span data-ttu-id="eee6b-130">Questo è un modulo di Azure Edge nativo scritto nel linguaggio di programmazione C.</span><span class="sxs-lookup"><span data-stu-id="eee6b-130">This is a native Azure Edge module written in the C programming language.</span></span> <span data-ttu-id="eee6b-131">Il modulo converte il formato dei messaggi ricevuti nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="eee6b-131">The module converts the format of received messages into the following one:</span></span>

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-the-module"></a><span data-ttu-id="eee6b-132">Compilare il modulo</span><span class="sxs-lookup"><span data-stu-id="eee6b-132">Compile the module</span></span>

<span data-ttu-id="eee6b-133">Per compilare il modulo, eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="eee6b-133">To compile the module, run the following commands:</span></span>

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change the build script runnable
chmod 777 build.sh
# remove the invalid windows character
sed -i -e "s/\r$//" build.sh
# run the build shell script
./build.sh
```

<span data-ttu-id="eee6b-134">Al termine della compilazione, viene creato un file `libmy_module.so`.</span><span class="sxs-lookup"><span data-stu-id="eee6b-134">You get a `libmy_module.so` file after the compile is completed.</span></span> <span data-ttu-id="eee6b-135">Prendere nota del percorso assoluto del file.</span><span class="sxs-lookup"><span data-stu-id="eee6b-135">Make a note of the absolute path of this file.</span></span>

## <a name="add-the-module-to-the-ble-sample-application"></a><span data-ttu-id="eee6b-136">Aggiungere il modulo all'applicazione di esempio BLE</span><span class="sxs-lookup"><span data-stu-id="eee6b-136">Add the module to the BLE sample application</span></span>

1. <span data-ttu-id="eee6b-137">Passare alla cartella degli esempi usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="eee6b-137">Go to the samples folder by running the following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. <span data-ttu-id="eee6b-138">Aprire il file di configurazione usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="eee6b-138">Open the configuration file by running the following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="eee6b-139">Aggiungere un modulo inserendo il codice seguente nella sezione `modules`.</span><span class="sxs-lookup"><span data-stu-id="eee6b-139">Add a module by inserting the following code to the `modules` section.</span></span>

   ```json
   {
       "name": "MyModule",
       "loader": {
           "name": "native",
           "entrypoint":{
               "module.path": "[Your libmy_module.so path]"
               }
            },
        "args": null
    },
    ```

1. <span data-ttu-id="eee6b-140">Sostituire `[Your libmy_module.so path]` nel codice con il percorso assoluto del file libmy_module.so.</span><span class="sxs-lookup"><span data-stu-id="eee6b-140">Replace `[Your libmy_module.so path]` in the code with the absolute path of the libmy_module.so\` file.</span></span>
1. <span data-ttu-id="eee6b-141">Sostituire il codice nella sezione `links` con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="eee6b-141">Replace the code in the `links` section with the following one:</span></span>

   ```json
   {
       "source": "SensorTag",
       "sink": "MyModule"
   },
   {
       "source": "MyModule",
       "sink": "mapping"
   }
   ```

1. <span data-ttu-id="eee6b-142">Premere `ESC` e quindi digitare `:wq` per salvare il file.</span><span class="sxs-lookup"><span data-stu-id="eee6b-142">Press `ESC`, and then type `:wq` to save the file.</span></span>

## <a name="run-the-sample-application"></a><span data-ttu-id="eee6b-143">Eseguire l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="eee6b-143">Run the sample application</span></span>

1. <span data-ttu-id="eee6b-144">Accendere il SensorTag.</span><span class="sxs-lookup"><span data-stu-id="eee6b-144">Power on the SensorTag.</span></span>
1. <span data-ttu-id="eee6b-145">Impostare la variabile di ambiente SSL_CERT_FILE usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="eee6b-145">Set the SSL_CERT_FILE environment variable by running the following command:</span></span>

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. <span data-ttu-id="eee6b-146">Eseguire l'applicazione di esempio con il modulo aggiunto usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="eee6b-146">Run the sample application with the added module by running the following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="eee6b-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eee6b-147">Next steps</span></span>

<span data-ttu-id="eee6b-148">È stato usato il gateway IoT per convertire il messaggio dal SensorTag nel formato JSON.</span><span class="sxs-lookup"><span data-stu-id="eee6b-148">You’ve successfully use the IoT gateway to convert the message from SensorTag into the .json format.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
