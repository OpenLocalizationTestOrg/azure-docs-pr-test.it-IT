---
title: un servizio web classica aaaRetrain | Documenti Microsoft
description: Informazioni su come tooprogrammatically ripetere il training di un modello e aggiornamento hello web servizio toouse hello appena modello con Training in Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: e36e1961-9e8b-4801-80ef-46d80b140452
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: d3ba21ed75f02868535cb2fcac607643303a9554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-classic-web-service"></a>Ripetere il training di un servizio Web classico
Hello predittiva del servizio Web è stato distribuito è predefinito hello punteggio endpoint. Gli endpoint predefiniti vengono mantenuti sincronizzati con hello originali di training e assegnazione dei punteggi esperimenti, e pertanto hello modello con training per l'endpoint predefinito hello non può essere sostituito. servizio web di hello tooretrain, è necessario aggiungere un nuovo servizio web toohello di endpoint. 

## <a name="prerequisites"></a>Prerequisiti
È necessario impostare un esperimento di training e un esperimento predittivo come illustrato in [Ripetere il training dei modelli di Machine Learning in modo programmatico](machine-learning-retrain-models-programmatically.md). 

> [!IMPORTANT]
> sperimentazione predittiva Hello deve essere distribuito come un classica servizio web machine learning. 
> 
> 

Per altre informazioni sulla distribuzione di servizi Web, vedere [Distribuire un servizio Web di Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="add-a-new-endpoint"></a>Aggiungere un nuovo endpoint
Hello predittiva del servizio Web che è stato distribuito contiene un endpoint che viene mantenuta la sincronizzazione con training originale hello e il modello con training di punteggio esperimenti di punteggio predefinito. tooupdate toowith per il servizio web un nuovo modello con training, è necessario creare un nuovo endpoint di assegnazione dei punteggi. 

un nuovo endpoint di punteggio, nel servizio Web predittivo che possono essere aggiornate con modello con training hello hello toocreate:

> [!NOTE]
> Assicurarsi che si sta aggiungendo hello toohello di endpoint servizio Web predittivo, non hello servizio Web di Training. Se sono stati distribuiti correttamente sia un servizio Web di training che uno predittivo, verranno visualizzati due servizi Web elencati separatamente. Servizio Web predittivo Hello deve terminare con "[predittiva exp]"..
> 
> 

Esistono tre modi in cui è possibile aggiungere un nuovo servizio web di tooa punto finale:

1. A livello di codice
2. Utilizzare il portale di servizi Web di Microsoft Azure hello
3. Utilizzare hello portale di Azure classico

### <a name="programmatically-add-an-endpoint"></a>Aggiungere un endpoint a livello di codice
È possibile aggiungere endpoint di assegnazione dei punteggi usando il codice di esempio hello fornito in questo [repository github](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).

### <a name="use-hello-microsoft-azure-web-services-portal-tooadd-an-endpoint"></a>Utilizzare hello tooadd portale di servizi Web di Microsoft Azure un endpoint
1. In Machine Learning Studio, nella colonna sinistra hello, fare clic su servizi Web.
2. Nella parte inferiore di hello del dashboard del servizio web hello, fare clic su **anteprima endpoint Gestisci**.
3. Fare clic su **Aggiungi**.
4. Digitare un nome e una descrizione per il nuovo endpoint di hello. Selezionare il livello di registrazione hello e indica se sono abilitati i dati di esempio. Per altre informazioni sulla registrazione, vedere [Abilitare la registrazione per i servizi Web di Machine Learning](machine-learning-web-services-logging.md).

### <a name="use-hello-azure-classic-portal-tooadd-an-endpoint"></a>Utilizzare hello Azure tooadd portale classico un endpoint
1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Nel menu a sinistra di hello, fare clic su **Machine Learning**.
3. In Nome fare clic sull'area di lavoro e quindi su **Servizi Web**.
4. In Nome fare clic su **Census Model [predictive exp.]**.
5. Nella parte inferiore di hello della pagina hello, fare clic su **Aggiungi Endpoint**. Per altre informazioni sull'aggiunta di endpoint, vedere [Creazione di endpoint](machine-learning-create-endpoint.md). 

## <a name="update-hello-added-endpoints-trained-model"></a>Aggiunta di hello aggiornamento modello con training dell'endpoint
processo di toocomplete i hello, è necessario aggiornare il modello con training di hello di hello nuovo endpoint in cui è stato aggiunto.

* Se è stato aggiunto nuovo endpoint hello usando il portale di Azure classico di hello, è possibile fare clic sul nome dell'endpoint di hello nuovo nel portale di hello quindi hello **UpdateResource** collegamento URL hello tooget è necessario il modello dell'endpoint di tooupdate hello.
* Se si aggiungono endpoint hello mediante il codice di esempio hello, sono inclusi percorso dell'URL della Guida hello identificato da hello *HelpLocationURL* valore nell'output di hello.

tooretrieve hello percorso URL:

1. Copiare e incollare l'URL di hello nel browser.
2. Fare clic sul collegamento di aggiornamento risorsa hello.
3. Copiare hello POST URL della richiesta PATCH hello. ad esempio:
   
     PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2

È ora possibile utilizzare hello tooupdate di modello con training hello punteggio endpoint creato in precedenza.

Hello codice di esempio seguente illustra come hello toouse *BaseLocation*, *RelativeLocation*, *SasBlobToken*e l'URL di PATCH tooupdate hello endpoint.

    private async Task OverwriteModel()
    {
        var resourceLocations = new
        {
            Resources = new[]
            {
                new
                {
                    Name = "Census Model [trained model]",
                    Location = new AzureBlobDataReference()
                    {
                        BaseLocation = "https://esintussouthsus.blob.core.windows.net/",
                        RelativeLocation = "your endpoint relative location", //from hello output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from hello output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
                    }
                }
            }
        };

        using (var client = new HttpClient())
        {
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", apiKey);

            using (var request = new HttpRequestMessage(new HttpMethod("PATCH"), endpointUrl))
            {
                request.Content = new StringContent(JsonConvert.SerializeObject(resourceLocations), System.Text.Encoding.UTF8, "application/json");
                HttpResponseMessage response = await client.SendAsync(request);

                if (!response.IsSuccessStatusCode)
                {
                    await WriteFailedResponse(response);
                }

                // Do what you want with a successful response here.
            }
        }
    }

Hello *apiKey* hello e *endpointUrl* per chiamata hello può essere ottenuto dal dashboard di endpoint.

valore di hello Hello *nome* parametro *risorse* deve hello corrispondenza nome risorsa di hello salvato il modello con training nella sperimentazione predittiva hello. hello tooget nome risorsa:

1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Nel menu a sinistra di hello, fare clic su **Machine Learning**.
3. In Nome fare clic sull'area di lavoro e quindi su **Servizi Web**.
4. In Nome fare clic su **Census Model [predictive exp.]**.
5. Fare clic su nuovo endpoint hello che è stato aggiunto.
6. Nel dashboard di endpoint hello, fare clic su **aggiornamento risorsa**.
7. Nella pagina di hello la documentazione dell'API di risorsa di aggiornamento per il servizio web hello, è possibile trovare hello **nome risorsa** in **risorse aggiornabili**.

Se il token di firma di accesso condiviso scade prima di completare l'aggiornamento dell'endpoint di hello, è necessario eseguire un'operazione GET con hello Id processo tooobtain un nuovo token.

Quando il codice hello è stato eseguito correttamente, deve iniziare nuovo endpoint hello tramite il modello di training hello in circa 30 secondi.

## <a name="summary"></a>Riepilogo
Utilizzando hello API ripetizione di training, è possibile aggiornare hello modello con training di un servizio Web predittivo abilitazione degli scenari, ad esempio:

* Ripetizione periodica del training del modello con nuovi dati.
* Distribuzione di un modello di toocustomers con obiettivo hello di informarli del training modello di hello usando i propri dati.

## <a name="next-steps"></a>Passaggi successivi
[Risoluzione dei problemi hello ripetizione di training di un servizio web classico di Azure Machine Learning](machine-learning-troubleshooting-retraining-models.md)

