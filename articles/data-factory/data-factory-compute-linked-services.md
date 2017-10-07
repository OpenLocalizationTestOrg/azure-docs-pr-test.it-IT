---
title: ambienti aaaCompute supportati da Data Factory di Azure | Documenti Microsoft
description: "Informazioni sugli ambienti di calcolo che è possibile utilizzare nei dati di processo o tootransform pipeline (ad esempio Azure HDInsight) Data Factory di Azure."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 6877a7e8-1a58-4cfb-bbd3-252ac72e4145
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 07/25/2017
ms.author: shlo
ms.openlocfilehash: aba7d7de695bc1c7d475f1e741ee3b3e884151c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="compute-environments-supported-by-azure-data-factory"></a>Ambienti di calcolo supportati da Azure Data Factory
Questo articolo illustra gli ambienti di calcolo diversi che è possibile utilizzare tooprocess o trasformare i dati. Fornisce inoltre informazioni dettagliate sulle diverse configurazioni (su richiesta e della modalità) supportati da Data Factory quando si configura servizi collegati collegamento questi calcolo ambienti tooan data factory di Azure.

Hello nella tabella seguente fornisce un elenco degli ambienti di elaborazione supportata dalle attività di Data Factory e hello che è possibile eseguire su di essi. 

| Ambiente di calcolo | attività |
| --- | --- |
| [Cluster HDInsight su richiesta](#azure-hdinsight-on-demand-linked-service) o [il proprio cluster HDInsight](#azure-hdinsight-linked-service) |[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [Hadoop Streaming](data-factory-hadoop-streaming-activity.md) |
| [Azure Batch](#azure-batch-linked-service) |[DotNet](data-factory-use-custom-activities.md) |
| [Azure Machine Learning](#azure-machine-learning-linked-service) |[Attività di Machine Learning: esecuzione batch e aggiornamento risorse](data-factory-azure-ml-batch-execution-activity.md) |
| [Azure Data Lake Analytics.](#azure-data-lake-analytics-linked-service) |[Attività U-SQL di Data Lake Analytics](data-factory-usql-activity.md) |
| [Azure SQL](#azure-sql-linked-service), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-linked-service), [SQL Server](#sql-server-linked-service) |[Stored procedure](data-factory-stored-proc-activity.md) |

## <a name="supported-hdinsight-versions-in-azure-data-factory"></a>Versioni supportate di HDInsight in Azure Data Factory
Azure HDInsight supporta più versioni cluster di Hadoop che possono essere distribuite in qualsiasi momento. Ogni opzione di versione viene creata una versione specifica di distribuzione di hello Hortonworks Data Platform (HDP) e un set di componenti contenuti all'interno di tale distribuzione. Microsoft tiene aggiornamento hello dell'elenco delle versioni supportate di HDInsight tooprovide Hadoop ecosistema di componenti più recenti e correzioni. Hello 3.2 di HDInsight è deprecato in 1 aprile 2017. Per altre dettagliate, vedere le [versioni di HDInsight supportate](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).

Ciò ha un impatto sulle versioni esistenti di Azure Data Factory che hanno attività in esecuzione nei cluster HDInsight 3.2. Si consiglia di linee guida di utenti toofollow hello nella seguente sezione tooupdate hello hello interessati Data Factory:

### <a name="for-linked-services-pointing-tooyour-own-hdinsight-clusters"></a>Per i servizi collegati che punta a un cluster di HDInsight tooyour
* **I servizi collegati HDInsight verso tooyour proprietari HDInsight 3.2 o di sotto di cluster:**

  Azure Data Factory supporta l'invio tooyour processi cluster HDInsight proprio da HDI 3.1 troppo[hello supportata più recente versione di HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions). Tuttavia, non è più creare cluster HDInsight 3.2 dopo il 1 aprile 2017 in base a criteri per deprecare hello documentati in [HDInsight versioni supportate](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).  

  **Consigli:** 
  * Eseguire test tooensure hello compatibilità di attività che fanno riferimento a questa servizi collegati troppo hello[hello supportata più recente versione di HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) con informazioni documentate in [disponibili con i componenti di Hadoop versioni diverse di HDInsight](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) e [Hortonworks note associato alle versioni HDInsight](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).
  * Aggiornare il cluster di HDInsight 3.2 troppo[hello supportata più recente versione di HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello componenti ecosistema di Hadoop e le correzioni più recenti. 

* **I servizi collegati HDInsight verso tooyour proprietari HDInsight 3.3 o versione successiva di cluster:**

  Azure Data Factory supporta l'invio tooyour processi cluster HDInsight proprio da HDI 3.1 troppo[hello supportata più recente versione di HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions). 
  
  **Consigli:** 
  * Non è necessaria alcuna azione dalla prospettiva di Data Factory. Tuttavia, se si utilizza una versione precedente di HDInsight, si consiglia comunque l'aggiornamento troppo[hello supportata più recente versione di HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello componenti ecosistema di Hadoop e le correzioni più recenti.

### <a name="for-hdinsight-on-demand-linked-services"></a>Per i servizi collegati HDInsight su richiesta
* **La versione 3.2 o precedente viene specificata nella definizione JSON dei servizi collegati HDInsight su richiesta:**
  
  Azure Data Factory supporterà la creazione di cluster HDInsight su richiesta della versione 3.3 o successiva a partire dal **15/05/2017**. E, alla fine di hello del supporto per esistente 3.2 di HDInsight su richiesta è troppo estesa dei servizi collegati**15/07/2017**.  

  **Consigli:** 
  * Eseguire test tooensure hello compatibilità di attività che fanno riferimento a questa servizi collegati troppo hello [hello supportata più recente versione di HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) con informazioni documentate in [disponibili con i componenti di Hadoop versioni diverse di HDInsight](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) e [Hortonworks note associato alle versioni HDInsight](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).
  * Prima di **15/07/2017**, aggiornare la proprietà di versione di hello nella definizione JSON di servizio su richiesta HDI collegato troppo[hello supportata più recente versione di HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello Hadoop ecosistema di componenti più recenti e correzioni. Per definizione JSON dettagliata, vedere toohello [esempio di servizio collegato di Azure HDInsight su richiesta](#azure-hdinsight-on-demand-linked-service). 

* **Versione non specificata nei servizi collegati HDInsight su richiesta:**
  
  Azure Data Factory supporterà la creazione di cluster HDInsight su richiesta della versione 3.3 o successiva a partire dal **15/05/2017**. E, fine hello del supporto tecnico clienti collegato 3.2 di HDInsight su richiesta tooexisting è troppo esteso.**15/07/2017**. 

  Prima di **15/07/2017**, se lasciato vuoto, per la versione è valori predefiniti di hello e osType proprietà sono: 

  | Proprietà | Default Value | Obbligatorio |
  | --- | --- | --- |
  Versione   | HDI 3.1 per cluster Windows e HDI 3.2 per cluster Linux.| No
  osType | valore predefinito di Hello è Windows | No

  Dopo aver **15/07/2017**, se lasciato vuoto, per la versione è valori predefiniti di hello e osType proprietà sono:

  | Proprietà | Default Value | Obbligatorio |
  | --- | --- | --- |
  Versione   | HDI 3.3 per cluster Windows e HDI 3.5 per cluster Linux.    | No
  osType | valore predefinito di Hello è Linux   | No

  **Consigli:** 
  * Prima di **15/07/2017**, eseguire test tooensure hello compatibilità di attività che fanno riferimento a questa servizi collegati troppo hello[hello supportata più recente versione di HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) con informazioni documentate in [Hadoop componenti disponibili con diverse versioni di HDInsight](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) e [Hortonworks note associato alle versioni HDInsight](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).  
  * Dopo aver **15/07/2017**, assicurarsi di specificare in modo esplicito i valori di versione e osType se si desidera che le impostazioni predefinite di toooverride hello. 

>[!Note]
>Azure Data Factory non supporta attualmente i cluster HDInsight con Azure Data Lake Store come archivio primario. È necessario usare Archiviazione di Azure come archivio primario per i cluster HDInsight. 
>  
>  

## <a name="on-demand-compute-environment"></a>Ambiente di calcolo “on-demand”
In questo tipo di configurazione, l'ambiente informatico hello è completamente gestiti dal servizio Azure Data Factory di hello. Viene automaticamente creata dal servizio Data Factory hello prima tooprocess inviato dati è un processo e rimosse quando viene completato il processo di hello. Si può creare un servizio collegato per l'ambiente di calcolo su richiesta hello, configurarlo e controllare le impostazioni del livello di granularità per l'esecuzione del processo, la gestione di cluster e l'avvio di azioni.

> [!NOTE]
> configurazione di Hello su richiesta è attualmente supportato solo per i cluster HDInsight di Azure.
> 
> 

## <a name="azure-hdinsight-on-demand-linked-service"></a>Servizio collegato Azure HDInsight su richiesta
Hello servizio Azure Data Factory può creare automaticamente un dati di tooprocess di basati su Windows o Linux su richiesta HDInsight cluster. Hello cluster viene creato nella stessa area dell'account di archiviazione hello (proprietà linkedServiceName in JSON hello) associata a cluster hello hello. account di archiviazione Hello deve essere un account di archiviazione di Azure standard utilizzo generale. 

Si noti segue hello **importante** punti su HDInsight su richiesta di servizio collegato:

* Hello su richiesta non viene visualizzato il cluster HDInsight creato nella sottoscrizione di Azure. Hello servizio Data Factory di Azure consente di gestire cluster HDInsight su richiesta di hello per conto dell'utente.
* Hello log per i processi eseguiti in un HDInsight su richiesta cluster vengono copiati toohello account di archiviazione associato al cluster HDInsight hello. È possibile accedere a questi log dal portale di Azure in hello hello **Dettagli esecuzione attività** blade. Per informazioni dettagliate, vedere l'articolo [Monitoraggio e gestione delle pipeline](data-factory-monitor-manage-pipelines.md) .
* Vengono addebitati solo i hello ora cluster HDInsight hello backup e i processi in esecuzione.

> [!IMPORTANT]
> In genere necessario **20 minuti** o altre tooprovision un Azure HDInsight su richiesta del cluster.
> 
> 

### <a name="example"></a>Esempio
Hello JSON seguente definisce un servizio di collegato di HDInsight su richiesta basati su Linux. Hello servizio Data Factory crea automaticamente un **basati su Linux** cluster HDInsight durante l'elaborazione di una sezione di dati. 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

impostare un cluster HDInsight basati su Windows, toouse **osType** troppo**windows** o non utilizzare proprietà hello come valore predefinito di hello: windows.  

> [!IMPORTANT]
> Crea cluster HDInsight Hello un **contenitore predefinito** nell'archiviazione blob hello specificato in JSON hello (**linkedServiceName**). HDInsight non eliminare questo contenitore quando viene eliminato il cluster hello. Questo comportamento dipende dalla progettazione. Con il servizio collegato di HDInsight su richiesta, un cluster HDInsight viene creato ogni volta che una sezione deve toobe elaborati a meno che non vi è un cluster esistente in tempo reale (**timeToLive**) e viene eliminata quando viene eseguita un'elaborazione hello. 
> 
> Man mano che vengono elaborate più sezioni, vengono visualizzati numerosi contenitori nell'archivio BLOB di Azure. Se non li necessario per la risoluzione dei problemi dei processi di hello, è opportuno toodelete li tooreduce hello il costo di archiviazione. i nomi di Hello di questi contenitori seguono un modello: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`. Utilizzare strumenti come [Esplora archivi Microsoft](http://storageexplorer.com/) toodelete contenitori di Azure nell'archiviazione blob.
> 
> 

### <a name="properties"></a>Proprietà
| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| type |proprietà tipo Hello deve essere impostato troppo**HDInsightOnDemand**. |Sì |
| clusterSize |Numero di nodi di lavoro o dati in cluster hello. cluster HDInsight Hello viene creato con 2 nodi head e il numero di hello di nodi di lavoro che è specificato per questa proprietà. nodi Hello sono di dimensioni Standard_D3 con 4 core, pertanto un cluster di nodi di 4 lavoro accetta 24 core (4\*4 = 16 core per i nodi di lavoro, più 2\*4 = 8 core per i nodi head). Vedere [cluster basati su Linux creare Hadoop in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) per informazioni dettagliate su livello hello Standard_D3. |Sì |
| timeToLive |Hello consentito tempo di inattività per il cluster HDInsight su richiesta di hello. Specifica quanto tempo rimarrà attivo cluster HDInsight su richiesta di hello dopo il completamento di un'attività eseguita se non sono disponibili altri processi attivi cluster hello.<br/><br/>Ad esempio, se un'attività eseguita richiede 6 minuti e la proprietà timetolive è impostato too5 minuti, hello cluster rimane attivo per 5 minuti dopo hello 6 minuti di elaborazione di esecuzione dell'attività hello. Se l'esecuzione di un'altra attività viene eseguita con finestra 6 minuti hello, che viene elaborato dalla hello dello stesso cluster.<br/><br/>Creazione di un cluster di HDInsight su richiesta è un'operazione dispendiosa (potrebbe richiedere un po' di tempo), quindi utilizzare questa impostazione prestazioni tooimprove necessari per una data factory riutilizzando un cluster di HDInsight su richiesta.<br/><br/>Se si imposta la proprietà timetolive valore too0, cluster hello viene eliminato, non appena viene completata l'esecuzione dell'attività hello. Considerando che, se si imposta un valore elevato, cluster hello può rimanere inattivo inutilmente risultante in costi elevati. Pertanto, è importante impostare hello di valore appropriato in base alle proprie esigenze.<br/><br/>Se è impostato in modo appropriato i valore della proprietà timetolive hello, più pipeline possono condividere istanza hello del cluster HDInsight su richiesta di hello.  |Sì |
| version |Versione del cluster HDInsight hello. valore predefinito di Hello è 3.1 per cluster di Windows e 3.2 per cluster Linux. |No |
| linkedServiceName | Servizio collegato di archiviazione Azure: toobe utilizzato dal cluster di hello su richiesta per l'archiviazione e l'elaborazione dei dati. Hello cluster HDInsight viene creato in hello stessa area come questo account di archiviazione di Azure.<p>Attualmente, è possibile creare un cluster HDInsight su richiesta che utilizza un archivio Azure Data Lake come archiviazione hello. Se si desiderano dati del risultato hello toostore dal HDInsight l'elaborazione in un archivio Azure Data Lake, utilizzare un attività di copia toocopy hello dati dall'archiviazione Blob di Azure di hello toohello archivio Azure Data Lake. </p>  | Sì |
| additionalLinkedServiceNames |Specifica l'account di archiviazione aggiuntivi per hello HDInsight servizio collegato in modo che il servizio di Data Factory hello può registrare per conto dell'utente. Questi account di archiviazione devono essere in hello stessa area cluster HDInsight hello, che viene creato in hello stessa regione dell'account di archiviazione hello specificato da linkedServiceName. |No |
| osType |Tipo di sistema operativo. I valori consentiti sono: Windows (impostazione predefinita) e Linux |No |
| hcatalogLinkedServiceName |nome Hello del collegato SQL Azure database HCatalog toohello punto del servizio. cluster di HDInsight su richiesta Hello viene creato utilizzando il database di SQL Azure hello come metastore hello. |No |

#### <a name="additionallinkedservicenames-json-example"></a>Esempio di codice JSON additionalLinkedServiceNames

```json
"additionalLinkedServiceNames": [
    "otherLinkedServiceName1",
    "otherLinkedServiceName2"
  ]
```

### <a name="advanced-properties"></a>Advanced Properties
È inoltre possibile specificare le proprietà seguenti per configurazione granulare di hello del cluster HDInsight su richiesta di hello hello.

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| coreConfiguration |Specifica i parametri di configurazione principali hello (come in core-Site.XML) per hello HDInsight cluster toobe creato. |No |
| hBaseConfiguration |Specifica hello parametri di configurazione HBase (hbase-Site.XML) per il cluster HDInsight hello. |No |
| hdfsConfiguration |Specifica hello parametri di configurazione HDFS (hdfs-Site.XML) per il cluster HDInsight hello. |No |
| hiveConfiguration |Specifica hello parametri di configurazione hive (hive-Site.XML) per il cluster HDInsight hello. |No |
| mapReduceConfiguration |Specifica hello parametri di configurazione MapReduce (mapred-Site.XML) per il cluster HDInsight hello. |No |
| oozieConfiguration |Specifica hello parametri di configurazione Oozie (oozie-Site.XML) per il cluster HDInsight hello. |No |
| stormConfiguration |Specifica hello parametri di configurazione Storm (Storm-Site.XML) per il cluster HDInsight hello. |No |
| yarnConfiguration |Specifica hello parametri di configurazione Yarn (yarn-Site.XML) per il cluster HDInsight hello. |No |

#### <a name="example--on-demand-hdinsight-cluster-configuration-with-advanced-properties"></a>Esempio: configurazione del cluster HDInsight su richiesta con le proprietà avanzate

```json
{
  "name": " HDInsightOnDemandLinkedService",
  "properties": {
    "type": "HDInsightOnDemand",
    "typeProperties": {
      "clusterSize": 16,
      "timeToLive": "01:30:00",
      "linkedServiceName": "adfods1",
      "coreConfiguration": {
        "templeton.mapper.memory.mb": "5000"
      },
      "hiveConfiguration": {
        "templeton.mapper.memory.mb": "5000"
      },
      "mapReduceConfiguration": {
        "mapreduce.reduce.java.opts": "-Xmx4000m",
        "mapreduce.map.java.opts": "-Xmx4000m",
        "mapreduce.map.memory.mb": "5000",
        "mapreduce.reduce.memory.mb": "5000",
        "mapreduce.job.reduce.slowstart.completedmaps": "0.8"
      },
      "yarnConfiguration": {
        "yarn.app.mapreduce.am.resource.mb": "5000",
        "mapreduce.map.memory.mb": "5000"
      },
      "additionalLinkedServiceNames": [
        "datafeeds",
        "adobedatafeed"
      ]
    }
  }
}
```

### <a name="node-sizes"></a>Dimensioni dei nodi
È possibile specificare le dimensioni di hello dei nodi head, i dati e zookeeper utilizzando hello le proprietà seguenti: 

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| headNodeSize |Specifica dimensioni hello del nodo head hello. valore predefinito di Hello è: Standard_D3. Vedere hello **specificare le dimensioni dei nodi** sezione per informazioni dettagliate. |No |
| dataNodeSize |Specifica dimensioni hello del nodo di dati hello. valore predefinito di Hello è: Standard_D3. |No |
| zookeeperNodeSize |Specifica dimensioni hello del nodo di zoo hello. valore predefinito di Hello è: Standard_D3. |No |

#### <a name="specifying-node-sizes"></a>Specificare le dimensioni dei nodi
Vedere hello [le dimensioni delle macchine virtuali](../virtual-machines/linux/sizes.md) articolo per i valori stringa, è necessario toospecify per proprietà hello indicate nella sezione precedente hello. i valori di Hello devono tooconform toohello **cmdlet & API** a cui fa riferimento nell'articolo hello. Come si può notare nell'articolo hello, nodo dati hello (impostazione predefinita) di grandi dimensioni è 7 GB di memoria, che potrebbe non essere adeguata per il proprio scenario. 

Se si desidera toocreate D4 dimensioni nodi head e lavoro, specificare **Standard_D4** come valore di hello per le proprietà headNodeSize e dataNodeSize. 

```json
"headNodeSize": "Standard_D4",    
"dataNodeSize": "Standard_D4",
```

Se si specifica un valore errato per queste proprietà, si potrebbe ricevere seguente hello **errore:** cluster toocreate non riuscito. Eccezione: L'operazione di creazione cluster di hello toocomplete non è possibile. L'operazione non è riuscita con codice '400'. Nello stato del cluster è apparso il messaggio 'Errore'. Messaggio: ’PreClusterCreationValidationFailure’. Quando si riceve questo errore, verificare che si sta utilizzando hello **CMDLET & API** nome tabella hello hello [le dimensioni delle macchine virtuali](../virtual-machines/linux/sizes.md) articolo.  

## <a name="bring-your-own-compute-environment"></a>Ambiente di calcolo “bring your own”
In questo tipo di configurazione, gli utenti possono registrare un ambiente informatico già esistente come servizio collegato in Data Factory. ambiente di elaborazione Hello è gestito da utente hello e hello servizio Data Factory utilizza le attività di hello tooexecute.

Questo tipo di configurazione è supportato per gli ambienti di calcolo seguente hello:

* HDInsight di Azure
* Azure Batch
* Azure Machine Learning
* Azure Data Lake Analytics.
* Azure SQL DB, Azure SQL DW e SQL Server

## <a name="azure-hdinsight-linked-service"></a>Servizio collegato Azure HDInsight
È possibile creare cluster HDInsight un tooregister di servizio collegato di HDInsight di Azure con Data Factory.

### <a name="example"></a>Esempio

```json
{
  "name": "HDInsightLinkedService",
  "properties": {
    "type": "HDInsight",
    "typeProperties": {
      "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
      "userName": "admin",
      "password": "<password>",
      "linkedServiceName": "MyHDInsightStoragelinkedService"
    }
  }
}
```

### <a name="properties"></a>Proprietà
| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| type |proprietà tipo Hello deve essere impostato troppo**HDInsight**. |Sì |
| clusterUri |URI del cluster HDInsight hello Hello. |Sì |
| username |Specificare nome hello di hello utente toobe utilizzata cluster di HDInsight tooconnect tooan esistente. |Sì |
| password |Specificare la password per l'account utente di hello. |Sì |
| linkedServiceName | Nome di servizio collegato di archiviazione di Azure che fa riferimento nell'archiviazione blob di Azure toohello hello utilizzato da hello cluster HDInsight. <p>Attualmente non è possibile specificare un servizio collegato di Azure Data Lake Store per questa proprietà. Se il cluster di HDInsight hello dispone di accesso toohello archivio Data Lake, è possibile accedere ai dati hello archivio Azure Data Lake dagli script Hive o Pig. </p>  |Sì |

## <a name="azure-batch-linked-service"></a>Servizio collegato Azure Batch
È possibile creare un tooregister di servizio collegato di Azure Batch con un pool di Batch di macchine virtuali (VM) tooa data factory. È possibile eseguire le attività .NET personalizzate utilizzando Batch Azure o Azure HDInsight.

Vedere i seguenti argomenti in caso di nuovo servizio di Batch tooAzure:

* [Nozioni di base di Azure Batch](../batch/batch-technical-overview.md) per una panoramica del servizio Azure Batch hello.
* [Nuovo AzureBatchAccount](https://msdn.microsoft.com/library/mt125880.aspx) toocreate cmdlet un account Azure Batch (o) [portale di Azure](../batch/batch-account-create-portal.md) account di Azure Batch hello toocreate tramite il portale di Azure. Vedere [toomanage PowerShell utilizzando Account di Azure Batch](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx) argomento per istruzioni dettagliate sull'utilizzo di cmdlet hello.
* [Nuovo AzureBatchPool](https://msdn.microsoft.com/library/mt125936.aspx) toocreate cmdlet un pool di Batch di Azure.

### <a name="example"></a>Esempio

```json
{
  "name": "AzureBatchLinkedService",
  "properties": {
    "type": "AzureBatch",
    "typeProperties": {
      "accountName": "<Azure Batch account name>",
      "accessKey": "<Azure Batch account key>",
      "poolName": "<Azure Batch pool name>",
      "linkedServiceName": "<Specify associated storage linked service reference here>"
    }
  }
}
```

Aggiungere "**.\< nome dell'area\>**"toohello nome dell'account di batch per hello **accountName** proprietà. Esempio:

```json
"accountName": "mybatchaccount.eastus"
```

Un'altra opzione è l'endpoint di batchUri hello tooprovide come illustrato nel seguente esempio hello:

```json
"accountName": "adfteam",
"batchUri": "https://eastus.batch.azure.com",
```

### <a name="properties"></a>Proprietà
| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| type |proprietà tipo Hello deve essere impostato troppo**AzureBatch**. |Sì |
| accountName |Nome dell'account Azure Batch hello. |Sì |
| accessKey |Chiave di accesso per account Azure Batch hello. |Sì |
| poolName |Nome del pool di hello delle macchine virtuali. |Sì |
| linkedServiceName |Nome del servizio collegato di archiviazione di Azure associato a questo servizio collegato di Azure Batch hello. Questo servizio collegato viene utilizzato per i file di gestione temporanea attività hello toorun e l'archiviazione dei log di esecuzione di attività hello obbligatori. |Sì |

## <a name="azure-machine-learning-linked-service"></a>Servizio collegato di Azure Machine Learning
Creare un tooregister di servizio collegato di Azure Machine Learning punteggio tooa data factory di endpoint di un batch di Machine Learning.

### <a name="example"></a>Esempio

```json
{
  "name": "AzureMLLinkedService",
  "properties": {
    "type": "AzureML",
    "typeProperties": {
      "mlEndpoint": "https://[batch scoring endpoint]/jobs",
      "apiKey": "<apikey>"
    }
  }
}
```

### <a name="properties"></a>Proprietà
| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| Tipo |proprietà di tipo Hello deve essere impostata su: **Azure ml**. |Sì |
| mlEndpoint |URL di punteggio batch di Hello. |Sì |
| apiKey |Hello pubblicati API del modello di area di lavoro. |Sì |

## <a name="azure-data-lake-analytics-linked-service"></a>Servizio collegato di Azure Data Lake Analytics
Si crea un **Azure Data Lake Analitica** collegato servizio toolink una factory di dati di Azure tooan del servizio di calcolo di Azure Data Lake Analitica. attività Data Lake Analitica U-SQL nella pipeline hello Hello fa riferimento a servizio toothis collegato. 

Hello nella tabella seguente vengono fornite descrizioni per hello generica proprietà utilizzate nella definizione JSON hello. È possibile scegliere anche tra l'autenticazione basata sull'entità servizio e l'autenticazione basata sulle credenziali utente.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| **type** |proprietà di tipo Hello deve essere impostata su: **AzureDataLakeAnalytics**. |Sì |
| **accountName** |Nome dell'account di Azure Data Lake Analytics. |Sì |
| **dataLakeAnalyticsUri** |URI di Azure Data Lake Analytics. |No |
| **subscriptionId** |ID sottoscrizione di Azure |No (se non specificato, sottoscrizione di hello viene utilizzata una data factory). |
| **resourceGroupName** |Nome del gruppo di risorse di Azure |No (se non specificato, il gruppo di risorse di hello viene utilizzata una data factory). |

### <a name="service-principal-authentication-recommended"></a>Autenticazione basata su entità servizio (opzione consigliata)
toouse l'autenticazione dell'entità servizio, registrare un'entità di applicazione in Azure Active Directory (Azure AD) e concedere hello accedere all'archivio Lake tooData. Per la procedura dettaglia, vedere [Autenticazione da servizio a servizio](../data-lake-store/data-lake-store-authenticate-using-active-directory.md). Prendere nota dei seguenti valori, che permette di hello hello toodefine servizio collegato:
* ID applicazione
* Chiave applicazione 
* ID tenant

Utilizzare l'autenticazione dell'entità servizio specificando hello le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| **servicePrincipalId** | Specificare un ID client. dell'applicazione hello | Sì |
| **servicePrincipalKey** | Specificare la chiave dell'applicazione hello. | Sì |
| **tenant** | Specificare le informazioni di hello tenant (dominio tenant o nome ID) in cui risiede l'applicazione. È possibile recuperarlo dal passaggio del mouse hello nell'angolo superiore destro di hello di hello portale di Azure. | Sì |

**Esempio: autenticazione basata su entità servizio**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Autenticazione basata su credenziali utente
In alternativa, è possibile utilizzare l'autenticazione delle credenziali utente per Data Lake Analitica specificando hello le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| **authorization** | Fare clic su hello **Authorize** pulsante hello Editor delle Data Factory e immettere le credenziali dell'utente che assegna la proprietà toothis hello generato automaticamente autorizzazione URL. | Sì |
| **sessionId** | ID di sessione OAuth della sessione di autorizzazione OAuth hello. Ogni ID di sessione è univoco e può essere usato solo una volta. Questa impostazione viene generata automaticamente quando si utilizza hello Editor delle Data Factory. | Sì |

**Esempio: autenticazione basata su credenziali utente**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a>Scadenza del token
codice di autorizzazione è stato generato utilizzando hello Hello **Authorize** pulsante scade dopo qualche minuto. Vedere hello nella tabella seguente per date di scadenza hello per diversi tipi di account utente. Si può vedere hello seguente messaggio di errore hello quando l'autenticazione **scadenza del token**: errore nell'operazione di credenziali: invalid_grant - AADSTS70002: errore di convalida delle credenziali. AADSTS70008: hello fornito concessione di accesso è scaduto o revocato. ID traccia: d18629e8-af88-43c5-88e3-d8419eb1fca1 ID correlazione: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z.

| Tipo di utente | Scade dopo |
|:--- |:--- |
| Account utente NON gestiti da Azure Active Directory (@hotmail.com, @live.com e così via). |12 ore |
| Account utente gestiti da Azure Active Directory (AAD) |eseguire 14 giorni dopo l'ultima sezione di hello. <br/><br/>90 giorni, se viene eseguita una sezione basata sul servizio collegato OAuth almeno una volta ogni 14 giorni. |

tooavoid e risolvere questo errore, riautorizzare utilizzando hello **Authorize** pulsante quando hello **scadenza del token** e ridistribuire il servizio collegato hello. È anche possibile generare valori per le proprietà **sessionId** e **authorization** a livello di codice usando il codice seguente:

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

Vedere [AzureDataLakeStoreLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), e [AuthorizationSessionGetResponse classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) argomenti per informazioni dettagliate informazioni sulle classi di Data Factory hello usate nel codice hello. Aggiungere un riferimento a: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll per hello WindowsFormsWebAuthenticationDialog classe. 

## <a name="azure-sql-linked-service"></a>Servizio collegato di Azure SQL
È possibile creare un servizio collegato SQL Azure e usarlo con hello [attività Stored Procedure](data-factory-stored-proc-activity.md) tooinvoke una stored procedure da una pipeline di Data Factory. Vedere l’articolo [Connettore di Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties) per informazioni dettagliate su questo servizio collegato.

## <a name="azure-sql-data-warehouse-linked-service"></a>Servizio collegato di Azure SQL Data Warehouse
È possibile creare un servizio collegato di Azure SQL Data Warehouse e usarlo con hello [attività Stored Procedure](data-factory-stored-proc-activity.md) tooinvoke una stored procedure da una pipeline di Data Factory. Vedere l'articolo [Proprietà del servizio collegato di Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) per informazioni dettagliate su questo servizio collegato.

## <a name="sql-server-linked-service"></a>Servizio collegato di SQL Server
Creare un servizio collegato SQL Server e usarlo con hello [attività Stored Procedure](data-factory-stored-proc-activity.md) tooinvoke una stored procedure da una pipeline di Data Factory. Vedere l'articolo [Proprietà del servizio collegato SQL Server](data-factory-sqlserver-connector.md#linked-service-properties) per informazioni dettagliate su questo servizio collegato.

