---
title: riferimenti di ricerca Log Analitica aaaAzure | Documenti Microsoft
description: "riferimento di ricerca Log Analitica Hello descrive il linguaggio di ricerca hello e fornisce le opzioni di sintassi di query generale hello che è possibile utilizzare quando si ricercano dati e filtro espressioni toohelp restringere la ricerca."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 402615a2-bed0-4831-ba69-53be49059718
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7478a1139b88a1ce76ebb7b76027a6ccd66f4f27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-search-reference"></a>Guida di riferimento alla ricerca in Log Analytics

>[!NOTE]
> Questo articolo descrive l'utilizzo del linguaggio di query corrente hello in Log Analitica ricerche nei log.  Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi è consigliabile consultare troppo[hello riferimenti al linguaggio per il nuovo linguaggio di hello](https://go.microsoft.com/fwlink/?linkid=856079).

Hello seguente sezione di riferimento sul linguaggio di ricerca vengono descritte le opzioni di sintassi di query generale hello che è possibile utilizzare quando si ricercano dati e filtro espressioni toohelp restringere la ricerca. Vengono inoltre descritti i comandi che è possibile utilizzare l'azione tootake hello dati recuperati.

Informazioni sui campi hello restituiti nelle ricerche e facet hello che consentono di individuare informazioni sulle categorie di dati, in hello simili [sezione fanno riferimento a campo di ricerca e ai facet](#search-field-and-facet-reference).

## <a name="general-query-syntax"></a>Sintassi di query generale
sintassi di Hello per le query generale è il seguente:

```
filterExpression | command1 | command2 …
```

espressione di filtro Hello (`filterExpression`) definisce hello condizione "where" per hello query. i comandi di Hello applicano toohello risultati restituiti dalla query hello. Più comandi devono essere separati dal carattere di barra verticale hello (|).

### <a name="general-syntax-examples"></a>Esempi di sintassi generale
Esempi:

```
system
```

Questa query restituisce risultati che contengono la parola hello *sistema* in qualsiasi campo che è stato indicizzato per full-text o le condizioni di ricerca.

> [!NOTE]
> Non tutti i campi sono indicizzati in questo modo, ma sono hello più comune in genere i campi testuali (ad esempio nomi e descrizioni).
>
>

```
system error
```

Questa query restituisce risultati che contengono parole hello *sistema* e *errore*.

```
system error | sort ManagementGroupName, TimeGenerated desc | top 10
```

Questa query restituisce risultati che contengono parole hello *sistema* e *errore*. Quindi ordina i risultati di hello da hello *ManagementGroupName* campo (in ordine crescente) e quindi per hello *TimeGenerated* campo (in ordine decrescente). Sono necessari solo hello primi 10 risultati.

> [!IMPORTANT]
> Tutti i nomi dei campi di hello e i valori dei campi di stringa e testo hello hello sono tra maiuscole e minuscole.
>
>

## <a name="filter-expressions"></a>Espressioni filtro
Hello sottosezioni seguenti illustrano le espressioni di filtro hello.

### <a name="string-literals"></a>Valori letterali stringa
Un valore letterale stringa è qualsiasi stringa non riconosciuta dal parser hello come una parola chiave o un tipo di dati predefiniti (ad esempio, un numero o data).

Esempi:

```
These all are string literals
```

Questa query cerca i risultati che contengono occorrenze di tutte le cinque parole. tooperform Cerca una stringa complessa, racchiudere stringa hello letterale tra virgolette. ad esempio:

```
"Windows Server"
```

Restituisce solo i risultati con corrispondenze esatte per *Windows Server*.

### <a name="numbers"></a>Numeri
parser di Hello supporta integer decimale hello e sintassi di numeri a virgola mobile per i campi numerici.

Esempi:

```
Type:Perf 0.5
```

```
HTTP 500
```

### <a name="dates-and-times"></a>Date e ore
Tutti i dati nel sistema hello ha un *TimeGenerated* proprietà, che rappresenta la data di hello originale e l'ora del record di hello. Alcuni tipi di dati possono inoltre avere campi di data e ora aggiuntivi, ad esempio *LastModified*.

sequenza temporale di Hello **grafico/ora** selettore in Azure Log Analitica Mostra una distribuzione dei risultati nel tempo (secondo toohello query corrente in esecuzione). Si basa su hello *TimeGenerated* campo. I campi di data e ora hanno un formato di stringa specifico che può essere utilizzato in query toorestrict hello query tooa determinato intervallo di tempo. È anche possibile utilizzare la sintassi toorefer toorelative gli intervalli di tempo (ad esempio, "tra 3 giorni fa e 2 ore fa").

di seguito Hello sono formati validi di sintassi per date e ore:

```
yyyy-mm-ddThh:mm:ss.dddZ
```

```
yyyy-mm-ddThh:mm:ss.ddd
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm
```

```
yyyy-mm-dd
```


ad esempio:

```
TimeGenerated:2013-10-01T12:20
```

comando precedente Hello restituisce solo i record con un *TimeGenerated* valore esattamente 12:20 del 1 ottobre 2013.

Hello parser supporta anche valore di data e ora mnemonico hello, NOW. (È improbabile che verrà restituito alcun risultato, quanto i dati non tramite sistema hello così velocemente.)

Questi esempi sono blocchi predefiniti toouse per le date relative e assolute. In hello tre sezioni successive, verrà visualizzato come toouse in più avanzate, filtri, con esempi che usano intervalli di date relative.

### <a name="datetime-math"></a>Operatori matematici di data/ora
Utilizzare toooffset di operatori matematici di data/ora hello o arrotondare il valore di data/ora hello, usando semplici calcoli di data/ora.

Sintassi:

```
datetime/unit
```

```
datetime[+|-]count unit
```

| Operatore | Descrizione |
| --- | --- |
| / |Arrotonda data/ora toohello specificate unit. Ad esempio, ora / DAY Arrotonda hello toomidnight di data/ora corrente di hello giorno corrente. |
| + o - |Offset di data/ora da hello specificato numero di unità. Ad esempio, NOW + 1HOUR esegue l'offset corrente di hello data/ora con un'ora avanti. 2013-10-01T12:00-10DAYS compensa il valore di data hello indietro di 10 giorni. |

È possibile concatenare gli operatori matematici di data/ora hello. ad esempio:

```
NOW+1HOUR-10MONTHS/MINUTE
```

Hello tabella seguente sono elencate le unità di data/ora hello è supportato.

| Unità di data/ora | Descrizione |
| --- | --- |
| YEAR, YEARS |Arrotonda toocurrent anno o offset da hello numero specificato di anni. |
| MONTH, MONTHS |Arrotonda toocurrent mese o offset da hello numero specificato di mesi. |
| DAY, DAYS, DATE |Arrotonda toocurrent giorno mese hello o offset da hello specificato numero di giorni. |
| HOUR, HOURS |Arrotonda toocurrent ora o offset da hello numero specificato di ore. |
| MINUTE, MINUTES |Arrotonda toocurrent minuto o offset da hello numero specificato di minuti. |
| SECOND, SECONDS |Viene arrotondata toocurrent secondo o compensa con hello specificato numero di secondi. |
| MILLISECOND, MILLISECONDS, MILLI, MILLIS |Specificare il numero di millisecondi millisecondo toocurrent Arrotonda o offset da hello. |

### <a name="field-facets"></a>Facet di campo
Usando i facet di campo, è possibile specificare la condizione di ricerca hello per campi specifici e i relativi valori esatti. Questo comportamento è diverso da scrivere query "testo libero" per diversi termini hello indice. Questa sintassi è già stata usata in vari esempi nei paragrafi precedenti. di seguito Hello sono esempi più complessi.

**Sintassi**

```
field:value
```

```
field=value
```

**Descrizione**

Ricerche hello hello specifico valore nel campo. il valore di Hello può essere un valore letterale stringa, numero o data e ora.

ad esempio:

```
TimeGenerated:NOW
```

```
ObjectDisplayName:"server01.contoso.com"
```

```
SampleValue:0.3
```

**Sintassi**

*field>value*

*field<value*

*field&gt;=value*

*field<=value*

*field!=value*

**Descrizione**

Fornisce i confronti.

ad esempio:

```
TimeGenerated>NOW+2HOURS
```

**Sintassi**

```
field:[from..to]
```

**Descrizione**

Fornisce il facet di intervallo.

Ad esempio:

```
TimeGenerated:[NOW..NOW+1DAY]
```

```
SampleValue:[0..2]
```

### <a name="in"></a>IN
Hello **IN** la parola chiave consente tooselect da un elenco di valori. A seconda di hello la sintassi utilizzata, questa può essere un semplice elenco di valori forniti o un elenco di valori di un'aggregazione.

Sintassi 1:

```
field IN {value1,value2,value3,...}
```

Questa sintassi consente tooinclude tutti i valori in un elenco semplice.



Esempi:

```
EventID IN {1201,1204,1210}
```

```
Computer IN {"srv01.contoso.com","srv02.contoso.com"}
```

Sintassi 2:

```
(Outer query) (Field toouse with inner query results) IN {Inner query | measure count() by (Field toosend tooouter query)} (rest  of outer query)  
```

Questa sintassi consente toocreate un'aggregazione. È quindi possibile inserire elenco hello di valori da tale aggregazione in un'altra ricerca (primaria) esterna che cerca gli eventi con tali valore. Tale scopo, racchiudere la ricerca interna hello tra parentesi graffe e inserire i risultati come possibili valori per un campo nella ricerca esterna hello utilizzando l'operatore IN hello.

Esempio di query interna: *computer attualmente privi di aggiornamenti della sicurezza* con hello query di aggregazione seguenti:

```
Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer
```    

query finale Hello che trova *tutti gli eventi di Windows per i computer attualmente privi di aggiornamenti della sicurezza* è simile al seguente hello:

```
Type=Event Computer IN {Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer}
```

### <a name="contains"></a>Contiene
Hello **Contains** la parola chiave consente toofilter per i record con un campo che contiene una stringa specificata. Viene fatta distinzione tra maiuscole e minuscole, funziona solo con campi di tipo stringa e non può includere i caratteri escape.

Sintassi:

```
field:contains("string")
```

Esempio:

```
Type:contains("Event")
```

Restituisce i record con un tipo che contiene la stringa hello "Event". Gli esempi includono **Event**, **SecurityEvent** e **ServiceFabricOperationEvent**.



### <a name="regular-expressions"></a>Espressioni regolari
È possibile specificare una condizione di ricerca per un campo con un'espressione regolare, utilizzando hello **Regex** (parola chiave). Per una descrizione completa della sintassi hello è possibile utilizzare nelle espressioni regolari, vedere [utilizzando espressioni regolari toofilter ricerche nei log nel Log Analitica](log-analytics-log-searches-regex.md).

Sintassi:

```
field:Regex("Regular Expression")
```

Esempio:

```
Computer:Regex("^C.*")
```

### <a name="logical-operators"></a>Operatori logici
query Hello linguaggi supportano gli operatori logici hello (*AND*, *o*, e *non*) e i relativi alias di tipo C (*&&*,  *||* , e *!*, rispettivamente). È possibile utilizzare le parentesi toogroup questi operatori.

Esempi:

```
system OR error

```

```
Type:Alert AND NOT(Severity:1 OR ObjectId:"8066bbc0-9ec8-ca83-1edc-6f30d4779bcb8066bbc0-9ec8-ca83-1edc-6f30d4779bcb")
```

È possibile omettere l'operatore logico di hello per gli argomenti di filtro di primo livello hello. In questo caso, viene usato hello operatore AND.

| Espressione di filtro | Equivalente troppo|
| --- | --- |
| system error |system AND error |
| system "Windows Server" OR Severity:1 |system AND ("Windows Server" OR Severity:1) |

### <a name="wildcarding"></a>Utilizzo dei caratteri jolly
il linguaggio di query Hello supporta l'utilizzo di hello ( \* ) carattere troppo rappresentano uno o più caratteri per un valore in una query.

Esempio:

 Trovare tutti i computer con "SQL" nel nome hello, ad esempio "Redmond-SQL".

```
Type=Event Computer=*SQL*
```

> [!NOTE]
> I caratteri jolly attualmente non possono essere usati tra virgolette, Ad esempio, il messaggio hello `"*This text*"` considera hello (\*) utilizzato come valore letterale (\*) caratteri.


## <a name="commands"></a>Comandi:


i comandi di Hello applicano toohello risultati restituiti dalla query hello. Utilizzare hello pipe (|) carattere tooapply toohello un comando recuperare risultati. Più comandi devono essere separati dal carattere barra verticale hello.

> [!NOTE]
> I nomi dei comandi possono essere scritti in lettere maiuscole o minuscole, a differenza dei nomi di campo hello e dati di hello.
>
>

### <a name="sort"></a>Ordina
Sintassi:

    sort field1 asc|desc, field2 asc|desc, …

Ordina risultati in base a determinati campi hello. risultati di Hello asc/desc suffisso toosort hello in ordine crescente o decrescente è facoltativo. Se viene omesso, hello *asc* viene usato l'ordinamento. Per hello **TimeGenerated** campo *desc* si presuppone che l'ordinamento, in modo che restituisca risultati più recenti hello innanzitutto per impostazione predefinita.

### <a name="toplimit"></a>Top/Limit
Sintassi:

    top number


    limit number
Limiti hello risposta toohello primi N risultati.

Esempio:

    Type:Alert errors detected | top 10

Restituisce hello primi 10 risultati corrispondenti.

### <a name="skip"></a>Skip
Sintassi:

    skip number

Ignora hello numero di risultati elencati.

Esempio:

    Type:Alert errors detected | top 10 | skip 200

Restituisce i primi 10 risultati corrispondenti a partire dal risultato 200.

### <a name="select"></a>Selezionare
Sintassi:

    select field1, field2, ...

Limita i campi dei risultati toohello che prescelto.

Esempio:

    Type:Alert errors detected | select Name, Severity

Limiti hello campi dei risultati restituiti troppo*nome* e *gravità*.

### <a name="measure"></a>Measure
Hello *misura* comando è risultati di ricerca non elaborati toohello funzioni statistiche tooapply utilizzato. Questo è molto utile tooget *group by* visualizzazioni sui dati hello. Quando si utilizza il comando di measure hello, ricerca Log Analitica Visualizza una tabella con risultati aggregati.

**Sintassi:**

    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]] by groupField1 [, groupField2 [, groupField3]]  [interval interval]


    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]]  interval interval



Consente di aggregare i risultati di hello da *groupField*e calcola i valori di misura aggregato hello tramite *aggregatedField*.

| Funzione statistica di measure | Descrizione |
| --- | --- |
| *aggregateFunction* |nome Hello hello della funzione di aggregazione (distinzione tra maiuscole e minuscole). Hello seguenti funzioni di aggregazione è supportata: COUNT, MAX, MIN, SUM, AVG, STDDEV, COUNTDISTINCT, PERCENTILE # # o PCT # # (# # è un numero compreso tra 1 e 99). |
| *aggregatedField* |campo Hello da aggregare. Questo campo è facoltativo per hello funzione di aggregazione COUNT, ma ha toobe un campo numerico esistente per SUM, MAX, MIN, AVG, STDDEV, PERCENTILE # # o PCT # # (# # è un numero compreso tra 1 e 99). può anche essere qualsiasi di hello Hello aggregatedField **Estendi** funzionalità supportate. |
| *fieldAlias* |valore dell'alias per hello calcolato aggregato Hello (facoltativo). Se non specificato, il nome del campo hello è **AggregatedValue**. |
| *groupField* |nome Hello del campo del set di risultati hello hello viene raggruppato. |
| *Interval* |intervallo di tempo Hello in formato hello:**nnnNAME**. **nnn**è numero intero positivo hello. **NOME** è hello nome dell'intervallo. I nomi di intervallo supportati fanno tra maiuscole e minuscole e includono: MILLISECOND[S] SECOND[S] MINUTE[S] HOUR[S] DAY[S] MONTH[S] e YEAR[S]. |

opzione Intervallo Hello può essere usata solo nei campi del gruppo data/ora (ad esempio *TimeGenerated* e *TimeCreated*). Attualmente, questo non viene applicato dal servizio hello, ma un campo senza data/ora passato toohello back-end causa un errore di runtime. Quando viene implementata la convalida dello schema di hello, hello API del servizio rifiuta le query che usano campi senza data/ora per l'aggregazione di intervalli. Hello corrente *misura* implementazione supporta il raggruppamento di intervallo per qualsiasi funzione di aggregazione.

Se hello BY viene omessa, ma viene specificato un intervallo (come una seconda sintassi), hello *TimeGenerated* campo viene utilizzato per impostazione predefinita.

Esempi:

**Esempio 1**

    Type:Alert | measure count() as Count by ObjectId

Gruppi di hello avvisi da *ObjectID*e calcola il numero di hello di avvisi per ogni gruppo. Hello valore aggregato viene restituito come hello *conteggio* campo (alias).

**Esempio 2**

    Type:Alert | measure count() interval 1HOUR

Gruppi di hello gli avvisi per intervalli di 1 ora tramite hello *TimeGenerated* campo e restituisce il numero di avvisi in ogni intervallo hello.

**Esempio 3**

    Type:Alert | measure count() as AlertsPerHour interval 1HOUR

Esempio hello precedente, ma con un alias del campo aggregato (*AlertsPerHour*).

**Esempio 4**

    * | measure count() by TimeCreated interval 5DAYS

Raggruppa i risultati di hello per intervalli di 5 giorni tramite hello *TimeCreated* campo e restituisce il numero di risultati in ogni intervallo hello.

**Esempio 5**

    Type:Alert | measure max(Severity) by WorkflowName

Gruppi di hello avvisi in base al nome del carico di lavoro e restituisce il valore di gravità massima degli avvisi per ogni flusso di lavoro di hello.

**Esempio 6**

    Type:Alert | measure min(Severity) by WorkflowName

Esempio hello precedente, ma con hello *min* funzione di aggregazione.

**Esempio 7**

    Type:Perf | measure avg(CounterValue) by Computer

Gruppi di prestazioni dal computer e calcola hello Media (avg).

**Esempio 8**

    Type:Perf | measure sum(CounterValue) by Computer

Identico hello esempio precedente, ma usa *somma*.

**Esempio 9**

    Type:Perf | measure stddev(CounterValue) by Computer

Identico hello esempio precedente, ma usa *stddev*.

**Esempio 10**

    Type:Perf | measure percentile70(CounterValue) by Computer

Identico hello esempio precedente, ma usa *percentile70*.

**Esempio 11**

    Type:Perf | measure pct70(CounterValue) by Computer

Identico hello esempio precedente, ma usa *pct70*. Notare che *PCT##* è solo un alias per la funzione *PERCENTILE##*.

**Esempio 12**

    Type:Perf | measure avg(CounterValue) by Computer, CounterName

Gruppi prima di prestazioni dal Computer e quindi CounterName calcola hello Media (avg).

**Esempio 13**

    Type:Alert | measure count() as Count by WorkflowName | sort Count desc | top 5

Ottiene hello primi cinque flussi di lavoro con il numero massimo di hello degli avvisi.

**Esempio 14**

    * | measure countdistinct(Computer) per tipo

Conta il numero di hello di computer univoci per ogni tipo.

**Esempio 15**

    * | measure countdistinct(Computer) Interval 1HOUR

Conta il numero di hello di computer univoci per ogni ora.

**Esempio 16**

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total” | measure avg(CounterValue) by Computer Interval 1HOUR
```

Raggruppa % tempo processore per Computer e restituisce la media hello per ogni ora.

**Esempio 17**

    Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES

Raggruppa W3CIISLog dal metodo e restituisce hello massima per ogni 5 minuti.

**Esempio 18**

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer Interval 1HOUR
```

Gruppi % tempo processore per computer e restituisce hello minima, Media, percentile 75th e massima per ogni ora.

**Esempio 19**

```
Type:Perf CounterName=”% Processor Time”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer, InstanceName Interval 1HOUR
```

Gruppi % tempo processore prima per computer e quindi per percentile 75th istanza il nome e restituisce hello minima, Media e massima per ogni ora.

**Esempio 20**

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | measure max(product(CounterValue,60)) as MaxDWPerMin by InstanceName Interval 1HOUR
```

Calcola il massimo hello di scritture su disco al minuto per ogni disco nel computer in uso.

### <a name="where"></a>Where
Sintassi:

```
**where** AggregatedValue>20
```

Può essere usata solo dopo un *misura* hello di filtro toofurther comando aggregato comporta che hello *misura* prodotti dalla funzione di aggregazione.

Esempi:

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) as MAXCPU by Computer

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) by Computer | where (AggregatedValue>50 and AggregatedValue<90)



### <a name="dedup"></a>Dedup
Sintassi:

    Dedup FieldName

Restituisce hello primo documento trovato per ogni valore univoco di hello campo specificato.

Esempio:

    Type=Event | Dedup EventID | sort TimeGenerated DESC

Questo esempio viene restituito un evento (evento più recente di hello) per ogni ID evento.

### <a name="join"></a>Join
Join hello risultati di due query tooform un singolo set di risultati.  Supporta più tipi di join è descritto in hello seguire una tabella.

| Tipo di join | Descrizione |
|:--|:--|
| interno | Consente di restituire solo i record con un valore corrispondente in entrambe le query. |
| esterno | Consente di restituire tutti i record da entrambe le query.  |
| sinistro  | Consente di restituire tutti i record da query a sinistra e i record corrispondenti da query a destra. |


- Join non supportano le query che includono hello **IN** (parola chiave), hello **misura** comando o hello **Estendi** comando se è destinato a un campo di query a destra hello.
- Attualmente, è possibile includere solo un singolo campo in un join.
- Una singola ricerca non può includere più di un join.

**Sintassi**

```
<left-query> | JOIN <join-type> <left-query-field-name> (<right-query>) <right-query-field-name>
```

**esempi**

tipi di join diverse tooillustrate hello, prendere in considerazione l'aggiunta di un tipo di dati raccolti da un log personalizzato denominato MyBackup_CL heartbeat hello per ogni computer.  Questi tipi di dati hanno hello dati seguenti.

`Type = MyBackup_CL`

| TimeGenerated | Computer | LastBackupStatus |
|:---|:---|:---|
| 4/20/2017 01:26:32.137 AM | srv01.contoso.com | Success |
| 4/20/2017 02:13:12.381 AM | srv02.contoso.com | Success |
| 4/20/2017 02:13:12.381 AM | srv03.contoso.com | Esito negativo |

`Type = Hearbeat` (solo un sottoinsieme dei campi visualizzati)

| TimeGenerated | Computer | ComputerIP |
|:---|:---|:---|
| 4/21/2017 12:01:34.482 PM | srv01.contoso.com | 10.10.100.1 |
| 4/21/2017 12:02:21.916 PM | srv02.contoso.com | 10.10.100.2 |
| 4/21/2017 12:01:47.373 PM | srv04.contoso.com | 10.10.100.4 |

#### <a name="inner-join"></a>join interno

`Type=MyBackup_CL | join inner Computer (Type=Heartbeat) Computer`

Restituisce i seguenti record in cui corrisponda al campo del computer hello per entrambi tipi di dati hello.

| Computer| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| srv01.contoso.com | 4/20/2017 01:26:32.137 AM | Success | 4/21/2017 12:01:34.482 PM | 10.10.100.1 | Heartbeat |
| srv02.contoso.com | 4/20/2017 02:13:12.381 AM | Success | 4/21/2017 12:02:21.916 PM | 10.10.100.2 | Heartbeat |


#### <a name="outer-join"></a>join esterno

`Type=MyBackup_CL | join outer Computer (Type=Heartbeat) Computer`

Restituisce i seguenti record per entrambi tipi di dati hello.

| Computer| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| srv01.contoso.com | 4/20/2017 01:26:32.137 AM | Success  | 4/21/2017 12:01:34.482 PM | 10.10.100.1 | Heartbeat |
| srv02.contoso.com | 4/20/2017 02:14:12.381 AM | Success  | 4/21/2017 12:02:21.916 PM | 10.10.100.2 | Heartbeat |
| srv03.contoso.com | 4/20/2017 01:33:35.974 AM | Esito negativo  | 4/21/2017 12:01:47.373 PM | | |
| srv04.contoso.com |                           |          | 4/21/2017 12:01:47.373 PM | 10.10.100.2 | Heartbeat |



#### <a name="left-join"></a>join sinistro

`Type=MyBackup_CL | join left Computer (Type=Heartbeat) Computer`

Restituisce i seguenti record da MyBackup_CL con tutti i campi corrispondenti da Heartbeat hello.

| Computer| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| srv01.contoso.com | 4/20/2017 01:26:32.137 AM | Success | 4/21/2017 12:01:34.482 PM | 10.10.100.1 | Heartbeat |
| srv02.contoso.com | 4/20/2017 02:13:12.381 AM | Success | 4/21/2017 12:02:21.916 PM | 10.10.100.2 | Heartbeat |
| srv03.contoso.com | 4/20/2017 02:13:12.381 AM | Esito negativo | | | |


### <a name="extend"></a>Extend
Consente di campi toocreate in fase di esecuzione delle query. Si noti che i campi di runtime possono essere utilizzati con l'aggregazione di tooperform comando misura hello.

**Esempio 1**

    Type=SQLAssessmentRecommendation | Extend product(RecommendationScore, RecommendationWeight) AS RecommendationWeightedScore
Visualizza il punteggio delle raccomandazioni ponderato per le raccomandazioni di SQL Assessment.

**Esempio 2**

    Type=Perf CounterName="Private Bytes" | EXTEND div(CounterValue,1024) AS KBs | Select CounterValue,Computer,KBs
Visualizza il valore del contatore in KB invece che in byte.

**Esempio 3**

    Type=WireData | EXTEND scale(TotalBytes,0,100) AS ScaledTotalBytes | Select ScaledTotalBytes,TotalBytes | SORT TotalBytes DESC
Scale hello valore di WireData TotalBytes, in modo che tutti i risultati siano compresi tra 0 e 100.

**Esempio 4**

```
Type=Perf CounterName="% Processor Time" | EXTEND if(map(CounterValue,0,50,0,1),"HIGH","LOW") as UTILIZATION
```
Contrassegna i valori del contatore prestazioni inferiori al 50% come LOW e gli altri come HIGH.

**Esempio 5**

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | Extend product(CounterValue,60) as DWPerMin| measure max(DWPerMin) by InstanceName Interval 1HOUR
```
Calcola il massimo hello di scritture su disco al minuto per ogni disco nel computer in uso.

**Funzioni supportate**

| Funzione | Descrizione | Esempi di sintassi |
| --- | --- | --- |
| abs |Restituisce il valore assoluto hello di hello specificato valore o funzione. |`abs(x)` <br> `abs(-5)` |
| acos |Restituisce l'arcocoseno di un valore o una funzione. |`acos(x)` |
| e |Restituisce un valore true se e solo se tutti gli operandi restituiscono tootrue. |`and(not(exists(popularity)),exists(price))` |
| asin |Restituisce l'arcoseno di un valore o una funzione. |`asin(x)` |
| atan |Restituisce l'arco tangente di un valore o una funzione. |`atan(x)` |
| atan2 |Restituisce l'angolo di hello risultante dalla conversione hello di coordinate rettangolari hello coordinate x, y toopolar. |`atan2(x,y)` |
| cbrt |Radice cubica. |`cbrt(x)` |
| ceil |Arrotonda tooan intero. |`ceil(x)`  <br> `ceil(5.6)`: restituisce il valore 6 |
| cos |Restituisce il coseno di un angolo. |`cos(x)` |
| cosh |Restituisce il coseno iperbolico di un angolo. |`cosh(x)` |
| def |Abbreviazione di default. Restituisce hello valore del campo "field". Se il campo hello non esiste, restituisce il valore predefinito hello specificato e restituisce hello primo valore in cui: `exists()==true`. |`def(rating,5)`. Questa funzione def() restituisce classificazione hello oppure se non viene specificata alcuna classificazione nel documento hello, 5. <br> `def(myfield, 1.0)`è equivalente troppo`if(exists(myfield),myfield,1.0)`. |
| deg |Converte i radianti toodegrees. |`deg(x)` |
| div |`div(x,y)` divide x per y. |`div(1,y)` <br> `div(sum(x,100),max(y,1))` |
| dist |Restituisce la distanza hello tra due vettori (punti) in uno spazio n-dimensionale. Accetta power hello, più due o più, istanze ValueSource e calcola le distanze tra due vettori di hello hello. Ogni ValueSource deve essere un numero. Deve esistere un numero pari di istanze ValueSource passate e il metodo hello si presuppone che hello prima metà rappresenti il primo vettore di hello e hello seconda metà rappresenti secondo vettore hello. |`dist(2, x, y, 0, 0)`Calcola hello distanza euclidea tra (0,0) e (x, y) per ogni documento. <br> `dist(1, x, y, 0, 0)`Calcola hello distanza di Manhattan (geometria del taxi) tra (0,0) e (x, y) per ogni documento. <br> `dist(2,,x,y,z,0,0,0)`: distanza euclidea tra (0,0,0) e (x,y,z) per ogni documento.<br>`dist(1,x,y,z,e,f,g)`: distanza di Manhattan tra (x,y,z) e (e,f,g), dove ogni lettera è un nome di campo. |
| exists |Restituisce TRUE se uno qualsiasi di campo hello esiste membro. |`exists(author)`Restituisce TRUE per qualsiasi documento che ha un valore nel campo "author" hello.<br>`exists(query(price:5.00))`: restituisce TRUE se "price" corrisponde a "5.00". |
| exp |Il numero di Eulero restituisce generato toopower x. |`exp(x)` |
| floor |Arrotonda per difetto tooan integer. |`floor(x)`  <br> `floor(5.6)`: restituisce il valore 5 |
| hypo |Restituisce sqrt(sum(pow(x,2),pow(y,2))) senza overflow o underflow intermedi. |`hypo(x,y)`  <br> ` |
| if |Abilita le query funzione condizionali. In `if(test,value1,value2)`, test oppure che faccia riferimento valore logico tooa o un'espressione che restituisce un valore logico (TRUE o FALSE). `value1`è il valore di hello restituito dalla funzione hello se test restituisce TRUE. `value2`è il valore di hello restituito dalla funzione hello se test restituisce FALSE. Un'espressione può essere una funzione che restituisce valori booleani o anche una funzione che restituisce valori numerici, nel qual caso il valore 0 verrà interpretato come false, oppure stringhe, nel qual caso una stringa vuota viene interpretata come false. |`if(termfreq(cat,'electronics'),popularity,42)`Questa funzione controlla ogni toosee documento se contiene hello termine "electronics" nel campo cat hello. Se quindi, hello valore del campo popolarità hello. In caso contrario, viene restituito il valore di hello 42. |
| linear |Implementa `m*x+c` dove m e c sono costanti e x è una funzione arbitraria. Ciò equivale troppo`sum(product(m,x),c)`, ma lievemente più efficiente perché viene implementata come una singola funzione. |`linear(x,m,c) linear(x,2,4)` restituisce `2*x+4` |
| ln |Logaritmo naturale di hello restituisce di hello funzione specificata. |`ln(x)` |
| log |Restituisce hello log in base 10 di hello funzione specificata. |`log(x)   log(sum(x,100))` |
| map |Esegue il mapping di tutti i valori di una funzione di input x compresi tra min e max, inclusi toohello destinazione specificato. hello argomenti min e max devono essere costanti. valore predefinito e destinazione di hello argomenti possono essere costanti o funzioni. Se il valore di hello di x non è compreso tra min e max, viene quindi restituito il valore di hello di x oppure viene restituito un valore predefinito, se specificato come argomento di 5. |`map(x,min,max,target) map(x,0,0,1)`Modifica qualsiasi valore too1 0. Può essere utile per gestire i valori 0 predefiniti.<br> `map(x,min,max,target,default)    map(x,0,100,1,-1)`Modifica qualsiasi valore compreso tra 0 e 100 too1 e tutti gli altri valori troppo-1.<br>  `map(x,0,100,sum(x,599),docfreq(text,solr))`Modifica qualsiasi valore compreso tra 0 e 100 toox + 599 e tutti gli altri toofrequency i valori del termine 'solr' nel testo del campo hello di hello. |
| max |Restituisce un valore numerico massimo di più funzioni o costanti nidificate, che sono specificate come argomenti di hello: `max(x,y,...)`. funzione max Hello può anche essere utile per "toccare il fondo" un'altra funzione o campo in corrispondenza di una costante specificata.  Hello utilizzare `field(myfield,max)` sintassi per la selezione hello valore massimo di un singolo campo multivalore. |`max(myfield,myotherfield,0)` |
| Min |Restituisce un valore numerico minimo di più funzioni nidificate delle costanti, che sono specificate come argomenti di hello: `min(x,y,...)`. funzione min Hello può anche essere utile per fornire un "limite superiore" in una funzione che usa una costante. Hello utilizzare `field(myfield,min)` sintassi per la selezione hello valore minimo di un singolo campo multivalore. |`min(myfield,myotherfield,0)` |
| mod |Calcola il modulo hello della funzione hello x per y funzione hello. |`mod(1,x)` <br> `mod(sum(x,100), max(y,1))` |
| ms |Restituisce i millisecondi di differenza tra gli argomenti. Le date sono relativa toohello Unix o POSIX periodo di tempo, mezzanotte dell'1 gennaio 1970 ora UTC. Gli argomenti possono essere hello nome di un campo TrieDateField indicizzato o calcoli sulle date in base a una data costante o NOW. `ms()`è equivalente troppo`ms(NOW)`, numero di millisecondi trascorsi hello. `ms(a)`Restituisce il numero di hello di millisecondi trascorsi hello rappresentato hello argomento. `ms(a,b)`Restituisce il numero di hello di millisecondi che b si verifica prima, ovvero `a - b`. |`ms(NOW/DAY)`<br>`ms(2000-01-01T00:00:00Z)`<br>`ms(mydatefield)`<br>`ms(NOW,mydatefield)`<br>`ms(mydatefield,2000-01-01T00:00:00Z)`<br>`ms(datefield1,datefield2)` |
| not |il valore di Hello negato in modo logico di hello inserito (funzione). |`not(exists(author))`: TRUE solo quando `exists(author)` è false. |
| oppure |Disgiunzione logica. |`or(value1,value2)`: TRUE se value1 o value2 è true. |
| pow |Genera hello specificato toohello base specificato risparmio energia. `pow(x,y)`Genera x toohello potenza di y. |`pow(x,y)`<br>`pow(x,log(y))`<br>`pow(x,0.5)`Hello uguale a sqrt. |
| product |Restituisce hello prodotto di più valori o funzioni, che sono specificati in un elenco delimitato da virgole. `mul(...)` può essere usato anche come alias per questa funzione. |`product(x,y,...)`<br>`product(x,2)`<br>`product(x,y)`<br>`mul(x,y)` |
| recip |Esegue una funzione reciproca con `recip(x,m,a,b)` che implementa `a/(m*x+b)` dove m, a, b sono costanti e x è una funzione arbitrariamente complessa. Quando a e b sono uguali e x>=0, questa funzione ha un valore massimo di 1 che diminuisce quando x aumenta. Aumentare il valore di hello di un e b contemporaneamente provoca un movimento del tooa intera funzione hello larga parte della curva hello. Queste proprietà possono rendere questa funzione ideale per il boosting dei documenti più recenti quando x è `rord(datefield)`. |`recip(myfield,m,a,b)`<br>`recip(rord(creationDate),1,1000,1000)` |
| rad |Converte i gradi tooradians. |`rad(x)` |
| rint |Arrotonda toohello numero intero più vicino. |`rint(x)`  <br> `rint(5.6)`: restituisce il valore 6 |
| sin |Restituisce il seno di un angolo. |`sin(x)` |
| sinh |Restituisce il seno iperbolico di un angolo. |`sinh(x)` |
| scala |I valori delle scale di funzione hello x, tale che siano compresi tra hello specificato minTarget e maxTarget inclusi. implementazione di Hello corrente scorre tutti di hello funzione valori tooobtain hello min e max, per poter selezionare la scala corretta hello. implementazione di Hello corrente non distingue quando i documenti sono stati eliminati, o i documenti che non hanno alcun valore. In questi casi, usa i valori 0,0. Ciò significa che se i valori sono tutti in genere maggiori di 0,0, uno può comunque avere 0,0 come hello toomap valore min da. In questi casi, un oggetto appropriati `map()` funzione può essere utilizzata come valore di tooa soluzione toochange 0,0 nell'intervallo reale hello, come illustrato di seguito:`scale(map(x,0,0,5),1,2)` |`scale(x,minTarget,maxTarget)`<br>`scale(x,1,2)`Scale hello valori di x, in modo che tutti i valori sono compresi tra 1 e 2 inclusi. |
| sqrt |Radice quadrata di hello restituisce di hello specificato valore o funzione. |`sqrt(x)`<br>`sqrt(100)`<br>`sqrt(sum(x,100))` |
| strdist |Calcola la distanza hello tra due stringhe. Usa l'interfaccia StringDistance del correttore ortografico Lucene hello e supporta tutte le implementazioni di hello disponibili nel pacchetto. Consente inoltre alle applicazioni tooplug le proprie, con risorse di Solr funzionalità di caricamento. strdist accetta `(string1, string2, distance measure)`. I valori possibili per la misura della distanza sono: <ul><li>jw: Jaro-Winkler</li><li>modifcare: Levenstein oppure Modifica distanza</li><li>ngram: hello ngramdistance; se specificata, può passare facoltativamente dimensioni ngram hello troppo. Il valore predefinito è 2.</li><li>FQN: Nome per l'implementazione di un'interfaccia StringDistance hello classe completo. Deve avere un costruttore no-arg.</li></ul> |`strdist("SOLR",id,edit)` |
| sub |Restituisce x-y da `sub(x,y)`. |`sub(myfield,myfield2)`<br>`sub(100,sqrt(myfield))` |
| Sum |Restituisce hello somma di più valori o funzioni, che sono specificati in un elenco delimitato da virgole. `add(...)` può essere usato come alias per questa funzione. |`sum(x,y,...)`<br>`sum(x,1)`<br>`sum(x,y)`<br>`sum(sqrt(x),log(y),z,0.5)`<br>`add(x,y)` |
| termfreq |Restituisce il numero di hello di volte hello termine viene visualizzato nel campo hello per il documento. |termfreq(text,'memory') |
| tan |Restituisce la tangente di un angolo. |`tan(x)` |
| tanh |Restituisce la tangente iperbolica di un angolo. |`tanh(x)` |

## <a name="search-field-and-facet-reference"></a>Riferimenti al campo Ricerca e ai facet
Quando si utilizzano dati toofind ricerca nei Log, i risultati visualizzano vari campi e facet. Alcune delle informazioni di hello potrebbero non essere molto descrittive. Utilizzare hello seguente toohelp informazioni interpretare i risultati di hello.

| Campo | Tipo di ricerca | Descrizione |
| --- | --- | --- |
| TenantId |Tutti |Toopartition dati utilizzati. |
| TimeGenerated |Tutti |Utilizzare toodrive hello timeline, selettori orari (in ricerca e in altre schermate). Rappresenta quando i dati hello sono stati generati (in genere nell'agente hello). tempo di Hello è espressa nel formato ISO ed è sempre UTC. Nel caso di hello di tipi che sono basati sulla strumentazione esistente (eventi in un log), si tratta in genere hello tempo reale che hello voce/riga/record di log è stato registrato. Per alcune delle hello altri tipi prodotti tramite management pack o nel cloud hello (ad esempio, indicazioni o gli avvisi), hello ora rappresenta un valore diverso. Si tratta ora hello è stato raccolto questa nuova parte di dati con uno snapshot di una configurazione di qualche tipo, o un suggerimento/avviso è stato generato in base a essi. |
| EventID |Evento |EventID nel registro eventi di Windows hello. |
| EventLog |Evento |Registro eventi in cui hello è stato registrato da Windows. |
| EventLevelName |Evento |Critico/avviso/informazioni/esito positivo |
| EventLevel |Evento |Valore numerico per critico/avviso/informazioni/esito positivo; usare EventLevelName invece di query più semplici o più leggibili |
| SourceSystem |Tutti |Da cui provengono i dati di hello (in termini di connessione del servizio in modalità toohello). ad esempio Microsoft System Center Operations Manager e Archiviazione di Azure |
| ObjectName |PerfHourly |Nome oggetto delle prestazioni di Windows |
| InstanceName |PerfHourly |Nome dell'istanza del contatore delle prestazioni di Windows |
| CounteName |PerfHourly |Nome del contatore delle prestazioni di Windows |
| ObjectDisplayName |PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty |Nome visualizzato dell'oggetto hello destinata di una regola di raccolta prestazioni in Operations Manager. Potrebbe inoltre essere il nome visualizzato hello di hello oggetto individuato da Operational Insights o per la quale hello è stato generato l'avviso. |
| RootObjectName |PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty |Nome visualizzato del padre hello padre hello (in una relazione di hosting doppia) dell'oggetto hello destinata di una regola di raccolta prestazioni in Operations Manager. Potrebbe inoltre essere il nome visualizzato hello di hello oggetto individuato da Operational Insights o per la quale hello è stato generato l'avviso. |
| Computer |La maggior parte dei tipi |Nome del computer a cui appartengono i dati di hello. |
| DeviceName |ProtectionStatus |Dati hello del nome computer appartengono troppo (uguale a "Computer"). |
| DetectionId |ProtectionStatus | |
| ThreatStatusRank |ProtectionStatus |Classificazione dello stato di minaccia è una rappresentazione numerica dello stato di minaccia hello. Codici di risposta tooHTTP simile, rango hello è presenti gap tra i numeri di hello (motivo per cui nessuna minaccia è 150, non 100 o 0), lasciando spazio sufficiente tooadd nuovi Stati. Per un rollup dello stato di minaccia e lo stato di protezione, l'intenzione di hello è tooshow hello stato peggiore in cui hello computer è rimasto durante il periodo di tempo selezionato hello. numeri di Hello classificare hello diversi stati, pertanto è possibile cercare il record di hello con numero più alto hello. |
| ThreatStatus |ProtectionStatus |Descrizione di ThreatStatus, viene eseguito il mapping 1:1 con ThreatStatusRank |
| TypeofProtection |ProtectionStatus |Prodotti antimalware rilevato nel computer di hello: Nessuno, strumento di rimozione Malware Microsoft, Forefront e così via. |
| ScanDate |ProtectionStatus | |
| SourceHealthServiceId |ProtectionStatus, RequiredUpdate |ID servizio di integrità per l'agente del computer |
| HealthServiceId |La maggior parte dei tipi |ID servizio di integrità per l'agente del computer |
| ManagementGroupName |La maggior parte dei tipi |Nome del gruppo di gestione per gli agenti di Operations Manager. In caso contrario, è null o vuoto. |
| ObjectType |ConfigurationObject |Tipo (come nel "tipo" o nella classe del Management Pack di Operations Manager) per l'oggetto individuato dalla valutazione della configurazione di Log Analytics |
| UpdateTitle |RequiredUpdate |Nome di hello aggiornamento trovato non installato. |
| PublishDate |RequiredUpdate |Aggiornamento di hello quando è stata pubblicata in Microsoft Update. |
| Server |RequiredUpdate |Dati hello del nome computer appartengono troppo (uguale a "Computer"). |
| Prodotto |RequiredUpdate |Prodotto hello aggiornamento si applica a. |
| UpdateClassification |RequiredUpdate |Tipo di aggiornamento, ad esempio rollup aggiornamento, Service Pack |
| KBID |RequiredUpdate |ID articolo della KB che descrive la procedura consigliata o l'aggiornamento |
| WorkflowName |ConfigurationAlert |Nome della regola hello o un monitoraggio che ha generato hello avviso. |
| Severity |ConfigurationAlert |Gravità dell'avviso hello. |
| Priorità |ConfigurationAlert |Priorità di avviso hello. |
| IsMonitorAlert |ConfigurationAlert |Questo avviso viene generato da un monitoraggio (true) o da una regola (false)? |
| AlertParameters |ConfigurationAlert |XML con parametri hello dell'avviso di Log Analitica hello. |
| Context |ConfigurationAlert |XML con il contesto di hello dell'avviso di Log Analitica hello. |
| Carico di lavoro |ConfigurationAlert |Tecnologia o il carico di lavoro hello avviso fa riferimento a. |
| AdvisorWorkload |Raccomandazione |Tecnologia o il carico di lavoro hello raccomandazione fa riferimento a. |
| Descrizione |ConfigurationAlert |Descrizione dell'avviso (breve) |
| DaysSinceLastUpdate |UpdateAgent |Quanti giorni fa (relativo tooTimeGenerated di questo record) questo agente ha installato un aggiornamento da Windows Server Update Service (WSUS) o Microsoft Update? |
| DaysSinceLastUpdateBucket |UpdateAgent |In base a DaysSinceLastUpdate, una categorizzazione in "bucket orari" del tempo trascorso dall'ultima installazione di aggiornamenti da WSUS/Microsoft Update da parte di un computer |
| AutomaticUpdateEnabled |UpdateAgent |Il controllo degli aggiornamenti automatici è abilitato o disabilitato su questo agente? |
| AutomaticUpdateValue |UpdateAgent |Download tooautomatically set controllo di aggiornamento automatico e installare, solo scaricare o solo controllare? |
| WindowsUpdateAgentVersion |UpdateAgent |Numero di versione dell'agente di Microsoft Update hello. |
| WSUSServer |UpdateAgent |A quale server WSUS è destinato questo agente di aggiornamento? |
| OSVersion |UpdateAgent |Versione del sistema operativo hello questo agente di aggiornamento è in esecuzione. |
| Nome |Recommendation, ConfigurationObjectProperty |Nome/titolo della raccomandazione hello o nome della proprietà hello dalla valutazione della configurazione di Log Analitica. |
| Valore |ConfigurationObjectProperty |Valore di una proprietà di valutazione configurazione di Log Analytics |
| KBLink |Raccomandazione |Articolo KB toohello URL che descrive la procedura consigliata o l'aggiornamento. |
| RecommendationStatus |Raccomandazione |Le raccomandazioni sono tra hello pochi tipi i cui record ottenere l'indice di ricerca toohello aggiornata, non appena aggiunta. Questo stato cambia se hello raccomandazione è attiva/aperta o se Log Analitica rileva che è stato risolto. |
| RenderedDescription |Evento |Descrizione con rendering (testo riutilizzato con parametri popolati) di un evento di Windows |
| ParameterXml |Evento |XML con parametri hello nella sezione dati hello di un evento di Windows (come illustrato nel Visualizzatore eventi). |
| EventData |Evento |XML con hello intera sezione data di un evento di Windows (come illustrato nel Visualizzatore eventi). |
| Sorgente |Evento |Registro eventi di origine che ha generato l'evento hello. |
| EventCategory |Evento |Categoria di eventi di hello, direttamente dal registro eventi di Windows hello. |
| UserName |Evento |Nome utente dell'evento di Windows hello (in genere, NT AUTHORITY\LOCALSYSTEM). |
| SampleValue |PerfHourly |Valore medio per l'aggregazione oraria di hello del contatore di prestazioni. |
| Min |PerfHourly |Valore minimo nell'intervallo orario di hello di un'aggregazione oraria del contatore delle prestazioni. |
| max |PerfHourly |Valore massimo nell'intervallo orario di hello di un'aggregazione oraria del contatore delle prestazioni. |
| Percentile95 |PerfHourly |Hello valore 95 ° percentile per l'intervallo orario di hello di un'aggregazione oraria del contatore delle prestazioni. |
| SampleCount |PerfHourly |Il numero di campioni del contatore delle prestazioni non elaborati sono stati utilizzati tooproduce questo orario aggregare i record. |
| Threat |ProtectionStatus |Nome del malware rilevato |
| StorageAccount |W3CIISLog |Azure log hello account di archiviazione è stato letto da. |
| AzureDeploymentID |W3CIISLog |ID di distribuzione di Azure di log di hello hello cloud servizio a cui appartiene. |
| Ruolo |W3CIISLog |Ruolo del log di hello servizio cloud di Azure hello a cui appartiene. |
| RoleInstance |W3CIISLog |Istanza del ruolo di Azure che hello log hello a cui appartiene. |
| sSiteName |W3CIISLog |Sito Web IIS che hello log appartiene too(metabase notation); campo s-sitename Hello nel log originale hello. |
| sComputerName |W3CIISLog |campo s-computername Hello nel log originale hello. |
| sIP |W3CIISLog |Richiesta HTTP hello indirizzo IP del server è stato risolto per. campo s-ip Hello nel log originale hello. |
| csMethod |W3CIISLog |Metodo HTTP (ad esempio, GET/POST) usato dal client di hello nella richiesta HTTP hello. Hello metodo cs nel log originale hello. |
| cIP |W3CIISLog |Provenienza della richiesta HTTP hello indirizzo IP del client. campo c-ip Hello nel log originale hello. |
| csUserAgent |W3CIISLog |Agente utente HTTP dichiarato dal client hello (browser o in caso contrario). Hello cs-user-agent nel log originale hello. |
| scStatus |W3CIISLog |Codice di stato HTTP (ad esempio 200/403/500) restituito dal client di toohello server hello. Hello stato cs nel log originale hello. |
| TimeTaken |W3CIISLog |La durata (in millisecondi) richiesta hello ha impiegato toocomplete. campo timetaken Hello nel log originale hello. |
| csUriStem |W3CIISLog |URI relativo (senza indirizzo host, che è '/search') che è stato richiesto. campo cs-uristem Hello nel log originale hello. |
| csUriQuery |W3CIISLog |Query dell'URI. Le query dell'URI sono necessarie solo per le pagine dinamiche, ad esempio le pagine ASP, per cui questo campo contiene in genere un trattino per le pagine statiche. |
| sPort |W3CIISLog |Porta del server che hello richiesta HTTP è stata inviata troppo (e in cui IIS è in ascolto, dopo averla scelta). |
| csUserName |W3CIISLog |Nome dell'utente, può essere autenticato se hello richiesta è autenticata e non anonima. |
| csVersion |W3CIISLog |Versione del protocollo HTTP usato nella richiesta di hello (ad esempio, HTTP/1.1). |
| csCookie |W3CIISLog |Informazioni sui cookie |
| csReferer |W3CIISLog |Il sito che l'utente hello ha visitato per ultimo. Questo sito fornisce un collegamento toohello corrente sito. |
| csHost |W3CIISLog |Intestazione host richiesta, ad esempio www.mysite.com |
| scSubStatus |W3CIISLog |Codice errore dello stato secondario. |
| scWin32Status |W3CIISLog |Codice di stato Windows. |
| csBytes |W3CIISLog |Byte inviati nella richiesta hello dal server di toohello hello client. |
| scBytes |W3CIISLog |Byte restituiti nella risposta hello del client di toohello server hello. |
| ConfigChangeType |ConfigurationChange |Tipo di modifica, ad esempio WindowsServices/Software |
| ChangeCategory |ConfigurationChange |Categoria della modifica hello (Modified/Added/Removed). |
| SoftwareType |ConfigurationChange |Tipo di software (Aggiornamento/Applicazione) |
| SoftwareName |ConfigurationChange |Nome del software hello (solo modifiche toosoftware applicabile). |
| Autore |ConfigurationChange |Fornitore che pubblica il software di hello (solo modifiche toosoftware applicabile). |
| SvcChangeType |ConfigurationChange |Tipo di modifica applicata a un servizio Windows (Stato/Tipo avvio/Percorso/Account servizio) Si tratta solo le modifiche di servizio tooWindows applicabile. |
| SvcDisplayName |ConfigurationChange |Nome visualizzato del servizio hello che è stato modificato. |
| SvcName |ConfigurationChange |Nome del servizio hello che è stato modificato. |
| SvcState |ConfigurationChange |Stato nuovo (corrente) del servizio hello. |
| SvcPreviousState |ConfigurationChange |Stato precedente noto del servizio di hello (applicabile solo se lo stato del servizio modificato). |
| SvcStartupType |ConfigurationChange |Tipo di servizio di avvio |
| SvcPreviousStartupType |ConfigurationChange |Tipo di avvio del servizio precedente (applicabile solo se il tipo di avvio del servizio è stato modificato) |
| SvcAccount |ConfigurationChange |Account del servizio |
| SvcPreviousAccount |ConfigurationChange |Account del servizio precedente (applicabile solo se l'account del servizio è stato modificato) |
| SvcPath |ConfigurationChange |File eseguibile toohello di percorso del servizio di Windows hello. |
| SvcPreviousPath |ConfigurationChange |Percorso precedente dell'eseguibile per il servizio Windows (applicabile solo se è stato modificato) hello hello. |
| SvcDescription |ConfigurationChange |Descrizione del servizio hello. |
| Precedente |ConfigurationChange |Stato precedente del software (Installato/Non installato/versione precedente) |
| Current |ConfigurationChange |Ultimo stato del software (Installato/Non installato/versione corrente) |

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sulle ricerche nei log:

* Acquisire familiarità con [log ricerche](log-analytics-log-searches.md) tooview dettagliate informazioni raccolte da soluzioni.
* Utilizzare [campi personalizzati nel registro Analitica](log-analytics-custom-fields.md) tooextend ricerche nei log.
