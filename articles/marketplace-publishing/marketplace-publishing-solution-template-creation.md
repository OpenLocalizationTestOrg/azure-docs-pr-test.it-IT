---
title: Guida alla creazione di un modello di soluzione per il Marketplace | Documentazione Microsoft
description: "Istruzioni dettagliate su come creare, certificare e distribuire un modello di soluzione con un'immagine con più macchine virtuali per l'acquisto in Azure Marketplace."
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
ms.openlocfilehash: b753bfb4bd69bd9aacf4eebd8999397394c28bc4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="guide-to-create-a-solution-template-for-azure-marketplace"></a><span data-ttu-id="7d3e8-103">Guida alla creazione di un modello di soluzione per Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="7d3e8-103">Guide to create a solution template for Azure Marketplace</span></span>
<span data-ttu-id="7d3e8-104">Dopo aver completato il passaggio 1, [Creazione e registrazione dell'account][link-acct-creation], sono state fornite indicazioni per la creazione di un modello di soluzione compatibile con Azure in [Prerequisiti tecnici per la creazione di un modello di soluzione](marketplace-publishing-solution-template-creation-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="7d3e8-104">After completing step 1, [Account creation and registration][link-acct-creation], we guided you on the creation of an Azure-compatible solution template at [Technical prerequisites for creating a solution template](marketplace-publishing-solution-template-creation-prerequisites.md).</span></span> <span data-ttu-id="7d3e8-105">Ora verranno illustrati i passaggi per la creazione di un modello di soluzione per più macchine virtuali nel [portale di pubblicazione][link-pubportal] per Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="7d3e8-105">Now we will walk you through the steps for creating a solution template for multiple VMs on the [Publishing Portal][link-pubportal] for the Azure Marketplace.</span></span>

## <a name="create-your-solution-template-offer-in-the-publishing-portal"></a><span data-ttu-id="7d3e8-106">Creare l'offerta di modello di soluzione nel portale di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="7d3e8-106">Create your solution template offer in the Publishing Portal</span></span>
<span data-ttu-id="7d3e8-107">Passare alla pagina [https://publish.windowsazure.com](http://publish.windowsazure.com). Quando si accede per la prima volta al [portale di pubblicazione](https://publish.windowsazure.com/), usare lo stesso account con cui è stato registrato il profilo venditore dell'azienda.</span><span class="sxs-lookup"><span data-stu-id="7d3e8-107">Go to  [https://publish.windowsazure.com](http://publish.windowsazure.com). When signing in for the first time to the [Publishing Portal](https://publish.windowsazure.com/), use the same account with which your company’s seller profile was registered.</span></span> <span data-ttu-id="7d3e8-108">Successivamente è possibile aggiungere qualsiasi dipendente dell'azienda come coamministratore nel portale di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="7d3e8-108">Later, you can add any employee of your company as a co-admin in the Publishing Portal.</span></span>

### <a name="1-select-solution-templates"></a><span data-ttu-id="7d3e8-109">1. Selezionare "Modelli di soluzione"</span><span class="sxs-lookup"><span data-stu-id="7d3e8-109">1. Select "Solution templates"</span></span>
  ![disegno][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a><span data-ttu-id="7d3e8-111">2. Creare un nuovo modello di soluzione</span><span class="sxs-lookup"><span data-stu-id="7d3e8-111">2. Create a new solution template</span></span>
  ![disegno][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a><span data-ttu-id="7d3e8-113">3. Iniziare con le topologie</span><span class="sxs-lookup"><span data-stu-id="7d3e8-113">3. Start with topologies</span></span>
<span data-ttu-id="7d3e8-114">Un modello di soluzione è un elemento padre per tutte le relative topologie.</span><span class="sxs-lookup"><span data-stu-id="7d3e8-114">A solution template is a "parent" to all of its topologies.</span></span> <span data-ttu-id="7d3e8-115">È possibile definire più topologie in un singolo modello di soluzione/offerta.</span><span class="sxs-lookup"><span data-stu-id="7d3e8-115">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="7d3e8-116">Quando un'offerta passa alla fase di gestione temporanea, passano a tale fase anche tutte le relative topologie.</span><span class="sxs-lookup"><span data-stu-id="7d3e8-116">When an offer is pushed to staging, it is pushed with all of its topologies.</span></span> <span data-ttu-id="7d3e8-117">Per definire l'offerta, eseguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7d3e8-117">Follow the steps below to define your offer:</span></span>     

* <span data-ttu-id="7d3e8-118">Creare una topologia. "Identificatore topologia" è in genere il nome della topologia per il modello di soluzione.</span><span class="sxs-lookup"><span data-stu-id="7d3e8-118">Create a Topology: “Topology Identifier” is typically the name of the topology for the solution template.</span></span> <span data-ttu-id="7d3e8-119">L'identificatore topologia viene usato nell'URL come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7d3e8-119">The topology identifier is used in the URL as shown below:</span></span>

  <span data-ttu-id="7d3e8-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="7d3e8-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span></span>

  <span data-ttu-id="7d3e8-121">Portale di Azure: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="7d3e8-121">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span></span>
* <span data-ttu-id="7d3e8-122">Aggiungere una nuova versione</span><span class="sxs-lookup"><span data-stu-id="7d3e8-122">Add a new version.</span></span>

### <a name="4-get-your-topology-versions-certified"></a><span data-ttu-id="7d3e8-123">4. Ottenere la certificazione per le versioni della topologia</span><span class="sxs-lookup"><span data-stu-id="7d3e8-123">4. Get your topology versions certified</span></span>
<span data-ttu-id="7d3e8-124">Caricare un file ZIP contenente tutti i file necessari per eseguire il provisioning della specifica versione della topologia.</span><span class="sxs-lookup"><span data-stu-id="7d3e8-124">Upload a zip file that contains all required files to provision that particular version of the topology.</span></span> <span data-ttu-id="7d3e8-125">Il file zip deve contenere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="7d3e8-125">This zip file must contain the following:</span></span>

* <span data-ttu-id="7d3e8-126">File *mainTemplate.json* e *createUiDefinition.json* nella directory radice.</span><span class="sxs-lookup"><span data-stu-id="7d3e8-126">*mainTemplate.json* and *createUiDefinition.json* file at its root directory.</span></span>
* <span data-ttu-id="7d3e8-127">Tutti i modelli collegati e tutti gli script necessari.</span><span class="sxs-lookup"><span data-stu-id="7d3e8-127">Any linked templates and all required scripts.</span></span>

  > [!TIP]
  > <span data-ttu-id="7d3e8-128">Mentre gli sviluppatori lavorano alla creazione delle topologie del modello di soluzione e alla relativa certificazione, il reparto commerciale, marketing e/o legale dell'azienda può occuparsi dei contenuti di marketing e legali.</span><span class="sxs-lookup"><span data-stu-id="7d3e8-128">While your developers work on creating the solution template topologies and getting them certified, the business, marketing, and/or legal departments of your company can work on the marketing and legal content.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="7d3e8-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7d3e8-129">Next steps</span></span>
<span data-ttu-id="7d3e8-130">Ora che il modello di soluzione è stato creato e il file zip caricato, seguire le istruzioni di [guida sui contenuti di marketing di Azure Marketplace](marketplace-publishing-push-to-staging.md) prima di eseguire il passaggio dell'offerta alla gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="7d3e8-130">Now that you created your solution template and uploaded the zip file, please follow the instructions in the [Marketplace marketing content guide](marketplace-publishing-push-to-staging.md) before pushing the offer to staging.</span></span> <span data-ttu-id="7d3e8-131">Per visualizzare il set completo di articoli di pubblicazione nel Marketplace, visitare [Come pubblicare e gestire un'offerta in Azure Marketplace](marketplace-publishing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="7d3e8-131">To see the full set of marketplace publishing articles, visit [Getting started: How to publish an offer to the Azure Marketplace](marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="7d3e8-132">Articoli correlati:</span><span class="sxs-lookup"><span data-stu-id="7d3e8-132">You might also be interested in these related articles:</span></span>

* <span data-ttu-id="7d3e8-133">Immagini di macchina virtuale: [Informazioni sulle immagini di macchine virtuali in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span><span class="sxs-lookup"><span data-stu-id="7d3e8-133">VM images: [About Virtual Machine Images in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span></span>
* <span data-ttu-id="7d3e8-134">Estensioni di macchina virtuale: [Panoramica sull'agente VM e sulle estensioni VM](https://msdn.microsoft.com/library/azure/dn832621.aspx) e [Estensioni VM e funzionalità di Azure](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span><span class="sxs-lookup"><span data-stu-id="7d3e8-134">VM extensions: [VM Agent and VM Extensions Overview](https://msdn.microsoft.com/library/azure/dn832621.aspx) and [Azure VM Extensions and Features](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span></span>
* <span data-ttu-id="7d3e8-135">Azure Resource Manager: [Creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) e [Semplici modelli di esempio](https://github.com/rjmax/ArmExamples)</span><span class="sxs-lookup"><span data-stu-id="7d3e8-135">Azure Resource Manager: [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) and [Simple Template Examples](https://github.com/rjmax/ArmExamples)</span></span>
* <span data-ttu-id="7d3e8-136">Limitazioni degli account di archiviazione: [Post di blog relativo al monitoraggio della limitazione degli account di archiviazione](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) e [Archiviazione Premium](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span><span class="sxs-lookup"><span data-stu-id="7d3e8-136">Storage account throttles: [How to Monitor for Storage Account Throttling](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) and [Premium storage](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span></span>

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
