---
title: Azure IoT SDK per dispositivi per C | Documentazione Microsoft
description: Introduzione ad Azure IoT SDK per dispositivi per C e informazioni su come creare app per dispositivi in grado di comunicare con un hub IoT.
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: e448b061-6bdd-470a-a527-15ec03cca7b9
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: obloch
ms.openlocfilehash: 459b630f28fe48064f4ba280974f3fdbdb82f0a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-iot-device-sdk-for-c"></a><span data-ttu-id="5b86b-103">Azure IoT SDK per dispositivi per C</span><span class="sxs-lookup"><span data-stu-id="5b86b-103">Azure IoT device SDK for C</span></span>

<span data-ttu-id="5b86b-104">**Azure IoT SDK per dispositivi** è un set di librerie concepite per semplificare l'invio di messaggi e la ricezione di messaggi nel servizio **Hub IoT di Azure**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-104">The **Azure IoT device SDK** is a set of libraries designed to simplify the process of sending messages to and receiving messages from the **Azure IoT Hub** service.</span></span> <span data-ttu-id="5b86b-105">Esistono diverse varianti dell'SDK, ognuna destinata a una piattaforma specifica, ma questo articolo illustrerà **Azure IoT device SDK per C**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-105">There are different variations of the SDK, each targeting a specific platform, but this article describes the **Azure IoT device SDK for C**.</span></span>

<span data-ttu-id="5b86b-106">Azure IoT device SDK per C è scritto in ANSI C (C99) per ottimizzare la portabilità.</span><span class="sxs-lookup"><span data-stu-id="5b86b-106">The Azure IoT device SDK for C is written in ANSI C (C99) to maximize portability.</span></span> <span data-ttu-id="5b86b-107">Questa funzionalità rende le librerie particolarmente adatte al funzionamento su più dispositivi e piattaforme, specialmente quando la riduzione del footprint del disco e della memoria costituisce una priorità.</span><span class="sxs-lookup"><span data-stu-id="5b86b-107">This feature makes the libraries well-suited to operate on multiple platforms and devices, especially where minimizing disk and memory footprint is a priority.</span></span>

<span data-ttu-id="5b86b-108">Esiste una vasta gamma di piattaforme in cui è stato testato l'SDK. Per altri dettagli, vedere l'[elenco dei dispositivi Azure Certified per IoT](https://catalog.azureiotsuite.com/).</span><span class="sxs-lookup"><span data-stu-id="5b86b-108">There are a broad range of platforms on which the SDK has been tested (see the [Azure Certified for IoT device catalog](https://catalog.azureiotsuite.com/) for details).</span></span> <span data-ttu-id="5b86b-109">Anche se questo articolo include procedure dettagliate di codice di esempio eseguito su piattaforma Windows, il codice descritto è identico per tutta la gamma di piattaforme supportate.</span><span class="sxs-lookup"><span data-stu-id="5b86b-109">Although this article includes walkthroughs of sample code running on the Windows platform, the code described in this article is identical across the range of supported platforms.</span></span>

<span data-ttu-id="5b86b-110">Questo articolo introduce l'architettura di Azure IoT SDK per dispositivi per C. Illustra come inizializzare la libreria di dispositivi, inviare dati all'hub IoT e riceverne i messaggi.</span><span class="sxs-lookup"><span data-stu-id="5b86b-110">This article introduces you to the architecture of the Azure IoT device SDK for C. It demonstrates how to initialize the device library, send data to IoT Hub, and receive messages from it.</span></span> <span data-ttu-id="5b86b-111">Le informazioni contenute in questo articolo dovrebbero essere sufficienti per iniziare a usare l'SDK, ma forniscono anche puntatori per ottenere informazioni aggiuntive sulle librerie.</span><span class="sxs-lookup"><span data-stu-id="5b86b-111">The information in this article should be enough to get started using the SDK, but also provides pointers to additional information about the libraries.</span></span>

## <a name="sdk-architecture"></a><span data-ttu-id="5b86b-112">Architettura dell'SDK</span><span class="sxs-lookup"><span data-stu-id="5b86b-112">SDK architecture</span></span>

<span data-ttu-id="5b86b-113">È possibile trovare il repository GitHub di [**Azure IoT SDK per dispositivi per C**](https://github.com/Azure/azure-iot-sdk-c) e visualizzare i dettagli dell'API nelle [informazioni di riferimento per l'API C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="5b86b-113">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

<span data-ttu-id="5b86b-114">L'ultima versione delle librerie è disponibile nel ramo **master** del repository:</span><span class="sxs-lookup"><span data-stu-id="5b86b-114">The latest version of the libraries can be found in the **master** branch of the repository:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* <span data-ttu-id="5b86b-115">L'implementazione di base dell'SDK è nella cartella **iothub\_client** contenente l'implementazione del livello di API più basso nell'SDK: la libreria **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-115">The core implementation of the SDK is in the **iothub\_client** folder that contains the implementation of the lowest API layer in the SDK: the **IoTHubClient** library.</span></span> <span data-ttu-id="5b86b-116">La libreria **IoTHubClient** contiene le API di implementazione di messaggistica non elaborata per inviare all'hub IoT i messaggi e per ricevere i messaggi dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5b86b-116">The **IoTHubClient** library contains APIs implementing raw messaging for sending messages to IoT Hub and receiving messages from IoT Hub.</span></span> <span data-ttu-id="5b86b-117">Quando si usa questa libreria, si dovrà implementare la serializzazione dei messaggi, mente gli altri dettagli della comunicazione con l'hub IoT vengono gestiti automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5b86b-117">When using this library, you are responsible for implementing message serialization, but other details of communicating with IoT Hub are handled for you.</span></span>
* <span data-ttu-id="5b86b-118">La cartella **serializer** contiene le funzioni di supporto e gli esempi che mostrano come serializzare i dati prima dell'invio all'hub IoT di Azure tramite la libreria client.</span><span class="sxs-lookup"><span data-stu-id="5b86b-118">The **serializer** folder contains helper functions and samples that show you how to serialize data before sending to Azure IoT Hub using the client library.</span></span> <span data-ttu-id="5b86b-119">L'uso del serializzatore, fornito per comodità, non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="5b86b-119">The use of the serializer is not mandatory and is provided as a convenience.</span></span> <span data-ttu-id="5b86b-120">Per usare la libreria **serializer**, si definisce un modello che specifica i dati da inviare all'hub IoT e i messaggi che si prevede di ricevere dall'hub stesso.</span><span class="sxs-lookup"><span data-stu-id="5b86b-120">To use the **serializer** library, you define a model that specifies the data to send to IoT Hub and the messages you expect to receive from it.</span></span> <span data-ttu-id="5b86b-121">Dopo la definizione del modello, l'SDK fornisce tuttavia una superficie dell'API che consente di usare facilmente messaggi da dispositivo a cloud e da cloud a dispositivo senza doversi occupare dei dettagli relativi alla serializzazione.</span><span class="sxs-lookup"><span data-stu-id="5b86b-121">Once the model is defined, the SDK provides you with an API surface that enables you to easily work with device-to-cloud and cloud-to-device messages without worrying about the serialization details.</span></span> <span data-ttu-id="5b86b-122">La libreria dipende dall'implementazione del trasporto tramite protocolli come MQTT e AMQP da parte di altre librerie open source.</span><span class="sxs-lookup"><span data-stu-id="5b86b-122">The library depends on other open source libraries that implement transport using protocols such as MQTT and AMQP.</span></span>
* <span data-ttu-id="5b86b-123">La libreria **IoTHubClient** dipende da altre librerie open source:</span><span class="sxs-lookup"><span data-stu-id="5b86b-123">The **IoTHubClient** library depends on other open source libraries:</span></span>
  * <span data-ttu-id="5b86b-124">La libreria [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility), che offre funzionalità comuni per le attività di base, ad esempio stringhe, manipolazione elenco e I/O, necessarie in diversi SDK per C relativi ad Azure.</span><span class="sxs-lookup"><span data-stu-id="5b86b-124">The [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility) library, which provides common functionality for basic tasks (such as strings, list manipulation, and IO) needed across several Azure-related C SDKs.</span></span>
  * <span data-ttu-id="5b86b-125">La libreria [Azure uAMQP](https://github.com/Azure/azure-uamqp-c), che è un'implementazione lato client di AMQP ottimizzata per i dispositivi con vincoli di risorse.</span><span class="sxs-lookup"><span data-stu-id="5b86b-125">The [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) library, which is a client-side implementation of AMQP optimized for resource constrained devices.</span></span>
  * <span data-ttu-id="5b86b-126">La libreria [Azure uMQTT](https://github.com/Azure/azure-umqtt-c), che è una libreria generica per l'implementazione del protocollo MQTT, ottimizzata per i dispositivi con vincoli di risorse.</span><span class="sxs-lookup"><span data-stu-id="5b86b-126">The [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) library, which is a general-purpose library implementing the MQTT protocol and optimized for resource constrained devices.</span></span>

<span data-ttu-id="5b86b-127">L'uso di queste librerie è più facilmente comprensibile osservando esempi di codice.</span><span class="sxs-lookup"><span data-stu-id="5b86b-127">Use of these libraries is easier to understand by looking at example code.</span></span> <span data-ttu-id="5b86b-128">Le sezioni seguenti illustrano in dettaglio alcune applicazioni di esempio incluse nell'SDK.</span><span class="sxs-lookup"><span data-stu-id="5b86b-128">The following sections walk you through several of the sample applications that are included in the SDK.</span></span> <span data-ttu-id="5b86b-129">Questa procedura guidata offre una panoramica delle diverse funzionalità dei livelli architetturali dell'SDK e un'introduzione al funzionamento delle API.</span><span class="sxs-lookup"><span data-stu-id="5b86b-129">This walkthrough should give you a good feel for the various capabilities of the architectural layers of the SDK and an introduction to how the APIs work.</span></span>

## <a name="before-you-run-the-samples"></a><span data-ttu-id="5b86b-130">Prima di eseguire gli esempi</span><span class="sxs-lookup"><span data-stu-id="5b86b-130">Before you run the samples</span></span>

<span data-ttu-id="5b86b-131">Prima di poter eseguire gli esempi in Azure IoT SDK per dispositivi per C, è necessario [creare un'istanza del servizio hub IoT](iot-hub-create-through-portal.md) nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5b86b-131">Before you can run the samples in the Azure IoT device SDK for C, you must [create an instance of the IoT Hub service](iot-hub-create-through-portal.md) in your Azure subscription.</span></span> <span data-ttu-id="5b86b-132">Completare quindi le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="5b86b-132">Then complete the following tasks:</span></span>

* <span data-ttu-id="5b86b-133">Preparare l'ambiente di sviluppo</span><span class="sxs-lookup"><span data-stu-id="5b86b-133">Prepare your development environment</span></span>
* <span data-ttu-id="5b86b-134">Ottenere le credenziali del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5b86b-134">Obtain device credentials.</span></span>

### <a name="prepare-your-development-environment"></a><span data-ttu-id="5b86b-135">Preparare l'ambiente di sviluppo</span><span class="sxs-lookup"><span data-stu-id="5b86b-135">Prepare your development environment</span></span>

<span data-ttu-id="5b86b-136">Sono disponibili pacchetti per le piattaforme comuni (ad esempio, NuGet per Windows o apt_get per Debian e Ubuntu), che vengono usati negli esempi.</span><span class="sxs-lookup"><span data-stu-id="5b86b-136">Packages are provided for common platforms (such as NuGet for Windows or apt_get for Debian and Ubuntu) and the samples use these packages when available.</span></span> <span data-ttu-id="5b86b-137">In alcuni casi, è necessario compilare l'SDK per o nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5b86b-137">In some cases, you need to compile the SDK for or on your device.</span></span> <span data-ttu-id="5b86b-138">Se è necessario compilare l'SDK, vedere [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) (Preparare l'ambiente di sviluppo) nel repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="5b86b-138">If you need to compile the SDK, see [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in the GitHub repository.</span></span>

<span data-ttu-id="5b86b-139">Per ottenere il codice di applicazione di esempio, scaricare una copia dell'SDK da GitHub.</span><span class="sxs-lookup"><span data-stu-id="5b86b-139">To obtain the sample application code, download a copy of the SDK from GitHub.</span></span> <span data-ttu-id="5b86b-140">Ottenere la copia del codice sorgente dal ramo **master** del [repository GitHub](https://github.com/Azure/azure-iot-sdk-c).</span><span class="sxs-lookup"><span data-stu-id="5b86b-140">Get your copy of the source from the **master** branch of the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c).</span></span>


### <a name="obtain-the-device-credentials"></a><span data-ttu-id="5b86b-141">Ottenere le credenziali del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5b86b-141">Obtain the device credentials</span></span>

<span data-ttu-id="5b86b-142">Quando il codice sorgente di esempio è disponibile, è necessario ottenere un set di credenziali del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5b86b-142">Now that you have the sample source code, the next thing to do is to get a set of device credentials.</span></span> <span data-ttu-id="5b86b-143">Perché un dispositivo possa accedere all'hub IoT, è necessario aggiungere prima di tutto il dispositivo al registro delle identità dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5b86b-143">For a device to be able to access an IoT hub, you must first add the device to the IoT Hub identity registry.</span></span> <span data-ttu-id="5b86b-144">Quando si aggiunge il dispositivo, si ottiene un set di credenziali del dispositivo, che sono necessarie per consentire la connessione del dispositivo all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5b86b-144">When you add your device, you get a set of device credentials that you need for the device to be able to connect to the IoT hub.</span></span> <span data-ttu-id="5b86b-145">Le applicazioni di esempio illustrate nella sezione successiva richiedono queste credenziali sotto forma di **stringa di connessione del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-145">The sample applications discussed in the next section expect these credentials in the form of a **device connection string**.</span></span>

<span data-ttu-id="5b86b-146">Esistono diversi strumenti open source che consentono di gestire l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5b86b-146">There are several open source tools to help you manage your IoT hub.</span></span>

* <span data-ttu-id="5b86b-147">Un'applicazione Windows denominata [Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="5b86b-147">A Windows application called [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>
* <span data-ttu-id="5b86b-148">Uno strumento dell'interfaccia della riga di comando di node.js multipiattaforma denominato [iothub-explorer](https://github.com/azure/iothub-explorer).</span><span class="sxs-lookup"><span data-stu-id="5b86b-148">A cross-platform node.js CLI tool called [iothub-explorer](https://github.com/azure/iothub-explorer).</span></span>

<span data-ttu-id="5b86b-149">Questa esercitazione usa lo strumento grafico *Device Explorer*.</span><span class="sxs-lookup"><span data-stu-id="5b86b-149">This tutorial uses the graphical *device explorer* tool.</span></span> <span data-ttu-id="5b86b-150">È anche possibile usare *iothub-explorer* se si preferisce uno strumento dell'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="5b86b-150">You can also use the *iothub-explorer* tool if you prefer to use a CLI tool.</span></span>

<span data-ttu-id="5b86b-151">Lo strumento Device Explorer usa le librerie del servizio IoT di Azure per eseguire diverse funzioni nell'hub IoT, inclusa l'aggiunta di dispositivi.</span><span class="sxs-lookup"><span data-stu-id="5b86b-151">The device explorer tool uses the Azure IoT service libraries to perform various functions on IoT Hub, including adding devices.</span></span> <span data-ttu-id="5b86b-152">Se si usa lo strumento Device Explorer per aggiungere un dispositivo, si ottiene una stringa di connessione per il dispositivo,</span><span class="sxs-lookup"><span data-stu-id="5b86b-152">If you use the device explorer tool to add a device, you get a connection string for your device.</span></span> <span data-ttu-id="5b86b-153">che sarà necessaria per eseguire le applicazioni di esempio.</span><span class="sxs-lookup"><span data-stu-id="5b86b-153">You need this connection string to run the sample applications.</span></span>

<span data-ttu-id="5b86b-154">Se non si ha familiarità con lo strumento Device Explorer, la procedura seguente descrive come usarlo per aggiungere un dispositivo e ottenere una stringa di connessione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5b86b-154">If you're not familiar with the device explorer tool, the following procedure describes how to use it to add a device and obtain a device connection string.</span></span>

<span data-ttu-id="5b86b-155">Per installare lo strumento Device Explorer, vedere [How to use the Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) (Come usare Device Explorer per i dispositivi dell'hub IoT).</span><span class="sxs-lookup"><span data-stu-id="5b86b-155">To install the device explorer tool, see [How to use the Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>

<span data-ttu-id="5b86b-156">Durante l'esecuzione del programma, viene visualizzata l'interfaccia seguente:</span><span class="sxs-lookup"><span data-stu-id="5b86b-156">When you run the program, you see this interface:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

<span data-ttu-id="5b86b-157">Immettere la **stringa di connessione all'hub IoT** nel primo campo e fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-157">Enter your **IoT Hub Connection String** in the first field and click **Update**.</span></span> <span data-ttu-id="5b86b-158">Questo passaggio configura lo strumento per la comunicazione con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5b86b-158">This step configures the tool so that it can communicate with IoT Hub.</span></span>

<span data-ttu-id="5b86b-159">Dopo la configurazione della stringa di connessione all'hub IoT, fare clic sulla scheda **Management** (Gestione):</span><span class="sxs-lookup"><span data-stu-id="5b86b-159">When the IoT Hub connection string is configured, click the **Management** tab:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

<span data-ttu-id="5b86b-160">In questa scheda si gestiscono i dispositivi registrati nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5b86b-160">This tab is where you manage the devices registered in your IoT hub.</span></span>

<span data-ttu-id="5b86b-161">Per creare un dispositivo, fare clic sul pulsante **Create** (Crea).</span><span class="sxs-lookup"><span data-stu-id="5b86b-161">You create a device by clicking the **Create** button.</span></span> <span data-ttu-id="5b86b-162">Viene visualizzata una finestra di dialogo con un set di chiavi, primaria e secondaria, prepopolato.</span><span class="sxs-lookup"><span data-stu-id="5b86b-162">A dialog displays with a set of pre-populated keys (primary and secondary).</span></span> <span data-ttu-id="5b86b-163">Immettere un valore in **Device ID** (ID dispositivo) e fare clic su **Create** (Crea).</span><span class="sxs-lookup"><span data-stu-id="5b86b-163">Enter a **Device ID** and then click **Create**.</span></span>

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

<span data-ttu-id="5b86b-164">Dopo la creazione del dispositivo, l'elenco Devices (Dispositivi) viene aggiornato con tutti i dispositivi registrati, incluso quello appena creato.</span><span class="sxs-lookup"><span data-stu-id="5b86b-164">When the device is created, the Devices list updates with all the registered devices, including the one you just created.</span></span> <span data-ttu-id="5b86b-165">Facendo clic con il pulsante destro del mouse sul nuovo dispositivo, viene visualizzato questo menu:</span><span class="sxs-lookup"><span data-stu-id="5b86b-165">If you right-click your new device, you see this menu:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

<span data-ttu-id="5b86b-166">Se si sceglie **Copy connection string for selected device** (Copia stringa di connessione per il dispositivo selezionato), la stringa di connessione del dispositivo viene copiata negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="5b86b-166">If you choose **Copy connection string for selected device**, the device connection string is copied to the clipboard.</span></span> <span data-ttu-id="5b86b-167">Conservare una copia della stringa di connessione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5b86b-167">Keep a copy of the device connection string.</span></span> <span data-ttu-id="5b86b-168">È necessaria quando si eseguono le applicazioni di esempio descritte nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="5b86b-168">You need it when running the sample applications described in the following sections.</span></span>

<span data-ttu-id="5b86b-169">Dopo aver completato i passaggi precedenti, si è pronti per iniziare a eseguire il codice.</span><span class="sxs-lookup"><span data-stu-id="5b86b-169">When you've completed the steps above, you're ready to start running some code.</span></span> <span data-ttu-id="5b86b-170">Entrambi gli esempi hanno una costante all'inizio del file di origine principale che consente di immettere una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="5b86b-170">Both samples have a constant at the top of the main source file that enables you to enter a connection string.</span></span> <span data-ttu-id="5b86b-171">Ecco, ad esempio, la stringa di connessione dell'applicazione **iothub\_client\_sample\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-171">For example, the corresponding line from the **iothub\_client\_sample\_mqtt** application appears as follows.</span></span>

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-the-iothubclient-library"></a><span data-ttu-id="5b86b-172">Usare la libreria IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="5b86b-172">Use the IoTHubClient library</span></span>

<span data-ttu-id="5b86b-173">Nella cartella **iothub\_client** del repository [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) è presente una cartella **samples** che contiene un'applicazione denominata **iothub\_client\_sample\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-173">Within the **iothub\_client** folder in the [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, there is a **samples** folder that contains an application called **iothub\_client\_sample\_mqtt**.</span></span>

<span data-ttu-id="5b86b-174">La versione per Windows dell'applicazione **iothub\_client\_sample\_mqtt** include la soluzione di Visual Studio seguente:</span><span class="sxs-lookup"><span data-stu-id="5b86b-174">The Windows version of the **iothub\_client\_sample\_mqtt** application includes the following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="5b86b-175">Se si apre questo progetto in Visual Studio 2017, accettare la richiesta di ridestinare il progetto alla versione più recente.</span><span class="sxs-lookup"><span data-stu-id="5b86b-175">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span></span>

<span data-ttu-id="5b86b-176">Questa soluzione contiene un singolo progetto.</span><span class="sxs-lookup"><span data-stu-id="5b86b-176">This solution contains a single project.</span></span> <span data-ttu-id="5b86b-177">In questa soluzione sono installati quattro pacchetti NuGet:</span><span class="sxs-lookup"><span data-stu-id="5b86b-177">There are four NuGet packages installed in this solution:</span></span>

* <span data-ttu-id="5b86b-178">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="5b86b-178">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="5b86b-179">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="5b86b-179">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="5b86b-180">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="5b86b-180">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="5b86b-181">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="5b86b-181">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="5b86b-182">Il pacchetto **Microsoft.Azure.C.SharedUtility** è sempre necessario quando si usa l'SDK.</span><span class="sxs-lookup"><span data-stu-id="5b86b-182">You always need the **Microsoft.Azure.C.SharedUtility** package when you are working with the SDK.</span></span> <span data-ttu-id="5b86b-183">Questo esempio usa il protocollo MQTT, quindi è necessario includere i pacchetti **Microsoft.Azure.umqtt** e **Microsoft.Azure.IoTHub.MqttTransport**. Sono disponibili pacchetti equivalenti per AMQP e HTTP.</span><span class="sxs-lookup"><span data-stu-id="5b86b-183">This sample uses the MQTT protocol, therefore you must include the **Microsoft.Azure.umqtt** and **Microsoft.Azure.IoTHub.MqttTransport** packages (there are equivalent packages for AMQP and HTTP).</span></span> <span data-ttu-id="5b86b-184">L'esempio usa la libreria **IoTHubClient**, quindi è necessario includere il pacchetto **Microsoft.Azure.IoTHub.IoTHubClient** nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="5b86b-184">Because the sample uses the **IoTHubClient** library, you must also include the **Microsoft.Azure.IoTHub.IoTHubClient** package in your solution.</span></span>

<span data-ttu-id="5b86b-185">L'implementazione dell'applicazione di esempio si trova nel file di origine **iothub\_client\_sample\_mqtt.c**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-185">You can find the implementation for the sample application in the **iothub\_client\_sample\_mqtt.c** source file.</span></span>

<span data-ttu-id="5b86b-186">I passaggi seguenti usano questa applicazione di esempio per illustrare i requisiti per l'uso della libreria **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-186">The following steps use this sample application to walk you through what's required to use the **IoTHubClient** library.</span></span>

### <a name="initialize-the-library"></a><span data-ttu-id="5b86b-187">Inizializzare la libreria</span><span class="sxs-lookup"><span data-stu-id="5b86b-187">Initialize the library</span></span>

> [!NOTE]
> <span data-ttu-id="5b86b-188">Prima di iniziare a usare le librerie, è necessario eseguire alcune operazioni di inizializzazione specifiche della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="5b86b-188">Before you start working with the libraries, you may need to perform some platform-specific initialization.</span></span> <span data-ttu-id="5b86b-189">Ad esempio, se si prevede di usare AMQP in Linux è necessario inizializzare la libreria OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="5b86b-189">For example, if you plan to use AMQP on Linux you must initialize the OpenSSL library.</span></span> <span data-ttu-id="5b86b-190">Negli esempi del [repository GitHub](https://github.com/Azure/azure-iot-sdk-c) viene chiamata la funzione di utilità **platform\_init** all'avvio del client e la funzione **platform\_deinit** prima dell'uscita.</span><span class="sxs-lookup"><span data-stu-id="5b86b-190">The samples in the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c) call the utility function **platform\_init** when the client starts and call the **platform\_deinit** function before exiting.</span></span> <span data-ttu-id="5b86b-191">Queste funzioni sono dichiarate nel file di intestazione platform.h.</span><span class="sxs-lookup"><span data-stu-id="5b86b-191">These functions are declared in the platform.h header file.</span></span> <span data-ttu-id="5b86b-192">Esaminare le definizioni di queste funzioni per la piattaforma di destinazione nel [repository](https://github.com/Azure/azure-iot-sdk-c) per determinare se è necessario includere un codice di inizializzazione specifico della piattaforma nel client.</span><span class="sxs-lookup"><span data-stu-id="5b86b-192">Examine the definitions of these functions for your target platform in the [repository](https://github.com/Azure/azure-iot-sdk-c) to determine whether you need to include any platform-specific initialization code in your client.</span></span>

<span data-ttu-id="5b86b-193">Per iniziare a lavorare con le librerie, allocare prima di tutto un handle del client per l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="5b86b-193">To start working with the libraries, first allocate an IoT Hub client handle:</span></span>

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

<span data-ttu-id="5b86b-194">Si passa una copia della stringa di connessione del dispositivo ottenuta dallo strumento Device Explorer a questa funzione.</span><span class="sxs-lookup"><span data-stu-id="5b86b-194">You pass a copy of the device connection string you obtained from the device explorer tool to this function.</span></span> <span data-ttu-id="5b86b-195">Si stabilisce anche il protocollo da usare per le comunicazioni.</span><span class="sxs-lookup"><span data-stu-id="5b86b-195">You also designate the communications protocol to use.</span></span> <span data-ttu-id="5b86b-196">In questo esempio si usa MQTT, ma è possibile usare anche AMQP e HTTP.</span><span class="sxs-lookup"><span data-stu-id="5b86b-196">This example uses MQTT, but AMQP and HTTP are also options.</span></span>

<span data-ttu-id="5b86b-197">Quando è disponibile uno **IOTHUB\_CLIENT\_HANDLE** valido, si potrà iniziare a chiamare le API per l'invio e la ricezione di messaggi nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5b86b-197">When you have a valid **IOTHUB\_CLIENT\_HANDLE**, you can start calling the APIs to send and receive messages to and from IoT Hub.</span></span>

### <a name="send-messages"></a><span data-ttu-id="5b86b-198">Inviare messaggi</span><span class="sxs-lookup"><span data-stu-id="5b86b-198">Send messages</span></span>

<span data-ttu-id="5b86b-199">L'applicazione di esempio configura un ciclo per inviare messaggi all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5b86b-199">The sample application sets up a loop to send messages to your IoT hub.</span></span> <span data-ttu-id="5b86b-200">Il frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="5b86b-200">The following snippet:</span></span>

- <span data-ttu-id="5b86b-201">Crea un messaggio.</span><span class="sxs-lookup"><span data-stu-id="5b86b-201">Creates a message.</span></span>
- <span data-ttu-id="5b86b-202">Aggiunge una proprietà al messaggio.</span><span class="sxs-lookup"><span data-stu-id="5b86b-202">Adds a property to the message.</span></span>
- <span data-ttu-id="5b86b-203">Invia un messaggio.</span><span class="sxs-lookup"><span data-stu-id="5b86b-203">Sends a message.</span></span>

<span data-ttu-id="5b86b-204">Prima di tutto, creare un messaggio:</span><span class="sxs-lookup"><span data-stu-id="5b86b-204">First, create a message:</span></span>

```c
size_t iterator = 0;
do
{
    if (iterator < MESSAGE_COUNT)
    {
        sprintf_s(msgText, sizeof(msgText), "{\"deviceId\":\"myFirstDevice\",\"windSpeed\":%.2f}", avgWindSpeed + (rand() % 4 + 2));
        if ((messages[iterator].messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText))) == NULL)
        {
            (void)printf("ERROR: iotHubMessageHandle is NULL!\r\n");
        }
        else
        {
            messages[iterator].messageTrackingId = iterator;
            MAP_HANDLE propMap = IoTHubMessage_Properties(messages[iterator].messageHandle);
            (void)sprintf_s(propText, sizeof(propText), "PropMsg_%zu", iterator);
            if (Map_AddOrUpdate(propMap, "PropName", propText) != MAP_OK)
            {
                (void)printf("ERROR: Map_AddOrUpdate Failed!\r\n");
            }

            if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messages[iterator].messageHandle, SendConfirmationCallback, &messages[iterator]) != IOTHUB_CLIENT_OK)
            {
                (void)printf("ERROR: IoTHubClient_LL_SendEventAsync..........FAILED!\r\n");
            }
            else
            {
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission to IoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

<span data-ttu-id="5b86b-205">Ogni volta che si invia un messaggio, si specifica un riferimento a una funzione di callback che viene richiamata quando i dati vengono inviati.</span><span class="sxs-lookup"><span data-stu-id="5b86b-205">Every time you send a message, you specify a reference to a callback function that's invoked when the data is sent.</span></span> <span data-ttu-id="5b86b-206">In questo esempio la funzione di callback è denominata **SendConfirmationCallback**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-206">In this example, the callback function is called **SendConfirmationCallback**.</span></span> <span data-ttu-id="5b86b-207">Il frammento seguente illustra questa funzione di callback:</span><span class="sxs-lookup"><span data-stu-id="5b86b-207">The following snippet shows this callback function:</span></span>

```c
static void SendConfirmationCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    EVENT_INSTANCE* eventInstance = (EVENT_INSTANCE*)userContextCallback;
    (void)printf("Confirmation[%d] received for message tracking id = %zu with result = %s\r\n", callbackCounter, eventInstance->messageTrackingId, ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
    /* Some device specific action code goes here... */
    callbackCounter++;
    IoTHubMessage_Destroy(eventInstance->messageHandle);
}
```

<span data-ttu-id="5b86b-208">Si noti la chiamata alla funzione **IoTHubMessage\_Destroy** dopo il completamento dell'invio del messaggio.</span><span class="sxs-lookup"><span data-stu-id="5b86b-208">Note the call to the **IoTHubMessage\_Destroy** function when you're done with the message.</span></span> <span data-ttu-id="5b86b-209">Questa funzione libera le risorse allocate quando si crea il messaggio.</span><span class="sxs-lookup"><span data-stu-id="5b86b-209">This function frees the resources allocated when you created the message.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="5b86b-210">Ricevere messaggi</span><span class="sxs-lookup"><span data-stu-id="5b86b-210">Receive messages</span></span>

<span data-ttu-id="5b86b-211">La ricezione di un messaggio è un'operazione asincrona.</span><span class="sxs-lookup"><span data-stu-id="5b86b-211">Receiving a message is an asynchronous operation.</span></span> <span data-ttu-id="5b86b-212">Prima di tutto registrare il callback da richiamare quando il dispositivo riceve un messaggio:</span><span class="sxs-lookup"><span data-stu-id="5b86b-212">First, you register the callback to invoke when the device receives a message:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext) != IOTHUB_CLIENT_OK)
{
    (void)printf("ERROR: IoTHubClient_LL_SetMessageCallback..........FAILED!\r\n");
}
else
{
    (void)printf("IoTHubClient_LL_SetMessageCallback...successful.\r\n");
...
```

<span data-ttu-id="5b86b-213">L'ultimo parametro è un puntatore nullo a qualsiasi elemento.</span><span class="sxs-lookup"><span data-stu-id="5b86b-213">The last parameter is a void pointer to whatever you want.</span></span> <span data-ttu-id="5b86b-214">Nell'esempio è un puntatore a un intero, ma potrebbe essere un puntatore a una struttura dei dati più complessa.</span><span class="sxs-lookup"><span data-stu-id="5b86b-214">In the sample, it's a pointer to an integer but it could be a pointer to a more complex data structure.</span></span> <span data-ttu-id="5b86b-215">Questo parametro consente alla funzione di callback di operare in uno stato condiviso con il chiamante della funzione.</span><span class="sxs-lookup"><span data-stu-id="5b86b-215">This parameter enables the callback function to operate on shared state with the caller of this function.</span></span>

<span data-ttu-id="5b86b-216">Quando il dispositivo riceve un messaggio, viene richiamata la funzione di callback registrata.</span><span class="sxs-lookup"><span data-stu-id="5b86b-216">When the device receives a message, the registered callback function is invoked.</span></span> <span data-ttu-id="5b86b-217">Questa funzione di callback recupera:</span><span class="sxs-lookup"><span data-stu-id="5b86b-217">This callback function retrieves:</span></span>

* <span data-ttu-id="5b86b-218">L'ID messaggio e l'ID correlazione dal messaggio.</span><span class="sxs-lookup"><span data-stu-id="5b86b-218">The message id and correlation id from the message.</span></span>
* <span data-ttu-id="5b86b-219">Il contenuto del messaggio.</span><span class="sxs-lookup"><span data-stu-id="5b86b-219">The message content.</span></span>
* <span data-ttu-id="5b86b-220">Eventuali proprietà personalizzate dal messaggio.</span><span class="sxs-lookup"><span data-stu-id="5b86b-220">Any custom properties from the message.</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    int* counter = (int*)userContextCallback;
    const char* buffer;
    size_t size;
    MAP_HANDLE mapProperties;
    const char* messageId;
    const char* correlationId;

    // Message properties
    if ((messageId = IoTHubMessage_GetMessageId(message)) == NULL)
    {
        messageId = "<null>";
    }

    if ((correlationId = IoTHubMessage_GetCorrelationId(message)) == NULL)
    {
        correlationId = "<null>";
    }

    // Message content
    if (IoTHubMessage_GetByteArray(message, (const unsigned char**)&buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        (void)printf("unable to retrieve the message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive the work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from the message
    mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                size_t index;

                printf(" Message Properties:\r\n");
                for (index = 0; index < propertyCount; index++)
                {
                    (void)printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                (void)printf("\r\n");
            }
        }
    }

    /* Some device specific action code goes here... */
    (*counter)++;
    return IOTHUBMESSAGE_ACCEPTED;
}
```

<span data-ttu-id="5b86b-221">Usare la funzione **IoTHubMessage\_GetByteArray** per recuperare il messaggio, che in questo esempio è una stringa.</span><span class="sxs-lookup"><span data-stu-id="5b86b-221">Use the **IoTHubMessage\_GetByteArray** function to retrieve the message, which in this example is a string.</span></span>

### <a name="uninitialize-the-library"></a><span data-ttu-id="5b86b-222">Annullare l'inizializzazione della libreria</span><span class="sxs-lookup"><span data-stu-id="5b86b-222">Uninitialize the library</span></span>

<span data-ttu-id="5b86b-223">Al termine dell'invio degli eventi e della ricezione dei messaggi, è possibile annullare l'inizializzazione della libreria IoT.</span><span class="sxs-lookup"><span data-stu-id="5b86b-223">When you're done sending events and receiving messages, you can uninitialize the IoT library.</span></span> <span data-ttu-id="5b86b-224">A questo scopo, effettuare la chiamata di funzione seguente:</span><span class="sxs-lookup"><span data-stu-id="5b86b-224">To do so, issue the following function call:</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="5b86b-225">Questa chiamata libera le risorse allocate in precedenza dalla funzione **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-225">This call frees up the resources previously allocated by the **IoTHubClient\_CreateFromConnectionString** function.</span></span>

<span data-ttu-id="5b86b-226">Come si può vedere, è facile inviare e ricevere messaggi con la libreria **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-226">As you can see, it's easy to send and receive messages with the **IoTHubClient** library.</span></span> <span data-ttu-id="5b86b-227">La libreria gestisce i dettagli della comunicazione con l'hub IoT, ad esempio il protocollo da usare. Dal punto di vista dello sviluppatore, questa è una semplice opzione di configurazione.</span><span class="sxs-lookup"><span data-stu-id="5b86b-227">The library handles the details of communicating with IoT Hub, including which protocol to use (from the perspective of the developer, this is a simple configuration option).</span></span>

<span data-ttu-id="5b86b-228">La libreria **IoTHubClient** offre anche un controllo preciso della modalità di serializzazione dei dati che il dispositivo invia all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5b86b-228">The **IoTHubClient** library also provides precise control over how to serialize the data your device sends to IoT Hub.</span></span> <span data-ttu-id="5b86b-229">In alcuni casi questo livello di controllo rappresenta un vantaggio, ma in altri è un dettaglio di implementazione di cui si preferirebbe non occuparsi.</span><span class="sxs-lookup"><span data-stu-id="5b86b-229">In some cases this level of control is an advantage, but in others it is an implementation detail that you don't want to be concerned with.</span></span> <span data-ttu-id="5b86b-230">In questo caso, è possibile considerare l'uso della libreria **serializer**, che viene illustrata nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="5b86b-230">If that's the case, you might consider using the **serializer** library, which is described in the next section.</span></span>

## <a name="use-the-serializer-library"></a><span data-ttu-id="5b86b-231">Usare la libreria serializer</span><span class="sxs-lookup"><span data-stu-id="5b86b-231">Use the serializer library</span></span>

<span data-ttu-id="5b86b-232">A livello concettuale, la libreria **serializer** si basa sulla libreria **IoTHubClient** nell'SDK.</span><span class="sxs-lookup"><span data-stu-id="5b86b-232">Conceptually the **serializer** library sits on top of the **IoTHubClient** library in the SDK.</span></span> <span data-ttu-id="5b86b-233">Usa la libreria **IoTHubClient** per la comunicazione sottostante con l'hub IoT, ma aggiunge anche funzionalità di modellazione che consentono allo sviluppatore di evitare l'impegno di doversi occupare della serializzazione dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="5b86b-233">It uses the **IoTHubClient** library for the underlying communication with IoT Hub, but it adds modeling capabilities that remove the burden of dealing with message serialization from the developer.</span></span> <span data-ttu-id="5b86b-234">Il funzionamento di questa libreria può essere illustrato meglio con un esempio.</span><span class="sxs-lookup"><span data-stu-id="5b86b-234">How this library works is best demonstrated by an example.</span></span>

<span data-ttu-id="5b86b-235">Nella cartella **serializer** del [repository azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c) è presente una cartella **samples** che contiene un'applicazione denominata **simplesample\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-235">Inside the **serializer** folder in the [azure-iot-sdk-c repository](https://github.com/Azure/azure-iot-sdk-c), is a **samples** folder that contains an application called **simplesample\_mqtt**.</span></span> <span data-ttu-id="5b86b-236">La versione per Windows di questo esempio include la soluzione di Visual Studio seguente:</span><span class="sxs-lookup"><span data-stu-id="5b86b-236">The Windows version of this sample includes the following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="5b86b-237">Se si apre questo progetto in Visual Studio 2017, accettare la richiesta di ridestinare il progetto alla versione più recente.</span><span class="sxs-lookup"><span data-stu-id="5b86b-237">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span></span>

<span data-ttu-id="5b86b-238">Come con l'esempio precedente, questo include diversi pacchetti NuGet:</span><span class="sxs-lookup"><span data-stu-id="5b86b-238">As with the previous sample, this one includes several NuGet packages:</span></span>

* <span data-ttu-id="5b86b-239">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="5b86b-239">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="5b86b-240">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="5b86b-240">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="5b86b-241">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="5b86b-241">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="5b86b-242">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="5b86b-242">Microsoft.Azure.IoTHub.Serializer</span></span>
* <span data-ttu-id="5b86b-243">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="5b86b-243">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="5b86b-244">La maggior parte di questi pacchetti è stata illustrata nell'esempio precedente, ma **Microsoft.Azure.IoTHub.Serializer** è nuovo.</span><span class="sxs-lookup"><span data-stu-id="5b86b-244">You've seen most of these packages in the previous sample, but **Microsoft.Azure.IoTHub.Serializer** is new.</span></span> <span data-ttu-id="5b86b-245">Questo pacchetto è necessario quando si usa la libreria **serializer**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-245">This package is required when you use the **serializer** library.</span></span>

<span data-ttu-id="5b86b-246">L'implementazione dell'applicazione di esempio si trova nel file **simplesample\_mqtt.c**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-246">You can find the implementation of the sample application in the **simplesample\_mqtt.c** file.</span></span>

<span data-ttu-id="5b86b-247">Le sezioni seguenti illustrano gli elementi chiave di questo esempio.</span><span class="sxs-lookup"><span data-stu-id="5b86b-247">The following sections walk you through the key parts of this sample.</span></span>

### <a name="initialize-the-library"></a><span data-ttu-id="5b86b-248">Inizializzare la libreria</span><span class="sxs-lookup"><span data-stu-id="5b86b-248">Initialize the library</span></span>

<span data-ttu-id="5b86b-249">Per iniziare a lavorare con la libreria **serializer**, chiamare le API di inizializzazione:</span><span class="sxs-lookup"><span data-stu-id="5b86b-249">To start working with the **serializer** library, call the initialization APIs:</span></span>

```c
if (serializer_init(NULL) != SERIALIZER_OK)
{
    (void)printf("Failed on serializer_init\r\n");
}
else
{
    IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol);
    srand((unsigned int)time(NULL));
    int avgWindSpeed = 10;

    if (iotHubClientHandle == NULL)
    {
        (void)printf("Failed on IoTHubClient_LL_Create\r\n");
    }
    else
    {
        ContosoAnemometer* myWeather = CREATE_MODEL_INSTANCE(WeatherStation, ContosoAnemometer);
        if (myWeather == NULL)
        {
            (void)printf("Failed on CREATE_MODEL_INSTANCE\r\n");
        }
        else
        {
...
```

<span data-ttu-id="5b86b-250">La chiamata alla funzione **serializer\_init** è una chiamata singola e inizializza la libreria sottostante.</span><span class="sxs-lookup"><span data-stu-id="5b86b-250">The call to the **serializer\_init** function is a one-time call and initializes the underlying library.</span></span> <span data-ttu-id="5b86b-251">Si chiamerà quindi la funzione **IoTHubClient\_LL\_CreateFromConnectionString**, che è la stessa API presente nell'esempio **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-251">Then, you call the **IoTHubClient\_LL\_CreateFromConnectionString** function, which is the same API as in the **IoTHubClient** sample.</span></span> <span data-ttu-id="5b86b-252">Questa chiamata imposta la stringa di connessione del dispositivo e consente anche di scegliere il protocollo da usare.</span><span class="sxs-lookup"><span data-stu-id="5b86b-252">This call sets your device connection string (this call is also where you choose the protocol you want to use).</span></span> <span data-ttu-id="5b86b-253">Questo esempio usa MQTT come trasporto, ma potrebbe usare AMQP o HTTP.</span><span class="sxs-lookup"><span data-stu-id="5b86b-253">This sample uses MQTT as the transport, but could use AMQP or HTTP.</span></span>

<span data-ttu-id="5b86b-254">Chiamare infine la funzione **CREATE\_MODEL\_INSTANCE**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-254">Finally, call the **CREATE\_MODEL\_INSTANCE** function.</span></span> <span data-ttu-id="5b86b-255">**WeatherStation** è lo spazio dei nomi del modello e **ContosoAnemometer** è il nome del modello.</span><span class="sxs-lookup"><span data-stu-id="5b86b-255">**WeatherStation** is the namespace of the model and **ContosoAnemometer** is the name of the model.</span></span> <span data-ttu-id="5b86b-256">Dopo la creazione dell'istanza del modello, è possibile usarla per iniziare a inviare e ricevere messaggi.</span><span class="sxs-lookup"><span data-stu-id="5b86b-256">Once the model instance is created, you can use it to start sending and receiving messages.</span></span> <span data-ttu-id="5b86b-257">Prima è però importante comprendere che cos'è un modello.</span><span class="sxs-lookup"><span data-stu-id="5b86b-257">However, it's important to understand what a model is.</span></span>

### <a name="define-the-model"></a><span data-ttu-id="5b86b-258">Definire il modello</span><span class="sxs-lookup"><span data-stu-id="5b86b-258">Define the model</span></span>

<span data-ttu-id="5b86b-259">Un modello nella libreria **serializer** definisce i messaggi che il dispositivo può inviare all'hub IoT e i messaggi, chiamati *azioni* nel linguaggio di modellazione, che può ricevere.</span><span class="sxs-lookup"><span data-stu-id="5b86b-259">A model in the **serializer** library defines the messages that your device can send to IoT Hub and the messages, called *actions* in the modeling language, which it can receive.</span></span> <span data-ttu-id="5b86b-260">Per definire un modello, usare un set di macro C come nell'applicazione di esempio **simplesample\_mqtt**:</span><span class="sxs-lookup"><span data-stu-id="5b86b-260">You define a model using a set of C macros as in the **simplesample\_mqtt** sample application:</span></span>

```c
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(int, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

<span data-ttu-id="5b86b-261">Le macro **BEGIN\_NAMESPACE** ed **END\_NAMESPACE** accettano entrambe lo spazio dei nomi del modello come argomento.</span><span class="sxs-lookup"><span data-stu-id="5b86b-261">The **BEGIN\_NAMESPACE** and **END\_NAMESPACE** macros both take the namespace of the model as an argument.</span></span> <span data-ttu-id="5b86b-262">Tutto ciò che si trova tra queste macro è la definizione del modello o dei modelli e le strutture dei dati usate dal modello.</span><span class="sxs-lookup"><span data-stu-id="5b86b-262">It's expected that anything between these macros is the definition of your model or models, and the data structures that the models use.</span></span>

<span data-ttu-id="5b86b-263">In questo esempio è presente un singolo modello chiamato **ContosoAnemometer**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-263">In this example, there is a single model called **ContosoAnemometer**.</span></span> <span data-ttu-id="5b86b-264">Questo modello definisce due parti di dati che il dispositivo può inviare all'hub IoT, ovvero **DeviceId** e **WindSpeed**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-264">This model defines two pieces of data that your device can send to IoT Hub: **DeviceId** and **WindSpeed**.</span></span> <span data-ttu-id="5b86b-265">Definisce anche tre azioni (messaggi) che il dispositivo può ricevere, cioè **TurnFanOn**, **TurnFanOff** e **SetAirResistance**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-265">It also defines three actions (messages) that your device can receive: **TurnFanOn**, **TurnFanOff**, and **SetAirResistance**.</span></span> <span data-ttu-id="5b86b-266">Ogni elemento dati ha un tipo e ogni azione un nome e facoltativamente un set di parametri.</span><span class="sxs-lookup"><span data-stu-id="5b86b-266">Each data element has a type, and each action has a name (and optionally a set of parameters).</span></span>

<span data-ttu-id="5b86b-267">I dati e le azioni specificati nel modello definiscono una superficie dell'API che si può usare per inviare messaggi all'hub IoT e per rispondere ai messaggi inviati al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5b86b-267">The data and actions defined in the model define an API surface that you can use to send messages to IoT Hub, and respond to messages sent to the device.</span></span> <span data-ttu-id="5b86b-268">L'uso di questo modello può essere illustrato meglio con un esempio.</span><span class="sxs-lookup"><span data-stu-id="5b86b-268">Use of this model is best understood through an example.</span></span>

### <a name="send-messages"></a><span data-ttu-id="5b86b-269">Inviare messaggi</span><span class="sxs-lookup"><span data-stu-id="5b86b-269">Send messages</span></span>

<span data-ttu-id="5b86b-270">Il modello definisce i dati che è possibile inviare all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5b86b-270">The model defines the data you can send to IoT Hub.</span></span> <span data-ttu-id="5b86b-271">In questo esempio è uno dei due elementi dati definiti con la macro **WITH_DATA**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-271">In this example, that means one of the two data items defined using the **WITH_DATA** macro.</span></span> <span data-ttu-id="5b86b-272">Sono necessari diversi passaggi per inviare i valori **DeviceId** e **WindSpeed** a un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5b86b-272">There are several steps required to send **DeviceId** and **WindSpeed** values to an IoT hub.</span></span> <span data-ttu-id="5b86b-273">Il primo consiste nell'impostare i dati da inviare:</span><span class="sxs-lookup"><span data-stu-id="5b86b-273">The first is to set the data you want to send:</span></span>

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

<span data-ttu-id="5b86b-274">Il modello definito prima consente di impostare i valori impostando i membri di una **struct**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-274">The model you defined earlier enables you to set the values by setting members of a **struct**.</span></span> <span data-ttu-id="5b86b-275">Serializzare quindi il messaggio che si vuole inviare:</span><span class="sxs-lookup"><span data-stu-id="5b86b-275">Next, serialize the message you want to send:</span></span>

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed to serialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

<span data-ttu-id="5b86b-276">Questo codice serializza il passaggio da dispositivo a cloud in un buffer, detto **destination**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-276">This code serializes the device-to-cloud to a buffer (referenced by **destination**).</span></span> <span data-ttu-id="5b86b-277">Il codice richiama quindi la funzione **sendMessage** per inviare il messaggio all'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="5b86b-277">The code then invokes the **sendMessage** function to send the message to IoT Hub:</span></span>

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable to create a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed to hand over the message to IoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted the message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


<span data-ttu-id="5b86b-278">Il penultimo parametro di **IoTHubClient\_LL\_SendEventAsync** è un riferimento a una funzione di callback chiamata dopo che l'invio dei dati è riuscito.</span><span class="sxs-lookup"><span data-stu-id="5b86b-278">The second to last parameter of **IoTHubClient\_LL\_SendEventAsync** is a reference to a callback function that's called when the data is successfully sent.</span></span> <span data-ttu-id="5b86b-279">Ecco la funzione di callback nell'esempio:</span><span class="sxs-lookup"><span data-stu-id="5b86b-279">Here's the callback function in the sample:</span></span>

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

<span data-ttu-id="5b86b-280">Il secondo parametro è un puntatore al contesto utente, lo stesso puntatore passato a **IoTHubClient\_LL\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-280">The second parameter is a pointer to user context; the same pointer passed to **IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="5b86b-281">In questo caso, il contesto è un semplice contatore, ma potrebbe essere qualsiasi altro elemento.</span><span class="sxs-lookup"><span data-stu-id="5b86b-281">In this case, the context is a simple counter, but it can be anything you want.</span></span>

<span data-ttu-id="5b86b-282">Non sono necessarie altre operazioni per l'invio di messaggi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="5b86b-282">That's all there is to sending device-to-cloud messages.</span></span> <span data-ttu-id="5b86b-283">Rimane solo da illustrare come ricevere i messaggi.</span><span class="sxs-lookup"><span data-stu-id="5b86b-283">The only thing left to cover is how to receive messages.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="5b86b-284">Ricevere messaggi</span><span class="sxs-lookup"><span data-stu-id="5b86b-284">Receive messages</span></span>

<span data-ttu-id="5b86b-285">La ricezione di un messaggi funziona in modo simile alla modalità d'uso dei messaggi nella libreria **IoTHubClient** .</span><span class="sxs-lookup"><span data-stu-id="5b86b-285">Receiving a message works similarly to the way messages work in the **IoTHubClient** library.</span></span> <span data-ttu-id="5b86b-286">Prima di tutto occorre registrare la funzione di callback di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="5b86b-286">First, you register a message callback function:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable to IoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

<span data-ttu-id="5b86b-287">Si scrive quindi la funzione di callback che viene richiamata alla ricezione di un messaggio:</span><span class="sxs-lookup"><span data-stu-id="5b86b-287">Then, you write the callback function that's invoked when a message is received:</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable to IoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed to malloc\r\n");
            result = IOTHUBMESSAGE_ABANDONED;
        }
        else
        {
            (void)memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

<span data-ttu-id="5b86b-288">Questo codice è un boilerplate, ovvero è lo stesso per qualsiasi soluzione.</span><span class="sxs-lookup"><span data-stu-id="5b86b-288">This code is boilerplate -- it's the same for any solution.</span></span> <span data-ttu-id="5b86b-289">La funzione riceve il messaggio e si occupa del routing alla funzione appropriata tramite la chiamata a **EXECUTE\_COMMAND**.</span><span class="sxs-lookup"><span data-stu-id="5b86b-289">This function receives the message and takes care of routing it to the appropriate function through the call to **EXECUTE\_COMMAND**.</span></span> <span data-ttu-id="5b86b-290">La funzione chiamata a questo punto dipende della definizione delle azioni nel modello.</span><span class="sxs-lookup"><span data-stu-id="5b86b-290">The function called at this point depends on the definition of the actions in your model.</span></span>

<span data-ttu-id="5b86b-291">Quando si definisce un'azione nel modello, viene richiesto di implementare una funzione che viene chiamata quando il dispositivo riceve il messaggio corrispondente.</span><span class="sxs-lookup"><span data-stu-id="5b86b-291">When you define an action in your model, you're required to implement a function that's called when your device receives the corresponding message.</span></span> <span data-ttu-id="5b86b-292">Ad esempio, se il modello definisce questa azione:</span><span class="sxs-lookup"><span data-stu-id="5b86b-292">For example, if your model defines this action:</span></span>

```c
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="5b86b-293">Definire una funzione con questa firma:</span><span class="sxs-lookup"><span data-stu-id="5b86b-293">Define a function with this signature:</span></span>

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position to %d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="5b86b-294">Si noti come il nome della funzione corrisponda al nome dell'azione nel modello e che i parametri della funzione corrispondono a quelli specificati per l'azione.</span><span class="sxs-lookup"><span data-stu-id="5b86b-294">Note how the name of the function matches the name of the action in the model and that the parameters of the function match the parameters specified for the action.</span></span> <span data-ttu-id="5b86b-295">Il primo parametro è sempre obbligatorio e contiene un puntatore all'istanza del modello.</span><span class="sxs-lookup"><span data-stu-id="5b86b-295">The first parameter is always required and contains a pointer to the instance of your model.</span></span>

<span data-ttu-id="5b86b-296">Quando il dispositivo riceve un messaggio che corrisponde alla firma, viene chiamata la funzione corrispondente.</span><span class="sxs-lookup"><span data-stu-id="5b86b-296">When the device receives a message that matches this signature, the corresponding function is called.</span></span> <span data-ttu-id="5b86b-297">Quindi, a parte la necessità di includere il codice boilerplate da **IoTHubMessage**, per la ricezione dei messaggi si tratta solo di definire una semplice funzione per ogni azione definita nel modello.</span><span class="sxs-lookup"><span data-stu-id="5b86b-297">Therefore, aside from having to include the boilerplate code from **IoTHubMessage**, receiving messages is just a matter of defining a simple function for each action defined in your model.</span></span>

### <a name="uninitialize-the-library"></a><span data-ttu-id="5b86b-298">Annullare l'inizializzazione della libreria</span><span class="sxs-lookup"><span data-stu-id="5b86b-298">Uninitialize the library</span></span>

<span data-ttu-id="5b86b-299">Dopo avere completato l'invio dei dati e la ricezione di messaggi, è possibile annullare l'inizializzazione della libreria IoT:</span><span class="sxs-lookup"><span data-stu-id="5b86b-299">When you're done sending data and receiving messages, you can uninitialize the IoT library:</span></span>

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

<span data-ttu-id="5b86b-300">Ognuna di queste tre funzioni è allineata con le tre funzioni di inizializzazione descritte in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5b86b-300">Each of these three functions aligns with the three initialization functions described previously.</span></span> <span data-ttu-id="5b86b-301">Chiamando questi API si assicura che siano liberate le risorse allocate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5b86b-301">Calling these APIs ensures that you free previously allocated resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b86b-302">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5b86b-302">Next Steps</span></span>

<span data-ttu-id="5b86b-303">Questo articolo descrive le nozioni di base relative all'uso delle librerie in **Azure IoT SDK per dispositivi per C**. Fornisce informazioni sufficienti per comprendere il contenuto dell'SDK, la relativa architettura e come iniziare a usare gli esempi per Windows.</span><span class="sxs-lookup"><span data-stu-id="5b86b-303">This article covered the basics of using the libraries in the **Azure IoT device SDK for C**. It provided you with enough information to understand what's included in the SDK, its architecture, and how to get started working with the Windows samples.</span></span> <span data-ttu-id="5b86b-304">L'articolo successivo continua la descrizione dell'SDK, fornendo [altre informazioni sulla libreria IoTHubClient](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="5b86b-304">The next article continues the description of the SDK by explaining [more about the IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span></span>

<span data-ttu-id="5b86b-305">Per altre informazioni sullo sviluppo dell'hub IoT, vedere gli [Azure IoT SDK][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="5b86b-305">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="5b86b-306">Per altre informazioni sulle funzionalità dell'hub IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="5b86b-306">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="5b86b-307">[Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="5b86b-307">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
