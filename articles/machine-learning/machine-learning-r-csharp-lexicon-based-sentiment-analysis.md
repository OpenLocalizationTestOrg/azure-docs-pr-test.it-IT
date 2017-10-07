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
# <a name="deprecated-lexicon-based-sentiment-analysis"></a><span data-ttu-id="88c5b-103">(Deprecato) Analisi del sentiment basata sul lessico</span><span class="sxs-lookup"><span data-stu-id="88c5b-103">(deprecated) Lexicon Based Sentiment Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="88c5b-104">è stata ritirata Hello Microsoft DataMarket e questa API è stata deprecata.</span><span class="sxs-lookup"><span data-stu-id="88c5b-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="88c5b-105">Sono disponibili molte esperimenti di esempio utile e API hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="88c5b-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="88c5b-106">Per ulteriori informazioni sulla raccolta hello, vedere [condivisione e individuare le risorse in Cortana Intelligence Gallery hello](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="88c5b-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="88c5b-107">Come si misurano le opinioni degli utenti e gli atteggiamenti verso i marchi o gli argomenti dei social network online, ad esempio post di Facebook, tweet, revisioni, ecc.?</span><span class="sxs-lookup"><span data-stu-id="88c5b-107">How can you measure users’ opinions and attitudes toward brands or topics in online social networks, such as Facebook posts, tweets, reviews, etc.?</span></span> <span data-ttu-id="88c5b-108">Le analisi dei sentimenti forniscono un metodo per l'analisi di queste domande.</span><span class="sxs-lookup"><span data-stu-id="88c5b-108">Sentiment analysis provides a method for analyzing such questions.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="88c5b-109">In genere esistono due metodi per l'analisi dei sentimenti.</span><span class="sxs-lookup"><span data-stu-id="88c5b-109">There are generally two methods for sentiment analysis.</span></span> <span data-ttu-id="88c5b-110">Viene utilizzato un algoritmo di apprendimento supervisionato e hello altri può essere considerato come apprendimento non supervisionato.</span><span class="sxs-lookup"><span data-stu-id="88c5b-110">One is using a supervised learning algorithm, and hello other can be treated as unsupervised learning.</span></span> <span data-ttu-id="88c5b-111">Un algoritmo di apprendimento supervisionato crea in genere un modello di classificazione in base a una raccolta con annotazioni di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="88c5b-111">A supervised learning algorithm generally builds a classification model on a large annotated corpus.</span></span> <span data-ttu-id="88c5b-112">L'accuratezza si basa principalmente sulla qualità hello dell'annotazione hello e in genere il processo di training hello richiederà molto tempo.</span><span class="sxs-lookup"><span data-stu-id="88c5b-112">Its accuracy is mainly based on hello quality of hello annotation, and usually hello training process will take a long time.</span></span> <span data-ttu-id="88c5b-113">Oltre che, quando si applica dominio tooanother algoritmo hello hello risultato in genere non è valido.</span><span class="sxs-lookup"><span data-stu-id="88c5b-113">Besides that, when we apply hello algorithm tooanother domain, hello result is usually not good.</span></span> <span data-ttu-id="88c5b-114">Confronto learning toosupervised, basata su dizionario di apprendimento non supervisionato utilizza un dizionario di valutazione, che non richiede l'archiviazione di una raccolta di dati di grandi dimensioni e formazione - rendendo hello intero processo molto più rapidamente.</span><span class="sxs-lookup"><span data-stu-id="88c5b-114">Compared toosupervised learning, lexicon-based unsupervised learning uses a sentiment dictionary, which doesn’t require storing a large data corpus and training - which makes hello whole process much faster.</span></span> 

<span data-ttu-id="88c5b-115">Il nostro [servizio](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) si basa su hello MPQA soggettività lessico (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), che è uno dei dizionari soggettività hello comunemente utilizzato.</span><span class="sxs-lookup"><span data-stu-id="88c5b-115">Our [service](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) is built on hello MPQA Subjectivity Lexicon (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), which is one of hello most commonly used subjectivity lexicons.</span></span> <span data-ttu-id="88c5b-116">MPQA include 5097 parole negative e 2533 parole positive.</span><span class="sxs-lookup"><span data-stu-id="88c5b-116">There are 5097 negative and 2533 positive words in MPQA.</span></span> <span data-ttu-id="88c5b-117">Tutte queste parole sono annotate con polarità forte o debole.</span><span class="sxs-lookup"><span data-stu-id="88c5b-117">And all of these words are annotated as strong or weak polarity.</span></span> <span data-ttu-id="88c5b-118">corpo intero Hello è sotto la licenza GNU General Public License.</span><span class="sxs-lookup"><span data-stu-id="88c5b-118">hello whole corpus is under GNU General Public License.</span></span> <span data-ttu-id="88c5b-119">servizio web Hello può essere frasi breve tooany applicato, ad esempio TWEET e post di Facebook.</span><span class="sxs-lookup"><span data-stu-id="88c5b-119">hello web service can be applied tooany short sentences, such as tweets and Facebook posts.</span></span> 

> <span data-ttu-id="88c5b-120">Questo servizio Web può essere utilizzato dagli utenti: potenzialmente tramite un'app mobile, un sito Web o anche in un computer locale, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="88c5b-120">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer for example.</span></span> <span data-ttu-id="88c5b-121">Ma scopo hello del servizio web hello anche tooserve come esempio di come Azure Machine Learning è possibile servizi web utilizzati toocreate su codice R.</span><span class="sxs-lookup"><span data-stu-id="88c5b-121">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="88c5b-122">Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="88c5b-122">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="88c5b-123">servizio web Hello può quindi essere pubblicata toohello Azure Marketplace e utilizzato da utenti e dispositivi attraverso HelloWorld con alcuna installazione dell'infrastruttura dall'autore hello del servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="88c5b-123">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="88c5b-124">Uso del servizio Web</span><span class="sxs-lookup"><span data-stu-id="88c5b-124">Consumption of web service</span></span>
<span data-ttu-id="88c5b-125">dati di input Hello possono essere qualsiasi testo, ma servizio web hello funziona meglio con frasi brevi.</span><span class="sxs-lookup"><span data-stu-id="88c5b-125">hello input data can be any text, but hello web service works better with short sentences.</span></span> <span data-ttu-id="88c5b-126">output di Hello è un valore numerico compreso tra -1 e 1.</span><span class="sxs-lookup"><span data-stu-id="88c5b-126">hello output is a numeric value between -1 and 1.</span></span> <span data-ttu-id="88c5b-127">Qualsiasi valore inferiore a 0 indica che la valutazione hello del testo hello è negativa; Se positivo maggiore di 0.</span><span class="sxs-lookup"><span data-stu-id="88c5b-127">Any value below 0 denotes that hello sentiment of hello text is negative; positive if above 0.</span></span> <span data-ttu-id="88c5b-128">valore assoluto di Hello del risultato hello indica resistenza hello del sentiment hello associata.</span><span class="sxs-lookup"><span data-stu-id="88c5b-128">hello absolute value of hello result denotes hello strength of hello associated sentiment.</span></span> 

> <span data-ttu-id="88c5b-129">Questo servizio, ospitato in Azure Marketplace, hello è un servizio OData. questi può essere chiamati tramite i metodi POST o GET.</span><span class="sxs-lookup"><span data-stu-id="88c5b-129">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="88c5b-130">Esistono diversi modi di utilizzo di servizio hello in modo automatico (è un'app di esempio [qui](http://microsoftazuremachinelearning.azurewebsites.net/)).</span><span class="sxs-lookup"><span data-stu-id="88c5b-130">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="88c5b-131">Codice C# iniziale per l'uso del servizio Web:</span><span class="sxs-lookup"><span data-stu-id="88c5b-131">Starting C# code for web service consumption:</span></span>
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



<span data-ttu-id="88c5b-132">input di Hello è "Oggi sono un buon giorno".</span><span class="sxs-lookup"><span data-stu-id="88c5b-132">hello input is “Today is a good day.”</span></span> <span data-ttu-id="88c5b-133">output di Hello è "1", che indica una valutazione positiva ha associato frase di input hello.</span><span class="sxs-lookup"><span data-stu-id="88c5b-133">hello output is “1”, which indicates a positive sentiment associated with hello input sentence.</span></span> 

## <a name="creation-of-web-service"></a><span data-ttu-id="88c5b-134">Creazione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="88c5b-134">Creation of web service</span></span>
> <span data-ttu-id="88c5b-135">Questo servizio Web è stato creato tramite Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="88c5b-135">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="88c5b-136">Per una versione di prova gratuita e per video introduttivi sulla creazione di esperimenti e sulla [pubblicazione di servizi Web](machine-learning-publish-a-machine-learning-web-service.md), vedere [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="88c5b-136">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="88c5b-137">Di seguito è riportata una schermata dell'esperimento hello creato codice di esempio e servizio web hello per ciascuno dei moduli di hello all'interno di sperimentazione hello.</span><span class="sxs-lookup"><span data-stu-id="88c5b-137">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="88c5b-138">In Azure Machine Learning è stato creato un nuovo esperimento vuoto.</span><span class="sxs-lookup"><span data-stu-id="88c5b-138">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="88c5b-139">Hello seguente figura flusso esperimento hello di analisi del sentiment basata su dizionario.</span><span class="sxs-lookup"><span data-stu-id="88c5b-139">hello figure below shows hello experiment flow of lexicon-based sentiment analysis.</span></span> <span data-ttu-id="88c5b-140">file "sent_dict.csv" Hello lessico soggettività MPQA di hello e viene impostato su uno degli input hello di [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="88c5b-140">hello “sent_dict.csv” file is hello MPQA subjectivity lexicon, and is set as one of hello inputs of [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="88c5b-141">Un altro input è una revisione campionata da set di dati di hello Amazon revisione per test, in cui è eseguita la selezione, modificarne il nome di colonna e operazioni di divisione.</span><span class="sxs-lookup"><span data-stu-id="88c5b-141">Another input is a sampled review from hello Amazon review dataset for test, where we performed selection, column name modification, and split operations.</span></span> <span data-ttu-id="88c5b-142">Si utilizza una libreria di oggetti hash pacchetto toostore hello soggettività in memoria hello e accelerazione il processo di calcolo di hello punteggio.</span><span class="sxs-lookup"><span data-stu-id="88c5b-142">We use a hash package toostore hello subjectivity lexicon in hello memory and accelerate hello score computation process.</span></span> <span data-ttu-id="88c5b-143">intero testo Hello verrà suddiviso in token dal pacchetto di "tm" e confrontato con la parola hello nel dizionario sentiment hello.</span><span class="sxs-lookup"><span data-stu-id="88c5b-143">hello whole text will be tokenized by “tm” package and compared with hello word in hello sentiment dictionary.</span></span> <span data-ttu-id="88c5b-144">Infine, un punteggio verrà calcolato aggiungendo il peso di hello di ogni parola soggettiva nel testo hello.</span><span class="sxs-lookup"><span data-stu-id="88c5b-144">Finally, a score will be calculated by adding hello weight of each subjective word in hello text.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="88c5b-145">Flusso dell'esperimento</span><span class="sxs-lookup"><span data-stu-id="88c5b-145">Experiment flow:</span></span>
![flusso dell'esperimento][2]

#### <a name="module-1"></a><span data-ttu-id="88c5b-147">Modulo 1:</span><span class="sxs-lookup"><span data-stu-id="88c5b-147">Module 1:</span></span>
    # Map 1-based optional input ports toovariables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a><span data-ttu-id="88c5b-148">Installare un pacchetto di hash</span><span class="sxs-lookup"><span data-stu-id="88c5b-148">Install hash package</span></span>
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



## <a name="limitations"></a><span data-ttu-id="88c5b-149">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="88c5b-149">Limitations</span></span>
<span data-ttu-id="88c5b-150">Da una prospettiva di algoritmo, analisi del sentiment basata su dizionario sono uno strumento di analisi di valutazione generale, non è possibile ottenere prestazioni migliori rispetto al metodo di classificazione hello per campi specifici.</span><span class="sxs-lookup"><span data-stu-id="88c5b-150">From an algorithm perspective, lexicon-based sentiment analysis is a general sentiment analysis tool, which may not perform better than hello classification method for specific fields.</span></span> <span data-ttu-id="88c5b-151">problema di negazione Hello non è trattato anche.</span><span class="sxs-lookup"><span data-stu-id="88c5b-151">hello negation problem is not well dealt with.</span></span> <span data-ttu-id="88c5b-152">Nel programma sono codificate alcune parole di negazione, ma è consigliabile usare un dizionario di negazione e creare alcune regole.</span><span class="sxs-lookup"><span data-stu-id="88c5b-152">We hardcode several negation words in our program, but a better way is using a negation dictionary and build some rules.</span></span> <span data-ttu-id="88c5b-153">servizio web Hello garantisce prestazioni migliori in frasi breve e semplice, ad esempio TWEET e post di Facebook, rispetto a sulle frasi lunghe e complesse quali le recensioni Amazon.</span><span class="sxs-lookup"><span data-stu-id="88c5b-153">hello web service performs better on short and simple sentences, such as tweets and Facebook posts, than on long and complex sentences such as Amazon reviews.</span></span> 

## <a name="faq"></a><span data-ttu-id="88c5b-154">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="88c5b-154">FAQ</span></span>
<span data-ttu-id="88c5b-155">Per domande frequenti sull'utilizzo del servizio web hello o pubblicazione toohello Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="88c5b-155">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


