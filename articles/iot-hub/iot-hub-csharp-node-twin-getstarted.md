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
ms.date: 09/07/2017
ms.author: elioda
ms.openlocfilehash: 4cf607e8e0ccd3aab06be54d715c2bf3777caeb0
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="get-started-with-device-twins-netnode"></a>Introduzione ai dispositivi gemelli (.NET/Node)
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

Con questa esercitazione vengono create un'app console Node.js e un'app console .NET:

* **AddTagsAndQuery.sln**, un'app back-end .NET, che aggiunge tag ed effettua una query dei dispositivi gemelli.
* **TwinSimulatedDevice.js**, un'app Node.js che simula un dispositivo che si connette all'hub IoT con l'identità del dispositivo creata prima e segnala la condizione della connettività.

> [!NOTE]
> L'articolo [Azure IoT SDK][lnk-hub-sdks] contiene informazioni sui componenti Azure IoT SDK che consentono di compilare le app back-end e per dispositivi.
> 
> 

Per completare l'esercitazione, sono necessari gli elementi seguenti:

* Visual Studio 2015 o Visual Studio 2017.
* Node.js 4.0.x o versione successiva.
* Un account Azure attivo. Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-service-app"></a>Creare l'app di servizio
In questa sezione si crea un'app console .NET (usando C#) e si aggiungono i metadati della posizione al dispositivo gemello associato a **myDeviceId**. Viene quindi eseguita una query nei dispositivi gemelli archiviati nell'hub IoT selezionando i dispositivi situati negli Stati Uniti e quindi quelli che segnalano una rete cellulare.

1. In Visual Studio aggiungere un progetto desktop di Windows classico in Visual C# usando il modello di progetto **Applicazione console** . Assegnare al progetto il nome **AddTagsAndQuery**.
   
    ![Nuovo progetto desktop di Windows classico in Visual C#][img-createapp]
1. In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **AddTagsAndQuery** e quindi fare clic su **Gestisci pacchetti NuGet**.
1. Nella finestra **Gestisci pacchetti NuGet** selezionare **Sfoglia** e cercare **microsoft.azure.devices**. Selezionare **Installa** per installare il pacchetto **Microsoft.Azure.Devices** e accettare le condizioni per l'utilizzo. Questa procedura scarica, installa e aggiunge un riferimento al [pacchetto NuGet Azure IoT - SDK per dispositivi][lnk-nuget-service-sdk] e alle relative dipendenze.
   
    ![Finestra Gestione pacchetti NuGet][img-servicenuget]
1. Aggiungere le istruzione `using` seguenti all'inizio del file **Program.cs** :
   
        using Microsoft.Azure.Devices;
1. Aggiungere i campi seguenti alla classe **Program** . Sostituire il valore del segnaposto con la stringa di connessione dell'hub IoT creato nella sezione precedente.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. Aggiungere il metodo seguente alla classe **Program** :
   
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
   
    L'oggetto **RegistryManager** espone tutti i metodi necessari per interagire con i dispositivi gemelli dal servizio. Il codice precedente inizializza prima di tutto l'oggetto **registryManager**, quindi recupera il dispositivo gemello per **myDeviceId** e infine ne aggiorna i tag con le informazioni sulla posizione desiderate.
   
    Dopo l'aggiornamento, il codice precedente esegue due query: la prima seleziona solo i dispositivi gemelli tra quelli situati nello stabilimento **Redmond43** e la seconda affina la query per selezionare solo i dispositivi che sono connessi anche tramite la rete cellulare.
   
    Si noti che il codice precedente, quando crea l'oggetto **query**, specifica un numero massimo di documenti restituiti. L'oggetto **query** contiene una proprietà booleana **HasMoreResults** che è possibile usare per richiamare i metodi **GetNextAsTwinAsync** più volte per recuperare tutti i risultati. Per i risultati che non sono dispositivi gemelli, ad esempio i risultati delle query di aggregazione, è disponibile un metodo chiamato **GetNextAsJson**.
1. Aggiungere infine le righe seguenti al metodo **Main** :
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. In Esplora soluzioni aprire **Imposta progetti di avvio** e assicurarsi che **Azione** per il progetto **AddTagsAndQuery** sia impostata su **Avvio**. Compilare la soluzione.
1. Eseguire l'applicazione facendo clic con il pulsante destro del mouse sul progetto **AddTagsAndQuery** e selezionando **Debug**, seguito da **Avvia nuova istanza**. Nei risultati si noterà un dispositivo per la query che cerca tutti i dispositivi situati in **Redmond43** e nessuno per la query che limita i risultati ai dispositivi che usano una rete cellulare.
   
    ![Risultati della query nella finestra][img-addtagapp]

Nella sezione successiva si crea un'app per dispositivo che segnala le informazioni sulla connettività e modifica il risultato della query nella sezione precedente.

## <a name="create-the-device-app"></a>Creare l'app per dispositivo
In questa sezione si crea un'app console Node.js che si connette all'hub come **myDeviceId** e quindi aggiorna le proprietà segnalate per poter contenere le informazioni relative alla connessione usando una rete cellulare.

1. Creare una nuova cartella vuota denominata **reportconnectivity**. Nella cartella **reportconnectivity** creare un nuovo file package.json immettendo il comando seguente al prompt dei comandi. Accettare tutte le impostazioni predefinite.
   
    ```
    npm init
    ```
1. Eseguire questo comando al prompt dei comandi nella cartella **reportconnectivity** per installare i pacchetti **azure-iot-device** e **azure-iot-device-mqtt**:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. Usando un editor di testo, creare un nuovo file **ReportConnectivity.js** nella cartella **reportconnectivity**.
1. Aggiungere il codice seguente al file **ReportConnectivity.js** e sostituire il segnaposto per la stringa di connessione al dispositivo con quello copiato quando è stata creata l'identità del dispositivo **myDeviceId**:
   
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
   
    L'oggetto **Client** espone tutti i metodi necessari per interagire con i dispositivi gemelli dal dispositivo. Il codice precedente, dopo avere inizializzato l'oggetto **Client**, recupera il dispositivo gemello per **myDeviceId** e aggiorna le proprietà segnalate con le informazioni sulla connettività.
1. Eseguire l'app per dispositivo
   
        node ReportConnectivity.js
   
    Dovrebbe essere visualizzato il messaggio `twin state reported`.
1. Ora che il dispositivo ha segnalato le informazioni sulla connettività, verrà visualizzato in entrambe le query. Eseguire l'app .NET **AddTagsAndQuery** per eseguire nuovamente la query. Questa volta **myDeviceId** verrà visualizzato nei risultati di entrambe le query.
   
    ![][img-addtagapp2]

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione è stato configurato un nuovo hub IoT nel Portale di Azure ed è stata quindi creata un'identità del dispositivo nel registro di identità dell'hub IoT. Sono stati aggiunti i metadati del dispositivo come tag da un'app back-end ed è stata scritta un'app per dispositivo simulato per segnalare le informazioni sulla connettività del dispositivo nel dispositivo gemello. Si è anche appreso come effettuare una query di queste informazioni usando il linguaggio di query simile a SQL dell'hub IoT.

Per altre informazioni, vedere le risorse seguenti:

* Per inviare dati di telemetria dai dispositivi, vedere l'esercitazione [Introduzione all'hub IoT][lnk-iothub-getstarted].
* Per configurare i dispositivi usando le proprietà desiderate del dispositivo gemello, vedere l'esercitazione [Usare le proprietà desiderate per configurare i dispositivi][lnk-twin-how-to-configure].
* Per controllare i dispositivi in modo interattivo, ad esempio per attivare un ventilatore da un'app controllata dall'utente, vedere l'esercitazione [Use direct methods][lnk-methods-tutorial] (Usare metodi diretti).

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

