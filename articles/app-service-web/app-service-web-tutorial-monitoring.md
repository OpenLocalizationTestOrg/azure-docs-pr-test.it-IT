---
title: un'App Web aaaMonitor | Documenti Microsoft
description: Informazioni su come tooset di monitoraggio nell'App Web
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: c2f5e9842c732a804f1caee5d67e53dad24e190a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-app-service"></a>Monitorare il servizio app
In questa esercitazione illustra il monitoraggio dell'applicazione e l'utilizzo di problemi di toosolve hello piattaforma incorporata strumenti quando si verificano.

Ogni sezione di questo documento illustra una funzionalità specifica. Uso combinato hello funzionalità consentono di:
- Identificare un problema nell'applicazione.
- Determinare quando hello è causato dalla piattaforma hello o codice.
- Restringere causa hello hello problema nel codice.
- Debug e risoluzione problema hello.

## <a name="before-you-begin"></a>Prima di iniziare
- È necessario un toomonitor App Web e seguire hello descritti passaggi.
    - È possibile creare un'applicazione hello passaggi descritti in hello [creare un'applicazione ASP.NET in Azure con il Database SQL](app-service-web-tutorial-dotnet-sqldatabase.md) esercitazione.

- Se si desidera tootry out **il debug remoto** dell'applicazione, è necessario Visual Studio.
    - Se si dispone già di Visual Studio 2017, che installata, è possibile scaricare e utilizzare hello libero [2017 di Visual Studio Community Edition](https://www.visualstudio.com/downloads/).
    - Assicurarsi di abilitare **lo sviluppo di Azure** durante l'installazione di Visual Studio hello.

## <a name="metrics"></a>Passaggio 1: visualizzare le metriche
**Metriche** toounderstand utili sono:
- Integrità dell'applicazione
- Prestazioni dell'applicazione
- Utilizzo di risorse

Quando si analizzano i problemi di un'applicazione, esaminare le metriche è toostart un buon punto. Portale di Azure è toovisually un modo rapido controllare metriche di hello dell'app utilizzando **Monitor Azure**.

Le metriche forniscono una visualizzazione cronologica in numerose aggregazioni chiave per l'app. Per qualsiasi applicazione ospitata nel servizio app, è necessario monitorare hello App Web sia hello piano di servizio App.

> [!NOTE]
> Un piano di servizio App rappresenta raccolta hello di risorse fisiche utilizzate toohost app. Tutte le applicazioni assegnate tooan risorse hello condivisione piano di servizio App da essa consentendo toosave costo quando più applicazioni di hosting definite.
>
> I piani di servizio app definiscono:
> * Area: Europa settentrionale, Stati Uniti orientali, Asia sud-orientale e così via.
> * Dimensione dell'istanza: Small, Medium, Large e così via.
> * Numero di scala: una, due o tre istanze e così via.
> * SKU: Free, Shared, Basic, Standard, Premium e così via.

metriche tooreview per l'App Web, visita toohello **Panoramica** pannello App hello desiderato toomonitor. A questo punto, è possibile visualizzare un grafico per le metriche dell'app come un **riquadro Monitoraggio**. Fare clic su tooedit riquadro hello e configurare quali tooview metriche e hello toodisplay intervallo di tempo.

Dal pannello della risorsa predefinita hello fornisce una visualizzazione per le richieste dell'applicazione hello e gli errori per hello ultima ora.
![Monitorare un'app](media/app-service-web-tutorial-monitoring/app-service-monitor.png)

Come si può notare nell'esempio hello, disporre di un'applicazione che genera molti **errori Server HTTP**. numero elevato di errori Hello è prima indicazione hello dobbiamo tooinvestigate questa applicazione.

> [!TIP]
> Ulteriori informazioni sul monitoraggio di Azure con hello seguenti collegamenti:
> - [Introduzione al monitoraggio di Azure](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [Metriche di Azure](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [Metriche supportate con il monitoraggio di Azure](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [Dashboard di Azure](..\azure-portal\azure-portal-dashboards.md)

## <a name="alerts"></a> Passaggio 2: configurare gli avvisi
**Avvisi** può essere configurato tootrigger condizioni specifiche per l'app.

In [passaggio 1 - metriche vista](#metrics), abbiamo visto che un'applicazione hello ha un numero elevato di errori.

Consente di configurare un avviso tooautomatically ricevere notifiche quando si verificano errori. In questo caso, si desidera toosend avviso hello e di posta elettronica ogni volta che il numero di hello di errori HTTP 50 X supera una determinata soglia.

toocreate un avviso, passare troppo**monitoraggio** > **avvisi** e fare clic su **[+] Aggiungi avviso**.

![Avvisi](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

Fornire valori per la configurazione di avviso hello:
- **Risorse:** hello toomonitor sito con avviso hello.
- **Nome:** un nome per l'avviso, in questo caso: *Troppi HTTP 50X*.
- **Descrizione:** spiegazione in formato testo normale di cosa sta monitorando questo avviso.
- **Avviso per:** gli avvisi possono monitorare Metriche o Eventi, in questo esempio monitoreremo le metriche.
- **Metrica:** quali toomonitor metrica, in questo caso: *errori Server HTTP*.
- **Condizione:** quando tooalert, in questo caso selezionare hello *maggiore* opzione.
- **Soglia:** novità toolook valore, in questo caso: *400*.
- **Periodo:** gli avvisi di operare su valore medio di hello di una metrica. Per i periodi di tempo più ristretti, gli avvisi sensibili vengono sospesi. In questo caso, consideriamo *5 minuti*.
- **Invia messaggio di posta elettronica a proprietari e collaboratori:** in questo caso *Abilitato*.

Dopo aver creato hello avviso tramite posta elettronica viene inviato ogni volta che hello app supera la soglia configurata di hello. Gli avvisi attivi possono anche essere rivista in hello portale di Azure.

![Avvisi attivati](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> Altre informazioni sugli avvisi di Azure con hello seguenti collegamenti:
> - [Cosa sono gli avvisi in Microsoft Azure?](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [Eseguire operazioni sulle metriche](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [Creare avvisi delle metriche](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <a name="companion"></a> Passaggio 3: App Service Companion
**Complementare di servizio app** offre un modo pratico di toomonitor dell'app con un'esperienza nativa nel dispositivo mobile (iOS e Android).

Usare App Service Companion per:
- Rivedere le metriche dell'applicazione
- Rivedere ed eseguire azioni su avvisi e suggerimenti dell'applicazione
- Base per la risoluzione (Sfoglia, start, stop, riavvio hello app)
- Ottenere notifiche push per gli eventi critici.

![App Service Companion](media/app-service-web-tutorial-monitoring/app-service-companion.png)

[![App Service Companion in App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion in Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

È possibile installare complementare di servizio App hello [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) o [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

## <a name="diagnose"></a> Passaggio 4: diagnostica e risoluzione dei problemi
La **diagnostica e risoluzione dei problemi** consente di separare i problemi legati all'app da quelli legati alla piattaforma. Può inoltre indicare soluzioni correttive possibili tooget toohealthy di back-l'App Web.

![Diagnostica e risoluzione dei problemi](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

Continuare con i passaggi precedenti form di esempio hello, possiamo vedere che un'applicazione hello è stata problemi di disponibilità. Al contrario, la disponibilità di hello piattaforma non è stato spostato dal 100%.

Quando l'app hello in caso di problema e hello rimane piattaforma backup, è una chiara indicazione che si sta gestiscono i problemi di un'applicazione.

## <a name="logging"></a> Passaggio 5: registrazione
Ora che è stato limitato, problema di hello errori tooan dell'applicazione, è possibile esaminare in tooget di registri applicazioni e server hello ulteriori informazioni.

La registrazione consente toocollect entrambi **Application Diagnostics** e **diagnostica del Server Web** log per l'App Web.

### <a name="application-diagnostics"></a>Diagnostica applicazioni
Diagnostica delle applicazioni consente si toocapture le tracce prodotte da un'applicazione hello in fase di esecuzione.

Aggiunta di funzionalità di traccia tooyour applicazione migliora notevolmente il possibilità toodebug e problemi di punto di blocco.

In ASP.NET, è possibile registrare le tracce di applicazione utilizzando [classe Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) eventi toogenerate acquisite dall'infrastruttura di log hello. È inoltre possibile specificare la gravità hello di traccia hello per il filtro più semplice.

```csharp
public ActionResult Delete(Guid? id)
{
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id);
    if (id == null)
    {
        System.Diagnostics.Trace.TraceError("/Todos/Delete/ failed, ID is null");
        return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
    }
    Todo todo = db.Todoes.Find(id);
    if (todo == null)
    {
        System.Diagnostics.Trace.TraceWarning("/Todos/Delete/ failed, ID: " + id + " could not be found");
        return HttpNotFound();
    }
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id + "completed successfully");
    return View(todo);
}
```
registrazione applicazioni tooenable andare troppo**monitoraggio** > **i log di diagnostica** e abilitare la registrazione delle applicazioni utilizzando gli elementi Toggle hello.

![Monitorare un'app](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

Log applicazioni possono essere il sistema di file dell'App Web tooyour stored o distribuirli tooblob archiviazione. Per gli scenari di produzione, è consigliato toouse nell'archiviazione blob.

> [!IMPORTANT]
> L'abilitazione della registrazione ha effetto sulle prestazioni dell'applicazione e l'uso delle risorse. Per gli scenari di produzione è consigliabile usare i log degli errori. Abilitare una registrazione più dettagliata solo durante l'analisi dei problemi.

 ### <a name="web-server-diagnostics"></a>Diagnostica del server Web
I log del server Web vengono generati anche se l'app non è instrumentata. Il servizio app consente di raccogliere tre tipi diversi di log del server:

- **Registrazione del server Web**
    - Informazioni sulle transazioni HTTP tramite hello [formato di file registro esteso W3C](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).
    - È utile quando si determinano le metriche di generale del sito, ad esempio il numero di hello di richieste gestite o il numero di richieste provengono da un indirizzo IP specifico.
- **Registrazione degli errori dettagliata**
    - Informazioni dettagliate sugli errori relativi ai codici di stato HTTP che indicano un'operazione non riuscita (codice di stato 400 o superiore).
    - [Altre informazioni sulla registrazione degli errori dettagliata](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- **Traccia delle richieste non riuscite**
    - Informazioni dettagliate sulle richieste non riuscite, inclusa un'analisi dei componenti IIS hello utilizzato tooprocess hello richiesta e hello tempo impiegato in ogni componente.
    - Registri richieste non riuscite sono utili quando si tenta di tooisolate causa un errore HTTP specifico.
    - [Altre informazioni sulla traccia delle richieste non riuscite](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

registrazione del Server tooenable:
- andare troppo**monitoraggio** > **i log di diagnostica**.
- Abilitare tipi diversi di hello di diagnostica del Server Web utilizzando gli elementi Toggle hello.

![Monitorare un'app](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> L'abilitazione della registrazione ha effetto sulle prestazioni dell'applicazione e l'uso delle risorse. Per gli scenari di produzione è consigliabile usare i log degli errori. Abilitare una registrazione più dettagliata solo durante l'analisi dei problemi.

### <a name="accessing-logs"></a>Accesso ai log
I log memorizzati nell'archiviazione BLOB sono accessibili tramite Azure Storage Explorer. Registri archiviati nel file System dell'App Web hello sono accessibili tramite FTP in hello seguenti percorsi:

- **Log applicazioni** - `%HOME%/LogFiles/Application/`.
    - In questa cartella sono presenti uno o più file di testo contenenti le informazioni generate dalla registrazione dell'applicazione.
- **Traccia delle richieste non riuscite** - `%HOME%/LogFiles/W3SVC#########/`.
    - Questa cartella contiene un file XSL e uno o più file XML.
- **Registrazione degli errori dettagliata** - `%HOME%/LogFiles/DetailedErrors/`.
    - Questa cartella contiene uno o più file con estensione htm con informazioni dettagliate sugli errori HTTP generati dall'app.
- **Log del server Web** - `%HOME%/LogFiles/http/RawLogs`.
    - Questa cartella contiene uno o più file di testo formattati con formato del file registro esteso W3C hello.

## <a name="streaming"></a> Passaggio 6: streaming dei log
I log di streaming sono particolarmente utili quando il debug di un'applicazione, poiché consente di risparmiare tempo confrontato troppo[accesso ai registri hello](#Accessing-Logs) tramite FTP.

Il servizio app può eseguire lo streaming dei **Log applicazione** e dei **Log del server Web** generati.

> [!TIP]
> Prima di tentare di registri toostream, assicurarsi che è stata attivata la raccolta dei registri, come descritto in hello [registrazione](#logging) sezione.

log toostream, andare troppo**monitoraggio**> **flusso del Log**. Selezionare **Log applicazione** o **Log del server Web**, a seconda delle informazioni desiderate. Da qui, è anche possibile sospendere, riavviare e cancellare il buffer di hello.

![Log in streaming](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> I log vengono generati solo quando il traffico è hello App, è anche possibile aumentare il livello di dettaglio hello di registri tooget più eventi o informazioni.

## <a name="remote"></a> Passaggio 7 - Debug remoto
Dopo avere origine a cui punta pin hello dei problemi di applicazioni di hello, utilizzare **il debug remoto** toowalk tramite codice hello.

Consente di debug remoto si collega un tooyour debugger App Web in esecuzione nel cloud hello. È possibile impostare i punti di interruzione, modificare direttamente memoria, esaminare il codice e cambiare anche percorso di codice hello come se si trattasse di un'app in esecuzione in locale.

tooattach hello debugger tooyour app in esecuzione nel cloud hello:

- Utilizzando Visual Studio 2017, soluzione hello aperto per l'applicazione hello desiderato toodebug
- Impostare alcuni punti di interruzione esattamente come si farebbe per lo sviluppo locale.
- Aprire **Cloud Explorer** (CTRL+/, CTRL+X).
- Accedere con le credenziali di Azure.
- Trova hello app da toodebug
- Selezionare **collega Debugger** hello modulo **azioni** riquadro.

![Debug remoto](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

Visual Studio consente di configurare l'applicazione per il debug remoto e viene avviata una finestra del browser che consente di passare tooyour app. Sfogliare i punti di interruzione tootrigger app e avanzare nel codice hello.

> [!WARNING]
> L'esecuzione in modalità debug in produzione non è una scelta consigliata. Se l'applicazione di produzione non è scalare orizzontalmente toomultiple istanze del server, il debug di evitare hello del server web da richieste tooother risponde. Per risolvere i problemi di produzione, la risorsa migliore è troppo[configurare la registrazione](#logging) e [Application Insights](#insights).



## <a name="explorer"></a> Passaggio 8: esplora processi
Quando l'applicazione viene ampliato toomore più di un'istanza, **Esplora processi** consente di identificare i problemi specifici di istanza.

Usare **Esplora processi** per:

- Consente di enumerare tutti i processi di hello tra istanze diverse del piano di servizio App.
- Drill-down e visualizzare gli handle di hello e moduli associati a ogni processo.
- Il numero di CPU di visualizzazione, Working Set e Thread a hello elaborare toohelp livello è identificare i processi per tale tipo
- Trovare gli handle di file aperti e terminare l'istanza di un processo specifico.

Esplora processi è disponibile in **Monitoraggio** > **Esplora processi**.

![Esplora processi](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <a name="insights"></a> Passaggio 9: Application Insights
**Application Insights** offre funzionalità avanzate di profilatura e monitoraggio dell'app.

Usare Application Insights toodetect e diagnosticare le eccezioni e i problemi di prestazioni nell'App Web.

È possibile abilitare Application Insights per l'app Web in **Monitoraggio** > **Application Insights**

> [!NOTE]
> Application Insights potrebbe richiedere toostart tooinstall hello Application Insights sito estensione con la raccolta dei dati. L'installazione dell'estensione del sito hello comporta il riavvio dell'applicazione.

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

Application Insights è una funzionalità avanzata, impostare toolearn, più collegamenti hello incluso in hello [passaggi successivi](#next) sezione.

## <a name="next"></a> Passaggi successivi

 - [Informazioni su Azure Application Insights](..\application-insights\app-insights-overview.md)
 - [Monitoraggio delle prestazioni dell'applicazione web di Azure](..\application-insights\app-insights-azure-web-apps.md)
 - [Monitorare la disponibilità e la velocità di risposta dei siti Web](..\application-insights\app-insights-monitor-web-app-availability.md)
