---
title: aaaMove tooor di dati dall'archiviazione Blob di Azure utilizzando i connettori SSIS | Documenti Microsoft
description: Spostare dati tooor dall'archiviazione Blob di Azure utilizzando i connettori SSIS.
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 96a1b5fb-34d1-4b9b-8d99-2bb8289e0398
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 15068af1c69f11e74e109ee5ae2b9f1a674ea388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooor-from-azure-blob-storage-using-ssis-connectors"></a>Spostare dati tooor dall'archiviazione Blob di Azure utilizzando i connettori SSIS
Hello [SQL Server Integration Services Feature Pack per Azure](https://msdn.microsoft.com/library/mt146770.aspx) fornisce componenti tooconnect tooAzure, trasferire i dati tra origini dati locali e Azure e di elaborare i dati archiviati in Azure.

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

Una volta che i clienti sono stati spostati i dati locali nel cloud hello, è possibile accedervi da qualsiasi servizio di Azure tooleverage hello potenzialità della suite hello di tecnologie di Azure. È ad esempio possibile usare i dati in Azure Machine Learning o in un cluster HDInsight.

Si tratta in genere essere innanzitutto hello per hello [SQL](machine-learning-data-science-process-sql-walkthrough.md) e [HDInsight](machine-learning-data-science-process-hive-walkthrough.md) procedure dettagliate.

Per una descrizione degli scenari canonici che usano business tooaccomplish SSIS deve comuni negli scenari di integrazione ibrido, vedere [ciò più con SQL Server Integration Services Feature Pack per Azure](http://blogs.msdn.com/b/ssis/archive/2015/06/25/doing-more-with-sql-server-integration-services-feature-pack-for-azure.aspx) blog.

> [!NOTE]
> Per un'archiviazione blob tooAzure introduzione completa, vedere troppo[nozioni fondamentali di Blob di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) e troppo[servizio Blob di Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Prerequisiti
attività di hello tooperform descritte in questo articolo, è necessario disporre una sottoscrizione di Azure e configurare un account di archiviazione di Azure. È necessario conoscere l'archiviazione di Azure account nome account e la chiave tooupload o il download dei dati.

* tooset backup un **sottoscrizione di Azure**, vedere [la versione di un mese valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Per istruzioni sulla creazione di un **account di archiviazione** e su come ottenere le informazioni sull'account e sulla chiave, vedere [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).

hello toouse **connettori SSIS**, è necessario scaricare:

* **SQL Server 2014 o 2016 Standard (o versioni successive)**: l'installazione include SQL Server Integration Services.
* **Microsoft SQL Server 2014 o 2016 Integration Services Feature Pack per Azure**: questi possono essere scaricati, rispettivamente, dalla hello [SQL Server 2014 Integration Services](http://www.microsoft.com/download/details.aspx?id=47366) e [integrazione di SQL Server 2016 Servizi](https://www.microsoft.com/download/details.aspx?id=49492) pagine.

> [!NOTE]
> SSIS viene installato con SQL Server, ma non è incluso nella versione Express hello. Per informazioni sulle applicazioni incluse nelle diverse edizioni di SQL Server, vedere [Edizioni di SQL Server](http://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/)
> 
> 

Per materiale di formazione su SSIS, vedere [Risorse pratiche per la formazione su SSIS](http://www.microsoft.com/download/details.aspx?id=20766)

Per informazioni su come tooget alto e a esecuzione prolungata tramite SISS toobuild semplice estrazione, trasformazione e caricamento (ETL) di pacchetti, vedere [SSIS Tutorial: creazione di un pacchetto ETL semplice](https://msdn.microsoft.com/library/ms169917.aspx).

## <a name="download-nyc-taxi-dataset"></a>Scaricare il set di dati NYC Taxi
Hello ad esempio descritto di seguito, usare un set di dati disponibile pubblicamente, hello [NYC Taxi trip](http://www.andresmh.com/nyctaxitrips/) set di dati. set di dati Hello è costituito da si basa taxi 173 milioni in NYC nell'anno hello 2013. Sono disponibili due tipi di dati: i dettagli sul tragitto e i dettagli sul costo del tragitto. Poiché è disponibile un file per ogni mese, sono presenti 24 file in tutto, ognuno dei quali ha dimensioni pari a circa 2 GB, senza compressione.

## <a name="upload-data-tooazure-blob-storage"></a>Carica l'archiviazione blob di dati tooAzure
feature pack dall'archiviazione blob di on-premise tooAzure di toomove dati tramite SSIS hello, si usa un'istanza di hello [ **attività di caricamento Blob di Azure**](https://msdn.microsoft.com/library/mt146776.aspx), illustrato di seguito:

![configure-data-science-vm](./media/machine-learning-data-science-move-data-to-azure-blob-using-ssis/ssis-azure-blob-upload-task.png)

parametri Hello hello utilizza attività sono descritti di seguito:

| Campo | Descrizione |
| --- | --- |
| **AzureStorageConnection** |Specifica una gestione connessione di archiviazione Azure esistente o crea un nuovo oggetto che fa riferimento tooan account di archiviazione Azure che fa riferimento a file di blob hello toowhere ospitati. |
| **BlobContainer** |Specifica il nome di hello del contenitore blob hello che contengono file hello caricato come BLOB. |
| **BlobDirectory** |Specifica directory blob hello in cui i file caricati hello è archiviato come blob in blocchi. directory blob Hello è una struttura gerarchica virtuale. Se il blob hello esiste già, ia sostituito. |
| **LocalDirectory** |Specifica directory locale hello contenente toobe file hello caricato. |
| **FileName** |Specifica un file con nome filtro tooselect con modello di nome specificato hello. Ad esempio, MySheet\*.xls\* include file, quali MySheet001.xls e MySheetABC.xlsx |
| **TimeRangeFrom/TimeRangeTo** |Specifica un filtro basato su un intervallo di tempo. Sono inclusi file modificati dopo *TimeRangeFrom* e prima di *TimeRangeTo*. |

> [!NOTE]
> Hello **AzureStorageConnection** le credenziali devono toobe corretto e hello **BlobContainer** deve essere presente prima di tenta di trasferimento hello.
> 
> 

## <a name="download-data-from-azure-blob-storage"></a>Scaricare i dati da un archivio BLOB di Azure
dati toodownload dall'archiviazione locale tooon di archiviazione blob di Azure con SSIS, utilizzare un'istanza di hello [attività di caricamento Blob di Azure](https://msdn.microsoft.com/library/mt146779.aspx).

## <a name="more-advanced-ssis-azure-scenarios"></a>Altri scenari avanzati di SSIS-Azure
feature pack di Hello SSIS consente più complessi toobe flussi gestiti insieme da attività di creazione del pacchetto. Ad esempio, possano feed di dati di blob hello direttamente in un cluster HDInsight, il cui output è stato possibile scaricare blob tooa indietro e quindi archiviazione tooon locale. SSIS può eseguire processi Hive e Pig in un cluster HDInsight usando connessioni SSIS aggiuntive:

* uno script Hive in un Azure HDInsight cluster con SSIS, utilizzare toorun [attività Hive di Azure HDInsight](https://msdn.microsoft.com/library/mt146771.aspx).
* uno script Pig in un Azure HDInsight cluster con SSIS, utilizzare toorun [attività Pig di Azure HDInsight](https://msdn.microsoft.com/library/mt146781.aspx).

