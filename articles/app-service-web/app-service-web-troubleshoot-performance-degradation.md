---
title: prestazioni dell'applicazione web aaaSlow nel servizio App | Documenti Microsoft
description: Questo articolo fornisce informazioni utili per la risoluzione dei rallentamenti delle prestazioni delle app Web nel Servizio app di Azure.
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: prestazioni dell'applicazione Web, app lenta, rallentamento app
ms.assetid: b8783c10-3a4a-4dd6-af8c-856baafbdde5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: cephalin
ms.openlocfilehash: 3e56b99b48db0e7baae1fac797a7fcb9eff74c9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-slow-web-app-performance-issues-in-azure-app-service"></a>Risoluzione dei problemi di rallentamento delle prestazioni delle app Web nel Servizio app di Azure
Questo articolo fornisce informazioni utili per la risoluzione dei rallentamenti delle prestazioni delle app Web nel [Servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti in [hello MSDN di Azure e forum di Overflow dello Stack di hello](https://azure.microsoft.com/support/forums/). In alternativa, è anche possibile archiviare un evento imprevisto di supporto tecnico di Azure. Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/support/options/) e fare clic su **supporto**.

## <a name="symptom"></a>Sintomo
Quando si passa hello web app, hello pagine carico lenta e talvolta timeout.

## <a name="cause"></a>Causa
Spesso la causa dell'errore deriva da problemi a livello dell'applicazione, ad esempio:

* le richieste di rete impiegano troppo tempo
* il codice dell'applicazione o le query di database non sono efficienti
* utilizzo elevato di memoria/CPU da parte dell'applicazione
* applicazione di un arresto anomalo a causa di eccezioni tooan

## <a name="troubleshooting-steps"></a>Passaggi per la risoluzione dei problemi
La risoluzione dei problemi prevede tre attività distinte, in ordine sequenziale:

1. [Osservare e monitorare il comportamento dell'applicazione](#observe)
2. [Raccogliere i dati](#collect)
3. [Limitare i problemi di hello](#mitigate)

[app Web del servizio app](/services/app-service/web/) vengono presentate diverse opzioni per ogni passaggio.

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a>1. Osservare e monitorare il comportamento dell'applicazione
#### <a name="track-service-health"></a>Tenere traccia dell'integrità del servizio
Microsoft Azure pubblica un annuncio ogni volta che si verifica un'interruzione del servizio o una riduzione delle prestazioni. È possibile tenere traccia dello stato di hello del servizio hello in hello [portale di Azure](https://portal.azure.com/). Per altre informazioni, vedere [Tenere traccia dell’integrità del servizio](../monitoring-and-diagnostics/insights-service-health.md).

#### <a name="monitor-your-web-app"></a>Monitorare l'app Web
Questa opzione consente toofind out dell'applicazione in caso di eventuali problemi. Nel pannello dell'app web, fare clic su hello **richieste ed errori** riquadro. Hello **metrica** pannello Mostra tutte le metriche di hello è possibile aggiungere.

Sono riportate alcune delle metriche hello che potrebbe essere toomonitor per l'app web

* Working set della memoria medio
* Tempo di risposta medio
* Tempo CPU
* Working set della memoria
* Requests

![monitoraggio delle prestazioni dell'app Web](./media/app-service-web-troubleshoot-performance-degradation/1-monitor-metrics.png)

Per altre informazioni, vedere:

* [Eseguire il monitoraggio delle app Web nel servizio app di Azure](web-sites-monitor.md)
* [Ricevere notifiche di avviso](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

#### <a name="monitor-web-endpoint-status"></a>Monitorare lo stato degli endpoint
Se si esegue l'app web in hello **Standard** livello di prezzo, le applicazioni Web consente di monitorare due endpoint da tre posizioni geografiche.

Il monitoraggio degli endpoint configura i test Web da posizioni distribuite a livello geografico che testano il tempo di risposta e di attività degli URL Web. test di Hello esegue un'operazione HTTP GET nel tempo di risposta hello toodetermine URL web hello e tempi di attività da ogni posizione. Ogni posizione configurata esegue un testo ogni cinque minuti.

Il tempo di attività viene monitorato mediante codici di risposta HTTP e il tempo di risposta è misurato in millisecondi. Un test di monitoraggio non riesce se hello codice di risposta HTTP è maggiore o uguale too400 o se la risposta hello richiede più di 30 secondi. Un endpoint è considerato disponibile se il test di monitoraggio hanno esito positivo da tutte hello specificati percorsi.

tooset, configurarlo, vedere [monitorare le App in Azure App Service](web-sites-monitor.md).

Per altre informazioni sul monitoraggio degli endpoint, vedere anche il video che illustra come [mantenere attivi i siti Web di Azure e monitorare gli endpoint con Stefan Schackow](https://channel9.msdn.com/Shows/Azure-Friday/Keeping-Azure-Web-Sites-up-plus-Endpoint-Monitoring-with-Stefan-Schackow) .

#### <a name="application-performance-monitoring-using-extensions"></a>Monitoraggio delle prestazioni dell'applicazione usando le estensioni
È anche possibile monitorare le prestazioni dell'applicazione usando le *estensioni del sito*.

Ogni applicazione di servizio App web fornisce un punto finale di gestione estensibile che consente di toouse un potente set di strumenti distribuito come estensioni del sito. Le estensioni includono: 

- Editor di codice sorgente come [Visual Studio Team Services](https://www.visualstudio.com/products/what-is-visual-studio-online-vs.aspx). 
- Gli strumenti di gestione per le risorse collegate ad esempio un database MySQL connesso tooa web app.

[Azure Application Insights](/services/application-insights/) e [New Relic](/marketplace/partners/newrelic/newrelic/) sono due hello di monitoraggio delle prestazioni per le estensioni del sito disponibili. toouse New Relic, si installa un agente in fase di esecuzione. toouse Azure Application Insights, si ricompila il codice con un SDK ed è inoltre possibile installare un'estensione che consente di accedere ai dati tooadditional. Hello SDK consente di scrivere codice toomonitor hello utilizzo e prestazioni dell'app in modo più dettagliato.

toouse Application Insights, vedere [monitorare le prestazioni in applicazioni web](../application-insights/app-insights-web-monitor-performance.md).

vedere toouse New Relic, [nuova gestione delle prestazioni delle applicazioni Relic in Azure](../store-new-relic-cloud-services-dotnet-application-performance-management.md).

<a name="collect" />

### <a name="2-collect-data"></a>2. Raccogliere i dati
ambiente di App Web Hello offre funzionalità di diagnostica per la registrazione delle informazioni dal server web hello e un'applicazione web hello. informazioni di Hello viene separate in diagnostica del server web e application diagnostics.

#### <a name="enable-web-server-diagnostics"></a>Abilitare la diagnostica del server Web
È possibile abilitare o disabilitare i seguenti tipi di registri hello:

* **Registrazione degli errori dettagliata**: consente di registrare informazioni dettagliate sugli errori relativi ai codici di stato HTTP che indicano un'operazione non riuscita (codice di stato 400 o superiore), Può contenere informazioni utili per determinare perché i server di hello ha restituito il codice di errore hello.
* **Non è stato possibile traccia richiesta** -informazioni dettagliate sulle richieste non riuscite, tra cui una traccia di hello IIS componenti utilizzati tooprocess hello richiesta e tempo hello in ogni componente. Può essere utile se si siano tentando di prestazioni dell'applicazione web tooimprove o isolare la causa un errore HTTP specifico.
* **Registrazione del Server Web** -informazioni sulle transazioni HTTP formato di file registro esteso W3C hello. Ciò è utile durante la determinazione delle metriche di app web globale, ad esempio il numero di hello di richieste gestite o il numero di richieste provengono da un indirizzo IP specifico.

#### <a name="enable-application-diagnostics"></a>Abilitare la diagnostica delle applicazioni
Esistono diverse opzioni toocollect applicazione dati sulle prestazioni da app Web, profilare l'applicazione in tempo reale da Visual Studio o modificare il toolog codice applicazione ulteriori informazioni e le tracce. È possibile scegliere le opzioni di hello basate sul livello di accesso toohello applicazione e osservate da hello gli strumenti di monitoraggio.

##### <a name="use-application-insights-profiler"></a>Usare Application Insights Profiler
È possibile abilitare toostart Application Insights Profiler hello acquisire tracce di prestazioni dettagliati. È possibile accedere tracce acquisite backup toofive giorni quando è necessario tooinvestigate problemi si sono verificati nelle ultime hello. È possibile scegliere questa opzione, purché si disponga di risorsa di Application Insights dell'app web toohello di accesso nel portale di Azure.

Application Insights Profiler fornisce statistiche sui tempi di risposta per ogni chiamata web e le tracce che indica la riga del codice ha causato una risposta lenta hello. In alcuni casi hello app del servizio App è lento perché determinato codice non scritto in un efficiente modo. È possibile ad esempio che siano presenti un codice sequenziale che può essere eseguito in parallelo e conflitti di blocco di database non previsti. Rimozione di questi colli di bottiglia nel codice hello aumenta le prestazioni dell'applicazione hello, ma sono toodetect disco senza configurare il log e le tracce elaborate. le tracce di Hello raccolte dal Profiler di Application Insights consente di identificare hello le righe di codice che rallenta l'applicazione hello e risolvere questo problema per le applicazioni di servizio App.

 Per altre informazioni, vedere [Profilatura delle app Web di Azure attive con Application Insights](../application-insights/app-insights-profiler.md).

##### <a name="use-remote-profiling"></a>Usare la profilatura remota
Nel servizio app di Azure è possibile profilare in modalità remota app Web, app per le API e processi Web. Scegliere questa opzione se si dispone di accesso toohello web app risorsa e si sa come tooreproduce hello problema o se si conosce esattamente hello problema di prestazioni hello intervallo di tempo si verifica.

Profilatura remota è utile se l'utilizzo della CPU del processo di hello hello è elevato e il processo è in esecuzione più lenta del previsto o latenza hello di richieste HTTP sono superiori al normale, in modalità remota è possibile profilare il processo e ottenere hello CPU campionamento chiamata stack tooanalyze attività processo Hello e frequente percorsi del codice.

Per altre informazioni, vedere [Remote Profiling support in Azure App Service](https://azure.microsoft.com/blog/remote-profiling-support-in-azure-app-service) (Supporto della profilatura remota in Servizio app di Azure).

##### <a name="set-up-diagnostic-traces-manually"></a>Configurare manualmente le tracce di diagnostica
Se si dispone di codice sorgente dell'applicazione web accesso toohello, Application diagnostics consente informazioni toocapture prodotte da un'applicazione web. Applicazioni ASP.NET possono usare hello `System.Diagnostics.Trace` classe toolog informazioni toohello application diagnostics log. Tuttavia, è necessario toochange codice hello e ridistribuire l'applicazione. Questo metodo è consigliato se l'app è in esecuzione in un ambiente di testing.

Per istruzioni dettagliate su come tooconfigure l'applicazione per la registrazione, vedere [abilitare la registrazione diagnostica per le app web in Azure App Service](web-sites-enable-diagnostic-log.md).

#### <a name="use-hello-azure-app-service-support-portal"></a>Utilizzare il portale di supporto del hello Azure App Service
App Web fornisce hello possibilità tootroubleshoot problemi correlati tooyour web app esaminando HTTP log, i registri eventi, i dump del processo e altro. È possibile accedere a tutte queste informazioni tramite il portale di supporto disponibile all'indirizzo **http://&lt;nome app>.scm.azurewebsites.net/Support**

portale di supporto di Azure App Service Hello fornisce con tre schede separate toosupport hello tre passaggi di uno scenario di risoluzione dei problemi più comune:

1. Osservare il comportamento corrente
2. Analizzare la raccolta di informazioni di diagnostica ed eseguendo hello analizzatori incorporati
3. Attenuare il problema

Se il problema di hello è in corso al momento, fare clic su **Analizza** > **diagnostica** > **diagnosticare ora** toocreate una sessione di diagnostica, che consente di raccogliere log HTTP, i registri del Visualizzatore eventi, dump della memoria, i log degli errori PHP e report processo PHP.

Una volta raccolti i dati di hello, il portale di supporto hello viene eseguita un'analisi sui dati hello e fornisce un report HTML.

Nel caso in cui si desiderano i dati di hello toodownload, per impostazione predefinita, potrebbe essere archiviato nella cartella D:\home\data\DaaS hello.

Per ulteriori informazioni sul portale di supporto di hello Azure App Service, vedere [tooSupport nuovi aggiornamenti estensione del sito per siti Web di Azure](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).

#### <a name="use-hello-kudu-debug-console"></a>Utilizzare hello Kudu Console di Debug
Il servizio App Web include una console di debug che è possibile usare per il debug, l'esplorazione e il caricamento di file, nonché endpoint JSON per ottenere informazioni sull'ambiente in uso. Questa console è chiamata hello *Kudu Console* o hello *Dashboard SCM* per l'app web.

È possibile accedere a questo dashboard per passare toohello collegamento **https://&lt;nome dell'app >.scm.azurewebsites.net/**.

Sono riportate alcune delle operazioni hello Kudu offre:

* impostazioni di ambiente per l'applicazione
* log in streaming
* dump di diagnostica
* console di debug in cui è possibile eseguire cmdlet di PowerShell e comandi DOS di base.

Un'altra caratteristica utile di Kudu è che, nel caso in cui l'applicazione è la generazione di eccezioni first-chance, è possibile utilizzare Kudu e dump della memoria di hello SysInternals strumento Procdump toocreate. Le immagini della memoria sono snapshot dei processo hello e spesso consentono di risolvere i problemi più complessi con l'app web.

Per altre informazioni sulle funzionalità disponibili in Kudu, vedere il post di blog relativo agli [strumenti di Azure Websites Team Services che è opportuno conoscere](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a>3. Limitare i problemi di hello
#### <a name="scale-hello-web-app"></a>Scala hello web app
In Azure App Service, per migliorare le prestazioni e velocità effettiva, è possibile modificare la scala hello in corrispondenza del quale si esegue l'applicazione. La scalabilità verticale un'app web prevede due azioni correlate: modifica il maggiore livello di prezzo e la configurazione di determinate impostazioni dopo avere impostato toohello maggiore livello di prezzo tooa di piano di servizio App.

Per altre informazioni sul ridimensionamento, vedere [Ridimensionare un'app Web nel servizio app di Azure](web-sites-scale.md).

Inoltre, è possibile scegliere toorun l'applicazione in più di un'istanza. La scalabilità orizzontale non consente solo di ottenere una maggiore capacità di elaborazione, ma anche di usufruire di un certo livello di tolleranza di errore. Se si arresta il processo di hello in un'istanza, hello altre istanze continuano tooserve richieste.

È possibile impostare hello scalabilità toobe manuale o automatico.

#### <a name="use-autoheal"></a>Usare la funzionalità AutoHeal
AutoHeal Ricicla il processo di lavoro hello per l'app in base alle impostazioni selezionate (ad esempio, è necessario tooexecute una richiesta di modifiche alla configurazione, le richieste, basata sulla memoria limiti o il tempo di hello). La maggior parte dei casi hello Ricicla i processi di hello sono toorecover modo più veloce di hello da un problema. Anche se è sempre possibile riavviare un'app web hello da direttamente in hello portale di Azure, AutoHeal si adatta automaticamente per l'utente. È sufficiente toodo aggiungere alcuni trigger in Web. config radice hello per le app web. Queste impostazioni funzionerà in hello stesso modo, anche se l'applicazione non è un'app .net.

Per altre informazioni, vedere il post di blog relativo alla [correzione automatica di Siti Web di Azure](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).

#### <a name="restart-hello-web-app"></a>Riavviare l'app web hello
Il riavvio è spesso toorecover modo più semplice di hello da problemi occasionali. In hello [portale di Azure](https://portal.azure.com/), nel pannello dell'app web, si dispone di hello opzioni toostop o riavviare l'app.

 ![riavviare i problemi di prestazioni toosolve app web](./media/app-service-web-troubleshoot-performance-degradation/2-restart.png)

È anche possibile gestire l'app Web usando Azure PowerShell. Per altre informazioni, vedere [Uso di Azure PowerShell con Gestione risorse di Azure](../powershell-azure-resource-manager.md).
