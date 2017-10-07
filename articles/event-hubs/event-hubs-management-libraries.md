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
# <a name="event-hubs-management-libraries"></a>Librerie di gestione di Hub eventi

le raccolte di gestione degli hub di eventi Hello possano il provisioning dinamico di entità e spazi dei nomi di hub eventi. In questo modo eseguire distribuzioni complesse e scenari di messaggistica, in modo che è possibile determinare a livello di programmazione quali tooprovision di entità. Queste librerie sono attualmente disponibili per .NET.

## <a name="supported-functionality"></a>Funzionalità supportate

* Creazione, aggiornamento, eliminazione di spazi dei nomi
* Creazione, aggiornamento, eliminazione di Hub eventi
* Creazione, aggiornamento, eliminazione di gruppi di consumer

## <a name="prerequisites"></a>Prerequisiti

tooget avviato utilizzando le raccolte di gestione di hello hub eventi, è necessario eseguire l'autenticazione con Azure Active Directory (AAD). AAD, è necessario eseguire l'autenticazione come un'entità servizio, che fornisce accesso tooyour risorse di Azure. Per informazioni su come creare un'entità servizio, vedere uno di questi articoli:  

* [Utilizzare un'applicazione hello toocreate portale di Azure Active Directory e dell'entità servizio che possono accedere alle risorse](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [Usare Azure PowerShell toocreate una risorse tooaccess dell'entità servizio](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [Utilizzare toocreate CLI di Azure un risorse tooaccess dell'entità servizio](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

Queste esercitazioni forniscono un `AppId` (ID Client), `TenantId`, e `ClientSecret` (chiave di autenticazione), ognuno dei quali vengono utilizzati per l'autenticazione per le raccolte di gestione di hello. È necessario disporre di **proprietario** le autorizzazioni per il gruppo di risorse hello in cui si desidera toorun.

## <a name="programming-pattern"></a>Modello di programmazione

Hello modello toomanipulate qualsiasi risorsa di hub eventi segue un protocollo comune:

1. Ottenere un token da Azure Active Directory utilizzando hello `Microsoft.IdentityModel.Clients.ActiveDirectory` libreria.
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. Creare hello `EventHubManagementClient` oggetto.
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. Set hello `CreateOrUpdate` tooyour i parametri specificati.
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. Chiamare hello Execute.
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a>Passaggi successivi
* [Esempio di gestione .NET](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [Riferimento di Microsoft.Azure.Management.EventHub](/dotnet/api/Microsoft.Azure.Management.EventHub) 
