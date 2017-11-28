---
title: aaaGuide toocreating un modello di soluzione hello Marketplace | Documenti Microsoft
description: Istruzioni dettagliate su come toocreate, certificare e distribuire un modello di soluzione Multi-VM immagine per l'acquisto in hello Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e14e05f2-2385-4ce0-b351-0747cb74ba19
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: b0e7067176337dd0d3f6f6ec04c963f80f706ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-solution-template-for-azure-marketplace"></a><span data-ttu-id="a773e-103">Guida toocreate un modello di soluzione di Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="a773e-103">Guide toocreate a solution template for Azure Marketplace</span></span>
<span data-ttu-id="a773e-104">Dopo aver completato il passaggio 1, [creazione di Account e la registrazione][link-acct-creation], è interattiva è al momento della creazione hello di un modello di soluzione Azure compatibile in [tecnici prerequisiti per la creazione di un modello di soluzione](marketplace-publishing-solution-template-creation-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="a773e-104">After completing step 1, [Account creation and registration][link-acct-creation], we guided you on hello creation of an Azure-compatible solution template at [Technical prerequisites for creating a solution template](marketplace-publishing-solution-template-creation-prerequisites.md).</span></span> <span data-ttu-id="a773e-105">Ora è verranno illustrati i passaggi di hello per la creazione di un modello di soluzione per più macchine virtuali di hello [portale pubblicazione] [ link-pubportal] per hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a773e-105">Now we will walk you through hello steps for creating a solution template for multiple VMs on hello [Publishing Portal][link-pubportal] for hello Azure Marketplace.</span></span>

## <a name="create-your-solution-template-offer-in-hello-publishing-portal"></a><span data-ttu-id="a773e-106">Creare l'offerta di modello di soluzione in hello portale di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="a773e-106">Create your solution template offer in hello Publishing Portal</span></span>
<span data-ttu-id="a773e-107">Andare troppo [https://publish.windowsazure.com](http://publish.windowsazure.com). Durante l'accesso per hello prima ora toohello [portale pubblicazione](https://publish.windowsazure.com/), utilizzare hello stesso account con cui è stato registrato profilo venditore della società.</span><span class="sxs-lookup"><span data-stu-id="a773e-107">Go too [https://publish.windowsazure.com](http://publish.windowsazure.com). When signing in for hello first time toohello [Publishing Portal](https://publish.windowsazure.com/), use hello same account with which your company’s seller profile was registered.</span></span> <span data-ttu-id="a773e-108">Successivamente, è possibile aggiungere qualsiasi dipendente della società come co-amministratore in hello portale di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="a773e-108">Later, you can add any employee of your company as a co-admin in hello Publishing Portal.</span></span>

### <a name="1-select-solution-templates"></a><span data-ttu-id="a773e-109">1. Selezionare "Modelli di soluzione"</span><span class="sxs-lookup"><span data-stu-id="a773e-109">1. Select "Solution templates"</span></span>
  ![disegno][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a><span data-ttu-id="a773e-111">2. Creare un nuovo modello di soluzione</span><span class="sxs-lookup"><span data-stu-id="a773e-111">2. Create a new solution template</span></span>
  ![disegno][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a><span data-ttu-id="a773e-113">3. Iniziare con le topologie</span><span class="sxs-lookup"><span data-stu-id="a773e-113">3. Start with topologies</span></span>
<span data-ttu-id="a773e-114">Un modello di soluzione è un tooall "padre" relativo topologie.</span><span class="sxs-lookup"><span data-stu-id="a773e-114">A solution template is a "parent" tooall of its topologies.</span></span> <span data-ttu-id="a773e-115">È possibile definire più topologie in un singolo modello di soluzione/offerta.</span><span class="sxs-lookup"><span data-stu-id="a773e-115">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="a773e-116">Quando un'offerta viene inserita toostaging, esso viene inserito con le relative topologie.</span><span class="sxs-lookup"><span data-stu-id="a773e-116">When an offer is pushed toostaging, it is pushed with all of its topologies.</span></span> <span data-ttu-id="a773e-117">Seguire i passaggi di hello seguito toodefine l'offerta:</span><span class="sxs-lookup"><span data-stu-id="a773e-117">Follow hello steps below toodefine your offer:</span></span>     

* <span data-ttu-id="a773e-118">Creare una topologia: "Identificatore topologia" è in genere nome hello della topologia hello per il modello di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="a773e-118">Create a Topology: “Topology Identifier” is typically hello name of hello topology for hello solution template.</span></span> <span data-ttu-id="a773e-119">Identificatore di topologia Hello viene utilizzato nell'URL di hello, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="a773e-119">hello topology identifier is used in hello URL as shown below:</span></span>

  <span data-ttu-id="a773e-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="a773e-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span></span>

  <span data-ttu-id="a773e-121">Portale di Azure: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="a773e-121">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span></span>
* <span data-ttu-id="a773e-122">Aggiungere una nuova versione</span><span class="sxs-lookup"><span data-stu-id="a773e-122">Add a new version.</span></span>

### <a name="4-get-your-topology-versions-certified"></a><span data-ttu-id="a773e-123">4. Ottenere la certificazione per le versioni della topologia</span><span class="sxs-lookup"><span data-stu-id="a773e-123">4. Get your topology versions certified</span></span>
<span data-ttu-id="a773e-124">Caricare un file zip che contiene tutti i file necessari tooprovision quella versione specifica della topologia hello.</span><span class="sxs-lookup"><span data-stu-id="a773e-124">Upload a zip file that contains all required files tooprovision that particular version of hello topology.</span></span> <span data-ttu-id="a773e-125">Il file zip deve contenere i seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="a773e-125">This zip file must contain hello following:</span></span>

* <span data-ttu-id="a773e-126">File *mainTemplate.json* e *createUiDefinition.json* nella directory radice.</span><span class="sxs-lookup"><span data-stu-id="a773e-126">*mainTemplate.json* and *createUiDefinition.json* file at its root directory.</span></span>
* <span data-ttu-id="a773e-127">Tutti i modelli collegati e tutti gli script necessari.</span><span class="sxs-lookup"><span data-stu-id="a773e-127">Any linked templates and all required scripts.</span></span>

  > [!TIP]
  > <span data-ttu-id="a773e-128">Mentre gli sviluppatori di lavoro per la creazione di soluzioni hello topologie di modello e ottenendoli certificate, business hello, marketing e/o legali reparti della società possono sul contenuto di marketing e legali hello.</span><span class="sxs-lookup"><span data-stu-id="a773e-128">While your developers work on creating hello solution template topologies and getting them certified, hello business, marketing, and/or legal departments of your company can work on hello marketing and legal content.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="a773e-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a773e-129">Next steps</span></span>
<span data-ttu-id="a773e-130">Ora che si crea il modello di soluzione e caricamento del file zip hello, seguire le istruzioni hello hello [Guida contenuto marketing Marketplace](marketplace-publishing-push-to-staging.md) prima push toostaging offerta hello.</span><span class="sxs-lookup"><span data-stu-id="a773e-130">Now that you created your solution template and uploaded hello zip file, please follow hello instructions in hello [Marketplace marketing content guide](marketplace-publishing-push-to-staging.md) before pushing hello offer toostaging.</span></span> <span data-ttu-id="a773e-131">set completo di hello toosee di marketplace la pubblicazione di articoli, visitare [Guida introduttiva: come toopublish un toohello offerta Azure Marketplace](marketplace-publishing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="a773e-131">toosee hello full set of marketplace publishing articles, visit [Getting started: How toopublish an offer toohello Azure Marketplace](marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="a773e-132">Articoli correlati:</span><span class="sxs-lookup"><span data-stu-id="a773e-132">You might also be interested in these related articles:</span></span>

* <span data-ttu-id="a773e-133">Immagini di macchina virtuale: [Informazioni sulle immagini di macchine virtuali in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span><span class="sxs-lookup"><span data-stu-id="a773e-133">VM images: [About Virtual Machine Images in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span></span>
* <span data-ttu-id="a773e-134">Estensioni di macchina virtuale: [Panoramica sull'agente VM e sulle estensioni VM](https://msdn.microsoft.com/library/azure/dn832621.aspx) e [Estensioni VM e funzionalità di Azure](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span><span class="sxs-lookup"><span data-stu-id="a773e-134">VM extensions: [VM Agent and VM Extensions Overview](https://msdn.microsoft.com/library/azure/dn832621.aspx) and [Azure VM Extensions and Features](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span></span>
* <span data-ttu-id="a773e-135">Azure Resource Manager: [Creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) e [Semplici modelli di esempio](https://github.com/rjmax/ArmExamples)</span><span class="sxs-lookup"><span data-stu-id="a773e-135">Azure Resource Manager: [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) and [Simple Template Examples](https://github.com/rjmax/ArmExamples)</span></span>
* <span data-ttu-id="a773e-136">Account di archiviazione limita: [come tooMonitor per la limitazione di Account di archiviazione](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) e [archiviazione Premium](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span><span class="sxs-lookup"><span data-stu-id="a773e-136">Storage account throttles: [How tooMonitor for Storage Account Throttling](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) and [Premium storage](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span></span>

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
