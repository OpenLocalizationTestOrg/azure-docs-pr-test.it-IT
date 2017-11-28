---
title: aaaAnalyze e JSON processo documenti con Hive in HDInsight | Documenti Microsoft
description: Informazioni su come toouse JSON documenti e analizzarli mediante Hive in HDInsight.
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
ms.openlocfilehash: b4b20172e8553f91a446615dc52f2ea2ef24cd04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a><span data-ttu-id="0a744-103">Elaborare e analizzare documenti JSON usando Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a744-103">Process and analyze JSON documents using Hive in HDInsight</span></span>

<span data-ttu-id="0a744-104">Informazioni su come tooprocess e analizzare i file JSON utilizzando Hive in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0a744-104">Learn how tooprocess and analyze JSON files using Hive in HDInsight.</span></span> <span data-ttu-id="0a744-105">Hello seguente documento JSON utilizzato nell'esercitazione hello:</span><span class="sxs-lookup"><span data-stu-id="0a744-105">hello following JSON document is used in hello tutorial:</span></span>

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

<span data-ttu-id="0a744-106">file Hello è reperibile in wasb://processjson@hditutorialdata.blob.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="0a744-106">hello file can be found at wasb://processjson@hditutorialdata.blob.core.windows.net/.</span></span> <span data-ttu-id="0a744-107">Per altre informazioni sull'uso dell'archivio BLOB di Azure con HDInsight, vedere [Usare un archivio BLOB di Azure compatibile con HDFS con Hadoop in HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="0a744-107">For more information on using Azure Blob storage with HDInsight, see [Use HDFS-compatible Azure Blob storage with Hadoop in HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="0a744-108">È possibile copiare contenitore predefinito di hello file toohello del cluster.</span><span class="sxs-lookup"><span data-stu-id="0a744-108">You can copy hello file toohello default container of your cluster.</span></span>

<span data-ttu-id="0a744-109">In questa esercitazione, utilizzare una console di Hive hello.</span><span class="sxs-lookup"><span data-stu-id="0a744-109">In this tutorial, you use hello Hive console.</span></span>  <span data-ttu-id="0a744-110">Per istruzioni di apertura hello Hive console, vedere [utilizzare Hive con Hadoop in HDInsight con Desktop remoto](hdinsight-hadoop-use-hive-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="0a744-110">For instructions of opening hello Hive console, see [Use Hive with Hadoop on HDInsight with Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md).</span></span>

## <a name="flatten-json-documents"></a><span data-ttu-id="0a744-111">Rendere flat i documenti JSON</span><span class="sxs-lookup"><span data-stu-id="0a744-111">Flatten JSON documents</span></span>
<span data-ttu-id="0a744-112">metodi di Hello elencati nella sezione successiva hello richiedono hello del documento JSON in una singola riga.</span><span class="sxs-lookup"><span data-stu-id="0a744-112">hello methods listed in hello next section require hello JSON document in a single row.</span></span> <span data-ttu-id="0a744-113">Pertanto, è necessario unire stringa tooa documento JSON di hello.</span><span class="sxs-lookup"><span data-stu-id="0a744-113">So you must flatten hello JSON document tooa string.</span></span> <span data-ttu-id="0a744-114">Se il documento JSON è già bidimensionale, è possibile ignorare questo passaggio e passare la sezione successiva toohello retta sui dati di analisi di JSON.</span><span class="sxs-lookup"><span data-stu-id="0a744-114">If your JSON document is already flattened, you can skip this step and go straight toohello next section on Analyzing JSON data.</span></span>

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

<span data-ttu-id="0a744-115">Hello file JSON non elaborato si trova in  **wasb://processjson@hditutorialdata.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="0a744-115">hello raw JSON file is located at **wasb://processjson@hditutorialdata.blob.core.windows.net/**.</span></span> <span data-ttu-id="0a744-116">Hello *StudentsRaw* tabella Hive punta toohello documento JSON non convertito non elaborato.</span><span class="sxs-lookup"><span data-stu-id="0a744-116">hello *StudentsRaw* Hive table points toohello raw unflattened JSON document.</span></span>

<span data-ttu-id="0a744-117">Hello *StudentsOneLine* tabella Hive archivia i dati di hello in file system predefinito HDInsight in hello hello */jsonstudenti/* percorso.</span><span class="sxs-lookup"><span data-stu-id="0a744-117">hello *StudentsOneLine* Hive table stores hello data in hello HDInsight default file system under hello */json/students/* path.</span></span>

<span data-ttu-id="0a744-118">istruzione INSERT Hello tabella viene popolata hello StudentOneLine con i dati JSON hello bidimensionale.</span><span class="sxs-lookup"><span data-stu-id="0a744-118">hello INSERT statement populates hello StudentOneLine table with hello flattened JSON data.</span></span>

<span data-ttu-id="0a744-119">istruzione SELECT Hello dovrà restituire una sola riga.</span><span class="sxs-lookup"><span data-stu-id="0a744-119">hello SELECT statement shall only return one row.</span></span>

<span data-ttu-id="0a744-120">Ecco l'output di hello dell'istruzione SELECT hello:</span><span class="sxs-lookup"><span data-stu-id="0a744-120">Here is hello output of hello SELECT statement:</span></span>

![Conversione del documento JSON hello.][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a><span data-ttu-id="0a744-122">Analizzare i documenti JSON in Hive</span><span class="sxs-lookup"><span data-stu-id="0a744-122">Analyze JSON documents in Hive</span></span>
<span data-ttu-id="0a744-123">Hive fornisce tre diversi meccanismi toorun query su documenti JSON:</span><span class="sxs-lookup"><span data-stu-id="0a744-123">Hive provides three different mechanisms toorun queries on JSON documents:</span></span>

* <span data-ttu-id="0a744-124">Utilizzare GET hello\_JSON\_oggetto funzione definita dall'utente (funzione definita dall'utente)</span><span class="sxs-lookup"><span data-stu-id="0a744-124">use hello GET\_JSON\_OBJECT UDF (User-defined function)</span></span>
* <span data-ttu-id="0a744-125">Utilizzare hello JSON_TUPLE funzione definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="0a744-125">use hello JSON_TUPLE UDF</span></span>
* <span data-ttu-id="0a744-126">Usare l'interfaccia SerDe personalizzata.</span><span class="sxs-lookup"><span data-stu-id="0a744-126">use custom SerDe</span></span>
* <span data-ttu-id="0a744-127">Scrivere una funzione definita dall'utente personalizzata usando Python o altri linguaggi.</span><span class="sxs-lookup"><span data-stu-id="0a744-127">write you own UDF using Python or other languages.</span></span> <span data-ttu-id="0a744-128">Vedere [questo articolo][hdinsight-python] sull'esecuzione del codice Python personalizzato con Hive.</span><span class="sxs-lookup"><span data-stu-id="0a744-128">See [this article][hdinsight-python] on running your own Python code with Hive.</span></span>

### <a name="use-hello-getjsonobject-udf"></a><span data-ttu-id="0a744-129">Hello utilizzare GET\_JSON_OBJECT funzione definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="0a744-129">Use hello GET\_JSON_OBJECT UDF</span></span>
<span data-ttu-id="0a744-130">Hive offre una funzione definita dall'utente predefinita denominata [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object) in grado di eseguire query JSON in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0a744-130">Hive provides a built-in UDF called [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), which can perform JSON querying during run time.</span></span> <span data-ttu-id="0a744-131">Questo metodo accetta due argomenti: nome della tabella hello e nome del metodo, che ha hello bidimensionale JSON hello e documenti JSON campo che deve toobe analizzato.</span><span class="sxs-lookup"><span data-stu-id="0a744-131">This method takes two arguments – hello table name and method name, which has hello flattened JSON document and hello JSON field that needs toobe parsed.</span></span> <span data-ttu-id="0a744-132">Esaminiamo un esempio toosee funzionamento di questa funzione definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="0a744-132">Let’s look at an example toosee how this UDF works.</span></span>

<span data-ttu-id="0a744-133">Ottenere hello nome e cognome di ogni studente</span><span class="sxs-lookup"><span data-stu-id="0a744-133">Get hello first name and last name for each student</span></span>

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

<span data-ttu-id="0a744-134">Ecco output di hello quando si esegue questa query nella finestra della console.</span><span class="sxs-lookup"><span data-stu-id="0a744-134">Here is hello output when running this query in console window.</span></span>

![Funzione definita dall'utente get_json_object][image-hdi-hivejson-getjsonobject]

<span data-ttu-id="0a744-136">Esistono alcune limitazioni di get-json_object hello funzione definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="0a744-136">There are a few limitations of hello get-json_object UDF.</span></span>

* <span data-ttu-id="0a744-137">Poiché ogni campo nella query hello richiede vuoti query hello, influisce sulle prestazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="0a744-137">Because each field in hello query requires reparsing hello query, it affects hello performance.</span></span>
* <span data-ttu-id="0a744-138">OTTENERE\_JSON_OBJECT() restituisce la rappresentazione di stringa hello di una matrice.</span><span class="sxs-lookup"><span data-stu-id="0a744-138">GET\_JSON_OBJECT() returns hello string representation of an array.</span></span> <span data-ttu-id="0a744-139">tooconvert questa matrice di matrice tooa Hive, aver toouse espressioni regolari tooreplace hello parentesi quadre "[' e ']' e quindi anche chiamata divisione matrice hello tooget.</span><span class="sxs-lookup"><span data-stu-id="0a744-139">tooconvert this array tooa Hive array, you have toouse regular expressions tooreplace hello square brackets ‘[‘ and ‘]’ and then also call split tooget hello array.</span></span>

<span data-ttu-id="0a744-140">Ecco perché hello Hive wiki consiglia l'uso di json_tuple.</span><span class="sxs-lookup"><span data-stu-id="0a744-140">This is why hello Hive wiki recommends using json_tuple.</span></span>  

### <a name="use-hello-jsontuple-udf"></a><span data-ttu-id="0a744-141">Utilizzare hello JSON_TUPLE funzione definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="0a744-141">Use hello JSON_TUPLE UDF</span></span>
<span data-ttu-id="0a744-142">L'altra funzione definita dall'utente disponibile in Hive è denominata [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple) e offre prestazioni migliori rispetto a [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span><span class="sxs-lookup"><span data-stu-id="0a744-142">Another UDF provided by Hive is called [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), which performs better than [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span></span> <span data-ttu-id="0a744-143">Questo metodo accetta un insieme di chiavi e una stringa JSON e restituisce una tupla di valori usando una funzione.</span><span class="sxs-lookup"><span data-stu-id="0a744-143">This method takes a set of keys and a JSON string, and returns a tuple of values using one function.</span></span> <span data-ttu-id="0a744-144">Hello query seguente restituisce id dello studente hello e livello di hello da un documento JSON hello:</span><span class="sxs-lookup"><span data-stu-id="0a744-144">hello following query returns hello student id and hello grade from hello JSON document:</span></span>

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

<span data-ttu-id="0a744-145">output di Hello dello script nella console di Hive hello:</span><span class="sxs-lookup"><span data-stu-id="0a744-145">hello output of this script in hello Hive console:</span></span>

![Funzione definita dall'utente json_tuple][image-hdi-hivejson-jsontuple]

<span data-ttu-id="0a744-147">JSON\_TUPLA utilizza hello [laterali vista](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) sintassi nell'Hive, che consente di json\_tupla toocreate una tabella virtuale applicando hello UDT funzione tooeach riga della tabella originale hello.</span><span class="sxs-lookup"><span data-stu-id="0a744-147">JSON\_TUPLE uses hello [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) syntax in Hive, which allows json\_tuple toocreate a virtual table by applying hello UDT function tooeach row of hello original table.</span></span>  <span data-ttu-id="0a744-148">Documenti JSON complessi diventare troppo difficile da gestire a causa di hello ripetuto l'utilizzo di visualizzazione laterale.</span><span class="sxs-lookup"><span data-stu-id="0a744-148">Complex JSONs become too unwieldy because of hello repeated use of LATERAL VIEW.</span></span> <span data-ttu-id="0a744-149">JSON_TUPLE non è in grado di gestire documenti JSON annidati.</span><span class="sxs-lookup"><span data-stu-id="0a744-149">Furthermore, JSON_TUPLE cannot handle nested JSONs.</span></span>

### <a name="use-custom-serde"></a><span data-ttu-id="0a744-150">Usare l'interfaccia SerDe personalizzata</span><span class="sxs-lookup"><span data-stu-id="0a744-150">Use custom SerDe</span></span>
<span data-ttu-id="0a744-151">SerDe sia hello migliore per l'analisi dei documenti JSON annidati, ma consente toodefine hello JSON schema e utilizzare hello schema tooparse hello documenti.</span><span class="sxs-lookup"><span data-stu-id="0a744-151">SerDe is hello best choice for parsing nested JSON documents, it allows you toodefine hello JSON schema, and use hello schema tooparse hello documents.</span></span> <span data-ttu-id="0a744-152">In questa esercitazione, utilizzare uno dei hello SerDe più comuni che è stato sviluppato da [Roberto Congiu](https://github.com/rcongiu).</span><span class="sxs-lookup"><span data-stu-id="0a744-152">In this tutorial, you use one of hello more popular SerDe that has been developed by [Roberto Congiu](https://github.com/rcongiu).</span></span>

<span data-ttu-id="0a744-153">**toouse hello SerDe personalizzato:**</span><span class="sxs-lookup"><span data-stu-id="0a744-153">**toouse hello custom SerDe:**</span></span>

1. <span data-ttu-id="0a744-154">Installare [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span><span class="sxs-lookup"><span data-stu-id="0a744-154">Install [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span></span> <span data-ttu-id="0a744-155">Scegliere hello JDK versione X64 di Windows hello se si sta utilizzando la distribuzione di Windows hello di HDInsight toobe</span><span class="sxs-lookup"><span data-stu-id="0a744-155">Choose hello Windows X64 version of hello JDK if you are going toobe using hello Windows deployment of HDInsight</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="0a744-156">JDK 1.8 non funziona con questa SerDe.</span><span class="sxs-lookup"><span data-stu-id="0a744-156">JDK 1.8 doesn't work with this SerDe.</span></span>
   > 
   > 
   
    <span data-ttu-id="0a744-157">Al termine dell'installazione di hello, aggiungere una nuova variabile di ambiente utente:</span><span class="sxs-lookup"><span data-stu-id="0a744-157">After hello installation is completed, add a new user environment variable:</span></span>
   
   1. <span data-ttu-id="0a744-158">Aprire **Visualizza impostazioni di sistema avanzate** dalla schermata di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="0a744-158">Open **View advanced system settings** from hello Windows screen.</span></span>
   2. <span data-ttu-id="0a744-159">Fare clic su **Variabili di ambiente**.</span><span class="sxs-lookup"><span data-stu-id="0a744-159">Click **Environment Variables**.</span></span>  
   3. <span data-ttu-id="0a744-160">Aggiungere un nuovo **JAVA_HOME** variabile di ambiente punta troppo**Files\Java\jdk1.7.0_55 c:\Programmi\Microsoft** o punto in cui è installato il pacchetto JDK.</span><span class="sxs-lookup"><span data-stu-id="0a744-160">Add a new **JAVA_HOME** environment variable is pointing too**C:\Program Files\Java\jdk1.7.0_55** or wherever your JDK is installed.</span></span>
      
      ![Configurazione dei valori di configurazione corretti per JDK][image-hdi-hivejson-jdk]
2. <span data-ttu-id="0a744-162">Installare [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span><span class="sxs-lookup"><span data-stu-id="0a744-162">Install [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span></span>
   
    <span data-ttu-id="0a744-163">Aggiungi percorso tooyour della cartella bin hello passando tooControl pannello--> Modifica le variabili di sistema di hello per le variabili di ambiente account.</span><span class="sxs-lookup"><span data-stu-id="0a744-163">Add hello bin folder tooyour path by going tooControl Panel-->Edit hello System Variables for your account Environment variables.</span></span> <span data-ttu-id="0a744-164">Hello cattura di schermata seguente illustra come toodo questo.</span><span class="sxs-lookup"><span data-stu-id="0a744-164">hello following screenshot shows you how toodo this.</span></span>
   
    ![Configurazione di Maven][image-hdi-hivejson-maven]
3. <span data-ttu-id="0a744-166">Progetto hello clone da [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) sito github.</span><span class="sxs-lookup"><span data-stu-id="0a744-166">Clone hello project from [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github site.</span></span> <span data-ttu-id="0a744-167">È possibile farlo facendo clic sul pulsante "Download Zip" hello come illustrato nella seguente schermata hello.</span><span class="sxs-lookup"><span data-stu-id="0a744-167">You can do this by clicking on hello “Download Zip” button as shown in hello following screenshot.</span></span>
   
    ![La clonazione progetto hello][image-hdi-hivejson-serde]

<span data-ttu-id="0a744-169">4: go toohello cartella in cui è stato scaricato il pacchetto e quindi il tipo "mvn pacchetto".</span><span class="sxs-lookup"><span data-stu-id="0a744-169">4: Go toohello folder where you have downloaded this package and then type “mvn package”.</span></span> <span data-ttu-id="0a744-170">Si deve creare hello file jar necessarie che è quindi possibile copiare su toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="0a744-170">This should create hello necessary jar files that you can then copy over toohello cluster.</span></span>

<span data-ttu-id="0a744-171">5: cartella di destinazione toohello andare nella cartella radice hello in cui è stato scaricato il pacchetto di hello.</span><span class="sxs-lookup"><span data-stu-id="0a744-171">5: Go toohello target folder under hello root folder where you downloaded hello package.</span></span> <span data-ttu-id="0a744-172">Caricare file json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar hello toohead-nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="0a744-172">Upload hello json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar file toohead-node of your cluster.</span></span> <span data-ttu-id="0a744-173">In genere inserirlo nella cartella di hello hive binari: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin o simile.</span><span class="sxs-lookup"><span data-stu-id="0a744-173">I usually put it under hello hive binary folder: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin or something similar.</span></span>

<span data-ttu-id="0a744-174">6: nel prompt dei comandi hive hello, digitare "Aggiungi jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar".</span><span class="sxs-lookup"><span data-stu-id="0a744-174">6: In hello hive prompt, type “add jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar”.</span></span> <span data-ttu-id="0a744-175">Poiché in questo caso, jar hello nella cartella C:\apps\dist\hive-0.13.x\bin hello, è possibile aggiungere direttamente jar hello con nome hello, come illustrato:</span><span class="sxs-lookup"><span data-stu-id="0a744-175">Since in my case, hello jar is in hello C:\apps\dist\hive-0.13.x\bin folder, I can directly add hello jar with hello name as shown:</span></span>

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![Aggiunta di file JAR tooyour progetto][image-hdi-hivejson-addjar]

<span data-ttu-id="0a744-177">A questo punto, si è pronti toouse hello SerDe toorun query documento JSON hello.</span><span class="sxs-lookup"><span data-stu-id="0a744-177">Now, you are ready toouse hello SerDe toorun queries against hello JSON document.</span></span>

<span data-ttu-id="0a744-178">Hello istruzione crea una tabella con uno schema definito:</span><span class="sxs-lookup"><span data-stu-id="0a744-178">hello following statement creates a table with a defined schema:</span></span>

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

<span data-ttu-id="0a744-179">toolist hello nome e cognome di hello studente</span><span class="sxs-lookup"><span data-stu-id="0a744-179">toolist hello first name and last name of hello student</span></span>

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

<span data-ttu-id="0a744-180">Di seguito è riportato il risultato di hello dalla console di Hive hello.</span><span class="sxs-lookup"><span data-stu-id="0a744-180">Here is hello result from hello Hive console.</span></span>

![Query SerDe 1][image-hdi-hivejson-serde_query1]

<span data-ttu-id="0a744-182">somma di hello toocalculate di punteggi del documento JSON hello</span><span class="sxs-lookup"><span data-stu-id="0a744-182">toocalculate hello sum of scores of hello JSON document</span></span>

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

<span data-ttu-id="0a744-183">Hello prima query utilizza [vista laterale esplodere](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) tooexpand funzione definita dall'utente hello matrice dei punteggi in modo che essi possono essere sommati.</span><span class="sxs-lookup"><span data-stu-id="0a744-183">hello preceding query uses [lateral view explode](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF tooexpand hello array of scores so that they can be summed.</span></span>

<span data-ttu-id="0a744-184">Ecco l'output di hello dalla console di Hive hello.</span><span class="sxs-lookup"><span data-stu-id="0a744-184">Here is hello output from hello Hive console.</span></span>

![Query SerDe 2][image-hdi-hivejson-serde_query2]

<span data-ttu-id="0a744-186">toofind cui soggetti uno studente specificato ha raggiunto più di 80 punti:</span><span class="sxs-lookup"><span data-stu-id="0a744-186">toofind which subjects a given student has scored more than 80 points:</span></span>

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

<span data-ttu-id="0a744-187">la query precedente Hello restituisce una matrice di Hive a differenza di get\_json\_oggetto, che restituisce una stringa.</span><span class="sxs-lookup"><span data-stu-id="0a744-187">hello preceding query returns a Hive array unlike get\_json\_object, which returns a string.</span></span>

![Query SerDe 3][image-hdi-hivejson-serde_query3]

<span data-ttu-id="0a744-189">Se si desidera tooskil JSON in formato non corretto, quindi come spiegato in hello [pagina wiki](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) di questo SerDe è possibile ottenere che digitando hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="0a744-189">If you want tooskil malformed JSON, then as explained in hello [wiki page](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) of this SerDe you can achieve that by typing hello following code:</span></span>  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a><span data-ttu-id="0a744-190">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="0a744-190">Summary</span></span>
<span data-ttu-id="0a744-191">In conclusione, hello tipo di operatore JSON nell'Hive scelto dipende dallo scenario.</span><span class="sxs-lookup"><span data-stu-id="0a744-191">In conclusion, hello type of JSON operator in Hive that you choose depends on your scenario.</span></span> <span data-ttu-id="0a744-192">Se si dispone di un documento JSON semplice e avere solo un campo toolook: è possibile scegliere toouse hello Hive UDF get\_json\_oggetto.</span><span class="sxs-lookup"><span data-stu-id="0a744-192">If you have a simple JSON document and you only have one field toolook up on – you can choose toouse hello Hive UDF get\_json\_object.</span></span> <span data-ttu-id="0a744-193">Se sono presenti toolook chiave più di un, è possibile utilizzare json_tuple.</span><span class="sxs-lookup"><span data-stu-id="0a744-193">If you have more than one key toolook up on, then you can use json_tuple.</span></span> <span data-ttu-id="0a744-194">Se si dispone di un documento nidificato, è necessario utilizzare hello SerDe JSON.</span><span class="sxs-lookup"><span data-stu-id="0a744-194">If you have a nested document, then you should use hello JSON SerDe.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a744-195">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0a744-195">Next steps</span></span>

<span data-ttu-id="0a744-196">Per altri articoli correlati, vedere</span><span class="sxs-lookup"><span data-stu-id="0a744-196">For other related articles, see</span></span>

* [<span data-ttu-id="0a744-197">Utilizzare Hive e HiveQL con Hadoop in HDInsight tooanalyze un file di esempio Apache log4j</span><span class="sxs-lookup"><span data-stu-id="0a744-197">Use Hive and HiveQL with Hadoop in HDInsight tooanalyze a sample Apache log4j file</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="0a744-198">Analizzare i dati sui ritardi dei voli mediante Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a744-198">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="0a744-199">Analizzare i dati Twitter mediante Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a744-199">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="0a744-200">Eseguire un processo Hadoop usando Azure Cosmos DB e HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a744-200">Run a Hadoop job using Azure Cosmos DB and HDInsight</span></span>](../documentdb/documentdb-run-hadoop-with-hdinsight.md)

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
