---
title: aaaUse Ambari viste toowork con Hive in HDInsight (Hadoop) - Azure | Documenti Microsoft
description: Informazioni su come toouse hello Hive vista dalle query Hive toosubmit browser web. Hello Hive visualizzazione fa parte di hello che dell'interfaccia utente Web Ambari fornito con il cluster HDInsight basati su Linux.
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
ms.openlocfilehash: f9a77b652e70d34a0ff9165fbb8c2e16d3401ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-hive-view-with-hadoop-in-hdinsight"></a><span data-ttu-id="329ab-104">Utilizzare hello vista Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="329ab-104">Use hello Hive View with Hadoop in HDInsight</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="329ab-105">Informazioni su come una query utilizza la visualizzazione Hive Ambari toorun Hive.</span><span class="sxs-lookup"><span data-stu-id="329ab-105">Learn how toorun Hive queries using Ambari Hive View.</span></span> <span data-ttu-id="329ab-106">Ambari è un'utilità per la gestione e il monitoraggio fornita con i cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="329ab-106">Ambari is a management and monitoring utility provided with Linux-based HDInsight clusters.</span></span> <span data-ttu-id="329ab-107">Una delle funzionalità di hello fornita tramite Ambari è un'interfaccia utente Web che può essere una query Hive toorun utilizzato.</span><span class="sxs-lookup"><span data-stu-id="329ab-107">One of hello features provided through Ambari is a Web UI that can be used toorun Hive queries.</span></span>

> [!NOTE]
> <span data-ttu-id="329ab-108">Ambari include numerose funzionalità non illustrate in questo documento.</span><span class="sxs-lookup"><span data-stu-id="329ab-108">Ambari has many capabilities that are not discussed in this document.</span></span> <span data-ttu-id="329ab-109">Per ulteriori informazioni, vedere [HDInsight gestire cluster utilizzando l'interfaccia utente Web Ambari hello](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="329ab-109">For more information, see [Manage HDInsight clusters by using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="329ab-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="329ab-110">Prerequisites</span></span>

* <span data-ttu-id="329ab-111">Un cluster HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="329ab-111">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="329ab-112">Per informazioni sulla creazione di un cluster, vedere [Introduzione all'uso di Hadoop con Hive in HDInsight in Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="329ab-112">For information on creating cluster, see [Get started with Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="329ab-113">passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Linux.</span><span class="sxs-lookup"><span data-stu-id="329ab-113">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="329ab-114">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="329ab-114">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="329ab-115">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="329ab-115">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="open-hello-hive-view"></a><span data-ttu-id="329ab-116">Aprire la visualizzazione di Hive hello</span><span class="sxs-lookup"><span data-stu-id="329ab-116">Open hello Hive view</span></span>

<span data-ttu-id="329ab-117">È possibile Ambari viste dal portale di Azure; hello Selezionare il cluster HDInsight e quindi **Ambari viste** da hello **collegamenti rapidi** sezione.</span><span class="sxs-lookup"><span data-stu-id="329ab-117">You can Ambari Views from hello Azure portal; select your HDInsight cluster and then select **Ambari Views** from hello **Quick Links** section.</span></span>

![sezione collegamenti rapidi del portale hello](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

<span data-ttu-id="329ab-119">Hello l'elenco delle visualizzazioni, selezionare hello __Hive vista__.</span><span class="sxs-lookup"><span data-stu-id="329ab-119">From hello list of views, select hello __Hive View__.</span></span>

![Hello Hive visualizzazione selezionata](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> <span data-ttu-id="329ab-121">Quando si accede a Ambari, verrà richiesta tooauthenticate toohello sito.</span><span class="sxs-lookup"><span data-stu-id="329ab-121">When accessing Ambari, you are prompted tooauthenticate toohello site.</span></span> <span data-ttu-id="329ab-122">Immettere salve (impostazione predefinita `admin`) del cluster di hello nome e la password utilizzati per la creazione di account.</span><span class="sxs-lookup"><span data-stu-id="329ab-122">Enter hello admin (default `admin`) account name and password you used when creating hello cluster.</span></span>

<span data-ttu-id="329ab-123">Verrà visualizzato un toohello simile pagina seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="329ab-123">You should see a page similar toohello following image:</span></span>

![Immagine di foglio di lavoro di query hello per Vista Hive hello](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <span data-ttu-id="329ab-125"><a name="hivequery"></a>Eseguire una query</span><span class="sxs-lookup"><span data-stu-id="329ab-125"><a name="hivequery"></a>Run a query</span></span>

<span data-ttu-id="329ab-126">toorun una query hive, usare hello dalla visualizzazione Hive hello come segue.</span><span class="sxs-lookup"><span data-stu-id="329ab-126">toorun a hive query, use hello following steps from hello Hive view.</span></span>

1. <span data-ttu-id="329ab-127">Da hello __Query__ scheda, incollare hello seguendo le istruzioni HiveQL nel foglio di lavoro hello:</span><span class="sxs-lookup"><span data-stu-id="329ab-127">From hello __Query__ tab, paste hello following HiveQL statements into hello worksheet:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    <span data-ttu-id="329ab-128">Queste istruzioni consentono di eseguire hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="329ab-128">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="329ab-129">`DROP TABLE`: Elimina tabella hello e file di dati hello, nel caso in cui hello tabella esiste già.</span><span class="sxs-lookup"><span data-stu-id="329ab-129">`DROP TABLE` - Deletes hello table and hello data file, in case hello table already exists.</span></span>

   * <span data-ttu-id="329ab-130">`CREATE EXTERNAL TABLE`: crea una nuova tabella "esterna" in Hive.</span><span class="sxs-lookup"><span data-stu-id="329ab-130">`CREATE EXTERNAL TABLE` - Creates a new "external" table in Hive.</span></span>
   <span data-ttu-id="329ab-131">Le tabelle esterne archiviano solo definizione della tabella hello nell'Hive.</span><span class="sxs-lookup"><span data-stu-id="329ab-131">External tables store only hello table definition in Hive.</span></span> <span data-ttu-id="329ab-132">dati Hello viene lasciati nella posizione originale hello.</span><span class="sxs-lookup"><span data-stu-id="329ab-132">hello data is left in hello original location.</span></span>

   * <span data-ttu-id="329ab-133">`ROW FORMAT`-Modalità hello di formattazione.</span><span class="sxs-lookup"><span data-stu-id="329ab-133">`ROW FORMAT` - How hello data is formatted.</span></span> <span data-ttu-id="329ab-134">In questo caso, i campi di hello in ogni log sono separati da uno spazio.</span><span class="sxs-lookup"><span data-stu-id="329ab-134">In this case, hello fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="329ab-135">`STORED AS TEXTFILE LOCATION`-Hello memorizzazione dei dati e che viene archiviato come testo.</span><span class="sxs-lookup"><span data-stu-id="329ab-135">`STORED AS TEXTFILE LOCATION` - Where hello data is stored, and that it is stored as text.</span></span>

   * <span data-ttu-id="329ab-136">`SELECT`-Seleziona un conteggio di tutte le righe in cui t4 colonna contiene il valore di hello [errore].</span><span class="sxs-lookup"><span data-stu-id="329ab-136">`SELECT` - Selects a count of all rows where column t4 contains hello value [ERROR].</span></span>

     > [!NOTE]
     > <span data-ttu-id="329ab-137">Le tabelle esterne da utilizzare quando si prevede di hello sottostante toobe dati aggiornati da un'origine esterna.</span><span class="sxs-lookup"><span data-stu-id="329ab-137">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="329ab-138">Ad esempio, un processo di caricamento dati automatizzato o un'altra operazione MapReduce.</span><span class="sxs-lookup"><span data-stu-id="329ab-138">For example, an automated data upload process, or by another MapReduce operation.</span></span> <span data-ttu-id="329ab-139">Eliminazione di una tabella esterna *non* eliminare dati hello e definizione della tabella solo hello.</span><span class="sxs-lookup"><span data-stu-id="329ab-139">Dropping an external table does *not* delete hello data, only hello table definition.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="329ab-140">Lasciare hello __Database__ selezione in __predefinito__.</span><span class="sxs-lookup"><span data-stu-id="329ab-140">Leave hello __Database__ selection at __default__.</span></span> <span data-ttu-id="329ab-141">esempi di Hello in questo documento usano database predefinito hello incluso in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="329ab-141">hello examples in this document use hello default database included with HDInsight.</span></span>

2. <span data-ttu-id="329ab-142">query hello toostart, utilizzare hello **Execute** pulsante foglio di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="329ab-142">toostart hello query, use hello **Execute** button below hello worksheet.</span></span> <span data-ttu-id="329ab-143">Le modifiche al testo arancione e hello diventa troppo**arrestare**.</span><span class="sxs-lookup"><span data-stu-id="329ab-143">It turns orange and hello text changes too**Stop**.</span></span>

3. <span data-ttu-id="329ab-144">Al termine di query hello, hello **risultati** scheda Visualizza risultati di hello dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="329ab-144">Once hello query has finished, hello **Results** tab displays hello results of hello operation.</span></span> <span data-ttu-id="329ab-145">Dopo il testo Hello è il risultato di hello di query hello:</span><span class="sxs-lookup"><span data-stu-id="329ab-145">hello following text is hello result of hello query:</span></span>

        sev       cnt
        [ERROR]   3

    <span data-ttu-id="329ab-146">Hello **registri** scheda può essere utilizzato tooview informazioni di registrazione di hello create dal processo di hello.</span><span class="sxs-lookup"><span data-stu-id="329ab-146">hello **Logs** tab can be used tooview hello logging information created by hello job.</span></span>

   > [!TIP]
   > <span data-ttu-id="329ab-147">Hello **salvare i risultati** finestra di dialogo di riepilogo a discesa in hello superiore sinistra del hello **risultati della Query processo** sezione permette toodownload o salvare i risultati.</span><span class="sxs-lookup"><span data-stu-id="329ab-147">hello **Save results** drop-down dialog in hello upper left of hello **Query Process Results** section allows you toodownload or save results.</span></span>

4. <span data-ttu-id="329ab-148">Selezionare hello prime quattro righe di questa query, quindi selezionare **Execute**.</span><span class="sxs-lookup"><span data-stu-id="329ab-148">Select hello first four lines of this query, then select **Execute**.</span></span> <span data-ttu-id="329ab-149">Si noti che non sono presenti risultati al termine il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="329ab-149">Notice that there are no results when hello job completes.</span></span> <span data-ttu-id="329ab-150">Utilizzo di hello **Execute** pulsante se fa parte di query hello è selezionata solo esecuzioni hello istruzioni selezionate.</span><span class="sxs-lookup"><span data-stu-id="329ab-150">Using hello **Execute** button when part of hello query is selected only runs hello selected statements.</span></span> <span data-ttu-id="329ab-151">In questo caso, selezione hello non include l'istruzione finale hello che recupera le righe dalla tabella hello.</span><span class="sxs-lookup"><span data-stu-id="329ab-151">In this case, hello selection didn't include hello final statement that retrieves rows from hello table.</span></span> <span data-ttu-id="329ab-152">Se si seleziona solo tale riga e utilizzare **Execute**, si otterranno risultati hello previsto.</span><span class="sxs-lookup"><span data-stu-id="329ab-152">If you select just that line and use **Execute**, you should see hello expected results.</span></span>

5. <span data-ttu-id="329ab-153">tooadd un foglio di lavoro, utilizzare hello **nuovo foglio di lavoro** pulsante nella parte inferiore di hello di hello **Editor di Query**.</span><span class="sxs-lookup"><span data-stu-id="329ab-153">tooadd a worksheet, use hello **New Worksheet** button at hello bottom of hello **Query Editor**.</span></span> <span data-ttu-id="329ab-154">In hello nuovo foglio di lavoro, immettere hello seguendo le istruzioni HiveQL:</span><span class="sxs-lookup"><span data-stu-id="329ab-154">In hello new worksheet, enter hello following HiveQL statements:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  <span data-ttu-id="329ab-155">Queste istruzioni consentono di eseguire hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="329ab-155">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="329ab-156">**CREATE TABLE IF NOT EXISTS** : crea una tabella, se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="329ab-156">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="329ab-157">Poiché hello **esterno** parola chiave non viene utilizzato, viene creata una tabella interna.</span><span class="sxs-lookup"><span data-stu-id="329ab-157">Since hello **EXTERNAL** keyword is not used, an internal table is created.</span></span> <span data-ttu-id="329ab-158">Una tabella interna verrà archiviata nel data warehouse di hello Hive e completamente gestita da Hive.</span><span class="sxs-lookup"><span data-stu-id="329ab-158">An internal table is stored in hello Hive data warehouse and is managed completely by Hive.</span></span> <span data-ttu-id="329ab-159">A differenza delle tabelle esterne, eliminazione di una tabella interna Elimina hello anche i dati sottostanti.</span><span class="sxs-lookup"><span data-stu-id="329ab-159">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

   * <span data-ttu-id="329ab-160">**ARCHIVIATI AS ORC** -archivia i dati di hello in formato con ottimizzazione per la riga a colonne (ORC).</span><span class="sxs-lookup"><span data-stu-id="329ab-160">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="329ab-161">ORC è un formato altamente ottimizzato ed efficiente per l'archiviazione di dati Hive.</span><span class="sxs-lookup"><span data-stu-id="329ab-161">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="329ab-162">**INSERT OVERWRITE ... Selezionare** -seleziona le righe da hello **log4jLogs** tabella contenenti `[ERROR]`, e quindi inserisce hello dati in hello **degli errori** tabella.</span><span class="sxs-lookup"><span data-stu-id="329ab-162">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain `[ERROR]`, and then inserts hello data into hello **errorLogs** table.</span></span>

     <span data-ttu-id="329ab-163">Hello utilizzare **Execute** pulsante toorun questa query.</span><span class="sxs-lookup"><span data-stu-id="329ab-163">Use hello **Execute** button toorun this query.</span></span> <span data-ttu-id="329ab-164">Hello **risultati** scheda non contiene alcuna informazione hello query restituisce zero righe.</span><span class="sxs-lookup"><span data-stu-id="329ab-164">hello **Results** tab does not contain any information when hello query returns zero rows.</span></span> <span data-ttu-id="329ab-165">deve essere stato Hello **SUCCEEDED** una volta completata la query hello.</span><span class="sxs-lookup"><span data-stu-id="329ab-165">hello status should show as **SUCCEEDED** once hello query completes.</span></span>

### <a name="visual-explain"></a><span data-ttu-id="329ab-166">Visual Explain</span><span class="sxs-lookup"><span data-stu-id="329ab-166">Visual explain</span></span>

<span data-ttu-id="329ab-167">una visualizzazione del piano di query hello, seleziona hello toodisplay **spiegare Visual** scheda di sotto del foglio di lavoro di hello.</span><span class="sxs-lookup"><span data-stu-id="329ab-167">toodisplay a visualization of hello query plan, select hello **Visual Explain** tab below hello worksheet.</span></span>

<span data-ttu-id="329ab-168">Hello **spiegare Visual** visualizzazione di query hello può essere utili per capire il flusso di hello di query complesse.</span><span class="sxs-lookup"><span data-stu-id="329ab-168">hello **Visual Explain** view of hello query can be helpful in understanding hello flow of complex queries.</span></span> <span data-ttu-id="329ab-169">È possibile visualizzare un equivalente testuale di questa vista utilizzando hello **esplicativo** pulsante hello Editor di Query.</span><span class="sxs-lookup"><span data-stu-id="329ab-169">You can view a textual equivalent of this view by using hello **Explain** button in hello Query Editor.</span></span>

### <a name="tez-ui"></a><span data-ttu-id="329ab-170">Interfaccia utente di Tez</span><span class="sxs-lookup"><span data-stu-id="329ab-170">Tez UI</span></span>

<span data-ttu-id="329ab-171">toodisplay hello Tez UI per query hello, seleziona hello **Tez** scheda di sotto del foglio di lavoro di hello.</span><span class="sxs-lookup"><span data-stu-id="329ab-171">toodisplay hello Tez UI for hello query, select hello **Tez** tab below hello worksheet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="329ab-172">Tez è tooresolve non in uso tutte le query.</span><span class="sxs-lookup"><span data-stu-id="329ab-172">Tez is not used tooresolve all queries.</span></span> <span data-ttu-id="329ab-173">Molte query possono essere risolte senza usare Tez.</span><span class="sxs-lookup"><span data-stu-id="329ab-173">Many queries can be resolved without using Tez.</span></span> 

<span data-ttu-id="329ab-174">Se Tez query hello tooresolve usato, viene visualizzato hello descritto grafico aciclico diretto (DAG).</span><span class="sxs-lookup"><span data-stu-id="329ab-174">If Tez was used tooresolve hello query, hello Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="329ab-175">Se si desidera tooview hello DAG per query è stato eseguito in hello precedente o eseguire il debug hello Tez processo, utilizzare hello [Tez vista](hdinsight-debug-ambari-tez-view.md) invece.</span><span class="sxs-lookup"><span data-stu-id="329ab-175">If you want tooview hello DAG for queries you've ran in hello past, or debug hello Tez process, use hello [Tez View](hdinsight-debug-ambari-tez-view.md) instead.</span></span>

## <a name="view-job-history"></a><span data-ttu-id="329ab-176">Visualizzare la cronologia processo</span><span class="sxs-lookup"><span data-stu-id="329ab-176">View job history</span></span>

<span data-ttu-id="329ab-177">Hello __processi__ scheda Visualizza una cronologia delle query Hive.</span><span class="sxs-lookup"><span data-stu-id="329ab-177">hello __Jobs__ tab displays a history of Hive queries.</span></span>

![Immagine di cronologia processo hello](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a><span data-ttu-id="329ab-179">Tabelle di database</span><span class="sxs-lookup"><span data-stu-id="329ab-179">Database tables</span></span>

<span data-ttu-id="329ab-180">È possibile utilizzare hello __tabelle__ scheda toowork con le tabelle all'interno di un database Hive.</span><span class="sxs-lookup"><span data-stu-id="329ab-180">You can use hello __Tables__ tab toowork with tables within a Hive database.</span></span>

![Immagine della scheda tabelle hello](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a><span data-ttu-id="329ab-182">Query salvate</span><span class="sxs-lookup"><span data-stu-id="329ab-182">Saved queries</span></span>

<span data-ttu-id="329ab-183">Dalla scheda Query hello, è possibile salvare le query.</span><span class="sxs-lookup"><span data-stu-id="329ab-183">From hello Query tab, you can optionally save queries.</span></span> <span data-ttu-id="329ab-184">Dopo il salvataggio, è possibile riutilizzare query hello da hello __query salvate__ scheda.</span><span class="sxs-lookup"><span data-stu-id="329ab-184">Once saved, you can reuse hello query from hello __Saved Queries__ tab.</span></span>

![Immagine della scheda delle query salvate](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a><span data-ttu-id="329ab-186">Funzioni definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="329ab-186">User-defined functions</span></span>

<span data-ttu-id="329ab-187">Hive può anche essere esteso tramite funzioni definite dall'utente,</span><span class="sxs-lookup"><span data-stu-id="329ab-187">Hive can also be extended through user-defined functions (UDF).</span></span> <span data-ttu-id="329ab-188">Una funzione definita dall'utente consente a funzionalità tooimplement o logica che non è facilmente modellata in HiveQL.</span><span class="sxs-lookup"><span data-stu-id="329ab-188">A UDF allows you tooimplement functionality or logic that isn't easily modeled in HiveQL.</span></span>

<span data-ttu-id="329ab-189">scheda definita dall'utente nella parte superiore di hello di hello Hive vista Hello consente toodeclare e salvare un set di funzioni definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="329ab-189">hello UDF tab at hello top of hello Hive View allows you toodeclare and save a set of UDFs.</span></span> <span data-ttu-id="329ab-190">Queste funzioni definite dall'utente può essere utilizzato con hello **Editor di Query**.</span><span class="sxs-lookup"><span data-stu-id="329ab-190">These UDFs can be used with hello **Query Editor**.</span></span>

![Immagine della scheda delle funzioni definite dall'utente](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

<span data-ttu-id="329ab-192">Dopo aver aggiunto un toohello funzione definita dall'utente, vista Hive, un **inserire funzioni definite dall'utente** pulsante viene visualizzato nella parte inferiore di hello di hello **Editor di Query**.</span><span class="sxs-lookup"><span data-stu-id="329ab-192">Once you have added a UDF toohello Hive View, an **Insert udfs** button appears at hello bottom of hello **Query Editor**.</span></span> <span data-ttu-id="329ab-193">Selezionando questa voce visualizza un elenco di riepilogo a discesa di funzioni definite dall'utente definito nella vista Hive hello hello.</span><span class="sxs-lookup"><span data-stu-id="329ab-193">Selecting this entry displays a drop-down list of hello UDFs defined in hello Hive View.</span></span> <span data-ttu-id="329ab-194">Selezione di una funzione definita dall'utente aggiunge HiveQL istruzioni tooyour query tooenable hello funzione definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="329ab-194">Selecting a UDF adds HiveQL statements tooyour query tooenable hello UDF.</span></span>

<span data-ttu-id="329ab-195">Ad esempio, se è stata definita una funzione definita dall'utente con hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="329ab-195">For example, if you have defined a UDF with hello following properties:</span></span>

* <span data-ttu-id="329ab-196">Nome della risorsa: myudfs</span><span class="sxs-lookup"><span data-stu-id="329ab-196">Resource name: myudfs</span></span>

* <span data-ttu-id="329ab-197">Percorso della risorsa: /myudfs.jar</span><span class="sxs-lookup"><span data-stu-id="329ab-197">Resource path: /myudfs.jar</span></span>

* <span data-ttu-id="329ab-198">Nome della funzione definita dall'utente: myawesomeudf</span><span class="sxs-lookup"><span data-stu-id="329ab-198">UDF name: myawesomeudf</span></span>

* <span data-ttu-id="329ab-199">Nome della classe per la funzione definita dall'utente: com.myudfs.Awesome</span><span class="sxs-lookup"><span data-stu-id="329ab-199">UDF class name: com.myudfs.Awesome</span></span>

<span data-ttu-id="329ab-200">Utilizzando hello **inserire funzioni definite dall'utente** pulsante Visualizza una voce denominata **myudfs**, con un altro elenco a discesa per ogni funzione definita dall'utente definito per tale risorsa.</span><span class="sxs-lookup"><span data-stu-id="329ab-200">Using hello **Insert udfs** button displays an entry named **myudfs**, with another drop-down for each UDF defined for that resource.</span></span> <span data-ttu-id="329ab-201">In questo caso, **myawesomeudf**.</span><span class="sxs-lookup"><span data-stu-id="329ab-201">In this case, **myawesomeudf**.</span></span> <span data-ttu-id="329ab-202">Selezionando questa voce aggiunge hello toohello inizio della query hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="329ab-202">Selecting this entry adds hello following toohello beginning of hello query:</span></span>

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

<span data-ttu-id="329ab-203">È quindi possibile utilizzare hello funzione definita dall'utente nella query.</span><span class="sxs-lookup"><span data-stu-id="329ab-203">You can then use hello UDF in your query.</span></span> <span data-ttu-id="329ab-204">ad esempio `SELECT myawesomeudf(name) FROM people;`.</span><span class="sxs-lookup"><span data-stu-id="329ab-204">For example, `SELECT myawesomeudf(name) FROM people;`.</span></span>

<span data-ttu-id="329ab-205">Per ulteriori informazioni sull'utilizzo di funzioni definite dall'utente con Hive in HDInsight, vedere hello seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="329ab-205">For more information on using UDFs with Hive on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="329ab-206">Usare Python con Hive e Pig in HDInsight</span><span class="sxs-lookup"><span data-stu-id="329ab-206">Using Python with Hive and Pig in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="329ab-207">Come tooadd un tooHDInsight Hive definita dall'utente personalizzato</span><span class="sxs-lookup"><span data-stu-id="329ab-207">How tooadd a custom Hive UDF tooHDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a><span data-ttu-id="329ab-208">Settings di Hive</span><span class="sxs-lookup"><span data-stu-id="329ab-208">Hive settings</span></span>

<span data-ttu-id="329ab-209">Le impostazioni possono essere utilizzati toochange varie impostazioni di Hive.</span><span class="sxs-lookup"><span data-stu-id="329ab-209">Settings can be used toochange various Hive settings.</span></span> <span data-ttu-id="329ab-210">Modifica, ad esempio, il motore di esecuzione hello per Hive da tooMapReduce Tez (impostazione predefinita hello).</span><span class="sxs-lookup"><span data-stu-id="329ab-210">For example, changing hello execution engine for Hive from Tez (hello default) tooMapReduce.</span></span>

## <span data-ttu-id="329ab-211"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="329ab-211"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="329ab-212">Per informazioni generali su Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="329ab-212">For general information on Hive in HDInsight:</span></span>

* [<span data-ttu-id="329ab-213">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="329ab-213">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="329ab-214">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="329ab-214">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="329ab-215">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="329ab-215">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="329ab-216">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="329ab-216">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
