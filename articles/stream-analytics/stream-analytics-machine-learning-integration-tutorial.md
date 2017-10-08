---
title: integrazione di flusso Analitica e Machine Learning aaaAzure | Documenti Microsoft
description: Come toouse una funzione definita dall'utente e Machine Learning in un processo di flusso Analitica
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: cfced01f-ccaa-4bc6-81e2-c03d1470a7a2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/06/2017
ms.author: jeffstok
ms.openlocfilehash: e1ba7ab51ece80719839793e1320a7666cfc4181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a>Analisi del sentiment con Analisi di flusso di Azure e Azure Machine Learning
In questo articolo viene descritto come tooquickly impostare un semplice processo Analitica di flusso di Azure che si integra Azure Machine Learning. Utilizzare un modello di analitica sentiment di Machine Learning da dati di testo Cortana Intelligence Gallery tooanalyze streaming hello e determinare il punteggio sentiment hello in tempo reale. Utilizzo di hello Cortana Intelligence Suite consente di eseguire questa operazione senza preoccuparsi delle complessità hello di compilazione di un modello di valutazione analitica.

È possibile applicare le operazioni da tooscenarios questo articolo come i seguenti:

* Analisi in tempo reale del sentiment su flussi di dati di Twitter.
* Analisi dei record delle chat dei client con il personale di supporto.
* Valutazione dei commenti per forum, blog e video. 
* Molti altri scenari di punteggio predittivo in tempo reale.

In uno scenario reale, si otterrebbe dati hello direttamente da un flusso di dati di Twitter. esercitazione di hello toosimplify, abbiamo scritto, in modo che hello il processo di Streaming Analitica Ottiene TWEET da un file CSV in archiviazione Blob di Azure. È possibile creare un file CSV oppure è possibile utilizzare un file CSV di esempio, come illustrato nella seguente immagine hello:

![tweet di esempio in un file CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

processo di Streaming Analitica Hello che si crea l'applicazione hello sentiment analitica modello come una funzione definita dall'utente (UDF) sui dati di testo di esempio hello dall'archivio blob hello. output di Hello (risultato hello di analisi del sentiment hello) viene scritto toohello stesso archivio di blob in un file CSV diverso. 

Hello nella figura seguente viene illustrata questa configurazione. Come indicato, per uno scenario più realistico è possibile sostituire l'archivio BLOB con il flusso di dati di Twitter provenienti da un input di Hub eventi di Azure. Inoltre, è possibile creare un [Microsoft Power BI](https://powerbi.microsoft.com/) visualizzazione in tempo reale di valutazione di aggregazione hello.    

![Panoramica dell'integrazione di Machine Learning in Analisi di flusso](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare, verificare di che aver seguito hello:

* Una sottoscrizione di Azure attiva.
* Un file CSV contenente alcuni dati. È possibile scaricare file hello illustrato in precedenza da [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), oppure è possibile creare un file. Questo articolo si presuppone che si usi file hello da GitHub.

In generale, attività di hello toocomplete illustrate in questo articolo hello seguenti:

1. Creare un account di archiviazione di Azure e un contenitore di archiviazione blob e caricare un contenitore di toohello file di input in formato CSV.
3. Aggiungere un modello di valutazione analitica dall'area di lavoro in Azure Machine Learning tooyour Cortana Intelligence Gallery hello e distribuire questo modello come un servizio web nell'area di lavoro Machine Learning hello.
5. Creare un processo di flusso Analitica che chiama il servizio web come funzione valutazione toodetermine ordine hello input di testo.
6. Avviare il processo di flusso Analitica hello e controllare l'output di hello.

## <a name="create-a-storage-container-and-upload-hello-csv-input-file"></a>Creare un contenitore di archiviazione e caricare il file di input CSV hello
Per questo passaggio, è possibile utilizzare qualsiasi file CSV, ad esempio hello uno disponibili da GitHub.

1. Nel portale di Azure hello, fare clic su **New** &gt; **archiviazione** &gt; **account di archiviazione**.

   ![creare un nuovo account di archiviazione](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. Specificare un nome (`samldemo` nell'esempio hello). nome Hello può utilizzare solo lettere minuscole e numeri e deve essere univoco in Azure. 

3. Specificare un gruppo di risorse esistente e specificare un percorso. Per il percorso, è consigliabile che tutte le risorse di hello create in questa esercitazione usare hello stesso percorso.

    ![specificare i dettagli dell'account di archiviazione](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. Nel portale di Azure hello, selezionare account di archiviazione hello. Nel Pannello di account di archiviazione hello, fare clic su **contenitori** e quindi fare clic su  **+ &nbsp;contenitore** toocreate nell'archiviazione blob.

    ![Creare un contenitore BLOB](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. Specificare un nome per il contenitore di hello (`azuresamldemoblob` nell'esempio hello) e verificare che **tipo di accesso** è troppo**Blob**. Al termine, fare clic su **OK**.

    ![specificare i dettagli del contenitore BLOB](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. In hello **contenitori** blade, hello selezionare nuovo contenitore, che apre il pannello hello per tale contenitore.

7. Fare clic su **Carica**.

    ![Pulsante 'Carica' per un contenitore](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. In hello **caricamento blob** pannello, specificare i file CSV hello che si desidera toouse per questa esercitazione. Per **Blob tipo**selezionare **blob in blocchi** e blocco hello set dimensioni too4 MB, che è sufficiente per questa esercitazione.

    ![caricare il file BLOB](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. Fare clic su hello **caricare** pulsante nella parte inferiore di hello del pannello hello.

## <a name="add-hello-sentiment-analytics-model-from-hello-cortana-intelligence-gallery"></a>Aggiungere modello di hello valutazione analitica da hello Cortana Intelligence Gallery

Ora che i dati di esempio hello sono in un blob, è possibile abilitare modello di analisi del sentiment hello in Cortana Intelligence Gallery.

1. Passare toohello [modello analitica predittiva sentiment](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) pagina hello Cortana Intelligence Gallery.  

2. Fare clic su **Open in Studio** (Apri in Studio).  
   
   ![Analisi di flusso e Machine Learning, aprire Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. Accedi toogo toohello area di lavoro. Selezionare una località.

4. Fare clic su **eseguire** nella parte inferiore di hello della pagina hello. esecuzione del processo di Hello, che richiede circa un minuto.

   ![eseguire l'esperimento in Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. Dopo il processo di hello è stata eseguita correttamente, selezionare **distribuzione servizio Web** nella parte inferiore di hello della pagina hello.

   ![distribuire l'esperimento in Machine Learning Studio come servizio Web](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. toovalidate che hello sentiment modello analitica è toouse pronti, fare clic su hello **Test** pulsante. Immettere testo, ad esempio "Mi piace Microsoft". 

   ![testare l'esperimento in Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    Se il test di hello funziona, viene visualizzato un toohello simile risultato esempio seguente:

   ![risultati del test in Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. In hello **app** colonna, fare clic su hello **Excel 2010 o cartella di lavoro precedenti** toodownload collegamento una cartella di lavoro di Excel. cartella di lavoro Hello contiene un'API hello chiave e l'URL di hello che è necessario tooset successive il processo di flusso Analitica hello.

    ![Analisi di flusso e Machine Learning, panoramica rapida](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-hello-machine-learning-model"></a>Creare un processo di flusso Analitica che utilizza il modello di Machine Learning hello

È ora possibile creare un processo di flusso Analitica che legge hello esempio TWEET da file CSV hello nell'archiviazione blob. 

### <a name="create-hello-job"></a>Creazione del processo di hello

1. Passare toohello [portale di Azure](https://portal.azure.com).  

2. Fare clic su **Nuovo** > **Internet delle cose** > **Processo di Analisi di flusso**. 

   ![Percorso del portale Azure per ottenere il nuovo processo di flusso Analitica tooa](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. Nome del processo hello `azure-sa-ml-demo`, specificare una sottoscrizione, specificare un gruppo di risorse esistente o crearne uno nuovo e selezionare il percorso di hello per processo hello.

   ![specificare le impostazioni per il nuovo processo di Analisi di flusso](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-hello-job-input"></a>Configurazione input processo hello
processo Hello Ottiene l'input da file CSV hello caricato archiviazione tooblob precedenti.

1. Dopo il processo di hello è stato creato in **processo topologia** nel Pannello di hello processo, fare clic su hello **input** casella.  
   
   ![Casella 'Input' nel pannello del processo di Analisi di flusso](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. In hello **input** pannello, fare clic su **+ Aggiungi**.

   ![Pulsante per l'aggiunta di un processo di flusso Analitica input toohello 'add'](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. Compilare hello **nuovo input** pannello con questi valori:

    * **Alias di input**: utilizza il nome di hello `datainput`.
    * **Tipo di origine**: selezionare **Flusso dati**.
    * **Origine**: selezionare **Archiviazione BLOB**.
    * **Opzioni di importazione**: selezionare **Usa l'archiviazione BLOB della sottoscrizione corrente**. 
    * **Account di archiviazione**. Selezionare l'account di archiviazione hello creato in precedenza.
    * **Contenitore**. Contenitore hello selezionare creato in precedenza (`azuresamldemoblob`).
    * **Formato di serializzazione eventi**. Selezionare **CSV**.

    ![Impostazioni per il nuovo input del processo](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. Fare clic su **Crea**.

### <a name="configure-hello-job-output"></a>Configurare l'output del processo hello
Hello processo Invia risultati toohello stesso blob di archiviazione in cui si ottiene input. 

1. In **processo topologia** nel Pannello di hello processo, fare clic su hello **output** casella.  
  
   ![Creare un nuovo output per il processo di Analisi di flusso](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. In hello **output** pannello, fare clic su **+ Aggiungi**, quindi aggiungere un output con alias hello `datamloutput`. 

3. In **Sink** selezionare **Archivio BLOB**. Compilare il resto di hello di hello output impostazioni mediante hello stessi valori utilizzati per l'archiviazione blob hello input:

    * **Account di archiviazione**. Selezionare l'account di archiviazione hello creato in precedenza.
    * **Contenitore**. Contenitore hello selezionare creato in precedenza (`azuresamldemoblob`).
    * **Formato di serializzazione eventi**. Selezionare **CSV**.

   ![Impostazioni per il nuovo output del processo](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. Fare clic su **Crea**.   


### <a name="add-hello-machine-learning-function"></a>Aggiungere una funzione di Machine Learning hello 
In precedenza è stato pubblicato un servizio web tooa del modello di Machine Learning. In questo scenario, quando si esegue il processo di analisi di flusso hello, invia tweet ogni esempio dal servizio web di input toohello hello per l'analisi di valutazione. servizio web Machine Learning Hello restituisce un sentiment (`positive`, `neutral`, o `negative`) e la probabilità di tweet hello viene positivo. 

In questa sezione dell'esercitazione hello, si definisce una funzione nel processo di analisi di flusso hello. funzione Hello può essere richiamato toosend un servizio web di toohello tweet e tornare risposta hello. 

1. Assicurarsi di disporre di hello web service URL e la chiave API che è stato scaricato in precedenza nella cartella di lavoro di Excel hello.

2. Pannello della panoramica processo toohello restituito.

3. In **Impostazioni** selezionare **Funzioni** e quindi fare clic su **+ Aggiungi**.

   ![Aggiungere un processo di flusso Analitica toohello (funzione)](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. Immettere `sentiment` come hello funzione alias e compilare il resto di hello del pannello hello utilizzando questi valori:

    * **Tipo funzione**: selezionare **Azure ML**.
    * **Opzione di importazione**: selezionare **Importa da un'altra sottoscrizione**. In questo modo, è un URL di probabilità tooenter hello e una chiave.
    * **URL**: Incolla in hello URL del servizio web.
    * **Chiave**: Incolla nella chiave hello API.
  
    ![Impostazioni per l'aggiunta di un processo di flusso Analitica Machine Learning toohello (funzione)](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. Fare clic su **Crea**.

### <a name="create-a-query-tootransform-hello-data"></a>Creare un query tootransform hello dati

Flusso Analitica utilizza un input di query dichiarativo basato su SQL tooexamine hello ed elaborarlo. In questa sezione creare una query che legge ogni tweet dall'input e quindi richiama l'analisi del sentiment tooperform funzione hello Machine Learning. query Hello quindi invia l'output di hello risultato toohello che sia definita (archiviazione blob).

1. Pannello della panoramica processo toohello restituito.

2.  In **processo topologia**, fare clic su hello **Query** casella.

    ![Creare una query per il processo di Analisi di flusso](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. Immettere hello seguente query:

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    query Hello richiama la funzione di hello creato in precedenza (`sentiment`) nell'analisi del sentiment tooperform ordine su ogni tweet hello input. 

4. Fare clic su **salvare** query hello toosave.


## <a name="start-hello-stream-analytics-job-and-check-hello-output"></a>Avviare il processo di flusso Analitica hello e controllare l'output di hello

È ora possibile avviare il processo di flusso Analitica hello.

### <a name="start-hello-job"></a>Avviare il processo di hello
1. Pannello della panoramica processo toohello restituito.

2. Fare clic su **avviare** nella parte superiore di hello del pannello hello.

    ![Creare una query per il processo di Analisi di flusso](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. In hello **inizio processo**selezionare **personalizzato**, quindi selezionare toowhen precedente di un giorno caricato archiviazione tooblob file CSV di hello. Al termine, fare clic su **Avvia**.  


### <a name="check-hello-output"></a>Controllare l'output di hello
1. Il processo di hello let eseguito per qualche minuto finché non viene visualizzata l'attività in hello **monitoraggio** casella. 

2. Se si dispone di uno strumento utilizzato normalmente contenuto hello tooexamine dell'archiviazione blob, utilizzare tale hello tooexamine strumento `azuresamldemoblob` contenitore. In alternativa, hello in hello portale di Azure come segue:

    1. Nel portale di hello trovare hello `samldemo` storage account e all'interno di account hello, trovare hello `azuresamldemoblob` contenitore. Viene visualizzato due file nel contenitore hello: hello file che contiene hello esempio TWEET e un file CSV generato dal processo di flusso Analitica hello.
    2. Fare clic sul file hello generato e quindi selezionare **scaricare**. 

   ![Scaricare l'output del processo CSV dall'archivio BLOB](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. Aprire hello ha generato il file CSV. Viene visualizzato un output simile al seguente esempio hello:  
   
   ![Analisi di flusso e Machine Learning, visualizzazione CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a>Visualizzare le metriche
È possibile osservare anche le metriche correlate alla funzione Azure Machine Learning. Hello seguendo le metriche correlate alla funzione viene visualizzato in hello **monitoraggio** casella nel pannello processo hello:

* **Funzione richieste** indica il numero di hello di richieste inviate tooa servizio web Machine Learning.  
* **Funzione eventi** indica il numero di hello di eventi nella richiesta di hello. Per impostazione predefinita, ogni tooa richiesta servizio web Machine Learning contiene backup too1, eventi 000.  


## <a name="next-steps"></a>Passaggi successivi

* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Integrare API REST e Machine Learning](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)



