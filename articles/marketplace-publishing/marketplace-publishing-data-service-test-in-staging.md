---
title: Testare l'offerta di servizi dati per il Marketplace | Microsoft Docs
description: Informazioni su come testare l'offerta del servizio dati per Azure Marketplace.
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
ms.openlocfilehash: 56a8aad7484fed18b74200ffa7acf22363625a15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a><span data-ttu-id="160bf-103">Test dell'offerta del servizio dati in gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="160bf-103">Testing your Data Service offer in Staging</span></span>
> [!IMPORTANT]
> <span data-ttu-id="160bf-104">**In questo momento non stiamo più caricando nuovi editori di servizi dati. I nuovi servizi dati non saranno approvati per l'elencazione.**</span><span class="sxs-lookup"><span data-stu-id="160bf-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="160bf-105">Se si dispone di un'applicazione aziendale SaaS che si vuole pubblicare in AppSource, è possibile trovare altre informazioni [qui](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="160bf-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="160bf-106">Se si dispone di un'applicazione IaaS o di un servizio per gli sviluppatori che si vuole pubblicare in Azure Marketplace, è possibile trovare altre informazioni [qui](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="160bf-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="160bf-107">Dopo aver completato i primi due passaggi della [creazione di un account per il Dashboard venditori](marketplace-publishing-accounts-creation-registration.md) e della [creazione dell'offerta del servizio dati nel portale di pubblicazione](marketplace-publishing-data-service-creation.md), si è pronti per rendere disponibile l'offerta in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="160bf-107">After completing the first two steps of [Creating your Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md) and [Creating your Data Service Offer in Publishing Portal](marketplace-publishing-data-service-creation.md) you’re ready for making your offer available in the Azure Marketplace.</span></span> <span data-ttu-id="160bf-108">Questo argomento illustra il primo passaggio intermedio denominato "Gestione temporanea"</span><span class="sxs-lookup"><span data-stu-id="160bf-108">This topic will walk you through the first, intermediate, step called “Staging”</span></span>

<span data-ttu-id="160bf-109">Per gestione temporanea si intende la distribuzione dell'offerta in un ambiente "sandbox" privato, in cui è possibile testarne e verificarne le funzionalità prima di eseguirne il push in produzione.</span><span class="sxs-lookup"><span data-stu-id="160bf-109">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it to production.</span></span> <span data-ttu-id="160bf-110">L'offerta verrà visualizzata nella gestione temporanea esattamente come verrebbe mostrata a un cliente che l'ha distribuita.</span><span class="sxs-lookup"><span data-stu-id="160bf-110">The offer will appear in staging just as it would to a customer who has deployed it.</span></span>

## <a name="step-1-pushing-your-offer-to-staging"></a><span data-ttu-id="160bf-111">Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="160bf-111">Step 1.</span></span> <span data-ttu-id="160bf-112">Push dell'offerta nella gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="160bf-112">Pushing your offer to staging</span></span>
<span data-ttu-id="160bf-113">Il push dell'offerta nella gestione temporanea consente di testare l'offerta prima che diventi disponibile ai sottoscrittori futuri.</span><span class="sxs-lookup"><span data-stu-id="160bf-113">Pushing your offer to staging allows you to test the offer before it becomes available to future subscribers.</span></span>  <span data-ttu-id="160bf-114">È possibile visualizzare come l'offerta verrà visualizzata e funzionerà per coloro che effettuano la sottoscrizione ai dati.</span><span class="sxs-lookup"><span data-stu-id="160bf-114">You can see how your offer will appear and function for those subscribing to your data.</span></span>  

  ![disegno](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. <span data-ttu-id="160bf-116">Accedere al [portale di pubblicazione](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="160bf-116">Login into the [Publishing Portal](https://publish.windowsazure.com)</span></span>
2. <span data-ttu-id="160bf-117">Selezionare **Servizi dati** nella finestra di navigazione a sinistra</span><span class="sxs-lookup"><span data-stu-id="160bf-117">Select **Data Services** in the left navigation window</span></span>
3. <span data-ttu-id="160bf-118">Selezionare l'offerta di cui si desidera effettuare il push in gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="160bf-118">Select your offer you want to push to staging.</span></span> <span data-ttu-id="160bf-119">Verrà visualizzata la schermata precedente.</span><span class="sxs-lookup"><span data-stu-id="160bf-119">You will see the above screen.</span></span>
4. <span data-ttu-id="160bf-120">Fare clic sul pulsante **Push gestione temporanea** .</span><span class="sxs-lookup"><span data-stu-id="160bf-120">Click **Push To Staging** button.</span></span>  
5. <span data-ttu-id="160bf-121">Se sono presenti problemi con l'offerta che devono essere risolti prima del push nella gestione temporanea, verrà visualizzato un elenco.</span><span class="sxs-lookup"><span data-stu-id="160bf-121">If there are issues with the offer that needed to be completed prior to pushing to staging, you will see a list displayed.</span></span>  <span data-ttu-id="160bf-122">Correggere questi elementi facendo clic su ogni elemento nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="160bf-122">Correct these items by clicking on each item in the list.</span></span> <span data-ttu-id="160bf-123">Quando tutte le correzioni sono state apportate, fare clic nuovamente sul pulsante **Push gestione temporanea** .</span><span class="sxs-lookup"><span data-stu-id="160bf-123">When all corrections made, click **Push to Staging** button again.</span></span>

<span data-ttu-id="160bf-124">Se non sono presenti problemi con l'offerta, si noterà la finestra popup di seguito.</span><span class="sxs-lookup"><span data-stu-id="160bf-124">If there are no issues with your offer you will see the popup window below.</span></span>  

<span data-ttu-id="160bf-125">Se non si prevede/non si è stati approvati per la presentazione dell'offerta nel portale di Azure (attualmente dispone di capacità limitate), chiudere semplicemente la finestra popup.</span><span class="sxs-lookup"><span data-stu-id="160bf-125">If you’re not planning/not approved to surface your offer in Azure Portal (currently has limited capacity), then just close the pop-up window.</span></span>

<span data-ttu-id="160bf-126">Per testare il servizio dati nel portale di Azure (oltre al portale di DataMarket), è necessario un ID di sottoscrizione di Azure con cui eseguire il test.</span><span class="sxs-lookup"><span data-stu-id="160bf-126">To test your Data Service in Azure Portal (in addition to the DataMarket portal), you will need an Azure Subscription ID to test with.</span></span>  <span data-ttu-id="160bf-127">Questo ID di sottoscrizione identificherà l'account consentito per testare l'offerta.</span><span class="sxs-lookup"><span data-stu-id="160bf-127">This Subscription ID will identify the account that will be allowed to test your offer.</span></span>  

<span data-ttu-id="160bf-128">Tagliare e incollare l'ID di sottoscrizione e fare clic sul segno di spunta per continuare.</span><span class="sxs-lookup"><span data-stu-id="160bf-128">Cut and paste your Subscription ID and click the checkmark to continue.</span></span>

  ![disegno](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> <span data-ttu-id="160bf-130">Questi ID di sottoscrizione di Azure sono necessari per il testing e la gestione temporanea nel [portale di gestione di Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="160bf-130">These Azure subscriptions IDs are only required for testing and staging in the [Azure Management Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="160bf-131">Non sono necessari per eseguire il test in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="160bf-131">They are not required to test in Azure Marketplace.</span></span>
> 
> 

<span data-ttu-id="160bf-132">La schermata successiva visualizzata mostra che la pubblicazione ha luogo visualizzando l'icona "In corso" evidenziata in giallo di seguito.</span><span class="sxs-lookup"><span data-stu-id="160bf-132">The next screen that appears shows that publishing is taking place by displaying the “In progress” icon highlighted yellow below.</span></span> <span data-ttu-id="160bf-133">Il push in gestione temporanea richiede tra 10 e 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="160bf-133">Pushing to staging takes between 10 to 15 minutes.</span></span>  <span data-ttu-id="160bf-134">Se richiede più tempo, prima di aggiornare il browser (premere F5 in Internet Explorer).</span><span class="sxs-lookup"><span data-stu-id="160bf-134">If it takes longer, first refresh your browser (press F5 in IE).</span></span>  <span data-ttu-id="160bf-135">In rari casi in cui l'offerta è ancora in fase di push in gestione temporanea dopo un'ora, fare clic sul collegamento dei contatti per comunicarci che è presente un problema.</span><span class="sxs-lookup"><span data-stu-id="160bf-135">In the rare cases where your offer is still pushing to staging after an hour, click the contact us link to let us know that there is an issue.</span></span>

  ![disegno](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

<span data-ttu-id="160bf-137">Quando il push in gestione temporanea viene completato, l'icona "In corso" smette di muoversi e lo stato viene aggiornato in "Gestione temporanea".</span><span class="sxs-lookup"><span data-stu-id="160bf-137">When the Push to Staging completes the “In progress” icon will stop moving and the status will be updated to “Staged”.</span></span>  <span data-ttu-id="160bf-138">È ora possibile testare l'offerta.</span><span class="sxs-lookup"><span data-stu-id="160bf-138">You are now ready to test your offer.</span></span>  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a><span data-ttu-id="160bf-139">Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="160bf-139">Step 2.</span></span> <span data-ttu-id="160bf-140">Testare l'offerta in gestione temporanea in DataMarket</span><span class="sxs-lookup"><span data-stu-id="160bf-140">Test your staged offer in DataMarket</span></span>
<span data-ttu-id="160bf-141">Fare clic sul collegamento che segue il testo **"Visualizza l’offerta di servizio in..."**</span><span class="sxs-lookup"><span data-stu-id="160bf-141">Click the link following the text **“See Your service offer at…”**</span></span> <span data-ttu-id="160bf-142">per visualizzare la schermata che il sottoscrittore potrà vedere quando l'offerta passerà alla produzione e verrà visualizzata nel DataMarket.</span><span class="sxs-lookup"><span data-stu-id="160bf-142">to display the screen that the subscriber will see when your offer goes to production and will appear in DataMarket.</span></span>

  ![disegno](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

<span data-ttu-id="160bf-144">Testare o verificare ognuno dei 12 elementi contrassegnati in precedenza affinché tutti i logo, prezzi/transazioni, testi, immagini, documentazione e collegamenti siano corretti e funzionino in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="160bf-144">Test or verify each of the 12 items marked above to ensure all logos, prices/transactions, text, images, documentation, and links are correct and working properly.</span></span>  <span data-ttu-id="160bf-145">Questo è il momento opportuno per assicurarsi che i valori di test specificati durante la creazione dell'offerta siano stati sostituiti con valori effettivi.</span><span class="sxs-lookup"><span data-stu-id="160bf-145">This is a good time to ensure any test values you entered when creating your offer have been replaced with actual values.</span></span>

1. <span data-ttu-id="160bf-146">Logo offerta</span><span class="sxs-lookup"><span data-stu-id="160bf-146">Offer logo</span></span>
2. <span data-ttu-id="160bf-147">Nome offerta</span><span class="sxs-lookup"><span data-stu-id="160bf-147">Offer name</span></span>
3. <span data-ttu-id="160bf-148">Nome server di pubblicazione/collegamento al sito Web della società</span><span class="sxs-lookup"><span data-stu-id="160bf-148">Publisher name/link to your company's website</span></span>
4. <span data-ttu-id="160bf-149">Categorie di ricerca per l'offerta</span><span class="sxs-lookup"><span data-stu-id="160bf-149">Search categories for your offer</span></span>
5. <span data-ttu-id="160bf-150">Collegamento di supporto dell'offerta per agevolare i sottoscrittori</span><span class="sxs-lookup"><span data-stu-id="160bf-150">Your offer's support link to assist subscribers</span></span>
6. <span data-ttu-id="160bf-151">Descrizione contestuale dell'offerta</span><span class="sxs-lookup"><span data-stu-id="160bf-151">Contextual description for your offer</span></span>
7. <span data-ttu-id="160bf-152">Piano dell’offerta che descrive i dettagli di fatturazione</span><span class="sxs-lookup"><span data-stu-id="160bf-152">Offer plan depicting billing details</span></span>
8. <span data-ttu-id="160bf-153">Collegamento al codice di implementazione</span><span class="sxs-lookup"><span data-stu-id="160bf-153">Link to implementation code</span></span>
9. <span data-ttu-id="160bf-154">Immagini di esempio che illustrano l'utilizzo dei dati dell’offerta</span><span class="sxs-lookup"><span data-stu-id="160bf-154">Sample images that illustrate use of offer data</span></span>
10. <span data-ttu-id="160bf-155">Metadati di input/output per ogni servizio all'interno dell'offerta</span><span class="sxs-lookup"><span data-stu-id="160bf-155">Input/Output metadata for each service within the offer</span></span>
11. <span data-ttu-id="160bf-156">Condizioni di utilizzo dell'offerta</span><span class="sxs-lookup"><span data-stu-id="160bf-156">Offer's Terms of Use</span></span>
12. <span data-ttu-id="160bf-157">Anteprima dei dati dell'offerta</span><span class="sxs-lookup"><span data-stu-id="160bf-157">Preview of the offer's data</span></span>

<span data-ttu-id="160bf-158">Infine, controllare che il servizio funzioni nel Datamarket facendo clic sul collegamento "ESPLORA QUESTO SET DI DATI".</span><span class="sxs-lookup"><span data-stu-id="160bf-158">Finally, check the service will work through the Datamarket by clicking the link “EXPLORE THIS DATASET”.</span></span>  <span data-ttu-id="160bf-159">Verrà aperta una nuova finestra dello strumento chiamiamo "Service Explorer", in modo che sia possibile visualizzare in anteprima i risultati di una query sul servizio.</span><span class="sxs-lookup"><span data-stu-id="160bf-159">A new window will open in the tool we call “Service Explorer” so you can preview the results of a query against your service.</span></span>  <span data-ttu-id="160bf-160">In questa finestra, è possibile immettere i parametri necessari e vedere i risultati visualizzati da una query sul servizio.</span><span class="sxs-lookup"><span data-stu-id="160bf-160">In this window, you can enter the parameters needed and see the results displayed from a query against your service.</span></span>   <span data-ttu-id="160bf-161">Inoltre, viene visualizzato l'URL per la Query.</span><span class="sxs-lookup"><span data-stu-id="160bf-161">Also, displayed is the URL for your Query.</span></span>  

> [!NOTE]
> <span data-ttu-id="160bf-162">Assicurarsi di esaminare la descrizione testuale del servizio visualizzato nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="160bf-162">Be sure to review the textual description of the service displayed at the top.</span></span>  <span data-ttu-id="160bf-163">Se l'offerta è costituita da più di un servizio, fare clic sulle schede nella parte inferiore per passare al servizio successivo da esaminare e testare.</span><span class="sxs-lookup"><span data-stu-id="160bf-163">And if your offer consists of more than one service call, click the tabs at the bottom to switch to the next service to review and test.</span></span>
> 
> 

## <a name="next-step"></a><span data-ttu-id="160bf-164">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="160bf-164">Next step</span></span>
<span data-ttu-id="160bf-165">Se si riscontrano problemi e serve assistenza per risolverli, contattare il [Supporto di pubblicazione di Azure](http://go.microsoft.com/fwlink/?LinkId=272975).</span><span class="sxs-lookup"><span data-stu-id="160bf-165">If you are having issues and need help resolving them please contact [Azure Publisher Support](http://go.microsoft.com/fwlink/?LinkId=272975).</span></span>

<span data-ttu-id="160bf-166">Se si è soddisfatti e pronti per la pubblicazione dell'offerta, leggere la documentazione [Richiedere l’approvazione per il push in produzione](marketplace-publishing-push-to-production.md) .</span><span class="sxs-lookup"><span data-stu-id="160bf-166">If you are satisfied and ready to publish your offer please read the [Request Approval to Push To Production](marketplace-publishing-push-to-production.md) documentation.</span></span>

## <a name="see-also"></a><span data-ttu-id="160bf-167">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="160bf-167">See Also</span></span>
* [<span data-ttu-id="160bf-168">Guida introduttiva: Come pubblicare un'offerta in Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="160bf-168">Getting Started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

