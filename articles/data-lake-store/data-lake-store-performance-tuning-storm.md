---
title: linee guida sull'ottimizzazione delle prestazioni tempesta di archivio Data Lake di aaaAzure | Documenti Microsoft
description: Linee guida per l'ottimizzazione delle prestazioni di Storm in Azure Data Lake Store
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: 5412fd46cf2373f5877030913df4fe1fc6f5473a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-storm-on-hdinsight-and-azure-data-lake-store"></a>Linee guida per l'ottimizzazione delle prestazioni di Storm in HDInsight e di Azure Data Lake Store

Comprendere i fattori da considerare quando si Ottimizza prestazioni hello di una topologia di Storm Azure hello. Ad esempio, è importante toounderstand caratteristiche di hello del lavoro hello scopo spouts hello e le viti hello (lavoro hello sia con utilizzo intensivo della memoria o dei / o). Questo articolo illustra una serie di linee guida per l'ottimizzazione delle prestazioni, inclusa la risoluzione dei problemi comuni.

## <a name="prerequisites"></a>Prerequisiti

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Un account Azure Data Lake Store**. Per istruzioni su come toocreate uno, vedere [introduzione archivio Azure Data Lake](data-lake-store-get-started-portal.md).
* **Un cluster Azure HDInsight** con accesso tooa account archivio Data Lake. Vedere [Creare un cluster HDInsight con Data Lake Store tramite il portale di Azure](data-lake-store-hdinsight-hadoop-use-portal.md). Assicurarsi di abilitare Desktop remoto per il cluster hello.
* **Esecuzione di un cluster Storm in Data Lake Store**. Per altre informazioni, vedere [Storm in HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-overview).
* **Linee guida per l'ottimizzazione delle prestazioni in Data Lake Store**.  Per i concetti generali relativi alle prestazioni, vedere [Linee guida per l'ottimizzazione delle prestazioni in Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance).  

## <a name="tune-hello-parallelism-of-hello-topology"></a>Ottimizzare il parallelismo hello della topologia hello

Potrebbe essere in grado di tooimprove prestazioni dalla concorrenza hello crescente di hello tooand dei / o dall'archivio Data Lake. Una topologia di Storm include un set di configurazioni che determinano il parallelismo hello:
* Numero di processi di lavoro (lavoratori hello sono distribuiti uniformemente tra le macchine virtuali hello).
* Numero di istanze di executor di spout.
* Numero di istanze di executor di bolt.
* Numero di attività spout.
* Numero di attività bolt.

Ad esempio, in un cluster con 4 macchine virtuali e i processi di lavoro 4, executor beccuccio 32 e 32 beccuccio attività e 256 executor fulmine e attività fulmine 512, considerare i seguenti hello:

Ogni supervisore, che è un ruolo di lavoro, ha un singolo processo di lavoro JVM (Java Virtual Machine). Questo processo JVM gestisce 4 thread di spout e 64 thread di bolt. In ogni thread le attività vengono eseguite in sequenza. Con hello configurazione precedente, ogni thread beccuccio dispone di 1 attività e ogni thread fulmine dispone di 2 attività.

In soprannumero, ecco hello vari componenti coinvolti, e gli effetti di livello hello di parallelismo che è:
* nodo head Hello (chiamato Nimbus in Storm) viene utilizzato toosubmit e gestire i processi. Questi nodi avere alcun impatto sul livello hello di parallelismo.
* nodi Supervisore Hello. Corrisponde in HDInsight, il nodo di lavoro tooa macchina virtuale di Azure.
* attività di lavoro Hello sono processi Storm in esecuzione in macchine virtuali hello. Ogni attività di lavoro corrispondente istanza JVM tooa. Storm distribuisce numero hello di processi di lavoro è specificare i nodi di lavoro toohello più uniforme possibile.
* Istanze di executor di spout e bolt. Ogni istanza di executor corrisponde tooa thread in esecuzione all'interno di processi di lavoro hello (JVMs).
* Attività di Storm. Si tratta di attività logiche eseguite da ognuno di questi thread. Ciò non modifica il livello di hello di parallelismo, pertanto è necessario valutare se è necessario disporre di più attività per l'esecutore o non.

### <a name="get-hello-best-performance-from-data-lake-store"></a>Ottenere prestazioni ottimali hello dall'archivio Data Lake

Quando si utilizza l'archivio Data Lake, ottenere migliori prestazioni di hello se hello seguenti:
* Unire le piccole aggiunte in dimensioni maggiori (idealmente 4 MB).
* Eseguire il maggior numero possibile di richieste simultanee. Poiché ogni thread fulmine esegue letture blocco, è auspicabile toohave in un punto qualsiasi nell'intervallo di hello di 8-12 thread per core. In questo modo hello NIC e hello CPU utilizzata correttamente. Una macchina virtuale più grande consente di eseguire un maggior numero di richieste simultanee.  

### <a name="example-topology"></a>Topologia di esempio

Si supponga di avere un cluster con 8 nodi di lavoro e una macchina virtuale di Azure D13v2. Questa macchina virtuale con 8 core, pertanto tra hello 8 nodi di lavoro, è necessario 64 core totale.

Si supponga di eseguire 8 thread bolt per core. Essendo i core 64, si vuole un totale di 512 istanze dell'executor (ovvero di thread) di bolt. In questo caso, ad esempio, è iniziare con una JVM per ogni macchina virtuale, utilizzare principalmente concorrenza di thread hello all'interno di concorrenza di tooachieve JVM hello. Ciò significa che sono necessari 8 attività di lavoro (uno per ogni macchina virtuale di Azure) e 512 executor bolt. Questa configurazione di Storm tenta toodistribute hello thread di lavoro in modo uniforme tra i nodi di lavoro (noto anche come nodi di supervisore), assegnando a ciascun nodo di lavoro 1 JVM. Ora in supervisori hello, Storm tenta executor hello toodistribute in modo uniforme tra i supervisori, assegnando ogni Supervisore (vale a dire JVM) 8 thread ognuno.

## <a name="tune-additional-parameters"></a>Ottimizzare i parametri aggiuntivi
Dopo aver creato una topologia di base hello, è possibile considerare se si desidera tootweak uno dei parametri di hello:
* **Number of JVMs per worker node** (Numero di JVM per nodo di lavoro). Se si ha una struttura dei dati di grandi dimensioni (ad esempio, tabella di ricerca) che si vuole ospitare in memoria, ogni JVM richiede una copia separata. In alternativa, è possibile utilizzare la struttura di data hello tra molti thread se si dispone di meno JVMs. Per i/o del fulmine hello, numero hello di JVMs non consente più di una differenza come numero hello di thread aggiunti tra tali JVMs. Per semplicità, è una buona idea toohave uno JVM per lavoro. A seconda delle operazioni del fulmine o applicazione di elaborazione è richiedono, tuttavia, potrebbe essere necessario toochange questo numero.
* **Number of spout executors** (Numero di executor spout). Poiché hello esempio precedente Usa bulloni per la scrittura di archivio Lake tooData, numero hello di spouts non è prestazioni fulmine toohello direttamente pertinenti. Tuttavia, a seconda della quantità di hello di elaborazione o i/o in corso nel beccuccio hello, è buona norma hello tootune spouts per prestazioni ottimali. Assicurarsi di disporre di sufficiente occupato bulloni spouts toobe tookeep in grado di hello. frequenze di output di Hello di hello spouts devono corrispondere a velocità effettiva di hello di bulloni hello. la configurazione effettiva Hello dipende da beccuccio hello.
* **Number of tasks** (Numero di attività). Ogni bolt viene eseguito come thread singolo. Attività aggiuntive sui bolt non forniscono concorrenza aggiuntiva. Hello solo tempo benefit è se il processo di riconoscimento hello tupla accetta gran parte del tempo di esecuzione fulmine. È un toogroup buona numero eccessivo di tuple in un maggiore aggiunta prima di inviare un acknowledgement da fulmine hello. Nella maggior parte dei casi quindi più attività non offrono vantaggi aggiuntivi.
* **Local or shuffle grouping** (Raggruppamento locale o casuale). Quando questa impostazione è abilitata, le tuple vengono inviate toobolts all'interno di hello stesso processo di lavoro. In questo modo si riduce il numero di comunicazioni tra processi e chiamate di rete. Tale operazione è consigliata per la maggior parte delle topologie.

Questo scenario di base è un buon punto di partenza. Eseguire test con la propria hello tootweak dati prima di ottenere prestazioni ottimali tooachieve parametri.

## <a name="tune-hello-spout"></a>Ottimizzare beccuccio hello

È possibile modificare hello impostazioni tootune hello beccuccio seguente.

- **Tuple timeout: topology.message.timeout.secs** (Timeout tuple: topology.message.timeout.secs). Questa impostazione determina hello quantità di tempo un messaggio toocomplete e ricevere acknowledgement, prima di essere considerato non riuscito.

- **Max memory per worker process: worker.childopts** (Memoria massima per processo di lavoro: worker.childopts). Questa impostazione consente di specificare ulteriori parametri della riga di comando toohello Java lavoratori. impostazione più diffuse Hello è XmX, che determina l'heap hello memoria massima allocata tooa JVM.

- **Max spout pending: topology.max.spout.pending** (Spout massimo in sospeso: topology.max.spout.pending). Questa impostazione determina il numero di hello di tuple che è possibile in fase di trasferimento (non riconosciuti in tutti i nodi nella topologia hello) per ogni thread beccuccio in qualsiasi momento.

 Toodo un buon calcolo è dimensioni hello tooestimate di ogni le tuple. Quindi capire di quanta memoria dispone un thread spout. Hello memoria totale allocata thread tooa, diviso per questo valore, viene fornito il limite superiore di hello per beccuccio max di hello in sospeso di parametro.

## <a name="tune-hello-bolt"></a>Ottimizzare fulmine hello
Quando si scrive archivio Lake tooData, impostare un criterio di sincronizzazione (buffer sul lato client hello) di dimensioni too4 MB. Lo scaricamento di hsync() viene quindi eseguita solo quando sono di dimensioni del buffer hello hello questo valore. driver di archivio Data Lake Hello in lavoro hello VM effettua automaticamente l'utilizzo del buffer, a meno che non si esegue in modo esplicito un hsync().

fulmine tempesta di archivio Data Lake di Hello predefinito ha un parametro di criteri di sincronizzazione di dimensioni (fileBufferSize) che può essere utilizzati tootune questo parametro.

Nelle topologie dei / O-con utilizzo intensivo è toohave una buona idea ogni thread di fulmine scrivere file proprio tooits e tooset un criterio di rotazione di file (fileRotationSize). Quando il file hello raggiunge una determinata dimensione, flusso hello viene scaricata automaticamente e viene scritto un nuovo file. dimensioni file per la rotazione consigliata Hello è 1 GB.

### <a name="handle-tuple-data"></a>Gestire i dati delle tuple

In soprannumero, beccuccio viene mantenuto nella tupla tooa fino a quando non è riconosciuto in modo esplicito da fulmine hello. Se è stato letto dal fulmine hello una tupla, ma non è ancora stata riconosciuta, beccuccio hello potrebbe non sono persistenti nel back-end di archivio Data Lake. Dopo una tupla viene riconosciuta, può essere garantita la persistenza dal fulmine hello beccuccio hello e quindi è stato possibile eliminare i dati di origine hello da qualsiasi origine che sta leggendo da.  

Per prestazioni ottimali in archivio Data Lake, avere fulmine hello buffer a 4 MB di dati di tupla. Quindi scrivere toohello nuovo archivio Data Lake terminare come un'operazione di scrittura 4 MB. Dopo che i dati hello sono stata scritta correttamente toohello archivio (dal chiamante hflush()), fulmine hello può riguardare hello dati back-toohello beccuccio. Si tratta di quali esempio hello bullone non qui. È inoltre accettabile toohold un maggior numero di tuple prima che venga effettuata chiamata hflush() hello e hello tuple riconosciute. Tuttavia, ciò aumenta il numero di hello di tuple in fase di trasferimento che necessita di beccuccio hello toohold e pertanto aumenta hello quantità di memoria richiesta per JVM.

> [!NOTE]
Applicazioni potrebbe essere presente una tuple tooacknowledge requisito più di frequente (in dimensioni di dati inferiori a 4 MB) per altri motivi di prestazioni non. Tuttavia, che potrebbe influenzare hello i/o della velocità effettiva toohello archiviazione back-end. Valutare con attenzione questo compromesso rispetto alle prestazioni dei / o del fulmine hello.

Se frequenza in ingresso di hello di tuple è non è elevato, pertanto il buffer di 4 MB hello accetta un toofill molto tempo, considerare il problema, riduzione del rischio:
* Ridurre il numero di hello di bulloni, pertanto esistono toofill un minor numero di buffer.
* Con un criterio basato sul tempo o basate sul conteggio, in cui un hflush() viene attivato ogni x scaricamenti o ogni millisecondi y e tuple hello accumulate finora sono riconosciute back.

Si noti che in questo caso la velocità effettiva hello è inferiore, ma con una frequenza lenta degli eventi, velocità effettiva massima non obiettivo principale di hello comunque. Queste soluzioni consentono di ridurre il tempo totale di hello impiegata per un tooflow tupla tramite toohello store. Questo potrebbe essere importante se è necessaria una pipeline in tempo reale anche con una frequenza di eventi bassa. Si noti inoltre che, se la frequenza in ingresso di tupla è bassa, è necessario regolare parametro topology.message.timeout_secs hello, in modo hello Tuple non è previsto un timeout mentre ricevono memorizzato nel buffer o elaborato.

## <a name="monitor-your-topology-in-storm"></a>Monitorare la topologia in Storm  
Durante l'esecuzione di una topologia, è possibile monitorare e nell'interfaccia utente di Storm hello. Di seguito sono toolook parametri principali hello in:

* **Total process execution latency** (Latenza totale di esecuzione del processo). Questo è il tempo medio di hello una tupla accetta toobe emessa beccuccio hello, elaborati da fulmine hello e riconosciuto.

* **Total bolt process latency** (Latenza totale del processo dei bolt). Si tratta di hello permanenza Media tupla hello in fulmine hello finché non viene ricevuto un acknowledgement.

* **Total bolt execute latency** (Latenza totale di esecuzione dei bolt). Si tratta di hello Media tempo fulmine hello in hello utilizzato dal metodo execute.

* **Number of failures** (Numero di errori). Si riferisce toohello numero di tuple che non è stato possibile toobe elaborato completamente prima che di timeout.

* **Capacity** (Capacità). Misura del carico di lavoro del sistema. Se questo numero è 1, i bolt stanno lavorando al massimo della velocità. Se è minore di 1, aumentare il parallelismo hello. Se è maggiore di 1, ridurre il parallelismo hello.

## <a name="troubleshoot-common-problems"></a>Risolvere i problemi comuni
Ecco alcuni scenari comuni per la risoluzione dei problemi.
* **È in corso il timeout di diverse tuple.** Esaminare ogni nodo hello topologia toodetermine dove collo di bottiglia hello è. Hello più comuni questo accade che bulloni hello non sono in grado di tookeep backup con spouts hello. In tal modo tootuples sommersa da buffer interni di hello durante l'attesa toobe elaborati. È consigliabile aumentare il valore di timeout hello o riducendo beccuccio max di hello in sospeso.

* **La latenza di esecuzione dei processi totale è elevata, ma la latenza dei processi bolt è bassa.** In questo caso, è possibile che le tuple hello non sono riconosciute sufficientemente veloce. Verificare che sia presente un numero sufficiente di elementi di acknowledgment. Un'altra possibilità consiste nel fatto che sono in attesa nella coda di hello per troppo tempo prima di avviare l'elaborazione di bulloni hello. Ridurre beccuccio max di hello in sospeso.

* **La latenza di esecuzione dei bolt è elevata.** Ciò significa che il metodo Execute () hello del fulmine sta richiedendo troppo tempo. Ottimizza codice hello, o esaminare le dimensioni di scrittura e il comportamento di scaricamento.

### <a name="data-lake-store-throttling"></a>Limitazione di Data Lake Store
Se si raggiunge i limiti di hello di larghezza di banda fornita dall'archivio Data Lake, potrebbero verificarsi errori di attività. Cercare errori di limitazione nei log delle attività. È possibile ridurre il parallelismo hello mediante l'aumento delle dimensioni del contenitore.    

toocheck se sono recupero limitate, abilitare il debug di hello registrazione sul lato client hello:

1. In **Ambari** > **Storm** > **Config** > **avanzate storm-worker-log4j**, modifica  **&lt;radice livello = "info"&gt;**  troppo**&lt;radice livello = "debug"&gt;**. Riavviare tutti i nodi di hello/servizio per effetto di tootake configurazione hello.
2. Monitoraggio hello Storm topologia accede nodi di lavoro (in /var/log/storm/worker-artifacts /&lt;TopologyName&gt;/&lt;porta&gt;/worker.log) per la limitazione delle richieste di eccezioni da archivio Data Lake.

## <a name="next-steps"></a>Passaggi successivi
L'ottimizzazione aggiuntiva delle prestazioni di Storm è reperibile in questo [blog](https://blogs.msdn.microsoft.com/shanyu/2015/05/14/performance-tuning-for-hdinsight-storm-and-microsoft-azure-eventhubs/).

Per un toorun esempi aggiuntivi, vedere [questo su GitHub](https://github.com/hdinsight/storm-performance-automation).
