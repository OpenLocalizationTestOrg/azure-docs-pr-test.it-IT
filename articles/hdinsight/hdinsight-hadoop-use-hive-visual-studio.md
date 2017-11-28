---
title: aaaHive con gli strumenti di Data Lake (Hadoop) per Visual Studio - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toouse hello Data Lake tools per Visual Studio toorun Apache Hive query con Apache Hadoop in HDInsight di Azure.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2b3e672a-1195-4fa5-afb7-b7b73937bfbe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: dc76974c02cf68bcf701b2b155842c9e9c5cb988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-data-lake-tools-for-visual-studio"></a><span data-ttu-id="1444a-103">Esecuzione di query Hive con strumenti di Data Lake hello per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1444a-103">Run Hive queries using hello Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="1444a-104">Informazioni su come toouse hello Data Lake strumenti per Apache Hive tooquery di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1444a-104">Learn how toouse hello Data Lake tools for Visual Studio tooquery Apache Hive.</span></span> <span data-ttu-id="1444a-105">gli strumenti di Data Lake Hello consentono tooeasily creare, inviare e monitorare tooHadoop query Hive in HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="1444a-105">hello Data Lake tools allow you tooeasily create, submit, and monitor Hive queries tooHadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="1444a-106"><a id="prereq"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1444a-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="1444a-107">Un cluster Azure HDInsight (Hadoop in HDInsight)</span><span class="sxs-lookup"><span data-stu-id="1444a-107">An Azure HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="1444a-108">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="1444a-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1444a-109">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1444a-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="1444a-110">Visual Studio (una delle seguenti versioni di hello):</span><span class="sxs-lookup"><span data-stu-id="1444a-110">Visual Studio (one of hello following versions):</span></span>

    * <span data-ttu-id="1444a-111">Visual Studio 2013 Community/Professional/Premium/Ultimate con Update 4</span><span class="sxs-lookup"><span data-stu-id="1444a-111">Visual Studio 2013 Community/Professional/Premium/Ultimate with Update 4</span></span>

    * <span data-ttu-id="1444a-112">Visual Studio 2015, qualsiasi edizione</span><span class="sxs-lookup"><span data-stu-id="1444a-112">Visual Studio 2015 (any edition)</span></span>

    * <span data-ttu-id="1444a-113">Visual Studio 2017, qualsiasi edizione</span><span class="sxs-lookup"><span data-stu-id="1444a-113">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="1444a-114">Strumenti HDInsight per Visual Studio o Azure Data Lake Tools per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1444a-114">HDInsight tools for Visual Studio or Azure Data Lake tools for Visual Studio.</span></span> <span data-ttu-id="1444a-115">Vedere [iniziare a usare gli strumenti di Visual Studio Hadoop per HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) per informazioni sull'installazione e configurazione di strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="1444a-115">See [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installing and configuring hello tools.</span></span>

## <span data-ttu-id="1444a-116"><a id="run"></a>Esecuzione di query Hive utilizzando hello Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1444a-116"><a id="run"></a> Run Hive queries using hello Visual Studio</span></span>

1. <span data-ttu-id="1444a-117">Aprire **Visual Studio** e scegliere **Nuovo** > **Progetto** > **Azure Data Lake** > **HIVE** > **Applicazione Hive**.</span><span class="sxs-lookup"><span data-stu-id="1444a-117">Open **Visual Studio** and select **New** > **Project** > **Azure Data Lake** > **HIVE** > **Hive Application**.</span></span> <span data-ttu-id="1444a-118">Specificare un nome per questo progetto.</span><span class="sxs-lookup"><span data-stu-id="1444a-118">Provide a name for this project.</span></span>

2. <span data-ttu-id="1444a-119">Aprire hello **Script.hql** file che viene creato con questo progetto e Incolla in hello seguendo le istruzioni HiveQL:</span><span class="sxs-lookup"><span data-stu-id="1444a-119">Open hello **Script.hql** file that is created with this project, and paste in hello following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    <span data-ttu-id="1444a-120">Queste istruzioni consentono di eseguire hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="1444a-120">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="1444a-121">`DROP TABLE`: Hello tabella esiste, questa istruzione eliminata.</span><span class="sxs-lookup"><span data-stu-id="1444a-121">`DROP TABLE`: If hello table exists, this statement deletes it.</span></span>

   * <span data-ttu-id="1444a-122">`CREATE EXTERNAL TABLE`: crea una nuova tabella "esterna" in Hive.</span><span class="sxs-lookup"><span data-stu-id="1444a-122">`CREATE EXTERNAL TABLE`: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="1444a-123">Le tabelle esterne archiviano solo la definizione di tabella hello nell'Hive (Buongiorno dati viene lasciati nella posizione originale hello).</span><span class="sxs-lookup"><span data-stu-id="1444a-123">External tables only store hello table definition in Hive (hello data is left in hello original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="1444a-124">Le tabelle esterne da utilizzare quando si prevede di hello sottostante toobe dati aggiornati da un'origine esterna.</span><span class="sxs-lookup"><span data-stu-id="1444a-124">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="1444a-125">Ad esempio, un processo MapReduce o un servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="1444a-125">For example, a MapReduce job or Azure service.</span></span>
     >
     > <span data-ttu-id="1444a-126">Eliminazione di una tabella esterna **non** eliminare dati hello e definizione della tabella solo hello.</span><span class="sxs-lookup"><span data-stu-id="1444a-126">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

   * <span data-ttu-id="1444a-127">`ROW FORMAT`: Indica la formattazione di dati hello Hive.</span><span class="sxs-lookup"><span data-stu-id="1444a-127">`ROW FORMAT`: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="1444a-128">In questo caso, i campi di hello in ogni log sono separati da uno spazio.</span><span class="sxs-lookup"><span data-stu-id="1444a-128">In this case, hello fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="1444a-129">`STORED AS TEXTFILE LOCATION`: Indica Hive dove hello memorizzati (directory dati di esempio/hello) e a cui è archiviato come testo.</span><span class="sxs-lookup"><span data-stu-id="1444a-129">`STORED AS TEXTFILE LOCATION`: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>

   * <span data-ttu-id="1444a-130">`SELECT`: Selezionare un conteggio di tutte le righe in cui colonna `t4` contiene il valore di hello `[ERROR]`.</span><span class="sxs-lookup"><span data-stu-id="1444a-130">`SELECT`: Select a count of all rows where column `t4` contains hello value `[ERROR]`.</span></span> <span data-ttu-id="1444a-131">L'istruzione dovrebbe restituire un valore pari a `3`, poiché sono presenti tre righe contenenti questo valore.</span><span class="sxs-lookup"><span data-stu-id="1444a-131">This statement returns a value of `3` because there are three rows that contain this value.</span></span>

   * <span data-ttu-id="1444a-132">`INPUT__FILE__NAME LIKE '%.log'`: indica a Hive che si dovrebbero restituire solo i dati da file che terminano con .log.</span><span class="sxs-lookup"><span data-stu-id="1444a-132">`INPUT__FILE__NAME LIKE '%.log'` - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="1444a-133">Questa clausola limita hello toohello sample.log file di ricerca contiene dati hello.</span><span class="sxs-lookup"><span data-stu-id="1444a-133">This clause restricts hello search toohello sample.log file that contains hello data.</span></span>

3. <span data-ttu-id="1444a-134">Dalla barra degli strumenti hello, selezionare hello **HDInsight Cluster** che si desidera toouse per questa query.</span><span class="sxs-lookup"><span data-stu-id="1444a-134">From hello toolbar, select hello **HDInsight Cluster** that you want toouse for this query.</span></span> <span data-ttu-id="1444a-135">Selezionare **Invia** istruzioni hello toorun come un processo Hive.</span><span class="sxs-lookup"><span data-stu-id="1444a-135">Select **Submit** toorun hello statements as a Hive job.</span></span>

   ![Barra di invio](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. <span data-ttu-id="1444a-137">Hello **Hive riepilogo** viene visualizzata e visualizza le informazioni sull'esecuzione del processo hello.</span><span class="sxs-lookup"><span data-stu-id="1444a-137">hello **Hive Job Summary** appears and displays information about hello running job.</span></span> <span data-ttu-id="1444a-138">Hello utilizzare **aggiornamento** collegamento toorefresh hello informazioni sul processo finché hello **lo stato del processo** cambia troppo**completato**.</span><span class="sxs-lookup"><span data-stu-id="1444a-138">Use hello **Refresh** link toorefresh hello job information, until hello **Job Status** changes too**Completed**.</span></span>

   ![riepilogo del processo che mostra un processo completato](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. <span data-ttu-id="1444a-140">Hello utilizzare **Output processo** collegamento di output di hello tooview del processo.</span><span class="sxs-lookup"><span data-stu-id="1444a-140">Use hello **Job Output** link tooview hello output of this job.</span></span> <span data-ttu-id="1444a-141">Visualizza `[ERROR] 3`, ovvero il valore di hello restituito dalla query.</span><span class="sxs-lookup"><span data-stu-id="1444a-141">It displays `[ERROR] 3`, which is hello value returned by this query.</span></span>

6. <span data-ttu-id="1444a-142">È anche possibile eseguire query Hive senza creare un progetto.</span><span class="sxs-lookup"><span data-stu-id="1444a-142">You can also run Hive queries without creating a project.</span></span> <span data-ttu-id="1444a-143">Usando **Esplora server**, espandere **Azure** > **HDInsight**, fare clic con il pulsante destro del mouse sul server HDInsight, quindi scegliere **Scrivi una query Hive**.</span><span class="sxs-lookup"><span data-stu-id="1444a-143">Using **Server Explorer**, expand **Azure** > **HDInsight**, right-click your HDInsight server, and then select **Write a Hive Query**.</span></span>

7. <span data-ttu-id="1444a-144">In hello **temp.hql** documento che viene visualizzata, aggiungere hello seguendo le istruzioni HiveQL:</span><span class="sxs-lookup"><span data-stu-id="1444a-144">In hello **temp.hql** document that appears, add hello following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    <span data-ttu-id="1444a-145">Queste istruzioni consentono di eseguire hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="1444a-145">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="1444a-146">`CREATE TABLE IF NOT EXISTS`: crea una tabella, se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="1444a-146">`CREATE TABLE IF NOT EXISTS`: Creates a table if it does not already exist.</span></span> <span data-ttu-id="1444a-147">Poiché hello `EXTERNAL` parola chiave non viene utilizzato, l'istruzione seguente crea una tabella interna.</span><span class="sxs-lookup"><span data-stu-id="1444a-147">Because hello `EXTERNAL` keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="1444a-148">Le tabelle interne vengono archiviate nel data warehouse di hello Hive e vengono gestite dall'Hive.</span><span class="sxs-lookup"><span data-stu-id="1444a-148">Internal tables are stored in hello Hive data warehouse and are managed by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="1444a-149">A differenza di `EXTERNAL` tabelle, anche l'eliminazione di una tabella interna Elimina hello dati sottostanti.</span><span class="sxs-lookup"><span data-stu-id="1444a-149">Unlike `EXTERNAL` tables, dropping an internal table also deletes hello underlying data.</span></span>

   * <span data-ttu-id="1444a-150">`STORED AS ORC`: Archivia hello dati in formato di riga con ottimizzazione per la colonna (ORC).</span><span class="sxs-lookup"><span data-stu-id="1444a-150">`STORED AS ORC`: Stores hello data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="1444a-151">ORC è un formato altamente ottimizzato ed efficiente per l'archiviazione di dati Hive.</span><span class="sxs-lookup"><span data-stu-id="1444a-151">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="1444a-152">`INSERT OVERWRITE ... SELECT`: Consente di selezionare le righe da hello `log4jLogs` tabella contenenti `[ERROR]`, quindi inserisce dati di hello in hello `errorLogs` tabella.</span><span class="sxs-lookup"><span data-stu-id="1444a-152">`INSERT OVERWRITE ... SELECT`: Selects rows from hello `log4jLogs` table that contain `[ERROR]`, then inserts hello data into hello `errorLogs` table.</span></span>

8. <span data-ttu-id="1444a-153">Dalla barra degli strumenti hello, selezionare **Invia** processo hello toorun.</span><span class="sxs-lookup"><span data-stu-id="1444a-153">From hello toolbar, select **Submit** toorun hello job.</span></span> <span data-ttu-id="1444a-154">Hello utilizzare **lo stato del processo** toodetermine processo hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="1444a-154">Use hello **Job Status** toodetermine that hello job has completed successfully.</span></span>

9. <span data-ttu-id="1444a-155">tooverify che hello processo creato tabella hello, utilizzare **Esplora Server** espandere **Azure** > **HDInsight** > cluster HDInsight > **Database hive** > **predefinito**.</span><span class="sxs-lookup"><span data-stu-id="1444a-155">tooverify that hello job created hello table, use **Server Explorer** and expand **Azure** > **HDInsight** > your HDInsight cluster > **Hive Databases** > **default**.</span></span> <span data-ttu-id="1444a-156">Hello **degli errori** tabella e hello **log4jLogs** sono elencati nella tabella.</span><span class="sxs-lookup"><span data-stu-id="1444a-156">hello **errorLogs** table and hello **log4jLogs** table are listed.</span></span>

## <span data-ttu-id="1444a-157"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1444a-157"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="1444a-158">Come si può notare, gli strumenti di HDInsight hello per Visual Studio forniscono un modo semplice di toowork con query Hive in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1444a-158">As you can see, hello HDInsight tools for Visual Studio provide an easy way toowork with Hive queries on HDInsight.</span></span>

<span data-ttu-id="1444a-159">Per informazioni generali su Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1444a-159">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="1444a-160">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1444a-160">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="1444a-161">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1444a-161">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="1444a-162">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1444a-162">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

* [<span data-ttu-id="1444a-163">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1444a-163">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="1444a-164">Per ulteriori informazioni sugli strumenti di HDInsight hello per Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="1444a-164">For more information about hello HDInsight tools for Visual Studio:</span></span>

* [<span data-ttu-id="1444a-165">Introduzione all'uso di HDInsight Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1444a-165">Getting started with HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx

[image-hdi-hive-powershell]: ./media/hdinsight-use-hive/HDI.HIVE.PowerShell.png
[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
[image-hdi-hive-architecture]: ./media/hdinsight-use-hive/HDI.Hive.Architecture.png
