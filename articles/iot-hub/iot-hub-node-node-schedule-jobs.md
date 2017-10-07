---
title: i processi di aaaSchedule con IoT Hub di Azure (nodo) | Documenti Microsoft
description: "Un IoT Hub Azure tooschedule come processo tooinvoke un metodo diretto su più dispositivi. Utilizzare hello Azure IoT SDK per Node.js tooimplement hello simulato dispositivo App e un processo del servizio app toorun hello."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: be293362447fbcddaa3433b66f208f22545fe0c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-node"></a>Pianificare e trasmettere processi (Node)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

IoT Hub Azure è un servizio completamente gestito che consente un toocreate app back-end e i processi di traccia di pianificare e aggiornare milioni di dispositivi.  I processi possono essere utilizzati per hello seguenti azioni:

* Aggiornare le proprietà desiderate
* Aggiornare i tag
* Richiamare metodi diretti

Concettualmente, un processo esegue il wrapping di una di queste azioni e tracce hello lo stato di avanzamento dell'esecuzione rispetto a un set di dispositivi, definito da una query di due dispositivi.  Ad esempio, un'applicazione back-end può utilizzare tooinvoke un processo un metodo di riavvio su 10.000 dispositivi, specificato da una query di due dispositivi e pianificata in un secondo momento.  L'applicazione può quindi avanzamento come ognuno di questi dispositivi di ricezione ed eseguire il metodo di riavvio hello.

Altre informazioni su queste funzionalità sono disponibili in questi articoli:

* Proprietà e un doppio dispositivo: [introduzione gemelli dispositivo] [ lnk-get-started-twin] e [esercitazione: come dispositivo toouse doppio proprietà][lnk-twin-props]
* Metodi diretti: [Guida per sviluppatori dell'hub IoT - Metodi diretti][lnk-dev-methods] ed [Esercitazione: Metodi diretti][lnk-c2d-methods]

Questa esercitazione illustra come:

* Creare un'app dispositivo simulato che dispone di un metodo diretto, che consente di **lockDoor** che può essere chiamato da hello soluzione back-end.
* Creare un'applicazione console in Node.js tale hello chiamate **lockDoor** dirette del metodo nell'app dispositivo simulato hello utilizzando un processo e gli aggiornamenti di hello desiderato utilizzando un processo di dispositivi di proprietà.

Alla fine di hello di questa esercitazione, si dispongono di due applicazioni di console Node.js:

**simDevice.js**, che collega l'hub IoT tooyour con l'identità del dispositivo hello e riceve un **lockDoor** metodo diretto.

**scheduleJobService.js**, che chiama un metodo diretto in hello dispositivo simulato app e aggiornamento hello il dispositivo di proprietà di un doppio desiderate tramite un processo.

toocomplete questa esercitazione, è necessario hello seguenti:

* Node.js 0.12.x o versione successiva. <br/>  [Preparare l'ambiente di sviluppo] [ lnk-dev-setup] viene descritto come tooinstall Node.js per questa esercitazione su Windows o Linux.
* Un account Azure attivo. Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Creare un'app di dispositivo simulato
In questa sezione si crea un'applicazione console Node. js che risponde tooa dirette del metodo chiamata dal cloud hello, che attiva un riavvio del dispositivo simulato e utilizza hello segnalato proprietà tooenable doppi query tooidentify dispositivi e quando sono riavviato.

1. Creare una nuova cartella vuota chiamata **simDevice**.  In hello **simDevice** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi.  Accettare tutte le impostazioni predefinite hello:
   
    ```
    npm init
    ```
2. Al prompt dei comandi in hello **simDevice** cartella, eseguire hello successivo comando tooinstall hello **dispositivi iot di azure** pacchetto SDK di dispositivo e **mqtt azure-iot-dispositivo** pacchetto:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Utilizzando un editor di testo, creare un nuovo **simDevice.js** file hello **simDevice** cartella.
4. Aggiungere i seguenti hello 'richiedono' istruzioni all'inizio di hello di hello **simDevice.js** file:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. Aggiungere un **connectionString** variabile e usarlo toocreate un **Client** istanza.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. Aggiungere i seguenti hello toohandle funzione hello **lockDoor** metodo.
   
    ```
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```
7. Aggiungere hello seguente gestore hello tooregister del codice per hello **lockDoor** metodo.
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. Salvare e chiudere hello **simDevice.js** file.

> [!NOTE]
> cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo. Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio un backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei][lnk-transient-faults].
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a>Pianificare i processi per chiamare un metodo diretto e aggiornare le proprietà dei dispositivi gemelli
In questa sezione si crea un'applicazione console Node. js che avvia un remoto **lockDoor** in un dispositivo utilizzando le proprietà di un diretto (metodo) e aggiornamento hello dispositivo doppi.

1. Creare una nuova cartella vuota chiamata **scheduleJobService**.  In hello **scheduleJobService** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi.  Accettare tutte le impostazioni predefinite hello:
   
    ```
    npm init
    ```
2. Al prompt dei comandi in hello **scheduleJobService** cartella, eseguire hello successivo comando tooinstall hello **hub IOT di azure** pacchetto SDK di dispositivo e **azure-iot-dispositivo-mqtt**pacchetto:
   
    ```
    npm install azure-iothub uuid --save
    ```
3. Utilizzando un editor di testo, creare un nuovo **scheduleJobService.js** file hello **scheduleJobService** cartella.
4. Aggiungere i seguenti hello 'richiedono' istruzioni all'inizio di hello di hello **dmpatterns_gscheduleJobServiceetstarted_service.js** file:
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. Aggiungere hello dopo le dichiarazioni di variabili e sostituire i valori segnaposto hello:
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. Aggiungere hello seguente una funzione che sarà utilizzato toomonitor hello esecuzione del processo di hello:
   
    ```
    function monitorJob (jobId, callback) {
        var jobMonitorInterval = setInterval(function() {
            jobClient.getJob(jobId, function(err, result) {
            if (err) {
                console.error('Could not get job status: ' + err.message);
            } else {
                console.log('Job: ' + jobId + ' - status: ' + result.status);
                if (result.status === 'completed' || result.status === 'failed' || result.status === 'cancelled') {
                clearInterval(jobMonitorInterval);
                callback(null, result);
                }
            }
            });
        }, 5000);
    }
    ```
7. Aggiungere i seguenti processi di hello tooschedule codice che chiama il metodo di dispositivo hello hello:
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable tooprocess method
    };
   
    var methodJobId = uuid.v4();
    console.log('scheduling Device Method job with id: ' + methodJobId);
    jobClient.scheduleDeviceMethod(methodJobId,
                                queryCondition,
                                methodParams,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule device method job: ' + err.message);
        } else {
            monitorJob(methodJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor device method job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
8. Aggiungere hello gemelli di codice tooschedule hello processo tooupdate hello dispositivo seguenti:
   
    ```
    var twinPatch = {
        etag: '*',
        desired: {
            building: '43',
            floor: 3
        }
    };
   
    var twinJobId = uuid.v4();
   
    console.log('scheduling Twin Update job with id: ' + twinJobId);
    jobClient.scheduleTwinUpdate(twinJobId,
                                queryCondition,
                                twinPatch,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule twin update job: ' + err.message);
        } else {
            monitorJob(twinJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor twin update job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
9. Salvare e chiudere hello **scheduleJobService.js** file.

## <a name="run-hello-applications"></a>Eseguire applicazioni hello
Si è ora applicazioni hello toorun pronto.

1. Al prompt dei comandi di hello in hello **simDevice** cartella, eseguire hello successivo comando toobegin in attesa di hello riavvio dirette del metodo.
   
    ```
    node simDevice.js
    ```
2. Al prompt dei comandi di hello in hello **scheduleJobService** cartella, eseguire hello successivo comando tootrigger hello processi toolock hello porta e l'aggiornamento hello doppi
   
    ```
    node scheduleJobService.js
    ```
3. Vedrai hello dispositivo risposta toohello metodo diretto nella console di hello.

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione è stato utilizzato un processo tooschedule un dispositivo tooa dirette del metodo e l'aggiornamento di hello delle proprietà del doppi dispositivo hello.

toocontinue introduzione IoT Hub e modelli di gestione di dispositivi, ad esempio remoto tramite l'aggiornamento del firmware di hello air, vedere:

[Esercitazione: Come toodo un aggiornamento firmware][lnk-fwupdate]

Introduzione a IoT Hub, toocontinue vedere [Introduzione a Azure IoT Edge][lnk-iot-edge].

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
