---
title: lo sviluppo dell'azione aaaScript con HDInsight basati su Linux - Azure | Documenti Microsoft
description: "Informazioni su come generare script per i cluster HDInsight basati su Linux toocustomize toouse Bash. Hello script azione di HDInsight consente toorun script durante o dopo la creazione del cluster. Gli script è possibile toochange utilizzate le impostazioni di configurazione del cluster o installare software aggiuntivo."
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
ms.openlocfilehash: 1f504b00365df5f4cfb3ae19ad55ff7630342650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="script-action-development-with-hdinsight"></a><span data-ttu-id="7331f-105">Sviluppo di azioni script con HDInsight</span><span class="sxs-lookup"><span data-stu-id="7331f-105">Script action development with HDInsight</span></span>

<span data-ttu-id="7331f-106">Informazioni su come è il cluster HDInsight tramite Bash toocustomize script.</span><span class="sxs-lookup"><span data-stu-id="7331f-106">Learn how toocustomize your HDInsight cluster using Bash scripts.</span></span> <span data-ttu-id="7331f-107">Le azioni script sono toocustomize un modo HDInsight durante o dopo la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="7331f-107">Script actions are a way toocustomize HDInsight during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7331f-108">passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Linux.</span><span class="sxs-lookup"><span data-stu-id="7331f-108">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="7331f-109">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="7331f-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7331f-110">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7331f-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="what-are-script-actions"></a><span data-ttu-id="7331f-111">Definizione di azioni script</span><span class="sxs-lookup"><span data-stu-id="7331f-111">What are script actions</span></span>

<span data-ttu-id="7331f-112">Le azioni script sono gli script Bash Azure viene eseguito sulle modifiche di configurazione toomake nodi cluster hello o installare software.</span><span class="sxs-lookup"><span data-stu-id="7331f-112">Script actions are Bash scripts that Azure runs on hello cluster nodes toomake configuration changes or install software.</span></span> <span data-ttu-id="7331f-113">Un'azione di script viene eseguita come radice e fornisce i nodi del cluster toohello diritti di accesso completo.</span><span class="sxs-lookup"><span data-stu-id="7331f-113">A script action is executed as root, and provides full access rights toohello cluster nodes.</span></span>

<span data-ttu-id="7331f-114">Le azioni script possono essere applicate tramite hello dei seguenti metodi:</span><span class="sxs-lookup"><span data-stu-id="7331f-114">Script actions can be applied through hello following methods:</span></span>

| <span data-ttu-id="7331f-115">Utilizzare questo tooapply metodo uno script...</span><span class="sxs-lookup"><span data-stu-id="7331f-115">Use this method tooapply a script...</span></span> | <span data-ttu-id="7331f-116">Durante la creazione di un cluster...</span><span class="sxs-lookup"><span data-stu-id="7331f-116">During cluster creation...</span></span> | <span data-ttu-id="7331f-117">In un cluster in esecuzione...</span><span class="sxs-lookup"><span data-stu-id="7331f-117">On a running cluster...</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="7331f-118">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7331f-118">Azure portal</span></span> |<span data-ttu-id="7331f-119">✓ </span><span class="sxs-lookup"><span data-stu-id="7331f-119">✓</span></span> |<span data-ttu-id="7331f-120">✓</span><span class="sxs-lookup"><span data-stu-id="7331f-120">✓</span></span> |
| <span data-ttu-id="7331f-121">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7331f-121">Azure PowerShell</span></span> |<span data-ttu-id="7331f-122">✓</span><span class="sxs-lookup"><span data-stu-id="7331f-122">✓</span></span> |<span data-ttu-id="7331f-123">✓</span><span class="sxs-lookup"><span data-stu-id="7331f-123">✓</span></span> |
| <span data-ttu-id="7331f-124">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="7331f-124">Azure CLI</span></span> |&nbsp; |<span data-ttu-id="7331f-125">✓</span><span class="sxs-lookup"><span data-stu-id="7331f-125">✓</span></span> |
| <span data-ttu-id="7331f-126">HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7331f-126">HDInsight .NET SDK</span></span> |<span data-ttu-id="7331f-127">✓</span><span class="sxs-lookup"><span data-stu-id="7331f-127">✓</span></span> |<span data-ttu-id="7331f-128">✓</span><span class="sxs-lookup"><span data-stu-id="7331f-128">✓</span></span> |
| <span data-ttu-id="7331f-129">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7331f-129">Azure Resource Manager Template</span></span> |<span data-ttu-id="7331f-130">✓</span><span class="sxs-lookup"><span data-stu-id="7331f-130">✓</span></span> |&nbsp; |

<span data-ttu-id="7331f-131">Per ulteriori informazioni sull'utilizzo di questi script azione tooapply metodi, vedere [HDInsight personalizzare cluster tramite le azioni script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7331f-131">For more information on using these methods tooapply script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="7331f-132"><a name="bestPracticeScripting"></a>Procedure consigliate per lo sviluppo di script</span><span class="sxs-lookup"><span data-stu-id="7331f-132"><a name="bestPracticeScripting"></a>Best practices for script development</span></span>

<span data-ttu-id="7331f-133">Quando si sviluppa uno script personalizzato per un cluster HDInsight, sono disponibili diverse procedure tookeep di procedure consigliate in considerazione:</span><span class="sxs-lookup"><span data-stu-id="7331f-133">When you develop a custom script for an HDInsight cluster, there are several best practices tookeep in mind:</span></span>

* [<span data-ttu-id="7331f-134">Versione di destinazione hello Hadoop</span><span class="sxs-lookup"><span data-stu-id="7331f-134">Target hello Hadoop version</span></span>](#bPS1)
* [<span data-ttu-id="7331f-135">Hello versione del sistema operativo di destinazione</span><span class="sxs-lookup"><span data-stu-id="7331f-135">Target hello OS Version</span></span>](#bps10)
* [<span data-ttu-id="7331f-136">Fornire stabile collega tooscript risorse</span><span class="sxs-lookup"><span data-stu-id="7331f-136">Provide stable links tooscript resources</span></span>](#bPS2)
* [<span data-ttu-id="7331f-137">Usare risorse precompilate</span><span class="sxs-lookup"><span data-stu-id="7331f-137">Use pre-compiled resources</span></span>](#bPS4)
* [<span data-ttu-id="7331f-138">Verificare che uno script di personalizzazione cluster hello è idempotente</span><span class="sxs-lookup"><span data-stu-id="7331f-138">Ensure that hello cluster customization script is idempotent</span></span>](#bPS3)
* [<span data-ttu-id="7331f-139">Verificare la disponibilità elevata dell'architettura di cluster hello</span><span class="sxs-lookup"><span data-stu-id="7331f-139">Ensure high availability of hello cluster architecture</span></span>](#bPS5)
* [<span data-ttu-id="7331f-140">Configurare l'archiviazione Blob di Azure toouse componenti personalizzati di hello</span><span class="sxs-lookup"><span data-stu-id="7331f-140">Configure hello custom components toouse Azure Blob storage</span></span>](#bPS6)
* [<span data-ttu-id="7331f-141">Scrivere informazioni tooSTDOUT e STDERR</span><span class="sxs-lookup"><span data-stu-id="7331f-141">Write information tooSTDOUT and STDERR</span></span>](#bPS7)
* [<span data-ttu-id="7331f-142">Salvare i file in formato ASCII con terminazioni di riga LF</span><span class="sxs-lookup"><span data-stu-id="7331f-142">Save files as ASCII with LF line endings</span></span>](#bps8)
* [<span data-ttu-id="7331f-143">Utilizzare toorecover logica di tentativi di errori temporanei</span><span class="sxs-lookup"><span data-stu-id="7331f-143">Use retry logic toorecover from transient errors</span></span>](#bps9)

> [!IMPORTANT]
> <span data-ttu-id="7331f-144">Le azioni script devono essere completate entro 60 minuti o hello processo avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="7331f-144">Script actions must complete within 60 minutes or hello process fails.</span></span> <span data-ttu-id="7331f-145">Durante il provisioning del nodo, script di hello viene eseguito contemporaneamente ad altri processi di installazione e configurazione.</span><span class="sxs-lookup"><span data-stu-id="7331f-145">During node provisioning, hello script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="7331f-146">Contesa per le risorse, ad esempio larghezza di banda della CPU ora o di rete potrebbe essere hello script tootake più toofinish rispetto a quello usato nell'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="7331f-146">Competition for resources such as CPU time or network bandwidth may cause hello script tootake longer toofinish than it does in your development environment.</span></span>

### <span data-ttu-id="7331f-147"><a name="bPS1"></a>Versione di destinazione hello Hadoop</span><span class="sxs-lookup"><span data-stu-id="7331f-147"><a name="bPS1"></a>Target hello Hadoop version</span></span>

<span data-ttu-id="7331f-148">Nelle diverse versioni di HDInsight sono installate versioni diverse di servizi e componenti di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="7331f-148">Different versions of HDInsight have different versions of Hadoop services and components installed.</span></span> <span data-ttu-id="7331f-149">Se lo script prevede una versione specifica di un servizio o componente, è necessario utilizzare solo script di hello con la versione di hello di HDInsight che include i componenti necessario di hello.</span><span class="sxs-lookup"><span data-stu-id="7331f-149">If your script expects a specific version of a service or component, you should only use hello script with hello version of HDInsight that includes hello required components.</span></span> <span data-ttu-id="7331f-150">È possibile trovare informazioni sulle versioni dei componenti inclusi in HDInsight usando hello [il controllo delle versioni di HDInsight componente](hdinsight-component-versioning.md) documento.</span><span class="sxs-lookup"><span data-stu-id="7331f-150">You can find information on component versions included with HDInsight using hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

### <span data-ttu-id="7331f-151"><a name="bps10"></a>Versione di hello del sistema operativo di destinazione</span><span class="sxs-lookup"><span data-stu-id="7331f-151"><a name="bps10"></a> Target hello OS version</span></span>

<span data-ttu-id="7331f-152">HDInsight basati su Linux si basa su hello distribuzione Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="7331f-152">Linux-based HDInsight is based on hello Ubuntu Linux distribution.</span></span> <span data-ttu-id="7331f-153">Versioni diverse di HDInsight si basano su versioni differenti di Ubuntu e questo può influire sul comportamento dello script.</span><span class="sxs-lookup"><span data-stu-id="7331f-153">Different versions of HDInsight rely on different versions of Ubuntu, which may change how your script behaves.</span></span> <span data-ttu-id="7331f-154">HDInsight 3.4 e versioni precedenti si basano ad esempio su versioni di Ubuntu che usano Upstart.</span><span class="sxs-lookup"><span data-stu-id="7331f-154">For example, HDInsight 3.4 and earlier are based on Ubuntu versions that use Upstart.</span></span> <span data-ttu-id="7331f-155">La versione 3.5 si basa su Ubuntu 16.04 che usa Systemd.</span><span class="sxs-lookup"><span data-stu-id="7331f-155">Version 3.5 is based on Ubuntu 16.04, which uses Systemd.</span></span> <span data-ttu-id="7331f-156">Systemd e Upstart si basano sui diversi comandi, in modo che lo script deve essere scritto toowork con entrambi.</span><span class="sxs-lookup"><span data-stu-id="7331f-156">Systemd and Upstart rely on different commands, so your script should be written toowork with both.</span></span>

<span data-ttu-id="7331f-157">Un'altra differenza importante tra 3.4 HDInsight e 3.5 è che `JAVA_HOME` punti ora tooJava 8.</span><span class="sxs-lookup"><span data-stu-id="7331f-157">Another important difference between HDInsight 3.4 and 3.5 is that `JAVA_HOME` now points tooJava 8.</span></span>

<span data-ttu-id="7331f-158">È possibile controllare la versione del sistema operativo hello utilizzando `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="7331f-158">You can check hello OS version by using `lsb_release`.</span></span> <span data-ttu-id="7331f-159">Hello codice seguente viene illustrato come toodetermine se hello script è in esecuzione in Ubuntu 14 o 16:</span><span class="sxs-lookup"><span data-stu-id="7331f-159">hello following code demonstrates how toodetermine if hello script is running on Ubuntu 14 or 16:</span></span>

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

<span data-ttu-id="7331f-160">È possibile trovare uno script completo di hello contenente questi frammenti di codice in https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span><span class="sxs-lookup"><span data-stu-id="7331f-160">You can find hello full script that contains these snippets at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span></span>

<span data-ttu-id="7331f-161">La versione di hello di Ubuntu utilizzato da HDInsight, vedere hello [la versione del componente HDInsight](hdinsight-component-versioning.md) documento.</span><span class="sxs-lookup"><span data-stu-id="7331f-161">For hello version of Ubuntu that is used by HDInsight, see hello [HDInsight component version](hdinsight-component-versioning.md) document.</span></span>

<span data-ttu-id="7331f-162">differenze di hello toounderstand tra Systemd e Upstart, vedere [Systemd per gli utenti Upstart](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span><span class="sxs-lookup"><span data-stu-id="7331f-162">toounderstand hello differences between Systemd and Upstart, see [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span></span>

### <span data-ttu-id="7331f-163"><a name="bPS2"></a>Fornire stabile collega tooscript risorse</span><span class="sxs-lookup"><span data-stu-id="7331f-163"><a name="bPS2"></a>Provide stable links tooscript resources</span></span>

<span data-ttu-id="7331f-164">Hello script e le risorse associate devono rimanere disponibile per tutta la durata di hello del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="7331f-164">hello script and associated resources must remain available throughout hello lifetime of hello cluster.</span></span> <span data-ttu-id="7331f-165">Queste risorse sono necessarie se vengono aggiunti nuovi nodi cluster toohello durante le operazioni di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="7331f-165">These resources are required if new nodes are added toohello cluster during scaling operations.</span></span>

<span data-ttu-id="7331f-166">procedura consigliata Hello è toodownload e archiviare tutti gli elementi di un account di archiviazione di Azure nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="7331f-166">hello best practice is toodownload and archive everything in an Azure Storage account on your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7331f-167">account di archiviazione Hello usato deve essere l'account di archiviazione predefinito hello per cluster hello o un contenitore di sola lettura pubblico su qualsiasi altro account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7331f-167">hello storage account used must be hello default storage account for hello cluster or a public, read-only container on any other storage account.</span></span>

<span data-ttu-id="7331f-168">Ad esempio, gli esempi di hello forniti da Microsoft vengono archiviati in hello [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7331f-168">For example, hello samples provided by Microsoft are stored in hello [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage account.</span></span> <span data-ttu-id="7331f-169">Si tratta di un contenitore di sola lettura pubblico gestito dal team di HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="7331f-169">This is a public, read-only container maintained by hello HDInsight team.</span></span>

### <span data-ttu-id="7331f-170"><a name="bPS4"></a>Usare risorse precompilate</span><span class="sxs-lookup"><span data-stu-id="7331f-170"><a name="bPS4"></a>Use pre-compiled resources</span></span>

<span data-ttu-id="7331f-171">hello tooreduce tempo accetta toorun hello script, evitare operazioni di compilazione risorse dal codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="7331f-171">tooreduce hello time it takes toorun hello script, avoid operations that compile resources from source code.</span></span> <span data-ttu-id="7331f-172">Ad esempio, la precompilazione risorse e archiviarli in un blob dell'account di archiviazione di Azure in hello stesso data center in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7331f-172">For example, pre-compile resources and store them in an Azure Storage account blob in hello same data center as HDInsight.</span></span>

### <span data-ttu-id="7331f-173"><a name="bPS3"></a>Verificare che uno script di personalizzazione cluster hello è idempotente</span><span class="sxs-lookup"><span data-stu-id="7331f-173"><a name="bPS3"></a>Ensure that hello cluster customization script is idempotent</span></span>

<span data-ttu-id="7331f-174">Gli script devono essere idempotenti.</span><span class="sxs-lookup"><span data-stu-id="7331f-174">Scripts must be idempotent.</span></span> <span data-ttu-id="7331f-175">Se viene eseguito più volte di script di hello, dovrebbe restituire hello toohello cluster stesso stato di ogni volta.</span><span class="sxs-lookup"><span data-stu-id="7331f-175">If hello script runs multiple times, it should return hello cluster toohello same state every time.</span></span>

<span data-ttu-id="7331f-176">Uno script che modifica i file di configurazione, ad esempio, non deve aggiungere voci duplicate se viene eseguito più volte.</span><span class="sxs-lookup"><span data-stu-id="7331f-176">For example, a script that modifies configuration files should not add duplicate entries if ran multiple times.</span></span>

### <span data-ttu-id="7331f-177"><a name="bPS5"></a>Verificare la disponibilità elevata dell'architettura di cluster hello</span><span class="sxs-lookup"><span data-stu-id="7331f-177"><a name="bPS5"></a>Ensure high availability of hello cluster architecture</span></span>

<span data-ttu-id="7331f-178">Cluster HDInsight basati su Linux forniscono due nodi head attivi all'interno di cluster hello e le azioni di script vengono eseguite in entrambi i nodi.</span><span class="sxs-lookup"><span data-stu-id="7331f-178">Linux-based HDInsight clusters provide two head nodes that are active within hello cluster, and script actions run on both nodes.</span></span> <span data-ttu-id="7331f-179">Se si installa i componenti di hello prevedono un solo nodo head, non installare i componenti di hello in entrambi i nodi head.</span><span class="sxs-lookup"><span data-stu-id="7331f-179">If hello components you install expect only one head node, do not install hello components on both head nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7331f-180">Fornito come parte di HDInsight sono servizi toofail progettato tra due nodi head di hello in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="7331f-180">Services provided as part of HDInsight are designed toofail over between hello two head nodes as needed.</span></span> <span data-ttu-id="7331f-181">Questa funzionalità non viene estesa toocustom componenti installati tramite le azioni script.</span><span class="sxs-lookup"><span data-stu-id="7331f-181">This functionality is not extended toocustom components installed through script actions.</span></span> <span data-ttu-id="7331f-182">Se i componenti personalizzati richiedono una disponibilità elevata, è necessario implementare un meccanismo di failover personalizzato.</span><span class="sxs-lookup"><span data-stu-id="7331f-182">If you need high availability for custom components, you must implement your own failover mechanism.</span></span>

### <span data-ttu-id="7331f-183"><a name="bPS6"></a>Configurare l'archiviazione Blob di Azure toouse componenti personalizzati di hello</span><span class="sxs-lookup"><span data-stu-id="7331f-183"><a name="bPS6"></a>Configure hello custom components toouse Azure Blob storage</span></span>

<span data-ttu-id="7331f-184">I componenti da installare nel cluster hello potrebbero essere una configurazione predefinita che utilizza l'archiviazione di Hadoop Distributed File System (HDFS).</span><span class="sxs-lookup"><span data-stu-id="7331f-184">Components that you install on hello cluster might have a default configuration that uses Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="7331f-185">HDInsight Usa archiviazione di Azure o archivio Data Lake come spazio di archiviazione predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="7331f-185">HDInsight uses either Azure Storage or Data Lake Store as hello default storage.</span></span> <span data-ttu-id="7331f-186">Forniscono entrambi un sistema compatibile file HDFS che mantiene i dati anche se hello cluster verrà eliminato.</span><span class="sxs-lookup"><span data-stu-id="7331f-186">Both provide an HDFS compatible file system that persists data even if hello cluster is deleted.</span></span> <span data-ttu-id="7331f-187">Potrebbe essere necessario tooconfigure componenti installati toouse WASB o ADL anziché HDFS.</span><span class="sxs-lookup"><span data-stu-id="7331f-187">You may need tooconfigure components you install toouse WASB or ADL instead of HDFS.</span></span>

<span data-ttu-id="7331f-188">Per la maggior parte delle operazioni, non è necessario del sistema di file hello toospecify.</span><span class="sxs-lookup"><span data-stu-id="7331f-188">For most operations, you do not need toospecify hello file system.</span></span> <span data-ttu-id="7331f-189">Ad esempio, seguente hello copia file giraph examples.jar hello dalla hello archivio locale del sistema toocluster dei file:</span><span class="sxs-lookup"><span data-stu-id="7331f-189">For example, hello following copies hello giraph-examples.jar file from hello local file system toocluster storage:</span></span>

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

<span data-ttu-id="7331f-190">In questo esempio hello `hdfs` comando utilizza in modo trasparente l'archiviazione del cluster predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="7331f-190">In this example, hello `hdfs` command transparently uses hello default cluster storage.</span></span> <span data-ttu-id="7331f-191">Per alcune operazioni, potrebbe essere necessario toospecify hello URI.</span><span class="sxs-lookup"><span data-stu-id="7331f-191">For some operations, you may need toospecify hello URI.</span></span> <span data-ttu-id="7331f-192">ad esempio `adl:///example/jars` per Data Lake Store o `wasb:///example/jars` per l'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7331f-192">For example, `adl:///example/jars` for Data Lake Store or `wasb:///example/jars` for Azure Storage.</span></span>

### <span data-ttu-id="7331f-193"><a name="bPS7"></a>Scrivere informazioni tooSTDOUT e STDERR</span><span class="sxs-lookup"><span data-stu-id="7331f-193"><a name="bPS7"></a>Write information tooSTDOUT and STDERR</span></span>

<span data-ttu-id="7331f-194">HDInsight registra l'output dello script che viene scritto tooSTDOUT e STDERR.</span><span class="sxs-lookup"><span data-stu-id="7331f-194">HDInsight logs script output that is written tooSTDOUT and STDERR.</span></span> <span data-ttu-id="7331f-195">È possibile visualizzare queste informazioni tramite interfaccia utente di hello Ambari web.</span><span class="sxs-lookup"><span data-stu-id="7331f-195">You can view this information using hello Ambari web UI.</span></span>

> [!NOTE]
> <span data-ttu-id="7331f-196">Ambari è disponibile solo se il cluster hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="7331f-196">Ambari is only available if hello cluster is successfully created.</span></span> <span data-ttu-id="7331f-197">Se si utilizza un'azione di script durante la creazione del cluster e non viene completata la creazione, vedere Risoluzione dei problemi di sezione hello [HDInsight personalizzare cluster utilizzando l'azione script](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) per altre modalità di accesso alle informazioni registrate.</span><span class="sxs-lookup"><span data-stu-id="7331f-197">If you use a script action during cluster creation, and creation fails, see hello troubleshooting section [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) for other ways of accessing logged information.</span></span>

<span data-ttu-id="7331f-198">La maggior parte delle utilità e pacchetti di installazione già scrivono informazioni tooSTDOUT e STDERR, tuttavia è opportuno tooadd ulteriori opzioni di registrazione.</span><span class="sxs-lookup"><span data-stu-id="7331f-198">Most utilities and installation packages already write information tooSTDOUT and STDERR, however you may want tooadd additional logging.</span></span> <span data-ttu-id="7331f-199">toosend testo tooSTDOUT, utilizzare `echo`.</span><span class="sxs-lookup"><span data-stu-id="7331f-199">toosend text tooSTDOUT, use `echo`.</span></span> <span data-ttu-id="7331f-200">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="7331f-200">For example:</span></span>

```bash
echo "Getting ready tooinstall Foo"
```

<span data-ttu-id="7331f-201">Per impostazione predefinita, `echo` invia hello tooSTDOUT stringa.</span><span class="sxs-lookup"><span data-stu-id="7331f-201">By default, `echo` sends hello string tooSTDOUT.</span></span> <span data-ttu-id="7331f-202">toodirect è tooSTDERR, aggiungere `>&2` prima `echo`.</span><span class="sxs-lookup"><span data-stu-id="7331f-202">toodirect it tooSTDERR, add `>&2` before `echo`.</span></span> <span data-ttu-id="7331f-203">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="7331f-203">For example:</span></span>

```bash
>&2 echo "An error occurred installing Foo"
```

<span data-ttu-id="7331f-204">Consente di reindirizzare le informazioni scritte invece tooSTDOUT tooSTDERR (2).</span><span class="sxs-lookup"><span data-stu-id="7331f-204">This redirects information written tooSTDOUT tooSTDERR (2) instead.</span></span> <span data-ttu-id="7331f-205">Per altre informazioni sul reindirizzamento I/O, vedere [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span><span class="sxs-lookup"><span data-stu-id="7331f-205">For more information on IO redirection, see [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span></span>

<span data-ttu-id="7331f-206">Per altre informazioni sulla visualizzazione delle informazioni registrate tramite azioni script, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span><span class="sxs-lookup"><span data-stu-id="7331f-206">For more information on viewing information logged by script actions, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span></span>

### <span data-ttu-id="7331f-207"><a name="bps8"></a> Salvare i file in formato ASCII con terminazioni di riga LF</span><span class="sxs-lookup"><span data-stu-id="7331f-207"><a name="bps8"></a> Save files as ASCII with LF line endings</span></span>

<span data-ttu-id="7331f-208">Gli script Bash devono essere archiviati nel formato ASCII con righe terminate da LF.</span><span class="sxs-lookup"><span data-stu-id="7331f-208">Bash scripts should be stored as ASCII format, with lines terminated by LF.</span></span> <span data-ttu-id="7331f-209">I file vengono archiviati come UTF-8 o utilizzano CRLF come terminazione di riga hello potrebbero non riuscire con hello errore seguente:</span><span class="sxs-lookup"><span data-stu-id="7331f-209">Files that are stored as UTF-8, or use CRLF as hello line ending may fail with hello following error:</span></span>

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <span data-ttu-id="7331f-210"><a name="bps9"></a>Utilizzare toorecover logica di tentativi di errori temporanei</span><span class="sxs-lookup"><span data-stu-id="7331f-210"><a name="bps9"></a> Use retry logic toorecover from transient errors</span></span>

<span data-ttu-id="7331f-211">Quando si scaricano file, l'installazione dei pacchetti tramite apt get o altre azioni che trasmettono dati su internet hello, azione hello potrebbe non riuscire a causa di errori di rete tootransient.</span><span class="sxs-lookup"><span data-stu-id="7331f-211">When downloading files, installing packages using apt-get, or other actions that transmit data over hello internet, hello action may fail due tootransient networking errors.</span></span> <span data-ttu-id="7331f-212">Ad esempio, si sta comunicando con la risorsa remota hello sia nel processo di hello del failover sul nodo backup tooa.</span><span class="sxs-lookup"><span data-stu-id="7331f-212">For example, hello remote resource you are communicating with may be in hello process of failing over tooa backup node.</span></span>

<span data-ttu-id="7331f-213">toomake gli errori di tootransient resilienti script, è possibile implementare la logica di ripetizione.</span><span class="sxs-lookup"><span data-stu-id="7331f-213">toomake your script resilient tootransient errors, you can implement retry logic.</span></span> <span data-ttu-id="7331f-214">Hello che segue viene illustrato come la logica di riesecuzione tooimplement.</span><span class="sxs-lookup"><span data-stu-id="7331f-214">hello following function demonstrates how tooimplement retry logic.</span></span> <span data-ttu-id="7331f-215">Eseguire un nuovo tentativo operazione hello tre volte prima che si verifichi.</span><span class="sxs-lookup"><span data-stu-id="7331f-215">It retries hello operation three times before failing.</span></span>

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

<span data-ttu-id="7331f-216">Hello esempi seguenti illustrano come toouse questa funzione.</span><span class="sxs-lookup"><span data-stu-id="7331f-216">hello following examples demonstrate how toouse this function.</span></span>

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <span data-ttu-id="7331f-217"><a name="helpermethods"></a>Metodi helper per gli script personalizzati</span><span class="sxs-lookup"><span data-stu-id="7331f-217"><a name="helpermethods"></a>Helper methods for custom scripts</span></span>

<span data-ttu-id="7331f-218">I metodi helper dell'azione script sono utilità che è possibile usare durante la scrittura di script personalizzati.</span><span class="sxs-lookup"><span data-stu-id="7331f-218">Script action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="7331f-219">Questi metodi sono contenuti nello script [https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="7331f-219">These methods are contained in the[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script.</span></span> <span data-ttu-id="7331f-220">Utilizzare hello seguente toodownload e utilizzarle come parte dello script:</span><span class="sxs-lookup"><span data-stu-id="7331f-220">Use hello following toodownload and use them as part of your script:</span></span>

```bash
# Import hello helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

<span data-ttu-id="7331f-221">Hello helper disponibili per l'utilizzo nello script seguente:</span><span class="sxs-lookup"><span data-stu-id="7331f-221">hello following helpers available for use in your script:</span></span>

| <span data-ttu-id="7331f-222">Utilizzo dell'helper</span><span class="sxs-lookup"><span data-stu-id="7331f-222">Helper usage</span></span> | <span data-ttu-id="7331f-223">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7331f-223">Description</span></span> |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |<span data-ttu-id="7331f-224">Scarica un file dal percorso del file specificato toohello hello origine URI.</span><span class="sxs-lookup"><span data-stu-id="7331f-224">Downloads a file from hello source URI toohello specified file path.</span></span> <span data-ttu-id="7331f-225">Per impostazione predefinita, non sovrascrive un file esistente.</span><span class="sxs-lookup"><span data-stu-id="7331f-225">By default, it does not overwrite an existing file.</span></span> |
| `untar_file TARFILE DESTDIR` |<span data-ttu-id="7331f-226">Estrae un file con estensione tar (utilizzando `-xf`) toohello directory di destinazione.</span><span class="sxs-lookup"><span data-stu-id="7331f-226">Extracts a tar file (using `-xf`) toohello destination directory.</span></span> |
| `test_is_headnode` |<span data-ttu-id="7331f-227">Se viene eseguito su un nodo head del cluster restituisce 1; in caso contrario, 0.</span><span class="sxs-lookup"><span data-stu-id="7331f-227">If ran on a cluster head node, return 1; otherwise, 0.</span></span> |
| `test_is_datanode` |<span data-ttu-id="7331f-228">Se il nodo corrente hello è un nodo di dati (lavoratore), restituisce 1; in caso contrario, 0.</span><span class="sxs-lookup"><span data-stu-id="7331f-228">If hello current node is a data (worker) node, return a 1; otherwise, 0.</span></span> |
| `test_is_first_datanode` |<span data-ttu-id="7331f-229">Se il nodo corrente di hello è hello innanzitutto i dati (lavoratore) nodo (denominata workernode0) restituisce 1; in caso contrario, 0.</span><span class="sxs-lookup"><span data-stu-id="7331f-229">If hello current node is hello first data (worker) node (named workernode0) return a 1; otherwise, 0.</span></span> |
| `get_headnodes` |<span data-ttu-id="7331f-230">Restituisce il nome di dominio completo hello di hello headnodes cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7331f-230">Return hello fully qualified domain name of hello headnodes in hello cluster.</span></span> <span data-ttu-id="7331f-231">I nomi sono delimitati da virgole.</span><span class="sxs-lookup"><span data-stu-id="7331f-231">Names are comma delimited.</span></span> <span data-ttu-id="7331f-232">In caso di errore, viene restituita una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="7331f-232">An empty string is returned on error.</span></span> |
| `get_primary_headnode` |<span data-ttu-id="7331f-233">Ottiene il nome di dominio completo hello del nodo head primario hello.</span><span class="sxs-lookup"><span data-stu-id="7331f-233">Gets hello fully qualified domain name of hello primary headnode.</span></span> <span data-ttu-id="7331f-234">In caso di errore, viene restituita una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="7331f-234">An empty string is returned on error.</span></span> |
| `get_secondary_headnode` |<span data-ttu-id="7331f-235">Ottiene il nome di dominio completo hello del nodo head secondario hello.</span><span class="sxs-lookup"><span data-stu-id="7331f-235">Gets hello fully qualified domain name of hello secondary headnode.</span></span> <span data-ttu-id="7331f-236">In caso di errore, viene restituita una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="7331f-236">An empty string is returned on error.</span></span> |
| `get_primary_headnode_number` |<span data-ttu-id="7331f-237">Ottiene hello suffisso numerico del nodo head primario hello.</span><span class="sxs-lookup"><span data-stu-id="7331f-237">Gets hello numeric suffix of hello primary headnode.</span></span> <span data-ttu-id="7331f-238">In caso di errore, viene restituita una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="7331f-238">An empty string is returned on error.</span></span> |
| `get_secondary_headnode_number` |<span data-ttu-id="7331f-239">Ottiene hello suffisso numerico del nodo head secondario hello.</span><span class="sxs-lookup"><span data-stu-id="7331f-239">Gets hello numeric suffix of hello secondary headnode.</span></span> <span data-ttu-id="7331f-240">In caso di errore, viene restituita una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="7331f-240">An empty string is returned on error.</span></span> |

## <span data-ttu-id="7331f-241"><a name="commonusage"></a>Modelli di utilizzo comuni</span><span class="sxs-lookup"><span data-stu-id="7331f-241"><a name="commonusage"></a>Common usage patterns</span></span>

<span data-ttu-id="7331f-242">Questa sezione vengono fornite informazioni aggiuntive sull'implementazione di alcuni dei modelli di utilizzo comuni hello che potrebbero essere generati durante la scrittura di script personalizzato.</span><span class="sxs-lookup"><span data-stu-id="7331f-242">This section provides guidance on implementing some of hello common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="passing-parameters-tooa-script"></a><span data-ttu-id="7331f-243">Passaggio di parametri script tooa</span><span class="sxs-lookup"><span data-stu-id="7331f-243">Passing parameters tooa script</span></span>

<span data-ttu-id="7331f-244">In alcuni casi, lo script potrebbe richiedere l'uso di parametri.</span><span class="sxs-lookup"><span data-stu-id="7331f-244">In some cases, your script may require parameters.</span></span> <span data-ttu-id="7331f-245">Ad esempio, potrebbe essere la password di amministratore di hello per cluster hello quando si utilizza l'API REST Ambari hello.</span><span class="sxs-lookup"><span data-stu-id="7331f-245">For example, you may need hello admin password for hello cluster when using hello Ambari REST API.</span></span>

<span data-ttu-id="7331f-246">I parametri passati toohello script sono note come *parametri posizionali*e sono assegnati troppo`$1` per primo parametro hello, `$2` per hello secondo e pertanto-on.</span><span class="sxs-lookup"><span data-stu-id="7331f-246">Parameters passed toohello script are known as *positional parameters*, and are assigned too`$1` for hello first parameter, `$2` for hello second, and so-on.</span></span> <span data-ttu-id="7331f-247">`$0`contiene il nome di hello dello script hello stesso.</span><span class="sxs-lookup"><span data-stu-id="7331f-247">`$0` contains hello name of hello script itself.</span></span>

<span data-ttu-id="7331f-248">Valori passati toohello script come parametri devono essere racchiusi tra virgolette singole (').</span><span class="sxs-lookup"><span data-stu-id="7331f-248">Values passed toohello script as parameters should be enclosed by single quotes (').</span></span> <span data-ttu-id="7331f-249">In modo da garantire che hello passato valore viene considerato come un valore letterale.</span><span class="sxs-lookup"><span data-stu-id="7331f-249">Doing so ensures that hello passed value is treated as a literal.</span></span>

### <a name="setting-environment-variables"></a><span data-ttu-id="7331f-250">Impostazioni delle variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="7331f-250">Setting environment variables</span></span>

<span data-ttu-id="7331f-251">L'impostazione di una variabile di ambiente viene eseguita dall'istruzione hello:</span><span class="sxs-lookup"><span data-stu-id="7331f-251">Setting an environment variable is performed by hello following statement:</span></span>

    VARIABLENAME=value

<span data-ttu-id="7331f-252">Dove nomevariabile è il nome di hello della variabile hello.</span><span class="sxs-lookup"><span data-stu-id="7331f-252">Where VARIABLENAME is hello name of hello variable.</span></span> <span data-ttu-id="7331f-253">uso delle variabili, hello tooaccess `$VARIABLENAME`.</span><span class="sxs-lookup"><span data-stu-id="7331f-253">tooaccess hello variable, use `$VARIABLENAME`.</span></span> <span data-ttu-id="7331f-254">Ad esempio, tooassign un valore fornito da un parametro posizionale come una variabile di ambiente denominata PASSWORD, si utilizzerebbe hello seguente istruzione:</span><span class="sxs-lookup"><span data-stu-id="7331f-254">For example, tooassign a value provided by a positional parameter as an environment variable named PASSWORD, you would use hello following statement:</span></span>

    PASSWORD=$1

<span data-ttu-id="7331f-255">Quindi è possibile utilizzare le informazioni di accesso successivo toohello `$PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="7331f-255">Subsequent access toohello information could then use `$PASSWORD`.</span></span>

<span data-ttu-id="7331f-256">Variabili di ambiente impostate all'interno dello script hello esistono solo nell'ambito di hello dello script hello.</span><span class="sxs-lookup"><span data-stu-id="7331f-256">Environment variables set within hello script only exist within hello scope of hello script.</span></span> <span data-ttu-id="7331f-257">In alcuni casi, potrebbe essere variabili di ambiente a livello di sistema tooadd che rimarrà termine script hello.</span><span class="sxs-lookup"><span data-stu-id="7331f-257">In some cases, you may need tooadd system-wide environment variables that will persist after hello script has finished.</span></span> <span data-ttu-id="7331f-258">variabili di ambiente a livello di sistema tooadd, aggiungere la variabile hello troppo`/etc/environment`.</span><span class="sxs-lookup"><span data-stu-id="7331f-258">tooadd system-wide environment variables, add hello variable too`/etc/environment`.</span></span> <span data-ttu-id="7331f-259">Ad esempio, hello istruzione aggiunge `HADOOP_CONF_DIR`:</span><span class="sxs-lookup"><span data-stu-id="7331f-259">For example, hello following statement adds `HADOOP_CONF_DIR`:</span></span>

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a><span data-ttu-id="7331f-260">Accesso toolocations in cui sono archiviati gli script personalizzati hello</span><span class="sxs-lookup"><span data-stu-id="7331f-260">Access toolocations where hello custom scripts are stored</span></span>

<span data-ttu-id="7331f-261">Script utilizzati toocustomize un cluster deve toobe archiviati in una delle posizioni seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="7331f-261">Scripts used toocustomize a cluster needs toobe stored in one of hello following locations:</span></span>

* <span data-ttu-id="7331f-262">Un __account di archiviazione Azure__ associato al cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7331f-262">An __Azure Storage account__ that is associated with hello cluster.</span></span>

* <span data-ttu-id="7331f-263">Un __account di archiviazione aggiuntivo__ associato hello cluster.</span><span class="sxs-lookup"><span data-stu-id="7331f-263">An __additional storage account__ associated with hello cluster.</span></span>

* <span data-ttu-id="7331f-264">__URI leggibile pubblicamente__,</span><span class="sxs-lookup"><span data-stu-id="7331f-264">A __publicly readable URI__.</span></span> <span data-ttu-id="7331f-265">Ad esempio, un URL toodata archiviato in OneDrive, Dropbox o altri file di servizio di hosting.</span><span class="sxs-lookup"><span data-stu-id="7331f-265">For example, a URL toodata stored on OneDrive, Dropbox, or other file hosting service.</span></span>

* <span data-ttu-id="7331f-266">Un __account archivio Azure Data Lake__ associato al cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="7331f-266">An __Azure Data Lake Store account__ that is associated with hello HDInsight cluster.</span></span> <span data-ttu-id="7331f-267">Per altre informazioni sull'uso di Azure Data Lake Store con HDInsight, vedere [Creare un cluster HDInsight con Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7331f-267">For more information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="7331f-268">Hello servizio principale HDInsight utilizza tooaccess archivio Data Lake deve avere accesso in lettura toohello script.</span><span class="sxs-lookup"><span data-stu-id="7331f-268">hello service principal HDInsight uses tooaccess Data Lake Store must have read access toohello script.</span></span>

<span data-ttu-id="7331f-269">Le risorse utilizzate dallo script hello devono essere disponibile pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="7331f-269">Resources used by hello script must also be publicly available.</span></span>

<span data-ttu-id="7331f-270">Archiviazione dei file hello in un account di archiviazione di Azure o l'archivio Azure Data Lake fornisce accesso veloce, sia all'interno di hello rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="7331f-270">Storing hello files in an Azure Storage account or Azure Data Lake Store provides fast access, as both within hello Azure network.</span></span>

> [!NOTE]
> <span data-ttu-id="7331f-271">Hello URI formato utilizzato tooreference hello script varia a seconda del servizio hello in uso.</span><span class="sxs-lookup"><span data-stu-id="7331f-271">hello URI format used tooreference hello script differs depending on hello service being used.</span></span> <span data-ttu-id="7331f-272">Per gli account di archiviazione associati al cluster HDInsight hello, utilizzare `wasb://` o `wasbs://`.</span><span class="sxs-lookup"><span data-stu-id="7331f-272">For storage accounts associated with hello HDInsight cluster, use `wasb://` or `wasbs://`.</span></span> <span data-ttu-id="7331f-273">Per gli URI leggibili pubblicamente, usare `http://` o `https://`.</span><span class="sxs-lookup"><span data-stu-id="7331f-273">For publicly readable URIs, use `http://` or `https://`.</span></span> <span data-ttu-id="7331f-274">Per Data Lake Store, usare `adl://`.</span><span class="sxs-lookup"><span data-stu-id="7331f-274">For Data Lake Store, use `adl://`.</span></span>

### <a name="checking-hello-operating-system-version"></a><span data-ttu-id="7331f-275">Controllo della versione del sistema operativo hello</span><span class="sxs-lookup"><span data-stu-id="7331f-275">Checking hello operating system version</span></span>

<span data-ttu-id="7331f-276">Le diverse versioni di HDInsight si basano su versioni specifiche di Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="7331f-276">Different versions of HDInsight rely on specific versions of Ubuntu.</span></span> <span data-ttu-id="7331f-277">Ci possono essere differenze tra le versioni del sistema operativo che è necessario verificare nello script.</span><span class="sxs-lookup"><span data-stu-id="7331f-277">There may be differences between OS versions that you must check for in your script.</span></span> <span data-ttu-id="7331f-278">Ad esempio, potrebbe essere necessario un file binario che è toohello legati versione Ubuntu tooinstall.</span><span class="sxs-lookup"><span data-stu-id="7331f-278">For example, you may need tooinstall a binary that is tied toohello version of Ubuntu.</span></span>

<span data-ttu-id="7331f-279">versione del sistema operativo hello toocheck, utilizzare `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="7331f-279">toocheck hello OS version, use `lsb_release`.</span></span> <span data-ttu-id="7331f-280">Ad esempio, hello lo script seguente viene illustrato come tooreference un specifico tar file a seconda della versione del sistema operativo hello:</span><span class="sxs-lookup"><span data-stu-id="7331f-280">For example, hello following script demonstrates how tooreference a specific tar file depending on hello OS version:</span></span>

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

## <span data-ttu-id="7331f-281"><a name="deployScript"></a>Elenco di controllo per la distribuzione di un'azione script</span><span class="sxs-lookup"><span data-stu-id="7331f-281"><a name="deployScript"></a>Checklist for deploying a script action</span></span>

<span data-ttu-id="7331f-282">Ecco i passaggi di hello effettuati durante la preparazione di questi script toodeploy:</span><span class="sxs-lookup"><span data-stu-id="7331f-282">Here are hello steps we took when preparing toodeploy these scripts:</span></span>

* <span data-ttu-id="7331f-283">Inserire i file hello che contengono gli script personalizzati hello in una posizione accessibile dai nodi di cluster hello durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="7331f-283">Put hello files that contain hello custom scripts in a place that is accessible by hello cluster nodes during deployment.</span></span> <span data-ttu-id="7331f-284">Ad esempio, hello archivio predefinito per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7331f-284">For example, hello default storage for hello cluster.</span></span> <span data-ttu-id="7331f-285">I file possono essere archiviati anche in servizi di hosting leggibili pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="7331f-285">Files can also be stored in publicly readable hosting services.</span></span>
* <span data-ttu-id="7331f-286">Verificare che sia impotent script hello.</span><span class="sxs-lookup"><span data-stu-id="7331f-286">Verify that hello script is impotent.</span></span> <span data-ttu-id="7331f-287">In questo modo possono hello script toobe eseguita più volte su hello stesso nodo.</span><span class="sxs-lookup"><span data-stu-id="7331f-287">Doing so allows hello script toobe executed multiple times on hello same node.</span></span>
* <span data-ttu-id="7331f-288">Utilizzare hello di tookeep un file temporaneo directory /tmp scaricato i file utilizzati dagli script hello e quindi li elimina dopo aver eseguito gli script.</span><span class="sxs-lookup"><span data-stu-id="7331f-288">Use a temporary file directory /tmp tookeep hello downloaded files used by hello scripts and then clean them up after scripts have executed.</span></span>
* <span data-ttu-id="7331f-289">Se vengono modificati le impostazioni a livello del sistema operativo o i file di configurazione del servizio di Hadoop, è consigliabile toorestart HDInsight servizi.</span><span class="sxs-lookup"><span data-stu-id="7331f-289">If OS-level settings or Hadoop service configuration files are changed, you may want toorestart HDInsight services.</span></span>

## <span data-ttu-id="7331f-290"><a name="runScriptAction"></a>Come toorun un'azione di script</span><span class="sxs-lookup"><span data-stu-id="7331f-290"><a name="runScriptAction"></a>How toorun a script action</span></span>

<span data-ttu-id="7331f-291">È possibile utilizzare script azioni toocustomize dei cluster HDInsight con hello dei seguenti metodi:</span><span class="sxs-lookup"><span data-stu-id="7331f-291">You can use script actions toocustomize HDInsight clusters using hello following methods:</span></span>

* <span data-ttu-id="7331f-292">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7331f-292">Azure portal</span></span>
* <span data-ttu-id="7331f-293">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7331f-293">Azure PowerShell</span></span>
* <span data-ttu-id="7331f-294">Modelli di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="7331f-294">Azure Resource Manager templates</span></span>
* <span data-ttu-id="7331f-295">Hello HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="7331f-295">hello HDInsight .NET SDK.</span></span>

<span data-ttu-id="7331f-296">Per ulteriori informazioni sull'utilizzo di ogni metodo, vedere [come toouse script azione](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7331f-296">For more information on using each method, see [How toouse script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="7331f-297"><a name="sampleScripts"></a>Esempi di script personalizzati</span><span class="sxs-lookup"><span data-stu-id="7331f-297"><a name="sampleScripts"></a>Custom script samples</span></span>

<span data-ttu-id="7331f-298">Microsoft fornisce gli script di esempio tooinstall componenti in un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7331f-298">Microsoft provides sample scripts tooinstall components on an HDInsight cluster.</span></span> <span data-ttu-id="7331f-299">Vedere i seguenti collegamenti per ulteriori azioni di script di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="7331f-299">See hello following links for more example script actions.</span></span>

* [<span data-ttu-id="7331f-300">Installare e usare Hue nei cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7331f-300">Install and use Hue on HDInsight clusters</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="7331f-301">Installare e usare Solr nei cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="7331f-301">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="7331f-302">Installare e usare Giraph nei cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="7331f-302">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="7331f-303">Installare o aggiornare Mono nei cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="7331f-303">Install or upgrade Mono on HDInsight clusters</span></span>](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a><span data-ttu-id="7331f-304">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="7331f-304">Troubleshooting</span></span>

<span data-ttu-id="7331f-305">di seguito Hello sono errori che possono verificarsi quando si usano script che è stato sviluppato.</span><span class="sxs-lookup"><span data-stu-id="7331f-305">hello following are errors you may encounter when using scripts you have developed:</span></span>

<span data-ttu-id="7331f-306">**Errore**: `$'\r': command not found`.</span><span class="sxs-lookup"><span data-stu-id="7331f-306">**Error**: `$'\r': command not found`.</span></span> <span data-ttu-id="7331f-307">A volte seguito da `syntax error: unexpected end of file`.</span><span class="sxs-lookup"><span data-stu-id="7331f-307">Sometimes followed by `syntax error: unexpected end of file`.</span></span>

<span data-ttu-id="7331f-308">*Causa*: questo errore si verifica quando le righe di hello in uno script di terminano con CR/LF.</span><span class="sxs-lookup"><span data-stu-id="7331f-308">*Cause*: This error is caused when hello lines in a script end with CRLF.</span></span> <span data-ttu-id="7331f-309">Sistemi UNIX prevedono solo LF come terminazione di riga hello.</span><span class="sxs-lookup"><span data-stu-id="7331f-309">Unix systems expect only LF as hello line ending.</span></span>

<span data-ttu-id="7331f-310">Questo problema più si verifica spesso quando è stato creato in un ambiente Windows script hello CRLF è una linea comune che termina per molti editor di testo in Windows.</span><span class="sxs-lookup"><span data-stu-id="7331f-310">This problem most often occurs when hello script is authored on a Windows environment, as CRLF is a common line ending for many text editors on Windows.</span></span>

<span data-ttu-id="7331f-311">*Risoluzione*: se è un'opzione nell'editor di testo, selezionare il formato Unix o LF per terminazioni di riga hello.</span><span class="sxs-lookup"><span data-stu-id="7331f-311">*Resolution*: If it is an option in your text editor, select Unix format or LF for hello line ending.</span></span> <span data-ttu-id="7331f-312">È inoltre possibile utilizzare i seguenti comandi in un tooan CRLF Unix system toochange hello LF hello:</span><span class="sxs-lookup"><span data-stu-id="7331f-312">You may also use hello following commands on a Unix system toochange hello CRLF tooan LF:</span></span>

> [!NOTE]
> <span data-ttu-id="7331f-313">Hello comandi riportati di seguito sono quasi equivalenti che deve essere cambiata tooLF terminazioni riga CRLF di hello.</span><span class="sxs-lookup"><span data-stu-id="7331f-313">hello following commands are roughly equivalent in that they should change hello CRLF line endings tooLF.</span></span> <span data-ttu-id="7331f-314">Selezionare una basata sull'utilità hello disponibili nel sistema.</span><span class="sxs-lookup"><span data-stu-id="7331f-314">Select one based on hello utilities available on your system.</span></span>

| <span data-ttu-id="7331f-315">Comando</span><span class="sxs-lookup"><span data-stu-id="7331f-315">Command</span></span> | <span data-ttu-id="7331f-316">Note</span><span class="sxs-lookup"><span data-stu-id="7331f-316">Notes</span></span> |
| --- | --- |
| `unix2dos -b INFILE` |<span data-ttu-id="7331f-317">il file originale di Hello viene eseguito il backup con una. Estensione BAK</span><span class="sxs-lookup"><span data-stu-id="7331f-317">hello original file is backed up with a .BAK extension</span></span> |
| `tr -d '\r' < INFILE > OUTFILE` |<span data-ttu-id="7331f-318">OUTFILE contiene una versione solo con le terminazioni LF</span><span class="sxs-lookup"><span data-stu-id="7331f-318">OUTFILE contains a version with only LF endings</span></span> |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | <span data-ttu-id="7331f-319">Modifica direttamente il file hello</span><span class="sxs-lookup"><span data-stu-id="7331f-319">Modifies hello file directly</span></span> |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |<span data-ttu-id="7331f-320">OUTFILE contiene una versione solo con le terminazioni LF.</span><span class="sxs-lookup"><span data-stu-id="7331f-320">OUTFILE contains a version with only LF endings.</span></span> |

<span data-ttu-id="7331f-321">**Errore**: `line 1: #!/usr/bin/env: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="7331f-321">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span></span>

<span data-ttu-id="7331f-322">*Causa*: questo errore si verifica quando hello script è stato salvato come UTF-8 con un provider di servizi Internet (BOM, Byte Order Mark).</span><span class="sxs-lookup"><span data-stu-id="7331f-322">*Cause*: This error occurs when hello script was saved as UTF-8 with a Byte Order Mark (BOM).</span></span>

<span data-ttu-id="7331f-323">*Risoluzione*: Save hello file come ASCII, oppure come UTF-8 senza una distinta base.</span><span class="sxs-lookup"><span data-stu-id="7331f-323">*Resolution*: Save hello file either as ASCII, or as UTF-8 without a BOM.</span></span> <span data-ttu-id="7331f-324">È inoltre possibile utilizzare hello comando seguente in un toocreate sistema un file senza hello DBA Linux o Unix:</span><span class="sxs-lookup"><span data-stu-id="7331f-324">You may also use hello following command on a Linux or Unix system toocreate a file without hello BOM:</span></span>

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

<span data-ttu-id="7331f-325">Sostituire `INFILE` con file hello contenente hello DBA.</span><span class="sxs-lookup"><span data-stu-id="7331f-325">Replace `INFILE` with hello file containing hello BOM.</span></span> <span data-ttu-id="7331f-326">`OUTFILE`deve essere un nuovo nome di file, che contiene lo script hello senza hello DBA.</span><span class="sxs-lookup"><span data-stu-id="7331f-326">`OUTFILE` should be a new file name, which contains hello script without hello BOM.</span></span>

## <span data-ttu-id="7331f-327"><a name="seeAlso"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7331f-327"><a name="seeAlso"></a>Next steps</span></span>

* <span data-ttu-id="7331f-328">Informazioni su come troppo[personalizzare HDInsight cluster mediante l'azione di script](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="7331f-328">Learn how too[Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
* <span data-ttu-id="7331f-329">Hello utilizzare [riferimento HDInsight .NET SDK](https://msdn.microsoft.com/library/mt271028.aspx) toolearn ulteriori informazioni sulla creazione di applicazioni .NET che gestire HDInsight</span><span class="sxs-lookup"><span data-stu-id="7331f-329">Use hello [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx) toolearn more about creating .NET applications that manage HDInsight</span></span>
* <span data-ttu-id="7331f-330">Hello utilizzare [API REST di HDInsight](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn come cluster di azioni di gestione di toouse REST tooperform in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7331f-330">Use hello [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn how toouse REST tooperform management actions on HDInsight clusters.</span></span>
