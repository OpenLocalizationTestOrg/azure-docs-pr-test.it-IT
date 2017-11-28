---
title: un'app Android in App mobili di Azure App Service aaaCreate | Documenti Microsoft
description: Seguire questa esercitazione tooget introduttive sull'utilizzo di back-end delle app mobili di Azure per lo sviluppo di Android
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 355f0959-aa7f-472c-a6c7-9eecea3a34a9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 0af85a3a4de9fc265976bbe3f34d73effc3807df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-android-app"></a><span data-ttu-id="61b6e-103">Creare un'app per Android</span><span class="sxs-lookup"><span data-stu-id="61b6e-103">Create an Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="61b6e-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="61b6e-104">Overview</span></span>
<span data-ttu-id="61b6e-105">Questa esercitazione viene illustrato come tooadd un back-end basato su cloud service tooan app per dispositivi mobili Android con un back-end dell'app per dispositivi mobili di Azure.</span><span class="sxs-lookup"><span data-stu-id="61b6e-105">This tutorial shows you how tooadd a cloud-based backend service tooan Android mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="61b6e-106">Verranno creati un nuovo back-end di app per dispositivi mobili e una semplice app Android di tipo *Todo list* che archivia dati delle app in Azure.</span><span class="sxs-lookup"><span data-stu-id="61b6e-106">You will create both a new mobile app backend and a simple *Todo list* Android app that stores app data in Azure.</span></span>

<span data-ttu-id="61b6e-107">Completato questa esercitazione è un prerequisito per tutte le altre esercitazioni sulla funzionalità delle App per dispositivi mobili hello in Azure App Service Android.</span><span class="sxs-lookup"><span data-stu-id="61b6e-107">Completing this tutorial is a prerequisite for all other Android tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61b6e-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="61b6e-108">Prerequisites</span></span>
<span data-ttu-id="61b6e-109">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="61b6e-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="61b6e-110">[Strumenti di sviluppo di Android](https://developer.android.com/sdk/index.html), che include l'ambiente di sviluppo integrato di Android Studio hello e la piattaforma Android più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="61b6e-110">[Android Developer Tools](https://developer.android.com/sdk/index.html), which includes hello Android Studio integrated development environment, and hello latest Android platform.</span></span>
* <span data-ttu-id="61b6e-111">Azure Mobile Android SDK, che viene fatto automaticamente riferimento come parte del progetto di avvio rapido hello scaricato.</span><span class="sxs-lookup"><span data-stu-id="61b6e-111">Azure Mobile Android SDK, which is automatically referenced as part of hello quickstart project you download.</span></span>
* <span data-ttu-id="61b6e-112">Un [account Azure attivo](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="61b6e-112">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="61b6e-113">Creare un nuovo back-end dell'app per dispositivi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="61b6e-113">Create a new Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a><span data-ttu-id="61b6e-114">Configurare il progetto server di hello</span><span class="sxs-lookup"><span data-stu-id="61b6e-114">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-android-app"></a><span data-ttu-id="61b6e-115">Scaricare ed eseguire l'applicazione Android hello</span><span class="sxs-lookup"><span data-stu-id="61b6e-115">Download and run hello Android app</span></span>
[!INCLUDE [app-service-mobile-android-run-app](../../includes/app-service-mobile-android-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
