---
title: Connessione di Apache Spark ad Azure Cosmos DB | Microsoft Docs
description: "Usare questa esercitazione per ottenere informazioni sul connettore Spark per Azure Cosmos DB, che consente di connettere Apache Spark ad Azure Cosmos DB per eseguire attività di data science e aggregazioni distribuite nel sistema di database multi-tenant con distribuzione globale di Microsoft progettato per il cloud."
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
ms.openlocfilehash: 8ecbb478c81cde25bbd0d1c9ee07ae02b07f8cc7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="accelerate-real-time-big-data-analytics-with-the-spark-to-azure-cosmos-db-connector"></a><span data-ttu-id="3aa3e-104">Velocizzare l'analisi di Big Data in tempo reale con il connettore Spark per Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3aa3e-104">Accelerate real-time big-data analytics with the Spark to Azure Cosmos DB connector</span></span>

<span data-ttu-id="3aa3e-105">Il connettore Spark per Azure Cosmos DB consente ad Azure Cosmos DB di fungere da origine di input o sink di output per i processi Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-105">The Spark to Azure Cosmos DB connector enables Azure Cosmos DB to act as an input source or output sink for Apache Spark jobs.</span></span> <span data-ttu-id="3aa3e-106">Connettendo [Spark](http://spark.apache.org/) ad [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/), è possibile risolvere più velocemente problemi di data science in rapida evoluzione usando Azure Cosmos DB per salvare in modo permanente i dati ed eseguire query su di essi in modo rapido.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-106">Connecting [Spark](http://spark.apache.org/) to [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) accelerates your ability to solve fast-moving data science problems where you can use Azure Cosmos DB to quickly persist and query data.</span></span> <span data-ttu-id="3aa3e-107">Il connettore Spark per Azure Cosmos DB usa in modo efficiente gli indici gestiti nativi di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-107">The Spark to Azure Cosmos DB connector efficiently utilizes the native Azure Cosmos DB managed indexes.</span></span> <span data-ttu-id="3aa3e-108">Gli indici consentono colonne aggiornabili in fase di analisi e propagazione del filtraggio in base al predicato per i dati distribuiti a livello globale in rapida evoluzione, che spaziano da scenari IoT (Internet delle cose) a scenari di data science e analisi.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-108">The indexes enable updateable columns when you perform analytics and push-down predicate filtering against fast-changing globally distributed data, which range from Internet of Things (IoT) to data science and analytics scenarios.</span></span>

<span data-ttu-id="3aa3e-109">Per usare Spark GraphX e le API Graph Gremlin di Azure Cosmos DB, vedere [Azure Cosmos DB: eseguire analisi dei grafi con Spark e Apache TinkerPop Gremlin](spark-connector-graph.md).</span><span class="sxs-lookup"><span data-stu-id="3aa3e-109">For working with Spark GraphX and the Gremlin graph APIs of Azure Cosmos DB, see [Perform graph analytics using Spark and Apache TinkerPop Gremlin](spark-connector-graph.md).</span></span>

## <a name="download"></a><span data-ttu-id="3aa3e-110">Scaricare</span><span class="sxs-lookup"><span data-stu-id="3aa3e-110">Download</span></span>

<span data-ttu-id="3aa3e-111">Per iniziare, scaricare il connettore Spark per Azure Cosmos DB (anteprima) dal repository [azure-documentdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) in GitHub.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-111">To get started, download the Spark to Azure Cosmos DB connector (preview) from the [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) repository on GitHub.</span></span>

## <a name="connector-components"></a><span data-ttu-id="3aa3e-112">Componenti del connettore</span><span class="sxs-lookup"><span data-stu-id="3aa3e-112">Connector components</span></span>

<span data-ttu-id="3aa3e-113">Sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-113">The connector utilizes the following components:</span></span>

* <span data-ttu-id="3aa3e-114">[Azure Cosmos DB](http://documentdb.com) consente ai clienti di effettuare il provisioning e ridimensionare in modo elastico la velocità effettiva e le risorse di archiviazione in un numero qualsiasi di aree geografiche.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-114">[Azure Cosmos DB](http://documentdb.com) enables customers to provision and elastically scale both throughput and storage across any number of geographical regions.</span></span> <span data-ttu-id="3aa3e-115">Il servizio offre:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-115">The service offers:</span></span>
   * <span data-ttu-id="3aa3e-116">[Distribuzione globale](distribute-data-globally.md) e scalabilità orizzontale chiavi in mano</span><span class="sxs-lookup"><span data-stu-id="3aa3e-116">Turn key [global distribution](distribute-data-globally.md) and horizontal scale</span></span>
   * <span data-ttu-id="3aa3e-117">Latenza garantita a una sola cifra al 99° percentile</span><span class="sxs-lookup"><span data-stu-id="3aa3e-117">Guaranteed single digit latencies at the 99th percentile</span></span>
   * [<span data-ttu-id="3aa3e-118">Più modelli di coerenza ben definiti</span><span class="sxs-lookup"><span data-stu-id="3aa3e-118">Multiple well-defined consistency models</span></span>](consistency-levels.md)
   * <span data-ttu-id="3aa3e-119">Disponibilità elevata garantita con funzionalità multihosting</span><span class="sxs-lookup"><span data-stu-id="3aa3e-119">Guaranteed high availability with multi-homing capabilities</span></span>
   * <span data-ttu-id="3aa3e-120">Tutte le funzionalità sono supportate da [contratti di servizio](https://azure.microsoft.com/support/legal/sla/cosmos-db) completi leader del settore.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-120">All features are backed by industry-leading, comprehensive [service level agreements](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLAs).</span></span>

* <span data-ttu-id="3aa3e-121">[Apache Spark](http://spark.apache.org/) è un potente motore di elaborazione open source incentrato su velocità, semplicità d'uso e analisi avanzata.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-121">[Apache Spark](http://spark.apache.org/) is a powerful open source processing engine that's built around speed, ease of use, and sophisticated analytics.</span></span>

* <span data-ttu-id="3aa3e-122">[Apache Spark in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) per poter distribuire Apache Spark nel cloud per distribuzioni cruciali usando [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="3aa3e-122">[Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) so that you can deploy Apache Spark in the cloud for mission-critical deployments by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="3aa3e-123">Versioni supportate ufficialmente:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-123">Officially supported versions:</span></span>

| <span data-ttu-id="3aa3e-124">Componente</span><span class="sxs-lookup"><span data-stu-id="3aa3e-124">Component</span></span> | <span data-ttu-id="3aa3e-125">Versione</span><span class="sxs-lookup"><span data-stu-id="3aa3e-125">Version</span></span> |
|---------|-------|
|<span data-ttu-id="3aa3e-126">Apache Spark</span><span class="sxs-lookup"><span data-stu-id="3aa3e-126">Apache Spark</span></span>|<span data-ttu-id="3aa3e-127">2.0+</span><span class="sxs-lookup"><span data-stu-id="3aa3e-127">2.0+</span></span>|
| <span data-ttu-id="3aa3e-128">Scala</span><span class="sxs-lookup"><span data-stu-id="3aa3e-128">Scala</span></span>| <span data-ttu-id="3aa3e-129">2.11</span><span class="sxs-lookup"><span data-stu-id="3aa3e-129">2.11</span></span>|
| <span data-ttu-id="3aa3e-130">Azure DocumentDB Java SDK</span><span class="sxs-lookup"><span data-stu-id="3aa3e-130">Azure DocumentDB Java SDK</span></span> | <span data-ttu-id="3aa3e-131">1.10.0</span><span class="sxs-lookup"><span data-stu-id="3aa3e-131">1.10.0</span></span> |

<span data-ttu-id="3aa3e-132">Questo articolo consente di eseguire alcuni semplici esempi con Python (tramite pyDocumentDB) e le interfacce di Scala.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-132">This article helps you run some simple samples by using Python (via pyDocumentDB) and the Scala interfaces.</span></span>

<span data-ttu-id="3aa3e-133">Per la connessione di Apache Spark e Azure Cosmos DB sono disponibili due approcci:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-133">There are two approaches to connect Apache Spark and Azure Cosmos DB:</span></span>
- <span data-ttu-id="3aa3e-134">Usare pyDocumentDB tramite [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).</span><span class="sxs-lookup"><span data-stu-id="3aa3e-134">Use pyDocumentDB via the [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).</span></span>
- <span data-ttu-id="3aa3e-135">Creare un connettore Spark per Azure Cosmos DB basato su Java usando [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="3aa3e-135">Create a Java-based Spark to Azure Cosmos DB connector by utilizing the [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

## <a name="pydocumentdb-implementation"></a><span data-ttu-id="3aa3e-136">Implementazione di pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="3aa3e-136">pyDocumentDB implementation</span></span>
<span data-ttu-id="3aa3e-137">La versione corrente di [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) consente di connettere Spark ad Azure Cosmos DB, come illustrato nel diagramma seguente:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-137">The current [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) enables you to connect Spark to Azure Cosmos DB as shown in the following diagram:</span></span>

![Flusso di dati da Spark ad Azure Cosmos DB tramite pyDocumentDB](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-the-pydocumentdb-implementation"></a><span data-ttu-id="3aa3e-139">Flusso di dati dell'implementazione di pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="3aa3e-139">Data flow of the pyDocumentDB implementation</span></span>

<span data-ttu-id="3aa3e-140">Il flusso di dati è il seguente:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-140">The data flow is as follows:</span></span>

1. <span data-ttu-id="3aa3e-141">Il nodo master Spark si connette al nodo del gateway Azure Cosmos DB tramite pyDocumentDB.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-141">The Spark master node connects to the Azure Cosmos DB gateway node via pyDocumentDB.</span></span> <span data-ttu-id="3aa3e-142">Un utente specifica solo le connessioni di Spark e Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-142">A user specifies only the Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="3aa3e-143">Le connessioni ai rispettivi nodi master e del gateway sono trasparenti per l'utente.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-143">Connections to the respective master and gateway nodes are transparent to the user.</span></span>
2. <span data-ttu-id="3aa3e-144">Il nodo del gateway esegue la query su Azure Cosmos DB, dove la query viene successivamente eseguita sulle partizioni della raccolta nei nodi dati.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-144">The gateway node makes the query against Azure Cosmos DB where the query subsequently runs against the collection's partitions in the data nodes.</span></span> <span data-ttu-id="3aa3e-145">La risposta a queste query viene inviata di nuovo al nodo del gateway e il set di risultati viene restituito al nodo master Spark.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-145">The response for those queries is sent back to the gateway node, and that result set is returned to the Spark master node.</span></span>
3. <span data-ttu-id="3aa3e-146">Le query successive, ad esempio su un frame di dati Spark, vengono inviate ai nodi di lavoro Spark per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-146">Subsequent queries (for example, against a Spark DataFrame) are sent to the Spark worker nodes for processing.</span></span>

<span data-ttu-id="3aa3e-147">La comunicazione tra Spark e Azure Cosmos DB è limitata al nodo master Spark e ai nodi del gateway Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-147">Communication between Spark and Azure Cosmos DB is limited to the Spark master node and Azure Cosmos DB gateway nodes.</span></span>  <span data-ttu-id="3aa3e-148">Le query vengono eseguite alla velocità consentita dal livello di trasporto tra i due nodi.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-148">The queries go as fast as the transport layer between these two nodes allows.</span></span>

### <a name="install-pydocumentdb"></a><span data-ttu-id="3aa3e-149">Installare pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="3aa3e-149">Install pyDocumentDB</span></span>
<span data-ttu-id="3aa3e-150">È possibile installare pyDocumentDB sul nodo del driver usando **pip**, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-150">You can install pyDocumentDB on your driver node by using **pip**, for example:</span></span>

```
pip install pyDocumentDB
```


### <a name="connect-spark-to-azure-cosmos-db-via-pydocumentdb"></a><span data-ttu-id="3aa3e-151">Connettere Spark ad Azure Cosmos DB tramite pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="3aa3e-151">Connect Spark to Azure Cosmos DB via pyDocumentDB</span></span>
<span data-ttu-id="3aa3e-152">La semplicità del trasporto di comunicazione rende relativamente semplice l'esecuzione di una query da Spark ad Azure Cosmos DB con pyDocumentDB.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-152">The simplicity of the communication transport makes execution of a query from Spark to Azure Cosmos DB by using pyDocumentDB relatively simple.</span></span>

<span data-ttu-id="3aa3e-153">Il frammento di codice seguente mostra come usare pyDocumentDB in un contesto Spark.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-153">The following code snippet shows how to use pyDocumentDB in a Spark context.</span></span>

```
# Import Necessary Libraries
import pydocumentdb
from pydocumentdb import document_client
from pydocumentdb import documents
import datetime

# Configuring the connection policy (allowing for endpoint discovery)
connectionPolicy = documents.ConnectionPolicy()
connectionPolicy.EnableEndpointDiscovery
connectionPolicy.PreferredLocations = ["Central US", "East US 2", "Southeast Asia", "Western Europe","Canada Central"]


# Set keys to connect to Azure Cosmos DB
masterKey = 'le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA=='
host = 'https://doctorwho.documents.azure.com:443/'
client = document_client.DocumentClient(host, {'masterKey': masterKey}, connectionPolicy)
```

<span data-ttu-id="3aa3e-154">Come indicato nel frammento di codice:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-154">As noted in the code snippet:</span></span>

* <span data-ttu-id="3aa3e-155">Azure Cosmos DB Python SDK (`pyDocumentDB`) contiene tutti i parametri di connessione necessari.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-155">The Azure Cosmos DB Python SDK (`pyDocumentDB`) contains the all the necessary connection parameters.</span></span> <span data-ttu-id="3aa3e-156">Il parametro relativo alle posizioni preferite determina ad esempio la replica di lettura e l'ordine di priorità.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-156">For example, the preferred locations parameter chooses the read replica and priority order.</span></span>
*  <span data-ttu-id="3aa3e-157">Importare le librerie necessarie e configurare **masterKey** e **host** per creare il *client* Azure Cosmos DB (**pydocumentdb.document_client**).</span><span class="sxs-lookup"><span data-stu-id="3aa3e-157">Import the necessary libraries and configure your **masterKey** and **host** to create the Azure Cosmos DB *client* (**pydocumentdb.document_client**).</span></span>


### <a name="execute-spark-queries-via-pydocumentdb"></a><span data-ttu-id="3aa3e-158">Eseguire query Spark tramite pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="3aa3e-158">Execute Spark Queries via pyDocumentDB</span></span>
<span data-ttu-id="3aa3e-159">Gli esempi seguenti usano l'istanza di Azure Cosmos DB creata nel frammento precedente con le chiavi di sola lettura specificate.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-159">The following examples use the Azure Cosmos DB instance that was created in the previous snippet by using the specified read-only keys.</span></span> <span data-ttu-id="3aa3e-160">Il frammento di codice seguente si connette alla raccolta **airports.codes** nell'account DoctorWho specificato in precedenza ed esegue una query per estrarre le città con aeroporto nello stato di Washington.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-160">The following code snippet connects to the **airports.codes** collection in the DoctorWho account as specified earlier and runs a query to extract the airport cities in Washington state.</span></span>

```
# Configure Database and Collections
databaseId = 'airports'
collectionId = 'codes'

# Configurations the Azure Cosmos DB client will use to connect to the database and collection
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

<span data-ttu-id="3aa3e-161">Dopo l'esecuzione della query tramite **query**, il risultato è un oggetto **query_iterable.QueryIterable** che viene convertito in un elenco Python.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-161">After the query has been executed via **query**, the result is a **query_iterable.QueryIterable** that is converted to a Python list.</span></span> <span data-ttu-id="3aa3e-162">Un elenco Python può essere convertito facilmente in un frame di dati Spark usando il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-162">A Python list can be easily converted to a Spark DataFrame by using the following code:</span></span>

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-the-pydocumentdb-to-connect-spark-to-azure-cosmos-db"></a><span data-ttu-id="3aa3e-163">Perché usare pyDocumentDB per connettere Spark ad Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="3aa3e-163">Why use the pyDocumentDB to connect Spark to Azure Cosmos DB?</span></span>
<span data-ttu-id="3aa3e-164">La connessione di Spark ad Azure Cosmos DB mediante pyDocumentDB viene usata in genere negli scenari in cui:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-164">Connecting Spark to Azure Cosmos DB by using pyDocumentDB is typically for scenarios where:</span></span>

* <span data-ttu-id="3aa3e-165">Si vuole usare Python.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-165">You want to use Python.</span></span>
* <span data-ttu-id="3aa3e-166">Si restituisce un set di risultati relativamente piccolo da Azure Cosmos DB a Spark.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-166">You are returning a relatively small result set from Azure Cosmos DB to Spark.</span></span> <span data-ttu-id="3aa3e-167">Si noti che il set di dati sottostante in Azure Cosmos DB può essere piuttosto grande.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-167">Note that the underlying dataset in Azure Cosmos DB can be quite large.</span></span> <span data-ttu-id="3aa3e-168">Si stanno applicando filtri, ovvero eseguendo filtri in base a predicati, sull'origine Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-168">You are applying filters, that is, running predicate filters, against your Azure Cosmos DB source.</span></span>  

## <a name="spark-to-azure-cosmos-db-connector"></a><span data-ttu-id="3aa3e-169">Connettore Spark per Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3aa3e-169">Spark to Azure Cosmos DB connector</span></span>

<span data-ttu-id="3aa3e-170">Il connettore Spark per Azure Cosmos DB usa [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) e sposta i dati tra i nodi di lavoro Spark e Azure Cosmos DB, come illustrato nel diagramma seguente:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-170">The Spark to Azure Cosmos DB connector utilizes the [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) and moves data between the Spark worker nodes and Azure Cosmos DB as shown in the following diagram:</span></span>

![Flusso di dati nel connettore Spark per Azure Cosmos DB](./media/spark-connector/spark-connector.png)

<span data-ttu-id="3aa3e-172">Il flusso di dati è il seguente:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-172">The data flow is as follows:</span></span>

1. <span data-ttu-id="3aa3e-173">Il nodo master Spark si connette al nodo del gateway Azure Cosmos DB per ottenere la mappa delle partizioni.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-173">The Spark master node connects to the Azure Cosmos DB gateway node to obtain the partition map.</span></span> <span data-ttu-id="3aa3e-174">Un utente specifica solo le connessioni di Spark e Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-174">A user specifies only the Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="3aa3e-175">Le connessioni ai rispettivi nodi master e del gateway sono trasparenti per l'utente.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-175">Connections to the respective master and gateway nodes are transparent to the user.</span></span>
2. <span data-ttu-id="3aa3e-176">Queste informazioni vengono restituite al nodo master Spark.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-176">This information is provided back to the Spark master node.</span></span>  <span data-ttu-id="3aa3e-177">A questo punto sarà possibile analizzare la query per determinare le partizioni e le relative posizioni in Azure Cosmos DB a cui è necessario accedere.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-177">At this point, you should be able to parse the query to determine the partitions and their locations in Azure Cosmos DB that you need to access.</span></span>
3. <span data-ttu-id="3aa3e-178">Queste informazioni vengono trasmesse ai nodi di lavoro Spark.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-178">This information is transmitted to the Spark worker nodes.</span></span>
4. <span data-ttu-id="3aa3e-179">I nodi di lavoro Spark si connettono direttamente alle partizioni Azure Cosmos DB per estrarre i dati e restituiscono i dati alle partizioni Spark nei nodi di lavoro Spark.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-179">The Spark worker nodes connect to the Azure Cosmos DB partitions directly to extract the data and return the data to the Spark partitions in the Spark worker nodes.</span></span>

<span data-ttu-id="3aa3e-180">La comunicazione tra Spark e Azure Cosmos DB è notevolmente più veloce perché lo spostamento dei dati avviene tra i nodi di lavoro Spark e i nodi dati (partizioni) Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-180">Communication between Spark and Azure Cosmos DB is significantly faster because the data movement is between the Spark worker nodes and the Azure Cosmos DB data nodes (partitions).</span></span>

### <a name="build-the-spark-to-azure-cosmos-db-connector"></a><span data-ttu-id="3aa3e-181">Creare il connettore Spark per Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3aa3e-181">Build the Spark to Azure Cosmos DB connector</span></span>
<span data-ttu-id="3aa3e-182">Attualmente il progetto del connettore usa Maven.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-182">Currently, the connector project uses maven.</span></span> <span data-ttu-id="3aa3e-183">Per creare il connettore senza le dipendenze, è possibile eseguire:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-183">To build the connector without dependencies, you can run:</span></span>
```
mvn clean package
```
<span data-ttu-id="3aa3e-184">È anche possibile scaricare le versioni più recenti del file JAR dalla cartella *releases*.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-184">You can also download the latest versions of the JAR from the *releases* folder.</span></span>

### <a name="include-the-azure-cosmos-db-spark-jar"></a><span data-ttu-id="3aa3e-185">Includere il file JAR di Spark per Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3aa3e-185">Include the Azure Cosmos DB Spark JAR</span></span>
<span data-ttu-id="3aa3e-186">Prima dell'esecuzione del codice, è necessario includere il file JAR di Spark per Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-186">Before you execute any code, you need to include the Azure Cosmos DB Spark JAR.</span></span>  <span data-ttu-id="3aa3e-187">Se si usa **spark-shell**, è possibile includere il file JAR usando l'opzione **--jars**.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-187">If you are using the **spark-shell**, then you can include the JAR by using the **--jars** option.</span></span>  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

<span data-ttu-id="3aa3e-188">Se si vuole eseguire il file JAR senza dipendenze, usare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-188">If you want to execute the JAR without dependencies, use the following code:</span></span>

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

<span data-ttu-id="3aa3e-189">Se si usa un servizio notebook, come Azure HDInsight Jupyter, è possibile usare i comandi **spark magic**:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-189">If you are using a notebook service such as Azure HDInsight Jupyter notebook service, you can use the **spark magic** commands:</span></span>

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

<span data-ttu-id="3aa3e-190">Il comando **jars** consente di includere i due file JAR necessari per **azure-cosmosdb-spark** (il file stesso e Azure DocumentDB Java SDK) ed escludere **scala-reflect** in modo da non interferire con le chiamate Livy (notebook Jupyter > Livy > Spark).</span><span class="sxs-lookup"><span data-stu-id="3aa3e-190">The **jars** command enables you to include the two JARs that are needed for **azure-cosmosdb-spark** (itself and the Azure DocumentDB Java SDK) and exclude **scala-reflect** so that it does not interfere with the Livy calls (Jupyter notebook > Livy > Spark).</span></span>

### <a name="connect-spark-to-azure-cosmos-db-using-the-connector"></a><span data-ttu-id="3aa3e-191">Connettere Spark ad Azure Cosmos DB con il connettore</span><span class="sxs-lookup"><span data-stu-id="3aa3e-191">Connect Spark to Azure Cosmos DB using the connector</span></span>
<span data-ttu-id="3aa3e-192">Anche se il trasporto di comunicazione è un po' più complesso, l'esecuzione di una query da Spark ad Azure Cosmos DB con il connettore è notevolmente più veloce.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-192">Although the communication transport is a little more complicated, executing a query from Spark to Azure Cosmos DB by using the connector is significantly faster.</span></span>

<span data-ttu-id="3aa3e-193">Il frammento di codice seguente illustra come usare il connettore in un contesto Spark.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-193">The following code snippet shows how to use the connector in a Spark context.</span></span>

```
// Import Necessary Libraries
import org.joda.time._
import org.joda.time.format._
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Configure connection to your collection
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

<span data-ttu-id="3aa3e-194">Come indicato nel frammento di codice:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-194">As noted in the code snippet:</span></span>

- <span data-ttu-id="3aa3e-195">**azure-cosmosdb-spark** contiene tutti i parametri di connessione necessari, che includono le posizioni preferite.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-195">**azure-cosmosdb-spark** contains the all the necessary connection parameters, which include the preferred locations.</span></span> <span data-ttu-id="3aa3e-196">È ad esempio possibile scegliere la replica di lettura e l'ordine di priorità.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-196">For example, you can choose the read replica and priority order.</span></span>
- <span data-ttu-id="3aa3e-197">Importare semplicemente le librerie necessarie e configurare masterKey e host per creare il client Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-197">Just import the necessary libraries and configure your masterKey and host to create the Azure Cosmos DB client.</span></span>

### <a name="execute-spark-queries-via-the-connector"></a><span data-ttu-id="3aa3e-198">Eseguire query Spark tramite il connettore</span><span class="sxs-lookup"><span data-stu-id="3aa3e-198">Execute Spark queries via the connector</span></span>

<span data-ttu-id="3aa3e-199">L'esempio seguente usa l'istanza di Azure Cosmos DB creata nel frammento precedente con le chiavi di sola lettura specificate.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-199">The following example uses the Azure Cosmos DB instance that was created in the previous snippet by using the specified read-only keys.</span></span> <span data-ttu-id="3aa3e-200">Il frammento di codice seguente consente la connessione alla raccolta DepartureDelays.flights_pcoll (nell'account DoctorWho specificato in precedenza) ed esegue una query per estrarre le informazioni sui ritardi dei voli in partenza da Seattle.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-200">The following code snippet connects to the DepartureDelays.flights_pcoll collection (in the DoctorWho account as specified earlier) and runs a query to extract the flight delay information of flights that are departing from Seattle.</span></span>

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-the-spark-to-azure-cosmos-db-connector-implementation"></a><span data-ttu-id="3aa3e-201">Vantaggi dell'implementazione del connettore Spark per Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3aa3e-201">Why use the Spark to Azure Cosmos DB connector implementation?</span></span>

<span data-ttu-id="3aa3e-202">La connessione di Spark ad Azure Cosmos DB con il connettore viene usata in genere negli scenari in cui:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-202">Connecting Spark to Azure Cosmos DB by using the connector is typically for scenarios where:</span></span>

* <span data-ttu-id="3aa3e-203">Si vuole usare Scala e aggiornarlo in modo da includere un wrapper Python come indicato in [Issue 3: Add Python wrapper and examples](https://github.com/Azure/azure-cosmosdb-spark/issues/3) (Problema 3: Aggiungere il wrapper Python ed esempi).</span><span class="sxs-lookup"><span data-stu-id="3aa3e-203">You want to use Scala and update it to include a Python wrapper as noted in [Issue 3: Add Python wrapper and examples](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span></span>
* <span data-ttu-id="3aa3e-204">La quantità di dati da trasferire tra Apache Spark e Azure Cosmos DB è elevata.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-204">You have a large amount of data to transfer between Apache Spark and Azure Cosmos DB.</span></span>

<span data-ttu-id="3aa3e-205">Per informazioni sulle differenze a livello di prestazioni delle query, vedere la [wiki sulle esecuzioni di test di query](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span><span class="sxs-lookup"><span data-stu-id="3aa3e-205">To give you an idea of the query performance difference, see the [Query Test Runs wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span></span>

## <a name="distributed-aggregation-example"></a><span data-ttu-id="3aa3e-206">Esempio di aggregazione distribuita</span><span class="sxs-lookup"><span data-stu-id="3aa3e-206">Distributed aggregation example</span></span>
<span data-ttu-id="3aa3e-207">Questa sezione fornisce alcuni esempi di come è possibile eseguire analisi e aggregazioni distribuite combinando Apache Spark e Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-207">This section provides some examples of how you can do distributed aggregations and analytics by using Apache Spark and Azure Cosmos DB together.</span></span> <span data-ttu-id="3aa3e-208">Azure Cosmos DB supporta già le aggregazioni, come illustrato nel post di blog sulle [aggregazioni su scala globale con Azure Cosmos DB](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span><span class="sxs-lookup"><span data-stu-id="3aa3e-208">Azure Cosmos DB already supports aggregations, which is discussed in the [Planet scale aggregates with Azure Cosmos DB blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span></span> <span data-ttu-id="3aa3e-209">Ecco come passare a un livello superiore con Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-209">Here is how you can take it to the next level with Apache Spark.</span></span>

<span data-ttu-id="3aa3e-210">Si noti che queste aggregazioni fanno riferimento al [notebook del connettore Spark per Azure Cosmos DB](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span><span class="sxs-lookup"><span data-stu-id="3aa3e-210">Note that these aggregations are in reference to the [Spark to Azure Cosmos DB Connector notebook](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span></span>

### <a name="connect-to-flights-sample-data"></a><span data-ttu-id="3aa3e-211">Eseguire la connessione ai dati di esempio sui voli</span><span class="sxs-lookup"><span data-stu-id="3aa3e-211">Connect to flights sample data</span></span>
<span data-ttu-id="3aa3e-212">Queste aggregazioni di esempio accedono ad alcuni dati sulle prestazioni dei voli archiviati nel database Azure Cosmos DB **DoctorWho**.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-212">These aggregation examples access some flight performance data that's stored in our **DoctorWho** Azure Cosmos DB database.</span></span> <span data-ttu-id="3aa3e-213">Per connettersi al database, è necessario usare il frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-213">To connect to it, you need to utilize the following code snippet:</span></span>

```
// Import Spark to Azure Cosmos DB connector
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Connect to Azure Cosmos DB Database
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

<span data-ttu-id="3aa3e-214">Con questo frammento si eseguirà anche una query di base che trasferisce il set di dati filtrato da Azure Cosmos DB a Spark, che potrà eseguire aggregazioni distribuite.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-214">With this snippet, we are also going to run a base query that transfers the filtered set of data from Azure Cosmos DB to Spark where the latter can perform distributed aggregates.</span></span> <span data-ttu-id="3aa3e-215">In questo caso la richiesta è relativa ai voli in partenza da Seattle (SEA).</span><span class="sxs-lookup"><span data-stu-id="3aa3e-215">In this case, we are asking for flights that depart from Seattle (SEA).</span></span>

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

<span data-ttu-id="3aa3e-216">I risultati seguenti sono stati generati eseguendo le query dal servizio notebook Jupyter.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-216">The following results were generated by running the queries from the Jupyter notebook service.</span></span>  <span data-ttu-id="3aa3e-217">Si noti che tutti i frammenti di codice sono generici e non specifici di un servizio.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-217">Note that all the code snippets are generic and not specific to any service.</span></span>

### <a name="running-limit-and-count-queries"></a><span data-ttu-id="3aa3e-218">Esecuzione di query LIMIT e COUNT</span><span class="sxs-lookup"><span data-stu-id="3aa3e-218">Running LIMIT and COUNT queries</span></span>
<span data-ttu-id="3aa3e-219">Come avviene in genere in SQL/Spark SQL, è possibile iniziare con una query **LIMIT**:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-219">Just like you're used to in SQL/Spark SQL, let's start off with a **LIMIT** query:</span></span>

![Query LIMIT Spark](./media/spark-connector/spark-sql-query.png)

<span data-ttu-id="3aa3e-221">La query successiva è una semplice e rapida query **COUNT**:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-221">The next query is a simple and fast **COUNT** query:</span></span>

![Query COUNT Spark](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a><span data-ttu-id="3aa3e-223">Query GROUP BY</span><span class="sxs-lookup"><span data-stu-id="3aa3e-223">GROUP BY query</span></span>
<span data-ttu-id="3aa3e-224">In questo set successivo è possibile eseguire facilmente query **GROUP BY** sul database Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-224">In this next set, we can easily run **GROUP BY** queries against our Azure Cosmos DB database:</span></span>

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![Grafico della query GROUP BY Spark](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a><span data-ttu-id="3aa3e-226">Query DISTINCT, ORDER BY</span><span class="sxs-lookup"><span data-stu-id="3aa3e-226">DISTINCT, ORDER BY query</span></span>
<span data-ttu-id="3aa3e-227">Di seguito una query **DISTINCT, ORDER BY**:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-227">And here is a **DISTINCT, ORDER BY** query:</span></span>

![Grafico della query GROUP BY Spark](./media/spark-connector/order-by-query.png)

### <a name="continue-the-flight-data-analysis"></a><span data-ttu-id="3aa3e-229">Continuare l'analisi dei dati relativi ai voli</span><span class="sxs-lookup"><span data-stu-id="3aa3e-229">Continue the flight data analysis</span></span>
<span data-ttu-id="3aa3e-230">Per continuare l'analisi di questi dati, è possibile usare le query di esempio seguenti:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-230">You can use the following example queries to continue analysis of the flight data:</span></span>

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a><span data-ttu-id="3aa3e-231">Prime 5 destinazioni (città) con ritardi in partenza da Seattle</span><span class="sxs-lookup"><span data-stu-id="3aa3e-231">Top 5 delayed destinations (cities) departing from Seattle</span></span>
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![Grafico dei ritardi massimi Spark](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a><span data-ttu-id="3aa3e-233">Calcolare i ritardi medi per città di destinazione dei voli in partenza da Seattle</span><span class="sxs-lookup"><span data-stu-id="3aa3e-233">Calculate median delays by destination cities departing from Seattle</span></span>
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![Grafico dei ritardi medi Spark](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a><span data-ttu-id="3aa3e-235">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3aa3e-235">Next steps</span></span>

<span data-ttu-id="3aa3e-236">Se ancora non lo si è fatto, scaricare il connettore Spark per Azure Cosmos DB dal repository GitHub [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) ed esplorare le risorse aggiuntive nel repository:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-236">If you haven't already, download the Spark to Azure Cosmos DB connector from the [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub repository and explore the additional resources in the repo:</span></span>

* [<span data-ttu-id="3aa3e-237">Esempi di aggregazioni distribuite</span><span class="sxs-lookup"><span data-stu-id="3aa3e-237">Distributed Aggregations Examples</span></span>](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)
* [<span data-ttu-id="3aa3e-238">Notebook e script di esempio</span><span class="sxs-lookup"><span data-stu-id="3aa3e-238">Sample Scripts and Notebooks</span></span>](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)

<span data-ttu-id="3aa3e-239">È possibile anche esaminare la [guida ad Apache Spark SQL, DataFrame e set di dati](http://spark.apache.org/docs/latest/sql-programming-guide.html) e l'articolo su [Apache Spark in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="3aa3e-239">You might also want to review the [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html) and the [Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) article.</span></span>
