---
title: Hive con strumenti Data Lake (Hadoop) per Visual Studio - Azure HDInsight | Microsoft Docs
description: Informazioni su come usare gli strumenti Data Lake per Visual Studio per eseguire query Apache Hive con Apache Hadoop in Azure HDInsight.
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
ms.openlocfilehash: 3411c59fee73aa2e26a05d70e1dae11cdfc865ff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-the-data-lake-tools-for-visual-studio"></a><span data-ttu-id="d7165-103">Eseguire query Hive usando gli strumenti Data Lake per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d7165-103">Run Hive queries using the Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="d7165-104">Informazioni su come usare gli strumenti Data Lake per Visual Studio per eseguire query su Apache Hive.</span><span class="sxs-lookup"><span data-stu-id="d7165-104">Learn how to use the Data Lake tools for Visual Studio to query Apache Hive.</span></span> <span data-ttu-id="d7165-105">Gli strumenti Data Lake consentono di creare, inviare e monitorare facilmente query Hive in Hadoop in HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="d7165-105">The Data Lake tools allow you to easily create, submit, and monitor Hive queries to Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="d7165-106"><a id="prereq"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d7165-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="d7165-107">Un cluster Azure HDInsight (Hadoop in HDInsight)</span><span class="sxs-lookup"><span data-stu-id="d7165-107">An Azure HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d7165-108">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="d7165-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d7165-109">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d7165-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="d7165-110">Visual Studio (una delle versioni seguenti):</span><span class="sxs-lookup"><span data-stu-id="d7165-110">Visual Studio (one of the following versions):</span></span>

    * <span data-ttu-id="d7165-111">Visual Studio 2013 Community/Professional/Premium/Ultimate con Update 4</span><span class="sxs-lookup"><span data-stu-id="d7165-111">Visual Studio 2013 Community/Professional/Premium/Ultimate with Update 4</span></span>

    * <span data-ttu-id="d7165-112">Visual Studio 2015, qualsiasi edizione</span><span class="sxs-lookup"><span data-stu-id="d7165-112">Visual Studio 2015 (any edition)</span></span>

    * <span data-ttu-id="d7165-113">Visual Studio 2017, qualsiasi edizione</span><span class="sxs-lookup"><span data-stu-id="d7165-113">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="d7165-114">Strumenti HDInsight per Visual Studio o Azure Data Lake Tools per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d7165-114">HDInsight tools for Visual Studio or Azure Data Lake tools for Visual Studio.</span></span> <span data-ttu-id="d7165-115">Vedere [Introduzione all'uso di HDInsight Hadoop Tools per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) per informazioni sull'installazione e la configurazione degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="d7165-115">See [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installing and configuring the tools.</span></span>

## <span data-ttu-id="d7165-116"><a id="run"></a> Eseguire query Hive usando Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d7165-116"><a id="run"></a> Run Hive queries using the Visual Studio</span></span>

1. <span data-ttu-id="d7165-117">Aprire **Visual Studio** e scegliere **Nuovo** > **Progetto** > **Azure Data Lake** > **HIVE** > **Applicazione Hive**.</span><span class="sxs-lookup"><span data-stu-id="d7165-117">Open **Visual Studio** and select **New** > **Project** > **Azure Data Lake** > **HIVE** > **Hive Application**.</span></span> <span data-ttu-id="d7165-118">Specificare un nome per questo progetto.</span><span class="sxs-lookup"><span data-stu-id="d7165-118">Provide a name for this project.</span></span>

2. <span data-ttu-id="d7165-119">Aprire il file **Script.hql** creato con il progetto e incollarvi le seguenti istruzioni HiveQL:</span><span class="sxs-lookup"><span data-stu-id="d7165-119">Open the **Script.hql** file that is created with this project, and paste in the following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    <span data-ttu-id="d7165-120">Di seguito sono elencate le istruzioni che eseguono queste azioni:</span><span class="sxs-lookup"><span data-stu-id="d7165-120">These statements perform the following actions:</span></span>

   * <span data-ttu-id="d7165-121">`DROP TABLE`: se la tabella esiste, questa istruzione la elimina.</span><span class="sxs-lookup"><span data-stu-id="d7165-121">`DROP TABLE`: If the table exists, this statement deletes it.</span></span>

   * <span data-ttu-id="d7165-122">`CREATE EXTERNAL TABLE`: crea una nuova tabella "esterna" in Hive.</span><span class="sxs-lookup"><span data-stu-id="d7165-122">`CREATE EXTERNAL TABLE`: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="d7165-123">Le tabelle esterne archiviano solo la definizione della tabella in Hive. I dati vengono lasciati nella posizione originale.</span><span class="sxs-lookup"><span data-stu-id="d7165-123">External tables only store the table definition in Hive (the data is left in the original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="d7165-124">Usa le tabelle esterne se si prevede che i dati sottostanti verranno aggiornati da un'origine esterna.</span><span class="sxs-lookup"><span data-stu-id="d7165-124">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="d7165-125">Ad esempio, un processo MapReduce o un servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="d7165-125">For example, a MapReduce job or Azure service.</span></span>
     >
     > <span data-ttu-id="d7165-126">L'eliminazione di una tabella esterna **non** comporta anche l'eliminazione dei dati. Viene eliminata solo la definizione della tabella.</span><span class="sxs-lookup"><span data-stu-id="d7165-126">Dropping an external table does **not** delete the data, only the table definition.</span></span>

   * <span data-ttu-id="d7165-127">`ROW FORMAT`: indica a Hive il modo in cui sono formattati i dati.</span><span class="sxs-lookup"><span data-stu-id="d7165-127">`ROW FORMAT`: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="d7165-128">In questo caso, i campi in ogni log sono separati da uno spazio.</span><span class="sxs-lookup"><span data-stu-id="d7165-128">In this case, the fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="d7165-129">`STORED AS TEXTFILE LOCATION`: indica a Hive dove sono archiviati i dati (la directory example/data) e che sono archiviati come testo.</span><span class="sxs-lookup"><span data-stu-id="d7165-129">`STORED AS TEXTFILE LOCATION`: Tells Hive where the data is stored (the example/data directory) and that it is stored as text.</span></span>

   * <span data-ttu-id="d7165-130">`SELECT`: seleziona un numero di tutte le righe in cui la colonna `t4` include il valore `[ERROR]`.</span><span class="sxs-lookup"><span data-stu-id="d7165-130">`SELECT`: Select a count of all rows where column `t4` contains the value `[ERROR]`.</span></span> <span data-ttu-id="d7165-131">L'istruzione dovrebbe restituire un valore pari a `3`, poiché sono presenti tre righe contenenti questo valore.</span><span class="sxs-lookup"><span data-stu-id="d7165-131">This statement returns a value of `3` because there are three rows that contain this value.</span></span>

   * <span data-ttu-id="d7165-132">`INPUT__FILE__NAME LIKE '%.log'`: indica a Hive che si dovrebbero restituire solo i dati da file che terminano con .log.</span><span class="sxs-lookup"><span data-stu-id="d7165-132">`INPUT__FILE__NAME LIKE '%.log'` - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="d7165-133">Questa clausola limita la ricerca al file sample.log che contiene i dati.</span><span class="sxs-lookup"><span data-stu-id="d7165-133">This clause restricts the search to the sample.log file that contains the data.</span></span>

3. <span data-ttu-id="d7165-134">Dalla barra degli strumenti, selezionare il **Cluster HDInsight** che si desidera usare per la query.</span><span class="sxs-lookup"><span data-stu-id="d7165-134">From the toolbar, select the **HDInsight Cluster** that you want to use for this query.</span></span> <span data-ttu-id="d7165-135">Selezionare **Invia** per eseguire le istruzioni come processo Hive.</span><span class="sxs-lookup"><span data-stu-id="d7165-135">Select **Submit** to run the statements as a Hive job.</span></span>

   ![Barra di invio](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. <span data-ttu-id="d7165-137">Verrà visualizzata una finestra di **riepilogo del processo Hive** con informazioni relative al processo in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d7165-137">The **Hive Job Summary** appears and displays information about the running job.</span></span> <span data-ttu-id="d7165-138">Usare il collegamento **Aggiorna** per aggiornare le informazioni del processo finché il campo **Stato processo** non viene impostato su **Completato**.</span><span class="sxs-lookup"><span data-stu-id="d7165-138">Use the **Refresh** link to refresh the job information, until the **Job Status** changes to **Completed**.</span></span>

   ![riepilogo del processo che mostra un processo completato](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. <span data-ttu-id="d7165-140">Usare il collegamento **Output processo** per visualizzare l'output del processo.</span><span class="sxs-lookup"><span data-stu-id="d7165-140">Use the **Job Output** link to view the output of this job.</span></span> <span data-ttu-id="d7165-141">Mostra `[ERROR] 3`, ovvero il valore restituito dalla query.</span><span class="sxs-lookup"><span data-stu-id="d7165-141">It displays `[ERROR] 3`, which is the value returned by this query.</span></span>

6. <span data-ttu-id="d7165-142">È anche possibile eseguire query Hive senza creare un progetto.</span><span class="sxs-lookup"><span data-stu-id="d7165-142">You can also run Hive queries without creating a project.</span></span> <span data-ttu-id="d7165-143">Usando **Esplora server**, espandere **Azure** > **HDInsight**, fare clic con il pulsante destro del mouse sul server HDInsight, quindi scegliere **Scrivi una query Hive**.</span><span class="sxs-lookup"><span data-stu-id="d7165-143">Using **Server Explorer**, expand **Azure** > **HDInsight**, right-click your HDInsight server, and then select **Write a Hive Query**.</span></span>

7. <span data-ttu-id="d7165-144">Nel documento **temp.hql** che viene visualizzato aggiungere le seguenti istruzioni HiveQL:</span><span class="sxs-lookup"><span data-stu-id="d7165-144">In the **temp.hql** document that appears, add the following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    <span data-ttu-id="d7165-145">Di seguito sono elencate le istruzioni che eseguono queste azioni:</span><span class="sxs-lookup"><span data-stu-id="d7165-145">These statements perform the following actions:</span></span>

   * <span data-ttu-id="d7165-146">`CREATE TABLE IF NOT EXISTS`: crea una tabella, se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="d7165-146">`CREATE TABLE IF NOT EXISTS`: Creates a table if it does not already exist.</span></span> <span data-ttu-id="d7165-147">Poiché la parola chiave `EXTERNAL` non viene usata, questa istruzione crea una tabella interna.</span><span class="sxs-lookup"><span data-stu-id="d7165-147">Because the `EXTERNAL` keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="d7165-148">Le tabelle interne vengono archiviate nel data warehouse di Hive e sono gestite da Hive.</span><span class="sxs-lookup"><span data-stu-id="d7165-148">Internal tables are stored in the Hive data warehouse and are managed by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="d7165-149">A differenza delle tabelle `EXTERNAL`, se si elimina una tabella interna, vengono eliminati anche i dati sottostanti.</span><span class="sxs-lookup"><span data-stu-id="d7165-149">Unlike `EXTERNAL` tables, dropping an internal table also deletes the underlying data.</span></span>

   * <span data-ttu-id="d7165-150">`STORED AS ORC`: archivia i dati nel formato ORC, Optimized Row Columnar.</span><span class="sxs-lookup"><span data-stu-id="d7165-150">`STORED AS ORC`: Stores the data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="d7165-151">ORC è un formato altamente ottimizzato ed efficiente per l'archiviazione di dati Hive.</span><span class="sxs-lookup"><span data-stu-id="d7165-151">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="d7165-152">`INSERT OVERWRITE ... SELECT`: seleziona le righe della tabella `log4jLogs` contenenti `[ERROR]`, quindi inserisce i dati nella tabella `errorLogs`.</span><span class="sxs-lookup"><span data-stu-id="d7165-152">`INSERT OVERWRITE ... SELECT`: Selects rows from the `log4jLogs` table that contain `[ERROR]`, then inserts the data into the `errorLogs` table.</span></span>

8. <span data-ttu-id="d7165-153">Nella barra degli strumenti selezionare **Invia** per eseguire il processo.</span><span class="sxs-lookup"><span data-stu-id="d7165-153">From the toolbar, select **Submit** to run the job.</span></span> <span data-ttu-id="d7165-154">Usare **Stato processo** per accertarsi che il processo sia stato completato correttamente.</span><span class="sxs-lookup"><span data-stu-id="d7165-154">Use the **Job Status** to determine that the job has completed successfully.</span></span>

9. <span data-ttu-id="d7165-155">Per verificare che il processo abbia creato la tabella, usare **Esplora server** ed espandere **Azure** > **HDInsight** > il proprio cluster HDInsight > **Database Hive** > **Predefinito**.</span><span class="sxs-lookup"><span data-stu-id="d7165-155">To verify that the job created the table, use **Server Explorer** and expand **Azure** > **HDInsight** > your HDInsight cluster > **Hive Databases** > **default**.</span></span> <span data-ttu-id="d7165-156">Vengono elencate la tabella **errorLogs** e la tabella **log4jLogs**.</span><span class="sxs-lookup"><span data-stu-id="d7165-156">The **errorLogs** table and the **log4jLogs** table are listed.</span></span>

## <span data-ttu-id="d7165-157"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d7165-157"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="d7165-158">Come si può notare, gli strumenti HDInsight per Visual Studio forniscono un modo semplice per lavorare con le query Hive in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d7165-158">As you can see, the HDInsight tools for Visual Studio provide an easy way to work with Hive queries on HDInsight.</span></span>

<span data-ttu-id="d7165-159">Per informazioni generali su Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d7165-159">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="d7165-160">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d7165-160">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="d7165-161">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d7165-161">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="d7165-162">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d7165-162">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

* [<span data-ttu-id="d7165-163">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d7165-163">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="d7165-164">Per altre informazioni su HDInsight Tools per Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="d7165-164">For more information about the HDInsight tools for Visual Studio:</span></span>

* [<span data-ttu-id="d7165-165">Introduzione all'uso di HDInsight Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d7165-165">Getting started with HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md)

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
