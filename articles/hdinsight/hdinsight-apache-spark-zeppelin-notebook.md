---
title: Usare i notebook di Zeppelin con cluster Apache Spark in Azure HDInsight | Documentazione Microsoft
description: Istruzioni dettagliate su come usare i notebook di Zeppelin con cluster Apache Spark in Azure HDInsight.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: df489d70-7788-4efa-a089-e5e5006421e2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 7fe5e3ec68e82945b972d2dd44f2cc3b8cf395d1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="7e578-103">Usare i notebook di Zeppelin con cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e578-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span></span>

<span data-ttu-id="7e578-104">I cluster HDInsight Spark includono notebook Zeppelin che possono essere usati per eseguire processi Spark.</span><span class="sxs-lookup"><span data-stu-id="7e578-104">HDInsight Spark clusters include Zeppelin notebooks that you can use to run Spark jobs.</span></span> <span data-ttu-id="7e578-105">Questo articolo illustra come usare il notebook Zeppelin in un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e578-105">In this article, you learn how to use the Zeppelin notebook on an HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="7e578-106">I notebook Zeppelin sono disponibili solo per Spark 1.6.3 in HDInsight 3.5 e Spark 2.1.0 in HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="7e578-106">Zeppelin notebooks are available only for Spark 1.6.3 on HDInsight 3.5 and Spark 2.1.0 on HDInsight 3.6.</span></span>
>

<span data-ttu-id="7e578-107">**Prerequisiti:**</span><span class="sxs-lookup"><span data-stu-id="7e578-107">**Prerequisites:**</span></span>

* <span data-ttu-id="7e578-108">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e578-108">An Azure subscription.</span></span> <span data-ttu-id="7e578-109">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="7e578-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="7e578-110">Un cluster Apache Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e578-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="7e578-111">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="7e578-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="launch-a-zeppelin-notebook"></a><span data-ttu-id="7e578-112">Avviare un notebook Zeppelin</span><span class="sxs-lookup"><span data-stu-id="7e578-112">Launch a Zeppelin notebook</span></span>
1. <span data-ttu-id="7e578-113">Nel pannello del cluster Spark fare clic su **Dashboard cluster** e quindi su **Notebook di Zeppelin**.</span><span class="sxs-lookup"><span data-stu-id="7e578-113">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span></span> <span data-ttu-id="7e578-114">Se richiesto, immettere le credenziali per il cluster.</span><span class="sxs-lookup"><span data-stu-id="7e578-114">If prompted, enter the admin credentials for the cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7e578-115">È anche possibile raggiungere il notebook di Zeppelin per il cluster aprendo l'URL seguente nel browser.</span><span class="sxs-lookup"><span data-stu-id="7e578-115">You may also reach the Zeppelin Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="7e578-116">Sostituire **CLUSTERNAME** con il nome del cluster:</span><span class="sxs-lookup"><span data-stu-id="7e578-116">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. <span data-ttu-id="7e578-117">Creare un nuovo notebook.</span><span class="sxs-lookup"><span data-stu-id="7e578-117">Create a new notebook.</span></span> <span data-ttu-id="7e578-118">Dal riquadro intestazione fare clic su **Notebook** e quindi su **Create New Note** (Crea una nuova nota).</span><span class="sxs-lookup"><span data-stu-id="7e578-118">From the header pane, click **Notebook**, and then click **Create New Note**.</span></span>
   
    <span data-ttu-id="7e578-119">![Creare un nuovo notebook Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Creare un nuovo notebook Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="7e578-119">![Create a new Zeppelin notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Create a new Zeppelin notebook")</span></span>
   
    <span data-ttu-id="7e578-120">Immettere un nome per il notebook e quindi fare clic su **Create New Note** (Crea una nuova nota).</span><span class="sxs-lookup"><span data-stu-id="7e578-120">Enter a name for the notebook, and then click **Create Note**.</span></span>
3. <span data-ttu-id="7e578-121">Verificare anche che l'intestazione del notebook mostri uno stato connesso,</span><span class="sxs-lookup"><span data-stu-id="7e578-121">Also, make sure the notebook header shows a connected status.</span></span> <span data-ttu-id="7e578-122">indicato da un punto verde nell'angolo superiore destro.</span><span class="sxs-lookup"><span data-stu-id="7e578-122">It is denoted by a green dot in the top-right corner.</span></span>
   
    <span data-ttu-id="7e578-123">![Stato del notebook Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Stato del notebook Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="7e578-123">![Zeppelin notebook status](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notebook status")</span></span>
4. <span data-ttu-id="7e578-124">Caricare i dati di esempio in una tabella temporanea.</span><span class="sxs-lookup"><span data-stu-id="7e578-124">Load sample data into a temporary table.</span></span> <span data-ttu-id="7e578-125">Quando si crea un cluster Spark in HDInsight, il file di dati di esempio, **hvac.csv**, viene copiato nell'account di archiviazione associato in **\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="7e578-125">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span></span>
   
    <span data-ttu-id="7e578-126">Nel paragrafo vuoto creato per impostazione predefinita del nuovo notebook, incollare il frammento di codice riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7e578-126">In the empty paragraph that is created by default in the new notebook, paste the following snippet.</span></span>
   
        %livy.spark
        //The above magic instructs Zeppelin to use the Livy Scala interpreter
   
        // Create an RDD using the default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map the values in the .csv file to the schema
        val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
            s => Hvac(s(0), 
                    s(1),
                    s(2).toInt,
                    s(3).toInt,
                    s(6)
            )
        ).toDF()
   
        // Register as a temporary table called "hvac"
        hvac.registerTempTable("hvac")
   
    <span data-ttu-id="7e578-127">Premere **MAIUSC+INVIO** oppure fare clic sul pulsante **Play** (Riproduci) in modo che il paragrafo esegua il frammento di codice.</span><span class="sxs-lookup"><span data-stu-id="7e578-127">Press **SHIFT + ENTER** or click the **Play** button for the paragraph to run the snippet.</span></span> <span data-ttu-id="7e578-128">Lo stato nell'angolo destro del paragrafo deve passare da PRONTO, IN ATTESA, IN ESECUZIONE, a COMPLETATO.</span><span class="sxs-lookup"><span data-stu-id="7e578-128">The status on the right-corner of the paragraph should progress from READY, PENDING, RUNNING to FINISHED.</span></span> <span data-ttu-id="7e578-129">L'output viene visualizzato nella parte inferiore dello stesso paragrafo.</span><span class="sxs-lookup"><span data-stu-id="7e578-129">The output shows up at the bottom of the same paragraph.</span></span> <span data-ttu-id="7e578-130">Nella schermata è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="7e578-130">The screenshot looks like the following:</span></span>
   
    <span data-ttu-id="7e578-131">![Creare una tabella temporanea dai dati non elaborati](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Creare una tabella temporanea dai dati non elaborati")</span><span class="sxs-lookup"><span data-stu-id="7e578-131">![Create a temporary table from raw data](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Create a temporary table from raw data")</span></span>
   
    <span data-ttu-id="7e578-132">È inoltre possibile fornire un titolo a ogni paragrafo.</span><span class="sxs-lookup"><span data-stu-id="7e578-132">You can also provide a title to each paragraph.</span></span> <span data-ttu-id="7e578-133">Nell'angolo superiore destro fare clic sull'icona **Settings** (Impostazioni) e quindi su **Show title** (Mostra titolo).</span><span class="sxs-lookup"><span data-stu-id="7e578-133">From the right-hand corner, click the **Settings** icon, and then click **Show title**.</span></span>
5. <span data-ttu-id="7e578-134">È ora possibile eseguire istruzioni SQL Spark su tabella **hvac** .</span><span class="sxs-lookup"><span data-stu-id="7e578-134">You can now run Spark SQL statements on the **hvac** table.</span></span> <span data-ttu-id="7e578-135">Incollare la query seguente in un nuovo paragrafo.</span><span class="sxs-lookup"><span data-stu-id="7e578-135">Paste the following query in a new paragraph.</span></span> <span data-ttu-id="7e578-136">La query recupera l'ID dell'edificio e la differenza tra le temperature effettive e quelle di destinazione per ogni edificio in una determinata data.</span><span class="sxs-lookup"><span data-stu-id="7e578-136">The query retrieves the building ID and the difference between the target and actual temperatures for each building on a given date.</span></span> <span data-ttu-id="7e578-137">Premere **MAIUSC + INVIO**.</span><span class="sxs-lookup"><span data-stu-id="7e578-137">Press **SHIFT + ENTER**.</span></span>
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    <span data-ttu-id="7e578-138">L'istruzione **%sql** all'inizio indica al notebook di usare l'interprete Livy Scala.</span><span class="sxs-lookup"><span data-stu-id="7e578-138">The **%sql** statement at the beginning tells the notebook to use the Livy Scala interpreter.</span></span>
   
    <span data-ttu-id="7e578-139">Nella schermata riportata di seguito sono illustrate questo output.</span><span class="sxs-lookup"><span data-stu-id="7e578-139">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="7e578-140">![Eseguire un'istruzione SQL Spark usando il notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Eseguire un'istruzione SQL Spark usando il notebook")</span><span class="sxs-lookup"><span data-stu-id="7e578-140">![Run a Spark SQL statement using the notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Run a Spark SQL statement using the notebook")</span></span>
   
     <span data-ttu-id="7e578-141">Scegliere le opzioni di visualizzazione (evidenziate nel rettangolo) per passare tra diverse rappresentazioni per lo stesso output.</span><span class="sxs-lookup"><span data-stu-id="7e578-141">Click the display options (highlighted in rectangle) to switch between different representations for the same output.</span></span> <span data-ttu-id="7e578-142">Fare clic su **Impostazioni** per scegliere la chiave e i valori nell'output.</span><span class="sxs-lookup"><span data-stu-id="7e578-142">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="7e578-143">La schermata precedente usa **buildingID** come chiave e la media di **temp_diff** come valore.</span><span class="sxs-lookup"><span data-stu-id="7e578-143">The screen capture above uses **buildingID** as the key and the average of **temp_diff** as the value.</span></span>
6. <span data-ttu-id="7e578-144">È inoltre possibile eseguire istruzioni SQL Spark tramite le variabili nella query.</span><span class="sxs-lookup"><span data-stu-id="7e578-144">You can also run Spark SQL statements using variables in the query.</span></span> <span data-ttu-id="7e578-145">Il seguente frammento di codice illustra come definire una variabile **Temp**nella query con i valori possibili che si vuole eseguire.</span><span class="sxs-lookup"><span data-stu-id="7e578-145">The next snippet shows how to define a variable, **Temp**, in the query with the possible values you want to query with.</span></span> <span data-ttu-id="7e578-146">Quando si esegue la query per la prima volta, un elenco a tendina viene popolato automaticamente con i valori specificati per la variabile.</span><span class="sxs-lookup"><span data-stu-id="7e578-146">When you first run the query, a drop-down is automatically populated with the values you specified for the variable.</span></span>
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    <span data-ttu-id="7e578-147">Incollare questo frammento di codice in un nuovo paragrafo e premere **MAIUSC+INVIO**.</span><span class="sxs-lookup"><span data-stu-id="7e578-147">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="7e578-148">Nella schermata riportata di seguito sono illustrate questo output.</span><span class="sxs-lookup"><span data-stu-id="7e578-148">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="7e578-149">![Eseguire un'istruzione SQL Spark usando il notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Eseguire un'istruzione SQL Spark usando il notebook")</span><span class="sxs-lookup"><span data-stu-id="7e578-149">![Run a Spark SQL statement using the notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Run a Spark SQL statement using the notebook")</span></span>
   
    <span data-ttu-id="7e578-150">Per le query successive, è possibile selezionare un nuovo valore dall'elenco a tendina e quindi eseguire nuovamente la query.</span><span class="sxs-lookup"><span data-stu-id="7e578-150">For subsequent queries, you can select a new value from the drop-down and run the query again.</span></span> <span data-ttu-id="7e578-151">Fare clic su **Impostazioni** per scegliere la chiave e i valori nell'output.</span><span class="sxs-lookup"><span data-stu-id="7e578-151">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="7e578-152">La schermata precedente usa **buildingID** come chiave, la media di **temp_diff** come valore e **targettemp** come gruppo.</span><span class="sxs-lookup"><span data-stu-id="7e578-152">The screen capture above uses **buildingID** as the key, the average of **temp_diff** as the value, and **targettemp** as the group.</span></span>
7. <span data-ttu-id="7e578-153">Riavviare l'interprete Livy per uscire dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7e578-153">Restart the Livy interpreter to exit the application.</span></span> <span data-ttu-id="7e578-154">A tale scopo, aprire le impostazioni dell'interprete facendo clic sul nome dell'utente connesso nell'angolo superiore destro e quindi fare clic su **Interpreter** (Interprete).</span><span class="sxs-lookup"><span data-stu-id="7e578-154">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="7e578-155">![Avviare l'interprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Output Hive")</span><span class="sxs-lookup"><span data-stu-id="7e578-155">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
8. <span data-ttu-id="7e578-156">Scorrere fino alle impostazioni dell'interprete e quindi fare clic su **Restart** (Riavvia).</span><span class="sxs-lookup"><span data-stu-id="7e578-156">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="7e578-157">![Riavviare l'interprete Livy](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Riavviare l'interprete Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="7e578-157">![Restart the Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span></span>

## <a name="how-do-i-use-external-packages-with-the-notebook"></a><span data-ttu-id="7e578-158">Come usare pacchetti esterni con il notebook</span><span class="sxs-lookup"><span data-stu-id="7e578-158">How do I use external packages with the notebook?</span></span>
<span data-ttu-id="7e578-159">È possibile configurare il notebook Zeppelin in un cluster Apache Spark in HDInsight (Linux) per l'uso di pacchetti esterni creati dalla community che non sono inclusi come predefiniti nel cluster.</span><span class="sxs-lookup"><span data-stu-id="7e578-159">You can configure the Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) to use external, community-contributed packages that are not included out-of-the-box in the cluster.</span></span> <span data-ttu-id="7e578-160">Per un elenco completo dei pacchetti disponibili, è possibile eseguire ricerche nel [repository Maven](http://search.maven.org/) .</span><span class="sxs-lookup"><span data-stu-id="7e578-160">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span></span> <span data-ttu-id="7e578-161">È anche possibile ottenere un elenco dei pacchetti disponibili da altre origini.</span><span class="sxs-lookup"><span data-stu-id="7e578-161">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="7e578-162">Ad esempio, un elenco completo dei pacchetti creati dalla community è disponibile nel sito Web [spark-packages.org](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="7e578-162">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="7e578-163">Questo articolo illustra come usare il pacchetto [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) con il notebook Jupyter.</span><span class="sxs-lookup"><span data-stu-id="7e578-163">In this article, you will see how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span></span>

1. <span data-ttu-id="7e578-164">Aprire le impostazioni dell'interprete.</span><span class="sxs-lookup"><span data-stu-id="7e578-164">Open interpreter settings.</span></span> <span data-ttu-id="7e578-165">Nell'angolo superiore destro fare clic sul nome dell'utente connesso e quindi su **Interpreter** (Interprete).</span><span class="sxs-lookup"><span data-stu-id="7e578-165">From the top-right corner, click the logged in user name, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="7e578-166">![Avviare l'interprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Output Hive")</span><span class="sxs-lookup"><span data-stu-id="7e578-166">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="7e578-167">Scorrere fino alle impostazioni dell'interprete e quindi fare clic su **Edit** (Modifica).</span><span class="sxs-lookup"><span data-stu-id="7e578-167">Scroll to Livy interpreter settings and then click **Edit**.</span></span>
   
    <span data-ttu-id="7e578-168">![Modificare le impostazioni dell'interprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Modificare le impostazioni dell'interprete")</span><span class="sxs-lookup"><span data-stu-id="7e578-168">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span></span>
3. <span data-ttu-id="7e578-169">Aggiungere una nuova chiave denominata **livy.spark.jars.packages** e impostarne il valore nel formato `group:id:version`.</span><span class="sxs-lookup"><span data-stu-id="7e578-169">Add a new key, called **livy.spark.jars.packages** and set its value in the format `group:id:version`.</span></span> <span data-ttu-id="7e578-170">Se si vuole usare il pacchetto [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar), è quindi necessario impostare il valore della chiave su `com.databricks:spark-csv_2.10:1.4.0`.</span><span class="sxs-lookup"><span data-stu-id="7e578-170">So, if you want to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set the value of the key to `com.databricks:spark-csv_2.10:1.4.0`.</span></span>
   
    <span data-ttu-id="7e578-171">![Modificare le impostazioni dell'interprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Modificare le impostazioni dell'interprete")</span><span class="sxs-lookup"><span data-stu-id="7e578-171">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span></span>
   
    <span data-ttu-id="7e578-172">Fare clic su **Save** (Salva) e quindi riavviare l'interprete Livy.</span><span class="sxs-lookup"><span data-stu-id="7e578-172">Click **Save** and then restart the Livy interpreter.</span></span>
4. <span data-ttu-id="7e578-173">**Suggerimento**: il valore della chiave immesso sopra si determina come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7e578-173">**Tip**: If you want to understand how to arrive at the value of the key entered above, here's how.</span></span>
   
    <span data-ttu-id="7e578-174">a.</span><span class="sxs-lookup"><span data-stu-id="7e578-174">a.</span></span> <span data-ttu-id="7e578-175">Individuare un pacchetto nel repository Maven.</span><span class="sxs-lookup"><span data-stu-id="7e578-175">Locate the package in the Maven Repository.</span></span> <span data-ttu-id="7e578-176">In questa esercitazione è stato usato [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="7e578-176">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="7e578-177">b.</span><span class="sxs-lookup"><span data-stu-id="7e578-177">b.</span></span> <span data-ttu-id="7e578-178">Recuperare dal repository i valori per **GroupId**, **ArtifactId** e **Version**.</span><span class="sxs-lookup"><span data-stu-id="7e578-178">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span></span>
   
    <span data-ttu-id="7e578-179">![Usare pacchetti esterni con notebook di Jupyter](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Usare pacchetti esterni con notebook di Jupyter")</span><span class="sxs-lookup"><span data-stu-id="7e578-179">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="7e578-180">c.</span><span class="sxs-lookup"><span data-stu-id="7e578-180">c.</span></span> <span data-ttu-id="7e578-181">Concatenare i tre valori, separati da due punti (**:**).</span><span class="sxs-lookup"><span data-stu-id="7e578-181">Concatenate the three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-the-zeppelin-notebooks-saved"></a><span data-ttu-id="7e578-182">Posizione di salvataggio dei notebook Zeppelin</span><span class="sxs-lookup"><span data-stu-id="7e578-182">Where are the Zeppelin notebooks saved?</span></span>
<span data-ttu-id="7e578-183">I notebook Zeppelin vengono salvati nei nodi head del cluster.</span><span class="sxs-lookup"><span data-stu-id="7e578-183">The Zeppelin notebooks are saved to the cluster headnodes.</span></span> <span data-ttu-id="7e578-184">Se si elimina il cluster, verranno quindi eliminati anche i notebook.</span><span class="sxs-lookup"><span data-stu-id="7e578-184">So, if you delete the cluster, the notebooks will be deleted as well.</span></span> <span data-ttu-id="7e578-185">Se si vogliono mantenere i notebook per usarli successivamente in altri cluster, è necessario esportarli al termine dell'esecuzione dei processi.</span><span class="sxs-lookup"><span data-stu-id="7e578-185">If you want to preserve your notebooks for later use on other clusters, you must export them after you have finished running the jobs.</span></span> <span data-ttu-id="7e578-186">Per esportare un notebook, fare clic sull'icona di **esportazione** come illustrato nell'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="7e578-186">To export a notebook, click the **Export** icon as shown in the image below.</span></span>

<span data-ttu-id="7e578-187">![Scaricare notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Scaricare il notebook")</span><span class="sxs-lookup"><span data-stu-id="7e578-187">![Download notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download the notebook")</span></span>

<span data-ttu-id="7e578-188">Il notebook verrà così salvato come file JSON nel percorso di download dell'utente.</span><span class="sxs-lookup"><span data-stu-id="7e578-188">This saves the notebook as a JSON file in your download location.</span></span>

## <a name="livy-session-management"></a><span data-ttu-id="7e578-189">Gestione delle sessioni di Livy</span><span class="sxs-lookup"><span data-stu-id="7e578-189">Livy session management</span></span>
<span data-ttu-id="7e578-190">Quando si esegue il primo paragrafo di codice nel notebook Zeppelin, nel cluster HDInsight Spark viene creata una nuova sessione di Livy.</span><span class="sxs-lookup"><span data-stu-id="7e578-190">When you run the first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span></span> <span data-ttu-id="7e578-191">Tale sessione sarà condivisa da tutti i notebook Zeppelin creati successivamente.</span><span class="sxs-lookup"><span data-stu-id="7e578-191">This session is shared across all Zeppelin notebooks that you subsequently create.</span></span> <span data-ttu-id="7e578-192">Se la sessione di Livy viene terminata per qualche motivo (riavvio del cluster e così via), non sarà possibile eseguire processi dal notebook Zeppelin.</span><span class="sxs-lookup"><span data-stu-id="7e578-192">If for some reason the Livy session is killed (cluster reboot, etc.), you will not be able to run jobs from the Zeppelin notebook.</span></span>

<span data-ttu-id="7e578-193">In tal caso, per poter eseguire processi dal notebook Zeppelin è prima necessario seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="7e578-193">In such a case, you must perform the following steps before you can start running jobs from a Zeppelin notebook.</span></span> 

1. <span data-ttu-id="7e578-194">Riavviare l'interprete Livy dal notebook Zeppelin.</span><span class="sxs-lookup"><span data-stu-id="7e578-194">Restart the Livy interpreter from the Zeppelin notebook.</span></span> <span data-ttu-id="7e578-195">A tale scopo, aprire le impostazioni dell'interprete facendo clic sul nome dell'utente connesso nell'angolo superiore destro e quindi fare clic su **Interpreter** (Interprete).</span><span class="sxs-lookup"><span data-stu-id="7e578-195">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="7e578-196">![Avviare l'interprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Output Hive")</span><span class="sxs-lookup"><span data-stu-id="7e578-196">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="7e578-197">Scorrere fino alle impostazioni dell'interprete e quindi fare clic su **Restart** (Riavvia).</span><span class="sxs-lookup"><span data-stu-id="7e578-197">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="7e578-198">![Riavviare l'interprete Livy](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Riavviare l'interprete Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="7e578-198">![Restart the Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span></span>
3. <span data-ttu-id="7e578-199">Eseguire una cella di codice da un notebook Zeppelin esistente.</span><span class="sxs-lookup"><span data-stu-id="7e578-199">Run a code cell from an existing Zeppelin notebook.</span></span> <span data-ttu-id="7e578-200">Verrà così creata una nuova sessione di Livy nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e578-200">This creates a new Livy session in the HDInsight cluster.</span></span>

## <span data-ttu-id="7e578-201"><a name="seealso"></a>Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7e578-201"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="7e578-202">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e578-202">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="7e578-203">Scenari</span><span class="sxs-lookup"><span data-stu-id="7e578-203">Scenarios</span></span>
* [<span data-ttu-id="7e578-204">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e578-204">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="7e578-205">Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC</span><span class="sxs-lookup"><span data-stu-id="7e578-205">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="7e578-206">Spark con Machine Learning: usare Spark in HDInsight per prevedere i risultati del controllo degli alimenti</span><span class="sxs-lookup"><span data-stu-id="7e578-206">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="7e578-207">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="7e578-207">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="7e578-208">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e578-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="7e578-209">Creare ed eseguire applicazioni</span><span class="sxs-lookup"><span data-stu-id="7e578-209">Create and run applications</span></span>
* [<span data-ttu-id="7e578-210">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="7e578-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="7e578-211">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="7e578-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="7e578-212">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="7e578-212">Tools and extensions</span></span>
* [<span data-ttu-id="7e578-213">Usare il plug-in degli strumenti HDInsight per IntelliJ IDEA per creare e inviare applicazioni Spark in Scala</span><span class="sxs-lookup"><span data-stu-id="7e578-213">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="7e578-214">Utilizzare il plug-in Strumenti HDInsight per IntelliJ IDEA per eseguire il debug di applicazioni Spark in remoto</span><span class="sxs-lookup"><span data-stu-id="7e578-214">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="7e578-215">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e578-215">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="7e578-216">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="7e578-216">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="7e578-217">Installare Jupyter Notebook nel computer e connetterlo a un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="7e578-217">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="7e578-218">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="7e578-218">Manage resources</span></span>
* [<span data-ttu-id="7e578-219">Gestire le risorse del cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e578-219">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="7e578-220">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e578-220">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







