---
title: aaaManage DNS zone DNS di Azure - portale di Azure | Documenti Microsoft
description: "È possibile gestire le zone DNS utilizzando hello portale di Azure. In questo articolo viene descritto come tooupdate, eliminare e creare le zone DNS in DNS di Azure"
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
ms.openlocfilehash: 0d8ce302bb7126dfe8077a6f3e33418e16fcea64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-hello-azure-portal"></a><span data-ttu-id="22b31-104">Come le zone DNS toomanage nella hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="22b31-104">How toomanage DNS Zones in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="22b31-105">Portale</span><span class="sxs-lookup"><span data-stu-id="22b31-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="22b31-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="22b31-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="22b31-107">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="22b31-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="22b31-108">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="22b31-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="22b31-109">Questo articolo illustra come toomanage zone DNS utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="22b31-109">This article shows you how toomanage your DNS zones by using hello Azure portal.</span></span> <span data-ttu-id="22b31-110">È inoltre possibile gestire le zone DNS utilizzando hello multipiattaforma [CLI di Azure](dns-operations-dnszones-cli.md) o hello Azure [PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="22b31-110">You can also manage your DNS zones using hello cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or hello Azure [PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="22b31-111">Creare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="22b31-111">Create a DNS zone</span></span>

1. <span data-ttu-id="22b31-112">Accedi toohello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="22b31-112">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="22b31-113">Nel menu Hub hello, fare clic su e fare clic su **nuovo > rete >** e quindi fare clic su **zona DNS** blade di zona DNS creare hello tooopen.</span><span class="sxs-lookup"><span data-stu-id="22b31-113">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![Zona DNS](./media/dns-operations-dnszones-portal/openzone650.png)

4. <span data-ttu-id="22b31-115">In hello **zona DNS creare** pannello immettere i seguenti valori hello, quindi fare clic su **crea**:</span><span class="sxs-lookup"><span data-stu-id="22b31-115">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>


   | <span data-ttu-id="22b31-116">**Impostazione**</span><span class="sxs-lookup"><span data-stu-id="22b31-116">**Setting**</span></span> | <span data-ttu-id="22b31-117">**Valore**</span><span class="sxs-lookup"><span data-stu-id="22b31-117">**Value**</span></span> | <span data-ttu-id="22b31-118">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="22b31-118">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="22b31-119">**Nome**</span><span class="sxs-lookup"><span data-stu-id="22b31-119">**Name**</span></span>|<span data-ttu-id="22b31-120">contoso.com</span><span class="sxs-lookup"><span data-stu-id="22b31-120">contoso.com</span></span>|<span data-ttu-id="22b31-121">nome Hello della zona DNS hello</span><span class="sxs-lookup"><span data-stu-id="22b31-121">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="22b31-122">**Sottoscrizione**</span><span class="sxs-lookup"><span data-stu-id="22b31-122">**Subscription**</span></span>|<span data-ttu-id="22b31-123">[Sottoscrizione]</span><span class="sxs-lookup"><span data-stu-id="22b31-123">[Your subscription]</span></span>|<span data-ttu-id="22b31-124">Selezionare una zona DNS di sottoscrizione toocreate hello in.</span><span class="sxs-lookup"><span data-stu-id="22b31-124">Select a subscription toocreate hello DNS zone in.</span></span>|
   |<span data-ttu-id="22b31-125">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="22b31-125">**Resource group**</span></span>|<span data-ttu-id="22b31-126">**Crea nuovo:** contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="22b31-126">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="22b31-127">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="22b31-127">Create a resource group.</span></span> <span data-ttu-id="22b31-128">nome del gruppo di risorse Hello deve essere univoco all'interno di sottoscrizione hello selezionata.</span><span class="sxs-lookup"><span data-stu-id="22b31-128">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="22b31-129">ulteriori informazioni sui gruppi di risorse, leggere hello toolearn [Gestione risorse](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) articolo introduttivo.</span><span class="sxs-lookup"><span data-stu-id="22b31-129">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="22b31-130">**Posizione**</span><span class="sxs-lookup"><span data-stu-id="22b31-130">**Location**</span></span>|<span data-ttu-id="22b31-131">Stati Uniti occidentali</span><span class="sxs-lookup"><span data-stu-id="22b31-131">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="22b31-132">gruppo di risorse Hello fa riferimento il percorso toohello hello del gruppo di risorse e non influisce sulla zona DNS hello.</span><span class="sxs-lookup"><span data-stu-id="22b31-132">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="22b31-133">percorso di zona DNS Hello sono sempre "globale" e non viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="22b31-133">hello DNS zone location is always "global", and is not shown.</span></span>

## <a name="list-dns-zones"></a><span data-ttu-id="22b31-134">Elencare le zone DNS</span><span class="sxs-lookup"><span data-stu-id="22b31-134">List DNS zones</span></span>

<span data-ttu-id="22b31-135">Nel portale di Azure hello, passare troppo**più servizi** > **rete** > **zone DNS**.</span><span class="sxs-lookup"><span data-stu-id="22b31-135">In hello Azure portal, navigate too**More services** > **Networking** > **DNS zones**.</span></span> <span data-ttu-id="22b31-136">Ogni zona DNS è una risorsa a sé e in questa vista sono disponibili informazioni quali il numero di set di record e i server dei nomi.</span><span class="sxs-lookup"><span data-stu-id="22b31-136">Each DNS zone is it's own resource, information such as number of record-sets and name servers are viewable from this view.</span></span> <span data-ttu-id="22b31-137">colonna Hello **server dei nomi** non è nella visualizzazione predefinita di hello, tooadd fare clic su **colonne**selezionare **server dei nomi** e fare clic su **eseguita**.</span><span class="sxs-lookup"><span data-stu-id="22b31-137">hello column **NAME SERVERS** is not in hello default view, tooadd it click **Columns**, select **Name servers** and click **Done**.</span></span>

![elenco delle zone DNS](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a><span data-ttu-id="22b31-139">Eliminare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="22b31-139">Delete a DNS zone</span></span>

<span data-ttu-id="22b31-140">Passare una zona DNS tooa nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="22b31-140">Navigate tooa DNS zone in hello portal.</span></span> <span data-ttu-id="22b31-141">In hello **zona DNS** pannello, fare clic su **Elimina zona**.</span><span class="sxs-lookup"><span data-stu-id="22b31-141">On hello **DNS zone** blade, click **Delete zone**.</span></span> <span data-ttu-id="22b31-142">Si è tooconfirm richiesta che si occupano di zona DNS di hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="22b31-142">You are prompted tooconfirm you are wanting toodelete hello DNS zone.</span></span> <span data-ttu-id="22b31-143">L'eliminazione di una zona DNS elimina inoltre tutti i record contenuti nella zona hello hello.</span><span class="sxs-lookup"><span data-stu-id="22b31-143">Deleting a DNS zone also deletes all hello records that are contained in hello zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22b31-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="22b31-144">Next steps</span></span>

<span data-ttu-id="22b31-145">Informazioni su come toowork con la zona DNS e i record visitando [introduzione DNS di Azure tramite il portale di Azure hello](dns-getstarted-portal.md).</span><span class="sxs-lookup"><span data-stu-id="22b31-145">Learn how toowork with your DNS Zone and records by visiting [Get started with Azure DNS using hello Azure portal](dns-getstarted-portal.md).</span></span>
