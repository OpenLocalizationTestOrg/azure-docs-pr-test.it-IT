---
title: un servizio web Machine Learning con un modello di app web aaaConsume | Documenti Microsoft
description: Utilizzare un modello di applicazione web in Azure Marketplace tooconsume un servizio web predittivo in Azure Machine Learning.
keywords: servizio Web,messa in funzione,API REST,Machine Learning
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e0d71683-61b9-4675-8df5-09ddc2f0d92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;raymondl
ms.openlocfilehash: 1199377bead470807d58ca7f7a667175cbb88450
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a>Utilizzare un servizio Web di Azure Machine Learning con un modello di app Web

Dopo aver sviluppato il modello predittivo e viene distribuito come servizio web di Azure tramite Machine Learning Studio o mediante strumenti quali R o Python, è possibile accedere hello operativi i modello utilizzando un'API REST.

Esistono diversi modi tooconsume hello API REST e accesso hello servizio web. Ad esempio, è possibile scrivere un'applicazione in c#, R, o Python mediante hello codice generato automaticamente al momento della distribuzione del servizio web hello di esempio (disponibile in hello [portale dei servizi Web Machine Learning](https://services.azureml.net/quickstart) o nel dashboard del servizio web hello in Machine Learning Studio). Oppure è possibile utilizzare una cartella di Microsoft Excel di esempio hello creata alla hello contemporaneamente.

Ma hello tooaccess più semplice e rapido è il servizio web tramite i modelli di App Web hello disponibili in hello [App Web di Azure Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-azure-machine-learning-web-app-templates"></a>Modelli di App Web di Azure Machine Learning Hello
modelli di app web Hello disponibili in Azure Marketplace hello è possono compilare un'app web personalizzato in grado di dati di input del servizio web e i risultati previsti. È sufficiente toodo è di fornire dati e il servizio web di hello web app accesso tooyour e modello hello hello rest.

Sono disponibili due modelli:

* [Modello di app Web del servizio di richiesta/risposta di Azure ML](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [Modello di app Web del servizio di esecuzione batch di Azure ML](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

Ogni modello crea un'applicazione ASP.NET di esempio, con hello URI API e la chiave per il servizio web e lo distribuisce come tooAzure un sito web. modello di servizio richiesta-risposta (RR) Hello crea un'app web che consente di toosend una singola riga di dati toohello web servizio tooget un singolo risultato. modello di servizio esecuzione Batch (BES) Hello crea un'app web che consente di toosend numerose righe di dati tooget più risultati.

Nessun tipo di codifica è obbligatorio toouse questi modelli. È sufficiente specificare hello chiave API e l'URI e il modello di hello compila l'applicazione hello.

chiave API hello tooget e l'URI della richiesta per un servizio web:

1. In hello [portale dei servizi Web](https://services.azureml.net/quickstart), per un nuovo servizio web, fare clic su **servizi Web** nella parte superiore di hello. Per un servizio Web classico, fare clic su **Servizi Web classici**.
2. Fare clic su servizio web di hello da tooaccess.
3. Per un servizio web classica, fare clic sull'endpoint hello desiderato tooaccess.
4. Fare clic su **consumare** nella parte superiore di hello.
5. Hello copia **primario** o **chiave secondaria** e salvarlo.
6. Se si sta creando un modello di servizio richiesta-risposta (RR), copiare hello **richiesta-risposta** URI e salvarlo. Se si sta creando un modello di servizio esecuzione Batch (BES), copiare hello **richieste Batch** URI e salvarlo.


## <a name="how-toouse-hello-request-response-service-rrs-template"></a>Come toouse hello modello richiesta-risposta del servizio (RR)
Seguire questi passaggi toouse hello RR app modello web, come illustrato nel seguente diagramma hello.

![Modello di processo toouse RR web][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. Passare toohello [portale di Azure](https://portal.azure.com), **accesso**, fare clic su **New**, cercare e selezionare **Azure ML richiesta-risposta del servizio Web App**, quindi fare clic su **Creare**. 
   
   * Assegnare all'app Web un nome univoco. URL di Hello dell'app web hello sarà il nome seguito da `.azurewebsites.net.` , ad esempio,`http://carprediction.azurewebsites.net.`
   * Selezionare servizi e hello sottoscrizione di Azure in cui è in esecuzione il servizio web.
   * Fare clic su **Crea**.
     
     ![Crea app Web][image5]

4. Quando Azure ha completato la distribuzione di app web hello, fare clic su hello **URL** hello pagina Impostazioni di app web in Azure, o immettere l'URL di hello in un web browser. Ad esempio, `http://carprediction.azurewebsites.net.`
5. Quando hello prima esecuzione applicazione web, verrà chiesto di hello **API Post URL** e **chiave API**.
   Immettere i valori hello salvato in precedenza (**URI della richiesta** e **chiave API**, rispettivamente).
     
     Fare clic su **Submit**.
     
     ![Immettere Post URI e API Key][image6]

6. Hello web app viene visualizzata la **configurazione delle App Web** pagina con le impostazioni del servizio web corrente hello. Qui è possibile modificare le impostazioni di toohello usate dall'app web hello.
   
   > [!NOTE]
   > Modifica delle impostazioni di hello qui solo li modifica per questa app web. Non modifica le impostazioni predefinite di hello del servizio web. Ad esempio, se si modifica hello **descrizione** qui non modifica descrizione hello visualizzate nel dashboard del servizio web hello in Machine Learning Studio.
   > 
   > 
   
    Al termine, fare clic su **salvare modifiche**, quindi fare clic su **passare tooHome pagina**.

7. Da hello pagina home che è possibile immettere i valori del servizio web di toosend tooyour. Fare clic su **Invia** quando è terminato e verrà restituito il risultato di hello.

Se si desidera tooreturn toohello **configurazione** pagina, visitare toohello `setting.aspx` pagina dell'app web hello. Ad esempio: `http://carprediction.azurewebsites.net/setting.aspx.` sarà chiave hello API tooenter richiesta nuovamente, è necessario che tooaccess hello pagina e aggiornare le impostazioni di hello.

È possibile riavviare, arrestare o eliminare l'app web hello in hello portale di Azure come qualsiasi altra app web. Fino a quando è in esecuzione è possibile individuare l'indirizzo web home toohello e immettere nuovi valori.

## <a name="how-toouse-hello-batch-execution-service-bes-template"></a>Come toouse hello modello Servizio esecuzione Batch (BES)
È possibile utilizzare BES hello modello applicazione web in hello stesso modo come modello di record di risorse hello, ad eccezione di app web hello creato sarà toosubmit più righe di dati e la ricezione di più risultati.

valori di input per un servizio web di esecuzione batch Hello possono provenire da archiviazione di Azure o un file locale. Hello risultati vengono archiviati in un contenitore di archiviazione di Azure.
In tal caso, sarà necessario un toohold contenitore di archiviazione di Azure hello risultati restituiti dall'app web hello e sarà necessario tooget i dati di input pronto.

![Elaborare toouse BES modello web][image2]

1. Seguire hello stesso hello toocreate procedure BES web app per modello di record di risorse hello, ad eccezione di go troppo[modello di App di Azure ML Batch esecuzione del servizio Web](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen hello modello BES in Azure Marketplace e fare clic su **creare App Web** .

2. toospecify in cui si desidera risultati hello archiviati, immettere le informazioni sul contenitore di destinazione hello nella home page di hello web app. Specificare anche dove hello web app può ottenere valori di input di hello, in un file locale o un contenitore di archiviazione di Azure.
   Fare clic su **Submit**.
   
    ![Informazioni sull'archiviazione][image7]

app web Hello verrà visualizzata una pagina con lo stato del processo.
Completato il processo di hello verranno presentate hello percorso di hello risultati nell'archiviazione blob di Azure. È anche possibile hello download hello risultati tooa del file locale.

## <a name="for-more-information"></a>Per altre informazioni
toolearn ulteriori informazioni...

* creazione di un esperimento di apprendimento automatico con Machine Learning Studio, vedere [Esercitazione di Machine Learning: Creare il primo esperimento in Azure Machine Learning Studio](machine-learning-create-experiment.md)
* toodeploy l'apprendimento esperimento come servizio web, vedere [distribuire un servizio web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md)
* altri modi tooaccess il servizio web, vedere [come tooconsume un servizio Web di Azure Machine Learning](machine-learning-consume-web-services.md)

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
