---
title: aaaBuild la prima data factory (portale di Azure) | Documenti Microsoft
description: "In questa esercitazione è creare una pipeline di Data Factory di Azure di esempio utilizzando l'Editor delle Data Factory nel portale di Azure hello."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d5b14e9e-e358-45be-943c-5297435d402d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fc80776001b181a59c04d80d2e05c20b107a63f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a>Esercitazione: Creare la prima data factory di Azure con il portale di Azure
> [!div class="op_single_selector"]
> * [Panoramica e prerequisiti](data-factory-build-your-first-pipeline.md)
> * [Portale di Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Modello di Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)


In questo articolo viene illustrato come toouse [portale di Azure](https://portal.azure.com/) toocreate prima data factory di Azure. esercitazione di hello toodo tramite altri strumenti/SDK, selezionare una delle opzioni di hello dall'elenco a discesa hello. 

pipeline Hello in questa esercitazione è un'attività: **attività Hive di HDInsight**. Questa attività esegue uno script hive in un cluster HDInsight di Azure che trasformazioni i dati di output tooproduce di dati di input. pipeline di Hello è toorun pianificato dopo un mese tra hello specificato di ore di inizio e fine. 

> [!NOTE]
> pipeline di dati Hello in questa esercitazione Trasforma i dati di output tooproduce di dati di input. Per un'esercitazione su come dati di toocopy tramite Data Factory di Azure, vedere [esercitazione: copiare i dati da archiviazione Blob tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Una pipeline può includere più attività Inoltre, è possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività. Per altre informazioni, vedere [Pianificazione ed esecuzione in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

## <a name="prerequisites"></a>Prerequisiti
1. Leggere [esercitazione Panoramica](data-factory-build-your-first-pipeline.md) articolo e hello completo **prerequisito** passaggi.
2. In questo articolo non fornisce una panoramica concettuale di hello servizio Azure Data Factory. È consigliabile eseguire [tooAzure introduzione Data Factory](data-factory-introduction.md) articolo per una panoramica dettagliata del servizio hello.  

## <a name="create-data-factory"></a>Creare un'istanza di Data Factory
Una data factory può comprendere una o più pipeline. Una pipeline può comprendere una o più attività. Ad esempio, una data toocopy attività di copia da un archivio dati di origine tooa destinazione e un toorun attività Hive di HDInsight un tootransform script Hive i dati di output tooproduct dati di input. Iniziamo con la creazione di data factory di hello in questo passaggio.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Fare clic su **NEW** scegliere dal menu a sinistra, hello **dati + Analitica**, fare clic su **Data Factory**.

   ![Pannello Crea](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. In hello **nuova data factory** pannello immettere **GetStartedDF** per hello Name.

   ![Pannello Nuova data factory](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > nome Hello di hello Azure data factory deve essere **univoco globale**. Se viene visualizzato l'errore hello: **"GetStartedDF" nome della Data factory non è disponibile**. Modificare il nome di hello di hello data factory (ad esempio, yournameGetStartedDF) e provare a creare di nuovo. Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .
   >
   > nome Hello della hello data factory può essere registrato come un **DNS** nome nel futuro hello e pertanto diventano visibili pubblicamente.
   >
   >
4. Seleziona hello **sottoscrizione di Azure** in cui si desidera hello data factory toobe creato.
5. Selezionare un **gruppo di risorse** esistente o crearne uno. Per l'esercitazione hello, creare un gruppo di risorse denominato: **ADFGetStartedRG**.
6. Seleziona hello **percorso** per data factory di hello. Solo le aree supportate dal servizio Data Factory hello vengono visualizzate nell'elenco a discesa hello.
7. Selezionare **toodashboard Pin**. 
8. Fare clic su **crea** su hello **nuova data factory** blade.

   > [!IMPORTANT]
   > le istanze di Data Factory toocreate, è necessario essere un membro di hello [Data Factory collaboratore](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) ruolo a livello di gruppo di risorse di sottoscrizione/hello.
   >
   >
7. Nel dashboard di hello, si vedrà hello segue riquadro con stato: data factory di distribuzione.    

   ![Stato creazione della data factory](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. Congratulazioni. La creazione della prima data factory è così completata. Dopo aver hello data factory è stata creata correttamente, vedrai hello data factory pagina nella quale viene hello contenuto di data factory di hello.     

    ![Pannello Data factory](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

Prima di creare una pipeline in data factory di hello, è necessario toocreate alcune entità Data Factory prima. Creare innanzitutto i dati di servizi collegati toolink archivi/calcola tooyour dati archiviano, definiscono l'input e output dei dati di input/output toorepresent di set di dati in archivi dati collegato e quindi creare pipeline hello con un'attività che utilizza questi set di dati.

## <a name="create-linked-services"></a>Creare servizi collegati
In questo passaggio è collegare l'account di archiviazione di Azure e una factory del dati tooyour cluster Azure HDInsight su richiesta. contiene account di archiviazione di Azure Hello hello dati di input e outpui per la pipeline di hello in questo esempio. servizio collegato di HDInsight Hello è toorun usato uno script Hive specificato nell'attività hello della pipeline hello in questo esempio. Identificare le [archivio dati](data-factory-data-movement-activities.md)/[servizi di calcolo](data-factory-compute-linked-services.md) vengono utilizzati nello scenario e collegare tali toohello data factory di servizi mediante la creazione di servizi collegati.  

### <a name="create-azure-storage-linked-service"></a>Creare il servizio collegato Archiviazione di Azure
In questo passaggio si collega la data factory tooyour account di archiviazione di Azure. In questa esercitazione è utilizzare hello stesso account di archiviazione di Azure i dati di input/output toostore e hello HQL file di script.

1. Fare clic su **autore e distribuire** su hello **DATA FACTORY** pannello **GetStartedDF**. Dovrebbe essere hello Editor delle Data Factory.

   ![Riquadro Creare e distribuire](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. Fare clic su **Nuovo archivio dati** e scegliere **Archiviazione di Azure**.

   ![Nuovo archivio dati - Archiviazione di Azure - Menu](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. Dovrebbe essere hello script JSON per la creazione di una risorsa di archiviazione di Azure il servizio nell'editor di hello collegato.

   ![Servizio collegato Archiviazione di Azure](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. Sostituire **nome account** con nome hello dell'account di archiviazione di Azure e **chiave dell'account** con la chiave di accesso hello di hello account di archiviazione di Azure. toolearn come accedere a tooget lo spazio di archiviazione della chiave, vedere informazioni come tooview, copiare e rigenerare archiviazione accedere alle chiavi in hello [gestire account di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
5. Fare clic su **Distribuisci** sul comando hello barra toodeploy hello collegato servizio.

    ![Pulsante Distribuisci](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   Dopo aver hello servizio collegato viene distribuito correttamente, hello **bozza 1** dovrebbe scomparire una finestra e viene visualizzato **AzureStorageLinkedService** nella visualizzazione ad albero di hello a sinistra di hello.

    ![Servizio collegato Archiviazione nel menu](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a>Creare un servizio collegato Azure HDInsight
In questo passaggio si collega una factory del dati tooyour cluster HDInsight su richiesta. cluster HDInsight Hello viene automaticamente creato in fase di esecuzione ed eliminato al termine per l'elaborazione e inattività per l'intervallo di tempo specificato hello.

1. In hello **Editor delle Data Factory**, fare clic su **... Altro** e quindi su **Nuovo calcolo** e selezionare **Cluster HDInsight su richiesta**.

    ![Nuovo calcolo](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. Copiare e incollare hello seguente frammento di codice toohello **bozza 1** finestra. frammento di codice JSON Hello descrive le proprietà di hello hello toocreate utilizzati cluster HDInsight su richiesta.

    ```JSON
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:

   | Proprietà | Descrizione |
   |:--- |:--- |
   | ClusterSize |Specifica dimensioni hello del cluster HDInsight hello. |
   | TimeToLive | Specifica il tempo di inattività hello per il cluster HDInsight hello, prima che venga eliminato. |
   | linkedServiceName | Specifica l'account di archiviazione hello toostore utilizzati hello registri generati da HDInsight. |

    Si noti hello seguenti punti:

   * Hello Data Factory viene creata una **basati su Linux** cluster HDInsight per l'utente con hello JSON. Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .
   * È possibile usare il **proprio cluster HDInsight** anziché un cluster HDInsight su richiesta. Per i dettagli, vedere [Servizio collegato Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .
   * Crea cluster HDInsight Hello un **contenitore predefinito** nell'archiviazione blob hello specificato in JSON hello (**linkedServiceName**). HDInsight non eliminare questo contenitore quando viene eliminato il cluster hello. Questo comportamento dipende dalla progettazione. Con il servizio collegato HDInsight su richiesta, viene creato un cluster HDInsight ogni volta che viene elaborata una sezione, a meno che non esista un cluster attivo (**timeToLive**). cluster Hello viene eliminato automaticamente quando viene eseguita un'elaborazione hello.

       Man mano che vengono elaborate più sezioni, vengono visualizzati numerosi contenitori nell'archivio BLOB di Azure. Se non li necessario per la risoluzione dei problemi dei processi di hello, è opportuno toodelete li tooreduce hello il costo di archiviazione. i nomi di Hello di questi contenitori seguono un modello: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Utilizzare strumenti come [Esplora archivi Microsoft](http://storageexplorer.com/) toodelete contenitori di Azure nell'archiviazione blob.

     Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .
3. Fare clic su **Distribuisci** sul comando hello barra toodeploy hello collegato servizio.

    ![Distribuire il servizio collegato HDInsight su richiesta](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. Assicurarsi di visualizzare entrambi **AzureStorageLinkedService** e **HDInsightOnDemandLinkedService** nella visualizzazione ad albero di hello a sinistra di hello.

    ![Visualizzazione albero con servizi collegati](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a>Creare set di dati
In questo passaggio creare set di dati toorepresent hello input e output dei dati per l'elaborazione Hive. Questi set di dati di riferimento toohello **AzureStorageLinkedService** creata precedentemente in questa esercitazione. Hello tooan punti di servizio collegato account di archiviazione di Azure e i set di dati specificare contenitore, cartella, nome del file nell'archiviazione hello che contiene l'input e output di dati.   

### <a name="create-input-dataset"></a>Creare set di dati di input
1. In hello **Editor delle Data Factory**, fare clic su **... Ulteriori** nella barra dei comandi di hello, fare clic su **nuovo set di dati**e selezionare **archiviazione Blob di Azure**.

    ![Nuovo set di dati](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. Copiare e incollare hello successiva finestra di frammento toohello bozza-1. Nel frammento di codice JSON hello, si sta creando un set di dati denominato **AzureBlobInput** che rappresenta i dati di input per un'attività nella pipeline hello. Inoltre, si specifica che i dati di input hello si trovano nel contenitore di blob hello chiamato **adfgetstarted** e cartella hello denominata **inputdata**.

    ```JSON
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "input.log",
                "folderPath": "adfgetstarted/inputdata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            },
            "external": true,
            "policy": {}
        }
    }
    ```
    Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:

   | Proprietà | Descrizione |
   |:--- |:--- |
   | type |proprietà tipo Hello è troppo**AzureBlob** perché i dati risiedono in una risorsa di archiviazione blob di Azure. |
   | linkedServiceName |Fa riferimento toohello **AzureStorageLinkedService** creato in precedenza. |
   | folderPath | Specifica il blob hello **contenitore** hello e **cartella** che contiene il BLOB di input. | 
   | fileName |Questa proprietà è facoltativa. Se si omette questa proprietà, vengono selezionati tutti i file hello folderPath hello. In questa esercitazione, hello solo **input.log** viene elaborato. |
   | type |file di log Hello sono in formato testo, permette di usare **TextFormat**. |
   | columnDelimiter |nei file di log hello colonne sono delimitate da **carattere virgola (`,`)** |
   | frequenza/intervallo |frequenza impostata troppo**mese** e l'intervallo è **1**, il che significa che hello input sezioni sono disponibili ogni mese. |
   | external | Questa proprietà è impostata troppo**true** se i dati di input hello non viene generati da questa pipeline. In questa esercitazione, i file input.log hello non viene generato da questa pipeline, è necessario impostare tootrue proprietà hello. |

    Per altre informazioni su queste proprietà JSON, vedere l'articolo relativo al [connettore BLOB di Azure](data-factory-azure-blob-connector.md#dataset-properties).
3. Fare clic su **Distribuisci** sul comando hello barra toodeploy hello appena creato set di dati. Dovrebbe essere hello set di dati nella visualizzazione ad albero di hello a sinistra di hello.

### <a name="create-output-dataset"></a>Creare il set di dati di output
È quindi possibile creare hello output dataset toorepresent hello output dati archiviati in archiviazione Blob di Azure hello.

1. In hello **Editor delle Data Factory**, fare clic su **... Ulteriori** nella barra dei comandi di hello, fare clic su **nuovo set di dati**e selezionare **archiviazione Blob di Azure**.  
2. Copiare e incollare hello successiva finestra di frammento toohello bozza-1. Nel frammento di codice JSON hello, si sta creando un set di dati denominato **AzureBlobOutput**e specificare la struttura di dati hello derivante da script Hive hello hello. Inoltre, si specifica che i risultati di hello vengono archiviati nel contenitore blob hello chiamato **adfgetstarted** e cartella hello denominata **partitioneddata**. Hello **disponibilità** sezione specifica di tale set di dati di output di hello viene prodotto su base mensile.

    ```JSON
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
          "folderPath": "adfgetstarted/partitioneddata",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Month",
          "interval": 1
        }
      }
    }
    ```
    Vedere **creare set di dati input hello** sezione per le descrizioni di queste proprietà. Non si imposta proprietà esterna hello in un set di dati di output come set di dati hello viene generato dal servizio Data Factory hello.
3. Fare clic su **Distribuisci** sul comando hello barra toodeploy hello appena creato set di dati.
4. Verificare che Hello set di dati è stata creata correttamente.

    ![Visualizzazione albero con servizi collegati](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a>Creare una pipeline
In questo passaggio viene creata la prima pipeline con un'attività **HDInsightHive** . Sezione di input è disponibile ogni mese (frequenza: mese, intervallo: 1), sezione di output viene prodotta ogni mese e hello dell'utilità di pianificazione per l'attività hello viene anche impostata toomonthly. le impostazioni di Hello per set di dati output hello e utilità di pianificazione attività hello devono corrispondere. Set di dati di output è attualmente, quali unità hello pianificazione, pertanto è necessario creare un set di dati di output, anche se l'attività hello non genera alcun output. Se l'attività hello non accetta alcun input, è possibile ignorare i set di dati input hello creazione. proprietà Hello utilizzate nei hello JSON seguente sono illustrate alla fine di hello in questa sezione.

1. In hello **Editor delle Data Factory**, fare clic su **i puntini di sospensione (...) Altri comandi** e quindi fare clic su **nuova pipeline**.

    ![Pulsante Nuova pipeline](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. Copiare e incollare hello successiva finestra di frammento toohello bozza-1.

   > [!IMPORTANT]
   > Sostituire **storageaccountname** con nome hello dell'account di archiviazione in hello JSON.
   >
   >

    ```JSON
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                        }
                    },
                    "inputs": [
                        {
                            "name": "AzureBlobInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobOutput"
                        }
                    ],
                    "policy": {
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                    },
                    "name": "RunSampleHiveActivity",
                    "linkedServiceName": "HDInsightOnDemandLinkedService"
                }
            ],
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    Nel frammento di codice JSON hello, si sta creando una pipeline che è costituito da una singola attività che utilizza Hive tooprocess dati in un cluster HDInsight.

    file di script Hive Hello, **partitionweblogs.hql**, viene archiviato nell'account di archiviazione Azure hello (specificato da scriptLinkedService hello, chiamato **AzureStorageLinkedService**) e in  **script** cartella nel contenitore hello **adfgetstarted**.

    Hello **definisce** sezione è le impostazioni di runtime hello toospecify utilizzati script hive toohello passati come valori di configurazione di Hive (ad esempio ${hiveconf: inputtable}, {hiveconf:partitionedtable} $).

    Hello **avviare** e **fine** le proprietà della pipeline hello specifica periodo attivo di hello della pipeline hello.

    In formato JSON dell'attività hello, specificare tale script Hive hello viene eseguito sul calcolo hello specificato da hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.

   > [!NOTE]
   > Vedere la sezione "JSON di Pipeline" in [pipeline e attività in Azure Data Factory](data-factory-create-pipelines.md) per dettagli sulle proprietà JSON utilizzato nell'esempio hello.
   >
   >
3. Verificare l'esempio hello:

   1. **input.log** file esista in hello **inputdata** cartella di hello **adfgetstarted** contenitore nell'archiviazione blob di Azure hello
   2. **partitionweblogs.hql** file esista in hello **script** cartella di hello **adfgetstarted** contenitore nell'archiviazione blob di Azure hello. Prerequisito hello completato i passaggi in hello [esercitazione Panoramica](data-factory-build-your-first-pipeline.md) se questi file non viene visualizzato.
   3. Confermare che è stato sostituito **storageaccountname** con nome hello dell'account di archiviazione in hello JSON di pipeline.
4. Fare clic su **Distribuisci** sul comando hello barra pipeline hello toodeploy. Poiché hello **avviare** e **fine** volte in cui vengono impostate in hello precedente e **isPaused** è toofalse set, pipeline hello esecuzioni (attività nella pipeline hello) immediatamente dopo la distribuzione.
5. Verificare che sia visualizzato pipeline hello nella visualizzazione ad albero di hello.

    ![Visualizzazione albero con pipeline](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. La creazione della prima pipeline è così completata.

## <a name="monitor-pipeline"></a>Monitorare la pipeline
### <a name="monitor-pipeline-using-diagram-view"></a>Monitorare la pipeline con la vista diagramma
1. Fare clic su **X** tooclose Editor delle Data Factory pannelli e toonavigate il pannello Data Factory toohello e fare clic su **diagramma**.

    ![Riquadro Diagramma](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. In vista diagramma hello, si visualizza una panoramica di pipeline hello e set di dati utilizzati in questa esercitazione.

    ![Vista Diagramma](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. tooview tutte le attività nella pipeline di hello, pipeline pulsante destro del mouse in hello diagramma e fare clic su Apri Pipeline.

    ![Menu Apri pipeline](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. Confermare la visualizzazione attività HDInsightHive hello nella pipeline hello.

    ![Visualizzazione Apri pipeline](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    toonavigate nuovamente toohello visualizzazione precedente, fare clic su **Data factory** nel menu di navigazione hello nella parte superiore di hello.
5. In hello **vista diagramma**, fare doppio clic sul set di dati hello **AzureBlobInput**. Verificare che tale sezione hello sia **pronto** stato. Potrebbe richiedere un paio di minuti per hello sezione tooshow fino nello stato pronto. Se non si verifica dopo attendere qualche minuto, verificare se si dispone di hello file di input (input.log) inserito in un contenitore destra hello (adfgetstarted) e cartella (inputdata).

   ![Sezione di input nello stato Pronto](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. Fare clic su **X** tooclose **AzureBlobInput** blade.
7. In hello **vista diagramma**, fare doppio clic sul set di dati hello **AzureBlobOutput**. Vedrai tale sezione hello che è in corso di elaborazione.

   ![Set di dati](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. Quando viene eseguita l'elaborazione, vedrai sezione hello **pronto** stato.

   ![Set di dati](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > La creazione di un cluster HDInsight su richiesta di solito richiede tempo (circa 20 minuti). Pertanto, prevedere pipeline hello richiedere troppo **circa 30 minuti** tooprocess hello sezione.
   >
   >

9. Quando si trova in sezione hello **pronto** stato, controllare hello **partitioneddata** cartella hello **adfgetstarted** contenitore nell'archiviazione blob per hello i dati di output.  

   ![Dati di output](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. Fare clic su hello sezione toosee dettagli in un **sezione dati** blade.

   ![Dettagli sezione dati](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. Fare clic su un'attività eseguire in hello **elenco viene eseguita l'attività** toosee dettagli su un'attività (attività Hive nello scenario di esempio) di eseguire in un **Dettagli esecuzione attività** finestra.   

   ![Dettagli esecuzione attività](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   Dai file di log hello, è possibile visualizzare informazioni sullo stato e query Hive hello che è stato eseguito. Tali file di log sono utili per risolvere eventuali problemi.
   Vedere l'articolo [Monitorare e gestire le pipeline di Azure Data Factory](data-factory-monitor-manage-pipelines.md) per altri dettagli.

> [!IMPORTANT]
> file di input Hello eliminato quando la sezione hello viene elaborata correttamente. Pertanto, se si desidera toorerun hello sezione o hello esercitazione nuovamente, hello del file di input (input.log) toohello inputdata cartella del contenitore adfgetstarted hello di caricamento.
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a>Monitorare la pipeline con l'app Monitoraggio e gestione
È possibile anche utilizzare Monitoraggio e Gestione applicazione toomonitor le pipeline. Per informazioni dettagliate sull'uso di questa applicazione, vedere [Monitorare e gestire le pipeline di Azure Data Factory con la nuova app di monitoraggio e gestione](data-factory-monitor-manage-app.md).

1. Fare clic su **monitoraggio e gestione** riquadro hello home page per la data factory.

    ![Riquadro Monitoraggio e gestione](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. Verrà visualizzata l'applicazione **Monitoraggio e gestione**. Hello modifica **ora di inizio** e **ora di fine** toomatch avvio e fine della pipeline e fare clic su **applica**.

    ![App Monitoraggio e gestione](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. Selezionare una finestra attività in hello **attività Windows** elenco dettagli toosee.

    ![Dettagli finestra attività](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

## <a name="summary"></a>Riepilogo
In questa esercitazione, creato un Azure factory tooprocess dati tramite l'esecuzione di script Hive in un cluster di HDInsight hadoop. È stato utilizzato hello Editor delle Data Factory in hello toodo portale Azure hello alla procedura seguente:  

1. Creare un'istanza di Azure **Data Factory**.
2. Creare due **servizi collegati**:
   1. **Archiviazione di Azure** collegati toolink servizio di archiviazione blob di Azure che contiene una data factory toohello di file di input/output.
   2. **Azure HDInsight** toolink servizio collegato su richiesta di una factory del dati toohello cluster HDInsight Hadoop su richiesta. Data Factory di Azure crea un HDInsight Hadoop dati di input tooprocess just-in-time di cluster e generare dati di output.
3. Creare due **set di dati**, che descrivono i dati di input e outpui per l'attività Hive di HDInsight nella pipeline hello.
4. Creare una **pipeline** con un'attività **Hive di HDInsight**.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo è stata creata una pipeline con un'attività di trasformazione (attività HDInsight) che esegue uno script Hive in un cluster HDInsight su richiesta. toosee toouse un dati toocopy attività di copia da un tooAzure Blob di Azure SQL, vedere [esercitazione: copiare i dati da un tooAzure blob di Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="see-also"></a>Vedere anche
| Argomento | Descrizione |
|:--- |:--- |
| [Pipeline](data-factory-create-pipelines.md) |In questo articolo consente di comprendere le pipeline e attività nella Data Factory di Azure e come toouse li tooconstruct end-to-end basato sui dati dei flussi di lavoro degli scenario o dell'azienda. |
| [Set di dati](data-factory-create-datasets.md) |Questo articolo fornisce informazioni sui set di dati in Azure Data Factory. |
| [Pianificazione ed esecuzione](data-factory-scheduling-and-execution.md) |Questo articolo illustra gli aspetti hello di pianificazione e l'esecuzione del modello di applicazione di Azure Data Factory. |
| [Monitorare e gestire le pipeline con l'app di monitoraggio](data-factory-monitor-manage-app.md) |In questo articolo viene descritto come toomonitor, gestire ed eseguire il debug pipeline utilizzando hello monitoraggio e gestione delle App. |
