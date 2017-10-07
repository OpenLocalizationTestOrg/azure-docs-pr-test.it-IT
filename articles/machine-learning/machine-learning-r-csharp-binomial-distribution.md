---
title: 'AAA(deprecated) distribuzione binomiale Suite: Azure | Documenti Microsoft'
description: (Deprecato) Binomial Distribution Suite
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: 6d102d57-8f20-4ab3-be31-02fcfe4d15ed
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: ireiter
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 6f94436cd19abeb518d179f340c8d4f43fcf4520
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binomial-distribution-suite"></a>(Deprecato) Binomial Distribution Suite

> [!NOTE]
> è stata ritirata Hello Microsoft DataMarket e questa API è stata deprecata. 
> 
> Sono disponibili molte esperimenti di esempio utile e API hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Per ulteriori informazioni sulla raccolta hello, vedere [condivisione e individuare le risorse in Cortana Intelligence Gallery hello](machine-learning-gallery-how-to-use-contribute-publish.md).

Distribuzione binomiale Suite Hello è un set di servizi web di esempio ([binomiale generatore](https://datamarket.azure.com/dataset/aml_labs/bdg5), [calcolatrice probabilità](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile Calcolatrice](https://datamarket.azure.com/dataset/aml_labs/bdq5)) che consentono di generare e gestione di binomiale. Hello services consente la generazione di una sequenza di distribuzione binomiale di qualsiasi lunghezza, il calcolo dei quantili fuori specificato da un determinato quantile probabilità e il calcolo di probabilità. Ognuno dei servizi hello genera output diversi basati sul servizio hello selezionato (vedere la descrizione riportata di seguito). Distribuzione binomiale Suite Hello dipende hello R funzioni qbinom rbinom e pbinom, che sono inclusi nel pacchetto di hello R statistiche. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> Questi servizi web che poteva essere usati dagli utenti: potenzialmente direttamente nel marketplace hello, tramite un'app per dispositivi mobili, tramite un sito Web, o anche in un computer locale, ad esempio. Ma scopo hello del servizio web hello anche tooserve come esempio di come Azure Machine Learning è possibile servizi web utilizzati toocreate su codice R. Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web. servizio web Hello può quindi essere pubblicata toohello Azure Marketplace e non utilizzati da utenti e dispositivi attraverso HelloWorld – alcuna installazione dell'infrastruttura dall'autore hello del servizio web hello è obbligatorio.
> 
> 

## <a name="consumption-of-web-service"></a>Uso del servizio Web
Hello binomiale Suite include hello dopo 3 servizi.

### <a name="binomial-distribution-quantile-calculator"></a>Binomial Distribution Quantile Calculator
Il servizio accetta 4 argomenti di una distribuzione normale e calcola i quantili hello associata.
gli argomenti di input Hello sono:

* p: probabilità aggregata singola di più prove.  
* dimensione - numero hello di prove.
* probabilità - probabilità hello di successo in una versione di valutazione.
* Lato - L per lato inferiore di hello della distribuzione di hello, U sul lato superiore di hello della distribuzione hello. 

output di Hello del servizio hello è quantile hello calcolato che è associato a hello dato probabilità.

### <a name="binomial-distribution-probability-calculator"></a>Binomial Distribution Probability Calculator
Il servizio accetta 4 argomenti di una distribuzione binomiale e calcola la probabilità associata hello.
gli argomenti di input Hello sono:

* q: singolo quantile di un evento con distribuzione binomiale. 
* dimensione - numero hello di prove.
* probabilità - probabilità hello di successo in una versione di valutazione.
* lato - L per lato inferiore di hello della distribuzione di hello, U sul lato superiore di hello della distribuzione hello o E che è uguale tooa singolo numero di esiti positivi.

output di Hello del servizio hello è hello calcolata la probabilità che è associato a hello specificato di quantili.

### <a name="binomial-distribution-generator"></a>Binomial Distribution Generator
Questo servizio accetta tre argomenti di una distribuzione binomiale e genera una sequenza casuale di numeri distribuiti in modo binomiale. Hello seguenti devono essere specificati argomenti tooit richiesta hello:

* n: numero di osservazioni. 
* size: numero di prove.
* prob: probabilità di successo.

output di Hello del servizio hello è una sequenza di lunghezza n con una distribuzione binomiale basata sugli argomenti di dimensioni e la probabilità di hello.

> Questo servizio, ospitato in Azure Marketplace, hello è un servizio OData. questi può essere chiamati tramite i metodi POST o GET. 
> 
> 

Esistono diversi modi di utilizzo di servizio hello in modo automatico (app di esempio in questa sezione sono: [generatore](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [calcolatrice probabilità](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile Calcolatrice](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)). 

### <a name="starting-c-code-for-web-service-consumption"></a>Codice C# iniziale per l'uso del servizio Web:
### <a name="binomial-distribution-quantile-calculator"></a>Binomial Distribution Quantile Calculator
    public class Input
    {
            public string p;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void main()
    {
            var input = new Input() { p = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="binomial-distribution-probability-calculator"></a>Binomial Distribution Probability Calculator
    public class Input
    {
            public string q;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = " PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="binomial-distribution-generator"></a>Binomial Distribution Generator
    public class Input
    {
            public string n;
            public string size;
            public string p;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, size = TextBox2.Text, p = TextBox3.Text };
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

### <a name="binomial-distribution-quantile-calculator"></a>Binomial Distribution Quantile Calculator
![Creare un'area di lavoro][4]

#### <a name="module-1"></a>Modulo 1:
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port
#### <a name="module-2"></a>Modulo 2:
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }

    if (param$prob < 0 ) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 0
    } else if (param$prob > 1) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 1
    }

    quantile = qbinom(param$p,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    quantile

    if (param$side == 'U'){
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = F)
    band=subset(df,x>quantile)
    } else if (param$side =='L') {
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = T)
    band=subset(df,x<=quantile)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(quantile)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");


### <a name="binomial-distribution-probability-calculator"></a>Binomial Distribution Probability Calculator
![Creare un'area di lavoro][5]

#### <a name="module-1"></a>Modulo 1:
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(q=5,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port


#### <a name="module-2"></a>Modulo 2:
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    prob = pbinom(param$q,size=param$size,prob=param$prob)
    prob.eq = dbinom(param$q,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    prob

    if (param$side == 'U'){
    prob = 1 - prob
    band=subset(df,x>param$q)
    } else if (param$side =='E') {
    prob = prob.eq
    band=subset(df,x==param$q)
    } else if (param$side =='L') {
    prob = prob
    band=subset(df,x<=param$q)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="binomial-distribution-generator"></a>Binomial Distribution Generator
![Creare un'area di lavoro][6]

#### <a name="module-1"></a>Modulo 1:
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,size=10,p=.5);
    maml.mapOutputPort("data.set"); #send data toooutput port

#### <a name="module-2"></a>Modulo 2:
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    dist = rbinom(param$n,param$size,param$p)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a>Limitazioni
Questi sono esempi molto semplici che circonda hello binomiale. Come si può notare dal codice di esempio hello precedente, il rilevamento di errori poco viene implementato.

## <a name="faq"></a>domande frequenti
Per domande frequenti sull'utilizzo del servizio web hello o pubblicazione toohello Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_1.png

[2]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_2.png

[3]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_3.png

[4]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_4.png

[5]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_5.png

[6]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_6.png

