---
title: aaaGet avviato con l'IoT Hub Azure (Python) | Documenti Microsoft
description: Informazioni su come toosend dispositivo a cloud messaggi tooAzure IoT Hub tramite IoT SDK per Python. Creare dispositivo simulato e servizio App tooregister il dispositivo, inviare messaggi e leggere messaggi da hub IoT.
services: iot-hub
author: dsk-2015
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: python
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: dkshir
ms.custom: na
ms.openlocfilehash: aa23e792fb144202e121274723bcfaeae0c04723
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-python"></a>Connessione hub IoT tooyour dispositivo simulato utilizzando Python
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

Alla fine di hello di questa esercitazione, si avranno due App Python:

* **CreateDeviceIdentity.py**, che consente di creare un'identità del dispositivo e protezione della chiave tooconnect app dispositivo simulato.
* **SimulatedDevice.py**, che connette tooyour hub IoT con l'identità del dispositivo hello creato in precedenza e periodicamente invia un telemetria messaggio utilizzando il protocollo MQTT hello.

> [!NOTE]
> articolo Hello [Azure IoT SDK] [ lnk-hub-sdks] vengono fornite informazioni hello Azure IoT SDK che è possibile utilizzare toobuild toorun entrambe le applicazioni in dispositivi e la soluzione di back-end.
> 
> 

toocomplete questa esercitazione, è necessario hello seguenti:

* [Python 2.x o 3.x][lnk-python-download]. Rendere che toouse hello 32 bit o 64 bit installazione come richiesto dall'installazione. Quando richiesto durante l'installazione di hello, assicurarsi che tooadd Python tooyour specifico della piattaforma variabile. Se si usa Python 2. x, potrebbe essere troppo[installare o aggiornare *pip*, Python hello pacchetto sistema di gestione][lnk-install-pip].
* Se si utilizza il sistema operativo Windows, quindi [Visual C++ redistributable package] [ lnk-visual-c-redist] utilizzare hello tooallow di DLL native da Python.
* [Node.js 4.0 o versione successiva][lnk-node-download]. Rendere che toouse hello 32 bit o 64 bit installazione come richiesto dall'installazione. Si tratta di hello necessari tooinstall [strumento di esplorazione di Hub IoT][lnk-iot-hub-explorer].
* Un account Azure attivo. Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.

> [!NOTE]
> Hello *pip* pacchetti per `azure-iothub-service-client` e `azure-iothub-device-client` sono attualmente disponibili solo per il sistema operativo Windows. Per il sistema operativo Linux o Mac, consultare le sezioni specifiche del sistema operativo Mac e Linux toohello in hello [preparare l'ambiente di sviluppo per Python] [ lnk-python-devbox] post.
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

L'hub IoT è stato creato. Utilizzare hello nome host dell'IoT Hub e stringa di connessione IoT Hub hello rest hello di questa esercitazione.

> [!NOTE]
> È possibile anche creare facilmente l'hub IoT su una riga di comando, utilizzando hello Python o Node.js su CLI di Azure. articolo Hello [creazione di un hub IoT mediante Azure CLI 2.0 hello] [ lnk-azure-cli-hub] Mostra hello in modo rapido seguendo questa procedura toodo. 
> 

## <a name="create-a-device-identity"></a>Creare un'identità del dispositivo
Questa sezione elenca i passaggi di hello toocreate un'applicazione console Python, che crea un'identità del dispositivo nel Registro di sistema identità hello dell'hub IoT. Un dispositivo può connettersi solo tooIoT Hub se dispone di una voce del Registro di sistema di hello identità. Per ulteriori informazioni, vedere hello **Registro di sistema di identità** sezione di hello [Guida per sviluppatori di IoT Hub][lnk-devguide-identity]. Quando si esegue questa app console, viene generato un ID univoco del dispositivo e chiave che il dispositivo può usare tooidentify stesso quando vengono inviati al dispositivo a cloud messaggi tooIoT Hub.

1. Aprire un prompt dei comandi e installare hello **Azure IoT Hub Service SDK per Python**. Chiudere il prompt dei comandi di hello dopo aver installato il SDK di hello.

    ```
    pip install azure-iothub-service-client
    ```

2. Creare un file di Python denominato **CreateDeviceIdentity.py**. Aprire il file in [un editor o dell'IDE Python di propria scelta][lnk-python-ide-list], ad esempio, hello predefinito [inattivo][lnk-idle].

3. Aggiungere i seguenti moduli di codice tooimport hello richiesto dal servizio hello SDK hello:

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. Aggiungere hello nel codice seguente, sostituendo il segnaposto hello per `[IoTHub Connection String]` hello stringa di connessione per l'hub IoT hello creato nella sezione precedente hello. È possibile utilizzare qualsiasi nome come hello `DEVICE_ID`.
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. Aggiungere alcune delle informazioni sul dispositivo hello hello seguenti tooprint (funzione).

    ```python
    def print_device_info(title, iothub_device):
        print ( title + ":" )
        print ( "iothubDevice.deviceId                    = {0}".format(iothub_device.deviceId) )
        print ( "iothubDevice.primaryKey                  = {0}".format(iothub_device.primaryKey) )
        print ( "iothubDevice.secondaryKey                = {0}".format(iothub_device.secondaryKey) )
        print ( "iothubDevice.connectionState             = {0}".format(iothub_device.connectionState) )
        print ( "iothubDevice.status                      = {0}".format(iothub_device.status) )
        print ( "iothubDevice.lastActivityTime            = {0}".format(iothub_device.lastActivityTime) )
        print ( "iothubDevice.cloudToDeviceMessageCount   = {0}".format(iothub_device.cloudToDeviceMessageCount) )
        print ( "iothubDevice.isManaged                   = {0}".format(iothub_device.isManaged) )
        print ( "iothubDevice.authMethod                  = {0}".format(iothub_device.authMethod) )
        print ( "" )
    ```
3. Aggiungere hello dopo l'identificazione del dispositivo hello toocreate funzione utilizzando hello gestore registro di sistema. 

    ```python
    def iothub_createdevice():
        try:
            iothub_registry_manager = IoTHubRegistryManager(CONNECTION_STRING)
            auth_method = IoTHubRegistryManagerAuthMethod.SHARED_PRIVATE_KEY
            new_device = iothub_registry_manager.create_device(DEVICE_ID, "", "", auth_method)
            print_device_info("CreateDevice", new_device)

        except IoTHubError as iothub_error:
            print ( "Unexpected error {0}".format(iothub_error) )
            return
        except KeyboardInterrupt:
            print ( "iothub_createdevice stopped" )
    ```
4. Infine, aggiungere la funzione principale di hello come indicato di seguito e salvare il file hello.

    ```python
    if __name__ == '__main__':
        print ( "" )
        print ( "Python {0}".format(sys.version) )
        print ( "Creating device using hello Azure IoT Hub Service SDK for Python" )
        print ( "" )
        print ( "    Connection string = {0}".format(CONNECTION_STRING) )
        print ( "    Device ID         = {0}".format(DEVICE_ID) )

        iothub_createdevice()
    ```
5. Nel prompt dei comandi di hello, eseguire hello **CreateDeviceIdentity.py** come indicato di seguito:

    ```python
    python CreateDeviceIdentity.py
    ```
6. Dovrebbe essere dispositivo simulato di hello recupero creato. Annotare hello **deviceId** hello e **primaryKey** di questo dispositivo. Questi valori è necessario in un secondo momento quando si crea un'applicazione che si connette tooIoT Hub come un dispositivo.

    ![La creazione del dispositivo è stata completata][1]

> [!NOTE]
> Hello del Registro di sistema di IoT Hub identità archivia solo hub IoT toohello di dispositivo identità tooenable proteggere l'accesso. Archivia toouse di chiavi e l'ID dispositivo come credenziali di sicurezza e un flag di abilitazione/disabilitazione che è possibile utilizzare toodisable accesso per un singolo dispositivo. Se l'applicazione deve toostore altri metadati specifici del dispositivo, deve utilizzare un archivio specifici dell'applicazione. Per ulteriori informazioni, vedere hello [Guida per sviluppatori di IoT Hub][lnk-devguide-identity].
> 
> 


## <a name="create-a-simulated-device-app"></a>Creare un'app di dispositivo simulato
Questa sezione elenca i passaggi di hello toocreate un'applicazione console Python, che simula un dispositivo e invia l'hub IoT tooyour messaggi da dispositivo a cloud.

1. Aprire un prompt dei comandi di nuovo e installare hello Azure IoT Hub dispositivo SDK per Python, come indicato di seguito. Chiudere il prompt di comandi hello dopo l'installazione di hello.

    ```
    pip install azure-iothub-device-client
    ```
2. Creare un file denominato **SimulatedDevice.py**. Aprire il file in un editor/IDE di Python di propria scelta, ad esempio IDLE.

3. Aggiungere i seguenti moduli di codice tooimport hello richiesto dal dispositivo hello SDK hello.

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. Aggiungere il seguente di hello codice e sostituire i segnaposto hello per `[IoTHub Device Connection String]` hello stringa di connessione per il dispositivo. stringa di connessione del dispositivo Hello è in genere in formato hello `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`. Hello utilizzare **deviceId** e **primaryKey** del dispositivo hello è stato creato in hello di hello precedente sezione tooreplace `<deviceId>` e `<primaryKey>` rispettivamente. Sostituire `<hostName>` con il nome host dell'hub IoT, in genere come `<IoT hub name>.azure-devices.net`.

    ```python
    # String containing Hostname, Device Id & Device Key in hello format
    CONNECTION_STRING = "[IoTHub Device Connection String]"
    # choose HTTP, AMQP or MQTT as transport protocol
    PROTOCOL = IoTHubTransportProvider.MQTT
    MESSAGE_TIMEOUT = 10000
    AVG_WIND_SPEED = 10.0
    SEND_CALLBACKS = 0
    MSG_TXT = "{\"deviceId\": \"MyFirstPythonDevice\",\"windSpeed\": %.2f}"    
    ```
5. Aggiungere hello seguente codice toodefine un callback di conferma di trasmissione. 

    ```python
    def send_confirmation_callback(message, result, user_context):
        global SEND_CALLBACKS
        print ( "Confirmation[%d] received for message with result = %s" % (user_context, result) )
        map_properties = message.properties()
        print ( "    message_id: %s" % message.message_id )
        print ( "    correlation_id: %s" % message.correlation_id )
        key_value_pair = map_properties.get_internals()
        print ( "    Properties: %s" % key_value_pair )
        SEND_CALLBACKS += 1
        print ( "    Total calls confirmed: %d" % SEND_CALLBACKS )
    ```
6. Aggiungere i seguenti client di dispositivo hello tooinitialize codice hello.

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set hello time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. Aggiungere i seguenti hello funzionano tooformat e inviare un messaggio dall'hub IoT di tooyour di dispositivo simulato.

    ```python
    def iothub_client_telemetry_sample_run():

        try:
            client = iothub_client_init()
            print ( "IoT Hub device sending periodic messages, press Ctrl-C tooexit" )
            message_counter = 0

            while True:
                msg_txt_formatted = MSG_TXT % (AVG_WIND_SPEED + (random.random() * 4 + 2))
                # messages can be encoded as string or bytearray
                if (message_counter & 1) == 1:
                    message = IoTHubMessage(bytearray(msg_txt_formatted, 'utf8'))
                else:
                    message = IoTHubMessage(msg_txt_formatted)
                # optional: assign ids
                message.message_id = "message_%d" % message_counter
                message.correlation_id = "correlation_%d" % message_counter
                # optional: assign properties
                prop_map = message.properties()
                prop_text = "PropMsg_%d" % message_counter
                prop_map.add("Property", prop_text)

                client.send_event_async(message, send_confirmation_callback, message_counter)
                print ( "IoTHubClient.send_event_async accepted message [%d] for transmission tooIoT Hub." % message_counter )

                status = client.get_send_status()
                print ( "Send status: %s" % status )
                time.sleep(30)

                status = client.get_send_status()
                print ( "Send status: %s" % status )

                message_counter += 1

        except IoTHubError as iothub_error:
            print ( "Unexpected error %s from IoTHub" % iothub_error )
            return
        except KeyboardInterrupt:
            print ( "IoTHubClient sample stopped" )
    ```
8. Infine, Aggiungi la funzione principale di hello. 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using hello Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. Salvare e chiudere hello **SimulatedDevice.py** file. Si sono ora pronti toorun questa app.

> [!NOTE]
> cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo. Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio un backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei][lnk-transient-faults].
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a>Ricevere messaggi dal dispositivo simulato
messaggi di dati di telemetria tooreceive dal dispositivo, è necessario toouse un [hub eventi][lnk-event-hubs-overview]-compatibile endpoint esposto dall'IoT Hub, che legge i messaggi da dispositivo a cloud hello hello. Hello lettura [Introduzione agli hub di eventi] [ lnk-eventhubs-tutorial] esercitazione per informazioni su come tooprocess messaggi dagli hub eventi per l'endpoint di Hub eventi compatibile con il valore dell'hub IoT. Hub eventi non supporta dati di telemetria in Python ancora, pertanto è possibile creare un [Node.js](iot-hub-node-node-getstarted.md#D2C_node) o [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) messaggi da dispositivo a cloud hello console basata su hub eventi app tooread dall'IoT Hub. In questa esercitazione viene illustrato come utilizzare hello [strumento di esplorazione di Hub IoT] [ lnk-iot-hub-explorer] tooread questi messaggi di dispositivo.

1. Aprire un prompt dei comandi e installare hello Esplora Hub IoT. 

    ```
    npm install -g iothub-explorer
    ```

2. Eseguire hello comando seguente nel prompt dei comandi di hello, monitoraggio toobegin hello messaggi da dispositivo a cloud dal dispositivo. Utilizzare la stringa di connessione dell'hub del IoT segnaposto hello dopo `--login`.

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. Aprire un nuovo prompt dei comandi e passare toohello directory contenente hello **SimulatedDevice.py** file.

4. Eseguire hello **SimulatedDevice.py** file, che invia periodicamente hub IoT tooyour dati di telemetria. 
   
    ```
    python SimulatedDevice.py
    ```
5. Osservare i messaggi di dispositivo hello nel prompt dei comandi di hello in esecuzione hello Esplora Hub IoT dalla sezione precedente hello. 

    ![Messaggi dal dispositivo Python al cloud][2]

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, è configurato un nuovo hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità. È stato utilizzato questo dispositivo identità tooenable hello simulato dispositivo app toosend messaggi da dispositivo a cloud toohello hub IoT. È stato notato messaggi hello ricevuti dall'hub IoT hello con l'aiuto di hello dello strumento Esplora Hub IoT hello. 

tooexplore hello Python SDK per l'uso di IoT Hub di Azure in modo approfondito, visitare [repository Git Hub][lnk-python-github]. tooreview hello funzionalità di messaggistica di hello Azure IoT Hub Service SDK per Python, è possibile scaricare ed eseguire [iothub_messaging_sample.py][lnk-messaging-sample]. Per la simulazione del lato dispositivo utilizzando hello Azure IoT Hub dispositivo SDK per Python, è possibile scaricare ed eseguire hello [iothub_client_sample.py][lnk-client-sample].

Guida introduttiva toocontinue con IoT Hub e tooexplore altri scenari IoT, vedere:

* [Connessione del dispositivo][lnk-connect-device]
* [Introduzione alla gestione dei dispositivi][lnk-device-management]
* [Introduzione ad Azure IoT Edge][lnk-iot-edge]

toolearn tooextend vedere i messaggi di dispositivo a cloud processo e di soluzione IoT su larga scala, hello [elaborare i messaggi da dispositivo a cloud] [ lnk-process-d2c-tutorial] esercitazione.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[1]: ./media/iot-hub-python-getstarted/createdevice.png
[2]: ./media/iot-hub-python-getstarted/sendd2cmessage.png

<!-- Links -->
[lnk-python-download]: https://www.python.org/downloads/
[lnk-visual-c-redist]: http://www.microsoft.com/download/confirmation.aspx?id=48145
[lnk-node-download]: https://nodejs.org/en/download/
[lnk-install-pip]: https://pip.pypa.io/en/stable/installing/
[lnk-azure-cli-hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-using-cli
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-idle]: https://docs.python.org/3/library/idle.html
[lnk-python-ide-list]: https://wiki.python.org/moin/IntegratedDevelopmentEnvironments
[lnk-iot-hub-explorer]: https://github.com/Azure/iothub-explorer
[lnk-python-github]: https://github.com/Azure/azure-iot-sdk-python
[lnk-messaging-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/service/samples/iothub_messaging_sample.py
[lnk-client-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/device/samples/iothub_client_sample.py

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-python-devbox]: https://github.com/Azure/azure-iot-sdk-python/blob/master/doc/python-devbox-setup.md

[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
