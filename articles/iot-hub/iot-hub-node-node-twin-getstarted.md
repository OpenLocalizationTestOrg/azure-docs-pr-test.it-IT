---
title: Introduzione ai dispositivi gemelli dell'hub IoT di Azure (Node) | Documentazione Microsoft
description: Come usare i dispositivi gemelli dell'hub IoT di Azure per aggiungere tag e quindi usare una query dell'hub IoT. Usare Azure IoT SDK per Node.js per implementare l'app per dispositivo simulato e un'app di servizio che aggiunge i tag ed esegue la query dell'hub IoT.
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
ms.openlocfilehash: 633c9fd4f8a1d017d93148f8c2e860ccba14238c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-device-twins-node"></a><span data-ttu-id="a21af-104">Introduzione ai dispositivi gemelli (Node)</span><span class="sxs-lookup"><span data-stu-id="a21af-104">Get started with device twins (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="a21af-105">Al termine di questa esercitazione si avranno due app console Node.js:</span><span class="sxs-lookup"><span data-stu-id="a21af-105">At the end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="a21af-106">**AddTagsAndQuery.js**, un'app back-end di Node.js, che aggiunge tag ed esegue query sui dispositivi gemelli.</span><span class="sxs-lookup"><span data-stu-id="a21af-106">**AddTagsAndQuery.js**, a Node.js back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="a21af-107">**TwinSimulatedDevice.js**, un'app Node.js che simula un dispositivo che si connette all'hub IoT con l'identità del dispositivo creata prima e segnala la condizione della connettività.</span><span class="sxs-lookup"><span data-stu-id="a21af-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="a21af-108">L'articolo [Azure IoT SDK][lnk-hub-sdks] contiene informazioni sui componenti Azure IoT SDK che consentono di compilare le app back-end e per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="a21af-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="a21af-109">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a21af-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="a21af-110">Node.js 0.10.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="a21af-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="a21af-111">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="a21af-111">An active Azure account.</span></span> <span data-ttu-id="a21af-112">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="a21af-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-service-app"></a><span data-ttu-id="a21af-113">Creare l'app di servizio</span><span class="sxs-lookup"><span data-stu-id="a21af-113">Create the service app</span></span>
<span data-ttu-id="a21af-114">In questa sezione si crea a un'app console Node.js che aggiunge i metadati della posizione al dispositivo gemello associato a **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="a21af-114">In this section, you create a Node.js console app that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="a21af-115">Viene quindi effettuata una query dei dispositivi gemelli archiviati nell'hub IoT selezionando i dispositivi situati negli Stati Uniti e quindi quelli che segnalano una rete cellulare.</span><span class="sxs-lookup"><span data-stu-id="a21af-115">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that are reporting a cellular connection.</span></span>

1. <span data-ttu-id="a21af-116">Creare una nuova cartella vuota denominata **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="a21af-116">Create a new empty folder called **addtagsandqueryapp**.</span></span> <span data-ttu-id="a21af-117">Nella cartella **addtagsandqueryapp** creare un nuovo file package.json immettendo il comando seguente al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="a21af-117">In the **addtagsandqueryapp** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="a21af-118">Accettare tutte le impostazioni predefinite:</span><span class="sxs-lookup"><span data-stu-id="a21af-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="a21af-119">Eseguire questo comando al prompt dei comandi nella cartella **addtagsandqueryapp** per installare il pacchetto **azure-iothub**:</span><span class="sxs-lookup"><span data-stu-id="a21af-119">At your command prompt in the **addtagsandqueryapp** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="a21af-120">Usando un editor di testo, creare un nuovo file **AddTagsAndQuery.js** nella cartella **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="a21af-120">Using a text editor, create a new **AddTagsAndQuery.js** file in the **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="a21af-121">Aggiungere il codice seguente al file **AddTagsAndQuery.js** e sostituire il segnaposto **{iot hub connection string}** con la stringa di connessione dell'hub IoT copiata quando è stato creato l'hub:</span><span class="sxs-lookup"><span data-stu-id="a21af-121">Add the following code to the **AddTagsAndQuery.js** file, and substitute the **{iot hub connection string}** placeholder with the IoT Hub connection string you copied when you created your hub:</span></span>
   
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
   
    <span data-ttu-id="a21af-122">L'oggetto **Registry** espone tutti i metodi necessari per interagire con i dispositivi gemelli dal servizio.</span><span class="sxs-lookup"><span data-stu-id="a21af-122">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="a21af-123">Il codice precedente inizializza prima l'oggetto **Registry**, quindi recupera il dispositivo gemello per **myDeviceId** e infine ne aggiorna i tag con le informazioni sulla posizione desiderate.</span><span class="sxs-lookup"><span data-stu-id="a21af-123">The previous code first initializes the **Registry** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="a21af-124">Dopo avere aggiornato i tag, chiama la funzione **queryTwins**.</span><span class="sxs-lookup"><span data-stu-id="a21af-124">After the updating the tags it calls the **queryTwins** function.</span></span>
5. <span data-ttu-id="a21af-125">Aggiungere il codice seguente alla fine di **AddTagsAndQuery.js** per implementare la funzione **queryTwins**:</span><span class="sxs-lookup"><span data-stu-id="a21af-125">Add the following code at the end of  **AddTagsAndQuery.js** to implement the **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    <span data-ttu-id="a21af-126">Il codice precedente esegue due query: la prima seleziona solo i dispositivi gemelli tra quelli situati nello stabilimento **Redmond43** e la seconda affina la query per selezionare solo i dispositivi che sono anche connessi tramite la rete cellulare.</span><span class="sxs-lookup"><span data-stu-id="a21af-126">The previous code executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="a21af-127">Si noti che il codice precedente, quando crea l'oggetto **query**, specifica un numero massimo di documenti restituiti.</span><span class="sxs-lookup"><span data-stu-id="a21af-127">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="a21af-128">L'oggetto **query** contiene una proprietà booleana **hasMoreResults** che è possibile usare per richiamare i metodi **nextAsTwin** più volte per recuperare tutti i risultati.</span><span class="sxs-lookup"><span data-stu-id="a21af-128">The **query** object contains a **hasMoreResults** boolean property that you can use to invoke the **nextAsTwin** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="a21af-129">Un metodo chiamato **next** è disponibile per i risultati che non sono dispositivi gemelli, ad esempio i risultati delle query di aggregazione.</span><span class="sxs-lookup"><span data-stu-id="a21af-129">A method called **next** is available for results that are not device twins for example, results of aggregation queries.</span></span>
6. <span data-ttu-id="a21af-130">Eseguire l'applicazione con:</span><span class="sxs-lookup"><span data-stu-id="a21af-130">Run the application with:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="a21af-131">Nei risultati si noterà un dispositivo per la query che cerca tutti i dispositivi situati in **Redmond43** e nessuno per la query che limita i risultati ai dispositivi che usano una rete cellulare.</span><span class="sxs-lookup"><span data-stu-id="a21af-131">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![][1]

<span data-ttu-id="a21af-132">Nella sezione successiva si crea un'app per dispositivo che segnala le informazioni sulla connettività e modifica il risultato della query nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="a21af-132">In the next section you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="a21af-133">Creare l'app per dispositivo</span><span class="sxs-lookup"><span data-stu-id="a21af-133">Create the device app</span></span>
<span data-ttu-id="a21af-134">In questa sezione si crea un'app console Node.js che si connette all'hub come **myDeviceId** e quindi aggiorna le proprietà segnalate del dispositivo gemello per poter contenere le informazioni relative alla connessione usando una rete cellulare.</span><span class="sxs-lookup"><span data-stu-id="a21af-134">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, and then updates its device twin's reported properties to contain the information that it is connected using a cellular network.</span></span>

> [!NOTE]
> <span data-ttu-id="a21af-135">Al momento i dispositivi gemelli sono accessibili solo dai dispositivi che si connettono all'hub IoT tramite il protocollo MQTT.</span><span class="sxs-lookup"><span data-stu-id="a21af-135">At this time, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span> <span data-ttu-id="a21af-136">Per istruzioni su come convertire l'app per dispositivo esistente in modo che usi MQTT, vedere l'articolo [Supporto di MQTT][lnk-devguide-mqtt].</span><span class="sxs-lookup"><span data-stu-id="a21af-136">Please refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span></span>
> 
> 

1. <span data-ttu-id="a21af-137">Creare una nuova cartella vuota denominata **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="a21af-137">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="a21af-138">Nella cartella **reportconnectivity** creare un nuovo file package.json immettendo il comando seguente al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="a21af-138">In the **reportconnectivity** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="a21af-139">Accettare tutte le impostazioni predefinite:</span><span class="sxs-lookup"><span data-stu-id="a21af-139">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="a21af-140">Eseguire questo comando al prompt dei comandi nella cartella **reportconnectivity** per installare i pacchetti **azure-iot-device** e **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="a21af-140">At your command prompt in the **reportconnectivity** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="a21af-141">Usando un editor di testo, creare un nuovo file **ReportConnectivity.js** nella cartella **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="a21af-141">Using a text editor, create a new **ReportConnectivity.js** file in the **reportconnectivity** folder.</span></span>
4. <span data-ttu-id="a21af-142">Aggiungere il codice seguente al file **ReportConnectivity.js** e sostituire il segnaposto **{device connection string}** con la stringa di connessione del dispositivo copiata quando si è creata l'identità del dispositivo **myDeviceId**:</span><span class="sxs-lookup"><span data-stu-id="a21af-142">Add the following code to the **ReportConnectivity.js** file, and substitute the **{device connection string}** placeholder with the device connection string you copied when you created the **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="a21af-143">L'oggetto **Client** espone tutti i metodi necessari per interagire con i dispositivi gemelli dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a21af-143">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="a21af-144">Il codice precedente, dopo avere inizializzato l'oggetto **Client**, recupera il dispositivo gemello per **myDeviceId** e aggiorna le proprietà segnalate con le informazioni sulla connettività.</span><span class="sxs-lookup"><span data-stu-id="a21af-144">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId** and updates its reported property with the connectivity information.</span></span>
5. <span data-ttu-id="a21af-145">Eseguire l'app per dispositivo</span><span class="sxs-lookup"><span data-stu-id="a21af-145">Run the device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="a21af-146">Dovrebbe essere visualizzato il messaggio `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="a21af-146">You should see the message `twin state reported`.</span></span>
6. <span data-ttu-id="a21af-147">Ora che il dispositivo ha segnalato le informazioni sulla connettività, verrà visualizzato in entrambe le query.</span><span class="sxs-lookup"><span data-stu-id="a21af-147">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="a21af-148">Tornare alla cartella **addtagsandqueryapp** ed eseguire di nuovo le query:</span><span class="sxs-lookup"><span data-stu-id="a21af-148">Go back in the **addtagsandqueryapp** folder and run the queries again:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="a21af-149">Questa volta **myDeviceId** verrà visualizzato nei risultati di entrambe le query.</span><span class="sxs-lookup"><span data-stu-id="a21af-149">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][3]

## <a name="next-steps"></a><span data-ttu-id="a21af-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a21af-150">Next steps</span></span>
<span data-ttu-id="a21af-151">In questa esercitazione è stato configurato un nuovo hub IoT nel Portale di Azure ed è stata quindi creata un'identità del dispositivo nel registro di identità dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a21af-151">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="a21af-152">Sono stati aggiunti i metadati del dispositivo come tag da un'app back-end ed è stata scritta un'app per dispositivo simulato per segnalare le informazioni sulla connettività del dispositivo nel dispositivo gemello.</span><span class="sxs-lookup"><span data-stu-id="a21af-152">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="a21af-153">Si è anche appreso come effettuare una query di queste informazioni usando il linguaggio di query simile a SQL dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a21af-153">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="a21af-154">Per altre informazioni, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="a21af-154">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="a21af-155">Per inviare dati di telemetria dai dispositivi, vedere l'esercitazione [Introduzione all'hub IoT][lnk-iothub-getstarted].</span><span class="sxs-lookup"><span data-stu-id="a21af-155">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="a21af-156">Per configurare i dispositivi usando le proprietà desiderate del dispositivo gemello, vedere l'esercitazione [Usare le proprietà desiderate per configurare i dispositivi][lnk-twin-how-to-configure].</span><span class="sxs-lookup"><span data-stu-id="a21af-156">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="a21af-157">Per controllare i dispositivi in modo interattivo, ad esempio per attivare un ventilatore da un'app controllata dall'utente, vedere l'esercitazione [Use direct methods][lnk-methods-tutorial] (Usare metodi diretti).</span><span class="sxs-lookup"><span data-stu-id="a21af-157">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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
