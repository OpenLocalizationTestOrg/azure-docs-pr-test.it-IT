---
title: servizio web esistente predittiva aaaRetrain | Documenti Microsoft
description: Informazioni su come tooretrain un modello e aggiornamento hello toouse hello appena sottoposto a training modello di servizio web in Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: cc4c26a2-5672-4255-a767-cfd971e46775
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-donglo
ms.openlocfilehash: fb0760d0a2adc34fc5f3df1ae41bdac075f91bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a>Ripetere il training di un servizio Web predittivo esistente
Questo documento descrive hello ripetizione di training processo per hello seguente scenario:

* Si dispone di un esperimento di training e di un esperimento predittivo distribuito come un servizio Web operativo.
* Si dispone di nuovi dati che si desidera il tooperform toouse di servizio web predittivo il relativo punteggio.

> [!NOTE] 
> un nuovo servizio web deve disporre di autorizzazioni sufficienti in hello toowhich di sottoscrizione per la distribuzione del servizio web hello toodeploy. Per ulteriori informazioni, vedere [gestire un servizio Web tramite il portale di servizi Web di Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

A partire dal servizio web esistente e gli esperimenti, è necessario toofollow questi passaggi:

1. Aggiornare il modello di hello.
   1. Modificare il tooallow esperimento di training per web servizio input e output.
   2. Distribuire hello esperimento di training come un servizio web i.
   3. Modello dell'esperimento di training hello servizio esecuzione Batch (BES) tooretrain hello.
2. Utilizzare l'esperimento predittiva di hello Azure Machine Learning PowerShell cmdlet tooupdate hello.
   1. Accedi tooyour account di gestione risorse di Azure.
   2. Ottenere una definizione del servizio web hello.
   3. Esportare una definizione del servizio web hello in formato JSON.
   4. Aggiornare i blob di ilearner toohello riferimento hello in hello JSON.
   5. Importare hello JSON in una definizione del servizio web.
   6. Aggiornare il servizio web di hello con una nuova definizione di servizio web.

## <a name="deploy-hello-training-experiment"></a>Distribuire l'esperimento di training hello
esperimento di training toodeploy hello come i servizio web, è necessario aggiungere l'input e output toohello modello di servizio web. Connettendo un *Output del servizio Web* dell'esperimento di modulo toohello  *[Train Model] [ train-model]*  modulo, si abilita hello esperimento di training tooproduce un nuovo modello con training che è possibile utilizzare nell'esperimento predittiva. Se dispone di un *Evaluate Model* modulo, è inoltre possibile allegare i risultati della valutazione hello tooget output servizio web come output.

tooupdate l'esperimento di training:

1. Connettere un *Web servizio Input* tooyour dati del modulo di input (ad esempio, un *Clean Missing Data* modulo). In genere, si desidera tooensure che i dati di input viene elaborati in hello stesso come dati di training originale.
2. Connettere un *Output del servizio Web* toohello output del modulo del *Train Model* modulo.
3. Se dispone di un *Evaluate Model* modulo e si desidera che i risultati della valutazione hello toooutput, connettere un *Output del servizio Web* toohello output del modulo del *Evaluate Model* modulo.

Eseguire l'esperimento.

Successivamente, è necessario distribuire hello esperimento di training come servizio web che produce un modello con training e risultati della valutazione del modello.  

Nella parte inferiore di hello dell'area di disegno esperimento hello, fare clic su **di servizio Web**, quindi selezionare **distribuzione servizio Web [New]**. viene visualizzato il portale di servizi Web di Azure Machine Learning Hello toohello **distribuzione servizio Web** pagina. Digitare un nome per il servizio Web, scegliere un piano di pagamento e quindi fare clic su **Deploy**(Distribuisci). Utilizzare il metodo di esecuzione Batch hello solo per la creazione di modelli di training.

## <a name="retrain-hello-model-with-new-data-by-using-bes"></a>Ripetere il training del modello di hello con nuovi dati utilizzando BES
Per questo esempio, si usa c# toocreate hello formazione dell'applicazione. È inoltre possibile utilizzare Python o R tooaccomplish codice di esempio questa attività.

hello toocall ripetizione di training API:

1. Creare un'applicazione console C# in Visual Studio. A tale scopo, selezionare **Nuovo** > **Progetto** > **Visual C#** > **Desktop classico di Windows** > **Applicazione console (.NET Framework)**.
2. Accedi toohello portale di servizi Web di Machine Learning.
3. Fare clic su servizio web hello che si sta lavorando.
4. Fare clic su **Consume**(Uso).
5. Nella parte inferiore di hello di hello **consumare** pagina hello **codice di esempio** fare clic su **Batch**.
6. Copiare hello c# codice di esempio per l'esecuzione batch e incollarlo nel file Program.cs hello. Verificare che lo spazio dei nomi hello rimane invariata.

Aggiungere il pacchetto NuGet hello webapi, come specificato nei commenti hello. tooadd hello riferimento tooMicrosoft.WindowsAzure.Storage.dll, è innanzitutto necessario tooinstall hello [libreria client per servizi di archiviazione di Azure](https://www.nuget.org/packages/WindowsAzure.Storage).

Hello schermata riportata di seguito viene illustrato hello **consumare** pagina nel portale di servizi Web di Azure Machine Learning hello.

![Pagina Consume (Utilizzo)][1]

### <a name="update-hello-apikey-declaration"></a>Aggiornare hello apikey dichiarazione
Individuare hello **apikey** dichiarazione:

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

In hello **informazioni di base al consumo** sezione di hello **consumare** individuare la chiave primaria di hello e copiarlo toohello **apikey** dichiarazione.

### <a name="update-hello-azure-storage-information"></a>Aggiornare le informazioni di archiviazione di Azure hello
codice di esempio BES Hello carica un file da un tooAzure unità locale (ad esempio, "C:\temp\CensusIpnput.csv"), archiviazione, elabora e scrive hello risultati indietro tooAzure archiviazione.  

informazioni di archiviazione di Azure hello tooupdate, è necessario recuperare l'account di archiviazione hello nome, chiave e contenitore le informazioni dell'account di archiviazione dal portale di Azure classico hello e aggiornamento hello correspondi dopo aver eseguito l'esperimento, hello risultante flusso di lavoro deve essere simile toohello seguenti:

![Flusso di lavoro risultante dopo l'esecuzione][4]valori nel codice hello NG.

1. Accedi toohello portale di Azure classico.
2. Nella colonna sinistra hello, fare clic su **archiviazione**.
3. Dall'elenco di hello di account di archiviazione, selezionare uno toostore hello ripetere il training del modello.
4. Nella parte inferiore di hello della pagina hello, fare clic su **Gestisci chiavi di accesso**.
5. Copiare e salvare hello **chiave di accesso primaria** e hello Chiudi finestra di dialogo.
6. Nella parte superiore di hello della pagina hello, fare clic su **contenitori**.
7. Selezionare un contenitore esistente, o crearne uno nuovo e salvare il nome di hello.

Individuare hello *StorageAccountName*, *StorageAccountKey*, e *StorageContainerName* dichiarazioni e aggiornare i valori hello salvato dal portale classico hello .

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

È inoltre necessario assicurarsi che file di input hello è disponibile nel percorso di hello specificate nel codice hello.

### <a name="specify-hello-output-location"></a>Specificare il percorso di output di hello
Quando si specifica il percorso di output di hello in hello del payload della richiesta, hello estensione del file hello specificato in *RelativeLocation* deve essere specificato come `ilearner`. Vedere hello di esempio seguente:

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you want toouse for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

Hello seguito è riportato un esempio di output di ripetizione di training: ![ripetizione di training output][6]

## <a name="evaluate-hello-retraining-results"></a>Valutare i risultati di ripetizione di training hello
Quando si esegue un'applicazione hello, l'output di hello include hello URL e il token di firme di accesso condiviso che sono risultati della valutazione hello tooaccess necessarie.

È possibile visualizzare i risultati delle prestazioni hello di hello Training modello combinando hello *BaseLocation*, *RelativeLocation*, e *SasBlobToken* dai risultati di output di hello per *USCITA2* (come mostrato nella precedente ripetizione di training immagine di output di hello) e incollare l'URL completo di hello nella barra degli indirizzi del browser hello.  

Esamina hello risultati toodetermine modello sottoposto a training appena hello esegue anche sufficiente hello tooreplace uno esistente.

Hello copia *BaseLocation*, *RelativeLocation*, e *SasBlobToken* dai risultati di output di hello.

## <a name="retrain-hello-web-service"></a>Ripetere il training del servizio web hello
Quando si ripetere il training di un nuovo servizio web, si aggiorna hello predittiva definizione tooreference hello nuovo sottoposto a training modello di servizio web. definizione del servizio web Hello è una rappresentazione interna del modello con training di hello del servizio web hello e non è direttamente modificabile. Assicurarsi che si desidera recuperare definizione hello del servizio web per l'esperimento predittiva e non l'esperimento di training.

## <a name="sign-in-tooazure-resource-manager"></a>Accedi tooAzure Gestione risorse
È innanzitutto necessario accedere tooyour account di Azure dall'ambiente di PowerShell hello utilizzando hello [Aggiungi AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.

## <a name="get-hello-web-service-definition-object"></a>Ottenere l'oggetto di definizione del servizio Web hello
Successivamente, ottenere l'oggetto di definizione del servizio Web di hello dal chiamante hello [Get AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

toodetermine hello Nome gruppo di risorse di un servizio web esistente, eseguire il cmdlet Get-AzureRmMlWebService hello senza servizi parametri toodisplay hello web nella sottoscrizione. Servizio web hello di individuare e quindi esaminare il relativo ID di servizio web. nome di Hello hello del gruppo di risorse è elemento quarto hello ID hello, subito dopo hello *resourceGroups* elemento. Nell'esempio seguente di hello, nome del gruppo di risorse hello è MachineLearning-predefinito-SouthCentralUS.

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

In alternativa, toodetermine hello Nome gruppo di risorse di un servizio web, accedere al portale di servizi Web di Azure Machine Learning toohello. Selezionare servizio web hello. nome del gruppo di risorse Hello è hello quinto elemento hello URL del servizio web hello, subito dopo hello *resourceGroups* elemento. Nell'esempio seguente di hello, nome del gruppo di risorse hello è MachineLearning-predefinito-SouthCentralUS.

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-object-as-json"></a>Esportare l'oggetto di definizione del servizio Web hello come JSON
definizione hello toomodify di hello toouse di modello con training hello appena eseguito il training del modello, è innanzitutto necessario utilizzare hello [esportazione AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) tooexport cmdlet è file tooa formato JSON.

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob"></a>Aggiornare hello riferimento toohello ilearner blob
Attività hello, individuare hello [modello con training], aggiornamento hello *uri* valore hello *locationInfo* nodo con l'URI del blob ilearner hello hello. Hello URI viene generato dalla combinazione hello *BaseLocation* hello e *RelativeLocation* dall'output di hello di chiamata i BES hello.

     "asset3": {
        "name": "Retrain Sample [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-hello-json-into-a-web-service-definition-object"></a>Importare hello JSON in un oggetto di definizione del servizio Web
È necessario utilizzare hello [importazione AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modificati file JSON in un oggetto di definizione del servizio Web che è possibile utilizzare predicative esperimento di tooupdate hello.

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service"></a>Aggiornare il servizio web hello
Infine, utilizzare hello [aggiornamento AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) tooupdate cmdlet hello esperimento predittiva.

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
