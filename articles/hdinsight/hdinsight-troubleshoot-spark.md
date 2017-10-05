---
title: Risolvere i problemi di Spark tramite Azure HDInsight | Microsoft Docs
description: Risposte alle domande frequenti sull'uso di Apache Spark e Azure HDInsight.
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
ms.openlocfilehash: cfed5f0f4f703821e83e3d365810c0e5ad22f035
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a><span data-ttu-id="93888-104">Risolvere i problemi di Spark tramite Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="93888-104">Troubleshoot Spark by using Azure HDInsight</span></span>

<span data-ttu-id="93888-105">Informazioni sui problemi principali che possono verificarsi quando si usano i payload di Apache Spark in Apache Ambari unitamente alle risoluzioni.</span><span class="sxs-lookup"><span data-stu-id="93888-105">Learn about the top issues and their resolutions when working with Apache Spark payloads in Apache Ambari.</span></span>

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a><span data-ttu-id="93888-106">Come configurare un'applicazione Spark tramite Ambari nei cluster</span><span class="sxs-lookup"><span data-stu-id="93888-106">How do I configure a Spark application by using Ambari on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="93888-107">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="93888-107">Resolution steps</span></span>

<span data-ttu-id="93888-108">I valori di configurazione per questa procedura sono stati impostati in precedenza in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="93888-108">The configuration values for this procedure were previously set in HDInsight.</span></span> <span data-ttu-id="93888-109">Per determinare le configurazioni di Spark da impostare e i rispettivi valori, vedere [Causa dell'eccezione OutOfMemoryError in un'applicazione Spark](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="93888-109">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

1. <span data-ttu-id="93888-110">Nell'elenco di cluster selezionare **Spark2**.</span><span class="sxs-lookup"><span data-stu-id="93888-110">In the list of clusters, select **Spark2**.</span></span>

    ![Selezionare un cluster dall'elenco](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. <span data-ttu-id="93888-112">Selezionare la scheda **Configs** (Configurazioni).</span><span class="sxs-lookup"><span data-stu-id="93888-112">Select the **Configs** tab.</span></span>

    ![Selezionare la scheda Configs (Configurazioni)](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. <span data-ttu-id="93888-114">Nell'elenco delle configurazioni selezionare **Custom-spark2-defaults**.</span><span class="sxs-lookup"><span data-stu-id="93888-114">In the list of configurations, select **Custom-spark2-defaults**.</span></span>

    ![Selezionare custom-spark-defaults](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. <span data-ttu-id="93888-116">Ricercare l'impostazione del valore che si desidera modificare, come **spark.executor.memory**.</span><span class="sxs-lookup"><span data-stu-id="93888-116">Look for the value setting that you need to adjust, such as **spark.executor.memory**.</span></span> <span data-ttu-id="93888-117">In questo caso il valore **4608m** è troppo alto.</span><span class="sxs-lookup"><span data-stu-id="93888-117">In this case, the value of **4608m** is too high.</span></span>

    ![Selezionare il campo spark.executor.memory](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. <span data-ttu-id="93888-119">Configurare il valore sull'impostazione consigliata.</span><span class="sxs-lookup"><span data-stu-id="93888-119">Set the value to the recommended setting.</span></span> <span data-ttu-id="93888-120">Il valore **2048m** è consigliato per questa impostazione.</span><span class="sxs-lookup"><span data-stu-id="93888-120">The value **2048m** is recommended for this setting.</span></span>

    ![Cambiare il valore in 2048m](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. <span data-ttu-id="93888-122">Salvare il valore, quindi salvare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="93888-122">Save the value, and then save the configuration.</span></span> <span data-ttu-id="93888-123">Sulla barra degli strumenti selezionare**Save** (Salva).</span><span class="sxs-lookup"><span data-stu-id="93888-123">On the toolbar, select **Save**.</span></span>

    ![Salvare l'impostazione e la configurazione](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    <span data-ttu-id="93888-125">Si riceve una notifica se una delle configurazioni richiede attenzione.</span><span class="sxs-lookup"><span data-stu-id="93888-125">You are notified if any configurations need attention.</span></span> <span data-ttu-id="93888-126">Annotare gli elementi e quindi selezionare **Proceed Anyway** (Continuare comunque).</span><span class="sxs-lookup"><span data-stu-id="93888-126">Note the items, and then select **Proceed Anyway**.</span></span> 

    ![Selezionare Proceed Anyway (Continuare comunque)](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    <span data-ttu-id="93888-128">Immettere una nota sulle modifiche apportate alla configurazione, quindi selezionare **Save** (Salva).</span><span class="sxs-lookup"><span data-stu-id="93888-128">Write a note about the configuration changes, and then select **Save**.</span></span>

    ![Immettere una nota sulle modifiche apportate](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. <span data-ttu-id="93888-130">Ogni volta che viene salvata una configurazione, viene chiesto di riavviare il servizio.</span><span class="sxs-lookup"><span data-stu-id="93888-130">Whenever a configuration is saved, you are prompted to restart the service.</span></span> <span data-ttu-id="93888-131">Selezionare **Restart** (Riavvia).</span><span class="sxs-lookup"><span data-stu-id="93888-131">Select **Restart**.</span></span>

    ![Selezionare Restart (Riavvia)](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    <span data-ttu-id="93888-133">Confermare il riavvio.</span><span class="sxs-lookup"><span data-stu-id="93888-133">Confirm the restart.</span></span>

    ![Selezionare la conferma del riavvio completo](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    <span data-ttu-id="93888-135">È possibile esaminare i processi in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="93888-135">You can review the processes that are running.</span></span>

    ![Esaminare i processi in esecuzione](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. <span data-ttu-id="93888-137">È possibile aggiungere configurazioni.</span><span class="sxs-lookup"><span data-stu-id="93888-137">You can add configurations.</span></span> <span data-ttu-id="93888-138">Nell'elenco delle configurazioni selezionare **Custom-spark2-defaults** e quindi selezionare **Add Property** (Aggiungi proprietà).</span><span class="sxs-lookup"><span data-stu-id="93888-138">In the list of configurations, select **Custom-spark2-defaults**, and then select **Add Property**.</span></span>

    ![Selezionare Add property (Aggiungi proprietà)](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. <span data-ttu-id="93888-140">Definire una nuova proprietà.</span><span class="sxs-lookup"><span data-stu-id="93888-140">Define a new property.</span></span> <span data-ttu-id="93888-141">È possibile definire una singola proprietà usando una finestra di dialogo per impostazioni specifiche, ad esempio il tipo di dati.</span><span class="sxs-lookup"><span data-stu-id="93888-141">You can define a single property by using a dialog box for specific settings such as the data type.</span></span> <span data-ttu-id="93888-142">In alternativa, è possibile definire più proprietà usando una definizione per riga.</span><span class="sxs-lookup"><span data-stu-id="93888-142">Or, you can define multiple properties by using one definition per line.</span></span> 

    <span data-ttu-id="93888-143">In questo esempio la proprietà **spark.driver.memory** è stata definita con un valore di **4g**.</span><span class="sxs-lookup"><span data-stu-id="93888-143">In this example, the **spark.driver.memory** property is defined with a value of **4g**.</span></span>

    ![Definire una nuova proprietà](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. <span data-ttu-id="93888-145">Salvare la configurazione e quindi riavviare il servizio come descritto nei passaggi 6 e 7.</span><span class="sxs-lookup"><span data-stu-id="93888-145">Save the configuration, and then restart the service as described in steps 6 and 7.</span></span>

<span data-ttu-id="93888-146">Queste modifiche si applicano a tutto il cluster ma è possibile eseguirne l'override quando si invia il processo Spark.</span><span class="sxs-lookup"><span data-stu-id="93888-146">These changes are cluster-wide but can be overridden when you submit the Spark job.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="93888-147">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="93888-147">Additional reading</span></span>

[<span data-ttu-id="93888-148">Invio del processo Spark nei cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="93888-148">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a><span data-ttu-id="93888-149">Come configurare un'applicazione Spark tramite un notebook di Jupyter nei cluster</span><span class="sxs-lookup"><span data-stu-id="93888-149">How do I configure a Spark application by using a Jupyter notebook on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="93888-150">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="93888-150">Resolution steps</span></span>

1. <span data-ttu-id="93888-151">Per determinare le configurazioni di Spark da impostare e i rispettivi valori, vedere [Causa dell'eccezione OutOfMemoryError in un'applicazione Spark](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="93888-151">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="93888-152">Nella prima cella del notebook Jupyter, dopo la direttiva **%%configure**, specificare le configurazioni di Spark in un formato JSON valido.</span><span class="sxs-lookup"><span data-stu-id="93888-152">In the first cell of the Jupyter notebook, after the **%%configure** directive, specify the Spark configurations in valid JSON format.</span></span> <span data-ttu-id="93888-153">Modificare i valori effettivi in base alla necessità:</span><span class="sxs-lookup"><span data-stu-id="93888-153">Change the actual values as necessary:</span></span>

    ![Aggiungere una configurazione](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a><span data-ttu-id="93888-155">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="93888-155">Additional reading</span></span>

[<span data-ttu-id="93888-156">Invio del processo Spark nei cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="93888-156">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a><span data-ttu-id="93888-157">Come configurare un'applicazione Spark tramite Livy nei cluster</span><span class="sxs-lookup"><span data-stu-id="93888-157">How do I configure a Spark application by using Livy on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="93888-158">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="93888-158">Resolution steps</span></span>

1. <span data-ttu-id="93888-159">Per determinare le configurazioni di Spark da impostare e i rispettivi valori, vedere [Causa dell'eccezione OutOfMemoryError in un'applicazione Spark](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="93888-159">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

2. <span data-ttu-id="93888-160">Inviare l'applicazione Spark a Livy usando un client REST come cURL.</span><span class="sxs-lookup"><span data-stu-id="93888-160">Submit the Spark application to Livy by using a REST client like cURL.</span></span> <span data-ttu-id="93888-161">Usare un comando simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="93888-161">Use a command similar to the following.</span></span> <span data-ttu-id="93888-162">Modificare i valori effettivi in base alla necessità:</span><span class="sxs-lookup"><span data-stu-id="93888-162">Change the actual values as necessary:</span></span>

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a><span data-ttu-id="93888-163">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="93888-163">Additional reading</span></span>

[<span data-ttu-id="93888-164">Invio del processo Spark nei cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="93888-164">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a><span data-ttu-id="93888-165">Come configurare un'applicazione Spark tramite spark-submit nei cluster</span><span class="sxs-lookup"><span data-stu-id="93888-165">How do I configure a Spark application by using spark-submit on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="93888-166">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="93888-166">Resolution steps</span></span>

1. <span data-ttu-id="93888-167">Per determinare le configurazioni di Spark da impostare e i rispettivi valori, vedere [Causa dell'eccezione OutOfMemoryError in un'applicazione Spark](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="93888-167">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="93888-168">Avviare spark-shell usando un comando simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="93888-168">Launch spark-shell by using a command similar to the following.</span></span> <span data-ttu-id="93888-169">Modificare il valore effettivo delle configurazioni in base alla necessità:</span><span class="sxs-lookup"><span data-stu-id="93888-169">Change the actual value of the configurations as necessary:</span></span> 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a><span data-ttu-id="93888-170">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="93888-170">Additional reading</span></span>

[<span data-ttu-id="93888-171">Invio del processo Spark nei cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="93888-171">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a><span data-ttu-id="93888-172">Causa dell'eccezione OutOfMemoryError in un'applicazione Spark</span><span class="sxs-lookup"><span data-stu-id="93888-172">What causes a Spark application OutofMemoryError exception</span></span>

### <a name="detailed-description"></a><span data-ttu-id="93888-173">Descrizione dettagliata</span><span class="sxs-lookup"><span data-stu-id="93888-173">Detailed description</span></span>

<span data-ttu-id="93888-174">L'applicazione Spark termina con un errore quando si verificano i seguenti tipi di eccezioni non rilevate:</span><span class="sxs-lookup"><span data-stu-id="93888-174">The Spark application fails, with the following types of uncaught exceptions:</span></span>

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

### <a name="probable-cause"></a><span data-ttu-id="93888-175">Possibile causa</span><span class="sxs-lookup"><span data-stu-id="93888-175">Probable cause</span></span>

<span data-ttu-id="93888-176">La causa più probabile per questa eccezione è costituita dall'allocazione di memoria heap insufficiente alle macchine virtuali Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="93888-176">The most likely cause of this exception is that not enough heap memory is allocated to the Java virtual machines (JVMs).</span></span> <span data-ttu-id="93888-177">Queste macchine virtuali Java vengono avviate come executor o driver come parte dell'applicazione Spark.</span><span class="sxs-lookup"><span data-stu-id="93888-177">These JVMs are launched as executors or drivers as part of the Spark application.</span></span> 

### <a name="resolution-steps"></a><span data-ttu-id="93888-178">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="93888-178">Resolution steps</span></span>

1. <span data-ttu-id="93888-179">Determinare le dimensioni massime dei dati che possono essere gestiti dall'applicazione Spark.</span><span class="sxs-lookup"><span data-stu-id="93888-179">Determine the maximum size of the data the Spark application handles.</span></span> <span data-ttu-id="93888-180">È possibile ottenere una stima in base alle dimensioni massime dei dati di input, i dati intermedi prodotti tramite la trasformazione dei dati di input e i dati di output prodotti quando l'applicazione trasforma ulteriormente i dati intermedi.</span><span class="sxs-lookup"><span data-stu-id="93888-180">You can make a guess based on the maximum size of the input data, the intermediate data that's produced by transforming the input data, and the output data that's produced when the application is further transforming the intermediate data.</span></span> <span data-ttu-id="93888-181">Questo processo può essere iterativo se non si riesce a ottenere una stima iniziale formale.</span><span class="sxs-lookup"><span data-stu-id="93888-181">This process can be an iterative if you can't make an initial formal guess.</span></span> 

2. <span data-ttu-id="93888-182">Assicurarsi che il cluster HDInsight da usare abbia risorse sufficienti in termini di memoria e di core per l'applicazione Spark.</span><span class="sxs-lookup"><span data-stu-id="93888-182">Make sure that the HDInsight cluster that you're going to use has enough resources in terms of memory and cores to accommodate the Spark application.</span></span> <span data-ttu-id="93888-183">Per eseguire questa verifica, visualizzare la sezione del cluster relativa alle metriche nell'interfaccia utente YARN e confrontare i valori di **Memory Used** (Memoria in uso) e **Memory Total** (Memoria totale) e i valori di **VCores Used** (VCore in uso) e **VCores Total** (VCore totali).</span><span class="sxs-lookup"><span data-stu-id="93888-183">You can determine this by viewing the cluster metrics section of the YARN UI for the values of **Memory Used** vs. **Memory Total**, and **VCores Used** vs. **VCores Total**.</span></span>

3. <span data-ttu-id="93888-184">Impostare i valori appropriati per le configurazioni seguenti di Spark, che non devono superare il 90% della memoria e dei core disponibili.</span><span class="sxs-lookup"><span data-stu-id="93888-184">Set the following Spark configurations to appropriate values, which should not exceed 90% of the available memory and cores.</span></span> <span data-ttu-id="93888-185">I valori devono essere compresi nei requisiti di memoria dell'applicazione Spark:</span><span class="sxs-lookup"><span data-stu-id="93888-185">The values should be well within the memory requirements of the Spark application:</span></span> 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    <span data-ttu-id="93888-186">Per ottenere il valore relativo alla memoria totale usata da tutti gli executor, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="93888-186">To get the total memory used by all executors, run the following command:</span></span> 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    <span data-ttu-id="93888-187">Per ottenere il valore relativo alla memoria totale usata dal driver, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="93888-187">To get the total memory used by the driver, run the following command:</span></span>
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a><span data-ttu-id="93888-188">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="93888-188">Additional reading</span></span>

- [<span data-ttu-id="93888-189">Spark memory management overview (Panoramica della gestione della memoria Spark)</span><span class="sxs-lookup"><span data-stu-id="93888-189">Spark memory management overview</span></span>](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)
- <span data-ttu-id="93888-190">[Debug a Spark application on an HDInsight cluster](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/) (Eseguire il debug di un'applicazione Spark in un cluster HDInsight)</span><span class="sxs-lookup"><span data-stu-id="93888-190">[Debug a Spark application on an HDInsight cluster](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/)</span></span>

