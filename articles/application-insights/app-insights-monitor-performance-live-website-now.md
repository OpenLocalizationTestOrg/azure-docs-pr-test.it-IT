---
title: aaaMonitor un live ASP.NET web app con Azure Application Insights | Documenti Microsoft
description: "Monitorare le prestazioni di un sito Web senza ripetere la distribuzione. Questa funzionalità può essere usata con app Web ASP.NET ospitate in locale, in macchine virtuali o in Azure."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 0d53f0a59974f40767fae681bafc4f358d1283a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a>Instrumentare app Web in fase di esecuzione con Application Insights


È possibile instrumentare un'applicazione web in tempo reale con Azure Application Insights, senza dovere toomodify o ridistribuire il codice. Se le applicazioni sono ospitate da un server IIS locale, installare Status Monitor. Se stai App web di Azure o eseguire in una macchina virtuale di Azure, è possibile attivare il monitoraggio di Application Insights hello Azure nel Pannello di controllo. Sono disponibili anche articoli separati sulla strumentazione di [app Web J2EE live](app-insights-java-live.md) e [Servizi cloud di Azure](app-insights-cloudservices.md). È necessaria una sottoscrizione di [Microsoft Azure](http://azure.com) .

![grafici di esempio](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

È possibile scegliere di tre route tooapply Application Insights tooyour applicazioni web .NET:

* **Fase di compilazione:** [hello Aggiungi Application Insights SDK] [ greenbrown] tooyour codice dell'applicazione web.
* **Fase di esecuzione:** instrumentare l'app web nel server di hello, come descritto di seguito, senza dover ricompilare e ridistribuire codice hello.
* **Both:** compilare hello SDK nel codice dell'app web e si applicano anche le estensioni di hello in fase di esecuzione. Ottenere hello migliori di entrambe le opzioni.

Ecco un riepilogo di ciò che offrono i singoli modi:

|  | Fase di compilazione | Fase di esecuzione |
| --- | --- | --- |
| Richieste ed eccezioni |Sì |Sì |
| [Eccezioni più dettagliate](app-insights-asp-net-exceptions.md) | |Sì |
| [Diagnostica delle dipendenze](app-insights-asp-net-dependencies.md) |In .NET 4.6 e versioni successive, ma meno dettagli |Sì, dettagli completi: codici risultato, testo del comando SQL, verbo HTTP|
| [Contatori delle prestazioni di sistema](app-insights-performance-counters.md) |Sì |Sì |
| [API per telemetria personalizzata][api] |Sì |No |
| [Integrazione log di traccia](app-insights-asp-net-trace-logs.md) |Sì |No |
| [Visualizzazione pagina e dati utente](app-insights-javascript.md) |Sì |No |
| È necessario codice toorebuild |Sì | No |


## <a name="monitor-a-live-azure-web-app"></a>Monitorare un'app Web live di Azure

Se l'applicazione è in esecuzione come servizio web di Azure, modalità tooswitch sul monitoraggio:

* Selezionare Application Insights nel Pannello di controllo dell'applicazione hello in Azure.

    ![Configurare Application Insights per un'app Web di Azure](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* Quando verrà visualizzata la pagina di riepilogo di hello Application Insights, fare clic sul collegamento hello in hello inferiore tooopen hello completa risorsa di Application Insights.

    ![Fare clic sulle tooApplication Insights](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

[Monitoraggio di app cloud e VM](app-insights-azure.md).

### <a name="enable-client-side-monitoring-in-azure"></a>Abilitare il monitoraggio lato client in Azure

Se è stato abilitato Application Insights in Azure, è possibile aggiungere la visualizzazione delle pagine e la telemetria utente.

1. Selezionare Impostazioni > Impostazioni applicazione
2.  In Impostazioni app aggiungere una nuova coppia chiave-valore: 
   
    Chiave: `APPINSIGHTS_JAVASCRIPT_ENABLED` 
    
    Valore: `true`
3. **Salvare** hello impostazioni e **riavviare** l'app.

Hello Application Insights JavaScript SDK ora viene inserito in ogni pagina web.

## <a name="monitor-a-live-iis-web-app"></a>Monitorare un'app Web live di IIS

Se l'app è ospitata in un server IIS, abilitare Application Insights usando Status Monitor.

1. Nel server Web IIS accedere con le credenziali di amministratore.
2. Se Application Insights Status Monitor non è già installato, scaricare ed eseguire hello [installer Status Monitor](http://go.microsoft.com/fwlink/?LinkId=506648) (o eseguire [installazione guidata piattaforma Web](https://www.microsoft.com/web/downloads/platform.aspx) e cercare in essa contenuti lo stato di Application Insights Monitoraggio).
3. In Monitoraggio di stato, selezionare un'applicazione web hello installato o un sito Web che si desidera toomonitor. Accedere con le credenziali di Azure.

    Configurare hello risorsa in cui si desidera risultati hello toosee portale Application Insights hello. (In genere, è migliore toocreate una nuova risorsa. Selezionare una risorsa esistente se sono già disponibili [test Web][availability] o il [monitoraggio del client][client] per questa app. 

    ![Scegliere un'applicazione e una risorsa.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. Riavviare IIS.

    ![Scegliere Riavvia nella parte superiore di hello della finestra di dialogo hello.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    Il servizio Web viene interrotto per un breve periodo di tempo.

## <a name="customize-monitoring-options"></a>Personalizzare le opzioni di monitoraggio

L'abilitazione di Application Insights aggiunge DLL e Applicationinsights tooyour web app. È possibile [modificare i file con estensione config hello](app-insights-configuration-with-applicationinsights-config.md) toochange alcune delle opzioni di hello.

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a>Quando si ripubblica l'app, riabilitare Application Insights

Prima di pubblicare nuovamente l'app, prendere in considerazione [aggiungendo codice toohello Application Insights in Visual Studio][greenbrown]. Si otterrà telemetria più dettagliata e dati di telemetria personalizzati hello possibilità toowrite.

Se si desidera toore-pubblicare senza aggiungere codice toohello Application Insights, tenere presente che il processo di distribuzione hello può eliminare le DLL hello e Applicationinsights da hello pubblicazione sito web. Di conseguenza:

1. Se sono state apportate modifiche al file ApplicationInsights.config, copiarlo prima di ripubblicare l'app.
2. Pubblicare di nuovo l'app.
3. Abilitare di nuovo il monitoraggio di Application Insights. (Utilizzare il metodo appropriato di hello: pannello di controllo di hello Azure web app o hello Status Monitor in un host IIS.)
4. Ripristinare le modifiche apportate al file con estensione config hello.


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a>Risoluzione dei problemi della configurazione del runtime di Application Insights

### <a name="cant-connect-no-telemetry"></a>Nessuna connessione? Nessun dato di telemetria?

* Aprire [hello porte in uscita necessarie](app-insights-ip-addresses.md#outgoing-ports) in toowork di monitoraggio stato tooallow firewall del server.

* Aprire Status Monitor e selezionare la propria applicazione nel pannello a sinistra. Verificare se sono presenti eventuali messaggi di diagnostica per questa applicazione nella sezione "Configurazione notifiche" hello:

  ![Aprire una richiesta di hello prestazioni pannello toosee, tempo di risposta, dipendenze e altri dati](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* Nel server di hello, se viene visualizzato un messaggio relativo ad autorizzazioni"insufficienti", provare a seguente hello:
  * In Gestione IIS, selezionare il pool di applicazioni, aprire **impostazioni avanzate**e in **modello di processo** nota identità hello.
  * Nel Pannello di controllo di gestione Computer, aggiungere questo gruppo Performance Monitor Users toohello di identità.
* Se nel server è installato MMA/SCOM (System Center Operations Manager), alcune versioni potrebbero entrare in conflitto. Disinstallare SCOM e monitoraggio dello stato e reinstallare la versione più recente di hello.
* Vedere [Risoluzione dei problemi][qna].

## <a name="system-requirements"></a>Requisiti di sistema
Supporto del sistema operativo per Application Insights Status Monitor sul server

* Windows Server 2008
* Windows Server 2008 R2
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

con SP più recente e .NET Framework 4.5

Sul lato client hello: Windows 7, 8, 8.1 e 10, con .NET Framework 4.5

Il supporto IIS è: IIS 7, 7.5, 8, 8.5 (IIS è obbligatorio)

## <a name="automation-with-powershell"></a>Automazione con PowerShell
È possibile usare PowerShell nel server IIS per avviare e arrestare il monitoraggio.

È innanzitutto necessario importare il modulo di Application Insights hello:

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

Individuare le applicazioni sottoposte a monitoraggio:

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* `-Name`Nome hello (facoltativo) di un'app web.
* Consente di visualizzare hello lo stato di monitoraggio di Application Insights per ogni app web (o hello denominato app) nel server IIS.
* Restituisce `ApplicationInsightsApplication` per ogni app.

  * `SdkState==EnabledAfterDeployment`: L'app viene monitorato ed è stato instrumentato in fase di esecuzione per lo strumento di monitoraggio dello stato di hello o per `Start-ApplicationInsightsMonitoring`.
  * `SdkState==Disabled`: hello app non è instrumentato per Application Insights. È non stato mai instrumentato o monitoraggio in fase di esecuzione è stato disabilitato con lo strumento di monitoraggio dello stato di hello o `Stop-ApplicationInsightsMonitoring`.
  * `SdkState==EnabledByCodeInstrumentation`: è stato instrumentato app hello mediante l'aggiunta di codice sorgente di hello SDK toohello. Il relativo SDK non può essere aggiornato o arrestato.
  * `SdkVersion`Mostra una versione di hello in uso per il monitoraggio di questa app.
  * `LatestAvailableSdkVersion`Mostra hello versione attualmente disponibile nella raccolta NuGet hello. versione del toothis app hello tooupgrade, utilizzare `Update-ApplicationInsightsMonitoring`.

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* `-Name`nome Hello dell'applicazione hello in IIS
* `-InstrumentationKey`Hello ikey di hello risorsa di Application Insights in cui si desidera toobe risultati hello visualizzato.
* Questo cmdlet influisce solo sulle app che non sono già instrumentate, ovvero SdkState==NotInstrumented.

    Hello non influisce invece un'applicazione che è già stata instrumentata. Non è rilevante se è stato instrumentato app hello in fase di compilazione aggiungendo hello SDK toohello codice, né in fase di esecuzione da una precedente, utilizzare questo cmdlet.

    app hello tooinstrument di Hello SDK versione utilizzata è la versione di hello ultimo scaricata toothis server.

    versione più recente di hello toodownload, utilizzare ApplicationInsightsVersion di aggiornamento.
* Se l'esito è positivo, restituisce `ApplicationInsightsApplication` . In caso contrario, viene registrato un toostderr di traccia.

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* `-Name`nome Hello di un'applicazione in IIS
* `-All`: arresta il monitoraggio di tutte le app nel server IIS per cui `SdkState==EnabledAfterDeployment`
* Arresta il monitoraggio hello le app specificate e rimuove strumentazione. Funziona solo per le applicazioni che sono stata modificate in fase di esecuzione usando hello dello strumento di monitoraggio dello stato o ApplicationInsightsApplication di inizio. (`SdkState==EnabledAfterDeployment`)
* Restituisce ApplicationInsightsApplication.

`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]

* `-Name`: nome hello di un'app web in IIS.
* `-InstrumentationKey` (facoltativo): Utilizzo di che dati di telemetria toochange hello risorsa toowhich hello dell'app viene inviato.
* Questo cmdlet:
  * Hello aggiornamenti denominato hello SDK versione toohello app scaricate più di recente toothis macchina. Funziona solo se `SdkState==EnabledAfterDeployment`.
  * Se si specifica una chiave di strumentazione, hello denominato app viene riconfigurato toosend telemetria toohello risorsa con tale chiave. Funziona se `SdkState != Disabled`.

`Update-ApplicationInsightsVersion`

* Scarica server toohello Application Insights SDK più recente di hello.

## <a name="questions"></a>Domande su Status Monitor

### <a name="what-is-status-monitor"></a>Che cos'è Status Monitor?

Un'applicazione desktop che viene installata nel server Web IIS e consente di instrumentare e configurare le app Web. 

### <a name="when-do-i-use-status-monitor"></a>Quando si usa Status Monitor?

* tooinstrument qualsiasi web app è in esecuzione sul server IIS, anche se è già in esecuzione.
* tooenable telemetria aggiuntive per le applicazioni web che sono stati [compilati con Application Insights SDK hello](app-insights-asp-net.md) in fase di compilazione. 

### <a name="can-i-close-it-after-it-runs"></a>È possibile chiudere Status Monitor dopo l'esecuzione?

Sì. Dopo che è instrumentato siti Web di hello che si seleziona, è possibile chiuderlo.

Status Monitor non raccoglie i dati di telemetria, Sufficiente Configura App web hello e imposta alcune autorizzazioni.

### <a name="what-does-status-monitor-do"></a>Che cosa fa Status Monitor?

Quando si seleziona un'app web per monitoraggio stato tooinstrument:

* Scarica e inserisce gli assembly di Application Insights hello e file. config nella cartella dei file binari dell'applicazione web hello.
* Modifica `web.config` modulo di rilevamento tooadd hello Application Insights HTTP.
* Abilita analisi toocollect chiamate a dipendenze di CLR.

### <a name="do-i-need-toorun-status-monitor-whenever-i-update-hello-app"></a>È necessario toorun monitoraggio stato quando si aggiorna l'applicazione hello?

Se si esegue la ridistribuzione in modo incrementale, non è necessario. 

Se si seleziona l'opzione 'eliminare i file esistenti' hello in hello processo di pubblicazione, è necessario eseguire toore Status Monitor tooconfigure Application Insights.

### <a name="what-telemetry-is-collected"></a>Quali dati di telemetria vengono raccolti?

Per le applicazioni che vengono instrumentate solo in fase di esecuzione tramite Status Monitor:

* Richieste HTTP
* Chiama toodependencies
* Eccezioni
* Contatori delle prestazioni

Per le applicazioni già instrumentate in fase di compilazione:

 * Contatori dei processi
 * Chiamate alle dipendenze (.NET 4.5) e valori restituiti nelle chiamate alle dipendenze (.NET 4.6)
 * Valori di analisi dello stack delle eccezioni

[Altre informazioni](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next"></a>Passaggi successivi

Visualizzare i dati di telemetria:

* [Esplorare le metriche](app-insights-metrics-explorer.md) toomonitor delle prestazioni e utilizzo
* [Ricerca di eventi e log] [ diagnostic] toodiagnose problemi
* Per informazioni sulle query più avanzate, vedere [Analytics](app-insights-analytics.md)
* [Creare i dashboard](app-insights-dashboards.md)

Aggiungere altri dati di telemetria:

* [Creare test web] [ availability] toomake che il sito rimane in tempo reale.
* [Aggiungi telemetria di client web] [ usage] toosee eccezioni dal codice della pagina web e si inserisce toolet tenere traccia delle chiamate.
* [Aggiungere il codice di Application Insights SDK tooyour] [ greenbrown] in modo che sia possibile inserire una traccia e registrare le chiamate

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
