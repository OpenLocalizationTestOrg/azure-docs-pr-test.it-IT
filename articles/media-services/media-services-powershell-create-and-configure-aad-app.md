---
title: Usare PowerShell per creare un'app Azure AD per l'accesso all'API Servizi multimediali di Azure | Microsoft Docs
description: Informazioni su come usare PowerShell per creare un'app Azure Active Directory (Azure AD) e configurarla per accedere all'API Servizi multimediali di Azure.
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
ms.openlocfilehash: eea0f3a03dd77ce56484f32b192299bd97c05300
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-powershell-to-create-an-azure-ad-app-to-use-with-the-azure-media-services-api"></a><span data-ttu-id="223e1-103">Usare PowerShell per creare un'app Azure AD da usare con l'API Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="223e1-103">Use PowerShell to create an Azure AD app to use with the Azure Media Services API</span></span>

<span data-ttu-id="223e1-104">Informazioni su come usare uno script di PowerShell per creare un'applicazione e un'entità servizio di Azure Active Directory (Azure AD) per accedere alle risorse di Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="223e1-104">Learn how to use a PowerShell script to create an Azure Active Directory (Azure AD) application and service principal to access Azure Media Services resources.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="223e1-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="223e1-105">Prerequisites</span></span>

- <span data-ttu-id="223e1-106">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="223e1-106">An Azure account.</span></span> <span data-ttu-id="223e1-107">Se non si dispone di un account, iniziare con una [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="223e1-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="223e1-108">Account di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="223e1-108">A Media Services account.</span></span> <span data-ttu-id="223e1-109">Per altre informazioni, vedere [Creare un account Servizi multimediali di Azure nel portale di Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="223e1-109">For more information, see [Create an Azure Media Services account in the Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="223e1-110">Azure PowerShell versione 0.8.8 o successiva.</span><span class="sxs-lookup"><span data-stu-id="223e1-110">Azure PowerShell version 0.8.8 or a later version.</span></span> <span data-ttu-id="223e1-111">Per altre informazioni, vedere [Come usare Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="223e1-111">For more information, see [How to use Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
- <span data-ttu-id="223e1-112">Cmdlet di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="223e1-112">Azure Resource Manager cmdlets.</span></span>  

## <a name="create-an-azure-ad-app-by-using-powershell"></a><span data-ttu-id="223e1-113">Creare un'app Azure AD usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="223e1-113">Create an Azure AD app by using PowerShell</span></span>  

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
    # Sleep here for a few seconds to allow the service principal application to become active (usually, it will take only a couple of seconds)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
}
```

<span data-ttu-id="223e1-114">Per altre informazioni, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="223e1-114">For more information, see the following articles:</span></span>

- [<span data-ttu-id="223e1-115">Usare Azure PowerShell per creare un'entità servizio per accedere alle risorse</span><span class="sxs-lookup"><span data-stu-id="223e1-115">Use Azure PowerShell to create a service principal to access resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [<span data-ttu-id="223e1-116">Gestire il controllo degli accessi in base al ruolo usando Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="223e1-116">Manage Role-Based Access Control by using Azure PowerShell</span></span>](../active-directory/role-based-access-control-manage-access-powershell.md)
- [<span data-ttu-id="223e1-117">Come configurare manualmente le app daemon usando i certificati</span><span class="sxs-lookup"><span data-stu-id="223e1-117">How to manually configure daemon apps by using certificates</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a><span data-ttu-id="223e1-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="223e1-118">Next steps</span></span>

<span data-ttu-id="223e1-119">Introduzione al [caricamento di file nell'account](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="223e1-119">Get started with [uploading files to your account](media-services-portal-upload-files.md).</span></span>
