---
title: aaaInvoke Spark programmi da Data Factory di Azure | Documenti Microsoft
description: "Informazioni su come i programmi di Spark tooinvoke da una factory di dati di Azure usando hello attività MapReduce."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: fd98931c-cab5-4d66-97cb-4c947861255c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: f88943ece7ee3d21dedbd857609f1b2713b62741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a>Chiamare i programmi Spark dalle pipeline Azure Data Factory

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Attività Hive](data-factory-hive-activity.md)
> * [Attività di Pig](data-factory-pig-activity.md)
> * [Attività MapReduce](data-factory-map-reduce.md)
> * [Attività di Hadoop Streaming](data-factory-hadoop-streaming-activity.md)
> * [Attività Spark](data-factory-spark.md)
> * [Attività di esecuzione batch di Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Attività della risorsa di aggiornamento di Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Attività stored procedure](data-factory-stored-proc-activity.md)
> * [Attività U-SQL di Data Lake Analytics](data-factory-usql-activity.md)
> * [Attività personalizzata di .NET](data-factory-use-custom-activities.md)

## <a name="introduction"></a>Introduzione
Attività Spark è uno dei hello [le attività di trasformazione dati](data-factory-data-transformation-activities.md) supportati da Data Factory di Azure. Questa attività esegue hello specificato programma Spark sul cluster Apache Spark in HDInsight di Azure.    

> [!IMPORTANT]
> - L'attività Spark non supporta i cluster Spark HDInsight che usano Azure Data Lake Store come risorsa di archiviazione primaria.
> - L'attività Spark supporta solo cluster Spark HDInsight esistenti (personalizzati). Non supporta un servizio collegato HDInsight su richiesta.

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a>Procedura dettagliata: creare una pipeline con attività Spark
Ecco i passaggi tipici di hello toocreate una pipeline di Data Factory con un'attività di Spark.  

1. Creare una data factory.
2. Creare un toolink di servizio collegato di archiviazione Azure l'archiviazione di Azure associata con la data factory di toohello cluster HDInsight Spark.     
2. Creare un toolink di servizio collegato di Azure HDInsight cluster Apache Spark in data factory di Azure HDInsight toohello.
3. Creare un set di dati che fa riferimento il servizio di archiviazione di Azure collegati toohello. Attualmente, è necessario specificare un set di dati di output per un'attività anche se non viene prodotto alcun output.  
4. Creare una pipeline con attività Spark che fa riferimento a servizio collegato di HDInsight toohello creato nel #2. attività Hello è configurato con dataset hello creato nel passaggio precedente di hello come un set di dati di output. set di dati output hello è quali unità hello pianificazione (oraria, giornaliera, e così via.). Pertanto, è necessario specificare il set di dati di hello output anche se l'attività hello non produce un output molto.

### <a name="prerequisites"></a>Prerequisiti
1. Crea un **generico Account di archiviazione di Azure** seguendo le istruzioni riportate in questa procedura dettagliata hello: [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account).  
2. Crea un **cluster Apache Spark in Azure HDInsight** seguendo le istruzioni riportate nell'esercitazione hello: [cluster creare Apache Spark in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). Associare l'account di archiviazione di Azure hello creato nel passaggio &#1; con questo cluster.  
3. Scaricare ed esaminare i file di script python hello **test.py** disponibile all'indirizzo: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).  
3.  Caricare **test.py** toohello **pyFiles** cartella hello **adfspark** contenitore nell'archiviazione Blob di Azure. Creare un contenitore di hello e cartella hello se non esistono.

### <a name="create-data-factory"></a>Creare un'istanza di Data Factory
Iniziamo con la creazione di data factory di hello in questo passaggio.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Fare clic su **NEW** scegliere dal menu a sinistra, hello **dati + Analitica**, fare clic su **Data Factory**.
3. In hello **nuova data factory** pannello immettere **SparkDF** per hello Name.

   > [!IMPORTANT]
   > nome Hello di hello Azure data factory deve essere **univoco globale**. Se viene visualizzato l'errore hello: **"SparkDF" nome della Data factory non è disponibile**. Modificare il nome di hello della data factory di hello (ad esempio, yournameSparkDFdate e provare a creare di nuovo. Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .   
4. Seleziona hello **sottoscrizione di Azure** in cui si desidera hello data factory toobe creato.
5. Selezionare un **gruppo di risorse** di Azure esistente o crearne uno nuovo.
6. Selezionare **toodashboard Pin** opzione.  
6. Fare clic su **crea** su hello **nuova data factory** blade.

   > [!IMPORTANT]
   > le istanze di Data Factory toocreate, è necessario essere un membro di hello [Data Factory collaboratore](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) ruolo a livello di gruppo di risorse di sottoscrizione/hello.
7. Vedrai data factory di hello viene creato nel hello **dashboard** di hello portale di Azure come indicato di seguito:   
8. Dopo aver hello data factory è stata creata correttamente, vedrai hello data factory pagina nella quale viene hello contenuto di data factory di hello. Se non è possibile visualizzare pagina factory di hello dati, fare clic su riquadro hello per la data factory di dashboard hello.

    ![Pannello Data factory](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a>Creare servizi collegati
In questo passaggio, creare due servizi collegati, una toolink la data factory di tooyour cluster Spark e hello altri toolink la data factory tooyour di archiviazione di Azure.  

#### <a name="create-azure-storage-linked-service"></a>Creare il servizio collegato Archiviazione di Azure
In questo passaggio si collega la data factory tooyour account di archiviazione di Azure. Un set di dati create in un passaggio più avanti in questa procedura dettagliata fa riferimento a servizio toothis collegato. servizio collegato di HDInsight definito nel passaggio successivo hello Hello servizio toothis collegato fa riferimento troppo.  

1. Fare clic su **autore e distribuire** su hello **Data Factory** pannello per il data factory. Dovrebbe essere hello Editor delle Data Factory.
2. Fare clic su **Nuovo archivio dati** e scegliere **Archiviazione di Azure**.

   ![Nuovo archivio dati - Archiviazione di Azure - Menu](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. Dovrebbe essere hello **script JSON** per la creazione di una risorsa di archiviazione di Azure il servizio nell'editor di hello collegato.

   ![Servizio collegato Archiviazione di Azure](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. Sostituire **nome account** e **chiave dell'account** con chiave hello di accesso e sul nome dell'account di archiviazione di Azure. toolearn come accedere a tooget lo spazio di archiviazione della chiave, vedere informazioni come tooview, copiare e rigenerare archiviazione accedere alle chiavi in hello [gestire account di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
5. toodeploy hello servizio collegato, fare clic su **Distribuisci** hello barra dei comandi. Dopo aver hello servizio collegato viene distribuito correttamente, hello **bozza 1** dovrebbe scomparire una finestra e viene visualizzato **AzureStorageLinkedService** nella visualizzazione ad albero di hello a sinistra di hello.

#### <a name="create-hdinsight-linked-service"></a>Creare un servizio collegato HDInsight
In questo passaggio è creare toolink di servizio collegato di Azure HDInsight la data factory di toohello cluster HDInsight Spark. cluster HDInsight Hello è programma Spark di hello toorun utilizzati specificato nell'attività di Spark hello della pipeline hello in questo esempio.  

1. Fare clic su **... Ulteriori** sulla barra degli strumenti hello, fare clic su **nuovo calcolo**, quindi fare clic su **cluster HDInsight**.

    ![Creare un servizio collegato HDInsight](media/data-factory-spark/new-hdinsight-linked-service.png)
2. Copiare e incollare hello seguente frammento di codice toohello **bozza 1** finestra. Nell'editor di JSON hello, hello alla procedura seguente:
    1. Specificare hello **URI** per HDInsight Spark hello del cluster. Ad esempio: `https://<sparkclustername>.azurehdinsight.net/`.
    2. Specificare il nome di hello di hello **utente** chi ha cluster Spark toohello di accesso.
    3. Specificare hello **password** per utente.
    4. Specificare hello **servizio collegato di archiviazione di Azure** associato hello cluster HDInsight Spark. Nell'esempio è: **AzureStorageLinkedService**.

    ```json
    {
        "name": "HDInsightLinkedService",
        "properties": {
            "type": "HDInsight",
            "typeProperties": {
                "clusterUri": "https://<sparkclustername>.azurehdinsight.net/",
                "userName": "admin",
                "password": "**********",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    > [!IMPORTANT]
    > - L'attività Spark non supporta i cluster Spark HDInsight che usano Azure Data Lake Store come risorsa di archiviazione primaria.
    > - L'attività Spark supporta solo cluster Spark HDInsight esistenti (personalizzati). Non supporta un servizio collegato HDInsight su richiesta.

    Vedere [servizio collegato di HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) per informazioni dettagliate su hello servizio collegato di HDInsight.
3.  toodeploy hello servizio collegato, fare clic su **Distribuisci** hello barra dei comandi.  

### <a name="create-output-dataset"></a>Creare il set di dati di output
set di dati output hello è quali unità hello pianificazione (oraria, giornaliera, e così via.). Pertanto, è necessario specificare un set di dati di output per l'attività di spark hello nella pipeline di hello, anche se l'attività hello effettivamente generato alcun output. Un set di dati di input per l'attività hello è facoltativo.

1. In hello **Editor delle Data Factory**, fare clic su **... Ulteriori** nella barra dei comandi di hello, fare clic su **nuovo set di dati**e selezionare **archiviazione Blob di Azure**.  
2. Copiare e incollare hello successiva finestra di frammento toohello bozza-1. frammento di codice JSON Hello definisce un set di dati denominato **OutputDataset**. Inoltre, si specifica che i risultati di hello vengono archiviati nel contenitore blob hello chiamato **adfspark** e cartella hello denominata **pyFiles/output**. Come accennato in precedenza, questo set di dati è un set di dati fittizio. programma di Spark Hello in questo esempio non produce alcun output. Hello **disponibilità** sezione specifica di tale set di dati di output di hello viene prodotta ogni giorno.  

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "sparkoutput.txt",
                "folderPath": "adfspark/pyFiles/output",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": "\t"
                }
            },
            "availability": {
                "frequency": "Day",
                "interval": 1
            }
        }
    }
    ```
3. toodeploy hello set di dati, fare clic su **Distribuisci** hello barra dei comandi.


### <a name="create-pipeline"></a>Creare una pipeline
In questo passaggio viene creata una pipeline con un'**attività HDInsightSpark**. Set di dati di output è attualmente, quali unità hello pianificazione, pertanto è necessario creare un set di dati di output, anche se l'attività hello non genera alcun output. Se l'attività hello non accetta alcun input, è possibile ignorare i set di dati input hello creazione. Pertanto in questo esempio non viene specificato alcun set di dati di input.

1. In hello **Editor delle Data Factory**, fare clic su **... Ulteriori** hello barra dei comandi e quindi fare clic su **nuova pipeline**.
2. Sostituire script hello nella finestra di hello bozza-1 con hello lo script seguente:

    ```json
    {
        "name": "SparkPipeline",
        "properties": {
            "activities": [
                {
                    "type": "HDInsightSpark",
                    "typeProperties": {
                        "rootPath": "adfspark\\pyFiles",
                        "entryFilePath": "test.py",
                        "getDebugInfo": "Always"
                    },
                    "outputs": [
                        {
                            "name": "OutputDataset"
                        }
                    ],
                    "name": "MySparkActivity",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-02-05T00:00:00Z",
            "end": "2017-02-06T00:00:00Z"
        }
    }
    ```
    Si noti hello seguenti punti:
    - Hello **tipo** impostata troppo**HDInsightSpark**.
    - Hello **rootPath** è troppo**adfspark\\pyFiles** dove adfspark è il contenitore di Blob di Azure hello e pyFiles è cartella correttamente in tale contenitore. In questo esempio hello archiviazione Blob di Azure è hello uno associato al cluster Spark hello. È possibile caricare tooa file hello archiviazione di Azure diversi. In tal caso, creare un toolink di servizio collegato di archiviazione di Azure che data factory toohello account di archiviazione. Quindi, specificare il nome di hello del servizio hello collegato come valore per hello **sparkJobLinkedService** proprietà. Vedere [le proprietà dell'attività di Spark](#spark-activity-properties) per informazioni dettagliate su questa proprietà e altre proprietà supportate dall'attività Spark hello.  
    - Hello **entryFilePath** è impostato toohello **test.py**, ossia file python hello.
    - Hello **getDebugInfo** impostata troppo**sempre**, ovvero i file di log hello vengono sempre generati (esito positivo o negativo).

        > [!IMPORTANT]
        > È consigliabile non impostare questa proprietà troppo`Always` in un ambiente di produzione a meno che non si sta risolvendo un problema.
    - Hello **restituisce** sezione ha un set di dati di output. Anche se il programma di spark hello non genera alcun output, è necessario specificare un set di dati di output. pianificazione di hello unità per set di dati di output Hello per pipeline hello (oraria, giornaliera, e così via.).  

        Per informazioni dettagliate sulle proprietà hello è supportata dall'attività Spark, vedere [nascita le proprietà dell'attività](#spark-activity-properties) sezione.
3. pipeline di hello toodeploy, fare clic su **Distribuisci** hello barra dei comandi.

### <a name="monitor-pipeline"></a>Monitorare la pipeline
1. Fare clic su **X** tooclose Editor delle Data Factory pannelli e toonavigate nuovamente home page di toohello Data Factory. Fare clic su **monitoraggio e gestione** hello toolaunch monitoraggio dell'applicazione in un'altra scheda.

    ![Riquadro Monitoraggio e gestione](media/data-factory-spark/monitor-and-manage-tile.png)
2. Hello modifica **ora di inizio** filtro nella parte superiore di hello troppo**1/2/2017**, fare clic su **applica**.
3. Verrà visualizzato solo una finestra di attività perché non esiste un solo giorno tra hello (2017-02-01) di inizio e di fine (2017-02-02) della pipeline hello. Verificare che la sezione dati hello viene **pronto** stato.

    ![Pipeline hello monitoraggio](media/data-factory-spark/monitor-and-manage-app.png)    
4. Seleziona hello **finestra attività** toosee dettagli sull'esecuzione dell'attività hello. Se si verifica un errore, si noterà dettagli nel riquadro di destra hello.

### <a name="verify-hello-results"></a>Verificare i risultati di hello

1. Avviare **Jupyter Notebook** per il cluster Spark HDInsight accedendo a: https://CLUSTERNAME.azurehdinsight.net/jupyter. È possibile anche avviare il dashboard del cluster per il cluster Spark HDInsight e quindi avviare **Jupyter Notebook**.
2. Fare clic su **New** -> **PySpark** toostart un nuovo blocco appunti.

    ![Nuovo notebook Jupyter](media/data-factory-spark/jupyter-new-book.png)
3. Esecuzione hello il seguente comando copia e Incolla di testo hello e premendo **MAIUSC + INVIO** alla fine di hello della seconda istruzione hello.  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. Confermare la visualizzazione dei dati hello hello impianto tabella:  

    ![Risultati della query Jupyter](media/data-factory-spark/jupyter-notebook-results.png)

Per informazioni dettagliate, vedere la sezione [Eseguire una query SQL Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql). 

### <a name="troubleshooting"></a>Risoluzione dei problemi
Poiché è impostato **getDebugInfo** troppo**sempre**, vedrai un **log** sottocartella hello **pyFiles** cartella nel contenitore del Blob di Azure. file di log Hello nella cartella dei log hello fornisce dettagli aggiuntivi. Tale file è particolarmente utile quando si verifica un errore. In un ambiente di produzione, è opportuno tooset è troppo**errore**.

Per un'ulteriore risoluzione dei problemi, hello alla procedura seguente:


1. Passare troppo`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.

    ![Applicazione interfaccia utente di Yarn](media/data-factory-spark/yarnui-application.png)  
2. Fare clic su **registri** per uno di hello eseguire tentativi.

    ![Pagina Applicazione](media/data-factory-spark/yarn-applications.png)
3. Informazioni aggiuntive sull'errore nella pagina log hello dovrebbe.

    ![Errore log](media/data-factory-spark/yarnui-application-error.png)

Hello le sezioni seguenti fornisce informazioni sul Data Factory entità toouse Apache Spark cluster e la data factory di attività Spark.

## <a name="spark-activity-properties"></a>Proprietà dell'attività Spark
Ecco definizione JSON di esempio hello di una pipeline con attività Spark:    

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "arguments": [ "arg1", "arg2" ],
                    "sparkConfig": {
                        "spark.python.worker.memory": "512m"
                    }
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "description": "This activity invokes hello Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

Hello tabella seguente vengono descritte le proprietà JSON hello utilizzate nella definizione JSON hello:

| Proprietà | Descrizione | Obbligatorio |
| -------- | ----------- | -------- |
| name | Nome dell'attività hello nella pipeline hello. | Sì |
| description | Testo che descrive le attività di hello esegue. | No |
| type | Questa proprietà deve essere impostata tooHDInsightSpark. | Sì |
| linkedServiceName | Nome di hello HDInsight collegato del servizio in cui hello Spark programma in esecuzione. | Sì |
| rootPath | contenitore di Blob di Azure Hello e della cartella che contiene file Spark hello. nome del file Hello è tra maiuscole e minuscole. | Sì |
| entryFilePath | Cartella radice di percorso relativo toohello di hello Spark codice o del pacchetto. | Sì |
| className | Classe principale Java/Spark dell'applicazione | No |
| arguments | Un elenco di programmi di Spark toohello gli argomenti della riga di comando. | No |
| proxyUser | programma di Hello utente account tooimpersonate tooexecute hello Spark | No |
| sparkConfig | Specificare i valori per le proprietà di configurazione di Spark elencati nell'argomento hello: [configurazione Spark - proprietà applicazione](https://spark.apache.org/docs/latest/configuration.html#available-properties). | No |
| getDebugInfo | Specifica quando i file di log Spark hello toohello copiato archiviazione di Azure usati dal cluster HDInsight (o) specificato da sparkJobLinkedService. Valori consentiti: None, Always o Failure. Valore predefinito: None. | No |
| sparkJobLinkedService | servizio collegato di archiviazione di Azure che contiene i registri, le dipendenze e hello Spark processo file Hello.  Se non si specifica un valore per questa proprietà, viene utilizzata l'archiviazione di hello associato al cluster HDInsight. | No |

## <a name="folder-structure"></a>Struttura di cartelle
Hello attività Spark non supporta uno script in linea come Pig e Hive attività eseguire. I processi Spark sono anche più estendibili dei processi Pig/Hive. Per i processi di Spark, è possibile fornire più dipendenze, ad esempio file jar di pacchetti (inseriti nel linguaggio hello CLASSPATH), i file di python (posizionati hello PYTHONPATH) e qualsiasi altro file.

Creare hello seguente struttura di cartelle in hello archiviazione Blob di Azure a cui fa riferimento hello servizio collegato di HDInsight. Successivamente, caricare le cartelle di file dipendenti toohello sub appropriato nella cartella radice hello rappresentato da **entryFilePath**. Ad esempio, caricare python file toohello pyFiles sottocartella e file jar toohello JAR sottocartella della cartella radice hello. In fase di esecuzione, il servizio Data Factory prevede hello seguente struttura di cartelle in hello archiviazione Blob di Azure:     

| Path | Descrizione | Obbligatorio | Tipo |
| ---- | ----------- | -------- | ---- |
| . | percorso radice Hello del processo di Spark hello nel servizio di archiviazione collegato hello    | Sì | Cartella |
| &lt;definito dall'utente &gt; | percorso di Hello che fa riferimento il file voce toohello del processo di Spark hello | Sì | File |
| ./jars | Tutti i file in questa cartella vengono caricati e inseriti in classpath java hello del cluster hello | No | Cartella |
| ./pyFiles | Tutti i file in questa cartella vengono caricati e inseriti in hello PYTHONPATH del cluster hello | No | Cartella |
| ./files | Tutti i file in questa cartella vengono caricati e inseriti nella directory di lavoro executor | No | Cartella |
| ./archives | Tutti i file in questa cartella sono decompressi | No | Cartella |
| ./logs | cartella Hello in cui sono archiviati i log da cluster Spark hello.| No | Cartella |

Di seguito è riportato un esempio per una risorsa di archiviazione che contiene due file di processo Spark in hello archiviazione Blob di Azure a cui fa riferimento hello servizio collegato di HDInsight.

```
SparkJob1
    main.jar
    files
        input1.txt
        input2.txt
    jars
        package1.jar
        package2.jar
    logs

SparkJob2
    main.py
    pyFiles
        scrip1.py
        script2.py
    logs
```
