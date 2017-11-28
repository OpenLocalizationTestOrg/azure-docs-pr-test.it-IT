---
title: aaaTroubleshoot Spark usando Azure HDInsight | Documenti Microsoft
description: Ottenere risposte toocommon domande sull'uso di Apache Spark e Azure HDInsight.
keywords: Azure HDInsight, Spark, domande frequenti, guida alla risoluzione dei problemi, problemi comuni, configurazione dell'applicazione, Ambari
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: 25D89586-DE5B-4268-B5D5-CC2CE12207ED
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: c9f910daf295462238a3143ae2589db6d383097f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a><span data-ttu-id="6cf88-104">Risolvere i problemi di Spark tramite Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="6cf88-104">Troubleshoot Spark by using Azure HDInsight</span></span>

<span data-ttu-id="6cf88-105">Informazioni sui problemi principali hello e le relative soluzioni quando si lavora con payload Apache Spark in Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="6cf88-105">Learn about hello top issues and their resolutions when working with Apache Spark payloads in Apache Ambari.</span></span>

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a><span data-ttu-id="6cf88-106">Come configurare un'applicazione Spark tramite Ambari nei cluster</span><span class="sxs-lookup"><span data-stu-id="6cf88-106">How do I configure a Spark application by using Ambari on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="6cf88-107">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="6cf88-107">Resolution steps</span></span>

<span data-ttu-id="6cf88-108">i valori di configurazione Hello per questa procedura sono stati impostati in precedenza in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6cf88-108">hello configuration values for this procedure were previously set in HDInsight.</span></span> <span data-ttu-id="6cf88-109">vedere quali configurazioni di Spark, sono necessari valori di set e toowhat toobe, toodetermine [cosa provoca l'eccezione dell'applicazione OutofMemoryError un Spark](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="6cf88-109">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

1. <span data-ttu-id="6cf88-110">Nell'elenco di hello del cluster, selezionare **Spark2**.</span><span class="sxs-lookup"><span data-stu-id="6cf88-110">In hello list of clusters, select **Spark2**.</span></span>

    ![Selezionare un cluster dall'elenco](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. <span data-ttu-id="6cf88-112">Seleziona hello **configurazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="6cf88-112">Select hello **Configs** tab.</span></span>

    ![Selezionare scheda configurazioni hello](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. <span data-ttu-id="6cf88-114">Nell'elenco di hello delle configurazioni, selezionare **impostazioni predefinite personalizzate-spark2**.</span><span class="sxs-lookup"><span data-stu-id="6cf88-114">In hello list of configurations, select **Custom-spark2-defaults**.</span></span>

    ![Selezionare custom-spark-defaults](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. <span data-ttu-id="6cf88-116">Cercare il valore di hello impostazione necessarie tooadjust, ad esempio **spark.executor.memory**.</span><span class="sxs-lookup"><span data-stu-id="6cf88-116">Look for hello value setting that you need tooadjust, such as **spark.executor.memory**.</span></span> <span data-ttu-id="6cf88-117">In questo caso, hello valore **m 4608** è troppo alto.</span><span class="sxs-lookup"><span data-stu-id="6cf88-117">In this case, hello value of **4608m** is too high.</span></span>

    ![Selezionare il campo di spark.executor.memory hello](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. <span data-ttu-id="6cf88-119">Set hello valore toohello impostazione consigliata.</span><span class="sxs-lookup"><span data-stu-id="6cf88-119">Set hello value toohello recommended setting.</span></span> <span data-ttu-id="6cf88-120">valore di Hello **m 2048** è consigliato per questa impostazione.</span><span class="sxs-lookup"><span data-stu-id="6cf88-120">hello value **2048m** is recommended for this setting.</span></span>

    ![Modifica valore too2048m](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. <span data-ttu-id="6cf88-122">Salvare il valore di hello e quindi salvare la configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="6cf88-122">Save hello value, and then save hello configuration.</span></span> <span data-ttu-id="6cf88-123">Sulla barra degli strumenti hello, selezionare **salvare**.</span><span class="sxs-lookup"><span data-stu-id="6cf88-123">On hello toolbar, select **Save**.</span></span>

    ![Salva la configurazione e l'impostazione di hello](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    <span data-ttu-id="6cf88-125">Si riceve una notifica se una delle configurazioni richiede attenzione.</span><span class="sxs-lookup"><span data-stu-id="6cf88-125">You are notified if any configurations need attention.</span></span> <span data-ttu-id="6cf88-126">Tenere presente hello e quindi selezionare **continuare comunque**.</span><span class="sxs-lookup"><span data-stu-id="6cf88-126">Note hello items, and then select **Proceed Anyway**.</span></span> 

    ![Selezionare Proceed Anyway (Continuare comunque)](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    <span data-ttu-id="6cf88-128">Scrivere una nota sulle modifiche di configurazione hello e quindi selezionare **salvare**.</span><span class="sxs-lookup"><span data-stu-id="6cf88-128">Write a note about hello configuration changes, and then select **Save**.</span></span>

    ![Immettere una nota relativa hello le modifiche](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. <span data-ttu-id="6cf88-130">Ogni volta che viene salvata una configurazione, viene richiesto il servizio di hello toorestart.</span><span class="sxs-lookup"><span data-stu-id="6cf88-130">Whenever a configuration is saved, you are prompted toorestart hello service.</span></span> <span data-ttu-id="6cf88-131">Selezionare **Restart** (Riavvia).</span><span class="sxs-lookup"><span data-stu-id="6cf88-131">Select **Restart**.</span></span>

    ![Selezionare Restart (Riavvia)](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    <span data-ttu-id="6cf88-133">Confermare il riavvio di hello.</span><span class="sxs-lookup"><span data-stu-id="6cf88-133">Confirm hello restart.</span></span>

    ![Selezionare la conferma del riavvio completo](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    <span data-ttu-id="6cf88-135">È possibile esaminare i processi di hello in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6cf88-135">You can review hello processes that are running.</span></span>

    ![Esaminare i processi in esecuzione](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. <span data-ttu-id="6cf88-137">È possibile aggiungere configurazioni.</span><span class="sxs-lookup"><span data-stu-id="6cf88-137">You can add configurations.</span></span> <span data-ttu-id="6cf88-138">Nell'elenco di hello delle configurazioni, selezionare **impostazioni predefinite di spark2 personalizzate**, quindi selezionare **Aggiungi proprietà**.</span><span class="sxs-lookup"><span data-stu-id="6cf88-138">In hello list of configurations, select **Custom-spark2-defaults**, and then select **Add Property**.</span></span>

    ![Selezionare Add property (Aggiungi proprietà)](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. <span data-ttu-id="6cf88-140">Definire una nuova proprietà.</span><span class="sxs-lookup"><span data-stu-id="6cf88-140">Define a new property.</span></span> <span data-ttu-id="6cf88-141">È possibile definire una singola proprietà tramite una finestra di dialogo per le impostazioni specifiche, ad esempio il tipo di dati di hello.</span><span class="sxs-lookup"><span data-stu-id="6cf88-141">You can define a single property by using a dialog box for specific settings such as hello data type.</span></span> <span data-ttu-id="6cf88-142">In alternativa, è possibile definire più proprietà usando una definizione per riga.</span><span class="sxs-lookup"><span data-stu-id="6cf88-142">Or, you can define multiple properties by using one definition per line.</span></span> 

    <span data-ttu-id="6cf88-143">In questo esempio hello **spark.driver.memory** proprietà è definita con un valore di **4g**.</span><span class="sxs-lookup"><span data-stu-id="6cf88-143">In this example, hello **spark.driver.memory** property is defined with a value of **4g**.</span></span>

    ![Definire una nuova proprietà](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. <span data-ttu-id="6cf88-145">Salvare la configurazione hello e quindi riavviare il servizio di hello, come descritto nei passaggi 6 e 7.</span><span class="sxs-lookup"><span data-stu-id="6cf88-145">Save hello configuration, and then restart hello service as described in steps 6 and 7.</span></span>

<span data-ttu-id="6cf88-146">Queste modifiche sono a livello di cluster, ma possono essere ignorate quando si invia il processo di Spark hello.</span><span class="sxs-lookup"><span data-stu-id="6cf88-146">These changes are cluster-wide but can be overridden when you submit hello Spark job.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="6cf88-147">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6cf88-147">Additional reading</span></span>

[<span data-ttu-id="6cf88-148">Invio del processo Spark nei cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="6cf88-148">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a><span data-ttu-id="6cf88-149">Come configurare un'applicazione Spark tramite un notebook di Jupyter nei cluster</span><span class="sxs-lookup"><span data-stu-id="6cf88-149">How do I configure a Spark application by using a Jupyter notebook on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="6cf88-150">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="6cf88-150">Resolution steps</span></span>

1. <span data-ttu-id="6cf88-151">vedere quali configurazioni di Spark, sono necessari valori di set e toowhat toobe, toodetermine [cosa provoca l'eccezione dell'applicazione OutofMemoryError un Spark](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="6cf88-151">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="6cf88-152">Nella prima cella di hello del server Jupyter notebook hello, dopo aver hello **% % configurare** direttiva, specificare le configurazioni di Spark hello nel formato JSON valido.</span><span class="sxs-lookup"><span data-stu-id="6cf88-152">In hello first cell of hello Jupyter notebook, after hello **%%configure** directive, specify hello Spark configurations in valid JSON format.</span></span> <span data-ttu-id="6cf88-153">Modificare i valori effettivi di hello in base alle esigenze:</span><span class="sxs-lookup"><span data-stu-id="6cf88-153">Change hello actual values as necessary:</span></span>

    ![Aggiungere una configurazione](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a><span data-ttu-id="6cf88-155">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6cf88-155">Additional reading</span></span>

[<span data-ttu-id="6cf88-156">Invio del processo Spark nei cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="6cf88-156">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a><span data-ttu-id="6cf88-157">Come configurare un'applicazione Spark tramite Livy nei cluster</span><span class="sxs-lookup"><span data-stu-id="6cf88-157">How do I configure a Spark application by using Livy on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="6cf88-158">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="6cf88-158">Resolution steps</span></span>

1. <span data-ttu-id="6cf88-159">vedere quali configurazioni di Spark, sono necessari valori di set e toowhat toobe, toodetermine [cosa provoca l'eccezione dell'applicazione OutofMemoryError un Spark](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="6cf88-159">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

2. <span data-ttu-id="6cf88-160">Inviare hello Spark applicazione tooLivy tramite un client REST come cURL.</span><span class="sxs-lookup"><span data-stu-id="6cf88-160">Submit hello Spark application tooLivy by using a REST client like cURL.</span></span> <span data-ttu-id="6cf88-161">Utilizzare una comando simile toohello che segue.</span><span class="sxs-lookup"><span data-stu-id="6cf88-161">Use a command similar toohello following.</span></span> <span data-ttu-id="6cf88-162">Modificare i valori effettivi di hello in base alle esigenze:</span><span class="sxs-lookup"><span data-stu-id="6cf88-162">Change hello actual values as necessary:</span></span>

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a><span data-ttu-id="6cf88-163">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6cf88-163">Additional reading</span></span>

[<span data-ttu-id="6cf88-164">Invio del processo Spark nei cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="6cf88-164">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a><span data-ttu-id="6cf88-165">Come configurare un'applicazione Spark tramite spark-submit nei cluster</span><span class="sxs-lookup"><span data-stu-id="6cf88-165">How do I configure a Spark application by using spark-submit on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="6cf88-166">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="6cf88-166">Resolution steps</span></span>

1. <span data-ttu-id="6cf88-167">vedere quali configurazioni di Spark, sono necessari valori di set e toowhat toobe, toodetermine [cosa provoca l'eccezione dell'applicazione OutofMemoryError un Spark](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="6cf88-167">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="6cf88-168">Avviare shell di spark usando un comando simile toohello.</span><span class="sxs-lookup"><span data-stu-id="6cf88-168">Launch spark-shell by using a command similar toohello following.</span></span> <span data-ttu-id="6cf88-169">Modificare il valore effettivo di hello delle configurazioni di hello in base alle esigenze:</span><span class="sxs-lookup"><span data-stu-id="6cf88-169">Change hello actual value of hello configurations as necessary:</span></span> 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a><span data-ttu-id="6cf88-170">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6cf88-170">Additional reading</span></span>

[<span data-ttu-id="6cf88-171">Invio del processo Spark nei cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="6cf88-171">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a><span data-ttu-id="6cf88-172">Causa dell'eccezione OutOfMemoryError in un'applicazione Spark</span><span class="sxs-lookup"><span data-stu-id="6cf88-172">What causes a Spark application OutofMemoryError exception</span></span>

### <a name="detailed-description"></a><span data-ttu-id="6cf88-173">Descrizione dettagliata</span><span class="sxs-lookup"><span data-stu-id="6cf88-173">Detailed description</span></span>

<span data-ttu-id="6cf88-174">applicazione di Spark Hello non riesce, con i seguenti tipi di eccezioni non rilevate hello:</span><span class="sxs-lookup"><span data-stu-id="6cf88-174">hello Spark application fails, with hello following types of uncaught exceptions:</span></span>

```apache
ERROR Executor: Exception in task 7.0 in stage 6.0 (TID 439) 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

```apache
ERROR SparkUncaughtExceptionHandler: Uncaught exception in thread Thread[Executor task launch worker-0,5,main] 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

### <a name="probable-cause"></a><span data-ttu-id="6cf88-175">Possibile causa</span><span class="sxs-lookup"><span data-stu-id="6cf88-175">Probable cause</span></span>

<span data-ttu-id="6cf88-176">causa più probabile di Hello di questa eccezione è che non è sufficiente memoria heap è allocata toohello Java virtual machine (JVMs).</span><span class="sxs-lookup"><span data-stu-id="6cf88-176">hello most likely cause of this exception is that not enough heap memory is allocated toohello Java virtual machines (JVMs).</span></span> <span data-ttu-id="6cf88-177">Questi JVMs vengono avviate come executor o i driver come parte dell'applicazione di Spark hello.</span><span class="sxs-lookup"><span data-stu-id="6cf88-177">These JVMs are launched as executors or drivers as part of hello Spark application.</span></span> 

### <a name="resolution-steps"></a><span data-ttu-id="6cf88-178">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="6cf88-178">Resolution steps</span></span>

1. <span data-ttu-id="6cf88-179">Determinare hello dimensioni massime di hello dati hello Spark applicazione handle.</span><span class="sxs-lookup"><span data-stu-id="6cf88-179">Determine hello maximum size of hello data hello Spark application handles.</span></span> <span data-ttu-id="6cf88-180">È possibile rendere un'ipotesi basata sulla dimensione massima di hello hello di dati di input, i dati intermedi hello prodotto dalla trasformazione di dati di input hello e dati di output di hello che viene generati quando un'applicazione hello è ulteriormente la trasformazione di dati intermedi hello.</span><span class="sxs-lookup"><span data-stu-id="6cf88-180">You can make a guess based on hello maximum size of hello input data, hello intermediate data that's produced by transforming hello input data, and hello output data that's produced when hello application is further transforming hello intermediate data.</span></span> <span data-ttu-id="6cf88-181">Questo processo può essere iterativo se non si riesce a ottenere una stima iniziale formale.</span><span class="sxs-lookup"><span data-stu-id="6cf88-181">This process can be an iterative if you can't make an initial formal guess.</span></span> 

2. <span data-ttu-id="6cf88-182">Verificare che il cluster HDInsight hello che si userà toouse disponga di sufficienti risorse in termini di memoria e core tooaccommodate hello Spark dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6cf88-182">Make sure that hello HDInsight cluster that you're going toouse has enough resources in terms of memory and cores tooaccommodate hello Spark application.</span></span> <span data-ttu-id="6cf88-183">È possibile determinare questo visualizzando una sezione di metriche di cluster hello di hello YARN UI per i valori hello di **di memoria utilizzata** Visual Studio. **Memory Total** (Memoria totale) e i valori di **VCores Used** (VCore in uso) e **VCores Total** (VCore totali).</span><span class="sxs-lookup"><span data-stu-id="6cf88-183">You can determine this by viewing hello cluster metrics section of hello YARN UI for hello values of **Memory Used** vs. **Memory Total**, and **VCores Used** vs. **VCores Total**.</span></span>

3. <span data-ttu-id="6cf88-184">Impostare hello seguente Spark valori tooappropriate delle configurazioni non devono superare il 90% di memoria disponibile hello e di core.</span><span class="sxs-lookup"><span data-stu-id="6cf88-184">Set hello following Spark configurations tooappropriate values, which should not exceed 90% of hello available memory and cores.</span></span> <span data-ttu-id="6cf88-185">i valori Hello devono essere anche all'interno di requisiti di memoria hello di hello applicazione Spark:</span><span class="sxs-lookup"><span data-stu-id="6cf88-185">hello values should be well within hello memory requirements of hello Spark application:</span></span> 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    <span data-ttu-id="6cf88-186">tooget hello memoria totale utilizzata da tutti gli esecutori, Esegui hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6cf88-186">tooget hello total memory used by all executors, run hello following command:</span></span> 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    <span data-ttu-id="6cf88-187">tooget hello memoria totale utilizzata dal driver hello, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6cf88-187">tooget hello total memory used by hello driver, run hello following command:</span></span>
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a><span data-ttu-id="6cf88-188">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6cf88-188">Additional reading</span></span>

- [<span data-ttu-id="6cf88-189">Spark memory management overview (Panoramica della gestione della memoria Spark)</span><span class="sxs-lookup"><span data-stu-id="6cf88-189">Spark memory management overview</span></span>](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)
- <span data-ttu-id="6cf88-190">[Debug a Spark application on an HDInsight cluster](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/) (Eseguire il debug di un'applicazione Spark in un cluster HDInsight)</span><span class="sxs-lookup"><span data-stu-id="6cf88-190">[Debug a Spark application on an HDInsight cluster](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/)</span></span>

