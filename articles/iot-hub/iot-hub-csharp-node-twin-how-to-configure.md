---
title: "proprietà di un doppio dispositivo IoT Hub Azure aaaUse (.NET/nodo) | Documenti Microsoft"
description: Come dispositivo di Azure IoT Hub toouse gemelli di tooconfigure dispositivi. Utilizzare il dispositivo di Azure IoT hello SDK per Node.js tooimplement un'app dispositivo simulato e hello Azure IoT servizio SDK per .NET tooimplement un'applicazione di servizio che consente di modificare la configurazione di un dispositivo utilizzando una coppia di dispositivo.
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
ms.openlocfilehash: 840a1b2e45f4763131299577583aa89015dcdd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a>Utilizzare i dispositivi di proprietà desiderato tooconfigure
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

Alla fine di hello di questa esercitazione, si avranno due applicazioni console:

* **SimulateDeviceConfiguration.js**, un'app dispositivo simulato che è in attesa di un aggiornamento della configurazione desiderata e hello Visualizza lo stato di un processo di aggiornamento configurazione simulato.
* **SetDesiredConfigurationAndQuery**, configurazione in un dispositivo di un'app di back-end .NET, che imposta hello desiderato e le query hello il processo di aggiornamento di configurazione.

> [!NOTE]
> articolo Hello [Azure IoT SDK] [ lnk-hub-sdks] fornisce informazioni su Azure IoT SDK hello che è possibile utilizzare toobuild applicazioni back-end sia sul dispositivo.
> 
> 

toocomplete questa esercitazione è necessario hello segue:

* Visual Studio 2015 o Visual Studio 2017.
* Node.js 0.10.x o versione successiva.
* Un account Azure attivo. Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.

Se si sono seguite hello [introduzione gemelli dispositivo] [ lnk-twin-tutorial] esercitazione, si dispone già di un hub IoT e un'identità del dispositivo chiamato **myDeviceId**. In tal caso, è possibile ignorare toohello [crea hello dispositivo simulato applicazione] [ lnk-how-to-configure-createapp] sezione.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a>Creare app dispositivo simulato hello
In questa sezione si crea un'applicazione console Node.js che si connette hub tooyour come **myDeviceId**, in attesa di un aggiornamento della configurazione desiderata e quindi segnala gli aggiornamenti nel processo di aggiornamento configurazione hello simulato.

1. Creare una nuova cartella vuota denominata **simulatedeviceconfiguration**. In hello **simulatedeviceconfiguration** cartella, creare un nuovo file package. JSON utilizzando hello seguente comando al prompt dei comandi. Accettare tutte le impostazioni predefinite hello.
   
    ```
    npm init
    ```
1. Al prompt dei comandi in hello **simulatedeviceconfiguration** cartella, eseguire hello successivo comando tooinstall hello **dispositivi iot di azure** e **azure-iot-dispositivo-mqtt**pacchetti:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. Utilizzando un editor di testo, creare un nuovo **SimulateDeviceConfiguration.js** file hello **simulatedeviceconfiguration** cartella.
1. Aggiungere hello seguente codice toohello **SimulateDeviceConfiguration.js** file e sostituire hello **{stringa di connessione dispositivo}** segnaposto con stringa di connessione dispositivo hello copiato quando si creato hello **myDeviceId** identità del dispositivo:
   
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
   
    Hello **Client** oggetto espone tutte hello metodi obbligatorio toointeract con gemelli di dispositivo dal dispositivo hello. Questo codice inizializza hello **Client** oggetto recupera hello gemelli di dispositivo per **myDeviceId**e quindi associa un gestore per l'aggiornamento di hello in *le proprietà desiderate*. gestore Hello verifica che sia presente una richiesta di modifica della configurazione effettiva confrontando configIds hello, quindi richiama un metodo che avvia una modifica della configurazione hello.
   
    Si noti che per i migliori risultati hello di semplicità, questo codice Usa valore predefinito è hardcoded per la configurazione iniziale di hello. Una vera app probabilmente caricherebbe tale configurazione da una risorsa di archiviazione locale.
   
   > [!IMPORTANT]
   > Gli eventi di modifica delle proprietà desiderate vengono inviati sempre una volta sola alla connessione al dispositivo. Assicurarsi che vi sia una modifica effettiva in hello toocheck le proprietà desiderate prima di eseguire qualsiasi azione.
   > 
   > 
1. Aggiungere i seguenti metodi prima hello hello `client.open()` chiamata:
   
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
   
    Hello **initConfigChange** metodo aggiornamenti hello segnalato le proprietà sull'oggetto di un doppio hello dispositivo locale con la configurazione di hello richiesta e imposta lo stato di hello di aggiornamento troppo**in sospeso**, quindi hello aggiornamenti doppio dispositivo nel servizio hello. Dopo aver aggiornato correttamente un doppio dispositivo hello, simula un processo a esecuzione prolungata che termina l'esecuzione di hello **completeConfigChange**. Questo metodo aggiorna hello segnalate le proprietà locali impostazione dello stato di hello troppo**successo** e rimozione di hello **pendingConfig** oggetto. Viene quindi aggiornato doppi dispositivo hello sul servizio hello.
   
    Si noti che, della larghezza di banda toosave segnalati proprietà vengono aggiornate specificando solo hello proprietà toobe modificato (denominato **patch** in hello sopra codice), anziché sostituire hello intero documento.
   
   > [!NOTE]
   > Questa esercitazione non simula alcun comportamento per gli aggiornamenti della configurazione simultanei. Alcuni processi di aggiornamento configurazione potrebbero essere in grado di tooaccommodate modifiche della configurazione di destinazione durante l'esecuzione di aggiornamento hello, alcuni potrebbe essere tooqueue mentre altri possibile rifiutarli con una condizione di errore. Verificare che tooconsider hello comportamento desiderato per il processo di configurazione specifica e aggiungere la logica appropriata hello prima dell'avvio di modifica della configurazione hello.
   > 
   > 
1. Eseguire app per dispositivi hello:
   
        node SimulateDeviceConfiguration.js
   
    Verrà visualizzato il messaggio hello `retrieved device twin`. Mantenere hello app in esecuzione.

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
   
    Hello **Registro di sistema** oggetto espone tutte hello metodi obbligatorio toointeract con gemelli di dispositivo dal servizio hello. Questo codice inizializza hello **Registro di sistema** oggetto recupera hello gemelli di dispositivo per **myDeviceId**e quindi aggiorna le proprietà desiderate con un nuovo oggetto di configurazione di telemetria.
    Successivamente, viene eseguita una query gemelli dispositivo hello archiviate nell'hub IoT hello ogni 10 secondi e stampa hello desiderato e segnalate le configurazioni di telemetria. Fare riferimento toohello [il linguaggio di query di IoT Hub] [ lnk-query] toolearn come rich toogenerate report tra tutti i dispositivi.
   
   > [!IMPORTANT]
   > Questa applicazione effettua una query dell'hub IoT ogni 10 secondi a scopo illustrativo. Utilizzare una query toogenerate rivolta all'utente report tra più dispositivi e non toodetect modifiche. Se la soluzione richiede notifiche in tempo reale degli eventi del dispositivo, usare le [notifiche relative al dispositivo gemello][lnk-twin-notifications].
   > 
   > 
1. Infine, aggiungere hello seguenti righe toohello **Main** metodo:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery().Wait();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. In Esplora soluzioni hello, aprire hello **progetti di avvio impostato...**  e verificare che hello **azione** per **SetDesiredConfigurationAndQuery** progetto **avviare**. Compilare la soluzione hello.
1. Con **SimulateDeviceConfiguration.js** in esecuzione, eseguire un'applicazione hello .NET da Visual Studio tramite **F5** dovrebbe essere possibile visualizzare hello segnalati configurazione modificare da **successo** troppo**in sospeso** troppo**successo** nuovamente Active nuovo hello frequenza di invio dei cinque minuti invece di 24 ore.

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
