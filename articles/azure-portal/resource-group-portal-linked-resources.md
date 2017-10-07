---
title: aaaRelated e le risorse collegate in hello riquadro raccolta
description: Informazioni sulle risorse correlate e collegate che vengono visualizzate nella raccolta di riquadro hello del portale di anteprima di Azure hello.
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
ms.openlocfilehash: c8f99be8e23dc9641ec3cd3169604b33a4b049f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="related-and-linked-resources-in-hello-tile-gallery"></a><span data-ttu-id="31f20-103">Risorse correlate e collegate in hello riquadro raccolta</span><span class="sxs-lookup"><span data-stu-id="31f20-103">Related and linked resources in hello tile gallery</span></span>
<span data-ttu-id="31f20-104">raccolta di riquadro Hello consente toofind riquadri per una particolare risorsa e trascinarli il pannello corrente.</span><span class="sxs-lookup"><span data-stu-id="31f20-104">hello tile gallery enables you toofind tiles for a particular resource and drag them onto your current blade.</span></span> <span data-ttu-id="31f20-105">Usando hello riquadro raccolta, è possibile creare viste di gestione che si estendono su risorse.</span><span class="sxs-lookup"><span data-stu-id="31f20-105">Using hello tile gallery, you can create management views that span resources.</span></span> <span data-ttu-id="31f20-106">Per qualsiasi risorsa specificato, hello correlate risorse includono tutte le risorse di hello relativo gruppo di risorse e le eventuali risorse che si collegano tooor dalla risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="31f20-106">For any specified resource, hello related resources include all hello resources in its resource group, and any resources that link tooor from hello resource.</span></span>

## <a name="linked-resources-in-resource-manager"></a><span data-ttu-id="31f20-107">Risorse collegate in Resource Manager</span><span class="sxs-lookup"><span data-stu-id="31f20-107">Linked resources in Resource Manager</span></span>
<span data-ttu-id="31f20-108">Il collegamento è una funzionalità di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="31f20-108">Linking is a feature of hello Resource Manager.</span></span>  <span data-ttu-id="31f20-109">La procedura permette toodeclare relazioni tra le risorse anche se non risiedono in hello stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="31f20-109">It enables you toodeclare relationships between resources even if they do not reside in hello same resource group.</span></span> <span data-ttu-id="31f20-110">Il collegamento non ha alcun impatto sull'ambiente di esecuzione hello di alcun impatto sull'accesso basato sui ruoli, senza impatto sulla fatturazione e le risorse.</span><span class="sxs-lookup"><span data-stu-id="31f20-110">Linking has no impact on hello runtime of your resources, no impact on billing, and no impact on role-based access.</span></span>  <span data-ttu-id="31f20-111">È semplicemente un meccanismo che è possibile utilizzare le relazioni toorepresent in modo che gli strumenti come raccolta riquadro hello può fornire una gestione avanzata esperienza.</span><span class="sxs-lookup"><span data-stu-id="31f20-111">It's simply a mechanism you can use toorepresent relationships so that tools like hello tile gallery can provide a rich management experience.</span></span>  <span data-ttu-id="31f20-112">Gli strumenti possono controllare i collegamenti di hello tramite collegamenti hello API e fornire l'esperienza nonché della gestione delle relazioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="31f20-112">Your tools can inspect hello links using hello links API and provide custom relationship management experiences as well.</span></span> 

## <a name="how-do-i-link-my-resources"></a><span data-ttu-id="31f20-113">Come si collegano le risorse?</span><span class="sxs-lookup"><span data-stu-id="31f20-113">How do I link my resources?</span></span>
<span data-ttu-id="31f20-114">Quando si creano risorse tramite il portale di hello o distribuzione di un modello tramite Azure PowerShell o l'interfaccia CLI di Azure, vengono creati automaticamente collegamenti per alcune risorse dipendenti.</span><span class="sxs-lookup"><span data-stu-id="31f20-114">When you create resources through hello portal or by deploying a template through Azure PowerShell or Azure CLI, links are automatically created for some dependent resources.</span></span> <span data-ttu-id="31f20-115">È possibile collegare anche a livello di codice alle risorse tramite hello [API REST di risorse collegato](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="31f20-115">You can also programmatically link resources by using hello [Linked Resources REST API](/rest/api/resources/resourcelinks).</span></span>

## <a name="next-steps"></a><span data-ttu-id="31f20-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="31f20-116">Next steps</span></span>
* <span data-ttu-id="31f20-117">Se è necessario modelli di gestione risorse toowriting un'introduzione, vedere [creazione di modelli](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="31f20-117">If you need an introduction toowriting Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="31f20-118">vedere toounderstand più informazioni sull'utilizzo di gruppi di risorse tramite il portale di hello [Using hello toomanage portale Azure le risorse di Azure](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="31f20-118">toounderstand more about working with resource groups through hello portal, see [Using hello Azure portal toomanage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span></span>

