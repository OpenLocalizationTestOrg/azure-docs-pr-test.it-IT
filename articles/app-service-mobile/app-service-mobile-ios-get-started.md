---
title: Creare un'app iOS in App per dispositivi mobili del servizio app di Azure | Microsoft Docs
description: Seguire questa esercitazione per iniziare a usare i back-end dell'app per dispositivi mobili di Azure per lo sviluppo per iOS in Objective-C o Swift
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 6461a899-9340-42dd-b118-ffc5ba00e846
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 36936ae66c458fcbedeec95cfa2f573a40c8af53
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-ios-app"></a><span data-ttu-id="5e9ff-103">Creare un'app iOS</span><span class="sxs-lookup"><span data-stu-id="5e9ff-103">Create an iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="5e9ff-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="5e9ff-104">Overview</span></span>
<span data-ttu-id="5e9ff-105">Questa esercitazione illustra come aggiungere [app per dispositivi mobili di Azure](app-service-mobile-value-prop.md), un servizio back-end cloud, a un'app per iOS.</span><span class="sxs-lookup"><span data-stu-id="5e9ff-105">This tutorial shows how to add [Azure Mobile Apps](app-service-mobile-value-prop.md), a cloud backend service, to an iOS app.</span></span> <span data-ttu-id="5e9ff-106">Per prima cosa si creerà un nuovo back-end mobile.</span><span class="sxs-lookup"><span data-stu-id="5e9ff-106">We'll first create a new mobile backend.</span></span> <span data-ttu-id="5e9ff-107">Si userà quindi una semplice app per iOS *Todo list* per archiviare i dati in Azure.</span><span class="sxs-lookup"><span data-stu-id="5e9ff-107">Then, we'll use a simple *Todo list* iOS app to store data in Azure.</span></span>

<span data-ttu-id="5e9ff-108">Per completare l'esercitazione, è necessario un computer Mac e [un account Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="5e9ff-108">To complete this tutorial, you need a Mac and [an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>

## <a name="step-i-create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="5e9ff-109">Passaggio I: Creare un nuovo back-end dell'app per dispositivi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="5e9ff-109">Step I: Create a new Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="step-ii-configure-the-backend-project"></a><span data-ttu-id="5e9ff-110">Passaggio II: Configurare il progetto back-end</span><span class="sxs-lookup"><span data-stu-id="5e9ff-110">Step II: Configure the backend project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="step-iii-download-and-run-the-ios-app"></a><span data-ttu-id="5e9ff-111">Passaggio III: Scaricare ed eseguire l'app iOS</span><span class="sxs-lookup"><span data-stu-id="5e9ff-111">Step III: Download and run the iOS app</span></span>
[!INCLUDE [app-service-mobile-ios-run-app](../../includes/app-service-mobile-ios-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
