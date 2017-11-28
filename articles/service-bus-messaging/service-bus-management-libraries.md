---
title: le raccolte di gestione di Service Bus aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: 9e4ad91f22815ca0838e6e4647a3606109b2b441
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-management-libraries"></a><span data-ttu-id="2c0cb-103">Librerie di gestione del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="2c0cb-103">Service Bus management libraries</span></span>

<span data-ttu-id="2c0cb-104">le raccolte di gestione di Azure Service Bus Hello possano il provisioning dinamico di entità e spazi dei nomi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-104">hello Azure Service Bus management libraries can dynamically provision Service Bus namespaces and entities.</span></span> <span data-ttu-id="2c0cb-105">Ciò consente di eseguire distribuzioni complesse e scenari di messaggistica e rende possibile tooprogrammatically determinare quali tooprovision di entità.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-105">This enables complex deployments and messaging scenarios, and makes it possible tooprogrammatically determine what entities tooprovision.</span></span> <span data-ttu-id="2c0cb-106">Queste librerie sono attualmente disponibili per .NET.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="2c0cb-107">Funzionalità supportate</span><span class="sxs-lookup"><span data-stu-id="2c0cb-107">Supported functionality</span></span>

* <span data-ttu-id="2c0cb-108">Creazione, aggiornamento, eliminazione di spazi dei nomi</span><span class="sxs-lookup"><span data-stu-id="2c0cb-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="2c0cb-109">Creazione, aggiornamento, eliminazione di code</span><span class="sxs-lookup"><span data-stu-id="2c0cb-109">Queue creation, update, deletion</span></span>
* <span data-ttu-id="2c0cb-110">Creazione, aggiornamento, eliminazione di argomenti</span><span class="sxs-lookup"><span data-stu-id="2c0cb-110">Topic creation, update, deletion</span></span>
* <span data-ttu-id="2c0cb-111">Creazione, aggiornamento, eliminazione di sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="2c0cb-111">Subscription creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c0cb-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2c0cb-112">Prerequisites</span></span>

<span data-ttu-id="2c0cb-113">tooget avviato utilizzando le raccolte di gestione di Service Bus hello, è necessario autenticare con hello servizio Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="2c0cb-113">tooget started using hello Service Bus management libraries, you must authenticate with hello Azure Active Directory (AAD) service.</span></span> <span data-ttu-id="2c0cb-114">AAD, è necessario eseguire l'autenticazione come un'entità servizio, che fornisce accesso tooyour risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-114">AAD requires that you authenticate as a service principal, which provides access tooyour Azure resources.</span></span> <span data-ttu-id="2c0cb-115">Per informazioni su come creare un'entità servizio, vedere uno di questi articoli:</span><span class="sxs-lookup"><span data-stu-id="2c0cb-115">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="2c0cb-116">Utilizzare un'applicazione hello toocreate portale di Azure Active Directory e dell'entità servizio che possono accedere alle risorse</span><span class="sxs-lookup"><span data-stu-id="2c0cb-116">Use hello Azure portal toocreate Active Directory application and service principal that can access resources</span></span>](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [<span data-ttu-id="2c0cb-117">Usare Azure PowerShell toocreate una risorse tooaccess dell'entità servizio</span><span class="sxs-lookup"><span data-stu-id="2c0cb-117">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="2c0cb-118">Utilizzare toocreate CLI di Azure un risorse tooaccess dell'entità servizio</span><span class="sxs-lookup"><span data-stu-id="2c0cb-118">Use Azure CLI toocreate a service principal tooaccess resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

<span data-ttu-id="2c0cb-119">Queste esercitazioni forniscono un `AppId` (ID Client), `TenantId`, e `ClientSecret` (chiave di autenticazione), ognuno dei quali vengono utilizzati per l'autenticazione per le raccolte di gestione di hello.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-119">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by hello management libraries.</span></span> <span data-ttu-id="2c0cb-120">È necessario disporre di **proprietario** le autorizzazioni per il gruppo di risorse hello in cui si desidera toorun.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-120">You must have **Owner** permissions for hello resource group on which you wish toorun.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="2c0cb-121">Modello di programmazione</span><span class="sxs-lookup"><span data-stu-id="2c0cb-121">Programming pattern</span></span>

<span data-ttu-id="2c0cb-122">Hello modello toomanipulate qualsiasi risorsa Bus di servizio segue un protocollo comune:</span><span class="sxs-lookup"><span data-stu-id="2c0cb-122">hello pattern toomanipulate any Service Bus resource follows a common protocol:</span></span>

1. <span data-ttu-id="2c0cb-123">Ottenere un token da Azure Active Directory tramite hello **ActiveDirectory** libreria.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-123">Obtain a token from Azure Active Directory using hello **Microsoft.IdentityModel.Clients.ActiveDirectory** library.</span></span>
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. <span data-ttu-id="2c0cb-124">Creare hello `ServiceBusManagementClient` oggetto.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-124">Create hello `ServiceBusManagementClient` object.</span></span>

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. <span data-ttu-id="2c0cb-125">Set hello `CreateOrUpdate` tooyour i parametri specificati.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-125">Set hello `CreateOrUpdate` parameters tooyour specified values.</span></span>

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. <span data-ttu-id="2c0cb-126">Chiamare hello Execute.</span><span class="sxs-lookup"><span data-stu-id="2c0cb-126">Execute hello call.</span></span>

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a><span data-ttu-id="2c0cb-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2c0cb-127">Next steps</span></span>
* [<span data-ttu-id="2c0cb-128">Esempio di gestione .NET</span><span class="sxs-lookup"><span data-stu-id="2c0cb-128">.NET management sample</span></span>](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [<span data-ttu-id="2c0cb-129">Informazioni di riferimento sull'API Microsoft.Azure.Management.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="2c0cb-129">Microsoft.Azure.Management.ServiceBus API reference</span></span>](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
