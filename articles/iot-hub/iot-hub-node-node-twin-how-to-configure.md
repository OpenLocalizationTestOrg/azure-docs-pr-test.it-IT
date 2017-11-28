---
title: "proprietà di un doppio dispositivo IoT Hub Azure aaaUse (nodo) | Documenti Microsoft"
description: "Come dispositivo di Azure IoT Hub toouse gemelli di tooconfigure dispositivi. È consigliabile utilizzare hello Azure IoT SDK per Node.js tooimplement un'app dispositivo simulato e un'applicazione di servizio che consente di modificare la configurazione di un dispositivo utilizzando una coppia di dispositivo."
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
ms.openlocfilehash: 7ebfe2dfa0876bf04fdbaceae55db76456523e8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices-node"></a><span data-ttu-id="4714b-104">Lo si desidera utilizzare proprietà tooconfigure dispositivi (nodo)</span><span class="sxs-lookup"><span data-stu-id="4714b-104">Use desired properties tooconfigure devices (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="4714b-105">Alla fine di hello di questa esercitazione, si avranno due applicazioni di console Node.js:</span><span class="sxs-lookup"><span data-stu-id="4714b-105">At hello end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="4714b-106">**SimulateDeviceConfiguration.js**, un'app dispositivo simulato che è in attesa di un aggiornamento della configurazione desiderata e hello Visualizza lo stato di un processo di aggiornamento configurazione simulato.</span><span class="sxs-lookup"><span data-stu-id="4714b-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="4714b-107">**SetDesiredConfigurationAndQuery.js**, configurazione in un dispositivo di un'applicazione back-end di Node. js, che imposta hello desiderato e le query hello il processo di aggiornamento di configurazione.</span><span class="sxs-lookup"><span data-stu-id="4714b-107">**SetDesiredConfigurationAndQuery.js**, a Node.js back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="4714b-108">articolo Hello [Azure IoT SDK] [ lnk-hub-sdks] fornisce informazioni su Azure IoT SDK hello che è possibile utilizzare toobuild applicazioni back-end sia sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4714b-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="4714b-109">toocomplete questa esercitazione è necessario hello segue:</span><span class="sxs-lookup"><span data-stu-id="4714b-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="4714b-110">Node.js 0.10.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="4714b-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="4714b-111">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="4714b-111">An active Azure account.</span></span> <span data-ttu-id="4714b-112">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="4714b-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="4714b-113">Se si sono seguite hello [introduzione gemelli dispositivo] [ lnk-twin-tutorial] esercitazione, si dispone già di un hub IoT e un'identità del dispositivo chiamato **myDeviceId**; ed è possibile ignorare toohello [ Creare app dispositivo simulato hello] [ lnk-how-to-configure-createapp] sezione.</span><span class="sxs-lookup"><span data-stu-id="4714b-113">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**; and you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="4714b-114">Creare app dispositivo simulato hello</span><span class="sxs-lookup"><span data-stu-id="4714b-114">Create hello simulated device app</span></span>
<span data-ttu-id="4714b-115">In questa sezione si crea un'applicazione console Node.js che si connette hub tooyour come **myDeviceId**, in attesa di un aggiornamento della configurazione desiderata e quindi segnala gli aggiornamenti nel processo di aggiornamento configurazione hello simulato.</span><span class="sxs-lookup"><span data-stu-id="4714b-115">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="4714b-116">Creare una nuova cartella vuota denominata **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="4714b-116">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="4714b-117">In hello **simulatedeviceconfiguration** cartella, creare un nuovo file package. JSON utilizzando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="4714b-117">In hello **simulatedeviceconfiguration** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="4714b-118">Accettare tutte le impostazioni predefinite hello:</span><span class="sxs-lookup"><span data-stu-id="4714b-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="4714b-119">Al prompt dei comandi in hello **simulatedeviceconfiguration** cartella, eseguire hello successivo comando tooinstall hello **dispositivi iot di azure**, e **azure-iot-dispositivo-mqtt**pacchetto:</span><span class="sxs-lookup"><span data-stu-id="4714b-119">At your command prompt in hello **simulatedeviceconfiguration** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="4714b-120">Utilizzando un editor di testo, creare un nuovo **SimulateDeviceConfiguration.js** file hello **simulatedeviceconfiguration** cartella.</span><span class="sxs-lookup"><span data-stu-id="4714b-120">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in hello **simulatedeviceconfiguration** folder.</span></span>
4. <span data-ttu-id="4714b-121">Aggiungere hello seguente codice toohello **SimulateDeviceConfiguration.js** file e sostituire hello **{stringa di connessione dispositivo}** segnaposto con stringa di connessione dispositivo hello copiato quando si creato hello **myDeviceId** identità del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="4714b-121">Add hello following code toohello **SimulateDeviceConfiguration.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="4714b-122">Hello **Client** oggetto espone tutte hello metodi obbligatorio toointeract con gemelli di dispositivo dal dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="4714b-122">hello **Client** object exposes all hello methods required toointeract with device twins from hello device.</span></span> <span data-ttu-id="4714b-123">Hello codice precedente, dopo l'inizializzazione hello **Client** oggetto recupera hello gemelli di dispositivo per **myDeviceId**e associa un gestore per l'aggiornamento di hello nella proprietà desiderate.</span><span class="sxs-lookup"><span data-stu-id="4714b-123">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId**, and attaches a handler for hello update on desired properties.</span></span> <span data-ttu-id="4714b-124">gestore Hello verifica che sia presente una richiesta di modifica della configurazione effettiva confrontando configIds hello, quindi richiama un metodo che avvia una modifica della configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="4714b-124">hello handler verifies that there is an actual configuration change request by comparing hello configIds, then invokes a method that starts hello configuration change.</span></span>
   
    <span data-ttu-id="4714b-125">Si noti che per i migliori risultati hello di semplicità, codice precedente hello Usa valore predefinito è hardcoded per la configurazione iniziale di hello.</span><span class="sxs-lookup"><span data-stu-id="4714b-125">Note that for hello sake of simplicity, hello previous code uses a hard-coded default for hello inital configuration.</span></span> <span data-ttu-id="4714b-126">Una vera app probabilmente caricherebbe tale configurazione da una risorsa di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="4714b-126">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="4714b-127">Gli eventi di modifica delle proprietà desiderati vengono sempre inviati una volta alla connessione del dispositivo, assicurarsi che vi sia una modifica effettiva in hello toocheck le proprietà desiderate prima di eseguire qualsiasi azione.</span><span class="sxs-lookup"><span data-stu-id="4714b-127">Desired property change events are always emitted once at device connection, make sure toocheck that there is an actual change in hello desired properties before performing any action.</span></span>
   > 
   > 
5. <span data-ttu-id="4714b-128">Aggiungere i seguenti metodi prima hello hello `client.open()` chiamata:</span><span class="sxs-lookup"><span data-stu-id="4714b-128">Add hello following methods before hello `client.open()` invocation:</span></span>
   
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
   
    <span data-ttu-id="4714b-129">Hello **initConfigChange** metodo aggiorna segnalati proprietà sull'oggetto di un doppio hello dispositivo locale con hello richiesta di aggiornamento della configurazione e set hello stato troppo**in sospeso**, quindi gli aggiornamenti hello dispositivo doppio servizio hello.</span><span class="sxs-lookup"><span data-stu-id="4714b-129">hello **initConfigChange** method updates reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="4714b-130">Dopo aver aggiornato correttamente un doppio dispositivo hello, simula un processo a esecuzione prolungata che termina l'esecuzione di hello **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="4714b-130">After successfully updating hello device twin, it simulates a long running process that terminates in hello execution of **completeConfigChange**.</span></span> <span data-ttu-id="4714b-131">Questo metodo aggiornamenti hello dispositivo locale disponibilità di una copia del segnalato le proprietà di impostazione dello stato di hello troppo**successo** e rimozione di hello **pendingConfig** oggetto.</span><span class="sxs-lookup"><span data-stu-id="4714b-131">This method updates hello local device twin's reported properties setting hello status too**Success** and removing hello **pendingConfig** object.</span></span> <span data-ttu-id="4714b-132">Viene quindi aggiornato doppi dispositivo hello sul servizio hello.</span><span class="sxs-lookup"><span data-stu-id="4714b-132">It then updates hello device twin on hello service.</span></span>
   
    <span data-ttu-id="4714b-133">Si noti che, della larghezza di banda toosave segnalati proprietà vengono aggiornate specificando solo hello proprietà toobe modificato (denominato **patch** in hello sopra codice), anziché sostituire hello intero documento.</span><span class="sxs-lookup"><span data-stu-id="4714b-133">Note that, toosave bandwidth, reported properties are updated by specifying only hello properties toobe modified (named **patch** in hello above code), instead of replacing hello whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4714b-134">Questa esercitazione non simula alcun comportamento per gli aggiornamenti della configurazione simultanei.</span><span class="sxs-lookup"><span data-stu-id="4714b-134">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="4714b-135">Alcuni processi di aggiornamento configurazione potrebbero essere in grado di tooaccommodate modifiche della configurazione di destinazione durante l'esecuzione di aggiornamento hello, altri utenti potrebbe essere tooqueue e su altri possibile rifiutarli con una condizione di errore.</span><span class="sxs-lookup"><span data-stu-id="4714b-135">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, others might have tooqueue them, and others could reject them with an error condition.</span></span> <span data-ttu-id="4714b-136">Verificare che tooconsider hello comportamento desiderato per il processo di configurazione specifica e aggiungere la logica appropriata hello prima dell'avvio di modifica della configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="4714b-136">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
6. <span data-ttu-id="4714b-137">Eseguire app per dispositivi hello:</span><span class="sxs-lookup"><span data-stu-id="4714b-137">Run hello device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="4714b-138">Verrà visualizzato il messaggio hello `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="4714b-138">You should see hello message `retrieved device twin`.</span></span> <span data-ttu-id="4714b-139">Mantenere hello app in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="4714b-139">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="4714b-140">Creare l'applicazione di servizio hello</span><span class="sxs-lookup"><span data-stu-id="4714b-140">Create hello service app</span></span>
<span data-ttu-id="4714b-141">In questa sezione si creerà un'applicazione console in Node.js tale hello aggiornamenti *le proprietà desiderate* su hello gemelli di dispositivo associati **myDeviceId** con un nuovo oggetto di configurazione di telemetria.</span><span class="sxs-lookup"><span data-stu-id="4714b-141">In this section, you will create a Node.js console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="4714b-142">Quindi esegue una query gemelli dispositivo hello archiviate nell'hub IoT hello e Mostra differenza hello tra hello desiderato e le configurazioni di dispositivo hello segnalato.</span><span class="sxs-lookup"><span data-stu-id="4714b-142">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="4714b-143">Creare una nuova cartella vuota denominata **setdesiredandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="4714b-143">Create a new empty folder called **setdesiredandqueryapp**.</span></span> <span data-ttu-id="4714b-144">In hello **setdesiredandqueryapp** cartella, creare un nuovo file package. JSON utilizzando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="4714b-144">In hello **setdesiredandqueryapp** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="4714b-145">Accettare tutte le impostazioni predefinite hello:</span><span class="sxs-lookup"><span data-stu-id="4714b-145">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="4714b-146">Al prompt dei comandi in hello **setdesiredandqueryapp** cartella, eseguire hello successivo comando tooinstall hello **hub IOT di azure** pacchetto:</span><span class="sxs-lookup"><span data-stu-id="4714b-146">At your command prompt in hello **setdesiredandqueryapp** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. <span data-ttu-id="4714b-147">Utilizzando un editor di testo, creare un nuovo **SetDesiredAndQuery.js** file hello **addtagsandqueryapp** cartella.</span><span class="sxs-lookup"><span data-stu-id="4714b-147">Using a text editor, create a new **SetDesiredAndQuery.js** file in hello **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="4714b-148">Aggiungere i seguenti toohello codice hello **SetDesiredAndQuery.js** file e sostituire hello **{stringa di connessione hub iot}** segnaposto con hello stringa di connessione IoT Hub è stato copiato al momento della creazione dell'hub :</span><span class="sxs-lookup"><span data-stu-id="4714b-148">Add hello following code toohello **SetDesiredAndQuery.js** file, and substitute hello **{iot hub connection string}** placeholder with hello IoT Hub connection string you copied when you created your hub:</span></span>
   
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

    <span data-ttu-id="4714b-149">Hello **Registro di sistema** oggetto espone tutte hello metodi obbligatorio toointeract con gemelli di dispositivo dal servizio hello.</span><span class="sxs-lookup"><span data-stu-id="4714b-149">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="4714b-150">Hello codice precedente, dopo l'inizializzazione hello **Registro di sistema** oggetto recupera hello gemelli di dispositivo per **myDeviceId**e aggiorna le proprietà desiderate con un nuovo oggetto di configurazione di telemetria.</span><span class="sxs-lookup"><span data-stu-id="4714b-150">hello previous code, after it initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and updates its desired properties with a new telemetry configuration object.</span></span> <span data-ttu-id="4714b-151">Successivamente, chiama hello **queryTwins** funzione evento 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="4714b-151">After that, it calls hello **queryTwins** function event 10 seconds.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4714b-152">Questa applicazione effettua una query dell'hub IoT ogni 10 secondi a scopo illustrativo.</span><span class="sxs-lookup"><span data-stu-id="4714b-152">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="4714b-153">Utilizzare una query toogenerate rivolta all'utente report tra più dispositivi e non toodetect modifiche.</span><span class="sxs-lookup"><span data-stu-id="4714b-153">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="4714b-154">Se la soluzione richiede notifiche in tempo reale degli eventi del dispositivo, usare le [notifiche relative al dispositivo gemello][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="4714b-154">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
    > 
    ><span data-ttu-id="4714b-155">.</span><span class="sxs-lookup"><span data-stu-id="4714b-155">.</span></span>

1. <span data-ttu-id="4714b-156">Aggiungere hello seguente di codice subito prima di hello `registry.getDeviceTwin()` hello tooimplement chiamata **queryTwins** funzione:</span><span class="sxs-lookup"><span data-stu-id="4714b-156">Add hello following code right before hello `registry.getDeviceTwin()` invocation tooimplement hello **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
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
   
    <span data-ttu-id="4714b-157">query di codice precedenti Hello hello gemelli dispositivo memorizzato nell'hub IoT hello e stampa hello desiderato e segnalate le configurazioni di telemetria.</span><span class="sxs-lookup"><span data-stu-id="4714b-157">hello previous code queries hello device twins stored in hello IoT hub and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="4714b-158">Fare riferimento toohello [il linguaggio di query di IoT Hub] [ lnk-query] toolearn come rich toogenerate report tra tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="4714b-158">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
2. <span data-ttu-id="4714b-159">Con **SimulateDeviceConfiguration.js** in esecuzione, eseguire un'applicazione hello con:</span><span class="sxs-lookup"><span data-stu-id="4714b-159">With **SimulateDeviceConfiguration.js** running, run hello application with:</span></span>
   
        node SetDesiredAndQuery.js 5m
   
    <span data-ttu-id="4714b-160">Dovrebbe essere hello segnalati configurazione modificare da **esito positivo** troppo**in sospeso** troppo**successo** nuovamente Active nuovo hello frequenza di invio dei cinque minuti anziché 24 ore.</span><span class="sxs-lookup"><span data-stu-id="4714b-160">You should see hello reported configuration change from **Success** too**Pending** too**Success** again with hello new active send frequency of five minutes instead of 24 hours.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="4714b-161">Si verifica un ritardo di backup tooa minuto tra funzionamento del report dispositivo hello e risultato della query hello.</span><span class="sxs-lookup"><span data-stu-id="4714b-161">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="4714b-162">Si tratta di tooenable hello query infrastruttura toowork su larga scala molto elevata.</span><span class="sxs-lookup"><span data-stu-id="4714b-162">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="4714b-163">viste di un doppio di un singolo dispositivo consistenza tooretrieve utilizzano hello **getDeviceTwin** metodo hello **Registro di sistema** classe.</span><span class="sxs-lookup"><span data-stu-id="4714b-163">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="4714b-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4714b-164">Next steps</span></span>
<span data-ttu-id="4714b-165">In questa esercitazione, impostare una configurazione desiderata come *le proprietà desiderate* da un'app di back-end e ha scritto un toodetect app dispositivo simulato che modificano e simulare un processo di aggiornamento di più passaggi reporting stato  *proprietà segnalati* toohello gemelli di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4714b-165">In this tutorial, you set a desired configuration as *desired properties* from a back-end app, and wrote a simulated device app toodetect that change and simulate a multi-step update process reporting its status as *reported properties* toohello device twin.</span></span>

<span data-ttu-id="4714b-166">Hello utilizzare seguenti come risorse toolearn per:</span><span class="sxs-lookup"><span data-stu-id="4714b-166">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="4714b-167">inviare i dati di telemetria dai dispositivi con hello [iniziare con l'IoT Hub] [ lnk-iothub-getstarted] esercitazione</span><span class="sxs-lookup"><span data-stu-id="4714b-167">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="4714b-168">pianificare o eseguire operazioni su grandi set di dispositivi Vedere hello [pianificazione e i processi di broadcast] [ lnk-schedule-jobs] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4714b-168">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="4714b-169">controllare i dispositivi in modo interattivo (ad esempio l'attivazione di una ventola da un'app controllata dall'utente), con hello [utilizzare metodi diretti] [ lnk-methods-tutorial] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4714b-169">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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
