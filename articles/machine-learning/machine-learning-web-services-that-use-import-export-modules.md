---
title: Utilizzo di Import Data ed Export Data nei servizi Web Azure Machine Learning | Documentazione Microsoft
description: Informazioni su come usare i moduli Import Data ed Export Data per inviare e ricevere dati da un servizio Web.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3a7ac351-ebd3-43a1-8c5d-18223903d08e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 123c8c2b1c5bae268b2a61c185743f2c3920175e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a><span data-ttu-id="bc1af-103">Distribuzione di servizi di Web Azure ML che usano i moduli Import Data ed Export Data</span><span class="sxs-lookup"><span data-stu-id="bc1af-103">Deploying Azure ML web services that use Data Import and Data Export modules</span></span>

<span data-ttu-id="bc1af-104">Quando si crea un esperimento predittivo, si aggiunge in genere un input e un output del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="bc1af-104">When you create a predictive experiment, you typically add a web service input and output.</span></span> <span data-ttu-id="bc1af-105">Quando si distribuisce l'esperimento, i consumer possono inviare e ricevere dati dal servizio Web tramite gli input e gli output.</span><span class="sxs-lookup"><span data-stu-id="bc1af-105">When you deploy the experiment, consumers can send and receive data from the web service through the inputs and outputs.</span></span> <span data-ttu-id="bc1af-106">Per alcune applicazioni, i dati del consumer possono essere disponibili da un feed di dati o risiedere già in un'origine dati esterna, ad esempio archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="bc1af-106">For some applications, a consumer's data may be available from a data feed or already reside in an external data source such as Azure Blob storage.</span></span> <span data-ttu-id="bc1af-107">In questi casi non è necessario leggere e scrivere dati usando gli input e gli output del servizio Web .</span><span class="sxs-lookup"><span data-stu-id="bc1af-107">In these cases, they do not need read and write data using web service inputs and outputs.</span></span> <span data-ttu-id="bc1af-108">Gli utenti possono invece usare il servizio di esecuzione batch (BES) per leggere i dati dall'origine dati mediante un modulo Import Data e scrivere i risultati di assegnazione dei punteggi in una posizione dati diversa mediante un modulo Export Data.</span><span class="sxs-lookup"><span data-stu-id="bc1af-108">They can, instead, use the Batch Execution Service (BES) to read data from the data source using an Import Data module and write the scoring results to a different data location using an Export Data module.</span></span>

<span data-ttu-id="bc1af-109">I moduli Import Data ed Export Data possono leggere e scrivere in numerose posizioni, ad esempio un URL Web tramite HTTP, una query Hive, un database SQL di Azure, l'archiviazione tabelle di Azure, l'Archiviazione BLOB di Azure, un provider di feed di dati o un database SQL locale.</span><span class="sxs-lookup"><span data-stu-id="bc1af-109">The Import Data and Export data modules, can read from and write to various data locations such as a Web URL via HTTP, a Hive Query, an Azure SQL database, Azure Table storage, Azure Blob storage, a Data Feed provide, or an on-premises SQL database.</span></span>

<span data-ttu-id="bc1af-110">Questo argomento usa l'esempio "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" e presuppone che il set di dati sia già stato caricato nella tabella SQL di Azure denominata censusdata.</span><span class="sxs-lookup"><span data-stu-id="bc1af-110">This topic uses the "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample and assumes the dataset has already been loaded into an Azure SQL table named censusdata.</span></span>

## <a name="create-the-training-experiment"></a><span data-ttu-id="bc1af-111">Creare l'esperimento di training</span><span class="sxs-lookup"><span data-stu-id="bc1af-111">Create the training experiment</span></span>
<span data-ttu-id="bc1af-112">Quando si apre l'esempio "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset", si usa il set di dati Adult Census Income Binary Classification di esempio.</span><span class="sxs-lookup"><span data-stu-id="bc1af-112">When you open the "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample it uses the sample Adult Census Income Binary Classification dataset.</span></span> <span data-ttu-id="bc1af-113">L'esperimento nell'area di disegno sarà simile all'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="bc1af-113">And the experiment in the canvas will look similar to the following image:</span></span>

![Configurazione iniziale dell'esperimento.](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

<span data-ttu-id="bc1af-115">Per leggere i dati dalla tabella SQL di Azure:</span><span class="sxs-lookup"><span data-stu-id="bc1af-115">To read the data from the Azure SQL table:</span></span>

1. <span data-ttu-id="bc1af-116">Eliminare il modulo del set di dati.</span><span class="sxs-lookup"><span data-stu-id="bc1af-116">Delete the dataset module.</span></span>
2. <span data-ttu-id="bc1af-117">Digitare import nella casella di ricerca dei componenti.</span><span class="sxs-lookup"><span data-stu-id="bc1af-117">In the components search box, type import.</span></span>
3. <span data-ttu-id="bc1af-118">Nell'elenco dei risultati aggiungere un modulo *Import data* nell'area di disegno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="bc1af-118">From the results list, add an *Import Data* module to the experiment canvas.</span></span>
4. <span data-ttu-id="bc1af-119">Connettere l'output del modulo *Import Data* (Importa dati) e l'input del modulo *Clean Missing Data* (Pulisci dati mancanti).</span><span class="sxs-lookup"><span data-stu-id="bc1af-119">Connect output of the *Import Data* module the input of the *Clean Missing Data* module.</span></span>
5. <span data-ttu-id="bc1af-120">Nel riquadro delle proprietà selezionare **Azure SQL Database** in the **Data Source** (Origine dati).</span><span class="sxs-lookup"><span data-stu-id="bc1af-120">In properties pane, select **Azure SQL Database** in the **Data Source** dropdown.</span></span>
6. <span data-ttu-id="bc1af-121">Immettere le informazioni appropriate per il database nei campi **Database server name** (Nome server database), **Database name** (Nome database), **User name** (Nome utente) e **Password**.</span><span class="sxs-lookup"><span data-stu-id="bc1af-121">In the **Database server name**, **Database name**, **User name**, and **Password** fields, enter the appropriate information for your database.</span></span>
7. <span data-ttu-id="bc1af-122">Immettere la query seguente nel campo Database query (Query database).</span><span class="sxs-lookup"><span data-stu-id="bc1af-122">In the Database query field, enter the following query.</span></span>
   
     <span data-ttu-id="bc1af-123">select [age],</span><span class="sxs-lookup"><span data-stu-id="bc1af-123">select [age],</span></span>
   
        [workclass],
        [fnlwgt],
        [education],
        [education-num],
        [marital-status],
        [occupation],
        [relationship],
        [race],
        [sex],
        [capital-gain],
        [capital-loss],
        [hours-per-week],
        [native-country],
        [income]
     <span data-ttu-id="bc1af-124">from dbo.censusdata;</span><span class="sxs-lookup"><span data-stu-id="bc1af-124">from dbo.censusdata;</span></span>
8. <span data-ttu-id="bc1af-125">Fare clic su **Run**(Esegui) nella parte inferiore dell'area di disegno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="bc1af-125">At the bottom of the experiment canvas, click **Run**.</span></span>

## <a name="create-the-predictive-experiment"></a><span data-ttu-id="bc1af-126">Creare l'esperimento predittivo</span><span class="sxs-lookup"><span data-stu-id="bc1af-126">Create the predictive experiment</span></span>
<span data-ttu-id="bc1af-127">Configurare quindi l'esperimento predittivo da cui distribuire il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="bc1af-127">Next you set up the predictive experiment from which you deploy your web service.</span></span>

1. <span data-ttu-id="bc1af-128">Nella parte inferiore dell'area di disegno dell'esperimento fare clic su **Set Up Web Service** (Configura servizio Web) e selezionare **Predictive Web Service [Recommended]** (Servizio Web predittivo - Scelta consigliata).</span><span class="sxs-lookup"><span data-stu-id="bc1af-128">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Predictive Web Service [Recommended]**.</span></span>
2. <span data-ttu-id="bc1af-129">Rimuovere i moduli *Web Service Input* e *Web Service Output modules* dall'esperimento predittivo.</span><span class="sxs-lookup"><span data-stu-id="bc1af-129">Remove the *Web Service Input* and *Web Service Output modules* from the predictive experiment.</span></span> 
3. <span data-ttu-id="bc1af-130">Digitare export nella casella di ricerca di componenti.</span><span class="sxs-lookup"><span data-stu-id="bc1af-130">In the components search box, type export.</span></span>
4. <span data-ttu-id="bc1af-131">Nell'elenco dei risultati aggiungere un modulo *Export Data* nell'area di disegno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="bc1af-131">From the results list, add an *Export Data* module to the experiment canvas.</span></span>
5. <span data-ttu-id="bc1af-132">Connettere l'output del modulo *Score Model* (Modello di punteggio) e l'input del modulo *Export Data* (Esporta dati).</span><span class="sxs-lookup"><span data-stu-id="bc1af-132">Connect output of the *Score Model* module the input of the *Export Data* module.</span></span> 
6. <span data-ttu-id="bc1af-133">Nel riquadro delle proprietà selezionare **Azure SQL Database** (Database SQL Azure) come destinazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="bc1af-133">In properties pane, select **Azure SQL Database** in the data destination dropdown.</span></span>
7. <span data-ttu-id="bc1af-134">Immettere le informazioni appropriate per il database nei campi **Database server name** (Nome server database), **Database name** (Nome database), **Server user account name** (Nome account utente server) e **Server user account password** (Password account utente server).</span><span class="sxs-lookup"><span data-stu-id="bc1af-134">In the **Database server name**, **Database name**, **Server user account name**, and **Server user account password** fields, enter the appropriate information for your database.</span></span>
8. <span data-ttu-id="bc1af-135">Nel campo **Comma separated list of columns to be saved** (Elenco di colonne da salvare delimitato da virgole) digitare Scored Labels.</span><span class="sxs-lookup"><span data-stu-id="bc1af-135">In the **Comma separated list of columns to be saved** field, type Scored Labels.</span></span>
9. <span data-ttu-id="bc1af-136">Nel campo **Data table name**(Nome tabella dati) digitare dbo.ScoredLabels.</span><span class="sxs-lookup"><span data-stu-id="bc1af-136">In the **Data table name field**, type dbo.ScoredLabels.</span></span> <span data-ttu-id="bc1af-137">Se non esiste, la tabella viene creata quando viene eseguito l'esperimento o viene chiamato il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="bc1af-137">If the table does not exist, it is created when the experiment is run or the web service is called.</span></span>
10. <span data-ttu-id="bc1af-138">Nel campo **Comma separated list of datatable columns** (Elenco di colonne di tabella di database delimitato da virgole) digitare ScoredLabels.</span><span class="sxs-lookup"><span data-stu-id="bc1af-138">In the **Comma separated list of datatable columns** field, type ScoredLabels.</span></span>

<span data-ttu-id="bc1af-139">Quando si scrive un'applicazione che chiama il servizio Web finale, è possibile specificare una tabella di destinazione o una query di input diversa in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="bc1af-139">When you write an application that calls the final web service, you may want to specify a different input query or destination table at run time.</span></span> <span data-ttu-id="bc1af-140">Per configurare questi input e output, usare la funzionalità Web Service Parameters (Parametri del servizio Web) per impostare la proprietà *Data source* (Origine dati) del modulo *Import Data* (Importa dati) e la proprietà di destinazione dei dati del modulo *Export Data* (Esporta dati).</span><span class="sxs-lookup"><span data-stu-id="bc1af-140">To configure these inputs and outputs, use the Web Service Parameters feature to set the *Import Data* module *Data source* property and the *Export Data* mode data destination property.</span></span>  <span data-ttu-id="bc1af-141">Per altre informazioni sui parametri del servizio Web, vedere [AzureML Web Service Parameters](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) su Cortana Intelligence and Machine Learning Blog.</span><span class="sxs-lookup"><span data-stu-id="bc1af-141">For more information on Web Service Parameters, see the [AzureML Web Service Parameters entry](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) on the Cortana Intelligence and Machine Learning Blog.</span></span>

<span data-ttu-id="bc1af-142">Per configurare i parametri del servizio Web per la query di importazione e la tabella di destinazione:</span><span class="sxs-lookup"><span data-stu-id="bc1af-142">To configure the Web Service Parameters for the import query and the destination table:</span></span>

1. <span data-ttu-id="bc1af-143">Nel riquadro delle proprietà per il modulo *Import Data* (Importa dati) fare clic sull'icona nella parte superiore destra del campo **Database query** (Query database) e selezionare **Set as web service parameter** (Imposta come parametro di servizio Web).</span><span class="sxs-lookup"><span data-stu-id="bc1af-143">In the properties pane for the *Import Data* module, click the icon at the top right of the **Database query** field and select **Set as web service parameter**.</span></span>
2. <span data-ttu-id="bc1af-144">Nel riquadro delle proprietà per il modulo *Export Data* (Esporta dati) fare clic sull'icona nella parte superiore destra del campo **Data table name** (Nome tabella dati) e selezionare **Set as web service parameter** (Imposta come parametro di servizio Web).</span><span class="sxs-lookup"><span data-stu-id="bc1af-144">In the properties pane for the *Export Data* module, click the icon at the top right of the **Data table name** field and select **Set as web service parameter**.</span></span>
3. <span data-ttu-id="bc1af-145">Nella parte inferiore del riquadro delle proprietà del modulo *Export Data* nella sezione **Web Service Parameters** (Parametri del servizio Web), fare clic su Database query (Query database) e rinominare in Query.</span><span class="sxs-lookup"><span data-stu-id="bc1af-145">At the bottom of the *Export Data* module properties pane, in the **Web Service Parameters** section, click Database query and rename it Query.</span></span>
4. <span data-ttu-id="bc1af-146">Fare clic su **Data table name** (Nome tabella dati) e rinominare in **Table** (Tabella).</span><span class="sxs-lookup"><span data-stu-id="bc1af-146">Click **Data table name** and rename it **Table**.</span></span>

<span data-ttu-id="bc1af-147">Al termine l'esperimento dovrebbe essere simile all'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="bc1af-147">When you are done, your experiment should look similar to the following image:</span></span>

![Risultato finale dell'esperimento.](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

<span data-ttu-id="bc1af-149">Ora è possibile distribuire l'esperimento come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="bc1af-149">Now you can deploy the experiment as a web service.</span></span>

## <a name="deploy-the-web-service"></a><span data-ttu-id="bc1af-150">Distribuire il servizio web</span><span class="sxs-lookup"><span data-stu-id="bc1af-150">Deploy the web service</span></span>
<span data-ttu-id="bc1af-151">È possibile eseguire la distribuzione come servizio Web nuovo o classico.</span><span class="sxs-lookup"><span data-stu-id="bc1af-151">You can deploy to either a Classic or New web service.</span></span>

### <a name="deploy-a-classic-web-service"></a><span data-ttu-id="bc1af-152">Distribuire un servizio Web classico</span><span class="sxs-lookup"><span data-stu-id="bc1af-152">Deploy a Classic Web Service</span></span>
<span data-ttu-id="bc1af-153">Per eseguire la distribuzione come servizio Web classico e creare un'applicazione per usare il servizio:</span><span class="sxs-lookup"><span data-stu-id="bc1af-153">To deploy as a Classic Web Service and create an application to consume it:</span></span>

1. <span data-ttu-id="bc1af-154">Nella parte inferiore dell'area di disegno dell'esperimento fare clic su Run (Esegui).</span><span class="sxs-lookup"><span data-stu-id="bc1af-154">At the bottom of the experiment canvas, click Run.</span></span>
2. <span data-ttu-id="bc1af-155">Al termine dell'esecuzione fare clic su **Deploy Web Service** (Distribuisci servizio Web) e selezionare **Deploy Web Service [Classic]** (Distribuisci servizio Web [Classico]).</span><span class="sxs-lookup"><span data-stu-id="bc1af-155">When the run has completed, click **Deploy Web Service** and select **Deploy Web Service [Classic]**.</span></span>
3. <span data-ttu-id="bc1af-156">Nel dashboard del servizio Web individuare la chiave API.</span><span class="sxs-lookup"><span data-stu-id="bc1af-156">On the web service dashboard, locate your API key.</span></span> <span data-ttu-id="bc1af-157">Copiarla e salvarla per usarla in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="bc1af-157">Copy and save it to use later.</span></span>
4. <span data-ttu-id="bc1af-158">Nella tabella **Default Endpoint** (Endpoint predefinito) fare clic sul collegamento **Esecuzione batch** per aprire la pagina della Guida dell'API.</span><span class="sxs-lookup"><span data-stu-id="bc1af-158">In the **Default Endpoint** table, click the **Batch Execution** link to open the API Help Page.</span></span>
5. <span data-ttu-id="bc1af-159">In Visual Studio creare un'applicazione console C#. A tale scopo, selezionare **Nuovo** > **Progetto** > **Visual C#** > **Desktop classico di Windows** > **Applicazione console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="bc1af-159">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
6. <span data-ttu-id="bc1af-160">Nella pagina della Guida di API individuare la sezione **Sample Code** (Codice di esempio) nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="bc1af-160">On the API Help Page, find the **Sample Code** section at the bottom of the page.</span></span>
7. <span data-ttu-id="bc1af-161">Copiare e incollare il codice di esempio in C# nel file Program.cs e rimuovere tutti i riferimenti nell'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="bc1af-161">Copy and paste the C# sample code into your Program.cs file, and remove all references to the blob storage.</span></span>
8. <span data-ttu-id="bc1af-162">Aggiornare il valore della variabile *apiKey* con la chiave API salvata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="bc1af-162">Update the value of the *apiKey* variable with the API key saved earlier.</span></span>
9. <span data-ttu-id="bc1af-163">Individuare la dichiarazione di richiesta e aggiornare i valori del servizio Web passati ai moduli *Import Data* (Importa dati) e *Export Data* (Esporta dati).</span><span class="sxs-lookup"><span data-stu-id="bc1af-163">Locate the request declaration and update the values of Web Service Parameters that are passed to the *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="bc1af-164">In questo caso, usare la query originale, ma definire un nome per la nuova tabella.</span><span class="sxs-lookup"><span data-stu-id="bc1af-164">In this case, you use the original query, but define a new table name.</span></span>
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. <span data-ttu-id="bc1af-165">Eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bc1af-165">Run the application.</span></span> 

<span data-ttu-id="bc1af-166">Al termine dell'esecuzione verrà aggiunta una nuova tabella al database contenente i risultati di punteggio.</span><span class="sxs-lookup"><span data-stu-id="bc1af-166">On completion of the run, a new table is added to the database containing the scoring results.</span></span>

### <a name="deploy-a-new-web-service"></a><span data-ttu-id="bc1af-167">Distribuire un servizio Web nuovo</span><span class="sxs-lookup"><span data-stu-id="bc1af-167">Deploy a New Web Service</span></span>

> [!NOTE] 
> <span data-ttu-id="bc1af-168">Per distribuire un nuovo servizio Web è necessario disporre delle autorizzazioni sufficienti nella sottoscrizione a cui si sta distribuendo il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="bc1af-168">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="bc1af-169">Per altre informazioni, vedere [Gestire un servizio Web usando il portale dei servizi Web di Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="bc1af-169">For more information, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="bc1af-170">Per eseguire la distribuzione come servizio Web nuovo e creare un'applicazione per usare il servizio:</span><span class="sxs-lookup"><span data-stu-id="bc1af-170">To deploy as a New Web Service and create an application to consume it:</span></span>

1. <span data-ttu-id="bc1af-171">Fare clic su **Run**(Esegui) nella parte inferiore dell'area di disegno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="bc1af-171">At the bottom of the experiment canvas, click **Run**.</span></span>
2. <span data-ttu-id="bc1af-172">Al termine dell'esecuzione fare clic su **Deploy Web Service** (Distribuisci servizio Web) e selezionare **Deploy Web Service [New]** (Distribuisci servizio Web [Nuovo]).</span><span class="sxs-lookup"><span data-stu-id="bc1af-172">When the run has completed, click **Deploy Web Service** and select **Deploy Web Service [New]**.</span></span>
3. <span data-ttu-id="bc1af-173">Nella pagina Deploy Experiment (Sperimentazione distribuzione) immettere un nome per il servizio Web e selezionare un piano tariffario, quindi fare clic su **Deploy**(Distribuzione).</span><span class="sxs-lookup"><span data-stu-id="bc1af-173">On the Deploy Experiment page, enter a name for your web service, and select a pricing plan, then click **Deploy**.</span></span>
4. <span data-ttu-id="bc1af-174">Nella pagina **Quickstart** (Avvio rapido) fare clic su **Consume** (Utilizzo).</span><span class="sxs-lookup"><span data-stu-id="bc1af-174">On the **Quickstart** page, click **Consume**.</span></span>
5. <span data-ttu-id="bc1af-175">Nella sezione **Sample Code** (Codice di esempio) fare clic su **Batch**.</span><span class="sxs-lookup"><span data-stu-id="bc1af-175">In the **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="bc1af-176">In Visual Studio creare un'applicazione console C#. A tale scopo, selezionare **Nuovo** > **Progetto** > **Visual C#** > **Desktop classico di Windows** > **Applicazione console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="bc1af-176">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
7. <span data-ttu-id="bc1af-177">Copiare e incollare il codice di esempio in C# nel file Program.cs.</span><span class="sxs-lookup"><span data-stu-id="bc1af-177">Copy and paste the C# sample code into your Program.cs file.</span></span>
8. <span data-ttu-id="bc1af-178">Aggiornare il valore della variabile *apiKey* con la **chiave primaria** presente nella sezione **Basic consumption info** (Informazioni di base sul consumo).</span><span class="sxs-lookup"><span data-stu-id="bc1af-178">Update the value of the *apiKey* variable with the **Primary Key** located in the **Basic consumption info** section.</span></span>
9. <span data-ttu-id="bc1af-179">Individuare la dichiarazione *scoreRequest* e aggiornare i valori dei parametri del servizio Web passati ai moduli *Import Data* (Importa dati) e *Export Data* (Esporta dati).</span><span class="sxs-lookup"><span data-stu-id="bc1af-179">Locate the *scoreRequest* declaration and update the values of Web Service Parameters that are passed to the *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="bc1af-180">In questo caso, usare la query originale, ma definire un nome per la nuova tabella.</span><span class="sxs-lookup"><span data-stu-id="bc1af-180">In this case, you use the original query, but define a new table name.</span></span>
   
        var scoreRequest = new
        {       
            Inputs = new Dictionary<string, StringTable>()
            {
            },
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable3" },
            }
        };
10. <span data-ttu-id="bc1af-181">Eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bc1af-181">Run the application.</span></span> 

