---
title: "Regressione lineare multivariata (funzionalità deprecata) - Azure| Documentazione Microsoft"
description: "Regressione lineare multivariata (funzionalità deprecata)"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 2fb78220-ced9-4564-a439-9e5df6772994
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 65a8005139e920cd19593e954fc1bf836354bdf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-multivariate-linear-regression"></a>Regressione lineare multivariata (funzionalità deprecata)

> [!NOTE]
> Microsoft DataMarket è in fase di ritiro e questa API è stata deprecata. 
> 
> Numerose API e molti esperimenti utili di esempio sono disponibili in [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Per altre informazioni sulla raccolta, vedere [Condividere e scoprire risorse in Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

Si supponga di disporre di un set di dati e di volere prevedere rapidamente una variabile dipendente (y) per ogni individuo (i) sulla base delle altre variabili indipendenti. La regressione lineare è una tecnica statistica popolare usata per previsioni di questo tipo. In questo caso si presuppone che la variabile dipendente y sia un valore continuo.  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Uno scenario semplice è costituito da un ricercatore che tenta di prevedere il peso di un individuo (y) basandosi sull'altezza (x). Uno scenario più avanzato è costituito da un ricercatore che ha a disposizione informazioni aggiuntive per l'individuo, ad esempio il peso, il genere e l'etnia, e tenta di prevedere il peso dell'individuo. Questo [servizio Web](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) adegua il modello di regressione lineare ai dati e fornisce come output il valore previsto (y) per ogni osservazione nei dati.

> Questo servizio Web può essere utilizzato dagli utenti: potenzialmente tramite un'app mobile, un sito Web o anche in un computer locale, ad esempio. Ma lo scopo del servizio Web è anche fornire un esempio di come è possibile utilizzare Azure Machine Learning per creare servizi Web in codice R. Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web. Il servizio Web può essere quindi pubblicato in Azure Marketplace e può essere usato da utenti e dispositivi in tutto il mondo, senza che l'autore del servizio Web debba configurare alcuna infrastruttura.  
> 
> 

## <a name="consumption-of-web-service"></a>Uso del servizio Web
Questo servizio Web fornisce i valori previsti della variabile dipendente sulla base delle variabili indipendenti per tutte le osservazioni. Il servizio Web richiede che l'utente finale immetta i dati come una stringa in cui le righe sono separate da virgola (,) e le colonne sono separate da punto e virgola (;). Il servizio Web richiede una riga alla volta e che la prima colonna corrisponda alla variabile dipendente. Un set di dati di esempio può avere un aspetto analogo al seguente:

![Dati di esempio][1]

Osservazioni senza una variabile dipendente devono essere immesse come "NA" per l'asse y. L'input di dati per il set di dati precedente sarebbe analogo alla seguente stringa: “10;5;2,18;1;6,6;5.3;2.1,7;5;5,22;3;4,12;2;1,NA;3;4. L'output è il valore previsto per ogni riga sulla base delle variabili indipendenti. 

> Questo servizio, come ospitato in Azure Marketplace, è un servizio OData ed è possibile utilizzare i metodi POST o GET per effettuare le chiamate. 
> 
> 

Sono disponibili molte opzioni per l'uso del servizio in modalità automatica. Per un'app di esempio, vedere [qui](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx).

### <a name="starting-c-code-for-web-service-consumption"></a>Codice C# iniziale per l'uso del servizio Web:
    public class Input
    {
            public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




## <a name="creation-of-web-service"></a>Creazione del servizio Web
> Questo servizio Web è stato creato tramite Azure Machine Learning. Per una versione di prova gratuita e per video introduttivi sulla creazione di esperimenti e sulla [pubblicazione di servizi Web](machine-learning-publish-a-machine-learning-web-service.md), vedere [azure.com/ml](http://azure.com/ml). La schermata seguente mostra un esperimento per la creazione del servizio Web e codice di esempio per ogni modulo incluso nell'esperimento.
> 
> 

In Azure Machine Learning è stato creato un nuovo esperimento vuoto e sono stati inseriti due moduli [Execute R Script][execute-r-script] (Esegui script R) nell'area di lavoro. Questo servizio Web esegue un esperimento di Azure Machine Learning con lo script R sottostante. Esistono 2 parti di questo esperimento: la definizione dello schema e il modello di training + punteggio. Il primo modulo definisce la struttura prevista del set di dati di input in cui la prima variabile è dipendente e le variabili rimanenti sono indipendenti. Il secondo modulo è appropriato per un modello di regressione lineare generico per i dati di input.  

![Flusso dell'esperimento][3]

#### <a name="module-1"></a>Modulo 1:
#### <a name="schema-definition"></a>Definizione dello schema
    data <- data.frame(value = "1;2;3,4;5;6,7;8;9", stringsAsFactors=FALSE) maml.mapOutputPort("data");  

#### <a name="module-2"></a>Modulo 2:
#### <a name="lm-modeling"></a>Creazione di modelli LM
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]]  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- as.data.frame(t(data.split)) 
    data.split <- data.matrix(data.split) 
    data.split <- data.frame(data.split) 
    model <- lm(data.split)  

    out=data.frame(predict(model,data.split))  
    out <- data.frame(t(out))

    maml.mapOutputPort("out");  

## <a name="limitations"></a>Limitazioni
Questo è un esempio molto semplice di un servizio Web di regressione lineare multipla. Come si può notare nell'esempio di codice precedente, il rilevamento degli errori non è implementato e il servizio presuppone che qualsiasi elemento sia una variabile continua (non sono consentite funzionalità categoriche), poiché il servizio immette come input solo valori numerici al momento della creazione del servizio Web. Il servizio, inoltre, gestisce attualmente dimensioni limitate di dati a causa della natura di richiesta/risposta della chiamata del servizio Web e del fatto che il modello viene definito ogni volta che il servizio Web viene chiamato. 

## <a name="faq"></a>Domande frequenti
Per le domande frequenti relative all'uso del servizio Web o alla pubblicazione in Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

