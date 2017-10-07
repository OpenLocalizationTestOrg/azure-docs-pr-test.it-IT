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
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-windows"></a><span data-ttu-id="258cd-103">Connettersi toohello il dispositivo remoto monitoraggio soluzione preconfigurata (Windows)</span><span class="sxs-lookup"><span data-stu-id="258cd-103">Connect your device toohello remote monitoring preconfigured solution (Windows)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a><span data-ttu-id="258cd-104">Creare una soluzione di esempio C in Windows</span><span class="sxs-lookup"><span data-stu-id="258cd-104">Create a C sample solution on Windows</span></span>
<span data-ttu-id="258cd-105">Hello alla procedura seguente viene illustrato come un'applicazione client che comunica con il monitoraggio remoto hello toocreate preconfigurato soluzione.</span><span class="sxs-lookup"><span data-stu-id="258cd-105">hello following steps show you how toocreate a client application that communicates with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="258cd-106">Questa applicazione è scritta in C e compilata ed eseguita in Windows.</span><span class="sxs-lookup"><span data-stu-id="258cd-106">This application is written in C and built and run on Windows.</span></span>

<span data-ttu-id="258cd-107">Creare un progetto di avvio in Visual Studio 2015 o Visual Studio 2017 e aggiungere pacchetti NuGet di hello Hub IoT dispositivo client:</span><span class="sxs-lookup"><span data-stu-id="258cd-107">Create a starter project in Visual Studio 2015 or Visual Studio 2017 and add hello IoT Hub device client NuGet packages:</span></span>

1. <span data-ttu-id="258cd-108">In Visual Studio, creare un'applicazione console C utilizzando Visual C++ hello **applicazione Console Win32** modello.</span><span class="sxs-lookup"><span data-stu-id="258cd-108">In Visual Studio, create a C console application using hello Visual C++ **Win32 Console Application** template.</span></span> <span data-ttu-id="258cd-109">Progetto hello nome **RMDevice**.</span><span class="sxs-lookup"><span data-stu-id="258cd-109">Name hello project **RMDevice**.</span></span>
2. <span data-ttu-id="258cd-110">In hello **le impostazioni dell'applicazione** pagina hello **Creazione guidata applicazione Win32**, assicurarsi che **applicazione Console** sia selezionata e deselezionare **precompilata intestazione** e **Security Development Lifecycle (SDL) controlla**.</span><span class="sxs-lookup"><span data-stu-id="258cd-110">On hello **Application Settings** page in hello **Win32 Application Wizard**, ensure that **Console application** is selected, and uncheck **Precompiled header** and **Security Development Lifecycle (SDL) checks**.</span></span>
3. <span data-ttu-id="258cd-111">In **Esplora**, eliminare stdafx.cpp, targetver e stdafx. h file hello.</span><span class="sxs-lookup"><span data-stu-id="258cd-111">In **Solution Explorer**, delete hello files stdafx.h, targetver.h, and stdafx.cpp.</span></span>
4. <span data-ttu-id="258cd-112">In **Esplora**, rinominare tooRMDevice.c RMDevice.cpp di file hello.</span><span class="sxs-lookup"><span data-stu-id="258cd-112">In **Solution Explorer**, rename hello file RMDevice.cpp tooRMDevice.c.</span></span>
5. <span data-ttu-id="258cd-113">In **Esplora**, fare clic su hello **RMDevice** del progetto e quindi fare clic su **Gestione pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="258cd-113">In **Solution Explorer**, right-click on hello **RMDevice** project and then click **Manage NuGet packages**.</span></span> <span data-ttu-id="258cd-114">Fare clic su **Sfoglia**, quindi cercare e installare i seguenti pacchetti NuGet hello:</span><span class="sxs-lookup"><span data-stu-id="258cd-114">Click **Browse**, then search for and install hello following NuGet packages:</span></span>
   
   * <span data-ttu-id="258cd-115">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="258cd-115">Microsoft.Azure.IoTHub.Serializer</span></span>
   * <span data-ttu-id="258cd-116">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="258cd-116">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
   * <span data-ttu-id="258cd-117">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="258cd-117">Microsoft.Azure.IoTHub.MqttTransport</span></span>
6. <span data-ttu-id="258cd-118">In **Esplora**, fare clic su hello **RMDevice** del progetto e quindi fare clic su **proprietà** del progetto hello tooopen **pagine delle proprietà**la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="258cd-118">In **Solution Explorer**, right-click on hello **RMDevice** project and then click **Properties** tooopen hello project's **Property Pages** dialog box.</span></span> <span data-ttu-id="258cd-119">Per informazioni dettagliate, vedere [Setting Visual C++ Project Properties][lnk-c-project-properties] (Impostazione delle proprietà dei progetti Visual C++).</span><span class="sxs-lookup"><span data-stu-id="258cd-119">For details, see [Setting Visual C++ Project Properties][lnk-c-project-properties].</span></span> 
7. <span data-ttu-id="258cd-120">Fare clic su hello **Linker** cartella, quindi fare clic su hello **Input** pagina delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="258cd-120">Click hello **Linker** folder, then click hello **Input** property page.</span></span>
8. <span data-ttu-id="258cd-121">Aggiungere **crypt32.lib** toohello **dipendenze aggiuntive** proprietà.</span><span class="sxs-lookup"><span data-stu-id="258cd-121">Add **crypt32.lib** toohello **Additional Dependencies** property.</span></span> <span data-ttu-id="258cd-122">Fare clic su **OK** e quindi **OK** nuovamente toosave hello progetto i valori delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="258cd-122">Click **OK** and then **OK** again toosave hello project property values.</span></span>

<span data-ttu-id="258cd-123">Aggiungere hello JSON Parson libreria toohello **RMDevice** del progetto e aggiungere hello necessario `#include` istruzioni:</span><span class="sxs-lookup"><span data-stu-id="258cd-123">Add hello Parson JSON library toohello **RMDevice** project and add hello required `#include` statements:</span></span>

1. <span data-ttu-id="258cd-124">In una cartella appropriata nel computer in uso, clonare il repository di GitHub Parson hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="258cd-124">In a suitable folder on your computer, clone hello Parson GitHub repository using hello following command:</span></span>

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. <span data-ttu-id="258cd-125">Copiare hello parson.h e parson.c dalla copia locale di hello di hello Parson repository tooyour **RMDevice** cartella del progetto.</span><span class="sxs-lookup"><span data-stu-id="258cd-125">Copy hello parson.h and parson.c files from hello local copy of hello Parson repository tooyour **RMDevice** project folder.</span></span>

1. <span data-ttu-id="258cd-126">In Visual Studio, fare doppio clic su hello **RMDevice** del progetto, fare clic su **Aggiungi**, quindi fare clic su **elemento esistente**.</span><span class="sxs-lookup"><span data-stu-id="258cd-126">In Visual Studio, right-click hello **RMDevice** project, click **Add**, and then click **Existing Item**.</span></span>

1. <span data-ttu-id="258cd-127">In hello **Aggiungi elemento esistente** finestra di dialogo, selezionare hello parson.h e parson.c i file hello **RMDevice** cartella del progetto.</span><span class="sxs-lookup"><span data-stu-id="258cd-127">In hello **Add Existing Item** dialog, select hello parson.h and parson.c files in hello **RMDevice** project folder.</span></span> <span data-ttu-id="258cd-128">Quindi fare clic su **Aggiungi** tooadd project tooyour due file.</span><span class="sxs-lookup"><span data-stu-id="258cd-128">Then click **Add** tooadd these two files tooyour project.</span></span>

1. <span data-ttu-id="258cd-129">In Visual Studio, aprire il file di RMDevice.c hello.</span><span class="sxs-lookup"><span data-stu-id="258cd-129">In Visual Studio, open hello RMDevice.c file.</span></span> <span data-ttu-id="258cd-130">Sostituire hello `#include` istruzioni con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="258cd-130">Replace hello existing `#include` statements with hello following code:</span></span>
   
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
    > <span data-ttu-id="258cd-131">Ora è possibile verificare che il progetto include dipendenze corrette di hello configurate da compilare.</span><span class="sxs-lookup"><span data-stu-id="258cd-131">Now you can verify that your project has hello correct dependencies set up by building it.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a><span data-ttu-id="258cd-132">Compilare ed eseguire l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="258cd-132">Build and run hello sample</span></span>

<span data-ttu-id="258cd-133">Aggiungere hello tooinvoke codice **remoto\_monitoraggio\_eseguire** funzione e quindi compilare ed eseguire un'applicazione hello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="258cd-133">Add code tooinvoke hello **remote\_monitoring\_run** function and then build and run hello device application.</span></span>

1. <span data-ttu-id="258cd-134">Sostituire hello **principale** funzione con hello tooinvoke di codice seguente **remoto\_monitoraggio\_eseguire** funzione:</span><span class="sxs-lookup"><span data-stu-id="258cd-134">Replace hello **main** function with following code tooinvoke hello **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="258cd-135">Fare clic su **compilare** e quindi **Compila soluzione** toobuild un'applicazione hello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="258cd-135">Click **Build** and then **Build Solution** toobuild hello device application.</span></span>

1. <span data-ttu-id="258cd-136">In **Esplora**, hello rapida **RMDevice** del progetto, fare clic su **Debug**e quindi fare clic su **Avvia nuova istanza** toorun hello esempio di.</span><span class="sxs-lookup"><span data-stu-id="258cd-136">In **Solution Explorer**, right-click hello **RMDevice** project, click **Debug**, and then click **Start new instance** toorun hello sample.</span></span> <span data-ttu-id="258cd-137">console Hello Visualizza messaggi come hello applicazione invia esempio telemetria toohello soluzione preconfigurato, riceve i valori di proprietà desiderato impostati in dashboard soluzione hello e risponde toomethods richiamato dal dashboard di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="258cd-137">hello console displays messages as hello application sends sample telemetry toohello preconfigured solution, receives desired property values set in hello solution dashboard, and responds toomethods invoked from hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
