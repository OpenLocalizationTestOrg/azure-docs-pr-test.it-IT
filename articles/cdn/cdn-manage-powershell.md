---
title: rete CDN di Azure con PowerShell aaaManage | Documenti Microsoft
description: Informazioni su come toouse hello Azure PowerShell cmdlet toomanage rete CDN di Azure.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: fb6f57a5-6e26-4847-8fd9-b51fb05a79eb
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 269373136d4ef018e4d31f147456b4be2253b463
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-cdn-with-powershell"></a><span data-ttu-id="843e5-103">Gestire la rete CDN di Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="843e5-103">Manage Azure CDN with PowerShell</span></span>
<span data-ttu-id="843e5-104">PowerShell fornisce uno dei toomanage metodi più flessibile hello i profili di rete CDN di Azure e l'endpoint.</span><span class="sxs-lookup"><span data-stu-id="843e5-104">PowerShell provides one of hello most flexible methods toomanage your Azure CDN profiles and endpoints.</span></span>  <span data-ttu-id="843e5-105">È possibile utilizzare PowerShell in modo interattivo o scrivendo script tooautomate attività di gestione.</span><span class="sxs-lookup"><span data-stu-id="843e5-105">You can use PowerShell interactively or by writing scripts tooautomate management tasks.</span></span>  <span data-ttu-id="843e5-106">In questa esercitazione vengono illustrate diverse di attività più comuni di hello è possibile eseguire con PowerShell toomanage i profili di rete CDN di Azure e l'endpoint.</span><span class="sxs-lookup"><span data-stu-id="843e5-106">This tutorial demonstrates several of hello most common tasks you can accomplish with PowerShell toomanage your Azure CDN profiles and endpoints.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="843e5-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="843e5-107">Prerequisites</span></span>
<span data-ttu-id="843e5-108">toouse PowerShell toomanage i profili di rete CDN di Azure e un endpoint, è necessario che il modulo di Azure PowerShell hello installato.</span><span class="sxs-lookup"><span data-stu-id="843e5-108">toouse PowerShell toomanage your Azure CDN profiles and endpoints, you must have hello Azure PowerShell module installed.</span></span>  <span data-ttu-id="843e5-109">toolearn come tooinstall Azure PowerShell e connettersi usando hello tooAzure `Login-AzureRmAccount` cmdlet, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="843e5-109">toolearn how tooinstall Azure PowerShell and connect tooAzure using hello `Login-AzureRmAccount` cmdlet, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="843e5-110">È necessario accedere con `Login-AzureRmAccount` per poter eseguire i cmdlet di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="843e5-110">You must log in with `Login-AzureRmAccount` before you can execute Azure PowerShell cmdlets.</span></span>
> 
> 

## <a name="listing-hello-azure-cdn-cmdlets"></a><span data-ttu-id="843e5-111">Elenca i cmdlet di hello rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="843e5-111">Listing hello Azure CDN cmdlets</span></span>
<span data-ttu-id="843e5-112">È possibile elencare tutti i cmdlet di Azure CDN hello utilizzando hello `Get-Command` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="843e5-112">You can list all hello Azure CDN cmdlets using hello `Get-Command` cmdlet.</span></span>

```text
PS C:\> Get-Command -Module AzureRM.Cdn

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Get-AzureRmCdnCustomDomain                         2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnEndpointNameAvailability             2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnOrigin                               2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnProfileSsoUrl                        2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnCustomDomain                         2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Publish-AzureRmCdnEndpointContent                  2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnCustomDomain                      2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnEndpoint                          2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnProfile                           2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnOrigin                               2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Start-AzureRmCdnEndpoint                           2.0.0      AzureRm.Cdn
Cmdlet          Stop-AzureRmCdnEndpoint                            2.0.0      AzureRm.Cdn
Cmdlet          Test-AzureRmCdnCustomDomain                        2.0.0      AzureRm.Cdn
Cmdlet          Unpublish-AzureRmCdnEndpointContent                2.0.0      AzureRm.Cdn
```

## <a name="getting-help"></a><span data-ttu-id="843e5-113">Risorse della Guida</span><span class="sxs-lookup"><span data-stu-id="843e5-113">Getting help</span></span>
<span data-ttu-id="843e5-114">È possibile ottenere assistenza con uno qualsiasi di questi cmdlet utilizzando hello `Get-Help` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="843e5-114">You can get help with any of these cmdlets using hello `Get-Help` cmdlet.</span></span>  <span data-ttu-id="843e5-115">`Get-Help` fornisce la sintassi e facoltativamente illustra gli esempi.</span><span class="sxs-lookup"><span data-stu-id="843e5-115">`Get-Help` provides usage and syntax, and optionally shows examples.</span></span>

```text
PS C:\> Get-Help Get-AzureRmCdnProfile

NAME
    Get-AzureRmCdnProfile

SYNOPSIS
    Gets an Azure CDN profile.


SYNTAX
    Get-AzureRmCdnProfile [-ProfileName <String>] [-ResourceGroupName <String>] [-InformationAction
    <ActionPreference>] [-InformationVariable <String>] [<CommonParameters>]


DESCRIPTION
    Gets an Azure CDN profile and all related information.


RELATED LINKS

REMARKS
    toosee hello examples, type: "get-help Get-AzureRmCdnProfile -examples".
    For more information, type: "get-help Get-AzureRmCdnProfile -detailed".
    For technical information, type: "get-help Get-AzureRmCdnProfile -full".

```

## <a name="listing-existing-azure-cdn-profiles"></a><span data-ttu-id="843e5-116">Inclusione in elenco dei profili della rete CDN di Azure esistenti</span><span class="sxs-lookup"><span data-stu-id="843e5-116">Listing existing Azure CDN profiles</span></span>
<span data-ttu-id="843e5-117">Hello `Get-AzureRmCdnProfile` cmdlet senza parametri consente di recuperare tutti i profili di rete CDN esistenti.</span><span class="sxs-lookup"><span data-stu-id="843e5-117">hello `Get-AzureRmCdnProfile` cmdlet without any parameters retrieves all your existing CDN profiles.</span></span>

```powershell
Get-AzureRmCdnProfile
```

<span data-ttu-id="843e5-118">Questo output può essere reindirizzato toocmdlets per l'enumerazione.</span><span class="sxs-lookup"><span data-stu-id="843e5-118">This output can be piped toocmdlets for enumeration.</span></span>

```powershell
# Output hello name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

<span data-ttu-id="843e5-119">È inoltre possibile restituire un unico profilo specificando nome e la risorsa gruppo di profili di hello.</span><span class="sxs-lookup"><span data-stu-id="843e5-119">You can also return a single profile by specifying hello profile name and resource group.</span></span>

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> <span data-ttu-id="843e5-120">È possibile toohave CDN più profili con hello stesso nome, purché si trovano in gruppi di risorse diverso.</span><span class="sxs-lookup"><span data-stu-id="843e5-120">It is possible toohave multiple CDN profiles with hello same name, so long as they are in different resource groups.</span></span>  <span data-ttu-id="843e5-121">L'omissione di hello `ResourceGroupName` parametro restituisce tutti i profili con un nome corrispondente.</span><span class="sxs-lookup"><span data-stu-id="843e5-121">Omitting hello `ResourceGroupName` parameter returns all profiles with a matching name.</span></span>
> 
> 

## <a name="listing-existing-cdn-endpoints"></a><span data-ttu-id="843e5-122">Inclusione in elenco degli endpoint della rete CDN esistenti</span><span class="sxs-lookup"><span data-stu-id="843e5-122">Listing existing CDN endpoints</span></span>
<span data-ttu-id="843e5-123">`Get-AzureRmCdnEndpoint`recuperare tutti gli endpoint hello in un profilo o un singolo endpoint.</span><span class="sxs-lookup"><span data-stu-id="843e5-123">`Get-AzureRmCdnEndpoint` can retrieve an individual endpoint or all hello endpoints on a profile.</span></span>  

```powershell
# Get a single endpoint.
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Get all of hello endpoints on a given profile. 
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG

# Return all of hello endpoints on all of hello profiles.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint

# Return all of hello endpoints in this subscription that are currently running.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Where-Object { $_.ResourceState -eq "Running" }
```

## <a name="creating-cdn-profiles-and-endpoints"></a><span data-ttu-id="843e5-124">Creazione dei profili e degli endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="843e5-124">Creating CDN profiles and endpoints</span></span>
<span data-ttu-id="843e5-125">`New-AzureRmCdnProfile`e `New-AzureRmCdnEndpoint` sono i profili di rete CDN toocreate utilizzato e gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="843e5-125">`New-AzureRmCdnProfile` and `New-AzureRmCdnEndpoint` are used toocreate CDN profiles and endpoints.</span></span>

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a><span data-ttu-id="843e5-126">Controllo della disponibilità del nome dell'endpoint</span><span class="sxs-lookup"><span data-stu-id="843e5-126">Checking endpoint name availability</span></span>
<span data-ttu-id="843e5-127">`Get-AzureRmCdnEndpointNameAvailability` restituisce un oggetto indicante se un nome di endpoint è disponibile.</span><span class="sxs-lookup"><span data-stu-id="843e5-127">`Get-AzureRmCdnEndpointNameAvailability` returns an object indicating if an endpoint name is available.</span></span>

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message toohello console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a><span data-ttu-id="843e5-128">Aggiunta di un dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="843e5-128">Adding a custom domain</span></span>
<span data-ttu-id="843e5-129">`New-AzureRmCdnCustomDomain`Aggiunge un endpoint della tooan nome dominio personalizzato esistente.</span><span class="sxs-lookup"><span data-stu-id="843e5-129">`New-AzureRmCdnCustomDomain` adds a custom domain name tooan existing endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="843e5-130">È necessario impostare hello CNAME con il provider DNS come descritto in [come endpoint di rete (CDN) di toomap dominio personalizzato tooContent](cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="843e5-130">You must set up hello CNAME with your DNS provider as described in [How toomap Custom Domain tooContent Delivery Network (CDN) endpoint](cdn-map-content-to-custom-domain.md).</span></span>  <span data-ttu-id="843e5-131">È possibile verificare il mapping di hello prima di modificare l'endpoint utilizzando `Test-AzureRmCdnCustomDomain`.</span><span class="sxs-lookup"><span data-stu-id="843e5-131">You can test hello mapping before modifying your endpoint using `Test-AzureRmCdnCustomDomain`.</span></span>
> 
> 

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Check hello mapping
$result = Test-AzureRmCdnCustomDomain -CdnEndpoint $endpoint -CustomDomainHostName "cdn.contoso.com"

# Create hello custom domain on hello endpoint
If($result.CustomDomainValidated){ New-AzureRmCdnCustomDomain -CustomDomainName Contoso -HostName "cdn.contoso.com" -CdnEndpoint $endpoint }
```

## <a name="modifying-an-endpoint"></a><span data-ttu-id="843e5-132">Modifica di un endpoint</span><span class="sxs-lookup"><span data-stu-id="843e5-132">Modifying an endpoint</span></span>
<span data-ttu-id="843e5-133">`Set-AzureRmCdnEndpoint` modifica un endpoint esistente.</span><span class="sxs-lookup"><span data-stu-id="843e5-133">`Set-AzureRmCdnEndpoint` modifies an existing endpoint.</span></span>

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save hello changed endpoint and apply hello changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a><span data-ttu-id="843e5-134">Ripulitura/Precaricamento degli asset della rete CDN</span><span class="sxs-lookup"><span data-stu-id="843e5-134">Purging/Pre-loading CDN assets</span></span>
<span data-ttu-id="843e5-135">`Unpublish-AzureRmCdnEndpointContent` ripulisce gli asset nella cache, mentre `Publish-AzureRmCdnEndpointContent` precarica gli asset negli endpoint supportati.</span><span class="sxs-lookup"><span data-stu-id="843e5-135">`Unpublish-AzureRmCdnEndpointContent` purges cached assets, while `Publish-AzureRmCdnEndpointContent` pre-loads assets on supported endpoints.</span></span>

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a><span data-ttu-id="843e5-136">Avvio/Arresto degli endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="843e5-136">Starting/Stopping CDN endpoints</span></span>
<span data-ttu-id="843e5-137">`Start-AzureRmCdnEndpoint`e `Stop-AzureRmCdnEndpoint` possibile toostart utilizzato e arresta l'endpoint singoli o gruppi di endpoint.</span><span class="sxs-lookup"><span data-stu-id="843e5-137">`Start-AzureRmCdnEndpoint` and `Stop-AzureRmCdnEndpoint` can be used toostart and stop individual endpoints or groups of endpoints.</span></span>

```powershell
# Stop hello cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a><span data-ttu-id="843e5-138">Eliminazione di risorse della rete CDN</span><span class="sxs-lookup"><span data-stu-id="843e5-138">Deleting CDN resources</span></span>
<span data-ttu-id="843e5-139">`Remove-AzureRmCdnProfile`e `Remove-AzureRmCdnEndpoint` possono essere utilizzati tooremove profili e gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="843e5-139">`Remove-AzureRmCdnProfile` and `Remove-AzureRmCdnEndpoint` can be used tooremove profiles and endpoints.</span></span>

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all hello endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a><span data-ttu-id="843e5-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="843e5-140">Next Steps</span></span>
<span data-ttu-id="843e5-141">Informazioni su come tooautomate rete CDN di Azure con [.NET](cdn-app-dev-net.md) o [Node.js](cdn-app-dev-node.md).</span><span class="sxs-lookup"><span data-stu-id="843e5-141">Learn how tooautomate Azure CDN with [.NET](cdn-app-dev-net.md) or [Node.js](cdn-app-dev-node.md).</span></span>

<span data-ttu-id="843e5-142">toolearn sulle funzionalità di rete CDN, vedere [Panoramica della rete CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="843e5-142">toolearn about CDN features, see [CDN Overview](cdn-overview.md).</span></span>

