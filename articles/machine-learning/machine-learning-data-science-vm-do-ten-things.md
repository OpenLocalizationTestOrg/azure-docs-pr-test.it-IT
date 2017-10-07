---
title: aaaTen operazioni da eseguire nella macchina virtuale di analisi scientifica dei dati di hello | Documenti Microsoft
description: "Eseguire varie attività di modellazione ed esplorazione dei dati in analisi scientifica dei dati hello macchina virtuale."
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
ms.openlocfilehash: 4dfe22f14f00208c63e26ce44b05123c9ac4b850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="ten-things-you-can-do-on-hello-data-science-virtual-machine"></a><span data-ttu-id="bfcc6-103">Dieci operazioni che è possibile eseguire su analisi scientifica dei dati hello macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="bfcc6-103">Ten things you can do on hello Data science Virtual Machine</span></span>
<span data-ttu-id="bfcc6-104">Hello Microsoft Data Science macchina virtuale (DSVM) è un ambiente di sviluppo dell'analisi scientifica dei dati potente che consente di tooperform varie attività di esplorazione e modellazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-104">hello Microsoft Data Science Virtual Machine (DSVM) is a powerful data science development environment that enables you tooperform various data exploration and modeling tasks.</span></span> <span data-ttu-id="bfcc6-105">Hello ambiente viene fornito già compilato e in dotazione con i dati più diffusi diversi strumenti analitica che consentono di tooget facile iniziare rapidamente con l'analisi per On-Premise, Cloud o ibrida distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-105">hello environment comes already built and bundled with several popular data analytics tools that make it easy tooget started quickly with your analysis for On-premises, Cloud or hybrid deployments.</span></span> <span data-ttu-id="bfcc6-106">Hello DSVM collabora a stretto contatto con molti servizi di Azure ed è in grado di tooread ed elaborare dati che sono già archiviati in Azure, Azure SQL Data Warehouse, Azure Data Lake, archiviazione di Azure o nel database di Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-106">hello DSVM works closely with many Azure services and is able tooread and process data that is already stored on Azure, in Azure SQL Data Warehouse, Azure Data Lake, Azure Storage, or in Azure Cosmos DB.</span></span> <span data-ttu-id="bfcc6-107">Può anche sfruttare altri strumenti di analisi come Azure Machine Learning e Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-107">It can also leverage other analytics tools such as Azure Machine Learning and Azure Data Factory.</span></span>

<span data-ttu-id="bfcc6-108">In questo articolo viene illustrato come toouse il tooperform DSVM analisi scientifica dei dati di varie attività e interagire con altri servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-108">In this article we walk you through how toouse your DSVM tooperform various data science tasks and interact with other Azure services.</span></span> <span data-ttu-id="bfcc6-109">Ecco alcune delle operazioni di hello che è possibile eseguire sul hello DSVM:</span><span class="sxs-lookup"><span data-stu-id="bfcc6-109">Here are some of hello things you can do on hello DSVM:</span></span>

1. <span data-ttu-id="bfcc6-110">Esplorare i dati e lo sviluppo di modelli in locale hello DSVM utilizzando Microsoft R Server, Python</span><span class="sxs-lookup"><span data-stu-id="bfcc6-110">Explore data and develop models locally on hello DSVM using Microsoft R Server, Python</span></span>
2. <span data-ttu-id="bfcc6-111">Usare un tooexperiment notebook Jupyter con i dati in un browser utilizzando una versione di pronto dell'organizzazione di R progettato per la scalabilità e prestazioni di Python 2, 3 Python, Microsoft R</span><span class="sxs-lookup"><span data-stu-id="bfcc6-111">Use a Jupyter notebook tooexperiment with your data on a browser using Python 2, Python 3, Microsoft R an enterprise ready version of R designed for scalability and performance</span></span>
3. <span data-ttu-id="bfcc6-112">Rendere operativi i modelli compilati usando R e Python in Azure Machine Learning in modo che le applicazioni client possano accedere ai modelli con una semplice interfaccia di servizi Web</span><span class="sxs-lookup"><span data-stu-id="bfcc6-112">Operationalize models built using R and Python on Azure Machine Learning so client applications can access your models using a simple web services interface</span></span>
4. <span data-ttu-id="bfcc6-113">Amministrare le risorse di Azure usando il portale di Azure o PowerShell</span><span class="sxs-lookup"><span data-stu-id="bfcc6-113">Administer your Azure resources using  Azure portal or Powershell</span></span>
5. <span data-ttu-id="bfcc6-114">Estendere lo spazio di archiviazione e condividere codice o set di dati su larga scala con l'intero team creando un archivio file di Azure come unità installabile in DSVM</span><span class="sxs-lookup"><span data-stu-id="bfcc6-114">Extend your storage space and share large-scale datasets / code across your whole team by creating an Azure File storage as a mountable drive on your DSVM</span></span>
6. <span data-ttu-id="bfcc6-115">Condividere codice con il team tramite GitHub e accedere repository utilizzando hello pre-installate client Git - Git Bash, GUI Git.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-115">Share code with your team using GitHub and access your repository using hello pre-installed Git clients - Git Bash, Git GUI.</span></span>
7. <span data-ttu-id="bfcc6-116">Accedere a diversi servizi dati e analisi di Azure, ad esempio Archiviazione BLOB di Azure, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse e database</span><span class="sxs-lookup"><span data-stu-id="bfcc6-116">Access various Azure data and analytics services like Azure blob storage, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse & databases</span></span>
8. <span data-ttu-id="bfcc6-117">Creare report e dashboard tramite Power BI Desktop pre-installato hello DSVM hello e distribuirle nel cloud hello</span><span class="sxs-lookup"><span data-stu-id="bfcc6-117">Build reports and dashboard using hello Power BI Desktop pre-installed on hello DSVM and deploy them on hello cloud</span></span>
9. <span data-ttu-id="bfcc6-118">Applicare la scalabilità dinamicamente il toomeet DSVM che richiesto dal progetto</span><span class="sxs-lookup"><span data-stu-id="bfcc6-118">Dynamically scale your DSVM toomeet your project needs</span></span>
10. <span data-ttu-id="bfcc6-119">Installare strumenti aggiuntivi nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="bfcc6-119">Install additional tools on your virtual machine</span></span>   

> [!NOTE]
> <span data-ttu-id="bfcc6-120">Spese aggiuntive si applicano per molti servizi hello dati aggiuntivi analitica e archiviazione elencate in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-120">Additional usage charges apply for many of hello additional data storage and analytics services listed in this article.</span></span> <span data-ttu-id="bfcc6-121">Consultare toohello [dei prezzi di Azure](https://azure.microsoft.com/pricing/) pagina per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-121">Please refer toohello [Azure Pricing](https://azure.microsoft.com/pricing/) page for details.</span></span>
> 
> 

<span data-ttu-id="bfcc6-122">**Prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="bfcc6-122">**Prerequisites**</span></span>

* <span data-ttu-id="bfcc6-123">È necessaria una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-123">You need an Azure subscription.</span></span> <span data-ttu-id="bfcc6-124">È possibile iscriversi per una versione di valutazione gratuita di Azure [qui](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="bfcc6-124">You can sign up for a free trial [here](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="bfcc6-125">Istruzioni per il provisioning di una macchina virtuale di analisi scientifica dei dati nel portale di Azure hello [la creazione di una macchina virtuale](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="bfcc6-125">Instructions for provisioning a Data Science Virtual Machine on hello Azure portal are available at [Creating a virtual machine](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).</span></span>

## <a name="1-explore-data-and-develop-models-using-microsoft-r-server-or-python"></a><span data-ttu-id="bfcc6-126">1. Esplorare dati e sviluppare modelli usando Microsoft R Server o Python</span><span class="sxs-lookup"><span data-stu-id="bfcc6-126">1. Explore data and develop models using Microsoft R Server or Python</span></span>
<span data-ttu-id="bfcc6-127">È possibile utilizzare linguaggi come R e Python toodo analitica i dati direttamente nel hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-127">You can use languages like R and Python toodo your data analytics right on hello DSVM.</span></span>

<span data-ttu-id="bfcc6-128">Per R, è possibile utilizzare un ambiente di sviluppo integrato denominato "Revolution R Enterprise 8.0" sono disponibili nel menu start hello o desktop hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-128">For R, you can use an IDE called "Revolution R Enterprise 8.0" that can be found on hello start menu or hello desktop.</span></span> <span data-ttu-id="bfcc6-129">Librerie aggiuntive sopra hello Apri origine/CRAN-R tooenable scalabile analitica e hello possibilità tooanalyze dati più grande delle dimensioni di memoria hello consentita in questo modo parallelo analisi blocchi forniti da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-129">Microsoft has provided additional libraries on top of hello Open source/CRAN-R tooenable scalable analytics and hello ability tooanalyze data larger than hello memory size allowed by doing parallel chunked analysis.</span></span> <span data-ttu-id="bfcc6-130">È anche possibile installare l'IDE R di desiderato, ad esempio [RStudio](https://www.rstudio.com/products/rstudio-desktop/).</span><span class="sxs-lookup"><span data-stu-id="bfcc6-130">You can also install an R IDE of your choice like [RStudio](https://www.rstudio.com/products/rstudio-desktop/).</span></span>

<span data-ttu-id="bfcc6-131">Per Python, è possibile utilizzare un IDE come Visual Studio Community Edition che ha hello strumenti Python per l'estensione di Visual Studio (PTVS) pre-installato.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-131">For Python, you can use an IDE like Visual Studio Community Edition which has hello Python Tools for Visual Studio (PTVS) extension pre-installed.</span></span> <span data-ttu-id="bfcc6-132">Per impostazione predefinita, in PTVS è configurato solo Python 2.7 di base, senza librerie di analisi come SciKit o Pandas.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-132">By default, only a basic Python 2.7 is configured on PTVS (without any analytics library like SciKit, Pandas).</span></span> <span data-ttu-id="bfcc6-133">In ordine tooenable Anaconda Python 2.7 e 3.5, è necessario seguente hello toodo:</span><span class="sxs-lookup"><span data-stu-id="bfcc6-133">In order tooenable Anaconda Python 2.7 and 3.5, you need toodo hello following:</span></span>

* <span data-ttu-id="bfcc6-134">Creare ambienti personalizzati per ogni versione passando troppo**strumenti** -> **Python Tools** -> **ambienti Python** e quindi fare clic su " **+ Personalizzato**"in Visual Studio 2015 Community Edition hello</span><span class="sxs-lookup"><span data-stu-id="bfcc6-134">Create custom environments for each version by navigating too**Tools** -> **Python Tools** -> **Python Environments** and then clicking "**+ Custom**" in hello Visual Studio 2015 Community Edition</span></span>
* <span data-ttu-id="bfcc6-135">Immettere una descrizione e impostare l'ambiente di hello percorsi prefisso come *c:\anaconda* per Anaconda Python 2.7 o *c:\anaconda\envs\py35* per Anaconda Python 3.5</span><span class="sxs-lookup"><span data-stu-id="bfcc6-135">Give a description and set hello environment prefix paths as *c:\anaconda* for Anaconda Python 2.7 OR *c:\anaconda\envs\py35* for Anaconda Python 3.5</span></span>
* <span data-ttu-id="bfcc6-136">Fare clic su **rilevamento automatico** e quindi **applica** ambiente hello toosave.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-136">Click **Auto Detect** and then **Apply** toosave hello environment.</span></span>

<span data-ttu-id="bfcc6-137">Di seguito è riportato il programma di installazione di hello ambiente personalizzato simile in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-137">Here is what hello custom environment setup looks like in Visual Studio.</span></span>

![Configurazione di PTVS](./media/machine-learning-data-science-vm-do-ten-things/PTVSSetup.png)

<span data-ttu-id="bfcc6-139">Vedere hello [documentazione PTVS](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) per altre informazioni su come toocreate ambienti Python.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-139">See hello [PTVS documentation](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) for additional details on how toocreate Python Environments.</span></span>

<span data-ttu-id="bfcc6-140">Ora è l'impostazione toocreate un nuovo progetto di Python.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-140">Now you are set up toocreate a new Python project.</span></span> <span data-ttu-id="bfcc6-141">Passare troppo**File** -> **New** -> **progetto** -> **Python** e selezionare il tipo di hello di Applicazione Python che si sta compilando.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-141">Navigate too**File** -> **New** -> **Project** -> **Python** and select hello type of Python application you are building.</span></span> <span data-ttu-id="bfcc6-142">È possibile impostare l'ambiente Python hello hello corrente progetto toohello versione desiderata (Anaconda 2.7 o 3.5): pulsante destro del mouse hello **ambiente Python**selezionare **gli ambienti Python Aggiungi/Rimuovi**, e quindi seleziona hello desiderato tooassociate ambiente progetto hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-142">You can set hello Python environment for hello current project toohello desired version (Anaconda 2.7 or 3.5): right-click hello **Python environment**, select **Add/Remove Python Environments**, and then select hello desired environment tooassociate with hello project.</span></span> <span data-ttu-id="bfcc6-143">È possibile trovare ulteriori informazioni sull'utilizzo di PTVS prodotto hello [documentazione](https://github.com/Microsoft/PTVS/wiki) pagina.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-143">You can find more information about working with PTVS on hello product [documentation](https://github.com/Microsoft/PTVS/wiki) page.</span></span>

## <a name="2-using-a-jupyter-notebook-tooexplore-and-model-your-data-with-python-or-r"></a><span data-ttu-id="bfcc6-144">2. Usando i dati di un modello e un server Jupyter Notebook tooexplore con Python o R</span><span class="sxs-lookup"><span data-stu-id="bfcc6-144">2. Using a Jupyter Notebook tooexplore and model your data with Python or R</span></span>
<span data-ttu-id="bfcc6-145">Hello Server Jupyter Notebook è un ambiente potente che fornisce basate su browser "IDE" per la modellazione e l'esplorazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-145">hello Jupyter Notebook is a powerful environment that provides a browser-based "IDE" for data exploration and modeling.</span></span> <span data-ttu-id="bfcc6-146">È possibile utilizzare Python 2, 3 Python o R (Open Source e Microsoft R Server hello) in un server Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-146">You can use Python 2, Python 3 or R (both Open Source and hello Microsoft R Server) in a Jupyter Notebook.</span></span>

<span data-ttu-id="bfcc6-147">hello toolaunch server Jupyter Notebook fare clic sull'icona del menu start hello / icona sul desktop denominato **server Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-147">toolaunch hello Jupyter Notebook click on hello start menu icon / desktop icon titled **Jupyter Notebook**.</span></span> <span data-ttu-id="bfcc6-148">In hello DSVM è inoltre possibile esplorare troppo "https://localhost:9999 /" tooaccess hello Jupiter Notebook.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-148">On hello DSVM you can also browse too"https://localhost:9999/" tooaccess hello Jupiter Notebook.</span></span> <span data-ttu-id="bfcc6-149">Se viene richiesto di immettere una password, usare le istruzioni fornite in hello ***come una password complessa nel server notebook jupyter hello toocreate*** sezione di hello [hello provisioning macchina virtuale di Microsoft Data Science](machine-learning-data-science-provision-vm.md)toocreate argomento un server Jupyter notebook hello tooaccess di una password complessa.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-149">If it prompts you for a password, use instructions provided in hello ***How toocreate a strong password on hello Jupyter notebook server*** section of hello [Provision hello Microsoft Data Science Virtual Machine](machine-learning-data-science-provision-vm.md) topic toocreate a strong password tooaccess hello Jupyter notebook.</span></span> 

<span data-ttu-id="bfcc6-150">Dopo aver aperto notebook hello, dovrebbe essere una directory che contiene alcuni blocchi appunti di esempio che sono sotto forma di pacchetto in hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-150">Once you have opened hello notebook, you should see a directory that contains a few example notebooks that are pre-packaged into hello DSVM.</span></span> <span data-ttu-id="bfcc6-151">A questo punto è possibile:</span><span class="sxs-lookup"><span data-stu-id="bfcc6-151">Now you can:</span></span>

* <span data-ttu-id="bfcc6-152">Fare clic sul codice hello toosee di hello notebook.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-152">click on hello notebook toosee hello code.</span></span>
* <span data-ttu-id="bfcc6-153">Eseguire ogni cella premendo **MAIUSC+INVIO**.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-153">execute each cell by pressing **SHIFT-ENTER**.</span></span>
* <span data-ttu-id="bfcc6-154">eseguire l'intero blocco hello facendo clic su **cella** -> **eseguire**</span><span class="sxs-lookup"><span data-stu-id="bfcc6-154">run hello entire notebook by clicking on **Cell** -> **Run**</span></span>
* <span data-ttu-id="bfcc6-155">creare un nuovo blocco appunti facendo clic sul hello icona Jupyter (angolo superiore sinistro) e quindi fare clic su **New** pulsante hello destro, quindi scegliere il linguaggio di notebook hello (noto anche come kernel).</span><span class="sxs-lookup"><span data-stu-id="bfcc6-155">create a new notebook by clicking on hello Jupyter Icon (left top corner) and then clicking **New** button on hello right and then choosing hello notebook language (also known as kernels).</span></span>   

> [!NOTE]
> <span data-ttu-id="bfcc6-156">Attualmente è supportato Python 2.7, Python 3.5 e R. kernel hello R supporta la programmazione in R Open source nonché a enterprise hello scalabile Microsoft R Server.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-156">Currently we support Python 2.7, Python 3.5 and R. hello R kernel supports programming in both Open source R as well as hello enterprise scalable Microsoft R Server.</span></span>   
> 
> 

<span data-ttu-id="bfcc6-157">Una volta nel blocco note hello è possibile esplorare i dati, compilare il modello di hello, hello modello con le librerie di test.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-157">Once you are in hello notebook you can explore your data, build hello model, test hello model using your choice of libraries.</span></span>

## <a name="3-build-models-using-r-or-python-and-operationalize-them-using-azure-machine-learning"></a><span data-ttu-id="bfcc6-158">3. Compilare modelli usando R o Python e renderli operativi con Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="bfcc6-158">3. Build models using R or Python and Operationalize them using Azure Machine Learning</span></span>
<span data-ttu-id="bfcc6-159">Dopo aver compilato e convalidato il passaggio successivo hello di modello è in genere toodeploy in produzione.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-159">Once you have built and validated your model hello next step is usually toodeploy it into production.</span></span> <span data-ttu-id="bfcc6-160">In questo modo, il client stime modello hello tooinvoke di applicazioni in un tempo reale o in base a una modalità batch.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-160">This allows your client applications tooinvoke hello model predictions on a real time or on a batch mode basis.</span></span> <span data-ttu-id="bfcc6-161">Azure Machine Learning fornisce un meccanismo toooperationalize un modello compilato in R o Python.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-161">Azure Machine Learning provides a mechanism toooperationalize a model built in either R or Python.</span></span>

<span data-ttu-id="bfcc6-162">Quando si rende operativo il modello in Azure Machine Learning, viene esposto un servizio web che consente ai client le chiamate REST toomake che passano nei parametri di input e di ricezione stime dal modello hello come output.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-162">When you operationalize your model in Azure Machine Learning, a web service is exposed that allows clients toomake REST calls that pass in input parameters and receive predictions from hello model as outputs.</span></span>   

> [!NOTE]
> <span data-ttu-id="bfcc6-163">Se non è ancora iscritti per Azure Machine Learning, è possibile ottenere un'area di lavoro gratuita o un'area di lavoro standard visitando hello [Azure Machine Learning Studio](https://studio.azureml.net/) home page e facendo clic su "Introduzione".</span><span class="sxs-lookup"><span data-stu-id="bfcc6-163">If you have not yet signed up for Azure Machine Learning, you can obtain a free workspace or a standard workspace by visiting hello [Azure Machine Learning Studio](https://studio.azureml.net/) home page and clicking on "Get Started".</span></span>   
> 
> 

### <a name="build-and-operationalize-python-models"></a><span data-ttu-id="bfcc6-164">Compilare e rendere operativi i modelli Python</span><span class="sxs-lookup"><span data-stu-id="bfcc6-164">Build and Operationalize Python models</span></span>
<span data-ttu-id="bfcc6-165">Di seguito è riportato un frammento di codice sviluppato in un server Jupyter Notebook di Python che consente di creare un modello semplice utilizzando hello informazioni SciKit libreria.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-165">Here is a snippet of code developed in a Python Jupyter Notebook that builds a simple model using hello SciKit-learn library.</span></span>

    #IRIS classification
    from sklearn import datasets
    from sklearn import svm
    clf = svm.SVC()
    iris = datasets.load_iris()
    X, y = iris.data, iris.target
    clf.fit(X, y)

<span data-ttu-id="bfcc6-166">metodo Hello utilizzato toodeploy il tooAzure modelli python Machine Learning esegue il wrapping hello stima del modello di hello in una funzione e decora con gli attributi forniti dalla libreria python di Azure Machine Learning pre-installata hello che identificano il computer di Azure ID area di lavoro di apprendimento e la chiave API hello di input e restituire i parametri.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-166">hello method used toodeploy your python models tooAzure Machine Learning wraps hello prediction of hello model into a function and decorates it with attributes provided by hello pre-installed Azure Machine Learning python library that denote your Azure Machine Learning workspace ID, API Key, and hello input and return parameters.</span></span>  

    from azureml import services
    @services.publish(workspaceid, auth_token)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(int) #0, or 1, or 2
    def predictIris(sep_l, sep_w, pet_l, pet_w):
     inputArray = [sep_l, sep_w, pet_l, pet_w]
    return clf.predict(inputArray)

<span data-ttu-id="bfcc6-167">Un client possa ora effettuare chiamate toohello web service.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-167">A client can now make calls toohello web service.</span></span> <span data-ttu-id="bfcc6-168">Sono disponibili wrapper praticità per costruire le richieste API REST di hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-168">There are convenience wrappers that construct hello REST API requests.</span></span> <span data-ttu-id="bfcc6-169">Di seguito è un servizio web di hello tooconsume di codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-169">Here is a sample code tooconsume hello web service.</span></span>

    # Consume through web service URL and keys
    from azureml import services
    @services.service(url, api_key)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(float)
    def IrisPredictor(sep_l, sep_w, pet_l, pet_w):
    pass

    IrisPredictor(3,2,3,4)


> [!NOTE]
> <span data-ttu-id="bfcc6-170">libreria di Azure Machine Learning Hello è supportata solo su Python 2.7 attualmente.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-170">hello Azure Machine Learning library is only supported on Python 2.7 currently.</span></span>   
> 
> 

### <a name="build-and-operationalize-r-models"></a><span data-ttu-id="bfcc6-171">Compilare e rendere operativi i modelli R</span><span class="sxs-lookup"><span data-stu-id="bfcc6-171">Build and Operationalize R models</span></span>
<span data-ttu-id="bfcc6-172">È possibile distribuire i modelli di R compilati nel hello macchina virtuale di analisi scientifica dei dati o in un' posizione in Azure Machine Learning in modo simile toohow che completamento per Python.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-172">You can deploy R models built on hello Data Science Virtual Machine or elsewhere onto Azure Machine Learning in a manner that is similar toohow it is done for Python.</span></span> <span data-ttu-id="bfcc6-173">Sua hello passaggi:</span><span class="sxs-lookup"><span data-stu-id="bfcc6-173">Her are hello steps:</span></span>

* <span data-ttu-id="bfcc6-174">creare un tooprovide file Settings l'ID area di lavoro e l'autenticazione del token come illustrato nel seguente esempio di codice hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-174">create a settings.json file tooprovide your workspace ID and auth token as shown in hello following code sample.</span></span>
* <span data-ttu-id="bfcc6-175">scrivere un wrapper per il modello di hello predict-funzione.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-175">write a wrapper for hello model's predict function.</span></span>
* <span data-ttu-id="bfcc6-176">chiamare ```publishWebService``` in Azure Machine Learning libreria toopass wrapper funzione hello hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-176">call ```publishWebService``` in hello Azure Machine Learning library toopass in hello function wrapper.</span></span>  

<span data-ttu-id="bfcc6-177">Di seguito è hello procedure e frammenti di codice che possono essere utilizzato tooset up, compilare, pubblicare e utilizzare un modello come un servizio web in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-177">Here is hello procedure and code snippets that can be used tooset up, build, publish, and consume a model as a web service in Azure Machine Learning.</span></span>

#### <a name="setup"></a><span data-ttu-id="bfcc6-178">Configurazione</span><span class="sxs-lookup"><span data-stu-id="bfcc6-178">Setup</span></span>
1. <span data-ttu-id="bfcc6-179">Installare il pacchetto di Machine Learning R hello digitando ```install.packages("AzureML")``` Revolution R Enterprise 8.0 IDE o l'IDE di R.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-179">Install hello Machine Learning R package by typing ```install.packages("AzureML")``` in Revolution R Enterprise 8.0 IDE or your R IDE.</span></span>
2. <span data-ttu-id="bfcc6-180">Scaricare RTools da [qui](https://cran.r-project.org/bin/windows/Rtools/).</span><span class="sxs-lookup"><span data-stu-id="bfcc6-180">Download RTools from [here](https://cran.r-project.org/bin/windows/Rtools/).</span></span> <span data-ttu-id="bfcc6-181">È necessario hello zip utilità percorso hello (e denominato zip.exe) toooperationalize il pacchetto R in Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-181">You need hello zip utility in hello path (and named zip.exe) toooperationalize your R package into Machine Learning.</span></span>
3. <span data-ttu-id="bfcc6-182">Creare un file Settings in una directory denominata ```.azureml``` nella directory principale e immettere i parametri di hello dall'area di lavoro di Azure Machine Learning:</span><span class="sxs-lookup"><span data-stu-id="bfcc6-182">Create a settings.json file under a directory called ```.azureml``` under your home directory and enter hello parameters from your Azure Machine Learning workspace:</span></span>

<span data-ttu-id="bfcc6-183">Struttura del file settings.json:</span><span class="sxs-lookup"><span data-stu-id="bfcc6-183">settings.json File structure:</span></span>

    {"workspace":{
    "id"                  : "ENTER YOUR AZUREML WORKSPACE ID",
    "authorization_token" : "ENTER YOUR AZUREML AUTH TOKEN"
    }}


#### <a name="build-a-model-in-r-and-publish-it-in-azure-machine-learning"></a><span data-ttu-id="bfcc6-184">Compilare un modello in R e pubblicarlo in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="bfcc6-184">Build a model in R and publish it in Azure Machine Learning</span></span>
    library(AzureML)
    ws <- workspace(config="~/.azureml/settings.json")

    if(!require("lme4")) install.packages("lme4")
    library(lme4)
    set.seed(1)
    train <- sleepstudy[sample(nrow(sleepstudy), 120),]
    m <- lm(Reaction ~ Days + Subject, data = train)

    # Define a prediction function toopublish based on hello model:
    sleepyPredict <- function(newdata){
          predict(m, newdata=newdata)
    }

    ep <- publishWebService(ws, fun = sleepyPredict, name="sleepy lm", inputSchema = sleepstudy, data.frame=TRUE)

#### <a name="consume-hello-model-deployed-in-azure-machine-learning"></a><span data-ttu-id="bfcc6-185">Utilizzare il modello di hello distribuito in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="bfcc6-185">Consume hello model deployed in Azure Machine Learning</span></span>
<span data-ttu-id="bfcc6-186">modello di hello tooconsume da un'applicazione client, utilizziamo hello Azure Machine Learning libreria toolook backup hello servizio web pubblicato per nome utilizzando hello `services` endpoint hello toodetermine chiamata dell'API.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-186">tooconsume hello model from a client application, we use hello Azure Machine Learning library toolook up hello published web service by name using hello `services` API call toodetermine hello endpoint.</span></span> <span data-ttu-id="bfcc6-187">È sufficiente chiamare hello `consume` funzione e passare hello toobe di frame di dati previsto.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-187">Then you just call hello `consume` function and pass in hello data frame toobe predicted.</span></span>
<span data-ttu-id="bfcc6-188">Hello seguente di codice è il modello di hello tooconsume utilizzati pubblicato come servizio web di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-188">hello following code is used tooconsume hello model published as an Azure Machine Learning web service.</span></span>

    library(AzureML)
    library(lme4)
    ws <- workspace(config="~/.azureml/settings.json")

    s <-  services(ws, name = "sleepy lm")
    s <- tail(s, 1) # use hello last published function, in case of duplicate function names

    ep <- endpoints(ws, s)

    # OK, try this out, and compare with raw data
    ans = consume(ep, sleepstudy)$ans

<span data-ttu-id="bfcc6-189">Sono disponibili ulteriori informazioni sulla libreria di Azure Machine Learning R hello [qui](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).</span><span class="sxs-lookup"><span data-stu-id="bfcc6-189">More information about hello Azure Machine Learning R library can be found [here](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).</span></span>

## <a name="4-administer-your-azure-resources-using-azure-portal-or-powershell"></a><span data-ttu-id="bfcc6-190">4. Amministrare le risorse di Azure usando il portale di Azure o PowerShell</span><span class="sxs-lookup"><span data-stu-id="bfcc6-190">4. Administer your Azure resources using Azure portal or Powershell</span></span>
<span data-ttu-id="bfcc6-191">Hello DSVM consente non solo toobuild soluzione analitica localmente sul hello macchina virtuale, ma consente anche tooaccess servizi nel cloud di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-191">hello DSVM not only allows you toobuild your analytics solution locally on hello virtual machine, but also allows you tooaccess services on Microsoft's Azure cloud.</span></span> <span data-ttu-id="bfcc6-192">Azure offre diversi servizi di calcolo, archiviazione e analisi dei dati e altri servizi amministrabili e accessibili da DSVM.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-192">Azure provides several compute, storage, data analytics services and other services that you can administer and access from your DSVM.</span></span>

<span data-ttu-id="bfcc6-193">tooadminister le risorse di sottoscrizione e nel cloud Azure è possibile utilizzare il browser e il punto toothe [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bfcc6-193">tooadminister your Azure subscription and cloud resources you can use your browser and point toothe [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="bfcc6-194">Sottoscrizione di Azure e alle risorse tramite uno script, è possibile utilizzare anche tooadminister Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-194">You can also use Azure Powershell tooadminister your Azure subscription and resources via a script.</span></span>
<span data-ttu-id="bfcc6-195">È possibile eseguire Azure Powershell da un collegamento sul desktop hello o da hello menu intitolato "Microsoft Azure Powershell" di avvio.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-195">You can run Azure Powershell from a shortcut on hello desktop or from hello start menu titled "Microsoft Azure Powershell".</span></span> <span data-ttu-id="bfcc6-196">Per altre informazioni su come amministrare le risorse e la sottoscrizione di Azure con gli script di Windows PowerShell, vedere la [documentazione di Microsoft Azure PowerShell](../powershell-azure-resource-manager.md) .</span><span class="sxs-lookup"><span data-stu-id="bfcc6-196">Refer to [Microsoft Azure Powershell documentation](../powershell-azure-resource-manager.md) for more information on how you can administer your Azure subscription and resources using Windows Powershell scripts.</span></span>

## <a name="5-extend-your-storage-space-with-a-shared-file-system"></a><span data-ttu-id="bfcc6-197">5. Estendere lo spazio di archiviazione con un file system condiviso</span><span class="sxs-lookup"><span data-stu-id="bfcc6-197">5. Extend your storage space with a shared file system</span></span>
<span data-ttu-id="bfcc6-198">Gli esperti di dati possono condividere i set di dati di grandi dimensioni, codice o altre risorse all'interno del team di hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-198">Data scientists can share large datasets, code or other resources within hello team.</span></span> <span data-ttu-id="bfcc6-199">Hello DSVM stesso è di circa 70GB di spazio disponibile.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-199">hello DSVM itself has about 70GB of space available.</span></span> <span data-ttu-id="bfcc6-200">tooextend lo spazio di archiviazione, è possibile utilizzare hello servizio File di Azure e montarlo in hello DSVM o accedervi tramite un'API REST.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-200">tooextend your storage, you can use hello Azure File Service and either mount it on hello DSVM or access it via a REST API.</span></span>   

> [!NOTE]
> <span data-ttu-id="bfcc6-201">lo spazio massimo di Hello della condivisione File servizio hello è 5TB e il limite di dimensioni di singoli file è di 1TB.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-201">hello maximum space of hello Azure File Service share is 5TB and individual file size limit is 1TB.</span></span>   
> 
> 

<span data-ttu-id="bfcc6-202">È possibile usare Azure Powershell toocreate una condivisione di File di servizio.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-202">You can use Azure Powershell toocreate an Azure File Service share.</span></span> <span data-ttu-id="bfcc6-203">Di seguito è toorun script hello in Azure PowerShell toocreate una condivisione di File di Azure del servizio.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-203">Here is hello script toorun under Azure PowerShell toocreate an Azure File service share.</span></span>

    # Authenticate tooAzure.
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
    # Create a directory under hello FIle share. You can give it any name
    New-AzureStorageDirectory -Share $s -Path <directory name>
    # List hello share tooconfirm that everything worked
    Get-AzureStorageFile -Share $s


<span data-ttu-id="bfcc6-204">A questo punto, dopo avere creato una condivisione file di Azure, è possibile installarla in una macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-204">Now that you have created an Azure file share, you can mount it in any virtual machine in Azure.</span></span> <span data-ttu-id="bfcc6-205">È consigliabile che hello VM è nella stessa data center di Azure come latenza tooavoid account di archiviazione hello e dati gli addebiti di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-205">It is highly recommended that hello VM is in same Azure data center as hello storage account tooavoid latency and data transfer charges.</span></span> <span data-ttu-id="bfcc6-206">Di seguito sono unità di hello comandi toomount hello in hello DSVM che è possibile eseguire in Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-206">Here are hello commands toomount hello drive on hello DSVM that you can run on Azure Powershell.</span></span>

    # Get storage key of hello storage account that has hello Azure file share from Azure portal. Store it securely on hello VM tooavoid prompted in next command.
    cmdkey /add:<<mydatadisk>>.file.core.windows.net /user:<<mydatadisk>> /pass:<storage key>

    # Mount hello Azure file share as Z: drive on hello VM. You can chose another drive letter if you wish
    net use z:  \\<mydatadisk>.file.core.windows.net\<<teamsharename>>


<span data-ttu-id="bfcc6-207">È ora possibile accedere questa unità come si farebbe per qualsiasi unità normale su hello VM.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-207">Now you can access this drive as you would any normal drive on hello VM.</span></span>

## <a name="6-share-code-with-your-team-using-github"></a><span data-ttu-id="bfcc6-208">6. Condividere il codice con il team usando GitHub</span><span class="sxs-lookup"><span data-stu-id="bfcc6-208">6. Share code with your team using GitHub</span></span>
<span data-ttu-id="bfcc6-209">GitHub è un repository di codice in cui è possibile trovare una notevole quantità di codice di esempio e origini per diversi strumenti con varie tecnologie condivise da una community di sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-209">GitHub is a code repository where you can find a lot of sample code and sources for different tools using various technologies shared by hello developer community.</span></span> <span data-ttu-id="bfcc6-210">Git viene utilizzato come hello versioni tootrack e l'archivio della tecnologia dei file di codice hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-210">It uses Git as hello technology tootrack and store versions of hello code files.</span></span> <span data-ttu-id="bfcc6-211">GitHub è inoltre una piattaforma in cui è possibile creare la propria toostore repository codice condiviso e la documentazione, il team implementa il controllo delle versioni e controllo che dispongono dell'accesso tooview e fornire codice.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-211">GitHub is also a platform where you can create your own repository toostore your team's shared code and documentation, implement version control and also control who have access tooview and contribute code.</span></span> <span data-ttu-id="bfcc6-212">Visitare hello [pagine della Guida di GitHub](https://help.github.com/) per ulteriori informazioni sull'uso di Git.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-212">Please visit hello [GitHub help pages](https://help.github.com/) for more information on using Git.</span></span> <span data-ttu-id="bfcc6-213">È possibile utilizzare GitHub come uno dei hello modi toocollaborate con il team, usare il codice sviluppato dalla community di hello e collaborazione della community toohello indietro di codice.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-213">You can use GitHub as one of hello ways toocollaborate with your team, use code developed by hello community and contribute code back toohello community.</span></span>

<span data-ttu-id="bfcc6-214">Hello DSVM include già caricato con gli strumenti client sia come ben GUI tooaccess repository GitHub della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-214">hello DSVM already comes loaded with client tools on both command-line as well GUI tooaccess GitHub repository.</span></span> <span data-ttu-id="bfcc6-215">Hello strumento da riga di comando toowork con Git e GitHub viene chiamato Git Bash.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-215">hello command-line tool toowork with Git and GitHub is called Git Bash.</span></span> <span data-ttu-id="bfcc6-216">Visual Studio installata sul hello DSVM dispone di estensioni di Git hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-216">Visual Studio installed on hello DSVM has hello Git extensions.</span></span> <span data-ttu-id="bfcc6-217">È possibile trovare le icone di avvio per questi strumenti nel menu start hello e sul desktop hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-217">You can find start-up icons for these tools on hello start menu and hello desktop.</span></span>

<span data-ttu-id="bfcc6-218">codice toodownload da un repository GitHub utilizzare hello ```git clone``` comando.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-218">toodownload code from a GitHub repository you use hello ```git clone``` command.</span></span> <span data-ttu-id="bfcc6-219">Ad esempio repository di toodownload analisi scientifica dei dati pubblicati da Microsoft nella directory corrente hello è possibile eseguire hello comando seguente, una volta nel ```git-bash```.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-219">For example toodownload data science repository published by Microsoft into hello current directory you can run hello following command once you are in ```git-bash```.</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="bfcc6-220">In Visual Studio, è possibile effettuare hello stessa operazione di clonazione.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-220">In Visual Studio, you can do hello same clone operation.</span></span> <span data-ttu-id="bfcc6-221">Hello cattura di schermata seguente mostra come tooaccess Git e GitHub degli strumenti in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-221">hello  following screen-shot shows how tooaccess Git and GitHub tools in Visual Studio.</span></span>

![Git in Visual Studio](./media/machine-learning-data-science-vm-do-ten-things/VSGit.PNG)

<span data-ttu-id="bfcc6-223">È possibile trovare ulteriori informazioni sull'uso di Git toowork con il repository GitHub da diverse risorse disponibili in github.com. Hello [foglio informativo](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) è un utile riferimento.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-223">You can find more information on using Git toowork with your GitHub repository from several resources available on github.com. hello [cheat sheet](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) is a useful reference.</span></span>

## <a name="7-access-various-azure-data-and-analytics-services"></a><span data-ttu-id="bfcc6-224">7. Accedere a diversi servizi dati e analisi di Azure</span><span class="sxs-lookup"><span data-stu-id="bfcc6-224">7. Access various Azure data and analytics services</span></span>
### <a name="azure-blob"></a><span data-ttu-id="bfcc6-225">BLOB Azure</span><span class="sxs-lookup"><span data-stu-id="bfcc6-225">Azure Blob</span></span>
<span data-ttu-id="bfcc6-226">BLOB di Azure è una risorsa di archiviazione cloud conveniente e affidabile per piccole e grandi quantità di dati.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-226">Azure blob is a reliable, economical cloud storage for data big and small.</span></span> <span data-ttu-id="bfcc6-227">Esaminiamo come è possibile spostare tooAzure dati Blob e accedere ai dati archiviati in un Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-227">Let us look at how you can move data tooAzure Blob and access data stored in an Azure Blob.</span></span>

<span data-ttu-id="bfcc6-228">**Prerequisito**</span><span class="sxs-lookup"><span data-stu-id="bfcc6-228">**Prerequisite**</span></span>

* <span data-ttu-id="bfcc6-229">**Creare l'account di archiviazione BLOB di Azure nel [portale di Azure](https://portal.azure.com).**</span><span class="sxs-lookup"><span data-stu-id="bfcc6-229">**Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).**</span></span>

![Create_Azure_Blob](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="bfcc6-231">Verificare che hello pre-installato da riga di comando strumento AzCopy si trova in corrispondenza ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-231">Confirm that hello pre-installed command-line AzCopy tool is found at ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```.</span></span> <span data-ttu-id="bfcc6-232">È possibile aggiungere hello directory contenitore hello azcopy.exe tooyour ambiente tooavoid variabile digitando hello comando completo percorso quando si esegue questo strumento.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-232">You can add hello directory containing hello azcopy.exe tooyour PATH environment variable tooavoid typing hello full command path when running this tool.</span></span> <span data-ttu-id="bfcc6-233">Per ulteriori informazioni sullo strumento AzCopy, vedere troppo[documentazione AzCopy](../storage/common/storage-use-azcopy.md)</span><span class="sxs-lookup"><span data-stu-id="bfcc6-233">For more info on AzCopy tool please refer too[AzCopy documentation](../storage/common/storage-use-azcopy.md)</span></span>
* <span data-ttu-id="bfcc6-234">Avviare lo strumento di hello Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-234">Start hello Azure Storage Explorer tool.</span></span> <span data-ttu-id="bfcc6-235">È possibile scaricarlo da [Esplora archivi di Microsoft Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="bfcc6-235">It can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span> 

![AzureStorageExplorer_v4](./media/machine-learning-data-science-vm-do-ten-things/AzureStorageExplorer_v4.png)

<span data-ttu-id="bfcc6-237">**Spostare i dati da una macchina virtuale tooAzure Blob: AzCopy**</span><span class="sxs-lookup"><span data-stu-id="bfcc6-237">**Move data from VM tooAzure Blob: AzCopy**</span></span>

<span data-ttu-id="bfcc6-238">toomove dati tra i file locali e l'archiviazione blob, è possibile usare AzCopy nella riga di comando o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bfcc6-238">toomove data between your local files and blob storage, you can use AzCopy in command-line or PowerShell:</span></span>

    AzCopy /Source:C:\myfolder /Dest:https://<mystorageaccount>.blob.core.windows.net/<mycontainer> /DestKey:<storage account key> /Pattern:abc.txt

<span data-ttu-id="bfcc6-239">Sostituire **C:\myfolder** toohello percorso in cui è archiviato il file, **mystorageaccount** nome account di archiviazione blob di tooyour, **mycontainer** il nome del contenitore toohello **chiave account di archiviazione** chiave di accesso di archiviazione blob tooyour.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-239">Replace **C:\myfolder** toohello path where your file is stored, **mystorageaccount** tooyour blob storage account name, **mycontainer** toohello container name, **storage account key** tooyour blob storage access key.</span></span> <span data-ttu-id="bfcc6-240">È possibile trovare le credenziali dell'account di archiviazione nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bfcc6-240">You can find your storage account credentials in [Azure portal](https://portal.azure.com).</span></span>

![StorageAccountCredential_v2](./media/machine-learning-data-science-vm-do-ten-things/StorageAccountCredential_v2.png)

<span data-ttu-id="bfcc6-242">Eseguire il comando AzCopy in PowerShell o al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-242">Run AzCopy command in PowerShell or from a command prompt.</span></span> <span data-ttu-id="bfcc6-243">Ecco un esempio di utilizzo del comando AzCopy:</span><span class="sxs-lookup"><span data-stu-id="bfcc6-243">Here is some example usage of AzCopy command:</span></span>

    # Copy *.sql from local machine tooa Azure Blob
    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:"c:\Aaqs\Data Science Scripts" /Dest:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /DestKey:[ENTER STORAGE KEY] /S /Pattern:*.sql

    # Copy back all files from Azure Blob container tooLocal machine

    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Dest:"c:\Aaqs\Data Science Scripts\temp" /Source:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /SourceKey:[ENTER STORAGE KEY] /S



<span data-ttu-id="bfcc6-244">Dopo aver eseguito la tooan toocopy di AzCopy comando è visualizzato il file del blob di Azure viene visualizzato in Esplora archivi Azure a breve.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-244">Once you run your AzCopy command toocopy tooan Azure blob you see your file shows up in Azure Storage Explorer shortly.</span></span>

![AzCopy_run_finshed_Storage_Explorer_v3](./media/machine-learning-data-science-vm-do-ten-things/AzCopy_run_finshed_Storage_Explorer_v3.png)

<span data-ttu-id="bfcc6-246">**Spostare i dati da una macchina virtuale tooAzure Blob: Azure Storage Explorer**</span><span class="sxs-lookup"><span data-stu-id="bfcc6-246">**Move data from VM tooAzure Blob: Azure Storage Explorer**</span></span>

<span data-ttu-id="bfcc6-247">È inoltre possibile caricare i dati da file locale hello nella macchina virtuale tramite Esplora archivi Azure:</span><span class="sxs-lookup"><span data-stu-id="bfcc6-247">You can also upload data from hello local file in your VM using Azure Storage Explorer:</span></span>

* <span data-ttu-id="bfcc6-248">contenitore di tooa dati tooupload, hello contenitore e fare clic su di destinazione selezionare hello **caricare** pulsante.![ Carica in Esplora archivi](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span><span class="sxs-lookup"><span data-stu-id="bfcc6-248">tooupload data tooa container, select hello target container and click hello **Upload** button.![Upload in Storage Explorer](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span></span>
* <span data-ttu-id="bfcc6-249">Fare clic su hello **...**  toohello diritto di hello **file** , selezionare uno o più tooupload file dal file system di hello e fare clic su **caricare** toobegin caricamento file hello.![ Caricare file tooblob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span><span class="sxs-lookup"><span data-stu-id="bfcc6-249">Click on hello **...** toohello right of hello **Files** box, select one or multiple files tooupload from hello file system and click **Upload** toobegin uploading hello files.![Upload files tooblob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span></span>

<span data-ttu-id="bfcc6-250">**Leggere i dati dal BLOB di Azure: modulo Reader di Machine Learning**</span><span class="sxs-lookup"><span data-stu-id="bfcc6-250">**Read data from Azure Blob: Machine Learning reader module**</span></span>

<span data-ttu-id="bfcc6-251">In Azure Machine Learning Studio è possibile utilizzare un **modulo Importa dati** dati tooread il blob.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-251">In Azure Machine Learning Studio you can use an **Import Data module** tooread data from your blob.</span></span>

![AML_ReaderBlob_Module_v3](./media/machine-learning-data-science-vm-do-ten-things/AML_ReaderBlob_Module_v3.png)

<span data-ttu-id="bfcc6-253">**Leggere i dati dal BLOB di Azure: ODBC Python**</span><span class="sxs-lookup"><span data-stu-id="bfcc6-253">**Read data from Azure Blob: Python ODBC**</span></span>

<span data-ttu-id="bfcc6-254">È possibile utilizzare **BlobService** dati tooread libreria direttamente dal blob in un programma server Jupyter Notebook o Python.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-254">You can use **BlobService** library tooread data directly from blob in a Jupyter Notebook or Python program.</span></span>

<span data-ttu-id="bfcc6-255">Prima di tutto importare i pacchetti necessari:</span><span class="sxs-lookup"><span data-stu-id="bfcc6-255">First, import required packages:</span></span>

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

<span data-ttu-id="bfcc6-256">Quindi collegare le credenziali dell'account BLOB di Azure e leggere i dati dal BLOB:</span><span class="sxs-lookup"><span data-stu-id="bfcc6-256">Then plug in your Azure Blob account credentials and read data from Blob:</span></span>

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
    print(("It takes %s seconds toodownload "+BLOBNAME) % (t2 - t1))

    #unzipping downloaded files if needed
    #with zipfile.ZipFile(ZIPPEDLOCALFILE, "r") as z:
    #    z.extractall(LOCALDIRECTORY)

    df1 = pd.read_csv(LOCALFILE, header=0)
    df1.columns = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime','passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude']
    print 'hello size of hello data is: %d rows and  %d columns' % df1.shape

<span data-ttu-id="bfcc6-257">sono possibile leggerlo dati Hello come frame di dati:</span><span class="sxs-lookup"><span data-stu-id="bfcc6-257">hello data is read in as a data frame:</span></span>

![IPNB_data_readin](./media/machine-learning-data-science-vm-do-ten-things/IPNB_data_readin.PNG)

### <a name="azure-data-lake"></a><span data-ttu-id="bfcc6-259">Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="bfcc6-259">Azure Data Lake</span></span>
<span data-ttu-id="bfcc6-260">Un Archivio Azure Data Lake è un repository con iperscalabilità per i carichi di lavoro di analisi dei Big Data compatibile con Hadoop Distributed File System (HDFS).</span><span class="sxs-lookup"><span data-stu-id="bfcc6-260">Azure Data Lake Storage is a hyper-scale repository for big data analytics workloads and compatible with Hadoop Distributed File System (HDFS).</span></span> <span data-ttu-id="bfcc6-261">Funziona con l'ecosistema di Hadoop hello sia hello Azure Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-261">It works with both hello Hadoop ecosystem and hello Azure Data Lake Analytics.</span></span> <span data-ttu-id="bfcc6-262">Ecco come è possibile spostare i dati in archivio Azure Data Lake hello ed eseguire analitica usando Azure Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-262">We show how you can move data into hello Azure Data Lake Store and run analytics using Azure Data Lake Analytics.</span></span>

<span data-ttu-id="bfcc6-263">**Prerequisito**</span><span class="sxs-lookup"><span data-stu-id="bfcc6-263">**Prerequisite**</span></span>

* <span data-ttu-id="bfcc6-264">Creare Azure Data Lake Analytics nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bfcc6-264">Create your Azure Data Lake Analytics in [Azure portal](https://portal.azure.com).</span></span>

![Azure_Data_Lake_Create_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_Create_v2.png)

* <span data-ttu-id="bfcc6-266">Hello **Azure Data Lake Tools** in **Visual Studio** trovare questo [collegamento](https://www.microsoft.com/download/details.aspx?id=49504) è già installato in Visual Studio Community Edition che si trova su una macchina virtuale hello hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-266">hello  **Azure Data Lake Tools** in **Visual Studio** found at this  [link](https://www.microsoft.com/download/details.aspx?id=49504) is already installed on hello Visual Studio Community Edition which is on hello virtual machine.</span></span> <span data-ttu-id="bfcc6-267">Dopo aver avviato Visual Studio e registrazione nella sottoscrizione di Azure, si dovrebbe essere l'account di Azure dati Analitica e l'archiviazione nel riquadro sinistro di hello di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-267">After starting Visual Studio and logging in your Azure subscription, you should see your Azure Data Analytics account and storage in hello left panel of Visual Studio.</span></span>

![Azure_Data_Lake_PlugIn_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_PlugIn_v2.PNG)

<span data-ttu-id="bfcc6-269">**Spostare i dati da una macchina virtuale tooData Lake: esplorazione di Azure Data Lake**</span><span class="sxs-lookup"><span data-stu-id="bfcc6-269">**Move data from VM tooData Lake: Azure Data Lake Explorer**</span></span>

<span data-ttu-id="bfcc6-270">È possibile utilizzare **Azure Data Lake Explorer** dati tooupload da file locali di hello nell'archiviazione Lake tooData macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-270">You can use **Azure Data Lake Explorer** tooupload data from hello local files in your Virtual Machine tooData Lake storage.</span></span>

![Azure_Data_Lake_UploadData](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_UploadData.PNG)

<span data-ttu-id="bfcc6-272">È anche possibile compilare un tooproductionize pipeline di dati del tooor lo spostamento dei dati da Azure Data Lake tramite hello [Azure dati Factory(ADF)](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="bfcc6-272">You can also build a data pipeline tooproductionize your data movement tooor from Azure Data Lake using hello [Azure Data Factory(ADF)](https://azure.microsoft.com/services/data-factory/).</span></span> <span data-ttu-id="bfcc6-273">Vedere toothis [articolo](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) tooguide è tra i dati di hello passaggi toobuild hello pipeline.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-273">We refer you toothis [article](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) tooguide you through hello steps toobuild hello data pipelines.</span></span>

<span data-ttu-id="bfcc6-274">**Leggere i dati da Azure Blob tooData Lake: U-SQL**</span><span class="sxs-lookup"><span data-stu-id="bfcc6-274">**Read data from Azure Blob tooData Lake: U-SQL**</span></span>

<span data-ttu-id="bfcc6-275">Se i dati si trovano nell'archivio BLOB di Azure, è possibile leggerli direttamente dal BLOB di archiviazione di Azure nella query U-SQL.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-275">If your data resides in Azure Blob storage, you can directly read data from Azure storage blob in U-SQL query.</span></span> <span data-ttu-id="bfcc6-276">Prima di composizione di query U-SQL, assicurarsi che l'account di archiviazione blob è tooyour collegato Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-276">Before composing your U-SQL query, make sure your blob storage account is linked tooyour Azure Data Lake.</span></span> <span data-ttu-id="bfcc6-277">Andare troppo**portale di Azure**, trovare il dashboard di Azure Data Lake Analitica, fare clic su **Aggiungi origine dati**, selezionare il tipo di archiviazione troppo**di archiviazione di Azure** e plug-in di archiviazione di Azure Nome dell'account e la chiave.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-277">Go too**Azure portal**, find your Azure Data Lake Analytics dashboard, click **Add Data Source**, select storage type too**Azure Storage** and plug in your Azure Storage Account Name and Key.</span></span> <span data-ttu-id="bfcc6-278">Si è tooreference in grado di dati di hello archiviati nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-278">Then you are able tooreference hello data stored in hello storage account.</span></span>

![Immettere l'account di archiviazione e la chiave](./media/machine-learning-data-science-vm-do-ten-things/Link_Blob_to_ADLA_v2.PNG)

<span data-ttu-id="bfcc6-280">In Visual Studio, è possibile leggere i dati dall'archiviazione blob, eseguire alcune manipolazione dei dati, progettazione di funzionalità e output hello risultante data tooeither Azure Data Lake o archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-280">In Visual Studio, you can read data from blob storage, do some data manipulation, feature engineering, and output hello resulting data tooeither Azure Data Lake or Azure Blob Storage.</span></span> <span data-ttu-id="bfcc6-281">Quando si fa riferimento a dati hello nell'archiviazione blob, utilizzare **wasb: / /**; quando si fa riferimento a dati hello in Azure Data Lake, utilizzare **swbhdfs: / /**</span><span class="sxs-lookup"><span data-stu-id="bfcc6-281">When you reference hello data in blob storage, use **wasb://**; when you reference hello data in Azure Data Lake, use **swbhdfs://**</span></span>

![Frame di dati](./media/machine-learning-data-science-vm-do-ten-things/USQL_Read_Blob_v2.PNG)

<span data-ttu-id="bfcc6-283">È possibile utilizzare hello seguente query U-SQL in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="bfcc6-283">You may use hello following U-SQL queries in Visual Studio:</span></span>

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
    too"swebhdfs://<Azure Data Lake Storage Account Name>.azuredatalakestore.net/<Folder Name>/<Output Data File Name>"
    USING Outputters.Csv();

    OUTPUT @b   
    too"wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Output Data File Name>"
    USING Outputters.Csv();



<span data-ttu-id="bfcc6-284">Dopo che la query è inviata toohello server, viene visualizzato un diagramma che illustra lo stato di hello del processo.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-284">After your query is submitted toohello server, a diagram showing hello status of your job is displayed.</span></span>

![Diagramma dello stato del processo](./media/machine-learning-data-science-vm-do-ten-things/USQL_Job_Status.PNG)

<span data-ttu-id="bfcc6-286">**Effettuare una query dei dati in Data Lake: U-SQL**</span><span class="sxs-lookup"><span data-stu-id="bfcc6-286">**Query data in Data Lake: U-SQL**</span></span>

<span data-ttu-id="bfcc6-287">Set di dati hello vengono acquisiti in Azure Data Lake, è possibile utilizzare [U-SQL language](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery ed esplorare i dati di hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-287">After hello dataset is ingested into Azure Data Lake, you can use [U-SQL language](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery and explore hello data.</span></span> <span data-ttu-id="bfcc6-288">Linguaggio U-SQL è simile tooT-SQL, ma combina alcune funzionalità di c# in modo che gli utenti possono scrivere moduli personalizzati e funzioni definite dall'utente e così via. È possibile utilizzare script hello nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-288">U-SQL language is similar tooT-SQL, but combines some features from C# so that users can write customized modules, user-defined functions, and etc. You can use hello scripts in hello previous step.</span></span>

<span data-ttu-id="bfcc6-289">Dopo aver inviato tooserver, tripdata_summary query hello. CSV sono reperibili poco **Azure Data Lake Explorer**, è possibile visualizzare l'anteprima dati hello dal file hello pulsante destro del mouse.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-289">After hello query is submitted tooserver, tripdata_summary.CSV can be found shortly in **Azure Data Lake Explorer**, you may preview hello data by right-click hello file.</span></span>

![File in Azure Data Lake Explorer](./media/machine-learning-data-science-vm-do-ten-things/USQL_create_summary.png)

<span data-ttu-id="bfcc6-291">informazioni sui file di hello toosee:</span><span class="sxs-lookup"><span data-stu-id="bfcc6-291">toosee hello file information:</span></span>

![Riepilogo del file](./media/machine-learning-data-science-vm-do-ten-things/USQL_tripdata_summary.png)

### <a name="hdinsight-hadoop-clusters"></a><span data-ttu-id="bfcc6-293">Cluster Hadoop di HDInsight</span><span class="sxs-lookup"><span data-stu-id="bfcc6-293">HDInsight Hadoop Clusters</span></span>
<span data-ttu-id="bfcc6-294">Azure HDInsight è un servizio gestito di Apache Hadoop, Spark, HBase e Storm nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-294">Azure HDInsight is a managed Apache Hadoop, Spark, HBase, and Storm service on hello cloud.</span></span> <span data-ttu-id="bfcc6-295">È possibile utilizzare facilmente con i cluster HDInsight di Azure dalla macchina virtuale di analisi scientifica dei dati hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-295">You can work easily with Azure HDInsight clusters from hello data science virtual machine.</span></span>

<span data-ttu-id="bfcc6-296">**Prerequisito**</span><span class="sxs-lookup"><span data-stu-id="bfcc6-296">**Prerequisite**</span></span>

* <span data-ttu-id="bfcc6-297">Creare l'account di archiviazione BLOB di Azure nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bfcc6-297">Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="bfcc6-298">Questo account di archiviazione è dati toostore utilizzato per i cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-298">This storage account is used toostore data for HDInsight clusters.</span></span>

![Creare un account di archiviazione BLOB di Azure](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="bfcc6-300">Personalizzare i cluster Hadoop di Azure HDInsight nel [portale di Azure](machine-learning-data-science-customize-hadoop-cluster.md)</span><span class="sxs-lookup"><span data-stu-id="bfcc6-300">Customize Azure HDInsight Hadoop Clusters from [Azure portal](machine-learning-data-science-customize-hadoop-cluster.md)</span></span>
  
  * <span data-ttu-id="bfcc6-301">È necessario collegare l'account di archiviazione hello creato con il cluster HDInsight quando viene creato.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-301">You must link hello storage account created with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="bfcc6-302">Questo account di archiviazione viene utilizzato per accedere ai dati che possono essere elaborati all'interno di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-302">This storage account is used for accessing data that can be processed within hello cluster.</span></span>

![Collegamento toostorage account creato con il cluster HDInsight](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_v4.PNG)

* <span data-ttu-id="bfcc6-304">È necessario abilitare **accesso remoto** toohello nodo head del cluster di hello dopo averlo creato.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-304">You must enable **Remote Access** toohello head node of hello cluster after it is created.</span></span> <span data-ttu-id="bfcc6-305">Memorizza le credenziali di accesso remoto hello è possibile specificare (diverse da quelle specificate per il cluster hello al momento della relativa creazione): non è presente la procedura successiva hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-305">Remember hello remote access credentials you specify here (different from those specified for hello cluster at its creation): you need them in hello subsequent procedure.</span></span>

![Abilitare l'accesso remoto](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_dashboard_v3.PNG)

* <span data-ttu-id="bfcc6-307">Creare un'area di lavoro di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-307">Create an Azure Machine Learning workspace.</span></span> <span data-ttu-id="bfcc6-308">Gli esperimenti di Machine Learning vengono archiviati in questa area di lavoro di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-308">Your Machine Learning Experiments are stored in this Machine Learning workspace.</span></span> <span data-ttu-id="bfcc6-309">Selezionare opzioni di hello evidenziato nel portale, come illustrato nella seguente schermata hello:</span><span class="sxs-lookup"><span data-stu-id="bfcc6-309">Select hello highlighted options in Portal as shown in hello following screenshot:</span></span>

![Creare un'area di lavoro di Machine Learning di Azure](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space.PNG)

* <span data-ttu-id="bfcc6-311">Quindi immettere i parametri di hello per l'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="bfcc6-311">Then enter hello parameters for your workspace</span></span>

![Immettere i parametri dell'area di lavoro di Machine Learning](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space_step2_v2.PNG)

* <span data-ttu-id="bfcc6-313">Caricare i dati con IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-313">Upload data using IPython Notebook.</span></span> <span data-ttu-id="bfcc6-314">È innanzitutto necessario importare pacchetti richiesti, inserire le credenziali, creare un database nell'account di archiviazione, quindi caricare cluster tooHDI di dati.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-314">First import required packages, plug in credentials, create a db in your storage account, then load data tooHDI clusters.</span></span>

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


        #Create hello connection tooHive using ODBC
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


        #Upload data from blob storage tooHDI cluster
        for i in range(1,13):
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxitripraw2/trip_data_%d.csv' INTO TABLE nyctaxidb2.trip PARTITION (month=%d);"%(i,i)
            cursor.execute(queryString)
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxifareraw2/trip_fare_%d.csv' INTO TABLE nyctaxidb2.fare PARTITION (month=%d);"%(i,i)  
            cursor.execute(queryString)


* <span data-ttu-id="bfcc6-315">In alternativa, è possibile seguire questo [procedura dettagliata](machine-learning-data-science-process-hive-walkthrough.md) tooupload cluster tooHDI di NYC Taxi dati.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-315">Alternately,  you can follow this [walkthrough](machine-learning-data-science-process-hive-walkthrough.md) tooupload NYC Taxi data tooHDI cluster.</span></span> <span data-ttu-id="bfcc6-316">I passaggi più importanti includono:</span><span class="sxs-lookup"><span data-stu-id="bfcc6-316">Major steps include:</span></span>
  
  * <span data-ttu-id="bfcc6-317">AzCopy: download compresso CSV dalla cartella locale di blob pubblici tooyour</span><span class="sxs-lookup"><span data-stu-id="bfcc6-317">AzCopy: download zipped CSV's from public blob tooyour local folder</span></span>
  * <span data-ttu-id="bfcc6-318">AzCopy: caricare decompresso CSV dal cluster tooHDI cartella locale</span><span class="sxs-lookup"><span data-stu-id="bfcc6-318">AzCopy: upload unzipped CSV's from local folder tooHDI cluster</span></span>
  * <span data-ttu-id="bfcc6-319">Accedere al nodo head di hello del cluster Hadoop e la preparazione per l'analisi esplorativa dei dati</span><span class="sxs-lookup"><span data-stu-id="bfcc6-319">Log into hello head node of Hadoop cluster and prepare for exploratory data analysis</span></span>

<span data-ttu-id="bfcc6-320">Dopo aver caricato tooHDI cluster dati hello, è possibile controllare i dati in Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-320">After hello data is loaded tooHDI cluster, you can check your data in Azure Storage Explorer.</span></span> <span data-ttu-id="bfcc6-321">Nel cluster HDI è stato creato un database nyctaxidb.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-321">And you have a database nyctaxidb created in HDI cluster.</span></span>

<span data-ttu-id="bfcc6-322">**Esplorazione dei dati: query Hive in Python**</span><span class="sxs-lookup"><span data-stu-id="bfcc6-322">**Data exploration: Hive Queries in Python**</span></span>

<span data-ttu-id="bfcc6-323">Poiché i dati di hello sono in cluster Hadoop, è possibile utilizzare hello pyodbc pacchetto tooconnect tooHadoop cluster e database di query utilizzando Progettazione di funzionalità e l'esplorazione toodo Hive.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-323">Since hello data is in Hadoop cluster, you can use hello pyodbc package tooconnect tooHadoop Clusters and query database using Hive toodo exploration and feature engineering.</span></span> <span data-ttu-id="bfcc6-324">È possibile visualizzare le tabelle esistenti di hello che è creati nel passaggio dei prerequisiti di hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-324">You can view hello existing tables we created in hello prerequisite step.</span></span>

    queryString = """
        show tables in nyctaxidb2;
        """
    pd.read_sql(queryString,connection)


![Visualizzare tabelle esistenti](./media/machine-learning-data-science-vm-do-ten-things/Python_View_Existing_Tables_Hive_v3.PNG)

<span data-ttu-id="bfcc6-326">Esaminiamo il numero di hello di record in ogni mese e hello le frequenze di inclinato o non presente nella tabella di andata e ritorno hello:</span><span class="sxs-lookup"><span data-stu-id="bfcc6-326">Let's look at hello number of records in each month and hello frequencies of tipped or not in hello trip table:</span></span>

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

<span data-ttu-id="bfcc6-329">È possibile anche calcolare distanza hello tra il percorso di prelievo e dropoff e confrontare quindi toohello attivarsi distanza.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-329">We can also compute hello distance between pickup location and dropoff location and then compare it toohello trip distance.</span></span>

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


![Tracciato di distanza tootrip prelievo/dropoff distanza](./media/machine-learning-data-science-vm-do-ten-things/Exploration_direct_distance_trip_distance_v2.PNG)

<span data-ttu-id="bfcc6-332">Verrà ora preparato un set di dati sottocampionati (1%) per la modellazione.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-332">Now let's prepare a down-sampled (1%) set of data for modeling.</span></span> <span data-ttu-id="bfcc6-333">È possibile usare questi dati nel modulo Reader di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-333">We can use this data in Machine Learning reader module.</span></span>

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

        --- now insert contents of hello join into hello preceding internal table

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

<span data-ttu-id="bfcc6-334">Dopo un periodo di tempo, è possibile visualizzare dati hello sono stati caricati nel cluster Hadoop:</span><span class="sxs-lookup"><span data-stu-id="bfcc6-334">After a while, you can see hello data has been loaded in Hadoop clusters:</span></span>

    queryString = """
        select * from nyctaxi_downsampled_dataset limit 10;
        """
    cursor.execute(queryString)
    pd.read_sql(queryString,connection)


![Tabella di dati](./media/machine-learning-data-science-vm-do-ten-things/DownSample_Data_For_Modeling_v2.PNG)

<span data-ttu-id="bfcc6-336">**Leggere i dati da HDI con il modulo Reader di Machine Learning**</span><span class="sxs-lookup"><span data-stu-id="bfcc6-336">**Read data from HDI using Machine Learning: reader module**</span></span>

<span data-ttu-id="bfcc6-337">È inoltre possibile utilizzare hello **lettore** modulo di Machine Learning Studio tooaccess hello database in un cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-337">You may also use hello **reader** module in Machine Learning Studio tooaccess hello database in Hadoop cluster.</span></span> <span data-ttu-id="bfcc6-338">Collegare le credenziali di hello dei cluster HDI e Account di archiviazione Azure tooenable compilazione sta eseguendo un'operazione di machine learning i modelli di utilizzo di database in cluster HDI.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-338">Plug in hello credentials of your HDI clusters and Azure Storage Account tooenable build ing machine learning models using database in HDI clusters.</span></span>

![Proprietà del modulo Reader](./media/machine-learning-data-science-vm-do-ten-things/AML_Reader_Hive.PNG)

<span data-ttu-id="bfcc6-340">Hello set di dati con punteggio possono quindi essere visualizzati:</span><span class="sxs-lookup"><span data-stu-id="bfcc6-340">hello scored dataset can then be viewed:</span></span>

![Visualizzare il set di dati con i punteggi](./media/machine-learning-data-science-vm-do-ten-things/AML_Model_Results.PNG)

### <a name="azure-sql-data-warehouse--databases"></a><span data-ttu-id="bfcc6-342">Azure SQL Data Warehouse e database</span><span class="sxs-lookup"><span data-stu-id="bfcc6-342">Azure SQL Data Warehouse & databases</span></span>
<span data-ttu-id="bfcc6-343">Azure SQL Data Warehouse è un data warehouse elastico distribuito come servizio con l'esperienza di classe enterprise di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-343">Azure SQL Data Warehouse is an elastic data warehouse as a service with enterprise-class SQL Server experience.</span></span>

<span data-ttu-id="bfcc6-344">È possibile eseguire il provisioning di Azure SQL Data Warehouse seguendo le istruzioni di hello fornite in questo [articolo](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="bfcc6-344">You can provision your Azure SQL Data Warehouse by following hello instructions provided in this [article](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md).</span></span> <span data-ttu-id="bfcc6-345">Una volta che viene effettuato il provisioning di Azure SQL Data Warehouse, è possibile utilizzare questo [procedura dettagliata](machine-learning-data-science-process-sqldw-walkthrough.md) di caricamento dei dati toodo, esplorazione e modellazione utilizzando i dati all'interno di hello SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-345">Once you provision your Azure SQL Data Warehouse, you can use this [walkthrough](machine-learning-data-science-process-sqldw-walkthrough.md) toodo data upload, exploration and modeling using data within hello SQL Data Warehouse.</span></span>

#### <a name="azure-cosmos-db"></a><span data-ttu-id="bfcc6-346">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bfcc6-346">Azure Cosmos DB</span></span>
<span data-ttu-id="bfcc6-347">DB Cosmos Azure è un database NoSQL nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-347">Azure Cosmos DB is a NoSQL database in hello cloud.</span></span> <span data-ttu-id="bfcc6-348">Consente si toowork con i documenti come JSON e consente toostore ed eseguire query sui documenti hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-348">It allows you toowork with documents like JSON and allows you toostore and query hello documents.</span></span>

<span data-ttu-id="bfcc6-349">È necessario hello toodo seguenti per ogni ora passaggi tooaccess Azure Cosmos DB dagli hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-349">You need toodo hello following per-requisites steps tooaccess Azure Cosmos DB from hello DSVM.</span></span>

1. <span data-ttu-id="bfcc6-350">Installare l'SDK DocumentDB Python eseguendo ```pip install pydocumentdb``` al prompt dei comandi</span><span class="sxs-lookup"><span data-stu-id="bfcc6-350">Install DocumentDB Python SDK (Run ```pip install pydocumentdb``` from command prompt)</span></span>
2. <span data-ttu-id="bfcc6-351">Creare l'account e il database Azure Cosmos DB nel [portale di Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="bfcc6-351">Create an Azure Cosmos DB account and a database from [Azure portal](https://portal.azure.com)</span></span>
3. <span data-ttu-id="bfcc6-352">Scaricare "Strumento di migrazione DB Cosmos di Azure" da [qui](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) ed estrarre tooa directory scelta</span><span class="sxs-lookup"><span data-stu-id="bfcc6-352">Download "Azure Cosmos DB Migration Tool" from [here](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) and extract tooa directory of your choice</span></span>
4. <span data-ttu-id="bfcc6-353">Importare i dati JSON (dati volcano) archiviati in un [blob pubblici](https://cahandson.blob.core.windows.net/samples/volcano.json) in DB Cosmos con seguente comando parametri toohello strumento di migrazione (dtui.exe dalla directory hello in cui è installato lo strumento di migrazione DB Cosmos hello).</span><span class="sxs-lookup"><span data-stu-id="bfcc6-353">Import JSON data (volcano data) stored on a [public blob](https://cahandson.blob.core.windows.net/samples/volcano.json) into Cosmos DB with following command parameters toohello migration tool (dtui.exe from hello directory where you installed hello Cosmos DB Migration Tool).</span></span> <span data-ttu-id="bfcc6-354">Immettere percorso di origine e destinazione hello con i seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="bfcc6-354">Enter hello source and target location with these parameters:</span></span>
   
    <span data-ttu-id="bfcc6-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span><span class="sxs-lookup"><span data-stu-id="bfcc6-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span></span>

<span data-ttu-id="bfcc6-356">Quando si importano dati hello, è possibile passare tooJupyter e blocco note aprire hello intitolata *DocumentDBSample* che contiene python codice tooaccess DocumentDB ed eseguire alcune query di base.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-356">Once you import hello data, you can go tooJupyter and open hello notebook titled *DocumentDBSample* which contains python code tooaccess DocumentDB and do some basic querying.</span></span> <span data-ttu-id="bfcc6-357">Maggiori informazioni su DB Cosmos visitando servizio hello [pagina della documentazione](https://docs.microsoft.com/azure/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="bfcc6-357">You can learn more about Cosmos DB by visiting hello service [documentation page](https://docs.microsoft.com/azure/cosmos-db/).</span></span>

## <a name="8-build-reports-and-dashboard-using-hello-power-bi-desktop"></a><span data-ttu-id="bfcc6-358">8. Creare report e dashboard tramite Power BI Desktop hello</span><span class="sxs-lookup"><span data-stu-id="bfcc6-358">8. Build reports and dashboard using hello Power BI Desktop</span></span>
<span data-ttu-id="bfcc6-359">Segnalare il problema, visualizzare i file JSON Volcano hello che è stato illustrato nell'esempio sopra riportato DB Cosmos in Power BI toogain visual approfondite dati hello hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-359">Let us visualize hello Volcano JSON file that we saw in hello preceding Cosmos DB example in Power BI toogain visual insights into hello data.</span></span> <span data-ttu-id="bfcc6-360">I passaggi dettagliati sono disponibili in hello [articolo Power BI](../cosmos-db/powerbi-visualize.md).</span><span class="sxs-lookup"><span data-stu-id="bfcc6-360">Detailed steps are available in hello [Power BI article](../cosmos-db/powerbi-visualize.md).</span></span> <span data-ttu-id="bfcc6-361">Ecco i passaggi di alto livello hello:</span><span class="sxs-lookup"><span data-stu-id="bfcc6-361">Here are hello high-level steps:</span></span>

1. <span data-ttu-id="bfcc6-362">Aprire Power BI Desktop ed eseguire "Recupera dati".</span><span class="sxs-lookup"><span data-stu-id="bfcc6-362">Open Power BI Desktop and do "Get Data".</span></span> <span data-ttu-id="bfcc6-363">Specificare l'URL come hello: https://cahandson.blob.core.windows.net/samples/volcano.json</span><span class="sxs-lookup"><span data-stu-id="bfcc6-363">Specify hello URL as: https://cahandson.blob.core.windows.net/samples/volcano.json</span></span>
2. <span data-ttu-id="bfcc6-364">Dovrebbe essere importato come un elenco di record di hello JSON</span><span class="sxs-lookup"><span data-stu-id="bfcc6-364">You should see hello JSON records imported as a list</span></span>
3. <span data-ttu-id="bfcc6-365">Convertire tabella tooa di hello elenco in modo che Power BI può lavorare con hello stesso</span><span class="sxs-lookup"><span data-stu-id="bfcc6-365">Convert hello list tooa table so Power BI can work with hello same</span></span>
4. <span data-ttu-id="bfcc6-366">Espandere le colonne di hello facendo clic su hello espandono l'icona (Buongiorno uno con l'icona di "freccia sinistra e una freccia a destra" hello in hello destra della colonna hello)</span><span class="sxs-lookup"><span data-stu-id="bfcc6-366">Expand hello columns by clicking on hello expand icon (hello one with hello "left arrow and a right arrow" icon on hello right of hello column)</span></span>
5. <span data-ttu-id="bfcc6-367">La posizione è un campo "Record".</span><span class="sxs-lookup"><span data-stu-id="bfcc6-367">Notice that location is a "Record" field.</span></span> <span data-ttu-id="bfcc6-368">Espandere i record di hello e selezionare solo le coordinate di hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-368">Expand hello record and select only hello coordinates.</span></span> <span data-ttu-id="bfcc6-369">La coordinata è una colonna elenco.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-369">Coordinate is a list column</span></span>
6. <span data-ttu-id="bfcc6-370">Aggiungere una nuova colonna tooconvert hello elenco coordinate colonna in una colonna di LatLong separata da virgole concatenazione elementi hello due nel campo elenco coordinate hello utilizzando la formula hello ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-370">Add a new column tooconvert hello list coordinate column into a comma separate LatLong column concatenating hello two elements in hello coordinate list field using hello formula ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.</span></span>
7. <span data-ttu-id="bfcc6-371">Convertire infine hello ```Elevation``` tooDecimal di colonna e seleziona hello **Chiudi** e **applica**.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-371">Finally convert hello ```Elevation``` column tooDecimal and select hello **Close** and **Apply**.</span></span>

<span data-ttu-id="bfcc6-372">Anziché passaggi precedenti, è possibile incollare hello seguente di codice che consente di generare script hello passaggi utilizzati in hello Editor avanzato in Power BI che consente le trasformazioni dei dati hello toowrite in un linguaggio di query.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-372">Instead of preceding steps, you can paste hello following code that scripts out hello steps used in hello Advanced Editor in Power BI that allows you toowrite hello data transformations in a query language.</span></span>

    let
        Source = Json.Document(Web.Contents("https://cahandson.blob.core.windows.net/samples/volcano.json")),
        #"Converted tooTable" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
        #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted tooTable", "Column1", {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}, {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}),
        #"Expanded Location" = Table.ExpandRecordColumn(#"Expanded Column1", "Location", {"coordinates"}, {"coordinates"}),
        #"Added Custom" = Table.AddColumn(#"Expanded Location", "LatLong", each Text.From([coordinates]{1})&","&Text.From([coordinates]{0})),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Elevation", type number}})
    in
        #"Changed Type"



<span data-ttu-id="bfcc6-373">Dati hello è ora disponibile nel modello di dati di Power BI.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-373">You now have hello data in your Power BI data model.</span></span> <span data-ttu-id="bfcc6-374">Power BI Desktop deve avere ora un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="bfcc6-374">Your Power BI desktop should appear as follows:</span></span>

![Power BI Desktop](./media/machine-learning-data-science-vm-do-ten-things/PowerBIVolcanoData.png)

<span data-ttu-id="bfcc6-376">È possibile avviare la creazione di report e visualizzazioni con modello di dati hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-376">You can start building reports and visualizations using hello data model.</span></span> <span data-ttu-id="bfcc6-377">È possibile seguire i passaggi di hello in questo [articolo Power BI](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild un report.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-377">You can follow hello steps in this [Power BI article](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild a report.</span></span> <span data-ttu-id="bfcc6-378">risultato finale Hello è un report simile al seguente hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-378">hello end result is a report that looks like hello following.</span></span>

![Visualizzazione report di Power BI Desktop - Connettore Power BI](./media/machine-learning-data-science-vm-do-ten-things/power_bi_connector_pbireportview2.png)

## <a name="9-dynamically-scale-your-dsvm-toomeet-your-project-needs"></a><span data-ttu-id="bfcc6-380">9. Applicare la scalabilità dinamicamente il toomeet DSVM che richiesto dal progetto</span><span class="sxs-lookup"><span data-stu-id="bfcc6-380">9. Dynamically scale your DSVM toomeet your project needs</span></span>
<span data-ttu-id="bfcc6-381">È possibile scalarle toomeet DSVM hello che richiesto dal progetto.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-381">You can scale up and down hello DSVM toomeet your project needs.</span></span> <span data-ttu-id="bfcc6-382">Se non è necessario toouse hello VM sera hello o nei fine settimana, è possibile semplicemente arrestare hello VM da hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bfcc6-382">If you don't need toouse hello VM in hello evening or weekends, you can just shut down hello VM from hello [Azure portal](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="bfcc6-383">Essere addebitati anche se si utilizza solo pulsante di arresto del sistema operativo hello in hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-383">You incur compute charges if you use just hello Operating system shutdown button on hello VM.</span></span>  
> 
> 

<span data-ttu-id="bfcc6-384">Se è necessario toohandle analisi su larga scala e necessario aumentare la capacità della CPU, memoria o disco sono disponibili diverse dimensioni delle macchine Virtuali in termini di core CPU, memoria e tipi di disco (incluse le unità SSD) che soddisfano le esigenze bilancio e il calcolo.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-384">If you need toohandle some large-scale analysis and need more CPU and/or memory and/or disk capacity you can find a large choice of VM sizes in terms of CPU cores, memory capacity and disk types (including Solid state drives) that meet your compute and budgetary needs.</span></span> <span data-ttu-id="bfcc6-385">Hello elenco completo delle macchine virtuali con il piano tariffario calcolo oraria è disponibile in hello [prezzi delle macchine virtuali di Azure](https://azure.microsoft.com/pricing/details/virtual-machines/) pagina.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-385">hello full list of VMs along with their hourly compute pricing is available on hello [Azure Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/) page.</span></span>

<span data-ttu-id="bfcc6-386">Analogamente, se si riduce la necessità di capacità di elaborazione di macchina virtuale (ad esempio: è stato spostato tooa un carico di lavoro principali Hadoop o in un cluster Spark), è possibile scalare verso il basso cluster hello da hello [portale di Azure](https://portal.azure.com) e in uscita toohello impostazioni della macchina virtuale istanza.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-386">Similarly, if your need for VM processing capacity reduces (for example: you moved a major workload tooa Hadoop or a Spark cluster), you can scale down hello cluster from hello [Azure portal](https://portal.azure.com) and going toohello settings of your VM instance.</span></span> <span data-ttu-id="bfcc6-387">Ecco uno screenshot.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-387">Here is a screenshot.</span></span>

![Impostazioni dell'istanza della VM](./media/machine-learning-data-science-vm-do-ten-things/VMScaling.PNG)

## <a name="10-install-additional-tools-on-your-virtual-machine"></a><span data-ttu-id="bfcc6-389">10. Installare strumenti aggiuntivi nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="bfcc6-389">10. Install additional tools on your virtual machine</span></span>
<span data-ttu-id="bfcc6-390">È stato incluso nel pacchetto di diversi strumenti che si ritiene che sono in grado di tooaddress numerose esigenze di analitica dei dati comuni hello e che deve risparmiare tempo evitando con tooinstall e configurare gli ambienti uno alla volta e risparmiare denaro pagando solo per le risorse utilizzare.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-390">We have packaged several tools that we believe are able tooaddress many of hello common data analytics needs and that should save you time by avoiding having tooinstall and configure your environments one by one and save you money by paying only for resources that you use.</span></span>

<span data-ttu-id="bfcc6-391">È possibile usare altri dati di Azure e servizi analitica profilato in questo articolo di tooenhance ambiente analitica.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-391">You can leverage other Azure data and analytics services profiled in this article tooenhance your analytics environment.</span></span> <span data-ttu-id="bfcc6-392">È possibile che in alcuni casi siano necessari strumenti aggiuntivi, inclusi alcuni strumenti proprietari di terze parti.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-392">We understand that in some cases your needs may require additional tools, including some proprietary third-party tools.</span></span> <span data-ttu-id="bfcc6-393">Disporre dell'accesso amministrativo completo in hello macchina virtuale tooinstall nuovi strumenti che necessari.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-393">You have full administrative access on hello virtual machine tooinstall new tools you need.</span></span> <span data-ttu-id="bfcc6-394">È anche possibile installare pacchetti aggiuntivi in Python e in R non preinstallati.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-394">You can also install additional packages in Python and R that are not pre-installed.</span></span> <span data-ttu-id="bfcc6-395">Per Python è possibile usare ```conda``` o ```pip```.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-395">For Python you can use either ```conda``` or ```pip```.</span></span> <span data-ttu-id="bfcc6-396">R è possibile utilizzare hello ```install.packages()``` in hello R console oppure utilizzare hello IDE e scegliere "**pacchetti** -> **pacchetti di installazione...** ".</span><span class="sxs-lookup"><span data-stu-id="bfcc6-396">For R you can use hello ```install.packages()``` in hello R console or use hello IDE and choose "**Packages** -> **Install Packages...**".</span></span>

## <a name="summary"></a><span data-ttu-id="bfcc6-397">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="bfcc6-397">Summary</span></span>
<span data-ttu-id="bfcc6-398">Questi sono solo alcune delle operazioni di hello che è possibile eseguire nella macchina virtuale di Microsoft Data Science hello.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-398">These are just some of hello things you can do on hello Microsoft Data Science Virtual Machine.</span></span> <span data-ttu-id="bfcc6-399">Sono disponibili molte altre operazioni che è possibile eseguire toomake è un ambiente analitica effettivo.</span><span class="sxs-lookup"><span data-stu-id="bfcc6-399">There are many more things you can do toomake it an effective analytics environment.</span></span>

