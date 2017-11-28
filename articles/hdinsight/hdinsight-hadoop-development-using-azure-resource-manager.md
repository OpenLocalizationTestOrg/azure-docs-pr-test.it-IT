---
title: strumenti di aaaMigrate tooAzure Gestione risorse per HDInsight | Documenti Microsoft
description: "Modalità di strumenti toomigrate tooAzure lo sviluppo di gestione risorse per i cluster HDInsight"
services: hdinsight
editor: cgronlun
manager: jhubbard
author: nitinme
documentationcenter: 
ms.assetid: 05efedb5-6456-4552-87ff-156d77fbe2e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: c087ae63d2544e5badae6be9c258f783aa92e2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-resource-manager-based-development-tools-for-hdinsight-clusters"></a><span data-ttu-id="8e6a6-103">Strumenti di sviluppo basato su Gestione risorse tooAzure la migrazione per i cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="8e6a6-103">Migrating tooAzure Resource Manager-based development tools for HDInsight clusters</span></span>

<span data-ttu-id="8e6a6-104">In HDInsight stanno per essere deprecati gli strumenti basati su Azure Service Management (ASM) per HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-104">HDInsight is deprecating Azure Service Manager (ASM)-based tools for HDInsight.</span></span> <span data-ttu-id="8e6a6-105">Se è stato utilizzato hello HDInsight .NET SDK toowork, CLI di Azure o Azure PowerShell con i cluster HDInsight, sono invitati toouse hello basato su Azure Resource Manager ARM le versioni di .NET SDK in futuro, PowerShell e CLI.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-105">If you have been using Azure PowerShell, Azure CLI, or hello HDInsight .NET SDK toowork with HDInsight clusters, you are encouraged toouse hello Azure Resource Manager (ARM)-based versions of PowerShell, CLI, and .NET SDK going forward.</span></span> <span data-ttu-id="8e6a6-106">In questo articolo vengono forniti i puntatori sull'approccio toomigrate toohello nuovo basato su ARM.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-106">This article provides pointers on how toomigrate toohello new ARM-based approach.</span></span> <span data-ttu-id="8e6a6-107">Se applicabile, questo articolo sono inoltre disponibili le differenze di hello tra gli approcci ASM e ARM hello per HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-107">Wherever applicable, this article also points out hello differences between hello ASM and ARM approaches for HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e6a6-108">supporto di Hello per ASM basati CLI, PowerShell e .NET SDK verrà sospeso **il 1 ° gennaio 2017**.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-108">hello support for ASM based PowerShell, CLI, and .NET SDK will discontinue on **January 1, 2017**.</span></span>
> 
> 

## <a name="migrating-azure-cli-tooazure-resource-manager"></a><span data-ttu-id="8e6a6-109">Migrazione tooAzure CLI di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8e6a6-109">Migrating Azure CLI tooAzure Resource Manager</span></span>
<span data-ttu-id="8e6a6-110">Hello CLI di Azure predefinito ora tooAzure modalità di gestione risorse (ARM), a meno che non si esegue l'aggiornamento da un'installazione precedente. In questo caso, potrebbe essere necessario toouse hello `azure config mode arm` modalità tooARM tooswitch dei comandi.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-110">hello Azure CLI now defaults tooAzure Resource Manager (ARM) mode, unless you are upgrading from a previous installation; in this case, you may need toouse hello `azure config mode arm` command tooswitch tooARM mode.</span></span>

<span data-ttu-id="8e6a6-111">comandi di base Hello che hello CLI di Azure fornito toowork con HDInsight mediante la gestione del servizio di Azure (ASM) sono hello stesso quando si utilizza ARM; tuttavia alcuni parametri e le opzioni siano i nuovi nomi, e sono disponibili molti nuovi parametri quando si utilizza ARM.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-111">hello basic commands that hello Azure CLI provided toowork with HDInsight using Azure Service Management (ASM) are hello same when using ARM; however some parameters and switches may have new names, and there are many new parameters available when using ARM.</span></span> <span data-ttu-id="8e6a6-112">Ad esempio, è ora possibile usare `azure hdinsight cluster create` toospecify hello rete virtuale di Azure che deve essere creato un cluster o Hive e Oozie metastore informazioni.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-112">For example, you can now use `azure hdinsight cluster create` toospecify hello Azure Virtual Network that a cluster should be created in, or Hive and Oozie metastore information.</span></span>

<span data-ttu-id="8e6a6-113">Ecco i comandi di base per l'utilizzo di HDInsight tramite Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="8e6a6-113">Basic commands for working with HDInsight through Azure Resource Manager are:</span></span>

* <span data-ttu-id="8e6a6-114">`azure hdinsight cluster create` : crea un nuovo cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-114">`azure hdinsight cluster create` - creates a new HDInsight cluster</span></span>
* <span data-ttu-id="8e6a6-115">`azure hdinsight cluster delete` : elimina un cluster HDInsight esistente.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-115">`azure hdinsight cluster delete` - deletes an existing HDInsight cluster</span></span>
* <span data-ttu-id="8e6a6-116">`azure hdinsight cluster show` : visualizza informazioni su un cluster esistente.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-116">`azure hdinsight cluster show` - display information about an existing cluster</span></span>
* <span data-ttu-id="8e6a6-117">`azure hdinsight cluster list` : elenca i cluster HDInsight per la sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="8e6a6-117">`azure hdinsight cluster list` - lists HDInsight clusters for your Azure subscription</span></span>

<span data-ttu-id="8e6a6-118">Hello utilizzare `-h` passare parametri di hello tooinspect e le opzioni disponibili per ogni comando.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-118">Use hello `-h` switch tooinspect hello parameters and switches available for each command.</span></span>

### <a name="new-commands"></a><span data-ttu-id="8e6a6-119">Nuovi comandi</span><span class="sxs-lookup"><span data-stu-id="8e6a6-119">New commands</span></span>
<span data-ttu-id="8e6a6-120">Ecco i nuovi comandi disponibili con Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="8e6a6-120">New commands available with Azure Resource Manager are:</span></span>

* <span data-ttu-id="8e6a6-121">`azure hdinsight cluster resize`-dinamicamente modifiche hello numero di nodi di lavoro in cluster hello</span><span class="sxs-lookup"><span data-stu-id="8e6a6-121">`azure hdinsight cluster resize` - dynamically changes hello number of worker nodes in hello cluster</span></span>
* <span data-ttu-id="8e6a6-122">`azure hdinsight cluster enable-http-access`-Abilita HTTPs accesso toohello cluster (in per impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-122">`azure hdinsight cluster enable-http-access` - enables HTTPs access toohello cluster (on by default)</span></span>
* <span data-ttu-id="8e6a6-123">`azure hdinsight cluster disable-http-access`-Disabilita cluster toohello di accesso HTTPs</span><span class="sxs-lookup"><span data-stu-id="8e6a6-123">`azure hdinsight cluster disable-http-access` - disables HTTPs access toohello cluster</span></span>
* <span data-ttu-id="8e6a6-124">`azure hdinsight script-action`: fornisce i comandi per la creazione o la gestione di azioni script in un cluster.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-124">`azure hdinsight script-action` - provides commands for creating/managing Script Actions on a cluster</span></span>
* <span data-ttu-id="8e6a6-125">`azure hdinsight config`-sono disponibili comandi per la creazione di un file di configurazione che può essere utilizzata con hello `hdinsight cluster create` comando tooprovide informazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-125">`azure hdinsight config` - provides commands for creating a configuration file that can be used with hello `hdinsight cluster create` command tooprovide configuration information.</span></span>

### <a name="deprecated-commands"></a><span data-ttu-id="8e6a6-126">Comandi deprecati</span><span class="sxs-lookup"><span data-stu-id="8e6a6-126">Deprecated commands</span></span>
<span data-ttu-id="8e6a6-127">Se si utilizza hello `azure hdinsight job` cluster di HDInsight tooyour processi toosubmit comandi, queste non sono disponibili tramite i comandi di hello ARM.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-127">If you use hello `azure hdinsight job` commands toosubmit jobs tooyour HDInsight cluster, these are not available through hello ARM commands.</span></span> <span data-ttu-id="8e6a6-128">Se è necessario tooprogrammatically invia i processi tooHDInsight dagli script, si dovrebbe usare invece hello API REST fornita da HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-128">If you need tooprogrammatically submit jobs tooHDInsight from scripts, you should instead use hello REST APIs provided by HDInsight.</span></span> <span data-ttu-id="8e6a6-129">Per ulteriori informazioni sull'invio di processi usando le API REST, vedere hello seguenti documenti.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-129">For more information on submitting jobs using REST APIs, see hello following documents.</span></span>

* [<span data-ttu-id="8e6a6-130">Eseguire processi MapReduce con Hadoop in HDInsight mediante cURL</span><span class="sxs-lookup"><span data-stu-id="8e6a6-130">Run MapReduce jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-mapreduce-curl.md)
* [<span data-ttu-id="8e6a6-131">Eseguire query Hive con Hadoop in HDInsight mediante Curl</span><span class="sxs-lookup"><span data-stu-id="8e6a6-131">Run Hive queries with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-hive-curl.md)
* [<span data-ttu-id="8e6a6-132">Eseguire processi Pig con Hadoop in HDInsight mediante cUrl</span><span class="sxs-lookup"><span data-stu-id="8e6a6-132">Run Pig jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-pig-curl.md)

<span data-ttu-id="8e6a6-133">Per informazioni su altri toorun modi MapReduce, Hive, Pig in modo interattivo, vedere [utilizzare MapReduce con Hadoop in HDInsight](hdinsight-use-mapreduce.md), [utilizzare Hive con Hadoop in HDInsight](hdinsight-use-hive.md), e [usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="8e6a6-133">For information on other ways toorun MapReduce, Hive, and Pig interactively, see [Use MapReduce with Hadoop on HDInsight](hdinsight-use-mapreduce.md), [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md), and [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

### <a name="examples"></a><span data-ttu-id="8e6a6-134">esempi</span><span class="sxs-lookup"><span data-stu-id="8e6a6-134">Examples</span></span>
<span data-ttu-id="8e6a6-135">**Creazione di un cluster**</span><span class="sxs-lookup"><span data-stu-id="8e6a6-135">**Creating a cluster**</span></span>

* <span data-ttu-id="8e6a6-136">Comando precedente (ASM): `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="8e6a6-136">Old command (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>
* <span data-ttu-id="8e6a6-137">Nuovo comando (ARM): `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="8e6a6-137">New command (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>

<span data-ttu-id="8e6a6-138">**Eliminazione di un cluster**</span><span class="sxs-lookup"><span data-stu-id="8e6a6-138">**Deleting a cluster**</span></span>

* <span data-ttu-id="8e6a6-139">Comando precedente (ASM): `azure hdinsight cluster delete myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="8e6a6-139">Old command (ASM) - `azure hdinsight cluster delete myhdicluster`</span></span>
* <span data-ttu-id="8e6a6-140">Nuovo comando (ARM): `azure hdinsight cluster delete mycluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="8e6a6-140">New command (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span></span>

<span data-ttu-id="8e6a6-141">**Elencare i cluster**</span><span class="sxs-lookup"><span data-stu-id="8e6a6-141">**List clusters**</span></span>

* <span data-ttu-id="8e6a6-142">Comando precedente (ASM): `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="8e6a6-142">Old command (ASM) - `azure hdinsight cluster list`</span></span>
* <span data-ttu-id="8e6a6-143">Nuovo comando (ARM): `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="8e6a6-143">New command (ARM) - `azure hdinsight cluster list`</span></span>

> [!NOTE]
> <span data-ttu-id="8e6a6-144">Per il comando di elenco hello, specificando hello gruppo di risorse utilizzando `-g` restituirà solo i cluster hello nel gruppo di risorse specificato hello.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-144">For hello list command, specifying hello resource group using `-g` will return only hello clusters in hello specified resource group.</span></span>
> 
> 

<span data-ttu-id="8e6a6-145">**Mostrare informazioni sul cluster**</span><span class="sxs-lookup"><span data-stu-id="8e6a6-145">**Show cluster information**</span></span>

* <span data-ttu-id="8e6a6-146">Comando precedente (ASM): `azure hdinsight cluster show myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="8e6a6-146">Old command (ASM) - `azure hdinsight cluster show myhdicluster`</span></span>
* <span data-ttu-id="8e6a6-147">Nuovo comando (ARM): `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="8e6a6-147">New command (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span></span>

## <a name="migrating-azure-powershell-tooazure-resource-manager"></a><span data-ttu-id="8e6a6-148">La migrazione di Azure PowerShell tooAzure Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="8e6a6-148">Migrating Azure PowerShell tooAzure Resource Manager</span></span>
<span data-ttu-id="8e6a6-149">informazioni generali su Azure PowerShell Hello in modalità Azure Resource Manager (ARM) hello sono reperibile in [tramite Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="8e6a6-149">hello general information about Azure PowerShell in hello Azure Resource Manager (ARM) mode can be found at [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="8e6a6-150">i cmdlet di Azure PowerShell ARM Hello può essere installato side-by-side con hello cmdlet ASM.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-150">hello Azure PowerShell ARM cmdlets can be installed side-by-side with hello ASM cmdlets.</span></span> <span data-ttu-id="8e6a6-151">è possibile distinguere i cmdlet di Hello dalle due modalità di hello con i relativi nomi.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-151">hello cmdlets from hello two modes can be distinguished by their names.</span></span>  <span data-ttu-id="8e6a6-152">modalità ARM Hello è *AzureRmHDInsight* nei nomi di cmdlet hello confronto troppo*AzureHDInsight* in modalità ASM hello.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-152">hello ARM mode has *AzureRmHDInsight* in hello cmdlet names comparing too*AzureHDInsight* in hello ASM mode.</span></span>  <span data-ttu-id="8e6a6-153">Ad esempio, *New-AzureRmHDInsightCluster* e *New-AzureHDInsightCluster*.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-153">For example, *New-AzureRmHDInsightCluster* vs. *New-AzureHDInsightCluster*.</span></span> <span data-ttu-id="8e6a6-154">Parametri e le opzioni possono avere nomi nuovi e sono disponibili molti nuovi parametri quando si usa ARM.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-154">Parameters and switches may have news names, and there are many new parameters available when using ARM.</span></span>  <span data-ttu-id="8e6a6-155">Ad esempio, alcuni cmdlet richiedono una nuova opzione denominata *- ResourceGroupName*.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-155">For example, several cmdlets require a new switch called *-ResourceGroupName*.</span></span> 

<span data-ttu-id="8e6a6-156">Prima di poter utilizzare i cmdlet di HDInsight hello, è necessario connettersi tooyour account Azure e creare un nuovo gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="8e6a6-156">Before you can use hello HDInsight cmdlets, you must connect tooyour Azure account, and create a new resource group:</span></span>

* <span data-ttu-id="8e6a6-157">Login-AzureRmAccount o [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span><span class="sxs-lookup"><span data-stu-id="8e6a6-157">Login-AzureRmAccount or [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span></span> <span data-ttu-id="8e6a6-158">Vedere [Autenticazione di un'entità servizio con Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-158">See [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span></span>
* [<span data-ttu-id="8e6a6-159">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8e6a6-159">New-AzureRmResourceGroup</span></span>](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a><span data-ttu-id="8e6a6-160">Cmdlet rinominati</span><span class="sxs-lookup"><span data-stu-id="8e6a6-160">Renamed cmdlets</span></span>
<span data-ttu-id="8e6a6-161">hello toolist i cmdlet di HDInsight ASM nella console di Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8e6a6-161">toolist hello HDInsight ASM cmdlets in Windows PowerShell console:</span></span>

    help *azurermhdinsight*

<span data-ttu-id="8e6a6-162">Hello nella tabella seguente elenca i cmdlet ASM hello e i relativi nomi in modalità ARM hello:</span><span class="sxs-lookup"><span data-stu-id="8e6a6-162">hello following table lists hello ASM cmdlets and their names in hello ARM mode:</span></span>

| <span data-ttu-id="8e6a6-163">Cmdlet ASM</span><span class="sxs-lookup"><span data-stu-id="8e6a6-163">ASM cmdlets</span></span> | <span data-ttu-id="8e6a6-164">Cmdlet ARM</span><span class="sxs-lookup"><span data-stu-id="8e6a6-164">ARM cmdlets</span></span> |
| --- | --- |
| <span data-ttu-id="8e6a6-165">Add-AzureHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="8e6a6-165">Add-AzureHDInsightConfigValues</span></span> |[<span data-ttu-id="8e6a6-166">Add-AzureRmHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="8e6a6-166">Add-AzureRmHDInsightConfigValues</span></span>](https://msdn.microsoft.com/library/mt603530.aspx) |
| <span data-ttu-id="8e6a6-167">Add-AzureHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="8e6a6-167">Add-AzureHDInsightMetastore</span></span> |[<span data-ttu-id="8e6a6-168">Add-AzureRmHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="8e6a6-168">Add-AzureRmHDInsightMetastore</span></span>](https://msdn.microsoft.com/library/mt603670.aspx) |
| <span data-ttu-id="8e6a6-169">Add-AzureHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="8e6a6-169">Add-AzureHDInsightScriptAction</span></span> |[<span data-ttu-id="8e6a6-170">Add-AzureRmHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="8e6a6-170">Add-AzureRmHDInsightScriptAction</span></span>](https://msdn.microsoft.com/library/mt603527.aspx) |
| <span data-ttu-id="8e6a6-171">Add-AzureHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="8e6a6-171">Add-AzureHDInsightStorage</span></span> |[<span data-ttu-id="8e6a6-172">Add-AzureRmHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="8e6a6-172">Add-AzureRmHDInsightStorage</span></span>](https://msdn.microsoft.com/library/mt619445.aspx) |
| <span data-ttu-id="8e6a6-173">Get-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="8e6a6-173">Get-AzureHDInsightCluster</span></span> |[<span data-ttu-id="8e6a6-174">Get-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="8e6a6-174">Get-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619371.aspx) |
| <span data-ttu-id="8e6a6-175">Get-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="8e6a6-175">Get-AzureHDInsightJob</span></span> |[<span data-ttu-id="8e6a6-176">Get-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="8e6a6-176">Get-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603590.aspx) |
| <span data-ttu-id="8e6a6-177">Get-AzureHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="8e6a6-177">Get-AzureHDInsightJobOutput</span></span> |[<span data-ttu-id="8e6a6-178">Get-AzureRmHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="8e6a6-178">Get-AzureRmHDInsightJobOutput</span></span>](https://msdn.microsoft.com/library/mt603793.aspx) |
| <span data-ttu-id="8e6a6-179">Get-AzureHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="8e6a6-179">Get-AzureHDInsightProperties</span></span> |[<span data-ttu-id="8e6a6-180">Get-AzureRmHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="8e6a6-180">Get-AzureRmHDInsightProperties</span></span>](https://msdn.microsoft.com/library/mt603546.aspx) |
| <span data-ttu-id="8e6a6-181">Grant-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="8e6a6-181">Grant-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="8e6a6-182">Grant-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="8e6a6-182">Grant-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619407.aspx) |
| <span data-ttu-id="8e6a6-183">Grant-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="8e6a6-183">Grant-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="8e6a6-184">Grant-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="8e6a6-184">Grant-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603717.aspx) |
| <span data-ttu-id="8e6a6-185">Invoke-AzureHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="8e6a6-185">Invoke-AzureHDInsightHiveJob</span></span> |[<span data-ttu-id="8e6a6-186">Invoke-AzureRmHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="8e6a6-186">Invoke-AzureRmHDInsightHiveJob</span></span>](https://msdn.microsoft.com/library/mt603593.aspx) |
| <span data-ttu-id="8e6a6-187">New-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="8e6a6-187">New-AzureHDInsightCluster</span></span> |[<span data-ttu-id="8e6a6-188">New-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="8e6a6-188">New-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619331.aspx) |
| <span data-ttu-id="8e6a6-189">New-AzureHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="8e6a6-189">New-AzureHDInsightClusterConfig</span></span> |[<span data-ttu-id="8e6a6-190">New-AzureRmHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="8e6a6-190">New-AzureRmHDInsightClusterConfig</span></span>](https://msdn.microsoft.com/library/mt603700.aspx) |
| <span data-ttu-id="8e6a6-191">New-AzureHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="8e6a6-191">New-AzureHDInsightHiveJobDefinition</span></span> |[<span data-ttu-id="8e6a6-192">New-AzureRmHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="8e6a6-192">New-AzureRmHDInsightHiveJobDefinition</span></span>](https://msdn.microsoft.com/library/mt619448.aspx) |
| <span data-ttu-id="8e6a6-193">New-AzureHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="8e6a6-193">New-AzureHDInsightMapReduceJobDefinition</span></span> |[<span data-ttu-id="8e6a6-194">New-AzureRmHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="8e6a6-194">New-AzureRmHDInsightMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="8e6a6-195">New-AzureHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="8e6a6-195">New-AzureHDInsightPigJobDefinition</span></span> |[<span data-ttu-id="8e6a6-196">New-AzureRmHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="8e6a6-196">New-AzureRmHDInsightPigJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603671.aspx) |
| <span data-ttu-id="8e6a6-197">New-AzureHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="8e6a6-197">New-AzureHDInsightSqoopJobDefinition</span></span> |[<span data-ttu-id="8e6a6-198">New-AzureRmHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="8e6a6-198">New-AzureRmHDInsightSqoopJobDefinition</span></span>](https://msdn.microsoft.com/library/mt608551.aspx) |
| <span data-ttu-id="8e6a6-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="8e6a6-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span></span> |[<span data-ttu-id="8e6a6-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="8e6a6-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="8e6a6-201">Remove-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="8e6a6-201">Remove-AzureHDInsightCluster</span></span> |[<span data-ttu-id="8e6a6-202">Remove-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="8e6a6-202">Remove-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619431.aspx) |
| <span data-ttu-id="8e6a6-203">Revoke-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="8e6a6-203">Revoke-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="8e6a6-204">Revoke-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="8e6a6-204">Revoke-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619375.aspx) |
| <span data-ttu-id="8e6a6-205">Revoke-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="8e6a6-205">Revoke-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="8e6a6-206">Revoke-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="8e6a6-206">Revoke-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603523.aspx) |
| <span data-ttu-id="8e6a6-207">Set-AzureHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="8e6a6-207">Set-AzureHDInsightClusterSize</span></span> |[<span data-ttu-id="8e6a6-208">Set-AzureRmHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="8e6a6-208">Set-AzureRmHDInsightClusterSize</span></span>](https://msdn.microsoft.com/library/mt603513.aspx) |
| <span data-ttu-id="8e6a6-209">Set-AzureHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="8e6a6-209">Set-AzureHDInsightDefaultStorage</span></span> |[<span data-ttu-id="8e6a6-210">Set-AzureRmHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="8e6a6-210">Set-AzureRmHDInsightDefaultStorage</span></span>](https://msdn.microsoft.com/library/mt603486.aspx) |
| <span data-ttu-id="8e6a6-211">Start-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="8e6a6-211">Start-AzureHDInsightJob</span></span> |[<span data-ttu-id="8e6a6-212">Start-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="8e6a6-212">Start-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603798.aspx) |
| <span data-ttu-id="8e6a6-213">Stop-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="8e6a6-213">Stop-AzureHDInsightJob</span></span> |[<span data-ttu-id="8e6a6-214">Stop-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="8e6a6-214">Stop-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt619424.aspx) |
| <span data-ttu-id="8e6a6-215">Use-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="8e6a6-215">Use-AzureHDInsightCluster</span></span> |[<span data-ttu-id="8e6a6-216">Use-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="8e6a6-216">Use-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619442.aspx) |
| <span data-ttu-id="8e6a6-217">Wait-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="8e6a6-217">Wait-AzureHDInsightJob</span></span> |[<span data-ttu-id="8e6a6-218">Wait-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="8e6a6-218">Wait-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a><span data-ttu-id="8e6a6-219">Nuovi cmdlet</span><span class="sxs-lookup"><span data-stu-id="8e6a6-219">New cmdlets</span></span>
<span data-ttu-id="8e6a6-220">di seguito Hello sono hello nuovi cmdlet che sono disponibili solo in modalità di hello ARM.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-220">hello following are hello new cmdlets that are only available in hello ARM mode.</span></span> 

<span data-ttu-id="8e6a6-221">**Cmdlet correlati all'azione script:**</span><span class="sxs-lookup"><span data-stu-id="8e6a6-221">**Script action related cmdlets:**</span></span>

* <span data-ttu-id="8e6a6-222">**Get-AzureRmHDInsightPersistedScriptAction**: hello Ottiene persistente azioni script per un cluster sono elencati in ordine cronologico e ottiene i dettagli per un'azione script persistente specificato.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-222">**Get-AzureRmHDInsightPersistedScriptAction**: Gets hello persisted script actions for a cluster and lists them in chronological order, or gets details for a specified persisted script action.</span></span> 
* <span data-ttu-id="8e6a6-223">**Get-AzureRmHDInsightScriptActionHistory**: Ottiene cronologia dell'azione script hello per un cluster e sono elencati in ordine cronologico inverso o ottiene i dettagli di un'azione di script eseguita in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-223">**Get-AzureRmHDInsightScriptActionHistory**: Gets hello script action history for a cluster and lists it in reverse chronological order, or gets details of a previously executed script action.</span></span> 
* <span data-ttu-id="8e6a6-224">**Remove AzureRmHDInsightPersistedScriptAction**: rimuove un'azione script persistente da un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-224">**Remove-AzureRmHDInsightPersistedScriptAction**: Removes a persisted script action from an HDInsight cluster.</span></span>
* <span data-ttu-id="8e6a6-225">**Set-AzureRmHDInsightPersistedScriptAction**: imposta una toobe azione script precedentemente eseguito un'azione di script con salvataggio permanente.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-225">**Set-AzureRmHDInsightPersistedScriptAction**: Sets a previously executed script action toobe a persisted script action.</span></span>
* <span data-ttu-id="8e6a6-226">**AzureRmHDInsightScriptAction inviare**: invia un nuovo cluster di Azure HDInsight tooan azione script.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-226">**Submit-AzureRmHDInsightScriptAction**: Submits a new script action tooan Azure HDInsight cluster.</span></span> 

<span data-ttu-id="8e6a6-227">Per altre informazioni sull'utilizzo, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="8e6a6-227">For additional usage information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="8e6a6-228">**Cmdlet correlati a identità del cluster:**</span><span class="sxs-lookup"><span data-stu-id="8e6a6-228">**Clsuter identity related cmdlets:**</span></span>

* <span data-ttu-id="8e6a6-229">**AzureRmHDInsightClusterIdentity aggiungere**: aggiunge un oggetto di configurazione di cluster identità tooa cluster in modo che hello cluster HDInsight possono accedere gli archivi di Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-229">**Add-AzureRmHDInsightClusterIdentity**: Adds a cluster identity tooa cluster configuration object so that hello HDInsight cluster can access Azure Data Lake Stores.</span></span> <span data-ttu-id="8e6a6-230">Vedere [Creare un cluster HDInsight con Archivio Data Lake tramite Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8e6a6-230">See [Create an HDInsight cluster with Data Lake Store using Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

### <a name="examples"></a><span data-ttu-id="8e6a6-231">esempi</span><span class="sxs-lookup"><span data-stu-id="8e6a6-231">Examples</span></span>
<span data-ttu-id="8e6a6-232">**Creare cluster**</span><span class="sxs-lookup"><span data-stu-id="8e6a6-232">**Create cluster**</span></span>

<span data-ttu-id="8e6a6-233">Comando precedente (ASM):</span><span class="sxs-lookup"><span data-stu-id="8e6a6-233">Old command (ASM):</span></span> 

    New-AzureHDInsightCluster `
        -Name $clusterName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainerName $containerName `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -Credential $httpCredential `
        -SshCredential $sshCredential

<span data-ttu-id="8e6a6-234">Nuovo comando (ARM):</span><span class="sxs-lookup"><span data-stu-id="8e6a6-234">New command (ARM):</span></span>

    New-AzureRmHDInsightCluster `
        -ClusterName $clusterName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainer $containerName  `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -HttpCredential $httpcredentials `
        -SshCredential $sshCredentials


<span data-ttu-id="8e6a6-235">**Eliminare cluster**</span><span class="sxs-lookup"><span data-stu-id="8e6a6-235">**Delete cluster**</span></span>

<span data-ttu-id="8e6a6-236">Comando precedente (ASM):</span><span class="sxs-lookup"><span data-stu-id="8e6a6-236">Old command (ASM):</span></span>

    Remove-AzureHDInsightCluster -name $clusterName 

<span data-ttu-id="8e6a6-237">Nuovo comando (ARM):</span><span class="sxs-lookup"><span data-stu-id="8e6a6-237">New command (ARM):</span></span>

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

<span data-ttu-id="8e6a6-238">**Elencare cluster**</span><span class="sxs-lookup"><span data-stu-id="8e6a6-238">**List cluster**</span></span>

<span data-ttu-id="8e6a6-239">Comando precedente (ASM):</span><span class="sxs-lookup"><span data-stu-id="8e6a6-239">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster

<span data-ttu-id="8e6a6-240">Nuovo comando (ARM):</span><span class="sxs-lookup"><span data-stu-id="8e6a6-240">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster 

<span data-ttu-id="8e6a6-241">**Mostrare cluster**</span><span class="sxs-lookup"><span data-stu-id="8e6a6-241">**Show cluster**</span></span>

<span data-ttu-id="8e6a6-242">Comando precedente (ASM):</span><span class="sxs-lookup"><span data-stu-id="8e6a6-242">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster -Name $clusterName

<span data-ttu-id="8e6a6-243">Nuovo comando (ARM):</span><span class="sxs-lookup"><span data-stu-id="8e6a6-243">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a><span data-ttu-id="8e6a6-244">Altri esempi</span><span class="sxs-lookup"><span data-stu-id="8e6a6-244">Other samples</span></span>
* [<span data-ttu-id="8e6a6-245">Creare cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="8e6a6-245">Create HDInsight clusters</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="8e6a6-246">Invio di processi Hive</span><span class="sxs-lookup"><span data-stu-id="8e6a6-246">Submit Hive jobs</span></span>](hdinsight-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="8e6a6-247">Eseguire processi Pig mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e6a6-247">Submit Pig jobs</span></span>](hdinsight-hadoop-use-pig-powershell.md)
* [<span data-ttu-id="8e6a6-248">Eseguire processi Sqoop con Azure PowerShell per Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="8e6a6-248">Submit Sqoop jobs</span></span>](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-toohello-arm-based-hdinsight-net-sdk"></a><span data-ttu-id="8e6a6-249">Migrazione toohello basato su ARM HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8e6a6-249">Migrating toohello ARM-based HDInsight .NET SDK</span></span>
<span data-ttu-id="8e6a6-250">Hello basate su gestione dei servizi Azure [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) è obsoleta.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-250">hello Azure Service Management-based [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is now deprecated.</span></span> <span data-ttu-id="8e6a6-251">Si consiglia toouse hello basate su Gestione risorse di Azure [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="8e6a6-251">You are encouraged toouse hello Azure Resource Management-based [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span></span> <span data-ttu-id="8e6a6-252">Hello pacchetti basato su ASM HDInsight seguenti sono deprecati.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-252">hello following ASM-based HDInsight packages are being deprecated.</span></span>

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

<span data-ttu-id="8e6a6-253">In questa sezione fornisce i puntatori toomore informazioni su come tooperform determinate attività utilizzando hello SDK basato su ARM.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-253">This section provides pointers toomore information on how tooperform certain tasks using hello ARM-based SDK.</span></span>

| <span data-ttu-id="8e6a6-254">Come... utilizzando hello basato su ARM SDK HDInsight</span><span class="sxs-lookup"><span data-stu-id="8e6a6-254">How to... using hello ARM-based HDInsight SDK</span></span> | <span data-ttu-id="8e6a6-255">Collegamenti</span><span class="sxs-lookup"><span data-stu-id="8e6a6-255">Links</span></span> |
| --- | --- |
| <span data-ttu-id="8e6a6-256">Creare cluster HDInsight con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8e6a6-256">Create HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="8e6a6-257">Vedere [Creare cluster basati su Linux in HDInsight tramite .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-257">See [Create HDInsight clusters using .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="8e6a6-258">Personalizzare un cluster tramite un'azione script con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8e6a6-258">Customize a cluster using Script Action with .NET SDK</span></span> |<span data-ttu-id="8e6a6-259">Vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-259">See [Customize HDInsight Linux clusters using Script Action](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span></span> |
| <span data-ttu-id="8e6a6-260">Autenticare le applicazioni in modo interattivo tramite Azure Active Directory con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8e6a6-260">Authenticate applications interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="8e6a6-261">Vedere [Eseguire query Hive con HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-261">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span> <span data-ttu-id="8e6a6-262">frammento di codice Hello in questo articolo usa l'approccio interattivo autenticazione hello.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-262">hello code snippet in this article uses hello interactive authentication approach.</span></span> |
| <span data-ttu-id="8e6a6-263">Autenticare le applicazioni in modo non interattivo tramite Azure Active Directory con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8e6a6-263">Authenticate applications non-interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="8e6a6-264">Vedere [Creare applicazioni .NET HDInsight di autenticazione non interattiva](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-264">See [Create non-interactive applications for HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span></span> |
| <span data-ttu-id="8e6a6-265">Inviare un processo Hive con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8e6a6-265">Submit a Hive job using .NET SDK</span></span> |<span data-ttu-id="8e6a6-266">Vedere [Eseguire query Hive con HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-266">See [Submit Hive jobs](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="8e6a6-267">Inviare un processo Pig con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8e6a6-267">Submit a Pig job using .NET SDK</span></span> |<span data-ttu-id="8e6a6-268">Vedere [Eseguire processi Pig con .NET SDK per Hadoop in HDInsight](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-268">See [Submit Pig jobs](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="8e6a6-269">Inviare un processo Sqoop con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8e6a6-269">Submit a Sqoop job using .NET SDK</span></span> |<span data-ttu-id="8e6a6-270">Vedere [Eseguire processi Sqoop con .NET SDK per Hadoop in HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-270">See [Submit Sqoop jobs](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="8e6a6-271">Elencare cluster HDInsight con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8e6a6-271">List HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="8e6a6-272">Vedere la sezione su come elencare cluster in [Gestire cluster Hadoop in HDInsight tramite .NET SDK](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-272">See [List HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span></span> |
| <span data-ttu-id="8e6a6-273">Ridimensionare cluster HDInsight con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8e6a6-273">Scale HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="8e6a6-274">Vedere la sezione su come ridimensionare cluster in [Gestire cluster Hadoop in HDInsight tramite .NET SDK](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-274">See [Scale HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span></span> |
| <span data-ttu-id="8e6a6-275">Concedere o revocare l'accesso tooHDInsight cluster mediante .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8e6a6-275">Grant/revoke access tooHDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="8e6a6-276">Vedere [cluster tooHDInsight di concedere o revocare l'accesso](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-276">See [Grant/revoke access tooHDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span></span> |
| <span data-ttu-id="8e6a6-277">Aggiornare le credenziali utente HTTP per i cluster HDInsight con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8e6a6-277">Update HTTP user credentials for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="8e6a6-278">Vedere la sezione su come aggiornare le credenziali utente HTTP in [Gestire cluster Hadoop in HDInsight tramite .NET SDK](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-278">See [Update HTTP user credentials for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span></span> |
| <span data-ttu-id="8e6a6-279">Trovare l'account di archiviazione predefinito hello per i cluster HDInsight mediante .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8e6a6-279">Find hello default storage account for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="8e6a6-280">Vedere [trovare account di archiviazione di hello predefinito per i cluster HDInsight](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-280">See [Find hello default storage account for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span></span> |
| <span data-ttu-id="8e6a6-281">Eliminare cluster HDInsight con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8e6a6-281">Delete HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="8e6a6-282">Vedere la sezione su come eliminare cluster in [Gestire cluster Hadoop in HDInsight tramite .NET SDK](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-282">See [Delete HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span></span> |

### <a name="examples"></a><span data-ttu-id="8e6a6-283">esempi</span><span class="sxs-lookup"><span data-stu-id="8e6a6-283">Examples</span></span>
<span data-ttu-id="8e6a6-284">Di seguito sono riportati alcuni esempi su come un'operazione viene eseguita utilizzando hello basato su ASM SDK e il frammento di codice equivalente hello per hello SDK basato su ARM.</span><span class="sxs-lookup"><span data-stu-id="8e6a6-284">Following are some examples on how an operation is performed using hello ASM-based SDK and hello equivalent code snippet for hello ARM-based SDK.</span></span>

<span data-ttu-id="8e6a6-285">**Creazione di un client CRUD del cluster**</span><span class="sxs-lookup"><span data-stu-id="8e6a6-285">**Creating a cluster CRUD client**</span></span>

* <span data-ttu-id="8e6a6-286">Comando precedente (ASM)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-286">Old command (ASM)</span></span>
  
        //Certificate auth
        //This logs hello application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* <span data-ttu-id="8e6a6-287">Nuovo comando (ARM) (autorizzazione dell'entità servizio)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-287">New command (ARM) (Service principal authorization)</span></span>
  
        //Service principal auth
        //This will log hello application in as itself, rather than on behalf of a specific user.
        //For details, including how tooset up hello application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* <span data-ttu-id="8e6a6-288">Nuovo comando (ARM) (autorizzazione utente)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-288">New command (ARM) (User authorization)</span></span>
  
        //User auth
        //This will log hello application in on behalf of hello user.
        //hello end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

<span data-ttu-id="8e6a6-289">**Creazione di un cluster**</span><span class="sxs-lookup"><span data-stu-id="8e6a6-289">**Creating a cluster**</span></span>

* <span data-ttu-id="8e6a6-290">Comando precedente (ASM)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-290">Old command (ASM)</span></span>
  
        var clusterInfo = new ClusterCreateParameters
                    {
                        Name = dnsName,
                        DefaultStorageAccountKey = key,
                        DefaultStorageContainer = defaultStorageContainer,
                        DefaultStorageAccountName = storageAccountDnsName,
                        ClusterSizeInNodes = 1,
                        ClusterType = type,
                        Location = "West US",
                        UserName = "admin",
                        Password = "*******",
                        Version = version,
                        HeadNodeSize = NodeVMSize.Large,
                    };
        clusterInfo.CoreConfiguration.Add(new KeyValuePair<string, string>("config1", "value1"));
        client.CreateCluster(clusterInfo);
* <span data-ttu-id="8e6a6-291">Nuovo comando (ARM)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-291">New command (ARM)</span></span>
  
        var clusterCreateParameters = new ClusterCreateParameters
            {
                Location = "West US",
                ClusterType = "Hadoop",
                Version = "3.1",
                OSType = OSType.Linux,
                DefaultStorageAccountName = "mystorage.blob.core.windows.net",
                DefaultStorageAccountKey =
                    "O9EQvp3A3AjXq/W27rst1GQfLllhp0gUeiUUn2D8zX2lU3taiXSSfqkZlcPv+nQcYUxYw==",
                UserName = "hadoopuser",
                Password = "*******",
                HeadNodeSize = "ExtraLarge",
                RdpUsername = "hdirp",
                RdpPassword = ""*******",
                RdpAccessExpiry = new DateTime(2025, 3, 1),
                ClusterSizeInNodes = 5
            };
        var coreConfigs = new Dictionary<string, string> {{"config1", "value1"}};
        clusterCreateParameters.Configurations.Add(ConfigurationKey.CoreSite, coreConfigs);

<span data-ttu-id="8e6a6-292">**Abilitazione dell'accesso HTTP**</span><span class="sxs-lookup"><span data-stu-id="8e6a6-292">**Enabling HTTP access**</span></span>

* <span data-ttu-id="8e6a6-293">Comando precedente (ASM)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-293">Old command (ASM)</span></span>
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* <span data-ttu-id="8e6a6-294">Nuovo comando (ARM)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-294">New command (ARM)</span></span>
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

<span data-ttu-id="8e6a6-295">**Eliminazione di un cluster**</span><span class="sxs-lookup"><span data-stu-id="8e6a6-295">**Deleting a cluster**</span></span>

* <span data-ttu-id="8e6a6-296">Comando precedente (ASM)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-296">Old command (ASM)</span></span>
  
        client.DeleteCluster(dnsName);
* <span data-ttu-id="8e6a6-297">Nuovo comando (ARM)</span><span class="sxs-lookup"><span data-stu-id="8e6a6-297">New command (ARM)</span></span>
  
        client.Clusters.Delete(resourceGroup, dnsname);

