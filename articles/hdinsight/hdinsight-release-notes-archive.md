---
title: note sulla versione di aaaArchived - componenti Hadoop in HDInsight di Azure | Documenti Microsoft
description: Note sulla versione in archivio per le vecchie versioni dei componenti Hadoop per Azure HDInsight.
services: hdinsight
documentationcenter: 
editor: cgronlun
manager: jhubbard
author: nitinme
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 7a99c77f4557ca8c1dabe924cc67b2e0a134f8c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-archive-for-hadoop-components-on-azure-hdinsight"></a>Note sulla versione in archivio per i componenti Hadoop in Azure HDInsight

Questo articolo fornisce informazioni su hello **precedente** gli aggiornamenti di versione di Azure HDInsight. Per informazioni sulle versioni più recenti, vedere [Note sulla versione di HDInsight](hdinsight-release-notes.md).

> [!IMPORTANT]
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere l'[articolo sul controllo delle versioni di HDInsight](hdinsight-component-versioning.md).



## <a name="notes-for-08302016-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 30/08/2016
numeri di versione completo Hello per i cluster HDInsight basati su Linux distribuita con questa versione:

| HDI | Cluster versione HDI | HDP | Compilazione HDP | Compilazione Ambari |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.8268980 |2.2 |2.2.9.1-19 |2.2.1.12-4 |
| 3.3 |3.3.1000.0.8268980 |2.3 |2.3.3.1-25 |2.2.1.12-4 |
| 3.4 |3.4.1000.0.8269383 |2.4 |2.4.2.4-5 |2.2.1.12-4 |

numeri di versione completo Hello per i cluster HDInsight basati su Windows distribuita con questa versione:

| HDI | Cluster versione HDI | HDP | Compilazione HDP |
| --- | --- | --- | --- |
| 2.1 |2.1.10.1033.2559206 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.1033.2559206 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.1033.2559206 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.1033.2559206 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.1033.2559206 |2.3 |2.3.3.1-25 |


## <a name="08172016---release-of-r-server-on-hdinsight"></a>17/08/2016: rilascio di R Server in HDInsight
* R Server 8.0.5 - principalmente una versione di correzione di bug. Vedere hello [le note sulla versione di R Server](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes) per altre informazioni.
* Pacchetto di Azure ml nel nodo del bordo hello - [il pacchetto R](https://cran.r-project.org/web/packages/AzureML/vignettes/getting_started.html) toobe modelli R Abilita pubblicato e consumato come servizio web di Azure ML.  Vedere hello ["Rendere operativo un modello"](hdinsight-hadoop-r-server-overview.md#operationalize-a-model) sezione del nostro ["Panoramica di R Server su HDInsight"](hdinsight-hadoop-r-server-overview.md) articolo per altre informazioni.
* Dipendenze di Linux di hello [le prime 100 pacchetti R più diffusi](https://github.com/metacran/cranlogs) -queste dipendenze di pacchetto Linux sono ora pre-installate.
* Opzione toouse hello CRAN repository quando si aggiungono R pacchetti toohello nodi di dati. Per altre informazioni, vedere ["Introduzione all'uso di R Server in HDInsight"](hdinsight-hadoop-r-server-get-started.md).
* Affidabilità migliorate hello di provisioning del Server di R quando vengono creati i cluster.

## <a name="notes-for-08012016-release-of-hdinsight"></a>Note sulla versione di HDInsight rilasciata in data 01/08/2016
numeri di versione completo Hello per i cluster HDInsight basati su Linux distribuita con questa versione:

| HDI | Cluster versione HDI | HDP | Compilazione HDP | Compilazione Ambari |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.8028416 |2.2 |2.2.9.1-19 |2.2.1.12-4 |
| 3.3 |3.3.1000.0.8028416 |2.3 |2.3.3.1-25 |2.2.1.12-4 |
| 3.4 |3.4.1000.0.8053402 |2.4 |2.4.2.4-5 |2.2.1.12-4 |

numeri di versione completo Hello per i cluster HDInsight basati su Windows distribuita con questa versione:

| HDI | Cluster versione HDI | HDP | Compilazione HDP |
| --- | --- | --- | --- |
| 2.1 |2.1.10.1005.2488842 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.1005.2488842 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.1005.2488842 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.1005.2488842 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.1005.2488842 |2.3 |2.3.3.1-25 |

Questa versione contiene hello seguenti aggiornamenti:

| Titolo | Descrizione | Area interessata (ad esempio servizio, componente o SDK) | Tipo di cluster (ad esempio Spark, Hadoop, HBase o Storm) | JIRA (se applicabile) |
| --- | --- | --- | --- | --- |
| Le modifiche tooHDInsight 3.4 cluster |vengono modificati i valori predefiniti di Hello per le configurazioni seguenti hive per migliorare le prestazioni <ul><li>`hive.vectorized.execution.reduce.enabled=true`</li><li>`hive.tez.min.partition.factor=1f`</li><li>`hive.tez.max.partition.factor=3f`</li><li>`tez.shuffle-vertex-manager.min-src-fraction=0.9`</li><li>`tez.shuffle-vertex-manager.max-src-fraction=0.95`</li><li>`tez.runtime.shuffle.connect.timeout= 30000`</li></ul> |Service |Tutti |N/D |
| In questa versione sono incluse le correzioni seguenti |HIVE-13632, HIVE-12897, HIVE-12907, HIVE-12908, HIVE-12988, HIVE-13510, HIVE-13572, HIVE-13716, HIVE-13726, HIVE-12505, HIVE-13632, HIVE-13661, HIVE-13705, HIVE-13743, HIVE-13810, HIVE-13857, HIVE-13902, HIVE-13911, HIVE-13933 |Service |Tutti |N/D |

## <a name="notes-for-07142016-release-of-hdinsight"></a>Note sulla versione di HDInsight rilasciata il 14/07/2016
numeri di versione completo Hello per i cluster HDInsight basati su Linux distribuita con questa versione:

| HDI | Cluster versione HDI | HDP | Compilazione HDP | Compilazione Ambari |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.7932505 |2.2 |2.2.9.1-11 |2.2.1.12-2 |
| 3.3 |3.3.1000.0.7932505 |2.3 |2.3.3.1-18 |2.2.1.12-2 |
| 3.4 |3.4.1000.0.7933003 |2.4 |2.4.2.0 |2.2.1.12-2 |

numeri di versione completo Hello per i cluster HDInsight basati su Windows distribuita con questa versione:

| HDI | Cluster versione HDI | HDP | Compilazione HDP |
| --- | --- | --- | --- |
| 2.1 |2.1.10.989.2441725 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.989.2441725 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.989.2441725 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.989.2441725 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.989.2441725 |2.3 |2.3.3.1-21 |

## <a name="notes-for-07072016-release-of-hdinsight"></a>Note sulla versione di HDInsight rilasciata il 07/07/2016
numeri di versione completo Hello per i cluster HDInsight basati su Linux distribuita con questa versione:

| HDI | Cluster versione HDI | HDP | Compilazione HDP |
| --- | --- | --- | --- |
| 3.2 |3.2.1000.0.7864996 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.1000.0.7864996 |2.3 |2.3.3.1-18 |
| 3.4 |3.4.1000.0.7861906 |2.4 |2.4.2.0 |

numeri di versione completo Hello per i cluster HDInsight basati su Windows distribuita con questa versione:

| HDI | Cluster versione HDI | HDP | Compilazione HDP |
| --- | --- | --- | --- |
| 2.1 |2.1.10.977.2413853 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.977.2413853 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.977.2413853 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.977.2413853 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.977.2413853 |2.3 |2.3.3.1-21 |

Questa versione contiene hello seguenti aggiornamenti:

| Titolo | Descrizione | Area interessata (ad esempio servizio, componente o SDK) | Tipo di cluster (ad esempio Spark, Hadoop, HBase o Storm) | JIRA (se applicabile) |
| --- | --- | --- | --- | --- |
| [Strumenti di HDInsight per IntelliJ](hdinsight-apache-spark-intellij-tool-plugin.md) |Il plug-in IntelliJ IDEA per i cluster HDInsight Spark è ora integrato nel toolkit di Azure per IntelliJ. Supporta v2.9.1 Azure SDK, SDK più recente di Java e include tutte le funzionalità di hello dal hello autonomo HDInsight Plugin per IntelliJ. |Strumenti |Spark |N/D |
| [Strumenti di HDInsight per Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md) |Il toolkit di Azure per Eclipse supporta ora i cluster HDInsight Spark e Consente di hello seguenti caratteristiche: <ul><li>Creare e scrivere facilmente un'applicazione Spark in Scala e Java con l'eccellente supporto per la creazione per IntelliSense, la formattazione automatica, il controllo degli errori e così via.</li><li>Testare l'applicazione Spark hello in locale.</li><li>Cluster di Spark tooHDInsight processi di inviare e recuperare risultati hello.</li><li>Accedere in tooAzure e accedere a tutti i cluster di Spark hello associati alle sottoscrizioni di Azure.</li><li>Passare tutte le risorse di archiviazione associata hello del cluster HDInsight Spark.</li></ul> |Strumenti |Spark |N/D |

A partire da questa versione, è stato modificato criteri applicazione di patch del sistema operativo guest di hello per i cluster HDInsight basati su Linux. obiettivo di Hello del nuovo criterio di hello è toosignificantly ridurre il numero di riavvii di hello toopatching scadenza. Hello nuovi criteri patch macchine virtuali (VM in Linux) cluster ogni lunedì o giovedì a partire da Mezzanotte ora UTC in un termineranno tra i nodi del cluster specificato. Tuttavia, tutte le VM determinata Riavvia solo al massimo una volta ogni 30 giorni a causa del sistema operativo tooguest l'applicazione di patch. Inoltre, il primo riavvio hello per un cluster appena creato non si verifica prima di 30 giorni dalla data di creazione di cluster hello.

> [!NOTE]
> Queste modifiche si applicano solo toonewly creato i cluster di, uguale o maggiore di questa versione.
>
>

## <a name="notes-for-06062016-release-of-hdinsight"></a>Note sulla versione di HDInsight rilasciata il 06/06/2016
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

| HDP | Versione HDI | Versione Spark | Numero di compilazione Ambari | Numero di compilazione HDP |
| --- | --- | --- | --- | --- |
| 2.3 |3.3.1000.0.7702215 |1.5.2 |2.2.1.8-2 |2.3.3.1-18 |
| 2.4 |3.4.1000.0.7702224 |1.6.1 |2.2.1.8-2 |2.4.2.0 |

Questa versione contiene hello seguenti aggiornamenti:

| Titolo | Descrizione | Area interessata (ad esempio servizio, componente o SDK) | Tipo di cluster (ad esempio Spark, Hadoop, HBase o Storm) | JIRA (se applicabile) |
| --- | --- | --- | --- | --- |
| Spark in HDInsight è disponibile a livello generale |Questa versione offre miglioramenti in disponibilità, scalabilità e la produttività tooopen origine Apache Spark in HDInsight. <ul><li>Contratto di servizio per la disponibilità del 99,9% che lo rende adatto a carichi di lavoro aziendali complessi.</li><li>Livello di archiviazione scalabile con Azure Data Lake Store.</li><li>Strumenti di produttività per ogni fase dell'esplorazione e dello sviluppo dei dati. I Jupyter Notebook con kernel Spark personalizzato consentono l'esplorazione interattiva dei dati, l'integrazione con dashboard BI come Power BI, Tableau e Qlik è perfetta per la condivisione rapida dei dati e il reporting continuo, il plug-in IntelliJ è un'opzione affidabile per lo sviluppo e il debug a lungo termine di elementi di codice.</li></ul> |Service |Spark |N/D |
| Strumenti di HDInsight per IntelliJ |Questo è un plug-in IntelliJ IDEA per cluster HDInsight Spark. Consente di hello seguenti caratteristiche:<ul><li>Creare e scrivere facilmente un'applicazione Spark in Scala e Java con l'eccellente supporto per la creazione per IntelliSense, la formattazione automatica, il controllo degli errori e così via.</li><li>Testare l'applicazione Spark hello in locale.</li><li>Cluster di Spark tooHDInsight processi di inviare e recuperare risultati hello.</li><li>Accedere in tooAzure e accedere a tutti i cluster di Spark hello associati alle sottoscrizioni di Azure.</li><li>Passare tutte le risorse di archiviazione associata hello del cluster HDInsight Spark.</li><li>Passare tutte hello processi Cronologia processo informazioni e per il cluster HDInsight Spark.</li><li>Eseguire il debug di processi Spark in modalità remota dal computer desktop.</li></ul> |Strumenti |Spark |N/D |

## <a name="notes-for-05132016-release-of-hdinsight"></a>Note sulla versione di HDInsight rilasciata il 13/05/2016
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight (Windows) 2.1.10.875.2159884 (HDP 1.3.12.0-01795 - non modificato)
* HDInsight (Windows) 3.0.6.875.2159884 (HDP 2.0.13.0-2117 - non modificato)
* HDInsight (Windows) 3.1.4.922.2266903 (HDP 2.1.15.0-2374 - non modificato)
* HDInsight (Windows) 3.2.7.922.2266903 (HDP 2.2.9.1-11)
* HDInsight (Windows) 3.3.0.922.2266903 (HDP 2.3.3.1-18)
* HDInsight (Linux) 3.2.1000.0.7565644 (HDP 2.2.9.1-11)
* HDInsight (Linux) 3.3.1000.0.7565644 (HDP 2.3.3.1-18)
* HDInsight (Linux) 3.4.1000.0.7548380 (HDP 2.4.2.0)

Questa versione contiene hello seguenti aggiornamenti:

| Titolo | Descrizione | Area interessata (ad esempio servizio, componente o SDK) | Tipo di cluster (ad esempio Spark, Hadoop, HBase o Storm) | JIRA (se applicabile) |
| --- | --- | --- | --- | --- |
| Aggiornamento della versione di Spark e altre correzioni di bug |Questa versione degli aggiornamenti di versione di hello Spark in HDInsight cluster too1.6.1 e corregge altri bug |Service |Spark |N/D |

## <a name="notes-for-04112016-release-of-hdinsight"></a>Note sulla versione di HDInsight dell'11/04/2016
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight (Windows) 2.1.10.889.2191206 (HDP 1.3.12.0-01795 - non modificato)
* HDInsight (Windows) 3.0.6.889.2191206 (HDP 2.0.13.0-2117 - non modificato)
* HDInsight (Windows) 3.1.4.889.2191206 (HDP 2.1.15.0-2374 - non modificato)
* HDInsight (Windows) 3.2.7.889.2191206 (HDP 2.2.9.1-10)
* HDInsight (Windows) 3.3.0.889.2191206 (HDP 2.3.3.1-16 -non modificato)
* HDInsight (Linux) 3.2.1000.0.7339916 (HDP 2.2.9.1-10)
* HDInsight (Linux) 3.3.1000.0.7339916 (HDP 2.3.3.1-16)
* HDInsight (Linux) 3.4.1000.0.7338911 (HDP 2.4.1.1-3)
* SDK 1.5.8

Questa versione contiene hello seguenti aggiornamenti:

| Titolo | Descrizione | Area interessata (ad esempio servizio, componente o SDK) | Tipo di cluster (ad esempio Hadoop, HBase o Storm) | JIRA (se applicabile) |
| --- | --- | --- | --- | --- |
| Problemi di aggiornamento metastore personalizzato per HDI 3.4 |La creazione del cluster non viene eseguita correttamente se si usa un metastore personalizzato già usato in una versione precedente di un altro cluster HDInsight. In questo stato a causa di errore di script aggiornamento tooan che ora è stato risolto. |Creazione del cluster |Tutti |N/D |
| Ripristino a seguito dell'arresto anomalo del sistema Livy |Fornisce resilienza dello stato del processo per qualsiasi processo inviato tramite Livy |Affidabilità |Spark su Linux |N/D |
| Contenuto Jupyter a disponibilità elevata |Fornisce hello possibilità toosave e carico Jupyter notebook contenuto tooand dall'account di archiviazione hello associato hello cluster. Per altre informazioni, vedere [Kernel disponibili per i Jupyter Notebook](hdinsight-apache-spark-jupyter-notebook-kernels.md). |Notebook |Spark su Linux |N/D  |
| Rimozione di hiveContext nei notebook Jupyter |Usare l'oggetto `%%sql` invece di `%%hive`. SqlContext è toohiveContext equivalente. Per altre informazioni, vedere [Kernel disponibili per i Jupyter Notebook](hdinsight-apache-spark-jupyter-notebook-kernels.md) |Notebook |Cluster Spark su Linux |N/D |
| Rimozione di versioni precedenti di Spark |Versione 1.3.1 Spark è stato rimosso dal servizio hello 5/31 |Service |Cluster Spark in Windows |N/D |

## <a name="notes-for-03292016-release-of-hdinsight"></a>Note sulla versione di HDInsight rilasciata il 29/03/2016
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight (Windows) 2.1.10.875.2159884 (HDP 1.3.12.0-01795 - non modificato)
* HDInsight (Windows) 3.0.6.875.2159884 (HDP 2.0.13.0-2117 - non modificato)
* HDInsight (Windows) 3.1.4.875.2159884 (HDP 2.1.15.0-2374 - non modificato)
* HDInsight (Windows) 3.2.7.875.2159884 (HDP 2.2.9.1-7 - non modificato)
* HDInsight (Windows) 3.3.0.875.2159884 (HDP 2.3.3.1-16)
* HDInsight (Linux) 3.2.1000.0.7193255 (HDP 2.2.9.1-8 - non modificato)
* HDInsight (Linux) 3.3.1000.0.7193255 (HDP 2.3.3.1-7 - non modificato)
* HDInsight (Linux) 3.4.1000.0.7195842 (HDP 2.4.1.0-327)
* SDK 1.5.8

Questa versione contiene hello seguenti aggiornamenti:

| Titolo | Descrizione | Area interessata (ad esempio servizio, componente o SDK) | Tipo di cluster (ad esempio Hadoop, HBase o Storm) | JIRA (se applicabile) |
| --- | --- | --- | --- | --- |
| È stata aggiunta la versione 3.4 di HDInsight e sono state aggiornate le versioni HDP di tutti i cluster di HDInsight |Con questa versione, è stata aggiunta la versione 3.4 di HDInsight (basata su HDP 2.4) e sono state aggiornate anche le altre versioni di HDP. Le note sulla versione di HDP 2.4 sono disponibili [qui](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.4.0/bk_HDP_RelNotes/content/ch_relnotes_v240.html) e altre informazioni sulle versioni di HDInsight sono disponibili [qui](hdinsight-component-versioning.md). |Service |Tutti i cluster Linux |N/D |
| HDInsight Premium |HDInsight è ora disponibile in due categorie: Standard e Premium. Attualmente HDInsight Premium è disponibile in anteprima e solo per i cluster Hadoop e Spark su Linux. Per altre informazioni, vedere [qui](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium). |Service |Hadoop e Spark su Linux |N/D |
| Microsoft R Server |HDInsight Premium mette a disposizione Microsoft R Server, che può essere incluso con i cluster Spark e Hadoop su Linux. Per altre informazioni, vedere [Panoramica di R Server su HDInsight (anteprima)](hdinsight-hadoop-r-server-overview.md). |Service |Hadoop e Spark su Linux |N/D |
| Spark 1.6.0 |I cluster HDInsight 3.4 ora includono Spark 1.6.0 |Service |Cluster Spark su Linux |N/D |
| Miglioramenti del notebook Jupyter |I notebook Jupyter disponibili con cluster Spark ora offrono kernel Spark supplementari. Includono inoltre miglioramenti quali utilizzo di %%magic, la visualizzazione automatica e l'integrazione con le librerie di visualizzazione Python (come matplotlib). Per altre informazioni, vedere [Kernel disponibili per i Jupyter Notebook](hdinsight-apache-spark-jupyter-notebook-kernels.md). |Service |Cluster Spark su Linux |N/D |

## <a name="notes-for-03222016-release-of-hdinsight"></a>Note sulla versione di HDInsight rilasciata il 22/03/2016
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight (Windows) 2.1.10.875.2159884 (HDP 1.3.12.0-01795 - non modificato)
* HDInsight (Windows) 3.0.6.875.2159884 (HDP 2.0.13.0-2117 - non modificato)
* HDInsight (Windows) 3.1.4.875.2159884 (HDP 2.1.15.0-2374 - non modificato)
* HDInsight (Windows) 3.2.7.875.2159884 (HDP 2.2.9.1-7 - non modificato)
* HDInsight (Windows) 3.3.0.875.2159884 (HDP 2.3.3.1-16)
* HDInsight (Linux) 3.2.1000.0.7193255 (HDP 2.2.9.1-8 - non modificato)
* HDInsight (Linux) 3.3.1000.0.7193255 (HDP 2.3.3.1-7 - non modificato)
* SDK 1.5.8

Questa versione contiene hello seguenti aggiornamenti:

| Titolo | Descrizione | Area interessata (ad esempio servizio, componente o SDK) | Tipo di cluster (ad esempio Hadoop, HBase o Storm) | JIRA (se applicabile) |
| --- | --- | --- | --- | --- |
| Versioni aggiornate di HDInsight per tutti i cluster HDInsight |Con questo rilascio sono state aggiornate le versioni di HDInsight per tutti i cluster HDInsight |Service |Tutti |N/D |

## <a name="notes-for-03102016-release-of-hdinsight"></a>Note sulla versione di HDInsight rilasciata il 10/03/2016
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight (Windows) 2.1.10.859.2123216 (HDP 1.3.12.0-01795 - non modificato)
* HDInsight (Windows) 3.0.6.859.2123216 (HDP 2.0.13.0-2117 - non modificato)
* HDInsight (Windows) 3.1.4.859.2123216 (HDP 2.1.15.0-2374 - non modificato)
* HDInsight (Windows) 3.2.7.859.2123216 (HDP 2.2.9.1-7)
* HDInsight (Windows) 3.3.0.859.2123216 (HDP 2.3.3.1-5 - non modificato)
* HDInsight (Linux) 3.2.1000.7076817 (HDP 2.2.9.1-8)
* HDInsight (Linux) 3.3.1000.7076817 (HDP 2.3.3.1-7)
* SDK 1.5.8

Questa versione contiene hello seguenti aggiornamenti:

| Titolo | Descrizione | Area interessata (ad esempio servizio, componente o SDK) | Tipo di cluster (ad esempio Hadoop, HBase o Storm) | JIRA (se applicabile) |
| --- | --- | --- | --- | --- |
| Versioni aggiornate di HDInsight per tutti i cluster HDInsight |Con questo rilascio sono state aggiornate le versioni di HDInsight per tutti i cluster HDInsight |Service |Tutti |N/D |

## <a name="notes-for-01272016-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 27/01/2016
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight (Windows) 2.1.10.817.2028315 (HDP 1.3.12.0-01795 - non modificato)
* HDInsight (Windows) 3.0.6.817.2028315 (HDP 2.0.13.0-2117 - non modificato)
* HDInsight (Windows) 3.1.4.817.2028315 (HDP 2.1.15.0-2374 - non modificato)
* HDInsight (Windows) 3.2.7.817.2028315 (HDP 2.2.9.1-1)
* HDInsight (Windows) 3.3.0.817.2028315 (HDP 2.3.3.1-5 - non modificato)
* HDInsight (Linux) 3.2.1000.4072335 (HDP 2.2.9.1-1)
* HDInsight (Linux) 3.3.1000.4072335 (HDP 2.3.3.1-1)
* SDK 1.5.8

Questa versione contiene hello seguenti aggiornamenti:

| Titolo | Descrizione | Area interessata (ad esempio servizio, componente o SDK) | Tipo di cluster (ad esempio Hadoop, HBase o Storm) | JIRA (se applicabile) |
| --- | --- | --- | --- | --- |
| Versioni aggiornate di HDInsight per tutti i cluster HDInsight |Con questo rilascio sono state aggiornate le versioni di HDInsight per tutti i cluster HDInsight |Service |Tutti |N/D |

## <a name="notes-for-12022015-release-of-hdinsight"></a>Note sulla versione di HDInsight rilasciata il 02/12/2015
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight (Windows) 2.1.10.763.1931434 (HDP 1.3.12.0-01795 - non modificato)
* HDInsight (Windows) 3.0.6.763.1931434 (HDP 2.0.13.0-2117 - non modificato)
* HDInsight (Windows) 3.1.4.763.1931434 (HDP 2.1.15.0-2374 - non modificato)
* HDInsight (Windows) 3.2.7.763.1931434 (HDP 2.2.7.1-34 - non modificato)
* HDInsight (Windows) 3.3.1000.0 (HDP 2.3.3.1-5)
* HDInsight (Linux) 3.2.1000.0.6392801 (HDP 2.2.7.1-34 - non modificato)
* HDInsight (Linux) 3.3.1000.0 (HDP 2.3.3.0-3039)
* SDK 1.5.8

Questa versione contiene hello seguenti aggiornamenti:

| Titolo | Descrizione | Area interessata (ad esempio servizio, componente o SDK) | Tipo di cluster (ad esempio Hadoop, HBase o Storm) | JIRA (se applicabile) |
| --- | --- | --- | --- | --- |
| È stata aggiunta la versione 3.3 di HDInsight e sono state aggiornate le versioni HDP di tutti i cluster di HDInsight |Con questa versione, è stata aggiunta la versione 3.3 di HDInsight (basata su HDP 2.3) e sono state aggiornate anche le altre versioni di HDP. Le note sulla versione di HDP 2.3 sono disponibili [qui](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_HDP_RelNotes/content/ch_relnotes_v230.html) e altre informazioni sulle versioni di HDInsight sono disponibili [qui](hdinsight-component-versioning.md). |Service |Tutti |N/D |

## <a name="notes-for-11302015-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 30/11/2015
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight (Windows) 2.1.10.757.1923908 (HDP 1.3.12.0-01795 - non modificato)
* HDInsight (Windows) 3.0.6.757.1923908 (HDP 2.0.13.0-2117 - non modificato)
* HDInsight (Windows) 3.1.4.757.1923908 (HDP 2.1.15.0-2374 - non modificato)
* HDInsight (Windows) 3.2.7.757.1923908 (HDP 2.2.7.1-34)
* HDInsight (Linux) 3.2.1000.0.6392801 (HDP 2.2.7.1-34)
* SDK 1.5.8

Questa versione contiene hello seguenti aggiornamenti:

| Titolo | Descrizione | Area interessata (ad esempio servizio, componente o SDK) | Tipo di cluster (ad esempio Hadoop, HBase o Storm) | JIRA (se applicabile) |
| --- | --- | --- | --- | --- |
| Versioni aggiornate di HDInsight per tutti i cluster HDInsight e le versioni HDP per i cluster HDInsight 3.2 (Windows e Linux) |Con questa versione, le versioni di HDInsight e HDP sono state aggiornate |Service |Tutti |N/D |

## <a name="notes-for-10272015-release-of-hdinsight"></a>Note sulla versione di HDInsight rilasciata il 27/10/2015
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight (Windows) 2.1.10.726.1866228 (HDP 1.3.12.0-01795 - non modificato)
* HDInsight (Windows) 3.0.6.726.1866228  (HDP 2.0.13.0-2117 - non modificato)
* HDInsight (Windows) 3.1.4.726.1866228 (HDP 2.1.15.0-2374 - non modificato)
* HDInsight (Windows) 3.2.7.726.1866228  (HDP 2.2.7.1-33)
* HDInsight (Linux) 3.2.1000.0.6035701 (HDP 2.2.7.1-33)
* SDK 1.5.8

Questa versione contiene hello seguenti aggiornamenti:

| Titolo | Descrizione | Area interessata (ad esempio servizio, componente o SDK) | Tipo di cluster (ad esempio Hadoop, HBase o Storm) | JIRA (se applicabile) |
| --- | --- | --- | --- | --- |
| Versioni di HDInsight aggiornate per tutti i cluster di HDInsight (Windows e Linux) |Con questa versione, le versioni di HDInsight e HDP sono state aggiornate |Service |Tutti |N/D |
| Jupyter corretto per i cluster di Windows Spark con cluster in lettere maiuscole |I cluster che contiene i nomi DNS specificati in lettere maiuscole presenta problemi con i notebook Jupyter scadenza tooan origine richiesta controllo. correzione di Hello è toochange hello nome DNS case toolower di configurazione del server Jupyter. |Service |HDInsight Spark (Windows) |N/D |

## <a name="notes-for-10202015-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 20/10/2015
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight     2.1.10.716.1846990 (Windows)     (HDP 1.3.12.0-01795 - non modificato)
* HDInsight 3.0.6.716.1846990 (Windows) (HDP 2.0.13.0-2117 - non modificato)
* HDInsight 3.1.4.716.1846990 (Windows) (HDP 2.1.16.0-2374)
* HDInsight 3.2.7.716.1846990 (Windows) (HDP 2.2.7.1-0004)
* HDInsight 3.2.1000.0.5930166 (Linux) (HDP 2.2.7.1-0004)
* SDK 1.5.8

Questa versione contiene hello seguenti aggiornamenti:

| Titolo | Descrizione | Area interessata (ad esempio servizio, componente o SDK) | Tipo di cluster (ad esempio Hadoop, HBase o Storm) | JIRA (se applicabile) |
| --- | --- | --- | --- | --- |
| Predefinito tooHDP versione modificata HDP 2.2 |versione di Hello predefinita per i cluster di Windows di HDInsight è modificato tooHDP 2.2. HDInsight versione 3.2 (HDP 2.2) è disponibile a livello generale dal mese di febbraio 2015. Questa modifica consente di capovolgere solo versione di hello predefinita cluster, quando una selezione esplicita non è stata effettuata durante il provisioning del cluster di hello utilizzando hello portale di Azure, i cmdlet di PowerShell o hello SDK. |Service |Tutti |N/D |
| Modifiche al formato dei nomi di macchina virtuale per la distribuzione di più cluster HDInsight basati su Linux in un'unica rete virtuale |In questa versione è stato aggiunto il supporto per la distribuzione di più cluster HDInsight basati su Linux in un'unica rete virtuale. Come parte dell'aggiornamento, il formato di hello di nomi di macchina virtuale in cluster hello è stato modificato dal nodo head\*, workernode\* e zookeepernode\* toohn\*, giù\*, zk e\* rispettivamente. Non è un tootake consigliata una dipendenza diretta in formato hello dei nomi di macchina virtuale, poiché si tratta di toochange soggetto. Utilizzare "hostname -f" nel computer locale hello o un elenco di hello toodetermine Ambari APIs di host e il mapping di hello di toohosts componenti. Altre informazioni sono disponibili agli indirizzi [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md) e [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md). |Service |Cluster HDInsight basati su Linux |N/D |
| Modifiche di configurazione |Per i cluster HDInsight 3.1, è ora abilitato hello seguenti configurazioni: <ul><li>tez.yarn.ats.enabled e yarn.log.server.url. In questo modo hello Server di applicazione della sequenza temporale e hello Log server toobe in grado di tooserve i registri.</li></ul>Per i cluster HDInsight 3.2, è stato modificato hello seguenti configurazioni: <ul><li>MapReduce.fileoutputcommitter.Algorithm.Version è stato impostato too2. In questo modo l'utilizzo di hello V2 versione di hello FileOutputCommitter.</li></ul> |Service |Tutti |N/D |

## <a name="notes-for-09092015-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 09/09/2015
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight     2.1.10.675.1768697 (HDP 1.3.12.0-01795 - non modificato)
* HDInsight     3.0.6.675.1768697  (HDP 2.0.13.0-2117 - non modificato)
* HDInsight     3.1.4.675.1768697  (HDP 2.1.15.0-2334 - non modificato)
* HDInsight 3.2.6.675.1768697 (HDP 2.2.6.1-0012 - non modificato)
* SDK 1.5.8

Questa versione contiene hello seguenti aggiornamenti:

| Titolo | Descrizione | Area interessata (ad esempio servizio, componente o SDK) | Tipo di cluster (ad esempio Hadoop, HBase o Storm) | JIRA (se applicabile) |
| --- | --- | --- | --- | --- |
| Versioni aggiornate di HDInsight per tutti i cluster HDInsight |Con questa versione le versioni di HDInsight sono state aggiornate |Service |Tutti |N/D |

## <a name="notes-for-07312015-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 31/07/2015
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight     2.1.10.640.1695824 (HDP 1.3.12.0-01795 - non modificato)
* HDInsight     3.0.6.640.1695824  (HDP 2.0.13.0-2117 - non modificato)
* HDInsight     3.1.4.640.1695824  (HDP 2.1.15.0-2334 - non modificato)
* HDInsight 3.2.6.640.1695824 (HDP 2.2.6.1-0012 - non modificato)
* SDK 1.5.8

Questa versione contiene hello seguenti aggiornamenti:

| Titolo | Descrizione | Area interessata (ad esempio servizio, componente o SDK) | Tipo di cluster (ad esempio Hadoop, HBase o Storm) | JIRA (se applicabile) |
| --- | --- | --- | --- | --- |
| Correggere il flusso di lavoro di ricreazione dell'immagine del nodo del cluster Spark |Correzione di un bug che causava Spark i nodi del cluster toonot ripristinare dopo la ricreazione dell'immagine |Service |Spark |N/D |

## <a name="notes-for-07312015-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 31/07/2015
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight     2.1.10.635.1684502 (HDP 1.3.12.0-01795 - non modificato)
* HDInsight     3.0.6.635.1684502  (HDP 2.0.13.0-2117 - non modificato)
* HDInsight     3.1.4.635.1684502  (HDP 2.1.15.0-2334 - non modificato)
* HDInsight 3.2.6.635.1684502 (HDP 2.2.6.1-0012 - non modificato)
* SDK 1.5.8

Questa versione contiene hello seguenti aggiornamenti:

| Titolo | Descrizione | Area interessata (ad esempio servizio, componente o SDK) | Tipo di cluster (ad esempio Hadoop, HBase o Storm) | JIRA (se applicabile) |
| --- | --- | --- | --- | --- |
| Versioni aggiornate di HDInsight per tutti i cluster HDInsight |Con questa versione le versioni di HDInsight sono state aggiornate |Service |Tutti |N/D |

## <a name="notes-for-07072015-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 07/07/2015
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight 2.1.10.610.1630216 (HDP 1.3.12.0-01795 - non modificato)
* HDInsight 3.0.6.610.1630216 (HDP 2.0.13.0-2117 - non modificato)
* HDInsight 3.1.4.610.1630216 (HDP 2.1.15.0-2334 - non modificato)
* HDInsight 3.2.4.610.1630216 (HDP 2.2.6.1-0012)
* SDK 1.5.8

Questa versione contiene hello seguenti aggiornamenti:

| Titolo | Descrizione | Area interessata (ad esempio servizio, componente o SDK) | Tipo di cluster (ad esempio Hadoop, HBase o Storm) | JIRA (se applicabile) |
| --- | --- | --- | --- | --- |
| Versioni aggiornate di HDP per i cluster HDInsight 3.2 |Con questa versione HDInsight 3.2 distribuisce HDP 2.2.6.1-0012 |Service |Tutti |N/D |

## <a name="notes-for-06262015-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 26/06/2015
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight 2.1.10.601.1610731 (HDP 1.3.12.0-01795 - non modificato)
* HDInsight 3.0.6.601.1610731 (HDP 2.0.13.0-2117 - non modificato)
* HDInsight 3.1.4.601.1610731 (HDP 2.1.15.0-2334 - non modificato)
* HDInsight 3.2.4.601.1610731 (HDP 2.2.6.1-0011)
* SDK 1.5.8

Questa versione contiene hello seguenti aggiornamenti:

<table border="1">
<tr>
<th>Titolo</th>
<th>Descrizione</th>
<th>Area interessata (ad esempio servizio, componente o SDK)</p></th>
<th>Tipo di cluster (ad esempio Hadoop, HBase o Storm)</th>
<th>JIRA (se applicabile)</th>
</tr>
<tr>
<td>Versioni aggiornate di HDP per i cluster HDInsight 3.2</td>
<td>Con questa versione HDInsight 3.2 distribuisce HDP 2.2.6.1</td>
<td>Service</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-06182015-release-of-hdinsight"></a>Note sulla versione di HDInsight rilasciata il 18/06/2015
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight 2.1.10.596.1601657 (HDP 1.3.12.0-01795 - non modificato)
* HDInsight 3.0.6.596.1601657 (HDP 2.0.13.0-2117 - non modificato)
* HDInsight 3.1.4.596.1601657 (HDP 2.1.15.0-2334)
* HDInsight 3.2.4.596.1601657 (HDP 2.2.6.1-0002)
* SDK 1.5.8

Questa versione contiene hello seguenti aggiornamenti:

<table border="1">
<tr>
<th>Titolo</th>
<th>Descrizione</th>
<th>Area interessata (ad esempio servizio, componente o SDK)</p></th>
<th>Tipo di cluster (ad esempio Hadoop, HBase o Storm)</th>
<th>JIRA (se applicabile)</th>
</tr>
<tr>
<td>Altre porte HTTPS aperte</td>
<td>servizio cloud Hello apre ora 5 too8005 8001 di porte nel cluster hello ad esempio all'indirizzo https://<clustername>.azurehdinsight.net:8001/. Le richieste URL toothese vengono autenticati utilizzando hello stesso meccanismo di password di autenticazione di base come la porta 443. Queste porte associate toohello stessa porta sul nodo head active hello. Le azioni script possono essere utilizzato toomake cliente servizi ascolto su queste porte in hello nodo head e route toooutside hello cluster.</td>
<td>Servizio cloud</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
<tr>
<td>Problema di riproduzione casuale MapReduce intermittente per HDInsight 3.2</td>
<td>Correzione di una rara race condition intermittente nella sequenza casuale MapReduce nei cluster di grandi dimensioni che provoca occasionali errori delle attività. Per altre informazioni, vedere <a href="https://issues.apache.org/jira/browse/MAPREDUCE-6361" target="_blank">MAPREDUCE-6361</a>.</td>
<td>Funzionalità principale di Hadoop</td>
<td>Tutti</td>
<td><a href="https://issues.apache.org/jira/browse/MAPREDUCE-6361" target="_blank">MAPREDUCE-6361</a></td>
</tr>
<tr>
<td>Spostare tooLatest Java di Azure SDK 2.2 per 3.2 di HDInsight</td>
<td>Spostare toolatest versione di hello Azure SDK per Java utilizzato dal driver WASB hello. note sulla versione di hello per hello stesso sono disponibile in https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt SDK più recente Hello ha alcune correzioni.</td>
<td>Funzionalità principale di Hadoop</td>
<td>Tutti</td>
<td><a href="https://issues.apache.org/jira/browse/HADOOP-11959" target="_blank">HADOOP-11959</a></td>
</tr>
<tr>
<td>Spostare tooHDP 2.1.15 per i cluster HDInsight 3.1</td>
<td>Sono disponibili note sulla versione Hortonworks per la versione di hello <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.15-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.15.html" target="_blank">qui</a>.</td>
<td>HDP</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-06042015-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 04/06/2015
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight 2.1.10.583.1575584 (HDP 1.3.12.0-01795 - non modificato)
* HDInsight 3.0.6.583.1575584 (HDP 2.0.13.0-2117 - non modificato)
* HDInsight 3.1.3.583.1575584 (HDP 2.1.12.1-0003 - non modificato)
* HDInsight 3.2.4.583.1575584 (HDP 2.2.6.1-1)
* SDK 1.5.8

Questa versione contiene hello seguenti aggiornamenti:

<table border="1">
<tr>
<th>Titolo</th>
<th>Descrizione</th>
<th>Area interessata (ad esempio servizio, componente o SDK)</p></th>
<th>Tipo di cluster (ad esempio Hadoop, HBase o Storm)</th>
<th>JIRA (se applicabile)</th>
</tr>
<tr>
<td>Correzione per errore gateway non valido 502 per i cluster Storm</td>
<td>Questa versione consente di correggere un bug che interessano hello processo invio API che ha causato hello sito Web toobe inattivo dopo un riavvio.</td>
<td>Service</td>
<td>Storm</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-06012015-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 01/06/2015
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight 2.1.10.577.1563827 (HDP 1.3.12.0-01795 - non modificato)
* HDInsight 3.0.6.577.1563827 (HDP 2.0.13.0-2117 - non modificato)
* HDInsight 3.1.3.577.1563827 (HDP 2.1.12.1-0003 - non modificato)
* HDInsight 3.2.4.577.1563827 (HDP 2.2.6.0-2800 - non modificato)
* SDK 1.5.8

Questa versione contiene hello seguenti aggiornamenti:

<table border="1">
<tr>
<th>Titolo</th>
<th>Descrizione</th>
<th>Area interessata (ad esempio servizio, componente o SDK)</p></th>
<th>Tipo di cluster (ad esempio Hadoop, HBase o Storm)</th>
<th>JIRA (se applicabile)</th>
</tr>
<tr>
<td>Varie correzioni di bug</td>
<td>Questa versione consente di correggere i bug relativi toocluster provisioning.</td>
<td>Service</td>
<td>Tutti i tipi di cluster</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-05272015-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 27/05/2015
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight  3.2.4.570.1554102 (HDP 2.2.6.0-2800)
* Altre versioni di cluster e SDK non vengono distribuiti all'interno di questa versione.

Questa versione contiene hello seguenti aggiornamenti:

<table border="1">
<tr>
<th>Titolo</th>
<th>Descrizione</th>
<th>Area interessata (ad esempio servizio, componente o SDK)</p></th>
<th>Tipo di cluster (ad esempio Hadoop, HBase o Storm)</th>
<th>JIRA (se applicabile)</th>
</tr>
<tr>
<td>Aggiornamento HDP 2.2</td>
<td>Questa versione di HDInsight 3.2 contiene HDP 2.2.6 e offre numerose correzioni di bug importanti tooHDInsight. Hello completo note sulla versione sono disponibili in <a href="http://dev.hortonworks.com.s3.amazonaws.com/HDPDocuments/HDP2/HDP-2.2.6/HDP_RelNotes_v226/index.html">HDP 2.2.6 note sulla versione</a>.</td>
<td>HDP</td>
<td>Tutti i tipi di cluster</td>
<td>N/D</td>
</tr>
<tr>
<td>Modificare tooDefault Yarn contenitore di configurazione della memoria</td>
<td>In questo aggiornamento, hello memoria disponibile tooYARN contenitori predefiniti (yarn.nodemanager.resource.memory mb e yarn.scheduler.maximum-allocazione-mb), avviata dal gestore di nodi, too5632MB maggiore. In precedenza era too4608MB ridotta, ma in base alle diverse esecuzioni di processo, nuovo valore hello deve offrire affidabilità e prestazioni migliori toomost processi e pertanto il valore predefinito è migliore. Come al solito, se si dispone di dipendenza critica nella configurazione della memoria, impostarlo in modo esplicito durante la creazione di cluster hello.</td>
<td>HDP</td>
<td>Tutti i tipi di cluster</td>
<td>N/D</td>
</tr>
<tr>
<td>Parità di configurazione predefinita per i cluster HBase e Storm</td>
<td>Questo aggiornamento consente di ripristinare Hbase e Storm cluster toouse hello stessi valori delle configurazioni YARN cluster Hadoop. Questa operazione viene eseguita per la parità in tutti i tipi di cluster.</td>
<td>HDP</td>
<td>HBase, Storm</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-05202015-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 20/05/2015
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight 2.1.10.564.1542093 (HDP 1.3.12.0-01795 - non modificato)
* HDInsight 3.0.6.564.1542093 (HDP 2.0.13.0-2117 - non modificato)
* HDInsight 3.1.3.564.1542093 (HDP 2.1.12.1-0003)
* HDInsight 3.2.4.564.1542093 (HDP 2.2.4.6-2)
* SDK 1.5.8

Questa versione contiene hello seguenti aggiornamenti:

<table border="1">
<tr>
<th>Titolo</th>
<th>Descrizione</th>
<th>Area interessata (ad esempio servizio, componente o SDK)</p></th>
<th>Tipo di cluster (ad esempio Hadoop, HBase o Storm)</th>
<th>JIRA (se applicabile)</th>
</tr>
<tr>
<td>Supporto dell'EventHub SCP.NET</td>
<td>pacchetti di cluster Hello aggiornato per HDInsight Storm portare tooSCP.NET di nuove funzionalità. È ora possibile toonew accesso API in Generatore di topologia che rendono più facile toouse EventHubSpout o Spouts Java. È necessario aggiornare il toowork SCP.NET client SDK con nuovi cluster come hello contratti sono stati aggiornati. Per informazioni dettagliate su hello nuovo note sulla versione e sull'utilizzo, le API (inclusi correzioni di bug), fare riferimento toohello file Readme incluso nel pacchetto NuGet SCP.NET hello.</td>
<td>Strumenti VS</td>
<td>Cluster Storm HDInsight 3.2</td>
<td>N/D</td>
</tr>
<tr>
<td>Aggiornamento del driver JDBC</td>
<td>Versione aggiornata hello driver toohello SQL Server supportata in sqljdbc_4.1.5605.100.</td>
<td>Metastore</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-04272015-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 27/04/2015
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight 2.1.10.537.1486660 (HDP 1.3.12.0-01795 - non modificato)
* HDInsight 3.0.6.537.1486660 (HDP 2.0.13.0-2117 - non modificato)
* HDInsight 3.1.3.537.1486660 (HDP 2.1.12.0-2329 - non modificato)
* HDInsight 3.2.3.537.1486660 (HDP 2.2.2.2-4)
* SDK 1.5.8

Questa versione contiene hello seguenti aggiornamenti:

<table border="1">
<tr>
<th>Titolo</th>
<th>Descrizione</th>
<th>Area interessata (ad esempio servizio, componente o SDK)</p></th>
<th>Tipo di cluster (ad esempio Hadoop, HBase o Storm)</th>
<th>JIRA (se applicabile)</th>
</tr>
<tr>
<td>Correggere le dipendenze DLL</td>
<td>Rimuove la dipendenza di HDInsight dal framework per unit test.</td>
<td>SDK</td>
<td>Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Correzione dei bug per race condition</td>
<td>Un cluster Crea richiesta ora attese PUT richiesta toobe accettato prima di polling stato hello</td>
<td>SDK</td>
<td>Hadoop</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-04142015-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 14/04/2015
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight 2.1.10.521.1453250 (HDP 1.3.12.0-01795 - non modificato)
* HDInsight 3.0.6.521.1453250 (HDP 2.0.13.0-2117 - non modificato)
* HDInsight 3.1.3.521.1453250 (HDP 2.1.12.0-2329 - non modificato)
* HDInsight 3.2.3.525.1459730 (HDP 2.2.2.2-2)
* SDK 1.5.6

Questa versione contiene hello seguenti aggiornamenti:

<table border="1">
<tr>
<th>Titolo</th>
<th>Descrizione</th>
<th>Area interessata (ad esempio servizio, componente o SDK)</p></th>
<th>Tipo di cluster (ad esempio Hadoop, HBase o Storm)</th>
<th>JIRA (se applicabile)</th>
</tr>
<tr>
<td>Correzioni di bug</td>
<td>In questa versione di HDI 3.2 sono incluse correzioni per Apache TEZ 2214 e TEZ 1923. Queste sono necessarie per determinate query Hive nel Tez che richiedono una quantità significativa di dati tooshuffle.
</td>
<td>HDP</td>
<td>Hadoop</td>
<td><a href="https://issues.apache.org/jira/browse/TEZ-2214">TEZ 2214</a></br><a href="https://issues.apache.org/jira/browse/TEZ-1923">TEZ 1923</a></td>
</tr>
</table>

## <a name="notes-for-04062015-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 06/04/2015
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight 2.1.10.521.1453250 (HDP 1.3.12.0-01795 - non modificato)
* HDInsight 3.0.6.521.1453250 (HDP 2.0.13.0-2117 - non modificato)
* HDInsight 3.1.3.521.1453250 (HDP 2.1.12.0-2329 - non modificato)
* HDInsight 3.2.3.521.1453250 (HDP 2.2.2.2-1)
* SDK 1.5.6

Questa versione contiene hello seguenti aggiornamenti:

<table border="1">
<tr>
<th>Titolo</th>
<th>Descrizione</th>
<th>Area interessata (ad esempio servizio, componente o SDK)</p></th>
<th>Tipo di cluster (ad esempio Hadoop, HBase o Storm)</th>
<th>JIRA (se applicabile)</th>
</tr>
<tr>
<td>HDInsight .NET SDK 1.5.6</td>
<td>Aggiorna tooremove alcune classi interne per HDInsight su Linux.</td>
<td>SDK</td>
<td>Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Libreria Avro 1.5.6</td>
<td>Aggiunto <b>KnownTypeAttribute</b> per il metodo <b>GetAllKnownTypes</b>. Corretto NullReferenceException quando un tipo è null per il metodo GetAllKnownTypes.</td>
<td>SDK</td>
<td>Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Correzioni di bug</td>
<td>Servizio di toohello varie correzioni di bug</td>
<td>Service</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-04012015-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 01/04/2015
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight 2.1.10.513.1431705 (HDP 1.3.12.0-01795)
* HDInsight 3.0.6.513.1431705 (HDP 2.0.13.0-2117)
* HDInsight 3.1.3.513.1431705 (HDP 2.1.12.0-2329)
* HDInsight 3.2.3.513.1431705 (HDP 2.2.2.1-2600)
* SDK 1.5.5

Questa versione contiene hello seguenti aggiornamenti:

<table border="1">
<tr>
<th>Titolo</th>
<th>Descrizione</th>
<th>Area interessata (ad esempio servizio, componente o SDK)</p></th>
<th>Tipo di cluster (ad esempio Hadoop, HBase o Storm)</th>
<th>JIRA (se applicabile)</th>
</tr>
<tr>
<td>Capacità tooenable o disabilitare remote desktop credenziali nei cluster di Windows mediante .NET SDK</td>
<td>Supporto a livello di codice per l'abilitazione o la disabilitazione di credenziali RDP su cluster Windows.</td>
<td>SDK</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
<tr>
<td>Capacità tooenable remote desktop credenziali nei cluster durante cui viene effettuato il provisioning</td>
<td>Supporto a livello di codice per abilitare le credenziali di desktop remoto al cluster hello della creazione. In questo modo viene rimosso il processo in due passaggi hello per primo cluster hello provisioning e quindi l'abilitazione di desktop remoto.</td>
<td>SDK</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
<tr>
<td>Too2.7.8 aggiornata di Python</td>
<td>Python aggiornata nel cluster HDInsight tooPython 2.7.8, che contiene alcune sicurezza importanti correzioni per le versioni 2.1, 3.0, 3.1 e 3.2 di HDInsight</td>
<td>Service</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
<tr>
<td>Modifica della configurazione di YARN</td>
<td>Modificato YARN Configurazione applicazioni completato yarn.resourcemanager.max too1000 per tutti i tipi di cluster per le versioni 3.1 e 3.2 di HDInsight. Questo valore controlla solo elenco hello di applicazioni complete in hello dell'interfaccia utente YARN. tooget informazioni sulle applicazioni che sono stati inviati toohello precedente elenco di applicazioni nella hello dell'interfaccia utente, è possibile passare direttamente toohello cronologia Server.</td>
<td>YARN</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
<tr>
<td>Ridimensionamento dei nodi in un cluster HBase</td>
<td>È ora possibile ridimensionare i nodi (verso l'alto e verso il basso) nei cluster HBase per HDInsight versioni 3.1 e 3.2</td>
<td>Service</td>
<td>hbase</td>
<td>N/D</td>
</tr>
<tr>
<td>Aggiornamento JDBC</td>
<td>Driver SQL JDBC è sqljdbc_4.0.2206.100 tooversion aggiornato per HDInsight versione 3.2. Questa versione contiene importanti miglioramenti per la sicurezza.</td>
<td>HDP</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
<tr>
<td>Aggiornamento della configurazione di JVM</td>
<td>Aggiornato JVM configurazione networkaddress.cache.ttl too300 secondi dal valore predefinito hello -1 per le versioni 3.1 e 3.2 di HDInsight. Questo valore controlla la memorizzazione nella cache dei criteri per le ricerche di nomi corretta dal servizio nome hello hello. Questa correzione risolve un bug toogrowing e compattazione cluster HBase correlati.</td>
<td>Service</td>
<td>hbase</td>
<td>N/D</td>
</tr>
<tr>
<td>Aggiornamento tooAzure Storage SDK per Java 2.0</td>
<td>Versione 3.2 di HDInsight è aggiornato toouse hello ultima versione di hello Azure Storage SDK per Java. Contiene diverse correzioni di bug importanti rispetto alla versione di hello 0.6.0 corrente.</td>
<td>HDP</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
<tr>
<td>Codice sorgente WASB tooApache aggiornato</td>
<td>HDInsight versione 3.2 ora utilizza hello codice più recenti per il driver filesystem WASB hello dal framework Apache Hadoop. Con questa modifica, driver WASB hello è ora fornito come un file jar di separato. Questo è semplicemente una modifica di pacchetti e non contiene alcun toobehavior modifiche del driver WASB hello. nome del file JAR di Hello è hadoop-azure-2.6.0.jar.</td>
<td>HDP</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
<tr>
<td>Aggiornamenti del nome file jar in HDInsight 3.2</td>
<td>Questa versione di aggiornamento tooHDInsight 3.2 include diverse correzioni di bug e alcuni JAR interno, incluso come parte di HDP sono stati aggiornati. Questi pacchetti HDP JAR filesare toohello interno e non per l'uso diretto per le applicazioni dei clienti. Le applicazioni devono creare un pacchetto una propria versione di hello JAR in modo che un aggiornamento toohello file JAR HDP interno non interrompere le applicazioni dei clienti.</td>
<td>HDP</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-03032015-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 03/03/2015
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight 2.1.10.488.1375841 (HDP 1.3.9.0-01351 - non modificato)
* HDInsight 3.0.6.488.1375841 (HDP 2.0.9.0-2097 -  non modificato)
* HDInsight 3.1.3.488.1375841 (HDP 2.1.10.0-2290 - non modificato)
* HDInsight 3.2.3.488.1375841 (HDP-2.2.10.0-2340 - non modificato)
* SDK 1.5.0 (non modificato)

Questa versione contiene hello seguente aggiornamento:

<table border="1">
<tr>
<th>Titolo</th>
<th>Descrizione</th>
<th>Area interessata (ad esempio servizio, componente o SDK)</p></th>
<th>Tipo di cluster (ad esempio Hadoop, HBase o Storm)</th>
<th>JIRA</th>
</tr>
<tr>
<td>Miglioramenti dell'affidabilità</td>
<td>Sono stati apportati aggiornamenti che consentono una migliore con hello aumento del carico con la creazione di toocluster riguardo tooscale servizio hello.</td>
<td>Service</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-02182015-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 18/02/2015
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight 2.1.10.471.1342507 (HDP 1.3.9.0-01351 - non modificato)
* HDInsight 3.0.6.471.1342507 (HDP 2.0.9.0-2097 -  non modificato)
* HDInsight 3.1.3.471.1342507 (HDP 2.1.10.0-2290 - non modificato)
* HDInsight 3.2.3.471.1342507 (HDP-2.2.10.0-2340)
* SDK 1.5.0

Questa versione contiene hello seguenti aggiornamenti:

<table border="1">
<tr>
<th>Titolo</th>
<th>Descrizione</th>
<th>Area interessata (ad esempio servizio, componente o SDK)</p></th>
<th>Tipo di cluster (ad esempio Hadoop, HBase o Storm)</th>
<th>JIRA (se applicabile)</th>
</tr>
<tr>
<td>Cluster HDInsight 3.2</td>
<td>Hadoop 2.6/HDP2.2 è disponibile con cluster HDInsight 3.2. Contiene gli aggiornamenti importanti tooall dei componenti di hello open source. Per altre informazioni, vedere le novità di HDInsight e <a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.0/HDP_2.2.0_Release_Notes_20141202_version/index.html" target="_blank">HDP 2.2.0.0 Release Notes</a> (Note sulla versione di HDP 2.2.0.0).</td>
<td>Software open source</td>
<td>Tutti</td>
<td>N/D </td>
</tr>
<tr>
<td>HDInsight in Linux (anteprima)</td>
<td>È possibile distribuire cluster per l'esecuzione in Ubuntu Linux. Per altre informazioni, vedere la guida introduttiva di HDInsight in Linux.</td>
<td>Service</td>
<td>Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Disponibilità generale di Storm</td>
<td>I cluster Apache Storm sono in genere disponibili. Per altre informazioni, vedere la guida introduttiva all'uso di Storm in HDInsight.</td>
<td>Service</td>
<td>Storm</td>
<td>N/D</td>
</tr>
<tr>
<td>Dimensioni delle macchine virtuali</td>
<td>Azure HDInsight è disponibile per più tipi e dimensioni di macchine virtuali. HDInsight può utilizzare dimensioni tooA7 A2 compilate per scopi generali. Serie D nodi che presentano unità SSD (unità SSD) e processori più veloci 60 percento; e dimensioni A8 e A9 InfiniBand con supportano per reti veloci.</td>
<td>Service</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
<tr>
<td>Scalabilità del cluster</td>
<td>È possibile modificare il numero di hello di nodi di dati per un cluster HDInsight in esecuzione senza dovere toodelete o ricrearlo. Attualmente, solo i tipi di cluster Hadoop Query e Apache Storm abbiano questa possibilità, ma il supporto per il tipo di cluster Apache HBase appena toofollow. Per altre informazioni, vedere Gestire i cluster di HDInsight.</td>
<td>Service</td>
<td>Hadoop, Storm</td>
<td>N/D</td>
</tr>
<tr>
<td>Strumenti di Visual Studio</td>
<td>Inoltre toocomplete gli strumenti per Apache Storm, hello gli strumenti per Apache Hive in Visual Studio è stato il completamento delle istruzioni tooinclude aggiornato, la convalida locale e supporto migliorato per il debug. Per altre informazioni, vedere Introduzione all'uso di HDInsight Tools per Visual Studio.</td>
<td>Strumenti</td>
<td>Hadoop</td>
<td>N/D </td>
</tr>
<td>Connettore Hadoop per Azure Cosmos DB</td>
<td>Il connettore Hadoop per Azure Cosmos DB consente di eseguire operazioni complesse di aggregazione, analisi e manipolazione sui documenti JSON senza schema archiviati in raccolte Azure Cosmos DB o in account di database. Per altre informazioni e per un'esercitazione, vedere Eseguire un processo Hadoop usando Azure Cosmos DB e HDInsight.</td>
<td>Service</td>
<td>Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Correzioni di bug</td>
<td>Sono state apportate diverse correzioni di bug di minore entità per i servizi di HDInsight. Non sono previste modifiche del comportamento rilevabili dai clienti.</td>
<td>Service</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-02062015-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 06/02/2015
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight 2.1.10.463.1325367 (HDP 1.3.9.0-01351 - non modificato)
* HDInsight 3.0.6.463.1325367 (HDP 2.0.9.0-2097 - non modificato)
* HDInsight 3.1.2.463.1325367 (HDP 2.1.10.0-2290)
* SDK N/D

Questa versione contiene hello seguenti aggiornamenti:

<table border="1">
<tr>
<th>Titolo</th>
<th>Descrizione</th>
<th>Area interessata (ad esempio servizio, componente o SDK)</p></th>
<th>Tipo di cluster (ad esempio Hadoop, HBase o Storm)</th>
<th>JIRA (se applicabile)</th>
</tr>
<tr>
<td>Correzioni di bug</td>
<td>Sono state apportate diverse correzioni di bug di minore entità per i servizi di HDInsight. Non sono previste modifiche del comportamento rilevabili dai clienti.</td>
<td>Service</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
<tr>
<td>Aggiornamento di manutenzione HDP 2.1</td>
<td>HDInsight 3.1 è aggiornato toodeploy HDP 2.1.10.0. Per altre informazioni, vedere <a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.10/bk_releasenotes_hdp_2.1/content/ch_relnotes-HDP-2.1.10.html" target="_blank">Release Notes HDP-2.1.10</a> (Note sulla versione di HDP 2.1.10). </td>
<td>Software open source</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
<tr>
<td>Aggiornamenti binari HDP</td>
<td>In HBase sono presenti alcuni file con estensione jar di cui sono stati aggiornati i nomi. I file JAR vengono utilizzati internamente HBase, pertanto non è previsto che i clienti hanno una dipendenza da nomi di questi file JAR di hello. incluse le seguenti:
<ul>
<li>./lib/jetty-6.1.26.hwx.jar</li>
<li>./lib/jetty-sslengine-6.1.26.hwx.jar</li>
<li>./lib/jetty-util-6.1.26.hwx.jar</li>
</ul>
</td>
<td>Software open source</td>
<td>HBase</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-1292015-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 29/01/2015
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight 2.1.10.455.1309616 (HDP 1.3.9.0-01351 - non modificato)
* HDInsight 3.0.6.455.1309616 (HDP 2.0.9.0-2097 - non modificato)
* HDInsight 3.1.2.455.1309616 (HDP 2.1.9.0-2196 - non modificato)
* SDK N/D

Questa versione contiene hello seguente aggiornamento:

<table border="1">

<tr>
<th>Titolo</th>
<th>Descrizione</th>
<th>Area interessata (ad esempio servizio, componente o SDK)</p></th>
<th>Tipo di cluster (ad esempio Hadoop, HBase o Storm)</th>
<th>JIRA (se applicabile)</th>
</tr>
<tr>
<td>Correzioni di bug</td>
<td>Abbiamo apportato alcune correzioni di bug importanti che consentono di migliorare l'affidabilità di hello di hello cluster HDInsight durante gli aggiornamenti di Azure.</td>
<td>Service</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-152015-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 5/1/2015
numeri di versione completa di Hello per i cluster HDInsight distribuiti con questa versione:

* HDInsight 2.1.10.420.1246118 (HDP 1.3.9.0-01351 - non modificato)
* HDInsight 3.0.6.420.1246118 (HDP 2.0.9.0-2097 - non modificato)
* HDInsight 3.1.2.420.1246118 (HDP 2.1.9.0-2196 - non modificato)

Questa versione contiene hello seguenti aggiornamenti:

<table border="1">

<tr>
<th>Titolo</th>
<th>Descrizione</th>
<th>Componente</th>
<th>Tipo di cluster</th>
<th>JIRA (se applicabile)</th>
</tr>
<tr>
<td>Esempi per l'analisi delle tendenze di Twitter e i consigli cinematografici basati su Mahout</td>
<td><p>In questa versione, hello console HDInsight Query presenta due esempi aggiuntivi:</p>

<p><b>Analisi delle tendenze di Twitter</b><br>
Le API pubbliche offerte da siti quali Twitter costituiscono un'utile origine di dati per l'analisi e la comprensione delle tendenze più popolari. In questa esercitazione, informazioni su come toouse Hive tooget un elenco di utenti di Twitter inviati hello la maggior parte dei TWEET che contiene una parola specifica. </p>

<p><b>Consigli cinematografici di Mahout</b><br>
Apache Mahout è una libreria Machine Learning di Apache Hadoop. Mahout contiene gli algoritmi per l'elaborazione dei dati, ad esempio applicazione di filtri, classificazione e clustering. In questa esercitazione, usare un suggerimenti di film toogenerate di motore di raccomandazione basati su filmati che sono visualizzati i tuoi amici.</p></td>
<td>Console query</td>
<td>Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Modificare il valore toodefault per la configurazione di Hive: hive.auto.convert.join.noconditionaltask.size</td>
<td><p>Tooautomatically convertito mappa join si applica questa configurazione di dimensioni. il valore di Hello rappresenta somma hello delle dimensioni di hello delle tabelle che possono essere convertiti toohash mappe che rientrano nella memoria. In una versione precedente, questo valore è aumentato da valore predefinito di hello pari a 10 MB too128 MB. Tuttavia, nuovo valore di hello di 128 MB causava processi toofail toolack a causa di memoria. Questa versione viene ripristinato il valore di predefinito hello nuovamente too10 MB. I clienti possono comunque scegliere toooverride questo valore durante la creazione del cluster specificata, le query e le dimensioni di tabella. Per ulteriori informazioni su questa impostazione e la modalità toooverride, vedere <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.0.2/ds_Hive/optimize-joins.html#JoinOptimization-OptimizeAutoJoinConversion" target="_blank">ottimizzare automaticamente Join conversione</a> in Hortonworks documentazione. </p></td>
<td>Hive</td>
<td>Hadoop, Hbase</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-12232014-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 23/12/2014
numeri di versione completo Hello per i cluster HDInsight distribuiti con questa versione sono:

* HDInsight 2.1.10.420.1246783 (versione di HDP non modificata)
* HDInsight 3.0.6.420.1246783 (versione di HDP non modificata)
* HDInsight 3.1.1.420.1246783 (versione di HDP non modificata)

Questa versione contiene hello seguente aggiornamento:

<table border="1">
<tr>
<th>Titolo</th>
<th>Descrizione</th>
<th>Componente</th>
<th>Tipo di cluster</th>
<th>JIRA (se applicabile)</th>
</tr>
<tr>
<td>Errori di creazione dei cluster intermittenti scadenza tooexcessive carico</td>
<td><p>Algoritmo migliorato per scaricare i pacchetti HDP durante la creazione del cluster consente la gestione di più affidabile di errori a causa di tooexcessive carico.</p></td>
<td>Service</td>
<td>Hadoop, Hbase, Storm</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-12182014-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 18/12/2014
Questa versione contiene hello dell'aggiornamento dei componenti seguenti:

<table border="1">
<tr>
<th>Titolo</th>
<th>Descrizione</th>
<th>Componente</th>
<th>Tipo di cluster</th>
<th>JIRA (se applicabile)</th>
</tr>
<tr>
<td><a href = "hdinsight-hadoop-customize-cluster.md" target="_blank">Personalizzazione dei cluster disponibile a livello generale</a></td>
<td><p>Personalizzazione offre capacità hello di toocustomize cluster Azure HDInsight con i progetti che sono disponibili dall'ecosistema di hello Apache Hadoop. Con questa nuova funzionalità, è possibile provare e distribuire progetti di Hadoop tooAzure HDInsight. Questa opzione è abilitata tramite hello **genera Script azione** funzionalità che è possibile modificare i cluster Hadoop in modo arbitrario tramite script personalizzati. Questa personalizzazione è disponibile su tutti i tipi di cluster HDInsight, inclusi Hadoop, HBase e Storm. potenza di hello toodemonstrate di questa funzionalità, è stato documentato hello tooinstall di hello processo comune <a href = "hdinsight-hadoop-spark-install.md" target="_blank">Spark</a>, <a href = "hdinsight-hadoop-r-scripts.md" target="_blank">R</a>, <a href = "hdinsight-hadoop-solr-install.md" target="_blank">Solr</a>, e <a href = "hdinsight-hadoop-giraph-install.md" target="_blank">Giraph</a> moduli. Questa versione anche aggiunge la funzionalità di hello per i clienti toospecify la loro azione script personalizzati tramite hello portale di Azure fornisce linee guida e procedure consigliate su come toobuild custom script azioni utilizzando i metodi di supporto e vengono fornite indicazioni sulla tootest azione di script Hello. </p></td>
<td>Disponibilità generale delle funzionalità</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-12052014-release-of-hdinsight"></a>Note per la versione di HDinsight rilasciata il 05/12/2014
numeri di versione completo Hello per i cluster HDInsight distribuiti con questa versione sono:

* HDInsight 2.1.9.406.1221105 (HDP 1.3.9.0-01351)
* HDInsight 3.0.5.406.1221105 (HDP 2.0.9.0-2097)
* HDInsight 3.1.1.406.1221105 (HDP 2.1.9.0-2196)
* SDK HDInsight N/D

Questa versione contiene hello aggiornamenti dei componenti seguenti:

<table border="1">
<tr>
<th>Titolo</th>
<th>Descrizione</th>
<th>Componente</th>
<th>Tipo di cluster</th>
<th>JIRA (se applicabile)</th>
</tr>
<tr>
<td>Correzione di bug: errore intermittenti durante l'aggiunta di un numero elevato di tabella tooa partizioni in un Hive DDL </td>
<td><p>Se si verifica un errore di connessione intermittente con database di metastore Hive hello durante l'aggiunta di molte tabella Hive tooa di partizioni, hello DDL Hive può non riuscire. Hello seguente istruzione isseen nel log degli errori di Hive hello se si verifica questo errore: </p><p>"ERROR [main]: ql.Driver (SessionState.java:printError(547)) - FAILED: Execution Error, return code 1 from org.apache.hadoop.hive.ql.exec.DDLTask. MetaException(message:java.lang.RuntimeException: commitTransaction was called but openTransactionCalls = 0. Ciò probabilmente indica che non vi siano chiamate sbilanciata tooopenTransaction/commitTransaction)"</p></td>
<td>Hive</td>
<td>Hadoop, Hbase</td>
<td>HIVE-482 (Si tratta di JIRA interno, non può essere indicato esternamente. Specificato qui come riferimento).</td>
</tr>
<tr>
<td>Correzione di bug: blocco occasionale in hello HDInsight Query Console</td>
<td>In questo caso, hello istruzione riportata di seguito può essere visualizzato nel registro WebHCat hello per il processo di avvio WebHCat hello: <p>"org.apache.hive.hcatalog.templeton.CatchallExceptionMapper | org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.yarn.exceptions.YarnRuntimeException): Impossibile caricare il file di cronologia {wasb url toohello cronologia file} "</p></td>
<td>WebHCat</td>
<td>Hadoop</td>
<td>HIVE-482 (Si tratta di JIRA interno, non può essere indicato esternamente. Specificato qui come riferimento).</td>
</tr>
<tr>
<td>Correzione di bug: picco occasionale della latenza delle query Hbase</td>
<td>In questo caso, gli utenti noteranno un picco occasionale di 3 secondi della latenza delle query di Hbase hello. </td>
<td>Gateway del cluster HDInsight</td>
<td>HBase</td>
<td>N/D</td>
</tr>
<tr>
<td>Modifiche al nome file jar HDP</td>
<td>Per HDI cluster versione 3.0, esistono un paio di modifiche toohello interni file JAR installati da HDP. jetty-6.1.26.jar è stato sostituito da jetty-6.1.26.hwx.jar. jetty-util-6.1.26.jar è stato sostituito da jetty-util-6.1.26.hwx.jar. Le modifiche si applicano a progetti di tooHadoop, Mahout, WebHCat e Oozie.</td>
<td>Hadoop, Mahout, WebHCat, Oozie</td>
<td>Hadoop, HBase</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-11212014-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 21/11/2014
numeri di versione completo Hello per i cluster HDInsight distribuiti con questa versione sono:

* HDInsight 2.1.9.382.1169709 (nessuna modifica rispetto al 14/11/2014)
* HDInsight 3.0.5.382.1169709 (nessuna modifica rispetto al 14/11/2014)
* HDInsight 3.1.1.382.1169709 (nessuna modifica rispetto al 14/11/2014)
* HDInsight SDK 1.4.0

Questa versione contiene hello aggiornamenti dei componenti seguenti:

<table border="1">
<tr><th>Titolo</th><th>Descrizione</th><th>Componente</th><th>Tipo di cluster</th><th>JIRA (se applicabile)</th></tr>
<tr>
<td>Accesso ai registri applicazioni</td>
<td>Possibilità tooprogrammatically enumerare applicazioni che sono state eseguite nel cluster e toodownload log specifici dell'applicazione o specifici per i contenitori rilevanti toohelp debug problematico.</td>
<td>SDK</td>
<td>Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Nome dell'area toospecify possibilità in IHdInsightClient.DeleteCluster </td>
<td>Hello Azure HDInsight SDK fornisce hello possibilità toospecify un nome di area quando si utilizza **DeleteCluster**. In questo modo i clienti che contiene due risorse con lo stesso nome in aree diverse e fosse stata toodelete non è possibile sbloccare una di esse.</td>
<td>SDK</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
<tr>
<td>ClusterDetails.DeploymentId</td>
<td>Hello **ClusterDetails** restituirà un **DeploymentID** campo che rappresenta un identificatore univoco per il cluster hello. È sicuramente univoco nella creazione del cluster toobe tenta con hello stesso nomi.</td>
<td>SDK</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-11142014-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 14/11/2014

numeri di versione completo Hello per i cluster HDInsight distribuiti con questa versione sono:

* HDInsight 2.1.9.382.1169709
* HDInsight 3.0.5.382.1169709
* HDInsight 3.1.1.382.1169709

Questa versione contiene hello seguenti correzioni di bug, nuove funzionalità e aggiornamenti dei componenti.

<table border="1">
<tr><th>Titolo</th><th>Descrizione</th><th>Componente</th><th>Tipo di cluster</th><th>JIRA (se applicabile)</th></tr>
<tr>
<td>Azione di script (anteprima)</td>
<td>Anteprima della funzionalità di personalizzazione di cluster hello che consente la modifica di Hadoop cluster in modo arbitrario con script personalizzati. Con questa funzionalità, gli utenti possono sperimentare e distribuire i progetti che sono disponibili da hello Apache Hadoop ecosistema tooAzure che cluster HDInsight. Questa funzionalità di personalizzazione è disponibile in tutti i tipi di cluster HDInsight, inclusi Hadoop, HBase e Storm.</td>
<td>Nuova funzionalità</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
<tr>
<td>Processi predefiniti per l'analisi dei log relativi a Siti web e Archiviazione di Azure</td>
<td>Hello HDInsight Query Console dispone di una raccolta di introduzione che supporta le soluzioni che funzionano sui dati o su dati di esempio.
<p>**Soluzioni utilizzabili sui dati dell'utente**:<br>
Abbiamo creato i processi per alcuni hello più comuni dati analisi scenari tooprovide un punto di partenza per la creazione di soluzioni personalizzate. È possibile utilizzare i dati con hello processo toosee funzionamento. Quindi quando si è pronti, utilizzare le informazioni acquisite toocreate una soluzione che viene modellata di processo predefiniti hello.</p>
<p>**Soluzioni utilizzabili sui dati di esempio**:<br>
Informazioni su come toowork con HDInsight esaminando alcuni scenari di base (ad esempio, l'analisi dei log web e i dati del sensore). Si apprenderà come toouse HDInsight tooanalyze tali dati e come è possibile connettere altri dati di toothis applicazioni e servizi. Visualizzazione dei dati tramite la connessione tooMicrosoft Excel viene fornito un esempio di potenza hello di questo approccio.</p></td>
<td>Console query</td>
<td>Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Correzione per la perdita di memoria in Templeton</td>
<td>È stata risolta la perdita di memoria in Templeton che ha interessato i clienti con cluster con esecuzioni di lunga durata o che inviavano centinaia di richieste di processi al secondo. Hello problema che si manifesta come Templeton 5xx errori e la soluzione alternativa hello servizio Attivazione processo Windows toorestart hello. soluzione alternativa Hello non è più necessario.</td>
<td>Templeton</td>
<td>Tutti</td>
<td>https://issues.apache.org/jira/browse/HADOOP-11248</td>
</tr>
</table>

> [!NOTE]
> nuove funzionalità rese disponibili dalla personalizzazione del cluster, le procedure di hello utilizzando l'azione Script tooinstall Spark e moduli R in un cluster hello toodemonstrate presentano. Per altre informazioni, vedere:

* [Installare e usare Spark 1.0 nei cluster HDInsight](hdinsight-hadoop-spark-install.md)
* [Installare e usare R nei cluster Hadoop HDInsight](hdinsight-hadoop-r-scripts.md)

## <a name="notes-for-11072014-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata il 07/11/2014

numeri di versione completo Hello per i cluster HDInsight distribuito con questa versione sono:

* HDInsight 2.1 2.1.9.374.1153876
* HDInsight 3.0 3.0.5.374.1153876
* HDInsight 3.1 3.1.1.374.1153876

Questa versione contiene hello aggiornamenti dei componenti seguenti:

<table border="1">
<tr><th>Titolo</th><th>Descrizione</th><th>Componente</th><th>Tipo di cluster</th><th>JIRA (se applicabile)</th></tr>
<tr>
<td>HDP 2.1.7</td>
<td>Questa versione è basata su Hortonworks Data Platform (HDP) 2.1.7. Per altre informazioni, vedere <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html" target="_blank">Release Notes for HDP 2.1.7</a> (Note sulla versione per HDP 2.1.7).</td>
<td>HDP</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
<tr>
<td>Server di sequenza temporale YARN</td>
<td>Hello Server sequenza temporale YARN (noto anche come hello generico applicazione cronologia Server) è stata abilitata per impostazione predefinita. Hello Timeline Server fornisce informazioni generiche sulle applicazioni completate (ad esempio l'ID dell'applicazione, nome dell'applicazione, lo stato dell'applicazione, ora di invio dell'applicazione e il tempo di completamento dell'applicazione).

Queste informazioni sull'applicazione può essere recuperati dal nodo head hello accedendo hello URI http://headnodehost:8188 o comando YARN hello: yarn applicazione - elenco - appStates tutti.

È anche possibile recuperare in modo remoto queste applicazioni tramite l'API REST all'indirizzo https://{ClusterDnsName}. azurehdinsight.net/ws/v1/applicationhistory/.

Per altre informazioni dettagliate, vedere <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN Timeline Server</a> (Server di sequenza temporale YARN).</td>
<td>Servizio, YARN</td>
<td>Hadoop, HBase</td>
<td>N/D</td>
</tr>
<tr>
<td>ID di distribuzione cluster</td>
<td>A partire dalla versione più recente dell'SDK, 1.3.3.1.5426.29232, gli utenti possono accedere agli ID univoci rilasciati da HDInsight per ogni cluster. Questo toofigure clienti consente istanze univoche dei cluster quando si riutilizza un nome DNS tra creare o eliminare gli scenari.</td>
<td>SDK</td>
<td>Tutti</td>
<td>N/D</td>
</tr>
</table>

> [!NOTE]
> bug Hello che ha impedito il numero di versione completo hello siano visualizzati nel portale di hello o la restituzione da hello SDK o da Windows PowerShell è stato risolto in questa versione.

## <a name="notes-for-10152014-release"></a>Note per la versione rilasciata il 15/10/2014

Questa versione di aggiornamento rapido risolto un problema di memoria in Templeton che interessava gli utenti elevato hello di Templeton. In alcuni casi, gli utenti che esercitato Templeton frequentemente sarebbero Vedere errori presentati come codici di errore 500 perché le richieste di hello non avrebbe toorun sufficiente memoria. soluzione Hello per questo problema è toorestart hello Templeton. Il problema è stato risolto.

## <a name="notes-for-1072014-release"></a>Note per la versione rilasciata il 07/10/2014

* Quando si utilizza Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", hello *host_name* campo restituisce Hello dominio nome completo (FQDN) del nodo hello anziché solo il nome di host hello. Ad esempio, anziché restituire "**headnode0**", si ottiene hello FQDN"**headnode0. { ClusterDNS} .azurehdinsight .net**". Questa modifica è stato richiesto toofacilitate scenari in cui più tipi di cluster (ad esempio HBase e Hadoop) possono essere distribuiti in una rete virtuale. Ciò accade, ad esempio, quando si usa HBase come piattaforma back-end per Hadoop.

* Vengono fornite nuove impostazioni di memoria per la distribuzione di hello predefinita del cluster HDInsight hello. Precedenti impostazioni predefinite della memoria non tiene conto in modo adeguato per indicazioni sull'hello per numero di hello di core CPU da distribuire. Queste nuove impostazioni di memoria dovrebbero offrire valori predefiniti migliori, sulla base delle raccomandazioni di Hortonworks. toochange queste operazioni, consultare la documentazione di riferimento SDK toohello sulla modifica di configurazione del cluster. impostazioni della memoria nuovo Hello utilizzati dal cluster di HDInsight hello predefinito 4 CPU core (8 contenitore) vengono classificate in hello nella tabella seguente. (versione di hello valori usati toothis precedenti vengono inoltre forniti parenthetically.)

<table border="1">
<tr><th>Componente</th><th>Allocazione della memoria</th></tr>
<tr><td> yarn.scheduler.minimum-allocation</td><td>768 MB (in precedenza 512 MB)</td></tr>
<tr><td> yarn.scheduler.maximum-allocation</td><td>6.144 MB (invariato)</td></tr>
<tr><td>yarn.nodemanager.resource.memory</td><td>6.144 MB (invariato)</td></tr>
<tr><td>mapreduce.map.memory</td><td>768 MB (in precedenza 512 MB)</td></tr>
<tr><td>mapreduce.map.java.opts</td><td>opts=-Xmx512m (in precedenza -Xmx410m)</td></tr>
<tr><td>mapreduce.reduce.memory</td><td>1.536 MB (in precedenza 1.024 MB)</td></tr>
<tr><td>mapreduce.reduce.java.opts</td><td>opts=-Xmx1024m (in precedenza -Xmx819m)</td></tr>
<tr><td>yarn.app.mapreduce.am.resource</td><td>768 MB (in precedenza 1.024 MB)</td></tr>
<tr><td>yarn.app.mapreduce.am.command</td><td>opts=-Xmx512m (in precedenza -Xmx819m)</td></tr>
<tr><td>mapreduce.task.io.sort</td><td>256 MB (in precedenza 200 MB)</td></tr>
<tr><td>tez.am.resource.memory</td><td>1.536 MB (invariato)</td></tr>
</table>

Per ulteriori informazioni sulle impostazioni di configurazione di memoria hello utilizzato da YARN e MapReduce in hello Hortonworks Data Platform che viene utilizzato da HDInsight, vedere [determinare le impostazioni di configurazione di HDP memoria](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1-latest/bk_installing_manually_book/content/rpm-chap1-11.html). Hortonworks inoltre disponibile uno strumento toocalculate le impostazioni di memoria appropriata.

Per quanto riguarda hello Azure PowerShell e il messaggio di errore SDK HDInsight hello: "*Cluster non è configurato per l'accesso HTTP services*":

* Questo errore è un noto [problema di compatibilità](https://social.msdn.microsoft.com/Forums/azure/a7de016d-8de1-4385-b89e-d2e7a1a9d927/hdinsight-powershellsdk-error-cluster-is-not-configured-for-http-services-access?forum=hdinsight) che possono verificarsi a causa di tooa differenza nella versione di hello di hello HDInsight SDK o Azure PowerShell e hello del cluster hello. Per i cluster creati sulla versione 8/15 o successiva esiste il supporto della nuova funzionalità di provisioning nelle reti virtuali, Ma questa funzionalità non viene interpretata correttamente da versioni precedenti di hello HDInsight SDK o Azure PowerShell. il risultato di Hello è un errore in alcune operazioni di invio del processo. Se si utilizzano i cmdlet di HDInsight SDK API o Azure PowerShell (**utilizzare AzureRmHDInsightCluster** o **Invoke AzureRmHDInsightHiveJob**) toosubmit processi, tali operazioni potrebbero non riuscire con un messaggio di errore hello " *Cluster <clustername> non è configurato per l'accesso HTTP services*. " O (a seconda operazione hello), si potrebbero ottenere altri messaggi di errore, ad esempio "*non è possibile connettersi toocluster*".
* Questi problemi di compatibilità vengono risolti nelle versioni più recenti di hello di hello HDInsight SDK e di Azure PowerShell. Si consiglia di aggiornare hello SDK HDInsight tooversion 1.3.1.6 o versione successiva e Azure PowerShell Tools tooversion 0.8.8 o versione successiva. È possibile ottenere accesso toohello SDK più recente di HDInsight da [NugGet](http://nuget.codeplex.com/wikipage?title=Getting%20Started) e hello Azure PowerShell strumenti [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

## <a name="notes-for-9122014-release-of-hdinsight-31"></a>Note per la versione di HDInsight 3.1 rilasciata il 12/09/2014
* Questa versione è basata su Hortonworks Data Platform (HDP) 2.1.5. Per un elenco di bug hello in questa versione, vedere hello [corretti in questa versione](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.5/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.5-fixed.html) pagina sul sito Hortonworks hello.
* Nella cartella di librerie di hello Pig, file hello "avro-mapred-1.7.4.jar" è stato modificato troppo "avro-mapred-1.7.4-hadoop2.jar." contenuto Hello di questo file contiene una correzione di bug secondaria che non è importante. È consigliabile che i clienti non effettuano una dipendenza diretta in nome hello di hello JAR file tooavoid interruzioni quando i file vengono rinominati.

## <a name="notes-for-8212014-release"></a>Note per la versione rilasciata il 21/08/2014
* Si aggiungono hello seguente configurazione WebHCat (7155 HIVE), che imposta limite di memoria hello predefinito per un controller Templeton processo too1 GB. (valore predefinito precedente hello è 512 MB).

     templeton.mapper.memory.mb (=1024)

  * Questa modifica risolve hello errore con determinate query Hive a causa dei limiti di memoria toolower seguente: "Oltre i limiti di memoria fisica è in esecuzione di contenitore."
  * toorevert toohello vecchi valori predefiniti, è possibile impostare questo too512 del valore di configurazione tramite Azure PowerShell al momento della creazione del cluster tramite hello comando seguente:

      Add-AzureRmHDInsightConfigValues -Core @{"templeton.mapper.memory.mb"="512";}
* nome host Hello del ruolo zookeeper hello è stato modificato troppo*zookeeper*. Ciò influisce sulla risoluzione dei nomi all'interno di cluster hello, ma non influisce sull'API REST esterne. Se si dispone di componenti che hello utilizzare *zookeepernode* nome host, è necessario tooupdate li toouse nuovo nome. Hello nuovi nomi per i nodi zookeeper tre hello sono:

  * zookeeper0
  * zookeeper1
  * zookeeper2
* La matrice di supporto delle versioni di HBase è stata aggiornata. Per i carichi di lavoro HBase di produzione è supportato solo HDInsight 3.1 (HBase versione 0.98). In futuro la versione 3.0 disponibile in anteprima non sarà supportata.

## <a name="notes-about-clusters-created-prior-too8152014"></a>Note sui cluster creati precedente too8/15/2014
Un messaggio di errore di Azure PowerShell o il SDK HDInsight "Cluster <clustername> non è configurato per l'accesso HTTP servizi" (o a seconda operazione hello, altri errori di messaggi, ad esempio: "Impossibile connettersi toocluster") possono essere rilevati a causa delle differenze tooa tra Azure PowerShell o hello HDInsight SDK e un cluster. Per i cluster creati sulla versione 8/15 o successiva esiste il supporto della nuova funzionalità di provisioning nelle reti virtuali, Questa funzionalità non è interpretata correttamente da versioni precedenti di hello Azure PowerShell o hello SDK HDInsight, determinando errori di operazioni di invio del processo. Se si utilizza l'API SDK HDInsight o Azure PowerShell cmdlet (ad esempio utilizzare AzureRmHDInsightCluster o Invoke AzureRmHDInsightHiveJob) toosubmit processi, tali operazioni potrebbero non riuscire con uno dei messaggi di errore hello descritti.

Questi problemi di compatibilità vengono risolti nelle versioni più recenti di hello di hello HDInsight SDK e di Azure PowerShell. Si consiglia di aggiornare hello SDK HDInsight tooversion 1.3.1.6 o versione successiva e Azure PowerShell Tools tooversion 0.8.8 o versione successiva. È possibile ottenere accesso toohello SDK più recente di HDInsight da [NuGet][nuget-link]. È possibile accedere a strumenti di PowerShell Azure hello utilizzando [installazione guidata piattaforma Web di Microsoft][webpi-link].

## <a name="notes-for-7282014-release"></a>Note per la versione rilasciata il 28/07/2014
* **HDInsight disponibile in nuove aree**: È stato espanso toothree le aree geografiche presenza di HDInsight. I clienti di HDInsight possono creare cluster nelle aree seguenti:
  * Asia orientale
  * Stati Uniti centro-settentrionali
  * Stati Uniti centro-meridionali
* HDInsight versione 1.6 (HDP 1.1 e Hadoop 1.0.3) e HDInsight versione 2.1 (HDP1.3 e Hadoop 1.2) devono essere rimossi dall'hello portale di Azure. È possibile continuare a cluster Hadoop toocreate per queste versioni utilizzando hello cmdlet di Azure PowerShell [New AzureRmHDInsightCluster](http://msdn.microsoft.com/library/dn593744.aspx) o utilizzando hello [HDInsight SDK](http://msdn.microsoft.com/library/azure/dn469975.aspx). Per altre informazioni, vedere l'articolo sul [controllo delle versioni del componente di HDInsight](hdinsight-component-versioning.md).
* Modifiche a Hortonworks Data Platform (HDP) in questa versione:

<table border="1">
<tr><th>HDP</th><th>Modifiche</th></tr>
<tr><td>HDP 1.3/HDI 2.1</td><td>Nessuna modifica</td></tr>
<tr><td>HDP 2.0/HDI 3.0</td><td>Nessuna modifica</td></tr>
<tr><td>HDP 2.1/HDI 3.1</td><td>zookeeper: ['3.4.5.2.1.3.0-1948'] -> ['3.4.5.2.1.3.2-0002']</td></tr>
</table>

## <a name="notes-for-6242014-release"></a>Note per la versione rilasciata il 24/6/2014
Questa versione contiene il servizio HDInsight di toohello miglioramenti:

* **Disponibilità di HDP 2.1**: 3.1 HDInsight (contenente HDP 2.1) è in genere disponibile ed è di versione di hello predefinita per nuovi cluster.
* **HBase - Miglioramenti nel portale di Azure**: i cluster HBase sono disponibili in anteprima. È possibile creare cluster HBase dal portale hello con pochi clic.

Con HBase, è possibile compilare un'ampia gamma di carichi di lavoro in tempo reale in HDInsight, da siti Web interattivo che funzionano con grandi set di dati tooservices l'archiviazione dei dati di telemetria e sensore da milioni di punti di fine. passaggio successivo Hello sarebbe dati hello tooanalyze in questi carichi di lavoro con i processi di Hadoop e questo è possibile in HDInsight mediante Azure PowerShell e dashboard del cluster di hello Hive.

### <a name="apache-mahout-preinstalled-on-hdinsight-31"></a>Apache Mahout è preinstallato in HDInsight 3.1
 [Mahout](http://hortonworks.com/hadoop/mahout/) sia già installato nel cluster HDInsight Hadoop 3.1, per poter eseguire i processi Mahout senza necessità di hello della configurazione di cluster aggiuntivo. Ad esempio, è possibile remoto in un cluster Hadoop usando Remote Desktop Protocol (RDP) e senza effettuare dei passaggi aggiuntivi, è possibile eseguire hello Hello World Mahout comando seguente:

        mahout org.apache.mahout.classifier.df.tools.Describe -p /user/hdp/glass.data -f /user/hdp/glass.info -d I 9 N L

        mahout org.apache.mahout.classifier.df.BreimanExample -d /user/hdp/glass.data -ds /user/hdp/glass.info -i 10 -t 100

Per una spiegazione più completa di questa procedura, vedere la documentazione di hello per hello [Breiman esempio](https://mahout.apache.org/users/classification/breiman-example.html) nel sito Web Apache Mahout hello.

### <a name="hive-queries-can-use-tez-in-hdinsight-31"></a>Le query Hive possono usare Tez in HDInsight 3.1
Hive 0.13 è disponibile in HDInsight 3.1 e può eseguire query mediante Tez, consentendo notevoli miglioramenti delle prestazioni.
Tez non è abilitato per impostazione predefinita per le query Hive. toouse, è necessario partecipare. È possibile abilitare Tez eseguendo hello frammento di codice seguente:

        set hive.execution.engine=tez;
        select sc_status, count(*), histogram_numeric(sc_bytes,5) from website_logs_orc_local group by sc_status;

Hortonworks ha pubblicato un elenco dettagliato dei miglioramenti delle prestazioni delle query Hive con Tez risultanti dall'esecuzione di benchmark standard. Per informazioni dettagliate, vedere l'articolo relativo al [benchmarking di Apache Hive 13 per la soluzione Hadoop di livello enterprise](http://hortonworks.com/blog/benchmarking-apache-hive-13-enterprise-hadoop/).

Per altre informazioni, vedere [Hive on Tez](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) (Hive in Tez).

### <a name="global-availability"></a>Disponibilità globale
Con la versione di hello di HDInsight in Hadoop 2.2, Microsoft ha reso HDInsight disponibile in tutti i principali aree geografiche in cui Azure è disponibile. In particolare, occidentale hello Data Center in Europa e Asia sudorientale portati online. In questo modo i cluster toolocate di clienti in un Data Center vicino e, potenzialmente, in una zona simili di requisiti di conformità.

### <a name="dos--donts-between-cluster-versions"></a>Operazioni consigliate e sconsigliate tra le versioni dei cluster
**I metastore Oozie usati con un cluster HDInsight 3.1 non sono compatibili con le versioni precedenti dei cluster HDInsight 2.1 e non possono essere usati con questa versione precedente**.

Un database metastore Oozie personalizzato, implementato con un cluster HDInsight 3.1, non può essere riutilizzato con un cluster HDInsight 2.1, Questo avviene hello anche se è stato originato il metastore hello con un cluster HDInsight 2.1. Questo scenario non è supportato perché lo schema di metastore hello Ottiene aggiornato quando si utilizza un cluster HDInsight 3.1, pertanto non è più compatibile con metastore hello richiesto dal cluster HDInsight 2.1 hello. Qualsiasi tooreuse tentativo un metastore Oozie che è stato usato con un cluster HDInsight 3.1 inutilizzabile cluster HDInsight 2.1 hello.

**I metastore Oozie non possono essere condivisi tra cluster.**

Oozie Metastore sono collegati toospecific cluster e non può essere condivisa tra cluster.

### <a name="breaking-changes"></a>Modifiche di rilievo
**Sintassi di prefisso**: hello solo "wasb: / /" sintassi è supportata nel 3.0 cluster e 3.1 di HDInsight. Hello precedente "asv: / /" sintassi è supportata in HDInsight 2.1 e 1.6 cluster, ma non è supportata nel 3.0 cluster o 3.1 di HDInsight. Ciò significa che tutti i processi inviati tooan HDInsight 3.1 o 3.0 in modo esplicito del cluster che utilizza hello "asv: / /" sintassi non riuscirà. Hello "wasb: / /" sintassi da utilizzare in sostituzione. Inoltre, i processi inviati tooany 3.1 HDInsight o 3.0 cluster creati con un metastore esistente che contiene esplicito fa riferimento a tooresources utilizzando hello "asv: / /" sintassi non riuscirà. I Metastore necessario toobe ricreati utilizzando hello "wasb: / /" risorse tooaddress di sintassi.

**Porte**: porte hello utilizzate dal servizio HDInsight hello sono stati modificati. i numeri di porta Hello che sono stati utilizzati erano entro l'intervallo di porte effimere hello del sistema operativo di Windows hello. Per le comunicazioni di breve durata basate su IP, le porte vengono allocate automaticamente da un intervallo di porte temporanee predefinito. nuovo set di Hello consentiti Hortonworks Data Platform (HDP) del servizio di numeri di porta sono di fuori di questo intervallo di tooavoid incorrere in conflitti tra che può verificarsi con porte hello utilizzate dai servizi in esecuzione nel nodo head hello. nuovi numeri di porta Hello non dovrebbero causare le modifiche di rilievo. di seguito sono riportati i numeri di Hello utilizzati:

 **HDInsight 1.6 (HDP 1.1)**

<table border="1">
<tr><th>Nome</th><th>Valore</th></tr>
<tr><td>dfs.http.address</td><td>namenodehost:30070</td></tr>
<tr><td>dfs.datanode.address</td><td>0.0.0.0:30010</td></tr>
<tr><td>dfs.datanode.http.address</td><td>0.0.0.0:30075</td></tr>
<tr><td>dfs.datanode.ipc.address</td><td>0.0.0.0:30020</td></tr>
<tr><td>dfs.secondary.http.address</td><td>0.0.0.0:30090</td></tr>
<tr><td>mapred.job.tracker.http.address</td><td>jobtrackerhost:30030</td></tr>
<tr><td>mapred.task.tracker.http.address</td><td>0.0.0.0:30060</td></tr>
<tr><td>mapreduce.history.server.http.address</td><td>0.0.0.0:31111</td></tr>
<tr><td>templeton.port</td><td>30111</td></tr>
</table>

 **HDInsight 3.1 e 3.0 (HDP 2.1 e 2.0)**

<table border="1">
<tr><th>Nome</th><th>Valore</th></tr>
<tr><td>dfs.namenode.http-address</td><td>namenodehost:30070</td></tr>
<tr><td>dfs.namenode.https-address</td><td>headnodehost:30470</td></tr>
<tr><td>dfs.datanode.address</td><td>0.0.0.0:30010</td></tr>
<tr><td>dfs.datanode.http.address</td><td>0.0.0.0:30075</td></tr>
<tr><td>dfs.datanode.ipc.address</td><td>0.0.0.0:30020</td></tr>
<tr><td>dfs.namenode.secondary.http-address</td><td>0.0.0.0:30090</td></tr>
<tr><td>yarn.nodemanager.webapp.address</td><td>0.0.0.0:30060</td></tr>
<tr><td>templeton.port</td><td>30111</td></tr>
</table>

### <a name="dependencies"></a>Dipendenze
salve le dipendenze seguenti sono state aggiunte in HDInsight 3. x (HDP2.x):

* guice-servlet
* optiq-core
* javax.inject
* activation
* jsr305
* geronimo-jaspic_1.0_spec
* jul-to-slf4j
* java-xmlbuilder
* ant
* commons-compiler
* jdo-api
* commons-math3
* paranamer
* jaxb-impl
* stringtemplate
* eigenbase-xom
* jersey-servlet
* commons-exec
* jaxb-api
* jetty-all-server
* janino
* xercesImpl
* optiq-avatica
* jta
* eigenbase-properties
* groovy-all
* hamcrest-core
* mail
* linq4j
* jpam
* jersey-client
* aopalliance
* geronimo-annotation_1.0_spec
* ant-launcher
* jersey-guice
* xml-apis
* stax-api
* asm-commons
* asm-tree
* wadl
* geronimo-jta_1.1_spec
* guice
* leveldbjni-all
* velocity
* jettison
* snappy-java
* jetty-all
* commons-dbcp

Hello seguenti non sono presenti dipendenze in HDInsight 3. x (HDP2.x):

* jdeb
* kfs
* sqlline
* ivy
* aspectjrt
* json
* core
* jdo2-api
* avro-mapred
* datanucleus-enhancer
* jsp
* commons-logging-api
* commons-math
* JavaEWAH
* aspectjtools
* javolution
* hdfsproxy
* hbase
* snappy

### <a name="version-changes"></a>Modifiche della versione
Hello dopo le modifiche della versione sono stata apportata tra HDInsight 2. x (HDP1.x) e HDInsight 3. x (HDP2.x):

* metrics-core: ['2.1.2'] -> ['3.0.0']
* derbynet: ['10.4.2.0'] -> ['10.10.1.1']
* datanucleus: ['rdbms-3.0.8'] -> ['rdbms-3.2.9']
* jasper-compiler: ['5.5.12'] -> ['5.5.23']
* log4j: ['1.2.15', '1.2.16'] -> ['1.2.16', '1.2.17']
* derbyclient: ['10.4.2.0'] -> ['10.10.1.1']
* httpcore: ['4.2.4'] -> ['4.2.5']
* hsqldb: ['1.8.0.10'] -> ['2.0.0']
* jets3t: ['0.6.1'] -> ['0.9.0']
* protobuf-java: ['2.4.1'] -> ['2.5.0']
* derby: ['10.4.2.0'] -> ['10.10.1.1']
* jasper: ['runtime-5.5.12'] -> ['runtime-5.5.23']
* commons-daemon: ['1.0.1'] -> ['1.0.13']
* datanucleus-core: ['3.0.9'] -> ['3.2.10']
* datanucleus-api-jdo: ['3.0.7'] -> ['3.2.6']
* zookeeper: ['3.4.5.1.3.9.0-01320'] -> ['3.4.5.2.1.3.0-1948']
* bonecp: ['0.7.1.RELEASE'] -> ['
* 0.8.0.RELEASE']

### <a name="drivers"></a>Driver
driver Java Database Connectivity (JDBC) Hello per SQL Server viene utilizzata internamente da HDInsight e non viene utilizzato per operazioni esterne. Se si desidera tooconnect tooHDInsight tramite Open Database Connectivity (ODBC), utilizzare hello Hive driver ODBC per Microsoft. Per ulteriori informazioni, vedere [tooHDInsight connessione Excel con il Driver ODBC di Hive Microsoft hello](hdinsight-connect-excel-hive-odbc-driver.md).

### <a name="bug-fixes"></a>Correzioni di bug
Con questa versione, è stato aggiornato hello seguenti versioni di HDInsight con diverse correzioni di bug:

* HDInsight 2,1 (HDP 1,3)
* HDInsight 3,0 (HDP 2,0)
* HDInsight 3.1 (HDP 2.1)

## <a name="hortonworks-release-notes"></a>Note sulla versione di Hortonworks
Note sulla versione di hello Hortonworks piattaforme di dati (HDPs) vengono usati dai cluster di HDInsight versione sono disponibili in hello posizioni seguenti:

* HDInsight versione 3.1 utilizza una distribuzione di Hadoop basato su hello [Hortonworks Data Platform 2.1.7][hdp-2-1-7]. Si tratta di un cluster Hadoop hello predefinito creato quando si utilizza hello portale di Azure dopo il 7/11/2014. I cluster di HDInsight 3.1 creati prima di 7/11/2014 erano basati su hello [Hortonworks Data Platform 2.1.1][hdp-2-1-1]
* HDInsight versione 3.0 utilizza una distribuzione di Hadoop basato su hello [Hortonworks Data Platform 2.0][hdp-2-0-8].
* HDInsight versione 2.1 utilizza una distribuzione di Hadoop basato su hello [Hortonworks Data Platform 1.3][hdp-1-3-0].
* HDInsight versione 1.6 utilizza una distribuzione di Hadoop basato su hello [Hortonworks Data Platform 1.1][hdp-1-1-0].

[hdp-2-1-7]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html

[hdp-2-1-1]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.1/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.1.html

[hdp-2-0-8]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.8.0/bk_releasenotes_hdp_2.0/content/ch_relnotes-hdp2.0.8.0.html

[hdp-1-3-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-1.3.0/bk_releasenotes_hdp_1.x/content/ch_relnotes-hdp1.3.0_1.html

[hdp-1-1-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-Win-1.1/bk_releasenotes_HDP-Win/content/ch_relnotes-hdp-win-1.1.0_1.html

[nuget-link]: https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.HDInsight/

[webpi-link]: http://go.microsoft.com/?linkid=9811175&clcid=0x409

[hdinsight-install-spark]: ../hdinsight-hadoop-spark-install/
[hdinsight-r-scripts]: ../hdinsight-hadoop-r-scripts/
