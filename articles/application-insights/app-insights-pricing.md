---
title: aaaManage volume di dati e sui prezzi per Azure Application Insights | Documenti Microsoft
description: Gestire volumi di dati di telemetria e monitorare i costi in Application Insights.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: ebd0d843-4780-4ff3-bc68-932aa44185f6
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: bwren
ms.openlocfilehash: 4621c989cd467735aefc48ec9547fcbe1b1ae41b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-pricing-and-data-volume-in-application-insights"></a>Gestire volumi di dati e prezzi in Application Insights


I prezzi per [Azure Application Insights][start] dipendono dal volume di dati per ogni applicazione. Un basso utilizzo durante lo sviluppo o per un'app di piccole dimensioni è probabilmente toobe gratuito, poiché non esiste un limite mensile consentito a 1 GB di dati di telemetria.

Ogni risorsa di Application Insights viene addebitata come un servizio distinto e contribuisce fattura toohello per tooAzure la sottoscrizione.

Esistono due piani tariffari. il piano predefinito Hello viene denominato Basic. È possibile scegliere per il piano aziendale hello, che non dispone di un addebito giornaliero, ma consente di determinate funzionalità aggiuntive, ad esempio [l'esportazione continua](app-insights-export-telemetry.md).

Nel caso di domande sul funzionamento dei prezzi per Application Insights, è possibile toopost disponibile una domanda nei nostri [forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=ApplicationInsights). 

## <a name="hello-price-plans"></a>piani di prezzo Hello

Vedere hello [pagina dei prezzi di Application Insights] [ pricing] per i prezzi correnti in valuta.

### <a name="basic-plan"></a>Piano Basic

piano di base Hello è predefinito hello quando viene creata una nuova risorsa di Application Insights e sarà sufficiente per la maggior parte dei clienti.

* Nel piano base hello, vengono addebitati dal volume di dati: numero di byte di dati di telemetria ricevuti da Application Insights. Volume di dati viene misurato come dimensione hello del pacchetto di dati JSON hello non compresso ricevuto da Application Insights dall'applicazione.
Per [dati tabulari importati Analitica](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-import), volume di dati hello viene misurato come hello dimensioni non compresse del file inviati tooApplication Insights.  
* Il primo 1 GB per ogni app è gratuita, pertanto se si è appena sperimentazione o lo sviluppo, improbabile che toohave toopay.
* I dati [Live Metrics Stream](app-insights-live-stream.md) non vengono conteggiati ai fini della determinazione del prezzo.
* [L'esportazione continua](app-insights-export-telemetry.md) è disponibile per un addebito per ogni GB aggiuntivo nel piano base hello.

### <a name="enterprise-plan"></a>Piano Enterprise

* Nel piano dell'organizzazione hello, l'app può utilizzare tutte le funzionalità di hello di Application Insights. [Esportazione continua](app-insights-export-telemetry.md) e 

[Registrare il connettore Analitica](https://go.microsoft.com/fwlink/?LinkId=833039&amp;clcid=0x409) disponibili senza alcun costo aggiuntivo nel piano dell'organizzazione hello.
* Si paga per ogni nodo che invia i dati di telemetria per le app nel piano dell'organizzazione hello. 
 * Un *nodo* è una macchina server fisica o virtuale oppure un'istanza del ruolo PaaS (piattaforma distribuita come servizio) che ospita l'app.
 * Computer di sviluppo, browser client e dispositivi mobili non sono conteggiati come nodi.
 * Se l'app dispone di diversi componenti che inviano dati di telemetria, ad esempio un servizio Web e un lavoro back-end, questi vengono conteggiati separatamente.
 * I dati di [Live Metrics Stream](app-insights-live-stream.md) non vengono conteggiati per la determinazione dei prezzi.* In una sottoscrizione, i costi vengono calcolati per ogni nodo, non per ogni app. Se si dispongano di cinque nodi l'invio dei dati di telemetria di 12 App, quindi hello addebitare i costi è per cinque nodi.
* Sebbene gli addebiti siano fatturati mensilmente, quelli effettivi hanno luogo solo nelle ore durante le quali un nodo invia dati di telemetria da un'app. Hello tariffa oraria è hello racchiuso tra virgolette addebito mensile / 744 (numero di ore al mese giorno 31 hello).
* Viene fornita un'allocazione di volume di dati di 200 MB al giorno per ciascun nodo rilevato (con granularità oraria). Allocazione di dati non utilizzati non vengono trasferito da un giorno toohello successivamente.
 * Se si sceglie l'opzione di determinazione dei prezzi di Enterprise hello, ogni sottoscrizione Ottiene un'indennità giornaliera di dati in base al numero di hello di nodi, l'invio di dati di telemetria toohello risorse di Application Insights nella sottoscrizione. Se si dispone di 5 nodi l'invio dei dati tutto il giorno, è una tolleranza in pool di risorse di Application Insights di 1 GB applicato tooall hello nella sottoscrizione. Non è importante se alcuni nodi inviano che più dati di altri nodi perché hello include i dati sono condivisa tra tutti i nodi. Se un determinato giorno, risorse di Application Insights hello ricevono più dati rispetto a quella inclusa in hello giornaliero l'allocazione di dati per questa sottoscrizione, hello GB dati eccedenza addebitati. 
 * indennità dati Hello viene calcolato come numero hello di ore della giornata hello (utilizzando l'ora UTC) che ogni nodo stia inviando dati di telemetria diviso per 24 ore pari a 200 MB. Pertanto se si dispone di 4 nodi, l'invio di dati di telemetria durante 15 di hello in hello 24 ore, hello inclusi dati per tale giorno sarebbe ((4 x 15) / 24) x 200 MB = 500 MB. Prezzi hello di 2.30 USD per GB per eccedenza dati, addebito hello per sarebbe USD 1.15 se i nodi di hello inviano 1 GB di dati del giorno corrente.
 * Indennità giornaliera del piano di hello Enterprise non è condivisa con le applicazioni per cui si è scelto l'opzione di base hello e inutilizzato indennità non viene trasferito su base giornaliera. 
* Di seguito sono riportati alcuni esempi di determinazione di un conteggio di nodi specifico:
| Scenario                               | Conteggio giornaliero totale dei nodi |
|:---------------------------------------|:----------------:|
| 1 applicazione usa 3 istanze del Servizio app di Azure e 1 server virtuale | 4 |
| 3 applicazioni in esecuzione su 2 macchine virtuali e risorse di Application Insights hello per queste applicazioni sono hello stessa sottoscrizione e in hello Enterprise del piano | 2 | 
| 4 applicazioni le cui risorse Insights applicazioni sono in hello stessa sottoscrizione. Ogni applicazione esegue 2 istanze durante 16 ore di scarso traffico e 4 istanze durante 8 ore di traffico intenso. | 13.33 | 
| Servizi cloud con ruolo di lavoro 1 e 1 ruolo Web, ognuno dei quali esegue 2 istanze | 4 | 
| Cluster Service Fabric a 5 nodi che esegue 50 microservizi. Ciascun microservizio esegue 3 istanze | 5|

* comportamento di conteggio di Hello preciso nodo varia utilizza Application Insights SDK dell'applicazione. 
  * In SDK versione 2.2 e poi, entrambi hello Application Insights [Core SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights/) o [Web SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/) verrà ogni applicazione host come un nodo di report, ad esempio hello nome del computer per i server fisici e gli host macchina virtuale o hello nome dell'istanza nel caso di hello di servizi cloud.  Hello solo eccezione è applicazioni utilizzando solo [.NET Core](https://dotnet.github.io/) e hello Application Insights Core SDK, in cui un solo nodo case risulterà per tutti gli host perché il nome host hello non è disponibile. 
  * Per le versioni precedenti di hello SDK hello [Web SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/) si comporteranno come hello versioni SDK più recente, tuttavia hello [Core SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights/) segnalerà un solo nodo indipendentemente dal numero di hello di host applicazioni effettivo. 
  * Si noti che se l'applicazione utilizza valore personalizzato di hello SDK tooset roleInstance tooa, per impostazione predefinita lo stesso valore verrà utilizzato il conteggio hello toodetermine di nodi. 
  * Se si utilizza una nuova versione SDK con un'applicazione che viene eseguita dal computer client o i dispositivi mobili, è possibile che il numero di hello dei nodi potrebbe restituire un numero molto elevato (dal numero elevato di hello di dispositivi mobili o computer client). 

### <a name="multi-step-web-tests"></a>Test Web in più passaggi

È prevista una tariffa aggiuntiva per i [test Web in più passaggi](app-insights-monitor-web-app-availability.md#multi-step-web-tests). Si riferisce tooweb test che eseguono una sequenza di azioni. 

Non è prevista una tariffa separata per le "verifiche ping" di una singola pagina. I dati di telemetria delle verifiche ping e delle verifiche in più fasi incorrono in costi insieme agli altri dati di telemetria provenienti dall'app.
 
## <a name="operations-management-suite-subscription-entitlement"></a>Diritti della sottoscrizione di Operations Management Suite

Come [ha recentemente annunciato](https://blogs.technet.microsoft.com/msoms/2017/05/19/azure-application-insights-enterprise-as-part-of-operations-management-suite-subscription/), i clienti che acquistano Microsoft Operations Management Suite E1 ed E2 sono in grado di tooget Application Insights Enterprise come un componente aggiuntivo senza alcun costo aggiuntivo. In particolare, ogni unità di Operations Management Suite E1 ed E2 include un nodo too1 il diritto del piano dell'organizzazione hello di Application Insights. Come indicato in precedenza, ogni nodo di Application Insights include backup too200 MB di dati di caricamento al giorno (separato dall'inserimento di dati di Log Analitica), con la conservazione dei dati di 90 giorni senza alcun costo aggiuntivo. 

> [!NOTE]
> tooensure si ottiene questo diritto, è necessario che le risorse di Application Insights in Enterprise hello prezzi piano. Questo diritto si applica solo come nodi, in modo da risorse di Application Insights nel piano base hello non otterranno alcun vantaggio. Si noti che questo diritto non saranno visibile in hello stimato costi visualizzati nella funzionalità hello + prezzi blade. 
>
 
## <a name="review-pricing-plans-and-estimate-costs"></a>Esaminare i piani tariffari e stimare i costi

Insights Applicaition rende facile toounderstand hello prezzi piani disponibili e quali hello costi sono probabilmente basarsi su modelli di utilizzo recenti. Inizio dall'apertura hello **funzionalità + prezzi** pannello nella risorsa di Application Insights nel portale di Azure hello hello:

![Scegliere Prezzi.](./media/app-insights-pricing/01-pricing.png)

**a.** Esaminare il volume di dati per il mese di hello. Sono inclusi tutti i dati ricevuti e conservati hello (dopo qualsiasi [campionamento](app-insights-sampling.md) dal server e le applicazioni client e il test di disponibilità.

**b.** I costi per i [test Web in più passaggi](app-insights-monitor-web-app-availability.md#multi-step-web-tests) vengono addebitati separatamente. (Questo non include test di disponibilità semplice, che rientrano nei costi di volume di dati hello).

**c.** Abilitare piano dell'organizzazione hello.

**d.** Fare clic sulle toodata gestione opzioni tooview volume dei dati per il mese scorso hello, impostare un limite giornaliero o impostare il campionamento di inserimento.

Gli addebiti di Application Insights vengono aggiunti tooyour fattura di Azure. È possibile visualizzare i dettagli di Azure fatturare nella sezione di fatturazione di hello portale di Azure o in hello hello [Azure Billing Portal](https://account.windowsazure.com/Subscriptions). 

![Nel menu laterale hello, scegliere la fatturazione.](./media/app-insights-pricing/02-billing.png)

## <a name="data-rate"></a>Velocità dati
Esistono tre modi in cui hello è limitato inviare i dati di volume:

* **Campionamento:** questo meccanismo consente di ridurre la quantità hello di telemetria inviato dall'App client e server, con distorsione delle metriche. Questo è lo strumento principale di hello è necessario tootune hello quantità di dati. Altre informazioni sulle [funzionalità di campionamento](app-insights-sampling.md). 
* **Limite giornaliero:** quando crea una risorsa di Application Insights dal portale di Azure hello è impostato too500 GB/giorno. salve predefinito durante la creazione di una risorsa di Application Insights da Visual Studio, è piccolo (solo 32,3 MB al giorno), che è destinato solo toofaciliate test. In questo caso lo scopo di che tale utente hello genererà limite giornaliero di hello prima di distribuire l'applicazione hello nell'ambiente di produzione. tetto massimo Hello è 500 GB/giorno, a meno che non è stata richiesta massima di un'applicazione di traffico elevato. Prestare attenzione quando si imposta limite giornaliero di hello, come lo scopo previsto deve essere **mai toohit hello limite giornaliero**, in quanto si verrà quindi perdita di dati per il resto di hello del giorno hello e deve essere toomonitor non è possibile l'applicazione. toochange non, utilizzare hello giornaliero volume perno pannello collegato dal Pannello di gestione di volumi di dati hello (vedere sotto). Tenere presente che ad alcuni tipi di sottoscrizione è associato un credito che non può essere usato per Application Insights. Se hello sottoscrizione ha una spesa limitare, hello quotidianamente pannello perno avrà come istruzioni tooremove e abilitare hello giornaliero toobe estremità generato oltre 32,3 MB al giorno.  
* **Limitazione:** questa limiti hello dati velocità too32 k gli eventi al secondo, calcolata la media di più di 1 minuto. 


*Cosa accade se mia app supera la limitazione di velocità hello?*

* volume Hello dei dati che invia l'app viene valutata ogni minuto. Se il valore supera hello al secondo medio minuto hello, server hello Rifiuta alcune richieste. Hello SDK hello dati nei buffer e quindi tenta tooresend, la distribuzione di un carico in diversi minuti. Se l'app in modo coerente invia dati di sopra di hello la limitazione di velocità, alcuni dati verranno eliminati. (hello ASP.NET, Java e JavaScript SDK provare tooresend in questo modo, altri SDK potrebbe semplicemente i dati di riepilogo limitata). In caso di avvenuta limitazione, verrà visualizzata una notifica che avviserà che ciò si è verificato.

*Come è possibile conoscere la quantità di dati inviati dall'app?*

* Aprire hello **gestione di volumi di dati** pannello toosee hello giornaliero dati volume grafico. 
* Altrimenti, in Esplora metriche, aggiungere un nuovo grafico e selezionare **Volume punti dati** come metrica. Attivare il raggruppamento in base a **Tipo di dati**.

## <a name="tooreduce-your-data-rate"></a>tooreduce la percentuale di dati
Ecco alcune operazioni è possibile eseguire tooreduce il volume di dati:

* Utilizzare [Campionamento](app-insights-sampling.md). Questa tecnologia consente di ridurre velocità dati senza inclinazione le metriche e senza interrompere hello possibilità toonavigate tra gli elementi correlati nella ricerca. Nelle app server funziona automaticamente.
* [Limitare il numero di hello di chiamate Ajax che può essere segnalata](app-insights-javascript.md#detailed-configuration) in ogni pagina o opzione reporting Ajax.
* Disattivare i moduli di raccolta non necessari [modificando il file ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Ad esempio, è possibile che i contatori delle prestazioni o dati sulle dipendenze siano non essenziali.
* Suddividere le chiavi di dati di telemetria tooseparate strumentazione. 
* Pre-aggregare metriche. Se è stato inserito chiamate tooTrackMetric nell'app, è possibile ridurre il traffico utilizzando hello overload che accetta il calcolo della media hello e deviazione standard di un batch di misure. In alternativa è possibile usare un [pacchetto di pre-aggregazione](https://www.myget.org/gallery/applicationinsights-sdk-labs).

## <a name="managing-hello-maximum-daily-data-volume"></a>Gestire il volume di dati di hello massimo giornaliero

È possibile utilizzare hello giornaliero volume perno toolimit hello dati raccolti, ma se viene soddisfatta perno hello, si verificherà una perdita di tutti i telemetery inviati dall'applicazione per il resto di hello del giorno hello. È **non consigliabile** toohave il limite giornaliero di hello toohit applicazione dal sono integrità hello tootrack non è possibile e le prestazioni dell'applicazione dopo che viene raggiunto. 

Utilizzare invece [campionamento](app-insights-sampling.md) tootune hello volume toohello livello di dati desiderato e utilizzare limite giornaliero di hello solo come "strettamente", nel caso in cui l'applicazione inizia a inviare quantità volumi più elevati di telemetery in modo imprevisto. 

Fare clic su toochange limite giornaliero di hello, nella sezione di configurazione della risorsa, Insihgts applicazione hello **gestione di volumi di dati** quindi **limite giornaliero**.

![Regolare il limite giornaliero telemetria volume hello](./media/app-insights-pricing/daily-cap.png) 

## <a name="sampling"></a>campionamento
[Campionamento](app-insights-sampling.md) è un metodo di riduzione hello frequenza dati di telemetria è inviati tooyour app, mentre pur mantenendo hello possibilità toofind eventi correlati durante le ricerche di diagnostica e di conta ancora conservazione evento corretto. 

Il campionamento è un modo efficace tooreduce spese e superare la quota mensile. Hello algoritmo di campionamento consente di mantenere gli elementi correlati di telemetria, in modo che, ad esempio, quando si usa la ricerca, è possibile trovare la richiesta hello correlati tooa particolare eccezione. algoritmo Hello mantiene inoltre i conteggi corretti, che consente di visualizzare i valori corretti hello in Esplora metriche per frequenza richieste, sulle tariffe di eccezione e altri contatori.

Sono disponibili diversi tipi di campionamento.

* [Campionamento adattivo](app-insights-sampling.md) è predefinito hello hello ASP.NET SDK, che consente di regolare automaticamente toohello volume di dati di telemetria che invia l'app. Funziona automaticamente in hello SDK nell'app web in modo che il traffico di dati di telemetria hello nella rete hello è ridotto. 
* *Campionamento inserimento* rappresenta un'alternativa che opera a punto hello telemetria dall'app entra in servizio di Application Insights hello. Non influisce sul volume hello di telemetria inviato dall'app, ma riduce il volume di hello mantenuto dal servizio hello. È possibile utilizzare la quota di hello tooreduce utilizzato dati di telemetria da altri SDK e i browser.

inserimento di tooset di campionamento, impostare il controllo hello nel Pannello di prezzi hello:

![Da hello quote e prezzi pannello, fare clic sul riquadro esempi hello e selezionare una frazione di campionamento.](./media/app-insights-pricing/04.png)

> [!WARNING]
> Pannello di campionamento dei dati Hello controlla solo il valore di hello di campionamento di inserimento. Non non indicare la frequenza di campionamento hello che viene applicata da hello Application Insights SDK nell'applicazione. Se i dati di telemetria hello in arrivo già campionati a hello SDK, il campionamento di inserimento non viene applicato.
> 

hello toodiscover effettivo campionamento frequenza indipendentemente da dove è stato applicato, usare un [query Analitica](app-insights-analytics.md) simile al seguente:

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

In ogni mantenuti record, `itemCount` indica il numero di hello di record originali che esso rappresenta, too1 uguale + il numero di hello di record scartati precedente. 


## <a name="automation"></a>Automazione

È possibile scrivere un piano di prezzo hello tooset di script, tramite Gestione risorse di Azure. [Informazioni](app-insights-powershell.md#price).

## <a name="limits-summary"></a>Riepilogo dei limiti
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

## <a name="next-steps"></a>Passaggi successivi

* [Campionamento](app-insights-sampling.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiproperties]: app-insights-api-custom-events-metrics.md#properties
[start]: app-insights-overview.md
[pricing]: http://azure.microsoft.com/pricing/details/application-insights/

