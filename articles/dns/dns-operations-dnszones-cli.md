---
title: Gestire le zone DNS in DNS di Azure - Interfaccia della riga di comando di Azure 2.0 | Documentazione Microsoft
description: "È possibile gestire le zone DNS usando l'interfaccia della riga di comando Azure 2.0. Questo articolo illustra come aggiornare, eliminare e creare le zone DNS in DNS di Azure."
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
ms.openlocfilehash: 1414baf9e51d648cc3a46c4f8635040b4d276910
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-azure-dns-using-the-azure-cli-20"></a><span data-ttu-id="454bd-104">Come gestire le zone DNS in DNS di Azure DNS usando l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="454bd-104">How to manage DNS Zones in Azure DNS using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="454bd-105">Portale</span><span class="sxs-lookup"><span data-stu-id="454bd-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="454bd-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="454bd-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="454bd-107">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="454bd-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="454bd-108">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="454bd-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)


<span data-ttu-id="454bd-109">Questa guida illustra come gestire le zone DNS usando l'interfaccia della riga di comando di Azure multipiattaforma, disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="454bd-109">This guide shows how to manage your DNS zones by using the cross-platform Azure CLI, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="454bd-110">È anche possibile gestire le zone DNS usando [Azure PowerShell](dns-operations-dnszones.md) o il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="454bd-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or the Azure portal.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="454bd-111">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="454bd-111">CLI versions to complete the task</span></span>

<span data-ttu-id="454bd-112">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="454bd-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="454bd-113">[Interfaccia della riga di comando di Azure 1.0](dns-operations-dnszones-cli-nodejs.md): l'interfaccia della riga di comando per il modello di distribuzione classico e di gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="454bd-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="454bd-114">[Interfaccia della riga di comando di Azure 2.0](dns-operations-dnszones-cli.md): interfaccia avanzata per il modello di distribuzione di gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="454bd-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="454bd-115">Introduzione</span><span class="sxs-lookup"><span data-stu-id="454bd-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a><span data-ttu-id="454bd-116">Configurare l'interfaccia della riga di comando di Azure 2.0 per DNS di Azure</span><span class="sxs-lookup"><span data-stu-id="454bd-116">Set up Azure CLI 2.0 for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="454bd-117">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="454bd-117">Before you begin</span></span>

<span data-ttu-id="454bd-118">Prima di iniziare la configurazione, verificare di essere in possesso degli elementi seguenti.</span><span class="sxs-lookup"><span data-stu-id="454bd-118">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="454bd-119">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="454bd-119">An Azure subscription.</span></span> <span data-ttu-id="454bd-120">Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="454bd-120">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="454bd-121">Installare la versione più recente dell'interfaccia della riga di comando di Azure 2.0, disponibile per Windows, Linux o Mac.</span><span class="sxs-lookup"><span data-stu-id="454bd-121">Install the latest version of the Azure CLI 2.0, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="454bd-122">Per altre informazioni, vedere [Installare l'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="454bd-122">More information is available at [Install the Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

### <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="454bd-123">Accedere con l'account Azure</span><span class="sxs-lookup"><span data-stu-id="454bd-123">Sign in to your Azure account</span></span>

<span data-ttu-id="454bd-124">Aprire una finestra della console ed eseguire l'autenticazione con le credenziali.</span><span class="sxs-lookup"><span data-stu-id="454bd-124">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="454bd-125">Per altre informazioni, vedere Accedere ad Azure dall'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="454bd-125">For more information, see Log in to Azure from the Azure CLI</span></span>

```
az login
```

### <a name="select-the-subscription"></a><span data-ttu-id="454bd-126">Selezionare la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="454bd-126">Select the subscription</span></span>

<span data-ttu-id="454bd-127">Controllare le sottoscrizioni per l'account.</span><span class="sxs-lookup"><span data-stu-id="454bd-127">Check the subscriptions for the account.</span></span>

```
az account list
```

<span data-ttu-id="454bd-128">Scegliere le sottoscrizioni ad Azure da usare.</span><span class="sxs-lookup"><span data-stu-id="454bd-128">Choose which of your Azure subscriptions to use.</span></span>

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="454bd-129">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="454bd-129">Create a resource group</span></span>

<span data-ttu-id="454bd-130">Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso</span><span class="sxs-lookup"><span data-stu-id="454bd-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="454bd-131">che viene usato come percorso predefinito per le risorse presenti in tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="454bd-131">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="454bd-132">Tuttavia, dato che tutte le risorse DNS sono globali, non regionali, la scelta del percorso del gruppo di risorse non ha alcun impatto sul servizio DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="454bd-132">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="454bd-133">Se si usa un gruppo di risorse esistente, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="454bd-133">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a><span data-ttu-id="454bd-134">Risorse della Guida</span><span class="sxs-lookup"><span data-stu-id="454bd-134">Getting help</span></span>

<span data-ttu-id="454bd-135">Tutti i comandi dell'interfaccia della riga di comando 2.0 relativi a DNS di Azure iniziano con `az network dns`.</span><span class="sxs-lookup"><span data-stu-id="454bd-135">All CLI 2.0 commands relating to Azure DNS start with `az network dns`.</span></span> <span data-ttu-id="454bd-136">Sono disponibili informazioni per ogni comando tramite l'opzione `--help` (forma breve `-h`).</span><span class="sxs-lookup"><span data-stu-id="454bd-136">Help is available for each command using the `--help` option (short form `-h`).</span></span>  <span data-ttu-id="454bd-137">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="454bd-137">For example:</span></span>

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="454bd-138">Creare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="454bd-138">Create a DNS zone</span></span>

<span data-ttu-id="454bd-139">Una zona DNS viene creata utilizzando il comando `az network dns zone create` .</span><span class="sxs-lookup"><span data-stu-id="454bd-139">A DNS zone is created using the `az network dns zone create` command.</span></span> <span data-ttu-id="454bd-140">Per altre informazioni, vedere `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="454bd-140">For help, see `az network dns zone create -h`.</span></span>

<span data-ttu-id="454bd-141">L'esempio seguente crea una zona DNS denominata *contoso.com* nel gruppo di risorse denominato *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="454bd-141">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="to-create-a-dns-zone-with-tags"></a><span data-ttu-id="454bd-142">Per creare una zona DNS con tag</span><span class="sxs-lookup"><span data-stu-id="454bd-142">To create a DNS zone with tags</span></span>

<span data-ttu-id="454bd-143">L'esempio seguente illustra come creare una zona DNS con due [tag di Azure Resource Manager](dns-zones-records.md#tags), *project = demo* ed *env = test*, usando il parametro `--tags` (forma breve `-t`):</span><span class="sxs-lookup"><span data-stu-id="454bd-143">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using the `--tags` parameter (short form `-t`):</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="454bd-144">Ottenere una zona DNS</span><span class="sxs-lookup"><span data-stu-id="454bd-144">Get a DNS zone</span></span>

<span data-ttu-id="454bd-145">Per recuperare una zona DNS, usare `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="454bd-145">To retrieve a DNS zone, use `az network dns zone show`.</span></span> <span data-ttu-id="454bd-146">Per altre informazioni, vedere `az network dns zone show --help`.</span><span class="sxs-lookup"><span data-stu-id="454bd-146">For help, see `az network dns zone show --help`.</span></span>

<span data-ttu-id="454bd-147">L'esempio seguente restituisce la zona DNS *contoso.com* e i relativi dati associati dal gruppo di risorse *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="454bd-147">The following example returns the DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

<span data-ttu-id="454bd-148">L'esempio seguente corrisponde alla risposta.</span><span class="sxs-lookup"><span data-stu-id="454bd-148">The following example is the response.</span></span>

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

<span data-ttu-id="454bd-149">Si noti che i record DNS non vengono restituiti da `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="454bd-149">Note that DNS records are not returned by `az network dns zone show`.</span></span> <span data-ttu-id="454bd-150">Per elencare i record DNS, usare `az network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="454bd-150">To list DNS records, use `az network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="454bd-151">Elencare le zone DNS</span><span class="sxs-lookup"><span data-stu-id="454bd-151">List DNS zones</span></span>

<span data-ttu-id="454bd-152">Per enumerare le zone DNS, usare `az network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="454bd-152">To enumerate DNS zones, use `az network dns zone list`.</span></span> <span data-ttu-id="454bd-153">Per altre informazioni, vedere `az network dns zone list --help`.</span><span class="sxs-lookup"><span data-stu-id="454bd-153">For help, see `az network dns zone list --help`.</span></span>

<span data-ttu-id="454bd-154">Se si specifica il gruppo di risorse, vengono elencate solo le zone all'interno del gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="454bd-154">Specifying the resource group lists only those zones within the resource group:</span></span>

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

<span data-ttu-id="454bd-155">Se invece il gruppo di risorse viene omesso, sono elencate tutte le zone nella sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="454bd-155">Omitting the resource group lists all zones in the subscription:</span></span>

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="454bd-156">Aggiornare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="454bd-156">Update a DNS zone</span></span>

<span data-ttu-id="454bd-157">È possibile apportare modifiche a una risorsa di zona DNS usando `az network dns zone update`.</span><span class="sxs-lookup"><span data-stu-id="454bd-157">Changes to a DNS zone resource can be made using `az network dns zone update`.</span></span> <span data-ttu-id="454bd-158">Per altre informazioni, vedere `az network dns zone update --help`.</span><span class="sxs-lookup"><span data-stu-id="454bd-158">For help, see `az network dns zone update --help`.</span></span>

<span data-ttu-id="454bd-159">Questo comando non consente di aggiornare alcun set di record DNS compreso nella zona (vedere [Come gestire i record DNS](dns-operations-recordsets-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="454bd-159">This command does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets-cli.md)).</span></span> <span data-ttu-id="454bd-160">Questa operazione permette solo di aggiornare le proprietà della risorsa di zona stessa.</span><span class="sxs-lookup"><span data-stu-id="454bd-160">It is only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="454bd-161">Queste proprietà sono attualmente limitate ai ["tag" di Azure Resource Manager](dns-zones-records.md#tags) relativi alla risorsa di zona.</span><span class="sxs-lookup"><span data-stu-id="454bd-161">These properties are currently limited to the [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for the zone resource.</span></span>

<span data-ttu-id="454bd-162">L'esempio seguente illustra come aggiornare i tag in una zona DNS.</span><span class="sxs-lookup"><span data-stu-id="454bd-162">The following example shows how to update the tags on a DNS zone.</span></span> <span data-ttu-id="454bd-163">I tag esistenti vengono sostituiti dal valore specificato.</span><span class="sxs-lookup"><span data-stu-id="454bd-163">The existing tags are replaced by the value specified.</span></span>

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="454bd-164">Eliminare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="454bd-164">Delete a DNS zone</span></span>

<span data-ttu-id="454bd-165">Le zone DNS possono essere eliminate usando `az network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="454bd-165">DNS zones can be deleted using `az network dns zone delete`.</span></span> <span data-ttu-id="454bd-166">Per altre informazioni, vedere `az network dns zone delete --help`.</span><span class="sxs-lookup"><span data-stu-id="454bd-166">For help, see `az network dns zone delete --help`.</span></span>

> [!NOTE]
> <span data-ttu-id="454bd-167">L'eliminazione di una zona DNS comporta anche l'eliminazione di tutti i record DNS all'interno della zona.</span><span class="sxs-lookup"><span data-stu-id="454bd-167">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="454bd-168">Questa operazione non può essere annullata.</span><span class="sxs-lookup"><span data-stu-id="454bd-168">This operation cannot be undone.</span></span> <span data-ttu-id="454bd-169">Se la zona DNS è in uso, i servizi che la usano rileveranno un errore quando la zona viene eliminata.</span><span class="sxs-lookup"><span data-stu-id="454bd-169">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="454bd-170">Per evitare l'eliminazione accidentale di una zona, vedere [How to protect DNS zones and records](dns-protect-zones-recordsets.md) (Come proteggere le zone e i record DNS).</span><span class="sxs-lookup"><span data-stu-id="454bd-170">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="454bd-171">Questo comando richiede una conferma.</span><span class="sxs-lookup"><span data-stu-id="454bd-171">This command prompts for confirmation.</span></span> <span data-ttu-id="454bd-172">Lo switch facoltativo `--yes` elimina questa richiesta.</span><span class="sxs-lookup"><span data-stu-id="454bd-172">The optional `--yes` switch suppresses this prompt.</span></span>

<span data-ttu-id="454bd-173">L'esempio seguente mostra come eliminare la zona *contoso.com* dal gruppo di risorse *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="454bd-173">The following example shows how to delete the zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="454bd-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="454bd-174">Next steps</span></span>

<span data-ttu-id="454bd-175">Informazioni su come [gestire record e set di record](dns-getstarted-create-recordset-cli.md) nella zona DNS.</span><span class="sxs-lookup"><span data-stu-id="454bd-175">Learn how to [manage record sets and records](dns-getstarted-create-recordset-cli.md) in your DNS zone.</span></span>

<span data-ttu-id="454bd-176">Informazioni su come [delegare il dominio al servizio DNS di Azure](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="454bd-176">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

