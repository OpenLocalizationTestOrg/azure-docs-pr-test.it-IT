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
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-linux"></a>Connettersi toohello il dispositivo remoto monitoraggio soluzione preconfigurata (Linux)
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a>Compilare ed eseguire un client C Linux di esempio
Hello alla procedura seguente viene illustrato come un'applicazione client che comunica con il monitoraggio remoto hello toocreate preconfigurato soluzione. Questa applicazione è scritta in C e compilata ed eseguita in Ubuntu Linux.

toocomplete questi passaggi, è necessario un dispositivo che esegue Ubuntu 15.04 o 15.10 versione. Prima di continuare, installare i pacchetti dei prerequisiti hello nel dispositivo Ubuntu utilizzando hello comando seguente:

```
sudo apt-get install cmake gcc g++
```

## <a name="install-hello-client-libraries-on-your-device"></a>Installare le librerie client hello sul dispositivo
Hello Azure IoT Hub librerie client sono disponibili come un pacchetto è possibile installare nel dispositivo Ubuntu utilizzando hello **apt get** comando. Completare i seguenti passaggi tooinstall hello pacchetto hello libreria client IoT Hub e il file di intestazione nel computer in uso Ubuntu hello:

1. In una shell, aggiungere hello AzureIoT repository tooyour computer:
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. Installare il pacchetto di azure-iot-sdk-c-dev hello
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-hello-parson-json-parser"></a>Installare hello parser Parson JSON
utilizzano le librerie client di IoT Hub Hello hello payload dei messaggi Parson JSON parser tooparse. In una cartella appropriata nel computer in uso, clonare il repository di GitHub Parson hello utilizzando hello comando seguente:

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a>Preparare il progetto
Nel computer Ubuntu creare una cartella denominata **remote\_monitoring**. In hello **remoto\_monitoraggio** cartella:

- Creare quattro file di hello **Main. c**, **remoto\_monitoring.c**, **remoto\_monitoring.h**, e **CMakeLists.txt**.
- Creare una cartella denominata **parson**.

Copiare i file hello **parson.c** e **parson.h** dalla copia locale del repository Parson hello in hello **remoto\_/parson monitoraggio** cartella.

In un editor di testo aprire hello **remoto\_monitoring.c** file. Aggiungere il seguente hello `#include` istruzioni:
   
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

## <a name="call-hello-remotemonitoringrun-function"></a>Chiamare hello remoto\_monitoraggio\_eseguire (funzione)
In un editor di testo aprire hello **remote_monitoring.h** file. Aggiungere hello seguente codice:

```
void remote_monitoring_run(void);
```

In un editor di testo aprire hello **Main. c** file. Aggiungere hello seguente codice:

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-hello-application"></a>Compilare ed eseguire un'applicazione hello
Hello passaggi seguenti viene descritto come toouse *CMake* toobuild l'applicazione client.

1. In un editor di testo aprire hello **CMakeLists.txt** file hello **remote_monitoring** cartella.

1. Aggiungere hello seguendo le istruzioni toodefine come toobuild l'applicazione client:
   
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
1. In hello **remote_monitoring** cartella, creare un hello toostore cartella *rendere* file tale CMake genera l'errore e quindi eseguire hello **cmake** e **rendere** comandi nel modo seguente:
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. Eseguire un'applicazione client hello e inviare dati di telemetria tooIoT Hub:
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

