---
title: aaaCreate Hive tabelle e caricare i dati dall'archiviazione Blob di Azure | Documenti Microsoft
description: Creare tabelle Hive e caricare i dati nelle tabelle toohive blob
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: cff9280d-18ce-4b66-a54f-19f358d1ad90
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 09622972bcac31c2971858393a8340f24e4b7390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a><span data-ttu-id="6638a-103">Creare tabelle Hive e caricare i dati dall'archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="6638a-103">Create Hive tables and load data from Azure Blob Storage</span></span>
<span data-ttu-id="6638a-104">Questo argomento presenta le query Hive generiche che consentono di creare tabelle Hive e di caricare i dati dall'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="6638a-104">This topic presents generic Hive queries that create Hive tables and load data from Azure blob storage.</span></span> <span data-ttu-id="6638a-105">Vengono inoltre forniti alcune indicazioni sul partizionamento di tabelle Hive e sull'utilizzo di hello con ottimizzazione per la riga a colonne (ORC) formattazione tooimprove le prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="6638a-105">Some guidance is also provided on partitioning Hive tables and on using hello Optimized Row Columnar (ORC) formatting tooimprove query performance.</span></span>

<span data-ttu-id="6638a-106">Questo **menu** collegamenti tootopics che descrivono come dati tooingest in ambienti di destinazione in cui i dati hello possono essere archiviati ed elaborati durante hello Team Data Science processo (TDSP).</span><span class="sxs-lookup"><span data-stu-id="6638a-106">This **menu** links tootopics that describe how tooingest data into target environments where hello data can be stored and processed during hello Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="6638a-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6638a-107">Prerequisites</span></span>
<span data-ttu-id="6638a-108">Questo articolo presuppone che l'utente abbia:</span><span class="sxs-lookup"><span data-stu-id="6638a-108">This article assumes that you have:</span></span>

* <span data-ttu-id="6638a-109">Creato un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6638a-109">Created an Azure storage account.</span></span> <span data-ttu-id="6638a-110">Per istruzioni, vedere [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="6638a-110">If you need instructions, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="6638a-111">Il provisioning di un cluster Hadoop personalizzato con hello servizio HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6638a-111">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span>  <span data-ttu-id="6638a-112">Per istruzioni, vedere [Personalizzazione di cluster Hadoop di Azure HDInsight per l'analisi scientifica dei dati](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="6638a-112">If you need instructions, see [Customize Azure HDInsight Hadoop clusters for advanced analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="6638a-113">Cluster toohello di accesso remoto abilitato, effettuato l'accesso, aprire console della riga di comando di hello Hadoop.</span><span class="sxs-lookup"><span data-stu-id="6638a-113">Enabled remote access toohello cluster, logged in, and opened hello Hadoop Command-Line console.</span></span> <span data-ttu-id="6638a-114">Se sono necessarie istruzioni, vedere [hello accesso nodo Head del Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="6638a-114">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="6638a-115">Carica l'archiviazione blob di dati tooAzure</span><span class="sxs-lookup"><span data-stu-id="6638a-115">Upload data tooAzure blob storage</span></span>
<span data-ttu-id="6638a-116">Se una macchina virtuale di Azure è stato creato tramite istruzioni hello fornite [configurare una macchina virtuale di Azure per analitica avanzate](machine-learning-data-science-setup-virtual-machine.md), questo script dovrebbe essere stato scaricato toohello *c:\\ Gli utenti\\\<nome utente\>\\documenti\\gli script di analisi scientifica dei dati* directory sulla macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="6638a-116">If you created an Azure virtual machine by following hello instructions provided in [Set up an Azure virtual machine for advanced analytics](machine-learning-data-science-setup-virtual-machine.md), this script file should have been downloaded toohello *C:\\Users\\\<user name\>\\Documents\\Data Science Scripts* directory on hello virtual machine.</span></span> <span data-ttu-id="6638a-117">Queste query Hive richiedono soltanto che si collega la propria schema dei dati e la configurazione dell'archiviazione blob di Azure in hello campi appropriati toobe pronto per l'invio.</span><span class="sxs-lookup"><span data-stu-id="6638a-117">These Hive queries only require that you plug in your own data schema and Azure blob storage configuration in hello appropriate fields toobe ready for submission.</span></span>

<span data-ttu-id="6638a-118">Si supponga che i dati di hello per le tabelle Hive siano un **non compresso** formato tabulare e che i dati di hello sono stati caricati toohello predefinita (o tooan aggiuntive) contenitore hello dell'account di archiviazione utilizzato da un cluster Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="6638a-118">We assume that hello data for Hive tables is in an **uncompressed** tabular format, and that hello data has been uploaded toohello default (or tooan additional) container of hello storage account used by hello Hadoop cluster.</span></span>

<span data-ttu-id="6638a-119">Se si desidera toopractice su hello **NYC Taxi viaggi dati**, è necessario:</span><span class="sxs-lookup"><span data-stu-id="6638a-119">If you want toopractice on hello **NYC Taxi Trip Data**, you need to:</span></span>

* <span data-ttu-id="6638a-120">**scaricare** hello 24 [NYC Taxi viaggi dati](http://www.andresmh.com/nyctaxitrips) file (12 di andata e ritorno e file file tariffa 12)</span><span class="sxs-lookup"><span data-stu-id="6638a-120">**download** hello 24 [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) files (12 Trip files and 12 Fare files),</span></span>
* <span data-ttu-id="6638a-121">**decomprimere** tutti i file in file con estensione .csv;</span><span class="sxs-lookup"><span data-stu-id="6638a-121">**unzip** all files into .csv files, and then</span></span>
* <span data-ttu-id="6638a-122">**caricare** li toohello predefinito o il contenitore appropriato di hello account di archiviazione di Azure che è stato creato da hello procedura hello [cluster personalizzare Azure HDInsight Hadoop per il processo di Analitica avanzate e tecnologia ](machine-learning-data-science-customize-hadoop-cluster.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="6638a-122">**upload** them toohello default (or appropriate container) of hello Azure storage account that was created by hello procedure outlined in hello [Customize Azure HDInsight Hadoop clusters for Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md) topic.</span></span> <span data-ttu-id="6638a-123">Hello processo tooupload hello CSV file toohello predefinito contenitore nell'account di archiviazione hello è disponibile su questo [pagina](machine-learning-data-science-process-hive-walkthrough.md#upload).</span><span class="sxs-lookup"><span data-stu-id="6638a-123">hello process tooupload hello .csv files toohello default container on hello storage account can be found on this [page](machine-learning-data-science-process-hive-walkthrough.md#upload).</span></span>

## <span data-ttu-id="6638a-124"><a name="submit"></a>La modalità query Hive toosubmit</span><span class="sxs-lookup"><span data-stu-id="6638a-124"><a name="submit"></a>How toosubmit Hive queries</span></span>
<span data-ttu-id="6638a-125">È possibile inviare query Hive mediante:</span><span class="sxs-lookup"><span data-stu-id="6638a-125">Hive queries can be submitted by using:</span></span>

1. [<span data-ttu-id="6638a-126">Inviare le query Hive attraverso la riga di comando di Hadoop nel nodo head del cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="6638a-126">Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>](#headnode)
2. [<span data-ttu-id="6638a-127">Inviare query Hive con hello Editor Hive</span><span class="sxs-lookup"><span data-stu-id="6638a-127">Submit Hive queries with hello Hive Editor</span></span>](#hive-editor)
3. [<span data-ttu-id="6638a-128">Inviare le query Hive con i comandi di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6638a-128">Submit Hive queries with Azure PowerShell Commands</span></span>](#ps)

<span data-ttu-id="6638a-129">Le query Hive sono simili a SQL.</span><span class="sxs-lookup"><span data-stu-id="6638a-129">Hive queries are SQL-like.</span></span> <span data-ttu-id="6638a-130">Se si ha familiarità con SQL, è possibile hello [Hive per SQL utenti irregolarità foglio](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) utile.</span><span class="sxs-lookup"><span data-stu-id="6638a-130">If you are familiar with SQL, you may find hello [Hive for SQL Users Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) useful.</span></span>

<span data-ttu-id="6638a-131">Quando si invia una query Hive, è inoltre possibile controllare destinazione hello dell'output di hello dalle query Hive, sia su hello schermata o tooa file locale nel nodo head hello o tooan blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="6638a-131">When submitting a Hive query, you can also control hello destination of hello output from Hive queries, whether it be on hello screen or tooa local file on hello head node or tooan Azure blob.</span></span>

### <span data-ttu-id="6638a-132"><a name="headnode"></a> 1. Inviare le query Hive attraverso la riga di comando di Hadoop nel nodo head del cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="6638a-132"><a name="headnode"></a> 1. Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>
<span data-ttu-id="6638a-133">Se l'Hive hello query è complessa, invio che direttamente nel nodo head di hello del cluster Hadoop hello in genere comporta toofaster inversione di inviarla con un Editor Hive o gli script di PowerShell di Azure.</span><span class="sxs-lookup"><span data-stu-id="6638a-133">If hello Hive query is complex, submitting it directly in hello head node of hello Hadoop cluster typically leads toofaster turn around than submitting it with a Hive Editor or Azure PowerShell scripts.</span></span>

<span data-ttu-id="6638a-134">Accedi toohello nodo head del cluster Hadoop hello, aprire hello riga di comando di Hadoop nel desktop di hello del nodo head hello e immettere comando `cd %hive_home%\bin`.</span><span class="sxs-lookup"><span data-stu-id="6638a-134">Log in toohello head node of hello Hadoop cluster, open hello Hadoop Command Line on hello desktop of hello head node, and enter command `cd %hive_home%\bin`.</span></span>

<span data-ttu-id="6638a-135">Sono presenti query Hive di tre modi toosubmit hello Hadoop della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="6638a-135">You have three ways toosubmit Hive queries in hello Hadoop Command Line:</span></span>

* <span data-ttu-id="6638a-136">Direttamente</span><span class="sxs-lookup"><span data-stu-id="6638a-136">directly</span></span>
* <span data-ttu-id="6638a-137">Mediante i file con estensione hql</span><span class="sxs-lookup"><span data-stu-id="6638a-137">using .hql files</span></span>
* <span data-ttu-id="6638a-138">con hello Hive console dei comandi</span><span class="sxs-lookup"><span data-stu-id="6638a-138">with hello Hive command console</span></span>

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a><span data-ttu-id="6638a-139">Inviare query Hive direttamente nella riga di comando di Hadoop</span><span class="sxs-lookup"><span data-stu-id="6638a-139">Submit Hive queries directly in Hadoop Command Line.</span></span>
<span data-ttu-id="6638a-140">È possibile eseguire comandi come `hive -e "<your hive query>;` toosubmit query Hive semplici direttamente in Hadoop riga di comando.</span><span class="sxs-lookup"><span data-stu-id="6638a-140">You can run command like `hive -e "<your hive query>;` toosubmit simple Hive queries directly in Hadoop Command Line.</span></span> <span data-ttu-id="6638a-141">Di seguito è riportato un esempio, in strutture di casella rossa hello hello comando che invia query Hive hello e hello casella verde contorni hello output dalla query Hive hello.</span><span class="sxs-lookup"><span data-stu-id="6638a-141">Here is an example, where hello red box outlines hello command that submits hello Hive query, and hello green box outlines hello output from hello Hive query.</span></span>

![Creare un'area di lavoro](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a><span data-ttu-id="6638a-143">Inviare query nei file con estensione hql</span><span class="sxs-lookup"><span data-stu-id="6638a-143">Submit Hive queries in .hql files</span></span>
<span data-ttu-id="6638a-144">Quando query Hive hello è più complicato e dispone di più righe, la modifica delle query nella riga di comando o la console di Hive comando non è pratica.</span><span class="sxs-lookup"><span data-stu-id="6638a-144">When hello Hive query is more complicated and has multiple lines, editing queries in command line or Hive command console is not practical.</span></span> <span data-ttu-id="6638a-145">In alternativa è toouse un editor di testo nel nodo head hello hello Hadoop cluster toosave hello le query Hive in un file .hql in una directory locale del nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="6638a-145">An alternative is toouse a text editor in hello head node of hello Hadoop cluster toosave hello Hive queries in a .hql file in a local directory of hello head node.</span></span> <span data-ttu-id="6638a-146">Quindi query Hive hello nel file .hql hello possono essere inviate utilizzando hello `-f` argomento come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6638a-146">Then hello Hive query in hello .hql file can be submitted by using hello `-f` argument as follows:</span></span>

    hive -f "<path toohello .hql file>"

![Creare un'area di lavoro](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

<span data-ttu-id="6638a-148">**Eliminare la visualizzazione relativa allo stato di avanzamento delle query Hive sullo schermo**</span><span class="sxs-lookup"><span data-stu-id="6638a-148">**Suppress progress status screen print of Hive queries**</span></span>

<span data-ttu-id="6638a-149">Per impostazione predefinita, dopo l'invio query Hive nella riga di comando di Hadoop, lo stato di avanzamento hello del processo MapReduce hello viene stampato nella schermata.</span><span class="sxs-lookup"><span data-stu-id="6638a-149">By default, after Hive query is submitted in Hadoop Command Line, hello progress of hello Map/Reduce job is printed out on screen.</span></span> <span data-ttu-id="6638a-150">toosuppress hello stampa schermata di avanzamento del processo MapReduce hello, è possibile usare un argomento `-S` ("S" in lettere maiuscole) in hello riga di comando come segue:</span><span class="sxs-lookup"><span data-stu-id="6638a-150">toosuppress hello screen print of hello Map/Reduce job progress, you can use an argument `-S` ("S" in upper case) in hello command line as follows:</span></span>

    hive -S -f "<path toohello .hql file>"
<span data-ttu-id="6638a-151">.</span><span class="sxs-lookup"><span data-stu-id="6638a-151">.</span></span>    <span data-ttu-id="6638a-152">hive -S -e "<Hive queries>"</span><span class="sxs-lookup"><span data-stu-id="6638a-152">hive -S -e "<Hive queries>"</span></span>

#### <a name="submit-hive-queries-in-hive-command-console"></a><span data-ttu-id="6638a-153">Inviare query Hive nella console dei comandi di Hive</span><span class="sxs-lookup"><span data-stu-id="6638a-153">Submit Hive queries in Hive command console.</span></span>
<span data-ttu-id="6638a-154">È possibile immettere anche prima console dei comandi Hive hello eseguendo comando `hive` nella riga di comando di Hadoop e quindi inviare le query Hive nel Hive console dei comandi.</span><span class="sxs-lookup"><span data-stu-id="6638a-154">You can also first enter hello Hive command console by running command `hive` in Hadoop Command Line, and then submit Hive queries in Hive command console.</span></span> <span data-ttu-id="6638a-155">Di seguito è fornito un esempio.</span><span class="sxs-lookup"><span data-stu-id="6638a-155">Here is an example.</span></span> <span data-ttu-id="6638a-156">In questo esempio hello due caselle rosse evidenziazione hello comandi utilizzati tooenter hello console dei comandi di Hive e hello query Hive inviato nella console di comando Hive, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="6638a-156">In this example, hello two red boxes highlight hello commands used tooenter hello Hive command console, and hello Hive query submitted in Hive command console, respectively.</span></span> <span data-ttu-id="6638a-157">casella Hello verde evidenzia l'output di hello dalla query Hive hello.</span><span class="sxs-lookup"><span data-stu-id="6638a-157">hello green box highlights hello output from hello Hive query.</span></span>

![Creare un'area di lavoro](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

<span data-ttu-id="6638a-159">Negli esempi precedenti Hello output direttamente risultati della query Hive hello sullo schermo.</span><span class="sxs-lookup"><span data-stu-id="6638a-159">hello previous examples directly output hello Hive query results on screen.</span></span> <span data-ttu-id="6638a-160">È anche possibile scrivere file locale tooa output di hello nel nodo head hello o tooan blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="6638a-160">You can also write hello output tooa local file on hello head node, or tooan Azure blob.</span></span> <span data-ttu-id="6638a-161">È quindi possibile utilizzare altri strumenti toofurther analizzare l'output di hello di query Hive.</span><span class="sxs-lookup"><span data-stu-id="6638a-161">Then, you can use other tools toofurther analyze hello output of Hive queries.</span></span>

<span data-ttu-id="6638a-162">**L'output di file locale tooa risultati query Hive.**</span><span class="sxs-lookup"><span data-stu-id="6638a-162">**Output Hive query results tooa local file.**</span></span>
<span data-ttu-id="6638a-163">toooutput Hive query risultati tooa directory locale nel nodo head hello, sono presenti query Hive di hello toosubmit hello Hadoop della riga di comando come segue:</span><span class="sxs-lookup"><span data-stu-id="6638a-163">toooutput Hive query results tooa local directory on hello head node, you have toosubmit hello Hive query in hello Hadoop Command Line as follows:</span></span>

    hive -e "<hive query>" > <local path in hello head node>

<span data-ttu-id="6638a-164">Nell'esempio seguente di hello, output di hello di query Hive viene scritto in un file `hivequeryoutput.txt` nella directory `C:\apps\temp`.</span><span class="sxs-lookup"><span data-stu-id="6638a-164">In hello following example, hello output of Hive query is written into a file `hivequeryoutput.txt` in directory `C:\apps\temp`.</span></span>

![Creare un'area di lavoro](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

<span data-ttu-id="6638a-166">**Tooan risultati di query Hive output blob di Azure**</span><span class="sxs-lookup"><span data-stu-id="6638a-166">**Output Hive query results tooan Azure blob**</span></span>

<span data-ttu-id="6638a-167">È anche possibile produrre tooan risultati di query Hive hello blob di Azure, all'interno del contenitore predefinito hello del cluster Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="6638a-167">You can also output hello Hive query results tooan Azure blob, within hello default container of hello Hadoop cluster.</span></span> <span data-ttu-id="6638a-168">query Hive Hello per questo è il seguente:</span><span class="sxs-lookup"><span data-stu-id="6638a-168">hello Hive query for this is as follows:</span></span>

    insert overwrite directory wasb:///<directory within hello default container> <select clause from ...>

<span data-ttu-id="6638a-169">Nell'esempio seguente di hello, output di hello di query Hive viene scritto directory blob tooa `queryoutputdir` all'interno del contenitore predefinito hello del cluster Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="6638a-169">In hello following example, hello output of Hive query is written tooa blob directory `queryoutputdir` within hello default container of hello Hadoop cluster.</span></span> <span data-ttu-id="6638a-170">In questo caso, è necessario solo nome di directory hello tooprovide, senza nome blob hello.</span><span class="sxs-lookup"><span data-stu-id="6638a-170">Here, you only need tooprovide hello directory name, without hello blob name.</span></span> <span data-ttu-id="6638a-171">Viene generato un errore se si specificano i nomi della directory e del BLOB, ad esempio `wasb:///queryoutputdir/queryoutput.txt`.</span><span class="sxs-lookup"><span data-stu-id="6638a-171">An error is thrown if you provide both directory and blob names, such as `wasb:///queryoutputdir/queryoutput.txt`.</span></span>

![Creare un'area di lavoro](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

<span data-ttu-id="6638a-173">Se si apre il contenitore predefinito hello del cluster Hadoop hello tramite Esplora archivi Azure, è possibile visualizzare l'output di hello della query Hive hello come illustrato nella seguente illustrazione hello.</span><span class="sxs-lookup"><span data-stu-id="6638a-173">If you open hello default container of hello Hadoop cluster using Azure Storage Explorer, you can see hello output of hello Hive query as shown in hello following figure.</span></span> <span data-ttu-id="6638a-174">È possibile applicare hello filtro (evidenziato in casella rossa) tooonly recuperare hello blob con le lettere nei nomi specificate.</span><span class="sxs-lookup"><span data-stu-id="6638a-174">You can apply hello filter (highlighted by red box) tooonly retrieve hello blob with specified letters in names.</span></span>

![Creare un'area di lavoro](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <span data-ttu-id="6638a-176"><a name="hive-editor"></a> 2. Inviare query Hive con hello Editor Hive</span><span class="sxs-lookup"><span data-stu-id="6638a-176"><a name="hive-editor"></a> 2. Submit Hive queries with hello Hive Editor</span></span>
<span data-ttu-id="6638a-177">È inoltre possibile utilizzare la Console di Query (Editor Hive) hello immettendo un URL di form hello *https://&#60; Nome del cluster Hadoop >.azurehdinsight.net/Home/HiveEditor* in un web browser.</span><span class="sxs-lookup"><span data-stu-id="6638a-177">You can also use hello Query Console (Hive Editor) by entering a URL of hello form *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* into a web browser.</span></span> <span data-ttu-id="6638a-178">È necessario essere registrati in hello vedere questa console e pertanto è necessario qui le credenziali del cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="6638a-178">You must be logged in hello see this console and so you need your Hadoop cluster credentials here.</span></span>

### <span data-ttu-id="6638a-179"><a name="ps"></a> 3. Inviare le query Hive con i comandi di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6638a-179"><a name="ps"></a> 3. Submit Hive queries with Azure PowerShell Commands</span></span>
<span data-ttu-id="6638a-180">È anche possibile utilizzare le query Hive toosubmit di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6638a-180">You can also use PowerShell toosubmit Hive queries.</span></span> <span data-ttu-id="6638a-181">Per istruzioni, vedere [Invio di processi Hive tramite PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6638a-181">For instructions, see [Submit Hive jobs using PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span></span>

## <span data-ttu-id="6638a-182"><a name="create-tables"></a>Creare il database e le tabelle Hive</span><span class="sxs-lookup"><span data-stu-id="6638a-182"><a name="create-tables"></a>Create Hive database and tables</span></span>
<span data-ttu-id="6638a-183">Hello query Hive vengono condivisi in hello [repository GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) e può essere scaricato da qui.</span><span class="sxs-lookup"><span data-stu-id="6638a-183">hello Hive queries are shared in hello [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) and can be downloaded from there.</span></span>

<span data-ttu-id="6638a-184">Ecco query Hive hello che crea una tabella Hive.</span><span class="sxs-lookup"><span data-stu-id="6638a-184">Here is hello Hive query that creates a Hive table.</span></span>

    create database if not exists <database name>;
    CREATE EXTERNAL TABLE if not exists <database name>.<table name>
    (
        field1 string,
        field2 int,
        field3 float,
        field4 double,
        ...,
        fieldN string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' lines terminated by '<line separator>'
    STORED AS TEXTFILE LOCATION '<storage location>' TBLPROPERTIES("skip.header.line.count"="1");

<span data-ttu-id="6638a-185">Ecco le descrizioni di hello dei campi hello tooplug in necessari e altre configurazioni:</span><span class="sxs-lookup"><span data-stu-id="6638a-185">Here are hello descriptions of hello fields that you need tooplug in and other configurations:</span></span>

* <span data-ttu-id="6638a-186">**&#60; nome database >**: nome hello del database di hello che si desidera toocreate.</span><span class="sxs-lookup"><span data-stu-id="6638a-186">**&#60;database name>**: hello name of hello database that you want toocreate.</span></span> <span data-ttu-id="6638a-187">Se si desidera database predefinito di hello toouse, hello query *creare database...*  può essere omesso.</span><span class="sxs-lookup"><span data-stu-id="6638a-187">If you just want toouse hello default database, hello query *create database...* can be omitted.</span></span>
* <span data-ttu-id="6638a-188">**&#60; nome tabella >**: nome hello della tabella di hello che si desidera toocreate all'interno del database specificato hello.</span><span class="sxs-lookup"><span data-stu-id="6638a-188">**&#60;table name>**: hello name of hello table that you want toocreate within hello specified database.</span></span> <span data-ttu-id="6638a-189">Se si desidera toouse hello predefinito database, tabella hello può fare riferimento direttamente *&#60; nome tabella >* senza &#60; nome database >.</span><span class="sxs-lookup"><span data-stu-id="6638a-189">If you want toouse hello default database, hello table can be directly referred by *&#60;table name>* without &#60;database name>.</span></span>
* <span data-ttu-id="6638a-190">**&#60; separatore di campo >**: separatore hello che delimita i campi in hello dati file toobe caricato tabella Hive toohello.</span><span class="sxs-lookup"><span data-stu-id="6638a-190">**&#60;field separator>**: hello separator that delimits fields in hello data file toobe uploaded toohello Hive table.</span></span>
* <span data-ttu-id="6638a-191">**&#60; il separatore di riga >**: separatore hello che delimita le righe nel file di dati hello.</span><span class="sxs-lookup"><span data-stu-id="6638a-191">**&#60;line separator>**: hello separator that delimits lines in hello data file.</span></span>
* <span data-ttu-id="6638a-192">**&#60; percorso di archiviazione >**: hello dati toosave hello percorso di archiviazione di Azure di tabelle Hive.</span><span class="sxs-lookup"><span data-stu-id="6638a-192">**&#60;storage location>**: hello Azure storage location toosave hello data of Hive tables.</span></span> <span data-ttu-id="6638a-193">Se non si specifica *posizione &#60; percorso di archiviazione >*, hello database e hello tabelle vengono archiviate in *hive/warehouse/* directory nel contenitore predefinito hello del cluster di Hive hello per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="6638a-193">If you do not specify *LOCATION &#60;storage location>*, hello database and hello tables are stored in *hive/warehouse/* directory in hello default container of hello Hive cluster by default.</span></span> <span data-ttu-id="6638a-194">Se si desidera una posizione di archiviazione hello toospecify, hello percorso di archiviazione toobe all'interno del contenitore predefinito hello per le tabelle e database hello.</span><span class="sxs-lookup"><span data-stu-id="6638a-194">If you want toospecify hello storage location, hello storage location has toobe within hello default container for hello database and tables.</span></span> <span data-ttu-id="6638a-195">Questa posizione è definito come contenitore predefinito di toohello relativo percorso di cluster hello in formato hello del toobe *' wasb: / / / &#60; directory 1 > /'* o *' wasb: / / / &#60; directory 1 > / &#60; Directory 2 > /'*e così via. Dopo l'esecuzione di query hello, le relative directory hello vengono create all'interno del contenitore predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="6638a-195">This location has toobe referred as location relative toohello default container of hello cluster in hello format of *'wasb:///&#60;directory 1>/'* or *'wasb:///&#60;directory 1>/&#60;directory 2>/'*, etc. After hello query is executed, hello relative directories are created within hello default container.</span></span>
* <span data-ttu-id="6638a-196">**TBLPROPERTIES("Skip.Header.Line.Count"="1")**: se il file di dati hello dispone di una riga di intestazione, questa proprietà è necessario tooadd **alla fine di hello** di hello *Crea tabella* query.</span><span class="sxs-lookup"><span data-stu-id="6638a-196">**TBLPROPERTIES("skip.header.line.count"="1")**: If hello data file has a header line, you have tooadd this property **at hello end** of hello *create table* query.</span></span> <span data-ttu-id="6638a-197">In caso contrario, la riga di intestazione hello viene caricata come una tabella di record toohello.</span><span class="sxs-lookup"><span data-stu-id="6638a-197">Otherwise, hello header line is loaded as a record toohello table.</span></span> <span data-ttu-id="6638a-198">Se il file di dati di hello non dispone di una riga di intestazione, questa configurazione può essere omesso nella query hello.</span><span class="sxs-lookup"><span data-stu-id="6638a-198">If hello data file does not have a header line, this configuration can be omitted in hello query.</span></span>

## <span data-ttu-id="6638a-199"><a name="load-data"></a>Caricare dati tooHive tabelle</span><span class="sxs-lookup"><span data-stu-id="6638a-199"><a name="load-data"></a>Load data tooHive tables</span></span>
<span data-ttu-id="6638a-200">Ecco query Hive hello che carica i dati in una tabella Hive.</span><span class="sxs-lookup"><span data-stu-id="6638a-200">Here is hello Hive query that loads data into a Hive table.</span></span>

    LOAD DATA INPATH '<path tooblob data>' INTO TABLE <database name>.<table name>;

* <span data-ttu-id="6638a-201">**&#60; i dati del percorso tooblob >**: hello se tabella Hive toohello di hello blob file toobe caricato nel contenitore predefinito hello di hello cluster HDInsight Hadoop, *&#60; i dati del percorso tooblob >* deve essere nel formato hello *' wasb: / / / &#60; directory in questo contenitore > / &#60; il nome di file blob >'*.</span><span class="sxs-lookup"><span data-stu-id="6638a-201">**&#60;path tooblob data>**: If hello blob file toobe uploaded toohello Hive table is in hello default container of hello HDInsight Hadoop cluster, hello *&#60;path tooblob data>* should be in hello format *'wasb:///&#60;directory in this container>/&#60;blob file name>'*.</span></span> <span data-ttu-id="6638a-202">file blob Hello può anche essere in un contenitore aggiuntivo del cluster HDInsight Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="6638a-202">hello blob file can also be in an additional container of hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="6638a-203">In questo caso, *&#60; i dati del percorso tooblob >* deve essere nel formato hello *' wasb: / / &#60; nome contenitore > @&#60; nome account di archiviazione >.blob.core.windows.net/ &#60; il nome di file blob >'*.</span><span class="sxs-lookup"><span data-stu-id="6638a-203">In this case, *&#60;path tooblob data>* should be in hello format *'wasb://&#60;container name>@&#60;storage account name>.blob.core.windows.net/&#60;blob file name>'*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="6638a-204">Hello blob caricato toobe tooHive tabella dati dispone di toobe predefinito hello o contenitori hello dell'account di archiviazione per cluster Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="6638a-204">hello blob data toobe uploaded tooHive table has toobe in hello default or additional container of hello storage account for hello Hadoop cluster.</span></span> <span data-ttu-id="6638a-205">In caso contrario, hello *Carica dati* query si verifica un errore che segnala che l'impossibilità di accedere dati hello.</span><span class="sxs-lookup"><span data-stu-id="6638a-205">Otherwise, hello *LOAD DATA* query fails complaining that it cannot access hello data.</span></span>
  >
  >

## <span data-ttu-id="6638a-206"><a name="partition-orc"></a>Argomenti avanzati: Tabella partizionata e archiviazione dei dati Hive in formato ORC</span><span class="sxs-lookup"><span data-stu-id="6638a-206"><a name="partition-orc"></a>Advanced topics: partitioned table and store Hive data in ORC format</span></span>
<span data-ttu-id="6638a-207">Se i dati di hello sono grandi, partizionamento tabella hello è utile per le query che richiedono solo tooscan alcune partizioni della tabella hello.</span><span class="sxs-lookup"><span data-stu-id="6638a-207">If hello data is large, partitioning hello table is beneficial for queries that only need tooscan a few partitions of hello table.</span></span> <span data-ttu-id="6638a-208">È ad esempio, dati del log hello toopartition ragionevole di un sito web per le date.</span><span class="sxs-lookup"><span data-stu-id="6638a-208">For instance, it is reasonable toopartition hello log data of a web site by dates.</span></span>

<span data-ttu-id="6638a-209">In aggiunta toopartitioning Hive tabelle, è inoltre utile toostore hello Hive dati di formato con ottimizzazione per la riga a colonne (ORC) hello.</span><span class="sxs-lookup"><span data-stu-id="6638a-209">In addition toopartitioning Hive tables, it is also beneficial toostore hello Hive data in hello Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="6638a-210">Per altre informazioni sulla formattazione ORC, vedere l’<a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">uso dei file ORC per migliorare le prestazioni quando Hive legge, scrive ed elabora dati</a>.</span><span class="sxs-lookup"><span data-stu-id="6638a-210">For more information on ORC formatting, see <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Using ORC files improves performance when Hive is reading, writing, and processing data</a>.</span></span>

### <a name="partitioned-table"></a><span data-ttu-id="6638a-211">Tabella partizionata</span><span class="sxs-lookup"><span data-stu-id="6638a-211">Partitioned table</span></span>
<span data-ttu-id="6638a-212">Ecco query Hive hello che crea una tabella partizionata e caricare i dati.</span><span class="sxs-lookup"><span data-stu-id="6638a-212">Here is hello Hive query that creates a partitioned table and loads data into it.</span></span>

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

<span data-ttu-id="6638a-213">Quando una query su tabelle partizionate, è consigliabile tooadd hello partizione condizione hello **inizio** di hello `where` clausola come ciò migliora l'efficacia hello di ricerca in modo significativo.</span><span class="sxs-lookup"><span data-stu-id="6638a-213">When querying partitioned tables, it is recommended tooadd hello partition condition in hello **beginning** of hello `where` clause as this improves hello efficacy of searching significantly.</span></span>

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <span data-ttu-id="6638a-214"><a name="orc"></a>Archiviare i dati Hive in formato ORC</span><span class="sxs-lookup"><span data-stu-id="6638a-214"><a name="orc"></a>Store Hive data in ORC format</span></span>
<span data-ttu-id="6638a-215">È possibile caricare direttamente dati dall'archiviazione blob in tabelle Hive archiviati in formato ORC hello.</span><span class="sxs-lookup"><span data-stu-id="6638a-215">You cannot directly load data from blob storage into Hive tables that is stored in hello ORC format.</span></span> <span data-ttu-id="6638a-216">Ecco i passaggi di hello che hello sono necessari dati tooload tootake da Azure BLOB tooHive tabelle archiviate in formato ORC.</span><span class="sxs-lookup"><span data-stu-id="6638a-216">Here are hello steps that hello you need tootake tooload data from Azure blobs tooHive tables stored in ORC format.</span></span>

<span data-ttu-id="6638a-217">Creare una tabella esterna **ARCHIVIATI file di testo AS** e caricare i dati dalla tabella toohello di archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="6638a-217">Create an external table **STORED AS TEXTFILE** and load data from blob storage toohello table.</span></span>

        CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<external textfile table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
            lines terminated by '<line separator>' STORED AS TEXTFILE
            LOCATION 'wasb:///<directory in Azure blob>' TBLPROPERTIES("skip.header.line.count"="1");

        LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<table name>;

<span data-ttu-id="6638a-218">Creare una tabella interna con hello stesso schema della tabella esterna hello nel passaggio 1, con hello stesso delimitatore di campo e archiviare hello Hive dati in formato ORC hello.</span><span class="sxs-lookup"><span data-stu-id="6638a-218">Create an internal table with hello same schema as hello external table in step 1, with hello same field delimiter, and store hello Hive data in hello ORC format.</span></span>

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

<span data-ttu-id="6638a-219">Selezionare i dati dalla tabella esterna di hello nel passaggio 1 e inserire nella tabella ORC hello</span><span class="sxs-lookup"><span data-stu-id="6638a-219">Select data from hello external table in step 1 and insert into hello ORC table</span></span>

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> <span data-ttu-id="6638a-220">Se nella tabella file di testo hello *&#60; nome database >. &#60; nome della tabella file di testo esterna >* contiene partizioni, nel passaggio 3, hello `SELECT * FROM <database name>.<external textfile table name>` comando Seleziona hello variabile partizione come un campo in hello restituiti set di dati.</span><span class="sxs-lookup"><span data-stu-id="6638a-220">If hello TEXTFILE table *&#60;database name>.&#60;external textfile table name>* has partitions, in STEP 3, hello `SELECT * FROM <database name>.<external textfile table name>` command selects hello partition variable as a field in hello returned data set.</span></span> <span data-ttu-id="6638a-221">Inserirlo nell'hello *&#60; nome database >. &#60; il nome di tabella ORC >* ha esito negativo poiché *&#60; nome database >. &#60; il nome di tabella ORC >* non dispone di una variabile di partizione hello come un campo nello schema di tabella hello.</span><span class="sxs-lookup"><span data-stu-id="6638a-221">Inserting it into hello *&#60;database name>.&#60;ORC table name>* fails since *&#60;database name>.&#60;ORC table name>* does not have hello partition variable as a field in hello table schema.</span></span> <span data-ttu-id="6638a-222">In questo caso, è necessario toospecifically hello selezionare campi toobe inserito troppo*&#60; nome database >. &#60; il nome di tabella ORC >* come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6638a-222">In this case, you need toospecifically select hello fields toobe inserted too*&#60;database name>.&#60;ORC table name>* as follows:</span></span>
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

<span data-ttu-id="6638a-223">È sicuro toodrop hello *&#60; nome della tabella file di testo esterna >* quando hello seguente query dopo che tutti i dati di utilizzo è stato inserito in *&#60; nome database >. &#60; il nome di tabella ORC >*:</span><span class="sxs-lookup"><span data-stu-id="6638a-223">It is safe toodrop hello *&#60;external textfile table name>* when using hello following query after all data has been inserted into *&#60;database name>.&#60;ORC table name>*:</span></span>

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

<span data-ttu-id="6638a-224">Dopo aver seguito questa procedura, è necessario utilizzare una tabella con dati in hello ORC formato pronto toouse.</span><span class="sxs-lookup"><span data-stu-id="6638a-224">After following this procedure, you should have a table with data in hello ORC format ready toouse.</span></span>  
