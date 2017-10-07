---
title: i valori aaaGet per l'autenticazione dell'app - Database SQL di Azure | Documenti Microsoft
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
ms.openlocfilehash: b57dc075ec9e679da9f2f5fa53e02312539cdf07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-required-values-for-authenticating-an-application-tooaccess-sql-database-from-code"></a><span data-ttu-id="34f07-103">Ottenere i valori hello necessario per l'autenticazione di un Database SQL di tooaccess applicazione dal codice</span><span class="sxs-lookup"><span data-stu-id="34f07-103">Get hello required values for authenticating an application tooaccess SQL Database from code</span></span>
<span data-ttu-id="34f07-104">toocreate e gestire Database SQL dal codice, è necessario registrare l'app nel dominio di nella sottoscrizione hello hello Azure Active Directory (AAD) in cui sono state create le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="34f07-104">toocreate and manage SQL Database from code you must register your app in hello Azure Active Directory (AAD) domain  in hello subscription where your Azure resources have been created.</span></span>

## <a name="create-a-service-principal-tooaccess-resources-from-an-application"></a><span data-ttu-id="34f07-105">Creare un tooaccess dell'entità servizio, le risorse da un'applicazione</span><span class="sxs-lookup"><span data-stu-id="34f07-105">Create a service principal tooaccess resources from an application</span></span>
<span data-ttu-id="34f07-106">È necessario più recente hello toohave [Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx) installato e in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="34f07-106">You need toohave hello latest [Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx) installed and running.</span></span> <span data-ttu-id="34f07-107">Per informazioni dettagliate, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="34f07-107">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

<span data-ttu-id="34f07-108">Hello script PowerShell seguente crea un'applicazione hello Active Directory (AD) e il servizio hello principale che è necessario tooauthenticate applicazione c#.</span><span class="sxs-lookup"><span data-stu-id="34f07-108">hello following PowerShell script creates hello Active Directory (AD) application and hello service principal that we need tooauthenticate our C# app.</span></span> <span data-ttu-id="34f07-109">script Hello restituisce valori che è base per hello precedente c# di esempio.</span><span class="sxs-lookup"><span data-stu-id="34f07-109">hello script outputs values we need for hello preceding C# sample.</span></span> <span data-ttu-id="34f07-110">Per informazioni dettagliate, vedere [toocreate usare Azure PowerShell un'entità servizio tooaccess risorse](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="34f07-110">For detailed information, see [Use Azure PowerShell toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    # Sign in tooAzure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set toohello subscription you want toowork with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is hello display name for your app, must be unique in your directory.
    # $uri does not need toobe a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for hello app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # tooavoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun hello following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output hello values we need for our C# application toosuccessfully authenticate

    Write-Output "Copy these values into hello C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret




## <a name="see-also"></a><span data-ttu-id="34f07-111">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="34f07-111">See also</span></span>
* [<span data-ttu-id="34f07-112">Usare C# per creare un database SQL</span><span class="sxs-lookup"><span data-stu-id="34f07-112">Create a SQL database with C#</span></span>](sql-database-get-started-csharp.md)
* [<span data-ttu-id="34f07-113">Connessione tooSQL Database usando Azure Active Directory l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="34f07-113">Connecting tooSQL Database By Using Azure Active Directory Authentication</span></span>](sql-database-aad-authentication.md)

