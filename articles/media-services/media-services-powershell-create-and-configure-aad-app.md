---
title: API di servizi multimediali di Azure di hello aaaUse PowerShell toocreate un tooaccess di app di Azure AD | Documenti Microsoft
description: Informazioni su come toouse PowerShell toocreate un'app di Azure Active Directory (Azure AD) e configurarlo tooaccess hello API di servizi multimediali di Azure.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 1a8b4a53ad10b559f6ee4242b95c5bd15ee8e903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-ad-app-toouse-with-hello-azure-media-services-api"></a>Utilizzare PowerShell toocreate un toouse di app di Azure AD con hello API di servizi multimediali di Azure

Informazioni su come toouse un PowerShell toocreate un'applicazione Azure Active Directory (Azure AD) e script tooaccess dell'entità servizio risorse di servizi multimediali di Azure.  

## <a name="prerequisites"></a>Prerequisiti

- Un account Azure. Se non si dispone di un account, iniziare con una [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/). 
- Account di Servizi multimediali. Per ulteriori informazioni, vedere [creare un account di servizi multimediali di Azure nel portale di Azure hello](media-services-portal-create-account.md).
- Azure PowerShell versione 0.8.8 o successiva. Per ulteriori informazioni, vedere [come toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).
- Cmdlet di Azure Resource Manager  

## <a name="create-an-azure-ad-app-by-using-powershell"></a>Creare un'app Azure AD usando PowerShell  

```powershell
Login-AzureRmAccount
Import-Module AzureRM.Resources
Set-AzureRmContext -SubscriptionId $SubscriptionId
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password

Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 
$NewRole = $null
$Scope = "/subscriptions/your subscription id/resourceGroups/userresourcegroup/providers/microsoft.media/mediaservices/your media account"

$Retries = 0;While ($NewRole -eq $null -and $Retries -le 6)
{
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (usually, it will take only a couple of seconds)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
}
```

Per ulteriori informazioni, vedere hello seguenti articoli:

- [Usare Azure PowerShell toocreate una risorse tooaccess dell'entità servizio](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [Gestire il controllo degli accessi in base al ruolo usando Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
- [Configurazione toomanually daemon App usando i certificati](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a>Passaggi successivi

Introduzione a [caricamento file account tooyour](media-services-portal-upload-files.md).
