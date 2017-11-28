---
title: cluster notebook Zeppelin aaaUse con Apache Spark in HDInsight di Azure | Documenti Microsoft
description: Istruzioni dettagliate su come cluster di notebook Zeppelin toouse con Apache Spark in HDInsight di Azure.
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
ms.openlocfilehash: 3ab479cfccc7fd38a9bf6a9fb4f5928beec8ff7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="73f8b-103">Usare i notebook di Zeppelin con cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="73f8b-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span></span>

<span data-ttu-id="73f8b-104">I cluster di HDInsight Spark sono notebook Zeppelin che è possibile utilizzare i processi di Spark toorun.</span><span class="sxs-lookup"><span data-stu-id="73f8b-104">HDInsight Spark clusters include Zeppelin notebooks that you can use toorun Spark jobs.</span></span> <span data-ttu-id="73f8b-105">In questo articolo viene illustrato come toouse hello notebook Zeppelin in un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="73f8b-105">In this article, you learn how toouse hello Zeppelin notebook on an HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="73f8b-106">I notebook Zeppelin sono disponibili solo per Spark 1.6.3 in HDInsight 3.5 e Spark 2.1.0 in HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="73f8b-106">Zeppelin notebooks are available only for Spark 1.6.3 on HDInsight 3.5 and Spark 2.1.0 on HDInsight 3.6.</span></span>
>

<span data-ttu-id="73f8b-107">**Prerequisiti:**</span><span class="sxs-lookup"><span data-stu-id="73f8b-107">**Prerequisites:**</span></span>

* <span data-ttu-id="73f8b-108">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="73f8b-108">An Azure subscription.</span></span> <span data-ttu-id="73f8b-109">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="73f8b-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="73f8b-110">Un cluster Apache Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="73f8b-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="73f8b-111">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="73f8b-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="launch-a-zeppelin-notebook"></a><span data-ttu-id="73f8b-112">Avviare un notebook Zeppelin</span><span class="sxs-lookup"><span data-stu-id="73f8b-112">Launch a Zeppelin notebook</span></span>
1. <span data-ttu-id="73f8b-113">Dal Pannello di cluster Spark hello, fare clic su **Dashboard Cluster**, quindi fare clic su **Zeppelin Notebook**.</span><span class="sxs-lookup"><span data-stu-id="73f8b-113">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span></span> <span data-ttu-id="73f8b-114">Se richiesto, immettere le credenziali di amministratore hello cluster hello.</span><span class="sxs-lookup"><span data-stu-id="73f8b-114">If prompted, enter hello admin credentials for hello cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="73f8b-115">È anche possibile raggiungere hello Notebook Zeppelin per il cluster usando hello apertura URL seguente nel browser.</span><span class="sxs-lookup"><span data-stu-id="73f8b-115">You may also reach hello Zeppelin Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="73f8b-116">Sostituire **CLUSTERNAME** con nome hello del cluster:</span><span class="sxs-lookup"><span data-stu-id="73f8b-116">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. <span data-ttu-id="73f8b-117">Creare un nuovo notebook.</span><span class="sxs-lookup"><span data-stu-id="73f8b-117">Create a new notebook.</span></span> <span data-ttu-id="73f8b-118">Riquadro intestazione hello fare clic su **Notebook**, quindi fare clic su **Crea nuova nota**.</span><span class="sxs-lookup"><span data-stu-id="73f8b-118">From hello header pane, click **Notebook**, and then click **Create New Note**.</span></span>
   
    <span data-ttu-id="73f8b-119">![Creare un nuovo notebook Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Creare un nuovo notebook Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="73f8b-119">![Create a new Zeppelin notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Create a new Zeppelin notebook")</span></span>
   
    <span data-ttu-id="73f8b-120">Immettere un nome per notebook hello e quindi fare clic su **Crea nota**.</span><span class="sxs-lookup"><span data-stu-id="73f8b-120">Enter a name for hello notebook, and then click **Create Note**.</span></span>
3. <span data-ttu-id="73f8b-121">Assicurarsi inoltre che l'intestazione di blocco per Appunti hello Mostra lo stato connesso.</span><span class="sxs-lookup"><span data-stu-id="73f8b-121">Also, make sure hello notebook header shows a connected status.</span></span> <span data-ttu-id="73f8b-122">Viene indicato da un punto verde nell'angolo superiore destro di hello.</span><span class="sxs-lookup"><span data-stu-id="73f8b-122">It is denoted by a green dot in hello top-right corner.</span></span>
   
    <span data-ttu-id="73f8b-123">![Stato del notebook Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Stato del notebook Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="73f8b-123">![Zeppelin notebook status](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notebook status")</span></span>
4. <span data-ttu-id="73f8b-124">Caricare i dati di esempio in una tabella temporanea.</span><span class="sxs-lookup"><span data-stu-id="73f8b-124">Load sample data into a temporary table.</span></span> <span data-ttu-id="73f8b-125">Quando si crea un cluster Spark in HDInsight, file di dati di esempio hello, **hvac.csv**, account di archiviazione toohello copiato associata in **\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="73f8b-125">When you create a Spark cluster in HDInsight, hello sample data file, **hvac.csv**, is copied toohello associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span></span>
   
    <span data-ttu-id="73f8b-126">Nel paragrafo vuoto hello creata per impostazione predefinita nel nuovo notebook hello, incollare hello seguente frammento di codice.</span><span class="sxs-lookup"><span data-stu-id="73f8b-126">In hello empty paragraph that is created by default in hello new notebook, paste hello following snippet.</span></span>
   
        %livy.spark
        //hello above magic instructs Zeppelin toouse hello Livy Scala interpreter
   
        // Create an RDD using hello default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map hello values in hello .csv file toohello schema
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
   
    <span data-ttu-id="73f8b-127">Premere **MAIUSC + INVIO** oppure fare clic su hello **riprodurre** pulsante per frammento di codice hello paragrafo toorun hello.</span><span class="sxs-lookup"><span data-stu-id="73f8b-127">Press **SHIFT + ENTER** or click hello **Play** button for hello paragraph toorun hello snippet.</span></span> <span data-ttu-id="73f8b-128">stato Hello nell'angolo destro hello di paragrafo hello deve sullo stato di avanzamento da pronto, in sospeso, tooFINISHED in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="73f8b-128">hello status on hello right-corner of hello paragraph should progress from READY, PENDING, RUNNING tooFINISHED.</span></span> <span data-ttu-id="73f8b-129">output di Hello viene visualizzato nella parte inferiore di hello di hello stesso paragraph.</span><span class="sxs-lookup"><span data-stu-id="73f8b-129">hello output shows up at hello bottom of hello same paragraph.</span></span> <span data-ttu-id="73f8b-130">schermata di Hello è simile hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="73f8b-130">hello screenshot looks like hello following:</span></span>
   
    <span data-ttu-id="73f8b-131">![Creare una tabella temporanea dai dati non elaborati](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Creare una tabella temporanea dai dati non elaborati")</span><span class="sxs-lookup"><span data-stu-id="73f8b-131">![Create a temporary table from raw data](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Create a temporary table from raw data")</span></span>
   
    <span data-ttu-id="73f8b-132">È anche possibile fornire un paragrafo tooeach titolo.</span><span class="sxs-lookup"><span data-stu-id="73f8b-132">You can also provide a title tooeach paragraph.</span></span> <span data-ttu-id="73f8b-133">Nell'angolo destro hello, fare clic su hello **impostazioni** icona e quindi fare clic su **Mostra titolo**.</span><span class="sxs-lookup"><span data-stu-id="73f8b-133">From hello right-hand corner, click hello **Settings** icon, and then click **Show title**.</span></span>
5. <span data-ttu-id="73f8b-134">È ora possibile eseguire istruzioni SQL Spark in hello **impianto** tabella.</span><span class="sxs-lookup"><span data-stu-id="73f8b-134">You can now run Spark SQL statements on hello **hvac** table.</span></span> <span data-ttu-id="73f8b-135">Incollare hello seguente query in un nuovo paragrafo.</span><span class="sxs-lookup"><span data-stu-id="73f8b-135">Paste hello following query in a new paragraph.</span></span> <span data-ttu-id="73f8b-136">Hello query recupera l'ID compilazione hello e hello differenza destinazione hello e temperature effettive per ogni compilazione in una determinata data.</span><span class="sxs-lookup"><span data-stu-id="73f8b-136">hello query retrieves hello building ID and hello difference between hello target and actual temperatures for each building on a given date.</span></span> <span data-ttu-id="73f8b-137">Premere **MAIUSC + INVIO**.</span><span class="sxs-lookup"><span data-stu-id="73f8b-137">Press **SHIFT + ENTER**.</span></span>
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    <span data-ttu-id="73f8b-138">Hello **sql %** istruzione all'inizio di hello indica interprete di hello notebook toouse hello inserire il Scala.</span><span class="sxs-lookup"><span data-stu-id="73f8b-138">hello **%sql** statement at hello beginning tells hello notebook toouse hello Livy Scala interpreter.</span></span>
   
    <span data-ttu-id="73f8b-139">Hello seguente schermata Mostra output di hello.</span><span class="sxs-lookup"><span data-stu-id="73f8b-139">hello following screenshot shows hello output.</span></span>
   
    <span data-ttu-id="73f8b-140">![Esecuzione di un'istruzione SQL Spark utilizzando blocco note hello](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "eseguire un'istruzione SQL Spark utilizzando blocco note hello")</span><span class="sxs-lookup"><span data-stu-id="73f8b-140">![Run a Spark SQL statement using hello notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Run a Spark SQL statement using hello notebook")</span></span>
   
     <span data-ttu-id="73f8b-141">Fare clic su hello visualizzazione Opzioni (evidenziato nel rettangolo) tooswitch tra diverse rappresentazioni per hello stesso output.</span><span class="sxs-lookup"><span data-stu-id="73f8b-141">Click hello display options (highlighted in rectangle) tooswitch between different representations for hello same output.</span></span> <span data-ttu-id="73f8b-142">Fare clic su **impostazioni** toochoose quali costituiscono hello chiave e i valori nell'output di hello.</span><span class="sxs-lookup"><span data-stu-id="73f8b-142">Click **Settings** toochoose what consitutes hello key and values in hello output.</span></span> <span data-ttu-id="73f8b-143">acquisizione schermo precedente viene Hello **buildingID** come chiave di hello e Media hello di **temp_diff** come valore di hello.</span><span class="sxs-lookup"><span data-stu-id="73f8b-143">hello screen capture above uses **buildingID** as hello key and hello average of **temp_diff** as hello value.</span></span>
6. <span data-ttu-id="73f8b-144">È inoltre possibile eseguire istruzioni SQL Spark utilizzo di variabili nelle query hello.</span><span class="sxs-lookup"><span data-stu-id="73f8b-144">You can also run Spark SQL statements using variables in hello query.</span></span> <span data-ttu-id="73f8b-145">Hello successivo illustrato frammento di codice come una variabile, toodefine **Temp**, in query hello con i valori possibili hello desiderato tooquery con.</span><span class="sxs-lookup"><span data-stu-id="73f8b-145">hello next snippet shows how toodefine a variable, **Temp**, in hello query with hello possible values you want tooquery with.</span></span> <span data-ttu-id="73f8b-146">Quando si esegue prima query hello, un elenco a discesa viene popolato automaticamente con i valori hello specificato per la variabile hello.</span><span class="sxs-lookup"><span data-stu-id="73f8b-146">When you first run hello query, a drop-down is automatically populated with hello values you specified for hello variable.</span></span>
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    <span data-ttu-id="73f8b-147">Incollare questo frammento di codice in un nuovo paragrafo e premere **MAIUSC+INVIO**.</span><span class="sxs-lookup"><span data-stu-id="73f8b-147">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="73f8b-148">Hello seguente schermata Mostra output di hello.</span><span class="sxs-lookup"><span data-stu-id="73f8b-148">hello following screenshot shows hello output.</span></span>
   
    <span data-ttu-id="73f8b-149">![Esecuzione di un'istruzione SQL Spark utilizzando blocco note hello](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "eseguire un'istruzione SQL Spark utilizzando blocco note hello")</span><span class="sxs-lookup"><span data-stu-id="73f8b-149">![Run a Spark SQL statement using hello notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Run a Spark SQL statement using hello notebook")</span></span>
   
    <span data-ttu-id="73f8b-150">Per le query successive, è possibile selezionare un nuovo valore dall'elenco a discesa hello e rieseguire la query hello.</span><span class="sxs-lookup"><span data-stu-id="73f8b-150">For subsequent queries, you can select a new value from hello drop-down and run hello query again.</span></span> <span data-ttu-id="73f8b-151">Fare clic su **impostazioni** toochoose quali costituiscono hello chiave e i valori nell'output di hello.</span><span class="sxs-lookup"><span data-stu-id="73f8b-151">Click **Settings** toochoose what consitutes hello key and values in hello output.</span></span> <span data-ttu-id="73f8b-152">Hello acquisizione schermo precedente viene **buildingID** come chiave hello, hello medio di **temp_diff** come valore hello e **targettemp** come gruppo hello.</span><span class="sxs-lookup"><span data-stu-id="73f8b-152">hello screen capture above uses **buildingID** as hello key, hello average of **temp_diff** as hello value, and **targettemp** as hello group.</span></span>
7. <span data-ttu-id="73f8b-153">Riavviare l'applicazione hello tooexit interprete di inserire il hello.</span><span class="sxs-lookup"><span data-stu-id="73f8b-153">Restart hello Livy interpreter tooexit hello application.</span></span> <span data-ttu-id="73f8b-154">In tal caso, aprire le impostazioni di interprete facendo hello connesso in nome utente dall'angolo in alto a destra hello toodo e quindi fare clic su **interprete**.</span><span class="sxs-lookup"><span data-stu-id="73f8b-154">toodo so, open interpreter settings by clicking hello logged in user name from hello top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="73f8b-155">![Avviare l'interprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Output Hive")</span><span class="sxs-lookup"><span data-stu-id="73f8b-155">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
8. <span data-ttu-id="73f8b-156">Scorrere le impostazioni di interprete tooLivy e quindi fare clic su **riavviare**.</span><span class="sxs-lookup"><span data-stu-id="73f8b-156">Scroll tooLivy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="73f8b-157">![Riavviare hello inserire il intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "riavviare hello Zeppelin intepreter")</span><span class="sxs-lookup"><span data-stu-id="73f8b-157">![Restart hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart hello Zeppelin intepreter")</span></span>

## <a name="how-do-i-use-external-packages-with-hello-notebook"></a><span data-ttu-id="73f8b-158">Utilizzo di pacchetti esterni con notebook hello</span><span class="sxs-lookup"><span data-stu-id="73f8b-158">How do I use external packages with hello notebook?</span></span>
<span data-ttu-id="73f8b-159">È possibile configurare notebook Zeppelin hello in cluster Apache Spark in HDInsight (Linux) toouse esterni, il contributo della community i pacchetti che non sono inclusi out-of-the-box in cluster hello.</span><span class="sxs-lookup"><span data-stu-id="73f8b-159">You can configure hello Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) toouse external, community-contributed packages that are not included out-of-the-box in hello cluster.</span></span> <span data-ttu-id="73f8b-160">È possibile cercare hello [repository Maven](http://search.maven.org/) per l'elenco completo di hello dei pacchetti disponibili.</span><span class="sxs-lookup"><span data-stu-id="73f8b-160">You can search hello [Maven repository](http://search.maven.org/) for hello complete list of packages that are available.</span></span> <span data-ttu-id="73f8b-161">È anche possibile ottenere un elenco dei pacchetti disponibili da altre origini.</span><span class="sxs-lookup"><span data-stu-id="73f8b-161">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="73f8b-162">Ad esempio, un elenco completo dei pacchetti creati dalla community è disponibile nel sito Web [spark-packages.org](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="73f8b-162">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="73f8b-163">In questo articolo, verrà visualizzato come hello toouse [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pacchetto con notebook Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="73f8b-163">In this article, you will see how toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with hello Jupyter notebook.</span></span>

1. <span data-ttu-id="73f8b-164">Aprire le impostazioni dell'interprete.</span><span class="sxs-lookup"><span data-stu-id="73f8b-164">Open interpreter settings.</span></span> <span data-ttu-id="73f8b-165">Nell'angolo superiore destro di hello, fare clic su hello connesso in nome utente e quindi fare clic su **interprete**.</span><span class="sxs-lookup"><span data-stu-id="73f8b-165">From hello top-right corner, click hello logged in user name, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="73f8b-166">![Avviare l'interprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Output Hive")</span><span class="sxs-lookup"><span data-stu-id="73f8b-166">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="73f8b-167">Scorrere le impostazioni di interprete tooLivy e quindi fare clic su **modifica**.</span><span class="sxs-lookup"><span data-stu-id="73f8b-167">Scroll tooLivy interpreter settings and then click **Edit**.</span></span>
   
    <span data-ttu-id="73f8b-168">![Modificare le impostazioni dell'interprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Modificare le impostazioni dell'interprete")</span><span class="sxs-lookup"><span data-stu-id="73f8b-168">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span></span>
3. <span data-ttu-id="73f8b-169">Aggiungere una nuova chiave denominata **livy.spark.jars.packages** e impostarne il valore in formato hello `group:id:version`.</span><span class="sxs-lookup"><span data-stu-id="73f8b-169">Add a new key, called **livy.spark.jars.packages** and set its value in hello format `group:id:version`.</span></span> <span data-ttu-id="73f8b-170">Pertanto, se si desidera hello toouse [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pacchetto, è necessario impostare il valore di hello della chiave di hello troppo`com.databricks:spark-csv_2.10:1.4.0`.</span><span class="sxs-lookup"><span data-stu-id="73f8b-170">So, if you want toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set hello value of hello key too`com.databricks:spark-csv_2.10:1.4.0`.</span></span>
   
    <span data-ttu-id="73f8b-171">![Modificare le impostazioni dell'interprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Modificare le impostazioni dell'interprete")</span><span class="sxs-lookup"><span data-stu-id="73f8b-171">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span></span>
   
    <span data-ttu-id="73f8b-172">Fare clic su **salvare** e quindi riavviare hello interprete di inserire il.</span><span class="sxs-lookup"><span data-stu-id="73f8b-172">Click **Save** and then restart hello Livy interpreter.</span></span>
4. <span data-ttu-id="73f8b-173">**Suggerimento**: se si desidera toounderstand come tooarrive valore hello chiave hello immessi sopra, ecco come.</span><span class="sxs-lookup"><span data-stu-id="73f8b-173">**Tip**: If you want toounderstand how tooarrive at hello value of hello key entered above, here's how.</span></span>
   
    <span data-ttu-id="73f8b-174">a.</span><span class="sxs-lookup"><span data-stu-id="73f8b-174">a.</span></span> <span data-ttu-id="73f8b-175">Individuare il pacchetto di hello in hello Maven Repository.</span><span class="sxs-lookup"><span data-stu-id="73f8b-175">Locate hello package in hello Maven Repository.</span></span> <span data-ttu-id="73f8b-176">In questa esercitazione è stato usato [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="73f8b-176">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="73f8b-177">b.</span><span class="sxs-lookup"><span data-stu-id="73f8b-177">b.</span></span> <span data-ttu-id="73f8b-178">Dal repository hello, raccogliere i valori hello per **GroupId**, **ID**, e **versione**.</span><span class="sxs-lookup"><span data-stu-id="73f8b-178">From hello repository, gather hello values for **GroupId**, **ArtifactId**, and **Version**.</span></span>
   
    <span data-ttu-id="73f8b-179">![Usare pacchetti esterni con notebook di Jupyter](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Usare pacchetti esterni con notebook di Jupyter")</span><span class="sxs-lookup"><span data-stu-id="73f8b-179">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="73f8b-180">c.</span><span class="sxs-lookup"><span data-stu-id="73f8b-180">c.</span></span> <span data-ttu-id="73f8b-181">Concatenare valori hello tre, separati da due punti (**:**).</span><span class="sxs-lookup"><span data-stu-id="73f8b-181">Concatenate hello three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-hello-zeppelin-notebooks-saved"></a><span data-ttu-id="73f8b-182">Dove è hello notebook Zeppelin salvate?</span><span class="sxs-lookup"><span data-stu-id="73f8b-182">Where are hello Zeppelin notebooks saved?</span></span>
<span data-ttu-id="73f8b-183">notebook Zeppelin Hello vengono salvate toohello headnodes di cluster.</span><span class="sxs-lookup"><span data-stu-id="73f8b-183">hello Zeppelin notebooks are saved toohello cluster headnodes.</span></span> <span data-ttu-id="73f8b-184">Pertanto, se si elimina il cluster di hello, verranno eliminati anche i notebook hello.</span><span class="sxs-lookup"><span data-stu-id="73f8b-184">So, if you delete hello cluster, hello notebooks will be deleted as well.</span></span> <span data-ttu-id="73f8b-185">Se si desidera toopreserve i blocchi appunti per utilizzarli in altri cluster, è necessario esportarli dopo aver hello processi in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="73f8b-185">If you want toopreserve your notebooks for later use on other clusters, you must export them after you have finished running hello jobs.</span></span> <span data-ttu-id="73f8b-186">tooexport un blocco per Appunti, fare clic su hello **esportare** icona come illustrato nell'immagine di hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="73f8b-186">tooexport a notebook, click hello **Export** icon as shown in hello image below.</span></span>

<span data-ttu-id="73f8b-187">![Scaricare notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "notebook hello Download")</span><span class="sxs-lookup"><span data-stu-id="73f8b-187">![Download notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download hello notebook")</span></span>

<span data-ttu-id="73f8b-188">Ciò consente di risparmiare notebook hello come un file JSON nel percorso di download.</span><span class="sxs-lookup"><span data-stu-id="73f8b-188">This saves hello notebook as a JSON file in your download location.</span></span>

## <a name="livy-session-management"></a><span data-ttu-id="73f8b-189">Gestione delle sessioni di Livy</span><span class="sxs-lookup"><span data-stu-id="73f8b-189">Livy session management</span></span>
<span data-ttu-id="73f8b-190">Quando si esegue primo paragrafo di codice hello nel blocco note Zeppelin, viene creata una nuova sessione di inserire il nel cluster di HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="73f8b-190">When you run hello first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span></span> <span data-ttu-id="73f8b-191">Tale sessione sarà condivisa da tutti i notebook Zeppelin creati successivamente.</span><span class="sxs-lookup"><span data-stu-id="73f8b-191">This session is shared across all Zeppelin notebooks that you subsequently create.</span></span> <span data-ttu-id="73f8b-192">Se ad alcune hello motivo inserire il sessione è terminata (riavviare il computer del cluster, e così via), non sarà in grado di toorun processi dal blocco appunti Zeppelin hello.</span><span class="sxs-lookup"><span data-stu-id="73f8b-192">If for some reason hello Livy session is killed (cluster reboot, etc.), you will not be able toorun jobs from hello Zeppelin notebook.</span></span>

<span data-ttu-id="73f8b-193">In tal caso, è necessario eseguire operazioni prima di iniziare l'esecuzione di processi da un blocco per Appunti Zeppelin hello.</span><span class="sxs-lookup"><span data-stu-id="73f8b-193">In such a case, you must perform hello following steps before you can start running jobs from a Zeppelin notebook.</span></span> 

1. <span data-ttu-id="73f8b-194">Riavviare hello interprete di inserire il blocco appunti Zeppelin hello.</span><span class="sxs-lookup"><span data-stu-id="73f8b-194">Restart hello Livy interpreter from hello Zeppelin notebook.</span></span> <span data-ttu-id="73f8b-195">In tal caso, aprire le impostazioni di interprete facendo hello connesso in nome utente dall'angolo in alto a destra hello toodo e quindi fare clic su **interprete**.</span><span class="sxs-lookup"><span data-stu-id="73f8b-195">toodo so, open interpreter settings by clicking hello logged in user name from hello top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="73f8b-196">![Avviare l'interprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Output Hive")</span><span class="sxs-lookup"><span data-stu-id="73f8b-196">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="73f8b-197">Scorrere le impostazioni di interprete tooLivy e quindi fare clic su **riavviare**.</span><span class="sxs-lookup"><span data-stu-id="73f8b-197">Scroll tooLivy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="73f8b-198">![Riavviare hello inserire il intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "riavviare hello Zeppelin intepreter")</span><span class="sxs-lookup"><span data-stu-id="73f8b-198">![Restart hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart hello Zeppelin intepreter")</span></span>
3. <span data-ttu-id="73f8b-199">Eseguire una cella di codice da un notebook Zeppelin esistente.</span><span class="sxs-lookup"><span data-stu-id="73f8b-199">Run a code cell from an existing Zeppelin notebook.</span></span> <span data-ttu-id="73f8b-200">Questo crea una nuova sessione di inserire il cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="73f8b-200">This creates a new Livy session in hello HDInsight cluster.</span></span>

## <span data-ttu-id="73f8b-201"><a name="seealso"></a>Vedere anche</span><span class="sxs-lookup"><span data-stu-id="73f8b-201"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="73f8b-202">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="73f8b-202">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="73f8b-203">Scenari</span><span class="sxs-lookup"><span data-stu-id="73f8b-203">Scenarios</span></span>
* [<span data-ttu-id="73f8b-204">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="73f8b-204">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="73f8b-205">Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC</span><span class="sxs-lookup"><span data-stu-id="73f8b-205">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="73f8b-206">Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict</span><span class="sxs-lookup"><span data-stu-id="73f8b-206">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="73f8b-207">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="73f8b-207">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="73f8b-208">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="73f8b-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="73f8b-209">Creare ed eseguire applicazioni</span><span class="sxs-lookup"><span data-stu-id="73f8b-209">Create and run applications</span></span>
* [<span data-ttu-id="73f8b-210">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="73f8b-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="73f8b-211">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="73f8b-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="73f8b-212">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="73f8b-212">Tools and extensions</span></span>
* [<span data-ttu-id="73f8b-213">Utilizzare i plug-in strumenti di HDInsight per toocreate IntelliJ IDEA e inviare applicazioni Spark Scala</span><span class="sxs-lookup"><span data-stu-id="73f8b-213">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="73f8b-214">Utilizzare i plug-in strumenti di HDInsight per le applicazioni di Spark toodebug IntelliJ IDEA in modalità remota</span><span class="sxs-lookup"><span data-stu-id="73f8b-214">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="73f8b-215">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="73f8b-215">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="73f8b-216">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="73f8b-216">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="73f8b-217">Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan</span><span class="sxs-lookup"><span data-stu-id="73f8b-217">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="73f8b-218">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="73f8b-218">Manage resources</span></span>
* [<span data-ttu-id="73f8b-219">Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure</span><span class="sxs-lookup"><span data-stu-id="73f8b-219">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="73f8b-220">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="73f8b-220">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







