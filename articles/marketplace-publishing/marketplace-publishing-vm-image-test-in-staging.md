---
title: Testare l'offerta di macchine virtuali per il Marketplace | Microsoft Docs
description: Informazioni su come testare l'immagine della macchina virtuale per Azure Marketplace.
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
ms.openlocfilehash: 26f856059b381be91b9cdd1f98a11dc90813c0c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="test-your-vm-offer-for-the-azure-marketplace-in-staging"></a><span data-ttu-id="0f02d-103">Testare la propria offerta di VM per Azure Marketplace nella gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="0f02d-103">Test your VM offer for the Azure Marketplace in staging</span></span>
<span data-ttu-id="0f02d-104">Per gestione temporanea si intende la distribuzione della SKU in un ambiente "sandbox" privato, in cui è possibile testarne e convalidarne le funzionalità prima di distribuirla nel Marketplace.</span><span class="sxs-lookup"><span data-stu-id="0f02d-104">Staging means deploying your SKU in a private “sandbox” where you can test and validate its functionality before deploying it to the Marketplace.</span></span> <span data-ttu-id="0f02d-105">La SKU viene visualizzata nella gestione temporanea esattamente come verrebbe mostrata a un cliente che l'ha distribuita.</span><span class="sxs-lookup"><span data-stu-id="0f02d-105">The SKU appears in staging just as it would to a customer who has deployed it.</span></span> <span data-ttu-id="0f02d-106">L'immagine della macchina virtuale deve essere certificata per il push nella gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="0f02d-106">Your VM image must be certified to be pushed to staging.</span></span>

## <a name="step-1-push-your-offer-to-staging"></a><span data-ttu-id="0f02d-107">Passaggio 1: push dell'offerta nella gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="0f02d-107">Step 1: Push your offer to staging</span></span>
1. <span data-ttu-id="0f02d-108">Nella scheda **Publish** (Pubblica) fare clic su **Push to Staging** (Passa a gestione temporanea).</span><span class="sxs-lookup"><span data-stu-id="0f02d-108">On the **Publish** tab, click **Push to Staging**.</span></span>
   
    ![disegno](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. <span data-ttu-id="0f02d-110">Se il portale di pubblicazione notifica eventuali errori, correggerli.</span><span class="sxs-lookup"><span data-stu-id="0f02d-110">If the Publishing Portal notifies you of any errors, correct them.</span></span>
3. <span data-ttu-id="0f02d-111">Nella finestra di dialogo **Chi può accedere all'offerta di gestione temporanea?** immettere l'elenco delle sottoscrizioni di Azure che verrà utilizzato per l'anteprima dell’offerta nel [portale di anteprima di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0f02d-111">In the **Who can access your staged offer?** dialog box, enter the list of Azure subscriptions that you will use to preview your offer in the [Azure preview portal](https://portal.azure.com).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0f02d-112">Per le macchine virtuali e i modelli di soluzioni, **non** aggiungere all'elenco degli elementi consentiti le sottoscrizioni di tipo CSP, DreamSpark o Azure in Open.</span><span class="sxs-lookup"><span data-stu-id="0f02d-112">In case of Virtual Machines and Solution templates, please **do not** whitelist subscriptions of type CSP, DreamSpark or Azure in Open.</span></span>
   > 
   > 

    > <span data-ttu-id="0f02d-113">Per le macchine virtuali, quando si fa clic sul pulsante **PASSA A GESTIONE TEMPORANEA**, dietro le quinte vengono eseguiti i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="0f02d-113">In case of Virtual Machines, when you click on the button **PUSH TO STAGING**, the following steps are performed behind the scene.</span></span> <span data-ttu-id="0f02d-114">Sarà quindi possibile visualizzare lo stato di avanzamento di ogni passaggio nella scheda PUBBLICA nel portale di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="0f02d-114">You will be able to view the progress of each step under the PUBLISH tab in the Publishing portal.</span></span> <span data-ttu-id="0f02d-115">È necessario controllare questa pagina regolarmente (fino a quando lo stato diventa ANTEPRIMA) per eventuali informazioni di errore che richiedono correzioni.</span><span class="sxs-lookup"><span data-stu-id="0f02d-115">You must check this page at regular interval (until the status shows STAGED) for any failure information which need correction from your end.</span></span>

    > - <span data-ttu-id="0f02d-116">Inizialmente la richiesta di gestione temporanea viene inviata al team di certificazione che convalida il VHD.</span><span class="sxs-lookup"><span data-stu-id="0f02d-116">At first your staging request goes to the certification team who validate the vhd.</span></span> <span data-ttu-id="0f02d-117">Se invece la richiesta include solo modifiche commerciali, il passaggio di certificazione viene ignorato.</span><span class="sxs-lookup"><span data-stu-id="0f02d-117">However, if your request has got only marketing change, then the certification step is skipped.</span></span>
    > - <span data-ttu-id="0f02d-118">Una volta completata la certificazione, viene avviata la replica dell'offerta in tutti i data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f02d-118">Once the certification is complete, replication of the offer start across all the Azure datacenters.</span></span> <span data-ttu-id="0f02d-119">Il completamento della replica richiede in genere 24-48 ore ma potrebbe richiedere fino a una settimana a seconda della dimensione del VHD.</span><span class="sxs-lookup"><span data-stu-id="0f02d-119">It generally takes 24-48hours for the replication to complete but may take up to a week depending on the size of the vhd.</span></span> <span data-ttu-id="0f02d-120">Se invece la richiesta include solo modifiche commerciali, la replica è più veloce.</span><span class="sxs-lookup"><span data-stu-id="0f02d-120">However, if your request has got only marketing change, then the replication is faster.</span></span>
    > - <span data-ttu-id="0f02d-121">Una volta completata la replica, l'offerta sarà disponibile nel [portale di Azure](http:/portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0f02d-121">When the replication is complete, then the offer will be available in the [Azure portal](http:/portal.azure.com).</span></span> <span data-ttu-id="0f02d-122">A quel punto lo stato diventerà ANTEPRIMA nel portale di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="0f02d-122">At that time the status become STAGED in the Publishing portal.</span></span> <span data-ttu-id="0f02d-123">Un'offerta in gestione temporanea è visibile nel [portale di Azure](http:/portal.azure.com) solo usando gli ID di posta elettronica associati con la sottoscrizione con cui l'offerta è gestita temporaneamente.</span><span class="sxs-lookup"><span data-stu-id="0f02d-123">A staged offer is visible in the [Azure portal](http:/portal.azure.com) only using the email id(s) associated with the subscription with which the offer is staged.</span></span>

1. <span data-ttu-id="0f02d-124">Accedere al [portale di anteprima di Azure](https://portal.azure.com) usando una delle sottoscrizioni di Azure elencate nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="0f02d-124">Sign in to the [Azure preview portal](https://portal.azure.com) by using one of the Azure subscriptions listed in the previous step.</span></span>
2. <span data-ttu-id="0f02d-125">Individuare la propria offerta e convalidare i punti dell'immagine della macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="0f02d-125">Find your offer and validate your VM image points:</span></span>
   
   * <span data-ttu-id="0f02d-126">Assicurarsi che il contenuto di marketing venga visualizzato correttamente nel Marketplace.</span><span class="sxs-lookup"><span data-stu-id="0f02d-126">Make sure that marketing content shows up correctly in the Marketplace.</span></span>
   * <span data-ttu-id="0f02d-127">Distribuzione end-to-end dell'immagine della VM.</span><span class="sxs-lookup"><span data-stu-id="0f02d-127">End-to-end deployment of the VM image.</span></span>
     
      ![img-map-portal](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> <span data-ttu-id="0f02d-129">L'offerta resterà nella fase di gestione temporanea fino a quando non si notifica a Microsoft tramite il portale di pubblicazione [scheda **Publish** (Pubblica) > clic sul pulsante **"Request Approval to Push to Production"** (Richiedi approvazione per push in produzione)] che si è pronti per passare alla fase di produzione.</span><span class="sxs-lookup"><span data-stu-id="0f02d-129">Your offer will remain in staging until you notify Microsoft via the Publishing Portal [**Publish** tab > click on the button **"Request Approval to Push to Production"**] that you are ready to push to production.</span></span> <span data-ttu-id="0f02d-130">A questo punto, è opportuno chiedere a tutti i membri del team di verificare tutti gli aspetti preliminari all'elencazione dell'offerta.</span><span class="sxs-lookup"><span data-stu-id="0f02d-130">This is an ideal time to have all members of your team check over everything in preparation for your offer going listed.</span></span>
> 
> <span data-ttu-id="0f02d-131">La piattaforma di gestione temporanea è progettata per il test dell'offerta in una modalità di anteprima da parte dell'autore.</span><span class="sxs-lookup"><span data-stu-id="0f02d-131">The staging platform is designed for testing the offer in a preview mode by the publisher.</span></span> <span data-ttu-id="0f02d-132">È fortemente sconsigliato l'uso di questa piattaforma a fini commerciali.</span><span class="sxs-lookup"><span data-stu-id="0f02d-132">We strongly discourage using this platofrm for commerical purposes.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0f02d-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0f02d-133">Next steps</span></span>
<span data-ttu-id="0f02d-134">Ora che l'offerta è in "gestione temporanea" e ne sono stati testati le funzionalità e i contenuti di marketing, è possibile procedere alla fase di pubblicazione finale, ovvero il **Passaggio 4**: [Distribuzione dell'offerta nel Marketplace](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="0f02d-134">Now that your offer is "staged" and you have tested its functionality and marketing content, you can proceed to the final publishing phase, **Step 4**: [Deploying your offer to the Marketplace](marketplace-publishing-push-to-production.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="0f02d-135">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0f02d-135">See also</span></span>
* [<span data-ttu-id="0f02d-136">Guida introduttiva: Come pubblicare un'offerta in Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="0f02d-136">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

