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
# <a name="get-started-with-device-twins-netnet"></a>Introduzione ai dispositivi gemelli (.NET/.NET)
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

Alla fine di hello di questa esercitazione, sarà necessario queste App console .NET:

* **CreateDeviceIdentity**, un'app .NET che crea un'identità del dispositivo e protezione della chiave tooconnect app dispositivo simulato.
* **AddTagsAndQuery**, un'app back-end .NET, che aggiunge tag ed effettua una query dei dispositivi gemelli.
* **ReportConnectivity**, un'app di dispositivo .NET che simula un dispositivo che si connette l'hub IoT tooyour con l'identità del dispositivo hello creato in precedenza e segnala la condizione di connettività.

> [!NOTE]
> articolo Hello [Azure IoT SDK] [ lnk-hub-sdks] fornisce informazioni su Azure IoT SDK hello che è possibile utilizzare toobuild applicazioni back-end sia sul dispositivo.
> 
> 

toocomplete questa esercitazione è necessario hello segue:

* Visual Studio 2015 o Visual Studio 2017.
* Un account Azure attivo. Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Se si desidera l'identità del dispositivo hello toocreate a livello di codice in alternativa, leggere una sezione corrispondente di hello in hello [connessione hub IoT tooyour dispositivo simulato utilizzando .NET] [ lnk-device-identity-csharp] articolo.

## <a name="create-hello-service-app"></a>Creare l'applicazione di servizio hello
In questa sezione si crea una console app .NET (tramite c#) che aggiunge un doppio dispositivo toohello metadati posizione associato a **myDeviceId**. Viene quindi gemelli dispositivo hello archiviate nell'hub IoT hello selezionando dispositivi hello che si trovano in hello ci le query e quindi hello quelle che ha segnalato una connessione di rete.

1. In Visual Studio, aggiungere una soluzione di Visual c# Windows Desktop classico progetto toohello corrente utilizzando hello **applicazione Console** modello di progetto. Progetto hello nome **AddTagsAndQuery**.
   
    ![Nuovo progetto desktop di Windows classico in Visual C#][img-createapp]
1. In Esplora soluzioni fare doppio clic su hello **AddTagsAndQuery** del progetto e quindi fare clic su **Gestisci pacchetti NuGet...** .
1. In hello **Gestione pacchetti NuGet** selezionare **Sfoglia** e cercare **microsoft.azure.devices**. Selezionare **installare** tooinstall hello **Microsoft.Azure.Devices** pacchetto e accettare le condizioni di hello d'uso. Questa procedura Scarica, installa e aggiunge un riferimento toohello [SDK di servizi di Azure IoT] [ lnk-nuget-service-sdk] NuGet pacchetto e le relative dipendenze.
   
    ![Finestra Gestione pacchetti NuGet][img-servicenuget]
1. Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:
   
        using Microsoft.Azure.Devices;
1. Aggiungere i seguenti campi toohello hello **programma** classe. Sostituire il valore di segnaposto hello con la stringa di connessione IoT Hub hub hello creato nella sezione precedente hello hello.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. Aggiungere hello seguente metodo toohello **programma** classe:
   
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
   
    Hello **RegistryManager** classe espone tutte hello metodi obbligatorio toointeract con gemelli di dispositivo dal servizio hello. codice precedente Hello inizializza innanzitutto hello **registryManager** dell'oggetto, quindi recupera hello gemelli di dispositivo per **myDeviceId**e infine gli aggiornamenti relativi tag con le informazioni sul percorso hello desiderato.
   
    Dopo l'aggiornamento, vengono eseguite due query: hello dapprima selezionati solo i gemelli dispositivo hello di dispositivi che si trovano in hello **Redmond43** impianto e hello secondo perfeziona hello query tooselect solo hello dispositivi connessi anche tramite rete cellulare.
   
    Si noti il codice precedente hello, durante la creazione di hello **query** dell'oggetto, specifica un numero massimo di documenti restituiti dalla query. Hello **query** oggetto contiene un **HasMoreResults** proprietà booleana che è possibile utilizzare hello tooinvoke **GetNextAsTwinAsync** metodi più volte tooretrieve tutti risultati. Per i risultati che non sono dispositivi gemelli, ad esempio i risultati delle query di aggregazione, è disponibile un metodo chiamato **GetNextAsJson**.
1. Infine, aggiungere hello seguenti righe toohello **Main** metodo:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. In Esplora soluzioni hello, aprire hello **progetti di avvio impostato...**  e verificare che hello **azione** per **AddTagsAndQuery** progetto **avviare**. Compilare la soluzione hello.
1. Eseguire l'applicazione facendo clic su hello **AddTagsAndQuery** progetto, quindi selezionando **Debug**, seguito da **Avvia nuova istanza**. Dovrebbe essere un dispositivo nei risultati di hello per hello porre query per tutti i dispositivi si trovano in **Redmond43** e none per query hello che limita hello risultati toodevices che utilizzano una rete cellulare.
   
    ![Risultati della query nella finestra][img-addtagapp]

Nella sezione successiva hello, si crea un'app per dispositivi vengono fornite informazioni di connettività hello e modifiche hello risultati di query hello nella sezione precedente hello.

## <a name="create-hello-device-app"></a>Creare app per dispositivi hello
In questa sezione si crea un'applicazione console .NET che si connette hub tooyour come **myDeviceId**e quindi aggiorna le informazioni di hello toocontain segnalate le proprietà che è connesso tramite una rete cellulare.

1. In Visual Studio, aggiungere una soluzione di Visual c# Windows Desktop classico progetto toohello corrente utilizzando hello **applicazione Console** modello di progetto. Progetto hello nome **ReportConnectivity**.
   
    ![Nuova app per il dispositivo di Windows classico in Visual C#][img-createdeviceapp]
    
1. In Esplora soluzioni fare doppio clic su hello **ReportConnectivity** del progetto e quindi fare clic su **Gestisci pacchetti NuGet...** .
1. In hello **Gestione pacchetti NuGet** selezionare **Sfoglia** e cercare **microsoft.azure.devices.client**. Selezionare **installare** tooinstall hello **Microsoft.Azure.Devices.Client** pacchetto e accettare le condizioni di hello d'uso. Questa procedura Scarica, installa e aggiunge un riferimento toohello [dispositivo IoT di Azure SDK] [ lnk-nuget-client-sdk] NuGet pacchetto e le relative dipendenze.
   
    ![App client della finestra Gestione pacchetti NuGet][img-clientnuget]
1. Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. Aggiungere i seguenti campi toohello hello **programma** classe. Sostituire il valore di segnaposto hello con stringa di connessione hello dispositivo che si è preso nota nella sezione precedente hello.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. Aggiungere hello seguente metodo toohello **programma** classe:

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

    Hello **Client** oggetto espone tutti i metodi di hello desiderate toointeract con gemelli di dispositivo dal dispositivo hello. Hello codice illustrato in precedenza, inizializza hello **Client** oggetto, quindi recupera hello dispositivo doppi per **myDeviceId**.

1. Aggiungere hello seguente metodo toohello **programma** classe:
   
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

   Hello codice sopra aggiornamenti **myDeviceId**del segnalati proprietà con informazioni sulla connettività hello.

1. Infine, aggiungere hello seguenti righe toohello **Main** metodo:
   
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

1. In Esplora soluzioni hello, aprire hello **progetti di avvio impostato...**  e verificare che hello **azione** per **ReportConnectivity** progetto **avviare**. Compilare la soluzione hello.
1. Eseguire l'applicazione facendo clic su hello **ReportConnectivity** progetto, quindi selezionando **Debug**, seguito da **Avvia nuova istanza**. Si dovrebbe vedere Recupero di informazioni doppi hello e invio di connettività un *segnalati proprietà*.
   
    ![Eseguire la connettività tooreport app per dispositivi][img-rundeviceapp]
    
    
1. Ora che hello dispositivo segnalato le informazioni di connettività, viene visualizzato in entrambe le query. Eseguire .NET hello **AddTagsAndQuery** hello toorun app nuovamente una query. Questa volta **myDeviceId** verrà visualizzato nei risultati di entrambe le query.
   
    ![Connettività del dispositivo segnalata correttamente][img-tagappsuccess]

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, è configurato un nuovo hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità. Aggiunti i metadati del dispositivo come tag da un'app di back-end e ha scritto informazioni di connettività un dispositivo simulato app tooreport dispositivo in un doppio dispositivo hello. È inoltre appreso tooquery queste informazioni usando il linguaggio di query di hello IoT Hub simile a SQL.

Hello utilizzare seguenti come risorse toolearn per:

* inviare i dati di telemetria dai dispositivi con hello [iniziare con l'IoT Hub] [ lnk-iothub-getstarted] esercitazione
* configurare i dispositivi con le proprietà desiderate di un doppio dispositivo hello [lo si desidera utilizzare i dispositivi di proprietà tooconfigure] [ lnk-twin-how-to-configure] esercitazione
* controllare i dispositivi in modo interattivo (ad esempio l'attivazione di una ventola da un'app controllata dall'utente) con hello [utilizzare metodi diretti] [ lnk-methods-tutorial] esercitazione.

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

