---
title: aaaUse Hadoop Oozie in HDInsight | Documenti Microsoft
description: Usare Oozie di Hadoop in HDInsight, una servizio per Big Data. Informazioni su come un flusso di lavoro, Oozie toodefine e inviare un processo di Oozie.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 870098f0-f416-4491-9719-78994bf4a369
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 12d0cf1a01838ab0f4e699c384ce2fb18f85cbad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-in-hdinsight"></a><span data-ttu-id="12984-104">Utilizzare Oozie con Hadoop toodefine ed eseguire un flusso di lavoro in HDInsight</span><span class="sxs-lookup"><span data-stu-id="12984-104">Use Oozie with Hadoop toodefine and run a workflow in HDInsight</span></span>
[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="12984-105">Informazioni su come toouse Apache Oozie toodefine un flusso di lavoro ed eseguire hello del flusso di lavoro in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="12984-105">Learn how toouse Apache Oozie toodefine a workflow and run hello workflow on HDInsight.</span></span> <span data-ttu-id="12984-106">toolearn su coordinatore Oozie hello, vedere [utilizzare basati sul tempo Coordinator Oozie di Hadoop con HDInsight][hdinsight-oozie-coordinator-time].</span><span class="sxs-lookup"><span data-stu-id="12984-106">toolearn about hello Oozie coordinator, see [Use time-based Hadoop Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time].</span></span> <span data-ttu-id="12984-107">toolearn Data Factory di Azure, vedere [usare Pig e Hive con Data Factory][azure-data-factory-pig-hive].</span><span class="sxs-lookup"><span data-stu-id="12984-107">toolearn Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

<span data-ttu-id="12984-108">Apache Oozie è un sistema di flusso di lavoro/coordinamento che consente di gestire i processi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="12984-108">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="12984-109">È integrato con lo stack di Hadoop hello e supporta i processi Hadoop MapReduce Apache, Pig Apache, Apache Hive e Sqoop Apache.</span><span class="sxs-lookup"><span data-stu-id="12984-109">It is integrated with hello Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="12984-110">Può essere anche i processi utilizzati tooschedule sistema tooa specifico, ad esempio programmi Java o gli script della shell.</span><span class="sxs-lookup"><span data-stu-id="12984-110">It can also be used tooschedule jobs that are specific tooa system, like Java programs or shell scripts.</span></span>

<span data-ttu-id="12984-111">flusso di lavoro di Hello che è implementare seguendo le istruzioni di hello in questa esercitazione contiene due azioni:</span><span class="sxs-lookup"><span data-stu-id="12984-111">hello workflow you implement by following hello instructions in this tutorial contains two actions:</span></span>

![Diagramma del flusso di lavoro][img-workflow-diagram]

1. <span data-ttu-id="12984-113">Un'azione di Hive viene eseguito un hello toocount di script HiveQL le occorrenze di ogni tipo di livello di registrazione in un file log4j.</span><span class="sxs-lookup"><span data-stu-id="12984-113">A Hive action runs a HiveQL script toocount hello occurrences of each log-level type in a log4j file.</span></span> <span data-ttu-id="12984-114">Ogni file log4j è costituito da una riga di campi che contiene un campo [LOG livello] che mostra il tipo di hello e la gravità di hello, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="12984-114">Each log4j file consists of a line of fields that contains a [LOG LEVEL] field that shows hello type and hello severity, for example:</span></span>
   
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
   
    <span data-ttu-id="12984-115">output dello script Hive Hello è simile a:</span><span class="sxs-lookup"><span data-stu-id="12984-115">hello Hive script output is similar to:</span></span>
   
        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4
   
    <span data-ttu-id="12984-116">Per altre informazioni su Hive, vedere [Usare Hive con HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="12984-116">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="12984-117">Un'azione Sqoop Esporta hello HiveQL output tooa nella tabella in un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="12984-117">A Sqoop action exports hello HiveQL output tooa table in an Azure SQL database.</span></span> <span data-ttu-id="12984-118">Per altre informazioni su Sqoop, vedere [Usare Sqoop con Hadoop in HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="12984-118">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="12984-119">Per le versioni Oozie supportate nei cluster HDInsight, vedere [novità introdotta nelle versioni di cluster Hadoop hello fornite da HDInsight?] [hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="12984-119">For supported Oozie versions on HDInsight clusters, see [What's new in hello Hadoop cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="12984-120">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="12984-120">Prerequisites</span></span>
<span data-ttu-id="12984-121">Prima di iniziare questa esercitazione, è necessario disporre di hello elemento seguente:</span><span class="sxs-lookup"><span data-stu-id="12984-121">Before you begin this tutorial, you must have hello following item:</span></span>

* <span data-ttu-id="12984-122">**Workstation con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="12984-122">**A workstation with Azure PowerShell**.</span></span> 
  

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]
  

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a><span data-ttu-id="12984-123">Definire Oozie del flusso di lavoro e hello script HiveQL correlato</span><span class="sxs-lookup"><span data-stu-id="12984-123">Define Oozie workflow and hello related HiveQL script</span></span>
<span data-ttu-id="12984-124">Le definizioni dei flussi di lavoro di Oozie sono scritte in linguaggio hPDL (XML Process Definition Language).</span><span class="sxs-lookup"><span data-stu-id="12984-124">Oozie workflows definitions are written in hPDL (a XML Process Definition Language).</span></span> <span data-ttu-id="12984-125">nome del file di flusso di lavoro predefinito Hello *workflow*.</span><span class="sxs-lookup"><span data-stu-id="12984-125">hello default workflow file name is *workflow.xml*.</span></span> <span data-ttu-id="12984-126">di seguito Hello è il file di flusso di lavoro hello che vengono usati in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="12984-126">hello following is hello workflow file you use in this tutorial.</span></span>

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
                <param>hiveOutputFolder=${hiveOutputFolder}</param>
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
            <arg>${hiveOutputFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\001"</arg>
            </sqoop>
            <ok to="end"/>
            <error to="fail"/>
        </action>

        <kill name="fail">
            <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>

        <end name="end"/>
    </workflow-app>

<span data-ttu-id="12984-127">Esistono due azioni definite nel flusso di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="12984-127">There are two actions defined in hello workflow.</span></span> <span data-ttu-id="12984-128">start-tooaction Hello è *RunHiveScript*.</span><span class="sxs-lookup"><span data-stu-id="12984-128">hello start-tooaction is *RunHiveScript*.</span></span> <span data-ttu-id="12984-129">Se l'azione di hello viene eseguito correttamente, l'azione successiva hello è *RunSqoopExport*.</span><span class="sxs-lookup"><span data-stu-id="12984-129">If hello action runs successfully, hello next action is *RunSqoopExport*.</span></span>

<span data-ttu-id="12984-130">Hello RunHiveScript ha diverse variabili.</span><span class="sxs-lookup"><span data-stu-id="12984-130">hello RunHiveScript has several variables.</span></span> <span data-ttu-id="12984-131">Passare i valori hello quando si invia il processo di Oozie hello dalla propria workstation con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="12984-131">You pass hello values when you submit hello Oozie job from your workstation by using Azure PowerShell.</span></span>

<table border = "1">
<tr><th><span data-ttu-id="12984-132">Variabili del flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="12984-132">Workflow variables</span></span></th><th><span data-ttu-id="12984-133">Descrizione</span><span class="sxs-lookup"><span data-stu-id="12984-133">Description</span></span></th></tr>
<tr><td><span data-ttu-id="12984-134">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="12984-134">${jobTracker}</span></span></td><td><span data-ttu-id="12984-135">Specifica l'URL di hello di gestione di processi Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="12984-135">Specifies hello URL of hello Hadoop job tracker.</span></span> <span data-ttu-id="12984-136">In HDInsight versione 3.0 o 2.1 usare <strong>jobtrackerhost: 9010</strong>.</span><span class="sxs-lookup"><span data-stu-id="12984-136">Use <strong>jobtrackerhost:9010</strong> in HDInsight version 3.0 and 2.1.</span></span></td></tr>
<tr><td><span data-ttu-id="12984-137">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="12984-137">${nameNode}</span></span></td><td><span data-ttu-id="12984-138">Specifica l'URL di hello del nodo del nome hello Hadoop.</span><span class="sxs-lookup"><span data-stu-id="12984-138">Specifies hello URL of hello Hadoop name node.</span></span> <span data-ttu-id="12984-139">Utilizzare ad esempio, l'indirizzo di sistema file predefinito hello, <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. n e t</i>.</span><span class="sxs-lookup"><span data-stu-id="12984-139">Use hello default file system address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
<tr><td><span data-ttu-id="12984-140">${queueName}</span><span class="sxs-lookup"><span data-stu-id="12984-140">${queueName}</span></span></td><td><span data-ttu-id="12984-141">Specifica del nome della coda hello hello processo viene inviato a.</span><span class="sxs-lookup"><span data-stu-id="12984-141">Specifies hello queue name that hello job is submitted to.</span></span> <span data-ttu-id="12984-142">Hello utilizzare <strong>predefinito</strong>.</span><span class="sxs-lookup"><span data-stu-id="12984-142">Use hello <strong>default</strong>.</span></span></td></tr>
</table>

<table border = "1">
<tr><th><span data-ttu-id="12984-143">Variabile azione Hive</span><span class="sxs-lookup"><span data-stu-id="12984-143">Hive action variable</span></span></th><th><span data-ttu-id="12984-144">Descrizione</span><span class="sxs-lookup"><span data-stu-id="12984-144">Description</span></span></th></tr>
<tr><td><span data-ttu-id="12984-145">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="12984-145">${hiveDataFolder}</span></span></td><td><span data-ttu-id="12984-146">Specifica la directory di origine hello per hello comando Hive Create Table.</span><span class="sxs-lookup"><span data-stu-id="12984-146">Specifies hello source directory for hello Hive Create Table command.</span></span></td></tr>
<tr><td><span data-ttu-id="12984-147">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="12984-147">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="12984-148">Specifica la cartella dell'output di hello hello istruzione INSERT SOVRASCRIVERE.</span><span class="sxs-lookup"><span data-stu-id="12984-148">Specifies hello output folder for hello INSERT OVERWRITE statement.</span></span></td></tr>
<tr><td><span data-ttu-id="12984-149">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="12984-149">${hiveTableName}</span></span></td><td><span data-ttu-id="12984-150">Specifica il nome di hello della tabella Hive hello che fa riferimento a file di dati log4j hello.</span><span class="sxs-lookup"><span data-stu-id="12984-150">Specifies hello name of hello Hive table that references hello log4j data files.</span></span></td></tr>
</table>

<table border = "1">
<tr><th><span data-ttu-id="12984-151">Variabile azione Sqoop</span><span class="sxs-lookup"><span data-stu-id="12984-151">Sqoop action variable</span></span></th><th><span data-ttu-id="12984-152">Descrizione</span><span class="sxs-lookup"><span data-stu-id="12984-152">Description</span></span></th></tr>
<tr><td><span data-ttu-id="12984-153">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="12984-153">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="12984-154">Specifica una stringa di connessione di database SQL di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="12984-154">Specifies hello Azure SQL database connection string.</span></span></td></tr>
<tr><td><span data-ttu-id="12984-155">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="12984-155">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="12984-156">Specifica una tabella di database SQL di Azure hello in cui sono esportati dati hello.</span><span class="sxs-lookup"><span data-stu-id="12984-156">Specifies hello Azure SQL database table where hello data is exported to.</span></span></td></tr>
<tr><td><span data-ttu-id="12984-157">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="12984-157">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="12984-158">Specifica la cartella dell'output di hello hello istruzione INSERT SOVRASCRIVERE l'Hive.</span><span class="sxs-lookup"><span data-stu-id="12984-158">Specifies hello output folder for hello Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="12984-159">Si tratta di hello stessa cartella per l'esportazione Sqoop hello (esportazione-dir).</span><span class="sxs-lookup"><span data-stu-id="12984-159">This is hello same folder for hello Sqoop export (export-dir).</span></span></td></tr>
</table>

<span data-ttu-id="12984-160">Per altre informazioni sul flusso di lavoro di Oozie e sull'uso di azioni del flusso di lavoro, vedere la [documentazione di Apache Oozie 4.0][apache-oozie-400] (per HDInsight versione 3.0) o la [documentazione di Apache Oozie 3.3.2][apache-oozie-332] (per HDInsight versione 2.1).</span><span class="sxs-lookup"><span data-stu-id="12984-160">For more information about Oozie workflow and using workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span></span>

<span data-ttu-id="12984-161">Hello Hive azione nel flusso di lavoro hello chiama un file di script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="12984-161">hello Hive action in hello workflow calls a HiveQL script file.</span></span> <span data-ttu-id="12984-162">che contiene tre istruzioni HiveQL:</span><span class="sxs-lookup"><span data-stu-id="12984-162">This script file contains three HiveQL statements:</span></span>

    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

1. <span data-ttu-id="12984-163">**istruzione DROP TABLE Hello** eliminazioni hello tabella Hive log4j se esiste.</span><span class="sxs-lookup"><span data-stu-id="12984-163">**hello DROP TABLE statement** deletes hello log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="12984-164">**istruzione CREATE TABLE Hello** crea una tabella log4j Hive esterna che fa riferimento il percorso toohello hello log4j del file di log.</span><span class="sxs-lookup"><span data-stu-id="12984-164">**hello CREATE TABLE statement** creates a log4j Hive external table that points toohello location of hello log4j log file.</span></span> <span data-ttu-id="12984-165">delimitatore di campo Hello è ",".</span><span class="sxs-lookup"><span data-stu-id="12984-165">hello field delimiter is ",".</span></span> <span data-ttu-id="12984-166">delimitatore di riga Hello predefinito è "\n".</span><span class="sxs-lookup"><span data-stu-id="12984-166">hello default line delimiter is "\n".</span></span> <span data-ttu-id="12984-167">Una tabella esterna Hive è tooavoid utilizzato i file di dati di hello viene rimosso dalla posizione originale hello se toorun hello Oozie flusso di lavoro più volte.</span><span class="sxs-lookup"><span data-stu-id="12984-167">A Hive external table is used tooavoid hello data file being removed from hello original location if you want toorun hello Oozie workflow multiple times.</span></span>
3. <span data-ttu-id="12984-168">**istruzione INSERT SOVRASCRIVERE Hello** conta le occorrenze di hello di ogni tipo di log a livello di tabella Hive log4j hello e Salva blob tooa output di hello in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="12984-168">**hello INSERT OVERWRITE statement** counts hello occurrences of each log-level type from hello log4j Hive table, and saves hello output tooa blob in Azure Storage.</span></span>

<span data-ttu-id="12984-169">Esistono tre variabili utilizzate nello script hello:</span><span class="sxs-lookup"><span data-stu-id="12984-169">There are three variables used in hello script:</span></span>

* <span data-ttu-id="12984-170">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="12984-170">${hiveTableName}</span></span>
* <span data-ttu-id="12984-171">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="12984-171">${hiveDataFolder}</span></span>
* <span data-ttu-id="12984-172">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="12984-172">${hiveOutputFolder}</span></span>

<span data-ttu-id="12984-173">file di definizione del flusso di lavoro Hello (workflow in questa esercitazione) passa script HiveQL toothis questi valori in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="12984-173">hello workflow definition file (workflow.xml in this tutorial) passes these values toothis HiveQL script at run time.</span></span>

<span data-ttu-id="12984-174">Entrambi i file di flusso di lavoro hello e hello HiveQL vengono archiviati in un contenitore blob.</span><span class="sxs-lookup"><span data-stu-id="12984-174">Both hello workflow file and hello HiveQL file are stored in a blob container.</span></span>  <span data-ttu-id="12984-175">script di PowerShell usare più avanti in questa esercitazione Hello copia sia account di archiviazione di file toohello predefinito.</span><span class="sxs-lookup"><span data-stu-id="12984-175">hello PowerShell script you use later in this tutorial copies both files toohello default Storage account.</span></span> 

## <a name="submit-oozie-jobs-using-powershell"></a><span data-ttu-id="12984-176">Invio di processi Oozie tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="12984-176">Submit Oozie jobs using PowerShell</span></span>
<span data-ttu-id="12984-177">Attualmente Azure PowerShell non fornisce alcun cmdlet per la definizione dei processi Oozie.</span><span class="sxs-lookup"><span data-stu-id="12984-177">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="12984-178">È possibile utilizzare hello **Invoke-RestMethod** cmdlet tooinvoke Oozie i servizi web.</span><span class="sxs-lookup"><span data-stu-id="12984-178">You can use hello **Invoke-RestMethod** cmdlet tooinvoke Oozie web services.</span></span> <span data-ttu-id="12984-179">API dei servizi web di Hello Oozie è un'API di HTTP REST JSON.</span><span class="sxs-lookup"><span data-stu-id="12984-179">hello Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="12984-180">Per ulteriori informazioni sui servizi web di hello Oozie API, vedere [documentazione di Apache Oozie 4.0] [ apache-oozie-400] (per HDInsight versione 3.0) o [documentazione di Apache Oozie 3.3.2] [ apache-oozie-332] (per HDInsight versione 2.1).</span><span class="sxs-lookup"><span data-stu-id="12984-180">For more information about hello Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span></span>

<span data-ttu-id="12984-181">script di PowerShell in questa sezione Hello esegue hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="12984-181">hello PowerShell script in this section performs hello following steps:</span></span>

1. <span data-ttu-id="12984-182">Connettersi tooAzure.</span><span class="sxs-lookup"><span data-stu-id="12984-182">Connect tooAzure.</span></span>
2. <span data-ttu-id="12984-183">Creare un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="12984-183">Create an Azure resource group.</span></span> <span data-ttu-id="12984-184">Per altre informazioni, vedere [Usare Azure PowerShell con Gestione risorse di Azure](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="12984-184">For more information, see [Use Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>
3. <span data-ttu-id="12984-185">Creare un server di Database SQL di Azure, un database SQL Azure e due tabelle.</span><span class="sxs-lookup"><span data-stu-id="12984-185">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> <span data-ttu-id="12984-186">Questi vengono utilizzati dal hello Sqoop azione nel flusso di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="12984-186">These are used by hello Sqoop action in hello workflow.</span></span>
   
    <span data-ttu-id="12984-187">nome della tabella Hello *log4jLogCount*.</span><span class="sxs-lookup"><span data-stu-id="12984-187">hello table name is *log4jLogCount*.</span></span>
4. <span data-ttu-id="12984-188">Creare un toorun cluster usato HDInsight Oozie processi.</span><span class="sxs-lookup"><span data-stu-id="12984-188">Create an HDInsight cluster used toorun Oozie jobs.</span></span>
   
    <span data-ttu-id="12984-189">cluster hello tooexamine, è possibile utilizzare hello portale di Azure o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="12984-189">tooexamine hello cluster, you can use hello Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="12984-190">Copiare i file di flusso di lavoro oozie hello e hello HiveQL script file toohello file system predefinito.</span><span class="sxs-lookup"><span data-stu-id="12984-190">Copy hello oozie workflow file and hello HiveQL script file toohello default file system.</span></span>
   
    <span data-ttu-id="12984-191">Entrambi i file vengono archiviati in un contenitore BLOB pubblico.</span><span class="sxs-lookup"><span data-stu-id="12984-191">Both files are stored in a public Blob container.</span></span>
   
   * <span data-ttu-id="12984-192">Copiare hello HiveQL script (useoozie.hql) tooAzure (wasb:///tutorials/useoozie/useoozie.hql) di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="12984-192">Copy hello HiveQL script (useoozie.hql) tooAzure Storage (wasb:///tutorials/useoozie/useoozie.hql).</span></span>
   * <span data-ttu-id="12984-193">Copiare toowasb:///tutorials/useoozie/workflow.xml workflow.</span><span class="sxs-lookup"><span data-stu-id="12984-193">Copy workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span></span>
   * <span data-ttu-id="12984-194">File di dati di Windows hello (o example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="12984-194">Copy hello data file (/example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span></span>
6. <span data-ttu-id="12984-195">Inviare un processo Oozie.</span><span class="sxs-lookup"><span data-stu-id="12984-195">Submit an Oozie job.</span></span>
   
    <span data-ttu-id="12984-196">risultati del processo tooexamine hello OOzie, utilizzare Visual Studio o altri toohello tooconnect strumenti Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="12984-196">tooexamine hello OOzie job results, use Visual Studio or other tools tooconnect toohello Azure SQL Database.</span></span>

<span data-ttu-id="12984-197">Di seguito è riportato uno script hello.</span><span class="sxs-lookup"><span data-stu-id="12984-197">Here is hello script.</span></span>  <span data-ttu-id="12984-198">È possibile eseguire script hello da Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="12984-198">You can run hello script from Windows PowerShell ISE.</span></span> <span data-ttu-id="12984-199">È necessario solo tooconfigure hello primi 7 variabili.</span><span class="sxs-lookup"><span data-stu-id="12984-199">You only need tooconfigure hello first 7 variables.</span></span>

    #region - provide hello following values

    $subscriptionID = "<Enter your Azure subscription ID>"

    # SQL Database server login credentials used for creating and connecting
    $sqlDatabaseLogin = "<Enter SQL Database Login Name>"
    $sqlDatabasePassword = "<Enter SQL Database Login Password>"

    # HDInsight cluster HTTP user credential used for creating and connectin
    $httpUserName = "admin"  # hello default name is "admin"
    $httpPassword = "<Enter HDInsight Cluster HTTP User Password>"

    # Used for creating Azure service names
    $nameToken = "<Enter an Alias>"
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{
        Login-AzureRmAccount
        Select-AzureRmSubscription -SubscriptionId $subscriptionID
    }
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $sqlLoginCredentials = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $sqlLoginCredentials `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }
    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }
    #endregion

    #region - Create SQL database tables
    Write-Host "Creating hello log4jlogs table  ..." -ForegroundColor Green

    $sqlDatabaseTableName = "log4jLogsCount"
    $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
            [Level] [nvarchar](10) NOT NULL,
            [Total] float,
        CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
        (
        [Level] ASC
        )
        )"

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jCountTable
    $cmd.ExecuteNonQuery()

    $conn.close()
    #endregion

    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - copy Oozie workflow and HiveQL files

    Write-Host "Copy workflow definition and HiveQL script file ..." -ForegroundColor Green

    # Both files are stored in a public Blob
    $publicBlobContext = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here

    Start-CopyAzureStorageBlob `
        -Context $publicBlobContext `
        -SrcContainer "useoozie" `
        -SrcBlob "useooziewf.hql"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -DestBlob "$destFolder/useooziewf.hql" `
        -Force

    Start-CopyAzureStorageBlob `
        -Context $publicBlobContext `
        -SrcContainer "useoozie" `
        -SrcBlob "workflow.xml"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -DestBlob "$destFolder/workflow.xml" `
        -Force

    #validate hello copy
    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/workflow.xml

    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/useooziewf.hql

    #endregion

    #region - copy hello sample.log file

    Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green

    Start-CopyAzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -SrcContainer $defaultBlobContainerName `
        -SrcBlob "example/data/sample.log"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -destBlob "$destFolder/data/sample.log" 

    #validate hello copy
    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/data/sample.log

    #endregion

    #region - submit Oozie job

    $storageUri="wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net"

    $oozieJobName = $namePrefix + "OozieJob"

    #Oozie WF variables
    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $OoziePayload =  @"
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

    <property>
        <name>nameNode</name>
        <value>$storageUrI</value>
    </property>

    <property>
        <name>jobTracker</name>
        <value>jobtrackerhost:9010</value>
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
        <value>$hiveScript</value>
    </property>

    <property>
        <name>hiveTableName</name>
        <value>$hiveTableName</value>
    </property>

    <property>
        <name>hiveDataFolder</name>
        <value>$hiveDataFolder</value>
    </property>

    <property>
        <name>hiveOutputFolder</name>
        <value>$hiveOutputFolder</value>
    </property>

    <property>
        <name>sqlDatabaseConnectionString</name>
        <value>&quot;$sqlDatabaseConnectionString&quot;</value>
    </property>

    <property>
        <name>sqlDatabaseTableName</name>
        <value>$SQLDatabaseTableName</value>
    </property>

    <property>
        <name>user.name</name>
        <value>$httpUserName</value>
    </property>

    <property>
        <name>oozie.wf.application.path</name>
        <value>$oozieWFPath</value>
    </property>

    </configuration>
    "@

    Write-Host "Checking Oozie server status..." -ForegroundColor Green
    $clusterUriStatus = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/admin/status"
    $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $httpCredential -OutVariable $OozieServerStatus

    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $oozieServerSatus = $jsonResponse[0].("systemMode")
    Write-Host "Oozie server status is $oozieServerSatus."

    # create Oozie job
    Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
    Write-Host "`n--------`n$OoziePayload`n--------"
    $clusterUriCreateJob = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/jobs"
    $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $httpCredential -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName #-debug

    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $oozieJobId = $jsonResponse[0].("id")
    Write-Host "Oozie job id is $oozieJobId..."

    # start Oozie job
    Write-Host "Starting hello Oozie job $oozieJobId..." -ForegroundColor Green
    $clusterUriStartJob = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=start"
    $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $httpCredential | Format-Table -HideTableHeaders #-debug

    # get job status
    Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
    Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

    Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
    $clusterUriGetJobStatus = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
    $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $httpCredential
    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $JobStatus = $jsonResponse[0].("status")

    while($JobStatus -notmatch "SUCCEEDED|KILLED")
    {
        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $httpCredential
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")
        $jobStatus
    }

    Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!" -ForegroundColor Green

    #endregion


<span data-ttu-id="12984-200">**esercitazione hello toore esecuzione**</span><span class="sxs-lookup"><span data-stu-id="12984-200">**toore-run hello tutorial**</span></span>

<span data-ttu-id="12984-201">flusso di lavoro hello toore esecuzione, è necessario eliminare hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="12984-201">toore-run hello workflow, you must delete hello following items:</span></span>

* <span data-ttu-id="12984-202">file di output di script Hive Hello</span><span class="sxs-lookup"><span data-stu-id="12984-202">hello Hive script output file</span></span>
* <span data-ttu-id="12984-203">dati Hello nella tabella log4jLogsCount hello</span><span class="sxs-lookup"><span data-stu-id="12984-203">hello data in hello log4jLogsCount table</span></span>

<span data-ttu-id="12984-204">Di seguito è riportato un esempio di script di PowerShell che è possibile utilizzare:</span><span class="sxs-lookup"><span data-stu-id="12984-204">Here is a sample PowerShell script that you can use:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"

    $defaultStorageAccountName = "<AzureStorageAccountName>"
    $defaultBlobContainerName = "<ContainerName>"

    #SQL database variables
    $sqlDatabaseServerName = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabasePassword = "<SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                -ResourceGroupName $resourceGroupName `
                                -Name $defaultStorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $defaultBlobContainerName

    Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = "delete from $sqlDatabaseTableName"
    $cmd.executenonquery()

    $conn.close()

## <a name="next-steps"></a><span data-ttu-id="12984-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="12984-205">Next steps</span></span>
<span data-ttu-id="12984-206">In questa esercitazione, si è appreso come toodefine un Oozie flusso di lavoro e come toorun un Oozie processo tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="12984-206">In this tutorial, you learned how toodefine an Oozie workflow and how toorun an Oozie job by using PowerShell.</span></span> <span data-ttu-id="12984-207">toolearn informazioni, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="12984-207">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="12984-208">[Usare il coordinatore Oozie basato sul tempo con HDInsight][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="12984-208">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="12984-209">[Introduzione all'uso di Hadoop con Hive in uso di HDInsight tooanalyze palmari mobili][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="12984-209">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="12984-210">[Usare l'archivio BLOB di Azure con HDInsight][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="12984-210">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="12984-211">[Amministrare HDInsight con PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="12984-211">[Administer HDInsight using PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="12984-212">[Caricare dati per processi Hadoop in HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="12984-212">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="12984-213">[Usare Sqoop con Hadoop in HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="12984-213">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="12984-214">[Usare Hive con Hadoop in HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="12984-214">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="12984-215">[Usare Pig con Hadoop in HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="12984-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="12984-216">[Sviluppare programmi MapReduce Java per HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="12984-216">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563



[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md


[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: ../sql-database-create-configure.md
[sqldatabase-get-started]: ../sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
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
