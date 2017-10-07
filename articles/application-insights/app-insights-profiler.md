---
title: le applicazioni web in tempo reale aaaProfiling in Azure con Application Insights | Documenti Microsoft
description: Identificare percorso critico di hello nel codice server web con un profiler footprint ridotto.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: 3c7f21076f19335e0f006327932e13623ec9526b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="profiling-live-azure-web-apps-with-application-insights"></a>Profilatura delle app Web di Azure attive con Application Insights

*Questa funzionalità di Application Insights è GA per i servizi app e in anteprima per il calcolo.*

Scoprire come tempo speso per ogni metodo nell'applicazione web in tempo reale tramite lo strumento di profilatura hello [Azure Application Insights](app-insights-overview.md). Consente di visualizzare dettagliati profili di richieste in tempo reale che sono state soddisfatte dall'app ed evidenzia hello 'percorso critico' che utilizza ora la maggior parte delle hello. Seleziona automaticamente esempi con tempi di risposta diversi. profiler Hello utilizza overhead di toominimize varie tecniche.

Hello profiler attualmente può essere usato per ASP.NET web App in esecuzione su servizi di App di Azure, in almeno hello a livello di prezzo Basic. 

<a id="installation"></a>
## <a name="enable-hello-profiler"></a>Attivare il profiler hello

[Installare Application Insights](app-insights-asp-net.md) nel codice. Se è già installato, verificare di che aver la versione più recente di hello. (toodo, mouse sul progetto in Esplora soluzioni e scegliere Gestione pacchetti NuGet. Selezionare gli aggiornamenti e aggiornare tutti i pacchetti. Distribuire nuovamente l'app.

*Uso di ASP.NET Core [Fare clic qui](#aspnetcore)*.

In [https://portal.azure.com](https://portal.azure.com), aprire la risorsa di Application Insights hello per le app web. Aprire **Prestazioni** e fare clic su **Abilita Application Insights Profiler...**.

![Fare clic sull'intestazione di profiler enable hello][enable-profiler-banner]

In alternativa, è sempre possibile fare clic **configura** stato tooview, abilitare o disabilitare hello Profiler.

![Nel pannello prestazioni hello, fare clic su Configura][performance-blade]

Le app Web configurate con Application Insights sono elencate nel pannello Configura. Seguire le istruzioni tooinstall hello Profiler agente se necessario. Se nessuna app Web è stata ancora configurata con Application Insights, fare clic su *Add Linked Apps* (Aggiungere app collegate).

Hello utilizzare *abilitare Profiler* o *disabilitare Profiler* pulsanti hello Configura pannello toocontrol hello Profiler in tutte le app web collegati.



![Pannello Configura][linked app services]

profiler hello toostop o il riavvio per una singola istanza di servizio App, risulterà **nella risorsa di servizio App hello**nella **processi Web**. toodelete che cerca in **estensioni**.

![Disabilitare il profiler per un processo Web][disable-profiler-webjob]

Si consiglia di disporre di hello Profiler abilitato in tutti i toodiscover App web un miglioramento delle prestazioni problemi appena possibile.

Se si utilizza l'applicazione web di WebDeploy toodeploy modifiche tooyour, assicurarsi che si esclude hello **App_Data** cartella venga eliminato durante la distribuzione. In caso contrario, hello file dell'estensione di profiler verrà eliminato alla successiva distribuzione tooAzure applicazione web di hello.

### <a name="using-profiler-with-azure-vms-and-compute-resources-preview"></a>Uso del profiler con le macchine virtuali di Azure e le risorse di calcolo (anteprima)

Quando si [abilita Application Insights per i servizi app di Azure in fase di esecuzione](app-insights-azure-web-apps.md#run-time-instrumentation-with-application-insights), il profiler è automaticamente disponibile. (Se già abilitato Application Insights per la risorsa hello, potrebbe essere necessario tooupdate toohello lates versione tramite hello **configura** procedura guidata.)

È presente un [versione di anteprima di hello Profiler per le risorse di calcolo di Azure](https://go.microsoft.com/fwlink/?linkid=848155).


## <a name="limits"></a>Limiti

conservazione dei dati di Hello predefinito è 5 giorni. Massimo 10 GB inseriti al giorno.

Non è previsto alcun addebito per il servizio profiler hello. L'app web deve essere ospitato in hello almeno del livello Basic di servizi di App.

## <a name="viewing-profiler-data"></a>Visualizzazione dei dati del profiler

Aprire il pannello di prestazioni hello e scorrere verso il basso l'elenco di operazioni toohello.




![Colonna di esempi del pannello delle prestazioni di Application Insights][performance-blade-examples]

Hello colonne nella tabella hello sono:

* **Conteggio** -numero di tali richieste nell'intervallo di tempo hello del pannello hello hello.
* **Mediana** -hello tipico tempo app toorespond tooa richiesta. La metà di tutte le risposte è più veloce rispetto a questo valore.
* **95° percentile**: il 95% delle risposte ha una velocità superiore rispetto a questo valore. Se questa figura è molto diversa dal valore mediano di hello, potrebbe esserci un problema intermittente con l'app. In alternativa la causa potrebbe essere una funzione di progettazione, ad esempio la memorizzazione nella cache.
* **Esempi di** -un'icona indica che il profiler hello ha acquisito le analisi dello stack per questa operazione.

Fare clic su Esplora di hello esempi icona tooopen hello traccia. Hello explorer mostra alcuni esempi in cui hello profiler ha acquisito, classificati per tempo di risposta.

Selezionare un tooshow esempio dettagli a livello di codice di tempo impiegato per richiesta hello in esecuzione.

![Explorer di analisi Application Insights][trace-explorer]

**Mostra percorso ricorrente** apre hello principale nodo foglia o chiudere almeno un valore. Nella maggior parte dei casi questo nodo sarà collo di bottiglia delle prestazioni tooa adiacenti.



* **Etichetta**: nome hello di funzione hello o un evento. struttura ad albero Hello Mostra una combinazione di codice e gli eventi che si è verificato (ad esempio gli eventi SQL e http). evento superiore Hello rappresenta hello complessivo durata della richiesta.
* **Trascorso**: intervallo di tempo hello tra inizio hello dell'operazione hello e di fine di hello.
* **Quando**: indica quando hello funzione/evento è stato in esecuzione nelle funzioni tooother relazione.

## <a name="how-tooread-performance-data"></a>Come i dati sulle prestazioni tooread

Il profiler di servizi di Microsoft utilizza una combinazione di campionamento (metodo) e la strumentazione tooanalyze hello delle prestazioni dell'applicazione.
Quando insieme dettagliato è in corso, esempi di profiler service hello puntatore all'istruzione di ogni CPU della macchina hello in ogni millisecondo.
Ogni esempio acquisisce stack di chiamate completo hello del thread di hello attualmente in esecuzione, fornendo informazioni dettagliate e utili sulle operazioni che thread stava eseguendo entrambi alti e bassi livelli di astrazione. Profiler servizio raccoglie anche altri eventi, ad esempio gli eventi di commutazione di contesto, gli eventi TPL e correlazione attività tootrack gli eventi di pool di thread e della causalità.

stack di chiamate Hello mostrato nella visualizzazione della cronologia di hello è risultato hello di hello di sopra di campionamento e strumentazione. Poiché ogni esempio acquisisce stack di chiamate completo hello del thread di hello, include codice da .NET framework di hello, nonché altri framework in cui che si fa riferimento.

### <a id="jitnewobj"></a>Allocazione oggetti (`clr!JIT\_New or clr!JIT\_Newarr1`)
`clr!JIT\_New and clr!JIT\_Newarr1` sono le funzioni di supporto all'interno di .NET Framework che consentono di allocare memoria dall'heap gestito. `clr!JIT\_New` viene richiamato quando si alloca un oggetto. `clr!JIT\_Newarr1` viene richiamato quando si alloca una matrice di oggetti. Queste due funzioni sono in genere molto veloci e richiedono un intervallo temporale relativamente ridotto. Se viene visualizzato `clr!JIT\_New` o `clr!JIT\_Newarr1` richiedere una notevole quantità di tempo nell'indicatore cronologico, è un'indicazione codice hello potrebbe essere l'allocazione di molti oggetti che utilizzano una quantità notevole di memoria.

### <a id="theprestub"></a>Caricamento di codice (`clr!ThePreStub`)
`clr!ThePreStub`è una funzione di supporto all'interno di .NET framework che prepara tooexecute codice hello hello prima volta. Include ad esempio la compilazione JIT (Just In Time). Per ogni metodo c# `clr!ThePreStub` deve essere richiamato più di una volta nel corso della durata hello di un processo.

Se viene visualizzato `clr!ThePreStub` richiede una quantità significativa di tempo per una richiesta, indica che la richiesta è hello primo che viene eseguita tale metodo e l'ora di hello per tooload di runtime .NET framework che metodo è significativo. È possibile considerare un processo di riscaldamento che esegue la parte di codice hello prima che agli utenti diritti di accesso o l'esecuzione di NGen nell'assembly.

### <a id="lockcontention"></a>Conflitto di blocchi (`clr!JITutil\_MonContention` o `clr!JITutil\_MonEnterWorker`)
`clr!JITutil\_MonContention`o `clr!JITutil\_MonEnterWorker` indicano thread corrente hello è in attesa di un blocco di toobe rilasciato. In genere viene visualizzato durante l'esecuzione di un'istruzione di blocco C#, richiamando il metodo Monitor.Enter o richiamando un metodo con l'attributo MethodImplOptions.Synchronized. Contesa dei blocchi avviene in genere quando un thread acquisisce un blocco, e thread B prova hello tooacquire stesso blocco prima che lo rilascia il thread.

### <a id="ngencold"></a>Caricamento di codice (`[COLD]`)
Se il nome del metodo hello contiene `[COLD]`, ad esempio `mscorlib.ni![COLD]System.Reflection.CustomAttribute.IsDefined`, significa che il runtime di .NET framework hello è in esecuzione il codice che non è ottimizzato per <a href="https://msdn.microsoft.com/library/e7k32f4k.aspx">ottimizzazione PGO</a> per hello prima volta. Per ogni metodo, dovrebbe essere inclusa più di una volta nel corso della durata hello del processo di hello.

Se durante il caricamento di codice richiede una quantità significativa di tempo per una richiesta, indica che la richiesta è hello prima uno tooexecute hello non ottimizzata parte del metodo hello. È possibile considerare un processo che esegue la parte di codice hello prima che agli utenti diritti di accesso di riscaldamento.

### <a id="httpclientsend"></a>Inviare una richiesta HTTP
I metodi come `HttpClient.Send` indicano codice hello è in attesa di un toocomplete di richiesta HTTP.

### <a id="sqlcommand"></a>Operazione di database
Metodo, ad esempio SqlCommand.Execute indica codice hello è in attesa di un toocomplete di operazione di database.

### <a id="await"></a>In attesa (`AWAIT\_TIME`)
`AWAIT\_TIME`indica il codice hello è in attesa di un'altra attività toocomplete. Questo accade solitamente con l'istruzione C# 'await'. Quando esegue codice hello c# 'await', rimuove hello thread e restituisce i pool di thread di controllo toohello e nessun thread bloccato in attesa per toofinish 'await' hello. Tuttavia, in modo logico hello thread che ha hello await "bloccato" in attesa toocomplete operazione hello. Il `AWAIT\_TIME` indica il tempo di hello bloccato in attesa di hello toocomplete di attività.

### <a id="block"></a>Tempo blocco
`BLOCKED_TIME`indica il codice hello è in attesa di un altro toobe di risorse disponibili, ad esempio in attesa di un oggetto di sincronizzazione, in attesa di un thread toobe disponibile, o in attesa di una richiesta toofinish.

### <a id="cpu"></a>Tempo CPU
Hello della CPU è occupato, l'esecuzione di istruzioni hello.

### <a id="disk"></a>Tempo disco
un'applicazione Hello sta eseguendo operazioni su disco.

### <a id="network"></a>Tempo rete
un'applicazione Hello esegue operazioni di rete.

### <a id="when"></a>Colonna Quando
Si tratta di una visualizzazione della modalità campioni INCLUSIVI di hello raccolti per un nodo variano nel tempo. intervallo totale di Hello della richiesta di hello è suddiviso in 32 intervalli di tempo e campioni inclusivi di hello per tale nodo vengono accumulate in tali 32 bucket. Ogni bucket è rappresentato come una barra, la cui altezza rappresenta un valore in scala. Per i nodi contrassegnati `CPU_TIME` o `BLOCKED_TIME`, o in cui è presente una relazione ovvia di utilizzo di una risorsa (cpu, disco, thread), hello barra rappresenta l'utilizzo di uno di tali risorse per periodo hello di bucket. Per queste metriche è possibile ottenere più del 100% utilizzando più risorse. Ad esempio, se in media si usano due CPU in un intervallo si ottiene il 200%.


## <a id="troubleshooting"></a>Risoluzione dei problemi

### <a name="how-can-i-know-whether-application-insights-profiler-is-running"></a>Come è possibile verificare se il profiler di Application Insights è in esecuzione?

profiler Hello viene eseguito come processo web continuo nell'App Web. È possibile aprire risorse di App Web hello in https://portal.azure.com e controllare lo stato di "ApplicationInsightsProfiler" nel pannello processi Web hello. Se non è in esecuzione, aprire **registri** toofind altre.

### <a name="why-cant-i-find-any-stack-examples-even-though-hello-profiler-is-running"></a>Non è possibile visualizzare eventuali esempi stack anche se è in esecuzione profiler hello?

Ecco alcuni aspetti da controllare:

1. Assicurarsi che il piano di servizio app sia di livello Basic e superiore.
2. Assicurarsi che l'app Web disponga di Application Insights SDK 2.2 Beta e superiore abilitato.
3. Verificare che l'App Web è l'impostazione APPINSIGHTS_INSTRUMENTATIONKEY hello con hello stessa chiave di strumentazione usata da Application Insights SDK.
4. Assicurarsi che l'App Web sia in esecuzione su .Net Framework 4.6.
5. In caso di un'applicazione ASP.NET di base, anche verificare [hello dipendenze obbligatorie](#aspnetcore).

Una volta avviato il profiler di hello, sussiste un periodo di riscaldamento breve quando hello profiler raccoglie attivamente le tracce di prestazioni diverse. Successivamente, hello profiler raccoglie le tracce sulle prestazioni per due minuti in ogni ora.  

### <a name="i-was-using-azure-service-profiler-what-happened-tooit"></a>Stavo usando il profiler del servizio Azure. Quali tooit verificato anomalo?  

Quando si abilita il profiler di Application Insights, l'agente del profiler del servizio Azure viene disabilitato.

### <a id="double-counting"></a>Doppio conteggio dei thread in parallelo

In alcuni hello casi metrica tempo totale in Visualizzatore stack hello è maggiore durata effettiva di hello della richiesta di hello.

Questa situazione può verificarsi quando sono presenti due o più thread associati a una richiesta, che operano in parallelo. Hello tempo totale di thread è quindi maggiore di tempo trascorso hello. In molti casi, potrebbe essere in attesa di un thread di hello altri toocomplete. Hello questo visualizzatore prova toodetect e omettere l'attesa di hello non interessanti, ma errs sul lato di hello mostrare troppa anziché l'omissione di ciò che potrebbe essere informazioni critiche.  

Quando si visualizza thread paralleli le tracce, è necessario toodetermine thread in attesa in modo è possibile determinare hello percorso critico per la richiesta di hello. Nella maggior parte dei casi, i thread hello rapidamente va in uno stato di attesa semplicemente in attesa di hello altri thread. Concentrare hello altri e ignorare il tempo di hello in thread in attesa di hello.

### <a id="issue-loading-trace-in-viewer"></a>Senza dati di profilatura

1. Se i dati di hello si sta tentando tooview è antecedente a un paio di settimane, è possibile limitare il filtro temporale e riprovare.

2. Verifica che un firewall o proxy non siano bloccate toohttps://gateway.azureserviceprofiler.net accesso.

3. Verificare che hello Application Insights è la chiave di strumentazione in uso nell'app stessa hello come risorsa di Application Insights è stato abilitato il profiling con hello. chiave di Hello è in genere in Applicationinsights, ma può essere rilevate anche in App. config o Web. config.

### <a name="error-report-in-hello-profiling-viewer"></a>Segnalazione di errori nel Visualizzatore profiling hello

Un ticket di supporto dal portale hello del file. Includere l'ID di correlazione hello dal messaggio di errore hello.

## <a name="manual-installation"></a>Installazione manuale

Quando si configura il profiler di hello, hello apportati gli aggiornamenti seguenti sono le impostazioni dell'App Web toohello. È possibile eseguire queste operazioni manualmente se l'ambiente lo richiede, ad esempio se l'applicazione viene eseguita nell'ambiente del servizio app di Azure:

1. Nel Pannello di controllo di hello web app, aprire le impostazioni.
2. Impostare ".Net Framework versione" toov4.6.
3. Impostare tooOn "Always On".
4. Aggiungere l'impostazione dell'app "__APPINSIGHTS_INSTRUMENTATIONKEY__" e set hello valore toohello stessa chiave di strumentazione usata da hello SDK.
5. Aprire Strumenti avanzati.
6. Fare clic su "Go" sito Web di tooopen hello Kudu.
7. Nel sito Web Kudu hello, selezionare "Le estensioni del sito".
8. Installare "__Application Insights__" dalla raccolta.
9. Riavviare l'app web hello.

## <a id="aspnetcore"></a>Supporto di ASP.NET Core

Applicazione ASP.NET di base deve tooinstall 2.1.0-beta6 pacchetto Microsoft.ApplicationInsights.AspNetCore Nuget o toowork superiore con hello Profiler. È non supportano più le versioni precedenti di hello dopo 27/6/2017.

## <a name="next-steps"></a>Passaggi successivi

* [Uso di Application Insights in Visual Studio](https://docs.microsoft.com/azure/application-insights/app-insights-visual-studio)

[performance-blade]: ./media/app-insights-profiler/performance-blade.png
[performance-blade-examples]: ./media/app-insights-profiler/performance-blade-examples.png
[trace-explorer]: ./media/app-insights-profiler/trace-explorer.png
[trace-explorer-toolbar]: ./media/app-insights-profiler/trace-explorer-toolbar.png
[trace-explorer-hint-tip]: ./media/app-insights-profiler/trace-explorer-hint-tip.png
[trace-explorer-hot-path]: ./media/app-insights-profiler/trace-explorer-hot-path.png
[enable-profiler-banner]: ./media/app-insights-profiler/enable-profiler-banner.png
[disable-profiler-webjob]: ./media/app-insights-profiler/disable-profiler-webjob.png
[linked app services]: ./media/app-insights-profiler/linked-app-services.png
