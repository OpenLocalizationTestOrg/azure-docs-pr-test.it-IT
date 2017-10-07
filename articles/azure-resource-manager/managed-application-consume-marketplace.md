---
title: Applicazione gestita da Azure Marketplace aaaConsume | Documenti Microsoft
description: "Describeshow toocreate un'applicazione gestita da Azure che è disponibile tramite Marketplace hello."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/11/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 9ae6e11a3f63eb58a9f3199364b5606a7afe5618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="consume-azure-managed-applications-in-hello-marketplace"></a><span data-ttu-id="3c0ea-103">Utilizzare Azure dalle applicazioni di hello Marketplace gestito</span><span class="sxs-lookup"><span data-stu-id="3c0ea-103">Consume Azure managed applications in hello Marketplace</span></span>

<span data-ttu-id="3c0ea-104">Come descritto in hello [panoramica delle applicazioni gestite](managed-application-overview.md) articolo, esistono due scenari hello fine tooend esperienza.</span><span class="sxs-lookup"><span data-stu-id="3c0ea-104">As discussed in hello [Managed Application overview](managed-application-overview.md) article, there are two scenarios in hello end tooend experience.</span></span> <span data-ttu-id="3c0ea-105">Uno è publisher hello o fornitore che desiderano toocreate un'applicazione gestita per l'utilizzo da parte dei clienti.</span><span class="sxs-lookup"><span data-stu-id="3c0ea-105">One is hello publisher or vendor who wants toocreate a managed application for use by customers.</span></span> <span data-ttu-id="3c0ea-106">Hello è secondo cliente finale hello o consumer hello di un'applicazione hello gestito.</span><span class="sxs-lookup"><span data-stu-id="3c0ea-106">hello second is hello end customer or hello consumer of hello managed application.</span></span> <span data-ttu-id="3c0ea-107">Questo articolo descrive il secondo scenario hello.</span><span class="sxs-lookup"><span data-stu-id="3c0ea-107">This article covers hello second scenario.</span></span> <span data-ttu-id="3c0ea-108">Viene descritto come è possibile distribuire un'applicazione gestita da Microsoft Azure Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="3c0ea-108">It describes how you can deploy a managed application from hello Microsoft Azure Marketplace.</span></span>

## <a name="create-from-hello-marketplace"></a><span data-ttu-id="3c0ea-109">Il nome di hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="3c0ea-109">Create from hello Marketplace</span></span>

<span data-ttu-id="3c0ea-110">La distribuzione di un'applicazione gestita da hello Marketplace è simile toodeploying qualsiasi tipo di risorse da hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3c0ea-110">Deploying a managed application from hello Marketplace is similar toodeploying any type of resources from hello Marketplace.</span></span> 

<span data-ttu-id="3c0ea-111">Nel portale di hello selezionare **+ nuovo** e cercare hello tipo di soluzione toodeploy.</span><span class="sxs-lookup"><span data-stu-id="3c0ea-111">In hello portal, select **+ New** and search for hello type of solution toodeploy.</span></span> <span data-ttu-id="3c0ea-112">Selezionare opzioni hello hello uno che è necessario.</span><span class="sxs-lookup"><span data-stu-id="3c0ea-112">From hello available options, select hello one you need.</span></span>

![cercare le soluzioni](./media/managed-application-consume-marketplace/search-apps.png)

<span data-ttu-id="3c0ea-114">Rivedere il riepilogo di hello di un'applicazione hello e selezionare **crea**.</span><span class="sxs-lookup"><span data-stu-id="3c0ea-114">Review hello summary of hello application, and select **Create**.</span></span>

![creare l'applicazione gestita](./media/managed-application-consume-marketplace/create-marketplace-managed-app.png)

<span data-ttu-id="3c0ea-116">Come qualsiasi altra soluzione, vengono visualizzate con valori di campi tooprovide per.</span><span class="sxs-lookup"><span data-stu-id="3c0ea-116">Like any other solution, you are presented with fields tooprovide values for.</span></span> <span data-ttu-id="3c0ea-117">Questi campi variano in base a tipo hello di creazione di applicazioni gestite.</span><span class="sxs-lookup"><span data-stu-id="3c0ea-117">These fields vary by hello type of managed application you create.</span></span> 

## <a name="view-support-information"></a><span data-ttu-id="3c0ea-118">Visualizzare le informazioni di supporto</span><span class="sxs-lookup"><span data-stu-id="3c0ea-118">View support information</span></span>

<span data-ttu-id="3c0ea-119">Dopo aver distribuito l'applicazione gestita, consente di visualizzare informazioni di supporto hello per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3c0ea-119">After your managed application has deployed, view hello support information for hello application.</span></span> <span data-ttu-id="3c0ea-120">Nel Pannello di hello applicazione gestita, le informazioni di supporto hello sono elencate.</span><span class="sxs-lookup"><span data-stu-id="3c0ea-120">In hello managed application blade, hello support information is listed.</span></span>

![support](./media/managed-application-consume-marketplace/support.png)

## <a name="view-publisher-permissions"></a><span data-ttu-id="3c0ea-122">Visualizzare le autorizzazioni dell'editore</span><span class="sxs-lookup"><span data-stu-id="3c0ea-122">View publisher permissions</span></span>

<span data-ttu-id="3c0ea-123">fornitore Hello che gestisce l'applicazione viene concessa tooyour di accedere alle risorse.</span><span class="sxs-lookup"><span data-stu-id="3c0ea-123">hello vendor that manages your application is granted access tooyour resources.</span></span> <span data-ttu-id="3c0ea-124">Selezionare le autorizzazioni, toosee **autorizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="3c0ea-124">toosee those permissions, select **Authorizations**.</span></span>

![autorizzazioni](./media/managed-application-consume-marketplace/authorizations.png)

## <a name="next-steps"></a><span data-ttu-id="3c0ea-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3c0ea-126">Next steps</span></span>

* <span data-ttu-id="3c0ea-127">Per informazioni sulla pubblicazione di un'applicazione gestita in hello Marketplace, vedere [applicazioni gestite di Azure Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="3c0ea-127">For information about publishing a managed application in hello Marketplace, see [Azure Managed Applications in Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="3c0ea-128">toopublish gestite le applicazioni che sono solo disponibili toousers nell'organizzazione, vedere [creare e pubblicare l'applicazione di servizio catalogo gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="3c0ea-128">toopublish managed applications that are only available toousers in your organization, see [Create and publish Service Catalog Managed Application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="3c0ea-129">tooconsume gestite le applicazioni che sono solo disponibili toousers nell'organizzazione, vedere [utilizzare un'applicazione del servizio catalogo gestiti](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="3c0ea-129">tooconsume managed applications that are only available toousers in your organization, see [Consume a Service Catalog Managed Application](managed-application-consumption.md).</span></span>
