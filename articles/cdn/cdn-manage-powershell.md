---
title: Gestire la rete CDN di Azure con PowerShell | Microsoft Docs
description: Informazioni su come usare i cmdlet di Azure PowerShell per gestire la rete CDN di Azure.
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
ms.openlocfilehash: 5bd2eed7b34cafa43e8f38279890405d4ae55568
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-cdn-with-powershell"></a><span data-ttu-id="20b12-103">Gestire la rete CDN di Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="20b12-103">Manage Azure CDN with PowerShell</span></span>
<span data-ttu-id="20b12-104">PowerShell offre uno dei metodi più flessibili per gestire i profili e gli endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="20b12-104">PowerShell provides one of the most flexible methods to manage your Azure CDN profiles and endpoints.</span></span>  <span data-ttu-id="20b12-105">È possibile usare PowerShell in modo interattivo o scrivendo script per automatizzare le attività di gestione.</span><span class="sxs-lookup"><span data-stu-id="20b12-105">You can use PowerShell interactively or by writing scripts to automate management tasks.</span></span>  <span data-ttu-id="20b12-106">Questa esercitazione illustra alcune delle attività più comuni che è possibile eseguire con PowerShell per gestire i profili e gli endpoint della rete CDN di Azure.</span><span class="sxs-lookup"><span data-stu-id="20b12-106">This tutorial demonstrates several of the most common tasks you can accomplish with PowerShell to manage your Azure CDN profiles and endpoints.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20b12-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="20b12-107">Prerequisites</span></span>
<span data-ttu-id="20b12-108">Per usare PowerShell per gestire i profili e gli endpoint della rete CDN di Azure, è necessario avere il modulo Azure PowerShell installato.</span><span class="sxs-lookup"><span data-stu-id="20b12-108">To use PowerShell to manage your Azure CDN profiles and endpoints, you must have the Azure PowerShell module installed.</span></span>  <span data-ttu-id="20b12-109">Per informazioni su come installare Azure PowerShell e connettersi ad Azure usando il cmdlet `Login-AzureRmAccount`[Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="20b12-109">To learn how to install Azure PowerShell and connect to Azure using the `Login-AzureRmAccount` cmdlet, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20b12-110">È necessario accedere con `Login-AzureRmAccount` per poter eseguire i cmdlet di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="20b12-110">You must log in with `Login-AzureRmAccount` before you can execute Azure PowerShell cmdlets.</span></span>
> 
> 

## <a name="listing-the-azure-cdn-cmdlets"></a><span data-ttu-id="20b12-111">Inclusione in elenco dei cmdlet della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="20b12-111">Listing the Azure CDN cmdlets</span></span>
<span data-ttu-id="20b12-112">È elencare tutti i cmdlet della rete CDN di Azure usando il cmdlet `Get-Command` .</span><span class="sxs-lookup"><span data-stu-id="20b12-112">You can list all the Azure CDN cmdlets using the `Get-Command` cmdlet.</span></span>

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

## <a name="getting-help"></a><span data-ttu-id="20b12-113">Risorse della Guida</span><span class="sxs-lookup"><span data-stu-id="20b12-113">Getting help</span></span>
<span data-ttu-id="20b12-114">È possibile visualizzare la Guida con uno di questi cmdlet usando il cmdlet `Get-Help` .</span><span class="sxs-lookup"><span data-stu-id="20b12-114">You can get help with any of these cmdlets using the `Get-Help` cmdlet.</span></span>  <span data-ttu-id="20b12-115">`Get-Help` fornisce la sintassi e facoltativamente illustra gli esempi.</span><span class="sxs-lookup"><span data-stu-id="20b12-115">`Get-Help` provides usage and syntax, and optionally shows examples.</span></span>

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
    To see the examples, type: "get-help Get-AzureRmCdnProfile -examples".
    For more information, type: "get-help Get-AzureRmCdnProfile -detailed".
    For technical information, type: "get-help Get-AzureRmCdnProfile -full".

```

## <a name="listing-existing-azure-cdn-profiles"></a><span data-ttu-id="20b12-116">Inclusione in elenco dei profili della rete CDN di Azure esistenti</span><span class="sxs-lookup"><span data-stu-id="20b12-116">Listing existing Azure CDN profiles</span></span>
<span data-ttu-id="20b12-117">Il cmdlet `Get-AzureRmCdnProfile` senza alcun parametro recupera tutti i profili della rete CDN esistenti.</span><span class="sxs-lookup"><span data-stu-id="20b12-117">The `Get-AzureRmCdnProfile` cmdlet without any parameters retrieves all your existing CDN profiles.</span></span>

```powershell
Get-AzureRmCdnProfile
```

<span data-ttu-id="20b12-118">È possibile inviare pipe di questo output ai cmdlet per l'enumerazione.</span><span class="sxs-lookup"><span data-stu-id="20b12-118">This output can be piped to cmdlets for enumeration.</span></span>

```powershell
# Output the name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

<span data-ttu-id="20b12-119">È anche possibile restituire un solo profilo specificando il gruppo di risorse e il nome del profilo.</span><span class="sxs-lookup"><span data-stu-id="20b12-119">You can also return a single profile by specifying the profile name and resource group.</span></span>

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> <span data-ttu-id="20b12-120">È possibile avere più profili della rete CDN con lo stesso nome, purché siano in gruppi di risorse diversi.</span><span class="sxs-lookup"><span data-stu-id="20b12-120">It is possible to have multiple CDN profiles with the same name, so long as they are in different resource groups.</span></span>  <span data-ttu-id="20b12-121">Se si omette il parametro `ResourceGroupName` , vengono restituiti tutti i profili con un nome corrispondente.</span><span class="sxs-lookup"><span data-stu-id="20b12-121">Omitting the `ResourceGroupName` parameter returns all profiles with a matching name.</span></span>
> 
> 

## <a name="listing-existing-cdn-endpoints"></a><span data-ttu-id="20b12-122">Inclusione in elenco degli endpoint della rete CDN esistenti</span><span class="sxs-lookup"><span data-stu-id="20b12-122">Listing existing CDN endpoints</span></span>
<span data-ttu-id="20b12-123">`Get-AzureRmCdnEndpoint` può recuperare un singolo endpoint o tutti gli endpoint in un profilo.</span><span class="sxs-lookup"><span data-stu-id="20b12-123">`Get-AzureRmCdnEndpoint` can retrieve an individual endpoint or all the endpoints on a profile.</span></span>  

```powershell
# Get a single endpoint.
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Get all of the endpoints on a given profile. 
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG

# Return all of the endpoints on all of the profiles.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint

# Return all of the endpoints in this subscription that are currently running.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Where-Object { $_.ResourceState -eq "Running" }
```

## <a name="creating-cdn-profiles-and-endpoints"></a><span data-ttu-id="20b12-124">Creazione dei profili e degli endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="20b12-124">Creating CDN profiles and endpoints</span></span>
<span data-ttu-id="20b12-125">`New-AzureRmCdnProfile` e `New-AzureRmCdnEndpoint` vengono usati per creare profili ed endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="20b12-125">`New-AzureRmCdnProfile` and `New-AzureRmCdnEndpoint` are used to create CDN profiles and endpoints.</span></span>

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a><span data-ttu-id="20b12-126">Controllo della disponibilità del nome dell'endpoint</span><span class="sxs-lookup"><span data-stu-id="20b12-126">Checking endpoint name availability</span></span>
<span data-ttu-id="20b12-127">`Get-AzureRmCdnEndpointNameAvailability` restituisce un oggetto indicante se un nome di endpoint è disponibile.</span><span class="sxs-lookup"><span data-stu-id="20b12-127">`Get-AzureRmCdnEndpointNameAvailability` returns an object indicating if an endpoint name is available.</span></span>

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message to the console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a><span data-ttu-id="20b12-128">Aggiunta di un dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="20b12-128">Adding a custom domain</span></span>
<span data-ttu-id="20b12-129">`New-AzureRmCdnCustomDomain` aggiunge un nome di dominio personalizzato a un endpoint esistente.</span><span class="sxs-lookup"><span data-stu-id="20b12-129">`New-AzureRmCdnCustomDomain` adds a custom domain name to an existing endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20b12-130">È necessario configurare CNAME con il provider DNS, come illustrato in [Come eseguire il mapping di un dominio personalizzato all'endpoint della rete per la distribuzione di contenuti (rete CDN)](cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="20b12-130">You must set up the CNAME with your DNS provider as described in [How to map Custom Domain to Content Delivery Network (CDN) endpoint](cdn-map-content-to-custom-domain.md).</span></span>  <span data-ttu-id="20b12-131">È possibile testare il mapping prima di modificare l'endpoint usando `Test-AzureRmCdnCustomDomain`.</span><span class="sxs-lookup"><span data-stu-id="20b12-131">You can test the mapping before modifying your endpoint using `Test-AzureRmCdnCustomDomain`.</span></span>
> 
> 

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Check the mapping
$result = Test-AzureRmCdnCustomDomain -CdnEndpoint $endpoint -CustomDomainHostName "cdn.contoso.com"

# Create the custom domain on the endpoint
If($result.CustomDomainValidated){ New-AzureRmCdnCustomDomain -CustomDomainName Contoso -HostName "cdn.contoso.com" -CdnEndpoint $endpoint }
```

## <a name="modifying-an-endpoint"></a><span data-ttu-id="20b12-132">Modifica di un endpoint</span><span class="sxs-lookup"><span data-stu-id="20b12-132">Modifying an endpoint</span></span>
<span data-ttu-id="20b12-133">`Set-AzureRmCdnEndpoint` modifica un endpoint esistente.</span><span class="sxs-lookup"><span data-stu-id="20b12-133">`Set-AzureRmCdnEndpoint` modifies an existing endpoint.</span></span>

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save the changed endpoint and apply the changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a><span data-ttu-id="20b12-134">Ripulitura/Precaricamento degli asset della rete CDN</span><span class="sxs-lookup"><span data-stu-id="20b12-134">Purging/Pre-loading CDN assets</span></span>
<span data-ttu-id="20b12-135">`Unpublish-AzureRmCdnEndpointContent` ripulisce gli asset nella cache, mentre `Publish-AzureRmCdnEndpointContent` precarica gli asset negli endpoint supportati.</span><span class="sxs-lookup"><span data-stu-id="20b12-135">`Unpublish-AzureRmCdnEndpointContent` purges cached assets, while `Publish-AzureRmCdnEndpointContent` pre-loads assets on supported endpoints.</span></span>

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a><span data-ttu-id="20b12-136">Avvio/Arresto degli endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="20b12-136">Starting/Stopping CDN endpoints</span></span>
<span data-ttu-id="20b12-137">`Start-AzureRmCdnEndpoint` e `Stop-AzureRmCdnEndpoint` possono essere usati per avviare e arrestare singoli endpoint o gruppi di endpoint.</span><span class="sxs-lookup"><span data-stu-id="20b12-137">`Start-AzureRmCdnEndpoint` and `Stop-AzureRmCdnEndpoint` can be used to start and stop individual endpoints or groups of endpoints.</span></span>

```powershell
# Stop the cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a><span data-ttu-id="20b12-138">Eliminazione di risorse della rete CDN</span><span class="sxs-lookup"><span data-stu-id="20b12-138">Deleting CDN resources</span></span>
<span data-ttu-id="20b12-139">`Remove-AzureRmCdnProfile` e `Remove-AzureRmCdnEndpoint` possono essere usati per rimuovere profili ed endpoint.</span><span class="sxs-lookup"><span data-stu-id="20b12-139">`Remove-AzureRmCdnProfile` and `Remove-AzureRmCdnEndpoint` can be used to remove profiles and endpoints.</span></span>

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all the endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a><span data-ttu-id="20b12-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="20b12-140">Next Steps</span></span>
<span data-ttu-id="20b12-141">Informazioni su come automatizzare la rete CDN di Azure con [.NET](cdn-app-dev-net.md) o [Node.js](cdn-app-dev-node.md).</span><span class="sxs-lookup"><span data-stu-id="20b12-141">Learn how to automate Azure CDN with [.NET](cdn-app-dev-net.md) or [Node.js](cdn-app-dev-node.md).</span></span>

<span data-ttu-id="20b12-142">Per informazioni sulle funzionalità della rete CDN, vedere [Panoramica della rete per la distribuzione di contenuti (rete CDN) di Azure](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="20b12-142">To learn about CDN features, see [CDN Overview](cdn-overview.md).</span></span>

