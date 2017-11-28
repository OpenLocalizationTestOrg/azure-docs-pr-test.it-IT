---
title: i flussi di lavoro di aaaUse Oozie Hadoop in HDInsight basati su Linux | Documenti Microsoft
description: Usare Oozie di Hadoop in HDInsight basati su Linux. Informazioni su come un flusso di lavoro, Oozie toodefine e inviare un processo di Oozie.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d7603471-5076-43d1-8b9a-dbc4e366ce5d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: cb5682837543312621e3424b7a9341b5d2a00bf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-on-linux-based-hdinsight"></a><span data-ttu-id="194b4-104">Utilizzare Oozie con Hadoop toodefine ed eseguire un flusso di lavoro in HDInsight basati su Linux</span><span class="sxs-lookup"><span data-stu-id="194b4-104">Use Oozie with Hadoop toodefine and run a workflow on Linux-based HDInsight</span></span>

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="194b4-105">Informazioni su come toouse Oozie Apache con Hadoop in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="194b4-105">Learn how toouse Apache Oozie with Hadoop on HDInsight.</span></span> <span data-ttu-id="194b4-106">Apache Oozie è un sistema di flusso di lavoro/coordinamento che consente di gestire i processi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="194b4-106">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="194b4-107">Oozie è integrato con lo stack di Hadoop hello e supporta hello seguenti processi:</span><span class="sxs-lookup"><span data-stu-id="194b4-107">Oozie is integrated with hello Hadoop stack, and it supports hello following jobs:</span></span>

* <span data-ttu-id="194b4-108">Apache MapReduce</span><span class="sxs-lookup"><span data-stu-id="194b4-108">Apache MapReduce</span></span>
* <span data-ttu-id="194b4-109">Apache Pig</span><span class="sxs-lookup"><span data-stu-id="194b4-109">Apache Pig</span></span>
* <span data-ttu-id="194b4-110">Apache Hive</span><span class="sxs-lookup"><span data-stu-id="194b4-110">Apache Hive</span></span>
* <span data-ttu-id="194b4-111">Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="194b4-111">Apache Sqoop</span></span>

<span data-ttu-id="194b4-112">Oozie può essere anche i processi utilizzati tooschedule sistema tooa specifico, ad esempio programmi Java o gli script della shell</span><span class="sxs-lookup"><span data-stu-id="194b4-112">Oozie can also be used tooschedule jobs that are specific tooa system, like Java programs or shell scripts</span></span>

> [!NOTE]
> <span data-ttu-id="194b4-113">Un'altra opzione per definire i flussi di lavoro con HDInsight è Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="194b4-113">Another option for defining workflows with HDInsight is Azure Data Factory.</span></span> <span data-ttu-id="194b4-114">toolearn ulteriori informazioni su Data Factory di Azure, vedere [usare Pig e Hive con Data Factory][azure-data-factory-pig-hive].</span><span class="sxs-lookup"><span data-stu-id="194b4-114">toolearn more about Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="194b4-115">Oozie non è abilitato su HDInsight appartenente al dominio.</span><span class="sxs-lookup"><span data-stu-id="194b4-115">Oozie is not enabled on domain-joined HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="194b4-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="194b4-116">Prerequisites</span></span>

* <span data-ttu-id="194b4-117">**Un cluster di HDInsight**: vedere [Introduzione all'uso di HDInsight in Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="194b4-117">**An HDInsight cluster**: See [Get Started with HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="194b4-118">passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Linux.</span><span class="sxs-lookup"><span data-stu-id="194b4-118">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="194b4-119">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="194b4-119">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="194b4-120">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="194b4-120">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="example-workflow"></a><span data-ttu-id="194b4-121">Esempio di flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="194b4-121">Example workflow</span></span>

<span data-ttu-id="194b4-122">flusso di lavoro Hello utilizzato in questo documento contiene due azioni.</span><span class="sxs-lookup"><span data-stu-id="194b4-122">hello workflow used in this document contains two actions.</span></span> <span data-ttu-id="194b4-123">Le azioni sono definizioni per attività, ad esempio l'esecuzione di Hive, Sqoop, MapReduce o altri processi:</span><span class="sxs-lookup"><span data-stu-id="194b4-123">Actions are definitions for tasks, such as running Hive, Sqoop, MapReduce, or other process:</span></span>

![Diagramma del flusso di lavoro][img-workflow-diagram]

1. <span data-ttu-id="194b4-125">Un'azione di Hive esegue uno script HiveQL tooextract record da hello **hivesampletable** incluso in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="194b4-125">A Hive action runs a HiveQL script tooextract records from hello **hivesampletable** included with HDInsight.</span></span> <span data-ttu-id="194b4-126">Ogni riga di dati descrive una visita da un dispositivo mobile specifico.</span><span class="sxs-lookup"><span data-stu-id="194b4-126">Each row of data describes a visit from a specific mobile device.</span></span> <span data-ttu-id="194b4-127">formato di record Hello viene visualizzato toohello simile, il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="194b4-127">hello record format appears similar toohello following text:</span></span>

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    <span data-ttu-id="194b4-128">Hello script Hive utilizzato in questo documento conta le visite totale hello per ogni piattaforma (ad esempio Android o iPhone) e archivia i conteggi hello tooa nuova tabella Hive.</span><span class="sxs-lookup"><span data-stu-id="194b4-128">hello Hive script used in this document counts hello total visits for each platform (such as Android or iPhone) and stores hello counts tooa new Hive table.</span></span>

    <span data-ttu-id="194b4-129">Per altre informazioni su Hive, vedere [Usare Hive con HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="194b4-129">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

2. <span data-ttu-id="194b4-130">Un'azione Sqoop Esporta contenuto hello di hello nuova tabella tooa tabella Hive in un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="194b4-130">A Sqoop action exports hello contents of hello new Hive table tooa table in an Azure SQL database.</span></span> <span data-ttu-id="194b4-131">Per altre informazioni su Sqoop, vedere [Usare Sqoop con Hadoop in HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="194b4-131">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="194b4-132">Per le versioni Oozie supportate nei cluster HDInsight, vedere [novità introdotta nelle versioni di cluster Hadoop hello fornite da HDInsight][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="194b4-132">For supported Oozie versions on HDInsight clusters, see [What's new in hello Hadoop cluster versions provided by HDInsight][hdinsight-versions].</span></span>

## <a name="create-hello-working-directory"></a><span data-ttu-id="194b4-133">Creare la directory di lavoro hello</span><span class="sxs-lookup"><span data-stu-id="194b4-133">Create hello working directory</span></span>

<span data-ttu-id="194b4-134">Oozie prevede che le risorse necessarie per un processo toobe archiviate in hello stessa directory.</span><span class="sxs-lookup"><span data-stu-id="194b4-134">Oozie expects resources required for a job toobe stored in hello same directory.</span></span> <span data-ttu-id="194b4-135">Questo esempio usa **wasb:///tutorials/useoozie**.</span><span class="sxs-lookup"><span data-stu-id="194b4-135">This example uses **wasb:///tutorials/useoozie**.</span></span> <span data-ttu-id="194b4-136">Directory e directory di dati hello che contiene una tabella Hive nuovo hello creata da questo flusso di lavoro, utilizzare hello toocreate di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="194b4-136">Use hello following command toocreate this directory, and hello data directory that holds hello new Hive table created by this workflow:</span></span>

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> <span data-ttu-id="194b4-137">Hello `-p` parametro fa sì che tutte le directory in hello percorso toobe creato.</span><span class="sxs-lookup"><span data-stu-id="194b4-137">hello `-p` parameter causes all directories in hello path toobe created.</span></span> <span data-ttu-id="194b4-138">Hello **dati** directory è toohold utilizzati dati utilizzati da hello **useooziewf.hql** script.</span><span class="sxs-lookup"><span data-stu-id="194b4-138">hello **data** directory is used toohold data used by hello **useooziewf.hql** script.</span></span>

<span data-ttu-id="194b4-139">Eseguire inoltre hello seguente comando, che assicura che Oozie può rappresentare l'account utente quando si eseguono processi Hive e Sqoop.</span><span class="sxs-lookup"><span data-stu-id="194b4-139">Also run hello following command, which ensures that Oozie can impersonate your user account when running Hive and Sqoop jobs.</span></span> <span data-ttu-id="194b4-140">Sostituire **USERNAME** con il proprio nome di accesso:</span><span class="sxs-lookup"><span data-stu-id="194b4-140">Replace **USERNAME** with your login name:</span></span>

```
sudo adduser USERNAME users
```

> [!NOTE]
> <span data-ttu-id="194b4-141">È possibile ignorare gli errori di tale utente hello è già membro di hello `users` gruppo.</span><span class="sxs-lookup"><span data-stu-id="194b4-141">You can ignore errors that hello user is already a member of hello `users` group.</span></span>

## <a name="add-a-database-driver"></a><span data-ttu-id="194b4-142">Aggiungere un driver di database</span><span class="sxs-lookup"><span data-stu-id="194b4-142">Add a database driver</span></span>

<span data-ttu-id="194b4-143">Poiché questo flusso di lavoro utilizza Sqoop tooexport dati tooSQL Database, è necessario fornire che una copia del driver JDBC hello utilizzato tootalk tooSQL Database.</span><span class="sxs-lookup"><span data-stu-id="194b4-143">Since this workflow uses Sqoop tooexport data tooSQL Database, you must provide a copy of hello JDBC driver used tootalk tooSQL Database.</span></span> <span data-ttu-id="194b4-144">Utilizzare hello seguenti toocopy comando è la directory di lavoro toohello:</span><span class="sxs-lookup"><span data-stu-id="194b4-144">Use hello following command toocopy it toohello working directory:</span></span>

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

<span data-ttu-id="194b4-145">Se il flusso di lavoro utilizzato altre risorse, ad esempio un file jar contenente un'applicazione di MapReduce, sarà necessario tooadd anche queste risorse.</span><span class="sxs-lookup"><span data-stu-id="194b4-145">If your workflow used other resources, such as a jar containing a MapReduce application, you would need tooadd these resources as well.</span></span>

## <a name="define-hello-hive-query"></a><span data-ttu-id="194b4-146">Definire query Hive hello</span><span class="sxs-lookup"><span data-stu-id="194b4-146">Define hello Hive query</span></span>

<span data-ttu-id="194b4-147">Utilizzare hello seguendo i passaggi toocreate uno script HiveQL che definisce una query, che viene utilizzata in un flusso di lavoro Oozie più avanti in questo documento.</span><span class="sxs-lookup"><span data-stu-id="194b4-147">Use hello following steps toocreate a HiveQL script that defines a query, which is used in an Oozie workflow later in this document.</span></span>

1. <span data-ttu-id="194b4-148">Connettere il cluster toohello tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="194b4-148">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="194b4-149">il comando seguente Hello è riportato un esempio dell'utilizzo di hello `ssh` comando.</span><span class="sxs-lookup"><span data-stu-id="194b4-149">hello following command is an example of using hello `ssh` command.</span></span> <span data-ttu-id="194b4-150">Sostituire __USERNAME__ con utente SSH hello per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-150">Replace __USERNAME__ with hello SSH user for hello cluster.</span></span> <span data-ttu-id="194b4-151">Sostituire __CLUSTERNAME__ con nome hello del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-151">Replace __CLUSTERNAME__ with hello name of hello HDInsight cluster.</span></span>

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="194b4-152">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="194b4-152">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="194b4-153">Da hello connessione SSH, utilizzare hello successivo comando toocreate un file:</span><span class="sxs-lookup"><span data-stu-id="194b4-153">From hello SSH connection, use hello following command toocreate a file:</span></span>

    ```
    nano useooziewf.hql
    ```

3. <span data-ttu-id="194b4-154">Una volta verrà aperto l'editor nano hello usare hello seguente query come contenuto di hello del file hello:</span><span class="sxs-lookup"><span data-stu-id="194b4-154">Once hello nano editor opens, use hello following query as hello contents of hello file:</span></span>

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    <span data-ttu-id="194b4-155">Esistono due variabili utilizzate nello script hello:</span><span class="sxs-lookup"><span data-stu-id="194b4-155">There are two variables used in hello script:</span></span>

    * <span data-ttu-id="194b4-156">**${hiveTableName}**: contiene il nome di hello di hello tabella toobe creato</span><span class="sxs-lookup"><span data-stu-id="194b4-156">**${hiveTableName}**: contains hello name of hello table toobe created</span></span>

    * <span data-ttu-id="194b4-157">**${hiveDataFolder}**: hello percorso toostore hello i file di dati per la tabella hello contiene</span><span class="sxs-lookup"><span data-stu-id="194b4-157">**${hiveDataFolder}**: contains hello location toostore hello data files for hello table</span></span>

    <span data-ttu-id="194b4-158">file di definizione del flusso di lavoro Hello (workflow in questa esercitazione) passa i valori toothis script HiveQL in fase di esecuzione</span><span class="sxs-lookup"><span data-stu-id="194b4-158">hello workflow definition file (workflow.xml in this tutorial) passes these values toothis HiveQL script at run time</span></span>

4. <span data-ttu-id="194b4-159">tooexit hello editor, premere Ctrl + X.</span><span class="sxs-lookup"><span data-stu-id="194b4-159">tooexit hello editor, press Ctrl-X.</span></span> <span data-ttu-id="194b4-160">Quando richiesto, selezionare **Y** toosave hello file, quindi utilizzare **invio** toouse hello **useooziewf.hql** nome file.</span><span class="sxs-lookup"><span data-stu-id="194b4-160">When prompted, select **Y** toosave hello file, then use **Enter** toouse hello **useooziewf.hql** file name.</span></span>

5. <span data-ttu-id="194b4-161">Seguente hello utilizzare comandi toocopy **useooziewf.hql** troppo**wasb:///tutorials/useoozie/useooziewf.hql**:</span><span class="sxs-lookup"><span data-stu-id="194b4-161">Use hello following commands toocopy **useooziewf.hql** too**wasb:///tutorials/useoozie/useooziewf.hql**:</span></span>

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    <span data-ttu-id="194b4-162">Questi comandi archiviano hello **useooziewf.hql** nel file per archiviazione hello HDFS compatibile con cluster hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-162">These commands store hello **useooziewf.hql** file on hello HDFS-compatible storage for hello cluster.</span></span>

## <a name="define-hello-workflow"></a><span data-ttu-id="194b4-163">Definire hello flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="194b4-163">Define hello workflow</span></span>

<span data-ttu-id="194b4-164">Le definizioni dei flussi di lavoro di Oozie sono scritte in linguaggio hPDL (XML Process Definition Language).</span><span class="sxs-lookup"><span data-stu-id="194b4-164">Oozie workflows definitions are written in hPDL (an XML Process Definition Language).</span></span> <span data-ttu-id="194b4-165">Utilizzare hello flusso di lavoro hello toodefine i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="194b4-165">Use hello following steps toodefine hello workflow:</span></span>

1. <span data-ttu-id="194b4-166">Dopo l'istruzione toocreate hello e modificare un nuovo file:</span><span class="sxs-lookup"><span data-stu-id="194b4-166">Use hello following statement toocreate and edit a new file:</span></span>

    ```
    nano workflow.xml
    ```

2. <span data-ttu-id="194b4-167">Una volta che viene aperto l'editor nano hello, immettere hello seguente XML come contenuto del file hello:</span><span class="sxs-lookup"><span data-stu-id="194b4-167">Once hello nano editor opens, enter hello following XML as hello file contents:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start too= "RunHiveScript"/>
        <action name="RunHiveScript">
        <hive xmlns="uri:oozie:hive-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.job.queue.name</name>
                <value>${queueName}</value>
            </property>
            </configuration>
            <script>${hiveScript}</script>
            <param>hiveTableName=${hiveTableName}</param>
            <param>hiveDataFolder=${hiveDataFolder}</param>
        </hive>
        <ok to="RunSqoopExport"/>
        <error to="fail"/>
        </action>
        <action name="RunSqoopExport">
        <sqoop xmlns="uri:oozie:sqoop-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.compress.map.output</name>
                <value>true</value>
            </property>
            </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveDataFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\t"</arg>
            <archive>sqljdbc41.jar</archive>
            </sqoop>
        <ok to="end"/>
        <error to="fail"/>
        </action>
        <kill name="fail">
        <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>
        <end name="end"/>
    </workflow-app>
    ```

    <span data-ttu-id="194b4-168">Esistono due azioni definite nel flusso di lavoro hello:</span><span class="sxs-lookup"><span data-stu-id="194b4-168">There are two actions defined in hello workflow:</span></span>

   * <span data-ttu-id="194b4-169">**RunHiveScript**: questa azione è l'azione di avvio hello ed esegue hello **useooziewf.hql** lo script Hive</span><span class="sxs-lookup"><span data-stu-id="194b4-169">**RunHiveScript**: This action is hello start action, and runs hello **useooziewf.hql** Hive script</span></span>

   * <span data-ttu-id="194b4-170">**RunSqoopExport**: questa azione Esporta dati hello creati da hello Hive script tooSQL utilizzando Sqoop del Database.</span><span class="sxs-lookup"><span data-stu-id="194b4-170">**RunSqoopExport**: This action exports hello data created from hello Hive script tooSQL Database using Sqoop.</span></span> <span data-ttu-id="194b4-171">Questa azione viene eseguita solo se hello **RunHiveScript** azione ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="194b4-171">This action only runs if hello **RunHiveScript** action is successful.</span></span>

     <span data-ttu-id="194b4-172">flusso di lavoro Hello ha diverse voci, ad esempio `${jobTracker}`.</span><span class="sxs-lookup"><span data-stu-id="194b4-172">hello workflow has several entries, such as `${jobTracker}`.</span></span> <span data-ttu-id="194b4-173">Queste voci vengono sostituite da valori utilizzati nella definizione di processo hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-173">These entries are replaced by values you use in hello job definition.</span></span> <span data-ttu-id="194b4-174">definizione di processo Hello viene creata più avanti in questo documento.</span><span class="sxs-lookup"><span data-stu-id="194b4-174">hello job definition is created later in this document.</span></span>

     <span data-ttu-id="194b4-175">Anche i hello nota `<archive>sqljdbc4.jar</arcive>` voce nella sezione Sqoop hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-175">Also note hello `<archive>sqljdbc4.jar</arcive>` entry in hello Sqoop section.</span></span> <span data-ttu-id="194b4-176">Questa voce indica Oozie toomake questo archivio disponibile per Sqoop quando si esegue questa azione.</span><span class="sxs-lookup"><span data-stu-id="194b4-176">This entry instructs Oozie toomake this archive available for Sqoop when this action runs.</span></span>

3. <span data-ttu-id="194b4-177">Utilizzare Ctrl + X, quindi **Y** e **invio** file hello toosave.</span><span class="sxs-lookup"><span data-stu-id="194b4-177">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

4. <span data-ttu-id="194b4-178">Comando che segue di hello utilizzare hello toocopy **workflow** file troppo**/tutorials/useoozie/workflow.xml**:</span><span class="sxs-lookup"><span data-stu-id="194b4-178">Use hello following command toocopy hello **workflow.xml** file too**/tutorials/useoozie/workflow.xml**:</span></span>

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-hello-database"></a><span data-ttu-id="194b4-179">Creare database hello</span><span class="sxs-lookup"><span data-stu-id="194b4-179">Create hello database</span></span>

<span data-ttu-id="194b4-180">toocreate un Database SQL di Azure, seguire i passaggi hello hello [creare un Database SQL](../sql-database/sql-database-get-started.md) documento.</span><span class="sxs-lookup"><span data-stu-id="194b4-180">toocreate an Azure SQL Database, follow hello steps in hello [Create a SQL Database](../sql-database/sql-database-get-started.md) document.</span></span> <span data-ttu-id="194b4-181">Quando si crea il database di hello, utilizzare `oozietest` come nome del database hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-181">When creating hello database, use `oozietest` as hello database name.</span></span> <span data-ttu-id="194b4-182">Inoltre, prendere nota del nome hello hello del server di database.</span><span class="sxs-lookup"><span data-stu-id="194b4-182">Also make a note of hello name of hello database server.</span></span>

### <a name="create-hello-table"></a><span data-ttu-id="194b4-183">Creare la tabella hello</span><span class="sxs-lookup"><span data-stu-id="194b4-183">Create hello table</span></span>

> [!NOTE]
> <span data-ttu-id="194b4-184">Esistono molti modi tooconnect tooSQL Database toocreate una tabella.</span><span class="sxs-lookup"><span data-stu-id="194b4-184">There are many ways tooconnect tooSQL Database toocreate a table.</span></span> <span data-ttu-id="194b4-185">Hello seguenti utilizzano [disporre di FreeTDS](http://www.freetds.org/) dal cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-185">hello following steps use [FreeTDS](http://www.freetds.org/) from hello HDInsight cluster.</span></span>


1. <span data-ttu-id="194b4-186">Utilizzare hello successivo comando tooinstall disporre di FreeTDS nel cluster HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="194b4-186">Use hello following command tooinstall FreeTDS on hello HDInsight cluster:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. <span data-ttu-id="194b4-187">Una volta installato, disporre di FreeTDS seguente hello utilizzare comandi tooconnect toohello server di Database SQL creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="194b4-187">Once FreeTDS has been installed, use hello following command tooconnect toohello SQL Database server you created previously:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="194b4-188">Viene visualizzato toohello simili di output il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="194b4-188">You receive output similar toohello following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toooozietest
        1>

3. <span data-ttu-id="194b4-189">In hello `1>` richiesto, immettere hello seguenti righe:</span><span class="sxs-lookup"><span data-stu-id="194b4-189">At hello `1>` prompt, enter hello following lines:</span></span>

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    <span data-ttu-id="194b4-190">Quando hello `GO` istruzione viene immessa, le istruzioni precedenti hello vengono valutate.</span><span class="sxs-lookup"><span data-stu-id="194b4-190">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="194b4-191">Le istruzioni seguenti creano una tabella denominata **mobiledata** utilizzato dal flusso di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-191">These statements create a table named **mobiledata** that is used by hello workflow.</span></span>

    <span data-ttu-id="194b4-192">Hello utilizzare tooverify che hello nella tabella seguente è stata creata:</span><span class="sxs-lookup"><span data-stu-id="194b4-192">Use hello following tooverify that hello table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="194b4-193">Vedrai toohello simili di output il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="194b4-193">You see output similar toohello following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. <span data-ttu-id="194b4-194">Immettere `exit` in hello `1>` richiedere utilità di tooexit hello tsql.</span><span class="sxs-lookup"><span data-stu-id="194b4-194">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="create-hello-job-definition"></a><span data-ttu-id="194b4-195">Crea definizione processo hello</span><span class="sxs-lookup"><span data-stu-id="194b4-195">Create hello job definition</span></span>

<span data-ttu-id="194b4-196">definizione del processo Hello descrive dove toofind hello workflow.</span><span class="sxs-lookup"><span data-stu-id="194b4-196">hello job definition describes where toofind hello workflow.xml.</span></span> <span data-ttu-id="194b4-197">Viene inoltre descritto dove toofind altri file utilizzati dal flusso di lavoro di hello (ad esempio useooziewf.hql). Definisce inoltre i valori hello per le proprietà utilizzate all'interno del flusso di lavoro hello e i file associati.</span><span class="sxs-lookup"><span data-stu-id="194b4-197">It also describes where toofind other files used by hello workflow (such as useooziewf.hql.) It also defines hello values for properties used within hello workflow and associated files.</span></span>

1. <span data-ttu-id="194b4-198">Utilizzare hello seguente comando tooget hello indirizzo completo di spazio di archiviazione predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-198">Use hello following command tooget hello full address of hello default storage.</span></span> <span data-ttu-id="194b4-199">Questo indirizzo viene utilizzato nel file di configurazione hello in proposito:</span><span class="sxs-lookup"><span data-stu-id="194b4-199">This address is used in hello configuration file in a moment:</span></span>

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    <span data-ttu-id="194b4-200">Questo comando restituisce toohello simile di informazioni XML seguente:</span><span class="sxs-lookup"><span data-stu-id="194b4-200">This command returns information similar toohello following XML:</span></span>

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > <span data-ttu-id="194b4-201">Se il cluster di HDInsight hello utilizza l'archiviazione di Azure come spazio di archiviazione predefinito hello, hello `<value>` il contenuto degli elementi inizia con `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="194b4-201">If hello HDInsight cluster uses Azure Storage as hello default storage, hello `<value>` element contents begin with `wasb://`.</span></span> <span data-ttu-id="194b4-202">Se, invece, viene usato Azure Data Lake Store, il contenuto inizia con `adl://`.</span><span class="sxs-lookup"><span data-stu-id="194b4-202">If Azure Data Lake Store is used instead, it begins with `adl://`.</span></span>

    <span data-ttu-id="194b4-203">Salvare il contenuto di hello di hello `<value>` elemento, perché viene utilizzato nei passaggi successivi hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-203">Save hello contents of hello `<value>` element, as it is used in hello next steps.</span></span>

2. <span data-ttu-id="194b4-204">Utilizzare hello successivo comando tooget FQDN del nodo head del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-204">Use hello following command tooget FQDN of hello cluster headnode.</span></span> <span data-ttu-id="194b4-205">Queste informazioni vengono utilizzate per hello JobTracker indirizzo hello cluster:</span><span class="sxs-lookup"><span data-stu-id="194b4-205">This information is used for hello JobTracker address for hello cluster:</span></span>

    ```
    hostname -f
    ```

    <span data-ttu-id="194b4-206">Restituisce toohello di informazioni simili seguente testo:</span><span class="sxs-lookup"><span data-stu-id="194b4-206">This returns information similar toohello following text:</span></span>

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    <span data-ttu-id="194b4-207">Hello porta usata per hello JobTracker è 8050, pertanto è hello indirizzo completo toouse per hello JobTracker `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span><span class="sxs-lookup"><span data-stu-id="194b4-207">hello port used for hello JobTracker is 8050, so hello full address toouse for hello JobTracker is `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span></span>

3. <span data-ttu-id="194b4-208">Utilizzare hello toocreate hello Oozie processo di configurazione della definizione seguente:</span><span class="sxs-lookup"><span data-stu-id="194b4-208">Use hello following toocreate hello Oozie job definition configuration:</span></span>

    ```
    nano job.xml
    ```

4. <span data-ttu-id="194b4-209">Una volta verrà aperto l'editor nano hello usare hello seguente XML come contenuto di hello del file hello:</span><span class="sxs-lookup"><span data-stu-id="194b4-209">Once hello nano editor opens, use hello following XML as hello contents of hello file:</span></span>

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
        <name>nameNode</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
        </property>

        <property>
        <name>jobTracker</name>
        <value>JOBTRACKERADDRESS</value>
        </property>

        <property>
        <name>queueName</name>
        <value>default</value>
        </property>

        <property>
        <name>oozie.use.system.libpath</name>
        <value>true</value>
        </property>

        <property>
        <name>hiveScript</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/useooziewf.hql</value>
        </property>

        <property>
        <name>hiveTableName</name>
        <value>mobilecount</value>
        </property>

        <property>
        <name>hiveDataFolder</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/data</value>
        </property>

        <property>
        <name>sqlDatabaseConnectionString</name>
        <value>"jdbc:sqlserver://serverName.database.windows.net;user=adminLogin;password=adminPassword;database=oozietest"</value>
        </property>

        <property>
        <name>sqlDatabaseTableName</name>
        <value>mobiledata</value>
        </property>

        <property>
        <name>user.name</name>
        <value>YourName</value>
        </property>

        <property>
        <name>oozie.wf.application.path</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
    </configuration>
    ```

   * <span data-ttu-id="194b4-210">Sostituire tutte le istanze di  **wasb://mycontainer@mystorageaccount.blob.core.windows.net**  con valore hello ricevuto in precedenza per l'archiviazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="194b4-210">Replace all instances of **wasb://mycontainer@mystorageaccount.blob.core.windows.net** with hello value you received earlier for default storage.</span></span>

     > [!WARNING]
     > <span data-ttu-id="194b4-211">Se il percorso di hello è un `wasb` percorso, è necessario utilizzare il percorso completo di hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-211">If hello path is a `wasb` path, you must use hello full path.</span></span> <span data-ttu-id="194b4-212">Non usare la versione abbreviata toojust `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="194b4-212">Do not shorten it toojust `wasb:///`.</span></span>

   * <span data-ttu-id="194b4-213">Sostituire **JOBTRACKERADDRESS** con hello JobTracker/ResourceManager indirizzo è stato ricevuto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="194b4-213">Replace **JOBTRACKERADDRESS** with hello JobTracker/ResourceManager address you received earlier.</span></span>
   * <span data-ttu-id="194b4-214">Sostituire **YourName** con il nome di accesso per il cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-214">Replace **YourName** with your login name for hello HDInsight cluster.</span></span>
   * <span data-ttu-id="194b4-215">Sostituire **serverName**, **adminLogin**, e **adminPassword** con informazioni hello per Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="194b4-215">Replace **serverName**, **adminLogin**, and **adminPassword** with hello information for your Azure SQL Database.</span></span>

     <span data-ttu-id="194b4-216">La maggior parte delle informazioni presenti nel file hello è valori hello utilizzati toopopulate utilizzati nei file di workflow o ooziewf.hql hello (ad esempio ${nameNode}.)</span><span class="sxs-lookup"><span data-stu-id="194b4-216">Most of hello information in this file is used toopopulate hello values used in hello workflow.xml or ooziewf.hql files (such as ${nameNode}.)</span></span>

     > [!NOTE]
     > <span data-ttu-id="194b4-217">Hello **oozie.wf.application.path** voce definisce dove i file di workflow hello di toofind, che contiene hello flusso di lavoro è stato eseguito da questo processo.</span><span class="sxs-lookup"><span data-stu-id="194b4-217">hello **oozie.wf.application.path** entry defines where toofind hello workflow.xml file, which contains hello workflow ran by this job.</span></span>

5. <span data-ttu-id="194b4-218">Utilizzare Ctrl + X, quindi **Y** e **invio** file hello toosave.</span><span class="sxs-lookup"><span data-stu-id="194b4-218">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

## <a name="submit-and-manage-hello-job"></a><span data-ttu-id="194b4-219">Inviare e gestire il processo di hello</span><span class="sxs-lookup"><span data-stu-id="194b4-219">Submit and manage hello job</span></span>

<span data-ttu-id="194b4-220">Hello passaggi seguenti utilizzano hello Oozie comando toosubmit e gestire i flussi di lavoro Oozie nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-220">hello following steps use hello Oozie command toosubmit and manage Oozie workflows on hello cluster.</span></span> <span data-ttu-id="194b4-221">comando Oozie Hello è un'interfaccia intuitiva su hello [API REST di Oozie](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="194b4-221">hello Oozie command is a friendly interface over hello [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="194b4-222">Quando si utilizza il comando di Oozie hello, è necessario utilizzare hello FQDN per nodo head HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-222">When using hello Oozie command, you must use hello FQDN for hello HDInsight headnode.</span></span> <span data-ttu-id="194b4-223">Questo nome di dominio completo è accessibile solo da cluster hello o se hello cluster si trova in una rete virtuale di Azure, da altre macchine su hello stessa rete.</span><span class="sxs-lookup"><span data-stu-id="194b4-223">This FQDN is only accessible from hello cluster, or if hello cluster is on an Azure Virtual Network, from other machines on hello same network.</span></span>


1. <span data-ttu-id="194b4-224">Utilizzare hello tooobtain hello URL toohello Oozie servizio:</span><span class="sxs-lookup"><span data-stu-id="194b4-224">Use hello following tooobtain hello URL toohello Oozie service:</span></span>

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    <span data-ttu-id="194b4-225">Restituisce toohello simile di informazioni XML seguente:</span><span class="sxs-lookup"><span data-stu-id="194b4-225">This returns information similar toohello following XML:</span></span>

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    <span data-ttu-id="194b4-226">Hello `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` parte è hello URL toouse con hello comando Oozie.</span><span class="sxs-lookup"><span data-stu-id="194b4-226">hello `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` portion is hello URL toouse with hello Oozie command.</span></span>

2. <span data-ttu-id="194b4-227">Hello utilizzare seguente toocreate una variabile di ambiente per hello URL, non vi è tootype per ogni comando:</span><span class="sxs-lookup"><span data-stu-id="194b4-227">Use hello following toocreate an environment variable for hello URL, so you don't have tootype it for every command:</span></span>

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    <span data-ttu-id="194b4-228">Sostituire l'URL di hello con hello uno che è stato ricevuto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="194b4-228">Replace hello URL with hello one you received earlier.</span></span>
3. <span data-ttu-id="194b4-229">Utilizzare hello processo hello toosubmit seguenti:</span><span class="sxs-lookup"><span data-stu-id="194b4-229">Use hello following toosubmit hello job:</span></span>

    ```
    oozie job -config job.xml -submit
    ```

    <span data-ttu-id="194b4-230">Il comando Carica le informazioni sul processo di hello da **job.xml** e lo invia tooOozie, ma non viene eseguito il.</span><span class="sxs-lookup"><span data-stu-id="194b4-230">This command loads hello job information from **job.xml** and submits it tooOozie, but does not run it.</span></span>

    <span data-ttu-id="194b4-231">Al termine del comando hello, dovrebbe restituire hello ID di processo hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-231">Once hello command completes, it should return hello ID of hello job.</span></span> <span data-ttu-id="194b4-232">ad esempio `0000005-150622124850154-oozie-oozi-W`.</span><span class="sxs-lookup"><span data-stu-id="194b4-232">For example, `0000005-150622124850154-oozie-oozi-W`.</span></span> <span data-ttu-id="194b4-233">Questo ID è il processo di hello toomanage utilizzato.</span><span class="sxs-lookup"><span data-stu-id="194b4-233">This ID is used toomanage hello job.</span></span>

4. <span data-ttu-id="194b4-234">Visualizzare lo stato di hello del processo di hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="194b4-234">View hello status of hello job using hello following command:</span></span>

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > <span data-ttu-id="194b4-235">Sostituire `<JOBID>` con hello ID restituito nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-235">Replace `<JOBID>` with hello ID returned in hello previous step.</span></span>

    <span data-ttu-id="194b4-236">Restituisce toohello di informazioni simili seguente testo:</span><span class="sxs-lookup"><span data-stu-id="194b4-236">This returns information similar toohello following text:</span></span>

    ```
    Job ID : 0000005-150622124850154-oozie-oozi-W
    ------------------------------------------------------------------------------------------------------------------------------------
    Workflow Name : useooziewf
    App Path      : wasb:///tutorials/useoozie
    Status        : PREP
    Run           : 0
    User          : USERNAME
    Group         : -
    Created       : 2015-06-22 15:06 GMT
    Started       : -
    Last Modified : 2015-06-22 15:06 GMT
    Ended         : -
    CoordAction ID: -
    ------------------------------------------------------------------------------------------------------------------------------------
    ```

    <span data-ttu-id="194b4-237">Lo stato del processo è `PREP`.</span><span class="sxs-lookup"><span data-stu-id="194b4-237">This job has a status of `PREP`.</span></span> <span data-ttu-id="194b4-238">Questo stato indica che il processo di hello è stato creato, ma non è stato avviato.</span><span class="sxs-lookup"><span data-stu-id="194b4-238">This status indicates that hello job was created, but not started.</span></span>

5. <span data-ttu-id="194b4-239">Utilizzare hello processo hello toostart di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="194b4-239">Use hello following command toostart hello job:</span></span>

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > <span data-ttu-id="194b4-240">Sostituire `<JOBID>` con hello ID restituito in precedenza.</span><span class="sxs-lookup"><span data-stu-id="194b4-240">Replace `<JOBID>` with hello ID returned previously.</span></span>

    <span data-ttu-id="194b4-241">Se si archivia lo stato di hello dopo questo comando, si trova in uno stato di esecuzione e vengono restituite informazioni per le azioni all'interno del processo di hello hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-241">If you check hello status after this command, it is in a running state, and information is returned for hello actions within hello job.</span></span>

6. <span data-ttu-id="194b4-242">Dopo l'attività hello viene completato correttamente, è possibile verificare che i dati di hello è stati generati ed esportavano toohello tabella del Database SQL utilizzando i seguenti comandi hello:</span><span class="sxs-lookup"><span data-stu-id="194b4-242">Once hello task completes successfully, you can verify that hello data was generated and exported toohello SQL Database table by using hello following commands:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="194b4-243">In hello `1>` richiesto, immettere hello seguente query:</span><span class="sxs-lookup"><span data-stu-id="194b4-243">At hello `1>` prompt, enter hello following query:</span></span>

    ```
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="194b4-244">informazioni di Hello restituite sono simile toohello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="194b4-244">hello information returned is similar toohello following text:</span></span>

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

<span data-ttu-id="194b4-245">Per ulteriori informazioni sul comando Oozie hello, vedere [strumento da riga di comando Oozie](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span><span class="sxs-lookup"><span data-stu-id="194b4-245">For more information on hello Oozie command, see [Oozie command-line tool](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span></span>

## <a name="oozie-rest-api"></a><span data-ttu-id="194b4-246">API REST di Oozie</span><span class="sxs-lookup"><span data-stu-id="194b4-246">Oozie REST API</span></span>

<span data-ttu-id="194b4-247">API REST Oozie Hello consente toobuild i propri strumenti che funzionano con Oozie.</span><span class="sxs-lookup"><span data-stu-id="194b4-247">hello Oozie REST API allows you toobuild your own tools that work with Oozie.</span></span> <span data-ttu-id="194b4-248">di seguito Hello sono HDInsight informazioni specifiche sull'utilizzo di API REST Oozie hello:</span><span class="sxs-lookup"><span data-stu-id="194b4-248">hello following are HDInsight specific information about using hello Oozie REST API:</span></span>

* <span data-ttu-id="194b4-249">**URI**: hello API REST sia accessibile dal cluster hello esterno`https://CLUSTERNAME.azurehdinsight.net/oozie`</span><span class="sxs-lookup"><span data-stu-id="194b4-249">**URI**: hello REST API can be accessed from outside hello cluster at `https://CLUSTERNAME.azurehdinsight.net/oozie`</span></span>

* <span data-ttu-id="194b4-250">**Autenticazione**: l'API toohello utilizzando account cluster HTTP hello (amministratore) e la password di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="194b4-250">**Authentication**: Authenticate toohello API using hello cluster HTTP account (admin) and password.</span></span> <span data-ttu-id="194b4-251">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="194b4-251">For example:</span></span>

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

<span data-ttu-id="194b4-252">Per ulteriori informazioni sull'utilizzo delle API REST Oozie hello, vedere [API per servizi Web Oozie](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="194b4-252">For more information on using hello Oozie REST API, see [Oozie Web Services API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

## <a name="oozie-web-ui"></a><span data-ttu-id="194b4-253">Interfaccia utente Web di Oozie</span><span class="sxs-lookup"><span data-stu-id="194b4-253">Oozie Web UI</span></span>

<span data-ttu-id="194b4-254">Hello dell'interfaccia utente Web Oozie fornisce una visualizzazione basata sul web in stato di hello dei processi di Oozie nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-254">hello Oozie Web UI provides a web-based view into hello status of Oozie jobs on hello cluster.</span></span> <span data-ttu-id="194b4-255">interfaccia utente web Hello consente hello tooview le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="194b4-255">hello web UI allows you tooview hello following information:</span></span>

* <span data-ttu-id="194b4-256">Stato processo</span><span class="sxs-lookup"><span data-stu-id="194b4-256">Job status</span></span>
* <span data-ttu-id="194b4-257">Definizione del processo</span><span class="sxs-lookup"><span data-stu-id="194b4-257">Job definition</span></span>
* <span data-ttu-id="194b4-258">Configurazione</span><span class="sxs-lookup"><span data-stu-id="194b4-258">Configuration</span></span>
* <span data-ttu-id="194b4-259">Un grafico di azioni di hello nel processo di hello</span><span class="sxs-lookup"><span data-stu-id="194b4-259">A graph of hello actions in hello job</span></span>
* <span data-ttu-id="194b4-260">Log per il processo di hello</span><span class="sxs-lookup"><span data-stu-id="194b4-260">Logs for hello job</span></span>

<span data-ttu-id="194b4-261">È anche possibile visualizzare i dettagli delle azioni all'interno di un processo.</span><span class="sxs-lookup"><span data-stu-id="194b4-261">You can also view details for actions within a job.</span></span>

<span data-ttu-id="194b4-262">tooaccess hello dell'interfaccia utente Web Oozie, usare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="194b4-262">tooaccess hello Oozie Web UI, use hello following steps:</span></span>

1. <span data-ttu-id="194b4-263">Creare un cluster di HDInsight toohello tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="194b4-263">Create an SSH tunnel toohello HDInsight cluster.</span></span> <span data-ttu-id="194b4-264">Per informazioni, vedere hello [usare SSH Tunneling con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.</span><span class="sxs-lookup"><span data-stu-id="194b4-264">For information, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="194b4-265">Dopo aver creato un tunnel, aprire hello Ambari web dell'interfaccia utente nel web browser.</span><span class="sxs-lookup"><span data-stu-id="194b4-265">Once a tunnel has been created, open hello Ambari web UI in your web browser.</span></span> <span data-ttu-id="194b4-266">Hello URI per il sito Ambari hello è **https://CLUSTERNAME.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="194b4-266">hello URI for hello Ambari site is **https://CLUSTERNAME.azurehdinsight.net**.</span></span> <span data-ttu-id="194b4-267">Sostituire **CLUSTERNAME** con nome hello del cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="194b4-267">Replace **CLUSTERNAME** with hello name of your Linux-based HDInsight cluster.</span></span>

3. <span data-ttu-id="194b4-268">Hello lato della pagina hello sinistro, selezionare **Oozie**, quindi **collegamenti rapidi**e infine **dell'interfaccia utente Web Oozie**.</span><span class="sxs-lookup"><span data-stu-id="194b4-268">From hello left side of hello page, select **Oozie**, then **Quick Links**, and finally **Oozie Web UI**.</span></span>

    ![immagine del menu hello](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. <span data-ttu-id="194b4-270">Hello toodisplaying impostazioni predefinite dell'interfaccia utente Web Oozie processi del flusso di lavoro in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="194b4-270">hello Oozie Web UI defaults toodisplaying running Workflow Jobs.</span></span> <span data-ttu-id="194b4-271">Selezionare tutti i processi del flusso di lavoro, toosee **tutti i processi**.</span><span class="sxs-lookup"><span data-stu-id="194b4-271">toosee all workflow jobs, select **All Jobs**.</span></span>

    ![Tutti i processi visualizzati](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. <span data-ttu-id="194b4-273">Selezionare un processo tooview ulteriori informazioni sul processo hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-273">Select a job tooview more information about hello job.</span></span>

    ![Job Info](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. <span data-ttu-id="194b4-275">Dalla scheda informazioni hello, è possibile visualizzare informazioni sul processo di base e le azioni di singoli hello all'interno del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-275">From hello Job Info tab, you can see basic job information and hello individual actions within hello job.</span></span> <span data-ttu-id="194b4-276">Utilizzo hello delle schede nella parte superiore di hello che è possibile visualizzare hello definizione del processo, la configurazione del processo, hello accesso Log Job o visualizzare indirizzate aciclico Graph (DAG) del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-276">Using hello tabs at hello top you can view hello Job Definition, Job Configuration, access hello Job Log or view a Directed Acyclic Graph (DAG) of hello job.</span></span>

   * <span data-ttu-id="194b4-277">**Processo di Log**: hello seleziona **GetLogs** pulsante tooget tutti i log per il processo di hello o utilizzare hello **filtro di ricerca immettere** campo toofilter log</span><span class="sxs-lookup"><span data-stu-id="194b4-277">**Job Log**: Select hello **GetLogs** button tooget all logs for hello job, or use hello **Enter Search Filter** field toofilter logs</span></span>

       ![Log del processo](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * <span data-ttu-id="194b4-279">**JobDAG**: hello DAG è una rappresentazione grafica dei percorsi di dati hello eseguite tramite flusso di lavoro hello</span><span class="sxs-lookup"><span data-stu-id="194b4-279">**JobDAG**: hello DAG is a graphical overview of hello data paths taken through hello workflow</span></span>

       ![DAG del processo](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. <span data-ttu-id="194b4-281">Selezionando una delle azioni hello hello **informazioni** scheda consente di visualizzare informazioni per l'azione di hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-281">Selecting one of hello actions from hello **Job Info** tab brings up information for hello action.</span></span> <span data-ttu-id="194b4-282">Ad esempio, selezionare hello **RunHiveScript** azione.</span><span class="sxs-lookup"><span data-stu-id="194b4-282">For example, select hello **RunHiveScript** action.</span></span>

    ![Informazioni sull'azione](./media/hdinsight-use-oozie-linux-mac/action.png)

8. <span data-ttu-id="194b4-284">È possibile visualizzare i dettagli per l'azione di hello, ad esempio un collegamento di toohello **URL della Console**.</span><span class="sxs-lookup"><span data-stu-id="194b4-284">You can see details for hello action, such as a link toohello **Console URL**.</span></span> <span data-ttu-id="194b4-285">Questo collegamento può essere utilizzato tooview JobTracker informazioni per il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-285">This link can be used tooview JobTracker information for hello job.</span></span>

## <a name="scheduling-jobs"></a><span data-ttu-id="194b4-286">Pianificazione di processi</span><span class="sxs-lookup"><span data-stu-id="194b4-286">Scheduling jobs</span></span>

<span data-ttu-id="194b4-287">coordinatore Hello consente toospecify una frequenza di occorrenza inizio e fine per i processi.</span><span class="sxs-lookup"><span data-stu-id="194b4-287">hello coordinator allows you toospecify a start, end, and occurrence frequency for jobs.</span></span> <span data-ttu-id="194b4-288">toodefine una pianificazione per flusso di lavoro hello, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="194b4-288">toodefine a schedule for hello workflow, use hello following steps:</span></span>

1. <span data-ttu-id="194b4-289">Hello utilizzare seguente toocreate un file denominato **coordinator.xml**:</span><span class="sxs-lookup"><span data-stu-id="194b4-289">Use hello following toocreate a file named **coordinator.xml**:</span></span>

    ```
    nano coordinator.xml
    ```

    <span data-ttu-id="194b4-290">Utilizzare hello seguente XML come contenuto di hello del file hello:</span><span class="sxs-lookup"><span data-stu-id="194b4-290">Use hello following XML as hello contents of hello file:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
        <workflow>
            <app-path>${workflowPath}</app-path>
        </workflow>
        </action>
    </coordinator-app>
    ```

    > [!NOTE]
    > <span data-ttu-id="194b4-291">Hello `${...}` variabili vengono sostituite dai valori nella definizione di processo hello in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="194b4-291">hello `${...}` variables are replaced by values in hello job definition at run-time.</span></span> <span data-ttu-id="194b4-292">le variabili di Hello sono:</span><span class="sxs-lookup"><span data-stu-id="194b4-292">hello variables are:</span></span>
    >
    > * <span data-ttu-id="194b4-293">`${coordFrequency}`: Il tempo tra l'esecuzione di istanze del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-293">`${coordFrequency}`: Time between running instances of hello job.</span></span>
    > <span data-ttu-id="194b4-294">** `${coordStart}`: ora di inizio processo hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-294">** `${coordStart}`: hello job start time.</span></span>
    > * <span data-ttu-id="194b4-295">`${coordEnd}`: ora di fine processo hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-295">`${coordEnd}`: hello job end time.</span></span>
    > * <span data-ttu-id="194b4-296">`${coordTimezone}`: i processi del coordinatore si trovano in un fuso orario predefinito che non tiene conto dell'ora legale (in genere rappresentato dall'acronimo UTC).</span><span class="sxs-lookup"><span data-stu-id="194b4-296">`${coordTimezone}`: Coordinator jobs are in a fixed time zone with no daylight savings time (typically represented by using UTC).</span></span> <span data-ttu-id="194b4-297">Il fuso orario viene definito come hello "Oozie elaborazione fuso orario."</span><span class="sxs-lookup"><span data-stu-id="194b4-297">This time zone is referred as hello "Oozie processing timezone."</span></span>
    > * <span data-ttu-id="194b4-298">`${wfPath}`: hello percorso toohello workflow.</span><span class="sxs-lookup"><span data-stu-id="194b4-298">`${wfPath}`: hello path toohello workflow.xml.</span></span>

2. <span data-ttu-id="194b4-299">hello toosave, utilizzare Ctrl + X, **Y**, e **invio**.</span><span class="sxs-lookup"><span data-stu-id="194b4-299">toosave hello file, use Ctrl-X, **Y**, and **Enter**.</span></span>

3. <span data-ttu-id="194b4-300">Utilizzare hello comando toocopy hello toohello working directory del file per il processo seguente:</span><span class="sxs-lookup"><span data-stu-id="194b4-300">Use hello following command toocopy hello file toohello working directory for this job:</span></span>

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. <span data-ttu-id="194b4-301">Hello utilizzare seguente hello toomodify **job.xml** file:</span><span class="sxs-lookup"><span data-stu-id="194b4-301">Use hello following toomodify hello **job.xml** file:</span></span>

    ```
    nano job.xml
    ```

    <span data-ttu-id="194b4-302">Apportare hello seguenti modifiche:</span><span class="sxs-lookup"><span data-stu-id="194b4-302">Make hello following changes:</span></span>

   * <span data-ttu-id="194b4-303">il file tooinstruct oozie toorun hello coordinator anziché hello flusso di lavoro modifica `<name>oozie.wf.application.path</name>` troppo`<name>oozie.coord.application.path</name>`.</span><span class="sxs-lookup"><span data-stu-id="194b4-303">tooinstruct oozie toorun hello coordinator file instead of hello workflow, change `<name>oozie.wf.application.path</name>` too`<name>oozie.coord.application.path</name>`.</span></span>

   * <span data-ttu-id="194b4-304">hello tooset `workflowPath` variabile utilizzata dal coordinatore hello, aggiungere hello XML seguente:</span><span class="sxs-lookup"><span data-stu-id="194b4-304">tooset hello `workflowPath` variable used by hello coordinator, add hello following XML:</span></span>

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       <span data-ttu-id="194b4-305">Sostituire hello `wasb://mycontainer@mystorageaccount.blob.core.windows` testo con il valore di hello utilizzato in altre voci nel file job.xml hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-305">Replace hello `wasb://mycontainer@mystorageaccount.blob.core.windows` text with hello value used in other entries in hello job.xml file.</span></span>

   * <span data-ttu-id="194b4-306">inizio hello toodefine, fine e la frequenza per coordinator hello, aggiungere hello XML seguente:</span><span class="sxs-lookup"><span data-stu-id="194b4-306">toodefine hello start, end, and frequency for hello coordinator, add hello following XML:</span></span>

        ```xml
        <property>
            <name>coordStart</name>
            <value>2017-05-10T12:00Z</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>2017-05-12T12:00Z</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>1440</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>UTC</value>
        </property>
        ```

       <span data-ttu-id="194b4-307">Questi valori impostati too12 ora di inizio hello: 00 PM del 10 maggio 2017, hello tooMay ora fine 12, 2017.</span><span class="sxs-lookup"><span data-stu-id="194b4-307">These values set hello start time too12:00PM on May 10, 2017, hello end time tooMay 12, 2017.</span></span> <span data-ttu-id="194b4-308">intervallo di Hello per l'esecuzione del processo ogni giorno.</span><span class="sxs-lookup"><span data-stu-id="194b4-308">hello interval for running this job daily.</span></span> <span data-ttu-id="194b4-309">frequenza di Hello è espresso in minuti, quindi 24 ore x 60 minuti = 1440 minuti.</span><span class="sxs-lookup"><span data-stu-id="194b4-309">hello frequency is in minutes, so 24 hours x 60 minutes = 1440 minutes.</span></span> <span data-ttu-id="194b4-310">Infine, fuso orario di hello è impostato tooUTC.</span><span class="sxs-lookup"><span data-stu-id="194b4-310">Finally, hello timezone is set tooUTC.</span></span>

5. <span data-ttu-id="194b4-311">Utilizzare Ctrl + X, quindi **Y** e **invio** file hello toosave.</span><span class="sxs-lookup"><span data-stu-id="194b4-311">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

6. <span data-ttu-id="194b4-312">processo di hello toorun, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="194b4-312">toorun hello job, use hello following command:</span></span>

    ```
    oozie job -config job.xml -run
    ```

    <span data-ttu-id="194b4-313">Questo comando Invia e avvia il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-313">This command submits and starts hello job.</span></span>

7. <span data-ttu-id="194b4-314">Se si visita dell'interfaccia utente Web Oozie hello e selezionare hello **processi coordinatore** scheda, viene visualizzato toohello di informazioni simili seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="194b4-314">If you visit hello Oozie Web UI and select hello **Coordinator Jobs** tab, you see information similar toohello following image:</span></span>

    ![scheda coordinator jobs](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    <span data-ttu-id="194b4-316">Hello **materializzazione Avanti** voce contiene hello successivo hello esecuzione del processo.</span><span class="sxs-lookup"><span data-stu-id="194b4-316">hello **Next Materialization** entry contains hello next time that hello job runs.</span></span>

8. <span data-ttu-id="194b4-317">Toohello simile precedente processo di flusso di lavoro, selezionando la voce di processi hello nell'interfaccia utente web hello Visualizza le informazioni sul processo hello:</span><span class="sxs-lookup"><span data-stu-id="194b4-317">Similar toohello earlier workflow job, selecting hello job entry in hello web UI displays information on hello job:</span></span>

    ![Informazioni sui processi coordinatore](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > <span data-ttu-id="194b4-319">Questa immagine Mostra solo l'esecuzione ha esito positivo del processo di hello, non singole azioni all'interno del flusso di lavoro hello pianificata.</span><span class="sxs-lookup"><span data-stu-id="194b4-319">This image only shows successful runs of hello job, not individual actions within hello scheduled workflow.</span></span> <span data-ttu-id="194b4-320">toosee che, selezionare una delle hello **azione** voci.</span><span class="sxs-lookup"><span data-stu-id="194b4-320">toosee that, select one of hello **Action** entries.</span></span>

    ![Informazioni sull'azione](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a><span data-ttu-id="194b4-322">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="194b4-322">Troubleshooting</span></span>

<span data-ttu-id="194b4-323">Hello Oozie UI consente tooview Oozie log.</span><span class="sxs-lookup"><span data-stu-id="194b4-323">hello Oozie UI allows you tooview Oozie logs.</span></span> <span data-ttu-id="194b4-324">Contiene inoltre i registri tooJobTracker collegamenti per l'attività MapReduce avviate dal flusso di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-324">It also contains links tooJobTracker logs for MapReduce tasks started by hello workflow.</span></span> <span data-ttu-id="194b4-325">deve essere modello Hello per la risoluzione dei problemi:</span><span class="sxs-lookup"><span data-stu-id="194b4-325">hello pattern for troubleshooting should be:</span></span>

1. <span data-ttu-id="194b4-326">Visualizza processo hello nell'interfaccia utente Web Oozie.</span><span class="sxs-lookup"><span data-stu-id="194b4-326">View hello job in Oozie Web UI.</span></span>

2. <span data-ttu-id="194b4-327">Se è presente un errore per un'azione specifica, selezionare hello toosee azione se hello **messaggio di errore** campo fornisce altre informazioni sull'errore hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-327">If there is an error or failure for a specific action, select hello action toosee if hello **Error Message** field provides more information on hello failure.</span></span>

3. <span data-ttu-id="194b4-328">Se disponibile, utilizzare URL hello da hello azione tooview ulteriori dettagli (ad esempio, i log JobTracker) per l'azione di hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-328">If available, use hello URL from hello action tooview more details (such as JobTracker logs) for hello action.</span></span>

<span data-ttu-id="194b4-329">di seguito Hello sono specifici errori che possono verificarsi, e come tooresolve li.</span><span class="sxs-lookup"><span data-stu-id="194b4-329">hello following are specific errors you may encounter, and how tooresolve them.</span></span>

### <a name="ja009-cannot-initialize-cluster"></a><span data-ttu-id="194b4-330">JA009: Cannot initialize cluster</span><span class="sxs-lookup"><span data-stu-id="194b4-330">JA009: Cannot initialize cluster</span></span>

<span data-ttu-id="194b4-331">**Sintomi**: hello modifiche dello stato di processo troppo**SUSPENDED**.</span><span class="sxs-lookup"><span data-stu-id="194b4-331">**Symptoms**: hello job status changes too**SUSPENDED**.</span></span> <span data-ttu-id="194b4-332">Dettagli per il processo di hello mostrano lo stato di RunHiveScript hello come **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="194b4-332">Details for hello job show hello RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="194b4-333">Selezionando l'azione di hello Visualizza hello seguente messaggio di errore:</span><span class="sxs-lookup"><span data-stu-id="194b4-333">Selecting hello action displays hello following error message:</span></span>

    JA009: Cannot initialize Cluster. Please check your configuration for map

<span data-ttu-id="194b4-334">**Causa**: hello indirizzi WASB utilizzati in hello **job.xml** file non contengono il contenitore di archiviazione hello o nome account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="194b4-334">**Cause**: hello WASB addresses used in hello **job.xml** file do not contain hello storage container or storage account name.</span></span> <span data-ttu-id="194b4-335">formato dell'indirizzo WASB Hello deve essere `wasb://containername@storageaccountname.blob.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="194b4-335">hello WASB address format must be `wasb://containername@storageaccountname.blob.core.windows.net`.</span></span>

<span data-ttu-id="194b4-336">**Risoluzione**: modificare gli indirizzi WASB hello utilizzati dal processo hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-336">**Resolution**: Change hello WASB addresses used by hello job.</span></span>

### <a name="ja002-oozie-is-not-allowed-tooimpersonate-ltuser"></a><span data-ttu-id="194b4-337">JA002: Oozie non è consentito tooimpersonate &lt;utente ></span><span class="sxs-lookup"><span data-stu-id="194b4-337">JA002: Oozie is not allowed tooimpersonate &lt;USER></span></span>

<span data-ttu-id="194b4-338">**Sintomi**: hello modifiche dello stato di processo troppo**SUSPENDED**.</span><span class="sxs-lookup"><span data-stu-id="194b4-338">**Symptoms**: hello job status changes too**SUSPENDED**.</span></span> <span data-ttu-id="194b4-339">Dettagli per il processo di hello mostrano lo stato di RunHiveScript hello come **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="194b4-339">Details for hello job show hello RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="194b4-340">Selezionare l'azione hello visualizzare hello seguente messaggio di errore:</span><span class="sxs-lookup"><span data-stu-id="194b4-340">Selecting hello action shows hello following error message:</span></span>

    JA002: User: oozie is not allowed tooimpersonate <USER>

<span data-ttu-id="194b4-341">**Causa**: impostazioni di autorizzazione correnti non consentono Oozie hello tooimpersonate l'account utente specificato.</span><span class="sxs-lookup"><span data-stu-id="194b4-341">**Cause**: Current permission settings do not allow Oozie tooimpersonate hello specified user account.</span></span>

<span data-ttu-id="194b4-342">**Risoluzione**: Oozie è consentito agli utenti di tooimpersonate in hello **utenti** gruppo.</span><span class="sxs-lookup"><span data-stu-id="194b4-342">**Resolution**: Oozie is allowed tooimpersonate users in hello **users** group.</span></span> <span data-ttu-id="194b4-343">Hello utilizzare `groups USERNAME` gruppi hello toosee hello account utente è membro.</span><span class="sxs-lookup"><span data-stu-id="194b4-343">Use hello `groups USERNAME` toosee hello groups that hello user account is a member of.</span></span> <span data-ttu-id="194b4-344">Se l'utente hello non è un membro di hello **utenti** gruppo, utilizzare hello gruppo toohello utente hello tooadd dei comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="194b4-344">If hello user is not a member of hello **users** group, use hello following command tooadd hello user toohello group:</span></span>

    sudo adduser USERNAME users

> [!NOTE]
> <span data-ttu-id="194b4-345">Potrebbe richiedere alcuni minuti prima di HDInsight riconosce che l'utente hello è stato aggiunto a un gruppo toohello.</span><span class="sxs-lookup"><span data-stu-id="194b4-345">It may take several minutes before HDInsight recognizes that hello user has been added toohello group.</span></span>

### <a name="launcher-error-sqoop"></a><span data-ttu-id="194b4-346">ERRORE dell'utilità di avvio (Sqoop)</span><span class="sxs-lookup"><span data-stu-id="194b4-346">Launcher ERROR (Sqoop)</span></span>

<span data-ttu-id="194b4-347">**Sintomi**: hello modifiche dello stato di processo troppo**KILLED**.</span><span class="sxs-lookup"><span data-stu-id="194b4-347">**Symptoms**: hello job status changes too**KILLED**.</span></span> <span data-ttu-id="194b4-348">Dettagli per il processo di hello mostrano lo stato di RunSqoopExport hello come **errore**.</span><span class="sxs-lookup"><span data-stu-id="194b4-348">Details for hello job show hello RunSqoopExport status as **ERROR**.</span></span> <span data-ttu-id="194b4-349">Selezionare l'azione hello visualizzare hello seguente messaggio di errore:</span><span class="sxs-lookup"><span data-stu-id="194b4-349">Selecting hello action shows hello following error message:</span></span>

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

<span data-ttu-id="194b4-350">**Causa**: Sqoop è Impossibile tooload hello driver necessari tooaccess hello di database.</span><span class="sxs-lookup"><span data-stu-id="194b4-350">**Cause**: Sqoop is unable tooload hello database driver required tooaccess hello database.</span></span>

<span data-ttu-id="194b4-351">**Risoluzione**: quando si utilizza Sqoop da un processo Oozie, è necessario includere i driver di database hello con hello altre risorse (ad esempio workflow hello) utilizzate dal processo hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-351">**Resolution**: When using Sqoop from an Oozie job, you must include hello database driver with hello other resources (such as hello workflow.xml) used by hello job.</span></span> <span data-ttu-id="194b4-352">Fare riferimento anche archivio hello contenente i driver di database hello da hello `<sqoop>...</sqoop>` sezione workflow hello.</span><span class="sxs-lookup"><span data-stu-id="194b4-352">Also Reference hello archive containing hello database driver from hello `<sqoop>...</sqoop>` section of hello workflow.xml.</span></span>

<span data-ttu-id="194b4-353">Ad esempio, per il processo di hello in questo documento, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="194b4-353">For example, for hello job in this document, you would use hello following steps:</span></span>

1. <span data-ttu-id="194b4-354">Copia hello sqljdbc4.1.jar toohello /tutorials/useoozie directory del file:</span><span class="sxs-lookup"><span data-stu-id="194b4-354">Copy hello sqljdbc4.1.jar file toohello /tutorials/useoozie directory:</span></span>

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. <span data-ttu-id="194b4-355">Modificare hello tooadd di workflow hello seguente XML in una nuova riga sopra `</sqoop>`:</span><span class="sxs-lookup"><span data-stu-id="194b4-355">Modify hello workflow.xml tooadd hello following XML on a new line above `</sqoop>`:</span></span>

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a><span data-ttu-id="194b4-356">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="194b4-356">Next steps</span></span>

<span data-ttu-id="194b4-357">In questa esercitazione, si è appreso come un flusso di lavoro Oozie toodefine e come toorun un processo di Oozie.</span><span class="sxs-lookup"><span data-stu-id="194b4-357">In this tutorial, you learned how toodefine an Oozie workflow and how toorun an Oozie job.</span></span> <span data-ttu-id="194b4-358">toolearn più informazioni sull'utilizzo di HDInsight, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="194b4-358">toolearn more about working with HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="194b4-359">[Usare il coordinatore Oozie basato sul tempo con HDInsight][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="194b4-359">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="194b4-360">[Caricare dati per processi Hadoop in HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="194b4-360">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="194b4-361">[Usare Sqoop con Hadoop in HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="194b4-361">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="194b4-362">[Usare Hive con Hadoop in HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="194b4-362">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="194b4-363">[Usare Pig con Hadoop in HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="194b4-363">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="194b4-364">[Sviluppare programmi MapReduce Java per HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="194b4-364">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563
[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started]: hdinsight-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started-emulator]: hdinsight-get-started-emulator.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: sql-database-create-configure.md
[sqldatabase-get-started]: sql-database-get-started.md

[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: https://technet.microsoft.com/en-us/library/ee176961.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.RunWF.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
