---
title: AAA(deprecated) pubblica machine learning tooAzure servizio web Marketplace | Documenti Microsoft
description: (obsoleto) Come toopublish il toohello servizio Web di Azure Machine Learning Azure Marketplace
services: machine-learning
documentationcenter: 
author: BharathS
manager: jhubbard
editor: cgronlun
ms.assetid: 68e908be-3a99-4cd7-9517-e2b5f2f341b8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: machine-learning-gallery-experiments
redirect_document_id: True
ms.openlocfilehash: 149abc3df9b79c1b37d233d5e85e803592ff1020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-toohello-azure-marketplace"></a><span data-ttu-id="8e41e-103">(obsoleto) Pubblicazione servizio Web di Azure Machine Learning toohello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="8e41e-103">(deprecated) Publish Azure Machine Learning Web Service toohello Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="8e41e-104">DataMarket e Servizi dati verranno ritirati e le sottoscrizioni esistenti verranno ritirate e annullate a partire dal 31/3/2017.</span><span class="sxs-lookup"><span data-stu-id="8e41e-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="8e41e-105">Di conseguenza, questo articolo è deprecato.</span><span class="sxs-lookup"><span data-stu-id="8e41e-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="8e41e-106">In alternativa, è possibile pubblicare il toohello esperimenti di Machine Learning [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) benefit hello della community di analisi scientifica dei dati hello.</span><span class="sxs-lookup"><span data-stu-id="8e41e-106">As an alternative, you can publish your Machine Learning experiments toohello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for hello benefit of hello data science community.</span></span> <span data-ttu-id="8e41e-107">Per ulteriori informazioni, vedere [condivisione e individuare le risorse in Cortana Intelligence Gallery hello](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span><span class="sxs-lookup"><span data-stu-id="8e41e-107">For more information, see [Share and discover resources in hello Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>

<span data-ttu-id="8e41e-108">Hello Azure Marketplace consente hello servizi web di Azure Machine Learning toopublish come a pagamento o gratuito servizi per l'utilizzo da parte dei clienti esterni.</span><span class="sxs-lookup"><span data-stu-id="8e41e-108">hello Azure Marketplace provides hello ability toopublish Azure Machine Learning web services as paid or free services for consumption by external customers.</span></span> <span data-ttu-id="8e41e-109">In questo articolo viene fornita una panoramica del processo con collegamenti tooguidelines tooget che è stato avviato.</span><span class="sxs-lookup"><span data-stu-id="8e41e-109">This article provides an overview of that process with links tooguidelines tooget you started.</span></span> <span data-ttu-id="8e41e-110">Tramite questo processo, apportare i servizi web disponibili per altri tooconsume sviluppatori nelle proprie applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8e41e-110">By using this process, you can make your web services available for other developers tooconsume in their applications.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-hello-publishing-process"></a><span data-ttu-id="8e41e-111">Panoramica del processo di pubblicazione hello</span><span class="sxs-lookup"><span data-stu-id="8e41e-111">Overview of hello publishing process</span></span>
<span data-ttu-id="8e41e-112">esempio Hello hello passaggi per la pubblicazione di un tooAzure di servizio web Azure Machine Learning Marketplace:</span><span class="sxs-lookup"><span data-stu-id="8e41e-112">hello following are hello steps for publishing an Azure Machine Learning web service tooAzure Marketplace:</span></span>

1. <span data-ttu-id="8e41e-113">Creare e pubblicare un servizio di richiesta-risposta di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="8e41e-113">Create and publish a Machine Learning Request-Response service (RRS)</span></span>
2. <span data-ttu-id="8e41e-114">Distribuire tooproduction servizio hello e ottenere informazioni sull'endpoint chiave API e OData hello.</span><span class="sxs-lookup"><span data-stu-id="8e41e-114">Deploy hello service tooproduction, and obtain hello API Key and OData endpoint information.</span></span>
3. <span data-ttu-id="8e41e-115">Utilizzo URL hello di hello pubblicati toopublish servizio web troppo[Azure Marketplace (dati di mercato)](https://publish.windowsazure.com/workspace/)</span><span class="sxs-lookup"><span data-stu-id="8e41e-115">Use hello URL of hello published web service toopublish too[Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span></span> 
4. <span data-ttu-id="8e41e-116">Una volta inviato, viene esaminato l'offerta e deve toobe approvata prima i clienti possono avviare acquisto.</span><span class="sxs-lookup"><span data-stu-id="8e41e-116">Once submitted, your offer is reviewed and needs toobe approved before your customers can start purchasing it.</span></span> <span data-ttu-id="8e41e-117">processo di pubblicazione Hello può richiedere qualche giorno lavorativo.</span><span class="sxs-lookup"><span data-stu-id="8e41e-117">hello publishing process can take a few business days.</span></span> 

## <a name="walk-through"></a><span data-ttu-id="8e41e-118">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="8e41e-118">Walk through</span></span>
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a><span data-ttu-id="8e41e-119">Passaggio 1: Creare e pubblicare un servizio di richiesta-risposta di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="8e41e-119">Step 1: Create and publish a Machine Learning Request-Response service (RRS)</span></span>
 <span data-ttu-id="8e41e-120">Se non è già stato fatto, vedere questa [procedura dettagliata](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="8e41e-120">If you have not done this already, please take a look at this [walk through](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

### <a name="step-2-deploy-hello-service-tooproduction-and-obtain-hello-api-key-and-odata-endpoint-information"></a><span data-ttu-id="8e41e-121">Passaggio 2: Distribuire tooproduction servizio hello e ottenere informazioni sull'endpoint chiave API e OData hello</span><span class="sxs-lookup"><span data-stu-id="8e41e-121">Step 2: Deploy hello service tooproduction, and obtain hello API Key and OData endpoint information</span></span>
1. <span data-ttu-id="8e41e-122">Da hello [portale di Azure classico](http://manage.windowsazure.com)selezionare hello **MACHINE LEARNING** opzione hello barra di navigazione sinistra e selezionare l'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8e41e-122">From hello [Azure Classic Portal](http://manage.windowsazure.com), select hello **MACHINE LEARNING** option from hello left navigation bar, and select your workspace.</span></span> 
2. <span data-ttu-id="8e41e-123">Fare clic su hello **servizi WEB** scheda e servizio web selezionare hello desideri toopublish toohello marketplace.</span><span class="sxs-lookup"><span data-stu-id="8e41e-123">Click on hello **WEB SERVICES** tab, and select hello web service you would like toopublish toohello marketplace.</span></span>
   
    ![Azure Marketplace][workspace]
3. <span data-ttu-id="8e41e-125">Selezionare l'endpoint di hello che comporta come toohave hello marketplace l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="8e41e-125">Select hello endpoint you would like toohave hello marketplace consume.</span></span> <span data-ttu-id="8e41e-126">Se non è stato creato alcun endpoint aggiuntivi, è possibile selezionare hello **predefinito** endpoint.</span><span class="sxs-lookup"><span data-stu-id="8e41e-126">If you have not created any additional endpoints, you can select hello **Default** endpoint.</span></span>
4. <span data-ttu-id="8e41e-127">Dopo aver selezionato sull'endpoint hello, sarà in grado di toosee hello **chiave API**.</span><span class="sxs-lookup"><span data-stu-id="8e41e-127">Once you have clicked on hello endpoint, you will be able toosee hello **API KEY**.</span></span> <span data-ttu-id="8e41e-128">Copiare la chiave, perché queste informazioni saranno necessarie in seguito nel passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="8e41e-128">You will need this piece of information later on in Step 3, so make a copy of it.</span></span>
   
    ![Azure Marketplace][apikey]
5. <span data-ttu-id="8e41e-130">Fare clic su hello **richiesta/risposta** toohello marketplace di servizi (metodo), a questo punto di pubblicazione dell'esecuzione batch non è supportata.</span><span class="sxs-lookup"><span data-stu-id="8e41e-130">Click on hello **REQUEST/RESPONSE** method, at this point we do not support publishing batch execution services toohello marketplace.</span></span> <span data-ttu-id="8e41e-131">Si passerà toohello API pagina della Guida per il metodo di richiesta/risposta hello.</span><span class="sxs-lookup"><span data-stu-id="8e41e-131">That will take you toohello API help page for hello Request/Response method.</span></span>
6. <span data-ttu-id="8e41e-132">Hello copia **indirizzo dell'Endpoint OData**, è necessario che queste informazioni in un secondo momento nel passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="8e41e-132">Copy hello **OData Endpoint Address**, you will need this information later on in Step 3.</span></span>
   
    ![Azure Marketplace][odata]

<span data-ttu-id="8e41e-134">distribuire il servizio di hello nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="8e41e-134">deploy hello service into production.</span></span>

### <a name="step-3-use-hello-url-of-hello-published-web-service-toopublish-tooazure-marketplace-datamarket"></a><span data-ttu-id="8e41e-135">Passaggio 3: Utilizzo hello URL di hello pubblicati web servizio toopublish tooAzure Marketplace (DataMarket)</span><span class="sxs-lookup"><span data-stu-id="8e41e-135">Step 3: Use hello URL of hello published web service toopublish tooAzure Marketplace (DataMarket)</span></span>
1. <span data-ttu-id="8e41e-136">Passare troppo[Azure Marketplace (dati di mercato)](http://datamarket.azure.com/home)</span><span class="sxs-lookup"><span data-stu-id="8e41e-136">Navigate too[Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span></span> 
2. <span data-ttu-id="8e41e-137">Fare clic su hello **pubblica** collegamento nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="8e41e-137">Click on hello **Publish** link at hello top of hello page.</span></span> <span data-ttu-id="8e41e-138">L'operazione richiederà toohello [portale di pubblicazione di Microsoft Azure](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="8e41e-138">This will take you toohello [Microsoft Azure Publishing Portal](https://publish.windowsazure.com)</span></span>
3. <span data-ttu-id="8e41e-139">Fare clic su hello **editori** sezione tooregister come server di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="8e41e-139">Click on hello **publishers** section tooregister as a publisher.</span></span>
4. <span data-ttu-id="8e41e-140">Quando si crea una nuova offerta, selezionare **Servizi dati**, quindi fare clic su **Crea un nuovo documento di servizio dati**.</span><span class="sxs-lookup"><span data-stu-id="8e41e-140">When creating a new offer, select **Data Services**, then click **Create a New Data Service**.</span></span> 
   
   ![Azure Marketplace][image1]
   
   <br />
5. <span data-ttu-id="8e41e-142">In **Piani** fornire le informazioni relative all'offerta, incluso un piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="8e41e-142">Under **Plans** provide information on your offering, including a pricing plan.</span></span> <span data-ttu-id="8e41e-143">Decidere se offrire un servizio gratuito o a pagamento.</span><span class="sxs-lookup"><span data-stu-id="8e41e-143">Decide if you will offer a free or paid service.</span></span> <span data-ttu-id="8e41e-144">tooget a pagamento, fornire le informazioni di pagamento, ad esempio le informazioni bancari e fiscali.</span><span class="sxs-lookup"><span data-stu-id="8e41e-144">tooget paid, provide payment information such as your bank and tax information.</span></span>
6. <span data-ttu-id="8e41e-145">In **Marketing** forniscono informazioni sull'offerta, ad esempio titolo hello e una descrizione per l'offerta.</span><span class="sxs-lookup"><span data-stu-id="8e41e-145">Under **Marketing** provide information about your offer, such as hello title and description for your offer.</span></span>
7. <span data-ttu-id="8e41e-146">In **prezzi** è possibile impostare il prezzo di hello per i piani di paesi specifici, oppure consentire al sistema di hello "autoprice" l'offerta.</span><span class="sxs-lookup"><span data-stu-id="8e41e-146">Under **Pricing** you can set hello price for your plans for specific countries, or let hello system "autoprice" your offer.</span></span>
8. <span data-ttu-id="8e41e-147">In hello **servizio dati** scheda, fare clic su **servizio Web** come hello **origine dati**.</span><span class="sxs-lookup"><span data-stu-id="8e41e-147">On hello **Data Service** tab, click **Web Service** as hello **Data Source**.</span></span>
   
    ![Azure Marketplace][image2]
9. <span data-ttu-id="8e41e-149">Ottenere hello web service URL e la chiave API da hello portale classico di Azure, come illustrato nel passaggio 2 precedente.</span><span class="sxs-lookup"><span data-stu-id="8e41e-149">Get hello web service URL and API key from hello Azure Classic Portal, as explained in step 2 above.</span></span>
10. <span data-ttu-id="8e41e-150">Nella casella di finestra di dialogo programma di installazione del servizio dati di Marketplace hello, incollare l'indirizzo dell'endpoint OData hello in hello **URL del servizio** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="8e41e-150">In hello Marketplace Data Service setup dialog box, paste hello OData endpoint address into hello **Service URL** text box.</span></span>
11. <span data-ttu-id="8e41e-151">Per **autenticazione**, scegliere **intestazione** come hello **schema di autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="8e41e-151">For **Authentication**, choose **Header** as hello **Authentication Scheme**.</span></span>
    
    * <span data-ttu-id="8e41e-152">Immettere "Authorization" per hello **nome intestazione**.</span><span class="sxs-lookup"><span data-stu-id="8e41e-152">Enter "Authorization" for hello **Header Name**.</span></span>
    * <span data-ttu-id="8e41e-153">Per hello **valore dell'intestazione**, immettere "Bearer" (senza virgolette hello), fare clic su hello **spazio** barra e quindi incollare la chiave API hello.</span><span class="sxs-lookup"><span data-stu-id="8e41e-153">For hello **Header Value**, enter "Bearer" (without hello quotation marks), click hello **Space** bar, and then paste hello API key.</span></span>
    * <span data-ttu-id="8e41e-154">Seleziona hello **questo servizio è OData** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="8e41e-154">Select hello **This Service is OData** check box.</span></span>
    * <span data-ttu-id="8e41e-155">Fare clic su **Test connessione** connessione hello tootest.</span><span class="sxs-lookup"><span data-stu-id="8e41e-155">Click **Test Connection** tootest hello connection.</span></span>
12. <span data-ttu-id="8e41e-156">In **Categorie** assicurarsi che sia selezionata l'opzione **Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="8e41e-156">Under **Categories**, ensure **Machine Learning** is selected.</span></span>
13. <span data-ttu-id="8e41e-157">Dopo avere immesso tutti hello metadati sull'offerta, fare clic su **pubblica**e quindi **Push tooStaging**.</span><span class="sxs-lookup"><span data-stu-id="8e41e-157">When you are done entering all hello metadata about your offer, click on **Publish**, and then **Push tooStaging**.</span></span> <span data-ttu-id="8e41e-158">A questo punto, si verrà informato di eventuali problemi rimanenti che è necessario toofix.</span><span class="sxs-lookup"><span data-stu-id="8e41e-158">At this point, you will be notified of any remaining issues that you need toofix.</span></span>
14. <span data-ttu-id="8e41e-159">Dopo aver verificato il completamento di tutti i problemi in sospeso hello, fare clic su **richiesta approvazione toopush tooProduction**.</span><span class="sxs-lookup"><span data-stu-id="8e41e-159">After you have ensured completion of all hello outstanding issues, click on **Request approval toopush tooProduction**.</span></span> <span data-ttu-id="8e41e-160">processo di pubblicazione Hello può richiedere qualche giorno lavorativo.</span><span class="sxs-lookup"><span data-stu-id="8e41e-160">hello publishing process can take a few business days.</span></span> 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

