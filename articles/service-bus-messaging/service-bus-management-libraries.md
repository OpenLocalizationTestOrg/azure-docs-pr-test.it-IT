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
# <a name="service-bus-management-libraries"></a>Librerie di gestione del bus di servizio

le raccolte di gestione di Azure Service Bus Hello possano il provisioning dinamico di entità e spazi dei nomi Service Bus. Ciò consente di eseguire distribuzioni complesse e scenari di messaggistica e rende possibile tooprogrammatically determinare quali tooprovision di entità. Queste librerie sono attualmente disponibili per .NET.

## <a name="supported-functionality"></a>Funzionalità supportate

* Creazione, aggiornamento, eliminazione di spazi dei nomi
* Creazione, aggiornamento, eliminazione di code
* Creazione, aggiornamento, eliminazione di argomenti
* Creazione, aggiornamento, eliminazione di sottoscrizioni

## <a name="prerequisites"></a>Prerequisiti

tooget avviato utilizzando le raccolte di gestione di Service Bus hello, è necessario autenticare con hello servizio Azure Active Directory (AAD). AAD, è necessario eseguire l'autenticazione come un'entità servizio, che fornisce accesso tooyour risorse di Azure. Per informazioni su come creare un'entità servizio, vedere uno di questi articoli:  

* [Utilizzare un'applicazione hello toocreate portale di Azure Active Directory e dell'entità servizio che possono accedere alle risorse](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [Usare Azure PowerShell toocreate una risorse tooaccess dell'entità servizio](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Utilizzare toocreate CLI di Azure un risorse tooaccess dell'entità servizio](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

Queste esercitazioni forniscono un `AppId` (ID Client), `TenantId`, e `ClientSecret` (chiave di autenticazione), ognuno dei quali vengono utilizzati per l'autenticazione per le raccolte di gestione di hello. È necessario disporre di **proprietario** le autorizzazioni per il gruppo di risorse hello in cui si desidera toorun.

## <a name="programming-pattern"></a>Modello di programmazione

Hello modello toomanipulate qualsiasi risorsa Bus di servizio segue un protocollo comune:

1. Ottenere un token da Azure Active Directory tramite hello **ActiveDirectory** libreria.
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. Creare hello `ServiceBusManagementClient` oggetto.

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. Set hello `CreateOrUpdate` tooyour i parametri specificati.

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. Chiamare hello Execute.

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a>Passaggi successivi
* [Esempio di gestione .NET](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [Informazioni di riferimento sull'API Microsoft.Azure.Management.ServiceBus](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
