---
title: Usare i flussi di lavoro Oozie di Hadoop in HDInsight basati su Linux | Microsoft Docs
description: Usare Oozie di Hadoop in HDInsight basati su Linux. Informazioni su come definire un flusso di lavoro di Oozie e inviare un processo Oozie.
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
ms.openlocfilehash: e3206078e451aefe02689bfb61ce22a20dd0fa70
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-oozie-with-hadoop-to-define-and-run-a-workflow-on-linux-based-hdinsight"></a><span data-ttu-id="2a681-104">Usare Oozie con Hadoop per definire ed eseguire un flusso di lavoro in HDInsight basato su Linux</span><span class="sxs-lookup"><span data-stu-id="2a681-104">Use Oozie with Hadoop to define and run a workflow on Linux-based HDInsight</span></span>

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="2a681-105">Informazioni su come usare Apache Oozie con Hadoop in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a681-105">Learn how to use Apache Oozie with Hadoop on HDInsight.</span></span> <span data-ttu-id="2a681-106">Apache Oozie è un sistema di flusso di lavoro/coordinamento che consente di gestire i processi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2a681-106">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="2a681-107">Oozie è integrato con lo stack Hadoop e supporta i processi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a681-107">Oozie is integrated with the Hadoop stack, and it supports the following jobs:</span></span>

* <span data-ttu-id="2a681-108">Apache MapReduce</span><span class="sxs-lookup"><span data-stu-id="2a681-108">Apache MapReduce</span></span>
* <span data-ttu-id="2a681-109">Apache Pig</span><span class="sxs-lookup"><span data-stu-id="2a681-109">Apache Pig</span></span>
* <span data-ttu-id="2a681-110">Apache Hive</span><span class="sxs-lookup"><span data-stu-id="2a681-110">Apache Hive</span></span>
* <span data-ttu-id="2a681-111">Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="2a681-111">Apache Sqoop</span></span>

<span data-ttu-id="2a681-112">Oozie può anche essere usato per pianificare processi specifici di un sistema, come i programmi Java o gli script della shell</span><span class="sxs-lookup"><span data-stu-id="2a681-112">Oozie can also be used to schedule jobs that are specific to a system, like Java programs or shell scripts</span></span>

> [!NOTE]
> <span data-ttu-id="2a681-113">Un'altra opzione per definire i flussi di lavoro con HDInsight è Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2a681-113">Another option for defining workflows with HDInsight is Azure Data Factory.</span></span> <span data-ttu-id="2a681-114">Per altre informazioni su Azure Data Factory, vedere [Usare Pig e Hive con Data Factory][azure-data-factory-pig-hive].</span><span class="sxs-lookup"><span data-stu-id="2a681-114">To learn more about Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2a681-115">Oozie non è abilitato su HDInsight appartenente al dominio.</span><span class="sxs-lookup"><span data-stu-id="2a681-115">Oozie is not enabled on domain-joined HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a681-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2a681-116">Prerequisites</span></span>

* <span data-ttu-id="2a681-117">**Un cluster di HDInsight**: vedere [Introduzione a HDInsight in Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="2a681-117">**An HDInsight cluster**: See [Get Started with HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="2a681-118">I passaggi descritti in questo documento richiedono un cluster HDInsight che usa Linux.</span><span class="sxs-lookup"><span data-stu-id="2a681-118">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="2a681-119">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="2a681-119">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2a681-120">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="2a681-120">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="example-workflow"></a><span data-ttu-id="2a681-121">Esempio di flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="2a681-121">Example workflow</span></span>

<span data-ttu-id="2a681-122">Il flusso di lavoro usato in questo documento prevede due azioni.</span><span class="sxs-lookup"><span data-stu-id="2a681-122">The workflow used in this document contains two actions.</span></span> <span data-ttu-id="2a681-123">Le azioni sono definizioni per attività, ad esempio l'esecuzione di Hive, Sqoop, MapReduce o altri processi:</span><span class="sxs-lookup"><span data-stu-id="2a681-123">Actions are definitions for tasks, such as running Hive, Sqoop, MapReduce, or other process:</span></span>

![Diagramma del flusso di lavoro][img-workflow-diagram]

1. <span data-ttu-id="2a681-125">Un'azione di Hive esegue uno script HiveQL per estrarre i record da **hivesampletable** inclusa in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a681-125">A Hive action runs a HiveQL script to extract records from the **hivesampletable** included with HDInsight.</span></span> <span data-ttu-id="2a681-126">Ogni riga di dati descrive una visita da un dispositivo mobile specifico.</span><span class="sxs-lookup"><span data-stu-id="2a681-126">Each row of data describes a visit from a specific mobile device.</span></span> <span data-ttu-id="2a681-127">Il formato del record risulterà simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="2a681-127">The record format appears similar to the following text:</span></span>

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    <span data-ttu-id="2a681-128">Lo script Hive usato in questo documento conta le visite totali per ogni piattaforma (ad esempio Android o iPhone) e archivia i conteggi in una nuova tabella Hive.</span><span class="sxs-lookup"><span data-stu-id="2a681-128">The Hive script used in this document counts the total visits for each platform (such as Android or iPhone) and stores the counts to a new Hive table.</span></span>

    <span data-ttu-id="2a681-129">Per altre informazioni su Hive, vedere [Usare Hive con HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="2a681-129">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

2. <span data-ttu-id="2a681-130">Un'azione di Sqoop esporta il contenuto della nuova tabella Hive in una tabella di un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a681-130">A Sqoop action exports the contents of the new Hive table to a table in an Azure SQL database.</span></span> <span data-ttu-id="2a681-131">Per altre informazioni su Sqoop, vedere [Usare Sqoop con Hadoop in HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="2a681-131">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="2a681-132">Per informazioni sulle versioni di Oozie supportate nei cluster HDInsight, vedere [Novità delle versioni cluster di Hadoop incluse in HDInsight][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="2a681-132">For supported Oozie versions on HDInsight clusters, see [What's new in the Hadoop cluster versions provided by HDInsight][hdinsight-versions].</span></span>

## <a name="create-the-working-directory"></a><span data-ttu-id="2a681-133">Creare la directory di lavoro</span><span class="sxs-lookup"><span data-stu-id="2a681-133">Create the working directory</span></span>

<span data-ttu-id="2a681-134">Oozie prevede che le risorse necessarie per un processo siano archiviate nella stessa directory.</span><span class="sxs-lookup"><span data-stu-id="2a681-134">Oozie expects resources required for a job to be stored in the same directory.</span></span> <span data-ttu-id="2a681-135">Questo esempio usa **wasb:///tutorials/useoozie**.</span><span class="sxs-lookup"><span data-stu-id="2a681-135">This example uses **wasb:///tutorials/useoozie**.</span></span> <span data-ttu-id="2a681-136">Usare il comando seguente per creare questa directory e la directory dati che contiene la nuova tabella Hive creata da questo flusso di lavoro:</span><span class="sxs-lookup"><span data-stu-id="2a681-136">Use the following command to create this directory, and the data directory that holds the new Hive table created by this workflow:</span></span>

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> <span data-ttu-id="2a681-137">Il parametro `-p` provoca la creazione di tutte le directory nel percorso.</span><span class="sxs-lookup"><span data-stu-id="2a681-137">The `-p` parameter causes all directories in the path to be created.</span></span> <span data-ttu-id="2a681-138">La directory **data** viene usata per contenere i dati usati dallo script **useooziewf.hql**.</span><span class="sxs-lookup"><span data-stu-id="2a681-138">The **data** directory is used to hold data used by the **useooziewf.hql** script.</span></span>

<span data-ttu-id="2a681-139">Eseguire anche il comando seguente, per assicurare che Oozie possa rappresentare l'account utente durante l'esecuzione di processi Hive e Sqoop.</span><span class="sxs-lookup"><span data-stu-id="2a681-139">Also run the following command, which ensures that Oozie can impersonate your user account when running Hive and Sqoop jobs.</span></span> <span data-ttu-id="2a681-140">Sostituire **USERNAME** con il proprio nome di accesso:</span><span class="sxs-lookup"><span data-stu-id="2a681-140">Replace **USERNAME** with your login name:</span></span>

```
sudo adduser USERNAME users
```

> [!NOTE]
> <span data-ttu-id="2a681-141">È possibile ignorare gli errori che indicano che l'utente è già un membro del gruppo `users`.</span><span class="sxs-lookup"><span data-stu-id="2a681-141">You can ignore errors that the user is already a member of the `users` group.</span></span>

## <a name="add-a-database-driver"></a><span data-ttu-id="2a681-142">Aggiungere un driver di database</span><span class="sxs-lookup"><span data-stu-id="2a681-142">Add a database driver</span></span>

<span data-ttu-id="2a681-143">Poiché questo flusso di lavoro usa Sqoop per esportare dati nel database SQL, è necessario fornire una copia del driver JDBC usato per comunicare con il database SQL.</span><span class="sxs-lookup"><span data-stu-id="2a681-143">Since this workflow uses Sqoop to export data to SQL Database, you must provide a copy of the JDBC driver used to talk to SQL Database.</span></span> <span data-ttu-id="2a681-144">Usare il comando seguente per copiarlo nella directory di lavoro:</span><span class="sxs-lookup"><span data-stu-id="2a681-144">Use the following command to copy it to the working directory:</span></span>

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

<span data-ttu-id="2a681-145">Se il flusso di lavoro usa altre risorse, ad esempio un file JAR contenente un'applicazione MapReduce, è necessario aggiungere anche queste risorse.</span><span class="sxs-lookup"><span data-stu-id="2a681-145">If your workflow used other resources, such as a jar containing a MapReduce application, you would need to add these resources as well.</span></span>

## <a name="define-the-hive-query"></a><span data-ttu-id="2a681-146">Definire la query Hive</span><span class="sxs-lookup"><span data-stu-id="2a681-146">Define the Hive query</span></span>

<span data-ttu-id="2a681-147">Usare i passaggi seguenti per creare uno script HiveQL che definisce la query usata in un flusso di lavoro di Oozie, più avanti in questo documento.</span><span class="sxs-lookup"><span data-stu-id="2a681-147">Use the following steps to create a HiveQL script that defines a query, which is used in an Oozie workflow later in this document.</span></span>

1. <span data-ttu-id="2a681-148">Connettersi al cluster tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="2a681-148">Connect to the cluster using SSH.</span></span> <span data-ttu-id="2a681-149">Il seguente è un esempio di utilizzo del comando `ssh`.</span><span class="sxs-lookup"><span data-stu-id="2a681-149">The following command is an example of using the `ssh` command.</span></span> <span data-ttu-id="2a681-150">Sostituire __USERNAME__ con il nome utente SSH del cluster.</span><span class="sxs-lookup"><span data-stu-id="2a681-150">Replace __USERNAME__ with the SSH user for the cluster.</span></span> <span data-ttu-id="2a681-151">Sostituire __CLUSTERNAME__ con il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a681-151">Replace __CLUSTERNAME__ with the name of the HDInsight cluster.</span></span>

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="2a681-152">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2a681-152">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="2a681-153">Dalla connessione SSH, usare il comando seguente per creare un file:</span><span class="sxs-lookup"><span data-stu-id="2a681-153">From the SSH connection, use the following command to create a file:</span></span>

    ```
    nano useooziewf.hql
    ```

3. <span data-ttu-id="2a681-154">All'apertura dell'editor nano, usare la query seguente come contenuto del file:</span><span class="sxs-lookup"><span data-stu-id="2a681-154">Once the nano editor opens, use the following query as the contents of the file:</span></span>

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    <span data-ttu-id="2a681-155">Nello script vengono usate due variabili:</span><span class="sxs-lookup"><span data-stu-id="2a681-155">There are two variables used in the script:</span></span>

    * <span data-ttu-id="2a681-156">**${hiveTableName}**: contiene il nome della tabella da creare.</span><span class="sxs-lookup"><span data-stu-id="2a681-156">**${hiveTableName}**: contains the name of the table to be created</span></span>

    * <span data-ttu-id="2a681-157">**${hiveDataFolder}**: contiene il percorso in cui archiviare i file di dati per la tabella.</span><span class="sxs-lookup"><span data-stu-id="2a681-157">**${hiveDataFolder}**: contains the location to store the data files for the table</span></span>

    <span data-ttu-id="2a681-158">Il file di definizione del flusso di lavoro (workflow.xml in questa esercitazione) passa questi valori allo script HiveQL in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2a681-158">The workflow definition file (workflow.xml in this tutorial) passes these values to this HiveQL script at run time</span></span>

4. <span data-ttu-id="2a681-159">Per uscire dall'editor, premere CTRL-X.</span><span class="sxs-lookup"><span data-stu-id="2a681-159">To exit the editor, press Ctrl-X.</span></span> <span data-ttu-id="2a681-160">Quando richiesto, selezionare **S** per salvare il file, quindi premere **INVIO** per usare il nome di file **useooziewf.hql**.</span><span class="sxs-lookup"><span data-stu-id="2a681-160">When prompted, select **Y** to save the file, then use **Enter** to use the **useooziewf.hql** file name.</span></span>

5. <span data-ttu-id="2a681-161">Usare i comandi seguenti per copiare **useooziewf.hql** in **wasb:///tutorials/useoozie/useooziewf.hql**:</span><span class="sxs-lookup"><span data-stu-id="2a681-161">Use the following commands to copy **useooziewf.hql** to **wasb:///tutorials/useoozie/useooziewf.hql**:</span></span>

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    <span data-ttu-id="2a681-162">Questi comandi archiviano il file **useooziewf.hql** nella risorsa di archiviazione compatibile con HDFS per il cluster.</span><span class="sxs-lookup"><span data-stu-id="2a681-162">These commands store the **useooziewf.hql** file on the HDFS-compatible storage for the cluster.</span></span>

## <a name="define-the-workflow"></a><span data-ttu-id="2a681-163">Definire il flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="2a681-163">Define the workflow</span></span>

<span data-ttu-id="2a681-164">Le definizioni dei flussi di lavoro di Oozie sono scritte in linguaggio hPDL (XML Process Definition Language).</span><span class="sxs-lookup"><span data-stu-id="2a681-164">Oozie workflows definitions are written in hPDL (an XML Process Definition Language).</span></span> <span data-ttu-id="2a681-165">Usare i passaggi seguenti per definire il flusso di lavoro:</span><span class="sxs-lookup"><span data-stu-id="2a681-165">Use the following steps to define the workflow:</span></span>

1. <span data-ttu-id="2a681-166">Usare l'istruzione seguente per creare e modificare un nuovo file:</span><span class="sxs-lookup"><span data-stu-id="2a681-166">Use the following statement to create and edit a new file:</span></span>

    ```
    nano workflow.xml
    ```

2. <span data-ttu-id="2a681-167">All'apertura dell'editor nano, immettere il codice XML seguente come contenuto del file:</span><span class="sxs-lookup"><span data-stu-id="2a681-167">Once the nano editor opens, enter the following XML as the file contents:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start to = "RunHiveScript"/>
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

    <span data-ttu-id="2a681-168">Nel flusso di lavoro vengono definite due azioni:</span><span class="sxs-lookup"><span data-stu-id="2a681-168">There are two actions defined in the workflow:</span></span>

   * <span data-ttu-id="2a681-169">**RunHiveScript**: questa azione è l'azione di avvio ed esegue lo script **useooziewf.hql** di Hive.</span><span class="sxs-lookup"><span data-stu-id="2a681-169">**RunHiveScript**: This action is the start action, and runs the **useooziewf.hql** Hive script</span></span>

   * <span data-ttu-id="2a681-170">**RunSqoopExport**: questa azione esporta i dati creati dallo script Hive nel database SQL tramite Sqoop.</span><span class="sxs-lookup"><span data-stu-id="2a681-170">**RunSqoopExport**: This action exports the data created from the Hive script to SQL Database using Sqoop.</span></span> <span data-ttu-id="2a681-171">Questa azione viene eseguita solo se l'azione **RunHiveScript** ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="2a681-171">This action only runs if the **RunHiveScript** action is successful.</span></span>

     <span data-ttu-id="2a681-172">Il flusso di lavoro include molte voci, ad esempio `${jobTracker}`.</span><span class="sxs-lookup"><span data-stu-id="2a681-172">The workflow has several entries, such as `${jobTracker}`.</span></span> <span data-ttu-id="2a681-173">Queste voci vengono sostituite dai valori usati nella definizione del processo,</span><span class="sxs-lookup"><span data-stu-id="2a681-173">These entries are replaced by values you use in the job definition.</span></span> <span data-ttu-id="2a681-174">che viene creata più avanti in questo documento.</span><span class="sxs-lookup"><span data-stu-id="2a681-174">The job definition is created later in this document.</span></span>

     <span data-ttu-id="2a681-175">Notare anche la voce `<archive>sqljdbc4.jar</arcive>` nella sezione Sqoop.</span><span class="sxs-lookup"><span data-stu-id="2a681-175">Also note the `<archive>sqljdbc4.jar</arcive>` entry in the Sqoop section.</span></span> <span data-ttu-id="2a681-176">Questa voce indica a Oozie di rendere disponibile questo archivio per Sqoop quando l'azione viene eseguita.</span><span class="sxs-lookup"><span data-stu-id="2a681-176">This entry instructs Oozie to make this archive available for Sqoop when this action runs.</span></span>

3. <span data-ttu-id="2a681-177">Usare CTRL+X, quindi **S** e **INVIO** per salvare il file.</span><span class="sxs-lookup"><span data-stu-id="2a681-177">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

4. <span data-ttu-id="2a681-178">Usare il comando seguente per copiare il file **workflow.xml** in **wasbs:///tutorials/useoozie/workflow.xml**:</span><span class="sxs-lookup"><span data-stu-id="2a681-178">Use the following command to copy the **workflow.xml** file to **/tutorials/useoozie/workflow.xml**:</span></span>

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-the-database"></a><span data-ttu-id="2a681-179">Creare il database</span><span class="sxs-lookup"><span data-stu-id="2a681-179">Create the database</span></span>

<span data-ttu-id="2a681-180">Per creare un database SQL di Azure, seguire la procedura illustrata nel documento [Creare un database SQL](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2a681-180">To create an Azure SQL Database, follow the steps in the [Create a SQL Database](../sql-database/sql-database-get-started.md) document.</span></span> <span data-ttu-id="2a681-181">Quando si crea il database, usare `oozietest` come nome del database.</span><span class="sxs-lookup"><span data-stu-id="2a681-181">When creating the database, use `oozietest` as the database name.</span></span> <span data-ttu-id="2a681-182">Annotare anche il nome del server di database.</span><span class="sxs-lookup"><span data-stu-id="2a681-182">Also make a note of the name of the database server.</span></span>

### <a name="create-the-table"></a><span data-ttu-id="2a681-183">Creare la tabella</span><span class="sxs-lookup"><span data-stu-id="2a681-183">Create the table</span></span>

> [!NOTE]
> <span data-ttu-id="2a681-184">Sono disponibili diversi modi per connettersi al database SQL per creare una tabella.</span><span class="sxs-lookup"><span data-stu-id="2a681-184">There are many ways to connect to SQL Database to create a table.</span></span> <span data-ttu-id="2a681-185">Nei seguenti passaggi viene usato [FreeTDS](http://www.freetds.org/) dal cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a681-185">The following steps use [FreeTDS](http://www.freetds.org/) from the HDInsight cluster.</span></span>


1. <span data-ttu-id="2a681-186">Usare il comando seguente per installare FreeTDS nel cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="2a681-186">Use the following command to install FreeTDS on the HDInsight cluster:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. <span data-ttu-id="2a681-187">Dopo aver installato FreeTDS, usare il comando seguente per connettersi al server del database SQL creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="2a681-187">Once FreeTDS has been installed, use the following command to connect to the SQL Database server you created previously:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="2a681-188">L'output che si riceve è simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="2a681-188">You receive output similar to the following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set to oozietest
        1>

3. <span data-ttu-id="2a681-189">Al prompt di `1>` , immettere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="2a681-189">At the `1>` prompt, enter the following lines:</span></span>

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    <span data-ttu-id="2a681-190">Dopo aver immesso l'istruzione `GO`, vengono valutate le istruzioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="2a681-190">When the `GO` statement is entered, the previous statements are evaluated.</span></span> <span data-ttu-id="2a681-191">Queste istruzioni creano una tabella denominata **mobiledata**, usata dal flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="2a681-191">These statements create a table named **mobiledata** that is used by the workflow.</span></span>

    <span data-ttu-id="2a681-192">Per verificare la corretta creazione della tabella, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2a681-192">Use the following to verify that the table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="2a681-193">L'output sarà simile al seguente testo:</span><span class="sxs-lookup"><span data-stu-id="2a681-193">You see output similar to the following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. <span data-ttu-id="2a681-194">Per uscire dall'utilità tsql, immettere `exit` al prompt di `1>`.</span><span class="sxs-lookup"><span data-stu-id="2a681-194">Enter `exit` at the `1>` prompt to exit the tsql utility.</span></span>

## <a name="create-the-job-definition"></a><span data-ttu-id="2a681-195">Creare la definizione del processo</span><span class="sxs-lookup"><span data-stu-id="2a681-195">Create the job definition</span></span>

<span data-ttu-id="2a681-196">La definizione del processo descrive dove trovare il file workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="2a681-196">The job definition describes where to find the workflow.xml.</span></span> <span data-ttu-id="2a681-197">Descrive inoltre dove trovare altri file usati dal flusso di lavoro, ad esempio useooziewf.hql. Definisce inoltre i valori delle proprietà usate nel flusso di lavoro e nei file associati.</span><span class="sxs-lookup"><span data-stu-id="2a681-197">It also describes where to find other files used by the workflow (such as useooziewf.hql.) It also defines the values for properties used within the workflow and associated files.</span></span>

1. <span data-ttu-id="2a681-198">Usare il comando seguente per ottenere l'indirizzo completo della risorsa di archiviazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="2a681-198">Use the following command to get the full address of the default storage.</span></span> <span data-ttu-id="2a681-199">L'indirizzo viene usato nel file di configurazione più avanti:</span><span class="sxs-lookup"><span data-stu-id="2a681-199">This address is used in the configuration file in a moment:</span></span>

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    <span data-ttu-id="2a681-200">Questo comando restituisce informazioni simili al codice XML seguente:</span><span class="sxs-lookup"><span data-stu-id="2a681-200">This command returns information similar to the following XML:</span></span>

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > <span data-ttu-id="2a681-201">Se il cluster HDInsight usa l'archiviazione di Azure come percorso di archiviazione predefinito, il contenuto dell'elemento `<value>` inizia con `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="2a681-201">If the HDInsight cluster uses Azure Storage as the default storage, the `<value>` element contents begin with `wasb://`.</span></span> <span data-ttu-id="2a681-202">Se, invece, viene usato Azure Data Lake Store, il contenuto inizia con `adl://`.</span><span class="sxs-lookup"><span data-stu-id="2a681-202">If Azure Data Lake Store is used instead, it begins with `adl://`.</span></span>

    <span data-ttu-id="2a681-203">Salvare il contenuto dell'elemento `<value>`, necessario nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="2a681-203">Save the contents of the `<value>` element, as it is used in the next steps.</span></span>

2. <span data-ttu-id="2a681-204">Usare il comando seguente per ottenere l'FQDN del nodo head del cluster.</span><span class="sxs-lookup"><span data-stu-id="2a681-204">Use the following command to get FQDN of the cluster headnode.</span></span> <span data-ttu-id="2a681-205">Queste informazioni vengono usate per l'indirizzo di JobTracker del cluster.</span><span class="sxs-lookup"><span data-stu-id="2a681-205">This information is used for the JobTracker address for the cluster:</span></span>

    ```
    hostname -f
    ```

    <span data-ttu-id="2a681-206">Verranno restituite informazioni simili al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="2a681-206">This returns information similar to the following text:</span></span>

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    <span data-ttu-id="2a681-207">La porta usata per JobTracker è la porta 8050, Pertanto l'indirizzo completo da usare per JobTracker è `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span><span class="sxs-lookup"><span data-stu-id="2a681-207">The port used for the JobTracker is 8050, so the full address to use for the JobTracker is `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span></span>

3. <span data-ttu-id="2a681-208">Usare quanto segue per creare la configurazione della definizione del processo Oozie:</span><span class="sxs-lookup"><span data-stu-id="2a681-208">Use the following to create the Oozie job definition configuration:</span></span>

    ```
    nano job.xml
    ```

4. <span data-ttu-id="2a681-209">All'apertura dell'editor nano, usare il codice XML seguente come contenuto del file:</span><span class="sxs-lookup"><span data-stu-id="2a681-209">Once the nano editor opens, use the following XML as the contents of the file:</span></span>

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

   * <span data-ttu-id="2a681-210">Sostituire tutte le istanze di **wasb://mycontainer@mystorageaccount.blob.core.windows.net** con il valore ricevuto in precedenza relativo alla risorsa di archiviazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="2a681-210">Replace all instances of **wasb://mycontainer@mystorageaccount.blob.core.windows.net** with the value you received earlier for default storage.</span></span>

     > [!WARNING]
     > <span data-ttu-id="2a681-211">Se il percorso è un percorso `wasb`, è necessario usare il percorso completo,</span><span class="sxs-lookup"><span data-stu-id="2a681-211">If the path is a `wasb` path, you must use the full path.</span></span> <span data-ttu-id="2a681-212">che non deve essere abbreviato in `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="2a681-212">Do not shorten it to just `wasb:///`.</span></span>

   * <span data-ttu-id="2a681-213">Sostituire **JOBTRACKERADDRESS** con l'indirizzo di JobTracker/ResourceManager ricevuto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2a681-213">Replace **JOBTRACKERADDRESS** with the JobTracker/ResourceManager address you received earlier.</span></span>
   * <span data-ttu-id="2a681-214">Sostituire **YourName** con il proprio nome di accesso per il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a681-214">Replace **YourName** with your login name for the HDInsight cluster.</span></span>
   * <span data-ttu-id="2a681-215">Sostituire **serverName**, **adminLogin** e **adminPassword** con le informazioni per il database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a681-215">Replace **serverName**, **adminLogin**, and **adminPassword** with the information for your Azure SQL Database.</span></span>

     <span data-ttu-id="2a681-216">La maggior parte delle informazioni in questo file viene usata per popolare i valori usati nel file workflow.xml o ooziewf.hql (ad esempio ${nameNode}).</span><span class="sxs-lookup"><span data-stu-id="2a681-216">Most of the information in this file is used to populate the values used in the workflow.xml or ooziewf.hql files (such as ${nameNode}.)</span></span>

     > [!NOTE]
     > <span data-ttu-id="2a681-217">La voce **oozie.wf.application.path** definisce la posizione del file workflow.xml, che contiene il flusso di lavoro eseguito da questo processo.</span><span class="sxs-lookup"><span data-stu-id="2a681-217">The **oozie.wf.application.path** entry defines where to find the workflow.xml file, which contains the workflow ran by this job.</span></span>

5. <span data-ttu-id="2a681-218">Usare CTRL+X, quindi **S** e **INVIO** per salvare il file.</span><span class="sxs-lookup"><span data-stu-id="2a681-218">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

## <a name="submit-and-manage-the-job"></a><span data-ttu-id="2a681-219">Inviare e gestire il processo</span><span class="sxs-lookup"><span data-stu-id="2a681-219">Submit and manage the job</span></span>

<span data-ttu-id="2a681-220">La procedura seguente usa il comando Oozie per inviare e gestire i flussi di lavoro di Oozie nel cluster.</span><span class="sxs-lookup"><span data-stu-id="2a681-220">The following steps use the Oozie command to submit and manage Oozie workflows on the cluster.</span></span> <span data-ttu-id="2a681-221">Il comando Oozie è un'interfaccia utente semplice per l' [API REST di Oozie](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="2a681-221">The Oozie command is a friendly interface over the [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2a681-222">Quando si usa il comando Oozie, è necessario usare l'FQDN per il nodo head di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a681-222">When using the Oozie command, you must use the FQDN for the HDInsight headnode.</span></span> <span data-ttu-id="2a681-223">Questo FQDN è accessibile solo dal cluster o se il cluster si trova in una rete virtuale di Azure, da altri computer nella stessa rete.</span><span class="sxs-lookup"><span data-stu-id="2a681-223">This FQDN is only accessible from the cluster, or if the cluster is on an Azure Virtual Network, from other machines on the same network.</span></span>


1. <span data-ttu-id="2a681-224">Usare quanto segue per ottenere l'URL del servizio di Oozie:</span><span class="sxs-lookup"><span data-stu-id="2a681-224">Use the following to obtain the URL to the Oozie service:</span></span>

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    <span data-ttu-id="2a681-225">Le informazioni restituite sono simili al codice XML seguente:</span><span class="sxs-lookup"><span data-stu-id="2a681-225">This returns information similar to the following XML:</span></span>

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    <span data-ttu-id="2a681-226">La parte `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` è l'URL da usare con il comando Oozie.</span><span class="sxs-lookup"><span data-stu-id="2a681-226">The `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` portion is the URL to use with the Oozie command.</span></span>

2. <span data-ttu-id="2a681-227">Usare quanto segue per creare una variabile di ambiente per l'URL, in modo che non sia necessario digitarlo per ogni comando:</span><span class="sxs-lookup"><span data-stu-id="2a681-227">Use the following to create an environment variable for the URL, so you don't have to type it for every command:</span></span>

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    <span data-ttu-id="2a681-228">Sostituire l'URL con quello ricevuto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2a681-228">Replace the URL with the one you received earlier.</span></span>
3. <span data-ttu-id="2a681-229">Usare quanto segue per inviare il processo:</span><span class="sxs-lookup"><span data-stu-id="2a681-229">Use the following to submit the job:</span></span>

    ```
    oozie job -config job.xml -submit
    ```

    <span data-ttu-id="2a681-230">Questo comando carica le informazioni sul processo da **job.xml** e le invia a Oozie, ma senza eseguirle.</span><span class="sxs-lookup"><span data-stu-id="2a681-230">This command loads the job information from **job.xml** and submits it to Oozie, but does not run it.</span></span>

    <span data-ttu-id="2a681-231">Dopo il completamento, il comando dovrebbe restituire l'ID del processo,</span><span class="sxs-lookup"><span data-stu-id="2a681-231">Once the command completes, it should return the ID of the job.</span></span> <span data-ttu-id="2a681-232">Ad esempio, `0000005-150622124850154-oozie-oozi-W`.</span><span class="sxs-lookup"><span data-stu-id="2a681-232">For example, `0000005-150622124850154-oozie-oozi-W`.</span></span> <span data-ttu-id="2a681-233">L'ID viene usato per gestire il processo.</span><span class="sxs-lookup"><span data-stu-id="2a681-233">This ID is used to manage the job.</span></span>

4. <span data-ttu-id="2a681-234">Visualizzare lo stato del processo tramite il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2a681-234">View the status of the job using the following command:</span></span>

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > <span data-ttu-id="2a681-235">Sostituire `<JOBID>` con l'ID restituito nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="2a681-235">Replace `<JOBID>` with the ID returned in the previous step.</span></span>

    <span data-ttu-id="2a681-236">Verranno restituite informazioni simili al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="2a681-236">This returns information similar to the following text:</span></span>

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

    <span data-ttu-id="2a681-237">Lo stato del processo è `PREP`.</span><span class="sxs-lookup"><span data-stu-id="2a681-237">This job has a status of `PREP`.</span></span> <span data-ttu-id="2a681-238">Questo stato indica che il processo è stato creato, ma non avviato.</span><span class="sxs-lookup"><span data-stu-id="2a681-238">This status indicates that the job was created, but not started.</span></span>

5. <span data-ttu-id="2a681-239">Usare il comando seguente per avviare il processo.</span><span class="sxs-lookup"><span data-stu-id="2a681-239">Use the following command to start the job:</span></span>

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > <span data-ttu-id="2a681-240">Sostituire `<JOBID>` con l'ID restituito in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2a681-240">Replace `<JOBID>` with the ID returned previously.</span></span>

    <span data-ttu-id="2a681-241">Se lo stato viene controllato dopo questo comando, risulterà in esecuzione e verranno restituite informazioni relative alle azioni all'interno del processo.</span><span class="sxs-lookup"><span data-stu-id="2a681-241">If you check the status after this command, it is in a running state, and information is returned for the actions within the job.</span></span>

6. <span data-ttu-id="2a681-242">Dopo aver completato l'attività, è possibile verificare che i dati siano stati generati ed esportati nella tabella del database SQL tramite i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a681-242">Once the task completes successfully, you can verify that the data was generated and exported to the SQL Database table by using the following commands:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="2a681-243">Al prompt di `1>` immettere la query seguente:</span><span class="sxs-lookup"><span data-stu-id="2a681-243">At the `1>` prompt, enter the following query:</span></span>

    ```
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="2a681-244">Le informazioni restituite sono simili al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="2a681-244">The information returned is similar to the following text:</span></span>

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

<span data-ttu-id="2a681-245">Per altre informazioni sul comando Oozie, vedere [Oozie command-line tool](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html) (Strumento da riga di comando di Oozie).</span><span class="sxs-lookup"><span data-stu-id="2a681-245">For more information on the Oozie command, see [Oozie command-line tool](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span></span>

## <a name="oozie-rest-api"></a><span data-ttu-id="2a681-246">API REST di Oozie</span><span class="sxs-lookup"><span data-stu-id="2a681-246">Oozie REST API</span></span>

<span data-ttu-id="2a681-247">L'API REST di Oozie consente di compilare strumenti personalizzati che funzionano con Oozie.</span><span class="sxs-lookup"><span data-stu-id="2a681-247">The Oozie REST API allows you to build your own tools that work with Oozie.</span></span> <span data-ttu-id="2a681-248">Di seguito sono riportate informazioni specifiche di HDInsight sull'uso dell'API REST di Oozie:</span><span class="sxs-lookup"><span data-stu-id="2a681-248">The following are HDInsight specific information about using the Oozie REST API:</span></span>

* <span data-ttu-id="2a681-249">**URI**: è possibile accedere all'API REST all'esterno del cluster in `https://CLUSTERNAME.azurehdinsight.net/oozie`.</span><span class="sxs-lookup"><span data-stu-id="2a681-249">**URI**: The REST API can be accessed from outside the cluster at `https://CLUSTERNAME.azurehdinsight.net/oozie`</span></span>

* <span data-ttu-id="2a681-250">**Autenticazione**: eseguire l'autenticazione all'API con l'account (admin) e la password HTTP del cluster.</span><span class="sxs-lookup"><span data-stu-id="2a681-250">**Authentication**: Authenticate to the API using the cluster HTTP account (admin) and password.</span></span> <span data-ttu-id="2a681-251">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="2a681-251">For example:</span></span>

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

<span data-ttu-id="2a681-252">Per altre informazioni sull'uso dell'API REST di Oozie, vedere la pagina relativa all' [API dei servizi Web di Oozie](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="2a681-252">For more information on using the Oozie REST API, see [Oozie Web Services API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

## <a name="oozie-web-ui"></a><span data-ttu-id="2a681-253">Interfaccia utente Web di Oozie</span><span class="sxs-lookup"><span data-stu-id="2a681-253">Oozie Web UI</span></span>

<span data-ttu-id="2a681-254">L'interfaccia utente Web di Oozie fornisce una visualizzazione basata sul Web dello stato dei processi Oozie nel cluster.</span><span class="sxs-lookup"><span data-stu-id="2a681-254">The Oozie Web UI provides a web-based view into the status of Oozie jobs on the cluster.</span></span> <span data-ttu-id="2a681-255">L'interfaccia utente Web consente di visualizzare le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a681-255">The web UI allows you to view the following information:</span></span>

* <span data-ttu-id="2a681-256">Stato processo</span><span class="sxs-lookup"><span data-stu-id="2a681-256">Job status</span></span>
* <span data-ttu-id="2a681-257">Definizione del processo</span><span class="sxs-lookup"><span data-stu-id="2a681-257">Job definition</span></span>
* <span data-ttu-id="2a681-258">Configurazione</span><span class="sxs-lookup"><span data-stu-id="2a681-258">Configuration</span></span>
* <span data-ttu-id="2a681-259">Grafico delle azioni nel processo</span><span class="sxs-lookup"><span data-stu-id="2a681-259">A graph of the actions in the job</span></span>
* <span data-ttu-id="2a681-260">Log per il processo</span><span class="sxs-lookup"><span data-stu-id="2a681-260">Logs for the job</span></span>

<span data-ttu-id="2a681-261">È anche possibile visualizzare i dettagli delle azioni all'interno di un processo.</span><span class="sxs-lookup"><span data-stu-id="2a681-261">You can also view details for actions within a job.</span></span>

<span data-ttu-id="2a681-262">Per accedere all'interfaccia utente Web di Oozie, attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2a681-262">To access the Oozie Web UI, use the following steps:</span></span>

1. <span data-ttu-id="2a681-263">Creare un tunnel SSH per il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a681-263">Create an SSH tunnel to the HDInsight cluster.</span></span> <span data-ttu-id="2a681-264">Per informazioni, vedere il documento [Usare il tunneling SSH con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="2a681-264">For information, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="2a681-265">Dopo aver creato un tunnel, aprire l'interfaccia utente Web di Ambari nel Web browser.</span><span class="sxs-lookup"><span data-stu-id="2a681-265">Once a tunnel has been created, open the Ambari web UI in your web browser.</span></span> <span data-ttu-id="2a681-266">L'URI del sito Ambari è **https://CLUSTERNAME.azurehdinsight.NET**.</span><span class="sxs-lookup"><span data-stu-id="2a681-266">The URI for the Ambari site is **https://CLUSTERNAME.azurehdinsight.net**.</span></span> <span data-ttu-id="2a681-267">Sostituire **CLUSTERNAME** con il nome del cluster HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="2a681-267">Replace **CLUSTERNAME** with the name of your Linux-based HDInsight cluster.</span></span>

3. <span data-ttu-id="2a681-268">Nel lato sinistro della pagina selezionare **Oozie**, quindi **Quick Links** e infine **Oozie Web UI**.</span><span class="sxs-lookup"><span data-stu-id="2a681-268">From the left side of the page, select **Oozie**, then **Quick Links**, and finally **Oozie Web UI**.</span></span>

    ![immagine dei menu](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. <span data-ttu-id="2a681-270">L'interfaccia utente Web di Oozie passa alla visualizzazione predefinita dei processi del flusso di lavoro in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2a681-270">The Oozie Web UI defaults to displaying running Workflow Jobs.</span></span> <span data-ttu-id="2a681-271">Per visualizzare tutti i processi del flusso di lavoro, selezionare **All Jobs**.</span><span class="sxs-lookup"><span data-stu-id="2a681-271">To see all workflow jobs, select **All Jobs**.</span></span>

    ![Tutti i processi visualizzati](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. <span data-ttu-id="2a681-273">Selezionare un processo per visualizzare altre informazioni specifiche.</span><span class="sxs-lookup"><span data-stu-id="2a681-273">Select a job to view more information about the job.</span></span>

    ![Job Info](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. <span data-ttu-id="2a681-275">Nella scheda relativa alle informazioni del processo è possibile visualizzare informazioni di base sul processo e le singole azioni all'interno del processo.</span><span class="sxs-lookup"><span data-stu-id="2a681-275">From the Job Info tab, you can see basic job information and the individual actions within the job.</span></span> <span data-ttu-id="2a681-276">Usando le schede nella parte superiore è possibile visualizzare la definizione, la configurazione, il log del processo o un grafo aciclico diretto (DAG) del processo.</span><span class="sxs-lookup"><span data-stu-id="2a681-276">Using the tabs at the top you can view the Job Definition, Job Configuration, access the Job Log or view a Directed Acyclic Graph (DAG) of the job.</span></span>

   * <span data-ttu-id="2a681-277">**Job Log**: selezionare il pulsante **GetLogs** per recuperare tutti i log relativi al processo o usare il campo **Enter Search Filter** per filtrare i log.</span><span class="sxs-lookup"><span data-stu-id="2a681-277">**Job Log**: Select the **GetLogs** button to get all logs for the job, or use the **Enter Search Filter** field to filter logs</span></span>

       ![Log del processo](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * <span data-ttu-id="2a681-279">**JobDAG**: il DAG è una rappresentazione grafica dei percorsi dati rilevati nel flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="2a681-279">**JobDAG**: The DAG is a graphical overview of the data paths taken through the workflow</span></span>

       ![DAG del processo](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. <span data-ttu-id="2a681-281">Selezionando una delle azioni dalla scheda **Job Info**, vengono visualizzate informazioni sull'azione.</span><span class="sxs-lookup"><span data-stu-id="2a681-281">Selecting one of the actions from the **Job Info** tab brings up information for the action.</span></span> <span data-ttu-id="2a681-282">Ad esempio, selezionare l'azione **RunHiveScript** .</span><span class="sxs-lookup"><span data-stu-id="2a681-282">For example, select the **RunHiveScript** action.</span></span>

    ![Informazioni sull'azione](./media/hdinsight-use-oozie-linux-mac/action.png)

8. <span data-ttu-id="2a681-284">È possibile visualizzare i dettagli per l'azione, ad esempio un collegamento a **Console URL** (URL della console).</span><span class="sxs-lookup"><span data-stu-id="2a681-284">You can see details for the action, such as a link to the **Console URL**.</span></span> <span data-ttu-id="2a681-285">Questo collegamento può essere usato per visualizzare le informazioni di JobTracker per il processo.</span><span class="sxs-lookup"><span data-stu-id="2a681-285">This link can be used to view JobTracker information for the job.</span></span>

## <a name="scheduling-jobs"></a><span data-ttu-id="2a681-286">Pianificazione di processi</span><span class="sxs-lookup"><span data-stu-id="2a681-286">Scheduling jobs</span></span>

<span data-ttu-id="2a681-287">Il coordinatore consente di specificare inizio, fine e frequenza dei processi.</span><span class="sxs-lookup"><span data-stu-id="2a681-287">The coordinator allows you to specify a start, end, and occurrence frequency for jobs.</span></span> <span data-ttu-id="2a681-288">Per definire una pianificazione per il flusso di lavoro,attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2a681-288">To define a schedule for the workflow, use the following steps:</span></span>

1. <span data-ttu-id="2a681-289">Usare quanto segue per creare un file denominato **coordinator.xml**:</span><span class="sxs-lookup"><span data-stu-id="2a681-289">Use the following to create a file named **coordinator.xml**:</span></span>

    ```
    nano coordinator.xml
    ```

    <span data-ttu-id="2a681-290">Usare il codice XML seguente come contenuto del file:</span><span class="sxs-lookup"><span data-stu-id="2a681-290">Use the following XML as the contents of the file:</span></span>

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
    > <span data-ttu-id="2a681-291">Le variabili `${...}` vengono sostituite dai valori nella definizione del processo in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2a681-291">The `${...}` variables are replaced by values in the job definition at run-time.</span></span> <span data-ttu-id="2a681-292">Le variabili sono:</span><span class="sxs-lookup"><span data-stu-id="2a681-292">The variables are:</span></span>
    >
    > * <span data-ttu-id="2a681-293">`${coordFrequency}`: tempo trascorso tra l'esecuzione di istanze del processo.</span><span class="sxs-lookup"><span data-stu-id="2a681-293">`${coordFrequency}`: Time between running instances of the job.</span></span>
    > <span data-ttu-id="2a681-294">** `${coordStart}`: ora di inizio del processo.</span><span class="sxs-lookup"><span data-stu-id="2a681-294">** `${coordStart}`: The job start time.</span></span>
    > * <span data-ttu-id="2a681-295">`${coordEnd}`: ora di fine del processo.</span><span class="sxs-lookup"><span data-stu-id="2a681-295">`${coordEnd}`: The job end time.</span></span>
    > * <span data-ttu-id="2a681-296">`${coordTimezone}`: i processi del coordinatore si trovano in un fuso orario predefinito che non tiene conto dell'ora legale (in genere rappresentato dall'acronimo UTC).</span><span class="sxs-lookup"><span data-stu-id="2a681-296">`${coordTimezone}`: Coordinator jobs are in a fixed time zone with no daylight savings time (typically represented by using UTC).</span></span> <span data-ttu-id="2a681-297">Questo fuso orario viene definito "Fuso orario di elaborazione Oozie".</span><span class="sxs-lookup"><span data-stu-id="2a681-297">This time zone is referred as the "Oozie processing timezone."</span></span>
    > * <span data-ttu-id="2a681-298">`${wfPath}`: percorso del file workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="2a681-298">`${wfPath}`: The path to the workflow.xml.</span></span>

2. <span data-ttu-id="2a681-299">Per salvare il file, usare CTRL-X, **Y** e **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="2a681-299">To save the file, use Ctrl-X, **Y**, and **Enter**.</span></span>

3. <span data-ttu-id="2a681-300">Usare il comando seguente per copiare il file nella directory di lavoro del processo:</span><span class="sxs-lookup"><span data-stu-id="2a681-300">Use the following command to copy the file to the working directory for this job:</span></span>

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. <span data-ttu-id="2a681-301">Usare il comando seguente per modificare il file **job.xml** :</span><span class="sxs-lookup"><span data-stu-id="2a681-301">Use the following to modify the **job.xml** file:</span></span>

    ```
    nano job.xml
    ```

    <span data-ttu-id="2a681-302">Apportare le modifiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a681-302">Make the following changes:</span></span>

   * <span data-ttu-id="2a681-303">Per indicare a Oozie di eseguire il file del coordinatore invece del file del flusso di lavoro sostituire `<name>oozie.wf.application.path</name>` con `<name>oozie.coord.application.path</name>`.</span><span class="sxs-lookup"><span data-stu-id="2a681-303">To instruct oozie to run the coordinator file instead of the workflow, change `<name>oozie.wf.application.path</name>` to `<name>oozie.coord.application.path</name>`.</span></span>

   * <span data-ttu-id="2a681-304">Per impostare la variabile `workflowPath` usata dal coordinatore, aggiornare il codice XML seguente:</span><span class="sxs-lookup"><span data-stu-id="2a681-304">To set the `workflowPath` variable used by the coordinator, add the following XML:</span></span>

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       <span data-ttu-id="2a681-305">Sostituire il testo `wasb://mycontainer@mystorageaccount.blob.core.windows` con il valore usato nelle altre voci del file job.xlm.</span><span class="sxs-lookup"><span data-stu-id="2a681-305">Replace the `wasb://mycontainer@mystorageaccount.blob.core.windows` text with the value used in other entries in the job.xml file.</span></span>

   * <span data-ttu-id="2a681-306">Per definire l'inizio, la fine e la frequenza per il coordinatore, aggiungere il codice XML seguente:</span><span class="sxs-lookup"><span data-stu-id="2a681-306">To define the start, end, and frequency for the coordinator, add the following XML:</span></span>

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

       <span data-ttu-id="2a681-307">Questi valori impostano l'ora di inizio sulle 12:00 del 10 maggio 2017 e la fine sul 12 maggio 2017.</span><span class="sxs-lookup"><span data-stu-id="2a681-307">These values set the start time to 12:00PM on May 10, 2017, the end time to May 12, 2017.</span></span> <span data-ttu-id="2a681-308">L'intervallo per l'esecuzione del processo viene impostato su ogni giorno.</span><span class="sxs-lookup"><span data-stu-id="2a681-308">The interval for running this job daily.</span></span> <span data-ttu-id="2a681-309">La frequenza è espressa in minuti, quindi 24 ore x 60 minuti = 1440 minuti.</span><span class="sxs-lookup"><span data-stu-id="2a681-309">The frequency is in minutes, so 24 hours x 60 minutes = 1440 minutes.</span></span> <span data-ttu-id="2a681-310">Infine, il fuso orario è impostato su UTC.</span><span class="sxs-lookup"><span data-stu-id="2a681-310">Finally, the timezone is set to UTC.</span></span>

5. <span data-ttu-id="2a681-311">Usare CTRL+X, quindi **S** e **INVIO** per salvare il file.</span><span class="sxs-lookup"><span data-stu-id="2a681-311">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

6. <span data-ttu-id="2a681-312">Per eseguire il processo, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2a681-312">To run the job, use the following command:</span></span>

    ```
    oozie job -config job.xml -run
    ```

    <span data-ttu-id="2a681-313">Il comando invia e avvia il processo.</span><span class="sxs-lookup"><span data-stu-id="2a681-313">This command submits and starts the job.</span></span>

7. <span data-ttu-id="2a681-314">Visitando l'interfaccia utente Web di Oozie e selezionando la scheda **Coordinator Jobs** (Processi del coordinatore), si ottengono informazioni simili all'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="2a681-314">If you visit the Oozie Web UI and select the **Coordinator Jobs** tab, you see information similar to the following image:</span></span>

    ![scheda coordinator jobs](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    <span data-ttu-id="2a681-316">La voce **Next Materialization** (Materializzazione successiva) contiene l'orario per l'esecuzione successiva del processo.</span><span class="sxs-lookup"><span data-stu-id="2a681-316">The **Next Materialization** entry contains the next time that the job runs.</span></span>

8. <span data-ttu-id="2a681-317">Come per il processo del flusso di lavoro precedente, selezionando la voce del processo nell'interfaccia utente Web vengono visualizzate informazioni sul processo:</span><span class="sxs-lookup"><span data-stu-id="2a681-317">Similar to the earlier workflow job, selecting the job entry in the web UI displays information on the job:</span></span>

    ![Informazioni sui processi coordinatore](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > <span data-ttu-id="2a681-319">Questa immagine visualizza solo le esecuzioni riuscite del processo, non le singole azioni nel flusso di lavoro pianificato.</span><span class="sxs-lookup"><span data-stu-id="2a681-319">This image only shows successful runs of the job, not individual actions within the scheduled workflow.</span></span> <span data-ttu-id="2a681-320">Per visualizzarle, selezionare una delle voci in **Action** .</span><span class="sxs-lookup"><span data-stu-id="2a681-320">To see that, select one of the **Action** entries.</span></span>

    ![Informazioni sull'azione](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a><span data-ttu-id="2a681-322">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="2a681-322">Troubleshooting</span></span>

<span data-ttu-id="2a681-323">L'interfaccia utente di Oozie consente di visualizzare i log di Oozie.</span><span class="sxs-lookup"><span data-stu-id="2a681-323">The Oozie UI allows you to view Oozie logs.</span></span> <span data-ttu-id="2a681-324">Contiene anche collegamenti ai log di JobTracker per le attività di MapReduce avviate dal flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="2a681-324">It also contains links to JobTracker logs for MapReduce tasks started by the workflow.</span></span> <span data-ttu-id="2a681-325">Il modello per la risoluzione dei problemi deve essere il seguente:</span><span class="sxs-lookup"><span data-stu-id="2a681-325">The pattern for troubleshooting should be:</span></span>

1. <span data-ttu-id="2a681-326">Visualizzare il processo nell'interfaccia utente Web di Oozie.</span><span class="sxs-lookup"><span data-stu-id="2a681-326">View the job in Oozie Web UI.</span></span>

2. <span data-ttu-id="2a681-327">Se si verifica un errore o un problema per un'azione specifica, selezionare l'azione per vedere se il campo **Error Message** fornisce altre informazioni sull'errore.</span><span class="sxs-lookup"><span data-stu-id="2a681-327">If there is an error or failure for a specific action, select the action to see if the **Error Message** field provides more information on the failure.</span></span>

3. <span data-ttu-id="2a681-328">Se disponibile, usare l'URL dall'azione per visualizzare altri dettagli (ad esempio, i log di JobTracker) relativi all'azione.</span><span class="sxs-lookup"><span data-stu-id="2a681-328">If available, use the URL from the action to view more details (such as JobTracker logs) for the action.</span></span>

<span data-ttu-id="2a681-329">Di seguito sono riportati errori specifici che possono verificarsi e come risolverli.</span><span class="sxs-lookup"><span data-stu-id="2a681-329">The following are specific errors you may encounter, and how to resolve them.</span></span>

### <a name="ja009-cannot-initialize-cluster"></a><span data-ttu-id="2a681-330">JA009: Cannot initialize cluster</span><span class="sxs-lookup"><span data-stu-id="2a681-330">JA009: Cannot initialize cluster</span></span>

<span data-ttu-id="2a681-331">**Sintomi**: lo stato del processo cambia in **SUSPENDED**.</span><span class="sxs-lookup"><span data-stu-id="2a681-331">**Symptoms**: The job status changes to **SUSPENDED**.</span></span> <span data-ttu-id="2a681-332">I dettagli del processo mostrano lo stato di RunHiveScript come **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="2a681-332">Details for the job show the RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="2a681-333">Selezionando l'azione verrà visualizzato il messaggio di errore seguente:</span><span class="sxs-lookup"><span data-stu-id="2a681-333">Selecting the action displays the following error message:</span></span>

    JA009: Cannot initialize Cluster. Please check your configuration for map

<span data-ttu-id="2a681-334">**Causa**: gli indirizzi WASB usati nel file **job.xml** non includono il contenitore di archiviazione o il nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2a681-334">**Cause**: The WASB addresses used in the **job.xml** file do not contain the storage container or storage account name.</span></span> <span data-ttu-id="2a681-335">Il formato dell'indirizzo WASB deve essere `wasb://containername@storageaccountname.blob.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="2a681-335">The WASB address format must be `wasb://containername@storageaccountname.blob.core.windows.net`.</span></span>

<span data-ttu-id="2a681-336">**Risoluzione**: modificare gli indirizzi WASB usati dal processo.</span><span class="sxs-lookup"><span data-stu-id="2a681-336">**Resolution**: Change the WASB addresses used by the job.</span></span>

### <a name="ja002-oozie-is-not-allowed-to-impersonate-ltuser"></a><span data-ttu-id="2a681-337">JA002: Oozie is not allowed to impersonate &lt;USER></span><span class="sxs-lookup"><span data-stu-id="2a681-337">JA002: Oozie is not allowed to impersonate &lt;USER></span></span>

<span data-ttu-id="2a681-338">**Sintomi**: lo stato del processo cambia in **SUSPENDED**.</span><span class="sxs-lookup"><span data-stu-id="2a681-338">**Symptoms**: The job status changes to **SUSPENDED**.</span></span> <span data-ttu-id="2a681-339">I dettagli del processo mostrano lo stato di RunHiveScript come **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="2a681-339">Details for the job show the RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="2a681-340">Selezionando l'azione verrà visualizzato il messaggio di errore seguente:</span><span class="sxs-lookup"><span data-stu-id="2a681-340">Selecting the action shows the following error message:</span></span>

    JA002: User: oozie is not allowed to impersonate <USER>

<span data-ttu-id="2a681-341">**Causa**: le impostazioni di autorizzazione correnti non consentono a Oozie di rappresentare l'account utente specificato.</span><span class="sxs-lookup"><span data-stu-id="2a681-341">**Cause**: Current permission settings do not allow Oozie to impersonate the specified user account.</span></span>

<span data-ttu-id="2a681-342">**Risoluzione**: Oozie è autorizzato a rappresentare gli utenti nel gruppo **users**.</span><span class="sxs-lookup"><span data-stu-id="2a681-342">**Resolution**: Oozie is allowed to impersonate users in the **users** group.</span></span> <span data-ttu-id="2a681-343">Usare `groups USERNAME` per visualizzare i gruppi di cui l'account utente è membro.</span><span class="sxs-lookup"><span data-stu-id="2a681-343">Use the `groups USERNAME` to see the groups that the user account is a member of.</span></span> <span data-ttu-id="2a681-344">Se l'utente non è un membro del gruppo **users** , usare il comando seguente per aggiungere l'utente al gruppo:</span><span class="sxs-lookup"><span data-stu-id="2a681-344">If the user is not a member of the **users** group, use the following command to add the user to the group:</span></span>

    sudo adduser USERNAME users

> [!NOTE]
> <span data-ttu-id="2a681-345">Potrebbero essere necessari alcuni minuti prima che HDInsight riconosca che l'utente è stato aggiunto al gruppo.</span><span class="sxs-lookup"><span data-stu-id="2a681-345">It may take several minutes before HDInsight recognizes that the user has been added to the group.</span></span>

### <a name="launcher-error-sqoop"></a><span data-ttu-id="2a681-346">ERRORE dell'utilità di avvio (Sqoop)</span><span class="sxs-lookup"><span data-stu-id="2a681-346">Launcher ERROR (Sqoop)</span></span>

<span data-ttu-id="2a681-347">**Sintomi**: lo stato del processo cambia in **KILLED**.</span><span class="sxs-lookup"><span data-stu-id="2a681-347">**Symptoms**: The job status changes to **KILLED**.</span></span> <span data-ttu-id="2a681-348">I dettagli del processo mostrano lo stato di RunSqoopExport come **ERROR**.</span><span class="sxs-lookup"><span data-stu-id="2a681-348">Details for the job show the RunSqoopExport status as **ERROR**.</span></span> <span data-ttu-id="2a681-349">Selezionando l'azione verrà visualizzato il messaggio di errore seguente:</span><span class="sxs-lookup"><span data-stu-id="2a681-349">Selecting the action shows the following error message:</span></span>

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

<span data-ttu-id="2a681-350">**Causa**: Sqoop non è in grado di caricare il driver del database necessario per accedere al database.</span><span class="sxs-lookup"><span data-stu-id="2a681-350">**Cause**: Sqoop is unable to load the database driver required to access the database.</span></span>

<span data-ttu-id="2a681-351">**Risoluzione**: quando si usa Sqoop da un processo Oozie, è necessario includere il driver del database con le altre risorse (ad esempio, workflow.xml) usate dal processo.</span><span class="sxs-lookup"><span data-stu-id="2a681-351">**Resolution**: When using Sqoop from an Oozie job, you must include the database driver with the other resources (such as the workflow.xml) used by the job.</span></span> <span data-ttu-id="2a681-352">È anche necessario fare riferimento all'archivio contenente il driver del database dalla sezione `<sqoop>...</sqoop>` di workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="2a681-352">Also Reference the archive containing the database driver from the `<sqoop>...</sqoop>` section of the workflow.xml.</span></span>

<span data-ttu-id="2a681-353">Ad esempio, per il processo in questo documento si useranno i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a681-353">For example, for the job in this document, you would use the following steps:</span></span>

1. <span data-ttu-id="2a681-354">Copiare il file sqljdbc4.1.jar nella directory /tutorials/useoozie:</span><span class="sxs-lookup"><span data-stu-id="2a681-354">Copy the sqljdbc4.1.jar file to the /tutorials/useoozie directory:</span></span>

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. <span data-ttu-id="2a681-355">Modificare il file workflow.xml per aggiungere il codice XML seguente in una nuova riga sopra `</sqoop>`:</span><span class="sxs-lookup"><span data-stu-id="2a681-355">Modify the workflow.xml to add the following XML on a new line above `</sqoop>`:</span></span>

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a><span data-ttu-id="2a681-356">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2a681-356">Next steps</span></span>

<span data-ttu-id="2a681-357">In questa esercitazione si è appreso come definire un flusso di lavoro di Oozie e come eseguire un processo Oozie.</span><span class="sxs-lookup"><span data-stu-id="2a681-357">In this tutorial, you learned how to define an Oozie workflow and how to run an Oozie job.</span></span> <span data-ttu-id="2a681-358">Per altre informazioni sull'uso di HDInsight, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a681-358">To learn more about working with HDInsight, see the following articles:</span></span>

* <span data-ttu-id="2a681-359">[Usare il coordinatore Oozie basato sul tempo con HDInsight][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="2a681-359">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="2a681-360">[Caricare dati per processi Hadoop in HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="2a681-360">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="2a681-361">[Usare Sqoop con Hadoop in HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="2a681-361">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="2a681-362">[Usare Hive con Hadoop in HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="2a681-362">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="2a681-363">[Usare Pig con Hadoop in HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="2a681-363">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="2a681-364">[Sviluppare programmi MapReduce Java per HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="2a681-364">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

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
