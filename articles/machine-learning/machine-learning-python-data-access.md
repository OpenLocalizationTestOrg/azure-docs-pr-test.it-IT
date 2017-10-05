---
title: Accedere a set di dati tramite la libreria client Python di Azure Machine Learning | Microsoft Docs
description: Installare e usare la libreria client Python per accedere e gestire i dati di Azure Machine Learning in modo protetto da un ambiente Python locale.
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
ms.openlocfilehash: e3ae712e0f8d386f637520fbbff4b348bc86f32d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="access-datasets-with-python-using-the-azure-machine-learning-python-client-library"></a><span data-ttu-id="aa4f3-103">Accedere a set di dati con Python mediante la libreria client Python di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="aa4f3-103">Access datasets with Python using the Azure Machine Learning Python client library</span></span>
<span data-ttu-id="aa4f3-104">L'anteprima della libreria client Python di Microsoft Azure Machine Learning consente l'accesso sicuro a set di dati di Azure Machine Learning da un ambiente Python locale, nonché la creazione e la gestione di set di dati in un'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-104">The preview of Microsoft Azure Machine Learning Python client library can enable secure access to your Azure Machine Learning datasets from a local Python environment and enables the creation and management of datasets in a workspace.</span></span>

<span data-ttu-id="aa4f3-105">Questo argomento fornisce istruzioni su come:</span><span class="sxs-lookup"><span data-stu-id="aa4f3-105">This topic provides instructions on how to:</span></span>

* <span data-ttu-id="aa4f3-106">Installare la libreria client Python di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="aa4f3-106">install the Machine Learning Python client library</span></span> 
* <span data-ttu-id="aa4f3-107">Accedere e caricare set di dati, fornendo istruzioni su come ottenere l'autorizzazione per accedere a set di dati di Azure Machine Learning dall'ambiente Python locale</span><span class="sxs-lookup"><span data-stu-id="aa4f3-107">access and upload datasets, including instructions on how to get authorization to access Azure Machine Learning datasets from your local Python environment</span></span>
* <span data-ttu-id="aa4f3-108">Accedere ai set di dati intermedi di un esperimento</span><span class="sxs-lookup"><span data-stu-id="aa4f3-108">access intermediate datasets from experiments</span></span>
* <span data-ttu-id="aa4f3-109">Usare la libreria client Python per enumerare set di dati, accedere a metadati, leggere il contenuto di un set di dati, creare nuovi set di dati e aggiornare set di dati esistenti.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-109">use the Python client library to enumerate datasets, access metadata, read the contents of a dataset, create new datasets and update existing datasets</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <span data-ttu-id="aa4f3-110"><a name="prerequisites"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="aa4f3-110"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="aa4f3-111">La libreria client Python è stata testata negli ambienti seguenti:</span><span class="sxs-lookup"><span data-stu-id="aa4f3-111">The Python client library has been tested under the following environments:</span></span>

* <span data-ttu-id="aa4f3-112">Windows, Mac e Linux</span><span class="sxs-lookup"><span data-stu-id="aa4f3-112">Windows, Mac and Linux</span></span>
* <span data-ttu-id="aa4f3-113">Python 2.7, 3.3 e 3.4</span><span class="sxs-lookup"><span data-stu-id="aa4f3-113">Python 2.7, 3.3 and 3.4</span></span>

<span data-ttu-id="aa4f3-114">Presenta una dipendenza dai pacchetti seguenti:</span><span class="sxs-lookup"><span data-stu-id="aa4f3-114">It has a dependency on the following packages:</span></span>

* <span data-ttu-id="aa4f3-115">requests</span><span class="sxs-lookup"><span data-stu-id="aa4f3-115">requests</span></span>
* <span data-ttu-id="aa4f3-116">python-dateutil</span><span class="sxs-lookup"><span data-stu-id="aa4f3-116">python-dateutil</span></span>
* <span data-ttu-id="aa4f3-117">pandas</span><span class="sxs-lookup"><span data-stu-id="aa4f3-117">pandas</span></span>

<span data-ttu-id="aa4f3-118">È consigliabile usare una distribuzione Python, ad esempio [Anaconda](http://continuum.io/downloads#all) o [Canopy](https://store.enthought.com/downloads/), inclusa in Python, IPython e i tre pacchetti installati ed elencati precedentemente.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-118">We recommend using a Python distribution such as [Anaconda](http://continuum.io/downloads#all) or [Canopy](https://store.enthought.com/downloads/), which come with Python, IPython and the three packages listed above installed.</span></span> <span data-ttu-id="aa4f3-119">Sebbene IPython non sia obbligatorio, costituisce un ambiente ottimale per la manipolazione e la visualizzazione dei dati in modo interattivo.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-119">Although IPython is not strictly required, it is a great environment for manipulating and visualizing data interactively.</span></span>

### <span data-ttu-id="aa4f3-120"><a name="installation"></a>Come installare la libreria client Python di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="aa4f3-120"><a name="installation"></a>How to install the Azure Machine Learning Python client library</span></span>
<span data-ttu-id="aa4f3-121">Per completare le attività descritte in questo argomento, è necessario che sia installata la libreria client Python di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-121">The Azure Machine Learning Python client library must also be installed to complete the tasks outlined in this topic.</span></span> <span data-ttu-id="aa4f3-122">È disponibile nella pagina [Python Package Index](https://pypi.python.org/pypi/azureml).</span><span class="sxs-lookup"><span data-stu-id="aa4f3-122">It is available from the [Python Package Index](https://pypi.python.org/pypi/azureml).</span></span> <span data-ttu-id="aa4f3-123">Per installarla nel proprio ambiente Python, eseguire il comando seguente dall'ambiente Python locale:</span><span class="sxs-lookup"><span data-stu-id="aa4f3-123">To install it in your Python environment, run the following command from your local Python environment:</span></span>

    pip install azureml

<span data-ttu-id="aa4f3-124">In alternativa, è possibile scaricarla e installarla dalle origini disponibili in [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span><span class="sxs-lookup"><span data-stu-id="aa4f3-124">Alternatively, you can download and install from the sources on [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span></span>

    python setup.py install

<span data-ttu-id="aa4f3-125">Se nel proprio computer è installato Git, è possibile usare pip per installarla direttamente dal repository Git.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-125">If you have git installed on your machine, you can use pip to install directly from the git repository:</span></span>

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <span data-ttu-id="aa4f3-126"><a name="datasetAccess"></a>Usare frammenti di codice di Studio per accedere a set di dati</span><span class="sxs-lookup"><span data-stu-id="aa4f3-126"><a name="datasetAccess"></a>Use Studio Code snippets to access datasets</span></span>
<span data-ttu-id="aa4f3-127">La libreria client Python consente l'accesso a livello di codice a set di dati esistenti in esperimenti in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-127">The Python client library gives you programmatic access to your existing datasets from experiments that have been run.</span></span>

<span data-ttu-id="aa4f3-128">Dall'interfaccia Web di Studio è possibile generare frammenti di codice che includono tutte le informazioni necessarie per scaricare e deserializzare set di dati come oggetti Pandas DataFrame nel proprio computer locale.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-128">From the Studio web interface, you can generate code snippets that include all the necessary information to download and deserialize datasets as Pandas DataFrame objects on your location machine.</span></span>

### <span data-ttu-id="aa4f3-129"><a name="security"></a>Sicurezza per l'accesso ai dati</span><span class="sxs-lookup"><span data-stu-id="aa4f3-129"><a name="security"></a>Security for data access</span></span>
<span data-ttu-id="aa4f3-130">I frammenti di codice forniti da Studio per essere usati con la libreria client Python includono l'ID dell'area di lavoro e il token di autorizzazione,</span><span class="sxs-lookup"><span data-stu-id="aa4f3-130">The code snippets provided by Studio for use with the Python client library includes your workspace id and authorization token.</span></span> <span data-ttu-id="aa4f3-131">che offrono l'accesso completo all'area di lavoro e pertanto devono essere protetti, come una password.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-131">These provide full access to your workspace and must be protected, like a password.</span></span>

<span data-ttu-id="aa4f3-132">Per motivi di sicurezza, le funzionalità dei frammenti di codice sono disponibili solo per gli utenti il cui ruolo nell'area di lavoro è impostato su **Owner** .</span><span class="sxs-lookup"><span data-stu-id="aa4f3-132">For security reasons, the code snippet functionality is only available to users that have their role set as **Owner** for the workspace.</span></span> <span data-ttu-id="aa4f3-133">Il ruolo viene visualizzato in Azure Machine Learning Studio nella pagina **USERS** in **Settings**.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-133">Your role is displayed in Azure Machine Learning Studio on the **USERS** page under **Settings**.</span></span>

![Sicurezza][security]

<span data-ttu-id="aa4f3-135">Se il proprio ruolo non è impostato su **Owner**, è possibile chiedere di essere nuovamente invitati con il ruolo di proprietario o chiedere il frammento di codice al proprietario dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-135">If your role is not set as **Owner**, you can either request to be reinvited as an owner, or ask the owner of the workspace to provide you with the code snippet.</span></span>

<span data-ttu-id="aa4f3-136">Per ottenere il token di autorizzazione, è possibile eseguire una di queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="aa4f3-136">To obtain the authorization token, you can do one of the following:</span></span>

* <span data-ttu-id="aa4f3-137">Chiedere un token a un proprietario.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-137">Ask for a token from an owner.</span></span> <span data-ttu-id="aa4f3-138">I proprietari possono accedere ai propri token di autorizzazione dalla pagina Settings dell'area di lavoro personale in Studio.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-138">Owners can access their authorization tokens from the Settings page of their workspace in Studio.</span></span> <span data-ttu-id="aa4f3-139">Selezionare **Settings** (Impostazioni) dal riquadro sinistro e fare clic su **AUTHORIZATION TOKENS** (Token di autorizzazione) per visualizzare i token primari e secondari.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-139">Select **Settings** from the left pane and click **AUTHORIZATION TOKENS** to see the primary and secondary tokens.</span></span>  <span data-ttu-id="aa4f3-140">Sebbene per il frammento di codice sia possibile usare sia i token di autorizzazione primari sia quelli secondari, è consigliabile che i proprietari condividano solo i token di autorizzazione secondari.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-140">Although either the primary or the secondary authorization tokens can be used in the code snippet, it is recommended that owners only share the secondary authorization tokens.</span></span>

![Token di autorizzazione](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* <span data-ttu-id="aa4f3-142">Chiedere di essere promossi al ruolo di proprietario.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-142">Ask to be promoted to role of owner.</span></span>  <span data-ttu-id="aa4f3-143">A questo scopo, è necessario prima essere rimossi dall'area di lavoro da un proprietario corrente dell'area di lavoro, quindi essere nuovamente invitati con il ruolo di proprietario.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-143">To do this, a current owner of the workspace needs to first remove you from the workspace then re-invite you to it as an owner.</span></span>

<span data-ttu-id="aa4f3-144">Dopo aver ottenuto l'ID dell'area di lavoro e il token di autorizzazione, gli sviluppatori possono usare il frammento di codice per accedere all'area di lavoro indipendentemente dal proprio ruolo.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-144">Once developers have obtained the workspace id and authorization token, they are able to access the workspace using the code snippet regardless of their role.</span></span>

<span data-ttu-id="aa4f3-145">I token di autorizzazione vengono gestiti nella pagina **AUTHORIZATION TOKENS** in **SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-145">Authorization tokens are managed on the **AUTHORIZATION TOKENS** page under **SETTINGS**.</span></span> <span data-ttu-id="aa4f3-146">È possibile rigenerarli, ma questa procedura revoca l'accesso al token precedente.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-146">You can regenerate them, but this procedure revokes access to the previous token.</span></span>

### <span data-ttu-id="aa4f3-147"><a name="accessingDatasets"></a>Accedere a set di dati da un'applicazione Python locale</span><span class="sxs-lookup"><span data-stu-id="aa4f3-147"><a name="accessingDatasets"></a>Access datasets from a local Python application</span></span>
1. <span data-ttu-id="aa4f3-148">In Machine Learning Studio fare clic su **DATASETS** (Set di dati) sulla barra di spostamento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-148">In Machine Learning Studio, click **DATASETS** in the navigation bar on the left.</span></span>
2. <span data-ttu-id="aa4f3-149">Selezionare il set di dati a cui si desidera accedere.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-149">Select the dataset you would like to access.</span></span> <span data-ttu-id="aa4f3-150">È possibile selezionare qualsiasi set di dati dall'elenco **MY DATASETS** o **SAMPLES**.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-150">You can select any of the datasets from the **MY DATASETS** list or from the **SAMPLES** list.</span></span>
3. <span data-ttu-id="aa4f3-151">Sulla barra degli strumenti inferiore fare clic su **Generate Data Access Code**(Genera codice di accesso ai dati).</span><span class="sxs-lookup"><span data-stu-id="aa4f3-151">From the bottom toolbar, click **Generate Data Access Code**.</span></span> <span data-ttu-id="aa4f3-152">Se i dati si presentano in un formato non compatibile con la raccolta client di Python, questo pulsante non è attivo.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-152">If the data is in a format incompatible with the Python client library, this button is disabled.</span></span>
   
    ![DATASETS][datasets]
4. <span data-ttu-id="aa4f3-154">Selezionare il frammento di codice dalla finestra che viene visualizzata e copiarlo negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-154">Select the code snippet from the window that appears and copy it to your clipboard.</span></span>
   
    ![Codice di accesso][dataset-access-code]
5. <span data-ttu-id="aa4f3-156">Incollare il codice nel blocco appunti dell'applicazione Python locale.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-156">Paste the code into the notebook of your local Python application.</span></span>
   
    ![Blocco appunti][ipython-dataset]

## <span data-ttu-id="aa4f3-158"><a name="accessingIntermediateDatasets"></a>Accedere a set di dati intermedi da esperimenti di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="aa4f3-158"><a name="accessingIntermediateDatasets"></a>Access intermediate datasets from Machine Learning experiments</span></span>
<span data-ttu-id="aa4f3-159">Dopo aver eseguito un esperimento in Machine Learning Studio, è possibile accedere ai set di dati intermedi dai nodi di output dei moduli.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-159">After an experiment is run in the Machine Learning Studio, it is possible to access the intermediate datasets from the output nodes of modules.</span></span> <span data-ttu-id="aa4f3-160">I set di dati intermedi sono costituiti da dati creati e usati per i passaggi intermedi quando è in esecuzione uno strumento di modello.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-160">Intermediate datasets are data that has been created and used for intermediate steps when a model tool has been run.</span></span>

<span data-ttu-id="aa4f3-161">È possibile accedere ai set di dati intermedi sono se si trovano in un formato compatibile con la libreria client Python.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-161">Intermediate datasets can be accessed as long as the data format is compatible with the Python client library.</span></span>

<span data-ttu-id="aa4f3-162">Sono supportati i formati seguenti (le costanti per questi formati sono disponibili nella classe `azureml.DataTypeIds` ):</span><span class="sxs-lookup"><span data-stu-id="aa4f3-162">The following formats are supported (constants for these are in the `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="aa4f3-163">PlainText</span><span class="sxs-lookup"><span data-stu-id="aa4f3-163">PlainText</span></span>
* <span data-ttu-id="aa4f3-164">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="aa4f3-164">GenericCSV</span></span>
* <span data-ttu-id="aa4f3-165">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="aa4f3-165">GenericTSV</span></span>
* <span data-ttu-id="aa4f3-166">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="aa4f3-166">GenericCSVNoHeader</span></span>
* <span data-ttu-id="aa4f3-167">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="aa4f3-167">GenericTSVNoHeader</span></span>

<span data-ttu-id="aa4f3-168">È possibile determinare il formato passando il puntatore del mouse su un nodo di output del modulo.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-168">You can determine the format by hovering over a module output node.</span></span> <span data-ttu-id="aa4f3-169">Il formato viene visualizzato in una descrizione comando insieme al nome del nodo.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-169">It is displayed along with the node name, in a tooltip.</span></span>

<span data-ttu-id="aa4f3-170">Alcuni moduli, ad esempio [Split][split], eseguono l'output in un formato denominato `Dataset`, che non è supportato dalla libreria client Python.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-170">Some of the modules, such as the [Split][split] module, output to a format named `Dataset`, which is not supported by the Python client library.</span></span>

![Formato del set di dati][dataset-format]

<span data-ttu-id="aa4f3-172">Per ottenere un output in un formato supportato, è necessario usare un modulo di conversione, ad esempio [Convert to CSV][convert-to-csv] (Converti in CSV).</span><span class="sxs-lookup"><span data-stu-id="aa4f3-172">You need to use a conversion module, such as [Convert to CSV][convert-to-csv], to get an output into a supported format.</span></span>

![Formato GenericCSV][csv-format]

<span data-ttu-id="aa4f3-174">I passaggi seguenti illustrano un esempio in cui si crea e si esegue un esperimento e si accede al set di dati intermedio.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-174">The following steps show an example that creates an experiment, runs it and accesses the intermediate dataset.</span></span>

1. <span data-ttu-id="aa4f3-175">Creare un nuovo esperimento.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-175">Create a new experiment.</span></span>
2. <span data-ttu-id="aa4f3-176">Inserire un modulo **Adult Census Income Binary Classification dataset** .</span><span class="sxs-lookup"><span data-stu-id="aa4f3-176">Insert an **Adult Census Income Binary Classification dataset** module.</span></span>
3. <span data-ttu-id="aa4f3-177">Inserire un modulo [Split][split] e connetterne l'input all'output del modulo del set di dati.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-177">Insert a [Split][split] module, and connect its input to the dataset module output.</span></span>
4. <span data-ttu-id="aa4f3-178">Inserire un modulo [Convert to CSV][convert-to-csv] (Converti in CSV) e connetterne l'input a uno degli output del modulo [Split][split] (Dividi).</span><span class="sxs-lookup"><span data-stu-id="aa4f3-178">Insert a [Convert to CSV][convert-to-csv] module and connect its input to one of the [Split][split] module outputs.</span></span>
5. <span data-ttu-id="aa4f3-179">Salvare l'esperimento, eseguirlo e attendere il completamento dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-179">Save the experiment, run it, and wait for it to finish running.</span></span>
6. <span data-ttu-id="aa4f3-180">Fare clic sul nodo di output del modulo [Convert to CSV][convert-to-csv] (Converti in CSV).</span><span class="sxs-lookup"><span data-stu-id="aa4f3-180">Click the output node on the [Convert to CSV][convert-to-csv] module.</span></span>
7. <span data-ttu-id="aa4f3-181">Nel menu di scelta rapida visualizzato selezionare **Generate Data Access Code** (Genera codice di accesso ai dati).</span><span class="sxs-lookup"><span data-stu-id="aa4f3-181">When the context menu appears, select **Generate Data Access Code**.</span></span>
   
    ![Menu di scelta rapida][experiment]
8. <span data-ttu-id="aa4f3-183">Selezionare il frammento di codice dalla finestra che viene visualizzata e copiarlo negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-183">Select the code snippet and copy it to your clipboard from the window that appears.</span></span>
   
    ![Codice di accesso][intermediate-dataset-access-code]
9. <span data-ttu-id="aa4f3-185">Incollare il codice nel blocco appunti.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-185">Paste the code in your notebook.</span></span>
   
    ![Blocco appunti][ipython-intermediate-dataset]
10. <span data-ttu-id="aa4f3-187">È possibile visualizzare i dati usando matplotlib.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-187">You can visualize the data using matplotlib.</span></span> <span data-ttu-id="aa4f3-188">In questo caso, viene creato un istogramma per la colonna dell'età.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-188">This displays in a histogram for the age column:</span></span>
    
    ![Istogramma][ipython-histogram]

## <span data-ttu-id="aa4f3-190"><a name="clientApis"></a>Usare la libreria client Python di Machine Learning per accedere, leggere, creare e gestire set di dati</span><span class="sxs-lookup"><span data-stu-id="aa4f3-190"><a name="clientApis"></a>Use the Machine Learning Python client library to access, read, create, and manage datasets</span></span>
### <a name="workspace"></a><span data-ttu-id="aa4f3-191">Area di lavoro</span><span class="sxs-lookup"><span data-stu-id="aa4f3-191">Workspace</span></span>
<span data-ttu-id="aa4f3-192">L'area di lavoro è il punto di ingresso della libreria client Python.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-192">The workspace is the entry point for the Python client library.</span></span> <span data-ttu-id="aa4f3-193">Per creare un'istanza è necessario specificare nella classe `Workspace` l'ID della propria area di lavoro e il token di autorizzazione:</span><span class="sxs-lookup"><span data-stu-id="aa4f3-193">Provide the `Workspace` class with your workspace id and authorization token to create an instance:</span></span>

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a><span data-ttu-id="aa4f3-194">Enumerare set di dati</span><span class="sxs-lookup"><span data-stu-id="aa4f3-194">Enumerate datasets</span></span>
<span data-ttu-id="aa4f3-195">Per enumerare tutti i set di dati presenti in un'area di lavoro:</span><span class="sxs-lookup"><span data-stu-id="aa4f3-195">To enumerate all datasets in a given workspace:</span></span>

    for ds in ws.datasets:
        print(ds.name)

<span data-ttu-id="aa4f3-196">Per enumerare solo i set di dati creati dall'utente:</span><span class="sxs-lookup"><span data-stu-id="aa4f3-196">To enumerate just the user-created datasets:</span></span>

    for ds in ws.user_datasets:
        print(ds.name)

<span data-ttu-id="aa4f3-197">Per enumerare solo i set di dati di esempio:</span><span class="sxs-lookup"><span data-stu-id="aa4f3-197">To enumerate just the example datasets:</span></span>

    for ds in ws.example_datasets:
        print(ds.name)

<span data-ttu-id="aa4f3-198">È possibile accedere a un set di dati per nome (si applica la distinzione maiuscole/minuscole):</span><span class="sxs-lookup"><span data-stu-id="aa4f3-198">You can access a dataset by name (which is case-sensitive):</span></span>

    ds = ws.datasets['my dataset name']

<span data-ttu-id="aa4f3-199">In alternativa, è possibile accedere tramite indice:</span><span class="sxs-lookup"><span data-stu-id="aa4f3-199">Or you can access it by index:</span></span>

    ds = ws.datasets[0]


### <a name="metadata"></a><span data-ttu-id="aa4f3-200">Metadata</span><span class="sxs-lookup"><span data-stu-id="aa4f3-200">Metadata</span></span>
<span data-ttu-id="aa4f3-201">I set di dati sono composti non solo dal contenuto ma anche da metadati</span><span class="sxs-lookup"><span data-stu-id="aa4f3-201">Datasets have metadata, in addition to content.</span></span> <span data-ttu-id="aa4f3-202">(i set di dati intermedi rappresentano un'eccezione a questa regola poiché non contengono metadati).</span><span class="sxs-lookup"><span data-stu-id="aa4f3-202">(Intermediate datasets are an exception to this rule and do not have any metadata.)</span></span>

<span data-ttu-id="aa4f3-203">Alcuni valori di metadati vengono assegnati dall'utente in fase di creazione:</span><span class="sxs-lookup"><span data-stu-id="aa4f3-203">Some metadata values are assigned by the user at creation time:</span></span>

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

<span data-ttu-id="aa4f3-204">Altri valori vengono assegnati da Azure Machine Learning:</span><span class="sxs-lookup"><span data-stu-id="aa4f3-204">Others are values assigned by Azure ML:</span></span>

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

<span data-ttu-id="aa4f3-205">Vedere la classe `SourceDataset` per altre informazioni sui metadati disponibili.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-205">See the `SourceDataset` class for more on the available metadata.</span></span>

### <a name="read-contents"></a><span data-ttu-id="aa4f3-206">Leggere il contenuto</span><span class="sxs-lookup"><span data-stu-id="aa4f3-206">Read contents</span></span>
<span data-ttu-id="aa4f3-207">I frammenti di codice forniti da Machine Learning Studio scaricano e deserializzano automaticamente il set di dati in un oggetto Pandas DataFrame.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-207">The code snippets provided by Machine Learning Studio automatically download and deserialize the dataset to a Pandas DataFrame object.</span></span> <span data-ttu-id="aa4f3-208">Questa operazione viene eseguita con il metodo `to_dataframe` :</span><span class="sxs-lookup"><span data-stu-id="aa4f3-208">This is done with the `to_dataframe` method:</span></span>

    frame = ds.to_dataframe()

<span data-ttu-id="aa4f3-209">Se lo si preferisce, è possibile scaricare i dati non elaborati ed eseguire la deserializzazione manualmente.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-209">If you prefer to download the raw data, and perform the deserialization yourself, that is an option.</span></span> <span data-ttu-id="aa4f3-210">Questa è l'unica alternativa per i formati come "ARFF" che la libreria client Python non è attualmente in grado di deserializzare.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-210">At the moment, this is the only option for formats such as 'ARFF', which the Python client library cannot deserialize.</span></span>

<span data-ttu-id="aa4f3-211">Per leggere il contenuto come file di testo:</span><span class="sxs-lookup"><span data-stu-id="aa4f3-211">To read the contents as text:</span></span>

    text_data = ds.read_as_text()

<span data-ttu-id="aa4f3-212">Per leggere il contenuto come file binario:</span><span class="sxs-lookup"><span data-stu-id="aa4f3-212">To read the contents as binary:</span></span>

    binary_data = ds.read_as_binary()

<span data-ttu-id="aa4f3-213">È anche possibile aprire un flusso nel contenuto:</span><span class="sxs-lookup"><span data-stu-id="aa4f3-213">You can also just open a stream to the contents:</span></span>

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a><span data-ttu-id="aa4f3-214">Creare un nuovo set di dati</span><span class="sxs-lookup"><span data-stu-id="aa4f3-214">Create a new dataset</span></span>
<span data-ttu-id="aa4f3-215">La libreria client Python consente di caricare set di dati dal programma Python,</span><span class="sxs-lookup"><span data-stu-id="aa4f3-215">The Python client library allows you to upload datasets from your Python program.</span></span> <span data-ttu-id="aa4f3-216">per poterli usare nell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-216">These datasets are then available for use in your workspace.</span></span>

<span data-ttu-id="aa4f3-217">Se i dati sono contenuti in un oggetto DataFrame Pandas, usare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="aa4f3-217">If you have your data in a Pandas DataFrame, use the following code:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="aa4f3-218">Se invece i dati sono già serializzati, è possibile usare:</span><span class="sxs-lookup"><span data-stu-id="aa4f3-218">If your data is already serialized, you can use:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="aa4f3-219">La libreria client Python è in grado di serializzare un oggetto DataFrame Pandas nei formati seguenti (le costanti per questi formati sono disponibili nella classe `azureml.DataTypeIds` ):</span><span class="sxs-lookup"><span data-stu-id="aa4f3-219">The Python client library is able to serialize a Pandas DataFrame to the following formats (constants for these are in the `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="aa4f3-220">PlainText</span><span class="sxs-lookup"><span data-stu-id="aa4f3-220">PlainText</span></span>
* <span data-ttu-id="aa4f3-221">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="aa4f3-221">GenericCSV</span></span>
* <span data-ttu-id="aa4f3-222">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="aa4f3-222">GenericTSV</span></span>
* <span data-ttu-id="aa4f3-223">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="aa4f3-223">GenericCSVNoHeader</span></span>
* <span data-ttu-id="aa4f3-224">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="aa4f3-224">GenericTSVNoHeader</span></span>

### <a name="update-an-existing-dataset"></a><span data-ttu-id="aa4f3-225">Aggiornare un set di dati esistente</span><span class="sxs-lookup"><span data-stu-id="aa4f3-225">Update an existing dataset</span></span>
<span data-ttu-id="aa4f3-226">Se si tenta di caricare un nuovo set di dati con un nome corrispondente a un set di dati esistente, si potrebbe ottiene un errore di conflitto.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-226">If you try to upload a new dataset with a name that matches an existing dataset, you should get a conflict error.</span></span>

<span data-ttu-id="aa4f3-227">Per aggiornare un set di dati esistente, è necessario prima ottenere un riferimento a tale set di dati:</span><span class="sxs-lookup"><span data-stu-id="aa4f3-227">To update an existing dataset, you first need to get a reference to the existing dataset:</span></span>

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="aa4f3-228">Quindi, è necessario usare `update_from_dataframe` per serializzare e sostituire il contenuto del set di dati in Azure:</span><span class="sxs-lookup"><span data-stu-id="aa4f3-228">Then use `update_from_dataframe` to serialize and replace the contents of the dataset on Azure:</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="aa4f3-229">Se si desidera serializzare i dati in un formato diverso, specificare un valore per il parametro `data_type_id` facoltativo.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-229">If you want to serialize the data to a different format, specify a value for the optional `data_type_id` parameter.</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="aa4f3-230">È possibile anche impostare una nuova descrizione specificando un valore per il parametro `description` .</span><span class="sxs-lookup"><span data-stu-id="aa4f3-230">You can optionally set a new description by specifying a value for the `description` parameter.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up to feb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to feb 2015'

<span data-ttu-id="aa4f3-231">È possibile anche impostare un nuovo nome specificando un valore per il parametro `name` .</span><span class="sxs-lookup"><span data-stu-id="aa4f3-231">You can optionally set a new name by specifying a value for the `name` parameter.</span></span> <span data-ttu-id="aa4f3-232">D'ora in poi sarà possibile recuperare il set di dati usando solo il nuovo nome.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-232">From now on, you'll retrieve the dataset using the new name only.</span></span> <span data-ttu-id="aa4f3-233">Il codice seguente consente di aggiornare i dati, il nome e la descrizione.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-233">The following code updates the data, name and description.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up to feb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up to feb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

<span data-ttu-id="aa4f3-234">I parametri `data_type_id`, `name` e `description` sono facoltativi e, per impostazione predefinita, vengono ripristinati ai valori precedenti.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-234">The `data_type_id`, `name` and `description` parameters are optional and default to their previous value.</span></span> <span data-ttu-id="aa4f3-235">Il parametro `dataframe` è sempre obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-235">The `dataframe` parameter is always required.</span></span>

<span data-ttu-id="aa4f3-236">Se i dati sono già serializzati, usare `update_from_raw_data` anziché `update_from_dataframe`.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-236">If your data is already serialized, use `update_from_raw_data` instead of `update_from_dataframe`.</span></span> <span data-ttu-id="aa4f3-237">Il funzionamento è analogo: è sufficiente passare `raw_data` invece di `dataframe`.</span><span class="sxs-lookup"><span data-stu-id="aa4f3-237">If you just pass in `raw_data` instead of  `dataframe`, it works in a similar way.</span></span>

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

