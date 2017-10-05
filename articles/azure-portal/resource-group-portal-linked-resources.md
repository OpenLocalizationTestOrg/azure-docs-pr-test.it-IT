---
title: Risorse correlate e collegate nella raccolta dei riquadri
description: Informazioni sulle risorse correlate e collegate visualizzate nella raccolta dei riquadri del portale di anteprima di Azure.
services: azure-portal
documentationcenter: 
author: adamabdelhamed
manager: wpickett
editor: 
ms.assetid: dba96d29-f518-49c8-bfd2-f14cecb44cbf
ms.service: azure-portal
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2015
ms.author: adamab
ms.openlocfilehash: efa7bce26c2c4c153b083e0e34d689a11d27dd16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="related-and-linked-resources-in-the-tile-gallery"></a><span data-ttu-id="c4996-103">Risorse correlate e collegate nella raccolta dei riquadri</span><span class="sxs-lookup"><span data-stu-id="c4996-103">Related and linked resources in the tile gallery</span></span>
<span data-ttu-id="c4996-104">La raccolta dei riquadri consente di trovare riquadri per una particolare risorsa e trascinarli nel pannello corrente.</span><span class="sxs-lookup"><span data-stu-id="c4996-104">The tile gallery enables you to find tiles for a particular resource and drag them onto your current blade.</span></span> <span data-ttu-id="c4996-105">Utilizzando la raccolta dei riquadri è possibile creare viste di gestione estese alle varie risorse.</span><span class="sxs-lookup"><span data-stu-id="c4996-105">Using the tile gallery, you can create management views that span resources.</span></span> <span data-ttu-id="c4996-106">Per qualsiasi risorsa specificata, le risorse correlate includono tutte le risorse nel relativo gruppo di risorse e tutte le risorse che si collegano a o da tale risorsa.</span><span class="sxs-lookup"><span data-stu-id="c4996-106">For any specified resource, the related resources include all the resources in its resource group, and any resources that link to or from the resource.</span></span>

## <a name="linked-resources-in-resource-manager"></a><span data-ttu-id="c4996-107">Risorse collegate in Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c4996-107">Linked resources in Resource Manager</span></span>
<span data-ttu-id="c4996-108">Il collegamento è una funzionalità di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c4996-108">Linking is a feature of the Resource Manager.</span></span>  <span data-ttu-id="c4996-109">Consente di dichiarare le relazioni tra le risorse anche se non si trovano nello stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c4996-109">It enables you to declare relationships between resources even if they do not reside in the same resource group.</span></span> <span data-ttu-id="c4996-110">Il collegamento non ha alcun impatto sul runtime delle risorse, sulla fatturazione e sull'accesso in base al ruolo.</span><span class="sxs-lookup"><span data-stu-id="c4996-110">Linking has no impact on the runtime of your resources, no impact on billing, and no impact on role-based access.</span></span>  <span data-ttu-id="c4996-111">È semplicemente un meccanismo che è possibile usare per rappresentare le relazioni in modo che gli strumenti come la raccolta dei riquadri possano offrire un'esperienza di gestione completa.</span><span class="sxs-lookup"><span data-stu-id="c4996-111">It's simply a mechanism you can use to represent relationships so that tools like the tile gallery can provide a rich management experience.</span></span>  <span data-ttu-id="c4996-112">Gli strumenti possono controllare i collegamenti mediante l'API per i collegamenti e fornire allo stesso tempo esperienze personalizzate per la gestione delle relazioni.</span><span class="sxs-lookup"><span data-stu-id="c4996-112">Your tools can inspect the links using the links API and provide custom relationship management experiences as well.</span></span> 

## <a name="how-do-i-link-my-resources"></a><span data-ttu-id="c4996-113">Come si collegano le risorse?</span><span class="sxs-lookup"><span data-stu-id="c4996-113">How do I link my resources?</span></span>
<span data-ttu-id="c4996-114">Quando si creano risorse tramite il portale o tramite la distribuzione di un modello tramite Azure PowerShell o l'interfaccia della riga di comando di Azure, vengono creati automaticamente collegamenti per alcune risorse dipendenti.</span><span class="sxs-lookup"><span data-stu-id="c4996-114">When you create resources through the portal or by deploying a template through Azure PowerShell or Azure CLI, links are automatically created for some dependent resources.</span></span> <span data-ttu-id="c4996-115">È inoltre possibile collegare le risorse a livello di programmazione tramite l' [API REST Risorse collegate](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="c4996-115">You can also programmatically link resources by using the [Linked Resources REST API](/rest/api/resources/resourcelinks).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4996-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c4996-116">Next steps</span></span>
* <span data-ttu-id="c4996-117">Se è necessaria un'introduzione alla scrittura dei modelli di Resource Manager, vedere [Creazione di modelli](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c4996-117">If you need an introduction to writing Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="c4996-118">Per ulteriori informazioni sull'uso dei gruppi di risorse tramite il portale, vedere [Uso del Portale di Azure per gestire le risorse di Azure](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c4996-118">To understand more about working with resource groups through the portal, see [Using the Azure portal to manage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span></span>

