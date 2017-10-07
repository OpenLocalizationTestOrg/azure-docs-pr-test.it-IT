---
title: servizio web esistente predittiva aaaRetrain | Documenti Microsoft
description: Informazioni su come tooretrain un modello e aggiornamento hello toouse hello appena sottoposto a training modello di servizio web in Azure Machine Learning.
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
ms.openlocfilehash: fb0760d0a2adc34fc5f3df1ae41bdac075f91bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a><span data-ttu-id="71e66-103">Ripetere il training di un servizio Web predittivo esistente</span><span class="sxs-lookup"><span data-stu-id="71e66-103">Retrain an existing predictive web service</span></span>
<span data-ttu-id="71e66-104">Questo documento descrive hello ripetizione di training processo per hello seguente scenario:</span><span class="sxs-lookup"><span data-stu-id="71e66-104">This document describes hello retraining process for hello following scenario:</span></span>

* <span data-ttu-id="71e66-105">Si dispone di un esperimento di training e di un esperimento predittivo distribuito come un servizio Web operativo.</span><span class="sxs-lookup"><span data-stu-id="71e66-105">You have a training experiment and a predictive experiment that you have deployed as an operationalized web service.</span></span>
* <span data-ttu-id="71e66-106">Si dispone di nuovi dati che si desidera il tooperform toouse di servizio web predittivo il relativo punteggio.</span><span class="sxs-lookup"><span data-stu-id="71e66-106">You have new data that you want your predictive web service toouse tooperform its scoring.</span></span>

> [!NOTE] 
> <span data-ttu-id="71e66-107">un nuovo servizio web deve disporre di autorizzazioni sufficienti in hello toowhich di sottoscrizione per la distribuzione del servizio web hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="71e66-107">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="71e66-108">Per ulteriori informazioni, vedere [gestire un servizio Web tramite il portale di servizi Web di Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="71e66-108">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="71e66-109">A partire dal servizio web esistente e gli esperimenti, è necessario toofollow questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="71e66-109">Starting with your existing web service and experiments, you need toofollow these steps:</span></span>

1. <span data-ttu-id="71e66-110">Aggiornare il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="71e66-110">Update hello model.</span></span>
   1. <span data-ttu-id="71e66-111">Modificare il tooallow esperimento di training per web servizio input e output.</span><span class="sxs-lookup"><span data-stu-id="71e66-111">Modify your training experiment tooallow for web service inputs and outputs.</span></span>
   2. <span data-ttu-id="71e66-112">Distribuire hello esperimento di training come un servizio web i.</span><span class="sxs-lookup"><span data-stu-id="71e66-112">Deploy hello training experiment as a retraining web service.</span></span>
   3. <span data-ttu-id="71e66-113">Modello dell'esperimento di training hello servizio esecuzione Batch (BES) tooretrain hello.</span><span class="sxs-lookup"><span data-stu-id="71e66-113">Use hello training experiment's Batch Execution Service (BES) tooretrain hello model.</span></span>
2. <span data-ttu-id="71e66-114">Utilizzare l'esperimento predittiva di hello Azure Machine Learning PowerShell cmdlet tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="71e66-114">Use hello Azure Machine Learning PowerShell cmdlets tooupdate hello predictive experiment.</span></span>
   1. <span data-ttu-id="71e66-115">Accedi tooyour account di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="71e66-115">Sign in tooyour Azure Resource Manager account.</span></span>
   2. <span data-ttu-id="71e66-116">Ottenere una definizione del servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="71e66-116">Get hello web service definition.</span></span>
   3. <span data-ttu-id="71e66-117">Esportare una definizione del servizio web hello in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="71e66-117">Export hello web service definition as JSON.</span></span>
   4. <span data-ttu-id="71e66-118">Aggiornare i blob di ilearner toohello riferimento hello in hello JSON.</span><span class="sxs-lookup"><span data-stu-id="71e66-118">Update hello reference toohello ilearner blob in hello JSON.</span></span>
   5. <span data-ttu-id="71e66-119">Importare hello JSON in una definizione del servizio web.</span><span class="sxs-lookup"><span data-stu-id="71e66-119">Import hello JSON into a web service definition.</span></span>
   6. <span data-ttu-id="71e66-120">Aggiornare il servizio web di hello con una nuova definizione di servizio web.</span><span class="sxs-lookup"><span data-stu-id="71e66-120">Update hello web service with a new web service definition.</span></span>

## <a name="deploy-hello-training-experiment"></a><span data-ttu-id="71e66-121">Distribuire l'esperimento di training hello</span><span class="sxs-lookup"><span data-stu-id="71e66-121">Deploy hello training experiment</span></span>
<span data-ttu-id="71e66-122">esperimento di training toodeploy hello come i servizio web, è necessario aggiungere l'input e output toohello modello di servizio web.</span><span class="sxs-lookup"><span data-stu-id="71e66-122">toodeploy hello training experiment as a retraining web service, you must add web service inputs and outputs toohello model.</span></span> <span data-ttu-id="71e66-123">Connettendo un *Output del servizio Web* dell'esperimento di modulo toohello  *[Train Model] [ train-model]*  modulo, si abilita hello esperimento di training tooproduce un nuovo modello con training che è possibile utilizzare nell'esperimento predittiva.</span><span class="sxs-lookup"><span data-stu-id="71e66-123">By connecting a *Web Service Output* module toohello experiment's *[Train Model][train-model]* module, you enable hello training experiment tooproduce a new trained model that you can use in your predictive experiment.</span></span> <span data-ttu-id="71e66-124">Se dispone di un *Evaluate Model* modulo, è inoltre possibile allegare i risultati della valutazione hello tooget output servizio web come output.</span><span class="sxs-lookup"><span data-stu-id="71e66-124">If you have an *Evaluate Model* module, you can also attach web service output tooget hello evaluation results as output.</span></span>

<span data-ttu-id="71e66-125">tooupdate l'esperimento di training:</span><span class="sxs-lookup"><span data-stu-id="71e66-125">tooupdate your training experiment:</span></span>

1. <span data-ttu-id="71e66-126">Connettere un *Web servizio Input* tooyour dati del modulo di input (ad esempio, un *Clean Missing Data* modulo).</span><span class="sxs-lookup"><span data-stu-id="71e66-126">Connect a *Web Service Input* module tooyour data input (for example, a *Clean Missing Data* module).</span></span> <span data-ttu-id="71e66-127">In genere, si desidera tooensure che i dati di input viene elaborati in hello stesso come dati di training originale.</span><span class="sxs-lookup"><span data-stu-id="71e66-127">Typically, you want tooensure that your input data is processed in hello same way as your original training data.</span></span>
2. <span data-ttu-id="71e66-128">Connettere un *Output del servizio Web* toohello output del modulo del *Train Model* modulo.</span><span class="sxs-lookup"><span data-stu-id="71e66-128">Connect a *Web Service Output* module toohello output of your *Train Model* module.</span></span>
3. <span data-ttu-id="71e66-129">Se dispone di un *Evaluate Model* modulo e si desidera che i risultati della valutazione hello toooutput, connettere un *Output del servizio Web* toohello output del modulo del *Evaluate Model* modulo.</span><span class="sxs-lookup"><span data-stu-id="71e66-129">If you have an *Evaluate Model* module and you want toooutput hello evaluation results, connect a *Web Service Output* module toohello output of your *Evaluate Model* module.</span></span>

<span data-ttu-id="71e66-130">Eseguire l'esperimento.</span><span class="sxs-lookup"><span data-stu-id="71e66-130">Run your experiment.</span></span>

<span data-ttu-id="71e66-131">Successivamente, è necessario distribuire hello esperimento di training come servizio web che produce un modello con training e risultati della valutazione del modello.</span><span class="sxs-lookup"><span data-stu-id="71e66-131">Next, you must deploy hello training experiment as a web service that produces a trained model and model evaluation results.</span></span>  

<span data-ttu-id="71e66-132">Nella parte inferiore di hello dell'area di disegno esperimento hello, fare clic su **di servizio Web**, quindi selezionare **distribuzione servizio Web [New]**.</span><span class="sxs-lookup"><span data-stu-id="71e66-132">At hello bottom of hello experiment canvas, click **Set Up Web Service**, and then select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="71e66-133">viene visualizzato il portale di servizi Web di Azure Machine Learning Hello toohello **distribuzione servizio Web** pagina.</span><span class="sxs-lookup"><span data-stu-id="71e66-133">hello Azure Machine Learning Web Services portal opens toohello **Deploy Web Service** page.</span></span> <span data-ttu-id="71e66-134">Digitare un nome per il servizio Web, scegliere un piano di pagamento e quindi fare clic su **Deploy**(Distribuisci).</span><span class="sxs-lookup"><span data-stu-id="71e66-134">Type a name for your web service, choose a payment plan, and then click **Deploy**.</span></span> <span data-ttu-id="71e66-135">Utilizzare il metodo di esecuzione Batch hello solo per la creazione di modelli di training.</span><span class="sxs-lookup"><span data-stu-id="71e66-135">You can only use hello Batch Execution method for creating trained models.</span></span>

## <a name="retrain-hello-model-with-new-data-by-using-bes"></a><span data-ttu-id="71e66-136">Ripetere il training del modello di hello con nuovi dati utilizzando BES</span><span class="sxs-lookup"><span data-stu-id="71e66-136">Retrain hello model with new data by using BES</span></span>
<span data-ttu-id="71e66-137">Per questo esempio, si usa c# toocreate hello formazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="71e66-137">For this example, we're using C# toocreate hello retraining application.</span></span> <span data-ttu-id="71e66-138">È inoltre possibile utilizzare Python o R tooaccomplish codice di esempio questa attività.</span><span class="sxs-lookup"><span data-stu-id="71e66-138">You can also use Python or R sample code tooaccomplish this task.</span></span>

<span data-ttu-id="71e66-139">hello toocall ripetizione di training API:</span><span class="sxs-lookup"><span data-stu-id="71e66-139">toocall hello retraining APIs:</span></span>

1. <span data-ttu-id="71e66-140">Creare un'applicazione console C# in Visual Studio. A tale scopo, selezionare **Nuovo** > **Progetto** > **Visual C#** > **Desktop classico di Windows** > **Applicazione console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="71e66-140">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="71e66-141">Accedi toohello portale di servizi Web di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="71e66-141">Sign in toohello Machine Learning Web Services portal.</span></span>
3. <span data-ttu-id="71e66-142">Fare clic su servizio web hello che si sta lavorando.</span><span class="sxs-lookup"><span data-stu-id="71e66-142">Click hello web service that you're working with.</span></span>
4. <span data-ttu-id="71e66-143">Fare clic su **Consume**(Uso).</span><span class="sxs-lookup"><span data-stu-id="71e66-143">Click **Consume**.</span></span>
5. <span data-ttu-id="71e66-144">Nella parte inferiore di hello di hello **consumare** pagina hello **codice di esempio** fare clic su **Batch**.</span><span class="sxs-lookup"><span data-stu-id="71e66-144">At hello bottom of hello **Consume** page, in hello **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="71e66-145">Copiare hello c# codice di esempio per l'esecuzione batch e incollarlo nel file Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="71e66-145">Copy hello sample C# code for batch execution and paste it into hello Program.cs file.</span></span> <span data-ttu-id="71e66-146">Verificare che lo spazio dei nomi hello rimane invariata.</span><span class="sxs-lookup"><span data-stu-id="71e66-146">Make sure that hello namespace remains intact.</span></span>

<span data-ttu-id="71e66-147">Aggiungere il pacchetto NuGet hello webapi, come specificato nei commenti hello.</span><span class="sxs-lookup"><span data-stu-id="71e66-147">Add hello NuGet package Microsoft.AspNet.WebApi.Client, as specified in hello comments.</span></span> <span data-ttu-id="71e66-148">tooadd hello riferimento tooMicrosoft.WindowsAzure.Storage.dll, è innanzitutto necessario tooinstall hello [libreria client per servizi di archiviazione di Azure](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="71e66-148">tooadd hello reference tooMicrosoft.WindowsAzure.Storage.dll, you might first need tooinstall hello [client library for Azure Storage services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

<span data-ttu-id="71e66-149">Hello schermata riportata di seguito viene illustrato hello **consumare** pagina nel portale di servizi Web di Azure Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="71e66-149">hello following screenshot shows hello **Consume** page in hello Azure Machine Learning Web Services portal.</span></span>

![Pagina Consume (Utilizzo)][1]

### <a name="update-hello-apikey-declaration"></a><span data-ttu-id="71e66-151">Aggiornare hello apikey dichiarazione</span><span class="sxs-lookup"><span data-stu-id="71e66-151">Update hello apikey declaration</span></span>
<span data-ttu-id="71e66-152">Individuare hello **apikey** dichiarazione:</span><span class="sxs-lookup"><span data-stu-id="71e66-152">Locate hello **apikey** declaration:</span></span>

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

<span data-ttu-id="71e66-153">In hello **informazioni di base al consumo** sezione di hello **consumare** individuare la chiave primaria di hello e copiarlo toohello **apikey** dichiarazione.</span><span class="sxs-lookup"><span data-stu-id="71e66-153">In hello **Basic consumption info** section of hello **Consume** page, locate hello primary key and copy it toohello **apikey** declaration.</span></span>

### <a name="update-hello-azure-storage-information"></a><span data-ttu-id="71e66-154">Aggiornare le informazioni di archiviazione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="71e66-154">Update hello Azure Storage information</span></span>
<span data-ttu-id="71e66-155">codice di esempio BES Hello carica un file da un tooAzure unità locale (ad esempio, "C:\temp\CensusIpnput.csv"), archiviazione, elabora e scrive hello risultati indietro tooAzure archiviazione.</span><span class="sxs-lookup"><span data-stu-id="71e66-155">hello BES sample code uploads a file from a local drive (for example, "C:\temp\CensusIpnput.csv") tooAzure Storage, processes it, and writes hello results back tooAzure Storage.</span></span>  

<span data-ttu-id="71e66-156">informazioni di archiviazione di Azure hello tooupdate, è necessario recuperare l'account di archiviazione hello nome, chiave e contenitore le informazioni dell'account di archiviazione dal portale di Azure classico hello e aggiornamento hello correspondi dopo aver eseguito l'esperimento, hello risultante flusso di lavoro deve essere simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="71e66-156">tooupdate hello Azure Storage information, you must retrieve hello storage account name, key, and container information for your storage account from hello Azure classic portal, and then update hello correspondi After running your experiment, hello resulting workflow should be similar toohello following:</span></span>

![Flusso di lavoro risultante dopo l'esecuzione][4]<span data-ttu-id="71e66-158">valori nel codice hello NG.</span><span class="sxs-lookup"><span data-stu-id="71e66-158">ng values in hello code.</span></span>

1. <span data-ttu-id="71e66-159">Accedi toohello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="71e66-159">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="71e66-160">Nella colonna sinistra hello, fare clic su **archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="71e66-160">In hello left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="71e66-161">Dall'elenco di hello di account di archiviazione, selezionare uno toostore hello ripetere il training del modello.</span><span class="sxs-lookup"><span data-stu-id="71e66-161">From hello list of storage accounts, select one toostore hello retrained model.</span></span>
4. <span data-ttu-id="71e66-162">Nella parte inferiore di hello della pagina hello, fare clic su **Gestisci chiavi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="71e66-162">At hello bottom of hello page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="71e66-163">Copiare e salvare hello **chiave di accesso primaria** e hello Chiudi finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="71e66-163">Copy and save hello **Primary Access Key** and close hello dialog.</span></span>
6. <span data-ttu-id="71e66-164">Nella parte superiore di hello della pagina hello, fare clic su **contenitori**.</span><span class="sxs-lookup"><span data-stu-id="71e66-164">At hello top of hello page, click **Containers**.</span></span>
7. <span data-ttu-id="71e66-165">Selezionare un contenitore esistente, o crearne uno nuovo e salvare il nome di hello.</span><span class="sxs-lookup"><span data-stu-id="71e66-165">Select an existing container, or create a new one and save hello name.</span></span>

<span data-ttu-id="71e66-166">Individuare hello *StorageAccountName*, *StorageAccountKey*, e *StorageContainerName* dichiarazioni e aggiornare i valori hello salvato dal portale classico hello .</span><span class="sxs-lookup"><span data-stu-id="71e66-166">Locate hello *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations, and update hello values that you saved from hello classic portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

<span data-ttu-id="71e66-167">È inoltre necessario assicurarsi che file di input hello è disponibile nel percorso di hello specificate nel codice hello.</span><span class="sxs-lookup"><span data-stu-id="71e66-167">You also must ensure that hello input file is available at hello location that you specify in hello code.</span></span>

### <a name="specify-hello-output-location"></a><span data-ttu-id="71e66-168">Specificare il percorso di output di hello</span><span class="sxs-lookup"><span data-stu-id="71e66-168">Specify hello output location</span></span>
<span data-ttu-id="71e66-169">Quando si specifica il percorso di output di hello in hello del payload della richiesta, hello estensione del file hello specificato in *RelativeLocation* deve essere specificato come `ilearner`.</span><span class="sxs-lookup"><span data-stu-id="71e66-169">When you specify hello output location in hello Request Payload, hello extension of hello file that is specified in *RelativeLocation* must be specified as `ilearner`.</span></span> <span data-ttu-id="71e66-170">Vedere hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="71e66-170">See hello following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you want toouse for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

<span data-ttu-id="71e66-171">Hello seguito è riportato un esempio di output di ripetizione di training: ![ripetizione di training output][6]</span><span class="sxs-lookup"><span data-stu-id="71e66-171">hello following is an example of retraining output: ![Retraining output][6]</span></span>

## <a name="evaluate-hello-retraining-results"></a><span data-ttu-id="71e66-172">Valutare i risultati di ripetizione di training hello</span><span class="sxs-lookup"><span data-stu-id="71e66-172">Evaluate hello retraining results</span></span>
<span data-ttu-id="71e66-173">Quando si esegue un'applicazione hello, l'output di hello include hello URL e il token di firme di accesso condiviso che sono risultati della valutazione hello tooaccess necessarie.</span><span class="sxs-lookup"><span data-stu-id="71e66-173">When you run hello application, hello output includes hello URL and shared access signatures token that are necessary tooaccess hello evaluation results.</span></span>

<span data-ttu-id="71e66-174">È possibile visualizzare i risultati delle prestazioni hello di hello Training modello combinando hello *BaseLocation*, *RelativeLocation*, e *SasBlobToken* dai risultati di output di hello per *USCITA2* (come mostrato nella precedente ripetizione di training immagine di output di hello) e incollare l'URL completo di hello nella barra degli indirizzi del browser hello.</span><span class="sxs-lookup"><span data-stu-id="71e66-174">You can see hello performance results of hello retrained model by combining hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results for *output2* (as shown in hello preceding retraining output image) and pasting hello complete URL into hello browser address bar.</span></span>  

<span data-ttu-id="71e66-175">Esamina hello risultati toodetermine modello sottoposto a training appena hello esegue anche sufficiente hello tooreplace uno esistente.</span><span class="sxs-lookup"><span data-stu-id="71e66-175">Examine hello results toodetermine whether hello newly trained model performs well enough tooreplace hello existing one.</span></span>

<span data-ttu-id="71e66-176">Hello copia *BaseLocation*, *RelativeLocation*, e *SasBlobToken* dai risultati di output di hello.</span><span class="sxs-lookup"><span data-stu-id="71e66-176">Copy hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results.</span></span>

## <a name="retrain-hello-web-service"></a><span data-ttu-id="71e66-177">Ripetere il training del servizio web hello</span><span class="sxs-lookup"><span data-stu-id="71e66-177">Retrain hello web service</span></span>
<span data-ttu-id="71e66-178">Quando si ripetere il training di un nuovo servizio web, si aggiorna hello predittiva definizione tooreference hello nuovo sottoposto a training modello di servizio web.</span><span class="sxs-lookup"><span data-stu-id="71e66-178">When you retrain a new web service, you update hello predictive web service definition tooreference hello new trained model.</span></span> <span data-ttu-id="71e66-179">definizione del servizio web Hello è una rappresentazione interna del modello con training di hello del servizio web hello e non è direttamente modificabile.</span><span class="sxs-lookup"><span data-stu-id="71e66-179">hello web service definition is an internal representation of hello trained model of hello web service and is not directly modifiable.</span></span> <span data-ttu-id="71e66-180">Assicurarsi che si desidera recuperare definizione hello del servizio web per l'esperimento predittiva e non l'esperimento di training.</span><span class="sxs-lookup"><span data-stu-id="71e66-180">Make sure that you are retrieving hello web service definition for your predictive experiment and not your training experiment.</span></span>

## <a name="sign-in-tooazure-resource-manager"></a><span data-ttu-id="71e66-181">Accedi tooAzure Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="71e66-181">Sign in tooAzure Resource Manager</span></span>
<span data-ttu-id="71e66-182">È innanzitutto necessario accedere tooyour account di Azure dall'ambiente di PowerShell hello utilizzando hello [Aggiungi AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="71e66-182">You must first sign in tooyour Azure account from within hello PowerShell environment by using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-hello-web-service-definition-object"></a><span data-ttu-id="71e66-183">Ottenere l'oggetto di definizione del servizio Web hello</span><span class="sxs-lookup"><span data-stu-id="71e66-183">Get hello Web Service Definition object</span></span>
<span data-ttu-id="71e66-184">Successivamente, ottenere l'oggetto di definizione del servizio Web di hello dal chiamante hello [Get AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="71e66-184">Next, get hello Web Service Definition object by calling hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="71e66-185">toodetermine hello Nome gruppo di risorse di un servizio web esistente, eseguire il cmdlet Get-AzureRmMlWebService hello senza servizi parametri toodisplay hello web nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="71e66-185">toodetermine hello resource group name of an existing web service, run hello Get-AzureRmMlWebService cmdlet without any parameters toodisplay hello web services in your subscription.</span></span> <span data-ttu-id="71e66-186">Servizio web hello di individuare e quindi esaminare il relativo ID di servizio web.</span><span class="sxs-lookup"><span data-stu-id="71e66-186">Locate hello web service, and then look at its web service ID.</span></span> <span data-ttu-id="71e66-187">nome di Hello hello del gruppo di risorse è elemento quarto hello ID hello, subito dopo hello *resourceGroups* elemento.</span><span class="sxs-lookup"><span data-stu-id="71e66-187">hello name of hello resource group is hello fourth element in hello ID, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="71e66-188">Nell'esempio seguente di hello, nome del gruppo di risorse hello è MachineLearning-predefinito-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="71e66-188">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="71e66-189">In alternativa, toodetermine hello Nome gruppo di risorse di un servizio web, accedere al portale di servizi Web di Azure Machine Learning toohello.</span><span class="sxs-lookup"><span data-stu-id="71e66-189">Alternatively, toodetermine hello resource group name of an existing web service, sign in toohello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="71e66-190">Selezionare servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="71e66-190">Select hello web service.</span></span> <span data-ttu-id="71e66-191">nome del gruppo di risorse Hello è hello quinto elemento hello URL del servizio web hello, subito dopo hello *resourceGroups* elemento.</span><span class="sxs-lookup"><span data-stu-id="71e66-191">hello resource group name is hello fifth element of hello URL of hello web service, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="71e66-192">Nell'esempio seguente di hello, nome del gruppo di risorse hello è MachineLearning-predefinito-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="71e66-192">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-object-as-json"></a><span data-ttu-id="71e66-193">Esportare l'oggetto di definizione del servizio Web hello come JSON</span><span class="sxs-lookup"><span data-stu-id="71e66-193">Export hello Web Service Definition object as JSON</span></span>
<span data-ttu-id="71e66-194">definizione hello toomodify di hello toouse di modello con training hello appena eseguito il training del modello, è innanzitutto necessario utilizzare hello [esportazione AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) tooexport cmdlet è file tooa formato JSON.</span><span class="sxs-lookup"><span data-stu-id="71e66-194">toomodify hello definition of hello trained model toouse hello newly trained model, you must first use hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport it tooa JSON-format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob"></a><span data-ttu-id="71e66-195">Aggiornare hello riferimento toohello ilearner blob</span><span class="sxs-lookup"><span data-stu-id="71e66-195">Update hello reference toohello ilearner blob</span></span>
<span data-ttu-id="71e66-196">Attività hello, individuare hello [modello con training], aggiornamento hello *uri* valore hello *locationInfo* nodo con l'URI del blob ilearner hello hello.</span><span class="sxs-lookup"><span data-stu-id="71e66-196">In hello assets, locate hello [trained model], update hello *uri* value in hello *locationInfo* node with hello URI of hello ilearner blob.</span></span> <span data-ttu-id="71e66-197">Hello URI viene generato dalla combinazione hello *BaseLocation* hello e *RelativeLocation* dall'output di hello di chiamata i BES hello.</span><span class="sxs-lookup"><span data-stu-id="71e66-197">hello URI is generated by combining hello *BaseLocation* and hello *RelativeLocation* from hello output of hello BES retraining call.</span></span>

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

## <a name="import-hello-json-into-a-web-service-definition-object"></a><span data-ttu-id="71e66-198">Importare hello JSON in un oggetto di definizione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="71e66-198">Import hello JSON into a Web Service Definition object</span></span>
<span data-ttu-id="71e66-199">È necessario utilizzare hello [importazione AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modificati file JSON in un oggetto di definizione del servizio Web che è possibile utilizzare predicative esperimento di tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="71e66-199">You must use hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modified JSON file back into a Web Service Definition object that you can use tooupdate hello predicative experiment.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service"></a><span data-ttu-id="71e66-200">Aggiornare il servizio web hello</span><span class="sxs-lookup"><span data-stu-id="71e66-200">Update hello web service</span></span>
<span data-ttu-id="71e66-201">Infine, utilizzare hello [aggiornamento AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) tooupdate cmdlet hello esperimento predittiva.</span><span class="sxs-lookup"><span data-stu-id="71e66-201">Finally, use hello [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello predictive experiment.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
