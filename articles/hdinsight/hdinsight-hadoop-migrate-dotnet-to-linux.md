---
title: aaaUse .NET con Hadoop MapReduce in HDInsight basati su Linux - Azure | Documenti Microsoft
description: Informazioni su come le applicazioni .NET toouse per lo streaming MapReduce in HDInsight basati su Linux.
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5a4e6dc1b4dafa8cc40780e3371fa4b8ba3e3d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-toolinux-based-hdinsight"></a>La migrazione di soluzioni .NET per HDInsight basati su Windows basato su tooLinux HDInsight

Utilizzare i cluster HDInsight basati su Linux [Mono (https://mono-project.com)](https://mono-project.com) toorun le applicazioni .NET. Mono consente toouse di componenti .NET, ad esempio applicazioni MapReduce con HDInsight basati su Linux. In questo documento, illustrate le modalità di creazione di soluzioni .NET toomigrate per toowork cluster HDInsight basati su Windows con Mono in HDInsight basati su Linux.

## <a name="mono-compatibility-with-net"></a>Compatibilità Mono con .NET

La versione Mono 4.2.1 è inclusa nella versione 3.5 di HDInsight. Per ulteriori informazioni sulla versione di hello di Mono incluso in HDInsight, vedere [versioni dei componenti di HDInsight](hdinsight-component-versioning.md). tooinstall una versione specifica di Mono, vedere hello [installazione o aggiornamento Mono](hdinsight-hadoop-install-mono.md) documento.

Per informazioni dettagliate sulla compatibilità tra .NET e Mono, vedere hello [compatibilità Mono (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) documento.

> [!IMPORTANT]
> framework SCP.NET Hello è compatibile con Mono. Per ulteriori informazioni sull'uso di SCP.NET con Mono, vedere [topologie toodevelop c# utilizzare Visual Studio per Apache Storm in HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="automated-portability-analysis"></a>Analisi di portabilità automatizzata

Hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) può essere utilizzato toogenerate un report di incompatibilità tra l'applicazione e Mono. Usare l'applicazione di hello seguendo i passaggi tooconfigure hello analyzer toocheck per garantire la portabilità Mono:

1. Installare hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer). Durante l'installazione, selezionare la versione hello di Visual Studio toouse.

2. Visual Studio 2015, selezionare __Analizza__ > __Portability Analyzer impostazioni__e assicurarsi che __4.5__ archiviazione hello __Mono__  sezione.

    ![4.5 selezionati nella sezione Mono per le impostazioni di hello analyzer](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    Selezionare __OK__ configurazione hello toosave.

3. Selezionare __Analizza__ > __Analyze Assembly Portability__ (Analizza portabilità assembly). Selezionare l'assembly hello che contiene la soluzione, quindi __aprire__ toobegin analysis.

4. Una volta completata l'analisi, selezionare __Analizza__ > __View analysis reports__ (Visualizza rapporti di analisi). In __risultati dell'analisi portabilità__selezionare __aprire report__ tooopen un report.

    ![Finestra di dialogo dei risultati dell'analizzatore di portabilità](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> analizzatore Hello non può intercettare tutti i problemi con la soluzione. Ad esempio, un percorso di file di `c:\temp\file.txt` viene considerata OK perché Mono viene eseguito in Windows e hello percorso sia valido in tale contesto. Percorso hello, tuttavia, non è valido in una piattaforma Linux.

## <a name="manual-portability-analysis"></a>Analisi di portabilità manuale

Esecuzione di un controllo manuale del codice utilizzando le informazioni di hello in hello [la portabilità dell'applicazione (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) documento.

## <a name="modify-and-build"></a>Modificare e compilare

È possibile continuare le soluzioni .NET toouse toobuild di Visual Studio per HDInsight. Tuttavia, è necessario assicurarsi di che tale progetto hello è configurato toouse .NET Framework 4.5.

## <a name="deploy-and-test"></a>Distribuire e testare

Dopo aver modificato la soluzione utilizzando hello indicazioni da hello .NET Portability Analyzer o da un'analisi manuale, è necessario eseguirne il test con HDInsight. Testare la soluzione hello in un cluster HDInsight basati su Linux può rivelare problemi complessi che necessitano di toobe corretti. Si consiglia di abilitare l'accesso aggiuntivo dell'applicazione durante l'esecuzione del test.

Per ulteriori informazioni sull'accesso ai registri, vedere hello seguenti documenti:

* [Accedere ai log delle applicazioni YARN in HDInsight basato su Linux](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a>Passaggi successivi

* [Use C# with MapReduce on HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md) (Usare C# con MapReduce in HDInsight)

* [Usare le funzioni definite dall'utente C# con lo streaming Hive e Pig in Hadoop in HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [Sviluppare topologie C# per Apache Storm in HDInsight tramite gli strumenti Hadoop per Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)