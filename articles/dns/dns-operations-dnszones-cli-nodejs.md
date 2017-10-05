---
title: Gestire le zone DNS in DNS di Azure - Interfaccia della riga di comando di Azure 1.0 | Documentazione Microsoft
description: "È possibile gestire le zone DNS usando l'interfaccia della riga di comando Azure 1.0. Questo articolo illustra come aggiornare, eliminare e creare le zone DNS in DNS di Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: 588c87749f049eff5b9e0729f6769c8367ba41e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-azure-dns-using-the-azure-cli-10"></a><span data-ttu-id="ba41f-104">Come gestire le zone DNS in DNS di Azure DNS usando l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="ba41f-104">How to manage DNS Zones in Azure DNS using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ba41f-105">Portale</span><span class="sxs-lookup"><span data-stu-id="ba41f-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="ba41f-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba41f-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="ba41f-107">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="ba41f-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="ba41f-108">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="ba41f-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="ba41f-109">Questa guida illustra come gestire le zone DNS usando l'interfaccia della riga di comando di Azure 1.0 multipiattaforma, disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="ba41f-109">This guide shows how to manage your DNS zones by using the cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="ba41f-110">È anche possibile gestire le zone DNS usando [Azure PowerShell](dns-operations-dnszones.md) o il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba41f-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or the Azure portal.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="ba41f-111">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="ba41f-111">CLI versions to complete the task</span></span>

<span data-ttu-id="ba41f-112">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="ba41f-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="ba41f-113">[Interfaccia della riga di comando di Azure 1.0](dns-operations-dnszones-cli-nodejs.md): l'interfaccia della riga di comando per il modello di distribuzione classico e di gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="ba41f-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="ba41f-114">[Interfaccia della riga di comando di Azure 2.0](dns-operations-dnszones-cli.md): interfaccia avanzata per il modello di distribuzione di gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="ba41f-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="ba41f-115">Introduzione</span><span class="sxs-lookup"><span data-stu-id="ba41f-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a><span data-ttu-id="ba41f-116">Risorse della Guida</span><span class="sxs-lookup"><span data-stu-id="ba41f-116">Getting help</span></span>

<span data-ttu-id="ba41f-117">Tutti i comandi dell'interfaccia della riga di comando 1.0 relativi a DNS di Azure iniziano con `azure network dns`.</span><span class="sxs-lookup"><span data-stu-id="ba41f-117">All CLI 1.0 commands relating to Azure DNS start with `azure network dns`.</span></span> <span data-ttu-id="ba41f-118">Sono disponibili informazioni per ogni comando tramite l'opzione `--help` (forma breve `-h`).</span><span class="sxs-lookup"><span data-stu-id="ba41f-118">Help is available for each command using the `--help` option (short form `-h`).</span></span>  <span data-ttu-id="ba41f-119">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ba41f-119">For example:</span></span>

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="ba41f-120">Creare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="ba41f-120">Create a DNS zone</span></span>

<span data-ttu-id="ba41f-121">Una zona DNS viene creata utilizzando il comando `azure network dns zone create` .</span><span class="sxs-lookup"><span data-stu-id="ba41f-121">A DNS zone is created using the `azure network dns zone create` command.</span></span> <span data-ttu-id="ba41f-122">Per altre informazioni, vedere `azure network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="ba41f-122">For help, see `azure network dns zone create -h`.</span></span>

<span data-ttu-id="ba41f-123">L'esempio seguente crea una zona DNS denominata *contoso.com* nel gruppo di risorse denominato *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="ba41f-123">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="to-create-a-dns-zone-with-tags"></a><span data-ttu-id="ba41f-124">Per creare una zona DNS con tag</span><span class="sxs-lookup"><span data-stu-id="ba41f-124">To create a DNS zone with tags</span></span>

<span data-ttu-id="ba41f-125">L'esempio seguente illustra come creare una zona DNS con due [tag di Azure Resource Manager](dns-zones-records.md#tags), *project = demo* ed *env = test*, usando il parametro `--tags` (forma breve `-t`):</span><span class="sxs-lookup"><span data-stu-id="ba41f-125">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using the `--tags` parameter (short form `-t`):</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="ba41f-126">Ottenere una zona DNS</span><span class="sxs-lookup"><span data-stu-id="ba41f-126">Get a DNS zone</span></span>

<span data-ttu-id="ba41f-127">Per recuperare una zona DNS, usare `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="ba41f-127">To retrieve a DNS zone, use `azure network dns zone show`.</span></span> <span data-ttu-id="ba41f-128">Per altre informazioni, vedere `azure network dns zone show -h`.</span><span class="sxs-lookup"><span data-stu-id="ba41f-128">For help, see `azure network dns zone show -h`.</span></span>

<span data-ttu-id="ba41f-129">L'esempio seguente restituisce la zona DNS *contoso.com* e i relativi dati associati dal gruppo di risorse *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="ba41f-129">The following example returns the DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

<span data-ttu-id="ba41f-130">L'esempio seguente corrisponde alla risposta.</span><span class="sxs-lookup"><span data-stu-id="ba41f-130">The following example is the response.</span></span>

```
info:    Executing command network dns zone show
+ Looking up the dns zone "contoso.com"
data:    Id                              : /subscriptions/.../contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 2
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            : project=demo;env=test
info:    network dns zone show command OK
```

<span data-ttu-id="ba41f-131">Si noti che i record DNS non vengono restituiti da `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="ba41f-131">Note that DNS records are not returned by `azure network dns zone show`.</span></span> <span data-ttu-id="ba41f-132">Per elencare i record DNS, usare `azure network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="ba41f-132">To list DNS records, use `azure network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="ba41f-133">Elencare le zone DNS</span><span class="sxs-lookup"><span data-stu-id="ba41f-133">List DNS zones</span></span>

<span data-ttu-id="ba41f-134">Per enumerare le zone DNS, usare `azure network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="ba41f-134">To enumerate DNS zones, use `azure network dns zone list`.</span></span> <span data-ttu-id="ba41f-135">Per altre informazioni, vedere `azure network dns zone list -h`.</span><span class="sxs-lookup"><span data-stu-id="ba41f-135">For help, see `azure network dns zone list -h`.</span></span>

<span data-ttu-id="ba41f-136">Se si specifica il gruppo di risorse, vengono elencate solo le zone all'interno del gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="ba41f-136">Specifying the resource group lists only those zones within the resource group:</span></span>

```azurecli
azure network dns zone list MyResourceGroup
```

<span data-ttu-id="ba41f-137">Se invece il gruppo di risorse viene omesso, sono elencate tutte le zone nella sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="ba41f-137">Omitting the resource group lists all zones in the subscription:</span></span>

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="ba41f-138">Aggiornare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="ba41f-138">Update a DNS zone</span></span>

<span data-ttu-id="ba41f-139">È possibile apportare modifiche a una risorsa di zona DNS usando `azure network dns zone set`.</span><span class="sxs-lookup"><span data-stu-id="ba41f-139">Changes to a DNS zone resource can be made using `azure network dns zone set`.</span></span> <span data-ttu-id="ba41f-140">Per altre informazioni, vedere `azure network dns zone set -h`.</span><span class="sxs-lookup"><span data-stu-id="ba41f-140">For help, see `azure network dns zone set -h`.</span></span>

<span data-ttu-id="ba41f-141">Questo comando non consente di aggiornare alcun set di record DNS compreso nella zona (vedere [Come gestire i record DNS](dns-operations-recordsets-cli-nodejs.md)).</span><span class="sxs-lookup"><span data-stu-id="ba41f-141">This command does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets-cli-nodejs.md)).</span></span> <span data-ttu-id="ba41f-142">Questa operazione permette solo di aggiornare le proprietà della risorsa di zona stessa.</span><span class="sxs-lookup"><span data-stu-id="ba41f-142">It is only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="ba41f-143">Queste proprietà sono attualmente limitate ai ["tag" di Azure Resource Manager](dns-zones-records.md#tags) relativi alla risorsa di zona.</span><span class="sxs-lookup"><span data-stu-id="ba41f-143">These properties are currently limited to the [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for the zone resource.</span></span>

<span data-ttu-id="ba41f-144">L'esempio seguente illustra come aggiornare i tag in una zona DNS.</span><span class="sxs-lookup"><span data-stu-id="ba41f-144">The following example shows how to update the tags on a DNS zone.</span></span> <span data-ttu-id="ba41f-145">I tag esistenti vengono sostituiti dal valore specificato.</span><span class="sxs-lookup"><span data-stu-id="ba41f-145">The existing tags are replaced by the value specified.</span></span>

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="ba41f-146">Eliminare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="ba41f-146">Delete a DNS Zone</span></span>

<span data-ttu-id="ba41f-147">Le zone DNS possono essere eliminate usando `azure network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="ba41f-147">DNS zones can be deleted using `azure network dns zone delete`.</span></span> <span data-ttu-id="ba41f-148">Per altre informazioni, vedere `azure network dns zone delete -h`.</span><span class="sxs-lookup"><span data-stu-id="ba41f-148">For help, see `azure network dns zone delete -h`.</span></span>

> [!NOTE]
> <span data-ttu-id="ba41f-149">L'eliminazione di una zona DNS comporta anche l'eliminazione di tutti i record DNS all'interno della zona.</span><span class="sxs-lookup"><span data-stu-id="ba41f-149">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="ba41f-150">Questa operazione non può essere annullata.</span><span class="sxs-lookup"><span data-stu-id="ba41f-150">This operation cannot be undone.</span></span> <span data-ttu-id="ba41f-151">Se la zona DNS è in uso, i servizi che la usano rileveranno un errore quando la zona viene eliminata.</span><span class="sxs-lookup"><span data-stu-id="ba41f-151">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="ba41f-152">Per evitare l'eliminazione accidentale di una zona, vedere [How to protect DNS zones and records](dns-protect-zones-recordsets.md) (Come proteggere le zone e i record DNS).</span><span class="sxs-lookup"><span data-stu-id="ba41f-152">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="ba41f-153">Questo comando richiede una conferma.</span><span class="sxs-lookup"><span data-stu-id="ba41f-153">This command prompts for confirmation.</span></span> <span data-ttu-id="ba41f-154">L'opzione facoltativa `--quiet` (forma breve `-q`) elimina questa richiesta.</span><span class="sxs-lookup"><span data-stu-id="ba41f-154">The optional `--quiet` switch (short form `-q`) suppresses this prompt.</span></span>

<span data-ttu-id="ba41f-155">L'esempio seguente mostra come eliminare la zona *contoso.com* dal gruppo di risorse *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="ba41f-155">The following example shows how to delete the zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="ba41f-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ba41f-156">Next steps</span></span>

<span data-ttu-id="ba41f-157">Informazioni su come [gestire record e set di record](dns-getstarted-create-recordset-cli-nodejs.md) nella zona DNS.</span><span class="sxs-lookup"><span data-stu-id="ba41f-157">Learn how to [manage record sets and records](dns-getstarted-create-recordset-cli-nodejs.md) in your DNS zone.</span></span>

<span data-ttu-id="ba41f-158">Informazioni su come [delegare il dominio al servizio DNS di Azure](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="ba41f-158">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

