---
title: Differenza in percentuale di Test - Azure AAA(deprecated) | Documenti Microsoft
description: (Deprecato) Differenza nel test sulle proporzioni
services: machine-learning
documentationcenter: 
author: aniedea
manager: jhubbard
editor: cgronlun
ms.assetid: 9356b821-5345-44f6-8e26-719f2dea5e6d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: aniedea
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 820aad377f9dec12b0ef455974aaa95f6e8d723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-difference-in-proportions-test"></a>(Deprecato) Differenza nel test sulle proporzioni

> [!NOTE]
> è stata ritirata Hello Microsoft DataMarket e questa API è stata deprecata. 
> 
> Sono disponibili molte esperimenti di esempio utile e API hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Per ulteriori informazioni sulla raccolta hello, vedere [condivisione e individuare le risorse in Cortana Intelligence Gallery hello](machine-learning-gallery-how-to-use-contribute-publish.md).

Due proporzioni presentano differenze a livello statistico? Si supponga che un utente desideri toocompare due filmati toodetermine se un filmato ha una proporzione notevolmente maggiore di "mi piace' quando confrontati toohello altri. Con un esempio di grandi dimensioni, potrebbe esserci una differenza tra percentuali hello 0,50 e 0.51 statisticamente significativa. Con un piccolo esempio, si potrebbe non essere sufficiente toodetermine dati se queste proporzioni in realtà sono diverse. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Questo [servizio web](https://datamarket.azure.com/dataset/aml_labs/prop_test) esegue un test di ipotesi di differenza hello in due proporzioni in base all'input utente hello numero di esiti positivi del numero totale di hello di versioni di valutazione per i gruppi di confronto hello 2. In uno scenario, il servizio web potrebbe essere chiamato all'interno di un'app di confronto di film, che indica hello se uno dei filmati hello è 'dinamica' più spesso degli altri, hello in base alle classificazioni di film.

> Questo servizio Web può essere utilizzato dagli utenti: potenzialmente tramite un'app mobile, un sito Web o anche in un computer locale, ad esempio. Ma scopo hello del servizio web hello anche tooserve come esempio di come Azure Machine Learning è possibile servizi web utilizzati toocreate su codice R. Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web. servizio web Hello può quindi essere pubblicata toohello Azure Marketplace e utilizzato da utenti e dispositivi attraverso HelloWorld con alcuna installazione dell'infrastruttura dall'autore hello del servizio web hello.
> 
> 

## <a name="consumption-of-web-service"></a>Uso del servizio Web
Questo servizio accetta quattro argomenti ed esegue una verifica dell'ipotesi delle proporzioni.

gli argomenti di input Hello sono:

* Successes1: numero di eventi con esito positivo nel campione 1.
* Successes2: numero di eventi con esito positivo nel campione 2.
* Total1: dimensione del campione 1.
* Total2: dimensione del campione 2.

output di Hello del servizio hello è risultato hello dell'ipotesi hello test insieme hello chi-quadrato statistica, df, p-valore e proporzioni nei limiti di 1/2 e l'intervallo di confidenza di esempio.

> Questo servizio, ospitato in Azure Marketplace, hello è un servizio OData. questi può essere chiamati tramite i metodi POST o GET. 
> 
> 

Esistono diversi modi di utilizzo di servizio hello in modo automatico (è un'app di esempio [qui](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Codice C# iniziale per l'uso del servizio Web:
    public class Input
    {
            public string successes1;
            public string successes2;
            public string total1;
            public string total2;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { successes1 = TextBox1.Text, successes2 = TextBox2.Text, total1 = TextBox3.Text, total2 = TextBox4.Text };
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
> Questo servizio Web è stato creato tramite Azure Machine Learning. Per una versione di prova gratuita e per video introduttivi sulla creazione di esperimenti e sulla [pubblicazione di servizi Web](machine-learning-publish-a-machine-learning-web-service.md), vedere [azure.com/ml](http://azure.com/ml). Di seguito è riportata una schermata dell'esperimento hello creato codice di esempio e servizio web hello per ciascuno dei moduli di hello all'interno di sperimentazione hello.
> 
> 

In Azure Machine Learning è stato creato un nuovo esperimento vuoto con due moduli [Execute R Script][execute-r-script] (Esegui script R). Nel primo modulo hello schema dati hello è definito, mentre il secondo modulo hello utilizza il comando prop.test hello all'interno dei test di ipotesi R tooperform hello per le 2 proporzioni. 

### <a name="experiment-flow"></a>Flusso dell'esperimento
![Flusso dell'esperimento][2]

#### <a name="module-1"></a>Modulo 1:
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data toooutput port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a>Modulo 2:
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"hello proportions are different!",
    "hello proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a>Limitazioni
Questo è un esempio molto semplice per la verifica della differenza tra due proporzioni. Come si può notare dal codice di esempio hello precedente, non viene implementato alcun rilevamento di errori e servizio hello si presuppone che tutte le variabili di hello continua.

## <a name="faq"></a>domande frequenti
Per domande frequenti sull'utilizzo del servizio web hello o pubblicazione toohello Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

