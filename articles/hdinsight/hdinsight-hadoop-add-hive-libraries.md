---
title: Aggiungere librerie Hive durante la creazione del cluster HDInsight - Azure | Microsoft Docs
description: Informazioni su come aggiungere librerie Hive (file con estensione jar) a un cluster HDInsight durante la creazione del cluster.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 2fd74b8d-c006-45c6-a9e2-72ff5d2d978a
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 3412864384961e8820d6700c1bf22a4cae64ba4b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a><span data-ttu-id="7371e-103">Aggiungere librerie Hive personalizzate durante la creazione del cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="7371e-103">Add custom Hive libraries when creating your HDInsight cluster</span></span>

<span data-ttu-id="7371e-104">Se sono disponibili librerie di uso frequente con Hive in HDInsight, questo documento contiene informazioni sull'uso di un'azione script per precaricare le librerie durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="7371e-104">If you have libraries that you use frequently with Hive on HDInsight, this document contains information on using a Script Action to pre-load the libraries during cluster creation.</span></span> <span data-ttu-id="7371e-105">Le librerie aggiunte usando i passaggi in questo documento sono disponibili in modo globale in Hive, non è necessario utilizzare [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) per caricarli.</span><span class="sxs-lookup"><span data-stu-id="7371e-105">Libraries added using the steps in this document are globally available in Hive - there is no need to use [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) to load them.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="7371e-106">Funzionamento</span><span class="sxs-lookup"><span data-stu-id="7371e-106">How it works</span></span>

<span data-ttu-id="7371e-107">Quando si crea un cluster, è possibile specificare facoltativamente un'azione script che esegue uno script nei nodi del cluster durante la creazione.</span><span class="sxs-lookup"><span data-stu-id="7371e-107">When creating a cluster, you can optionally specify a Script Action that runs a script on the cluster nodes while they are being created.</span></span> <span data-ttu-id="7371e-108">Lo script in questo documento accetta un singolo parametro, ovvero un percorso WASB che contiene le librerie (archiviate come file con estensione JAR) da precaricare.</span><span class="sxs-lookup"><span data-stu-id="7371e-108">The script in this document accepts a single parameter, which is a WASB location that contains the libraries (stored as jar files) to be pre-loaded.</span></span>

<span data-ttu-id="7371e-109">Durante la creazione del cluster, lo script enumera i file, li copia nella directory `/usr/lib/customhivelibs/` nei nodi head e di lavoro, quindi li aggiunge alla proprietà `hive.aux.jars.path` nel file `core-site.xml`.</span><span class="sxs-lookup"><span data-stu-id="7371e-109">During cluster creation, the script enumerates the files, copies them to the `/usr/lib/customhivelibs/` directory on head and worker nodes, then adds them to the `hive.aux.jars.path` property in the `core-site.xml` file.</span></span> <span data-ttu-id="7371e-110">Nei cluster basati su Linux, aggiorna anche il file `hive-env.sh` con il percorso dei file.</span><span class="sxs-lookup"><span data-stu-id="7371e-110">On Linux-based clusters, it also updates the `hive-env.sh` file with the location of the files.</span></span>

> [!NOTE]
> <span data-ttu-id="7371e-111">L'uso delle azioni script in questo articolo rende le librerie disponibili negli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="7371e-111">Using the script actions in this article makes the libraries available in the following scenarios:</span></span>
>
> * <span data-ttu-id="7371e-112">**HDInsight basato su Linux**: quando si usa un client Hive, **WebHCat**, e **HiveServer2**.</span><span class="sxs-lookup"><span data-stu-id="7371e-112">**Linux-based HDInsight** - when using the a Hive client, **WebHCat**, and **HiveServer2**.</span></span>
> * <span data-ttu-id="7371e-113">**HDInsight basato su Windows**, quando si usa un client Hive e **WebHCat**.</span><span class="sxs-lookup"><span data-stu-id="7371e-113">**Windows-based HDInsight** - when using the Hive client and **WebHCat**.</span></span>

## <a name="the-script"></a><span data-ttu-id="7371e-114">Lo script</span><span class="sxs-lookup"><span data-stu-id="7371e-114">The script</span></span>

<span data-ttu-id="7371e-115">**Percorso dello script**</span><span class="sxs-lookup"><span data-stu-id="7371e-115">**Script location**</span></span>

<span data-ttu-id="7371e-116">Per i **cluster basati su Linux**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="7371e-116">For **Linux-based clusters**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span></span>

<span data-ttu-id="7371e-117">Per i **cluster basati su Windows**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span><span class="sxs-lookup"><span data-stu-id="7371e-117">For **Windows-based clusters**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7371e-118">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="7371e-118">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7371e-119">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7371e-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="7371e-120">**Requisiti**</span><span class="sxs-lookup"><span data-stu-id="7371e-120">**Requirements**</span></span>

* <span data-ttu-id="7371e-121">Gli script devono essere applicati ai **nodi head** e ai **nodi di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="7371e-121">The scripts must be applied to both the **Head nodes** and **Worker nodes**.</span></span>

* <span data-ttu-id="7371e-122">I file con estensione jar da installare devono essere memorizzati nell'archivio BLOB di Azure in un **singolo contenitore**.</span><span class="sxs-lookup"><span data-stu-id="7371e-122">The jars you wish to install must be stored in Azure Blob Storage in a **single container**.</span></span>

* <span data-ttu-id="7371e-123">L'account di archiviazione contenente la libreria dei file con estensione jar **deve** essere collegato al cluster HDInsight durante la creazione.</span><span class="sxs-lookup"><span data-stu-id="7371e-123">The storage account containing the library of jar files **must** be linked to the HDInsight cluster during creation.</span></span> <span data-ttu-id="7371e-124">Deve essere l'account di archiviazione predefinito o un account aggiunto tramite la __configurazione facoltativa__.</span><span class="sxs-lookup"><span data-stu-id="7371e-124">It must either be the default storage account, or an account added through __optional configuration__.</span></span>

* <span data-ttu-id="7371e-125">Il percorso WASB al contenitore deve essere specificato come parametro dell'azione script.</span><span class="sxs-lookup"><span data-stu-id="7371e-125">The WASB path to the container must be specified as a parameter to the Script Action.</span></span> <span data-ttu-id="7371e-126">Ad esempio, se i file con estensione jar sono archiviati in un contenitore denominato **libs** in un account di archiviazione denominato **mystorage**, il parametro deve essere **wasb://libs@mystorage.blob.core.windows.net/**.</span><span class="sxs-lookup"><span data-stu-id="7371e-126">For example, if the jars are stored in a container named **libs** on a storage account named **mystorage**, the parameter would be **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="7371e-127">In questo documento si presuppone che un account di archiviazione e un contenitore BLOB siano già stati creati e che i file siano stati caricati nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="7371e-127">This document assumes that you have already create a storage account, blob container, and uploaded the files to it.</span></span>
  >
  > <span data-ttu-id="7371e-128">Se non è stato creato un account di archiviazione, è possibile farlo tramite il [Portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7371e-128">If you have not created a storage account, you can do so through the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7371e-129">È quindi possibile usare un'utilità, ad esempio [Azure Storage Explorer](http://storageexplorer.com/) (Esplora archivi di Azure), per creare un contenitore nell'account e caricarvi i file.</span><span class="sxs-lookup"><span data-stu-id="7371e-129">You can then use a utility such as [Azure Storage Explorer](http://storageexplorer.com/) to create a container in the account and upload files to it.</span></span>

## <a name="create-a-cluster-using-the-script"></a><span data-ttu-id="7371e-130">Creare un cluster usando lo script</span><span class="sxs-lookup"><span data-stu-id="7371e-130">Create a cluster using the script</span></span>

> [!NOTE]
> <span data-ttu-id="7371e-131">La procedura seguente consente di creare un cluster HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="7371e-131">The following steps create a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="7371e-132">Per creare un cluster basato su Windows, selezionare **Windows** come sistema operativo del cluster durante la creazione del cluster e usare lo script di Windows (PowerShell) invece dello script bash.</span><span class="sxs-lookup"><span data-stu-id="7371e-132">To create a Windows-based cluster, select **Windows** as the cluster OS when creating the cluster, and use the Windows (PowerShell) script instead of the bash script.</span></span>
>
> <span data-ttu-id="7371e-133">È anche possibile usare Azure PowerShell o HDInsight .NET SDK per creare un cluster con questo script.</span><span class="sxs-lookup"><span data-stu-id="7371e-133">You can also use Azure PowerShell or the HDInsight .NET SDK to create a cluster using this script.</span></span> <span data-ttu-id="7371e-134">Per altre informazioni sull'uso di questi metodi, vedere [Personalizzare i cluster HDInsight con azioni script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7371e-134">For more information on using these methods, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="7371e-135">Avviare il provisioning di un cluster seguendo i passaggi descritti in [Effettuare il provisioning di cluster HDInsight in Linux](hdinsight-hadoop-provision-linux-clusters.md) senza completarlo.</span><span class="sxs-lookup"><span data-stu-id="7371e-135">Start provisioning a cluster by using the steps in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md), but do not complete provisioning.</span></span>

2. <span data-ttu-id="7371e-136">Nel pannello **Configurazione facoltativa** selezionare **Azioni script** e specificare le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7371e-136">On the **Optional Configuration** blade, select **Script Actions**, and provide the following information:</span></span>

   * <span data-ttu-id="7371e-137">**NOME**: immettere un nome descrittivo per l'azione script.</span><span class="sxs-lookup"><span data-stu-id="7371e-137">**NAME**: Enter a friendly name for the script action.</span></span>

   * <span data-ttu-id="7371e-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span><span class="sxs-lookup"><span data-stu-id="7371e-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span></span>

   * <span data-ttu-id="7371e-139">**HEAD**: selezionare questa opzione.</span><span class="sxs-lookup"><span data-stu-id="7371e-139">**HEAD**: Check this option.</span></span>

   * <span data-ttu-id="7371e-140">**LAVORO**: selezionare questa opzione.</span><span class="sxs-lookup"><span data-stu-id="7371e-140">**WORKER**: Check this option.</span></span>

   * <span data-ttu-id="7371e-141">**ZOOKEEPER**: lasciare vuoto questo campo.</span><span class="sxs-lookup"><span data-stu-id="7371e-141">**ZOOKEEPER**: Leave this blank.</span></span>

   * <span data-ttu-id="7371e-142">**PARAMETRI**: immettere l'indirizzo WASB per l'account di archiviazione e il contenitore che contiene i file con estensione jar.</span><span class="sxs-lookup"><span data-stu-id="7371e-142">**PARAMETERS**: Enter the WASB address to the container and storage account that contains the jars.</span></span> <span data-ttu-id="7371e-143">Ad esempio, **wasb://libs@mystorage.blob.core.windows.net/**.</span><span class="sxs-lookup"><span data-stu-id="7371e-143">For example, **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

3. <span data-ttu-id="7371e-144">Nella parte inferiore di **Azioni di script** usare il pulsante **Seleziona** per salvare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="7371e-144">At the bottom of the **Script Actions**, use the **Select** button to save the configuration.</span></span>

4. <span data-ttu-id="7371e-145">Nel pannello **Configurazione facoltativa** selezionare **Account di archiviazione collegati** e il collegamento **Aggiungi una chiave di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="7371e-145">On the **Optional Configuration** blade, select **Linked Storage Accounts** and select the **Add a storage key** link.</span></span> <span data-ttu-id="7371e-146">Selezionare l'account di archiviazione che contiene i file con estensione jar e quindi usare i pulsanti di **selezione** per salvare le impostazioni e tornare al pannello **Configurazione facoltativa**.</span><span class="sxs-lookup"><span data-stu-id="7371e-146">Select the storage account that contains the jars, and then use the **select** buttons to save settings and return the **Optional Configuration** blade.</span></span>

5. <span data-ttu-id="7371e-147">Usare il pulsante **Seleziona** nella parte inferiore del pannello **Configurazione facoltativa** per salvare le informazioni relative alla configurazione facoltativa.</span><span class="sxs-lookup"><span data-stu-id="7371e-147">Use the **Select** button at the bottom of the **Optional Configuration** blade to save the optional configuration information.</span></span>

6. <span data-ttu-id="7371e-148">Continuare il provisioning del cluster come descritto in [Effettuare il provisioning dei cluster HDInsight in Linux](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="7371e-148">Continue provisioning the cluster as described in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="7371e-149">Al termine della creazione del cluster, sarà possibile usare i file con estensione JAR aggiunti tramite questo script da Hive senza dover usare l'istruzione `ADD JAR`.</span><span class="sxs-lookup"><span data-stu-id="7371e-149">Once cluster creation finishes, you are able to use the jars added through this script from Hive without having to use the `ADD JAR` statement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7371e-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7371e-150">Next steps</span></span>

<span data-ttu-id="7371e-151">Per altre informazioni sull'uso di Hive, vedere l'articolo relativo all' [uso di Hive con HDInsight](hdinsight-use-hive.md)</span><span class="sxs-lookup"><span data-stu-id="7371e-151">For more information on working with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md)</span></span>
