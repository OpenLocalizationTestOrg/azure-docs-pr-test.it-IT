---
title: il dispositivo di Azure IoT aaaThe SDK per C | Documenti Microsoft
description: Iniziare con il dispositivo di Azure IoT hello SDK per C e informazioni su come le App per dispositivi toocreate che comunicano con un hub IoT.
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
ms.openlocfilehash: 9e20742e6ea513c124bfaf28f02f6fba86170daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c"></a><span data-ttu-id="baea7-103">Azure IoT SDK per dispositivi per C</span><span class="sxs-lookup"><span data-stu-id="baea7-103">Azure IoT device SDK for C</span></span>

<span data-ttu-id="baea7-104">Hello **dispositivo IoT di Azure SDK** è un set di librerie progettato processo hello toosimplify di invio di messaggi tooand ricezione di messaggi da hello **IoT Hub Azure** servizio.</span><span class="sxs-lookup"><span data-stu-id="baea7-104">hello **Azure IoT device SDK** is a set of libraries designed toosimplify hello process of sending messages tooand receiving messages from hello **Azure IoT Hub** service.</span></span> <span data-ttu-id="baea7-105">Sono disponibili diverse varianti di hello SDK, ogni destinazione una piattaforma specifica, ma in questo articolo descrive hello **dispositivo IoT di Azure SDK per C**.</span><span class="sxs-lookup"><span data-stu-id="baea7-105">There are different variations of hello SDK, each targeting a specific platform, but this article describes hello **Azure IoT device SDK for C**.</span></span>

<span data-ttu-id="baea7-106">il dispositivo di Azure IoT Hello SDK per C viene scritta in ANSI C (C99) toomaximize portabilità.</span><span class="sxs-lookup"><span data-stu-id="baea7-106">hello Azure IoT device SDK for C is written in ANSI C (C99) toomaximize portability.</span></span> <span data-ttu-id="baea7-107">Questa funzionalità rende toooperate ideale di librerie hello su più piattaforme e dispositivi, in particolare quando riducendo al minimo su disco e footprint di memoria è una priorità.</span><span class="sxs-lookup"><span data-stu-id="baea7-107">This feature makes hello libraries well-suited toooperate on multiple platforms and devices, especially where minimizing disk and memory footprint is a priority.</span></span>

<span data-ttu-id="baea7-108">Sono disponibili un'ampia gamma di piattaforme in cui hello SDK è stato testato (vedere hello [Azure Certified per catalogo dispositivo IoT](https://catalog.azureiotsuite.com/) per informazioni dettagliate).</span><span class="sxs-lookup"><span data-stu-id="baea7-108">There are a broad range of platforms on which hello SDK has been tested (see hello [Azure Certified for IoT device catalog](https://catalog.azureiotsuite.com/) for details).</span></span> <span data-ttu-id="baea7-109">Sebbene in questo articolo include procedure dettagliate di codice di esempio in esecuzione nella piattaforma Windows hello, codice hello descritto in questo articolo è identico per intervallo hello delle piattaforme supportate.</span><span class="sxs-lookup"><span data-stu-id="baea7-109">Although this article includes walkthroughs of sample code running on hello Windows platform, hello code described in this article is identical across hello range of supported platforms.</span></span>

<span data-ttu-id="baea7-110">In questo articolo viene illustrata toohello architettura del dispositivo di Azure IoT hello SDK per C. Viene illustrato come inviare dati tooIoT Hub libreria dispositivi di hello tooinitialize e ricevere messaggi da esso.</span><span class="sxs-lookup"><span data-stu-id="baea7-110">This article introduces you toohello architecture of hello Azure IoT device SDK for C. It demonstrates how tooinitialize hello device library, send data tooIoT Hub, and receive messages from it.</span></span> <span data-ttu-id="baea7-111">informazioni di Hello in questo articolo dovrebbero essere sufficiente tooget avviato utilizzando hello SDK, ma fornisce anche informazioni tooadditional puntatori sulle librerie hello.</span><span class="sxs-lookup"><span data-stu-id="baea7-111">hello information in this article should be enough tooget started using hello SDK, but also provides pointers tooadditional information about hello libraries.</span></span>

## <a name="sdk-architecture"></a><span data-ttu-id="baea7-112">Architettura dell'SDK</span><span class="sxs-lookup"><span data-stu-id="baea7-112">SDK architecture</span></span>

<span data-ttu-id="baea7-113">È possibile trovare hello [ **dispositivo IoT di Azure SDK per C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repository e visualizzarne i dettagli di hello API in hello [riferimento all'API C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="baea7-113">You can find hello [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of hello API in hello [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

<span data-ttu-id="baea7-114">sono disponibili più recente delle librerie di hello Hello in hello **master** ramo del repository hello:</span><span class="sxs-lookup"><span data-stu-id="baea7-114">hello latest version of hello libraries can be found in hello **master** branch of hello repository:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* <span data-ttu-id="baea7-115">Hello core implementazione di hello SDK è hello **l'hub IOT\_client** cartella che contiene l'implementazione di hello del livello API minimo di hello in hello SDK: hello **IoTHubClient** libreria.</span><span class="sxs-lookup"><span data-stu-id="baea7-115">hello core implementation of hello SDK is in hello **iothub\_client** folder that contains hello implementation of hello lowest API layer in hello SDK: hello **IoTHubClient** library.</span></span> <span data-ttu-id="baea7-116">Hello **IoTHubClient** libreria contiene le API di messaggistica non elaborato per l'invio di messaggi tooIoT Hub e la ricezione di messaggi dall'IoT Hub di implementazione.</span><span class="sxs-lookup"><span data-stu-id="baea7-116">hello **IoTHubClient** library contains APIs implementing raw messaging for sending messages tooIoT Hub and receiving messages from IoT Hub.</span></span> <span data-ttu-id="baea7-117">Quando si usa questa libreria, si dovrà implementare la serializzazione dei messaggi, mente gli altri dettagli della comunicazione con l'hub IoT vengono gestiti automaticamente.</span><span class="sxs-lookup"><span data-stu-id="baea7-117">When using this library, you are responsible for implementing message serialization, but other details of communicating with IoT Hub are handled for you.</span></span>
* <span data-ttu-id="baea7-118">Hello **serializzatore** cartella contiene funzioni di supporto ed esempi che illustrano come dati tooserialize prima dell'invio tramite Hub IoT tooAzure hello libreria client.</span><span class="sxs-lookup"><span data-stu-id="baea7-118">hello **serializer** folder contains helper functions and samples that show you how tooserialize data before sending tooAzure IoT Hub using hello client library.</span></span> <span data-ttu-id="baea7-119">utilizzo di Hello del serializzatore hello non è obbligatorio e viene fornita per praticità.</span><span class="sxs-lookup"><span data-stu-id="baea7-119">hello use of hello serializer is not mandatory and is provided as a convenience.</span></span> <span data-ttu-id="baea7-120">hello toouse **serializzatore** library, si definisce un modello che specifica dati toosend tooIoT Hub e hello messaggi hello previsto tooreceive da esso.</span><span class="sxs-lookup"><span data-stu-id="baea7-120">toouse hello **serializer** library, you define a model that specifies hello data toosend tooIoT Hub and hello messages you expect tooreceive from it.</span></span> <span data-ttu-id="baea7-121">Una volta definito il modello di hello, hello SDK vengono fornite con una superficie API che consente di lavoro tooeasily da dispositivo a cloud e i messaggi da cloud a dispositivo senza doversi preoccupare hello dettagli di serializzazione.</span><span class="sxs-lookup"><span data-stu-id="baea7-121">Once hello model is defined, hello SDK provides you with an API surface that enables you tooeasily work with device-to-cloud and cloud-to-device messages without worrying about hello serialization details.</span></span> <span data-ttu-id="baea7-122">libreria Hello dipende dalle altre librerie open source che implementano il trasporto utilizzando i protocolli, ad esempio MQTT e AMQP.</span><span class="sxs-lookup"><span data-stu-id="baea7-122">hello library depends on other open source libraries that implement transport using protocols such as MQTT and AMQP.</span></span>
* <span data-ttu-id="baea7-123">Hello **IoTHubClient** libreria dipende da altre librerie open source:</span><span class="sxs-lookup"><span data-stu-id="baea7-123">hello **IoTHubClient** library depends on other open source libraries:</span></span>
  * <span data-ttu-id="baea7-124">Hello [C Azure condiviso utilità](https://github.com/Azure/azure-c-shared-utility) libreria, che fornisce funzionalità comuni per le attività di base (ad esempio stringhe, la modifica di elenco e i/o) necessaria per molti SDK C correlate ad Azure.</span><span class="sxs-lookup"><span data-stu-id="baea7-124">hello [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility) library, which provides common functionality for basic tasks (such as strings, list manipulation, and IO) needed across several Azure-related C SDKs.</span></span>
  * <span data-ttu-id="baea7-125">Hello [uAMQP Azure](https://github.com/Azure/azure-uamqp-c) libreria, è un'implementazione sul lato client di AMQP ottimizzate per i dispositivi di risorse sufficienti.</span><span class="sxs-lookup"><span data-stu-id="baea7-125">hello [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) library, which is a client-side implementation of AMQP optimized for resource constrained devices.</span></span>
  * <span data-ttu-id="baea7-126">Hello [uMQTT Azure](https://github.com/Azure/azure-umqtt-c) libreria che è una raccolta generica che implementa il protocollo MQTT hello e ottimizzate per i dispositivi di risorse sufficienti.</span><span class="sxs-lookup"><span data-stu-id="baea7-126">hello [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) library, which is a general-purpose library implementing hello MQTT protocol and optimized for resource constrained devices.</span></span>

<span data-ttu-id="baea7-127">Utilizzo di queste librerie è più facile toounderstand esaminando il codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="baea7-127">Use of these libraries is easier toounderstand by looking at example code.</span></span> <span data-ttu-id="baea7-128">Hello le sezioni seguenti consentono di eseguire molte delle applicazioni di esempio hello inclusi in hello SDK.</span><span class="sxs-lookup"><span data-stu-id="baea7-128">hello following sections walk you through several of hello sample applications that are included in hello SDK.</span></span> <span data-ttu-id="baea7-129">Viene fornito in questa procedura dettagliata una buona ritiene per hello varie funzionalità di livelli dell'architettura di hello di hello SDK e un hello toohow introduzione API funzionano.</span><span class="sxs-lookup"><span data-stu-id="baea7-129">This walkthrough should give you a good feel for hello various capabilities of hello architectural layers of hello SDK and an introduction toohow hello APIs work.</span></span>

## <a name="before-you-run-hello-samples"></a><span data-ttu-id="baea7-130">Prima di eseguire gli esempi di hello</span><span class="sxs-lookup"><span data-stu-id="baea7-130">Before you run hello samples</span></span>

<span data-ttu-id="baea7-131">Prima di eseguire gli esempi di hello in dispositivi Azure IoT hello SDK per C, è necessario [creare un'istanza del servizio dell'IoT Hub hello](iot-hub-create-through-portal.md) nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="baea7-131">Before you can run hello samples in hello Azure IoT device SDK for C, you must [create an instance of hello IoT Hub service](iot-hub-create-through-portal.md) in your Azure subscription.</span></span> <span data-ttu-id="baea7-132">Completare quindi hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="baea7-132">Then complete hello following tasks:</span></span>

* <span data-ttu-id="baea7-133">Preparare l'ambiente di sviluppo</span><span class="sxs-lookup"><span data-stu-id="baea7-133">Prepare your development environment</span></span>
* <span data-ttu-id="baea7-134">Ottenere le credenziali del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="baea7-134">Obtain device credentials.</span></span>

### <a name="prepare-your-development-environment"></a><span data-ttu-id="baea7-135">Preparare l'ambiente di sviluppo</span><span class="sxs-lookup"><span data-stu-id="baea7-135">Prepare your development environment</span></span>

<span data-ttu-id="baea7-136">I pacchetti vengono forniti per le piattaforme comune (ad esempio NuGet per Windows o apt_get per Debian e Ubuntu) e gli esempi di hello utilizzano questi pacchetti, se disponibile.</span><span class="sxs-lookup"><span data-stu-id="baea7-136">Packages are provided for common platforms (such as NuGet for Windows or apt_get for Debian and Ubuntu) and hello samples use these packages when available.</span></span> <span data-ttu-id="baea7-137">In alcuni casi, è necessario toocompile hello SDK per o nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="baea7-137">In some cases, you need toocompile hello SDK for or on your device.</span></span> <span data-ttu-id="baea7-138">Se è necessario toocompile hello SDK, vedere [preparare l'ambiente di sviluppo](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) nel repository GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="baea7-138">If you need toocompile hello SDK, see [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in hello GitHub repository.</span></span>

<span data-ttu-id="baea7-139">codice dell'applicazione esempio hello tooobtain, scaricare una copia di hello SDK da GitHub.</span><span class="sxs-lookup"><span data-stu-id="baea7-139">tooobtain hello sample application code, download a copy of hello SDK from GitHub.</span></span> <span data-ttu-id="baea7-140">Ottenere la copia di origine hello da hello **master** ramo di hello [repository GitHub](https://github.com/Azure/azure-iot-sdk-c).</span><span class="sxs-lookup"><span data-stu-id="baea7-140">Get your copy of hello source from hello **master** branch of hello [GitHub repository](https://github.com/Azure/azure-iot-sdk-c).</span></span>


### <a name="obtain-hello-device-credentials"></a><span data-ttu-id="baea7-141">Ottenere le credenziali di dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="baea7-141">Obtain hello device credentials</span></span>

<span data-ttu-id="baea7-142">Ora che si dispone di codice sorgente dell'esempio hello, hello Avanti cosa toodo è tooget un insieme di credenziali di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="baea7-142">Now that you have hello sample source code, hello next thing toodo is tooget a set of device credentials.</span></span> <span data-ttu-id="baea7-143">Per un dispositivo toobe in grado di tooaccess un hub IoT, è innanzitutto necessario aggiungere hello dispositivo toohello del Registro di sistema di IoT Hub identità.</span><span class="sxs-lookup"><span data-stu-id="baea7-143">For a device toobe able tooaccess an IoT hub, you must first add hello device toohello IoT Hub identity registry.</span></span> <span data-ttu-id="baea7-144">Quando si aggiunge il dispositivo, ottenere un set di credenziali per un dispositivo che è necessario per l'hub IoT di hello dispositivo toobe tooconnect in grado di toohello.</span><span class="sxs-lookup"><span data-stu-id="baea7-144">When you add your device, you get a set of device credentials that you need for hello device toobe able tooconnect toohello IoT hub.</span></span> <span data-ttu-id="baea7-145">applicazioni di esempio Hello descritte nella sezione successiva hello prevede che le credenziali sotto forma di hello di un **stringa di connessione dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="baea7-145">hello sample applications discussed in hello next section expect these credentials in hello form of a **device connection string**.</span></span>

<span data-ttu-id="baea7-146">Esistono diversi toohelp di strumenti Apri origine si gestione l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="baea7-146">There are several open source tools toohelp you manage your IoT hub.</span></span>

* <span data-ttu-id="baea7-147">Un'applicazione Windows denominata [Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="baea7-147">A Windows application called [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>
* <span data-ttu-id="baea7-148">Uno strumento dell'interfaccia della riga di comando di node.js multipiattaforma denominato [iothub-explorer](https://github.com/azure/iothub-explorer).</span><span class="sxs-lookup"><span data-stu-id="baea7-148">A cross-platform node.js CLI tool called [iothub-explorer](https://github.com/azure/iothub-explorer).</span></span>

<span data-ttu-id="baea7-149">Questa esercitazione viene utilizzato con interfaccia grafica hello *Esplora dispositivo* strumento.</span><span class="sxs-lookup"><span data-stu-id="baea7-149">This tutorial uses hello graphical *device explorer* tool.</span></span> <span data-ttu-id="baea7-150">È inoltre possibile utilizzare hello *l'hub IOT Esplora* strumento se si preferisce uno strumento CLI toouse.</span><span class="sxs-lookup"><span data-stu-id="baea7-150">You can also use hello *iothub-explorer* tool if you prefer toouse a CLI tool.</span></span>

<span data-ttu-id="baea7-151">strumenti di Esplora Hello dispositivo utilizza hello Azure IoT servizio librerie tooperform varie funzioni nell'IoT Hub, inclusa l'aggiunta di dispositivi.</span><span class="sxs-lookup"><span data-stu-id="baea7-151">hello device explorer tool uses hello Azure IoT service libraries tooperform various functions on IoT Hub, including adding devices.</span></span> <span data-ttu-id="baea7-152">Se si utilizza hello dispositivo Esplora strumento tooadd un dispositivo, si ottiene una stringa di connessione per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="baea7-152">If you use hello device explorer tool tooadd a device, you get a connection string for your device.</span></span> <span data-ttu-id="baea7-153">È necessario questo applicazioni di esempio hello toorun stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="baea7-153">You need this connection string toorun hello sample applications.</span></span>

<span data-ttu-id="baea7-154">Se non si ha familiarità con lo strumento Esplora dispositivo di hello, hello seguente procedura descrive come toouse è tooadd un dispositivo e ottenere una stringa di connessione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="baea7-154">If you're not familiar with hello device explorer tool, hello following procedure describes how toouse it tooadd a device and obtain a device connection string.</span></span>

<span data-ttu-id="baea7-155">strumento di explorer tooinstall hello dispositivo, vedere [come toouse hello Esplora dispositivo per i dispositivi IoT Hub](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="baea7-155">tooinstall hello device explorer tool, see [How toouse hello Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>

<span data-ttu-id="baea7-156">Quando si esegue il programma hello, viene visualizzato di questa interfaccia:</span><span class="sxs-lookup"><span data-stu-id="baea7-156">When you run hello program, you see this interface:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

<span data-ttu-id="baea7-157">Immettere il **stringa di connessione Hub IoT** in hello primo campo e fare clic su **aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="baea7-157">Enter your **IoT Hub Connection String** in hello first field and click **Update**.</span></span> <span data-ttu-id="baea7-158">Questo passaggio Configura strumento hello in modo che possa comunicare con l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="baea7-158">This step configures hello tool so that it can communicate with IoT Hub.</span></span>

<span data-ttu-id="baea7-159">Quando la stringa di connessione IoT Hub hello è configurato, fare clic su hello **gestione** scheda:</span><span class="sxs-lookup"><span data-stu-id="baea7-159">When hello IoT Hub connection string is configured, click hello **Management** tab:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

<span data-ttu-id="baea7-160">Questa scheda è possibile gestire i dispositivi hello registrati nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="baea7-160">This tab is where you manage hello devices registered in your IoT hub.</span></span>

<span data-ttu-id="baea7-161">Per creare un dispositivo scegliere hello **crea** pulsante.</span><span class="sxs-lookup"><span data-stu-id="baea7-161">You create a device by clicking hello **Create** button.</span></span> <span data-ttu-id="baea7-162">Viene visualizzata una finestra di dialogo con un set di chiavi, primaria e secondaria, prepopolato.</span><span class="sxs-lookup"><span data-stu-id="baea7-162">A dialog displays with a set of pre-populated keys (primary and secondary).</span></span> <span data-ttu-id="baea7-163">Immettere un valore in **Device ID** (ID dispositivo) e fare clic su **Create** (Crea).</span><span class="sxs-lookup"><span data-stu-id="baea7-163">Enter a **Device ID** and then click **Create**.</span></span>

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

<span data-ttu-id="baea7-164">Quando viene creato il dispositivo di hello, hello dispositivi elencare gli aggiornamenti con tutti i dispositivi hello registrato, tra cui hello che quello appena creato.</span><span class="sxs-lookup"><span data-stu-id="baea7-164">When hello device is created, hello Devices list updates with all hello registered devices, including hello one you just created.</span></span> <span data-ttu-id="baea7-165">Facendo clic con il pulsante destro del mouse sul nuovo dispositivo, viene visualizzato questo menu:</span><span class="sxs-lookup"><span data-stu-id="baea7-165">If you right-click your new device, you see this menu:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

<span data-ttu-id="baea7-166">Se si sceglie **copiare la stringa di connessione per il dispositivo selezionato**, stringa di connessione del dispositivo hello è Appunti toohello copiato.</span><span class="sxs-lookup"><span data-stu-id="baea7-166">If you choose **Copy connection string for selected device**, hello device connection string is copied toohello clipboard.</span></span> <span data-ttu-id="baea7-167">Mantenere una copia della stringa di connessione dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="baea7-167">Keep a copy of hello device connection string.</span></span> <span data-ttu-id="baea7-168">È necessario durante l'esecuzione di applicazioni di esempio hello descritte in hello le sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="baea7-168">You need it when running hello sample applications described in hello following sections.</span></span>

<span data-ttu-id="baea7-169">Dopo aver completato i passaggi di hello precedenti, si è pronti toostart esegua codice.</span><span class="sxs-lookup"><span data-stu-id="baea7-169">When you've completed hello steps above, you're ready toostart running some code.</span></span> <span data-ttu-id="baea7-170">Entrambi gli esempi di avere una costante nella parte superiore di hello del file di origine principale hello che consente di tooenter una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="baea7-170">Both samples have a constant at hello top of hello main source file that enables you tooenter a connection string.</span></span> <span data-ttu-id="baea7-171">Hello, ad esempio, la riga corrispondente dalla hello **l'hub IOT\_client\_esempio\_mqtt** applicazione viene visualizzata come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="baea7-171">For example, hello corresponding line from hello **iothub\_client\_sample\_mqtt** application appears as follows.</span></span>

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-hello-iothubclient-library"></a><span data-ttu-id="baea7-172">Utilizzo della libreria IoTHubClient hello</span><span class="sxs-lookup"><span data-stu-id="baea7-172">Use hello IoTHubClient library</span></span>

<span data-ttu-id="baea7-173">All'interno di hello **l'hub IOT\_client** cartella hello [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, è presente un **esempi** cartella che contiene un'applicazione denominata **l'hub IOT\_client\_esempio\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="baea7-173">Within hello **iothub\_client** folder in hello [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, there is a **samples** folder that contains an application called **iothub\_client\_sample\_mqtt**.</span></span>

<span data-ttu-id="baea7-174">versione di Windows Hello di hello **l'hub IOT\_client\_esempio\_mqtt** applicazione include hello seguente soluzione di Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="baea7-174">hello Windows version of hello **iothub\_client\_sample\_mqtt** application includes hello following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="baea7-175">Se si apre il progetto in Visual Studio 2017, accettare hello richieste tooretarget hello toohello ultima versione del progetto.</span><span class="sxs-lookup"><span data-stu-id="baea7-175">If you open this project in Visual Studio 2017, accept hello prompts tooretarget hello project toohello latest version.</span></span>

<span data-ttu-id="baea7-176">Questa soluzione contiene un singolo progetto.</span><span class="sxs-lookup"><span data-stu-id="baea7-176">This solution contains a single project.</span></span> <span data-ttu-id="baea7-177">In questa soluzione sono installati quattro pacchetti NuGet:</span><span class="sxs-lookup"><span data-stu-id="baea7-177">There are four NuGet packages installed in this solution:</span></span>

* <span data-ttu-id="baea7-178">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="baea7-178">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="baea7-179">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="baea7-179">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="baea7-180">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="baea7-180">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="baea7-181">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="baea7-181">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="baea7-182">È sempre necessario hello **Microsoft.Azure.C.SharedUtility** pacchetto quando si lavora con hello SDK.</span><span class="sxs-lookup"><span data-stu-id="baea7-182">You always need hello **Microsoft.Azure.C.SharedUtility** package when you are working with hello SDK.</span></span> <span data-ttu-id="baea7-183">In questo esempio Usa il protocollo MQTT hello, pertanto è necessario includere hello **Microsoft.Azure.umqtt** e **Microsoft.Azure.IoTHub.MqttTransport** pacchetti (sono presenti pacchetti equivalenti per AMQP e HTTP ).</span><span class="sxs-lookup"><span data-stu-id="baea7-183">This sample uses hello MQTT protocol, therefore you must include hello **Microsoft.Azure.umqtt** and **Microsoft.Azure.IoTHub.MqttTransport** packages (there are equivalent packages for AMQP and HTTP).</span></span> <span data-ttu-id="baea7-184">Poiché l'esempio hello utilizza hello **IoTHubClient** libreria, è necessario includere anche hello **Microsoft.Azure.IoTHub.IoTHubClient** pacchetto della soluzione.</span><span class="sxs-lookup"><span data-stu-id="baea7-184">Because hello sample uses hello **IoTHubClient** library, you must also include hello **Microsoft.Azure.IoTHub.IoTHubClient** package in your solution.</span></span>

<span data-ttu-id="baea7-185">È possibile trovare l'implementazione di hello per l'applicazione di esempio hello in hello **l'hub IOT\_client\_esempio\_mqtt.c** file di origine.</span><span class="sxs-lookup"><span data-stu-id="baea7-185">You can find hello implementation for hello sample application in hello **iothub\_client\_sample\_mqtt.c** source file.</span></span>

<span data-ttu-id="baea7-186">i passaggi seguenti Hello usano questo toowalk di applicazione di esempio tramite le impostazioni necessarie hello toouse **IoTHubClient** libreria.</span><span class="sxs-lookup"><span data-stu-id="baea7-186">hello following steps use this sample application toowalk you through what's required toouse hello **IoTHubClient** library.</span></span>

### <a name="initialize-hello-library"></a><span data-ttu-id="baea7-187">Inizializzare la libreria hello</span><span class="sxs-lookup"><span data-stu-id="baea7-187">Initialize hello library</span></span>

> [!NOTE]
> <span data-ttu-id="baea7-188">Prima di iniziare con le librerie di hello, potrebbe essere necessario tooperform alcune operazioni di inizializzazione specifiche della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="baea7-188">Before you start working with hello libraries, you may need tooperform some platform-specific initialization.</span></span> <span data-ttu-id="baea7-189">Ad esempio, se si intende toouse AMQP Linux è necessario inizializzare libreria OpenSSL hello.</span><span class="sxs-lookup"><span data-stu-id="baea7-189">For example, if you plan toouse AMQP on Linux you must initialize hello OpenSSL library.</span></span> <span data-ttu-id="baea7-190">Negli esempi di hello Hello [repository GitHub](https://github.com/Azure/azure-iot-sdk-c) chiamare la funzione di utilità hello **piattaforma\_init** quando hello client avvia e chiamare hello **piattaforma\_deinit**  funzione prima della chiusura.</span><span class="sxs-lookup"><span data-stu-id="baea7-190">hello samples in hello [GitHub repository](https://github.com/Azure/azure-iot-sdk-c) call hello utility function **platform\_init** when hello client starts and call hello **platform\_deinit** function before exiting.</span></span> <span data-ttu-id="baea7-191">Queste funzioni vengono dichiarate nel file di intestazione platform.h hello.</span><span class="sxs-lookup"><span data-stu-id="baea7-191">These functions are declared in hello platform.h header file.</span></span> <span data-ttu-id="baea7-192">Esaminare le definizioni di hello di queste funzioni per la piattaforma di destinazione in hello [repository](https://github.com/Azure/azure-iot-sdk-c) toodetermine se è necessario tooinclude qualsiasi codice di inizializzazione specifiche della piattaforma nel client.</span><span class="sxs-lookup"><span data-stu-id="baea7-192">Examine hello definitions of these functions for your target platform in hello [repository](https://github.com/Azure/azure-iot-sdk-c) toodetermine whether you need tooinclude any platform-specific initialization code in your client.</span></span>

<span data-ttu-id="baea7-193">Innanzitutto, toostart utilizzano le librerie di hello, allocare un handle di client di IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="baea7-193">toostart working with hello libraries, first allocate an IoT Hub client handle:</span></span>

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

<span data-ttu-id="baea7-194">Si passa una copia della stringa di connessione hello dispositivo ottenuto da funzione toothis di hello dispositivo explorer dello strumento.</span><span class="sxs-lookup"><span data-stu-id="baea7-194">You pass a copy of hello device connection string you obtained from hello device explorer tool toothis function.</span></span> <span data-ttu-id="baea7-195">È inoltre possibile designare toouse protocollo di comunicazione hello.</span><span class="sxs-lookup"><span data-stu-id="baea7-195">You also designate hello communications protocol toouse.</span></span> <span data-ttu-id="baea7-196">In questo esempio si usa MQTT, ma è possibile usare anche AMQP e HTTP.</span><span class="sxs-lookup"><span data-stu-id="baea7-196">This example uses MQTT, but AMQP and HTTP are also options.</span></span>

<span data-ttu-id="baea7-197">Quando si dispone di un oggetto valido **l'hub IOT\_CLIENT\_gestire**, è possibile iniziare a chiamare toosend API hello e ricevere messaggi tooand dall'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="baea7-197">When you have a valid **IOTHUB\_CLIENT\_HANDLE**, you can start calling hello APIs toosend and receive messages tooand from IoT Hub.</span></span>

### <a name="send-messages"></a><span data-ttu-id="baea7-198">Inviare messaggi</span><span class="sxs-lookup"><span data-stu-id="baea7-198">Send messages</span></span>

<span data-ttu-id="baea7-199">applicazione di esempio Hello imposta un ciclo toosend messaggi tooyour l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="baea7-199">hello sample application sets up a loop toosend messages tooyour IoT hub.</span></span> <span data-ttu-id="baea7-200">Hello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="baea7-200">hello following snippet:</span></span>

- <span data-ttu-id="baea7-201">Crea un messaggio.</span><span class="sxs-lookup"><span data-stu-id="baea7-201">Creates a message.</span></span>
- <span data-ttu-id="baea7-202">Aggiunge un messaggio toohello di proprietà.</span><span class="sxs-lookup"><span data-stu-id="baea7-202">Adds a property toohello message.</span></span>
- <span data-ttu-id="baea7-203">Invia un messaggio.</span><span class="sxs-lookup"><span data-stu-id="baea7-203">Sends a message.</span></span>

<span data-ttu-id="baea7-204">Prima di tutto, creare un messaggio:</span><span class="sxs-lookup"><span data-stu-id="baea7-204">First, create a message:</span></span>

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
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission tooIoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

<span data-ttu-id="baea7-205">Ogni volta che si invia un messaggio, si specifica una funzione di callback tooa di riferimento che viene richiamata quando viene inviati dati hello.</span><span class="sxs-lookup"><span data-stu-id="baea7-205">Every time you send a message, you specify a reference tooa callback function that's invoked when hello data is sent.</span></span> <span data-ttu-id="baea7-206">In questo esempio viene chiamata la funzione di callback hello **SendConfirmationCallback**.</span><span class="sxs-lookup"><span data-stu-id="baea7-206">In this example, hello callback function is called **SendConfirmationCallback**.</span></span> <span data-ttu-id="baea7-207">Hello frammento di codice seguente viene illustrata questa funzione di callback:</span><span class="sxs-lookup"><span data-stu-id="baea7-207">hello following snippet shows this callback function:</span></span>

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

<span data-ttu-id="baea7-208">Si noti hello chiamata toohello **IoTHubMessage\_Destroy** funzione una volta terminato con un messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="baea7-208">Note hello call toohello **IoTHubMessage\_Destroy** function when you're done with hello message.</span></span> <span data-ttu-id="baea7-209">Questa funzione libera le risorse di hello allocate al momento della creazione messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="baea7-209">This function frees hello resources allocated when you created hello message.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="baea7-210">Ricevere messaggi</span><span class="sxs-lookup"><span data-stu-id="baea7-210">Receive messages</span></span>

<span data-ttu-id="baea7-211">La ricezione di un messaggio è un'operazione asincrona.</span><span class="sxs-lookup"><span data-stu-id="baea7-211">Receiving a message is an asynchronous operation.</span></span> <span data-ttu-id="baea7-212">È innanzitutto necessario registrare hello callback tooinvoke quando il dispositivo hello riceve un messaggio:</span><span class="sxs-lookup"><span data-stu-id="baea7-212">First, you register hello callback tooinvoke when hello device receives a message:</span></span>

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

<span data-ttu-id="baea7-213">Hello ultimo parametro è un puntatore void di toowhatever desiderato.</span><span class="sxs-lookup"><span data-stu-id="baea7-213">hello last parameter is a void pointer toowhatever you want.</span></span> <span data-ttu-id="baea7-214">Nell'esempio hello è un numero intero tooan puntatore, ma potrebbe essere un puntatore tooa struttura più complessa di dati.</span><span class="sxs-lookup"><span data-stu-id="baea7-214">In hello sample, it's a pointer tooan integer but it could be a pointer tooa more complex data structure.</span></span> <span data-ttu-id="baea7-215">Questo parametro Abilita toooperate funzione di callback hello in uno stato condiviso con chiamante hello di questa funzione.</span><span class="sxs-lookup"><span data-stu-id="baea7-215">This parameter enables hello callback function toooperate on shared state with hello caller of this function.</span></span>

<span data-ttu-id="baea7-216">Quando il dispositivo hello riceve un messaggio, hello funzione di callback registrato viene richiamato.</span><span class="sxs-lookup"><span data-stu-id="baea7-216">When hello device receives a message, hello registered callback function is invoked.</span></span> <span data-ttu-id="baea7-217">Questa funzione di callback recupera:</span><span class="sxs-lookup"><span data-stu-id="baea7-217">This callback function retrieves:</span></span>

* <span data-ttu-id="baea7-218">id di messaggio Hello e id di correlazione dal messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="baea7-218">hello message id and correlation id from hello message.</span></span>
* <span data-ttu-id="baea7-219">contenuto del messaggio Hello.</span><span class="sxs-lookup"><span data-stu-id="baea7-219">hello message content.</span></span>
* <span data-ttu-id="baea7-220">Tutte le proprietà personalizzate dal messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="baea7-220">Any custom properties from hello message.</span></span>

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
        (void)printf("unable tooretrieve hello message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive hello work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from hello message
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

<span data-ttu-id="baea7-221">Hello utilizzare **IoTHubMessage\_GetByteArray** messaggio hello tooretrieve di funzione, che in questo esempio è una stringa.</span><span class="sxs-lookup"><span data-stu-id="baea7-221">Use hello **IoTHubMessage\_GetByteArray** function tooretrieve hello message, which in this example is a string.</span></span>

### <a name="uninitialize-hello-library"></a><span data-ttu-id="baea7-222">Annullare l'inizializzazione della libreria hello</span><span class="sxs-lookup"><span data-stu-id="baea7-222">Uninitialize hello library</span></span>

<span data-ttu-id="baea7-223">Quando è terminato l'invio di eventi e la ricezione dei messaggi, è possibile annullare l'inizializzazione della libreria IoT hello.</span><span class="sxs-lookup"><span data-stu-id="baea7-223">When you're done sending events and receiving messages, you can uninitialize hello IoT library.</span></span> <span data-ttu-id="baea7-224">toodo in tal caso, eseguire hello in seguito a chiamata di funzione:</span><span class="sxs-lookup"><span data-stu-id="baea7-224">toodo so, issue hello following function call:</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="baea7-225">Questa chiamata consente di liberare risorse hello precedentemente allocate dal hello **IoTHubClient\_CreateFromConnectionString** (funzione).</span><span class="sxs-lookup"><span data-stu-id="baea7-225">This call frees up hello resources previously allocated by hello **IoTHubClient\_CreateFromConnectionString** function.</span></span>

<span data-ttu-id="baea7-226">Come si può notare, è facile toosend e ricevere messaggi con hello **IoTHubClient** libreria.</span><span class="sxs-lookup"><span data-stu-id="baea7-226">As you can see, it's easy toosend and receive messages with hello **IoTHubClient** library.</span></span> <span data-ttu-id="baea7-227">libreria Hello gestisce i dettagli di hello di comunicare con l'IoT Hub, tra cui toouse protocollo (dal punto di vista hello dello sviluppatore di hello, si tratta di un'opzione di configurazione minima).</span><span class="sxs-lookup"><span data-stu-id="baea7-227">hello library handles hello details of communicating with IoT Hub, including which protocol toouse (from hello perspective of hello developer, this is a simple configuration option).</span></span>

<span data-ttu-id="baea7-228">Hello **IoTHubClient** libreria fornisce anche un controllo preciso come dati hello tooserialize il dispositivo invia tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="baea7-228">hello **IoTHubClient** library also provides precise control over how tooserialize hello data your device sends tooIoT Hub.</span></span> <span data-ttu-id="baea7-229">In alcuni casi, questo livello di controllo è un vantaggio, ma in altri è un dettaglio di implementazione che non si desidera toobe riguarda.</span><span class="sxs-lookup"><span data-stu-id="baea7-229">In some cases this level of control is an advantage, but in others it is an implementation detail that you don't want toobe concerned with.</span></span> <span data-ttu-id="baea7-230">Se è questo caso di hello, è possibile utilizzare hello **serializzatore** libreria, descritto nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="baea7-230">If that's hello case, you might consider using hello **serializer** library, which is described in hello next section.</span></span>

## <a name="use-hello-serializer-library"></a><span data-ttu-id="baea7-231">Utilizzo della libreria serializzatore hello</span><span class="sxs-lookup"><span data-stu-id="baea7-231">Use hello serializer library</span></span>

<span data-ttu-id="baea7-232">Concettualmente hello **serializzatore** libreria si trova nella parte superiore di hello **IoTHubClient** libreria in hello SDK.</span><span class="sxs-lookup"><span data-stu-id="baea7-232">Conceptually hello **serializer** library sits on top of hello **IoTHubClient** library in hello SDK.</span></span> <span data-ttu-id="baea7-233">Usa hello **IoTHubClient** libreria per hello sottostante la comunicazione con l'IoT Hub, ma aggiunge funzionalità di modellazione per la rimozione di carico hello per gestire la serializzazione dei messaggi da Developer Edition hello.</span><span class="sxs-lookup"><span data-stu-id="baea7-233">It uses hello **IoTHubClient** library for hello underlying communication with IoT Hub, but it adds modeling capabilities that remove hello burden of dealing with message serialization from hello developer.</span></span> <span data-ttu-id="baea7-234">Il funzionamento di questa libreria può essere illustrato meglio con un esempio.</span><span class="sxs-lookup"><span data-stu-id="baea7-234">How this library works is best demonstrated by an example.</span></span>

<span data-ttu-id="baea7-235">Inside hello **serializzatore** cartella hello [repository di azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c), è un **esempi** cartella che contiene un'applicazione denominata **simplesample \_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="baea7-235">Inside hello **serializer** folder in hello [azure-iot-sdk-c repository](https://github.com/Azure/azure-iot-sdk-c), is a **samples** folder that contains an application called **simplesample\_mqtt**.</span></span> <span data-ttu-id="baea7-236">versione di Windows Hello di questo esempio include hello seguente soluzione di Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="baea7-236">hello Windows version of this sample includes hello following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="baea7-237">Se si apre il progetto in Visual Studio 2017, accettare hello richieste tooretarget hello toohello ultima versione del progetto.</span><span class="sxs-lookup"><span data-stu-id="baea7-237">If you open this project in Visual Studio 2017, accept hello prompts tooretarget hello project toohello latest version.</span></span>

<span data-ttu-id="baea7-238">Come esempio hello precedente, questo include diversi pacchetti NuGet:</span><span class="sxs-lookup"><span data-stu-id="baea7-238">As with hello previous sample, this one includes several NuGet packages:</span></span>

* <span data-ttu-id="baea7-239">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="baea7-239">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="baea7-240">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="baea7-240">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="baea7-241">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="baea7-241">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="baea7-242">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="baea7-242">Microsoft.Azure.IoTHub.Serializer</span></span>
* <span data-ttu-id="baea7-243">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="baea7-243">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="baea7-244">Si è visto la maggior parte dei pacchetti nell'esempio precedente hello, ma **Microsoft.Azure.IoTHub.Serializer** è nuovo.</span><span class="sxs-lookup"><span data-stu-id="baea7-244">You've seen most of these packages in hello previous sample, but **Microsoft.Azure.IoTHub.Serializer** is new.</span></span> <span data-ttu-id="baea7-245">Questo pacchetto è necessario quando si utilizza hello **serializzatore** libreria.</span><span class="sxs-lookup"><span data-stu-id="baea7-245">This package is required when you use hello **serializer** library.</span></span>

<span data-ttu-id="baea7-246">È possibile trovare l'implementazione di hello dell'applicazione di esempio hello in hello **simplesample\_mqtt.c** file.</span><span class="sxs-lookup"><span data-stu-id="baea7-246">You can find hello implementation of hello sample application in hello **simplesample\_mqtt.c** file.</span></span>

<span data-ttu-id="baea7-247">Hello nelle sezioni seguenti vengono illustrati le parti principali di questo esempio hello.</span><span class="sxs-lookup"><span data-stu-id="baea7-247">hello following sections walk you through hello key parts of this sample.</span></span>

### <a name="initialize-hello-library"></a><span data-ttu-id="baea7-248">Inizializzare la libreria hello</span><span class="sxs-lookup"><span data-stu-id="baea7-248">Initialize hello library</span></span>

<span data-ttu-id="baea7-249">utilizzo di hello toostart **serializzatore** libreria, l'inizializzazione di hello chiamata API:</span><span class="sxs-lookup"><span data-stu-id="baea7-249">toostart working with hello **serializer** library, call hello initialization APIs:</span></span>

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

<span data-ttu-id="baea7-250">Hello chiamata toohello **serializzatore\_init** funzione è una singola chiamata e inizializza hello raccolta sottostante.</span><span class="sxs-lookup"><span data-stu-id="baea7-250">hello call toohello **serializer\_init** function is a one-time call and initializes hello underlying library.</span></span> <span data-ttu-id="baea7-251">Chiamare quindi hello **IoTHubClient\_LL\_CreateFromConnectionString** funzione, che è hello stessa API come hello **IoTHubClient** esempio.</span><span class="sxs-lookup"><span data-stu-id="baea7-251">Then, you call hello **IoTHubClient\_LL\_CreateFromConnectionString** function, which is hello same API as in hello **IoTHubClient** sample.</span></span> <span data-ttu-id="baea7-252">Questa chiamata imposta la stringa di connessione del dispositivo (questa chiamata è anche in cui si sceglie di protocollo hello desiderato toouse).</span><span class="sxs-lookup"><span data-stu-id="baea7-252">This call sets your device connection string (this call is also where you choose hello protocol you want toouse).</span></span> <span data-ttu-id="baea7-253">In questo esempio utilizza MQTT trasporto hello, ma è possibile usare AMQP o HTTP.</span><span class="sxs-lookup"><span data-stu-id="baea7-253">This sample uses MQTT as hello transport, but could use AMQP or HTTP.</span></span>

<span data-ttu-id="baea7-254">Chiamare infine hello **crea\_modello\_istanza** (funzione).</span><span class="sxs-lookup"><span data-stu-id="baea7-254">Finally, call hello **CREATE\_MODEL\_INSTANCE** function.</span></span> <span data-ttu-id="baea7-255">**WeatherStation** hello uno spazio dei nomi del modello di hello e **ContosoAnemometer** hello nome del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="baea7-255">**WeatherStation** is hello namespace of hello model and **ContosoAnemometer** is hello name of hello model.</span></span> <span data-ttu-id="baea7-256">Una volta creata l'istanza del modello hello, è possibile utilizzare toostart inviando e ricevendo messaggi.</span><span class="sxs-lookup"><span data-stu-id="baea7-256">Once hello model instance is created, you can use it toostart sending and receiving messages.</span></span> <span data-ttu-id="baea7-257">Tuttavia, è importante toounderstand è il tipo di modello.</span><span class="sxs-lookup"><span data-stu-id="baea7-257">However, it's important toounderstand what a model is.</span></span>

### <a name="define-hello-model"></a><span data-ttu-id="baea7-258">Definire il modello di hello</span><span class="sxs-lookup"><span data-stu-id="baea7-258">Define hello model</span></span>

<span data-ttu-id="baea7-259">Un modello in hello **serializzatore** libreria definisce messaggi hello che il dispositivo può inviare tooIoT Hub e hello i messaggi, chiamato *azioni* in hello modeling language, che può ricevere.</span><span class="sxs-lookup"><span data-stu-id="baea7-259">A model in hello **serializer** library defines hello messages that your device can send tooIoT Hub and hello messages, called *actions* in hello modeling language, which it can receive.</span></span> <span data-ttu-id="baea7-260">Si definisce un modello usando un set di macro di C come hello **simplesample\_mqtt** applicazione di esempio:</span><span class="sxs-lookup"><span data-stu-id="baea7-260">You define a model using a set of C macros as in hello **simplesample\_mqtt** sample application:</span></span>

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

<span data-ttu-id="baea7-261">Hello **iniziare\_dello spazio dei nomi** e **fine\_dello spazio dei nomi** entrambi eseguire hello dello spazio dei nomi del modello di hello come argomento.</span><span class="sxs-lookup"><span data-stu-id="baea7-261">hello **BEGIN\_NAMESPACE** and **END\_NAMESPACE** macros both take hello namespace of hello model as an argument.</span></span> <span data-ttu-id="baea7-262">È previsto che svolgono queste macro è definizione hello del modello o i modelli e strutture dei dati che utilizzano modelli hello hello.</span><span class="sxs-lookup"><span data-stu-id="baea7-262">It's expected that anything between these macros is hello definition of your model or models, and hello data structures that hello models use.</span></span>

<span data-ttu-id="baea7-263">In questo esempio è presente un singolo modello chiamato **ContosoAnemometer**.</span><span class="sxs-lookup"><span data-stu-id="baea7-263">In this example, there is a single model called **ContosoAnemometer**.</span></span> <span data-ttu-id="baea7-264">Questo modello definisce due tipi di dati che il dispositivo può inviare tooIoT Hub: **DeviceId** e **WindSpeed**.</span><span class="sxs-lookup"><span data-stu-id="baea7-264">This model defines two pieces of data that your device can send tooIoT Hub: **DeviceId** and **WindSpeed**.</span></span> <span data-ttu-id="baea7-265">Definisce anche tre azioni (messaggi) che il dispositivo può ricevere, cioè **TurnFanOn**, **TurnFanOff** e **SetAirResistance**.</span><span class="sxs-lookup"><span data-stu-id="baea7-265">It also defines three actions (messages) that your device can receive: **TurnFanOn**, **TurnFanOff**, and **SetAirResistance**.</span></span> <span data-ttu-id="baea7-266">Ogni elemento dati ha un tipo e ogni azione un nome e facoltativamente un set di parametri.</span><span class="sxs-lookup"><span data-stu-id="baea7-266">Each data element has a type, and each action has a name (and optionally a set of parameters).</span></span>

<span data-ttu-id="baea7-267">dati Hello e azioni definite nel modello hello definiscono una superficie API che è possibile utilizzare toosend messaggi tooIoT Hub e rispondere dispositivo toohello toomessages inviato.</span><span class="sxs-lookup"><span data-stu-id="baea7-267">hello data and actions defined in hello model define an API surface that you can use toosend messages tooIoT Hub, and respond toomessages sent toohello device.</span></span> <span data-ttu-id="baea7-268">L'uso di questo modello può essere illustrato meglio con un esempio.</span><span class="sxs-lookup"><span data-stu-id="baea7-268">Use of this model is best understood through an example.</span></span>

### <a name="send-messages"></a><span data-ttu-id="baea7-269">Inviare messaggi</span><span class="sxs-lookup"><span data-stu-id="baea7-269">Send messages</span></span>

<span data-ttu-id="baea7-270">modello Hello definisce i dati di hello è possibile inviare tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="baea7-270">hello model defines hello data you can send tooIoT Hub.</span></span> <span data-ttu-id="baea7-271">In questo esempio, che indica una delle hello due elementi di dati definiti tramite hello **WITH_DATA** (macro).</span><span class="sxs-lookup"><span data-stu-id="baea7-271">In this example, that means one of hello two data items defined using hello **WITH_DATA** macro.</span></span> <span data-ttu-id="baea7-272">Esistono diversi toosend necessarie di passaggi **DeviceId** e **WindSpeed** hub IoT tooan di valori.</span><span class="sxs-lookup"><span data-stu-id="baea7-272">There are several steps required toosend **DeviceId** and **WindSpeed** values tooan IoT hub.</span></span> <span data-ttu-id="baea7-273">i dati di hello tooset da toosend per primo è Hello:</span><span class="sxs-lookup"><span data-stu-id="baea7-273">hello first is tooset hello data you want toosend:</span></span>

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

<span data-ttu-id="baea7-274">Hello modello definita in precedenza consente valori hello tooset impostando i membri di un **struct**.</span><span class="sxs-lookup"><span data-stu-id="baea7-274">hello model you defined earlier enables you tooset hello values by setting members of a **struct**.</span></span> <span data-ttu-id="baea7-275">Quindi serializzare il messaggio hello da toosend:</span><span class="sxs-lookup"><span data-stu-id="baea7-275">Next, serialize hello message you want toosend:</span></span>

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed tooserialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

<span data-ttu-id="baea7-276">Questo codice serializza i buffer di dispositivo a cloud tooa hello (a cui fa riferimento **destinazione**).</span><span class="sxs-lookup"><span data-stu-id="baea7-276">This code serializes hello device-to-cloud tooa buffer (referenced by **destination**).</span></span> <span data-ttu-id="baea7-277">codice Hello richiama quindi hello **sendMessage** funzione toosend hello messaggio tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="baea7-277">hello code then invokes hello **sendMessage** function toosend hello message tooIoT Hub:</span></span>

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable toocreate a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted hello message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


<span data-ttu-id="baea7-278">secondo parametro toolast di Hello **IoTHubClient\_LL\_SendEventAsync** è una funzione di callback tooa di riferimento che viene chiamata quando viene ricevuti correttamente i dati hello.</span><span class="sxs-lookup"><span data-stu-id="baea7-278">hello second toolast parameter of **IoTHubClient\_LL\_SendEventAsync** is a reference tooa callback function that's called when hello data is successfully sent.</span></span> <span data-ttu-id="baea7-279">Di seguito è la funzione di callback hello nell'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="baea7-279">Here's hello callback function in hello sample:</span></span>

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

<span data-ttu-id="baea7-280">Hello secondo parametro è un contesto di toouser puntatore. lo stesso puntatore passato troppo Hello**IoTHubClient\_LL\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="baea7-280">hello second parameter is a pointer toouser context; hello same pointer passed too**IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="baea7-281">In questo caso, il contesto di hello è un contatore semplice, ma è possibile assegnare qualsiasi.</span><span class="sxs-lookup"><span data-stu-id="baea7-281">In this case, hello context is a simple counter, but it can be anything you want.</span></span>

<span data-ttu-id="baea7-282">Questo è tutto è toosending i messaggi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="baea7-282">That's all there is toosending device-to-cloud messages.</span></span> <span data-ttu-id="baea7-283">Hello solo cosa toocover a sinistra è come tooreceive messaggi.</span><span class="sxs-lookup"><span data-stu-id="baea7-283">hello only thing left toocover is how tooreceive messages.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="baea7-284">Ricevere messaggi</span><span class="sxs-lookup"><span data-stu-id="baea7-284">Receive messages</span></span>

<span data-ttu-id="baea7-285">Ricezione di un messaggio in modo simile toohello funzionamento messaggi in hello **IoTHubClient** libreria.</span><span class="sxs-lookup"><span data-stu-id="baea7-285">Receiving a message works similarly toohello way messages work in hello **IoTHubClient** library.</span></span> <span data-ttu-id="baea7-286">Prima di tutto occorre registrare la funzione di callback di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="baea7-286">First, you register a message callback function:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable tooIoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

<span data-ttu-id="baea7-287">È quindi necessario scrivere hello di callback che viene richiamato quando viene ricevuto un messaggio:</span><span class="sxs-lookup"><span data-stu-id="baea7-287">Then, you write hello callback function that's invoked when a message is received:</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
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

<span data-ttu-id="baea7-288">Questo codice boilerplate--è hello uguali per una soluzione.</span><span class="sxs-lookup"><span data-stu-id="baea7-288">This code is boilerplate -- it's hello same for any solution.</span></span> <span data-ttu-id="baea7-289">Questa funzione riceve messaggi hello e si occupa di routing toohello funzione appropriata tramite chiamata hello troppo**EXECUTE\_comando**.</span><span class="sxs-lookup"><span data-stu-id="baea7-289">This function receives hello message and takes care of routing it toohello appropriate function through hello call too**EXECUTE\_COMMAND**.</span></span> <span data-ttu-id="baea7-290">funzione Hello chiamata a questo punto dipende dalla definizione di hello di azioni di hello nel modello.</span><span class="sxs-lookup"><span data-stu-id="baea7-290">hello function called at this point depends on hello definition of hello actions in your model.</span></span>

<span data-ttu-id="baea7-291">Quando si definisce un'azione nel modello, è necessario tooimplement una funzione che viene chiamata quando il dispositivo riceve il messaggio hello corrispondente.</span><span class="sxs-lookup"><span data-stu-id="baea7-291">When you define an action in your model, you're required tooimplement a function that's called when your device receives hello corresponding message.</span></span> <span data-ttu-id="baea7-292">Ad esempio, se il modello definisce questa azione:</span><span class="sxs-lookup"><span data-stu-id="baea7-292">For example, if your model defines this action:</span></span>

```c
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="baea7-293">Definire una funzione con questa firma:</span><span class="sxs-lookup"><span data-stu-id="baea7-293">Define a function with this signature:</span></span>

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="baea7-294">Si noti come hello nome della funzione hello hello di corrisponde azione hello nel modello hello e che hello della funzione hello corrispondano hello parametri specificati per l'azione di hello.</span><span class="sxs-lookup"><span data-stu-id="baea7-294">Note how hello name of hello function matches hello name of hello action in hello model and that hello parameters of hello function match hello parameters specified for hello action.</span></span> <span data-ttu-id="baea7-295">primo parametro Hello è sempre necessario e contiene un'istanza di toohello indicatore di misura del modello.</span><span class="sxs-lookup"><span data-stu-id="baea7-295">hello first parameter is always required and contains a pointer toohello instance of your model.</span></span>

<span data-ttu-id="baea7-296">Quando il dispositivo di hello riceve un messaggio che corrisponde alla firma, la funzione corrispondente hello viene chiamata.</span><span class="sxs-lookup"><span data-stu-id="baea7-296">When hello device receives a message that matches this signature, hello corresponding function is called.</span></span> <span data-ttu-id="baea7-297">Pertanto, a parte con il codice di boilerplate hello tooinclude da **IoTHubMessage**, la ricezione di messaggi è sufficiente definire una funzione semplice per ogni azione definita nel modello.</span><span class="sxs-lookup"><span data-stu-id="baea7-297">Therefore, aside from having tooinclude hello boilerplate code from **IoTHubMessage**, receiving messages is just a matter of defining a simple function for each action defined in your model.</span></span>

### <a name="uninitialize-hello-library"></a><span data-ttu-id="baea7-298">Annullare l'inizializzazione della libreria hello</span><span class="sxs-lookup"><span data-stu-id="baea7-298">Uninitialize hello library</span></span>

<span data-ttu-id="baea7-299">Quando è terminato l'invio dei dati e la ricezione dei messaggi, è possibile annullare l'inizializzazione della libreria IoT hello:</span><span class="sxs-lookup"><span data-stu-id="baea7-299">When you're done sending data and receiving messages, you can uninitialize hello IoT library:</span></span>

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

<span data-ttu-id="baea7-300">Ognuna di queste tre funzioni in linea con hello tre funzioni inizializzazione descritte in precedenza.</span><span class="sxs-lookup"><span data-stu-id="baea7-300">Each of these three functions aligns with hello three initialization functions described previously.</span></span> <span data-ttu-id="baea7-301">Chiamando questi API si assicura che siano liberate le risorse allocate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="baea7-301">Calling these APIs ensures that you free previously allocated resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="baea7-302">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="baea7-302">Next Steps</span></span>

<span data-ttu-id="baea7-303">In questo articolo coperto nozioni fondamentali di hello dell'uso delle librerie di hello in hello **dispositivo IoT di Azure SDK per C**. È stata fornita toounderstand sufficienti informazioni cosa è incluso in hello SDK, architettura e come tooget ha iniziato a lavorare con hello gli esempi di Windows.</span><span class="sxs-lookup"><span data-stu-id="baea7-303">This article covered hello basics of using hello libraries in hello **Azure IoT device SDK for C**. It provided you with enough information toounderstand what's included in hello SDK, its architecture, and how tooget started working with hello Windows samples.</span></span> <span data-ttu-id="baea7-304">articolo successivo Hello continua descrizione hello di hello SDK per spiegare in che [ulteriori informazioni sulla raccolta IoTHubClient hello](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="baea7-304">hello next article continues hello description of hello SDK by explaining [more about hello IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span></span>

<span data-ttu-id="baea7-305">toolearn più sullo sviluppo per l'IoT Hub, vedere hello [Azure IoT SDK][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="baea7-305">toolearn more about developing for IoT Hub, see hello [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="baea7-306">toofurther esplorare le funzionalità di hello di IoT Hub, vedere:</span><span class="sxs-lookup"><span data-stu-id="baea7-306">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="baea7-307">[Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="baea7-307">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
