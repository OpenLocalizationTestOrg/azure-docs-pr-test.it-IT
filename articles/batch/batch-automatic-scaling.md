---
title: scala aaaAutomatically nodi di calcolo in un pool di Azure Batch | Documenti Microsoft
description: "Abilitare la scalabilità automatica in un toodynamically pool cloud regolare il numero di hello di nodi di calcolo nel pool di hello."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: tysonn
ms.assetid: c624cdfc-c5f2-4d13-a7d7-ae080833b779
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: multiple
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6d1e0c5d8e0e56e15a4d3588150f2466a689f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-automatic-scaling-formula-for-scaling-compute-nodes-in-a-batch-pool"></a>Creare una formula di scalabilità automatica per la scalabilità dei nodi di calcolo in un pool Batch

Azure Batch supporta la scalabilità automatica dei pool in base ai parametri definiti. Con il ridimensionamento automatico, Batch consente di aggiungere in modo dinamico i nodi tooa pool come attività aumento della richiesta e rimuove i nodi di calcolo come riducono. È possibile salvare tempo e denaro modificando automaticamente il numero di hello dei nodi di calcolo utilizzato dall'applicazione di Batch. 

Per abilitare la scalabilità automatica in un pool di nodi di calcolo, definire e associare al pool una *formula di scalabilità automatica*. Hello servizio Batch Usa numero di hello toodetermine formula di scalabilità automatica hello dei nodi di calcolo che sono necessari tooexecute il carico di lavoro. I nodi di calcolo possono essere nodi dedicati o [nodi con priorità bassa](batch-low-pri-vms.md). I dati di metrica tooservice raccolti periodicamente di risposta batch. Utilizza i dati di metrica, Batch regola numero hello dei nodi di calcolo nel pool di hello in base a intervalli configurabili e formule.

È possibile abilitare la scalabilità automatica al momento della creazione di un pool o in un pool esistente. Si può anche modificare una formula esistente in un pool configurato per la scalabilità automatica. Batch consente tooevaluate formule prima dell'assegnazione di stato di hello toopools e toomonitor di ridimensionamento automatico viene eseguito.

Questo articolo illustra hello varie entità che costituiscono le formule di scalabilità automatica, ad esempio variabili, operatori, operazioni e funzioni. Viene illustrato come tooobtain varie metriche relative a risorse e attività all'interno di Batch di calcolo. È possibile utilizzare questi tooadjust metrica conteggio dei nodi del pool in base allo stato di attività e l'utilizzo della risorsa. È quindi descrivere la modalità tooconstruct una formula e abilitare utilizzando sia la scalabilità in un pool automatico hello Batch REST e le API .NET. concludendo con alcune formule di esempio.

> [!IMPORTANT]
> Quando si crea un account Batch, è possibile specificare hello [configurazione dell'account](batch-api-basics.md#account), che determina se i pool vengono allocati in una sottoscrizione al servizio Batch (impostazione predefinita hello) o nella sottoscrizione utente. Se l'account Batch è stato creato con la configurazione di servizio Batch hello predefinita, l'account è tooa limitato il numero massimo di core che può essere utilizzato per l'elaborazione. servizio Batch Hello Ridimensiona i nodi di calcolo solo backup toothat limite di core. Per questo motivo, hello servizio Batch potrebbe non raggiungere il numero di destinazione hello dei nodi di calcolo specificata da una formula di scalabilità automatica. Vedere [quote e limiti per il servizio Azure Batch hello](batch-quota-limit.md) per informazioni sulla visualizzazione e ad aumentare le quote di account.
>
>Se l'account è stato creato con la configurazione della sottoscrizione utente hello, l'account nelle condivisioni di quota di core hello per sottoscrizione hello. Per altre informazioni, vedere [Limiti relativi a Macchine virtuali](../azure-subscription-service-limits.md#virtual-machines-limits) in [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../azure-subscription-service-limits.md).
>
>

## <a name="automatic-scaling-formulas"></a>Formule di ridimensionamento automatico
Una formula di scalabilità automatica è un valore stringa definito che contiene una o più istruzioni. formula di scalabilità automatica Hello viene assegnato del pool tooa [autoScaleFormula] [ rest_autoscaleformula] elemento (Batch REST) o [CloudPool.AutoScaleFormula] [ net_cloudpool_autoscaleformula] proprietà (.NET per Batch). Hello servizio Batch utilizza il numero di destinazione toodetermine formula hello di nodi di calcolo nel pool di hello per successivo intervallo di elaborazione di hello. formula la stringa Hello non può superare gli 8 KB, è possibile includere i rendiconti too100 che sono separati da punti e virgola e possono includere interruzioni di riga e i commenti.

È possibile paragonare le formule di ridimensionamento automatico a un "linguaggio" di ridimensionamento automatico di Batch. Le istruzioni formula sono espressioni in formato libero che possono includere sia definito dal servizio variabili (variabili definite dal servizio Batch hello) variabili definite dall'utente (variabili che definiscono). Possono eseguire diverse operazioni su questi valori usando funzioni, operatori e tipi predefiniti. Ad esempio, un'istruzione potrebbe richiedere hello seguente formato:

```
$myNewVariable = function($ServiceDefinedVariable, $myCustomVariable);
```

Le formule contengono in genere più istruzioni che eseguono operazioni su valori ottenuti nelle istruzioni precedenti. Ad esempio, prima è ottenere un valore per `variable1`, quindi passarlo tooa funzione toopopulate `variable2`:

```
$variable1 = function1($ServiceDefinedVariable);
$variable2 = function2($OtherServiceDefinedVariable, $variable1);
```

Dichiarazioni del tooarrive formula di scalabilità automatica in un numero di nodi di calcolo di destinazione. I nodi dedicati e i nodi con priorità bassa hanno impostazioni proprie per la destinazione, in modo da poter definire una destinazione per ogni tipo di nodo. Una formula di scalabilità automatica può includere un valore di destinazione per i nodi dedicati, un valore di destinazione per i nodi con priorità bassa o entrambi.

numero di destinazione Hello dei nodi potrebbe essere superiore, inferiore o uguale hello numero corrente di nodi di quel tipo nel pool di hello hello. Batch valuta la formula di scalabilità automatica del pool a intervalli specifici (vedere gli [intervalli di scalabilità automatica](#automatic-scaling-interval)). Batch consente di regolare il numero di destinazione hello di ogni tipo di nodo nel numero di toohello pool hello che specifica la formula di scalabilità automatica in fase di valutazione di hello.

### <a name="sample-autoscale-formula"></a>Esempio di formula di scalabilità automatica

Di seguito è riportato un esempio di una formula di scalabilità automatica che può essere adattato toowork per la maggior parte degli scenari. Hello variabili `startingNumberOfVMs` e `maxNumberofVMs` in hello formula di esempio può essere adattato tooyour esigenze. Questa formula viene ridimensionata nodi dedicati, ma può essere modificato tooapply tooscale anche i nodi con priorità bassa. 

```
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicatedNodes=min(maxNumberofVMs, pendingTaskSamples);
```

Con questa formula di scalabilità automatica, il pool di hello viene inizialmente creato con una singola macchina virtuale. Hello `$PendingTasks` metrica definisce il numero di hello di attività che sono in esecuzione o in coda. formula Hello trova numero medio di hello attività in sospeso in hello ultimi 180 secondi e imposta hello `$TargetDedicatedNodes` variabile di conseguenza. formula di Hello garantisce che il numero di destinazione hello dei nodi dedicati non superi mai il 25 macchine virtuali. Quando vengono inviate nuove attività, si espande automaticamente pool hello. Come attività di completamento, le macchine virtuali diventano disponibile uno alla volta e la formula di scalabilità automatica hello hello ridotta.

## <a name="variables"></a>variables
Nelle formule di scalabilità automatica è possibile usare sia **variabili definite dal servizio** sia **variabili definite dall'utente**. le variabili di Hello definito dal servizio vengono compilate in toohello servizio Batch. Alcune sono in lettura/scrittura e altre di sola lettura. Le variabili definite dall'utente vengono configurate dall'utente. Nella formula di esempio hello illustrato nella sezione precedente hello `$TargetDedicatedNodes` e `$PendingTasks` sono variabili definito dal servizio. Le variabili `startingNumberOfVMs` e `maxNumberofVMs` sono definite dall'utente.

> [!NOTE]
> Le variabili definite dal servizio sono sempre precedute da un segno di dollaro ($). Variabili definite dall'utente, il segno di dollaro hello è facoltativo.
>
>

Hello le tabelle seguenti Mostra sia in lettura / scrittura e le variabili di sola lettura che sono definite hello servizio Batch.

È possibile ottenere e impostare i valori hello di queste variabili definito dal servizio numero hello toomanage di nodi di calcolo in un pool di:

| Variabili in lettura/scrittura definite dal servizio | Descrizione |
| --- | --- |
| $TargetDedicatedNodes |numero di destinazione Hello di dedicato nodi per il pool di hello di calcolo. numero di Hello dei nodi dedicati viene specificato come destinazione, perché un pool non può ottenere sempre numero desiderato di hello di nodi. Ad esempio, se viene modificato il numero di destinazione hello dei nodi dedicati da una versione di valutazione di scalabilità automatica prima di hello pool ha raggiunto la destinazione iniziale hello e quindi pool hello potrebbero non raggiungere la destinazione hello. <br /><br /> Un pool in un account creato con la configurazione del servizio Batch hello potrebbe non raggiungere la destinazione se destinazione hello supera una quota di nodi o core account Batch. Un pool in un account creato con la configurazione della sottoscrizione utente hello non può ottenere la relativa destinazione destinazione hello supera la quota di core condiviso hello per sottoscrizione hello.|
| $TargetLowPriorityNodes |numero di destinazione Hello di bassa priorità nodi per il pool di hello di calcolo. numero di Hello di nodi con priorità bassa viene specificato come destinazione, perché un pool non può ottenere sempre numero desiderato di hello di nodi. Ad esempio, se il numero di destinazione hello di nodi con priorità bassa viene modificato da una versione di valutazione di scalabilità automatica prima di hello pool ha raggiunto la destinazione iniziale hello, quindi pool hello potrebbero non raggiungere la destinazione hello. Un pool di anche potrebbe non raggiungere la destinazione se destinazione hello supera una quota di nodi o core account Batch. <br /><br /> Per altre informazioni sui nodi calcolo con priorità bassa, vedere [Usare le VM con priorità bassa in Batch (anteprima)](batch-low-pri-vms.md). |
| $NodeDeallocationOption |azione di Hello che si verifica quando i nodi di calcolo vengono rimossi da un pool. I valori possibili sono:<ul><li>**riaccodamento**-termina immediatamente le attività e le inserisce nuovamente nella coda processi hello in modo che vengano ripianificate.<li>**terminare**-termina le attività immediatamente e li rimuove dalla coda dei processi di hello.<li>**taskcompletion**-attende attualmente in esecuzione attività toofinish e quindi rimuove il nodo hello dal pool di hello.<li>**retaineddata**-attende tutti hello mantenuti attività dati locali nel hello nodo toobe puliti prima di rimuovere il nodo hello dal pool hello.</ul> |

È possibile ottenere il valore di hello di queste modifiche toomake definito dal servizio variabili che sono in base alle metriche dal servizio Batch hello:

| Variabili di sola lettura definite dal servizio | Descrizione |
| --- | --- |
| $CPUPercent |percentuale media di Hello di utilizzo della CPU. |
| $WallClockSeconds |numero di Hello di secondi usati. |
| $MemoryBytes |numero medio di Hello di megabyte usati. |
| $DiskBytes |numero medio di Hello di gigabyte usati nei dischi locali hello. |
| $DiskReadBytes |numero di Hello di byte letti. |
| $DiskWriteBytes |numero di Hello di byte scritti. |
| $DiskReadOps |eseguita il conteggio di Hello delle operazioni di lettura del disco. |
| $DiskWriteOps |conteggio di Hello di eseguire operazioni di scrittura su disco. |
| $NetworkInBytes |numero di Hello di byte in ingresso. |
| $NetworkOutBytes |numero di Hello di byte in uscita. |
| $SampleNodeCount |conteggio di Hello dei nodi di calcolo. |
| $ActiveTasks |numero di Hello di attività che sono pronti tooexecute ma non ancora in esecuzione. conteggio di Hello $ActiveTasks include tutte le attività che si trovano in stato attivo hello e le cui dipendenze sono state soddisfatte. Tutte le attività che sono in stato attivo hello ma non sono stati soddisfatti le cui dipendenze sono escluse dal conteggio hello $ActiveTasks.|
| $RunningTasks |numero di Hello di attività in esecuzione. |
| $PendingTasks |somma di Hello di $ActiveTasks e $RunningTasks. |
| $SucceededTasks |numero di Hello di attività che è stata completata. |
| $FailedTasks |numero di Hello di attività che non è riuscita. |
| $CurrentDedicatedNodes |numero corrente di Hello di dedicato nodi di calcolo. |
| $CurrentLowPriorityNodes |numero corrente di Hello di bassa priorità nodi di calcolo, inclusi tutti i nodi che sono stati rimovibile. |
| $PreemptedNodeCount | numero di Hello di nodi nel pool di hello che sono in uno stato rimovibile. |

> [!TIP]
> sono Hello le variabili di sola lettura, definito dal servizio vengono visualizzate nella tabella precedente hello *oggetti* vari metodi che forniscono dati tooaccess associati a ognuna. Per altre informazioni, vedere [Ottenere dati di esempio](#getsampledata) più avanti in questo articolo.
>
>

## <a name="types"></a>Tipi
Questi sono i tipi supportati in una formula:

* double
* doubleVec
* doubleVecList
* string
* timestamp - timestamp è una struttura composta che contiene i seguenti membri hello:

  * year
  * month (1-12)
  * day (1-31)
  * giorno della settimana (in formato hello del numero; ad esempio, 1 per lunedì)
  * hour (in formato 24 ore, ad esempio 13 per indicare le ore 13.00)
  * minute (00-59)
  * second (00-59)
* timeInterval

  * TimeInterval_Zero
  * TimeInterval_100ns
  * TimeInterval_Microsecond
  * TimeInterval_Millisecond
  * TimeInterval_Second
  * TimeInterval_Minute
  * TimeInterval_Hour
  * TimeInterval_Day
  * TimeInterval_Week
  * TimeInterval_Year

## <a name="operations"></a>Operazioni
Queste operazioni sono consentite sui tipi di hello elencati nella sezione precedente hello.

| Operazione | Operatori supportati | Tipo di risultato |
| --- | --- | --- |
| double *operatore* double |+, -, *, / |double |
| double *operatore* timeinterval |* |timeInterval |
| doubleVec *operatore* double |+, -, *, / |doubleVec |
| doubleVec *operatore* doubleVec |+, -, *, / |doubleVec |
| timeinterval *operatore* double |*, / |timeInterval |
| timeinterval *operatore* timeinterval |+, - |timeInterval |
| timeinterval *operatore* timestamp |+ |timestamp |
| timestamp *operatore* timeinterval |+ |timestamp |
| timestamp *operatore* timestamp |- |timeInterval |
| *operatoree*double |-, ! |double |
| *operatoree*timeInterval |- |timeInterval |
| double *operatore* double |<, <=, ==, >=, >, != |double |
| string *operatore* string |<, <=, ==, >=, >, != |double |
| timestamp *operatore* timestamp |<, <=, ==, >=, >, != |double |
| timeinterval *operatore* timeinterval |<, <=, ==, >=, >, != |double |
| double *operatore* double |&&, &#124;&#124; |double |

Durante il test di un valore double con un operatore ternario (`double ? statement1 : statement2`), diverso da zero è **true** e zero è **false**.

## <a name="functions"></a>Funzioni
Questi predefiniti **funzioni** sono disponibili per toouse nella definizione di una formula di scalabilità automatica.

| Funzione | Tipo restituito | Descrizione |
| --- | --- | --- |
| avg(doubleVecList) |double |Restituisce hello valore medio per tutti i valori in doubleVecList hello. |
| len(doubleVecList) |double |Restituisce hello lunghezza del vettore hello creato da doubleVecList hello. |
| lg(double) |double |Restituisce hello logaritmo in base 2 di hello double. |
| lg(doubleVecList) |doubleVec |Restituisce hello component-wise logaritmo in base 2 di hello doubleVecList. Un vec (Double) deve essere passato in modo esplicito per il parametro hello. In caso contrario, verrà utilizzato versione double LG (Double) hello. |
| ln(double) |double |Restituisce hello logaritmo naturale di hello double. |
| ln(doubleVecList) |doubleVec |Restituisce hello component-wise logaritmo in base 2 di hello doubleVecList. Un vec (Double) deve essere passato in modo esplicito per il parametro hello. In caso contrario, verrà utilizzato versione double LG (Double) hello. |
| log(double) |double |Restituisce hello logaritmo in base 10 di hello double. |
| log(doubleVecList) |doubleVec |Restituisce hello component-wise logaritmo in base 10 di hello doubleVecList. Un vec (Double) deve essere passato in modo esplicito per il singolo parametro double hello. In caso contrario, verrà utilizzato versione double log (Double) hello. |
| max(doubleVecList) |double |Restituisce hello valore massimo in doubleVecList hello. |
| min(doubleVecList) |double |Restituisce hello valore minimo in doubleVecList hello. |
| norm(doubleVecList) |double |Restituisce hello seminorma del vettore hello creato da doubleVecList hello. |
| percentile(doubleVec v, double p) |double |Restituisce hello elemento percentile del vettore hello v. |
| rand() |double |Restituisce un valore casuale compreso tra 0,0 e 1,0. |
| range(doubleVecList) |double |Restituisce la differenza di hello tra valori hello minimo e massimo in doubleVecList hello. |
| std(doubleVecList) |double |Restituisce hello deviazione standard del campione di valori hello in hello doubleVecList. |
| stop() | |Arresta la valutazione dell'espressione per la scalabilità automatica hello. |
| sum(doubleVecList) |double |Restituisce hello somma di tutti i componenti di doubleVecList hello hello. |
| time(string dateTime="") |timestamp |Restituisce timestamp hello di hello ora corrente, se nessun parametro viene passato o hello timestamp della stringa dateTime hello se viene passato. I formati dateTime supportati sono W3C-DTF e RFC 1123. |
| val(doubleVec v, double i) |double |Restituisce il valore di hello dell'elemento hello nella posizione i nel vettore v con un indice iniziale pari a zero. |

Alcune funzioni che sono descritte nella tabella precedente hello hello può accettare un elenco come argomento. elenco delimitato da virgole di Hello è qualsiasi combinazione di *doppie* e *doubleVec*. ad esempio:

`doubleVecList := ( (double | doubleVec)+(, (double | doubleVec) )* )?`

Hello *doubleVecList* valore viene convertito tooa singolo *doubleVec* prima della valutazione. Ad esempio, se `v = [1,2,3]`, quindi chiamare `avg(v)` è equivalente toocalling `avg(1,2,3)`. La chiamata `avg(v, 7)` è equivalente toocalling `avg(1,2,3,7)`.

## <a name="getsampledata"></a>Ottenere dati di esempio
Formule di scalabilità automatica agiscono su dati di metrica (esempi) fornito dal servizio Batch hello. Una formula aumenta o riduce le dimensioni del pool in base a valori hello ottenuto dal servizio hello. Hello definito dal servizio le variabili sono stati descritti in precedenza sono oggetti che forniscono vari metodi tooaccess dati associato a tale oggetto. Ad esempio, hello espressione riportata di seguito viene illustrato un hello tooget richiesta ultimi 5 minuti di utilizzo della CPU:

```
$CPUPercent.GetSample(TimeInterval_Minute * 5)
```

| Metodo | Descrizione |
| --- | --- |
| GetSample() |Hello `GetSample()` metodo restituisce un vettore di esempi di dati.<br/><br/>Un campione rappresenta 30 secondi di dati di metrica. In altre parole i campioni vengono raccolti ogni 30 secondi, Ma, come indicato di seguito, si verifica un ritardo tra quando viene raccolto un campione e quando è disponibile tooa formula. Di conseguenza, i campioni per un determinato periodo di tempo potrebbero non essere tutti disponibili per la valutazione da parte di una formula.<ul><li>`doubleVec GetSample(double count)`<br/>Specifica il numero di hello di esempi tooobtain dagli esempi più recenti hello che sono stati raccolti.<br/><br/>`GetSample(1)`Restituisce l'ultimo esempio disponibile di hello. Per le metriche quali `$CPUPercent`, tuttavia, questo non deve essere utilizzato perché è Impossibile tooknow *quando* è stato raccolto il campione hello. Potrebbe essere recente o risultare molto meno recente a causa di problemi di sistema. È preferibile in tali toouse casi un intervallo di tempo, come illustrato di seguito.<li>`doubleVec GetSample((timestamp or timeinterval) startTime [, double samplePercent])`<br/>Specifica un intervallo di tempo per la raccolta di dati di esempio. Facoltativamente, specifica inoltre percentuale hello di campioni che deve essere disponibile in hello richiesto l'intervallo di tempo.<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10)`restituisce 20 campioni se sono presenti nella cronologia CPUPercent hello tutti i campioni per hello ultimi 10 minuti. Se hello ultimo minuto della cronologia non è disponibile, tuttavia, verranno restituiti solo 18 esempi. In questo caso:<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10, 95)`avrà esito negativo perché solo il 90% di campioni di hello sono disponibili.<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10, 80)` avrà esito positivo.<li>`doubleVec GetSample((timestamp or timeinterval) startTime, (timestamp or timeinterval) endTime [, double samplePercent])`<br/>Specifica un intervallo di tempo per la raccolta dei dati, con un'ora di inizio e un'ora di fine.<br/><br/>Come indicato in precedenza, si verifica un ritardo tra quando viene raccolto un campione e quando è disponibile tooa formula. Considerare questo ritardo quando si utilizza hello `GetSample` metodo. Vedere `GetSamplePercent` di seguito. |
| GetSamplePeriod() |Restituisce il periodo di hello di campioni che sono stati eseguiti in un set di dati cronologici di esempio. |
| Count() |Restituisce hello numero totale di campioni nella cronologia di metrica hello. |
| HistoryBeginTime() |Restituisce hello timestamp dell'esempio di dati disponibili per metrica hello meno recente hello. |
| GetSamplePercent() |Restituisce hello percentuali di campioni che sono disponibili per un determinato intervallo di tempo. ad esempio:<br/><br/>`doubleVec GetSamplePercent( (timestamp or timeinterval) startTime [, (timestamp or timeinterval) endTime] )`<br/><br/>Poiché hello `GetSample` metodo ha esito negativo se la percentuale di hello di campioni restituito è minore di hello `samplePercent` specificato, è possibile utilizzare hello `GetSamplePercent` metodo toocheck prima. È quindi possibile eseguire un'azione alternativa se sufficienti esempi sono presenti, senza interrompere la valutazione di scalabilità automatica di hello. |

### <a name="samples-sample-percentage-and-hello-getsample-method"></a>Esempi, la percentuale di campionamento e hello *GetSample()* (metodo)
funzionamento di base Hello di una formula di scalabilità automatica è tooobtain attività e risorse dati di metrica e quindi modificare le dimensioni del pool in base a tali dati. Di conseguenza, è importante toohave una comprensione chiara della modalità di interazione delle formule di scalabilità automatica con i dati di metrica (esempi).

**Esempi**

Hello servizio Batch periodicamente accetta gli esempi di metriche di attività e risorse e li rende disponibili tooyour formule di scalabilità automatica. Questi esempi vengono registrati ogni 30 secondi per hello servizio Batch. Tuttavia, si verifica in genere un ritardo tra registrati quando tali esempi e quando vengono resi disponibili troppo (e può essere letto da) delle formule di scalabilità automatica. Inoltre, a causa di fattori toovarious, ad esempio una rete o altri problemi di infrastruttura, gli esempi potrebbero non essere registrati per un determinato intervallo.

**Percentuale di campioni**

Quando `samplePercent` viene passato toohello `GetSample()` metodo o hello `GetSamplePercent()` metodo viene chiamato, _%_ fa riferimento confronto tooa tra hello possibile totale di campioni che vengono registrati dal servizio Batch hello e numero di Hello di campioni che sono disponibili tooyour formula di scalabilità automatica.

Come esempio, si esaminerà un intervallo di tempo di 10 minuti. Poiché gli esempi vengono registrati ogni 30 secondi all'interno di un intervallo di tempo di 10 minuti, hello numero massimo totale di campioni che vengono registrati dal Batch sarà 20 campioni (2 al minuto). Tuttavia, a causa di latenza inerente a toohello di hello reporting meccanismo e altri problemi all'interno di Azure, è possibile solo 15 esempi disponibili tooyour formula di scalabilità automatica per la lettura. In tal caso, ad esempio, per tale periodo di 10 minuti, solo il 75% del numero totale di hello di campioni registrati possibile formula tooyour disponibili.

**GetSample() e intervalli di campioni**

Le formule di scalabilità automatica sono in corso toobe espansione e riduzione del pool di &mdash; aggiunta di nodi o rimozione di nodi. Poiché i nodi una perdita di denaro, si desidera tooensure che le formule utilizzano un metodo di analisi che si basa su dati sufficienti intelligente. È quindi consigliabile usare un tipo di analisi delle tendenze nelle formule, aumentando e riducendo i pool in base a un intervallo di campioni raccolti.

toodo in tal caso, utilizzare `GetSample(interval look-back start, interval look-back end)` tooreturn un vettore di campioni:

```
$runningTasksSample = $RunningTasks.GetSample(1 * TimeInterval_Minute, 6 * TimeInterval_Minute);
```

Quando hello sopra linea viene valutata dal Batch, restituisce un elenco di esempi di come un vettore di valori. ad esempio:

```
$runningTasksSample=[1,1,1,1,1,1,1,1,1,1];
```

Dopo aver raccolto il vettore di hello di esempi, è quindi possibile utilizzare funzioni quali `min()`, `max()`, e `avg()` tooderive valori significativi da hello raccolti intervallo.

Per una maggiore sicurezza, è possibile forzare una formula di valutazione toofail se inferiore a una determinata percentuale di esempio è disponibile per un determinato periodo di tempo. Se si forza toofail una formula di valutazione, è indicare toocease Batch un'ulteriore valutazione della formula hello se hello specificato percentuali di campioni non è disponibile. In questo caso, dimensioni del pool toohello viene apportata alcuna modifica. toospecify una percentuale di campioni per toosucceed valutazione hello, obbligatoria specificarlo come hello terzo parametro troppo`GetSample()`. Qui è specificato un requisito pari al 75% dei campioni:

```
$runningTasksSample = $RunningTasks.GetSample(60 * TimeInterval_Second, 120 * TimeInterval_Second, 75);
```

Poiché possono essere presenti un ritardo nella disponibilità di esempio, è importante tooalways specificare un intervallo di tempo con un'ora di inizio ricerca back antecedenti a un minuto. Per esempi toopropagate attraverso il sistema di hello, pertanto esempi nell'intervallo di hello, richiede circa un minuto `(0 * TimeInterval_Second, 60 * TimeInterval_Second)` potrebbe non essere disponibile. Nuovamente, è possibile utilizzare il parametro di percentuale hello di `GetSample()` tooforce un requisito di percentuale di esempio specifico.

> [!IMPORTANT]
> È **consigliabile** **evitare di basarsi *solo* su `GetSample(1)` nelle formule di scalabilità automatica**. In questo modo `GetSample(1)` essenzialmente afferma servizio Batch toohello, "Offrono me hello ultimo esempio si dispone, indipendentemente dal tempo trascorso che è stato recuperato." Poiché è solo un singolo campione e può essere un esempio precedente, potrebbe non essere rappresentativo di immagine hello dell'attività recente o lo stato della risorsa. Se si utilizza `GetSample(1)`, assicurarsi che è parte di un'istruzione più grande e non hello solo punto dati da cui dipende la formula.
>
>

## <a name="metrics"></a>Metrica
Quando si definisce una formula, è possibile usare metriche di risorse e di attività. È regolare il numero di destinazione hello dei nodi dedicati in pool hello in base ai dati di metrica hello che è possibile ottenere e valutare. Vedere hello [variabili](#variables) precedente sezione per ulteriori informazioni su ogni metrica.

<table>
  <tr>
    <th>Metrica</th>
    <th>Descrizione</th>
  </tr>
  <tr>
    <td><b>Risorsa</b></td>
    <td><p>Metriche delle risorse basati su hello CPU, larghezza di banda hello, utilizzo della memoria hello di nodi di calcolo e hello numero di nodi.</p>
        <p> Queste variabili definite dal servizio sono utili per eseguire adeguamenti in base al conteggio dei nodi:</p>
    <p><ul>
            <li>$TargetDedicatedNodes</li>
            <li>$TargetLowPriorityNodes</li>
            <li>$CurrentDedicatedNodes</li>
            <li>$CurrentLowPriorityNodes</li>
            <li>$preemptedNodeCount</li>
            <li>$SampleNodeCount</li>
    </ul></p>
    <p>Queste variabili definite dal servizio sono utili per eseguire adeguamenti in base all'utilizzo delle risorse dei nodi:</p>
    <p><ul>
      <li>$CPUPercent</li>
      <li>$WallClockSeconds</li>
      <li>$MemoryBytes</li>
      <li>$DiskBytes</li>
      <li>$DiskReadBytes</li>
      <li>$DiskWriteBytes</li>
      <li>$DiskReadOps</li>
      <li>$DiskWriteOps</li>
      <li>$NetworkInBytes</li>
      <li>$NetworkOutBytes</li></ul></p>
  </tr>
  <tr>
    <td><b>Task</b></td>
    <td><p>Le metriche di attività sono in base allo stato di hello di attività, come ad esempio attivo, in sospeso e completate. Hello seguenti variabili definito dal servizio sono utili per apportare modifiche di dimensione del pool in base alle metriche di attività:</p>
    <p><ul>
      <li>$ActiveTasks</li>
      <li>$RunningTasks</li>
      <li>$PendingTasks</li>
      <li>$SucceededTasks</li>
            <li>$FailedTasks</li></ul></p>
        </td>
  </tr>
</table>

## <a name="write-an-autoscale-formula"></a>Scrivere una formula di scalabilità automatica
Per compilare una formula di scalabilità automatica che costituiscono le istruzioni che utilizzano hello in precedenza componenti, quindi combinare tali istruzioni in una formula completa. In questa sezione si crea una formula di scalabilità automatica di esempio che può assumere alcune decisioni di scalabilità in scenari del mondo reale.

In primo luogo, è pertanto possibile definire i requisiti di hello per la nuova formula di scalabilità automatica. formula Hello deve:

1. Aumentare il numero di destinazione di hello dedicato di nodi di calcolo in un pool se l'utilizzo della CPU è elevato.
2. Ridurre il numero di destinazione di hello dedicato di nodi di calcolo in un pool quando l'utilizzo della CPU è insufficiente.
3. Sempre limitare hello massimo numero di nodi dedicato too400.

Consente di definire i nodi durante l'utilizzo elevato della CPU, svariate hello tooincrease istruzione hello che popola una variabile definita dall'utente (`$totalDedicatedNodes`) con un valore che corrisponde al 110% del numero di destinazione corrente di hello di nodi dedicati, ma solo se hello minimo utilizzo medio della CPU durante l'hello ultimi 10 minuti è superiore al 70%. In caso contrario, è possibile utilizzare il valore di hello per numero corrente di hello di nodi dedicati.

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
```

troppo*diminuire* hello numero di nodi dedicati durante un basso utilizzo della CPU, hello stessa istruzione successiva nel nostro hello set formula `$totalDedicatedNodes` too90 variabile percentuale del numero di destinazione corrente di hello di nodi dedicati se hello utilizzo medio CPU hello negli ultimi 60 minuti è stato in % 20. In caso contrario, utilizzare il valore corrente di hello di `$totalDedicatedNodes` è popolati nell'istruzione hello precedente.

```
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
```

Ora limite hello destinazione numero massimo di tooa di nodi di calcolo dedicato di 400:

```
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

Di seguito è riportata la formula completa hello:

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

## <a name="create-an-autoscale-enabled-pool-with-net"></a>Creare un pool abilitato per la scalabilità automatica con .NET

toocreate un pool con scalabilità automatica abilitata in .NET, seguire questi passaggi:

1. Creare pool di hello con [BatchClient.PoolOperations.CreatePool](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.createpool).
2. Set hello [CloudPool.AutoScaleEnabled](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleenabled) proprietà troppo`true`.
3. Set hello [CloudPool.AutoScaleFormula](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula) proprietà con la formula di scalabilità automatica.
4. (Facoltativo) Set hello [CloudPool.AutoScaleEvaluationInterval](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval) proprietà (valore predefinito è 15 minuti).
5. Eseguire il commit pool hello con [CloudPool.Commit](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commit) o [a CommitAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commitasync).

Hello frammento di codice seguente crea un pool di scalabilità automatica abilitata in .NET. Hello formula di scalabilità automatica del pool imposta hello destinazione numero di nodi dedicato too5 lunedì e 1 il giorno della settimana hello. Hello [intervallo di ridimensionamento automatico](#automatic-scaling-interval) è impostato too30 minuti. In questo e altri frammenti c# in questo articolo, hello `myBatchClient` è un'istanza di hello inizializzata correttamente [BatchClient] [ net_batchclient] classe.

```csharp
CloudPool pool = myBatchClient.PoolOperations.CreatePool(
                    poolId: "mypool",
                    virtualMachineSize: "small", // single-core, 1.75 GB memory, 225 GB disk
                    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));    
pool.AutoScaleEnabled = true;
pool.AutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";
pool.AutoScaleEvaluationInterval = TimeSpan.FromMinutes(30);
await pool.CommitAsync();
```

> [!IMPORTANT]
> Quando si crea un pool di scalabilità automatica abilitata, non si specifica hello _targetDedicatedComputeNodes_ parametro o hello _targetLowPriorityComputeNodes_ parametro hello chiamare troppo **CreatePool**. Specificare invece hello **AutoScaleEnabled** e **AutoScaleFormula** proprietà nel pool di hello. valori di Hello per queste proprietà determinano il numero di destinazione hello di ogni tipo di nodo. Inoltre, toomanually ridimensionare un pool di scalabilità automatica abilitata (ad esempio, con [BatchClient.PoolOperations.ResizePoolAsync][net_poolops_resizepoolasync]), primo **disabilitare** la scalabilità automatica in Hello pool, quindi ridimensionarlo.
>
>

Inoltre tooBatch .NET, è possibile utilizzare una delle altre hello [Batch SDK](batch-apis-tools.md#azure-accounts-for-batch-development), [Batch REST](https://docs.microsoft.com/rest/api/batchservice/), [i cmdlet di PowerShell Batch](batch-powershell-cmdlets-get-started.md), hello e [CLI Batch](batch-cli-get-started.md)tooconfigure per la scalabilità automatica.


### <a name="automatic-scaling-interval"></a>Intervallo di ridimensionamento automatico
Per impostazione predefinita, hello servizio Batch consente di regolare le dimensioni di un pool in base tooits formula di scalabilità automatica ogni 15 minuti. Questo intervallo è configurabile tramite hello seguenti proprietà del pool:

* [CloudPool.AutoScaleEvaluationInterval][net_cloudpool_autoscaleevalinterval] (Batch .NET)
* [autoScaleEvaluationInterval][rest_autoscaleinterval] (API REST)

intervallo minimo Hello è cinque minuti e hello massimo è 168 ore. Se viene specificato un intervallo all'esterno di questo intervallo, hello servizio Batch restituisce un errore di richiesta non valida (400).

> [!NOTE]
> La scalabilità automatica non è attualmente previsto toorespond toochanges in meno di un minuto, ma è invece destinato dimensioni hello tooadjust del pool di gradualmente durante l'esecuzione di un carico di lavoro.
>
>

## <a name="enable-autoscaling-on-an-existing-pool"></a>Abilitare la scalabilità automatica in un pool esistente

Ogni Batch di SDK fornisce un adattamento automatico tooenable modo. ad esempio:

* [BatchClient.PoolOperations.EnableAutoScaleAsync][net_enableautoscaleasync] (Batch .NET)
* [Abilitare la scalabilità automatica in un pool][rest_enableautoscale] (API REST)

Quando si abilita il ridimensionamento automatico in un pool esistente, tenere hello presente seguenti punti:

* Se la scalabilità automatica è attualmente disabilitata nel pool di hello quando si esegue il ridimensionamento automatico di hello richiesta tooenable, è necessario specificare una formula di scalabilità automatica valido quando si esegue una richiesta di hello. Facoltativamente, è possibile specificare un intervallo di valutazione della scalabilità automatica. Se non si specifica un intervallo, viene utilizzato il valore predefinito hello di 15 minuti.
* Se scalabilità automatica sono attualmente abilitata nel pool di hello, è possibile specificare una formula di scalabilità automatica, un intervallo di valutazione o entrambi. È necessario specificare almeno una di queste proprietà.

  * Se si specifica un nuovo intervallo di valutazione di scalabilità automatica, pianificazione valutazione esistente hello viene arrestato e viene avviata una nuova pianificazione. ora di inizio della pianificazione nuova Hello è ora hello in cui hello è stato inviato il ridimensionamento automatico tooenable richiesta.
  * Se si omette entrambi intervallo hello formula o evaluation di scalabilità automatica, hello servizio Batch continua valore corrente di hello toouse di tale impostazione.

> [!NOTE]
> Se sono specificati valori per hello *targetDedicatedComputeNodes* o *targetLowPriorityComputeNodes* parametri di hello **CreatePool** metodo durante la creazione di hello pool in .NET, o per i parametri di confrontabili hello in un'altra lingua, quindi tali valori vengono ignorati quando viene valutata hello formula di scalabilità automatica.
>
>

Questo frammento di codice c# utilizza hello [.NET per Batch] [ net_api] la scalabilità automatica tooenable libreria in un pool esistente:

```csharp
// Define hello autoscaling formula. This formula sets hello target number of nodes
// too5 on Mondays, and 1 on every other day of hello week
string myAutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";

// Set hello autoscale formula on hello existing pool
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myAutoScaleFormula);
```

### <a name="update-an-autoscale-formula"></a>Aggiornare una formula di scalabilità automatica

formula di hello tooupdate esistente di scalabilità automatica abilitata pool, la scalabilità automatica tooenable operazione chiamata hello con nuova formula hello. Se, ad esempio, la scalabilità automatica è già abilitata nel `myexistingpool` quando viene eseguita dopo il codice .NET hello, la formula di scalabilità automatica viene sostituita con il contenuto di hello di `myNewFormula`.

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myNewFormula);
```

### <a name="update-hello-autoscale-interval"></a>Intervallo di aggiornamento hello scalabilità automatica

tooupdate hello scalabilità automatica l'intervallo di valutazione di un di scalabilità automatica abilitata pool esistente, la scalabilità automatica tooenable operazione chiamata hello nuovamente con il nuovo intervallo di hello. Ad esempio, tooset hello scalabilità automatica valutazione intervallo too60 minuti per un pool è già abilitato per la scalabilità automatica in .NET:

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleEvaluationInterval: TimeSpan.FromMinutes(60));
```

## <a name="evaluate-an-autoscale-formula"></a>Valutare la formula di scalabilità automatica

È possibile valutare una formula prima di applicarla tooa pool. In questo modo, è possibile testare toosee formula di hello come le relative istruzioni valutano prima di inserire la formula hello nell'ambiente di produzione.

tooevaluate una formula di scalabilità automatica, è innanzitutto necessario abilitare la scalabilità automatica nel pool di hello con una formula valida. tootest una formula in un pool che non dispone ancora di scalabilità automatica è abilitata, utilizzare hello una sola riga formula `$TargetDedicatedNodes = 0` quando si attiva prima di tutto la scalabilità automatica. Quindi, utilizzare uno dei hello tooevaluate hello formula desiderata tootest seguente:

* [BatchClient.PoolOperations.EvaluateAutoScale](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscale) o [EvaluateAutoScaleAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscaleasync)

    Questi metodi .NET per Batch richiedono hello ID di un pool esistente e una stringa contenente hello tooevaluate di formula di scalabilità automatica.

* [Valutare la formula di scalabilità automatica](https://docs.microsoft.com/rest/api/batchservice/evaluate-an-automatic-scaling-formula)

    In questa richiesta di API REST, specificare l'ID del pool di hello in hello URI e hello formula di scalabilità automatica in hello *autoScaleFormula* elemento del corpo della richiesta hello. risposta di Hello dell'operazione hello contiene eventuali informazioni sugli errori che potrebbero essere correlati toohello formula.

Questo frammento di codice [Batch .NET][net_api] valuta una formula di scalabilità automatica. Se il pool di hello non dispone di scalabilità automatica abilitata, è abilitarlo prima.

```csharp
// First obtain a reference tooan existing pool
CloudPool pool = await batchClient.PoolOperations.GetPoolAsync("myExistingPool");

// If autoscaling isn't already enabled on hello pool, enable it.
// You can't evaluate an autoscale formula on non-autoscale-enabled pool.
if (pool.AutoScaleEnabled == false)
{
    // We need a valid autoscale formula tooenable autoscaling on the
    // pool. This formula is valid, but won't resize hello pool:
    await pool.EnableAutoScaleAsync(
        autoscaleFormula: "$TargetDedicatedNodes = {pool.CurrentDedicatedNodes};",
        autoscaleEvaluationInterval: TimeSpan.FromMinutes(5));

    // Batch limits EnableAutoScaleAsync calls tooonce every 30 seconds.
    // Because we want tooapply our new autoscale formula below if it
    // evaluates successfully, and we *just* enabled autoscaling on
    // this pool, we pause here tooensure we pass that threshold.
    Thread.Sleep(TimeSpan.FromSeconds(31));

    // Refresh hello properties of hello pool so that we've got the
    // latest value for AutoScaleEnabled
    await pool.RefreshAsync();
}

// We must ensure that autoscaling is enabled on hello pool prior to
// evaluating a formula
if (pool.AutoScaleEnabled == true)
{
    // hello formula tooevaluate - adjusts target number of nodes based on
    // day of week and time of day
    string myFormula = @"
        $curTime = time();
        $workHours = $curTime.hour >= 8 && $curTime.hour < 18;
        $isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
        $isWorkingWeekdayHour = $workHours && $isWeekday;
        $TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
    ";

    // Perform hello autoscale formula evaluation. Note that this code does not
    // actually apply hello formula toohello pool.
    AutoScaleRun eval =
        await batchClient.PoolOperations.EvaluateAutoScaleAsync(pool.Id, myFormula);

    if (eval.Error == null)
    {
        // Evaluation success - print hello results of hello AutoScaleRun.
        // This will display hello values of each variable as evaluated by the
        // autoscale formula.
        Console.WriteLine("AutoScaleRun.Results: " +
            eval.Results.Replace("$", "\n    $"));

        // Apply hello formula toohello pool since it evaluated successfully
        await batchClient.PoolOperations.EnableAutoScaleAsync(pool.Id, myFormula);
    }
    else
    {
        // Evaluation failed, output hello message associated with hello error
        Console.WriteLine("AutoScaleRun.Error.Message: " +
            eval.Error.Message);
    }
}
```

Valutazione con esito positivo della formula hello illustrata in questo frammento di codice produce risultati simili a:

```
AutoScaleRun.Results:
    $TargetDedicatedNodes=10;
    $NodeDeallocationOption=requeue;
    $curTime=2016-10-13T19:18:47.805Z;
    $isWeekday=1;
    $isWorkingWeekdayHour=0;
    $workHours=0
```

## <a name="get-information-about-autoscale-runs"></a>Visualizzare informazioni sulle esecuzioni della scalabilità automatica

tooensure che sta eseguendo la formula come previsto, è consigliabile verificare periodicamente risultati hello di viene eseguito il ridimensionamento automatico hello che esegue il pool di Batch. toodo in tal caso, get (o aggiornare) toohello un riferimento pool e, esaminare le proprietà di hello della scalabilità automatica ultima esecuzione.

In .NET per Batch, hello [CloudPool.AutoScaleRun](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscalerun) proprietà ha diverse proprietà che forniscono informazioni su hello più recente il ridimensionamento automatico eseguire eseguita nel pool di hello:

* [AutoScaleRun.Timestamp](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.timestamp)
* [AutoScaleRun.Results](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.results)
* [AutoScaleRun.Error](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.error)

In hello API REST, hello [ottenere informazioni su un pool](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool) richiesta restituisce informazioni sul pool di hello, che include hello più recente il ridimensionamento automatico le informazioni sull'esecuzione di hello [autoScaleRun](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool#bk_autrun) proprietà.

Hello seguente frammento di codice c# utilizza le hello .NET per Batch libreria tooprint informazioni hello ultima per la scalabilità automatica eseguire sul pool _myPool_:

```csharp
await Cloud pool = myBatchClient.PoolOperations.GetPoolAsync("myPool");
Console.WriteLine("Last execution: " + pool.AutoScaleRun.Timestamp);
Console.WriteLine("Result:" + pool.AutoScaleRun.Results.Replace("$", "\n  $"));
Console.WriteLine("Error: " + pool.AutoScaleRun.Error);
```

Esempio di output di hello precedente frammento di codice:

```
Last execution: 10/14/2016 18:36:43
Result:
  $TargetDedicatedNodes=10;
  $NodeDeallocationOption=requeue;
  $curTime=2016-10-14T18:36:43.282Z;
  $isWeekday=1;
  $isWorkingWeekdayHour=0;
  $workHours=0
Error:
```

## <a name="example-autoscale-formulas"></a>Formule di scalabilità automatica di esempio
Esaminiamo alcune formule che mostrano l'importo di hello tooadjust modi diversi delle risorse di calcolo in un pool.

### <a name="example-1-time-based-adjustment"></a>Esempio 1: Adeguamento basato sul tempo
Si supponga di dimensioni del pool hello tooadjust in base a hello giorno della settimana hello e l'ora del giorno. Questo esempio mostra come tooincrease o diminuire il numero di hello di nodi in hello del pool di conseguenza.

formula Hello ottiene innanzitutto hello ora corrente. Se si tratta di un giorno della settimana (1-5) e nelle ore lavorative (8 AM too6 PM), dimensione del pool di destinazione hello è impostato too20 nodi. In caso contrario, è stata impostata too10 nodi.

```
$curTime = time();
$workHours = $curTime.hour >= 8 && $curTime.hour < 18;
$isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
$isWorkingWeekdayHour = $workHours && $isWeekday;
$TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
```

### <a name="example-2-task-based-adjustment"></a>Esempio 2: Adeguamento basato sulle attività
In questo esempio hello pool viene ridimensionata in base al numero di hello delle attività nella coda di hello. Sia i commenti che le interruzioni di riga sono accettabili nelle stringhe della formula.

```csharp
// Get pending tasks for hello past 15 minutes.
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
// If we have fewer than 70 percent data points, we use hello last sample point,
// otherwise we use hello maximum of last sample point and hello history average.
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1), avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// If number of pending tasks is not 0, set targetVM toopending tasks, otherwise
// half of current dedicated.
$targetVMs = $tasks > 0? $tasks:max(0, $TargetDedicatedNodes/2);
// hello pool size is capped at 20, if target VM value is more than that, set it
// too20. This value should be adjusted according tooyour use case.
$TargetDedicatedNodes = max(0, min($targetVMs, 20));
// Set node deallocation mode - keep nodes active only until tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-3-accounting-for-parallel-tasks"></a>Esempio 3: Considerazioni sulle attività parallele
Questo esempio Adatta dimensioni del pool hello in base al numero di hello delle attività. Questa formula accetta anche in hello account [MaxTasksPerComputeNode] [ net_maxtasks] valore impostato per il pool di hello. Questo approccio è utile nelle situazioni in cui l'[esecuzione di attività parallele](batch-parallel-node-tasks.md) è abilitata nel pool.

```csharp
// Determine whether 70 percent of hello samples have been recorded in hello past
// 15 minutes; if not, use last sample
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1),avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// Set hello number of nodes tooadd tooone-fourth hello number of active tasks (the
// MaxTasksPerComputeNode property on this pool is set too4, adjust this number
// for your use case)
$cores = $TargetDedicatedNodes * 4;
$extraVMs = (($tasks - $cores) + 3) / 4;
$targetVMs = ($TargetDedicatedNodes + $extraVMs);
// Attempt toogrow hello number of compute nodes toomatch hello number of active
// tasks, with a maximum of 3
$TargetDedicatedNodes = max(0,min($targetVMs,3));
// Keep hello nodes active until hello tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-4-setting-an-initial-pool-size"></a>Esempio 4: Impostazione di dimensioni iniziali del pool
In questo esempio mostra frammento con una formula di scalabilità automatica che imposta di codice c# hello tooa dimensioni pool specificato numero di nodi per un periodo di tempo iniziale. Modifica dimensioni del pool hello in base al numero di hello dell'esecuzione e le attività attive dopo hello iniziale periodo di tempo trascorso.

formula Hello nel seguente frammento di codice hello:

* Imposta pool iniziale di hello nodi toofour dimensioni.
* Non ridimensionare hello pool all'interno di hello primi 10 minuti del ciclo di vita del pool di hello.
* Dopo 10 minuti, ottiene il valore massimo di hello hello active e numero di esecuzione di attività all'interno di hello negli ultimi 60 minuti.
  * Se entrambi i valori sono 0 (che indica che nessuna attività erano in esecuzione o attivi in hello 60 minuti), dimensione del pool di hello è impostato too0.
  * Se uno dei valori è maggiore di zero, non viene apportata alcuna modifica.

```csharp
string now = DateTime.UtcNow.ToString("r");
string formula = string.Format(@"
    $TargetDedicatedNodes = {1};
    lifespan         = time() - time(""{0}"");
    span             = TimeInterval_Minute * 60;
    startup          = TimeInterval_Minute * 10;
    ratio            = 50;

    $TargetDedicatedNodes = (lifespan > startup ? (max($RunningTasks.GetSample(span, ratio), $ActiveTasks.GetSample(span, ratio)) == 0 ? 0 : $TargetDedicatedNodes) : {1});
    ", now, 4);
```

## <a name="next-steps"></a>Passaggi successivi
* [Ottimizzare l'utilizzo delle risorse di calcolo di Azure Batch con le attività simultanee nodo](batch-parallel-node-tasks.md) contiene informazioni dettagliate su come è possibile eseguire più attività contemporaneamente sui nodi di calcolo hello del pool. Inoltre tooautoscaling, questa funzionalità può aiutare a toolower la durata del processo per alcuni carichi di lavoro, riducendo i costi.
* Per un altro ottimizzatore di efficienza, verificare che le query dell'applicazione di Batch hello servizio Batch in modo ottimale la maggior parte delle hello. Vedere [Query in modo efficiente il servizio di Azure Batch hello](batch-efficient-list-queries.md) toolearn come toolimit hello quantità di dati che attraversa il transito hello quando si esegue una query sullo stato di hello di potenzialmente migliaia di calcolo nodi o attività.

[net_api]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch
[net_batchclient]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.batchclient
[net_cloudpool_autoscaleformula]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula
[net_cloudpool_autoscaleevalinterval]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval
[net_enableautoscaleasync]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.enableautoscaleasync
[net_maxtasks]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.maxtaskspercomputenode
[net_poolops_resizepoolasync]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.resizepoolasync

[rest_api]: https://docs.microsoft.com/rest/api/batchservice/
[rest_autoscaleformula]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
[rest_autoscaleinterval]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
[rest_enableautoscale]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
