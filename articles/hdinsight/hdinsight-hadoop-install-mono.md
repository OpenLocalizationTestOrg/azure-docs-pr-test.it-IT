---
title: aaaInstall o aggiornare Mono in HDInsight - Azure | Documenti Microsoft
description: "Informazioni su come toouse una versione specifica di Mono con cluster HDInsight. Mono è applicazioni .NET toorun utilizzati nei cluster HDInsight basati su Linux."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: hdinsightactive
ms.openlocfilehash: 1e8a8aaeff231c93a9e232379448517b326da965
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-or-update-mono-on-hdinsight"></a>Installare o aggiornare Mono in HDInsight

Informazioni su come tooinstall una versione specifica di [Mono](https://www.mono-project.com) in HDInsight 3.4 o versione successiva.

Mono viene installato su HDInsight 3.4 e versioni successive e viene utilizzato toorun applicazioni .NET. Per informazioni sulla versione di hello di Mono incluso con ogni versione di HDInsight, vedere [il controllo delle versioni di HDInsight componente](hdinsight-component-versioning.md). tooinstall una versione diversa nel cluster, utilizzare hello genera script azione in questo documento. 

## <a name="how-it-works"></a>Funzionamento

Questo script accetta hello seguente parametro:

* __Numero di versione mono__: versione di hello di tooinstall Mono. versione di Hello deve essere disponibile dal [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).

script di Hello installa hello Mono pacchetti seguenti:

* __mono-complete__

* __ca-certificates-mono__

## <a name="hello-script"></a>script Hello

__Percorso dello script__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)

__Requisiti__:

* script Hello deve essere applicato a hello __nodi head__ e __nodi di lavoro__.

## <a name="toouse-hello-script"></a>script hello toouse

Per informazioni su come toouse questo script con HDInsight, vedere hello [ai cluster HDInsight basati su Linux personalizzare mediante l'azione di script](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) documento. È possibile utilizzare uno script di hello tramite hello portale di Azure, Azure PowerShell, o hello CLI di Azure.

Mentre l'esempio hello documento azione script, utilizzare hello seguente URI:

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> Quando si configura HDInsight con questo script, contrassegnare script hello come __Persisted__. Questa impostazione consente di HDInsight tooapply nodi tooworker di script hello aggiunti tramite operazioni di ridimensionamento.


## <a name="next-steps"></a>Passaggi successivi

Si è appreso come tooupgrade o installare una versione specifica di Mono in HDInsight. Per ulteriori informazioni sull'uso di applicazioni .NET con Mono in HDInsight, vedere hello seguenti documenti:

* [Usare C# con lo streaming di MapReduce su Hadoop in HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [Usare le funzioni definite dall'utente C# con lo streaming Hive e Pig in Hadoop in HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)
* [Sviluppare topologie C# per Apache Storm in HDInsight tramite gli strumenti Hadoop per Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [La migrazione di soluzioni .NET basato su tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)

Per altre informazioni sulle azioni di script, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md)