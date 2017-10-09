---
title: aaaCustomizing preconfigurato soluzioni | Documenti Microsoft
description: Vengono fornite indicazioni su come toocustomize hello Azure IoT Suite preconfigurato soluzioni.
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
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 1a8573f5ac6ed944c44459df495446f15174d513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-a-preconfigured-solution"></a>Personalizzare una soluzione preconfigurata

soluzioni Hello preconfigurato fornite con hello Azure IoT Suite dimostrano dei servizi di hello all'interno di hello suite lavoro insieme toodeliver una soluzione end-to-end. A questo punto di partenza, sono disponibili vari punti in cui è possibile estendere e personalizzare soluzioni hello per scenari specifici. Hello le sezioni seguenti vengono descritti questi punti di personalizzazione comuni.

## <a name="find-hello-source-code"></a>Trovare il codice sorgente hello

il codice sorgente Hello per le soluzioni hello preconfigurato è disponibile in hello seguenti repository in GitHub:

* Monitoraggio remoto: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)
* Manutenzione predittiva: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)
* Factory connesso: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)

il codice sorgente Hello per le soluzioni hello preconfigurato è fornite procedure consigliate e i pattern di hello toodemonstrate utilizzata la funzionalità di tooimplement hello end-to-end di una soluzione IoT utilizzando Azure IoT Suite. È possibile trovare altre informazioni su come toobuild e distribuire soluzioni hello nei repository GitHub hello.

## <a name="change-hello-preconfigured-rules"></a>Modificare le regole di hello preconfigurato

Hello soluzione di monitoraggio remoto include tre [Azure flusso Analitica](https://azure.microsoft.com/services/stream-analytics/) processi toohandle informazioni del dispositivo, la telemetria e logica delle regole nella soluzione hello.

Hello tre flusso processi analitica e la loro sintassi sono descritti in dettaglio in hello [monitoraggio remoto preconfigurato procedura dettagliata sulla soluzione](iot-suite-remote-monitoring-sample-walkthrough.md). 

È possibile modificare questi processi direttamente tooalter hello logica, o aggiungere logica tooyour specifico scenario. È possibile trovare hello Analitica flusso processi come indicato di seguito:

1. Andare troppo[portale di Azure](https://portal.azure.com).
2. Passare il gruppo di risorse toohello con stesso nome come soluzione IoT hello. 
3. Selezionare il processo di Azure flusso Analitica hello toomodify desiderato. 
4. Processo di arresto hello selezionando **arrestare** nel set di hello di comandi. 
5. Modificare gli output, query e gli input hello.
   
    Una semplice modifica è query hello toochange per hello **regole** toouse processo un **"<"** anziché un **">"**. portale di soluzione Hello viene comunque mostrata **">"** quando si modifica una regola, ma si noti come comportamento hello viene capovolta a causa di modifica toohello hello processo sottostante.
6. Avviare il processo di hello

> [!NOTE]
> dashboard di monitoraggio remoto Hello dipende dai dati specifici, pertanto modifica processi hello può causare toofail dashboard hello.

## <a name="add-your-own-rules"></a>Aggiungere le regole personalizzate

Inoltre toochanging hello preconfigurato processi Analitica di flusso di Azure, è possibile utilizzare i nuovi processi hello tooadd portale Azure o aggiungere nuovi processi tooexisting di query.

## <a name="customize-devices"></a>Personalizzare i dispositivi

Uno dei più comuni attività di estensione hello funziona con scenari con dispositivi tooyour specifico. Esistono diversi metodi per usare i dispositivi, Questi metodi includono la modifica di un toomatch dispositivo simulato lo scenario o utilizzando hello [SDK dispositivo IoT] [ IoT Device SDK] tooconnect soluzione toohello dispositivo fisico.

Per i dispositivi tooadding una Guida dettagliata, vedere hello [i dispositivi Iot Suite connessione](iot-suite-connecting-devices.md) articolo e hello [monitoraggio esempio SDK C remota](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring). Questo esempio è progettato toowork con hello soluzione preconfigurata di monitoraggio remoto.

### <a name="create-your-own-simulated-device"></a>Creare il dispositivo simulato

Incluso in hello [il codice sorgente della soluzione di monitoraggio remoto](https://github.com/Azure/azure-iot-remote-monitoring), è un simulatore di .NET. Il simulatore è hello uno stato effettuato il provisioning come parte della soluzione hello ed è possibile modificarla toosend metadati diversi, dati di telemetria e rispondere metodi e i comandi toodifferent.

simulatore preconfigurata di Hello nella soluzione preconfigurata di monitoraggio remoto hello simula un dispositivo di raffreddamento dispositivo che genera i dati di telemetria temperatura e umidità. È possibile modificare il simulatore hello in hello [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) quando è stata duplicata repository GitHub hello del progetto.

### <a name="available-locations-for-simulated-devices"></a>Posizioni disponibili per i dispositivi simulati

set di percorsi predefinito Hello è in Seattle/Redmond, Washington, Stati Uniti d'America. È possibile modificare queste località nel file [SampleDeviceFactory.cs][lnk-sample-device-factory].

### <a name="add-a-desired-property-update-handler-toohello-simulator"></a>Aggiungere un simulatore di toohello gestore aggiornamento proprietà desiderata

È possibile impostare un valore per una proprietà desiderata per un dispositivo nel portale di soluzione hello. È responsabilità di hello della richiesta di modifica proprietà hello dispositivo toohandle hello quando dispositivo hello recupera il valore di proprietà hello desiderato. supporto tooadd per la modifica di un valore di proprietà tramite una proprietà desiderata, è necessario un simulatore toohello gestore tooadd.

simulatore Hello contiene gestori per hello **SetPointTemp** e **TelemetryInterval** le proprietà che è possibile aggiornare impostando desiderati valori nel portale di soluzione hello.

Hello esempio seguente viene illustrato il gestore di hello per hello **SetPointTemp** proprietà in hello desiderata **CoolerDevice** classe:

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

Questo metodo aggiorna il punto di dati di telemetria hello temperatura e quindi hello report modificare tooIoT indietro Hub impostando una proprietà segnalata.

È possibile aggiungere i propri gestori per le proprietà dal modello hello in hello sopra riportato.

È necessario anche associare gestore toohello di hello proprietà desiderata come illustrato nel seguente esempio di hello hello **CoolerDevice** costruttore:

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

Si noti che **SetPointTempPropertyName** è una costante definita come "Config.SetPointTemp".

### <a name="add-support-for-a-new-method-toohello-simulator"></a>Aggiungere il supporto per un nuovo simulatore toohello (metodo)

È possibile personalizzare il supporto di hello simulatore tooadd per un nuovo [metodo (metodo diretto)][lnk-direct-methods]. La procedura prevede due passaggi principali:

- simulatore Hello deve notificare hub IoT hello nella soluzione hello preconfigurato con i dettagli del metodo hello.
- simulatore Hello deve includere chiamata al metodo hello toohandle codice quando viene richiamata da hello **dettagli dispositivo** pannello in Esplora soluzioni hello o tramite un processo.

Hello monitoraggio remoto preconfigurato soluzione utilizza *segnalati proprietà* toosend dettagli dell'hub tooIoT metodi supportati. back-end di Hello soluzione gestisce un elenco di tutti i metodi di hello supportati da ogni dispositivo insieme a una cronologia delle chiamate al metodo. È possibile visualizzare queste informazioni sui dispositivi e richiamare i metodi nel portale di soluzione hello.

toonotify hello IoT hub che un dispositivo supporta un metodo, il dispositivo hello necessario aggiungere i dettagli di hello metodo toohello **SupportedMethods** nodo hello segnalati proprietà:

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

firma del metodo Hello è hello seguente formato: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`. Ad esempio, toospecify hello **InitiateFirmwareUpdate** metodo prevede un parametro di stringa denominato **FwPackageURI**, utilizzare hello firma del metodo seguente:

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

Per un elenco dei tipi di parametro supportati, vedere hello **CommandTypes** classe nel progetto di infrastruttura hello.

toodelete un metodo, impostare la firma del metodo hello troppo`null` in hello segnalati proprietà.

> [!NOTE]
> Hello soluzione back-end solo Aggiorna le informazioni sui metodi supportati quando si riceve un *informazioni sul dispositivo* messaggi da dispositivo hello.

Hello seguente codice di esempio hello **SampleDeviceFactory** classe hello comune progetto viene mostrato come un elenco di metodo toohello tooadd di **SupportedMethods** in hello segnalati proprietà inviata dal hello dispositivo:

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' toospecifiy hello URI of hello firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

Questo frammento di codice aggiunge dettagli di hello **InitiateFirmwareUpdate** metodo incluso testo toodisplay portale soluzione hello e i dettagli di hello richiesto parametri del metodo.

simulatore Hello invia proprietà segnalate, tra cui elenco hello dei metodi supportati, tooIoT Hub simulatore hello all'avvio.

Aggiungere un codice del simulatore toohello gestore per ogni metodo che supporta. È possibile visualizzare i gestori esistenti hello hello **CoolerDevice** classe nel progetto Simulator.WebJob hello. Hello esempio seguente viene illustrato il gestore di hello per **InitiateFirmwareUpdate** metodo:

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

I nomi dei gestori di metodo deve iniziare con `On` aggiungendo il nome del metodo hello hello. Hello **methodRequest** parametro contiene tutti i parametri passati con la chiamata di metodo hello dal back-end di hello soluzione. Hello valore restituito deve essere di tipo **attività&lt;MethodResponse&gt;**. Hello **BuildMethodResponse** metodo di utilità consente di creare il valore restituito di hello.

All'interno di gestore del metodo hello, è possibile:

- Avviare un'attività asincrona.
- Recuperare le proprietà desiderate da hello *doppi dispositivo* nell'IoT Hub.
- Aggiornare una singola proprietà segnalate tramite hello **SetReportedPropertyAsync** metodo hello **CoolerDevice** classe.
- Aggiornare più proprietà segnalate tramite la creazione di un **TwinCollection** istanza e chiamata hello **Transport.UpdateReportedPropertiesAsync** metodo.

Hello precedente esempio di aggiornamento del firmware esegue hello alla procedura seguente:

- Controlli dispositivo di hello è richiesta di aggiornamento del firmware tooaccept in grado di hello.
- Avvia l'operazione di aggiornamento del firmware hello e reimposta i dati di telemetria hello quando hello operazione è stata completata in modo asincrono.
- Immediatamente restituisce hello "FirmwareUpdate accettato" messaggio tooindicate hello richiesta è stata accettata dal dispositivo hello.

### <a name="build-and-use-your-own-physical-device"></a>Compilare e usare il proprio dispositivo (fisico)

Hello [Azure IoT SDK](https://github.com/Azure/azure-iot-sdks) forniscono librerie per la connessione di vari tipi di dispositivo (lingue e i sistemi operativi) in soluzioni IoT.

## <a name="modify-dashboard-limits"></a>Modificare i limiti del dashboard

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a>Numero di dispositivi visualizzati nell'elenco a discesa del dashboard

valore predefinito di Hello è 200. È possibile modificare questo numero nel file [DashboardController.cs][lnk-dashboard-controller].

### <a name="number-of-pins-toodisplay-in-bing-map-control"></a>Numero di pin toodisplay nel controllo mappa di Bing

valore predefinito di Hello è 200. È possibile modificare questo numero nel file [TelemetryApiController.cs][lnk-telemetry-api-controller-01].

### <a name="time-period-of-telemetry-graph"></a>Periodo di tempo del grafico di dati di telemetria

valore predefinito di Hello è 10 minuti. È possibile modificare questo valore nel file [TelmetryApiController.cs][lnk-telemetry-api-controller-02].

## <a name="manually-set-up-application-roles"></a>Configurare manualmente i ruoli dell'applicazione

Hello procedura riportata di seguito viene descritto come tooadd **Admin** e **ReadOnly** tooa ruoli applicazione preconfigurato soluzione. Si noti che le soluzioni preconfigurate già eseguito il provisioning dal sito azureiotsuite.com hello includono hello **Admin** e **ReadOnly** ruoli.

I membri di hello **ReadOnly** ruolo è possibile visualizzare dashboard hello e l'elenco dei dispositivi hello, ma non sono consentiti tooadd dispositivi, gli attributi di modifica dispositivo o i comandi di trasmissione.  I membri di hello **Admin** ruolo dispone di funzionalità di accesso completo tooall hello nella soluzione hello.

1. Passare toohello [portale di Azure classico][lnk-classic-portal].
2. Selezionare **Active Directory**.
3. Fare clic su nome hello del tenant AAD hello che è utilizzato quando è stato effettuato il provisioning della soluzione.
4. Fare clic su **Applicazioni**.
5. Fare clic su nome hello dell'applicazione hello che corrisponde al nome della soluzione preconfigurata. Se non viene visualizzata l'applicazione nell'elenco di hello, selezionare **applicazioni proprietà dell'azienda** in hello **Mostra** elenco a discesa e fare clic su hello segno di spunta.
6. Nella parte inferiore di hello della pagina hello, fare clic su **Gestisci manifesto** e quindi **Scarica manifesto**.
7. Questa procedura consente di scaricare una versione locale macchina tooyour di file con estensione JSON. Aprire il file per modificarlo in un editor di testo di propria scelta.
8. Nella terza riga hello del file con estensione JSON hello, è possibile visualizzare:

   ```json
   "appRoles" : [],
   ```
   Sostituire questa riga con hello seguente codice:

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access toohello application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access toodevice information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. Salvare file con estensione JSON aggiornato hello (è possibile sovrascrivere il file esistente di hello).
10. Nel portale di Azure classico, nella parte inferiore di hello della pagina hello hello selezionare **Gestisci manifesto** quindi **carica manifesto** file con estensione JSON di hello tooupload salvato nel passaggio precedente hello.
11. È stato aggiunto hello **Admin** e **ReadOnly** applicazione tooyour dei ruoli.
12. tooassign uno di questi utente tooa ruoli nella directory, vedere [le autorizzazioni nel sito azureiotsuite.com hello][lnk-permissions].

## <a name="feedback"></a>Commenti e suggerimenti

Si dispone di una personalizzazione che si desidera toosee trattate in questo documento? Aggiungere i suggerimenti sulle funzionalità troppo[Uservoice](https://feedback.azure.com/forums/321918-azure-iot), o un commento di questo articolo. 

## <a name="next-steps"></a>Passaggi successivi

toolearn più sulle opzioni di hello per personalizzare soluzioni hello preconfigurato, vedere:

* [Connessione logica App tooyour Azure IoT Suite remoto preconfigurato soluzione di monitoraggio][lnk-logicapp]
* [Utilizzare i dati di telemetria dinamico con hello soluzione preconfigurata di monitoraggio remoto][lnk-dynamic]
* [Metadati informazioni del dispositivo nella soluzione preconfigurata di monitoraggio remoto hello][lnk-devinfo]
* [Personalizzare la modalità di connessione factory soluzione consente di visualizzare dati dai server OPC UA hello][lnk-cf-customize]

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