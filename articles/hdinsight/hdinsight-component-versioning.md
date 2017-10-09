---
title: aaaHadoop componenti e le versioni - HDInsight di Azure | Documenti Microsoft
description: Informazioni sui componenti Hadoop hello e le versioni in HDInsight e hello livelli di servizio disponibile in questa distribuzione cloud di Hortonworks Data Platform.
keywords: versioni di Hadoop, componenti ecosistema di hadoop, componenti hadoop, come versione di hadoop toocheck
services: hdinsight
editor: cgronlun
manager: asadk
author: bprakash
tags: azure-portal
documentationcenter: 
ms.assetid: 367b3f4a-f7d3-4e59-abd0-5dc59576f1ff
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: bprakash
ms.openlocfilehash: b661d901b0113458c3501ec06454fc8841189672
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-hello-hadoop-components-and-versions-available-with-hdinsight"></a>Quali sono i componenti di hello Hadoop e le versioni disponibili con HDInsight?

Informazioni sui componenti ecosistema di hello Apache Hadoop e le versioni in Microsoft Azure HDInsight, nonché hello livelli di servizio Standard e Premium. Inoltre, informazioni su come versioni dei componenti di toocheck Hadoop in HDInsight. 

Ogni versione di HDInsight è una distribuzione cloud di una versione di Hortonworks Data Platform (HDP).

## <a name="hadoop-components-available-with-different-hdinsight-versions"></a>Componenti di Hadoop disponibili con diverse versioni di HDInsight
Azure HDInsight supporta più versioni cluster di Hadoop che possono essere distribuite in qualsiasi momento. Ogni opzione di versione viene creata una versione specifica di distribuzione HDP hello e un set di componenti contenuti all'interno di tale distribuzione. A partire da febbraio 17, 2017, versione del cluster hello predefinito utilizzato da Azure HDInsight è 3.5 e si basa sull'HDP 2.5.

Nella hello nella tabella seguente sono elencate le versioni dei componenti di Hello associati alle versioni cluster HDInsight. 

> [!NOTE]
> versione di Hello predefinita per il servizio HDInsight hello potrebbe cambiare senza preavviso. Se si dispone di una dipendenza della versione, specificare la versione di HDInsight hello quando si crea il cluster con hello .NET SDK con Azure PowerShell e CLI di Azure.

| Componente | HDInsight 3.6 (predefinito) | HDInsight 3.5 | HDInsight 3.4 | HDInsight 3.3 | HDInsight 3.2 | HDInsight 3.1 | HDInsight 3.0 |
| --- | --- | --- | --- | --- | --- | --- |--- |
| Hortonworks Data Platform |2.6 |2.5 |2.4 |2.3 |2.2 |2.1.7 |2.0 |
| Apache Hadoop e YARN |2.7.3 |2.7.3 |2.7.1 |2.7.1 |2.6.0 |2.4.0 |2.2.0 |
| Apache Tez |0.7.0 |0.7.0 |0.7.0 |0.7.0 |0.5.2 |0.4.0 |-|
| Apache Pig |0.16.0 |0.16.0 |0.15.0 |0.15.0 |0.14.0 |0.12.1 |0.12.0 |
| Apache Hive e HCatalog |1.2.1 |1.2.1 |1.2.1 |1.2.1 |0.14.0 |0.13.1 |0.12.0 |
| Apache Hive2 | 2.1.0 |-|-|-|-|-|-|
| Apache Tez Hive2 | 0.8.4 |-|-|-|-|-|-|
| Apache Ranger | 0.7.0 |0.6.0 |-|-|-|-|-|
| Apache HBase |1.1.2 |1.1.2 |1.1.2 |1.1.1 |0.98.4 |0.98.0 |-|
| Apache Sqoop |1.4.6 |1.4.6 |1.4.6 |1.4.6 |1.4.5 |1.4.4 |1.4.4 |
| Apache Oozie |4.2.0 |4.2.0 |4.2.0 |4.2.0 |4.1.0 |4.0.0 |4.0.0 |
| Apache Zookeeper |3.4.6 |3.4.6 |3.4.6 |3.4.6 |3.4.6 |3.4.5 |3.4.5 |
| Apache Storm |1.1.0 |1.0.1 |0.10.0 |0.10.0 |0.9.3 |0.9.1 |-|
| Apache Mahout |0.9.0+ |0.9.0+ |0.9.0+ |0.9.0+ |0.9.0 |0.9.0 |-|
| Apache Phoenix |4.7.0 |4.7.0 |4.4.0 |4.4.0 |4.2.0 |4.0.0.2.1.7.0-2162 |-|
| Apache Spark |2.1.0 (solo Linux) |1.6.2 + 2.0 (solo Linux) |1.6.0 (solo Linux) |1.5.2 (solo Linux/build sperimentale) |1.3.1 (solo Windows) |-|-|
| Apache Kafka | 0.10.0 | 0.10.0 | 0.9.0 |-|-|-|-|
| Apache Ambari | 2.5.0 | 2.4.0 | 2.2.1 | 2.1.0 |-|-|-|
| Apache Zeppelin | 0.7.0 |-|-|-|-|-|-|
| Mono |4.2.1 |4.2.1 |3.2.8 |-|-|-|

## <a name="check-for-current-hadoop-component-version-information"></a>Controllare le informazioni sulle versioni correnti dei componenti Hadoop

versioni di componenti di Hello Hadoop ecosistema associate alle versioni cluster HDInsight può essere modificato con tooHDInsight gli aggiornamenti. componenti di Hadoop toocheck hello e tooverify vengono utilizzate le versioni per un cluster, utilizzare hello Ambari REST API. Hello **GetComponentInformation** comando recupera le informazioni sui componenti del servizio. Per informazioni dettagliate, vedere hello [Ambari documentazione][ambari-docs].

Per i cluster di Windows, un altro modo toocheck hello la versione del componente è toolog tooa cluster tramite Desktop remoto ed esaminarne il contenuto di hello della directory C:\apps\dist\ hello.

> [!IMPORTANT]
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere [Ritiro di HDInsight su Windows](#hdinsight-windows-retirement).

### <a name="release-notes"></a>Note sulla versione

Vedere [note sulla versione di HDInsight](hdinsight-release-notes.md) per note aggiuntive nelle versioni più recenti di hello di HDInsight.

## <a name="supported-hdinsight-versions"></a>Versioni supportate di HDInsight
Hello nella tabella seguente elenca le versioni hello di HDInsight attualmente disponibili nel portale di Azure hello. versioni HDP Hello corrispondenti alla versione di HDInsight tooeach vengono elencate insieme ai date di rilascio del prodotto hello. date di scadenza e sul ritiro di supporto Hello vengono inoltre fornite, quando vengono pertanto definiti.

> [!NOTE]
> Supporto per una versione è scaduto, che non sia disponibile tramite il portale classico di hello Microsoft Azure. Tuttavia, versioni precedenti di cluster verranno toobe disponibili utilizzando hello `Version` parametro hello Windows PowerShell [New AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619331.aspx) comando e hello .NET SDK fino a quando la versione hello data del ritiro.
> 
> I cluster ad alta disponibilità con due nodi head vengono distribuiti per impostazione predefinita per HDInsight versione 2.1 e successive. Non sono disponibili per i cluster HDInsight versione 1.6.

| Versione HDInsight | Versione HDP | Sistema operativo della macchina virtuale | Disponibilità elevata | Data di rilascio | Disponibilità su hello portale di Azure | Data di scadenza del supporto | Data di ritiro |
| --- | --- | --- | --- | --- | --- | --- | --- |
| HDInsight 3.6 |HDP 2.6 |Ubuntu 16 |Sì |4 aprile 2017 |Sì | | |
| HDInsight 3.5 |HDP 2.5 |Ubuntu 16 |Sì |30 settembre 2016 |Sì |5 settembre 2017 |31 maggio 2018 |
| HDInsight 3.4 |HDP 2.4 |Ubuntu 14.0.4 LTS |Sì |29 marzo 2016 |Sì |29 dicembre 2016 |9 gennaio 2018 |
| HDInsight 3.3 |HDP 2.3 |Windows Server 2012 R2 |Sì |2 dicembre 2015 |Sì |27 giugno 2016 |31 luglio 2018 |
| HDInsight 3.3 |HDP 2.3 |Ubuntu 14.0.4 LTS |Sì |2 dicembre 2015 |Sì |27 giugno 2016 |31 luglio 2017 |
| HDInsight 3.2 |HDP 2.2 |Ubuntu 12.04 LTS o Windows Server 2012 R2 |Sì |18 febbraio 2015 |No |1° marzo 2016 |1° aprile 2017 |
| HDInsight 3.1 |HDP 2.1 |Windows Server 2012 R2 |Sì |24 giugno 2014 |No |18 maggio 2015 |30 giugno 2016 |
| HDInsight 3.0 |HDP 2.0 |Windows Server 2012 R2 |Sì |11 febbraio 2014 |No |17 settembre 2014 |30 giugno 2015 |
| HDInsight 2.1 |HDP 1.3 |Windows Server 2012 R2 |Sì |28 ottobre 2013 |No |12 maggio 2014 |31 maggio 2015 |
| HDInsight 1.6 |HDP 1.1 | |No |28 ottobre 2013 |No |26 aprile 2014 |31 maggio 2015 |

## <a name="hdinsight-windows-retirement"></a>Ritiro di HDInsight in Windows
Microsoft Azure HDInsight versione 3.3 era l'ultima versione di hello di HDInsight in Windows. Hello data di ritiro per HDInsight in Windows è 31 luglio 2018. Se si dispone di tutti i cluster HDInsight in Windows 3.3 o versioni precedenti, è necessario eseguire la migrazione tooHDInsight in Linux (HDInsight 3.5 o versione successiva) prima del 31 luglio 2018. La migrazione toohello del sistema operativo Linux consente tooretain hello possibilità toocreate o ridimensionare i cluster HDInsight. Il supporto per HDInsight versione 3.3 per Windows è scaduto il 27 giugno 2016.

A partire dalla versione 3.4 HDInsight, Microsoft ha rilasciato HDInsight solo su hello del sistema operativo Linux. Di conseguenza, alcuni dei componenti di hello all'interno di HDInsight sono disponibili per Linux solo. Sono inclusi Apache cane, Kafka, Hive interattivo, Spark, le applicazioni, HDInsight e archivio Azure Data Lake come sistema di hello file primario. Nelle versioni future di HDInsight sono disponibili solo in hello del sistema operativo Linux. Per il sistema operativo Windows non saranno più rilasciate versioni di HDInsight. 

## <a name="faqs"></a>Domande frequenti

### <a name="what-is-hello-timeline-for-retiring-hdinsight-on-windows"></a>Che cos'è hello sequenza temporale per il ritiro di HDInsight in Windows?
31 luglio 2018 è hello data di ritiro per HDInsight in Windows. Se hello pianificata data del ritiro è diversa per l'area, riceverà una notifica separatamente. 

### <a name="what-is-hello-impact-of-retiring-hdinsight-on-windows-for-existing-customers"></a>Che cos'è l'impatto di hello del ritiro di HDInsight in Windows per i clienti esistenti?
Dopo che HDInsight per Windows è ritirato, non sarà possibile creare un nuovo cluster HDInsight su Windows o ridimensionarne uno esistente. Il supporto per HDInsight versione 3.3 è scaduto il 27 giugno 2016. Non sono pertanto disponibili supporto e correzioni di bug per HDInsight 3.3 o versioni precedenti. Nelle versioni future di HDInsight sono disponibili solo in hello del sistema operativo Linux. Per il sistema operativo Windows non saranno più rilasciate versioni di HDInsight.
 
### <a name="which-versions-of-hdinsight-on-windows-are-affected"></a>Quali versioni di HDInsight per Windows sono interessate?
Azure HDInsight versione 3.3 è hello l'ultima versione di HDInsight per Windows. Prima di HDInsight in Windows viene ritirata, tutte le finestre di HDInsight cluster 3.3 o versione precedente deve essere eseguita la migrazione tooHDInsight in Linux 3.5 o versione successiva. La migrazione del cluster di tooHDInsight in Linux consente tooretain hello possibilità toocreate nuovi cluster o ridimensionare cluster esistenti. 

### <a name="what-do-i-need-toodo"></a>Cosa devo toodo?
Eseguire la migrazione del cluster di HDInsight Linux tooa supportato i cluster HDInsight Windows prima di 31 luglio 2018. Per ulteriori hello [documento migrazione HDInsight](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). Per informazioni dettagliate sulle versioni di Azure HDInsight, vedere elenco hello di [le versioni supportate](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-component-versioning#supported-hdinsight-versions). 

### <a name="where-do-i-find-hello-cluster-os-type"></a>Dove trovare tipo di sistema operativo cluster hello?
Nel portale di Azure hello, andare toohello pagina Panoramica HDInsight Cluster e individuare **Cluster tipo** in **Essentials**. Nella pagina sono elencati i tipi di sistemi operativi cluster Hello. 

### <a name="i-cant-migrate-tooan-hdinsight-linux-cluster-by-july-31-2018-what-is-hello-impact-toomy-hdinsight-windows-cluster"></a>Impossibile eseguire la migrazione di tooan cluster HDInsight Linux 31 luglio 2018. Che cos'è l'impatto di hello toomy cluster HDInsight Windows?
Hello cluster HDInsight Windows viene eseguito come-è, ma non è possibile creare un nuovo cluster di HDInsight Windows o ridimensionare un cluster HDInsight Windows esistente. 

### <a name="my-cluster-has-a-net-dependency-how-do-i-resolve-this-dependency-on-linux"></a>Il cluster include una dipendenza .NET. Come si risolve questa dipendenza su Linux?
È possibile risolvere la dipendenza di cluster Linux usando hello [progetto Mono](http://www.mono-project.com/). Questa implementazione open source di .NET è disponibile per i cluster HDInsight su Linux. Per ulteriori hello [documento migrazione HDInsight](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). 

### <a name="im-a-new-customer-for-hdinsight-on-windows-how-can-i-create-an-hdinsight-windows-cluster"></a>Sono un nuovo cliente di HDInsight per Windows. Come è possibile creare un cluster HDInsight per Windows?
A partire dal 3 luglio 2017, solo i clienti esistenti di HDInsight per Windows possono creare nuovi cluster HDInsight per Windows. Nuovi clienti non è possibile creare un cluster di Windows di HDInsight nel portale di Azure hello mediante PowerShell o hello SDK. È consigliabile che i nuovi clienti creino un cluster HDInsight per Linux. I clienti esistenti possono creare i cluster di nuove finestre di HDInsight finché hello HDInsight in Windows data del ritiro. 

### <a name="is-there-a-pricing-impact-associated-with-moving-from-hdinsight-on-windows-toohdinsight-on-linux"></a>Si è verificato un impatto sui prezzi associato lo spostamento da HDInsight in Windows tooHDInsight in Linux?
No, prezzi hello è hello stesso per HDInsight su un sistema operativo. 

### <a name="what-are-hello-customer-advantages-associated-with-hello-move-tooonly-using-hdinsight-on-linux"></a>Quali sono i vantaggi di cliente hello associati hello Sposta tooonly tramite HDInsight su Linux?
* Più veloce time-to-market per le tecnologie Apri origine dati tramite hello servizio HDInsight
* Sono disponibili una community e un ecosistema di grandi dimensioni per il supporto
* Capacità tooexercise fase di sviluppo attivo da hello aprire community di origine per Hadoop e altre tecnologie di dati

### <a name="does-hdinsight-on-linux-provide-additional-functionality-beyond-what-is-available-in-hdinsight-on-windows"></a>HDInsight per Linux fornisce funzionalità aggiuntive oltre a quelle disponibili in HDInsight per Windows?
A partire dalla versione 3.4 HDInsight, Microsoft ha rilasciato HDInsight solo su hello del sistema operativo Linux. Di conseguenza, alcuni dei componenti di hello all'interno di HDInsight sono disponibili per Linux solo. Sono inclusi Apache cane, Kafka, Hive interattivo, Spark, le applicazioni, HDInsight e archivio Azure Data Lake come sistema di hello file primario. 

## <a name="service-level-agreement-for-hdinsight-cluster-versions"></a>Contratto di servizio per le versioni dei cluster HDInsight
Hello contratto di servizio (SLA) è definito in termini di un _finestra supporto_. finestra supporto Hello è hello periodo di tempo da una versione del cluster HDInsight è supportata da Microsoft il servizio supporto tecnico. Se la versione di hello presenta un _supportano la data di scadenza_ che ha superato, il cluster di HDInsight hello è all'esterno della finestra supporto hello. Per ulteriori informazioni sulle versioni supportate, vedere l'elenco di hello di [versioni cluster HDInsight](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). Data di scadenza Hello supporto per una versione X (dopo che è disponibile una versione più recente di X + 1) di HDInsight specificato viene calcolata come hello in seguito di:  

* La formula 1: Aggiungere data toohello 180 giorni quando è stata rilasciata la versione del cluster HDInsight hello X.
* Formula 2: Aggiungere data toohello 90 giorni quando versione del cluster HDInsight hello X + 1 è reso disponibile nel portale di Azure.

Hello _data del ritiro_ data hello dopo il quale non è possibile creare la versione del cluster hello in HDInsight. A partire dal 31 luglio 2017 non è possibile ridimensionare un cluster HDInsight dopo la data di ritiro. 

> [!NOTE]
> I cluster HDInsight Windows (incluse le versioni 2.1, 3.0, 3.1, 3.2 e 3.3) eseguire nella famiglia di sistemi operativi Guest Azure versione 4, che utilizza una versione a 64 bit di Windows Server 2012 R2 hello. Famiglia di sistemi operativi Guest Azure versione 4 supporta versioni di .NET Framework hello 4.0, 4.5, 4.5.1 e 4.5.2.

## <a name="hortonworks-release-notes-associated-with-hdinsight-versions"></a>Note sulla versione di Hortonworks associate alle versioni di HDInsight

sezione Hello collegamenti toorelease note per le distribuzioni di Hortonworks Data Platform hello e componenti di Apache che vengono utilizzati con HDInsight.
* Il cluster HDInsight versione 3.6 usa una distribuzione Hadoop basata su [Hortonworks Data Platform 2.6](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.0/bk_release-notes/content/ch_relnotes.html).
* Il cluster HDInsight versione 3.5 usa una distribuzione Hadoop basata su [Hortonworks Data Platform 2.5](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.5.0/bk_release-notes/content/ch_relnotes_v250.html). Versione del cluster HDInsight 3.5 è hello _predefinito_ cluster Hadoop che viene creato nel portale di Azure hello.
* Il cluster HDInsight versione 3.4 usa una distribuzione Hadoop basata su [Hortonworks Data Platform 2.4](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.4.0/bk_HDP_RelNotes/content/ch_relnotes_v240.html).
* Il cluster HDInsight versione 3.3 usa una distribuzione Hadoop basata su [Hortonworks Data Platform 2.3](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_HDP_RelNotes/content/ch_relnotes_v230.html).

  * [Note sulla versione di Apache Storm](https://storm.apache.org/2015/11/05/storm0100-released.html) sono disponibili nel sito Web Apache hello.
  * [Note sulla versione Apache Hive](https://issues.apache.org/jira/secure/ReleaseNote.jspa?version=12332384&styleName=Text&projectId=12310843) sono disponibili nel sito Web Apache hello.
* Il cluster HDInsight versione 3.2 usa una distribuzione Hadoop basata su [Hortonworks Data Platform 2.2][hdp-2-2].

  * Note sulla versione per componenti specifici di Apache sono disponibili come segue: [Hive 0.14](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310843&version=12326450), [Pig 0.14](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310730&version=12326954), [HBase 0.98.4](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310753&version=12326810), [Phoenix 4.2.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12315120&version=12327581), [M/R 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310941&version=12327180), [HDFS 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310942&version=12327181), [YARN 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12313722&version=12327197), [Common](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310240&version=12327179), [Tez 0.5.2](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12314426&version=12328742), [Ambari 2.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12312020&version=12327486), [Storm 0.9.3](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12314820&version=12327112) e [Oozie 4.1.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?version=12324960&projectId=12311620).
* Il cluster HDInsight versione 3.1 usa una distribuzione Hadoop basata su [Hortonworks Data Platform 2.1.7][hdp-2-1-7]. I cluster HDInsight 3.1 creati prima del 7 novembre 2014 sono basati su [Hortonworks Data Platform 2.1.1][hdp-2-1-1].
* Il cluster HDInsight versione 3.0 usa una distribuzione Hadoop basata su [Hortonworks Data Platform 2.0][hdp-2-0-8].
* Il cluster HDInsight versione 2.1 usa una distribuzione Hadoop basata su [Hortonworks Data Platform 1.3][hdp-1-3-0].
* Il cluster HDInsight versione 1.6 usa una distribuzione Hadoop basata su [Hortonworks Data Platform 1.1][hdp-1-1-0].

## <a name="hdinsight-standard-and-hdinsight-premium"></a>HDInsight Standard e HDInsight Premium

Azure HDInsight offre hello offerte di cloud di dati in due categorie: _Standard_ e _Premium_. Hello nella tabella seguente sono elencate le funzionalità disponibili _solo_ in HDInsight Premium. Funzionalità che non sono descritti in modo esplicito nella tabella hello sono disponibili in HDInsight Standard e Premium.

> [!NOTE]
> Hello HDInsight Premium offerta è attualmente in anteprima e disponibile solo per i cluster Linux.

| Funzionalità HDInsight Premium | Description |
| --- | --- |
| Cluster HDInsight aggiunti al dominio |Aggiungere i domini di Active Directory (Azure AD) tooAzure cluster HDInsight per la sicurezza a livello aziendale. In HDInsight Premium, è possibile configurare un elenco di dipendenti dalla propria organizzazione che è possibile eseguire l'autenticazione in Azure AD toolog nel cluster HDInsight tooan. salve enterprise è possibile configurare il controllo di accesso basato sui ruoli per la sicurezza Hive usando [cane Apache](http://hortonworks.com/apache/ranger/) e limitare i dati accesso toouse solo l'importo necessario. Infine, salve controllare dati cui che si accede da dipendenti e le modifiche tooaccess controllare i criteri, ottenendo un livello elevato di governance delle risorse aziendali. Per altre informazioni, vedere [Configure domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Configurare i cluster HDInsight aggiunti al dominio). |

### <a name="cluster-types-supported-in-hdinsight-premium"></a>Tipi di cluster supportati in HDInsight Premium
Hello nella tabella seguente sono elencati i tipi di cluster hello sono supportati in HDInsight Premium.

| Tipo di cluster | Standard | Premium (anteprima) |
| --- | --- | --- |
| Hadoop |Sì |Sì (solo HDInsight 3.6) |
| Spark |Sì |No |
| HBase |Sì |No |
| Storm |Sì |No |
| R Server |Sì |No |
| Interactive Hive (anteprima) |Sì |No |
| Kafka (anteprima) |Sì |No | 

### <a name="support-for-azure-data-lake-store-in-hdinsight-premium"></a>Supporto per Azure Data Lake Store in HDInsight Premium

I cluster HDInsight Premium non supportano l'utilizzo di Azure Data Lake Store come risorsa di archiviazione primaria. È comunque possibile usare Azure Data Lake Store come risorsa di archiviazione aggiuntiva con i cluster HDInsight Premium.

### <a name="pricing-and-sla"></a>Prezzi e contratto di servizio
Per informazioni su prezzi e contratto di servizio per HDInsight Premium, vedere [Prezzi di HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="default-node-configuration-and-virtual-machine-sizes-for-clusters"></a>Configurazione del nodo predefinito e dimensioni della macchina virtuale per i cluster
Hello seguenti dimensioni delle tabelle elenco hello predefinito macchine virtuali (VM) per i cluster HDInsight.

> [!IMPORTANT]
> Se si prevedono più di 32 nodi di lavoro in un cluster, è necessario selezionare una dimensione del nodo head con almeno 8 core e 14 GB di RAM.
> 
> 

* Tutte le aree supportate tranne Brasile meridionale e Giappone occidentale:

  | Tipo di cluster | Hadoop | HBase | Storm | Spark | R Server |
  | --- | --- | --- | --- | --- | --- |
  | Head: dimensioni VM predefinite |D3 v2 |D3 v2 |A3 |D12 v2 |D12 v2 |
  | Head: dimensioni VM consigliate |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |A3, A4, A5 |D12 v2, D13 v2, D14 v2 |D12 v2, D13 v2, D14 v2 |
  | Ruolo di lavoro: dimensioni VM predefinite |D3 v2 |D3 v2 |D3 v2 |Windows: D12 v2; Linux: D4 v2 |Windows: D12 v2; Linux: D4 v2 |
  | Ruolo di lavoro: dimensioni VM consigliate |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |Windows: D12 v2, D13 v2, D14 v2; Linux: D4 v2, D12 v2, D13 v2, D14 v2 |Windows: D12 v2, D13 v2, D14 v2; Linux: D4 v2, D12 v2, D13 v2, D14 v2 |
  | ZooKeeper: dimensioni VM predefinite | |A3 |A2 | | |
  | ZooKeeper: dimensioni VM consigliate | |A3, A4, A5 |A2, A3, A4 | | |
  | Edge: dimensioni VM predefinite | | | | |Windows: D12 v2; Linux: D4 v2 |
  | Edge: dimensioni VM consigliate | | | | |Windows: D12 v2, D13 v2, D14 v2; Linux: D4 v2, D12 v2, D13 v2, D14 v2 |
* Solo Brasile meridionale e Giappone occidentale (non sono disponibili dimensioni v2):

  | Tipo di cluster | Hadoop | HBase | Storm | Spark | R Server |
  | --- | --- | --- | --- | --- | --- |
  | Head: dimensioni VM predefinite |D3 |D3 |A3 |D12 |D12 |
  | Head: dimensioni VM consigliate |D3, D4, D12 |D3, D4, D12 |A3, A4, A5 |D12, D13, D14 |D12, D13, D14 |
  | Ruolo di lavoro: dimensioni VM predefinite |D3 |D3 |D3 |Windows: D12; Linux: D4 |Windows: D12; Linux: D4 |
  | Ruolo di lavoro: dimensioni VM consigliate |D3, D4, D12 |D3, D4, D12 |D3, D4, D12 |Windows: D12, D13, D14; Linux: D4, D12, D13, D14 |Windows: D12, D13, D14; Linux: D4, D12, D13, D14 |
  | ZooKeeper: dimensioni VM predefinite | |A2 |A2 | | |
  | ZooKeeper: dimensioni VM consigliate | |A2, A3, A4 |A2, A3, A4 | | |
  | Edge: dimensioni VM predefinite | | | | |Windows: D12; Linux: D4 |
  | Edge: dimensioni VM consigliate | | | | |Windows: D12, D13, D14; Linux: D4, D12, D13, D14 |

> [!NOTE]
> - HEAD è noto come *Nimbus* per hello elevato numero di cluster di tipo.
> - Lavoro è noto come *Supervisore* per hello elevato numero di cluster di tipo.
> - Lavoro è noto come *area* per hello HBase del tipo di cluster.

## <a name="next-steps"></a>Passaggi successivi
- [Configurazione del cluster per Hadoop, Spark e altre informazioni su HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
- [Lavorare da un computer Windows in Hadoop su HDInsight](hdinsight-hadoop-windows-tools.md)

[Supported HDInsight versions]:(#supported-hdinsight-versions)

[image-hdi-versioning-versionscreen]: ./media/hdinsight-component-versioning/hdi-versioning-version-screen.png

[wa-forums]: http://azure.microsoft.com/support/forums/

[connect-excel-with-hive-ODBC]: hdinsight-connect-excel-hive-ODBC-driver.md

[hdp-2-2]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.0/HDP_2.2.0_Release_Notes_20141202_version/index.html

[hdp-2-1-7]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html

[hdp-2-1-1]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.1/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.1.html

[hdp-2-0-8]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.8.0/bk_releasenotes_hdp_2.0/content/ch_relnotes-hdp2.0.8.0.html

[hdp-1-3-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-1.3.0/bk_releasenotes_hdp_1.x/content/ch_relnotes-hdp1.3.0_1.html

[hdp-1-1-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-Win-1.1/bk_releasenotes_HDP-Win/content/ch_relnotes-hdp-win-1.1.0_1.html

[ambari-docs]: https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md

[zookeeper]: http://zookeeper.apache.org/
