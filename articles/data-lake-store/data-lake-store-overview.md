---
title: aaaOverview di archivio Azure Data Lake | Documenti Microsoft
description: Comprendere l'archivio Azure Data Lake e hello valore che consente di altri archivi dati
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: b3475057-9427-4492-a3af-25a802a23a79
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 5a60a6b86a51c44647cf4ee168fb333d1c37b1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-data-lake-store"></a>Panoramica dell’Archivio Data Lake di Azure
Azure Data Lake Store è un repository su vasta scala a livello aziendale per carichi di lavoro di analisi di Big Data. Azure Data Lake consente toocapture dati di qualsiasi velocità di dimensioni, tipo e l'inserimento in un'unica posizione per analitica operative ed esplorative.

> [!TIP]
> Hello utilizzare [percorso di apprendimento di archivio Data Lake](https://azure.microsoft.com/documentation/learning-paths/data-lake-store-self-guided-training/) toostart esplorazione servizio Archivio Azure Data Lake hello.
> 
> 

Archivio Azure Data Lake è possibile accedere da Hadoop (disponibile con il cluster HDInsight) utilizzando le API REST WebHDFS compatibile hello. È specificamente progettato tooenable analitica sui dati archiviato hello ed è ottimizzato per le prestazioni per scenari di dati analitica. Viene fornita, hello include tutte le funzionalità di livello aziendale hello, sicurezza, gestibilità, scalabilità, affidabilità e disponibilità, essenziale per casi di utilizzo reali enterprise.

![Azure Data Lake](./media/data-lake-store-overview/data-lake-store-concept.png)

Alcune delle funzionalità principali di hello di hello Azure Data Lake includono seguente hello.

### <a name="built-for-hadoop"></a>Creato per Hadoop
archivio Azure Data Lake Hello è un file system Apache Hadoop compatibile con Hadoop Distributed File System (HDFS) e funziona con l'ecosistema di Hadoop hello.  Esistente HDInsight o servizi che utilizzano API WebHDFS hello possono integrare facilmente con l'archivio Data Lake. L’Archivio Data Lake presenta anche un'interfaccia REST compatibile con WebHDFS per le applicazioni

I dati archiviati nell'Archivio Data Lake possono essere analizzati facilmente mediante framework di analisi di Hadoop, come MapReduce o Hive. I cluster di Microsoft Azure HDInsight possono eseguire il provisioning e configurato toodirectly accedere ai dati archiviati nell'archivio Data Lake.

### <a name="unlimited-storage-petabyte-files"></a>Archiviazione illimitata, file dei petabyte
L’Archivio Data Lake di Azure fornisce un'archiviazione illimitata ed è adatto per l'archiviazione di una serie di dati per l'analisi. Ciò non impone eventuali limiti di dimensioni di account, le dimensioni dei file o quantità hello di dati che possono essere archiviati in un servizio di data lake. Singoli file possono variare da toopetabytes kilobyte in rendendo toostore un'ottima scelta qualsiasi tipo di dati. Dati vengono archiviati in modo durevole, eseguendo copie più e non è previsto alcun limite per la durata di hello di tempo per cui hello dati possono essere archiviati nel servizio di data lake hello.

### <a name="performance-tuned-for-big-data-analytics"></a>Prestazioni ottimizzate per l'analisi di Big Data
Archivio Azure Data Lake è compilato per l'esecuzione di sistemi analitici che richiedono una velocità effettiva massive tooquery e analizzare grandi quantità di dati su larga scala. servizio di data lake Hello distribuisce parti di un file su un numero di server di archiviazione singolo. Ciò migliora la velocità effettiva di lettura durante la lettura di file hello in parallelo per l'esecuzione di analitica dati hello.

### <a name="enterprise-ready-highly-available-and-secure"></a>A livello aziendale: con disponibilità elevata e sicuro
L’Archivio Data Lake di Azure offre affidabilità e disponibilità standard del settore. Asset di dati vengono archiviati in modo durevole, eseguendo copie ridondanti tooguard contro eventuali errori imprevisti. Le aziende possono utilizzare Azure Data Lake nelle loro soluzioni come una parte importante della piattaforma di dati esistente.

Archivio Data Lake offre inoltre la sicurezza a livello aziendale per i dati archiviato hello. Per altre informazioni, vedere [Protezione dei dati in Archivio Data Lake di Azure](#DataLakeStoreSecurity).

### <a name="all-data"></a>Tutti i dati
L’Archivio Data Lake di Azure può immagazzinare i dati nel loro formato originale, così come sono, senza alcuna trasformazione. Archivio Data Lake non richiedono un toobe schema definito prima di caricare dati hello, lasciandolo backup dei dati di toohello singoli framework analitiche toointerpret hello e definire uno schema in fase di analisi hello di hello. Da file toostore in grado di dimensioni arbitrarie e formati rende possibile toohandle archivio Data Lake strutturati, semistrutturati e non strutturati dati.

I contenitori di Archivio Azure Data Lake per i dati sono essenzialmente cartelle e file. Operare sui dati hello archiviato utilizzando il SDK, il portale di Azure e Azure Powershell. Come si inseriscono i dati nell'archivio di hello usando queste interfacce e contenitori adatti hello, è possibile archiviare qualsiasi tipo di dati. Archivio Data Lake non esegue una gestione speciale dei dati in base al tipo di hello di dati in esso memorizzati.

## <a name="DataLakeStoreSecurity"></a>Protezione dei dati nell'archivio Data Lake di Azure
Archivio Azure Data Lake Usa Azure Active Directory per l'autenticazione e gli elenchi di controllo di accesso (ACL) toomanage accedere ai dati di tooyour.

| Funzionalità | Descrizione |
| --- | --- |
| Autenticazione |Archivio Azure Data Lake si integra con Azure Active Directory (AAD) per la gestione di identità e accessi per tutti i dati di hello archiviati nell'archivio Azure Data Lake. Grazie all'integrazione di hello, vantaggi di Azure Data Lake da tutte le funzionalità AAD, tra cui multi-factor authentication, l'accesso condizionale, il controllo di accesso basato sui ruoli, monitoraggio dell'utilizzo dell'applicazione, sicurezza di monitoraggio e avviso, e così via. Archivio Azure Data Lake supporta hello protocollo OAuth 2.0 per l'autenticazione con nell'interfaccia REST hello. |
| Controllo di accesso |Archivio Azure Data Lake fornisce controllo di accesso tramite il supporto delle autorizzazioni di tipo POSIX esposte dall'hello WebHDFS protocollo. In hello Data Lake archivio pubblico Preview (versione corrente di hello), gli ACL possono essere abilitati nella cartella radice hello, le sottocartelle e sui singoli file. Per altre informazioni sul funzionamento degli elenchi di controllo di accesso nel contesto di Data Lake Store, vedere [Controllo di accesso in Data Lake Store](data-lake-store-access-control.md). |
| Crittografia |Archivio Data Lake offre anche la crittografia per i dati vengono archiviati in account hello. Specificare le impostazioni di crittografia hello durante la creazione di un account archivio Data Lake. Puoi scegliere toohave i dati crittografati o optare per alcuna crittografia. Per ulteriori informazioni sulla configurazione relative a crittografia tooprovide, vedere [introduzione archivio Azure Data Lake tramite il portale di Azure hello](data-lake-store-get-started-portal.md). |

Desidera toolearn ulteriori informazioni sulla protezione dei dati in archivio Data Lake. Seguire i collegamenti di hello riportati di seguito.

* Per istruzioni su come visualizzare dati toosecure in archivio Data Lake, [la protezione dei dati in archivio Azure Data Lake](data-lake-store-secure-data.md).
* Se si preferiscono i video, [Guardare questo video](https://mix.office.com/watch/1q2mgzh9nn5lx) sulla modalità di archiviazione dati toosecure in archivio Data Lake.

## <a name="applications-compatible-with-azure-data-lake-store"></a>Applicazioni compatibili con l'archivio Data Lake di Azure
Archivio Azure Data Lake è compatibile con i componenti di origine più aperti nell'ecosistema Hadoop hello. Si integra bene anche con altri servizi di Azure. Questo fa di Archivio Data Lake la soluzione ideale per le esigenze di archiviazione dei dati. Seguire i collegamenti di hello sotto toolearn informazioni su come archivio Data Lake può essere utilizzato sia con i componenti di origine aperti, nonché altri servizi di Azure.

* Vedere [Applicazioni e servizi compatibili con Archivio Azure Data Lake](data-lake-store-compatible-oss-other-applications.md) per un elenco di applicazioni open source interoperative con Archivio Data Lake.
* Vedere [l'integrazione con altri servizi di Azure](data-lake-store-integrate-with-other-services.md) toounderstand come archivio Data Lake è utilizzabile con altri Azure servizi tooenable una vasta gamma di scenari.
* Vedere [scenari per l'utilizzo di archivio Data Lake](data-lake-store-data-scenarios.md) toolearn sulla modalità di memorizzazione toouse Data Lake negli scenari, ad esempio l'inserimento di dati, l'elaborazione dei dati, il download dei dati e visualizzazione dei dati.

## <a name="what-is-azure-data-lake-store-file-system-adl"></a>Informazioni sul file system di Azure Data Lake Store (adl://)
Archivio Data Lake sono accessibili tramite hello nuovo filesystem, hello AzureDataLakeFilesystem (adl: / /), in ambienti di Hadoop (disponibili con il cluster HDInsight). Le applicazioni e servizi che usano adl: / / sono tootake in grado di sfruttare un'ulteriore ottimizzazione delle prestazioni che non sono attualmente disponibili in WebHDFS. Di conseguenza, offre archivio Data Lake hello tooeither flessibilità avvalersi prestazioni ottimali hello con opzione di utilizzo adl consigliata hello: / / o mantengono direttamente il codice esistente continua toouse hello WebHDFS API. Azure HDInsight sfrutta completamente hello AzureDataLakeFilesystem tooprovide hello prestazioni ottimali in archivio Data Lake.

È possibile accedere ai dati con archivio Data Lake hello `adl://<data_lake_store_name>.azuredatalakestore.net`. Per ulteriori informazioni su come tooaccess hello dati in archivio Data Lake hello, vedere [visualizzare le proprietà di hello dati archiviati](data-lake-store-get-started-portal.md#properties)

## <a name="how-do-i-start-using-azure-data-lake-store"></a>Come iniziare ad utilizzare Archivio Data Lake di Azure?
Vedere [informazioni introduttive sull'utilizzo di archivio Data Lake hello Azure Portal](data-lake-store-get-started-portal.md), in modo tooprovision un archivio Data Lake tramite hello portale di Azure. Una volta che si è eseguito il provisioning di Azure Data Lake, è possibile ottenere informazioni come toouse offerte di dati di grandi dimensioni, ad esempio Azure Data Lake Analitica o Azure HDInsight con archivio Data Lake. È anche possibile creare un toocreate applicazione .NET un account archivio Azure Data Lake ed eseguire operazioni quali dati di caricamento, download dei dati e così via.

* [Introduzione all’analisi dei dati di Data Lake di Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Usare Azure HDInsight con Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Introduzione a Azure Data Lake Store utilizzando .NET SDK](data-lake-store-get-started-net-sdk.md)

## <a name="data-lake-store-videos"></a>Video su Archivio Data Lake
Se si preferisce guardare i video toolearn, archivio Data Lake fornisce video su una gamma di funzionalità.

* [Creare un account di Archivio Azure Data Lake](https://mix.office.com/watch/1k1cycy4l4gen)
* [Utilizzare hello Esplora dati tooManage dati in archivio Azure Data Lake](https://mix.office.com/watch/icletrxrh6pc)
* [La connessione di archivio Azure Data Lake Analitica tooAzure Data Lake](https://mix.office.com/watch/qwji0dc9rx9k)
* [Accedere ad Archivio Azure Data Lake con Analisi Azure Data Lake](https://mix.office.com/watch/1n0s45up381a8)
* [La connessione di archivio Data Lake di Azure HDInsight tooAzure](https://mix.office.com/watch/l93xri2yhtp2)
* [Accedere ad Archivio Azure Data Lake con Hive e Pig](https://mix.office.com/watch/1n9g5w0fiqv1q)
* [Utilizzare DistCp (Hadoop Distributed copia) toocopy dati tooand dall'archivio Azure Data Lake](https://mix.office.com/watch/1liuojvdx6sie)
* [Utilizzare Apache Sqoop toomove dati tra origini relazionali e archivio Azure Data Lake](https://mix.office.com/watch/1butcdjxmu114)
* [Orchestrazione di dati con Azure Data Factory per Archivio Azure Data Lake](https://mix.office.com/watch/1oa7le7t2u4ka)
* [Protezione dei dati in hello archivio Azure Data Lake](https://mix.office.com/watch/1q2mgzh9nn5lx)

