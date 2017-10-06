---
title: aaaAzure Application Insights Snapshot Debugger per le app .NET | Documenti Microsoft
description: Gli snapshot di debug vengono raccolti automaticamente quando vengono generate eccezioni nelle app di produzione .NET
services: application-insights
documentationcenter: 
author: qubitron
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: bwren
ms.openlocfilehash: f0173a752b5795d934fbab1bd53eb077433edc90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a>Snapshot di debug per le eccezioni nelle app .NET

Quando si verifica un'eccezione, è possibile raccogliere automaticamente uno snapshot di debug dall'applicazione Web live. lo snapshot di Hello Mostra lo stato di hello del codice sorgente e le variabili a eccezione di hello hello momento in cui è stata generata. Hello Debugger Snapshot (anteprima) in [Azure Application Insights](app-insights-overview.md) monitora telemetria delle eccezioni dall'app web. Raccolta di snapshot nella generazione superiore eccezioni in modo da disporre di informazioni hello necessarie toodiagnose problemi nell'ambiente di produzione. Includere hello [pacchetto NuGet di agente di raccolta dati dello Snapshot](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) nell'applicazione e, facoltativamente, configurare i parametri della raccolta in [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md). Snapshot sono visualizzati in [eccezioni](app-insights-asp-net-exceptions.md) portale Application Insights hello.

È possibile visualizzare gli snapshot di debug nello stack di chiamate di hello toosee portale hello e controllare le variabili in ogni frame dello stack di chiamate. un'esperienza di debug più potente con codice sorgente, open snapshot con Visual Studio 2017 Enterprise da tooget [il download di estensione del Debugger Snapshot hello per Visual Studio](https://aka.ms/snapshotdebugger).

La raccolta di snapshot è disponibile per:
* Applicazioni .NET Framework e ASP.NET che eseguono .NET Framework 4.5 o versione successiva.
* Applicazioni .NET Core 2.0 e ASP.NET Core 2.0 in esecuzione in Windows.

### <a name="configure-snapshot-collection-for-aspnet-applications"></a>Configurare la raccolta di snapshot per le applicazioni ASP.NET

1. [Abilitare Application Insights nell'app Web](app-insights-asp-net.md) se non è ancora stato fatto.

2. Includere hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) pacchetto NuGet dell'app. 

3. Esaminare le opzioni predefinite hello hello pacchetto aggiunto troppo[Applicationinsights](app-insights-configuration-with-applicationinsights-config.md):

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- hello default is true, but you can disable Snapshot Debugging by setting it toofalse -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this tootrue. -->
        <!-- DeveloperMode is a property on hello active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need toosee an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- hello maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- hello maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often tooreset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- hello maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- hello maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. Gli snapshot vengono raccolti solo sulle eccezioni che vengono segnalati tooApplication Insights. In alcuni casi (ad esempio, versioni precedenti della piattaforma .NET hello), potrebbe essere troppo[configurare la raccolta di eccezioni](app-insights-asp-net-exceptions.md#exceptions) toosee eccezioni con gli snapshot nel portale di hello.


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a>Configurare la raccolta di snapshot per le applicazioni ASP.NET Core 2.0

1. [Abilitare Application Insights nell'app Web ASP.NET Core](app-insights-asp-net-core.md) se non è ancora stato fatto.

2. Includere hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) pacchetto NuGet dell'app.

3. Modificare hello `ConfigureServices` metodo dell'applicazione `Startup` classe del processore di tooadd hello Snapshot dell'agente di raccolta dati di telemetria. è consigliabile aggiungere codice di Hello dipende dalla versione di cui viene fatto riferimento hello del pacchetto Microsoft.ApplicationInsights.ASPNETCore NuGet hello.

   Per Microsoft.ApplicationInsights.AspNetCore 2.1.0 aggiungere:
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   Per Microsoft.ApplicationInsights.AspNetCore 2.1.1 aggiungere:
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       private class SnapshotCollectorTelemetryProcessorFactory : ITelemetryProcessorFactory
       {
           public ITelemetryProcessor Create(ITelemetryProcessor next) =>
               new SnapshotCollectorTelemetryProcessor(next);
       }

       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a>Configurare la raccolta di snapshot per le altre applicazioni .NET

1. Se l'applicazione non è già instrumentato con Application Insights, è possibile iniziare [l'abilitazione di Application Insights e chiave di strumentazione hello impostazione](app-insights-windows-desktop.md).

2. Aggiungere hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) pacchetto NuGet dell'app.

3. Gli snapshot vengono raccolti solo sulle eccezioni che vengono segnalati tooApplication Insights. Potrebbe essere necessario toomodify tooreport il codice li. gestione delle eccezioni Hello dipende dalla struttura hello dell'applicazione, ma è un esempio di seguito:
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle hello request.
        }
        catch (Exception ex)
        {
            // Report hello exception tooApplication Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow hello exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a>Concedere le autorizzazioni

I proprietari di hello sottoscrizione di Azure è possono esaminare gli snapshot. Agli altri utenti deve essere concessa l'autorizzazione da un proprietario.

autorizzazione toogrant, assegnare hello `Application Insights Snapshot Debugger` toousers di ruolo che esamina gli snapshot. Questo ruolo può essere assegnato tooindividual utenti o gruppi per i proprietari di sottoscrizioni per la destinazione di hello risorsa di Application Insights oppure il suo gruppo di risorse o sottoscrizione.

1. Aprire il pannello di controllo di accesso (IAM) hello.
1. Fare clic su hello + pulsante Aggiungi.
1. Selezionare Application Insights Snapshot Debugger dall'elenco a discesa hello ruoli.
1. Cercare e immettere un nome per tooadd utente hello.
1. Fare clic su ruolo toohello hello Salva pulsante tooadd hello utente.


[!IMPORTANT]
    Gli snapshot possono contenere informazioni personali e altre informazioni riservate nei valori delle variabili e dei parametri.

## <a name="debug-snapshots-in-hello-application-insights-portal"></a>Eseguire il debug di snapshot nel portale Application Insights hello

Se uno snapshot è disponibile per una determinata eccezione o un ID problema, un **Apri Snapshot Debug** pulsante viene visualizzato in hello [eccezione](app-insights-asp-net-exceptions.md) portale Application Insights hello.

![Pulsante Open Debug Snapshot per l'eccezione](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

In visualizzazione di Snapshot di eseguire il Debug di hello, viene visualizzato uno stack di chiamate e un riquadro variabili. Quando si seleziona dello stack frame di chiamata hello nel riquadro dello stack di chiamate hello, è possibile visualizzare le variabili locali e parametri per la funzione chiamata nel riquadro variabili hello.

![Visualizzazione Debug Snapshot nel portale di hello](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

Gli snapshot potrebbero contenere informazioni riservate e per impostazione predefinita non sono visibili. tooview snapshot, è necessario disporre di hello `Application Insights Snapshot Debugger` tooyou ruolo assegnato.

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a>Snapshot di debug con Visual Studio 2017 Enterprise
1. Fare clic su hello **scaricare Snapshot** toodownload pulsante un `.diagsession` file, che può essere aperta da Visual Studio 2017 Enterprise. 

2. hello tooopen `.diagsession` file, è innanzitutto necessario [scaricare e installare l'estensione del Debugger Snapshot hello per Visual Studio](https://aka.ms/snapshotdebugger).

3. Dopo aver aperto il file di snapshot hello, verrà visualizzata la pagina di debug di Minidump hello in Visual Studio. Fare clic su **eseguire il Debug di codice gestito** toostart debug snapshot hello. snapshot Hello apre toohello riga di codice in cui è stata generata l'eccezione di hello in modo che è possibile eseguire il debug dello stato corrente di hello del processo di hello.

    ![Visualizzare lo snapshot di debug in Visual Studio](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

snapshot scaricato Hello contiene tutti i file di simboli che sono stati trovati nel server applicazioni web. Questi file di simboli sono necessari tooassociate dati di snapshot con codice sorgente. Per le applicazioni di servizio App, verificare la distribuzione di simboli che tooenable quando si pubblica l'App web.

## <a name="how-snapshots-work"></a>Funzionamento degli snapshot

All'avvio dell'applicazione viene creato un processo di caricamento degli snapshot separato che monitora le richieste di snapshot nell'applicazione. Quando viene richiesto uno snapshot, viene effettuata una copia shadow di hello esecuzione processo di circa 10 minuti di too20. processo shadow Hello viene quindi analizzata e uno snapshot viene creato durante il processo principale hello continua toorun e non hanno toousers traffico. Hello snapshot viene quindi caricato tooApplication Insights insieme a eventuali file rilevanti simboli (PDB) che sono necessari tooview snapshot hello.

## <a name="current-limitations"></a>Limitazioni correnti

### <a name="publish-symbols"></a>Pubblicare i simboli
Hello Debugger Snapshot richiede i file di simboli in variabili toodecode server di produzione hello e tooprovide un'esperienza di debug in Visual Studio. versione di Hello 15.2 di Visual Studio 2017 pubblica i simboli per le build di rilascio per impostazione predefinita quando pubblica tooApp servizio. Nelle versioni precedenti, è necessario seguente hello tooadd profilo di pubblicazione riga tooyour `.pubxml` file in modo che i simboli vengono pubblicati in modalità di rilascio:

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

Per altri tipi e calcolo di Azure, verificare che i file di simboli hello siano in hello stessa cartella della DLL principale dell'applicazione hello (in genere, `wwwroot/bin`) o sono disponibili nel percorso corrente hello.

### <a name="optimized-builds"></a>Compilazioni ottimizzate
In alcuni casi, le variabili locali non possono essere visualizzate nelle build di rilascio a causa di ottimizzazioni che vengono applicate durante il processo di compilazione hello.

## <a name="troubleshooting"></a>Risoluzione dei problemi

Questi suggerimenti sulla risoluzione di problemi con hello Debugger Snapshot.

### <a name="verify-hello-instrumentation-key"></a>Verificare la chiave di strumentazione hello

Assicurarsi che si usi chiave di strumentazione corretta hello nell'applicazione pubblicata. In genere, Application Insights legge la chiave di strumentazione hello dal file Applicationinsights config hello. Verificare che il valore di hello è hello stesso come chiave di strumentazione hello per la risorsa di Application Insights hello che sia visualizzato nel portale di hello.

### <a name="check-hello-uploader-logs"></a>Controllare i registri uploader hello

Dopo la creazione di uno snapshot, un file di minidump (DMP) viene creato sul disco. Un processo separato uploader accetta file minidump e lo carica, insieme a qualsiasi file PDB associato, tooApplication archiviazione Insights Snapshot Debugger. Dopo il minidump hello è caricato correttamente, viene eliminato dal disco. file di log Hello per uploader minidump hello vengono mantenuti su disco. In un ambiente del servizio app questi log si trovano in `D:\Home\LogFiles\Uploader_*.log`. Sito di gestione di utilizzare hello Kudu per servizio App toofind i file di registro.

1. Aprire l'applicazione di servizio App in hello portale di Azure.

2. Seleziona hello **strumenti avanzati** pannello oppure cercare **Kudu**.
3. Fare clic su **Vai**.
4. In hello **console Debug** casella di riepilogo a discesa, seleziona **CMD**.
5. Fare clic su **LogFiles**.

Verrà visualizzato almeno un file con il nome che inizia con `Uploader_` e l'estensione `.log`. Fare clic su qualsiasi file di log toodownload sull'icona appropriata hello o aperti in un browser.
nome del file Hello include il nome di computer hello. Se l'istanza del servizio app è ospitata in più di un computer, è presente un file di log separato per ogni computer. Quando il caricatore di hello rileva un nuovo file di minidump, vengono registrate nel file di log hello. Ecco un esempio di caricamento corretto:

```
MinidumpUploader.exe Information: 0 : Dump available 139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:08.0349846Z
MinidumpUploader.exe Information: 0 : Uploading D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp, 329.12 MB
    DateTime=2017-05-25T14:25:16.0145444Z
MinidumpUploader.exe Information: 0 : Upload successful.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Extracting PDB info from D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Matched 2 PDB(s) with local files.
    DateTime=2017-05-25T14:25:44.2310982Z
MinidumpUploader.exe Information: 0 : Stamp does not want any of our matched PDBs.
    DateTime=2017-05-25T14:25:44.5435948Z
MinidumpUploader.exe Information: 0 : Deleted D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:44.6095821Z
```

Nell'esempio precedente hello è la chiave di strumentazione hello `c12a605e73c44346a984e00000000000`. Questo valore deve corrispondere la chiave di strumentazione hello per l'applicazione.
minidump Hello è associata a uno snapshot con ID hello `139e411a23934dc0b9ea08a626db16c5`. È possibile utilizzare questo ID successive hello toolocate associata telemetria delle eccezioni in Application Insights Analitica.

caricatore di Hello esegue l'analisi dei file PDB di nuovo su una sola volta ogni 15 minuti. Ad esempio:

```
MinidumpUploader.exe Information: 0 : PDB rescan requested.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\home\site\wwwroot\ for local PDBs.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\local\Temporary ASP.NET Files\root\a6554c94\e3ad6f22\assembly\dl3\81d5008b\00b93cc8_dec5d201 for local PDBs.
    DateTime=2017-05-25T15:11:38.8160276Z
MinidumpUploader.exe Information: 0 : Local PDB scan complete. Found 2 PDB(s).
    DateTime=2017-05-25T15:11:38.8316450Z
MinidumpUploader.exe Information: 0 : Deleted PDB scan marker D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\.pdbscan.
    DateTime=2017-05-25T15:11:38.8316450Z
```

Per le applicazioni che sono _non_ ospitato nel servizio App, hello uploader log presenti hello stessa cartella minidump hello: `%TEMP%\Dumps\<ikey>` (dove `<ikey>` è la chiave di strumentazione).

### <a name="use-application-insights-search-toofind-exceptions-with-snapshots"></a>Usare Application Insights ricerca toofind eccezioni con gli snapshot

Quando viene creato uno snapshot, hello eccezioni è contrassegnato con un ID dello snapshot. Quando telemetria delle eccezioni hello è segnalato tooApplication Insights, l'ID dello snapshot è incluso come una proprietà personalizzata. Tramite il pannello di ricerca hello in Application Insights, è possibile trovare tutti i dati di telemetria con hello `ai.snapshot.id` proprietà personalizzata.

1. Sfoglia risorsa di Application Insights tooyour in hello portale di Azure.
2. Fare clic su **Search**(Cerca).
3. Tipo `ai.snapshot.id` in hello casella di testo di ricerca e premere INVIO.

![Ricerca di dati di telemetria con un ID dello snapshot nel portale di hello](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

Se la ricerca non restituisce alcun risultato, Nessuno snapshot sono stati segnalati tooApplication Insights per l'applicazione nell'intervallo di tempo hello selezionato.

toosearch per un ID di uno snapshot specifico da log Uploader hello, digitare l'ID nella casella di ricerca hello. Se non è possibile trovare dati di telemetria per uno snapshot che è stato sicuramente caricato, seguire questa procedura:

1. Verificare che si sta consultando risorsa di Application Insights destra hello verificando la chiave di strumentazione hello.

2. Utilizza timestamp hello dal log Uploader hello, filtro di intervallo di tempo hello di hello ricerca toocover regolare l'intervallo di tempo.

Se un'eccezione con tale ID dello snapshot non viene ancora visualizzato, telemetria delle eccezioni hello non è stata segnalata tooApplication Insights. Questa situazione può verificarsi se l'applicazione di arresto anomalo dopo impiegato snapshot hello ma prima che ha segnalato la telemetria delle eccezioni hello. In questo caso, verificare hello log di servizio App in `Diagnose and solve problems` toosee se fossero imprevisto riavvia o le eccezioni non gestite.

## <a name="next-steps"></a>Passaggi successivi

* [Impostare snappoints nel codice](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) tooget snapshot senza attendere che un'eccezione.
* [Diagnosi delle eccezioni nelle App web](app-insights-asp-net-exceptions.md) spiega come toomake altre eccezioni visibili tooApplication Insights. 
* Il [rilevamento intelligente](app-insights-proactive-diagnostics.md) rileva automaticamente le anomalie delle prestazioni.
