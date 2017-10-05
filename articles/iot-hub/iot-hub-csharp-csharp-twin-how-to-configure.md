---
title: "Usare le proprietà di un dispositivo gemello dell'hub IoT di Azure (.NET/.NET) | Microsoft Docs"
description: "Come usare le proprietà di un dispositivo gemello dell'hub IoT di Azure per configurare dispositivi. Usare Azure IoT SDK per dispositivi per .NET per implementare un'app per dispositivo simulato e Azure IoT SDK per servizi per .NET per implementare un'app di servizio che modifica la configurazione di un dispositivo usando un dispositivo gemello."
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
ms.openlocfilehash: 679cda28bf3ce9fb207fe3693a3453b355f1de15
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="use-desired-properties-to-configure-devices"></a><span data-ttu-id="75b93-104">Usare le proprietà desiderate per configurare i dispositivi</span><span class="sxs-lookup"><span data-stu-id="75b93-104">Use desired properties to configure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="75b93-105">Al termine di questa esercitazione si avranno due app console .NET:</span><span class="sxs-lookup"><span data-stu-id="75b93-105">At the end of this tutorial, you will have two .NET console apps:</span></span>

* <span data-ttu-id="75b93-106">**SimulateDeviceConfiguration**, un'app per dispositivo simulata che attende un aggiornamento della configurazione desiderata e segnala lo stato di un processo di aggiornamento della configurazione simulata.</span><span class="sxs-lookup"><span data-stu-id="75b93-106">**SimulateDeviceConfiguration**, a simulated device app that waits for a desired configuration update and reports the status of a simulated configuration update process.</span></span>
* <span data-ttu-id="75b93-107">**SetDesiredConfigurationAndQuery.js**, un'app back-end che imposta la configurazione desiderata in un dispositivo ed esegue query sul processo di aggiornamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="75b93-107">**SetDesiredConfigurationAndQuery**, a back-end app, which sets the desired configuration on a device and queries the configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="75b93-108">L'articolo [Azure IoT SDK][lnk-hub-sdks] contiene informazioni sui componenti Azure IoT SDK che consentono di compilare le app back-end e per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="75b93-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="75b93-109">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="75b93-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="75b93-110">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="75b93-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="75b93-111">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="75b93-111">An active Azure account.</span></span> <span data-ttu-id="75b93-112">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="75b93-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="75b93-113">Se è stata seguita l'esercitazione [Introduzione ai dispositivi gemelli][lnk-twin-tutorial] sono già disponibili un hub IoT e un'identità del dispositivo denominata **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="75b93-113">If you followed the [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="75b93-114">È quindi possibile ignorare la sezione [Creare l'app per dispositivo simulata][lnk-how-to-configure-createapp].</span><span class="sxs-lookup"><span data-stu-id="75b93-114">In that case, you can skip to the [Create the simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-the-simulated-device-app"></a><span data-ttu-id="75b93-115">Creare l'app per dispositivo simulata</span><span class="sxs-lookup"><span data-stu-id="75b93-115">Create the simulated device app</span></span>
<span data-ttu-id="75b93-116">In questa sezione si crea un'app console .NET che si connette all'hub come **myDeviceId**, attende un aggiornamento della configurazione desiderata e quindi segnala gli aggiornamenti nel processo di aggiornamento della configurazione simulata.</span><span class="sxs-lookup"><span data-stu-id="75b93-116">In this section, you create a .NET console app that connects to your hub as **myDeviceId**, waits for a desired configuration update and then reports updates on the simulated configuration update process.</span></span>

1. <span data-ttu-id="75b93-117">In Visual Studio creare un nuovo progetto desktop classico di Windows Visual C# usando il modello di progetto **Applicazione console**.</span><span class="sxs-lookup"><span data-stu-id="75b93-117">In Visual Studio, create a new Visual C# Windows Classic Desktop project by using the **Console Application** project template.</span></span> <span data-ttu-id="75b93-118">Chiamare il progetto **SimulateDeviceConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="75b93-118">Name the project **SimulateDeviceConfiguration**.</span></span>
   
    ![Nuova app per il dispositivo di Windows classico in Visual C#][img-createdeviceapp]

1. <span data-ttu-id="75b93-120">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **SimulateDeviceConfiguration** e quindi scegliere **Gestisci pacchetti NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="75b93-120">In Solution Explorer, right-click the **SimulateDeviceConfiguration** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="75b93-121">Nella finestra **Gestione pacchetti NuGet** selezionare **Sfoglia** e cercare **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="75b93-121">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="75b93-122">Selezionare **Installa** per installare il pacchetto **microsoft.azure.devices.client** e accettare le condizioni d'uso.</span><span class="sxs-lookup"><span data-stu-id="75b93-122">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="75b93-123">Questa procedura scarica, installa e aggiunge un riferimento al pacchetto NuGet [Azure IoT SDK per dispositivi][lnk-nuget-client-sdk] e alle relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="75b93-123">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![App client della finestra Gestione pacchetti NuGet][img-clientnuget]
1. <span data-ttu-id="75b93-125">Aggiungere le istruzione `using` seguenti all'inizio del file **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="75b93-125">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="75b93-126">Aggiungere i campi seguenti alla classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="75b93-126">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="75b93-127">Sostituire il valore del segnaposto con la stringa di connessione del dispositivo annotato nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="75b93-127">Replace the placeholder value with the device connection string that you noted in the previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();

1. <span data-ttu-id="75b93-128">Aggiungere il metodo seguente alla classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="75b93-128">Add the following method to the **Program** class:</span></span>
 
        public static void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting to hub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }
    <span data-ttu-id="75b93-129">L'oggetto **Client** espone tutti i metodi necessari per interagire con i dispositivi gemelli dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="75b93-129">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="75b93-130">Il codice riportato sopra inizializza l'oggetto **Client** e quindi recupera il dispositivo gemello per **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="75b93-130">The code shown above, initializes the **Client** object, and then retrieves the device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="75b93-131">Aggiungere il metodo seguente alla classe **Program**.</span><span class="sxs-lookup"><span data-stu-id="75b93-131">Add the following method to the **Program** class.</span></span> <span data-ttu-id="75b93-132">Questo metodo imposta i valori iniziali di telemetria nel dispositivo locale e quindi aggiorna il dispositivo gemello.</span><span class="sxs-lookup"><span data-stu-id="75b93-132">This method sets the initial values of telemetry on the local device and then updates the device twin.</span></span>

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

1. <span data-ttu-id="75b93-133">Aggiungere il metodo seguente alla classe **Program**.</span><span class="sxs-lookup"><span data-stu-id="75b93-133">Add the following method to the **Program** class.</span></span> <span data-ttu-id="75b93-134">Si tratta di un callback che rileva una modifica nelle *proprietà desiderate* del dispositivo gemello.</span><span class="sxs-lookup"><span data-stu-id="75b93-134">This is a callback which will detect a change in *desired properties* in the device twin.</span></span>

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

    <span data-ttu-id="75b93-135">Questo metodo aggiorna le proprietà segnalate nell'oggetto dispositivo gemello locale con la richiesta di aggiornamento della configurazione e imposta lo stato su **Pending** (Sospeso), quindi aggiorna il dispositivo gemello nel servizio.</span><span class="sxs-lookup"><span data-stu-id="75b93-135">This method updates the reported properties on the local device twin object with the configuration update request and sets the status to **Pending**, then updates the device twin on the service.</span></span> <span data-ttu-id="75b93-136">Dopo aver aggiornato correttamente il dispositivo gemello, quest'ultimo completerà la configurazione chiamando il metodo `CompleteConfigChange` descritto nel punto successivo.</span><span class="sxs-lookup"><span data-stu-id="75b93-136">After successfully updating the device twin, it completes the config change by calling the method `CompleteConfigChange` described in the next point.</span></span>

1. <span data-ttu-id="75b93-137">Aggiungere il metodo seguente alla classe **Program**.</span><span class="sxs-lookup"><span data-stu-id="75b93-137">Add the following method to the **Program** class.</span></span> <span data-ttu-id="75b93-138">Questo metodo simula una reimpostazione del dispositivo, aggiorna le proprietà segnalate locali impostando lo stato su **Success** e rimuove l'elemento **pendingConfig**,</span><span class="sxs-lookup"><span data-stu-id="75b93-138">This method simulates a device reset, then updates the local reported properties setting the status to **Success** and removes the **pendingConfig** element.</span></span> <span data-ttu-id="75b93-139">quindi aggiorna il dispositivo gemello nel servizio.</span><span class="sxs-lookup"><span data-stu-id="75b93-139">It then updates the device twin on the service.</span></span> 

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
                Console.WriteLine("Config change complete \nPress any key to exit.");
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

1. <span data-ttu-id="75b93-140">Aggiungere infine le righe seguenti al metodo **Main**:</span><span class="sxs-lookup"><span data-stu-id="75b93-140">Finally add the following lines to the **Main** method:</span></span>

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
   > <span data-ttu-id="75b93-141">Questa esercitazione non simula alcun comportamento per gli aggiornamenti della configurazione simultanei.</span><span class="sxs-lookup"><span data-stu-id="75b93-141">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="75b93-142">Alcuni processi di aggiornamento della configurazione potrebbero consentire modifiche della configurazione di destinazione mentre l'aggiornamento è in esecuzione, altre potrebbero doverle accodare e altri ancora rifiutarle con una condizione di errore.</span><span class="sxs-lookup"><span data-stu-id="75b93-142">Some configuration update processes might be able to accommodate changes of target configuration while the update is running, some might have to queue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="75b93-143">È importante tenere in considerazione il comportamento desiderato per il processo di configurazione specifico e aggiungere la logica appropriata prima di iniziare la modifica della configurazione.</span><span class="sxs-lookup"><span data-stu-id="75b93-143">Make sure to consider the desired behavior for your specific configuration process, and add the appropriate logic before initiating the configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="75b93-144">Compilare la soluzione e quindi eseguire l'app del dispositivo da Visual Studio facendo clic su **F5**.</span><span class="sxs-lookup"><span data-stu-id="75b93-144">Build the solution and then run the device app from Visual Studio by clicking **F5**.</span></span> <span data-ttu-id="75b93-145">Nella console di output vengono visualizzati i messaggi che indicano che il dispositivo simulato sta recuperando il dispositivo gemello e configurando la telemetria ed è in attesa della modifica della proprietà desiderata.</span><span class="sxs-lookup"><span data-stu-id="75b93-145">On the output console, you should see the messages indicating that your simulated device is retrieving the device twin, setting up the telemetry, and waiting for desired property change.</span></span> <span data-ttu-id="75b93-146">Mantenere l'app in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="75b93-146">Keep the app running.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="75b93-147">Creare l'app di servizio</span><span class="sxs-lookup"><span data-stu-id="75b93-147">Create the service app</span></span>
<span data-ttu-id="75b93-148">In questa sezione si creerà un'app console .NET che aggiorna le *proprietà desiderate* nel dispositivo gemello associato a **myDeviceId** con un nuovo oggetto di configurazione di telemetria.</span><span class="sxs-lookup"><span data-stu-id="75b93-148">In this section, you will create a .NET console app that updates the *desired properties* on the device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="75b93-149">Viene quindi effettuata una query dei dispositivi gemelli archiviati nell'hub IoT e viene visualizzata la differenza tra la configurazione desiderata e quella segnalata del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="75b93-149">It then queries the device twins stored in the IoT hub and shows the difference between the desired and reported configurations of the device.</span></span>

1. <span data-ttu-id="75b93-150">In Visual Studio aggiungere un progetto desktop di Windows classico in Visual C# usando il modello di progetto **Applicazione console** .</span><span class="sxs-lookup"><span data-stu-id="75b93-150">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="75b93-151">Assegnare al progetto il nome **SetDesiredConfigurationAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="75b93-151">Name the project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Nuovo progetto desktop di Windows classico in Visual C#][img-createapp]
1. <span data-ttu-id="75b93-153">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **SetDesiredConfigurationAndQuery** e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="75b93-153">In Solution Explorer, right-click the **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="75b93-154">Nella finestra **Gestione pacchetti NuGet** selezionare **Esplora**, cercare **microsoft.azure.devices**, selezionare **Installa** per installare il pacchetto **Microsoft.Azure.Devices** e accettare le condizioni per l'uso.</span><span class="sxs-lookup"><span data-stu-id="75b93-154">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="75b93-155">Questa procedura scarica, installa e aggiunge un riferimento al [pacchetto NuGet Azure IoT - SDK per dispositivi][lnk-nuget-service-sdk] e alle relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="75b93-155">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Finestra Gestione pacchetti NuGet][img-servicenuget]
1. <span data-ttu-id="75b93-157">Aggiungere le istruzione `using` seguenti all'inizio del file **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="75b93-157">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="75b93-158">Aggiungere i campi seguenti alla classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="75b93-158">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="75b93-159">Sostituire il valore del segnaposto con la stringa di connessione dell'hub IoT creato nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="75b93-159">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="75b93-160">Aggiungere il metodo seguente alla classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="75b93-160">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="75b93-161">L'oggetto **Registry** espone tutti i metodi necessari per interagire con i dispositivi gemelli dal servizio.</span><span class="sxs-lookup"><span data-stu-id="75b93-161">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="75b93-162">Questo codice inizializza l'oggetto **Registry**, recupera il dispositivo gemello per **myDeviceId** e ne aggiorna le proprietà desiderate con un nuovo oggetto di configurazione dei dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="75b93-162">This code initializes the **Registry** object, retrieves the device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="75b93-163">Ogni 10 secondi esegue una query dei dispositivi gemelli archiviati nell'hub IoT e stampa le configurazioni dei dati di telemetria desiderate e segnalate.</span><span class="sxs-lookup"><span data-stu-id="75b93-163">After that, it queries the device twins stored in the IoT hub every 10 seconds, and prints the desired and reported telemetry configurations.</span></span> <span data-ttu-id="75b93-164">Vedere il [linguaggio di query dell'hub IoT][lnk-query] per informazioni su come generare report avanzati in tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="75b93-164">Refer to the [IoT Hub query language][lnk-query] to learn how to generate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="75b93-165">Questa applicazione effettua una query dell'hub IoT ogni 10 secondi a scopo illustrativo.</span><span class="sxs-lookup"><span data-stu-id="75b93-165">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="75b93-166">Usare le query per generare i report destinati all'utente in più dispositivi e non per rilevare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="75b93-166">Use queries to generate user-facing reports across many devices, and not to detect changes.</span></span> <span data-ttu-id="75b93-167">Se la soluzione richiede notifiche in tempo reale degli eventi del dispositivo, usare le [notifiche relative al dispositivo gemello][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="75b93-167">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="75b93-168">Aggiungere infine le righe seguenti al metodo **Main** :</span><span class="sxs-lookup"><span data-stu-id="75b93-168">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery();
        Console.WriteLine("Press any key to quit.");
        Console.ReadLine();
1. <span data-ttu-id="75b93-169">In Esplora soluzioni aprire **Imposta progetti di avvio** e assicurarsi che **Azione** per il progetto **SetDesiredConfigurationAndQuery** sia impostata su **Avvio**.</span><span class="sxs-lookup"><span data-stu-id="75b93-169">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="75b93-170">Compilare la soluzione.</span><span class="sxs-lookup"><span data-stu-id="75b93-170">Build the solution.</span></span>
1. <span data-ttu-id="75b93-171">Con l'app di dispositivo **SimulateDeviceConfiguration** in esecuzione, eseguire l'app di servizio da Visual Studio tramite **F5**.</span><span class="sxs-lookup"><span data-stu-id="75b93-171">With **SimulateDeviceConfiguration** device app running, run the service app from Visual Studio using **F5**.</span></span> <span data-ttu-id="75b93-172">Si potrà osservare la configurazione segnalata passare da **Pending** a **Success** con la nuova frequenza di invio attiva di cinque minuti e non più di 24 ore.</span><span class="sxs-lookup"><span data-stu-id="75b93-172">You should see the reported configuration change from **Pending** to **Success** with the new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Dispositivo configurato correttamente][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="75b93-174">Tra l'operazione relativa al report del dispositivo e il risultato della query si verifica un ritardo fino a un minuto,</span><span class="sxs-lookup"><span data-stu-id="75b93-174">There is a delay of up to a minute between the device report operation and the query result.</span></span> <span data-ttu-id="75b93-175">che consente all'infrastruttura della query di funzionare su una scala molto ampia.</span><span class="sxs-lookup"><span data-stu-id="75b93-175">This is to enable the query infrastructure to work at very high scale.</span></span> <span data-ttu-id="75b93-176">Per recuperare visualizzazioni coerenti di un solo dispositivo gemello, usare il metodo **getDeviceTwin** nella classe **Registry**.</span><span class="sxs-lookup"><span data-stu-id="75b93-176">To retrieve consistent views of a single device twin use the **getDeviceTwin** method in the **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="75b93-177">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="75b93-177">Next steps</span></span>
<span data-ttu-id="75b93-178">In questa esercitazione è stata impostata una configurazione desiderata come *proprietà desiderate* da un back-end della soluzione ed è stata scritta un'app per dispositivo per rilevare tale modifica e simulare un processo di aggiornamento in più fasi che segnala lo stato tramite le proprietà segnalate.</span><span class="sxs-lookup"><span data-stu-id="75b93-178">In this tutorial, you set a desired configuration as *desired properties* from the solution back end, and wrote a device app to detect that change and simulate a multi-step update process reporting its status through the reported properties.</span></span>

<span data-ttu-id="75b93-179">Per altre informazioni, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="75b93-179">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="75b93-180">Per inviare dati di telemetria dai dispositivi, vedere l'esercitazione [Introduzione all'hub IoT][lnk-iothub-getstarted].</span><span class="sxs-lookup"><span data-stu-id="75b93-180">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="75b93-181">Per pianificare o eseguire operazioni su grandi set di dispositivi, vedere l'esercitazione [Pianificare e trasmettere processi][lnk-schedule-jobs].</span><span class="sxs-lookup"><span data-stu-id="75b93-181">schedule or perform operations on large sets of devices see the [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="75b93-182">Per controllare i dispositivi in modo interattivo, ad esempio per attivare un ventilatore da un'app controllata dall'utente, vedere l'esercitazione [Use direct methods][lnk-methods-tutorial] (Usare metodi diretti).</span><span class="sxs-lookup"><span data-stu-id="75b93-182">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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
