---
title: aaaGet introduttiva gemelli dispositivi Azure IoT Hub (nodo) | Documenti Microsoft
description: "Modalità toouse IoT Hub Azure dispositivo gemelli tooadd tag e quindi utilizzare una query di IoT Hub. Utilizzare hello IoT di Azure SDK per Node.js tooimplement hello dispositivo simulato app e un'applicazione di servizio che consente di aggiungere tag hello ed esegue query IoT Hub hello."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: 314c88e4-cce1-441c-b75a-d2e08e39ae7d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.openlocfilehash: d60b8c3de85e9285e496b86e27d4ee31a0554a1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-node"></a>Introduzione ai dispositivi gemelli (Node)
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

Alla fine di hello di questa esercitazione, si avranno due applicazioni di console Node.js:

* **AddTagsAndQuery.js**, un'app back-end di Node.js, che aggiunge tag ed esegue query sui dispositivi gemelli.
* **TwinSimulatedDevice.js**, un'app Node.js che simula un dispositivo che si connette l'hub IoT tooyour con l'identità del dispositivo hello creato in precedenza e segnala la condizione di connettività.

> [!NOTE]
> articolo Hello [Azure IoT SDK] [ lnk-hub-sdks] fornisce informazioni su Azure IoT SDK hello che è possibile utilizzare toobuild applicazioni back-end sia sul dispositivo.
> 
> 

toocomplete questa esercitazione è necessario hello segue:

* Node.js 0.10.x o versione successiva.
* Un account Azure attivo. Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a>Creare l'applicazione di servizio hello
In questa sezione si crea un'applicazione console Node. js che aggiunge un doppio dispositivo toohello metadati posizione associato a **myDeviceId**. Viene quindi gemelli dispositivo hello archiviate nell'hub IoT hello selezionando dispositivi hello che si trovano in hello ci le query e quindi hello quelli che riportano una connessione di rete.

1. Creare una nuova cartella vuota denominata **addtagsandqueryapp**. In hello **addtagsandqueryapp** cartella, creare un nuovo file package. JSON utilizzando hello seguente comando al prompt dei comandi. Accettare tutte le impostazioni predefinite hello:
   
    ```
    npm init
    ```
2. Al prompt dei comandi in hello **addtagsandqueryapp** cartella, eseguire hello successivo comando tooinstall hello **hub IOT di azure** pacchetto:
   
    ```
    npm install azure-iothub --save
    ```
3. Utilizzando un editor di testo, creare un nuovo **AddTagsAndQuery.js** file hello **addtagsandqueryapp** cartella.
4. Aggiungere i seguenti toohello codice hello **AddTagsAndQuery.js** file e sostituire hello **{stringa di connessione hub iot}** segnaposto con hello stringa di connessione IoT Hub è stato copiato al momento della creazione dell'hub:
   
        'use strict';
        var iothub = require('azure-iothub');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var patch = {
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                      }
                    }
                };
   
                twin.update(patch, function(err) {
                  if (err) {
                    console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                  } else {
                    console.log(twin.deviceId + ' twin updated successfully');
                    queryTwins();
                  }
                });
            }
        });
   
    Hello **Registro di sistema** oggetto espone tutte hello metodi obbligatorio toointeract con gemelli di dispositivo dal servizio hello. codice precedente Hello inizializza innanzitutto hello **Registro di sistema** dell'oggetto, quindi recupera hello gemelli di dispositivo per **myDeviceId**e infine gli aggiornamenti relativi tag con le informazioni sul percorso hello desiderato.
   
    Dopo aver hello aggiornamento hello tag che hello chiamate **queryTwins** (funzione).
5. Aggiungere hello seguente codice alla fine hello **AddTagsAndQuery.js** tooimplement hello **queryTwins** funzione:
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    il codice precedente Hello esegue due query: hello dapprima selezionati solo i gemelli dispositivo hello di dispositivi che si trovano in hello **Redmond43** impianto e hello secondo perfeziona hello query tooselect solo hello dispositivi connessi anche tramite rete cellulare.
   
    Si noti il codice precedente hello, durante la creazione di hello **query** dell'oggetto, specifica un numero massimo di documenti restituiti dalla query. Hello **query** oggetto contiene un **hasMoreResults** proprietà booleana che è possibile utilizzare hello tooinvoke **nextAsTwin** metodi più volte tooretrieve tutti i risultati. Un metodo chiamato **next** è disponibile per i risultati che non sono dispositivi gemelli, ad esempio i risultati delle query di aggregazione.
6. Eseguire un'applicazione hello con:
   
        node AddTagsAndQuery.js
   
    Dovrebbe essere un dispositivo nei risultati di hello per hello porre query per tutti i dispositivi si trovano in **Redmond43** e none per query hello che limita hello risultati toodevices che utilizzano una rete cellulare.
   
    ![][1]

Nella sezione successiva hello crei un'app per dispositivi vengono fornite informazioni di connettività hello e modifiche hello risultati di query hello nella sezione precedente hello.

## <a name="create-hello-device-app"></a>Creare app per dispositivi hello
In questa sezione si crea un'applicazione console Node.js che si connette hub tooyour come **myDeviceId**e quindi gli aggiornamenti relativi doppi dispositivo del segnalato informazioni hello toocontain di proprietà che è connesso tramite una rete cellulare.

> [!NOTE]
> A questo punto, sono accessibili solo da dispositivi che si connettono tooIoT Hub gemelli di dispositivo utilizzando il protocollo MQTT hello. Consultare toohello [supporto MQTT] [ lnk-devguide-mqtt] per istruzioni su come tooconvert esistente dispositivo app toouse MQTT.
> 
> 

1. Creare una nuova cartella vuota denominata **reportconnectivity**. In hello **reportconnectivity** cartella, creare un nuovo file package. JSON utilizzando hello seguente comando al prompt dei comandi. Accettare tutte le impostazioni predefinite hello:
   
    ```
    npm init
    ```
2. Al prompt dei comandi in hello **reportconnectivity** cartella, eseguire hello successivo comando tooinstall hello **dispositivi iot di azure**, e **mqtt azure-iot-dispositivo** pacchetto :
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Utilizzando un editor di testo, creare un nuovo **ReportConnectivity.js** file hello **reportconnectivity** cartella.
4. Aggiungere i seguenti toohello codice hello **ReportConnectivity.js** file e sostituire hello **{stringa di connessione dispositivo}** segnaposto con stringa di connessione dispositivo hello copiato al momento della creazione hello **myDeviceId** identità del dispositivo:
   
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
   
    Hello **Client** oggetto espone tutti i metodi di hello desiderate toointeract con gemelli di dispositivo dal dispositivo hello. Hello codice precedente, dopo l'inizializzazione hello **Client** oggetto recupera hello gemelli di dispositivo per **myDeviceId** e aggiorna la proprietà segnalata con informazioni sulla connettività hello.
5. Eseguire app dispositivo hello
   
        node ReportConnectivity.js
   
    Verrà visualizzato il messaggio hello `twin state reported`.
6. Ora che hello dispositivo segnalato le informazioni di connettività, viene visualizzato in entrambe le query. Andare in hello **addtagsandqueryapp** hello cartella ed eseguire nuovamente una query:
   
        node AddTagsAndQuery.js
   
    Questa volta **myDeviceId** verrà visualizzato nei risultati di entrambe le query.
   
    ![][3]

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, è configurato un nuovo hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità. Aggiunti i metadati del dispositivo come tag da un'app di back-end e ha scritto informazioni di connettività un dispositivo simulato app tooreport dispositivo in un doppio dispositivo hello. È inoltre appreso tooquery queste informazioni usando il linguaggio di query di hello IoT Hub simile a SQL.

Hello utilizzare seguenti come risorse toolearn per:

* inviare i dati di telemetria dai dispositivi con hello [iniziare con l'IoT Hub] [ lnk-iothub-getstarted] esercitazione
* configurare i dispositivi con le proprietà desiderate di un doppio dispositivo hello [lo si desidera utilizzare i dispositivi di proprietà tooconfigure] [ lnk-twin-how-to-configure] esercitazione
* controllare i dispositivi in modo interattivo (ad esempio l'attivazione di una ventola da un'app controllata dall'utente), con hello [utilizzare metodi diretti] [ lnk-methods-tutorial] esercitazione.

<!-- images -->
[1]: media/iot-hub-node-node-twin-getstarted/service1.png
[3]: media/iot-hub-node-node-twin-getstarted/service2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/

[lnk-twin-how-to-configure]: iot-hub-node-node-twin-how-to-configure.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
