---
title: Dieci cose da fare con la macchina virtuale data science | Documentazione Microsoft
description: "Eseguire diverse attività di esplorazione e modellazione dei dati nella macchina virtuale per l'analisi scientifica dei dati."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 145dfe3e-2bd2-478f-9b6e-99d97d789c62
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;weig;bradsev
ms.openlocfilehash: 45af1cd3a05b483429d2307659f1882ef28921f6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="ten-things-you-can-do-on-the-data-science-virtual-machine"></a><span data-ttu-id="84d3c-103">Dieci cose da fare con la macchina virtuale per l'analisi scientifica dei dati</span><span class="sxs-lookup"><span data-stu-id="84d3c-103">Ten things you can do on the Data science Virtual Machine</span></span>
<span data-ttu-id="84d3c-104">La macchina virtuale per l'analisi scientifica dei dati (DSVM, Data Science Virtual Machine) di Microsoft è un ambiente di sviluppo di analisi scientifica dei dati avanzato che consente di eseguire diverse attività di esplorazione e modellazione dati.</span><span class="sxs-lookup"><span data-stu-id="84d3c-104">The Microsoft Data Science Virtual Machine (DSVM) is a powerful data science development environment that enables you to perform various data exploration and modeling tasks.</span></span> <span data-ttu-id="84d3c-105">L'ambiente è già compilato e in bundle in diversi strumenti comuni di analisi dei dati che consentono di iniziare a usare rapidamente e facilmente l'analisi per le distribuzioni locali, cloud o ibride.</span><span class="sxs-lookup"><span data-stu-id="84d3c-105">The environment comes already built and bundled with several popular data analytics tools that make it easy to get started quickly with your analysis for On-premises, Cloud or hybrid deployments.</span></span> <span data-ttu-id="84d3c-106">DSVM è ben integrata con diversi servizi di Azure e può leggere ed elaborare dati già archiviati in Azure, in Azure SQL Data Warehouse, Azure Data Lake, Archiviazione di Azure o in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="84d3c-106">The DSVM works closely with many Azure services and is able to read and process data that is already stored on Azure, in Azure SQL Data Warehouse, Azure Data Lake, Azure Storage, or in Azure Cosmos DB.</span></span> <span data-ttu-id="84d3c-107">Può anche sfruttare altri strumenti di analisi come Azure Machine Learning e Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="84d3c-107">It can also leverage other analytics tools such as Azure Machine Learning and Azure Data Factory.</span></span>

<span data-ttu-id="84d3c-108">Questo articolo illustra come usare DSVM per eseguire diverse attività di analisi scientifica dei dati e interagire con altri servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="84d3c-108">In this article we walk you through how to use your DSVM to perform various data science tasks and interact with other Azure services.</span></span> <span data-ttu-id="84d3c-109">Ecco alcune attività che è possibile eseguire con DSVM:</span><span class="sxs-lookup"><span data-stu-id="84d3c-109">Here are some of the things you can do on the DSVM:</span></span>

1. <span data-ttu-id="84d3c-110">Esplorare dati e sviluppare modelli in locale in DSVM usando Microsoft R Server e Python</span><span class="sxs-lookup"><span data-stu-id="84d3c-110">Explore data and develop models locally on the DSVM using Microsoft R Server, Python</span></span>
2. <span data-ttu-id="84d3c-111">Usare un notebook di Jupyter per sperimentare con i dati in un browser usando Python 2, Python 3 e Microsoft R, una versione di R pronta per l'azienda progettata per la scalabilità e le prestazioni</span><span class="sxs-lookup"><span data-stu-id="84d3c-111">Use a Jupyter notebook to experiment with your data on a browser using Python 2, Python 3, Microsoft R an enterprise ready version of R designed for scalability and performance</span></span>
3. <span data-ttu-id="84d3c-112">Rendere operativi i modelli compilati usando R e Python in Azure Machine Learning in modo che le applicazioni client possano accedere ai modelli con una semplice interfaccia di servizi Web</span><span class="sxs-lookup"><span data-stu-id="84d3c-112">Operationalize models built using R and Python on Azure Machine Learning so client applications can access your models using a simple web services interface</span></span>
4. <span data-ttu-id="84d3c-113">Amministrare le risorse di Azure usando il portale di Azure o PowerShell</span><span class="sxs-lookup"><span data-stu-id="84d3c-113">Administer your Azure resources using  Azure portal or Powershell</span></span>
5. <span data-ttu-id="84d3c-114">Estendere lo spazio di archiviazione e condividere codice o set di dati su larga scala con l'intero team creando un archivio file di Azure come unità installabile in DSVM</span><span class="sxs-lookup"><span data-stu-id="84d3c-114">Extend your storage space and share large-scale datasets / code across your whole team by creating an Azure File storage as a mountable drive on your DSVM</span></span>
6. <span data-ttu-id="84d3c-115">Condividere il codice con il team usando GitHub e accedere all'archivio con i client Git preinstallati (Git Bash, Git GUI).</span><span class="sxs-lookup"><span data-stu-id="84d3c-115">Share code with your team using GitHub and access your repository using the pre-installed Git clients - Git Bash, Git GUI.</span></span>
7. <span data-ttu-id="84d3c-116">Accedere a diversi servizi dati e analisi di Azure, ad esempio Archiviazione BLOB di Azure, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse e database</span><span class="sxs-lookup"><span data-stu-id="84d3c-116">Access various Azure data and analytics services like Azure blob storage, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse & databases</span></span>
8. <span data-ttu-id="84d3c-117">Compilare report e dashboard usando Power BI Desktop preinstallato in DSVM e distribuirli nel cloud</span><span class="sxs-lookup"><span data-stu-id="84d3c-117">Build reports and dashboard using the Power BI Desktop pre-installed on the DSVM and deploy them on the cloud</span></span>
9. <span data-ttu-id="84d3c-118">Ridimensionare in modo dinamico DSVM per poter soddisfare le esigenze del progetto</span><span class="sxs-lookup"><span data-stu-id="84d3c-118">Dynamically scale your DSVM to meet your project needs</span></span>
10. <span data-ttu-id="84d3c-119">Installare strumenti aggiuntivi nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="84d3c-119">Install additional tools on your virtual machine</span></span>   

> [!NOTE]
> <span data-ttu-id="84d3c-120">Per molti dei servizi di archiviazione e analisi dei dati aggiuntivi elencati in questo articolo vengono applicati costi di utilizzo aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="84d3c-120">Additional usage charges apply for many of the additional data storage and analytics services listed in this article.</span></span> <span data-ttu-id="84d3c-121">Per altri dettagli, vedere la pagina [Prezzi di Azure](https://azure.microsoft.com/pricing/) .</span><span class="sxs-lookup"><span data-stu-id="84d3c-121">Please refer to the [Azure Pricing](https://azure.microsoft.com/pricing/) page for details.</span></span>
> 
> 

<span data-ttu-id="84d3c-122">**Prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="84d3c-122">**Prerequisites**</span></span>

* <span data-ttu-id="84d3c-123">È necessaria una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="84d3c-123">You need an Azure subscription.</span></span> <span data-ttu-id="84d3c-124">È possibile iscriversi per una versione di valutazione gratuita di Azure [qui](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="84d3c-124">You can sign up for a free trial [here](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="84d3c-125">Le istruzioni per il provisioning di una macchina virtuale per l'analisi scientifica dei dati nel portale di Azure sono disponibili nel documento relativo alla [creazione di una macchina virtuale](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="84d3c-125">Instructions for provisioning a Data Science Virtual Machine on the Azure portal are available at [Creating a virtual machine](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).</span></span>

## <a name="1-explore-data-and-develop-models-using-microsoft-r-server-or-python"></a><span data-ttu-id="84d3c-126">1. Esplorare dati e sviluppare modelli usando Microsoft R Server o Python</span><span class="sxs-lookup"><span data-stu-id="84d3c-126">1. Explore data and develop models using Microsoft R Server or Python</span></span>
<span data-ttu-id="84d3c-127">È possibile usare linguaggi come R e Python per eseguire l'analisi dei dati direttamente in DSVM.</span><span class="sxs-lookup"><span data-stu-id="84d3c-127">You can use languages like R and Python to do your data analytics right on the DSVM.</span></span>

<span data-ttu-id="84d3c-128">Per R, è possibile usare un IDE chiamato "Revolution R Enterprise 8.0" presente nel menu Start o nel desktop.</span><span class="sxs-lookup"><span data-stu-id="84d3c-128">For R, you can use an IDE called "Revolution R Enterprise 8.0" that can be found on the start menu or the desktop.</span></span> <span data-ttu-id="84d3c-129">Microsoft ha fornito librerie aggiuntive oltre a Open source/CRAN-R per consentire l'analisi scalabile e offrire la possibilità di analizzare dati di dimensioni maggiori di quelle consentite dalla memoria eseguendo un'analisi parallela in blocchi.</span><span class="sxs-lookup"><span data-stu-id="84d3c-129">Microsoft has provided additional libraries on top of the Open source/CRAN-R to enable scalable analytics and the ability to analyze data larger than the memory size allowed by doing parallel chunked analysis.</span></span> <span data-ttu-id="84d3c-130">È anche possibile installare l'IDE R di desiderato, ad esempio [RStudio](https://www.rstudio.com/products/rstudio-desktop/).</span><span class="sxs-lookup"><span data-stu-id="84d3c-130">You can also install an R IDE of your choice like [RStudio](https://www.rstudio.com/products/rstudio-desktop/).</span></span>

<span data-ttu-id="84d3c-131">Per Python, è possibile usare un IDE come Visual Studio Community Edition in cui è preinstallata l'estensione Python Tools for Visual Studio (PTVS).</span><span class="sxs-lookup"><span data-stu-id="84d3c-131">For Python, you can use an IDE like Visual Studio Community Edition which has the Python Tools for Visual Studio (PTVS) extension pre-installed.</span></span> <span data-ttu-id="84d3c-132">Per impostazione predefinita, in PTVS è configurato solo Python 2.7 di base, senza librerie di analisi come SciKit o Pandas.</span><span class="sxs-lookup"><span data-stu-id="84d3c-132">By default, only a basic Python 2.7 is configured on PTVS (without any analytics library like SciKit, Pandas).</span></span> <span data-ttu-id="84d3c-133">Per abilitare Anaconda Python 2.7 e 3.5, è necessario eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="84d3c-133">In order to enable Anaconda Python 2.7 and 3.5, you need to do the following:</span></span>

* <span data-ttu-id="84d3c-134">Creare ambienti personalizzati per ogni versione passando a **Strumenti** -> **Python Tools** -> **Python Environments** (Strumenti Python -> Ambienti Python) e quindi facendo clic su "**+ Custom**" (+ Personalizza) in Visual Studio 2015 Community Edition.</span><span class="sxs-lookup"><span data-stu-id="84d3c-134">Create custom environments for each version by navigating to **Tools** -> **Python Tools** -> **Python Environments** and then clicking "**+ Custom**" in the Visual Studio 2015 Community Edition</span></span>
* <span data-ttu-id="84d3c-135">Immettere una descrizione e impostare i percorsi con il prefisso dell'ambiente come *c:\anaconda* per Anaconda Python 2.7 OPPURE *c:\anaconda\envs\py35* per Anaconda Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="84d3c-135">Give a description and set the environment prefix paths as *c:\anaconda* for Anaconda Python 2.7 OR *c:\anaconda\envs\py35* for Anaconda Python 3.5</span></span>
* <span data-ttu-id="84d3c-136">Fare clic su **Rilevamento automatico** e quindi su **Applica** per salvare l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="84d3c-136">Click **Auto Detect** and then **Apply** to save the environment.</span></span>

<span data-ttu-id="84d3c-137">Ecco come appare la configurazione dell'ambiente personalizzato in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="84d3c-137">Here is what the custom environment setup looks like in Visual Studio.</span></span>

![Configurazione di PTVS](./media/machine-learning-data-science-vm-do-ten-things/PTVSSetup.png)

<span data-ttu-id="84d3c-139">Per altri dettagli su come creare gli ambienti Python, vedere la [documentazione relativa a PTVS](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) .</span><span class="sxs-lookup"><span data-stu-id="84d3c-139">See the [PTVS documentation](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) for additional details on how to create Python Environments.</span></span>

<span data-ttu-id="84d3c-140">A questo punto è possibile iniziare a creare un nuovo progetto Python.</span><span class="sxs-lookup"><span data-stu-id="84d3c-140">Now you are set up to create a new Python project.</span></span> <span data-ttu-id="84d3c-141">Passare a **File** -> **Nuovo** -> **Progetto** -> **Python** e selezionare il tipo di applicazione Python da compilare.</span><span class="sxs-lookup"><span data-stu-id="84d3c-141">Navigate to **File** -> **New** -> **Project** -> **Python** and select the type of Python application you are building.</span></span> <span data-ttu-id="84d3c-142">È possibile impostare l'ambiente Python per il progetto corrente sulla versione desiderata, ad esempio Anaconda 2.7 o 3.5. Fare clic con il pulsante destro del mouse su **Python Environments** (Ambienti Python), selezionare **Aggiungi/Rimuovi Python Environments** e quindi selezionare l'ambiente desiderato da associare al progetto.</span><span class="sxs-lookup"><span data-stu-id="84d3c-142">You can set the Python environment for the current project to the desired version (Anaconda 2.7 or 3.5): right-click the **Python environment**, select **Add/Remove Python Environments**, and then select the desired environment to associate with the project.</span></span> <span data-ttu-id="84d3c-143">È possibile trovare altre informazioni sull'uso di PTVS nella pagina di [documentazione](https://github.com/Microsoft/PTVS/wiki) del prodotto.</span><span class="sxs-lookup"><span data-stu-id="84d3c-143">You can find more information about working with PTVS on the product [documentation](https://github.com/Microsoft/PTVS/wiki) page.</span></span>

## <a name="2-using-a-jupyter-notebook-to-explore-and-model-your-data-with-python-or-r"></a><span data-ttu-id="84d3c-144">2. Uso di un notebook di Jupyter per esplorare e modellare i dati con Python o R</span><span class="sxs-lookup"><span data-stu-id="84d3c-144">2. Using a Jupyter Notebook to explore and model your data with Python or R</span></span>
<span data-ttu-id="84d3c-145">Il notebook di Jupyter è un ambiente avanzato che fornisce un "IDE" basato su browser per l'esplorazione e la modellazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="84d3c-145">The Jupyter Notebook is a powerful environment that provides a browser-based "IDE" for data exploration and modeling.</span></span> <span data-ttu-id="84d3c-146">È possibile usare Python 2, Python 3 o R, sia open source che Microsoft R Server, in un notebook di Jupyter.</span><span class="sxs-lookup"><span data-stu-id="84d3c-146">You can use Python 2, Python 3 or R (both Open Source and the Microsoft R Server) in a Jupyter Notebook.</span></span>

<span data-ttu-id="84d3c-147">Per avviare il notebook di Jupyter, fare clic sull'icona del menu Start o sull'icona del desktop denominata **Notebook di Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="84d3c-147">To launch the Jupyter Notebook click on the start menu icon / desktop icon titled **Jupyter Notebook**.</span></span> <span data-ttu-id="84d3c-148">In DSVM è anche possibile passare a "https://localhost:9999/" per accedere al notebook di Jupyter.</span><span class="sxs-lookup"><span data-stu-id="84d3c-148">On the DSVM you can also browse to "https://localhost:9999/" to access the Jupiter Notebook.</span></span> <span data-ttu-id="84d3c-149">Se viene richiesta una password, seguire le istruzioni fornite nella sezione ***Come creare una password complessa nel server notebook di Jupyter*** dell'argomento [Eseguire il provisioning di una macchina virtuale per l'analisi scientifica dei dati di Microsoft](machine-learning-data-science-provision-vm.md) per creare una password complessa per l'accesso a Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="84d3c-149">If it prompts you for a password, use instructions provided in the ***How to create a strong password on the Jupyter notebook server*** section of the [Provision the Microsoft Data Science Virtual Machine](machine-learning-data-science-provision-vm.md) topic to create a strong password to access the Jupyter notebook.</span></span> 

<span data-ttu-id="84d3c-150">Una volta effettuato l'accesso al notebook, viene visualizzata una directory contenente alcuni notebook di esempio inclusi nel pacchetto DSVM.</span><span class="sxs-lookup"><span data-stu-id="84d3c-150">Once you have opened the notebook, you should see a directory that contains a few example notebooks that are pre-packaged into the DSVM.</span></span> <span data-ttu-id="84d3c-151">A questo punto è possibile:</span><span class="sxs-lookup"><span data-stu-id="84d3c-151">Now you can:</span></span>

* <span data-ttu-id="84d3c-152">Fare clic sul notebook per visualizzare il codice.</span><span class="sxs-lookup"><span data-stu-id="84d3c-152">click on the notebook to see the code.</span></span>
* <span data-ttu-id="84d3c-153">Eseguire ogni cella premendo **MAIUSC+INVIO**.</span><span class="sxs-lookup"><span data-stu-id="84d3c-153">execute each cell by pressing **SHIFT-ENTER**.</span></span>
* <span data-ttu-id="84d3c-154">Eseguire l'intero notebook facendo clic su **Cell** -> **Run** (Cella -> Esegui).</span><span class="sxs-lookup"><span data-stu-id="84d3c-154">run the entire notebook by clicking on **Cell** -> **Run**</span></span>
* <span data-ttu-id="84d3c-155">Creare un nuovo notebook facendo clic sull'icona di Jupyter nell'angolo in alto a sinistra. Fare quindi clic sul pulsante **New** (Nuovo) a destra e infine scegliere il linguaggio del notebook, detto anche kernel.</span><span class="sxs-lookup"><span data-stu-id="84d3c-155">create a new notebook by clicking on the Jupyter Icon (left top corner) and then clicking **New** button on the right and then choosing the notebook language (also known as kernels).</span></span>   

> [!NOTE]
> <span data-ttu-id="84d3c-156">Attualmente sono supportati Python 2.7, Python 3.5 e R. Il kernel R supporta la programmazione sia in R open source che in Microsoft R Server scalabile aziendale.</span><span class="sxs-lookup"><span data-stu-id="84d3c-156">Currently we support Python 2.7, Python 3.5 and R. The R kernel supports programming in both Open source R as well as the enterprise scalable Microsoft R Server.</span></span>   
> 
> 

<span data-ttu-id="84d3c-157">Una volta effettuato l'accesso al notebook, è possibile esplorare i dati, compilare il modello e testare il modello usando le librerie preferite.</span><span class="sxs-lookup"><span data-stu-id="84d3c-157">Once you are in the notebook you can explore your data, build the model, test the model using your choice of libraries.</span></span>

## <a name="3-build-models-using-r-or-python-and-operationalize-them-using-azure-machine-learning"></a><span data-ttu-id="84d3c-158">3. Compilare modelli usando R o Python e renderli operativi con Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="84d3c-158">3. Build models using R or Python and Operationalize them using Azure Machine Learning</span></span>
<span data-ttu-id="84d3c-159">Una volta compilato e convalidato il modello, il passaggio successivo consiste in genere nel distribuirlo nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="84d3c-159">Once you have built and validated your model the next step is usually to deploy it into production.</span></span> <span data-ttu-id="84d3c-160">Ciò consente alle applicazioni client di richiamare le stime del modello in tempo reale o in modalità batch.</span><span class="sxs-lookup"><span data-stu-id="84d3c-160">This allows your client applications to invoke the model predictions on a real time or on a batch mode basis.</span></span> <span data-ttu-id="84d3c-161">Azure Machine Learning offre un meccanismo per rendere operativo il modello compilato in R o Python.</span><span class="sxs-lookup"><span data-stu-id="84d3c-161">Azure Machine Learning provides a mechanism to operationalize a model built in either R or Python.</span></span>

<span data-ttu-id="84d3c-162">Quando si rende operativo il modello in Azure Machine Learning, viene esposto un servizio Web che consente ai client di effettuare chiamate REST che passano i parametri di input e ricevono le stime dal modello come output.</span><span class="sxs-lookup"><span data-stu-id="84d3c-162">When you operationalize your model in Azure Machine Learning, a web service is exposed that allows clients to make REST calls that pass in input parameters and receive predictions from the model as outputs.</span></span>   

> [!NOTE]
> <span data-ttu-id="84d3c-163">Se non si è ancora iscritti ad Azure Machine Learning, è possibile ottenere un'area di lavoro gratuita o standard visitando la home page di [Azure Machine Learning Studio](https://studio.azureml.net/) e facendo clic su "Get Started" (Per iniziare).</span><span class="sxs-lookup"><span data-stu-id="84d3c-163">If you have not yet signed up for Azure Machine Learning, you can obtain a free workspace or a standard workspace by visiting the [Azure Machine Learning Studio](https://studio.azureml.net/) home page and clicking on "Get Started".</span></span>   
> 
> 

### <a name="build-and-operationalize-python-models"></a><span data-ttu-id="84d3c-164">Compilare e rendere operativi i modelli Python</span><span class="sxs-lookup"><span data-stu-id="84d3c-164">Build and Operationalize Python models</span></span>
<span data-ttu-id="84d3c-165">Di seguito è riportato un frammento di codice sviluppato in un notebook di Jupyter con Python che compila un semplice modello con la libreria SciKit-learn.</span><span class="sxs-lookup"><span data-stu-id="84d3c-165">Here is a snippet of code developed in a Python Jupyter Notebook that builds a simple model using the SciKit-learn library.</span></span>

    #IRIS classification
    from sklearn import datasets
    from sklearn import svm
    clf = svm.SVC()
    iris = datasets.load_iris()
    X, y = iris.data, iris.target
    clf.fit(X, y)

<span data-ttu-id="84d3c-166">Il metodo usato per distribuire i modelli di Python in Azure Machine Learning consiste nell'eseguire il wrapping della stima del modello in una funzione e nel decorarla con gli attributi forniti dalla libreria di Azure Machine Learning che identificano l'ID, la chiave API, i parametri di input e i parametri restituiti dell'area di lavoro di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="84d3c-166">The method used to deploy your python models to Azure Machine Learning wraps the prediction of the model into a function and decorates it with attributes provided by the pre-installed Azure Machine Learning python library that denote your Azure Machine Learning workspace ID, API Key, and the input and return parameters.</span></span>  

    from azureml import services
    @services.publish(workspaceid, auth_token)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(int) #0, or 1, or 2
    def predictIris(sep_l, sep_w, pet_l, pet_w):
     inputArray = [sep_l, sep_w, pet_l, pet_w]
    return clf.predict(inputArray)

<span data-ttu-id="84d3c-167">Un client può ora effettuare chiamate al servizio Web.</span><span class="sxs-lookup"><span data-stu-id="84d3c-167">A client can now make calls to the web service.</span></span> <span data-ttu-id="84d3c-168">Esistono pratici wrapper che costruiscono le richieste dell'API REST.</span><span class="sxs-lookup"><span data-stu-id="84d3c-168">There are convenience wrappers that construct the REST API requests.</span></span> <span data-ttu-id="84d3c-169">Ecco un codice di esempio per utilizzare il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="84d3c-169">Here is a sample code to consume the web service.</span></span>

    # Consume through web service URL and keys
    from azureml import services
    @services.service(url, api_key)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(float)
    def IrisPredictor(sep_l, sep_w, pet_l, pet_w):
    pass

    IrisPredictor(3,2,3,4)


> [!NOTE]
> <span data-ttu-id="84d3c-170">La libreria di Azure Machine Learning è attualmente supportata solo in Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="84d3c-170">The Azure Machine Learning library is only supported on Python 2.7 currently.</span></span>   
> 
> 

### <a name="build-and-operationalize-r-models"></a><span data-ttu-id="84d3c-171">Compilare e rendere operativi i modelli R</span><span class="sxs-lookup"><span data-stu-id="84d3c-171">Build and Operationalize R models</span></span>
<span data-ttu-id="84d3c-172">È possibile distribuire in Azure Machine Learning i modelli R compilati nella macchina virtuale per l'analisi scientifica dei dati o altrove in modo simile a come è stato fatto per Python.</span><span class="sxs-lookup"><span data-stu-id="84d3c-172">You can deploy R models built on the Data Science Virtual Machine or elsewhere onto Azure Machine Learning in a manner that is similar to how it is done for Python.</span></span> <span data-ttu-id="84d3c-173">Ecco i passaggi necessari:</span><span class="sxs-lookup"><span data-stu-id="84d3c-173">Her are the steps:</span></span>

* <span data-ttu-id="84d3c-174">Creare un file settings.json per fornire l'ID area di lavoro e il token di autorizzazione, come illustrato nel codice di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="84d3c-174">create a settings.json file to provide your workspace ID and auth token as shown in the following code sample.</span></span>
* <span data-ttu-id="84d3c-175">Scrivere un wrapper per la funzione di stima del modello.</span><span class="sxs-lookup"><span data-stu-id="84d3c-175">write a wrapper for the model's predict function.</span></span>
* <span data-ttu-id="84d3c-176">Chiamare ```publishWebService``` nella libreria di Azure Machine Learning per passare il wrapper della funzione.</span><span class="sxs-lookup"><span data-stu-id="84d3c-176">call ```publishWebService``` in the Azure Machine Learning library to pass in the function wrapper.</span></span>  

<span data-ttu-id="84d3c-177">Ecco la procedura e i frammenti di codice che è possibile usare per configurare, creare, pubblicare e usare un modello come servizio Web in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="84d3c-177">Here is the procedure and code snippets that can be used to set up, build, publish, and consume a model as a web service in Azure Machine Learning.</span></span>

#### <a name="setup"></a><span data-ttu-id="84d3c-178">Configurazione</span><span class="sxs-lookup"><span data-stu-id="84d3c-178">Setup</span></span>
1. <span data-ttu-id="84d3c-179">Installare il pacchetto R di Machine Learning digitando ```install.packages("AzureML")``` nell'IDE Revolution R Enterprise 8.0 o nell'IDE R.</span><span class="sxs-lookup"><span data-stu-id="84d3c-179">Install the Machine Learning R package by typing ```install.packages("AzureML")``` in Revolution R Enterprise 8.0 IDE or your R IDE.</span></span>
2. <span data-ttu-id="84d3c-180">Scaricare RTools da [qui](https://cran.r-project.org/bin/windows/Rtools/).</span><span class="sxs-lookup"><span data-stu-id="84d3c-180">Download RTools from [here](https://cran.r-project.org/bin/windows/Rtools/).</span></span> <span data-ttu-id="84d3c-181">Per rendere operativo il pacchetto R in Machine Learning, l'utilità zip, denominata zip.exe, deve trovarsi nel percorso.</span><span class="sxs-lookup"><span data-stu-id="84d3c-181">You need the zip utility in the path (and named zip.exe) to operationalize your R package into Machine Learning.</span></span>
3. <span data-ttu-id="84d3c-182">Nella home directory creare un file settings.json in una directory denominata ```.azureml``` e immettere i parametri dall'area di lavoro di Azure Machine Learning:</span><span class="sxs-lookup"><span data-stu-id="84d3c-182">Create a settings.json file under a directory called ```.azureml``` under your home directory and enter the parameters from your Azure Machine Learning workspace:</span></span>

<span data-ttu-id="84d3c-183">Struttura del file settings.json:</span><span class="sxs-lookup"><span data-stu-id="84d3c-183">settings.json File structure:</span></span>

    {"workspace":{
    "id"                  : "ENTER YOUR AZUREML WORKSPACE ID",
    "authorization_token" : "ENTER YOUR AZUREML AUTH TOKEN"
    }}


#### <a name="build-a-model-in-r-and-publish-it-in-azure-machine-learning"></a><span data-ttu-id="84d3c-184">Compilare un modello in R e pubblicarlo in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="84d3c-184">Build a model in R and publish it in Azure Machine Learning</span></span>
    library(AzureML)
    ws <- workspace(config="~/.azureml/settings.json")

    if(!require("lme4")) install.packages("lme4")
    library(lme4)
    set.seed(1)
    train <- sleepstudy[sample(nrow(sleepstudy), 120),]
    m <- lm(Reaction ~ Days + Subject, data = train)

    # Define a prediction function to publish based on the model:
    sleepyPredict <- function(newdata){
          predict(m, newdata=newdata)
    }

    ep <- publishWebService(ws, fun = sleepyPredict, name="sleepy lm", inputSchema = sleepstudy, data.frame=TRUE)

#### <a name="consume-the-model-deployed-in-azure-machine-learning"></a><span data-ttu-id="84d3c-185">Utilizzare il modello distribuito in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="84d3c-185">Consume the model deployed in Azure Machine Learning</span></span>
<span data-ttu-id="84d3c-186">Per usare il modello da un'applicazione client si usa la libreria di Azure Machine Learning per cercare per nome il servizio Web pubblicato usando la chiamata API `services` per determinare l'endpoint.</span><span class="sxs-lookup"><span data-stu-id="84d3c-186">To consume the model from a client application, we use the Azure Machine Learning library to look up the published web service by name using the `services` API call to determine the endpoint.</span></span> <span data-ttu-id="84d3c-187">Sarà quindi sufficiente chiamare la funzione `consume` e passare il frame di dati di cui eseguire la stima.</span><span class="sxs-lookup"><span data-stu-id="84d3c-187">Then you just call the `consume` function and pass in the data frame to be predicted.</span></span>
<span data-ttu-id="84d3c-188">Il codice seguente consente di utilizzare il modello pubblicato come servizio Web di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="84d3c-188">The following code is used to consume the model published as an Azure Machine Learning web service.</span></span>

    library(AzureML)
    library(lme4)
    ws <- workspace(config="~/.azureml/settings.json")

    s <-  services(ws, name = "sleepy lm")
    s <- tail(s, 1) # use the last published function, in case of duplicate function names

    ep <- endpoints(ws, s)

    # OK, try this out, and compare with raw data
    ans = consume(ep, sleepstudy)$ans

<span data-ttu-id="84d3c-189">Altre informazioni sulla libreria R di Azure Machine Learning sono disponibili [qui](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).</span><span class="sxs-lookup"><span data-stu-id="84d3c-189">More information about the Azure Machine Learning R library can be found [here](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).</span></span>

## <a name="4-administer-your-azure-resources-using-azure-portal-or-powershell"></a><span data-ttu-id="84d3c-190">4. Amministrare le risorse di Azure usando il portale di Azure o PowerShell</span><span class="sxs-lookup"><span data-stu-id="84d3c-190">4. Administer your Azure resources using Azure portal or Powershell</span></span>
<span data-ttu-id="84d3c-191">DSVM non solo consente di compilare la soluzione di analisi in locale nella macchina virtuale, ma anche di accedere ai servizi nel cloud di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="84d3c-191">The DSVM not only allows you to build your analytics solution locally on the virtual machine, but also allows you to access services on Microsoft's Azure cloud.</span></span> <span data-ttu-id="84d3c-192">Azure offre diversi servizi di calcolo, archiviazione e analisi dei dati e altri servizi amministrabili e accessibili da DSVM.</span><span class="sxs-lookup"><span data-stu-id="84d3c-192">Azure provides several compute, storage, data analytics services and other services that you can administer and access from your DSVM.</span></span>

<span data-ttu-id="84d3c-193">Per amministrare la sottoscrizione di Azure e le risorse cloud, è possibile usare il browser e accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="84d3c-193">To administer your Azure subscription and cloud resources you can use your browser and point to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="84d3c-194">È anche possibile usare Azure PowerShell per amministrare le risorse e la sottoscrizione di Azure con uno script.</span><span class="sxs-lookup"><span data-stu-id="84d3c-194">You can also use Azure Powershell to administer your Azure subscription and resources via a script.</span></span>
<span data-ttu-id="84d3c-195">È possibile eseguire Azure PowerShell da un collegamento "Microsoft Azure PowerShell" sul desktop o nel menu Start.</span><span class="sxs-lookup"><span data-stu-id="84d3c-195">You can run Azure Powershell from a shortcut on the desktop or from the start menu titled "Microsoft Azure Powershell".</span></span> <span data-ttu-id="84d3c-196">Per altre informazioni su come amministrare le risorse e la sottoscrizione di Azure con gli script di Windows PowerShell, vedere la [documentazione di Microsoft Azure PowerShell](../powershell-azure-resource-manager.md) .</span><span class="sxs-lookup"><span data-stu-id="84d3c-196">Refer to [Microsoft Azure Powershell documentation](../powershell-azure-resource-manager.md) for more information on how you can administer your Azure subscription and resources using Windows Powershell scripts.</span></span>

## <a name="5-extend-your-storage-space-with-a-shared-file-system"></a><span data-ttu-id="84d3c-197">5. Estendere lo spazio di archiviazione con un file system condiviso</span><span class="sxs-lookup"><span data-stu-id="84d3c-197">5. Extend your storage space with a shared file system</span></span>
<span data-ttu-id="84d3c-198">Gli esperti di gestione dati possono condividere grandi set di dati, codice o alte risorse all'interno del team.</span><span class="sxs-lookup"><span data-stu-id="84d3c-198">Data scientists can share large datasets, code or other resources within the team.</span></span> <span data-ttu-id="84d3c-199">In DSVM sono disponibili circa 70 GB di spazio.</span><span class="sxs-lookup"><span data-stu-id="84d3c-199">The DSVM itself has about 70GB of space available.</span></span> <span data-ttu-id="84d3c-200">Per estendere lo spazio di archiviazione, è possibile usare il Servizio file di Azure e installarlo in DSVM o accedervi tramite l'API REST.</span><span class="sxs-lookup"><span data-stu-id="84d3c-200">To extend your storage, you can use the Azure File Service and either mount it on the DSVM or access it via a REST API.</span></span>   

> [!NOTE]
> <span data-ttu-id="84d3c-201">La quantità massima di spazio della condivisione del Servizio file di Azure è di 5 TB e il limite delle dimensioni dei singoli file è di 1 TB.</span><span class="sxs-lookup"><span data-stu-id="84d3c-201">The maximum space of the Azure File Service share is 5TB and individual file size limit is 1TB.</span></span>   
> 
> 

<span data-ttu-id="84d3c-202">È possibile usare Azure Powershell per creare una condivisione del Servizio file di Azure.</span><span class="sxs-lookup"><span data-stu-id="84d3c-202">You can use Azure Powershell to create an Azure File Service share.</span></span> <span data-ttu-id="84d3c-203">Ecco lo script da eseguire in Azure PowerShell per creare una condivisione del Servizio file di Azure.</span><span class="sxs-lookup"><span data-stu-id="84d3c-203">Here is the script to run under Azure PowerShell to create an Azure File service share.</span></span>

    # Authenticate to Azure.
    Login-AzureRmAccount
    # Select your subscription
    Get-AzureRmSubscription –SubscriptionName "<your subscription name>" | Select-AzureRmSubscription
    # Create a new resource group.
    New-AzureRmResourceGroup -Name <dsvmdatarg>
    # Create a new storage account. You can reuse existing storage account if you wish.
    New-AzureRmStorageAccount -Name <mydatadisk> -ResourceGroupName <dsvmdatarg> -Location "<Azure Data Center Name For eg. South Central US>" -Type "Standard_LRS"
    # Set your current working storage account
    Set-AzureRmCurrentStorageAccount –ResourceGroupName "<dsvmdatarg>" –StorageAccountName <mydatadisk>

    # Create a Azure File Service Share
    $s = New-AzureStorageShare <<teamsharename>>
    # Create a directory under the FIle share. You can give it any name
    New-AzureStorageDirectory -Share $s -Path <directory name>
    # List the share to confirm that everything worked
    Get-AzureStorageFile -Share $s


<span data-ttu-id="84d3c-204">A questo punto, dopo avere creato una condivisione file di Azure, è possibile installarla in una macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="84d3c-204">Now that you have created an Azure file share, you can mount it in any virtual machine in Azure.</span></span> <span data-ttu-id="84d3c-205">È consigliabile che la VM sia nello stesso data center di Azure dell'account di archiviazione per evitare la latenza e gli addebiti per il trasferimento dei dati.</span><span class="sxs-lookup"><span data-stu-id="84d3c-205">It is highly recommended that the VM is in same Azure data center as the storage account to avoid latency and data transfer charges.</span></span> <span data-ttu-id="84d3c-206">Ecco i comandi per installare l'unità in DSVM, che è possibile eseguire in Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="84d3c-206">Here are the commands to mount the drive on the DSVM that you can run on Azure Powershell.</span></span>

    # Get storage key of the storage account that has the Azure file share from Azure portal. Store it securely on the VM to avoid prompted in next command.
    cmdkey /add:<<mydatadisk>>.file.core.windows.net /user:<<mydatadisk>> /pass:<storage key>

    # Mount the Azure file share as Z: drive on the VM. You can chose another drive letter if you wish
    net use z:  \\<mydatadisk>.file.core.windows.net\<<teamsharename>>


<span data-ttu-id="84d3c-207">Ora è possibile accedere a questa unità come a qualsiasi altra unità della VM.</span><span class="sxs-lookup"><span data-stu-id="84d3c-207">Now you can access this drive as you would any normal drive on the VM.</span></span>

## <a name="6-share-code-with-your-team-using-github"></a><span data-ttu-id="84d3c-208">6. Condividere il codice con il team usando GitHub</span><span class="sxs-lookup"><span data-stu-id="84d3c-208">6. Share code with your team using GitHub</span></span>
<span data-ttu-id="84d3c-209">GitHub è un archivio di codice dove è possibile trovare numerosi codici di esempio e origini per strumenti diversi usando svariate tecnologie condivise dalla community degli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="84d3c-209">GitHub is a code repository where you can find a lot of sample code and sources for different tools using various technologies shared by the developer community.</span></span> <span data-ttu-id="84d3c-210">Usa Git come tecnologia per tenere traccia delle versioni dei file di codice e per archiviarle.</span><span class="sxs-lookup"><span data-stu-id="84d3c-210">It uses Git as the technology to track and store versions of the code files.</span></span> <span data-ttu-id="84d3c-211">GitHub è anche una piattaforma in cui è possibile creare il proprio archivio in cui archiviare la documentazione e il codice condiviso del team, implementare il controllo della versione e anche controllare chi ha l'accesso per visualizzare il codice e per contribuirvi.</span><span class="sxs-lookup"><span data-stu-id="84d3c-211">GitHub is also a platform where you can create your own repository to store your team's shared code and documentation, implement version control and also control who have access to view and contribute code.</span></span> <span data-ttu-id="84d3c-212">Per altre informazioni sull'uso di Git, visitare le [pagine della guida di GitHub](https://help.github.com/).</span><span class="sxs-lookup"><span data-stu-id="84d3c-212">Please visit the [GitHub help pages](https://help.github.com/) for more information on using Git.</span></span> <span data-ttu-id="84d3c-213">È possibile usare GitHub per collaborare con il team, usare il codice sviluppato dalla community e contribuire al codice della community.</span><span class="sxs-lookup"><span data-stu-id="84d3c-213">You can use GitHub as one of the ways to collaborate with your team, use code developed by the community and contribute code back to the community.</span></span>

<span data-ttu-id="84d3c-214">In DSVM sono già caricati gli strumenti client sia nella riga di comando sia nella GUI per accedere al repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="84d3c-214">The DSVM already comes loaded with client tools on both command-line as well GUI to access GitHub repository.</span></span> <span data-ttu-id="84d3c-215">Lo strumento da riga di comando per usare con Git e GitHub si chiama Git Bash.</span><span class="sxs-lookup"><span data-stu-id="84d3c-215">The command-line tool to work with Git and GitHub is called Git Bash.</span></span> <span data-ttu-id="84d3c-216">Visual Studio installato in DSVM include le estensioni Git.</span><span class="sxs-lookup"><span data-stu-id="84d3c-216">Visual Studio installed on the DSVM has the Git extensions.</span></span> <span data-ttu-id="84d3c-217">È possibile trovare le icone di avvio per questi strumenti nel menu Start e sul desktop.</span><span class="sxs-lookup"><span data-stu-id="84d3c-217">You can find start-up icons for these tools on the start menu and the desktop.</span></span>

<span data-ttu-id="84d3c-218">Per scaricare il codice da un repository GitHub, usare il comando ```git clone```.</span><span class="sxs-lookup"><span data-stu-id="84d3c-218">To download code from a GitHub repository you use the ```git clone``` command.</span></span> <span data-ttu-id="84d3c-219">Ad esempio, per scaricare il repository di analisi scientifica dei dati pubblicato da Microsoft nella directory corrente, è possibile eseguire il comando seguente in ```git-bash```.</span><span class="sxs-lookup"><span data-stu-id="84d3c-219">For example to download data science repository published by Microsoft into the current directory you can run the following command once you are in ```git-bash```.</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="84d3c-220">In Visual Studio è possibile eseguire la stessa operazione di clonazione.</span><span class="sxs-lookup"><span data-stu-id="84d3c-220">In Visual Studio, you can do the same clone operation.</span></span> <span data-ttu-id="84d3c-221">Per accedere agli strumenti Git e GitHub in Visual Studio, vedere lo screenshot seguente.</span><span class="sxs-lookup"><span data-stu-id="84d3c-221">The  following screen-shot shows how to access Git and GitHub tools in Visual Studio.</span></span>

![Git in Visual Studio](./media/machine-learning-data-science-vm-do-ten-things/VSGit.PNG)

<span data-ttu-id="84d3c-223">In github.com sono disponibili altre informazioni sull'uso di Git per lavorare con l'archivio GitHub da diverse risorse. Il [foglio informativo](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) è un riferimento utile.</span><span class="sxs-lookup"><span data-stu-id="84d3c-223">You can find more information on using Git to work with your GitHub repository from several resources available on github.com. The [cheat sheet](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) is a useful reference.</span></span>

## <a name="7-access-various-azure-data-and-analytics-services"></a><span data-ttu-id="84d3c-224">7. Accedere a diversi servizi dati e analisi di Azure</span><span class="sxs-lookup"><span data-stu-id="84d3c-224">7. Access various Azure data and analytics services</span></span>
### <a name="azure-blob"></a><span data-ttu-id="84d3c-225">BLOB Azure</span><span class="sxs-lookup"><span data-stu-id="84d3c-225">Azure Blob</span></span>
<span data-ttu-id="84d3c-226">BLOB di Azure è una risorsa di archiviazione cloud conveniente e affidabile per piccole e grandi quantità di dati.</span><span class="sxs-lookup"><span data-stu-id="84d3c-226">Azure blob is a reliable, economical cloud storage for data big and small.</span></span> <span data-ttu-id="84d3c-227">Si vedrà ora come è possibile spostare dati nel BLOB di Azure e accedere ai dati archiviati in un BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="84d3c-227">Let us look at how you can move data to Azure Blob and access data stored in an Azure Blob.</span></span>

<span data-ttu-id="84d3c-228">**Prerequisito**</span><span class="sxs-lookup"><span data-stu-id="84d3c-228">**Prerequisite**</span></span>

* <span data-ttu-id="84d3c-229">**Creare l'account di archiviazione BLOB di Azure nel [portale di Azure](https://portal.azure.com).**</span><span class="sxs-lookup"><span data-stu-id="84d3c-229">**Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).**</span></span>

![Create_Azure_Blob](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="84d3c-231">Verificare che lo strumento da riga di comando AzCopy preinstallato sia disponibile in ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```.</span><span class="sxs-lookup"><span data-stu-id="84d3c-231">Confirm that the pre-installed command-line AzCopy tool is found at ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```.</span></span> <span data-ttu-id="84d3c-232">È possibile aggiungere la directory contenente il file azcopy.exe alla variabile di ambiente PATH per evitare di digitare il percorso completo del comando quando si esegue lo strumento.</span><span class="sxs-lookup"><span data-stu-id="84d3c-232">You can add the directory containing the azcopy.exe to your PATH environment variable to avoid typing the full command path when running this tool.</span></span> <span data-ttu-id="84d3c-233">Per altre informazioni su AzCopy, vedere la [documentazione di AzCopy](../storage/common/storage-use-azcopy.md)</span><span class="sxs-lookup"><span data-stu-id="84d3c-233">For more info on AzCopy tool please refer to [AzCopy documentation](../storage/common/storage-use-azcopy.md)</span></span>
* <span data-ttu-id="84d3c-234">Avviare lo strumento Esplora archivi di Azure.</span><span class="sxs-lookup"><span data-stu-id="84d3c-234">Start the Azure Storage Explorer tool.</span></span> <span data-ttu-id="84d3c-235">È possibile scaricarlo da [Esplora archivi di Microsoft Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="84d3c-235">It can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span> 

![AzureStorageExplorer_v4](./media/machine-learning-data-science-vm-do-ten-things/AzureStorageExplorer_v4.png)

<span data-ttu-id="84d3c-237">**Spostare i dati dalla VM al BLOB di Azure: AzCopy**</span><span class="sxs-lookup"><span data-stu-id="84d3c-237">**Move data from VM to Azure Blob: AzCopy**</span></span>

<span data-ttu-id="84d3c-238">Per spostare i dati tra i file locali e l'archiviazione BLOB, è possibile usare AzCopy nella riga di comando o in PowerShell:</span><span class="sxs-lookup"><span data-stu-id="84d3c-238">To move data between your local files and blob storage, you can use AzCopy in command-line or PowerShell:</span></span>

    AzCopy /Source:C:\myfolder /Dest:https://<mystorageaccount>.blob.core.windows.net/<mycontainer> /DestKey:<storage account key> /Pattern:abc.txt

<span data-ttu-id="84d3c-239">Sostituire **C:\myfolder** con il percorso di archiviazione del file, **mystorageaccount** con il nome dell'account di archiviazione BLOB, **mycontainer** con il nome del contenitore e **storage account key** con la chiave di accesso alle risorse di archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="84d3c-239">Replace **C:\myfolder** to the path where your file is stored, **mystorageaccount** to your blob storage account name, **mycontainer** to the container name, **storage account key** to your blob storage access key.</span></span> <span data-ttu-id="84d3c-240">È possibile trovare le credenziali dell'account di archiviazione nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="84d3c-240">You can find your storage account credentials in [Azure portal](https://portal.azure.com).</span></span>

![StorageAccountCredential_v2](./media/machine-learning-data-science-vm-do-ten-things/StorageAccountCredential_v2.png)

<span data-ttu-id="84d3c-242">Eseguire il comando AzCopy in PowerShell o al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="84d3c-242">Run AzCopy command in PowerShell or from a command prompt.</span></span> <span data-ttu-id="84d3c-243">Ecco un esempio di utilizzo del comando AzCopy:</span><span class="sxs-lookup"><span data-stu-id="84d3c-243">Here is some example usage of AzCopy command:</span></span>

    # Copy *.sql from local machine to a Azure Blob
    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:"c:\Aaqs\Data Science Scripts" /Dest:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /DestKey:[ENTER STORAGE KEY] /S /Pattern:*.sql

    # Copy back all files from Azure Blob container to Local machine

    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Dest:"c:\Aaqs\Data Science Scripts\temp" /Source:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /SourceKey:[ENTER STORAGE KEY] /S



<span data-ttu-id="84d3c-244">Una volta eseguito il comando AzCopy per la copia in un BLOB di Azure, il file viene visualizzato in Azure Storage Explorer entro breve.</span><span class="sxs-lookup"><span data-stu-id="84d3c-244">Once you run your AzCopy command to copy to an Azure blob you see your file shows up in Azure Storage Explorer shortly.</span></span>

![AzCopy_run_finshed_Storage_Explorer_v3](./media/machine-learning-data-science-vm-do-ten-things/AzCopy_run_finshed_Storage_Explorer_v3.png)

<span data-ttu-id="84d3c-246">**Spostare i dati dalla VM al BLOB di Azure: Azure Storage Explorer**</span><span class="sxs-lookup"><span data-stu-id="84d3c-246">**Move data from VM to Azure Blob: Azure Storage Explorer**</span></span>

<span data-ttu-id="84d3c-247">È anche possibile caricare i dati dal file locale nella VM usando Azure Storage Explorer:</span><span class="sxs-lookup"><span data-stu-id="84d3c-247">You can also upload data from the local file in your VM using Azure Storage Explorer:</span></span>

* <span data-ttu-id="84d3c-248">Per caricare dati in un contenitore, selezionare il contenitore di destinazione e fare clic sul pulsante **Carica**.![Caricare in Storage Explorer](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span><span class="sxs-lookup"><span data-stu-id="84d3c-248">To upload data to a container, select the target container and click the **Upload** button.![Upload in Storage Explorer](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span></span>
* <span data-ttu-id="84d3c-249">Fare clic su **...** a destra della casella **File**, selezionare uno o più file da caricare dal file system e fare clic su **Carica** per iniziare a caricare i file.![Caricare i file nel BLOB](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span><span class="sxs-lookup"><span data-stu-id="84d3c-249">Click on the **...** to the right of the **Files** box, select one or multiple files to upload from the file system and click **Upload** to begin uploading the files.![Upload files to blob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span></span>

<span data-ttu-id="84d3c-250">**Leggere i dati dal BLOB di Azure: modulo Reader di Machine Learning**</span><span class="sxs-lookup"><span data-stu-id="84d3c-250">**Read data from Azure Blob: Machine Learning reader module**</span></span>

<span data-ttu-id="84d3c-251">In Azure Machine Learning Studio è possibile usare un **modulo Import Data** per leggere i dati dal BLOB.</span><span class="sxs-lookup"><span data-stu-id="84d3c-251">In Azure Machine Learning Studio you can use an **Import Data module** to read data from your blob.</span></span>

![AML_ReaderBlob_Module_v3](./media/machine-learning-data-science-vm-do-ten-things/AML_ReaderBlob_Module_v3.png)

<span data-ttu-id="84d3c-253">**Leggere i dati dal BLOB di Azure: ODBC Python**</span><span class="sxs-lookup"><span data-stu-id="84d3c-253">**Read data from Azure Blob: Python ODBC**</span></span>

<span data-ttu-id="84d3c-254">È possibile usare la libreria **BlobService** per leggere i dati direttamente dal BLOB in Jupyter Notebook o in un programma Python.</span><span class="sxs-lookup"><span data-stu-id="84d3c-254">You can use **BlobService** library to read data directly from blob in a Jupyter Notebook or Python program.</span></span>

<span data-ttu-id="84d3c-255">Prima di tutto importare i pacchetti necessari:</span><span class="sxs-lookup"><span data-stu-id="84d3c-255">First, import required packages:</span></span>

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random

<span data-ttu-id="84d3c-256">Quindi collegare le credenziali dell'account BLOB di Azure e leggere i dati dal BLOB:</span><span class="sxs-lookup"><span data-stu-id="84d3c-256">Then plug in your Azure Blob account credentials and read data from Blob:</span></span>

    CONTAINERNAME = 'xxx'
    STORAGEACCOUNTNAME = 'xxxx'
    STORAGEACCOUNTKEY = 'xxxxxxxxxxxxxxxx'
    BLOBNAME = 'nyctaxidataset/nyctaxitrip/trip_data_1.csv'
    localfilename = 'trip_data_1.csv'
    LOCALDIRECTORY = os.getcwd()
    LOCALFILE =  os.path.join(LOCALDIRECTORY, localfilename)

    #download from blob
    t1 = time.time()
    blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
    blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILE)
    t2 = time.time()
    print(("It takes %s seconds to download "+BLOBNAME) % (t2 - t1))

    #unzipping downloaded files if needed
    #with zipfile.ZipFile(ZIPPEDLOCALFILE, "r") as z:
    #    z.extractall(LOCALDIRECTORY)

    df1 = pd.read_csv(LOCALFILE, header=0)
    df1.columns = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime','passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude']
    print 'the size of the data is: %d rows and  %d columns' % df1.shape

<span data-ttu-id="84d3c-257">I dati vengono letti come frame di dati:</span><span class="sxs-lookup"><span data-stu-id="84d3c-257">The data is read in as a data frame:</span></span>

![IPNB_data_readin](./media/machine-learning-data-science-vm-do-ten-things/IPNB_data_readin.PNG)

### <a name="azure-data-lake"></a><span data-ttu-id="84d3c-259">Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="84d3c-259">Azure Data Lake</span></span>
<span data-ttu-id="84d3c-260">Un Archivio Azure Data Lake è un repository con iperscalabilità per i carichi di lavoro di analisi dei Big Data compatibile con Hadoop Distributed File System (HDFS).</span><span class="sxs-lookup"><span data-stu-id="84d3c-260">Azure Data Lake Storage is a hyper-scale repository for big data analytics workloads and compatible with Hadoop Distributed File System (HDFS).</span></span> <span data-ttu-id="84d3c-261">Funziona con l'ecosistema Hadoop e con Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="84d3c-261">It works with both the Hadoop ecosystem and the Azure Data Lake Analytics.</span></span> <span data-ttu-id="84d3c-262">Verrà illustrato come è possibile spostare i dati nell'Archivio Azure Data Lake ed eseguire analisi con Analisi Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="84d3c-262">We show how you can move data into the Azure Data Lake Store and run analytics using Azure Data Lake Analytics.</span></span>

<span data-ttu-id="84d3c-263">**Prerequisito**</span><span class="sxs-lookup"><span data-stu-id="84d3c-263">**Prerequisite**</span></span>

* <span data-ttu-id="84d3c-264">Creare Azure Data Lake Analytics nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="84d3c-264">Create your Azure Data Lake Analytics in [Azure portal](https://portal.azure.com).</span></span>

![Azure_Data_Lake_Create_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_Create_v2.png)

* <span data-ttu-id="84d3c-266">**Azure Data Lake Tools** in **Visual Studio** disponibile da questo [collegamento](https://www.microsoft.com/download/details.aspx?id=49504) è già installato in Visual Studio Community Edition nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="84d3c-266">The  **Azure Data Lake Tools** in **Visual Studio** found at this  [link](https://www.microsoft.com/download/details.aspx?id=49504) is already installed on the Visual Studio Community Edition which is on the virtual machine.</span></span> <span data-ttu-id="84d3c-267">Dopo avere avviato Visual Studio e avere effettuato l'accesso alla sottoscrizione di Azure, l'archivio e l'account di Azure Data Analytics vengono visualizzati nel panello sinistro di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="84d3c-267">After starting Visual Studio and logging in your Azure subscription, you should see your Azure Data Analytics account and storage in the left panel of Visual Studio.</span></span>

![Azure_Data_Lake_PlugIn_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_PlugIn_v2.PNG)

<span data-ttu-id="84d3c-269">**Spostare i dati dalla VM a Data Lake: Azure Data Lake Explorer**</span><span class="sxs-lookup"><span data-stu-id="84d3c-269">**Move data from VM to Data Lake: Azure Data Lake Explorer**</span></span>

<span data-ttu-id="84d3c-270">È possibile usare **Azure Data Lake Explorer** per caricare i dati dai file locali della macchina virtuale nell'archivio di Data Lake.</span><span class="sxs-lookup"><span data-stu-id="84d3c-270">You can use **Azure Data Lake Explorer** to upload data from the local files in your Virtual Machine to Data Lake storage.</span></span>

![Azure_Data_Lake_UploadData](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_UploadData.PNG)

<span data-ttu-id="84d3c-272">È anche possibile creare una pipeline di dati per lo spostamento dei dati da e verso Azure Data Lake tramite [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="84d3c-272">You can also build a data pipeline to productionize your data movement to or from Azure Data Lake using the [Azure Data Factory(ADF)](https://azure.microsoft.com/services/data-factory/).</span></span> <span data-ttu-id="84d3c-273">Per una guida dettagliata della compilazione di pipeline di dati, vedere questo [articolo](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) .</span><span class="sxs-lookup"><span data-stu-id="84d3c-273">We refer you to this [article](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) to guide you through the steps to build the data pipelines.</span></span>

<span data-ttu-id="84d3c-274">**Leggere i dati dal BLOB di Azure a Data Lake: U-SQL**</span><span class="sxs-lookup"><span data-stu-id="84d3c-274">**Read data from Azure Blob to Data Lake: U-SQL**</span></span>

<span data-ttu-id="84d3c-275">Se i dati si trovano nell'archivio BLOB di Azure, è possibile leggerli direttamente dal BLOB di archiviazione di Azure nella query U-SQL.</span><span class="sxs-lookup"><span data-stu-id="84d3c-275">If your data resides in Azure Blob storage, you can directly read data from Azure storage blob in U-SQL query.</span></span> <span data-ttu-id="84d3c-276">Prima di scrivere la query U-SQL, verificare che l'account di archiviazione BLOB sia collegato ad Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="84d3c-276">Before composing your U-SQL query, make sure your blob storage account is linked to your Azure Data Lake.</span></span> <span data-ttu-id="84d3c-277">Passare al **portale di Azure**, individuare il dashboard di Azure Data Lake Analytics, fare clic su **Aggiungi origine dati**, selezionare **Archiviazione di Azure** come tipo di archiviazione e inserire il nome e la chiave dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="84d3c-277">Go to **Azure portal**, find your Azure Data Lake Analytics dashboard, click **Add Data Source**, select storage type to **Azure Storage** and plug in your Azure Storage Account Name and Key.</span></span> <span data-ttu-id="84d3c-278">Sarà ora possibile fare riferimento ai dati archiviati nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="84d3c-278">Then you are able to reference the data stored in the storage account.</span></span>

![Immettere l'account di archiviazione e la chiave](./media/machine-learning-data-science-vm-do-ten-things/Link_Blob_to_ADLA_v2.PNG)

<span data-ttu-id="84d3c-280">In Visual Studio è possibile leggere i dati dall'archivio BLOB, modificarli, progettare funzionalità e pubblicare i dati risultanti in Azure Data Lake o nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="84d3c-280">In Visual Studio, you can read data from blob storage, do some data manipulation, feature engineering, and output the resulting data to either Azure Data Lake or Azure Blob Storage.</span></span> <span data-ttu-id="84d3c-281">Quando si fa riferimento ai dati nell'archiviazione BLOB, usare **wasb://**; quando si fa riferimento ai dati in Azure Data Lake, usare **swbhdfs://**</span><span class="sxs-lookup"><span data-stu-id="84d3c-281">When you reference the data in blob storage, use **wasb://**; when you reference the data in Azure Data Lake, use **swbhdfs://**</span></span>

![Frame di dati](./media/machine-learning-data-science-vm-do-ten-things/USQL_Read_Blob_v2.PNG)

<span data-ttu-id="84d3c-283">È possibile usare le query U-SQL seguenti in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="84d3c-283">You may use the following U-SQL queries in Visual Studio:</span></span>

    @a =
        EXTRACT medallion string,
                hack_license string,
                vendor_id string,
                rate_code string,
                store_and_fwd_flag string,
                pickup_datetime string,
                dropoff_datetime string,
                passenger_count int,
                trip_time_in_secs double,
                trip_distance double,
                pickup_longitude string,
                pickup_latitude string,
                dropoff_longitude string,
                dropoff_latitude string

        FROM "wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Input Data File Name>"
        USING Extractors.Csv();

    @b =
        SELECT vendor_id,
        COUNT(medallion) AS cnt_medallion,
        SUM(passenger_count) AS cnt_passenger,
        AVG(trip_distance) AS avg_trip_dist,
        MIN(trip_distance) AS min_trip_dist,
        MAX(trip_distance) AS max_trip_dist,
        AVG(trip_time_in_secs) AS avg_trip_time
        FROM @a
        GROUP BY vendor_id;

    OUTPUT @b   
    TO "swebhdfs://<Azure Data Lake Storage Account Name>.azuredatalakestore.net/<Folder Name>/<Output Data File Name>"
    USING Outputters.Csv();

    OUTPUT @b   
    TO "wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Output Data File Name>"
    USING Outputters.Csv();



<span data-ttu-id="84d3c-284">Dopo che la query è stata inviata al server, viene visualizzato un diagramma che illustra lo stato del processo.</span><span class="sxs-lookup"><span data-stu-id="84d3c-284">After your query is submitted to the server, a diagram showing the status of your job is displayed.</span></span>

![Diagramma dello stato del processo](./media/machine-learning-data-science-vm-do-ten-things/USQL_Job_Status.PNG)

<span data-ttu-id="84d3c-286">**Effettuare una query dei dati in Data Lake: U-SQL**</span><span class="sxs-lookup"><span data-stu-id="84d3c-286">**Query data in Data Lake: U-SQL**</span></span>

<span data-ttu-id="84d3c-287">Dopo che il set di dati è stato inserito in Azure Data Lake, è possibile usare il [linguaggio U-SQL](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) per l'esecuzione di query e l'esplorazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="84d3c-287">After the dataset is ingested into Azure Data Lake, you can use [U-SQL language](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) to query and explore the data.</span></span> <span data-ttu-id="84d3c-288">Il linguaggio U-SQL è simile a T-SQL, ma combina alcune funzionalità di C# in modo che gli utenti possano scrivere moduli personalizzati, funzioni definite dall'utente e così via. È possibile usare gli script del passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="84d3c-288">U-SQL language is similar to T-SQL, but combines some features from C# so that users can write customized modules, user-defined functions, and etc. You can use the scripts in the previous step.</span></span>

<span data-ttu-id="84d3c-289">Dopo l'invio della query al server, in **Azure Data Lake Explorer** sarà disponibile il file tripdata_summary.CSV. Per visualizzare i dati in anteprima, fare clic sul file con il pulsante destro del mouse.</span><span class="sxs-lookup"><span data-stu-id="84d3c-289">After the query is submitted to server, tripdata_summary.CSV can be found shortly in **Azure Data Lake Explorer**, you may preview the data by right-click the file.</span></span>

![File in Azure Data Lake Explorer](./media/machine-learning-data-science-vm-do-ten-things/USQL_create_summary.png)

<span data-ttu-id="84d3c-291">Per visualizzare le informazioni del file:</span><span class="sxs-lookup"><span data-stu-id="84d3c-291">To see the file information:</span></span>

![Riepilogo del file](./media/machine-learning-data-science-vm-do-ten-things/USQL_tripdata_summary.png)

### <a name="hdinsight-hadoop-clusters"></a><span data-ttu-id="84d3c-293">Cluster Hadoop di HDInsight</span><span class="sxs-lookup"><span data-stu-id="84d3c-293">HDInsight Hadoop Clusters</span></span>
<span data-ttu-id="84d3c-294">Azure HDInsight è un servizio di Apache Hadoop, Spark, HBase e Storm gestito nel cloud.</span><span class="sxs-lookup"><span data-stu-id="84d3c-294">Azure HDInsight is a managed Apache Hadoop, Spark, HBase, and Storm service on the cloud.</span></span> <span data-ttu-id="84d3c-295">È possibile utilizzare facilmente i cluster Azure HDInsight dalla macchina virtuale di analisi scientifica dei dati.</span><span class="sxs-lookup"><span data-stu-id="84d3c-295">You can work easily with Azure HDInsight clusters from the data science virtual machine.</span></span>

<span data-ttu-id="84d3c-296">**Prerequisito**</span><span class="sxs-lookup"><span data-stu-id="84d3c-296">**Prerequisite**</span></span>

* <span data-ttu-id="84d3c-297">Creare l'account di archiviazione BLOB di Azure nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="84d3c-297">Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="84d3c-298">Questo account di archiviazione viene usato per archiviare i dati per i cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="84d3c-298">This storage account is used to store data for HDInsight clusters.</span></span>

![Creare un account di archiviazione BLOB di Azure](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="84d3c-300">Personalizzare i cluster Hadoop di Azure HDInsight nel [portale di Azure](machine-learning-data-science-customize-hadoop-cluster.md)</span><span class="sxs-lookup"><span data-stu-id="84d3c-300">Customize Azure HDInsight Hadoop Clusters from [Azure portal](machine-learning-data-science-customize-hadoop-cluster.md)</span></span>
  
  * <span data-ttu-id="84d3c-301">È necessario collegare l'account di archiviazione creato al cluster HDInsight al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="84d3c-301">You must link the storage account created with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="84d3c-302">Questo account di archiviazione viene usato per accedere ai dati che possono essere elaborati all'interno del cluster.</span><span class="sxs-lookup"><span data-stu-id="84d3c-302">This storage account is used for accessing data that can be processed within the cluster.</span></span>

![Collegamento all'account di archiviazione creato con il cluster HDInsight](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_v4.PNG)

* <span data-ttu-id="84d3c-304">È necessario abilitare l' **accesso remoto** al nodo head del cluster dopo la creazione.</span><span class="sxs-lookup"><span data-stu-id="84d3c-304">You must enable **Remote Access** to the head node of the cluster after it is created.</span></span> <span data-ttu-id="84d3c-305">Ricordare le credenziali di accesso remoto specificate qui, diverse da quelle specificate durante la creazione del cluster, poiché saranno necessarie per completare la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="84d3c-305">Remember the remote access credentials you specify here (different from those specified for the cluster at its creation): you need them in the subsequent procedure.</span></span>

![Abilitare l'accesso remoto](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_dashboard_v3.PNG)

* <span data-ttu-id="84d3c-307">Creare un'area di lavoro di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="84d3c-307">Create an Azure Machine Learning workspace.</span></span> <span data-ttu-id="84d3c-308">Gli esperimenti di Machine Learning vengono archiviati in questa area di lavoro di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="84d3c-308">Your Machine Learning Experiments are stored in this Machine Learning workspace.</span></span> <span data-ttu-id="84d3c-309">Selezionare le opzioni evidenziate nel portale, come illustrato nello screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="84d3c-309">Select the highlighted options in Portal as shown in the following screenshot:</span></span>

![Creare un'area di lavoro di Machine Learning di Azure](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space.PNG)

* <span data-ttu-id="84d3c-311">Immettere quindi i parametri per l'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="84d3c-311">Then enter the parameters for your workspace</span></span>

![Immettere i parametri dell'area di lavoro di Machine Learning](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space_step2_v2.PNG)

* <span data-ttu-id="84d3c-313">Caricare i dati con IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="84d3c-313">Upload data using IPython Notebook.</span></span> <span data-ttu-id="84d3c-314">Importare prima di tutto i pacchetti necessari, inserire le credenziali, creare un database nell'account di archiviazione, quindi caricare i dati nei cluster HDI.</span><span class="sxs-lookup"><span data-stu-id="84d3c-314">First import required packages, plug in credentials, create a db in your storage account, then load data to HDI clusters.</span></span>

        #Import required Packages
        import pyodbc
        import time as time
        import json
        import os
        import urllib
        import urllib2
        import warnings
        import re
        import pandas as pd
        import matplotlib.pyplot as plt
        from azure.storage.blob import BlobService
        warnings.filterwarnings("ignore", category=UserWarning, module='urllib2')


        #Create the connection to Hive using ODBC
        SERVER_NAME='xxx.azurehdinsight.net'
        DATABASE_NAME='nyctaxidb'
        USERID='xxx'
        PASSWORD='xxxx'
        DB_DRIVER='Microsoft Hive ODBC Driver'
        driver = 'DRIVER={' + DB_DRIVER + '}'
        server = 'Host=' + SERVER_NAME + ';Port=443'
        database = 'Schema=' + DATABASE_NAME
        hiveserv = 'HiveServerType=2'
        auth = 'AuthMech=6'
        uid = 'UID=' + USERID
        pwd = 'PWD=' + PASSWORD
        CONNECTION_STRING = ';'.join([driver,server,database,hiveserv,auth,uid,pwd])
        connection = pyodbc.connect(CONNECTION_STRING, autocommit=True)
        cursor=connection.cursor()


        #Create Hive database and tables
        queryString = "create database if not exists nyctaxidb;"
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.trip
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            rate_code string,
                            store_and_fwd_flag string,
                            pickup_datetime string,
                            dropoff_datetime string,
                            passenger_count int,
                            trip_time_in_secs double,
                            trip_distance double,
                            pickup_longitude double,
                            pickup_latitude double,
                            dropoff_longitude double,
                            dropoff_latitude double)  
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.fare
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            pickup_datetime string,
                            payment_type string,
                            fare_amount double,
                            surcharge double,
                            mta_tax double,
                            tip_amount double,
                            tolls_amount double,
                            total_amount double)
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)


        #Upload data from blob storage to HDI cluster
        for i in range(1,13):
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxitripraw2/trip_data_%d.csv' INTO TABLE nyctaxidb2.trip PARTITION (month=%d);"%(i,i)
            cursor.execute(queryString)
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxifareraw2/trip_fare_%d.csv' INTO TABLE nyctaxidb2.fare PARTITION (month=%d);"%(i,i)  
            cursor.execute(queryString)


* <span data-ttu-id="84d3c-315">In alternativa è possibile seguire questa [procedura dettagliata](machine-learning-data-science-process-hive-walkthrough.md) per caricare i dati relativi ai taxi di New York nel cluster HDI.</span><span class="sxs-lookup"><span data-stu-id="84d3c-315">Alternately,  you can follow this [walkthrough](machine-learning-data-science-process-hive-walkthrough.md) to upload NYC Taxi data to HDI cluster.</span></span> <span data-ttu-id="84d3c-316">I passaggi più importanti includono:</span><span class="sxs-lookup"><span data-stu-id="84d3c-316">Major steps include:</span></span>
  
  * <span data-ttu-id="84d3c-317">AzCopy: scaricare i file CSV compressi dal BLOB pubblico alla cartella locale</span><span class="sxs-lookup"><span data-stu-id="84d3c-317">AzCopy: download zipped CSV's from public blob to your local folder</span></span>
  * <span data-ttu-id="84d3c-318">AzCopy: caricare i file CSV decompressi dalla cartella locale al cluster HDI</span><span class="sxs-lookup"><span data-stu-id="84d3c-318">AzCopy: upload unzipped CSV's from local folder to HDI cluster</span></span>
  * <span data-ttu-id="84d3c-319">Accedere al nodo head del cluster Hadoop e preparare l'analisi esplorativa dei dati</span><span class="sxs-lookup"><span data-stu-id="84d3c-319">Log into the head node of Hadoop cluster and prepare for exploratory data analysis</span></span>

<span data-ttu-id="84d3c-320">Dopo aver caricato i dati nel cluster HDI, è possibile controllarli in Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="84d3c-320">After the data is loaded to HDI cluster, you can check your data in Azure Storage Explorer.</span></span> <span data-ttu-id="84d3c-321">Nel cluster HDI è stato creato un database nyctaxidb.</span><span class="sxs-lookup"><span data-stu-id="84d3c-321">And you have a database nyctaxidb created in HDI cluster.</span></span>

<span data-ttu-id="84d3c-322">**Esplorazione dei dati: query Hive in Python**</span><span class="sxs-lookup"><span data-stu-id="84d3c-322">**Data exploration: Hive Queries in Python**</span></span>

<span data-ttu-id="84d3c-323">Poiché i dati si trovano nel cluster Hadoop, è possibile usare il pacchetto pyodbc per connettersi ai cluster Hadoop ed eseguire una query sul database con Hive per l'esplorazione e la progettazione di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="84d3c-323">Since the data is in Hadoop cluster, you can use the pyodbc package to connect to Hadoop Clusters and query database using Hive to do exploration and feature engineering.</span></span> <span data-ttu-id="84d3c-324">È possibile visualizzare le tabelle esistenti create nel passaggio del prerequisito.</span><span class="sxs-lookup"><span data-stu-id="84d3c-324">You can view the existing tables we created in the prerequisite step.</span></span>

    queryString = """
        show tables in nyctaxidb2;
        """
    pd.read_sql(queryString,connection)


![Visualizzare tabelle esistenti](./media/machine-learning-data-science-vm-do-ten-things/Python_View_Existing_Tables_Hive_v3.PNG)

<span data-ttu-id="84d3c-326">Verrà ora esaminato il numero di record per ogni mese e le frequenze delle corse per le quali è stata lasciata una mancia o meno nella tabella delle corse:</span><span class="sxs-lookup"><span data-stu-id="84d3c-326">Let's look at the number of records in each month and the frequencies of tipped or not in the trip table:</span></span>

    queryString = """
        select month, count(*) from nyctaxidb.trip group by month;
        """
    results = pd.read_sql(queryString,connection)

    %matplotlib inline

    results.columns = ['month', 'trip_count']
    df = results.copy()
    df.index = df['month']
    df['trip_count'].plot(kind='bar')


![Tracciato del numero di record in ogni mese](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Number_Records_by_Month_v3.PNG)

    queryString = """
        SELECT tipped, COUNT(*) AS tip_freq
        FROM
        (
            SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
            FROM nyctaxidb.fare
        )tc
        GROUP BY tipped;
        """
    results = pd.read_sql(queryString,connection)

    results.columns = ['tipped', 'trip_count']
    df = results.copy()
    df.index = df['tipped']
    df['trip_count'].plot(kind='bar')


![Tracciato della frequenze delle mance](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Frequency_tip_or_not_v3.PNG)

<span data-ttu-id="84d3c-329">È anche possibile calcolare la distanza tra il punto di partenza e il punto di arrivo e quindi confrontarla con la distanza della corsa.</span><span class="sxs-lookup"><span data-stu-id="84d3c-329">We can also compute the distance between pickup location and dropoff location and then compare it to the trip distance.</span></span>

    queryString = """
                    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
                        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
                        *radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
                        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
                        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
                        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*
                        pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance
                        from nyctaxidb.trip
                        where month=1
                            and pickup_longitude between -90 and -30
                            and pickup_latitude between 30 and 90
                            and dropoff_longitude between -90 and -30
                            and dropoff_latitude between 30 and 90;
                """
    results = pd.read_sql(queryString,connection)
    results.head(5)


![Tabella di punti di partenza e punti di arrivo](./media/machine-learning-data-science-vm-do-ten-things/Exploration_compute_pickup_dropoff_distance_v2.PNG)

    results.columns = ['pickup_longitude', 'pickup_latitude', 'dropoff_longitude',
                       'dropoff_latitude', 'trip_distance', 'trip_time_in_secs', 'direct_distance']
    df = results.loc[results['trip_distance']<=100] #remove outliers
    df = df.loc[df['direct_distance']<=100] #remove outliers
    plt.scatter(df['direct_distance'], df['trip_distance'])


![Tracciato della distanza partenza/arrivo rispetto alla distanza delle corse](./media/machine-learning-data-science-vm-do-ten-things/Exploration_direct_distance_trip_distance_v2.PNG)

<span data-ttu-id="84d3c-332">Verrà ora preparato un set di dati sottocampionati (1%) per la modellazione.</span><span class="sxs-lookup"><span data-stu-id="84d3c-332">Now let's prepare a down-sampled (1%) set of data for modeling.</span></span> <span data-ttu-id="84d3c-333">È possibile usare questi dati nel modulo Reader di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="84d3c-333">We can use this data in Machine Learning reader module.</span></span>

        queryString = """
        create  table if not exists nyctaxi_downsampled_dataset_testNEW (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\\n'
        stored as textfile;
        """
        cursor.execute(queryString)

        --- now insert contents of the join into the preceding internal table

        queryString = """
        insert overwrite table nyctaxi_downsampled_dataset_testNEW
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class
        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance,
        rand() as sample_key

        from trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01
        """
        cursor.execute(queryString)

<span data-ttu-id="84d3c-334">Dopo poco, è possibile vedere che i dati sono stati caricati nei cluster Hadoop:</span><span class="sxs-lookup"><span data-stu-id="84d3c-334">After a while, you can see the data has been loaded in Hadoop clusters:</span></span>

    queryString = """
        select * from nyctaxi_downsampled_dataset limit 10;
        """
    cursor.execute(queryString)
    pd.read_sql(queryString,connection)


![Tabella di dati](./media/machine-learning-data-science-vm-do-ten-things/DownSample_Data_For_Modeling_v2.PNG)

<span data-ttu-id="84d3c-336">**Leggere i dati da HDI con il modulo Reader di Machine Learning**</span><span class="sxs-lookup"><span data-stu-id="84d3c-336">**Read data from HDI using Machine Learning: reader module**</span></span>

<span data-ttu-id="84d3c-337">È anche possibile usare il modulo **Reader** in Machine Learning Studio per accedere al database nel cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="84d3c-337">You may also use the **reader** module in Machine Learning Studio to access the database in Hadoop cluster.</span></span> <span data-ttu-id="84d3c-338">Collegare le credenziali dei cluster HDI e l'account di archiviazione di Azure per poter compilare modelli di Machine Learning usando il database nei cluster HDI.</span><span class="sxs-lookup"><span data-stu-id="84d3c-338">Plug in the credentials of your HDI clusters and Azure Storage Account to enable build ing machine learning models using database in HDI clusters.</span></span>

![Proprietà del modulo Reader](./media/machine-learning-data-science-vm-do-ten-things/AML_Reader_Hive.PNG)

<span data-ttu-id="84d3c-340">È quindi possibile visualizzare il set di dati con i punteggi:</span><span class="sxs-lookup"><span data-stu-id="84d3c-340">The scored dataset can then be viewed:</span></span>

![Visualizzare il set di dati con i punteggi](./media/machine-learning-data-science-vm-do-ten-things/AML_Model_Results.PNG)

### <a name="azure-sql-data-warehouse--databases"></a><span data-ttu-id="84d3c-342">Azure SQL Data Warehouse e database</span><span class="sxs-lookup"><span data-stu-id="84d3c-342">Azure SQL Data Warehouse & databases</span></span>
<span data-ttu-id="84d3c-343">Azure SQL Data Warehouse è un data warehouse elastico distribuito come servizio con l'esperienza di classe enterprise di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="84d3c-343">Azure SQL Data Warehouse is an elastic data warehouse as a service with enterprise-class SQL Server experience.</span></span>

<span data-ttu-id="84d3c-344">È possibile effettuare il provisioning di Azure SQL Data Warehouse seguendo le istruzioni fornite in questo [articolo](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="84d3c-344">You can provision your Azure SQL Data Warehouse by following the instructions provided in this [article](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md).</span></span> <span data-ttu-id="84d3c-345">Dopo il provisioning di Azure SQL Data Warehouse, è possibile seguire questa [procedura dettagliata](machine-learning-data-science-process-sqldw-walkthrough.md) per il caricamento dei dati, l'esplorazione e la modellazione usando i dati disponibili in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="84d3c-345">Once you provision your Azure SQL Data Warehouse, you can use this [walkthrough](machine-learning-data-science-process-sqldw-walkthrough.md) to do data upload, exploration and modeling using data within the SQL Data Warehouse.</span></span>

#### <a name="azure-cosmos-db"></a><span data-ttu-id="84d3c-346">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="84d3c-346">Azure Cosmos DB</span></span>
<span data-ttu-id="84d3c-347">Azure Cosmos DB è un database NoSQL sul cloud.</span><span class="sxs-lookup"><span data-stu-id="84d3c-347">Azure Cosmos DB is a NoSQL database in the cloud.</span></span> <span data-ttu-id="84d3c-348">Consente di utilizzare documenti come JSON e di archiviarli ed eseguire query su di essi.</span><span class="sxs-lookup"><span data-stu-id="84d3c-348">It allows you to work with documents like JSON and allows you to store and query the documents.</span></span>

<span data-ttu-id="84d3c-349">Per accedere ad Azure Cosmos DB da DSVM, è necessario eseguire questa procedura preliminare.</span><span class="sxs-lookup"><span data-stu-id="84d3c-349">You need to do the following per-requisites steps to access Azure Cosmos DB from the DSVM.</span></span>

1. <span data-ttu-id="84d3c-350">Installare l'SDK DocumentDB Python eseguendo ```pip install pydocumentdb``` al prompt dei comandi</span><span class="sxs-lookup"><span data-stu-id="84d3c-350">Install DocumentDB Python SDK (Run ```pip install pydocumentdb``` from command prompt)</span></span>
2. <span data-ttu-id="84d3c-351">Creare l'account e il database Azure Cosmos DB nel [portale di Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="84d3c-351">Create an Azure Cosmos DB account and a database from [Azure portal](https://portal.azure.com)</span></span>
3. <span data-ttu-id="84d3c-352">Scaricare "Azure Cosmos DB Migration Tool" da [qui](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) ed estrarlo nella directory desiderata</span><span class="sxs-lookup"><span data-stu-id="84d3c-352">Download "Azure Cosmos DB Migration Tool" from [here](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) and extract to a directory of your choice</span></span>
4. <span data-ttu-id="84d3c-353">Importare in Cosmos DB i dati JSON (dati sui vulcani) archiviati in un [BLOB pubblico](https://cahandson.blob.core.windows.net/samples/volcano.json) con i parametri di comando seguenti per lo strumento di migrazione, ovvero dtui.exe dalla directory in cui è stato installato Cosmos DB Migration Tool.</span><span class="sxs-lookup"><span data-stu-id="84d3c-353">Import JSON data (volcano data) stored on a [public blob](https://cahandson.blob.core.windows.net/samples/volcano.json) into Cosmos DB with following command parameters to the migration tool (dtui.exe from the directory where you installed the Cosmos DB Migration Tool).</span></span> <span data-ttu-id="84d3c-354">Immettere i percorsi di origine e di destinazione con questi parametri:</span><span class="sxs-lookup"><span data-stu-id="84d3c-354">Enter the source and target location with these parameters:</span></span>
   
    <span data-ttu-id="84d3c-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span><span class="sxs-lookup"><span data-stu-id="84d3c-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span></span>

<span data-ttu-id="84d3c-356">Dopo avere importato i dati è possibile passare a Jupyter e aprire il notebook denominato *DocumentDBSample* contenente il codice Python per accedere a DocumentDB ed eseguire alcune query di base.</span><span class="sxs-lookup"><span data-stu-id="84d3c-356">Once you import the data, you can go to Jupyter and open the notebook titled *DocumentDBSample* which contains python code to access DocumentDB and do some basic querying.</span></span> <span data-ttu-id="84d3c-357">Per altre informazioni su Cosmos DB, vedere la [pagina della documentazione](https://docs.microsoft.com/azure/cosmos-db/) del servizio.</span><span class="sxs-lookup"><span data-stu-id="84d3c-357">You can learn more about Cosmos DB by visiting the service [documentation page](https://docs.microsoft.com/azure/cosmos-db/).</span></span>

## <a name="8-build-reports-and-dashboard-using-the-power-bi-desktop"></a><span data-ttu-id="84d3c-358">8. Compilare report e dashboard usando Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="84d3c-358">8. Build reports and dashboard using the Power BI Desktop</span></span>
<span data-ttu-id="84d3c-359">Viene ora visualizzato in Power BI il file JSON sui vulcani usato nell'esempio precedente di Cosmos DB per ottenere informazioni visive sui dati.</span><span class="sxs-lookup"><span data-stu-id="84d3c-359">Let us visualize the Volcano JSON file that we saw in the preceding Cosmos DB example in Power BI to gain visual insights into the data.</span></span> <span data-ttu-id="84d3c-360">I passaggi dettagliati sono disponibili nell' [articolo relativo a Power BI](../cosmos-db/powerbi-visualize.md).</span><span class="sxs-lookup"><span data-stu-id="84d3c-360">Detailed steps are available in the [Power BI article](../cosmos-db/powerbi-visualize.md).</span></span> <span data-ttu-id="84d3c-361">Ecco i passaggi principali:</span><span class="sxs-lookup"><span data-stu-id="84d3c-361">Here are the high-level steps:</span></span>

1. <span data-ttu-id="84d3c-362">Aprire Power BI Desktop ed eseguire "Recupera dati".</span><span class="sxs-lookup"><span data-stu-id="84d3c-362">Open Power BI Desktop and do "Get Data".</span></span> <span data-ttu-id="84d3c-363">Specificare l'URL come: https://cahandson.blob.core.windows.net/samples/volcano.json</span><span class="sxs-lookup"><span data-stu-id="84d3c-363">Specify the URL as: https://cahandson.blob.core.windows.net/samples/volcano.json</span></span>
2. <span data-ttu-id="84d3c-364">Verranno visualizzati i record JSON importati come elenco.</span><span class="sxs-lookup"><span data-stu-id="84d3c-364">You should see the JSON records imported as a list</span></span>
3. <span data-ttu-id="84d3c-365">Convertire l'elenco in una tabella in modo che Power BI possa usare gli stessi dati.</span><span class="sxs-lookup"><span data-stu-id="84d3c-365">Convert the list to a table so Power BI can work with the same</span></span>
4. <span data-ttu-id="84d3c-366">Espandere le colonne facendo clic sull'icona di espansione, ovvero l'icona con "una freccia verso sinistra e una freccia verso destra" a destra della colonna.</span><span class="sxs-lookup"><span data-stu-id="84d3c-366">Expand the columns by clicking on the expand icon (the one with the "left arrow and a right arrow" icon on the right of the column)</span></span>
5. <span data-ttu-id="84d3c-367">La posizione è un campo "Record".</span><span class="sxs-lookup"><span data-stu-id="84d3c-367">Notice that location is a "Record" field.</span></span> <span data-ttu-id="84d3c-368">Espandere il record e selezionare solo le coordinate.</span><span class="sxs-lookup"><span data-stu-id="84d3c-368">Expand the record and select only the coordinates.</span></span> <span data-ttu-id="84d3c-369">La coordinata è una colonna elenco.</span><span class="sxs-lookup"><span data-stu-id="84d3c-369">Coordinate is a list column</span></span>
6. <span data-ttu-id="84d3c-370">Aggiungere una nuova colonna per convertire la colonna dell'elenco di coordinate in una colonna LatLong con valori delimitati da virgole concatenando i due elementi nel campo dell'elenco di coordinate con la formula ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.</span><span class="sxs-lookup"><span data-stu-id="84d3c-370">Add a new column to convert the list coordinate column into a comma separate LatLong column concatenating the two elements in the coordinate list field using the formula ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.</span></span>
7. <span data-ttu-id="84d3c-371">Convertire infine la colonna ```Elevation``` in Decimali e fare clic su **Chiudi** e **Applica**.</span><span class="sxs-lookup"><span data-stu-id="84d3c-371">Finally convert the ```Elevation``` column to Decimal and select the **Close** and **Apply**.</span></span>

<span data-ttu-id="84d3c-372">Anziché eseguire i passaggi precedenti, è possibile incollare il codice seguente che inserisce nello script i passaggi usati nell'editor avanzato in Power BI, in modo da poter scrivere le trasformazioni dei dati in un linguaggio di query.</span><span class="sxs-lookup"><span data-stu-id="84d3c-372">Instead of preceding steps, you can paste the following code that scripts out the steps used in the Advanced Editor in Power BI that allows you to write the data transformations in a query language.</span></span>

    let
        Source = Json.Document(Web.Contents("https://cahandson.blob.core.windows.net/samples/volcano.json")),
        #"Converted to Table" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
        #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted to Table", "Column1", {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}, {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}),
        #"Expanded Location" = Table.ExpandRecordColumn(#"Expanded Column1", "Location", {"coordinates"}, {"coordinates"}),
        #"Added Custom" = Table.AddColumn(#"Expanded Location", "LatLong", each Text.From([coordinates]{1})&","&Text.From([coordinates]{0})),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Elevation", type number}})
    in
        #"Changed Type"



<span data-ttu-id="84d3c-373">I dati sono ora inclusi nel modello di dati di Power BI.</span><span class="sxs-lookup"><span data-stu-id="84d3c-373">You now have the data in your Power BI data model.</span></span> <span data-ttu-id="84d3c-374">Power BI Desktop deve avere ora un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="84d3c-374">Your Power BI desktop should appear as follows:</span></span>

![Power BI Desktop](./media/machine-learning-data-science-vm-do-ten-things/PowerBIVolcanoData.png)

<span data-ttu-id="84d3c-376">È possibile avviare la compilazione di report e visualizzazioni usando il modello di dati.</span><span class="sxs-lookup"><span data-stu-id="84d3c-376">You can start building reports and visualizations using the data model.</span></span> <span data-ttu-id="84d3c-377">Per compilare un report, è possibile seguire i passaggi in questo [articolo relativo a Power BI](../cosmos-db/powerbi-visualize.md#build-the-reports) .</span><span class="sxs-lookup"><span data-stu-id="84d3c-377">You can follow the steps in this [Power BI article](../cosmos-db/powerbi-visualize.md#build-the-reports) to build a report.</span></span> <span data-ttu-id="84d3c-378">Il risultato finale è un report simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="84d3c-378">The end result is a report that looks like the following.</span></span>

![Visualizzazione report di Power BI Desktop - Connettore Power BI](./media/machine-learning-data-science-vm-do-ten-things/power_bi_connector_pbireportview2.png)

## <a name="9-dynamically-scale-your-dsvm-to-meet-your-project-needs"></a><span data-ttu-id="84d3c-380">9. Ridimensionare in modo dinamico DSVM per poter soddisfare le esigenze del progetto</span><span class="sxs-lookup"><span data-stu-id="84d3c-380">9. Dynamically scale your DSVM to meet your project needs</span></span>
<span data-ttu-id="84d3c-381">È possibile aumentare e ridurre le prestazioni di DSVM per soddisfare le esigenze del progetto.</span><span class="sxs-lookup"><span data-stu-id="84d3c-381">You can scale up and down the DSVM to meet your project needs.</span></span> <span data-ttu-id="84d3c-382">Se non è necessario usare la VM la sera o nei fine settimana, è sufficiente arrestarla dal [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="84d3c-382">If you don't need to use the VM in the evening or weekends, you can just shut down the VM from the [Azure portal](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="84d3c-383">Vengono addebitati i costi di calcolo se si usa solo il pulsante di arresto del sistema operativo nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="84d3c-383">You incur compute charges if you use just the Operating system shutdown button on the VM.</span></span>  
> 
> 

<span data-ttu-id="84d3c-384">Se è necessario gestire analisi su larga scala e si ha bisogno di più CPU e/o memoria e/o capacità disco, è possibile trovare un'ampia scelta di dimensioni di macchina virtuale in termini di core CPU, capacità di memoria e tipi di disco (incluse le unità SSD), che soddisfano qualsiasi esigenza di calcolo e di budget.</span><span class="sxs-lookup"><span data-stu-id="84d3c-384">If you need to handle some large-scale analysis and need more CPU and/or memory and/or disk capacity you can find a large choice of VM sizes in terms of CPU cores, memory capacity and disk types (including Solid state drives) that meet your compute and budgetary needs.</span></span> <span data-ttu-id="84d3c-385">L'elenco completo di VM con i rispettivi prezzi di calcolo orario è disponibile nella pagina [Prezzi di Macchine virtuali di Azure](https://azure.microsoft.com/pricing/details/virtual-machines/) .</span><span class="sxs-lookup"><span data-stu-id="84d3c-385">The full list of VMs along with their hourly compute pricing is available on the [Azure Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/) page.</span></span>

<span data-ttu-id="84d3c-386">Allo stesso modo, se le esigenze di capacità di elaborazione della VM diminuiscono, ad esempio se si è spostato un carico di lavoro principale in un cluster Hadoop o Spark, è possibile passare a un piano inferiore per il cluster dal [portale di Azure](https://portal.azure.com) tramite le impostazioni dell'istanza della VM.</span><span class="sxs-lookup"><span data-stu-id="84d3c-386">Similarly, if your need for VM processing capacity reduces (for example: you moved a major workload to a Hadoop or a Spark cluster), you can scale down the cluster from the [Azure portal](https://portal.azure.com) and going to the settings of your VM instance.</span></span> <span data-ttu-id="84d3c-387">Ecco uno screenshot.</span><span class="sxs-lookup"><span data-stu-id="84d3c-387">Here is a screenshot.</span></span>

![Impostazioni dell'istanza della VM](./media/machine-learning-data-science-vm-do-ten-things/VMScaling.PNG)

## <a name="10-install-additional-tools-on-your-virtual-machine"></a><span data-ttu-id="84d3c-389">10. Installare strumenti aggiuntivi nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="84d3c-389">10. Install additional tools on your virtual machine</span></span>
<span data-ttu-id="84d3c-390">Sono stati inclusi in un pacchetto diversi strumenti che consentono di soddisfare molte delle comuni esigenze di analisi dei dati e di risparmiare sia tempo, perché si evita di dover installare e configurare gli ambienti uno alla volta, sia denaro, perché si pagano solo le risorse usate.</span><span class="sxs-lookup"><span data-stu-id="84d3c-390">We have packaged several tools that we believe are able to address many of the common data analytics needs and that should save you time by avoiding having to install and configure your environments one by one and save you money by paying only for resources that you use.</span></span>

<span data-ttu-id="84d3c-391">È possibile sfruttare altri servizi dati e di analisi di Azure, come illustrato in questo articolo, per migliorare l'ambiente di analisi.</span><span class="sxs-lookup"><span data-stu-id="84d3c-391">You can leverage other Azure data and analytics services profiled in this article to enhance your analytics environment.</span></span> <span data-ttu-id="84d3c-392">È possibile che in alcuni casi siano necessari strumenti aggiuntivi, inclusi alcuni strumenti proprietari di terze parti.</span><span class="sxs-lookup"><span data-stu-id="84d3c-392">We understand that in some cases your needs may require additional tools, including some proprietary third-party tools.</span></span> <span data-ttu-id="84d3c-393">L'accesso amministrativo completo alla macchina virtuale consente di installare i nuovi strumenti necessari.</span><span class="sxs-lookup"><span data-stu-id="84d3c-393">You have full administrative access on the virtual machine to install new tools you need.</span></span> <span data-ttu-id="84d3c-394">È anche possibile installare pacchetti aggiuntivi in Python e in R non preinstallati.</span><span class="sxs-lookup"><span data-stu-id="84d3c-394">You can also install additional packages in Python and R that are not pre-installed.</span></span> <span data-ttu-id="84d3c-395">Per Python è possibile usare ```conda``` o ```pip```.</span><span class="sxs-lookup"><span data-stu-id="84d3c-395">For Python you can use either ```conda``` or ```pip```.</span></span> <span data-ttu-id="84d3c-396">Per R è possibile usare ```install.packages()``` nella console di R oppure usare l'IDE e scegliere "**Packages** -> **Install Packages...**" (Pacchetti -> Installa pacchetti...).</span><span class="sxs-lookup"><span data-stu-id="84d3c-396">For R you can use the ```install.packages()``` in the R console or use the IDE and choose "**Packages** -> **Install Packages...**".</span></span>

## <a name="summary"></a><span data-ttu-id="84d3c-397">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="84d3c-397">Summary</span></span>
<span data-ttu-id="84d3c-398">Queste sono solo alcune delle attività che è possibile eseguire nella macchina virtuale per l'analisi scientifica dei dati di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="84d3c-398">These are just some of the things you can do on the Microsoft Data Science Virtual Machine.</span></span> <span data-ttu-id="84d3c-399">Ce ne sono molte altre che è possibile eseguire per renderla un ambiente di analisi efficace.</span><span class="sxs-lookup"><span data-stu-id="84d3c-399">There are many more things you can do to make it an effective analytics environment.</span></span>

