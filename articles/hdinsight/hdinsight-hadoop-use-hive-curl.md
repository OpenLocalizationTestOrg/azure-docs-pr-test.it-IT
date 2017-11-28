---
title: aaaUse Hadoop Hive in HDInsight - Azure latino | Documenti Microsoft
description: Informazioni su come inviare tooremotely Pig processi tooHDInsight utilizzando Curl.
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
ms.openlocfilehash: e725829ad2adcf3540f44375e3e87b7cdaebd15e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a><span data-ttu-id="a033d-103">Esecuzione di query Hive con Hadoop in HDInsight tramite REST</span><span class="sxs-lookup"><span data-stu-id="a033d-103">Run Hive queries with Hadoop in HDInsight using REST</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="a033d-104">Informazioni su come toouse hello API REST WebHCat toorun Hive esegue una query con Hadoop in cluster HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="a033d-104">Learn how toouse hello WebHCat REST API toorun Hive queries with Hadoop on Azure HDInsight cluster.</span></span>

<span data-ttu-id="a033d-105">[CURL](http://curl.haxx.se/) è toodemonstrate usato come è possibile interagire con HDInsight mediante richieste HTTP non elaborate.</span><span class="sxs-lookup"><span data-stu-id="a033d-105">[Curl](http://curl.haxx.se/) is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests.</span></span> <span data-ttu-id="a033d-106">Hello [jq](http://stedolan.github.io/jq/) utilità viene restituiti da richieste REST i dati JSON hello tooprocess utilizzato.</span><span class="sxs-lookup"><span data-stu-id="a033d-106">hello [jq](http://stedolan.github.io/jq/) utility is used tooprocess hello JSON data returned from REST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="a033d-107">Se si ha già familiarità con i server basati su Linux, Hadoop, ma sono tooHDInsight nuovo, vedere hello [è necessario tooknow su Hadoop in HDInsight basati su Linux](hdinsight-hadoop-linux-information.md) documento.</span><span class="sxs-lookup"><span data-stu-id="a033d-107">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see hello [What you need tooknow about Hadoop on Linux-based HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>

## <span data-ttu-id="a033d-108"><a id="curl"></a>Eseguire query Hive</span><span class="sxs-lookup"><span data-stu-id="a033d-108"><a id="curl"></a>Run Hive queries</span></span>

> [!NOTE]
> <span data-ttu-id="a033d-109">Quando si utilizza cURL o qualsiasi altra comunicazione REST con WebHCat, è necessario autenticare le richieste di hello specificando nome utente hello e la password per l'amministratore del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="a033d-109">When using cURL or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span>
>
> <span data-ttu-id="a033d-110">Per i comandi hello in questa sezione, sostituire **USERNAME** con hello utente tooauthenticate toohello cluster e sostituire **PASSWORD** con password hello per account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="a033d-110">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and replace **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="a033d-111">Sostituire **CLUSTERNAME** con nome hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="a033d-111">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
>
> <span data-ttu-id="a033d-112">Hello API REST è protetto tramite [l'autenticazione di base](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="a033d-112">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="a033d-113">toohelp assicurarsi che le credenziali non sono in modo sicuro inviato toohello server, richiedere sempre tramite HTTPS (Secure HTTP).</span><span class="sxs-lookup"><span data-stu-id="a033d-113">toohelp ensure that your credentials are securely sent toohello server, always make requests by using Secure HTTP (HTTPS).</span></span>

1. <span data-ttu-id="a033d-114">Dalla riga di comando, utilizzare hello dopo che è possibile connettersi a cluster di HDInsight tooyour tooverify di comando:</span><span class="sxs-lookup"><span data-stu-id="a033d-114">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="a033d-115">Viene visualizzato un toohello simile di risposta seguente testo:</span><span class="sxs-lookup"><span data-stu-id="a033d-115">You receive a response similar toohello following text:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="a033d-116">i parametri di Hello utilizzati in questo comando sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="a033d-116">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="a033d-117">**-u** -nome utente hello e la password utilizzati richiesta hello tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="a033d-117">**-u** - hello user name and password used tooauthenticate hello request.</span></span>
   * <span data-ttu-id="a033d-118">**-G** - indica che è un'operazione GET.</span><span class="sxs-lookup"><span data-stu-id="a033d-118">**-G** - Indicates that this request is a GET operation.</span></span>

     <span data-ttu-id="a033d-119">Hello inizio hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, hello uguale per tutte le richieste.</span><span class="sxs-lookup"><span data-stu-id="a033d-119">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span> <span data-ttu-id="a033d-120">percorso di Hello, **/status**, indica che la richiesta hello è tooreturn stato WebHCat (noto anche come Templeton) per il server di hello.</span><span class="sxs-lookup"><span data-stu-id="a033d-120">hello path, **/status**, indicates that hello request is tooreturn a status of WebHCat (also known as Templeton) for hello server.</span></span> <span data-ttu-id="a033d-121">È inoltre possibile richiedere una versione di hello dell'Hive tramite hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a033d-121">You can also request hello version of Hive by using hello following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     <span data-ttu-id="a033d-122">Questa richiesta restituisce un toohello simile di risposta seguente testo:</span><span class="sxs-lookup"><span data-stu-id="a033d-122">This request returns a response similar toohello following text:</span></span>

       <span data-ttu-id="a033d-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span><span class="sxs-lookup"><span data-stu-id="a033d-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span></span>

2. <span data-ttu-id="a033d-124">Hello utilizzare seguenti una tabella denominata toocreate **log4jLogs**:</span><span class="sxs-lookup"><span data-stu-id="a033d-124">Use hello following toocreate a table named **log4jLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="a033d-125">Hello parametri utilizzati con la richiesta seguente:</span><span class="sxs-lookup"><span data-stu-id="a033d-125">hello following parameters used with this request:</span></span>

   * <span data-ttu-id="a033d-126">**-d** - dal `-G` non viene utilizzato, richiesta hello predefinite metodo POST toohello.</span><span class="sxs-lookup"><span data-stu-id="a033d-126">**-d** - Since `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="a033d-127">`-d`Specifica i valori dei dati hello vengono inviati con richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="a033d-127">`-d` specifies hello data values that are sent with hello request.</span></span>

     * <span data-ttu-id="a033d-128">**User.Name** -utente hello che esegue il comando hello.</span><span class="sxs-lookup"><span data-stu-id="a033d-128">**user.name** - hello user that is running hello command.</span></span>
     * <span data-ttu-id="a033d-129">**eseguire** -hello tooexecute istruzioni HiveQL.</span><span class="sxs-lookup"><span data-stu-id="a033d-129">**execute** - hello HiveQL statements tooexecute.</span></span>
     * <span data-ttu-id="a033d-130">**statusdir** -directory hello hello stato per questo processo viene scritto.</span><span class="sxs-lookup"><span data-stu-id="a033d-130">**statusdir** - hello directory that hello status for this job is written to.</span></span>

     <span data-ttu-id="a033d-131">Queste istruzioni consentono di eseguire hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="a033d-131">These statements perform hello following actions:</span></span>
   * <span data-ttu-id="a033d-132">**DROP TABLE** -hello tabella esiste già, viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="a033d-132">**DROP TABLE** - If hello table already exists, it is deleted.</span></span>
   * <span data-ttu-id="a033d-133">**CREATE EXTERNAL TABLE** : crea una nuova tabella "external" in Hive.</span><span class="sxs-lookup"><span data-stu-id="a033d-133">**CREATE EXTERNAL TABLE** - Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="a033d-134">Le tabelle esterne archiviano solo definizione della tabella hello nell'Hive.</span><span class="sxs-lookup"><span data-stu-id="a033d-134">External tables store only hello table definition in Hive.</span></span> <span data-ttu-id="a033d-135">dati Hello viene lasciati nella posizione originale hello.</span><span class="sxs-lookup"><span data-stu-id="a033d-135">hello data is left in hello original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="a033d-136">Le tabelle esterne da utilizzare quando si prevede di hello sottostante toobe dati aggiornati da un'origine esterna.</span><span class="sxs-lookup"><span data-stu-id="a033d-136">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="a033d-137">Ad esempio, un processo di caricamento dati automatizzato o un'altra operazione MapReduce.</span><span class="sxs-lookup"><span data-stu-id="a033d-137">For example, an automated data upload process or another MapReduce operation.</span></span>
     >
     > <span data-ttu-id="a033d-138">Eliminazione di una tabella esterna **non** eliminare dati hello e definizione della tabella solo hello.</span><span class="sxs-lookup"><span data-stu-id="a033d-138">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

   * <span data-ttu-id="a033d-139">**FORMATO di riga** - come dati hello viene formattati.</span><span class="sxs-lookup"><span data-stu-id="a033d-139">**ROW FORMAT** - How hello data is formatted.</span></span> <span data-ttu-id="a033d-140">i campi di Hello in ogni log sono separati da uno spazio.</span><span class="sxs-lookup"><span data-stu-id="a033d-140">hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="a033d-141">**ARCHIVIATO come file di testo percorso** - hello memorizzati (directory dati di esempio/hello) e a cui è archiviato come testo.</span><span class="sxs-lookup"><span data-stu-id="a033d-141">**STORED AS TEXTFILE LOCATION** - Where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="a033d-142">**Selezionare** -seleziona un conteggio di tutte le righe in cui colonna **t4** contiene il valore di hello **[errore]**.</span><span class="sxs-lookup"><span data-stu-id="a033d-142">**SELECT** - Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="a033d-143">L'istruzione dovrebbe restituire un valore pari a **3**, poiché sono presenti tre righe contenenti questo valore.</span><span class="sxs-lookup"><span data-stu-id="a033d-143">This statement returns a value of **3** as there are three rows that contain this value.</span></span>

     > [!NOTE]
     > <span data-ttu-id="a033d-144">Si noti che gli spazi di hello tra le istruzioni HiveQL vengono sostituiti da hello `+` carattere se usato con Curl.</span><span class="sxs-lookup"><span data-stu-id="a033d-144">Notice that hello spaces between HiveQL statements are replaced by hello `+` character when used with Curl.</span></span> <span data-ttu-id="a033d-145">I valori tra virgolette che contengono uno spazio, ad esempio il delimitatore di hello, non devono essere sostituiti da `+`.</span><span class="sxs-lookup"><span data-stu-id="a033d-145">Quoted values that contain a space, such as hello delimiter, should not be replaced by `+`.</span></span>

   * <span data-ttu-id="a033d-146">**INPUT__FILE__NAME come '% 25.log'** - questa istruzione limiti hello ricerca tooonly utilizza file che terminano con. log.</span><span class="sxs-lookup"><span data-stu-id="a033d-146">**INPUT__FILE__NAME LIKE '%25.log'** - This statement limits hello search tooonly use files ending in .log.</span></span>

     > [!NOTE]
     > <span data-ttu-id="a033d-147">Hello `%25` è un formato di URL codificato hello %, pertanto condizione effettiva hello è `like '%.log'`.</span><span class="sxs-lookup"><span data-stu-id="a033d-147">hello `%25` is hello URL encoded form of %, so hello actual condition is `like '%.log'`.</span></span> <span data-ttu-id="a033d-148">% Hello ha toobe URL codificato, viene considerato come un carattere speciale in URL.</span><span class="sxs-lookup"><span data-stu-id="a033d-148">hello % has toobe URL encoded, as it is treated as a special character in URLs.</span></span>

     <span data-ttu-id="a033d-149">Questo comando deve restituire un ID di processo che può essere utilizzato toocheck hello stato del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="a033d-149">This command should return a job ID that can be used toocheck hello status of hello job.</span></span>

       <span data-ttu-id="a033d-150">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="a033d-150">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="a033d-151">stato di hello toocheck del processo di hello, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a033d-151">toocheck hello status of hello job, use hello following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="a033d-152">Sostituire **JOBID** con valore hello restituito nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="a033d-152">Replace **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="a033d-153">Ad esempio, se hello restituirà valore `{"id":"job_1415651640909_0026"}`, quindi **JOBID** sarebbe `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="a033d-153">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="a033d-154">Se ha completato il processo di hello, non è stato hello **SUCCEEDED**.</span><span class="sxs-lookup"><span data-stu-id="a033d-154">If hello job has finished, hello state is **SUCCEEDED**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a033d-155">Questa richiesta Curl restituisce un documento di JavaScript Object Notation (JSON) con informazioni sul processo hello.</span><span class="sxs-lookup"><span data-stu-id="a033d-155">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job.</span></span> <span data-ttu-id="a033d-156">Viene utilizzato Jq tooretrieve hello solo valore di stato.</span><span class="sxs-lookup"><span data-stu-id="a033d-156">Jq is used tooretrieve only hello state value.</span></span>

4. <span data-ttu-id="a033d-157">Dopo aver cambiato troppo hello lo stato del processo di hello**SUCCEEDED**, è possibile recuperare i risultati di hello del processo di hello dall'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="a033d-157">Once hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="a033d-158">Hello `statusdir` parametro passato con query hello contiene percorso hello hello del file di output; in questo caso, **esempio/curl**.</span><span class="sxs-lookup"><span data-stu-id="a033d-158">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, **/example/curl**.</span></span> <span data-ttu-id="a033d-159">Questo indirizzo archivia l'output di hello in hello **esempio/curl** directory hello cluster di archiviazione predefinito.</span><span class="sxs-lookup"><span data-stu-id="a033d-159">This address stores hello output in hello **example/curl** directory in hello clusters default storage.</span></span>

    <span data-ttu-id="a033d-160">È possibile elencare e scaricare questi file tramite hello [CLI di Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a033d-160">You can list and download these files by using hello [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="a033d-161">Per ulteriori informazioni sull'utilizzo di hello CLI di Azure con l'archiviazione di Azure, vedere hello [Usa Azure CLI 2.0 con l'archiviazione di Azure](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) documento.</span><span class="sxs-lookup"><span data-stu-id="a033d-161">For more information on using hello Azure CLI with Azure Storage, see hello [Use Azure CLI 2.0 with Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) document.</span></span>

5. <span data-ttu-id="a033d-162">Hello utilizzare seguendo le istruzioni toocreate 'internal' nuova tabella denominata **degli errori**:</span><span class="sxs-lookup"><span data-stu-id="a033d-162">Use hello following statements toocreate a new 'internal' table named **errorLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="a033d-163">Queste istruzioni consentono di eseguire hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="a033d-163">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="a033d-164">**CREATE TABLE IF NOT EXISTS** : crea una tabella, se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="a033d-164">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="a033d-165">Questa istruzione crea una tabella interna, che viene archiviata nel data warehouse di hello Hive e completamente gestita da Hive.</span><span class="sxs-lookup"><span data-stu-id="a033d-165">This statement creates an internal table, which is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="a033d-166">A differenza delle tabelle esterne, eliminazione di una tabella interna Elimina hello anche i dati sottostanti.</span><span class="sxs-lookup"><span data-stu-id="a033d-166">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

   * <span data-ttu-id="a033d-167">**ARCHIVIATI AS ORC** -archivia i dati di hello in formato con ottimizzazione per la riga a colonne (ORC).</span><span class="sxs-lookup"><span data-stu-id="a033d-167">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="a033d-168">ORC è un formato altamente ottimizzato ed efficiente per l'archiviazione di dati Hive.</span><span class="sxs-lookup"><span data-stu-id="a033d-168">ORC is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="a033d-169">**INSERT OVERWRITE ... Selezionare** -seleziona le righe da hello **log4jLogs** tabella contenenti **[errore]**, quindi inserisce dati di hello in hello **degli errori** tabella.</span><span class="sxs-lookup"><span data-stu-id="a033d-169">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>
   * <span data-ttu-id="a033d-170">**Selezionare** -Seleziona tutte le righe da hello nuovo **degli errori** tabella.</span><span class="sxs-lookup"><span data-stu-id="a033d-170">**SELECT** - Selects all rows from hello new **errorLogs** table.</span></span>

6. <span data-ttu-id="a033d-171">Utilizzare l'ID di processo hello toocheck hello stato del processo di hello restituito.</span><span class="sxs-lookup"><span data-stu-id="a033d-171">Use hello job ID returned toocheck hello status of hello job.</span></span> <span data-ttu-id="a033d-172">Una volta completata, utilizzare hello CLI di Azure come descritto in precedenza toodownload e visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="a033d-172">Once it has succeeded, use hello Azure CLI as described previously toodownload and view hello results.</span></span> <span data-ttu-id="a033d-173">output di Hello deve contenere tre righe, ciascuna delle quali contiene **[errore]**.</span><span class="sxs-lookup"><span data-stu-id="a033d-173">hello output should contain three lines, all of which contain **[ERROR]**.</span></span>

## <span data-ttu-id="a033d-174"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a033d-174"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="a033d-175">Per informazioni generali su Hive con HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a033d-175">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="a033d-176">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="a033d-176">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="a033d-177">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a033d-177">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="a033d-178">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="a033d-178">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="a033d-179">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="a033d-179">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="a033d-180">Se si utilizza Tez con Hive, vedere hello documenti per le informazioni di debug seguenti:</span><span class="sxs-lookup"><span data-stu-id="a033d-180">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="a033d-181">Utilizzare hello vista Ambari Tez in HDInsight basati su Linux</span><span class="sxs-lookup"><span data-stu-id="a033d-181">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

<span data-ttu-id="a033d-182">Per ulteriori informazioni sull'API REST utilizzato in questo documento hello, vedere hello [WebHCat riferimento](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) documento.</span><span class="sxs-lookup"><span data-stu-id="a033d-182">For more information on hello REST API used in this document, see hello [WebHCat reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.</span></span>

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


