---
title: aaaAzure gestite le applicazioni in hello Marketplace | Documenti Microsoft
description: Viene descritto Azure gestite le applicazioni che sono disponibili tramite hello Marketplace.
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b3cdf3f1fccdd47db699e4892ae8bce35118bfd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-in-hello-marketplace"></a><span data-ttu-id="66d5e-103">Le applicazioni in hello Marketplace gestito di Azure</span><span class="sxs-lookup"><span data-stu-id="66d5e-103">Azure managed applications in hello Marketplace</span></span>

 <span data-ttu-id="66d5e-104">File msp, ISV e integratori di sistema (SIs) possono usare Azure gestito toooffer applicazioni ai clienti di Azure Marketplace tooall soluzioni.</span><span class="sxs-lookup"><span data-stu-id="66d5e-104">MSPs, ISVs, and system integrators (SIs) can use Azure managed applications toooffer their solutions tooall Azure Marketplace customers.</span></span> <span data-ttu-id="66d5e-105">Tali soluzioni ridurre la manutenzione di hello e overhead di manutenzione per i clienti.</span><span class="sxs-lookup"><span data-stu-id="66d5e-105">Such solutions reduce hello maintenance and servicing overhead for customers.</span></span> <span data-ttu-id="66d5e-106">I server di pubblicazione è possibile vendere infrastruttura e il software tramite hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="66d5e-106">Publishers can sell infrastructure and software through hello Marketplace.</span></span> <span data-ttu-id="66d5e-107">È possibile collegare supporto operativo toomanaged applicazioni e servizi.</span><span class="sxs-lookup"><span data-stu-id="66d5e-107">They can attach services and operational support toomanaged applications.</span></span> <span data-ttu-id="66d5e-108">Per altre informazioni, vedere [Panoramica delle applicazioni gestite di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="66d5e-108">For more information, see [Managed application overview](managed-application-overview.md).</span></span>

<span data-ttu-id="66d5e-109">In questo articolo viene illustrato un MSP, ISV o SI può pubblicare un toohello applicazione Marketplace e renderlo toocustomers ampiamente disponibili.</span><span class="sxs-lookup"><span data-stu-id="66d5e-109">This article explains how an MSP, ISV, or SI can publish an application toohello Marketplace and make it broadly available toocustomers.</span></span>

## <a name="prerequisites-for-publishing-a-managed-application"></a><span data-ttu-id="66d5e-110">Prerequisiti per la pubblicazione di un'applicazione gestita</span><span class="sxs-lookup"><span data-stu-id="66d5e-110">Prerequisites for publishing a managed application</span></span>

<span data-ttu-id="66d5e-111">Prerequisiti toolisting in hello Marketplace:</span><span class="sxs-lookup"><span data-stu-id="66d5e-111">Prerequisites toolisting in hello Marketplace:</span></span>

* <span data-ttu-id="66d5e-112">Tecnici</span><span class="sxs-lookup"><span data-stu-id="66d5e-112">Technical</span></span>

    *  <span data-ttu-id="66d5e-113">Per informazioni sulla struttura di base hello e la sintassi dei modelli di gestione risorse di Azure, vedere [modelli di Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="66d5e-113">For information about hello basic structure and syntax of Azure Resource Manager templates, see [Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
    *  <span data-ttu-id="66d5e-114">soluzioni di tooview modello completo, vedere [modelli di avvio rapido di Azure](https://azure.microsoft.com/en-us/documentation/templates/) o hello [repository di modelli di avvio rapido](https://github.com/azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="66d5e-114">tooview complete template solutions, see [Azure Quickstart templates](https://azure.microsoft.com/en-us/documentation/templates/) or hello [Quickstart template repository](https://github.com/azure/azure-quickstart-templates).</span></span>
    *  <span data-ttu-id="66d5e-115">Per informazioni su come toocreate hello interfaccia per i clienti di distribuire l'applicazione tramite hello Marketplace, vedere [creare un file di definizione dell'interfaccia](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="66d5e-115">For information about how toocreate hello interface for customers who deploy your application through hello Marketplace, see [Create a user interface definition file](managed-application-createuidefinition-overview.md).</span></span>

* <span data-ttu-id="66d5e-116">Non tecnici (requisiti aziendali)</span><span class="sxs-lookup"><span data-stu-id="66d5e-116">Nontechnical (business requirements)</span></span>

    *   <span data-ttu-id="66d5e-117">L'azienda o figlie devono trovarsi in un paese in cui vendite sono supportate da hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="66d5e-117">Your company or its subsidiary must be located in a country where sales are supported by hello Marketplace.</span></span>
    *   <span data-ttu-id="66d5e-118">Il prodotto deve essere concesso in licenza in modo che sia compatibile con i modelli di fatturazione supportati da hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="66d5e-118">Your product must be licensed in a way that is compatible with billing models supported by hello Marketplace.</span></span>
    *   <span data-ttu-id="66d5e-119">Si è responsabile di garantire il supporto tecnico disponibile toocustomers in modo commercialmente ragionevole.</span><span class="sxs-lookup"><span data-stu-id="66d5e-119">You're responsible for making technical support available toocustomers in a commercially reasonable manner.</span></span> <span data-ttu-id="66d5e-120">supporto Hello può essere disponibile, a pagamento, o tramite una community di supporto.</span><span class="sxs-lookup"><span data-stu-id="66d5e-120">hello support can be free, paid, or through community support.</span></span>
    *   <span data-ttu-id="66d5e-121">Il partner ha la responsabilità di concedere in licenza il software e le dipendenze da software di terze parti.</span><span class="sxs-lookup"><span data-stu-id="66d5e-121">You're responsible for licensing your software and any third-party software dependencies.</span></span>
    *   <span data-ttu-id="66d5e-122">È necessario fornire contenuto che soddisfa i criteri per l'offerta di toobe elencato nel Marketplace hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="66d5e-122">You must provide content that meets criteria for your offering toobe listed in hello Marketplace and in hello Azure portal.</span></span>
    *   <span data-ttu-id="66d5e-123">È necessario accettare i termini toohello dell'accordo di server di pubblicazione e i criteri di partecipazione hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="66d5e-123">You must agree toohello terms of hello Azure Marketplace Participation Policies and Publisher Agreement.</span></span>
    *   <span data-ttu-id="66d5e-124">È necessario accettare toocomply con contratto di Microsoft Azure Certified programma hello condizioni per l'utilizzo e informativa sulla Privacy di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="66d5e-124">You must agree toocomply with hello Terms of Use, Microsoft Privacy Statement, and Microsoft Azure Certified Program Agreement.</span></span>

## <a name="create-a-new-azure-application-offer"></a><span data-ttu-id="66d5e-125">Creare una nuova offerta di applicazione Azure</span><span class="sxs-lookup"><span data-stu-id="66d5e-125">Create a new Azure application offer</span></span>

<span data-ttu-id="66d5e-126">Una volta soddisfatti i prerequisiti di hello, si è pronti toocreate l'offerta di applicazione gestita.</span><span class="sxs-lookup"><span data-stu-id="66d5e-126">After you meet hello prerequisites, you're ready toocreate your managed application offer.</span></span> <span data-ttu-id="66d5e-127">Di seguito è disponibile una breve panoramica di un'offerta e di uno SKU.</span><span class="sxs-lookup"><span data-stu-id="66d5e-127">Let's take a quick overview of an offer and a SKU.</span></span>

### <a name="offer"></a><span data-ttu-id="66d5e-128">Offerta</span><span class="sxs-lookup"><span data-stu-id="66d5e-128">Offer</span></span>

<span data-ttu-id="66d5e-129">offerta Hello per un'applicazione gestita corrisponde classe tooa del prodotto offerta da un server di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="66d5e-129">hello offer for a managed application corresponds tooa class of product offering from a publisher.</span></span> <span data-ttu-id="66d5e-130">Se si dispone di un nuovo tipo di soluzione dell'applicazione che si desidera toomake disponibile in hello Marketplace, è possibile configurarlo come una nuova offerta.</span><span class="sxs-lookup"><span data-stu-id="66d5e-130">If you have a new type of solution/application that you want toomake available in hello Marketplace, you can set it up as a new offer.</span></span> <span data-ttu-id="66d5e-131">Un'offerta è una raccolta di SKU.</span><span class="sxs-lookup"><span data-stu-id="66d5e-131">An offer is a collection of SKUs.</span></span> <span data-ttu-id="66d5e-132">Ogni offerta viene visualizzata come proprio entità in hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="66d5e-132">Every offer appears as its own entity in hello Marketplace.</span></span>

### <a name="sku"></a><span data-ttu-id="66d5e-133">SKU</span><span class="sxs-lookup"><span data-stu-id="66d5e-133">SKU</span></span>

<span data-ttu-id="66d5e-134">Uno SKU è hello unità più piccola acquistabili di un'offerta.</span><span class="sxs-lookup"><span data-stu-id="66d5e-134">A SKU is hello smallest purchasable unit of an offer.</span></span> <span data-ttu-id="66d5e-135">È possibile utilizzare uno SKU all'interno di hello toodifferentiate di classe (offerta) stesso prodotto tra:</span><span class="sxs-lookup"><span data-stu-id="66d5e-135">You can use a SKU within hello same product class (offer) toodifferentiate between:</span></span>

* <span data-ttu-id="66d5e-136">le diverse funzionalità supportate</span><span class="sxs-lookup"><span data-stu-id="66d5e-136">Different features that are supported.</span></span>
* <span data-ttu-id="66d5e-137">Se offerta hello sia gestita o meno.</span><span class="sxs-lookup"><span data-stu-id="66d5e-137">Whether hello offer is managed or unmanaged.</span></span>
* <span data-ttu-id="66d5e-138">i modelli di fatturazione supportati</span><span class="sxs-lookup"><span data-stu-id="66d5e-138">Billing models that are supported.</span></span>

<span data-ttu-id="66d5e-139">Uno SKU appare sotto hello padre offerta in Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="66d5e-139">A SKU appears under hello parent offer in hello Marketplace.</span></span> <span data-ttu-id="66d5e-140">Viene visualizzato come il proprio entità acquistabili in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="66d5e-140">It appears as its own purchasable entity in hello Azure portal.</span></span>

### <a name="set-up-an-offer"></a><span data-ttu-id="66d5e-141">Configurare un'offerta</span><span class="sxs-lookup"><span data-stu-id="66d5e-141">Set up an offer</span></span>

1. <span data-ttu-id="66d5e-142">Accedi toohello [portale per i Partner di Cloud](https://cloudpartner.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="66d5e-142">Sign in toohello [Cloud Partner portal](https://cloudpartner.azure.com/).</span></span>

2. <span data-ttu-id="66d5e-143">Nel riquadro di spostamento hello hello sinistra, selezionare **+ nuova offerta** > **applicazioni Azure**.</span><span class="sxs-lookup"><span data-stu-id="66d5e-143">In hello navigation pane on hello left, select **+ New offer** > **Azure Applications**.</span></span>

    ![Nuova offerta](./media/managed-application-author-marketplace/newOffer.png)

3. <span data-ttu-id="66d5e-145">Compilare moduli hello che vengono visualizzati nel hello lasciato in hello **Editor** visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="66d5e-145">Fill out hello forms that appear on hello left in hello **Editor** view.</span></span> <span data-ttu-id="66d5e-146">I campi obbligatori sono contrassegnati con un asterisco rosso (*).</span><span class="sxs-lookup"><span data-stu-id="66d5e-146">Required fields are marked with a red asterisk (*).</span></span>

    ![Impostazioni dell'offerta](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    <span data-ttu-id="66d5e-148">Quattro moduli principali sono utilizzati toocreate un'applicazione gestita:</span><span class="sxs-lookup"><span data-stu-id="66d5e-148">Four main forms are used toocreate a managed application:</span></span>

    <span data-ttu-id="66d5e-149">a.</span><span class="sxs-lookup"><span data-stu-id="66d5e-149">a.</span></span> <span data-ttu-id="66d5e-150">Impostazioni dell'offerta</span><span class="sxs-lookup"><span data-stu-id="66d5e-150">Offer Settings</span></span>

    <span data-ttu-id="66d5e-151">b.</span><span class="sxs-lookup"><span data-stu-id="66d5e-151">b.</span></span> <span data-ttu-id="66d5e-152">SKU</span><span class="sxs-lookup"><span data-stu-id="66d5e-152">SKUs</span></span>

    <span data-ttu-id="66d5e-153">c.</span><span class="sxs-lookup"><span data-stu-id="66d5e-153">c.</span></span> <span data-ttu-id="66d5e-154">Marketplace</span><span class="sxs-lookup"><span data-stu-id="66d5e-154">Marketplace</span></span>

    <span data-ttu-id="66d5e-155">d.</span><span class="sxs-lookup"><span data-stu-id="66d5e-155">d.</span></span> <span data-ttu-id="66d5e-156">Supporto</span><span class="sxs-lookup"><span data-stu-id="66d5e-156">Support</span></span>

<span data-ttu-id="66d5e-157">Questi moduli sono descritti in dettaglio nelle sezioni che seguono hello.</span><span class="sxs-lookup"><span data-stu-id="66d5e-157">These forms are described in greater detail in hello following sections.</span></span>

## <a name="offer-settings-form"></a><span data-ttu-id="66d5e-158">Modulo delle impostazioni dell'offerta</span><span class="sxs-lookup"><span data-stu-id="66d5e-158">Offer Settings form</span></span>
<span data-ttu-id="66d5e-159">Utilizzare le impostazioni di offerta hello toospecify questo form di base.</span><span class="sxs-lookup"><span data-stu-id="66d5e-159">Use this basic form toospecify hello offer settings.</span></span>

1. <span data-ttu-id="66d5e-160">Compilare hello **offrono impostazioni** form.</span><span class="sxs-lookup"><span data-stu-id="66d5e-160">Fill in hello **Offer Settings** form.</span></span> <span data-ttu-id="66d5e-161">Hello diversi campi sono:</span><span class="sxs-lookup"><span data-stu-id="66d5e-161">hello different fields are:</span></span>

    <span data-ttu-id="66d5e-162">a.</span><span class="sxs-lookup"><span data-stu-id="66d5e-162">a.</span></span> <span data-ttu-id="66d5e-163">**ID di offerta**: questo identificatore univoco identifica hello offerta all'interno di un profilo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="66d5e-163">**Offer ID**: This unique identifier identifies hello offer within a publisher profile.</span></span> <span data-ttu-id="66d5e-164">Questo ID è visibile negli URL dei prodotti, nei modelli di Resource Manager e nei report di fatturazione.</span><span class="sxs-lookup"><span data-stu-id="66d5e-164">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="66d5e-165">Può essere composto solo da caratteri alfanumerici minuscoli o trattini (-).</span><span class="sxs-lookup"><span data-stu-id="66d5e-165">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="66d5e-166">Hello ID non può terminare con un trattino.</span><span class="sxs-lookup"><span data-stu-id="66d5e-166">hello ID can't end in a dash.</span></span> <span data-ttu-id="66d5e-167">È limitato tooa massimo 50 caratteri.</span><span class="sxs-lookup"><span data-stu-id="66d5e-167">It's limited tooa maximum of 50 characters.</span></span> <span data-ttu-id="66d5e-168">Questo campo è bloccato dopo la pubblicazione dell'offerta.</span><span class="sxs-lookup"><span data-stu-id="66d5e-168">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="66d5e-169">b.</span><span class="sxs-lookup"><span data-stu-id="66d5e-169">b.</span></span> <span data-ttu-id="66d5e-170">**ID dell'editore**: usare questo profilo di pubblicazione riepilogo toochoose hello desiderato toopublish questa offerta in.</span><span class="sxs-lookup"><span data-stu-id="66d5e-170">**Publisher ID**: Use this drop-down list toochoose hello publisher profile you want toopublish this offer under.</span></span> <span data-ttu-id="66d5e-171">Questo campo è bloccato dopo la pubblicazione dell'offerta.</span><span class="sxs-lookup"><span data-stu-id="66d5e-171">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="66d5e-172">c.</span><span class="sxs-lookup"><span data-stu-id="66d5e-172">c.</span></span> <span data-ttu-id="66d5e-173">**Nome**: viene visualizzato questo nome per l'offerta in Marketplace hello e nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="66d5e-173">**Name**: This display name for your offer appears in hello Marketplace and in hello portal.</span></span> <span data-ttu-id="66d5e-174">Può contenere massimo 50 caratteri.</span><span class="sxs-lookup"><span data-stu-id="66d5e-174">It can have a maximum of 50 characters.</span></span> <span data-ttu-id="66d5e-175">Includere un nome di marchio riconoscibile per il prodotto.</span><span class="sxs-lookup"><span data-stu-id="66d5e-175">Include a recognizable brand name for your product.</span></span> <span data-ttu-id="66d5e-176">Non includere il nome della società, a meno che non corrisponda al nome con cui viene commercializzato.</span><span class="sxs-lookup"><span data-stu-id="66d5e-176">Don't include your company name here unless that's how it's marketed.</span></span> <span data-ttu-id="66d5e-177">Se si sta marketing questa offerta nel proprio sito Web, verificare che il nome hello sia esattamente come viene visualizzato nel sito Web.</span><span class="sxs-lookup"><span data-stu-id="66d5e-177">If you're marketing this offer on your own website, ensure that hello name is exactly how it appears on your website.</span></span>

2. <span data-ttu-id="66d5e-178">Selezionare **salvare** toosave dello stato di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="66d5e-178">Select **Save** toosave your progress.</span></span> 

## <a name="skus-form"></a><span data-ttu-id="66d5e-179">Modulo degli SKU</span><span class="sxs-lookup"><span data-stu-id="66d5e-179">SKUs form</span></span>
<span data-ttu-id="66d5e-180">passaggio successivo Hello è tooadd SKU per l'offerta.</span><span class="sxs-lookup"><span data-stu-id="66d5e-180">hello next step is tooadd SKUs for your offer.</span></span>

1. <span data-ttu-id="66d5e-181">Selezionare **SKU** > **New SKU** (Nuovo SKU).</span><span class="sxs-lookup"><span data-stu-id="66d5e-181">Select **SKUs** > **New SKU**.</span></span> 

    ![Selezionare il nuovo SKU](./media/managed-application-author-marketplace/newOffer_skus.png)

2. <span data-ttu-id="66d5e-183">Immettere un **ID SKU**.</span><span class="sxs-lookup"><span data-stu-id="66d5e-183">Enter a **SKU ID**.</span></span> <span data-ttu-id="66d5e-184">Un ID SKU è un identificatore univoco per hello SKU all'interno di un'offerta.</span><span class="sxs-lookup"><span data-stu-id="66d5e-184">A SKU ID is a unique identifier for hello SKU within an offer.</span></span> <span data-ttu-id="66d5e-185">Questo ID è visibile negli URL dei prodotti, nei modelli di Resource Manager e nei report di fatturazione.</span><span class="sxs-lookup"><span data-stu-id="66d5e-185">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="66d5e-186">Può essere composto solo da caratteri alfanumerici minuscoli o trattini (-).</span><span class="sxs-lookup"><span data-stu-id="66d5e-186">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="66d5e-187">Hello ID non può terminare con un trattino, ed è limitato tooa massimo 50 caratteri.</span><span class="sxs-lookup"><span data-stu-id="66d5e-187">hello ID can't end in a dash, and it's limited tooa maximum of 50 characters.</span></span> <span data-ttu-id="66d5e-188">Questo campo è bloccato dopo la pubblicazione dell'offerta.</span><span class="sxs-lookup"><span data-stu-id="66d5e-188">After an offer goes live, this field is locked.</span></span> <span data-ttu-id="66d5e-189">All'interno di un'offerta possono essere presenti più SKU.</span><span class="sxs-lookup"><span data-stu-id="66d5e-189">You can have multiple SKUs within an offer.</span></span> <span data-ttu-id="66d5e-190">È necessario uno SKU per ogni immagine Prevedi toopublish.</span><span class="sxs-lookup"><span data-stu-id="66d5e-190">You need a SKU for each image you plan toopublish.</span></span>

3. <span data-ttu-id="66d5e-191">Compilare hello **dettagli di SKU** sezione hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="66d5e-191">Fill out hello **SKU Details** section on hello following form:</span></span>

    ![Fornire il nuovo SKU](./media/managed-application-author-marketplace/newOffer_newsku.png)

    <span data-ttu-id="66d5e-193">Compilare hello seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="66d5e-193">Fill out hello following fields:</span></span>
    
    <span data-ttu-id="66d5e-194">a.</span><span class="sxs-lookup"><span data-stu-id="66d5e-194">a.</span></span> <span data-ttu-id="66d5e-195">**Title** (Titolo): immettere un titolo per lo SKU,</span><span class="sxs-lookup"><span data-stu-id="66d5e-195">**Title**: Enter a title for this SKU.</span></span> <span data-ttu-id="66d5e-196">Questa opzione è disponibile nella raccolta di hello per questo elemento.</span><span class="sxs-lookup"><span data-stu-id="66d5e-196">This title appears in hello gallery for this item.</span></span>

    <span data-ttu-id="66d5e-197">b.</span><span class="sxs-lookup"><span data-stu-id="66d5e-197">b.</span></span> <span data-ttu-id="66d5e-198">**Summary (Riepilogo)**: immettere un breve riepilogo per questo SKU,</span><span class="sxs-lookup"><span data-stu-id="66d5e-198">**Summary**: Enter a short summary for this SKU.</span></span> <span data-ttu-id="66d5e-199">Questo testo viene visualizzato sotto il titolo di hello.</span><span class="sxs-lookup"><span data-stu-id="66d5e-199">This text appears underneath hello title.</span></span>

    <span data-ttu-id="66d5e-200">c.</span><span class="sxs-lookup"><span data-stu-id="66d5e-200">c.</span></span> <span data-ttu-id="66d5e-201">**Descrizione**: immettere una descrizione dettagliata hello SKU.</span><span class="sxs-lookup"><span data-stu-id="66d5e-201">**Description**: Enter a detailed description about hello SKU.</span></span>

    <span data-ttu-id="66d5e-202">d.</span><span class="sxs-lookup"><span data-stu-id="66d5e-202">d.</span></span> <span data-ttu-id="66d5e-203">**Tipo SKU**: hello i valori consentiti sono **applicazione gestita** e **modelli di soluzioni**.</span><span class="sxs-lookup"><span data-stu-id="66d5e-203">**SKU Type**: hello allowed values are **Managed Application** and **Solution Templates**.</span></span> <span data-ttu-id="66d5e-204">In questo caso, selezionare **Managed Application** (Applicazione gestita).</span><span class="sxs-lookup"><span data-stu-id="66d5e-204">For this case, select **Managed Application**.</span></span>

4. <span data-ttu-id="66d5e-205">Compilare hello **i dettagli del pacchetto** sezione hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="66d5e-205">Fill out hello **Package Details** section on hello following form:</span></span>

    ![Pacchetto](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    <span data-ttu-id="66d5e-207">Compilare hello seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="66d5e-207">Fill out hello following fields:</span></span>

    <span data-ttu-id="66d5e-208">a.</span><span class="sxs-lookup"><span data-stu-id="66d5e-208">a.</span></span> <span data-ttu-id="66d5e-209">**Versione corrente**: immettere una versione per il pacchetto di hello caricati.</span><span class="sxs-lookup"><span data-stu-id="66d5e-209">**Current Version**: Enter a version for hello package you upload.</span></span> <span data-ttu-id="66d5e-210">Deve essere nel formato hello `{number}.{number}.{number}{number}`.</span><span class="sxs-lookup"><span data-stu-id="66d5e-210">It should be in hello format `{number}.{number}.{number}{number}`.</span></span>

    <span data-ttu-id="66d5e-211">b.</span><span class="sxs-lookup"><span data-stu-id="66d5e-211">b.</span></span> <span data-ttu-id="66d5e-212">**Selezionare un file di pacchetto**: questo pacchetto contiene i seguenti file vengono compressi in un file ZIP hello:</span><span class="sxs-lookup"><span data-stu-id="66d5e-212">**Select a package file**: This package contains hello following files that are compressed into a .zip file:</span></span>
    * <span data-ttu-id="66d5e-213">**applianceMainTemplate.json**: file di modello di distribuzione hello utilizzati toodeploy hello soluzione/applicazione.</span><span class="sxs-lookup"><span data-stu-id="66d5e-213">**applianceMainTemplate.json**: hello deployment template file that's used toodeploy hello solution/application.</span></span> <span data-ttu-id="66d5e-214">Per informazioni su come file di modello di distribuzione toocreate, vedere [creare il primo modello di gestione risorse di Azure](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="66d5e-214">For information about how toocreate deployment template files, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>
    * <span data-ttu-id="66d5e-215">**appliancecreateUIDefinition.json**: questo file viene utilizzato tramite l'interfaccia hello toogenerate portale Azure hello utente che ha utilizzato tooprovision questa soluzione/applicazione.</span><span class="sxs-lookup"><span data-stu-id="66d5e-215">**appliancecreateUIDefinition.json**: This file is used by hello Azure portal toogenerate hello user interface that's used tooprovision this solution/application.</span></span> <span data-ttu-id="66d5e-216">Per altre informazioni, vedere [Introduzione a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="66d5e-216">For more information, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
    * <span data-ttu-id="66d5e-217">**mainTemplate.json**: il file modello contiene solo risorse di Microsoft.Solution/appliances hello.</span><span class="sxs-lookup"><span data-stu-id="66d5e-217">**mainTemplate.json**: This template file contains only hello Microsoft.Solution/appliances resource.</span></span> <span data-ttu-id="66d5e-218">file mainTemplate Hello include hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="66d5e-218">hello mainTemplate file includes hello following properties:</span></span>

        *  <span data-ttu-id="66d5e-219">**tipo**: utilizzare **Marketplace** per le applicazioni gestite in hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="66d5e-219">**kind**: Use **Marketplace** for managed applications in hello Marketplace.</span></span>
        *  <span data-ttu-id="66d5e-220">**ManagedResourceGroupId**: il gruppo di risorse nella sottoscrizione del cliente hello è distribuite in tutte le risorse di hello definite in applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="66d5e-220">**ManagedResourceGroupId**: This resource group in hello customer's subscription is where all hello resources defined in applianceMainTemplate.json are deployed.</span></span>
        *  <span data-ttu-id="66d5e-221">**PublisherPackageId**: la stringa che identifica in modo univoco il pacchetto di hello.</span><span class="sxs-lookup"><span data-stu-id="66d5e-221">**PublisherPackageId**: This string uniquely identifies hello package.</span></span> <span data-ttu-id="66d5e-222">Fornire il valore di hello in formato hello `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span><span class="sxs-lookup"><span data-stu-id="66d5e-222">Provide hello value in hello format of `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span></span>

<span data-ttu-id="66d5e-223">Ottenere hello **ID offerta** e **ID editore** dal portale di pubblicazione, come illustrato nella seguente immagine hello hello:</span><span class="sxs-lookup"><span data-stu-id="66d5e-223">Obtain hello **Offer ID** and **Publisher ID** from hello publishing portal, as shown in hello following image:</span></span>

![Offer ID (ID offerta)](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
<span data-ttu-id="66d5e-225">Ottenere hello **ID SKU**, come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="66d5e-225">Obtain hello **SKU ID**, as shown in hello following image:</span></span>

![ID SKU](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
<span data-ttu-id="66d5e-227">Ottenere il pacchetto di hello **versione**, come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="66d5e-227">Obtain hello package **Version**, as shown in hello following image:</span></span>

![Versione del pacchetto](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  <span data-ttu-id="66d5e-229">In base a hello precedenti esempi, hello valore **PublisherPackageId** è `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="66d5e-229">Based on hello preceding examples, hello value of **PublisherPackageId** is `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span></span>

  <span data-ttu-id="66d5e-230">mainTemplate.json di esempio:</span><span class="sxs-lookup"><span data-stu-id="66d5e-230">Sample mainTemplate.json:</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify hello name of hello storage account"
        }
      },
      "storageAccountType": {
        "type": "string"
      }
    },
    "variables": {
      "managedResourceGroup": "[concat(resourceGroup().id,uniquestring(resourceGroup().id))]"
    },
    "resources": [{
      "type": "Microsoft.Solutions/appliances",
      "apiVersion": "2016-09-01-preview",
      "name": "[concat(parameters('storageAccountNamePrefix'), '-', 'managed')]",
      "location": "[resourceGroup().location]",
      "kind": "marketplace",
      "properties": {
        "managedResourceGroupId": "[variables('managedResourceGroup')]",
        "PublisherPackageId":"azureappliancetest.ravmanagedapptest.ravpreviewmanagedsku.1.0.0",
        "parameters": {
          "storageAccountName": {
            "value": "[parameters('storageAccountNamePrefix')]"
          },
          "storageAccountType": {
            "value": "[parameters('storageAccountType')]"
          }
        }
      }
    }],
    "outputs": {

    }
  }
  ```

<span data-ttu-id="66d5e-231">Il pacchetto deve contenere tutti i modelli annidati o gli script toosuccessfully necessario effettuare il provisioning di questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="66d5e-231">This package should contain any other nested templates or scripts that are required toosuccessfully provision this application.</span></span> <span data-ttu-id="66d5e-232">Hello mainTemplate.json applianceMainTemplate.json e applianceCreateUIDefinition.json file devono essere presenti nella cartella radice hello.</span><span class="sxs-lookup"><span data-stu-id="66d5e-232">hello mainTemplate.json, applianceMainTemplate.json, and applianceCreateUIDefinition.json files must be present at hello root folder.</span></span>

* <span data-ttu-id="66d5e-233">**Autorizzazioni**: questa proprietà definisce l'accesso e hello livello di accesso che ottiene risorse toohello nelle sottoscrizioni dei clienti.</span><span class="sxs-lookup"><span data-stu-id="66d5e-233">**Authorizations**: This property defines who gets access and hello level of access toohello resources in customers' subscriptions.</span></span> <span data-ttu-id="66d5e-234">server di pubblicazione Hello utilizzarlo applicazione hello toomanage per conto cliente hello.</span><span class="sxs-lookup"><span data-stu-id="66d5e-234">hello publisher can use it toomanage hello application on behalf of hello customer.</span></span>
* <span data-ttu-id="66d5e-235">**PrincipalId**: questa proprietà è l'identificatore di hello Azure Active Directory (Azure AD) di un'applicazione che ha concesso autorizzazioni determinate risorse di hello nella sottoscrizione del cliente hello, un gruppo di utenti o un utente.</span><span class="sxs-lookup"><span data-stu-id="66d5e-235">**PrincipalId**: This property is hello Azure Active Directory (Azure AD) identifier of a user, user group, or application that's granted certain permissions on hello resources in hello customer's subscription.</span></span> <span data-ttu-id="66d5e-236">Definizione di ruolo Hello descritte le autorizzazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="66d5e-236">hello Role Definition describes hello permissions.</span></span> 
* <span data-ttu-id="66d5e-237">**Definizione di ruolo**: questa proprietà è un elenco di tutti i ruoli controllo di accesso basato sui ruoli (RBAC) di incorporati hello fornite da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66d5e-237">**Role Definition**: This property is a list of all hello built-in Role-Based Access Control (RBAC) roles provided by Azure AD.</span></span> <span data-ttu-id="66d5e-238">È possibile selezionare hello ruolo più appropriato alle risorse di hello toomanage toouse per conto cliente hello.</span><span class="sxs-lookup"><span data-stu-id="66d5e-238">You can select hello role that's most appropriate toouse toomanage hello resources on behalf of hello customer.</span></span>

<span data-ttu-id="66d5e-239">È possibile aggiungere più autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="66d5e-239">You can add multiple authorizations.</span></span> <span data-ttu-id="66d5e-240">È consigliabile creare un gruppo di utenti di AD e specificare il relativo ID in **PrincipalId**.</span><span class="sxs-lookup"><span data-stu-id="66d5e-240">We recommend that you create an AD user group and specify its ID in **PrincipalId**.</span></span> <span data-ttu-id="66d5e-241">In questo modo, è possibile aggiungere più utenti toohello gruppo senza necessità di prova prova tooupdate SKU.</span><span class="sxs-lookup"><span data-stu-id="66d5e-241">This way, you can add more users toohello user group without hello need tooupdate hello SKU.</span></span>

<span data-ttu-id="66d5e-242">Per ulteriori informazioni sui ruoli, vedere [introduzione RBAC nel portale di Azure hello](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="66d5e-242">For more information about RBAC, see [Get started with RBAC in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>

## <a name="marketplace-form"></a><span data-ttu-id="66d5e-243">Modulo Marketplace</span><span class="sxs-lookup"><span data-stu-id="66d5e-243">Marketplace form</span></span>

<span data-ttu-id="66d5e-244">chiede di Hello modulo Marketplace per i campi visualizzati nell'hello [Azure Marketplace](https://azuremarketplace.microsoft.com) e hello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="66d5e-244">hello Marketplace form asks for fields that show up on hello [Azure Marketplace](https://azuremarketplace.microsoft.com) and on hello [Azure portal](https://portal.azure.com/).</span></span>

### <a name="preview-subscription-ids"></a><span data-ttu-id="66d5e-245">Preview Subscription IDs (ID sottoscrizione di anteprima)</span><span class="sxs-lookup"><span data-stu-id="66d5e-245">Preview subscription IDs</span></span>

<span data-ttu-id="66d5e-246">Immettere un elenco di ID che può accedere l'offerta di hello dopo la pubblicazione di sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="66d5e-246">Enter a list of Azure subscription IDs that can access hello offer after it's published.</span></span> <span data-ttu-id="66d5e-247">È possibile utilizzare questi offerta di sottoscrizioni elencate vuoti tootest hello visualizzato in anteprima prima di renderlo in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="66d5e-247">You can use these white-listed subscriptions tootest hello previewed offer before you make it live.</span></span> <span data-ttu-id="66d5e-248">È possibile compilare un elenco vuoto di too100 sottoscrizioni nel portale di partner hello.</span><span class="sxs-lookup"><span data-stu-id="66d5e-248">You can compile a white list of up too100 subscriptions in hello partner portal.</span></span>

### <a name="suggested-categories"></a><span data-ttu-id="66d5e-249">Suggested Categories (Categorie suggerite)</span><span class="sxs-lookup"><span data-stu-id="66d5e-249">Suggested categories</span></span>

<span data-ttu-id="66d5e-250">Selezionare le categorie di toofive dall'elenco di hello che l'offerta può essere più associato.</span><span class="sxs-lookup"><span data-stu-id="66d5e-250">Select up toofive categories from hello list that your offer can be best associated with.</span></span> <span data-ttu-id="66d5e-251">Queste categorie sono utilizzati toomap le categorie di prodotti toohello offerta sono disponibili in hello [Azure Marketplace](https://azuremarketplace.microsoft.com) hello e [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="66d5e-251">These categories are used toomap your offer toohello product categories that are available in hello [Azure Marketplace](https://azuremarketplace.microsoft.com) and hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="azure-marketplace"></a><span data-ttu-id="66d5e-252">Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="66d5e-252">Azure Marketplace</span></span>

<span data-ttu-id="66d5e-253">riepilogo Hello dell'applicazione gestita Visualizza hello seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="66d5e-253">hello summary of your managed application displays hello following fields:</span></span>

![Riepilogo del Marketplace](./media/managed-application-author-marketplace/publishvm10.png)

<span data-ttu-id="66d5e-255">Hello **Panoramica** scheda applicazione gestita Visualizza hello seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="66d5e-255">hello **Overview** tab for your managed application displays hello following fields:</span></span>

![Panoramica del Marketplace](./media/managed-application-author-marketplace/publishvm11.png)

<span data-ttu-id="66d5e-257">Hello **piani + prezzi** scheda applicazione gestita Visualizza hello seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="66d5e-257">hello **Plans + Pricing** tab for your managed application displays hello following fields:</span></span>

![Piani del Marketplace](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a><span data-ttu-id="66d5e-259">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="66d5e-259">Azure portal</span></span>

<span data-ttu-id="66d5e-260">riepilogo Hello dell'applicazione gestita Visualizza hello seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="66d5e-260">hello summary of your managed application displays hello following fields:</span></span>

![Riepilogo del portale](./media/managed-application-author-marketplace/publishvm12.png)

<span data-ttu-id="66d5e-262">Panoramica di Hello per l'applicazione gestita Visualizza hello seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="66d5e-262">hello overview for your managed application displays hello following fields:</span></span>

![Panoramica del portale](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a><span data-ttu-id="66d5e-264">Linee guida per il logo</span><span class="sxs-lookup"><span data-stu-id="66d5e-264">Logo guidelines</span></span>

<span data-ttu-id="66d5e-265">Seguire queste linee guida per qualsiasi logo che viene caricato nel portale di Partner di Cloud hello:</span><span class="sxs-lookup"><span data-stu-id="66d5e-265">Follow these guidelines for any logo that you upload in hello Cloud Partner portal:</span></span>

*   <span data-ttu-id="66d5e-266">Hello progettazione di Azure dispone di una tavolozza dei colori semplice.</span><span class="sxs-lookup"><span data-stu-id="66d5e-266">hello Azure design has a simple color palette.</span></span> <span data-ttu-id="66d5e-267">Limita il numero di hello database primario e secondario colori sul logo.</span><span class="sxs-lookup"><span data-stu-id="66d5e-267">Limit hello number of primary and secondary colors on your logo.</span></span>
*   <span data-ttu-id="66d5e-268">colori del tema Hello del portale hello sono bianchi e neri.</span><span class="sxs-lookup"><span data-stu-id="66d5e-268">hello theme colors of hello portal are white and black.</span></span> <span data-ttu-id="66d5e-269">Non utilizzare i colori come colore di sfondo hello per il logo.</span><span class="sxs-lookup"><span data-stu-id="66d5e-269">Don't use these colors as hello background color for your logo.</span></span> <span data-ttu-id="66d5e-270">Usare un colore che rende visibile nel portale di hello del logo.</span><span class="sxs-lookup"><span data-stu-id="66d5e-270">Use a color that makes your logo prominent in hello portal.</span></span> <span data-ttu-id="66d5e-271">Si consiglia di usare colori primari semplici.</span><span class="sxs-lookup"><span data-stu-id="66d5e-271">We recommend simple primary colors.</span></span> <span data-ttu-id="66d5e-272">*Se si utilizza uno sfondo trasparente, assicurarsi che i logo hello e testo non sono bianchi, nero o blu.*</span><span class="sxs-lookup"><span data-stu-id="66d5e-272">*If you use a transparent background, make sure that hello logo and text aren't white, black, or blue.*</span></span>
*   <span data-ttu-id="66d5e-273">Non usare uno sfondo sfumato sul logo hello.</span><span class="sxs-lookup"><span data-stu-id="66d5e-273">Don't use a gradient background on hello logo.</span></span>
*   <span data-ttu-id="66d5e-274">Non inserire testo in logo hello, nemmeno società o nome dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="66d5e-274">Don't place text on hello logo, not even your company or brand name.</span></span> <span data-ttu-id="66d5e-275">Hello aspetto del logo deve essere flat ed evitare le sfumature.</span><span class="sxs-lookup"><span data-stu-id="66d5e-275">hello look and feel of your logo should be flat and avoid gradients.</span></span>
*   <span data-ttu-id="66d5e-276">Assicurarsi che non siano stati estesi logo hello.</span><span class="sxs-lookup"><span data-stu-id="66d5e-276">Make sure hello logo isn't stretched.</span></span>

#### <a name="hero-logo"></a><span data-ttu-id="66d5e-277">Logo alto</span><span class="sxs-lookup"><span data-stu-id="66d5e-277">Hero logo</span></span>

<span data-ttu-id="66d5e-278">logo hero Hello è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="66d5e-278">hello hero logo is optional.</span></span> <span data-ttu-id="66d5e-279">server di pubblicazione Hello possibile scegliere di non tooupload un logo hero.</span><span class="sxs-lookup"><span data-stu-id="66d5e-279">hello publisher can choose not tooupload a hero logo.</span></span> <span data-ttu-id="66d5e-280">Icona hero hello viene caricato, non può essere eliminata.</span><span class="sxs-lookup"><span data-stu-id="66d5e-280">After hello hero icon is uploaded, it can't be deleted.</span></span> <span data-ttu-id="66d5e-281">In quel momento, partner hello deve seguire le linee guida Marketplace hello per le icone hero.</span><span class="sxs-lookup"><span data-stu-id="66d5e-281">At that time, hello partner must follow hello Marketplace guidelines for hero icons.</span></span>

<span data-ttu-id="66d5e-282">Seguire queste linee guida per l'icona del logo hero hello:</span><span class="sxs-lookup"><span data-stu-id="66d5e-282">Follow these guidelines for hello hero logo icon:</span></span>

*   <span data-ttu-id="66d5e-283">nome visualizzato di publisher Hello, hello piano titolo e offerta hello riepilogo lunghe vengono visualizzati in bianco.</span><span class="sxs-lookup"><span data-stu-id="66d5e-283">hello publisher display name, hello plan title, and hello offer long summary are displayed in white.</span></span> <span data-ttu-id="66d5e-284">Pertanto, non utilizzare un colore chiaro per lo sfondo di hello dell'icona hero hello.</span><span class="sxs-lookup"><span data-stu-id="66d5e-284">Therefore, don't use a light color for hello background of hello hero icon.</span></span> <span data-ttu-id="66d5e-285">Lo sfondo nero, bianco o trasparente non è ammesso per le icone del logo alto.</span><span class="sxs-lookup"><span data-stu-id="66d5e-285">A black, white, or transparent background isn't allowed for hero icons.</span></span>
*   <span data-ttu-id="66d5e-286">Dopo l'offerta di hello è elencato, server di pubblicazione hello il nome visualizzato, titolo piano hello, offerta hello riepilogo lunghe e hello **crea** pulsante sono incorporati a livello di codice all'interno di logo hero hello.</span><span class="sxs-lookup"><span data-stu-id="66d5e-286">After hello offer is listed, hello publisher display name, hello plan title, hello offer long summary, and hello **Create** button are embedded programmatically inside hello hero logo.</span></span> <span data-ttu-id="66d5e-287">Di conseguenza, non immettere il testo durante la progettazione logo hero hello.</span><span class="sxs-lookup"><span data-stu-id="66d5e-287">Consequently, don't enter any text while you design hello hero logo.</span></span> <span data-ttu-id="66d5e-288">Lasciare spazio vuoto in hello destra perché include testo hello a livello di codice che lo spazio.</span><span class="sxs-lookup"><span data-stu-id="66d5e-288">Leave empty space on hello right because hello text is included programmatically in that space.</span></span> <span data-ttu-id="66d5e-289">spazio vuoto di Hello per testo hello deve essere 415 x 100 pixel in hello destra.</span><span class="sxs-lookup"><span data-stu-id="66d5e-289">hello empty space for hello text should be 415 x 100 pixels on hello right.</span></span> <span data-ttu-id="66d5e-290">Viene applicato un offset di 370 pixel da sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="66d5e-290">It's offset by 370 pixels from hello left.</span></span>

    ![Esempio di logo alto](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a><span data-ttu-id="66d5e-292">Modulo di supporto</span><span class="sxs-lookup"><span data-stu-id="66d5e-292">Support form</span></span>

<span data-ttu-id="66d5e-293">Compilare hello **supporta** form con il supporto contatti dalla società.</span><span class="sxs-lookup"><span data-stu-id="66d5e-293">Fill out hello **Support** form with support contacts from your company.</span></span> <span data-ttu-id="66d5e-294">ad esempio le informazioni di contatto del supporto tecnico e dell'assistenza clienti.</span><span class="sxs-lookup"><span data-stu-id="66d5e-294">This information might be engineering contacts and customer support contacts.</span></span>

## <a name="publish-an-offer"></a><span data-ttu-id="66d5e-295">Pubblicare un'offerta</span><span class="sxs-lookup"><span data-stu-id="66d5e-295">Publish an offer</span></span>

<span data-ttu-id="66d5e-296">Dopo aver specificato tutte le sezioni di hello, selezionare **pubblica** processo hello toostart che rende il toocustomers disponibili offerta.</span><span class="sxs-lookup"><span data-stu-id="66d5e-296">After you fill out all hello sections, select **Publish** toostart hello process that makes your offer available toocustomers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66d5e-297">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="66d5e-297">Next steps</span></span>

* <span data-ttu-id="66d5e-298">Per le applicazioni toomanaged un'introduzione, vedere [panoramica delle applicazioni gestite](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="66d5e-298">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="66d5e-299">Per informazioni sull'utilizzo di un'applicazione gestita da hello Marketplace, vedere [utilizzare Azure gestite le applicazioni in hello Marketplace](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="66d5e-299">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="66d5e-300">Per informazioni sulla pubblicazione di un'applicazione gestita del catalogo di servizi, vedere [Creare e pubblicare un'applicazione gestita del catalogo di servizi](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="66d5e-300">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="66d5e-301">Per informazioni sull'uso delle applicazioni gestite del catalogo di servizi, vedere [Utilizzare un'applicazione gestita di Azure](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="66d5e-301">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
