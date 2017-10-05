---
title: Librerie di gestione di Hub eventi di Azure | Microsoft Docs
description: "Gestire entità e spazi dei nomi di Hub eventi da .NET"
services: event-hubs
cloud: na
documentationcenter: na
author: sethmanheim
manager: timlt
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 0d659cb860a6c98342b548212820efe046decfcc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-management-libraries"></a><span data-ttu-id="56024-103">Librerie di gestione di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="56024-103">Event Hubs management libraries</span></span>

<span data-ttu-id="56024-104">Le librerie di gestione di Hub eventi possono effettuare il provisioning di entità e spazi dei nomi di Hub eventi in modo dinamico,</span><span class="sxs-lookup"><span data-stu-id="56024-104">The Event Hubs management libraries can dynamically provision Event Hubs namespaces and entities.</span></span> <span data-ttu-id="56024-105">per consentire distribuzioni complesse e scenari di messaggistica e permettere di determinare a livello di codice le entità di cui effettuare il provisioning.</span><span class="sxs-lookup"><span data-stu-id="56024-105">This enables complex deployments and messaging scenarios, so that you can programmatically determine what entities to provision.</span></span> <span data-ttu-id="56024-106">Queste librerie sono attualmente disponibili per .NET.</span><span class="sxs-lookup"><span data-stu-id="56024-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="56024-107">Funzionalità supportate</span><span class="sxs-lookup"><span data-stu-id="56024-107">Supported functionality</span></span>

* <span data-ttu-id="56024-108">Creazione, aggiornamento, eliminazione di spazi dei nomi</span><span class="sxs-lookup"><span data-stu-id="56024-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="56024-109">Creazione, aggiornamento, eliminazione di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="56024-109">Event Hubs creation, update, deletion</span></span>
* <span data-ttu-id="56024-110">Creazione, aggiornamento, eliminazione di gruppi di consumer</span><span class="sxs-lookup"><span data-stu-id="56024-110">Consumer Group creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56024-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="56024-111">Prerequisites</span></span>

<span data-ttu-id="56024-112">Per iniziare a usare le librerie di gestione di Hub eventi, è necessario eseguire l'autenticazione con Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="56024-112">To get started using the Event Hubs management libraries, you must authenticate with Azure Active Directory (AAD).</span></span> <span data-ttu-id="56024-113">AAD richiede l'autenticazione come entità servizio, che fornisce l'accesso alle risorse di Azure in uso.</span><span class="sxs-lookup"><span data-stu-id="56024-113">AAD requires that you authenticate as a service principal, which provides access to your Azure resources.</span></span> <span data-ttu-id="56024-114">Per informazioni su come creare un'entità servizio, vedere uno di questi articoli:</span><span class="sxs-lookup"><span data-stu-id="56024-114">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="56024-115">Usare il portale di Azure per creare un'applicazione Active Directory e un'entità servizio che accedono alle risorse</span><span class="sxs-lookup"><span data-stu-id="56024-115">Use the Azure portal to create Active Directory application and service principal that can access resources</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="56024-116">Usare Azure PowerShell per creare un'entità servizio per accedere alle risorse</span><span class="sxs-lookup"><span data-stu-id="56024-116">Use Azure PowerShell to create a service principal to access resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="56024-117">Usare l'interfaccia della riga di comando di Azure per creare un'entità servizio per accedere alle risorse</span><span class="sxs-lookup"><span data-stu-id="56024-117">Use Azure CLI to create a service principal to access resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

<span data-ttu-id="56024-118">Nel corso di queste esercitazioni vengono forniti un `AppId` (ID client), un `TenantId` e un `ClientSecret` (chiave di autenticazione) che sono usati per l'autenticazione da parte delle librerie di gestione.</span><span class="sxs-lookup"><span data-stu-id="56024-118">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by the management libraries.</span></span> <span data-ttu-id="56024-119">È necessario avere autorizzazioni di **Proprietario** per il gruppo di risorse in cui verranno eseguite le librerie.</span><span class="sxs-lookup"><span data-stu-id="56024-119">You must have **Owner** permissions for the resource group on which you want to run.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="56024-120">Modello di programmazione</span><span class="sxs-lookup"><span data-stu-id="56024-120">Programming pattern</span></span>

<span data-ttu-id="56024-121">Il modello di modifica delle risorse di Hub eventi segue un protocollo comune:</span><span class="sxs-lookup"><span data-stu-id="56024-121">The pattern to manipulate any Event Hubs resource follows a common protocol:</span></span>

1. <span data-ttu-id="56024-122">Ottenere un token da AAD usando la libreria `Microsoft.IdentityModel.Clients.ActiveDirectory`.</span><span class="sxs-lookup"><span data-stu-id="56024-122">Obtain a token from AAD using the `Microsoft.IdentityModel.Clients.ActiveDirectory` library.</span></span>
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. <span data-ttu-id="56024-123">Creare l'oggetto `EventHubManagementClient`.</span><span class="sxs-lookup"><span data-stu-id="56024-123">Create the `EventHubManagementClient` object.</span></span>
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. <span data-ttu-id="56024-124">Impostare i parametri `CreateOrUpdate` sui valori specificati.</span><span class="sxs-lookup"><span data-stu-id="56024-124">Set the `CreateOrUpdate` parameters to your specified values.</span></span>
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. <span data-ttu-id="56024-125">Effettuare la chiamata.</span><span class="sxs-lookup"><span data-stu-id="56024-125">Execute the call.</span></span>
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a><span data-ttu-id="56024-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="56024-126">Next steps</span></span>
* [<span data-ttu-id="56024-127">Esempio di gestione .NET</span><span class="sxs-lookup"><span data-stu-id="56024-127">.NET Management sample</span></span>](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [<span data-ttu-id="56024-128">Riferimento di Microsoft.Azure.Management.EventHub</span><span class="sxs-lookup"><span data-stu-id="56024-128">Microsoft.Azure.Management.EventHub Reference</span></span>](/dotnet/api/Microsoft.Azure.Management.EventHub) 
