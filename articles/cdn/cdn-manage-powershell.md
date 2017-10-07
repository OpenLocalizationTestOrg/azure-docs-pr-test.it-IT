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
# <a name="manage-azure-cdn-with-powershell"></a>Gestire la rete CDN di Azure con PowerShell
PowerShell fornisce uno dei toomanage metodi più flessibile hello i profili di rete CDN di Azure e l'endpoint.  È possibile utilizzare PowerShell in modo interattivo o scrivendo script tooautomate attività di gestione.  In questa esercitazione vengono illustrate diverse di attività più comuni di hello è possibile eseguire con PowerShell toomanage i profili di rete CDN di Azure e l'endpoint.

## <a name="prerequisites"></a>Prerequisiti
toouse PowerShell toomanage i profili di rete CDN di Azure e un endpoint, è necessario che il modulo di Azure PowerShell hello installato.  toolearn come tooinstall Azure PowerShell e connettersi usando hello tooAzure `Login-AzureRmAccount` cmdlet, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

> [!IMPORTANT]
> È necessario accedere con `Login-AzureRmAccount` per poter eseguire i cmdlet di Azure PowerShell.
> 
> 

## <a name="listing-hello-azure-cdn-cmdlets"></a>Elenca i cmdlet di hello rete CDN di Azure
È possibile elencare tutti i cmdlet di Azure CDN hello utilizzando hello `Get-Command` cmdlet.

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

## <a name="getting-help"></a>Risorse della Guida
È possibile ottenere assistenza con uno qualsiasi di questi cmdlet utilizzando hello `Get-Help` cmdlet.  `Get-Help` fornisce la sintassi e facoltativamente illustra gli esempi.

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

## <a name="listing-existing-azure-cdn-profiles"></a>Inclusione in elenco dei profili della rete CDN di Azure esistenti
Hello `Get-AzureRmCdnProfile` cmdlet senza parametri consente di recuperare tutti i profili di rete CDN esistenti.

```powershell
Get-AzureRmCdnProfile
```

Questo output può essere reindirizzato toocmdlets per l'enumerazione.

```powershell
# Output hello name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

È inoltre possibile restituire un unico profilo specificando nome e la risorsa gruppo di profili di hello.

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> È possibile toohave CDN più profili con hello stesso nome, purché si trovano in gruppi di risorse diverso.  L'omissione di hello `ResourceGroupName` parametro restituisce tutti i profili con un nome corrispondente.
> 
> 

## <a name="listing-existing-cdn-endpoints"></a>Inclusione in elenco degli endpoint della rete CDN esistenti
`Get-AzureRmCdnEndpoint`recuperare tutti gli endpoint hello in un profilo o un singolo endpoint.  

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

## <a name="creating-cdn-profiles-and-endpoints"></a>Creazione dei profili e degli endpoint della rete CDN
`New-AzureRmCdnProfile`e `New-AzureRmCdnEndpoint` sono i profili di rete CDN toocreate utilizzato e gli endpoint.

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a>Controllo della disponibilità del nome dell'endpoint
`Get-AzureRmCdnEndpointNameAvailability` restituisce un oggetto indicante se un nome di endpoint è disponibile.

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message toohello console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a>Aggiunta di un dominio personalizzato
`New-AzureRmCdnCustomDomain`Aggiunge un endpoint della tooan nome dominio personalizzato esistente.

> [!IMPORTANT]
> È necessario impostare hello CNAME con il provider DNS come descritto in [come endpoint di rete (CDN) di toomap dominio personalizzato tooContent](cdn-map-content-to-custom-domain.md).  È possibile verificare il mapping di hello prima di modificare l'endpoint utilizzando `Test-AzureRmCdnCustomDomain`.
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

## <a name="modifying-an-endpoint"></a>Modifica di un endpoint
`Set-AzureRmCdnEndpoint` modifica un endpoint esistente.

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save hello changed endpoint and apply hello changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a>Ripulitura/Precaricamento degli asset della rete CDN
`Unpublish-AzureRmCdnEndpointContent` ripulisce gli asset nella cache, mentre `Publish-AzureRmCdnEndpointContent` precarica gli asset negli endpoint supportati.

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a>Avvio/Arresto degli endpoint della rete CDN
`Start-AzureRmCdnEndpoint`e `Stop-AzureRmCdnEndpoint` possibile toostart utilizzato e arresta l'endpoint singoli o gruppi di endpoint.

```powershell
# Stop hello cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a>Eliminazione di risorse della rete CDN
`Remove-AzureRmCdnProfile`e `Remove-AzureRmCdnEndpoint` possono essere utilizzati tooremove profili e gli endpoint.

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all hello endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a>Passaggi successivi
Informazioni su come tooautomate rete CDN di Azure con [.NET](cdn-app-dev-net.md) o [Node.js](cdn-app-dev-node.md).

toolearn sulle funzionalità di rete CDN, vedere [Panoramica della rete CDN](cdn-overview.md).

