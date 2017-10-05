---
title: Usare la telemetria dinamica | Documentazione Microsoft
description: Seguire questa esercitazione per imparare a usare la telemetria dinamica con la soluzione preconfigurata per il monitoraggio remoto di Azure IoT Suite.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 0114f27f9b8ae76e1170d04ddf66e2c4bf20686a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-dynamic-telemetry-with-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="a5d9b-103">Usare la telemetria dinamica con la soluzione preconfigurata per il monitoraggio remoto</span><span class="sxs-lookup"><span data-stu-id="a5d9b-103">Use dynamic telemetry with the remote monitoring preconfigured solution</span></span>

<span data-ttu-id="a5d9b-104">La telemetria dinamica consente di visualizzare eventuali dati di telemetria inviati alla soluzione preconfigurata per il monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-104">Dynamic telemetry enables you to visualize any telemetry sent to the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="a5d9b-105">I dispositivi simulati distribuiti con la soluzione preconfigurata inviano dati di telemetria su temperatura e umidità visualizzabili nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-105">The simulated devices that deploy with the preconfigured solution send temperature and humidity telemetry, which you can visualize on the dashboard.</span></span> <span data-ttu-id="a5d9b-106">Se si personalizzano i dispositivi simulati esistenti, si creano nuovi dispositivi simulati o si collegano i dispositivi fisici alla soluzione preconfigurata, è possibile inviare altri valori di telemetria, ad esempio temperatura esterna, RPM o velocità del vento.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-106">If you customize existing simulated devices, create new simulated devices, or connect physical devices to the preconfigured solution you can send other telemetry values such as the external temperature, RPM, or windspeed.</span></span> <span data-ttu-id="a5d9b-107">È quindi possibile visualizzare questi dati di telemetria aggiuntivi nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-107">You can then visualize this additional telemetry on the dashboard.</span></span>

<span data-ttu-id="a5d9b-108">Questa esercitazione usa un semplice dispositivo simulato Node.js facilmente modificabile per provare la telemetria dinamica.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-108">This tutorial uses a simple Node.js simulated device that you can easily modify to experiment with dynamic telemetry.</span></span>

<span data-ttu-id="a5d9b-109">Per completare questa esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a5d9b-109">To complete this tutorial, you’ll need:</span></span>

* <span data-ttu-id="a5d9b-110">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-110">An active Azure subscription.</span></span> <span data-ttu-id="a5d9b-111">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-111">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a5d9b-112">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="a5d9b-112">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="a5d9b-113">[Node.js][lnk-node] 0.12.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-113">[Node.js][lnk-node] version 0.12.x or later.</span></span>

<span data-ttu-id="a5d9b-114">È possibile completare questa esercitazione su qualsiasi sistema operativo, ad esempio Windows o Linux, in cui si può installare Node.js.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-114">You can complete this tutorial on any operating system, such as Windows or Linux, where you can install Node.js.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a><span data-ttu-id="a5d9b-115">Aggiungere un tipo di dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="a5d9b-115">Add a telemetry type</span></span>

<span data-ttu-id="a5d9b-116">Il passaggio successivo consiste nella sostituzione dei dati di telemetria generati dal dispositivo simulato Node.js con un nuovo set di valori:</span><span class="sxs-lookup"><span data-stu-id="a5d9b-116">The next step is to replace the telemetry generated by the Node.js simulated device with a new set of values:</span></span>

1. <span data-ttu-id="a5d9b-117">Arrestare il dispositivo simulato Node.js digitando **Ctrl+C** al prompt dei comandi o nella shell.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-117">Stop the Node.js simulated device by typing **Ctrl+C** in your command prompt or shell.</span></span>
2. <span data-ttu-id="a5d9b-118">Nel file remote_monitoring.js è possibile visualizzare i valori dei dati di base per la telemetria su temperatura, umidità e temperatura esterna esistente.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-118">In the remote_monitoring.js file, you can see the base data values for the existing temperature, humidity, and external temperature telemetry.</span></span> <span data-ttu-id="a5d9b-119">Aggiungere un valore di dati di base per **rpm** come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="a5d9b-119">Add a base data value for **rpm** as follows:</span></span>

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. <span data-ttu-id="a5d9b-120">Il dispositivo simulato Node.js usa la funzione **generateRandomIncrement** nel file remote_monitoring.js per aggiungere un incremento casuale ai valori di dati di base.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-120">The Node.js simulated device uses the **generateRandomIncrement** function in the remote_monitoring.js file to add a random increment to the base data values.</span></span> <span data-ttu-id="a5d9b-121">Impostare in modo casuale il valore **rpm** aggiungendo una riga di codice dopo le sequenze casuali esistenti come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="a5d9b-121">Randomize the **rpm** value by adding a line of code after the existing randomizations as follows:</span></span>

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. <span data-ttu-id="a5d9b-122">Aggiungere il nuovo valore rpm per il payload JSON che il dispositivo invia all'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="a5d9b-122">Add the new rpm value to the JSON payload the device sends to IoT Hub:</span></span>

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. <span data-ttu-id="a5d9b-123">Avviare l'esecuzione del dispositivo simulato Node.js usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a5d9b-123">Run the Node.js simulated device using the following command:</span></span>

    `node remote_monitoring.js`

6. <span data-ttu-id="a5d9b-124">Osservare il nuovo tipo di dati di telemetria RPM visualizzato sul grafico nel dashboard:</span><span class="sxs-lookup"><span data-stu-id="a5d9b-124">Observe the new RPM telemetry type that displays on the chart in the dashboard:</span></span>

![Aggiungere RPM al dashboard][image3]

> [!NOTE]
> <span data-ttu-id="a5d9b-126">Per visualizzare la modifica immediatamente, potrebbe essere necessario disabilitare e quindi abilitare il dispositivo Node.js nella pagina **Devices** (Dispositivi) nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-126">You may need to disable and then enable the Node.js device on the **Devices** page in the dashboard to see the change immediately.</span></span>

## <a name="customize-the-dashboard-display"></a><span data-ttu-id="a5d9b-127">Personalizzare la schermata del dashboard</span><span class="sxs-lookup"><span data-stu-id="a5d9b-127">Customize the dashboard display</span></span>

<span data-ttu-id="a5d9b-128">Il messaggio **Device-Info** può includere i metadati relativi ai dati di telemetria che il dispositivo può inviare all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-128">The **Device-Info** message can include metadata about the telemetry the device can send to IoT Hub.</span></span> <span data-ttu-id="a5d9b-129">Questi metadati possono specificare i tipi di dati di telemetria che il dispositivo invia.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-129">This metadata can specify the telemetry types the device sends.</span></span> <span data-ttu-id="a5d9b-130">Modificare il valore **deviceMetaData** nel file remote_monitoring.js per includere una definizione **Telemetry** dopo la definizione **Commands**.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-130">Modify the **deviceMetaData** value in the remote_monitoring.js file to include a **Telemetry** definition following the **Commands** definition.</span></span> <span data-ttu-id="a5d9b-131">Il frammento di codice seguente illustra la definizione **Commands**. Assicurarsi di aggiungere una `,` dopo la definizione **Commands**:</span><span class="sxs-lookup"><span data-stu-id="a5d9b-131">The following code snippet shows the **Commands** definition (be sure to add a `,` after the **Commands** definition):</span></span>

```nodejs
'Commands': [{
  'Name': 'SetTemperature',
  'Parameters': [{
    'Name': 'Temperature',
    'Type': 'double'
  }]
},
{
  'Name': 'SetHumidity',
  'Parameters': [{
    'Name': 'Humidity',
    'Type': 'double'
  }]
}],
'Telemetry': [{
  'Name': 'Temperature',
  'Type': 'double'
},
{
  'Name': 'Humidity',
  'Type': 'double'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double'
}]
```

> [!NOTE]
> <span data-ttu-id="a5d9b-132">La soluzione di monitoraggio remoto non fa distinzione tra maiuscole e minuscole per confrontare la definizione dei metadati con i dati nel flusso di telemetria.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-132">The remote monitoring solution uses a case-insensitive match to compare the metadata definition with data in the telemetry stream.</span></span>


<span data-ttu-id="a5d9b-133">L'aggiunta di una definizione **Telemetry** , come mostrato nel frammento di codice precedente, non cambia il comportamento del dashboard.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-133">Adding a **Telemetry** definition as shown in the preceding code snippet does not change the behavior of the dashboard.</span></span> <span data-ttu-id="a5d9b-134">Tuttavia, i metadati possono includere anche un attributo **DisplayName** per personalizzare la visualizzazione nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-134">However, the metadata can also include a **DisplayName** attribute to customize the display in the dashboard.</span></span> <span data-ttu-id="a5d9b-135">Aggiornare la definizione dei metadati **Telemetry** come illustrato nel codice seguente:</span><span class="sxs-lookup"><span data-stu-id="a5d9b-135">Update the **Telemetry** metadata definition as shown in the following snippet:</span></span>

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double',
  'DisplayName': 'Outdoor Temperature (C*)'
}
]
```

<span data-ttu-id="a5d9b-136">La schermata seguente illustra in che modo questo cambiamento modifica la legenda del grafico nel dashboard:</span><span class="sxs-lookup"><span data-stu-id="a5d9b-136">The following screenshot shows how this change modifies the chart legend on the dashboard:</span></span>

![Personalizzare la legenda del grafico][image4]

> [!NOTE]
> <span data-ttu-id="a5d9b-138">Per visualizzare la modifica immediatamente, potrebbe essere necessario disabilitare e quindi abilitare il dispositivo Node.js nella pagina **Devices** (Dispositivi) nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-138">You may need to disable and then enable the Node.js device on the **Devices** page in the dashboard to see the change immediately.</span></span>

## <a name="filter-the-telemetry-types"></a><span data-ttu-id="a5d9b-139">Filtrare i tipi di dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="a5d9b-139">Filter the telemetry types</span></span>

<span data-ttu-id="a5d9b-140">Per impostazione predefinita, il grafico nel dashboard mostra ogni serie di dati nel flusso di telemetria.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-140">By default, the chart on the dashboard shows every data series in the telemetry stream.</span></span> <span data-ttu-id="a5d9b-141">È possibile usare i metadati **Device-Info** per disattivare la visualizzazione di tipi di dati di telemetria specifici nel grafico.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-141">You can use the **Device-Info** metadata to suppress the display of specific telemetry types on the chart.</span></span> 

<span data-ttu-id="a5d9b-142">Per far sì che il grafico mostri solo i dati di telemetria su temperatura e umidità, omettere **ExternalTemperature** dai metadati **Device-Info** **Telemetry** nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="a5d9b-142">To make the chart show only Temperature and Humidity telemetry, omit **ExternalTemperature** from the **Device-Info** **Telemetry** metadata as follows:</span></span>

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
//{
//  'Name': 'ExternalTemperature',
//  'Type': 'double',
//  'DisplayName': 'Outdoor Temperature (C*)'
//}
]
```

<span data-ttu-id="a5d9b-143">La **temperatura esterna** non viene più visualizzata sul grafico:</span><span class="sxs-lookup"><span data-stu-id="a5d9b-143">The **Outdoor Temperature** no longer displays on the chart:</span></span>

![Filtrare i dati di telemetria nel dashboard][image5]

<span data-ttu-id="a5d9b-145">Questa modifica interessa solo la visualizzazione del grafico.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-145">This change only affects the chart display.</span></span> <span data-ttu-id="a5d9b-146">Tuttavia, i valori dei dati **ExternalTemperature** vengono comunque memorizzati e resi disponibili per qualsiasi elaborazione back-end.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-146">The **ExternalTemperature** data values are still stored and made available for any backend processing.</span></span>

> [!NOTE]
> <span data-ttu-id="a5d9b-147">Per visualizzare la modifica immediatamente, potrebbe essere necessario disabilitare e quindi abilitare il dispositivo Node.js nella pagina **Devices** (Dispositivi) nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-147">You may need to disable and then enable the Node.js device on the **Devices** page in the dashboard to see the change immediately.</span></span>

## <a name="handle-errors"></a><span data-ttu-id="a5d9b-148">Gestire gli errori</span><span class="sxs-lookup"><span data-stu-id="a5d9b-148">Handle errors</span></span>

<span data-ttu-id="a5d9b-149">Per visualizzare un flusso di dati sul grafico, il relativo attributo **Type** nei metadati **Device-Info** deve corrispondere al tipo di dati dei valori di telemetria.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-149">For a data stream to display on the chart, its **Type** in the **Device-Info** metadata must match the data type of the telemetry values.</span></span> <span data-ttu-id="a5d9b-150">Se ad esempio i metadati specificano che l'attributo **Type** dei dati sull'umidità è **int** ma nel flusso di dati di telemetria è indicato **double**, i dati di telemetria sull'umidità non saranno visualizzati nel grafico.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-150">For example, if the metadata specifies that the **Type** of humidity data is **int** and a **double** is found in the telemetry stream then the humidity telemetry does not display on the chart.</span></span> <span data-ttu-id="a5d9b-151">Tuttavia, i valori **Humidity** vengono comunque memorizzati e resi disponibili per qualsiasi elaborazione back-end.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-151">However, the **Humidity** values are still stored and made available for any back-end processing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5d9b-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a5d9b-152">Next steps</span></span>

<span data-ttu-id="a5d9b-153">Ora che si è appreso come usare la telemetria dinamica, è possibile consultare altre informazioni su come le soluzioni preconfigurate possono usare le informazioni sul dispositivo in [Metadati di informazioni sul dispositivo nella soluzione preconfigurata per il monitoraggio remoto][lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="a5d9b-153">Now that you've seen how to use dynamic telemetry, you can learn more about how the preconfigured solutions use device information: [Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
