---
title: procedura dettagliata sulla soluzione di monitoraggio preconfigurato aaaRemote | Documenti Microsoft
description: Una descrizione di hello Azure IoT preconfigurato soluzione di monitoraggio remoto e la relativa architettura.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57a336bd94938c2b9ee5d3456ea8e45446cf3d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a><span data-ttu-id="de946-103">Procedura dettagliata della soluzione preconfigurata per il monitoraggio remoto</span><span class="sxs-lookup"><span data-stu-id="de946-103">Remote monitoring preconfigured solution walkthrough</span></span>

<span data-ttu-id="de946-104">Hello IoT Suite di monitoraggio remoto [preconfigurato soluzione] [ lnk-preconfigured-solutions] è un'implementazione di un end-to-end monitoraggio soluzione per più macchine virtuali in esecuzione in posizioni remote.</span><span class="sxs-lookup"><span data-stu-id="de946-104">hello IoT Suite remote monitoring [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end monitoring solution for multiple machines running in remote locations.</span></span> <span data-ttu-id="de946-105">soluzione Hello combina servizi Azure chiave tooprovide un'implementazione generica di scenario aziendale hello.</span><span class="sxs-lookup"><span data-stu-id="de946-105">hello solution combines key Azure services tooprovide a generic implementation of hello business scenario.</span></span> <span data-ttu-id="de946-106">È possibile utilizzare la soluzione hello come punto di partenza per la propria implementazione e [personalizzare] [ lnk-customize] è toomeet i requisiti aziendali specifici.</span><span class="sxs-lookup"><span data-stu-id="de946-106">You can use hello solution as a starting point for your own implementation and [customize][lnk-customize] it toomeet your own specific business requirements.</span></span>

<span data-ttu-id="de946-107">Questo articolo vengono illustrati alcuni elementi chiave hello, di hello remoto monitoraggio soluzione tooenable toounderstand il funzionamento.</span><span class="sxs-lookup"><span data-stu-id="de946-107">This article walks you through some of hello key elements of hello remote monitoring solution tooenable you toounderstand how it works.</span></span> <span data-ttu-id="de946-108">Queste informazioni consentono di:</span><span class="sxs-lookup"><span data-stu-id="de946-108">This knowledge helps you to:</span></span>

* <span data-ttu-id="de946-109">Risolvere i problemi nella soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="de946-109">Troubleshoot issues in hello solution.</span></span>
* <span data-ttu-id="de946-110">Pianificare la modalità toocustomize toohello soluzione toomeet esigenze specifiche.</span><span class="sxs-lookup"><span data-stu-id="de946-110">Plan how toocustomize toohello solution toomeet your own specific requirements.</span></span> 
* <span data-ttu-id="de946-111">Progettare la propria soluzione IoT che usa i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="de946-111">Design your own IoT solution that uses Azure services.</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="de946-112">Architettura logica</span><span class="sxs-lookup"><span data-stu-id="de946-112">Logical architecture</span></span>

<span data-ttu-id="de946-113">Hello seguente diagramma illustra i componenti logici hello della soluzione preconfigurata hello:</span><span class="sxs-lookup"><span data-stu-id="de946-113">hello following diagram outlines hello logical components of hello preconfigured solution:</span></span>

![Architettura logica](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a><span data-ttu-id="de946-115">Dispositivi simulati</span><span class="sxs-lookup"><span data-stu-id="de946-115">Simulated devices</span></span>

<span data-ttu-id="de946-116">Nella soluzione hello preconfigurato, dispositivo simulato hello rappresenta un dispositivo di raffreddamento (ad esempio una compilazione condizionatore o unità di gestione delle funzionalità aria).</span><span class="sxs-lookup"><span data-stu-id="de946-116">In hello preconfigured solution, hello simulated device represents a cooling device (such as a building air conditioner or facility air handling unit).</span></span> <span data-ttu-id="de946-117">Quando si distribuisce la soluzione hello preconfigurato, inoltre automaticamente il provisioning di quattro simulati dispositivi che vengono eseguiti in un [processo Web di Azure][lnk-webjobs].</span><span class="sxs-lookup"><span data-stu-id="de946-117">When you deploy hello preconfigured solution, you also automatically provision four simulated devices that run in an [Azure WebJob][lnk-webjobs].</span></span> <span data-ttu-id="de946-118">dispositivi Hello simulato semplificano si tooexplore hello comportamento della soluzione hello senza hello necessità toodeploy eventuali dispositivi fisici.</span><span class="sxs-lookup"><span data-stu-id="de946-118">hello simulated devices make it easy for you tooexplore hello behavior of hello solution without hello need toodeploy any physical devices.</span></span> <span data-ttu-id="de946-119">toodeploy un dispositivo fisico reale, vedere hello [connettersi toohello il dispositivo remoto monitoraggio soluzione preconfigurata] [ lnk-connect-rm] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="de946-119">toodeploy a real physical device, see hello [Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

### <a name="device-to-cloud-messages"></a><span data-ttu-id="de946-120">Messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="de946-120">Device-to-cloud messages</span></span>

<span data-ttu-id="de946-121">Ogni dispositivo simulato può inviare i seguenti tipi di messaggio tooIoT Hub hello:</span><span class="sxs-lookup"><span data-stu-id="de946-121">Each simulated device can send hello following message types tooIoT Hub:</span></span>

| <span data-ttu-id="de946-122">Message</span><span class="sxs-lookup"><span data-stu-id="de946-122">Message</span></span> | <span data-ttu-id="de946-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="de946-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de946-124">Startup</span><span class="sxs-lookup"><span data-stu-id="de946-124">Startup</span></span> |<span data-ttu-id="de946-125">Quando si avvia il dispositivo di hello, invia un **informazioni sul dispositivo** messaggio contenente informazioni su se stesso toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="de946-125">When hello device starts, it sends a **device-info** message containing information about itself toohello back end.</span></span> <span data-ttu-id="de946-126">Questi dati includono l'id dispositivo hello e un elenco di comandi hello e metodi hello supporta dispositivi.</span><span class="sxs-lookup"><span data-stu-id="de946-126">This data includes hello device id and a list of hello commands and methods hello device supports.</span></span> |
| <span data-ttu-id="de946-127">Presenza</span><span class="sxs-lookup"><span data-stu-id="de946-127">Presence</span></span> |<span data-ttu-id="de946-128">Un dispositivo invia periodicamente un **presenza** messaggio tooreport se dispositivo hello può rilevare la presenza hello di un sensore.</span><span class="sxs-lookup"><span data-stu-id="de946-128">A device periodically sends a **presence** message tooreport whether hello device can sense hello presence of a sensor.</span></span> |
| <span data-ttu-id="de946-129">Telemetria</span><span class="sxs-lookup"><span data-stu-id="de946-129">Telemetry</span></span> |<span data-ttu-id="de946-130">Un dispositivo invia periodicamente un **telemetria** messaggio che segnala simulati i valori di temperatura hello e l'umidità non raccolti dal dispositivo hello del simulato sensori.</span><span class="sxs-lookup"><span data-stu-id="de946-130">A device periodically sends a **telemetry** message that reports simulated values for hello temperature and humidity collected from hello device's simulated sensors.</span></span> |

> [!NOTE]
> <span data-ttu-id="de946-131">soluzione Hello archivia l'elenco di hello di comandi supportato dal dispositivo hello in un database DB Cosmos e non in un doppio dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="de946-131">hello solution stores hello list of commands supported by hello device in a Cosmos DB database and not in hello device twin.</span></span>

### <a name="properties-and-device-twins"></a><span data-ttu-id="de946-132">Proprietà e dispositivi gemelli</span><span class="sxs-lookup"><span data-stu-id="de946-132">Properties and device twins</span></span>

<span data-ttu-id="de946-133">Hello simulati i dispositivi le inviano hello seguente dispositivo proprietà toohello [doppi] [ lnk-device-twins] nell'hub IoT hello come *segnalati proprietà*.</span><span class="sxs-lookup"><span data-stu-id="de946-133">hello simulated devices send hello following device properties toohello [twin][lnk-device-twins] in hello IoT hub as *reported properties*.</span></span> <span data-ttu-id="de946-134">dispositivo invia Hello segnalati proprietà all'avvio e risposta tooa **modifica dello stato del dispositivo** metodo o il comando.</span><span class="sxs-lookup"><span data-stu-id="de946-134">hello device sends reported properties at startup and in response tooa **Change Device State** command or method.</span></span>

| <span data-ttu-id="de946-135">Proprietà</span><span class="sxs-lookup"><span data-stu-id="de946-135">Property</span></span> | <span data-ttu-id="de946-136">Scopo</span><span class="sxs-lookup"><span data-stu-id="de946-136">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="de946-137">Config.TelemetryInterval</span><span class="sxs-lookup"><span data-stu-id="de946-137">Config.TelemetryInterval</span></span> | <span data-ttu-id="de946-138">Dispositivo hello frequenza (secondi) invia i dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="de946-138">Frequency (seconds) hello device sends telemetry</span></span> |
| <span data-ttu-id="de946-139">Config.TemperatureMeanValue</span><span class="sxs-lookup"><span data-stu-id="de946-139">Config.TemperatureMeanValue</span></span> | <span data-ttu-id="de946-140">Specifica il valore medio di hello per hello simulato temperatura telemetria</span><span class="sxs-lookup"><span data-stu-id="de946-140">Specifies hello mean value for hello simulated temperature telemetry</span></span> |
| <span data-ttu-id="de946-141">Device.DeviceID</span><span class="sxs-lookup"><span data-stu-id="de946-141">Device.DeviceID</span></span> |<span data-ttu-id="de946-142">ID che viene fornito o assegnato al momento della creazione di un dispositivo nella soluzione hello</span><span class="sxs-lookup"><span data-stu-id="de946-142">Id that is either provided or assigned when a device is created in hello solution</span></span> |
| <span data-ttu-id="de946-143">Device.DeviceState</span><span class="sxs-lookup"><span data-stu-id="de946-143">Device.DeviceState</span></span> | <span data-ttu-id="de946-144">Stato segnalato dal dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="de946-144">State reported by hello device</span></span> |
| <span data-ttu-id="de946-145">Device.CreatedTime</span><span class="sxs-lookup"><span data-stu-id="de946-145">Device.CreatedTime</span></span> |<span data-ttu-id="de946-146">Dispositivo hello ora è stato creato nella soluzione hello</span><span class="sxs-lookup"><span data-stu-id="de946-146">Time hello device was created in hello solution</span></span> |
| <span data-ttu-id="de946-147">Device.StartupTime</span><span class="sxs-lookup"><span data-stu-id="de946-147">Device.StartupTime</span></span> |<span data-ttu-id="de946-148">Dispositivo hello ora è stato avviato</span><span class="sxs-lookup"><span data-stu-id="de946-148">Time hello device was started</span></span> |
| <span data-ttu-id="de946-149">Device.LastDesiredPropertyChange</span><span class="sxs-lookup"><span data-stu-id="de946-149">Device.LastDesiredPropertyChange</span></span> |<span data-ttu-id="de946-150">modificare il numero di versione Hello della proprietà desiderata ultimo hello</span><span class="sxs-lookup"><span data-stu-id="de946-150">hello version number of hello last desired property change</span></span> |
| <span data-ttu-id="de946-151">Device.Location.Latitude</span><span class="sxs-lookup"><span data-stu-id="de946-151">Device.Location.Latitude</span></span> |<span data-ttu-id="de946-152">Posizione di latitudine di hello dispositivo</span><span class="sxs-lookup"><span data-stu-id="de946-152">Latitude location of hello device</span></span> |
| <span data-ttu-id="de946-153">Device.Location.Longitude</span><span class="sxs-lookup"><span data-stu-id="de946-153">Device.Location.Longitude</span></span> |<span data-ttu-id="de946-154">Posizione di longitudine di hello dispositivo</span><span class="sxs-lookup"><span data-stu-id="de946-154">Longitude location of hello device</span></span> |
| <span data-ttu-id="de946-155">System.Manufacturer</span><span class="sxs-lookup"><span data-stu-id="de946-155">System.Manufacturer</span></span> |<span data-ttu-id="de946-156">Produttore del dispositivo</span><span class="sxs-lookup"><span data-stu-id="de946-156">Device manufacturer</span></span> |
| <span data-ttu-id="de946-157">System.ModelNumber</span><span class="sxs-lookup"><span data-stu-id="de946-157">System.ModelNumber</span></span> |<span data-ttu-id="de946-158">Numero di modello di dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="de946-158">Model number of hello device</span></span> |
| <span data-ttu-id="de946-159">System.SerialNumber</span><span class="sxs-lookup"><span data-stu-id="de946-159">System.SerialNumber</span></span> |<span data-ttu-id="de946-160">Numero di serie del dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="de946-160">Serial number of hello device</span></span> |
| <span data-ttu-id="de946-161">System.FirmwareVersion</span><span class="sxs-lookup"><span data-stu-id="de946-161">System.FirmwareVersion</span></span> |<span data-ttu-id="de946-162">Versione corrente del firmware sul dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="de946-162">Current version of firmware on hello device</span></span> |
| <span data-ttu-id="de946-163">System.Platform</span><span class="sxs-lookup"><span data-stu-id="de946-163">System.Platform</span></span> |<span data-ttu-id="de946-164">Architettura della piattaforma del dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="de946-164">Platform architecture of hello device</span></span> |
| <span data-ttu-id="de946-165">System.Processor</span><span class="sxs-lookup"><span data-stu-id="de946-165">System.Processor</span></span> |<span data-ttu-id="de946-166">Dispositivo hello in esecuzione processore</span><span class="sxs-lookup"><span data-stu-id="de946-166">Processor running hello device</span></span> |
| <span data-ttu-id="de946-167">System.InstalledRAM</span><span class="sxs-lookup"><span data-stu-id="de946-167">System.InstalledRAM</span></span> |<span data-ttu-id="de946-168">Quantità di RAM installato sul dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="de946-168">Amount of RAM installed on hello device</span></span> |

<span data-ttu-id="de946-169">simulatore Hello semi queste proprietà in dispositivi simulati con valori di esempio.</span><span class="sxs-lookup"><span data-stu-id="de946-169">hello simulator seeds these properties in simulated devices with sample values.</span></span> <span data-ttu-id="de946-170">Ogni volta che il simulatore hello Inizializza un dispositivo simulato, il dispositivo hello report hello metadati predefiniti tooIoT Hub come proprietà segnalate.</span><span class="sxs-lookup"><span data-stu-id="de946-170">Each time hello simulator initializes a simulated device, hello device reports hello pre-defined metadata tooIoT Hub as reported properties.</span></span> <span data-ttu-id="de946-171">Proprietà restituita può essere aggiornata solo dal dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="de946-171">Reported properties can only be updated by hello device.</span></span> <span data-ttu-id="de946-172">una proprietà segnalata toochange, impostare la proprietà desiderata nel portale di soluzione.</span><span class="sxs-lookup"><span data-stu-id="de946-172">toochange a reported property, you set a desired property in solution portal.</span></span> <span data-ttu-id="de946-173">È responsabilità di hello del dispositivo hello per:</span><span class="sxs-lookup"><span data-stu-id="de946-173">It is hello responsibility of hello device to:</span></span>

1. <span data-ttu-id="de946-174">Dall'hub IoT hello recuperare periodicamente le proprietà desiderate.</span><span class="sxs-lookup"><span data-stu-id="de946-174">Periodically retrieve desired properties from hello IoT hub.</span></span>
2. <span data-ttu-id="de946-175">Aggiornare la configurazione con valore della proprietà hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="de946-175">Update its configuration with hello desired property value.</span></span>
3. <span data-ttu-id="de946-176">Inviare nuovo hub di back-toohello valore hello come una proprietà segnalata.</span><span class="sxs-lookup"><span data-stu-id="de946-176">Send hello new value back toohello hub as a reported property.</span></span>

<span data-ttu-id="de946-177">Dal dashboard di soluzione hello, è possibile utilizzare *le proprietà desiderate* tooset proprietà in un dispositivo utilizzando hello [doppi dispositivo][lnk-device-twins].</span><span class="sxs-lookup"><span data-stu-id="de946-177">From hello solution dashboard, you can use *desired properties* tooset properties on a device by using hello [device twin][lnk-device-twins].</span></span> <span data-ttu-id="de946-178">In genere, un dispositivo legge un valore della proprietà desiderata da hello hub tooupdate che il relativo stato interno e hello report modificare nuovamente come una proprietà segnalata.</span><span class="sxs-lookup"><span data-stu-id="de946-178">Typically, a device reads a desired property value from hello hub tooupdate its internal state and report hello change back as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="de946-179">Hello dispositivo simulato solo codice hello **Desired.Config.TemperatureMeanValue** e **Desired.Config.TelemetryInterval** hello tooupdate proprietà desiderate segnalati proprietà restituita tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="de946-179">hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties sent back tooIoT Hub.</span></span> <span data-ttu-id="de946-180">Nel dispositivo simulato hello, vengono ignorate tutte le altre richieste di modifica della proprietà desiderata.</span><span class="sxs-lookup"><span data-stu-id="de946-180">All other desired property change requests are ignored in hello simulated device.</span></span>

### <a name="methods"></a><span data-ttu-id="de946-181">Metodi</span><span class="sxs-lookup"><span data-stu-id="de946-181">Methods</span></span>

<span data-ttu-id="de946-182">Hello dispositivi simulati in grado di gestire hello dei seguenti metodi ([diretta metodi][lnk-direct-methods]) viene richiamato dal portale di soluzione hello tramite l'hub IoT hello:</span><span class="sxs-lookup"><span data-stu-id="de946-182">hello simulated devices can handle hello following methods ([direct methods][lnk-direct-methods]) invoked from hello solution portal through hello IoT hub:</span></span>

| <span data-ttu-id="de946-183">Metodo</span><span class="sxs-lookup"><span data-stu-id="de946-183">Method</span></span> | <span data-ttu-id="de946-184">Descrizione</span><span class="sxs-lookup"><span data-stu-id="de946-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de946-185">InitiateFirmwareUpdate</span><span class="sxs-lookup"><span data-stu-id="de946-185">InitiateFirmwareUpdate</span></span> |<span data-ttu-id="de946-186">Indica a hello dispositivo tooperform un aggiornamento del firmware</span><span class="sxs-lookup"><span data-stu-id="de946-186">Instructs hello device tooperform a firmware update</span></span> |
| <span data-ttu-id="de946-187">Reboot</span><span class="sxs-lookup"><span data-stu-id="de946-187">Reboot</span></span> |<span data-ttu-id="de946-188">Indica a hello dispositivo tooreboot</span><span class="sxs-lookup"><span data-stu-id="de946-188">Instructs hello device tooreboot</span></span> |
| <span data-ttu-id="de946-189">FactoryReset</span><span class="sxs-lookup"><span data-stu-id="de946-189">FactoryReset</span></span> |<span data-ttu-id="de946-190">Indica di Reimposta una factory di hello dispositivo tooperform</span><span class="sxs-lookup"><span data-stu-id="de946-190">Instructs hello device tooperform a factory reset</span></span> |

<span data-ttu-id="de946-191">Alcuni metodi utilizzano proprietà segnalati tooreport sullo stato di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="de946-191">Some methods use reported properties tooreport on progress.</span></span> <span data-ttu-id="de946-192">Ad esempio, hello **InitiateFirmwareUpdate** metodo Simula aggiornamento hello in esecuzione in modo asincrono sul dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="de946-192">For example, hello **InitiateFirmwareUpdate** method simulates running hello update asynchronously on hello device.</span></span> <span data-ttu-id="de946-193">metodo Hello restituisce immediatamente sul dispositivo hello, mentre l'attività asincrona hello continua toosend nuovamente gli aggiornamenti dello stato toohello soluzione dashboard usando segnalato proprietà.</span><span class="sxs-lookup"><span data-stu-id="de946-193">hello method returns immediately on hello device, while hello asynchronous task continues toosend status updates back toohello solution dashboard using reported properties.</span></span>

### <a name="commands"></a><span data-ttu-id="de946-194">Comandi:</span><span class="sxs-lookup"><span data-stu-id="de946-194">Commands</span></span>

<span data-ttu-id="de946-195">dispositivi Hello simulato è possono gestire hello comandi (cloud a dispositivo messaggi) inviati dal portale di soluzione hello tramite l'hub IoT hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="de946-195">hello simulated devices can handle hello following commands (cloud-to-device messages) sent from hello solution portal through hello IoT hub:</span></span>

| <span data-ttu-id="de946-196">Comando</span><span class="sxs-lookup"><span data-stu-id="de946-196">Command</span></span> | <span data-ttu-id="de946-197">Descrizione</span><span class="sxs-lookup"><span data-stu-id="de946-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de946-198">PingDevice</span><span class="sxs-lookup"><span data-stu-id="de946-198">PingDevice</span></span> |<span data-ttu-id="de946-199">Invia un *ping* toohello toocheck di dispositivo è attivo</span><span class="sxs-lookup"><span data-stu-id="de946-199">Sends a *ping* toohello device toocheck it is alive</span></span> |
| <span data-ttu-id="de946-200">StartTelemetry</span><span class="sxs-lookup"><span data-stu-id="de946-200">StartTelemetry</span></span> |<span data-ttu-id="de946-201">Dispositivo hello viene avviato l'invio di dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="de946-201">Starts hello device sending telemetry</span></span> |
| <span data-ttu-id="de946-202">StopTelemetry</span><span class="sxs-lookup"><span data-stu-id="de946-202">StopTelemetry</span></span> |<span data-ttu-id="de946-203">Interrompe l'invio di dati di telemetria di hello</span><span class="sxs-lookup"><span data-stu-id="de946-203">Stops hello device from sending telemetry</span></span> |
| <span data-ttu-id="de946-204">ChangeSetPointTemp</span><span class="sxs-lookup"><span data-stu-id="de946-204">ChangeSetPointTemp</span></span> |<span data-ttu-id="de946-205">Modifica il valore dell'imposta punto hello intorno al quale hello vengono generati dati casuali</span><span class="sxs-lookup"><span data-stu-id="de946-205">Changes hello set point value around which hello random data is generated</span></span> |
| <span data-ttu-id="de946-206">DiagnosticTelemetry</span><span class="sxs-lookup"><span data-stu-id="de946-206">DiagnosticTelemetry</span></span> |<span data-ttu-id="de946-207">I trigger hello toosend simulatore di dispositivo un valore di dati di telemetria aggiuntive (externalTemp)</span><span class="sxs-lookup"><span data-stu-id="de946-207">Triggers hello device simulator toosend an additional telemetry value (externalTemp)</span></span> |
| <span data-ttu-id="de946-208">ChangeDeviceState</span><span class="sxs-lookup"><span data-stu-id="de946-208">ChangeDeviceState</span></span> |<span data-ttu-id="de946-209">Modifica una proprietà di stato esteso per il dispositivo hello e Invia messaggio di informazioni sul dispositivo di hello dal dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="de946-209">Changes an extended state property for hello device and sends hello device info message from hello device</span></span> |

> [!NOTE]
> <span data-ttu-id="de946-210">Per un confronto tra questi comandi (messaggi da cloud a dispositivo) e i metodi (metodi diretti), vedere [Indicazioni sulle comunicazioni da cloud a dispositivo][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="de946-210">For a comparison of these commands (cloud-to-device messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>

## <a name="iot-hub"></a><span data-ttu-id="de946-211">Hub IoT</span><span class="sxs-lookup"><span data-stu-id="de946-211">IoT Hub</span></span>

<span data-ttu-id="de946-212">Hello [hub IoT] [ lnk-iothub] inserisce i dati inviati da dispositivi hello in cloud hello e rende disponibili toohello i processi di Azure flusso Analitica (ASA).</span><span class="sxs-lookup"><span data-stu-id="de946-212">hello [IoT hub][lnk-iothub] ingests data sent from hello devices into hello cloud and makes it available toohello Azure Stream Analytics (ASA) jobs.</span></span> <span data-ttu-id="de946-213">Ogni processo ASA flusso Usa IoT Hub consumer gruppo tooread hello flusso separato di messaggi dai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="de946-213">Each stream ASA job uses a separate IoT Hub consumer group tooread hello stream of messages from your devices.</span></span>

<span data-ttu-id="de946-214">Hello anche hub IoT nella soluzione hello:</span><span class="sxs-lookup"><span data-stu-id="de946-214">hello IoT hub in hello solution also:</span></span>

- <span data-ttu-id="de946-215">Gestisce un registro di sistema di identità che archivia gli ID hello e chiavi di autenticazione di tutti i dispositivi di hello tooconnect toohello portale è consentiti.</span><span class="sxs-lookup"><span data-stu-id="de946-215">Maintains an identity registry that stores hello ids and authentication keys of all hello devices permitted tooconnect toohello portal.</span></span> <span data-ttu-id="de946-216">È possibile abilitare e disabilitare i dispositivi tramite il Registro di identità hello.</span><span class="sxs-lookup"><span data-stu-id="de946-216">You can enable and disable devices through hello identity registry.</span></span>
- <span data-ttu-id="de946-217">Invia comandi tooyour dispositivi per conto di portale soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="de946-217">Sends commands tooyour devices on behalf of hello solution portal.</span></span>
- <span data-ttu-id="de946-218">Richiama i metodi nei dispositivi per conto di portale soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="de946-218">Invokes methods on your devices on behalf of hello solution portal.</span></span>
- <span data-ttu-id="de946-219">Gestisce i dispositivi gemelli per tutti i dispositivi registrati.</span><span class="sxs-lookup"><span data-stu-id="de946-219">Maintains device twins for all registered devices.</span></span> <span data-ttu-id="de946-220">Un doppio di un dispositivo archivia i valori delle proprietà hello segnalati da un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="de946-220">A device twin stores hello property values reported by a device.</span></span> <span data-ttu-id="de946-221">Un doppio di un dispositivo archivia anche le proprietà desiderate impostate nel portale di soluzione hello per hello dispositivo tooretrieve quando si connette quindi.</span><span class="sxs-lookup"><span data-stu-id="de946-221">A device twin also stores desired properties, set in hello solution portal, for hello device tooretrieve when it next connects.</span></span>
- <span data-ttu-id="de946-222">Le pianificazioni dei processi di proprietà tooset per più dispositivi o chiamare metodi su più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="de946-222">Schedules jobs tooset properties for multiple devices or invoke methods on multiple devices.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="de946-223">Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="de946-223">Azure Stream Analytics</span></span>

<span data-ttu-id="de946-224">Nella soluzione, di monitoraggio remoto hello [Azure flusso Analitica] [ lnk-asa] (ASA) invia i messaggi di dispositivo ricevuti dai componenti hello IoT hub tooother back-end per l'elaborazione o di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="de946-224">In hello remote monitoring solution, [Azure Stream Analytics][lnk-asa] (ASA) dispatches device messages received by hello IoT hub tooother back-end components for processing or storage.</span></span> <span data-ttu-id="de946-225">Diversi processi ASA eseguono operazioni specifiche in base al contenuto dei messaggi hello hello.</span><span class="sxs-lookup"><span data-stu-id="de946-225">Different ASA jobs perform specific functions based on hello content of hello messages.</span></span>

<span data-ttu-id="de946-226">**Processo 1: Informazioni sul dispositivo** Filtra i messaggi informativi di dispositivo dal flusso di messaggi hello in arrivo e li invia a endpoint di Hub eventi tooan.</span><span class="sxs-lookup"><span data-stu-id="de946-226">**Job 1: Device Info** filters device information messages from hello incoming message stream and sends them tooan Event Hub endpoint.</span></span> <span data-ttu-id="de946-227">Un dispositivo invia i messaggi informativi di dispositivo all'avvio e di risposta tooa **SendDeviceInfo** comando.</span><span class="sxs-lookup"><span data-stu-id="de946-227">A device sends device information messages at startup and in response tooa **SendDeviceInfo** command.</span></span> <span data-ttu-id="de946-228">Questo processo Usa hello seguente query definizione tooidentify **informazioni sul dispositivo** messaggi:</span><span class="sxs-lookup"><span data-stu-id="de946-228">This job uses hello following query definition tooidentify **device-info** messages:</span></span>

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

<span data-ttu-id="de946-229">Consente di inviare il tooan output Hub eventi per un'ulteriore elaborazione.</span><span class="sxs-lookup"><span data-stu-id="de946-229">This job sends its output tooan Event Hub for further processing.</span></span>

<span data-ttu-id="de946-230">**Processo 2: Regole** restituisce valori di telemetria in entrata relativi a temperatura e umidità rispetto alle soglie per dispositivo.</span><span class="sxs-lookup"><span data-stu-id="de946-230">**Job 2: Rules** evaluates incoming temperature and humidity telemetry values against per-device thresholds.</span></span> <span data-ttu-id="de946-231">I valori di soglia vengono impostati nell'editor delle regole hello disponibile nel portale di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="de946-231">Threshold values are set in hello rules editor available in hello solution portal.</span></span> <span data-ttu-id="de946-232">Ogni coppia dispositivo/valore viene archiviata in base al timestamp in un BLOB che viene letto in Analisi di flusso come **dati di riferimento**.</span><span class="sxs-lookup"><span data-stu-id="de946-232">Each device/value pair is stored by timestamp in a blob which Stream Analytics reads in as **Reference Data**.</span></span> <span data-ttu-id="de946-233">qualsiasi valore non vuoto hello di soglia impostata per il dispositivo hello viene confrontato con il processo di Hello.</span><span class="sxs-lookup"><span data-stu-id="de946-233">hello job compares any non-empty value against hello set threshold for hello device.</span></span> <span data-ttu-id="de946-234">Se il valore supera hello ' >' condizione, l'output del processo di hello un **allarme** evento che indica che tale soglia hello viene superato e fornisce dispositivo hello, valore e i valori di timestamp.</span><span class="sxs-lookup"><span data-stu-id="de946-234">If it exceeds hello '>' condition, hello job outputs an **alarm** event that indicates that hello threshold is exceeded and provides hello device, value, and timestamp values.</span></span> <span data-ttu-id="de946-235">Questo processo Usa hello seguente query definizione tooidentify telemetria messaggi devono attivare un allarme:</span><span class="sxs-lookup"><span data-stu-id="de946-235">This job uses hello following query definition tooidentify telemetry messages that should trigger an alarm:</span></span>

```
WITH AlarmsData AS 
(
SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Temperature' as ReadingType,
     Stream.Temperature as Reading,
     Ref.Temperature as Threshold,
     Ref.TemperatureRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature

UNION ALL

SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Humidity' as ReadingType,
     Stream.Humidity as Reading,
     Ref.Humidity as Threshold,
     Ref.HumidityRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
)

SELECT *
INTO DeviceRulesMonitoring
FROM AlarmsData

SELECT *
INTO DeviceRulesHub
FROM AlarmsData
```

<span data-ttu-id="de946-236">Hello processo invia relativo tooan output Hub eventi per un'ulteriore elaborazione e lo salva i dettagli di ogni archiviazione tooblob avviso da dove portale soluzione hello possa leggere informazioni sugli avvisi di hello.</span><span class="sxs-lookup"><span data-stu-id="de946-236">hello job sends its output tooan Event Hub for further processing and saves details of each alert tooblob storage from where hello solution portal can read hello alert information.</span></span>

<span data-ttu-id="de946-237">**Processo 3: Telemetria** opera su hello flusso in ingresso dispositivo telemetria in due modi.</span><span class="sxs-lookup"><span data-stu-id="de946-237">**Job 3: Telemetry** operates on hello incoming device telemetry stream in two ways.</span></span> <span data-ttu-id="de946-238">Hello invia prima tutti i messaggi di dati di telemetria dall'archiviazione blob di toopersistent hello dispositivi per l'archiviazione a lungo termine.</span><span class="sxs-lookup"><span data-stu-id="de946-238">hello first sends all telemetry messages from hello devices toopersistent blob storage for long-term storage.</span></span> <span data-ttu-id="de946-239">Hello secondo calcola umidità medio, minimo e massimo valori su una finestra temporale scorrevole di cinque minuti e invia l'archiviazione dei dati tooblob.</span><span class="sxs-lookup"><span data-stu-id="de946-239">hello second computes average, minimum, and maximum humidity values over a five-minute sliding window and sends this data tooblob storage.</span></span> <span data-ttu-id="de946-240">portale di soluzione Hello legge i dati di telemetria hello da grafici di hello toopopulate archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="de946-240">hello solution portal reads hello telemetry data from blob storage toopopulate hello charts.</span></span> <span data-ttu-id="de946-241">Questo processo Usa hello dopo la definizione della query:</span><span class="sxs-lookup"><span data-stu-id="de946-241">This job uses hello following query definition:</span></span>

```
WITH 
    [StreamData]
AS (
    SELECT
        *
    FROM [IoTHubStream]
    WHERE
        [ObjectType] IS NULL -- Filter out device info and command responses
) 

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    Temperature,
    Humidity,
    ExternalTemperature,
    EventProcessedUtcTime,
    PartitionId,
    EventEnqueuedUtcTime,
    * 
INTO
    [Telemetry]
FROM
    [StreamData]

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    AVG (Humidity) AS [AverageHumidity],
    MIN(Humidity) AS [MinimumHumidity],
    MAX(Humidity) AS [MaxHumidity],
    5.0 AS TimeframeMinutes 
INTO
    [TelemetrySummary]
FROM [StreamData]
WHERE
    [Humidity] IS NOT NULL
GROUP BY
    IoTHub.ConnectionDeviceId,
    SlidingWindow (mi, 5)
```

## <a name="event-hubs"></a><span data-ttu-id="de946-242">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="de946-242">Event Hubs</span></span>

<span data-ttu-id="de946-243">Hello **informazioni sul dispositivo** e **regole** processi ASA output i relativi dati tooEvent hub tooreliably rollforward in toohello **processore di eventi** in esecuzione in hello processo Web.</span><span class="sxs-lookup"><span data-stu-id="de946-243">hello **device info** and **rules** ASA jobs output their data tooEvent Hubs tooreliably forward on toohello **Event Processor** running in hello WebJob.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="de946-244">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="de946-244">Azure storage</span></span>

<span data-ttu-id="de946-245">soluzione Hello utilizza tutti i dati di telemetria non elaborati e riepilogati hello dai dispositivi hello toopersist di archiviazione blob di Azure nella soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="de946-245">hello solution uses Azure blob storage toopersist all hello raw and summarized telemetry data from hello devices in hello solution.</span></span> <span data-ttu-id="de946-246">portale Hello legge i dati di telemetria hello da grafici di hello toopopulate archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="de946-246">hello portal reads hello telemetry data from blob storage toopopulate hello charts.</span></span> <span data-ttu-id="de946-247">avvisi toodisplay, portale soluzione hello legge dati hello dall'archiviazione blob che registra hello valori superati telemetria configurati i valori di soglia.</span><span class="sxs-lookup"><span data-stu-id="de946-247">toodisplay alerts, hello solution portal reads hello data from blob storage that records when telemetry values exceeded hello configured threshold values.</span></span> <span data-ttu-id="de946-248">soluzione Hello utilizza valori soglia blob archiviazione toorecord hello che è impostato nel portale di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="de946-248">hello solution also uses blob storage toorecord hello threshold values you set in hello solution portal.</span></span>

## <a name="webjobs"></a><span data-ttu-id="de946-249">WebJobs</span><span class="sxs-lookup"><span data-stu-id="de946-249">WebJobs</span></span>

<span data-ttu-id="de946-250">Inoltre simulatori di dispositivo toohosting hello, hello processi Web nella soluzione hello anche hello host **processore di eventi** in esecuzione in un processo Web di Azure che gestisce le risposte di comando.</span><span class="sxs-lookup"><span data-stu-id="de946-250">In addition toohosting hello device simulators, hello WebJobs in hello solution also host hello **Event Processor** running in an Azure WebJob that handles command responses.</span></span> <span data-ttu-id="de946-251">Usa comando risposta messaggi tooupdate hello comando Cronologia dispositivo (archiviata nel database DB Cosmos hello).</span><span class="sxs-lookup"><span data-stu-id="de946-251">It uses command response messages tooupdate hello device command history (stored in hello Cosmos DB database).</span></span>

## <a name="cosmos-db"></a><span data-ttu-id="de946-252">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="de946-252">Cosmos DB</span></span>

<span data-ttu-id="de946-253">soluzione di Hello utilizza un DB Cosmos database toostore informazioni sulle hello dispositivi connessi toohello soluzione.</span><span class="sxs-lookup"><span data-stu-id="de946-253">hello solution uses a Cosmos DB database toostore information about hello devices connected toohello solution.</span></span> <span data-ttu-id="de946-254">Queste informazioni includono cronologia hello di comandi inviati toodevices dal portale di soluzione hello e i metodi richiamati dal portale di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="de946-254">This information includes hello history of commands sent toodevices from hello solution portal and of methods invoked from hello solution portal.</span></span>

## <a name="solution-portal"></a><span data-ttu-id="de946-255">Portale della soluzione</span><span class="sxs-lookup"><span data-stu-id="de946-255">Solution portal</span></span>

<span data-ttu-id="de946-256">portale di soluzione hello è un'app web distribuita come parte della soluzione hello preconfigurato.</span><span class="sxs-lookup"><span data-stu-id="de946-256">hello solution portal is a web app deployed as part of hello preconfigured solution.</span></span> <span data-ttu-id="de946-257">le pagine di chiave Hello nel portale di soluzione hello sono dashboard hello e l'elenco dei dispositivi hello.</span><span class="sxs-lookup"><span data-stu-id="de946-257">hello key pages in hello solution portal are hello dashboard and hello device list.</span></span>

### <a name="dashboard"></a><span data-ttu-id="de946-258">Dashboard</span><span class="sxs-lookup"><span data-stu-id="de946-258">Dashboard</span></span>

<span data-ttu-id="de946-259">Questa pagina nell'app web hello utilizza controlli javascript Power BI (vedere [repository PowerBI-visuals](https://www.github.com/Microsoft/PowerBI-visuals)) toovisualize i dati di telemetria dai dispositivi hello hello.</span><span class="sxs-lookup"><span data-stu-id="de946-259">This page in hello web app uses PowerBI javascript controls (See [PowerBI-visuals repo](https://www.github.com/Microsoft/PowerBI-visuals)) toovisualize hello telemetry data from hello devices.</span></span> <span data-ttu-id="de946-260">soluzione di Hello utilizza hello ASA telemetria processo toowrite hello telemetria tooblob archiviazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="de946-260">hello solution uses hello ASA telemetry job toowrite hello telemetry data tooblob storage.</span></span>

### <a name="device-list"></a><span data-ttu-id="de946-261">Elenco dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="de946-261">Device list</span></span>

<span data-ttu-id="de946-262">In questa pagina nel portale di soluzione hello è possibile:</span><span class="sxs-lookup"><span data-stu-id="de946-262">From this page in hello solution portal you can:</span></span>

* <span data-ttu-id="de946-263">Effettuare il provisioning di un nuovo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="de946-263">Provision a new device.</span></span> <span data-ttu-id="de946-264">Questa azione imposta l'id univoco del dispositivo hello e genera la chiave di autenticazione hello.</span><span class="sxs-lookup"><span data-stu-id="de946-264">This action sets hello unique device id and generates hello authentication key.</span></span> <span data-ttu-id="de946-265">Scrive informazioni hello di tooboth dispositivo hello del Registro di sistema identità IoT Hub e il database di DB Cosmos hello specifici della soluzione.</span><span class="sxs-lookup"><span data-stu-id="de946-265">It writes information about hello device tooboth hello IoT Hub identity registry and hello solution-specific Cosmos DB database.</span></span>
* <span data-ttu-id="de946-266">Gestire le proprietà dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="de946-266">Manage device properties.</span></span> <span data-ttu-id="de946-267">Questa azione include la visualizzazione delle proprietà esistenti e l'aggiornamento con nuove proprietà.</span><span class="sxs-lookup"><span data-stu-id="de946-267">This action includes viewing existing properties and updating with new properties.</span></span>
* <span data-ttu-id="de946-268">Invio dispositivo tooa comandi.</span><span class="sxs-lookup"><span data-stu-id="de946-268">Send commands tooa device.</span></span>
* <span data-ttu-id="de946-269">Consente di visualizzare la cronologia dei comandi hello per un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="de946-269">View hello command history for a device.</span></span>
* <span data-ttu-id="de946-270">Abilitare e disabilitare i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="de946-270">Enable and disable devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de946-271">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="de946-271">Next steps</span></span>

<span data-ttu-id="de946-272">Hello post di blog di TechNet seguenti forniscono ulteriori dettagli su hello soluzione preconfigurata di monitoraggio remoto:</span><span class="sxs-lookup"><span data-stu-id="de946-272">hello following TechNet blog posts provide more detail about hello remote monitoring preconfigured solution:</span></span>

* [<span data-ttu-id="de946-273">Monitoraggio remoto di IoT Suite - Under hello quinte-</span><span class="sxs-lookup"><span data-stu-id="de946-273">IoT Suite - Under hello Hood - Remote Monitoring</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [<span data-ttu-id="de946-274">Aggiunta di dispositivi veri e simulati per il monitoraggio remoto in IoT Suite</span><span class="sxs-lookup"><span data-stu-id="de946-274">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

<span data-ttu-id="de946-275">È possibile continuare introduzione IoT Suite leggendo hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="de946-275">You can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="de946-276">[Connettere la soluzione preconfigurata di monitoraggio remoto toohello di dispositivo][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="de946-276">[Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="de946-277">[Autorizzazioni nel sito azureiotsuite.com hello][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="de946-277">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-iothub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-webjobs]: https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twins]:  ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
