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
# <a name="install-or-update-mono-on-hdinsight"></a><span data-ttu-id="94840-104">Installare o aggiornare Mono in HDInsight</span><span class="sxs-lookup"><span data-stu-id="94840-104">Install or update Mono on HDInsight</span></span>

<span data-ttu-id="94840-105">Informazioni su come tooinstall una versione specifica di [Mono](https://www.mono-project.com) in HDInsight 3.4 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="94840-105">Learn how tooinstall a specific version of [Mono](https://www.mono-project.com) on HDInsight 3.4 or higher.</span></span>

<span data-ttu-id="94840-106">Mono viene installato su HDInsight 3.4 e versioni successive e viene utilizzato toorun applicazioni .NET.</span><span class="sxs-lookup"><span data-stu-id="94840-106">Mono is installed on HDInsight 3.4 and higher, and is used toorun .NET applications.</span></span> <span data-ttu-id="94840-107">Per informazioni sulla versione di hello di Mono incluso con ogni versione di HDInsight, vedere [il controllo delle versioni di HDInsight componente](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="94840-107">For information on hello version of Mono included with each HDInsight version, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="94840-108">tooinstall una versione diversa nel cluster, utilizzare hello genera script azione in questo documento.</span><span class="sxs-lookup"><span data-stu-id="94840-108">tooinstall a different version on your cluster, use hello script action in this document.</span></span> 

## <a name="how-it-works"></a><span data-ttu-id="94840-109">Funzionamento</span><span class="sxs-lookup"><span data-stu-id="94840-109">How it works</span></span>

<span data-ttu-id="94840-110">Questo script accetta hello seguente parametro:</span><span class="sxs-lookup"><span data-stu-id="94840-110">This script accepts hello following parameter:</span></span>

* <span data-ttu-id="94840-111">__Numero di versione mono__: versione di hello di tooinstall Mono.</span><span class="sxs-lookup"><span data-stu-id="94840-111">__Mono version number__: hello version of Mono tooinstall.</span></span> <span data-ttu-id="94840-112">versione di Hello deve essere disponibile dal [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span><span class="sxs-lookup"><span data-stu-id="94840-112">hello version must be available from [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span></span>

<span data-ttu-id="94840-113">script di Hello installa hello Mono pacchetti seguenti:</span><span class="sxs-lookup"><span data-stu-id="94840-113">hello script installs hello following Mono packages:</span></span>

* <span data-ttu-id="94840-114">__mono-complete__</span><span class="sxs-lookup"><span data-stu-id="94840-114">__mono-complete__</span></span>

* <span data-ttu-id="94840-115">__ca-certificates-mono__</span><span class="sxs-lookup"><span data-stu-id="94840-115">__ca-certificates-mono__</span></span>

## <a name="hello-script"></a><span data-ttu-id="94840-116">script Hello</span><span class="sxs-lookup"><span data-stu-id="94840-116">hello script</span></span>

<span data-ttu-id="94840-117">__Percorso dello script__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span><span class="sxs-lookup"><span data-stu-id="94840-117">__Script location__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span></span>

<span data-ttu-id="94840-118">__Requisiti__:</span><span class="sxs-lookup"><span data-stu-id="94840-118">__Requirements__:</span></span>

* <span data-ttu-id="94840-119">script Hello deve essere applicato a hello __nodi head__ e __nodi di lavoro__.</span><span class="sxs-lookup"><span data-stu-id="94840-119">hello script must be applied on hello __head nodes__ and __worker nodes__.</span></span>

## <a name="toouse-hello-script"></a><span data-ttu-id="94840-120">script hello toouse</span><span class="sxs-lookup"><span data-stu-id="94840-120">toouse hello script</span></span>

<span data-ttu-id="94840-121">Per informazioni su come toouse questo script con HDInsight, vedere hello [ai cluster HDInsight basati su Linux personalizzare mediante l'azione di script](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) documento.</span><span class="sxs-lookup"><span data-stu-id="94840-121">For information on how toouse this script with HDInsight, see hello [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span> <span data-ttu-id="94840-122">È possibile utilizzare uno script di hello tramite hello portale di Azure, Azure PowerShell, o hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="94840-122">You can use hello script through hello Azure portal, Azure PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="94840-123">Mentre l'esempio hello documento azione script, utilizzare hello seguente URI:</span><span class="sxs-lookup"><span data-stu-id="94840-123">While following hello script action document, use hello following URI:</span></span>

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> <span data-ttu-id="94840-124">Quando si configura HDInsight con questo script, contrassegnare script hello come __Persisted__.</span><span class="sxs-lookup"><span data-stu-id="94840-124">When configuring HDInsight with this script, mark hello script as __Persisted__.</span></span> <span data-ttu-id="94840-125">Questa impostazione consente di HDInsight tooapply nodi tooworker di script hello aggiunti tramite operazioni di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="94840-125">This setting allows HDInsight tooapply hello script tooworker nodes added through scaling operations.</span></span>


## <a name="next-steps"></a><span data-ttu-id="94840-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="94840-126">Next steps</span></span>

<span data-ttu-id="94840-127">Si è appreso come tooupgrade o installare una versione specifica di Mono in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="94840-127">You have learned how tooupgrade or install a specific version of Mono on HDInsight.</span></span> <span data-ttu-id="94840-128">Per ulteriori informazioni sull'uso di applicazioni .NET con Mono in HDInsight, vedere hello seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="94840-128">For more information on using .NET applications with Mono on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="94840-129">Usare C# con lo streaming di MapReduce su Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="94840-129">Use .NET for streaming MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [<span data-ttu-id="94840-130">Usare le funzioni definite dall'utente C# con lo streaming Hive e Pig in Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="94840-130">Use .NET with Hive and Pig on HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)
* [<span data-ttu-id="94840-131">Sviluppare topologie C# per Apache Storm in HDInsight tramite gli strumenti Hadoop per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="94840-131">Develop C# solutions with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="94840-132">La migrazione di soluzioni .NET basato su tooLinux HDInsight</span><span class="sxs-lookup"><span data-stu-id="94840-132">Migrate .NET solutions tooLinux-based HDInsight</span></span>](hdinsight-hadoop-migrate-dotnet-to-linux.md)

<span data-ttu-id="94840-133">Per altre informazioni sulle azioni di script, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="94840-133">For more information on using script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>