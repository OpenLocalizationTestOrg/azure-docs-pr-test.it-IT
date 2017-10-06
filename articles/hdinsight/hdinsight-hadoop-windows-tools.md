---
title: aaaUse un PC Windows con Hadoop in HDInsight - Azure | Documenti Microsoft
description: Lavorare da un computer Windows in Hadoop in HDInsight. Gestire ed eseguire query sui cluster con gli strumenti di PowerShell, Visual Studio e Linux. Sviluppare soluzioni Big Data con .NET.
services: hdinsight
keywords: hadoop in windows, hadoop per windows
author: cjgronlund
manager: jhubbard
ms.author: cgronlun
ms.date: 05/17/2017
ms.topic: article
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 7c93f16e93349c0b8fb1abd55320c2c172b93aa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="work-in-hello-hadoop-ecosystem-on-hdinsight-from-a-windows-pc"></a>Lavorare in hello ecosistema di Hadoop in HDInsight da un PC Windows

Informazioni sulle opzioni di sviluppo e gestione in PC Windows hello per l'utilizzo nell'ecosistema di hello Hadoop in HDInsight. 

HDInsight si basa su componenti Apache Hadoop e Hadoop, tecnologie open source sviluppate in Linux. HDInsight versione 3.4 e successive Usa hello distribuzione Ubuntu Linux come hello sottostante del sistema operativo per cluster hello. Tuttavia, è possibile lavorare con HDInsight da un client Windows o l'ambiente di sviluppo Windows.

## <a name="use-powershell-for-deployment-and-management-tasks"></a>Usare PowerShell per attività di distribuzione e gestione
Azure PowerShell è un ambiente di scripting che è possibile utilizzare toocontrol e automatizzare le attività di distribuzione e gestione in HDInsight da Windows.

Esempi di attività che è possibile eseguire con PowerShell:

* [Creare cluster usando PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [Esecuzione di query Hive usando PowerShell](hdinsight-hadoop-use-hive-powershell.md)
* [Gestire cluster con PowerShell](hdinsight-administer-use-powershell.md)

Seguire i passaggi troppo[installare e configurare Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooget versione più recente di hello. Se si dispone di script che devono modificare toobe toouse hello nuovi cmdlet per Gestione risorse di Azure, vedere [migrare tooAzure strumenti di sviluppo basato su Gestione risorse per i cluster HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md).

## <a name="utilities-you-can-run-in-a-browser"></a>Utilità che è possibile eseguire in un browser
Hello utilità seguenti hanno un'interfaccia utente che viene eseguita in un browser web:
* **[Shell Cloud Azure (anteprima)](https://docs.microsoft.com/azure/cloud-shell/quickstart)**  è una shell da riga di comando interattivo che viene eseguito nel browser e dall'interno hello portale di Azure.
* **[Interfaccia utente Web Ambari](hdinsight-hadoop-manage-ambari.md)**  è una gestione e monitoraggio di utilità disponibile nel portale di Azure che può essere utilizzato toomanage diversi tipi di processi, ad esempio hello:
    * [Utilizzare Ambari con hello API REST](hdinsight-hadoop-manage-ambari-rest-api.md)
    * [vista Hive in Ambari](hdinsight-hadoop-use-hive-ambari-view.md)
    * [Vista Tez in Ambari](hdinsight-debug-ambari-tez-view.md)

## <a name="data-lake-hadoop-tools-for-visual-studio"></a>Strumenti Data Lake (Hadoop) per Visual Studio
Utilizzare Data Lake Tools per Visual Studio toodeploy e gestire le topologie di Storm. Data Lake Tools viene installato anche hello SCP.NET SDK, che consente le topologie di c# Storm toodevelop con Visual Studio.

Prima di passare toohello seguono esempi [installare, provare a Data Lake Tools per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md). 

Esempi di attività che è possibile eseguire con Visual Studio e gli strumenti Data Lake per Visual Studio:
* [Distribuire e gestire topologie Storm da Visual Studio](hdinsight-storm-deploy-monitor-topology-linux.md)
* [Sviluppare topologie C# per Storm con Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md). bits Hello includono modelli di esempio per le topologie di Storm è possibile connettersi toodatabases, ad esempio Azure Cosmos DB e il Database SQL.

## <a name="visual-studio-and-hello-net-sdk"></a>Visual Studio e .NET SDK hello 

È possibile utilizzare Visual Studio con i cluster toomanage SDK .NET di hello e sviluppo di applicazioni per dati di grandi dimensioni. È possibile utilizzare altri IDE per hello seguenti attività, ma sono riportati alcuni esempi in Visual Studio.

Esempi di attività che è possibile eseguire con hello SDK .NET in Visual Studio:
* [Creare cluster e lavorare in HDInsight da un'applicazione .NET Framework](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)
* [Esecuzione di query Hive utilizzando hello .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md)
* [Usare funzioni C# definite dall'utente con lo streaming Hive e Pig in Hadoop](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

> Suggerimento Se si esegue soluzioni .NET con i cluster HDInsight basati su Windows, è un tooplan tempestivamente una migrazione basata su tooLinux cluster. Per ulteriori informazioni, vedere [soluzione .NET di eseguire la migrazione per HDInsight basati su Windows basato su tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).

## <a name="intellij-idea-and-eclipse-ide-for-spark-clusters"></a>Intellij IDEA e IDE di Eclipse per cluster Spark
Entrambi [Intellij IDEA](https://www.jetbrains.com/idea/download) hello e [Eclipse IDE](https://www.eclipse.org/downloads/) può essere utilizzato per:
* Sviluppare e inviare un'applicazione Spark in Scala in un cluster HDInsight Spark.
* Accedere a risorse cluster di Spark.
* Sviluppare ed eseguire un'applicazione Spark in Scala localmente.

Questi articoli mostrano come: 
* Intellij IDEA: [applicazioni Spark Create mediante Azure Toolkit per plug-in Intellij hello e hello Scala SDK.](hdinsight-apache-spark-intellij-tool-plugin.md)
* Eclipse IDE o IDE Scala per Eclipse: [applicazioni creare Spark e hello Azure Toolkit per Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md) 


## <a name="notebooks-on-spark-for-data-scientists"></a>Notebook su Spark per data scientist 
I cluster Apache Spark in HDInsight includono notebook e kernel Zeppelin che possono essere usati con notebook Jupyter. 

* [Informazioni su come i cluster con le applicazioni server Jupyter notebook tootest Spark toouse kernel in Spark](hdinsight-apache-spark-zeppelin-notebook.md)
* [Informazioni su come notebook Zeppelin toouse in Spark cluster processi Spark toorun](hdinsight-apache-spark-jupyter-notebook-kernels.md) 


## <a name="run-linux-based-tools-and-technologies-on-windows"></a>Eseguire strumenti e tecnologie basate su Linux in Windows

Se si verifica una situazione in cui è necessario utilizzare uno strumento o una tecnologia che è disponibile solo in Linux, prendere in considerazione hello le opzioni seguenti:

* **Bash (beta) in Windows 10** fornisce un sottosistema Linux in Windows. Bash consente di eseguire l'utilità Linux senza la necessità di un'installazione di Linux dedicata toomaintain toodirectly. [Installare ed eseguire beta Bash hello in Windows 10](https://msdn.microsoft.com/commandline/wsl/install_guide)
* **Docker per Windows** consente l'accesso gli strumenti basati su Linux toomany e può essere eseguito direttamente da Windows. Ad esempio, è possibile utilizzare client di Docker toorun hello Beeline per Hive direttamente da Windows. È possibile anche usare Docker toorun notebook Jupyter locale e connettersi in remoto tooSpark in HDInsight. [Introduzione a Docker per Windows](https://docs.docker.com/docker-for-windows/)
* **[MobaXTerm](http://mobaxterm.mobatek.net/)**  permette di sistema di file di toographically Sfoglia hello cluster tramite una connessione SSH.

## <a name="next-steps"></a>Passaggi successivi
Se si è nuovo tooworking in cluster basati su Linux, vedere hello seguire articoli:
* [Configurare Hadoop, Kafka, Spark o altri cluster](hdinsight-hadoop-provision-linux-clusters.md)
* [Suggerimenti per i cluster HDInsight in Linux](hdinsight-hadoop-linux-information.md)