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
# <a name="use-dynamic-telemetry-with-hello-remote-monitoring-preconfigured-solution"></a>Utilizzare i dati di telemetria dinamico con hello soluzione preconfigurata di monitoraggio remoto

Telemetria dinamica consente si toovisualize qualsiasi toohello telemetria inviato soluzione preconfigurata di monitoraggio remoto. dispositivi di Hello simulato distribuiti con la soluzione hello preconfigurato inviano temperatura e umidità telemetria, è possibile visualizzare nel dashboard di hello. Se si personalizzano dispositivi simulati esistenti, creare nuovi dispositivi simulati o connettere i dispositivi fisici toohello preconfigurato soluzione è possibile inviare altri valori di dati di telemetria come temperatura esterno hello, RPM o velocità del vento. È quindi possibile visualizzare questi dati di telemetria aggiuntive nel dashboard di hello.

Questa esercitazione viene utilizzato un semplice dispositivo simulato Node. js che è possibile modificare facilmente tooexperiment con dati di telemetria dinamica.

toocomplete questa esercitazione, è necessario:

* Una sottoscrizione di Azure attiva. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk_free_trial].
* [Node.js][lnk-node] 0.12.x o versione successiva.

È possibile completare questa esercitazione su qualsiasi sistema operativo, ad esempio Windows o Linux, in cui si può installare Node.js.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a>Aggiungere un tipo di dati di telemetria

passaggio successivo Hello è telemetria hello tooreplace generato dal dispositivo simulato hello di Node. js con un nuovo set di valori:

1. Arresto hello Node.js dispositivo simulato digitando **Ctrl + C** nel prompt dei comandi o della shell.
2. Nel file remote_monitoring.js hello, è possibile visualizzare i valori di dati di base hello per temperatura esistente hello e umidità, dati di telemetria temperatura esterno. Aggiungere un valore di dati di base per **rpm** come indicato di seguito:

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. dispositivo simulato di Hello Node.js utilizza hello **generateRandomIncrement** in hello remote_monitoring.js file tooadd toohello un incremento casuale dati di base di valori di funzione. Scegliere in modo casuale hello **rpm** valore aggiungendo una riga di codice dopo casuali esistente hello come indicato di seguito:

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. Aggiungere hello nuovo rpm valore toohello JSON payload hello dispositivo invia tooIoT Hub:

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. Eseguire dispositivo simulato Node.js hello utilizzando hello comando seguente:

    `node remote_monitoring.js`

6. Osservare hello nuovo RPM telemetria tipo che verrà visualizzato nel grafico hello nel dashboard di hello:

![Aggiungere dashboard toohello RPM][image3]

> [!NOTE]
> È possibile toodisable necessario e quindi abilitare dispositivo Node.js hello hello **dispositivi** pagina Modifica hello di hello dashboard toosee immediatamente.

## <a name="customize-hello-dashboard-display"></a>Personalizzare la visualizzazione dashboard hello

Hello **informazioni sul dispositivo** messaggio può includere i metadati sulla telemetria di hello dispositivo hello può inviare tooIoT Hub. Questi metadati è possono specificare i tipi di dati di telemetria hello hello dispositivo invia. Modificare hello **deviceMetaData** valore hello remote_monitoring.js file tooinclude un **telemetria** definizione dopo hello **comandi** definizione. Hello frammento di codice seguente viene illustrato hello **comandi** definizione (tooadd assicurarsi di essere un `,` dopo hello **comandi** definizione):

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
> soluzione di monitoraggio remoto Hello utilizza una definizione di metadati di distinzione tra maiuscole toocompare hello con i dati nel flusso di dati di telemetria hello.


Aggiunta di un **telemetria** definizione come illustrato nella precedente hello frammento di codice non modifica il comportamento di hello del dashboard hello. Tuttavia, è possono anche includere metadati hello un **DisplayName** toocustomize hello visualizzato nel dashboard di hello dell'attributo. Hello aggiornamento **telemetria** definizione dei metadati, come illustrato nel seguente frammento di codice hello:

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

Hello schermata seguente mostra in che modo questa modifica modifica legenda del grafico hello dashboard hello:

![Personalizzare una legenda del grafico hello][image4]

> [!NOTE]
> È possibile toodisable necessario e quindi abilitare dispositivo Node.js hello hello **dispositivi** pagina Modifica hello di hello dashboard toosee immediatamente.

## <a name="filter-hello-telemetry-types"></a>Filtrare i tipi di dati di telemetria hello

Per impostazione predefinita, il grafico di hello dashboard hello Mostra ogni serie di dati nel flusso di dati di telemetria hello. È possibile utilizzare hello **informazioni sul dispositivo** toosuppress metadati hello la visualizzazione dei tipi di dati di telemetria specifico sul grafico hello. 

grafico hello toomake Mostra solo temperatura e umidità dati di telemetria, omettere **ExternalTemperature** da hello **informazioni sul dispositivo** **telemetria** metadati come indicato di seguito:

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

Hello **temperatura esterni** non vengono più visualizzati sul grafico hello:

![Filtrare i dati di telemetria relativi hello dashboard hello][image5]

Questa modifica interessa solo visualizzazione grafico hello. Hello **ExternalTemperature** i valori dei dati vengono comunque memorizzati e resi disponibili per operazioni di elaborazione back-end.

> [!NOTE]
> È possibile toodisable necessario e quindi abilitare dispositivo Node.js hello hello **dispositivi** pagina Modifica hello di hello dashboard toosee immediatamente.

## <a name="handle-errors"></a>Gestire gli errori

Per un toodisplay del flusso di dati nel grafico hello, il relativo **tipo** in hello **informazioni sul dispositivo** metadati devono corrispondere il tipo di dati hello dei valori di dati di telemetria hello. Ad esempio, se hello metadati specificano tale hello **tipo** di umidità sono dati **int** e **doppie** viene rilevato nel flusso di dati di telemetria hello telemetria umidità hello non non visualizzare nel grafico hello. Tuttavia, hello **umidità** valori ancora archiviati e rese disponibili per qualsiasi elaborazione back-end.

## <a name="next-steps"></a>Passaggi successivi

Ora che si è visto come telemetria dinamica toouse, sono disponibili ulteriori informazioni su come hello preconfigurato soluzioni utilizzare informazioni sul dispositivo: [metadati informazioni del dispositivo in Monitoraggio remoto hello preconfigurato soluzione] [ lnk-devinfo].

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
