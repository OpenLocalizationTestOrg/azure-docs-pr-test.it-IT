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
# <a name="deprecated-cluster-model"></a>(Deprecato) Modello di cluster

> [!NOTE]
> è stata ritirata Hello Microsoft DataMarket e questa API è stata deprecata. 
> 
> Sono disponibili molte esperimenti di esempio utile e API hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Per ulteriori informazioni sulla raccolta hello, vedere [condivisione e individuare le risorse in Cortana Intelligence Gallery hello](machine-learning-gallery-how-to-use-contribute-publish.md).

Come è possibile stimare gruppi dei comportamenti dei titolari di carta di credito in ordine tooreduce hello ammortamento rischio di autorità emittenti di carta di credito? Come possiamo è definire gruppi di tratti dalla personalità dei dipendenti in ordine tooimprove delle relative prestazioni al lavoro? Come possono medici classificare i pazienti in gruppi in base alle caratteristiche di hello della loro diseases? Teoricamente, è possibile rispondere a tutte queste domande tramite l'analisi dei cluster.   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

In pratica, l'analisi dei cluster classifica un set di osservazioni in due o più gruppi sconosciuti che si escludono a vicenda in base a una combinazione di variabili. scopo di Hello dell'analisi del cluster è toodiscover un sistema di organizzare le osservazioni, in genere gli utenti o le caratteristiche, in gruppi, in cui i membri dei gruppi di hello condividono le proprietà. Questo [servizio](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) utilizza hello metodologia K-medie, una tecnica di clustering utilizzata frequentemente, toocluster dati arbitrari in gruppi. Questo servizio web accetta dati hello e il numero di hello di k cluster come input e produce stime che hello k gruppi toowhich appartiene ogni osservazioni. 

> Questo servizio Web può essere utilizzato dagli utenti: potenzialmente tramite un'app mobile, un sito Web o anche in un computer locale, ad esempio. Ma scopo hello del servizio web hello anche tooserve come esempio di come Azure Machine Learning è possibile servizi web utilizzati toocreate su codice R. Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web. servizio web Hello può quindi essere pubblicata toohello Azure Marketplace e utilizzato da utenti e dispositivi attraverso HelloWorld con alcuna installazione dell'infrastruttura dall'autore hello del servizio web hello.  
> 
> 

## <a name="consumption-of-web-service"></a>Uso del servizio Web
Questo servizio web consente di raggruppare dati hello in un set di k gruppi e gli output hello assegnazione del gruppo per ogni riga. servizio web Hello dati tooinput utente finale di hello previsto è una stringa in cui le righe sono separate da virgole (,) e le colonne sono separate da punti e virgola (;). servizio web Hello previsto 1 riga alla volta. Un set di dati di esempio può avere un aspetto analogo al seguente:

![Dati di esempio][1]

Si supponga di hello utente desiderata tooseparate questi dati in 3 gruppi si escludono a vicenda. dati di input per hello di sopra di set di dati sarebbe seguente hello Hello: valore = "10 5; 2,18; 1; 6,7; 5; 5,22; 3; 4,12; 2; 1,10; 3; 4"; k = "3". output di Hello è hello l'appartenenza al gruppo stimati per ognuna delle righe hello.

> Questo servizio, ospitato in Azure Marketplace, hello è un servizio OData. questi può essere chiamati tramite i metodi POST o GET. 
> 
> 

Esistono diversi modi di utilizzo di servizio hello in modo automatico (è un'app di esempio [qui](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Codice C# iniziale per l'uso del servizio Web:
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




## <a name="creation-of-web-service"></a>Creazione del servizio Web
> Questo servizio Web è stato creato tramite Azure Machine Learning. Per una versione di prova gratuita e per video introduttivi sulla creazione di esperimenti e sulla [pubblicazione di servizi Web](machine-learning-publish-a-machine-learning-web-service.md), vedere [azure.com/ml](http://azure.com/ml). Di seguito è riportata una schermata dell'esperimento hello creato codice di esempio e servizio web hello per ciascuno dei moduli di hello all'interno di sperimentazione hello.
> 
> 

Da Azure Machine Learning, all'interno di un esperimento vuoto nuovo è stato creato e due [Execute R Script] [ execute-r-script] moduli estratta nell'area di lavoro hello. schema dati Hello è stato creato con un semplice [Execute R Script][execute-r-script]. Quindi, schema dati hello è stato collegato toohello cluster sezione modello nuovamente creato con un [Execute R Script][execute-r-script]. In hello [Execute R Script] [ execute-r-script] utilizzato per il modello di cluster hello, servizio web hello utilizza quindi la funzione "k-means" hello, che è predefinita in hello [Execute R Script] [ execute-r-script] di Azure Machine Learning.    

![Flusso dell'esperimento][3]

#### <a name="module-1"></a>Modulo 1:
    #Enter hello input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a>Modulo 2:
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


## <a name="limitations"></a>Limitazioni
Questo è un esempio molto semplice di un servizio Web di clustering. Nessun rilevamento di errori viene implementato come possono essere visualizzati dal codice di esempio hello precedente, e presuppone servizio hello tutto ciò che è una variabile continua (nessuna funzionalità categorica consentita), come hello servizio solo input valori numerici in fase di hello della creazione di hello del sito web servizio. Inoltre, hello servizio gestisce attualmente le dimensioni dei dati limitato, a causa di natura di richiesta/risposta toohello del servizio web hello si adatta chiamata e hello delle tabelle dei fatti che hello modello ogni volta che viene chiamato servizio web hello. 

## <a name="faq"></a>domande frequenti
Per domande frequenti sull'utilizzo del servizio web hello o pubblicazione toohello Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

