---
title: Gestire le zone DNS in DNS di Azure - PowerShell | Documentazione Microsoft
description: "È possibile gestire le zone DNS usando PowerShell di Azure. Questo articolo illustra come aggiornare, eliminare e creare le zone DNS in DNS di Azure"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: a67992ab-8166-4052-9b28-554c5a39e60c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 92f1da660d875c76d5d826669d6c1d12018c3d0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-using-powershell"></a><span data-ttu-id="2353a-104">Come gestire le zone DNS utilizzando PowerShell</span><span class="sxs-lookup"><span data-stu-id="2353a-104">How to manage DNS Zones using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2353a-105">Portale</span><span class="sxs-lookup"><span data-stu-id="2353a-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="2353a-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2353a-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="2353a-107">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="2353a-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="2353a-108">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="2353a-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="2353a-109">Questo articolo spiega come gestire una zona DNS mediante Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2353a-109">This article shows you how to manage your DNS zones by using Azure PowerShell.</span></span> <span data-ttu-id="2353a-110">È anche possibile gestire le zone DNS usando l'[interfaccia della riga di comando di Azure](dns-operations-dnszones-cli.md) multipiattaforma o il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2353a-110">You can also manage your DNS zones using the cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or the Azure portal.</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a><span data-ttu-id="2353a-111">Creare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="2353a-111">Create a DNS zone</span></span>

<span data-ttu-id="2353a-112">Viene creata una zona DNS con il cmdlet `New-AzureRmDnsZone` .</span><span class="sxs-lookup"><span data-stu-id="2353a-112">A DNS zone is created by using the `New-AzureRmDnsZone` cmdlet.</span></span>

<span data-ttu-id="2353a-113">L'esempio seguente crea una zona DNS denominata *contoso.com* nel gruppo di risorse denominato *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="2353a-113">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="2353a-114">L'esempio seguente illustra come creare una zona DNS con due [tag di Azure Resource Manager](dns-zones-records.md#tags), *project = demo* e *env = test*:</span><span class="sxs-lookup"><span data-stu-id="2353a-114">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="2353a-115">Ottenere una zona DNS</span><span class="sxs-lookup"><span data-stu-id="2353a-115">Get a DNS zone</span></span>

<span data-ttu-id="2353a-116">Per recuperare una zona DNS, usare il cmdlet `Get-AzureRmDnsZone` .</span><span class="sxs-lookup"><span data-stu-id="2353a-116">To retrieve a DNS zone, use the `Get-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="2353a-117">Questa operazione restituisce un oggetto di zona DNS corrispondente a una zona esistente nel servizio DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="2353a-117">This operation returns a DNS zone object corresponding to an existing zone in Azure DNS.</span></span> <span data-ttu-id="2353a-118">L'oggetto contiene i dati sulla zona (ad esempio il numero di set di record), ma non contiene i set di record stessi (vedere `Get-AzureRmDnsRecordSet`).</span><span class="sxs-lookup"><span data-stu-id="2353a-118">The object contains data about the zone (such as the number of record sets), but does not contain the record sets themselves (see `Get-AzureRmDnsRecordSet`).</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com –ResourceGroupName MyAzureResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-8ec2-f4879750d201
Tags                  : {project, env}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org.,
                        ns4-01.azure-dns.info.}
NumberOfRecordSets    : 2
MaxNumberOfRecordSets : 5000
```

## <a name="list-dns-zones"></a><span data-ttu-id="2353a-119">Elencare le zone DNS</span><span class="sxs-lookup"><span data-stu-id="2353a-119">List DNS zones</span></span>

<span data-ttu-id="2353a-120">Omettendo il nome della zona da `Get-AzureRmDnsZone`, è possibile enumerare tutte le zone in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="2353a-120">By omitting the zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group.</span></span> <span data-ttu-id="2353a-121">Questa operazione restituisce una matrice di oggetti di zona.</span><span class="sxs-lookup"><span data-stu-id="2353a-121">This operation returns an array of zone objects.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="2353a-122">Omettendo il nome della zona e il nome del gruppo di risorse da `Get-AzureRmDnsZone`, è possibile enumerare tutte le zone nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2353a-122">By omitting both the zone name and the resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in the Azure subscription.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="2353a-123">Aggiornare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="2353a-123">Update a DNS zone</span></span>

<span data-ttu-id="2353a-124">È possibile apportare modifiche a una risorsa di zona DNS usando `Set-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="2353a-124">Changes to a DNS zone resource can be made by using `Set-AzureRmDnsZone`.</span></span> <span data-ttu-id="2353a-125">Il cmdlet non consente di aggiornare alcuni dei set di record DNS compresi nella zona (vedere [Come gestire i record DNS](dns-operations-recordsets.md)).</span><span class="sxs-lookup"><span data-stu-id="2353a-125">This cmdlet does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets.md)).</span></span> <span data-ttu-id="2353a-126">Questa operazione permette solo di aggiornare le proprietà della risorsa di zona stessa.</span><span class="sxs-lookup"><span data-stu-id="2353a-126">It's only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="2353a-127">Le proprietà della zona scrivibile sono attualmente limitate ai ["tag" di Azure Resource Manager relativi alla risorsa di zona](dns-zones-records.md#tags).</span><span class="sxs-lookup"><span data-stu-id="2353a-127">The writable zone properties are currently limited to the [Azure Resource Manager ‘tags’ for the zone resource](dns-zones-records.md#tags).</span></span>

<span data-ttu-id="2353a-128">Usare una delle due opzioni seguenti per aggiornare una zona DNS:</span><span class="sxs-lookup"><span data-stu-id="2353a-128">Use one of the following two ways to update a DNS zone:</span></span>

### <a name="specify-the-zone-using-the-zone-name-and-resource-group"></a><span data-ttu-id="2353a-129">Specificare la zona usando il nome della zona e del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="2353a-129">Specify the zone using the zone name and resource group</span></span>

<span data-ttu-id="2353a-130">Questo approccio sostituisce i tag di zona esistenti con i valori specificati.</span><span class="sxs-lookup"><span data-stu-id="2353a-130">This approach replaces the existing zone tags with the values specified.</span></span>

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-the-zone-using-a-zone-object"></a><span data-ttu-id="2353a-131">Specificare la zona usando un oggetto $zone</span><span class="sxs-lookup"><span data-stu-id="2353a-131">Specify the zone using a $zone object</span></span>

<span data-ttu-id="2353a-132">Questo approccio recupera l'oggetto zona esistente, modifica i tag e quindi esegue il commit delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="2353a-132">This approach retrieves the existing zone object, modifies the tags, and then commits the changes.</span></span> <span data-ttu-id="2353a-133">Ciò consente di conservare i tag esistenti.</span><span class="sxs-lookup"><span data-stu-id="2353a-133">In this way, existing tags can be preserved.</span></span>

```powershell
# Get the zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="2353a-134">Quando si usa `Set-AzureRmDnsZone` con un oggetto $zone, i [controlli ETag](dns-zones-records.md#etags) vengono usati per verificare che le modifiche simultanee non vengano sovrascritte.</span><span class="sxs-lookup"><span data-stu-id="2353a-134">When using `Set-AzureRmDnsZone` with a $zone object, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="2353a-135">È possibile usare l'opzione facoltativa `-Overwrite` per disattivare tali controlli.</span><span class="sxs-lookup"><span data-stu-id="2353a-135">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

## <a name="delete-a-dns-zone"></a><span data-ttu-id="2353a-136">Eliminare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="2353a-136">Delete a DNS Zone</span></span>

<span data-ttu-id="2353a-137">Le zone DNS possono essere eliminate usando il cmdlet `Remove-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="2353a-137">DNS zones can be deleted using the `Remove-AzureRmDnsZone` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="2353a-138">L'eliminazione di una zona DNS comporta anche l'eliminazione di tutti i record DNS all'interno della zona.</span><span class="sxs-lookup"><span data-stu-id="2353a-138">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="2353a-139">Questa operazione non può essere annullata.</span><span class="sxs-lookup"><span data-stu-id="2353a-139">This operation cannot be undone.</span></span> <span data-ttu-id="2353a-140">Se la zona DNS è in uso, i servizi che la usano rileveranno un errore quando la zona viene eliminata.</span><span class="sxs-lookup"><span data-stu-id="2353a-140">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="2353a-141">Per evitare l'eliminazione accidentale di una zona, vedere [How to protect DNS zones and records](dns-protect-zones-recordsets.md) (Come proteggere le zone e i record DNS).</span><span class="sxs-lookup"><span data-stu-id="2353a-141">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>


<span data-ttu-id="2353a-142">Usare una delle due opzioni seguenti per eliminare la zona DNS:</span><span class="sxs-lookup"><span data-stu-id="2353a-142">Use one of the following two ways to delete a DNS zone:</span></span>

### <a name="specify-the-zone-using-the-zone-name-and-resource-group-name"></a><span data-ttu-id="2353a-143">Specificare la zona usando il nome della zona e del gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="2353a-143">Specify the zone using the zone name and resource group name</span></span>

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-the-zone-using-a-zone-object"></a><span data-ttu-id="2353a-144">Specificare la zona usando un oggetto $zone</span><span class="sxs-lookup"><span data-stu-id="2353a-144">Specify the zone using a $zone object</span></span>

<span data-ttu-id="2353a-145">È possibile specificare la zona da eliminare usando un oggetto `$zone` restituito da `Get-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="2353a-145">You can specify the zone to be deleted using a `$zone` object returned by `Get-AzureRmDnsZone`.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="2353a-146">L'oggetto di zona può essere anche reindirizzato invece che passato come parametro:</span><span class="sxs-lookup"><span data-stu-id="2353a-146">The zone object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

<span data-ttu-id="2353a-147">Come con `Set-AzureRmDnsZone`, specificare la zona usando un oggetto `$zone` consente di abilitare i controlli ETag per garantire che le modifiche simultanee non vengano eliminate.</span><span class="sxs-lookup"><span data-stu-id="2353a-147">As with `Set-AzureRmDnsZone`, specifying the zone using a `$zone` object enables Etag checks to ensure concurrent changes are not deleted.</span></span> <span data-ttu-id="2353a-148">Usare l'opzione `-Overwrite` per disattivare tali controlli.</span><span class="sxs-lookup"><span data-stu-id="2353a-148">Use the `-Overwrite` switch to suppress these checks.</span></span>

## <a name="confirmation-prompts"></a><span data-ttu-id="2353a-149">Richieste di conferma</span><span class="sxs-lookup"><span data-stu-id="2353a-149">Confirmation prompts</span></span>

<span data-ttu-id="2353a-150">I cmdlet `New-AzureRmDnsZone`, `Set-AzureRmDnsZone` e `Remove-AzureRmDnsZone` supportano le richieste di conferma.</span><span class="sxs-lookup"><span data-stu-id="2353a-150">The `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, and `Remove-AzureRmDnsZone` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="2353a-151">`New-AzureRmDnsZone` e `Set-AzureRmDnsZone` richiedono la conferma se la variabile di preferenza `$ConfirmPreference` di PowerShell ha un valore uguale o inferiore a `Medium`.</span><span class="sxs-lookup"><span data-stu-id="2353a-151">Both `New-AzureRmDnsZone` and `Set-AzureRmDnsZone` prompt for confirmation if the `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="2353a-152">A causa dell'impatto potenzialmente significativo dell'eliminazione di una zona DNS, il cmdlet `Remove-AzureRmDnsZone` richiede la conferma se la variabile `$ConfirmPreference` di PowerShell ha un valore diverso da `None`.</span><span class="sxs-lookup"><span data-stu-id="2353a-152">Due to the potentially high impact of deleting a DNS zone, the `Remove-AzureRmDnsZone` cmdlet prompts for confirmation if the `$ConfirmPreference` PowerShell variable has any value other than `None`.</span></span>

<span data-ttu-id="2353a-153">Poiché il valore predefinito per `$ConfirmPreference` è `High`, solo `Remove-AzureRmDnsZone` richiede la conferma per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="2353a-153">Since the default value for `$ConfirmPreference` is `High`, only `Remove-AzureRmDnsZone` prompts for confirmation by default.</span></span>

<span data-ttu-id="2353a-154">Per eseguire l'override dell'impostazione `$ConfirmPreference` corrente è possibile usare il parametro `-Confirm`.</span><span class="sxs-lookup"><span data-stu-id="2353a-154">You can override the current `$ConfirmPreference` setting using the `-Confirm` parameter.</span></span> <span data-ttu-id="2353a-155">Se si specifica `-Confirm` o `-Confirm:$True`, il cmdlet chiede conferma prima dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2353a-155">If you specify `-Confirm` or `-Confirm:$True` , the cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="2353a-156">Se si specifica `-Confirm:$False`, il cmdlet non chiede alcuna conferma.</span><span class="sxs-lookup"><span data-stu-id="2353a-156">If you specify `-Confirm:$False` , the cmdlet does not prompt you for confirmation.</span></span>

<span data-ttu-id="2353a-157">Per altre informazioni su `-Confirm` e `$ConfirmPreference`, vedere [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables) (Informazioni sulle variabili di preferenza).</span><span class="sxs-lookup"><span data-stu-id="2353a-157">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2353a-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2353a-158">Next steps</span></span>

<span data-ttu-id="2353a-159">Informazioni su come [gestire record e set di record](dns-operations-recordsets.md) nella zona DNS.</span><span class="sxs-lookup"><span data-stu-id="2353a-159">Learn how to [manage record sets and records](dns-operations-recordsets.md) in your DNS zone.</span></span>
<br>
<span data-ttu-id="2353a-160">Informazioni su come [delegare il dominio al servizio DNS di Azure](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="2353a-160">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>
<br>
<span data-ttu-id="2353a-161">Vedere la [documentazione di riferimento di PowerShell nel servizio DNS di Azure](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="2353a-161">Review the [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>

