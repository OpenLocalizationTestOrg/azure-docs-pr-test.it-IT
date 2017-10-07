---
title: "proprietà di un doppio dispositivo IoT Hub Azure aaaUse (nodo) | Documenti Microsoft"
description: "Come dispositivo di Azure IoT Hub toouse gemelli di tooconfigure dispositivi. È consigliabile utilizzare hello Azure IoT SDK per Node.js tooimplement un'app dispositivo simulato e un'applicazione di servizio che consente di modificare la configurazione di un dispositivo utilizzando una coppia di dispositivo."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: d0bcec50-26e6-40f0-8096-733b2f3071ec
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: elioda
ms.openlocfilehash: 7ebfe2dfa0876bf04fdbaceae55db76456523e8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices-node"></a>Lo si desidera utilizzare proprietà tooconfigure dispositivi (nodo)
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

Alla fine di hello di questa esercitazione, si avranno due applicazioni di console Node.js:

* **SimulateDeviceConfiguration.js**, un'app dispositivo simulato che è in attesa di un aggiornamento della configurazione desiderata e hello Visualizza lo stato di un processo di aggiornamento configurazione simulato.
* **SetDesiredConfigurationAndQuery.js**, configurazione in un dispositivo di un'applicazione back-end di Node. js, che imposta hello desiderato e le query hello il processo di aggiornamento di configurazione.

> [!NOTE]
> articolo Hello [Azure IoT SDK] [ lnk-hub-sdks] fornisce informazioni su Azure IoT SDK hello che è possibile utilizzare toobuild applicazioni back-end sia sul dispositivo.
> 
> 

toocomplete questa esercitazione è necessario hello segue:

* Node.js 0.10.x o versione successiva.
* Un account Azure attivo. Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.

Se si sono seguite hello [introduzione gemelli dispositivo] [ lnk-twin-tutorial] esercitazione, si dispone già di un hub IoT e un'identità del dispositivo chiamato **myDeviceId**; ed è possibile ignorare toohello [ Creare app dispositivo simulato hello] [ lnk-how-to-configure-createapp] sezione.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-simulated-device-app"></a>Creare app dispositivo simulato hello
In questa sezione si crea un'applicazione console Node.js che si connette hub tooyour come **myDeviceId**, in attesa di un aggiornamento della configurazione desiderata e quindi segnala gli aggiornamenti nel processo di aggiornamento configurazione hello simulato.

1. Creare una nuova cartella vuota denominata **simulatedeviceconfiguration**. In hello **simulatedeviceconfiguration** cartella, creare un nuovo file package. JSON utilizzando hello seguente comando al prompt dei comandi. Accettare tutte le impostazioni predefinite hello:
   
    ```
    npm init
    ```
2. Al prompt dei comandi in hello **simulatedeviceconfiguration** cartella, eseguire hello successivo comando tooinstall hello **dispositivi iot di azure**, e **azure-iot-dispositivo-mqtt**pacchetto:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Utilizzando un editor di testo, creare un nuovo **SimulateDeviceConfiguration.js** file hello **simulatedeviceconfiguration** cartella.
4. Aggiungere hello seguente codice toohello **SimulateDeviceConfiguration.js** file e sostituire hello **{stringa di connessione dispositivo}** segnaposto con stringa di connessione dispositivo hello copiato quando si creato hello **myDeviceId** identità del dispositivo:
   
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
   
    Hello **Client** oggetto espone tutte hello metodi obbligatorio toointeract con gemelli di dispositivo dal dispositivo hello. Hello codice precedente, dopo l'inizializzazione hello **Client** oggetto recupera hello gemelli di dispositivo per **myDeviceId**e associa un gestore per l'aggiornamento di hello nella proprietà desiderate. gestore Hello verifica che sia presente una richiesta di modifica della configurazione effettiva confrontando configIds hello, quindi richiama un metodo che avvia una modifica della configurazione hello.
   
    Si noti che per i migliori risultati hello di semplicità, codice precedente hello Usa valore predefinito è hardcoded per la configurazione iniziale di hello. Una vera app probabilmente caricherebbe tale configurazione da una risorsa di archiviazione locale.
   
   > [!IMPORTANT]
   > Gli eventi di modifica delle proprietà desiderati vengono sempre inviati una volta alla connessione del dispositivo, assicurarsi che vi sia una modifica effettiva in hello toocheck le proprietà desiderate prima di eseguire qualsiasi azione.
   > 
   > 
5. Aggiungere i seguenti metodi prima hello hello `client.open()` chiamata:
   
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
   
    Hello **initConfigChange** metodo aggiorna segnalati proprietà sull'oggetto di un doppio hello dispositivo locale con hello richiesta di aggiornamento della configurazione e set hello stato troppo**in sospeso**, quindi gli aggiornamenti hello dispositivo doppio servizio hello. Dopo aver aggiornato correttamente un doppio dispositivo hello, simula un processo a esecuzione prolungata che termina l'esecuzione di hello **completeConfigChange**. Questo metodo aggiornamenti hello dispositivo locale disponibilità di una copia del segnalato le proprietà di impostazione dello stato di hello troppo**successo** e rimozione di hello **pendingConfig** oggetto. Viene quindi aggiornato doppi dispositivo hello sul servizio hello.
   
    Si noti che, della larghezza di banda toosave segnalati proprietà vengono aggiornate specificando solo hello proprietà toobe modificato (denominato **patch** in hello sopra codice), anziché sostituire hello intero documento.
   
   > [!NOTE]
   > Questa esercitazione non simula alcun comportamento per gli aggiornamenti della configurazione simultanei. Alcuni processi di aggiornamento configurazione potrebbero essere in grado di tooaccommodate modifiche della configurazione di destinazione durante l'esecuzione di aggiornamento hello, altri utenti potrebbe essere tooqueue e su altri possibile rifiutarli con una condizione di errore. Verificare che tooconsider hello comportamento desiderato per il processo di configurazione specifica e aggiungere la logica appropriata hello prima dell'avvio di modifica della configurazione hello.
   > 
   > 
6. Eseguire app per dispositivi hello:
   
        node SimulateDeviceConfiguration.js
   
    Verrà visualizzato il messaggio hello `retrieved device twin`. Mantenere hello app in esecuzione.

## <a name="create-hello-service-app"></a>Creare l'applicazione di servizio hello
In questa sezione si creerà un'applicazione console in Node.js tale hello aggiornamenti *le proprietà desiderate* su hello gemelli di dispositivo associati **myDeviceId** con un nuovo oggetto di configurazione di telemetria. Quindi esegue una query gemelli dispositivo hello archiviate nell'hub IoT hello e Mostra differenza hello tra hello desiderato e le configurazioni di dispositivo hello segnalato.

1. Creare una nuova cartella vuota denominata **setdesiredandqueryapp**. In hello **setdesiredandqueryapp** cartella, creare un nuovo file package. JSON utilizzando hello seguente comando al prompt dei comandi. Accettare tutte le impostazioni predefinite hello:
   
    ```
    npm init
    ```
2. Al prompt dei comandi in hello **setdesiredandqueryapp** cartella, eseguire hello successivo comando tooinstall hello **hub IOT di azure** pacchetto:
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. Utilizzando un editor di testo, creare un nuovo **SetDesiredAndQuery.js** file hello **addtagsandqueryapp** cartella.
4. Aggiungere i seguenti toohello codice hello **SetDesiredAndQuery.js** file e sostituire hello **{stringa di connessione hub iot}** segnaposto con hello stringa di connessione IoT Hub è stato copiato al momento della creazione dell'hub :
   
        'use strict';
        var iothub = require('azure-iothub');
        var uuid = require('node-uuid');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var newConfigId = uuid.v4();
                var newFrequency = process.argv[2] || "5m";
                var patch = {
                    properties: {
                        desired: {
                            telemetryConfig: {
                                configId: newConfigId,
                                sendFrequency: newFrequency
                            }
                        }
                    }
                }
                twin.update(patch, function(err) {
                    if (err) {
                        console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                    } else {
                        console.log(twin.deviceId + ' twin updated successfully');
                    }
                });
                setInterval(queryTwins, 10000);
            }
        });

    Hello **Registro di sistema** oggetto espone tutte hello metodi obbligatorio toointeract con gemelli di dispositivo dal servizio hello. Hello codice precedente, dopo l'inizializzazione hello **Registro di sistema** oggetto recupera hello gemelli di dispositivo per **myDeviceId**e aggiorna le proprietà desiderate con un nuovo oggetto di configurazione di telemetria. Successivamente, chiama hello **queryTwins** funzione evento 10 secondi.

    > [!IMPORTANT]
    > Questa applicazione effettua una query dell'hub IoT ogni 10 secondi a scopo illustrativo. Utilizzare una query toogenerate rivolta all'utente report tra più dispositivi e non toodetect modifiche. Se la soluzione richiede notifiche in tempo reale degli eventi del dispositivo, usare le [notifiche relative al dispositivo gemello][lnk-twin-notifications].
    > 
    >.

1. Aggiungere hello seguente di codice subito prima di hello `registry.getDeviceTwin()` hello tooimplement chiamata **queryTwins** funzione:
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log();
                    results.forEach(function(twin) {
                        var desiredConfig = twin.properties.desired.telemetryConfig;
                        var reportedConfig = twin.properties.reported.telemetryConfig;
                        console.log("Config report for: " + twin.deviceId);
                        console.log("Desired: ");
                        console.log(JSON.stringify(desiredConfig, null, 2));
                        console.log("Reported: ");
                        console.log(JSON.stringify(reportedConfig, null, 2));
                    });
                }
            });
        };
   
    query di codice precedenti Hello hello gemelli dispositivo memorizzato nell'hub IoT hello e stampa hello desiderato e segnalate le configurazioni di telemetria. Fare riferimento toohello [il linguaggio di query di IoT Hub] [ lnk-query] toolearn come rich toogenerate report tra tutti i dispositivi.
2. Con **SimulateDeviceConfiguration.js** in esecuzione, eseguire un'applicazione hello con:
   
        node SetDesiredAndQuery.js 5m
   
    Dovrebbe essere hello segnalati configurazione modificare da **esito positivo** troppo**in sospeso** troppo**successo** nuovamente Active nuovo hello frequenza di invio dei cinque minuti anziché 24 ore.
   
   > [!IMPORTANT]
   > Si verifica un ritardo di backup tooa minuto tra funzionamento del report dispositivo hello e risultato della query hello. Si tratta di tooenable hello query infrastruttura toowork su larga scala molto elevata. viste di un doppio di un singolo dispositivo consistenza tooretrieve utilizzano hello **getDeviceTwin** metodo hello **Registro di sistema** classe.
   > 
   > 

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, impostare una configurazione desiderata come *le proprietà desiderate* da un'app di back-end e ha scritto un toodetect app dispositivo simulato che modificano e simulare un processo di aggiornamento di più passaggi reporting stato  *proprietà segnalati* toohello gemelli di dispositivo.

Hello utilizzare seguenti come risorse toolearn per:

* inviare i dati di telemetria dai dispositivi con hello [iniziare con l'IoT Hub] [ lnk-iothub-getstarted] esercitazione
* pianificare o eseguire operazioni su grandi set di dispositivi Vedere hello [pianificazione e i processi di broadcast] [ lnk-schedule-jobs] esercitazione.
* controllare i dispositivi in modo interattivo (ad esempio l'attivazione di una ventola da un'app controllata dall'utente), con hello [utilizzare metodi diretti] [ lnk-methods-tutorial] esercitazione.

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

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
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-node-node-twin-how-to-configure.md#create-the-simulated-device-app
