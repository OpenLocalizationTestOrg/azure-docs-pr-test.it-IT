---
title: aaaGet introduttiva gemelli dispositivi Azure IoT Hub (.NET/nodo) | Documenti Microsoft
description: "Modalità toouse IoT Hub Azure dispositivo gemelli tooadd tag e quindi utilizzare una query di IoT Hub. Utilizzare il dispositivo di Azure IoT hello SDK per Node.js tooimplement hello dispositivo simulato app e il servizio di IoT di Azure SDK per .NET tooimplement un'applicazione di servizio che consente di aggiungere tag hello ed esegue query IoT Hub hello hello."
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
ms.openlocfilehash: 1cec082ebddc19c9b87998a5fd0159d32b07acd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnode"></a><span data-ttu-id="e1615-104">Introduzione ai dispositivi gemelli (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="e1615-104">Get started with device twins (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="e1615-105">Alla fine di hello di questa esercitazione, si avrà un .NET e un'applicazione console in Node.js:</span><span class="sxs-lookup"><span data-stu-id="e1615-105">At hello end of this tutorial, you will have a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="e1615-106">**AddTagsAndQuery.sln**, un'app back-end .NET, che aggiunge tag ed effettua una query dei dispositivi gemelli.</span><span class="sxs-lookup"><span data-stu-id="e1615-106">**AddTagsAndQuery.sln**, a .NET back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="e1615-107">**TwinSimulatedDevice.js**, un'app Node.js che simula un dispositivo che si connette l'hub IoT tooyour con l'identità del dispositivo hello creato in precedenza e segnala la condizione di connettività.</span><span class="sxs-lookup"><span data-stu-id="e1615-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="e1615-108">articolo Hello [Azure IoT SDK] [ lnk-hub-sdks] fornisce informazioni su Azure IoT SDK hello che è possibile utilizzare toobuild applicazioni back-end sia sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e1615-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="e1615-109">toocomplete questa esercitazione è necessario hello segue:</span><span class="sxs-lookup"><span data-stu-id="e1615-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="e1615-110">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="e1615-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="e1615-111">Node.js 0.10.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="e1615-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="e1615-112">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="e1615-112">An active Azure account.</span></span> <span data-ttu-id="e1615-113">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="e1615-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a><span data-ttu-id="e1615-114">Creare l'applicazione di servizio hello</span><span class="sxs-lookup"><span data-stu-id="e1615-114">Create hello service app</span></span>
<span data-ttu-id="e1615-115">In questa sezione si crea una console app .NET (tramite c#) che aggiunge un doppio dispositivo toohello metadati posizione associato a **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="e1615-115">In this section, you create a .NET console app (using C#) that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="e1615-116">Viene quindi gemelli dispositivo hello archiviate nell'hub IoT hello selezionando dispositivi hello che si trovano in hello ci le query e quindi hello quelle che ha segnalato una connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="e1615-116">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="e1615-117">In Visual Studio, aggiungere una soluzione di Visual c# Windows Desktop classico progetto toohello corrente utilizzando hello **applicazione Console** modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="e1615-117">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="e1615-118">Progetto hello nome **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="e1615-118">Name hello project **AddTagsAndQuery**.</span></span>
   
    ![Nuovo progetto desktop di Windows classico in Visual C#][img-createapp]
1. <span data-ttu-id="e1615-120">In Esplora soluzioni fare doppio clic su hello **AddTagsAndQuery** del progetto e quindi fare clic su **Gestisci pacchetti NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="e1615-120">In Solution Explorer, right-click hello **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="e1615-121">In hello **Gestione pacchetti NuGet** selezionare **Sfoglia** e cercare **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="e1615-121">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="e1615-122">Selezionare **installare** tooinstall hello **Microsoft.Azure.Devices** pacchetto e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="e1615-122">Select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="e1615-123">Questa procedura Scarica, installa e aggiunge un riferimento toohello [SDK di servizi di Azure IoT] [ lnk-nuget-service-sdk] NuGet pacchetto e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="e1615-123">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Finestra Gestione pacchetti NuGet][img-servicenuget]
1. <span data-ttu-id="e1615-125">Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="e1615-125">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="e1615-126">Aggiungere i seguenti campi toohello hello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="e1615-126">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="e1615-127">Sostituire il valore di segnaposto hello con la stringa di connessione IoT Hub hub hello creato nella sezione precedente hello hello.</span><span class="sxs-lookup"><span data-stu-id="e1615-127">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="e1615-128">Aggiungere hello seguente metodo toohello **programma** classe:</span><span class="sxs-lookup"><span data-stu-id="e1615-128">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="e1615-129">Hello **RegistryManager** classe espone tutte hello metodi obbligatorio toointeract con gemelli di dispositivo dal servizio hello.</span><span class="sxs-lookup"><span data-stu-id="e1615-129">hello **RegistryManager** class exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="e1615-130">codice precedente Hello inizializza innanzitutto hello **registryManager** dell'oggetto, quindi recupera hello gemelli di dispositivo per **myDeviceId**e infine gli aggiornamenti relativi tag con le informazioni sul percorso hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="e1615-130">hello previous code first initializes hello **registryManager** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="e1615-131">Dopo l'aggiornamento, vengono eseguite due query: hello dapprima selezionati solo i gemelli dispositivo hello di dispositivi che si trovano in hello **Redmond43** impianto e hello secondo perfeziona hello query tooselect solo hello dispositivi connessi anche tramite rete cellulare.</span><span class="sxs-lookup"><span data-stu-id="e1615-131">After updating, it executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="e1615-132">Si noti il codice precedente hello, durante la creazione di hello **query** dell'oggetto, specifica un numero massimo di documenti restituiti dalla query.</span><span class="sxs-lookup"><span data-stu-id="e1615-132">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="e1615-133">Hello **query** oggetto contiene un **HasMoreResults** proprietà booleana che è possibile utilizzare hello tooinvoke **GetNextAsTwinAsync** metodi più volte tooretrieve tutti risultati.</span><span class="sxs-lookup"><span data-stu-id="e1615-133">hello **query** object contains a **HasMoreResults** boolean property that you can use tooinvoke hello **GetNextAsTwinAsync** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="e1615-134">Per i risultati che non sono dispositivi gemelli, ad esempio i risultati delle query di aggregazione, è disponibile un metodo chiamato **GetNextAsJson**.</span><span class="sxs-lookup"><span data-stu-id="e1615-134">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="e1615-135">Infine, aggiungere hello seguenti righe toohello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="e1615-135">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="e1615-136">In Esplora soluzioni hello, aprire hello **progetti di avvio impostato...**  e verificare che hello **azione** per **AddTagsAndQuery** progetto **avviare**.</span><span class="sxs-lookup"><span data-stu-id="e1615-136">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="e1615-137">Compilare la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="e1615-137">Build hello solution.</span></span>
1. <span data-ttu-id="e1615-138">Eseguire l'applicazione facendo clic su hello **AddTagsAndQuery** progetto, quindi selezionando **Debug**, seguito da **Avvia nuova istanza**.</span><span class="sxs-lookup"><span data-stu-id="e1615-138">Run this application by right-clicking on hello **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="e1615-139">Dovrebbe essere un dispositivo nei risultati di hello per hello porre query per tutti i dispositivi si trovano in **Redmond43** e none per query hello che limita hello risultati toodevices che utilizzano una rete cellulare.</span><span class="sxs-lookup"><span data-stu-id="e1615-139">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![Risultati della query nella finestra][img-addtagapp]

<span data-ttu-id="e1615-141">Nella sezione successiva hello, si crea un'app per dispositivi vengono fornite informazioni di connettività hello e modifiche hello risultati di query hello nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="e1615-141">In hello next section, you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="e1615-142">Creare app per dispositivi hello</span><span class="sxs-lookup"><span data-stu-id="e1615-142">Create hello device app</span></span>
<span data-ttu-id="e1615-143">In questa sezione si crea un'applicazione console Node.js che si connette hub tooyour come **myDeviceId**e quindi aggiorna le informazioni di hello toocontain segnalate le proprietà che è connesso tramite una rete cellulare.</span><span class="sxs-lookup"><span data-stu-id="e1615-143">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, and then updates its reported properties toocontain hello information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="e1615-144">Creare una nuova cartella vuota denominata **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="e1615-144">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="e1615-145">In hello **reportconnectivity** cartella, creare un nuovo file package. JSON utilizzando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="e1615-145">In hello **reportconnectivity** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="e1615-146">Accettare tutte le impostazioni predefinite hello.</span><span class="sxs-lookup"><span data-stu-id="e1615-146">Accept all hello defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="e1615-147">Al prompt dei comandi in hello **reportconnectivity** cartella, eseguire hello successivo comando tooinstall hello **dispositivi iot di azure**, e **mqtt azure-iot-dispositivo** pacchetto :</span><span class="sxs-lookup"><span data-stu-id="e1615-147">At your command prompt in hello **reportconnectivity** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="e1615-148">Utilizzando un editor di testo, creare un nuovo **ReportConnectivity.js** file hello **reportconnectivity** cartella.</span><span class="sxs-lookup"><span data-stu-id="e1615-148">Using a text editor, create a new **ReportConnectivity.js** file in hello **reportconnectivity** folder.</span></span>
1. <span data-ttu-id="e1615-149">Aggiungere i seguenti toohello codice hello **ReportConnectivity.js** file e sostituire il segnaposto hello per la stringa di connessione dispositivo con hello uno è stato copiato al momento della creazione hello **myDeviceId** dispositivo identità:</span><span class="sxs-lookup"><span data-stu-id="e1615-149">Add hello following code toohello **ReportConnectivity.js** file, and substitute hello placeholder for device connection string with hello one you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="e1615-150">Hello **Client** oggetto espone tutti i metodi di hello desiderate toointeract con gemelli di dispositivo dal dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="e1615-150">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="e1615-151">Hello codice precedente, dopo l'inizializzazione hello **Client** oggetto recupera hello gemelli di dispositivo per **myDeviceId** e aggiorna la proprietà segnalata con informazioni sulla connettività hello.</span><span class="sxs-lookup"><span data-stu-id="e1615-151">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId** and updates its reported property with hello connectivity information.</span></span>
1. <span data-ttu-id="e1615-152">Eseguire app dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="e1615-152">Run hello device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="e1615-153">Verrà visualizzato il messaggio hello `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="e1615-153">You should see hello message `twin state reported`.</span></span>
1. <span data-ttu-id="e1615-154">Ora che hello dispositivo segnalato le informazioni di connettività, viene visualizzato in entrambe le query.</span><span class="sxs-lookup"><span data-stu-id="e1615-154">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="e1615-155">Eseguire .NET hello **AddTagsAndQuery** hello toorun app nuovamente una query.</span><span class="sxs-lookup"><span data-stu-id="e1615-155">Run hello .NET **AddTagsAndQuery** app toorun hello queries again.</span></span> <span data-ttu-id="e1615-156">Questa volta **myDeviceId** verrà visualizzato nei risultati di entrambe le query.</span><span class="sxs-lookup"><span data-stu-id="e1615-156">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][img-addtagapp2]

## <a name="next-steps"></a><span data-ttu-id="e1615-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e1615-157">Next steps</span></span>
<span data-ttu-id="e1615-158">In questa esercitazione, è configurato un nuovo hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità.</span><span class="sxs-lookup"><span data-stu-id="e1615-158">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="e1615-159">Aggiunti i metadati del dispositivo come tag da un'app di back-end e ha scritto informazioni di connettività un dispositivo simulato app tooreport dispositivo in un doppio dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="e1615-159">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="e1615-160">È inoltre appreso tooquery queste informazioni usando il linguaggio di query di hello IoT Hub simile a SQL.</span><span class="sxs-lookup"><span data-stu-id="e1615-160">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="e1615-161">Hello utilizzare seguenti come risorse toolearn per:</span><span class="sxs-lookup"><span data-stu-id="e1615-161">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="e1615-162">inviare i dati di telemetria dai dispositivi con hello [iniziare con l'IoT Hub] [ lnk-iothub-getstarted] esercitazione</span><span class="sxs-lookup"><span data-stu-id="e1615-162">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="e1615-163">configurare i dispositivi con le proprietà desiderate di un doppio dispositivo hello [lo si desidera utilizzare i dispositivi di proprietà tooconfigure] [ lnk-twin-how-to-configure] esercitazione</span><span class="sxs-lookup"><span data-stu-id="e1615-163">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="e1615-164">controllare i dispositivi in modo interattivo (ad esempio l'attivazione di una ventola da un'app controllata dall'utente) con hello [utilizzare metodi diretti] [ lnk-methods-tutorial] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="e1615-164">control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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

