---
title: gli scenari di aaaData che l'archivio Data Lake | Documenti Microsoft
description: Comprendere hello diversi scenari e strumenti con i dati possono caricamento, elaborata, scaricato e visualizzato in un archivio Data Lake
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 37409a71-a563-4bb7-bc46-2cbd426a2ece
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: caaa3979b8a2532089778c3e3db3c711714d3c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-data-lake-store-for-big-data-requirements"></a>Uso di Archivio Data Lake di Azure per requisiti Big Data
L'elaborazione di Big Data prevede quattro fasi principali:

* Inserimento di grandi quantità di dati in un archivio dati, in tempo reale o in batch
* L'elaborazione dei dati hello
* Download dei dati di hello
* Visualizzazione dei dati hello

In questo articolo verranno esaminate queste fasi con riguardo tooAzure archivio Data Lake toounderstand hello opzioni e gli strumenti disponibili toomeet le esigenze di dati.

## <a name="ingest-data-into-data-lake-store"></a>Inserire i dati in Archivio Data Lake
In questa sezione evidenzia hello diverse origini dati e hello diversi modi in cui è possano caricamento dati in un account archivio Data Lake.

![Inserire i dati in Data Lake Store](./media/data-lake-store-data-scenarios/ingest-data.png "Inserire i dati in Data Lake Store")

### <a name="ad-hoc-data"></a>Dati ad hoc
Si tratta di set di dati di piccole dimensioni usati per la creazione del prototipo di un'applicazione Big Data. Esistono diversi metodi per l'inserimento di dati ad hoc a seconda origine hello hello dati.

| origine dati | Inserire usando |
| --- | --- |
| Computer locale |<ul> <li>[Portale di Azure](/data-lake-store-get-started-portal.md)</li> <li>[Azure PowerShell](data-lake-store-get-started-powershell.md)</li> <li>[Interfaccia della riga di comando multipiattaforma di Azure 2.0](data-lake-store-get-started-cli-2.0.md)</li> <li>[Usare Strumenti di Data Lake per Visual Studio](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md) </li></ul> |
| BLOB di Archiviazione di Azure |<ul> <li>[Data factory di Azure](../data-factory/data-factory-azure-datalake-connector.md)</li> <li>[strumento AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)</li><li>[DistCp in esecuzione nel cluster HDInsight](data-lake-store-copy-data-wasb-distcp.md)</li> </ul> |

### <a name="streamed-data"></a>Dati di streaming
Si tratta dei dati che possono essere generati da origini diverse, ad esempio applicazioni, dispositivi, sensori, ecc. Questi dati possono essere inseriti in un Archivio Data Lake tramite strumenti diversi. Questi strumenti vengano in genere acquisire ed elaborare dati hello un singolo evento per evento in tempo reale e quindi scrivere gli eventi di hello in batch in archivio Data Lake in modo che possono essere elaborati ulteriormente.

Di seguito sono elencati gli strumenti che è possibile usare:

* [Azure Analitica flusso](../stream-analytics/stream-analytics-data-lake-output.md) -eventi di caricamento hub di eventi possono essere scritte tooAzure Data Lake con un archivio Azure Data Lake di output.
* [Azure HDInsight Storm](../hdinsight/hdinsight-storm-write-data-lake-store.md) -è possibile scrivere i dati direttamente tooData Lake archivio da hello cluster Storm.
* [EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md) : È possibile ricevere eventi dall'hub eventi e scriverli tooData Lake archivio utilizzando hello [Data Lake archivio .NET SDK](data-lake-store-get-started-net-sdk.md).

### <a name="relational-data"></a>Dati relazionali
È inoltre possibile recuperare i dati dai database relazionali. I database relazionali raccolgono nel tempo elevate quantità di dati che possono fornire informazioni significative se elaborate tramite una pipeline Big Data. È possibile utilizzare tali dati hello seguenti strumenti toomove in archivio Data Lake.

* [Apache Sqoop](data-lake-store-data-transfer-sql-sqoop.md)
* [Data factory di Azure](../data-factory/data-factory-data-movement-activities.md)

### <a name="web-server-log-data-upload-using-custom-applications"></a>Dati di log del server Web (caricamento tramite applicazioni personalizzate)
Questo tipo di set di dati è indicato in modo specifico perché l'analisi dei dati di log del server web è un caso di utilizzo comune per le applicazioni di dati e richiede grandi volumi di log file toobe caricato archivio toohello Data Lake. È possibile utilizzare uno qualsiasi dei seguenti strumenti toowrite hello tooupload proprie applicazioni o script tali dati.

* [Interfaccia della riga di comando multipiattaforma di Azure 2.0](data-lake-store-get-started-cli-2.0.md)
* [Azure PowerShell](data-lake-store-get-started-powershell.md)
* [.NET SDK di Archivio Azure Data Lake](data-lake-store-get-started-net-sdk.md)
* [Data factory di Azure](../data-factory/data-factory-data-movement-activities.md)

Per il caricamento dei dati di log del server web e per il caricamento di altri tipi di dati (ad esempio, i rispettivi social), è un buon approccio toowrite script/applicazioni personalizzate poiché consente di hello flessibilità tooinclude componente come parte di caricamento dati dell'applicazione di dati più grande. In alcuni casi, questo codice potrebbe richiedere modulo hello di uno script o utilità della riga di comando semplice. In altri casi, il codice di hello può essere utilizzato toointegrate elaborazione di big data in un'applicazione di business o una soluzione.

### <a name="data-associated-with-azure-hdinsight-clusters"></a>Dati associati ai cluster Azure HDInsight
La maggior parte dei tipi di cluster HDInsight (Hadoop, HBase, Storm) supportano Archivio Data Lake come repository di archiviazione dei dati. I cluster HDInsight accedono ai dati dai BLOB di archiviazione di Azure (WASB). Per ottenere prestazioni migliori, è possibile copiare dati hello da WASB in un account archivio Data Lake associato hello cluster. È possibile utilizzare hello strumenti toocopy hello dati seguenti.

* [Apache DistCp](data-lake-store-copy-data-wasb-distcp.md)
* [Servizio AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
* [Data factory di Azure](../data-factory/data-factory-azure-datalake-connector.md)

### <a name="data-stored-in-on-premises-or-iaas-hadoop-clusters"></a>Dati archiviati in locale o in cluster IaaS Hadoop
Grandi quantità di dati possono essere archiviati in cluster Hadoop esistenti, localmente, nei computer che usano HDFS. cluster Hadoop Hello potrebbero trovarsi in una distribuzione locale o può essere all'interno di un cluster IaaS in Azure. Può avere requisiti toocopy tooAzure tali dati archivio Data Lake per un approccio One-Off o in modo ricorrente. Sono disponibili varie opzioni che è possibile utilizzare tooachieve questo. Di seguito è riportato un elenco di alternative e hello associati vantaggi e svantaggi.

| Approccio | Dettagli | Vantaggi | Considerazioni |
| --- | --- | --- | --- |
| Utilizzare i dati di Azure Data Factory (ADF) toocopy direttamente dall'archivio di Hadoop cluster tooAzure Data Lake |[ADF supporta HDFS come origine dati](../data-factory/data-factory-hdfs-connector.md) |ADF fornisce il supporto nativo per HDFS e il monitoraggio e gestione end-to-end di prima classe |Richiede toobe Gateway di gestione dati distribuiti in locale o in cluster IaaS hello |
| Esportare dati da Hadoop come file. Quindi copia hello file tooAzure archivio Data Lake tramite il meccanismo appropriato. |È possibile copiare i file tooAzure archivio Data Lake mediante: <ul><li>[Azure PowerShell per sistema operativo Windows](data-lake-store-get-started-powershell.md)</li><li>[Interfaccia della riga di comando multipiattaforma di Azure 2.0 per sistemi operativi non Windows](data-lake-store-get-started-cli-2.0.md)</li><li>Applicazione personalizzata che usa qualsiasi SDK di Data Lake Store</li></ul> |Avvio rapido tooget. È possibile eseguire caricamenti personalizzati |Processo in più passaggi che prevede più tecnologie. Gestione e monitoraggio aumenterà toobe una richiesta di verifica tramite strumenti hello natura hello personalizzato ora specificate |
| Utilizzare dati toocopy Distcp Hadoop tooAzure archiviazione. Copiare quindi i dati dall'archivio Lake tooData archiviazione di Azure utilizzando il meccanismo appropriato. |È possibile copiare dati da un archivio Azure Storage tooData Lake tramite: <ul><li>[Data factory di Azure](../data-factory/data-factory-data-movement-activities.md)</li><li>[strumento AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)</li><li>[DistCp Apache in esecuzione nei cluster HDInsight](data-lake-store-copy-data-wasb-distcp.md)</li></ul> |È possibile usare strumenti open source. |Processo in più passaggi che prevede più tecnologie |

### <a name="really-large-datasets"></a>Set di dati di grandi dimensioni
Per il caricamento dei set di dati in un intervallo più terabyte, usando metodi hello descritti in precedenza può talvolta essere lenta e dispendiosa. In questi casi, è possibile utilizzare le opzioni di hello riportate di seguito.

* **Uso di Azure ExpressRoute**. Azure ExpressRoute consente di creare connessioni private tra i data center di Azure e l'infrastruttura locale. Ciò offre un'opzione affidabile per il trasferimento di grandi quantità di dati. Per altre informazioni, vedere la [Documentazione su ExpressRoute](../expressroute/expressroute-introduction.md).
* **Caricamento "offline" dei dati**. Se l'uso di Azure ExpressRoute non è fattibile per qualsiasi motivo, è possibile utilizzare [servizio di importazione/esportazione di Azure](../storage/common/storage-import-export-service.md) tooship unità disco con i dati tooan data center di Azure. I dati vengono prima caricato tooAzure archiviazione BLOB. È quindi possibile utilizzare [Data Factory di Azure](../data-factory/data-factory-azure-datalake-connector.md) o [AdlCopy strumento](data-lake-store-copy-data-azure-storage-blob.md) toocopy dati da un archivio Azure archiviazione BLOB tooData Lake.

  > [!NOTE]
  > Mentre tramite hello servizio importazione/esportazione, delle dimensioni del file hello in hello dischi che si effettua la spedizione tooAzure data center non devono essere maggiore di 195 GB.
  >
  >

## <a name="process-data-stored-in-data-lake-store"></a>Elaborare i dati archiviati in Archivio Data Lake
Una volta hello dati sono disponibili in archivio Data Lake è possibile eseguire analisi che i dati utilizzando hello supportati applicazioni big data. Attualmente, è possibile utilizzare i processi di analisi dati toorun HDInsight di Azure e Azure Data Lake Analitica dati hello archiviati in archivio Data Lake.

![Analizzare i dati in Data Lake Store](./media/data-lake-store-data-scenarios/analyze-data.png "Analizzare i dati in Data Lake Store")

È possibile esaminare hello seguono esempi.

* [Creare un cluster HDInsight con Archivio Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Usare Azure Data Lake Analytics con Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

## <a name="download-data-from-data-lake-store"></a>Scaricare i dati da Archivio Data Lake
È anche possibile desidera toodownload o spostare i dati dall'archivio Azure Data Lake per gli scenari, ad esempio:

* Spostare dati tooother repository toointerface con le pipeline di elaborazione dei dati esistente. Ad esempio, si potrebbe essere necessario toomove dati dall'archivio Data Lake tooAzure Database SQL o SQL Server locale.
* Scaricare computer locale tooyour di dati per l'elaborazione in ambienti IDE durante la creazione di prototipi di applicazioni.

![Estrarre i dati da Data Lake Store](./media/data-lake-store-data-scenarios/egress-data.png "Estrarre i dati da Data Lake Store")

In questi casi, è possibile utilizzare uno qualsiasi dei hello le opzioni seguenti:

* [Apache Sqoop](data-lake-store-data-transfer-sql-sqoop.md)
* [Data factory di Azure](../data-factory/data-factory-data-movement-activities.md)
* [Apache DistCp](data-lake-store-copy-data-wasb-distcp.md)

Consente inoltre hello seguenti metodi toowrite dati toodownload/applicazione di script da un archivio Data Lake.

* [Interfaccia della riga di comando multipiattaforma di Azure 2.0](data-lake-store-get-started-cli-2.0.md)
* [Azure PowerShell](data-lake-store-get-started-powershell.md)
* [.NET SDK di Archivio Azure Data Lake](data-lake-store-get-started-net-sdk.md)

## <a name="visualize-data-in-data-lake-store"></a>Visualizzare i dati in Archivio Data Lake
È possibile utilizzare una combinazione di rappresentazioni visive toocreate di servizi di dati archiviati nell'archivio Data Lake.

![Visualizzare i dati in Data Lake Store](./media/data-lake-store-data-scenarios/visualize-data.png "Visualizzare i dati in Data Lake Store")

* È possibile avviare utilizzando [dati toomove Data Factory di Azure dall'archivio Data Lake tooAzure SQL Data Warehouse](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats)
* Successivamente, è possibile [Power BI viene integrato con Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-integrate-power-bi.md) toocreate rappresentazione visiva dei dati di hello.
