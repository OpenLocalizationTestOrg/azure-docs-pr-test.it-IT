---
title: aaaRetrain Machine Learning i modelli a livello di codice | Documenti Microsoft
description: Informazioni su come tooprogrammatically ripetere il training di un modello e aggiornamento hello web servizio toouse hello appena modello con Training in Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: 7ae4f977-e6bf-4d04-9dde-28a66ce7b664
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raymondl;garye;v-donglo
ms.openlocfilehash: edbb64c08f7d9edf3c76e23e0cc7e14c0125d697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a>Ripetere il training dei modelli di Machine Learning a livello di codice
In questa procedura dettagliata si apprenderà come tooprogrammatically ripetere il training di un servizio Web di Azure Machine Learning con c# e hello servizio esecuzione Batch di Machine Learning.

Dopo avere ripetere il training del modello di hello, hello procedure dettagliate seguenti Mostra come tooupdate hello modello del servizio web predittivo:

* Se è stato distribuito un servizio web classica nel portale di servizi Web di Machine Learning hello, vedere [ripetere il training di un servizio web classica](machine-learning-retrain-a-classic-web-service.md). 
* Se è stato distribuito un nuovo servizio web, vedere [ripetere il training di un nuovo servizio web usando i cmdlet di Machine Learning Management hello](machine-learning-retrain-new-web-service-using-powershell.md).

Per una panoramica del processo di ripetizione di training hello, vedere [ripetere il training di un modello di Machine Learning](machine-learning-retrain-machine-learning-model.md).

Se si desidera toostart esistenti nuovo gestore di risorse di Azure basato su servizio web, vedere [ripetere il training di un servizio web predittivo esistente](machine-learning-retrain-existing-resource-manager-based-web-service.md).

## <a name="create-a-training-experiment"></a>Creare un esperimento di training
Per questo esempio, si utilizzerà "esempio 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" dagli esempi di Microsoft Azure Machine Learning hello. 

sperimentazione hello toocreate:

1. Accedere a tooMicrosoft Azure Machine Learning Studio. 
2. Scegliere hello nell'angolo inferiore destro del dashboard hello, **New**.
3. Hello Microsoft Samples, selezionare 5 di esempio.
4. esperimento hello toorename, nella parte superiore di hello dell'area di disegno di hello esperimento, selezionare il nome di sperimentazione hello "esempio 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".
5. Digitare Census Model.
6. Nella parte inferiore di hello dell'area di disegno esperimento hello, fare clic su **eseguire**.
7. Fare clic su **Set Up Web service** (Configura servizio Web) e selezionare **Retraining Web service** (Servizio Web di ripetizione del training). 

Hello il seguente esperimento iniziale hello.
   
   ![Esperimento iniziale.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a>Creare un esperimento predittivo e pubblicarlo come servizio Web
Ora viene creato un esperimento predicativo.

1. Nella parte inferiore di hello dell'area di disegno esperimento hello, fare clic su **di servizio Web** e selezionare **servizio Web predittivo**. Questo modello hello viene salvata come un modello con training e aggiunge i moduli di Input e Output del servizio web. 
2. Fare clic su **Run**. 
3. Al termine dell'esecuzione esperimento hello, fare clic su **distribuzione di un servizio Web [classica]** o **distribuzione servizio Web [New]**.

> [!NOTE] 
> un nuovo servizio web deve disporre di autorizzazioni sufficienti in hello toowhich di sottoscrizione per la distribuzione del servizio web hello toodeploy. Per ulteriori informazioni, vedere [gestire un servizio Web tramite il portale di servizi Web di Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

## <a name="deploy-hello-training-experiment-as-a-training-web-service"></a>Distribuire hello esperimento di training come un servizio web di Training
modello con training hello tooretrain, è necessario distribuire l'esperimento di training hello che è stato creato come un servizio web Retraining. Questo servizio web è necessario un *Output del servizio Web* modulo connesso toohello  *[Train Model] [ train-model]*  module, toobe tooproduce in grado di nuovo modelli di training.

1. esperimento di training toohello tooreturn, fare clic sull'icona esperimenti hello nel riquadro di sinistra hello, quindi fare clic su esperimento hello denominato modello di censimento.  
2. Nella casella di ricerca di hello elementi esperimento di ricerca, digitare il servizio web. 
3. Trascinare un *Input del servizio Web* modulo sul hello provare l'area di disegno e connettersi toohello il relativo output *Clean Missing Data* modulo.  In questo modo si garantisce che i dati viene elaborati hello stesso come dati di training originale.
4. Trascinare due *servizio Output web* moduli su hello provare l'area di disegno. Connettere l'output di hello di hello *Train Model* output tooone e hello del modulo di hello *Evaluate Model* toohello altro modulo. output del servizio web per Hello **Train Model** offre un nuovo modello con training di hello. Hello output collegato troppo**Evaluate Model** restituisce tale modulo dell'output, ovvero i risultati delle prestazioni hello.
5. Fare clic su **Run**. 

Successivamente è necessario distribuire hello esperimento di training come servizio web che produce un modello con training e risultati della valutazione del modello. tooaccomplish questa operazione, il set successivo di azioni dipendono se si lavora con un servizio web classica o di un nuovo servizio web.  

**Servizio Web classico**

Nella parte inferiore di hello dell'area di disegno esperimento hello, fare clic su **di servizio Web** e selezionare **distribuzione di un servizio Web [classica]**. Servizio Web Hello **Dashboard** viene visualizzato con una pagina della Guida hello chiave API e hello API per l'esecuzione Batch. È utilizzabile solo hello metodo di esecuzione Batch per la creazione di modelli di training.

**Nuovo servizio Web**

Nella parte inferiore di hello dell'area di disegno esperimento hello, fare clic su **di servizio Web** e selezionare **distribuzione servizio Web [New]**. portale Web del servizio servizi Web di Azure Machine Learning Hello verrà visualizzata la pagina del servizio web di distribuire toohello. Digitare un nome per il servizio Web e scegliere un piano di pagamento, quindi fare clic su **Distribuisci**. Solo hello metodo di esecuzione di Batch può essere utilizzato per la creazione di modelli con training

In entrambi i casi, dopo l'esperimento ha completata esecuzione, flusso di lavoro hello risultante dovrebbe apparire come segue:

![Flusso di lavoro risultante dopo l'esecuzione.][4]



## <a name="retrain-hello-model-with-new-data-using-bes"></a>Ripetere il training del modello di hello con nuovi dati usando BES
Per questo esempio, si utilizza c# toocreate hello formazione dell'applicazione. È possibile inoltre utilizzare hello Python o R esempio codice tooaccomplish questa attività.

toocall hello API ripetizione di training:

1. Creare un'applicazione console C# in Visual Studio. A tale scopo, selezionare **Nuovo** > **Progetto** > **Visual C#** > **Desktop classico di Windows** > **Applicazione console (.NET Framework)**.
2. Accedi toohello portale servizio Web di Machine Learning.
3. Se si usa un servizio Web classico, fare clic su **Classic Web Services**(Servizi Web classici).
   1. Fare clic su servizio web hello in uso.
   2. Fare clic su endpoint predefinito hello.
   3. Fare clic su **Consume**(Uso).
   4. Nella parte inferiore di hello di hello **consumare** pagina hello **codice di esempio** fare clic su **Batch**.
   5. Continuare toostep 5 di questa procedura.
4. Se si usa un nuovo servizio Web, fare clic su **Servizi Web**.
   1. Fare clic su servizio web hello in uso.
   2. Fare clic su **Consume**(Uso).
   3. Nella parte inferiore di hello di hello consumare nella pagina hello **codice di esempio** fare clic su **Batch**.
5. Copiare hello c# codice di esempio per l'esecuzione batch e incollarlo nel file Program.cs hello, assicurandosi che lo spazio dei nomi hello rimane invariata.

Aggiungere il pacchetto Nuget hello webapi come specificato nei commenti hello. tooadd hello riferimento tooMicrosoft.WindowsAzure.Storage.dll, si potrebbe essere necessario innanzitutto libreria client di hello tooinstall per servizi di archiviazione di Microsoft Azure. Per altre informazioni, vedere i [servizi di archiviazione Windows](https://www.nuget.org/packages/WindowsAzure.Storage).

### <a name="update-hello-apikey-declaration"></a>Aggiornare hello apikey dichiarazione
Individuare hello **apikey** dichiarazione.

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

In hello **informazioni di base al consumo** sezione di hello **consumare** individuare la chiave primaria di hello e copiarlo toohello **apikey** dichiarazione.

### <a name="update-hello-azure-storage-information"></a>Aggiornare le informazioni di archiviazione di Azure hello
codice di esempio BES Hello carica un file da un tooAzure unità locale (ad esempio "C:\temp\CensusIpnput.csv"), archiviazione, elabora e scrive hello risultati indietro tooAzure archiviazione.  

tooaccomplish questa attività, è necessario recuperare hello archiviazione nome, chiave e contenitore informazioni sull'account per l'account di archiviazione dal portale di Azure classico hello e aggiornamento hello corrispondenti valori nel codice hello. 

1. Accedi a portale di Azure classico toohello.
2. Nella colonna sinistra hello, fare clic su **archiviazione**.
3. Dall'elenco di hello di account di archiviazione, selezionare uno toostore hello ripetere il training del modello.
4. Nella parte inferiore di hello della pagina hello, fare clic su **Gestisci chiavi di accesso**.
5. Copiare e salvare hello **chiave di accesso primaria** e hello Chiudi finestra di dialogo. 
6. Nella parte superiore di hello della pagina hello, fare clic su **contenitori**.
7. Selezionare un contenitore esistente o crearne uno nuovo e salvare il nome di hello.

Individuare hello *StorageAccountName*, *StorageAccountKey*, e *StorageContainerName* dichiarazioni e aggiornare i valori di hello è stato salvato da hello portale di Azure.

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

È anche necessario verificare il file di input hello è disponibile nel percorso di hello specificate nel codice hello. 

### <a name="specify-hello-output-location"></a>Specificare il percorso di output di hello
Quando si specifica il percorso di output di hello in hello del payload della richiesta, hello estensione del file hello specificato *RelativeLocation* deve essere specificato come ilearner. 

Vedere hello di esempio seguente:

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you would like toouse for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> nomi di Hello di percorsi di output possono essere diversi da quelle in questa procedura dettagliata sulla base di hello ordine in cui è stato aggiunto moduli di output di hello web servizio hello. Dopo aver impostato questo esperimento di training con due output, risultati di hello includono informazioni sul percorso di archiviazione per entrambi gli elementi.  
> 
> 

![Output della ripetizione del training.][6]

Diagramma 4: output della ripetizione del training.

## <a name="evaluate-hello-retraining-results"></a>Valutare i risultati di ripetizione di training hello
Quando si esegue un'applicazione hello, output di hello include l'URL di hello e tooaccess necessari token SAS hello risultati della valutazione.

È possibile visualizzare i risultati delle prestazioni hello di hello Training modello combinando hello *BaseLocation*, *RelativeLocation*, e *SasBlobToken* dai risultati di output di hello per *USCITA2* (come mostrato nella precedente ripetizione di training immagine di output di hello) e incollare l'URL completo di hello nella barra degli indirizzi del browser hello.  

Esamina hello risultati toodetermine modello sottoposto a training appena hello esegue anche sufficiente hello tooreplace uno esistente.

Hello copia *BaseLocation*, *RelativeLocation*, e *SasBlobToken* dai risultati di output di hello, che verranno utilizzati durante il processo di ripetizione di training hello.

## <a name="next-steps"></a>Passaggi successivi
Se è stata distribuita, fare clic su servizio web predittivo hello **distribuzione di un servizio Web [classica]**, vedere [ripetere il training di un servizio web classica](machine-learning-retrain-a-classic-web-service.md).

Se è stata distribuita, fare clic su servizio web predittivo hello **distribuzione servizio Web [New]**, vedere [ripetere il training di un nuovo servizio web usando i cmdlet di Machine Learning Management hello](machine-learning-retrain-new-web-service-using-powershell.md).

<!-- Retrain a New web service using hello Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
