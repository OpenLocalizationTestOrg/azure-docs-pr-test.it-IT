---
title: Creare tabelle Hive e caricare i dati dall'archiviazione BLOB di Azure | Documentazione Microsoft
description: Creare tabelle Hive e caricare dati in BLOB nelle tabelle Hive
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
ms.openlocfilehash: eca4ecd8f639bb9816903f4b1d1f999755da819c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a><span data-ttu-id="9dea0-103">Creare tabelle Hive e caricare i dati dall'archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="9dea0-103">Create Hive tables and load data from Azure Blob Storage</span></span>
<span data-ttu-id="9dea0-104">Questo argomento presenta le query Hive generiche che consentono di creare tabelle Hive e di caricare i dati dall'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="9dea0-104">This topic presents generic Hive queries that create Hive tables and load data from Azure blob storage.</span></span> <span data-ttu-id="9dea0-105">Vengono inoltre fornite alcune linee guida sul partizionamento delle tabelle Hive e sull'uso della formattazione ORC per migliorare le prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="9dea0-105">Some guidance is also provided on partitioning Hive tables and on using the Optimized Row Columnar (ORC) formatting to improve query performance.</span></span>

<span data-ttu-id="9dea0-106">Questo **menu** si collega ad argomenti che descrivono come inserire dati in ambienti di destinazione in cui i dati possono essere archiviati ed elaborati durante il Processo di analisi scientifica dei dati per i team (TDSP).</span><span class="sxs-lookup"><span data-stu-id="9dea0-106">This **menu** links to topics that describe how to ingest data into target environments where the data can be stored and processed during the Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="9dea0-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9dea0-107">Prerequisites</span></span>
<span data-ttu-id="9dea0-108">Questo articolo presuppone che l'utente abbia:</span><span class="sxs-lookup"><span data-stu-id="9dea0-108">This article assumes that you have:</span></span>

* <span data-ttu-id="9dea0-109">Creato un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9dea0-109">Created an Azure storage account.</span></span> <span data-ttu-id="9dea0-110">Per istruzioni, vedere [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="9dea0-110">If you need instructions, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="9dea0-111">Eseguito il provisioning di un cluster Hadoop personalizzato con il servizio HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9dea0-111">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span>  <span data-ttu-id="9dea0-112">Per istruzioni, vedere [Personalizzazione di cluster Hadoop di Azure HDInsight per l'analisi scientifica dei dati](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="9dea0-112">If you need instructions, see [Customize Azure HDInsight Hadoop clusters for advanced analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="9dea0-113">Abilitato l'accesso remoto al cluster, eseguito l'accesso e aperto la console della riga di comando di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9dea0-113">Enabled remote access to the cluster, logged in, and opened the Hadoop Command-Line console.</span></span> <span data-ttu-id="9dea0-114">Per istruzioni, vedere [Accesso al nodo head del cluster Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="9dea0-114">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="9dea0-115">Caricare dati nell'archivio BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="9dea0-115">Upload data to Azure blob storage</span></span>
<span data-ttu-id="9dea0-116">Se è stata creata una macchina virtuale di Azure seguendo le istruzioni fornite nell'articolo [Configurare una macchina virtuale di Azure per l'analisi avanzata](machine-learning-data-science-setup-virtual-machine.md), questo file di script deve essere stato scaricato nella directory *C:\\Users\\\<nome utente name\>\\Documents\\Data Science Scripts* della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9dea0-116">If you created an Azure virtual machine by following the instructions provided in [Set up an Azure virtual machine for advanced analytics](machine-learning-data-science-setup-virtual-machine.md), this script file should have been downloaded to the *C:\\Users\\\<user name\>\\Documents\\Data Science Scripts* directory on the virtual machine.</span></span> <span data-ttu-id="9dea0-117">Affinché le query Hive siano pronte per l'invio, è necessario solo collegare il proprio schema dei dati e la configurazione dell'archiviazione BLOB di Azure ai campi appropriati.</span><span class="sxs-lookup"><span data-stu-id="9dea0-117">These Hive queries only require that you plug in your own data schema and Azure blob storage configuration in the appropriate fields to be ready for submission.</span></span>

<span data-ttu-id="9dea0-118">Si supponga che i dati delle tabelle Hive siano in un formato tabulare **non compresso** e che i dati siano stati caricati nel contenitore predefinito (o in uno aggiuntivo) dell'account di archiviazione usato dal cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9dea0-118">We assume that the data for Hive tables is in an **uncompressed** tabular format, and that the data has been uploaded to the default (or to an additional) container of the storage account used by the Hadoop cluster.</span></span>

<span data-ttu-id="9dea0-119">Se si desidera far pratica con i **dati relativi alle corse dei Taxi di NYC**, è necessario:</span><span class="sxs-lookup"><span data-stu-id="9dea0-119">If you want to practice on the **NYC Taxi Trip Data**, you need to:</span></span>

* <span data-ttu-id="9dea0-120">**scaricare** i 24 file di [dati elativi alle corse dei Taxi di NYC](http://www.andresmh.com/nyctaxitrips) (12 file relativi alle corse e 12 file delle tariffe);</span><span class="sxs-lookup"><span data-stu-id="9dea0-120">**download** the 24 [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) files (12 Trip files and 12 Fare files),</span></span>
* <span data-ttu-id="9dea0-121">**decomprimere** tutti i file in file con estensione .csv;</span><span class="sxs-lookup"><span data-stu-id="9dea0-121">**unzip** all files into .csv files, and then</span></span>
* <span data-ttu-id="9dea0-122">**caricare** i file nel percorso predefinito (o nel contenitore appropriato) dell'account di archiviazione di Azure creato mediante la procedura descritta nell'argomento [Personalizzare i cluster Hadoop di Azure HDInsight per Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md) .</span><span class="sxs-lookup"><span data-stu-id="9dea0-122">**upload** them to the default (or appropriate container) of the Azure storage account that was created by the procedure outlined in the [Customize Azure HDInsight Hadoop clusters for Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md) topic.</span></span> <span data-ttu-id="9dea0-123">Il processo per caricare i file con estensione csv per il contenitore predefinito nell'account di archiviazione sono disponibili in questa [pagina](machine-learning-data-science-process-hive-walkthrough.md#upload).</span><span class="sxs-lookup"><span data-stu-id="9dea0-123">The process to upload the .csv files to the default container on the storage account can be found on this [page](machine-learning-data-science-process-hive-walkthrough.md#upload).</span></span>

## <span data-ttu-id="9dea0-124"><a name="submit"></a>Come inviare query Hive</span><span class="sxs-lookup"><span data-stu-id="9dea0-124"><a name="submit"></a>How to submit Hive queries</span></span>
<span data-ttu-id="9dea0-125">È possibile inviare query Hive mediante:</span><span class="sxs-lookup"><span data-stu-id="9dea0-125">Hive queries can be submitted by using:</span></span>

1. [<span data-ttu-id="9dea0-126">Inviare le query Hive attraverso la riga di comando di Hadoop nel nodo head del cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="9dea0-126">Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>](#headnode)
2. [<span data-ttu-id="9dea0-127">Inviare le query Hive con l'editor Hive</span><span class="sxs-lookup"><span data-stu-id="9dea0-127">Submit Hive queries with the Hive Editor</span></span>](#hive-editor)
3. [<span data-ttu-id="9dea0-128">Inviare le query Hive con i comandi di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9dea0-128">Submit Hive queries with Azure PowerShell Commands</span></span>](#ps)

<span data-ttu-id="9dea0-129">Le query Hive sono simili a SQL.</span><span class="sxs-lookup"><span data-stu-id="9dea0-129">Hive queries are SQL-like.</span></span> <span data-ttu-id="9dea0-130">Se si ha già familiarità con SQL, i [fogli informativi per gli utenti di Hive](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) possono rivelarsi utili.</span><span class="sxs-lookup"><span data-stu-id="9dea0-130">If you are familiar with SQL, you may find the [Hive for SQL Users Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) useful.</span></span>

<span data-ttu-id="9dea0-131">Quando si invia una query Hive, è possibile controllare la destinazione dell'output, sia questo visualizzato sullo schermo o incluso in un file locale nel nodo head o in un BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="9dea0-131">When submitting a Hive query, you can also control the destination of the output from Hive queries, whether it be on the screen or to a local file on the head node or to an Azure blob.</span></span>

### <span data-ttu-id="9dea0-132"><a name="headnode"></a> 1. Inviare le query Hive attraverso la riga di comando di Hadoop nel nodo head del cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="9dea0-132"><a name="headnode"></a> 1. Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>
<span data-ttu-id="9dea0-133">Se la query Hive è complessa e la si invia direttamente al nodo head del cluster Hadoop, il completamento dell'operazione sarà più rapido rispetto a quando l'invio viene effettuato con l'editor Hive o gli script di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9dea0-133">If the Hive query is complex, submitting it directly in the head node of the Hadoop cluster typically leads to faster turn around than submitting it with a Hive Editor or Azure PowerShell scripts.</span></span>

<span data-ttu-id="9dea0-134">Accedere al nodo head del cluster Hadoop, aprire la riga di comando di Hadoop sul desktop del nodo head e immettere il comando `cd %hive_home%\bin`.</span><span class="sxs-lookup"><span data-stu-id="9dea0-134">Log in to the head node of the Hadoop cluster, open the Hadoop Command Line on the desktop of the head node, and enter command `cd %hive_home%\bin`.</span></span>

<span data-ttu-id="9dea0-135">Esistono tre modi per inviare query Hive nella riga di comando di Hadoop:</span><span class="sxs-lookup"><span data-stu-id="9dea0-135">You have three ways to submit Hive queries in the Hadoop Command Line:</span></span>

* <span data-ttu-id="9dea0-136">Direttamente</span><span class="sxs-lookup"><span data-stu-id="9dea0-136">directly</span></span>
* <span data-ttu-id="9dea0-137">Mediante i file con estensione hql</span><span class="sxs-lookup"><span data-stu-id="9dea0-137">using .hql files</span></span>
* <span data-ttu-id="9dea0-138">Con la console dei comandi di Hive</span><span class="sxs-lookup"><span data-stu-id="9dea0-138">with the Hive command console</span></span>

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a><span data-ttu-id="9dea0-139">Inviare query Hive direttamente nella riga di comando di Hadoop</span><span class="sxs-lookup"><span data-stu-id="9dea0-139">Submit Hive queries directly in Hadoop Command Line.</span></span>
<span data-ttu-id="9dea0-140">È possibile eseguire comandi come `hive -e "<your hive query>;` per inviare query Hive semplici direttamente nella riga di comando di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9dea0-140">You can run command like `hive -e "<your hive query>;` to submit simple Hive queries directly in Hadoop Command Line.</span></span> <span data-ttu-id="9dea0-141">In questo esempio, la casella rossa evidenzia il comando che consente di inviare la query Hive, mentre quella verde evidenzia l'output della query.</span><span class="sxs-lookup"><span data-stu-id="9dea0-141">Here is an example, where the red box outlines the command that submits the Hive query, and the green box outlines the output from the Hive query.</span></span>

![Creare un'area di lavoro](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a><span data-ttu-id="9dea0-143">Inviare query nei file con estensione hql</span><span class="sxs-lookup"><span data-stu-id="9dea0-143">Submit Hive queries in .hql files</span></span>
<span data-ttu-id="9dea0-144">Quando la query Hive è più complicata e presenta più righe, modificare le query nella riga di comando o nella console dei comandi di Hive non è pratico.</span><span class="sxs-lookup"><span data-stu-id="9dea0-144">When the Hive query is more complicated and has multiple lines, editing queries in command line or Hive command console is not practical.</span></span> <span data-ttu-id="9dea0-145">Un'alternativa consiste nell'usare un editor di testo nel nodo head del cluster Hadoop per salvare le query Hive in un file con estensione hql in una directory locale del nodo head.</span><span class="sxs-lookup"><span data-stu-id="9dea0-145">An alternative is to use a text editor in the head node of the Hadoop cluster to save the Hive queries in a .hql file in a local directory of the head node.</span></span> <span data-ttu-id="9dea0-146">Quindi la query Hive nel file con estensione hql può essere inviata usando l'argomento `-f` nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="9dea0-146">Then the Hive query in the .hql file can be submitted by using the `-f` argument as follows:</span></span>

    hive -f "<path to the .hql file>"

![Creare un'area di lavoro](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

<span data-ttu-id="9dea0-148">**Eliminare la visualizzazione relativa allo stato di avanzamento delle query Hive sullo schermo**</span><span class="sxs-lookup"><span data-stu-id="9dea0-148">**Suppress progress status screen print of Hive queries**</span></span>

<span data-ttu-id="9dea0-149">Per impostazione predefinita, dopo l'invio della query Hive nella riga di comando di Hadoop, lo stato di avanzamento del processo di mapping e riduzione viene mostrato sullo schermo.</span><span class="sxs-lookup"><span data-stu-id="9dea0-149">By default, after Hive query is submitted in Hadoop Command Line, the progress of the Map/Reduce job is printed out on screen.</span></span> <span data-ttu-id="9dea0-150">Per eliminare la stampa della schermata di avanzamento del processo di mapping e riduzione, è possibile usare un argomento `-S` ("S" in lettere maiuscole) nella riga di comando nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="9dea0-150">To suppress the screen print of the Map/Reduce job progress, you can use an argument `-S` ("S" in upper case) in the command line as follows:</span></span>

    hive -S -f "<path to the .hql file>"
<span data-ttu-id="9dea0-151">.</span><span class="sxs-lookup"><span data-stu-id="9dea0-151">.</span></span>    <span data-ttu-id="9dea0-152">hive -S -e "<Hive queries>"</span><span class="sxs-lookup"><span data-stu-id="9dea0-152">hive -S -e "<Hive queries>"</span></span>

#### <a name="submit-hive-queries-in-hive-command-console"></a><span data-ttu-id="9dea0-153">Inviare query Hive nella console dei comandi di Hive</span><span class="sxs-lookup"><span data-stu-id="9dea0-153">Submit Hive queries in Hive command console.</span></span>
<span data-ttu-id="9dea0-154">Innanzitutto è possibile immettere la console dei comandi di Hive eseguendo il comando `hive` nella riga di comando di Hadoop, quindi inviare query Hive nella console dei comandi di Hive.</span><span class="sxs-lookup"><span data-stu-id="9dea0-154">You can also first enter the Hive command console by running command `hive` in Hadoop Command Line, and then submit Hive queries in Hive command console.</span></span> <span data-ttu-id="9dea0-155">Di seguito è fornito un esempio.</span><span class="sxs-lookup"><span data-stu-id="9dea0-155">Here is an example.</span></span> <span data-ttu-id="9dea0-156">In questo esempio, le due caselle rosse evidenziano i comandi usati per inserire la console dei comandi di Hive e la query Hive inviata nella console dei comandi.</span><span class="sxs-lookup"><span data-stu-id="9dea0-156">In this example, the two red boxes highlight the commands used to enter the Hive command console, and the Hive query submitted in Hive command console, respectively.</span></span> <span data-ttu-id="9dea0-157">La casella verde evidenzia l'output dalla query Hive.</span><span class="sxs-lookup"><span data-stu-id="9dea0-157">The green box highlights the output from the Hive query.</span></span>

![Creare un'area di lavoro](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

<span data-ttu-id="9dea0-159">Negli esempi precedenti, i risultati della query Hive vengono visualizzati direttamente sullo schermo.</span><span class="sxs-lookup"><span data-stu-id="9dea0-159">The previous examples directly output the Hive query results on screen.</span></span> <span data-ttu-id="9dea0-160">È anche possibile salvare l'output su un file locale nel nodo head o in un BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="9dea0-160">You can also write the output to a local file on the head node, or to an Azure blob.</span></span> <span data-ttu-id="9dea0-161">Quindi, è possibile usare altri strumenti per analizzare ulteriormente l'output delle query Hive.</span><span class="sxs-lookup"><span data-stu-id="9dea0-161">Then, you can use other tools to further analyze the output of Hive queries.</span></span>

<span data-ttu-id="9dea0-162">**Restituire i risultati delle query Hive in un file locale.**</span><span class="sxs-lookup"><span data-stu-id="9dea0-162">**Output Hive query results to a local file.**</span></span>
<span data-ttu-id="9dea0-163">Per restituire i risultati delle query Hive in una directory locale nel nodo head, si deve inviare la query Hive nella riga di comando di Hadoop come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9dea0-163">To output Hive query results to a local directory on the head node, you have to submit the Hive query in the Hadoop Command Line as follows:</span></span>

    hive -e "<hive query>" > <local path in the head node>

<span data-ttu-id="9dea0-164">Nell'esempio seguente, l'output della query Hive viene scritto in un file `hivequeryoutput.txt` all'interno della directory `C:\apps\temp`.</span><span class="sxs-lookup"><span data-stu-id="9dea0-164">In the following example, the output of Hive query is written into a file `hivequeryoutput.txt` in directory `C:\apps\temp`.</span></span>

![Creare un'area di lavoro](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

<span data-ttu-id="9dea0-166">**Restituire i risultati delle query Hive in un BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="9dea0-166">**Output Hive query results to an Azure blob**</span></span>

<span data-ttu-id="9dea0-167">Si può anche restituire i risultati della query Hive in un BLOB di Azure, nel contenitore predefinito del cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9dea0-167">You can also output the Hive query results to an Azure blob, within the default container of the Hadoop cluster.</span></span> <span data-ttu-id="9dea0-168">In questo caso la query Hive del client è la seguente:</span><span class="sxs-lookup"><span data-stu-id="9dea0-168">The Hive query for this is as follows:</span></span>

    insert overwrite directory wasb:///<directory within the default container> <select clause from ...>

<span data-ttu-id="9dea0-169">Nell'esempio seguente, l'output della query Hive viene scritto in una directory del BLOB `queryoutputdir` nel contenitore predefinito del cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9dea0-169">In the following example, the output of Hive query is written to a blob directory `queryoutputdir` within the default container of the Hadoop cluster.</span></span> <span data-ttu-id="9dea0-170">In questo caso, è sufficiente fornire il nome della directory, senza il nome del BLOB.</span><span class="sxs-lookup"><span data-stu-id="9dea0-170">Here, you only need to provide the directory name, without the blob name.</span></span> <span data-ttu-id="9dea0-171">Viene generato un errore se si specificano i nomi della directory e del BLOB, ad esempio `wasb:///queryoutputdir/queryoutput.txt`.</span><span class="sxs-lookup"><span data-stu-id="9dea0-171">An error is thrown if you provide both directory and blob names, such as `wasb:///queryoutputdir/queryoutput.txt`.</span></span>

![Creare un'area di lavoro](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

<span data-ttu-id="9dea0-173">Se si apre il contenitore predefinito del cluster Hadoop usando Esplora archivi di Azure, è possibile visualizzare l'output della query Hive come indicato nell'immagine di seguito.</span><span class="sxs-lookup"><span data-stu-id="9dea0-173">If you open the default container of the Hadoop cluster using Azure Storage Explorer, you can see the output of the Hive query as shown in the following figure.</span></span> <span data-ttu-id="9dea0-174">È possibile applicare il filtro (evidenziato da una casella rossa) per recuperare solo il BLOB con le lettere specificate nei nomi.</span><span class="sxs-lookup"><span data-stu-id="9dea0-174">You can apply the filter (highlighted by red box) to only retrieve the blob with specified letters in names.</span></span>

![Creare un'area di lavoro](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <span data-ttu-id="9dea0-176"><a name="hive-editor"></a> 2. Inviare le query Hive con l'editor Hive</span><span class="sxs-lookup"><span data-stu-id="9dea0-176"><a name="hive-editor"></a> 2. Submit Hive queries with the Hive Editor</span></span>
<span data-ttu-id="9dea0-177">È inoltre possibile usare la Console di Query (Editor Hive) immettendo un URL con formato *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* in un Web browser.</span><span class="sxs-lookup"><span data-stu-id="9dea0-177">You can also use the Query Console (Hive Editor) by entering a URL of the form *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* into a web browser.</span></span> <span data-ttu-id="9dea0-178">La console è visualizzabile solo dopo aver eseguito l'accesso, pertanto è necessario disporre delle proprie credenziali del cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9dea0-178">You must be logged in the see this console and so you need your Hadoop cluster credentials here.</span></span>

### <span data-ttu-id="9dea0-179"><a name="ps"></a> 3. Inviare le query Hive con i comandi di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9dea0-179"><a name="ps"></a> 3. Submit Hive queries with Azure PowerShell Commands</span></span>
<span data-ttu-id="9dea0-180">È possibile usare anche PowerShell per inviare le query Hive.</span><span class="sxs-lookup"><span data-stu-id="9dea0-180">You can also use PowerShell to submit Hive queries.</span></span> <span data-ttu-id="9dea0-181">Per istruzioni, vedere [Invio di processi Hive tramite PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9dea0-181">For instructions, see [Submit Hive jobs using PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span></span>

## <span data-ttu-id="9dea0-182"><a name="create-tables"></a>Creare il database e le tabelle Hive</span><span class="sxs-lookup"><span data-stu-id="9dea0-182"><a name="create-tables"></a>Create Hive database and tables</span></span>
<span data-ttu-id="9dea0-183">Le query Hive vengono condivise nell'[archivio GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) e possono essere scaricate da questa posizione.</span><span class="sxs-lookup"><span data-stu-id="9dea0-183">The Hive queries are shared in the [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) and can be downloaded from there.</span></span>

<span data-ttu-id="9dea0-184">Di seguito è presentata la query Hive che crea una tabella Hive.</span><span class="sxs-lookup"><span data-stu-id="9dea0-184">Here is the Hive query that creates a Hive table.</span></span>

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

<span data-ttu-id="9dea0-185">Di seguito sono presentate le descrizioni dei campi da collegare e altre configurazioni:</span><span class="sxs-lookup"><span data-stu-id="9dea0-185">Here are the descriptions of the fields that you need to plug in and other configurations:</span></span>

* <span data-ttu-id="9dea0-186">**&#60;database name>**: il nome del database che si desidera creare.</span><span class="sxs-lookup"><span data-stu-id="9dea0-186">**&#60;database name>**: the name of the database that you want to create.</span></span> <span data-ttu-id="9dea0-187">Se si desidera usare solo il database predefinito, la query di *creazione del database* può essere omessa.</span><span class="sxs-lookup"><span data-stu-id="9dea0-187">If you just want to use the default database, the query *create database...* can be omitted.</span></span>
* <span data-ttu-id="9dea0-188">**&#60;table name>**: il nome della tabella che si desidera creare nel database specificato.</span><span class="sxs-lookup"><span data-stu-id="9dea0-188">**&#60;table name>**: the name of the table that you want to create within the specified database.</span></span> <span data-ttu-id="9dea0-189">Se si desidera usare il database predefinito, è possibile fare direttamente riferimento alla tabella da *&#60;table name>* senza &#60;database name>.</span><span class="sxs-lookup"><span data-stu-id="9dea0-189">If you want to use the default database, the table can be directly referred by *&#60;table name>* without &#60;database name>.</span></span>
* <span data-ttu-id="9dea0-190">**&#60;field separator>**: il separatore che delimita i campi nel file di dati da caricare nella tabella Hive.</span><span class="sxs-lookup"><span data-stu-id="9dea0-190">**&#60;field separator>**: the separator that delimits fields in the data file to be uploaded to the Hive table.</span></span>
* <span data-ttu-id="9dea0-191">**&#60;line separator>**: il separatore che delimita le righe nel file di dati.</span><span class="sxs-lookup"><span data-stu-id="9dea0-191">**&#60;line separator>**: the separator that delimits lines in the data file.</span></span>
* <span data-ttu-id="9dea0-192">**&#60;storage location>**: il percorso di archiviazione di Azure in cui salvare i dati delle tabelle Hive.</span><span class="sxs-lookup"><span data-stu-id="9dea0-192">**&#60;storage location>**: the Azure storage location to save the data of Hive tables.</span></span> <span data-ttu-id="9dea0-193">Se il parametro *LOCATION &#60;storage location>* non viene specificato, il database e le tabelle vengono archiviati per impostazione predefinita nella directory *hive/warehouse/* nel contenitore predefinito del cluster Hive.</span><span class="sxs-lookup"><span data-stu-id="9dea0-193">If you do not specify *LOCATION &#60;storage location>*, the database and the tables are stored in *hive/warehouse/* directory in the default container of the Hive cluster by default.</span></span> <span data-ttu-id="9dea0-194">Se si desidera specificare il percorso di archiviazione, questo deve trovarsi nel contenitore predefinito per database e tabelle.</span><span class="sxs-lookup"><span data-stu-id="9dea0-194">If you want to specify the storage location, the storage location has to be within the default container for the database and tables.</span></span> <span data-ttu-id="9dea0-195">Questo percorso deve essere definito come percorso relativo per il contenitore predefinito del cluster nel formato*'wasb:///&#60;directory 1>/'* o *'wasb:///&#60;directory 1>/&#60;directory 2>/'* e così via. Dopo l'esecuzione della query, vengono create le relative directory nel contenitore predefinito.</span><span class="sxs-lookup"><span data-stu-id="9dea0-195">This location has to be referred as location relative to the default container of the cluster in the format of *'wasb:///&#60;directory 1>/'* or *'wasb:///&#60;directory 1>/&#60;directory 2>/'*, etc. After the query is executed, the relative directories are created within the default container.</span></span>
* <span data-ttu-id="9dea0-196">**TBLPROPERTIES("skip.header.line.count"="1")**: se il file di dati presenta una riga di intestazione, si deve aggiungere questa proprietà **alla fine** della query di *creazione della tabella*.</span><span class="sxs-lookup"><span data-stu-id="9dea0-196">**TBLPROPERTIES("skip.header.line.count"="1")**: If the data file has a header line, you have to add this property **at the end** of the *create table* query.</span></span> <span data-ttu-id="9dea0-197">In caso contrario, la riga di intestazione verrà caricata come un record nella tabella.</span><span class="sxs-lookup"><span data-stu-id="9dea0-197">Otherwise, the header line is loaded as a record to the table.</span></span> <span data-ttu-id="9dea0-198">Se il file di dati non presenta una riga di intestazione, questa configurazione può essere omessa nella query.</span><span class="sxs-lookup"><span data-stu-id="9dea0-198">If the data file does not have a header line, this configuration can be omitted in the query.</span></span>

## <span data-ttu-id="9dea0-199"><a name="load-data"></a>Caricare dati nelle tabelle Hive</span><span class="sxs-lookup"><span data-stu-id="9dea0-199"><a name="load-data"></a>Load data to Hive tables</span></span>
<span data-ttu-id="9dea0-200">Di seguito è presentata la query Hive che carica i dati in una tabella Hive.</span><span class="sxs-lookup"><span data-stu-id="9dea0-200">Here is the Hive query that loads data into a Hive table.</span></span>

    LOAD DATA INPATH '<path to blob data>' INTO TABLE <database name>.<table name>;

* <span data-ttu-id="9dea0-201">**&#60;path to blob data>**: se il file BLOB da caricare nella tabella Hive si trova nel contenitore predefinito del cluster Hadoop di HDInsight, *&#60;path to blob data>* deve essere nel formato *'wasb:///&#60;directory in this container>/&#60;blob file name>'*.</span><span class="sxs-lookup"><span data-stu-id="9dea0-201">**&#60;path to blob data>**: If the blob file to be uploaded to the Hive table is in the default container of the HDInsight Hadoop cluster, the *&#60;path to blob data>* should be in the format *'wasb:///&#60;directory in this container>/&#60;blob file name>'*.</span></span> <span data-ttu-id="9dea0-202">Il file BLOB può trovarsi inoltre in un contenitore aggiuntivo del cluster Hadoop di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9dea0-202">The blob file can also be in an additional container of the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="9dea0-203">In questo caso, *&#60;path to blob data>* deve essere nel formato *'wasb://&#60;container name>@&#60;storage account name>.blob.core.windows.net/&#60;blob file name>'*.</span><span class="sxs-lookup"><span data-stu-id="9dea0-203">In this case, *&#60;path to blob data>* should be in the format *'wasb://&#60;container name>@&#60;storage account name>.blob.core.windows.net/&#60;blob file name>'*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9dea0-204">I dati BLOB da caricare nella tabella Hive devono trovarsi nel contenitore predefinito o aggiuntivo dell'account di archiviazione del cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9dea0-204">The blob data to be uploaded to Hive table has to be in the default or additional container of the storage account for the Hadoop cluster.</span></span> <span data-ttu-id="9dea0-205">In caso contrario, la query di *LOAD DATA* avrà esito negativo perché non può accedere ai dati.</span><span class="sxs-lookup"><span data-stu-id="9dea0-205">Otherwise, the *LOAD DATA* query fails complaining that it cannot access the data.</span></span>
  >
  >

## <span data-ttu-id="9dea0-206"><a name="partition-orc"></a>Argomenti avanzati: Tabella partizionata e archiviazione dei dati Hive in formato ORC</span><span class="sxs-lookup"><span data-stu-id="9dea0-206"><a name="partition-orc"></a>Advanced topics: partitioned table and store Hive data in ORC format</span></span>
<span data-ttu-id="9dea0-207">Se i dati sono di grandi dimensioni, il partizionamento della tabella è utile per le query che devono solo eseguire l'analisi di alcune partizioni della tabella.</span><span class="sxs-lookup"><span data-stu-id="9dea0-207">If the data is large, partitioning the table is beneficial for queries that only need to scan a few partitions of the table.</span></span> <span data-ttu-id="9dea0-208">Ad esempio, è ragionevole partizionare i dati di log di un sito Web per date.</span><span class="sxs-lookup"><span data-stu-id="9dea0-208">For instance, it is reasonable to partition the log data of a web site by dates.</span></span>

<span data-ttu-id="9dea0-209">Oltre al partizionamento delle tabelle Hive, è inoltre utile archiviare i dati Hive in formato ORC.</span><span class="sxs-lookup"><span data-stu-id="9dea0-209">In addition to partitioning Hive tables, it is also beneficial to store the Hive data in the Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="9dea0-210">Per altre informazioni sulla formattazione ORC, vedere l’<a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">uso dei file ORC per migliorare le prestazioni quando Hive legge, scrive ed elabora dati</a>.</span><span class="sxs-lookup"><span data-stu-id="9dea0-210">For more information on ORC formatting, see <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Using ORC files improves performance when Hive is reading, writing, and processing data</a>.</span></span>

### <a name="partitioned-table"></a><span data-ttu-id="9dea0-211">Tabella partizionata</span><span class="sxs-lookup"><span data-stu-id="9dea0-211">Partitioned table</span></span>
<span data-ttu-id="9dea0-212">Di seguito è presentata la query Hive che crea una tabella partizionata e vi carica i dati.</span><span class="sxs-lookup"><span data-stu-id="9dea0-212">Here is the Hive query that creates a partitioned table and loads data into it.</span></span>

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path to the source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

<span data-ttu-id="9dea0-213">Quando si interrogano tabelle partizionate, è opportuno aggiungere la condizione di partizione all'**inizio** della clausola `where` in modo da migliorare sensibilmente l'efficacia della ricerca.</span><span class="sxs-lookup"><span data-stu-id="9dea0-213">When querying partitioned tables, it is recommended to add the partition condition in the **beginning** of the `where` clause as this improves the efficacy of searching significantly.</span></span>

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <span data-ttu-id="9dea0-214"><a name="orc"></a>Archiviare i dati Hive in formato ORC</span><span class="sxs-lookup"><span data-stu-id="9dea0-214"><a name="orc"></a>Store Hive data in ORC format</span></span>
<span data-ttu-id="9dea0-215">Non è possibile caricare direttamente i dati del BLOB nelle tabelle Hive nel formato di archiviazione ORC.</span><span class="sxs-lookup"><span data-stu-id="9dea0-215">You cannot directly load data from blob storage into Hive tables that is stored in the ORC format.</span></span> <span data-ttu-id="9dea0-216">Di seguito sono presentati i passaggi da eseguire per caricare dati dai BLOB Azure nelle tabelle Hive archiviate in formato ORC.</span><span class="sxs-lookup"><span data-stu-id="9dea0-216">Here are the steps that the you need to take to load data from Azure blobs to Hive tables stored in ORC format.</span></span>

<span data-ttu-id="9dea0-217">Creare una tabella esterna **ARCHIVIATA COME TEXTFILE** e caricare i dati dall'archiviazione BLOB nella tabella.</span><span class="sxs-lookup"><span data-stu-id="9dea0-217">Create an external table **STORED AS TEXTFILE** and load data from blob storage to the table.</span></span>

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

        LOAD DATA INPATH '<path to the source file>' INTO TABLE <database name>.<table name>;

<span data-ttu-id="9dea0-218">Creare una tabella interna con lo stesso schema della tabella esterna nel passaggio 1, lo stesso delimitatore dei campi e archiviare i dati Hive in formato ORC.</span><span class="sxs-lookup"><span data-stu-id="9dea0-218">Create an internal table with the same schema as the external table in step 1, with the same field delimiter, and store the Hive data in the ORC format.</span></span>

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

<span data-ttu-id="9dea0-219">Selezionare i dati della tabella esterna nel passaggio 1 e inserirli nella tabella ORC.</span><span class="sxs-lookup"><span data-stu-id="9dea0-219">Select data from the external table in step 1 and insert into the ORC table</span></span>

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> <span data-ttu-id="9dea0-220">Se la tabella TEXTFILE *&#60;database name>.&#60;external textfile table name>* presenta partizioni, al PASSAGGIO 3, il comando `SELECT * FROM <database name>.<external textfile table name>` selezionerà la variabile della partizione come un campo nel set di dati restituito.</span><span class="sxs-lookup"><span data-stu-id="9dea0-220">If the TEXTFILE table *&#60;database name>.&#60;external textfile table name>* has partitions, in STEP 3, the `SELECT * FROM <database name>.<external textfile table name>` command selects the partition variable as a field in the returned data set.</span></span> <span data-ttu-id="9dea0-221">L'inserimento di tale tabella in *&#60;database name>.&#60;ORC table name>* avrà esito negativo poiché *&#60;database name>.&#60;ORC table name>* non dispone della variabile della partizione come campo nello schema della tabella.</span><span class="sxs-lookup"><span data-stu-id="9dea0-221">Inserting it into the *&#60;database name>.&#60;ORC table name>* fails since *&#60;database name>.&#60;ORC table name>* does not have the partition variable as a field in the table schema.</span></span> <span data-ttu-id="9dea0-222">In questo caso, si devono selezionare i campi da inserire in *&#60;database name>.&#60;ORC table name>* come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9dea0-222">In this case, you need to specifically select the fields to be inserted to *&#60;database name>.&#60;ORC table name>* as follows:</span></span>
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

<span data-ttu-id="9dea0-223">È opportuno eliminare *&#60;external textfile table name>* quando si usa la query seguente dopo che tutti i dati sono stati inseriti in *&#60;database name>.&#60;ORC table name>*:</span><span class="sxs-lookup"><span data-stu-id="9dea0-223">It is safe to drop the *&#60;external textfile table name>* when using the following query after all data has been inserted into *&#60;database name>.&#60;ORC table name>*:</span></span>

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

<span data-ttu-id="9dea0-224">Al termine della procedura, si disporrà di una tabella con i dati nel formato ORC pronta per l'uso.</span><span class="sxs-lookup"><span data-stu-id="9dea0-224">After following this procedure, you should have a table with data in the ORC format ready to use.</span></span>  
