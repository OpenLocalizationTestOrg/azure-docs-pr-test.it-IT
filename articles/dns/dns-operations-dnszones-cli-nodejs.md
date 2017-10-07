---
title: zone DNS di Azure - CLI di Azure 1.0 aaaManage DNS | Documenti Microsoft
description: "È possibile gestire le zone DNS usando l'interfaccia della riga di comando Azure 1.0. Questo articolo illustra come tooupdate, eliminare e creare le zone DNS in DNS di Azure."
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
ms.openlocfilehash: cb9790cc46626ef7f38a43edb57511104fe6057e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-10"></a><span data-ttu-id="fb685-104">Come toomanage zone DNS di Azure utilizzando hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="fb685-104">How toomanage DNS Zones in Azure DNS using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fb685-105">Portale</span><span class="sxs-lookup"><span data-stu-id="fb685-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="fb685-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb685-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="fb685-107">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="fb685-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="fb685-108">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="fb685-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="fb685-109">Questa guida viene spiegato come toomanage zone DNS utilizzando hello multipiattaforma CLI di Azure 1.0, disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="fb685-109">This guide shows how toomanage your DNS zones by using hello cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="fb685-110">È inoltre possibile gestire le zone DNS utilizzando [Azure PowerShell](dns-operations-dnszones.md) o hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fb685-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or hello Azure portal.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="fb685-111">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="fb685-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="fb685-112">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="fb685-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="fb685-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -nostri CLI per hello classic e risorse Gestione modelli di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fb685-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="fb685-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello.</span><span class="sxs-lookup"><span data-stu-id="fb685-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="fb685-115">Introduzione</span><span class="sxs-lookup"><span data-stu-id="fb685-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a><span data-ttu-id="fb685-116">Risorse della Guida</span><span class="sxs-lookup"><span data-stu-id="fb685-116">Getting help</span></span>

<span data-ttu-id="fb685-117">Avviano tutti i comandi CLI 1.0 relative tooAzure DNS con `azure network dns`.</span><span class="sxs-lookup"><span data-stu-id="fb685-117">All CLI 1.0 commands relating tooAzure DNS start with `azure network dns`.</span></span> <span data-ttu-id="fb685-118">La Guida è disponibile per ogni comando utilizzando hello `--help` opzione (forma breve `-h`).</span><span class="sxs-lookup"><span data-stu-id="fb685-118">Help is available for each command using hello `--help` option (short form `-h`).</span></span>  <span data-ttu-id="fb685-119">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fb685-119">For example:</span></span>

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="fb685-120">Creare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="fb685-120">Create a DNS zone</span></span>

<span data-ttu-id="fb685-121">Una zona DNS viene creata utilizzando hello `azure network dns zone create` comando.</span><span class="sxs-lookup"><span data-stu-id="fb685-121">A DNS zone is created using hello `azure network dns zone create` command.</span></span> <span data-ttu-id="fb685-122">Per altre informazioni, vedere `azure network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="fb685-122">For help, see `azure network dns zone create -h`.</span></span>

<span data-ttu-id="fb685-123">esempio Hello crea una zona DNS denominata *contoso.com* nel gruppo di risorse hello chiamato *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="fb685-123">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a><span data-ttu-id="fb685-124">toocreate una zona DNS con i tag</span><span class="sxs-lookup"><span data-stu-id="fb685-124">toocreate a DNS zone with tags</span></span>

<span data-ttu-id="fb685-125">Hello esempio seguente viene illustrato come della zona DNS toocreate con due [tag Azure Resource Manager](dns-zones-records.md#tags), *progetto = demo* e *env = test*, utilizzando hello `--tags` parametro (forma breve `-t`):</span><span class="sxs-lookup"><span data-stu-id="fb685-125">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using hello `--tags` parameter (short form `-t`):</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="fb685-126">Ottenere una zona DNS</span><span class="sxs-lookup"><span data-stu-id="fb685-126">Get a DNS zone</span></span>

<span data-ttu-id="fb685-127">tooretrieve una zona DNS, utilizzare `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="fb685-127">tooretrieve a DNS zone, use `azure network dns zone show`.</span></span> <span data-ttu-id="fb685-128">Per altre informazioni, vedere `azure network dns zone show -h`.</span><span class="sxs-lookup"><span data-stu-id="fb685-128">For help, see `azure network dns zone show -h`.</span></span>

<span data-ttu-id="fb685-129">esempio Hello restituisce zona DNS hello *contoso.com* e i dati dal gruppo di risorse associati *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="fb685-129">hello following example returns hello DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

<span data-ttu-id="fb685-130">Hello di esempio seguente è riportata la risposta hello.</span><span class="sxs-lookup"><span data-stu-id="fb685-130">hello following example is hello response.</span></span>

```
info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
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

<span data-ttu-id="fb685-131">Si noti che i record DNS non vengono restituiti da `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="fb685-131">Note that DNS records are not returned by `azure network dns zone show`.</span></span> <span data-ttu-id="fb685-132">Utilizzare i record DNS toolist, `azure network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="fb685-132">toolist DNS records, use `azure network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="fb685-133">Elencare le zone DNS</span><span class="sxs-lookup"><span data-stu-id="fb685-133">List DNS zones</span></span>

<span data-ttu-id="fb685-134">Utilizzare le zone DNS tooenumerate, `azure network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="fb685-134">tooenumerate DNS zones, use `azure network dns zone list`.</span></span> <span data-ttu-id="fb685-135">Per altre informazioni, vedere `azure network dns zone list -h`.</span><span class="sxs-lookup"><span data-stu-id="fb685-135">For help, see `azure network dns zone list -h`.</span></span>

<span data-ttu-id="fb685-136">Gruppo di risorse specificando hello sono elencate solo le zone nel gruppo di risorse hello:</span><span class="sxs-lookup"><span data-stu-id="fb685-136">Specifying hello resource group lists only those zones within hello resource group:</span></span>

```azurecli
azure network dns zone list MyResourceGroup
```

<span data-ttu-id="fb685-137">L'omissione di gruppo di risorse hello Elenca tutte le zone nella sottoscrizione hello:</span><span class="sxs-lookup"><span data-stu-id="fb685-137">Omitting hello resource group lists all zones in hello subscription:</span></span>

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="fb685-138">Aggiornare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="fb685-138">Update a DNS zone</span></span>

<span data-ttu-id="fb685-139">Le modifiche tooa possibile creare la risorsa di zona DNS mediante `azure network dns zone set`.</span><span class="sxs-lookup"><span data-stu-id="fb685-139">Changes tooa DNS zone resource can be made using `azure network dns zone set`.</span></span> <span data-ttu-id="fb685-140">Per altre informazioni, vedere `azure network dns zone set -h`.</span><span class="sxs-lookup"><span data-stu-id="fb685-140">For help, see `azure network dns zone set -h`.</span></span>

<span data-ttu-id="fb685-141">Questo comando consente di aggiornare set di record DNS hello zona hello (vedere [come i record DNS tooManage](dns-operations-recordsets-cli-nodejs.md)).</span><span class="sxs-lookup"><span data-stu-id="fb685-141">This command does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets-cli-nodejs.md)).</span></span> <span data-ttu-id="fb685-142">È tooupdate utilizzati solo le proprietà della risorsa di zona hello stesso.</span><span class="sxs-lookup"><span data-stu-id="fb685-142">It is only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="fb685-143">Queste proprietà sono attualmente limitata toohello [Azure Resource Manager 'tag'](dns-zones-records.md#tags) per la risorsa di zona hello.</span><span class="sxs-lookup"><span data-stu-id="fb685-143">These properties are currently limited toohello [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for hello zone resource.</span></span>

<span data-ttu-id="fb685-144">Hello esempio seguente viene illustrato come tooupdate hello tag in una zona DNS.</span><span class="sxs-lookup"><span data-stu-id="fb685-144">hello following example shows how tooupdate hello tags on a DNS zone.</span></span> <span data-ttu-id="fb685-145">i tag Hello esistenti vengono sostituiti da hello valore specificato.</span><span class="sxs-lookup"><span data-stu-id="fb685-145">hello existing tags are replaced by hello value specified.</span></span>

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="fb685-146">Eliminare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="fb685-146">Delete a DNS Zone</span></span>

<span data-ttu-id="fb685-147">Le zone DNS possono essere eliminate usando `azure network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="fb685-147">DNS zones can be deleted using `azure network dns zone delete`.</span></span> <span data-ttu-id="fb685-148">Per altre informazioni, vedere `azure network dns zone delete -h`.</span><span class="sxs-lookup"><span data-stu-id="fb685-148">For help, see `azure network dns zone delete -h`.</span></span>

> [!NOTE]
> <span data-ttu-id="fb685-149">L'eliminazione di una zona DNS elimina inoltre tutti i record DNS nella zona hello.</span><span class="sxs-lookup"><span data-stu-id="fb685-149">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="fb685-150">Questa operazione non può essere annullata.</span><span class="sxs-lookup"><span data-stu-id="fb685-150">This operation cannot be undone.</span></span> <span data-ttu-id="fb685-151">Se zona DNS hello è in uso, con zone hello services avrà esito negativo quando viene eliminata hello.</span><span class="sxs-lookup"><span data-stu-id="fb685-151">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="fb685-152">tooprotect l'eliminazione accidentale di zona, vedere [come tooprotect DNS zone e record](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="fb685-152">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="fb685-153">Questo comando richiede una conferma.</span><span class="sxs-lookup"><span data-stu-id="fb685-153">This command prompts for confirmation.</span></span> <span data-ttu-id="fb685-154">Hello facoltativo `--quiet` passare (forma breve `-q`) Elimina questa richiesta.</span><span class="sxs-lookup"><span data-stu-id="fb685-154">hello optional `--quiet` switch (short form `-q`) suppresses this prompt.</span></span>

<span data-ttu-id="fb685-155">Hello esempio seguente viene illustrato come toodelete hello zona *contoso.com* dal gruppo di risorse *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="fb685-155">hello following example shows how toodelete hello zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="fb685-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fb685-156">Next steps</span></span>

<span data-ttu-id="fb685-157">Informazioni su come troppo[gestire set di record e i record](dns-getstarted-create-recordset-cli-nodejs.md) nella zona DNS.</span><span class="sxs-lookup"><span data-stu-id="fb685-157">Learn how too[manage record sets and records](dns-getstarted-create-recordset-cli-nodejs.md) in your DNS zone.</span></span>

<span data-ttu-id="fb685-158">Informazioni su come troppo[delegare il tooAzure di dominio DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="fb685-158">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

