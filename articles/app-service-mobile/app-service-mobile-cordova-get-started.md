---
title: Creare un'app Cordova in App per dispositivi mobili del Servizio app di Azure | Microsoft Docs
description: Seguire questa esercitazione per iniziare a usare i back-end dell'app per dispositivi mobili per lo sviluppo di Apache Cordova
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
ms.openlocfilehash: b620465cdc3cfa04933dc6e70163fc32aa9a839b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-apache-cordova-app"></a><span data-ttu-id="54d68-104">Creare un'app Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="54d68-104">Create an Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="54d68-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="54d68-105">Overview</span></span>
<span data-ttu-id="54d68-106">Questa esercitazione illustra come aggiungere un servizio back-end basato sul cloud a un'app per dispositivi mobili Apache Cordova mediante un back-end per app per dispositivi mobili di Azure.</span><span class="sxs-lookup"><span data-stu-id="54d68-106">This tutorial shows you how to add a cloud-based backend service to an Apache Cordova mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="54d68-107">Verranno creati un nuovo back-end di app per dispositivi mobili e una semplice app Apache Cordova di tipo *Todo list* che archivia i dati delle app in Azure.</span><span class="sxs-lookup"><span data-stu-id="54d68-107">You create both a new mobile app backend and a simple *Todo list* Apache Cordova app that stores app data in Azure.</span></span>

<span data-ttu-id="54d68-108">Il completamento di questa esercitazione è un prerequisito per tutte le altre esercitazioni Apache Cordova relative all'uso della funzionalità delle app per dispositivi mobili nel Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="54d68-108">Completing this tutorial is a prerequisite for all other Apache Cordova tutorials about using the Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54d68-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="54d68-109">Prerequisites</span></span>
<span data-ttu-id="54d68-110">Per completare questa esercitazione è necessario soddisfare i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="54d68-110">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="54d68-111">Un PC con installato [Visual Studio Community 2017] o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="54d68-111">A PC with [Visual Studio Community 2017] or newer.</span></span>
* <span data-ttu-id="54d68-112">[Visual Studio Tools per Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="54d68-112">[Visual Studio Tools for Apache Cordova].</span></span>
* <span data-ttu-id="54d68-113">Un [account Azure attivo](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="54d68-113">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="54d68-114">È anche possibile ignorare Visual Studio e usare direttamente la riga di comando di Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="54d68-114">You may also bypass Visual Studio and use the Apache Cordova command line directly.</span></span>  <span data-ttu-id="54d68-115">L'uso della riga di comando è utile quando l'esercitazione viene completata in un computer Mac.</span><span class="sxs-lookup"><span data-stu-id="54d68-115">Using the command line is useful when completing the tutorial on a Mac computer.</span></span>  <span data-ttu-id="54d68-116">La compilazione di applicazioni client di Apache Cordova dalla riga di comando non è trattata in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="54d68-116">Compiling Apache Cordova client applications using the command line is not covered by this tutorial.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="54d68-117">Creare un back-end dell'app per dispositivi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="54d68-117">Create an Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[<span data-ttu-id="54d68-118">Guardare un video che illustra una procedura simile</span><span class="sxs-lookup"><span data-stu-id="54d68-118">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-the-server-project"></a><span data-ttu-id="54d68-119">Configurare il progetto server</span><span class="sxs-lookup"><span data-stu-id="54d68-119">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-apache-cordova-app"></a><span data-ttu-id="54d68-120">Scaricare ed eseguire l'app Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="54d68-120">Download and run the Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a><span data-ttu-id="54d68-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="54d68-121">Next Steps</span></span>
<span data-ttu-id="54d68-122">Ora che l'esercitazione introduttiva è stata completata, passare a una delle esercitazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="54d68-122">Now that you completed this quick start tutorial, move on to one of the following tutorials:</span></span>

* <span data-ttu-id="54d68-123">[Aggiungere dati offline](app-service-mobile-cordova-get-started-offline-data.md) all'app Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="54d68-123">[Add Offline Data](app-service-mobile-cordova-get-started-offline-data.md) to your Apache Cordova app.</span></span>
* <span data-ttu-id="54d68-124">[Aggiungere l'autenticazione all'app Apache Cordova](app-service-mobile-cordova-get-started-users.md) .</span><span class="sxs-lookup"><span data-stu-id="54d68-124">[Add Authentication](app-service-mobile-cordova-get-started-users.md) to your Apache Cordova app.</span></span>
* <span data-ttu-id="54d68-125">[Aggiungere notifiche push all'app Apache Cordova](app-service-mobile-cordova-get-started-push.md) .</span><span class="sxs-lookup"><span data-stu-id="54d68-125">[Add Push Notifications](app-service-mobile-cordova-get-started-push.md) to your Apache Cordova app.</span></span>

<span data-ttu-id="54d68-126">Altre informazioni sui concetti chiave del servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="54d68-126">Learn more about key concepts with Azure App Service.</span></span>

* <span data-ttu-id="54d68-127">[Dati offline]</span><span class="sxs-lookup"><span data-stu-id="54d68-127">[Offline Data]</span></span>
* <span data-ttu-id="54d68-128">[autenticazione]</span><span class="sxs-lookup"><span data-stu-id="54d68-128">[Authentication]</span></span>
* <span data-ttu-id="54d68-129">[Notifiche push]</span><span class="sxs-lookup"><span data-stu-id="54d68-129">[Push Notifications]</span></span>

<span data-ttu-id="54d68-130">Informazioni su come usare gli SDK.</span><span class="sxs-lookup"><span data-stu-id="54d68-130">Learn how to use the SDKs.</span></span>

* <span data-ttu-id="54d68-131">[Apache Cordova SDK]</span><span class="sxs-lookup"><span data-stu-id="54d68-131">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="54d68-132">[ASP.NET Server SDK]</span><span class="sxs-lookup"><span data-stu-id="54d68-132">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="54d68-133">[Node.js Server SDK]</span><span class="sxs-lookup"><span data-stu-id="54d68-133">[Node.js Server SDK]</span></span>

<!-- Images. -->

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
<span data-ttu-id="54d68-134">[Visual Studio Community 2017]: http://www.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="54d68-134">[Visual Studio Community 2017]: http://www.visualstudio.com/</span></span>
<span data-ttu-id="54d68-135">[Visual Studio Tools per Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span><span class="sxs-lookup"><span data-stu-id="54d68-135">[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span></span>
<span data-ttu-id="54d68-136">[Dati offline]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="54d68-136">[Offline Data]: app-service-mobile-offline-data-sync.md</span></span>
<span data-ttu-id="54d68-137">[autenticazione]: app-service-mobile-auth.md</span><span class="sxs-lookup"><span data-stu-id="54d68-137">[Authentication]: app-service-mobile-auth.md</span></span>
<span data-ttu-id="54d68-138">[Notifiche push]: ../notification-hubs/notification-hubs-push-notification-overview.md</span><span class="sxs-lookup"><span data-stu-id="54d68-138">[Push Notifications]: ../notification-hubs/notification-hubs-push-notification-overview.md</span></span>
<span data-ttu-id="54d68-139">[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md</span><span class="sxs-lookup"><span data-stu-id="54d68-139">[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md</span></span>
<span data-ttu-id="54d68-140">[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="54d68-140">[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span></span>
<span data-ttu-id="54d68-141">[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="54d68-141">[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span></span>
