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
# <a name="use-desired-properties-tooconfigure-devices"></a>Utilizzare i dispositivi di proprietà desiderato tooconfigure
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

Alla fine di hello di questa esercitazione, si avranno due applicazioni di console .NET:

* **SimulateDeviceConfiguration**, un'app dispositivo simulato che è in attesa di un aggiornamento della configurazione desiderata e hello Visualizza lo stato di un processo di aggiornamento configurazione simulato.
* **SetDesiredConfigurationAndQuery**, configurazione in un dispositivo di un'applicazione back-end, che imposta hello desiderato e le query hello il processo di aggiornamento di configurazione.

> [!NOTE]
> articolo Hello [Azure IoT SDK] [ lnk-hub-sdks] fornisce informazioni su Azure IoT SDK hello che è possibile utilizzare toobuild applicazioni back-end sia sul dispositivo.
> 
> 

toocomplete questa esercitazione è necessario hello segue:

* Visual Studio 2015 o Visual Studio 2017.
* Un account Azure attivo. Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.

Se si sono seguite hello [introduzione gemelli dispositivo] [ lnk-twin-tutorial] esercitazione, si dispone già di un hub IoT e un'identità del dispositivo chiamato **myDeviceId**. In tal caso, è possibile ignorare toohello [crea hello dispositivo simulato applicazione] [ lnk-how-to-configure-createapp] sezione.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a>Creare app dispositivo simulato hello
In questa sezione si crea un'applicazione console .NET che si connette hub tooyour come **myDeviceId**, in attesa di un aggiornamento della configurazione desiderata e quindi segnala gli aggiornamenti nel processo di aggiornamento configurazione hello simulato.

1. In Visual Studio, creare un nuovo progetto di Visual c# Windows Desktop classico utilizzando hello **applicazione Console** modello di progetto. Progetto hello nome **SimulateDeviceConfiguration**.
   
    ![Nuova app per il dispositivo di Windows classico in Visual C#][img-createdeviceapp]

1. In Esplora soluzioni fare doppio clic su hello **SimulateDeviceConfiguration** del progetto e quindi fare clic su **Gestisci pacchetti NuGet...** .
1. In hello **Gestione pacchetti NuGet** selezionare **Sfoglia** e cercare **microsoft.azure.devices.client**. Selezionare **installare** tooinstall hello **Microsoft.Azure.Devices.Client** pacchetto e accettare le condizioni di hello d'uso. Questa procedura Scarica, installa e aggiunge un riferimento toohello [dispositivo IoT di Azure SDK] [ lnk-nuget-client-sdk] NuGet pacchetto e le relative dipendenze.
   
    ![App client della finestra Gestione pacchetti NuGet][img-clientnuget]
1. Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. Aggiungere i seguenti campi toohello hello **programma** classe. Sostituire il valore di segnaposto hello con stringa di connessione hello dispositivo che si è preso nota nella sezione precedente hello.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();

1. Aggiungere hello seguente metodo toohello **programma** classe:
 
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
    Hello **Client** oggetto espone tutti i metodi di hello desiderate toointeract con gemelli di dispositivo dal dispositivo hello. Hello codice illustrato in precedenza, inizializza hello **Client** oggetto, quindi recupera hello dispositivo doppi per **myDeviceId**.

1. Aggiungere hello seguente metodo toohello **programma** classe. Questo metodo imposta i valori iniziali di hello di telemetria sul dispositivo locale hello e quindi gli aggiornamenti hello gemelli di dispositivo.

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

1. Aggiungere hello seguente metodo toohello **programma** classe. Si tratta di un callback che rileva una modifica in *le proprietà desiderate* in un doppio dispositivo hello.

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

    Questo hello aggiornamenti metodo segnalato le proprietà sull'oggetto di un doppio hello dispositivo locale con la configurazione di hello richiesta e imposta lo stato di hello di aggiornamento troppo**in sospeso**, quindi gli aggiornamenti hello gemelli di dispositivo nel servizio hello. Dopo aver aggiornato correttamente un doppio dispositivo hello, completamento di modifica della configurazione hello chiamando il metodo hello `CompleteConfigChange` descritta al punto successivo hello.

1. Aggiungere hello seguente metodo toohello **programma** classe. Questo metodo simula un ripristino del dispositivo, quindi gli aggiornamenti hello proprietà segnalate locale impostazione dello stato di hello troppo**successo** e rimuove hello **pendingConfig** elemento. Viene quindi aggiornato doppi dispositivo hello sul servizio hello. 

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

1. Aggiungere infine hello seguenti righe toohello **Main** metodo:

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
   > Questa esercitazione non simula alcun comportamento per gli aggiornamenti della configurazione simultanei. Alcuni processi di aggiornamento configurazione potrebbero essere in grado di tooaccommodate modifiche della configurazione di destinazione durante l'esecuzione di aggiornamento hello, alcuni potrebbe essere tooqueue mentre altri possibile rifiutarli con una condizione di errore. Verificare che tooconsider hello comportamento desiderato per il processo di configurazione specifica e aggiungere la logica appropriata hello prima dell'avvio di modifica della configurazione hello.
   > 
   > 
1. Compilare la soluzione hello ed eseguire hello dispositivo app da Visual Studio, fare clic su **F5**. Nella console di output di hello, dovrebbe essere messaggi hello che indica che il dispositivo simulato è il recupero di un doppio dispositivo hello, impostazione dati di telemetria hello e in attesa di modifica della proprietà desiderata. Mantenere hello app in esecuzione.

## <a name="create-hello-service-app"></a>Creare l'applicazione di servizio hello
In questa sezione si creerà un'applicazione console .NET che hello aggiornamenti *le proprietà desiderate* su hello gemelli di dispositivo associati **myDeviceId** con un nuovo oggetto di configurazione di telemetria. Quindi esegue una query gemelli dispositivo hello archiviate nell'hub IoT hello e Mostra differenza hello tra hello desiderato e le configurazioni di dispositivo hello segnalato.

1. In Visual Studio, aggiungere una soluzione di Visual c# Windows Desktop classico progetto toohello corrente utilizzando hello **applicazione Console** modello di progetto. Progetto hello nome **SetDesiredConfigurationAndQuery**.
   
    ![Nuovo progetto desktop di Windows classico in Visual C#][img-createapp]
1. In Esplora soluzioni fare doppio clic su hello **SetDesiredConfigurationAndQuery** del progetto e quindi fare clic su **Gestisci pacchetti NuGet...** .
1. In hello **Gestione pacchetti NuGet** selezionare **Sfoglia**, cercare **microsoft.azure.devices**selezionare **installare** tooinstall Hello **Microsoft.Azure.Devices** pacchetto e accettare le condizioni di hello d'uso. Questa procedura Scarica, installa e aggiunge un riferimento toohello [SDK di servizi di Azure IoT] [ lnk-nuget-service-sdk] NuGet pacchetto e le relative dipendenze.
   
    ![Finestra Gestione pacchetti NuGet][img-servicenuget]
1. Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. Aggiungere i seguenti campi toohello hello **programma** classe. Sostituire il valore di segnaposto hello con la stringa di connessione IoT Hub hub hello creato nella sezione precedente hello hello.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. Aggiungere hello seguente metodo toohello **programma** classe:
   
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
   
    Hello **Registro di sistema** oggetto espone tutte hello metodi obbligatorio toointeract con gemelli di dispositivo dal servizio hello. Questo codice inizializza hello **Registro di sistema** oggetto recupera hello gemelli di dispositivo per **myDeviceId**e quindi aggiorna le proprietà desiderate con un nuovo oggetto di configurazione di telemetria.
    Successivamente, viene eseguita una query gemelli dispositivo hello archiviate nell'hub IoT hello ogni 10 secondi e stampa hello desiderato e segnalate le configurazioni di telemetria. Fare riferimento toohello [il linguaggio di query di IoT Hub] [ lnk-query] toolearn come rich toogenerate report tra tutti i dispositivi.
   
   > [!IMPORTANT]
   > Questa applicazione effettua una query dell'hub IoT ogni 10 secondi a scopo illustrativo. Utilizzare una query toogenerate rivolta all'utente report tra più dispositivi e non toodetect modifiche. Se la soluzione richiede notifiche in tempo reale degli eventi del dispositivo, usare le [notifiche relative al dispositivo gemello][lnk-twin-notifications].
   > 
   > 
1. Infine, aggiungere hello seguenti righe toohello **Main** metodo:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. In Esplora soluzioni hello, aprire hello **progetti di avvio impostato...**  e verificare che hello **azione** per **SetDesiredConfigurationAndQuery** progetto **avviare**. Compilare la soluzione hello.
1. Con **SimulateDeviceConfiguration** dispositivo che esegue di app, hello esecuzione del servizio app da Visual Studio tramite **F5**. Dovrebbe essere hello segnalati configurazione modificare da **in sospeso** troppo**successo** Active nuovo hello frequenza di invio dei cinque minuti invece di 24 ore.

 ![Dispositivo configurato correttamente][img-deviceconfigured]
   
   > [!IMPORTANT]
   > Si verifica un ritardo di backup tooa minuto tra funzionamento del report dispositivo hello e risultato della query hello. Si tratta di tooenable hello query infrastruttura toowork su larga scala molto elevata. viste di un doppio di un singolo dispositivo consistenza tooretrieve utilizzano hello **getDeviceTwin** metodo hello **Registro di sistema** classe.
   > 
   > 

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, impostare una configurazione desiderata come *le proprietà desiderate* dalla soluzione hello back-end e ha scritto un toodetect app dispositivo che modificano e simulare un processo di aggiornamento di più passaggi tramite hello segnalato lo stato di creazione di report proprietà.

Hello utilizzare seguenti come risorse toolearn per:

* inviare i dati di telemetria dai dispositivi con hello [iniziare con l'IoT Hub] [ lnk-iothub-getstarted] esercitazione
* pianificare o eseguire operazioni su grandi set di dispositivi Vedere hello [pianificazione e i processi di broadcast] [ lnk-schedule-jobs] esercitazione.
* controllare i dispositivi in modo interattivo (ad esempio l'attivazione di una ventola da un'app controllata dall'utente), con hello [utilizzare metodi diretti] [ lnk-methods-tutorial] esercitazione.

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
