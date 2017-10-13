---
title: Personalizzazione di soluzioni preconfigurate | Documentazione Microsoft
description: Fornisce una guida alla personalizzazione delle soluzioni preconfigurate di Azure IoT Suite.
services: 
suite: iot-suite
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4653ae53-4110-4a10-bd6c-7dc034c293a8
ms.service: iot-suite
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/15/2017
ms.author: corywink
ms.openlocfilehash: 110085f8a4ef0b22b1b4982615eabc29487f9413
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="customize-a-preconfigured-solution"></a>Personalizzare una soluzione preconfigurata

Le soluzioni preconfigurate disponibili in Azure IoT Suite dimostrano come i servizi nella suite si integrano per fornire una soluzione end-to-end. Esistono poi diverse posizioni in cui è possibile personalizzare ed estendere la soluzione per adattarla a scenari specifici. Le sezioni seguenti descrivono questi punti di personalizzazione comuni.

## <a name="find-the-source-code"></a>Trovare il codice sorgente

Il codice sorgente per le soluzioni preconfigurate è disponibile in GitHub nei repository seguenti:

* Monitoraggio remoto: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)
* Manutenzione predittiva: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)
* Factory connesso: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)

Il codice sorgente per le soluzioni preconfigurate viene fornito per illustrare i modelli e le procedure usate per implementare la funzionalità end-to-end di una soluzione IoT tramite Azure IoT Suite. È possibile trovare altre informazioni su come compilare e distribuire le soluzioni in repository GitHub.

## <a name="change-the-preconfigured-rules"></a>Modificare le regole preconfigurate

La soluzione per il monitoraggio remoto include tre processi di [Analisi di flusso di Azure](https://azure.microsoft.com/services/stream-analytics/) per gestire le informazioni sul dispositivo, la telemetria e la logica delle regole nella soluzione.

I tre processi di analisi di flusso e la relativa sintassi sono descritti in dettaglio in [Procedura dettagliata della soluzione preconfigurata per il monitoraggio remoto](iot-suite-remote-monitoring-sample-walkthrough.md). 

È possibile modificare questi processi direttamente per alterare la logica o aggiungere una logica specifica allo scenario. È possibile trovare i processi di analisi di flusso come segue:

1. Accedere al [portale di Azure](https://portal.azure.com).
2. Passare a un nuovo gruppo di risorse con lo stesso nome della soluzione IoT. 
3. Selezionare il processo di Analisi di flusso di Azure che si vuole modificare. 
4. Arrestare il processo selezionando **Arresta** nel set di comandi. 
5. Modificare i valori di input, query e output.
   
    Una modifica semplice consiste nel cambiare la query per il processo **Regole** in modo da usare **"<"** anziché **">"**. Il portale della soluzione visualizza ancora **">"** quando si modifica una regola, ma si noterà come il comportamento viene capovolto a causa della modifica del processo sottostante.
6. Avviare il processo

> [!NOTE]
> Il dashboard per il monitoraggio remoto dipende da dati specifici, quindi la modifica dei processi può causare un errore del dashboard.

## <a name="add-your-own-rules"></a>Aggiungere le regole personalizzate

Oltre a modificare i processi preconfigurati di analisi di flusso di Azure, è possibile usare il portale di Azure per aggiungere nuovi processi o nuove query ai processi esistenti.

## <a name="customize-devices"></a>Personalizzare i dispositivi

Una delle attività di estensione più comuni è l'uso di dispositivi specifici per lo scenario. Esistono diversi metodi per usare i dispositivi, tra cui modificare un dispositivo simulato in modo che corrisponda allo scenario o usare l'[IoT Device SDK][IoT Device SDK] per connettere il dispositivo fisico alla soluzione.

Per indicazioni dettagliate sull'aggiunta di dispositivi, vedere l'articolo [Dispositivi di connessione a Iot Suite](iot-suite-connecting-devices.md) e [Remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring) (Esempio C SDK per il monitoraggio remoto). Questo esempio è stato progettato in modo specifico per la soluzione preconfigurata per il monitoraggio remoto.

### <a name="create-your-own-simulated-device"></a>Creare il dispositivo simulato

Nel [codice sorgente della soluzione per il monitoraggio remoto](https://github.com/Azure/azure-iot-remote-monitoring) è incluso un simulatore .NET. Il provisioning di questo simulatore viene eseguito nell'ambito della soluzione ed è possibile modificarlo per inviare metadati diversi, la telemetria o per rispondere a comandi e metodi diversi.

Il simulatore preconfigurato nella soluzione preconfigurata per il monitoraggio remoto simula un dispositivo ad accesso sporadico che emette dati di telemetria su temperatura e umidità. È possibile modificare il simulatore nel progetto [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) una volta duplicato il repository di GitHub.

### <a name="available-locations-for-simulated-devices"></a>Posizioni disponibili per i dispositivi simulati

Il set predefinito di posizioni si trova a Seattle/Redmond, Washington, Stati Uniti d'America. È possibile modificare queste località nel file [SampleDeviceFactory.cs][lnk-sample-device-factory].

### <a name="add-a-desired-property-update-handler-to-the-simulator"></a>Aggiungere un gestore di aggiornamento della proprietà desiderata al simulatore

È possibile configurare un valore per la proprietà desiderata per un dispositivo nel portale della soluzione. La gestione della richiesta di modifica della proprietà quando il dispositivo recupera il valore della proprietà desiderata è a carico del dispositivo. Per aggiungere il supporto per una modifica del valore della proprietà tramite una proprietà desiderata, è necessario aggiungere un gestore al simulatore.

Il simulatore contiene gestori per le proprietà **SetPointTemp** e **TelemetryInterval** che possono essere aggiornate impostando i valori desiderati nel portale della soluzione.

L'esempio seguente mostra il gestore per la proprietà desiderata **SetPointTemp** nella classe **CoolerDevice**:

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

Questo metodo aggiorna la temperatura del punto dati di telemetria e quindi segnala la modifica all'hub IoT impostando una proprietà segnalata.

È possibile aggiungere gestori personalizzati per le proprietà specifiche seguendo il modello dell'esempio precedente.

È anche necessario associare la proprietà desiderata al gestore, come illustrato nell'esempio seguente dal costruttore **CoolerDevice**:

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

Si noti che **SetPointTempPropertyName** è una costante definita come "Config.SetPointTemp".

### <a name="add-support-for-a-new-method-to-the-simulator"></a>Aggiungere il supporto per un nuovo metodo al simulatore

È possibile personalizzare il simulatore per aggiungere il supporto per un nuovo [metodo (metodo diretto)][lnk-direct-methods]. La procedura prevede due passaggi principali:

- Il simulatore deve inviare una notifica all'hub IoT nella soluzione preconfigurata con i dettagli del metodo.
- Il simulatore deve includere il codice per gestire la chiamata al metodo quando viene richiamato dal pannello **Dettagli dispositivo** in Esplora soluzioni o tramite un processo.

La soluzione preconfigurata per il monitoraggio remoto usa le *proprietà segnalate* per inviare i dettagli dei metodi supportati all'hub IoT. Il back-end della soluzione gestisce un elenco di tutti i metodi supportati da ogni dispositivo, insieme a una cronologia delle chiamate al metodo. È possibile visualizzare queste informazioni sui dispositivi e richiamare i metodi nel portale della soluzione.

Per segnalare all'hub IoT che un dispositivo supporta un metodo, il dispositivo deve aggiungere i dettagli del metodo al nodo **SupportedMethods** nelle proprietà segnalate:

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

La firma del metodo ha il formato seguente: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`. Per specificare, ad esempio, che il metodo **InitiateFirmwareUpdate** prevede un parametro di stringa denominato **FwPackageURI**, usare la firma del metodo seguente:

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

Per un elenco di tipi di parametri supportati, vedere la classe **CommandTypes** nel progetto Infrastructure.

Per eliminare un metodo, impostare la firma del metodo su `null` nelle proprietà segnalate.

> [!NOTE]
> Il back-end della soluzione aggiorna solo le informazioni sui metodi supportati quando riceve un messaggio sulle *informazioni del dispositivo* dal dispositivo.

L'esempio di codice seguente dalla classe **SampleDeviceFactory** nel progetto Common mostra come aggiungere un metodo all'elenco **SupportedMethods** nelle proprietà segnalate inviate dal dispositivo:

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' to specifiy the URI of the firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

Questo frammento di codice aggiunge i dettagli del metodo **InitiateFirmwareUpdate**, incluso il testo da visualizzare nel portale della soluzione e i dettagli dei parametri del metodo necessario.

Il simulatore invia le proprietà segnalate, incluso l'elenco dei metodi supportati, all'hub IoT quando viene avviato.

Aggiungere un gestore al codice del simulatore per ogni metodo supportato. È possibile visualizzare i gestori esistenti nella classe **CoolerDevice** del progetto Simulator.WebJob. L'esempio seguente mostra il gestore per il metodo **InitiateFirmwareUpdate**:

```csharp
public async Task<MethodResponse> OnInitiateFirmwareUpdate(MethodRequest methodRequest, object userContext)
{
    if (_deviceManagementTask != null && !_deviceManagementTask.IsCompleted)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "Device is busy"
        }, 409));
    }

    try
    {
        var operation = new FirmwareUpdate(methodRequest);
        _deviceManagementTask = operation.Run(Transport).ContinueWith(async task =>
        {
            // after firmware completed, we reset telemetry
            var telemetry = _telemetryController as ITelemetryWithTemperatureMeanValue;
            if (telemetry != null)
            {
                telemetry.TemperatureMeanValue = 34.5;
            }

            await UpdateReportedTemperatureMeanValue();
        });

        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "FirmwareUpdate accepted",
            Uri = operation.Uri
        }));
    }
    catch (Exception ex)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = ex.Message
        }, 400));
    }
}
```

I nomi dei gestori dei metodi devono iniziare con `On`, seguito dal nome del metodo. Il parametro **methodRequest** contiene tutti i parametri passati con la chiamata al metodo dal back-end della soluzione. Il valore restituito deve essere di tipo **Task&lt;MethodResponse&gt;**. Il metodo **BuildMethodResponse** dell'utilità consente di creare il valore restituito.

All'interno del gestore del metodo è possibile eseguire queste operazioni:

- Avviare un'attività asincrona.
- Recuperare le proprietà desiderate dal *dispositivo gemello* nell'hub IoT.
- Aggiornare una singola proprietà segnalata usando il metodo **SetReportedPropertyAsync** nella classe **CoolerDevice**.
- Aggiornare più proprietà segnalate creando un'istanza di **TwinCollection** e chiamando il metodo **Transport.UpdateReportedPropertiesAsync**.

L'esempio precedente di aggiornamento del firmware segue questa procedura:

- Controlla che il dispositivo sia in grado di accettare la richiesta di aggiornamento del firmware.
- Avvia in modo asincrono l'operazione di aggiornamento del firmware e reimposta i dati di telemetria al termine dell'operazione.
- Restituisce immediatamente il messaggio "FirmwareUpdate accepted" per indicare che la richiesta è stata accettata dal dispositivo.

### <a name="build-and-use-your-own-physical-device"></a>Compilare e usare il proprio dispositivo (fisico)

Gli [SDK Azure IoT](https://github.com/Azure/azure-iot-sdks) forniscono librerie per la connessione di numerosi tipi di dispositivi (linguaggi e sistemi operativi) alle soluzioni IoT.

## <a name="modify-dashboard-limits"></a>Modificare i limiti del dashboard

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a>Numero di dispositivi visualizzati nell'elenco a discesa del dashboard

Il valore predefinito è 200. È possibile modificare questo numero nel file [DashboardController.cs][lnk-dashboard-controller].

### <a name="number-of-pins-to-display-in-bing-map-control"></a>Numero di pin da visualizzare nel controllo di Bing Mappe

Il valore predefinito è 200. È possibile modificare questo numero nel file [TelemetryApiController.cs][lnk-telemetry-api-controller-01].

### <a name="time-period-of-telemetry-graph"></a>Periodo di tempo del grafico di dati di telemetria

Il valore predefinito è 10 minuti. È possibile modificare questo valore nel file [TelmetryApiController.cs][lnk-telemetry-api-controller-02].

## <a name="manually-set-up-application-roles"></a>Configurare manualmente i ruoli dell'applicazione

La procedura seguente descrive come aggiungere i ruoli applicazione **Admin** e **ReadOnly** a una soluzione preconfigurata. Si noti che le soluzioni preconfigurate per le quali è stato eseguito il provisioning dal sito azureiotsuite.com includono già i ruoli **Admin** e **ReadOnly**.

I membri del ruolo **ReadOnly** possono visualizzare il dashboard e l'elenco dei dispositivi, ma non sono autorizzati ad aggiungere dispositivi, modificare gli attributi del dispositivo o inviare comandi.  I membri del ruolo **Admin** hanno accesso completo a tutte le funzionalità nella soluzione.

1. Passare al [portale di Azure classico][lnk-classic-portal].
2. Selezionare **Active Directory**.
3. Fare clic sul nome del tenant AAD usato durante il provisioning della soluzione.
4. Fare clic su **Applicazioni**.
5. Fare clic sul nome dell'applicazione che coincide con il nome della soluzione preconfigurata. Se l'applicazione non viene visualizzata nell'elenco, selezionare **Applicazioni di proprietà dell'azienda** nell'elenco a discesa **Mostra** e fare clic sul segno di spunta.
6. Nella parte inferiore della pagina fare clic su **Gestisci manifesto** e quindi su **Scarica manifesto**.
7. Questa procedura scarica un file con estensione JSON nel computer locale. Aprire il file per modificarlo in un editor di testo di propria scelta.
8. Nella terza riga del file con estensione JSON, è possibile trovare:

   ```json
   "appRoles" : [],
   ```
   Sostituire questa riga con il codice seguente:

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access to the application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access to device information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. Salvare il file con estensione JSON aggiornato (è possibile sovrascrivere il file esistente).
10. Nel portale di Azure classico, nella parte inferiore della pagina selezionare **Gestisci manifesto** e quindi **Carica manifesto** per caricare il file con estensione json salvato nel passaggio precedente.
11. Sono stati aggiunti all'applicazione i ruoli **Admin** e **ReadOnly**.
12. Per assegnare uno di questi ruoli a un utente nella directory, vedere [Autorizzazioni per il sito azureiotsuite.com][lnk-permissions].

## <a name="feedback"></a>Commenti e suggerimenti

Per altre informazioni relative a una personalizzazione, Inviare suggerimenti sulla funzionalità a [User Voice](https://feedback.azure.com/forums/321918-azure-iot) oppure lasciare un commento nell'apposita sezione di questo articolo. 

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle opzioni per personalizzare le soluzioni preconfigurate, vedere:

* [Connettere l'app per la logica alla soluzione preconfigurata per il monitoraggio remoto Azure IoT Suite][lnk-logicapp]
* [Usare la telemetria dinamica con la soluzione preconfigurata per il monitoraggio remoto][lnk-dynamic]
* [Metadati di informazioni sul dispositivo nella soluzione preconfigurata per il monitoraggio remoto][lnk-devinfo]
* [Personalizzare la modalità di visualizzazione dei dati dai server OPC UA da parte della soluzione del factory connesso][lnk-cf-customize]

[lnk-logicapp]: iot-suite-logic-apps-tutorial.md
[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[IoT Device SDK]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-permissions]: iot-suite-permissions.md
[lnk-dashboard-controller]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/Controllers/DashboardController.cs#L27
[lnk-telemetry-api-controller-01]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L27
[lnk-telemetry-api-controller-02]: https://github.com/Azure/azure-iot-remote-monitoring/blob/e7003339f73e21d3930f71ceba1e74fb5c0d9ea0/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L25 
[lnk-sample-device-factory]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Common/Factory/SampleDeviceFactory.cs#L40
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-cf-customize]: iot-suite-connected-factory-customize.md