---
title: set di dati aaaAccess alla libreria client Python di Machine Learning | Documenti Microsoft
description: Installare e utilizzare hello tooaccess libreria client di Python e gestire i dati di Azure Machine Learning in modo sicuro da un ambiente locale in Python.
services: machine-learning
documentationcenter: python
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ab42272-c30c-4b7e-8e66-d64eafef22d0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: huvalo;bradsev
ms.openlocfilehash: f55067118f13c52bf677930a20836ce6989f8187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="access-datasets-with-python-using-hello-azure-machine-learning-python-client-library"></a><span data-ttu-id="0d070-103">Set di dati di accesso con Python mediante una libreria client di Azure Machine Learning Python hello</span><span class="sxs-lookup"><span data-stu-id="0d070-103">Access datasets with Python using hello Azure Machine Learning Python client library</span></span>
<span data-ttu-id="0d070-104">Anteprima Hello della libreria client Python di Microsoft Azure Machine Learning consente l'accesso sicuro tooyour Azure Machine Learning i set di dati da un ambiente di Python locale e consente la creazione di hello e gestione di set di dati in un'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="0d070-104">hello preview of Microsoft Azure Machine Learning Python client library can enable secure access tooyour Azure Machine Learning datasets from a local Python environment and enables hello creation and management of datasets in a workspace.</span></span>

<span data-ttu-id="0d070-105">Questo argomento fornisce istruzioni su come:</span><span class="sxs-lookup"><span data-stu-id="0d070-105">This topic provides instructions on how to:</span></span>

* <span data-ttu-id="0d070-106">installare una libreria client di Machine Learning Python hello</span><span class="sxs-lookup"><span data-stu-id="0d070-106">install hello Machine Learning Python client library</span></span> 
* <span data-ttu-id="0d070-107">accedere e caricare i set di dati, incluse le istruzioni su come tooget autorizzazione tooaccess set di dati di Azure Machine Learning dall'ambiente locale di Python</span><span class="sxs-lookup"><span data-stu-id="0d070-107">access and upload datasets, including instructions on how tooget authorization tooaccess Azure Machine Learning datasets from your local Python environment</span></span>
* <span data-ttu-id="0d070-108">Accedere ai set di dati intermedi di un esperimento</span><span class="sxs-lookup"><span data-stu-id="0d070-108">access intermediate datasets from experiments</span></span>
* <span data-ttu-id="0d070-109">Utilizzare i set di dati di hello Python client libreria tooenumerate, accedere ai metadati, leggere il contenuto di hello di un set di dati, creare nuovi set di dati e aggiornare i set di dati esistente</span><span class="sxs-lookup"><span data-stu-id="0d070-109">use hello Python client library tooenumerate datasets, access metadata, read hello contents of a dataset, create new datasets and update existing datasets</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <span data-ttu-id="0d070-110"><a name="prerequisites"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0d070-110"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="0d070-111">libreria client Python di Hello è stata testata in hello seguenti ambienti:</span><span class="sxs-lookup"><span data-stu-id="0d070-111">hello Python client library has been tested under hello following environments:</span></span>

* <span data-ttu-id="0d070-112">Windows, Mac e Linux</span><span class="sxs-lookup"><span data-stu-id="0d070-112">Windows, Mac and Linux</span></span>
* <span data-ttu-id="0d070-113">Python 2.7, 3.3 e 3.4</span><span class="sxs-lookup"><span data-stu-id="0d070-113">Python 2.7, 3.3 and 3.4</span></span>

<span data-ttu-id="0d070-114">E presenta una dipendenza su hello pacchetti seguenti:</span><span class="sxs-lookup"><span data-stu-id="0d070-114">It has a dependency on hello following packages:</span></span>

* <span data-ttu-id="0d070-115">requests</span><span class="sxs-lookup"><span data-stu-id="0d070-115">requests</span></span>
* <span data-ttu-id="0d070-116">python-dateutil</span><span class="sxs-lookup"><span data-stu-id="0d070-116">python-dateutil</span></span>
* <span data-ttu-id="0d070-117">pandas</span><span class="sxs-lookup"><span data-stu-id="0d070-117">pandas</span></span>

<span data-ttu-id="0d070-118">Si consiglia di utilizzare, ad esempio una distribuzione di Python [Anaconda](http://continuum.io/downloads#all) o [Canopy](https://store.enthought.com/downloads/), che vengono forniti con Python, IPython e installare i pacchetti hello tre elencati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0d070-118">We recommend using a Python distribution such as [Anaconda](http://continuum.io/downloads#all) or [Canopy](https://store.enthought.com/downloads/), which come with Python, IPython and hello three packages listed above installed.</span></span> <span data-ttu-id="0d070-119">Sebbene IPython non sia obbligatorio, costituisce un ambiente ottimale per la manipolazione e la visualizzazione dei dati in modo interattivo.</span><span class="sxs-lookup"><span data-stu-id="0d070-119">Although IPython is not strictly required, it is a great environment for manipulating and visualizing data interactively.</span></span>

### <span data-ttu-id="0d070-120"><a name="installation"></a>Come tooinstall hello libreria client Python di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0d070-120"><a name="installation"></a>How tooinstall hello Azure Machine Learning Python client library</span></span>
<span data-ttu-id="0d070-121">libreria client di Azure Machine Learning Python Hello debba essere installati toocomplete hello attività descritte in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="0d070-121">hello Azure Machine Learning Python client library must also be installed toocomplete hello tasks outlined in this topic.</span></span> <span data-ttu-id="0d070-122">È disponibile da hello [indice del pacchetto Python](https://pypi.python.org/pypi/azureml).</span><span class="sxs-lookup"><span data-stu-id="0d070-122">It is available from hello [Python Package Index](https://pypi.python.org/pypi/azureml).</span></span> <span data-ttu-id="0d070-123">tooinstall Python nell'ambiente in uso, eseguirlo hello il seguente comando da ambiente locale Python:</span><span class="sxs-lookup"><span data-stu-id="0d070-123">tooinstall it in your Python environment, run hello following command from your local Python environment:</span></span>

    pip install azureml

<span data-ttu-id="0d070-124">In alternativa, è possibile scaricare e installare da origini hello in [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span><span class="sxs-lookup"><span data-stu-id="0d070-124">Alternatively, you can download and install from hello sources on [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span></span>

    python setup.py install

<span data-ttu-id="0d070-125">Se si dispone di git installati nel computer, è possibile utilizzare tooinstall pip direttamente dal repository git hello:</span><span class="sxs-lookup"><span data-stu-id="0d070-125">If you have git installed on your machine, you can use pip tooinstall directly from hello git repository:</span></span>

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <span data-ttu-id="0d070-126"><a name="datasetAccess"></a>Utilizzano i DataSet tooaccess frammenti di codice Studio</span><span class="sxs-lookup"><span data-stu-id="0d070-126"><a name="datasetAccess"></a>Use Studio Code snippets tooaccess datasets</span></span>
<span data-ttu-id="0d070-127">libreria client Python di Hello permette l'accesso programmatico tooyour set di dati esistenti da esperimenti che sono stati eseguiti.</span><span class="sxs-lookup"><span data-stu-id="0d070-127">hello Python client library gives you programmatic access tooyour existing datasets from experiments that have been run.</span></span>

<span data-ttu-id="0d070-128">Dall'interfaccia web di hello Studio, è possibile generare frammenti di codice che includono tutti i toodownload le informazioni necessarie hello e deserializzare i set di dati come oggetti Pandas frame di dati nel computer di percorso.</span><span class="sxs-lookup"><span data-stu-id="0d070-128">From hello Studio web interface, you can generate code snippets that include all hello necessary information toodownload and deserialize datasets as Pandas DataFrame objects on your location machine.</span></span>

### <span data-ttu-id="0d070-129"><a name="security"></a>Sicurezza per l'accesso ai dati</span><span class="sxs-lookup"><span data-stu-id="0d070-129"><a name="security"></a>Security for data access</span></span>
<span data-ttu-id="0d070-130">frammenti di codice forniti da Studio per utilizzare alla libreria client Python di hello include l'id area di lavoro e l'autorizzazione di Hello token.</span><span class="sxs-lookup"><span data-stu-id="0d070-130">hello code snippets provided by Studio for use with hello Python client library includes your workspace id and authorization token.</span></span> <span data-ttu-id="0d070-131">Questi forniscono l'area di lavoro tooyour accesso completo e deve essere protetto, ad esempio una password.</span><span class="sxs-lookup"><span data-stu-id="0d070-131">These provide full access tooyour workspace and must be protected, like a password.</span></span>

<span data-ttu-id="0d070-132">Per motivi di sicurezza, la funzionalità dei frammenti di codice hello è solo toousers disponibile con il proprio ruolo impostato come **proprietario** per area di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="0d070-132">For security reasons, hello code snippet functionality is only available toousers that have their role set as **Owner** for hello workspace.</span></span> <span data-ttu-id="0d070-133">Il ruolo verrà visualizzato in Azure Machine Learning Studio hello **utenti** pagina **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="0d070-133">Your role is displayed in Azure Machine Learning Studio on hello **USERS** page under **Settings**.</span></span>

![Sicurezza][security]

<span data-ttu-id="0d070-135">Se il ruolo non è impostato come **proprietario**, è possibile richiedere toobe invito come proprietario, o richiedere al proprietario di hello dell'area di lavoro tooprovide hello è con il frammento di codice hello.</span><span class="sxs-lookup"><span data-stu-id="0d070-135">If your role is not set as **Owner**, you can either request toobe reinvited as an owner, or ask hello owner of hello workspace tooprovide you with hello code snippet.</span></span>

<span data-ttu-id="0d070-136">token di autorizzazione hello tooobtain, è possibile eseguire una delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="0d070-136">tooobtain hello authorization token, you can do one of hello following:</span></span>

* <span data-ttu-id="0d070-137">Chiedere un token a un proprietario.</span><span class="sxs-lookup"><span data-stu-id="0d070-137">Ask for a token from an owner.</span></span> <span data-ttu-id="0d070-138">I proprietari possono accedere i token di autorizzazione dalla pagina di impostazioni di hello della propria area di lavoro di Studio.</span><span class="sxs-lookup"><span data-stu-id="0d070-138">Owners can access their authorization tokens from hello Settings page of their workspace in Studio.</span></span> <span data-ttu-id="0d070-139">Selezionare **impostazioni** dal riquadro e fare clic a sinistra hello **token di autorizzazione** toosee hello token primario e secondario.</span><span class="sxs-lookup"><span data-stu-id="0d070-139">Select **Settings** from hello left pane and click **AUTHORIZATION TOKENS** toosee hello primary and secondary tokens.</span></span>  <span data-ttu-id="0d070-140">Sebbene hello primario o i token di autorizzazione secondario hello possono essere utilizzati nel frammento di codice hello, è consigliabile che i proprietari condividano solo i token di autorizzazione secondario hello.</span><span class="sxs-lookup"><span data-stu-id="0d070-140">Although either hello primary or hello secondary authorization tokens can be used in hello code snippet, it is recommended that owners only share hello secondary authorization tokens.</span></span>

![Token di autorizzazione](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* <span data-ttu-id="0d070-142">Chiedere toorole toobe alzate di livello del proprietario.</span><span class="sxs-lookup"><span data-stu-id="0d070-142">Ask toobe promoted toorole of owner.</span></span>  <span data-ttu-id="0d070-143">toodo questa operazione, un proprietario corrente di hello dell'area di lavoro esigenze toofirst è rimuovere dall'area di lavoro hello quindi nuovamente invito tooit come proprietario.</span><span class="sxs-lookup"><span data-stu-id="0d070-143">toodo this, a current owner of hello workspace needs toofirst remove you from hello workspace then re-invite you tooit as an owner.</span></span>

<span data-ttu-id="0d070-144">Dopo aver ottenuto gli sviluppatori id area di lavoro hello e l'autorizzazione token, sono in grado di tooaccess area di lavoro hello tramite il frammento di codice hello indipendentemente dal loro ruolo.</span><span class="sxs-lookup"><span data-stu-id="0d070-144">Once developers have obtained hello workspace id and authorization token, they are able tooaccess hello workspace using hello code snippet regardless of their role.</span></span>

<span data-ttu-id="0d070-145">Token di autorizzazione vengono gestiti nel hello **token di autorizzazione** pagina **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="0d070-145">Authorization tokens are managed on hello **AUTHORIZATION TOKENS** page under **SETTINGS**.</span></span> <span data-ttu-id="0d070-146">Può essere rigenerato, ma questa procedura revoca token di accesso toohello precedente.</span><span class="sxs-lookup"><span data-stu-id="0d070-146">You can regenerate them, but this procedure revokes access toohello previous token.</span></span>

### <span data-ttu-id="0d070-147"><a name="accessingDatasets"></a>Accedere a set di dati da un'applicazione Python locale</span><span class="sxs-lookup"><span data-stu-id="0d070-147"><a name="accessingDatasets"></a>Access datasets from a local Python application</span></span>
1. <span data-ttu-id="0d070-148">In Machine Learning Studio, fare clic su **set di dati** hello sinistra sulla barra di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="0d070-148">In Machine Learning Studio, click **DATASETS** in hello navigation bar on hello left.</span></span>
2. <span data-ttu-id="0d070-149">Selezionare hello set di dati tooaccess.</span><span class="sxs-lookup"><span data-stu-id="0d070-149">Select hello dataset you would like tooaccess.</span></span> <span data-ttu-id="0d070-150">È possibile selezionare uno dei set di dati hello hello **set di dati personali** elenco o da hello **esempi** elenco.</span><span class="sxs-lookup"><span data-stu-id="0d070-150">You can select any of hello datasets from hello **MY DATASETS** list or from hello **SAMPLES** list.</span></span>
3. <span data-ttu-id="0d070-151">Dalla barra degli strumenti nella parte inferiore di hello, fare clic su **genera codice di accesso ai dati**.</span><span class="sxs-lookup"><span data-stu-id="0d070-151">From hello bottom toolbar, click **Generate Data Access Code**.</span></span> <span data-ttu-id="0d070-152">Se i dati di hello in un formato incompatibile con una libreria client Python di hello, questo pulsante è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="0d070-152">If hello data is in a format incompatible with hello Python client library, this button is disabled.</span></span>
   
    ![DATASETS][datasets]
4. <span data-ttu-id="0d070-154">Selezionare il frammento di codice hello dalla finestra hello che viene visualizzata e copiarlo negli Appunti tooyour.</span><span class="sxs-lookup"><span data-stu-id="0d070-154">Select hello code snippet from hello window that appears and copy it tooyour clipboard.</span></span>
   
    ![Codice di accesso][dataset-access-code]
5. <span data-ttu-id="0d070-156">Incollare il codice hello notebook hello di applicazione Python locale.</span><span class="sxs-lookup"><span data-stu-id="0d070-156">Paste hello code into hello notebook of your local Python application.</span></span>
   
    ![Blocco appunti][ipython-dataset]

## <span data-ttu-id="0d070-158"><a name="accessingIntermediateDatasets"></a>Accedere a set di dati intermedi da esperimenti di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0d070-158"><a name="accessingIntermediateDatasets"></a>Access intermediate datasets from Machine Learning experiments</span></span>
<span data-ttu-id="0d070-159">Dopo l'esecuzione di un esperimento in hello Machine Learning Studio, è possibile tooaccess hello intermedia set di dati di nodi di output di hello dei moduli.</span><span class="sxs-lookup"><span data-stu-id="0d070-159">After an experiment is run in hello Machine Learning Studio, it is possible tooaccess hello intermediate datasets from hello output nodes of modules.</span></span> <span data-ttu-id="0d070-160">I set di dati intermedi sono costituiti da dati creati e usati per i passaggi intermedi quando è in esecuzione uno strumento di modello.</span><span class="sxs-lookup"><span data-stu-id="0d070-160">Intermediate datasets are data that has been created and used for intermediate steps when a model tool has been run.</span></span>

<span data-ttu-id="0d070-161">Set di dati intermedi sono accessibili, purché il formato di dati hello è compatibile con libreria client Python di hello.</span><span class="sxs-lookup"><span data-stu-id="0d070-161">Intermediate datasets can be accessed as long as hello data format is compatible with hello Python client library.</span></span>

<span data-ttu-id="0d070-162">Hello sono supportati i seguenti formati (costanti per questi sono hello `azureml.DataTypeIds` classe):</span><span class="sxs-lookup"><span data-stu-id="0d070-162">hello following formats are supported (constants for these are in hello `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="0d070-163">PlainText</span><span class="sxs-lookup"><span data-stu-id="0d070-163">PlainText</span></span>
* <span data-ttu-id="0d070-164">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="0d070-164">GenericCSV</span></span>
* <span data-ttu-id="0d070-165">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="0d070-165">GenericTSV</span></span>
* <span data-ttu-id="0d070-166">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="0d070-166">GenericCSVNoHeader</span></span>
* <span data-ttu-id="0d070-167">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="0d070-167">GenericTSVNoHeader</span></span>

<span data-ttu-id="0d070-168">È possibile determinare formato hello al passaggio del mouse su un nodo di output del modulo.</span><span class="sxs-lookup"><span data-stu-id="0d070-168">You can determine hello format by hovering over a module output node.</span></span> <span data-ttu-id="0d070-169">Viene visualizzato insieme al nome nodo hello, in una descrizione comando.</span><span class="sxs-lookup"><span data-stu-id="0d070-169">It is displayed along with hello node name, in a tooltip.</span></span>

<span data-ttu-id="0d070-170">Alcuni dei moduli di hello, ad esempio hello [Split] [ split] modulo, denominato formato di output tooa `Dataset`, che non è supportato dalla libreria client Python di hello.</span><span class="sxs-lookup"><span data-stu-id="0d070-170">Some of hello modules, such as hello [Split][split] module, output tooa format named `Dataset`, which is not supported by hello Python client library.</span></span>

![Formato del set di dati][dataset-format]

<span data-ttu-id="0d070-172">È necessario toouse un modulo di conversione, ad esempio [convertire tooCSV][convert-to-csv], tooget un output in un formato supportato.</span><span class="sxs-lookup"><span data-stu-id="0d070-172">You need toouse a conversion module, such as [Convert tooCSV][convert-to-csv], tooget an output into a supported format.</span></span>

![Formato GenericCSV][csv-format]

<span data-ttu-id="0d070-174">Hello passaggi seguenti viene illustrato un esempio che crea un esperimento, eseguirlo e accede a set di dati intermedi hello.</span><span class="sxs-lookup"><span data-stu-id="0d070-174">hello following steps show an example that creates an experiment, runs it and accesses hello intermediate dataset.</span></span>

1. <span data-ttu-id="0d070-175">Creare un nuovo esperimento.</span><span class="sxs-lookup"><span data-stu-id="0d070-175">Create a new experiment.</span></span>
2. <span data-ttu-id="0d070-176">Inserire un modulo **Adult Census Income Binary Classification dataset** .</span><span class="sxs-lookup"><span data-stu-id="0d070-176">Insert an **Adult Census Income Binary Classification dataset** module.</span></span>
3. <span data-ttu-id="0d070-177">Inserire un [Split] [ split] modulo e connettere l'output di modulo di input toohello set di dati.</span><span class="sxs-lookup"><span data-stu-id="0d070-177">Insert a [Split][split] module, and connect its input toohello dataset module output.</span></span>
4. <span data-ttu-id="0d070-178">Inserire un [convertire tooCSV] [ convert-to-csv] modulo e il relativo input tooone di hello connettersi [Split] [ split] modulo restituisce.</span><span class="sxs-lookup"><span data-stu-id="0d070-178">Insert a [Convert tooCSV][convert-to-csv] module and connect its input tooone of hello [Split][split] module outputs.</span></span>
5. <span data-ttu-id="0d070-179">Salvare l'esperimento hello, eseguirlo e attendere che toofinish in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0d070-179">Save hello experiment, run it, and wait for it toofinish running.</span></span>
6. <span data-ttu-id="0d070-180">Fare clic sul nodo di output di hello in hello [convertire tooCSV] [ convert-to-csv] modulo.</span><span class="sxs-lookup"><span data-stu-id="0d070-180">Click hello output node on hello [Convert tooCSV][convert-to-csv] module.</span></span>
7. <span data-ttu-id="0d070-181">Quando viene visualizzato il menu di scelta rapida hello, selezionare **genera codice di accesso ai dati**.</span><span class="sxs-lookup"><span data-stu-id="0d070-181">When hello context menu appears, select **Generate Data Access Code**.</span></span>
   
    ![Menu di scelta rapida][experiment]
8. <span data-ttu-id="0d070-183">Selezionare il frammento di codice hello e copiarlo negli Appunti tooyour dalla finestra hello che viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="0d070-183">Select hello code snippet and copy it tooyour clipboard from hello window that appears.</span></span>
   
    ![Codice di accesso][intermediate-dataset-access-code]
9. <span data-ttu-id="0d070-185">Incollare il codice hello nel blocco note.</span><span class="sxs-lookup"><span data-stu-id="0d070-185">Paste hello code in your notebook.</span></span>
   
    ![Blocco appunti][ipython-intermediate-dataset]
10. <span data-ttu-id="0d070-187">È possibile visualizzare i dati di hello usando matplotlib.</span><span class="sxs-lookup"><span data-stu-id="0d070-187">You can visualize hello data using matplotlib.</span></span> <span data-ttu-id="0d070-188">Verrà visualizzata in un istogramma per la colonna age hello:</span><span class="sxs-lookup"><span data-stu-id="0d070-188">This displays in a histogram for hello age column:</span></span>
    
    ![Istogramma][ipython-histogram]

## <span data-ttu-id="0d070-190"><a name="clientApis"></a>Utilizzare tooaccess libreria client Python di Machine Learning di hello, leggere, creare e gestire set di dati</span><span class="sxs-lookup"><span data-stu-id="0d070-190"><a name="clientApis"></a>Use hello Machine Learning Python client library tooaccess, read, create, and manage datasets</span></span>
### <a name="workspace"></a><span data-ttu-id="0d070-191">Area di lavoro</span><span class="sxs-lookup"><span data-stu-id="0d070-191">Workspace</span></span>
<span data-ttu-id="0d070-192">area di lavoro di Hello è il punto di ingresso hello per la libreria client Python di hello.</span><span class="sxs-lookup"><span data-stu-id="0d070-192">hello workspace is hello entry point for hello Python client library.</span></span> <span data-ttu-id="0d070-193">Fornire hello `Workspace` classe con l'area di lavoro id e l'autorizzazione toocreate di token a un'istanza:</span><span class="sxs-lookup"><span data-stu-id="0d070-193">Provide hello `Workspace` class with your workspace id and authorization token toocreate an instance:</span></span>

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a><span data-ttu-id="0d070-194">Enumerare set di dati</span><span class="sxs-lookup"><span data-stu-id="0d070-194">Enumerate datasets</span></span>
<span data-ttu-id="0d070-195">tooenumerate tutti i set di dati di una determinata area di lavoro:</span><span class="sxs-lookup"><span data-stu-id="0d070-195">tooenumerate all datasets in a given workspace:</span></span>

    for ds in ws.datasets:
        print(ds.name)

<span data-ttu-id="0d070-196">tooenumerate hello appena creati dall'utente i set di dati:</span><span class="sxs-lookup"><span data-stu-id="0d070-196">tooenumerate just hello user-created datasets:</span></span>

    for ds in ws.user_datasets:
        print(ds.name)

<span data-ttu-id="0d070-197">tooenumerate set di dati per l'esempio hello solo:</span><span class="sxs-lookup"><span data-stu-id="0d070-197">tooenumerate just hello example datasets:</span></span>

    for ds in ws.example_datasets:
        print(ds.name)

<span data-ttu-id="0d070-198">È possibile accedere a un set di dati per nome (si applica la distinzione maiuscole/minuscole):</span><span class="sxs-lookup"><span data-stu-id="0d070-198">You can access a dataset by name (which is case-sensitive):</span></span>

    ds = ws.datasets['my dataset name']

<span data-ttu-id="0d070-199">In alternativa, è possibile accedere tramite indice:</span><span class="sxs-lookup"><span data-stu-id="0d070-199">Or you can access it by index:</span></span>

    ds = ws.datasets[0]


### <a name="metadata"></a><span data-ttu-id="0d070-200">Metadata</span><span class="sxs-lookup"><span data-stu-id="0d070-200">Metadata</span></span>
<span data-ttu-id="0d070-201">Set di dati dispongono di metadati, in aggiunta toocontent.</span><span class="sxs-lookup"><span data-stu-id="0d070-201">Datasets have metadata, in addition toocontent.</span></span> <span data-ttu-id="0d070-202">(Set di dati intermedi sono una regola di eccezione toothis e non dispone di tutti i metadati).</span><span class="sxs-lookup"><span data-stu-id="0d070-202">(Intermediate datasets are an exception toothis rule and do not have any metadata.)</span></span>

<span data-ttu-id="0d070-203">Alcuni valori dei metadati vengono assegnati dall'utente hello in fase di creazione:</span><span class="sxs-lookup"><span data-stu-id="0d070-203">Some metadata values are assigned by hello user at creation time:</span></span>

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

<span data-ttu-id="0d070-204">Altri valori vengono assegnati da Azure Machine Learning:</span><span class="sxs-lookup"><span data-stu-id="0d070-204">Others are values assigned by Azure ML:</span></span>

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

<span data-ttu-id="0d070-205">Vedere hello `SourceDataset` classe per altre su hello disponibili i metadati.</span><span class="sxs-lookup"><span data-stu-id="0d070-205">See hello `SourceDataset` class for more on hello available metadata.</span></span>

### <a name="read-contents"></a><span data-ttu-id="0d070-206">Leggere il contenuto</span><span class="sxs-lookup"><span data-stu-id="0d070-206">Read contents</span></span>
<span data-ttu-id="0d070-207">frammenti di codice Hello forniti automaticamente da Machine Learning Studio scaricano e deserializzare l'oggetto di hello dataset tooa Pandas frame di dati.</span><span class="sxs-lookup"><span data-stu-id="0d070-207">hello code snippets provided by Machine Learning Studio automatically download and deserialize hello dataset tooa Pandas DataFrame object.</span></span> <span data-ttu-id="0d070-208">Questa operazione viene eseguita con hello `to_dataframe` metodo:</span><span class="sxs-lookup"><span data-stu-id="0d070-208">This is done with hello `to_dataframe` method:</span></span>

    frame = ds.to_dataframe()

<span data-ttu-id="0d070-209">Se si preferiscono dati non elaborati di toodownload hello ed esegue manualmente la deserializzazione di hello, che è un'opzione.</span><span class="sxs-lookup"><span data-stu-id="0d070-209">If you prefer toodownload hello raw data, and perform hello deserialization yourself, that is an option.</span></span> <span data-ttu-id="0d070-210">In un momento hello, questa è hello unica opzione per i formati, ad esempio 'ARFF', non è possibile deserializzare la libreria client Python di hello.</span><span class="sxs-lookup"><span data-stu-id="0d070-210">At hello moment, this is hello only option for formats such as 'ARFF', which hello Python client library cannot deserialize.</span></span>

<span data-ttu-id="0d070-211">contenuto di hello tooread come testo:</span><span class="sxs-lookup"><span data-stu-id="0d070-211">tooread hello contents as text:</span></span>

    text_data = ds.read_as_text()

<span data-ttu-id="0d070-212">contenuto di hello tooread in formato binario:</span><span class="sxs-lookup"><span data-stu-id="0d070-212">tooread hello contents as binary:</span></span>

    binary_data = ds.read_as_binary()

<span data-ttu-id="0d070-213">È possibile anche aprire un contenuto di flusso toohello:</span><span class="sxs-lookup"><span data-stu-id="0d070-213">You can also just open a stream toohello contents:</span></span>

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a><span data-ttu-id="0d070-214">Creare un nuovo set di dati</span><span class="sxs-lookup"><span data-stu-id="0d070-214">Create a new dataset</span></span>
<span data-ttu-id="0d070-215">libreria client Python di Hello consente tooupload i set di dati dal programma Python.</span><span class="sxs-lookup"><span data-stu-id="0d070-215">hello Python client library allows you tooupload datasets from your Python program.</span></span> <span data-ttu-id="0d070-216">per poterli usare nell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="0d070-216">These datasets are then available for use in your workspace.</span></span>

<span data-ttu-id="0d070-217">Se i dati si trovano in un frame di dati Pandas, utilizzare hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="0d070-217">If you have your data in a Pandas DataFrame, use hello following code:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="0d070-218">Se invece i dati sono già serializzati, è possibile usare:</span><span class="sxs-lookup"><span data-stu-id="0d070-218">If your data is already serialized, you can use:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="0d070-219">libreria client Python Hello è in grado di tooserialize Pandas DataFrame toohello seguito formati (costanti per questi sono hello `azureml.DataTypeIds` classe):</span><span class="sxs-lookup"><span data-stu-id="0d070-219">hello Python client library is able tooserialize a Pandas DataFrame toohello following formats (constants for these are in hello `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="0d070-220">PlainText</span><span class="sxs-lookup"><span data-stu-id="0d070-220">PlainText</span></span>
* <span data-ttu-id="0d070-221">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="0d070-221">GenericCSV</span></span>
* <span data-ttu-id="0d070-222">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="0d070-222">GenericTSV</span></span>
* <span data-ttu-id="0d070-223">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="0d070-223">GenericCSVNoHeader</span></span>
* <span data-ttu-id="0d070-224">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="0d070-224">GenericTSVNoHeader</span></span>

### <a name="update-an-existing-dataset"></a><span data-ttu-id="0d070-225">Aggiornare un set di dati esistente</span><span class="sxs-lookup"><span data-stu-id="0d070-225">Update an existing dataset</span></span>
<span data-ttu-id="0d070-226">Se si tenta di tooupload un nuovo set di dati con un nome che corrisponde a un set di dati esistente, è necessario ottenere un errore di conflitto.</span><span class="sxs-lookup"><span data-stu-id="0d070-226">If you try tooupload a new dataset with a name that matches an existing dataset, you should get a conflict error.</span></span>

<span data-ttu-id="0d070-227">tooupdate un set di dati esistente, è innanzitutto necessario tooget un dataset esistente toohello di riferimento:</span><span class="sxs-lookup"><span data-stu-id="0d070-227">tooupdate an existing dataset, you first need tooget a reference toohello existing dataset:</span></span>

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="0d070-228">Utilizzare quindi `update_from_dataframe` tooserialize e sostituire contenuto hello del set di dati di hello in Azure:</span><span class="sxs-lookup"><span data-stu-id="0d070-228">Then use `update_from_dataframe` tooserialize and replace hello contents of hello dataset on Azure:</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="0d070-229">Se si desidera tooserialize hello dati tooa altro formato, specificare un valore per hello facoltativo `data_type_id` parametro.</span><span class="sxs-lookup"><span data-stu-id="0d070-229">If you want tooserialize hello data tooa different format, specify a value for hello optional `data_type_id` parameter.</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="0d070-230">Facoltativamente, è possibile impostare una nuova descrizione specificando un valore per hello `description` parametro.</span><span class="sxs-lookup"><span data-stu-id="0d070-230">You can optionally set a new description by specifying a value for hello `description` parameter.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toofeb 2015'

<span data-ttu-id="0d070-231">Facoltativamente, è possibile impostare un nuovo nome, specificando un valore per hello `name` parametro.</span><span class="sxs-lookup"><span data-stu-id="0d070-231">You can optionally set a new name by specifying a value for hello `name` parameter.</span></span> <span data-ttu-id="0d070-232">In futuro, si recupererà hello dataset utilizzando hello solo nuovo nome.</span><span class="sxs-lookup"><span data-stu-id="0d070-232">From now on, you'll retrieve hello dataset using hello new name only.</span></span> <span data-ttu-id="0d070-233">Hello seguente codice Aggiorna dati hello, descrizione e nome.</span><span class="sxs-lookup"><span data-stu-id="0d070-233">hello following code updates hello data, name and description.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up toofeb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

<span data-ttu-id="0d070-234">Hello `data_type_id`, `name` e `description` i parametri sono facoltativi e il valore precedente tootheir predefinito.</span><span class="sxs-lookup"><span data-stu-id="0d070-234">hello `data_type_id`, `name` and `description` parameters are optional and default tootheir previous value.</span></span> <span data-ttu-id="0d070-235">Hello `dataframe` parametro è sempre obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="0d070-235">hello `dataframe` parameter is always required.</span></span>

<span data-ttu-id="0d070-236">Se i dati sono già serializzati, usare `update_from_raw_data` anziché `update_from_dataframe`.</span><span class="sxs-lookup"><span data-stu-id="0d070-236">If your data is already serialized, use `update_from_raw_data` instead of `update_from_dataframe`.</span></span> <span data-ttu-id="0d070-237">Il funzionamento è analogo: è sufficiente passare `raw_data` invece di `dataframe`.</span><span class="sxs-lookup"><span data-stu-id="0d070-237">If you just pass in `raw_data` instead of  `dataframe`, it works in a similar way.</span></span>

<!-- Images -->
[security]:./media/machine-learning-python-data-access/security.png
[dataset-format]:./media/machine-learning-python-data-access/dataset-format.png
[csv-format]:./media/machine-learning-python-data-access/csv-format.png
[datasets]:./media/machine-learning-python-data-access/datasets.png
[dataset-access-code]:./media/machine-learning-python-data-access/dataset-access-code.png
[ipython-dataset]:./media/machine-learning-python-data-access/ipython-dataset.png
[experiment]:./media/machine-learning-python-data-access/experiment.png
[intermediate-dataset-access-code]:./media/machine-learning-python-data-access/intermediate-dataset-access-code.png
[ipython-intermediate-dataset]:./media/machine-learning-python-data-access/ipython-intermediate-dataset.png
[ipython-histogram]:./media/machine-learning-python-data-access/ipython-histogram.png


<!-- Module References -->
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

