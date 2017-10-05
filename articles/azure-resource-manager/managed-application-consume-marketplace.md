---
title: Utilizzare un'applicazione gestita di Azure in Marketplace| Microsoft Docs
description: Descrive come creare un'applicazione gestita di Azure disponibile tramite Marketplace.
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/11/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: baf456740bddd562391ed64d707f990c8921d710
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="consume-azure-managed-applications-in-the-marketplace"></a><span data-ttu-id="e9ff5-103">Utilizzare un'applicazione gestita di Azure in Marketplace</span><span class="sxs-lookup"><span data-stu-id="e9ff5-103">Consume Azure managed applications in the Marketplace</span></span>

<span data-ttu-id="e9ff5-104">Come illustrato nell'articolo [Panoramica di Applicazione gestita di Azure](managed-application-overview.md), gli scenari nell'esperienza end-to-end sono due.</span><span class="sxs-lookup"><span data-stu-id="e9ff5-104">As discussed in the [Managed Application overview](managed-application-overview.md) article, there are two scenarios in the end to end experience.</span></span> <span data-ttu-id="e9ff5-105">Nel primo l'editore o il fornitore vuole creare un'applicazione gestita che verrà usata dai clienti.</span><span class="sxs-lookup"><span data-stu-id="e9ff5-105">One is the publisher or vendor who wants to create a managed application for use by customers.</span></span> <span data-ttu-id="e9ff5-106">Il secondo è relativo al cliente finale o all'utente dell'applicazione gestita.</span><span class="sxs-lookup"><span data-stu-id="e9ff5-106">The second is the end customer or the consumer of the managed application.</span></span> <span data-ttu-id="e9ff5-107">Questo articolo riguarda il secondo scenario.</span><span class="sxs-lookup"><span data-stu-id="e9ff5-107">This article covers the second scenario.</span></span> <span data-ttu-id="e9ff5-108">Descrive come è possibile distribuire un'applicazione gestita da Microsoft Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e9ff5-108">It describes how you can deploy a managed application from the Microsoft Azure Marketplace.</span></span>

## <a name="create-from-the-marketplace"></a><span data-ttu-id="e9ff5-109">Creare da Marketplace</span><span class="sxs-lookup"><span data-stu-id="e9ff5-109">Create from the Marketplace</span></span>

<span data-ttu-id="e9ff5-110">La distribuzione di un'applicazione gestita da Marketplace è simile alla distribuzione di qualsiasi tipo di risorse da Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e9ff5-110">Deploying a managed application from the Marketplace is similar to deploying any type of resources from the Marketplace.</span></span> 

<span data-ttu-id="e9ff5-111">Nel portale selezionare **+ Nuovo** e cercare il tipo di soluzione da distribuire.</span><span class="sxs-lookup"><span data-stu-id="e9ff5-111">In the portal, select **+ New** and search for the type of solution to deploy.</span></span> <span data-ttu-id="e9ff5-112">Selezionare l'opzione appropriata tra quelle disponibili.</span><span class="sxs-lookup"><span data-stu-id="e9ff5-112">From the available options, select the one you need.</span></span>

![cercare le soluzioni](./media/managed-application-consume-marketplace/search-apps.png)

<span data-ttu-id="e9ff5-114">Esaminare il riepilogo dell'applicazione e selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e9ff5-114">Review the summary of the application, and select **Create**.</span></span>

![creare l'applicazione gestita](./media/managed-application-consume-marketplace/create-marketplace-managed-app.png)

<span data-ttu-id="e9ff5-116">Come per qualsiasi altra soluzione, vengono visualizzati i campi per cui fornire i valori.</span><span class="sxs-lookup"><span data-stu-id="e9ff5-116">Like any other solution, you are presented with fields to provide values for.</span></span> <span data-ttu-id="e9ff5-117">Questi campi variano a seconda del tipo di applicazione gestita creata.</span><span class="sxs-lookup"><span data-stu-id="e9ff5-117">These fields vary by the type of managed application you create.</span></span> 

## <a name="view-support-information"></a><span data-ttu-id="e9ff5-118">Visualizzare le informazioni di supporto</span><span class="sxs-lookup"><span data-stu-id="e9ff5-118">View support information</span></span>

<span data-ttu-id="e9ff5-119">Dopo avere distribuito l'applicazione gestita, visualizzare le informazioni di supporto per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e9ff5-119">After your managed application has deployed, view the support information for the application.</span></span> <span data-ttu-id="e9ff5-120">Nel pannello dell'applicazione gestita sono elencate le informazioni di supporto.</span><span class="sxs-lookup"><span data-stu-id="e9ff5-120">In the managed application blade, the support information is listed.</span></span>

![support](./media/managed-application-consume-marketplace/support.png)

## <a name="view-publisher-permissions"></a><span data-ttu-id="e9ff5-122">Visualizzare le autorizzazioni dell'editore</span><span class="sxs-lookup"><span data-stu-id="e9ff5-122">View publisher permissions</span></span>

<span data-ttu-id="e9ff5-123">Al fornitore che gestisce l'applicazione viene concesso l'accesso alle risorse.</span><span class="sxs-lookup"><span data-stu-id="e9ff5-123">The vendor that manages your application is granted access to your resources.</span></span> <span data-ttu-id="e9ff5-124">Per esaminare queste autorizzazioni, selezionare **Autorizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="e9ff5-124">To see those permissions, select **Authorizations**.</span></span>

![autorizzazioni](./media/managed-application-consume-marketplace/authorizations.png)

## <a name="next-steps"></a><span data-ttu-id="e9ff5-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e9ff5-126">Next steps</span></span>

* <span data-ttu-id="e9ff5-127">Per informazioni sulla pubblicazione di un'applicazione gestita in Marketplace, vedere [Applicazioni gestite di Azure Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="e9ff5-127">For information about publishing a managed application in the Marketplace, see [Azure Managed Applications in Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="e9ff5-128">Per pubblicare le applicazioni gestite disponibili solo per gli utenti dell'organizzazione, vedere [Creare e pubblicare un'applicazione gestita del catalogo di servizi](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="e9ff5-128">To publish managed applications that are only available to users in your organization, see [Create and publish Service Catalog Managed Application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="e9ff5-129">Per usare le applicazioni gestite disponibili solo per gli utenti dell'organizzazione, vedere [Utilizzare un'applicazione gestita del catalogo di servizi](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="e9ff5-129">To consume managed applications that are only available to users in your organization, see [Consume a Service Catalog Managed Application](managed-application-consumption.md).</span></span>