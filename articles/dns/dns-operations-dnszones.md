---
title: aaaManage DNS zone DNS di Azure - PowerShell | Documenti Microsoft
description: "È possibile gestire le zone DNS usando PowerShell di Azure. In questo articolo viene descritto come tooupdate, eliminare e creare le zone DNS in DNS di Azure"
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
ms.openlocfilehash: 261b89f72213aa9784034d47ff9d1c55a4e80d65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-using-powershell"></a><span data-ttu-id="18f6b-104">Come le zone DNS toomanage tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="18f6b-104">How toomanage DNS Zones using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="18f6b-105">Portale</span><span class="sxs-lookup"><span data-stu-id="18f6b-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="18f6b-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="18f6b-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="18f6b-107">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="18f6b-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="18f6b-108">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="18f6b-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="18f6b-109">Questo articolo illustra come toomanage zone DNS tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="18f6b-109">This article shows you how toomanage your DNS zones by using Azure PowerShell.</span></span> <span data-ttu-id="18f6b-110">È inoltre possibile gestire le zone DNS utilizzando hello multipiattaforma [CLI di Azure](dns-operations-dnszones-cli.md) o hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="18f6b-110">You can also manage your DNS zones using hello cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or hello Azure portal.</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a><span data-ttu-id="18f6b-111">Creare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="18f6b-111">Create a DNS zone</span></span>

<span data-ttu-id="18f6b-112">Una zona DNS viene creata utilizzando hello `New-AzureRmDnsZone` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="18f6b-112">A DNS zone is created by using hello `New-AzureRmDnsZone` cmdlet.</span></span>

<span data-ttu-id="18f6b-113">esempio Hello crea una zona DNS denominata *contoso.com* nel gruppo di risorse hello chiamato *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="18f6b-113">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="18f6b-114">Hello esempio seguente viene illustrato come della zona DNS toocreate con due [tag Azure Resource Manager](dns-zones-records.md#tags), *progetto = demo* e *env = test*:</span><span class="sxs-lookup"><span data-stu-id="18f6b-114">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="18f6b-115">Ottenere una zona DNS</span><span class="sxs-lookup"><span data-stu-id="18f6b-115">Get a DNS zone</span></span>

<span data-ttu-id="18f6b-116">tooretrieve una zona DNS, utilizzare hello `Get-AzureRmDnsZone` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="18f6b-116">tooretrieve a DNS zone, use hello `Get-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="18f6b-117">Questa operazione restituisce l'oggetto corrispondente tooan zona esistente in Azure DNS della zona DNS.</span><span class="sxs-lookup"><span data-stu-id="18f6b-117">This operation returns a DNS zone object corresponding tooan existing zone in Azure DNS.</span></span> <span data-ttu-id="18f6b-118">Hello oggetto contiene i dati sull'area di hello (ad esempio numero hello di set di record), ma non contiene alcun set di record hello stessi (vedere `Get-AzureRmDnsRecordSet`).</span><span class="sxs-lookup"><span data-stu-id="18f6b-118">hello object contains data about hello zone (such as hello number of record sets), but does not contain hello record sets themselves (see `Get-AzureRmDnsRecordSet`).</span></span>

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

## <a name="list-dns-zones"></a><span data-ttu-id="18f6b-119">Elencare le zone DNS</span><span class="sxs-lookup"><span data-stu-id="18f6b-119">List DNS zones</span></span>

<span data-ttu-id="18f6b-120">Omettendo il nome della zona hello `Get-AzureRmDnsZone`, è possibile enumerare tutte le zone in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="18f6b-120">By omitting hello zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group.</span></span> <span data-ttu-id="18f6b-121">Questa operazione restituisce una matrice di oggetti di zona.</span><span class="sxs-lookup"><span data-stu-id="18f6b-121">This operation returns an array of zone objects.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="18f6b-122">Omettendo il nome di zona hello e nome del gruppo di risorse hello da `Get-AzureRmDnsZone`, è possibile enumerare tutte le zone di hello sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="18f6b-122">By omitting both hello zone name and hello resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in hello Azure subscription.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="18f6b-123">Aggiornare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="18f6b-123">Update a DNS zone</span></span>

<span data-ttu-id="18f6b-124">Modifica risorsa di zona DNS può essere reso usando tooa `Set-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="18f6b-124">Changes tooa DNS zone resource can be made by using `Set-AzureRmDnsZone`.</span></span> <span data-ttu-id="18f6b-125">Questo cmdlet non aggiorna hello DNS set di record nella zona hello (vedere [come i record DNS tooManage](dns-operations-recordsets.md)).</span><span class="sxs-lookup"><span data-stu-id="18f6b-125">This cmdlet does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets.md)).</span></span> <span data-ttu-id="18f6b-126">È utilizzato solo proprietà tooupdate della risorsa di zona hello stessa.</span><span class="sxs-lookup"><span data-stu-id="18f6b-126">It's only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="18f6b-127">proprietà della zona scrivibile Hello sono attualmente limitata toohello [Azure Resource Manager 'tag' per la risorsa di zona hello](dns-zones-records.md#tags).</span><span class="sxs-lookup"><span data-stu-id="18f6b-127">hello writable zone properties are currently limited toohello [Azure Resource Manager ‘tags’ for hello zone resource](dns-zones-records.md#tags).</span></span>

<span data-ttu-id="18f6b-128">Utilizzare uno dei seguenti due modi tooupdate hello una zona DNS:</span><span class="sxs-lookup"><span data-stu-id="18f6b-128">Use one of hello following two ways tooupdate a DNS zone:</span></span>

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group"></a><span data-ttu-id="18f6b-129">Specificare il fuso hello con gruppo di risorse e nome zona hello</span><span class="sxs-lookup"><span data-stu-id="18f6b-129">Specify hello zone using hello zone name and resource group</span></span>

<span data-ttu-id="18f6b-130">Questo approccio sostituisce i tag zona hello esistenti con i valori hello specificati.</span><span class="sxs-lookup"><span data-stu-id="18f6b-130">This approach replaces hello existing zone tags with hello values specified.</span></span>

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-hello-zone-using-a-zone-object"></a><span data-ttu-id="18f6b-131">Specificare il fuso hello utilizzando un oggetto $zone</span><span class="sxs-lookup"><span data-stu-id="18f6b-131">Specify hello zone using a $zone object</span></span>

<span data-ttu-id="18f6b-132">Questo approccio recupera l'oggetto zona esistente hello Modifica tag hello e quindi esegue il commit delle modifiche hello.</span><span class="sxs-lookup"><span data-stu-id="18f6b-132">This approach retrieves hello existing zone object, modifies hello tags, and then commits hello changes.</span></span> <span data-ttu-id="18f6b-133">Ciò consente di conservare i tag esistenti.</span><span class="sxs-lookup"><span data-stu-id="18f6b-133">In this way, existing tags can be preserved.</span></span>

```powershell
# Get hello zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="18f6b-134">Quando si utilizza `Set-AzureRmDnsZone` con un oggetto $zone, [Etag controlla](dns-zones-records.md#etags) vengono utilizzate le modifiche simultanee tooensure non vengono sovrascritti.</span><span class="sxs-lookup"><span data-stu-id="18f6b-134">When using `Set-AzureRmDnsZone` with a $zone object, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="18f6b-135">È possibile utilizzare hello facoltativo `-Overwrite` passare toosuppress questi controlli.</span><span class="sxs-lookup"><span data-stu-id="18f6b-135">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

## <a name="delete-a-dns-zone"></a><span data-ttu-id="18f6b-136">Eliminare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="18f6b-136">Delete a DNS Zone</span></span>

<span data-ttu-id="18f6b-137">È possibile eliminare le zone DNS tramite hello `Remove-AzureRmDnsZone` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="18f6b-137">DNS zones can be deleted using hello `Remove-AzureRmDnsZone` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="18f6b-138">L'eliminazione di una zona DNS elimina inoltre tutti i record DNS nella zona hello.</span><span class="sxs-lookup"><span data-stu-id="18f6b-138">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="18f6b-139">Questa operazione non può essere annullata.</span><span class="sxs-lookup"><span data-stu-id="18f6b-139">This operation cannot be undone.</span></span> <span data-ttu-id="18f6b-140">Se zona DNS hello è in uso, con zone hello services avrà esito negativo quando viene eliminata hello.</span><span class="sxs-lookup"><span data-stu-id="18f6b-140">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="18f6b-141">tooprotect l'eliminazione accidentale di zona, vedere [come tooprotect DNS zone e record](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="18f6b-141">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>


<span data-ttu-id="18f6b-142">Utilizzare uno dei seguenti due modi toodelete hello una zona DNS:</span><span class="sxs-lookup"><span data-stu-id="18f6b-142">Use one of hello following two ways toodelete a DNS zone:</span></span>

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group-name"></a><span data-ttu-id="18f6b-143">Specificare il fuso hello utilizzando nome zona hello e nome del gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="18f6b-143">Specify hello zone using hello zone name and resource group name</span></span>

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-hello-zone-using-a-zone-object"></a><span data-ttu-id="18f6b-144">Specificare il fuso hello utilizzando un oggetto $zone</span><span class="sxs-lookup"><span data-stu-id="18f6b-144">Specify hello zone using a $zone object</span></span>

<span data-ttu-id="18f6b-145">È possibile specificare toobe zona hello eliminato usando un `$zone` oggetto restituito da `Get-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="18f6b-145">You can specify hello zone toobe deleted using a `$zone` object returned by `Get-AzureRmDnsZone`.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="18f6b-146">oggetto fuso Hello può anche essere reindirizzato anziché passato come parametro:</span><span class="sxs-lookup"><span data-stu-id="18f6b-146">hello zone object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

<span data-ttu-id="18f6b-147">Come con `Set-AzureRmDnsZone`, specificando hello zona utilizzando un `$zone` oggetto Abilita Etag Controlla modifiche simultanee tooensure non vengono eliminate.</span><span class="sxs-lookup"><span data-stu-id="18f6b-147">As with `Set-AzureRmDnsZone`, specifying hello zone using a `$zone` object enables Etag checks tooensure concurrent changes are not deleted.</span></span> <span data-ttu-id="18f6b-148">Hello utilizzare `-Overwrite` passare toosuppress questi controlli.</span><span class="sxs-lookup"><span data-stu-id="18f6b-148">Use hello `-Overwrite` switch toosuppress these checks.</span></span>

## <a name="confirmation-prompts"></a><span data-ttu-id="18f6b-149">Richieste di conferma</span><span class="sxs-lookup"><span data-stu-id="18f6b-149">Confirmation prompts</span></span>

<span data-ttu-id="18f6b-150">Hello `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, e `Remove-AzureRmDnsZone` tutti i cmdlet supportano richieste di conferma.</span><span class="sxs-lookup"><span data-stu-id="18f6b-150">hello `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, and `Remove-AzureRmDnsZone` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="18f6b-151">Entrambi `New-AzureRmDnsZone` e `Set-AzureRmDnsZone` chiede conferma se hello `$ConfirmPreference` variabile di preferenza PowerShell ha un valore di `Medium` o inferiore.</span><span class="sxs-lookup"><span data-stu-id="18f6b-151">Both `New-AzureRmDnsZone` and `Set-AzureRmDnsZone` prompt for confirmation if hello `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="18f6b-152">A causa di impatto potenzialmente elevato di toohello dell'eliminazione di una zona DNS, hello `Remove-AzureRmDnsZone` cmdlet chiede conferma se hello `$ConfirmPreference` variabile PowerShell ha un valore diverso da `None`.</span><span class="sxs-lookup"><span data-stu-id="18f6b-152">Due toohello potentially high impact of deleting a DNS zone, hello `Remove-AzureRmDnsZone` cmdlet prompts for confirmation if hello `$ConfirmPreference` PowerShell variable has any value other than `None`.</span></span>

<span data-ttu-id="18f6b-153">Poiché il valore predefinito hello per `$ConfirmPreference` è `High`, solo `Remove-AzureRmDnsZone` chiesta la conferma per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="18f6b-153">Since hello default value for `$ConfirmPreference` is `High`, only `Remove-AzureRmDnsZone` prompts for confirmation by default.</span></span>

<span data-ttu-id="18f6b-154">È possibile eseguire l'override di hello corrente `$ConfirmPreference` impostazione utilizzando hello `-Confirm` parametro.</span><span class="sxs-lookup"><span data-stu-id="18f6b-154">You can override hello current `$ConfirmPreference` setting using hello `-Confirm` parameter.</span></span> <span data-ttu-id="18f6b-155">Se si specifica `-Confirm` o `-Confirm:$True` , hello cmdlet chiede conferma prima dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="18f6b-155">If you specify `-Confirm` or `-Confirm:$True` , hello cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="18f6b-156">Se si specifica `-Confirm:$False` , hello cmdlet non viene chiesto di confermare.</span><span class="sxs-lookup"><span data-stu-id="18f6b-156">If you specify `-Confirm:$False` , hello cmdlet does not prompt you for confirmation.</span></span>

<span data-ttu-id="18f6b-157">Per altre informazioni su `-Confirm` e `$ConfirmPreference`, vedere [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables) (Informazioni sulle variabili di preferenza).</span><span class="sxs-lookup"><span data-stu-id="18f6b-157">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="18f6b-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="18f6b-158">Next steps</span></span>

<span data-ttu-id="18f6b-159">Informazioni su come troppo[gestire set di record e i record](dns-operations-recordsets.md) nella zona DNS.</span><span class="sxs-lookup"><span data-stu-id="18f6b-159">Learn how too[manage record sets and records](dns-operations-recordsets.md) in your DNS zone.</span></span>
<br>
<span data-ttu-id="18f6b-160">Informazioni su come troppo[delegare il tooAzure di dominio DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="18f6b-160">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>
<br>
<span data-ttu-id="18f6b-161">Hello revisione [la documentazione di riferimento di Azure PowerShell DNS](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="18f6b-161">Review hello [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>

