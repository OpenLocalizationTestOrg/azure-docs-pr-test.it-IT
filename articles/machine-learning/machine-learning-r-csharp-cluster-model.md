---
title: AAA(deprecated) - modello di Cluster di Azure | Documenti Microsoft
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
redirect_document_id: True
ms.openlocfilehash: 7b2dffb855a8d91114752b579115e97d07210e45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-cluster-model"></a><span data-ttu-id="13dce-103">(Deprecato) Modello di cluster</span><span class="sxs-lookup"><span data-stu-id="13dce-103">(deprecated) Cluster Model</span></span>

> [!NOTE]
> <span data-ttu-id="13dce-104">è stata ritirata Hello Microsoft DataMarket e questa API è stata deprecata.</span><span class="sxs-lookup"><span data-stu-id="13dce-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="13dce-105">Sono disponibili molte esperimenti di esempio utile e API hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="13dce-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="13dce-106">Per ulteriori informazioni sulla raccolta hello, vedere [condivisione e individuare le risorse in Cortana Intelligence Gallery hello](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="13dce-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="13dce-107">Come è possibile stimare gruppi dei comportamenti dei titolari di carta di credito in ordine tooreduce hello ammortamento rischio di autorità emittenti di carta di credito?</span><span class="sxs-lookup"><span data-stu-id="13dce-107">How can we predict groups of credit cardholders’ behaviors in order tooreduce hello charge-off risk of credit card issuers?</span></span> <span data-ttu-id="13dce-108">Come possiamo è definire gruppi di tratti dalla personalità dei dipendenti in ordine tooimprove delle relative prestazioni al lavoro?</span><span class="sxs-lookup"><span data-stu-id="13dce-108">How can we define groups of personality traits of employees in order tooimprove their performance at work?</span></span> <span data-ttu-id="13dce-109">Come possono medici classificare i pazienti in gruppi in base alle caratteristiche di hello della loro diseases?</span><span class="sxs-lookup"><span data-stu-id="13dce-109">How can doctors classify patients into groups based on hello characteristics of their diseases?</span></span> <span data-ttu-id="13dce-110">Teoricamente, è possibile rispondere a tutte queste domande tramite l'analisi dei cluster.</span><span class="sxs-lookup"><span data-stu-id="13dce-110">In principle, all of these questions can be answered through cluster analysis.</span></span>   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="13dce-111">In pratica, l'analisi dei cluster classifica un set di osservazioni in due o più gruppi sconosciuti che si escludono a vicenda in base a una combinazione di variabili.</span><span class="sxs-lookup"><span data-stu-id="13dce-111">Cluster analysis classifies a set of observations into two or more mutually exclusive unknown groups based on combinations of variables.</span></span> <span data-ttu-id="13dce-112">scopo di Hello dell'analisi del cluster è toodiscover un sistema di organizzare le osservazioni, in genere gli utenti o le caratteristiche, in gruppi, in cui i membri dei gruppi di hello condividono le proprietà.</span><span class="sxs-lookup"><span data-stu-id="13dce-112">hello purpose of cluster analysis is toodiscover a system of organizing observations, usually people or their characteristics, into groups, where members of hello groups share properties in common.</span></span> <span data-ttu-id="13dce-113">Questo [servizio](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) utilizza hello metodologia K-medie, una tecnica di clustering utilizzata frequentemente, toocluster dati arbitrari in gruppi.</span><span class="sxs-lookup"><span data-stu-id="13dce-113">This [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) uses hello K-Means methodology, a commonly used clustering technique, toocluster arbitrary data into groups.</span></span> <span data-ttu-id="13dce-114">Questo servizio web accetta dati hello e il numero di hello di k cluster come input e produce stime che hello k gruppi toowhich appartiene ogni osservazioni.</span><span class="sxs-lookup"><span data-stu-id="13dce-114">This web service takes hello data and hello number of k clusters as input, and produces predictions of which of hello k groups toowhich each observations belongs.</span></span> 

> <span data-ttu-id="13dce-115">Questo servizio Web può essere utilizzato dagli utenti: potenzialmente tramite un'app mobile, un sito Web o anche in un computer locale, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="13dce-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="13dce-116">Ma scopo hello del servizio web hello anche tooserve come esempio di come Azure Machine Learning è possibile servizi web utilizzati toocreate su codice R.</span><span class="sxs-lookup"><span data-stu-id="13dce-116">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="13dce-117">Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="13dce-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="13dce-118">servizio web Hello può quindi essere pubblicata toohello Azure Marketplace e utilizzato da utenti e dispositivi attraverso HelloWorld con alcuna installazione dell'infrastruttura dall'autore hello del servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="13dce-118">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="13dce-119">Uso del servizio Web</span><span class="sxs-lookup"><span data-stu-id="13dce-119">Consumption of web service</span></span>
<span data-ttu-id="13dce-120">Questo servizio web consente di raggruppare dati hello in un set di k gruppi e gli output hello assegnazione del gruppo per ogni riga.</span><span class="sxs-lookup"><span data-stu-id="13dce-120">This web service groups hello data into a set of k groups and outputs hello group assignment for each row.</span></span> <span data-ttu-id="13dce-121">servizio web Hello dati tooinput utente finale di hello previsto è una stringa in cui le righe sono separate da virgole (,) e le colonne sono separate da punti e virgola (;).</span><span class="sxs-lookup"><span data-stu-id="13dce-121">hello web service expects hello end user tooinput data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="13dce-122">servizio web Hello previsto 1 riga alla volta.</span><span class="sxs-lookup"><span data-stu-id="13dce-122">hello web service expects 1 row at a time.</span></span> <span data-ttu-id="13dce-123">Un set di dati di esempio può avere un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="13dce-123">An example dataset could look like this:</span></span>

![Dati di esempio][1]

<span data-ttu-id="13dce-125">Si supponga di hello utente desiderata tooseparate questi dati in 3 gruppi si escludono a vicenda.</span><span class="sxs-lookup"><span data-stu-id="13dce-125">Suppose hello user wanted tooseparate this data into 3 mutually exclusive groups.</span></span> <span data-ttu-id="13dce-126">dati di input per hello di sopra di set di dati sarebbe seguente hello Hello: valore = "10 5; 2,18; 1; 6,7; 5; 5,22; 3; 4,12; 2; 1,10; 3; 4"; k = "3".</span><span class="sxs-lookup"><span data-stu-id="13dce-126">hello data input for hello above dataset would be hello following: value = “10;5;2,18;1;6,7;5;5,22;3;4,12;2;1,10;3;4”; k=”3”.</span></span> <span data-ttu-id="13dce-127">output di Hello è hello l'appartenenza al gruppo stimati per ognuna delle righe hello.</span><span class="sxs-lookup"><span data-stu-id="13dce-127">hello output is hello predicted group membership for each of hello rows.</span></span>

> <span data-ttu-id="13dce-128">Questo servizio, ospitato in Azure Marketplace, hello è un servizio OData. questi può essere chiamati tramite i metodi POST o GET.</span><span class="sxs-lookup"><span data-stu-id="13dce-128">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="13dce-129">Esistono diversi modi di utilizzo di servizio hello in modo automatico (è un'app di esempio [qui](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span><span class="sxs-lookup"><span data-stu-id="13dce-129">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="13dce-130">Codice C# iniziale per l'uso del servizio Web:</span><span class="sxs-lookup"><span data-stu-id="13dce-130">Starting C# code for web service consumption:</span></span>
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




## <a name="creation-of-web-service"></a><span data-ttu-id="13dce-131">Creazione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="13dce-131">Creation of web service</span></span>
> <span data-ttu-id="13dce-132">Questo servizio Web è stato creato tramite Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="13dce-132">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="13dce-133">Per una versione di prova gratuita e per video introduttivi sulla creazione di esperimenti e sulla [pubblicazione di servizi Web](machine-learning-publish-a-machine-learning-web-service.md), vedere [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="13dce-133">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="13dce-134">Di seguito è riportata una schermata dell'esperimento hello creato codice di esempio e servizio web hello per ciascuno dei moduli di hello all'interno di sperimentazione hello.</span><span class="sxs-lookup"><span data-stu-id="13dce-134">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="13dce-135">Da Azure Machine Learning, all'interno di un esperimento vuoto nuovo è stato creato e due [Execute R Script] [ execute-r-script] moduli estratta nell'area di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="13dce-135">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto hello workspace.</span></span> <span data-ttu-id="13dce-136">schema dati Hello è stato creato con un semplice [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="13dce-136">hello data schema was created with a simple [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="13dce-137">Quindi, schema dati hello è stato collegato toohello cluster sezione modello nuovamente creato con un [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="13dce-137">Then, hello data schema was linked toohello cluster model section, again created with an [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="13dce-138">In hello [Execute R Script] [ execute-r-script] utilizzato per il modello di cluster hello, servizio web hello utilizza quindi la funzione "k-means" hello, che è predefinita in hello [Execute R Script] [ execute-r-script] di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="13dce-138">In hello [Execute R Script][execute-r-script] used for hello cluster model, hello web service then utilizes hello “k-means” function, which is prebuilt into hello [Execute R Script][execute-r-script] of Azure Machine Learning.</span></span>    

![Flusso dell'esperimento][3]

#### <a name="module-1"></a><span data-ttu-id="13dce-140">Modulo 1:</span><span class="sxs-lookup"><span data-stu-id="13dce-140">Module 1:</span></span>
    #Enter hello input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a><span data-ttu-id="13dce-141">Modulo 2:</span><span class="sxs-lookup"><span data-stu-id="13dce-141">Module 2:</span></span>
    # Map 1-based optional input ports toovariables
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

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("mydatafinal");


## <a name="limitations"></a><span data-ttu-id="13dce-142">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="13dce-142">Limitations</span></span>
<span data-ttu-id="13dce-143">Questo è un esempio molto semplice di un servizio Web di clustering.</span><span class="sxs-lookup"><span data-stu-id="13dce-143">This is a very simple example of a clustering web service.</span></span> <span data-ttu-id="13dce-144">Nessun rilevamento di errori viene implementato come possono essere visualizzati dal codice di esempio hello precedente, e presuppone servizio hello tutto ciò che è una variabile continua (nessuna funzionalità categorica consentita), come hello servizio solo input valori numerici in fase di hello della creazione di hello del sito web servizio.</span><span class="sxs-lookup"><span data-stu-id="13dce-144">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="13dce-145">Inoltre, hello servizio gestisce attualmente le dimensioni dei dati limitato, a causa di natura di richiesta/risposta toohello del servizio web hello si adatta chiamata e hello delle tabelle dei fatti che hello modello ogni volta che viene chiamato servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="13dce-145">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="13dce-146">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="13dce-146">FAQ</span></span>
<span data-ttu-id="13dce-147">Per domande frequenti sull'utilizzo del servizio web hello o pubblicazione toohello Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="13dce-147">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

