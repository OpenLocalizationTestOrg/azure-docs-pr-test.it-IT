---
title: aaaApache Storm scrivere tooStorage/Data Lake Store - HDInsight di Azure | Documenti Microsoft
description: "Informazioni su come toouse hello archiviazione toohello HDFS compatibile di Apache Storm toowrite per HDInsight. Archiviazione Azure o archivio Azure Data Lake fornire archiviazione hello HDFS comptabile per HDInsight. Questo documento e hello associato esempio illustrano come componente HdfsBolt hello può essere utilizzati toowrite toohello predefinito archiviazione di un elevato numero di cluster HDInsight."
services: hdinsight
documentationcenter: na
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 1df98653-a6c8-4662-a8c6-5d288fc4f3a6
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: d76159a9ecd1be18e519511cfdb3bcfd18ae4d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="write-toohdfs-from-apache-storm-on-hdinsight"></a><span data-ttu-id="af025-105">Scrivere tooHDFS da Apache Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="af025-105">Write tooHDFS from Apache Storm on HDInsight</span></span>

<span data-ttu-id="af025-106">Informazioni sull'utilizzo toouse Storm toowrite dati toohello archiviazione HDFS compatibile da Apache Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="af025-106">Learn how toouse Storm toowrite data toohello HDFS-compatible storage used by Apache Storm on HDInsight.</span></span> <span data-ttu-id="af025-107">HDInsight può usare sia Archiviazione di Azure che Azure Data Lake Store come archivio compatibile con HDFS.</span><span class="sxs-lookup"><span data-stu-id="af025-107">HDInsight can use both Azure Storage and Azure Data Lake store as HDFS-comptabile storage.</span></span> <span data-ttu-id="af025-108">Storm fornisce un [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) componente che scrive dati tooHDFS.</span><span class="sxs-lookup"><span data-stu-id="af025-108">Storm provides an [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component that writes data tooHDFS.</span></span> <span data-ttu-id="af025-109">Questo documento vengono fornite informazioni sulla scrittura di tipo tooeither di archiviazione da hello HdfsBolt.</span><span class="sxs-lookup"><span data-stu-id="af025-109">This document provides information on writing tooeither type of storage from hello HdfsBolt.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="af025-110">esempio Hello topologia utilizzata in questo documento si basa sui componenti inclusi in Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="af025-110">hello example topology used in this document relies on components that are included with Storm on HDInsight.</span></span> <span data-ttu-id="af025-111">Potrebbe essere necessario toowork modifica con l'archivio Azure Data Lake se utilizzato con altri cluster Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="af025-111">It may require modification toowork with Azure Data Lake Store when used with other Apache Storm clusters.</span></span>

## <a name="get-hello-code"></a><span data-ttu-id="af025-112">Ottenere il codice hello</span><span class="sxs-lookup"><span data-stu-id="af025-112">Get hello code</span></span>

<span data-ttu-id="af025-113">è disponibile come download dal progetto Hello contenente questa topologia [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="af025-113">hello project containing this topology is available as a download from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span></span>

<span data-ttu-id="af025-114">toocompile questo progetto, è necessario hello seguente configurazione per l'ambiente di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="af025-114">toocompile this project, you need hello following configuration for your development environment:</span></span>

* <span data-ttu-id="af025-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="af025-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="af025-116">Per HDInsight 3.5 o una versione successiva è necessario Java 8.</span><span class="sxs-lookup"><span data-stu-id="af025-116">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="af025-117">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="af025-117">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

<span data-ttu-id="af025-118">Hello seguenti variabili di ambiente possono essere impostate durante l'installazione di Java e hello JDK nella workstation di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="af025-118">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="af025-119">Tuttavia, è necessario verificare che esistano e che contengono i valori corretti di hello per il sistema.</span><span class="sxs-lookup"><span data-stu-id="af025-119">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="af025-120">`JAVA_HOME`-deve puntare toohello directory in cui hello JDK è installato.</span><span class="sxs-lookup"><span data-stu-id="af025-120">`JAVA_HOME` - should point toohello directory where hello JDK is installed.</span></span>
* <span data-ttu-id="af025-121">`PATH`-deve contenere hello seguenti percorsi:</span><span class="sxs-lookup"><span data-stu-id="af025-121">`PATH` - should contain hello following paths:</span></span>
  
    * <span data-ttu-id="af025-122">`JAVA_HOME`(o percorso equivalente hello).</span><span class="sxs-lookup"><span data-stu-id="af025-122">`JAVA_HOME` (or hello equivalent path).</span></span>
    * <span data-ttu-id="af025-123">`JAVA_HOME\bin`(o percorso equivalente hello).</span><span class="sxs-lookup"><span data-stu-id="af025-123">`JAVA_HOME\bin` (or hello equivalent path).</span></span>
    * <span data-ttu-id="af025-124">directory di Hello in cui è installato Maven.</span><span class="sxs-lookup"><span data-stu-id="af025-124">hello directory where Maven is installed.</span></span>

## <a name="how-toouse-hello-hdfsbolt-with-hdinsight"></a><span data-ttu-id="af025-125">Come toouse hello HdfsBolt con HDInsight</span><span class="sxs-lookup"><span data-stu-id="af025-125">How toouse hello HdfsBolt with HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af025-126">Prima di utilizzare hello HdfsBolt con Storm in HDInsight, è innanzitutto necessario utilizzare un file jar di script azione toocopy necessarie in hello `extpath` per Storm.</span><span class="sxs-lookup"><span data-stu-id="af025-126">Before using hello HdfsBolt with Storm on HDInsight, you must first use a script action toocopy required jar files into hello `extpath` for Storm.</span></span> <span data-ttu-id="af025-127">Per ulteriori informazioni, vedere hello [cluster hello configura](#configure) sezione.</span><span class="sxs-lookup"><span data-stu-id="af025-127">For more information, see hello [Configure hello cluster](#configure) section.</span></span>

<span data-ttu-id="af025-128">Hello HdfsBolt utilizza lo schema di file hello fornire toounderstand modalità toowrite tooHDFS.</span><span class="sxs-lookup"><span data-stu-id="af025-128">hello HdfsBolt uses hello file scheme that you provide toounderstand how toowrite tooHDFS.</span></span> <span data-ttu-id="af025-129">Con HDInsight, utilizzare uno dei seguenti schemi hello:</span><span class="sxs-lookup"><span data-stu-id="af025-129">With HDInsight, use one of hello following schemes:</span></span>

* <span data-ttu-id="af025-130">`wasb://`: usato con l'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="af025-130">`wasb://`: Used with an Azure Storage account.</span></span>
* <span data-ttu-id="af025-131">`adl://`: usato con Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="af025-131">`adl://`: Used with Azure Data Lake Store.</span></span>

<span data-ttu-id="af025-132">Hello nella tabella seguente vengono forniti esempi dell'utilizzo dello schema di file hello per scenari diversi:</span><span class="sxs-lookup"><span data-stu-id="af025-132">hello following table provides examples of using hello file scheme for different scenarios:</span></span>

| <span data-ttu-id="af025-133">Schema</span><span class="sxs-lookup"><span data-stu-id="af025-133">Scheme</span></span> | <span data-ttu-id="af025-134">Note</span><span class="sxs-lookup"><span data-stu-id="af025-134">Notes</span></span> |
| ----- | ----- |
| `wasb:///` | <span data-ttu-id="af025-135">account di archiviazione predefinito Hello è un contenitore blob in un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="af025-135">hello default storage account is a blob container in an Azure Storage account</span></span> |
| `adl:///` | <span data-ttu-id="af025-136">account di archiviazione predefinito Hello è una directory nell'archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="af025-136">hello default storage account is a directory in Azure Data Lake Store.</span></span> <span data-ttu-id="af025-137">Durante la creazione del cluster, specificare la directory hello in archivio Data Lake che sarà radice hello HDFS del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="af025-137">During cluster creation, you specify hello directory in Data Lake Store that is hello root of hello cluster's HDFS.</span></span> <span data-ttu-id="af025-138">Ad esempio, hello `/clusters/myclustername/` directory.</span><span class="sxs-lookup"><span data-stu-id="af025-138">For example, hello `/clusters/myclustername/` directory.</span></span> |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | <span data-ttu-id="af025-139">Un account di archiviazione di Azure (aggiuntive) non predefinito associato hello cluster.</span><span class="sxs-lookup"><span data-stu-id="af025-139">A non-default (additional) Azure storage account associated with hello cluster.</span></span> |
| `adl://STORENAME/` | <span data-ttu-id="af025-140">radice Hello hello archivio Data Lake usati dal cluster hello.</span><span class="sxs-lookup"><span data-stu-id="af025-140">hello root of hello Data Lake Store used by hello cluster.</span></span> <span data-ttu-id="af025-141">Questo schema consente tooaccess dati che si trovano all'esterno della directory contenente il sistema di hello cluster file hello.</span><span class="sxs-lookup"><span data-stu-id="af025-141">This scheme allows you tooaccess data that is located outside hello directory that contains hello cluster file system.</span></span> |

<span data-ttu-id="af025-142">Per ulteriori informazioni, vedere hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) riferimento all'indirizzo Apache.org.</span><span class="sxs-lookup"><span data-stu-id="af025-142">For more information, see hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) reference at Apache.org.</span></span>

### <a name="example-configuration"></a><span data-ttu-id="af025-143">Configurazione di esempio</span><span class="sxs-lookup"><span data-stu-id="af025-143">Example configuration</span></span>

<span data-ttu-id="af025-144">YAML seguente Hello è un estratto dal hello `resources/writetohdfs.yaml` file incluso nell'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="af025-144">hello following YAML is an excerpt from hello `resources/writetohdfs.yaml` file included in hello example.</span></span> <span data-ttu-id="af025-145">Questo file definisce topologia Storm hello utilizzando hello [flusso](https://storm.apache.org/releases/1.1.0/flux.html) framework per Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="af025-145">This file defines hello Storm topology using hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework for Apache Storm.</span></span>

```yaml
components:
  - id: "syncPolicy"
    className: "org.apache.storm.hdfs.bolt.sync.CountSyncPolicy"
    constructorArgs:
      - 1000

  - id: "rotationPolicy"
    className: "org.apache.storm.hdfs.bolt.rotation.NoRotationPolicy"

  - id: "fileNameFormat"
    className: "org.apache.storm.hdfs.bolt.format.DefaultFileNameFormat"
    configMethods:
      - name: "withPath"
        args: ["${hdfs.write.dir}"]
      - name: "withExtension"
        args: [".txt"]

  - id: "recordFormat"
    className: "org.apache.storm.hdfs.bolt.format.DelimitedRecordFormat"
    configMethods:
      - name: "withFieldDelimiter"
        args: ["|"]

# spout definitions
spouts:
  - id: "tick-spout"
    className: "com.microsoft.example.TickSpout"
    parallelism: 1


# bolt definitions
bolts:
  - id: "hdfs-bolt"
    className: "org.apache.storm.hdfs.bolt.HdfsBolt"
    configMethods:
      - name: "withConfigKey"
        args: ["hdfs.config"]
      - name: "withFsUrl"
        args: ["${hdfs.url}"]
      - name: "withFileNameFormat"
        args: [ref: "fileNameFormat"]
      - name: "withRecordFormat"
        args: [ref: "recordFormat"]
      - name: "withRotationPolicy"
        args: [ref: "rotationPolicy"]
      - name: "withSyncPolicy"
        args: [ref: "syncPolicy"]
```

<span data-ttu-id="af025-146">Questo YAML definisce hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="af025-146">This YAML defines hello following items:</span></span>

* <span data-ttu-id="af025-147">`syncPolicy`: Definisce quando i file vengono sincronizzati scaricati toohello sistema di file.</span><span class="sxs-lookup"><span data-stu-id="af025-147">`syncPolicy`: Defines when files are synched/flushed toohello file system.</span></span> <span data-ttu-id="af025-148">In questo esempio, ogni 1000 tuple.</span><span class="sxs-lookup"><span data-stu-id="af025-148">In this example, every 1000 tuples.</span></span>
* <span data-ttu-id="af025-149">`fileNameFormat`: Definisce hello percorso e il nome modello toouse durante la scrittura di file.</span><span class="sxs-lookup"><span data-stu-id="af025-149">`fileNameFormat`: Defines hello path and file name pattern toouse when writing files.</span></span> <span data-ttu-id="af025-150">In questo esempio viene specificato un percorso di hello in fase di esecuzione utilizzando un filtro e l'estensione del file hello è `.txt`.</span><span class="sxs-lookup"><span data-stu-id="af025-150">In this example, hello path is provided at runtime using a filter, and hello file extension is `.txt`.</span></span>
* <span data-ttu-id="af025-151">`recordFormat`: Definisce formato interno di hello del file hello scritti.</span><span class="sxs-lookup"><span data-stu-id="af025-151">`recordFormat`: Defines hello internal format of hello files written.</span></span> <span data-ttu-id="af025-152">In questo esempio, i campi delimitati hello `|` carattere.</span><span class="sxs-lookup"><span data-stu-id="af025-152">In this example, fields are delimited by hello `|` character.</span></span>
* <span data-ttu-id="af025-153">`rotationPolicy`: Definisce quando toorotate file.</span><span class="sxs-lookup"><span data-stu-id="af025-153">`rotationPolicy`: Defines when toorotate files.</span></span> <span data-ttu-id="af025-154">In questo esempio, non viene eseguita alcuna rotazione.</span><span class="sxs-lookup"><span data-stu-id="af025-154">In this example, no rotation is performed.</span></span>
* <span data-ttu-id="af025-155">`hdfs-bolt`: Usa hello componenti precedenti come parametri di configurazione per hello `HdfsBolt` classe.</span><span class="sxs-lookup"><span data-stu-id="af025-155">`hdfs-bolt`: Uses hello previous components as configuration parameters for hello `HdfsBolt` class.</span></span>

<span data-ttu-id="af025-156">Per ulteriori informazioni sul framework luminoso hello, vedere [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="af025-156">For more information on hello Flux framework, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="configure-hello-cluster"></a><span data-ttu-id="af025-157">Configurare il cluster hello</span><span class="sxs-lookup"><span data-stu-id="af025-157">Configure hello cluster</span></span>

<span data-ttu-id="af025-158">Per impostazione predefinita, Storm in HDInsight non include componenti hello HdfsBolt utilizza toocommunicate con archiviazione di Azure o archivio Data Lake in classpath elevato del numero.</span><span class="sxs-lookup"><span data-stu-id="af025-158">By default, Storm on HDInsight does not include hello components that HdfsBolt uses toocommunicate with Azure Storage or Data Lake Store in Storm's classpath.</span></span> <span data-ttu-id="af025-159">Azione tooadd lo script seguente hello utilizzare toohello questi componenti `extlib` directory per Storm sul cluster:</span><span class="sxs-lookup"><span data-stu-id="af025-159">Use hello following script action tooadd these components toohello `extlib` directory for Storm on your cluster:</span></span>

<span data-ttu-id="af025-160">| Script URI | Nodi tooapply a | I parametri | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisore | None |</span><span class="sxs-lookup"><span data-stu-id="af025-160">| Script URI | Nodes tooapply it to| Parameters | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | None |</span></span>

<span data-ttu-id="af025-161">Per informazioni sull'uso di questo script con il cluster, vedere hello [HDInsight personalizzare cluster tramite le azioni script](./hdinsight-hadoop-customize-cluster-linux.md) documento.</span><span class="sxs-lookup"><span data-stu-id="af025-161">For information on using this script with your cluster, see hello [Customize HDInsight clusters using script actions](./hdinsight-hadoop-customize-cluster-linux.md) document.</span></span>

## <a name="build-and-package-hello-topology"></a><span data-ttu-id="af025-162">Compilare e assemblare topologia hello</span><span class="sxs-lookup"><span data-stu-id="af025-162">Build and package hello topology</span></span>

1. <span data-ttu-id="af025-163">Scaricare il progetto di esempio hello da [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="af025-163">Download hello example project from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour development environment.</span></span>

2. <span data-ttu-id="af025-164">Da un prompt dei comandi, terminale o una sessione della shell, modifica directory toohello radice hello scaricato progetto.</span><span class="sxs-lookup"><span data-stu-id="af025-164">From a command prompt, terminal, or shell session, change directories toohello root of hello downloaded project.</span></span> <span data-ttu-id="af025-165">toobuild e pacchetto hello topologia, usare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="af025-165">toobuild and package hello topology, use hello following command:</span></span>
   
        mvn compile package
   
    <span data-ttu-id="af025-166">Una volta completata la compilazione di hello e dei pacchetti, è una nuova directory denominata `target`, che contiene un file denominato `StormToHdfs-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="af025-166">Once hello build and packaging completes, there is a new directory named `target`, that contains a file named `StormToHdfs-1.0-SNAPSHOT.jar`.</span></span> <span data-ttu-id="af025-167">Questo file contiene la topologia hello compilato.</span><span class="sxs-lookup"><span data-stu-id="af025-167">This file contains hello compiled topology.</span></span>

## <a name="deploy-and-run-hello-topology"></a><span data-ttu-id="af025-168">Distribuire ed eseguire topologia hello</span><span class="sxs-lookup"><span data-stu-id="af025-168">Deploy and run hello topology</span></span>

1. <span data-ttu-id="af025-169">Utilizzare hello seguendo il cluster di HDInsight toohello comando toocopy hello topologia.</span><span class="sxs-lookup"><span data-stu-id="af025-169">Use hello following command toocopy hello topology toohello HDInsight cluster.</span></span> <span data-ttu-id="af025-170">Sostituire **utente** con nome utente di hello SSH utilizzato per la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="af025-170">Replace **USER** with hello SSH user name you used when creating hello cluster.</span></span> <span data-ttu-id="af025-171">Sostituire **CLUSTERNAME** con nome hello del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="af025-171">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    <span data-ttu-id="af025-172">Quando richiesto, immettere la password di hello utilizzati durante la creazione utente SSH hello per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="af025-172">When prompted, enter hello password used when creating hello SSH user for hello cluster.</span></span> <span data-ttu-id="af025-173">Se si utilizza una chiave pubblica anziché una password, potrebbe essere necessario hello toouse `-i` parametro toospecify hello percorso toohello corrispondente chiave privata.</span><span class="sxs-lookup"><span data-stu-id="af025-173">If you used a public key instead of a password, you may need toouse hello `-i` parameter toospecify hello path toohello matching private key.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="af025-174">Per altre informazioni sull'uso di `scp` con HDInsight, vedere [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md) (Uso di SSH con HDInsight).</span><span class="sxs-lookup"><span data-stu-id="af025-174">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="af025-175">Una volta completato il caricamento di hello, utilizzare hello dopo i cluster di HDInsight toohello tooconnect tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="af025-175">Once hello upload completes, use hello following tooconnect toohello HDInsight cluster using SSH.</span></span> <span data-ttu-id="af025-176">Sostituire **utente** con nome utente di hello SSH utilizzato per la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="af025-176">Replace **USER** with hello SSH user name you used when creating hello cluster.</span></span> <span data-ttu-id="af025-177">Sostituire **CLUSTERNAME** con nome hello del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="af025-177">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="af025-178">Quando richiesto, immettere la password di hello utilizzati durante la creazione utente SSH hello per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="af025-178">When prompted, enter hello password used when creating hello SSH user for hello cluster.</span></span> <span data-ttu-id="af025-179">Se si utilizza una chiave pubblica anziché una password, potrebbe essere necessario hello toouse `-i` parametro toospecify hello percorso toohello corrispondente chiave privata.</span><span class="sxs-lookup"><span data-stu-id="af025-179">If you used a public key instead of a password, you may need toouse hello `-i` parameter toospecify hello path toohello matching private key.</span></span>
   
   <span data-ttu-id="af025-180">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="af025-180">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="af025-181">Una volta connessi, utilizzare hello comando che segue toocreate un file denominato `dev.properties`:</span><span class="sxs-lookup"><span data-stu-id="af025-181">Once connected, use hello following command toocreate a file named `dev.properties`:</span></span>

        nano dev.properties

4. <span data-ttu-id="af025-182">Hello utilizzo successivo di testo come contenuto di hello di hello `dev.properties` file:</span><span class="sxs-lookup"><span data-stu-id="af025-182">Use hello following text as hello contents of hello `dev.properties` file:</span></span>

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > <span data-ttu-id="af025-183">Questo esempio si presuppone che il cluster utilizza un account di archiviazione di Azure come spazio di archiviazione predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="af025-183">This example assumes that your cluster uses an Azure Storage account as hello default storage.</span></span> <span data-ttu-id="af025-184">Se il cluster usa Azure Data Lake Store, usare invece `hdfs.url: adl:///`.</span><span class="sxs-lookup"><span data-stu-id="af025-184">If your cluster uses Azure Data Lake Store, use `hdfs.url: adl:///` instead.</span></span>
    
    <span data-ttu-id="af025-185">file hello toosave, usare __Ctrl + X__, quindi __Y__e infine __invio__.</span><span class="sxs-lookup"><span data-stu-id="af025-185">toosave hello file, use __Ctrl + X__, then __Y__, and finally __Enter__.</span></span> <span data-ttu-id="af025-186">valori Hello in questo file impostare l'URL dell'archivio Data Lake hello e nome della directory hello che vengono scritti dati.</span><span class="sxs-lookup"><span data-stu-id="af025-186">hello values in this file set hello Data Lake store URL and hello directory name that data is written to.</span></span>

3. <span data-ttu-id="af025-187">Utilizzare hello topologia hello toostart di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="af025-187">Use hello following command toostart hello topology:</span></span>
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    <span data-ttu-id="af025-188">Questo comando avvia una topologia di hello con framework luminoso hello inviandolo nodo Nimbus toohello del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="af025-188">This command starts hello topology using hello Flux framework by submitting it toohello Nimbus node of hello cluster.</span></span> <span data-ttu-id="af025-189">topologia Hello è definita da hello `writetohdfs.yaml` file incluso nel file jar hello.</span><span class="sxs-lookup"><span data-stu-id="af025-189">hello topology is defined by hello `writetohdfs.yaml` file included in hello jar.</span></span> <span data-ttu-id="af025-190">Hello `dev.properties` file viene passato come un filtro e vengono letti i valori hello contenuti nel file hello dalla topologia hello.</span><span class="sxs-lookup"><span data-stu-id="af025-190">hello `dev.properties` file is passed as a filter, and hello values contained in hello file are read by hello topology.</span></span>

## <a name="view-output-data"></a><span data-ttu-id="af025-191">Visualizzare i dati di output</span><span class="sxs-lookup"><span data-stu-id="af025-191">View output data</span></span>

<span data-ttu-id="af025-192">dati hello tooview, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="af025-192">tooview hello data, use hello following command:</span></span>

    hdfs dfs -ls /stormdata/

<span data-ttu-id="af025-193">Viene visualizzato un elenco dei file hello creati da questa topologia.</span><span class="sxs-lookup"><span data-stu-id="af025-193">A list of hello files created by this topology is displayed.</span></span>

<span data-ttu-id="af025-194">Hello elenco riportato di seguito è riportato un esempio di dati hello restituiti dai comandi precedenti hello:</span><span class="sxs-lookup"><span data-stu-id="af025-194">hello following list is an example of hello data retuned by hello previous commands:</span></span>

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-hello-topology"></a><span data-ttu-id="af025-195">Arrestare la topologia hello</span><span class="sxs-lookup"><span data-stu-id="af025-195">Stop hello topology</span></span>

<span data-ttu-id="af025-196">Topologie di Storm eseguire finché non viene interrotto o hello cluster verrà eliminato.</span><span class="sxs-lookup"><span data-stu-id="af025-196">Storm topologies run until stopped, or hello cluster is deleted.</span></span> <span data-ttu-id="af025-197">toostop hello topologia, usare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="af025-197">toostop hello topology, use hello following command:</span></span>

    storm kill hdfswriter

## <a name="delete-your-cluster"></a><span data-ttu-id="af025-198">Eliminare il cluster</span><span class="sxs-lookup"><span data-stu-id="af025-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="af025-199">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="af025-199">Next steps</span></span>

<span data-ttu-id="af025-200">Ora che si è appreso come toouse Storm toowrite tooAzure archiviazione e l'archivio Azure Data Lake, individuare altri [Storm esempi per HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="af025-200">Now that you have learned how toouse Storm toowrite tooAzure Storage and Azure Data Lake Store, discover other [Storm examples for HDInsight](hdinsight-storm-example-topology.md).</span></span>

