---
title: Archivio Data Lake con altri servizi Azure aaaIntegrating | Documenti Microsoft
description: "Informazioni sulle modalità di integrazione di Data Lake Store con altri servizi di Azure"
documentationcenter: 
services: data-lake-store
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 48a5d1f4-3850-4c22-bbc4-6d1d394fba8a
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 839689f04623f8225884e7aa9c0b533a09323e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-data-lake-store-with-other-azure-services"></a>Integrazione di Data Lake Store con altri servizi di Azure
Archivio Azure Data Lake può essere utilizzato in combinazione con altri tooenable di servizi di Azure una vasta gamma di scenari. Hello articolo seguente elenca i servizi di hello che può essere integrato con archivio Data Lake.

## <a name="use-data-lake-store-with-azure-hdinsight"></a>Usare Archivio Data Lake con Azure HDInsight
È possibile fornire un [Azure HDInsight](https://azure.microsoft.com/documentation/learning-paths/hdinsight-self-guided-hadoop-training/) cluster che utilizza l'archivio Data Lake come archiviazione hello conformi a HDFS. Per questa versione, per i cluster Hadoop e Storm in Windows e Linux è possibile usare Data Lake Store solo come un'ulteriore risorsa di archiviazione. Tali cluster comunque usare l'archiviazione di Azure (WASB) come spazio di archiviazione predefinito hello. Tuttavia, per i cluster HBase in Windows e Linux, è possibile utilizzare archivio Data Lake come spazio di archiviazione predefinito hello, o di ulteriore spazio di archiviazione o di entrambi.

Per istruzioni su come tooprovision un HDInsight cluster con archivio Data Lake, vedere:

* [Effettuare il provisioning di un cluster HDInsight con Archivio Data Lake tramite il portale di Azure](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Eseguire il provisioning di un cluster HDInsight con Data Lake Store come archivio predefinito mediante Azure PowerShell](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [Eseguire il provisioning di un cluster HDInsight con Data Lake Store come archivio aggiuntivo mediante Azure PowerShell](data-lake-store-hdinsight-hadoop-use-powershell.md)

## <a name="use-data-lake-store-with-azure-data-lake-analytics"></a>Usare Archivio Data Lake con Analisi Data Lake di Azure
[Azure Data Lake Analitica](../data-lake-analytics/data-lake-analytics-overview.md) consente toowork dati di grandi dimensioni a livello di cloud. Il servizio effettua il provisioning dinamico delle risorse e permette di svolgere analisi su terabyte e addirittura exabyte di dati che possono essere archiviati nelle numerose origini dati supportate, ad esempio Data Lake Store. Data Lake Analitica è appositamente ottimizzato toowork con archivio Azure Data Lake - fornendo hello massimo livello di prestazioni, velocità effettiva e la parallelizzazione automaticamente i carichi di lavoro di big data.

Per istruzioni su come toouse Data Lake Analitica con archivio Data Lake, vedere [Introduzione a Data Lake Analitica con archivio Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md).

## <a name="use-data-lake-store-with-azure-data-factory"></a>Usare Archivio Data Lake con Data factory di Azure
È possibile utilizzare [Data Factory di Azure](https://azure.microsoft.com/services/data-factory/) tooingest dati da tabelle di Azure, Database SQL di Azure, Azure SQL data warehouse, il BLOB di archiviazione di Azure e database locali. La prima classe cittadinanza in hello ecosistema di Azure, Azure Data Factory può essere utilizzato tooorchestrate hello inserimento di dati da questi tooAzure origine archivio Data Lake.

Per istruzioni su come toouse Data Factory di Azure con archivio Data Lake, vedere [spostare tooand dati dall'archivio Data Lake con Data Factory](../data-factory/data-factory-azure-datalake-connector.md).

## <a name="copy-data-from-azure-storage-blobs-into-data-lake-store"></a>Copiare i dati da BLOB di Archiviazione di Azure ad Archivio Data Lake
Archivio Azure Data Lake offre uno strumento da riga di comando, AdlCopy, che consente di toocopy dati dall'archiviazione Blob di Azure in un account archivio Data Lake. Per ulteriori informazioni, vedere [copiare i dati da un archivio Azure archiviazione BLOB tooData Lake](data-lake-store-copy-data-azure-storage-blob.md).

## <a name="copy-data-between-azure-sql-database-and-data-lake-store"></a>Copiare i dati dal database SQL di Azure nell'Archivio Data Lake
È possibile utilizzare Apache Sqoop tooimport ed esportare dati tra Database SQL di Azure e archivio Data Lake. Per altre informazioni, vedere [Copiare i dati tra Archivio Data Lake e un database SQL di Azure usando Sqoop](data-lake-store-data-transfer-sql-sqoop.md).

## <a name="use-data-lake-store-with-stream-analytics"></a>Uso di Archivio Data Lake con l'analisi di flusso
È possibile utilizzare l'archivio Data Lake come uno dei hello restituisce toostore dati trasmessi tramite Analitica di flusso di Azure. Per altre informazioni, vedere [Trasmettere i dati dal BLOB di archiviazione di Azure ad Archivio Data Lake usando l'analisi di flusso di Azure](data-lake-store-stream-analytics.md).

## <a name="use-data-lake-store-with-power-bi"></a>Uso di Archivio Data Lake con Power BI
È possibile utilizzare i dati di Power BI tooimport da un tooanalyze account archivio Data Lake e visualizzare i dati di hello. Per altre informazioni, vedere [Analisi dei dati in Archivio Data Lake con Power BI](data-lake-store-power-bi.md).

## <a name="use-data-lake-store-with-data-catalog"></a>Uso di Archivio Data Lake con Catalogo dati di Azure
È possibile registrare i dati di archivio Data Lake in hello dati hello Azure Data Catalog toomake individuabili nell'intera organizzazione hello. Per altre informazioni, vedere [Registrazione i dati da Archivio Data Lake in Catalogo dati di Azure](data-lake-store-with-data-catalog.md).

## <a name="use-data-lake-store-with-sql-server-integration-services-ssis"></a>Uso di Data Lake Store con SQL Server Integration Services (SSIS)
È possibile utilizzare Gestione connessione di archivio Azure Data Lake hello in tooconnect SSIS un pacchetto SSIS con archivio Azure Data Lake. Per altre informazioni, vedere [Usare Data Lake Store con SSIS](https://docs.microsoft.com/sql/integration-services/connection-manager/azure-data-lake-store-connection-manager).

## <a name="use-data-lake-store-with-sql-data-warehouse"></a>Uso di Data Lake Store con SQL Data Warehouse
È possibile utilizzare i dati di PolyBase tooload dall'archivio Azure Data Lake in SQL Data Warehouse. Per altre informazioni, vedere [Usare Data Lake Store con SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-load-from-azure-data-lake-store.md).

## <a name="see-also"></a>Vedere anche
* [Panoramica di Data Lake Store di Azure](data-lake-store-overview.md)
* [Introduzione a Data Lake Store mediante il portale](data-lake-store-get-started-portal.md)
* [Introduzione a Data Lake Store mediante PowerShell](data-lake-store-get-started-powershell.md)  

