---
title: Ripetere il training di un servizio Web predittivo esistente | Documentazione Microsoft
description: Informazioni su come ripetere il training di un modello e aggiornare il servizio Web per usare il modello appena sottoposto a training in Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: cc4c26a2-5672-4255-a767-cfd971e46775
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-donglo
ms.openlocfilehash: bdc994daf441d397157f8e6cbcf84d72584927f0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a><span data-ttu-id="93a93-103">Ripetere il training di un servizio Web predittivo esistente</span><span class="sxs-lookup"><span data-stu-id="93a93-103">Retrain an existing predictive web service</span></span>
<span data-ttu-id="93a93-104">Questo documento descrive il processo di ripetizione del training nello scenario seguente:</span><span class="sxs-lookup"><span data-stu-id="93a93-104">This document describes the retraining process for the following scenario:</span></span>

* <span data-ttu-id="93a93-105">Si dispone di un esperimento di training e di un esperimento predittivo distribuito come un servizio Web operativo.</span><span class="sxs-lookup"><span data-stu-id="93a93-105">You have a training experiment and a predictive experiment that you have deployed as an operationalized web service.</span></span>
* <span data-ttu-id="93a93-106">Si hanno a disposizione nuovi dati che si vuole vengano usati dal servizio Web predittivo per assegnarne il punteggio.</span><span class="sxs-lookup"><span data-stu-id="93a93-106">You have new data that you want your predictive web service to use to perform its scoring.</span></span>

> [!NOTE] 
> <span data-ttu-id="93a93-107">Per distribuire un nuovo servizio Web è necessario disporre delle autorizzazioni sufficienti nella sottoscrizione a cui si sta distribuendo il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="93a93-107">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="93a93-108">Per altre informazioni, vedere [Gestire un servizio Web usando il portale dei servizi Web di Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="93a93-108">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="93a93-109">Seguire questa procedura usando il servizio Web e gli esperimenti esistenti:</span><span class="sxs-lookup"><span data-stu-id="93a93-109">Starting with your existing web service and experiments, you need to follow these steps:</span></span>

1. <span data-ttu-id="93a93-110">Aggiornare il modello.</span><span class="sxs-lookup"><span data-stu-id="93a93-110">Update the model.</span></span>
   1. <span data-ttu-id="93a93-111">Modificare l'esperimento di training per consentire l'uso di input e output del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="93a93-111">Modify your training experiment to allow for web service inputs and outputs.</span></span>
   2. <span data-ttu-id="93a93-112">Distribuire l'esperimento di training come servizio Web di ripetizione del training.</span><span class="sxs-lookup"><span data-stu-id="93a93-112">Deploy the training experiment as a retraining web service.</span></span>
   3. <span data-ttu-id="93a93-113">Usare il servizio Esecuzione batch dell'esperimento di training per ripetere il training del modello.</span><span class="sxs-lookup"><span data-stu-id="93a93-113">Use the training experiment's Batch Execution Service (BES) to retrain the model.</span></span>
2. <span data-ttu-id="93a93-114">Usare i cmdlet di PowerShell per Azure Machine Learning per aggiornare l'esperimento predittivo.</span><span class="sxs-lookup"><span data-stu-id="93a93-114">Use the Azure Machine Learning PowerShell cmdlets to update the predictive experiment.</span></span>
   1. <span data-ttu-id="93a93-115">Accedere con l'account di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="93a93-115">Sign in to your Azure Resource Manager account.</span></span>
   2. <span data-ttu-id="93a93-116">Ottenere la definizione del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="93a93-116">Get the web service definition.</span></span>
   3. <span data-ttu-id="93a93-117">Esportare la definizione del servizio Web in un file in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="93a93-117">Export the web service definition as JSON.</span></span>
   4. <span data-ttu-id="93a93-118">Aggiornare il riferimento al BLOB ilearner nel file JSON.</span><span class="sxs-lookup"><span data-stu-id="93a93-118">Update the reference to the ilearner blob in the JSON.</span></span>
   5. <span data-ttu-id="93a93-119">Importare il file JSON in una definizione del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="93a93-119">Import the JSON into a web service definition.</span></span>
   6. <span data-ttu-id="93a93-120">Aggiornare il servizio Web con la nuova definizione.</span><span class="sxs-lookup"><span data-stu-id="93a93-120">Update the web service with a new web service definition.</span></span>

## <a name="deploy-the-training-experiment"></a><span data-ttu-id="93a93-121">Distribuire l'esperimento di training</span><span class="sxs-lookup"><span data-stu-id="93a93-121">Deploy the training experiment</span></span>
<span data-ttu-id="93a93-122">Per distribuire l'esperimento di training come servizio Web di ripetizione del training, è necessario aggiungere input e output del servizio Web al modello.</span><span class="sxs-lookup"><span data-stu-id="93a93-122">To deploy the training experiment as a retraining web service, you must add web service inputs and outputs to the model.</span></span> <span data-ttu-id="93a93-123">Se si collega un modulo di *output del servizio Web* al modulo *[Train Model][train-model]* dell'esperimento, si consente all'esperimento di training di generare un nuovo modello sottoposto a training che sarà possibile usare in un esperimento predittivo.</span><span class="sxs-lookup"><span data-stu-id="93a93-123">By connecting a *Web Service Output* module to the experiment's *[Train Model][train-model]* module, you enable the training experiment to produce a new trained model that you can use in your predictive experiment.</span></span> <span data-ttu-id="93a93-124">Se si dispone di un modulo di *valutazione del modello*, è possibile collegare l'output del servizio Web anche per ottenere i risultati della valutazione come output.</span><span class="sxs-lookup"><span data-stu-id="93a93-124">If you have an *Evaluate Model* module, you can also attach web service output to get the evaluation results as output.</span></span>

<span data-ttu-id="93a93-125">Per aggiornare l'esperimento di training:</span><span class="sxs-lookup"><span data-stu-id="93a93-125">To update your training experiment:</span></span>

1. <span data-ttu-id="93a93-126">Connettere un modulo di *input del servizio Web* al proprio input di dati (ad esempio, un modulo di *pulizia dei dati mancanti*).</span><span class="sxs-lookup"><span data-stu-id="93a93-126">Connect a *Web Service Input* module to your data input (for example, a *Clean Missing Data* module).</span></span> <span data-ttu-id="93a93-127">In genere, infatti, si vuole che i dati di input vengano elaborati allo stesso modo dei dati di training originali.</span><span class="sxs-lookup"><span data-stu-id="93a93-127">Typically, you want to ensure that your input data is processed in the same way as your original training data.</span></span>
2. <span data-ttu-id="93a93-128">Connettere un modulo di *output del servizio Web* all'output del modulo *Training modello*.</span><span class="sxs-lookup"><span data-stu-id="93a93-128">Connect a *Web Service Output* module to the output of your *Train Model* module.</span></span>
3. <span data-ttu-id="93a93-129">Se si ha un modulo di *valutazione del modello* e si vuole eseguire l'output dei risultati della valutazione, connettere un modulo di *output del servizio Web* all'output del proprio modulo di *valutazione del modello*.</span><span class="sxs-lookup"><span data-stu-id="93a93-129">If you have an *Evaluate Model* module and you want to output the evaluation results, connect a *Web Service Output* module to the output of your *Evaluate Model* module.</span></span>

<span data-ttu-id="93a93-130">Eseguire l'esperimento.</span><span class="sxs-lookup"><span data-stu-id="93a93-130">Run your experiment.</span></span>

<span data-ttu-id="93a93-131">Sarà quindi necessario distribuire l'esperimento di training come un servizio Web che produce un modello sottoposto a training e risultati di valutazione del modello.</span><span class="sxs-lookup"><span data-stu-id="93a93-131">Next, you must deploy the training experiment as a web service that produces a trained model and model evaluation results.</span></span>  

<span data-ttu-id="93a93-132">Nella parte inferiore dell'area di disegno dell'esperimento fare clic su **Set Up Web Service** (Configura servizio Web) e selezionare **Deploy Web Service [New]** (Distribuisci servizio Web [Nuovo]).</span><span class="sxs-lookup"><span data-stu-id="93a93-132">At the bottom of the experiment canvas, click **Set Up Web Service**, and then select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="93a93-133">Il portale dei servizi Web Microsoft Azure Machine Learning visualizzerà la pagina **Deploy Web Service** (Distribuisci servizio Web).</span><span class="sxs-lookup"><span data-stu-id="93a93-133">The Azure Machine Learning Web Services portal opens to the **Deploy Web Service** page.</span></span> <span data-ttu-id="93a93-134">Digitare un nome per il servizio Web, scegliere un piano di pagamento e quindi fare clic su **Deploy**(Distribuisci).</span><span class="sxs-lookup"><span data-stu-id="93a93-134">Type a name for your web service, choose a payment plan, and then click **Deploy**.</span></span> <span data-ttu-id="93a93-135">È possibile usare solo il metodo Esecuzione batch per la creazione di modelli di training.</span><span class="sxs-lookup"><span data-stu-id="93a93-135">You can only use the Batch Execution method for creating trained models.</span></span>

## <a name="retrain-the-model-with-new-data-by-using-bes"></a><span data-ttu-id="93a93-136">Ripetere il training del modello con nuovi dati usando il servizio Esecuzione batch</span><span class="sxs-lookup"><span data-stu-id="93a93-136">Retrain the model with new data by using BES</span></span>
<span data-ttu-id="93a93-137">In questo esempio si userà il linguaggio C# per creare l'applicazione di ripetizione del training.</span><span class="sxs-lookup"><span data-stu-id="93a93-137">For this example, we're using C# to create the retraining application.</span></span> <span data-ttu-id="93a93-138">Per eseguire questa attività, tuttavia, è possibile usare anche il codice di esempio Python o R.</span><span class="sxs-lookup"><span data-stu-id="93a93-138">You can also use Python or R sample code to accomplish this task.</span></span>

<span data-ttu-id="93a93-139">Per chiamare le API per la ripetizione del training:</span><span class="sxs-lookup"><span data-stu-id="93a93-139">To call the retraining APIs:</span></span>

1. <span data-ttu-id="93a93-140">Creare un'applicazione console C# in Visual Studio. A tale scopo, selezionare **Nuovo** > **Progetto** > **Visual C#** > **Desktop classico di Windows** > **Applicazione console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="93a93-140">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="93a93-141">Accedere al portale dei servizi Web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="93a93-141">Sign in to the Machine Learning Web Services portal.</span></span>
3. <span data-ttu-id="93a93-142">Fare clic sul servizio Web usato.</span><span class="sxs-lookup"><span data-stu-id="93a93-142">Click the web service that you're working with.</span></span>
4. <span data-ttu-id="93a93-143">Fare clic su **Consume**(Uso).</span><span class="sxs-lookup"><span data-stu-id="93a93-143">Click **Consume**.</span></span>
5. <span data-ttu-id="93a93-144">Nella sezione **Sample Code** (Codice di esempio) nella parte inferiore della pagina **Consume** (Uso) fare clic su **Batch**.</span><span class="sxs-lookup"><span data-stu-id="93a93-144">At the bottom of the **Consume** page, in the **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="93a93-145">Copiare il codice C# di esempio per l'esecuzione batch e incollarlo nel file Program.cs,</span><span class="sxs-lookup"><span data-stu-id="93a93-145">Copy the sample C# code for batch execution and paste it into the Program.cs file.</span></span> <span data-ttu-id="93a93-146">verificando che lo spazio dei nomi rimanga invariato.</span><span class="sxs-lookup"><span data-stu-id="93a93-146">Make sure that the namespace remains intact.</span></span>

<span data-ttu-id="93a93-147">Aggiungere il pacchetto NuGet Microsoft.AspNet.WebApi.Client come specificato nei commenti.</span><span class="sxs-lookup"><span data-stu-id="93a93-147">Add the NuGet package Microsoft.AspNet.WebApi.Client, as specified in the comments.</span></span> <span data-ttu-id="93a93-148">Per aggiungere il riferimento a Microsoft.WindowsAzure.Storage.dll, è possibile che sia prima necessario installare la [libreria client per i servizi di archiviazione di Azure](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="93a93-148">To add the reference to Microsoft.WindowsAzure.Storage.dll, you might first need to install the [client library for Azure Storage services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

<span data-ttu-id="93a93-149">La schermata seguente illustra la pagina **Consume** (Utilizzo) del portale di servizi Web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="93a93-149">The following screenshot shows the **Consume** page in the Azure Machine Learning Web Services portal.</span></span>

![Pagina Consume (Utilizzo)][1]

### <a name="update-the-apikey-declaration"></a><span data-ttu-id="93a93-151">Aggiornare la dichiarazione apikey</span><span class="sxs-lookup"><span data-stu-id="93a93-151">Update the apikey declaration</span></span>
<span data-ttu-id="93a93-152">Individuare la dichiarazione **apikey**:</span><span class="sxs-lookup"><span data-stu-id="93a93-152">Locate the **apikey** declaration:</span></span>

    const string apiKey = "abc123"; // Replace this with the API key for the web service

<span data-ttu-id="93a93-153">Nella sezione **Basic consumption info** (Informazioni di base sul consumo) della pagina **Consume** (Uso) individuare la chiave primaria e copiarla nella dichiarazione **apikey**.</span><span class="sxs-lookup"><span data-stu-id="93a93-153">In the **Basic consumption info** section of the **Consume** page, locate the primary key and copy it to the **apikey** declaration.</span></span>

### <a name="update-the-azure-storage-information"></a><span data-ttu-id="93a93-154">Aggiornare le informazioni di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="93a93-154">Update the Azure Storage information</span></span>
<span data-ttu-id="93a93-155">Il codice di esempio BES carica un file da un'unità locale (ad esempio, "C:\temp\CensusIpnput.csv") in Archiviazione di Azure, lo elabora e scrive i risultati in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="93a93-155">The BES sample code uploads a file from a local drive (for example, "C:\temp\CensusIpnput.csv") to Azure Storage, processes it, and writes the results back to Azure Storage.</span></span>  

<span data-ttu-id="93a93-156">Per aggiornare le informazioni di Archiviazione di Azure è necessario recuperare dal portale classico di Azure il nome dell'account di archiviazione, la chiave e informazioni sul contenitore per l'account di archiviazione e quindi aggiornare i valori corrispondenti nel codice. Dopo aver eseguito l'esperimento, il flusso di lavoro dovrebbe risultare simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="93a93-156">To update the Azure Storage information, you must retrieve the storage account name, key, and container information for your storage account from the Azure classic portal, and then update the correspondi After running your experiment, the resulting workflow should be similar to the following:</span></span>

![Flusso di lavoro risultante dopo l'esecuzione][4]<span data-ttu-id="93a93-158">valori ng nel codice.</span><span class="sxs-lookup"><span data-stu-id="93a93-158">ng values in the code.</span></span>

1. <span data-ttu-id="93a93-159">Accedere al portale di Microsoft Azure classico.</span><span class="sxs-lookup"><span data-stu-id="93a93-159">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="93a93-160">Nella colonna di spostamento a sinistra fare clic su **Archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="93a93-160">In the left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="93a93-161">Nell'elenco degli account di archiviazione selezionarne uno per l'archiviazione del modello per il quale è stato ripetuto il training.</span><span class="sxs-lookup"><span data-stu-id="93a93-161">From the list of storage accounts, select one to store the retrained model.</span></span>
4. <span data-ttu-id="93a93-162">Nella parte inferiore della pagina fare clic su **Gestisci chiavi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="93a93-162">At the bottom of the page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="93a93-163">Copiare e salvare la **chiave di accesso primaria** , quindi chiudere la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="93a93-163">Copy and save the **Primary Access Key** and close the dialog.</span></span>
6. <span data-ttu-id="93a93-164">Nella parte superiore della pagina fare clic su **Contenitori**.</span><span class="sxs-lookup"><span data-stu-id="93a93-164">At the top of the page, click **Containers**.</span></span>
7. <span data-ttu-id="93a93-165">Selezionare un contenitore esistente oppure crearne uno nuovo e salvare il nome.</span><span class="sxs-lookup"><span data-stu-id="93a93-165">Select an existing container, or create a new one and save the name.</span></span>

<span data-ttu-id="93a93-166">Individuare le dichiarazioni *StorageAccountName*, *StorageAccountKey* e *StorageContainerName* e aggiornare i valori salvati dal portale classico.</span><span class="sxs-lookup"><span data-stu-id="93a93-166">Locate the *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations, and update the values that you saved from the classic portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

<span data-ttu-id="93a93-167">È necessario anche assicurarsi che il file di input sia disponibile nella posizione specificata nel codice.</span><span class="sxs-lookup"><span data-stu-id="93a93-167">You also must ensure that the input file is available at the location that you specify in the code.</span></span>

### <a name="specify-the-output-location"></a><span data-ttu-id="93a93-168">Specificare il percorso di output</span><span class="sxs-lookup"><span data-stu-id="93a93-168">Specify the output location</span></span>
<span data-ttu-id="93a93-169">Quando si specifica il percorso di output nel payload della richiesta, l'estensione del file specificata in *RelativeLocation* deve essere indicata come `ilearner`.</span><span class="sxs-lookup"><span data-stu-id="93a93-169">When you specify the output location in the Request Payload, the extension of the file that is specified in *RelativeLocation* must be specified as `ilearner`.</span></span> <span data-ttu-id="93a93-170">Vedere l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="93a93-170">See the following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with the location you want to use for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

<span data-ttu-id="93a93-171">Di seguito è riportato un output di ripetizione del training di esempio: ![Output di ripetizione del training][6]</span><span class="sxs-lookup"><span data-stu-id="93a93-171">The following is an example of retraining output: ![Retraining output][6]</span></span>

## <a name="evaluate-the-retraining-results"></a><span data-ttu-id="93a93-172">Valutare i risultati della ripetizione del training</span><span class="sxs-lookup"><span data-stu-id="93a93-172">Evaluate the retraining results</span></span>
<span data-ttu-id="93a93-173">Quando si esegue l'applicazione, l'output include l'URL e il token di firma di accesso condiviso necessari per accedere ai risultati della valutazione.</span><span class="sxs-lookup"><span data-stu-id="93a93-173">When you run the application, the output includes the URL and shared access signatures token that are necessary to access the evaluation results.</span></span>

<span data-ttu-id="93a93-174">È possibile visualizzare i risultati sulle prestazioni del modello sottoposto nuovamente a training combinando *BaseLocation*, *RelativeLocation* e *SasBlobToken* dai risultati di output per *output2* (come illustrato nell'immagine precedente dell'output di ripetizione del training) e incollando l'URL completo nella barra degli indirizzi del browser.</span><span class="sxs-lookup"><span data-stu-id="93a93-174">You can see the performance results of the retrained model by combining the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results for *output2* (as shown in the preceding retraining output image) and pasting the complete URL into the browser address bar.</span></span>  

<span data-ttu-id="93a93-175">Esaminare i risultati per determinare se le prestazioni del modello appena sottoposto a training sono abbastanza elevate da sostituire quello esistente.</span><span class="sxs-lookup"><span data-stu-id="93a93-175">Examine the results to determine whether the newly trained model performs well enough to replace the existing one.</span></span>

<span data-ttu-id="93a93-176">Copiare *BaseLocation*, *RelativeLocation* e *SasBlobToken* dai risultati di output.</span><span class="sxs-lookup"><span data-stu-id="93a93-176">Copy the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results.</span></span>

## <a name="retrain-the-web-service"></a><span data-ttu-id="93a93-177">Ripetere il training del servizio Web</span><span class="sxs-lookup"><span data-stu-id="93a93-177">Retrain the web service</span></span>
<span data-ttu-id="93a93-178">Quando si ripete il training di un nuovo servizio Web, si aggiorna la definizione del servizio Web predittivo perché faccia riferimento al nuovo modello sottoposto a training.</span><span class="sxs-lookup"><span data-stu-id="93a93-178">When you retrain a new web service, you update the predictive web service definition to reference the new trained model.</span></span> <span data-ttu-id="93a93-179">La definizione del servizio Web è una rappresentazione interna del modello sottoposto a training del servizio Web e non è direttamente modificabile.</span><span class="sxs-lookup"><span data-stu-id="93a93-179">The web service definition is an internal representation of the trained model of the web service and is not directly modifiable.</span></span> <span data-ttu-id="93a93-180">Assicurarsi di recuperare la definizione del servizio Web per l'esperimento predittivo e non per l'esperimento di training.</span><span class="sxs-lookup"><span data-stu-id="93a93-180">Make sure that you are retrieving the web service definition for your predictive experiment and not your training experiment.</span></span>

## <a name="sign-in-to-azure-resource-manager"></a><span data-ttu-id="93a93-181">Accedere a Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="93a93-181">Sign in to Azure Resource Manager</span></span>
<span data-ttu-id="93a93-182">È prima necessario accedere al proprio account Azure dall'interno dell'ambiente di PowerShell tramite il cmdlet [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx).</span><span class="sxs-lookup"><span data-stu-id="93a93-182">You must first sign in to your Azure account from within the PowerShell environment by using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-the-web-service-definition-object"></a><span data-ttu-id="93a93-183">Ottenere l'oggetto definizione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="93a93-183">Get the Web Service Definition object</span></span>
<span data-ttu-id="93a93-184">È quindi necessario ottenere l'oggetto definizione del servizio Web chiamando il cmdlet [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx).</span><span class="sxs-lookup"><span data-stu-id="93a93-184">Next, get the Web Service Definition object by calling the [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="93a93-185">Per determinare il nome del gruppo di risorse di un servizio Web esistente, eseguire il cmdlet Get-AzureRmMlWebService senza parametri per visualizzare i servizi Web nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="93a93-185">To determine the resource group name of an existing web service, run the Get-AzureRmMlWebService cmdlet without any parameters to display the web services in your subscription.</span></span> <span data-ttu-id="93a93-186">Individuare il servizio Web e quindi osservare l'ID del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="93a93-186">Locate the web service, and then look at its web service ID.</span></span> <span data-ttu-id="93a93-187">Il nome del gruppo di risorse è il quarto elemento dell'ID, subito dopo l'elemento *resourceGroups* .</span><span class="sxs-lookup"><span data-stu-id="93a93-187">The name of the resource group is the fourth element in the ID, just after the *resourceGroups* element.</span></span> <span data-ttu-id="93a93-188">Nell'esempio seguente, il nome del gruppo di risorse è Default-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="93a93-188">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="93a93-189">In alternativa, per determinare il nome del gruppo di risorse di un servizio Web esistente, accedere al portale dei servizi Web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="93a93-189">Alternatively, to determine the resource group name of an existing web service, sign in to the Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="93a93-190">Selezionare il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="93a93-190">Select the web service.</span></span> <span data-ttu-id="93a93-191">Il nome del gruppo di risorse è il quinto elemento dell'URL del servizio Web, subito dopo l'elemento *resourceGroups* .</span><span class="sxs-lookup"><span data-stu-id="93a93-191">The resource group name is the fifth element of the URL of the web service, just after the *resourceGroups* element.</span></span> <span data-ttu-id="93a93-192">Nell'esempio seguente, il nome del gruppo di risorse è Default-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="93a93-192">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-the-web-service-definition-object-as-json"></a><span data-ttu-id="93a93-193">Esportare l'oggetto definizione del servizio Web in un file in formato JSON</span><span class="sxs-lookup"><span data-stu-id="93a93-193">Export the Web Service Definition object as JSON</span></span>
<span data-ttu-id="93a93-194">Per modificare la definizione in modo da poter usare il modello appena sottoposto a training, è prima necessario usare il cmdlet [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) per esportare la definizione in un file in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="93a93-194">To modify the definition of the trained model to use the newly trained model, you must first use the [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet to export it to a JSON-format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-the-reference-to-the-ilearner-blob"></a><span data-ttu-id="93a93-195">Aggiornare il riferimento al BLOB ilearner</span><span class="sxs-lookup"><span data-stu-id="93a93-195">Update the reference to the ilearner blob</span></span>
<span data-ttu-id="93a93-196">Negli asset individuare il [modello con training] e aggiornare il valore *uri* nel nodo *locationInfo* con l'URI del BLOB ilearner.</span><span class="sxs-lookup"><span data-stu-id="93a93-196">In the assets, locate the [trained model], update the *uri* value in the *locationInfo* node with the URI of the ilearner blob.</span></span> <span data-ttu-id="93a93-197">L'URI viene generato combinando i valori di *BaseLocation* e *RelativeLocation* dell'output della chiamata di ripetizione del training del servizio Esecuzione batch.</span><span class="sxs-lookup"><span data-stu-id="93a93-197">The URI is generated by combining the *BaseLocation* and the *RelativeLocation* from the output of the BES retraining call.</span></span>

     "asset3": {
        "name": "Retrain Sample [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-the-json-into-a-web-service-definition-object"></a><span data-ttu-id="93a93-198">Importare il file JSON in un oggetto definizione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="93a93-198">Import the JSON into a Web Service Definition object</span></span>
<span data-ttu-id="93a93-199">È necessario usare il cmdlet [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) per convertire di nuovo il file JSON modificato in un oggetto definizione del servizio Web che è possibile usare per aggiornare l'esperimento predicativo.</span><span class="sxs-lookup"><span data-stu-id="93a93-199">You must use the [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet to convert the modified JSON file back into a Web Service Definition object that you can use to update the predicative experiment.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-the-web-service"></a><span data-ttu-id="93a93-200">Aggiornare il servizio Web</span><span class="sxs-lookup"><span data-stu-id="93a93-200">Update the web service</span></span>
<span data-ttu-id="93a93-201">Usare infine il cmdlet [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) per aggiornare l'esperimento predittivo.</span><span class="sxs-lookup"><span data-stu-id="93a93-201">Finally, use the [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet to update the predictive experiment.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
