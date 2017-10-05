---
title: Librerie di gestione del bus di servizio di Azure | Microsoft Docs
description: "Gestire entità di messaggistica e spazi dei nomi del bus di servizio da .NET."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: 1db00dc1f91e8976b622030450445babbe547ad8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="service-bus-management-libraries"></a><span data-ttu-id="5f3d8-103">Librerie di gestione del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="5f3d8-103">Service Bus management libraries</span></span>

<span data-ttu-id="5f3d8-104">Le librerie di gestione del bus di servizio di Azure possono eseguire il provisioning di entità e spazi dei nomi del bus di servizio in modo dinamico,</span><span class="sxs-lookup"><span data-stu-id="5f3d8-104">The Azure Service Bus management libraries can dynamically provision Service Bus namespaces and entities.</span></span> <span data-ttu-id="5f3d8-105">per consentire distribuzioni complesse e scenari di messaggistica e permettere di determinare a livello di codice le entità di cui eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="5f3d8-105">This enables complex deployments and messaging scenarios, and makes it possible to programmatically determine what entities to provision.</span></span> <span data-ttu-id="5f3d8-106">Queste librerie sono attualmente disponibili per .NET.</span><span class="sxs-lookup"><span data-stu-id="5f3d8-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="5f3d8-107">Funzionalità supportate</span><span class="sxs-lookup"><span data-stu-id="5f3d8-107">Supported functionality</span></span>

* <span data-ttu-id="5f3d8-108">Creazione, aggiornamento, eliminazione di spazi dei nomi</span><span class="sxs-lookup"><span data-stu-id="5f3d8-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="5f3d8-109">Creazione, aggiornamento, eliminazione di code</span><span class="sxs-lookup"><span data-stu-id="5f3d8-109">Queue creation, update, deletion</span></span>
* <span data-ttu-id="5f3d8-110">Creazione, aggiornamento, eliminazione di argomenti</span><span class="sxs-lookup"><span data-stu-id="5f3d8-110">Topic creation, update, deletion</span></span>
* <span data-ttu-id="5f3d8-111">Creazione, aggiornamento, eliminazione di sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="5f3d8-111">Subscription creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f3d8-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5f3d8-112">Prerequisites</span></span>

<span data-ttu-id="5f3d8-113">Per iniziare a usare le librerie di gestione del bus di servizio, è necessario eseguire l'autenticazione con il servizio Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="5f3d8-113">To get started using the Service Bus management libraries, you must authenticate with the Azure Active Directory (AAD) service.</span></span> <span data-ttu-id="5f3d8-114">AAD richiede l'autenticazione come entità servizio, che fornisce l'accesso alle risorse di Azure in uso.</span><span class="sxs-lookup"><span data-stu-id="5f3d8-114">AAD requires that you authenticate as a service principal, which provides access to your Azure resources.</span></span> <span data-ttu-id="5f3d8-115">Per informazioni su come creare un'entità servizio, vedere uno di questi articoli:</span><span class="sxs-lookup"><span data-stu-id="5f3d8-115">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="5f3d8-116">Usare il portale di Azure per creare un'applicazione Active Directory e un'entità servizio che accedono alle risorse</span><span class="sxs-lookup"><span data-stu-id="5f3d8-116">Use the Azure portal to create Active Directory application and service principal that can access resources</span></span>](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [<span data-ttu-id="5f3d8-117">Usare Azure PowerShell per creare un'entità servizio per accedere alle risorse</span><span class="sxs-lookup"><span data-stu-id="5f3d8-117">Use Azure PowerShell to create a service principal to access resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="5f3d8-118">Usare l'interfaccia della riga di comando di Azure per creare un'entità servizio per accedere alle risorse</span><span class="sxs-lookup"><span data-stu-id="5f3d8-118">Use Azure CLI to create a service principal to access resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

<span data-ttu-id="5f3d8-119">Nel corso di queste esercitazioni vengono forniti un `AppId` (ID client), un `TenantId` e un `ClientSecret` (chiave di autenticazione) che sono usati per l'autenticazione da parte delle librerie di gestione.</span><span class="sxs-lookup"><span data-stu-id="5f3d8-119">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by the management libraries.</span></span> <span data-ttu-id="5f3d8-120">È necessario disporre delle autorizzazioni di **Proprietario** per il gruppo di risorse in cui verranno eseguite le librerie.</span><span class="sxs-lookup"><span data-stu-id="5f3d8-120">You must have **Owner** permissions for the resource group on which you wish to run.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="5f3d8-121">Modello di programmazione</span><span class="sxs-lookup"><span data-stu-id="5f3d8-121">Programming pattern</span></span>

<span data-ttu-id="5f3d8-122">Il modello di modifica delle risorse del bus di servizio segue un protocollo comune:</span><span class="sxs-lookup"><span data-stu-id="5f3d8-122">The pattern to manipulate any Service Bus resource follows a common protocol:</span></span>

1. <span data-ttu-id="5f3d8-123">Ottenere un token da Azure Active Directory usando la libreria **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="5f3d8-123">Obtain a token from Azure Active Directory using the **Microsoft.IdentityModel.Clients.ActiveDirectory** library.</span></span>
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. <span data-ttu-id="5f3d8-124">Creare l'oggetto `ServiceBusManagementClient`.</span><span class="sxs-lookup"><span data-stu-id="5f3d8-124">Create the `ServiceBusManagementClient` object.</span></span>

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. <span data-ttu-id="5f3d8-125">Impostare i parametri `CreateOrUpdate` sui valori specificati.</span><span class="sxs-lookup"><span data-stu-id="5f3d8-125">Set the `CreateOrUpdate` parameters to your specified values.</span></span>

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. <span data-ttu-id="5f3d8-126">Effettuare la chiamata.</span><span class="sxs-lookup"><span data-stu-id="5f3d8-126">Execute the call.</span></span>

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a><span data-ttu-id="5f3d8-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5f3d8-127">Next steps</span></span>
* [<span data-ttu-id="5f3d8-128">Esempio di gestione .NET</span><span class="sxs-lookup"><span data-stu-id="5f3d8-128">.NET management sample</span></span>](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [<span data-ttu-id="5f3d8-129">Informazioni di riferimento sull'API Microsoft.Azure.Management.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="5f3d8-129">Microsoft.Azure.Management.ServiceBus API reference</span></span>](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
