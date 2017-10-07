---
title: dati aaaFind con ricerche nei log in Azure Log Analitica | Documenti Microsoft
description: "Ricerche nei log consentono toocombine e correlare i dati dei computer da più origini all'interno dell'ambiente."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 0d7b6712-1722-423b-a60f-05389cde3625
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 1161857a0027f05726492417362cb24a8fe21ef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a>Trovare dati con ricerche nei log in Log Analytics

>[!NOTE]
> Questo articolo descrive l'utilizzo del linguaggio di query corrente hello in Log Analitica ricerche nei log.  Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi è consigliabile consultare troppo[Understanding log eseguire ricerche nei Log Analitica (nuovo)](log-analytics-log-search-new.md).


Base hello di Log Analitica è funzionalità di ricerca log hello, che consente toocombine e correlare i dati dei computer da più origini all'interno dell'ambiente. Le soluzioni sono inoltre basate toobring di ricerca di log è metriche specifiche per una particolare area problematica.

Nella pagina di ricerca hello, è possibile creare una query e quindi quando esegue la ricerca, è possibile filtrare hello risultati usando controlli facet. È anche possibile creare query avanzate tootransform, filtro e report sui risultati.

Le query di ricerca log più comuni sono visualizzate nella maggior parte delle pagine delle soluzioni. Nella console di OMS hello, è possibile fare clic su riquadri o analizzare elementi tooother tooview dettagli sull'elemento hello utilizzando la ricerca di log.

In questa esercitazione verranno esaminati esempi toocover tutti elementi fondamentali di hello quando si usa la ricerca di log.

Viene iniziano con esempi semplici e pratici e quindi compilare su di essi in modo che è possibile ottenere la comprensione di casi d'uso pratici sulla modalità di insights di toouse hello sintassi tooextract hello dai dati hello.

Dopo avere acquisito familiarità con le tecniche di ricerca, è possibile esaminare hello [riferimento alla ricerca di log Log Analitica](log-analytics-search-reference.md).

## <a name="use-basic-filters"></a>Usare filtri di base
Hello in primo luogo tooknow è tale hello prima parte di una query di ricerca, prima di qualsiasi "|" carattere di barra verticale, è sempre un *filtro*. Si può considerare come una clausola WHERE in TSQL: determina *cosa* subset di dati toopull dall'archivio dati OMS di hello. Ricerca nell'archivio dati hello è importante specificare caratteristiche hello dei dati di hello che si desidera tooextract, pertanto è normale che una query inizi con hello clausola WHERE.

Hello filtri più semplici è possibile utilizzare sono *parole chiave*, ad esempio 'error' o 'timeout' o un nome di computer. Questi tipi di query semplici restituiscono in genere diverse forme di dati all'interno di hello stesso set di risultati. Infatti Log Analitica presenta diversi *tipi* dei dati nel sistema hello.

### <a name="tooconduct-a-simple-search"></a>tooconduct una ricerca semplice
1. Nel portale OMS hello, fare clic su **ricerca nei Log**.  
    ![riquadro di ricerca](./media/log-analytics-log-searches/oms-overview-log-search.png)
2. Nel campo della query hello digitare `error` e quindi fare clic su **ricerca**.  
    ![errore di ricerca](./media/log-analytics-log-searches/oms-search-error.png)  
    Ad esempio, query di hello per `error` in hello immagine seguente ha restituito 100.000 **evento** record (raccolti da Log Management), 18 **ConfigurationAlert** record (generato dalla configurazione Assessment) e 12 **ConfigurationChange** record (acquisiti da Change Tracking hello).   
    ![risultati della ricerca](./media/log-analytics-log-searches/oms-search-results01.png)  

Questi filtri non sono realmente tipi o classi di oggetti. *Tipo* è semplicemente un tag o una proprietà o una stringa/nome/categoria, che è collegato tooa parte dei dati. Alcuni documenti nel sistema hello vengono contrassegnati come **Type: ConfigurationAlert** e alcuni vengono contrassegnati come **tipo: prestazioni**, o **Type: Event**e così via. Ogni risultato della ricerca, documento, record o voce vengono visualizzate tutte le proprietà non elaborato di hello e i relativi valori per ciascuno di tali dati, e utilizzare tali toospecify di nomi di campo nel filtro hello quando si desidera che solo i record hello tooretrieve cui campo hello presenta specificato valore.

*Type* è in realtà solo un campo che contiene tutti i record, non è diverso dagli altri campi. Ciò è stato stabilito in base al valore di hello hello del campo di tipo. Quel record avrà una forma o un formato diversi. Tra l'altro, **tipo = Perf**, o **tipo di evento =** è anche hello sintassi che è necessario toolearn tooquery per gli eventi o dati sulle prestazioni.

È possibile utilizzare i due punti (:) o un segno di uguale (=) dopo il nome di campo hello e prima del valore hello. **Type: Event** e **tipo di evento =** sono equivalenti nel significato, è possibile scegliere hello stile desiderato.

In tal caso, se hello digitare = Perf record hanno un campo denominato 'CounterName', quindi è possibile scrivere una query simile a `Type=Perf CounterName="% Processor Time"`.

Questa query fornirà solo i dati sulle prestazioni hello in cui il nome del contatore delle prestazioni di hello è "% Processor Time".

### <a name="toosearch-for-processor-time-performance-data"></a>toosearch per i dati sulle prestazioni di tempo processore
* Nel campo di query di ricerca hello, digitare`Type=Perf CounterName="% Processor Time"`

È anche possibile essere più specifici e usare **InstanceName = _ 'Total'** nella query hello, che rappresenta un contatore delle prestazioni di Windows. È possibile anche selezionare un facet e un altro **field:value**. filtro Hello viene automaticamente aggiunto tooyour filtro nella barra di query hello. È possibile vedere questo nella seguente immagine hello. Viene illustrato dove tooclick tooadd **InstanceName: Total'** toohello query senza digitare nulla.

![facet di ricerca](./media/log-analytics-log-searches/oms-search-facet.png)

La query diventa `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`

In questo esempio, non si dispone di toospecify **tipo = Perf** tooget toothis risultato. Poiché hello campi CounterName e InstanceName esistono solo per i record di tipo = Perf, query hello è abbastanza specifico tooreturn hello stessi risultati come hello precedente, più lunga:

```
CounterName="% Processor Time" InstanceName="_Total"
```

In questo modo tutti i filtri nella query hello hello vengono valutati come in *AND* tra loro. In effetti, hello ulteriori campi aggiunti toohello criteri, si ottiene minore, risultati più specifici e complessi.

Ad esempio, query di hello `Type=Event EventLog="Windows PowerShell"` è identico troppo`Type=Event AND EventLog="Windows PowerShell"`. Restituisce tutti gli eventi che sono stati registrati nel e raccolti dal registro eventi di Windows PowerShell hello. Se si aggiunge un filtro più volte selezionando ripetutamente hello stesso facet, quindi problema hello è puramente descrittivo, potrebbe creare confusione barra di ricerca hello, ma restituisce comunque hello stessi risultati perché l'operatore AND implicito hello è sempre presente.

È possibile invertire facilmente l'operatore AND implicito hello usando un operatore NOT in modo esplicito. ad esempio:

`Type:Event NOT(EventLog:"Windows PowerShell")`o l'equivalente `Type=Event EventLog!="Windows PowerShell"` restituiscono tutti gli eventi da tutti gli altri log che non sono il log di Windows PowerShell hello.

In alternativa, è possibile usare altri operatori booleani, ad esempio 'OR'. esempio Hello query restituisce i record per cui hello EventLog è Application OR System.

```
EventLog=Application OR EventLog=System
```

Utilizza hello di sopra di query, si otterranno le voci per entrambi i log in hello stesso set di risultati.

Tuttavia, se rimuove hello o lasciando hello operatore implicito AND, quindi hello nella query seguente non produrrà alcun risultato perché non è una voce del registro eventi che appartiene tooBOTH log. Ogni voce del registro eventi è stato scritto tooonly uno dei due log hello.

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a>Usare filtri aggiuntivi
Hello nella query seguente restituisce le voci per 2 registri eventi per tutti i computer hello che hanno inviato dati.

```
EventLog=Application OR EventLog=System
```

![risultati della ricerca](./media/log-analytics-log-searches/oms-search-results03.png)

Se si seleziona uno dei campi hello o filtri restringerà hello query tooa computer specifico, escludendo tutti gli altri. la query risultante Hello è simile al seguente esempio hello.

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

Che è equivalente toohello seguenti, a causa di hello operatore AND implicito.

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

Ogni query viene considerata nell'ordine esplicito seguente hello. Parentesi hello nota.

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

Come campo hello del registro eventi, è possibile recuperare i dati solo per un set di computer specifici aggiungendo o. ad esempio:

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

Analogamente, questa hello seguenti restituiscono query **% CPU Time** per hello selezionato solo due computer.

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a>Tipi di campo
Quando si creano filtri, è necessario comprendere le differenze di hello durante l'utilizzo di tipi diversi di campi restituiti nelle ricerche di log.

**I campi ricercabili** sono in blu nei risultati della ricerca.  È possibile utilizzare i campi ricercabili nel campo toohello specifiche condizioni di ricerca come illustrato di seguito hello:

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

**I campi ricercabili a testo libero** vengono visualizzati in grigio nei risultati della ricerca.  Non possono essere utilizzate con campo toohello specifiche condizioni di ricerca come campi ricercabili.  Ricerca solo quando si esegue una query per tutti i campi come illustrato di seguito hello.

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a>Operatori booleani
Con i campi di data/ora e numerici, è possibile cercare i valori usando *maggiore di*, *minore di* e *minore o uguale a*. È possibile usare operatori semplici come >, <>, =, < =,! = nella barra di ricerca di query hello.

È possibile eseguire una query su un registro eventi specifico per uno specifico periodo di tempo. Ad esempio, hello ultime 24 ore viene espresso con hello seguente espressione mnemonica.

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="toosearch-using-a-boolean-operator"></a>toosearch usando un operatore booleano
* Nel campo di query di ricerca hello, digitare`EventLog=System TimeGenerated>NOW-24HOURS`  
    ![ricerca con valore booleano](./media/log-analytics-log-searches/oms-search-boolean.png)

Anche se è possibile controllare hello graficamente l'intervallo di tempo e la maggior parte delle volte in cui è possibile toodo, vi sono vantaggi tooincluding un filtro temporale direttamente nella query hello. Ad esempio, è efficace con i dashboard in cui è possibile eseguire l'override di tempo hello per ogni riquadro, indipendentemente dal hello *globale* selettore ora nella pagina dashboard hello. Per altre informazioni, vedere l'argomento relativo alle [questioni di tempo nel dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).

Quando si Filtra per volta, tenere presente che si ottengano risultati per hello *intersezione* di hello due periodi di tempo: quello specificato nel portale OMS hello (S1) hello e hello quello specificato nella query hello (S2).

![intersezione](./media/log-analytics-log-searches/oms-search-intersection.png)

Ciò significa che, se hello periodi di tempo non si intersecano, ad esempio nel portale OMS hello è stata scelta **questa settimana** e nella query hello in cui si definisce **ultima settimana**, non esiste alcuna intersezione e non è visualizzato alcun risultato.

Gli operatori di confronto utilizzati per il campo TimeGenerated hello sono utili anche in altre situazioni. Ad esempio, con i campi numerici.

Ad esempio, poiché gli avvisi di Configuration Assessment presentano hello i valori di gravità seguenti:

* 0 = Informazioni
* 1 = Avviso
* 2 = Avviso critico

È possibile eseguire una query per gli avvisi critici o avvisi e informativi con hello seguenti query di escludere anche:

```
Type=ConfigurationAlert  Severity>=1
```


È inoltre possibile usare le query di intervallo. Ciò significa che è possibile fornire hello inizio e fine dell'intervallo di valori in una sequenza. Ad esempio, se si desidera che gli eventi dal registro eventi di Operations Manager hello dove hello EventID è maggiore o uguale too2100 ma non maggiore di 2199, quindi hello query seguente restituirà tali eventi.

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> è necessario utilizzare sintassi dell'intervallo hello è separatore: valore del campo di due punti (:) hello e *non* hello segno di uguale (=). Estremità di hello inferiore e superiore dell'intervallo di hello di racchiudere tra parentesi quadre e separarle con due punti (.).
>
>

## <a name="manipulate-search-results"></a>Modificare i risultati della ricerca
Quando si esegue una ricerca per i dati, verranno desidera toorefine query di ricerca e avere un buon livello di controllo sui risultati di hello. Quando vengono recuperati i risultati, è possibile applicare comandi tootransform li.

I comandi nelle ricerche Log Analitica *deve* seguire hello carattere di barra verticale (|). Un filtro deve essere sempre prima parte di hello di una stringa di query. Definisce il set di dati hello in uso e quindi "Invia" i risultati in un comando. È quindi possibile utilizzare comandi aggiuntivi di hello pipe tooadd. Si tratta della pipeline di Windows PowerShell toohello simile a regime di controllo libero.

In generale, il linguaggio di ricerca Log Analitica hello Cerca toomake di stile e le linee guida di PowerShell toofollow it simili toohello IT Pro e tooease hello curva di apprendimento.

I comandi hanno nomi di verbi, pertanto è possibile stabilire facilmente quali azioni eseguono.  

### <a name="sort"></a>Ordina
comando sort Hello consente hello toodefine ordinamento da uno o più campi. Anche se non viene usato, per impostazione predefinita, viene applicato un ordine decrescente di tempo. risultati più recenti Hello sono sempre nella parte superiore di hello dei risultati della ricerca. Ciò significa che quando si esegue una ricerca con `Type=Event EventID=1234`, in realtà la query che viene eseguita automaticamente è:

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

Ciò avviene perché è il tipo di hello di esperienza con che cui si ha familiarità nei log. Ad esempio, nel Visualizzatore eventi di Windows hello.

È possibile utilizzare l'ordinamento toochange hello modo risultati vengono restituiti. Hello esempi seguenti viene illustrato il funzionamento.

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


Hello esempi semplici sopra illustrano il funzionano dei comandi - cambiano la forma hello dei risultati hello hello filtro restituito.

### <a name="limit-and-top"></a>Limit e top
Un altro comando meno noto è LIMIT. Limit è un verbo di tipo PowerShell. Limite è comando TOP toohello funzionalmente identico. Hello query seguenti restituiscono hello stessi risultati.

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="toosearch-using-top"></a>utilizzo di top toosearch
* Nel campo di query di ricerca hello, digitare`Type=Event EventID=600 | Top 1`   
    ![top di ricerca](./media/log-analytics-log-searches/oms-search-top.png)

Nell'immagine hello precedente, sono presenti migliaia di 358 record con EventID = 600. Hello campi e facet filtri su hello lasciato sempre mostrano informazioni sui risultati di hello *dalla parte filtro hello* di query hello, che fa parte di hello prima di qualsiasi carattere di barra verticale. Hello **risultati** riquadro restituisce solo il risultato di hello 1 più recente, perché il comando di esempio hello ha definito e trasformato i risultati di hello.

### <a name="select"></a>Selezionare
comando SELECT Hello si comporta come Select-Object in PowerShell. Restituisce i risultati filtrati che non presentano tutte le relative proprietà originali. Al contrario, seleziona solo le proprietà hello specificate.

#### <a name="toorun-a-search-using-hello-select-command"></a>toorun una ricerca usando il comando select hello
1. Nella ricerca, digitare `Type=Event` e quindi fare clic su **Search**.
2. Fare clic su **+ Mostra altre** in uno dei tooview risultati hello tutte le proprietà di hello che hello risultati.
3. Selezionandone alcune in modo esplicito e hello le modifiche alle query troppo`Type=Event | Select Computer,EventID,RenderedDescription`.  
    ![select di ricerca](./media/log-analytics-log-searches/oms-search-select.png)

Questo comando è particolarmente utile quando si desidera toocontrol output di ricerca e scegliere hello porzioni di dati davvero importanti per l'esplorazione, che spesso non record completo hello. Il comando è utile anche quando record di tipo diverso hanno *alcune* proprietà comuni, ma non *tutte*. È possibile generare un output simile a una tabella o funziona bene quando esportato file CSV tooa e quindi modificato in Excel.

## <a name="use-hello-measure-command"></a>Usare il comando di measure hello
MEASURE è uno dei comandi più versatili di hello nelle ricerche Log Analitica. Consente di tooapply statistica *funzioni* tooyour dati e aggregare i risultati raggruppati in base a un determinato campo. Esistono più funzioni statistiche supportate dal comando Measure.

### <a name="measure-count"></a>Measure count()
Hello prima funzione statistica toowork con, e uno di toounderstand più semplice hello è hello *Count ()* (funzione).

Nei risultati di una query di ricerca, ad esempio `Type=Event`, i filtri, denominati anche facet su hello il lato sinistro di risultati della ricerca. Hello filtri visualizzano una distribuzione di valori da un determinato campo, per risultati hello hello ricerca eseguita.

![measure count di ricerca](./media/log-analytics-log-searches/oms-search-measure-count01.png)

Ad esempio, nei hello immagine sopra si noterà hello **Computer** campo indica che in hello quasi 739 migliaia di eventi nei risultati di hello, esistono 68 valori univoci e distinti per hello **Computer** campo in questi record. Hello riquadro vengono visualizzati solo hello i primi 5, che sono hello 5 i valori più comuni che vengono scritti in hello **Computer** campi), ordinati in base al numero di hello di documenti che contengono quel valore specifico in quel campo. Nell'immagine hello si noterà che, quasi 369 migliaia di eventi, delle migliaia 90 provengono dal computer OpsInsights04.contoso.com hello, mille 83 dal computer DB03.contoso.com hello e così via.

Cosa accade se si desidera toosee tutti i valori, poiché hello riquadro vengono visualizzati solo hello solo i primi 5?

Ovvero le misure hello comando è possibile eseguire con funzione di hello Count (). Per questa funzione non viene usato alcun parametro. È sufficiente specificare il campo hello mediante il quale si desidera toogroup da – hello **Computer** in questo caso:

`Type=Event | Measure count() by Computer`

![measure count di ricerca](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

Tuttavia, **Computer** è semplicemente un campo usato *in* tutti i dati: non è coinvolto alcun database relazionale e non esiste alcun oggetto **Computer** separato altrove. Hello solo valori *in* hello dati possono descrivere quale entità ha generato e un numero di altre caratteristiche e aspetti dei dati hello: hello pertanto termine *facet*. Tuttavia, è possibile eseguire il raggruppamento anche in base ad altri campi. Poiché i risultati originali di hello di quasi 739 migliaia di eventi inviati comando measure hello presentano anche un campo denominato **EventID**, è possibile applicare hello stessa tecnica toogroup base a tale campo e ottenere un conteggio di eventi per EventID:

```
Type=Event | Measure count() by EventID
```

Se non si è interessati Conteggio record effettivo hello che contengono un valore specifico, ma invece se si vuole solo un elenco di hello gli stessi valori, è possibile aggiungere un *selezionare* comando alla fine hello e nella prima colonna hello basta selezionare:

```
Type=Event | Measure count() by EventID | Select EventID
```

È quindi possibile ottenere risultati più complessi e ordinare in precedenza hello risultati query hello oppure è possibile fare semplicemente clic colonne hello nella griglia hello troppo.

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="toosearch-using-measure-count"></a>toosearch con measure count
* Nel campo di query di ricerca hello, digitare`Type=Event | Measure count() by EventID`
* Aggiungere `| Select EventID` toohello fine della query hello.
* Infine, aggiungere `| Sort EventID asc` toohello fine della query hello.

Esistono due aspetti importanti toonotice e mettere in evidenza:

In primo luogo, hello risultati visualizzati non sono risultati originali non elaborati di hello più. Sono invece risultati aggregati, essenzialmente gruppi di risultati. Ciò non rappresenta un problema, ma è importante comprendere che si interagisce con una forma di dati che è molto diversa da hello forma originale non elaborata che viene creata in tempo reale di hello come risultato di funzione di aggregazione/statistica hello.

In secondo luogo, **misura Conteggio** attualmente restituisce hello solo primi 100 risultati distinti. Questo limite non si applica toohello altre funzioni statistiche. In tal caso, in genere è necessario toouse un toosearch prima di filtro più preciso per elementi specifici prima di applicare measure Count ().

## <a name="use-hello-max-and-min-functions-with-hello-measure-command"></a>Utilizzare le funzioni max e min hello con il comando measure hello
Esistono vari scenari in cui è utile usare **Measure Max()** e **Measure Min()**. Tuttavia, poiché ciascuna funzione è opposta all'altra, verrà illustrata la funzione Max() e l'utente sperimenterà autonomamente la funzione Min().

Se si esegue una query per gli eventi di sicurezza, tali eventi hanno una proprietà **Livello** che può variare. Ad esempio:

```
Type=SecurityEvent
```

![measure count start di ricerca](./media/log-analytics-log-searches/oms-search-measure-max01.png)

Se si desidera valore più alto di hello tooview per sicurezza hello tutti gli eventi di un determinato Computer comune, hello campo Raggruppa per, è possibile utilizzare

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![measure max computer di ricerca](./media/log-analytics-log-searches/oms-search-measure-max02.png)

Che verrà visualizzato per i computer che avevano hello **livello** record, la maggior parte di essi hanno almeno 8, a livello molti ha un livello di 16.

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![measure max time generated computer di ricerca](./media/log-analytics-log-searches/oms-search-measure-max03.png)

Questa funzione è adatta ad essere usata con i numeri, ma può essere usata anche con i campi di data/ora. È utile toocheck per hello ultimo o timestamp più recente per tutti i dati indicizzati per ciascun computer. Ad esempio: quando è stato evento di sicurezza più recente di hello segnalato per ciascuna macchina?

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-hello-avg-function-with-hello-measure-command"></a>Funzione avg hello con il comando measure hello
valore medio di hello toocalculate per alcuni campi consente Hello utilizzata con misura la funzione statistica AVG () e gruppo di risultati da hello stesso o un altro campo. Questa funzione è utile in diversi casi, ad esempio con i dati sulle prestazioni.

Si inizierà con i dati sulle prestazioni. Si noti che OMS attualmente raccoglie i contatori delle prestazioni sia per i computer Windows che Linux.

toosearch per *tutti* dati sulle prestazioni, la query più semplice di hello è:

```
Type=Perf
```

![avg start di ricerca](./media/log-analytics-log-searches/oms-search-avg01.png)

Hello prima cosa da notare è che Analitica Log mostra tre prospettive: elenco che mostra che mostra i record effettivi hello dietro i grafici hello; Tabella che mostra una vista tabulare di dati del contatore delle prestazioni. e la metrica che mostra i grafici per hello contatori delle prestazioni.

Nell'immagine hello sopra, sono disponibili due set di campi contrassegnati che indicano l'esempio hello:

* Hello primo set identifica nome contatore delle prestazioni di Windows, il nome di oggetto e nome dell'istanza nel filtro di query hello. Questi sono campi hello è probabilmente verranno in genere utilizzato come facet/filtri
* **CounterValue** è hello valore effettivo del contatore hello. In questo esempio, il valore di hello è *75*.
* **TimeGenerated** è 12:51, nel formato 24 ore.

Di seguito è riportata una visualizzazione delle metriche hello in un grafico.

![avg start di ricerca](./media/log-analytics-log-searches/oms-search-avg02.png)

Dopo la lettura di informazioni sulla forma di record prestazioni hello e, con informazioni sulle altre tecniche di ricerca, è possibile utilizzare questo tipo di dati numerici misura tooaggregate AVG ().

Un semplice esempio viene riportato di seguito:

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![avg samplevalue di ricerca](./media/log-analytics-log-searches/oms-search-avg03.png)

In questo esempio si seleziona contatore delle prestazioni CPU Total Time hello e Media dal Computer. Se si desidera toonarrow verso il basso il hello tooonly risultati ultima 6 ore, è possibile utilizzare il controllo di filtro ora hello o specificare la query come indicato di seguito:

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="toosearch-using-hello-avg-function-with-hello-measure-command"></a>funzione avg hello con il comando measure hello toosearch
* Nella casella Search hello, digitare `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.

È possibile aggregare e correlare i dati *tra* computer. Ad esempio, si supponga di disporre di un set di host in un certo tipo di farm in cui ogni nodo è uguale tooany altro e avviene solo hello tutti stesso tipo di lavoro e il carico è approssimativamente bilanciato. È possibile ottenere i contatori che tutti contemporaneamente con hello seguente query e ottenere le medie per l'intera farm hello. È possibile iniziare scegliendo i computer hello con hello di esempio seguente:

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

Ora che sono presenti computer hello, si desidera anche solo tooselect due gli indicatori delle prestazioni chiave (KPI): % CPU Usage e % spazio libero su disco. In tal caso, quella parte della query hello diventa:

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

È ora possibile aggiungere computer e contatori con hello di esempio seguente:

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

Poiché si dispone di una selezione molto specifica, hello **misurare AVG ()** comando può restituire hello Media non dal computer, ma la farm di hello, eseguendo il raggruppamento per CounterName. ad esempio:

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

Ciò consente una visualizzazione utile e compatta di un paio di indicatori di prestazioni chiave dell'ambiente.

![avg grouping di ricerca](./media/log-analytics-log-searches/oms-search-avg04.png)

In un dashboard, è possibile utilizzare facilmente query di ricerca hello. Ad esempio, è possibile salvare la query di ricerca hello e creare un dashboard da esso denominato *gli indicatori KPI di Web Farm*. toolearn ulteriori informazioni sull'utilizzo di dashboard, vedere [creare un dashboard personalizzato in Log Analitica](log-analytics-dashboards.md).

![avg dashboard di ricerca](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-hello-sum-function-with-hello-measure-command"></a>Utilizzare la funzione di somma hello con il comando measure hello
Funzione sum Hello è simile tooother funzioni del comando measure hello. È possibile visualizzare un esempio su come toouse hello funzione sum [ricerca nei log di IIS W3C in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).

È possibile usare Max() e Min() con numeri, intervalli di data/ora e stringhe di testo. Le stringhe di testo sono ordinate in ordine alfabetico e vengono visualizzate la prima e l'ultima.

Tuttavia, è possibile usare Sum() con elementi diversi dai campi numerici. Questo vale anche tooAvg().

### <a name="use-hello-percentile-function-with-hello-measure-command"></a>Utilizzare la funzione di percentile hello con il comando measure hello
funzione percentile Hello è simile tooAvg() e SUM () in quanto è possibile utilizzare solo per i campi numerici. È possibile utilizzare qualsiasi percentile tra 1 too99 in un campo numerico. È possibile usare sia il comando**percentile** che il comando **pct**. Di seguito sono riportati alcuni esempi:  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-hello-where-command"></a>Utilizzare hello dove comando
Hello in cui funziona come un filtro, ma può essere applicato nel filtro di hello pipeline toofurther aggregati i risultati prodotti da un comando Measure, come tooraw anziché i risultati vengono filtrati all'inizio di hello di una query.

ad esempio:

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

È possibile aggiungere un'altra barra verticale "|" hello e carattere comando tooonly dove ottenere i computer il cui utilizzo medio della CPU è superiore all'80%, con hello seguente esempio:

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

Se si ha familiarità con Microsoft System Center - Operations Manager, è possibile pensare di hello dove comando in termini di management pack. Se l'esempio hello fosse una regola, hello prima parte della query hello sarebbe hello e origine dati hello in cui comando sarebbe rilevamento della condizione hello.

È possibile utilizzare query hello come un riquadro in **My Dashboard**, come un monitoraggio di ordinamento, toosee quando computer CPU è sovrautilizzato. toolearn altre informazioni sui dashboard, vedere [creare un dashboard personalizzato in Log Analitica](log-analytics-dashboards.md). È anche possibile creare e utilizzare i dashboard con hello app per dispositivi mobili. Per altre informazioni, vedere la pagina relativa all'[app OMS per dispositivi mobili ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865). Nei riquadri di inferiore due hello di hello seguente immagine, è possibile vedere Monitoraggio hello visualizzati un elenco e come un numero. In pratica, sempre necessario hello numero toobe zero e hello toobe elenco vuoto. In caso contrario, indica una condizione di avviso. Se necessario, è possibile utilizzare tootake esaminare quali computer sono sotto pressione.

![dashboard mobile](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-hello-in-operator"></a>Utilizzare hello in (operatore)
Hello *IN* (operatore), insieme a *NOT IN* consente le ricerche secondarie toouse, ovvero ricerche che includono un'altra ricerca come argomento. Sono racchiuse tra parentesi graffe {} all'interno di un'altra ricerca *primaria* o *esterna*. il risultato di Hello di una ricerca secondaria, spesso un elenco di risultati distinti, viene quindi usato come argomento nella ricerca primaria.

È possibile utilizzare le ricerche secondarie toomatch subset di dati che non è possibile descrivere direttamente in un'espressione di ricerca, ma che possono essere generati da una ricerca. Ad esempio, se si è interessati all'uso di tutti gli eventi da una ricerca toofind *computer privi di aggiornamenti della sicurezza*, è necessario toodesign una ricerca secondaria che identifichi *computer privi di aggiornamenti della sicurezza*  prima di trovare gli eventi appartenenti toothose host.

In tal caso, è possibile esprimere *computer attualmente privi di necessari aggiornamenti della sicurezza* con hello seguente query:

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![esempio di ricerca con IN](./media/log-analytics-log-searches/oms-search-in01-revised.png)

Dopo aver creato elenco hello, è possibile utilizzare ricerca hello come un elenco di hello toofeed ricerca interna dei computer in una ricerca esterna (primaria) che cercherà gli eventi per tali computer. Questo caso, racchiudere la ricerca interna hello tra parentesi graffe e inserire i risultati come possibili valori per un filtro/campo nella ricerca esterna di hello utilizzando l'operatore IN hello. query Hello è simile al seguente:

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![esempio di ricerca con IN](./media/log-analytics-log-searches/oms-search-in02-revised.png)

Anche tempo hello notifica filtro usato nella ricerca interna hello perché hello System Update Assessment esegue uno snapshot di tutti i computer ogni 24 ore. È possibile rendere la query interna di hello più leggera e precisa cercando solo un giorno. ricerca esterna Hello Usa invece la selezione di tempo hello nell'interfaccia utente di hello, recuperando gli eventi da hello ultimi 7 giorni. Per altre informazioni sugli operatori temporali, vedere la sezione [Operatori booleani](#boolean-operators) .

Perché si usa solo hello i risultati della ricerca interna di hello come un valore di filtro per hello esterno, è comunque possibile applicare i comandi nella ricerca esterna hello. Ad esempio, è comunque possibile hello gruppo sopra gli eventi con un altro comando measure:

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![esempio di ricerca con IN](./media/log-analytics-log-searches/oms-search-in03-revised.png)

In genere, si desidera tooexecute la query interna rapidamente perché in Log Analitica timeout lato servizio, nonché tooreturn una piccola quantità di risultati. Se la query interna hello restituisce più risultati, viene troncato elenco risultati hello, che possono provocare hello ricerca esterna tooreturn risultati non corretti.

Un'altra regola prevede che ricerca interna hello attualmente tooprovide *aggregati* risultati. In altre parole deve contenere un comando *measure* , perché attualmente non è possibile inserire risultati non elaborati in una ricerca esterna.

Inoltre, può esistere un solo operatore IN, e che deve essere hello l'ultimo filtro nella query hello. Non possono essere più operatori IN o sarebbe: ciò che impedisce essenzialmente l'esecuzione di più ricerche secondarie: hello importante punto è che una sola ricerca secondaria/interna, è possibile per ogni ricerca esterna.

Anche con questi limiti, IN consente diverse tipologie di ricerche correlate e permette toodefine toogroups simile, ad esempio computer, utenti o file, tutti gli eventuali campi hello nei dati contengono. Di seguito sono riportati altri esempi:

**Tutti gli aggiornamenti mancanti nei computer in cui è disabilitato l'aggiornamento automatico**

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

**Tutti gli eventi di errore dai computer che eseguono SQL Server, in cui viene eseguito SQL Assessment**

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

**Tutti gli eventi di sicurezza dai computer che sono controller di dominio, in cui viene eseguito AD Assessment**

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

**Quali altri account hanno effettuato toohello stesso computer in cui si è connesso l'account BACONLAND\jochan?**

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-hello-distinct-command"></a>Comando distinti hello
Come suggerisce il nome di hello, questo comando fornisce un elenco di valori distinct per un campo. È estremamente semplice ma molto utile. Hello che stesso può essere ottenuto anche, come illustrato di seguito con il comando measure Count ().

```
Type=Event | Measure count() by Computer
```

![esempio di comando di ricerca DISTINCT](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

Tuttavia, se si è interessati solo a un elenco di valori distinti e non hello conteggio dei documenti che contengono che i valori, quindi DISTINCT può fornire tooread più semplice e leggibile di output e una sintassi più breve, come illustrato di seguito.

```
Type=Event | Distinct Computer
```
![esempio di comando di ricerca DISTINCT](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-hello-countdistinct-function-with-hello-measure-command"></a>Funzione countdistinct hello con il comando measure hello
funzione countdistinct Hello hello conteggio di valori distinti in ogni gruppo. Ad esempio, potrebbe essere utilizzato toocount hello numero di computer univoci per ogni tipo:

```
* | measure countdistinct(Computer) by Type
```

![OMS-countdistinct](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-hello-measure-interval-command"></a>Comando hello misura intervallo
La raccolta di dati sulle prestazioni quasi in tempo reale permette di raccogliere e visualizzare qualsiasi contatore delle prestazioni in Log Analytics. Semplicemente immettere query hello **tipo: prestazioni** restituirà migliaia di grafici metrica in base al numero di hello di contatori e i server nell'ambiente Analitica di Log. Con l'aggregazione di metrica su richiesta, è possibile esaminare hello complessive metriche nell'ambiente a un livello elevato e approfondimento di dati più granulari che è necessario.

Si supponga che si desidera tooknow hello utilizzo medio della CPU tra tutti i computer. Esaminando hello utilizzo medio della CPU per tutti i computer potrebbe non essere utile in quanto i risultati possono ottenere smussati. toolook in ulteriori dettagli, è possibile aggregare i risultati in un momento più piccolo blocchi di finestra e cercare in una serie temporale tra diverse dimensioni. Ad esempio, è possibile eseguire hello oraria circa l'utilizzo della CPU tra tutti i computer come indicato di seguito:

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![misura intervallo medio](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

Per impostazione predefinita, questi risultati vengono visualizzati in un grafico a linee interattivo a più serie.  Il grafico supporta l'attivazione e la disattivazione delle serie con ridimensionamento dell'asse Y, lo zoom e il passaggio del puntatore.  opzione di visualizzazione tabella Hello è ancora disponibile per la visualizzazione dei dati non elaborati hello se necessario.

È anche possibile raggruppare in base ad altri campi. In questo esempio, ricerca di tutti i contatori % hello per un computer specifico e desidera tooknow i percentili oraria 70 hello di ogni contatore:

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
Una cosa toonote è che queste query non sono limitate tooperformance contatori. È possibile applicarle tooany metrica. In questo esempio si esaminano i log di IIS W3C. Desidera tooknow hello massimo tempo su un intervallo di 5 minuti per l'elaborazione di ogni richiesta:

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a>Usare più aggregazioni in una query
È possibile specificare più clausole di aggregazione in un comando measure.  Ognuna di esse può essere associata a un alias in modo indipendente.  Se non viene assegnato un alias di hello risultante il nome del campo sarà la funzione di aggregazione hello che è stata utilizzata (ad esempio "avg(CounterValue)" per avg(CounterValue)).

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS-multiaggregates1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

Di seguito è riportato un altro esempio:

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sulle ricerche nei log:

* Utilizzare [campi personalizzati nel registro Analitica](log-analytics-custom-fields.md) tooextend ricerche nei log.
* Hello revisione [riferimento alla ricerca di log Log Analitica](log-analytics-search-reference.md) tooview tutti hello cerca i campi e facet disponibile nel Log Analitica.
