---
title: un'app Cordova in App mobili di Azure App Service aaaCreate | Documenti Microsoft
description: Seguire questa esercitazione tooget introduttive sull'utilizzo di back-end delle app mobili di Azure per lo sviluppo di Apache Cordova
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
tags: 
keywords: cordova,javascript,dispositivi mobili,client
ms.assetid: 0b08fc12-0a80-42d3-9cc1-9b3f8d3e3a3f
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: hero-article
ms.date: 07/07/2017
ms.author: glenga
ms.openlocfilehash: 4981cbc0686c15230019ac9f30495f30cbf2c791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-cordova-app"></a>Creare un'app Apache Cordova
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Panoramica
Questa esercitazione viene illustrato come tooadd un back-end basato su cloud service tooan Apache Cordova app per dispositivi mobili utilizzando un back-end dell'app per dispositivi mobili di Azure.  Verranno creati un nuovo back-end di app per dispositivi mobili e una semplice app Apache Cordova di tipo *Todo list* che archivia i dati delle app in Azure.

Completato questa esercitazione è un prerequisito per tutte le altre esercitazioni di Apache Cordova sull'utilizzo delle funzionalità di App per dispositivi mobili hello in Azure App Service.

## <a name="prerequisites"></a>Prerequisiti
toocomplete questa esercitazione, è necessario hello seguenti prerequisiti:

* Un PC con installato [Visual Studio Community 2017] o versione successiva.
* [Visual Studio Tools per Apache Cordova].
* Un [account Azure attivo](https://azure.microsoft.com/pricing/free-trial/).

È anche possibile ignorare Visual Studio e utilizzare direttamente la riga di comando di hello Apache Cordova.  Tramite riga di comando hello è utile quando si completa l'esercitazione hello in un computer Mac.  La compilazione di applicazioni client di Apache Cordova tramite riga di comando hello non rientrano in questa esercitazione.

## <a name="create-an-azure-mobile-app-backend"></a>Creare un back-end dell'app per dispositivi mobili di Azure
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[Guardare un video che illustra una procedura simile](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-hello-server-project"></a>Configurare il progetto server di hello
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-apache-cordova-app"></a>Scaricare ed eseguire app di Apache Cordova hello
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a>Passaggi successivi
Ora che è stata completata questa esercitazione introduttiva, passare tooone di hello seguenti esercitazioni:

* [Aggiungere dati Offline](app-service-mobile-cordova-get-started-offline-data.md) tooyour app di Apache Cordova.
* [Aggiungere l'autenticazione](app-service-mobile-cordova-get-started-users.md) tooyour app di Apache Cordova.
* [Aggiungere le notifiche Push](app-service-mobile-cordova-get-started-push.md) tooyour app di Apache Cordova.

Altre informazioni sui concetti chiave del servizio app di Azure.

* [Dati offline]
* [autenticazione]
* [Notifiche push]

Informazioni su come toouse hello SDK.

* [Apache Cordova SDK]
* [ASP.NET Server SDK]
* [Node.js Server SDK]

<!-- Images. -->

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2017]: http://www.visualstudio.com/
[Visual Studio Tools per Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Dati offline]: app-service-mobile-offline-data-sync.md
[autenticazione]: app-service-mobile-auth.md
[Notifiche push]: ../notification-hubs/notification-hubs-push-notification-overview.md
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
