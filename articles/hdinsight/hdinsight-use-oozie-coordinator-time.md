---
title: aaaUse basati sul tempo coordinator Hadoop Oozie in HDInsight | Documenti Microsoft
description: Usare il coordinatore Oozie di Hadoop basato sul tempo in HDInsight, un servizio per Big Data. Informazioni su come toodefine Oozie coordinatori e flussi di lavoro e inviare i processi.
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
ms.openlocfilehash: aecbb5ee94a4234d1a7768bdb6de2a33508b1e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-toodefine-workflows-and-coordinate-jobs"></a><span data-ttu-id="933b6-104">Utilizzare basati sul tempo coordinator Oozie con Hadoop in HDInsight toodefine flussi di lavoro e coordinare i processi</span><span class="sxs-lookup"><span data-stu-id="933b6-104">Use time-based Oozie coordinator with Hadoop in HDInsight toodefine workflows and coordinate jobs</span></span>
<span data-ttu-id="933b6-105">In questo articolo si apprenderà come flussi di lavoro toodefine e coordinatori e come tootrigger hello processi coordinatore, basati sul tempo.</span><span class="sxs-lookup"><span data-stu-id="933b6-105">In this article, you'll learn how toodefine workflows and coordinators, and how tootrigger hello coordinator jobs, based on time.</span></span> <span data-ttu-id="933b6-106">È utile toogo tramite [utilizzare Oozie con HDInsight] [ hdinsight-use-oozie] prima di leggere questo articolo.</span><span class="sxs-lookup"><span data-stu-id="933b6-106">It is helpful toogo through [Use Oozie with HDInsight][hdinsight-use-oozie] before you read this article.</span></span> <span data-ttu-id="933b6-107">Inoltre tooOozie, è inoltre possibile pianificare i processi tramite Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="933b6-107">In addition tooOozie, you can also schedule jobs using Azure Data Factory.</span></span> <span data-ttu-id="933b6-108">toolearn Data Factory di Azure, vedere [usare Pig e Hive con Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="933b6-108">toolearn Azure Data Factory, see [Use Pig and Hive with Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="933b6-109">Questo articolo richiede un cluster HDInsight basato su Windows.</span><span class="sxs-lookup"><span data-stu-id="933b6-109">This article requires a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="933b6-110">Per informazioni sull'utilizzo di Oozie, inclusi i processi basati sul tempo, in un cluster basato su Linux, vedere [utilizzare Oozie con Hadoop toodefine ed eseguire un flusso di lavoro in HDInsight basati su Linux](hdinsight-use-oozie-linux-mac.md)</span><span class="sxs-lookup"><span data-stu-id="933b6-110">For information on using Oozie, including time-based jobs, on a Linux-based cluster, see [Use Oozie with Hadoop toodefine and run a workflow on Linux-based HDInsight](hdinsight-use-oozie-linux-mac.md)</span></span>

## <a name="what-is-oozie"></a><span data-ttu-id="933b6-111">Informazioni su Oozie</span><span class="sxs-lookup"><span data-stu-id="933b6-111">What is Oozie</span></span>
<span data-ttu-id="933b6-112">Apache Oozie è un sistema di flusso di lavoro/coordinamento che consente di gestire i processi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="933b6-112">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="933b6-113">È integrato con lo stack di Hadoop hello e supporta i processi Hadoop MapReduce Apache, Pig Apache, Apache Hive e Sqoop Apache.</span><span class="sxs-lookup"><span data-stu-id="933b6-113">It is integrated with hello Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="933b6-114">Può essere anche i processi utilizzati tooschedule sistema tooa specifico, ad esempio programmi Java o gli script della shell.</span><span class="sxs-lookup"><span data-stu-id="933b6-114">It can also be used tooschedule jobs that are specific tooa system, such as Java programs or shell scripts.</span></span>

<span data-ttu-id="933b6-115">Hello immagine seguente mostra del flusso di lavoro hello che verrà implementata:</span><span class="sxs-lookup"><span data-stu-id="933b6-115">hello following image shows hello workflow you will implement:</span></span>

![Diagramma del flusso di lavoro][img-workflow-diagram]

<span data-ttu-id="933b6-117">flusso di lavoro di Hello contiene due azioni:</span><span class="sxs-lookup"><span data-stu-id="933b6-117">hello workflow contains two actions:</span></span>

1. <span data-ttu-id="933b6-118">Un'azione di Hive viene eseguito un hello toocount di script HiveQL le occorrenze di ogni tipo di livello di registrazione in un file di registro log4j.</span><span class="sxs-lookup"><span data-stu-id="933b6-118">A Hive action runs a HiveQL script toocount hello occurrences of each log-level type in a log4j log file.</span></span> <span data-ttu-id="933b6-119">Ogni log log4j è costituita da una riga di campi che contiene un [LOG livello] campo tooshow hello hello e tipo di gravità, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="933b6-119">Each log4j log consists of a line of fields that contains a [LOG LEVEL] field tooshow hello type and hello severity, for example:</span></span>

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    <span data-ttu-id="933b6-120">output dello script Hive Hello è simile a:</span><span class="sxs-lookup"><span data-stu-id="933b6-120">hello Hive script output is similar to:</span></span>

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    <span data-ttu-id="933b6-121">Per altre informazioni su Hive, vedere [Usare Hive con HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="933b6-121">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="933b6-122">Un'azione Sqoop Esporta tabella tooa output hello HiveQL azioni in un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="933b6-122">A Sqoop action exports hello HiveQL action output tooa table in an Azure SQL database.</span></span> <span data-ttu-id="933b6-123">Per altre informazioni su Sqoop, vedere [Usare Sqoop con HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="933b6-123">For more information about Sqoop, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="933b6-124">Per le versioni Oozie supportate nei cluster HDInsight, vedere [novità introdotta nelle versioni di cluster hello fornite da HDInsight?] [hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="933b6-124">For supported Oozie versions on HDInsight clusters, see [What's new in hello cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="933b6-125">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="933b6-125">Prerequisites</span></span>
<span data-ttu-id="933b6-126">Prima di iniziare questa esercitazione, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="933b6-126">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="933b6-127">**Workstation con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="933b6-127">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="933b6-128">Il supporto di Azure PowerShell per la gestione delle risorse HDInsight tramite Azure Service Manager è **deprecato** e verrà rimosso dal 1° gennaio 2017.</span><span class="sxs-lookup"><span data-stu-id="933b6-128">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="933b6-129">Hello passaggi in questo documento usa hello nuovi cmdlet di HDInsight che funzionano con Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="933b6-129">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="933b6-130">Eseguire le operazioni di hello in [installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello più recente di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="933b6-130">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="933b6-131">Se si dispone di script che toobe necessità modificato toouse hello nuovi cmdlet che funzionano con Gestione risorse di Azure, vedere [di strumenti di migrazione tooAzure sviluppo basato su Gestione risorse per i cluster HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="933b6-131">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="933b6-132">**Un cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="933b6-132">**An HDInsight cluster**.</span></span> <span data-ttu-id="933b6-133">Per informazioni sulla creazione di un cluster HDInsight, vedere [Creare cluster HDInsight][hdinsight-provision] o [Introduzione a HDInsight][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="933b6-133">For information about creating an HDInsight cluster, see [Create HDInsight clusters][hdinsight-provision], or [Get started with HDInsight][hdinsight-get-started].</span></span> <span data-ttu-id="933b6-134">È necessario hello toogo dati esercitazione hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="933b6-134">You will need hello following data toogo through hello tutorial:</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="933b6-135">Proprietà del cluster</span><span class="sxs-lookup"><span data-stu-id="933b6-135">Cluster property</span></span></th><th><span data-ttu-id="933b6-136">Nome variabile di Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="933b6-136">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="933b6-137">Valore</span><span class="sxs-lookup"><span data-stu-id="933b6-137">Value</span></span></th><th><span data-ttu-id="933b6-138">Descrizione</span><span class="sxs-lookup"><span data-stu-id="933b6-138">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="933b6-139">Nome del cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="933b6-139">HDInsight cluster name</span></span></td><td><span data-ttu-id="933b6-140">$clusterName</span><span class="sxs-lookup"><span data-stu-id="933b6-140">$clusterName</span></span></td><td></td><td><span data-ttu-id="933b6-141">cluster HDInsight Hello in cui verrà eseguito in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="933b6-141">hello HDInsight cluster on which you will run this tutorial.</span></span></td></tr>
    <tr><td><span data-ttu-id="933b6-142">Nome utente del cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="933b6-142">HDInsight cluster username</span></span></td><td><span data-ttu-id="933b6-143">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="933b6-143">$clusterUsername</span></span></td><td></td><td><span data-ttu-id="933b6-144">nome utente del cluster HDInsight Hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-144">hello HDInsight cluster user name.</span></span> </td></tr>
    <tr><td><span data-ttu-id="933b6-145">Password utente del cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="933b6-145">HDInsight cluster user password</span></span> </td><td><span data-ttu-id="933b6-146">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="933b6-146">$clusterPassword</span></span></td><td></td><td><span data-ttu-id="933b6-147">password dell'utente del cluster HDInsight Hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-147">hello HDInsight cluster user password.</span></span></td></tr>
    <tr><td><span data-ttu-id="933b6-148">Nome dell'account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="933b6-148">Azure storage account name</span></span></td><td><span data-ttu-id="933b6-149">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="933b6-149">$storageAccountName</span></span></td><td></td><td><span data-ttu-id="933b6-150">Un cluster di HDInsight toohello disponibili account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="933b6-150">An Azure Storage account available toohello HDInsight cluster.</span></span> <span data-ttu-id="933b6-151">Per questa esercitazione, utilizzare l'account di archiviazione hello predefinito specificato durante il processo di provisioning di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-151">For this tutorial, use hello default storage account that you specified during hello cluster provision process.</span></span></td></tr>
    <tr><td><span data-ttu-id="933b6-152">Nome del contenitore BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="933b6-152">Azure Blob container name</span></span></td><td><span data-ttu-id="933b6-153">$containerName</span><span class="sxs-lookup"><span data-stu-id="933b6-153">$containerName</span></span></td><td></td><td><span data-ttu-id="933b6-154">Per questo esempio, utilizzare il contenitore di archiviazione Blob di Azure hello utilizzata per file system cluster HDInsight di hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="933b6-154">For this example, use hello Azure Blob storage container that is used for hello default HDInsight cluster file system.</span></span> <span data-ttu-id="933b6-155">Per impostazione predefinita, ha hello stesso nome del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-155">By default, it has hello same name as hello HDInsight cluster.</span></span></td></tr>
    </table><span data-ttu-id="933b6-156">
* **Un database SQL di Azure**.</span><span class="sxs-lookup"><span data-stu-id="933b6-156">
* **An Azure SQL database**.</span></span> <span data-ttu-id="933b6-157">È necessario configurare una regola del firewall per l'accesso al Database di SQL server tooallow hello dalla propria workstation.</span><span class="sxs-lookup"><span data-stu-id="933b6-157">You must configure a firewall rule for hello SQL Database server tooallow access from your workstation.</span></span> <span data-ttu-id="933b6-158">Per istruzioni sulla creazione di un database SQL di Azure e configurazione di firewall hello, vedere [iniziare a usare database SQL di Azure] [sqldatabase-get-avviato].</span><span class="sxs-lookup"><span data-stu-id="933b6-158">For instructions about creating an Azure SQL database and configuring hello firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> <span data-ttu-id="933b6-159">In questo articolo fornisce uno script di Windows PowerShell per la creazione di tabella di database SQL di Azure hello che è necessario per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="933b6-159">This article provides a Windows PowerShell script for creating hello Azure SQL database table that you need for this tutorial.</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="933b6-160">Proprietà del database SQL</span><span class="sxs-lookup"><span data-stu-id="933b6-160">SQL database property</span></span></th><th><span data-ttu-id="933b6-161">Nome variabile di Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="933b6-161">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="933b6-162">Valore</span><span class="sxs-lookup"><span data-stu-id="933b6-162">Value</span></span></th><th><span data-ttu-id="933b6-163">Descrizione</span><span class="sxs-lookup"><span data-stu-id="933b6-163">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="933b6-164">Nome del server di database SQL</span><span class="sxs-lookup"><span data-stu-id="933b6-164">SQL database server name</span></span></td><td><span data-ttu-id="933b6-165">$sqlDatabaseServer</span><span class="sxs-lookup"><span data-stu-id="933b6-165">$sqlDatabaseServer</span></span></td><td></td><td><span data-ttu-id="933b6-166">Hello SQL database server toowhich Sqoop esporterà i dati.</span><span class="sxs-lookup"><span data-stu-id="933b6-166">hello SQL database server toowhich Sqoop will export data.</span></span> </td></tr>
    <tr><td><span data-ttu-id="933b6-167">Nome di accesso al database SQL</span><span class="sxs-lookup"><span data-stu-id="933b6-167">SQL database login name</span></span></td><td><span data-ttu-id="933b6-168">$sqlDatabaseLogin</span><span class="sxs-lookup"><span data-stu-id="933b6-168">$sqlDatabaseLogin</span></span></td><td></td><td><span data-ttu-id="933b6-169">Il nome di accesso al database SQL.</span><span class="sxs-lookup"><span data-stu-id="933b6-169">SQL Database login name.</span></span></td></tr>
    <tr><td><span data-ttu-id="933b6-170">Password di accesso al database SQL</span><span class="sxs-lookup"><span data-stu-id="933b6-170">SQL database login password</span></span></td><td><span data-ttu-id="933b6-171">$sqlDatabaseLoginPassword</span><span class="sxs-lookup"><span data-stu-id="933b6-171">$sqlDatabaseLoginPassword</span></span></td><td></td><td><span data-ttu-id="933b6-172">La password di accesso al database SQL.</span><span class="sxs-lookup"><span data-stu-id="933b6-172">SQL Database login password.</span></span></td></tr>
    <tr><td><span data-ttu-id="933b6-173">Nome del database SQL</span><span class="sxs-lookup"><span data-stu-id="933b6-173">SQL database name</span></span></td><td><span data-ttu-id="933b6-174">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="933b6-174">$sqlDatabaseName</span></span></td><td></td><td><span data-ttu-id="933b6-175">Hello Azure SQL database toowhich Sqoop esporterà i dati.</span><span class="sxs-lookup"><span data-stu-id="933b6-175">hello Azure SQL database toowhich Sqoop will export data.</span></span> </td></tr>
    </table>

  > [!NOTE]
  > <span data-ttu-id="933b6-176">Per impostazione predefinita, un database SQL di Azure consente connessioni da servizi di Azure, ad esempio Azure HDinsight.</span><span class="sxs-lookup"><span data-stu-id="933b6-176">By default an Azure SQL database allows connections from Azure Services, such as Azure HDInsight.</span></span> <span data-ttu-id="933b6-177">Se questa impostazione del firewall è disabilitata, è necessario abilitarlo dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-177">If this firewall setting is disabled, you must enable it from hello Azure Portal.</span></span> <span data-ttu-id="933b6-178">Per istruzioni sulla creazione di un database SQL e sulla configurazione di regole del firewall, vedere [Creare e configurare un database SQL][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="933b6-178">For instruction about creating a SQL Database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-get-started].</span></span>

> [!NOTE]
> <span data-ttu-id="933b6-179">Valori hello di riempimento nelle tabelle di hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-179">Fill-in hello values in hello tables.</span></span> <span data-ttu-id="933b6-180">potrà essere utile per completare questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="933b6-180">It will be helpful for going through this tutorial.</span></span>

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a><span data-ttu-id="933b6-181">Definire Oozie del flusso di lavoro e hello script HiveQL correlato</span><span class="sxs-lookup"><span data-stu-id="933b6-181">Define Oozie workflow and hello related HiveQL script</span></span>
<span data-ttu-id="933b6-182">Le definizioni dei flussi di lavoro di Oozie sono scritte in linguaggio hPDL (XML Process Definition Language).</span><span class="sxs-lookup"><span data-stu-id="933b6-182">Oozie workflows definitions are written in hPDL (an XML process definition language).</span></span> <span data-ttu-id="933b6-183">nome del file di flusso di lavoro predefinito Hello *workflow*.</span><span class="sxs-lookup"><span data-stu-id="933b6-183">hello default workflow file name is *workflow.xml*.</span></span>  <span data-ttu-id="933b6-184">Si verrà salvare file in locale di hello del flusso di lavoro e quindi distribuirlo cluster HDInsight toohello tramite Azure PowerShell più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="933b6-184">You will save hello workflow file locally, and then deploy it toohello HDInsight cluster by using Azure PowerShell later in this tutorial.</span></span>

<span data-ttu-id="933b6-185">Hello Hive azione nel flusso di lavoro hello chiama un file di script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="933b6-185">hello Hive action in hello workflow calls a HiveQL script file.</span></span> <span data-ttu-id="933b6-186">che contiene tre istruzioni HiveQL:</span><span class="sxs-lookup"><span data-stu-id="933b6-186">This script file contains three HiveQL statements:</span></span>

1. <span data-ttu-id="933b6-187">**istruzione DROP TABLE Hello** eliminazioni hello tabella Hive log4j se esiste.</span><span class="sxs-lookup"><span data-stu-id="933b6-187">**hello DROP TABLE statement** deletes hello log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="933b6-188">**istruzione CREATE TABLE Hello** crea una tabella esterna di Hive log4j, che fa riferimento toohello percorso del file di log log4j hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-188">**hello CREATE TABLE statement** creates a log4j Hive external table, which points toohello location of hello log4j log file;</span></span>
3. <span data-ttu-id="933b6-189">**percorso del file di registro log4j hello Hello**.</span><span class="sxs-lookup"><span data-stu-id="933b6-189">**hello location of hello log4j log file**.</span></span> <span data-ttu-id="933b6-190">delimitatore di campo Hello è ",".</span><span class="sxs-lookup"><span data-stu-id="933b6-190">hello field delimiter is ",".</span></span> <span data-ttu-id="933b6-191">delimitatore di riga Hello predefinito è "\n".</span><span class="sxs-lookup"><span data-stu-id="933b6-191">hello default line delimiter is "\n".</span></span> <span data-ttu-id="933b6-192">Una tabella esterna Hive è tooavoid utilizzato i file di dati di hello viene rimosso dalla posizione originale hello, nel caso in cui si desidera del flusso di lavoro di toorun hello Oozie più volte.</span><span class="sxs-lookup"><span data-stu-id="933b6-192">A Hive external table is used tooavoid hello data file being removed from hello original location, in case you want toorun hello Oozie workflow multiple times.</span></span>
4. <span data-ttu-id="933b6-193">**istruzione INSERT SOVRASCRIVERE Hello** conta le occorrenze di hello di ogni tipo di log a livello di tabella Hive log4j hello e Salva percorso di archiviazione Blob di Azure tooan output hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-193">**hello INSERT OVERWRITE statement** counts hello occurrences of each log-level type from hello log4j Hive table, and it saves hello output tooan Azure Blob storage location.</span></span>

> [!NOTE]
> <span data-ttu-id="933b6-194">Il percorso di Hive è caratterizzato da un problema noto</span><span class="sxs-lookup"><span data-stu-id="933b6-194">There is a known Hive path issue.</span></span> <span data-ttu-id="933b6-195">che si verifica durante l'invio di un processo Oozie.</span><span class="sxs-lookup"><span data-stu-id="933b6-195">You will run into this problem when submitting an Oozie job.</span></span> <span data-ttu-id="933b6-196">Hello istruzioni per risoluzione hello problema sono disponibili su TechNet Wiki hello: [Hive di HDInsight errore: Impossibile toorename][technetwiki-hive-error].</span><span class="sxs-lookup"><span data-stu-id="933b6-196">hello instructions for fixing hello issue can be found on hello TechNet Wiki: [HDInsight Hive error: Unable toorename][technetwiki-hive-error].</span></span>

<span data-ttu-id="933b6-197">**chiamato dal flusso di lavoro hello toodefine hello HiveQL script file toobe**</span><span class="sxs-lookup"><span data-stu-id="933b6-197">**toodefine hello HiveQL script file toobe called by hello workflow**</span></span>

1. <span data-ttu-id="933b6-198">Creare un file di testo con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="933b6-198">Create a text file with hello following content:</span></span>

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    <span data-ttu-id="933b6-199">Esistono tre variabili utilizzate nello script hello:</span><span class="sxs-lookup"><span data-stu-id="933b6-199">There are three variables used in hello script:</span></span>

   * <span data-ttu-id="933b6-200">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="933b6-200">${hiveTableName}</span></span>
   * <span data-ttu-id="933b6-201">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="933b6-201">${hiveDataFolder}</span></span>
   * <span data-ttu-id="933b6-202">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="933b6-202">${hiveOutputFolder}</span></span>

     <span data-ttu-id="933b6-203">file di definizione del flusso di lavoro Hello (workflow in questa esercitazione) passerà questi toothis valori script HiveQL in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="933b6-203">hello workflow definition file (workflow.xml in this tutorial) will pass these values toothis HiveQL script at run time.</span></span>
2. <span data-ttu-id="933b6-204">Salvare il file hello come **C:\Tutorials\UseOozie\useooziewf.hql** utilizzando la codifica ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="933b6-204">Save hello file as **C:\Tutorials\UseOozie\useooziewf.hql** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="933b6-205">Usare il blocco note se l'editor di testo non offre questa opzione. Questo file di script sarà cluster HDInsight toohello distribuito in un secondo momento nell'esercitazione di hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-205">(Use Notepad if your text editor doesn't provide this option.) This script file will be deployed toohello HDInsight cluster later in hello tutorial.</span></span>

<span data-ttu-id="933b6-206">**toodefine un flusso di lavoro**</span><span class="sxs-lookup"><span data-stu-id="933b6-206">**toodefine a workflow**</span></span>

1. <span data-ttu-id="933b6-207">Creare un file di testo con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="933b6-207">Create a text file with hello following content:</span></span>

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

    <span data-ttu-id="933b6-208">Esistono due azioni definite nel flusso di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-208">There are two actions defined in hello workflow.</span></span> <span data-ttu-id="933b6-209">start-tooaction Hello è *RunHiveScript*.</span><span class="sxs-lookup"><span data-stu-id="933b6-209">hello start-tooaction is *RunHiveScript*.</span></span> <span data-ttu-id="933b6-210">Se viene eseguito l'azione di hello *OK*, azione successiva hello è *RunSqoopExport*.</span><span class="sxs-lookup"><span data-stu-id="933b6-210">If hello action runs *OK*, hello next action is *RunSqoopExport*.</span></span>

    <span data-ttu-id="933b6-211">Hello RunHiveScript ha diverse variabili.</span><span class="sxs-lookup"><span data-stu-id="933b6-211">hello RunHiveScript has several variables.</span></span> <span data-ttu-id="933b6-212">I valori hello verrà passato quando si invia il processo di Oozie hello dalla propria workstation con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="933b6-212">You will pass hello values when you submit hello Oozie job from your workstation by using Azure PowerShell.</span></span>

    <span data-ttu-id="933b6-213">Variabili del flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="933b6-213">Workflow variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="933b6-214">Variabili del flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="933b6-214">Workflow variables</span></span></th><th><span data-ttu-id="933b6-215">Descrizione</span><span class="sxs-lookup"><span data-stu-id="933b6-215">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="933b6-216">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="933b6-216">${jobTracker}</span></span></td><td><span data-ttu-id="933b6-217">Specificare l'URL di hello di gestione di processi Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-217">Specify hello URL of hello Hadoop job tracker.</span></span> <span data-ttu-id="933b6-218">Usare <strong>jobtrackerhost:9010</strong> nel cluster HDInsight versione 3.0 e 2.0.</span><span class="sxs-lookup"><span data-stu-id="933b6-218">Use <strong>jobtrackerhost:9010</strong> on HDInsight cluster version 3.0 and 2.0.</span></span></td></tr>
    <tr><td><span data-ttu-id="933b6-219">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="933b6-219">${nameNode}</span></span></td><td><span data-ttu-id="933b6-220">Specificare l'URL di hello del nodo del nome hello Hadoop.</span><span class="sxs-lookup"><span data-stu-id="933b6-220">Specify hello URL of hello Hadoop name node.</span></span> <span data-ttu-id="933b6-221">Utilizzare hello predefinito file system wasb: / / l'indirizzo, ad esempio, <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. n e t</i>.</span><span class="sxs-lookup"><span data-stu-id="933b6-221">Use hello default file system wasb:// address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
    <tr><td><span data-ttu-id="933b6-222">${queueName}</span><span class="sxs-lookup"><span data-stu-id="933b6-222">${queueName}</span></span></td><td><span data-ttu-id="933b6-223">Specifica del nome della coda hello hello processo verrà inviato a.</span><span class="sxs-lookup"><span data-stu-id="933b6-223">Specifies hello queue name that hello job will be submitted to.</span></span> <span data-ttu-id="933b6-224">Usare l'<strong>impostazione predefinita</strong>.</span><span class="sxs-lookup"><span data-stu-id="933b6-224">Use <strong>default</strong>.</span></span></td></tr>
    </table>

    <span data-ttu-id="933b6-225">Variabili dell'azione Hive</span><span class="sxs-lookup"><span data-stu-id="933b6-225">Hive action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="933b6-226">Variabile azione Hive</span><span class="sxs-lookup"><span data-stu-id="933b6-226">Hive action variable</span></span></th><th><span data-ttu-id="933b6-227">Descrizione</span><span class="sxs-lookup"><span data-stu-id="933b6-227">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="933b6-228">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="933b6-228">${hiveDataFolder}</span></span></td><td><span data-ttu-id="933b6-229">directory di origine Hello per hello comando Hive Create Table.</span><span class="sxs-lookup"><span data-stu-id="933b6-229">hello source directory for hello Hive Create Table command.</span></span></td></tr>
    <tr><td><span data-ttu-id="933b6-230">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="933b6-230">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="933b6-231">cartella di output di Hello per hello istruzione INSERT SOVRASCRIVERE.</span><span class="sxs-lookup"><span data-stu-id="933b6-231">hello output folder for hello INSERT OVERWRITE statement.</span></span></td></tr>
    <tr><td><span data-ttu-id="933b6-232">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="933b6-232">${hiveTableName}</span></span></td><td><span data-ttu-id="933b6-233">nome Hello della tabella Hive hello che fa riferimento a file di dati log4j hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-233">hello name of hello Hive table that references hello log4j data files.</span></span></td></tr>
    </table>

    <span data-ttu-id="933b6-234">Variabili dell'azione Sqoop</span><span class="sxs-lookup"><span data-stu-id="933b6-234">Sqoop action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="933b6-235">Variabile azione Sqoop</span><span class="sxs-lookup"><span data-stu-id="933b6-235">Sqoop action variable</span></span></th><th><span data-ttu-id="933b6-236">Descrizione</span><span class="sxs-lookup"><span data-stu-id="933b6-236">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="933b6-237">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="933b6-237">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="933b6-238">Stringa di connessione del database SQL.</span><span class="sxs-lookup"><span data-stu-id="933b6-238">SQL Database connection string.</span></span></td></tr>
    <tr><td><span data-ttu-id="933b6-239">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="933b6-239">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="933b6-240">verrà esportato Hello dati hello toowhere tabella del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="933b6-240">hello Azure SQL database table toowhere hello data will be exported.</span></span></td></tr>
    <tr><td><span data-ttu-id="933b6-241">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="933b6-241">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="933b6-242">cartella di output di Hello per hello istruzione INSERT SOVRASCRIVERE l'Hive.</span><span class="sxs-lookup"><span data-stu-id="933b6-242">hello output folder for hello Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="933b6-243">Si tratta di hello stessa cartella per l'esportazione Sqoop hello (esportazione-dir).</span><span class="sxs-lookup"><span data-stu-id="933b6-243">This is hello same folder for hello Sqoop export (export-dir).</span></span></td></tr>
    </table>

    <span data-ttu-id="933b6-244">Per ulteriori informazioni sulla Oozie del flusso di lavoro e l'utilizzo di azioni del flusso di lavoro hello, vedere [documentazione di Apache Oozie 4.0] [ apache-oozie-400] (per la versione del cluster HDInsight 3.0) o [Oozie Apache 3.3.2 documentazione] [ apache-oozie-332] (per la versione del cluster HDInsight 2.1).</span><span class="sxs-lookup"><span data-stu-id="933b6-244">For more information about Oozie workflow and using hello workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

1. <span data-ttu-id="933b6-245">Salvare il file hello come **C:\Tutorials\UseOozie\workflow.xml** utilizzando la codifica ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="933b6-245">Save hello file as **C:\Tutorials\UseOozie\workflow.xml** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="933b6-246">Usare il blocco note se l'editor di testo non offre questa opzione.</span><span class="sxs-lookup"><span data-stu-id="933b6-246">(Use Notepad if your text editor doesn't provide this option.)</span></span>

<span data-ttu-id="933b6-247">**coordinatore toodefine**</span><span class="sxs-lookup"><span data-stu-id="933b6-247">**toodefine coordinator**</span></span>

1. <span data-ttu-id="933b6-248">Creare un file di testo con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="933b6-248">Create a text file with hello following content:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    <span data-ttu-id="933b6-249">Esistono cinque variabili utilizzate nel file di definizione hello:</span><span class="sxs-lookup"><span data-stu-id="933b6-249">There are five variables used in hello definition file:</span></span>

   | <span data-ttu-id="933b6-250">Variabile</span><span class="sxs-lookup"><span data-stu-id="933b6-250">Variable</span></span> | <span data-ttu-id="933b6-251">Descrizione</span><span class="sxs-lookup"><span data-stu-id="933b6-251">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="933b6-252">${coordFrequency}</span><span class="sxs-lookup"><span data-stu-id="933b6-252">${coordFrequency}</span></span> |<span data-ttu-id="933b6-253">Tempo di sospensione del processo.</span><span class="sxs-lookup"><span data-stu-id="933b6-253">Job pause time.</span></span> <span data-ttu-id="933b6-254">La frequenza è sempre espressa in minuti.</span><span class="sxs-lookup"><span data-stu-id="933b6-254">Frequency is always expressed in minutes.</span></span> |
   | <span data-ttu-id="933b6-255">${coordStart}</span><span class="sxs-lookup"><span data-stu-id="933b6-255">${coordStart}</span></span> |<span data-ttu-id="933b6-256">Ora di inizio del processo.</span><span class="sxs-lookup"><span data-stu-id="933b6-256">Job start time.</span></span> |
   | <span data-ttu-id="933b6-257">${coordEnd}</span><span class="sxs-lookup"><span data-stu-id="933b6-257">${coordEnd}</span></span> |<span data-ttu-id="933b6-258">Ora di fine del processo.</span><span class="sxs-lookup"><span data-stu-id="933b6-258">Job end time.</span></span> |
   | <span data-ttu-id="933b6-259">${coordTimezone}</span><span class="sxs-lookup"><span data-stu-id="933b6-259">${coordTimezone}</span></span> |<span data-ttu-id="933b6-260">Oozie elabora i processi del coordinatore in un fuso orario predefinito che non tiene conto dell'ora legale (in genere rappresentato dall'acronimo UTC).</span><span class="sxs-lookup"><span data-stu-id="933b6-260">Oozie processes coordinator jobs in a fixed time zone with no daylight saving time (typically represented by using UTC).</span></span> <span data-ttu-id="933b6-261">Il fuso orario viene definito come hello "Oozie elaborazione fuso orario."</span><span class="sxs-lookup"><span data-stu-id="933b6-261">This time zone is referred as hello "Oozie processing timezone."</span></span> |
   | <span data-ttu-id="933b6-262">${wfPath}</span><span class="sxs-lookup"><span data-stu-id="933b6-262">${wfPath}</span></span> |<span data-ttu-id="933b6-263">percorso Hello hello workflow.</span><span class="sxs-lookup"><span data-stu-id="933b6-263">hello path for hello workflow.xml.</span></span>  <span data-ttu-id="933b6-264">Se non nome del file del flusso di lavoro hello è nome del file hello predefinito (workflow), è necessario specificarlo.</span><span class="sxs-lookup"><span data-stu-id="933b6-264">If hello workflow file name is not hello default file name (workflow.xml), you must specify it.</span></span> |
2. <span data-ttu-id="933b6-265">Salvare il file hello come **C:\Tutorials\UseOozie\coordinator.xml** usando la codifica ANSI (ASCII) hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-265">Save hello file as **C:\Tutorials\UseOozie\coordinator.xml** by using hello ANSI (ASCII) encoding.</span></span> <span data-ttu-id="933b6-266">Usare il blocco note se l'editor di testo non offre questa opzione.</span><span class="sxs-lookup"><span data-stu-id="933b6-266">(Use Notepad if your text editor doesn't provide this option.)</span></span>

## <a name="deploy-hello-oozie-project-and-prepare-hello-tutorial"></a><span data-ttu-id="933b6-267">Distribuire il progetto di Oozie hello e preparare l'esercitazione hello</span><span class="sxs-lookup"><span data-stu-id="933b6-267">Deploy hello Oozie project and prepare hello tutorial</span></span>
<span data-ttu-id="933b6-268">Eseguire un esempio di hello tooperform script Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="933b6-268">You will run an Azure PowerShell script tooperform hello following:</span></span>

* <span data-ttu-id="933b6-269">Hello copia nell'archiviazione Blob tooAzure script (useoozie.hql) HiveQL, wasb:///tutorials/useoozie/useoozie.hql.</span><span class="sxs-lookup"><span data-stu-id="933b6-269">Copy hello HiveQL script (useoozie.hql) tooAzure Blob storage, wasb:///tutorials/useoozie/useoozie.hql.</span></span>
* <span data-ttu-id="933b6-270">Copiare toowasb:///tutorials/useoozie/workflow.xml workflow.</span><span class="sxs-lookup"><span data-stu-id="933b6-270">Copy workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span></span>
* <span data-ttu-id="933b6-271">Copiare coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.</span><span class="sxs-lookup"><span data-stu-id="933b6-271">Copy coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.</span></span>
* <span data-ttu-id="933b6-272">File di dati di Windows hello (o example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="933b6-272">Copy hello data file (/example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span></span>
* <span data-ttu-id="933b6-273">Creare una tabella di database SQL di Azure per l'archiviazione dei dati di esportazione di Sqoop.</span><span class="sxs-lookup"><span data-stu-id="933b6-273">Create an Azure SQL database table for storing Sqoop export data.</span></span> <span data-ttu-id="933b6-274">nome della tabella Hello *log4jLogCount*.</span><span class="sxs-lookup"><span data-stu-id="933b6-274">hello table name is *log4jLogCount*.</span></span>

<span data-ttu-id="933b6-275">**Informazioni sull'archiviazione in HDInsight**</span><span class="sxs-lookup"><span data-stu-id="933b6-275">**Understand HDInsight storage**</span></span>

<span data-ttu-id="933b6-276">HDInsight usa l'archiviazione BLOB di Azure per l'archiviazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="933b6-276">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="933b6-277">wasb: / / è l'implementazione Microsoft di hello file system distribuito Hadoop (HDFS) nell'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="933b6-277">wasb:// is Microsoft's implementation of hello Hadoop distributed file system (HDFS) in Azure Blob storage.</span></span> <span data-ttu-id="933b6-278">Per altre informazioni, vedere [Usare l'archivio BLOB di Azure con HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="933b6-278">For more information, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="933b6-279">Quando si esegue il provisioning di un cluster HDInsight, un account di archiviazione Blob di Azure e un contenitore specifico da tale account viene designato come hello predefiniti del file system, ad esempio in HDFS.</span><span class="sxs-lookup"><span data-stu-id="933b6-279">When you provision an HDInsight cluster, an Azure Blob storage account and a specific container from that account is designated as hello default file system, like in HDFS.</span></span> <span data-ttu-id="933b6-280">In account di archiviazione toothis, è inoltre possibile aggiungere ulteriore spazio di archiviazione di account da hello stessa sottoscrizione di Azure o da diverse sottoscrizioni di Azure durante il processo di provisioning hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-280">In addition toothis storage account, you can add additional storage accounts from hello same Azure subscription or from different Azure subscriptions during hello provisioning process.</span></span> <span data-ttu-id="933b6-281">Per istruzioni sull'aggiunta di altri account di archiviazione, vedere [Effettuare il provisioning di cluster HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="933b6-281">For instructions about adding additional storage accounts, see [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="933b6-282">script di PowerShell Azure hello toosimplify utilizzati in questa esercitazione, tutti i file vengono archiviati nel contenitore di sistema di hello predefinito file hello posizione *esercitazioni/useoozie*.</span><span class="sxs-lookup"><span data-stu-id="933b6-282">toosimplify hello Azure PowerShell script used in this tutorial, all of hello files are stored in hello default file system container located at */tutorials/useoozie*.</span></span> <span data-ttu-id="933b6-283">Per impostazione predefinita, questo contenitore comprende hello stesso nome come nome del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-283">By default, this container has hello same name as hello HDInsight cluster name.</span></span>
<span data-ttu-id="933b6-284">sintassi di Hello è:</span><span class="sxs-lookup"><span data-stu-id="933b6-284">hello syntax is:</span></span>

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> <span data-ttu-id="933b6-285">Solo hello *wasb: / /* sintassi è supportata nella versione 3.0 del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="933b6-285">Only hello *wasb://* syntax is supported in HDInsight cluster version 3.0.</span></span> <span data-ttu-id="933b6-286">Hello precedente *asv: / /* sintassi è supportata in HDInsight 2.1 e 1.6 cluster, ma non è supportata nei cluster di HDInsight 3.0.</span><span class="sxs-lookup"><span data-stu-id="933b6-286">hello older *asv://* syntax is supported in HDInsight 2.1 and 1.6 clusters, but it is not supported in HDInsight 3.0 clusters.</span></span>
>
> <span data-ttu-id="933b6-287">Hello wasb: / / percorso è un percorso virtuale.</span><span class="sxs-lookup"><span data-stu-id="933b6-287">hello wasb:// path is a virtual path.</span></span> <span data-ttu-id="933b6-288">Per altre informazioni, vedere [Usare l'archivio BLOB di Azure con HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="933b6-288">For more information see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="933b6-289">Un file che viene archiviato nel contenitore di sistema di hello predefinito file è possibile accedere da HDInsight utilizzando uno dei seguenti URI (ad esempio utilizzando workflow) hello:</span><span class="sxs-lookup"><span data-stu-id="933b6-289">A file that is stored in hello default file system container can be accessed from HDInsight by using any of hello following URIs (I am using workflow.xml as an example):</span></span>

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

<span data-ttu-id="933b6-290">Se si desidera file hello tooaccess direttamente dall'account di archiviazione hello, nome blob hello file hello è:</span><span class="sxs-lookup"><span data-stu-id="933b6-290">If you want tooaccess hello file directly from hello storage account, hello blob name for hello file is:</span></span>

    tutorials/useoozie/workflow.xml

<span data-ttu-id="933b6-291">**Informazioni sulle tabelle interne ed esterne di Hive**</span><span class="sxs-lookup"><span data-stu-id="933b6-291">**Understand Hive internal and external tables**</span></span>

<span data-ttu-id="933b6-292">Esistono alcuni aspetti, è necessario tooknow sulle tabelle interne ed esterne di Hive:</span><span class="sxs-lookup"><span data-stu-id="933b6-292">There are a few things you need tooknow about Hive internal and external tables:</span></span>

* <span data-ttu-id="933b6-293">Hello comando CREATE TABLE crea una tabella interna, noto anche come una tabella gestita.</span><span class="sxs-lookup"><span data-stu-id="933b6-293">hello CREATE TABLE command creates an internal table, also known as a managed table.</span></span> <span data-ttu-id="933b6-294">file di dati Hello deve trovarsi nel contenitore predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-294">hello data file must be located in hello default container.</span></span>
* <span data-ttu-id="933b6-295">comando CREATE TABLE Hello sposta dati hello filetoohello/hive/warehouse/<TableName> cartella nel contenitore predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-295">hello CREATE TABLE command moves hello data file toohello /hive/warehouse/<TableName> folder in hello default container.</span></span>
* <span data-ttu-id="933b6-296">Hello comando CREATE EXTERNAL TABLE crea una tabella esterna.</span><span class="sxs-lookup"><span data-stu-id="933b6-296">hello CREATE EXTERNAL TABLE command creates an external table.</span></span> <span data-ttu-id="933b6-297">file di dati Hello può trovarsi all'esterno di contenitore predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-297">hello data file can be located outside hello default container.</span></span>
* <span data-ttu-id="933b6-298">Hello comando CREATE EXTERNAL TABLE non sposta i file di dati hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-298">hello CREATE EXTERNAL TABLE command does not move hello data file.</span></span>
* <span data-ttu-id="933b6-299">Hello comando CREATE EXTERNAL TABLE non consente sottocartelle nella cartella hello specificato nella clausola percorso hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-299">hello CREATE EXTERNAL TABLE command doesn't allow any subfolders under hello folder that is specified in hello LOCATION clause.</span></span> <span data-ttu-id="933b6-300">Questo è il motivo di hello perché esercitazione hello crea una copia del file sample.log hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-300">This is hello reason why hello tutorial makes a copy of hello sample.log file.</span></span>

<span data-ttu-id="933b6-301">Per altre informazioni, vedere [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables] (HDInsight: introduzione alle tabelle Hive interne ed esterne).</span><span class="sxs-lookup"><span data-stu-id="933b6-301">For more information, see [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables].</span></span>

<span data-ttu-id="933b6-302">**esercitazione hello tooprepare**</span><span class="sxs-lookup"><span data-stu-id="933b6-302">**tooprepare hello tutorial**</span></span>

1. <span data-ttu-id="933b6-303">Hello aprire Windows PowerShell ISE (nella schermata iniziale di Windows 8 hello digitare **PowerShell_ISE**, quindi fare clic su **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="933b6-303">Open hello Windows PowerShell ISE (in hello Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="933b6-304">Per altre informazioni, vedere [Start Windows PowerShell on Windows 8 and Windows][powershell-start] (Avviare Windows PowerShell in Windows 8 e Windows).</span><span class="sxs-lookup"><span data-stu-id="933b6-304">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="933b6-305">Nel riquadro inferiore hello eseguire hello successivo comando tooconnect tooyour sottoscrizione di Azure:</span><span class="sxs-lookup"><span data-stu-id="933b6-305">In hello bottom pane, run hello following command tooconnect tooyour Azure subscription:</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="933b6-306">Si sarà tooenter richieste le credenziali dell'account Azure.</span><span class="sxs-lookup"><span data-stu-id="933b6-306">You will be prompted tooenter your Azure account credentials.</span></span> <span data-ttu-id="933b6-307">Questo metodo di aggiunta di una connessione di sottoscrizione scade e dopo 12 ore, si disporrà di cmdlet hello toorun nuovamente.</span><span class="sxs-lookup"><span data-stu-id="933b6-307">This method of adding a subscription connection times out, and after 12 hours, you will have toorun hello cmdlet again.</span></span>

   > [!NOTE]
   > <span data-ttu-id="933b6-308">Se si dispone di più sottoscrizioni di Azure e sottoscrizione predefinita hello non è hello quello desiderato toouse, utilizzare hello <strong>Select-AzureSubscription</strong> tooselect cmdlet una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="933b6-308">If you have multiple Azure subscriptions and hello default subscription is not hello one you want toouse, use hello <strong>Select-AzureSubscription</strong> cmdlet tooselect a subscription.</span></span>

3. <span data-ttu-id="933b6-309">Copiare lo script seguente nel riquadro di script hello hello e quindi impostare le variabili primi sei hello:</span><span class="sxs-lookup"><span data-stu-id="933b6-309">Copy hello following script into hello script pane, and then set hello first six variables:</span></span>

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

    # Oozie files for hello tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here
    ```

    <span data-ttu-id="933b6-310">Per ulteriori descrizioni delle variabili di hello, vedere hello [prerequisiti](#prerequisites) sezione in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="933b6-310">For more descriptions of hello variables, see hello [Prerequisites](#prerequisites) section in this tutorial.</span></span>

4. <span data-ttu-id="933b6-311">Aggiungere hello toohello lo script nel riquadro di script hello seguente:</span><span class="sxs-lookup"><span data-stu-id="933b6-311">Append hello following toohello script in hello script pane:</span></span>

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
        Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green
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

        #Create hello log4jLogsCount table
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

    # make a copy of example/data/sample.log tooexample/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. <span data-ttu-id="933b6-312">Fare clic su **Esegui Script** o premere **F5** script hello toorun.</span><span class="sxs-lookup"><span data-stu-id="933b6-312">Click **Run Script** or press **F5** toorun hello script.</span></span> <span data-ttu-id="933b6-313">output di Hello sarà simile a:</span><span class="sxs-lookup"><span data-stu-id="933b6-313">hello output will be similar to:</span></span>

    ![Output delle operazioni preliminari all'esercitazione][img-preparation-output]

## <a name="run-hello-oozie-project"></a><span data-ttu-id="933b6-315">Eseguire il progetto di Oozie hello</span><span class="sxs-lookup"><span data-stu-id="933b6-315">Run hello Oozie project</span></span>
<span data-ttu-id="933b6-316">Attualmente Azure PowerShell non fornisce alcun cmdlet per la definizione dei processi Oozie.</span><span class="sxs-lookup"><span data-stu-id="933b6-316">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="933b6-317">È possibile utilizzare hello **Invoke-RestMethod** cmdlet tooinvoke Oozie i servizi web.</span><span class="sxs-lookup"><span data-stu-id="933b6-317">You can use hello **Invoke-RestMethod** cmdlet tooinvoke Oozie web services.</span></span> <span data-ttu-id="933b6-318">API dei servizi web di Hello Oozie è un'API di HTTP REST JSON.</span><span class="sxs-lookup"><span data-stu-id="933b6-318">hello Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="933b6-319">Per ulteriori informazioni sui servizi web di hello Oozie API, vedere [documentazione di Apache Oozie 4.0] [ apache-oozie-400] (per la versione del cluster HDInsight 3.0) o [documentazione di Apache Oozie 3.3.2] [ apache-oozie-332] (per la versione del cluster HDInsight 2.1).</span><span class="sxs-lookup"><span data-stu-id="933b6-319">For more information about hello Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

<span data-ttu-id="933b6-320">**un processo di Oozie toosubmit**</span><span class="sxs-lookup"><span data-stu-id="933b6-320">**toosubmit an Oozie job**</span></span>

1. <span data-ttu-id="933b6-321">Hello aprire Windows PowerShell ISE (nella schermata iniziale di Windows 8 digitare **PowerShell_ISE**, quindi fare clic su **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="933b6-321">Open hello Windows PowerShell ISE (in Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="933b6-322">Per altre informazioni, vedere [Start Windows PowerShell on Windows 8 and Windows][powershell-start] (Avviare Windows PowerShell in Windows 8 e Windows).</span><span class="sxs-lookup"><span data-stu-id="933b6-322">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="933b6-323">Lo script seguente di hello di copia nel riquadro di script hello e quindi set hello innanzitutto quattordici variabili (tuttavia, ignorare **$storageUri**).</span><span class="sxs-lookup"><span data-stu-id="933b6-323">Copy hello following script into hello script pane, and then set hello first fourteen variables (however, skip **$storageUri**).</span></span>

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

    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
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

    <span data-ttu-id="933b6-324">Per ulteriori descrizioni delle variabili di hello, vedere hello [prerequisiti](#prerequisites) sezione in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="933b6-324">For more descriptions of hello variables, see hello [Prerequisites](#prerequisites) section in this tutorial.</span></span>

    <span data-ttu-id="933b6-325">$coordstart e $coordend sono l'avvio del flusso di lavoro di hello e l'ora di fine.</span><span class="sxs-lookup"><span data-stu-id="933b6-325">$coordstart and $coordend are hello workflow starting and ending time.</span></span> <span data-ttu-id="933b6-326">toofind ora UTC o GMT hello, cercare "utc ora" bing.com. Hello $coordFrequency è la frequenza in minuti che toorun hello flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="933b6-326">toofind out hello UTC/GMT time, search "utc time" on bing.com. hello $coordFrequency is how often in minutes you want toorun hello workflow.</span></span>
3. <span data-ttu-id="933b6-327">Aggiungere lo script toohello seguente hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-327">Append hello following toohello script.</span></span> <span data-ttu-id="933b6-328">Questa parte definisce payload Oozie hello:</span><span class="sxs-lookup"><span data-stu-id="933b6-328">This part defines hello Oozie payload:</span></span>

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
   > <span data-ttu-id="933b6-329">file di payload invio del flusso di lavoro toohello differenza principale rispetto Hello è variabile hello **oozie.coord.application.path**.</span><span class="sxs-lookup"><span data-stu-id="933b6-329">hello major difference compared toohello workflow submission payload file is hello variable **oozie.coord.application.path**.</span></span> <span data-ttu-id="933b6-330">Quando si invia un processo del flusso di lavoro si usa invece la variabile **oozie.wf.application.path** .</span><span class="sxs-lookup"><span data-stu-id="933b6-330">When you submit a workflow job, you use **oozie.wf.application.path** instead.</span></span>

4. <span data-ttu-id="933b6-331">Aggiungere lo script toohello seguente hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-331">Append hello following toohello script.</span></span> <span data-ttu-id="933b6-332">Questa parte Controlla stato del servizio web Oozie hello:</span><span class="sxs-lookup"><span data-stu-id="933b6-332">This part checks hello Oozie web service status:</span></span>

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
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check hello server status and re-run hello job."
            exit 1
        }
    }
    ```

5. <span data-ttu-id="933b6-333">Aggiungere lo script toohello seguente hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-333">Append hello following toohello script.</span></span> <span data-ttu-id="933b6-334">Questa parte consente di creare un processo Oozie:</span><span class="sxs-lookup"><span data-stu-id="933b6-334">This part creates an Oozie job:</span></span>

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
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
   > <span data-ttu-id="933b6-335">Quando si invia un processo del flusso di lavoro, è necessario effettuare un altro processo di hello toostart web servizio chiamata dopo hello processo viene creato.</span><span class="sxs-lookup"><span data-stu-id="933b6-335">When you submit a workflow job, you must make another web service call toostart hello job after hello job is created.</span></span> <span data-ttu-id="933b6-336">In questo caso, il processo di coordinatore hello viene attivato da ora.</span><span class="sxs-lookup"><span data-stu-id="933b6-336">In this case, hello coordinator job is triggered by time.</span></span> <span data-ttu-id="933b6-337">processo Hello verrà avviato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="933b6-337">hello job will start automatically.</span></span>

6. <span data-ttu-id="933b6-338">Aggiungere lo script toohello seguente hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-338">Append hello following toohello script.</span></span> <span data-ttu-id="933b6-339">Questa parte controlla lo stato del processo Oozie hello:</span><span class="sxs-lookup"><span data-stu-id="933b6-339">This part checks hello Oozie job status:</span></span>

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
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

7. <span data-ttu-id="933b6-340">(Facoltativo) Aggiungere lo script toohello seguente hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-340">(Optional) Append hello following toohello script.</span></span>

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
        Write-Host "Killing hello Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for hello 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. <span data-ttu-id="933b6-341">Aggiungere hello toohello script seguente:</span><span class="sxs-lookup"><span data-stu-id="933b6-341">Append hello following toohello script:</span></span>

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    <span data-ttu-id="933b6-342">Rimuovere i segni # hello se si desidera toorun hello altre funzioni.</span><span class="sxs-lookup"><span data-stu-id="933b6-342">Remove hello # signs if you want toorun hello additional functions.</span></span>
9. <span data-ttu-id="933b6-343">Se si usa la versione 2.1 del cluster HDinsight, sostituire "https://$clusterName.azurehdinsight.net:443/oozie/v2/" con "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span><span class="sxs-lookup"><span data-stu-id="933b6-343">If your HDinsight cluster is version 2.1, replace "https://$clusterName.azurehdinsight.net:443/oozie/v2/" with "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span></span> <span data-ttu-id="933b6-344">Versione del cluster HDInsight 2.1 non non supporta la versione 2 di servizi web hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-344">HDInsight cluster version 2.1 does not supports version 2 of hello web services.</span></span>
10. <span data-ttu-id="933b6-345">Fare clic su **Esegui Script** o premere **F5** script hello toorun.</span><span class="sxs-lookup"><span data-stu-id="933b6-345">Click **Run Script** or press **F5** toorun hello script.</span></span> <span data-ttu-id="933b6-346">output di Hello sarà simile a:</span><span class="sxs-lookup"><span data-stu-id="933b6-346">hello output will be similar to:</span></span>

     ![Output dell'esecuzione del flusso di lavoro nell'esercitazione][img-runworkflow-output]
11. <span data-ttu-id="933b6-348">Connettersi tooyour dati del Database SQL toosee hello esportata.</span><span class="sxs-lookup"><span data-stu-id="933b6-348">Connect tooyour SQL Database toosee hello exported data.</span></span>

<span data-ttu-id="933b6-349">**log degli errori di processo hello toocheck**</span><span class="sxs-lookup"><span data-stu-id="933b6-349">**toocheck hello job error log**</span></span>

<span data-ttu-id="933b6-350">tootroubleshoot un flusso di lavoro, file di log Oozie hello è reperibile in C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log dal nodo head del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-350">tootroubleshoot a workflow, hello Oozie log file can be found at C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log from hello cluster headnode.</span></span> <span data-ttu-id="933b6-351">Per informazioni su RDP, vedere [cluster HDInsight amministrazione mediante hello Azure portal][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="933b6-351">For information on RDP, see [Administering HDInsight clusters using hello Azure portal][hdinsight-admin-portal].</span></span>

<span data-ttu-id="933b6-352">**esercitazione hello toorerun**</span><span class="sxs-lookup"><span data-stu-id="933b6-352">**toorerun hello tutorial**</span></span>

<span data-ttu-id="933b6-353">flusso di lavoro hello toorerun, è necessario eseguire hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="933b6-353">toorerun hello workflow, you must perform hello following tasks:</span></span>

* <span data-ttu-id="933b6-354">Eliminare i file di output di hello Hive script.</span><span class="sxs-lookup"><span data-stu-id="933b6-354">Delete hello Hive script output file.</span></span>
* <span data-ttu-id="933b6-355">Eliminare i dati di hello nella tabella log4jLogsCount hello.</span><span class="sxs-lookup"><span data-stu-id="933b6-355">Delete hello data in hello log4jLogsCount table.</span></span>

<span data-ttu-id="933b6-356">Di seguito è riportato un esempio di script di Windows PowerShell che è possibile usare:</span><span class="sxs-lookup"><span data-stu-id="933b6-356">Here is a sample Windows PowerShell script that you can use:</span></span>

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="933b6-357">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="933b6-357">Next steps</span></span>
<span data-ttu-id="933b6-358">In questa esercitazione, si è appreso come toodefine un flusso di lavoro Oozie e un coordinatore Oozie e come toorun un coordinatore Oozie processo usando Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="933b6-358">In this tutorial, you learned how toodefine an Oozie workflow and an Oozie coordinator, and how toorun an Oozie coordinator job by using Azure PowerShell.</span></span> <span data-ttu-id="933b6-359">toolearn informazioni, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="933b6-359">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="933b6-360">[Introduzione a HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="933b6-360">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="933b6-361">[Usare l'archivio BLOB di Azure con HDInsight][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="933b6-361">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="933b6-362">[Amministrare HDInsight con Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="933b6-362">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="933b6-363">[Caricare dati tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="933b6-363">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="933b6-364">[Usare Sqoop con Hadoop in HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="933b6-364">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="933b6-365">[Usare Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="933b6-365">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="933b6-366">[Usare Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="933b6-366">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="933b6-367">[Sviluppare programmi MapReduce Java per HDInsight][hdinsight-develop-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="933b6-367">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-java-mapreduce]</span></span>

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
