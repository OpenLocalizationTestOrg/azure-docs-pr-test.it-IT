---
title: Guida alla creazione di un servizio dati per il Marketplace | Documentazione Microsoft
description: Istruzioni dettagliate su come creare, certificare e distribuire un servizio dati per l'acquisto in Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 96194198-6991-43b4-918e-ee337e250339
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: c0c9362f1c2e15c947aaaf7187f3383ad243140f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="data-service-publishing-guide-for-the-azure-marketplace"></a><span data-ttu-id="71bdf-103">Guida alla pubblicazione del servizio dati per Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="71bdf-103">Data Service Publishing Guide for the Azure Marketplace</span></span>
> [!IMPORTANT]
> <span data-ttu-id="71bdf-104">**In questo momento non stiamo più caricando nuovi editori di servizi dati. I nuovi servizi dati non saranno approvati per l'elencazione.**</span><span class="sxs-lookup"><span data-stu-id="71bdf-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="71bdf-105">Se si dispone di un'applicazione aziendale SaaS che si vuole pubblicare in AppSource, è possibile trovare altre informazioni [qui](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="71bdf-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="71bdf-106">Se si dispone di un'applicazione IaaS o di un servizio per gli sviluppatori che si vuole pubblicare in Azure Marketplace, è possibile trovare altre informazioni [qui](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="71bdf-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="71bdf-107">Dopo aver completato il passaggio 1, [Creazione e registrazione dell'account](marketplace-publishing-accounts-creation-registration.md), sono state fornite indicazioni sui [requisiti generali non tecnici](marketplace-publishing-pre-requisites.md) e [tecnici](marketplace-publishing-data-service-creation-prerequisites.md) delle offerte di servizi dati in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="71bdf-107">After completing the step 1, [Account Creation and Registration](marketplace-publishing-accounts-creation-registration.md), we guided you through the [General Non-Technical](marketplace-publishing-pre-requisites.md) and [Technical Requirements](marketplace-publishing-data-service-creation-prerequisites.md) of a Data Service offer on Azure Marketplace.</span></span> <span data-ttu-id="71bdf-108">Ora verranno illustrati i passaggi per la creazione di un'offerta di servizio dati nel [portale di pubblicazione][link-pubportal] per Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="71bdf-108">Now we will walk you through the steps for creating a Data Service offer on the [Publishing Portal][link-pubportal] for the Azure Marketplace.</span></span>

## <a name="1----login-to-the-publishing-portal"></a><span data-ttu-id="71bdf-109">1.    Accedere al portale di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="71bdf-109">1.    Login to the Publishing Portal.</span></span>
<span data-ttu-id="71bdf-110">Passare alla pagina [https://publish.windowsazure.com](https://publish.windowsazure.com.)</span><span class="sxs-lookup"><span data-stu-id="71bdf-110">Go to [https://publish.windowsazure.com](https://publish.windowsazure.com.)</span></span>

<span data-ttu-id="71bdf-111">**Per il primo accesso al portale di pubblicazione, usare lo stesso account con cui è stato registrato il profilo venditore della società nel Centro per sviluppatori.**</span><span class="sxs-lookup"><span data-stu-id="71bdf-111">**For first time login to Publishing Portal, use the same account with which your company’s Seller Profile was registered in Developer Center.**</span></span>  <span data-ttu-id="71bdf-112">(Successivamente è possibile aggiungere qualsiasi dipendente della società come coamministratore nel portale di pubblicazione).</span><span class="sxs-lookup"><span data-stu-id="71bdf-112">(Later you can add any employee of your company as a co-admin in the Publishing Portal).</span></span>

<span data-ttu-id="71bdf-113">Fare clic sul riquadro **Pubblica servizi dati** se si tratta del primo accesso al portale di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="71bdf-113">Click on the **Publish a Data Services** tile if this is the first login into the publishing portal.</span></span>

## <a name="2----choose-data-services-in-the-navigation-menu-on-the-left-side"></a><span data-ttu-id="71bdf-114">2.    Selezionare **Servizi dati** nel menu di navigazione a sinistra.</span><span class="sxs-lookup"><span data-stu-id="71bdf-114">2.    Choose **Data Services** in the navigation menu on the left side.</span></span>
  ![disegno](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a><span data-ttu-id="71bdf-116">3.    Creare un nuovo servizio dati</span><span class="sxs-lookup"><span data-stu-id="71bdf-116">3.    Create a New Data Service</span></span>
<span data-ttu-id="71bdf-117">Immettere il titolo per l'offerta del nuovo servizio, fare clic su "+" a destra.</span><span class="sxs-lookup"><span data-stu-id="71bdf-117">Fill in the title for your new Data Service Offer and click on “+” on the right.</span></span>

  ![disegno](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-the-sub-menu-under-the-newly-created-data-service-in-the-navigation-menu"></a><span data-ttu-id="71bdf-119">4.    Esaminare il sottomenu relativo al servizio dati appena creato nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="71bdf-119">4.    Review the sub-menu under the newly created Data Service in the navigation menu.</span></span>
<span data-ttu-id="71bdf-120">Fare clic sulla scheda **Procedura dettagliata** ed esaminare tutti i passaggi necessari per pubblicare correttamente il servizio dati in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="71bdf-120">Click on the **Walkthrough** tab and review all necessary steps needed to publish properly the Data Service on the Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="71bdf-121">È sempre possibile fare clic sui collegamenti nella pagina "Procedura dettagliata" o utilizzare schede nel sottomenu dell'offerta del servizio dati sul lato sinistro.</span><span class="sxs-lookup"><span data-stu-id="71bdf-121">You always can click on the links in the “Walkthrough” page or use tabs on the Data Service offer’s sub-menu on the left side.</span></span>
> 
> 

## <a name="5----create-a-new-plan"></a><span data-ttu-id="71bdf-122">5.    Creare un nuovo piano.</span><span class="sxs-lookup"><span data-stu-id="71bdf-122">5.    Create a new Plan.</span></span>
### <a name="offers-plans-transactions"></a><span data-ttu-id="71bdf-123">Offerte, piani, transazioni.</span><span class="sxs-lookup"><span data-stu-id="71bdf-123">Offers, Plans, transactions.</span></span>
<span data-ttu-id="71bdf-124">Ciascuna offerta può contenere più piani, tuttavia è necessario disporre di almeno un (1) piano.</span><span class="sxs-lookup"><span data-stu-id="71bdf-124">Each Offer can have multiple Plans, but must have at least one (1) Plan.</span></span> <span data-ttu-id="71bdf-125">La sottoscrizione da parte degli utenti riguarda uno dei piani dell'offerta.</span><span class="sxs-lookup"><span data-stu-id="71bdf-125">When end-users subscribe to your offer they subscribe for one of the offer’s Plan.</span></span> <span data-ttu-id="71bdf-126">Ciascun piano definisce il modo in cui gli utenti finali potranno utilizzare il servizio.</span><span class="sxs-lookup"><span data-stu-id="71bdf-126">Each plan defines how end-users will be able to use your service.</span></span>

<span data-ttu-id="71bdf-127">Al momento Azure Marketplace supporta solo il modello basato su transazioni di sottoscrizione mensile per i servizi dati, ad esempio l'utente finale pagherà un canone mensile in base al prezzo del piano specifico sottoscritto e potrà usufruire del numero di transazioni previsto dal piano su base mensile.</span><span class="sxs-lookup"><span data-stu-id="71bdf-127">Currently Azure Marketplace support only Monthly Subscription Transaction Based model for Data Services, i.e. end-users will pay monthly fee according to the price of the specific plan they subscribed to and will be able to consume each month number of transaction defined by the plan.</span></span>

<span data-ttu-id="71bdf-128">Di solito, ciascuna transazione viene definita come il numero di record restituiti dal servizio dati in base alla query inviata al servizio.</span><span class="sxs-lookup"><span data-stu-id="71bdf-128">Each Transaction usually defined as number of records your Data Service will return based on the query sent to the Service.</span></span> <span data-ttu-id="71bdf-129">Il valore predefinito è 100.</span><span class="sxs-lookup"><span data-stu-id="71bdf-129">The default is 100.</span></span> <span data-ttu-id="71bdf-130">Il numero di transazioni restituite per ciascuna query corrisponde al numero di record diviso per 100 e arrotondato per eccesso al numero intero più vicino.</span><span class="sxs-lookup"><span data-stu-id="71bdf-130">Number of transactions returned to each query will be number of records divided by 100 and rounded up to the closest integer.</span></span>

<span data-ttu-id="71bdf-131">Il monitoraggio (misurazione) del numero di transazioni utilizzate da ciascuna query è responsabilità del livello di servizio di Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="71bdf-131">It’s Azure Marketplace Service layer responsibility to monitor (meter) number of transactions consumed by each query.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="71bdf-132">Gli utenti finali che hanno raggiunto il limite delle transazioni durante il mese non potranno continuare a usare il servizio fino alla fine del relativo ciclo di sottoscrizione mensile.</span><span class="sxs-lookup"><span data-stu-id="71bdf-132">End-Users which reached the transaction limit during the month will be blocked from continuing to use the service until end of their monthly subscription cycle.</span></span>
> 
> <span data-ttu-id="71bdf-133">Facoltativamente, il piano o uno dei piani possono comprendere un numero illimitato di transazioni.</span><span class="sxs-lookup"><span data-stu-id="71bdf-133">The plan or one of the plans can (but not must) include unlimited number of transactions.</span></span>
> 
> 

### <a name="create-a-plan"></a><span data-ttu-id="71bdf-134">Creare un piano.</span><span class="sxs-lookup"><span data-stu-id="71bdf-134">Create a plan.</span></span>
1. <span data-ttu-id="71bdf-135">Fare clic su **"+"** accanto a "Aggiungi un nuovo piano".</span><span class="sxs-lookup"><span data-stu-id="71bdf-135">Click on **“+”** next to the “Add a new plan”.</span></span>
2. <span data-ttu-id="71bdf-136">Selezionare una delle opzioni: uso **Senza limiti** o **Limitato** per questo piano.</span><span class="sxs-lookup"><span data-stu-id="71bdf-136">Choose one of the options: **Unlimited** or **Limited** usage for this plan.</span></span>  <span data-ttu-id="71bdf-137">Se si seleziona Limitato, indicare il numero di transazioni mensili consentito dal piano.</span><span class="sxs-lookup"><span data-stu-id="71bdf-137">If Limited then provide the number of transaction the plan will allow to consume in a month.</span></span>
   
    ![disegno](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    <span data-ttu-id="71bdf-139">Il portale di pubblicazione suggerirà anche un "identificatore del piano", utilizzato per comunicare agli utenti finali il nome del piano nell'interfaccia utente e utilizzato dal servizio del Marketplace per identificarlo.</span><span class="sxs-lookup"><span data-stu-id="71bdf-139">Publishing Portal will also suggest “Plan Identifier”, which will be used to communicate to the end-users the name of the plan in the UI and also used by the Market Place Service to identify the Plan.</span></span> <span data-ttu-id="71bdf-140">Facoltativamente, è possibile modificare tale identificatore.</span><span class="sxs-lookup"><span data-stu-id="71bdf-140">You can change the “Plan Identifier” if you want.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="71bdf-141">L'identificatore del piano deve essere univoco all'interno dell'ambito di ciascuna offerta.</span><span class="sxs-lookup"><span data-stu-id="71bdf-141">The “Plan Identifier” must be unique within the scope of each offer.</span></span> <span data-ttu-id="71bdf-142">Come molti altri identificatori utilizzati nel portale di pubblicazione, l'identificatore del piano verrà bloccato dopo la prima pubblicazione prodotta e non sarà più modificabile.</span><span class="sxs-lookup"><span data-stu-id="71bdf-142">As many other Identifiers used in the Publishing Portal Plan identifier will be locked after the first publishing to production and you will not be able to change this identifier.</span></span>
   > 
   > 
3. <span data-ttu-id="71bdf-143">Fare clic per confermare la scelta.</span><span class="sxs-lookup"><span data-stu-id="71bdf-143">Click to accept your choice.</span></span>
4. <span data-ttu-id="71bdf-144">Verranno quindi poste alcune domande aggiuntive circa il piano appena creato.</span><span class="sxs-lookup"><span data-stu-id="71bdf-144">Then you will be asked few additional questions regarding your newly created Plan.</span></span>
   
    ![disegno](media/marketplace-publishing-data-service-creation/step-5.2.png)

| <span data-ttu-id="71bdf-146">Domanda</span><span class="sxs-lookup"><span data-stu-id="71bdf-146">Question</span></span> | <span data-ttu-id="71bdf-147">Significato</span><span class="sxs-lookup"><span data-stu-id="71bdf-147">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="71bdf-148">**Il piano è gratuito e disponibile tutto il mondo?**</span><span class="sxs-lookup"><span data-stu-id="71bdf-148">**This Plan is free and available world-wide?**</span></span> |<span data-ttu-id="71bdf-149">È possibile creare un piano completamente gratuito.</span><span class="sxs-lookup"><span data-stu-id="71bdf-149">You can create a completely free-of-charge plan.</span></span> <span data-ttu-id="71bdf-150">Se si tratta dell'unico piano di questa offerta, verrà pubblicata un'offerta gratuita in Marketplace.</span><span class="sxs-lookup"><span data-stu-id="71bdf-150">If it’s the only plan for this offer – it means that you are publishing “Free Offer” in the Marketplace.</span></span> <span data-ttu-id="71bdf-151">Se si tratta solo di uno di alcuni piani, sarà possibile offrire agli utenti finali per ulteriori informazioni sul servizio con un numero relativamente ridotto di transazioni mensili.</span><span class="sxs-lookup"><span data-stu-id="71bdf-151">If it’s only for one (of few) Plan, the it gives you an option to offer end-users to learn more about your service with a relatively small number of transactions per month.</span></span>  <span data-ttu-id="71bdf-152">Se la risposta è "Sì", non verranno poste ulteriori domande.</span><span class="sxs-lookup"><span data-stu-id="71bdf-152">If the answer is "Yes," then no further questions will be asked.</span></span> |

> [!NOTE]
> <span data-ttu-id="71bdf-153">Gli utenti finali possono effettuare l'aggiornamento ai piani a pagamento.</span><span class="sxs-lookup"><span data-stu-id="71bdf-153">End users can always upgrade to the paid plans.</span></span>
> 
> 

| <span data-ttu-id="71bdf-154">Domanda</span><span class="sxs-lookup"><span data-stu-id="71bdf-154">Question</span></span> | <span data-ttu-id="71bdf-155">Significato</span><span class="sxs-lookup"><span data-stu-id="71bdf-155">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="71bdf-156">**È disponibile una versione di prova gratuita?**</span><span class="sxs-lookup"><span data-stu-id="71bdf-156">**Is free trial available?**</span></span> |<span data-ttu-id="71bdf-157">È possibile selezionare "Nessuna versione di prova" o fornire un'opzione per utilizzare il piano per "Un mese".</span><span class="sxs-lookup"><span data-stu-id="71bdf-157">You can choose between “No Trial” at all or give an option to use your Plan for “One Month”.</span></span> <span data-ttu-id="71bdf-158">Gli autori preferiscono questa opzione per offrire agli utenti finali la possibilità di scoprire i vantaggi dell'offerta mediante un mese di utilizzo gratuito.</span><span class="sxs-lookup"><span data-stu-id="71bdf-158">Publishers like to use this option to provide end-users the possibility to understand the benefits of the offer for free for one month.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="71bdf-159">Gli utenti finali potranno acquistare una versione di prova gratuita solo se hanno impostato uno strumento per i pagamenti, ad esempio una carta di credito, un contratto aziendale ecc.</span><span class="sxs-lookup"><span data-stu-id="71bdf-159">End-users will only be able to purchase a free trial if they have established payment instrument e.g. credit card, enterprise agreement.</span></span>
> 
> <span data-ttu-id="71bdf-160">Dopo un mese di prova gratuita, Azure Marketplace addebiterà ai clienti il prezzo a partire dalla data della sottoscrizione, a meno che il cliente non abbia richiesto l'annullamento della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="71bdf-160">After one month of the free trial, Azure Marketplace will start charging customers the price as of the date of the subscription, unless the customer initiated the subscription cancellation.</span></span> <span data-ttu-id="71bdf-161">Gli utenti finali non riceveranno alcuna particolare notifica.</span><span class="sxs-lookup"><span data-stu-id="71bdf-161">No special notification will be provided to the end-users.</span></span>
> 
> 

| <span data-ttu-id="71bdf-162">Domanda</span><span class="sxs-lookup"><span data-stu-id="71bdf-162">Question</span></span> | <span data-ttu-id="71bdf-163">Significato</span><span class="sxs-lookup"><span data-stu-id="71bdf-163">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="71bdf-164">**Il piano richiede un codice di promozione per l'acquisto?**</span><span class="sxs-lookup"><span data-stu-id="71bdf-164">**This plan requires a promotion code to purchase?**</span></span> |<span data-ttu-id="71bdf-165">Gli autori hanno la possibilità di limitare l'accesso ai propri piani di servizio fornendo un codice speciale, noto come "codice di promozione", a determinati clienti.</span><span class="sxs-lookup"><span data-stu-id="71bdf-165">Publishers have an option to limit access to their Service Plans by providing a special code, called “A Promocode” to specific customers.</span></span> <span data-ttu-id="71bdf-166">Solo gli utenti finali che dispongono di tale codice di promozione potranno sottoscrivere il piano.</span><span class="sxs-lookup"><span data-stu-id="71bdf-166">Only end-users which will have this Promocode will be able to subscribe to the Plan.</span></span> <span data-ttu-id="71bdf-167">Se si seleziona "No", si accetta che tutti gli utenti dall'area in cui l'offerta è disponibile (vedere [Guida ai contenuti marketing nel Marketplace](marketplace-publishing-push-to-staging.md) per ulteriori dettagli) potranno sottoscrivere il piano.</span><span class="sxs-lookup"><span data-stu-id="71bdf-167">If you choose “No”, then you agree that everyone from the region where the offer is available (See [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) for more details) will be able to subscribe to this plan.</span></span> <span data-ttu-id="71bdf-168">Non verranno poste ulteriori domande.</span><span class="sxs-lookup"><span data-stu-id="71bdf-168">No further questions will be asked.</span></span> |
| <span data-ttu-id="71bdf-169">**Nascondere anche il piano a tutti gli utenti che non dispongono di un codice di promozione valido?**</span><span class="sxs-lookup"><span data-stu-id="71bdf-169">**Also hide this plan from anyone who doesn’t have a valid promotion code?**</span></span> |<span data-ttu-id="71bdf-170">Se la risposta alla domanda precedente è "Sì", l'autore può anche rimuovere completamente il piano dalla visualizzazione nell'interfaccia utente del Marketplace.</span><span class="sxs-lookup"><span data-stu-id="71bdf-170">If the answer to the previous question is “Yes” the Publisher has an option to completely remove this plan from appearing in the UI of the Marketplace.</span></span> <span data-ttu-id="71bdf-171">Ciò significa che i clienti non visualizzeranno il piano nella pagina dei dettagli dell'offerta.</span><span class="sxs-lookup"><span data-stu-id="71bdf-171">It means, customers will not see this plan in the Offer’s details page.</span></span> <span data-ttu-id="71bdf-172">Gli utenti finali che riceveranno un codice di promozione per l'acquisto potranno effettuare la sottoscrizione tramite tale codice.</span><span class="sxs-lookup"><span data-stu-id="71bdf-172">End-users which will receive a promocode to purchase it, will be able to subscribe to it using this promocode.</span></span> |

## <a name="6----create-your-marketplace-marketing-content"></a><span data-ttu-id="71bdf-173">6.    Creare contenuti di marketing di Marketplace</span><span class="sxs-lookup"><span data-stu-id="71bdf-173">6.    Create your Marketplace marketing content</span></span>
<span data-ttu-id="71bdf-174">Per dettagli su come fornire le informazioni necessarie nelle schede **Marketing, Prezzi, Supporto e Categorie** , visitare la [Guida ai contenuti marketing nel Marketplace](marketplace-publishing-push-to-staging.md) che è comune a tutti gli elementi pubblicati in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="71bdf-174">For How to provide information required in **Marketing, Pricing, Support and Categories** tabs please visit [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) which is common to all artifacts published in the Azure Marketplace.</span></span>  

## <a name="7----connect-your-offer-to-your-service-sql-azure-based-or-web-service-based"></a><span data-ttu-id="71bdf-175">7.    Collegare l'offerta al servizio (basato su SQL Azure o su servizio Web).</span><span class="sxs-lookup"><span data-stu-id="71bdf-175">7.    Connect your offer to your Service (SQL Azure based or Web Service based).</span></span>
<span data-ttu-id="71bdf-176">Fare clic sul sottomenu **Servizi dati** .</span><span class="sxs-lookup"><span data-stu-id="71bdf-176">Click on the **Data Services** sub-menu.</span></span>

<span data-ttu-id="71bdf-177">Nella metà superiore della pagina verrà richiesto di indicare lo **spazio dei nomi**dell'offerta.</span><span class="sxs-lookup"><span data-stu-id="71bdf-177">On the upper half of the page you’ll be asked to provide the offer’s **Namespace**.</span></span>  

  ![disegno](media/marketplace-publishing-data-service-creation/step-7.png)

<span data-ttu-id="71bdf-179">La domanda seguente definirà in che modo l'autore esporrà l'offerta appena creata in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="71bdf-179">The below question will define how the Publisher is going to expose newly created offer to Azure Marketplace.</span></span> <span data-ttu-id="71bdf-180">(Per ulteriori informazioni, vedere la [Guida ai prerequisiti tecnici dei servizi dati](marketplace-publishing-data-service-creation-prerequisites.md)).</span><span class="sxs-lookup"><span data-stu-id="71bdf-180">(For more details see the [Data Services Technical Prerequisite Guide](marketplace-publishing-data-service-creation-prerequisites.md)).</span></span>

  ![disegno](media/marketplace-publishing-data-service-creation/step-7.2.png)

<span data-ttu-id="71bdf-182">**Pubblicazione del servizio basato su database**</span><span class="sxs-lookup"><span data-stu-id="71bdf-182">**Publishing the Database based service**</span></span>

<span data-ttu-id="71bdf-183">Fare clic su **Database**.</span><span class="sxs-lookup"><span data-stu-id="71bdf-183">Click on **Database**.</span></span> <span data-ttu-id="71bdf-184">Verrà visualizzata la pagina seguente:</span><span class="sxs-lookup"><span data-stu-id="71bdf-184">The following page will appear:</span></span>

  ![disegno](media/marketplace-publishing-data-service-creation/step-7.3.png)

<span data-ttu-id="71bdf-186">Per creare un mapping CSDL per il set di dati basato su database di SQL Azure:</span><span class="sxs-lookup"><span data-stu-id="71bdf-186">To create a CSDL mapping for the Dataset based on the SQL Azure DB:</span></span>

  ![disegno](media/marketplace-publishing-data-service-creation/step-7.4.png)

<span data-ttu-id="71bdf-188">E quindi per ciascuna tabella</span><span class="sxs-lookup"><span data-stu-id="71bdf-188">And then for each table</span></span>

  ![disegno](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![disegno](media/marketplace-publishing-data-service-creation/step-7.6.png)

<span data-ttu-id="71bdf-191">Se il servizio Web</span><span class="sxs-lookup"><span data-stu-id="71bdf-191">If Web Service</span></span>

  ![disegno](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> <span data-ttu-id="71bdf-193">Leggere [Mapping di un servizio Web esistente in OData tramite CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) per istruzioni dettagliate ed esempi sulla creazione di un servizio Web CSDL.</span><span class="sxs-lookup"><span data-stu-id="71bdf-193">Read [Mapping an existing web service to OData through CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) for detailed instructions and examples for creating a CSDL Web Service.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="71bdf-194">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="71bdf-194">Next Steps</span></span>
<span data-ttu-id="71bdf-195">Una volta creata l'offerta del servizio dati, verificare di aver completato le istruzioni della [guida ai contenuti di marketing nel Marketplace](marketplace-publishing-push-to-staging.md) prima di proseguire all'articolo [Testing your Data Service in Staging](marketplace-publishing-data-service-test-in-staging.md) (Test del servizio dati in staging).</span><span class="sxs-lookup"><span data-stu-id="71bdf-195">Now that you've created your Data Service offer, please ensure that you complete the instructions in the [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) before you move forward to [Testing your Data Service in Staging](marketplace-publishing-data-service-test-in-staging.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="71bdf-196">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="71bdf-196">See Also</span></span>
* [<span data-ttu-id="71bdf-197">Guida introduttiva: Come pubblicare un'offerta in Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="71bdf-197">Getting Started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* <span data-ttu-id="71bdf-198">Per apprendere il processo di mapping generale e lo scopo di OData , leggere questo articolo [Mapping di OData del servizio dati](marketplace-publishing-data-service-creation-odata-mapping.md) per esaminare le definizioni, le strutture e le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="71bdf-198">If you are interested in understanding the overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) to review definitions, structures, and instructions.</span></span>
* <span data-ttu-id="71bdf-199">Per ricevere formazione e informazioni sui nodi specifici e i relativi parametri, leggere l'articolo relativo ai [nodi di mapping di OData del servizio dati](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) per definizioni, spiegazioni, esempi e casi di utilizzo contestuali.</span><span class="sxs-lookup"><span data-stu-id="71bdf-199">If you are interested in learning and understanding the specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="71bdf-200">Per esaminare gli esempi, leggere questo articolo [Esempi di mapping di OData del servizio dati](marketplace-publishing-data-service-creation-odata-mapping-examples.md) per consultare il codice di esempio e apprendere la sintassi del codice e il contesto.</span><span class="sxs-lookup"><span data-stu-id="71bdf-200">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) to see sample code and understand code syntax and context.</span></span>

[link-pubportal]:https://publish.windowsazure.com
