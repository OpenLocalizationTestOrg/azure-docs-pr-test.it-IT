---
title: aaaTroubleshooting alcun dato - Application Insights per .NET
description: "I dati non vengono visualizzati in Azure Application Insights Risposte ai problemi più comuni."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: e231569f-1b38-48f8-a744-6329f41d91d3
ms.service: application-insights
ms.workload: mobile
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 261c25c89884c46e41bbc305474ac854360221ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-no-data---application-insights-for-net"></a>Risoluzione dei problemi relativi a dati non disponibili in Application Insights per .NET
## <a name="some-of-my-telemetry-is-missing"></a>Alcuni dati di telemetria sono mancanti
*In Application Insights, vedere solo una frazione di eventi di hello che vengono generati dall'applicazione.*

* Se si verifica in modo coerente hello stesso frazione, è probabilmente dovuto tooadaptive [campionamento](app-insights-sampling.md). tooconfirm, aprire ricerca (dal pannello della panoramica hello) ed esaminare un'istanza di una richiesta o un altro evento. Nella parte inferiore di hello della sezione di proprietà hello fare clic su "…" informazioni dettagliate sulla proprietà completo tooget. Se il Conteggio richieste è inferiore a 1, il campionamento è in esecuzione. 
* In caso contrario, è possibile che sia stato raggiunto il [limite di velocità dati](app-insights-pricing.md#limits-summary) per il piano tariffario. Questi limiti vengono applicati per minuto.

## <a name="no-data-from-my-server"></a>Non sono disponibili dati dal server
*L'app è stata installata nel server Web e ora non vengono visualizzati i dati di telemetria. Nel computer di sviluppo funzionava correttamente.*

* Probabilmente è un problema del firewall. [Impostare le eccezioni del firewall per i dati di Application Insights toosend](app-insights-ip-addresses.md).

*Si [installato monitoraggio stato](app-insights-monitor-performance-live-website-now.md) in my app di esistenti toomonitor di server web. ma non è presente alcun risultato.*

* Vedere [Risoluzione dei problemi relativi a Status Monitor](app-insights-monitor-performance-live-website-now.md#troubleshooting-runtime-configuration-of-application-insights). 

## <a name="q01"></a>Nessuna opzione "Aggiungi Application Insights" in Visual Studio
*Quando si fa clic con il pulsante destro del mouse su un progetto esistente in Esplora soluzioni, non è presente alcuna opzione di Application Insights.*

* Non tutti i tipi di progetto .NET sono supportati dagli strumenti di hello. I progetti Web e WCF sono supportati. Per altri tipi di progetto, ad esempio applicazioni desktop o servizio, è comunque possibile [aggiungere manualmente un progetto di Application Insights SDK tooyour](app-insights-windows-desktop.md).
* Assicurarsi di disporre di [Visual Studio 2013 Update 3 o versioni successive](http://go.microsoft.com/fwlink/?LinkId=397827). Si tratta di pre-installata con strumenti per sviluppatori Analitica, che forniscono hello Application Insights SDK.
* Selezionare **Strumenti**, **Estensioni e aggiornamenti** e verificare l'installazione e l'abilitazione di **Developer Analytics Tools**. In questo caso, fare clic su **aggiornamenti** toosee se è disponibile un aggiornamento.
* Aprire una finestra di dialogo Nuovo progetto hello e scegliere l'applicazione Web ASP.NET. Se viene visualizzato hello opzione Application Insights non esiste, quindi vengono installati gli strumenti di hello. In caso contrario, provare a disinstallare e quindi nuovamente l'installazione di strumenti di Application Insights hello.

## <a name="q02"></a>Non è stato possibile aggiungere Application Insights
*Quando si tenta di progetto esistente tooan di Application Insights tooadd, viene visualizzato un messaggio di errore.*

Cause possibili:

* Comunicazione con il portale di Application Insights hello non è riuscita. o
* si è verificato un problema con l'account Azure;
* È sufficiente [sottoscrizione toohello accesso in lettura o gruppo in cui si sta tentando di nuova risorsa di hello toocreate](app-insights-resources-roles-access-control.md).

Correzione:

* Controllare fornite credenziali di accesso per il diritto di hello account Azure. 
* Nel browser, verificare di disporre di accesso toohello [portale di Azure](https://portal.azure.com). Aprire le impostazioni e vedere se sono presenti restrizioni.
* [Progetto esistente di Aggiungi Application Insights tooyour](app-insights-asp-net.md): In Esplora soluzioni, fare clic con il pulsante destro del progetto e scegliere "Aggiungi Application Insights".
* Se ancora non funziona, attenersi alla hello [procedura manuale](app-insights-windows-services.md) tooadd una risorsa nel portale di hello e quindi aggiungere hello SDK tooyour progetto. 

## <a name="emptykey"></a>Viene visualizzato l'errore: "La chiave di strumentazione non può essere vuota"
Sembra che si sia verificato un problema durante l'installazione di Application Insights o forse di un adattatore di registrazione.

Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni e scegliere **Application Insights > Configura Application Insights**. Si otterrà una finestra di dialogo Invita toosign in tooAzure e creare una risorsa di Application Insights, o riutilizzare uno esistente.

## <a name="NuGetBuild"></a> Un messaggio informa che i pacchetti NuGet sono mancanti nel server di compilazione
*Tutto ciò che compila OK quando sto debug nel computer di sviluppo, ma viene visualizzato un errore di NuGet nel server di compilazione hello.*

Vedere [NuGet Package Restore](http://docs.nuget.org/Consume/Package-Restore) (Ripristino dei pacchetti NuGet) e [Automatic Package Restore](http://docs.nuget.org/Consume/package-restore/migrating-to-automatic-package-restore) (Ripristino automatico dei pacchetti).

## <a name="missing-menu-command-tooopen-application-insights-from-visual-studio"></a>Mancante menu comando tooopen Application Insights da Visual Studio
*Quando si fa doppio clic su un progetto in Esplora soluzioni, non vengono visualizzati i comandi di Application Insights o non viene visualizzato il comando Apri Application Insights.*

Cause possibili:

* Se la risorsa di Application Insights hello è stato creato manualmente o se il progetto di hello è di un tipo che non è supportato dagli strumenti di Application Insights hello.
* strumenti per sviluppatori Analitica Hello sono disabilitati in di Visual Studio. 
* la versione di Visual Studio è precedente alla 2013 Update 3.

Correzione:

* Assicurarsi che la versione di Visual Studio sia 2013 Update 3 o versione successiva.
* Selezionare **Strumenti**, **Estensioni e aggiornamenti** e verificare l'installazione e l'abilitazione di **Developer Analytics Tools**. In questo caso, fare clic su **aggiornamenti** toosee se è disponibile un aggiornamento.
* Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni. Se viene visualizzato il comando hello **Application Insights > Configura Application Insights**, utilizzarlo tooconnect risorsa nel servizio di Application Insights hello toohello progetto.

In caso contrario, il tipo di progetto non è direttamente supportato dagli strumenti di Application Insights hello. toosee dati di telemetria, accedi toohello [portale di Azure](https://portal.azure.com)selezionare Application Insights nella barra di spostamento a sinistra di hello, selezionare l'applicazione.

## <a name="access-denied-on-opening-application-insights-from-visual-studio"></a>"Accesso negato" all'apertura di Application Insights da Visual Studio
*comando di menu 'Apri Application Insights' Hello richiede me toohello portale di Azure, ma viene visualizzato un errore "accesso negato".*

![](./media/app-insights-asp-net-troubleshoot-no-data/access-denied.png)

Hello Microsoft Accedi ultima utilizzata nel browser predefinito non ha accesso troppo[hello risorsa creata al momento di Application Insights è stato aggiunto l'app toothis](app-insights-asp-net.md). Le cause possibili sono due: 

* Si dispone di più di un account Microsoft - forse un lavoro e un account Microsoft personale? Hello accesso che è utilizzata l'ultima volta nel browser predefinito è per un account diverso rispetto a quello che ha accesso troppo hello[aggiungere Application Insights toohello progetto](app-insights-asp-net.md). 
  
  * Correzione: Fare clic sul nome nella parte superiore destra della finestra del browser hello e disconnettersi. Accedere quindi con account di hello dotato di accesso. Nella barra di spostamento a sinistra di hello, quindi fare clic su Application Insights e selezionare l'app.
* Un altro utente aggiunto progetto toohello Application Insights e dimenticanza toogive è [gruppo di risorse toohello accesso](app-insights-resources-roles-access-control.md) in cui è stato creato. 
  
  * Correzione: Se si usa un account aziendale, possono aggiungere si toohello team. oppure possono concedere si accesso individuale toohello gruppo di risorse.

## <a name="asset-not-found-on-opening-application-insights-from-visual-studio"></a>L'asset non viene trovato all'apertura di Application Insights da Visual Studio
*comando di menu 'Apri Application Insights' Hello richiede me toohello portale di Azure, ma viene visualizzato un errore "asset non trovato".*

Cause possibili:

* risorsa di Application Insights per l'applicazione Hello è stato eliminato, o
* chiave di strumentazione Hello è stato impostato o modificato in Applicationinsights, modificando direttamente, senza aggiornare il file di progetto hello. 

chiave di strumentazione Hello nei controlli Applicationinsights in cui vengono inviati i dati di telemetria hello. Una riga nel file di progetto hello determina quale risorsa viene aperto quando si utilizza il comando di hello in Visual Studio. 

Correzione:

* In Esplora soluzioni, fare clic sul progetto hello e scegliere di Application Insights, configurare Application Insights. Nella finestra di dialogo hello, è possibile scegliere una risorsa esistente di toosend telemetria tooan o crearne uno nuovo. In alternativa:
* Aprire la risorsa di hello direttamente. Accedi troppo[hello Azure portal](https://portal.azure.com), fare clic su Application Insights nella barra di spostamento a sinistra di hello e quindi selezionare l'app.

## <a name="where-do-i-find-my-telemetry"></a>Dove è possibile trovare i dati di telemetria?
*È stato firmato in toohello [portale Microsoft Azure](https://portal.azure.com), e si esamineranno hello Azure dashboard principale. dove è possibile trovare i dati di Application Insights?*

* Nella barra di spostamento a sinistra di hello, fare clic su Application Insights, quindi al nome dell'app. Se tutti i progetti non è presente, è necessario troppo[aggiungere o configurare Application Insights nel progetto web](app-insights-asp-net.md).
  
    Verranno visualizzati alcuni grafici di riepilogo. È possibile fare clic al loro interno toosee ulteriori dettagli.
* In Visual Studio, durante il debug dell'app, fare clic su pulsante Application Insights hello.

## <a name="q03"></a> Dati assenti o dati del server non presenti
*Si è stata eseguita l'applicazione e quindi aprire il servizio di Application Insights hello in Microsoft Azure, ma tutti hello grafici Mostra ' informazioni come toocollect... ' o "Non configurato".* Oppure *mostrano solo la visualizzazione pagina e i dati utente, ma non i dati del server.*

* Eseguire l'applicazione in modalità di debug in Visual Studio (F5). Utilizzare un'applicazione hello così come toogenerate alcuni dati di telemetria. Verificare che è possibile visualizzare gli eventi registrati nella finestra di output di hello Visual Studio. 
  
    ![](./media/app-insights-asp-net-troubleshoot-no-data/output-window.png)
* Nel portale Application Insights hello, aprire [ricerca diagnostica](app-insights-diagnostic-search.md). I dati vengono in genere visualizzati prima qui.
* Fare clic su pulsante Aggiorna hello. Pannello Hello viene automaticamente aggiornato periodicamente, ma è anche possibile farlo manualmente. intervallo di aggiornamento Hello è più lunga per gli intervalli di tempo maggiori.
* Verificare le chiavi di strumentazione hello corrispondano. Nel pannello principale di hello per l'app nel portale Application Insights hello in hello **Essentials** elenco a discesa, esaminare **chiave di strumentazione**. Quindi, nel progetto in Visual Studio, aprire Applicationinsights e trovare hello `<instrumentationkey>`. Verificare che hello due chiavi sono uguali. In caso contrario:
  
  * Nel portale di hello, fare clic su Application Insights e cercare risorse app hello con tasto destro hello; o
  * In Esplora soluzioni di Visual Studio, fare clic sul progetto hello e scegliere Configura Application Insights. Reimpostare hello app toosend telemetria toohello risorsa di destra.
  * Se non si trova hello chiavi corrispondenti, verificare che si utilizza hello stesso credenziali di accesso in Visual Studio come toohello portale.
    
    ![](./media/app-insights-asp-net-troubleshoot-no-data/ikey-check.png)
* In hello [dashboard principale di Microsoft Azure](https://portal.azure.com), esaminare mappa servizio integrità hello. Se sono presenti alcune indicazioni relative all'avviso, attendere hanno restituito tooOK e quindi chiudere e riaprire il pannello di applicazioni di Application Insights.
* Controllare anche il [blog sullo stato](http://blogs.msdn.com/b/applicationinsights-status/).
* È stato scritto il codice per hello [sul lato server SDK](app-insights-api-custom-events-metrics.md) che potrebbero modificare la chiave di strumentazione hello in `TelemetryClient` istanze o in `TelemetryContext`? Potrebbe anche essere stata scritta una [configurazione del filtro o di campionamento](app-insights-api-filtering-sampling.md) che esclude troppi dati.
* Se si modifica Applicationinsights, verificare con attenzione configurazione hello di [TelemetryInitializers e TelemetryProcessors](app-insights-api-filtering-sampling.md). Un tipo denominato in modo non corretto o il parametro non può causare hello SDK toosend alcun dato.

## <a name="q04"></a>Dati non presenti in Visualizzazioni pagina, Browser o Utilizzo
*Dati in tempo di risposta di Server e i grafici di richieste al Server, ma nessun dato viene visualizzato in fase di caricamento della visualizzazione pagina o in hello Browser o sui pannelli di utilizzo.*

Hello dati provengono da script nelle pagine web hello. 

* Se è stato aggiunto tooan Application Insights esistente progetto web, [aver manualmente gli script hello tooadd](app-insights-javascript.md).
* Verificare che il sito non venga visualizzato in modalità di compatibilità in Internet Explorer.
* Utilizzare funzionalità di debug del browser hello (F12 alcuni browser, quindi scegliere rete) tooverify che i dati vengano inviati troppo`dc.services.visualstudio.com`.

## <a name="no-dependency-or-exception-data"></a>Dati eccezione o dati sulle dipendenze non presenti
Vedere gli articoli relativi alla [telemetria delle dipendenze](app-insights-asp-net-dependencies.md) e alla [telemetria delle eccezioni](app-insights-asp-net-exceptions.md).

## <a name="no-performance-data"></a>Nessun dato sulle prestazioni
I dati sulle prestazioni (CPU, velocità di IO e così via) sono disponibili per[servizi Web Java](app-insights-java-collectd.md), [app desktop di Windows](app-insights-windows-desktop.md), [app e servizi Web IIS se si installa Status Monitor](app-insights-monitor-performance-live-website-now.md) e [servizi cloud di Azure](app-insights-azure.md). Sono disponibili in Impostazioni > Server.

I dati non sono disponibili per i siti Web di Azure.

## <a name="no-server-data-since-i-published-hello-app-toomy-server"></a>Nessun dato (server) poiché è stato pubblicato hello server toomy app
* Verificare che è stato effettivamente copiato tutti hello Microsoft. DLL di ApplicationInsights toohello server, insieme a Microsoft.Diagnostics.Instrumentation.Extensions.Intercept.dll
* Nel firewall, potrebbe essere troppo[aprire alcune porte TCP](app-insights-ip-addresses.md#data-access-api).
* Se si dispone di toouse toosend un proxy all'esterno della rete azienda, impostare [defaultProxy](https://msdn.microsoft.com/library/aa903360.aspx) in Web. config
* Windows Server 2008: Assicurarsi di avere installato hello dopo gli aggiornamenti: [KB2468871](https://support.microsoft.com/kb/2468871), [KB2533523](https://support.microsoft.com/kb/2533523), [KB2600217](https://support.microsoft.com/kb/2600217).

## <a name="i-used-toosee-data-but-it-has-stopped"></a>Utilizzato toosee dati, ma è stato arrestato
* Controllare hello [stato blog](http://blogs.msdn.com/b/applicationinsights-status/).
* È stata raggiunta la quota mensile relativa ai punti dati? Aprire hello impostazioni/quote e prezzi toofind out. Se la quota è stata raggiunta, è possibile aggiornare il piano oppure pagare per disporre di ulteriore capacità. Vedere hello [prezzi schema](https://azure.microsoft.com/pricing/details/application-insights/).

## <a name="i-dont-see-all-hello-data-im-expecting"></a>Non ho tutti i dati di hello che consapevole previsto
Se l'applicazione invia una grande quantità di dati e si utilizza hello Application Insights SDK per ASP.NET versione 2.0.0-beta3 o versione successiva, hello [campionamento adattivo](app-insights-sampling.md) funzionalità può operare e inviare solo una percentuale dei dati di telemetria. 

È possibile disabilitarla, ma non è consigliabile. Il campionamento è progettato in modo che i dati di telemetria correlati vengano trasmessi correttamente per scopi diagnostici. 

## <a name="wrong-geographical-data-in-user-telemetry"></a>Dati geografici errati nella telemetria utente
dimensioni paese, regione e città Hello sono derivate da indirizzi IP e non sono sempre accurate.

## <a name="exception-method-not-found-on-running-in-azure-cloud-services"></a>Eccezione "metodo non trovato" durante l'esecuzione dei servizi cloud di Azure
È stata eseguita la compilazione per .NET 4.6? La versione 4.6 non è supportata automaticamente nei ruoli dei servizi cloud di Azure. [Installare la versione 4.6 in ogni ruolo](../cloud-services/cloud-services-dotnet-install-dotnet.md) prima di eseguire l'app.

## <a name="still-not-working"></a>Non funzionante...
* [Forum di Application Insights](https://social.msdn.microsoft.com/Forums/vstudio/en-US/home?forum=ApplicationInsights)

