---
title: telemetria aaaSeparating dallo sviluppo, test e rilascio in Azure Application Insights | Documenti Microsoft
description: Risorse di toodifferent diretto telemetria per gli indicatori di sviluppo, test e produzione.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 578e30f0-31ed-4f39-baa8-01b4c2f310c9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: a294c8c70f46d7c29b460461c3494c83e13a0cbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a>Separazione della telemetria da sviluppo, test e produzione

Quando si sviluppa prossima versione di hello di un'applicazione web, non si desidera toomix backup hello [Application Insights](app-insights-overview.md) telemetria dalla nuova versione di hello e hello già rilasciato. tooavoid confusione, trasmissione hello telemetria dallo sviluppo diverso fasi di risorse di Application Insights tooseparate, con chiavi di strumentazione separato (ikeys). toomake si sposta da una fase tooanother, chiave di strumentazione hello toochange più semplice come una versione può essere utile tooset hello ikey nel codice anziché in file di configurazione hello. 

Se il sistema è un servizio cloud di Azure, è disponibile [un altro metodo di impostazione di valori iKey separati](app-insights-cloudservices.md).)

## <a name="about-resources-and-instrumentation-keys"></a>Sulle risorse e le chiavi di strumentazione

Quando si configura il monitoraggio di Application Insights per l'app Web, viene creata una *risorsa* di Application Insights in Microsoft Azure. Aprire questa risorsa nel portale di Azure in ordine toosee hello e analizzare dati di telemetria hello raccolti dall'app. risorsa Hello è identificato da un *chiave di strumentazione* (ikey). Quando si installa hello Application Insights pacchetto toomonitor dell'app, si configura con chiave di strumentazione hello, in modo che rilevi dove toosend hello telemetria.

È in genere scegliere risorse diverse toouse o una singola risorsa condivisa in scenari diversi:

* Diverse applicazioni indipendenti: usare una risorsa separata e l'iKey per ogni applicazione.
* Utilizzare più componenti o i ruoli dell'applicazione di una business - un [singola risorsa condivisa](app-insights-monitor-multi-role-apps.md) per tutte le app di componente di hello. Dati di telemetria può essere filtrato o segmentate per proprietà cloud_RoleName hello.
* Sviluppo, Test e rilascio: utilizzare una risorsa distinta e ikey per le versioni del sistema hello in 'timestamp' o una fase di produzione.
* Test A | B: usare una singola risorsa. È possibile creare un tooadd TelemetryInitializer telemetria di toohello una proprietà che identifica le varianti hello.


## <a name="dynamic-ikey"></a> Chiave di strumentazione dinamica

toomake che più semplice toochange hello ikey come codice hello si sposta tra le diverse fasi di produzione, impostati nel codice anziché nel file di configurazione di hello.

Impostare la chiave di hello in un metodo di inizializzazione, ad esempio global.aspx.cs in un servizio ASP.NET:

*C#*

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

In questo esempio, ikeys hello per le diverse risorse hello vengono posizionate in diverse versioni del file di configurazione web hello. File di configurazione web hello scambio, che è possibile eseguire come parte dello script di versione di hello - scambiano risorsa di destinazione hello.

### <a name="web-pages"></a>Pagina Web
iKey Hello viene utilizzato anche nelle pagine web dell'app, in hello [script che è stato ottenuto dal pannello avvio rapido hello](app-insights-javascript.md). Anziché nel codice viene letteralmente in script hello, generati dallo stato del server hello. Ad esempio, in un'app ASP.NET:

*JavaScript in Razor*

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a>Creare risorse di Application Insights aggiuntive
dati di telemetria tooseparate per componenti diversi dell'applicazione o per timbri differenti (sviluppo/test o produzione) di hello stesso componente, sarà necessario toocreate una nuova risorsa di Application Insights.

In hello [portal.azure.com](https://portal.azure.com), aggiungere una risorsa di Application Insights:

![Fare clic su Nuovo, Application Insights](./media/app-insights-separate-resources/01-new.png)

* **Tipo di applicazione** influisce su ciò che viene visualizzato nel pannello della panoramica hello e le proprietà di hello disponibili in [Esplora metrica](app-insights-metrics-explorer.md). Se non viene visualizzato il tipo di app, scegliere uno dei tipi di web hello per le pagine web.
* **gruppo di risorse** è utile per gestire le proprietà come il [controllo di accesso](app-insights-resources-roles-access-controldi Microsoft Azure.md)di Microsoft Azure. È possibile usare gruppi di risorse separati per lo sviluppo, i test e la produzione.
* **sottoscrizione** è il proprio account di pagamento in Azure.
* Il **percorso** è la posizione in cui vengono conservati i dati. e attualmente non è modificabile. 
* **Aggiungere toodashboard** assegna un riquadro di accesso rapido per la risorsa per la Home page di Azure. 

Creazione di risorse hello richiede pochi secondi. Al termine della creazione verrà visualizzato un avviso.

(È possibile scrivere un [script di PowerShell](app-insights-powershell-script-create-resource.md) toocreate una risorsa automaticamente.)

### <a name="getting-hello-instrumentation-key"></a>Ottenere la chiave di strumentazione hello
chiave di strumentazione Hello identifica risorse hello creato. 

![Essentials fare clic su hello chiave di strumentazione, CTRL + C](./media/app-insights-separate-resources/02-props.png)

Sono necessarie le chiavi di strumentazione hello di tutti i toowhich risorse hello l'app verrà inviato alcun dato.

## <a name="filter-on-build-number"></a>Filtrare in base al numero di build
Quando si pubblica una nuova versione dell'app, è opportuno telemetria di hello in grado di tooseparate toobe dalle build diverse.

È possibile impostare proprietà di versione dell'applicazione hello in modo che è possibile filtrare [ricerca](app-insights-diagnostic-search.md) e [Esplora metrica](app-insights-metrics-explorer.md) risultati.

![Filtro su una proprietà](./media/app-insights-separate-resources/050-filter.png)

Esistono diversi metodi di impostazione di proprietà di versione dell'applicazione hello.

* Impostare direttamente:

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* Eseguire il wrapping di tale riga in un [inizializzatore telemetria](app-insights-api-custom-events-metrics.md#defaults) tooensure che tutte le istanze di TelemetryClient sono impostate in modo coerente.
* [ASP.NET] La versione di hello in `BuildInfo.config`. il modulo web Hello selezionerà versione hello dal nodo BuildLabel hello. Includere questo file nel progetto e ricordare di proprietà di tooset Copia sempre hello in Esplora soluzioni.

    ```XML

    <?xml version="1.0" encoding="utf-8"?>
    <DeploymentEvent xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/DeploymentEvent/2013/06">
      <ProjectName>AppVersionExpt</ProjectName>
      <Build type="MSBuild">
        <MSBuild>
          <BuildLabel kind="label">1.0.0.2</BuildLabel>
        </MSBuild>
      </Build>
    </DeploymentEvent>

    ```
* [ASP.NET] Generare automaticamente BuildInfo.config in MSBuild. toodo, aggiungere alcune righe tooyour `.csproj` file:

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    Verrà generato un file denominato *yourProjectName*. Hello Buildinfo. processo di pubblicazione viene rinominato tooBuildInfo.config.

    etichetta di compilazione Hello contiene un segnaposto (autogen _) durante la compilazione con Visual Studio. Tuttavia, quando viene compilato con MSBuild, viene popolata con il numero di versione corretto hello.

    ad esempio la versione di hello tooallow numeri di versione di MSBuild toogenerate, `1.0.*` in AssemblyReference.cs

## <a name="version-and-release-tracking"></a>Verifica della versione
versione dell'applicazione hello tootrack, assicurarsi che `buildinfo.config` viene generato dal processo di Microsoft Build Engine. Nel file con estensione csproj, aggiungere:  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

Quando si dispone di informazioni di compilazione hello, modulo web di Application Insights hello aggiunge automaticamente **versione dell'applicazione** come elemento proprietà tooevery di telemetria. Che consente di toofilter dalla versione quando si eseguono [ricerche diagnostica](app-insights-diagnostic-search.md), o quando si [Esplora metriche](app-insights-metrics-explorer.md).

Si noti tuttavia che il numero di versione build hello viene generato solo dal hello Microsoft Build Engine, non dallo sviluppatore di hello compilati in Visual Studio.

### <a name="release-annotations"></a>Annotazioni sulle versioni
Se si utilizza Visual Studio Team Services, è possibile [ottenere un marcatore di annotazione](app-insights-annotations.md) aggiunti tooyour grafici quando si rilascia una nuova versione. Hello immagine seguente mostra come viene visualizzato l'indicatore.

![Screenshot di annotazione sulla versione di esempio in un grafico](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a>Passaggi successivi

* [Risorse condivise da più ruoli](app-insights-monitor-multi-role-apps.md)
* [Creare toodistinguish un inizializzatore di telemetria A | Varianti B](app-insights-api-filtering-sampling.md#add-properties)
