---
title: Procedura dettagliata della soluzione preconfigurata per il monitoraggio remoto| Microsoft Docs
description: Descrizione della soluzione preconfigurata per il monitoraggio remoto di Azure IoT e relativa architettura.
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
ms.openlocfilehash: b28105f300723b542fa6d1aebc569439d5c73dc4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a><span data-ttu-id="255c2-103">Procedura dettagliata della soluzione preconfigurata per il monitoraggio remoto</span><span class="sxs-lookup"><span data-stu-id="255c2-103">Remote monitoring preconfigured solution walkthrough</span></span>

<span data-ttu-id="255c2-104">La [soluzione preconfigurata][lnk-preconfigured-solutions] per il monitoraggio remoto IoT Suite è un'implementazione di una soluzione di monitoraggio end-to-end per più computer in località remote.</span><span class="sxs-lookup"><span data-stu-id="255c2-104">The IoT Suite remote monitoring [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end monitoring solution for multiple machines running in remote locations.</span></span> <span data-ttu-id="255c2-105">La soluzione combina i servizi chiave di Azure per offrire un'implementazione generica dello scenario aziendale.</span><span class="sxs-lookup"><span data-stu-id="255c2-105">The solution combines key Azure services to provide a generic implementation of the business scenario.</span></span> <span data-ttu-id="255c2-106">È possibile usare la soluzione come punto di partenza per l'implementazione e [personalizzarla][lnk-customize] in base ai requisiti aziendali specifici.</span><span class="sxs-lookup"><span data-stu-id="255c2-106">You can use the solution as a starting point for your own implementation and [customize][lnk-customize] it to meet your own specific business requirements.</span></span>

<span data-ttu-id="255c2-107">Questo articolo illustra alcuni degli elementi principali della soluzione di monitoraggio remoto per comprenderne il funzionamento.</span><span class="sxs-lookup"><span data-stu-id="255c2-107">This article walks you through some of the key elements of the remote monitoring solution to enable you to understand how it works.</span></span> <span data-ttu-id="255c2-108">Queste informazioni consentono di:</span><span class="sxs-lookup"><span data-stu-id="255c2-108">This knowledge helps you to:</span></span>

* <span data-ttu-id="255c2-109">Risolvere i problemi nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="255c2-109">Troubleshoot issues in the solution.</span></span>
* <span data-ttu-id="255c2-110">Pianificare come personalizzare la soluzione per soddisfare requisiti specifici.</span><span class="sxs-lookup"><span data-stu-id="255c2-110">Plan how to customize to the solution to meet your own specific requirements.</span></span> 
* <span data-ttu-id="255c2-111">Progettare la propria soluzione IoT che usa i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="255c2-111">Design your own IoT solution that uses Azure services.</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="255c2-112">Architettura logica</span><span class="sxs-lookup"><span data-stu-id="255c2-112">Logical architecture</span></span>

<span data-ttu-id="255c2-113">Il diagramma seguente illustra i componenti logici della soluzione preconfigurata:</span><span class="sxs-lookup"><span data-stu-id="255c2-113">The following diagram outlines the logical components of the preconfigured solution:</span></span>

![Architettura logica](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a><span data-ttu-id="255c2-115">Dispositivi simulati</span><span class="sxs-lookup"><span data-stu-id="255c2-115">Simulated devices</span></span>

<span data-ttu-id="255c2-116">Nella soluzione preconfigurata il dispositivo simulato rappresenta un dispositivo di raffreddamento (ad esempio, un condizionatore d'aria di un edificio o un'unita di trattamento aria di una struttura).</span><span class="sxs-lookup"><span data-stu-id="255c2-116">In the preconfigured solution, the simulated device represents a cooling device (such as a building air conditioner or facility air handling unit).</span></span> <span data-ttu-id="255c2-117">Quando si distribuisce la soluzione preconfigurata, viene effettuato automaticamente anche il provisioning di quattro dispositivi simulati eseguiti in un [processo Web di Azure][lnk-webjobs].</span><span class="sxs-lookup"><span data-stu-id="255c2-117">When you deploy the preconfigured solution, you also automatically provision four simulated devices that run in an [Azure WebJob][lnk-webjobs].</span></span> <span data-ttu-id="255c2-118">I dispositivi simulati semplificano l'esplorazione del comportamento della soluzione senza la necessità di distribuire dispositivi fisici.</span><span class="sxs-lookup"><span data-stu-id="255c2-118">The simulated devices make it easy for you to explore the behavior of the solution without the need to deploy any physical devices.</span></span> <span data-ttu-id="255c2-119">Per distribuire un dispositivo fisico reale, vedere l'esercitazione [Connettere il dispositivo alla soluzione preconfigurata per il monitoraggio remoto][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="255c2-119">To deploy a real physical device, see the [Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

### <a name="device-to-cloud-messages"></a><span data-ttu-id="255c2-120">Messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="255c2-120">Device-to-cloud messages</span></span>

<span data-ttu-id="255c2-121">Ogni dispositivo simulato può inviare i messaggi seguenti all'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="255c2-121">Each simulated device can send the following message types to IoT Hub:</span></span>

| <span data-ttu-id="255c2-122">Message</span><span class="sxs-lookup"><span data-stu-id="255c2-122">Message</span></span> | <span data-ttu-id="255c2-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="255c2-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="255c2-124">Startup</span><span class="sxs-lookup"><span data-stu-id="255c2-124">Startup</span></span> |<span data-ttu-id="255c2-125">Quando il dispositivo viene avviato, invia al back-end un messaggio di **informazioni sul dispositivo** contenente informazioni su se stesso.</span><span class="sxs-lookup"><span data-stu-id="255c2-125">When the device starts, it sends a **device-info** message containing information about itself to the back end.</span></span> <span data-ttu-id="255c2-126">I dati includono l'ID dispositivo e un elenco dei comandi e dei metodi supportati dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-126">This data includes the device id and a list of the commands and methods the device supports.</span></span> |
| <span data-ttu-id="255c2-127">Presenza</span><span class="sxs-lookup"><span data-stu-id="255c2-127">Presence</span></span> |<span data-ttu-id="255c2-128">Un dispositivo invia periodicamente un messaggio di **presenza** per segnalare se il dispositivo può rilevare la presenza di un sensore.</span><span class="sxs-lookup"><span data-stu-id="255c2-128">A device periodically sends a **presence** message to report whether the device can sense the presence of a sensor.</span></span> |
| <span data-ttu-id="255c2-129">Telemetria</span><span class="sxs-lookup"><span data-stu-id="255c2-129">Telemetry</span></span> |<span data-ttu-id="255c2-130">Un dispositivo invia periodicamente un messaggio di **telemetria** che segnala i valori simulati per la temperatura e l'umidità raccolti dai sensori simulati del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-130">A device periodically sends a **telemetry** message that reports simulated values for the temperature and humidity collected from the device's simulated sensors.</span></span> |

> [!NOTE]
> <span data-ttu-id="255c2-131">La soluzione memorizza l'elenco dei comandi supportati dal dispositivo in un database Cosmos DB e non in un dispositivo gemello.</span><span class="sxs-lookup"><span data-stu-id="255c2-131">The solution stores the list of commands supported by the device in a Cosmos DB database and not in the device twin.</span></span>

### <a name="properties-and-device-twins"></a><span data-ttu-id="255c2-132">Proprietà e dispositivi gemelli</span><span class="sxs-lookup"><span data-stu-id="255c2-132">Properties and device twins</span></span>

<span data-ttu-id="255c2-133">Le proprietà del dispositivo riportate di seguito vengono inviate dai dispositivi simulati ai [dispositivi gemelli][lnk-device-twins] nell'hub IoT come *proprietà segnalate*.</span><span class="sxs-lookup"><span data-stu-id="255c2-133">The simulated devices send the following device properties to the [twin][lnk-device-twins] in the IoT hub as *reported properties*.</span></span> <span data-ttu-id="255c2-134">Il dispositivo invia le proprietà segnalate all'avvio e in risposta a un metodo o un comando di **modifica dello stato del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="255c2-134">The device sends reported properties at startup and in response to a **Change Device State** command or method.</span></span>

| <span data-ttu-id="255c2-135">Proprietà</span><span class="sxs-lookup"><span data-stu-id="255c2-135">Property</span></span> | <span data-ttu-id="255c2-136">Scopo</span><span class="sxs-lookup"><span data-stu-id="255c2-136">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="255c2-137">Config.TelemetryInterval</span><span class="sxs-lookup"><span data-stu-id="255c2-137">Config.TelemetryInterval</span></span> | <span data-ttu-id="255c2-138">Frequenza (in secondi) di invio dei dati di telemetria dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-138">Frequency (seconds) the device sends telemetry</span></span> |
| <span data-ttu-id="255c2-139">Config.TemperatureMeanValue</span><span class="sxs-lookup"><span data-stu-id="255c2-139">Config.TemperatureMeanValue</span></span> | <span data-ttu-id="255c2-140">Specifica il valore medio per i dati di telemetria della temperatura simulata.</span><span class="sxs-lookup"><span data-stu-id="255c2-140">Specifies the mean value for the simulated temperature telemetry</span></span> |
| <span data-ttu-id="255c2-141">Device.DeviceID</span><span class="sxs-lookup"><span data-stu-id="255c2-141">Device.DeviceID</span></span> |<span data-ttu-id="255c2-142">ID fornito o assegnato al momento della creazione di un dispositivo nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="255c2-142">Id that is either provided or assigned when a device is created in the solution</span></span> |
| <span data-ttu-id="255c2-143">Device.DeviceState</span><span class="sxs-lookup"><span data-stu-id="255c2-143">Device.DeviceState</span></span> | <span data-ttu-id="255c2-144">Stato segnalato dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-144">State reported by the device</span></span> |
| <span data-ttu-id="255c2-145">Device.CreatedTime</span><span class="sxs-lookup"><span data-stu-id="255c2-145">Device.CreatedTime</span></span> |<span data-ttu-id="255c2-146">Data e ora in cui il dispositivo è stato creato nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="255c2-146">Time the device was created in the solution</span></span> |
| <span data-ttu-id="255c2-147">Device.StartupTime</span><span class="sxs-lookup"><span data-stu-id="255c2-147">Device.StartupTime</span></span> |<span data-ttu-id="255c2-148">Ora in cui il dispositivo è stato avviato.</span><span class="sxs-lookup"><span data-stu-id="255c2-148">Time the device was started</span></span> |
| <span data-ttu-id="255c2-149">Device.LastDesiredPropertyChange</span><span class="sxs-lookup"><span data-stu-id="255c2-149">Device.LastDesiredPropertyChange</span></span> |<span data-ttu-id="255c2-150">Numero di versione dell'ultima modifica della proprietà desiderata.</span><span class="sxs-lookup"><span data-stu-id="255c2-150">The version number of the last desired property change</span></span> |
| <span data-ttu-id="255c2-151">Device.Location.Latitude</span><span class="sxs-lookup"><span data-stu-id="255c2-151">Device.Location.Latitude</span></span> |<span data-ttu-id="255c2-152">Posizione di latitudine del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-152">Latitude location of the device</span></span> |
| <span data-ttu-id="255c2-153">Device.Location.Longitude</span><span class="sxs-lookup"><span data-stu-id="255c2-153">Device.Location.Longitude</span></span> |<span data-ttu-id="255c2-154">Posizione di longitudine del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-154">Longitude location of the device</span></span> |
| <span data-ttu-id="255c2-155">System.Manufacturer</span><span class="sxs-lookup"><span data-stu-id="255c2-155">System.Manufacturer</span></span> |<span data-ttu-id="255c2-156">Produttore del dispositivo</span><span class="sxs-lookup"><span data-stu-id="255c2-156">Device manufacturer</span></span> |
| <span data-ttu-id="255c2-157">System.ModelNumber</span><span class="sxs-lookup"><span data-stu-id="255c2-157">System.ModelNumber</span></span> |<span data-ttu-id="255c2-158">Numero di modello del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-158">Model number of the device</span></span> |
| <span data-ttu-id="255c2-159">System.SerialNumber</span><span class="sxs-lookup"><span data-stu-id="255c2-159">System.SerialNumber</span></span> |<span data-ttu-id="255c2-160">Numero di serie del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-160">Serial number of the device</span></span> |
| <span data-ttu-id="255c2-161">System.FirmwareVersion</span><span class="sxs-lookup"><span data-stu-id="255c2-161">System.FirmwareVersion</span></span> |<span data-ttu-id="255c2-162">Versione corrente del firmware del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-162">Current version of firmware on the device</span></span> |
| <span data-ttu-id="255c2-163">System.Platform</span><span class="sxs-lookup"><span data-stu-id="255c2-163">System.Platform</span></span> |<span data-ttu-id="255c2-164">Architettura della piattaforma del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-164">Platform architecture of the device</span></span> |
| <span data-ttu-id="255c2-165">System.Processor</span><span class="sxs-lookup"><span data-stu-id="255c2-165">System.Processor</span></span> |<span data-ttu-id="255c2-166">Processore in esecuzione nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-166">Processor running the device</span></span> |
| <span data-ttu-id="255c2-167">System.InstalledRAM</span><span class="sxs-lookup"><span data-stu-id="255c2-167">System.InstalledRAM</span></span> |<span data-ttu-id="255c2-168">Quantità di RAM installata sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-168">Amount of RAM installed on the device</span></span> |

<span data-ttu-id="255c2-169">Il simulatore effettua il seeding di queste proprietà nei dispositivi simulati con valori di esempio.</span><span class="sxs-lookup"><span data-stu-id="255c2-169">The simulator seeds these properties in simulated devices with sample values.</span></span> <span data-ttu-id="255c2-170">Ogni volta che il simulatore inizializza un dispositivo simulato, quest'ultimo segnala i metadati predefiniti nell'hub IoT come proprietà segnale.</span><span class="sxs-lookup"><span data-stu-id="255c2-170">Each time the simulator initializes a simulated device, the device reports the pre-defined metadata to IoT Hub as reported properties.</span></span> <span data-ttu-id="255c2-171">Le proprietà segnalate possono essere aggiornate solo dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-171">Reported properties can only be updated by the device.</span></span> <span data-ttu-id="255c2-172">Per modificare una proprietà segnalata, impostare una proprietà desiderata nel portale della soluzione.</span><span class="sxs-lookup"><span data-stu-id="255c2-172">To change a reported property, you set a desired property in solution portal.</span></span> <span data-ttu-id="255c2-173">Il dispositivo è responsabile delle operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="255c2-173">It is the responsibility of the device to:</span></span>

1. <span data-ttu-id="255c2-174">Recuperare periodicamente le proprietà desiderate dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="255c2-174">Periodically retrieve desired properties from the IoT hub.</span></span>
2. <span data-ttu-id="255c2-175">Aggiornare la configurazione con il valore della proprietà desiderata.</span><span class="sxs-lookup"><span data-stu-id="255c2-175">Update its configuration with the desired property value.</span></span>
3. <span data-ttu-id="255c2-176">Inviare il nuovo valore all'hub come proprietà segnalata.</span><span class="sxs-lookup"><span data-stu-id="255c2-176">Send the new value back to the hub as a reported property.</span></span>

<span data-ttu-id="255c2-177">Nel dashboard della soluzione è possibile usare le *proprietà desiderate* per impostare le proprietà in un dispositivo tramite il [dispositivo gemello][lnk-device-twins].</span><span class="sxs-lookup"><span data-stu-id="255c2-177">From the solution dashboard, you can use *desired properties* to set properties on a device by using the [device twin][lnk-device-twins].</span></span> <span data-ttu-id="255c2-178">In genere, il dispositivo legge il valore di una proprietà desiderata dall'hub per aggiornare lo stato interno e segnalare la modifica come proprietà segnalata.</span><span class="sxs-lookup"><span data-stu-id="255c2-178">Typically, a device reads a desired property value from the hub to update its internal state and report the change back as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="255c2-179">Il codice del dispositivo simulato usa le proprietà desiderate **Desired.Config.TemperatureMeanValue** e **Desired.Config.TelemetryInterval** soltanto per aggiornare le proprietà segnalate inviate all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="255c2-179">The simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties sent back to IoT Hub.</span></span> <span data-ttu-id="255c2-180">Tutte le altre richieste di modifica delle proprietà desiderate vengono ignorate nel dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="255c2-180">All other desired property change requests are ignored in the simulated device.</span></span>

### <a name="methods"></a><span data-ttu-id="255c2-181">Metodi</span><span class="sxs-lookup"><span data-stu-id="255c2-181">Methods</span></span>

<span data-ttu-id="255c2-182">I dispositivi simulati possono gestire i [metodi diretti][lnk-direct-methods] seguenti richiamati dal dashboard della soluzione tramite l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="255c2-182">The simulated devices can handle the following methods ([direct methods][lnk-direct-methods]) invoked from the solution portal through the IoT hub:</span></span>

| <span data-ttu-id="255c2-183">Metodo</span><span class="sxs-lookup"><span data-stu-id="255c2-183">Method</span></span> | <span data-ttu-id="255c2-184">Descrizione</span><span class="sxs-lookup"><span data-stu-id="255c2-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="255c2-185">InitiateFirmwareUpdate</span><span class="sxs-lookup"><span data-stu-id="255c2-185">InitiateFirmwareUpdate</span></span> |<span data-ttu-id="255c2-186">Indica al dispositivo di eseguire un aggiornamento del firmware.</span><span class="sxs-lookup"><span data-stu-id="255c2-186">Instructs the device to perform a firmware update</span></span> |
| <span data-ttu-id="255c2-187">Reboot</span><span class="sxs-lookup"><span data-stu-id="255c2-187">Reboot</span></span> |<span data-ttu-id="255c2-188">Indica al dispositivo di eseguire il riavvio.</span><span class="sxs-lookup"><span data-stu-id="255c2-188">Instructs the device to reboot</span></span> |
| <span data-ttu-id="255c2-189">FactoryReset</span><span class="sxs-lookup"><span data-stu-id="255c2-189">FactoryReset</span></span> |<span data-ttu-id="255c2-190">Indica al dispositivo di eseguire un ripristino delle impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="255c2-190">Instructs the device to perform a factory reset</span></span> |

<span data-ttu-id="255c2-191">Alcuni metodi fanno uso delle proprietà segnalate per segnalare lo stato.</span><span class="sxs-lookup"><span data-stu-id="255c2-191">Some methods use reported properties to report on progress.</span></span> <span data-ttu-id="255c2-192">Ad esempio, il metodo **InitiateFirmwareUpdate** simula l'esecuzione asincrona dell'aggiornamento nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-192">For example, the **InitiateFirmwareUpdate** method simulates running the update asynchronously on the device.</span></span> <span data-ttu-id="255c2-193">Il metodo viene restituito immediatamente nel dispositivo, mentre l'attività asincrona continua a inviare aggiornamenti di stato al dashboard della soluzione tramite le proprietà segnalate.</span><span class="sxs-lookup"><span data-stu-id="255c2-193">The method returns immediately on the device, while the asynchronous task continues to send status updates back to the solution dashboard using reported properties.</span></span>

### <a name="commands"></a><span data-ttu-id="255c2-194">Comandi:</span><span class="sxs-lookup"><span data-stu-id="255c2-194">Commands</span></span>

<span data-ttu-id="255c2-195">I dispositivi simulati possono gestire i comandi seguenti, sotto forma di messaggi da cloud a dispositivo, inviati dal portale della soluzione tramite l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="255c2-195">The simulated devices can handle the following commands (cloud-to-device messages) sent from the solution portal through the IoT hub:</span></span>

| <span data-ttu-id="255c2-196">Comando</span><span class="sxs-lookup"><span data-stu-id="255c2-196">Command</span></span> | <span data-ttu-id="255c2-197">Descrizione</span><span class="sxs-lookup"><span data-stu-id="255c2-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="255c2-198">PingDevice</span><span class="sxs-lookup"><span data-stu-id="255c2-198">PingDevice</span></span> |<span data-ttu-id="255c2-199">Invia un *ping* al dispositivo per verificare che sia attivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-199">Sends a *ping* to the device to check it is alive</span></span> |
| <span data-ttu-id="255c2-200">StartTelemetry</span><span class="sxs-lookup"><span data-stu-id="255c2-200">StartTelemetry</span></span> |<span data-ttu-id="255c2-201">Avvia l'invio dei dati di telemetria dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-201">Starts the device sending telemetry</span></span> |
| <span data-ttu-id="255c2-202">StopTelemetry</span><span class="sxs-lookup"><span data-stu-id="255c2-202">StopTelemetry</span></span> |<span data-ttu-id="255c2-203">Arresta l'invio dei dati di telemetria dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-203">Stops the device from sending telemetry</span></span> |
| <span data-ttu-id="255c2-204">ChangeSetPointTemp</span><span class="sxs-lookup"><span data-stu-id="255c2-204">ChangeSetPointTemp</span></span> |<span data-ttu-id="255c2-205">Modifica il valore del punto dati impostato in base al quale vengono generati i dati casuali.</span><span class="sxs-lookup"><span data-stu-id="255c2-205">Changes the set point value around which the random data is generated</span></span> |
| <span data-ttu-id="255c2-206">DiagnosticTelemetry</span><span class="sxs-lookup"><span data-stu-id="255c2-206">DiagnosticTelemetry</span></span> |<span data-ttu-id="255c2-207">Attiva il simulatore del dispositivo per l'invio di un valore di telemetria aggiuntivo (externalTemp)</span><span class="sxs-lookup"><span data-stu-id="255c2-207">Triggers the device simulator to send an additional telemetry value (externalTemp)</span></span> |
| <span data-ttu-id="255c2-208">ChangeDeviceState</span><span class="sxs-lookup"><span data-stu-id="255c2-208">ChangeDeviceState</span></span> |<span data-ttu-id="255c2-209">Modifica una proprietà di stato estesa per il dispositivo e invia il messaggio di informazioni sul dispositivo dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-209">Changes an extended state property for the device and sends the device info message from the device</span></span> |

> [!NOTE]
> <span data-ttu-id="255c2-210">Per un confronto tra questi comandi (messaggi da cloud a dispositivo) e i metodi (metodi diretti), vedere [Indicazioni sulle comunicazioni da cloud a dispositivo][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="255c2-210">For a comparison of these commands (cloud-to-device messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>

## <a name="iot-hub"></a><span data-ttu-id="255c2-211">Hub IoT</span><span class="sxs-lookup"><span data-stu-id="255c2-211">IoT Hub</span></span>

<span data-ttu-id="255c2-212">L'[hub IoT][lnk-iothub] acquisisce i dati inviati dai dispositivi nel cloud e li rende disponibili per i processi di Analisi di flusso di Azure.</span><span class="sxs-lookup"><span data-stu-id="255c2-212">The [IoT hub][lnk-iothub] ingests data sent from the devices into the cloud and makes it available to the Azure Stream Analytics (ASA) jobs.</span></span> <span data-ttu-id="255c2-213">Ogni processo di Analisi di flusso di Azure usa un gruppo di consumer dell'hub IoT separato per leggere il flusso dei messaggi dai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="255c2-213">Each stream ASA job uses a separate IoT Hub consumer group to read the stream of messages from your devices.</span></span>

<span data-ttu-id="255c2-214">L'hub IoT nella soluzione esegue anche le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="255c2-214">The IoT hub in the solution also:</span></span>

- <span data-ttu-id="255c2-215">Gestisce un registro delle identità in cui vengono archiviati gli ID e le chiavi di autenticazione di tutti i dispositivi autorizzati a connettersi al portale.</span><span class="sxs-lookup"><span data-stu-id="255c2-215">Maintains an identity registry that stores the ids and authentication keys of all the devices permitted to connect to the portal.</span></span> <span data-ttu-id="255c2-216">Il registro delle identità permette di abilitare e disabilitare i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="255c2-216">You can enable and disable devices through the identity registry.</span></span>
- <span data-ttu-id="255c2-217">Invia comandi ai dispositivi per conto del portale della soluzione.</span><span class="sxs-lookup"><span data-stu-id="255c2-217">Sends commands to your devices on behalf of the solution portal.</span></span>
- <span data-ttu-id="255c2-218">Richiama i metodi nei dispositivi per conto del portale della soluzione.</span><span class="sxs-lookup"><span data-stu-id="255c2-218">Invokes methods on your devices on behalf of the solution portal.</span></span>
- <span data-ttu-id="255c2-219">Gestisce i dispositivi gemelli per tutti i dispositivi registrati.</span><span class="sxs-lookup"><span data-stu-id="255c2-219">Maintains device twins for all registered devices.</span></span> <span data-ttu-id="255c2-220">Nel dispositivo gemello vengono archiviati i valori delle proprietà segnalati da un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-220">A device twin stores the property values reported by a device.</span></span> <span data-ttu-id="255c2-221">Qui vengono archiviate anche le proprietà desiderate, impostate nel portale della soluzione, in modo che il dispositivo possa recuperarle alla connessione successiva.</span><span class="sxs-lookup"><span data-stu-id="255c2-221">A device twin also stores desired properties, set in the solution portal, for the device to retrieve when it next connects.</span></span>
- <span data-ttu-id="255c2-222">Pianifica processi per impostare proprietà per più dispositivi o richiamare metodi in più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="255c2-222">Schedules jobs to set properties for multiple devices or invoke methods on multiple devices.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="255c2-223">Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="255c2-223">Azure Stream Analytics</span></span>

<span data-ttu-id="255c2-224">Nella soluzione di monitoraggio remoto i messaggi che l'hub IoT riceve dai dispositivi vengono inviati da [Analisi di flusso di Azure][lnk-asa] ad altri componenti di back-end per l'elaborazione o l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="255c2-224">In the remote monitoring solution, [Azure Stream Analytics][lnk-asa] (ASA) dispatches device messages received by the IoT hub to other back-end components for processing or storage.</span></span> <span data-ttu-id="255c2-225">I diversi processi di Analisi di flusso di Azure eseguono operazioni specifiche in base al contenuto dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="255c2-225">Different ASA jobs perform specific functions based on the content of the messages.</span></span>

<span data-ttu-id="255c2-226">**Processo 1: Informazioni sul dispositivo** filtra i messaggi informativi sul dispositivo dal flusso di messaggi in arrivo e li invia a un endpoint di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="255c2-226">**Job 1: Device Info** filters device information messages from the incoming message stream and sends them to an Event Hub endpoint.</span></span> <span data-ttu-id="255c2-227">Un dispositivo invia messaggi di informazioni sul dispositivo all'avvio e in risposta a un comando **SendDeviceInfo** .</span><span class="sxs-lookup"><span data-stu-id="255c2-227">A device sends device information messages at startup and in response to a **SendDeviceInfo** command.</span></span> <span data-ttu-id="255c2-228">Questo processo usa la definizione di query seguente per identificare i messaggi di **informazioni sul dispositivo** :</span><span class="sxs-lookup"><span data-stu-id="255c2-228">This job uses the following query definition to identify **device-info** messages:</span></span>

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

<span data-ttu-id="255c2-229">Questo processo invia l'output a un hub eventi per un'ulteriore elaborazione.</span><span class="sxs-lookup"><span data-stu-id="255c2-229">This job sends its output to an Event Hub for further processing.</span></span>

<span data-ttu-id="255c2-230">**Processo 2: Regole** restituisce valori di telemetria in entrata relativi a temperatura e umidità rispetto alle soglie per dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-230">**Job 2: Rules** evaluates incoming temperature and humidity telemetry values against per-device thresholds.</span></span> <span data-ttu-id="255c2-231">I valori di soglia vengono impostati nell'editor delle regole incluso nel portale della soluzione.</span><span class="sxs-lookup"><span data-stu-id="255c2-231">Threshold values are set in the rules editor available in the solution portal.</span></span> <span data-ttu-id="255c2-232">Ogni coppia dispositivo/valore viene archiviata in base al timestamp in un BLOB che viene letto in Analisi di flusso come **dati di riferimento**.</span><span class="sxs-lookup"><span data-stu-id="255c2-232">Each device/value pair is stored by timestamp in a blob which Stream Analytics reads in as **Reference Data**.</span></span> <span data-ttu-id="255c2-233">Il processo confronta tutti i valori non vuoti rispetto alla soglia impostata per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-233">The job compares any non-empty value against the set threshold for the device.</span></span> <span data-ttu-id="255c2-234">Se supera la condizione ">", il processo genera un evento di **avviso** che segnala che la soglia è stata superata e indica il dispositivo, il valore e i valori di timestamp.</span><span class="sxs-lookup"><span data-stu-id="255c2-234">If it exceeds the '>' condition, the job outputs an **alarm** event that indicates that the threshold is exceeded and provides the device, value, and timestamp values.</span></span> <span data-ttu-id="255c2-235">Questo processo usa la definizione di query seguente per identificare i messaggi di telemetria che devono attivare un allarme:</span><span class="sxs-lookup"><span data-stu-id="255c2-235">This job uses the following query definition to identify telemetry messages that should trigger an alarm:</span></span>

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

<span data-ttu-id="255c2-236">Il processo invia l'output a un hub eventi per un'ulteriore elaborazione e salva i dettagli di ogni avviso nell'archivio BLOB da cui il portale della soluzione può leggere le informazioni sull'avviso.</span><span class="sxs-lookup"><span data-stu-id="255c2-236">The job sends its output to an Event Hub for further processing and saves details of each alert to blob storage from where the solution portal can read the alert information.</span></span>

<span data-ttu-id="255c2-237">**Processo 3: Telemetria** agisce in due modi sul flusso in entrata dei dati di telemetria del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-237">**Job 3: Telemetry** operates on the incoming device telemetry stream in two ways.</span></span> <span data-ttu-id="255c2-238">Il primo invia tutti i messaggi di telemetria dai dispositivi all'archivio BLOB permanente per l'archiviazione a lungo termine.</span><span class="sxs-lookup"><span data-stu-id="255c2-238">The first sends all telemetry messages from the devices to persistent blob storage for long-term storage.</span></span> <span data-ttu-id="255c2-239">Il secondo calcola i valori di umidità media, minima e massima in una finestra temporale scorrevole di cinque minuti e invia questi dati all'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="255c2-239">The second computes average, minimum, and maximum humidity values over a five-minute sliding window and sends this data to blob storage.</span></span> <span data-ttu-id="255c2-240">Il portale della soluzione legge i dati di telemetria dall'archivio BLOB per popolare i grafici.</span><span class="sxs-lookup"><span data-stu-id="255c2-240">The solution portal reads the telemetry data from blob storage to populate the charts.</span></span> <span data-ttu-id="255c2-241">Questo processo usa la definizione di query seguente:</span><span class="sxs-lookup"><span data-stu-id="255c2-241">This job uses the following query definition:</span></span>

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

## <a name="event-hubs"></a><span data-ttu-id="255c2-242">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="255c2-242">Event Hubs</span></span>

<span data-ttu-id="255c2-243">I processi **Informazioni sul dispositivo** e **Regole** di Analisi di flusso di Azure inviano i dati ad Hub eventi, che li inoltra in modo affidabile al **processore di eventi** in esecuzione nel processo Web.</span><span class="sxs-lookup"><span data-stu-id="255c2-243">The **device info** and **rules** ASA jobs output their data to Event Hubs to reliably forward on to the **Event Processor** running in the WebJob.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="255c2-244">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="255c2-244">Azure storage</span></span>

<span data-ttu-id="255c2-245">La soluzione usa l'archivio BLOB di Azure per rendere persistenti tutti i dati di telemetria non elaborati e sintetizzati dai dispositivi presenti nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="255c2-245">The solution uses Azure blob storage to persist all the raw and summarized telemetry data from the devices in the solution.</span></span> <span data-ttu-id="255c2-246">Il portale legge i dati di telemetria dall'archivio BLOB per popolare i grafici.</span><span class="sxs-lookup"><span data-stu-id="255c2-246">The portal reads the telemetry data from blob storage to populate the charts.</span></span> <span data-ttu-id="255c2-247">Per visualizzare gli avvisi, il portale della soluzione legge i dati dall'archivio BLOB che registra quando i valori dei dati di telemetria superano i valori soglia configurati.</span><span class="sxs-lookup"><span data-stu-id="255c2-247">To display alerts, the solution portal reads the data from blob storage that records when telemetry values exceeded the configured threshold values.</span></span> <span data-ttu-id="255c2-248">La soluzione usa anche l'archivio BLOB per registrare i valori soglia impostati nel portale della soluzione.</span><span class="sxs-lookup"><span data-stu-id="255c2-248">The solution also uses blob storage to record the threshold values you set in the solution portal.</span></span>

## <a name="webjobs"></a><span data-ttu-id="255c2-249">WebJobs</span><span class="sxs-lookup"><span data-stu-id="255c2-249">WebJobs</span></span>

<span data-ttu-id="255c2-250">Oltre a ospitare i simulatori dei dispositivi, i processi Web nella soluzione ospitano il **processore di eventi** eseguito in un processo Web di Azure che gestisce le risposte ai comandi.</span><span class="sxs-lookup"><span data-stu-id="255c2-250">In addition to hosting the device simulators, the WebJobs in the solution also host the **Event Processor** running in an Azure WebJob that handles command responses.</span></span> <span data-ttu-id="255c2-251">I messaggi di risposta ai comandi vengono usati per aggiornare la cronologia dei comandi del dispositivo archiviata nel database di Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="255c2-251">It uses command response messages to update the device command history (stored in the Cosmos DB database).</span></span>

## <a name="cosmos-db"></a><span data-ttu-id="255c2-252">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="255c2-252">Cosmos DB</span></span>

<span data-ttu-id="255c2-253">La soluzione usa un database Cosmos DB per archiviare le informazioni nei dispositivi connessi alla soluzione.</span><span class="sxs-lookup"><span data-stu-id="255c2-253">The solution uses a Cosmos DB database to store information about the devices connected to the solution.</span></span> <span data-ttu-id="255c2-254">Tali informazioni includono la cronologia dei comandi inviati ai dispositivi dal portale della soluzione e dei metodi richiamati dal portale della soluzione.</span><span class="sxs-lookup"><span data-stu-id="255c2-254">This information includes the history of commands sent to devices from the solution portal and of methods invoked from the solution portal.</span></span>

## <a name="solution-portal"></a><span data-ttu-id="255c2-255">Portale della soluzione</span><span class="sxs-lookup"><span data-stu-id="255c2-255">Solution portal</span></span>

<span data-ttu-id="255c2-256">Il portale della soluzione è un'app Web che viene distribuita come parte della soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="255c2-256">The solution portal is a web app deployed as part of the preconfigured solution.</span></span> <span data-ttu-id="255c2-257">Le pagine principali nel portale della soluzione sono il dashboard e l'elenco dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="255c2-257">The key pages in the solution portal are the dashboard and the device list.</span></span>

### <a name="dashboard"></a><span data-ttu-id="255c2-258">Dashboard</span><span class="sxs-lookup"><span data-stu-id="255c2-258">Dashboard</span></span>

<span data-ttu-id="255c2-259">Questa pagina dell'app Web usa i controlli JavaScript di Power BI per visualizzare i dati di telemetria inviati dai dispositivi. Vedere in proposito il [repository PowerBI-visuals](https://www.github.com/Microsoft/PowerBI-visuals).</span><span class="sxs-lookup"><span data-stu-id="255c2-259">This page in the web app uses PowerBI javascript controls (See [PowerBI-visuals repo](https://www.github.com/Microsoft/PowerBI-visuals)) to visualize the telemetry data from the devices.</span></span> <span data-ttu-id="255c2-260">La soluzione usa il processo di telemetria di Analisi di flusso di Azure per scrivere i dati di telemetria nell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="255c2-260">The solution uses the ASA telemetry job to write the telemetry data to blob storage.</span></span>

### <a name="device-list"></a><span data-ttu-id="255c2-261">Elenco dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="255c2-261">Device list</span></span>

<span data-ttu-id="255c2-262">Da questa pagina del portale della soluzione è possibile:</span><span class="sxs-lookup"><span data-stu-id="255c2-262">From this page in the solution portal you can:</span></span>

* <span data-ttu-id="255c2-263">Effettuare il provisioning di un nuovo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-263">Provision a new device.</span></span> <span data-ttu-id="255c2-264">Questa azione permette di impostare l'ID univoco del dispositivo e di generare la chiave di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="255c2-264">This action sets the unique device id and generates the authentication key.</span></span> <span data-ttu-id="255c2-265">Le informazioni sul dispositivo verranno scritte sia nel registro delle identità dell'hub IoT che nel database Cosmos DB specifico della soluzione.</span><span class="sxs-lookup"><span data-stu-id="255c2-265">It writes information about the device to both the IoT Hub identity registry and the solution-specific Cosmos DB database.</span></span>
* <span data-ttu-id="255c2-266">Gestire le proprietà dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="255c2-266">Manage device properties.</span></span> <span data-ttu-id="255c2-267">Questa azione include la visualizzazione delle proprietà esistenti e l'aggiornamento con nuove proprietà.</span><span class="sxs-lookup"><span data-stu-id="255c2-267">This action includes viewing existing properties and updating with new properties.</span></span>
* <span data-ttu-id="255c2-268">Inviare comandi a un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-268">Send commands to a device.</span></span>
* <span data-ttu-id="255c2-269">Visualizzare la cronologia dei comandi per un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255c2-269">View the command history for a device.</span></span>
* <span data-ttu-id="255c2-270">Abilitare e disabilitare i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="255c2-270">Enable and disable devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="255c2-271">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="255c2-271">Next steps</span></span>

<span data-ttu-id="255c2-272">I post del blog TechNet offrono altri dettagli sulla soluzione preconfigurata per il monitoraggio remoto:</span><span class="sxs-lookup"><span data-stu-id="255c2-272">The following TechNet blog posts provide more detail about the remote monitoring preconfigured solution:</span></span>

* [<span data-ttu-id="255c2-273">Approfondimento sul monitoraggio remoto in IoT Suite</span><span class="sxs-lookup"><span data-stu-id="255c2-273">IoT Suite - Under The Hood - Remote Monitoring</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [<span data-ttu-id="255c2-274">Aggiunta di dispositivi veri e simulati per il monitoraggio remoto in IoT Suite</span><span class="sxs-lookup"><span data-stu-id="255c2-274">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

<span data-ttu-id="255c2-275">È possibile proseguire con l'introduzione a IoT Suite vedendo gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="255c2-275">You can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="255c2-276">[Connettere il dispositivo alla soluzione preconfigurata per il monitoraggio remoto][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="255c2-276">[Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="255c2-277">[Autorizzazioni per il sito azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="255c2-277">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>

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
