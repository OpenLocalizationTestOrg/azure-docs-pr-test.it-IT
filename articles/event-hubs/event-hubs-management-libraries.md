---
title: le raccolte di gestione degli hub di eventi aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: b7db0077f6f31397ae46e926c3c28630a157824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-management-libraries"></a><span data-ttu-id="90347-103">Librerie di gestione di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="90347-103">Event Hubs management libraries</span></span>

<span data-ttu-id="90347-104">le raccolte di gestione degli hub di eventi Hello possano il provisioning dinamico di entità e spazi dei nomi di hub eventi.</span><span class="sxs-lookup"><span data-stu-id="90347-104">hello Event Hubs management libraries can dynamically provision Event Hubs namespaces and entities.</span></span> <span data-ttu-id="90347-105">In questo modo eseguire distribuzioni complesse e scenari di messaggistica, in modo che è possibile determinare a livello di programmazione quali tooprovision di entità.</span><span class="sxs-lookup"><span data-stu-id="90347-105">This enables complex deployments and messaging scenarios, so that you can programmatically determine what entities tooprovision.</span></span> <span data-ttu-id="90347-106">Queste librerie sono attualmente disponibili per .NET.</span><span class="sxs-lookup"><span data-stu-id="90347-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="90347-107">Funzionalità supportate</span><span class="sxs-lookup"><span data-stu-id="90347-107">Supported functionality</span></span>

* <span data-ttu-id="90347-108">Creazione, aggiornamento, eliminazione di spazi dei nomi</span><span class="sxs-lookup"><span data-stu-id="90347-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="90347-109">Creazione, aggiornamento, eliminazione di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="90347-109">Event Hubs creation, update, deletion</span></span>
* <span data-ttu-id="90347-110">Creazione, aggiornamento, eliminazione di gruppi di consumer</span><span class="sxs-lookup"><span data-stu-id="90347-110">Consumer Group creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90347-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="90347-111">Prerequisites</span></span>

<span data-ttu-id="90347-112">tooget avviato utilizzando le raccolte di gestione di hello hub eventi, è necessario eseguire l'autenticazione con Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="90347-112">tooget started using hello Event Hubs management libraries, you must authenticate with Azure Active Directory (AAD).</span></span> <span data-ttu-id="90347-113">AAD, è necessario eseguire l'autenticazione come un'entità servizio, che fornisce accesso tooyour risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="90347-113">AAD requires that you authenticate as a service principal, which provides access tooyour Azure resources.</span></span> <span data-ttu-id="90347-114">Per informazioni su come creare un'entità servizio, vedere uno di questi articoli:</span><span class="sxs-lookup"><span data-stu-id="90347-114">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="90347-115">Utilizzare un'applicazione hello toocreate portale di Azure Active Directory e dell'entità servizio che possono accedere alle risorse</span><span class="sxs-lookup"><span data-stu-id="90347-115">Use hello Azure portal toocreate Active Directory application and service principal that can access resources</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="90347-116">Usare Azure PowerShell toocreate una risorse tooaccess dell'entità servizio</span><span class="sxs-lookup"><span data-stu-id="90347-116">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="90347-117">Utilizzare toocreate CLI di Azure un risorse tooaccess dell'entità servizio</span><span class="sxs-lookup"><span data-stu-id="90347-117">Use Azure CLI toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

<span data-ttu-id="90347-118">Queste esercitazioni forniscono un `AppId` (ID Client), `TenantId`, e `ClientSecret` (chiave di autenticazione), ognuno dei quali vengono utilizzati per l'autenticazione per le raccolte di gestione di hello.</span><span class="sxs-lookup"><span data-stu-id="90347-118">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by hello management libraries.</span></span> <span data-ttu-id="90347-119">È necessario disporre di **proprietario** le autorizzazioni per il gruppo di risorse hello in cui si desidera toorun.</span><span class="sxs-lookup"><span data-stu-id="90347-119">You must have **Owner** permissions for hello resource group on which you want toorun.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="90347-120">Modello di programmazione</span><span class="sxs-lookup"><span data-stu-id="90347-120">Programming pattern</span></span>

<span data-ttu-id="90347-121">Hello modello toomanipulate qualsiasi risorsa di hub eventi segue un protocollo comune:</span><span class="sxs-lookup"><span data-stu-id="90347-121">hello pattern toomanipulate any Event Hubs resource follows a common protocol:</span></span>

1. <span data-ttu-id="90347-122">Ottenere un token da Azure Active Directory utilizzando hello `Microsoft.IdentityModel.Clients.ActiveDirectory` libreria.</span><span class="sxs-lookup"><span data-stu-id="90347-122">Obtain a token from AAD using hello `Microsoft.IdentityModel.Clients.ActiveDirectory` library.</span></span>
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. <span data-ttu-id="90347-123">Creare hello `EventHubManagementClient` oggetto.</span><span class="sxs-lookup"><span data-stu-id="90347-123">Create hello `EventHubManagementClient` object.</span></span>
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. <span data-ttu-id="90347-124">Set hello `CreateOrUpdate` tooyour i parametri specificati.</span><span class="sxs-lookup"><span data-stu-id="90347-124">Set hello `CreateOrUpdate` parameters tooyour specified values.</span></span>
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. <span data-ttu-id="90347-125">Chiamare hello Execute.</span><span class="sxs-lookup"><span data-stu-id="90347-125">Execute hello call.</span></span>
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a><span data-ttu-id="90347-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="90347-126">Next steps</span></span>
* [<span data-ttu-id="90347-127">Esempio di gestione .NET</span><span class="sxs-lookup"><span data-stu-id="90347-127">.NET Management sample</span></span>](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [<span data-ttu-id="90347-128">Riferimento di Microsoft.Azure.Management.EventHub</span><span class="sxs-lookup"><span data-stu-id="90347-128">Microsoft.Azure.Management.EventHub Reference</span></span>](/dotnet/api/Microsoft.Azure.Management.EventHub) 
