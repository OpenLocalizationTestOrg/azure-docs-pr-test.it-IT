---
title: aaaConnect un dispositivo utilizzando C in Linux | Documenti Microsoft
description: Viene descritto come tooconnect toohello un dispositivo Azure IoT Suite preconfigurato soluzione di monitoraggio remoto utilizzando un'applicazione scritta in C in esecuzione in Linux.
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0c7c8039-0bbf-4bb5-9e79-ed8cff433629
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57393817d40d3555177956a01fa71058bc256988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-linux"></a><span data-ttu-id="b47dc-103">Connettersi toohello il dispositivo remoto monitoraggio soluzione preconfigurata (Linux)</span><span class="sxs-lookup"><span data-stu-id="b47dc-103">Connect your device toohello remote monitoring preconfigured solution (Linux)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a><span data-ttu-id="b47dc-104">Compilare ed eseguire un client C Linux di esempio</span><span class="sxs-lookup"><span data-stu-id="b47dc-104">Build and run a sample C client Linux</span></span>
<span data-ttu-id="b47dc-105">Hello alla procedura seguente viene illustrato come un'applicazione client che comunica con il monitoraggio remoto hello toocreate preconfigurato soluzione.</span><span class="sxs-lookup"><span data-stu-id="b47dc-105">hello following steps show you how toocreate a client application that communicates with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="b47dc-106">Questa applicazione è scritta in C e compilata ed eseguita in Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="b47dc-106">This application is written in C and built and run on Ubuntu Linux.</span></span>

<span data-ttu-id="b47dc-107">toocomplete questi passaggi, è necessario un dispositivo che esegue Ubuntu 15.04 o 15.10 versione.</span><span class="sxs-lookup"><span data-stu-id="b47dc-107">toocomplete these steps, you need a device running Ubuntu version 15.04 or 15.10.</span></span> <span data-ttu-id="b47dc-108">Prima di continuare, installare i pacchetti dei prerequisiti hello nel dispositivo Ubuntu utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b47dc-108">Before proceeding, install hello prerequisite packages on your Ubuntu device using hello following command:</span></span>

```
sudo apt-get install cmake gcc g++
```

## <a name="install-hello-client-libraries-on-your-device"></a><span data-ttu-id="b47dc-109">Installare le librerie client hello sul dispositivo</span><span class="sxs-lookup"><span data-stu-id="b47dc-109">Install hello client libraries on your device</span></span>
<span data-ttu-id="b47dc-110">Hello Azure IoT Hub librerie client sono disponibili come un pacchetto è possibile installare nel dispositivo Ubuntu utilizzando hello **apt get** comando.</span><span class="sxs-lookup"><span data-stu-id="b47dc-110">hello Azure IoT Hub client libraries are available as a package you can install on your Ubuntu device using hello **apt-get** command.</span></span> <span data-ttu-id="b47dc-111">Completare i seguenti passaggi tooinstall hello pacchetto hello libreria client IoT Hub e il file di intestazione nel computer in uso Ubuntu hello:</span><span class="sxs-lookup"><span data-stu-id="b47dc-111">Complete hello following steps tooinstall hello package that contains hello IoT Hub client library and header files on your Ubuntu computer:</span></span>

1. <span data-ttu-id="b47dc-112">In una shell, aggiungere hello AzureIoT repository tooyour computer:</span><span class="sxs-lookup"><span data-stu-id="b47dc-112">In a shell, add hello AzureIoT repository tooyour computer:</span></span>
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. <span data-ttu-id="b47dc-113">Installare il pacchetto di azure-iot-sdk-c-dev hello</span><span class="sxs-lookup"><span data-stu-id="b47dc-113">Install hello azure-iot-sdk-c-dev package</span></span>
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-hello-parson-json-parser"></a><span data-ttu-id="b47dc-114">Installare hello parser Parson JSON</span><span class="sxs-lookup"><span data-stu-id="b47dc-114">Install hello Parson JSON parser</span></span>
<span data-ttu-id="b47dc-115">utilizzano le librerie client di IoT Hub Hello hello payload dei messaggi Parson JSON parser tooparse.</span><span class="sxs-lookup"><span data-stu-id="b47dc-115">hello IoT Hub client libraries use hello Parson JSON parser tooparse message payloads.</span></span> <span data-ttu-id="b47dc-116">In una cartella appropriata nel computer in uso, clonare il repository di GitHub Parson hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b47dc-116">In a suitable folder on your computer, clone hello Parson GitHub repository using hello following command:</span></span>

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a><span data-ttu-id="b47dc-117">Preparare il progetto</span><span class="sxs-lookup"><span data-stu-id="b47dc-117">Prepare your project</span></span>
<span data-ttu-id="b47dc-118">Nel computer Ubuntu creare una cartella denominata **remote\_monitoring**.</span><span class="sxs-lookup"><span data-stu-id="b47dc-118">On your Ubuntu machine, create a folder called **remote\_monitoring**.</span></span> <span data-ttu-id="b47dc-119">In hello **remoto\_monitoraggio** cartella:</span><span class="sxs-lookup"><span data-stu-id="b47dc-119">In hello **remote\_monitoring** folder:</span></span>

- <span data-ttu-id="b47dc-120">Creare quattro file di hello **Main. c**, **remoto\_monitoring.c**, **remoto\_monitoring.h**, e **CMakeLists.txt**.</span><span class="sxs-lookup"><span data-stu-id="b47dc-120">Create hello four files **main.c**, **remote\_monitoring.c**, **remote\_monitoring.h**, and **CMakeLists.txt**.</span></span>
- <span data-ttu-id="b47dc-121">Creare una cartella denominata **parson**.</span><span class="sxs-lookup"><span data-stu-id="b47dc-121">Create folder called **parson**.</span></span>

<span data-ttu-id="b47dc-122">Copiare i file hello **parson.c** e **parson.h** dalla copia locale del repository Parson hello in hello **remoto\_/parson monitoraggio** cartella.</span><span class="sxs-lookup"><span data-stu-id="b47dc-122">Copy hello files **parson.c** and **parson.h** from your local copy of hello Parson repository into hello **remote\_monitoring/parson** folder.</span></span>

<span data-ttu-id="b47dc-123">In un editor di testo aprire hello **remoto\_monitoring.c** file.</span><span class="sxs-lookup"><span data-stu-id="b47dc-123">In a text editor, open hello **remote\_monitoring.c** file.</span></span> <span data-ttu-id="b47dc-124">Aggiungere il seguente hello `#include` istruzioni:</span><span class="sxs-lookup"><span data-stu-id="b47dc-124">Add hello following `#include` statements:</span></span>
   
```
#include "iothubtransportmqtt.h"
#include "schemalib.h"
#include "iothub_client.h"
#include "serializer_devicetwin.h"
#include "schemaserializer.h"
#include "azure_c_shared_utility/threadapi.h"
#include "azure_c_shared_utility/platform.h"
#include "parson.h"
```

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="call-hello-remotemonitoringrun-function"></a><span data-ttu-id="b47dc-125">Chiamare hello remoto\_monitoraggio\_eseguire (funzione)</span><span class="sxs-lookup"><span data-stu-id="b47dc-125">Call hello remote\_monitoring\_run function</span></span>
<span data-ttu-id="b47dc-126">In un editor di testo aprire hello **remote_monitoring.h** file.</span><span class="sxs-lookup"><span data-stu-id="b47dc-126">In a text editor, open hello **remote_monitoring.h** file.</span></span> <span data-ttu-id="b47dc-127">Aggiungere hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="b47dc-127">Add hello following code:</span></span>

```
void remote_monitoring_run(void);
```

<span data-ttu-id="b47dc-128">In un editor di testo aprire hello **Main. c** file.</span><span class="sxs-lookup"><span data-stu-id="b47dc-128">In a text editor, open hello **main.c** file.</span></span> <span data-ttu-id="b47dc-129">Aggiungere hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="b47dc-129">Add hello following code:</span></span>

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-hello-application"></a><span data-ttu-id="b47dc-130">Compilare ed eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="b47dc-130">Build and run hello application</span></span>
<span data-ttu-id="b47dc-131">Hello passaggi seguenti viene descritto come toouse *CMake* toobuild l'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="b47dc-131">hello following steps describe how toouse *CMake* toobuild your client application.</span></span>

1. <span data-ttu-id="b47dc-132">In un editor di testo aprire hello **CMakeLists.txt** file hello **remote_monitoring** cartella.</span><span class="sxs-lookup"><span data-stu-id="b47dc-132">In a text editor, open hello **CMakeLists.txt** file in hello **remote_monitoring** folder.</span></span>

1. <span data-ttu-id="b47dc-133">Aggiungere hello seguendo le istruzioni toodefine come toobuild l'applicazione client:</span><span class="sxs-lookup"><span data-stu-id="b47dc-133">Add hello following instructions toodefine how toobuild your client application:</span></span>
   
    ```
    macro(compileAsC99)
      if (CMAKE_VERSION VERSION_LESS "3.1")
        if (CMAKE_C_COMPILER_ID STREQUAL "GNU")
          set (CMAKE_C_FLAGS "--std=c99 ${CMAKE_C_FLAGS}")
          set (CMAKE_CXX_FLAGS "--std=c++11 ${CMAKE_CXX_FLAGS}")
        endif()
      else()
        set (CMAKE_C_STANDARD 99)
        set (CMAKE_CXX_STANDARD 11)
      endif()
    endmacro(compileAsC99)

    cmake_minimum_required(VERSION 2.8.11)
    compileAsC99()

    set(AZUREIOT_INC_FOLDER "${CMAKE_SOURCE_DIR}" "${CMAKE_SOURCE_DIR}/parson" "/usr/include/azureiot" "/usr/include/azureiot/inc")

    include_directories(${AZUREIOT_INC_FOLDER})

    set(sample_application_c_files
        ./parson/parson.c
        ./remote_monitoring.c
        ./main.c
    )

    set(sample_application_h_files
        ./parson/parson.h
        ./remote_monitoring.h
    )

    add_executable(sample_app ${sample_application_c_files} ${sample_application_h_files})

    target_link_libraries(sample_app
        serializer
        iothub_client
        iothub_client_mqtt_transport
        aziotsharedutil
        umqtt
        pthread
        curl
        ssl
        crypto
        m
    )
    ```
1. <span data-ttu-id="b47dc-134">In hello **remote_monitoring** cartella, creare un hello toostore cartella *rendere* file tale CMake genera l'errore e quindi eseguire hello **cmake** e **rendere** comandi nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="b47dc-134">In hello **remote_monitoring** folder, create a folder toostore hello *make* files that CMake generates and then run hello **cmake** and **make** commands as follows:</span></span>
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. <span data-ttu-id="b47dc-135">Eseguire un'applicazione client hello e inviare dati di telemetria tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="b47dc-135">Run hello client application and send telemetry tooIoT Hub:</span></span>
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

