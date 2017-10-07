---
title: aaaBuild la prima data factory (Visual Studio) | Documenti Microsoft
description: In questa esercitazione viene creata una pipeline di esempio di Azure Data Factory usando Visual Studio.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7398c0c9-7a03-4628-94b3-f2aaef4a72c5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 0c5eb01b685d978d80916da0293cc2d3701b2d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-by-using-visual-studio"></a>Esercitazione: Creare una data factory con Visual Studio
> [!div class="op_single_selector" title="Tools/SDKs"]
> * [Panoramica e prerequisiti](data-factory-build-your-first-pipeline.md)
> * [Portale di Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Modello di Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)

In questa esercitazione illustra come toocreate una data factory di Azure tramite Visual Studio. Creare un progetto di Visual Studio con modello di progetto di Data Factory di hello, definiscono le entità Data Factory (servizi collegati, i set di dati e della pipeline) in formato JSON e quindi pubblicare o distribuire questi cloud toohello di entità. 

pipeline Hello in questa esercitazione è un'attività: **attività Hive di HDInsight**. Questa attività esegue uno script hive in un cluster HDInsight di Azure che trasformazioni i dati di output tooproduce di dati di input. pipeline di Hello è toorun pianificato dopo un mese tra hello specificato di ore di inizio e fine. 

> [!NOTE]
> Questa esercitazione non illustra come copiare dati con Azure Data Factory. Per un'esercitazione su come dati di toocopy tramite Data Factory di Azure, vedere [esercitazione: copiare i dati da archiviazione Blob tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Una pipeline può includere più attività Inoltre, è possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività. Per altre informazioni, vedere [Pianificazione ed esecuzione in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).


## <a name="walkthrough-create-and-publish-data-factory-entities"></a>Procedura dettagliata: Creare e pubblicare le entità della data factory
Ecco i passaggi di hello eseguite come parte di questa procedura dettagliata:

1. Creare due servizi collegati, **AzureStorageLinkedService1** e **HDInsightOnDemandLinkedService1**. 
   
    In questa esercitazione, i dati di input e di output da cui attività hive hello hello stessa archiviazione Blob di Azure. Si utilizza un su richiesta HDInsight cluster tooprocess dati di input tooproduce output dati esistente. cluster HDInsight su richiesta di Hello viene automaticamente creato automaticamente da Data Factory di Azure in fase di esecuzione quando i dati di input hello sono pronto toobe elaborati. È necessario toolink i dati vengono archiviati o calcola tooyour data factory in modo che il servizio di Data Factory hello può connettersi toothem in fase di esecuzione. Pertanto, collegare la data factory di Account di archiviazione Azure toohello utilizzando hello AzureStorageLinkedService1 e collegare un cluster di HDInsight su richiesta utilizzando hello HDInsightOnDemandLinkedService1. Quando si pubblica, si specifica il nome di hello per hello data factory toobe creato o una data factory esistente.  
2. Creare due set di dati: **InputDataset** e **OutputDataset**, che rappresentano dati di input/output di hello che viene archiviati in archiviazione blob di Azure hello. 
   
    Queste definizioni di set di dati, vedere il servizio di archiviazione di Azure collegati toohello creato nel passaggio precedente hello. Per hello InputDataset, specificare il contenitore di blob hello (adfgetstarted) e cartella (inptutdata) che contiene un blob con i dati di input hello hello. Per hello OutputDataset, specificare il contenitore di blob hello (adfgetstarted) e cartella hello (partitioneddata) che contiene i dati di output di hello. Specificare anche altre proprietà come struttura, disponibilità e criteri.
3. Creare una pipeline denominata **MyFirstPipeline**. 
  
    In questa procedura dettagliata, hello pipeline dispone di una sola attività: **attività Hive di HDInsight**. Attività Trasforma dati di input tooproduce dati di output eseguendo uno script hive in un cluster di HDInsight su richiesta. toolearn ulteriori informazioni sull'attività hive, vedere [attività Hive](data-factory-hive-activity.md) 
4. Creare una data factory denominata **DataFactoryUsingVS**. Distribuire hello data factory e tutte le entità Data Factory (servizi collegati, tabelle e pipeline hello).
5. Dopo la pubblicazione, utilizzare pannelli portali Azure e monitoraggio e gestione App pipeline hello toomonitor. 
  
### <a name="prerequisites"></a>Prerequisiti
1. Leggere [esercitazione Panoramica](data-factory-build-your-first-pipeline.md) articolo e hello completo **prerequisito** passaggi. È inoltre possibile selezionare hello **panoramica e prerequisiti** opzione nell'elenco a discesa hello articolo toohello di hello tooswitch superiore. Dopo aver completato i prerequisiti di hello, passa indietro toothis articolo selezionando **Visual Studio** opzione nell'elenco a discesa hello.
2. le istanze di Data Factory toocreate, è necessario essere un membro di hello [Data Factory collaboratore](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) ruolo a livello di gruppo di risorse di sottoscrizione/hello.  
3. È necessario disporre delle seguenti hello installato nel computer:
   * Visual Studio 2013 o Visual Studio 2015
   * Download di Azure SDK per Visual Studio 2013 o Visual Studio 2015. Passare troppo[pagina di Download di Azure](https://azure.microsoft.com/downloads/) e fare clic su **VS 2013** o **Visual Studio 2015** in hello **.NET** sezione.
   * Scaricare hello plug-in Data Factory di Azure più recenti per Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) o [Visual Studio 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). È inoltre possibile aggiornare i plug-in hello effettuando hello alla procedura seguente: hello scegliere **strumenti** -> **estensioni e aggiornamenti** -> **Online**  ->  **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools per Visual Studio** -> **aggiornamento**.

A questo punto, è possibile utilizzare Visual Studio toocreate una data factory di Azure.

### <a name="create-visual-studio-project"></a>Creare un progetto di Visual Studio
1. Avviare **Visual Studio 2013** o **Visual Studio 2015**. Fare clic su **File**, punto troppo**New**, fare clic su **progetto**. Dovrebbe essere hello **nuovo progetto** la finestra di dialogo.  
2. In hello **nuovo progetto** finestra di dialogo, seleziona hello **DataFactory** modello e fare clic su **progetto vuoto di Factory dati**.   

    ![Finestra di dialogo Nuovo progetto](./media/data-factory-build-your-first-pipeline-using-vs/new-project-dialog.png)
3. Immettere un **nome** per progetto hello, **percorso**e un nome per hello **soluzione**, fare clic su **OK**.

    ![Esplora soluzioni](./media/data-factory-build-your-first-pipeline-using-vs/solution-explorer.png)

### <a name="create-linked-services"></a>Creazione di servizi collegati
In questo passaggio si creano due servizi collegati: **Archiviazione di Azure** e **HDInsight su richiesta**. 

Hello archiviazione di Azure collegati collegamenti al servizio la data factory toohello account di archiviazione di Azure fornendo informazioni di connessione hello. Servizio Data Factory Usa stringa di connessione hello toohello tooconnect hello collegato un'impostazione di servizio di archiviazione di Azure in fase di esecuzione. Questa risorsa di archiviazione contiene input e output di dati pipeline hello e hello hive file script utilizzato dall'attività hive di hello. 

Con il servizio collegato di HDInsight su richiesta, hello cluster HDInsight viene creato automaticamente in fase di esecuzione quando i dati di input hello sono tooprocessed pronto. Hello cluster viene eliminato al termine per l'elaborazione e inattività per l'intervallo di tempo specificato hello. 

> [!NOTE]
> Creare una data factory specificando il nome e le impostazioni in fase di hello di pubblicare la soluzione di Data Factory.

#### <a name="create-azure-storage-linked-service"></a>Creare il servizio collegato Archiviazione di Azure
1. Fare doppio clic su **servizi collegati** in Esplora soluzioni hello punto troppo**Aggiungi**, fare clic su **nuovo elemento**.      
2. In hello **Aggiungi nuovo elemento** nella finestra di dialogo **servizio collegato di archiviazione di Azure** hello elenco e fare clic su **Aggiungi**.
    ![Servizio collegato Archiviazione di Azure](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)
3. Sostituire `<accountname>` e `<accountkey>` con nome hello dell'account di archiviazione Azure e la relativa chiave. toolearn come accedere a tooget lo spazio di archiviazione della chiave, vedere informazioni come tooview, copiare e rigenerare archiviazione accedere alle chiavi in hello [gestire account di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
    ![Servizio collegato Archiviazione di Azure](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)
4. Salvare hello **AzureStorageLinkedService1.json** file.

#### <a name="create-azure-hdinsight-linked-service"></a>Creare un servizio collegato Azure HDInsight
1. In hello **Esplora**, fare doppio clic su **servizi collegati**, punto troppo**Aggiungi**, fare clic su **nuovo elemento**.
2. Selezionare **HDInsight On Demand Linked Service** (Servizio collegato HDInsight su richiesta) e fare clic su **Aggiungi**.
3. Sostituire hello **JSON** con hello JSON seguente:

     ```json
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
        "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService1"
            }
        }
    }
    ```

    Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:

    Proprietà | Descrizione
    -------- | ----------- 
    ClusterSize | Specifica dimensioni hello di hello cluster HDInsight Hadoop.
    TimeToLive | Specifica il tempo di inattività hello per il cluster HDInsight hello, prima che venga eliminato.
    linkedServiceName | Specifica l'account di archiviazione hello toostore utilizzati hello registri generati da un cluster HDInsight Hadoop. 

    > [!IMPORTANT]
    > Crea cluster HDInsight Hello un **contenitore predefinito** nell'archiviazione blob hello specificato nel hello JSON (linkedServiceName). HDInsight non eliminare questo contenitore quando viene eliminato il cluster hello. Questo comportamento dipende dalla progettazione. Con il servizio collegato HDInsight su richiesta, viene creato un cluster HDInsight ogni volta che viene elaborata una sezione, a meno che non esista un cluster attivo (timeToLive). cluster Hello viene eliminato automaticamente quando viene eseguita un'elaborazione hello.
    > 
    > Man mano che vengono elaborate più sezioni, vengono visualizzati numerosi contenitori nell'archivio BLOB di Azure. Se non li necessario per la risoluzione dei problemi dei processi di hello, è opportuno toodelete li tooreduce hello il costo di archiviazione. i nomi di Hello di questi contenitori seguono un modello: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`. Utilizzare strumenti come [Esplora archivi Microsoft](http://storageexplorer.com/) toodelete contenitori di Azure nell'archiviazione blob.

    Per altre informazioni sulle proprietà JSON, vedere l'articolo relativo ai [servizi collegati di calcolo](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service). 
4. Salvare hello **HDInsightOnDemandLinkedService1.json** file.

### <a name="create-datasets"></a>Creare set di dati
In questo passaggio creare set di dati toorepresent hello input e output dei dati per l'elaborazione Hive. Questi set di dati di riferimento toohello **AzureStorageLinkedService1** creata precedentemente in questa esercitazione. Hello tooan punti di servizio collegato account di archiviazione di Azure e i set di dati specificare contenitore, cartella, nome del file nell'archiviazione hello che contiene l'input e output di dati.   

#### <a name="create-input-dataset"></a>Creare set di dati di input
1. In hello **Esplora**, fare doppio clic su **tabelle**, punto troppo**Aggiungi**, fare clic su **nuovo elemento**.
2. Selezionare **Blob di Azure** dall'elenco di hello, modificare il nome di hello del file hello troppo**InputDataSet.json**, fare clic su **Aggiungi**.
3. Sostituire hello **JSON** nell'editor di hello con hello frammento di codice JSON seguente:

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
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
    Questo frammento di codice JSON definisce un set di dati denominato **AzureBlobInput** che rappresenta i dati di input per l'attività hive di hello nella pipeline hello. Specificare che i dati di input hello si trovano nel contenitore di blob hello chiamato `adfgetstarted` e cartella hello denominata `inputdata`.

    Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:

    Proprietà | Descrizione |
    -------- | ----------- |
    type |proprietà tipo Hello è troppo**AzureBlob** perché i dati si trovano in archiviazione Blob di Azure.
    linkedServiceName | Si riferisce toohello AzureStorageLinkedService1 creato in precedenza.
    fileName |Questa proprietà è facoltativa. Se si omette questa proprietà, vengono selezionati tutti i file hello folderPath hello. In questo caso, viene elaborato solo hello input.log.
    type | file di log Hello sono in formato testo, permette di usare TextFormat. |
    columnDelimiter | le colonne nei file di log hello sono delimitate da virgola hello (`,`)
    frequenza/intervallo | frequenza impostata tooMonth e l'intervallo è 1, che significa che le sezioni di input hello sono disponibili ogni mese.
    external | Questa proprietà è impostata tootrue se i dati di input per l'attività hello hello non viene generati dalla pipeline hello. Viene specificata solo per i set di dati di input. Per hello input set di dati della prima attività hello sempre impostarla tootrue.
4. Salvare hello **InputDataset.json** file.

#### <a name="create-output-dataset"></a>Creare il set di dati di output
È quindi possibile creare hello output dataset toorepresent output dei dati archiviati in archiviazione Blob di Azure hello.

1. In hello **Esplora**, fare doppio clic su **tabelle**, punto troppo**Aggiungi**, fare clic su **nuovo elemento**.
2. Selezionare **Blob di Azure** dall'elenco di hello, modificare il nome di hello del file hello troppo**OutputDataset.json**, fare clic su **Aggiungi**.
3. Sostituire hello **JSON** nell'editor di hello con hello JSON seguente:
    
    ```json
    {
        "name": "AzureBlobOutput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
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
    frammento di codice JSON Hello definisce un set di dati denominato **AzureBlobOutput** che rappresenta i dati prodotti da attività hive di hello nella pipeline hello di output. Specificare che l'output di hello dati prodotto dall'attività hive hello inserito nel contenitore blob hello chiamato `adfgetstarted` e cartella hello denominata `partitioneddata`. 
    
    Hello **disponibilità** sezione specifica di tale set di dati di output di hello viene prodotto su base mensile. pianificazione di hello unità per set di dati di output Hello della pipeline hello. pipeline Hello viene eseguito ogni mese tra relativo ora di inizio e fine. 

    Vedere **creare set di dati input hello** sezione per le descrizioni di queste proprietà. Non si imposta proprietà esterna hello in un set di dati di output come set di dati hello viene generato dalla pipeline hello.
4. Salvare hello **OutputDataset.json** file.

### <a name="create-pipeline"></a>Creare una pipeline
È stato creato il servizio di archiviazione di Azure collegati hello e set di dati di input e output finora. Ora si creerà una pipeline con un'attività **HDInsightHive**. Hello **input** per hive hello attività viene impostato troppo**AzureBlobInput** e **output** è troppo**AzureBlobOutput**. Una sezione di un set di dati di input è disponibile ogni mese (frequenza: mese, intervallo: 1), e sezione di output di hello viene prodotta mensile troppo. 

1. In hello **Esplora**, fare doppio clic su **pipeline**, punto troppo**Aggiungi**, fare clic su **nuovo elemento.**
2. Selezionare **della Pipeline di trasformazione Hive** hello elenco e fare clic su **Aggiungi**.
3. Sostituire hello **JSON** con hello frammento di codice seguente:

    > [!IMPORTANT]
    > Sostituire `<storageaccountname>` con nome hello dell'account di archiviazione.

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService1",
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
            "start": "2016-04-01T00:00:00Z",
            "end": "2016-04-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    > [!IMPORTANT]
    > Sostituire `<storageaccountname>` con nome hello dell'account di archiviazione.

    frammento di codice JSON Hello definisce una pipeline che è costituito da una singola attività (attività Hive). Questa attività viene eseguito un Hive script tooprocess input di dati in un dati di output su richiesta tooproduce cluster HDInsight. Nella sezione di attività hello del formato JSON della pipeline hello, vedrai una sola attività nella matrice hello con tipo impostato troppo**HDInsightHive**. 

    In proprietà del tipo di hello che sono attività Hive tooHDInsight specifico, specificare il tipo di servizio collegato di archiviazione di Azure dispone di file di script hive hello, file di script toohello percorso hello e file di script toohello dei parametri. 

    file di script Hive Hello, **partitionweblogs.hql**, viene archiviato nell'account di archiviazione Azure hello (specificato da scriptLinkedService hello) e in hello `script` cartella nel contenitore hello `adfgetstarted`.

    Hello `defines` sezione è le impostazioni di runtime hello toospecify utilizzati script hive toohello passati come valori di configurazione di Hive (ad esempio `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.

    Hello **avviare** e **fine** le proprietà della pipeline hello specifica periodo attivo di hello della pipeline hello. È stata configurata hello dataset toobe prodotti mensili, pertanto, solo una volta alla sezione viene prodotta dalla pipeline hello (perché mese hello è lo stesso in date di inizio e fine).

    In formato JSON dell'attività hello, specificare tale script Hive hello viene eseguito sul calcolo hello specificato da hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.
4. Salvare hello **HiveActivity1.json** file.

### <a name="add-partitionweblogshql-and-inputlog-as-a-dependency"></a>Aggiungere partitionweblogs.hql e input.log come dipendenza
1. Fare doppio clic su **dipendenze** in hello **Esplora** finestra, scegliere troppo**Aggiungi**, fare clic su **elemento esistente**.  
2. Passare toohello **C:\ADFGettingStarted** e selezionare **partitionweblogs.hql**, **input.log** file e fare clic su **Aggiungi**. Questi due file è stato creato come parte dei prerequisiti da hello [Panoramica esercitazione](data-factory-build-your-first-pipeline.md).

Quando si pubblica la soluzione hello nel passaggio successivo hello, hello **partitionweblogs.hql** file viene caricato toohello **script** cartella hello `adfgetstarted` contenitore blob.   

### <a name="publishdeploy-data-factory-entities"></a>Pubblicare/Distribuire le entità della data factory
In questo passaggio si pubblicazione delle entità di Data Factory hello (servizi collegati, i set di dati e della pipeline) nei toohello progetto servizio Azure Data Factory. Nel processo di hello di pubblicazione, specificare il nome di hello per la data factory. 

1. Fare clic sul progetto in Esplora soluzioni hello e fare clic su **pubblica**.
2. Se viene visualizzato **Accedi tooyour account Microsoft** nella finestra di dialogo immettere le credenziali di account hello con sottoscrizione di Azure e fare clic su **Accedi**.
3. È necessario visualizzare hello la finestra di dialogo seguenti:

   ![Finestra di dialogo Pubblica](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
4. In hello **Configura data factory di** pagina, hello i passaggi seguenti:

    ![Pubblicazione: impostazioni per una nuova data factory](media/data-factory-build-your-first-pipeline-using-vs/publish-new-data-factory.png)

   1. Selezionare l’opzione **Crea nuova data factory** .
   2. Immettere un univoco **nome** per data factory di hello. ad esempio **DataFactoryUsingVS09152016**. nome Hello deve essere globalmente univoco.
   3. Selezionare la sottoscrizione destra di hello per hello **sottoscrizione** campo. 
        > [!IMPORTANT]
        > Se non viene visualizzata alcuna sottoscrizione, assicurarsi che si è connessi con un account che è un amministratore o co-amministratore della sottoscrizione hello.
   4. Seleziona hello **gruppo di risorse** per hello data factory toobe creato.
   5. Seleziona hello **area** per data factory di hello.
   6. Fare clic su **Avanti** tooswitch toohello **pubblicare elementi** pagina. (Premere **scheda** toomove fuori hello di hello Nome campo tooif **Avanti** pulsante è disabilitato.)

    > [!IMPORTANT]
    > Se viene visualizzato l'errore hello **"DataFactoryUsingVS" nome della Data factory non è disponibile** durante la pubblicazione, modificare il nome di hello (ad esempio, yournameDataFactoryUsingVS). Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .   
1. In hello **pubblicare elementi** pagina, assicurarsi che tutti hello Data factory di entità vengono selezionate e fare clic su **Avanti** tooswitch toohello **riepilogo** pagina.

    ![Pagina Publish Items (Pubblica elementi)](media/data-factory-build-your-first-pipeline-using-vs/publish-items-page.png)     
2. Esaminare hello riepilogo e fare clic su **Avanti** toostart hello distribuzione elaborare e visualizzare hello **lo stato di distribuzione**.

    ![Pagina Riepilogo](media/data-factory-build-your-first-pipeline-using-vs/summary-page.png)
3. In hello **lo stato di distribuzione** pagina, dovrebbe essere stato hello hello processo di distribuzione. Dopo la distribuzione hello viene eseguita, fare clic su Fine.

Toonote punti importanti:

- Se viene visualizzato l'errore hello: **questa sottoscrizione non è registrato toouse dello spazio dei nomi Microsoft. DataFactory**, effettuare una delle seguenti hello e riprovare:
    - In Azure PowerShell, eseguire hello seguenti provider di comandi tooregister hello Data Factory.
        ```PowerShell   
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
        ```
        È possibile eseguire hello successivo comando tooconfirm tale hello Data Factory di provider è registrato.

        ```PowerShell
        Get-AzureRmResourceProvider
        ```
    - Account di accesso tramite hello sottoscrizione di Azure in toohello [portale di Azure](https://portal.azure.com) e passare a pannello di Data Factory tooa creare una data factory nel portale di Azure hello (o). Questa azione registra automaticamente i provider di hello.
- nome Hello della hello data factory può essere registrato come un nome DNS in futuro hello e pertanto diventano visibili pubblicamente.
- le istanze di Data Factory toocreate, è necessario toobe un amministratore o co-amministratore della sottoscrizione di Azure hello

### <a name="monitor-pipeline"></a>Monitorare la pipeline
In questo passaggio è monitorare pipeline hello tramite vista diagramma della data factory di hello. 

#### <a name="monitor-pipeline-using-diagram-view"></a>Monitorare la pipeline con la vista diagramma
1. Accedi toohello [portale di Azure](https://portal.azure.com/), hello i passaggi seguenti:
   1. Fare clic su **Altri servizi** e quindi su **Data factory**.
       
        ![Esplora data factory](./media/data-factory-build-your-first-pipeline-using-vs/browse-datafactories.png)
   2. Nome di hello selezionare la data factory (ad esempio: **DataFactoryUsingVS09152016**) dall'elenco di hello di data factory.
   
       ![Selezionare la data factory](./media/data-factory-build-your-first-pipeline-using-vs/select-first-data-factory.png)
2. Nella pagina iniziale di hello per la data factory, fare clic su **diagramma**.

    ![Riquadro Diagramma](./media/data-factory-build-your-first-pipeline-using-vs/diagram-tile.png)
3. In vista diagramma hello, si visualizza una panoramica di pipeline hello e set di dati utilizzati in questa esercitazione.

    ![Vista Diagramma](./media/data-factory-build-your-first-pipeline-using-vs/diagram-view-2.png)
4. tooview tutte le attività nella pipeline di hello, pipeline pulsante destro del mouse in hello diagramma e fare clic su Apri Pipeline.

    ![Menu Apri pipeline](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-menu.png)
5. Confermare la visualizzazione attività HDInsightHive hello nella pipeline hello.

    ![Visualizzazione Apri pipeline](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-view.png)

    toonavigate nuovamente toohello visualizzazione precedente, fare clic su **Data factory** nel menu di navigazione hello nella parte superiore di hello.
6. In hello **vista diagramma**, fare doppio clic sul set di dati hello **AzureBlobInput**. Verificare che tale sezione hello sia **pronto** stato. Potrebbe richiedere un paio di minuti per hello sezione tooshow fino nello stato pronto. Se non si verifica dopo attendere qualche minuto, verificare se si dispone di hello file di input (input.log) incluso nel contenitore destra hello (`adfgetstarted`) e cartella (`inputdata`). E, assicurarsi che tale hello **esterno** nel set di dati input hello è impostata troppo**true**. 

   ![Sezione di input nello stato Pronto](./media/data-factory-build-your-first-pipeline-using-vs/input-slice-ready.png)
7. Fare clic su **X** tooclose **AzureBlobInput** blade.
8. In hello **vista diagramma**, fare doppio clic sul set di dati hello **AzureBlobOutput**. Vedrai tale sezione hello che è in corso di elaborazione.

   ![Set di dati](./media/data-factory-build-your-first-pipeline-using-vs/dataset-blade.png)
9. Quando viene eseguita l'elaborazione, vedrai sezione hello **pronto** stato.

   > [!IMPORTANT]
   > La creazione di un cluster HDInsight su richiesta di solito richiede tempo (circa 20 minuti). Pertanto, prevedere hello pipeline tootake **circa 30 minuti** tooprocess hello sezione.  
   
    ![Set di dati](./media/data-factory-build-your-first-pipeline-using-vs/dataset-slice-ready.png)    
10. Quando si trova in sezione hello **pronto** stato, controllare hello `partitioneddata` cartella hello `adfgetstarted` contenitore nell'archiviazione blob per hello i dati di output.  

    ![Dati di output](./media/data-factory-build-your-first-pipeline-using-vs/three-ouptut-files.png)
11. Fare clic su hello sezione toosee dettagli in un **sezione dati** blade.

    ![Dettagli sezione dati](./media/data-factory-build-your-first-pipeline-using-vs/data-slice-details.png)  
12. Fare clic su un'attività eseguire in hello **elenco viene eseguita l'attività** toosee dettagli su un'attività (attività Hive nello scenario di esempio) di eseguire in un **Dettagli esecuzione attività** finestra. 
  
    ![Dettagli esecuzione attività](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-blade.png)    

    Dai file di log hello, è possibile visualizzare informazioni sullo stato e query Hive hello che è stato eseguito. Tali file di log sono utili per risolvere eventuali problemi.  

Vedere [monitorare set di dati e della pipeline](data-factory-monitor-manage-pipelines.md) per istruzioni su come pipeline di hello toouse hello toomonitor portale Azure e set di dati è stato creato in questa esercitazione.

#### <a name="monitor-pipeline-using-monitor--manage-app"></a>Monitorare la pipeline con l'app Monitoraggio e gestione
È possibile anche utilizzare Monitoraggio e Gestione applicazione toomonitor le pipeline. Per informazioni dettagliate sull'uso di questa applicazione, vedere [Monitorare e gestire le pipeline di Azure Data Factory con la nuova app di monitoraggio e gestione](data-factory-monitor-manage-app.md).

1. Fare clic sul riquadro Monitoraggio e gestione.

    ![Riquadro Monitoraggio e gestione](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-tile.png)
2. Verrà visualizzata l'applicazione Monitoraggio e gestione. Hello modifica **ora di inizio** e **ora di fine** toomatch iniziale (01-04-2016 12:00 AM) e l'ora di fine (04-02-2016 12:00 AM) di pipeline, fare clic su **applica**.

    ![App Monitoraggio e gestione](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-app.png)
3. Dettagli toosee su una finestra attività, selezionarlo in hello **elenco attività Windows** dettagli toosee.
    ![Dettagli finestra attività](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)

> [!IMPORTANT]
> file di input Hello eliminato quando la sezione hello viene elaborata correttamente. Pertanto, se si desidera toorerun hello sezione o hello esercitazione nuovamente, caricare hello del file di input (input.log) toohello `inputdata` cartella di hello `adfgetstarted` contenitore.

### <a name="additional-notes"></a>Note aggiuntive
- Una data factory può comprendere una o più pipeline. Una pipeline può comprendere una o più attività. Dati di input, ad esempio, una data toocopy attività di copia da un archivio dati di origine tooa destinazione e un toorun attività Hive di HDInsight un tootransform script Hive. Vedere [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) per tutti hello origini e sink supportati dall'attività di copia hello. Vedere [servizi collegati di calcolo](data-factory-compute-linked-services.md) per elenco hello di servizi di calcolo supportati da Data Factory.
- Servizi collegati collegano archivi dati o servizi tooan data factory di Azure di calcolo. Vedere [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) per tutti hello origini e sink supportati dall'attività di copia hello. Vedere [servizi collegati di calcolo](data-factory-compute-linked-services.md) per elenco hello di servizi di calcolo supportati da Data Factory e [le attività di trasformazione](data-factory-data-transformation-activities.md) che è possibile eseguire su di essi.
- Vedere [spostare i dati da / Blob tooAzure](data-factory-azure-blob-connector.md#azure-storage-linked-service) per dettagli sulle proprietà JSON utilizzato in hello collegato definizione del Servizio archiviazione di Azure.
- È possibile usare il proprio cluster HDInsight anziché un cluster HDInsight su richiesta. Per informazioni dettagliate, vedere [Servizi collegati di calcolo](data-factory-compute-linked-services.md) .
-  Hello Data Factory viene creata una **basati su Linux** cluster HDInsight per l'utente con hello precedente JSON. Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .
- Crea cluster HDInsight Hello un **contenitore predefinito** nell'archiviazione blob hello specificato nel hello JSON (linkedServiceName). HDInsight non eliminare questo contenitore quando viene eliminato il cluster hello. Questo comportamento dipende dalla progettazione. Con il servizio collegato HDInsight su richiesta, viene creato un cluster HDInsight ogni volta che viene elaborata una sezione, a meno che non esista un cluster attivo (timeToLive). cluster Hello viene eliminato automaticamente quando viene eseguita un'elaborazione hello.
    
    Man mano che vengono elaborate più sezioni, vengono visualizzati numerosi contenitori nell'archivio BLOB di Azure. Se non li necessario per la risoluzione dei problemi dei processi di hello, è opportuno toodelete li tooreduce hello il costo di archiviazione. i nomi di Hello di questi contenitori seguono un modello: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`. Utilizzare strumenti come [Esplora archivi Microsoft](http://storageexplorer.com/) toodelete contenitori di Azure nell'archiviazione blob.
- Set di dati di output è attualmente, quali unità hello pianificazione, pertanto è necessario creare un set di dati di output, anche se l'attività hello non genera alcun output. Se l'attività hello non accetta alcun input, è possibile ignorare i set di dati input hello creazione. 
- Questa esercitazione non illustra come copiare dati con Azure Data Factory. Per un'esercitazione su come dati di toocopy tramite Data Factory di Azure, vedere [esercitazione: copiare i dati da archiviazione Blob tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).


## <a name="use-server-explorer-tooview-data-factories"></a>Utilizzare Esplora Server tooview data factory
1. In **Visual Studio**, fare clic su **vista** hello menu e fare clic su **Esplora Server**.
2. Nella finestra di Esplora Server hello, espandere **Azure** espandere **Data Factory**. Se viene visualizzato **Accedi tooVisual Studio**, immettere hello **account** associata con la sottoscrizione di Azure e fare clic su **continua**. Immettere la **password** e fare clic su **Accedi**. Visual Studio tenta tooget informazioni su tutte le data factory di Azure nella sottoscrizione. Viene visualizzato lo stato di hello di questa operazione in hello **elenco attività di Data Factory** finestra.

    ![Esplora server](./media/data-factory-build-your-first-pipeline-using-vs/server-explorer.png)
3. È possibile fare doppio clic su una data factory e selezionare **tooNew esportare Data Factory progetto** toocreate un progetto di Visual Studio basato su una data factory esistente.

    ![Data factory di Azure](./media/data-factory-build-your-first-pipeline-using-vs/export-data-factory-menu.png)

## <a name="update-data-factory-tools-for-visual-studio"></a>Aggiornare gli strumenti di Data factory di Azure per Visual Studio
hello tooupdate strumenti di Data Factory di Azure per Visual Studio, come segue:

1. Fare clic su **strumenti** nel menu hello e selezionare **estensioni e aggiornamenti**.
2. Selezionare **aggiornamenti** in hello riquadro sinistro e quindi selezionare **Visual Studio Gallery**.
3. Selezionare **Azure Data Factory tools for Visual Studio** e fare clic su **Aggiorna**. Se non viene visualizzata questa voce, si dispone già di più recente degli strumenti hello hello.

## <a name="use-configuration-files"></a>Usare i file di configurazione
È possibile utilizzare i file di configurazione nelle proprietà tooconfigure di Visual Studio per servizi/tabelle/pipeline del collegato in modo diverso per ogni ambiente.

Prendere in considerazione hello seguente definizione JSON per un servizio collegato di archiviazione di Azure. toospecify **connectionString** con valori diversi per accountname e accountkey in base a hello ambiente (sviluppo/Test o produzione) toowhich si distribuiscono le entità di Data Factory. usare un file di configurazione separato per ogni ambiente.

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="add-a-configuration-file"></a>Aggiungere un file di configurazione
Aggiungere un file di configurazione per ogni ambiente eseguendo hello alla procedura seguente:   

1. Fare clic sul progetto Data Factory hello nella soluzione Visual Studio, scegliere troppo**Aggiungi**, fare clic su **nuovo elemento**.
2. Selezionare **Config** selezionare nell'elenco dei modelli installati a sinistra di hello hello **File di configurazione**, immettere un **nome** per la configurazione di hello file e fare clic su **Aggiungere**.

    ![Aggiungere un file di configurazione](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. Aggiungere parametri di configurazione e i relativi valori in hello seguente formato:

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    Questo esempio configura la proprietà connectionString di un servizio collegato Archiviazione di Azure e di un servizio collegato Azure SQL. Si noti che la sintassi di hello per specificare nome [JsonPath](http://goessner.net/articles/JsonPath/).   

    Se JSON ha una proprietà che è una matrice di valori, come illustrato nel seguente codice hello:  

    ```json
    "structure": [
          {
              "name": "FirstName",
            "type": "String"
          },
          {
            "name": "LastName",
            "type": "String"
        }
    ],
    ```

    Configurare le proprietà come illustrato nel seguente file di configurazione (utilizzare indicizzazione in base zero) hello:

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a>Nomi delle proprietà con spazi
Se un nome di proprietà contiene spazi, utilizzare le parentesi quadre, come illustrato in hello (nome server di Database) di esempio seguente:

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a>Distribuire la soluzione usando una configurazione
Quando si pubblicano le entità di Azure Data Factory in Visual Studio, è possibile specificare una configurazione di hello che si vuole toouse per tale operazione di pubblicazione.

entità toopublish in un progetto di Data Factory di Azure tramite file di configurazione:   

1. Fare clic sul progetto Data Factory e fare clic su **pubblica** toosee hello **pubblicare elementi** la finestra di dialogo.
2. Selezionare una data factory esistente oppure specificare valori per la creazione di una data factory in hello **Configura data factory di** pagina e fare clic su **Avanti**.   
3. In hello **pubblicare elementi** pagina: viene visualizzato un elenco a discesa con le configurazioni disponibili per hello **selezionare configurazione della distribuzione** campo.

    ![Selezionare un file di configurazione](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. Seleziona hello **file di configurazione** che desideri toouse e fare clic su **Avanti**.
5. Assicurarsi di visualizzare il nome di hello del file JSON in hello **riepilogo** pagina e fare clic su **Avanti**.
6. Fare clic su **fine** al termine dell'operazione di distribuzione hello.

Quando si distribuisce, i valori hello dal file di configurazione hello sono tooset utilizzati valori di proprietà nei file JSON hello prima entità hello tooAzure distribuito il servizio Data Factory.   

## <a name="use-azure-key-vault"></a>Usare l'Insieme di credenziali delle chiavi di Azure
Non è consigliabile e spesso rispetto ai dati sensibili toocommit criteri di sicurezza, ad esempio repository di codice toohello stringhe di connessione. Vedere [ADF Secure pubblicare](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample in GitHub toolearn sull'archiviazione di informazioni riservate nell'insieme di credenziali chiave di Azure e l'uso durante la pubblicazione entità Data Factory. Hello Secure pubblicare l'estensione di Visual Studio consente hello toobe di segreti archiviati nell'insieme di credenziali chiave e solo i riferimenti toothem vengono specificati in servizi collegati o configurazioni di distribuzione. Questi riferimenti vengono risolti durante la pubblicazione tooAzure entità Data Factory. Questi file possono quindi essere eseguito il commit toosource repository senza esporre tutti i segreti.

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

È possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività. Per informazioni dettagliate, vedere [Pianificazione ed esecuzione con Data Factory](data-factory-scheduling-and-execution.md). 


## <a name="see-also"></a>Vedere anche
| Argomento | Descrizione |
|:--- |:--- |
| [Pipeline](data-factory-create-pipelines.md) |In questo articolo consente di comprendere le pipeline e attività nella Data Factory di Azure e come toouse li tooconstruct basati sui dati dei flussi di lavoro degli scenario o dell'azienda. |
| [Set di dati](data-factory-create-datasets.md) |Questo articolo fornisce informazioni sui set di dati in Azure Data Factory. |
| [Attività di trasformazione dei dati](data-factory-data-transformation-activities.md) |Questo articolo fornisce un elenco di attività di trasformazione dei dati (ad esempio, la trasformazione Hive di HDInsight usata in questa esercitazione) supportate da Azure Data Factory. |
| [Pianificazione ed esecuzione](data-factory-scheduling-and-execution.md) |Questo articolo illustra gli aspetti hello di pianificazione e l'esecuzione del modello di applicazione di Azure Data Factory. |
| [Monitorare e gestire le pipeline con l'app di monitoraggio](data-factory-monitor-manage-app.md) |In questo articolo viene descritto come toomonitor, gestire ed eseguire il debug pipeline utilizzando hello monitoraggio e gestione delle App. |
