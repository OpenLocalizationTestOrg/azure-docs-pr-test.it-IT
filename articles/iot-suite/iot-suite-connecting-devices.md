---
title: aaaConnect un dispositivo utilizzando C in Windows | Documenti Microsoft
description: Viene descritto come tooconnect toohello un dispositivo Azure IoT Suite preconfigurato soluzione di monitoraggio remoto utilizzando un'applicazione scritta in C in esecuzione su Windows.
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 34e39a58-2434-482c-b3fa-29438a0c05e8
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 51041e0cec113a5cfa006ab2276096baf928eef5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-windows"></a>Connettersi toohello il dispositivo remoto monitoraggio soluzione preconfigurata (Windows)
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a>Creare una soluzione di esempio C in Windows
Hello alla procedura seguente viene illustrato come un'applicazione client che comunica con il monitoraggio remoto hello toocreate preconfigurato soluzione. Questa applicazione è scritta in C e compilata ed eseguita in Windows.

Creare un progetto di avvio in Visual Studio 2015 o Visual Studio 2017 e aggiungere pacchetti NuGet di hello Hub IoT dispositivo client:

1. In Visual Studio, creare un'applicazione console C utilizzando Visual C++ hello **applicazione Console Win32** modello. Progetto hello nome **RMDevice**.
2. In hello **le impostazioni dell'applicazione** pagina hello **Creazione guidata applicazione Win32**, assicurarsi che **applicazione Console** sia selezionata e deselezionare **precompilata intestazione** e **Security Development Lifecycle (SDL) controlla**.
3. In **Esplora**, eliminare stdafx.cpp, targetver e stdafx. h file hello.
4. In **Esplora**, rinominare tooRMDevice.c RMDevice.cpp di file hello.
5. In **Esplora**, fare clic su hello **RMDevice** del progetto e quindi fare clic su **Gestione pacchetti NuGet**. Fare clic su **Sfoglia**, quindi cercare e installare i seguenti pacchetti NuGet hello:
   
   * Microsoft.Azure.IoTHub.Serializer
   * Microsoft.Azure.IoTHub.IoTHubClient
   * Microsoft.Azure.IoTHub.MqttTransport
6. In **Esplora**, fare clic su hello **RMDevice** del progetto e quindi fare clic su **proprietà** del progetto hello tooopen **pagine delle proprietà**la finestra di dialogo. Per informazioni dettagliate, vedere [Setting Visual C++ Project Properties][lnk-c-project-properties] (Impostazione delle proprietà dei progetti Visual C++). 
7. Fare clic su hello **Linker** cartella, quindi fare clic su hello **Input** pagina delle proprietà.
8. Aggiungere **crypt32.lib** toohello **dipendenze aggiuntive** proprietà. Fare clic su **OK** e quindi **OK** nuovamente toosave hello progetto i valori delle proprietà.

Aggiungere hello JSON Parson libreria toohello **RMDevice** del progetto e aggiungere hello necessario `#include` istruzioni:

1. In una cartella appropriata nel computer in uso, clonare il repository di GitHub Parson hello utilizzando hello comando seguente:

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. Copiare hello parson.h e parson.c dalla copia locale di hello di hello Parson repository tooyour **RMDevice** cartella del progetto.

1. In Visual Studio, fare doppio clic su hello **RMDevice** del progetto, fare clic su **Aggiungi**, quindi fare clic su **elemento esistente**.

1. In hello **Aggiungi elemento esistente** finestra di dialogo, selezionare hello parson.h e parson.c i file hello **RMDevice** cartella del progetto. Quindi fare clic su **Aggiungi** tooadd project tooyour due file.

1. In Visual Studio, aprire il file di RMDevice.c hello. Sostituire hello `#include` istruzioni con hello seguente codice:
   
    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"
    ```

    > [!NOTE]
    > Ora è possibile verificare che il progetto include dipendenze corrette di hello configurate da compilare.

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a>Compilare ed eseguire l'esempio hello

Aggiungere hello tooinvoke codice **remoto\_monitoraggio\_eseguire** funzione e quindi compilare ed eseguire un'applicazione hello dispositivo.

1. Sostituire hello **principale** funzione con hello tooinvoke di codice seguente **remoto\_monitoraggio\_eseguire** funzione:
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. Fare clic su **compilare** e quindi **Compila soluzione** toobuild un'applicazione hello dispositivo.

1. In **Esplora**, hello rapida **RMDevice** del progetto, fare clic su **Debug**e quindi fare clic su **Avvia nuova istanza** toorun hello esempio di. console Hello Visualizza messaggi come hello applicazione invia esempio telemetria toohello soluzione preconfigurato, riceve i valori di proprietà desiderato impostati in dashboard soluzione hello e risponde toomethods richiamato dal dashboard di soluzione hello.

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
