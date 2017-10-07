---
title: AAA(deprecated) lessico basato su analisi del Sentiment - Azure | Documenti Microsoft
description: (Deprecato) Analisi del sentiment basata sul lessico
services: machine-learning
documentationcenter: 
author: pengxia
manager: jhubbard
editor: cgronlun
ms.assetid: 912f41af-966c-4d79-a413-6f9fc02823df
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: pengxia
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 1ed7e19441c6a8ad270a0c0f567b4aea588a583e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-lexicon-based-sentiment-analysis"></a>(Deprecato) Analisi del sentiment basata sul lessico

> [!NOTE]
> è stata ritirata Hello Microsoft DataMarket e questa API è stata deprecata. 
> 
> Sono disponibili molte esperimenti di esempio utile e API hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Per ulteriori informazioni sulla raccolta hello, vedere [condivisione e individuare le risorse in Cortana Intelligence Gallery hello](machine-learning-gallery-how-to-use-contribute-publish.md).

Come si misurano le opinioni degli utenti e gli atteggiamenti verso i marchi o gli argomenti dei social network online, ad esempio post di Facebook, tweet, revisioni, ecc.? Le analisi dei sentimenti forniscono un metodo per l'analisi di queste domande.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

In genere esistono due metodi per l'analisi dei sentimenti. Viene utilizzato un algoritmo di apprendimento supervisionato e hello altri può essere considerato come apprendimento non supervisionato. Un algoritmo di apprendimento supervisionato crea in genere un modello di classificazione in base a una raccolta con annotazioni di grandi dimensioni. L'accuratezza si basa principalmente sulla qualità hello dell'annotazione hello e in genere il processo di training hello richiederà molto tempo. Oltre che, quando si applica dominio tooanother algoritmo hello hello risultato in genere non è valido. Confronto learning toosupervised, basata su dizionario di apprendimento non supervisionato utilizza un dizionario di valutazione, che non richiede l'archiviazione di una raccolta di dati di grandi dimensioni e formazione - rendendo hello intero processo molto più rapidamente. 

Il nostro [servizio](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) si basa su hello MPQA soggettività lessico (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), che è uno dei dizionari soggettività hello comunemente utilizzato. MPQA include 5097 parole negative e 2533 parole positive. Tutte queste parole sono annotate con polarità forte o debole. corpo intero Hello è sotto la licenza GNU General Public License. servizio web Hello può essere frasi breve tooany applicato, ad esempio TWEET e post di Facebook. 

> Questo servizio Web può essere utilizzato dagli utenti: potenzialmente tramite un'app mobile, un sito Web o anche in un computer locale, ad esempio. Ma scopo hello del servizio web hello anche tooserve come esempio di come Azure Machine Learning è possibile servizi web utilizzati toocreate su codice R. Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web. servizio web Hello può quindi essere pubblicata toohello Azure Marketplace e utilizzato da utenti e dispositivi attraverso HelloWorld con alcuna installazione dell'infrastruttura dall'autore hello del servizio web hello.
> 
> 

## <a name="consumption-of-web-service"></a>Uso del servizio Web
dati di input Hello possono essere qualsiasi testo, ma servizio web hello funziona meglio con frasi brevi. output di Hello è un valore numerico compreso tra -1 e 1. Qualsiasi valore inferiore a 0 indica che la valutazione hello del testo hello è negativa; Se positivo maggiore di 0. valore assoluto di Hello del risultato hello indica resistenza hello del sentiment hello associata. 

> Questo servizio, ospitato in Azure Marketplace, hello è un servizio OData. questi può essere chiamati tramite i metodi POST o GET. 
> 
> 

Esistono diversi modi di utilizzo di servizio hello in modo automatico (è un'app di esempio [qui](http://microsoftazuremachinelearning.azurewebsites.net/)).

### <a name="starting-c-code-for-web-service-consumption"></a>Codice C# iniziale per l'uso del servizio Web:
    public class ScoreResult
    {
            [DataMember]
            public double result
            {
                get;
                set;
            }
    }

    void main()
    {
            using (var wb = new WebClient())
            {
                var acitionUri = new Uri("PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score");
                DataServiceContext ctx = new DataServiceContext(acitionUri);
                var cred = new NetworkCredential("PutEmailAddressHere", "ChangeToAPIKey");
                var cache = new CredentialCache();

                cache.Add(acitionUri, "Basic", cred);
                ctx.Credentials = cache;
                var query = ctx.Execute<ScoreResult>(acitionUri, "POST", true, new BodyOperationParameter("Text", TextBox1.Text));
                ScoreResult scoreResult = query.ElementAt(0);
                double result = scoreResult.result;
            }
    }



input di Hello è "Oggi sono un buon giorno". output di Hello è "1", che indica una valutazione positiva ha associato frase di input hello. 

## <a name="creation-of-web-service"></a>Creazione del servizio Web
> Questo servizio Web è stato creato tramite Azure Machine Learning. Per una versione di prova gratuita e per video introduttivi sulla creazione di esperimenti e sulla [pubblicazione di servizi Web](machine-learning-publish-a-machine-learning-web-service.md), vedere [azure.com/ml](http://azure.com/ml). Di seguito è riportata una schermata dell'esperimento hello creato codice di esempio e servizio web hello per ciascuno dei moduli di hello all'interno di sperimentazione hello.
> 
> 

In Azure Machine Learning è stato creato un nuovo esperimento vuoto. Hello seguente figura flusso esperimento hello di analisi del sentiment basata su dizionario. file "sent_dict.csv" Hello lessico soggettività MPQA di hello e viene impostato su uno degli input hello di [Execute R Script][execute-r-script]. Un altro input è una revisione campionata da set di dati di hello Amazon revisione per test, in cui è eseguita la selezione, modificarne il nome di colonna e operazioni di divisione. Si utilizza una libreria di oggetti hash pacchetto toostore hello soggettività in memoria hello e accelerazione il processo di calcolo di hello punteggio. intero testo Hello verrà suddiviso in token dal pacchetto di "tm" e confrontato con la parola hello nel dizionario sentiment hello. Infine, un punteggio verrà calcolato aggiungendo il peso di hello di ogni parola soggettiva nel testo hello. 

### <a name="experiment-flow"></a>Flusso dell'esperimento
![flusso dell'esperimento][2]

#### <a name="module-1"></a>Modulo 1:
    # Map 1-based optional input ports toovariables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a>Installare un pacchetto di hash
    install.packages("src/hash_2.2.6.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("hash", lib.loc = ".", logical.return = TRUE, verbose = TRUE)
    library(tm)
    library(stringr)

    #create sentiment dictionary
    negation_word <- c("not","nor", "no")
    result <- c()
    sent_dict <- hash()
    sent_dict <- hash(sent_dict_data$word, sent_dict_data$polarity)

    #  Compute sentiment score for each document
    for (m in 1:nrow(dataset2)){
    polarity_ratio <- 0
    polarity_total <- 0
    not <- 0
    sentence <- tolower(dataset2[m,1])
    if (nchar(sentence) > 0){
        token_array <- scan_tokenizer(sentence)
        for (j in 1:length(token_array)){
            word = str_replace_all(token_array[j], "[^[:alnum:]]", "")
            for (k in 1:length(negation_word)){
              if (word == negation_word[k]){
                not <- (not+1) %% 2

              }
            }
            if (word != ""){
                if (!is.null(sent_dict[[word]])){
                  polarity_ratio <- polarity_ratio + (-2*not+1)*sent_dict[[word]]
                  polarity_total <- polarity_total + abs(sent_dict[[word]])
                }
            }

        }
    }
    if (polarity_total > 0){
        result <- c(result, polarity_ratio/polarity_total)
    }else{
        result<- c(result,0)
    }
    }

    # Sample operation
    data.set <- data.frame(result)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("data.set")



## <a name="limitations"></a>Limitazioni
Da una prospettiva di algoritmo, analisi del sentiment basata su dizionario sono uno strumento di analisi di valutazione generale, non è possibile ottenere prestazioni migliori rispetto al metodo di classificazione hello per campi specifici. problema di negazione Hello non è trattato anche. Nel programma sono codificate alcune parole di negazione, ma è consigliabile usare un dizionario di negazione e creare alcune regole. servizio web Hello garantisce prestazioni migliori in frasi breve e semplice, ad esempio TWEET e post di Facebook, rispetto a sulle frasi lunghe e complesse quali le recensioni Amazon. 

## <a name="faq"></a>domande frequenti
Per domande frequenti sull'utilizzo del servizio web hello o pubblicazione toohello Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


