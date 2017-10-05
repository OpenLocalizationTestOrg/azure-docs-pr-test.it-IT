---
title: Ottenere valori per l'autenticazione delle app - Database SQL di Azure | Microsoft Docs
description: "Creare un'entità servizio per l'accesso al database SQL dal codice."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
tags: 
ms.assetid: b43e43bb-6660-49e6-b069-abde97eb5770
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 09/30/2016
ms.author: sstein
ms.openlocfilehash: ec6256e9c5bb0d9c8d15d0f673cea70b3915eb34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-required-values-for-authenticating-an-application-to-access-sql-database-from-code"></a><span data-ttu-id="30fc2-103">Ottenere i valori richiesti per l'autenticazione di un'applicazione per l'accesso al database SQL dal codice</span><span class="sxs-lookup"><span data-stu-id="30fc2-103">Get the required values for authenticating an application to access SQL Database from code</span></span>
<span data-ttu-id="30fc2-104">Per creare e gestire database SQL dal codice è necessario registrare l'app nel dominio di Azure Active Directory (AAD) nella sottoscrizione in cui sono state create le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="30fc2-104">To create and manage SQL Database from code you must register your app in the Azure Active Directory (AAD) domain  in the subscription where your Azure resources have been created.</span></span>

## <a name="create-a-service-principal-to-access-resources-from-an-application"></a><span data-ttu-id="30fc2-105">Creare un'entità servizio per accedere alle risorse da un'applicazione</span><span class="sxs-lookup"><span data-stu-id="30fc2-105">Create a service principal to access resources from an application</span></span>
<span data-ttu-id="30fc2-106">È necessario che sia installata ed eseguita la versione più recente di [Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx).</span><span class="sxs-lookup"><span data-stu-id="30fc2-106">You need to have the latest [Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx) installed and running.</span></span> <span data-ttu-id="30fc2-107">Per informazioni dettagliate, vedere [Come installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="30fc2-107">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

<span data-ttu-id="30fc2-108">Lo script di PowerShell seguente permette di creare l'applicazione Active Directory (AD) e l'entità servizio necessarie per autenticare l'app C#.</span><span class="sxs-lookup"><span data-stu-id="30fc2-108">The following PowerShell script creates the Active Directory (AD) application and the service principal that we need to authenticate our C# app.</span></span> <span data-ttu-id="30fc2-109">Lo script restituisce i valori necessari per l'esempio di C# precedente.</span><span class="sxs-lookup"><span data-stu-id="30fc2-109">The script outputs values we need for the preceding C# sample.</span></span> <span data-ttu-id="30fc2-110">Per informazioni dettagliate, vedere [Usare Azure PowerShell per creare un'entità servizio per accedere alle risorse](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="30fc2-110">For detailed information, see [Use Azure PowerShell to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    # Sign in to Azure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set to the subscription you want to work with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is the display name for your app, must be unique in your directory.
    # $uri does not need to be a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for the app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # To avoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun the following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output the values we need for our C# application to successfully authenticate

    Write-Output "Copy these values into the C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret




## <a name="see-also"></a><span data-ttu-id="30fc2-111">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="30fc2-111">See also</span></span>
* [<span data-ttu-id="30fc2-112">Usare C# per creare un database SQL</span><span class="sxs-lookup"><span data-stu-id="30fc2-112">Create a SQL database with C#</span></span>](sql-database-get-started-csharp.md)
* [<span data-ttu-id="30fc2-113">Connettersi al Database SQL utilizzando l’autenticazione di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="30fc2-113">Connecting to SQL Database By Using Azure Active Directory Authentication</span></span>](sql-database-aad-authentication.md)

