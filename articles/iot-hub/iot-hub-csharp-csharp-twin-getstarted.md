---
title: Introduzione ai dispositivi gemelli dell'hub IoT di Azure (.NET/.NET) | Microsoft Docs
description: Come usare i dispositivi gemelli dell'hub IoT di Azure per aggiungere tag e quindi usare una query dell'hub IoT. Usare Azure IoT SDK per dispositivi per Node.js per implementare l'app per dispositivo simulato e Azure IoT SDK per servizi per .NET per implementare un'app di servizio che aggiunge i tag ed esegue la query dell'hub IoT.
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
ms.openlocfilehash: 6073d594117e69676b753a1e3af25fffa3583a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-device-twins-netnet"></a><span data-ttu-id="dab36-104">Introduzione ai dispositivi gemelli (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="dab36-104">Get started with device twins (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="dab36-105">Al termine di questa esercitazione si avranno queste due app console .NET:</span><span class="sxs-lookup"><span data-stu-id="dab36-105">At the end of this tutorial, you will have these .NET console apps:</span></span>

* <span data-ttu-id="dab36-106">**CreateDeviceIdentity**, un'app .NET che crea un'identità del dispositivo e la chiave di sicurezza associata per connettere l'app per dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="dab36-106">**CreateDeviceIdentity**, a .NET app which creates a device identity and associated security key to connect your simulated device app.</span></span>
* <span data-ttu-id="dab36-107">**AddTagsAndQuery**, un'app back-end .NET, che aggiunge tag ed effettua una query dei dispositivi gemelli.</span><span class="sxs-lookup"><span data-stu-id="dab36-107">**AddTagsAndQuery**, a .NET back-end app which adds tags and queries device twins.</span></span>
* <span data-ttu-id="dab36-108">**ReportConnectivity.js**, un dispositivo .NET che simula un dispositivo che si connette all'hub IoT con l'identità del dispositivo creata prima e segnala la condizione della connettività.</span><span class="sxs-lookup"><span data-stu-id="dab36-108">**ReportConnectivity**, a .NET device app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="dab36-109">L'articolo [Azure IoT SDK][lnk-hub-sdks] contiene informazioni sui componenti Azure IoT SDK che consentono di compilare le app back-end e per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="dab36-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="dab36-110">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="dab36-110">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="dab36-111">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="dab36-111">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="dab36-112">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="dab36-112">An active Azure account.</span></span> <span data-ttu-id="dab36-113">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="dab36-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="dab36-114">Se invece si desidera creare l'identità del dispositivo a livello di codice, leggere la sezione corrispondente nell'articolo [Connettere il dispositivo simulato all'hub IoT tramite .NET][lnk-device-identity-csharp].</span><span class="sxs-lookup"><span data-stu-id="dab36-114">If you want to create the device identity programmatically instead, read the corresponding section in the [Connect your simulated device to your IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="dab36-115">Creare l'app di servizio</span><span class="sxs-lookup"><span data-stu-id="dab36-115">Create the service app</span></span>
<span data-ttu-id="dab36-116">In questa sezione si crea un'app console .NET (usando C#) e si aggiungono i metadati della posizione al dispositivo gemello associato a **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="dab36-116">In this section, you create a .NET console app (using C#) that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="dab36-117">Viene quindi eseguita una query nei dispositivi gemelli archiviati nell'hub IoT selezionando i dispositivi situati negli Stati Uniti e quindi quelli che segnalano una rete cellulare.</span><span class="sxs-lookup"><span data-stu-id="dab36-117">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="dab36-118">In Visual Studio aggiungere un progetto desktop di Windows classico in Visual C# usando il modello di progetto **Applicazione console** .</span><span class="sxs-lookup"><span data-stu-id="dab36-118">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="dab36-119">Assegnare al progetto il nome **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="dab36-119">Name the project **AddTagsAndQuery**.</span></span>
   
    ![Nuovo progetto desktop di Windows classico in Visual C#][img-createapp]
1. <span data-ttu-id="dab36-121">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **AddTagsAndQuery** e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="dab36-121">In Solution Explorer, right-click the **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="dab36-122">Nella finestra **Gestisci pacchetti NuGet** selezionare **Sfoglia** e cercare **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="dab36-122">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="dab36-123">Selezionare **Installa** per installare il pacchetto **Microsoft.Azure.Devices** e accettare le condizioni per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="dab36-123">Select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="dab36-124">Questa procedura scarica, installa e aggiunge un riferimento al [pacchetto NuGet Azure IoT - SDK per dispositivi][lnk-nuget-service-sdk] e alle relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="dab36-124">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Finestra Gestione pacchetti NuGet][img-servicenuget]
1. <span data-ttu-id="dab36-126">Aggiungere le istruzione `using` seguenti all'inizio del file **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="dab36-126">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="dab36-127">Aggiungere i campi seguenti alla classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="dab36-127">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="dab36-128">Sostituire il valore del segnaposto con la stringa di connessione dell'hub IoT creato nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="dab36-128">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="dab36-129">Aggiungere il metodo seguente alla classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="dab36-129">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="dab36-130">L'oggetto **RegistryManager** espone tutti i metodi necessari per interagire con i dispositivi gemelli dal servizio.</span><span class="sxs-lookup"><span data-stu-id="dab36-130">The **RegistryManager** class exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="dab36-131">Il codice precedente inizializza prima di tutto l'oggetto **registryManager**, quindi recupera il dispositivo gemello per **myDeviceId** e infine ne aggiorna i tag con le informazioni sulla posizione desiderate.</span><span class="sxs-lookup"><span data-stu-id="dab36-131">The previous code first initializes the **registryManager** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="dab36-132">Dopo l'aggiornamento, il codice precedente esegue due query: la prima seleziona solo i dispositivi gemelli tra quelli situati nello stabilimento **Redmond43** e la seconda affina la query per selezionare solo i dispositivi che sono connessi anche tramite la rete cellulare.</span><span class="sxs-lookup"><span data-stu-id="dab36-132">After updating, it executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="dab36-133">Si noti che il codice precedente, quando crea l'oggetto **query**, specifica un numero massimo di documenti restituiti.</span><span class="sxs-lookup"><span data-stu-id="dab36-133">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="dab36-134">L'oggetto **query** contiene una proprietà booleana **HasMoreResults** che è possibile usare per richiamare i metodi **GetNextAsTwinAsync** più volte per recuperare tutti i risultati.</span><span class="sxs-lookup"><span data-stu-id="dab36-134">The **query** object contains a **HasMoreResults** boolean property that you can use to invoke the **GetNextAsTwinAsync** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="dab36-135">Per i risultati che non sono dispositivi gemelli, ad esempio i risultati delle query di aggregazione, è disponibile un metodo chiamato **GetNextAsJson**.</span><span class="sxs-lookup"><span data-stu-id="dab36-135">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="dab36-136">Aggiungere infine le righe seguenti al metodo **Main** :</span><span class="sxs-lookup"><span data-stu-id="dab36-136">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="dab36-137">In Esplora soluzioni aprire **Imposta progetti di avvio** e assicurarsi che **Azione** per il progetto **AddTagsAndQuery** sia impostata su **Avvio**.</span><span class="sxs-lookup"><span data-stu-id="dab36-137">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="dab36-138">Compilare la soluzione.</span><span class="sxs-lookup"><span data-stu-id="dab36-138">Build the solution.</span></span>
1. <span data-ttu-id="dab36-139">Eseguire l'applicazione facendo clic con il pulsante destro del mouse sul progetto **AddTagsAndQuery** e selezionando **Debug**, seguito da **Avvia nuova istanza**.</span><span class="sxs-lookup"><span data-stu-id="dab36-139">Run this application by right-clicking on the **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="dab36-140">Nei risultati si noterà un dispositivo per la query che cerca tutti i dispositivi situati in **Redmond43** e nessuno per la query che limita i risultati ai dispositivi che usano una rete cellulare.</span><span class="sxs-lookup"><span data-stu-id="dab36-140">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![Risultati della query nella finestra][img-addtagapp]

<span data-ttu-id="dab36-142">Nella sezione successiva si crea un'app per dispositivo che segnala le informazioni sulla connettività e modifica il risultato della query nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="dab36-142">In the next section, you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="dab36-143">Creare l'app per dispositivo</span><span class="sxs-lookup"><span data-stu-id="dab36-143">Create the device app</span></span>
<span data-ttu-id="dab36-144">In questa sezione si crea un'app console .NET che si connette all'hub come **myDeviceId** e quindi aggiorna le proprietà segnalate per poter contenere le informazioni relative alla connessione usando una rete cellulare.</span><span class="sxs-lookup"><span data-stu-id="dab36-144">In this section, you create a .NET console app that connects to your hub as **myDeviceId**, and then updates its reported properties to contain the information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="dab36-145">In Visual Studio aggiungere un progetto desktop di Windows classico in Visual C# usando il modello di progetto **Applicazione console** .</span><span class="sxs-lookup"><span data-stu-id="dab36-145">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="dab36-146">Denominare il progetto **ReportConnectivity**.</span><span class="sxs-lookup"><span data-stu-id="dab36-146">Name the project **ReportConnectivity**.</span></span>
   
    ![Nuova app per il dispositivo di Windows classico in Visual C#][img-createdeviceapp]
    
1. <span data-ttu-id="dab36-148">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **ReportConnectivity**, quindi fare clic su **Gestisci pacchetti NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="dab36-148">In Solution Explorer, right-click the **ReportConnectivity** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="dab36-149">Nella finestra **Gestione pacchetti NuGet** selezionare **Sfoglia** e cercare **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="dab36-149">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="dab36-150">Selezionare **Installa** per installare il pacchetto **microsoft.azure.devices.client** e accettare le condizioni d'uso.</span><span class="sxs-lookup"><span data-stu-id="dab36-150">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="dab36-151">Questa procedura scarica, installa e aggiunge un riferimento al pacchetto NuGet [Azure IoT SDK per dispositivi][lnk-nuget-client-sdk] e alle relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="dab36-151">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![App client della finestra Gestione pacchetti NuGet][img-clientnuget]
1. <span data-ttu-id="dab36-153">Aggiungere le istruzione `using` seguenti all'inizio del file **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="dab36-153">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="dab36-154">Aggiungere i campi seguenti alla classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="dab36-154">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="dab36-155">Sostituire il valore del segnaposto con la stringa di connessione del dispositivo annotato nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="dab36-155">Replace the placeholder value with the device connection string that you noted in the previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="dab36-156">Aggiungere il metodo seguente alla classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="dab36-156">Add the following method to the **Program** class:</span></span>

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting to hub");
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

    <span data-ttu-id="dab36-157">L'oggetto **Client** espone tutti i metodi necessari per interagire con i dispositivi gemelli dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="dab36-157">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="dab36-158">Il codice riportato sopra inizializza l'oggetto **Client** e quindi recupera il dispositivo gemello per **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="dab36-158">The code shown above, initializes the **Client** object, and then retrieves the device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="dab36-159">Aggiungere il metodo seguente alla classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="dab36-159">Add the following method to the **Program** class:</span></span>
   
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

   <span data-ttu-id="dab36-160">Il codice sopra riportato aggiorna le proprietà segnalate di **myDeviceId** con le informazioni di connettività.</span><span class="sxs-lookup"><span data-stu-id="dab36-160">The code above updates **myDeviceId**'s reported property with the connectivity information.</span></span>

1. <span data-ttu-id="dab36-161">Aggiungere infine le righe seguenti al metodo **Main** :</span><span class="sxs-lookup"><span data-stu-id="dab36-161">Finally, add the following lines to the **Main** method:</span></span>
   
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
       Console.WriteLine("Press Enter to exit.");
       Console.ReadLine();

1. <span data-ttu-id="dab36-162">In Esplora soluzioni aprire **Imposta progetti di avvio...** e assicurarsi che **Azione** per il progetto **ReportConnectivity** sia impostato su **Avvio**.</span><span class="sxs-lookup"><span data-stu-id="dab36-162">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **ReportConnectivity** project is **Start**.</span></span> <span data-ttu-id="dab36-163">Compilare la soluzione.</span><span class="sxs-lookup"><span data-stu-id="dab36-163">Build the solution.</span></span>
1. <span data-ttu-id="dab36-164">Eseguire l'applicazione facendo clic con il pulsante destro del mouse sul progetto **ReportConnectivity** e selezionando **Debug**, seguito da **Avvia nuova istanza**.</span><span class="sxs-lookup"><span data-stu-id="dab36-164">Run this application by right-clicking on the **ReportConnectivity** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="dab36-165">Si dovrebbero vedere le informazioni gemelle e quindi l'invio della connettività come *proprietà segnalata*.</span><span class="sxs-lookup"><span data-stu-id="dab36-165">You should see it getting the twin information, and then sending connectivity as a *reported property*.</span></span>
   
    ![Eseguire l'app per dispositivi per segnalare la connettività][img-rundeviceapp]
    
    
1. <span data-ttu-id="dab36-167">Ora che il dispositivo ha segnalato le informazioni sulla connettività, verrà visualizzato in entrambe le query.</span><span class="sxs-lookup"><span data-stu-id="dab36-167">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="dab36-168">Eseguire l'app .NET **AddTagsAndQuery** per eseguire nuovamente la query.</span><span class="sxs-lookup"><span data-stu-id="dab36-168">Run the .NET **AddTagsAndQuery** app to run the queries again.</span></span> <span data-ttu-id="dab36-169">Questa volta **myDeviceId** verrà visualizzato nei risultati di entrambe le query.</span><span class="sxs-lookup"><span data-stu-id="dab36-169">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![Connettività del dispositivo segnalata correttamente][img-tagappsuccess]

## <a name="next-steps"></a><span data-ttu-id="dab36-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dab36-171">Next steps</span></span>
<span data-ttu-id="dab36-172">In questa esercitazione è stato configurato un nuovo hub IoT nel Portale di Azure ed è stata quindi creata un'identità del dispositivo nel registro di identità dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="dab36-172">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="dab36-173">Sono stati aggiunti i metadati del dispositivo come tag da un'app back-end ed è stata scritta un'app per dispositivo simulato per segnalare le informazioni sulla connettività del dispositivo nel dispositivo gemello.</span><span class="sxs-lookup"><span data-stu-id="dab36-173">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="dab36-174">Si è anche appreso come effettuare una query di queste informazioni usando il linguaggio di query simile a SQL dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="dab36-174">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="dab36-175">Per altre informazioni, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="dab36-175">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="dab36-176">Per inviare dati di telemetria dai dispositivi, vedere l'esercitazione [Introduzione all'hub IoT][lnk-iothub-getstarted].</span><span class="sxs-lookup"><span data-stu-id="dab36-176">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="dab36-177">Per configurare i dispositivi usando le proprietà desiderate del dispositivo gemello, vedere l'esercitazione [Usare le proprietà desiderate per configurare i dispositivi][lnk-twin-how-to-configure].</span><span class="sxs-lookup"><span data-stu-id="dab36-177">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="dab36-178">Per controllare i dispositivi in modo interattivo, ad esempio per attivare un ventilatore da un'app controllata dall'utente, vedere l'esercitazione [Use direct methods][lnk-methods-tutorial] (Usare metodi diretti).</span><span class="sxs-lookup"><span data-stu-id="dab36-178">control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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

