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
# <a name="get-started-with-device-twins-node"></a><span data-ttu-id="b04c5-104">Introduzione ai dispositivi gemelli (Node)</span><span class="sxs-lookup"><span data-stu-id="b04c5-104">Get started with device twins (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="b04c5-105">Alla fine di hello di questa esercitazione, si avranno due applicazioni di console Node.js:</span><span class="sxs-lookup"><span data-stu-id="b04c5-105">At hello end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="b04c5-106">**AddTagsAndQuery.js**, un'app back-end di Node.js, che aggiunge tag ed esegue query sui dispositivi gemelli.</span><span class="sxs-lookup"><span data-stu-id="b04c5-106">**AddTagsAndQuery.js**, a Node.js back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="b04c5-107">**TwinSimulatedDevice.js**, un'app Node.js che simula un dispositivo che si connette l'hub IoT tooyour con l'identità del dispositivo hello creato in precedenza e segnala la condizione di connettività.</span><span class="sxs-lookup"><span data-stu-id="b04c5-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="b04c5-108">articolo Hello [Azure IoT SDK] [ lnk-hub-sdks] fornisce informazioni su Azure IoT SDK hello che è possibile utilizzare toobuild applicazioni back-end sia sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b04c5-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="b04c5-109">toocomplete questa esercitazione è necessario hello segue:</span><span class="sxs-lookup"><span data-stu-id="b04c5-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="b04c5-110">Node.js 0.10.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="b04c5-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="b04c5-111">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="b04c5-111">An active Azure account.</span></span> <span data-ttu-id="b04c5-112">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="b04c5-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a><span data-ttu-id="b04c5-113">Creare l'applicazione di servizio hello</span><span class="sxs-lookup"><span data-stu-id="b04c5-113">Create hello service app</span></span>
<span data-ttu-id="b04c5-114">In questa sezione si crea un'applicazione console Node. js che aggiunge un doppio dispositivo toohello metadati posizione associato a **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="b04c5-114">In this section, you create a Node.js console app that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="b04c5-115">Viene quindi gemelli dispositivo hello archiviate nell'hub IoT hello selezionando dispositivi hello che si trovano in hello ci le query e quindi hello quelli che riportano una connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="b04c5-115">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that are reporting a cellular connection.</span></span>

1. <span data-ttu-id="b04c5-116">Creare una nuova cartella vuota denominata **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="b04c5-116">Create a new empty folder called **addtagsandqueryapp**.</span></span> <span data-ttu-id="b04c5-117">In hello **addtagsandqueryapp** cartella, creare un nuovo file package. JSON utilizzando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="b04c5-117">In hello **addtagsandqueryapp** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="b04c5-118">Accettare tutte le impostazioni predefinite hello:</span><span class="sxs-lookup"><span data-stu-id="b04c5-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="b04c5-119">Al prompt dei comandi in hello **addtagsandqueryapp** cartella, eseguire hello successivo comando tooinstall hello **hub IOT di azure** pacchetto:</span><span class="sxs-lookup"><span data-stu-id="b04c5-119">At your command prompt in hello **addtagsandqueryapp** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="b04c5-120">Utilizzando un editor di testo, creare un nuovo **AddTagsAndQuery.js** file hello **addtagsandqueryapp** cartella.</span><span class="sxs-lookup"><span data-stu-id="b04c5-120">Using a text editor, create a new **AddTagsAndQuery.js** file in hello **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="b04c5-121">Aggiungere i seguenti toohello codice hello **AddTagsAndQuery.js** file e sostituire hello **{stringa di connessione hub iot}** segnaposto con hello stringa di connessione IoT Hub è stato copiato al momento della creazione dell'hub:</span><span class="sxs-lookup"><span data-stu-id="b04c5-121">Add hello following code toohello **AddTagsAndQuery.js** file, and substitute hello **{iot hub connection string}** placeholder with hello IoT Hub connection string you copied when you created your hub:</span></span>
   
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
   
    <span data-ttu-id="b04c5-122">Hello **Registro di sistema** oggetto espone tutte hello metodi obbligatorio toointeract con gemelli di dispositivo dal servizio hello.</span><span class="sxs-lookup"><span data-stu-id="b04c5-122">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="b04c5-123">codice precedente Hello inizializza innanzitutto hello **Registro di sistema** dell'oggetto, quindi recupera hello gemelli di dispositivo per **myDeviceId**e infine gli aggiornamenti relativi tag con le informazioni sul percorso hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="b04c5-123">hello previous code first initializes hello **Registry** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="b04c5-124">Dopo aver hello aggiornamento hello tag che hello chiamate **queryTwins** (funzione).</span><span class="sxs-lookup"><span data-stu-id="b04c5-124">After hello updating hello tags it calls hello **queryTwins** function.</span></span>
5. <span data-ttu-id="b04c5-125">Aggiungere hello seguente codice alla fine hello **AddTagsAndQuery.js** tooimplement hello **queryTwins** funzione:</span><span class="sxs-lookup"><span data-stu-id="b04c5-125">Add hello following code at hello end of  **AddTagsAndQuery.js** tooimplement hello **queryTwins** function:</span></span>
   
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
   
    <span data-ttu-id="b04c5-126">il codice precedente Hello esegue due query: hello dapprima selezionati solo i gemelli dispositivo hello di dispositivi che si trovano in hello **Redmond43** impianto e hello secondo perfeziona hello query tooselect solo hello dispositivi connessi anche tramite rete cellulare.</span><span class="sxs-lookup"><span data-stu-id="b04c5-126">hello previous code executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="b04c5-127">Si noti il codice precedente hello, durante la creazione di hello **query** dell'oggetto, specifica un numero massimo di documenti restituiti dalla query.</span><span class="sxs-lookup"><span data-stu-id="b04c5-127">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="b04c5-128">Hello **query** oggetto contiene un **hasMoreResults** proprietà booleana che è possibile utilizzare hello tooinvoke **nextAsTwin** metodi più volte tooretrieve tutti i risultati.</span><span class="sxs-lookup"><span data-stu-id="b04c5-128">hello **query** object contains a **hasMoreResults** boolean property that you can use tooinvoke hello **nextAsTwin** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="b04c5-129">Un metodo chiamato **next** è disponibile per i risultati che non sono dispositivi gemelli, ad esempio i risultati delle query di aggregazione.</span><span class="sxs-lookup"><span data-stu-id="b04c5-129">A method called **next** is available for results that are not device twins for example, results of aggregation queries.</span></span>
6. <span data-ttu-id="b04c5-130">Eseguire un'applicazione hello con:</span><span class="sxs-lookup"><span data-stu-id="b04c5-130">Run hello application with:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="b04c5-131">Dovrebbe essere un dispositivo nei risultati di hello per hello porre query per tutti i dispositivi si trovano in **Redmond43** e none per query hello che limita hello risultati toodevices che utilizzano una rete cellulare.</span><span class="sxs-lookup"><span data-stu-id="b04c5-131">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![][1]

<span data-ttu-id="b04c5-132">Nella sezione successiva hello crei un'app per dispositivi vengono fornite informazioni di connettività hello e modifiche hello risultati di query hello nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="b04c5-132">In hello next section you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="b04c5-133">Creare app per dispositivi hello</span><span class="sxs-lookup"><span data-stu-id="b04c5-133">Create hello device app</span></span>
<span data-ttu-id="b04c5-134">In questa sezione si crea un'applicazione console Node.js che si connette hub tooyour come **myDeviceId**e quindi gli aggiornamenti relativi doppi dispositivo del segnalato informazioni hello toocontain di proprietà che è connesso tramite una rete cellulare.</span><span class="sxs-lookup"><span data-stu-id="b04c5-134">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, and then updates its device twin's reported properties toocontain hello information that it is connected using a cellular network.</span></span>

> [!NOTE]
> <span data-ttu-id="b04c5-135">A questo punto, sono accessibili solo da dispositivi che si connettono tooIoT Hub gemelli di dispositivo utilizzando il protocollo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="b04c5-135">At this time, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="b04c5-136">Consultare toohello [supporto MQTT] [ lnk-devguide-mqtt] per istruzioni su come tooconvert esistente dispositivo app toouse MQTT.</span><span class="sxs-lookup"><span data-stu-id="b04c5-136">Please refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>
> 
> 

1. <span data-ttu-id="b04c5-137">Creare una nuova cartella vuota denominata **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="b04c5-137">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="b04c5-138">In hello **reportconnectivity** cartella, creare un nuovo file package. JSON utilizzando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="b04c5-138">In hello **reportconnectivity** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="b04c5-139">Accettare tutte le impostazioni predefinite hello:</span><span class="sxs-lookup"><span data-stu-id="b04c5-139">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="b04c5-140">Al prompt dei comandi in hello **reportconnectivity** cartella, eseguire hello successivo comando tooinstall hello **dispositivi iot di azure**, e **mqtt azure-iot-dispositivo** pacchetto :</span><span class="sxs-lookup"><span data-stu-id="b04c5-140">At your command prompt in hello **reportconnectivity** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="b04c5-141">Utilizzando un editor di testo, creare un nuovo **ReportConnectivity.js** file hello **reportconnectivity** cartella.</span><span class="sxs-lookup"><span data-stu-id="b04c5-141">Using a text editor, create a new **ReportConnectivity.js** file in hello **reportconnectivity** folder.</span></span>
4. <span data-ttu-id="b04c5-142">Aggiungere i seguenti toohello codice hello **ReportConnectivity.js** file e sostituire hello **{stringa di connessione dispositivo}** segnaposto con stringa di connessione dispositivo hello copiato al momento della creazione hello **myDeviceId** identità del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="b04c5-142">Add hello following code toohello **ReportConnectivity.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="b04c5-143">Hello **Client** oggetto espone tutti i metodi di hello desiderate toointeract con gemelli di dispositivo dal dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="b04c5-143">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="b04c5-144">Hello codice precedente, dopo l'inizializzazione hello **Client** oggetto recupera hello gemelli di dispositivo per **myDeviceId** e aggiorna la proprietà segnalata con informazioni sulla connettività hello.</span><span class="sxs-lookup"><span data-stu-id="b04c5-144">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId** and updates its reported property with hello connectivity information.</span></span>
5. <span data-ttu-id="b04c5-145">Eseguire app dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="b04c5-145">Run hello device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="b04c5-146">Verrà visualizzato il messaggio hello `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="b04c5-146">You should see hello message `twin state reported`.</span></span>
6. <span data-ttu-id="b04c5-147">Ora che hello dispositivo segnalato le informazioni di connettività, viene visualizzato in entrambe le query.</span><span class="sxs-lookup"><span data-stu-id="b04c5-147">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="b04c5-148">Andare in hello **addtagsandqueryapp** hello cartella ed eseguire nuovamente una query:</span><span class="sxs-lookup"><span data-stu-id="b04c5-148">Go back in hello **addtagsandqueryapp** folder and run hello queries again:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="b04c5-149">Questa volta **myDeviceId** verrà visualizzato nei risultati di entrambe le query.</span><span class="sxs-lookup"><span data-stu-id="b04c5-149">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][3]

## <a name="next-steps"></a><span data-ttu-id="b04c5-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b04c5-150">Next steps</span></span>
<span data-ttu-id="b04c5-151">In questa esercitazione, è configurato un nuovo hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità.</span><span class="sxs-lookup"><span data-stu-id="b04c5-151">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="b04c5-152">Aggiunti i metadati del dispositivo come tag da un'app di back-end e ha scritto informazioni di connettività un dispositivo simulato app tooreport dispositivo in un doppio dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="b04c5-152">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="b04c5-153">È inoltre appreso tooquery queste informazioni usando il linguaggio di query di hello IoT Hub simile a SQL.</span><span class="sxs-lookup"><span data-stu-id="b04c5-153">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="b04c5-154">Hello utilizzare seguenti come risorse toolearn per:</span><span class="sxs-lookup"><span data-stu-id="b04c5-154">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="b04c5-155">inviare i dati di telemetria dai dispositivi con hello [iniziare con l'IoT Hub] [ lnk-iothub-getstarted] esercitazione</span><span class="sxs-lookup"><span data-stu-id="b04c5-155">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="b04c5-156">configurare i dispositivi con le proprietà desiderate di un doppio dispositivo hello [lo si desidera utilizzare i dispositivi di proprietà tooconfigure] [ lnk-twin-how-to-configure] esercitazione</span><span class="sxs-lookup"><span data-stu-id="b04c5-156">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="b04c5-157">controllare i dispositivi in modo interattivo (ad esempio l'attivazione di una ventola da un'app controllata dall'utente), con hello [utilizzare metodi diretti] [ lnk-methods-tutorial] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b04c5-157">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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
