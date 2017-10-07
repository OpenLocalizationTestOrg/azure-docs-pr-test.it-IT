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
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a>Elaborare e analizzare documenti JSON usando Hive in HDInsight

Informazioni su come tooprocess e analizzare i file JSON utilizzando Hive in HDInsight. Hello seguente documento JSON utilizzato nell'esercitazione hello:

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

file Hello è reperibile in wasb://processjson@hditutorialdata.blob.core.windows.net/. Per altre informazioni sull'uso dell'archivio BLOB di Azure con HDInsight, vedere [Usare un archivio BLOB di Azure compatibile con HDFS con Hadoop in HDInsight](hdinsight-hadoop-use-blob-storage.md). È possibile copiare contenitore predefinito di hello file toohello del cluster.

In questa esercitazione, utilizzare una console di Hive hello.  Per istruzioni di apertura hello Hive console, vedere [utilizzare Hive con Hadoop in HDInsight con Desktop remoto](hdinsight-hadoop-use-hive-remote-desktop.md).

## <a name="flatten-json-documents"></a>Rendere flat i documenti JSON
metodi di Hello elencati nella sezione successiva hello richiedono hello del documento JSON in una singola riga. Pertanto, è necessario unire stringa tooa documento JSON di hello. Se il documento JSON è già bidimensionale, è possibile ignorare questo passaggio e passare la sezione successiva toohello retta sui dati di analisi di JSON.

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

Hello file JSON non elaborato si trova in  **wasb://processjson@hditutorialdata.blob.core.windows.net/** . Hello *StudentsRaw* tabella Hive punta toohello documento JSON non convertito non elaborato.

Hello *StudentsOneLine* tabella Hive archivia i dati di hello in file system predefinito HDInsight in hello hello */jsonstudenti/* percorso.

istruzione INSERT Hello tabella viene popolata hello StudentOneLine con i dati JSON hello bidimensionale.

istruzione SELECT Hello dovrà restituire una sola riga.

Ecco l'output di hello dell'istruzione SELECT hello:

![Conversione del documento JSON hello.][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a>Analizzare i documenti JSON in Hive
Hive fornisce tre diversi meccanismi toorun query su documenti JSON:

* Utilizzare GET hello\_JSON\_oggetto funzione definita dall'utente (funzione definita dall'utente)
* Utilizzare hello JSON_TUPLE funzione definita dall'utente
* Usare l'interfaccia SerDe personalizzata.
* Scrivere una funzione definita dall'utente personalizzata usando Python o altri linguaggi. Vedere [questo articolo][hdinsight-python] sull'esecuzione del codice Python personalizzato con Hive.

### <a name="use-hello-getjsonobject-udf"></a>Hello utilizzare GET\_JSON_OBJECT funzione definita dall'utente
Hive offre una funzione definita dall'utente predefinita denominata [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object) in grado di eseguire query JSON in fase di esecuzione. Questo metodo accetta due argomenti: nome della tabella hello e nome del metodo, che ha hello bidimensionale JSON hello e documenti JSON campo che deve toobe analizzato. Esaminiamo un esempio toosee funzionamento di questa funzione definita dall'utente.

Ottenere hello nome e cognome di ogni studente

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

Ecco output di hello quando si esegue questa query nella finestra della console.

![Funzione definita dall'utente get_json_object][image-hdi-hivejson-getjsonobject]

Esistono alcune limitazioni di get-json_object hello funzione definita dall'utente.

* Poiché ogni campo nella query hello richiede vuoti query hello, influisce sulle prestazioni di hello.
* OTTENERE\_JSON_OBJECT() restituisce la rappresentazione di stringa hello di una matrice. tooconvert questa matrice di matrice tooa Hive, aver toouse espressioni regolari tooreplace hello parentesi quadre "[' e ']' e quindi anche chiamata divisione matrice hello tooget.

Ecco perché hello Hive wiki consiglia l'uso di json_tuple.  

### <a name="use-hello-jsontuple-udf"></a>Utilizzare hello JSON_TUPLE funzione definita dall'utente
L'altra funzione definita dall'utente disponibile in Hive è denominata [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple) e offre prestazioni migliori rispetto a [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object). Questo metodo accetta un insieme di chiavi e una stringa JSON e restituisce una tupla di valori usando una funzione. Hello query seguente restituisce id dello studente hello e livello di hello da un documento JSON hello:

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

output di Hello dello script nella console di Hive hello:

![Funzione definita dall'utente json_tuple][image-hdi-hivejson-jsontuple]

JSON\_TUPLA utilizza hello [laterali vista](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) sintassi nell'Hive, che consente di json\_tupla toocreate una tabella virtuale applicando hello UDT funzione tooeach riga della tabella originale hello.  Documenti JSON complessi diventare troppo difficile da gestire a causa di hello ripetuto l'utilizzo di visualizzazione laterale. JSON_TUPLE non è in grado di gestire documenti JSON annidati.

### <a name="use-custom-serde"></a>Usare l'interfaccia SerDe personalizzata
SerDe sia hello migliore per l'analisi dei documenti JSON annidati, ma consente toodefine hello JSON schema e utilizzare hello schema tooparse hello documenti. In questa esercitazione, utilizzare uno dei hello SerDe più comuni che è stato sviluppato da [Roberto Congiu](https://github.com/rcongiu).

**toouse hello SerDe personalizzato:**

1. Installare [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR). Scegliere hello JDK versione X64 di Windows hello se si sta utilizzando la distribuzione di Windows hello di HDInsight toobe
   
   > [!WARNING]
   > JDK 1.8 non funziona con questa SerDe.
   > 
   > 
   
    Al termine dell'installazione di hello, aggiungere una nuova variabile di ambiente utente:
   
   1. Aprire **Visualizza impostazioni di sistema avanzate** dalla schermata di Windows hello.
   2. Fare clic su **Variabili di ambiente**.  
   3. Aggiungere un nuovo **JAVA_HOME** variabile di ambiente punta troppo**Files\Java\jdk1.7.0_55 c:\Programmi\Microsoft** o punto in cui è installato il pacchetto JDK.
      
      ![Configurazione dei valori di configurazione corretti per JDK][image-hdi-hivejson-jdk]
2. Installare [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)
   
    Aggiungi percorso tooyour della cartella bin hello passando tooControl pannello--> Modifica le variabili di sistema di hello per le variabili di ambiente account. Hello cattura di schermata seguente illustra come toodo questo.
   
    ![Configurazione di Maven][image-hdi-hivejson-maven]
3. Progetto hello clone da [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) sito github. È possibile farlo facendo clic sul pulsante "Download Zip" hello come illustrato nella seguente schermata hello.
   
    ![La clonazione progetto hello][image-hdi-hivejson-serde]

4: go toohello cartella in cui è stato scaricato il pacchetto e quindi il tipo "mvn pacchetto". Si deve creare hello file jar necessarie che è quindi possibile copiare su toohello cluster.

5: cartella di destinazione toohello andare nella cartella radice hello in cui è stato scaricato il pacchetto di hello. Caricare file json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar hello toohead-nodo del cluster. In genere inserirlo nella cartella di hello hive binari: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin o simile.

6: nel prompt dei comandi hive hello, digitare "Aggiungi jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar". Poiché in questo caso, jar hello nella cartella C:\apps\dist\hive-0.13.x\bin hello, è possibile aggiungere direttamente jar hello con nome hello, come illustrato:

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![Aggiunta di file JAR tooyour progetto][image-hdi-hivejson-addjar]

A questo punto, si è pronti toouse hello SerDe toorun query documento JSON hello.

Hello istruzione crea una tabella con uno schema definito:

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

toolist hello nome e cognome di hello studente

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

Di seguito è riportato il risultato di hello dalla console di Hive hello.

![Query SerDe 1][image-hdi-hivejson-serde_query1]

somma di hello toocalculate di punteggi del documento JSON hello

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

Hello prima query utilizza [vista laterale esplodere](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) tooexpand funzione definita dall'utente hello matrice dei punteggi in modo che essi possono essere sommati.

Ecco l'output di hello dalla console di Hive hello.

![Query SerDe 2][image-hdi-hivejson-serde_query2]

toofind cui soggetti uno studente specificato ha raggiunto più di 80 punti:

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

la query precedente Hello restituisce una matrice di Hive a differenza di get\_json\_oggetto, che restituisce una stringa.

![Query SerDe 3][image-hdi-hivejson-serde_query3]

Se si desidera tooskil JSON in formato non corretto, quindi come spiegato in hello [pagina wiki](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) di questo SerDe è possibile ottenere che digitando hello seguente codice:  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a>Riepilogo
In conclusione, hello tipo di operatore JSON nell'Hive scelto dipende dallo scenario. Se si dispone di un documento JSON semplice e avere solo un campo toolook: è possibile scegliere toouse hello Hive UDF get\_json\_oggetto. Se sono presenti toolook chiave più di un, è possibile utilizzare json_tuple. Se si dispone di un documento nidificato, è necessario utilizzare hello SerDe JSON.

## <a name="next-steps"></a>Passaggi successivi

Per altri articoli correlati, vedere

* [Utilizzare Hive e HiveQL con Hadoop in HDInsight tooanalyze un file di esempio Apache log4j](hdinsight-use-hive.md)
* [Analizzare i dati sui ritardi dei voli mediante Hive in HDInsight](hdinsight-analyze-flight-delay-data.md)
* [Analizzare i dati Twitter mediante Hive in HDInsight](hdinsight-analyze-twitter-data.md)
* [Eseguire un processo Hadoop usando Azure Cosmos DB e HDInsight](../documentdb/documentdb-run-hadoop-with-hdinsight.md)

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
