---
title: aaaAndroid integrazione del SDK per Azure Mobile Engagement
description: Viene descritto come toointegrate Azure Mobile Engagement SDK nelle App Android
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
ms.openlocfilehash: 0c63bfaf673abbda7ea498390f8282c43e2fb8df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a><span data-ttu-id="4066a-103">Integrazione di Android SDK per Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="4066a-103">Android SDK Integration for Azure Mobile Engagement</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4066a-104">Windows universale</span><span class="sxs-lookup"><span data-stu-id="4066a-104">Universal Windows</span></span>](mobile-engagement-windows-store-sdk-overview.md)
> * [<span data-ttu-id="4066a-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="4066a-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-sdk-overview.md)
> * [<span data-ttu-id="4066a-106">iOS</span><span class="sxs-lookup"><span data-stu-id="4066a-106">iOS</span></span>](mobile-engagement-ios-sdk-overview.md)
> * [<span data-ttu-id="4066a-107">Android</span><span class="sxs-lookup"><span data-stu-id="4066a-107">Android</span></span>](mobile-engagement-android-sdk-overview.md)
> 
> 

<span data-ttu-id="4066a-108">Questo documento descrive tutti hello integration e opzioni di configurazione disponibili per Azure Mobile Engagement SDK Android.</span><span class="sxs-lookup"><span data-stu-id="4066a-108">This document describes all hello integration and configuration options available for Azure Mobile Engagement Android SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4066a-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4066a-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a><span data-ttu-id="4066a-110">Funzionalità avanzate</span><span class="sxs-lookup"><span data-stu-id="4066a-110">Advanced Features</span></span>
### <a name="reporting-features"></a><span data-ttu-id="4066a-111">Funzionalità di segnalazione</span><span class="sxs-lookup"><span data-stu-id="4066a-111">Reporting Features</span></span>
<span data-ttu-id="4066a-112">È possibile aggiungere queste funzionalità:</span><span class="sxs-lookup"><span data-stu-id="4066a-112">You can add these features:</span></span>

1. [<span data-ttu-id="4066a-113">Opzioni di segnalazione avanzata</span><span class="sxs-lookup"><span data-stu-id="4066a-113">Advanced reporting options</span></span>](mobile-engagement-android-advanced-reporting.md)
2. [<span data-ttu-id="4066a-114">Opzioni di segnalazione della posizione</span><span class="sxs-lookup"><span data-stu-id="4066a-114">Location Reporting options</span></span>](mobile-engagement-android-location-reporting.md)
3. [<span data-ttu-id="4066a-115">Opzioni di configurazione avanzate</span><span class="sxs-lookup"><span data-stu-id="4066a-115">Advanced Configuration options</span></span>](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a><span data-ttu-id="4066a-116">Notifiche:</span><span class="sxs-lookup"><span data-stu-id="4066a-116">Notifications:</span></span>
[<span data-ttu-id="4066a-117">Come toointegrate Reach (notifiche) nell'app Android</span><span class="sxs-lookup"><span data-stu-id="4066a-117">How toointegrate Reach (Notifications) in your Android app</span></span>](mobile-engagement-android-integrate-engagement-reach.md)

1. <span data-ttu-id="4066a-118">Google Cloud Messaging (GCM): [come tooIntegrate GCM con Engagement Mobile](mobile-engagement-android-gcm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="4066a-118">Google Cloud Messaging (GCM): [How tooIntegrate GCM with Mobile Engagement](mobile-engagement-android-gcm-integrate.md)</span></span>
2. <span data-ttu-id="4066a-119">Amazon Device Messaging (ADM): [come tooIntegrate ADM con Engagement Mobile](mobile-engagement-android-adm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="4066a-119">Amazon Device Messaging (ADM): [How tooIntegrate ADM with Mobile Engagement](mobile-engagement-android-adm-integrate.md)</span></span>

### <a name="tag-plan-implementation"></a><span data-ttu-id="4066a-120">Implementazione del piano di tag:</span><span class="sxs-lookup"><span data-stu-id="4066a-120">Tag plan implementation:</span></span>
[<span data-ttu-id="4066a-121">Come toouse hello avanzate tag API nell'app Android di Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="4066a-121">How toouse hello advanced Mobile Engagement tagging API in your Android app</span></span>](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a><span data-ttu-id="4066a-122">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="4066a-122">Release notes</span></span>

### <a name="431-07172017"></a><span data-ttu-id="4066a-123">4.3.1 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="4066a-123">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="4066a-124">Correzione di un arresto anomalo che poteva verificarsi raramente quando si chiama `EngagementAgentUtils.isInDedicatedEngagementProcess`, che viene utilizzato anche dal hello `EngagementApplication` classe.</span><span class="sxs-lookup"><span data-stu-id="4066a-124">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by hello `EngagementApplication` class.</span></span>

### <a name="430-06272017"></a><span data-ttu-id="4066a-125">4.3.0 (06/27/2017)</span><span class="sxs-lookup"><span data-stu-id="4066a-125">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="4066a-126">Supporto Android 8 (versioni precedenti del SDK non funziona in 8 Android hello).</span><span class="sxs-lookup"><span data-stu-id="4066a-126">Android 8 support (previous versions of hello SDK will not work on Android 8).</span></span>
* <span data-ttu-id="4066a-127">Nessuna dipendenza nella raccolta di supporto.</span><span class="sxs-lookup"><span data-stu-id="4066a-127">No more dependency on support library.</span></span>
* <span data-ttu-id="4066a-128">Rimuovere la classe `EngagementFragmentActivity`.</span><span class="sxs-lookup"><span data-stu-id="4066a-128">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="4066a-129">Scadenza troppo[limiti di esecuzione in Background](https://developer.android.com/preview/features/background.html) in Android 8, i log in background potrebbero subire un ritardo fino a quando non hello utente interagisce con dispositivi hello, ciò avrà un impatto sulla campagna Push **consegnati** e **Notifica di sistema visualizzata** statistiche viene ritardate se è stato sospeso dispositivo hello (notifica hello verranno comunque visualizzata, verrà dell'anello e vibrare in tempo reale senza problemi).</span><span class="sxs-lookup"><span data-stu-id="4066a-129">Due too[Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until hello user interacts with hello device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if hello device was sleeping (hello notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="4066a-130">Scadenza troppo[Background percorso limiti](https://developer.android.com/preview/features/background-location-limits.html), posizione in tempo reale hello in background non verranno aggiornati frequentemente in Android 8.</span><span class="sxs-lookup"><span data-stu-id="4066a-130">Due too[Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), hello real time location in background will not be updated frequently on Android 8.</span></span>

<span data-ttu-id="4066a-131">Per tutte le versioni, vedere hello [completare note sulla versione](mobile-engagement-android-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="4066a-131">For all versions, see hello [complete release notes](mobile-engagement-android-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="4066a-132">Procedure di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="4066a-132">Upgrade procedures</span></span>
<span data-ttu-id="4066a-133">Se è già stata integrata una versione precedente di Windows SDK nell'applicazione, vedere le [procedure di aggiornamento](mobile-engagement-android-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="4066a-133">If you already have integrated an older version of our SDK into your application, consult [Upgrade Procedures](mobile-engagement-android-upgrade-procedure.md).</span></span>

