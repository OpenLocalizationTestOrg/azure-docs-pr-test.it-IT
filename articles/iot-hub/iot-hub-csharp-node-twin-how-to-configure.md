---
title: "Usare le proprietà di un dispositivo gemello dell'hub IoT di Azure (.NET/Node) | Microsoft Docs"
description: "Come usare le proprietà di un dispositivo gemello dell'hub IoT di Azure per configurare dispositivi. Usare Azure IoT SDK per dispositivi per Node.js per implementare un'app per dispositivo simulato e Azure IoT SDK per servizi per .NET per implementare un'app di servizio che modifica la configurazione di un dispositivo usando un dispositivo gemello."
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
ms.openlocfilehash: 78b4523fa7d0c056f84214429730a5df1bcdcef7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-desired-properties-to-configure-devices"></a><span data-ttu-id="bb0d8-104">Usare le proprietà desiderate per configurare i dispositivi</span><span class="sxs-lookup"><span data-stu-id="bb0d8-104">Use desired properties to configure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="bb0d8-105">Al termine di questa esercitazione si avranno due app console:</span><span class="sxs-lookup"><span data-stu-id="bb0d8-105">At the end of this tutorial, you will have two console apps:</span></span>

* <span data-ttu-id="bb0d8-106">**SimulateDeviceConfiguration.js**, un'app per dispositivo simulata che attende un aggiornamento della configurazione desiderata e segnala lo stato di un processo di aggiornamento della configurazione simulata.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports the status of a simulated configuration update process.</span></span>
* <span data-ttu-id="bb0d8-107">**SetDesiredConfigurationAndQuery.js**, un'app back-end di .NET, che imposta la configurazione desiderata in un dispositivo ed esegue query sul processo di aggiornamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-107">**SetDesiredConfigurationAndQuery**, a .NET back-end app, which sets the desired configuration on a device and queries the configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="bb0d8-108">L'articolo [Azure IoT SDK][lnk-hub-sdks] contiene informazioni sui componenti Azure IoT SDK che consentono di compilare le app back-end e per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="bb0d8-109">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb0d8-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="bb0d8-110">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="bb0d8-111">Node.js 0.10.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="bb0d8-112">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-112">An active Azure account.</span></span> <span data-ttu-id="bb0d8-113">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-113">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="bb0d8-114">Se è stata seguita l'esercitazione [Introduzione ai dispositivi gemelli][lnk-twin-tutorial] sono già disponibili un hub IoT e un'identità del dispositivo denominata **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-114">If you followed the [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="bb0d8-115">È quindi possibile ignorare la sezione [Creare l'app per dispositivo simulata][lnk-how-to-configure-createapp].</span><span class="sxs-lookup"><span data-stu-id="bb0d8-115">In that case, you can skip to the [Create the simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-the-simulated-device-app"></a><span data-ttu-id="bb0d8-116">Creare l'app per dispositivo simulata</span><span class="sxs-lookup"><span data-stu-id="bb0d8-116">Create the simulated device app</span></span>
<span data-ttu-id="bb0d8-117">In questa sezione si crea un'app console Node.js che si connette all'hub come **myDeviceId**, attende un aggiornamento della configurazione desiderata e quindi segnala gli aggiornamenti nel processo di aggiornamento della configurazione simulata.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-117">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, waits for a desired configuration update and then reports updates on the simulated configuration update process.</span></span>

1. <span data-ttu-id="bb0d8-118">Creare una nuova cartella vuota denominata **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-118">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="bb0d8-119">Nella cartella **simulatedeviceconfiguration** creare un nuovo file package.json immettendo il comando seguente al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-119">In the **simulatedeviceconfiguration** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="bb0d8-120">Accettare tutte le impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-120">Accept all the defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="bb0d8-121">Al prompt dei comandi nella cartella **simulatedeviceconfiguration** digitare il comando seguente per installare i pacchetti **azure-iot-device** e **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="bb0d8-121">At your command prompt in the **simulatedeviceconfiguration** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="bb0d8-122">Usando un editor di testo, creare un nuovo file **SimulateDeviceConfiguration.js** nella cartella **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-122">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in the **simulatedeviceconfiguration** folder.</span></span>
1. <span data-ttu-id="bb0d8-123">Aggiungere il codice seguente al file **SimulateDeviceConfiguration.js** e sostituire il segnaposto **{device connection string}** con la stringa di connessione copiata quando si è creata l'identità del dispositivo **myDeviceId**:</span><span class="sxs-lookup"><span data-stu-id="bb0d8-123">Add the following code to the **SimulateDeviceConfiguration.js** file, and substitute the **{device connection string}** placeholder with the device connection string you copied when you created the **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="bb0d8-124">L'oggetto **Client** espone tutti i metodi necessari per interagire con i dispositivi gemelli dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-124">The **Client** object exposes all the methods required to interact with device twins from the device.</span></span> <span data-ttu-id="bb0d8-125">Questo codice inizializza l'oggetto **Client**, recupera il dispositivo gemello per **myDeviceId** e quindi collega un gestore per l'aggiornamento nelle *proprietà desiderate*.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-125">This code initializes the **Client** object, retrieves the device twin for **myDeviceId**, and then attaches a handler for the update on *desired properties*.</span></span> <span data-ttu-id="bb0d8-126">Il gestore verifica che esista una richiesta di modifica della configurazione effettiva confrontando gli elementi configId, quindi richiama un metodo che avvia la modifica della configurazione.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-126">The handler verifies that there is an actual configuration change request by comparing the configIds, then invokes a method that starts the configuration change.</span></span>
   
    <span data-ttu-id="bb0d8-127">Per motivi di semplicità, questo codice usa un valore predefinito hardcoded per la configurazione iniziale.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-127">Note that for the sake of simplicity, this code uses a hard-coded default for the initial configuration.</span></span> <span data-ttu-id="bb0d8-128">Una vera app probabilmente caricherebbe tale configurazione da una risorsa di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-128">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="bb0d8-129">Gli eventi di modifica delle proprietà desiderate vengono inviati sempre una volta sola alla connessione al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-129">Desired property change events are always emitted once at device connection.</span></span> <span data-ttu-id="bb0d8-130">Assicurarsi di verificare che vi sia un'effettiva modifica nelle proprietà desiderate prima di eseguire qualsiasi azione.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-130">Make sure to check that there is an actual change in the desired properties before performing any action.</span></span>
   > 
   > 
1. <span data-ttu-id="bb0d8-131">Aggiungere i metodi seguenti prima della chiamata a `client.open()`:</span><span class="sxs-lookup"><span data-stu-id="bb0d8-131">Add the following methods before the `client.open()` invocation:</span></span>
   
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
   
    <span data-ttu-id="bb0d8-132">Il metodo **initConfigChange** aggiorna le proprietà segnalate nell'oggetto dispositivo gemello locale con la richiesta di aggiornamento della configurazione e imposta lo stato su **Pending** (Sospeso), quindi aggiorna il dispositivo gemello nel servizio.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-132">The **initConfigChange** method updates the reported properties on the local device twin object with the configuration update request and sets the status to **Pending**, then updates the device twin on the service.</span></span> <span data-ttu-id="bb0d8-133">Dopo l'aggiornamento del dispositivo gemello, simula un processo a esecuzione prolungata che termina con l'esecuzione di **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-133">After successfully updating the device twin, it simulates a long running process that terminates in the execution of **completeConfigChange**.</span></span> <span data-ttu-id="bb0d8-134">Questo metodo aggiorna le proprietà segnalate locali impostando lo stato su **Success** e rimuovendo l'oggetto **pendingConfig**,</span><span class="sxs-lookup"><span data-stu-id="bb0d8-134">This method updates the local reported properties setting the status to **Success** and removing the **pendingConfig** object.</span></span> <span data-ttu-id="bb0d8-135">quindi aggiorna il dispositivo gemello nel servizio.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-135">It then updates the device twin on the service.</span></span>
   
    <span data-ttu-id="bb0d8-136">Si noti che, per risparmiare larghezza di banda, le proprietà segnalate vengono aggiornate specificando solo le proprietà da modificare (denominate **patch** nel codice precedente), invece di sostituire l'intero documento.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-136">Note that, to save bandwidth, reported properties are updated by specifying only the properties to be modified (named **patch** in the above code), instead of replacing the whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bb0d8-137">Questa esercitazione non simula alcun comportamento per gli aggiornamenti della configurazione simultanei.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-137">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="bb0d8-138">Alcuni processi di aggiornamento della configurazione potrebbero consentire modifiche della configurazione di destinazione mentre l'aggiornamento è in esecuzione, altre potrebbero doverle accodare e altri ancora rifiutarle con una condizione di errore.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-138">Some configuration update processes might be able to accommodate changes of target configuration while the update is running, some might have to queue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="bb0d8-139">È importante tenere in considerazione il comportamento desiderato per il processo di configurazione specifico e aggiungere la logica appropriata prima di iniziare la modifica della configurazione.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-139">Make sure to consider the desired behavior for your specific configuration process, and add the appropriate logic before initiating the configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="bb0d8-140">Eseguire l'app per dispositivo:</span><span class="sxs-lookup"><span data-stu-id="bb0d8-140">Run the device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="bb0d8-141">Dovrebbe essere visualizzato il messaggio `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-141">You should see the message `retrieved device twin`.</span></span> <span data-ttu-id="bb0d8-142">Mantenere l'app in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-142">Keep the app running.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="bb0d8-143">Creare l'app di servizio</span><span class="sxs-lookup"><span data-stu-id="bb0d8-143">Create the service app</span></span>
<span data-ttu-id="bb0d8-144">In questa sezione si creerà un'app console .NET che aggiorna le *proprietà desiderate* nel dispositivo gemello associato a **myDeviceId** con un nuovo oggetto di configurazione di telemetria.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-144">In this section, you will create a .NET console app that updates the *desired properties* on the device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="bb0d8-145">Viene quindi effettuata una query dei dispositivi gemelli archiviati nell'hub IoT e viene visualizzata la differenza tra la configurazione desiderata e quella segnalata del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-145">It then queries the device twins stored in the IoT hub and shows the difference between the desired and reported configurations of the device.</span></span>

1. <span data-ttu-id="bb0d8-146">In Visual Studio aggiungere un progetto desktop di Windows classico in Visual C# usando il modello di progetto **Applicazione console** .</span><span class="sxs-lookup"><span data-stu-id="bb0d8-146">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="bb0d8-147">Assegnare al progetto il nome **SetDesiredConfigurationAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-147">Name the project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Nuovo progetto desktop di Windows classico in Visual C#][img-createapp]
1. <span data-ttu-id="bb0d8-149">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **SetDesiredConfigurationAndQuery** e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-149">In Solution Explorer, right-click the **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="bb0d8-150">Nella finestra **Gestione pacchetti NuGet** selezionare **Esplora**, cercare **microsoft.azure.devices**, selezionare **Installa** per installare il pacchetto **Microsoft.Azure.Devices** e accettare le condizioni per l'uso.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-150">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="bb0d8-151">Questa procedura scarica, installa e aggiunge un riferimento al [pacchetto NuGet Azure IoT - SDK per dispositivi][lnk-nuget-service-sdk] e alle relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-151">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Finestra Gestione pacchetti NuGet][img-servicenuget]
1. <span data-ttu-id="bb0d8-153">Aggiungere le istruzione `using` seguenti all'inizio del file **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="bb0d8-153">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="bb0d8-154">Aggiungere i campi seguenti alla classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="bb0d8-154">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="bb0d8-155">Sostituire il valore del segnaposto con la stringa di connessione dell'hub IoT creato nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-155">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="bb0d8-156">Aggiungere il metodo seguente alla classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="bb0d8-156">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="bb0d8-157">L'oggetto **Registry** espone tutti i metodi necessari per interagire con i dispositivi gemelli dal servizio.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-157">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="bb0d8-158">Questo codice inizializza l'oggetto **Registry**, recupera il dispositivo gemello per **myDeviceId** e ne aggiorna le proprietà desiderate con un nuovo oggetto di configurazione dei dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-158">This code initializes the **Registry** object, retrieves the device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="bb0d8-159">Ogni 10 secondi esegue una query dei dispositivi gemelli archiviati nell'hub IoT e stampa le configurazioni dei dati di telemetria desiderate e segnalate.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-159">After that, it queries the device twins stored in the IoT hub every 10 seconds, and prints the desired and reported telemetry configurations.</span></span> <span data-ttu-id="bb0d8-160">Vedere il [linguaggio di query dell'hub IoT][lnk-query] per informazioni su come generare report avanzati in tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-160">Refer to the [IoT Hub query language][lnk-query] to learn how to generate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="bb0d8-161">Questa applicazione effettua una query dell'hub IoT ogni 10 secondi a scopo illustrativo.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-161">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="bb0d8-162">Usare le query per generare i report destinati all'utente in più dispositivi e non per rilevare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-162">Use queries to generate user-facing reports across many devices, and not to detect changes.</span></span> <span data-ttu-id="bb0d8-163">Se la soluzione richiede notifiche in tempo reale degli eventi del dispositivo, usare le [notifiche relative al dispositivo gemello][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="bb0d8-163">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="bb0d8-164">Aggiungere infine le righe seguenti al metodo **Main** :</span><span class="sxs-lookup"><span data-stu-id="bb0d8-164">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery().Wait();
        Console.WriteLine("Press any key to quit.");
        Console.ReadLine();
1. <span data-ttu-id="bb0d8-165">In Esplora soluzioni aprire **Imposta progetti di avvio** e assicurarsi che **Azione** per il progetto **SetDesiredConfigurationAndQuery** sia impostata su **Avvio**.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-165">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="bb0d8-166">Compilare la soluzione.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-166">Build the solution.</span></span>
1. <span data-ttu-id="bb0d8-167">Mentre **SimulateDeviceConfiguration.js** è in esecuzione, eseguire l'applicazione .NET da Visual Studio tramite **F5**: si potrà notare che la configurazione segnalata passa da **Operazione riuscita** a **In sospeso** e di nuovo a **Operazione riuscita** con la nuova frequenza di invio attiva di cinque minuti e non più di 24 ore.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-167">With **SimulateDeviceConfiguration.js** running, run the .NET application from Visual Studio using **F5** and you should see the reported configuration change from **Success** to **Pending** to **Success** again with the new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Dispositivo configurato correttamente][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="bb0d8-169">Tra l'operazione relativa al report del dispositivo e il risultato della query si verifica un ritardo fino a un minuto,</span><span class="sxs-lookup"><span data-stu-id="bb0d8-169">There is a delay of up to a minute between the device report operation and the query result.</span></span> <span data-ttu-id="bb0d8-170">che consente all'infrastruttura della query di funzionare su una scala molto ampia.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-170">This is to enable the query infrastructure to work at very high scale.</span></span> <span data-ttu-id="bb0d8-171">Per recuperare visualizzazioni coerenti di un solo dispositivo gemello, usare il metodo **getDeviceTwin** nella classe **Registry**.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-171">To retrieve consistent views of a single device twin use the **getDeviceTwin** method in the **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="bb0d8-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bb0d8-172">Next steps</span></span>
<span data-ttu-id="bb0d8-173">In questa esercitazione è stata impostata una configurazione desiderata come *proprietà desiderate* da un back-end della soluzione ed è stata scritta un'app per dispositivo per rilevare tale modifica e simulare un processo di aggiornamento in più fasi che segnala lo stato tramite le proprietà segnalate.</span><span class="sxs-lookup"><span data-stu-id="bb0d8-173">In this tutorial, you set a desired configuration as *desired properties* from the solution back end, and wrote a device app to detect that change and simulate a multi-step update process reporting its status through the reported properties.</span></span>

<span data-ttu-id="bb0d8-174">Per altre informazioni, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb0d8-174">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="bb0d8-175">Per inviare dati di telemetria dai dispositivi, vedere l'esercitazione [Introduzione all'hub IoT][lnk-iothub-getstarted].</span><span class="sxs-lookup"><span data-stu-id="bb0d8-175">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="bb0d8-176">Per pianificare o eseguire operazioni su grandi set di dispositivi, vedere l'esercitazione [Pianificare e trasmettere processi][lnk-schedule-jobs].</span><span class="sxs-lookup"><span data-stu-id="bb0d8-176">schedule or perform operations on large sets of devices see the [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="bb0d8-177">Per controllare i dispositivi in modo interattivo, ad esempio per attivare un ventilatore da un'app controllata dall'utente, vedere l'esercitazione [Use direct methods][lnk-methods-tutorial] (Usare metodi diretti).</span><span class="sxs-lookup"><span data-stu-id="bb0d8-177">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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
