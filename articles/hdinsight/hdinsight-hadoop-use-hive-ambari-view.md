---
title: Usare le visualizzazioni di Ambari per l'uso di Hive in HDInsight (Hadoop) - Azure | Documentazione Microsoft
description: Informazioni su come usare la visualizzazione Hive dal Web browser per inviare query Hive. La visualizzazione Hive fa parte delle visualizzazioni di Ambari fornite con il cluster HDInsight basato su Linux.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1abe9104-f4b2-41b9-9161-abbc43de8294
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 80df3da4d62feb814ea2dd97c96e57954093c5c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-hive-view-with-hadoop-in-hdinsight"></a><span data-ttu-id="2ea0f-104">Usare la visualizzazione Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="2ea0f-104">Use the Hive View with Hadoop in HDInsight</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="2ea0f-105">Informazioni su come eseguire query Hive usando la vista Hive di Ambari.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-105">Learn how to run Hive queries using Ambari Hive View.</span></span> <span data-ttu-id="2ea0f-106">Ambari è un'utilità per la gestione e il monitoraggio fornita con i cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-106">Ambari is a management and monitoring utility provided with Linux-based HDInsight clusters.</span></span> <span data-ttu-id="2ea0f-107">Una delle funzionalità fornite da Ambari è un'interfaccia utente Web che può essere usata per eseguire query Hive.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-107">One of the features provided through Ambari is a Web UI that can be used to run Hive queries.</span></span>

> [!NOTE]
> <span data-ttu-id="2ea0f-108">Ambari include numerose funzionalità non illustrate in questo documento.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-108">Ambari has many capabilities that are not discussed in this document.</span></span> <span data-ttu-id="2ea0f-109">Per altre informazioni, vedere [Gestire i cluster HDInsight usando l'interfaccia utente Web di Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="2ea0f-109">For more information, see [Manage HDInsight clusters by using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ea0f-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2ea0f-110">Prerequisites</span></span>

* <span data-ttu-id="2ea0f-111">Un cluster HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-111">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="2ea0f-112">Per informazioni sulla creazione di un cluster, vedere [Introduzione all'uso di Hadoop con Hive in HDInsight in Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2ea0f-112">For information on creating cluster, see [Get started with Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2ea0f-113">I passaggi descritti in questo documento richiedono un cluster HDInsight che usa Linux.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-113">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="2ea0f-114">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-114">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2ea0f-115">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="2ea0f-115">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="open-the-hive-view"></a><span data-ttu-id="2ea0f-116">Aprire la visualizzazione Hive</span><span class="sxs-lookup"><span data-stu-id="2ea0f-116">Open the Hive view</span></span>

<span data-ttu-id="2ea0f-117">Per accedere alle visualizzazioni di Ambari dal portale di Azure, selezionare il cluster HDInsight e quindi **Visualizzazioni di Ambari** nella sezione **Collegamenti rapidi**.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-117">You can Ambari Views from the Azure portal; select your HDInsight cluster and then select **Ambari Views** from the **Quick Links** section.</span></span>

![Sezione Collegamenti rapidi del portale](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

<span data-ttu-id="2ea0f-119">Nell'elenco di viste selezionare __vista Hive__.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-119">From the list of views, select the __Hive View__.</span></span>

![Vista Hive selezionata](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> <span data-ttu-id="2ea0f-121">Quando si accede ad Ambari, viene richiesto di eseguire l'autenticazione al sito.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-121">When accessing Ambari, you are prompted to authenticate to the site.</span></span> <span data-ttu-id="2ea0f-122">Immettere il nome dell'account amministratore (il valore predefinito è `admin`) e la password usati durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-122">Enter the admin (default `admin`) account name and password you used when creating the cluster.</span></span>

<span data-ttu-id="2ea0f-123">Verrà visualizzata una pagina simile all'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="2ea0f-123">You should see a page similar to the following image:</span></span>

![Immagine del foglio di lavoro della query per la vista Hive](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <span data-ttu-id="2ea0f-125"><a name="hivequery"></a>Eseguire una query</span><span class="sxs-lookup"><span data-stu-id="2ea0f-125"><a name="hivequery"></a>Run a query</span></span>

<span data-ttu-id="2ea0f-126">Per eseguire una query Hive, seguire questa procedura dalla vista di Hive.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-126">To run a hive query, use the following steps from the Hive view.</span></span>

1. <span data-ttu-id="2ea0f-127">Dalla scheda __Query__ incollare le istruzioni HiveQL seguenti nel foglio di lavoro:</span><span class="sxs-lookup"><span data-stu-id="2ea0f-127">From the __Query__ tab, paste the following HiveQL statements into the worksheet:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    <span data-ttu-id="2ea0f-128">Di seguito sono elencate le istruzioni che eseguono queste azioni:</span><span class="sxs-lookup"><span data-stu-id="2ea0f-128">These statements perform the following actions:</span></span>

   * <span data-ttu-id="2ea0f-129">`DROP TABLE`: elimina la tabella e il file di dati, qualora la tabella esista già.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-129">`DROP TABLE` - Deletes the table and the data file, in case the table already exists.</span></span>

   * <span data-ttu-id="2ea0f-130">`CREATE EXTERNAL TABLE`: crea una nuova tabella "esterna" in Hive.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-130">`CREATE EXTERNAL TABLE` - Creates a new "external" table in Hive.</span></span>
   <span data-ttu-id="2ea0f-131">Le tabelle esterne archiviano solo la definizione della tabella in Hive.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-131">External tables store only the table definition in Hive.</span></span> <span data-ttu-id="2ea0f-132">I dati rimangono nel percorso originale.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-132">The data is left in the original location.</span></span>

   * <span data-ttu-id="2ea0f-133">`ROW FORMAT`: indica il modo in cui sono formattati i dati.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-133">`ROW FORMAT` - How the data is formatted.</span></span> <span data-ttu-id="2ea0f-134">In questo caso, i campi in ogni log sono separati da uno spazio.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-134">In this case, the fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="2ea0f-135">`STORED AS TEXTFILE LOCATION`: indica dove sono archiviati i dati e che sono archiviati come testo.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-135">`STORED AS TEXTFILE LOCATION` - Where the data is stored, and that it is stored as text.</span></span>

   * <span data-ttu-id="2ea0f-136">`SELECT`: seleziona un conteggio di tutte le righe in cui la colonna t4 include il valore [ERROR].</span><span class="sxs-lookup"><span data-stu-id="2ea0f-136">`SELECT` - Selects a count of all rows where column t4 contains the value [ERROR].</span></span>

     > [!NOTE]
     > <span data-ttu-id="2ea0f-137">Usa le tabelle esterne se si prevede che i dati sottostanti verranno aggiornati da un'origine esterna.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-137">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="2ea0f-138">Ad esempio, un processo di caricamento dati automatizzato o un'altra operazione MapReduce.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-138">For example, an automated data upload process, or by another MapReduce operation.</span></span> <span data-ttu-id="2ea0f-139">L'eliminazione di una tabella esterna *non* comporta anche l'eliminazione dei dati. Viene eliminata solo la definizione della tabella.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-139">Dropping an external table does *not* delete the data, only the table definition.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2ea0f-140">Mantenere la selezione di __Database__ __predefinita__.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-140">Leave the __Database__ selection at __default__.</span></span> <span data-ttu-id="2ea0f-141">Gli esempi di questo documento usano il database predefinito incluso in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-141">The examples in this document use the default database included with HDInsight.</span></span>

2. <span data-ttu-id="2ea0f-142">Per avviare la query, usare il pulsante **Execute** (Esegui) sotto il foglio di lavoro.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-142">To start the query, use the **Execute** button below the worksheet.</span></span> <span data-ttu-id="2ea0f-143">Il pulsante diventa arancione e il testo cambia in **Stop** (Arresta).</span><span class="sxs-lookup"><span data-stu-id="2ea0f-143">It turns orange and the text changes to **Stop**.</span></span>

3. <span data-ttu-id="2ea0f-144">Al termine dell'elaborazione della query, nella scheda **Results** (Risultati) vengono visualizzati i risultati dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-144">Once the query has finished, The **Results** tab displays the results of the operation.</span></span> <span data-ttu-id="2ea0f-145">Il testo seguente è il risultato della query:</span><span class="sxs-lookup"><span data-stu-id="2ea0f-145">The following text is the result of the query:</span></span>

        sev       cnt
        [ERROR]   3

    <span data-ttu-id="2ea0f-146">La scheda **Logs** può essere usata per visualizzare le informazioni sulla registrazione create dal processo,</span><span class="sxs-lookup"><span data-stu-id="2ea0f-146">The **Logs** tab can be used to view the logging information created by the job.</span></span>

   > [!TIP]
   > <span data-ttu-id="2ea0f-147">La finestra di dialogo **Save results** (Salva risultati) nella parte superiore sinistra della sezione **Query Process Results** (Risultati del processo query) consente di scaricare o salvare i risultati.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-147">The **Save results** drop-down dialog in the upper left of the **Query Process Results** section allows you to download or save results.</span></span>

4. <span data-ttu-id="2ea0f-148">Selezionare le prime quattro righe di questa query, quindi selezionare **Execute** (Esegui).</span><span class="sxs-lookup"><span data-stu-id="2ea0f-148">Select the first four lines of this query, then select **Execute**.</span></span> <span data-ttu-id="2ea0f-149">Si noti che, al termine del processo, non viene visualizzato alcun risultato.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-149">Notice that there are no results when the job completes.</span></span> <span data-ttu-id="2ea0f-150">Se si usa il pulsante **Execute** (Esegui) quando parte della query è selezionata, verranno eseguite solo le istruzioni selezionate.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-150">Using the **Execute** button when part of the query is selected only runs the selected statements.</span></span> <span data-ttu-id="2ea0f-151">In questo caso, la selezione non include l'istruzione finale che recupera le righe dalla tabella.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-151">In this case, the selection didn't include the final statement that retrieves rows from the table.</span></span> <span data-ttu-id="2ea0f-152">Se si seleziona solo tale riga e si usa **Execute** (Esegui), verranno visualizzati i risultati previsti.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-152">If you select just that line and use **Execute**, you should see the expected results.</span></span>

5. <span data-ttu-id="2ea0f-153">Per aggiungere un foglio di lavoro, usare il pulsate **New Worksheet** (Nuovo foglio di lavoro) nella parte inferiore di **Query Editor** (Editor query).</span><span class="sxs-lookup"><span data-stu-id="2ea0f-153">To add a worksheet, use the **New Worksheet** button at the bottom of the **Query Editor**.</span></span> <span data-ttu-id="2ea0f-154">Nel nuovo foglio di lavoro immettere le istruzioni HiveQL seguenti:</span><span class="sxs-lookup"><span data-stu-id="2ea0f-154">In the new worksheet, enter the following HiveQL statements:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  <span data-ttu-id="2ea0f-155">Di seguito sono elencate le istruzioni che eseguono queste azioni:</span><span class="sxs-lookup"><span data-stu-id="2ea0f-155">These statements perform the following actions:</span></span>

   * <span data-ttu-id="2ea0f-156">**CREATE TABLE IF NOT EXISTS** : crea una tabella, se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-156">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="2ea0f-157">Poiché non viene usata la parola chiave **EXTERNAL**, viene creata una tabella interna.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-157">Since the **EXTERNAL** keyword is not used, an internal table is created.</span></span> <span data-ttu-id="2ea0f-158">Una tabella interna verrà archiviata nel data warehouse di Hive e gestita completamente da Hive.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-158">An internal table is stored in the Hive data warehouse and is managed completely by Hive.</span></span> <span data-ttu-id="2ea0f-159">A differenza delle tabelle esterne, se si elimina una tabella interna, vengono eliminati anche i dati sottostanti.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-159">Unlike external tables, dropping an internal table deletes the underlying data as well.</span></span>

   * <span data-ttu-id="2ea0f-160">**STORED AS ORC** : archivia i dati nel formato ORC (Optimized Row Columnar).</span><span class="sxs-lookup"><span data-stu-id="2ea0f-160">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="2ea0f-161">ORC è un formato altamente ottimizzato ed efficiente per l'archiviazione di dati Hive.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-161">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="2ea0f-162">**INSERT OVERWRITE ... SELECT**: seleziona dalla tabella **log4jLogs** le righe contenenti `[ERROR]` e quindi inserisce i dati nella tabella **errorLogs**.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-162">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain `[ERROR]`, and then inserts the data into the **errorLogs** table.</span></span>

     <span data-ttu-id="2ea0f-163">Usare il pulsante **Execute** (Esegui) per eseguire la query.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-163">Use the **Execute** button to run this query.</span></span> <span data-ttu-id="2ea0f-164">La scheda **Results** (Risultati) non contiene informazioni quando la query restituisce zero righe.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-164">The **Results** tab does not contain any information when the query returns zero rows.</span></span> <span data-ttu-id="2ea0f-165">Lo stato visualizzato deve essere **SUCCEEDED** dopo il completamento della query.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-165">The status should show as **SUCCEEDED** once the query completes.</span></span>

### <a name="visual-explain"></a><span data-ttu-id="2ea0f-166">Visual Explain</span><span class="sxs-lookup"><span data-stu-id="2ea0f-166">Visual explain</span></span>

<span data-ttu-id="2ea0f-167">Per aprire una visualizzazione del piano di query, selezionare la scheda **Visual Explain** (Spiegazione visiva) sotto il foglio di lavoro.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-167">To display a visualization of the query plan, select the **Visual Explain** tab below the worksheet.</span></span>

<span data-ttu-id="2ea0f-168">La vista **Visual Explain** (Spiegazione visiva) della query può essere utile per conoscere il flusso delle query complesse.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-168">The **Visual Explain** view of the query can be helpful in understanding the flow of complex queries.</span></span> <span data-ttu-id="2ea0f-169">Per un equivalente testuale di questa visualizzazione, usare il pulsante **Explain** (Spiega) in Query Editor.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-169">You can view a textual equivalent of this view by using the **Explain** button in the Query Editor.</span></span>

### <a name="tez-ui"></a><span data-ttu-id="2ea0f-170">Interfaccia utente di Tez</span><span class="sxs-lookup"><span data-stu-id="2ea0f-170">Tez UI</span></span>

<span data-ttu-id="2ea0f-171">Per visualizzare l'interfaccia utente di Tez per la query, selezionare la scheda **Tez** sotto il foglio di lavoro.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-171">To display the Tez UI for the query, select the **Tez** tab below the worksheet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2ea0f-172">Tez non viene usato per risolvere tutte le query.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-172">Tez is not used to resolve all queries.</span></span> <span data-ttu-id="2ea0f-173">Molte query possono essere risolte senza usare Tez.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-173">Many queries can be resolved without using Tez.</span></span> 

<span data-ttu-id="2ea0f-174">Se per risolvere la query è stato usato Tez, viene visualizzato il grafo aciclico diretto.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-174">If Tez was used to resolve the query, the Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="2ea0f-175">Se si vuole visualizzare il DAG per le query eseguite in passato o eseguire il debug del processo Tez, usare invece [Tez View](hdinsight-debug-ambari-tez-view.md) .</span><span class="sxs-lookup"><span data-stu-id="2ea0f-175">If you want to view the DAG for queries you've ran in the past, or debug the Tez process, use the [Tez View](hdinsight-debug-ambari-tez-view.md) instead.</span></span>

## <a name="view-job-history"></a><span data-ttu-id="2ea0f-176">Visualizzare la cronologia processo</span><span class="sxs-lookup"><span data-stu-id="2ea0f-176">View job history</span></span>

<span data-ttu-id="2ea0f-177">La scheda __Jobs__ (Processi) visualizza una cronologia delle query Hive.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-177">The __Jobs__ tab displays a history of Hive queries.</span></span>

![Immagine della cronologia processo](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a><span data-ttu-id="2ea0f-179">Tabelle di database</span><span class="sxs-lookup"><span data-stu-id="2ea0f-179">Database tables</span></span>

<span data-ttu-id="2ea0f-180">È possibile usare la scheda __Tables__ (Tabelle) per utilizzare le tabelle in un database Hive.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-180">You can use the __Tables__ tab to work with tables within a Hive database.</span></span>

![Immagine della scheda delle tabelle](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a><span data-ttu-id="2ea0f-182">Query salvate</span><span class="sxs-lookup"><span data-stu-id="2ea0f-182">Saved queries</span></span>

<span data-ttu-id="2ea0f-183">Dalla scheda Query è facoltativamente possibile salvare le query.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-183">From the Query tab, you can optionally save queries.</span></span> <span data-ttu-id="2ea0f-184">Dopo avere salvato una query, è possibile usarla di nuovo dalla scheda __Saved Queries__ (Query salvate).</span><span class="sxs-lookup"><span data-stu-id="2ea0f-184">Once saved, you can reuse the query from the __Saved Queries__ tab.</span></span>

![Immagine della scheda delle query salvate](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a><span data-ttu-id="2ea0f-186">Funzioni definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="2ea0f-186">User-defined functions</span></span>

<span data-ttu-id="2ea0f-187">Hive può anche essere esteso tramite funzioni definite dall'utente,</span><span class="sxs-lookup"><span data-stu-id="2ea0f-187">Hive can also be extended through user-defined functions (UDF).</span></span> <span data-ttu-id="2ea0f-188">che consentono di implementare funzionalità o logica non facilmente modellate in HiveQL.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-188">A UDF allows you to implement functionality or logic that isn't easily modeled in HiveQL.</span></span>

<span data-ttu-id="2ea0f-189">La scheda della funzione definita dall'utente nella parte superiore della vista Hive consente di dichiarare e salvare un set di funzioni definite dall'utente,</span><span class="sxs-lookup"><span data-stu-id="2ea0f-189">The UDF tab at the top of the Hive View allows you to declare and save a set of UDFs.</span></span> <span data-ttu-id="2ea0f-190">che è possibile usare con **Query Editor**.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-190">These UDFs can be used with the **Query Editor**.</span></span>

![Immagine della scheda delle funzioni definite dall'utente](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

<span data-ttu-id="2ea0f-192">Dopo avere aggiunto una funzione definita dall'utente alla visualizzazione Hive, verrà visualizzato un pulsante **Insert udfs** (Inserisci funzioni definite dall'utente) nella parte inferiore di **Query Editor**.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-192">Once you have added a UDF to the Hive View, an **Insert udfs** button appears at the bottom of the **Query Editor**.</span></span> <span data-ttu-id="2ea0f-193">Se si seleziona questa voce, verrà visualizzato un elenco di riepilogo a discesa di funzioni definite dall'utente nella vista Hive.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-193">Selecting this entry displays a drop-down list of the UDFs defined in the Hive View.</span></span> <span data-ttu-id="2ea0f-194">La selezione di una funzione definita dall'utente aggiungerà istruzioni HiveQL alla query per abilitare la funzione definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-194">Selecting a UDF adds HiveQL statements to your query to enable the UDF.</span></span>

<span data-ttu-id="2ea0f-195">Ad esempio, se è stata specificata una funzione definita dall'utente con le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="2ea0f-195">For example, if you have defined a UDF with the following properties:</span></span>

* <span data-ttu-id="2ea0f-196">Nome della risorsa: myudfs</span><span class="sxs-lookup"><span data-stu-id="2ea0f-196">Resource name: myudfs</span></span>

* <span data-ttu-id="2ea0f-197">Percorso della risorsa: /myudfs.jar</span><span class="sxs-lookup"><span data-stu-id="2ea0f-197">Resource path: /myudfs.jar</span></span>

* <span data-ttu-id="2ea0f-198">Nome della funzione definita dall'utente: myawesomeudf</span><span class="sxs-lookup"><span data-stu-id="2ea0f-198">UDF name: myawesomeudf</span></span>

* <span data-ttu-id="2ea0f-199">Nome della classe per la funzione definita dall'utente: com.myudfs.Awesome</span><span class="sxs-lookup"><span data-stu-id="2ea0f-199">UDF class name: com.myudfs.Awesome</span></span>

<span data-ttu-id="2ea0f-200">Se si usa il pulsante **Insert udfs** (Inserisci funzioni definite dall'utente), verrà visualizzata una voce denominata **myudfs**, con un altro elenco a discesa per ogni funzione definita dall'utente specificata per tale risorsa.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-200">Using the **Insert udfs** button displays an entry named **myudfs**, with another drop-down for each UDF defined for that resource.</span></span> <span data-ttu-id="2ea0f-201">In questo caso, **myawesomeudf**.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-201">In this case, **myawesomeudf**.</span></span> <span data-ttu-id="2ea0f-202">Se si seleziona questa voce, verrà aggiunto quanto segue all'inizio della query:</span><span class="sxs-lookup"><span data-stu-id="2ea0f-202">Selecting this entry adds the following to the beginning of the query:</span></span>

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

<span data-ttu-id="2ea0f-203">Si potrà quindi usare la funzione definita dall'utente nella query,</span><span class="sxs-lookup"><span data-stu-id="2ea0f-203">You can then use the UDF in your query.</span></span> <span data-ttu-id="2ea0f-204">Ad esempio, `SELECT myawesomeudf(name) FROM people;`.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-204">For example, `SELECT myawesomeudf(name) FROM people;`.</span></span>

<span data-ttu-id="2ea0f-205">Per altre informazioni sull'uso di funzioni definite dall'utente con Hive in HDInsight, vedere i documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="2ea0f-205">For more information on using UDFs with Hive on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="2ea0f-206">Usare Python con Hive e Pig in HDInsight</span><span class="sxs-lookup"><span data-stu-id="2ea0f-206">Using Python with Hive and Pig in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="2ea0f-207">Come aggiungere una funzione definita dall'utente Hive personalizzata in HDInsight</span><span class="sxs-lookup"><span data-stu-id="2ea0f-207">How to add a custom Hive UDF to HDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a><span data-ttu-id="2ea0f-208">Settings di Hive</span><span class="sxs-lookup"><span data-stu-id="2ea0f-208">Hive settings</span></span>

<span data-ttu-id="2ea0f-209">Le impostazioni possono essere usate per modificare varie impostazioni di Hive.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-209">Settings can be used to change various Hive settings.</span></span> <span data-ttu-id="2ea0f-210">Consentono ad esempio di cambiare il motore di esecuzione per Hive da Tez (opzione predefinita) a MapReduce.</span><span class="sxs-lookup"><span data-stu-id="2ea0f-210">For example, changing the execution engine for Hive from Tez (the default) to MapReduce.</span></span>

## <span data-ttu-id="2ea0f-211"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2ea0f-211"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="2ea0f-212">Per informazioni generali su Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="2ea0f-212">For general information on Hive in HDInsight:</span></span>

* [<span data-ttu-id="2ea0f-213">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="2ea0f-213">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="2ea0f-214">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="2ea0f-214">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="2ea0f-215">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="2ea0f-215">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="2ea0f-216">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="2ea0f-216">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
