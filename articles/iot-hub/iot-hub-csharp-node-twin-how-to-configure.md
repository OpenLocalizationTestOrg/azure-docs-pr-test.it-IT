---
title: "proprietà di un doppio dispositivo IoT Hub Azure aaaUse (.NET/nodo) | Documenti Microsoft"
description: Come dispositivo di Azure IoT Hub toouse gemelli di tooconfigure dispositivi. Utilizzare il dispositivo di Azure IoT hello SDK per Node.js tooimplement un'app dispositivo simulato e hello Azure IoT servizio SDK per .NET tooimplement un'applicazione di servizio che consente di modificare la configurazione di un dispositivo utilizzando una coppia di dispositivo.
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: elioda
ms.openlocfilehash: 840a1b2e45f4763131299577583aa89015dcdd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a><span data-ttu-id="a747c-104">Utilizzare i dispositivi di proprietà desiderato tooconfigure</span><span class="sxs-lookup"><span data-stu-id="a747c-104">Use desired properties tooconfigure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="a747c-105">Alla fine di hello di questa esercitazione, si avranno due applicazioni console:</span><span class="sxs-lookup"><span data-stu-id="a747c-105">At hello end of this tutorial, you will have two console apps:</span></span>

* <span data-ttu-id="a747c-106">**SimulateDeviceConfiguration.js**, un'app dispositivo simulato che è in attesa di un aggiornamento della configurazione desiderata e hello Visualizza lo stato di un processo di aggiornamento configurazione simulato.</span><span class="sxs-lookup"><span data-stu-id="a747c-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="a747c-107">**SetDesiredConfigurationAndQuery**, configurazione in un dispositivo di un'app di back-end .NET, che imposta hello desiderato e le query hello il processo di aggiornamento di configurazione.</span><span class="sxs-lookup"><span data-stu-id="a747c-107">**SetDesiredConfigurationAndQuery**, a .NET back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="a747c-108">articolo Hello [Azure IoT SDK] [ lnk-hub-sdks] fornisce informazioni su Azure IoT SDK hello che è possibile utilizzare toobuild applicazioni back-end sia sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a747c-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="a747c-109">toocomplete questa esercitazione è necessario hello segue:</span><span class="sxs-lookup"><span data-stu-id="a747c-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="a747c-110">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="a747c-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="a747c-111">Node.js 0.10.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="a747c-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="a747c-112">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="a747c-112">An active Azure account.</span></span> <span data-ttu-id="a747c-113">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="a747c-113">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="a747c-114">Se si sono seguite hello [introduzione gemelli dispositivo] [ lnk-twin-tutorial] esercitazione, si dispone già di un hub IoT e un'identità del dispositivo chiamato **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="a747c-114">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="a747c-115">In tal caso, è possibile ignorare toohello [crea hello dispositivo simulato applicazione] [ lnk-how-to-configure-createapp] sezione.</span><span class="sxs-lookup"><span data-stu-id="a747c-115">In that case, you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="a747c-116">Creare app dispositivo simulato hello</span><span class="sxs-lookup"><span data-stu-id="a747c-116">Create hello simulated device app</span></span>
<span data-ttu-id="a747c-117">In questa sezione si crea un'applicazione console Node.js che si connette hub tooyour come **myDeviceId**, in attesa di un aggiornamento della configurazione desiderata e quindi segnala gli aggiornamenti nel processo di aggiornamento configurazione hello simulato.</span><span class="sxs-lookup"><span data-stu-id="a747c-117">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="a747c-118">Creare una nuova cartella vuota denominata **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="a747c-118">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="a747c-119">In hello **simulatedeviceconfiguration** cartella, creare un nuovo file package. JSON utilizzando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="a747c-119">In hello **simulatedeviceconfiguration** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="a747c-120">Accettare tutte le impostazioni predefinite hello.</span><span class="sxs-lookup"><span data-stu-id="a747c-120">Accept all hello defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="a747c-121">Al prompt dei comandi in hello **simulatedeviceconfiguration** cartella, eseguire hello successivo comando tooinstall hello **dispositivi iot di azure** e **azure-iot-dispositivo-mqtt**pacchetti:</span><span class="sxs-lookup"><span data-stu-id="a747c-121">At your command prompt in hello **simulatedeviceconfiguration** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="a747c-122">Utilizzando un editor di testo, creare un nuovo **SimulateDeviceConfiguration.js** file hello **simulatedeviceconfiguration** cartella.</span><span class="sxs-lookup"><span data-stu-id="a747c-122">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in hello **simulatedeviceconfiguration** folder.</span></span>
1. <span data-ttu-id="a747c-123">Aggiungere hello seguente codice toohello **SimulateDeviceConfiguration.js** file e sostituire hello **{stringa di connessione dispositivo}** segnaposto con stringa di connessione dispositivo hello copiato quando si creato hello **myDeviceId** identità del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="a747c-123">Add hello following code toohello **SimulateDeviceConfiguration.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="a747c-124">Hello **Client** oggetto espone tutte hello metodi obbligatorio toointeract con gemelli di dispositivo dal dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="a747c-124">hello **Client** object exposes all hello methods required toointeract with device twins from hello device.</span></span> <span data-ttu-id="a747c-125">Questo codice inizializza hello **Client** oggetto recupera hello gemelli di dispositivo per **myDeviceId**e quindi associa un gestore per l'aggiornamento di hello in *le proprietà desiderate*.</span><span class="sxs-lookup"><span data-stu-id="a747c-125">This code initializes hello **Client** object, retrieves hello device twin for **myDeviceId**, and then attaches a handler for hello update on *desired properties*.</span></span> <span data-ttu-id="a747c-126">gestore Hello verifica che sia presente una richiesta di modifica della configurazione effettiva confrontando configIds hello, quindi richiama un metodo che avvia una modifica della configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="a747c-126">hello handler verifies that there is an actual configuration change request by comparing hello configIds, then invokes a method that starts hello configuration change.</span></span>
   
    <span data-ttu-id="a747c-127">Si noti che per i migliori risultati hello di semplicità, questo codice Usa valore predefinito è hardcoded per la configurazione iniziale di hello.</span><span class="sxs-lookup"><span data-stu-id="a747c-127">Note that for hello sake of simplicity, this code uses a hard-coded default for hello initial configuration.</span></span> <span data-ttu-id="a747c-128">Una vera app probabilmente caricherebbe tale configurazione da una risorsa di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="a747c-128">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="a747c-129">Gli eventi di modifica delle proprietà desiderate vengono inviati sempre una volta sola alla connessione al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a747c-129">Desired property change events are always emitted once at device connection.</span></span> <span data-ttu-id="a747c-130">Assicurarsi che vi sia una modifica effettiva in hello toocheck le proprietà desiderate prima di eseguire qualsiasi azione.</span><span class="sxs-lookup"><span data-stu-id="a747c-130">Make sure toocheck that there is an actual change in hello desired properties before performing any action.</span></span>
   > 
   > 
1. <span data-ttu-id="a747c-131">Aggiungere i seguenti metodi prima hello hello `client.open()` chiamata:</span><span class="sxs-lookup"><span data-stu-id="a747c-131">Add hello following methods before hello `client.open()` invocation:</span></span>
   
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
   
    <span data-ttu-id="a747c-132">Hello **initConfigChange** metodo aggiornamenti hello segnalato le proprietà sull'oggetto di un doppio hello dispositivo locale con la configurazione di hello richiesta e imposta lo stato di hello di aggiornamento troppo**in sospeso**, quindi hello aggiornamenti doppio dispositivo nel servizio hello.</span><span class="sxs-lookup"><span data-stu-id="a747c-132">hello **initConfigChange** method updates hello reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="a747c-133">Dopo aver aggiornato correttamente un doppio dispositivo hello, simula un processo a esecuzione prolungata che termina l'esecuzione di hello **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="a747c-133">After successfully updating hello device twin, it simulates a long running process that terminates in hello execution of **completeConfigChange**.</span></span> <span data-ttu-id="a747c-134">Questo metodo aggiorna hello segnalate le proprietà locali impostazione dello stato di hello troppo**successo** e rimozione di hello **pendingConfig** oggetto.</span><span class="sxs-lookup"><span data-stu-id="a747c-134">This method updates hello local reported properties setting hello status too**Success** and removing hello **pendingConfig** object.</span></span> <span data-ttu-id="a747c-135">Viene quindi aggiornato doppi dispositivo hello sul servizio hello.</span><span class="sxs-lookup"><span data-stu-id="a747c-135">It then updates hello device twin on hello service.</span></span>
   
    <span data-ttu-id="a747c-136">Si noti che, della larghezza di banda toosave segnalati proprietà vengono aggiornate specificando solo hello proprietà toobe modificato (denominato **patch** in hello sopra codice), anziché sostituire hello intero documento.</span><span class="sxs-lookup"><span data-stu-id="a747c-136">Note that, toosave bandwidth, reported properties are updated by specifying only hello properties toobe modified (named **patch** in hello above code), instead of replacing hello whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a747c-137">Questa esercitazione non simula alcun comportamento per gli aggiornamenti della configurazione simultanei.</span><span class="sxs-lookup"><span data-stu-id="a747c-137">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="a747c-138">Alcuni processi di aggiornamento configurazione potrebbero essere in grado di tooaccommodate modifiche della configurazione di destinazione durante l'esecuzione di aggiornamento hello, alcuni potrebbe essere tooqueue mentre altri possibile rifiutarli con una condizione di errore.</span><span class="sxs-lookup"><span data-stu-id="a747c-138">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, some might have tooqueue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="a747c-139">Verificare che tooconsider hello comportamento desiderato per il processo di configurazione specifica e aggiungere la logica appropriata hello prima dell'avvio di modifica della configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="a747c-139">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="a747c-140">Eseguire app per dispositivi hello:</span><span class="sxs-lookup"><span data-stu-id="a747c-140">Run hello device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="a747c-141">Verrà visualizzato il messaggio hello `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="a747c-141">You should see hello message `retrieved device twin`.</span></span> <span data-ttu-id="a747c-142">Mantenere hello app in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a747c-142">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="a747c-143">Creare l'applicazione di servizio hello</span><span class="sxs-lookup"><span data-stu-id="a747c-143">Create hello service app</span></span>
<span data-ttu-id="a747c-144">In questa sezione si creerà un'applicazione console .NET che hello aggiornamenti *le proprietà desiderate* su hello gemelli di dispositivo associati **myDeviceId** con un nuovo oggetto di configurazione di telemetria.</span><span class="sxs-lookup"><span data-stu-id="a747c-144">In this section, you will create a .NET console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="a747c-145">Quindi esegue una query gemelli dispositivo hello archiviate nell'hub IoT hello e Mostra differenza hello tra hello desiderato e le configurazioni di dispositivo hello segnalato.</span><span class="sxs-lookup"><span data-stu-id="a747c-145">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="a747c-146">In Visual Studio, aggiungere una soluzione di Visual c# Windows Desktop classico progetto toohello corrente utilizzando hello **applicazione Console** modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="a747c-146">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="a747c-147">Progetto hello nome **SetDesiredConfigurationAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="a747c-147">Name hello project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Nuovo progetto desktop di Windows classico in Visual C#][img-createapp]
1. <span data-ttu-id="a747c-149">In Esplora soluzioni fare doppio clic su hello **SetDesiredConfigurationAndQuery** del progetto e quindi fare clic su **Gestisci pacchetti NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="a747c-149">In Solution Explorer, right-click hello **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="a747c-150">In hello **Gestione pacchetti NuGet** selezionare **Sfoglia**, cercare **microsoft.azure.devices**selezionare **installare** tooinstall Hello **Microsoft.Azure.Devices** pacchetto e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="a747c-150">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="a747c-151">Questa procedura Scarica, installa e aggiunge un riferimento toohello [SDK di servizi di Azure IoT] [ lnk-nuget-service-sdk] NuGet pacchetto e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="a747c-151">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Finestra Gestione pacchetti NuGet][img-servicenuget]
1. <span data-ttu-id="a747c-153">Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="a747c-153">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="a747c-154">Aggiungere i seguenti campi toohello hello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="a747c-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="a747c-155">Sostituire il valore di segnaposto hello con la stringa di connessione IoT Hub hub hello creato nella sezione precedente hello hello.</span><span class="sxs-lookup"><span data-stu-id="a747c-155">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="a747c-156">Aggiungere hello seguente metodo toohello **programma** classe:</span><span class="sxs-lookup"><span data-stu-id="a747c-156">Add hello following method toohello **Program** class:</span></span>
   
        static private async Task SetDesiredConfigurationAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch = new {
                    properties = new {
                        desired = new {
                            telemetryConfig = new {
                                configId = Guid.NewGuid().ToString(),
                                sendFrequency = "5m"
                            }
                        }
                    }
                };
   
            await registryManager.UpdateTwinAsync(twin.DeviceId, JsonConvert.SerializeObject(patch), twin.ETag);
            Console.WriteLine("Updated desired configuration");
   
            try
            {
                while (true)
                {
                    var query = registryManager.CreateQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'");
                    var results = await query.GetNextAsTwinAsync();
                    foreach (var result in results)
                    {
                        Console.WriteLine("Config report for: {0}", result.DeviceId);
                        Console.WriteLine("Desired telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Desired["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine("Reported telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Reported["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine();
                    }
                    Thread.Sleep(10000);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Exception: {ex.Message}");
            }
        }
   
    <span data-ttu-id="a747c-157">Hello **Registro di sistema** oggetto espone tutte hello metodi obbligatorio toointeract con gemelli di dispositivo dal servizio hello.</span><span class="sxs-lookup"><span data-stu-id="a747c-157">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="a747c-158">Questo codice inizializza hello **Registro di sistema** oggetto recupera hello gemelli di dispositivo per **myDeviceId**e quindi aggiorna le proprietà desiderate con un nuovo oggetto di configurazione di telemetria.</span><span class="sxs-lookup"><span data-stu-id="a747c-158">This code initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="a747c-159">Successivamente, viene eseguita una query gemelli dispositivo hello archiviate nell'hub IoT hello ogni 10 secondi e stampa hello desiderato e segnalate le configurazioni di telemetria.</span><span class="sxs-lookup"><span data-stu-id="a747c-159">After that, it queries hello device twins stored in hello IoT hub every 10 seconds, and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="a747c-160">Fare riferimento toohello [il linguaggio di query di IoT Hub] [ lnk-query] toolearn come rich toogenerate report tra tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="a747c-160">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="a747c-161">Questa applicazione effettua una query dell'hub IoT ogni 10 secondi a scopo illustrativo.</span><span class="sxs-lookup"><span data-stu-id="a747c-161">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="a747c-162">Utilizzare una query toogenerate rivolta all'utente report tra più dispositivi e non toodetect modifiche.</span><span class="sxs-lookup"><span data-stu-id="a747c-162">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="a747c-163">Se la soluzione richiede notifiche in tempo reale degli eventi del dispositivo, usare le [notifiche relative al dispositivo gemello][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="a747c-163">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="a747c-164">Infine, aggiungere hello seguenti righe toohello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="a747c-164">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery().Wait();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. <span data-ttu-id="a747c-165">In Esplora soluzioni hello, aprire hello **progetti di avvio impostato...**  e verificare che hello **azione** per **SetDesiredConfigurationAndQuery** progetto **avviare**.</span><span class="sxs-lookup"><span data-stu-id="a747c-165">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="a747c-166">Compilare la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="a747c-166">Build hello solution.</span></span>
1. <span data-ttu-id="a747c-167">Con **SimulateDeviceConfiguration.js** in esecuzione, eseguire un'applicazione hello .NET da Visual Studio tramite **F5** dovrebbe essere possibile visualizzare hello segnalati configurazione modificare da **successo** troppo**in sospeso** troppo**successo** nuovamente Active nuovo hello frequenza di invio dei cinque minuti invece di 24 ore.</span><span class="sxs-lookup"><span data-stu-id="a747c-167">With **SimulateDeviceConfiguration.js** running, run hello .NET application from Visual Studio using **F5** and you should see hello reported configuration change from **Success** too**Pending** too**Success** again with hello new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Dispositivo configurato correttamente][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="a747c-169">Si verifica un ritardo di backup tooa minuto tra funzionamento del report dispositivo hello e risultato della query hello.</span><span class="sxs-lookup"><span data-stu-id="a747c-169">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="a747c-170">Si tratta di tooenable hello query infrastruttura toowork su larga scala molto elevata.</span><span class="sxs-lookup"><span data-stu-id="a747c-170">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="a747c-171">viste di un doppio di un singolo dispositivo consistenza tooretrieve utilizzano hello **getDeviceTwin** metodo hello **Registro di sistema** classe.</span><span class="sxs-lookup"><span data-stu-id="a747c-171">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="a747c-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a747c-172">Next steps</span></span>
<span data-ttu-id="a747c-173">In questa esercitazione, impostare una configurazione desiderata come *le proprietà desiderate* dalla soluzione hello back-end e ha scritto un toodetect app dispositivo che modificano e simulare un processo di aggiornamento di più passaggi tramite hello segnalato lo stato di creazione di report proprietà.</span><span class="sxs-lookup"><span data-stu-id="a747c-173">In this tutorial, you set a desired configuration as *desired properties* from hello solution back end, and wrote a device app toodetect that change and simulate a multi-step update process reporting its status through hello reported properties.</span></span>

<span data-ttu-id="a747c-174">Hello utilizzare seguenti come risorse toolearn per:</span><span class="sxs-lookup"><span data-stu-id="a747c-174">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="a747c-175">inviare i dati di telemetria dai dispositivi con hello [iniziare con l'IoT Hub] [ lnk-iothub-getstarted] esercitazione</span><span class="sxs-lookup"><span data-stu-id="a747c-175">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="a747c-176">pianificare o eseguire operazioni su grandi set di dispositivi Vedere hello [pianificazione e i processi di broadcast] [ lnk-schedule-jobs] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a747c-176">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="a747c-177">controllare i dispositivi in modo interattivo (ad esempio l'attivazione di una ventola da un'app controllata dall'utente), con hello [utilizzare metodi diretti] [ lnk-methods-tutorial] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a747c-177">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-node-twin-how-to-configure/deviceconfigured.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

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
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-csharp-node-twin-how-to-configure.md#create-the-simulated-device-app
