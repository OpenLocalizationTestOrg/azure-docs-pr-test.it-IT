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
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-python"></a><span data-ttu-id="4150b-104">Connessione hub IoT tooyour dispositivo simulato utilizzando Python</span><span class="sxs-lookup"><span data-stu-id="4150b-104">Connect your simulated device tooyour IoT hub using Python</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="4150b-105">Alla fine di hello di questa esercitazione, si avranno due App Python:</span><span class="sxs-lookup"><span data-stu-id="4150b-105">At hello end of this tutorial, you will have two Python apps:</span></span>

* <span data-ttu-id="4150b-106">**CreateDeviceIdentity.py**, che consente di creare un'identità del dispositivo e protezione della chiave tooconnect app dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="4150b-106">**CreateDeviceIdentity.py**, which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="4150b-107">**SimulatedDevice.py**, che connette tooyour hub IoT con l'identità del dispositivo hello creato in precedenza e periodicamente invia un telemetria messaggio utilizzando il protocollo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="4150b-107">**SimulatedDevice.py**, which connects tooyour IoT hub with hello device identity created earlier, and periodically sends a telemetry message using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="4150b-108">articolo Hello [Azure IoT SDK] [ lnk-hub-sdks] vengono fornite informazioni hello Azure IoT SDK che è possibile utilizzare toobuild toorun entrambe le applicazioni in dispositivi e la soluzione di back-end.</span><span class="sxs-lookup"><span data-stu-id="4150b-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="4150b-109">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="4150b-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="4150b-110">[Python 2.x o 3.x][lnk-python-download].</span><span class="sxs-lookup"><span data-stu-id="4150b-110">[Python 2.x or 3.x][lnk-python-download].</span></span> <span data-ttu-id="4150b-111">Rendere che toouse hello 32 bit o 64 bit installazione come richiesto dall'installazione.</span><span class="sxs-lookup"><span data-stu-id="4150b-111">Make sure toouse hello 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="4150b-112">Quando richiesto durante l'installazione di hello, assicurarsi che tooadd Python tooyour specifico della piattaforma variabile.</span><span class="sxs-lookup"><span data-stu-id="4150b-112">When prompted during hello installation, make sure tooadd Python tooyour platform-specific environment variable.</span></span> <span data-ttu-id="4150b-113">Se si usa Python 2. x, potrebbe essere troppo[installare o aggiornare *pip*, Python hello pacchetto sistema di gestione][lnk-install-pip].</span><span class="sxs-lookup"><span data-stu-id="4150b-113">If you are using Python 2.x, you may need too[install or upgrade *pip*, hello Python package management system][lnk-install-pip].</span></span>
* <span data-ttu-id="4150b-114">Se si utilizza il sistema operativo Windows, quindi [Visual C++ redistributable package] [ lnk-visual-c-redist] utilizzare hello tooallow di DLL native da Python.</span><span class="sxs-lookup"><span data-stu-id="4150b-114">If you are using Windows OS, then [Visual C++ redistributable package][lnk-visual-c-redist] tooallow hello use of native DLLs from Python.</span></span>
* <span data-ttu-id="4150b-115">[Node.js 4.0 o versione successiva][lnk-node-download].</span><span class="sxs-lookup"><span data-stu-id="4150b-115">[Node.js 4.0 or later][lnk-node-download].</span></span> <span data-ttu-id="4150b-116">Rendere che toouse hello 32 bit o 64 bit installazione come richiesto dall'installazione.</span><span class="sxs-lookup"><span data-stu-id="4150b-116">Make sure toouse hello 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="4150b-117">Si tratta di hello necessari tooinstall [strumento di esplorazione di Hub IoT][lnk-iot-hub-explorer].</span><span class="sxs-lookup"><span data-stu-id="4150b-117">This is needed tooinstall hello [IoT Hub Explorer tool][lnk-iot-hub-explorer].</span></span>
* <span data-ttu-id="4150b-118">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="4150b-118">An active Azure account.</span></span> <span data-ttu-id="4150b-119">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="4150b-119">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="4150b-120">Hello *pip* pacchetti per `azure-iothub-service-client` e `azure-iothub-device-client` sono attualmente disponibili solo per il sistema operativo Windows.</span><span class="sxs-lookup"><span data-stu-id="4150b-120">hello *pip* packages for `azure-iothub-service-client` and `azure-iothub-device-client` are currently available only for Windows OS.</span></span> <span data-ttu-id="4150b-121">Per il sistema operativo Linux o Mac, consultare le sezioni specifiche del sistema operativo Mac e Linux toohello in hello [preparare l'ambiente di sviluppo per Python] [ lnk-python-devbox] post.</span><span class="sxs-lookup"><span data-stu-id="4150b-121">For Linux/Mac OS, please refer toohello Linux and Mac OS-specific sections on hello [Prepare your development environment for Python][lnk-python-devbox] post.</span></span>
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="4150b-122">L'hub IoT è stato creato.</span><span class="sxs-lookup"><span data-stu-id="4150b-122">You have now created your IoT hub.</span></span> <span data-ttu-id="4150b-123">Utilizzare hello nome host dell'IoT Hub e stringa di connessione IoT Hub hello rest hello di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4150b-123">Use hello IoT Hub host name and hello IoT Hub connection string in hello rest of this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="4150b-124">È possibile anche creare facilmente l'hub IoT su una riga di comando, utilizzando hello Python o Node.js su CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="4150b-124">You can also easily create your IoT hub on a command line, using hello Python or Node.js based Azure CLI.</span></span> <span data-ttu-id="4150b-125">articolo Hello [creazione di un hub IoT mediante Azure CLI 2.0 hello] [ lnk-azure-cli-hub] Mostra hello in modo rapido seguendo questa procedura toodo.</span><span class="sxs-lookup"><span data-stu-id="4150b-125">hello article [Create an IoT hub using hello Azure CLI 2.0][lnk-azure-cli-hub] shows you hello quick steps toodo so.</span></span> 
> 

## <a name="create-a-device-identity"></a><span data-ttu-id="4150b-126">Creare un'identità del dispositivo</span><span class="sxs-lookup"><span data-stu-id="4150b-126">Create a device identity</span></span>
<span data-ttu-id="4150b-127">Questa sezione elenca i passaggi di hello toocreate un'applicazione console Python, che crea un'identità del dispositivo nel Registro di sistema identità hello dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4150b-127">This section lists hello steps toocreate a Python console app, that creates a device identity in hello identity registry of your IoT hub.</span></span> <span data-ttu-id="4150b-128">Un dispositivo può connettersi solo tooIoT Hub se dispone di una voce del Registro di sistema di hello identità.</span><span class="sxs-lookup"><span data-stu-id="4150b-128">A device can only connect tooIoT Hub if it has an entry in hello identity registry.</span></span> <span data-ttu-id="4150b-129">Per ulteriori informazioni, vedere hello **Registro di sistema di identità** sezione di hello [Guida per sviluppatori di IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="4150b-129">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="4150b-130">Quando si esegue questa app console, viene generato un ID univoco del dispositivo e chiave che il dispositivo può usare tooidentify stesso quando vengono inviati al dispositivo a cloud messaggi tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4150b-130">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="4150b-131">Aprire un prompt dei comandi e installare hello **Azure IoT Hub Service SDK per Python**.</span><span class="sxs-lookup"><span data-stu-id="4150b-131">Open a command prompt and install hello **Azure IoT Hub Service SDK for Python**.</span></span> <span data-ttu-id="4150b-132">Chiudere il prompt dei comandi di hello dopo aver installato il SDK di hello.</span><span class="sxs-lookup"><span data-stu-id="4150b-132">Close hello command prompt after you install hello SDK.</span></span>

    ```
    pip install azure-iothub-service-client
    ```

2. <span data-ttu-id="4150b-133">Creare un file di Python denominato **CreateDeviceIdentity.py**.</span><span class="sxs-lookup"><span data-stu-id="4150b-133">Create a Python file named **CreateDeviceIdentity.py**.</span></span> <span data-ttu-id="4150b-134">Aprire il file in [un editor o dell'IDE Python di propria scelta][lnk-python-ide-list], ad esempio, hello predefinito [inattivo][lnk-idle].</span><span class="sxs-lookup"><span data-stu-id="4150b-134">Open it in [a Python editor/IDE of your choice][lnk-python-ide-list], for example, hello default [IDLE][lnk-idle].</span></span>

3. <span data-ttu-id="4150b-135">Aggiungere i seguenti moduli di codice tooimport hello richiesto dal servizio hello SDK hello:</span><span class="sxs-lookup"><span data-stu-id="4150b-135">Add hello following code tooimport hello required modules from hello service SDK:</span></span>

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. <span data-ttu-id="4150b-136">Aggiungere hello nel codice seguente, sostituendo il segnaposto hello per `[IoTHub Connection String]` hello stringa di connessione per l'hub IoT hello creato nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="4150b-136">Add hello following code, replacing hello placeholder for `[IoTHub Connection String]` with hello connection string for hello IoT hub you created in hello previous section.</span></span> <span data-ttu-id="4150b-137">È possibile utilizzare qualsiasi nome come hello `DEVICE_ID`.</span><span class="sxs-lookup"><span data-stu-id="4150b-137">You can use any name as hello `DEVICE_ID`.</span></span>
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. <span data-ttu-id="4150b-138">Aggiungere alcune delle informazioni sul dispositivo hello hello seguenti tooprint (funzione).</span><span class="sxs-lookup"><span data-stu-id="4150b-138">Add hello following function tooprint some of hello device information.</span></span>

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
3. <span data-ttu-id="4150b-139">Aggiungere hello dopo l'identificazione del dispositivo hello toocreate funzione utilizzando hello gestore registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="4150b-139">Add hello following function toocreate hello device identification using hello Registry Manager.</span></span> 

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
4. <span data-ttu-id="4150b-140">Infine, aggiungere la funzione principale di hello come indicato di seguito e salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="4150b-140">Finally, add hello main function as follows and save hello file.</span></span>

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
5. <span data-ttu-id="4150b-141">Nel prompt dei comandi di hello, eseguire hello **CreateDeviceIdentity.py** come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="4150b-141">On hello command prompt, run hello **CreateDeviceIdentity.py** as follows:</span></span>

    ```python
    python CreateDeviceIdentity.py
    ```
6. <span data-ttu-id="4150b-142">Dovrebbe essere dispositivo simulato di hello recupero creato.</span><span class="sxs-lookup"><span data-stu-id="4150b-142">You should see hello simulated device getting created.</span></span> <span data-ttu-id="4150b-143">Annotare hello **deviceId** hello e **primaryKey** di questo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4150b-143">Note down hello **deviceId** and hello **primaryKey** of this device.</span></span> <span data-ttu-id="4150b-144">Questi valori è necessario in un secondo momento quando si crea un'applicazione che si connette tooIoT Hub come un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4150b-144">You need these values later when you create an application that connects tooIoT Hub as a device.</span></span>

    ![La creazione del dispositivo è stata completata][1]

> [!NOTE]
> <span data-ttu-id="4150b-146">Hello del Registro di sistema di IoT Hub identità archivia solo hub IoT toohello di dispositivo identità tooenable proteggere l'accesso.</span><span class="sxs-lookup"><span data-stu-id="4150b-146">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="4150b-147">Archivia toouse di chiavi e l'ID dispositivo come credenziali di sicurezza e un flag di abilitazione/disabilitazione che è possibile utilizzare toodisable accesso per un singolo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4150b-147">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="4150b-148">Se l'applicazione deve toostore altri metadati specifici del dispositivo, deve utilizzare un archivio specifici dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4150b-148">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="4150b-149">Per ulteriori informazioni, vedere hello [Guida per sviluppatori di IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="4150b-149">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="4150b-150">Creare un'app di dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="4150b-150">Create a simulated device app</span></span>
<span data-ttu-id="4150b-151">Questa sezione elenca i passaggi di hello toocreate un'applicazione console Python, che simula un dispositivo e invia l'hub IoT tooyour messaggi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="4150b-151">This section lists hello steps toocreate a Python console app, that simulates a device and sends device-to-cloud messages tooyour IoT hub.</span></span>

1. <span data-ttu-id="4150b-152">Aprire un prompt dei comandi di nuovo e installare hello Azure IoT Hub dispositivo SDK per Python, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="4150b-152">Open a new command prompt and install hello Azure IoT Hub Device SDK for Python as follows.</span></span> <span data-ttu-id="4150b-153">Chiudere il prompt di comandi hello dopo l'installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="4150b-153">Close hello command prompt after hello installation.</span></span>

    ```
    pip install azure-iothub-device-client
    ```
2. <span data-ttu-id="4150b-154">Creare un file denominato **SimulatedDevice.py**.</span><span class="sxs-lookup"><span data-stu-id="4150b-154">Create a file named **SimulatedDevice.py**.</span></span> <span data-ttu-id="4150b-155">Aprire il file in un editor/IDE di Python di propria scelta, ad esempio IDLE.</span><span class="sxs-lookup"><span data-stu-id="4150b-155">Open this file in a Python editor/IDE of your choice (for example, IDLE).</span></span>

3. <span data-ttu-id="4150b-156">Aggiungere i seguenti moduli di codice tooimport hello richiesto dal dispositivo hello SDK hello.</span><span class="sxs-lookup"><span data-stu-id="4150b-156">Add hello following code tooimport hello required modules from hello device SDK.</span></span>

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. <span data-ttu-id="4150b-157">Aggiungere il seguente di hello codice e sostituire i segnaposto hello per `[IoTHub Device Connection String]` hello stringa di connessione per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4150b-157">Add hello following code and replace hello placeholder for `[IoTHub Device Connection String]` with hello connection string for your device.</span></span> <span data-ttu-id="4150b-158">stringa di connessione del dispositivo Hello è in genere in formato hello `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span><span class="sxs-lookup"><span data-stu-id="4150b-158">hello device connection string is usually in hello format of `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span></span> <span data-ttu-id="4150b-159">Hello utilizzare **deviceId** e **primaryKey** del dispositivo hello è stato creato in hello di hello precedente sezione tooreplace `<deviceId>` e `<primaryKey>` rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="4150b-159">Use hello **deviceId** and **primaryKey** of hello device you created in hello previous section tooreplace hello `<deviceId>` and `<primaryKey>` respectively.</span></span> <span data-ttu-id="4150b-160">Sostituire `<hostName>` con il nome host dell'hub IoT, in genere come `<IoT hub name>.azure-devices.net`.</span><span class="sxs-lookup"><span data-stu-id="4150b-160">Replace `<hostName>` with your IoT hub's host name, usually as `<IoT hub name>.azure-devices.net`.</span></span>

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
5. <span data-ttu-id="4150b-161">Aggiungere hello seguente codice toodefine un callback di conferma di trasmissione.</span><span class="sxs-lookup"><span data-stu-id="4150b-161">Add hello following code toodefine a send confirmation callback.</span></span> 

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
6. <span data-ttu-id="4150b-162">Aggiungere i seguenti client di dispositivo hello tooinitialize codice hello.</span><span class="sxs-lookup"><span data-stu-id="4150b-162">Add hello following code tooinitialize hello device client.</span></span>

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set hello time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. <span data-ttu-id="4150b-163">Aggiungere i seguenti hello funzionano tooformat e inviare un messaggio dall'hub IoT di tooyour di dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="4150b-163">Add hello following function tooformat and send a message from your simulated device tooyour IoT hub.</span></span>

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
8. <span data-ttu-id="4150b-164">Infine, Aggiungi la funzione principale di hello.</span><span class="sxs-lookup"><span data-stu-id="4150b-164">Finally, add hello main function.</span></span> 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using hello Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. <span data-ttu-id="4150b-165">Salvare e chiudere hello **SimulatedDevice.py** file.</span><span class="sxs-lookup"><span data-stu-id="4150b-165">Save and close hello **SimulatedDevice.py** file.</span></span> <span data-ttu-id="4150b-166">Si sono ora pronti toorun questa app.</span><span class="sxs-lookup"><span data-stu-id="4150b-166">You are now ready toorun this app.</span></span>

> [!NOTE]
> <span data-ttu-id="4150b-167">cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo.</span><span class="sxs-lookup"><span data-stu-id="4150b-167">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="4150b-168">Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio un backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="4150b-168">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a><span data-ttu-id="4150b-169">Ricevere messaggi dal dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="4150b-169">Receive messages from your simulated device</span></span>
<span data-ttu-id="4150b-170">messaggi di dati di telemetria tooreceive dal dispositivo, è necessario toouse un [hub eventi][lnk-event-hubs-overview]-compatibile endpoint esposto dall'IoT Hub, che legge i messaggi da dispositivo a cloud hello hello.</span><span class="sxs-lookup"><span data-stu-id="4150b-170">tooreceive telemetry messages from your device, you need toouse an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint exposed by hello IoT Hub, which reads hello device-to-cloud messages.</span></span> <span data-ttu-id="4150b-171">Hello lettura [Introduzione agli hub di eventi] [ lnk-eventhubs-tutorial] esercitazione per informazioni su come tooprocess messaggi dagli hub eventi per l'endpoint di Hub eventi compatibile con il valore dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4150b-171">Read hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial for information on how tooprocess messages from Event Hubs for your IoT hub's Event Hub-compatible endpoint.</span></span> <span data-ttu-id="4150b-172">Hub eventi non supporta dati di telemetria in Python ancora, pertanto è possibile creare un [Node.js](iot-hub-node-node-getstarted.md#D2C_node) o [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) messaggi da dispositivo a cloud hello console basata su hub eventi app tooread dall'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4150b-172">Event Hubs does not support telemetry in Python yet, so you can either create a [Node.js](iot-hub-node-node-getstarted.md#D2C_node) or a [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) Event Hubs-based console app tooread hello device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="4150b-173">In questa esercitazione viene illustrato come utilizzare hello [strumento di esplorazione di Hub IoT] [ lnk-iot-hub-explorer] tooread questi messaggi di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4150b-173">This tutorial shows how you can use hello [IoT Hub Explorer tool][lnk-iot-hub-explorer] tooread these device messages.</span></span>

1. <span data-ttu-id="4150b-174">Aprire un prompt dei comandi e installare hello Esplora Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4150b-174">Open a command prompt and install hello IoT Hub Explorer.</span></span> 

    ```
    npm install -g iothub-explorer
    ```

2. <span data-ttu-id="4150b-175">Eseguire hello comando seguente nel prompt dei comandi di hello, monitoraggio toobegin hello messaggi da dispositivo a cloud dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4150b-175">Run hello following command on hello command prompt, toobegin monitoring hello device-to-cloud messages from your device.</span></span> <span data-ttu-id="4150b-176">Utilizzare la stringa di connessione dell'hub del IoT segnaposto hello dopo `--login`.</span><span class="sxs-lookup"><span data-stu-id="4150b-176">Use your IoT hub's connection string in hello placeholder after `--login`.</span></span>

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. <span data-ttu-id="4150b-177">Aprire un nuovo prompt dei comandi e passare toohello directory contenente hello **SimulatedDevice.py** file.</span><span class="sxs-lookup"><span data-stu-id="4150b-177">Open a new command prompt and navigate toohello directory containing hello **SimulatedDevice.py** file.</span></span>

4. <span data-ttu-id="4150b-178">Eseguire hello **SimulatedDevice.py** file, che invia periodicamente hub IoT tooyour dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="4150b-178">Run hello **SimulatedDevice.py** file, which periodically sends telemetry data tooyour IoT hub.</span></span> 
   
    ```
    python SimulatedDevice.py
    ```
5. <span data-ttu-id="4150b-179">Osservare i messaggi di dispositivo hello nel prompt dei comandi di hello in esecuzione hello Esplora Hub IoT dalla sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="4150b-179">Observe hello device messages on hello command prompt running hello IoT Hub Explorer from hello previous section.</span></span> 

    ![Messaggi dal dispositivo Python al cloud][2]

## <a name="next-steps"></a><span data-ttu-id="4150b-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4150b-181">Next steps</span></span>
<span data-ttu-id="4150b-182">In questa esercitazione, è configurato un nuovo hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità.</span><span class="sxs-lookup"><span data-stu-id="4150b-182">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="4150b-183">È stato utilizzato questo dispositivo identità tooenable hello simulato dispositivo app toosend messaggi da dispositivo a cloud toohello hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4150b-183">You used this device identity tooenable hello simulated device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="4150b-184">È stato notato messaggi hello ricevuti dall'hub IoT hello con l'aiuto di hello dello strumento Esplora Hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="4150b-184">You observed hello messages received by hello IoT hub with hello help of hello IoT Hub Explorer tool.</span></span> 

<span data-ttu-id="4150b-185">tooexplore hello Python SDK per l'uso di IoT Hub di Azure in modo approfondito, visitare [repository Git Hub][lnk-python-github].</span><span class="sxs-lookup"><span data-stu-id="4150b-185">tooexplore hello Python SDK for Azure IoT Hub usage in depth, visit [this Git Hub repo][lnk-python-github].</span></span> <span data-ttu-id="4150b-186">tooreview hello funzionalità di messaggistica di hello Azure IoT Hub Service SDK per Python, è possibile scaricare ed eseguire [iothub_messaging_sample.py][lnk-messaging-sample].</span><span class="sxs-lookup"><span data-stu-id="4150b-186">tooreview hello messaging capabilities of hello Azure IoT Hub Service SDK for Python, you can download and run [iothub_messaging_sample.py][lnk-messaging-sample].</span></span> <span data-ttu-id="4150b-187">Per la simulazione del lato dispositivo utilizzando hello Azure IoT Hub dispositivo SDK per Python, è possibile scaricare ed eseguire hello [iothub_client_sample.py][lnk-client-sample].</span><span class="sxs-lookup"><span data-stu-id="4150b-187">For device side simulation using hello Azure IoT Hub Device SDK for Python, you can download and run hello [iothub_client_sample.py][lnk-client-sample].</span></span>

<span data-ttu-id="4150b-188">Guida introduttiva toocontinue con IoT Hub e tooexplore altri scenari IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="4150b-188">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="4150b-189">[Connessione del dispositivo][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="4150b-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="4150b-190">[Introduzione alla gestione dei dispositivi][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="4150b-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="4150b-191">[Introduzione ad Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="4150b-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="4150b-192">toolearn tooextend vedere i messaggi di dispositivo a cloud processo e di soluzione IoT su larga scala, hello [elaborare i messaggi da dispositivo a cloud] [ lnk-process-d2c-tutorial] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4150b-192">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
