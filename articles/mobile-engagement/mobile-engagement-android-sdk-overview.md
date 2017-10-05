---
title: Integrazione di Android SDK per Azure Mobile Engagement
description: Descrive come integrare l'SDK di Azure Mobile Engagement nelle app Android
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a91ed04f-f3ce-4692-a6dd-b56a28d7dee8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo;ricksal
ms.openlocfilehash: 35935e911f1f17989beb71978396c6d1b7d601d6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a><span data-ttu-id="5da1c-103">Integrazione di Android SDK per Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="5da1c-103">Android SDK Integration for Azure Mobile Engagement</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5da1c-104">Windows universale</span><span class="sxs-lookup"><span data-stu-id="5da1c-104">Universal Windows</span></span>](mobile-engagement-windows-store-sdk-overview.md)
> * [<span data-ttu-id="5da1c-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="5da1c-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-sdk-overview.md)
> * [<span data-ttu-id="5da1c-106">iOS</span><span class="sxs-lookup"><span data-stu-id="5da1c-106">iOS</span></span>](mobile-engagement-ios-sdk-overview.md)
> * [<span data-ttu-id="5da1c-107">Android</span><span class="sxs-lookup"><span data-stu-id="5da1c-107">Android</span></span>](mobile-engagement-android-sdk-overview.md)
> 
> 

<span data-ttu-id="5da1c-108">Questo documento descrive tutte le opzioni di configurazione e integrazione disponibili per Android SDK per Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="5da1c-108">This document describes all the integration and configuration options available for Azure Mobile Engagement Android SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5da1c-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5da1c-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a><span data-ttu-id="5da1c-110">Funzionalità avanzate</span><span class="sxs-lookup"><span data-stu-id="5da1c-110">Advanced Features</span></span>
### <a name="reporting-features"></a><span data-ttu-id="5da1c-111">Funzionalità di segnalazione</span><span class="sxs-lookup"><span data-stu-id="5da1c-111">Reporting Features</span></span>
<span data-ttu-id="5da1c-112">È possibile aggiungere queste funzionalità:</span><span class="sxs-lookup"><span data-stu-id="5da1c-112">You can add these features:</span></span>

1. [<span data-ttu-id="5da1c-113">Opzioni di segnalazione avanzata</span><span class="sxs-lookup"><span data-stu-id="5da1c-113">Advanced reporting options</span></span>](mobile-engagement-android-advanced-reporting.md)
2. [<span data-ttu-id="5da1c-114">Opzioni di segnalazione della posizione</span><span class="sxs-lookup"><span data-stu-id="5da1c-114">Location Reporting options</span></span>](mobile-engagement-android-location-reporting.md)
3. [<span data-ttu-id="5da1c-115">Opzioni di configurazione avanzate</span><span class="sxs-lookup"><span data-stu-id="5da1c-115">Advanced Configuration options</span></span>](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a><span data-ttu-id="5da1c-116">Notifiche:</span><span class="sxs-lookup"><span data-stu-id="5da1c-116">Notifications:</span></span>
[<span data-ttu-id="5da1c-117">Come integrare la copertura (notifiche) nell'app per Android</span><span class="sxs-lookup"><span data-stu-id="5da1c-117">How to integrate Reach (Notifications) in your Android app</span></span>](mobile-engagement-android-integrate-engagement-reach.md)

1. <span data-ttu-id="5da1c-118">Google Cloud Messaging (GCM): [Come integrare GCM con Mobile Engagement](mobile-engagement-android-gcm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="5da1c-118">Google Cloud Messaging (GCM): [How to Integrate GCM with Mobile Engagement](mobile-engagement-android-gcm-integrate.md)</span></span>
2. <span data-ttu-id="5da1c-119">Amazon Device Messaging (ADM): [Come integrare ADM con Mobile Engagement](mobile-engagement-android-adm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="5da1c-119">Amazon Device Messaging (ADM): [How to Integrate ADM with Mobile Engagement](mobile-engagement-android-adm-integrate.md)</span></span>

### <a name="tag-plan-implementation"></a><span data-ttu-id="5da1c-120">Implementazione del piano di tag:</span><span class="sxs-lookup"><span data-stu-id="5da1c-120">Tag plan implementation:</span></span>
[<span data-ttu-id="5da1c-121">Come usare l'API di assegnazione di tag di Mobile Engagement avanzata nell'app per Android</span><span class="sxs-lookup"><span data-stu-id="5da1c-121">How to use the advanced Mobile Engagement tagging API in your Android app</span></span>](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a><span data-ttu-id="5da1c-122">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="5da1c-122">Release notes</span></span>

### <a name="431-07172017"></a><span data-ttu-id="5da1c-123">4.3.1 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="5da1c-123">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="5da1c-124">Correzione di un arresto anomalo del sistema che può verificarsi raramente quando si chiama `EngagementAgentUtils.isInDedicatedEngagementProcess`, che viene usato anche dalla classe `EngagementApplication`.</span><span class="sxs-lookup"><span data-stu-id="5da1c-124">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by the `EngagementApplication` class.</span></span>

### <a name="430-06272017"></a><span data-ttu-id="5da1c-125">4.3.0 (06/27/2017)</span><span class="sxs-lookup"><span data-stu-id="5da1c-125">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="5da1c-126">Supporto Android 8 (versioni precedenti dell'SDK non funzionano in Android 8).</span><span class="sxs-lookup"><span data-stu-id="5da1c-126">Android 8 support (previous versions of the SDK will not work on Android 8).</span></span>
* <span data-ttu-id="5da1c-127">Nessuna dipendenza nella raccolta di supporto.</span><span class="sxs-lookup"><span data-stu-id="5da1c-127">No more dependency on support library.</span></span>
* <span data-ttu-id="5da1c-128">Rimuovere la classe `EngagementFragmentActivity`.</span><span class="sxs-lookup"><span data-stu-id="5da1c-128">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="5da1c-129">A causa di [limiti di esecuzione in Background](https://developer.android.com/preview/features/background.html) in Android 8, i log in background potrebbero subire un ritardo fino a quando l'utente non interagisce con il dispositivo; ciò avrà un impatto sulla campagna Push **Consegnata** e sulle statistiche **Notifica di sistema visualizzata** che subiscono un ritardo se il dispositivo era in sospensione (la notifica verrà ancora visualizzata, suonerà e vibrerà in tempo reale senza problemi).</span><span class="sxs-lookup"><span data-stu-id="5da1c-129">Due to [Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until the user interacts with the device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if the device was sleeping (the notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="5da1c-130">A causa di [limiti del percorso di background](https://developer.android.com/preview/features/background-location-limits.html), il percorso in tempo reale in background non verrà aggiornato frequentemente in Android 8.</span><span class="sxs-lookup"><span data-stu-id="5da1c-130">Due to [Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), the real time location in background will not be updated frequently on Android 8.</span></span>

<span data-ttu-id="5da1c-131">Per tutte le versioni, vedere le [note sulla versione complete](mobile-engagement-android-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="5da1c-131">For all versions, see the [complete release notes](mobile-engagement-android-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="5da1c-132">Procedure di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="5da1c-132">Upgrade procedures</span></span>
<span data-ttu-id="5da1c-133">Se è già stata integrata una versione precedente di Windows SDK nell'applicazione, vedere le [procedure di aggiornamento](mobile-engagement-android-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="5da1c-133">If you already have integrated an older version of our SDK into your application, consult [Upgrade Procedures](mobile-engagement-android-upgrade-procedure.md).</span></span>

