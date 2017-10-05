---
title: Analizzare ed elaborare documenti JSON con Hive in HDInsight | Microsoft Docs
description: Informazioni su come usare e analizzare i documenti JSON usando Hive in HDInsight.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e17794e8-faae-4264-9434-67f61ea78f13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2017
ms.author: jgao
ms.openlocfilehash: bd136afebeceb0cd9c24cfc5f15601caa80a755e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a><span data-ttu-id="bce55-103">Elaborare e analizzare documenti JSON usando Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="bce55-103">Process and analyze JSON documents using Hive in HDInsight</span></span>

<span data-ttu-id="bce55-104">Informazioni su come elaborare e analizzare file JSON usando Hive in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bce55-104">Learn how to process and analyze JSON files using Hive in HDInsight.</span></span> <span data-ttu-id="bce55-105">Nell'esercitazione viene usato il documento JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="bce55-105">The following JSON document is used in the tutorial:</span></span>

    {
        "StudentId": "trgfg-5454-fdfdg-4346",
        "Grade": 7,
        "StudentDetails": [
            {
                "FirstName": "Peggy",
                "LastName": "Williams",
                "YearJoined": 2012
            }
        ],
        "StudentClassCollection": [
            {
                "ClassId": "89084343",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "High",
                "Score": 93,
                "PerformedActivity": false
            },
            {
                "ClassId": "78547522",
                "ClassParticipation": "NotSatisfied",
                "ClassParticipationRank": "None",
                "Score": 74,
                "PerformedActivity": false
            },
            {
                "ClassId": "78675563",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "Low",
                "Score": 83,
                "PerformedActivity": true
            }
        ]
    }

<span data-ttu-id="bce55-106">Il file è disponibile in wasb://processjson@hditutorialdata.blob.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="bce55-106">The file can be found at wasb://processjson@hditutorialdata.blob.core.windows.net/.</span></span> <span data-ttu-id="bce55-107">Per altre informazioni sull'uso dell'archivio BLOB di Azure con HDInsight, vedere [Usare un archivio BLOB di Azure compatibile con HDFS con Hadoop in HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="bce55-107">For more information on using Azure Blob storage with HDInsight, see [Use HDFS-compatible Azure Blob storage with Hadoop in HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="bce55-108">È possibile copiare il file nel contenitore predefinito del cluster.</span><span class="sxs-lookup"><span data-stu-id="bce55-108">You can copy the file to the default container of your cluster.</span></span>

<span data-ttu-id="bce55-109">In questa esercitazione viene usata la console di Hive.</span><span class="sxs-lookup"><span data-stu-id="bce55-109">In this tutorial, you use the Hive console.</span></span>  <span data-ttu-id="bce55-110">Per istruzioni sull'apertura della console Hive, vedere [Usare Hive con Hadoop in HDInsight con Desktop remoto](hdinsight-hadoop-use-hive-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="bce55-110">For instructions of opening the Hive console, see [Use Hive with Hadoop on HDInsight with Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md).</span></span>

## <a name="flatten-json-documents"></a><span data-ttu-id="bce55-111">Rendere flat i documenti JSON</span><span class="sxs-lookup"><span data-stu-id="bce55-111">Flatten JSON documents</span></span>
<span data-ttu-id="bce55-112">I metodi elencati nella sezione seguente presuppongono che il documento JSON sia in una singola riga.</span><span class="sxs-lookup"><span data-stu-id="bce55-112">The methods listed in the next section require the JSON document in a single row.</span></span> <span data-ttu-id="bce55-113">È quindi necessario rendere flat il documento JSON in una stringa.</span><span class="sxs-lookup"><span data-stu-id="bce55-113">So you must flatten the JSON document to a string.</span></span> <span data-ttu-id="bce55-114">Se il documento JSON è già flat, è possibile saltare questo passaggio e passare alla sezione successiva relativa all'analisi dei dati JSON.</span><span class="sxs-lookup"><span data-stu-id="bce55-114">If your JSON document is already flattened, you can skip this step and go straight to the next section on Analyzing JSON data.</span></span>

    DROP TABLE IF EXISTS StudentsRaw;
    CREATE EXTERNAL TABLE StudentsRaw (textcol string) STORED AS TEXTFILE LOCATION "wasb://processjson@hditutorialdata.blob.core.windows.net/";

    DROP TABLE IF EXISTS StudentsOneLine;
    CREATE EXTERNAL TABLE StudentsOneLine
    (
      json_body string
    )
    STORED AS TEXTFILE LOCATION '/json/students';

    INSERT OVERWRITE TABLE StudentsOneLine
    SELECT CONCAT_WS(' ',COLLECT_LIST(textcol)) AS singlelineJSON
          FROM (SELECT INPUT__FILE__NAME,BLOCK__OFFSET__INSIDE__FILE, textcol FROM StudentsRaw DISTRIBUTE BY INPUT__FILE__NAME SORT BY BLOCK__OFFSET__INSIDE__FILE) x
          GROUP BY INPUT__FILE__NAME;

    SELECT * FROM StudentsOneLine

<span data-ttu-id="bce55-115">Il file JSON non elaborato è disponibile in **wasb://processjson@hditutorialdata.blob.core.windows.net/**.</span><span class="sxs-lookup"><span data-stu-id="bce55-115">The raw JSON file is located at **wasb://processjson@hditutorialdata.blob.core.windows.net/**.</span></span> <span data-ttu-id="bce55-116">La tabella Hive *StudentsRaw* punta al documento JSON non elaborato e non flat.</span><span class="sxs-lookup"><span data-stu-id="bce55-116">The *StudentsRaw* Hive table points to the raw unflattened JSON document.</span></span>

<span data-ttu-id="bce55-117">La tabella Hive *StudentsOneLine* archivia i dati nel file system predefinito di HDInsight nel percorso */json/students/*.</span><span class="sxs-lookup"><span data-stu-id="bce55-117">The *StudentsOneLine* Hive table stores the data in the HDInsight default file system under the */json/students/* path.</span></span>

<span data-ttu-id="bce55-118">L'istruzione INSERT popola la tabella StudentOneLine con i dati JSON flat.</span><span class="sxs-lookup"><span data-stu-id="bce55-118">The INSERT statement populates the StudentOneLine table with the flattened JSON data.</span></span>

<span data-ttu-id="bce55-119">L'istruzione SELECT restituirà solo una riga.</span><span class="sxs-lookup"><span data-stu-id="bce55-119">The SELECT statement shall only return one row.</span></span>

<span data-ttu-id="bce55-120">Ecco l'output dell'istruzione SELECT:</span><span class="sxs-lookup"><span data-stu-id="bce55-120">Here is the output of the SELECT statement:</span></span>

![Rendere flat il documento JSON.][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a><span data-ttu-id="bce55-122">Analizzare i documenti JSON in Hive</span><span class="sxs-lookup"><span data-stu-id="bce55-122">Analyze JSON documents in Hive</span></span>
<span data-ttu-id="bce55-123">Hive offre tre meccanismi diversi per l'esecuzione di query nei documenti JSON:</span><span class="sxs-lookup"><span data-stu-id="bce55-123">Hive provides three different mechanisms to run queries on JSON documents:</span></span>

* <span data-ttu-id="bce55-124">Usare la funzione definita dall'utente GET\_JSON\_OBJECT UDF.</span><span class="sxs-lookup"><span data-stu-id="bce55-124">use the GET\_JSON\_OBJECT UDF (User-defined function)</span></span>
* <span data-ttu-id="bce55-125">Usare la funzione definita dall'utente JSON_TUPLE.</span><span class="sxs-lookup"><span data-stu-id="bce55-125">use the JSON_TUPLE UDF</span></span>
* <span data-ttu-id="bce55-126">Usare l'interfaccia SerDe personalizzata.</span><span class="sxs-lookup"><span data-stu-id="bce55-126">use custom SerDe</span></span>
* <span data-ttu-id="bce55-127">Scrivere una funzione definita dall'utente personalizzata usando Python o altri linguaggi.</span><span class="sxs-lookup"><span data-stu-id="bce55-127">write you own UDF using Python or other languages.</span></span> <span data-ttu-id="bce55-128">Vedere [questo articolo][hdinsight-python] sull'esecuzione del codice Python personalizzato con Hive.</span><span class="sxs-lookup"><span data-stu-id="bce55-128">See [this article][hdinsight-python] on running your own Python code with Hive.</span></span>

### <a name="use-the-getjsonobject-udf"></a><span data-ttu-id="bce55-129">Usare la funzione definita dall'utente GET\_JSON_OBJECT</span><span class="sxs-lookup"><span data-stu-id="bce55-129">Use the GET\_JSON_OBJECT UDF</span></span>
<span data-ttu-id="bce55-130">Hive offre una funzione definita dall'utente predefinita denominata [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object) in grado di eseguire query JSON in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="bce55-130">Hive provides a built-in UDF called [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), which can perform JSON querying during run time.</span></span> <span data-ttu-id="bce55-131">Questo metodo accetta due argomenti, ovvero il nome della tabella e il nome del metodo che include il documento JSON flat e il campo JSON da analizzare.</span><span class="sxs-lookup"><span data-stu-id="bce55-131">This method takes two arguments – the table name and method name, which has the flattened JSON document and the JSON field that needs to be parsed.</span></span> <span data-ttu-id="bce55-132">L'esempio seguente illustra il funzionamento di questa funzione definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="bce55-132">Let’s look at an example to see how this UDF works.</span></span>

<span data-ttu-id="bce55-133">Ottenere il nome e il cognome di ogni studente</span><span class="sxs-lookup"><span data-stu-id="bce55-133">Get the first name and last name for each student</span></span>

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

<span data-ttu-id="bce55-134">Questo è l'output ottenuto quando si esegue la query nella finestra della console.</span><span class="sxs-lookup"><span data-stu-id="bce55-134">Here is the output when running this query in console window.</span></span>

![Funzione definita dall'utente get_json_object][image-hdi-hivejson-getjsonobject]

<span data-ttu-id="bce55-136">La funzione definita dall'utente get-json_object presenta alcune limitazioni.</span><span class="sxs-lookup"><span data-stu-id="bce55-136">There are a few limitations of the get-json_object UDF.</span></span>

* <span data-ttu-id="bce55-137">Poiché ogni campo della query richiede una nuova analisi della query, si ha un impatto sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="bce55-137">Because each field in the query requires reparsing the query, it affects the performance.</span></span>
* <span data-ttu-id="bce55-138">GET\_JSON_OBJECT() restituisce la rappresentazione di stringa di una matrice.</span><span class="sxs-lookup"><span data-stu-id="bce55-138">GET\_JSON_OBJECT() returns the string representation of an array.</span></span> <span data-ttu-id="bce55-139">Per convertirla in una matrice Hive, è necessario usare espressioni regolari per sostituire le parentesi quadre ('[' e ']') e quindi chiamare anche una suddivisione per ottenere la matrice.</span><span class="sxs-lookup"><span data-stu-id="bce55-139">To convert this array to a Hive array, you have to use regular expressions to replace the square brackets ‘[‘ and ‘]’ and then also call split to get the array.</span></span>

<span data-ttu-id="bce55-140">Il wiki relativo a Hive consiglia quindi di usare json_tuple, come illustrato più avanti.</span><span class="sxs-lookup"><span data-stu-id="bce55-140">This is why the Hive wiki recommends using json_tuple.</span></span>  

### <a name="use-the-jsontuple-udf"></a><span data-ttu-id="bce55-141">Usare la funzione definita dall'utente JSON_TUPLE</span><span class="sxs-lookup"><span data-stu-id="bce55-141">Use the JSON_TUPLE UDF</span></span>
<span data-ttu-id="bce55-142">L'altra funzione definita dall'utente disponibile in Hive è denominata [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple) e offre prestazioni migliori rispetto a [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span><span class="sxs-lookup"><span data-stu-id="bce55-142">Another UDF provided by Hive is called [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), which performs better than [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span></span> <span data-ttu-id="bce55-143">Questo metodo accetta un insieme di chiavi e una stringa JSON e restituisce una tupla di valori usando una funzione.</span><span class="sxs-lookup"><span data-stu-id="bce55-143">This method takes a set of keys and a JSON string, and returns a tuple of values using one function.</span></span> <span data-ttu-id="bce55-144">La query seguente restituisce l'ID dello studente e il livello dal documento JSON:</span><span class="sxs-lookup"><span data-stu-id="bce55-144">The following query returns the student id and the grade from the JSON document:</span></span>

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

<span data-ttu-id="bce55-145">Output dello script nella console di Hive:</span><span class="sxs-lookup"><span data-stu-id="bce55-145">The output of this script in the Hive console:</span></span>

![Funzione definita dall'utente json_tuple][image-hdi-hivejson-jsontuple]

<span data-ttu-id="bce55-147">JSON\_TUPLE usa la sintassi di tipo [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) in Hive, che consente a json\_tuple di creare una tabella virtuale applicando la funzione UDT a ogni riga della tabella originale.</span><span class="sxs-lookup"><span data-stu-id="bce55-147">JSON\_TUPLE uses the [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) syntax in Hive, which allows json\_tuple to create a virtual table by applying the UDT function to each row of the original table.</span></span>  <span data-ttu-id="bce55-148">I documenti JSON complessi diventano troppo difficili da gestire a causa dell'uso ripetuto di LATERAL VIEW.</span><span class="sxs-lookup"><span data-stu-id="bce55-148">Complex JSONs become too unwieldy because of the repeated use of LATERAL VIEW.</span></span> <span data-ttu-id="bce55-149">JSON_TUPLE non è in grado di gestire documenti JSON annidati.</span><span class="sxs-lookup"><span data-stu-id="bce55-149">Furthermore, JSON_TUPLE cannot handle nested JSONs.</span></span>

### <a name="use-custom-serde"></a><span data-ttu-id="bce55-150">Usare l'interfaccia SerDe personalizzata</span><span class="sxs-lookup"><span data-stu-id="bce55-150">Use custom SerDe</span></span>
<span data-ttu-id="bce55-151">SerDe è la scelta migliore per l'analisi di documenti JSON annidati, perché consente di definire lo schema JSON e di usarlo per analizzare i documenti.</span><span class="sxs-lookup"><span data-stu-id="bce55-151">SerDe is the best choice for parsing nested JSON documents, it allows you to define the JSON schema, and use the schema to parse the documents.</span></span> <span data-ttu-id="bce55-152">In questa esercitazione viene usata una delle interfacce SerDe più diffuse, sviluppata da [rcongiu](https://github.com/rcongiu).</span><span class="sxs-lookup"><span data-stu-id="bce55-152">In this tutorial, you use one of the more popular SerDe that has been developed by [Roberto Congiu](https://github.com/rcongiu).</span></span>

<span data-ttu-id="bce55-153">**Per usare l'interfaccia SerDe personalizzata:**</span><span class="sxs-lookup"><span data-stu-id="bce55-153">**To use the custom SerDe:**</span></span>

1. <span data-ttu-id="bce55-154">Installare [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span><span class="sxs-lookup"><span data-stu-id="bce55-154">Install [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span></span> <span data-ttu-id="bce55-155">Se si usa la distribuzione Windows di HDInsight, scegliere la versione Windows X64 del JDK.</span><span class="sxs-lookup"><span data-stu-id="bce55-155">Choose the Windows X64 version of the JDK if you are going to be using the Windows deployment of HDInsight</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="bce55-156">JDK 1.8 non funziona con questa SerDe.</span><span class="sxs-lookup"><span data-stu-id="bce55-156">JDK 1.8 doesn't work with this SerDe.</span></span>
   > 
   > 
   
    <span data-ttu-id="bce55-157">Al termine dell'installazione, aggiungere una nuova variabile di ambiente utente:</span><span class="sxs-lookup"><span data-stu-id="bce55-157">After the installation is completed, add a new user environment variable:</span></span>
   
   1. <span data-ttu-id="bce55-158">Aprire **Visualizza impostazioni di sistema avanzate** dalla schermata di Windows.</span><span class="sxs-lookup"><span data-stu-id="bce55-158">Open **View advanced system settings** from the Windows screen.</span></span>
   2. <span data-ttu-id="bce55-159">Fare clic su **Variabili di ambiente**.</span><span class="sxs-lookup"><span data-stu-id="bce55-159">Click **Environment Variables**.</span></span>  
   3. <span data-ttu-id="bce55-160">Aggiungere una nuova variabile di ambiente **JAVA_HOME** che punta a **C:\Programmi\Java\jdk1.7.0_55** o al percorso di installazione del JDK.</span><span class="sxs-lookup"><span data-stu-id="bce55-160">Add a new **JAVA_HOME** environment variable is pointing to **C:\Program Files\Java\jdk1.7.0_55** or wherever your JDK is installed.</span></span>
      
      ![Configurazione dei valori di configurazione corretti per JDK][image-hdi-hivejson-jdk]
2. <span data-ttu-id="bce55-162">Installare [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span><span class="sxs-lookup"><span data-stu-id="bce55-162">Install [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span></span>
   
    <span data-ttu-id="bce55-163">Aggiungere la cartella Bin al percorso scegliendo Pannello di controllo-->Modifica le variabili di ambiente relative al sistema per l'account, quindi scegliere Variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="bce55-163">Add the bin folder to your path by going to Control Panel-->Edit the System Variables for your account Environment variables.</span></span> <span data-ttu-id="bce55-164">La schermata seguente illustra come eseguire questa operazione.</span><span class="sxs-lookup"><span data-stu-id="bce55-164">The following screenshot shows you how to do this.</span></span>
   
    ![Configurazione di Maven][image-hdi-hivejson-maven]
3. <span data-ttu-id="bce55-166">Clonare il progetto dal sito GitHub [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) .</span><span class="sxs-lookup"><span data-stu-id="bce55-166">Clone the project from [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github site.</span></span> <span data-ttu-id="bce55-167">Per eseguire questa operazione, fare clic sul pulsante "Download Zip", come illustrato nella schermata seguente.</span><span class="sxs-lookup"><span data-stu-id="bce55-167">You can do this by clicking on the “Download Zip” button as shown in the following screenshot.</span></span>
   
    ![Clonazione del progetto][image-hdi-hivejson-serde]

<span data-ttu-id="bce55-169">4: Passare alla cartella in cui è stato scaricato il pacchetto e quindi digitare "mvn package".</span><span class="sxs-lookup"><span data-stu-id="bce55-169">4: Go to the folder where you have downloaded this package and then type “mvn package”.</span></span> <span data-ttu-id="bce55-170">Verranno creati i file jar necessari, che verranno quindi copiati nel cluster.</span><span class="sxs-lookup"><span data-stu-id="bce55-170">This should create the necessary jar files that you can then copy over to the cluster.</span></span>

<span data-ttu-id="bce55-171">5: Passare alla cartella di destinazione nella cartella radice in cui è stato scaricato il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bce55-171">5: Go to the target folder under the root folder where you downloaded the package.</span></span> <span data-ttu-id="bce55-172">Caricare il file json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar nel nodo head del cluster.</span><span class="sxs-lookup"><span data-stu-id="bce55-172">Upload the json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar file to head-node of your cluster.</span></span> <span data-ttu-id="bce55-173">È in genere consigliabile inserirlo sotto la cartella dei file binari di Hive, ad esempio C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin o in una cartella analoga.</span><span class="sxs-lookup"><span data-stu-id="bce55-173">I usually put it under the hive binary folder: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin or something similar.</span></span>

<span data-ttu-id="bce55-174">6: Al prompt di Hive digitare "add jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar".</span><span class="sxs-lookup"><span data-stu-id="bce55-174">6: In the hive prompt, type “add jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar”.</span></span> <span data-ttu-id="bce55-175">Poiché in questo esempio il file jar si trova nella cartella C:\apps\dist\hive-0.13.x\bin, è possibile aggiungere direttamente il file jar con il nome, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="bce55-175">Since in my case, the jar is in the C:\apps\dist\hive-0.13.x\bin folder, I can directly add the jar with the name as shown:</span></span>

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![Aggiunta di JAR al progetto][image-hdi-hivejson-addjar]

<span data-ttu-id="bce55-177">A questo punto è possibile usare SerDe per eseguire le query sul documento JSON.</span><span class="sxs-lookup"><span data-stu-id="bce55-177">Now, you are ready to use the SerDe to run queries against the JSON document.</span></span>

<span data-ttu-id="bce55-178">L'istruzione seguente crea una tabella con uno schema definito:</span><span class="sxs-lookup"><span data-stu-id="bce55-178">The following statement creates a table with a defined schema:</span></span>

    DROP TABLE json_table;
    CREATE EXTERNAL TABLE json_table (
      StudentId string,
      Grade int,
      StudentDetails array<struct<
          FirstName:string,
          LastName:string,
          YearJoined:int
          >
      >,
      StudentClassCollection array<struct<
          ClassId:string,
          ClassParticipation:string,
          ClassParticipationRank:string,
          Score:int,
          PerformedActivity:boolean
          >
      >
    ) ROW FORMAT SERDE 'org.openx.data.jsonserde.JsonSerDe'
    LOCATION '/json/students';

<span data-ttu-id="bce55-179">Per elencare il nome e il cognome dello studente</span><span class="sxs-lookup"><span data-stu-id="bce55-179">To list the first name and last name of the student</span></span>

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

<span data-ttu-id="bce55-180">Questo è il risultato ottenuto dalla console di Hive.</span><span class="sxs-lookup"><span data-stu-id="bce55-180">Here is the result from the Hive console.</span></span>

![Query SerDe 1][image-hdi-hivejson-serde_query1]

<span data-ttu-id="bce55-182">Per calcolare la somma dei punteggi del documento JSON</span><span class="sxs-lookup"><span data-stu-id="bce55-182">To calculate the sum of scores of the JSON document</span></span>

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

<span data-ttu-id="bce55-183">La query precedente usa la funzione definita dall'utente di tipo [lateral view explode](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) per espandere la matrice di punteggi, in modo che sia possibile riepilogarli.</span><span class="sxs-lookup"><span data-stu-id="bce55-183">The preceding query uses [lateral view explode](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF to expand the array of scores so that they can be summed.</span></span>

<span data-ttu-id="bce55-184">Questo è l'output ottenuto dalla console di Hive.</span><span class="sxs-lookup"><span data-stu-id="bce55-184">Here is the output from the Hive console.</span></span>

![Query SerDe 2][image-hdi-hivejson-serde_query2]

<span data-ttu-id="bce55-186">Per trovare le materie in cui un determinato studente ha ottenuto un punteggio superiore a 80:</span><span class="sxs-lookup"><span data-stu-id="bce55-186">To find which subjects a given student has scored more than 80 points:</span></span>

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

<span data-ttu-id="bce55-187">La query precedente restituisce una matrice Hive, a differenza di get\_json\_object, che restituisce una stringa.</span><span class="sxs-lookup"><span data-stu-id="bce55-187">The preceding query returns a Hive array unlike get\_json\_object, which returns a string.</span></span>

![Query SerDe 3][image-hdi-hivejson-serde_query3]

<span data-ttu-id="bce55-189">Se si vogliono ignorare documenti JSON non validi, come illustrato nella [pagina wiki](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) di questo SerDe, è possibile ottenere questo risultato con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="bce55-189">If you want to skil malformed JSON, then as explained in the [wiki page](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) of this SerDe you can achieve that by typing the following code:</span></span>  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a><span data-ttu-id="bce55-190">Summary</span><span class="sxs-lookup"><span data-stu-id="bce55-190">Summary</span></span>
<span data-ttu-id="bce55-191">In conclusione, il tipo di operatore JSON in Hive scelto dipende dallo scenario.</span><span class="sxs-lookup"><span data-stu-id="bce55-191">In conclusion, the type of JSON operator in Hive that you choose depends on your scenario.</span></span> <span data-ttu-id="bce55-192">Se è disponibile un documento JSON semplice ed è necessario eseguire ricerche in un solo campo, è possibile scegliere di usare la funzione Hive definita dall'utente get\_json\_object.</span><span class="sxs-lookup"><span data-stu-id="bce55-192">If you have a simple JSON document and you only have one field to look up on – you can choose to use the Hive UDF get\_json\_object.</span></span> <span data-ttu-id="bce55-193">Se è necessario cercare più di una chiave, è possibile usare json_tuple.</span><span class="sxs-lookup"><span data-stu-id="bce55-193">If you have more than one key to look up on, then you can use json_tuple.</span></span> <span data-ttu-id="bce55-194">Se è disponibile un documento annidato, è consigliabile usare il SerDe JSON.</span><span class="sxs-lookup"><span data-stu-id="bce55-194">If you have a nested document, then you should use the JSON SerDe.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bce55-195">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bce55-195">Next steps</span></span>

<span data-ttu-id="bce55-196">Per altri articoli correlati, vedere</span><span class="sxs-lookup"><span data-stu-id="bce55-196">For other related articles, see</span></span>

* [<span data-ttu-id="bce55-197">Usare Hive e HiveQL con Hadoop in HDInsight per analizzare un file Apache log4j di esempio</span><span class="sxs-lookup"><span data-stu-id="bce55-197">Use Hive and HiveQL with Hadoop in HDInsight to analyze a sample Apache log4j file</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="bce55-198">Analizzare i dati sui ritardi dei voli mediante Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="bce55-198">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="bce55-199">Analizzare i dati Twitter mediante Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="bce55-199">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="bce55-200">Eseguire un processo Hadoop usando Azure Cosmos DB e HDInsight</span><span class="sxs-lookup"><span data-stu-id="bce55-200">Run a Hadoop job using Azure Cosmos DB and HDInsight</span></span>](../documentdb/documentdb-run-hadoop-with-hdinsight.md)

[hdinsight-python]: hdinsight-python.md

[image-hdi-hivejson-flatten]: ./media/hdinsight-using-json-in-hive/flatten.png
[image-hdi-hivejson-getjsonobject]: ./media/hdinsight-using-json-in-hive/getjsonobject.png
[image-hdi-hivejson-jsontuple]: ./media/hdinsight-using-json-in-hive/jsontuple.png
[image-hdi-hivejson-jdk]: ./media/hdinsight-using-json-in-hive/jdk.png
[image-hdi-hivejson-maven]: ./media/hdinsight-using-json-in-hive/maven.png
[image-hdi-hivejson-serde]: ./media/hdinsight-using-json-in-hive/serde.png
[image-hdi-hivejson-addjar]: ./media/hdinsight-using-json-in-hive/addjar.png
[image-hdi-hivejson-serde_query1]: ./media/hdinsight-using-json-in-hive/serde_query1.png
[image-hdi-hivejson-serde_query2]: ./media/hdinsight-using-json-in-hive/serde_query2.png
[image-hdi-hivejson-serde_query3]: ./media/hdinsight-using-json-in-hive/serde_query3.png
[image-hdi-hivejson-serde_result]: ./media/hdinsight-using-json-in-hive/serde_result.png
