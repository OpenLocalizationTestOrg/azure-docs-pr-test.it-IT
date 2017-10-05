---
title: "Usare le proprietà di un dispositivo gemello dell'hub IoT di Azure (Node) | Documentazione Microsoft"
description: "Come usare le proprietà di un dispositivo gemello dell'hub IoT di Azure per configurare dispositivi. Usare Azure IoT SDK per Node.js per implementare un'app per dispositivo simulato e un'app di servizio che modifica la configurazione di un dispositivo usando un dispositivo gemello."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: d0bcec50-26e6-40f0-8096-733b2f3071ec
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: elioda
ms.openlocfilehash: 771106ce7b00a5231d9929e4b5ea34aefe693597
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-desired-properties-to-configure-devices-node"></a><span data-ttu-id="a6de1-104">Usare le proprietà desiderate per configurare i dispositivi (Node)</span><span class="sxs-lookup"><span data-stu-id="a6de1-104">Use desired properties to configure devices (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="a6de1-105">Al termine di questa esercitazione si avranno due app console Node.js:</span><span class="sxs-lookup"><span data-stu-id="a6de1-105">At the end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="a6de1-106">**SimulateDeviceConfiguration.js**, un'app per dispositivo simulata che attende un aggiornamento della configurazione desiderata e segnala lo stato di un processo di aggiornamento della configurazione simulata.</span><span class="sxs-lookup"><span data-stu-id="a6de1-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports the status of a simulated configuration update process.</span></span>
* <span data-ttu-id="a6de1-107">**SetDesiredConfigurationAndQuery.js**, un'app back-end di Node.js, che imposta la configurazione desiderata in un dispositivo ed esegue query sul processo di aggiornamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="a6de1-107">**SetDesiredConfigurationAndQuery.js**, a Node.js back-end app, which sets the desired configuration on a device and queries the configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="a6de1-108">L'articolo [Azure IoT SDK][lnk-hub-sdks] contiene informazioni sui componenti Azure IoT SDK che consentono di compilare le app back-end e per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="a6de1-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="a6de1-109">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a6de1-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="a6de1-110">Node.js 0.10.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="a6de1-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="a6de1-111">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="a6de1-111">An active Azure account.</span></span> <span data-ttu-id="a6de1-112">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="a6de1-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="a6de1-113">Se si è seguita l'esercitazione [Introduzione ai dispositivi gemelli][lnk-twin-tutorial] sono già disponibili un hub IoT e un'identità del dispositivo denominata **myDeviceId**. È quindi possibile saltare la sezione [Creare l'app per dispositivo simulato][lnk-how-to-configure-createapp].</span><span class="sxs-lookup"><span data-stu-id="a6de1-113">If you followed the [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**; and you can skip to the [Create the simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-simulated-device-app"></a><span data-ttu-id="a6de1-114">Creare l'app per dispositivo simulata</span><span class="sxs-lookup"><span data-stu-id="a6de1-114">Create the simulated device app</span></span>
<span data-ttu-id="a6de1-115">In questa sezione si crea un'app console Node.js che si connette all'hub come **myDeviceId**, attende un aggiornamento della configurazione desiderata e quindi segnala gli aggiornamenti nel processo di aggiornamento della configurazione simulata.</span><span class="sxs-lookup"><span data-stu-id="a6de1-115">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, waits for a desired configuration update and then reports updates on the simulated configuration update process.</span></span>

1. <span data-ttu-id="a6de1-116">Creare una nuova cartella vuota denominata **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="a6de1-116">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="a6de1-117">Nella cartella **simulatedeviceconfiguration** creare un nuovo file package.json immettendo il comando seguente al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="a6de1-117">In the **simulatedeviceconfiguration** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="a6de1-118">Accettare tutte le impostazioni predefinite:</span><span class="sxs-lookup"><span data-stu-id="a6de1-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="a6de1-119">Eseguire questo comando al prompt dei comandi nella cartella **simulatedeviceconfiguration** per installare i pacchetti **azure-iot-device** e **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="a6de1-119">At your command prompt in the **simulatedeviceconfiguration** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="a6de1-120">Usando un editor di testo, creare un nuovo file **SimulateDeviceConfiguration.js** nella cartella **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="a6de1-120">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in the **simulatedeviceconfiguration** folder.</span></span>
4. <span data-ttu-id="a6de1-121">Aggiungere il codice seguente al file **SimulateDeviceConfiguration.js** e sostituire il segnaposto **{device connection string}** con la stringa di connessione copiata quando si è creata l'identità del dispositivo **myDeviceId**:</span><span class="sxs-lookup"><span data-stu-id="a6de1-121">Add the following code to the **SimulateDeviceConfiguration.js** file, and substitute the **{device connection string}** placeholder with the device connection string you copied when you created the **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    <span data-ttu-id="a6de1-122">L'oggetto **Client** espone tutti i metodi necessari per interagire con i dispositivi gemelli dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a6de1-122">The **Client** object exposes all the methods required to interact with device twins from the device.</span></span> <span data-ttu-id="a6de1-123">Il codice precedente, dopo avere inizializzato l'oggetto **Client**, recupera il dispositivo gemello per **myDeviceId** e collega un gestore per l'aggiornamento nelle proprietà desiderate.</span><span class="sxs-lookup"><span data-stu-id="a6de1-123">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId**, and attaches a handler for the update on desired properties.</span></span> <span data-ttu-id="a6de1-124">Il gestore verifica che esista una richiesta di modifica della configurazione effettiva confrontando gli elementi configId, quindi richiama un metodo che avvia la modifica della configurazione.</span><span class="sxs-lookup"><span data-stu-id="a6de1-124">The handler verifies that there is an actual configuration change request by comparing the configIds, then invokes a method that starts the configuration change.</span></span>
   
    <span data-ttu-id="a6de1-125">Si noti che per semplicità il codice precedente usa un valore predefinito hardcoded per la configurazione iniziale.</span><span class="sxs-lookup"><span data-stu-id="a6de1-125">Note that for the sake of simplicity, the previous code uses a hard-coded default for the inital configuration.</span></span> <span data-ttu-id="a6de1-126">Una vera app probabilmente caricherebbe tale configurazione da una risorsa di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="a6de1-126">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="a6de1-127">Gli eventi di modifica delle proprietà desiderate vengono generati sempre una volta al momento della connessione del dispositivo. Controllare che esista una modifica effettiva nelle proprietà desiderate prima di eseguire eventuali azioni.</span><span class="sxs-lookup"><span data-stu-id="a6de1-127">Desired property change events are always emitted once at device connection, make sure to check that there is an actual change in the desired properties before performing any action.</span></span>
   > 
   > 
5. <span data-ttu-id="a6de1-128">Aggiungere i metodi seguenti prima della chiamata a `client.open()`:</span><span class="sxs-lookup"><span data-stu-id="a6de1-128">Add the following methods before the `client.open()` invocation:</span></span>
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    <span data-ttu-id="a6de1-129">Il metodo **initConfigChange** aggiorna le proprietà segnalate nell'oggetto dispositivo gemello locale con la richiesta di aggiornamento della configurazione e imposta lo stato su **Pending** (Sospeso), quindi aggiorna il dispositivo gemello nel servizio.</span><span class="sxs-lookup"><span data-stu-id="a6de1-129">The **initConfigChange** method updates reported properties on the local device twin object with the configuration update request and sets the status to **Pending**, then updates the device twin on the service.</span></span> <span data-ttu-id="a6de1-130">Dopo l'aggiornamento del dispositivo gemello, simula un processo a esecuzione prolungata che termina con l'esecuzione di **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="a6de1-130">After successfully updating the device twin, it simulates a long running process that terminates in the execution of **completeConfigChange**.</span></span> <span data-ttu-id="a6de1-131">Questo metodo aggiorna le proprietà segnalate del dispositivo gemello locale impostando lo stato su **Success** e rimuovendo l'oggetto **pendingConfig**,</span><span class="sxs-lookup"><span data-stu-id="a6de1-131">This method updates the local device twin's reported properties setting the status to **Success** and removing the **pendingConfig** object.</span></span> <span data-ttu-id="a6de1-132">quindi aggiorna il dispositivo gemello nel servizio.</span><span class="sxs-lookup"><span data-stu-id="a6de1-132">It then updates the device twin on the service.</span></span>
   
    <span data-ttu-id="a6de1-133">Si noti che, per risparmiare larghezza di banda, le proprietà segnalate vengono aggiornate specificando solo le proprietà da modificare (denominate **patch** nel codice precedente), invece di sostituire l'intero documento.</span><span class="sxs-lookup"><span data-stu-id="a6de1-133">Note that, to save bandwidth, reported properties are updated by specifying only the properties to be modified (named **patch** in the above code), instead of replacing the whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a6de1-134">Questa esercitazione non simula alcun comportamento per gli aggiornamenti della configurazione simultanei.</span><span class="sxs-lookup"><span data-stu-id="a6de1-134">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="a6de1-135">Alcuni processi di aggiornamento della configurazione potrebbero consentire modifiche della configurazione di destinazione mentre l'aggiornamento è in esecuzione, altre potrebbero doverle accodare e altri ancora rifiutarle con una condizione di errore.</span><span class="sxs-lookup"><span data-stu-id="a6de1-135">Some configuration update processes might be able to accommodate changes of target configuration while the update is running, others might have to queue them, and others could reject them with an error condition.</span></span> <span data-ttu-id="a6de1-136">È importante tenere in considerazione il comportamento desiderato per il processo di configurazione specifico e aggiungere la logica appropriata prima di iniziare la modifica della configurazione.</span><span class="sxs-lookup"><span data-stu-id="a6de1-136">Make sure to consider the desired behavior for your specific configuration process, and add the appropriate logic before initiating the configuration change.</span></span>
   > 
   > 
6. <span data-ttu-id="a6de1-137">Eseguire l'app per dispositivo:</span><span class="sxs-lookup"><span data-stu-id="a6de1-137">Run the device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="a6de1-138">Dovrebbe essere visualizzato il messaggio `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="a6de1-138">You should see the message `retrieved device twin`.</span></span> <span data-ttu-id="a6de1-139">Mantenere l'app in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a6de1-139">Keep the app running.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="a6de1-140">Creare l'app di servizio</span><span class="sxs-lookup"><span data-stu-id="a6de1-140">Create the service app</span></span>
<span data-ttu-id="a6de1-141">In questa sezione si creerà un'app console Node.js che aggiorna le *proprietà desiderate* nel dispositivo gemello associato a **myDeviceId** con un nuovo oggetto di configurazione di telemetria.</span><span class="sxs-lookup"><span data-stu-id="a6de1-141">In this section, you will create a Node.js console app that updates the *desired properties* on the device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="a6de1-142">Viene quindi effettuata una query dei dispositivi gemelli archiviati nell'hub IoT e viene visualizzata la differenza tra la configurazione desiderata e quella segnalata del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a6de1-142">It then queries the device twins stored in the IoT hub and shows the difference between the desired and reported configurations of the device.</span></span>

1. <span data-ttu-id="a6de1-143">Creare una nuova cartella vuota denominata **setdesiredandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="a6de1-143">Create a new empty folder called **setdesiredandqueryapp**.</span></span> <span data-ttu-id="a6de1-144">Nella cartella **setdesiredandqueryapp** creare un nuovo file package.json immettendo il comando seguente al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="a6de1-144">In the **setdesiredandqueryapp** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="a6de1-145">Accettare tutte le impostazioni predefinite:</span><span class="sxs-lookup"><span data-stu-id="a6de1-145">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="a6de1-146">Eseguire questo comando al prompt dei comandi nella cartella **setdesiredandqueryapp** per installare il pacchetto **azure-iothub**:</span><span class="sxs-lookup"><span data-stu-id="a6de1-146">At your command prompt in the **setdesiredandqueryapp** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. <span data-ttu-id="a6de1-147">Usando un editor di testo, creare un nuovo file **SetDesiredAndQuery.js** nella cartella **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="a6de1-147">Using a text editor, create a new **SetDesiredAndQuery.js** file in the **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="a6de1-148">Aggiungere il codice seguente al file **SetDesiredAndQuery.js** e sostituire il segnaposto **{iot hub connection string}** con la stringa di connessione dell'hub IoT copiata quando è stato creato l'hub:</span><span class="sxs-lookup"><span data-stu-id="a6de1-148">Add the following code to the **SetDesiredAndQuery.js** file, and substitute the **{iot hub connection string}** placeholder with the IoT Hub connection string you copied when you created your hub:</span></span>
   
        'use strict';
        var iothub = require('azure-iothub');
        var uuid = require('node-uuid');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var newConfigId = uuid.v4();
                var newFrequency = process.argv[2] || "5m";
                var patch = {
                    properties: {
                        desired: {
                            telemetryConfig: {
                                configId: newConfigId,
                                sendFrequency: newFrequency
                            }
                        }
                    }
                }
                twin.update(patch, function(err) {
                    if (err) {
                        console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                    } else {
                        console.log(twin.deviceId + ' twin updated successfully');
                    }
                });
                setInterval(queryTwins, 10000);
            }
        });

    <span data-ttu-id="a6de1-149">L'oggetto **Registry** espone tutti i metodi necessari per interagire con i dispositivi gemelli dal servizio.</span><span class="sxs-lookup"><span data-stu-id="a6de1-149">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="a6de1-150">Il codice precedente, dopo avere inizializzato l'oggetto **Registry**, recupera il dispositivo gemello per **myDeviceId** e ne aggiorna le proprietà desiderate con un nuovo oggetto di configurazione della telemetria.</span><span class="sxs-lookup"><span data-stu-id="a6de1-150">The previous code, after it initializes the **Registry** object, retrieves the device twin for **myDeviceId**, and updates its desired properties with a new telemetry configuration object.</span></span> <span data-ttu-id="a6de1-151">quindi chiama l'evento della funzione **queryTwins** ogni 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="a6de1-151">After that, it calls the **queryTwins** function event 10 seconds.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="a6de1-152">Questa applicazione effettua una query dell'hub IoT ogni 10 secondi a scopo illustrativo.</span><span class="sxs-lookup"><span data-stu-id="a6de1-152">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="a6de1-153">Usare le query per generare i report destinati all'utente in più dispositivi e non per rilevare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="a6de1-153">Use queries to generate user-facing reports across many devices, and not to detect changes.</span></span> <span data-ttu-id="a6de1-154">Se la soluzione richiede notifiche in tempo reale degli eventi del dispositivo, usare le [notifiche relative al dispositivo gemello][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="a6de1-154">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
    > 
    ><span data-ttu-id="a6de1-155">.</span><span class="sxs-lookup"><span data-stu-id="a6de1-155">.</span></span>

1. <span data-ttu-id="a6de1-156">Aggiungere il codice seguente subito prima della chiamata a `registry.getDeviceTwin()` per implementare la funzione **queryTwins**:</span><span class="sxs-lookup"><span data-stu-id="a6de1-156">Add the following code right before the `registry.getDeviceTwin()` invocation to implement the **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
                } else {
                    console.log();
                    results.forEach(function(twin) {
                        var desiredConfig = twin.properties.desired.telemetryConfig;
                        var reportedConfig = twin.properties.reported.telemetryConfig;
                        console.log("Config report for: " + twin.deviceId);
                        console.log("Desired: ");
                        console.log(JSON.stringify(desiredConfig, null, 2));
                        console.log("Reported: ");
                        console.log(JSON.stringify(reportedConfig, null, 2));
                    });
                }
            });
        };
   
    <span data-ttu-id="a6de1-157">Il codice precedente effettua una query dei dispositivi gemelli archiviati nell'hub IoT e visualizza la configurazione della telemetria desiderata e quella segnalata.</span><span class="sxs-lookup"><span data-stu-id="a6de1-157">The previous code queries the device twins stored in the IoT hub and prints the desired and reported telemetry configurations.</span></span> <span data-ttu-id="a6de1-158">Vedere il [linguaggio di query dell'hub IoT][lnk-query] per informazioni su come generare report avanzati in tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="a6de1-158">Refer to the [IoT Hub query language][lnk-query] to learn how to generate rich reports across all your devices.</span></span>
2. <span data-ttu-id="a6de1-159">Con **SimulateDeviceConfiguration.js** in esecuzione, eseguire l'applicazione con:</span><span class="sxs-lookup"><span data-stu-id="a6de1-159">With **SimulateDeviceConfiguration.js** running, run the application with:</span></span>
   
        node SetDesiredAndQuery.js 5m
   
    <span data-ttu-id="a6de1-160">Si potrà osservare la configurazione segnalata passare da **Success** a **Pending** e di nuovo a **Success** con la nuova frequenza di invio attiva di cinque minuti e non più di 24 ore.</span><span class="sxs-lookup"><span data-stu-id="a6de1-160">You should see the reported configuration change from **Success** to **Pending** to **Success** again with the new active send frequency of five minutes instead of 24 hours.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="a6de1-161">Tra l'operazione relativa al report del dispositivo e il risultato della query si verifica un ritardo fino a un minuto,</span><span class="sxs-lookup"><span data-stu-id="a6de1-161">There is a delay of up to a minute between the device report operation and the query result.</span></span> <span data-ttu-id="a6de1-162">che consente all'infrastruttura della query di funzionare su una scala molto ampia.</span><span class="sxs-lookup"><span data-stu-id="a6de1-162">This is to enable the query infrastructure to work at very high scale.</span></span> <span data-ttu-id="a6de1-163">Per recuperare visualizzazioni coerenti di un solo dispositivo gemello, usare il metodo **getDeviceTwin** nella classe **Registry**.</span><span class="sxs-lookup"><span data-stu-id="a6de1-163">To retrieve consistent views of a single device twin use the **getDeviceTwin** method in the **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="a6de1-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a6de1-164">Next steps</span></span>
<span data-ttu-id="a6de1-165">In questa esercitazione è stata impostata una configurazione desiderata come *proprietà desiderate* da un'app back-end ed è stata scritta un'app per dispositivo simulato per rilevare tale modifica e simulare un processo di aggiornamento in più fasi che segnala lo stato come *proprietà segnalate* al dispositivo gemello.</span><span class="sxs-lookup"><span data-stu-id="a6de1-165">In this tutorial, you set a desired configuration as *desired properties* from a back-end app, and wrote a simulated device app to detect that change and simulate a multi-step update process reporting its status as *reported properties* to the device twin.</span></span>

<span data-ttu-id="a6de1-166">Per altre informazioni, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="a6de1-166">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="a6de1-167">Per inviare dati di telemetria dai dispositivi, vedere l'esercitazione [Introduzione all'hub IoT][lnk-iothub-getstarted].</span><span class="sxs-lookup"><span data-stu-id="a6de1-167">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="a6de1-168">Per pianificare o eseguire operazioni su grandi set di dispositivi, vedere l'esercitazione [Pianificare e trasmettere processi][lnk-schedule-jobs].</span><span class="sxs-lookup"><span data-stu-id="a6de1-168">schedule or perform operations on large sets of devices see the [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="a6de1-169">Per controllare i dispositivi in modo interattivo, ad esempio per attivare un ventilatore da un'app controllata dall'utente, vedere l'esercitazione [Use direct methods][lnk-methods-tutorial] (Usare metodi diretti).</span><span class="sxs-lookup"><span data-stu-id="a6de1-169">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-node-node-twin-how-to-configure.md#create-the-simulated-device-app
