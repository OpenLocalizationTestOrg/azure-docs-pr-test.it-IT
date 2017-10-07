---
title: una regola personalizzata in Azure IoT Suite aaaCreate | Documenti Microsoft
description: Una regola personalizzata in un gruppo di IoT toocreate preconfigurato come soluzione.
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
ms.openlocfilehash: 6c5bb2ca54f3f17b99ad482e727c8e9fa28d7fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-rule-in-hello-remote-monitoring-preconfigured-solution"></a>Creare una regola personalizzata in hello soluzione preconfigurata di monitoraggio remoto

## <a name="introduction"></a>Introduzione

Nelle soluzioni hello preconfigurato, è possibile configurare [regole che attivano quando un telemetria valore per un dispositivo raggiunge una soglia specifica][lnk-builtin-rule]. [Utilizzare i dati di telemetria dinamico con hello soluzione preconfigurata di monitoraggio remoto] [ lnk-dynamic-telemetry] descrive come è possibile aggiungere valori di dati di telemetria personalizzati, ad esempio *ExternalTemperature* tooyour soluzione. In questo articolo viene illustrato come tipi di toocreate regola personalizzata per dati di telemetria dinamico nella soluzione.

Questa esercitazione viene utilizzato un semplice Node.js dispositivo simulato toogenerate telemetria dinamica toosend toohello soluzione preconfigurata back-end. Aggiungere quindi una serie di regole personalizzate in hello **RemoteMonitoring** soluzione di Visual Studio e distribuire questo tooyour back-end personalizzato sottoscrizione di Azure.

toocomplete questa esercitazione, è necessario:

* Una sottoscrizione di Azure attiva. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk_free_trial].
* [Node.js] [ lnk-node] versione 0.12.x o versioni successive toocreate un dispositivo simulato.
* Visual Studio 2015 o Visual Studio 2017 toomodify hello preconfigurato soluzione nuovamente terminare con le nuove regole.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

Prendere nota del nome di soluzione hello che scelto per la distribuzione. Il nome della soluzione sarà necessario più avanti nell'esercitazione.

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

È possibile arrestare l'applicazione console in Node.js hello dopo avere verificato che stia inviando **ExternalTemperature** toohello telemetria preconfigurato soluzione. Mantenere aperta la finestra di console hello perché si esegue nuovamente l'app console Node.js dopo aver aggiunto una soluzione di toohello hello regola personalizzata.

## <a name="rule-storage-locations"></a>Posizioni di archiviazione delle regole

Le informazioni sulle regole vengono mantenute in due posizioni:

* **DeviceRulesNormalizedTable** -questa tabella archivia un normalizzato fanno riferimento a regole toohello definite dal portale di soluzione hello. Quando il portale di soluzione hello Visualizza le regole del dispositivo, viene eseguita una query in questa tabella per le definizioni delle regole di hello.
* **DeviceRules** blob: blob archivia tutte le regole di hello definite per tutti i dispositivi registrati e viene definiti come processi di Azure flusso Analitica toohello input un riferimento.
 
Quando si aggiorna una regola esistente o definita una nuova regola nel portale di soluzione hello sia la tabella di hello blob sono modifiche hello tooreflect aggiornato. regola Hello definizione visualizzata nel portale di hello proviene dall'archivio tabelle hello e regola hello definizione fa riferimento a processi di flusso Analitica hello proviene dal blob hello. 

## <a name="update-hello-remotemonitoring-visual-studio-solution"></a>Aggiornare qualsiasi soluzione di Visual Studio RemoteMonitoring hello

Hello passaggi seguenti viene illustrato come toomodify hello tooinclude soluzione Visual Studio RemoteMonitoring una nuova regola che usi hello **ExternalTemperature** telemetria inviato dal dispositivo simulato hello:

1. Se non si è già fatto, hello clone **azure iot-remoto monitoraggio** percorso del repository tooa appropriato nel computer locale utilizzando hello Git comando seguente:

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. In Visual Studio, aprire il file di RemoteMonitoring.sln hello dalla copia locale di hello **azure iot-remoto monitoraggio** repository.

3. Aprire il file hello Infrastructure\Models\DeviceRuleBlobEntity.cs e aggiungere un **ExternalTemperature** proprietà come indicato di seguito:

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. In hello stesso file, aggiungere un **ExternalTemperatureRuleOutput** proprietà come indicato di seguito:

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. Aprire il file hello Infrastructure\Models\DeviceRuleDataFields.cs e aggiungere il seguente hello **ExternalTemperature** proprietà dopo hello esistente **umidità** proprietà:

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. Nel file stesso hello, aggiornare hello **_availableDataFields** metodo tooinclude **ExternalTemperature** come indicato di seguito:

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. Aprire il file hello Infrastructure\Repository\DeviceRulesRepository.cs e modificare hello **BuildBlobEntityListFromTableRows** metodo come indicato di seguito:

    ```csharp
    else if (rule.DataField == DeviceRuleDataFields.Humidity)
    {
        entity.Humidity = rule.Threshold;
        entity.HumidityRuleOutput = rule.RuleOutput;
    }
    else if (rule.DataField == DeviceRuleDataFields.ExternalTemperature)
    {
      entity.ExternalTemperature = rule.Threshold;
      entity.ExternalTemperatureRuleOutput = rule.RuleOutput;
    }
    ```

## <a name="rebuild-and-redeploy-hello-solution"></a>Ricompilare e ridistribuire la soluzione hello.

È ora possibile distribuire hello aggiornato soluzione tooyour sottoscrizione di Azure.

1. Aprire un prompt dei comandi con privilegi elevati e passare toohello radice della copia locale del repository di hello azure iot-remoto monitoraggio.

2. toodeploy la soluzione aggiornata, eseguire hello seguente sostituendo comando **{nome distribuzione}** con nome hello della distribuzione di soluzioni preconfigurate che si è preso nota in precedenza:

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-hello-stream-analytics-job"></a>Aggiornare il processo di flusso Analitica hello

Una volta completata la distribuzione di hello, è possibile aggiornare hello Analitica flusso processo toouse hello nuove definizioni regole.

1. Nel portale di Azure hello, passare toohello gruppo di risorse che contiene le risorse della soluzione preconfigurata. Questo gruppo di risorse hello stesso nome è specificato per hello soluzione durante la distribuzione di hello.

2. Passare toohello {nome distribuzione}-processo regole flusso Analitica. 

3. Fare clic su **arrestare** toostop hello Analitica flusso processo in esecuzione. (È necessario attendere hello toostop processo di streaming prima di poter modificare query hello).

4. Fare clic su **Query**. Modifica hello di hello query tooinclude **selezionare** istruzione per **ExternalTemperature**. Hello seguenti vengono illustrate query completa di hello con hello nuovo **selezionare** istruzione:

    ```
    WITH AlarmsData AS 
    (
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Temperature' as ReadingType,
         Stream.Temperature as Reading,
         Ref.Temperature as Threshold,
         Ref.TemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Humidity' as ReadingType,
         Stream.Humidity as Reading,
         Ref.Humidity as Threshold,
         Ref.HumidityRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'ExternalTemperature' as ReadingType,
         Stream.ExternalTemperature as Reading,
         Ref.ExternalTemperature as Threshold,
         Ref.ExternalTemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.ExternalTemperature IS NOT null AND Stream.ExternalTemperature > Ref.ExternalTemperature
    )
     
    SELECT *
    INTO DeviceRulesMonitoring
    FROM AlarmsData
     
    SELECT *
    INTO DeviceRulesHub
    FROM AlarmsData
    ```

5. Fare clic su **salvare** toochange hello aggiornato query della regola.

6. Fare clic su **avviare** processo di flusso Analitica hello toostart eseguire di nuovo.

## <a name="add-your-new-rule-in-hello-dashboard"></a>Aggiungere la nuova regola nel dashboard di hello

È ora possibile aggiungere hello **ExternalTemperature** dispositivo tooa regola nel dashboard di soluzione hello.

1. Passare il portale di soluzione toohello.

2. Passare toohello **dispositivi** pannello.

3. Individuare hello dispositivo personalizzata creata che invia **ExternalTemperature** telemetria e hello **dettagli dispositivo** pannello, fare clic su **Aggiungi regola**.

4. Selezionare **ExternalTemperature** in **Campo dati**.

5. Impostare **soglia** too56. Quindi fare clic su **Salva e visualizza regole**.

6. Restituisce la cronologia allarme toohello dashboard tooview hello.

7. Nella finestra di console hello è lasciato aperto, avviare l'invio di hello Node.js console app toobegin **ExternalTemperature** i dati di telemetria.

8. Si noti che hello **cronologia allarme** tabella illustra i nuovi avvisi quando hello nuova regola viene attivata.
 
## <a name="additional-information"></a>Informazioni aggiuntive

Modifica operatore hello  **>**  è più complessa e va oltre hello descritte in questa esercitazione. Mentre è possibile modificare hello Analitica flusso processo toouse qualsiasi operatore a cui si desidera, indicare che l'operatore nel portale di soluzione hello è un'attività più complessa. 

## <a name="next-steps"></a>Passaggi successivi
Ora che si è visto come toocreate regole personalizzate, sono disponibili ulteriori informazioni sulle soluzioni preconfigurata hello:

- [Connessione logica App tooyour Azure IoT Suite remoto preconfigurato soluzione di monitoraggio][lnk-logic-app]
- [Metadati del dispositivo informazioni di monitoraggio remoto hello preconfigurato soluzione][lnk-devinfo].

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md