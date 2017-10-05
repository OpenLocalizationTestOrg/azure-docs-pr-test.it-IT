---
title: Introduzione ai dispositivi gemelli dell'hub IoT di Azure (.NET/Node) | Microsoft Docs
description: Come usare i dispositivi gemelli dell'hub IoT di Azure per aggiungere tag e quindi usare una query dell'hub IoT. Si usa Azure IoT SDK per dispositivi per Node.js per implementare l'app per dispositivo simulato e Azure IoT SDK per servizi per .NET per implementare un'app di servizio che aggiunge i tag ed esegue la query dell'hub IoT.
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: elioda
ms.openlocfilehash: 07797b9159c9b926e9eb47d8864c63048951931a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-device-twins-netnode"></a><span data-ttu-id="9e36c-104">Introduzione ai dispositivi gemelli (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="9e36c-104">Get started with device twins (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="9e36c-105">Con questa esercitazione vengono create un'app console Node.js e un'app console .NET:</span><span class="sxs-lookup"><span data-stu-id="9e36c-105">At the end of this tutorial, you will have a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="9e36c-106">**AddTagsAndQuery.sln**, un'app back-end .NET, che aggiunge tag ed effettua una query dei dispositivi gemelli.</span><span class="sxs-lookup"><span data-stu-id="9e36c-106">**AddTagsAndQuery.sln**, a .NET back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="9e36c-107">**TwinSimulatedDevice.js**, un'app Node.js che simula un dispositivo che si connette all'hub IoT con l'identità del dispositivo creata prima e segnala la condizione della connettività.</span><span class="sxs-lookup"><span data-stu-id="9e36c-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="9e36c-108">L'articolo [Azure IoT SDK][lnk-hub-sdks] contiene informazioni sui componenti Azure IoT SDK che consentono di compilare le app back-end e per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="9e36c-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="9e36c-109">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9e36c-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="9e36c-110">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="9e36c-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="9e36c-111">Node.js 0.10.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="9e36c-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="9e36c-112">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="9e36c-112">An active Azure account.</span></span> <span data-ttu-id="9e36c-113">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="9e36c-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-service-app"></a><span data-ttu-id="9e36c-114">Creare l'app di servizio</span><span class="sxs-lookup"><span data-stu-id="9e36c-114">Create the service app</span></span>
<span data-ttu-id="9e36c-115">In questa sezione si crea un'app console .NET (usando C#) e si aggiungono i metadati della posizione al dispositivo gemello associato a **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="9e36c-115">In this section, you create a .NET console app (using C#) that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="9e36c-116">Viene quindi eseguita una query nei dispositivi gemelli archiviati nell'hub IoT selezionando i dispositivi situati negli Stati Uniti e quindi quelli che segnalano una rete cellulare.</span><span class="sxs-lookup"><span data-stu-id="9e36c-116">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="9e36c-117">In Visual Studio aggiungere un progetto desktop di Windows classico in Visual C# usando il modello di progetto **Applicazione console** .</span><span class="sxs-lookup"><span data-stu-id="9e36c-117">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="9e36c-118">Assegnare al progetto il nome **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="9e36c-118">Name the project **AddTagsAndQuery**.</span></span>
   
    ![Nuovo progetto desktop di Windows classico in Visual C#][img-createapp]
1. <span data-ttu-id="9e36c-120">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **AddTagsAndQuery** e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="9e36c-120">In Solution Explorer, right-click the **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="9e36c-121">Nella finestra **Gestisci pacchetti NuGet** selezionare **Sfoglia** e cercare **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="9e36c-121">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="9e36c-122">Selezionare **Installa** per installare il pacchetto **Microsoft.Azure.Devices** e accettare le condizioni per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="9e36c-122">Select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="9e36c-123">Questa procedura scarica, installa e aggiunge un riferimento al [pacchetto NuGet Azure IoT - SDK per dispositivi][lnk-nuget-service-sdk] e alle relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="9e36c-123">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Finestra Gestione pacchetti NuGet][img-servicenuget]
1. <span data-ttu-id="9e36c-125">Aggiungere le istruzione `using` seguenti all'inizio del file **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="9e36c-125">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="9e36c-126">Aggiungere i campi seguenti alla classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="9e36c-126">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="9e36c-127">Sostituire il valore del segnaposto con la stringa di connessione dell'hub IoT creato nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="9e36c-127">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="9e36c-128">Aggiungere il metodo seguente alla classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="9e36c-128">Add the following method to the **Program** class:</span></span>
   
        public static async Task AddTagsAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch =
                @"{
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                        }
                    }
                }";
            await registryManager.UpdateTwinAsync(twin.DeviceId, patch, twin.ETag);
   
            var query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            var twinsInRedmond43 = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43: {0}", string.Join(", ", twinsInRedmond43.Select(t => t.DeviceId)));
   
            query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            var twinsInRedmond43UsingCellular = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43 using cellular network: {0}", string.Join(", ", twinsInRedmond43UsingCellular.Select(t => t.DeviceId)));
        }
   
    <span data-ttu-id="9e36c-129">L'oggetto **RegistryManager** espone tutti i metodi necessari per interagire con i dispositivi gemelli dal servizio.</span><span class="sxs-lookup"><span data-stu-id="9e36c-129">The **RegistryManager** class exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="9e36c-130">Il codice precedente inizializza prima di tutto l'oggetto **registryManager**, quindi recupera il dispositivo gemello per **myDeviceId** e infine ne aggiorna i tag con le informazioni sulla posizione desiderate.</span><span class="sxs-lookup"><span data-stu-id="9e36c-130">The previous code first initializes the **registryManager** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="9e36c-131">Dopo l'aggiornamento, il codice precedente esegue due query: la prima seleziona solo i dispositivi gemelli tra quelli situati nello stabilimento **Redmond43** e la seconda affina la query per selezionare solo i dispositivi che sono connessi anche tramite la rete cellulare.</span><span class="sxs-lookup"><span data-stu-id="9e36c-131">After updating, it executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="9e36c-132">Si noti che il codice precedente, quando crea l'oggetto **query**, specifica un numero massimo di documenti restituiti.</span><span class="sxs-lookup"><span data-stu-id="9e36c-132">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="9e36c-133">L'oggetto **query** contiene una proprietà booleana **HasMoreResults** che è possibile usare per richiamare i metodi **GetNextAsTwinAsync** più volte per recuperare tutti i risultati.</span><span class="sxs-lookup"><span data-stu-id="9e36c-133">The **query** object contains a **HasMoreResults** boolean property that you can use to invoke the **GetNextAsTwinAsync** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="9e36c-134">Per i risultati che non sono dispositivi gemelli, ad esempio i risultati delle query di aggregazione, è disponibile un metodo chiamato **GetNextAsJson**.</span><span class="sxs-lookup"><span data-stu-id="9e36c-134">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="9e36c-135">Aggiungere infine le righe seguenti al metodo **Main** :</span><span class="sxs-lookup"><span data-stu-id="9e36c-135">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="9e36c-136">In Esplora soluzioni aprire **Imposta progetti di avvio** e assicurarsi che **Azione** per il progetto **AddTagsAndQuery** sia impostata su **Avvio**.</span><span class="sxs-lookup"><span data-stu-id="9e36c-136">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="9e36c-137">Compilare la soluzione.</span><span class="sxs-lookup"><span data-stu-id="9e36c-137">Build the solution.</span></span>
1. <span data-ttu-id="9e36c-138">Eseguire l'applicazione facendo clic con il pulsante destro del mouse sul progetto **AddTagsAndQuery** e selezionando **Debug**, seguito da **Avvia nuova istanza**.</span><span class="sxs-lookup"><span data-stu-id="9e36c-138">Run this application by right-clicking on the **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="9e36c-139">Nei risultati si noterà un dispositivo per la query che cerca tutti i dispositivi situati in **Redmond43** e nessuno per la query che limita i risultati ai dispositivi che usano una rete cellulare.</span><span class="sxs-lookup"><span data-stu-id="9e36c-139">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![Risultati della query nella finestra][img-addtagapp]

<span data-ttu-id="9e36c-141">Nella sezione successiva si crea un'app per dispositivo che segnala le informazioni sulla connettività e modifica il risultato della query nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="9e36c-141">In the next section, you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="9e36c-142">Creare l'app per dispositivo</span><span class="sxs-lookup"><span data-stu-id="9e36c-142">Create the device app</span></span>
<span data-ttu-id="9e36c-143">In questa sezione si crea un'app console Node.js che si connette all'hub come **myDeviceId** e quindi aggiorna le proprietà segnalate per poter contenere le informazioni relative alla connessione usando una rete cellulare.</span><span class="sxs-lookup"><span data-stu-id="9e36c-143">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, and then updates its reported properties to contain the information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="9e36c-144">Creare una nuova cartella vuota denominata **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="9e36c-144">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="9e36c-145">Nella cartella **reportconnectivity** creare un nuovo file package.json immettendo il comando seguente al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="9e36c-145">In the **reportconnectivity** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="9e36c-146">Accettare tutte le impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="9e36c-146">Accept all the defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="9e36c-147">Eseguire questo comando al prompt dei comandi nella cartella **reportconnectivity** per installare i pacchetti **azure-iot-device** e **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="9e36c-147">At your command prompt in the **reportconnectivity** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="9e36c-148">Usando un editor di testo, creare un nuovo file **ReportConnectivity.js** nella cartella **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="9e36c-148">Using a text editor, create a new **ReportConnectivity.js** file in the **reportconnectivity** folder.</span></span>
1. <span data-ttu-id="9e36c-149">Aggiungere il codice seguente al file **ReportConnectivity.js** e sostituire il segnaposto per la stringa di connessione al dispositivo con quello copiato quando è stata creata l'identità del dispositivo **myDeviceId**:</span><span class="sxs-lookup"><span data-stu-id="9e36c-149">Add the following code to the **ReportConnectivity.js** file, and substitute the placeholder for device connection string with the one you copied when you created the **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    <span data-ttu-id="9e36c-150">L'oggetto **Client** espone tutti i metodi necessari per interagire con i dispositivi gemelli dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9e36c-150">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="9e36c-151">Il codice precedente, dopo avere inizializzato l'oggetto **Client**, recupera il dispositivo gemello per **myDeviceId** e aggiorna le proprietà segnalate con le informazioni sulla connettività.</span><span class="sxs-lookup"><span data-stu-id="9e36c-151">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId** and updates its reported property with the connectivity information.</span></span>
1. <span data-ttu-id="9e36c-152">Eseguire l'app per dispositivo</span><span class="sxs-lookup"><span data-stu-id="9e36c-152">Run the device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="9e36c-153">Dovrebbe essere visualizzato il messaggio `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="9e36c-153">You should see the message `twin state reported`.</span></span>
1. <span data-ttu-id="9e36c-154">Ora che il dispositivo ha segnalato le informazioni sulla connettività, verrà visualizzato in entrambe le query.</span><span class="sxs-lookup"><span data-stu-id="9e36c-154">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="9e36c-155">Eseguire l'app .NET **AddTagsAndQuery** per eseguire nuovamente la query.</span><span class="sxs-lookup"><span data-stu-id="9e36c-155">Run the .NET **AddTagsAndQuery** app to run the queries again.</span></span> <span data-ttu-id="9e36c-156">Questa volta **myDeviceId** verrà visualizzato nei risultati di entrambe le query.</span><span class="sxs-lookup"><span data-stu-id="9e36c-156">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][img-addtagapp2]

## <a name="next-steps"></a><span data-ttu-id="9e36c-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9e36c-157">Next steps</span></span>
<span data-ttu-id="9e36c-158">In questa esercitazione è stato configurato un nuovo hub IoT nel Portale di Azure ed è stata quindi creata un'identità del dispositivo nel registro di identità dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9e36c-158">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="9e36c-159">Sono stati aggiunti i metadati del dispositivo come tag da un'app back-end ed è stata scritta un'app per dispositivo simulato per segnalare le informazioni sulla connettività del dispositivo nel dispositivo gemello.</span><span class="sxs-lookup"><span data-stu-id="9e36c-159">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="9e36c-160">Si è anche appreso come effettuare una query di queste informazioni usando il linguaggio di query simile a SQL dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9e36c-160">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="9e36c-161">Per altre informazioni, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="9e36c-161">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="9e36c-162">Per inviare dati di telemetria dai dispositivi, vedere l'esercitazione [Introduzione all'hub IoT][lnk-iothub-getstarted].</span><span class="sxs-lookup"><span data-stu-id="9e36c-162">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="9e36c-163">Per configurare i dispositivi usando le proprietà desiderate del dispositivo gemello, vedere l'esercitazione [Usare le proprietà desiderate per configurare i dispositivi][lnk-twin-how-to-configure].</span><span class="sxs-lookup"><span data-stu-id="9e36c-163">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="9e36c-164">Per controllare i dispositivi in modo interattivo, ad esempio per attivare un ventilatore da un'app controllata dall'utente, vedere l'esercitazione [Use direct methods][lnk-methods-tutorial] (Usare metodi diretti).</span><span class="sxs-lookup"><span data-stu-id="9e36c-164">control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-node-twin-getstarted/addtagapp.png
[img-addtagapp2]: media/iot-hub-csharp-node-twin-getstarted/addtagapp2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

