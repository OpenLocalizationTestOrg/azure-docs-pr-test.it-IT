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
# <a name="use-powershell-toocreate-an-azure-ad-app-toouse-with-hello-azure-media-services-api"></a><span data-ttu-id="e0058-103">Utilizzare PowerShell toocreate un toouse di app di Azure AD con hello API di servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="e0058-103">Use PowerShell toocreate an Azure AD app toouse with hello Azure Media Services API</span></span>

<span data-ttu-id="e0058-104">Informazioni su come toouse un PowerShell toocreate un'applicazione Azure Active Directory (Azure AD) e script tooaccess dell'entità servizio risorse di servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="e0058-104">Learn how toouse a PowerShell script toocreate an Azure Active Directory (Azure AD) application and service principal tooaccess Azure Media Services resources.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="e0058-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e0058-105">Prerequisites</span></span>

- <span data-ttu-id="e0058-106">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="e0058-106">An Azure account.</span></span> <span data-ttu-id="e0058-107">Se non si dispone di un account, iniziare con una [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e0058-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="e0058-108">Account di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="e0058-108">A Media Services account.</span></span> <span data-ttu-id="e0058-109">Per ulteriori informazioni, vedere [creare un account di servizi multimediali di Azure nel portale di Azure hello](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="e0058-109">For more information, see [Create an Azure Media Services account in hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="e0058-110">Azure PowerShell versione 0.8.8 o successiva.</span><span class="sxs-lookup"><span data-stu-id="e0058-110">Azure PowerShell version 0.8.8 or a later version.</span></span> <span data-ttu-id="e0058-111">Per ulteriori informazioni, vedere [come toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e0058-111">For more information, see [How toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
- <span data-ttu-id="e0058-112">Cmdlet di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e0058-112">Azure Resource Manager cmdlets.</span></span>  

## <a name="create-an-azure-ad-app-by-using-powershell"></a><span data-ttu-id="e0058-113">Creare un'app Azure AD usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0058-113">Create an Azure AD app by using PowerShell</span></span>  

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

<span data-ttu-id="e0058-114">Per ulteriori informazioni, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="e0058-114">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="e0058-115">Usare Azure PowerShell toocreate una risorse tooaccess dell'entità servizio</span><span class="sxs-lookup"><span data-stu-id="e0058-115">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [<span data-ttu-id="e0058-116">Gestire il controllo degli accessi in base al ruolo usando Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0058-116">Manage Role-Based Access Control by using Azure PowerShell</span></span>](../active-directory/role-based-access-control-manage-access-powershell.md)
- [<span data-ttu-id="e0058-117">Configurazione toomanually daemon App usando i certificati</span><span class="sxs-lookup"><span data-stu-id="e0058-117">How toomanually configure daemon apps by using certificates</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a><span data-ttu-id="e0058-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e0058-118">Next steps</span></span>

<span data-ttu-id="e0058-119">Introduzione a [caricamento file account tooyour](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="e0058-119">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
