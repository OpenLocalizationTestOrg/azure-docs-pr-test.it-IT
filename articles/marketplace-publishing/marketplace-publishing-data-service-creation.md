---
title: aaaGuide toocreating un servizio dati per hello Marketplace | Documenti Microsoft
description: Istruzioni dettagliate su come toocreate, certificare e distribuire un servizio dati per acquistano su hello Azure Marketplace.
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
ms.openlocfilehash: 0220d357ae0ec89e7d4f6399605850e57c646f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-service-publishing-guide-for-hello-azure-marketplace"></a><span data-ttu-id="e6e19-103">Guida alla pubblicazione dei dati del servizio per hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="e6e19-103">Data Service Publishing Guide for hello Azure Marketplace</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e6e19-104">**In questo momento non stiamo più caricando nuovi editori di servizi dati. I nuovi servizi dati non saranno approvati per l'elencazione.**</span><span class="sxs-lookup"><span data-stu-id="e6e19-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="e6e19-105">Se si dispone di un'applicazione SaaS di business si desidera toopublish in AppSource è possibile trovare ulteriori informazioni [qui](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="e6e19-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="e6e19-106">Se si utilizzano applicazioni IaaS sviluppatore del servizio si sarebbe ad esempio toopublish in Azure Marketplace è possibile trovare ulteriori informazioni [qui](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="e6e19-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="e6e19-107">Dopo aver completato il passaggio di hello 1, [la creazione di Account e la registrazione](marketplace-publishing-accounts-creation-registration.md), si è illustrate hello [generale tecnici](marketplace-publishing-pre-requisites.md) e [requisiti tecnici](marketplace-publishing-data-service-creation-prerequisites.md) di un servizio dati offrono in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e6e19-107">After completing hello step 1, [Account Creation and Registration](marketplace-publishing-accounts-creation-registration.md), we guided you through hello [General Non-Technical](marketplace-publishing-pre-requisites.md) and [Technical Requirements](marketplace-publishing-data-service-creation-prerequisites.md) of a Data Service offer on Azure Marketplace.</span></span> <span data-ttu-id="e6e19-108">Ora è verranno illustrati i passaggi di hello per la creazione di un'offerta di servizio dati su hello [portale pubblicazione] [ link-pubportal] per hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e6e19-108">Now we will walk you through hello steps for creating a Data Service offer on hello [Publishing Portal][link-pubportal] for hello Azure Marketplace.</span></span>

## <a name="1----login-toohello-publishing-portal"></a><span data-ttu-id="e6e19-109">1.    Account di accesso toohello portale di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="e6e19-109">1.    Login toohello Publishing Portal.</span></span>
<span data-ttu-id="e6e19-110">Andare troppo[https://publish.windowsazure.com](https://publish.windowsazure.com.)</span><span class="sxs-lookup"><span data-stu-id="e6e19-110">Go too[https://publish.windowsazure.com](https://publish.windowsazure.com.)</span></span>

<span data-ttu-id="e6e19-111">**Per prima tooPublishing di account di accesso a tempo portale, utilizzare hello stesso account con cui profilo venditore della società è stato registrato nel centro per sviluppatori.**</span><span class="sxs-lookup"><span data-stu-id="e6e19-111">**For first time login tooPublishing Portal, use hello same account with which your company’s Seller Profile was registered in Developer Center.**</span></span>  <span data-ttu-id="e6e19-112">(In un secondo momento è possibile aggiungere qualsiasi dipendente della società come co-amministratore in hello portale di pubblicazione).</span><span class="sxs-lookup"><span data-stu-id="e6e19-112">(Later you can add any employee of your company as a co-admin in hello Publishing Portal).</span></span>

<span data-ttu-id="e6e19-113">Fare clic su hello **pubblicare un servizi dati** espansa se si tratta di account di accesso prima hello nel portale di pubblicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e6e19-113">Click on hello **Publish a Data Services** tile if this is hello first login into hello publishing portal.</span></span>

## <a name="2----choose-data-services-in-hello-navigation-menu-on-hello-left-side"></a><span data-ttu-id="e6e19-114">2.    Scegliere **Data Services** nel menu di navigazione hello sul lato sinistro hello.</span><span class="sxs-lookup"><span data-stu-id="e6e19-114">2.    Choose **Data Services** in hello navigation menu on hello left side.</span></span>
  ![disegno](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a><span data-ttu-id="e6e19-116">3.    Creare un nuovo servizio dati</span><span class="sxs-lookup"><span data-stu-id="e6e19-116">3.    Create a New Data Service</span></span>
<span data-ttu-id="e6e19-117">Compilare per il nuovo servizio dati offrono titolo hello e fare clic su "+" su hello destra.</span><span class="sxs-lookup"><span data-stu-id="e6e19-117">Fill in hello title for your new Data Service Offer and click on “+” on hello right.</span></span>

  ![disegno](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-hello-sub-menu-under-hello-newly-created-data-service-in-hello-navigation-menu"></a><span data-ttu-id="e6e19-119">4.    Sottomenu hello revisione in hello appena creata servizio dati in menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="e6e19-119">4.    Review hello sub-menu under hello newly created Data Service in hello navigation menu.</span></span>
<span data-ttu-id="e6e19-120">Fare clic su hello **procedura dettagliata** scheda e di esaminare tutti i passaggi necessari esigenze toopublish hello correttamente il servizio dati su hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e6e19-120">Click on hello **Walkthrough** tab and review all necessary steps needed toopublish properly hello Data Service on hello Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="e6e19-121">È sempre possibile fare clic sui collegamenti hello nella pagina "Procedura dettagliata" hello o utilizzare schede di sottomenu dell'offerta di servizio dati hello sul lato sinistro di hello.</span><span class="sxs-lookup"><span data-stu-id="e6e19-121">You always can click on hello links in hello “Walkthrough” page or use tabs on hello Data Service offer’s sub-menu on hello left side.</span></span>
> 
> 

## <a name="5----create-a-new-plan"></a><span data-ttu-id="e6e19-122">5.    Creare un nuovo piano.</span><span class="sxs-lookup"><span data-stu-id="e6e19-122">5.    Create a new Plan.</span></span>
### <a name="offers-plans-transactions"></a><span data-ttu-id="e6e19-123">Offerte, piani, transazioni.</span><span class="sxs-lookup"><span data-stu-id="e6e19-123">Offers, Plans, transactions.</span></span>
<span data-ttu-id="e6e19-124">Ciascuna offerta può contenere più piani, tuttavia è necessario disporre di almeno un (1) piano.</span><span class="sxs-lookup"><span data-stu-id="e6e19-124">Each Offer can have multiple Plans, but must have at least one (1) Plan.</span></span> <span data-ttu-id="e6e19-125">Quando gli utenti finali di eseguire la sottoscrizione tooyour offerta sottoscrivono un piano dell'offerta hello.</span><span class="sxs-lookup"><span data-stu-id="e6e19-125">When end-users subscribe tooyour offer they subscribe for one of hello offer’s Plan.</span></span> <span data-ttu-id="e6e19-126">Ogni piano definisce come gli utenti finali potrà essere in grado di toouse il servizio.</span><span class="sxs-lookup"><span data-stu-id="e6e19-126">Each plan defines how end-users will be able toouse your service.</span></span>

<span data-ttu-id="e6e19-127">Attualmente Azure Marketplace supporta solo modello basato su transazioni di sottoscrizione mensile per i servizi dati, ad esempio gli utenti finali pagamento mensile in base a prezzo toohello del piano di hello specifico hanno eseguito la sottoscrizione tooand sarà in grado di tooconsume ogni numero di mese di transazione definito dal piano hello.</span><span class="sxs-lookup"><span data-stu-id="e6e19-127">Currently Azure Marketplace support only Monthly Subscription Transaction Based model for Data Services, i.e. end-users will pay monthly fee according toohello price of hello specific plan they subscribed tooand will be able tooconsume each month number of transaction defined by hello plan.</span></span>

<span data-ttu-id="e6e19-128">Ogni transazione, in genere definita come numero di record, che verrà restituito il servizio dati basato su query di hello inviato toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="e6e19-128">Each Transaction usually defined as number of records your Data Service will return based on hello query sent toohello Service.</span></span> <span data-ttu-id="e6e19-129">valore predefinito di Hello è 100.</span><span class="sxs-lookup"><span data-stu-id="e6e19-129">hello default is 100.</span></span> <span data-ttu-id="e6e19-130">Numero di transazioni restituiti tooeach query verrà numero di record diviso per 100 e arrotondato per eccesso toohello numero intero più vicino.</span><span class="sxs-lookup"><span data-stu-id="e6e19-130">Number of transactions returned tooeach query will be number of records divided by 100 and rounded up toohello closest integer.</span></span>

<span data-ttu-id="e6e19-131">Si tratta del servizio di Azure Marketplace livello responsabilità toomonitor (misuratore) numero di transazioni utilizzato da ogni query.</span><span class="sxs-lookup"><span data-stu-id="e6e19-131">It’s Azure Marketplace Service layer responsibility toomonitor (meter) number of transactions consumed by each query.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e6e19-132">Gli utenti finali che ha raggiunto il limite di transazione hello durante il mese di hello non potranno continuare servizio hello toouse fino al termine del loro ciclo di sottoscrizione mensile.</span><span class="sxs-lookup"><span data-stu-id="e6e19-132">End-Users which reached hello transaction limit during hello month will be blocked from continuing toouse hello service until end of their monthly subscription cycle.</span></span>
> 
> <span data-ttu-id="e6e19-133">Hello piano o uno dei piani di hello possibile (ma non necessario) includono un numero illimitato di transazioni.</span><span class="sxs-lookup"><span data-stu-id="e6e19-133">hello plan or one of hello plans can (but not must) include unlimited number of transactions.</span></span>
> 
> 

### <a name="create-a-plan"></a><span data-ttu-id="e6e19-134">Creare un piano.</span><span class="sxs-lookup"><span data-stu-id="e6e19-134">Create a plan.</span></span>
1. <span data-ttu-id="e6e19-135">Fare clic su **"+"** toohello successivo "aggiungere un nuovo piano".</span><span class="sxs-lookup"><span data-stu-id="e6e19-135">Click on **“+”** next toohello “Add a new plan”.</span></span>
2. <span data-ttu-id="e6e19-136">Scegliere una delle opzioni di hello: **Unlimited** o **limitato** utilizzo per questo piano.</span><span class="sxs-lookup"><span data-stu-id="e6e19-136">Choose one of hello options: **Unlimited** or **Limited** usage for this plan.</span></span>  <span data-ttu-id="e6e19-137">Se Limited quindi fornire il numero di hello del piano di hello transazione consentirà tooconsume in un mese.</span><span class="sxs-lookup"><span data-stu-id="e6e19-137">If Limited then provide hello number of transaction hello plan will allow tooconsume in a month.</span></span>
   
    ![disegno](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    <span data-ttu-id="e6e19-139">Portale di pubblicazione verrà inoltre indicare "Identificatore del piano", che sarà utilizzato toocommunicate toohello gli utenti finali hello nome di piano hello hello dell'interfaccia utente e anche usato dai hello tooidentify di mercato servizio hello piano.</span><span class="sxs-lookup"><span data-stu-id="e6e19-139">Publishing Portal will also suggest “Plan Identifier”, which will be used toocommunicate toohello end-users hello name of hello plan in hello UI and also used by hello Market Place Service tooidentify hello Plan.</span></span> <span data-ttu-id="e6e19-140">Se si desidera, è possibile modificare hello "Identificatore del piano".</span><span class="sxs-lookup"><span data-stu-id="e6e19-140">You can change hello “Plan Identifier” if you want.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e6e19-141">Hello "Identificatore del piano" deve essere univoco nell'ambito di hello di ogni offerta.</span><span class="sxs-lookup"><span data-stu-id="e6e19-141">hello “Plan Identifier” must be unique within hello scope of each offer.</span></span> <span data-ttu-id="e6e19-142">Come molti altri identificatori nell'hello pubblicazione portale pianificare identificatore sarà bloccato dopo hello prima tooproduction di pubblicazione e non saranno più in grado di toochange questo identificatore.</span><span class="sxs-lookup"><span data-stu-id="e6e19-142">As many other Identifiers used in hello Publishing Portal Plan identifier will be locked after hello first publishing tooproduction and you will not be able toochange this identifier.</span></span>
   > 
   > 
3. <span data-ttu-id="e6e19-143">Fare clic su tooaccept prescelto.</span><span class="sxs-lookup"><span data-stu-id="e6e19-143">Click tooaccept your choice.</span></span>
4. <span data-ttu-id="e6e19-144">Verranno quindi poste alcune domande aggiuntive circa il piano appena creato.</span><span class="sxs-lookup"><span data-stu-id="e6e19-144">Then you will be asked few additional questions regarding your newly created Plan.</span></span>
   
    ![disegno](media/marketplace-publishing-data-service-creation/step-5.2.png)

| <span data-ttu-id="e6e19-146">Domanda</span><span class="sxs-lookup"><span data-stu-id="e6e19-146">Question</span></span> | <span data-ttu-id="e6e19-147">Significato</span><span class="sxs-lookup"><span data-stu-id="e6e19-147">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="e6e19-148">**Il piano è gratuito e disponibile tutto il mondo?**</span><span class="sxs-lookup"><span data-stu-id="e6e19-148">**This Plan is free and available world-wide?**</span></span> |<span data-ttu-id="e6e19-149">È possibile creare un piano completamente gratuito.</span><span class="sxs-lookup"><span data-stu-id="e6e19-149">You can create a completely free-of-charge plan.</span></span> <span data-ttu-id="e6e19-150">Se è hello prevede solo per questa offerta – significa che si sta pubblicando "Offrono libero" in hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e6e19-150">If it’s hello only plan for this offer – it means that you are publishing “Free Offer” in hello Marketplace.</span></span> <span data-ttu-id="e6e19-151">Se è solo per un (numero) piano, hello consente di definire un toolearn gli utenti finali toooffer opzione ulteriori informazioni sul servizio con un numero relativamente ridotto di transazioni al mese.</span><span class="sxs-lookup"><span data-stu-id="e6e19-151">If it’s only for one (of few) Plan, hello it gives you an option toooffer end-users toolearn more about your service with a relatively small number of transactions per month.</span></span>  <span data-ttu-id="e6e19-152">Se la risposta hello è "Sì", non verranno richiesto alcun ulteriori domande.</span><span class="sxs-lookup"><span data-stu-id="e6e19-152">If hello answer is "Yes," then no further questions will be asked.</span></span> |

> [!NOTE]
> <span data-ttu-id="e6e19-153">Gli utenti finali possono aggiornare sempre toohello a pagamento di piani.</span><span class="sxs-lookup"><span data-stu-id="e6e19-153">End users can always upgrade toohello paid plans.</span></span>
> 
> 

| <span data-ttu-id="e6e19-154">Domanda</span><span class="sxs-lookup"><span data-stu-id="e6e19-154">Question</span></span> | <span data-ttu-id="e6e19-155">Significato</span><span class="sxs-lookup"><span data-stu-id="e6e19-155">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="e6e19-156">**È disponibile una versione di prova gratuita?**</span><span class="sxs-lookup"><span data-stu-id="e6e19-156">**Is free trial available?**</span></span> |<span data-ttu-id="e6e19-157">È possibile scegliere tra "Nessuna versione di valutazione" affatto o assegnare toouse un'opzione il piano per "Un mese".</span><span class="sxs-lookup"><span data-stu-id="e6e19-157">You can choose between “No Trial” at all or give an option toouse your Plan for “One Month”.</span></span> <span data-ttu-id="e6e19-158">I server di pubblicazione, ad esempio toouse questa opzione tooprovide gli utenti finali hello possibilità toounderstand hello vantaggi di hello offrono gratuitamente per un mese.</span><span class="sxs-lookup"><span data-stu-id="e6e19-158">Publishers like toouse this option tooprovide end-users hello possibility toounderstand hello benefits of hello offer for free for one month.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="e6e19-159">Gli utenti finali saranno in grado di toopurchase una valutazione gratuita solo se hanno stabilito di pagamento, ad esempio carta di credito, contratto enterprise agreement.</span><span class="sxs-lookup"><span data-stu-id="e6e19-159">End-users will only be able toopurchase a free trial if they have established payment instrument e.g. credit card, enterprise agreement.</span></span>
> 
> <span data-ttu-id="e6e19-160">Dopo un mese di valutazione gratuita di hello, Azure Marketplace inizierà ad addebitare i costi clienti prezzo hello data hello di sottoscrizione hello, a meno che il cliente hello avviata annullamento sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="e6e19-160">After one month of hello free trial, Azure Marketplace will start charging customers hello price as of hello date of hello subscription, unless hello customer initiated hello subscription cancellation.</span></span> <span data-ttu-id="e6e19-161">Non verranno fornito agli utenti finali toohello alcuna notifica speciale.</span><span class="sxs-lookup"><span data-stu-id="e6e19-161">No special notification will be provided toohello end-users.</span></span>
> 
> 

| <span data-ttu-id="e6e19-162">Domanda</span><span class="sxs-lookup"><span data-stu-id="e6e19-162">Question</span></span> | <span data-ttu-id="e6e19-163">Significato</span><span class="sxs-lookup"><span data-stu-id="e6e19-163">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="e6e19-164">**Il piano è richiesto un toopurchase codice promozione?**</span><span class="sxs-lookup"><span data-stu-id="e6e19-164">**This plan requires a promotion code toopurchase?**</span></span> |<span data-ttu-id="e6e19-165">I server di pubblicazione hanno un tootheir di accesso toolimit opzione piani di servizio, fornendo un codice speciale, denominato "Un codice promozione" toospecific clienti.</span><span class="sxs-lookup"><span data-stu-id="e6e19-165">Publishers have an option toolimit access tootheir Service Plans by providing a special code, called “A Promocode” toospecific customers.</span></span> <span data-ttu-id="e6e19-166">Solo gli utenti finali che conterrà il codice promozione sarà in grado di toosubscribe toohello piano.</span><span class="sxs-lookup"><span data-stu-id="e6e19-166">Only end-users which will have this Promocode will be able toosubscribe toohello Plan.</span></span> <span data-ttu-id="e6e19-167">Se si sceglie "No", quindi si accetta che tutti gli utenti dall'area hello in hello offerta è disponibili (vedere [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) per altri dettagli) sarà in grado di toosubscribe toothis piano.</span><span class="sxs-lookup"><span data-stu-id="e6e19-167">If you choose “No”, then you agree that everyone from hello region where hello offer is available (See [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) for more details) will be able toosubscribe toothis plan.</span></span> <span data-ttu-id="e6e19-168">Non verranno poste ulteriori domande.</span><span class="sxs-lookup"><span data-stu-id="e6e19-168">No further questions will be asked.</span></span> |
| <span data-ttu-id="e6e19-169">**Nascondere anche il piano a tutti gli utenti che non dispongono di un codice di promozione valido?**</span><span class="sxs-lookup"><span data-stu-id="e6e19-169">**Also hide this plan from anyone who doesn’t have a valid promotion code?**</span></span> |<span data-ttu-id="e6e19-170">Se hello risposta toohello precedente domanda "Yes" hello, server di pubblicazione contiene toocompletely un'opzione rimuovere questo piano venga visualizzato nell'interfaccia utente di hello Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="e6e19-170">If hello answer toohello previous question is “Yes” hello Publisher has an option toocompletely remove this plan from appearing in hello UI of hello Marketplace.</span></span> <span data-ttu-id="e6e19-171">Significa che, i clienti non visualizzeranno il piano nella pagina dei dettagli dell'offerta hello.</span><span class="sxs-lookup"><span data-stu-id="e6e19-171">It means, customers will not see this plan in hello Offer’s details page.</span></span> <span data-ttu-id="e6e19-172">Gli utenti finali che riceveranno toopurchase un codice promozione, sarà in grado di toosubscribe tooit tramite questo codice promozione.</span><span class="sxs-lookup"><span data-stu-id="e6e19-172">End-users which will receive a promocode toopurchase it, will be able toosubscribe tooit using this promocode.</span></span> |

## <a name="6----create-your-marketplace-marketing-content"></a><span data-ttu-id="e6e19-173">6.    Creare contenuti di marketing di Marketplace</span><span class="sxs-lookup"><span data-stu-id="e6e19-173">6.    Create your Marketplace marketing content</span></span>
<span data-ttu-id="e6e19-174">Per modalità tooprovide informazioni necessarie **Marketing, prezzi, supporto e le categorie** schede, visitare [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) che è comune tooall gli elementi pubblicati in hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e6e19-174">For How tooprovide information required in **Marketing, Pricing, Support and Categories** tabs please visit [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) which is common tooall artifacts published in hello Azure Marketplace.</span></span>  

## <a name="7----connect-your-offer-tooyour-service-sql-azure-based-or-web-service-based"></a><span data-ttu-id="e6e19-175">7.    Connettere il tooyour offerta di servizio (SQL Azure basato su o il servizio Web basato su).</span><span class="sxs-lookup"><span data-stu-id="e6e19-175">7.    Connect your offer tooyour Service (SQL Azure based or Web Service based).</span></span>
<span data-ttu-id="e6e19-176">Fare clic su hello **Data Services** sottomenu.</span><span class="sxs-lookup"><span data-stu-id="e6e19-176">Click on hello **Data Services** sub-menu.</span></span>

<span data-ttu-id="e6e19-177">Nella parte superiore hello pagina hello verrà chiesto di offerta di hello tooprovide **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="e6e19-177">On hello upper half of hello page you’ll be asked tooprovide hello offer’s **Namespace**.</span></span>  

  ![disegno](media/marketplace-publishing-data-service-creation/step-7.png)

<span data-ttu-id="e6e19-179">Hello seguito domanda definirà hello Publisher modalità tooexpose appena creati offerta tooAzure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e6e19-179">hello below question will define how hello Publisher is going tooexpose newly created offer tooAzure Marketplace.</span></span> <span data-ttu-id="e6e19-180">(Per ulteriori informazioni, vedere hello [Guida prerequisiti tecniche di Data Services](marketplace-publishing-data-service-creation-prerequisites.md)).</span><span class="sxs-lookup"><span data-stu-id="e6e19-180">(For more details see hello [Data Services Technical Prerequisite Guide](marketplace-publishing-data-service-creation-prerequisites.md)).</span></span>

  ![disegno](media/marketplace-publishing-data-service-creation/step-7.2.png)

<span data-ttu-id="e6e19-182">**Pubblicazione hello Database basato su servizio**</span><span class="sxs-lookup"><span data-stu-id="e6e19-182">**Publishing hello Database based service**</span></span>

<span data-ttu-id="e6e19-183">Fare clic su **Database**.</span><span class="sxs-lookup"><span data-stu-id="e6e19-183">Click on **Database**.</span></span> <span data-ttu-id="e6e19-184">verrà visualizzata la seguente pagina Hello:</span><span class="sxs-lookup"><span data-stu-id="e6e19-184">hello following page will appear:</span></span>

  ![disegno](media/marketplace-publishing-data-service-creation/step-7.3.png)

<span data-ttu-id="e6e19-186">toocreate un mapping di CSDL per hello set di dati in base hello database SQL di Azure:</span><span class="sxs-lookup"><span data-stu-id="e6e19-186">toocreate a CSDL mapping for hello Dataset based on hello SQL Azure DB:</span></span>

  ![disegno](media/marketplace-publishing-data-service-creation/step-7.4.png)

<span data-ttu-id="e6e19-188">E quindi per ciascuna tabella</span><span class="sxs-lookup"><span data-stu-id="e6e19-188">And then for each table</span></span>

  ![disegno](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![disegno](media/marketplace-publishing-data-service-creation/step-7.6.png)

<span data-ttu-id="e6e19-191">Se il servizio Web</span><span class="sxs-lookup"><span data-stu-id="e6e19-191">If Web Service</span></span>

  ![disegno](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> <span data-ttu-id="e6e19-193">Lettura [Mapping esistente web servizio tooOData tramite CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) per istruzioni dettagliate ed esempi sulla creazione di un servizio Web di CSDL.</span><span class="sxs-lookup"><span data-stu-id="e6e19-193">Read [Mapping an existing web service tooOData through CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) for detailed instructions and examples for creating a CSDL Web Service.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e6e19-194">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e6e19-194">Next Steps</span></span>
<span data-ttu-id="e6e19-195">Dopo aver creato l'offerta di servizio dati, assicurarsi di aver completato le istruzioni di hello in hello [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) prima di spostare in avanti troppo[test il servizio dati in gestione temporanea](marketplace-publishing-data-service-test-in-staging.md).</span><span class="sxs-lookup"><span data-stu-id="e6e19-195">Now that you've created your Data Service offer, please ensure that you complete hello instructions in hello [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) before you move forward too[Testing your Data Service in Staging](marketplace-publishing-data-service-test-in-staging.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="e6e19-196">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="e6e19-196">See Also</span></span>
* [<span data-ttu-id="e6e19-197">Guida introduttiva: Come toopublish un toohello offerta Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="e6e19-197">Getting Started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* <span data-ttu-id="e6e19-198">Se si è interessati alla comprensione hello l'intero processo di mapping di OData e lo scopo, leggere questo articolo [Mapping di dati del servizio OData](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definizioni, strutture e le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="e6e19-198">If you are interested in understanding hello overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definitions, structures, and instructions.</span></span>
* <span data-ttu-id="e6e19-199">Se è interessati a learning e informazioni sui nodi specifici di hello e i relativi parametri, leggere questo articolo [nodi Mapping di dati del servizio OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) per le definizioni e le spiegazioni, esempi e il contesto casi di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="e6e19-199">If you are interested in learning and understanding hello specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="e6e19-200">Se si è interessati a esaminare alcuni esempi, leggere questo articolo [esempi di Mapping di dati del servizio OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee codice di esempio e comprendere la sintassi di codice e il contesto.</span><span class="sxs-lookup"><span data-stu-id="e6e19-200">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee sample code and understand code syntax and context.</span></span>

[link-pubportal]:https://publish.windowsazure.com
