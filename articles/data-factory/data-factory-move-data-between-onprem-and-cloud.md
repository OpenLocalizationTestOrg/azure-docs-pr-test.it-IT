---
title: dati aaaMove - Gateway di gestione dati | Documenti Microsoft
description: Impostare un data gateway toomove di dati tra sedi locali e hello cloud. Usare Gateway di gestione dati in Azure Data Factory toomove i dati.
keywords: gateway dati, integrazione di dati, spostare dati, credenziali del gateway
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 7bf6d8fd-04b5-499d-bd19-eff217aa4a9c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 314341c142d5260c785b7e82081774f044450e81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-between-on-premises-sources-and-hello-cloud-with-data-management-gateway"></a>Spostare dati tra origini locali e cloud hello con Gateway di gestione dati
Questo articolo offre una panoramica sull'integrazione tra archivi dati locali e archivi dati cloud con Data Factory. È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo e altri articoli concetti principali di data factory: [set di dati](data-factory-create-datasets.md) e [pipeline](data-factory-create-pipelines.md).

## <a name="data-management-gateway"></a>Gateway di gestione dati
È necessario installare il Gateway di gestione di dati nel tooenable macchina locale lo spostamento dei dati da e verso un archivio dati locale. Hello gateway può essere installato su hello che stesso computer come archivio dati hello o in un computer diverso, purché il gateway di hello possa connettersi toohello archivio di dati.

> [!IMPORTANT]
> Leggere l'articolo [Gateway di gestione dati](data-factory-data-management-gateway.md) per i dettagli sul Gateway di gestione dati. 

Hello seguente procedura dettagliata illustra come una data factory con una pipeline che sposta i dati da una locale toocreate **SQL Server** database archivio blob di Azure tooan. Come parte della procedura dettagliata di hello, installare e configurare hello Gateway di gestione dati nel computer.

## <a name="walkthrough-copy-on-premises-data-toocloud"></a>Procedura dettagliata: copiare toocloud dati locale
In questa procedura dettagliata hello i passaggi seguenti: 

1. Creare una data factory.
2. Creare un gateway di gestione dati. 
3. Creare servizi collegati per gli archivi dati di origine e sink.
4. Creare set di dati toorepresent input e output dei dati.
5. Creare una pipeline con un copia attività toomove hello dati.

## <a name="prerequisites-for-hello-tutorial"></a>Prerequisiti per l'esercitazione hello
Prima di iniziare questa procedura dettagliata, è necessario disporre di hello seguenti prerequisiti:

* **Sottoscrizione di Azure**.  Se non è disponibile una sottoscrizione, è possibile creare un account di valutazione gratuita in pochi minuti. Vedere hello [versione di valutazione gratuita](http://azure.microsoft.com/pricing/free-trial/) articolo per informazioni dettagliate.
* **Account di archiviazione di Azure**. Usare l'archiviazione di blob hello come un **destinazione/sink** archivio dati in questa esercitazione. Se non si dispone di un account di archiviazione di Azure, vedere hello [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) articolo per passaggi toocreate uno.
* **SQL Server**. Usare un database di SQL Server locale come archivio dati di **origine** in questa esercitazione. 

## <a name="create-data-factory"></a>Creare un'istanza di Data Factory
In questo passaggio, si usa hello Azure toocreate portale un'istanza di Azure Data Factory denominato **ADFTutorialOnPremDF**.

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **+ Nuovo**, su **Intelligence e analisi** e quindi su **Data factory**.

   ![Nuovo->DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. In hello **nuova data factory** pagina, immettere **ADFTutorialOnPremDF** per hello Name.

    ![Aggiungere tooStartboard](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > nome Hello di hello Azure data factory deve essere globalmente univoco. Se viene visualizzato l'errore hello: **"ADFTutorialOnPremDF" nome della Data factory non è disponibile**, modificare il nome di hello di hello data factory (ad esempio, yournameADFTutorialOnPremDF) e provare a creare di nuovo. Durante l'esecuzione dei passaggi rimanenti in questa esercitazione usare questo nome anziché ADFTutorialOnPremDF.
   >
   > nome Hello della hello data factory può essere registrato come un **DNS** nome nel futuro hello e pertanto diventano visibili pubblicamente.
   >
   >
4. Seleziona hello **sottoscrizione di Azure** in cui si desidera hello data factory toobe creato.
5. Selezionare un **gruppo di risorse** esistente o crearne uno. Per l'esercitazione hello, creare un gruppo di risorse denominato: **ADFTutorialResourceGroup**.
6. Fare clic su **crea** su hello **nuova data factory** pagina.

   > [!IMPORTANT]
   > le istanze di Data Factory toocreate, è necessario essere un membro di hello [Data Factory collaboratore](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) ruolo a livello di gruppo di risorse di sottoscrizione/hello.
   >
   >
7. Una volta completata la creazione, vedrai hello **Data Factory** pagina come illustrato nella seguente immagine hello:

   ![Home page di Data Factory](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a>Creare il gateway
1. In hello **Data Factory** pagina, fare clic su **autore e distribuire** riquadro toolaunch hello **Editor** per data factory di hello.

    ![Riquadro Creare e distribuire](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. Nell'Editor delle Data Factory hello, fare clic su **... Ulteriori** hello barra degli strumenti e quindi fare clic su **nuovo gateway dati**. In alternativa, è possibile fare doppio clic **gateway dati** in hello visualizzazione struttura ad albero, quindi fare clic su **nuovo gateway dati**.

   ![Nuovo gateway di dati nella barra degli strumenti](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. In hello **crea** pagina, immettere **adftutorialgateway** per hello **nome**, fare clic su **OK**.     

    ![Pagina per la creazione del gateway](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > In questa procedura dettagliata, si crea gateway logico hello con un solo nodo (computer di Windows locale). È possibile scalare orizzontalmente un gateway di gestione di dati mediante l'associazione di più computer locali con gateway hello. È possibile aumentare le prestazioni aumentando il numero di processi di spostamento di dati eseguibili contemporaneamente in un nodo. Questa funzionalità è disponibile anche per un gateway logico con un singolo nodo. Per informazioni dettagliate, vedere l'articolo [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) (Gateway di gestione dati - Disponibilità elevata e scalabilità (anteprima).  
4. In hello **configura** pagina, fare clic su **installare direttamente in questo computer**. Questa azione Scarica il pacchetto di installazione hello per gateway hello, installa, configura e registra gateway hello computer hello.  

   > [!NOTE]
   > Usare Internet Explorer o un Web browser compatibile con Microsoft ClickOnce.
   >
   > Se si utilizza Chrome, andare toohello [archivio web Chrome](https://chrome.google.com/webstore/), eseguire la ricerca con la parola chiave "ClickOnce", scegliere una delle estensioni di ClickOnce hello e installarlo.
   >
   > Hello stesso per Firefox (Installa componente aggiuntivo). Fare clic su **Apri Menu** sulla barra degli strumenti hello (**tre linee orizzontali** nell'angolo superiore destro hello), fare clic su **componenti aggiuntivi**, eseguire la ricerca con la parola chiave "ClickOnce", scegliere una delle hello Estensioni di ClickOnce e installarlo.    
   >
   >

    ![Gateway - Pagina Configura](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    In questo modo è più semplice toodownload modo (un solo clic) hello, installare, configurare e registrare il gateway di hello in un unico passaggio. È possibile visualizzare hello **Gestione configurazione di Microsoft Data Management Gateway** applicazione è installata nel computer in uso. È anche possibile trovare hello eseguibile **ConfigManager.exe** nella cartella hello: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.

    È anche possibile scaricare e installare il gateway manualmente utilizzando i collegamenti di hello in questa pagina e registrarlo con chiave hello indicata nella hello **nuova chiave** casella di testo.

    Vedere [Gateway di gestione dati](data-factory-data-management-gateway.md) articolo per tutti i dettagli sul gateway hello di hello.

   > [!NOTE]
   > È necessario essere un amministratore hello tooinstall di computer locale e configurare correttamente hello Gateway di gestione dati. È possibile aggiungere altri utenti toohello **Data Management Gateway Users** gruppo locale di Windows. membri di Hello di questo gruppo possono usare gateway di hello gestione di configurazione di Gateway di gestione dati strumento tooconfigure hello.
   >
   >
5. Attendere un paio di minuti o attendere fino a visualizzare hello seguente messaggio di notifica:

    ![Installazione del gateway riuscita](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. Avviare l'applicazione **Gateway di gestione dati di Configuration Manager** nel computer. In hello **ricerca** finestra **Gateway di gestione dati** tooaccess questo utilità. È anche possibile trovare hello eseguibile **ConfigManager.exe** nella cartella hello: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

    ![Gestione configurazione di gateway](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. Verificare che venga visualizzato il messaggio `adftutorialgateway is connected toohello cloud service`. Consente di visualizzare hello nella parte inferiore della barra di stato Hello **toohello cloud servizio connesso** insieme a un **segno di spunta verde**.

    In hello **Home** scheda, è inoltre possibile eseguire hello seguenti operazioni:

   * **Registrare** un gateway con una chiave dal portale di Azure usando il pulsante Registro hello hello.
   * **Arrestare** hello Gateway Host servizio di gestione dati in esecuzione nel computer gateway.
   * **Pianificare gli aggiornamenti** toobe installato in un momento specifico del giorno hello.
   * Verificare quando è stato gateway hello **ultimo aggiornamento**.
   * Specificare l'ora in cui è possibile installare un gateway toohello di aggiornamento.
8. Passare toohello **impostazioni** scheda hello certificato hello **certificato** sezione è costituita dalle credenziali tooencrypt/decrittografia utilizzati per l'archivio di dati locale hello specificato nel portale di hello. (facoltativo) Fare clic su **modifica** toouse il proprio certificato invece. Per impostazione predefinita, il gateway hello utilizza certificato hello è generato automaticamente da hello servizio Data Factory.

    ![Configurazione certificati del gateway](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    È inoltre possibile eseguire hello le azioni seguenti sulla hello **impostazioni** scheda:

   * Consente di visualizzare o esportare il certificato di hello usato dal gateway hello.
   * Modificare l'endpoint HTTPS hello usati dal gateway hello.    
   * Impostare un toobe proxy HTTP utilizzato dal gateway hello.     
9. (facoltativo) Passare toohello **diagnostica** scheda, controllare hello **abilitare la registrazione dettagliata** opzione se si desidera la registrazione che è possibile utilizzare tootroubleshoot eventuali problemi con il gateway hello dettagliata tooenable. Hello informazioni di registrazione possono trovarsi **Visualizzatore eventi** in **registri applicazioni e servizi** -> **Gateway di gestione dati** nodo.

    ![Scheda Diagnostica](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    È inoltre possibile eseguire dopo le azioni in hello hello **diagnostica** scheda:

   * Utilizzare **Test connessione** origine dati locale tooan sezione usando hello gateway.
   * Fare clic su **Visualizza log** toosee hello Gateway di gestione dati di log in una finestra del Visualizzatore eventi.
   * Fare clic su **inviare i log** tooupload un file zip con log di ultimi sette giorni tooMicrosoft toofacilitate risoluzione dei problemi.
10. In hello **diagnostica** scheda hello **Test connessione** selezionare **SqlServer** per tipo hello hello dati archivio, immettere il nome di hello hello del server di database, nome del Hello database, specificare il tipo di autenticazione, immettere nome utente e password e fare clic su **Test** tootest se gateway hello può connettersi toohello database.
11. Browser web toohello di commutatore e in hello **portale di Azure**, fare clic su **OK** su hello **configura** pagina e quindi su hello **nuovo gateway dati** pagina.
12. Dovrebbe essere **adftutorialgateway** in **gateway dati** nella visualizzazione ad albero di hello a sinistra di hello.  Se è selezionata, verrà visualizzato hello associata JSON.

## <a name="create-linked-services"></a>Creare servizi collegati
In questo passaggio vengono creati due servizi collegati: **AzureStorageLinkedService** e **SqlServerLinkedService**. Hello **SqlServerLinkedService** collega un database di SQL Server locale e hello **AzureStorageLinkedService** servizio collegato collega una data factory di toohello archivio blob di Azure. Una pipeline viene creata più avanti in questa procedura dettagliata che copia i dati dal database SQL Server on-premise di hello toohello archivio di blob di Azure.

#### <a name="add-a-linked-service-tooan-on-premises-sql-server-database"></a>Aggiungere un database di SQL Server on-premise tooan servizio collegato
1. In hello **Editor delle Data Factory**, fare clic su **nuovo archivio dati** sulla barra degli strumenti hello e selezionare **SQL Server**.

   ![Nuovo servizio collegato di SQL Server](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. In hello **editor JSON** su hello destra, hello i passaggi seguenti:

   1. Per hello **gatewayName**, specificare **adftutorialgateway**.    
   2. In hello **connectionString**, hello i passaggi seguenti:    

      1. Per **servername**, immettere il nome di hello del server di hello che ospita il database di SQL Server hello.
      2. Per **databasename**, immettere il nome di hello del database di hello.
      3. Fare clic su **Encrypt** sulla barra degli strumenti hello. Viene visualizzata l'applicazione di gestione credenziali di hello.

         ![Applicazione Gestione credenziali](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. In hello **impostazione delle credenziali** la finestra di dialogo, specificare il tipo di autenticazione, nome utente e password e fare clic su **OK**. Se la connessione hello ha esito positivo, crittografato hello credenziali vengono archiviate in hello JSON e chiude la finestra di dialogo hello.
      5. Chiudere scheda del browser vuota hello avviata la finestra di dialogo hello se non viene chiuso automaticamente e tornare scheda toohello con hello portale di Azure.

         Nel computer gateway hello, queste credenziali sono **crittografati** proprietario di servizio utilizzando un certificato che hello Data Factory. Se si desidera certificato hello toouse viene invece associato hello Gateway di gestione dati, vedere [impostare in modo sicuro le credenziali](#set-credentials-and-security).    
   3. Fare clic su **Distribuisci** sul comando hello barra toodeploy hello servizio collegato SQL Server. Verrà visualizzato il servizio collegato hello nella visualizzazione ad albero di hello.

      ![Servizio collegato SQL Server nella visualizzazione ad albero hello](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a>Aggiungere un servizio collegato per un account di archiviazione di Azure
1. In hello **Editor delle Data Factory**, fare clic su **nuovo archivio dati** hello barra dei comandi e fare clic su **archiviazione di Azure**.
2. Immettere nome hello dell'account di archiviazione di Azure per hello **nome Account**.
3. Immettere la chiave hello per l'account di archiviazione di Azure per hello **chiave dell'Account**.
4. Fare clic su **Distribuisci** toodeploy hello **AzureStorageLinkedService**.

## <a name="create-datasets"></a>Creare set di dati
In questo passaggio, creare input e output di set di dati che rappresentano i dati di input e outpui per l'operazione di copia hello (database di SQL Server in locale = > archiviazione blob di Azure). Prima di creare set di dati, hello (procedura dettagliata seguente elenco hello) come segue:

* Creare una tabella denominata **emp** in Database di SQL Server è stato aggiunto come una data factory di servizio collegato toohello hello e inserire un paio di voci di esempio nella tabella hello.
* Creare un contenitore blob denominato **adftutorial** in hello Azure blob account di archiviazione è stato aggiunto come una data factory toohello servizio collegato.

### <a name="prepare-on-premises-sql-server-for-hello-tutorial"></a>Preparare il Server SQL locale hello esercitazione
1. Nel database di hello specificata per hello on-premise SQL Server il servizio collegato (**SqlServerLinkedService**), utilizzare hello hello toocreate di script SQL seguente **emp** tabella nel database di hello.

    ```SQL   
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
        CONSTRAINT PK_emp PRIMARY KEY (ID)
    )
    GO
    ```
2. Inserire un punto qualsiasi nella tabella di hello:

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a>Creare set di dati di input

1. In hello **Editor delle Data Factory**, fare clic su **... Ulteriori**, fare clic su **nuovo set di dati** hello barra dei comandi e fare clic su **tabella di SQL Server**.
2. Sostituire hello JSON nel riquadro di destra hello con hello seguente testo:

    ```JSON   
    {        
        "name": "EmpOnPremSQLTable",
        "properties": {
            "type": "SqlServerTable",
            "linkedServiceName": "SqlServerLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }     
    ```     
   Si noti hello seguenti punti:

   * **tipo** è troppo**SqlServerTable**.
   * **tableName** è troppo**emp**.
   * **linkedServiceName** è troppo**SqlServerLinkedService** (è stato creato questo servizio collegato in precedenza in questa procedura dettagliata.).
   * Per un set di dati input che non viene generato da un'altra pipeline nella Data Factory di Azure, è necessario impostare **esterno** troppo**true**. Indica i dati di input hello sono prodotto toohello esterno, il servizio Data Factory di Azure. È possibile specificare i criteri di dati esterni tramite hello **externalData** elemento hello **criteri** sezione.    

   Per informazioni dettagliate sulle proprietà JSON, vedere [Spostare dati da/verso SQL Server](data-factory-sqlserver-connector.md).
3. Fare clic su **Distribuisci** sul comando hello barra toodeploy hello set di dati.  

### <a name="create-output-dataset"></a>Creare il set di dati di output

1. In hello **Editor delle Data Factory**, fare clic su **nuovo set di dati** hello barra dei comandi e fare clic su **archiviazione Blob di Azure**.
2. Sostituire hello JSON nel riquadro di destra hello con hello seguente testo:

    ```JSON   
    {
        "name": "OutputBlobTable",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "adftutorial/outfromonpremdf",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```   
   Si noti hello seguenti punti:

   * **tipo** è troppo**AzureBlob**.
   * **linkedServiceName** è troppo**AzureStorageLinkedService** (nel passaggio 2 è stato creato questo servizio collegato).
   * **folderPath** è troppo**adftutorial/outfromonpremdf** dove outfromonpremdf è la cartella hello nel contenitore adftutorial hello. Creare hello **adftutorial** contenitore se non esiste già.
   * Hello **disponibilità** è troppo**oraria** (**frequenza** impostare troppo**ora** e **intervallo** impostare troppo **1**).  servizio Data Factory Hello genera una sezione di dati di output ogni ora in hello **emp** tabella nel Database SQL di Azure hello.

   Se non si specifica un **fileName** per un **tabella di output**, i file generato hello in hello **folderPath** indicati nel seguente formato hello: dati.<Guid>. txt (ad esempio:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).

   tooset **folderPath** e **fileName** in modo dinamico in base a hello **SliceStart** tempo, utilizzare proprietà partitionedBy hello. Nell'esempio seguente di hello, folderPath Usa anno, mese e giorno da hello SliceStart (ora di inizio della sezione hello in fase di elaborazione) e nome file utilizza ora da hello SliceStart. Ad esempio, se viene viene prodotta una sezione per 2014-10-20T08:00:00, folderName hello è impostato toowikidatagateway/wikisampledataout/2014/10/20 e hello fileName è impostato too08.csv.

    ```JSON
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy":
    [

        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
    ],
    ```

    Per informazioni dettagliate sulle proprietà JSON, vedere [Spostare dati da/verso l'archivio BLOB di Azure](data-factory-azure-blob-connector.md).
3. Fare clic su **Distribuisci** sul comando hello barra toodeploy hello set di dati. Assicurarsi di visualizzare i set di dati sia hello nella visualizzazione ad albero di hello.  

## <a name="create-pipeline"></a>Creare una pipeline
In questo passaggio viene creata una **pipeline** con un'**attività di copia** che usa **EmpOnPremSQLTable** come input e **OutputBlobTable** come output.

1. Nell'editor di Data Factory fare clic su **... Altro** e quindi su **Nuova pipeline**.
2. Sostituire hello JSON nel riquadro di destra hello con hello seguente testo:    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL tooAzure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server tooblob",
             "type": "Copy",
             "inputs": [
               {
                 "name": "EmpOnPremSQLTable"
               }
             ],
             "outputs": [
               {
                 "name": "OutputBlobTable"
               }
             ],
             "typeProperties": {
               "source": {
                 "type": "SqlSource",
                 "sqlReaderQuery": "select * from emp"
               },
               "sink": {
                 "type": "BlobSink"
               }
             },
             "Policy": {
               "concurrency": 1,
               "executionPriorityOrder": "NewestFirst",
               "style": "StartOfInterval",
               "retry": 0,
               "timeout": "01:00:00"
             }
           }
         ],
         "start": "2016-07-05T00:00:00Z",
         "end": "2016-07-06T00:00:00Z",
         "isPaused": false
       }
     }
    ```   
   > [!IMPORTANT]
   > Sostituire il valore di hello di hello **avviare** proprietà con hello giorno corrente e **fine** valore con hello giorno successivo.
   >
   >

   Si noti hello seguenti punti:

   * Nella sezione attività hello è solo l'attività il cui **tipo** è troppo**copia**.
   * **Input** per attività hello è troppo**EmpOnPremSQLTable** e **output** per attività hello è troppo**OutputBlobTable**.
   * In hello **typeProperties** sezione **SqlSource** è specificato come hello **tipo di origine** e * * BlobSink * * è specificato come hello **tipodisink**.
   * Query SQL `select * from emp` specificato per hello **sqlReaderQuery** proprietà di **SqlSource**.

   Per la data e l'ora di inizio è necessario usare il [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). ad esempio 2014-10-14T16:32:41Z. Hello **fine** è facoltativo, ma viene usata in questa esercitazione.

   Se non specifica alcun valore per hello **fine** proprietà, viene calcolato come "**start + 48 ore**". specificare in modo indefinito, pipeline hello toorun **9/9/9999** come valore hello hello **fine** proprietà.

   Si sta definendo il periodo di tempo in cui hello vengono elaborate le sezioni di dati in base a hello hello **disponibilità** proprietà che sono state definite per ogni set di dati di Azure Data Factory.

   Nell'esempio hello, esistono 24 sezioni di dati come ogni sezione di dati viene prodotta ogni ora.        
3. Fare clic su **Distribuisci** sul comando hello barra toodeploy hello dataset (la tabella è un set di dati rettangolare). Confermare che pipeline hello viene visualizzato nella visualizzazione struttura ad albero di hello in **pipeline** nodo.  
4. A questo punto, fare clic su **X** due volte tooclose hello pagina tooget indietro toohello **Data Factory** pagina per hello **ADFTutorialOnPremDF**.

**Congratulazioni.** Creazione completata una data factory di Azure, servizi collegati, i set di dati e una pipeline e pipeline hello pianificato.

#### <a name="view-hello-data-factory-in-a-diagram-view"></a>Data factory di visualizzazione hello in una vista diagramma
1. In hello **portale di Azure**, fare clic su **diagramma** riquadro hello home page di hello **ADFTutorialOnPremDF** factory di dati. :

    ![Collegamento al diagramma](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. Dovrebbe essere simile toohello diagramma hello seguente immagine:

    ![Vista Diagramma](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    È possibile eseguire lo zoom avanti, eseguire lo zoom indietro, zoom too100%, toofit zoom, automaticamente le pipeline di posizione e i set di dati e visualizzare le informazioni di derivazione (evidenzia gli elementi a monte e a valle degli elementi selezionati).  È possibile fare doppio clic su una proprietà toosee dell'oggetto (set di dati di input/output o pipeline) per tale.

## <a name="monitor-pipeline"></a>Monitorare la pipeline
In questo passaggio, utilizzare hello Azure toomonitor portale cosa accade in un data factory di Azure. È anche possibile utilizzare le pipeline e set di dati toomonitor cmdlet PowerShell. Per altre informazioni sul monitoraggio, vedere [Monitorare e gestire le pipeline](data-factory-monitor-manage-pipelines.md).

1. Nel diagramma hello, fare doppio clic su **EmpOnPremSQLTable**.  

    ![Sezioni EmpOnPremSQLTable](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. Si noti che tutti i dati di hello seziona backup sono **pronto** stato perché la durata della pipeline hello (ora di inizio ora tooend) si trova in hello precedente. È inoltre perché è stato inserito dati hello nel database di SQL Server hello e è presente tutto il tempo hello. Verificare che non sono presenti sezioni visualizzati in hello **sezioni problema** sezione nella parte inferiore di hello. Fare clic su tutte le sezioni, hello tooview **vedere più** nella parte inferiore di hello dell'elenco di hello di sezioni.
3. A questo punto, In hello **set di dati** pagina, fare clic su **OutputBlobTable**.

    ![Sezioni OputputBlobTable](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. Fare clic su qualsiasi sezione di dati dall'elenco hello e dovrebbe essere hello **sezione dati** pagina. Viene visualizzato l'attività viene eseguita per sezione hello. In genere viene visualizzata una sola esecuzione di attività.  

    ![Pannello Sezione dati](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    Se la sezione hello non hello **pronto** stato, è possibile vedere le sezioni upstream hello che non sono pronti e bloccano l'intervallo corrente di hello l'esecuzione in hello **sezioni Upstream non pronte** elenco.
5. Fare clic su hello **esecuzione dell'attività** dall'elenco hello hello inferiore toosee **Dettagli esecuzione attività**.

   ![Pagina Dettagli esecuzione attività](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   Ad esempio la velocità effettiva, la durata e gateway hello utilizzati dati hello tootransfer, si vedrà informazioni.
6. Fare clic su **X** tooclose tutti hello pagine fino a
7. tornare home page di toohello per hello **ADFTutorialOnPremDF**.
8. (Facoltativo) Fare clic su **Pipeline** e su **ADFTutorialOnPremDF**, quindi eseguire il drill-through delle tabelle di input (**utilizzate**) o dei set di dati di output (**generati**).
9. Utilizzare strumenti come [Esplora archivi Microsoft](http://storageexplorer.com/) tooverify che viene creato un blob o file per ogni ora.

   ![Azure Storage Explorer](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a>Passaggi successivi
* Vedere [Gateway di gestione dati](data-factory-data-management-gateway.md) articolo per tutti i dettagli sul Gateway di gestione dati hello di hello.
* Vedere [copiare i dati da Blob di Azure tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn su come dati di toomove toouse attività di copia da un'origine archiviano tooa sink dati.
