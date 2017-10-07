---
title: aaaAzure Data Factory - esempi
description: Fornisce informazioni dettagliate sugli esempi forniti con hello servizio Azure Data Factory.
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c0538b90-2695-4c4c-a6c8-82f59111f4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: aa1c15eca21b34b7bcc64358b685d7606baaf691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---samples"></a>Azure Data Factory: esempi
## <a name="samples-on-github"></a>Esempi in GitHub
Hello [repository GitHub. Azure-DataFactory](https://github.com/azure/azure-datafactory) contiene diversi esempi che consentono rapidamente di salita con il servizio Data Factory di Azure (o) modificare script hello e usarlo nella propria applicazione. cartella Samples\JSON Hello contiene frammenti di codice JSON per scenari comuni.

| Esempio | Descrizione |
|:--- |:--- |
| [Procedura dettagliata di Azure Data Factory](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFWalkthrough) |In questo esempio fornisce una procedura dettagliata end-to-end per l'elaborazione di file di log con dati di Azure Data Factory tooturn dai file di log in tooinsights. <br/><br/>In questa procedura dettagliata, la pipeline di Data Factory hello raccoglie i log di esempio, i processi e arricchisce dati hello dai log con dati di riferimento e trasforma hello dati tooevaluate hello l'efficacia di una campagna di marketing che di recente è stata avviata. |
| [Esempi JSON](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON) |Questo esempio fornisce esempi JSON relativi a scenari comuni. |
| [Esempio relativo all'unità di download dei dati HTTP](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample) |Questo download presenta campione di dati da un tooAzure endpoint HTTP nell'archiviazione Blob utilizzando l'attività personalizzata di .NET. |
| [Esempio di attività .NET di passaggio tra AppDomain](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |In questo esempio è tooauthor un'attività personalizzata di .NET che non è vincolato versioni tooassembly usate dal hello ADF dell'utilità di avvio (ad esempio, la versione 4.3.0 Windowsazure, v6.0.x newtonsoft. JSON e così via). |
| [Esecuzione di script R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample) |In questo esempio include una Data Factory attività personalizzata hello che possono essere utilizzati tooinvoke RScript.exe. Questo esempio funziona soltanto con il cluster HDInsight dell'utente (non con quello su richiesta) in cui è già installato R. |
| [Richiamare processi Spark in cluster Hadoop di HDInsight](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/Spark) |Questo esempio viene illustrato come toouse MapReduce attività tooinvoke un programma di Spark. Hello spark appena copiato dati da un Blob di Azure contenitore tooanother. |
| [Analisi Twitter mediante un'attività batch di Azure Machine Learning per l'assegnazione dei punteggi](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-AzureMLBatchScoringActivity) |Questo esempio viene illustrato come toouse AzureMLBatchScoringActivity tooinvoke un Azure Machine Learning modello che esegue l'analisi del sentiment twitter, assegnazione dei punteggi, stima e così via. |
| [Analisi Twitter mediante un'attività personalizzata](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |Questo esempio viene illustrato come un tooinvoke di attività personalizzate .NET che esegue un modello di Azure Machine Learning toouse twitter analisi del sentiment, assegnazione dei punteggi, stima e così via. |
| [Pipeline con parametri per Azure Machine Learning](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ParameterizedPipelinesForAzureML/) |esempio Hello fornisce un end-to-end c# codice toodeploy N pipeline per l'assegnazione di punteggi e ripetizione di training ognuno con un parametro di area geografica diversa in elenco hello delle aree proviene da un file parameters.txt, incluso in questo esempio. |
| [Aggiornamento dei dati di riferimento per i processi di Analisi di flusso di Azure](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs) |Questo esempio viene illustrato come l'aggiornamento dei dati di riferimento in una pianificazione toouse Data Factory di Azure e Azure flusso Analitica toorun insieme hello query con hello setup e i dati di riferimento. |
| [Pipeline ibrida con Hortonworks Hadoop locale](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HybridPipelineWithOnPremisesHortonworksHadoop) |esempio Hello utilizza un cluster Hadoop locale come destinazione del calcolo per eseguire i processi in Data Factory, come ad esempio un HDInsight in base a un cluster Hadoop nel cloud, è necessario aggiungere altre destinazioni di calcolo. |
| [Strumento di conversione JSON](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSONConversionTool) |Questo strumento consente tooconvert documenti JSON dalla versione precedente too2015-07-01-preview toolatest o 2015-07-01-preview (impostazione predefinita). |
| [File di input di esempio U-SQL](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/U-SQL%20Sample%20Input%20File) |Si tratta di un file di esempio usato da un'attività di U-SQL. |
| [Eliminare il file BLOB](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity) | Questo esempio illustra un file c# che può essere utilizzato come parte del file ADF .net attività toodelete file personalizzati dall'origine hello posizione del Blob di Azure dopo avere copiati i file hello.|

## <a name="azure-resource-manager-templates"></a>Modelli di Gestione risorse di Azure
È possibile trovare hello seguenti modelli di gestione risorse di Azure Data factory in GitHub.

| Modello | Descrizione |
| --- | --- |
| [Copiare da tooAzure di archiviazione Blob di Azure SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy) |Questo modello di distribuzione crea un data factory di Azure con una pipeline che copia i dati da hello specificato database SQL di Azure toohello di archiviazione blob di Azure |
| [Copiare da Salesforce tooAzure nell'archiviazione Blob](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy) |Questo modello di distribuzione crea un data factory di Azure con una pipeline che copia i dati da hello specificato nell'archiviazione blob Azure toohello account Salesforce. |
| [Trasformare i dati eseguendo lo script Hive in un cluster HDInsight di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation) |La distribuzione di questo modello crea una data factory di Azure con una pipeline che trasforma i dati tramite l'esecuzione di script Hive di esempio hello in un cluster Azure HDInsight Hadoop. |

## <a name="samples-in-azure-portal"></a>Esempi nel portale di Azure
È possibile utilizzare hello **pipeline di esempio** riquadro nella data factory di tooyour hello home page delle pipeline di esempio toodeploy factory dati e le entità associate (set di dati e i servizi collegati).

1. Creare una data factory o aprire una data factory esistente. Vedere [copiare i dati da archiviazione Blob tooSQL Database tramite Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per passaggi toocreate una data factory.
2. In hello **DATA FACTORY** pannello per data factory di hello, fare clic su hello **pipeline di esempio** riquadro.

    ![Riquadro Pipeline di esempio](./media/data-factory-samples/SamplePipelinesTile.png)
3. In hello **pipeline di esempio** pannello, fare clic su hello **esempio** che si desidera toodeploy.

    ![Pannello Pipeline di esempio](./media/data-factory-samples/SampleTile.png)
4. Specificare le impostazioni di configurazione per l'esempio hello. ad esempio il nome dell'account di archiviazione di Azure e la chiave dell'account, il nome del server di Azure SQL, il database, l'ID utente, la password e così via.

    ![Pannello Esempio](./media/data-factory-samples/SampleBlade.png)
5. Dopo avere completato con impostazioni di configurazione hello, fare clic su **crea** toocreate/distribuire hello pipeline di esempio e servizi/tabelle collegate utilizzate dalle pipeline hello.
6. Viene visualizzato lo stato di hello di distribuzione nel riquadro di esempio hello selezionato in precedenza hello **pipeline di esempio** blade.

    ![Stato della distribuzione](./media/data-factory-samples/DeploymentStatus.png)
7. Quando viene visualizzato hello **distribuzione ha avuto esito positivo** messaggio nel riquadro hello per esempio hello, chiude hello **pipeline di esempio** blade.  
8. In **DATA FACTORY** pannello vedere che i servizi collegati, set di dati e pipeline vengono aggiunti tooyour data factory di.  

    ![Pannello Data factory](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="samples-in-visual-studio"></a>Esempi in Visual Studio
### <a name="prerequisites"></a>Prerequisiti
È necessario disporre delle seguenti hello installato nel computer:

* Visual Studio 2013 o Visual Studio 2015
* Download di Azure SDK per Visual Studio 2013 o Visual Studio 2015. Passare troppo[pagina di Download di Azure](https://azure.microsoft.com/downloads/) e fare clic su **VS 2013** o **Visual Studio 2015** in hello **.NET** sezione.
* Scaricare hello plug-in Data Factory di Azure più recenti per Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) o [Visual Studio 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). Se si utilizza Visual Studio 2013, è inoltre possibile aggiornare i plug-in hello effettuando hello alla procedura seguente: hello scegliere **strumenti** -> **estensioni e aggiornamenti**  ->  **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools per Visual Studio**  ->  **Aggiornamento**.

### <a name="use-data-factory-templates"></a>Usare Modelli di Data Factory
1. Fare clic su **File** hello, scegliere dal menu troppo**New**, fare clic su **progetto**.
2. In hello **nuovo progetto** finestra di dialogo casella, hello i passaggi seguenti:

   1. Selezionare **DataFactory** in **Modelli**.
   2. Selezionare **modelli di Data Factory** nel riquadro di destra hello.
   3. Immettere un **nome** per progetto hello.
   4. Selezionare un **percorso** per progetto hello.
   5. Fare clic su **OK**.

      ![Finestra di dialogo Nuovo progetto](./media/data-factory-samples/vs-new-project-adf-templates.png)
3. In hello **modelli di Data Factory** la finestra di dialogo, il modello di esempio hello selezionare da hello **in caso di utilizzo modelli** sezione e fare clic su **Avanti**. Hello passaggi seguenti consentono di eseguire utilizzando hello **cliente profilatura** modello. Passaggi sono simili per altri esempi di hello.

    ![Finestra di dialogo Modelli di Data Factory](./media/data-factory-samples/vs-data-factory-templates-dialog.png)
4. In hello **Data Factory configurazione** finestra di dialogo, fare clic su **Avanti** su hello **nozioni fondamentali sulla Factory dati** pagina.
5. In hello **Configura data factory di** pagina, hello i passaggi seguenti:
   1. Selezionare **Create new data factory** (Crea nuova data factory). In alternativa, selezionare **Use existing data factory**(Usa data factory esistente).
   2. Immettere un **nome** per data factory di hello.
   3. Seleziona hello **sottoscrizione di Azure** in cui si desidera hello data factory toobe creato.
   4. Seleziona hello **gruppo di risorse** per data factory di hello.
   5. Seleziona hello **Stati Uniti occidentali**, **Stati Uniti orientali**, o **Europa settentrionale** per hello **area**.
   6. Fare clic su **Avanti**.
6. In hello **configurare archivi dati** , specificare un oggetto esistente **database SQL di Azure** e **account di archiviazione Azure** creare database o dell'archiviazione (o) e fare clic su Avanti.
7. In hello **configurare calcolo** pagina, selezionare le impostazioni predefinite e fare clic su **Avanti**.
8. In hello **riepilogo** pagina, esaminare tutte le impostazioni e fare clic su **Avanti**.
9. In hello **lo stato di distribuzione** pagina, attendere fino al completamento distribuzione hello e fare clic su **fine**.
10. Fare clic sul progetto in Esplora soluzioni hello e fare clic su **pubblica**.
11. Se viene visualizzato **Accedi tooyour account Microsoft** nella finestra di dialogo immettere le credenziali di account hello con sottoscrizione di Azure e fare clic su **Accedi**.
12. È necessario visualizzare hello la finestra di dialogo seguenti:

    ![Finestra di dialogo Pubblica](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
13. In hello **Configura data factory di** pagina, hello i passaggi seguenti:

    1. Confermare l'opzione **Use existing data factory** (Usa data factory esistente).
    2. Seleziona hello **data factory di** era selezionare quando si utilizza il modello di hello.
    3. Fare clic su **Avanti** tooswitch toohello **pubblicare elementi** pagina. (Premere **scheda** toomove fuori hello di hello Nome campo tooif **Avanti** pulsante è disabilitato.)
14. In hello **pubblicare elementi** pagina, assicurarsi che tutti hello Data factory di entità vengono selezionate e fare clic su **Avanti** tooswitch toohello **riepilogo** pagina.     
15. Esaminare hello riepilogo e fare clic su **Avanti** toostart hello distribuzione elaborare e visualizzare hello **lo stato di distribuzione**.
16. In hello **lo stato di distribuzione** pagina, dovrebbe essere stato hello hello processo di distribuzione. Dopo la distribuzione hello viene eseguita, fare clic su Fine.

Vedere [compilare la prima data factory (Visual Studio)](data-factory-build-your-first-pipeline-using-vs.md) per informazioni dettagliate sull'utilizzo di entità di Visual Studio tooauthor Data Factory e pubblicarli tooAzure.          
