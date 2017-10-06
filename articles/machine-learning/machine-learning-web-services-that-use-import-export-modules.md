---
title: aaaUsing importazione/esportazione di dati nei servizi web di Azure Machine Learning | Documenti Microsoft
description: Informazioni su come toouse hello toosend moduli dati di importazione ed esportazione di dati e ricevere dati da un servizio web.
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
ms.openlocfilehash: 176380259b15cb338ede61c7f28ba2296b35dd52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a><span data-ttu-id="2e5a6-103">Distribuzione di servizi di Web Azure ML che usano i moduli Import Data ed Export Data</span><span class="sxs-lookup"><span data-stu-id="2e5a6-103">Deploying Azure ML web services that use Data Import and Data Export modules</span></span>

<span data-ttu-id="2e5a6-104">Quando si crea un esperimento predittivo, si aggiunge in genere un input e un output del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-104">When you create a predictive experiment, you typically add a web service input and output.</span></span> <span data-ttu-id="2e5a6-105">Quando si distribuisce l'esperimento hello, i consumer possono inviare e ricevere dati dal servizio web hello tramite hello input e output.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-105">When you deploy hello experiment, consumers can send and receive data from hello web service through hello inputs and outputs.</span></span> <span data-ttu-id="2e5a6-106">Per alcune applicazioni, i dati del consumer possono essere disponibili da un feed di dati o risiedere già in un'origine dati esterna, ad esempio archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-106">For some applications, a consumer's data may be available from a data feed or already reside in an external data source such as Azure Blob storage.</span></span> <span data-ttu-id="2e5a6-107">In questi casi non è necessario leggere e scrivere dati usando gli input e gli output del servizio Web .</span><span class="sxs-lookup"><span data-stu-id="2e5a6-107">In these cases, they do not need read and write data using web service inputs and outputs.</span></span> <span data-ttu-id="2e5a6-108">Possono, in alternativa, utilizzare dati tooread di hello servizio esecuzione Batch (BES) dall'origine dati hello mediante un modulo di importazione dei dati e scrivere hello punteggio percorso dati diversi tooa mediante un modulo di esportare dati di risultati.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-108">They can, instead, use hello Batch Execution Service (BES) tooread data from hello data source using an Import Data module and write hello scoring results tooa different data location using an Export Data module.</span></span>

<span data-ttu-id="2e5a6-109">Hello l'importazione dei dati e i moduli di dati di esportazione, possono leggere e scrivere dati toovarious forniscono percorsi, ad esempio un URL Web tramite HTTP, una Query Hive, un database SQL di Azure, archiviazione tabelle di Azure, archiviazione Blob di Azure, un Feed di dati o un database SQL locale.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-109">hello Import Data and Export data modules, can read from and write toovarious data locations such as a Web URL via HTTP, a Hive Query, an Azure SQL database, Azure Table storage, Azure Blob storage, a Data Feed provide, or an on-premises SQL database.</span></span>

<span data-ttu-id="2e5a6-110">In questo argomento utilizza hello "esempio 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" di esempio e presuppone che il dataset hello è già stato caricato in una tabella di SQL Azure denominata censusdata.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-110">This topic uses hello "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample and assumes hello dataset has already been loaded into an Azure SQL table named censusdata.</span></span>

## <a name="create-hello-training-experiment"></a><span data-ttu-id="2e5a6-111">Creare l'esperimento di training hello</span><span class="sxs-lookup"><span data-stu-id="2e5a6-111">Create hello training experiment</span></span>
<span data-ttu-id="2e5a6-112">Quando si apre hello "esempio 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" esempio di set di dati utilizza hello campione la classificazione binaria per adulti Census reddito.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-112">When you open hello "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample it uses hello sample Adult Census Income Binary Classification dataset.</span></span> <span data-ttu-id="2e5a6-113">Ed esperimento hello nell'area di disegno hello avrà un aspetto simile toohello seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="2e5a6-113">And hello experiment in hello canvas will look similar toohello following image:</span></span>

![Configurazione iniziale di sperimentazione hello.](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

<span data-ttu-id="2e5a6-115">dati di hello tooread dalla tabella di SQL Azure hello:</span><span class="sxs-lookup"><span data-stu-id="2e5a6-115">tooread hello data from hello Azure SQL table:</span></span>

1. <span data-ttu-id="2e5a6-116">Eliminare il modulo di hello set di dati.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-116">Delete hello dataset module.</span></span>
2. <span data-ttu-id="2e5a6-117">Nella casella di ricerca di componenti hello, tipo di importazione.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-117">In hello components search box, type import.</span></span>
3. <span data-ttu-id="2e5a6-118">Dall'elenco dei risultati di hello, aggiungere un *l'importazione dei dati* toohello modulo provare l'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-118">From hello results list, add an *Import Data* module toohello experiment canvas.</span></span>
4. <span data-ttu-id="2e5a6-119">Connettere l'output di hello *l'importazione dei dati* input hello modulo di hello *Clean Missing Data* modulo.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-119">Connect output of hello *Import Data* module hello input of hello *Clean Missing Data* module.</span></span>
5. <span data-ttu-id="2e5a6-120">Nel riquadro Proprietà selezionare **Database SQL di Azure** in hello **origine dati** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-120">In properties pane, select **Azure SQL Database** in hello **Data Source** dropdown.</span></span>
6. <span data-ttu-id="2e5a6-121">In hello **nome server Database**, **nome del Database**, **nome utente**, e **Password** campi, immettere le informazioni appropriate per hello il database.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-121">In hello **Database server name**, **Database name**, **User name**, and **Password** fields, enter hello appropriate information for your database.</span></span>
7. <span data-ttu-id="2e5a6-122">Nel campo della query Database hello immettere hello seguente query.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-122">In hello Database query field, enter hello following query.</span></span>
   
     <span data-ttu-id="2e5a6-123">select [age],</span><span class="sxs-lookup"><span data-stu-id="2e5a6-123">select [age],</span></span>
   
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
     <span data-ttu-id="2e5a6-124">from dbo.censusdata;</span><span class="sxs-lookup"><span data-stu-id="2e5a6-124">from dbo.censusdata;</span></span>
8. <span data-ttu-id="2e5a6-125">Nella parte inferiore di hello dell'area di disegno esperimento hello, fare clic su **eseguire**.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-125">At hello bottom of hello experiment canvas, click **Run**.</span></span>

## <a name="create-hello-predictive-experiment"></a><span data-ttu-id="2e5a6-126">Creare l'esperimento predittiva hello</span><span class="sxs-lookup"><span data-stu-id="2e5a6-126">Create hello predictive experiment</span></span>
<span data-ttu-id="2e5a6-127">Successivamente impostare esperimento predittiva di hello da cui si distribuisce il servizio web.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-127">Next you set up hello predictive experiment from which you deploy your web service.</span></span>

1. <span data-ttu-id="2e5a6-128">Nella parte inferiore di hello dell'area di disegno esperimento hello, fare clic su **di servizio Web** e selezionare **predittiva servizio Web (scelta consigliata)**.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-128">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Predictive Web Service [Recommended]**.</span></span>
2. <span data-ttu-id="2e5a6-129">Rimuovere hello *Input del servizio Web* e *moduli di Output del servizio Web* da esperimento predittiva hello.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-129">Remove hello *Web Service Input* and *Web Service Output modules* from hello predictive experiment.</span></span> 
3. <span data-ttu-id="2e5a6-130">Nella casella di ricerca di componenti hello, tipo di esportazione.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-130">In hello components search box, type export.</span></span>
4. <span data-ttu-id="2e5a6-131">Dall'elenco dei risultati di hello, aggiungere un *Esporta dati* toohello modulo provare l'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-131">From hello results list, add an *Export Data* module toohello experiment canvas.</span></span>
5. <span data-ttu-id="2e5a6-132">Connettere l'output di hello *Score Model* input hello modulo di hello *Esporta dati* modulo.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-132">Connect output of hello *Score Model* module hello input of hello *Export Data* module.</span></span> 
6. <span data-ttu-id="2e5a6-133">Nel riquadro Proprietà selezionare **Database SQL di Azure** nell'elenco a discesa destinazione di dati hello.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-133">In properties pane, select **Azure SQL Database** in hello data destination dropdown.</span></span>
7. <span data-ttu-id="2e5a6-134">In hello **nome server Database**, **nome del Database**, **nome dell'account utente Server**, e **password dell'account utente Server** immettere informazioni appropriate Hello per il database.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-134">In hello **Database server name**, **Database name**, **Server user account name**, and **Server user account password** fields, enter hello appropriate information for your database.</span></span>
8. <span data-ttu-id="2e5a6-135">In hello **elenco delimitato da virgole di colonne toobe salvato** digitare Scored Labels.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-135">In hello **Comma separated list of columns toobe saved** field, type Scored Labels.</span></span>
9. <span data-ttu-id="2e5a6-136">In hello **campo Nome tabella di dati**, digitare dbo. ScoredLabels.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-136">In hello **Data table name field**, type dbo.ScoredLabels.</span></span> <span data-ttu-id="2e5a6-137">Se la tabella hello non esiste, viene creato quando viene eseguito l'esperimento hello o servizio web hello viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-137">If hello table does not exist, it is created when hello experiment is run or hello web service is called.</span></span>
10. <span data-ttu-id="2e5a6-138">In hello **elenco delimitato da virgole delle colonne di datatable** campo digitare ScoredLabels.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-138">In hello **Comma separated list of datatable columns** field, type ScoredLabels.</span></span>

<span data-ttu-id="2e5a6-139">Quando si scrive un'applicazione che chiama hello servizio web finale, è opportuno toospecify un'altra tabella di query o di destinazione input in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-139">When you write an application that calls hello final web service, you may want toospecify a different input query or destination table at run time.</span></span> <span data-ttu-id="2e5a6-140">tooconfigure questi input e output, utilizzare hello tooset funzionalità parametri del servizio Web di hello *l'importazione dei dati* modulo *origine dati* proprietà e hello *Esporta dati* modalità proprietà destinazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-140">tooconfigure these inputs and outputs, use hello Web Service Parameters feature tooset hello *Import Data* module *Data source* property and hello *Export Data* mode data destination property.</span></span>  <span data-ttu-id="2e5a6-141">Per ulteriori informazioni sui parametri di servizio Web, vedere hello [voce parametri del servizio Web Azure ml](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) hello Intelligence Cortana e Blog di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-141">For more information on Web Service Parameters, see hello [AzureML Web Service Parameters entry](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) on hello Cortana Intelligence and Machine Learning Blog.</span></span>

<span data-ttu-id="2e5a6-142">per le query di importazione hello e tabella di destinazione hello tooconfigure hello parametri del servizio Web:</span><span class="sxs-lookup"><span data-stu-id="2e5a6-142">tooconfigure hello Web Service Parameters for hello import query and hello destination table:</span></span>

1. <span data-ttu-id="2e5a6-143">Nel riquadro Proprietà hello hello *l'importazione dei dati* modulo, fare clic sull'icona hello hello in alto a destra di hello **query Database** campo e selezionare **come parametro di servizio web**.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-143">In hello properties pane for hello *Import Data* module, click hello icon at hello top right of hello **Database query** field and select **Set as web service parameter**.</span></span>
2. <span data-ttu-id="2e5a6-144">Nel riquadro Proprietà hello hello *Esporta dati* modulo, fare clic sull'icona hello hello in alto a destra di hello **nome della tabella dati** campo e selezionare **come parametro di servizio web**.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-144">In hello properties pane for hello *Export Data* module, click hello icon at hello top right of hello **Data table name** field and select **Set as web service parameter**.</span></span>
3. <span data-ttu-id="2e5a6-145">Nella parte inferiore di hello di hello *Esporta dati* hello riquadro Proprietà modulo **parametri del servizio Web** sezione, fare clic su query di Database e rinominare la cartella Query.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-145">At hello bottom of hello *Export Data* module properties pane, in hello **Web Service Parameters** section, click Database query and rename it Query.</span></span>
4. <span data-ttu-id="2e5a6-146">Fare clic su **Data table name** (Nome tabella dati) e rinominare in **Table** (Tabella).</span><span class="sxs-lookup"><span data-stu-id="2e5a6-146">Click **Data table name** and rename it **Table**.</span></span>

<span data-ttu-id="2e5a6-147">Al termine, l'esperimento dovrebbe essere simile toohello seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="2e5a6-147">When you are done, your experiment should look similar toohello following image:</span></span>

![Risultato finale dell'esperimento.](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

<span data-ttu-id="2e5a6-149">È ora possibile distribuire hello esperimento come servizio web.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-149">Now you can deploy hello experiment as a web service.</span></span>

## <a name="deploy-hello-web-service"></a><span data-ttu-id="2e5a6-150">Distribuzione di servizio web hello</span><span class="sxs-lookup"><span data-stu-id="2e5a6-150">Deploy hello web service</span></span>
<span data-ttu-id="2e5a6-151">È possibile distribuire tooeither un servizio web classica o nuovo.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-151">You can deploy tooeither a Classic or New web service.</span></span>

### <a name="deploy-a-classic-web-service"></a><span data-ttu-id="2e5a6-152">Distribuire un servizio Web classico</span><span class="sxs-lookup"><span data-stu-id="2e5a6-152">Deploy a Classic Web Service</span></span>
<span data-ttu-id="2e5a6-153">toodeploy come servizio Web classico e creare un'applicazione tooconsume è:</span><span class="sxs-lookup"><span data-stu-id="2e5a6-153">toodeploy as a Classic Web Service and create an application tooconsume it:</span></span>

1. <span data-ttu-id="2e5a6-154">Nella parte inferiore di hello dell'area di disegno esperimento hello, fare clic su Esegui.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-154">At hello bottom of hello experiment canvas, click Run.</span></span>
2. <span data-ttu-id="2e5a6-155">Al termine dell'esecuzione hello, fare clic su **distribuzione servizio Web** e selezionare **distribuzione di un servizio Web [classica]**.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-155">When hello run has completed, click **Deploy Web Service** and select **Deploy Web Service [Classic]**.</span></span>
3. <span data-ttu-id="2e5a6-156">Nel dashboard del servizio web hello, individuare la chiave API.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-156">On hello web service dashboard, locate your API key.</span></span> <span data-ttu-id="2e5a6-157">Copiare e salvarlo toouse in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-157">Copy and save it toouse later.</span></span>
4. <span data-ttu-id="2e5a6-158">In hello **Endpoint predefinito** tabella, fare clic su hello **esecuzione Batch** hello tooopen collegamento pagina della Guida di API.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-158">In hello **Default Endpoint** table, click hello **Batch Execution** link tooopen hello API Help Page.</span></span>
5. <span data-ttu-id="2e5a6-159">In Visual Studio creare un'applicazione console C#. A tale scopo, selezionare **Nuovo** > **Progetto** > **Visual C#** > **Desktop classico di Windows** > **Applicazione console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-159">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
6. <span data-ttu-id="2e5a6-160">Nella pagina della Guida API hello, trovare hello **codice di esempio** sezione hello parte inferiore della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-160">On hello API Help Page, find hello **Sample Code** section at hello bottom of hello page.</span></span>
7. <span data-ttu-id="2e5a6-161">Copiare e incollare hello c# il codice di esempio nel file Program.cs e rimuovere tutti gli archivi blob toohello di riferimenti.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-161">Copy and paste hello C# sample code into your Program.cs file, and remove all references toohello blob storage.</span></span>
8. <span data-ttu-id="2e5a6-162">Aggiornare il valore di hello di hello *apiKey* variabile con la chiave API hello salvato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-162">Update hello value of hello *apiKey* variable with hello API key saved earlier.</span></span>
9. <span data-ttu-id="2e5a6-163">Individuare hello richiesta dichiarazione e l'aggiornamento hello valori dei parametri del servizio Web che vengono passati toohello *l'importazione dei dati* e *Esporta dati* moduli.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-163">Locate hello request declaration and update hello values of Web Service Parameters that are passed toohello *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="2e5a6-164">In questo caso, utilizzare la query originale hello ma definire un nuovo nome di tabella.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-164">In this case, you use hello original query, but define a new table name.</span></span>
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. <span data-ttu-id="2e5a6-165">Eseguire un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-165">Run hello application.</span></span> 

<span data-ttu-id="2e5a6-166">Al termine dell'esecuzione di hello, database toohello contenente i risultati di punteggio hello è aggiunto a una nuova tabella.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-166">On completion of hello run, a new table is added toohello database containing hello scoring results.</span></span>

### <a name="deploy-a-new-web-service"></a><span data-ttu-id="2e5a6-167">Distribuire un servizio Web nuovo</span><span class="sxs-lookup"><span data-stu-id="2e5a6-167">Deploy a New Web Service</span></span>

> [!NOTE] 
> <span data-ttu-id="2e5a6-168">un nuovo servizio web deve disporre di autorizzazioni sufficienti in hello toowhich di sottoscrizione per la distribuzione del servizio web hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-168">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="2e5a6-169">Per ulteriori informazioni, vedere [gestire un servizio Web tramite il portale di servizi Web di Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="2e5a6-169">For more information, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="2e5a6-170">toodeploy come un nuovo servizio Web e creare un'applicazione tooconsume è:</span><span class="sxs-lookup"><span data-stu-id="2e5a6-170">toodeploy as a New Web Service and create an application tooconsume it:</span></span>

1. <span data-ttu-id="2e5a6-171">Nella parte inferiore di hello dell'area di disegno esperimento hello, fare clic su **eseguire**.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-171">At hello bottom of hello experiment canvas, click **Run**.</span></span>
2. <span data-ttu-id="2e5a6-172">Al termine dell'esecuzione hello, fare clic su **distribuzione servizio Web** e selezionare **distribuzione servizio Web [New]**.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-172">When hello run has completed, click **Deploy Web Service** and select **Deploy Web Service [New]**.</span></span>
3. <span data-ttu-id="2e5a6-173">Selezionare un piano tariffario, nella pagina di distribuire esperimento hello, immettere un nome per il servizio web, quindi fare clic su **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-173">On hello Deploy Experiment page, enter a name for your web service, and select a pricing plan, then click **Deploy**.</span></span>
4. <span data-ttu-id="2e5a6-174">In hello **delle Guide rapide** pagina, fare clic su **consumare**.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-174">On hello **Quickstart** page, click **Consume**.</span></span>
5. <span data-ttu-id="2e5a6-175">In hello **codice di esempio** fare clic su **Batch**.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-175">In hello **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="2e5a6-176">In Visual Studio creare un'applicazione console C#. A tale scopo, selezionare **Nuovo** > **Progetto** > **Visual C#** > **Desktop classico di Windows** > **Applicazione console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-176">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
7. <span data-ttu-id="2e5a6-177">Copiare e incollare codice di esempio hello c# nel file Program.cs.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-177">Copy and paste hello C# sample code into your Program.cs file.</span></span>
8. <span data-ttu-id="2e5a6-178">Aggiornare il valore di hello di hello *apiKey* variabile con hello **chiave primaria** si trova in hello **informazioni di base al consumo** sezione.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-178">Update hello value of hello *apiKey* variable with hello **Primary Key** located in hello **Basic consumption info** section.</span></span>
9. <span data-ttu-id="2e5a6-179">Individuare hello *scoreRequest* dichiarazione e aggiornare i valori hello dei parametri del servizio Web che vengono passati toohello *l'importazione dei dati* e *Esporta dati* moduli.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-179">Locate hello *scoreRequest* declaration and update hello values of Web Service Parameters that are passed toohello *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="2e5a6-180">In questo caso, utilizzare la query originale hello ma definire un nuovo nome di tabella.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-180">In this case, you use hello original query, but define a new table name.</span></span>
   
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
10. <span data-ttu-id="2e5a6-181">Eseguire un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="2e5a6-181">Run hello application.</span></span> 

