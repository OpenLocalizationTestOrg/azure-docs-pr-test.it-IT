---
title: AAA(deprecated) Multivariate Linear Regression - Azure | Documenti Microsoft
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
redirect_document_id: True
ms.openlocfilehash: 0ff7221cd06c0ef059b0c5bf327016588174dcfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-multivariate-linear-regression"></a>Regressione lineare multivariata (funzionalità deprecata)

> [!NOTE]
> è stata ritirata Hello Microsoft DataMarket e questa API è stata deprecata. 
> 
> Sono disponibili molte esperimenti di esempio utile e API hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Per ulteriori informazioni sulla raccolta hello, vedere [condivisione e individuare le risorse in Cortana Intelligence Gallery hello](machine-learning-gallery-how-to-use-contribute-publish.md).

Si supponga che si dispone di un set di dati e come tooquickly potrebbe prevedere una variabile dipendente (y) per ogni singolo cliente (i) in base alle variabili indipendenti. La regressione lineare è una tecnica statistica popolare usata per previsioni di questo tipo. Di seguito hello variabile dipendente y presuppone toobe un valore continuo.  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Potrebbe essere un semplice scenario in cui ingegno hello tenta peso hello toopredict di una persona (y) in base all'altezza (x). Uno scenario più avanzato potrebbe essere in ingegno hello dispone di informazioni aggiuntive per singola (ad esempio, weight, sesso, race) hello e tenta di peso hello toopredict di hello singolo. Questo [servizio web](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) adatto hello dati toohello del modello di regressione lineare e output hello valore stimato (y) per ognuna delle osservazioni hello nei dati hello.

> Questo servizio Web può essere utilizzato dagli utenti: potenzialmente tramite un'app mobile, un sito Web o anche in un computer locale, ad esempio. Ma scopo hello del servizio web hello anche tooserve come esempio di come Azure Machine Learning è possibile servizi web utilizzati toocreate su codice R. Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web. servizio web Hello può quindi essere pubblicata toohello Azure Marketplace e utilizzato da utenti e dispositivi attraverso HelloWorld con alcuna installazione dell'infrastruttura dall'autore hello del servizio web hello.  
> 
> 

## <a name="consumption-of-web-service"></a>Uso del servizio Web
I valori di variabile dipendente hello in base alle variabili indipendenti hello per tutte le osservazioni hello è stato stimato questo hello consente di servizio web. servizio web Hello dati tooinput utente finale di hello previsto è una stringa in cui le righe sono separate da virgole (,) e le colonne sono separate da punti e virgola (;). servizio web Hello prevista 1 riga alla volta e non prevede hello prima colonna toobe hello variabile dipendente. Un set di dati di esempio può avere un aspetto analogo al seguente:

![Dati di esempio][1]

Osservazioni senza una variabile dipendente devono essere immesse come "NA" per l'asse y. Hello dati di input per hello di sopra di set di dati potrebbe essere hello seguente stringa: "10 5; 2,18; 1; 6,6; 5.3; 2.1,7; 5; 5,22; 3; 4,12; 2; 1, NA, 3, 4". output di Hello hello valore stimato per ognuna delle righe hello si basa su variabili indipendenti hello. 

> Questo servizio, ospitato in Azure Marketplace, hello è un servizio OData. questi può essere chiamati tramite i metodi POST o GET. 
> 
> 

Esistono diversi modi di utilizzo di servizio hello in modo automatico (è un'app di esempio [qui](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).

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
> Questo servizio Web è stato creato tramite Azure Machine Learning. Per una versione di prova gratuita e per video introduttivi sulla creazione di esperimenti e sulla [pubblicazione di servizi Web](machine-learning-publish-a-machine-learning-web-service.md), vedere [azure.com/ml](http://azure.com/ml). Di seguito è riportata una schermata dell'esperimento hello creato codice di esempio e servizio web hello per ciascuno dei moduli di hello all'interno di sperimentazione hello.
> 
> 

Da Azure Machine Learning, all'interno di un esperimento vuoto nuovo è stato creato e due [Execute R Script] [ execute-r-script] moduli sono stati estratti nell'area di lavoro hello. Questo servizio Web esegue un esperimento di Azure Machine Learning con lo script R sottostante. Esistono sperimentare toothis 2 part: definizione di schema e di training del modello di + punteggio. primo modulo Hello definisce struttura hello previsto di hello input set di dati, in cui hello prima variabile è variabile dipendente hello e variabili rimanenti hello sono indipendenti. secondo modulo Hello adatta un modello di regressione lineare generico per i dati di input hello.  

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
Questo è un esempio molto semplice di un servizio Web di regressione lineare multipla. Nessun rilevamento di errori viene implementato come possono essere visualizzati dal codice di esempio hello precedente, e presuppone servizio hello tutto ciò che è una variabile continua (nessuna funzionalità categorica consentita), come hello servizio solo input valori numerici in fase di hello della creazione di hello del sito web servizio. Inoltre, hello servizio gestisce attualmente le dimensioni dei dati limitato, a causa di natura di richiesta/risposta toohello del servizio web hello si adatta chiamata e hello delle tabelle dei fatti che hello modello ogni volta che viene chiamato servizio web hello. 

## <a name="faq"></a>domande frequenti
Per domande frequenti sull'utilizzo del servizio web hello o pubblicazione toohello Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

