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
# <a name="create-an-apache-cordova-app"></a><span data-ttu-id="27759-104">Creare un'app Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="27759-104">Create an Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="27759-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="27759-105">Overview</span></span>
<span data-ttu-id="27759-106">Questa esercitazione viene illustrato come tooadd un back-end basato su cloud service tooan Apache Cordova app per dispositivi mobili utilizzando un back-end dell'app per dispositivi mobili di Azure.</span><span class="sxs-lookup"><span data-stu-id="27759-106">This tutorial shows you how tooadd a cloud-based backend service tooan Apache Cordova mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="27759-107">Verranno creati un nuovo back-end di app per dispositivi mobili e una semplice app Apache Cordova di tipo *Todo list* che archivia i dati delle app in Azure.</span><span class="sxs-lookup"><span data-stu-id="27759-107">You create both a new mobile app backend and a simple *Todo list* Apache Cordova app that stores app data in Azure.</span></span>

<span data-ttu-id="27759-108">Completato questa esercitazione è un prerequisito per tutte le altre esercitazioni di Apache Cordova sull'utilizzo delle funzionalità di App per dispositivi mobili hello in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="27759-108">Completing this tutorial is a prerequisite for all other Apache Cordova tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27759-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="27759-109">Prerequisites</span></span>
<span data-ttu-id="27759-110">toocomplete questa esercitazione, è necessario hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="27759-110">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="27759-111">Un PC con installato [Visual Studio Community 2017] o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="27759-111">A PC with [Visual Studio Community 2017] or newer.</span></span>
* <span data-ttu-id="27759-112">[Visual Studio Tools per Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="27759-112">[Visual Studio Tools for Apache Cordova].</span></span>
* <span data-ttu-id="27759-113">Un [account Azure attivo](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="27759-113">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="27759-114">È anche possibile ignorare Visual Studio e utilizzare direttamente la riga di comando di hello Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="27759-114">You may also bypass Visual Studio and use hello Apache Cordova command line directly.</span></span>  <span data-ttu-id="27759-115">Tramite riga di comando hello è utile quando si completa l'esercitazione hello in un computer Mac.</span><span class="sxs-lookup"><span data-stu-id="27759-115">Using hello command line is useful when completing hello tutorial on a Mac computer.</span></span>  <span data-ttu-id="27759-116">La compilazione di applicazioni client di Apache Cordova tramite riga di comando hello non rientrano in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="27759-116">Compiling Apache Cordova client applications using hello command line is not covered by this tutorial.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="27759-117">Creare un back-end dell'app per dispositivi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="27759-117">Create an Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[<span data-ttu-id="27759-118">Guardare un video che illustra una procedura simile</span><span class="sxs-lookup"><span data-stu-id="27759-118">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-hello-server-project"></a><span data-ttu-id="27759-119">Configurare il progetto server di hello</span><span class="sxs-lookup"><span data-stu-id="27759-119">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-apache-cordova-app"></a><span data-ttu-id="27759-120">Scaricare ed eseguire app di Apache Cordova hello</span><span class="sxs-lookup"><span data-stu-id="27759-120">Download and run hello Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a><span data-ttu-id="27759-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="27759-121">Next Steps</span></span>
<span data-ttu-id="27759-122">Ora che è stata completata questa esercitazione introduttiva, passare tooone di hello seguenti esercitazioni:</span><span class="sxs-lookup"><span data-stu-id="27759-122">Now that you completed this quick start tutorial, move on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="27759-123">[Aggiungere dati Offline](app-service-mobile-cordova-get-started-offline-data.md) tooyour app di Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="27759-123">[Add Offline Data](app-service-mobile-cordova-get-started-offline-data.md) tooyour Apache Cordova app.</span></span>
* <span data-ttu-id="27759-124">[Aggiungere l'autenticazione](app-service-mobile-cordova-get-started-users.md) tooyour app di Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="27759-124">[Add Authentication](app-service-mobile-cordova-get-started-users.md) tooyour Apache Cordova app.</span></span>
* <span data-ttu-id="27759-125">[Aggiungere le notifiche Push](app-service-mobile-cordova-get-started-push.md) tooyour app di Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="27759-125">[Add Push Notifications](app-service-mobile-cordova-get-started-push.md) tooyour Apache Cordova app.</span></span>

<span data-ttu-id="27759-126">Altre informazioni sui concetti chiave del servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="27759-126">Learn more about key concepts with Azure App Service.</span></span>

* <span data-ttu-id="27759-127">[Dati offline]</span><span class="sxs-lookup"><span data-stu-id="27759-127">[Offline Data]</span></span>
* <span data-ttu-id="27759-128">[autenticazione]</span><span class="sxs-lookup"><span data-stu-id="27759-128">[Authentication]</span></span>
* <span data-ttu-id="27759-129">[Notifiche push]</span><span class="sxs-lookup"><span data-stu-id="27759-129">[Push Notifications]</span></span>

<span data-ttu-id="27759-130">Informazioni su come toouse hello SDK.</span><span class="sxs-lookup"><span data-stu-id="27759-130">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="27759-131">[Apache Cordova SDK]</span><span class="sxs-lookup"><span data-stu-id="27759-131">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="27759-132">[ASP.NET Server SDK]</span><span class="sxs-lookup"><span data-stu-id="27759-132">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="27759-133">[Node.js Server SDK]</span><span class="sxs-lookup"><span data-stu-id="27759-133">[Node.js Server SDK]</span></span>

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
