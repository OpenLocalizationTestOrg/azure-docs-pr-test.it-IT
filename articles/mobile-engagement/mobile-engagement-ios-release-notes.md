---
title: aaaAzure Engagement Mobile iOS note sulla versione di SDK | Documenti Microsoft
description: Ultimi aggiornamenti e procedure relativi a iOS SDK per Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a43ff0f6-90d5-4b3c-8d7a-a1db21bc776b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: ae29d200ebb1784357b29edbd1f66b71df0778cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a><span data-ttu-id="bab6c-103">Note sulla versione di Azure Mobile Engagement iOS SDK</span><span class="sxs-lookup"><span data-stu-id="bab6c-103">Azure Mobile Engagement iOS SDK release notes</span></span>

## <a name="410-07172017"></a><span data-ttu-id="bab6c-104">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="bab6c-104">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="bab6c-105">Risolto il problema delle notifiche cancellate in background.</span><span class="sxs-lookup"><span data-stu-id="bab6c-105">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="bab6c-106">Risolto il problema degli avvisi in XCode 9 sulle API non chiamate nella coda principale.</span><span class="sxs-lookup"><span data-stu-id="bab6c-106">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="bab6c-107">Risolto un problema di memoria nei poll di copertura.</span><span class="sxs-lookup"><span data-stu-id="bab6c-107">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="bab6c-108">Eliminazione del supporto per iOS 6.X.</span><span class="sxs-lookup"><span data-stu-id="bab6c-108">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="bab6c-109">A partire da questa destinazione di distribuzione hello versione dell'applicazione deve essere almeno iOS 7.</span><span class="sxs-lookup"><span data-stu-id="bab6c-109">Starting from this version hello deployment target of your application must be at least iOS 7.</span></span>

## <a name="401-12132016"></a><span data-ttu-id="bab6c-110">4.0.1 (12/13/2016)</span><span class="sxs-lookup"><span data-stu-id="bab6c-110">4.0.1 (12/13/2016)</span></span>
* <span data-ttu-id="bab6c-111">Recapito del log migliorato in background.</span><span class="sxs-lookup"><span data-stu-id="bab6c-111">Improved log delivery in background.</span></span>

## <a name="400-09122016"></a><span data-ttu-id="bab6c-112">4.0.0 (12/09/2016)</span><span class="sxs-lookup"><span data-stu-id="bab6c-112">4.0.0 (09/12/2016)</span></span>
* <span data-ttu-id="bab6c-113">Risolto il problema delle notifiche non prese in considerazione sui dispositivi iOS 10.</span><span class="sxs-lookup"><span data-stu-id="bab6c-113">Fixed notification not actioned on iOS 10 devices.</span></span>
* <span data-ttu-id="bab6c-114">Deprecare XCode 7.</span><span class="sxs-lookup"><span data-stu-id="bab6c-114">Deprecate XCode 7.</span></span>

## <a name="324-06302016"></a><span data-ttu-id="bab6c-115">3.2.4 (30/06/2016)</span><span class="sxs-lookup"><span data-stu-id="bab6c-115">3.2.4 (06/30/2016)</span></span>
* <span data-ttu-id="bab6c-116">Aggregazione fissa tra log tecnici e altri log.</span><span class="sxs-lookup"><span data-stu-id="bab6c-116">Fixed aggregation between technical logs and other logs.</span></span>

## <a name="323-06072016"></a><span data-ttu-id="bab6c-117">3.2.3 (07/06/2016)</span><span class="sxs-lookup"><span data-stu-id="bab6c-117">3.2.3 (06/07/2016)</span></span>
* <span data-ttu-id="bab6c-118">Commenti e suggerimenti di recapito in cui non viene segnalato quando l'app è in background hello bug di hello fisso.</span><span class="sxs-lookup"><span data-stu-id="bab6c-118">Fixed hello bug where delivery feedback is not reported when app is in hello background.</span></span>
* <span data-ttu-id="bab6c-119">Hello ottimizzato l'invio dei log tecniche.</span><span class="sxs-lookup"><span data-stu-id="bab6c-119">Optimized hello sending of technical logs.</span></span>

## <a name="322-04072016"></a><span data-ttu-id="bab6c-120">3.2.2 (07/04/2016)</span><span class="sxs-lookup"><span data-stu-id="bab6c-120">3.2.2 (04/07/2016)</span></span>
* <span data-ttu-id="bab6c-121">Annullamento di richiesta HTTP con un conseguente talvolta toocrash correzione del bug.</span><span class="sxs-lookup"><span data-stu-id="bab6c-121">Fixed bug on HTTP request cancellation which sometimes leads toocrash.</span></span>

## <a name="321-12112015"></a><span data-ttu-id="bab6c-122">3.2.1 (12/11/2015)</span><span class="sxs-lookup"><span data-stu-id="bab6c-122">3.2.1 (12/11/2015)</span></span>
* <span data-ttu-id="bab6c-123">Ritardo hello predefinito quando viene attivata una nuova istanza di applicazione da una notifica con collegamenti diretti</span><span class="sxs-lookup"><span data-stu-id="bab6c-123">Fixed hello delay when a new app instance is triggered by a notification with deep links</span></span>

## <a name="320-10082015"></a><span data-ttu-id="bab6c-124">3.2.0 (10/08/2015)</span><span class="sxs-lookup"><span data-stu-id="bab6c-124">3.2.0 (10/08/2015)</span></span>
* <span data-ttu-id="bab6c-125">Abilitato Bitcode in hello SDK toomake funziona con **Xcode 7**.</span><span class="sxs-lookup"><span data-stu-id="bab6c-125">Enabled Bitcode in hello SDK toomake it work with **Xcode 7**.</span></span>
* <span data-ttu-id="bab6c-126">Bug risolti correlati notifiche tooin-app.</span><span class="sxs-lookup"><span data-stu-id="bab6c-126">Fixed bugs related tooin-app notifications.</span></span>
* <span data-ttu-id="bab6c-127">Apportate le notifiche in-app hello più affidabile in caso di batteria in esaurimento e altri scenari di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="bab6c-127">Made hello in-app notifications more reliable in case of low battery and other such scenarios.</span></span>
* <span data-ttu-id="bab6c-128">Rimossi i registri aggiuntivi della console generati dalla libreria di terze parti 3.</span><span class="sxs-lookup"><span data-stu-id="bab6c-128">Removed extra console logs generated by 3rd party library.</span></span>

## <a name="310-08262015"></a><span data-ttu-id="bab6c-129">3.1.0 (08/26/2015)</span><span class="sxs-lookup"><span data-stu-id="bab6c-129">3.1.0 (08/26/2015)</span></span>
* <span data-ttu-id="bab6c-130">Correzione del bug di compatibilità di iOS 9 con una libreria di terze parti.</span><span class="sxs-lookup"><span data-stu-id="bab6c-130">Fix iOS 9 compatibility bug with a third party library.</span></span> <span data-ttu-id="bab6c-131">Provocava arresti anomali durante l'invio del polling dei risultati, di informazioni sull'applicazione o di dati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="bab6c-131">It was causing crashes while sending polls results, application information or extra data.</span></span>

## <a name="300-06192015"></a><span data-ttu-id="bab6c-132">3.0.0 (19/06/2015)</span><span class="sxs-lookup"><span data-stu-id="bab6c-132">3.0.0 (06/19/2015)</span></span>
* <span data-ttu-id="bab6c-133">Mobile Enagement usa le notifiche push Silent.</span><span class="sxs-lookup"><span data-stu-id="bab6c-133">Mobile Engagement uses Silent Push Notifications.</span></span>
* <span data-ttu-id="bab6c-134">Eliminazione del supporto per iOS 4.X.</span><span class="sxs-lookup"><span data-stu-id="bab6c-134">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="bab6c-135">A partire da questa destinazione di distribuzione hello versione dell'applicazione deve essere almeno iOS 6.</span><span class="sxs-lookup"><span data-stu-id="bab6c-135">Starting from this version hello deployment target of your application must be at least iOS 6.</span></span>

## <a name="220-05212015"></a><span data-ttu-id="bab6c-136">2.2.0 (21/05/2015)</span><span class="sxs-lookup"><span data-stu-id="bab6c-136">2.2.0 (05/21/2015)</span></span>
* <span data-ttu-id="bab6c-137">id del dispositivo Mobile Engagement Hello per i dispositivi < iOS 6 è basata su un GUID generato in fase di installazione.</span><span class="sxs-lookup"><span data-stu-id="bab6c-137">hello Mobile Engagement device id for devices < iOS 6 is now based on a GUID generated at installation time.</span></span>

## <a name="210-04242015"></a><span data-ttu-id="bab6c-138">2.1.0 (24/04/2015)</span><span class="sxs-lookup"><span data-stu-id="bab6c-138">2.1.0 (04/24/2015)</span></span>
* <span data-ttu-id="bab6c-139">È stata aggiunta la compatibilità per Swift.</span><span class="sxs-lookup"><span data-stu-id="bab6c-139">Added Swift compatibility.</span></span>
* <span data-ttu-id="bab6c-140">Quando si fa clic su una notifica, l'azione hello che URL viene ora eseguita destra dopo l'apertura di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="bab6c-140">When clicking on a notification, hello action URL is now executed right after hello application is opened.</span></span>
* <span data-ttu-id="bab6c-141">È stato aggiunto il file di intestazione mancante nel pacchetto dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="bab6c-141">Added missing header file in SDK package.</span></span>
* <span data-ttu-id="bab6c-142">Risolto un problema quando reporter di arresto anomalo di Mobile Engagement hello è stato disabilitato.</span><span class="sxs-lookup"><span data-stu-id="bab6c-142">Fixed an issue when hello Mobile Engagement crash reporter was disabled.</span></span>

## <a name="200-02172015"></a><span data-ttu-id="bab6c-143">2.0.0 (17/02/2015)</span><span class="sxs-lookup"><span data-stu-id="bab6c-143">2.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="bab6c-144">Versione iniziale di Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="bab6c-144">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="bab6c-145">La configurazione di appId/sdkKey viene sostituita da una configurazione della stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="bab6c-145">appId/sdkKey configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="bab6c-146">Rimosso toosend API e ricevere messaggi XMPP arbitrari da entità XMPP arbitraria.</span><span class="sxs-lookup"><span data-stu-id="bab6c-146">Removed API toosend and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="bab6c-147">Rimosso toosend API e ricevere messaggi tra i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="bab6c-147">Removed API toosend and receive messages between devices.</span></span>
* <span data-ttu-id="bab6c-148">Sono stati introdotti miglioramenti per la sicurezza.</span><span class="sxs-lookup"><span data-stu-id="bab6c-148">Security improvements.</span></span>
* <span data-ttu-id="bab6c-149">È stato eliminato il rilevamento di SmartAd.</span><span class="sxs-lookup"><span data-stu-id="bab6c-149">SmartAd tracking removed.</span></span>
