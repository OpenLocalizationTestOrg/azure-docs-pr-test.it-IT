---
title: metadati di servizio App per le API aaaApp per la generazione di individuazione e il codice API | Documenti Microsoft
description: Informazioni sull'App per le API in Azure App Service utilizzo generazione metadati Swagger toofacilitate API di individuazione e il codice.
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: c7f8e33a-61cc-486f-89df-4a97dc3c71d4
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: alkarche
ms.openlocfilehash: b27e70b7dd6bd97f5b0b490b496320befe7442c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-api-apps-metadata-for-api-discovery-and-code-generation"></a>Metadati delle app per le API del servizio app per l'individuazione di API e la generazione di codice
Il supporto per i metadati dell'API [Swagger 2.0](http://swagger.io/) è incorporato nelle app per le API del servizio app. Non è necessario toouse Swagger, ma se si utilizza, è possibile sfruttare le funzionalità di App per le API che semplificano l'individuazione e l'utilizzo.   

## <a name="swagger-endpoint"></a>Endpoint Swagger
È possibile specificare un endpoint che fornisce i metadati di Swagger 2.0 JSON per un'app per le API in una proprietà dell'app per le API hello. Hello endpoint può essere relativo toohello URL di base di app per le API hello o un URL assoluto. URL assoluto può puntare all'esterno delle app per le API hello. 

Numero di client downstream (ad esempio, la generazione del codice di Visual Studio e il flusso di "Aggiungi API" PowerApps), hello URL deve essere accessibile pubblicamente (non protetto dall'utente o l'autenticazione del servizio). Ciò significa che se si utilizza l'autenticazione del servizio App e si desidera definizione dell'API hello tooexpose all'interno dell'app stessa, è necessario toouse opzione di autenticazione che consente il traffico anonimo tooreach dell'API. Per altre informazioni, vedere [Autenticazione e autorizzazione per le app per le API del servizio app](app-service-api-authentication.md).

### <a name="portal-blade"></a>Pannello del portale
In hello [portale di Azure](https://portal.azure.com/) hello endpoint URL può essere visualizzato e modificato in hello **di definizione dell'API** blade.

![](./media/app-service-api-metadata/apidefblade.png)

### <a name="azure-resource-manager-property"></a>Proprietà Gestione risorse di Azure
È inoltre possibile configurare l'URL di definizione dell'API hello per un'app per le API tramite [Esplora inventario risorse](https://resources.azure.com/) o [modelli di gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md) in strumenti da riga di comando, ad esempio [Azure PowerShell](/powershell/azureps-cmdlets-docs)hello e [CLI di Azure](../cli-install-nodejs.md). 

In **Esplora inventario risorse**, andare troppo**sottoscrizioni > {sottoscrizione} > resourceGroups > {il gruppo di risorse} > provider > Microsoft > siti > {sito} > Configurazione > web**, si noterà hello `apiDefinition` proprietà:

        "apiDefinition": {
          "url": "https://contactslistapi.azurewebsites.net/swagger/docs/v1"
        }

Per un esempio di un modello di gestione risorse di Azure che imposta hello `apiDefinition` proprietà, aprire hello [azuredeploy.json file nell'applicazione di esempio elenco attività hello](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json). Individuare la sezione hello del modello di hello simile: esempio hello JSON illustrato in precedenza.

### <a name="default-value"></a>Valore predefinito
Quando si utilizza Visual Studio toocreate un'app per le API, endpoint di definizione API hello viene impostata automaticamente URL di base dell'applicazione hello API più toohello `/swagger/docs/v1`. Si tratta di URL predefinito hello che hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) pacchetto NuGet Usa i metadati di Swagger tooserve generato dinamicamente per un progetto ASP.NET Web API. 

## <a name="code-generation"></a>Generazione del codice
Uno dei vantaggi di hello integrazione dei Swagger in App per le API di Azure è la generazione automatica di codice. Classi client generate rendono più semplice toowrite il codice che chiama un'API app.

È possibile generare codice client per un'app per le API tramite Visual Studio o dalla riga di comando hello. Per informazioni su come client toogenerate le classi in Visual Studio per un progetto di API Web ASP.NET, vedere [Introduzione alle App per le API e ASP.NET](app-service-api-dotnet-get-started.md#codegen). Per informazioni su come toodo dal comando hello riga per tutte le lingue supportate, vedere il file Leggimi hello di hello [Azure/autorest](https://github.com/azure/autorest) repository in GitHub.com.

## <a name="next-steps"></a>Passaggi successivi
Per un'esercitazione dettagliata sulle procedure di creazione, distribuzione e utilizzo di un'app per le API, vedere [Introduzione alle app per le API nel servizio app di Azure](app-service-api-dotnet-get-started.md).

Se si utilizza Gestione API di Azure con App per le API, è possibile utilizzare tooimport metadati Swagger dell'API in Gestione API. Per ulteriori informazioni, vedere [come tooimport hello definizione di un'API con le operazioni di gestione API di Azure](../api-management/api-management-howto-import-api.md). 

