---
title: "proprietà di un doppio dispositivo IoT Hub Azure aaaUse (.NET/.NET) | Documenti Microsoft"
description: Come dispositivo di Azure IoT Hub toouse gemelli di tooconfigure dispositivi. Utilizzare il dispositivo di Azure IoT hello SDK per .NET tooimplement un'app dispositivo simulato e hello Azure IoT servizio SDK per .NET tooimplement un'applicazione di servizio che consente di modificare la configurazione di un dispositivo utilizzando una coppia di dispositivo.
services: iot-hub
documentationcenter: .net
author: dsk-2015
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: dkshir
ms.openlocfilehash: 486436d29abfd5158c253adc5abf5935e0e1fdba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a><span data-ttu-id="2a395-104">Utilizzare i dispositivi di proprietà desiderato tooconfigure</span><span class="sxs-lookup"><span data-stu-id="2a395-104">Use desired properties tooconfigure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="2a395-105">Alla fine di hello di questa esercitazione, si avranno due applicazioni di console .NET:</span><span class="sxs-lookup"><span data-stu-id="2a395-105">At hello end of this tutorial, you will have two .NET console apps:</span></span>

* <span data-ttu-id="2a395-106">**SimulateDeviceConfiguration**, un'app dispositivo simulato che è in attesa di un aggiornamento della configurazione desiderata e hello Visualizza lo stato di un processo di aggiornamento configurazione simulato.</span><span class="sxs-lookup"><span data-stu-id="2a395-106">**SimulateDeviceConfiguration**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="2a395-107">**SetDesiredConfigurationAndQuery**, configurazione in un dispositivo di un'applicazione back-end, che imposta hello desiderato e le query hello il processo di aggiornamento di configurazione.</span><span class="sxs-lookup"><span data-stu-id="2a395-107">**SetDesiredConfigurationAndQuery**, a back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="2a395-108">articolo Hello [Azure IoT SDK] [ lnk-hub-sdks] fornisce informazioni su Azure IoT SDK hello che è possibile utilizzare toobuild applicazioni back-end sia sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2a395-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="2a395-109">toocomplete questa esercitazione è necessario hello segue:</span><span class="sxs-lookup"><span data-stu-id="2a395-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="2a395-110">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="2a395-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="2a395-111">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="2a395-111">An active Azure account.</span></span> <span data-ttu-id="2a395-112">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="2a395-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="2a395-113">Se si sono seguite hello [introduzione gemelli dispositivo] [ lnk-twin-tutorial] esercitazione, si dispone già di un hub IoT e un'identità del dispositivo chiamato **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="2a395-113">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="2a395-114">In tal caso, è possibile ignorare toohello [crea hello dispositivo simulato applicazione] [ lnk-how-to-configure-createapp] sezione.</span><span class="sxs-lookup"><span data-stu-id="2a395-114">In that case, you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="2a395-115">Creare app dispositivo simulato hello</span><span class="sxs-lookup"><span data-stu-id="2a395-115">Create hello simulated device app</span></span>
<span data-ttu-id="2a395-116">In questa sezione si crea un'applicazione console .NET che si connette hub tooyour come **myDeviceId**, in attesa di un aggiornamento della configurazione desiderata e quindi segnala gli aggiornamenti nel processo di aggiornamento configurazione hello simulato.</span><span class="sxs-lookup"><span data-stu-id="2a395-116">In this section, you create a .NET console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="2a395-117">In Visual Studio, creare un nuovo progetto di Visual c# Windows Desktop classico utilizzando hello **applicazione Console** modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="2a395-117">In Visual Studio, create a new Visual C# Windows Classic Desktop project by using hello **Console Application** project template.</span></span> <span data-ttu-id="2a395-118">Progetto hello nome **SimulateDeviceConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="2a395-118">Name hello project **SimulateDeviceConfiguration**.</span></span>
   
    ![Nuova app per il dispositivo di Windows classico in Visual C#][img-createdeviceapp]

1. <span data-ttu-id="2a395-120">In Esplora soluzioni fare doppio clic su hello **SimulateDeviceConfiguration** del progetto e quindi fare clic su **Gestisci pacchetti NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="2a395-120">In Solution Explorer, right-click hello **SimulateDeviceConfiguration** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="2a395-121">In hello **Gestione pacchetti NuGet** selezionare **Sfoglia** e cercare **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="2a395-121">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="2a395-122">Selezionare **installare** tooinstall hello **Microsoft.Azure.Devices.Client** pacchetto e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="2a395-122">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="2a395-123">Questa procedura Scarica, installa e aggiunge un riferimento toohello [dispositivo IoT di Azure SDK] [ lnk-nuget-client-sdk] NuGet pacchetto e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="2a395-123">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![App client della finestra Gestione pacchetti NuGet][img-clientnuget]
1. <span data-ttu-id="2a395-125">Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="2a395-125">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="2a395-126">Aggiungere i seguenti campi toohello hello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="2a395-126">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="2a395-127">Sostituire il valore di segnaposto hello con stringa di connessione hello dispositivo che si è preso nota nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="2a395-127">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();

1. <span data-ttu-id="2a395-128">Aggiungere hello seguente metodo toohello **programma** classe:</span><span class="sxs-lookup"><span data-stu-id="2a395-128">Add hello following method toohello **Program** class:</span></span>
 
        public static void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }
    <span data-ttu-id="2a395-129">Hello **Client** oggetto espone tutti i metodi di hello desiderate toointeract con gemelli di dispositivo dal dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="2a395-129">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="2a395-130">Hello codice illustrato in precedenza, inizializza hello **Client** oggetto, quindi recupera hello dispositivo doppi per **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="2a395-130">hello code shown above, initializes hello **Client** object, and then retrieves hello device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="2a395-131">Aggiungere hello seguente metodo toohello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="2a395-131">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="2a395-132">Questo metodo imposta i valori iniziali di hello di telemetria sul dispositivo locale hello e quindi gli aggiornamenti hello gemelli di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2a395-132">This method sets hello initial values of telemetry on hello local device and then updates hello device twin.</span></span>

        public static async void InitTelemetry()
        {
            try
            {
                Console.WriteLine("Report initial telemetry config:");
                TwinCollection telemetryConfig = new TwinCollection();
                
                telemetryConfig["configId"] = "0";
                telemetryConfig["sendFrequency"] = "24h";
                reportedProperties["telemetryConfig"] = telemetryConfig;
                Console.WriteLine(JsonConvert.SerializeObject(reportedProperties));

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. <span data-ttu-id="2a395-133">Aggiungere hello seguente metodo toohello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="2a395-133">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="2a395-134">Si tratta di un callback che rileva una modifica in *le proprietà desiderate* in un doppio dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="2a395-134">This is a callback which will detect a change in *desired properties* in hello device twin.</span></span>

        private static async Task OnDesiredPropertyChanged(TwinCollection desiredProperties, object userContext)
        {
            try
            {
                Console.WriteLine("Desired property change:");
                Console.WriteLine(JsonConvert.SerializeObject(desiredProperties));

                var currentTelemetryConfig = reportedProperties["telemetryConfig"];
                var desiredTelemetryConfig = desiredProperties["telemetryConfig"];

                if ((desiredTelemetryConfig != null) && (desiredTelemetryConfig["configId"] != currentTelemetryConfig["configId"]))
                {
                    Console.WriteLine("\nInitiating config change");
                    currentTelemetryConfig["status"] = "Pending";
                    currentTelemetryConfig["pendingConfig"] = desiredTelemetryConfig;

                    await Client.UpdateReportedPropertiesAsync(reportedProperties);

                    CompleteConfigChange();
                }
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    <span data-ttu-id="2a395-135">Questo hello aggiornamenti metodo segnalato le proprietà sull'oggetto di un doppio hello dispositivo locale con la configurazione di hello richiesta e imposta lo stato di hello di aggiornamento troppo**in sospeso**, quindi gli aggiornamenti hello gemelli di dispositivo nel servizio hello.</span><span class="sxs-lookup"><span data-stu-id="2a395-135">This method updates hello reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="2a395-136">Dopo aver aggiornato correttamente un doppio dispositivo hello, completamento di modifica della configurazione hello chiamando il metodo hello `CompleteConfigChange` descritta al punto successivo hello.</span><span class="sxs-lookup"><span data-stu-id="2a395-136">After successfully updating hello device twin, it completes hello config change by calling hello method `CompleteConfigChange` described in hello next point.</span></span>

1. <span data-ttu-id="2a395-137">Aggiungere hello seguente metodo toohello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="2a395-137">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="2a395-138">Questo metodo simula un ripristino del dispositivo, quindi gli aggiornamenti hello proprietà segnalate locale impostazione dello stato di hello troppo**successo** e rimuove hello **pendingConfig** elemento.</span><span class="sxs-lookup"><span data-stu-id="2a395-138">This method simulates a device reset, then updates hello local reported properties setting hello status too**Success** and removes hello **pendingConfig** element.</span></span> <span data-ttu-id="2a395-139">Viene quindi aggiornato doppi dispositivo hello sul servizio hello.</span><span class="sxs-lookup"><span data-stu-id="2a395-139">It then updates hello device twin on hello service.</span></span> 

        public static async void CompleteConfigChange()
        {
            try
            {
                var currentTelemetryConfig = reportedProperties["telemetryConfig"];

                Console.WriteLine("\nSimulating device reset");
                await Task.Delay(30000); 

                Console.WriteLine("\nCompleting config change");
                currentTelemetryConfig["configId"] = currentTelemetryConfig["pendingConfig"]["configId"];
                currentTelemetryConfig["sendFrequency"] = currentTelemetryConfig["pendingConfig"]["sendFrequency"];
                currentTelemetryConfig["status"] = "Success";
                currentTelemetryConfig["pendingConfig"] = null;

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
                Console.WriteLine("Config change complete \nPress any key tooexit.");
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. <span data-ttu-id="2a395-140">Aggiungere infine hello seguenti righe toohello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="2a395-140">Finally add hello following lines toohello **Main** method:</span></span>

        try
        {
            InitClient();
            InitTelemetry();

            Console.WriteLine("Wait for desired telemetry...");
            Client.SetDesiredPropertyUpdateCallback(OnDesiredPropertyChanged, null).Wait();
            Console.ReadKey();
        }
        catch (AggregateException ex)
        {
            foreach (Exception exception in ex.InnerExceptions)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", exception);
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }

   > [!NOTE]
   > <span data-ttu-id="2a395-141">Questa esercitazione non simula alcun comportamento per gli aggiornamenti della configurazione simultanei.</span><span class="sxs-lookup"><span data-stu-id="2a395-141">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="2a395-142">Alcuni processi di aggiornamento configurazione potrebbero essere in grado di tooaccommodate modifiche della configurazione di destinazione durante l'esecuzione di aggiornamento hello, alcuni potrebbe essere tooqueue mentre altri possibile rifiutarli con una condizione di errore.</span><span class="sxs-lookup"><span data-stu-id="2a395-142">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, some might have tooqueue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="2a395-143">Verificare che tooconsider hello comportamento desiderato per il processo di configurazione specifica e aggiungere la logica appropriata hello prima dell'avvio di modifica della configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="2a395-143">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="2a395-144">Compilare la soluzione hello ed eseguire hello dispositivo app da Visual Studio, fare clic su **F5**.</span><span class="sxs-lookup"><span data-stu-id="2a395-144">Build hello solution and then run hello device app from Visual Studio by clicking **F5**.</span></span> <span data-ttu-id="2a395-145">Nella console di output di hello, dovrebbe essere messaggi hello che indica che il dispositivo simulato è il recupero di un doppio dispositivo hello, impostazione dati di telemetria hello e in attesa di modifica della proprietà desiderata.</span><span class="sxs-lookup"><span data-stu-id="2a395-145">On hello output console, you should see hello messages indicating that your simulated device is retrieving hello device twin, setting up hello telemetry, and waiting for desired property change.</span></span> <span data-ttu-id="2a395-146">Mantenere hello app in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2a395-146">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="2a395-147">Creare l'applicazione di servizio hello</span><span class="sxs-lookup"><span data-stu-id="2a395-147">Create hello service app</span></span>
<span data-ttu-id="2a395-148">In questa sezione si creerà un'applicazione console .NET che hello aggiornamenti *le proprietà desiderate* su hello gemelli di dispositivo associati **myDeviceId** con un nuovo oggetto di configurazione di telemetria.</span><span class="sxs-lookup"><span data-stu-id="2a395-148">In this section, you will create a .NET console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="2a395-149">Quindi esegue una query gemelli dispositivo hello archiviate nell'hub IoT hello e Mostra differenza hello tra hello desiderato e le configurazioni di dispositivo hello segnalato.</span><span class="sxs-lookup"><span data-stu-id="2a395-149">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="2a395-150">In Visual Studio, aggiungere una soluzione di Visual c# Windows Desktop classico progetto toohello corrente utilizzando hello **applicazione Console** modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="2a395-150">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="2a395-151">Progetto hello nome **SetDesiredConfigurationAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="2a395-151">Name hello project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Nuovo progetto desktop di Windows classico in Visual C#][img-createapp]
1. <span data-ttu-id="2a395-153">In Esplora soluzioni fare doppio clic su hello **SetDesiredConfigurationAndQuery** del progetto e quindi fare clic su **Gestisci pacchetti NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="2a395-153">In Solution Explorer, right-click hello **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="2a395-154">In hello **Gestione pacchetti NuGet** selezionare **Sfoglia**, cercare **microsoft.azure.devices**selezionare **installare** tooinstall Hello **Microsoft.Azure.Devices** pacchetto e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="2a395-154">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="2a395-155">Questa procedura Scarica, installa e aggiunge un riferimento toohello [SDK di servizi di Azure IoT] [ lnk-nuget-service-sdk] NuGet pacchetto e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="2a395-155">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Finestra Gestione pacchetti NuGet][img-servicenuget]
1. <span data-ttu-id="2a395-157">Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="2a395-157">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="2a395-158">Aggiungere i seguenti campi toohello hello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="2a395-158">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="2a395-159">Sostituire il valore di segnaposto hello con la stringa di connessione IoT Hub hub hello creato nella sezione precedente hello hello.</span><span class="sxs-lookup"><span data-stu-id="2a395-159">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="2a395-160">Aggiungere hello seguente metodo toohello **programma** classe:</span><span class="sxs-lookup"><span data-stu-id="2a395-160">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="2a395-161">Hello **Registro di sistema** oggetto espone tutte hello metodi obbligatorio toointeract con gemelli di dispositivo dal servizio hello.</span><span class="sxs-lookup"><span data-stu-id="2a395-161">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="2a395-162">Questo codice inizializza hello **Registro di sistema** oggetto recupera hello gemelli di dispositivo per **myDeviceId**e quindi aggiorna le proprietà desiderate con un nuovo oggetto di configurazione di telemetria.</span><span class="sxs-lookup"><span data-stu-id="2a395-162">This code initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="2a395-163">Successivamente, viene eseguita una query gemelli dispositivo hello archiviate nell'hub IoT hello ogni 10 secondi e stampa hello desiderato e segnalate le configurazioni di telemetria.</span><span class="sxs-lookup"><span data-stu-id="2a395-163">After that, it queries hello device twins stored in hello IoT hub every 10 seconds, and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="2a395-164">Fare riferimento toohello [il linguaggio di query di IoT Hub] [ lnk-query] toolearn come rich toogenerate report tra tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="2a395-164">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="2a395-165">Questa applicazione effettua una query dell'hub IoT ogni 10 secondi a scopo illustrativo.</span><span class="sxs-lookup"><span data-stu-id="2a395-165">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="2a395-166">Utilizzare una query toogenerate rivolta all'utente report tra più dispositivi e non toodetect modifiche.</span><span class="sxs-lookup"><span data-stu-id="2a395-166">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="2a395-167">Se la soluzione richiede notifiche in tempo reale degli eventi del dispositivo, usare le [notifiche relative al dispositivo gemello][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="2a395-167">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="2a395-168">Infine, aggiungere hello seguenti righe toohello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="2a395-168">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. <span data-ttu-id="2a395-169">In Esplora soluzioni hello, aprire hello **progetti di avvio impostato...**  e verificare che hello **azione** per **SetDesiredConfigurationAndQuery** progetto **avviare**.</span><span class="sxs-lookup"><span data-stu-id="2a395-169">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="2a395-170">Compilare la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="2a395-170">Build hello solution.</span></span>
1. <span data-ttu-id="2a395-171">Con **SimulateDeviceConfiguration** dispositivo che esegue di app, hello esecuzione del servizio app da Visual Studio tramite **F5**.</span><span class="sxs-lookup"><span data-stu-id="2a395-171">With **SimulateDeviceConfiguration** device app running, run hello service app from Visual Studio using **F5**.</span></span> <span data-ttu-id="2a395-172">Dovrebbe essere hello segnalati configurazione modificare da **in sospeso** troppo**successo** Active nuovo hello frequenza di invio dei cinque minuti invece di 24 ore.</span><span class="sxs-lookup"><span data-stu-id="2a395-172">You should see hello reported configuration change from **Pending** too**Success** with hello new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Dispositivo configurato correttamente][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="2a395-174">Si verifica un ritardo di backup tooa minuto tra funzionamento del report dispositivo hello e risultato della query hello.</span><span class="sxs-lookup"><span data-stu-id="2a395-174">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="2a395-175">Si tratta di tooenable hello query infrastruttura toowork su larga scala molto elevata.</span><span class="sxs-lookup"><span data-stu-id="2a395-175">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="2a395-176">viste di un doppio di un singolo dispositivo consistenza tooretrieve utilizzano hello **getDeviceTwin** metodo hello **Registro di sistema** classe.</span><span class="sxs-lookup"><span data-stu-id="2a395-176">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="2a395-177">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2a395-177">Next steps</span></span>
<span data-ttu-id="2a395-178">In questa esercitazione, impostare una configurazione desiderata come *le proprietà desiderate* dalla soluzione hello back-end e ha scritto un toodetect app dispositivo che modificano e simulare un processo di aggiornamento di più passaggi tramite hello segnalato lo stato di creazione di report proprietà.</span><span class="sxs-lookup"><span data-stu-id="2a395-178">In this tutorial, you set a desired configuration as *desired properties* from hello solution back end, and wrote a device app toodetect that change and simulate a multi-step update process reporting its status through hello reported properties.</span></span>

<span data-ttu-id="2a395-179">Hello utilizzare seguenti come risorse toolearn per:</span><span class="sxs-lookup"><span data-stu-id="2a395-179">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="2a395-180">inviare i dati di telemetria dai dispositivi con hello [iniziare con l'IoT Hub] [ lnk-iothub-getstarted] esercitazione</span><span class="sxs-lookup"><span data-stu-id="2a395-180">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="2a395-181">pianificare o eseguire operazioni su grandi set di dispositivi Vedere hello [pianificazione e i processi di broadcast] [ lnk-schedule-jobs] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2a395-181">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="2a395-182">controllare i dispositivi in modo interattivo (ad esempio l'attivazione di una ventola da un'app controllata dall'utente), con hello [utilizzare metodi diretti] [ lnk-methods-tutorial] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2a395-182">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/devicesdknuget.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png


<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-twin-tutorial]: iot-hub-csharp-csharp-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-how-to-configure-createapp]: iot-hub-csharp-csharp-twin-how-to-configure.md#create-the-simulated-device-app
