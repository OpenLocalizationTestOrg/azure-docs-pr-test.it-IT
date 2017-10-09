---
title: "la macchina virtuale è offrire per hello Marketplace aaaTest | Documenti Microsoft"
description: Comprendere in che modo tootest immagine di macchina virtuale per hello Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 7a41c3c6-625c-4478-b804-e124dee89040
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: hascipio
ms.openlocfilehash: ab166d2c3c536810a3a8f48330f0482b9b4e58d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-vm-offer-for-hello-azure-marketplace-in-staging"></a><span data-ttu-id="b0943-103">Testare l'offerta VM per hello Azure Marketplace in gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="b0943-103">Test your VM offer for hello Azure Marketplace in staging</span></span>
<span data-ttu-id="b0943-104">Indica lo SKU in una "sandbox" in cui è possibile testare e convalidare le funzionalità prima di distribuirlo toohello Marketplace privata di distribuzione di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="b0943-104">Staging means deploying your SKU in a private “sandbox” where you can test and validate its functionality before deploying it toohello Marketplace.</span></span> <span data-ttu-id="b0943-105">Hello SKU viene visualizzato come nel caso tooa cliente che ha distribuito di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="b0943-105">hello SKU appears in staging just as it would tooa customer who has deployed it.</span></span> <span data-ttu-id="b0943-106">L'immagine di macchina virtuale deve essere toostaging toobe Certificate inserito.</span><span class="sxs-lookup"><span data-stu-id="b0943-106">Your VM image must be certified toobe pushed toostaging.</span></span>

## <a name="step-1-push-your-offer-toostaging"></a><span data-ttu-id="b0943-107">Passaggio 1: Push toostaging l'offerta</span><span class="sxs-lookup"><span data-stu-id="b0943-107">Step 1: Push your offer toostaging</span></span>
1. <span data-ttu-id="b0943-108">In hello **pubblica** scheda, fare clic su **Push tooStaging**.</span><span class="sxs-lookup"><span data-stu-id="b0943-108">On hello **Publish** tab, click **Push tooStaging**.</span></span>
   
    ![disegno](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. <span data-ttu-id="b0943-110">Se hello portale di pubblicazione invia una notifica di eventuali errori, è necessario correggerli.</span><span class="sxs-lookup"><span data-stu-id="b0943-110">If hello Publishing Portal notifies you of any errors, correct them.</span></span>
3. <span data-ttu-id="b0943-111">In hello **chi può accedere l'offerta di installazione di appoggio?** finestra di dialogo immettere elenco hello delle sottoscrizioni di Azure che si utilizzeranno toopreview l'offerta in hello [portale di anteprima Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b0943-111">In hello **Who can access your staged offer?** dialog box, enter hello list of Azure subscriptions that you will use toopreview your offer in hello [Azure preview portal](https://portal.azure.com).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b0943-112">Per le macchine virtuali e i modelli di soluzioni, **non** aggiungere all'elenco degli elementi consentiti le sottoscrizioni di tipo CSP, DreamSpark o Azure in Open.</span><span class="sxs-lookup"><span data-stu-id="b0943-112">In case of Virtual Machines and Solution templates, please **do not** whitelist subscriptions of type CSP, DreamSpark or Azure in Open.</span></span>
   > 
   > 

    > <span data-ttu-id="b0943-113">In caso di macchine virtuali, quando si fa clic sul pulsante hello **tooSTAGING PUSH**, hello alla procedura seguente viene eseguita dietro la scena hello.</span><span class="sxs-lookup"><span data-stu-id="b0943-113">In case of Virtual Machines, when you click on hello button **PUSH tooSTAGING**, hello following steps are performed behind hello scene.</span></span> <span data-ttu-id="b0943-114">Si sarà in grado di tooview lo stato di avanzamento hello di ogni passaggio nella scheda pubblicazione hello hello portale di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="b0943-114">You will be able tooview hello progress of each step under hello PUBLISH tab in hello Publishing portal.</span></span> <span data-ttu-id="b0943-115">È necessario controllare questa pagina a intervalli regolari (fino a ottenere lo stato di hello APPRONTATO) per qualsiasi informazione di errore che necessitano di correzione da end.</span><span class="sxs-lookup"><span data-stu-id="b0943-115">You must check this page at regular interval (until hello status shows STAGED) for any failure information which need correction from your end.</span></span>

    > - <span data-ttu-id="b0943-116">Inizialmente la richiesta di gestione temporanea passa team certificazione toohello che convalidare hello vhd.</span><span class="sxs-lookup"><span data-stu-id="b0943-116">At first your staging request goes toohello certification team who validate hello vhd.</span></span> <span data-ttu-id="b0943-117">Tuttavia, se la richiesta dispone solo di marketing modifica, quindi hello certificazione passaggio viene ignorato.</span><span class="sxs-lookup"><span data-stu-id="b0943-117">However, if your request has got only marketing change, then hello certification step is skipped.</span></span>
    > - <span data-ttu-id="b0943-118">Una volta completata la certificazione hello, replica di inizio offerta hello in tutti hello Data Center di Azure.</span><span class="sxs-lookup"><span data-stu-id="b0943-118">Once hello certification is complete, replication of hello offer start across all hello Azure datacenters.</span></span> <span data-ttu-id="b0943-119">In genere richiede 24-48hours per hello replica toocomplete ma può richiedere fino a settimana tooa a seconda delle dimensioni di hello del disco rigido virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="b0943-119">It generally takes 24-48hours for hello replication toocomplete but may take up tooa week depending on hello size of hello vhd.</span></span> <span data-ttu-id="b0943-120">Tuttavia, se la richiesta dispone di marketing solo modifiche, replica hello è più veloce.</span><span class="sxs-lookup"><span data-stu-id="b0943-120">However, if your request has got only marketing change, then hello replication is faster.</span></span>
    > - <span data-ttu-id="b0943-121">Una volta completata la replica di hello, quindi offerta hello saranno disponibile in hello [portale di Azure](http:/portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b0943-121">When hello replication is complete, then hello offer will be available in hello [Azure portal](http:/portal.azure.com).</span></span> <span data-ttu-id="b0943-122">A tale hello ora stato diventano presenti hello portale di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="b0943-122">At that time hello status become STAGED in hello Publishing portal.</span></span> <span data-ttu-id="b0943-123">Un'offerta di gestione temporanea è visibile in hello [portale di Azure](http:/portal.azure.com) solo tramite gli ID di posta elettronica hello associati hello sottoscrizione con cui hello viene gestita l'offerta.</span><span class="sxs-lookup"><span data-stu-id="b0943-123">A staged offer is visible in hello [Azure portal](http:/portal.azure.com) only using hello email id(s) associated with hello subscription with which hello offer is staged.</span></span>

1. <span data-ttu-id="b0943-124">Accedi toohello [portale di anteprima Azure](https://portal.azure.com) utilizzando uno dei hello le sottoscrizioni di Azure è elencato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="b0943-124">Sign in toohello [Azure preview portal](https://portal.azure.com) by using one of hello Azure subscriptions listed in hello previous step.</span></span>
2. <span data-ttu-id="b0943-125">Individuare la propria offerta e convalidare i punti dell'immagine della macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="b0943-125">Find your offer and validate your VM image points:</span></span>
   
   * <span data-ttu-id="b0943-126">Assicurarsi che il contenuto di marketing venga visualizzata correttamente in hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b0943-126">Make sure that marketing content shows up correctly in hello Marketplace.</span></span>
   * <span data-ttu-id="b0943-127">Distribuzione end-to-end dell'immagine di macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="b0943-127">End-to-end deployment of hello VM image.</span></span>
     
      ![img-map-portal](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> <span data-ttu-id="b0943-129">L'offerta rimarrà fino a quando non è informare Microsoft tramite hello portale di pubblicazione di gestione temporanea [**pubblica** scheda > fare clic sul pulsante hello **"Richiesta di approvazione tooPush tooProduction"**] che si è pronti toopush tooproduction.</span><span class="sxs-lookup"><span data-stu-id="b0943-129">Your offer will remain in staging until you notify Microsoft via hello Publishing Portal [**Publish** tab > click on hello button **"Request Approval tooPush tooProduction"**] that you are ready toopush tooproduction.</span></span> <span data-ttu-id="b0943-130">Si tratta di un toohave ideale ora che tutti i membri del team di controllare tutti gli elementi in preparazione per l'offerta prevede elencati.</span><span class="sxs-lookup"><span data-stu-id="b0943-130">This is an ideal time toohave all members of your team check over everything in preparation for your offer going listed.</span></span>
> 
> <span data-ttu-id="b0943-131">Hello piattaforma di gestione temporanea è progettato per test offerta hello in modalità di anteprima da server di pubblicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b0943-131">hello staging platform is designed for testing hello offer in a preview mode by hello publisher.</span></span> <span data-ttu-id="b0943-132">È fortemente sconsigliato l'uso di questa piattaforma a fini commerciali.</span><span class="sxs-lookup"><span data-stu-id="b0943-132">We strongly discourage using this platofrm for commerical purposes.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b0943-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b0943-133">Next steps</span></span>
<span data-ttu-id="b0943-134">Ora che l'offerta è "gestione temporanea" e dopo aver testato le funzionalità e contenuti di marketing, è possibile procedere pubblicazione finale toohello fase **passaggio 4**: [distribuzione il toohello offerta Marketplace](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="b0943-134">Now that your offer is "staged" and you have tested its functionality and marketing content, you can proceed toohello final publishing phase, **Step 4**: [Deploying your offer toohello Marketplace](marketplace-publishing-push-to-production.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="b0943-135">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b0943-135">See also</span></span>
* [<span data-ttu-id="b0943-136">Guida introduttiva: come toopublish un toohello offerta Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="b0943-136">Getting started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

