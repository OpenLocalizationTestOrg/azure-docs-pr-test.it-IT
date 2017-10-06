---
title: 'Archiviazione Premium di Azure: progettata per prestazioni elevate | Microsoft Docs'
description: Progettare applicazioni a prestazioni elevate con l'Archiviazione Premium di Azure. Archiviazione Premium offre prestazioni elevate e supporto per dischi a bassa latenza per carichi di lavoro con I/O intensivo in esecuzione su Macchine virtuali di Azure.
services: storage
documentationcenter: na
author: aungoo-msft
manager: tadb
editor: tysonn
ms.assetid: e6a409c3-d31a-4704-a93c-0a04fdc95960
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: aungoo
ms.openlocfilehash: dde3e60ae4c8387150b65f0715166b5d549891e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-premium-storage-design-for-high-performance"></a>Archiviazione Premium di Azure: progettata per prestazioni elevate
## <a name="overview"></a>Overview
Questo articolo fornisce indicazioni per lo sviluppo di applicazioni a prestazioni elevate mediante l'Archiviazione Premium di Azure. È possibile utilizzare istruzioni hello fornite in questo documento combinato con prestazioni migliori procedure consigliate applicabile tootechnologies utilizzati dall'applicazione. linee guida hello tooillustrate, è stato utilizzato SQL Server in esecuzione in archiviazione Premium come un esempio in questo documento.

Mentre si risolve gli scenari di prestazioni per il livello di archiviazione hello in questo articolo, sarà necessario toooptimize livello dell'applicazione hello. Ad esempio, se si ospita una SharePoint Farm su archiviazione Premium di Azure, è possibile utilizzare gli esempi di SQL Server hello dal server di database in questo articolo toooptimize hello. Inoltre, ottimizzare hello tooget di applicazioni server e di server Web della Farm di SharePoint hello la maggior parte delle prestazioni.

Questo articolo è utile per rispondere alle domande comuni seguenti sull'ottimizzazione delle prestazioni dell'applicazione nell'Archiviazione Premium di Azure:

* Come toomeasure le prestazioni dell'applicazione?  
* Perché non si ottengono le prestazioni elevate previste?  
* Quali fattori influenzano le prestazioni dell'applicazione nell'Archiviazione Premium?  
* In che modo questi fattori influenzano le prestazioni dell'applicazione nell'Archiviazione Premium?  
* Come si ottiene l'ottimizzazione per IOPS, larghezza di banda e latenza?  

Queste indicazioni sono specifiche per l'Archiviazione Premium, perché i carichi di lavoro in esecuzione nell'Archiviazione Premium sono influenzati in modo significativo dalle prestazioni. Sono disponibili esempi nei casi appropriati. È inoltre possibile applicare alcune di queste linee guida tooapplications in esecuzione in macchine virtuali IaaS con i dischi di archiviazione Standard.

Prima di iniziare, se si è tooPremium nuova archiviazione, leggere prima hello [archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro di macchina virtuale Azure](../storage-premium-storage.md) e [Azure obiettivi di scalabilità e prestazioni](storage-scalability-targets.md)articoli.

## <a name="application-performance-indicators"></a>Indicatori di prestazioni dell'applicazione
È valutare se l'esecuzione di un'applicazione ben o non utilizzare come indicatori di prestazioni, la velocità con cui un'applicazione sta elaborando una richiesta dell'utente, la quantità di dati è l'elaborazione di un'applicazione per ogni richiesta, il numero di richieste è un'applicazione di elaborazione in uno specifico periodo di tempo, quanto tempo che un utente ha toowait tooget una risposta dopo aver inviato la richiesta. termini tecnici di Hello per questi indicatori di prestazioni sono IOPS, velocità effettiva o della larghezza di banda e latenza.

In questa sezione verranno trattati hello comuni gli indicatori di prestazioni nel contesto di hello dell'archiviazione Premium. In hello seguente sezione, la raccolta dei requisiti dell'applicazione, si apprenderà come toomeasure questi indicatori di prestazioni per l'applicazione. Più avanti in ottimizzazione delle prestazioni dell'applicazione, si apprenderà incidono hello questi toooptimize di indicatori e indicazioni sulle prestazioni li.

## <a name="iops"></a>IOPS
IOPS è numero di richieste che l'applicazione invia toohello dischi di archiviazione in un secondo. Un'operazione di input/output può essere di lettura o di scrittura, sequenziale o casuale. Le applicazioni OLTP come un sito Web delle vendite al dettaglio online necessitano tooprocess immediatamente le richieste di molti utenti simultanei. le richieste utente Hello sono insert e aggiornare le transazioni di database con utilizzo intensivo, l'applicazione hello deve elaborare rapidamente. Le applicazioni OLTP richiedono quindi valori molto elevati per IOPS. Queste applicazioni gestiscono milioni di richieste I/O di piccole dimensioni e casuali. Se si dispone di un'applicazione, è necessario progettare hello applicazione infrastruttura toooptimize per IOPS. In hello sezione in un secondo momento, *ottimizzazione delle prestazioni delle applicazioni*, verranno illustrate in dettaglio tutti i fattori di hello che è necessario considerare tooget numero elevato di IOPS.

Quando si collega un premium archiviazione disco tooyour su larga scala macchina virtuale, Azure esegue il provisioning per consentire un numero garantito di IOPS in base alla specifica di disco hello. Ad esempio, un disco P50 effettua il provisioning di 7500 IOPS. Ogni dimensione di VM a scalabilità elevata prevede anche un limite di IOPS specifico sostenibile. Ad esempio, una VM GS5 Standard ha un limite di 80.000 IOPS.

## <a name="throughput"></a>Velocità effettiva
Velocità effettiva o larghezza di banda è quantità hello di dati che l'applicazione invia toohello dischi di archiviazione in un intervallo specificato. Se l'applicazione esegue operazioni di input/output con dimensioni elevate per le unità I/O, richiederà una velocità effettiva elevata. Applicazioni del data warehouse tendono tooissue con utilizzo intensivo operazioni di analisi che accedono a grandi porzioni di dati in un momento e in genere eseguono operazioni di massa. In altri termini, queste applicazioni richiedono una velocità effettiva più elevata. Se si dispone di un'applicazione, è necessario progettare il toooptimize infrastruttura per la velocità effettiva. Nella sezione successiva hello, vengono discussi in fattori hello di dettaglio necessario ottimizzare questo tooachieve.

Quando si collega un premium archiviazione disco tooa su larga scala macchina virtuale, Azure esegue il provisioning della velocità effettiva in base a tale specifica del disco. Ad esempio, un disco P50 effettua il provisioning di una velocità effettiva di 250 MB al secondo per il disco. Ogni dimensione di VM a scalabilità elevata prevede anche un limite di velocità effettiva specifico sostenibile. Ad esempio, una VM GS5 Standard ha una velocità effettiva massima di 2.000 MB al secondo. 

C'è una relazione tra la velocità effettiva e IOPS, come illustrato nella formula hello riportato di seguito.

![](media/storage-premium-storage-performance/image1.png)

È pertanto importante toodetermine hello velocità effettiva e IOPS valori ottimali richieste dall'applicazione. Quando si tenta di toooptimize uno, ottiene interessato anche altri hello. In una sezione successiva, *Ottimizzazione delle prestazioni dell'applicazione*, verrà illustrata in modo dettagliato l'ottimizzazione di IOPS e velocità effettiva.

## <a name="latency"></a>Latency
La latenza è hello tempo tooreceive un'applicazione una singola richiesta, inviarlo toohello dischi di archiviazione e inviare hello risposta toohello client. Si tratta di una misura critica di prestazioni di un'applicazione in tooIOPS aggiunta e la velocità effettiva. Hello latenza di un disco di archiviazione premium è ora hello accetta informazioni hello tooretrieve per una richiesta e comunicare nuovamente tooyour applicazione. L'Archiviazione Premium offre latenze uniformemente basse. Se si abilita la memorizzazione nella cache host ReadOnly nei dischi di Archiviazione Premium, sarà possibile ottenere una latenza di lettura molto più bassa. La memorizzazione nella cache dei dischi sarà illustrata in modo più dettagliato nella sezione successiva, *Ottimizzazione delle prestazioni dell'applicazione*.

Quando si ottimizza il tooget applicazione superiore IOPS e la velocità effettiva, influisce negativamente hello latenza dell'applicazione. Dopo l'ottimizzazione delle prestazioni dell'applicazione hello, restituiscono sempre hello latenza di tooavoid applicazione hello comportamento imprevisto ad alta latenza.

## <a name="gather-application-performance-requirements"></a>Recuperare i requisiti dell'applicazione
è innanzitutto Hello nella progettazione di applicazioni ad alte prestazioni in esecuzione in archiviazione Premium di Azure, i requisiti di prestazioni hello toounderstand dell'applicazione. Dopo aver raccolto i requisiti di prestazioni, è possibile ottimizzare le prestazioni dell'applicazione tooachieve hello ottimale.

Nella sezione precedente hello, spiegare hello comuni indicatori di prestazioni, IOPS, velocità effettiva e latenza. È necessario identificare quali di questi indicatori di prestazioni critici tooyour applicazione hello desiderato toodeliver esperienza dell'utente. Ad esempio, numero elevato di IOPS è rilevante la maggior parte delle applicazioni tooOLTP elaborazione milioni di transazioni in un secondo. Una velocità effettiva elevata, invece, è essenziale per applicazioni di tipo data warehouse che elaborano quantità elevate di dati in un secondo. Una latenza estremamente bassa è critica per applicazioni in tempo reale come siti Web per lo streaming di video.

Successivamente, misurare requisiti massimi di prestazioni hello dell'applicazione in tutta la durata. Utilizzare l'elenco di controllo esempio hello sotto come punto di partenza. Requisiti relativi alle prestazioni massime hello record durante il normale, periodi di carico di lavoro di picco e orario di lavoro. Identificazione dei requisiti per tutti i livelli di carichi di lavoro, sarà in grado di toodetermine hello requisito prestazioni complessive dell'applicazione. Ad esempio, hello normale il carico di lavoro di un sito Web di e-commerce sarà transazioni hello che svolge la maggior parte dei giorni in un anno. il carico di lavoro di Hello picco del sito Web di hello sarà transazioni hello che serve durante le feste natalizie o eventi di vendita speciale. carico di picco Hello esperto in genere per un periodo limitato, ma può richiedere il tooscale applicazione due o più volte il normale funzionamento. Individuare percentile 50 hello, 90 ° percentile e i requisiti di percentile 99. Ciò consente di filtrare tutti gli outlier nei requisiti di prestazioni hello e sarà possibile concentrare l'attenzione sull'ottimizzazione per i valori corretti di hello.

**Elenco di controllo per i requisiti relativi alle prestazioni dell'applicazione**

| **Requisiti relativi alle prestazioni** | **50° percentile** | **90° percentile** | **99° percentile** |
| --- | --- | --- | --- |
| Max. Transazioni al secondo | | | |
| % di operazioni di lettura | | | |
| % di operazioni di scrittura | | | |
| % di operazioni casuali | | | |
| % di operazioni sequenziali | | | |
| Dimensioni delle richieste I/O | | | |
| Velocità effettiva media | | | |
| Max. Velocità effettiva | | | |
| Min Latency | | | |
| Latenza media | | | |
| Max. CPU | | | |
| Utilizzo medio CPU | | | |
| Max. Memoria | | | |
| Memoria media | | | |
| Profondità coda | | | |

> [!NOTE]
> è consigliabile prendere in considerazione il ridimensionamento di questi numeri sulla base della crescita futura prevista per l'applicazione. È un tooplan buona crescita anticipatamente, perché potrebbe essere più difficile l'infrastruttura di hello toochange per migliorare le prestazioni in un secondo momento.
>
>

Se si dispone di un'applicazione esistente e si desidera toomove tooPremium archiviazione, è innanzitutto necessario generare hello elenco di controllo sopra per un'applicazione hello esistente. Quindi, compilare un prototipo di un'applicazione in un'applicazione hello archiviazione Premium e di progettazione in base alle linee guida descritte in *ottimizzazione delle prestazioni dell'applicazione* in una sezione successiva di questo documento. Nella sezione successiva Hello vengono descritti gli strumenti di hello è possibile utilizzare le misurazioni delle prestazioni toogather hello.

Creare un'elenco di controllo simile tooyour applicazione esistente per il prototipo di hello. Utilizzando gli strumenti di Benchmarking è possibile simulare carichi di lavoro hello e misurare le prestazioni in un'applicazione hello prototipo. Vedere la sezione hello [Benchmarking](#benchmarking) toolearn altre. Sarà quindi possibile determinare se l'Archiviazione Premium può soddisfare o sorpassare i requisiti relativi alle prestazioni per l'applicazione. È possibile implementare hello stesse linee guida per l'applicazione di produzione.

### <a name="counters-toomeasure-application-performance-requirements"></a>Contatori toomeasure requisiti delle prestazioni dell'applicazione
requisiti di prestazioni toomeasure modo ottimali dell'applicazione Hello, strumenti di monitoraggio delle prestazioni toouse forniti dal sistema operativo hello del server di hello. È possibile usare PerfMon per Windows e iostat per Linux. Questi strumenti acquisiscono i contatori corrispondenti tooeach misure illustrate in hello sopra la sezione. Quando l'applicazione è in esecuzione la normale, i carichi di lavoro di picco e orario di lavoro, è necessario acquisire i valori hello di questi contatori.

contatori di PerfMon Hello sono disponibili per il processore, memoria e ogni disco logico e un disco fisico del server. Quando si usano i dischi di archiviazione premium con una macchina virtuale, contatori del disco fisico hello sono per ogni disco di archiviazione premium e contatori del disco logico sono per ogni volume creati nei dischi di archiviazione premium hello. È necessario acquisire i valori hello per i dischi di hello che ospitano il carico di lavoro dell'applicazione. Se è presente un mapping di tooone uno tra i dischi logici e fisici, è possibile fare riferimento a contatori del disco toophysical; in caso contrario, consultare i contatori del disco logico toohello. In Linux, il comando di iostat hello genera un report di utilizzo della CPU e disco. report utilizzo dischi di Hello fornisce statistiche per ogni dispositivo fisico o partizione. Se è presente un server di database con dati e log in dischi separati, raccogliere questi dati per entrambi i dischi. La tabella seguente illustra i contatori per dischi, processore e memoria:

| Contatore | Descrizione | PerfMon | Iostat |
| --- | --- | --- | --- |
| **IOPS o transazioni al secondo** |Numero di richieste dei / o emessi toohello su disco di archiviazione al secondo. |Letture disco/sec  <br> Scritture disco/sec |tps  <br> r/s  <br> w/s |
| **Letture e scritture del disco** |% di letture e le operazioni eseguite su disco hello di scrittura. |% Tempo lettura disco  <br> % Tempo scrittura disco |r/s  <br> w/s |
| **Velocità effettiva** |Quantità di dati lette o scritte su disco toohello al secondo. |Byte letti da disco/sec  <br> Byte scritti su disco/sec |kB_read/s <br> kB_wrtn/s |
| **Latency** |Numero totale di tempo toocomplete una richiesta dei / o disco. |Media letture disco/sec  <br> Media scritture disco/sec |await  <br> svctm |
| **Dimensioni I/O** |dimensione Hello delle richieste dei / o problemi toohello dischi di archiviazione. |Media byte letti da disco  <br> Media byte scritti su disco |avgrq-sz |
| **Profondità coda** |Numero dei / o in attesa di richieste in attesa toobe lettura modulo o la scrittura su disco di archiviazione toohello. |Lunghezza corrente coda su disco |avgqu-sz |
| **Max. memoria** |Quantità di memoria richiesta toorun applicazione in modo uniforme |% byte vincolati in uso |Use vmstat |
| **Max. CPU** |Quantità di CPU richiesto toorun applicazione in modo uniforme |% tempo processore |%util |

Altre informazioni su [iostat](http://linuxcommand.org/man_pages/iostat1.html) e [PerfMon](https://msdn.microsoft.com/library/aa645516.aspx).

## <a name="optimizing-application-performance"></a>Ottimizzazione delle prestazioni dell'applicazione
i fattori principali Hello che influenzano le prestazioni di un'applicazione in esecuzione in archiviazione Premium sono di natura dei / o richieste, dimensioni della macchina virtuale, dimensioni del disco, numero di dischi, la cache del disco, Multithreading e profondità della coda. È possibile controllare alcuni di questi fattori con manopole fornite dal sistema hello. La maggior parte delle applicazioni potrebbero non produrre un hello tooalter opzione dimensioni i/o e la profondità della coda direttamente. Ad esempio, se si utilizza SQL Server, è possibile scegliere di profondità di dimensioni e la coda dei / o hello. SQL Server sceglie hello ottimale IO dimensioni e la coda profondità valori tooget hello la maggior parte delle prestazioni. È importante toounderstand hello impatto di entrambi i tipi di fattori le prestazioni dell'applicazione, in modo che è possibile eseguire il provisioning delle risorse appropriate toomeet le esigenze di prestazioni.

In questa sezione, vedere toohello applicazione requisiti di sistema per cui è stato creato, tooidentify quanto è necessario toooptimize le prestazioni dell'applicazione. In base che sarà in grado di toodetermine quali fattori in questa sezione sarà necessario tootune. toowitness hello gli effetti di ogni fattore sulle prestazioni dell'applicazione, eseguire prove comparative gli strumenti di installazione dell'applicazione. Fare riferimento toohello [Benchmarking](#Benchmarking) sezione alla fine di hello di questo articolo per toorun passaggi comuni strumenti di Windows e le macchine virtuali Linux di benchmarking.

### <a name="optimizing-iops-throughput-and-latency-at-a-glance"></a>Breve panoramica sull'ottimizzazione di IOPS, velocità effettiva e latenza
tabella Hello seguente riepiloga i fattori relativi alle prestazioni hello tutte e hello passaggi toooptimize IOPS, velocità effettiva e latenza. Hello sezioni seguenti questo riepilogo descrivono ogni fattore è molto più approfondito.

| &nbsp; | **IOPS** | **Velocità effettiva** | **Latency** |
| --- | --- | --- | --- |
| **Scenario di esempio** |Applicazione OLTP aziendale che richiede una frequenza molto elevata di transazioni al secondo. |Applicazione aziendale di tipo data warehouse che elabora quantità elevate di dati. |Quasi in tempo reale applicazioni richiedono le richieste di toouser risposte immediata, ad esempio giochi online. |
| Fattori relativi alle prestazioni | &nbsp; | &nbsp; | &nbsp; |
| **Dimensioni I/O** |Dimensioni I/O ridotte producono valori superiori per IOPS. |Tooyields di dimensioni dei / o maggiore velocità effettiva più elevata. | &nbsp;|
| **Dimensioni macchina virtuale** |Usare una dimensione di VM che offre IOPS superiori ai requisiti dell'applicazione. Per informazioni sulle dimensioni delle VM e i relativi limiti di IOPS, vedere qui. |Usare una dimensione di VM con un limite di velocità effettiva superiore ai requisiti dell'applicazione. Per informazioni sulle dimensioni delle VM e i relativi limiti di velocità effettiva, vedere qui. |Usare una dimensione di VM che offre limiti di ridimensionamento superiori ai requisiti dell'applicazione. Per informazioni sulle dimensioni delle VM e i relativi limiti, vedere qui. |
| **Dimensioni disco** |Usare una dimensione di disco che offre IOPS superiori ai requisiti dell'applicazione. Per informazioni sulle dimensioni dei dischi e i relativi limiti di IOPS, vedere qui. |Usare una dimensione di disco con un limite di velocità effettiva superiore ai requisiti dell'applicazione. Per informazioni sulle dimensioni dei dischi e i relativi limiti di velocità effettiva, vedere qui. |Usare una dimensione di disco che offre limiti di ridimensionamento superiori ai requisiti dell'applicazione. Per informazioni sulle dimensioni dei dischi e i relativi limiti, vedere qui. |
| **Limiti relativi al ridimensionamento di VM e dischi** |Limite di IOPS della scelta di dimensioni VM hello deve essere maggiore del totale di IOPS dovute ai dischi di archiviazione premium collegato tooit. |Limite di velocità effettiva della scelta di dimensioni VM hello deve essere maggiore della velocità effettiva totale dovuta ai dischi di archiviazione premium collegato tooit. |I limiti di scalabilità della scelta di dimensioni VM hello devono essere maggiori di limiti di scalabilità totale premium collegati dei dischi di archiviazione. |
| **Memorizzazione nella cache del disco** |Abilitare la Cache di sola lettura nei dischi di archiviazione premium con tooget onerose operazioni di lettura superiori IOPS di lettura. | &nbsp; |Abilitare la Cache di sola lettura nei dischi di archiviazione premium con latenze di lettura pronto onerose operazioni tooget molto basse. |
| **Striping del disco** |Utilizzo di più dischi ed eseguire lo striping insieme tooget un'operazione di IOPS maggiore combinato e il limite di velocità effettiva. Si noti che hello limite combinato per ogni macchina virtuale devono essere superiori a quello hello combinati i limiti di dischi collegati premium. | &nbsp; | &nbsp; |
| **Dimensioni di striping** |Dimensioni di striping ridotte per modelli di I/O casuali presenti in applicazioni OLTP. Ad esempio, usare dimensioni di striping pari a 64 KB per un'applicazione OLTP di SQL Server. |Dimensioni di striping superiori per modelli di I/O sequenziali di grandi dimensioni presenti in applicazioni di tipo data warehouse. Ad esempio, usare dimensioni di striping pari a 256 KB per applicazioni SQL Server di tipo data warehouse. | &nbsp; |
| **Multithreading** |Utilizzare il multithreading toopush un numero superiore di richieste tooPremium archiviazione che potrebbero causare toohigher IOPS e la velocità effettiva. Ad esempio, in SQL Server impostato un'elevata tooallocate valore MAXDOP tooSQL CPU più Server. | &nbsp; | &nbsp; |
| **Profondità coda** |Una profondità maggiore per la coda genera valori più elevati per IOPS. |Una profondità maggiore per la coda genera valori più elevati per la velocità effettiva. |Una profondità minore per la coda genera latenze più basse. |

## <a name="nature-of-io-requests"></a>Natura delle richieste I/O
Una richiesta I/O è un'unità di operazioni di input/output che verrà eseguita dall'applicazione. Identificazione di natura hello di richieste dei / o casuali o sequenziale, di lettura o scrittura, piccola o grande, consentirà di determinare i requisiti di prestazioni hello dell'applicazione. È molto importante toounderstand natura hello delle richieste dei / o, toomake hello destra decisioni appropriate durante la progettazione dell'infrastruttura dell'applicazione.

Dimensioni dei / o è uno dei hello fattori più importanti. dimensioni dei / o Hello è dimensioni hello della richiesta di operazione di input/output di hello generato dall'applicazione. Hello dimensioni i/o ha un impatto significativo sulle prestazioni, soprattutto sulle hello IOPS e larghezza di banda hello applicazione è in grado di tooachieve. Hello formula seguente viene illustrata hello relazione tra IOPS, della larghezza di banda/velocità effettiva e dimensioni dei / o.  
    ![](media/storage-premium-storage-performance/image1.png)

Alcune applicazioni consentono le operazioni dei / o modificare le dimensioni, mentre alcune applicazioni non tooalter. Ad esempio, SQL Server determina hello IO sulle dimensioni ottimali se stesso e non fornisce agli utenti con qualsiasi toochange manopole è. In hello invece, Oracle fornisce un parametro denominato [DB\_blocco\_dimensioni](https://docs.oracle.com/cd/B19306_01/server.102/b14211/iodesign.htm#i28815) tramite il quale è possibile configurare hello dimensione richiesta dei / o del database hello.

Se si utilizza un'applicazione, che non si toochange hello dimensioni i/o, utilizzare le linee guida hello in questo articolo toooptimize hello delle prestazioni indicatore KPI che applicazione tooyour più rilevanti. Ad esempio,

* Un'applicazione OLTP genera milioni di richieste I/O piccole e casuali. toohandle questi tipo dei / o richieste, è necessario progettare il tooget infrastruttura applicazione IOPS superiore.  
* Un'applicazione di tipo data warehouse genera richieste I/O di grandi dimensioni e sequenziali. toohandle questi tipo di richieste dei / o, è necessario progettare l'infrastruttura di applicazioni tooget maggiore larghezza di banda o una velocità effettiva.

Se si utilizza un'applicazione, che consenta di dimensioni dei / o toochange hello, usare questa regola empirica per hello IO dimensioni inoltre linee guida sulle prestazioni tooother,

* Tooget di dimensioni più piccole operazioni i/o IOPS superiore. Ad esempio, 8 KB per un'applicazione OLTP.  
* Tooget di dimensioni dei / o maggiore della larghezza di banda superiore la velocità effettiva. Ad esempio, 1024 KB per un'applicazione di tipo data warehouse.

Di seguito è riportato un esempio su come è possibile calcolare hello IOPS e la larghezza di banda/velocità effettiva per l'applicazione. Prendere in considerazione un'applicazione che usa un disco P30. Hello numero massimo di IOPS e velocità effettiva/larghezza di banda possibile ottenere un disco P30 è 5000 IOPS e 200 MB al secondo. A questo punto, se l'applicazione richiede hello che numero massimo di IOPS da disco hello P30 e utilizza una dimensione più piccola dei / o come 8 KB, hello risultante sarà la larghezza di banda in grado di tooget è 40 MB al secondo. Tuttavia, se l'applicazione richiede una velocità effettiva/larghezza di banda massima dal disco P30 hello e si utilizza una dimensione maggiore dei / o come 1024 KB, hello IOPS risultante sarà minore, 200 IOPS. Pertanto, l'ottimizzazione di dimensioni dei / o hello in modo che soddisfi i requisiti di IOPS e velocità effettiva/larghezza di banda sia dell'applicazione. Nella tabella seguente sono riepilogate diverse dimensioni dei / o hello e IOPS e corrispondenti velocità effettiva di un disco P30.

| Requisiti dell'applicazione | Dimensioni di I/O | IOPS | Velocità effettiva/Larghezza di banda |
| --- | --- | --- | --- |
| Operazioni di I/O al secondo max |8 KB |5.000 |40 MB al secondo |
| Velocità effettiva massima |1024 KB |200 |200 MB al secondo |
| Velocità effettiva massima + IOPS elevati |64 KB |3.200 |200 MB al secondo |
| IOPS massimi + Velocità effettiva elevata |32 KB |5.000 |160 MB al secondo |

tooget IOPS e larghezza di banda superiore al valore massimo di hello di un disco di archiviazione premium singolo, utilizzare più dischi premium con striping. Ad esempio, eseguire lo striping due P30 dischi tooget un IOPS combinato di 10.000 IOPS o una velocità effettiva di combinato di 400 MB al secondo. Come illustrato nella sezione successiva di hello, è necessario utilizzare una dimensione di macchina virtuale che supporta il disco di hello combinato IOPS e la velocità effettiva.

> [!NOTE]
> Quando si aumenta l'IOPS o aumenta anche altri hello velocità effettiva, assicurarsi che non rilevamento di velocità effettiva o limiti IOPS di hello disco o di macchina virtuale quando viene incrementato di uno.
>
>

toowitness hello gli effetti delle dimensioni dei / o sulle prestazioni dell'applicazione, è possibile eseguire gli strumenti benchmark nelle macchine Virtuali e dischi. Creare più esecuzioni dei test e utilizzare dimensioni i/o diverse per ogni impatto hello toosee esecuzione. Fare riferimento toohello [Benchmarking](#Benchmarking) sezione alla fine di hello di questo articolo per ulteriori dettagli.

## <a name="high-scale-vm-sizes"></a>Dimensioni di VM a scalabilità elevata
Quando si avvia la progettazione di un'applicazione, uno di hello prima cose toodo è, scegliere toohost una macchina virtuale dell'applicazione. L'Archiviazione Premium include dimensioni di VM a scalabilità elevata in grado di eseguire applicazioni che richiedono capacità di calcolo elevate e prestazioni di I/O elevate per il disco locale. Queste macchine virtuali offrono processori più veloci, un rapporto memoria-core superiore e allo stato solido unità SSD per disco locale hello. Esempi di macchine virtuali di scala elevata supporto archiviazione Premium sono hello, DSv2 serie DS e GS macchine virtuali.

Le VM a scalabilità elevata sono disponibili in dimensioni diverse con un numero diverso di core CPU, memoria, sistema operativo e dimensioni del disco temporaneo. Ogni dimensione della macchina virtuale è anche il numero massimo di dischi dati che è possibile collegare toohello macchina virtuale. Pertanto, dimensioni della macchina virtuale hello scelto influirà quanta capacità di elaborazione, memoria e archiviazione è disponibile per l'applicazione. Influisce inoltre hello calcolo e i costi di archiviazione. Ad esempio, di seguito sono specifiche di hello hello più grande delle dimensioni delle VM in una serie di dominio Active Directory, DSv2 serie e una serie di GS:

| Dimensioni macchina virtuale | Core CPU | Memoria | Dimensioni di disco della VM | Max. dischi dati | Dimensioni cache | IOPS | Limiti di I/O della cache della larghezza di banda |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS14 |16 |112 GB |Sistema operativo = 1023 GB  <br> SSD locale = 224 GB |32 |576 GB |50.000 IOPS  <br> 512 MB al secondo |4.000 IOPS e 33 MB al secondo |
| Standard_GS5 |32 |448 GB |Sistema operativo = 1023 GB  <br> SSD locale = 896 GB |64 |4224 GB |80.000 IOPS  <br> 2.000 MB al secondo |5.000 IOPS e 50 MB al secondo |

tooview un elenco completo di tutte le dimensioni delle macchine Virtuali di Azure disponibili, fare riferimento troppo[dimensioni delle macchine Virtuali di Windows](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [le dimensioni di VM Linux](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Scegliere una dimensione di macchina virtuale in grado di soddisfare e scala tooyour desiderato requisiti delle prestazioni dell'applicazione. Inoltre, toothis, prendere in considerazione seguenti considerazioni importanti quando si sceglie di dimensioni delle macchine Virtuali.

*Limiti di scalabilità*  
Hello IOPS i limiti massimi per ogni macchina virtuale e per ogni disco sono diversi e indipendenti tra loro. Assicurarsi che l'applicazione hello sta lanciando IOPS entro i limiti di hello di hello VM, nonché hello premium dischi collegati tooit. In caso contrario, le prestazioni dell'applicazione verranno limitate.

Si supponga, ad esempio, che i requisiti dell'applicazione siano pari a 4.000 IOPS. tooachieve, questo è il provisioning un disco P30 in una macchina virtuale DS1. disco P30 Hello grado di portare too5, IOPS 000. Tuttavia, hello DS1 VM è limitato too3, 200 IOPS. Di conseguenza, le prestazioni dell'applicazione hello saranno vincolata dal limite di VM hello in 3.200 IOPS e il calo delle prestazioni. tooprevent questa situazione, scegliere una macchina virtuale e dimensioni che verranno entrambi applicazione soddisfa i requisiti del disco.

*Costo operativo*  
In molti casi è possibile che il costo operativo complessivo con l'Archiviazione Premium sia inferiore al costo dell'uso dell'Archiviazione Standard.

Ad esempio, si consideri un'applicazione che richiede 16.000 IOPS. tooachieve queste prestazioni, è necessario uno Standard\_D14 Azure IaaS con macchina virtuale, che può concedere a un numero massimo di IOPS di 16.000 con 32 dischi di 1 TB di archiviazione standard. Ogni disco di archiviazione Standard da 1 TB può raggiungere un valore massimo di 500 IOPS. Hello stimato costo di questa macchina virtuale al mese sarà $1,570. Costo mensile di Hello 32 standard dei dischi di archiviazione sarà $1,638. Hello stimato totale mensile sarà $3,208.

Tuttavia, se è ospitato hello stessa applicazione in archiviazione Premium, è necessario una dimensione di macchina virtuale più piccola e meno i dischi di archiviazione premium, riducendo in tal modo hello costo complessivo. Standard\_DS13 VM grado di soddisfare il requisito di IOPS hello 16.000 utilizzando quattro dischi P30. ogni disco P30 è un numero massimo di IOPS di 5.000 Hello DS13 VM è un numero massimo di IOPS di 25,600. Questa configurazione consente complessivamente di ottenere 5.000 x 4 = 20.000 IOPS. Hello stimato costo di questa macchina virtuale al mese sarà $1,003. Costo mensile di Hello di quattro dischi di archiviazione premium P30 sarà $544.34. Hello stimato totale mensile sarà $1,544.

Nella tabella seguente sono riepilogate hello la scomposizione dei costi di questo scenario di Standard e di archiviazione Premium.

| &nbsp; | **Standard** | **Premium** |
| --- | --- | --- |
| **Costo di VM al mese** |$1.570,58 (Standard\_D14) |$1.003,66 (Standard\_DS13) |
| **Costo di dischi al mese** |$ 1.638,40 (32 x dischi da 1 TB) |$ 544,34 (4 x dischi P30) |
| **Costo complessivo al mese** |$ 3.208,98 |$ 1.544,34 |

*Distribuzioni Linux*  

Con archiviazione Premium di Azure, si otterrà hello stesso livello di prestazioni per le macchine virtuali che eseguono Windows e Linux. Sono supportati molti tipi di distribuzioni Linux, ed è possibile visualizzare l'elenco completo di hello [qui](../../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). È importante che diverse distribuzioni sono migliori toonote adatto per diversi tipi di carichi di lavoro. Verranno visualizzati diversi livelli di prestazioni a seconda della distribuzione hello che in cui è in esecuzione il carico di lavoro. Le distribuzioni di Linux hello con l'applicazione di test e scegliere hello uno che funziona in modo ottimale.

Quando si esegue Linux con archiviazione Premium, verificare gli aggiornamenti più recenti di hello sulle prestazioni elevate di tooensure i driver necessari.

## <a name="premium-storage-disk-sizes"></a>Dimensioni dei dischi di Archiviazione Premium
L'Archiviazione Premium di Azure offre attualmente sette dimensioni di disco. Ogni dimensione di disco ha un limite di scala diverso per IOPS, larghezza di banda e archiviazione. Scegliere le dimensioni del disco di archiviazione Premium destra di hello in base a requisiti dell'applicazione hello e su larga scala hello dimensioni della macchina virtuale. tabella Hello seguente mostra le dimensioni di sette dischi hello e le relative funzionalità. Le dimensioni di disco P4 e P6 sono attualmente supportate solo per Managed Disks.

| Tipo di disco Premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Dimensioni disco           | 32 GB | 64 GB | 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| IOPS per disco       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Velocità effettiva per disco | 25 MB al secondo  | 50 MB al secondo  | 100 MB al secondo | 150 MB al secondo | 200 MB al secondo | 250 MB al secondo | 250 MB al secondo | 


Il numero di dischi scelto dipende dal disco hello dimensioni definite. È possibile utilizzare un singolo disco P50 o più P10 dischi toomeet il requisito per un'applicazione. Prendono in considerazioni sull'account elencati di seguito quando si effettua una scelta hello.

*Limiti di scalabilità (IOPS e velocità effettiva)*  
limiti di velocità effettiva e IOPS Hello di ogni dimensione del disco Premium è diversa e indipendente dal hello limiti di scalabilità di macchine Virtuali. Verificare che hello totale di IOPS e velocità effettiva da dischi hello vengono scelti entro i limiti di scala di hello dimensioni della macchina virtuale.

Ad esempio, si supponga che un requisito di applicazione preveda una velocità effettiva massima di 250 MB/sec e si usi una VM DS4 con un singolo disco P30. Hello DS4 VM consentono di velocità effettiva di too256 MB/sec. Tuttavia, un singolo disco P30 ha un limite di velocità effettiva di 200 MB/sec. Di conseguenza, un'applicazione hello sarà vincolata a 200 MB al secondo a causa di limite disco toohello. tooovercome questo limite, il provisioning toohello dischi di dati più di una macchina virtuale o ridimensionare i dischi tooP40 o P50.

> [!NOTE]
> Letture servite dalla cache di hello non presenti nel disco hello IOPS e la velocità effettiva, pertanto non soggetto toodisk limiti. La cache ha un limite di IOPS e velocità effettiva specifico per ogni VM.
>
> Ad esempio, le operazioni di lettura e scrittura iniziali sono rispettivamente pari a 60 MB/sec e 40 MB/sec. Nel corso del tempo, cache di hello riscaldamento e serve di hello letture dalla cache di hello. Quindi, è possibile ottenere la velocità effettiva di scrittura superiore dal disco hello.
>
>

*Numero di dischi*  
Determinare il numero di hello dei dischi che sarà necessario a valutare i requisiti dell'applicazione. Ogni dimensione della macchina virtuale ha anche un limite sul numero di hello di dischi che è possibile collegare toohello macchina virtuale. In genere, si tratta di due volte hello numero di core. Verificare che hello prescelto può supportare hello numero di dischi necessari dimensioni della macchina virtuale.

Tenere presente che i dischi di archiviazione Premium hello dispongono di più dischi di archiviazione tooStandard di funzionalità rispetto delle prestazioni. Pertanto, se si esegue la migrazione dell'applicazione dalla macchina virtuale IaaS di Azure tramite archiviazione Standard tooPremium archiviazione, sarà probabilmente necessario meno i dischi premium tooachieve hello prestazioni uguale o superiore per l'applicazione.

## <a name="disk-caching"></a>Memorizzazione nella cache del disco
Le VM a scalabilità elevata che sfruttano i vantaggi dell'Archiviazione Premium di Azure includono una tecnologia di memorizzazione nella cache multilivello denominata BlobCache. BlobCache utilizza una combinazione di macchina virtuale RAM hello e unità SSD locale per la memorizzazione nella cache. Questa cache è disponibile per i dischi persistenti di archiviazione Premium hello e dischi locali di hello macchina virtuale. Per impostazione predefinita, questa impostazione della cache è tooRead/scrittura per i dischi del sistema operativo e sola lettura per i dischi dati ospitati in archiviazione Premium. Con la cache del disco attivata su dischi di archiviazione Premium hello, su larga scala hello macchine virtuali possa ottenere livelli estremamente elevati di prestazioni che superano le prestazioni del disco sottostante hello.

> [!WARNING]
> Modifica l'impostazione della cache di hello di un disco di Azure si disconnette e aggiunge di nuovo il disco di destinazione hello. In caso di disco del sistema operativo hello, hello VM viene riavviata. Arrestare tutte le applicazioni/servizi che potrebbero essere interessati da questa interruzione prima di modificare l'impostazione della cache di hello disco.
>
>

toolearn ulteriori informazioni su come funziona BlobCache, fare riferimento toohello all'interno di [archiviazione Premium di Azure](https://azure.microsoft.com/blog/azure-premium-storage-now-generally-available-2/) post di blog.

È importante tooenable cache set corretto di hello dei dischi. Se è necessario abilitare la cache del disco in un disco premium o non dipenderà il modello di carico di lavoro hello tale disco gestiscono. Tabella riportata di seguito viene illustrato come predefinito hello le impostazioni della cache per i dischi del sistema operativo e dati.

| **Tipo di disco** | **Impostazione predefinita per la cache** |
| --- | --- |
| Disco del sistema operativo |ReadWrite |
| Disco dati |Nessuno |

Seguenti sono hello le impostazioni della cache su disco consigliato per i dischi dati,

| **Impostazione per la memorizzazione nella cache su disco** | **Indicazioni su quando toouse questa impostazione** |
| --- | --- |
| Nessuno |Configurare la cache host come None per dischi di sola scrittura e dischi con numero elevato di operazioni di scrittura. |
| ReadOnly |Configurare la cache host come ReadOnly per dischi di sola lettura e di lettura-scrittura. |
| ReadWrite |Configurare cache dell'host come ReadWrite solo se l'applicazione gestisca correttamente la scrittura nella cache i dischi dati toopersistent quando necessario. |

*ReadOnly*  
Configurando la memorizzazione nella cache ReadOnly nei dischi dati di Archiviazione Premium, è possibile ottenere una latenza di lettura bassa e valori molto elevati di IOPS e velocità effettiva di lettura per l'applicazione. Questo è dovuto ai due motivi seguenti:

1. Letture eseguite dalla cache, che si trova in memoria della macchina virtuale hello e unità SSD locale, sono molto più veloce rispetto letture da disco dati hello, che si trova in hello archiviazione blob di Azure.  
2. Archiviazione Premium non inclusi nel conteggio hello letture soddisfatte dalla cache, verso il disco di hello IOPS e la velocità effettiva. Pertanto, l'applicazione è in grado di tooachieve superiore totale di IOPS e la velocità effettiva.

*ReadWrite*  
Per impostazione predefinita, i dischi del sistema operativo hello abbiano abilitata la memorizzazione nella cache ReadWrite. È stato recentemente aggiunto il supporto per la memorizzazione nella cache ReadWrite anche sui dischi dati. Se si utilizza la memorizzazione nella cache di lettura/scrittura, è necessario disporre di un metodo migliore toowrite hello di dati dai dischi toopersistent cache. Ad esempio, gli handle SQL Server la scrittura memorizzati nella cache di dischi di archiviazione permanente dati toohello autonomamente. L'utilizzo della cache di lettura/scrittura con un'applicazione che non gestisce la persistenza hello necessario dei dati può causare la perdita di toodata, se si blocca hello VM.

Ad esempio, è possibile applicare questi tooSQL linee guida Server in esecuzione in archiviazione Premium procedendo come indicato di seguito hello,

1. Configurare la cache "ReadOnly" nei dischi di Archiviazione Premium che ospitano i file di dati.  
   a.  Hello veloce letta la fase di query di cache inferiore hello SQL Server perché le pagine di dati vengono recuperate più velocemente da hello cache confrontata toodirectly dai dischi dati hello.  
   b.  Le fornitura delle letture dalla cache consente di rendere disponibile velocità effettiva aggiuntiva dai dischi dati Premium. SQL Server può usare questa velocità effettiva aggiuntiva per recuperare un numero superiore di pagine di dati e altre operazioni come il backup/ripristino, i carichi in batch e le ricompilazioni degli indici.  
2. Configurare "None" cache in archiviazione premium dischi host i file di log hello.  
   a.  I file di log hanno principalmente operazioni intensive a livello di lettura. Pertanto, non usano hello cache di sola lettura.

## <a name="disk-striping"></a>Striping del disco
Quando è possibile un'elevata scalabilità che macchina virtuale è collegata con diversi premium archiviazione permanente, dischi hello striping tooaggregate loro IOPs, della larghezza di banda e capacità di archiviazione.

In Windows, è possibile utilizzare i dischi toostripe spazi di archiviazione. È necessario configurare una colonna per ogni disco in un pool. In caso contrario, hello prestazioni complessive del volume con striping possono essere inferiore al previsto, a causa di toouneven distribuzione del traffico tra dischi hello.

Importante: Utilizzando Server Manager UI, è possibile impostare hello totale colonne backup too8 per un volume con striping. Se si installa più di 8 dischi, utilizzare volume hello toocreate di PowerShell. Tramite PowerShell, è possibile impostare il numero di hello di colonne uguale toohello numero di dischi. Ad esempio, se sono presenti 16 dischi in un set di striping singolo. specificare 16 colonne in hello *NumberOfColumns* parametro di hello *New-VirtualDisk* cmdlet di PowerShell.

In Linux, usare i dischi di hello MDADM utilità toostripe insieme. Per i passaggi dettagliati per i dischi di striping in Linux, vedere troppo[configurare RAID Software in Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

*Dimensioni di striping*  
Una configurazione più rilevanti nello striping del disco è la dimensione di striping hello. dimensione di striping Hello o dimensione del blocco è blocco più piccolo di hello di dati che l'applicazione può risolvere in un volume con striping. dimensione di striping Hello che configuri dipende dal tipo di hello dell'applicazione e il modello di richiesta. Se si sceglie una dimensione di striping non corretto di hello, può causare problemi di allineamento tooIO, con un conseguente toodegraded delle prestazioni dell'applicazione.

Ad esempio, se una richiesta dei / o generata dall'applicazione è maggiore di dimensione di striping del disco hello, sistema di archiviazione hello scrive tra stripe i limiti di unità in più di un disco. Quando è ora tooaccess tali dati, si otterrà tooseek tra più di una striscia unità toocomplete hello richiesta. effetto cumulativo di Hello di tale comportamento può causare un calo delle prestazioni toosubstantial. In hello se hello dimensione richiesta dei / o è minore di dimensione di striping e se è casuale, le richieste dei / o hello potrebbero sommare su hello stesso invece del disco causando un collo di bottiglia e infine compromettere le prestazioni dei / o hello.

A seconda del carico di lavoro di tipo hello è in esecuzione l'applicazione, scegliere una dimensione di striping appropriato. Per richieste I/O di piccole dimensioni e casuali, usare una dimensione di striping minore. Per richieste I/O di grandi dimensioni e sequenziali, usare una dimensione di striping maggiore. Scoprire hello stripe dimensioni consigliate per l'applicazione hello che verrà eseguita in archiviazione Premium. Per SQL Server configurare dimensioni di striping pari a 64 KB per carichi di lavoro OLTP e 256 KB per carichi di lavoro di tipo data warehouse. Vedere [procedure consigliate per SQL Server in macchine virtuali di Azure](../../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md#disks-guidance) toolearn altre.

> [!NOTE]
> è possibile effettuare lo striping di un massimo di 32 dischi di Archiviazione Premium in una VM di serie DS e di 64 dischi di Archiviazione Premium in una VM di serie GS.
>
>

## <a name="multi-threading"></a>Multithreading
Azure è progettato archiviazione Premium piattaforma toobe parallela massiva. Un'applicazione multithreading ottiene prestazioni molto più elevate rispetto a un'applicazione a thread singolo. Un'applicazione multithreading suddivide le attività tra più thread e aumenta l'efficienza dell'esecuzione da hello utilizzo macchina virtuale e disco risorse toohello massimo.

Ad esempio, se l'applicazione è in esecuzione su un singolo core VM utilizzando due thread, hello CPU possibile alternare efficienza tooachieve due thread di hello. Mentre un thread è in attesa un toocomplete IO disco, hello CPU passare toohello altri thread. In questo modo, due thread possono ottenere molto di più rispetto a un singolo thread. Se hello VM ha più di un core, riduce ulteriormente tempo di esecuzione, poiché ogni core può eseguire le attività in parallelo.

Potrebbe non essere modo hello toochange in grado di un'applicazione preconfigurata implementa single threading o multithreading. Ad esempio, SQL Server è in grado di gestire più CPU e più core. Tuttavia, SQL Server decide quali condizioni verrà utilizzati uno o più thread tooprocess una query. Può eseguire query e compilare indici usando il multithreading. Per una query che include un join di tabelle di grandi dimensioni e l'ordinamento dei dati prima della restituzione toohello utente, SQL Server utilizzerà probabilmente più thread. Un utente non può tuttavia controllare se SQL Server esegue una query usando un singolo thread o più thread.

Sono disponibili le impostazioni di configurazione che è possibile modificare tooinfluence questo multithreading o parallelo l'elaborazione di un'applicazione. Ad esempio, in caso di SQL Server è configurazione grado di parallelismo massimo hello. Questa impostazione di MAXDOP, consente di numero massimo di hello tooconfigure di SQL Server può utilizzare durante l'elaborazione parallela di processori. È possibile configurare MAXDOP per singole query o per operazioni sull'indice. Ciò è utile quando si desidera toobalance risorse di sistema per un'applicazione critica di prestazioni.

Se ad esempio, l'applicazione utilizzando SQL Server è in esecuzione una query di grandi dimensioni e un'operazione di indice in hello contemporaneamente. Si supponga che si desiderava hello indice operazione toobe più query di grandi dimensioni toohello ad alte prestazioni confrontati. In tal caso, è possibile impostare il valore MAXDOP di hello toobe operazione di indice maggiore hello valore MAXDOP per query hello. In questo modo, SQL Server disponga di un numero maggiore di processori che è possibile sfruttare per numero di processori, è possibile dedicare hello indice operazioni confrontati toohello toohello query di grandi dimensioni. Tenere presente che non si controlla il numero di hello di thread di SQL Server verrà utilizzata per ogni operazione. È possibile controllare hello il numero massimo di processori da dedicati per il multithreading.

Altre informazioni sui [Gradi di parallelismo](https://technet.microsoft.com/library/ms188611.aspx) in SQL Server. Individuare tali impostazioni che determinano il multithreading nell'applicazione e delle relative prestazioni toooptimize configurazioni.

## <a name="queue-depth"></a>Profondità coda
Hello profondità della coda o lunghezza della coda o dimensione della coda è numero hello di richieste dei / o in sospeso nel sistema hello. il valore di Hello la profondità della coda determina il numero di operazioni possibile allineare l'applicazione, verranno elaborati i dischi di archiviazione hello. Influisce su tutti hello tre applicazioni gli indicatori di prestazioni cui abbiamo discusso in bastano questo articolo, IOPS, velocità effettiva e latenza.

La profondità della coda e il multithreading sono strettamente correlati. il valore di profondità della coda di Hello indica quanti multithreading può essere ottenuto da un'applicazione hello. Se la profondità della coda hello è grande, applicazione può eseguire più operazioni contemporaneamente, in altre parole, più il multithreading. Se hello profondità della coda è ridotta, anche se l'applicazione è a thread multipli, non avrà sufficiente richieste allineate per l'esecuzione simultanea.

In genere, disattivare hello applicazioni scaffale non consentono la profondità della coda toochange hello, perché se impostare in modo non corretto tale più male che bene. Applicazioni imposterà hello destra valore prestazioni ottimali hello tooget profondità della coda. Tuttavia, è importante toounderstand questo concetto in modo che è possibile risolvere i problemi di prestazioni con l'applicazione. È anche possibile osservare gli effetti di hello la profondità della coda eseguendo benchmark tools nel sistema.

Alcune applicazioni forniscono impostazioni tooinfluence hello profondità della coda. Impostazione di MAXDOP (massimo grado di parallelismo) hello in SQL Server, ad esempio, descritto nella sezione precedente. MAXDOP è tooinfluence un modo profondità della coda e multithreading, anche se non modifica direttamente il valore di profondità della coda hello di SQL Server.

*Profondità elevata della coda*  
Righe di una profondità della coda ad alta le altre operazioni su disco hello. disco Hello SA successiva richiesta di hello nella propria coda di anticipo. Di conseguenza, disco hello possa pianificare le operazioni di anticipo e li elaborano in una sequenza ottimale. Poiché il disco di toohello più le richieste inviate dall'applicazione hello, disco hello in grado di elaborare ulteriori IOs parallelo. Infine, un'applicazione hello sarà in grado di tooachieve IOPS superiore. Poiché l'elaborazione di più richieste, hello velocità effettiva totale di un'applicazione hello aumenta.

In genere, un'applicazione può ottenere una velocità effettiva massima con 8-16+ I/O in attesa per ogni disco collegato. Se una profondità della coda, applicazione non viene eseguita sufficiente sistema toohello IOs e minore quantità di verrà elaborato in un periodo specifico. In altri termini, si otterrà una velocità effettiva minore.

Ad esempio, in SQL Server, hello impostazione MAXDOP valore per una query troppo indica a SQL Server che è possibile utilizzare query di hello toofour core tooexecute "4". SQL Server consente di verificare cosa è migliore coda profondità valore e hello il numero di core per l'esecuzione di query hello.

*Profondità ottimale della coda*  
Un valore molto elevato per la coda può avere alcuni svantaggi. Se il valore di profondità della coda è eccessivo, un'applicazione hello tenterà toodrive numero molto elevato di IOPS. A meno che un'applicazione non abbia dischi persistenti con un numero sufficiente di IOPS con provisioning, ciò può influire negativamente sulle latenze dell'applicazione. Formula seguente mostra una relazione di hello tra IOPS, latenza e la profondità della coda.  
    ![](media/storage-premium-storage-performance/image6.png)

Non è consigliabile configurare valore elevato tooany di profondità della coda, ma il valore ottimale tooan, in grado di offrire sufficiente di IOPS per un'applicazione hello senza influire sulla latenza. Ad esempio, se la latenza dell'applicazione hello deve toobe 1 millisecondo, hello profondità della coda obbligatorio tooachieve è 5.000 IOPS, PC = 5000 x 0,001 = 5.

*Profondità della coda per un volume con striping*  
Per un volume con striping è consigliabile mantenere una profondità della coda sufficientemente elevata da consentire a ogni disco di avere individualmente un picco di profondità della coda. Ad esempio, si consideri un'applicazione che inserisce una profondità della coda di 2 e sono presenti 4 dischi in striscia hello. due richieste dei / o Hello entra tootwo dischi, rimanenti due dischi sarà inattiva. Pertanto, configurare la profondità della coda hello tale che tutti i dischi di hello possono essere occupati. Formula seguente viene illustrato come toodetermine hello profondità della coda di volumi con striping.  
    ![](media/storage-premium-storage-performance/image7.png)

## <a name="throttling"></a>Limitazione
Provisioning di archiviazione Premium Azure numero specificato di IOPS e la velocità effettiva a seconda delle dimensioni delle macchine Virtuali hello e le dimensioni di disco desiderato. Ogni volta che l'applicazione tenta toodrive IOPS o una velocità effettiva di sopra di questi limiti di in grado di gestire quali hello macchina virtuale o un disco, verrà limitazione archiviazione Premium. Questa situazione si manifesta sotto forma di hello di riduzione delle prestazioni dell'applicazione. Ciò può comportare una latenza più alta, una velocità effettiva minore o valori di IOPS più bassi. Se l'Archiviazione Premium non applica la limitazione, è possibile che si verifichi un errore irreversibile dell'applicazione a causa del superamento dei limiti delle risorse. In tal caso, tooavoid problemi di prestazione in scadenza toothrottling, sempre il provisioning di risorse sufficienti per l'applicazione. Prendere in considerazione è descritto nelle sezioni di dimensioni disco precedente e di dimensioni delle macchine Virtuali di hello. Benchmark è toofigure modo migliore hello quali risorse è necessario toohost l'applicazione.

## <a name="benchmarking"></a>Benchmarking
Benchmark è il processo di hello di simulazione di carichi di lavoro diversi sull'applicazione e misurare le prestazioni dell'applicazione hello per ogni carico di lavoro. Utilizzare i passaggi di hello descritti in una sezione precedente, si sono stati raccolti i requisiti delle prestazioni dell'applicazione hello. Tramite l'esecuzione di prove comparative strumenti nelle macchine virtuali hello ospita un'applicazione hello, è possibile determinare i livelli di prestazioni hello che l'applicazione può ottenere con archiviazione Premium. In questa sezione sono disponibili esempi di benchmarking per una VM DS14 Standard con provisioning con dischi di Archiviazione Premium di Azure.

Sono stati usati gli strumenti di benchmarking comuni Iometer e FIO, rispettivamente per Windows e Linux. Questi strumenti generano la simulazione di produzione come carico di lavoro e le prestazioni del sistema hello misure di più thread. Utilizzando gli strumenti di hello è inoltre possibile configurare i parametri come blocco dimensioni e la coda di profondità, che è in genere non è possibile modificare per un'applicazione. In questo modo è più flessibilità toodrive hello le massime prestazioni su una scala elevata VM eseguito il provisioning con i dischi premium per diversi tipi di carichi di lavoro dell'applicazione. informazioni su ogni strumento di valutazione, visitare toolearn [Iometer](http://www.iometer.org/) e [FIO](http://freecode.com/projects/fio).

toofollow hello esempi riportati di seguito, creare una VM DS14 Standard e allegare toohello dischi di archiviazione Premium 11 macchina virtuale. Dei dischi hello 11, configurare i dischi di 10 con memorizzazione nella cache come "None" host e li eseguire lo striping in un volume denominato NoCacheWrites. Configurare la memorizzazione nella cache come "ReadOnly" su disco rimanente hello host e creare un volume denominato CacheReads con il disco. Tramite il programma di installazione, sarà in grado di toosee hello massimo lettura e scrittura delle prestazioni da una VM DS14 Standard. Per informazioni dettagliate sulla creazione di una macchina virtuale DS14 con i dischi premium, passare troppo[creare e utilizzare uno spazio di archiviazione Premium di conto per un disco di dati della macchina virtuale](../storage-premium-storage.md).

*Riscaldamento di Cache di hello*  
disco di Hello con memorizzazione nella cache di sola lettura host sarà in grado di toogive IOPS superiore rispetto al limite di hello. tooget massime prestazioni leggere dalla cache di hello host, è necessario innanzitutto riscaldamento della cache di hello del disco. In questo modo si garantisce che hello IOs lettura determinerà quale strumento benchmark sul volume CacheReads effettivamente riscontri cache di hello e non il disco hello direttamente. risultato di riscontri cache di Hello in IOPS aggiuntive dalla cache di hello singolo abilitata su disco.

> **Importante:**  
> È necessario riscaldamento della cache di hello prima di eseguire prove comparative, ogni volta che viene riavviato macchina virtuale.
>
>

#### <a name="iometer"></a>Iometer
[Scaricare lo strumento Iometer hello](http://sourceforge.net/projects/iometer/files/iometer-stable/2006-07-27/iometer-2006.07.27.win32.i386-setup.exe/download) su hello macchina virtuale.

*File di test*  
Iometer utilizza un file di test che verrà archiviato nel volume hello in cui eseguire test di benchmark hello. Unità di letture e scritture in questo test toomeasure disco hello del file di IOPS e la velocità effettiva. Iometer crea questo file di test se non ne è stato fornito uno. Creare un file di test di 200GB denominato iobw.tst volumi hello CacheReads e NoCacheWrites.

*Specifiche di accesso*  
Hello specifiche, dimensione della richiesta i/o, lettura/scrittura %, % casuali o sequenziali sono configurati utilizzando hello "Specifiche di accesso" scheda Iometer. Creare una specifica di accesso per ognuno di hello scenari descritti di seguito. Creare specifiche di accesso hello e "Salva" con un appropriato assegnare un nome simile: RandomWrites\_8 KB, RandomReads\_8 KB. Selezionare specifica corrispondente hello durante l'esecuzione di uno scenario di test hello.

Un esempio di specifiche di accesso per uno scenario con valori massimi di IOPS di scrittura è riportato di seguito,   
    ![](media/storage-premium-storage-performance/image8.png)

*Specifiche per il valore massimo di IOPS di test*  
toodemonstrate massimo IOPs, utilizzare dimensioni richiesta. Usare una dimensione di richiesta pari a 8 K e creare specifiche per letture e scritture casuali.

| Specifica di accesso | Dimensione della richiesta | % di casuali | % di letture |
| --- | --- | --- | --- |
| RandomWrites\_8K |8 K |100 |0 |
| RandomReads\_8K |8 K |100 |100 |

*Specifiche per il valore massimo di velocità effettiva di test*  
toodemonstrate velocità effettiva massima, utilizzano le maggiori dimensioni della richiesta. Usare una dimensione di richiesta pari a 64 K e creare specifiche per letture e scritture casuali.

| Specifica di accesso | Dimensione della richiesta | % di casuali | % di letture |
| --- | --- | --- | --- |
| RandomWrites\_64K |64 K |100 |0 |
| RandomReads\_64K |64 K |100 |100 |

*Esecuzione di Iometer Test hello*  
Eseguire procedure hello toowarm cache

1. Creare le specifiche di accesso con i valori seguenti.

   | Nome | Dimensione della richiesta | % di casuali | % di letture |
   | --- | --- | --- | --- |
   | RandomWrites\_1MB |1 MB |100 |0 |
   | RandomReads\_1MB |1 MB |100 |100 |
2. Eseguire test Iometer hello per inizializzare il disco della cache con i parametri seguenti. Utilizzare tre thread di lavoro per il volume di destinazione di hello e una profondità della coda di 128. Impostare hello "Runtime" la durata di hello test too2hrs nella scheda "Configurazione di Test" hello.

   | Scenario | Volume di destinazione | Nome | Durata |
   | --- | --- | --- | --- |
   | Inizializzare il disco della cache |CacheReads |RandomWrites\_1MB |2 ore |
3. Eseguire test Iometer hello per il riscaldamento disco cache con i parametri seguenti. Utilizzare tre thread di lavoro per il volume di destinazione di hello e una profondità della coda di 128. Impostare hello "Runtime" la durata di hello test too2hrs nella scheda "Configurazione di Test" hello.

   | Scenario | Volume di destinazione | Nome | Durata |
   | --- | --- | --- | --- |
   | Preparare il disco della cache |CacheReads |RandomReads\_1MB |2 ore |

Dopo che il disco della cache è stato riscaldato, procedere con scenari di test hello elencati di seguito. hello toorun Iometer test, utilizzare almeno tre thread di lavoro per **ogni** volume di destinazione. Per ogni thread di lavoro, selezionare il volume di destinazione hello, impostare la profondità della coda e selezionare una delle specifiche di test salvata hello, come illustrato nella tabella hello sotto, toorun hello corrispondente uno scenario di test. Quando si eseguono questi test, tabella di Hello illustra anche i risultati previsti per IOPS e la velocità effettiva. Per tutti gli scenari vengono usati una dimensione di I/O ridotta pari a 8 KB e un valore elevato per la profondità della coda, pari a 128.

| Scenario di test | Volume di destinazione | Nome | Risultato |
| --- | --- | --- | --- |
| Max. IOPS di lettura |CacheReads |RandomWrites\_8K |50.000 IOPS  |
| Max. IOPS di scrittura |NoCacheWrites |RandomReads\_8K |64.000 IOPS |
| Max. IOPS combinate |CacheReads |RandomWrites\_8K |100.000 IOPS |
| NoCacheWrites |RandomReads\_8K | &nbsp; | &nbsp; |
| Max. letture MB/sec |CacheReads |RandomWrites\_64K |524 MB/sec |
| Max. scritture MB/sec |NoCacheWrites |RandomReads\_64K |524 MB/sec |
| MB/sec combinati |CacheReads |RandomWrites\_64K |1000 MB/sec |
| NoCacheWrites |RandomReads\_64K | &nbsp; | &nbsp; |

Di seguito sono schermate di hello Iometer risultati dei test per scenari IOPS e la velocità effettiva combinati.

*Valori massimi per IOPS di letture e scritture combinate*  
![](media/storage-premium-storage-performance/image9.png)

*Velocità effettiva massima di letture e scritture combinate*  
![](media/storage-premium-storage-performance/image10.png)

### <a name="fio"></a>FIO
FIO è un archivio di toobenchmark strumento comune in hello macchine virtuali Linux. Dispone di hello flessibilità tooselect diversi i/o le dimensioni, sequenziale o casuale letture e scritture. Genera il thread di lavoro o hello tooperform processi specificati operazioni i/o. È possibile specificare il tipo di hello di operazioni dei / o che necessario eseguire ogni thread di lavoro utilizzando i file del processo. È stato creato un file di processo per ogni scenario illustrato negli esempi di hello riportato di seguito. È possibile modificare specifiche hello in questi processi file toobenchmark diversi carichi di lavoro in esecuzione in archiviazione Premium. Negli esempi di hello, si sta usando un in esecuzione Standard per VM 14 DS **Ubuntu**. Hello utilizzare stesso programma di installazione descritti in inizio hello di hello [benchmark sezione](#Benchmarking) e riscaldamento della cache di hello prima di eseguire i test di benchmark hello.

Prima di iniziare, [scaricare FIO](https://github.com/axboe/fio) e installarlo nella macchina virtuale.

Eseguire hello comando seguente per Ubuntu,

```
apt-get install fio
```

Si utilizzerà per le operazioni di lettura determinante su dischi hello quattro thread di lavoro per la Guida di operazioni di scrittura e quattro thread di lavoro. Hello scrittura lavoratori verranno essere piedi traffico nel volume nocache"hello", che include 10 dischi con cache troppo imposta "None". Hello thread di lavoro di lettura verrà essere che indirizza il traffico nel volume readcache"hello", con il 1 disco con il set di cache troppo "ReadOnly".

*IOPS massime di scrittura*  
Creare il file di processo hello con tooget specifiche seguenti numero massimo di IOPS di scrittura. Assegnare al file il nome "fiowrite.ini".

```
[global]
size=30g
direct=1
iodepth=256
ioengine=libaio
bs=8k

[writer1]
rw=randwrite
directory=/mnt/nocache
[writer2]
rw=randwrite
directory=/mnt/nocache
[writer3]
rw=randwrite
directory=/mnt/nocache
[writer4]
rw=randwrite
directory=/mnt/nocache
```

Hello nota seguire elementi principali che sono in base alle linee guida di progettazione hello illustrate nelle sezioni precedenti. Queste specifiche sono essenziali toodrive numero massimo di IOPS  

* Profondità della coda elevata pari a 256.  
* Dimensione di blocco ridotta pari a 8 KB.  
* Più thread che eseguono scritture casuali.

Eseguire hello successivo comando tookick off hello FIO verificare la presenza di 30 secondi,  

```
sudo fio --runtime 30 fiowrite.ini
```

Durante l'esecuzione di test hello, sarà il numero hello toosee in grado di distribuire i dischi di macchina virtuale e Premium hello IOPS di scrittura. Come illustrato nell'esempio hello riportato di seguito, hello VM DS14 recapita il limite di IOPS di 50.000 IOPS massima di scrittura.  
    ![](media/storage-premium-storage-performance/image11.png)

*IOPS massime di lettura*  
Creare il file di processo hello con tooget specifiche seguenti numero massimo di IOPS di lettura. Assegnare al file il nome "fioread.ini".

```
[global]
size=30g
direct=1
iodepth=256
ioengine=libaio
bs=8k

[reader1]
rw=randread
directory=/mnt/readcache
[reader2]
rw=randread
directory=/mnt/readcache
[reader3]
rw=randread
directory=/mnt/readcache
[reader4]
rw=randread
directory=/mnt/readcache
```

Hello nota seguire elementi principali che sono in base alle linee guida di progettazione hello illustrate nelle sezioni precedenti. Queste specifiche sono essenziali toodrive numero massimo di IOPS

* Profondità della coda elevata pari a 256.  
* Dimensione di blocco ridotta pari a 8 KB.  
* Più thread che eseguono scritture casuali.

Eseguire hello successivo comando tookick off hello FIO verificare la presenza di 30 secondi,

```
sudo fio --runtime 30 fioread.ini
```

Durante l'esecuzione di test hello, sarà il numero hello toosee in grado di hello IOPS lettura VM e forniscono i dischi Premium. Come illustrato nell'esempio hello riportato di seguito, hello VM DS14 offre più di 64.000 IOPS di lettura. Si tratta di una combinazione di disco hello e le prestazioni della cache di hello.  
    ![](media/storage-premium-storage-performance/image12.png)

*IOPS massime di lettura e scrittura*  
Creare file di processo hello con tooget di specifiche seguenti massimo combinati in lettura e scrittura di IOPS. Assegnare al file il nome "fioreadwrite.ini".

```
[global]
size=30g
direct=1
iodepth=128
ioengine=libaio
bs=4k

[reader1]
rw=randread
directory=/mnt/readcache
[reader2]
rw=randread
directory=/mnt/readcache
[reader3]
rw=randread
directory=/mnt/readcache
[reader4]
rw=randread
directory=/mnt/readcache

[writer1]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer2]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer3]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer4]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
```

Hello nota seguire elementi principali che sono in base alle linee guida di progettazione hello illustrate nelle sezioni precedenti. Queste specifiche sono essenziali toodrive numero massimo di IOPS

* Profondità della coda elevata pari a 128.  
* Dimensione di blocco ridotta pari a 4 KB.  
* Più thread che eseguono scritture e letture casuali.

Eseguire hello successivo comando tookick off hello FIO verificare la presenza di 30 secondi,

```
sudo fio --runtime 30 fioreadwrite.ini
```

Durante l'esecuzione di test hello, si verrà numero hello toosee in grado di lettura combinato e IOPS di scrittura VM hello e forniscono i dischi Premium. Come illustrato nell'esempio hello riportato di seguito, hello VM DS14 offre più di 100.000 lettura combinato e IOPS di scrittura. Si tratta di una combinazione di disco hello e le prestazioni della cache di hello.  
    ![](media/storage-premium-storage-performance/image13.png)

*Velocità effettiva massima combinata*  
hello tooget massimo combinato di lettura e la velocità effettiva di scrittura, utilizzare una dimensione del blocco più grande e la profondità della coda di grandi dimensioni con più thread di esecuzione di letture e scritture. È possibile usare una dimensione di blocco pari a 64 KB e una profondità della coda pari a 128.

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni sull'Archiviazione Premium di Azure:

* [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../storage-premium-storage.md)  

Per gli utenti di SQL Server sono disponibili articoli sulle procedure consigliate per le prestazioni per SQL Server:

* [Procedure consigliate per le prestazioni per SQL Server in Macchine virtuali di Azure](../../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md)
* [L'Archiviazione Premium di Azure offre le prestazioni più elevate per SQL Server in VM di Azure](http://blogs.technet.com/b/dataplatforminsider/archive/2015/04/23/azure-premium-storage-provides-highest-performance-for-sql-server-in-azure-vm.aspx)
