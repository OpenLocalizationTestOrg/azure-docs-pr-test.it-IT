---
title: (Deprecato) Modello di cluster - Azure | Documentazione Microsoft
description: (Deprecato) Modello di cluster
services: machine-learning
documentationcenter: 
author: FrancescaLazzeri
manager: jhubbard
editor: cgronlun
ms.assetid: 51b8d012-ed44-4312-920c-9c808dfd4ff6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: lazzeri
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 7cbbbd6d4236dab638eb3051595a584557480841
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-cluster-model"></a><span data-ttu-id="814b8-103">(Deprecato) Modello di cluster</span><span class="sxs-lookup"><span data-stu-id="814b8-103">(deprecated) Cluster Model</span></span>

> [!NOTE]
> <span data-ttu-id="814b8-104">Microsoft DataMarket è in fase di ritiro e questa API è stata deprecata.</span><span class="sxs-lookup"><span data-stu-id="814b8-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="814b8-105">Numerose API e molti esperimenti utili di esempio sono disponibili in [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="814b8-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="814b8-106">Per altre informazioni sulla raccolta, vedere [Condividere e scoprire risorse in Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="814b8-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="814b8-107">In che modo si può prevedere il comportamento di gruppi di titolari di carte di credito, per ridurre gli addebiti relativi ai rischi per le autorità emittenti di carte di credito?</span><span class="sxs-lookup"><span data-stu-id="814b8-107">How can we predict groups of credit cardholders’ behaviors in order to reduce the charge-off risk of credit card issuers?</span></span> <span data-ttu-id="814b8-108">In che modo è possibile definire gruppi di aspetti della personalità dei dipendenti per migliorarne le prestazioni lavorative?</span><span class="sxs-lookup"><span data-stu-id="814b8-108">How can we define groups of personality traits of employees in order to improve their performance at work?</span></span> <span data-ttu-id="814b8-109">In che modo i medici possono classificare i pazienti, suddividendoli in gruppi in base alle caratteristiche delle patologie?</span><span class="sxs-lookup"><span data-stu-id="814b8-109">How can doctors classify patients into groups based on the characteristics of their diseases?</span></span> <span data-ttu-id="814b8-110">Teoricamente, è possibile rispondere a tutte queste domande tramite l'analisi dei cluster.</span><span class="sxs-lookup"><span data-stu-id="814b8-110">In principle, all of these questions can be answered through cluster analysis.</span></span>   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="814b8-111">In pratica, l'analisi dei cluster classifica un set di osservazioni in due o più gruppi sconosciuti che si escludono a vicenda in base a una combinazione di variabili.</span><span class="sxs-lookup"><span data-stu-id="814b8-111">Cluster analysis classifies a set of observations into two or more mutually exclusive unknown groups based on combinations of variables.</span></span> <span data-ttu-id="814b8-112">La finalità dell'analisi dei cluster consiste nell'individuare un sistema appropriato per organizzare le osservazioni, in genere relative a persone o alle rispettive caratteristiche, suddividendole in gruppi, in modo che i membri dei gruppi condividano proprietà comuni.</span><span class="sxs-lookup"><span data-stu-id="814b8-112">The purpose of cluster analysis is to discover a system of organizing observations, usually people or their characteristics, into groups, where members of the groups share properties in common.</span></span> <span data-ttu-id="814b8-113">Questo [servizio](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) usa la metodologia K-Means, una tecnica di clustering comunemente usata per raggruppare dati arbitrari.</span><span class="sxs-lookup"><span data-stu-id="814b8-113">This [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) uses the K-Means methodology, a commonly used clustering technique, to cluster arbitrary data into groups.</span></span> <span data-ttu-id="814b8-114">Questo servizio Web accetta i dati e il numero di cluster k come input e produce previsioni relative all'appartenenza delle osservazioni a uno dei gruppi  k.</span><span class="sxs-lookup"><span data-stu-id="814b8-114">This web service takes the data and the number of k clusters as input, and produces predictions of which of the k groups to which each observations belongs.</span></span> 

> <span data-ttu-id="814b8-115">Questo servizio Web può essere utilizzato dagli utenti: potenzialmente tramite un'app mobile, un sito Web o anche in un computer locale, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="814b8-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="814b8-116">Ma lo scopo del servizio Web è anche fornire un esempio di come è possibile utilizzare Azure Machine Learning per creare servizi Web in codice R.</span><span class="sxs-lookup"><span data-stu-id="814b8-116">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="814b8-117">Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="814b8-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="814b8-118">Il servizio Web può essere quindi pubblicato in Azure Marketplace e può essere usato da utenti e dispositivi in tutto il mondo, senza che l'autore del servizio Web debba configurare alcuna infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="814b8-118">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="814b8-119">Uso del servizio Web</span><span class="sxs-lookup"><span data-stu-id="814b8-119">Consumption of web service</span></span>
<span data-ttu-id="814b8-120">Questo servizio Web raggruppa i dati in un set di k gruppi e fornisce come output l'assegnazione ai gruppi per ogni riga.</span><span class="sxs-lookup"><span data-stu-id="814b8-120">This web service groups the data into a set of k groups and outputs the group assignment for each row.</span></span> <span data-ttu-id="814b8-121">Il servizio Web richiede che l'utente finale immetta i dati come una stringa in cui le righe sono separate da virgola (,) e le colonne sono separate da punto e virgola (;).</span><span class="sxs-lookup"><span data-stu-id="814b8-121">The web service expects the end user to input data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="814b8-122">Il servizio Web richiede l'immissione di una riga alla volta.</span><span class="sxs-lookup"><span data-stu-id="814b8-122">The web service expects 1 row at a time.</span></span> <span data-ttu-id="814b8-123">Un set di dati di esempio può avere un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="814b8-123">An example dataset could look like this:</span></span>

![Dati di esempio][1]

<span data-ttu-id="814b8-125">Si supponga che l'utente voglia separare questi dati in tre gruppi che si escludono a vicenda.</span><span class="sxs-lookup"><span data-stu-id="814b8-125">Suppose the user wanted to separate this data into 3 mutually exclusive groups.</span></span> <span data-ttu-id="814b8-126">L'input di dati per il set di dati precedente sarebbe analogo al seguente: valore = “10;5;2,18;1;6,7;5;5,22;3;4,12;2;1,10;3;4”; k=”3”.</span><span class="sxs-lookup"><span data-stu-id="814b8-126">The data input for the above dataset would be the following: value = “10;5;2,18;1;6,7;5;5,22;3;4,12;2;1,10;3;4”; k=”3”.</span></span> <span data-ttu-id="814b8-127">L'output corrisponde all'appartenenza prevista ai gruppi per ogni riga.</span><span class="sxs-lookup"><span data-stu-id="814b8-127">The output is the predicted group membership for each of the rows.</span></span>

> <span data-ttu-id="814b8-128">Questo servizio, come ospitato in Azure Marketplace, è un servizio OData ed è possibile utilizzare i metodi POST o GET per effettuare le chiamate.</span><span class="sxs-lookup"><span data-stu-id="814b8-128">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="814b8-129">Sono disponibili molte opzioni per l'uso del servizio in modalità automatica. Per un'app di esempio, vedere [qui](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx).</span><span class="sxs-lookup"><span data-stu-id="814b8-129">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="814b8-130">Codice C# iniziale per l'uso del servizio Web:</span><span class="sxs-lookup"><span data-stu-id="814b8-130">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string value;
            public string k;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text, k = TextBox2.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




## <a name="creation-of-web-service"></a><span data-ttu-id="814b8-131">Creazione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="814b8-131">Creation of web service</span></span>
> <span data-ttu-id="814b8-132">Questo servizio Web è stato creato tramite Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="814b8-132">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="814b8-133">Per una versione di prova gratuita e per video introduttivi sulla creazione di esperimenti e sulla [pubblicazione di servizi Web](machine-learning-publish-a-machine-learning-web-service.md), vedere [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="814b8-133">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="814b8-134">La schermata seguente mostra un esperimento per la creazione del servizio Web e codice di esempio per ogni modulo incluso nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="814b8-134">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="814b8-135">In Azure Machine Learning è stato creato un nuovo esperimento vuoto e due moduli [Execute R Script][execute-r-script] sono stati inseriti nell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="814b8-135">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto the workspace.</span></span> <span data-ttu-id="814b8-136">Lo schema di dati è stato creato con un semplice modello [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="814b8-136">The data schema was created with a simple [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="814b8-137">In seguito, è stato collegato alla sezione del modello di cluster, creato a sua volta con un modulo [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="814b8-137">Then, the data schema was linked to the cluster model section, again created with an [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="814b8-138">Nel modulo [Execute R Script][execute-r-script] usato per il modello di cluster, il servizio Web usa quindi la funzione "k-means", incorporata in [Execute R Script][execute-r-script] di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="814b8-138">In the [Execute R Script][execute-r-script] used for the cluster model, the web service then utilizes the “k-means” function, which is prebuilt into the [Execute R Script][execute-r-script] of Azure Machine Learning.</span></span>    

![Flusso dell'esperimento][3]

#### <a name="module-1"></a><span data-ttu-id="814b8-140">Modulo 1:</span><span class="sxs-lookup"><span data-stu-id="814b8-140">Module 1:</span></span>
    #Enter the input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a><span data-ttu-id="814b8-141">Modulo 2:</span><span class="sxs-lookup"><span data-stu-id="814b8-141">Module 2:</span></span>
    # Map 1-based optional input ports to variables
    mydata <- maml.mapInputPort(1) # class: data.frame

    data.split <- strsplit(mydata[1,1], ",")[[1]]
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- as.data.frame(t(data.split))

    data.split <- data.matrix(data.split)
    data.split <- data.frame(data.split)

    # K-Means cluster analysis
    fit <- kmeans(data.split, mydata$k) # k-cluster solution

    # Get cluster means 
    aggregate(data.split,by=list(fit$cluster),FUN=mean)
    # Append cluster assignment
    mydatafinal <- data.frame(t(fit$cluster))
    n_col=ncol(mydatafinal)
    colnames(mydatafinal) <- paste("V",1:n_col,sep="")

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("mydatafinal");


## <a name="limitations"></a><span data-ttu-id="814b8-142">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="814b8-142">Limitations</span></span>
<span data-ttu-id="814b8-143">Questo è un esempio molto semplice di un servizio Web di clustering.</span><span class="sxs-lookup"><span data-stu-id="814b8-143">This is a very simple example of a clustering web service.</span></span> <span data-ttu-id="814b8-144">Come si può notare nell'esempio di codice precedente, il rilevamento degli errori non è implementato e il servizio presuppone che qualsiasi elemento sia una variabile continua (non sono consentite funzionalità categoriche), poiché il servizio immette come input solo valori numerici al momento della creazione del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="814b8-144">As can be seen from the example code above, no error catching is implemented and the service assumes everything is a continuous variable (no categorical features allowed), as the service only inputs numeric values at the time of the creation of this web service.</span></span> <span data-ttu-id="814b8-145">Il servizio, inoltre, gestisce attualmente dimensioni limitate di dati a causa della natura di richiesta/risposta della chiamata del servizio Web e del fatto che il modello viene definito ogni volta che il servizio Web viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="814b8-145">Also, the service currently handles limited data size, due to the request/response nature of the web service call and the fact that the model is being fit every time the web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="814b8-146">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="814b8-146">FAQ</span></span>
<span data-ttu-id="814b8-147">Per le domande frequenti relative all'uso del servizio Web o alla pubblicazione in Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="814b8-147">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

