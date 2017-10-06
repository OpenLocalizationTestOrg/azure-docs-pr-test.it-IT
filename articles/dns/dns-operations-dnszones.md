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
# <a name="how-toomanage-dns-zones-using-powershell"></a>Come le zone DNS toomanage tramite PowerShell

> [!div class="op_single_selector"]
> * [Portale](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Interfaccia della riga di comando di Azure 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Interfaccia della riga di comando di Azure 2.0](dns-operations-dnszones-cli.md)

Questo articolo illustra come toomanage zone DNS tramite Azure PowerShell. È inoltre possibile gestire le zone DNS utilizzando hello multipiattaforma [CLI di Azure](dns-operations-dnszones-cli.md) o hello portale di Azure.

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a>Creare una zona DNS

Una zona DNS viene creata utilizzando hello `New-AzureRmDnsZone` cmdlet.

esempio Hello crea una zona DNS denominata *contoso.com* nel gruppo di risorse hello chiamato *MyResourceGroup*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

Hello esempio seguente viene illustrato come della zona DNS toocreate con due [tag Azure Resource Manager](dns-zones-records.md#tags), *progetto = demo* e *env = test*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a>Ottenere una zona DNS

tooretrieve una zona DNS, utilizzare hello `Get-AzureRmDnsZone` cmdlet. Questa operazione restituisce l'oggetto corrispondente tooan zona esistente in Azure DNS della zona DNS. Hello oggetto contiene i dati sull'area di hello (ad esempio numero hello di set di record), ma non contiene alcun set di record hello stessi (vedere `Get-AzureRmDnsRecordSet`).

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

## <a name="list-dns-zones"></a>Elencare le zone DNS

Omettendo il nome della zona hello `Get-AzureRmDnsZone`, è possibile enumerare tutte le zone in un gruppo di risorse. Questa operazione restituisce una matrice di oggetti di zona.

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

Omettendo il nome di zona hello e nome del gruppo di risorse hello da `Get-AzureRmDnsZone`, è possibile enumerare tutte le zone di hello sottoscrizione di Azure.

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a>Aggiornare una zona DNS

Modifica risorsa di zona DNS può essere reso usando tooa `Set-AzureRmDnsZone`. Questo cmdlet non aggiorna hello DNS set di record nella zona hello (vedere [come i record DNS tooManage](dns-operations-recordsets.md)). È utilizzato solo proprietà tooupdate della risorsa di zona hello stessa. proprietà della zona scrivibile Hello sono attualmente limitata toohello [Azure Resource Manager 'tag' per la risorsa di zona hello](dns-zones-records.md#tags).

Utilizzare uno dei seguenti due modi tooupdate hello una zona DNS:

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group"></a>Specificare il fuso hello con gruppo di risorse e nome zona hello

Questo approccio sostituisce i tag zona hello esistenti con i valori hello specificati.

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-hello-zone-using-a-zone-object"></a>Specificare il fuso hello utilizzando un oggetto $zone

Questo approccio recupera l'oggetto zona esistente hello Modifica tag hello e quindi esegue il commit delle modifiche hello. Ciò consente di conservare i tag esistenti.

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

Quando si utilizza `Set-AzureRmDnsZone` con un oggetto $zone, [Etag controlla](dns-zones-records.md#etags) vengono utilizzate le modifiche simultanee tooensure non vengono sovrascritti. È possibile utilizzare hello facoltativo `-Overwrite` passare toosuppress questi controlli.

## <a name="delete-a-dns-zone"></a>Eliminare una zona DNS

È possibile eliminare le zone DNS tramite hello `Remove-AzureRmDnsZone` cmdlet.

> [!NOTE]
> L'eliminazione di una zona DNS elimina inoltre tutti i record DNS nella zona hello. Questa operazione non può essere annullata. Se zona DNS hello è in uso, con zone hello services avrà esito negativo quando viene eliminata hello.
>
>tooprotect l'eliminazione accidentale di zona, vedere [come tooprotect DNS zone e record](dns-protect-zones-recordsets.md).


Utilizzare uno dei seguenti due modi toodelete hello una zona DNS:

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group-name"></a>Specificare il fuso hello utilizzando nome zona hello e nome del gruppo di risorse

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-hello-zone-using-a-zone-object"></a>Specificare il fuso hello utilizzando un oggetto $zone

È possibile specificare toobe zona hello eliminato usando un `$zone` oggetto restituito da `Get-AzureRmDnsZone`.

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

oggetto fuso Hello può anche essere reindirizzato anziché passato come parametro:

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

Come con `Set-AzureRmDnsZone`, specificando hello zona utilizzando un `$zone` oggetto Abilita Etag Controlla modifiche simultanee tooensure non vengono eliminate. Hello utilizzare `-Overwrite` passare toosuppress questi controlli.

## <a name="confirmation-prompts"></a>Richieste di conferma

Hello `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, e `Remove-AzureRmDnsZone` tutti i cmdlet supportano richieste di conferma.

Entrambi `New-AzureRmDnsZone` e `Set-AzureRmDnsZone` chiede conferma se hello `$ConfirmPreference` variabile di preferenza PowerShell ha un valore di `Medium` o inferiore. A causa di impatto potenzialmente elevato di toohello dell'eliminazione di una zona DNS, hello `Remove-AzureRmDnsZone` cmdlet chiede conferma se hello `$ConfirmPreference` variabile PowerShell ha un valore diverso da `None`.

Poiché il valore predefinito hello per `$ConfirmPreference` è `High`, solo `Remove-AzureRmDnsZone` chiesta la conferma per impostazione predefinita.

È possibile eseguire l'override di hello corrente `$ConfirmPreference` impostazione utilizzando hello `-Confirm` parametro. Se si specifica `-Confirm` o `-Confirm:$True` , hello cmdlet chiede conferma prima dell'esecuzione. Se si specifica `-Confirm:$False` , hello cmdlet non viene chiesto di confermare.

Per altre informazioni su `-Confirm` e `$ConfirmPreference`, vedere [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables) (Informazioni sulle variabili di preferenza).

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come troppo[gestire set di record e i record](dns-operations-recordsets.md) nella zona DNS.
<br>
Informazioni su come troppo[delegare il tooAzure di dominio DNS](dns-domain-delegation.md).
<br>
Hello revisione [la documentazione di riferimento di Azure PowerShell DNS](/powershell/module/azurerm.dns).

