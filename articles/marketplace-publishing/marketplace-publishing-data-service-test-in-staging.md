---
title: aaaTesting offrono il servizio dati per hello Marketplace | Documenti Microsoft
description: Comprendere in che modo tootest offrono il servizio dati per hello Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e861bd11-f74d-4d77-b4b5-23fb463644ad
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 1b9c7027d8e0818b9bdee5cfca971bab25dd1959
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a><span data-ttu-id="3ef64-103">Test dell'offerta del servizio dati in gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="3ef64-103">Testing your Data Service offer in Staging</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3ef64-104">**In questo momento non stiamo più caricando nuovi editori di servizi dati. I nuovi servizi dati non saranno approvati per l'elencazione.**</span><span class="sxs-lookup"><span data-stu-id="3ef64-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="3ef64-105">Se si dispone di un'applicazione SaaS di business si desidera toopublish in AppSource è possibile trovare ulteriori informazioni [qui](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="3ef64-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="3ef64-106">Se si utilizzano applicazioni IaaS sviluppatore del servizio si sarebbe ad esempio toopublish in Azure Marketplace è possibile trovare ulteriori informazioni [qui](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="3ef64-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="3ef64-107">Dopo aver completato i primi due passaggi di hello di [creazione dell'account di Microsoft Developer](marketplace-publishing-accounts-creation-registration.md) e [creazione l'offerta di servizio dati nel portale di pubblicazione](marketplace-publishing-data-service-creation.md) si è pronti per rendere disponibili in hello l'offerta Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3ef64-107">After completing hello first two steps of [Creating your Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md) and [Creating your Data Service Offer in Publishing Portal](marketplace-publishing-data-service-creation.md) you’re ready for making your offer available in hello Azure Marketplace.</span></span> <span data-ttu-id="3ef64-108">In questo argomento verrà illustrati hello prima, intermedia, passaggio denominato "gestione temporanea"</span><span class="sxs-lookup"><span data-stu-id="3ef64-108">This topic will walk you through hello first, intermediate, step called “Staging”</span></span>

<span data-ttu-id="3ef64-109">Indica l'offerta in una "sandbox" in cui è possibile testare e verificare le funzionalità prima di pubblicarlo tooproduction privata di distribuzione di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="3ef64-109">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it tooproduction.</span></span> <span data-ttu-id="3ef64-110">offerta Hello apparirà come avverrebbe tooa cliente che ha distribuito di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="3ef64-110">hello offer will appear in staging just as it would tooa customer who has deployed it.</span></span>

## <a name="step-1-pushing-your-offer-toostaging"></a><span data-ttu-id="3ef64-111">Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="3ef64-111">Step 1.</span></span> <span data-ttu-id="3ef64-112">Push toostaging l'offerta</span><span class="sxs-lookup"><span data-stu-id="3ef64-112">Pushing your offer toostaging</span></span>
<span data-ttu-id="3ef64-113">Inserendo l'offerta toostaging consente offerta hello tootest prima che diventi disponibile toofuture sottoscrittori.</span><span class="sxs-lookup"><span data-stu-id="3ef64-113">Pushing your offer toostaging allows you tootest hello offer before it becomes available toofuture subscribers.</span></span>  <span data-ttu-id="3ef64-114">È possibile visualizzare come l'offerta la corretta visualizzazione e per quelli tooyour dati di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="3ef64-114">You can see how your offer will appear and function for those subscribing tooyour data.</span></span>  

  ![disegno](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. <span data-ttu-id="3ef64-116">Account di accesso in hello [portale di pubblicazione](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="3ef64-116">Login into hello [Publishing Portal](https://publish.windowsazure.com)</span></span>
2. <span data-ttu-id="3ef64-117">Selezionare **Data Services** nella finestra di navigazione a sinistra di hello</span><span class="sxs-lookup"><span data-stu-id="3ef64-117">Select **Data Services** in hello left navigation window</span></span>
3. <span data-ttu-id="3ef64-118">Selezionare l'offerta desiderata toopush toostaging.</span><span class="sxs-lookup"><span data-stu-id="3ef64-118">Select your offer you want toopush toostaging.</span></span> <span data-ttu-id="3ef64-119">Si noterà hello schermata.</span><span class="sxs-lookup"><span data-stu-id="3ef64-119">You will see hello above screen.</span></span>
4. <span data-ttu-id="3ef64-120">Fare clic su **Push tooStaging** pulsante.</span><span class="sxs-lookup"><span data-stu-id="3ef64-120">Click **Push tooStaging** button.</span></span>  
5. <span data-ttu-id="3ef64-121">Se si verificano problemi con hello offerta necessari toobe completato toostaging toopushing precedente, verrà visualizzato un elenco visualizzato.</span><span class="sxs-lookup"><span data-stu-id="3ef64-121">If there are issues with hello offer that needed toobe completed prior toopushing toostaging, you will see a list displayed.</span></span>  <span data-ttu-id="3ef64-122">Correggere questi elementi facendo clic su ogni elemento nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="3ef64-122">Correct these items by clicking on each item in hello list.</span></span> <span data-ttu-id="3ef64-123">Quando tutte le correzioni apportate, fare clic su **Push tooStaging** nuovamente clic sul pulsante.</span><span class="sxs-lookup"><span data-stu-id="3ef64-123">When all corrections made, click **Push tooStaging** button again.</span></span>

<span data-ttu-id="3ef64-124">Se non esistono problemi con l'offerta finestra popup hello seguente verrà visualizzato.</span><span class="sxs-lookup"><span data-stu-id="3ef64-124">If there are no issues with your offer you will see hello popup window below.</span></span>  

<span data-ttu-id="3ef64-125">Se non si pianificazione/non approvato toosurface l'offerta nel portale di Azure (attualmente dispone di capacità limitata), quindi finestra popup hello appena Chiudi.</span><span class="sxs-lookup"><span data-stu-id="3ef64-125">If you’re not planning/not approved toosurface your offer in Azure Portal (currently has limited capacity), then just close hello pop-up window.</span></span>

<span data-ttu-id="3ef64-126">tootest i dati del servizio nel portale di Azure (nel portale di DataMarket toohello di addizione), sarà necessario tootest un ID sottoscrizione di Azure con.</span><span class="sxs-lookup"><span data-stu-id="3ef64-126">tootest your Data Service in Azure Portal (in addition toohello DataMarket portal), you will need an Azure Subscription ID tootest with.</span></span>  <span data-ttu-id="3ef64-127">L'ID sottoscrizione identificherà account hello che verrà consentito tootest l'offerta.</span><span class="sxs-lookup"><span data-stu-id="3ef64-127">This Subscription ID will identify hello account that will be allowed tootest your offer.</span></span>  

<span data-ttu-id="3ef64-128">Tagliare e incollare l'ID sottoscrizione e fare clic su hello toocontinue di segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="3ef64-128">Cut and paste your Subscription ID and click hello checkmark toocontinue.</span></span>

  ![disegno](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> <span data-ttu-id="3ef64-130">Questi ID le sottoscrizioni di Azure sono necessari per il testing e di gestione temporanea in hello [il portale di gestione di Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="3ef64-130">These Azure subscriptions IDs are only required for testing and staging in hello [Azure Management Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="3ef64-131">Non sono necessari tootest in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3ef64-131">They are not required tootest in Azure Marketplace.</span></span>
> 
> 

<span data-ttu-id="3ef64-132">Hello che viene visualizzato nella schermata successiva che la pubblicazione viene eseguita mediante la visualizzazione di hello "In corso" icona evidenziata giallo riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="3ef64-132">hello next screen that appears shows that publishing is taking place by displaying hello “In progress” icon highlighted yellow below.</span></span> <span data-ttu-id="3ef64-133">Push toostaging accetta tra 10 minuti too15.</span><span class="sxs-lookup"><span data-stu-id="3ef64-133">Pushing toostaging takes between 10 too15 minutes.</span></span>  <span data-ttu-id="3ef64-134">Se richiede più tempo, prima di aggiornare il browser (premere F5 in Internet Explorer).</span><span class="sxs-lookup"><span data-stu-id="3ef64-134">If it takes longer, first refresh your browser (press F5 in IE).</span></span>  <span data-ttu-id="3ef64-135">In casi rari hello in cui l'offerta viene comunque eseguita toostaging dopo un'ora, fare clic su contatto hello ci toolet inviarci che si verifica un problema di collegamento.</span><span class="sxs-lookup"><span data-stu-id="3ef64-135">In hello rare cases where your offer is still pushing toostaging after an hour, click hello contact us link toolet us know that there is an issue.</span></span>

  ![disegno](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

<span data-ttu-id="3ef64-137">Al termine di hello Push tooStaging hello "In corso" icona verrà interrotta lo spostamento e verrà aggiornato lo stato di hello troppo "staging".</span><span class="sxs-lookup"><span data-stu-id="3ef64-137">When hello Push tooStaging completes hello “In progress” icon will stop moving and hello status will be updated too“Staged”.</span></span>  <span data-ttu-id="3ef64-138">Si sono ora pronti tootest l'offerta.</span><span class="sxs-lookup"><span data-stu-id="3ef64-138">You are now ready tootest your offer.</span></span>  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a><span data-ttu-id="3ef64-139">Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="3ef64-139">Step 2.</span></span> <span data-ttu-id="3ef64-140">Testare l'offerta in gestione temporanea in DataMarket</span><span class="sxs-lookup"><span data-stu-id="3ef64-140">Test your staged offer in DataMarket</span></span>
<span data-ttu-id="3ef64-141">Fare clic sul collegamento hello dopo il testo hello **"vedere il servizio di offerta...."**</span><span class="sxs-lookup"><span data-stu-id="3ef64-141">Click hello link following hello text **“See Your service offer at…”**</span></span> <span data-ttu-id="3ef64-142">schermata di hello toodisplay hello sottoscrittore verrà visualizzato quando l'offerta passa tooproduction e verrà visualizzato in DataMarket.</span><span class="sxs-lookup"><span data-stu-id="3ef64-142">toodisplay hello screen that hello subscriber will see when your offer goes tooproduction and will appear in DataMarket.</span></span>

  ![disegno](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

<span data-ttu-id="3ef64-144">Testare o verificare tutti gli elementi 12 hello contrassegnato sopra tooensure tutti i logo, prezzi/transazioni, testo, immagini, documentazione e collegamenti siano corrette e funzionino correttamente.</span><span class="sxs-lookup"><span data-stu-id="3ef64-144">Test or verify each of hello 12 items marked above tooensure all logos, prices/transactions, text, images, documentation, and links are correct and working properly.</span></span>  <span data-ttu-id="3ef64-145">Si tratta di un tooensure tempestivamente eventuali valori di test che immessi durante la creazione dell'offerta sono stati sostituiti con i valori effettivi.</span><span class="sxs-lookup"><span data-stu-id="3ef64-145">This is a good time tooensure any test values you entered when creating your offer have been replaced with actual values.</span></span>

1. <span data-ttu-id="3ef64-146">Logo offerta</span><span class="sxs-lookup"><span data-stu-id="3ef64-146">Offer logo</span></span>
2. <span data-ttu-id="3ef64-147">Nome offerta</span><span class="sxs-lookup"><span data-stu-id="3ef64-147">Offer name</span></span>
3. <span data-ttu-id="3ef64-148">Sito Web della società tooyour/collegamento del relativo nome di server di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="3ef64-148">Publisher name/link tooyour company's website</span></span>
4. <span data-ttu-id="3ef64-149">Categorie di ricerca per l'offerta</span><span class="sxs-lookup"><span data-stu-id="3ef64-149">Search categories for your offer</span></span>
5. <span data-ttu-id="3ef64-150">Sottoscrittori tooassist collegamento di supporto dell'offerta</span><span class="sxs-lookup"><span data-stu-id="3ef64-150">Your offer's support link tooassist subscribers</span></span>
6. <span data-ttu-id="3ef64-151">Descrizione contestuale dell'offerta</span><span class="sxs-lookup"><span data-stu-id="3ef64-151">Contextual description for your offer</span></span>
7. <span data-ttu-id="3ef64-152">Piano dell’offerta che descrive i dettagli di fatturazione</span><span class="sxs-lookup"><span data-stu-id="3ef64-152">Offer plan depicting billing details</span></span>
8. <span data-ttu-id="3ef64-153">Collegamento tooimplementation codice</span><span class="sxs-lookup"><span data-stu-id="3ef64-153">Link tooimplementation code</span></span>
9. <span data-ttu-id="3ef64-154">Immagini di esempio che illustrano l'utilizzo dei dati dell’offerta</span><span class="sxs-lookup"><span data-stu-id="3ef64-154">Sample images that illustrate use of offer data</span></span>
10. <span data-ttu-id="3ef64-155">Metadati di Input/Output per ogni servizio all'interno di offerta hello</span><span class="sxs-lookup"><span data-stu-id="3ef64-155">Input/Output metadata for each service within hello offer</span></span>
11. <span data-ttu-id="3ef64-156">Condizioni di utilizzo dell'offerta</span><span class="sxs-lookup"><span data-stu-id="3ef64-156">Offer's Terms of Use</span></span>
12. <span data-ttu-id="3ef64-157">Anteprima dei dati dell'offerta hello</span><span class="sxs-lookup"><span data-stu-id="3ef64-157">Preview of hello offer's data</span></span>

<span data-ttu-id="3ef64-158">Infine, controllare il servizio hello funzionerà tramite hello Datamarket facendo clic sul collegamento hello "Esplora set di dati".</span><span class="sxs-lookup"><span data-stu-id="3ef64-158">Finally, check hello service will work through hello Datamarket by clicking hello link “EXPLORE THIS DATASET”.</span></span>  <span data-ttu-id="3ef64-159">Verrà aperta una nuova finestra dello strumento hello è chiamare "Service Explorer" in modo che è possibile visualizzare l'anteprima risultati hello di una query per il servizio.</span><span class="sxs-lookup"><span data-stu-id="3ef64-159">A new window will open in hello tool we call “Service Explorer” so you can preview hello results of a query against your service.</span></span>  <span data-ttu-id="3ef64-160">In questa finestra, è possibile immettere hello parametri necessari e visualizzare i risultati di hello visualizzati da una query sul servizio.</span><span class="sxs-lookup"><span data-stu-id="3ef64-160">In this window, you can enter hello parameters needed and see hello results displayed from a query against your service.</span></span>   <span data-ttu-id="3ef64-161">Inoltre, visualizzato è hello URL per la Query.</span><span class="sxs-lookup"><span data-stu-id="3ef64-161">Also, displayed is hello URL for your Query.</span></span>  

> [!NOTE]
> <span data-ttu-id="3ef64-162">Impossibile verificare tooreview hello descrizione testuale del servizio hello visualizzato nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="3ef64-162">Be sure tooreview hello textual description of hello service displayed at hello top.</span></span>  <span data-ttu-id="3ef64-163">E se l'offerta è costituito da più di un servizio di chiamata, fare clic sulle schede hello in hello inferiore tooswitch toohello successivo servizio tooreview e al test.</span><span class="sxs-lookup"><span data-stu-id="3ef64-163">And if your offer consists of more than one service call, click hello tabs at hello bottom tooswitch toohello next service tooreview and test.</span></span>
> 
> 

## <a name="next-step"></a><span data-ttu-id="3ef64-164">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="3ef64-164">Next step</span></span>
<span data-ttu-id="3ef64-165">Se si riscontrano problemi e serve assistenza per risolverli, contattare il [Supporto di pubblicazione di Azure](http://go.microsoft.com/fwlink/?LinkId=272975).</span><span class="sxs-lookup"><span data-stu-id="3ef64-165">If you are having issues and need help resolving them please contact [Azure Publisher Support](http://go.microsoft.com/fwlink/?LinkId=272975).</span></span>

<span data-ttu-id="3ef64-166">Se si è soddisfatti e toopublish pronto l'offerta leggere hello [richiesta approvazione tooPush tooProduction](marketplace-publishing-push-to-production.md) documentazione.</span><span class="sxs-lookup"><span data-stu-id="3ef64-166">If you are satisfied and ready toopublish your offer please read hello [Request Approval tooPush tooProduction](marketplace-publishing-push-to-production.md) documentation.</span></span>

## <a name="see-also"></a><span data-ttu-id="3ef64-167">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="3ef64-167">See Also</span></span>
* [<span data-ttu-id="3ef64-168">Guida introduttiva: Come toopublish un toohello offerta Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="3ef64-168">Getting Started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

