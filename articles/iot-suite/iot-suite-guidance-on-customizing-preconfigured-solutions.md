---
title: Personalizzazione di soluzioni preconfigurate | Documentazione Microsoft
description: Fornisce una guida alla personalizzazione delle soluzioni preconfigurate di Azure IoT Suite.
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
ms.openlocfilehash: bdf4cd89d5ad0392337dfe761108608d506adf18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="customize-a-preconfigured-solution"></a><span data-ttu-id="9a8bd-103">Personalizzare una soluzione preconfigurata</span><span class="sxs-lookup"><span data-stu-id="9a8bd-103">Customize a preconfigured solution</span></span>

<span data-ttu-id="9a8bd-104">Le soluzioni preconfigurate disponibili in Azure IoT Suite dimostrano come i servizi nella suite si integrano per fornire una soluzione end-to-end.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-104">The preconfigured solutions provided with the Azure IoT Suite demonstrate the services within the suite working together to deliver an end-to-end solution.</span></span> <span data-ttu-id="9a8bd-105">Esistono poi diverse posizioni in cui è possibile personalizzare ed estendere la soluzione per adattarla a scenari specifici.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-105">From this starting point, there are various places in which you can extend and customize the solution for specific scenarios.</span></span> <span data-ttu-id="9a8bd-106">Le sezioni seguenti descrivono questi punti di personalizzazione comuni.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-106">The following sections describe these common customization points.</span></span>

## <a name="find-the-source-code"></a><span data-ttu-id="9a8bd-107">Trovare il codice sorgente</span><span class="sxs-lookup"><span data-stu-id="9a8bd-107">Find the source code</span></span>

<span data-ttu-id="9a8bd-108">Il codice sorgente per le soluzioni preconfigurate è disponibile in GitHub nei repository seguenti:</span><span class="sxs-lookup"><span data-stu-id="9a8bd-108">The source code for the preconfigured solutions is available on GitHub in the following repositories:</span></span>

* <span data-ttu-id="9a8bd-109">Monitoraggio remoto: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span><span class="sxs-lookup"><span data-stu-id="9a8bd-109">Remote Monitoring: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span></span>
* <span data-ttu-id="9a8bd-110">Manutenzione predittiva: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span><span class="sxs-lookup"><span data-stu-id="9a8bd-110">Predictive Maintenance: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span></span>
* <span data-ttu-id="9a8bd-111">Factory connesso: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span><span class="sxs-lookup"><span data-stu-id="9a8bd-111">Connected factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span></span>

<span data-ttu-id="9a8bd-112">Il codice sorgente per le soluzioni preconfigurate viene fornito per illustrare i modelli e le procedure usate per implementare la funzionalità end-to-end di una soluzione IoT tramite Azure IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-112">The source code for the preconfigured solutions is provided to demonstrate the patterns and practices used to implement the end-to-end functionality of an IoT solution using Azure IoT Suite.</span></span> <span data-ttu-id="9a8bd-113">È possibile trovare altre informazioni su come compilare e distribuire le soluzioni in repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-113">You can find more information about how to build and deploy the solutions in the GitHub repositories.</span></span>

## <a name="change-the-preconfigured-rules"></a><span data-ttu-id="9a8bd-114">Modificare le regole preconfigurate</span><span class="sxs-lookup"><span data-stu-id="9a8bd-114">Change the preconfigured rules</span></span>

<span data-ttu-id="9a8bd-115">La soluzione per il monitoraggio remoto include tre processi di [Analisi di flusso di Azure](https://azure.microsoft.com/services/stream-analytics/) per gestire le informazioni sul dispositivo, la telemetria e la logica delle regole nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-115">The remote monitoring solution includes three [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jobs to handle device information, telemetry, and rules logic in the solution.</span></span>

<span data-ttu-id="9a8bd-116">I tre processi di analisi di flusso e la relativa sintassi sono descritti in dettaglio in [Procedura dettagliata della soluzione preconfigurata per il monitoraggio remoto](iot-suite-remote-monitoring-sample-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="9a8bd-116">The three stream analytics jobs and their syntax are described in depth in the [Remote monitoring preconfigured solution walkthrough](iot-suite-remote-monitoring-sample-walkthrough.md).</span></span> 

<span data-ttu-id="9a8bd-117">È possibile modificare questi processi direttamente per alterare la logica o aggiungere una logica specifica allo scenario.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-117">You can edit these jobs directly to alter the logic, or add logic specific to your scenario.</span></span> <span data-ttu-id="9a8bd-118">È possibile trovare i processi di analisi di flusso come segue:</span><span class="sxs-lookup"><span data-stu-id="9a8bd-118">You can find the Stream Analytics jobs as follows:</span></span>

1. <span data-ttu-id="9a8bd-119">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9a8bd-119">Go to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9a8bd-120">Passare a un nuovo gruppo di risorse con lo stesso nome della soluzione IoT.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-120">Navigate to the resource group with the same name as your IoT solution.</span></span> 
3. <span data-ttu-id="9a8bd-121">Selezionare il processo di Analisi di flusso di Azure che si vuole modificare.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-121">Select the Azure Stream Analytics job you'd like to modify.</span></span> 
4. <span data-ttu-id="9a8bd-122">Arrestare il processo selezionando **Arresta** nel set di comandi.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-122">Stop the job by selecting **Stop** in the set of commands.</span></span> 
5. <span data-ttu-id="9a8bd-123">Modificare i valori di input, query e output.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-123">Edit the inputs, query, and outputs.</span></span>
   
    <span data-ttu-id="9a8bd-124">Una modifica semplice consiste nel cambiare la query per il processo **Regole** in modo da usare **"<"** anziché **">"**.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-124">A simple modification is to change the query for the **Rules** job to use a **"<"** instead of a **">"**.</span></span> <span data-ttu-id="9a8bd-125">Il portale della soluzione visualizza ancora **">"** quando si modifica una regola, ma si noterà come il comportamento viene capovolto a causa della modifica del processo sottostante.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-125">The solution portal still shows **">"** when you edit a rule, but notice how the behavior is flipped due to the change in the underlying job.</span></span>
6. <span data-ttu-id="9a8bd-126">Avviare il processo</span><span class="sxs-lookup"><span data-stu-id="9a8bd-126">Start the job</span></span>

> [!NOTE]
> <span data-ttu-id="9a8bd-127">Il dashboard per il monitoraggio remoto dipende da dati specifici, quindi la modifica dei processi può causare un errore del dashboard.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-127">The remote monitoring dashboard depends on specific data, so altering the jobs can cause the dashboard to fail.</span></span>

## <a name="add-your-own-rules"></a><span data-ttu-id="9a8bd-128">Aggiungere le regole personalizzate</span><span class="sxs-lookup"><span data-stu-id="9a8bd-128">Add your own rules</span></span>

<span data-ttu-id="9a8bd-129">Oltre a modificare i processi preconfigurati di analisi di flusso di Azure, è possibile usare il portale di Azure per aggiungere nuovi processi o nuove query ai processi esistenti.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-129">In addition to changing the preconfigured Azure Stream Analytics jobs, you can use the Azure portal to add new jobs or add new queries to existing jobs.</span></span>

## <a name="customize-devices"></a><span data-ttu-id="9a8bd-130">Personalizzare i dispositivi</span><span class="sxs-lookup"><span data-stu-id="9a8bd-130">Customize devices</span></span>

<span data-ttu-id="9a8bd-131">Una delle attività di estensione più comuni è l'uso di dispositivi specifici per lo scenario.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-131">One of the most common extension activities is working with devices specific to your scenario.</span></span> <span data-ttu-id="9a8bd-132">Esistono diversi metodi per usare i dispositivi,</span><span class="sxs-lookup"><span data-stu-id="9a8bd-132">There are several methods for working with devices.</span></span> <span data-ttu-id="9a8bd-133">tra cui modificare un dispositivo simulato in modo che corrisponda allo scenario o usare l'[IoT Device SDK][IoT Device SDK] per connettere il dispositivo fisico alla soluzione.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-133">These methods include altering a simulated device to match your scenario, or using the [IoT Device SDK][IoT Device SDK] to connect your physical device to the solution.</span></span>

<span data-ttu-id="9a8bd-134">Per indicazioni dettagliate sull'aggiunta di dispositivi, vedere l'articolo [Dispositivi di connessione a Iot Suite](iot-suite-connecting-devices.md) e [Remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring) (Esempio C SDK per il monitoraggio remoto).</span><span class="sxs-lookup"><span data-stu-id="9a8bd-134">For a step-by-step guide to adding devices, see the [Iot Suite Connecting Devices](iot-suite-connecting-devices.md) article and the [remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span></span> <span data-ttu-id="9a8bd-135">Questo esempio è stato progettato in modo specifico per la soluzione preconfigurata per il monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-135">This sample is designed to work with the remote monitoring preconfigured solution.</span></span>

### <a name="create-your-own-simulated-device"></a><span data-ttu-id="9a8bd-136">Creare il dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="9a8bd-136">Create your own simulated device</span></span>

<span data-ttu-id="9a8bd-137">Nel [codice sorgente della soluzione per il monitoraggio remoto](https://github.com/Azure/azure-iot-remote-monitoring) è incluso un simulatore .NET.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-137">Included in the [remote monitoring solution source code](https://github.com/Azure/azure-iot-remote-monitoring), is a .NET simulator.</span></span> <span data-ttu-id="9a8bd-138">Il provisioning di questo simulatore viene eseguito nell'ambito della soluzione ed è possibile modificarlo per inviare metadati diversi, la telemetria o per rispondere a comandi e metodi diversi.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-138">This simulator is the one provisioned as part of the solution and you can alter it to send different metadata, telemetry, and respond to different commands and methods.</span></span>

<span data-ttu-id="9a8bd-139">Il simulatore preconfigurato nella soluzione preconfigurata per il monitoraggio remoto simula un dispositivo ad accesso sporadico che emette dati di telemetria su temperatura e umidità.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-139">The preconfigured simulator in the remote monitoring preconfigured solution simulates a cooler device that emits temperature and humidity telemetry.</span></span> <span data-ttu-id="9a8bd-140">È possibile modificare il simulatore nel progetto [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) una volta duplicato il repository di GitHub.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-140">You can modify the simulator in the [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) project when you've forked the GitHub repository.</span></span>

### <a name="available-locations-for-simulated-devices"></a><span data-ttu-id="9a8bd-141">Posizioni disponibili per i dispositivi simulati</span><span class="sxs-lookup"><span data-stu-id="9a8bd-141">Available locations for simulated devices</span></span>

<span data-ttu-id="9a8bd-142">Il set predefinito di posizioni si trova a Seattle/Redmond, Washington, Stati Uniti d'America.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-142">The default set of locations is in Seattle/Redmond, Washington, United States of America.</span></span> <span data-ttu-id="9a8bd-143">È possibile modificare queste località nel file [SampleDeviceFactory.cs][lnk-sample-device-factory].</span><span class="sxs-lookup"><span data-stu-id="9a8bd-143">You can change these locations in [SampleDeviceFactory.cs][lnk-sample-device-factory].</span></span>

### <a name="add-a-desired-property-update-handler-to-the-simulator"></a><span data-ttu-id="9a8bd-144">Aggiungere un gestore di aggiornamento della proprietà desiderata al simulatore</span><span class="sxs-lookup"><span data-stu-id="9a8bd-144">Add a desired property update handler to the simulator</span></span>

<span data-ttu-id="9a8bd-145">È possibile configurare un valore per la proprietà desiderata per un dispositivo nel portale della soluzione.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-145">You can set a value for a desired property for a device in the solution portal.</span></span> <span data-ttu-id="9a8bd-146">La gestione della richiesta di modifica della proprietà quando il dispositivo recupera il valore della proprietà desiderata è a carico del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-146">It is the responsibility of the device to handle the property change request when the device retrieves the desired property value.</span></span> <span data-ttu-id="9a8bd-147">Per aggiungere il supporto per una modifica del valore della proprietà tramite una proprietà desiderata, è necessario aggiungere un gestore al simulatore.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-147">To add support for a property value change through a desired property, you need to add a handler to the simulator.</span></span>

<span data-ttu-id="9a8bd-148">Il simulatore contiene gestori per le proprietà **SetPointTemp** e **TelemetryInterval** che possono essere aggiornate impostando i valori desiderati nel portale della soluzione.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-148">The simulator contains handlers for the **SetPointTemp** and **TelemetryInterval** properties that you can update by setting desired values in the solution portal.</span></span>

<span data-ttu-id="9a8bd-149">L'esempio seguente mostra il gestore per la proprietà desiderata **SetPointTemp** nella classe **CoolerDevice**:</span><span class="sxs-lookup"><span data-stu-id="9a8bd-149">The following example shows the handler for the **SetPointTemp** desired property in the **CoolerDevice** class:</span></span>

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

<span data-ttu-id="9a8bd-150">Questo metodo aggiorna la temperatura del punto dati di telemetria e quindi segnala la modifica all'hub IoT impostando una proprietà segnalata.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-150">This method updates the telemetry point temperature and then reports the change back to IoT Hub by setting a reported property.</span></span>

<span data-ttu-id="9a8bd-151">È possibile aggiungere gestori personalizzati per le proprietà specifiche seguendo il modello dell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-151">You can add your own handlers for your own properties by following the pattern in the preceding example.</span></span>

<span data-ttu-id="9a8bd-152">È anche necessario associare la proprietà desiderata al gestore, come illustrato nell'esempio seguente dal costruttore **CoolerDevice**:</span><span class="sxs-lookup"><span data-stu-id="9a8bd-152">You must also bind the desired property to the handler as shown in the following example from the **CoolerDevice** constructor:</span></span>

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

<span data-ttu-id="9a8bd-153">Si noti che **SetPointTempPropertyName** è una costante definita come "Config.SetPointTemp".</span><span class="sxs-lookup"><span data-stu-id="9a8bd-153">Note that **SetPointTempPropertyName** is a constant defined as "Config.SetPointTemp".</span></span>

### <a name="add-support-for-a-new-method-to-the-simulator"></a><span data-ttu-id="9a8bd-154">Aggiungere il supporto per un nuovo metodo al simulatore</span><span class="sxs-lookup"><span data-stu-id="9a8bd-154">Add support for a new method to the simulator</span></span>

<span data-ttu-id="9a8bd-155">È possibile personalizzare il simulatore per aggiungere il supporto per un nuovo [metodo (metodo diretto)][lnk-direct-methods].</span><span class="sxs-lookup"><span data-stu-id="9a8bd-155">You can customize the simulator to add support for a new [method (direct method)][lnk-direct-methods].</span></span> <span data-ttu-id="9a8bd-156">La procedura prevede due passaggi principali:</span><span class="sxs-lookup"><span data-stu-id="9a8bd-156">There are two key steps required:</span></span>

- <span data-ttu-id="9a8bd-157">Il simulatore deve inviare una notifica all'hub IoT nella soluzione preconfigurata con i dettagli del metodo.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-157">The simulator must notify the IoT hub in the preconfigured solution with details of the method.</span></span>
- <span data-ttu-id="9a8bd-158">Il simulatore deve includere il codice per gestire la chiamata al metodo quando viene richiamato dal pannello **Dettagli dispositivo** in Esplora soluzioni o tramite un processo.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-158">The simulator must include code to handle the method call when you invoke it from the **Device details** panel in the solution explorer or through a job.</span></span>

<span data-ttu-id="9a8bd-159">La soluzione preconfigurata per il monitoraggio remoto usa le *proprietà segnalate* per inviare i dettagli dei metodi supportati all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-159">The remote monitoring preconfigured solution uses *reported properties* to send details of supported methods to IoT hub.</span></span> <span data-ttu-id="9a8bd-160">Il back-end della soluzione gestisce un elenco di tutti i metodi supportati da ogni dispositivo, insieme a una cronologia delle chiamate al metodo.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-160">The solution back end maintains a list of all the methods supported by each device along with a history of method invocations.</span></span> <span data-ttu-id="9a8bd-161">È possibile visualizzare queste informazioni sui dispositivi e richiamare i metodi nel portale della soluzione.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-161">You can view this information about devices and invoke methods in the solution portal.</span></span>

<span data-ttu-id="9a8bd-162">Per segnalare all'hub IoT che un dispositivo supporta un metodo, il dispositivo deve aggiungere i dettagli del metodo al nodo **SupportedMethods** nelle proprietà segnalate:</span><span class="sxs-lookup"><span data-stu-id="9a8bd-162">To notify the IoT hub that a device supports a method, the device must add details of the method to the **SupportedMethods** node in the reported properties:</span></span>

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

<span data-ttu-id="9a8bd-163">La firma del metodo ha il formato seguente: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-163">The method signature has the following format: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span></span> <span data-ttu-id="9a8bd-164">Per specificare, ad esempio, che il metodo **InitiateFirmwareUpdate** prevede un parametro di stringa denominato **FwPackageURI**, usare la firma del metodo seguente:</span><span class="sxs-lookup"><span data-stu-id="9a8bd-164">For example, to specify the **InitiateFirmwareUpdate** method expects a string parameter named **FwPackageURI**, use the following method signature:</span></span>

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

<span data-ttu-id="9a8bd-165">Per un elenco di tipi di parametri supportati, vedere la classe **CommandTypes** nel progetto Infrastructure.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-165">For a list of supported parameter types, see the **CommandTypes** class in the Infrastructure project.</span></span>

<span data-ttu-id="9a8bd-166">Per eliminare un metodo, impostare la firma del metodo su `null` nelle proprietà segnalate.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-166">To delete a method, set the method signature to `null` in the reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="9a8bd-167">Il back-end della soluzione aggiorna solo le informazioni sui metodi supportati quando riceve un messaggio sulle *informazioni del dispositivo* dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-167">The solution back end only updates information about supported methods when it receives a *device information* message from the device.</span></span>

<span data-ttu-id="9a8bd-168">L'esempio di codice seguente dalla classe **SampleDeviceFactory** nel progetto Common mostra come aggiungere un metodo all'elenco **SupportedMethods** nelle proprietà segnalate inviate dal dispositivo:</span><span class="sxs-lookup"><span data-stu-id="9a8bd-168">The following code sample from the **SampleDeviceFactory** class in the Common project shows how to add a method to the list of **SupportedMethods** in the reported properties sent by the device:</span></span>

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' to specifiy the URI of the firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

<span data-ttu-id="9a8bd-169">Questo frammento di codice aggiunge i dettagli del metodo **InitiateFirmwareUpdate**, incluso il testo da visualizzare nel portale della soluzione e i dettagli dei parametri del metodo necessario.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-169">This code snippet adds details of the **InitiateFirmwareUpdate** method including text to display in the solution portal and details of the required method parameters.</span></span>

<span data-ttu-id="9a8bd-170">Il simulatore invia le proprietà segnalate, incluso l'elenco dei metodi supportati, all'hub IoT quando viene avviato.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-170">The simulator sends reported properties, including the list of supported methods, to IoT Hub when the simulator starts.</span></span>

<span data-ttu-id="9a8bd-171">Aggiungere un gestore al codice del simulatore per ogni metodo supportato.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-171">Add a handler to the simulator code for each method it supports.</span></span> <span data-ttu-id="9a8bd-172">È possibile visualizzare i gestori esistenti nella classe **CoolerDevice** del progetto Simulator.WebJob.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-172">You can see the existing handlers in the **CoolerDevice** class in the Simulator.WebJob project.</span></span> <span data-ttu-id="9a8bd-173">L'esempio seguente mostra il gestore per il metodo **InitiateFirmwareUpdate**:</span><span class="sxs-lookup"><span data-stu-id="9a8bd-173">The following example shows the handler for **InitiateFirmwareUpdate** method:</span></span>

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

<span data-ttu-id="9a8bd-174">I nomi dei gestori dei metodi devono iniziare con `On`, seguito dal nome del metodo.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-174">Method handler names must start with `On` followed by the name of the method.</span></span> <span data-ttu-id="9a8bd-175">Il parametro **methodRequest** contiene tutti i parametri passati con la chiamata al metodo dal back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-175">The **methodRequest** parameter contains any parameters passed with the method invocation from the solution back end.</span></span> <span data-ttu-id="9a8bd-176">Il valore restituito deve essere di tipo **Task&lt;MethodResponse&gt;**.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-176">The return value must be of type **Task&lt;MethodResponse&gt;**.</span></span> <span data-ttu-id="9a8bd-177">Il metodo **BuildMethodResponse** dell'utilità consente di creare il valore restituito.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-177">The **BuildMethodResponse** utility method helps you create the return value.</span></span>

<span data-ttu-id="9a8bd-178">All'interno del gestore del metodo è possibile eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="9a8bd-178">Inside the method handler, you could:</span></span>

- <span data-ttu-id="9a8bd-179">Avviare un'attività asincrona.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-179">Start an asynchronous task.</span></span>
- <span data-ttu-id="9a8bd-180">Recuperare le proprietà desiderate dal *dispositivo gemello* nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-180">Retrieve desired properties from the *device twin* in IoT Hub.</span></span>
- <span data-ttu-id="9a8bd-181">Aggiornare una singola proprietà segnalata usando il metodo **SetReportedPropertyAsync** nella classe **CoolerDevice**.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-181">Update a single reported property using the **SetReportedPropertyAsync** method in the **CoolerDevice** class.</span></span>
- <span data-ttu-id="9a8bd-182">Aggiornare più proprietà segnalate creando un'istanza di **TwinCollection** e chiamando il metodo **Transport.UpdateReportedPropertiesAsync**.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-182">Update multiple reported properties by creating a **TwinCollection** instance and calling the **Transport.UpdateReportedPropertiesAsync** method.</span></span>

<span data-ttu-id="9a8bd-183">L'esempio precedente di aggiornamento del firmware segue questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9a8bd-183">The preceding firmware update example performs the following steps:</span></span>

- <span data-ttu-id="9a8bd-184">Controlla che il dispositivo sia in grado di accettare la richiesta di aggiornamento del firmware.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-184">Checks the device is able to accept the firmware update request.</span></span>
- <span data-ttu-id="9a8bd-185">Avvia in modo asincrono l'operazione di aggiornamento del firmware e reimposta i dati di telemetria al termine dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-185">Asynchronously initiates the firmware update operation and resets the telemetry when the operation is complete.</span></span>
- <span data-ttu-id="9a8bd-186">Restituisce immediatamente il messaggio "FirmwareUpdate accepted" per indicare che la richiesta è stata accettata dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-186">Immediately returns the "FirmwareUpdate accepted" message to indicate the request was accepted by the device.</span></span>

### <a name="build-and-use-your-own-physical-device"></a><span data-ttu-id="9a8bd-187">Compilare e usare il proprio dispositivo (fisico)</span><span class="sxs-lookup"><span data-stu-id="9a8bd-187">Build and use your own (physical) device</span></span>

<span data-ttu-id="9a8bd-188">Gli [SDK Azure IoT](https://github.com/Azure/azure-iot-sdks) forniscono librerie per la connessione di numerosi tipi di dispositivi (linguaggi e sistemi operativi) alle soluzioni IoT.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-188">The [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) provide libraries for connecting numerous device types (languages and operating systems) into IoT solutions.</span></span>

## <a name="modify-dashboard-limits"></a><span data-ttu-id="9a8bd-189">Modificare i limiti del dashboard</span><span class="sxs-lookup"><span data-stu-id="9a8bd-189">Modify dashboard limits</span></span>

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a><span data-ttu-id="9a8bd-190">Numero di dispositivi visualizzati nell'elenco a discesa del dashboard</span><span class="sxs-lookup"><span data-stu-id="9a8bd-190">Number of devices displayed in dashboard dropdown</span></span>

<span data-ttu-id="9a8bd-191">Il valore predefinito è 200.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-191">The default is 200.</span></span> <span data-ttu-id="9a8bd-192">È possibile modificare questo numero nel file [DashboardController.cs][lnk-dashboard-controller].</span><span class="sxs-lookup"><span data-stu-id="9a8bd-192">You can change this number in [DashboardController.cs][lnk-dashboard-controller].</span></span>

### <a name="number-of-pins-to-display-in-bing-map-control"></a><span data-ttu-id="9a8bd-193">Numero di pin da visualizzare nel controllo di Bing Mappe</span><span class="sxs-lookup"><span data-stu-id="9a8bd-193">Number of pins to display in Bing Map control</span></span>

<span data-ttu-id="9a8bd-194">Il valore predefinito è 200.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-194">The default is 200.</span></span> <span data-ttu-id="9a8bd-195">È possibile modificare questo numero nel file [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span><span class="sxs-lookup"><span data-stu-id="9a8bd-195">You can change this number in [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span></span>

### <a name="time-period-of-telemetry-graph"></a><span data-ttu-id="9a8bd-196">Periodo di tempo del grafico di dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="9a8bd-196">Time period of telemetry graph</span></span>

<span data-ttu-id="9a8bd-197">Il valore predefinito è 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-197">The default is 10 minutes.</span></span> <span data-ttu-id="9a8bd-198">È possibile modificare questo valore nel file [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span><span class="sxs-lookup"><span data-stu-id="9a8bd-198">You can change this value in [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span></span>

## <a name="manually-set-up-application-roles"></a><span data-ttu-id="9a8bd-199">Configurare manualmente i ruoli dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="9a8bd-199">Manually set up application roles</span></span>

<span data-ttu-id="9a8bd-200">La procedura seguente descrive come aggiungere i ruoli applicazione **Admin** e **ReadOnly** a una soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-200">The following procedure describes how to add **Admin** and **ReadOnly** application roles to a preconfigured solution.</span></span> <span data-ttu-id="9a8bd-201">Si noti che le soluzioni preconfigurate per le quali è stato eseguito il provisioning dal sito azureiotsuite.com includono già i ruoli **Admin** e **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-201">Note that preconfigured solutions provisioned from the azureiotsuite.com site already include the **Admin** and **ReadOnly** roles.</span></span>

<span data-ttu-id="9a8bd-202">I membri del ruolo **ReadOnly** possono visualizzare il dashboard e l'elenco dei dispositivi, ma non sono autorizzati ad aggiungere dispositivi, modificare gli attributi del dispositivo o inviare comandi.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-202">Members of the **ReadOnly** role can see the dashboard and the device list, but are not allowed to add devices, change device attributes, or send commands.</span></span>  <span data-ttu-id="9a8bd-203">I membri del ruolo **Admin** hanno accesso completo a tutte le funzionalità nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-203">Members of the **Admin** role have full access to all the functionality in the solution.</span></span>

1. <span data-ttu-id="9a8bd-204">Passare al [portale di Azure classico][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="9a8bd-204">Go to the [Azure classic portal][lnk-classic-portal].</span></span>
2. <span data-ttu-id="9a8bd-205">Selezionare **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-205">Select **Active Directory**.</span></span>
3. <span data-ttu-id="9a8bd-206">Fare clic sul nome del tenant AAD usato durante il provisioning della soluzione.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-206">Click the name of the AAD tenant you used when you provisioned your solution.</span></span>
4. <span data-ttu-id="9a8bd-207">Fare clic su **Applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-207">Click **Applications**.</span></span>
5. <span data-ttu-id="9a8bd-208">Fare clic sul nome dell'applicazione che coincide con il nome della soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-208">Click the name of the application that matches your preconfigured solution name.</span></span> <span data-ttu-id="9a8bd-209">Se l'applicazione non viene visualizzata nell'elenco, selezionare **Applicazioni di proprietà dell'azienda** nell'elenco a discesa **Mostra** e fare clic sul segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-209">If you don't see your application in the list, select **Applications my company owns** in the **Show** dropdown and click the check mark.</span></span>
6. <span data-ttu-id="9a8bd-210">Nella parte inferiore della pagina fare clic su **Gestisci manifesto** e quindi su **Scarica manifesto**.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-210">At the bottom of the page, click **Manage Manifest** and then **Download Manifest**.</span></span>
7. <span data-ttu-id="9a8bd-211">Questa procedura scarica un file con estensione JSON nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-211">This procedure downloads a .json file to your local machine.</span></span> <span data-ttu-id="9a8bd-212">Aprire il file per modificarlo in un editor di testo di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-212">Open this file for editing in a text editor of your choice.</span></span>
8. <span data-ttu-id="9a8bd-213">Nella terza riga del file con estensione JSON, è possibile trovare:</span><span class="sxs-lookup"><span data-stu-id="9a8bd-213">On the third line of the .json file, you can see:</span></span>

   ```json
   "appRoles" : [],
   ```
   <span data-ttu-id="9a8bd-214">Sostituire questa riga con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="9a8bd-214">Replace this line with the following code:</span></span>

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access to the application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access to device information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. <span data-ttu-id="9a8bd-215">Salvare il file con estensione JSON aggiornato (è possibile sovrascrivere il file esistente).</span><span class="sxs-lookup"><span data-stu-id="9a8bd-215">Save the updated .json file (you can overwrite the existing file).</span></span>
10. <span data-ttu-id="9a8bd-216">Nel portale di Azure classico, nella parte inferiore della pagina selezionare **Gestisci manifesto** e quindi **Carica manifesto** per caricare il file con estensione json salvato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-216">In the Azure classic portal, at the bottom of the page, select **Manage Manifest** then **Upload Manifest** to upload the .json file you saved in the previous step.</span></span>
11. <span data-ttu-id="9a8bd-217">Sono stati aggiunti all'applicazione i ruoli **Admin** e **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-217">You have now added the **Admin** and **ReadOnly** roles to your application.</span></span>
12. <span data-ttu-id="9a8bd-218">Per assegnare uno di questi ruoli a un utente nella directory, vedere [Autorizzazioni per il sito azureiotsuite.com][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="9a8bd-218">To assign one of these roles to a user in your directory, see [Permissions on the azureiotsuite.com site][lnk-permissions].</span></span>

## <a name="feedback"></a><span data-ttu-id="9a8bd-219">Commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="9a8bd-219">Feedback</span></span>

<span data-ttu-id="9a8bd-220">Per altre informazioni relative a una personalizzazione,</span><span class="sxs-lookup"><span data-stu-id="9a8bd-220">Do you have a customization you'd like to see covered in this document?</span></span> <span data-ttu-id="9a8bd-221">Inviare suggerimenti sulla funzionalità a [User Voice](https://feedback.azure.com/forums/321918-azure-iot) oppure lasciare un commento nell'apposita sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="9a8bd-221">Add feature suggestions to [User Voice](https://feedback.azure.com/forums/321918-azure-iot), or comment on this article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9a8bd-222">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9a8bd-222">Next steps</span></span>

<span data-ttu-id="9a8bd-223">Per altre informazioni sulle opzioni per personalizzare le soluzioni preconfigurate, vedere:</span><span class="sxs-lookup"><span data-stu-id="9a8bd-223">To learn more about the options for customizing the preconfigured solutions, see:</span></span>

* <span data-ttu-id="9a8bd-224">[Connettere l'app per la logica alla soluzione preconfigurata per il monitoraggio remoto Azure IoT Suite][lnk-logicapp]</span><span class="sxs-lookup"><span data-stu-id="9a8bd-224">[Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapp]</span></span>
* <span data-ttu-id="9a8bd-225">[Usare la telemetria dinamica con la soluzione preconfigurata per il monitoraggio remoto][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="9a8bd-225">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="9a8bd-226">[Metadati di informazioni sul dispositivo nella soluzione preconfigurata per il monitoraggio remoto][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="9a8bd-226">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo]</span></span>
* <span data-ttu-id="9a8bd-227">[Personalizzare la modalità di visualizzazione dei dati dai server OPC UA da parte della soluzione del factory connesso][lnk-cf-customize]</span><span class="sxs-lookup"><span data-stu-id="9a8bd-227">[Customize how the connected factory solution displays data from your OPC UA servers][lnk-cf-customize]</span></span>

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