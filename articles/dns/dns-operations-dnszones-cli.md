---
title: zone DNS di Azure - CLI di Azure 2.0 aaaManage DNS | Documenti Microsoft
description: "È possibile gestire le zone DNS usando l'interfaccia della riga di comando Azure 2.0. Questo articolo illustra come tooupdate, eliminare e creare le zone DNS in DNS di Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: 3945a558b2db3490e50678d8395a47e55a85c8fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-20"></a><span data-ttu-id="bafaa-104">Come toomanage zone DNS di Azure utilizzando hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="bafaa-104">How toomanage DNS Zones in Azure DNS using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bafaa-105">Portale</span><span class="sxs-lookup"><span data-stu-id="bafaa-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="bafaa-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bafaa-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="bafaa-107">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="bafaa-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="bafaa-108">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="bafaa-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)


<span data-ttu-id="bafaa-109">Questa guida viene spiegato come toomanage zone DNS utilizzando hello multipiattaforma CLI di Azure, che è disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="bafaa-109">This guide shows how toomanage your DNS zones by using hello cross-platform Azure CLI, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="bafaa-110">È inoltre possibile gestire le zone DNS utilizzando [Azure PowerShell](dns-operations-dnszones.md) o hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bafaa-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or hello Azure portal.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="bafaa-111">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="bafaa-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="bafaa-112">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="bafaa-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="bafaa-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -nostri CLI per hello classic e risorse Gestione modelli di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="bafaa-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="bafaa-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello.</span><span class="sxs-lookup"><span data-stu-id="bafaa-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="bafaa-115">Introduzione</span><span class="sxs-lookup"><span data-stu-id="bafaa-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a><span data-ttu-id="bafaa-116">Configurare l'interfaccia della riga di comando di Azure 2.0 per DNS di Azure</span><span class="sxs-lookup"><span data-stu-id="bafaa-116">Set up Azure CLI 2.0 for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="bafaa-117">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="bafaa-117">Before you begin</span></span>

<span data-ttu-id="bafaa-118">Verificare di aver hello seguenti prima di iniziare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="bafaa-118">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="bafaa-119">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="bafaa-119">An Azure subscription.</span></span> <span data-ttu-id="bafaa-120">Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bafaa-120">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="bafaa-121">Installare hello l'ultima versione di hello Azure CLI 2.0, disponibile per Windows, Linux o Mac.</span><span class="sxs-lookup"><span data-stu-id="bafaa-121">Install hello latest version of hello Azure CLI 2.0, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="bafaa-122">Altre informazioni sono disponibile all'indirizzo [installazione hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="bafaa-122">More information is available at [Install hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="bafaa-123">Accedi tooyour account Azure</span><span class="sxs-lookup"><span data-stu-id="bafaa-123">Sign in tooyour Azure account</span></span>

<span data-ttu-id="bafaa-124">Aprire una finestra della console ed eseguire l'autenticazione con le credenziali.</span><span class="sxs-lookup"><span data-stu-id="bafaa-124">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="bafaa-125">Per ulteriori informazioni, vedere il Log in tooAzure da hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="bafaa-125">For more information, see Log in tooAzure from hello Azure CLI</span></span>

```
az login
```

### <a name="select-hello-subscription"></a><span data-ttu-id="bafaa-126">Selezionare la sottoscrizione hello</span><span class="sxs-lookup"><span data-stu-id="bafaa-126">Select hello subscription</span></span>

<span data-ttu-id="bafaa-127">Controllare le sottoscrizioni di hello per account hello.</span><span class="sxs-lookup"><span data-stu-id="bafaa-127">Check hello subscriptions for hello account.</span></span>

```
az account list
```

<span data-ttu-id="bafaa-128">Scegliere quali di toouse le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="bafaa-128">Choose which of your Azure subscriptions toouse.</span></span>

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="bafaa-129">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="bafaa-129">Create a resource group</span></span>

<span data-ttu-id="bafaa-130">Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso</span><span class="sxs-lookup"><span data-stu-id="bafaa-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="bafaa-131">Viene utilizzato come percorso predefinito di hello per le risorse in tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="bafaa-131">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="bafaa-132">Tuttavia, poiché tutte le risorse DNS sono globali, non è regionale, scelta hello del percorso del gruppo di risorse ha alcun impatto su DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="bafaa-132">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="bafaa-133">Se si usa un gruppo di risorse esistente, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="bafaa-133">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a><span data-ttu-id="bafaa-134">Risorse della Guida</span><span class="sxs-lookup"><span data-stu-id="bafaa-134">Getting help</span></span>

<span data-ttu-id="bafaa-135">Avviano tutti i comandi CLI 2.0 relative tooAzure DNS con `az network dns`.</span><span class="sxs-lookup"><span data-stu-id="bafaa-135">All CLI 2.0 commands relating tooAzure DNS start with `az network dns`.</span></span> <span data-ttu-id="bafaa-136">La Guida è disponibile per ogni comando utilizzando hello `--help` opzione (forma breve `-h`).</span><span class="sxs-lookup"><span data-stu-id="bafaa-136">Help is available for each command using hello `--help` option (short form `-h`).</span></span>  <span data-ttu-id="bafaa-137">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="bafaa-137">For example:</span></span>

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="bafaa-138">Creare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="bafaa-138">Create a DNS zone</span></span>

<span data-ttu-id="bafaa-139">Una zona DNS viene creata utilizzando hello `az network dns zone create` comando.</span><span class="sxs-lookup"><span data-stu-id="bafaa-139">A DNS zone is created using hello `az network dns zone create` command.</span></span> <span data-ttu-id="bafaa-140">Per altre informazioni, vedere `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="bafaa-140">For help, see `az network dns zone create -h`.</span></span>

<span data-ttu-id="bafaa-141">esempio Hello crea una zona DNS denominata *contoso.com* nel gruppo di risorse hello chiamato *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="bafaa-141">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a><span data-ttu-id="bafaa-142">toocreate una zona DNS con i tag</span><span class="sxs-lookup"><span data-stu-id="bafaa-142">toocreate a DNS zone with tags</span></span>

<span data-ttu-id="bafaa-143">Hello esempio seguente viene illustrato come della zona DNS toocreate con due [tag Azure Resource Manager](dns-zones-records.md#tags), *progetto = demo* e *env = test*, utilizzando hello `--tags` parametro (forma breve `-t`):</span><span class="sxs-lookup"><span data-stu-id="bafaa-143">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using hello `--tags` parameter (short form `-t`):</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="bafaa-144">Ottenere una zona DNS</span><span class="sxs-lookup"><span data-stu-id="bafaa-144">Get a DNS zone</span></span>

<span data-ttu-id="bafaa-145">tooretrieve una zona DNS, utilizzare `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="bafaa-145">tooretrieve a DNS zone, use `az network dns zone show`.</span></span> <span data-ttu-id="bafaa-146">Per altre informazioni, vedere `az network dns zone show --help`.</span><span class="sxs-lookup"><span data-stu-id="bafaa-146">For help, see `az network dns zone show --help`.</span></span>

<span data-ttu-id="bafaa-147">esempio Hello restituisce zona DNS hello *contoso.com* e i dati dal gruppo di risorse associati *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="bafaa-147">hello following example returns hello DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

<span data-ttu-id="bafaa-148">Hello di esempio seguente è riportata la risposta hello.</span><span class="sxs-lookup"><span data-stu-id="bafaa-148">hello following example is hello response.</span></span>

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="bafaa-149">Si noti che i record DNS non vengono restituiti da `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="bafaa-149">Note that DNS records are not returned by `az network dns zone show`.</span></span> <span data-ttu-id="bafaa-150">Utilizzare i record DNS toolist, `az network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="bafaa-150">toolist DNS records, use `az network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="bafaa-151">Elencare le zone DNS</span><span class="sxs-lookup"><span data-stu-id="bafaa-151">List DNS zones</span></span>

<span data-ttu-id="bafaa-152">Utilizzare le zone DNS tooenumerate, `az network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="bafaa-152">tooenumerate DNS zones, use `az network dns zone list`.</span></span> <span data-ttu-id="bafaa-153">Per altre informazioni, vedere `az network dns zone list --help`.</span><span class="sxs-lookup"><span data-stu-id="bafaa-153">For help, see `az network dns zone list --help`.</span></span>

<span data-ttu-id="bafaa-154">Gruppo di risorse specificando hello sono elencate solo le zone nel gruppo di risorse hello:</span><span class="sxs-lookup"><span data-stu-id="bafaa-154">Specifying hello resource group lists only those zones within hello resource group:</span></span>

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

<span data-ttu-id="bafaa-155">L'omissione di gruppo di risorse hello Elenca tutte le zone nella sottoscrizione hello:</span><span class="sxs-lookup"><span data-stu-id="bafaa-155">Omitting hello resource group lists all zones in hello subscription:</span></span>

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="bafaa-156">Aggiornare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="bafaa-156">Update a DNS zone</span></span>

<span data-ttu-id="bafaa-157">Le modifiche tooa possibile creare la risorsa di zona DNS mediante `az network dns zone update`.</span><span class="sxs-lookup"><span data-stu-id="bafaa-157">Changes tooa DNS zone resource can be made using `az network dns zone update`.</span></span> <span data-ttu-id="bafaa-158">Per altre informazioni, vedere `az network dns zone update --help`.</span><span class="sxs-lookup"><span data-stu-id="bafaa-158">For help, see `az network dns zone update --help`.</span></span>

<span data-ttu-id="bafaa-159">Questo comando consente di aggiornare set di record DNS hello zona hello (vedere [come i record DNS tooManage](dns-operations-recordsets-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="bafaa-159">This command does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets-cli.md)).</span></span> <span data-ttu-id="bafaa-160">È tooupdate utilizzati solo le proprietà della risorsa di zona hello stesso.</span><span class="sxs-lookup"><span data-stu-id="bafaa-160">It is only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="bafaa-161">Queste proprietà sono attualmente limitata toohello [Azure Resource Manager 'tag'](dns-zones-records.md#tags) per la risorsa di zona hello.</span><span class="sxs-lookup"><span data-stu-id="bafaa-161">These properties are currently limited toohello [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for hello zone resource.</span></span>

<span data-ttu-id="bafaa-162">Hello esempio seguente viene illustrato come tooupdate hello tag in una zona DNS.</span><span class="sxs-lookup"><span data-stu-id="bafaa-162">hello following example shows how tooupdate hello tags on a DNS zone.</span></span> <span data-ttu-id="bafaa-163">i tag Hello esistenti vengono sostituiti da hello valore specificato.</span><span class="sxs-lookup"><span data-stu-id="bafaa-163">hello existing tags are replaced by hello value specified.</span></span>

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="bafaa-164">Eliminare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="bafaa-164">Delete a DNS zone</span></span>

<span data-ttu-id="bafaa-165">Le zone DNS possono essere eliminate usando `az network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="bafaa-165">DNS zones can be deleted using `az network dns zone delete`.</span></span> <span data-ttu-id="bafaa-166">Per altre informazioni, vedere `az network dns zone delete --help`.</span><span class="sxs-lookup"><span data-stu-id="bafaa-166">For help, see `az network dns zone delete --help`.</span></span>

> [!NOTE]
> <span data-ttu-id="bafaa-167">L'eliminazione di una zona DNS elimina inoltre tutti i record DNS nella zona hello.</span><span class="sxs-lookup"><span data-stu-id="bafaa-167">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="bafaa-168">Questa operazione non può essere annullata.</span><span class="sxs-lookup"><span data-stu-id="bafaa-168">This operation cannot be undone.</span></span> <span data-ttu-id="bafaa-169">Se zona DNS hello è in uso, con zone hello services avrà esito negativo quando viene eliminata hello.</span><span class="sxs-lookup"><span data-stu-id="bafaa-169">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="bafaa-170">tooprotect l'eliminazione accidentale di zona, vedere [come tooprotect DNS zone e record](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="bafaa-170">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="bafaa-171">Questo comando richiede una conferma.</span><span class="sxs-lookup"><span data-stu-id="bafaa-171">This command prompts for confirmation.</span></span> <span data-ttu-id="bafaa-172">Hello facoltativo `--yes` commutatore Elimina questa richiesta.</span><span class="sxs-lookup"><span data-stu-id="bafaa-172">hello optional `--yes` switch suppresses this prompt.</span></span>

<span data-ttu-id="bafaa-173">Hello esempio seguente viene illustrato come toodelete hello zona *contoso.com* dal gruppo di risorse *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="bafaa-173">hello following example shows how toodelete hello zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="bafaa-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bafaa-174">Next steps</span></span>

<span data-ttu-id="bafaa-175">Informazioni su come troppo[gestire set di record e i record](dns-getstarted-create-recordset-cli.md) nella zona DNS.</span><span class="sxs-lookup"><span data-stu-id="bafaa-175">Learn how too[manage record sets and records](dns-getstarted-create-recordset-cli.md) in your DNS zone.</span></span>

<span data-ttu-id="bafaa-176">Informazioni su come troppo[delegare il tooAzure di dominio DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="bafaa-176">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

