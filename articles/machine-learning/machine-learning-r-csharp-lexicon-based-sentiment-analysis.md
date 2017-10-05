---
title: (Deprecato) Analisi del sentiment basata sul lessico - Azure | Documentazione Microsoft
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
redirect_document_id: TRUE
ms.openlocfilehash: 7bc80a1e1067296528eca1a843ea30b0c27af616
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-lexicon-based-sentiment-analysis"></a><span data-ttu-id="f2fdb-103">(Deprecato) Analisi del sentiment basata sul lessico</span><span class="sxs-lookup"><span data-stu-id="f2fdb-103">(deprecated) Lexicon Based Sentiment Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="f2fdb-104">Microsoft DataMarket è in fase di ritiro e questa API è stata deprecata.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="f2fdb-105">Numerose API e molti esperimenti utili di esempio sono disponibili in [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="f2fdb-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="f2fdb-106">Per altre informazioni sulla raccolta, vedere [Condividere e scoprire risorse in Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="f2fdb-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="f2fdb-107">Come si misurano le opinioni degli utenti e gli atteggiamenti verso i marchi o gli argomenti dei social network online, ad esempio post di Facebook, tweet, revisioni, ecc.?</span><span class="sxs-lookup"><span data-stu-id="f2fdb-107">How can you measure users’ opinions and attitudes toward brands or topics in online social networks, such as Facebook posts, tweets, reviews, etc.?</span></span> <span data-ttu-id="f2fdb-108">Le analisi dei sentimenti forniscono un metodo per l'analisi di queste domande.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-108">Sentiment analysis provides a method for analyzing such questions.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="f2fdb-109">In genere esistono due metodi per l'analisi dei sentimenti.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-109">There are generally two methods for sentiment analysis.</span></span> <span data-ttu-id="f2fdb-110">Uno consiste nell'utilizzare un algoritmo di apprendimento supervisionato e l'altro può essere considerato come un apprendimento senza supervisione.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-110">One is using a supervised learning algorithm, and the other can be treated as unsupervised learning.</span></span> <span data-ttu-id="f2fdb-111">Un algoritmo di apprendimento supervisionato crea in genere un modello di classificazione in base a una raccolta con annotazioni di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-111">A supervised learning algorithm generally builds a classification model on a large annotated corpus.</span></span> <span data-ttu-id="f2fdb-112">La precisione si basa principalmente sulla qualità dell'annotazione e in genere il processo di training richiede molto tempo.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-112">Its accuracy is mainly based on the quality of the annotation, and usually the training process will take a long time.</span></span> <span data-ttu-id="f2fdb-113">Quando si applica l'algoritmo a un altro dominio, inoltre, i risultati non sono in genere validi.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-113">Besides that, when we apply the algorithm to another domain, the result is usually not good.</span></span> <span data-ttu-id="f2fdb-114">Rispetto all'apprendimento supervisionato, l'apprendimento non supervisionato basato sul lessico usa un dizionario di sentimenti, che non richiede l'archiviazione di un corpus di dati di grandi dimensioni e non necessita di training. Il processo risulta quindi molto più veloce.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-114">Compared to supervised learning, lexicon-based unsupervised learning uses a sentiment dictionary, which doesn’t require storing a large data corpus and training - which makes the whole process much faster.</span></span> 

<span data-ttu-id="f2fdb-115">Questo [servizio](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) è basato sul lessico di soggettività MPQA (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), che è uno dei lessici di soggettività più usati.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-115">Our [service](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) is built on the MPQA Subjectivity Lexicon (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), which is one of the most commonly used subjectivity lexicons.</span></span> <span data-ttu-id="f2fdb-116">MPQA include 5097 parole negative e 2533 parole positive.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-116">There are 5097 negative and 2533 positive words in MPQA.</span></span> <span data-ttu-id="f2fdb-117">Tutte queste parole sono annotate con polarità forte o debole.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-117">And all of these words are annotated as strong or weak polarity.</span></span> <span data-ttu-id="f2fdb-118">L'intero corpus è disponibile con la licenza pubblica generale GNU.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-118">The whole corpus is under GNU General Public License.</span></span> <span data-ttu-id="f2fdb-119">Il servizio Web può essere applicato a qualsiasi frase breve, ad esempio tweet, post di Facebook e così via.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-119">The web service can be applied to any short sentences, such as tweets and Facebook posts.</span></span> 

> <span data-ttu-id="f2fdb-120">Questo servizio Web può essere utilizzato dagli utenti: potenzialmente tramite un'app mobile, un sito Web o anche in un computer locale, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-120">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer for example.</span></span> <span data-ttu-id="f2fdb-121">Ma lo scopo del servizio Web è anche fornire un esempio di come è possibile utilizzare Azure Machine Learning per creare servizi Web in codice R.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-121">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="f2fdb-122">Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-122">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="f2fdb-123">Il servizio Web può essere quindi pubblicato in Azure Marketplace e può essere usato da utenti e dispositivi in tutto il mondo, senza che l'autore del servizio Web debba configurare alcuna infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-123">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="f2fdb-124">Uso del servizio Web</span><span class="sxs-lookup"><span data-stu-id="f2fdb-124">Consumption of web service</span></span>
<span data-ttu-id="f2fdb-125">Come dati di input è possibile usare qualsiasi testo, ma il servizio funziona in modo ottimale con frasi brevi.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-125">The input data can be any text, but the web service works better with short sentences.</span></span> <span data-ttu-id="f2fdb-126">L'output è un valore numerico compreso tra -1 e 1.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-126">The output is a numeric value between -1 and 1.</span></span> <span data-ttu-id="f2fdb-127">Qualsiasi valore inferiore a 0 indica che il sentimento del testo è negativo; mentre un valore maggiore di 0 indica che è positivo.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-127">Any value below 0 denotes that the sentiment of the text is negative; positive if above 0.</span></span> <span data-ttu-id="f2fdb-128">Il valore assoluto del risultato indica il livello di attendibilità del sentimento associato.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-128">The absolute value of the result denotes the strength of the associated sentiment.</span></span> 

> <span data-ttu-id="f2fdb-129">Questo servizio, come ospitato in Azure Marketplace, è un servizio OData ed è possibile utilizzare i metodi POST o GET per effettuare le chiamate.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-129">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="f2fdb-130">Sono disponibili molte opzioni per l'uso del servizio in modalità automatica. Per un'app di esempio, vedere [qui](http://microsoftazuremachinelearning.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="f2fdb-130">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="f2fdb-131">Codice C# iniziale per l'uso del servizio Web:</span><span class="sxs-lookup"><span data-stu-id="f2fdb-131">Starting C# code for web service consumption:</span></span>
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



<span data-ttu-id="f2fdb-132">L'input è "Oggi è un buon giorno".</span><span class="sxs-lookup"><span data-stu-id="f2fdb-132">The input is “Today is a good day.”</span></span> <span data-ttu-id="f2fdb-133">L'output è "1", che indica un sentimento positivo associato alla frase di input.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-133">The output is “1”, which indicates a positive sentiment associated with the input sentence.</span></span> 

## <a name="creation-of-web-service"></a><span data-ttu-id="f2fdb-134">Creazione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="f2fdb-134">Creation of web service</span></span>
> <span data-ttu-id="f2fdb-135">Questo servizio Web è stato creato tramite Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-135">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="f2fdb-136">Per una versione di prova gratuita e per video introduttivi sulla creazione di esperimenti e sulla [pubblicazione di servizi Web](machine-learning-publish-a-machine-learning-web-service.md), vedere [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="f2fdb-136">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="f2fdb-137">La schermata seguente mostra un esperimento per la creazione del servizio Web e codice di esempio per ogni modulo incluso nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-137">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="f2fdb-138">In Azure Machine Learning è stato creato un nuovo esperimento vuoto.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-138">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="f2fdb-139">La figura seguente mostra il flusso dell'esperimento di un'analisi del sentimento basata sul lessico.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-139">The figure below shows the experiment flow of lexicon-based sentiment analysis.</span></span> <span data-ttu-id="f2fdb-140">Il file "sent_dict.csv" è il lessico di soggettività MPQA ed è configurato come uno degli input di [Execute R Script][execute-r-script] (Esegui script R).</span><span class="sxs-lookup"><span data-stu-id="f2fdb-140">The “sent_dict.csv” file is the MPQA subjectivity lexicon, and is set as one of the inputs of [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="f2fdb-141">Un altro input è costituito da una revisione campionata dal set di dati di revisioni Amazon per la verifica, in cui sono state eseguite operazioni di selezione, modifica del nome di colonna e suddivisione.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-141">Another input is a sampled review from the Amazon review dataset for test, where we performed selection, column name modification, and split operations.</span></span> <span data-ttu-id="f2fdb-142">Un pacchetto di hash viene usato per archiviare il lessico di soggettività in memoria e accelerare il processo di calcolo del punteggio.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-142">We use a hash package to store the subjectivity lexicon in the memory and accelerate the score computation process.</span></span> <span data-ttu-id="f2fdb-143">L'intero testo verrà suddiviso in token dal pacchetto "tm" e verrà confrontato con le parole disponibili nel dizionario di sentiment.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-143">The whole text will be tokenized by “tm” package and compared with the word in the sentiment dictionary.</span></span> <span data-ttu-id="f2fdb-144">Verrà infine calcolato un punteggio tramite la somma dei pesi di ogni parola soggettiva nel testo.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-144">Finally, a score will be calculated by adding the weight of each subjective word in the text.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="f2fdb-145">Flusso dell'esperimento</span><span class="sxs-lookup"><span data-stu-id="f2fdb-145">Experiment flow:</span></span>
![flusso dell'esperimento][2]

#### <a name="module-1"></a><span data-ttu-id="f2fdb-147">Modulo 1:</span><span class="sxs-lookup"><span data-stu-id="f2fdb-147">Module 1:</span></span>
    # Map 1-based optional input ports to variables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a><span data-ttu-id="f2fdb-148">Installare un pacchetto di hash</span><span class="sxs-lookup"><span data-stu-id="f2fdb-148">Install hash package</span></span>
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

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("data.set")



## <a name="limitations"></a><span data-ttu-id="f2fdb-149">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="f2fdb-149">Limitations</span></span>
<span data-ttu-id="f2fdb-150">Dal punto di vista dell'algoritmo, l'analisi dei sentimenti basata sul lessico è uno strumento generale per l'analisi dei sentimenti ed è possibile che non offra prestazioni migliori rispetto al metodo di classificazione per campi specifici.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-150">From an algorithm perspective, lexicon-based sentiment analysis is a general sentiment analysis tool, which may not perform better than the classification method for specific fields.</span></span> <span data-ttu-id="f2fdb-151">Il problema relativo alla negazione non viene affrontato.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-151">The negation problem is not well dealt with.</span></span> <span data-ttu-id="f2fdb-152">Nel programma sono codificate alcune parole di negazione, ma è consigliabile usare un dizionario di negazione e creare alcune regole.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-152">We hardcode several negation words in our program, but a better way is using a negation dictionary and build some rules.</span></span> <span data-ttu-id="f2fdb-153">Il servizio Web offre prestazioni migliori per frasi brevi e semplici quali tweet e post di Facebook rispetto a frasi lunghe e complesse come quelle delle revisioni di Amazon.</span><span class="sxs-lookup"><span data-stu-id="f2fdb-153">The web service performs better on short and simple sentences, such as tweets and Facebook posts, than on long and complex sentences such as Amazon reviews.</span></span> 

## <a name="faq"></a><span data-ttu-id="f2fdb-154">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="f2fdb-154">FAQ</span></span>
<span data-ttu-id="f2fdb-155">Per le domande frequenti relative all'uso del servizio Web o alla pubblicazione in Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="f2fdb-155">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


