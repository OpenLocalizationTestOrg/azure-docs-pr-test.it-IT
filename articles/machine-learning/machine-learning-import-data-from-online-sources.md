---
title: dati aaaImport in Machine Learning Studio da origini dati online | Documenti Microsoft
description: Come tooimport i dati di training, Azure Machine Learning Studio di varie origini online.
keywords: dati di importazione, formato dati, tipi di dati, origini dati, dati di training
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 701b93fe-765b-4d15-a1cf-9b607f17add6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;garye
ms.openlocfilehash: aae6907cdd0b4dc373ae08c2569caa276c198b49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-azure-machine-learning-studio-from-various-online-data-sources-with-hello-import-data-module"></a>Importare dati in Azure Machine Learning Studio da diverse origini dati online con il modulo di importazione dei dati hello
In questo articolo viene descritto il supporto di hello per l'importazione di dati online da diverse origini e le informazioni di hello necessarie toomove dati da queste origini in un esperimento di Azure Machine Learning.

> [!NOTE]
> In questo articolo fornisce informazioni generali sull'hello [l'importazione dei dati] [ import-data] modulo. Per ulteriori informazioni sui tipi di hello dei dati è possibile accedere, formati, parametri e le risposte alle domande di toocommon, vedere argomento di riferimento modulo hello per hello [l'importazione dei dati] [ import-data] modulo.
> 
> 

<!-- -->

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

## <a name="introduction"></a>Introduzione
Utilizzando hello [l'importazione dei dati] [ import-data] modulo, è possibile accedere ai dati da una delle diverse origini dati online mentre l'esperimento è in esecuzione in [Azure Machine Learning Studio](https://studio.azureml.net/Home):

* URL Web tramite HTTP
* Hadoop tramite HiveQL
* Archivio BLOB di Azure
* Tabella di Azure
* Database SQL di Azure o SQL Server in una macchina virtuale di Azure
* Database SQL Server locale
* Provider di feed di dati, attualmente OData
* Azure CosmosDB (in precedenza denominato DocumentDB)

le origini dati online tooaccess nell'esperimento Studio, aggiungere hello [l'importazione dei dati] [ import-data] tooyour modulo, seleziona hello **origine dati**, quindi specificare i parametri di hello necessari dati hello tooaccess. le origini dati online Hello supportate vengono classificate in tabella hello riportata di seguito. Questa tabella sono elencati anche i formati di file hello supportati e i parametri che vengono utilizzati tooaccess hello dati.

Dal momento che si accede a questi dati di training durante l'esecuzione dell'esperimento, i dati sono disponibili solo durante l'esperimento. In confronto, i dati archiviati in un modulo di set di dati sono esperimento tooany disponibile nell'area di lavoro.

> [!IMPORTANT]
> Attualmente, hello [l'importazione dei dati] [ import-data] e [Esporta dati] [ export-data] moduli possono leggere e scrivere dati solo dall'archiviazione di Azure creata utilizzando hello Modello di distribuzione classica. In altre parole, hello nuovo tipo di account di archiviazione Blob di Azure che offre un livello di accesso di archiviazione di frequente o il livello di accesso sporadico archiviazione non è ancora supportato. 
> 
> In genere gli account di archiviazione di Azure creati prima che fosse disponibile questa opzione non dovrebbero essere influenzati. 
> Se è necessario un nuovo account toocreate, selezionare **classico** per hello distribuzione del modello, oppure utilizzare Gestione risorse e selezionare **generici** anziché **nell'archiviazione Blob** per **Account kind**. 
> 
> Per altre informazioni, vedere [Archivio BLOB di Azure: livelli di archiviazione ad accesso frequente e sporadico](../storage/blobs/storage-blob-storage-tiers.md).
> 
> 

## <a name="supported-online-data-sources"></a>Origini dati online supportate
Azure Machine Learning **l'importazione dei dati** modulo supporta le seguenti origini dati hello:

| origine dati | Descrizione | Parametri |
| --- | --- | --- |
| URL Web tramite HTTP |Legge i dati nei formati CSV (Comma-Separated Values), TSV (Tab-Separated Values), ARFF (Attribute-Relation File Format) e SVM-light (Support Vector Machines), da qualsiasi URL Web che usa HTTP. |<b>URL</b>: hello nome completo del file di hello, incluso l'URL del sito hello e nome del file hello, con un'estensione specifica. <br/><br/><b>Formato dati</b>: specifica uno dei dati supportata hello formati: CSV, TSV, ARFF o svmlight. Se i dati di hello dispone di una riga di intestazione, è tooassign utilizzati nomi di colonna. |
| Hadoop/HDFS |Legge i dati dall'archivio distribuito in Hadoop. Specificare i dati di hello desiderati tramite HiveQL, un linguaggio di query simile a SQL. HiveQL può anche essere tooaggregate utilizzati dati e filtrarli prima di aggiungere dati di hello tooMachine Learning Studio. |<b>Query di database hive</b>: specifica di query Hive hello utilizzati dati hello toogenerate.<br/><br/><b>URI del server HCatalog </b> : il nome specificato hello del cluster utilizzando il formato di hello  *&lt;il nome del cluster&gt;. cluster>.azurehdinsight.NET.*<br/><br/><b>Nome dell'account utente Hadoop</b>: specifica di account utente di Hadoop hello nome utilizzato cluster hello tooprovision.<br/><br/><b>Password dell'account utente Hadoop</b> : specifica le credenziali utilizzate durante il provisioning di cluster hello hello. Per altre informazioni, vedere [Creare cluster Hadoop basati su Windows in HDInsight](../hdinsight/hdinsight-provision-clusters.md).<br/><br/><b>Percorso dei dati di output</b>: Specifica se i dati hello sono archiviati in un file system distribuito Hadoop (HDFS) o in Azure. <br/><ul>Se si archiviano dati di output in HDFS, specificare l'URI del server HDFS hello. (Utilizzare che toouse hello nome del cluster HDInsight senza prefisso HTTPS:// hello). <br/><br/>Se si archiviano i dati di output in Azure, è necessario specificare nome account di archiviazione di Azure hello, chiave di accesso di archiviazione e il nome di contenitore di archiviazione.</ul> |
| Database SQL |Legge i dati archiviati in un database SQL di Azure o in un database SQL Server in esecuzione in una macchina virtuale di Azure. |<b>Nome del server database</b>: Specifica il nome di hello del server di hello nel quale hello database è in esecuzione.<br/><ul>In caso di Database SQL di Azure consente di immettere nome hello del server che viene generato. In genere ha il formato di hello  *&lt;generated_identifier&gt;. database.windows.net.* <br/><br/>Nel caso di un'istanza di SQL Server ospitata in una macchina virtuale di Azure immettere *tcp:&lt;Nome DNS macchina virtuale&gt;, 1433*</ul><br/><b>Nome del database </b>: Specifica il nome di hello del database hello del server hello. <br/><br/><b>Nome dell'account utente server</b>: specifica un nome utente per un account che dispone delle autorizzazioni di accesso per il database di hello. <br/><br/><b>Password dell'account utente server</b>: specifica la password di hello per account utente di hello.<br/><br/><b>Qualsiasi certificato server accettare</b>: utilizzare questa opzione (meno sicura) se si desidera tooskip revisione certificato del sito hello prima di leggere i dati.<br/><br/><b>Query di database</b>: immettere un'istruzione SQL che descrive i dati di hello da tooread. |
| Database SQL locale |Legge i dati archiviati in un database SQL locale. |<b>Gateway dati</b>: Specifica il nome di hello di hello Gateway di gestione di dati installato in un computer in cui è possibile accedere al database SQL Server. Per informazioni sulla configurazione di gateway di hello, vedere [eseguire advanced analitica con Azure Machine Learning che usano dati da un server SQL locale](machine-learning-use-data-from-an-on-premises-sql-server.md).<br/><br/><b>Nome del server database</b>: Specifica il nome di hello del server di hello nel quale hello database è in esecuzione.<br/><br/><b>Nome del database </b>: Specifica il nome di hello del database hello del server hello. <br/><br/><b>Nome dell'account utente server</b>: specifica un nome utente per un account che dispone delle autorizzazioni di accesso per il database di hello. <br/><br/><b>Nome utente e password</b>: fare clic su <b>immettere i valori</b> tooenter le credenziali di database. È possibile usare Autenticazione integrata di Windows o Autenticazione di SQL Server, in base al tipo di configurazione del database SQL Server locale.<br/><br/><b>Query di database</b>: immettere un'istruzione SQL che descrive i dati di hello da tooread. |
| tabella di Azure |Legge i dati dal servizio tabelle di archiviazione di Azure hello.<br/><br/>Se si legge spesso grandi quantità di dati, utilizzare hello del servizio tabelle di Azure. Offre una soluzione di archiviazione flessibile, non relazionale (NoSQL), a scalabilità elevata, poco costosa e a disponibilità elevata. |opzioni di hello Hello **l'importazione dei dati** variano a seconda che si acceda a informazioni pubbliche o a un account di archiviazione privato che richiede credenziali di accesso. Ciò è determinato dal hello <b>tipo di autenticazione</b> che possono avere valore "PublicOrSAS" o "Account", ognuno dei quali ha un proprio set di parametri. <br/><br/><b>Pubblico o condiviso (firma di accesso) URI</b>: hello parametri sono:<br/><br/><ul><b>Tabella URI</b>: specifica hello pubblico o l'URL di firma di accesso condiviso per tabella hello.<br/><br/><b>Specifica hello tooscan di righe per i nomi delle proprietà</b>: i valori hello sono <i>TopN</i> tooscan hello specificato numero di righe o <i>ScanAll</i> tooget tutte le righe della tabella hello. <br/><br/>Se hello dati sono omogenei e prevedibili, è consigliabile selezionare *TopN* e immettere un numero per N. Per le tabelle di grandi dimensioni, questo può comportare tempi di lettura.<br/><br/>Se i dati di hello sono strutturati con set di proprietà che variano in base a una profondità di hello e la posizione della tabella hello, scegliere hello *ScanAll* opzione tooscan tutte le righe. Ciò garantisce l'integrità della conversione dei metadati di proprietà risultante e hello.<br/><br/></ul><b>Account di archiviazione privati</b>: hello parametri sono: <br/><br/><ul><b>Nome dell'account</b>: Specifica il nome di hello dell'account hello contenente tooread tabella hello.<br/><br/><b>Chiave dell'account</b>: specifica chiave di archiviazione di hello associata hello account.<br/><br/><b>Nome della tabella</b> : Specifica il nome di hello della tabella hello contenente tooread dati hello.<br/><br/><b>Tooscan righe per i nomi delle proprietà</b>: i valori hello sono <i>TopN</i> tooscan hello specificato numero di righe o <i>ScanAll</i> tooget tutte le righe della tabella hello.<br/><br/>Se hello dati sono omogenei e prevedibili, è consigliabile selezionare *TopN* e immettere un numero per N. Per le tabelle di grandi dimensioni, questo può comportare tempi di lettura.<br/><br/>Se i dati di hello sono strutturati con set di proprietà che variano in base a una profondità di hello e la posizione della tabella hello, scegliere hello *ScanAll* opzione tooscan tutte le righe. Ciò garantisce l'integrità della conversione dei metadati di proprietà risultante e hello.<br/><br/> |
| Archiviazione BLOB di Azure |Legge i dati archiviati nel servizio Blob hello in archiviazione di Azure, tra cui immagini, testo non strutturato o dati binari.<br/><br/>È possibile utilizzare dati di esporre toopublicly servizio Blob hello o tooprivately archivio dati dell'applicazione. È possibile accedere ai dati da qualsiasi posizione mediante connessioni HTTP o HTTPS. |opzioni di hello Hello **l'importazione dei dati** modulo cambia a seconda che si acceda a informazioni pubbliche o a un account di archiviazione privato che richiede credenziali di accesso. Ciò è determinato dal hello <b>tipo di autenticazione</b> che possono avere un valore di "PublicOrSAS" o "Account".<br/><br/><b>Pubblico o condiviso (firma di accesso) URI</b>: hello parametri sono:<br/><br/><ul><b>URI</b>: specifica hello pubblico o l'URL di firma di accesso condiviso per il blob di archiviazione hello.<br/><br/><b>Formato di file</b>: Specifica il formato di hello dei dati hello hello servizio Blob. formati di Hello supportato sono CSV, TSV e ARFF.<br/><br/></ul><b>Account di archiviazione privati</b>: hello parametri sono: <br/><br/><ul><b>Nome dell'account</b>: Specifica il nome di hello dell'account hello che contiene il blob hello desiderato tooread.<br/><br/><b>Chiave dell'account</b>: specifica chiave di archiviazione di hello associata hello account.<br/><br/><b>Blob, directory o percorso toocontainer </b> : Specifica il nome di hello del blob hello contenente tooread dati hello.<br/><br/><b>Formato del file BLOB</b>: Specifica il formato di hello dei dati di hello nel servizio blob hello. Hello formati dati supportati sono CSV, TSV, ARFF, CSV con una codifica specificata ed Excel. <br/><br/><ul>Se il formato di hello è CSV o TSV, essere tooindicate che indica se il file hello contiene una riga di intestazione.<br/><br/>È possibile utilizzare dati tooread di opzione hello Excel dalle cartelle di lavoro di Excel. In hello <i>formato dati di Excel</i> opzione, indicare se i dati di hello sono in un foglio di lavoro Excel o in una tabella di Excel. In hello <i>foglio di Excel o tabella incorporata </i>, specificare il nome di hello di hello foglio o della tabella che si desidera tooread da.</ul><br/> |
| Provider di feed di dati |Legge dati da un provider di feed supportato. Formato di Open Data Protocol (OData) attualmente solo hello è supportato. |<b>Tipo di dati contenuto</b>: Specifica il formato di OData hello.<br/><br/><b>URL di origine</b>: specifica l'URL completo per i feed di dati hello hello. <br/>Ad esempio, hello seguente URL legge dal database di esempio Northwind hello: http://services.odata.org/northwind/northwind.svc/ |

## <a name="next-steps"></a>Passaggi successivi

[Distribuzione di servizi di Web Azure ML che usano i moduli Import Data ed Export Data](machine-learning-web-services-that-use-import-export-modules.md)


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[export-data]: https://msdn.microsoft.com/library/azure/7A391181-B6A7-4AD4-B82D-E419C0D6522C/
