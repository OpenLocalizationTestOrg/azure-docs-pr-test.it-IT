---
title: introduzione di App aaaAPI | Documenti Microsoft
description: Informazioni su come usare il servizio app di Azure per sviluppare, ospitare e utilizzare le API RESTful.
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 60049a16-8159-47aa-a34b-110be0d8dab6
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
ms.author: alkarche
ms.openlocfilehash: f066e96db667d4685480001bc43c2b1bff4ea352
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="api-apps-overview"></a>Panoramica delle app per le API
App per le API in funzionalità offerta di servizio App di Azure che rendono più semplice toodevelop, host e utilizzare le API in locale e cloud di hello. Le app per le API offrono sicurezza di livello aziendale, controllo di accesso semplificato, connettività ibrida, generazione automatica di SDK e perfetta integrazione con le [app per la logica](../logic-apps/logic-apps-what-are-logic-apps.md).

[servizio app di Azure](../app-service/app-service-value-prop-what-is.md) è una piattaforma completamente gestita per scenari Web, mobili e di integrazione. Le app per le API sono uno dei quattro tipi di app offerti da [Servizio app di Azure](../app-service/app-service-value-prop-what-is.md).

![Tipi di app nel Servizio app di Azure](./media/app-service-api-apps-why-best-platform/appservicesuite.png)

## <a name="why-use-api-apps"></a>Perché usare le app per le API?
Di seguito sono elencate alcune delle funzionalità principali delle app per le API:

* **Portare l'API esistente come-è** - non si dispone di hello codice toochange in esistente API tootake comodamente di App per le API - appena distribuire l'app tooan API di codice. L'API può usare qualsiasi linguaggio o framework supportato dal servizio app, inclusi ASP.NET, C#, Java, PHP, Node. js e Python.
* **Facilità di utilizzo** : grazie al supporto integrato per i [metadati dell’API Swagger](http://swagger.io/) le API sono più facilmente utilizzabili da client diversi.  Viene generato automaticamente il codice client per le API in diversi linguaggi, inclusi C#, Java e Javascript. Configurare facilmente [CORS](app-service-api-cors-consume-javascript.md) senza modificare il codice. Per altre informazioni, vedere [Metadati delle app per le API del servizio app per l'individuazione di API e la generazione di codice](app-service-api-metadata.md) e [Utilizzare un'app per le API da JavaScript tramite CORS](app-service-api-cors-consume-javascript.md). 
* **Controllo di accesso semplice** -proteggere un'app per le API da accesso non autenticato senza codice tooyour le modifiche. I servizi di autenticazione integrati proteggono le API dall'accesso da altri servizi o da client che rappresentano gli utenti. I provider di identità supportati includono Azure Active Directory, Facebook, Twitter, Google e account Microsoft. I client possono usare Active Directory Authentication Library (ADAL) o hello Mobile App SDK. Per altre informazioni, vedere [Autenticazione e autorizzazione per app per le API nel servizio app di Azure](app-service-api-authentication.md).
* **Integrazione di Visual Studio** -dedicati strumenti in Visual Studio semplificano il lavoro hello di creazione, la distribuzione, utilizzo, il debug e la gestione di App per le API. Per ulteriori informazioni, vedere [Announcing hello Azure SDK 2.8.1 per .NET](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/).
* **Integrazione con app per la logica** : le app per le API create possono essere utilizzate dalle [app per la logica del servizio app](../logic-apps/logic-apps-what-are-logic-apps.md).  Per altre informazioni, vedere [Uso dell'API personalizzata ospitata nel servizio app con App per la logica](../logic-apps/logic-apps-custom-hosted-api.md) and [Nuova versione dello schema 2015-08-01-preview](../logic-apps/logic-apps-schema-2015-08-01.md).

Inoltre, un'app per le API può avvalersi delle funzionalità offerte dalle [app Web](../app-service-web/app-service-web-overview.md) e dalle [app per dispositivi mobili](../app-service-mobile/app-service-mobile-value-prop.md). Hello inversa è anche vero: se si usa un'app web o app per dispositivi mobili toohost un'API, possa usufruire delle funzionalità di App per le API, ad esempio i metadati Swagger per client la generazione di codice e la condivisione CORS per l'accesso tra domini diversi browser. Hello solo differenza tra hello tre tipi di app (API, web, dispositivi mobili) è il nome di hello e l'icona utilizzata per essi in hello portale di Azure.

## <a name="whats-hello-difference-between-api-apps-and-azure-api-management"></a>Qual è la differenza hello tra App per le API e di gestione API di Azure?
Le app per le API e la [Gestione API di Azure](../api-management/api-management-key-concepts.md) sono servizi complementari:

* Gestione API permette di gestire le API. Inserire un front-end di gestione API in un toomonitor API e limitare l'utilizzo della, modificare l'input e output, consolidare diverse API in un endpoint e così via. Hello API gestite può essere ospitato in qualsiasi punto.
* Le app per le api consentono l'hosting delle API. servizio Hello include funzionalità che semplificano lo sviluppo e dispendiosa in termini di API, ma non i tipi di monitoraggio, la limitazione delle richieste, la modifica o il consolidamento di che Gestione API non hello. Se non sono necessarie le funzionalità di Gestione API, è possibile ospitare le API nelle app per le API senza usare Gestione API.

Ecco un diagramma che illustra Gestione API usato per le API ospitate nelle app per le API e altrove.

![Gestione API di Azure e app per le API](./media/app-service-api-apps-why-best-platform/apia-apim.png)

Gestione API e le app per le API talvolta offrono funzionalità simili.  Ad esempio, entrambe permettono di automatizzare il supporto CORS. Quando si utilizzano due servizi hello insieme, utilizzare Gestione API per CORS perché funzioni come hello App tooyour API front-end. 

## <a name="getting-started"></a>introduttiva
tooget iniziare con le app API distribuendo tooone codice di esempio, vedere Esercitazione hello per il framework desiderato:

* [ASP.NET](app-service-api-dotnet-get-started.md) 
* [Node.JS](app-service-api-nodejs-api-app.md) 
* [Java](app-service-api-java-api-app.md) 

tooask domande sulle API App, avviare un thread in hello [forum di App per le API](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureAPIApps). 

