---
title: dati di telemetria dinamica aaaUse | Documenti Microsoft
description: Seguire questa esercitazione toolearn come dati di telemetria dinamica toouse con monitoraggio remoto di hello Azure IoT Suite preconfigurato soluzione.
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
ms.openlocfilehash: 06cb2a370b67b4950efdfa4c7d906ac92106f4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-dynamic-telemetry-with-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="30d88-103">Utilizzare i dati di telemetria dinamico con hello soluzione preconfigurata di monitoraggio remoto</span><span class="sxs-lookup"><span data-stu-id="30d88-103">Use dynamic telemetry with hello remote monitoring preconfigured solution</span></span>

<span data-ttu-id="30d88-104">Telemetria dinamica consente si toovisualize qualsiasi toohello telemetria inviato soluzione preconfigurata di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="30d88-104">Dynamic telemetry enables you toovisualize any telemetry sent toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="30d88-105">dispositivi di Hello simulato distribuiti con la soluzione hello preconfigurato inviano temperatura e umidità telemetria, è possibile visualizzare nel dashboard di hello.</span><span class="sxs-lookup"><span data-stu-id="30d88-105">hello simulated devices that deploy with hello preconfigured solution send temperature and humidity telemetry, which you can visualize on hello dashboard.</span></span> <span data-ttu-id="30d88-106">Se si personalizzano dispositivi simulati esistenti, creare nuovi dispositivi simulati o connettere i dispositivi fisici toohello preconfigurato soluzione è possibile inviare altri valori di dati di telemetria come temperatura esterno hello, RPM o velocità del vento.</span><span class="sxs-lookup"><span data-stu-id="30d88-106">If you customize existing simulated devices, create new simulated devices, or connect physical devices toohello preconfigured solution you can send other telemetry values such as hello external temperature, RPM, or windspeed.</span></span> <span data-ttu-id="30d88-107">È quindi possibile visualizzare questi dati di telemetria aggiuntive nel dashboard di hello.</span><span class="sxs-lookup"><span data-stu-id="30d88-107">You can then visualize this additional telemetry on hello dashboard.</span></span>

<span data-ttu-id="30d88-108">Questa esercitazione viene utilizzato un semplice dispositivo simulato Node. js che è possibile modificare facilmente tooexperiment con dati di telemetria dinamica.</span><span class="sxs-lookup"><span data-stu-id="30d88-108">This tutorial uses a simple Node.js simulated device that you can easily modify tooexperiment with dynamic telemetry.</span></span>

<span data-ttu-id="30d88-109">toocomplete questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="30d88-109">toocomplete this tutorial, you’ll need:</span></span>

* <span data-ttu-id="30d88-110">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="30d88-110">An active Azure subscription.</span></span> <span data-ttu-id="30d88-111">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="30d88-111">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="30d88-112">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="30d88-112">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="30d88-113">[Node.js][lnk-node] 0.12.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="30d88-113">[Node.js][lnk-node] version 0.12.x or later.</span></span>

<span data-ttu-id="30d88-114">È possibile completare questa esercitazione su qualsiasi sistema operativo, ad esempio Windows o Linux, in cui si può installare Node.js.</span><span class="sxs-lookup"><span data-stu-id="30d88-114">You can complete this tutorial on any operating system, such as Windows or Linux, where you can install Node.js.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a><span data-ttu-id="30d88-115">Aggiungere un tipo di dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="30d88-115">Add a telemetry type</span></span>

<span data-ttu-id="30d88-116">passaggio successivo Hello è telemetria hello tooreplace generato dal dispositivo simulato hello di Node. js con un nuovo set di valori:</span><span class="sxs-lookup"><span data-stu-id="30d88-116">hello next step is tooreplace hello telemetry generated by hello Node.js simulated device with a new set of values:</span></span>

1. <span data-ttu-id="30d88-117">Arresto hello Node.js dispositivo simulato digitando **Ctrl + C** nel prompt dei comandi o della shell.</span><span class="sxs-lookup"><span data-stu-id="30d88-117">Stop hello Node.js simulated device by typing **Ctrl+C** in your command prompt or shell.</span></span>
2. <span data-ttu-id="30d88-118">Nel file remote_monitoring.js hello, è possibile visualizzare i valori di dati di base hello per temperatura esistente hello e umidità, dati di telemetria temperatura esterno.</span><span class="sxs-lookup"><span data-stu-id="30d88-118">In hello remote_monitoring.js file, you can see hello base data values for hello existing temperature, humidity, and external temperature telemetry.</span></span> <span data-ttu-id="30d88-119">Aggiungere un valore di dati di base per **rpm** come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="30d88-119">Add a base data value for **rpm** as follows:</span></span>

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. <span data-ttu-id="30d88-120">dispositivo simulato di Hello Node.js utilizza hello **generateRandomIncrement** in hello remote_monitoring.js file tooadd toohello un incremento casuale dati di base di valori di funzione.</span><span class="sxs-lookup"><span data-stu-id="30d88-120">hello Node.js simulated device uses hello **generateRandomIncrement** function in hello remote_monitoring.js file tooadd a random increment toohello base data values.</span></span> <span data-ttu-id="30d88-121">Scegliere in modo casuale hello **rpm** valore aggiungendo una riga di codice dopo casuali esistente hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="30d88-121">Randomize hello **rpm** value by adding a line of code after hello existing randomizations as follows:</span></span>

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. <span data-ttu-id="30d88-122">Aggiungere hello nuovo rpm valore toohello JSON payload hello dispositivo invia tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="30d88-122">Add hello new rpm value toohello JSON payload hello device sends tooIoT Hub:</span></span>

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. <span data-ttu-id="30d88-123">Eseguire dispositivo simulato Node.js hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="30d88-123">Run hello Node.js simulated device using hello following command:</span></span>

    `node remote_monitoring.js`

6. <span data-ttu-id="30d88-124">Osservare hello nuovo RPM telemetria tipo che verrà visualizzato nel grafico hello nel dashboard di hello:</span><span class="sxs-lookup"><span data-stu-id="30d88-124">Observe hello new RPM telemetry type that displays on hello chart in hello dashboard:</span></span>

![Aggiungere dashboard toohello RPM][image3]

> [!NOTE]
> <span data-ttu-id="30d88-126">È possibile toodisable necessario e quindi abilitare dispositivo Node.js hello hello **dispositivi** pagina Modifica hello di hello dashboard toosee immediatamente.</span><span class="sxs-lookup"><span data-stu-id="30d88-126">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="customize-hello-dashboard-display"></a><span data-ttu-id="30d88-127">Personalizzare la visualizzazione dashboard hello</span><span class="sxs-lookup"><span data-stu-id="30d88-127">Customize hello dashboard display</span></span>

<span data-ttu-id="30d88-128">Hello **informazioni sul dispositivo** messaggio può includere i metadati sulla telemetria di hello dispositivo hello può inviare tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="30d88-128">hello **Device-Info** message can include metadata about hello telemetry hello device can send tooIoT Hub.</span></span> <span data-ttu-id="30d88-129">Questi metadati è possono specificare i tipi di dati di telemetria hello hello dispositivo invia.</span><span class="sxs-lookup"><span data-stu-id="30d88-129">This metadata can specify hello telemetry types hello device sends.</span></span> <span data-ttu-id="30d88-130">Modificare hello **deviceMetaData** valore hello remote_monitoring.js file tooinclude un **telemetria** definizione dopo hello **comandi** definizione.</span><span class="sxs-lookup"><span data-stu-id="30d88-130">Modify hello **deviceMetaData** value in hello remote_monitoring.js file tooinclude a **Telemetry** definition following hello **Commands** definition.</span></span> <span data-ttu-id="30d88-131">Hello frammento di codice seguente viene illustrato hello **comandi** definizione (tooadd assicurarsi di essere un `,` dopo hello **comandi** definizione):</span><span class="sxs-lookup"><span data-stu-id="30d88-131">hello following code snippet shows hello **Commands** definition (be sure tooadd a `,` after hello **Commands** definition):</span></span>

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
> <span data-ttu-id="30d88-132">soluzione di monitoraggio remoto Hello utilizza una definizione di metadati di distinzione tra maiuscole toocompare hello con i dati nel flusso di dati di telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="30d88-132">hello remote monitoring solution uses a case-insensitive match toocompare hello metadata definition with data in hello telemetry stream.</span></span>


<span data-ttu-id="30d88-133">Aggiunta di un **telemetria** definizione come illustrato nella precedente hello frammento di codice non modifica il comportamento di hello del dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="30d88-133">Adding a **Telemetry** definition as shown in hello preceding code snippet does not change hello behavior of hello dashboard.</span></span> <span data-ttu-id="30d88-134">Tuttavia, è possono anche includere metadati hello un **DisplayName** toocustomize hello visualizzato nel dashboard di hello dell'attributo.</span><span class="sxs-lookup"><span data-stu-id="30d88-134">However, hello metadata can also include a **DisplayName** attribute toocustomize hello display in hello dashboard.</span></span> <span data-ttu-id="30d88-135">Hello aggiornamento **telemetria** definizione dei metadati, come illustrato nel seguente frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="30d88-135">Update hello **Telemetry** metadata definition as shown in hello following snippet:</span></span>

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

<span data-ttu-id="30d88-136">Hello schermata seguente mostra in che modo questa modifica modifica legenda del grafico hello dashboard hello:</span><span class="sxs-lookup"><span data-stu-id="30d88-136">hello following screenshot shows how this change modifies hello chart legend on hello dashboard:</span></span>

![Personalizzare una legenda del grafico hello][image4]

> [!NOTE]
> <span data-ttu-id="30d88-138">È possibile toodisable necessario e quindi abilitare dispositivo Node.js hello hello **dispositivi** pagina Modifica hello di hello dashboard toosee immediatamente.</span><span class="sxs-lookup"><span data-stu-id="30d88-138">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="filter-hello-telemetry-types"></a><span data-ttu-id="30d88-139">Filtrare i tipi di dati di telemetria hello</span><span class="sxs-lookup"><span data-stu-id="30d88-139">Filter hello telemetry types</span></span>

<span data-ttu-id="30d88-140">Per impostazione predefinita, il grafico di hello dashboard hello Mostra ogni serie di dati nel flusso di dati di telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="30d88-140">By default, hello chart on hello dashboard shows every data series in hello telemetry stream.</span></span> <span data-ttu-id="30d88-141">È possibile utilizzare hello **informazioni sul dispositivo** toosuppress metadati hello la visualizzazione dei tipi di dati di telemetria specifico sul grafico hello.</span><span class="sxs-lookup"><span data-stu-id="30d88-141">You can use hello **Device-Info** metadata toosuppress hello display of specific telemetry types on hello chart.</span></span> 

<span data-ttu-id="30d88-142">grafico hello toomake Mostra solo temperatura e umidità dati di telemetria, omettere **ExternalTemperature** da hello **informazioni sul dispositivo** **telemetria** metadati come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="30d88-142">toomake hello chart show only Temperature and Humidity telemetry, omit **ExternalTemperature** from hello **Device-Info** **Telemetry** metadata as follows:</span></span>

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

<span data-ttu-id="30d88-143">Hello **temperatura esterni** non vengono più visualizzati sul grafico hello:</span><span class="sxs-lookup"><span data-stu-id="30d88-143">hello **Outdoor Temperature** no longer displays on hello chart:</span></span>

![Filtrare i dati di telemetria relativi hello dashboard hello][image5]

<span data-ttu-id="30d88-145">Questa modifica interessa solo visualizzazione grafico hello.</span><span class="sxs-lookup"><span data-stu-id="30d88-145">This change only affects hello chart display.</span></span> <span data-ttu-id="30d88-146">Hello **ExternalTemperature** i valori dei dati vengono comunque memorizzati e resi disponibili per operazioni di elaborazione back-end.</span><span class="sxs-lookup"><span data-stu-id="30d88-146">hello **ExternalTemperature** data values are still stored and made available for any backend processing.</span></span>

> [!NOTE]
> <span data-ttu-id="30d88-147">È possibile toodisable necessario e quindi abilitare dispositivo Node.js hello hello **dispositivi** pagina Modifica hello di hello dashboard toosee immediatamente.</span><span class="sxs-lookup"><span data-stu-id="30d88-147">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="handle-errors"></a><span data-ttu-id="30d88-148">Gestire gli errori</span><span class="sxs-lookup"><span data-stu-id="30d88-148">Handle errors</span></span>

<span data-ttu-id="30d88-149">Per un toodisplay del flusso di dati nel grafico hello, il relativo **tipo** in hello **informazioni sul dispositivo** metadati devono corrispondere il tipo di dati hello dei valori di dati di telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="30d88-149">For a data stream toodisplay on hello chart, its **Type** in hello **Device-Info** metadata must match hello data type of hello telemetry values.</span></span> <span data-ttu-id="30d88-150">Ad esempio, se hello metadati specificano tale hello **tipo** di umidità sono dati **int** e **doppie** viene rilevato nel flusso di dati di telemetria hello telemetria umidità hello non non visualizzare nel grafico hello.</span><span class="sxs-lookup"><span data-stu-id="30d88-150">For example, if hello metadata specifies that hello **Type** of humidity data is **int** and a **double** is found in hello telemetry stream then hello humidity telemetry does not display on hello chart.</span></span> <span data-ttu-id="30d88-151">Tuttavia, hello **umidità** valori ancora archiviati e rese disponibili per qualsiasi elaborazione back-end.</span><span class="sxs-lookup"><span data-stu-id="30d88-151">However, hello **Humidity** values are still stored and made available for any back-end processing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30d88-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="30d88-152">Next steps</span></span>

<span data-ttu-id="30d88-153">Ora che si è visto come telemetria dinamica toouse, sono disponibili ulteriori informazioni su come hello preconfigurato soluzioni utilizzare informazioni sul dispositivo: [metadati informazioni del dispositivo in Monitoraggio remoto hello preconfigurato soluzione] [ lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="30d88-153">Now that you've seen how toouse dynamic telemetry, you can learn more about how hello preconfigured solutions use device information: [Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
