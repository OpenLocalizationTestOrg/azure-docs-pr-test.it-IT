---
title: (Deprecato) Pubblicare il servizio Web di Machine Learning in Azure Marketplace | Documentazione Microsoft
description: (Deprecato) Informazioni su come pubblicare il servizio Web di Azure Machine Learning in Azure Marketplace
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
redirect_document_id: TRUE
ms.openlocfilehash: 3e3420872f0c604e027d1f309a6de6f52a5a788c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-to-the-azure-marketplace"></a><span data-ttu-id="438fc-103">(Deprecato) Pubblicare il servizio Web di Azure Machine Learning in Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="438fc-103">(deprecated) Publish Azure Machine Learning Web Service to the Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="438fc-104">DataMarket e Servizi dati verranno ritirati e le sottoscrizioni esistenti verranno ritirate e annullate a partire dal 31/3/2017.</span><span class="sxs-lookup"><span data-stu-id="438fc-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="438fc-105">Di conseguenza, questo articolo è deprecato.</span><span class="sxs-lookup"><span data-stu-id="438fc-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="438fc-106">In alternativa, è possibile pubblicare gli esperimenti di Machine Learning in [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) a vantaggio della community scientifica dei dati.</span><span class="sxs-lookup"><span data-stu-id="438fc-106">As an alternative, you can publish your Machine Learning experiments to the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for the benefit of the data science community.</span></span> <span data-ttu-id="438fc-107">Per altre informazioni, vedere [Condividere e scoprire risorse in Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span><span class="sxs-lookup"><span data-stu-id="438fc-107">For more information, see [Share and discover resources in the Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>

<span data-ttu-id="438fc-108">Azure Marketplace consente di pubblicare servizi Web di Azure Machine Learning sotto forma di servizi a pagamento o gratuiti utilizzabili da clienti esterni.</span><span class="sxs-lookup"><span data-stu-id="438fc-108">The Azure Marketplace provides the ability to publish Azure Machine Learning web services as paid or free services for consumption by external customers.</span></span> <span data-ttu-id="438fc-109">Questo articolo offre una panoramica del processo e fornisce i collegamenti alle linee guida per iniziare.</span><span class="sxs-lookup"><span data-stu-id="438fc-109">This article provides an overview of that process with links to guidelines to get you started.</span></span> <span data-ttu-id="438fc-110">In questo modo sarà possibile rendere disponibili i servizi Web ad altri sviluppatori che potranno usarli nelle proprie applicazioni.</span><span class="sxs-lookup"><span data-stu-id="438fc-110">By using this process, you can make your web services available for other developers to consume in their applications.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-the-publishing-process"></a><span data-ttu-id="438fc-111">Panoramica della procedura di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="438fc-111">Overview of the publishing process</span></span>
<span data-ttu-id="438fc-112">I passaggi seguenti consentono di pubblicare un servizio Web di Azure Machine Learning in Azure Marketplace:</span><span class="sxs-lookup"><span data-stu-id="438fc-112">The following are the steps for publishing an Azure Machine Learning web service to Azure Marketplace:</span></span>

1. <span data-ttu-id="438fc-113">Creare e pubblicare un servizio di richiesta-risposta di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="438fc-113">Create and publish a Machine Learning Request-Response service (RRS)</span></span>
2. <span data-ttu-id="438fc-114">Distribuire il servizio in produzione e ottenere le informazioni sull'endpoint OData e sulla chiave API.</span><span class="sxs-lookup"><span data-stu-id="438fc-114">Deploy the service to production, and obtain the API Key and OData endpoint information.</span></span>
3. <span data-ttu-id="438fc-115">Usare l'URL del servizio Web pubblicato per la pubblicazione in [Azure Marketplace](https://publish.windowsazure.com/workspace/)</span><span class="sxs-lookup"><span data-stu-id="438fc-115">Use the URL of the published web service to publish to [Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span></span> 
4. <span data-ttu-id="438fc-116">Una volta inviata, l'offerta viene esaminata e deve essere approvata prima che i clienti possano iniziare ad acquistarla.</span><span class="sxs-lookup"><span data-stu-id="438fc-116">Once submitted, your offer is reviewed and needs to be approved before your customers can start purchasing it.</span></span> <span data-ttu-id="438fc-117">La procedura di pubblicazione può richiedere alcuni giorni lavorativi.</span><span class="sxs-lookup"><span data-stu-id="438fc-117">The publishing process can take a few business days.</span></span> 

## <a name="walk-through"></a><span data-ttu-id="438fc-118">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="438fc-118">Walk through</span></span>
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a><span data-ttu-id="438fc-119">Passaggio 1: Creare e pubblicare un servizio di richiesta-risposta di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="438fc-119">Step 1: Create and publish a Machine Learning Request-Response service (RRS)</span></span>
 <span data-ttu-id="438fc-120">Se non è già stato fatto, vedere questa [procedura dettagliata](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="438fc-120">If you have not done this already, please take a look at this [walk through](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

### <a name="step-2-deploy-the-service-to-production-and-obtain-the-api-key-and-odata-endpoint-information"></a><span data-ttu-id="438fc-121">Passaggio 2: Distribuire il servizio in produzione e ottenere le informazioni sull'endpoint OData e sulla chiave API.</span><span class="sxs-lookup"><span data-stu-id="438fc-121">Step 2: Deploy the service to production, and obtain the API Key and OData endpoint information</span></span>
1. <span data-ttu-id="438fc-122">Nel [portale di Azure classico](http://manage.windowsazure.com)selezionare l'opzione **MACHINE LEARNING** nella barra di spostamento a sinistra e quindi selezionare l'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="438fc-122">From the [Azure Classic Portal](http://manage.windowsazure.com), select the **MACHINE LEARNING** option from the left navigation bar, and select your workspace.</span></span> 
2. <span data-ttu-id="438fc-123">Fare clic sulla scheda **WEB SERVICES** e selezionare il servizio Web che si vuole pubblicare nel Marketplace.</span><span class="sxs-lookup"><span data-stu-id="438fc-123">Click on the **WEB SERVICES** tab, and select the web service you would like to publish to the marketplace.</span></span>
   
    ![Azure Marketplace][workspace]
3. <span data-ttu-id="438fc-125">Selezionare l'endpoint che dovrà essere utilizzato nel Marketplace.</span><span class="sxs-lookup"><span data-stu-id="438fc-125">Select the endpoint you would like to have the marketplace consume.</span></span> <span data-ttu-id="438fc-126">Se non sono ancora stati creati endpoint aggiuntivi, è possibile selezionare l'endpoint **Default** .</span><span class="sxs-lookup"><span data-stu-id="438fc-126">If you have not created any additional endpoints, you can select the **Default** endpoint.</span></span>
4. <span data-ttu-id="438fc-127">Dopo avere fatto clic sull'endpoint, si potrà visualizzare **API KEY**.</span><span class="sxs-lookup"><span data-stu-id="438fc-127">Once you have clicked on the endpoint, you will be able to see the **API KEY**.</span></span> <span data-ttu-id="438fc-128">Copiare la chiave, perché queste informazioni saranno necessarie in seguito nel passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="438fc-128">You will need this piece of information later on in Step 3, so make a copy of it.</span></span>
   
    ![Azure Marketplace][apikey]
5. <span data-ttu-id="438fc-130">Fare clic sul metodo **REQUEST/RESPONSE**. Al momento, non è supportata la pubblicazione di servizi di esecuzione batch nel Marketplace.</span><span class="sxs-lookup"><span data-stu-id="438fc-130">Click on the **REQUEST/RESPONSE** method, at this point we do not support publishing batch execution services to the marketplace.</span></span> <span data-ttu-id="438fc-131">Verrà visualizzata la pagina della Guida per l'API relativa al metodo Request/Response.</span><span class="sxs-lookup"><span data-stu-id="438fc-131">That will take you to the API help page for the Request/Response method.</span></span>
6. <span data-ttu-id="438fc-132">Copiare l'indirizzo disponibile in **OData Endpoint Address** (Indirizzo endpoint OData). Queste informazioni saranno necessarie in seguito nel passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="438fc-132">Copy the **OData Endpoint Address**, you will need this information later on in Step 3.</span></span>
   
    ![Azure Marketplace][odata]

<span data-ttu-id="438fc-134">distribuire il servizio in produzione.</span><span class="sxs-lookup"><span data-stu-id="438fc-134">deploy the service into production.</span></span>

### <a name="step-3-use-the-url-of-the-published-web-service-to-publish-to-azure-marketplace-datamarket"></a><span data-ttu-id="438fc-135">Passaggio 3: Usare l'URL del servizio Web pubblicato per la pubblicazione in Azure Marketplace (store online per dati)</span><span class="sxs-lookup"><span data-stu-id="438fc-135">Step 3: Use the URL of the published web service to publish to Azure Marketplace (DataMarket)</span></span>
1. <span data-ttu-id="438fc-136">Passare ad [Azure Marketplace (store online per dati)](http://datamarket.azure.com/home)</span><span class="sxs-lookup"><span data-stu-id="438fc-136">Navigate to [Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span></span> 
2. <span data-ttu-id="438fc-137">Fare clic sul collegamento **Pubblica** nella parte superiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="438fc-137">Click on the **Publish** link at the top of the page.</span></span> <span data-ttu-id="438fc-138">Verrà visualizzato il [portale di pubblicazione di Microsoft Azure](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="438fc-138">This will take you to the [Microsoft Azure Publishing Portal](https://publish.windowsazure.com)</span></span>
3. <span data-ttu-id="438fc-139">Fare clic sulla sezione **editori** per registrarsi come editore.</span><span class="sxs-lookup"><span data-stu-id="438fc-139">Click on the **publishers** section to register as a publisher.</span></span>
4. <span data-ttu-id="438fc-140">Quando si crea una nuova offerta, selezionare **Servizi dati**, quindi fare clic su **Crea un nuovo documento di servizio dati**.</span><span class="sxs-lookup"><span data-stu-id="438fc-140">When creating a new offer, select **Data Services**, then click **Create a New Data Service**.</span></span> 
   
   ![Azure Marketplace][image1]
   
   <br />
5. <span data-ttu-id="438fc-142">In **Piani** fornire le informazioni relative all'offerta, incluso un piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="438fc-142">Under **Plans** provide information on your offering, including a pricing plan.</span></span> <span data-ttu-id="438fc-143">Decidere se offrire un servizio gratuito o a pagamento.</span><span class="sxs-lookup"><span data-stu-id="438fc-143">Decide if you will offer a free or paid service.</span></span> <span data-ttu-id="438fc-144">Nel caso di un servizio a pagamento, fornire i dati per il pagamento, come le coordinate bancarie e le informazioni fiscali.</span><span class="sxs-lookup"><span data-stu-id="438fc-144">To get paid, provide payment information such as your bank and tax information.</span></span>
6. <span data-ttu-id="438fc-145">In **Marketing** fornire le informazioni relative all'offerta, ad esempio il titolo e una descrizione dell'offerta.</span><span class="sxs-lookup"><span data-stu-id="438fc-145">Under **Marketing** provide information about your offer, such as the title and description for your offer.</span></span>
7. <span data-ttu-id="438fc-146">In **Prezzi** è possibile impostare il prezzo dei piani per paesi specifici o consentire al sistema di applicare un prezzo automatico all'offerta.</span><span class="sxs-lookup"><span data-stu-id="438fc-146">Under **Pricing** you can set the price for your plans for specific countries, or let the system "autoprice" your offer.</span></span>
8. <span data-ttu-id="438fc-147">Nella scheda **Servizio dati** fare clic su **Servizio Web** come **Origine dati**.</span><span class="sxs-lookup"><span data-stu-id="438fc-147">On the **Data Service** tab, click **Web Service** as the **Data Source**.</span></span>
   
    ![Azure Marketplace][image2]
9. <span data-ttu-id="438fc-149">Ottenere l'URL del servizio Web e la chiave API dal portale di Azure classico, come descritto nel passaggio 2 precedente.</span><span class="sxs-lookup"><span data-stu-id="438fc-149">Get the web service URL and API key from the Azure Classic Portal, as explained in step 2 above.</span></span>
10. <span data-ttu-id="438fc-150">Nella finestra di dialogo di configurazione del servizio dati del Marketplace incollare l'indirizzo dell'endpoint OData nella casella **URL servizio** .</span><span class="sxs-lookup"><span data-stu-id="438fc-150">In the Marketplace Data Service setup dialog box, paste the OData endpoint address into the **Service URL** text box.</span></span>
11. <span data-ttu-id="438fc-151">Per **Autenticazione** scegliere **Intestazione** come **Schema autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="438fc-151">For **Authentication**, choose **Header** as the **Authentication Scheme**.</span></span>
    
    * <span data-ttu-id="438fc-152">Immettere "Autorizzazione" per **Nome intestazione**.</span><span class="sxs-lookup"><span data-stu-id="438fc-152">Enter "Authorization" for the **Header Name**.</span></span>
    * <span data-ttu-id="438fc-153">Per **Valore intestazione** immettere "Portante" (senza virgolette), fare clic sulla **BARRA SPAZIATRICE** e quindi incollare la chiave API.</span><span class="sxs-lookup"><span data-stu-id="438fc-153">For the **Header Value**, enter "Bearer" (without the quotation marks), click the **Space** bar, and then paste the API key.</span></span>
    * <span data-ttu-id="438fc-154">Selezionare la casella di controllo **Questo servizio è OData** .</span><span class="sxs-lookup"><span data-stu-id="438fc-154">Select the **This Service is OData** check box.</span></span>
    * <span data-ttu-id="438fc-155">Fare clic su **Test connessione** per testare la connessione.</span><span class="sxs-lookup"><span data-stu-id="438fc-155">Click **Test Connection** to test the connection.</span></span>
12. <span data-ttu-id="438fc-156">In **Categorie** assicurarsi che sia selezionata l'opzione **Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="438fc-156">Under **Categories**, ensure **Machine Learning** is selected.</span></span>
13. <span data-ttu-id="438fc-157">Dopo avere completato l'immissione di tutti i metadati dell'offerta, fare clic su **Publish** e quindi su **Push to Staging** (Esegui push a staging).</span><span class="sxs-lookup"><span data-stu-id="438fc-157">When you are done entering all the metadata about your offer, click on **Publish**, and then **Push to Staging**.</span></span> <span data-ttu-id="438fc-158">A questo punto si verrà informati della presenza di eventuali problemi rimanenti da correggere.</span><span class="sxs-lookup"><span data-stu-id="438fc-158">At this point, you will be notified of any remaining issues that you need to fix.</span></span>
14. <span data-ttu-id="438fc-159">Dopo avere verificato il completamento di tutti i problemi in sospeso, fare clic su **Approvazione richiesta per push in produzione**.</span><span class="sxs-lookup"><span data-stu-id="438fc-159">After you have ensured completion of all the outstanding issues, click on **Request approval to push to Production**.</span></span> <span data-ttu-id="438fc-160">La procedura di pubblicazione può richiedere alcuni giorni lavorativi.</span><span class="sxs-lookup"><span data-stu-id="438fc-160">The publishing process can take a few business days.</span></span> 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

