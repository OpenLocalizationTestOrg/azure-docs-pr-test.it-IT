---
title: Connettere un dispositivo tramite C in Windows | Documentazione Microsoft
description: "Descrive come connettere un dispositivo alla soluzione di monitoraggio remoto preconfigurata Azure IoT Suite con un’applicazione scritta in C in esecuzione in Windows."
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
ms.openlocfilehash: d222bcbd64f288d4091acb0ecd2922b9ceee57e5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-windows"></a><span data-ttu-id="10e26-103">Connettere il dispositivo alla soluzione preconfigurata per il monitoraggio remoto (Windows)</span><span class="sxs-lookup"><span data-stu-id="10e26-103">Connect your device to the remote monitoring preconfigured solution (Windows)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a><span data-ttu-id="10e26-104">Creare una soluzione di esempio C in Windows</span><span class="sxs-lookup"><span data-stu-id="10e26-104">Create a C sample solution on Windows</span></span>
<span data-ttu-id="10e26-105">La procedura seguente illustra come creare un'applicazione client che comunica con la soluzione di monitoraggio remoto preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="10e26-105">The following steps show you how to create a client application that communicates with the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="10e26-106">Questa applicazione è scritta in C e compilata ed eseguita in Windows.</span><span class="sxs-lookup"><span data-stu-id="10e26-106">This application is written in C and built and run on Windows.</span></span>

<span data-ttu-id="10e26-107">Creare un progetto iniziale in Visual Studio 2015 o Visual Studio 2017 e aggiungere i pacchetti NuGet del client dispositivo hub IoT:</span><span class="sxs-lookup"><span data-stu-id="10e26-107">Create a starter project in Visual Studio 2015 or Visual Studio 2017 and add the IoT Hub device client NuGet packages:</span></span>

1. <span data-ttu-id="10e26-108">In Visual Studio creare un'applicazione console C usando il modello **Applicazione console Win32** di Visual C++ .</span><span class="sxs-lookup"><span data-stu-id="10e26-108">In Visual Studio, create a C console application using the Visual C++ **Win32 Console Application** template.</span></span> <span data-ttu-id="10e26-109">Assegnare al progetto il nome **RMDevice**.</span><span class="sxs-lookup"><span data-stu-id="10e26-109">Name the project **RMDevice**.</span></span>
2. <span data-ttu-id="10e26-110">Nella pagina **Impostazioni applicazione** della **Creazione guidata applicazione Win32** verificare che l'opzione **Applicazione console** sia selezionata e deselezionare **Intestazione precompilata** e **Controlli Security Development Lifecycle (SDL)**.</span><span class="sxs-lookup"><span data-stu-id="10e26-110">On the **Application Settings** page in the **Win32 Application Wizard**, ensure that **Console application** is selected, and uncheck **Precompiled header** and **Security Development Lifecycle (SDL) checks**.</span></span>
3. <span data-ttu-id="10e26-111">In **Esplora soluzioni**eliminare i file stdafx.h, targetver.h e stdafx.cpp.</span><span class="sxs-lookup"><span data-stu-id="10e26-111">In **Solution Explorer**, delete the files stdafx.h, targetver.h, and stdafx.cpp.</span></span>
4. <span data-ttu-id="10e26-112">In **Esplora soluzioni**rinominare il file RMDevice.cpp in RMDevice.c.</span><span class="sxs-lookup"><span data-stu-id="10e26-112">In **Solution Explorer**, rename the file RMDevice.cpp to RMDevice.c.</span></span>
5. <span data-ttu-id="10e26-113">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **RMDevice** e quindi scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="10e26-113">In **Solution Explorer**, right-click on the **RMDevice** project and then click **Manage NuGet packages**.</span></span> <span data-ttu-id="10e26-114">Fare clic su **Sfoglia**, quindi cercare e installare i seguenti pacchetti NuGet:</span><span class="sxs-lookup"><span data-stu-id="10e26-114">Click **Browse**, then search for and install the following NuGet packages:</span></span>
   
   * <span data-ttu-id="10e26-115">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="10e26-115">Microsoft.Azure.IoTHub.Serializer</span></span>
   * <span data-ttu-id="10e26-116">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="10e26-116">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
   * <span data-ttu-id="10e26-117">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="10e26-117">Microsoft.Azure.IoTHub.MqttTransport</span></span>
6. <span data-ttu-id="10e26-118">In **Esplora soluzioni** fare clic sul progetto **RMDevice** e quindi scegliere **Proprietà** per aprire la finestra di dialogo **Pagine** delle proprietà del progetto.</span><span class="sxs-lookup"><span data-stu-id="10e26-118">In **Solution Explorer**, right-click on the **RMDevice** project and then click **Properties** to open the project's **Property Pages** dialog box.</span></span> <span data-ttu-id="10e26-119">Per informazioni dettagliate, vedere [Setting Visual C++ Project Properties][lnk-c-project-properties] (Impostazione delle proprietà dei progetti Visual C++).</span><span class="sxs-lookup"><span data-stu-id="10e26-119">For details, see [Setting Visual C++ Project Properties][lnk-c-project-properties].</span></span> 
7. <span data-ttu-id="10e26-120">Fare clic sulla cartella **Linker**, quindi fare clic sulla pagina delle proprietà **Input**.</span><span class="sxs-lookup"><span data-stu-id="10e26-120">Click the **Linker** folder, then click the **Input** property page.</span></span>
8. <span data-ttu-id="10e26-121">Aggiungere **crypt32.lib** alla proprietà **Dipendenze aggiuntive**.</span><span class="sxs-lookup"><span data-stu-id="10e26-121">Add **crypt32.lib** to the **Additional Dependencies** property.</span></span> <span data-ttu-id="10e26-122">Fare clic su **OK** e quindi scegliere nuovamente **OK** per salvare i valori delle proprietà del progetto.</span><span class="sxs-lookup"><span data-stu-id="10e26-122">Click **OK** and then **OK** again to save the project property values.</span></span>

<span data-ttu-id="10e26-123">Aggiungere la libreria Parson JSON al progetto **RMDevice** e aggiungere le istruzioni `#include` richieste:</span><span class="sxs-lookup"><span data-stu-id="10e26-123">Add the Parson JSON library to the **RMDevice** project and add the required `#include` statements:</span></span>

1. <span data-ttu-id="10e26-124">In una cartella appropriata nel computer, clonare il repository Parson GitHub usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="10e26-124">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span></span>

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. <span data-ttu-id="10e26-125">Copiare i file parson.h e parson.c dalla copia locale del repository Parson alla cartella del progetto **RMDevice**.</span><span class="sxs-lookup"><span data-stu-id="10e26-125">Copy the parson.h and parson.c files from the local copy of the Parson repository to your **RMDevice** project folder.</span></span>

1. <span data-ttu-id="10e26-126">In Visual Studio fare clic con il pulsante destro del mouse sul progetto **RMDevice**, scegliere **Aggiungi** e quindi **Elemento esistente**.</span><span class="sxs-lookup"><span data-stu-id="10e26-126">In Visual Studio, right-click the **RMDevice** project, click **Add**, and then click **Existing Item**.</span></span>

1. <span data-ttu-id="10e26-127">Nella finestra di dialogo **Aggiungi elemento esistente**, selezionare i file parson.h e parson.c file nella cartella di progetto **RMDevice**.</span><span class="sxs-lookup"><span data-stu-id="10e26-127">In the **Add Existing Item** dialog, select the parson.h and parson.c files in the **RMDevice** project folder.</span></span> <span data-ttu-id="10e26-128">Quindi fare clic su **Aggiungi** per aggiungere i due file al progetto.</span><span class="sxs-lookup"><span data-stu-id="10e26-128">Then click **Add** to add these two files to your project.</span></span>

1. <span data-ttu-id="10e26-129">In Visual Studio aprire il file RMDevice.c.</span><span class="sxs-lookup"><span data-stu-id="10e26-129">In Visual Studio, open the RMDevice.c file.</span></span> <span data-ttu-id="10e26-130">Sostituire le istruzioni `#include` esistenti con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="10e26-130">Replace the existing `#include` statements with the following code:</span></span>
   
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
    > <span data-ttu-id="10e26-131">Compilando il progetto è possibile verificare che siano state impostate le dipendenze corrette.</span><span class="sxs-lookup"><span data-stu-id="10e26-131">Now you can verify that your project has the correct dependencies set up by building it.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-the-sample"></a><span data-ttu-id="10e26-132">Compilare ed eseguire l'esempio</span><span class="sxs-lookup"><span data-stu-id="10e26-132">Build and run the sample</span></span>

<span data-ttu-id="10e26-133">Aggiungere codice per richiamare la funzione **remote\_monitoring\_run** e quindi creare ed eseguire l'applicazione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="10e26-133">Add code to invoke the **remote\_monitoring\_run** function and then build and run the device application.</span></span>

1. <span data-ttu-id="10e26-134">Sostituire la funzione **main** con il codice seguente per richiamare la funzione **remote\_monitoring\_run**:</span><span class="sxs-lookup"><span data-stu-id="10e26-134">Replace the **main** function with following code to invoke the **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="10e26-135">Fare clic su **Compila** e quindi su **Compila soluzione** per compilare l'applicazione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="10e26-135">Click **Build** and then **Build Solution** to build the device application.</span></span>

1. <span data-ttu-id="10e26-136">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **RMDevice**, scegliere **Debug** e quindi fare clic su **Avvia nuova istanza** per eseguire l'esempio.</span><span class="sxs-lookup"><span data-stu-id="10e26-136">In **Solution Explorer**, right-click the **RMDevice** project, click **Debug**, and then click **Start new instance** to run the sample.</span></span> <span data-ttu-id="10e26-137">Nella console vengono visualizzati i messaggi mano a mano che l'applicazione invia i dati di telemetria di esempio alla soluzione preconfigurata, riceve i valori delle proprietà desiderate impostate nel dashboard della soluzione e risponde ai metodi richiamati dal dashboard della soluzione.</span><span class="sxs-lookup"><span data-stu-id="10e26-137">The console displays messages as the application sends sample telemetry to the preconfigured solution, receives desired property values set in the solution dashboard, and responds to methods invoked from the solution dashboard.</span></span>

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
