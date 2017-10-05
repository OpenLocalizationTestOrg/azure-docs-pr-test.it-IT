---
title: Sviluppo di azioni script con HDInsight basato su Linux - Azure | Documentazione Microsoft
description: "Informazioni su come usare script Bash per personalizzare cluster HDInsight basati su Linux. La funzionalità di azione script in HDInsight consente di eseguire script durante o dopo la creazione del cluster. Gli script possono essere usati per modificare le impostazioni di configurazione del cluster o per installare software aggiuntivo."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf4c89cd-f7da-4a10-857f-838004965d3e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 7f1a0bd8c7e60770d376f10eaea136a55c632c5e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="script-action-development-with-hdinsight"></a><span data-ttu-id="c4852-105">Sviluppo di azioni script con HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4852-105">Script action development with HDInsight</span></span>

<span data-ttu-id="c4852-106">Informazioni su come personalizzare il cluster HDInsight tramite script Bash.</span><span class="sxs-lookup"><span data-stu-id="c4852-106">Learn how to customize your HDInsight cluster using Bash scripts.</span></span> <span data-ttu-id="c4852-107">Le azioni script consentono di personalizzare HDInsight durante o dopo la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="c4852-107">Script actions are a way to customize HDInsight during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4852-108">I passaggi descritti in questo documento richiedono un cluster HDInsight che usa Linux.</span><span class="sxs-lookup"><span data-stu-id="c4852-108">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="c4852-109">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="c4852-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c4852-110">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c4852-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="what-are-script-actions"></a><span data-ttu-id="c4852-111">Definizione di azioni script</span><span class="sxs-lookup"><span data-stu-id="c4852-111">What are script actions</span></span>

<span data-ttu-id="c4852-112">Le azioni script sono script Bash eseguiti da Azure sui nodi del cluster per apportare modifiche alla configurazione o installare software.</span><span class="sxs-lookup"><span data-stu-id="c4852-112">Script actions are Bash scripts that Azure runs on the cluster nodes to make configuration changes or install software.</span></span> <span data-ttu-id="c4852-113">Un'azione script viene eseguita come radice e fornisce diritti di accesso completo ai nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="c4852-113">A script action is executed as root, and provides full access rights to the cluster nodes.</span></span>

<span data-ttu-id="c4852-114">L'azione script può essere applicata usando i metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c4852-114">Script actions can be applied through the following methods:</span></span>

| <span data-ttu-id="c4852-115">Usare questo metodo per applicare uno script...</span><span class="sxs-lookup"><span data-stu-id="c4852-115">Use this method to apply a script...</span></span> | <span data-ttu-id="c4852-116">Durante la creazione di un cluster...</span><span class="sxs-lookup"><span data-stu-id="c4852-116">During cluster creation...</span></span> | <span data-ttu-id="c4852-117">In un cluster in esecuzione...</span><span class="sxs-lookup"><span data-stu-id="c4852-117">On a running cluster...</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="c4852-118">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c4852-118">Azure portal</span></span> |<span data-ttu-id="c4852-119">✓ </span><span class="sxs-lookup"><span data-stu-id="c4852-119">✓</span></span> |<span data-ttu-id="c4852-120">✓</span><span class="sxs-lookup"><span data-stu-id="c4852-120">✓</span></span> |
| <span data-ttu-id="c4852-121">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4852-121">Azure PowerShell</span></span> |<span data-ttu-id="c4852-122">✓</span><span class="sxs-lookup"><span data-stu-id="c4852-122">✓</span></span> |<span data-ttu-id="c4852-123">✓</span><span class="sxs-lookup"><span data-stu-id="c4852-123">✓</span></span> |
| <span data-ttu-id="c4852-124">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="c4852-124">Azure CLI</span></span> |&nbsp; |<span data-ttu-id="c4852-125">✓</span><span class="sxs-lookup"><span data-stu-id="c4852-125">✓</span></span> |
| <span data-ttu-id="c4852-126">HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c4852-126">HDInsight .NET SDK</span></span> |<span data-ttu-id="c4852-127">✓</span><span class="sxs-lookup"><span data-stu-id="c4852-127">✓</span></span> |<span data-ttu-id="c4852-128">✓</span><span class="sxs-lookup"><span data-stu-id="c4852-128">✓</span></span> |
| <span data-ttu-id="c4852-129">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c4852-129">Azure Resource Manager Template</span></span> |<span data-ttu-id="c4852-130">✓</span><span class="sxs-lookup"><span data-stu-id="c4852-130">✓</span></span> |&nbsp; |

<span data-ttu-id="c4852-131">Per altre informazioni sull'uso di questi metodi per l'applicazione di azioni script, vedere [Personalizzare cluster HDInsight tramite azioni script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c4852-131">For more information on using these methods to apply script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="c4852-132"><a name="bestPracticeScripting"></a>Procedure consigliate per lo sviluppo di script</span><span class="sxs-lookup"><span data-stu-id="c4852-132"><a name="bestPracticeScripting"></a>Best practices for script development</span></span>

<span data-ttu-id="c4852-133">Quando si sviluppa uno script personalizzato per un cluster HDInsight, è opportuno seguire le procedure consigliate indicate di seguito:</span><span class="sxs-lookup"><span data-stu-id="c4852-133">When you develop a custom script for an HDInsight cluster, there are several best practices to keep in mind:</span></span>

* [<span data-ttu-id="c4852-134">Usare la versione di Hadoop</span><span class="sxs-lookup"><span data-stu-id="c4852-134">Target the Hadoop version</span></span>](#bPS1)
* [<span data-ttu-id="c4852-135">Usare la versione del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="c4852-135">Target the OS Version</span></span>](#bps10)
* [<span data-ttu-id="c4852-136">Fornire collegamenti stabili alle risorse di script</span><span class="sxs-lookup"><span data-stu-id="c4852-136">Provide stable links to script resources</span></span>](#bPS2)
* [<span data-ttu-id="c4852-137">Usare risorse precompilate</span><span class="sxs-lookup"><span data-stu-id="c4852-137">Use pre-compiled resources</span></span>](#bPS4)
* [<span data-ttu-id="c4852-138">Assicurarsi che lo script di personalizzazione del cluster sia idempotente</span><span class="sxs-lookup"><span data-stu-id="c4852-138">Ensure that the cluster customization script is idempotent</span></span>](#bPS3)
* [<span data-ttu-id="c4852-139">Verificare la disponibilità elevata dell'architettura del cluster</span><span class="sxs-lookup"><span data-stu-id="c4852-139">Ensure high availability of the cluster architecture</span></span>](#bPS5)
* [<span data-ttu-id="c4852-140">Configurare i componenti personalizzati per l'uso dell'archivio BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="c4852-140">Configure the custom components to use Azure Blob storage</span></span>](#bPS6)
* [<span data-ttu-id="c4852-141">Scrivere informazioni in STDOUT e STDERR</span><span class="sxs-lookup"><span data-stu-id="c4852-141">Write information to STDOUT and STDERR</span></span>](#bPS7)
* [<span data-ttu-id="c4852-142">Salvare i file in formato ASCII con terminazioni di riga LF</span><span class="sxs-lookup"><span data-stu-id="c4852-142">Save files as ASCII with LF line endings</span></span>](#bps8)
* [<span data-ttu-id="c4852-143">Usare la logica di ripetizione dei tentativi per il ripristino da errori temporanei</span><span class="sxs-lookup"><span data-stu-id="c4852-143">Use retry logic to recover from transient errors</span></span>](#bps9)

> [!IMPORTANT]
> <span data-ttu-id="c4852-144">Le azioni di script devono essere completate entro 60 minuti; in caso contrario il processo avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="c4852-144">Script actions must complete within 60 minutes or the process fails.</span></span> <span data-ttu-id="c4852-145">Durante il provisioning dei nodi, lo script viene eseguito contemporaneamente ad altri processi di installazione e configurazione.</span><span class="sxs-lookup"><span data-stu-id="c4852-145">During node provisioning, the script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="c4852-146">In caso di concorrenza per risorse come il tempo di CPU o la larghezza di banda di rete, lo script può richiedere più tempo per completare l'operazione rispetto al tempo che impiegherebbe in un ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="c4852-146">Competition for resources such as CPU time or network bandwidth may cause the script to take longer to finish than it does in your development environment.</span></span>

### <span data-ttu-id="c4852-147"><a name="bPS1"></a>Usare la versione di Hadoop</span><span class="sxs-lookup"><span data-stu-id="c4852-147"><a name="bPS1"></a>Target the Hadoop version</span></span>

<span data-ttu-id="c4852-148">Nelle diverse versioni di HDInsight sono installate versioni diverse di servizi e componenti di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c4852-148">Different versions of HDInsight have different versions of Hadoop services and components installed.</span></span> <span data-ttu-id="c4852-149">Se lo script prevede una versione specifica di un servizio o un componente, si dovrà usare lo script solo con la versione di HDInsight che include i componenti richiesti.</span><span class="sxs-lookup"><span data-stu-id="c4852-149">If your script expects a specific version of a service or component, you should only use the script with the version of HDInsight that includes the required components.</span></span> <span data-ttu-id="c4852-150">Per trovare informazioni sulle versioni dei componenti incluse in HDInsight, usare il documento relativo al [controllo delle versioni dei componenti di HDInsight](hdinsight-component-versioning.md) .</span><span class="sxs-lookup"><span data-stu-id="c4852-150">You can find information on component versions included with HDInsight using the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

### <span data-ttu-id="c4852-151"><a name="bps10"></a> Usare la versione del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="c4852-151"><a name="bps10"></a> Target the OS version</span></span>

<span data-ttu-id="c4852-152">HDInsight basato su Linux si basa sulla distribuzione di Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="c4852-152">Linux-based HDInsight is based on the Ubuntu Linux distribution.</span></span> <span data-ttu-id="c4852-153">Versioni diverse di HDInsight si basano su versioni differenti di Ubuntu e questo può influire sul comportamento dello script.</span><span class="sxs-lookup"><span data-stu-id="c4852-153">Different versions of HDInsight rely on different versions of Ubuntu, which may change how your script behaves.</span></span> <span data-ttu-id="c4852-154">HDInsight 3.4 e versioni precedenti si basano ad esempio su versioni di Ubuntu che usano Upstart.</span><span class="sxs-lookup"><span data-stu-id="c4852-154">For example, HDInsight 3.4 and earlier are based on Ubuntu versions that use Upstart.</span></span> <span data-ttu-id="c4852-155">La versione 3.5 si basa su Ubuntu 16.04 che usa Systemd.</span><span class="sxs-lookup"><span data-stu-id="c4852-155">Version 3.5 is based on Ubuntu 16.04, which uses Systemd.</span></span> <span data-ttu-id="c4852-156">Systemd e Upstart si basano su comandi diversi, quindi lo script deve essere scritto in modo da funzionare con entrambi.</span><span class="sxs-lookup"><span data-stu-id="c4852-156">Systemd and Upstart rely on different commands, so your script should be written to work with both.</span></span>

<span data-ttu-id="c4852-157">Un'altra differenza importante tra HDInsight 3.4 e 3.5 è che `JAVA_HOME` punta ora a Java 8.</span><span class="sxs-lookup"><span data-stu-id="c4852-157">Another important difference between HDInsight 3.4 and 3.5 is that `JAVA_HOME` now points to Java 8.</span></span>

<span data-ttu-id="c4852-158">È possibile verificare la versione del sistema operativo con `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="c4852-158">You can check the OS version by using `lsb_release`.</span></span> <span data-ttu-id="c4852-159">Il codice seguente illustra come determinare se lo script è in esecuzione su Ubuntu 14 o 16:</span><span class="sxs-lookup"><span data-stu-id="c4852-159">The following code demonstrates how to determine if the script is running on Ubuntu 14 or 16:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
...
if [[ $OS_VERSION == 16* ]]; then
    echo "Using systemd configuration"
    systemctl daemon-reload
    systemctl stop webwasb.service    
    systemctl start webwasb.service
else
    echo "Using upstart configuration"
    initctl reload-configuration
    stop webwasb
    start webwasb
fi
...
if [[ $OS_VERSION == 14* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
elif [[ $OS_VERSION == 16* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
fi
```

<span data-ttu-id="c4852-160">Lo script completo contenente questi frammenti è disponibile all'indirizzo https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span><span class="sxs-lookup"><span data-stu-id="c4852-160">You can find the full script that contains these snippets at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span></span>

<span data-ttu-id="c4852-161">Per la versione di Ubuntu usata da HDInsight, vedere il documento sulle [versioni dei componenti HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="c4852-161">For the version of Ubuntu that is used by HDInsight, see the [HDInsight component version](hdinsight-component-versioning.md) document.</span></span>

<span data-ttu-id="c4852-162">Per comprendere le differenze tra Systemd e Upstart, vedere [Systemd per gli utenti di Upstart](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span><span class="sxs-lookup"><span data-stu-id="c4852-162">To understand the differences between Systemd and Upstart, see [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span></span>

### <span data-ttu-id="c4852-163"><a name="bPS2"></a>Fornire collegamenti stabili alle risorse di script</span><span class="sxs-lookup"><span data-stu-id="c4852-163"><a name="bPS2"></a>Provide stable links to script resources</span></span>

<span data-ttu-id="c4852-164">Lo script e le risorse associate devono rimanere disponibili per tutta la durata del cluster.</span><span class="sxs-lookup"><span data-stu-id="c4852-164">The script and associated resources must remain available throughout the lifetime of the cluster.</span></span> <span data-ttu-id="c4852-165">Queste risorse sono necessarie se vengono aggiunti nuovi nodi al cluster durante operazioni di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="c4852-165">These resources are required if new nodes are added to the cluster during scaling operations.</span></span>

<span data-ttu-id="c4852-166">È consigliabile scaricare e archiviare tutti gli elementi in un account di archiviazione di Azure nella propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="c4852-166">The best practice is to download and archive everything in an Azure Storage account on your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4852-167">L'account di archiviazione usato deve essere quello predefinito per il cluster o un contenitore pubblico di sola lettura per qualsiasi altro account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c4852-167">The storage account used must be the default storage account for the cluster or a public, read-only container on any other storage account.</span></span>

<span data-ttu-id="c4852-168">Gli esempi forniti da Microsoft, ad esempio, vengono archiviati nell'account di archiviazione [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/).</span><span class="sxs-lookup"><span data-stu-id="c4852-168">For example, the samples provided by Microsoft are stored in the [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage account.</span></span> <span data-ttu-id="c4852-169">Si tratta di un contenitore pubblico e di sola lettura, gestito dal team di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c4852-169">This is a public, read-only container maintained by the HDInsight team.</span></span>

### <span data-ttu-id="c4852-170"><a name="bPS4"></a>Usare risorse precompilate</span><span class="sxs-lookup"><span data-stu-id="c4852-170"><a name="bPS4"></a>Use pre-compiled resources</span></span>

<span data-ttu-id="c4852-171">Per ridurre il tempo necessario per eseguire lo script, evitare operazioni di compilazione delle risorse dal codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="c4852-171">To reduce the time it takes to run the script, avoid operations that compile resources from source code.</span></span> <span data-ttu-id="c4852-172">Ad esempio, precompilare le risorse e archiviarle in un BLOB dell'account di archiviazione di Azure nello stesso data center di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c4852-172">For example, pre-compile resources and store them in an Azure Storage account blob in the same data center as HDInsight.</span></span>

### <span data-ttu-id="c4852-173"><a name="bPS3"></a>Assicurarsi che lo script di personalizzazione del cluster sia idempotente</span><span class="sxs-lookup"><span data-stu-id="c4852-173"><a name="bPS3"></a>Ensure that the cluster customization script is idempotent</span></span>

<span data-ttu-id="c4852-174">Gli script devono essere idempotenti.</span><span class="sxs-lookup"><span data-stu-id="c4852-174">Scripts must be idempotent.</span></span> <span data-ttu-id="c4852-175">Se lo script viene eseguito più volte, ogni volta deve riportare il cluster allo stato iniziale.</span><span class="sxs-lookup"><span data-stu-id="c4852-175">If the script runs multiple times, it should return the cluster to the same state every time.</span></span>

<span data-ttu-id="c4852-176">Uno script che modifica i file di configurazione, ad esempio, non deve aggiungere voci duplicate se viene eseguito più volte.</span><span class="sxs-lookup"><span data-stu-id="c4852-176">For example, a script that modifies configuration files should not add duplicate entries if ran multiple times.</span></span>

### <span data-ttu-id="c4852-177"><a name="bPS5"></a>Verificare la disponibilità elevata dell'architettura del cluster</span><span class="sxs-lookup"><span data-stu-id="c4852-177"><a name="bPS5"></a>Ensure high availability of the cluster architecture</span></span>

<span data-ttu-id="c4852-178">I cluster HDInsight basati su Linux forniscono due nodi head attivi all'interno del cluster e le azioni script vengono eseguite per entrambi i nodi.</span><span class="sxs-lookup"><span data-stu-id="c4852-178">Linux-based HDInsight clusters provide two head nodes that are active within the cluster, and script actions run on both nodes.</span></span> <span data-ttu-id="c4852-179">Se i componenti da installare prevedono un solo nodo head, non installare i componenti in entrambi i nodi head.</span><span class="sxs-lookup"><span data-stu-id="c4852-179">If the components you install expect only one head node, do not install the components on both head nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4852-180">I servizi forniti nell'ambito di HDInsight sono progettati per supportare il failover tra i due nodi head, se necessario.</span><span class="sxs-lookup"><span data-stu-id="c4852-180">Services provided as part of HDInsight are designed to fail over between the two head nodes as needed.</span></span> <span data-ttu-id="c4852-181">Questa funzionalità non è estesa ai componenti personalizzati installati tramite azioni script.</span><span class="sxs-lookup"><span data-stu-id="c4852-181">This functionality is not extended to custom components installed through script actions.</span></span> <span data-ttu-id="c4852-182">Se i componenti personalizzati richiedono una disponibilità elevata, è necessario implementare un meccanismo di failover personalizzato.</span><span class="sxs-lookup"><span data-stu-id="c4852-182">If you need high availability for custom components, you must implement your own failover mechanism.</span></span>

### <span data-ttu-id="c4852-183"><a name="bPS6"></a>Configurare i componenti personalizzati per l'uso dell'archivio BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="c4852-183"><a name="bPS6"></a>Configure the custom components to use Azure Blob storage</span></span>

<span data-ttu-id="c4852-184">I componenti installati nel cluster possono avere una configurazione predefinita che usa l'archiviazione di Hadoop Distributed File System (HDFS).</span><span class="sxs-lookup"><span data-stu-id="c4852-184">Components that you install on the cluster might have a default configuration that uses Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="c4852-185">HDInsight usa l'archiviazione di Azure o Azure Data Lake Store come risorsa di archiviazione predefinita,</span><span class="sxs-lookup"><span data-stu-id="c4852-185">HDInsight uses either Azure Storage or Data Lake Store as the default storage.</span></span> <span data-ttu-id="c4852-186">poiché entrambi forniscono un file system compatibile con HDFS che rende permanenti i dati anche se il cluster viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="c4852-186">Both provide an HDFS compatible file system that persists data even if the cluster is deleted.</span></span> <span data-ttu-id="c4852-187">In alcuni casi, è possibile che sia necessario configurare i componenti installati in modo da usare WASB o ADL anziché HDFS.</span><span class="sxs-lookup"><span data-stu-id="c4852-187">You may need to configure components you install to use WASB or ADL instead of HDFS.</span></span>

<span data-ttu-id="c4852-188">Per la maggior parte delle operazioni, tuttavia, non è necessario specificare il file system.</span><span class="sxs-lookup"><span data-stu-id="c4852-188">For most operations, you do not need to specify the file system.</span></span> <span data-ttu-id="c4852-189">Il codice seguente, ad esempio, copia il file giraph-examples.jar dal file system locale alla risorsa di archiviazione del cluster:</span><span class="sxs-lookup"><span data-stu-id="c4852-189">For example, the following copies the giraph-examples.jar file from the local file system to cluster storage:</span></span>

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

<span data-ttu-id="c4852-190">In questo esempio, il comando `hdfs` usa in modo trasparente la risorsa di archiviazione del cluster predefinita.</span><span class="sxs-lookup"><span data-stu-id="c4852-190">In this example, the `hdfs` command transparently uses the default cluster storage.</span></span> <span data-ttu-id="c4852-191">Per alcune operazioni, è necessario specificare l'URI,</span><span class="sxs-lookup"><span data-stu-id="c4852-191">For some operations, you may need to specify the URI.</span></span> <span data-ttu-id="c4852-192">ad esempio `adl:///example/jars` per Data Lake Store o `wasb:///example/jars` per l'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c4852-192">For example, `adl:///example/jars` for Data Lake Store or `wasb:///example/jars` for Azure Storage.</span></span>

### <span data-ttu-id="c4852-193"><a name="bPS7"></a>Scrivere informazioni in STDOUT e STDERR</span><span class="sxs-lookup"><span data-stu-id="c4852-193"><a name="bPS7"></a>Write information to STDOUT and STDERR</span></span>

<span data-ttu-id="c4852-194">HDInsight registra l'output dello script scritto in STDOUT e STDERR.</span><span class="sxs-lookup"><span data-stu-id="c4852-194">HDInsight logs script output that is written to STDOUT and STDERR.</span></span> <span data-ttu-id="c4852-195">È possibile visualizzare queste informazioni tramite l'interfaccia utente Web di Ambari.</span><span class="sxs-lookup"><span data-stu-id="c4852-195">You can view this information using the Ambari web UI.</span></span>

> [!NOTE]
> <span data-ttu-id="c4852-196">Ambari è disponibile solo se il cluster viene creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="c4852-196">Ambari is only available if the cluster is successfully created.</span></span> <span data-ttu-id="c4852-197">Se si usa un'azione script durante la creazione del cluster e la creazione ha esito negativo, vedere la sezione relativa alla risoluzione dei problemi nell'articolo [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) che illustra altri modi per accedere alle informazioni registrate.</span><span class="sxs-lookup"><span data-stu-id="c4852-197">If you use a script action during cluster creation, and creation fails, see the troubleshooting section [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) for other ways of accessing logged information.</span></span>

<span data-ttu-id="c4852-198">Sebbene la maggior parte delle utilità e dei pacchetti di installazione scriva già le informazioni in STDOUT e STDERR, è possibile aggiungere altre opzioni di registrazione.</span><span class="sxs-lookup"><span data-stu-id="c4852-198">Most utilities and installation packages already write information to STDOUT and STDERR, however you may want to add additional logging.</span></span> <span data-ttu-id="c4852-199">Per inviare testo a STDOUT, usare `echo`.</span><span class="sxs-lookup"><span data-stu-id="c4852-199">To send text to STDOUT, use `echo`.</span></span> <span data-ttu-id="c4852-200">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c4852-200">For example:</span></span>

```bash
echo "Getting ready to install Foo"
```

<span data-ttu-id="c4852-201">Per impostazione predefinita, `echo` invia la stringa a STDOUT.</span><span class="sxs-lookup"><span data-stu-id="c4852-201">By default, `echo` sends the string to STDOUT.</span></span> <span data-ttu-id="c4852-202">Per indirizzarla a STDERR, aggiungere `>&2` prima di `echo`.</span><span class="sxs-lookup"><span data-stu-id="c4852-202">To direct it to STDERR, add `>&2` before `echo`.</span></span> <span data-ttu-id="c4852-203">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c4852-203">For example:</span></span>

```bash
>&2 echo "An error occurred installing Foo"
```

<span data-ttu-id="c4852-204">Questo codice reindirizza a STDERR (2) le informazioni scritte in STDOUT.</span><span class="sxs-lookup"><span data-stu-id="c4852-204">This redirects information written to STDOUT to STDERR (2) instead.</span></span> <span data-ttu-id="c4852-205">Per altre informazioni sul reindirizzamento I/O, vedere [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span><span class="sxs-lookup"><span data-stu-id="c4852-205">For more information on IO redirection, see [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span></span>

<span data-ttu-id="c4852-206">Per altre informazioni sulla visualizzazione delle informazioni registrate tramite azioni script, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span><span class="sxs-lookup"><span data-stu-id="c4852-206">For more information on viewing information logged by script actions, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span></span>

### <span data-ttu-id="c4852-207"><a name="bps8"></a> Salvare i file in formato ASCII con terminazioni di riga LF</span><span class="sxs-lookup"><span data-stu-id="c4852-207"><a name="bps8"></a> Save files as ASCII with LF line endings</span></span>

<span data-ttu-id="c4852-208">Gli script Bash devono essere archiviati nel formato ASCII con righe terminate da LF.</span><span class="sxs-lookup"><span data-stu-id="c4852-208">Bash scripts should be stored as ASCII format, with lines terminated by LF.</span></span> <span data-ttu-id="c4852-209">Se i file vengono archiviati in formato UTF-8 o usano CRLF come terminazione di riga, è possibile che abbiano esito negativo con l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="c4852-209">Files that are stored as UTF-8, or use CRLF as the line ending may fail with the following error:</span></span>

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <span data-ttu-id="c4852-210"><a name="bps9"></a> Usare la logica di ripetizione dei tentativi per il ripristino da errori temporanei</span><span class="sxs-lookup"><span data-stu-id="c4852-210"><a name="bps9"></a> Use retry logic to recover from transient errors</span></span>

<span data-ttu-id="c4852-211">Quando si scaricano file, l'installazione di pacchetti tramite apt-get o altre azioni che trasmettono dati su Internet, l'azione potrebbe non riuscire a causa di errori di rete temporanei.</span><span class="sxs-lookup"><span data-stu-id="c4852-211">When downloading files, installing packages using apt-get, or other actions that transmit data over the internet, the action may fail due to transient networking errors.</span></span> <span data-ttu-id="c4852-212">Ad esempio, è possibile che sia in corso il failover a un nodo di backup della risorsa remota con la quale si sta comunicando.</span><span class="sxs-lookup"><span data-stu-id="c4852-212">For example, the remote resource you are communicating with may be in the process of failing over to a backup node.</span></span>

<span data-ttu-id="c4852-213">Per rendere lo script resiliente agli errori temporanei, è possibile implementare la logica di ripetizione dei tentativi.</span><span class="sxs-lookup"><span data-stu-id="c4852-213">To make your script resilient to transient errors, you can implement retry logic.</span></span> <span data-ttu-id="c4852-214">La funzione seguente illustra come implementare la logica di ripetizione dei tentativi:</span><span class="sxs-lookup"><span data-stu-id="c4852-214">The following function demonstrates how to implement retry logic.</span></span> <span data-ttu-id="c4852-215">prima che venga generato l'errore, ripete per tre volte il tentativo di eseguire l'operazione.</span><span class="sxs-lookup"><span data-stu-id="c4852-215">It retries the operation three times before failing.</span></span>

```bash
#retry
MAXATTEMPTS=3

retry() {
    local -r CMD="$@"
    local -i ATTMEPTNUM=1
    local -i RETRYINTERVAL=2

    until $CMD
    do
        if (( ATTMEPTNUM == MAXATTEMPTS ))
        then
                echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                return 1
        else
                echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                sleep $(( RETRYINTERVAL ))
                ATTMEPTNUM=$ATTMEPTNUM+1
        fi
    done
}
```

<span data-ttu-id="c4852-216">Gli esempi seguenti illustrano come usare questa funzione.</span><span class="sxs-lookup"><span data-stu-id="c4852-216">The following examples demonstrate how to use this function.</span></span>

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <span data-ttu-id="c4852-217"><a name="helpermethods"></a>Metodi helper per gli script personalizzati</span><span class="sxs-lookup"><span data-stu-id="c4852-217"><a name="helpermethods"></a>Helper methods for custom scripts</span></span>

<span data-ttu-id="c4852-218">I metodi helper dell'azione script sono utilità che è possibile usare durante la scrittura di script personalizzati.</span><span class="sxs-lookup"><span data-stu-id="c4852-218">Script action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="c4852-219">Questi metodi sono contenuti nello script [https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="c4852-219">These methods are contained in the[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script.</span></span> <span data-ttu-id="c4852-220">Usare il codice seguente per scaricarli e usarli nell'ambito dello script:</span><span class="sxs-lookup"><span data-stu-id="c4852-220">Use the following to download and use them as part of your script:</span></span>

```bash
# Import the helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

<span data-ttu-id="c4852-221">In uno script personalizzato possono essere usati gli helper seguenti:</span><span class="sxs-lookup"><span data-stu-id="c4852-221">The following helpers available for use in your script:</span></span>

| <span data-ttu-id="c4852-222">Utilizzo dell'helper</span><span class="sxs-lookup"><span data-stu-id="c4852-222">Helper usage</span></span> | <span data-ttu-id="c4852-223">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c4852-223">Description</span></span> |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |<span data-ttu-id="c4852-224">Scarica un file dall'URI di origine al percorso file specificato.</span><span class="sxs-lookup"><span data-stu-id="c4852-224">Downloads a file from the source URI to the specified file path.</span></span> <span data-ttu-id="c4852-225">Per impostazione predefinita, non sovrascrive un file esistente.</span><span class="sxs-lookup"><span data-stu-id="c4852-225">By default, it does not overwrite an existing file.</span></span> |
| `untar_file TARFILE DESTDIR` |<span data-ttu-id="c4852-226">Estrae un file TAR (usando `-xf`) nella directory di destinazione.</span><span class="sxs-lookup"><span data-stu-id="c4852-226">Extracts a tar file (using `-xf`) to the destination directory.</span></span> |
| `test_is_headnode` |<span data-ttu-id="c4852-227">Se viene eseguito su un nodo head del cluster restituisce 1; in caso contrario, 0.</span><span class="sxs-lookup"><span data-stu-id="c4852-227">If ran on a cluster head node, return 1; otherwise, 0.</span></span> |
| `test_is_datanode` |<span data-ttu-id="c4852-228">Se il nodo corrente è un nodo dati (di lavoro) restituisce 1; in caso contrario, 0.</span><span class="sxs-lookup"><span data-stu-id="c4852-228">If the current node is a data (worker) node, return a 1; otherwise, 0.</span></span> |
| `test_is_first_datanode` |<span data-ttu-id="c4852-229">Se il nodo corrente è il primo nodo dati (di lavoro), denominato workernode0, restituisce 1; in caso contrario, 0.</span><span class="sxs-lookup"><span data-stu-id="c4852-229">If the current node is the first data (worker) node (named workernode0) return a 1; otherwise, 0.</span></span> |
| `get_headnodes` |<span data-ttu-id="c4852-230">Restituisce il nome di dominio completo dei nodi head nel cluster.</span><span class="sxs-lookup"><span data-stu-id="c4852-230">Return the fully qualified domain name of the headnodes in the cluster.</span></span> <span data-ttu-id="c4852-231">I nomi sono delimitati da virgole.</span><span class="sxs-lookup"><span data-stu-id="c4852-231">Names are comma delimited.</span></span> <span data-ttu-id="c4852-232">In caso di errore, viene restituita una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="c4852-232">An empty string is returned on error.</span></span> |
| `get_primary_headnode` |<span data-ttu-id="c4852-233">Ottiene il nome di dominio completo del nodo head primario.</span><span class="sxs-lookup"><span data-stu-id="c4852-233">Gets the fully qualified domain name of the primary headnode.</span></span> <span data-ttu-id="c4852-234">In caso di errore, viene restituita una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="c4852-234">An empty string is returned on error.</span></span> |
| `get_secondary_headnode` |<span data-ttu-id="c4852-235">Ottiene il nome di dominio completo del nodo head secondario.</span><span class="sxs-lookup"><span data-stu-id="c4852-235">Gets the fully qualified domain name of the secondary headnode.</span></span> <span data-ttu-id="c4852-236">In caso di errore, viene restituita una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="c4852-236">An empty string is returned on error.</span></span> |
| `get_primary_headnode_number` |<span data-ttu-id="c4852-237">Ottiene il suffisso numerico del nodo head primario.</span><span class="sxs-lookup"><span data-stu-id="c4852-237">Gets the numeric suffix of the primary headnode.</span></span> <span data-ttu-id="c4852-238">In caso di errore, viene restituita una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="c4852-238">An empty string is returned on error.</span></span> |
| `get_secondary_headnode_number` |<span data-ttu-id="c4852-239">Ottiene il suffisso numerico del nodo head secondario.</span><span class="sxs-lookup"><span data-stu-id="c4852-239">Gets the numeric suffix of the secondary headnode.</span></span> <span data-ttu-id="c4852-240">In caso di errore, viene restituita una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="c4852-240">An empty string is returned on error.</span></span> |

## <span data-ttu-id="c4852-241"><a name="commonusage"></a>Modelli di utilizzo comuni</span><span class="sxs-lookup"><span data-stu-id="c4852-241"><a name="commonusage"></a>Common usage patterns</span></span>

<span data-ttu-id="c4852-242">Questa sezione fornisce indicazioni sull'implementazione di alcuni dei modelli di utilizzo comuni che si potrebbero riscontrare durante la scrittura dello script personalizzato.</span><span class="sxs-lookup"><span data-stu-id="c4852-242">This section provides guidance on implementing some of the common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="passing-parameters-to-a-script"></a><span data-ttu-id="c4852-243">Passaggio di parametri a uno script</span><span class="sxs-lookup"><span data-stu-id="c4852-243">Passing parameters to a script</span></span>

<span data-ttu-id="c4852-244">In alcuni casi, lo script potrebbe richiedere l'uso di parametri.</span><span class="sxs-lookup"><span data-stu-id="c4852-244">In some cases, your script may require parameters.</span></span> <span data-ttu-id="c4852-245">Quando si usa l'API REST di Ambari, ad esempio, è possibile che sia necessaria la password amministratore per il cluster.</span><span class="sxs-lookup"><span data-stu-id="c4852-245">For example, you may need the admin password for the cluster when using the Ambari REST API.</span></span>

<span data-ttu-id="c4852-246">I parametri passati allo script sono noti come *parametri posizionali* e vengono assegnati a `$1` per il primo parametro, a `$2` per il secondo e così via.</span><span class="sxs-lookup"><span data-stu-id="c4852-246">Parameters passed to the script are known as *positional parameters*, and are assigned to `$1` for the first parameter, `$2` for the second, and so-on.</span></span> <span data-ttu-id="c4852-247">`$0` contiene il nome dello script stesso.</span><span class="sxs-lookup"><span data-stu-id="c4852-247">`$0` contains the name of the script itself.</span></span>

<span data-ttu-id="c4852-248">I valori passati allo script come parametri devono essere racchiusi tra virgolette singole ('),</span><span class="sxs-lookup"><span data-stu-id="c4852-248">Values passed to the script as parameters should be enclosed by single quotes (').</span></span> <span data-ttu-id="c4852-249">in modo che vengano considerati come valori letterali.</span><span class="sxs-lookup"><span data-stu-id="c4852-249">Doing so ensures that the passed value is treated as a literal.</span></span>

### <a name="setting-environment-variables"></a><span data-ttu-id="c4852-250">Impostazioni delle variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="c4852-250">Setting environment variables</span></span>

<span data-ttu-id="c4852-251">L'impostazione di una variabile di ambiente viene eseguita con l'istruzione seguente:</span><span class="sxs-lookup"><span data-stu-id="c4852-251">Setting an environment variable is performed by the following statement:</span></span>

    VARIABLENAME=value

<span data-ttu-id="c4852-252">Dove VARIABLENAME è il nome della variabile.</span><span class="sxs-lookup"><span data-stu-id="c4852-252">Where VARIABLENAME is the name of the variable.</span></span> <span data-ttu-id="c4852-253">Per accedere alla variabile, usare `$VARIABLENAME`.</span><span class="sxs-lookup"><span data-stu-id="c4852-253">To access the variable, use `$VARIABLENAME`.</span></span> <span data-ttu-id="c4852-254">Per assegnare un valore fornito da un parametro posizionale come variabile di ambiente denominata PASSWORD, ad esempio, usare l'istruzione seguente:</span><span class="sxs-lookup"><span data-stu-id="c4852-254">For example, to assign a value provided by a positional parameter as an environment variable named PASSWORD, you would use the following statement:</span></span>

    PASSWORD=$1

<span data-ttu-id="c4852-255">Per il successivo accesso alle informazioni, si potrà quindi usare `$PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="c4852-255">Subsequent access to the information could then use `$PASSWORD`.</span></span>

<span data-ttu-id="c4852-256">Le variabili di ambiente impostate all'interno dello script sono disponibili solo nell'ambito dello script.</span><span class="sxs-lookup"><span data-stu-id="c4852-256">Environment variables set within the script only exist within the scope of the script.</span></span> <span data-ttu-id="c4852-257">In alcuni casi può essere necessario aggiungere variabili di ambiente a livello di sistema, che rimarranno persistenti dopo il completamento dello script.</span><span class="sxs-lookup"><span data-stu-id="c4852-257">In some cases, you may need to add system-wide environment variables that will persist after the script has finished.</span></span> <span data-ttu-id="c4852-258">Per aggiungere variabili di ambiente a livello di sistema, aggiungere la variabile a `/etc/environment`.</span><span class="sxs-lookup"><span data-stu-id="c4852-258">To add system-wide environment variables, add the variable to `/etc/environment`.</span></span> <span data-ttu-id="c4852-259">L'istruzione seguente, ad esempio, aggiunge `HADOOP_CONF_DIR`:</span><span class="sxs-lookup"><span data-stu-id="c4852-259">For example, the following statement adds `HADOOP_CONF_DIR`:</span></span>

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-to-locations-where-the-custom-scripts-are-stored"></a><span data-ttu-id="c4852-260">Accedere alle posizioni in cui sono archiviati gli script personalizzati</span><span class="sxs-lookup"><span data-stu-id="c4852-260">Access to locations where the custom scripts are stored</span></span>

<span data-ttu-id="c4852-261">Gli script usati per la personalizzazione di un cluster devono essere archiviati in una delle posizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c4852-261">Scripts used to customize a cluster needs to be stored in one of the following locations:</span></span>

* <span data-ttu-id="c4852-262">__Account di archiviazione di Azure__ associato al cluster.</span><span class="sxs-lookup"><span data-stu-id="c4852-262">An __Azure Storage account__ that is associated with the cluster.</span></span>

* <span data-ttu-id="c4852-263">__Account di archiviazione aggiuntivo__ associato al cluster.</span><span class="sxs-lookup"><span data-stu-id="c4852-263">An __additional storage account__ associated with the cluster.</span></span>

* <span data-ttu-id="c4852-264">__URI leggibile pubblicamente__,</span><span class="sxs-lookup"><span data-stu-id="c4852-264">A __publicly readable URI__.</span></span> <span data-ttu-id="c4852-265">ad esempio un URL per accedere ai dati archiviati in OneDrive, Dropbox o altri servizi di hosting di file.</span><span class="sxs-lookup"><span data-stu-id="c4852-265">For example, a URL to data stored on OneDrive, Dropbox, or other file hosting service.</span></span>

* <span data-ttu-id="c4852-266">__Account Azure Data Lake Store__ associato al cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c4852-266">An __Azure Data Lake Store account__ that is associated with the HDInsight cluster.</span></span> <span data-ttu-id="c4852-267">Per altre informazioni sull'uso di Azure Data Lake Store con HDInsight, vedere [Creare un cluster HDInsight con Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c4852-267">For more information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="c4852-268">L'entità servizio usata da HDInsight per accedere a Data Lake Store deve avere accesso in lettura allo script.</span><span class="sxs-lookup"><span data-stu-id="c4852-268">The service principal HDInsight uses to access Data Lake Store must have read access to the script.</span></span>

<span data-ttu-id="c4852-269">Anche le risorse usate dallo script devono essere disponibili pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="c4852-269">Resources used by the script must also be publicly available.</span></span>

<span data-ttu-id="c4852-270">L'archiviazione dei file in un account di archiviazione di Azure o in Azure Data Lake Store ne consentirà l'accesso in tempi rapidi, poiché si trovano entrambi nella rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="c4852-270">Storing the files in an Azure Storage account or Azure Data Lake Store provides fast access, as both within the Azure network.</span></span>

> [!NOTE]
> <span data-ttu-id="c4852-271">Il formato URI usato per fare riferimento allo script varia a seconda del servizio in uso.</span><span class="sxs-lookup"><span data-stu-id="c4852-271">The URI format used to reference the script differs depending on the service being used.</span></span> <span data-ttu-id="c4852-272">Per gli account di archiviazione associati al cluster HDInsight, usare `wasb://` o `wasbs://`.</span><span class="sxs-lookup"><span data-stu-id="c4852-272">For storage accounts associated with the HDInsight cluster, use `wasb://` or `wasbs://`.</span></span> <span data-ttu-id="c4852-273">Per gli URI leggibili pubblicamente, usare `http://` o `https://`.</span><span class="sxs-lookup"><span data-stu-id="c4852-273">For publicly readable URIs, use `http://` or `https://`.</span></span> <span data-ttu-id="c4852-274">Per Data Lake Store, usare `adl://`.</span><span class="sxs-lookup"><span data-stu-id="c4852-274">For Data Lake Store, use `adl://`.</span></span>

### <a name="checking-the-operating-system-version"></a><span data-ttu-id="c4852-275">Verifica della versione del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="c4852-275">Checking the operating system version</span></span>

<span data-ttu-id="c4852-276">Le diverse versioni di HDInsight si basano su versioni specifiche di Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c4852-276">Different versions of HDInsight rely on specific versions of Ubuntu.</span></span> <span data-ttu-id="c4852-277">Ci possono essere differenze tra le versioni del sistema operativo che è necessario verificare nello script.</span><span class="sxs-lookup"><span data-stu-id="c4852-277">There may be differences between OS versions that you must check for in your script.</span></span> <span data-ttu-id="c4852-278">Può essere ad esempio necessario installare un file binario associato alla versione di Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c4852-278">For example, you may need to install a binary that is tied to the version of Ubuntu.</span></span>

<span data-ttu-id="c4852-279">Per verificare la versione del sistema operativo usare `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="c4852-279">To check the OS version, use `lsb_release`.</span></span> <span data-ttu-id="c4852-280">Lo script seguente, ad esempio, illustra come fare riferimento a uno specifico file tar, in base alla versione del sistema operativo:</span><span class="sxs-lookup"><span data-stu-id="c4852-280">For example, the following script demonstrates how to reference a specific tar file depending on the OS version:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
```

## <span data-ttu-id="c4852-281"><a name="deployScript"></a>Elenco di controllo per la distribuzione di un'azione script</span><span class="sxs-lookup"><span data-stu-id="c4852-281"><a name="deployScript"></a>Checklist for deploying a script action</span></span>

<span data-ttu-id="c4852-282">Di seguito sono indicati i passaggi effettuati durante la preparazione della distribuzione degli script:</span><span class="sxs-lookup"><span data-stu-id="c4852-282">Here are the steps we took when preparing to deploy these scripts:</span></span>

* <span data-ttu-id="c4852-283">Inserire i file che contengono gli script personalizzati in un percorso accessibile per i nodi del cluster durante la distribuzione,</span><span class="sxs-lookup"><span data-stu-id="c4852-283">Put the files that contain the custom scripts in a place that is accessible by the cluster nodes during deployment.</span></span> <span data-ttu-id="c4852-284">ad esempio la risorsa di archiviazione predefinita per il cluster.</span><span class="sxs-lookup"><span data-stu-id="c4852-284">For example, the default storage for the cluster.</span></span> <span data-ttu-id="c4852-285">I file possono essere archiviati anche in servizi di hosting leggibili pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="c4852-285">Files can also be stored in publicly readable hosting services.</span></span>
* <span data-ttu-id="c4852-286">Verificare che lo script sia idempotente,</span><span class="sxs-lookup"><span data-stu-id="c4852-286">Verify that the script is impotent.</span></span> <span data-ttu-id="c4852-287">in modo che possa essere eseguito più volte nello stesso nodo.</span><span class="sxs-lookup"><span data-stu-id="c4852-287">Doing so allows the script to be executed multiple times on the same node.</span></span>
* <span data-ttu-id="c4852-288">Usare una directory di file temporanei /tmp per conservare i file scaricati usati dagli script e quindi eliminarli dopo aver eseguito gli script.</span><span class="sxs-lookup"><span data-stu-id="c4852-288">Use a temporary file directory /tmp to keep the downloaded files used by the scripts and then clean them up after scripts have executed.</span></span>
* <span data-ttu-id="c4852-289">Nel caso in cui vengano modificate le impostazioni a livello di sistema operativo o i file di configurazione del servizio Hadoop, può essere opportuno riavviare i servizi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c4852-289">If OS-level settings or Hadoop service configuration files are changed, you may want to restart HDInsight services.</span></span>

## <span data-ttu-id="c4852-290"><a name="runScriptAction"></a>Come eseguire un'azione script</span><span class="sxs-lookup"><span data-stu-id="c4852-290"><a name="runScriptAction"></a>How to run a script action</span></span>

<span data-ttu-id="c4852-291">È possibile usare azioni script per personalizzare i cluster HDInsight adottando uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c4852-291">You can use script actions to customize HDInsight clusters using the following methods:</span></span>

* <span data-ttu-id="c4852-292">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c4852-292">Azure portal</span></span>
* <span data-ttu-id="c4852-293">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4852-293">Azure PowerShell</span></span>
* <span data-ttu-id="c4852-294">Modelli di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="c4852-294">Azure Resource Manager templates</span></span>
* <span data-ttu-id="c4852-295">HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c4852-295">The HDInsight .NET SDK.</span></span>

<span data-ttu-id="c4852-296">Per altre informazioni sull'utilizzo di ogni metodo, vedere [Come usare azioni script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c4852-296">For more information on using each method, see [How to use script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="c4852-297"><a name="sampleScripts"></a>Esempi di script personalizzati</span><span class="sxs-lookup"><span data-stu-id="c4852-297"><a name="sampleScripts"></a>Custom script samples</span></span>

<span data-ttu-id="c4852-298">Microsoft fornisce script di esempio per installare i componenti in un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c4852-298">Microsoft provides sample scripts to install components on an HDInsight cluster.</span></span> <span data-ttu-id="c4852-299">Vedere i collegamenti seguenti per altre azioni di script di esempio.</span><span class="sxs-lookup"><span data-stu-id="c4852-299">See the following links for more example script actions.</span></span>

* [<span data-ttu-id="c4852-300">Installare e usare Hue nei cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c4852-300">Install and use Hue on HDInsight clusters</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="c4852-301">Installare e usare Solr nei cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4852-301">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="c4852-302">Installare e usare Giraph nei cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4852-302">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="c4852-303">Installare o aggiornare Mono nei cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4852-303">Install or upgrade Mono on HDInsight clusters</span></span>](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a><span data-ttu-id="c4852-304">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="c4852-304">Troubleshooting</span></span>

<span data-ttu-id="c4852-305">Di seguito sono elencati gli errori che potrebbero essere visualizzati quando si usano script personalizzati:</span><span class="sxs-lookup"><span data-stu-id="c4852-305">The following are errors you may encounter when using scripts you have developed:</span></span>

<span data-ttu-id="c4852-306">**Errore**: `$'\r': command not found`.</span><span class="sxs-lookup"><span data-stu-id="c4852-306">**Error**: `$'\r': command not found`.</span></span> <span data-ttu-id="c4852-307">A volte seguito da `syntax error: unexpected end of file`.</span><span class="sxs-lookup"><span data-stu-id="c4852-307">Sometimes followed by `syntax error: unexpected end of file`.</span></span>

<span data-ttu-id="c4852-308">*Causa*: questo errore si verifica quando le righe di uno script terminano con CRLF.</span><span class="sxs-lookup"><span data-stu-id="c4852-308">*Cause*: This error is caused when the lines in a script end with CRLF.</span></span> <span data-ttu-id="c4852-309">I sistemi Unix prevedono unicamente LF come terminazione di riga.</span><span class="sxs-lookup"><span data-stu-id="c4852-309">Unix systems expect only LF as the line ending.</span></span>

<span data-ttu-id="c4852-310">Questo problema si verifica più spesso quando lo script viene creato in un ambiente Windows, perché CRLF è una terminazione di riga comune per molti editor di testo in Windows.</span><span class="sxs-lookup"><span data-stu-id="c4852-310">This problem most often occurs when the script is authored on a Windows environment, as CRLF is a common line ending for many text editors on Windows.</span></span>

<span data-ttu-id="c4852-311">*Risoluzione*: se nell'editor di testo è disponibile come opzione, selezionare il formato Unix o LF come terminazione di riga.</span><span class="sxs-lookup"><span data-stu-id="c4852-311">*Resolution*: If it is an option in your text editor, select Unix format or LF for the line ending.</span></span> <span data-ttu-id="c4852-312">È anche possibile usare i comandi seguenti in un sistema Unix per cambiare CRLF in LF:</span><span class="sxs-lookup"><span data-stu-id="c4852-312">You may also use the following commands on a Unix system to change the CRLF to an LF:</span></span>

> [!NOTE]
> <span data-ttu-id="c4852-313">I comandi seguenti sono all'incirca equivalenti nel senso che cambiano le terminazioni di riga CRLF in LF.</span><span class="sxs-lookup"><span data-stu-id="c4852-313">The following commands are roughly equivalent in that they should change the CRLF line endings to LF.</span></span> <span data-ttu-id="c4852-314">Selezionarne uno in base alle utilità disponibili nel proprio sistema.</span><span class="sxs-lookup"><span data-stu-id="c4852-314">Select one based on the utilities available on your system.</span></span>

| <span data-ttu-id="c4852-315">Comando</span><span class="sxs-lookup"><span data-stu-id="c4852-315">Command</span></span> | <span data-ttu-id="c4852-316">Note</span><span class="sxs-lookup"><span data-stu-id="c4852-316">Notes</span></span> |
| --- | --- |
| `unix2dos -b INFILE` |<span data-ttu-id="c4852-317">Viene creata una copia di backup del file originale con estensione BAK</span><span class="sxs-lookup"><span data-stu-id="c4852-317">The original file is backed up with a .BAK extension</span></span> |
| `tr -d '\r' < INFILE > OUTFILE` |<span data-ttu-id="c4852-318">OUTFILE contiene una versione solo con le terminazioni LF</span><span class="sxs-lookup"><span data-stu-id="c4852-318">OUTFILE contains a version with only LF endings</span></span> |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | <span data-ttu-id="c4852-319">Modifica direttamente il file</span><span class="sxs-lookup"><span data-stu-id="c4852-319">Modifies the file directly</span></span> |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |<span data-ttu-id="c4852-320">OUTFILE contiene una versione solo con le terminazioni LF.</span><span class="sxs-lookup"><span data-stu-id="c4852-320">OUTFILE contains a version with only LF endings.</span></span> |

<span data-ttu-id="c4852-321">**Errore**: `line 1: #!/usr/bin/env: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="c4852-321">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span></span>

<span data-ttu-id="c4852-322">*Causa*: questo errore si verifica quando lo script è stato salvato in formato UTF-8 con un byte order mark (BOM).</span><span class="sxs-lookup"><span data-stu-id="c4852-322">*Cause*: This error occurs when the script was saved as UTF-8 with a Byte Order Mark (BOM).</span></span>

<span data-ttu-id="c4852-323">*Risoluzione*: salvare il file in formato ASCII o UTF-8 senza un carattere BOM.</span><span class="sxs-lookup"><span data-stu-id="c4852-323">*Resolution*: Save the file either as ASCII, or as UTF-8 without a BOM.</span></span> <span data-ttu-id="c4852-324">È anche possibile usare il comando seguente in un sistema Linux o Unix per creare un file senza il carattere BOM:</span><span class="sxs-lookup"><span data-stu-id="c4852-324">You may also use the following command on a Linux or Unix system to create a file without the BOM:</span></span>

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

<span data-ttu-id="c4852-325">Sostituire `INFILE` con il file contenente il carattere BOM.</span><span class="sxs-lookup"><span data-stu-id="c4852-325">Replace `INFILE` with the file containing the BOM.</span></span> <span data-ttu-id="c4852-326">`OUTFILE` deve essere un nuovo nome di file, contenente lo script senza il carattere BOM.</span><span class="sxs-lookup"><span data-stu-id="c4852-326">`OUTFILE` should be a new file name, which contains the script without the BOM.</span></span>

## <span data-ttu-id="c4852-327"><a name="seeAlso"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c4852-327"><a name="seeAlso"></a>Next steps</span></span>

* <span data-ttu-id="c4852-328">Informazioni su come [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="c4852-328">Learn how to [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
* <span data-ttu-id="c4852-329">Per informazioni sulla creazione di applicazioni .NET che gestiscono HDInsight, vedere [Riferimento .NET per HDInsight](https://msdn.microsoft.com/library/mt271028.aspx)</span><span class="sxs-lookup"><span data-stu-id="c4852-329">Use the [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx) to learn more about creating .NET applications that manage HDInsight</span></span>
* <span data-ttu-id="c4852-330">Per informazioni su come usare REST per eseguire azioni di gestione nei cluster HDInsight, vedere l' [API REST del provider di risorse HDInsight](https://msdn.microsoft.com/library/azure/mt622197.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c4852-330">Use the [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) to learn how to use REST to perform management actions on HDInsight clusters.</span></span>
