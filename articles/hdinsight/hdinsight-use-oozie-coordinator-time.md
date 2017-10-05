---
title: Usare il coordinatore Oozie di Hadoop basato sul tempo in HDInsight | Documentazione Microsoft
description: Usare il coordinatore Oozie di Hadoop basato sul tempo in HDInsight, un servizio per Big Data. Informazioni su come definire i flussi di lavoro e i coordinatori di Oozie e come inviare i processi.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00c3a395-d51a-44ff-af2d-1f116c4b1c83
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 600a70c74a16e2601a874f804ac2e8382c8bfa90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-to-define-workflows-and-coordinate-jobs"></a><span data-ttu-id="2b0cb-104">Usare il coordinatore di Oozie basato sul tempo con Hadoop in HDInsight per definire flussi di lavoro e coordinare processi</span><span class="sxs-lookup"><span data-stu-id="2b0cb-104">Use time-based Oozie coordinator with Hadoop in HDInsight to define workflows and coordinate jobs</span></span>
<span data-ttu-id="2b0cb-105">Questo articolo descrive come definire flussi di lavoro e coordinatori e come attivare i processi del coordinatore in base al tempo.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-105">In this article, you'll learn how to define workflows and coordinators, and how to trigger the coordinator jobs, based on time.</span></span> <span data-ttu-id="2b0cb-106">Prima di procedere può essere utile vedere [Usare Oozie con HDInsight][hdinsight-use-oozie].</span><span class="sxs-lookup"><span data-stu-id="2b0cb-106">It is helpful to go through [Use Oozie with HDInsight][hdinsight-use-oozie] before you read this article.</span></span> <span data-ttu-id="2b0cb-107">Oltre a Oozie, è possibile pianificare processi anche con Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-107">In addition to Oozie, you can also schedule jobs using Azure Data Factory.</span></span> <span data-ttu-id="2b0cb-108">Per informazioni su Azure Data Factory, vedere [Usare Pig e Hive con Data factory](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="2b0cb-108">To learn Azure Data Factory, see [Use Pig and Hive with Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2b0cb-109">Questo articolo richiede un cluster HDInsight basato su Windows.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-109">This article requires a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="2b0cb-110">Per informazioni sull'utilizzo di Oozie, inclusi i processi basati sul tempo, in un cluster basato su Linux, vedere [utilizzo di Oozie con Hadoop per definire ed eseguire un flusso di lavoro in HDInsight basati su Linux](hdinsight-use-oozie-linux-mac.md)</span><span class="sxs-lookup"><span data-stu-id="2b0cb-110">For information on using Oozie, including time-based jobs, on a Linux-based cluster, see [Use Oozie with Hadoop to define and run a workflow on Linux-based HDInsight](hdinsight-use-oozie-linux-mac.md)</span></span>

## <a name="what-is-oozie"></a><span data-ttu-id="2b0cb-111">Informazioni su Oozie</span><span class="sxs-lookup"><span data-stu-id="2b0cb-111">What is Oozie</span></span>
<span data-ttu-id="2b0cb-112">Apache Oozie è un sistema di flusso di lavoro/coordinamento che consente di gestire i processi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-112">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="2b0cb-113">È integrato nello stack di Hadoop e supporta i processi Hadoop per Apache MapReduce, Apache Pig, Apache Hive e Apache Sqoop.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-113">It is integrated with the Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="2b0cb-114">Può anche essere usato per pianificare processi specifici di un sistema, come i programmi Java o gli script della shell.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-114">It can also be used to schedule jobs that are specific to a system, such as Java programs or shell scripts.</span></span>

<span data-ttu-id="2b0cb-115">L'immagine seguente illustra il flusso di lavoro che verrà implementato:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-115">The following image shows the workflow you will implement:</span></span>

![Diagramma del flusso di lavoro][img-workflow-diagram]

<span data-ttu-id="2b0cb-117">Il flusso di lavoro contiene due azioni:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-117">The workflow contains two actions:</span></span>

1. <span data-ttu-id="2b0cb-118">Un'azione di Hive esegue uno script HiveQL per contare le occorrenze di ogni tipo di livello di log in un file log4j.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-118">A Hive action runs a HiveQL script to count the occurrences of each log-level type in a log4j log file.</span></span> <span data-ttu-id="2b0cb-119">Ogni log log4j è costituito da una riga di campi che contiene un campo [LOG LEVEL] per visualizzare il tipo e la gravità. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-119">Each log4j log consists of a line of fields that contains a [LOG LEVEL] field to show the type and the severity, for example:</span></span>

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    <span data-ttu-id="2b0cb-120">L'output dello script Hive è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-120">The Hive script output is similar to:</span></span>

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    <span data-ttu-id="2b0cb-121">Per altre informazioni su Hive, vedere [Usare Hive con HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="2b0cb-121">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="2b0cb-122">Un'azione di Sqoop esporta l'output dell'azione di HiveQL in una tabella di un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-122">A Sqoop action exports the HiveQL action output to a table in an Azure SQL database.</span></span> <span data-ttu-id="2b0cb-123">Per altre informazioni su Sqoop, vedere [Usare Sqoop con HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="2b0cb-123">For more information about Sqoop, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="2b0cb-124">Per informazioni sulle versioni di Oozie supportate nei cluster HDInsight, vedere [Novità delle versioni cluster di Hadoop incluse in HDInsight][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="2b0cb-124">For supported Oozie versions on HDInsight clusters, see [What's new in the cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="2b0cb-125">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2b0cb-125">Prerequisites</span></span>
<span data-ttu-id="2b0cb-126">Prima di iniziare questa esercitazione, è necessario disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-126">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="2b0cb-127">**Workstation con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-127">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2b0cb-128">Il supporto di Azure PowerShell per la gestione delle risorse HDInsight tramite Azure Service Manager è **deprecato** e verrà rimosso dal 1° gennaio 2017.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-128">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="2b0cb-129">La procedura descritta in questo documento usa i nuovi cmdlet HDInsight, compatibili con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-129">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="2b0cb-130">Per installare la versione più recente, seguire la procedura descritta in [Come installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) .</span><span class="sxs-lookup"><span data-stu-id="2b0cb-130">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="2b0cb-131">Se sono presenti script che devono essere modificati per l'uso dei nuovi cmdlet compatibili con Azure Resource Manager, per altre informazioni vedere [Migrazione a strumenti di sviluppo basati su Azure Resource Manager per i cluster HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="2b0cb-131">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="2b0cb-132">**Un cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-132">**An HDInsight cluster**.</span></span> <span data-ttu-id="2b0cb-133">Per informazioni sulla creazione di un cluster HDInsight, vedere [Creare cluster HDInsight][hdinsight-provision] o [Introduzione a HDInsight][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="2b0cb-133">For information about creating an HDInsight cluster, see [Create HDInsight clusters][hdinsight-provision], or [Get started with HDInsight][hdinsight-get-started].</span></span> <span data-ttu-id="2b0cb-134">Per completare l'esercitazione sono necessari i dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-134">You will need the following data to go through the tutorial:</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="2b0cb-135">Proprietà del cluster</span><span class="sxs-lookup"><span data-stu-id="2b0cb-135">Cluster property</span></span></th><th><span data-ttu-id="2b0cb-136">Nome variabile di Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="2b0cb-136">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="2b0cb-137">Valore</span><span class="sxs-lookup"><span data-stu-id="2b0cb-137">Value</span></span></th><th><span data-ttu-id="2b0cb-138">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2b0cb-138">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="2b0cb-139">Nome del cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="2b0cb-139">HDInsight cluster name</span></span></td><td><span data-ttu-id="2b0cb-140">$clusterName</span><span class="sxs-lookup"><span data-stu-id="2b0cb-140">$clusterName</span></span></td><td></td><td><span data-ttu-id="2b0cb-141">Cluster HDInsight su cui si eseguirà questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-141">The HDInsight cluster on which you will run this tutorial.</span></span></td></tr>
    <tr><td><span data-ttu-id="2b0cb-142">Nome utente del cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="2b0cb-142">HDInsight cluster username</span></span></td><td><span data-ttu-id="2b0cb-143">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="2b0cb-143">$clusterUsername</span></span></td><td></td><td><span data-ttu-id="2b0cb-144">Nome utente del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-144">The HDInsight cluster user name.</span></span> </td></tr>
    <tr><td><span data-ttu-id="2b0cb-145">Password utente del cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="2b0cb-145">HDInsight cluster user password</span></span> </td><td><span data-ttu-id="2b0cb-146">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="2b0cb-146">$clusterPassword</span></span></td><td></td><td><span data-ttu-id="2b0cb-147">La password utente del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-147">The HDInsight cluster user password.</span></span></td></tr>
    <tr><td><span data-ttu-id="2b0cb-148">Nome dell'account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="2b0cb-148">Azure storage account name</span></span></td><td><span data-ttu-id="2b0cb-149">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="2b0cb-149">$storageAccountName</span></span></td><td></td><td><span data-ttu-id="2b0cb-150">Un account di archiviazione di Azure disponibile per il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-150">An Azure Storage account available to the HDInsight cluster.</span></span> <span data-ttu-id="2b0cb-151">Ai fini di questa esercitazione, usare l'account di archiviazione predefinito, specificato durante il processo di provisioning del cluster.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-151">For this tutorial, use the default storage account that you specified during the cluster provision process.</span></span></td></tr>
    <tr><td><span data-ttu-id="2b0cb-152">Nome del contenitore BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="2b0cb-152">Azure Blob container name</span></span></td><td><span data-ttu-id="2b0cb-153">$containerName</span><span class="sxs-lookup"><span data-stu-id="2b0cb-153">$containerName</span></span></td><td></td><td><span data-ttu-id="2b0cb-154">Per questo esempio, usare il contenitore di archiviazione BLOB di Azure usato come file system predefinito del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-154">For this example, use the Azure Blob storage container that is used for the default HDInsight cluster file system.</span></span> <span data-ttu-id="2b0cb-155">Per impostazione predefinita, il nome del contenitore corrisponde al nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-155">By default, it has the same name as the HDInsight cluster.</span></span></td></tr>
    </table><span data-ttu-id="2b0cb-156">
* **Un database SQL di Azure**.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-156">
* **An Azure SQL database**.</span></span> <span data-ttu-id="2b0cb-157">È necessario configurare una regola del firewall per il server di database SQL per consentire l'accesso dalla workstation.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-157">You must configure a firewall rule for the SQL Database server to allow access from your workstation.</span></span> <span data-ttu-id="2b0cb-158">Per istruzioni sulla creazione di un database SQL di Azure e sulla configurazione del firewall, vedere [Introduzione al database SQL di Azure][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="2b0cb-158">For instructions about creating an Azure SQL database and configuring the firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> <span data-ttu-id="2b0cb-159">Questo articolo fornisce uno script di Windows PowerShell per consentire la creazione della tabella del database SQL di Azure necessaria per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-159">This article provides a Windows PowerShell script for creating the Azure SQL database table that you need for this tutorial.</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="2b0cb-160">Proprietà del database SQL</span><span class="sxs-lookup"><span data-stu-id="2b0cb-160">SQL database property</span></span></th><th><span data-ttu-id="2b0cb-161">Nome variabile di Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="2b0cb-161">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="2b0cb-162">Valore</span><span class="sxs-lookup"><span data-stu-id="2b0cb-162">Value</span></span></th><th><span data-ttu-id="2b0cb-163">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2b0cb-163">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="2b0cb-164">Nome del server di database SQL</span><span class="sxs-lookup"><span data-stu-id="2b0cb-164">SQL database server name</span></span></td><td><span data-ttu-id="2b0cb-165">$sqlDatabaseServer</span><span class="sxs-lookup"><span data-stu-id="2b0cb-165">$sqlDatabaseServer</span></span></td><td></td><td><span data-ttu-id="2b0cb-166">Il server di database SQL in cui Sqoop esporterà i dati.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-166">The SQL database server to which Sqoop will export data.</span></span> </td></tr>
    <tr><td><span data-ttu-id="2b0cb-167">Nome di accesso al database SQL</span><span class="sxs-lookup"><span data-stu-id="2b0cb-167">SQL database login name</span></span></td><td><span data-ttu-id="2b0cb-168">$sqlDatabaseLogin</span><span class="sxs-lookup"><span data-stu-id="2b0cb-168">$sqlDatabaseLogin</span></span></td><td></td><td><span data-ttu-id="2b0cb-169">Il nome di accesso al database SQL.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-169">SQL Database login name.</span></span></td></tr>
    <tr><td><span data-ttu-id="2b0cb-170">Password di accesso al database SQL</span><span class="sxs-lookup"><span data-stu-id="2b0cb-170">SQL database login password</span></span></td><td><span data-ttu-id="2b0cb-171">$sqlDatabaseLoginPassword</span><span class="sxs-lookup"><span data-stu-id="2b0cb-171">$sqlDatabaseLoginPassword</span></span></td><td></td><td><span data-ttu-id="2b0cb-172">La password di accesso al database SQL.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-172">SQL Database login password.</span></span></td></tr>
    <tr><td><span data-ttu-id="2b0cb-173">Nome del database SQL</span><span class="sxs-lookup"><span data-stu-id="2b0cb-173">SQL database name</span></span></td><td><span data-ttu-id="2b0cb-174">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="2b0cb-174">$sqlDatabaseName</span></span></td><td></td><td><span data-ttu-id="2b0cb-175">Il database SQL di Azure in cui Sqoop esporterà i dati.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-175">The Azure SQL database to which Sqoop will export data.</span></span> </td></tr>
    </table>

  > [!NOTE]
  > <span data-ttu-id="2b0cb-176">Per impostazione predefinita, un database SQL di Azure consente connessioni da servizi di Azure, ad esempio Azure HDinsight.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-176">By default an Azure SQL database allows connections from Azure Services, such as Azure HDInsight.</span></span> <span data-ttu-id="2b0cb-177">Se questa impostazione del firewall è disabilitata, sarà necessario abilitarla nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-177">If this firewall setting is disabled, you must enable it from the Azure Portal.</span></span> <span data-ttu-id="2b0cb-178">Per istruzioni sulla creazione di un database SQL e sulla configurazione di regole del firewall, vedere [Creare e configurare un database SQL][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="2b0cb-178">For instruction about creating a SQL Database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-get-started].</span></span>

> [!NOTE]
> <span data-ttu-id="2b0cb-179">L'inserimento dei valori nelle tabelle</span><span class="sxs-lookup"><span data-stu-id="2b0cb-179">Fill-in the values in the tables.</span></span> <span data-ttu-id="2b0cb-180">potrà essere utile per completare questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-180">It will be helpful for going through this tutorial.</span></span>

## <a name="define-oozie-workflow-and-the-related-hiveql-script"></a><span data-ttu-id="2b0cb-181">Definire il flusso di lavoro di Oozie e il relativo script HiveQL</span><span class="sxs-lookup"><span data-stu-id="2b0cb-181">Define Oozie workflow and the related HiveQL script</span></span>
<span data-ttu-id="2b0cb-182">Le definizioni dei flussi di lavoro di Oozie sono scritte in linguaggio hPDL (XML Process Definition Language).</span><span class="sxs-lookup"><span data-stu-id="2b0cb-182">Oozie workflows definitions are written in hPDL (an XML process definition language).</span></span> <span data-ttu-id="2b0cb-183">Il nome del file del flusso di lavoro predefinito è *workflow.xml*.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-183">The default workflow file name is *workflow.xml*.</span></span>  <span data-ttu-id="2b0cb-184">Il file del flusso di lavoro verrà salvato a livello locale e distribuito nel cluster HDInsight tramite Azure PowerShell più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-184">You will save the workflow file locally, and then deploy it to the HDInsight cluster by using Azure PowerShell later in this tutorial.</span></span>

<span data-ttu-id="2b0cb-185">L'azione di Hive nel flusso di lavoro chiama un file di script HiveQL</span><span class="sxs-lookup"><span data-stu-id="2b0cb-185">The Hive action in the workflow calls a HiveQL script file.</span></span> <span data-ttu-id="2b0cb-186">che contiene tre istruzioni HiveQL:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-186">This script file contains three HiveQL statements:</span></span>

1. <span data-ttu-id="2b0cb-187">**L'istruzione DROP TABLE** consente di eliminare la tabella di Hive log4j, se esistente.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-187">**The DROP TABLE statement** deletes the log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="2b0cb-188">**L'istruzione CREATE TABLE** consente di creare una tabella di Hive log4j esterna che punti al percorso del file di log log4j.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-188">**The CREATE TABLE statement** creates a log4j Hive external table, which points to the location of the log4j log file;</span></span>
3. <span data-ttu-id="2b0cb-189">**Il percorso del file di log log4j**.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-189">**The location of the log4j log file**.</span></span> <span data-ttu-id="2b0cb-190">Il delimitatore di campo è ",".</span><span class="sxs-lookup"><span data-stu-id="2b0cb-190">The field delimiter is ",".</span></span> <span data-ttu-id="2b0cb-191">Il delimitatore di riga predefinito è "\n".</span><span class="sxs-lookup"><span data-stu-id="2b0cb-191">The default line delimiter is "\n".</span></span> <span data-ttu-id="2b0cb-192">La tabella esterna di Hive viene usata per evitare che il file di dati venga rimosso dal percorso originale, nel caso in cui si desideri eseguire il flusso di lavoro di Oozie più volte.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-192">A Hive external table is used to avoid the data file being removed from the original location, in case you want to run the Oozie workflow multiple times.</span></span>
4. <span data-ttu-id="2b0cb-193">**L'istruzione INSERT OVERWRITE** conta le occorrenze di ogni tipo di livello di log nella tabella di Hive log4j e salva l'output in un percorso dell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-193">**The INSERT OVERWRITE statement** counts the occurrences of each log-level type from the log4j Hive table, and it saves the output to an Azure Blob storage location.</span></span>

> [!NOTE]
> <span data-ttu-id="2b0cb-194">Il percorso di Hive è caratterizzato da un problema noto</span><span class="sxs-lookup"><span data-stu-id="2b0cb-194">There is a known Hive path issue.</span></span> <span data-ttu-id="2b0cb-195">che si verifica durante l'invio di un processo Oozie.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-195">You will run into this problem when submitting an Oozie job.</span></span> <span data-ttu-id="2b0cb-196">Le istruzioni per la correzione del problema sono disponibili nell'articolo della sezione Wiki di TechNet [HDInsight Hive error: Unable to rename][technetwiki-hive-error] (Errore di HDInsight Hive "Impossibile rinominare").</span><span class="sxs-lookup"><span data-stu-id="2b0cb-196">The instructions for fixing the issue can be found on the TechNet Wiki: [HDInsight Hive error: Unable to rename][technetwiki-hive-error].</span></span>

<span data-ttu-id="2b0cb-197">**Per definire il file di script HiveQL che deve essere chiamato dal flusso di lavoro**</span><span class="sxs-lookup"><span data-stu-id="2b0cb-197">**To define the HiveQL script file to be called by the workflow**</span></span>

1. <span data-ttu-id="2b0cb-198">Creare un file di testo con il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-198">Create a text file with the following content:</span></span>

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    <span data-ttu-id="2b0cb-199">Nello script vengono usate tre variabili:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-199">There are three variables used in the script:</span></span>

   * <span data-ttu-id="2b0cb-200">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="2b0cb-200">${hiveTableName}</span></span>
   * <span data-ttu-id="2b0cb-201">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="2b0cb-201">${hiveDataFolder}</span></span>
   * <span data-ttu-id="2b0cb-202">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="2b0cb-202">${hiveOutputFolder}</span></span>

     <span data-ttu-id="2b0cb-203">Il file di definizione del flusso di lavoro (workflow.xml in questa esercitazione) passerà questi valori allo script HiveQL in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-203">The workflow definition file (workflow.xml in this tutorial) will pass these values to this HiveQL script at run time.</span></span>
2. <span data-ttu-id="2b0cb-204">Salvare il file come **C:\Tutorials\UseOozie\useooziewf.hql** usando la codifica ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="2b0cb-204">Save the file as **C:\Tutorials\UseOozie\useooziewf.hql** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="2b0cb-205">Usare il blocco note se l'editor di testo non offre questa opzione. Il file di script verrà distribuito nel cluster HDInsight più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-205">(Use Notepad if your text editor doesn't provide this option.) This script file will be deployed to the HDInsight cluster later in the tutorial.</span></span>

<span data-ttu-id="2b0cb-206">**Per definire un flusso di lavoro**</span><span class="sxs-lookup"><span data-stu-id="2b0cb-206">**To define a workflow**</span></span>

1. <span data-ttu-id="2b0cb-207">Creare un file di testo con il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-207">Create a text file with the following content:</span></span>

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
    ```

    <span data-ttu-id="2b0cb-208">Nel flusso di lavoro vengono definite due azioni.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-208">There are two actions defined in the workflow.</span></span> <span data-ttu-id="2b0cb-209">L'azione start-to è *RunHiveScript*.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-209">The start-to action is *RunHiveScript*.</span></span> <span data-ttu-id="2b0cb-210">Se l'azione viene eseguita *correttamente*, l'azione successiva è *RunSqoopExport*.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-210">If the action runs *OK*, the next action is *RunSqoopExport*.</span></span>

    <span data-ttu-id="2b0cb-211">RunHiveScript è caratterizzato da diverse variabili.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-211">The RunHiveScript has several variables.</span></span> <span data-ttu-id="2b0cb-212">I valori verranno passati quando si invia il processo Oozie dalla workstation con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-212">You will pass the values when you submit the Oozie job from your workstation by using Azure PowerShell.</span></span>

    <span data-ttu-id="2b0cb-213">Variabili del flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="2b0cb-213">Workflow variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="2b0cb-214">Variabili del flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="2b0cb-214">Workflow variables</span></span></th><th><span data-ttu-id="2b0cb-215">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2b0cb-215">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="2b0cb-216">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="2b0cb-216">${jobTracker}</span></span></td><td><span data-ttu-id="2b0cb-217">Specifica l'URL dell'utilità di analisi dei processi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-217">Specify the URL of the Hadoop job tracker.</span></span> <span data-ttu-id="2b0cb-218">Usare <strong>jobtrackerhost:9010</strong> nel cluster HDInsight versione 3.0 e 2.0.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-218">Use <strong>jobtrackerhost:9010</strong> on HDInsight cluster version 3.0 and 2.0.</span></span></td></tr>
    <tr><td><span data-ttu-id="2b0cb-219">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="2b0cb-219">${nameNode}</span></span></td><td><span data-ttu-id="2b0cb-220">Specifica l'URL del nodo dei nomi di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-220">Specify the URL of the Hadoop name node.</span></span> <span data-ttu-id="2b0cb-221">Usare l'indirizzo wasb:// del file system predefinito, ad esempio <i>wasb://&lt;nomecontenitore&gt;@&lt;nomeaccountarchiviazione&gt;.blob.core.windows.net</i>.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-221">Use the default file system wasb:// address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
    <tr><td><span data-ttu-id="2b0cb-222">${queueName}</span><span class="sxs-lookup"><span data-stu-id="2b0cb-222">${queueName}</span></span></td><td><span data-ttu-id="2b0cb-223">Consente di specificare il nome della coda alla quale verrà inviato il processo.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-223">Specifies the queue name that the job will be submitted to.</span></span> <span data-ttu-id="2b0cb-224">Usare l'<strong>impostazione predefinita</strong>.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-224">Use <strong>default</strong>.</span></span></td></tr>
    </table>

    <span data-ttu-id="2b0cb-225">Variabili dell'azione Hive</span><span class="sxs-lookup"><span data-stu-id="2b0cb-225">Hive action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="2b0cb-226">Variabile azione Hive</span><span class="sxs-lookup"><span data-stu-id="2b0cb-226">Hive action variable</span></span></th><th><span data-ttu-id="2b0cb-227">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2b0cb-227">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="2b0cb-228">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="2b0cb-228">${hiveDataFolder}</span></span></td><td><span data-ttu-id="2b0cb-229">La directory di origine per il comando Hive Create Table.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-229">The source directory for the Hive Create Table command.</span></span></td></tr>
    <tr><td><span data-ttu-id="2b0cb-230">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="2b0cb-230">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="2b0cb-231">La cartella di output per l'istruzione INSERT OVERWRITE.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-231">The output folder for the INSERT OVERWRITE statement.</span></span></td></tr>
    <tr><td><span data-ttu-id="2b0cb-232">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="2b0cb-232">${hiveTableName}</span></span></td><td><span data-ttu-id="2b0cb-233">Il nome della tabella di Hive che fa riferimento ai file di dati log4j.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-233">The name of the Hive table that references the log4j data files.</span></span></td></tr>
    </table>

    <span data-ttu-id="2b0cb-234">Variabili dell'azione Sqoop</span><span class="sxs-lookup"><span data-stu-id="2b0cb-234">Sqoop action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="2b0cb-235">Variabile azione Sqoop</span><span class="sxs-lookup"><span data-stu-id="2b0cb-235">Sqoop action variable</span></span></th><th><span data-ttu-id="2b0cb-236">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2b0cb-236">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="2b0cb-237">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="2b0cb-237">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="2b0cb-238">Stringa di connessione del database SQL.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-238">SQL Database connection string.</span></span></td></tr>
    <tr><td><span data-ttu-id="2b0cb-239">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="2b0cb-239">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="2b0cb-240">La tabella del database SQL di Azure in cui verranno esportati i dati.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-240">The Azure SQL database table to where the data will be exported.</span></span></td></tr>
    <tr><td><span data-ttu-id="2b0cb-241">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="2b0cb-241">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="2b0cb-242">La cartella di output per l'istruzione INSERT OVERWRITE di Hive.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-242">The output folder for the Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="2b0cb-243">È la stessa cartella dell'esportazione tramite Sqoop (export-dir).</span><span class="sxs-lookup"><span data-stu-id="2b0cb-243">This is the same folder for the Sqoop export (export-dir).</span></span></td></tr>
    </table>

    <span data-ttu-id="2b0cb-244">Per altre informazioni sul flusso di lavoro di Oozie e sull'uso di azioni del flusso di lavoro, vedere la [documentazione di Apache Oozie 4.0][apache-oozie-400] (per cluster HDInsight versione 3.0) o la [documentazione di Apache Oozie 3.3.2][apache-oozie-332] (per cluster HDInsight versione 2.1).</span><span class="sxs-lookup"><span data-stu-id="2b0cb-244">For more information about Oozie workflow and using the workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

1. <span data-ttu-id="2b0cb-245">Salvare il file come **C:\Tutorials\UseOozie\workflow.xml** usando la codifica ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="2b0cb-245">Save the file as **C:\Tutorials\UseOozie\workflow.xml** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="2b0cb-246">Usare il blocco note se l'editor di testo non offre questa opzione.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-246">(Use Notepad if your text editor doesn't provide this option.)</span></span>

<span data-ttu-id="2b0cb-247">**Per definire il coordinatore**</span><span class="sxs-lookup"><span data-stu-id="2b0cb-247">**To define coordinator**</span></span>

1. <span data-ttu-id="2b0cb-248">Creare un file di testo con il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-248">Create a text file with the following content:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    <span data-ttu-id="2b0cb-249">Nel file di definizione vengono usate cinque variabili:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-249">There are five variables used in the definition file:</span></span>

   | <span data-ttu-id="2b0cb-250">Variabile</span><span class="sxs-lookup"><span data-stu-id="2b0cb-250">Variable</span></span> | <span data-ttu-id="2b0cb-251">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2b0cb-251">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="2b0cb-252">${coordFrequency}</span><span class="sxs-lookup"><span data-stu-id="2b0cb-252">${coordFrequency}</span></span> |<span data-ttu-id="2b0cb-253">Tempo di sospensione del processo.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-253">Job pause time.</span></span> <span data-ttu-id="2b0cb-254">La frequenza è sempre espressa in minuti.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-254">Frequency is always expressed in minutes.</span></span> |
   | <span data-ttu-id="2b0cb-255">${coordStart}</span><span class="sxs-lookup"><span data-stu-id="2b0cb-255">${coordStart}</span></span> |<span data-ttu-id="2b0cb-256">Ora di inizio del processo.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-256">Job start time.</span></span> |
   | <span data-ttu-id="2b0cb-257">${coordEnd}</span><span class="sxs-lookup"><span data-stu-id="2b0cb-257">${coordEnd}</span></span> |<span data-ttu-id="2b0cb-258">Ora di fine del processo.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-258">Job end time.</span></span> |
   | <span data-ttu-id="2b0cb-259">${coordTimezone}</span><span class="sxs-lookup"><span data-stu-id="2b0cb-259">${coordTimezone}</span></span> |<span data-ttu-id="2b0cb-260">Oozie elabora i processi del coordinatore in un fuso orario predefinito che non tiene conto dell'ora legale (in genere rappresentato dall'acronimo UTC).</span><span class="sxs-lookup"><span data-stu-id="2b0cb-260">Oozie processes coordinator jobs in a fixed time zone with no daylight saving time (typically represented by using UTC).</span></span> <span data-ttu-id="2b0cb-261">Questo fuso orario viene definito "Fuso orario di elaborazione Oozie".</span><span class="sxs-lookup"><span data-stu-id="2b0cb-261">This time zone is referred as the "Oozie processing timezone."</span></span> |
   | <span data-ttu-id="2b0cb-262">${wfPath}</span><span class="sxs-lookup"><span data-stu-id="2b0cb-262">${wfPath}</span></span> |<span data-ttu-id="2b0cb-263">Percorso del file workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-263">The path for the workflow.xml.</span></span>  <span data-ttu-id="2b0cb-264">Se il nome file del flusso di lavoro non è quello predefinito (workflow.xml) sarà necessario specificarlo.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-264">If the workflow file name is not the default file name (workflow.xml), you must specify it.</span></span> |
2. <span data-ttu-id="2b0cb-265">Salvare il file come **C:\Tutorials\UseOozie\coordinator.xml** usando la codifica ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="2b0cb-265">Save the file as **C:\Tutorials\UseOozie\coordinator.xml** by using the ANSI (ASCII) encoding.</span></span> <span data-ttu-id="2b0cb-266">Usare il blocco note se l'editor di testo non offre questa opzione.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-266">(Use Notepad if your text editor doesn't provide this option.)</span></span>

## <a name="deploy-the-oozie-project-and-prepare-the-tutorial"></a><span data-ttu-id="2b0cb-267">Distribuzione del progetto Oozie e operazioni preliminari all'esercitazione</span><span class="sxs-lookup"><span data-stu-id="2b0cb-267">Deploy the Oozie project and prepare the tutorial</span></span>
<span data-ttu-id="2b0cb-268">Eseguire uno script di Azure PowerShell per completare le seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-268">You will run an Azure PowerShell script to perform the following:</span></span>

* <span data-ttu-id="2b0cb-269">Copiare lo script di HiveQL (useoozie.hql) nell'archivio BLOB di Azure: wasb:///tutorials/useoozie/useoozie.hql.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-269">Copy the HiveQL script (useoozie.hql) to Azure Blob storage, wasb:///tutorials/useoozie/useoozie.hql.</span></span>
* <span data-ttu-id="2b0cb-270">Copiare il file workflow.xml in wasb:///tutorials/useoozie/workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-270">Copy workflow.xml to wasb:///tutorials/useoozie/workflow.xml.</span></span>
* <span data-ttu-id="2b0cb-271">Copiare il file coordinator.xml in wasb:///tutorials/useoozie/coordinator.xml.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-271">Copy coordinator.xml to wasb:///tutorials/useoozie/coordinator.xml.</span></span>
* <span data-ttu-id="2b0cb-272">Copiare il file di dati (/example/data/sample.log) in wasb:///tutorials/useoozie/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-272">Copy the data file (/example/data/sample.log) to wasb:///tutorials/useoozie/data/sample.log.</span></span>
* <span data-ttu-id="2b0cb-273">Creare una tabella di database SQL di Azure per l'archiviazione dei dati di esportazione di Sqoop.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-273">Create an Azure SQL database table for storing Sqoop export data.</span></span> <span data-ttu-id="2b0cb-274">Il nome della tabella è *log4jLogCount*.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-274">The table name is *log4jLogCount*.</span></span>

<span data-ttu-id="2b0cb-275">**Informazioni sull'archiviazione in HDInsight**</span><span class="sxs-lookup"><span data-stu-id="2b0cb-275">**Understand HDInsight storage**</span></span>

<span data-ttu-id="2b0cb-276">HDInsight usa l'archiviazione BLOB di Azure per l'archiviazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-276">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="2b0cb-277">wasb:// è l'implementazione Microsoft di HDFS (Hadoop Distributed File System) nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-277">wasb:// is Microsoft's implementation of the Hadoop distributed file system (HDFS) in Azure Blob storage.</span></span> <span data-ttu-id="2b0cb-278">Per altre informazioni, vedere [Usare l'archivio BLOB di Azure con HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="2b0cb-278">For more information, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="2b0cb-279">Quando si effettua il provisioning di un cluster HDInsight, vengono designati come file system predefinito un account di archiviazione BLOB di Azure e un contenitore specifico di tale account, proprio come in HDFS.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-279">When you provision an HDInsight cluster, an Azure Blob storage account and a specific container from that account is designated as the default file system, like in HDFS.</span></span> <span data-ttu-id="2b0cb-280">Oltre a questo account di archiviazione, durante il processo di provisioning è possibile aggiungere anche altri account di archiviazione provenienti dalla stessa sottoscrizione di Azure o da sottoscrizioni di Azure diverse.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-280">In addition to this storage account, you can add additional storage accounts from the same Azure subscription or from different Azure subscriptions during the provisioning process.</span></span> <span data-ttu-id="2b0cb-281">Per istruzioni sull'aggiunta di altri account di archiviazione, vedere [Effettuare il provisioning di cluster HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="2b0cb-281">For instructions about adding additional storage accounts, see [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="2b0cb-282">Per semplificare lo script di Azure PowerShell usato in questa esercitazione, tutti i file vengono archiviati nel contenitore del file system predefinito, presente in */tutorials/useoozie*.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-282">To simplify the Azure PowerShell script used in this tutorial, all of the files are stored in the default file system container located at */tutorials/useoozie*.</span></span> <span data-ttu-id="2b0cb-283">Per impostazione predefinita, il nome di questo contenitore corrisponde al nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-283">By default, this container has the same name as the HDInsight cluster name.</span></span>
<span data-ttu-id="2b0cb-284">La sintassi è:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-284">The syntax is:</span></span>

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> <span data-ttu-id="2b0cb-285">Nella versione 3.0 del cluster HDInsight è supportata solo la sintassi *wasb://*.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-285">Only the *wasb://* syntax is supported in HDInsight cluster version 3.0.</span></span> <span data-ttu-id="2b0cb-286">La sintassi *asv://* precedente è supportata nei cluster HDInsight 2.1 e 1.6, ma non è supportata nei cluster HDInsight 3.0 e non sarà supportata nelle versioni successive.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-286">The older *asv://* syntax is supported in HDInsight 2.1 and 1.6 clusters, but it is not supported in HDInsight 3.0 clusters.</span></span>
>
> <span data-ttu-id="2b0cb-287">Il percorso wasb:// è un percorso virtuale.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-287">The wasb:// path is a virtual path.</span></span> <span data-ttu-id="2b0cb-288">Per altre informazioni, vedere [Usare l'archivio BLOB di Azure con HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="2b0cb-288">For more information see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="2b0cb-289">È possibile accedere da HDInsight a un file archiviato nel contenitore del file system predefinito usando uno degli URI seguenti (in questo esempio si userà workflow.xml):</span><span class="sxs-lookup"><span data-stu-id="2b0cb-289">A file that is stored in the default file system container can be accessed from HDInsight by using any of the following URIs (I am using workflow.xml as an example):</span></span>

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

<span data-ttu-id="2b0cb-290">Per accedere al file direttamente dall'account di archiviazione, il nome del BLOB per questo file è:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-290">If you want to access the file directly from the storage account, the blob name for the file is:</span></span>

    tutorials/useoozie/workflow.xml

<span data-ttu-id="2b0cb-291">**Informazioni sulle tabelle interne ed esterne di Hive**</span><span class="sxs-lookup"><span data-stu-id="2b0cb-291">**Understand Hive internal and external tables**</span></span>

<span data-ttu-id="2b0cb-292">Relativamente alle tabelle interne ed esterne di Hive è importante conoscere alcune informazioni:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-292">There are a few things you need to know about Hive internal and external tables:</span></span>

* <span data-ttu-id="2b0cb-293">Il comando CREATE TABLE consente di creare una tabella interna, nota anche come tabella gestita.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-293">The CREATE TABLE command creates an internal table, also known as a managed table.</span></span> <span data-ttu-id="2b0cb-294">Il file di dati deve trovarsi nel contenitore predefinito.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-294">The data file must be located in the default container.</span></span>
* <span data-ttu-id="2b0cb-295">Il comando CREATE TABLE consente di spostare il file di dati nella cartella /hive/warehouse/<TableName> del contenitore predefinito.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-295">The CREATE TABLE command moves the data file to the /hive/warehouse/<TableName> folder in the default container.</span></span>
* <span data-ttu-id="2b0cb-296">Il comando CREATE EXTERNAL TABLE consente di creare una tabella esterna.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-296">The CREATE EXTERNAL TABLE command creates an external table.</span></span> <span data-ttu-id="2b0cb-297">Il file di dati può trovarsi all'esterno del contenitore predefinito.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-297">The data file can be located outside the default container.</span></span>
* <span data-ttu-id="2b0cb-298">Il comando CREATE EXTERNAL TABLE non consente di spostare il file di dati.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-298">The CREATE EXTERNAL TABLE command does not move the data file.</span></span>
* <span data-ttu-id="2b0cb-299">Il comando CREATE EXTERNAL TABLE non consente di creare sottocartelle nella cartella specificata nella clausola LOCATION.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-299">The CREATE EXTERNAL TABLE command doesn't allow any subfolders under the folder that is specified in the LOCATION clause.</span></span> <span data-ttu-id="2b0cb-300">È per questo motivo che nell'esercitazione si esegue una copia del file sample.log.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-300">This is the reason why the tutorial makes a copy of the sample.log file.</span></span>

<span data-ttu-id="2b0cb-301">Per altre informazioni, vedere [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables] (HDInsight: introduzione alle tabelle Hive interne ed esterne).</span><span class="sxs-lookup"><span data-stu-id="2b0cb-301">For more information, see [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables].</span></span>

<span data-ttu-id="2b0cb-302">**Operazioni preliminari all'esercitazione**</span><span class="sxs-lookup"><span data-stu-id="2b0cb-302">**To prepare the tutorial**</span></span>

1. <span data-ttu-id="2b0cb-303">Aprire Windows PowerShell ISE. A questo scopo, nella schermata Start di Windows 8 digitare **PowerShell_ISE** e quindi fare clic su **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-303">Open the Windows PowerShell ISE (in the Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="2b0cb-304">Per altre informazioni, vedere [Start Windows PowerShell on Windows 8 and Windows][powershell-start] (Avviare Windows PowerShell in Windows 8 e Windows).</span><span class="sxs-lookup"><span data-stu-id="2b0cb-304">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="2b0cb-305">Nel riquadro inferiore eseguire questo comando per connettersi alla sottoscrizione di Azure:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-305">In the bottom pane, run the following command to connect to your Azure subscription:</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="2b0cb-306">Verrà richiesto di immettere le credenziali dell'account Azure.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-306">You will be prompted to enter your Azure account credentials.</span></span> <span data-ttu-id="2b0cb-307">Questo metodo, che prevede l'aggiunta di una connessione alla sottoscrizione, scade dopo 12 ore, di conseguenza sarà necessario eseguire nuovamente il cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-307">This method of adding a subscription connection times out, and after 12 hours, you will have to run the cmdlet again.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2b0cb-308">Se si dispone di più sottoscrizioni di Azure e non si desidera usare quella predefinita, eseguire il cmdlet <strong>Select-AzureSubscription</strong> per selezionare una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-308">If you have multiple Azure subscriptions and the default subscription is not the one you want to use, use the <strong>Select-AzureSubscription</strong> cmdlet to select a subscription.</span></span>

3. <span data-ttu-id="2b0cb-309">Copiare lo script seguente nel riquadro di script e impostare le prime sei variabili:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-309">Copy the following script into the script pane, and then set the first six variables:</span></span>

    ```powershell
    # WASB variables
    $storageAccountName = "<StorageAccountName>"
    $containerName = "<BlobStorageContainerName>"

    # SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    # Oozie files for the tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing the Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use the long path here
    ```

    <span data-ttu-id="2b0cb-310">Per altre descrizioni di queste variabili, vedere la sezione [Prerequisiti](#prerequisites) di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-310">For more descriptions of the variables, see the [Prerequisites](#prerequisites) section in this tutorial.</span></span>

4. <span data-ttu-id="2b0cb-311">Aggiungere il codice seguente allo script nel relativo riquadro:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-311">Append the following to the script in the script pane:</span></span>

    ```powershell
    # Create a storage context object
    $storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

    function uploadOozieFiles()
    {
        Write-Host "Copy HiveQL script, workflow definition and coordinator definition ..." -ForegroundColor Green
        Set-AzureStorageBlobContent -File $hiveQLScript -Container $containerName -Blob "$destFolder/useooziewf.hql" -Context $destContext
        Set-AzureStorageBlobContent -File $workflowDefinition -Container $containerName -Blob "$destFolder/workflow.xml" -Context $destContext
        Set-AzureStorageBlobContent -File $coordDefinition -Container $containerName -Blob "$destFolder/coordinator.xml" -Context $destContext
    }

    function prepareHiveDataFile()
    {
        Write-Host "Make a copy of the sample.log file ... " -ForegroundColor Green
        Start-CopyAzureStorageBlob -SrcContainer $containerName -SrcBlob "example/data/sample.log" -Context $destContext -DestContainer $containerName -destBlob "$destFolder/data/sample.log" -DestContext $destContext
    }

    function prepareSQLDatabase()
    {
        # SQL query string for creating log4jLogsCount table
        $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [Level] [nvarchar](10) NOT NULL,
                [Total] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
            [Level] ASC
            )
            )"

        #Create the log4jLogsCount table
        Write-Host "Create Log4jLogsCount table ..." -ForegroundColor Green
        $conn = New-Object System.Data.SqlClient.SqlConnection
        $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
        $conn.open()
        $cmd = New-Object System.Data.SqlClient.SqlCommand
        $cmd.connection = $conn
        $cmd.commandtext = $cmdCreateLog4jCountTable
        $cmd.executenonquery()

        $conn.close()
    }

    # upload workflow.xml, coordinator.xml, and ooziewf.hql
    uploadOozieFiles;

    # make a copy of example/data/sample.log to example/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. <span data-ttu-id="2b0cb-312">Fare clic su **Esegui script** o premere **F5** per eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-312">Click **Run Script** or press **F5** to run the script.</span></span> <span data-ttu-id="2b0cb-313">L'output sarà analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-313">The output will be similar to:</span></span>

    ![Output delle operazioni preliminari all'esercitazione][img-preparation-output]

## <a name="run-the-oozie-project"></a><span data-ttu-id="2b0cb-315">Eseguire il progetto Oozie</span><span class="sxs-lookup"><span data-stu-id="2b0cb-315">Run the Oozie project</span></span>
<span data-ttu-id="2b0cb-316">Attualmente Azure PowerShell non fornisce alcun cmdlet per la definizione dei processi Oozie.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-316">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="2b0cb-317">È possibile usare il cmdlet **Invoke-RestMethod** per richiamare i servizi Web di Oozie.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-317">You can use the **Invoke-RestMethod** cmdlet to invoke Oozie web services.</span></span> <span data-ttu-id="2b0cb-318">L'API dei servizi Web di Oozie è una API HTTP REST JSON.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-318">The Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="2b0cb-319">Per altre informazioni sull'API dei servizi Web di Oozie, vedere la [documentazione di Apache Oozie 4.0][apache-oozie-400] (per cluster HDInsight versione 3.0) o la [documentazione di Apache Oozie 3.3.2][apache-oozie-332] (per cluster HDInsight versione 2.1).</span><span class="sxs-lookup"><span data-stu-id="2b0cb-319">For more information about the Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

<span data-ttu-id="2b0cb-320">**Per inviare un processo Oozie**</span><span class="sxs-lookup"><span data-stu-id="2b0cb-320">**To submit an Oozie job**</span></span>

1. <span data-ttu-id="2b0cb-321">Aprire Windows PowerShell ISE. A questo scopo, nella schermata Start di Windows 8 digitare **PowerShell_ISE** e quindi fare clic su **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-321">Open the Windows PowerShell ISE (in Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="2b0cb-322">Per altre informazioni, vedere [Start Windows PowerShell on Windows 8 and Windows][powershell-start] (Avviare Windows PowerShell in Windows 8 e Windows).</span><span class="sxs-lookup"><span data-stu-id="2b0cb-322">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="2b0cb-323">Copiare lo script seguente nel riquadro di script e impostare le prime 14 variabili (ignorare **$storageUri**).</span><span class="sxs-lookup"><span data-stu-id="2b0cb-323">Copy the following script into the script pane, and then set the first fourteen variables (however, skip **$storageUri**).</span></span>

    ```powershell
    #HDInsight cluster variables
    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterUserPassword>"

    #Azure Blob storage (WASB) variables
    $storageAccountName = "<StorageAccountName>"
    $storageContainerName = "<BlobContainerName>"
    $storageUri="wasb://$storageContainerName@$storageAccountName.blob.core.windows.net"

    #Azure SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "<SQLDatabaseloginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"

    #Oozie WF/coordinator variables
    $coordStart = "2014-03-21T13:45Z"
    $coordEnd = "2014-03-21T13:45Z"
    $coordFrequency = "1440"    # in minutes, 24h x 60m = 1440m
    $coordTimezone = "UTC"    #UTC/GMT

    $oozieWFPath="$storageUri/tutorials/useoozie"  # The default name is workflow.xml. And you don't need to specify the file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServer.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServer;password=$sqlDatabaseLoginPassword;database=$sqlDatabaseName"
    $sqlDatabaseTableName = "log4jLogsCount"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)
    ```

    <span data-ttu-id="2b0cb-324">Per altre descrizioni di queste variabili, vedere la sezione [Prerequisiti](#prerequisites) di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-324">For more descriptions of the variables, see the [Prerequisites](#prerequisites) section in this tutorial.</span></span>

    <span data-ttu-id="2b0cb-325">$coordstart e $coordend indicano l'ora di inizio e di fine del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-325">$coordstart and $coordend are the workflow starting and ending time.</span></span> <span data-ttu-id="2b0cb-326">Per individuare l'ora UTC/GMT, cercare "ora utc" in bing.com. Il valore di $coordFrequency corrisponde alla frequenza in minuti in base alla quale si vuole eseguire il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-326">To find out the UTC/GMT time, search "utc time" on bing.com. The $coordFrequency is how often in minutes you want to run the workflow.</span></span>
3. <span data-ttu-id="2b0cb-327">Aggiungere il codice seguente allo script.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-327">Append the following to the script.</span></span> <span data-ttu-id="2b0cb-328">Questa parte definisce il payload di Oozie:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-328">This part defines the Oozie payload:</span></span>

    ```powershell
    #OoziePayload used for Oozie web service submission
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
            <name>oozie.coord.application.path</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>wfPath</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>coordStart</name>
            <value>$coordStart</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>$coordEnd</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>$coordFrequency</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>$coordTimezone</value>
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
            <value>admin</value>
        </property>

    </configuration>
    "@
    ```

   > [!NOTE]
   > <span data-ttu-id="2b0cb-329">La differenza principale rispetto al file di payload di invio del flusso di lavoro è la variabile **oozie.coord.application.path**.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-329">The major difference compared to the workflow submission payload file is the variable **oozie.coord.application.path**.</span></span> <span data-ttu-id="2b0cb-330">Quando si invia un processo del flusso di lavoro si usa invece la variabile **oozie.wf.application.path** .</span><span class="sxs-lookup"><span data-stu-id="2b0cb-330">When you submit a workflow job, you use **oozie.wf.application.path** instead.</span></span>

4. <span data-ttu-id="2b0cb-331">Aggiungere il codice seguente allo script.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-331">Append the following to the script.</span></span> <span data-ttu-id="2b0cb-332">Questa parte consente di verificare lo stato del servizio Web Oozie:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-332">This part checks the Oozie web service status:</span></span>

    ```powershell
    function checkOozieServerStatus()
    {
        Write-Host "Checking Oozie server status..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/admin/status"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds -OutVariable $OozieServerStatus

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieServerSatus = $jsonResponse[0].("systemMode")
        Write-Host "Oozie server status is $oozieServerSatus..."

        if($oozieServerSatus -notmatch "NORMAL")
        {
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check the server status and re-run the job."
            exit 1
        }
    }
    ```

5. <span data-ttu-id="2b0cb-333">Aggiungere il codice seguente allo script.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-333">Append the following to the script.</span></span> <span data-ttu-id="2b0cb-334">Questa parte consente di creare un processo Oozie:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-334">This part creates an Oozie job:</span></span>

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending the following Payload to the cluster:" -ForegroundColor Green
        Write-Host "`n--------`n$OoziePayload`n--------"
        $clusterUriCreateJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $creds -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName -debug -Verbose

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieJobId = $jsonResponse[0].("id")
        Write-Host "Oozie job id is $oozieJobId..."

        return $oozieJobId
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="2b0cb-335">Quando si invia un processo del flusso di lavoro, è necessario creare un'altra chiamata del servizio Web per avviare il processo dopo che questo è stato creato.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-335">When you submit a workflow job, you must make another web service call to start the job after the job is created.</span></span> <span data-ttu-id="2b0cb-336">In tal caso, il processo del coordinatore viene attivato dal tempo.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-336">In this case, the coordinator job is triggered by time.</span></span> <span data-ttu-id="2b0cb-337">Il processo verrà avviato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-337">The job will start automatically.</span></span>

6. <span data-ttu-id="2b0cb-338">Aggiungere il codice seguente allo script.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-338">Append the following to the script.</span></span> <span data-ttu-id="2b0cb-339">Questa parte consente di verificare lo stato del processo Oozie:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-339">This part checks the Oozie job status:</span></span>

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until the job metadata is populated in the Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for the job to complete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for the job to complete..."
            Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
            $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
            $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
            $JobStatus = $jsonResponse[0].("status")
        }

        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!"
        if($JobStatus -notmatch "SUCCEEDED")
        {
            Write-Host "Check logs at http://headnode0:9014/cluster for detais."
            exit -1
        }
    }
    ```

7. <span data-ttu-id="2b0cb-340">(Facoltativo) Aggiungere il codice seguente allo script.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-340">(Optional) Append the following to the script.</span></span>

    ```powershell
    function listOozieJobs()
    {
        Write-Host "Listing Oozie jobs..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds

        write-host "Job ID                                   App Name        Status      Started                         Ended"
        write-host "----------------------------------------------------------------------------------------------------------------------------------"
        foreach($job in $response.workflows)
        {
            Write-Host $job.id "`t" $job.appName "`t" $job.status "`t" $job.startTime "`t" $job.endTime
        }
    }

    function ShowOozieJobLog($oozieJobId)
    {
        Write-Host "Showing Oozie job info..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/$oozieJobId" + "?show=log"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds
        write-host $response
    }

    function killOozieJob($oozieJobId)
    {
        Write-Host "Killing the Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for the 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. <span data-ttu-id="2b0cb-341">Aggiungere il codice seguente allo script:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-341">Append the following to the script:</span></span>

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    <span data-ttu-id="2b0cb-342">Rimuovere i segni # se si desidera eseguire le funzioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-342">Remove the # signs if you want to run the additional functions.</span></span>
9. <span data-ttu-id="2b0cb-343">Se si usa la versione 2.1 del cluster HDinsight, sostituire "https://$clusterName.azurehdinsight.net:443/oozie/v2/" con "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span><span class="sxs-lookup"><span data-stu-id="2b0cb-343">If your HDinsight cluster is version 2.1, replace "https://$clusterName.azurehdinsight.net:443/oozie/v2/" with "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span></span> <span data-ttu-id="2b0cb-344">La versione 2.1 del cluster HDInsight non supporta la versione 2 dei servizi Web.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-344">HDInsight cluster version 2.1 does not supports version 2 of the web services.</span></span>
10. <span data-ttu-id="2b0cb-345">Fare clic su **Esegui script** o premere **F5** per eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-345">Click **Run Script** or press **F5** to run the script.</span></span> <span data-ttu-id="2b0cb-346">L'output sarà analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-346">The output will be similar to:</span></span>

     ![Output dell'esecuzione del flusso di lavoro nell'esercitazione][img-runworkflow-output]
11. <span data-ttu-id="2b0cb-348">Connettersi al database SQL per visualizzare i dati esportati.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-348">Connect to your SQL Database to see the exported data.</span></span>

<span data-ttu-id="2b0cb-349">**Per verificare il log degli errori del processo**</span><span class="sxs-lookup"><span data-stu-id="2b0cb-349">**To check the job error log**</span></span>

<span data-ttu-id="2b0cb-350">Per risolvere i problemi relativi a un flusso di lavoro, consultare il file di log di Oozie in C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log dal nodo head del cluster.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-350">To troubleshoot a workflow, the Oozie log file can be found at C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log from the cluster headnode.</span></span> <span data-ttu-id="2b0cb-351">Per informazioni su RDP vedere l'articolo su come [amministrare cluster HDInsight con il portale di Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="2b0cb-351">For information on RDP, see [Administering HDInsight clusters using the Azure portal][hdinsight-admin-portal].</span></span>

<span data-ttu-id="2b0cb-352">**Per ripetere l'esecuzione dell'esercitazione**</span><span class="sxs-lookup"><span data-stu-id="2b0cb-352">**To rerun the tutorial**</span></span>

<span data-ttu-id="2b0cb-353">Per eseguire nuovamente il flusso di lavoro sarà necessario eseguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-353">To rerun the workflow, you must perform the following tasks:</span></span>

* <span data-ttu-id="2b0cb-354">Eliminare il file di output dello script Hive.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-354">Delete the Hive script output file.</span></span>
* <span data-ttu-id="2b0cb-355">Eliminare i dati nella tabella log4jLogsCount.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-355">Delete the data in the log4jLogsCount table.</span></span>

<span data-ttu-id="2b0cb-356">Di seguito è riportato un esempio di script di Windows PowerShell che è possibile usare:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-356">Here is a sample Windows PowerShell script that you can use:</span></span>

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete the Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all the records from the log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="2b0cb-357">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2b0cb-357">Next steps</span></span>
<span data-ttu-id="2b0cb-358">In questa esercitazione si è appreso come definire un flusso di lavoro di Oozie e un coordinatore Oozie e come eseguire un processo del coordinatore Oozie con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2b0cb-358">In this tutorial, you learned how to define an Oozie workflow and an Oozie coordinator, and how to run an Oozie coordinator job by using Azure PowerShell.</span></span> <span data-ttu-id="2b0cb-359">Per altre informazioni, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="2b0cb-359">To learn more, see the following articles:</span></span>

* <span data-ttu-id="2b0cb-360">[Introduzione a HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="2b0cb-360">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="2b0cb-361">[Usare l'archivio BLOB di Azure con HDInsight][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="2b0cb-361">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="2b0cb-362">[Amministrare HDInsight con Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="2b0cb-362">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="2b0cb-363">[Caricare dati in HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="2b0cb-363">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="2b0cb-364">[Usare Sqoop con Hadoop in HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="2b0cb-364">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="2b0cb-365">[Usare Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="2b0cb-365">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="2b0cb-366">[Usare Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="2b0cb-366">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="2b0cb-367">[Sviluppare programmi MapReduce Java per HDInsight][hdinsight-develop-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="2b0cb-367">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-java-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-develop-java-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.RunCoord.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
