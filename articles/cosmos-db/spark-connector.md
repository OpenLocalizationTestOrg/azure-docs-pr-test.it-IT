---
title: aaaConnecting Apache Spark tooAzure DB Cosmos | Documenti Microsoft
description: "Utilizzare questo toolearn esercitazione sul connettore di Azure Cosmos DB Spark hello che permette di tooconnect Apache Spark tooAzure DB Cosmos tooperform distribuita aggregazioni e scienze dati nel sistema di database distribuiti in modo globale multi-tenant hello da Microsoft che è progettato per il cloud hello."
keywords: Apache Spark
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: c4f46007-2606-4273-ab16-29d0e15c0736
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: denlee
ms.openlocfilehash: 70b496fc5ca8f65675f0224e749637f5d533c346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="accelerate-real-time-big-data-analytics-with-hello-spark-tooazure-cosmos-db-connector"></a>Consente di accelerare analitica big dati in tempo reale con connettore di hello Spark tooAzure Cosmos DB

connettore di Hello Spark tooAzure DB Cosmos consente tooact DB Cosmos Azure come origine di input o un sink di output per i processi di Apache Spark. Connessione [Spark](http://spark.apache.org/) troppo[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) accelera il possibilità toosolve rapido analisi scientifica dei dati in cui è possibile utilizzare Azure Cosmos DB tooquickly problemi persistono e query sui dati. connettore di Hello Spark tooAzure DB Cosmos utilizza in modo efficiente hello nativo gestito di Azure Cosmos DB indici. Quando si esegue analitica e push-down predicato filtro rapido cambiamento globale distribuiti di dati, compresi tra gli scenari di scientifici e analitica toodata Internet delle cose (IoT), gli indici di Hello consentono colonne aggiornabili.

Per l'utilizzo di GraphX Spark e di grafico Gremlin hello API di Azure Cosmos DB, vedere [eseguire analitica grafico utilizzando Spark e Apache TinkerPop Gremlin](spark-connector-graph.md).

## <a name="download"></a>Scaricare

avvio tooget, scaricare hello Spark tooAzure Cosmos DB connector (anteprima) da hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) repository in GitHub.

## <a name="connector-components"></a>Componenti del connettore

connettore Hello Usa hello seguenti componenti:

* [Azure DB Cosmos](http://documentdb.com) consente ai clienti tooprovision e scala elastico velocità effettiva e archiviazione per un numero qualsiasi di aree geografiche. offerte di servizio Hello:
   * [Distribuzione globale](distribute-data-globally.md) e scalabilità orizzontale chiavi in mano
   * Le latenze di cifra al dato percentile 99th hello è garantito
   * [Più modelli di coerenza ben definiti](consistency-levels.md)
   * Disponibilità elevata garantita con funzionalità multihosting
   * Tutte le funzionalità sono supportate da [contratti di servizio](https://azure.microsoft.com/support/legal/sla/cosmos-db) completi leader del settore.

* [Apache Spark](http://spark.apache.org/) è un potente motore di elaborazione open source incentrato su velocità, semplicità d'uso e analisi avanzata.

* [Apache Spark in HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) in modo che è possibile distribuire Apache Spark in cloud hello per le distribuzioni di importanza critica utilizzando [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).

Versioni supportate ufficialmente:

| Componente | Versione |
|---------|-------|
|Apache Spark|2.0+|
| Scala| 2.11|
| Azure DocumentDB Java SDK | 1.10.0 |

In questo articolo consente di eseguire alcuni semplici esempi con Python (tramite pyDocumentDB) e hello interfacce di Scala.

Esistono due approcci tooconnect Apache Spark e Azure Cosmos DB:
- Utilizzare pyDocumentDB tramite hello [Azure SDK per Python DocumentDB](https://github.com/Azure/azure-documentdb-python).
- Creare un connettore di DB Cosmos tooAzure di Spark basati su Java utilizzando hello [Azure SDK per Java DocumentDB](https://github.com/Azure/azure-documentdb-java).

## <a name="pydocumentdb-implementation"></a>Implementazione di pyDocumentDB
Hello corrente [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) consente tooconnect Spark tooAzure DB Cosmos come illustrato nel seguente diagramma hello:

![Spark tooAzure flusso di dati DB Cosmos tramite pyDocumentDB DB](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-hello-pydocumentdb-implementation"></a>Flusso di dati di implementazione pyDocumentDB hello

flusso di dati Hello è come segue:

1. nodo principale di Hello Spark connette nodo gateway di Azure Cosmos DB toohello tramite pyDocumentDB. Un utente specifica solo hello Spark e Azure Cosmos DB connessioni. Connessioni toohello rispettivi master e gateway sono nodi utente toohello trasparente.
2. nodo gateway Hello rende query hello Azure Cosmos DB in cui query hello viene eseguita successivamente le partizioni dell'insieme di hello in nodi dati hello. risposta Hello per le query viene inviato nuovamente il nodo di gateway toohello e tale set di risultati viene restituito toohello nodo principale di Spark.
3. Le query successive (ad esempio, su un frame di dati di Spark) vengono inviate i nodi di lavoro Spark toohello per l'elaborazione.

La comunicazione tra Spark e Azure Cosmos DB è limitato toohello nodo principale di Spark e nodi di Azure Cosmos DB gateway.  le query Hello passare la stessa velocità consente a livello di trasporto hello tra questi due nodi.

### <a name="install-pydocumentdb"></a>Installare pyDocumentDB
È possibile installare pyDocumentDB sul nodo del driver usando **pip**, ad esempio:

```
pip install pyDocumentDB
```


### <a name="connect-spark-tooazure-cosmos-db-via-pydocumentdb"></a>Connettersi Spark tooAzure DB Cosmos tramite pyDocumentDB
semplicità di Hello del trasporto di comunicazione hello rende l'esecuzione di una query da Spark tooAzure DB Cosmos utilizzando pyDocumentDB relativamente semplice.

Hello seguente frammento di codice viene illustrato come pyDocumentDB toouse in un contesto di Spark.

```
# Import Necessary Libraries
import pydocumentdb
from pydocumentdb import document_client
from pydocumentdb import documents
import datetime

# Configuring hello connection policy (allowing for endpoint discovery)
connectionPolicy = documents.ConnectionPolicy()
connectionPolicy.EnableEndpointDiscovery
connectionPolicy.PreferredLocations = ["Central US", "East US 2", "Southeast Asia", "Western Europe","Canada Central"]


# Set keys tooconnect tooAzure Cosmos DB
masterKey = 'le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA=='
host = 'https://doctorwho.documents.azure.com:443/'
client = document_client.DocumentClient(host, {'masterKey': masterKey}, connectionPolicy)
```

Come indicato nel frammento di codice hello:

* Hello Azure Cosmos DB Python SDK (`pyDocumentDB`) contiene hello tutti hello parametri di connessione necessarie. Ad esempio, hello preferito parametro percorsi sceglie hello lettura dell'ordine di priorità e di replica.
*  Importare le librerie necessarie hello e configurare il **masterKey** e **host** toocreate hello Azure Cosmos DB *client* (**pydocumentdb.document_ client**).


### <a name="execute-spark-queries-via-pydocumentdb"></a>Eseguire query Spark tramite pyDocumentDB
Hello seguenti esempi usare hello Azure Cosmos DB l'istanza che è stato creato nel frammento precedente hello utilizzando hello specifica le chiavi di sola lettura. frammento di codice seguente Hello connette toohello **airports.codes** insieme nell'account DoctorWho hello come specificato in precedenza e viene eseguito un aeroporto di hello tooextract query città nello stato di Washington.

```
# Configure Database and Collections
databaseId = 'airports'
collectionId = 'codes'

# Configurations hello Azure Cosmos DB client will use tooconnect toohello database and collection
dbLink = 'dbs/' + databaseId
collLink = dbLink + '/colls/' + collectionId

# Set query parameter
querystr = "SELECT c.City FROM c WHERE c.State='WA'"

# Query documents
query = client.QueryDocuments(collLink, querystr, options=None, partition_key=None)

# Query for partitioned collections
# query = client.QueryDocuments(collLink, query, options= { 'enableCrossPartitionQuery': True }, partition_key=None)

# Push into list `elements`
elements = list(query)
```

Dopo l'esecuzione di query hello tramite **query**, hello risultato è un **query_iterable. QueryIterable** ovvero convertito tooa Python elenco. Un elenco di Python può essere convertito facilmente tooa frame di dati di Spark usando hello seguente codice:

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-hello-pydocumentdb-tooconnect-spark-tooazure-cosmos-db"></a>Perché utilizzare hello pyDocumentDB tooconnect Spark tooAzure Cosmos DB?
Connessione tooAzure Spark DB Cosmos utilizzando pyDocumentDB è in genere per gli scenari in cui:

* Si desidera toouse Python.
* Viene restituito un relativamente piccolo set di risultati da Azure Cosmos DB tooSpark. Si noti che un set di dati sottostante nel database di Azure Cosmos hello possono essere notevoli. Si stanno applicando filtri, ovvero eseguendo filtri in base a predicati, sull'origine Azure Cosmos DB.  

## <a name="spark-tooazure-cosmos-db-connector"></a>Spark tooAzure Cosmos DB connector

connettore di Hello Spark tooAzure DB Cosmos utilizza hello [Azure SDK per Java DocumentDB](https://github.com/Azure/azure-documentdb-java) e sposta i dati tra i nodi di lavoro Spark hello e database di Azure Cosmos come illustrato nel seguente diagramma hello:

![Flusso di dati nel connettore di hello Spark tooAzure Cosmos DB](./media/spark-connector/spark-connector.png)

flusso di dati Hello è come segue:

1. nodo principale di Hello Spark connette mappa partizione toohello Azure Cosmos DB gateway nodo tooobtain hello. Un utente specifica solo hello Spark e Azure Cosmos DB connessioni. Connessioni toohello rispettivi master e gateway sono nodi utente toohello trasparente.
2. Queste informazioni vengono fornite nodo principale di Spark toohello indietro.  A questo punto, deve essere in grado di tooparse hello query toodetermine hello partizioni e i relativi percorsi nel database di Azure Cosmos che è necessario tooaccess.
3. Queste informazioni sono trasmessi toohello Spark nodi di lavoro.
4. nodi di lavoro Spark Hello connettono toohello Azure Cosmos DB partizioni direttamente tooextract hello dati e restituire hello dati toohello partizioni Spark in nodi di lavoro di hello Spark.

La comunicazione tra Spark e Azure Cosmos DB è notevolmente più veloce perché lo spostamento dei dati di hello è tra i nodi di lavoro Spark hello e nodi di dati di Azure Cosmos DB hello (partizioni).

### <a name="build-hello-spark-tooazure-cosmos-db-connector"></a>Connettore di hello Spark tooAzure DB Cosmos di compilazione
Attualmente, il progetto di connettore hello utilizza maven. connettore di hello toobuild senza dipendenze, è possibile eseguire:
```
mvn clean package
```
È inoltre possibile scaricare le versioni più recenti di hello di hello JAR da hello *rilascia* cartella.

### <a name="include-hello-azure-cosmos-db-spark-jar"></a>Includere hello Azure Cosmos DB Spark JAR
Prima di eseguire qualsiasi codice, è necessario tooinclude hello Azure Cosmos DB Spark JAR.  Se si utilizza hello **spark shell**, è possibile includere hello JAR utilizzando hello **-JAR** opzione.  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

Se si desidera tooexecute hello JAR senza dipendenze, usare hello seguente codice:

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

Se si utilizza un servizio di blocco note, ad esempio servizio di Azure HDInsight Jupyter notebook, è possibile utilizzare hello **nascita magic** comandi:

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

Hello **JAR** comando abilita si tooinclude hello due file JAR che sono necessari per **azure-cosmosdb-spark** (stesso e hello Azure SDK per Java DocumentDB) ed escludere **scala-riflettere** in modo che non interferiscano con hello inserire il chiama (server Jupyter notebook > inserire il > Spark).

### <a name="connect-spark-tooazure-cosmos-db-using-hello-connector"></a>Connettersi Spark usando Cosmos DB tooAzure hello connettore
Anche se il trasporto di comunicazione hello è leggermente più complesso, l'esecuzione di una query da Spark tooAzure Cosmos DB tramite il connettore hello è molto veloce.

Hello frammento di codice seguente viene illustrato come toouse hello connettore in un contesto di Spark.

```
// Import Necessary Libraries
import org.joda.time._
import org.joda.time.format._
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Configure connection tooyour collection
val readConfig2 = Config(Map("Endpoint" -> "https://doctorwho.documents.azure.com:443/",
"Masterkey" -> "le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA==",
"Database" -> "DepartureDelays",
"preferredRegions" -> "Central US;East US2;",
"Collection" -> "flights_pcoll",
"SamplingRatio" -> "1.0"))

// Create collection connection
val coll = spark.sqlContext.read.cosmosDB(readConfig2)
coll.createOrReplaceTempView("c")
```

Come indicato nel frammento di codice hello:

- **Azure-cosmosdb-spark** contiene hello tutti hello parametri di connessione necessarie, che includono i percorsi di hello preferito. Ad esempio, è possibile scegliere di hello lettura dell'ordine di priorità e di replica.
- Solo hello necessarie librerie di importazione e configurare il client di Azure Cosmos DB hello di toocreate masterKey e host.

### <a name="execute-spark-queries-via-hello-connector"></a>Eseguire query Spark tramite il connettore hello

Hello seguente esempio Usa hello Azure Cosmos DB istanza creata nel frammento precedente hello utilizzando hello specifica le chiavi di sola lettura. Hello frammento di codice seguente si connette toohello DepartureDelays.flights_pcoll raccolta (in hello DoctorWho account come specificato in precedenza) e viene eseguita una query tooextract hello ritardo le informazioni di volo dei voli che sono abbandonare Seattle.

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-hello-spark-tooazure-cosmos-db-connector-implementation"></a>Perché utilizzare l'implementazione del connettore DB Cosmos tooAzure Spark hello?

Connessione tooAzure Spark Cosmos DB tramite il connettore hello è in genere per gli scenari in cui:

* Si desidera toouse Scala e aggiornarlo tooinclude un wrapper di Python, come indicato nella [problema 3: wrapper aggiungere Python ed esempi](https://github.com/Azure/azure-cosmosdb-spark/issues/3).
* Si dispone di una grande quantità di dati tootransfer tra Apache Spark e Azure Cosmos DB.

toogive un'idea della differenza di prestazioni delle query di hello, vedrai hello [wiki esecuzioni dei Test Query](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).

## <a name="distributed-aggregation-example"></a>Esempio di aggregazione distribuita
Questa sezione fornisce alcuni esempi di come è possibile eseguire analisi e aggregazioni distribuite combinando Apache Spark e Azure Cosmos DB. Azure DB Cosmos già supporta le aggregazioni, come descritto nell'hello [aggregazioni scala pianeta con blog di Azure Cosmos DB](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/). Ecco come è possibile trasferirli toohello successivo livello con Apache Spark.

Si noti che queste aggregazioni sono in riferimento toohello [notebook Cosmos DB Connector di Spark tooAzure](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).

### <a name="connect-tooflights-sample-data"></a>Connettere i dati di esempio tooflights
Queste aggregazioni di esempio accedono ad alcuni dati sulle prestazioni dei voli archiviati nel database Azure Cosmos DB **DoctorWho**. tooit tooconnect, è necessario hello tooutilize frammento di codice seguente:

```
// Import Spark tooAzure Cosmos DB connector
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Connect tooAzure Cosmos DB Database
val readConfig2 = Config(Map("Endpoint" -> "https://doctorwho.documents.azure.com:443/",
"Masterkey" -> "le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA==",
"Database" -> "DepartureDelays",
"preferredRegions" -> "Central US;East US 2;",
"Collection" -> "flights_pcoll",
"SamplingRatio" -> "1.0"))

// Create collection connection
val coll = spark.sqlContext.read.cosmosDB(readConfig2)
coll.createOrReplaceTempView("c")
```

Con questo frammento di codice, siamo anche passare toorun una query di base che i trasferimenti hello set filtrato di dati dal database di Azure Cosmos tooSpark in hello quest'ultimo può eseguire aggregazioni distribuite. In questo caso la richiesta è relativa ai voli in partenza da Seattle (SEA).

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

Hello risultati riportati di seguito sono stati generati eseguendo query hello dal servizio notebook Jupyter hello.  Si noti che tutti i frammenti di codice hello sono tooany generici e non specifici del servizio.

### <a name="running-limit-and-count-queries"></a>Esecuzione di query LIMIT e COUNT
Ad esempio si è appena utilizzata tooin SQL/Spark SQL, si iniziare con un **limite** query:

![Query LIMIT Spark](./media/spark-connector/spark-sql-query.png)

Hello query successiva è una semplice e rapido **conteggio** query:

![Query COUNT Spark](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a>Query GROUP BY
In questo set successivo è possibile eseguire facilmente query **GROUP BY** sul database Azure Cosmos DB:

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![Grafico della query GROUP BY Spark](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a>Query DISTINCT, ORDER BY
Di seguito una query **DISTINCT, ORDER BY**:

![Grafico della query GROUP BY Spark](./media/spark-connector/order-by-query.png)

### <a name="continue-hello-flight-data-analysis"></a>Continuare l'analisi dei dati di volo hello
È possibile utilizzare hello analisi toocontinue query di esempio di dati di volo hello:

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a>Prime 5 destinazioni (città) con ritardi in partenza da Seattle
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![Grafico dei ritardi massimi Spark](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a>Calcolare i ritardi medi per città di destinazione dei voli in partenza da Seattle
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![Grafico dei ritardi medi Spark](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a>Passaggi successivi

Se hai già fatto, scaricare connettore di hello Spark tooAzure DB Cosmos da hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) repository GitHub ed esplorare le risorse aggiuntive di hello in repository hello:

* [Esempi di aggregazioni distribuite](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)
* [Notebook e script di esempio](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)

È inoltre possibile hello tooreview [Apache Spark SQL, frame di dati e set di dati Guida](http://spark.apache.org/docs/latest/sql-programming-guide.html) hello e [Apache Spark in HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) articolo.
