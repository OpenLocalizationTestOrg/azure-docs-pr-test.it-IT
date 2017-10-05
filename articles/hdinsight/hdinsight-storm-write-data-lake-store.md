---
title: Scrittura in un archivio con Apache Storm/Data Lake Store - Azure HDInsight | Microsoft Docs
description: Informazioni su come usare Apache Storm per eseguire operazioni di scrittura in un archivio compatibile con HDFS per HDInsight. Archiviazione di Azure o Azure Data Lake Store offre un'archiviazione compatibile con HDFS per HDInsight. Questo documento e il relativo esempio dimostrano come usare il componente HdfsBolt per scrivere nell'archivio predefinito di uno Storm in un cluster HDInsight.
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
ms.openlocfilehash: 10dc8789e8f4a2b27fd3a4c6fec2ab28c674170a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="write-to-hdfs-from-apache-storm-on-hdinsight"></a><span data-ttu-id="060ae-105">Scrivere da Apache Storm a HDFS in HDInsight</span><span class="sxs-lookup"><span data-stu-id="060ae-105">Write to HDFS from Apache Storm on HDInsight</span></span>

<span data-ttu-id="060ae-106">Informazioni su come usare Storm per scrivere dati in un archivio compatibile con HDFS usato da Apache Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="060ae-106">Learn how to use Storm to write data to the HDFS-compatible storage used by Apache Storm on HDInsight.</span></span> <span data-ttu-id="060ae-107">HDInsight può usare sia Archiviazione di Azure che Azure Data Lake Store come archivio compatibile con HDFS.</span><span class="sxs-lookup"><span data-stu-id="060ae-107">HDInsight can use both Azure Storage and Azure Data Lake store as HDFS-comptabile storage.</span></span> <span data-ttu-id="060ae-108">Storm offre un componente [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) che scrive i dati in HDFS.</span><span class="sxs-lookup"><span data-stu-id="060ae-108">Storm provides an [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component that writes data to HDFS.</span></span> <span data-ttu-id="060ae-109">Questo documento contiene informazioni su come eseguire operazioni di scrittura da HdfsBolt in entrambi gli archivi.</span><span class="sxs-lookup"><span data-stu-id="060ae-109">This document provides information on writing to either type of storage from the HdfsBolt.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="060ae-110">La topologia di esempio usata in questo documento si basa su componenti inclusi con Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="060ae-110">The example topology used in this document relies on components that are included with Storm on HDInsight.</span></span> <span data-ttu-id="060ae-111">Può essere necessario apportare delle modifiche per usare Azure Data Lake Store con altri cluster Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="060ae-111">It may require modification to work with Azure Data Lake Store when used with other Apache Storm clusters.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="060ae-112">Ottenere il codice</span><span class="sxs-lookup"><span data-stu-id="060ae-112">Get the code</span></span>

<span data-ttu-id="060ae-113">Il progetto contenente questa topologia è disponibile per il download da [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="060ae-113">The project containing this topology is available as a download from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span></span>

<span data-ttu-id="060ae-114">Per compilare questo progetto, è necessaria la seguente configurazione per l'ambiente di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="060ae-114">To compile this project, you need the following configuration for your development environment:</span></span>

* <span data-ttu-id="060ae-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="060ae-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="060ae-116">Per HDInsight 3.5 o una versione successiva è necessario Java 8.</span><span class="sxs-lookup"><span data-stu-id="060ae-116">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="060ae-117">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="060ae-117">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

<span data-ttu-id="060ae-118">Le variabili di ambiente seguenti possono essere impostate quando si installa Java e l'JDK nella workstation di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="060ae-118">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="060ae-119">È tuttavia necessario verificare che esistano e che contengano i valori corretti per il sistema in uso.</span><span class="sxs-lookup"><span data-stu-id="060ae-119">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="060ae-120">`JAVA_HOME` - deve puntare alla directory dove è installato JDK.</span><span class="sxs-lookup"><span data-stu-id="060ae-120">`JAVA_HOME` - should point to the directory where the JDK is installed.</span></span>
* <span data-ttu-id="060ae-121">`PATH`: deve contenere i percorsi seguenti:</span><span class="sxs-lookup"><span data-stu-id="060ae-121">`PATH` - should contain the following paths:</span></span>
  
    * <span data-ttu-id="060ae-122">`JAVA_HOME` o il percorso equivalente.</span><span class="sxs-lookup"><span data-stu-id="060ae-122">`JAVA_HOME` (or the equivalent path).</span></span>
    * <span data-ttu-id="060ae-123">`JAVA_HOME\bin` o il percorso equivalente.</span><span class="sxs-lookup"><span data-stu-id="060ae-123">`JAVA_HOME\bin` (or the equivalent path).</span></span>
    * <span data-ttu-id="060ae-124">Directory in cui è installato Maven.</span><span class="sxs-lookup"><span data-stu-id="060ae-124">The directory where Maven is installed.</span></span>

## <a name="how-to-use-the-hdfsbolt-with-hdinsight"></a><span data-ttu-id="060ae-125">Procedura per usare HdfsBolt con HDInsight</span><span class="sxs-lookup"><span data-stu-id="060ae-125">How to use the HdfsBolt with HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="060ae-126">Prima di usare HdfsBolt con Storm in HDInsight, è necessario usare l'azione script per copiare i file .jar richiesti in `extpath` per Storm.</span><span class="sxs-lookup"><span data-stu-id="060ae-126">Before using the HdfsBolt with Storm on HDInsight, you must first use a script action to copy required jar files into the `extpath` for Storm.</span></span> <span data-ttu-id="060ae-127">Per altre informazioni, vedere la sezione [Configurare il cluster](#configure).</span><span class="sxs-lookup"><span data-stu-id="060ae-127">For more information, see the [Configure the cluster](#configure) section.</span></span>

<span data-ttu-id="060ae-128">HdfsBolt usa lo schema file specificato dall'utente per capire come scrivere in HDFS.</span><span class="sxs-lookup"><span data-stu-id="060ae-128">The HdfsBolt uses the file scheme that you provide to understand how to write to HDFS.</span></span> <span data-ttu-id="060ae-129">Per HDInsight, usare uno dei seguenti schemi:</span><span class="sxs-lookup"><span data-stu-id="060ae-129">With HDInsight, use one of the following schemes:</span></span>

* <span data-ttu-id="060ae-130">`wasb://`: usato con l'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="060ae-130">`wasb://`: Used with an Azure Storage account.</span></span>
* <span data-ttu-id="060ae-131">`adl://`: usato con Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="060ae-131">`adl://`: Used with Azure Data Lake Store.</span></span>

<span data-ttu-id="060ae-132">La seguente tabella riporta esempi di utilizzo dello schema di file in diversi scenari:</span><span class="sxs-lookup"><span data-stu-id="060ae-132">The following table provides examples of using the file scheme for different scenarios:</span></span>

| <span data-ttu-id="060ae-133">Schema</span><span class="sxs-lookup"><span data-stu-id="060ae-133">Scheme</span></span> | <span data-ttu-id="060ae-134">Note</span><span class="sxs-lookup"><span data-stu-id="060ae-134">Notes</span></span> |
| ----- | ----- |
| `wasb:///` | <span data-ttu-id="060ae-135">L'account di archiviazione predefinito è un contenitore BLOB nell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="060ae-135">The default storage account is a blob container in an Azure Storage account</span></span> |
| `adl:///` | <span data-ttu-id="060ae-136">L'account di archiviazione predefinito è una directory in Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="060ae-136">The default storage account is a directory in Azure Data Lake Store.</span></span> <span data-ttu-id="060ae-137">Durante la creazione del cluster, si specifica la directory in Data Lake Store che rappresenta la radice dell'HDFS del cluster.</span><span class="sxs-lookup"><span data-stu-id="060ae-137">During cluster creation, you specify the directory in Data Lake Store that is the root of the cluster's HDFS.</span></span> <span data-ttu-id="060ae-138">Ad esempio, la directory `/clusters/myclustername/`.</span><span class="sxs-lookup"><span data-stu-id="060ae-138">For example, the `/clusters/myclustername/` directory.</span></span> |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | <span data-ttu-id="060ae-139">Un account di archiviazione di Azure non predefinito (aggiuntivo) associato al cluster.</span><span class="sxs-lookup"><span data-stu-id="060ae-139">A non-default (additional) Azure storage account associated with the cluster.</span></span> |
| `adl://STORENAME/` | <span data-ttu-id="060ae-140">La radice di Data Lake Store usata dal cluster.</span><span class="sxs-lookup"><span data-stu-id="060ae-140">The root of the Data Lake Store used by the cluster.</span></span> <span data-ttu-id="060ae-141">Questo schema permette di accedere ai dati situati all'esterno della directory che contiene il file system del cluster.</span><span class="sxs-lookup"><span data-stu-id="060ae-141">This scheme allows you to access data that is located outside the directory that contains the cluster file system.</span></span> |

<span data-ttu-id="060ae-142">Per altre informazioni, vedere il riferimento [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) su Apache.org.</span><span class="sxs-lookup"><span data-stu-id="060ae-142">For more information, see the [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) reference at Apache.org.</span></span>

### <a name="example-configuration"></a><span data-ttu-id="060ae-143">Configurazione di esempio</span><span class="sxs-lookup"><span data-stu-id="060ae-143">Example configuration</span></span>

<span data-ttu-id="060ae-144">Il seguente YAML è un estratto del file `resources/writetohdfs.yaml` incluso nell'esempio.</span><span class="sxs-lookup"><span data-stu-id="060ae-144">The following YAML is an excerpt from the `resources/writetohdfs.yaml` file included in the example.</span></span> <span data-ttu-id="060ae-145">Questo file definisce la topologia di Storm usando il framework [Flux](https://storm.apache.org/releases/1.1.0/flux.html) per Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="060ae-145">This file defines the Storm topology using the [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework for Apache Storm.</span></span>

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

<span data-ttu-id="060ae-146">Questo YAML definisce i seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="060ae-146">This YAML defines the following items:</span></span>

* <span data-ttu-id="060ae-147">`syncPolicy`: specifica quando i file vengono sincronizzati/allineati con il file system.</span><span class="sxs-lookup"><span data-stu-id="060ae-147">`syncPolicy`: Defines when files are synched/flushed to the file system.</span></span> <span data-ttu-id="060ae-148">In questo esempio, ogni 1000 tuple.</span><span class="sxs-lookup"><span data-stu-id="060ae-148">In this example, every 1000 tuples.</span></span>
* <span data-ttu-id="060ae-149">`fileNameFormat`: specifica il modello di percorso e nome del file da usare per la scrittura di file.</span><span class="sxs-lookup"><span data-stu-id="060ae-149">`fileNameFormat`: Defines the path and file name pattern to use when writing files.</span></span> <span data-ttu-id="060ae-150">In questo esempio, il percorso viene fornito in fase di runtime usando un filtro e l'estensione è `.txt`.</span><span class="sxs-lookup"><span data-stu-id="060ae-150">In this example, the path is provided at runtime using a filter, and the file extension is `.txt`.</span></span>
* <span data-ttu-id="060ae-151">`recordFormat`: specifica il formato interno dei file scritti.</span><span class="sxs-lookup"><span data-stu-id="060ae-151">`recordFormat`: Defines the internal format of the files written.</span></span> <span data-ttu-id="060ae-152">In questo esempio, i campi sono delimitati dal carattere `|`.</span><span class="sxs-lookup"><span data-stu-id="060ae-152">In this example, fields are delimited by the `|` character.</span></span>
* <span data-ttu-id="060ae-153">`rotationPolicy`: specifica quando ruotare i file.</span><span class="sxs-lookup"><span data-stu-id="060ae-153">`rotationPolicy`: Defines when to rotate files.</span></span> <span data-ttu-id="060ae-154">In questo esempio, non viene eseguita alcuna rotazione.</span><span class="sxs-lookup"><span data-stu-id="060ae-154">In this example, no rotation is performed.</span></span>
* <span data-ttu-id="060ae-155">`hdfs-bolt`: usa i componenti precedenti come parametri di configurazione per la classe `HdfsBolt`.</span><span class="sxs-lookup"><span data-stu-id="060ae-155">`hdfs-bolt`: Uses the previous components as configuration parameters for the `HdfsBolt` class.</span></span>

<span data-ttu-id="060ae-156">Per altre informazioni sul framework Flux, vedere [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="060ae-156">For more information on the Flux framework, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="configure-the-cluster"></a><span data-ttu-id="060ae-157">Configurare il cluster</span><span class="sxs-lookup"><span data-stu-id="060ae-157">Configure the cluster</span></span>

<span data-ttu-id="060ae-158">Per impostazione predefinita, Storm in HDInsight non include i componenti che HdfsBolt usa per comunicare con Archiviazione di Azure o Data Lake Store nel classpath di Storm.</span><span class="sxs-lookup"><span data-stu-id="060ae-158">By default, Storm on HDInsight does not include the components that HdfsBolt uses to communicate with Azure Storage or Data Lake Store in Storm's classpath.</span></span> <span data-ttu-id="060ae-159">Usare la seguente azione script per aggiungere questi componenti alla directory `extlib` per Storm nel cluster:</span><span class="sxs-lookup"><span data-stu-id="060ae-159">Use the following script action to add these components to the `extlib` directory for Storm on your cluster:</span></span>

<span data-ttu-id="060ae-160">| URI script | Nodi per l'applicazione| Parametri | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisore | Nessuno |</span><span class="sxs-lookup"><span data-stu-id="060ae-160">| Script URI | Nodes to apply it to| Parameters | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | None |</span></span>

<span data-ttu-id="060ae-161">Per informazioni sull'uso di questo script con il cluster, vedere il documento [Customize HDInsight clusters using script actions](./hdinsight-hadoop-customize-cluster-linux.md) (Personalizzare i cluster HDInsight con le azioni script).</span><span class="sxs-lookup"><span data-stu-id="060ae-161">For information on using this script with your cluster, see the [Customize HDInsight clusters using script actions](./hdinsight-hadoop-customize-cluster-linux.md) document.</span></span>

## <a name="build-and-package-the-topology"></a><span data-ttu-id="060ae-162">Compilare e creare il pacchetto della topologia</span><span class="sxs-lookup"><span data-stu-id="060ae-162">Build and package the topology</span></span>

1. <span data-ttu-id="060ae-163">Scaricare il progetto di esempio da [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) nell'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="060ae-163">Download the example project from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) to your development environment.</span></span>

2. <span data-ttu-id="060ae-164">Da un prompt dei comandi, un terminale o una sessione shell, modificare le directory impostandole sulla directory principale del progetto scaricato.</span><span class="sxs-lookup"><span data-stu-id="060ae-164">From a command prompt, terminal, or shell session, change directories to the root of the downloaded project.</span></span> <span data-ttu-id="060ae-165">Per compilare e creare la topologia, usare il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="060ae-165">To build and package the topology, use the following command:</span></span>
   
        mvn compile package
   
    <span data-ttu-id="060ae-166">Al termine della compilazione e creazione, ci sarà una nuova directory denominata `target`, che contiene un file denominato `StormToHdfs-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="060ae-166">Once the build and packaging completes, there is a new directory named `target`, that contains a file named `StormToHdfs-1.0-SNAPSHOT.jar`.</span></span> <span data-ttu-id="060ae-167">Questo file contiene la topologia compilata.</span><span class="sxs-lookup"><span data-stu-id="060ae-167">This file contains the compiled topology.</span></span>

## <a name="deploy-and-run-the-topology"></a><span data-ttu-id="060ae-168">Distribuire ed eseguire la topologia</span><span class="sxs-lookup"><span data-stu-id="060ae-168">Deploy and run the topology</span></span>

1. <span data-ttu-id="060ae-169">Usare il comando seguente per copiare la topologia nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="060ae-169">Use the following command to copy the topology to the HDInsight cluster.</span></span> <span data-ttu-id="060ae-170">Sostituire **USER** con il nome utente SSH usato durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="060ae-170">Replace **USER** with the SSH user name you used when creating the cluster.</span></span> <span data-ttu-id="060ae-171">Sostituire **CLUSTERNAME** con il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="060ae-171">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    <span data-ttu-id="060ae-172">Quando richiesto, immettere la password usata durante la creazione dell'utente SSH per il cluster.</span><span class="sxs-lookup"><span data-stu-id="060ae-172">When prompted, enter the password used when creating the SSH user for the cluster.</span></span> <span data-ttu-id="060ae-173">Se è stata usata una chiave pubblica anziché una password, può essere necessario usare il parametro `-i` per specificare il percorso della chiave privata corrispondente.</span><span class="sxs-lookup"><span data-stu-id="060ae-173">If you used a public key instead of a password, you may need to use the `-i` parameter to specify the path to the matching private key.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="060ae-174">Per altre informazioni sull'uso di `scp` con HDInsight, vedere [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md) (Uso di SSH con HDInsight).</span><span class="sxs-lookup"><span data-stu-id="060ae-174">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="060ae-175">Al termine del caricamento, usare il comando seguente per connettersi al cluster HDInsight tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="060ae-175">Once the upload completes, use the following to connect to the HDInsight cluster using SSH.</span></span> <span data-ttu-id="060ae-176">Sostituire **USER** con il nome utente SSH usato durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="060ae-176">Replace **USER** with the SSH user name you used when creating the cluster.</span></span> <span data-ttu-id="060ae-177">Sostituire **CLUSTERNAME** con il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="060ae-177">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="060ae-178">Quando richiesto, immettere la password usata durante la creazione dell'utente SSH per il cluster.</span><span class="sxs-lookup"><span data-stu-id="060ae-178">When prompted, enter the password used when creating the SSH user for the cluster.</span></span> <span data-ttu-id="060ae-179">Se è stata usata una chiave pubblica anziché una password, può essere necessario usare il parametro `-i` per specificare il percorso della chiave privata corrispondente.</span><span class="sxs-lookup"><span data-stu-id="060ae-179">If you used a public key instead of a password, you may need to use the `-i` parameter to specify the path to the matching private key.</span></span>
   
   <span data-ttu-id="060ae-180">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="060ae-180">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="060ae-181">Dopo la connessione, usare il comando seguente per creare un file denominato `dev.properties`:</span><span class="sxs-lookup"><span data-stu-id="060ae-181">Once connected, use the following command to create a file named `dev.properties`:</span></span>

        nano dev.properties

4. <span data-ttu-id="060ae-182">Usare il testo seguente come contenuto del file `dev.properties`:</span><span class="sxs-lookup"><span data-stu-id="060ae-182">Use the following text as the contents of the `dev.properties` file:</span></span>

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > <span data-ttu-id="060ae-183">In questo esempio si presuppone che il cluster usi un account di archiviazione di Azure come archivio predefinito.</span><span class="sxs-lookup"><span data-stu-id="060ae-183">This example assumes that your cluster uses an Azure Storage account as the default storage.</span></span> <span data-ttu-id="060ae-184">Se il cluster usa Azure Data Lake Store, usare invece `hdfs.url: adl:///`.</span><span class="sxs-lookup"><span data-stu-id="060ae-184">If your cluster uses Azure Data Lake Store, use `hdfs.url: adl:///` instead.</span></span>
    
    <span data-ttu-id="060ae-185">Per salvare il file, usare __CTRL + X__, poi __Y__e infine premere __Invio__.</span><span class="sxs-lookup"><span data-stu-id="060ae-185">To save the file, use __Ctrl + X__, then __Y__, and finally __Enter__.</span></span> <span data-ttu-id="060ae-186">I valori in questo file impostano l'URL di Data Lake Store e il nome della directory in cui vengono scritti i dati.</span><span class="sxs-lookup"><span data-stu-id="060ae-186">The values in this file set the Data Lake store URL and the directory name that data is written to.</span></span>

3. <span data-ttu-id="060ae-187">Per avviare la topologia, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="060ae-187">Use the following command to start the topology:</span></span>
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    <span data-ttu-id="060ae-188">Questo comando avvia la topologia usando il framework Flux, inviandolo al nodo Nimbus del cluster.</span><span class="sxs-lookup"><span data-stu-id="060ae-188">This command starts the topology using the Flux framework by submitting it to the Nimbus node of the cluster.</span></span> <span data-ttu-id="060ae-189">La topologia viene definita mediante il file `writetohdfs.yaml` incluso nel file con estensione jar.</span><span class="sxs-lookup"><span data-stu-id="060ae-189">The topology is defined by the `writetohdfs.yaml` file included in the jar.</span></span> <span data-ttu-id="060ae-190">Il file `dev.properties` viene passato come filtro e la topologia legge i dati contenuti nel file.</span><span class="sxs-lookup"><span data-stu-id="060ae-190">The `dev.properties` file is passed as a filter, and the values contained in the file are read by the topology.</span></span>

## <a name="view-output-data"></a><span data-ttu-id="060ae-191">Visualizzare i dati di output</span><span class="sxs-lookup"><span data-stu-id="060ae-191">View output data</span></span>

<span data-ttu-id="060ae-192">Per visualizzare i dati, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="060ae-192">To view the data, use the following command:</span></span>

    hdfs dfs -ls /stormdata/

<span data-ttu-id="060ae-193">Viene visualizzato un elenco dei file creati dalla topologia.</span><span class="sxs-lookup"><span data-stu-id="060ae-193">A list of the files created by this topology is displayed.</span></span>

<span data-ttu-id="060ae-194">Nell'elenco seguente è riportato un esempio dei dati restituiti dai comandi precedenti:</span><span class="sxs-lookup"><span data-stu-id="060ae-194">The following list is an example of the data retuned by the previous commands:</span></span>

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-the-topology"></a><span data-ttu-id="060ae-195">Arrestare la topologia</span><span class="sxs-lookup"><span data-stu-id="060ae-195">Stop the topology</span></span>

<span data-ttu-id="060ae-196">Le topologie Storm vengono eseguite fino all'arresto o all'eliminazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="060ae-196">Storm topologies run until stopped, or the cluster is deleted.</span></span> <span data-ttu-id="060ae-197">Per arrestare la topologia, usare il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="060ae-197">To stop the topology, use the following command:</span></span>

    storm kill hdfswriter

## <a name="delete-your-cluster"></a><span data-ttu-id="060ae-198">Eliminare il cluster</span><span class="sxs-lookup"><span data-stu-id="060ae-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="060ae-199">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="060ae-199">Next steps</span></span>

<span data-ttu-id="060ae-200">Dopo aver appreso come usare Storm per scrivere in Archiviazione di Azure e Azure Data Lake Store, è possibile vedere altri [esempi di Storm per HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="060ae-200">Now that you have learned how to use Storm to write to Azure Storage and Azure Data Lake Store, discover other [Storm examples for HDInsight](hdinsight-storm-example-topology.md).</span></span>

