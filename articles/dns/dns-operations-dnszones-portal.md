---
title: Gestire le zone DNS in DNS Azure - Portale di Azure | Microsoft Docs
description: "È possibile gestire le zone DNS usando il portale di Azure. Questo articolo illustra come aggiornare, eliminare e creare le zone DNS in DNS di Azure"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/18/2017
ms.author: gwallace
ms.openlocfilehash: 69a509612e6204fc93dd42bf2fe69cb165b5777c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-the-azure-portal"></a><span data-ttu-id="36193-104">Come gestire le zone DNS nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="36193-104">How to manage DNS Zones in the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="36193-105">Portale</span><span class="sxs-lookup"><span data-stu-id="36193-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="36193-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="36193-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="36193-107">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="36193-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="36193-108">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="36193-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="36193-109">Questo articolo spiega come gestire le zone DNS usando il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="36193-109">This article shows you how to manage your DNS zones by using the Azure portal.</span></span> <span data-ttu-id="36193-110">È anche possibile gestire le zone DNS usando l'[interfaccia della riga di comando di Azure](dns-operations-dnszones-cli.md) multipiattaforma o Azure [PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="36193-110">You can also manage your DNS zones using the cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or the Azure [PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="36193-111">Creare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="36193-111">Create a DNS zone</span></span>

1. <span data-ttu-id="36193-112">Accedere al portale di Azure</span><span class="sxs-lookup"><span data-stu-id="36193-112">Sign in to the Azure portal</span></span>
2. <span data-ttu-id="36193-113">Nel menu Hub fare clic su **Nuovo > Rete >** e quindi fare clic su **Zona DNS** per aprire il pannello per creare una zona DNS.</span><span class="sxs-lookup"><span data-stu-id="36193-113">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![Zona DNS](./media/dns-operations-dnszones-portal/openzone650.png)

4. <span data-ttu-id="36193-115">Nel pannello **Crea zona DNS** immettere i valori seguenti, quindi fare clic su **Crea**:</span><span class="sxs-lookup"><span data-stu-id="36193-115">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>


   | <span data-ttu-id="36193-116">**Impostazione**</span><span class="sxs-lookup"><span data-stu-id="36193-116">**Setting**</span></span> | <span data-ttu-id="36193-117">**Valore**</span><span class="sxs-lookup"><span data-stu-id="36193-117">**Value**</span></span> | <span data-ttu-id="36193-118">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="36193-118">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="36193-119">**Nome**</span><span class="sxs-lookup"><span data-stu-id="36193-119">**Name**</span></span>|<span data-ttu-id="36193-120">contoso.com</span><span class="sxs-lookup"><span data-stu-id="36193-120">contoso.com</span></span>|<span data-ttu-id="36193-121">Nome della zona DNS</span><span class="sxs-lookup"><span data-stu-id="36193-121">The name of the DNS zone</span></span>|
   |<span data-ttu-id="36193-122">**Sottoscrizione**</span><span class="sxs-lookup"><span data-stu-id="36193-122">**Subscription**</span></span>|<span data-ttu-id="36193-123">[Sottoscrizione]</span><span class="sxs-lookup"><span data-stu-id="36193-123">[Your subscription]</span></span>|<span data-ttu-id="36193-124">Selezionare una sottoscrizione in cui creare la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="36193-124">Select a subscription to create the DNS zone in.</span></span>|
   |<span data-ttu-id="36193-125">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="36193-125">**Resource group**</span></span>|<span data-ttu-id="36193-126">**Crea nuovo:** contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="36193-126">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="36193-127">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="36193-127">Create a resource group.</span></span> <span data-ttu-id="36193-128">Il nome del gruppo di risorse deve essere univoco all'interno della sottoscrizione selezionata.</span><span class="sxs-lookup"><span data-stu-id="36193-128">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="36193-129">Per altre informazioni sui gruppi di risorse, vedere l'articolo [Panoramica di Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="36193-129">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="36193-130">**Posizione**</span><span class="sxs-lookup"><span data-stu-id="36193-130">**Location**</span></span>|<span data-ttu-id="36193-131">Stati Uniti occidentali</span><span class="sxs-lookup"><span data-stu-id="36193-131">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="36193-132">Il gruppo di risorse indica la località del gruppo di risorse e non ha alcun impatto sulla zona DNS.</span><span class="sxs-lookup"><span data-stu-id="36193-132">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="36193-133">La posizione della zona DNS è sempre "globale" e non viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="36193-133">The DNS zone location is always "global", and is not shown.</span></span>

## <a name="list-dns-zones"></a><span data-ttu-id="36193-134">Elencare le zone DNS</span><span class="sxs-lookup"><span data-stu-id="36193-134">List DNS zones</span></span>

<span data-ttu-id="36193-135">Nel portale di Azure passare a **Altri servizi** > **Rete** > **Zone DNS**.</span><span class="sxs-lookup"><span data-stu-id="36193-135">In the Azure portal, navigate to **More services** > **Networking** > **DNS zones**.</span></span> <span data-ttu-id="36193-136">Ogni zona DNS è una risorsa a sé e in questa vista sono disponibili informazioni quali il numero di set di record e i server dei nomi.</span><span class="sxs-lookup"><span data-stu-id="36193-136">Each DNS zone is it's own resource, information such as number of record-sets and name servers are viewable from this view.</span></span> <span data-ttu-id="36193-137">La colonna **SERVER DEI NOMI** non è presente nella visualizzazione predefinita. Per aggiungerla, fare clic su **Colonne**, selezionare **Server dei nomi** e quindi fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="36193-137">The column **NAME SERVERS** is not in the default view, to add it click **Columns**, select **Name servers** and click **Done**.</span></span>

![elenco delle zone DNS](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a><span data-ttu-id="36193-139">Eliminare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="36193-139">Delete a DNS zone</span></span>

<span data-ttu-id="36193-140">Passare a una zona DNS nel portale.</span><span class="sxs-lookup"><span data-stu-id="36193-140">Navigate to a DNS zone in the portal.</span></span> <span data-ttu-id="36193-141">Nel pannello **Zona DNS** fare clic su **Elimina zona**.</span><span class="sxs-lookup"><span data-stu-id="36193-141">On the **DNS zone** blade, click **Delete zone**.</span></span> <span data-ttu-id="36193-142">Verrà chiesto di confermare l'intenzione di eliminare la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="36193-142">You are prompted to confirm you are wanting to delete the DNS zone.</span></span> <span data-ttu-id="36193-143">L'eliminazione di una zona DNS comporta anche l'eliminazione di tutti i record contenuti nella zona.</span><span class="sxs-lookup"><span data-stu-id="36193-143">Deleting a DNS zone also deletes all the records that are contained in the zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36193-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="36193-144">Next steps</span></span>

<span data-ttu-id="36193-145">Per informazioni su come usare la zona e i record DNS, vedere [Introduzione a DNS Azure con il portale di Azure](dns-getstarted-portal.md).</span><span class="sxs-lookup"><span data-stu-id="36193-145">Learn how to work with your DNS Zone and records by visiting [Get started with Azure DNS using the Azure portal](dns-getstarted-portal.md).</span></span>