---
title: Installare o aggiornare Mono in HDInsight - Azure | Microsoft Docs
description: Informazioni su come usare una versione specifica di Mono con cluster HDInsight. Mono viene usato per eseguire applicazioni .NET in cluster HDInsight basati su Linux.
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
ms.openlocfilehash: fd284542e1de65f323f1e3a092689f847e025be6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="install-or-update-mono-on-hdinsight"></a><span data-ttu-id="490d9-104">Installare o aggiornare Mono in HDInsight</span><span class="sxs-lookup"><span data-stu-id="490d9-104">Install or update Mono on HDInsight</span></span>

<span data-ttu-id="490d9-105">Informazioni su come installare una versione specifica di [Mono](https://www.mono-project.com) in HDInsight 3.4 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="490d9-105">Learn how to install a specific version of [Mono](https://www.mono-project.com) on HDInsight 3.4 or higher.</span></span>

<span data-ttu-id="490d9-106">Mono viene installato in HDInsight 3.4 e versioni successive per eseguire applicazioni .NET.</span><span class="sxs-lookup"><span data-stu-id="490d9-106">Mono is installed on HDInsight 3.4 and higher, and is used to run .NET applications.</span></span> <span data-ttu-id="490d9-107">Per informazioni sulla versione di Mono inclusa in ogni versione di HDInsight, vedere [Componenti e versioni di Hadoop disponibili in HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="490d9-107">For information on the version of Mono included with each HDInsight version, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="490d9-108">Per installare una versione diversa nel cluster, usare l'azione di script presente in questo documento.</span><span class="sxs-lookup"><span data-stu-id="490d9-108">To install a different version on your cluster, use the script action in this document.</span></span> 

## <a name="how-it-works"></a><span data-ttu-id="490d9-109">Funzionamento</span><span class="sxs-lookup"><span data-stu-id="490d9-109">How it works</span></span>

<span data-ttu-id="490d9-110">Questo script accetta il parametro seguente:</span><span class="sxs-lookup"><span data-stu-id="490d9-110">This script accepts the following parameter:</span></span>

* <span data-ttu-id="490d9-111">__Numero di versione di Mono__: versione di Mono da installare.</span><span class="sxs-lookup"><span data-stu-id="490d9-111">__Mono version number__: The version of Mono to install.</span></span> <span data-ttu-id="490d9-112">La versione deve essere disponibile sul sito Web all'indirizzo [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span><span class="sxs-lookup"><span data-stu-id="490d9-112">The version must be available from [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span></span>

<span data-ttu-id="490d9-113">Lo script installa i pacchetti Mono seguenti:</span><span class="sxs-lookup"><span data-stu-id="490d9-113">The script installs the following Mono packages:</span></span>

* <span data-ttu-id="490d9-114">__mono-complete__</span><span class="sxs-lookup"><span data-stu-id="490d9-114">__mono-complete__</span></span>

* <span data-ttu-id="490d9-115">__ca-certificates-mono__</span><span class="sxs-lookup"><span data-stu-id="490d9-115">__ca-certificates-mono__</span></span>

## <a name="the-script"></a><span data-ttu-id="490d9-116">Lo script</span><span class="sxs-lookup"><span data-stu-id="490d9-116">The script</span></span>

<span data-ttu-id="490d9-117">__Percorso dello script__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span><span class="sxs-lookup"><span data-stu-id="490d9-117">__Script location__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span></span>

<span data-ttu-id="490d9-118">__Requisiti__:</span><span class="sxs-lookup"><span data-stu-id="490d9-118">__Requirements__:</span></span>

* <span data-ttu-id="490d9-119">Lo script deve essere applicato a di __nodi head__ e ai __nodi del ruolo di lavoro__.</span><span class="sxs-lookup"><span data-stu-id="490d9-119">The script must be applied on the __head nodes__ and __worker nodes__.</span></span>

## <a name="to-use-the-script"></a><span data-ttu-id="490d9-120">Per usare lo script</span><span class="sxs-lookup"><span data-stu-id="490d9-120">To use the script</span></span>

<span data-ttu-id="490d9-121">Per informazioni su come usare questo script con HDInsight, vedere il documento [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster).</span><span class="sxs-lookup"><span data-stu-id="490d9-121">For information on how to use this script with HDInsight, see the [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span> <span data-ttu-id="490d9-122">È possibile usare lo script tramite il portale di Azure, Azure PowerShell o l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="490d9-122">You can use the script through the Azure portal, Azure PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="490d9-123">Quando si segue il documento di azione di script, usare l'URI seguente:</span><span class="sxs-lookup"><span data-stu-id="490d9-123">While following the script action document, use the following URI:</span></span>

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> <span data-ttu-id="490d9-124">Durante la configurazione di HDInsight con lo script, contrassegnare quest'ultimo con l'opzione __Con salvataggio permanente__.</span><span class="sxs-lookup"><span data-stu-id="490d9-124">When configuring HDInsight with this script, mark the script as __Persisted__.</span></span> <span data-ttu-id="490d9-125">Questa impostazione consente a HDInsight di applicare lo script ai nodi del ruolo di lavoro aggiunti tramite operazioni di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="490d9-125">This setting allows HDInsight to apply the script to worker nodes added through scaling operations.</span></span>


## <a name="next-steps"></a><span data-ttu-id="490d9-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="490d9-126">Next steps</span></span>

<span data-ttu-id="490d9-127">Si è appreso come aggiornare o installare una versione specifica di Mono in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="490d9-127">You have learned how to upgrade or install a specific version of Mono on HDInsight.</span></span> <span data-ttu-id="490d9-128">Per altre informazioni sull'uso di applicazioni .NET con Mono in HDInsight, vedere i documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="490d9-128">For more information on using .NET applications with Mono on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="490d9-129">Usare C# con lo streaming di MapReduce su Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="490d9-129">Use .NET for streaming MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [<span data-ttu-id="490d9-130">Usare le funzioni definite dall'utente C# con lo streaming Hive e Pig in Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="490d9-130">Use .NET with Hive and Pig on HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)
* [<span data-ttu-id="490d9-131">Sviluppare topologie C# per Apache Storm in HDInsight tramite gli strumenti Hadoop per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="490d9-131">Develop C# solutions with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="490d9-132">Eseguire la migrazione di soluzioni .NET per HDInsight basato su Windows a HDInsight basato su Linux</span><span class="sxs-lookup"><span data-stu-id="490d9-132">Migrate .NET solutions to Linux-based HDInsight</span></span>](hdinsight-hadoop-migrate-dotnet-to-linux.md)

<span data-ttu-id="490d9-133">Per altre informazioni sulle azioni di script, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="490d9-133">For more information on using script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>