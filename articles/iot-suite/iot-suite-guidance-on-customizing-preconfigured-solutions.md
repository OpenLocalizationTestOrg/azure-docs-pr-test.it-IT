---
title: aaaCustomizing preconfigurato soluzioni | Documenti Microsoft
description: Vengono fornite indicazioni su come toocustomize hello Azure IoT Suite preconfigurato soluzioni.
services: 
suite: iot-suite
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4653ae53-4110-4a10-bd6c-7dc034c293a8
ms.service: iot-suite
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 1a8573f5ac6ed944c44459df495446f15174d513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-a-preconfigured-solution"></a><span data-ttu-id="a4dcf-103">Personalizzare una soluzione preconfigurata</span><span class="sxs-lookup"><span data-stu-id="a4dcf-103">Customize a preconfigured solution</span></span>

<span data-ttu-id="a4dcf-104">soluzioni Hello preconfigurato fornite con hello Azure IoT Suite dimostrano dei servizi di hello all'interno di hello suite lavoro insieme toodeliver una soluzione end-to-end.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-104">hello preconfigured solutions provided with hello Azure IoT Suite demonstrate hello services within hello suite working together toodeliver an end-to-end solution.</span></span> <span data-ttu-id="a4dcf-105">A questo punto di partenza, sono disponibili vari punti in cui è possibile estendere e personalizzare soluzioni hello per scenari specifici.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-105">From this starting point, there are various places in which you can extend and customize hello solution for specific scenarios.</span></span> <span data-ttu-id="a4dcf-106">Hello le sezioni seguenti vengono descritti questi punti di personalizzazione comuni.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-106">hello following sections describe these common customization points.</span></span>

## <a name="find-hello-source-code"></a><span data-ttu-id="a4dcf-107">Trovare il codice sorgente hello</span><span class="sxs-lookup"><span data-stu-id="a4dcf-107">Find hello source code</span></span>

<span data-ttu-id="a4dcf-108">il codice sorgente Hello per le soluzioni hello preconfigurato è disponibile in hello seguenti repository in GitHub:</span><span class="sxs-lookup"><span data-stu-id="a4dcf-108">hello source code for hello preconfigured solutions is available on GitHub in hello following repositories:</span></span>

* <span data-ttu-id="a4dcf-109">Monitoraggio remoto: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span><span class="sxs-lookup"><span data-stu-id="a4dcf-109">Remote Monitoring: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span></span>
* <span data-ttu-id="a4dcf-110">Manutenzione predittiva: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span><span class="sxs-lookup"><span data-stu-id="a4dcf-110">Predictive Maintenance: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span></span>
* <span data-ttu-id="a4dcf-111">Factory connesso: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span><span class="sxs-lookup"><span data-stu-id="a4dcf-111">Connected factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span></span>

<span data-ttu-id="a4dcf-112">il codice sorgente Hello per le soluzioni hello preconfigurato è fornite procedure consigliate e i pattern di hello toodemonstrate utilizzata la funzionalità di tooimplement hello end-to-end di una soluzione IoT utilizzando Azure IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-112">hello source code for hello preconfigured solutions is provided toodemonstrate hello patterns and practices used tooimplement hello end-to-end functionality of an IoT solution using Azure IoT Suite.</span></span> <span data-ttu-id="a4dcf-113">È possibile trovare altre informazioni su come toobuild e distribuire soluzioni hello nei repository GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-113">You can find more information about how toobuild and deploy hello solutions in hello GitHub repositories.</span></span>

## <a name="change-hello-preconfigured-rules"></a><span data-ttu-id="a4dcf-114">Modificare le regole di hello preconfigurato</span><span class="sxs-lookup"><span data-stu-id="a4dcf-114">Change hello preconfigured rules</span></span>

<span data-ttu-id="a4dcf-115">Hello soluzione di monitoraggio remoto include tre [Azure flusso Analitica](https://azure.microsoft.com/services/stream-analytics/) processi toohandle informazioni del dispositivo, la telemetria e logica delle regole nella soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-115">hello remote monitoring solution includes three [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jobs toohandle device information, telemetry, and rules logic in hello solution.</span></span>

<span data-ttu-id="a4dcf-116">Hello tre flusso processi analitica e la loro sintassi sono descritti in dettaglio in hello [monitoraggio remoto preconfigurato procedura dettagliata sulla soluzione](iot-suite-remote-monitoring-sample-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="a4dcf-116">hello three stream analytics jobs and their syntax are described in depth in hello [Remote monitoring preconfigured solution walkthrough](iot-suite-remote-monitoring-sample-walkthrough.md).</span></span> 

<span data-ttu-id="a4dcf-117">È possibile modificare questi processi direttamente tooalter hello logica, o aggiungere logica tooyour specifico scenario.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-117">You can edit these jobs directly tooalter hello logic, or add logic specific tooyour scenario.</span></span> <span data-ttu-id="a4dcf-118">È possibile trovare hello Analitica flusso processi come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="a4dcf-118">You can find hello Stream Analytics jobs as follows:</span></span>

1. <span data-ttu-id="a4dcf-119">Andare troppo[portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a4dcf-119">Go too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a4dcf-120">Passare il gruppo di risorse toohello con stesso nome come soluzione IoT hello.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-120">Navigate toohello resource group with hello same name as your IoT solution.</span></span> 
3. <span data-ttu-id="a4dcf-121">Selezionare il processo di Azure flusso Analitica hello toomodify desiderato.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-121">Select hello Azure Stream Analytics job you'd like toomodify.</span></span> 
4. <span data-ttu-id="a4dcf-122">Processo di arresto hello selezionando **arrestare** nel set di hello di comandi.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-122">Stop hello job by selecting **Stop** in hello set of commands.</span></span> 
5. <span data-ttu-id="a4dcf-123">Modificare gli output, query e gli input hello.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-123">Edit hello inputs, query, and outputs.</span></span>
   
    <span data-ttu-id="a4dcf-124">Una semplice modifica è query hello toochange per hello **regole** toouse processo un **"<"** anziché un **">"**.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-124">A simple modification is toochange hello query for hello **Rules** job toouse a **"<"** instead of a **">"**.</span></span> <span data-ttu-id="a4dcf-125">portale di soluzione Hello viene comunque mostrata **">"** quando si modifica una regola, ma si noti come comportamento hello viene capovolta a causa di modifica toohello hello processo sottostante.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-125">hello solution portal still shows **">"** when you edit a rule, but notice how hello behavior is flipped due toohello change in hello underlying job.</span></span>
6. <span data-ttu-id="a4dcf-126">Avviare il processo di hello</span><span class="sxs-lookup"><span data-stu-id="a4dcf-126">Start hello job</span></span>

> [!NOTE]
> <span data-ttu-id="a4dcf-127">dashboard di monitoraggio remoto Hello dipende dai dati specifici, pertanto modifica processi hello può causare toofail dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-127">hello remote monitoring dashboard depends on specific data, so altering hello jobs can cause hello dashboard toofail.</span></span>

## <a name="add-your-own-rules"></a><span data-ttu-id="a4dcf-128">Aggiungere le regole personalizzate</span><span class="sxs-lookup"><span data-stu-id="a4dcf-128">Add your own rules</span></span>

<span data-ttu-id="a4dcf-129">Inoltre toochanging hello preconfigurato processi Analitica di flusso di Azure, è possibile utilizzare i nuovi processi hello tooadd portale Azure o aggiungere nuovi processi tooexisting di query.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-129">In addition toochanging hello preconfigured Azure Stream Analytics jobs, you can use hello Azure portal tooadd new jobs or add new queries tooexisting jobs.</span></span>

## <a name="customize-devices"></a><span data-ttu-id="a4dcf-130">Personalizzare i dispositivi</span><span class="sxs-lookup"><span data-stu-id="a4dcf-130">Customize devices</span></span>

<span data-ttu-id="a4dcf-131">Uno dei più comuni attività di estensione hello funziona con scenari con dispositivi tooyour specifico.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-131">One of hello most common extension activities is working with devices specific tooyour scenario.</span></span> <span data-ttu-id="a4dcf-132">Esistono diversi metodi per usare i dispositivi,</span><span class="sxs-lookup"><span data-stu-id="a4dcf-132">There are several methods for working with devices.</span></span> <span data-ttu-id="a4dcf-133">Questi metodi includono la modifica di un toomatch dispositivo simulato lo scenario o utilizzando hello [SDK dispositivo IoT] [ IoT Device SDK] tooconnect soluzione toohello dispositivo fisico.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-133">These methods include altering a simulated device toomatch your scenario, or using hello [IoT Device SDK][IoT Device SDK] tooconnect your physical device toohello solution.</span></span>

<span data-ttu-id="a4dcf-134">Per i dispositivi tooadding una Guida dettagliata, vedere hello [i dispositivi Iot Suite connessione](iot-suite-connecting-devices.md) articolo e hello [monitoraggio esempio SDK C remota](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span><span class="sxs-lookup"><span data-stu-id="a4dcf-134">For a step-by-step guide tooadding devices, see hello [Iot Suite Connecting Devices](iot-suite-connecting-devices.md) article and hello [remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span></span> <span data-ttu-id="a4dcf-135">Questo esempio è progettato toowork con hello soluzione preconfigurata di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-135">This sample is designed toowork with hello remote monitoring preconfigured solution.</span></span>

### <a name="create-your-own-simulated-device"></a><span data-ttu-id="a4dcf-136">Creare il dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="a4dcf-136">Create your own simulated device</span></span>

<span data-ttu-id="a4dcf-137">Incluso in hello [il codice sorgente della soluzione di monitoraggio remoto](https://github.com/Azure/azure-iot-remote-monitoring), è un simulatore di .NET.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-137">Included in hello [remote monitoring solution source code](https://github.com/Azure/azure-iot-remote-monitoring), is a .NET simulator.</span></span> <span data-ttu-id="a4dcf-138">Il simulatore è hello uno stato effettuato il provisioning come parte della soluzione hello ed è possibile modificarla toosend metadati diversi, dati di telemetria e rispondere metodi e i comandi toodifferent.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-138">This simulator is hello one provisioned as part of hello solution and you can alter it toosend different metadata, telemetry, and respond toodifferent commands and methods.</span></span>

<span data-ttu-id="a4dcf-139">simulatore preconfigurata di Hello nella soluzione preconfigurata di monitoraggio remoto hello simula un dispositivo di raffreddamento dispositivo che genera i dati di telemetria temperatura e umidità.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-139">hello preconfigured simulator in hello remote monitoring preconfigured solution simulates a cooler device that emits temperature and humidity telemetry.</span></span> <span data-ttu-id="a4dcf-140">È possibile modificare il simulatore hello in hello [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) quando è stata duplicata repository GitHub hello del progetto.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-140">You can modify hello simulator in hello [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) project when you've forked hello GitHub repository.</span></span>

### <a name="available-locations-for-simulated-devices"></a><span data-ttu-id="a4dcf-141">Posizioni disponibili per i dispositivi simulati</span><span class="sxs-lookup"><span data-stu-id="a4dcf-141">Available locations for simulated devices</span></span>

<span data-ttu-id="a4dcf-142">set di percorsi predefinito Hello è in Seattle/Redmond, Washington, Stati Uniti d'America.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-142">hello default set of locations is in Seattle/Redmond, Washington, United States of America.</span></span> <span data-ttu-id="a4dcf-143">È possibile modificare queste località nel file [SampleDeviceFactory.cs][lnk-sample-device-factory].</span><span class="sxs-lookup"><span data-stu-id="a4dcf-143">You can change these locations in [SampleDeviceFactory.cs][lnk-sample-device-factory].</span></span>

### <a name="add-a-desired-property-update-handler-toohello-simulator"></a><span data-ttu-id="a4dcf-144">Aggiungere un simulatore di toohello gestore aggiornamento proprietà desiderata</span><span class="sxs-lookup"><span data-stu-id="a4dcf-144">Add a desired property update handler toohello simulator</span></span>

<span data-ttu-id="a4dcf-145">È possibile impostare un valore per una proprietà desiderata per un dispositivo nel portale di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-145">You can set a value for a desired property for a device in hello solution portal.</span></span> <span data-ttu-id="a4dcf-146">È responsabilità di hello della richiesta di modifica proprietà hello dispositivo toohandle hello quando dispositivo hello recupera il valore di proprietà hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-146">It is hello responsibility of hello device toohandle hello property change request when hello device retrieves hello desired property value.</span></span> <span data-ttu-id="a4dcf-147">supporto tooadd per la modifica di un valore di proprietà tramite una proprietà desiderata, è necessario un simulatore toohello gestore tooadd.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-147">tooadd support for a property value change through a desired property, you need tooadd a handler toohello simulator.</span></span>

<span data-ttu-id="a4dcf-148">simulatore Hello contiene gestori per hello **SetPointTemp** e **TelemetryInterval** le proprietà che è possibile aggiornare impostando desiderati valori nel portale di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-148">hello simulator contains handlers for hello **SetPointTemp** and **TelemetryInterval** properties that you can update by setting desired values in hello solution portal.</span></span>

<span data-ttu-id="a4dcf-149">Hello esempio seguente viene illustrato il gestore di hello per hello **SetPointTemp** proprietà in hello desiderata **CoolerDevice** classe:</span><span class="sxs-lookup"><span data-stu-id="a4dcf-149">hello following example shows hello handler for hello **SetPointTemp** desired property in hello **CoolerDevice** class:</span></span>

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

<span data-ttu-id="a4dcf-150">Questo metodo aggiorna il punto di dati di telemetria hello temperatura e quindi hello report modificare tooIoT indietro Hub impostando una proprietà segnalata.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-150">This method updates hello telemetry point temperature and then reports hello change back tooIoT Hub by setting a reported property.</span></span>

<span data-ttu-id="a4dcf-151">È possibile aggiungere i propri gestori per le proprietà dal modello hello in hello sopra riportato.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-151">You can add your own handlers for your own properties by following hello pattern in hello preceding example.</span></span>

<span data-ttu-id="a4dcf-152">È necessario anche associare gestore toohello di hello proprietà desiderata come illustrato nel seguente esempio di hello hello **CoolerDevice** costruttore:</span><span class="sxs-lookup"><span data-stu-id="a4dcf-152">You must also bind hello desired property toohello handler as shown in hello following example from hello **CoolerDevice** constructor:</span></span>

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

<span data-ttu-id="a4dcf-153">Si noti che **SetPointTempPropertyName** è una costante definita come "Config.SetPointTemp".</span><span class="sxs-lookup"><span data-stu-id="a4dcf-153">Note that **SetPointTempPropertyName** is a constant defined as "Config.SetPointTemp".</span></span>

### <a name="add-support-for-a-new-method-toohello-simulator"></a><span data-ttu-id="a4dcf-154">Aggiungere il supporto per un nuovo simulatore toohello (metodo)</span><span class="sxs-lookup"><span data-stu-id="a4dcf-154">Add support for a new method toohello simulator</span></span>

<span data-ttu-id="a4dcf-155">È possibile personalizzare il supporto di hello simulatore tooadd per un nuovo [metodo (metodo diretto)][lnk-direct-methods].</span><span class="sxs-lookup"><span data-stu-id="a4dcf-155">You can customize hello simulator tooadd support for a new [method (direct method)][lnk-direct-methods].</span></span> <span data-ttu-id="a4dcf-156">La procedura prevede due passaggi principali:</span><span class="sxs-lookup"><span data-stu-id="a4dcf-156">There are two key steps required:</span></span>

- <span data-ttu-id="a4dcf-157">simulatore Hello deve notificare hub IoT hello nella soluzione hello preconfigurato con i dettagli del metodo hello.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-157">hello simulator must notify hello IoT hub in hello preconfigured solution with details of hello method.</span></span>
- <span data-ttu-id="a4dcf-158">simulatore Hello deve includere chiamata al metodo hello toohandle codice quando viene richiamata da hello **dettagli dispositivo** pannello in Esplora soluzioni hello o tramite un processo.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-158">hello simulator must include code toohandle hello method call when you invoke it from hello **Device details** panel in hello solution explorer or through a job.</span></span>

<span data-ttu-id="a4dcf-159">Hello monitoraggio remoto preconfigurato soluzione utilizza *segnalati proprietà* toosend dettagli dell'hub tooIoT metodi supportati.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-159">hello remote monitoring preconfigured solution uses *reported properties* toosend details of supported methods tooIoT hub.</span></span> <span data-ttu-id="a4dcf-160">back-end di Hello soluzione gestisce un elenco di tutti i metodi di hello supportati da ogni dispositivo insieme a una cronologia delle chiamate al metodo.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-160">hello solution back end maintains a list of all hello methods supported by each device along with a history of method invocations.</span></span> <span data-ttu-id="a4dcf-161">È possibile visualizzare queste informazioni sui dispositivi e richiamare i metodi nel portale di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-161">You can view this information about devices and invoke methods in hello solution portal.</span></span>

<span data-ttu-id="a4dcf-162">toonotify hello IoT hub che un dispositivo supporta un metodo, il dispositivo hello necessario aggiungere i dettagli di hello metodo toohello **SupportedMethods** nodo hello segnalati proprietà:</span><span class="sxs-lookup"><span data-stu-id="a4dcf-162">toonotify hello IoT hub that a device supports a method, hello device must add details of hello method toohello **SupportedMethods** node in hello reported properties:</span></span>

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

<span data-ttu-id="a4dcf-163">firma del metodo Hello è hello seguente formato: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-163">hello method signature has hello following format: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span></span> <span data-ttu-id="a4dcf-164">Ad esempio, toospecify hello **InitiateFirmwareUpdate** metodo prevede un parametro di stringa denominato **FwPackageURI**, utilizzare hello firma del metodo seguente:</span><span class="sxs-lookup"><span data-stu-id="a4dcf-164">For example, toospecify hello **InitiateFirmwareUpdate** method expects a string parameter named **FwPackageURI**, use hello following method signature:</span></span>

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

<span data-ttu-id="a4dcf-165">Per un elenco dei tipi di parametro supportati, vedere hello **CommandTypes** classe nel progetto di infrastruttura hello.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-165">For a list of supported parameter types, see hello **CommandTypes** class in hello Infrastructure project.</span></span>

<span data-ttu-id="a4dcf-166">toodelete un metodo, impostare la firma del metodo hello troppo`null` in hello segnalati proprietà.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-166">toodelete a method, set hello method signature too`null` in hello reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="a4dcf-167">Hello soluzione back-end solo Aggiorna le informazioni sui metodi supportati quando si riceve un *informazioni sul dispositivo* messaggi da dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-167">hello solution back end only updates information about supported methods when it receives a *device information* message from hello device.</span></span>

<span data-ttu-id="a4dcf-168">Hello seguente codice di esempio hello **SampleDeviceFactory** classe hello comune progetto viene mostrato come un elenco di metodo toohello tooadd di **SupportedMethods** in hello segnalati proprietà inviata dal hello dispositivo:</span><span class="sxs-lookup"><span data-stu-id="a4dcf-168">hello following code sample from hello **SampleDeviceFactory** class in hello Common project shows how tooadd a method toohello list of **SupportedMethods** in hello reported properties sent by hello device:</span></span>

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' toospecifiy hello URI of hello firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

<span data-ttu-id="a4dcf-169">Questo frammento di codice aggiunge dettagli di hello **InitiateFirmwareUpdate** metodo incluso testo toodisplay portale soluzione hello e i dettagli di hello richiesto parametri del metodo.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-169">This code snippet adds details of hello **InitiateFirmwareUpdate** method including text toodisplay in hello solution portal and details of hello required method parameters.</span></span>

<span data-ttu-id="a4dcf-170">simulatore Hello invia proprietà segnalate, tra cui elenco hello dei metodi supportati, tooIoT Hub simulatore hello all'avvio.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-170">hello simulator sends reported properties, including hello list of supported methods, tooIoT Hub when hello simulator starts.</span></span>

<span data-ttu-id="a4dcf-171">Aggiungere un codice del simulatore toohello gestore per ogni metodo che supporta.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-171">Add a handler toohello simulator code for each method it supports.</span></span> <span data-ttu-id="a4dcf-172">È possibile visualizzare i gestori esistenti hello hello **CoolerDevice** classe nel progetto Simulator.WebJob hello.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-172">You can see hello existing handlers in hello **CoolerDevice** class in hello Simulator.WebJob project.</span></span> <span data-ttu-id="a4dcf-173">Hello esempio seguente viene illustrato il gestore di hello per **InitiateFirmwareUpdate** metodo:</span><span class="sxs-lookup"><span data-stu-id="a4dcf-173">hello following example shows hello handler for **InitiateFirmwareUpdate** method:</span></span>

```csharp
public async Task<MethodResponse> OnInitiateFirmwareUpdate(MethodRequest methodRequest, object userContext)
{
    if (_deviceManagementTask != null && !_deviceManagementTask.IsCompleted)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "Device is busy"
        }, 409));
    }

    try
    {
        var operation = new FirmwareUpdate(methodRequest);
        _deviceManagementTask = operation.Run(Transport).ContinueWith(async task =>
        {
            // after firmware completed, we reset telemetry
            var telemetry = _telemetryController as ITelemetryWithTemperatureMeanValue;
            if (telemetry != null)
            {
                telemetry.TemperatureMeanValue = 34.5;
            }

            await UpdateReportedTemperatureMeanValue();
        });

        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "FirmwareUpdate accepted",
            Uri = operation.Uri
        }));
    }
    catch (Exception ex)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = ex.Message
        }, 400));
    }
}
```

<span data-ttu-id="a4dcf-174">I nomi dei gestori di metodo deve iniziare con `On` aggiungendo il nome del metodo hello hello.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-174">Method handler names must start with `On` followed by hello name of hello method.</span></span> <span data-ttu-id="a4dcf-175">Hello **methodRequest** parametro contiene tutti i parametri passati con la chiamata di metodo hello dal back-end di hello soluzione.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-175">hello **methodRequest** parameter contains any parameters passed with hello method invocation from hello solution back end.</span></span> <span data-ttu-id="a4dcf-176">Hello valore restituito deve essere di tipo **attività&lt;MethodResponse&gt;**.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-176">hello return value must be of type **Task&lt;MethodResponse&gt;**.</span></span> <span data-ttu-id="a4dcf-177">Hello **BuildMethodResponse** metodo di utilità consente di creare il valore restituito di hello.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-177">hello **BuildMethodResponse** utility method helps you create hello return value.</span></span>

<span data-ttu-id="a4dcf-178">All'interno di gestore del metodo hello, è possibile:</span><span class="sxs-lookup"><span data-stu-id="a4dcf-178">Inside hello method handler, you could:</span></span>

- <span data-ttu-id="a4dcf-179">Avviare un'attività asincrona.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-179">Start an asynchronous task.</span></span>
- <span data-ttu-id="a4dcf-180">Recuperare le proprietà desiderate da hello *doppi dispositivo* nell'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-180">Retrieve desired properties from hello *device twin* in IoT Hub.</span></span>
- <span data-ttu-id="a4dcf-181">Aggiornare una singola proprietà segnalate tramite hello **SetReportedPropertyAsync** metodo hello **CoolerDevice** classe.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-181">Update a single reported property using hello **SetReportedPropertyAsync** method in hello **CoolerDevice** class.</span></span>
- <span data-ttu-id="a4dcf-182">Aggiornare più proprietà segnalate tramite la creazione di un **TwinCollection** istanza e chiamata hello **Transport.UpdateReportedPropertiesAsync** metodo.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-182">Update multiple reported properties by creating a **TwinCollection** instance and calling hello **Transport.UpdateReportedPropertiesAsync** method.</span></span>

<span data-ttu-id="a4dcf-183">Hello precedente esempio di aggiornamento del firmware esegue hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a4dcf-183">hello preceding firmware update example performs hello following steps:</span></span>

- <span data-ttu-id="a4dcf-184">Controlli dispositivo di hello è richiesta di aggiornamento del firmware tooaccept in grado di hello.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-184">Checks hello device is able tooaccept hello firmware update request.</span></span>
- <span data-ttu-id="a4dcf-185">Avvia l'operazione di aggiornamento del firmware hello e reimposta i dati di telemetria hello quando hello operazione è stata completata in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-185">Asynchronously initiates hello firmware update operation and resets hello telemetry when hello operation is complete.</span></span>
- <span data-ttu-id="a4dcf-186">Immediatamente restituisce hello "FirmwareUpdate accettato" messaggio tooindicate hello richiesta è stata accettata dal dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-186">Immediately returns hello "FirmwareUpdate accepted" message tooindicate hello request was accepted by hello device.</span></span>

### <a name="build-and-use-your-own-physical-device"></a><span data-ttu-id="a4dcf-187">Compilare e usare il proprio dispositivo (fisico)</span><span class="sxs-lookup"><span data-stu-id="a4dcf-187">Build and use your own (physical) device</span></span>

<span data-ttu-id="a4dcf-188">Hello [Azure IoT SDK](https://github.com/Azure/azure-iot-sdks) forniscono librerie per la connessione di vari tipi di dispositivo (lingue e i sistemi operativi) in soluzioni IoT.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-188">hello [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) provide libraries for connecting numerous device types (languages and operating systems) into IoT solutions.</span></span>

## <a name="modify-dashboard-limits"></a><span data-ttu-id="a4dcf-189">Modificare i limiti del dashboard</span><span class="sxs-lookup"><span data-stu-id="a4dcf-189">Modify dashboard limits</span></span>

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a><span data-ttu-id="a4dcf-190">Numero di dispositivi visualizzati nell'elenco a discesa del dashboard</span><span class="sxs-lookup"><span data-stu-id="a4dcf-190">Number of devices displayed in dashboard dropdown</span></span>

<span data-ttu-id="a4dcf-191">valore predefinito di Hello è 200.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-191">hello default is 200.</span></span> <span data-ttu-id="a4dcf-192">È possibile modificare questo numero nel file [DashboardController.cs][lnk-dashboard-controller].</span><span class="sxs-lookup"><span data-stu-id="a4dcf-192">You can change this number in [DashboardController.cs][lnk-dashboard-controller].</span></span>

### <a name="number-of-pins-toodisplay-in-bing-map-control"></a><span data-ttu-id="a4dcf-193">Numero di pin toodisplay nel controllo mappa di Bing</span><span class="sxs-lookup"><span data-stu-id="a4dcf-193">Number of pins toodisplay in Bing Map control</span></span>

<span data-ttu-id="a4dcf-194">valore predefinito di Hello è 200.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-194">hello default is 200.</span></span> <span data-ttu-id="a4dcf-195">È possibile modificare questo numero nel file [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span><span class="sxs-lookup"><span data-stu-id="a4dcf-195">You can change this number in [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span></span>

### <a name="time-period-of-telemetry-graph"></a><span data-ttu-id="a4dcf-196">Periodo di tempo del grafico di dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="a4dcf-196">Time period of telemetry graph</span></span>

<span data-ttu-id="a4dcf-197">valore predefinito di Hello è 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-197">hello default is 10 minutes.</span></span> <span data-ttu-id="a4dcf-198">È possibile modificare questo valore nel file [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span><span class="sxs-lookup"><span data-stu-id="a4dcf-198">You can change this value in [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span></span>

## <a name="manually-set-up-application-roles"></a><span data-ttu-id="a4dcf-199">Configurare manualmente i ruoli dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="a4dcf-199">Manually set up application roles</span></span>

<span data-ttu-id="a4dcf-200">Hello procedura riportata di seguito viene descritto come tooadd **Admin** e **ReadOnly** tooa ruoli applicazione preconfigurato soluzione.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-200">hello following procedure describes how tooadd **Admin** and **ReadOnly** application roles tooa preconfigured solution.</span></span> <span data-ttu-id="a4dcf-201">Si noti che le soluzioni preconfigurate già eseguito il provisioning dal sito azureiotsuite.com hello includono hello **Admin** e **ReadOnly** ruoli.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-201">Note that preconfigured solutions provisioned from hello azureiotsuite.com site already include hello **Admin** and **ReadOnly** roles.</span></span>

<span data-ttu-id="a4dcf-202">I membri di hello **ReadOnly** ruolo è possibile visualizzare dashboard hello e l'elenco dei dispositivi hello, ma non sono consentiti tooadd dispositivi, gli attributi di modifica dispositivo o i comandi di trasmissione.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-202">Members of hello **ReadOnly** role can see hello dashboard and hello device list, but are not allowed tooadd devices, change device attributes, or send commands.</span></span>  <span data-ttu-id="a4dcf-203">I membri di hello **Admin** ruolo dispone di funzionalità di accesso completo tooall hello nella soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-203">Members of hello **Admin** role have full access tooall hello functionality in hello solution.</span></span>

1. <span data-ttu-id="a4dcf-204">Passare toohello [portale di Azure classico][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="a4dcf-204">Go toohello [Azure classic portal][lnk-classic-portal].</span></span>
2. <span data-ttu-id="a4dcf-205">Selezionare **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-205">Select **Active Directory**.</span></span>
3. <span data-ttu-id="a4dcf-206">Fare clic su nome hello del tenant AAD hello che è utilizzato quando è stato effettuato il provisioning della soluzione.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-206">Click hello name of hello AAD tenant you used when you provisioned your solution.</span></span>
4. <span data-ttu-id="a4dcf-207">Fare clic su **Applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-207">Click **Applications**.</span></span>
5. <span data-ttu-id="a4dcf-208">Fare clic su nome hello dell'applicazione hello che corrisponde al nome della soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-208">Click hello name of hello application that matches your preconfigured solution name.</span></span> <span data-ttu-id="a4dcf-209">Se non viene visualizzata l'applicazione nell'elenco di hello, selezionare **applicazioni proprietà dell'azienda** in hello **Mostra** elenco a discesa e fare clic su hello segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-209">If you don't see your application in hello list, select **Applications my company owns** in hello **Show** dropdown and click hello check mark.</span></span>
6. <span data-ttu-id="a4dcf-210">Nella parte inferiore di hello della pagina hello, fare clic su **Gestisci manifesto** e quindi **Scarica manifesto**.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-210">At hello bottom of hello page, click **Manage Manifest** and then **Download Manifest**.</span></span>
7. <span data-ttu-id="a4dcf-211">Questa procedura consente di scaricare una versione locale macchina tooyour di file con estensione JSON.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-211">This procedure downloads a .json file tooyour local machine.</span></span> <span data-ttu-id="a4dcf-212">Aprire il file per modificarlo in un editor di testo di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-212">Open this file for editing in a text editor of your choice.</span></span>
8. <span data-ttu-id="a4dcf-213">Nella terza riga hello del file con estensione JSON hello, è possibile visualizzare:</span><span class="sxs-lookup"><span data-stu-id="a4dcf-213">On hello third line of hello .json file, you can see:</span></span>

   ```json
   "appRoles" : [],
   ```
   <span data-ttu-id="a4dcf-214">Sostituire questa riga con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="a4dcf-214">Replace this line with hello following code:</span></span>

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access toohello application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access toodevice information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. <span data-ttu-id="a4dcf-215">Salvare file con estensione JSON aggiornato hello (è possibile sovrascrivere il file esistente di hello).</span><span class="sxs-lookup"><span data-stu-id="a4dcf-215">Save hello updated .json file (you can overwrite hello existing file).</span></span>
10. <span data-ttu-id="a4dcf-216">Nel portale di Azure classico, nella parte inferiore di hello della pagina hello hello selezionare **Gestisci manifesto** quindi **carica manifesto** file con estensione JSON di hello tooupload salvato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-216">In hello Azure classic portal, at hello bottom of hello page, select **Manage Manifest** then **Upload Manifest** tooupload hello .json file you saved in hello previous step.</span></span>
11. <span data-ttu-id="a4dcf-217">È stato aggiunto hello **Admin** e **ReadOnly** applicazione tooyour dei ruoli.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-217">You have now added hello **Admin** and **ReadOnly** roles tooyour application.</span></span>
12. <span data-ttu-id="a4dcf-218">tooassign uno di questi utente tooa ruoli nella directory, vedere [le autorizzazioni nel sito azureiotsuite.com hello][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="a4dcf-218">tooassign one of these roles tooa user in your directory, see [Permissions on hello azureiotsuite.com site][lnk-permissions].</span></span>

## <a name="feedback"></a><span data-ttu-id="a4dcf-219">Commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="a4dcf-219">Feedback</span></span>

<span data-ttu-id="a4dcf-220">Si dispone di una personalizzazione che si desidera toosee trattate in questo documento?</span><span class="sxs-lookup"><span data-stu-id="a4dcf-220">Do you have a customization you'd like toosee covered in this document?</span></span> <span data-ttu-id="a4dcf-221">Aggiungere i suggerimenti sulle funzionalità troppo[Uservoice](https://feedback.azure.com/forums/321918-azure-iot), o un commento di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a4dcf-221">Add feature suggestions too[User Voice](https://feedback.azure.com/forums/321918-azure-iot), or comment on this article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a4dcf-222">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a4dcf-222">Next steps</span></span>

<span data-ttu-id="a4dcf-223">toolearn più sulle opzioni di hello per personalizzare soluzioni hello preconfigurato, vedere:</span><span class="sxs-lookup"><span data-stu-id="a4dcf-223">toolearn more about hello options for customizing hello preconfigured solutions, see:</span></span>

* <span data-ttu-id="a4dcf-224">[Connessione logica App tooyour Azure IoT Suite remoto preconfigurato soluzione di monitoraggio][lnk-logicapp]</span><span class="sxs-lookup"><span data-stu-id="a4dcf-224">[Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapp]</span></span>
* <span data-ttu-id="a4dcf-225">[Utilizzare i dati di telemetria dinamico con hello soluzione preconfigurata di monitoraggio remoto][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="a4dcf-225">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="a4dcf-226">[Metadati informazioni del dispositivo nella soluzione preconfigurata di monitoraggio remoto hello][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="a4dcf-226">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo]</span></span>
* <span data-ttu-id="a4dcf-227">[Personalizzare la modalità di connessione factory soluzione consente di visualizzare dati dai server OPC UA hello][lnk-cf-customize]</span><span class="sxs-lookup"><span data-stu-id="a4dcf-227">[Customize how hello connected factory solution displays data from your OPC UA servers][lnk-cf-customize]</span></span>

[lnk-logicapp]: iot-suite-logic-apps-tutorial.md
[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[IoT Device SDK]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-permissions]: iot-suite-permissions.md
[lnk-dashboard-controller]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/Controllers/DashboardController.cs#L27
[lnk-telemetry-api-controller-01]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L27
[lnk-telemetry-api-controller-02]: https://github.com/Azure/azure-iot-remote-monitoring/blob/e7003339f73e21d3930f71ceba1e74fb5c0d9ea0/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L25 
[lnk-sample-device-factory]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Common/Factory/SampleDeviceFactory.cs#L40
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-cf-customize]: iot-suite-connected-factory-customize.md