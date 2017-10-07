---
title: aaaGet introduttiva gemelli dispositivi Azure IoT Hub (.NET/.NET) | Documenti Microsoft
description: "Modalità toouse IoT Hub Azure dispositivo gemelli tooadd tag e quindi utilizzare una query di IoT Hub. Usare il dispositivo di Azure IoT hello SDK per .NET tooimplement hello dispositivo simulato app e il servizio di IoT di Azure SDK per .NET tooimplement un'applicazione di servizio che consente di aggiungere tag hello ed esegue query IoT Hub hello hello."
services: iot-hub
documentationcenter: node
author: dsk-2015
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: dkshir
ms.openlocfilehash: 7fa73ac896c44e79c6522d252cd1515bd6e7bb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnet"></a><span data-ttu-id="4018a-104">Introduzione ai dispositivi gemelli (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="4018a-104">Get started with device twins (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="4018a-105">Alla fine di hello di questa esercitazione, sarà necessario queste App console .NET:</span><span class="sxs-lookup"><span data-stu-id="4018a-105">At hello end of this tutorial, you will have these .NET console apps:</span></span>

* <span data-ttu-id="4018a-106">**CreateDeviceIdentity**, un'app .NET che crea un'identità del dispositivo e protezione della chiave tooconnect app dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="4018a-106">**CreateDeviceIdentity**, a .NET app which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="4018a-107">**AddTagsAndQuery**, un'app back-end .NET, che aggiunge tag ed effettua una query dei dispositivi gemelli.</span><span class="sxs-lookup"><span data-stu-id="4018a-107">**AddTagsAndQuery**, a .NET back-end app which adds tags and queries device twins.</span></span>
* <span data-ttu-id="4018a-108">**ReportConnectivity**, un'app di dispositivo .NET che simula un dispositivo che si connette l'hub IoT tooyour con l'identità del dispositivo hello creato in precedenza e segnala la condizione di connettività.</span><span class="sxs-lookup"><span data-stu-id="4018a-108">**ReportConnectivity**, a .NET device app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="4018a-109">articolo Hello [Azure IoT SDK] [ lnk-hub-sdks] fornisce informazioni su Azure IoT SDK hello che è possibile utilizzare toobuild applicazioni back-end sia sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4018a-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="4018a-110">toocomplete questa esercitazione è necessario hello segue:</span><span class="sxs-lookup"><span data-stu-id="4018a-110">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="4018a-111">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="4018a-111">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="4018a-112">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="4018a-112">An active Azure account.</span></span> <span data-ttu-id="4018a-113">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="4018a-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="4018a-114">Se si desidera l'identità del dispositivo hello toocreate a livello di codice in alternativa, leggere una sezione corrispondente di hello in hello [connessione hub IoT tooyour dispositivo simulato utilizzando .NET] [ lnk-device-identity-csharp] articolo.</span><span class="sxs-lookup"><span data-stu-id="4018a-114">If you want toocreate hello device identity programmatically instead, read hello corresponding section in hello [Connect your simulated device tooyour IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="4018a-115">Creare l'applicazione di servizio hello</span><span class="sxs-lookup"><span data-stu-id="4018a-115">Create hello service app</span></span>
<span data-ttu-id="4018a-116">In questa sezione si crea una console app .NET (tramite c#) che aggiunge un doppio dispositivo toohello metadati posizione associato a **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="4018a-116">In this section, you create a .NET console app (using C#) that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="4018a-117">Viene quindi gemelli dispositivo hello archiviate nell'hub IoT hello selezionando dispositivi hello che si trovano in hello ci le query e quindi hello quelle che ha segnalato una connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="4018a-117">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="4018a-118">In Visual Studio, aggiungere una soluzione di Visual c# Windows Desktop classico progetto toohello corrente utilizzando hello **applicazione Console** modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="4018a-118">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="4018a-119">Progetto hello nome **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="4018a-119">Name hello project **AddTagsAndQuery**.</span></span>
   
    ![Nuovo progetto desktop di Windows classico in Visual C#][img-createapp]
1. <span data-ttu-id="4018a-121">In Esplora soluzioni fare doppio clic su hello **AddTagsAndQuery** del progetto e quindi fare clic su **Gestisci pacchetti NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="4018a-121">In Solution Explorer, right-click hello **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="4018a-122">In hello **Gestione pacchetti NuGet** selezionare **Sfoglia** e cercare **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="4018a-122">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="4018a-123">Selezionare **installare** tooinstall hello **Microsoft.Azure.Devices** pacchetto e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="4018a-123">Select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="4018a-124">Questa procedura Scarica, installa e aggiunge un riferimento toohello [SDK di servizi di Azure IoT] [ lnk-nuget-service-sdk] NuGet pacchetto e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="4018a-124">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Finestra Gestione pacchetti NuGet][img-servicenuget]
1. <span data-ttu-id="4018a-126">Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="4018a-126">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="4018a-127">Aggiungere i seguenti campi toohello hello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="4018a-127">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="4018a-128">Sostituire il valore di segnaposto hello con la stringa di connessione IoT Hub hub hello creato nella sezione precedente hello hello.</span><span class="sxs-lookup"><span data-stu-id="4018a-128">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="4018a-129">Aggiungere hello seguente metodo toohello **programma** classe:</span><span class="sxs-lookup"><span data-stu-id="4018a-129">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="4018a-130">Hello **RegistryManager** classe espone tutte hello metodi obbligatorio toointeract con gemelli di dispositivo dal servizio hello.</span><span class="sxs-lookup"><span data-stu-id="4018a-130">hello **RegistryManager** class exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="4018a-131">codice precedente Hello inizializza innanzitutto hello **registryManager** dell'oggetto, quindi recupera hello gemelli di dispositivo per **myDeviceId**e infine gli aggiornamenti relativi tag con le informazioni sul percorso hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="4018a-131">hello previous code first initializes hello **registryManager** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="4018a-132">Dopo l'aggiornamento, vengono eseguite due query: hello dapprima selezionati solo i gemelli dispositivo hello di dispositivi che si trovano in hello **Redmond43** impianto e hello secondo perfeziona hello query tooselect solo hello dispositivi connessi anche tramite rete cellulare.</span><span class="sxs-lookup"><span data-stu-id="4018a-132">After updating, it executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="4018a-133">Si noti il codice precedente hello, durante la creazione di hello **query** dell'oggetto, specifica un numero massimo di documenti restituiti dalla query.</span><span class="sxs-lookup"><span data-stu-id="4018a-133">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="4018a-134">Hello **query** oggetto contiene un **HasMoreResults** proprietà booleana che è possibile utilizzare hello tooinvoke **GetNextAsTwinAsync** metodi più volte tooretrieve tutti risultati.</span><span class="sxs-lookup"><span data-stu-id="4018a-134">hello **query** object contains a **HasMoreResults** boolean property that you can use tooinvoke hello **GetNextAsTwinAsync** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="4018a-135">Per i risultati che non sono dispositivi gemelli, ad esempio i risultati delle query di aggregazione, è disponibile un metodo chiamato **GetNextAsJson**.</span><span class="sxs-lookup"><span data-stu-id="4018a-135">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="4018a-136">Infine, aggiungere hello seguenti righe toohello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="4018a-136">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="4018a-137">In Esplora soluzioni hello, aprire hello **progetti di avvio impostato...**  e verificare che hello **azione** per **AddTagsAndQuery** progetto **avviare**.</span><span class="sxs-lookup"><span data-stu-id="4018a-137">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="4018a-138">Compilare la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="4018a-138">Build hello solution.</span></span>
1. <span data-ttu-id="4018a-139">Eseguire l'applicazione facendo clic su hello **AddTagsAndQuery** progetto, quindi selezionando **Debug**, seguito da **Avvia nuova istanza**.</span><span class="sxs-lookup"><span data-stu-id="4018a-139">Run this application by right-clicking on hello **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="4018a-140">Dovrebbe essere un dispositivo nei risultati di hello per hello porre query per tutti i dispositivi si trovano in **Redmond43** e none per query hello che limita hello risultati toodevices che utilizzano una rete cellulare.</span><span class="sxs-lookup"><span data-stu-id="4018a-140">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![Risultati della query nella finestra][img-addtagapp]

<span data-ttu-id="4018a-142">Nella sezione successiva hello, si crea un'app per dispositivi vengono fornite informazioni di connettività hello e modifiche hello risultati di query hello nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="4018a-142">In hello next section, you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="4018a-143">Creare app per dispositivi hello</span><span class="sxs-lookup"><span data-stu-id="4018a-143">Create hello device app</span></span>
<span data-ttu-id="4018a-144">In questa sezione si crea un'applicazione console .NET che si connette hub tooyour come **myDeviceId**e quindi aggiorna le informazioni di hello toocontain segnalate le proprietà che è connesso tramite una rete cellulare.</span><span class="sxs-lookup"><span data-stu-id="4018a-144">In this section, you create a .NET console app that connects tooyour hub as **myDeviceId**, and then updates its reported properties toocontain hello information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="4018a-145">In Visual Studio, aggiungere una soluzione di Visual c# Windows Desktop classico progetto toohello corrente utilizzando hello **applicazione Console** modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="4018a-145">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="4018a-146">Progetto hello nome **ReportConnectivity**.</span><span class="sxs-lookup"><span data-stu-id="4018a-146">Name hello project **ReportConnectivity**.</span></span>
   
    ![Nuova app per il dispositivo di Windows classico in Visual C#][img-createdeviceapp]
    
1. <span data-ttu-id="4018a-148">In Esplora soluzioni fare doppio clic su hello **ReportConnectivity** del progetto e quindi fare clic su **Gestisci pacchetti NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="4018a-148">In Solution Explorer, right-click hello **ReportConnectivity** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="4018a-149">In hello **Gestione pacchetti NuGet** selezionare **Sfoglia** e cercare **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="4018a-149">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="4018a-150">Selezionare **installare** tooinstall hello **Microsoft.Azure.Devices.Client** pacchetto e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="4018a-150">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="4018a-151">Questa procedura Scarica, installa e aggiunge un riferimento toohello [dispositivo IoT di Azure SDK] [ lnk-nuget-client-sdk] NuGet pacchetto e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="4018a-151">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![App client della finestra Gestione pacchetti NuGet][img-clientnuget]
1. <span data-ttu-id="4018a-153">Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="4018a-153">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="4018a-154">Aggiungere i seguenti campi toohello hello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="4018a-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="4018a-155">Sostituire il valore di segnaposto hello con stringa di connessione hello dispositivo che si è preso nota nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="4018a-155">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="4018a-156">Aggiungere hello seguente metodo toohello **programma** classe:</span><span class="sxs-lookup"><span data-stu-id="4018a-156">Add hello following method toohello **Program** class:</span></span>

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
                Console.WriteLine("Retrieving twin");
                await Client.GetTwinAsync();
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    <span data-ttu-id="4018a-157">Hello **Client** oggetto espone tutti i metodi di hello desiderate toointeract con gemelli di dispositivo dal dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="4018a-157">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="4018a-158">Hello codice illustrato in precedenza, inizializza hello **Client** oggetto, quindi recupera hello dispositivo doppi per **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="4018a-158">hello code shown above, initializes hello **Client** object, and then retrieves hello device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="4018a-159">Aggiungere hello seguente metodo toohello **programma** classe:</span><span class="sxs-lookup"><span data-stu-id="4018a-159">Add hello following method toohello **Program** class:</span></span>
   
        public static async void ReportConnectivity()
        {
            try
            {
                Console.WriteLine("Sending connectivity data as reported property");
                
                TwinCollection reportedProperties, connectivity;
                reportedProperties = new TwinCollection();
                connectivity = new TwinCollection();
                connectivity["type"] = "cellular";
                reportedProperties["connectivity"] = connectivity;
                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

   <span data-ttu-id="4018a-160">Hello codice sopra aggiornamenti **myDeviceId**del segnalati proprietà con informazioni sulla connettività hello.</span><span class="sxs-lookup"><span data-stu-id="4018a-160">hello code above updates **myDeviceId**'s reported property with hello connectivity information.</span></span>

1. <span data-ttu-id="4018a-161">Infine, aggiungere hello seguenti righe toohello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="4018a-161">Finally, add hello following lines toohello **Main** method:</span></span>
   
       try
       {
            InitClient();
            ReportConnectivity();
       }
       catch (Exception ex)
       {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
       }
       Console.WriteLine("Press Enter tooexit.");
       Console.ReadLine();

1. <span data-ttu-id="4018a-162">In Esplora soluzioni hello, aprire hello **progetti di avvio impostato...**  e verificare che hello **azione** per **ReportConnectivity** progetto **avviare**.</span><span class="sxs-lookup"><span data-stu-id="4018a-162">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **ReportConnectivity** project is **Start**.</span></span> <span data-ttu-id="4018a-163">Compilare la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="4018a-163">Build hello solution.</span></span>
1. <span data-ttu-id="4018a-164">Eseguire l'applicazione facendo clic su hello **ReportConnectivity** progetto, quindi selezionando **Debug**, seguito da **Avvia nuova istanza**.</span><span class="sxs-lookup"><span data-stu-id="4018a-164">Run this application by right-clicking on hello **ReportConnectivity** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="4018a-165">Si dovrebbe vedere Recupero di informazioni doppi hello e invio di connettività un *segnalati proprietà*.</span><span class="sxs-lookup"><span data-stu-id="4018a-165">You should see it getting hello twin information, and then sending connectivity as a *reported property*.</span></span>
   
    ![Eseguire la connettività tooreport app per dispositivi][img-rundeviceapp]
    
    
1. <span data-ttu-id="4018a-167">Ora che hello dispositivo segnalato le informazioni di connettività, viene visualizzato in entrambe le query.</span><span class="sxs-lookup"><span data-stu-id="4018a-167">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="4018a-168">Eseguire .NET hello **AddTagsAndQuery** hello toorun app nuovamente una query.</span><span class="sxs-lookup"><span data-stu-id="4018a-168">Run hello .NET **AddTagsAndQuery** app toorun hello queries again.</span></span> <span data-ttu-id="4018a-169">Questa volta **myDeviceId** verrà visualizzato nei risultati di entrambe le query.</span><span class="sxs-lookup"><span data-stu-id="4018a-169">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![Connettività del dispositivo segnalata correttamente][img-tagappsuccess]

## <a name="next-steps"></a><span data-ttu-id="4018a-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4018a-171">Next steps</span></span>
<span data-ttu-id="4018a-172">In questa esercitazione, è configurato un nuovo hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità.</span><span class="sxs-lookup"><span data-stu-id="4018a-172">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="4018a-173">Aggiunti i metadati del dispositivo come tag da un'app di back-end e ha scritto informazioni di connettività un dispositivo simulato app tooreport dispositivo in un doppio dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="4018a-173">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="4018a-174">È inoltre appreso tooquery queste informazioni usando il linguaggio di query di hello IoT Hub simile a SQL.</span><span class="sxs-lookup"><span data-stu-id="4018a-174">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="4018a-175">Hello utilizzare seguenti come risorse toolearn per:</span><span class="sxs-lookup"><span data-stu-id="4018a-175">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="4018a-176">inviare i dati di telemetria dai dispositivi con hello [iniziare con l'IoT Hub] [ lnk-iothub-getstarted] esercitazione</span><span class="sxs-lookup"><span data-stu-id="4018a-176">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="4018a-177">configurare i dispositivi con le proprietà desiderate di un doppio dispositivo hello [lo si desidera utilizzare i dispositivi di proprietà tooconfigure] [ lnk-twin-how-to-configure] esercitazione</span><span class="sxs-lookup"><span data-stu-id="4018a-177">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="4018a-178">controllare i dispositivi in modo interattivo (ad esempio l'attivazione di una ventola da un'app controllata dall'utente) con hello [utilizzare metodi diretti] [ lnk-methods-tutorial] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4018a-178">control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-csharp-twin-getstarted/addtagapp.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-getstarted/clientsdknuget.png
[img-rundeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/rundeviceapp.png
[img-tagappsuccess]: media/iot-hub-csharp-csharp-twin-getstarted/tagappsuccess.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp
[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

