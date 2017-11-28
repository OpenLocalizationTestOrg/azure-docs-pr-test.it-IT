---
title: conversione di aaaData nel gateway IoT con bordo IoT di Azure | Documenti Microsoft
description: Utilizzare IoT gateway tooconvert hello il formato di dati del sensore tramite un modulo personalizzato dal bordo IoT di Azure.
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
ms.openlocfilehash: ae94b1f96f36dfcb4f77fadc0ece3cff3d0bba91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a><span data-ttu-id="dcf3e-104">Usare il gateway IoT per la trasformazione dei dati del sensore con Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="dcf3e-104">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>

> [!NOTE]
> <span data-ttu-id="dcf3e-105">Prima di iniziare questa esercitazione, assicurarsi di che aver completato hello seguente lezioni in sequenza:</span><span class="sxs-lookup"><span data-stu-id="dcf3e-105">Before you start this tutorial, make sure you’ve completed hello following lessons in sequence:</span></span>
> * [<span data-ttu-id="dcf3e-106">Configurare Intel NUC come gateway IoT</span><span class="sxs-lookup"><span data-stu-id="dcf3e-106">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [<span data-ttu-id="dcf3e-107">Utilizzare il cloud IoT gateway tooconnect operazioni toohello - SensorTag tooAzure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="dcf3e-107">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

<span data-ttu-id="dcf3e-108">Un solo scopo di un gateway Iot è tooprocess raccolti dati prima di inviarlo toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="dcf3e-108">One purpose of an Iot gateway is tooprocess collected data before sending it toohello cloud.</span></span> <span data-ttu-id="dcf3e-109">Azure IoT Edge introduce i moduli che possono essere flusso di lavoro creati e assemblati tooform hello l'elaborazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="dcf3e-109">Azure IoT Edge introduces modules which can be created and assembled tooform hello data processing workflow.</span></span> <span data-ttu-id="dcf3e-110">Un modulo riceve un messaggio, esegue un'azione su di esso e quindi spostarla per tooprocess altri moduli.</span><span class="sxs-lookup"><span data-stu-id="dcf3e-110">A module receives a message, performs some action on it, and then move it on for other modules tooprocess.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="dcf3e-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="dcf3e-111">What you learn</span></span>

<span data-ttu-id="dcf3e-112">Viene illustrato come i messaggi toocreate tooconvert un modulo da hello SensorTag in un formato diverso.</span><span class="sxs-lookup"><span data-stu-id="dcf3e-112">You learn how toocreate a module tooconvert messages from hello SensorTag into a different format.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="dcf3e-113">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="dcf3e-113">What you do</span></span>

* <span data-ttu-id="dcf3e-114">Creare un modulo tooconvert un messaggio ricevuto in formato JSON hello.</span><span class="sxs-lookup"><span data-stu-id="dcf3e-114">Create a module tooconvert a received message into hello .json format.</span></span>
* <span data-ttu-id="dcf3e-115">Compilare il modulo di hello.</span><span class="sxs-lookup"><span data-stu-id="dcf3e-115">Compile hello module.</span></span>
* <span data-ttu-id="dcf3e-116">Aggiungere l'applicazione di esempio hello modulo toohello BILITA dal bordo IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="dcf3e-116">Add hello module toohello BLE sample application from Azure IoT Edge.</span></span>
* <span data-ttu-id="dcf3e-117">Eseguire l'applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="dcf3e-117">Run hello sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="dcf3e-118">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="dcf3e-118">What you need</span></span>

* <span data-ttu-id="dcf3e-119">Hello seguenti esercitazioni completate in sequenza:</span><span class="sxs-lookup"><span data-stu-id="dcf3e-119">hello following tutorials completed in sequence:</span></span>
  * [<span data-ttu-id="dcf3e-120">Configurare Intel NUC come gateway IoT</span><span class="sxs-lookup"><span data-stu-id="dcf3e-120">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [<span data-ttu-id="dcf3e-121">Utilizzare il cloud IoT gateway tooconnect operazioni toohello - SensorTag tooAzure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="dcf3e-121">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* <span data-ttu-id="dcf3e-122">Un client SSH in esecuzione nel computer host.</span><span class="sxs-lookup"><span data-stu-id="dcf3e-122">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="dcf3e-123">Si consiglia l'uso di PuTTY in Windows.</span><span class="sxs-lookup"><span data-stu-id="dcf3e-123">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="dcf3e-124">Linux e macOS sono già dotati di un client SSH.</span><span class="sxs-lookup"><span data-stu-id="dcf3e-124">Linux and macOS already come with an SSH client.</span></span>
* <span data-ttu-id="dcf3e-125">indirizzo IP Hello e hello nome utente e password tooaccess hello gateway dal client SSH hello.</span><span class="sxs-lookup"><span data-stu-id="dcf3e-125">hello IP address and hello username and password tooaccess hello gateway from hello SSH client.</span></span>
* <span data-ttu-id="dcf3e-126">Una connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="dcf3e-126">An Internet connection.</span></span>

## <a name="create-a-module"></a><span data-ttu-id="dcf3e-127">Creare un modulo</span><span class="sxs-lookup"><span data-stu-id="dcf3e-127">Create a module</span></span>

1. <span data-ttu-id="dcf3e-128">Nel computer host hello, eseguire client SSH hello e toohello IoT gateway di connessione.</span><span class="sxs-lookup"><span data-stu-id="dcf3e-128">On hello host computer, run hello SSH client and connect toohello IoT gateway.</span></span>
1. <span data-ttu-id="dcf3e-129">Clonare il file di origine hello del modulo di conversione hello da GitHub toohello home directory di gateway IoT hello eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="dcf3e-129">Clone hello source files of hello conversion module from GitHub toohello home directory of hello IoT gateway by running hello following commands:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   <span data-ttu-id="dcf3e-130">Si tratta di un modulo di Azure Edge nativo scritto in linguaggio di programmazione C hello.</span><span class="sxs-lookup"><span data-stu-id="dcf3e-130">This is a native Azure Edge module written in hello C programming language.</span></span> <span data-ttu-id="dcf3e-131">modulo Hello converte formato hello di messaggi ricevuti in hello uno seguenti:</span><span class="sxs-lookup"><span data-stu-id="dcf3e-131">hello module converts hello format of received messages into hello following one:</span></span>

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-hello-module"></a><span data-ttu-id="dcf3e-132">Compilare il modulo hello</span><span class="sxs-lookup"><span data-stu-id="dcf3e-132">Compile hello module</span></span>

<span data-ttu-id="dcf3e-133">modulo hello toocompile, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="dcf3e-133">toocompile hello module, run hello following commands:</span></span>

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change hello build script runnable
chmod 777 build.sh
# remove hello invalid windows character
sed -i -e "s/\r$//" build.sh
# run hello build shell script
./build.sh
```

<span data-ttu-id="dcf3e-134">Ottenere un `libmy_module.so` file dopo aver completata la compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="dcf3e-134">You get a `libmy_module.so` file after hello compile is completed.</span></span> <span data-ttu-id="dcf3e-135">Prendere nota del percorso assoluto di hello di questo file.</span><span class="sxs-lookup"><span data-stu-id="dcf3e-135">Make a note of hello absolute path of this file.</span></span>

## <a name="add-hello-module-toohello-ble-sample-application"></a><span data-ttu-id="dcf3e-136">Aggiungere l'applicazione di esempio BILITA toohello hello modulo</span><span class="sxs-lookup"><span data-stu-id="dcf3e-136">Add hello module toohello BLE sample application</span></span>

1. <span data-ttu-id="dcf3e-137">Cartella di esempi di passare toohello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="dcf3e-137">Go toohello samples folder by running hello following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. <span data-ttu-id="dcf3e-138">Aprire il file di configurazione di hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="dcf3e-138">Open hello configuration file by running hello following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="dcf3e-139">Aggiungere un modulo inserendo hello seguente codice toohello `modules` sezione.</span><span class="sxs-lookup"><span data-stu-id="dcf3e-139">Add a module by inserting hello following code toohello `modules` section.</span></span>

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

1. <span data-ttu-id="dcf3e-140">Sostituire `[Your libmy_module.so path]` nel codice hello con percorso assoluto di hello del libmy_module.so hello' file.</span><span class="sxs-lookup"><span data-stu-id="dcf3e-140">Replace `[Your libmy_module.so path]` in hello code with hello absolute path of hello libmy_module.so\` file.</span></span>
1. <span data-ttu-id="dcf3e-141">Sostituire il codice hello in hello `links` sezione con hello uno seguenti:</span><span class="sxs-lookup"><span data-stu-id="dcf3e-141">Replace hello code in hello `links` section with hello following one:</span></span>

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

1. <span data-ttu-id="dcf3e-142">Premere `ESC`, quindi digitare `:wq` file hello toosave.</span><span class="sxs-lookup"><span data-stu-id="dcf3e-142">Press `ESC`, and then type `:wq` toosave hello file.</span></span>

## <a name="run-hello-sample-application"></a><span data-ttu-id="dcf3e-143">Eseguire l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="dcf3e-143">Run hello sample application</span></span>

1. <span data-ttu-id="dcf3e-144">Accensione hello SensorTag.</span><span class="sxs-lookup"><span data-stu-id="dcf3e-144">Power on hello SensorTag.</span></span>
1. <span data-ttu-id="dcf3e-145">Impostare una variabile di ambiente SSL_CERT_FILE hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="dcf3e-145">Set hello SSL_CERT_FILE environment variable by running hello following command:</span></span>

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. <span data-ttu-id="dcf3e-146">Eseguire l'applicazione di esempio hello con modulo aggiunto hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="dcf3e-146">Run hello sample application with hello added module by running hello following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="dcf3e-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dcf3e-147">Next steps</span></span>

<span data-ttu-id="dcf3e-148">Hai correttamente utilizzare hello IoT gateway tooconvert messaggio hello da SensorTag in formato JSON hello.</span><span class="sxs-lookup"><span data-stu-id="dcf3e-148">You’ve successfully use hello IoT gateway tooconvert hello message from SensorTag into hello .json format.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
