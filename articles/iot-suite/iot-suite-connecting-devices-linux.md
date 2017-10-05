---
title: Connettere un dispositivo tramite C in Linux | Documentazione Microsoft
description: "Descrive come connettere un dispositivo alla soluzione di monitoraggio remoto preconfigurata Azure IoT Suite con un’applicazione scritta in C in esecuzione in Linux."
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
ms.openlocfilehash: 9adbc9cc13f0b4cafa3a3a7703c46f8085b15232
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-linux"></a><span data-ttu-id="95689-103">Connettere il dispositivo alla soluzione preconfigurata per il monitoraggio remoto (Linux)</span><span class="sxs-lookup"><span data-stu-id="95689-103">Connect your device to the remote monitoring preconfigured solution (Linux)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a><span data-ttu-id="95689-104">Compilare ed eseguire un client C Linux di esempio</span><span class="sxs-lookup"><span data-stu-id="95689-104">Build and run a sample C client Linux</span></span>
<span data-ttu-id="95689-105">La procedura seguente illustra come creare un'applicazione client che comunica con la soluzione di monitoraggio remoto preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="95689-105">The following steps show you how to create a client application that communicates with the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="95689-106">Questa applicazione è scritta in C e compilata ed eseguita in Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="95689-106">This application is written in C and built and run on Ubuntu Linux.</span></span>

<span data-ttu-id="95689-107">Per completare questa procedura, è necessario un dispositivo che esegue Ubuntu versione 15.04 o 15.10.</span><span class="sxs-lookup"><span data-stu-id="95689-107">To complete these steps, you need a device running Ubuntu version 15.04 or 15.10.</span></span> <span data-ttu-id="95689-108">Prima di continuare, installare i pacchetti dei prerequisiti nel dispositivo Ubuntu usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="95689-108">Before proceeding, install the prerequisite packages on your Ubuntu device using the following command:</span></span>

```
sudo apt-get install cmake gcc g++
```

## <a name="install-the-client-libraries-on-your-device"></a><span data-ttu-id="95689-109">Installare le librerie client sul dispositivo</span><span class="sxs-lookup"><span data-stu-id="95689-109">Install the client libraries on your device</span></span>
<span data-ttu-id="95689-110">Le librerie client dell'hub IoT di Azure sono disponibili in forma di pacchetto da installare sul dispositivo Ubuntu tramite il comando **apt-get** .</span><span class="sxs-lookup"><span data-stu-id="95689-110">The Azure IoT Hub client libraries are available as a package you can install on your Ubuntu device using the **apt-get** command.</span></span> <span data-ttu-id="95689-111">Completare la procedura seguente per installare il pacchetto che contiene la libreria del client dell'hub IoT e i file d'intestazione nel computer Ubuntu:</span><span class="sxs-lookup"><span data-stu-id="95689-111">Complete the following steps to install the package that contains the IoT Hub client library and header files on your Ubuntu computer:</span></span>

1. <span data-ttu-id="95689-112">In una shell, aggiungere il repository AzureIoT al computer:</span><span class="sxs-lookup"><span data-stu-id="95689-112">In a shell, add the AzureIoT repository to your computer:</span></span>
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. <span data-ttu-id="95689-113">Installare il pacchetto azure-iot-sdk-c-dev</span><span class="sxs-lookup"><span data-stu-id="95689-113">Install the azure-iot-sdk-c-dev package</span></span>
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-the-parson-json-parser"></a><span data-ttu-id="95689-114">Installare il parser JSON Parson</span><span class="sxs-lookup"><span data-stu-id="95689-114">Install the Parson JSON parser</span></span>
<span data-ttu-id="95689-115">Le librerie client di hub IoT usano il parser JSON per analizzare il payload dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="95689-115">The IoT Hub client libraries use the Parson JSON parser to parse message payloads.</span></span> <span data-ttu-id="95689-116">In una cartella appropriata nel computer, clonare il repository Parson GitHub usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="95689-116">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span></span>

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a><span data-ttu-id="95689-117">Preparare il progetto</span><span class="sxs-lookup"><span data-stu-id="95689-117">Prepare your project</span></span>
<span data-ttu-id="95689-118">Nel computer Ubuntu creare una cartella denominata **remote\_monitoring**.</span><span class="sxs-lookup"><span data-stu-id="95689-118">On your Ubuntu machine, create a folder called **remote\_monitoring**.</span></span> <span data-ttu-id="95689-119">Nella cartella **remote\_monitoring**:</span><span class="sxs-lookup"><span data-stu-id="95689-119">In the **remote\_monitoring** folder:</span></span>

- <span data-ttu-id="95689-120">Creare i quattro file **main.c**, **remote\_monitoring.c**, **remote\_monitoring.h** e **CMakeLists.txt**.</span><span class="sxs-lookup"><span data-stu-id="95689-120">Create the four files **main.c**, **remote\_monitoring.c**, **remote\_monitoring.h**, and **CMakeLists.txt**.</span></span>
- <span data-ttu-id="95689-121">Creare una cartella denominata **parson**.</span><span class="sxs-lookup"><span data-stu-id="95689-121">Create folder called **parson**.</span></span>

<span data-ttu-id="95689-122">Copiare i file **parson.c** e **parson.h** dalla copia locale del repository Parson nella cartella **remote\_monitoring/parson**.</span><span class="sxs-lookup"><span data-stu-id="95689-122">Copy the files **parson.c** and **parson.h** from your local copy of the Parson repository into the **remote\_monitoring/parson** folder.</span></span>

<span data-ttu-id="95689-123">In un editor di testo aprire il file **remote\_monitoring.c**.</span><span class="sxs-lookup"><span data-stu-id="95689-123">In a text editor, open the **remote\_monitoring.c** file.</span></span> <span data-ttu-id="95689-124">Aggiungere le istruzioni `#include` seguenti:</span><span class="sxs-lookup"><span data-stu-id="95689-124">Add the following `#include` statements:</span></span>
   
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

## <a name="call-the-remotemonitoringrun-function"></a><span data-ttu-id="95689-125">Chiamare la funzione remote\_monitoring\_run</span><span class="sxs-lookup"><span data-stu-id="95689-125">Call the remote\_monitoring\_run function</span></span>
<span data-ttu-id="95689-126">In un editor di testo aprire il file **remote_monitoring.h**.</span><span class="sxs-lookup"><span data-stu-id="95689-126">In a text editor, open the **remote_monitoring.h** file.</span></span> <span data-ttu-id="95689-127">Aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="95689-127">Add the following code:</span></span>

```
void remote_monitoring_run(void);
```

<span data-ttu-id="95689-128">In un editor di testo aprire il file **main. c** .</span><span class="sxs-lookup"><span data-stu-id="95689-128">In a text editor, open the **main.c** file.</span></span> <span data-ttu-id="95689-129">Aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="95689-129">Add the following code:</span></span>

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-the-application"></a><span data-ttu-id="95689-130">Compilare ed eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="95689-130">Build and run the application</span></span>
<span data-ttu-id="95689-131">La procedura seguente descrive i metodi d'uso di *CMake* per compilare l'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="95689-131">The following steps describe how to use *CMake* to build your client application.</span></span>

1. <span data-ttu-id="95689-132">In un editor di testo aprire il file **CMakeLists.txt** nella cartella **remote_monitoring**.</span><span class="sxs-lookup"><span data-stu-id="95689-132">In a text editor, open the **CMakeLists.txt** file in the **remote_monitoring** folder.</span></span>

1. <span data-ttu-id="95689-133">Aggiungere le istruzioni seguenti per definire la modalità di compilazione dell'applicazione client:</span><span class="sxs-lookup"><span data-stu-id="95689-133">Add the following instructions to define how to build your client application:</span></span>
   
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
1. <span data-ttu-id="95689-134">Nella cartella **remote_monitoring** creare una cartella per archiviare i file *make* generati da CMake e quindi eseguire i comandi **cmake** e **make** come segue:</span><span class="sxs-lookup"><span data-stu-id="95689-134">In the **remote_monitoring** folder, create a folder to store the *make* files that CMake generates and then run the **cmake** and **make** commands as follows:</span></span>
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. <span data-ttu-id="95689-135">Eseguire l'applicazione client e inviare dati di telemetria all'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="95689-135">Run the client application and send telemetry to IoT Hub:</span></span>
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

