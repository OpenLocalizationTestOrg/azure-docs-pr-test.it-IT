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
# <a name="accelerate-real-time-big-data-analytics-with-hello-spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="d8f68-104">Consente di accelerare analitica big dati in tempo reale con connettore di hello Spark tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d8f68-104">Accelerate real-time big-data analytics with hello Spark tooAzure Cosmos DB connector</span></span>

<span data-ttu-id="d8f68-105">connettore di Hello Spark tooAzure DB Cosmos consente tooact DB Cosmos Azure come origine di input o un sink di output per i processi di Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="d8f68-105">hello Spark tooAzure Cosmos DB connector enables Azure Cosmos DB tooact as an input source or output sink for Apache Spark jobs.</span></span> <span data-ttu-id="d8f68-106">Connessione [Spark](http://spark.apache.org/) troppo[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) accelera il possibilità toosolve rapido analisi scientifica dei dati in cui è possibile utilizzare Azure Cosmos DB tooquickly problemi persistono e query sui dati.</span><span class="sxs-lookup"><span data-stu-id="d8f68-106">Connecting [Spark](http://spark.apache.org/) too[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) accelerates your ability toosolve fast-moving data science problems where you can use Azure Cosmos DB tooquickly persist and query data.</span></span> <span data-ttu-id="d8f68-107">connettore di Hello Spark tooAzure DB Cosmos utilizza in modo efficiente hello nativo gestito di Azure Cosmos DB indici.</span><span class="sxs-lookup"><span data-stu-id="d8f68-107">hello Spark tooAzure Cosmos DB connector efficiently utilizes hello native Azure Cosmos DB managed indexes.</span></span> <span data-ttu-id="d8f68-108">Quando si esegue analitica e push-down predicato filtro rapido cambiamento globale distribuiti di dati, compresi tra gli scenari di scientifici e analitica toodata Internet delle cose (IoT), gli indici di Hello consentono colonne aggiornabili.</span><span class="sxs-lookup"><span data-stu-id="d8f68-108">hello indexes enable updateable columns when you perform analytics and push-down predicate filtering against fast-changing globally distributed data, which range from Internet of Things (IoT) toodata science and analytics scenarios.</span></span>

<span data-ttu-id="d8f68-109">Per l'utilizzo di GraphX Spark e di grafico Gremlin hello API di Azure Cosmos DB, vedere [eseguire analitica grafico utilizzando Spark e Apache TinkerPop Gremlin](spark-connector-graph.md).</span><span class="sxs-lookup"><span data-stu-id="d8f68-109">For working with Spark GraphX and hello Gremlin graph APIs of Azure Cosmos DB, see [Perform graph analytics using Spark and Apache TinkerPop Gremlin](spark-connector-graph.md).</span></span>

## <a name="download"></a><span data-ttu-id="d8f68-110">Scaricare</span><span class="sxs-lookup"><span data-stu-id="d8f68-110">Download</span></span>

<span data-ttu-id="d8f68-111">avvio tooget, scaricare hello Spark tooAzure Cosmos DB connector (anteprima) da hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) repository in GitHub.</span><span class="sxs-lookup"><span data-stu-id="d8f68-111">tooget started, download hello Spark tooAzure Cosmos DB connector (preview) from hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) repository on GitHub.</span></span>

## <a name="connector-components"></a><span data-ttu-id="d8f68-112">Componenti del connettore</span><span class="sxs-lookup"><span data-stu-id="d8f68-112">Connector components</span></span>

<span data-ttu-id="d8f68-113">connettore Hello Usa hello seguenti componenti:</span><span class="sxs-lookup"><span data-stu-id="d8f68-113">hello connector utilizes hello following components:</span></span>

* <span data-ttu-id="d8f68-114">[Azure DB Cosmos](http://documentdb.com) consente ai clienti tooprovision e scala elastico velocità effettiva e archiviazione per un numero qualsiasi di aree geografiche.</span><span class="sxs-lookup"><span data-stu-id="d8f68-114">[Azure Cosmos DB](http://documentdb.com) enables customers tooprovision and elastically scale both throughput and storage across any number of geographical regions.</span></span> <span data-ttu-id="d8f68-115">offerte di servizio Hello:</span><span class="sxs-lookup"><span data-stu-id="d8f68-115">hello service offers:</span></span>
   * <span data-ttu-id="d8f68-116">[Distribuzione globale](distribute-data-globally.md) e scalabilità orizzontale chiavi in mano</span><span class="sxs-lookup"><span data-stu-id="d8f68-116">Turn key [global distribution](distribute-data-globally.md) and horizontal scale</span></span>
   * <span data-ttu-id="d8f68-117">Le latenze di cifra al dato percentile 99th hello è garantito</span><span class="sxs-lookup"><span data-stu-id="d8f68-117">Guaranteed single digit latencies at hello 99th percentile</span></span>
   * [<span data-ttu-id="d8f68-118">Più modelli di coerenza ben definiti</span><span class="sxs-lookup"><span data-stu-id="d8f68-118">Multiple well-defined consistency models</span></span>](consistency-levels.md)
   * <span data-ttu-id="d8f68-119">Disponibilità elevata garantita con funzionalità multihosting</span><span class="sxs-lookup"><span data-stu-id="d8f68-119">Guaranteed high availability with multi-homing capabilities</span></span>
   * <span data-ttu-id="d8f68-120">Tutte le funzionalità sono supportate da [contratti di servizio](https://azure.microsoft.com/support/legal/sla/cosmos-db) completi leader del settore.</span><span class="sxs-lookup"><span data-stu-id="d8f68-120">All features are backed by industry-leading, comprehensive [service level agreements](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLAs).</span></span>

* <span data-ttu-id="d8f68-121">[Apache Spark](http://spark.apache.org/) è un potente motore di elaborazione open source incentrato su velocità, semplicità d'uso e analisi avanzata.</span><span class="sxs-lookup"><span data-stu-id="d8f68-121">[Apache Spark](http://spark.apache.org/) is a powerful open source processing engine that's built around speed, ease of use, and sophisticated analytics.</span></span>

* <span data-ttu-id="d8f68-122">[Apache Spark in HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) in modo che è possibile distribuire Apache Spark in cloud hello per le distribuzioni di importanza critica utilizzando [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="d8f68-122">[Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) so that you can deploy Apache Spark in hello cloud for mission-critical deployments by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="d8f68-123">Versioni supportate ufficialmente:</span><span class="sxs-lookup"><span data-stu-id="d8f68-123">Officially supported versions:</span></span>

| <span data-ttu-id="d8f68-124">Componente</span><span class="sxs-lookup"><span data-stu-id="d8f68-124">Component</span></span> | <span data-ttu-id="d8f68-125">Versione</span><span class="sxs-lookup"><span data-stu-id="d8f68-125">Version</span></span> |
|---------|-------|
|<span data-ttu-id="d8f68-126">Apache Spark</span><span class="sxs-lookup"><span data-stu-id="d8f68-126">Apache Spark</span></span>|<span data-ttu-id="d8f68-127">2.0+</span><span class="sxs-lookup"><span data-stu-id="d8f68-127">2.0+</span></span>|
| <span data-ttu-id="d8f68-128">Scala</span><span class="sxs-lookup"><span data-stu-id="d8f68-128">Scala</span></span>| <span data-ttu-id="d8f68-129">2.11</span><span class="sxs-lookup"><span data-stu-id="d8f68-129">2.11</span></span>|
| <span data-ttu-id="d8f68-130">Azure DocumentDB Java SDK</span><span class="sxs-lookup"><span data-stu-id="d8f68-130">Azure DocumentDB Java SDK</span></span> | <span data-ttu-id="d8f68-131">1.10.0</span><span class="sxs-lookup"><span data-stu-id="d8f68-131">1.10.0</span></span> |

<span data-ttu-id="d8f68-132">In questo articolo consente di eseguire alcuni semplici esempi con Python (tramite pyDocumentDB) e hello interfacce di Scala.</span><span class="sxs-lookup"><span data-stu-id="d8f68-132">This article helps you run some simple samples by using Python (via pyDocumentDB) and hello Scala interfaces.</span></span>

<span data-ttu-id="d8f68-133">Esistono due approcci tooconnect Apache Spark e Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="d8f68-133">There are two approaches tooconnect Apache Spark and Azure Cosmos DB:</span></span>
- <span data-ttu-id="d8f68-134">Utilizzare pyDocumentDB tramite hello [Azure SDK per Python DocumentDB](https://github.com/Azure/azure-documentdb-python).</span><span class="sxs-lookup"><span data-stu-id="d8f68-134">Use pyDocumentDB via hello [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).</span></span>
- <span data-ttu-id="d8f68-135">Creare un connettore di DB Cosmos tooAzure di Spark basati su Java utilizzando hello [Azure SDK per Java DocumentDB](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="d8f68-135">Create a Java-based Spark tooAzure Cosmos DB connector by utilizing hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

## <a name="pydocumentdb-implementation"></a><span data-ttu-id="d8f68-136">Implementazione di pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="d8f68-136">pyDocumentDB implementation</span></span>
<span data-ttu-id="d8f68-137">Hello corrente [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) consente tooconnect Spark tooAzure DB Cosmos come illustrato nel seguente diagramma hello:</span><span class="sxs-lookup"><span data-stu-id="d8f68-137">hello current [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) enables you tooconnect Spark tooAzure Cosmos DB as shown in hello following diagram:</span></span>

![Spark tooAzure flusso di dati DB Cosmos tramite pyDocumentDB DB](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-hello-pydocumentdb-implementation"></a><span data-ttu-id="d8f68-139">Flusso di dati di implementazione pyDocumentDB hello</span><span class="sxs-lookup"><span data-stu-id="d8f68-139">Data flow of hello pyDocumentDB implementation</span></span>

<span data-ttu-id="d8f68-140">flusso di dati Hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="d8f68-140">hello data flow is as follows:</span></span>

1. <span data-ttu-id="d8f68-141">nodo principale di Hello Spark connette nodo gateway di Azure Cosmos DB toohello tramite pyDocumentDB.</span><span class="sxs-lookup"><span data-stu-id="d8f68-141">hello Spark master node connects toohello Azure Cosmos DB gateway node via pyDocumentDB.</span></span> <span data-ttu-id="d8f68-142">Un utente specifica solo hello Spark e Azure Cosmos DB connessioni.</span><span class="sxs-lookup"><span data-stu-id="d8f68-142">A user specifies only hello Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="d8f68-143">Connessioni toohello rispettivi master e gateway sono nodi utente toohello trasparente.</span><span class="sxs-lookup"><span data-stu-id="d8f68-143">Connections toohello respective master and gateway nodes are transparent toohello user.</span></span>
2. <span data-ttu-id="d8f68-144">nodo gateway Hello rende query hello Azure Cosmos DB in cui query hello viene eseguita successivamente le partizioni dell'insieme di hello in nodi dati hello.</span><span class="sxs-lookup"><span data-stu-id="d8f68-144">hello gateway node makes hello query against Azure Cosmos DB where hello query subsequently runs against hello collection's partitions in hello data nodes.</span></span> <span data-ttu-id="d8f68-145">risposta Hello per le query viene inviato nuovamente il nodo di gateway toohello e tale set di risultati viene restituito toohello nodo principale di Spark.</span><span class="sxs-lookup"><span data-stu-id="d8f68-145">hello response for those queries is sent back toohello gateway node, and that result set is returned toohello Spark master node.</span></span>
3. <span data-ttu-id="d8f68-146">Le query successive (ad esempio, su un frame di dati di Spark) vengono inviate i nodi di lavoro Spark toohello per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="d8f68-146">Subsequent queries (for example, against a Spark DataFrame) are sent toohello Spark worker nodes for processing.</span></span>

<span data-ttu-id="d8f68-147">La comunicazione tra Spark e Azure Cosmos DB è limitato toohello nodo principale di Spark e nodi di Azure Cosmos DB gateway.</span><span class="sxs-lookup"><span data-stu-id="d8f68-147">Communication between Spark and Azure Cosmos DB is limited toohello Spark master node and Azure Cosmos DB gateway nodes.</span></span>  <span data-ttu-id="d8f68-148">le query Hello passare la stessa velocità consente a livello di trasporto hello tra questi due nodi.</span><span class="sxs-lookup"><span data-stu-id="d8f68-148">hello queries go as fast as hello transport layer between these two nodes allows.</span></span>

### <a name="install-pydocumentdb"></a><span data-ttu-id="d8f68-149">Installare pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="d8f68-149">Install pyDocumentDB</span></span>
<span data-ttu-id="d8f68-150">È possibile installare pyDocumentDB sul nodo del driver usando **pip**, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d8f68-150">You can install pyDocumentDB on your driver node by using **pip**, for example:</span></span>

```
pip install pyDocumentDB
```


### <a name="connect-spark-tooazure-cosmos-db-via-pydocumentdb"></a><span data-ttu-id="d8f68-151">Connettersi Spark tooAzure DB Cosmos tramite pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="d8f68-151">Connect Spark tooAzure Cosmos DB via pyDocumentDB</span></span>
<span data-ttu-id="d8f68-152">semplicità di Hello del trasporto di comunicazione hello rende l'esecuzione di una query da Spark tooAzure DB Cosmos utilizzando pyDocumentDB relativamente semplice.</span><span class="sxs-lookup"><span data-stu-id="d8f68-152">hello simplicity of hello communication transport makes execution of a query from Spark tooAzure Cosmos DB by using pyDocumentDB relatively simple.</span></span>

<span data-ttu-id="d8f68-153">Hello seguente frammento di codice viene illustrato come pyDocumentDB toouse in un contesto di Spark.</span><span class="sxs-lookup"><span data-stu-id="d8f68-153">hello following code snippet shows how toouse pyDocumentDB in a Spark context.</span></span>

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

<span data-ttu-id="d8f68-154">Come indicato nel frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="d8f68-154">As noted in hello code snippet:</span></span>

* <span data-ttu-id="d8f68-155">Hello Azure Cosmos DB Python SDK (`pyDocumentDB`) contiene hello tutti hello parametri di connessione necessarie.</span><span class="sxs-lookup"><span data-stu-id="d8f68-155">hello Azure Cosmos DB Python SDK (`pyDocumentDB`) contains hello all hello necessary connection parameters.</span></span> <span data-ttu-id="d8f68-156">Ad esempio, hello preferito parametro percorsi sceglie hello lettura dell'ordine di priorità e di replica.</span><span class="sxs-lookup"><span data-stu-id="d8f68-156">For example, hello preferred locations parameter chooses hello read replica and priority order.</span></span>
*  <span data-ttu-id="d8f68-157">Importare le librerie necessarie hello e configurare il **masterKey** e **host** toocreate hello Azure Cosmos DB *client* (**pydocumentdb.document_ client**).</span><span class="sxs-lookup"><span data-stu-id="d8f68-157">Import hello necessary libraries and configure your **masterKey** and **host** toocreate hello Azure Cosmos DB *client* (**pydocumentdb.document_client**).</span></span>


### <a name="execute-spark-queries-via-pydocumentdb"></a><span data-ttu-id="d8f68-158">Eseguire query Spark tramite pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="d8f68-158">Execute Spark Queries via pyDocumentDB</span></span>
<span data-ttu-id="d8f68-159">Hello seguenti esempi usare hello Azure Cosmos DB l'istanza che è stato creato nel frammento precedente hello utilizzando hello specifica le chiavi di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="d8f68-159">hello following examples use hello Azure Cosmos DB instance that was created in hello previous snippet by using hello specified read-only keys.</span></span> <span data-ttu-id="d8f68-160">frammento di codice seguente Hello connette toohello **airports.codes** insieme nell'account DoctorWho hello come specificato in precedenza e viene eseguito un aeroporto di hello tooextract query città nello stato di Washington.</span><span class="sxs-lookup"><span data-stu-id="d8f68-160">hello following code snippet connects toohello **airports.codes** collection in hello DoctorWho account as specified earlier and runs a query tooextract hello airport cities in Washington state.</span></span>

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

<span data-ttu-id="d8f68-161">Dopo l'esecuzione di query hello tramite **query**, hello risultato è un **query_iterable. QueryIterable** ovvero convertito tooa Python elenco.</span><span class="sxs-lookup"><span data-stu-id="d8f68-161">After hello query has been executed via **query**, hello result is a **query_iterable.QueryIterable** that is converted tooa Python list.</span></span> <span data-ttu-id="d8f68-162">Un elenco di Python può essere convertito facilmente tooa frame di dati di Spark usando hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="d8f68-162">A Python list can be easily converted tooa Spark DataFrame by using hello following code:</span></span>

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-hello-pydocumentdb-tooconnect-spark-tooazure-cosmos-db"></a><span data-ttu-id="d8f68-163">Perché utilizzare hello pyDocumentDB tooconnect Spark tooAzure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="d8f68-163">Why use hello pyDocumentDB tooconnect Spark tooAzure Cosmos DB?</span></span>
<span data-ttu-id="d8f68-164">Connessione tooAzure Spark DB Cosmos utilizzando pyDocumentDB è in genere per gli scenari in cui:</span><span class="sxs-lookup"><span data-stu-id="d8f68-164">Connecting Spark tooAzure Cosmos DB by using pyDocumentDB is typically for scenarios where:</span></span>

* <span data-ttu-id="d8f68-165">Si desidera toouse Python.</span><span class="sxs-lookup"><span data-stu-id="d8f68-165">You want toouse Python.</span></span>
* <span data-ttu-id="d8f68-166">Viene restituito un relativamente piccolo set di risultati da Azure Cosmos DB tooSpark.</span><span class="sxs-lookup"><span data-stu-id="d8f68-166">You are returning a relatively small result set from Azure Cosmos DB tooSpark.</span></span> <span data-ttu-id="d8f68-167">Si noti che un set di dati sottostante nel database di Azure Cosmos hello possono essere notevoli.</span><span class="sxs-lookup"><span data-stu-id="d8f68-167">Note that hello underlying dataset in Azure Cosmos DB can be quite large.</span></span> <span data-ttu-id="d8f68-168">Si stanno applicando filtri, ovvero eseguendo filtri in base a predicati, sull'origine Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d8f68-168">You are applying filters, that is, running predicate filters, against your Azure Cosmos DB source.</span></span>  

## <a name="spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="d8f68-169">Spark tooAzure Cosmos DB connector</span><span class="sxs-lookup"><span data-stu-id="d8f68-169">Spark tooAzure Cosmos DB connector</span></span>

<span data-ttu-id="d8f68-170">connettore di Hello Spark tooAzure DB Cosmos utilizza hello [Azure SDK per Java DocumentDB](https://github.com/Azure/azure-documentdb-java) e sposta i dati tra i nodi di lavoro Spark hello e database di Azure Cosmos come illustrato nel seguente diagramma hello:</span><span class="sxs-lookup"><span data-stu-id="d8f68-170">hello Spark tooAzure Cosmos DB connector utilizes hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) and moves data between hello Spark worker nodes and Azure Cosmos DB as shown in hello following diagram:</span></span>

![Flusso di dati nel connettore di hello Spark tooAzure Cosmos DB](./media/spark-connector/spark-connector.png)

<span data-ttu-id="d8f68-172">flusso di dati Hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="d8f68-172">hello data flow is as follows:</span></span>

1. <span data-ttu-id="d8f68-173">nodo principale di Hello Spark connette mappa partizione toohello Azure Cosmos DB gateway nodo tooobtain hello.</span><span class="sxs-lookup"><span data-stu-id="d8f68-173">hello Spark master node connects toohello Azure Cosmos DB gateway node tooobtain hello partition map.</span></span> <span data-ttu-id="d8f68-174">Un utente specifica solo hello Spark e Azure Cosmos DB connessioni.</span><span class="sxs-lookup"><span data-stu-id="d8f68-174">A user specifies only hello Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="d8f68-175">Connessioni toohello rispettivi master e gateway sono nodi utente toohello trasparente.</span><span class="sxs-lookup"><span data-stu-id="d8f68-175">Connections toohello respective master and gateway nodes are transparent toohello user.</span></span>
2. <span data-ttu-id="d8f68-176">Queste informazioni vengono fornite nodo principale di Spark toohello indietro.</span><span class="sxs-lookup"><span data-stu-id="d8f68-176">This information is provided back toohello Spark master node.</span></span>  <span data-ttu-id="d8f68-177">A questo punto, deve essere in grado di tooparse hello query toodetermine hello partizioni e i relativi percorsi nel database di Azure Cosmos che è necessario tooaccess.</span><span class="sxs-lookup"><span data-stu-id="d8f68-177">At this point, you should be able tooparse hello query toodetermine hello partitions and their locations in Azure Cosmos DB that you need tooaccess.</span></span>
3. <span data-ttu-id="d8f68-178">Queste informazioni sono trasmessi toohello Spark nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="d8f68-178">This information is transmitted toohello Spark worker nodes.</span></span>
4. <span data-ttu-id="d8f68-179">nodi di lavoro Spark Hello connettono toohello Azure Cosmos DB partizioni direttamente tooextract hello dati e restituire hello dati toohello partizioni Spark in nodi di lavoro di hello Spark.</span><span class="sxs-lookup"><span data-stu-id="d8f68-179">hello Spark worker nodes connect toohello Azure Cosmos DB partitions directly tooextract hello data and return hello data toohello Spark partitions in hello Spark worker nodes.</span></span>

<span data-ttu-id="d8f68-180">La comunicazione tra Spark e Azure Cosmos DB è notevolmente più veloce perché lo spostamento dei dati di hello è tra i nodi di lavoro Spark hello e nodi di dati di Azure Cosmos DB hello (partizioni).</span><span class="sxs-lookup"><span data-stu-id="d8f68-180">Communication between Spark and Azure Cosmos DB is significantly faster because hello data movement is between hello Spark worker nodes and hello Azure Cosmos DB data nodes (partitions).</span></span>

### <a name="build-hello-spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="d8f68-181">Connettore di hello Spark tooAzure DB Cosmos di compilazione</span><span class="sxs-lookup"><span data-stu-id="d8f68-181">Build hello Spark tooAzure Cosmos DB connector</span></span>
<span data-ttu-id="d8f68-182">Attualmente, il progetto di connettore hello utilizza maven.</span><span class="sxs-lookup"><span data-stu-id="d8f68-182">Currently, hello connector project uses maven.</span></span> <span data-ttu-id="d8f68-183">connettore di hello toobuild senza dipendenze, è possibile eseguire:</span><span class="sxs-lookup"><span data-stu-id="d8f68-183">toobuild hello connector without dependencies, you can run:</span></span>
```
mvn clean package
```
<span data-ttu-id="d8f68-184">È inoltre possibile scaricare le versioni più recenti di hello di hello JAR da hello *rilascia* cartella.</span><span class="sxs-lookup"><span data-stu-id="d8f68-184">You can also download hello latest versions of hello JAR from hello *releases* folder.</span></span>

### <a name="include-hello-azure-cosmos-db-spark-jar"></a><span data-ttu-id="d8f68-185">Includere hello Azure Cosmos DB Spark JAR</span><span class="sxs-lookup"><span data-stu-id="d8f68-185">Include hello Azure Cosmos DB Spark JAR</span></span>
<span data-ttu-id="d8f68-186">Prima di eseguire qualsiasi codice, è necessario tooinclude hello Azure Cosmos DB Spark JAR.</span><span class="sxs-lookup"><span data-stu-id="d8f68-186">Before you execute any code, you need tooinclude hello Azure Cosmos DB Spark JAR.</span></span>  <span data-ttu-id="d8f68-187">Se si utilizza hello **spark shell**, è possibile includere hello JAR utilizzando hello **-JAR** opzione.</span><span class="sxs-lookup"><span data-stu-id="d8f68-187">If you are using hello **spark-shell**, then you can include hello JAR by using hello **--jars** option.</span></span>  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

<span data-ttu-id="d8f68-188">Se si desidera tooexecute hello JAR senza dipendenze, usare hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="d8f68-188">If you want tooexecute hello JAR without dependencies, use hello following code:</span></span>

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

<span data-ttu-id="d8f68-189">Se si utilizza un servizio di blocco note, ad esempio servizio di Azure HDInsight Jupyter notebook, è possibile utilizzare hello **nascita magic** comandi:</span><span class="sxs-lookup"><span data-stu-id="d8f68-189">If you are using a notebook service such as Azure HDInsight Jupyter notebook service, you can use hello **spark magic** commands:</span></span>

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

<span data-ttu-id="d8f68-190">Hello **JAR** comando abilita si tooinclude hello due file JAR che sono necessari per **azure-cosmosdb-spark** (stesso e hello Azure SDK per Java DocumentDB) ed escludere **scala-riflettere** in modo che non interferiscano con hello inserire il chiama (server Jupyter notebook > inserire il > Spark).</span><span class="sxs-lookup"><span data-stu-id="d8f68-190">hello **jars** command enables you tooinclude hello two JARs that are needed for **azure-cosmosdb-spark** (itself and hello Azure DocumentDB Java SDK) and exclude **scala-reflect** so that it does not interfere with hello Livy calls (Jupyter notebook > Livy > Spark).</span></span>

### <a name="connect-spark-tooazure-cosmos-db-using-hello-connector"></a><span data-ttu-id="d8f68-191">Connettersi Spark usando Cosmos DB tooAzure hello connettore</span><span class="sxs-lookup"><span data-stu-id="d8f68-191">Connect Spark tooAzure Cosmos DB using hello connector</span></span>
<span data-ttu-id="d8f68-192">Anche se il trasporto di comunicazione hello è leggermente più complesso, l'esecuzione di una query da Spark tooAzure Cosmos DB tramite il connettore hello è molto veloce.</span><span class="sxs-lookup"><span data-stu-id="d8f68-192">Although hello communication transport is a little more complicated, executing a query from Spark tooAzure Cosmos DB by using hello connector is significantly faster.</span></span>

<span data-ttu-id="d8f68-193">Hello frammento di codice seguente viene illustrato come toouse hello connettore in un contesto di Spark.</span><span class="sxs-lookup"><span data-stu-id="d8f68-193">hello following code snippet shows how toouse hello connector in a Spark context.</span></span>

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

<span data-ttu-id="d8f68-194">Come indicato nel frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="d8f68-194">As noted in hello code snippet:</span></span>

- <span data-ttu-id="d8f68-195">**Azure-cosmosdb-spark** contiene hello tutti hello parametri di connessione necessarie, che includono i percorsi di hello preferito.</span><span class="sxs-lookup"><span data-stu-id="d8f68-195">**azure-cosmosdb-spark** contains hello all hello necessary connection parameters, which include hello preferred locations.</span></span> <span data-ttu-id="d8f68-196">Ad esempio, è possibile scegliere di hello lettura dell'ordine di priorità e di replica.</span><span class="sxs-lookup"><span data-stu-id="d8f68-196">For example, you can choose hello read replica and priority order.</span></span>
- <span data-ttu-id="d8f68-197">Solo hello necessarie librerie di importazione e configurare il client di Azure Cosmos DB hello di toocreate masterKey e host.</span><span class="sxs-lookup"><span data-stu-id="d8f68-197">Just import hello necessary libraries and configure your masterKey and host toocreate hello Azure Cosmos DB client.</span></span>

### <a name="execute-spark-queries-via-hello-connector"></a><span data-ttu-id="d8f68-198">Eseguire query Spark tramite il connettore hello</span><span class="sxs-lookup"><span data-stu-id="d8f68-198">Execute Spark queries via hello connector</span></span>

<span data-ttu-id="d8f68-199">Hello seguente esempio Usa hello Azure Cosmos DB istanza creata nel frammento precedente hello utilizzando hello specifica le chiavi di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="d8f68-199">hello following example uses hello Azure Cosmos DB instance that was created in hello previous snippet by using hello specified read-only keys.</span></span> <span data-ttu-id="d8f68-200">Hello frammento di codice seguente si connette toohello DepartureDelays.flights_pcoll raccolta (in hello DoctorWho account come specificato in precedenza) e viene eseguita una query tooextract hello ritardo le informazioni di volo dei voli che sono abbandonare Seattle.</span><span class="sxs-lookup"><span data-stu-id="d8f68-200">hello following code snippet connects toohello DepartureDelays.flights_pcoll collection (in hello DoctorWho account as specified earlier) and runs a query tooextract hello flight delay information of flights that are departing from Seattle.</span></span>

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-hello-spark-tooazure-cosmos-db-connector-implementation"></a><span data-ttu-id="d8f68-201">Perché utilizzare l'implementazione del connettore DB Cosmos tooAzure Spark hello?</span><span class="sxs-lookup"><span data-stu-id="d8f68-201">Why use hello Spark tooAzure Cosmos DB connector implementation?</span></span>

<span data-ttu-id="d8f68-202">Connessione tooAzure Spark Cosmos DB tramite il connettore hello è in genere per gli scenari in cui:</span><span class="sxs-lookup"><span data-stu-id="d8f68-202">Connecting Spark tooAzure Cosmos DB by using hello connector is typically for scenarios where:</span></span>

* <span data-ttu-id="d8f68-203">Si desidera toouse Scala e aggiornarlo tooinclude un wrapper di Python, come indicato nella [problema 3: wrapper aggiungere Python ed esempi](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span><span class="sxs-lookup"><span data-stu-id="d8f68-203">You want toouse Scala and update it tooinclude a Python wrapper as noted in [Issue 3: Add Python wrapper and examples](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span></span>
* <span data-ttu-id="d8f68-204">Si dispone di una grande quantità di dati tootransfer tra Apache Spark e Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d8f68-204">You have a large amount of data tootransfer between Apache Spark and Azure Cosmos DB.</span></span>

<span data-ttu-id="d8f68-205">toogive un'idea della differenza di prestazioni delle query di hello, vedrai hello [wiki esecuzioni dei Test Query](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span><span class="sxs-lookup"><span data-stu-id="d8f68-205">toogive you an idea of hello query performance difference, see hello [Query Test Runs wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span></span>

## <a name="distributed-aggregation-example"></a><span data-ttu-id="d8f68-206">Esempio di aggregazione distribuita</span><span class="sxs-lookup"><span data-stu-id="d8f68-206">Distributed aggregation example</span></span>
<span data-ttu-id="d8f68-207">Questa sezione fornisce alcuni esempi di come è possibile eseguire analisi e aggregazioni distribuite combinando Apache Spark e Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d8f68-207">This section provides some examples of how you can do distributed aggregations and analytics by using Apache Spark and Azure Cosmos DB together.</span></span> <span data-ttu-id="d8f68-208">Azure DB Cosmos già supporta le aggregazioni, come descritto nell'hello [aggregazioni scala pianeta con blog di Azure Cosmos DB](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span><span class="sxs-lookup"><span data-stu-id="d8f68-208">Azure Cosmos DB already supports aggregations, which is discussed in hello [Planet scale aggregates with Azure Cosmos DB blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span></span> <span data-ttu-id="d8f68-209">Ecco come è possibile trasferirli toohello successivo livello con Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="d8f68-209">Here is how you can take it toohello next level with Apache Spark.</span></span>

<span data-ttu-id="d8f68-210">Si noti che queste aggregazioni sono in riferimento toohello [notebook Cosmos DB Connector di Spark tooAzure](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span><span class="sxs-lookup"><span data-stu-id="d8f68-210">Note that these aggregations are in reference toohello [Spark tooAzure Cosmos DB Connector notebook](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span></span>

### <a name="connect-tooflights-sample-data"></a><span data-ttu-id="d8f68-211">Connettere i dati di esempio tooflights</span><span class="sxs-lookup"><span data-stu-id="d8f68-211">Connect tooflights sample data</span></span>
<span data-ttu-id="d8f68-212">Queste aggregazioni di esempio accedono ad alcuni dati sulle prestazioni dei voli archiviati nel database Azure Cosmos DB **DoctorWho**.</span><span class="sxs-lookup"><span data-stu-id="d8f68-212">These aggregation examples access some flight performance data that's stored in our **DoctorWho** Azure Cosmos DB database.</span></span> <span data-ttu-id="d8f68-213">tooit tooconnect, è necessario hello tooutilize frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="d8f68-213">tooconnect tooit, you need tooutilize hello following code snippet:</span></span>

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

<span data-ttu-id="d8f68-214">Con questo frammento di codice, siamo anche passare toorun una query di base che i trasferimenti hello set filtrato di dati dal database di Azure Cosmos tooSpark in hello quest'ultimo può eseguire aggregazioni distribuite.</span><span class="sxs-lookup"><span data-stu-id="d8f68-214">With this snippet, we are also going toorun a base query that transfers hello filtered set of data from Azure Cosmos DB tooSpark where hello latter can perform distributed aggregates.</span></span> <span data-ttu-id="d8f68-215">In questo caso la richiesta è relativa ai voli in partenza da Seattle (SEA).</span><span class="sxs-lookup"><span data-stu-id="d8f68-215">In this case, we are asking for flights that depart from Seattle (SEA).</span></span>

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

<span data-ttu-id="d8f68-216">Hello risultati riportati di seguito sono stati generati eseguendo query hello dal servizio notebook Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="d8f68-216">hello following results were generated by running hello queries from hello Jupyter notebook service.</span></span>  <span data-ttu-id="d8f68-217">Si noti che tutti i frammenti di codice hello sono tooany generici e non specifici del servizio.</span><span class="sxs-lookup"><span data-stu-id="d8f68-217">Note that all hello code snippets are generic and not specific tooany service.</span></span>

### <a name="running-limit-and-count-queries"></a><span data-ttu-id="d8f68-218">Esecuzione di query LIMIT e COUNT</span><span class="sxs-lookup"><span data-stu-id="d8f68-218">Running LIMIT and COUNT queries</span></span>
<span data-ttu-id="d8f68-219">Ad esempio si è appena utilizzata tooin SQL/Spark SQL, si iniziare con un **limite** query:</span><span class="sxs-lookup"><span data-stu-id="d8f68-219">Just like you're used tooin SQL/Spark SQL, let's start off with a **LIMIT** query:</span></span>

![Query LIMIT Spark](./media/spark-connector/spark-sql-query.png)

<span data-ttu-id="d8f68-221">Hello query successiva è una semplice e rapido **conteggio** query:</span><span class="sxs-lookup"><span data-stu-id="d8f68-221">hello next query is a simple and fast **COUNT** query:</span></span>

![Query COUNT Spark](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a><span data-ttu-id="d8f68-223">Query GROUP BY</span><span class="sxs-lookup"><span data-stu-id="d8f68-223">GROUP BY query</span></span>
<span data-ttu-id="d8f68-224">In questo set successivo è possibile eseguire facilmente query **GROUP BY** sul database Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="d8f68-224">In this next set, we can easily run **GROUP BY** queries against our Azure Cosmos DB database:</span></span>

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![Grafico della query GROUP BY Spark](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a><span data-ttu-id="d8f68-226">Query DISTINCT, ORDER BY</span><span class="sxs-lookup"><span data-stu-id="d8f68-226">DISTINCT, ORDER BY query</span></span>
<span data-ttu-id="d8f68-227">Di seguito una query **DISTINCT, ORDER BY**:</span><span class="sxs-lookup"><span data-stu-id="d8f68-227">And here is a **DISTINCT, ORDER BY** query:</span></span>

![Grafico della query GROUP BY Spark](./media/spark-connector/order-by-query.png)

### <a name="continue-hello-flight-data-analysis"></a><span data-ttu-id="d8f68-229">Continuare l'analisi dei dati di volo hello</span><span class="sxs-lookup"><span data-stu-id="d8f68-229">Continue hello flight data analysis</span></span>
<span data-ttu-id="d8f68-230">È possibile utilizzare hello analisi toocontinue query di esempio di dati di volo hello:</span><span class="sxs-lookup"><span data-stu-id="d8f68-230">You can use hello following example queries toocontinue analysis of hello flight data:</span></span>

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a><span data-ttu-id="d8f68-231">Prime 5 destinazioni (città) con ritardi in partenza da Seattle</span><span class="sxs-lookup"><span data-stu-id="d8f68-231">Top 5 delayed destinations (cities) departing from Seattle</span></span>
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![Grafico dei ritardi massimi Spark](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a><span data-ttu-id="d8f68-233">Calcolare i ritardi medi per città di destinazione dei voli in partenza da Seattle</span><span class="sxs-lookup"><span data-stu-id="d8f68-233">Calculate median delays by destination cities departing from Seattle</span></span>
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![Grafico dei ritardi medi Spark](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a><span data-ttu-id="d8f68-235">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d8f68-235">Next steps</span></span>

<span data-ttu-id="d8f68-236">Se hai già fatto, scaricare connettore di hello Spark tooAzure DB Cosmos da hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) repository GitHub ed esplorare le risorse aggiuntive di hello in repository hello:</span><span class="sxs-lookup"><span data-stu-id="d8f68-236">If you haven't already, download hello Spark tooAzure Cosmos DB connector from hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub repository and explore hello additional resources in hello repo:</span></span>

* [<span data-ttu-id="d8f68-237">Esempi di aggregazioni distribuite</span><span class="sxs-lookup"><span data-stu-id="d8f68-237">Distributed Aggregations Examples</span></span>](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)
* [<span data-ttu-id="d8f68-238">Notebook e script di esempio</span><span class="sxs-lookup"><span data-stu-id="d8f68-238">Sample Scripts and Notebooks</span></span>](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)

<span data-ttu-id="d8f68-239">È inoltre possibile hello tooreview [Apache Spark SQL, frame di dati e set di dati Guida](http://spark.apache.org/docs/latest/sql-programming-guide.html) hello e [Apache Spark in HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="d8f68-239">You might also want tooreview hello [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html) and hello [Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) article.</span></span>
