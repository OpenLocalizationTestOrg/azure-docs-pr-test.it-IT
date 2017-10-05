---
title: Usare Hive di Hadoop con Curl in HDInsight - Azure | Microsoft Docs
description: "Informazioni su come inviare in modalità remota processi Pig a HDInsight mediante Curl."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6ce18163-63b5-4df6-9bb6-8fcbd4db05d8
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 8a4f217b046121f85be0585eab18d90c44f21b9e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a><span data-ttu-id="62b22-103">Esecuzione di query Hive con Hadoop in HDInsight tramite REST</span><span class="sxs-lookup"><span data-stu-id="62b22-103">Run Hive queries with Hadoop in HDInsight using REST</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="62b22-104">Informazioni su come usare l'API REST WebHCat per eseguire query Hive con Hadoop nel cluster HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="62b22-104">Learn how to use the WebHCat REST API to run Hive queries with Hadoop on Azure HDInsight cluster.</span></span>

<span data-ttu-id="62b22-105">[Curl](http://curl.haxx.se/) viene usato per illustrare come sia possibile interagire con HDInsight usando richieste HTTP non elaborate.</span><span class="sxs-lookup"><span data-stu-id="62b22-105">[Curl](http://curl.haxx.se/) is used to demonstrate how you can interact with HDInsight by using raw HTTP requests.</span></span> <span data-ttu-id="62b22-106">L'utilità [jq](http://stedolan.github.io/jq/) viene usata per elaborare i dati JSON restituiti dalle richieste REST.</span><span class="sxs-lookup"><span data-stu-id="62b22-106">The [jq](http://stedolan.github.io/jq/) utility is used to process the JSON data returned from REST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="62b22-107">Se si ha già familiarità con l'uso di server Hadoop basati su Linux, ma non si ha esperienza con HDInsight, vedere il documento [Informazioni utili su Hadoop in HDInsight basato su Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="62b22-107">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see the [What you need to know about Hadoop on Linux-based HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>

## <span data-ttu-id="62b22-108"><a id="curl"></a>Eseguire query Hive</span><span class="sxs-lookup"><span data-stu-id="62b22-108"><a id="curl"></a>Run Hive queries</span></span>

> [!NOTE]
> <span data-ttu-id="62b22-109">Quando si usa Curl o qualsiasi altra forma di comunicazione REST con WebHCat, è necessario autenticare le richieste fornendo il nome utente e la password dell'amministratore cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="62b22-109">When using cURL or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span>
>
> <span data-ttu-id="62b22-110">Per i comandi riportati in questa sezione, sostituire **USERNAME** con l'utente da autenticare nel cluster e **PASSWORD** con la password dell'account utente.</span><span class="sxs-lookup"><span data-stu-id="62b22-110">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="62b22-111">Sostituire **CLUSTERNAME** con il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="62b22-111">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
>
> <span data-ttu-id="62b22-112">L'API REST viene protetta tramite l' [autenticazione di base](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="62b22-112">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="62b22-113">Per essere certi che le credenziali vengano inviate in modo sicuro al server, eseguire sempre le richieste usando il protocollo Secure HTTP (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="62b22-113">To help ensure that your credentials are securely sent to the server, always make requests by using Secure HTTP (HTTPS).</span></span>

1. <span data-ttu-id="62b22-114">Da una riga di comando usare il comando seguente per verificare che sia possibile connettersi al cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="62b22-114">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="62b22-115">Si riceverà un messaggio simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="62b22-115">You receive a response similar to the following text:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="62b22-116">I parametri usati in questo comando sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="62b22-116">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="62b22-117">**-u** : il nome utente e la password usati per autenticare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="62b22-117">**-u** - The user name and password used to authenticate the request.</span></span>
   * <span data-ttu-id="62b22-118">**-G** - indica che è un'operazione GET.</span><span class="sxs-lookup"><span data-stu-id="62b22-118">**-G** - Indicates that this request is a GET operation.</span></span>

     <span data-ttu-id="62b22-119">L'inizio dell'URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, sarà uguale per tutte le richieste.</span><span class="sxs-lookup"><span data-stu-id="62b22-119">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span> <span data-ttu-id="62b22-120">Il percorso, **/status**, indica che la richiesta deve restituire uno stato di WebHCat (noto anche come Templeton) per il server.</span><span class="sxs-lookup"><span data-stu-id="62b22-120">The path, **/status**, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span></span> <span data-ttu-id="62b22-121">È inoltre possibile richiedere la versione di Hive usando il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="62b22-121">You can also request the version of Hive by using the following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     <span data-ttu-id="62b22-122">Questa richiesta restituisce una risposta simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="62b22-122">This request returns a response similar to the following text:</span></span>

       <span data-ttu-id="62b22-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span><span class="sxs-lookup"><span data-stu-id="62b22-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span></span>

2. <span data-ttu-id="62b22-124">Usare quanto segue per creare una tabella denominata **log4jLogs**:</span><span class="sxs-lookup"><span data-stu-id="62b22-124">Use the following to create a table named **log4jLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="62b22-125">Con questa richiesta sono stati usati i seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="62b22-125">The following parameters used with this request:</span></span>

   * <span data-ttu-id="62b22-126">**-d**: poiché `-G` non viene usato, la richiesta userà il metodo POST per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="62b22-126">**-d** - Since `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="62b22-127">`-d` specifica i valori di dati che vengono inviati con la richiesta.</span><span class="sxs-lookup"><span data-stu-id="62b22-127">`-d` specifies the data values that are sent with the request.</span></span>

     * <span data-ttu-id="62b22-128">**user.name** : l'utente che esegue il comando.</span><span class="sxs-lookup"><span data-stu-id="62b22-128">**user.name** - The user that is running the command.</span></span>
     * <span data-ttu-id="62b22-129">**execute** : le istruzioni HiveQL da eseguire.</span><span class="sxs-lookup"><span data-stu-id="62b22-129">**execute** - The HiveQL statements to execute.</span></span>
     * <span data-ttu-id="62b22-130">**statusdir** - La directory in cui è scritto lo stato per questo processo.</span><span class="sxs-lookup"><span data-stu-id="62b22-130">**statusdir** - The directory that the status for this job is written to.</span></span>

     <span data-ttu-id="62b22-131">Di seguito sono elencate le istruzioni che eseguono queste azioni:</span><span class="sxs-lookup"><span data-stu-id="62b22-131">These statements perform the following actions:</span></span>
   * <span data-ttu-id="62b22-132">**DROP TABLE** - Se la tabella esiste già, viene eliminata.</span><span class="sxs-lookup"><span data-stu-id="62b22-132">**DROP TABLE** - If the table already exists, it is deleted.</span></span>
   * <span data-ttu-id="62b22-133">**CREATE EXTERNAL TABLE** : crea una nuova tabella "external" in Hive.</span><span class="sxs-lookup"><span data-stu-id="62b22-133">**CREATE EXTERNAL TABLE** - Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="62b22-134">Le tabelle esterne archiviano solo la definizione della tabella in Hive.</span><span class="sxs-lookup"><span data-stu-id="62b22-134">External tables store only the table definition in Hive.</span></span> <span data-ttu-id="62b22-135">I dati rimangono nel percorso originale.</span><span class="sxs-lookup"><span data-stu-id="62b22-135">The data is left in the original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="62b22-136">Usa le tabelle esterne se si prevede che i dati sottostanti verranno aggiornati da un'origine esterna.</span><span class="sxs-lookup"><span data-stu-id="62b22-136">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="62b22-137">Ad esempio, un processo di caricamento dati automatizzato o un'altra operazione MapReduce.</span><span class="sxs-lookup"><span data-stu-id="62b22-137">For example, an automated data upload process or another MapReduce operation.</span></span>
     >
     > <span data-ttu-id="62b22-138">L'eliminazione di una tabella esterna **non** comporta anche l'eliminazione dei dati. Viene eliminata solo la definizione della tabella.</span><span class="sxs-lookup"><span data-stu-id="62b22-138">Dropping an external table does **not** delete the data, only the table definition.</span></span>

   * <span data-ttu-id="62b22-139">**ROW FORMAT** - Indica il modo in cui sono formattati i dati.</span><span class="sxs-lookup"><span data-stu-id="62b22-139">**ROW FORMAT** - How the data is formatted.</span></span> <span data-ttu-id="62b22-140">I campi in ogni log sono separati da uno spazio.</span><span class="sxs-lookup"><span data-stu-id="62b22-140">The fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="62b22-141">**STORED AS TEXTFILE LOCATION** - Indica dove sono archiviati i dati (la directory example/data) e che sono archiviati come testo.</span><span class="sxs-lookup"><span data-stu-id="62b22-141">**STORED AS TEXTFILE LOCATION** - Where the data is stored (the example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="62b22-142">**SELECT**: seleziona un numero di tutte le righe in cui la colonna **t4** include il valore **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="62b22-142">**SELECT** - Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="62b22-143">L'istruzione dovrebbe restituire un valore pari a **3**, poiché sono presenti tre righe contenenti questo valore.</span><span class="sxs-lookup"><span data-stu-id="62b22-143">This statement returns a value of **3** as there are three rows that contain this value.</span></span>

     > [!NOTE]
     > <span data-ttu-id="62b22-144">Si noti che gli spazi tra le istruzioni HiveQL vengono sostituiti dal carattere `+` se è in uso Curl.</span><span class="sxs-lookup"><span data-stu-id="62b22-144">Notice that the spaces between HiveQL statements are replaced by the `+` character when used with Curl.</span></span> <span data-ttu-id="62b22-145">I valori tra virgolette che contengono uno spazio, ad esempio il delimitatore, non devono essere sostituiti da `+`.</span><span class="sxs-lookup"><span data-stu-id="62b22-145">Quoted values that contain a space, such as the delimiter, should not be replaced by `+`.</span></span>

   * <span data-ttu-id="62b22-146">**INPUT__FILE__NAME LIKE '%25.log'** - Questa istruzione limita la ricerca solo ai file che terminano con .log.</span><span class="sxs-lookup"><span data-stu-id="62b22-146">**INPUT__FILE__NAME LIKE '%25.log'** - This statement limits the search to only use files ending in .log.</span></span>

     > [!NOTE]
     > <span data-ttu-id="62b22-147">`%25` è l'URL con codifica %, pertanto la condizione effettiva è `like '%.log'`.</span><span class="sxs-lookup"><span data-stu-id="62b22-147">The `%25` is the URL encoded form of %, so the actual condition is `like '%.log'`.</span></span> <span data-ttu-id="62b22-148">% deve essere l'URL codificato, poiché viene considerato come un carattere speciale negli URL.</span><span class="sxs-lookup"><span data-stu-id="62b22-148">The % has to be URL encoded, as it is treated as a special character in URLs.</span></span>

     <span data-ttu-id="62b22-149">Questo comando dovrebbe restituire un ID processo utilizzabile per verificare lo stato del processo.</span><span class="sxs-lookup"><span data-stu-id="62b22-149">This command should return a job ID that can be used to check the status of the job.</span></span>

       <span data-ttu-id="62b22-150">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="62b22-150">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="62b22-151">Per verificare lo stato del processo, usare il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="62b22-151">To check the status of the job, use the following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="62b22-152">Sostituire **JOBID** con il valore restituito nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="62b22-152">Replace **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="62b22-153">Se ad esempio il valore restituito è `{"id":"job_1415651640909_0026"}`, **JOBID** sarà `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="62b22-153">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="62b22-154">Se il processo è stato completato, lo stato è **SUCCEEDED**.</span><span class="sxs-lookup"><span data-stu-id="62b22-154">If the job has finished, the state is **SUCCEEDED**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="62b22-155">Questa richiesta curl restituisce un documento JSON (JavaScript Object Notation) con informazioni sul processo.</span><span class="sxs-lookup"><span data-stu-id="62b22-155">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job.</span></span> <span data-ttu-id="62b22-156">Jq viene usato per recuperare solo il valore di stato.</span><span class="sxs-lookup"><span data-stu-id="62b22-156">Jq is used to retrieve only the state value.</span></span>

4. <span data-ttu-id="62b22-157">Dopo che lo stato del processo risulta essere **SUCCEEDED**, è possibile recuperare i risultati del processo dall'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="62b22-157">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="62b22-158">Il parametro `statusdir` passato con la query contiene il percorso del file di output; in questo caso **/example/curl**.</span><span class="sxs-lookup"><span data-stu-id="62b22-158">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **/example/curl**.</span></span> <span data-ttu-id="62b22-159">Questo indirizzo archivia l'output nella directory **esempio/curl** nell'archiviazione predefinita dei cluster.</span><span class="sxs-lookup"><span data-stu-id="62b22-159">This address stores the output in the **example/curl** directory in the clusters default storage.</span></span>

    <span data-ttu-id="62b22-160">È possibile elencare e scaricare questi file usando l' [Interfaccia della riga di comando di Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="62b22-160">You can list and download these files by using the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="62b22-161">Per altre informazioni sull'uso dell'Interfaccia della riga di comando di Azure con Archiviazione di Azure, vedere il documento [Usa Interfaccia della riga di comando di Azure 2.0 con Archiviazione di Azure](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs).</span><span class="sxs-lookup"><span data-stu-id="62b22-161">For more information on using the Azure CLI with Azure Storage, see the [Use Azure CLI 2.0 with Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) document.</span></span>

5. <span data-ttu-id="62b22-162">Usare le seguenti istruzioni per creare una nuova tabella "internal" denominata **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="62b22-162">Use the following statements to create a new 'internal' table named **errorLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="62b22-163">Le istruzioni eseguono queste azioni:</span><span class="sxs-lookup"><span data-stu-id="62b22-163">These statements perform the following actions:</span></span>

   * <span data-ttu-id="62b22-164">**CREATE TABLE IF NOT EXISTS** : crea una tabella, se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="62b22-164">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="62b22-165">Questa istruzione crea una tabella interna, che viene archiviata nel data warehouse di Hive e gestita completamente da Hive.</span><span class="sxs-lookup"><span data-stu-id="62b22-165">This statement creates an internal table, which is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="62b22-166">A differenza delle tabelle esterne, se si elimina una tabella interna, vengono eliminati anche i dati sottostanti.</span><span class="sxs-lookup"><span data-stu-id="62b22-166">Unlike external tables, dropping an internal table deletes the underlying data as well.</span></span>

   * <span data-ttu-id="62b22-167">**STORED AS ORC** : archivia i dati nel formato ORC (Optimized Row Columnar).</span><span class="sxs-lookup"><span data-stu-id="62b22-167">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="62b22-168">ORC è un formato altamente ottimizzato ed efficiente per l'archiviazione di dati Hive.</span><span class="sxs-lookup"><span data-stu-id="62b22-168">ORC is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="62b22-169">**INSERT OVERWRITE ... SELECT**: seleziona dalla tabella **log4jLogs** le righe contenenti **[ERROR]**, poi inserisce i dati nella tabella **errorLogs**.</span><span class="sxs-lookup"><span data-stu-id="62b22-169">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>
   * <span data-ttu-id="62b22-170">**SELECT**: seleziona tutte le righe della nuova tabella **errorLogs**.</span><span class="sxs-lookup"><span data-stu-id="62b22-170">**SELECT** - Selects all rows from the new **errorLogs** table.</span></span>

6. <span data-ttu-id="62b22-171">Usare l'ID processo restituito per verificare lo stato del processo.</span><span class="sxs-lookup"><span data-stu-id="62b22-171">Use the job ID returned to check the status of the job.</span></span> <span data-ttu-id="62b22-172">Se il processo è stato completato correttamente, usare l'interfaccia della riga di comando di Azure come spiegato in precedenza per scaricare e visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="62b22-172">Once it has succeeded, use the Azure CLI as described previously to download and view the results.</span></span> <span data-ttu-id="62b22-173">L'output dovrebbe contenere tre righe, tutte contenenti **ERROR**.</span><span class="sxs-lookup"><span data-stu-id="62b22-173">The output should contain three lines, all of which contain **[ERROR]**.</span></span>

## <span data-ttu-id="62b22-174"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="62b22-174"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="62b22-175">Per informazioni generali su Hive con HDInsight:</span><span class="sxs-lookup"><span data-stu-id="62b22-175">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="62b22-176">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="62b22-176">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="62b22-177">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="62b22-177">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="62b22-178">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="62b22-178">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="62b22-179">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="62b22-179">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="62b22-180">Se si usa Tez con Hive, vedere i documenti seguenti per le informazioni di debug:</span><span class="sxs-lookup"><span data-stu-id="62b22-180">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="62b22-181">Usare la vista Ambari Tez in HDInsight basato su Linux</span><span class="sxs-lookup"><span data-stu-id="62b22-181">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

<span data-ttu-id="62b22-182">Per altre informazioni sull'API REST usata in questo documento, vedere il documento [Informazioni di riferimento su WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="62b22-182">For more information on the REST API used in this document, see the [WebHCat reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.</span></span>

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




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


