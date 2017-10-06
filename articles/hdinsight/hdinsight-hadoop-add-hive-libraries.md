---
title: le librerie Hive aaaAdd durante HDInsight cluster creazione - Azure | Documenti Microsoft
description: Informazioni su come le librerie Hive tooadd (file jar), tooan HDInsight cluster durante la creazione del cluster.
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
ms.openlocfilehash: 2e028a07c3248205def0789af2c262a0774a8f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a><span data-ttu-id="5dd3f-103">Aggiungere librerie Hive personalizzate durante la creazione del cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="5dd3f-103">Add custom Hive libraries when creating your HDInsight cluster</span></span>

<span data-ttu-id="5dd3f-104">Se si dispongono di librerie di uso frequente con Hive in HDInsight, in questo documento contiene informazioni sull'utilizzo di librerie di hello toopre carico un'azione Script durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-104">If you have libraries that you use frequently with Hive on HDInsight, this document contains information on using a Script Action toopre-load hello libraries during cluster creation.</span></span> <span data-ttu-id="5dd3f-105">Librerie aggiunte utilizzando i passaggi di hello in questo documento sono disponibili a livello globale nell'Hive, non c'è alcuna necessità toouse [aggiungere JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload li.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-105">Libraries added using hello steps in this document are globally available in Hive - there is no need toouse [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload them.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="5dd3f-106">Funzionamento</span><span class="sxs-lookup"><span data-stu-id="5dd3f-106">How it works</span></span>

<span data-ttu-id="5dd3f-107">Quando si crea un cluster, è possibile specificare facoltativamente un'azione che esegue uno script nei nodi del cluster hello durante la creazione di Script.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-107">When creating a cluster, you can optionally specify a Script Action that runs a script on hello cluster nodes while they are being created.</span></span> <span data-ttu-id="5dd3f-108">script Hello in questo documento accetta un solo parametro, ovvero una posizione WASB contenente hello librerie (archiviate come file jar) toobe precaricati.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-108">hello script in this document accepts a single parameter, which is a WASB location that contains hello libraries (stored as jar files) toobe pre-loaded.</span></span>

<span data-ttu-id="5dd3f-109">Durante la creazione del cluster script hello enumera i file hello, li copia toohello `/usr/lib/customhivelibs/` directory nei nodi head e di lavoro, quindi li aggiunge toohello `hive.aux.jars.path` proprietà hello `core-site.xml` file.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-109">During cluster creation, hello script enumerates hello files, copies them toohello `/usr/lib/customhivelibs/` directory on head and worker nodes, then adds them toohello `hive.aux.jars.path` property in hello `core-site.xml` file.</span></span> <span data-ttu-id="5dd3f-110">Nei cluster basati su Linux, viene anche aggiornato hello `hive-env.sh` file con percorso hello del file hello.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-110">On Linux-based clusters, it also updates hello `hive-env.sh` file with hello location of hello files.</span></span>

> [!NOTE]
> <span data-ttu-id="5dd3f-111">Usando le azioni script hello in questo articolo, le librerie di hello rende disponibili in hello seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="5dd3f-111">Using hello script actions in this article makes hello libraries available in hello following scenarios:</span></span>
>
> * <span data-ttu-id="5dd3f-112">**HDInsight basati su Linux** : quando l'utilizzo di un client di Hive, hello **WebHCat**, e **HiveServer2**.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-112">**Linux-based HDInsight** - when using hello a Hive client, **WebHCat**, and **HiveServer2**.</span></span>
> * <span data-ttu-id="5dd3f-113">**HDInsight basati su Windows** - quando si utilizza il client di Hive hello e **WebHCat**.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-113">**Windows-based HDInsight** - when using hello Hive client and **WebHCat**.</span></span>

## <a name="hello-script"></a><span data-ttu-id="5dd3f-114">script Hello</span><span class="sxs-lookup"><span data-stu-id="5dd3f-114">hello script</span></span>

<span data-ttu-id="5dd3f-115">**Percorso dello script**</span><span class="sxs-lookup"><span data-stu-id="5dd3f-115">**Script location**</span></span>

<span data-ttu-id="5dd3f-116">Per i **cluster basati su Linux**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="5dd3f-116">For **Linux-based clusters**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span></span>

<span data-ttu-id="5dd3f-117">Per i **cluster basati su Windows**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span><span class="sxs-lookup"><span data-stu-id="5dd3f-117">For **Windows-based clusters**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5dd3f-118">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-118">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5dd3f-119">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="5dd3f-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="5dd3f-120">**Requisiti**</span><span class="sxs-lookup"><span data-stu-id="5dd3f-120">**Requirements**</span></span>

* <span data-ttu-id="5dd3f-121">gli script Hello devono essere applicato tooboth hello **nodi Head** e **nodi di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-121">hello scripts must be applied tooboth hello **Head nodes** and **Worker nodes**.</span></span>

* <span data-ttu-id="5dd3f-122">Hello JAR desiderato tooinstall devono essere archiviate nell'archiviazione Blob di Azure in un **singolo contenitore**.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-122">hello jars you wish tooinstall must be stored in Azure Blob Storage in a **single container**.</span></span>

* <span data-ttu-id="5dd3f-123">account di archiviazione Hello libreria hello dei file jar contenente **deve** essere cluster HDInsight toohello collegato durante la creazione.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-123">hello storage account containing hello library of jar files **must** be linked toohello HDInsight cluster during creation.</span></span> <span data-ttu-id="5dd3f-124">Deve essere account di archiviazione predefinito hello o un account aggiunto tramite __configurazione facoltativa__.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-124">It must either be hello default storage account, or an account added through __optional configuration__.</span></span>

* <span data-ttu-id="5dd3f-125">Hello WASB percorso toohello contenitore deve essere specificato come un toohello parametro azione Script.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-125">hello WASB path toohello container must be specified as a parameter toohello Script Action.</span></span> <span data-ttu-id="5dd3f-126">Ad esempio, se hello JAR vengono archiviati in un contenitore denominato **librerie** su un account di archiviazione denominato **la risorsa mystorage**, il parametro hello sarebbe  **wasb://libs@mystorage.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="5dd3f-126">For example, if hello jars are stored in a container named **libs** on a storage account named **mystorage**, hello parameter would be **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="5dd3f-127">Questo documento presuppone che hanno già crei un account di archiviazione, il contenitore blob e tooit file hello caricato.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-127">This document assumes that you have already create a storage account, blob container, and uploaded hello files tooit.</span></span>
  >
  > <span data-ttu-id="5dd3f-128">Se non è stato creato un account di archiviazione, è possibile farlo tramite hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5dd3f-128">If you have not created a storage account, you can do so through hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5dd3f-129">È quindi possibile utilizzare un'utilità, ad esempio [Azure Storage Explorer](http://storageexplorer.com/) toocreate un contenitore nell'account di hello e caricamento file tooit.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-129">You can then use a utility such as [Azure Storage Explorer](http://storageexplorer.com/) toocreate a container in hello account and upload files tooit.</span></span>

## <a name="create-a-cluster-using-hello-script"></a><span data-ttu-id="5dd3f-130">Creare un cluster utilizzando script hello</span><span class="sxs-lookup"><span data-stu-id="5dd3f-130">Create a cluster using hello script</span></span>

> [!NOTE]
> <span data-ttu-id="5dd3f-131">Hello alla procedura seguente crea un cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-131">hello following steps create a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="5dd3f-132">Selezionare un cluster basato su Windows, toocreate **Windows** come hello cluster del sistema operativo durante la creazione di cluster hello e utilizzare script di Windows (PowerShell) hello anziché script bash hello.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-132">toocreate a Windows-based cluster, select **Windows** as hello cluster OS when creating hello cluster, and use hello Windows (PowerShell) script instead of hello bash script.</span></span>
>
> <span data-ttu-id="5dd3f-133">È inoltre possibile utilizzare Azure PowerShell o hello HDInsight .NET SDK toocreate un cluster utilizzando lo script.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-133">You can also use Azure PowerShell or hello HDInsight .NET SDK toocreate a cluster using this script.</span></span> <span data-ttu-id="5dd3f-134">Per altre informazioni sull'uso di questi metodi, vedere [Personalizzare i cluster HDInsight con azioni script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5dd3f-134">For more information on using these methods, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="5dd3f-135">Avviare il provisioning di un cluster attenendosi alla procedura hello in [cluster HDInsight di effettuare il provisioning in Linux](hdinsight-hadoop-provision-linux-clusters.md), ma non viene completato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-135">Start provisioning a cluster by using hello steps in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md), but do not complete provisioning.</span></span>

2. <span data-ttu-id="5dd3f-136">In hello **configurazione facoltativa** pannello seleziona **azioni Script**e fornire hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="5dd3f-136">On hello **Optional Configuration** blade, select **Script Actions**, and provide hello following information:</span></span>

   * <span data-ttu-id="5dd3f-137">**NOME**: immettere un nome descrittivo per l'azione script hello.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-137">**NAME**: Enter a friendly name for hello script action.</span></span>

   * <span data-ttu-id="5dd3f-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span><span class="sxs-lookup"><span data-stu-id="5dd3f-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span></span>

   * <span data-ttu-id="5dd3f-139">**HEAD**: selezionare questa opzione.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-139">**HEAD**: Check this option.</span></span>

   * <span data-ttu-id="5dd3f-140">**LAVORO**: selezionare questa opzione.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-140">**WORKER**: Check this option.</span></span>

   * <span data-ttu-id="5dd3f-141">**ZOOKEEPER**: lasciare vuoto questo campo.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-141">**ZOOKEEPER**: Leave this blank.</span></span>

   * <span data-ttu-id="5dd3f-142">**I parametri**: immettere hello WASB toohello contenitore e l'archiviazione account indirizzo contenente JAR hello.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-142">**PARAMETERS**: Enter hello WASB address toohello container and storage account that contains hello jars.</span></span> <span data-ttu-id="5dd3f-143">Ad esempio, **wasb://libs@mystorage.blob.core.windows.net/**.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-143">For example, **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

3. <span data-ttu-id="5dd3f-144">Nella parte inferiore di hello di hello **azioni Script**, utilizzare hello **selezionare** configurazione hello toosave dei pulsanti.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-144">At hello bottom of hello **Script Actions**, use hello **Select** button toosave hello configuration.</span></span>

4. <span data-ttu-id="5dd3f-145">In hello **configurazione facoltativa** pannello seleziona **account di archiviazione collegati** e seleziona hello **aggiungere una chiave di archiviazione** collegamento.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-145">On hello **Optional Configuration** blade, select **Linked Storage Accounts** and select hello **Add a storage key** link.</span></span> <span data-ttu-id="5dd3f-146">Selezionare l'account di archiviazione hello contenente JAR hello e quindi utilizzare hello **selezionare** impostazioni toosave pulsanti e hello restituito **configurazione facoltativa** blade.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-146">Select hello storage account that contains hello jars, and then use hello **select** buttons toosave settings and return hello **Optional Configuration** blade.</span></span>

5. <span data-ttu-id="5dd3f-147">Hello utilizzare **selezionare** pulsante nella parte inferiore di hello di hello **configurazione facoltativa** informazioni di configurazione facoltativa hello toosave blade.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-147">Use hello **Select** button at hello bottom of hello **Optional Configuration** blade toosave hello optional configuration information.</span></span>

6. <span data-ttu-id="5dd3f-148">Continuano il provisioning del cluster di hello, come descritto in [cluster HDInsight di effettuare il provisioning in Linux](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="5dd3f-148">Continue provisioning hello cluster as described in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="5dd3f-149">Al termine della creazione del cluster, si è in grado di toouse JAR di hello aggiunti tramite questo script dall'Hive senza hello toouse `ADD JAR` istruzione.</span><span class="sxs-lookup"><span data-stu-id="5dd3f-149">Once cluster creation finishes, you are able toouse hello jars added through this script from Hive without having toouse hello `ADD JAR` statement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5dd3f-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5dd3f-150">Next steps</span></span>

<span data-ttu-id="5dd3f-151">Per altre informazioni sull'uso di Hive, vedere l'articolo relativo all' [uso di Hive con HDInsight](hdinsight-use-hive.md)</span><span class="sxs-lookup"><span data-stu-id="5dd3f-151">For more information on working with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md)</span></span>
