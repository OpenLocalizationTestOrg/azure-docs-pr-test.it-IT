---
title: Note sulla versione di Azure Mobile Engagement iOS SDK | Documentazione Microsoft
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
ms.openlocfilehash: 9bdaa57f9902373ccf796ff109332b64c66bf9e7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a><span data-ttu-id="893d7-103">Note sulla versione di Azure Mobile Engagement iOS SDK</span><span class="sxs-lookup"><span data-stu-id="893d7-103">Azure Mobile Engagement iOS SDK release notes</span></span>

## <a name="410-07172017"></a><span data-ttu-id="893d7-104">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="893d7-104">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="893d7-105">Risolto il problema delle notifiche cancellate in background.</span><span class="sxs-lookup"><span data-stu-id="893d7-105">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="893d7-106">Risolto il problema degli avvisi in XCode 9 sulle API non chiamate nella coda principale.</span><span class="sxs-lookup"><span data-stu-id="893d7-106">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="893d7-107">Risolto un problema di memoria nei poll di copertura.</span><span class="sxs-lookup"><span data-stu-id="893d7-107">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="893d7-108">Eliminazione del supporto per iOS 6.X.</span><span class="sxs-lookup"><span data-stu-id="893d7-108">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="893d7-109">A partire da questa versione, la destinazione della distribuzione dell'applicazione deve essere almeno iOS 7.</span><span class="sxs-lookup"><span data-stu-id="893d7-109">Starting from this version the deployment target of your application must be at least iOS 7.</span></span>

## <a name="401-12132016"></a><span data-ttu-id="893d7-110">4.0.1 (12/13/2016)</span><span class="sxs-lookup"><span data-stu-id="893d7-110">4.0.1 (12/13/2016)</span></span>
* <span data-ttu-id="893d7-111">Recapito del log migliorato in background.</span><span class="sxs-lookup"><span data-stu-id="893d7-111">Improved log delivery in background.</span></span>

## <a name="400-09122016"></a><span data-ttu-id="893d7-112">4.0.0 (12/09/2016)</span><span class="sxs-lookup"><span data-stu-id="893d7-112">4.0.0 (09/12/2016)</span></span>
* <span data-ttu-id="893d7-113">Risolto il problema delle notifiche non prese in considerazione sui dispositivi iOS 10.</span><span class="sxs-lookup"><span data-stu-id="893d7-113">Fixed notification not actioned on iOS 10 devices.</span></span>
* <span data-ttu-id="893d7-114">Deprecare XCode 7.</span><span class="sxs-lookup"><span data-stu-id="893d7-114">Deprecate XCode 7.</span></span>

## <a name="324-06302016"></a><span data-ttu-id="893d7-115">3.2.4 (30/06/2016)</span><span class="sxs-lookup"><span data-stu-id="893d7-115">3.2.4 (06/30/2016)</span></span>
* <span data-ttu-id="893d7-116">Aggregazione fissa tra log tecnici e altri log.</span><span class="sxs-lookup"><span data-stu-id="893d7-116">Fixed aggregation between technical logs and other logs.</span></span>

## <a name="323-06072016"></a><span data-ttu-id="893d7-117">3.2.3 (07/06/2016)</span><span class="sxs-lookup"><span data-stu-id="893d7-117">3.2.3 (06/07/2016)</span></span>
* <span data-ttu-id="893d7-118">Correzione del bug che causava la mancata segnalazione del feedback di recapito con l'applicazione in background.</span><span class="sxs-lookup"><span data-stu-id="893d7-118">Fixed the bug where delivery feedback is not reported when app is in the background.</span></span>
* <span data-ttu-id="893d7-119">Ottimizzazione dell’invio di log tecnici.</span><span class="sxs-lookup"><span data-stu-id="893d7-119">Optimized the sending of technical logs.</span></span>

## <a name="322-04072016"></a><span data-ttu-id="893d7-120">3.2.2 (07/04/2016)</span><span class="sxs-lookup"><span data-stu-id="893d7-120">3.2.2 (04/07/2016)</span></span>
* <span data-ttu-id="893d7-121">Correzione del bug sull'annullamento della richiesta HTTP che a volte provoca l'arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="893d7-121">Fixed bug on HTTP request cancellation which sometimes leads to crash.</span></span>

## <a name="321-12112015"></a><span data-ttu-id="893d7-122">3.2.1 (12/11/2015)</span><span class="sxs-lookup"><span data-stu-id="893d7-122">3.2.1 (12/11/2015)</span></span>
* <span data-ttu-id="893d7-123">Correzione del ritardo durante l’attivazione di una nuova istanza dell’app tramite notifica con collegamenti diretti</span><span class="sxs-lookup"><span data-stu-id="893d7-123">Fixed the delay when a new app instance is triggered by a notification with deep links</span></span>

## <a name="320-10082015"></a><span data-ttu-id="893d7-124">3.2.0 (10/08/2015)</span><span class="sxs-lookup"><span data-stu-id="893d7-124">3.2.0 (10/08/2015)</span></span>
* <span data-ttu-id="893d7-125">Abilitato Bitcode nel SDK per utilizzarlo con **Xcode 7**.</span><span class="sxs-lookup"><span data-stu-id="893d7-125">Enabled Bitcode in the SDK to make it work with **Xcode 7**.</span></span>
* <span data-ttu-id="893d7-126">Bug corretti relativi a notifiche all'interno dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="893d7-126">Fixed bugs related to in-app notifications.</span></span>
* <span data-ttu-id="893d7-127">Apportate le notifiche all'interno dell'app più affidabili in caso di batteria scarica e altri scenari.</span><span class="sxs-lookup"><span data-stu-id="893d7-127">Made the in-app notifications more reliable in case of low battery and other such scenarios.</span></span>
* <span data-ttu-id="893d7-128">Rimossi i registri aggiuntivi della console generati dalla libreria di terze parti 3.</span><span class="sxs-lookup"><span data-stu-id="893d7-128">Removed extra console logs generated by 3rd party library.</span></span>

## <a name="310-08262015"></a><span data-ttu-id="893d7-129">3.1.0 (08/26/2015)</span><span class="sxs-lookup"><span data-stu-id="893d7-129">3.1.0 (08/26/2015)</span></span>
* <span data-ttu-id="893d7-130">Correzione del bug di compatibilità di iOS 9 con una libreria di terze parti.</span><span class="sxs-lookup"><span data-stu-id="893d7-130">Fix iOS 9 compatibility bug with a third party library.</span></span> <span data-ttu-id="893d7-131">Provocava arresti anomali durante l'invio del polling dei risultati, di informazioni sull'applicazione o di dati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="893d7-131">It was causing crashes while sending polls results, application information or extra data.</span></span>

## <a name="300-06192015"></a><span data-ttu-id="893d7-132">3.0.0 (19/06/2015)</span><span class="sxs-lookup"><span data-stu-id="893d7-132">3.0.0 (06/19/2015)</span></span>
* <span data-ttu-id="893d7-133">Mobile Enagement usa le notifiche push Silent.</span><span class="sxs-lookup"><span data-stu-id="893d7-133">Mobile Engagement uses Silent Push Notifications.</span></span>
* <span data-ttu-id="893d7-134">Eliminazione del supporto per iOS 4.X.</span><span class="sxs-lookup"><span data-stu-id="893d7-134">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="893d7-135">A partire da questa versione, la destinazione della distribuzione dell'applicazione deve essere almeno iOS 6.</span><span class="sxs-lookup"><span data-stu-id="893d7-135">Starting from this version the deployment target of your application must be at least iOS 6.</span></span>

## <a name="220-05212015"></a><span data-ttu-id="893d7-136">2.2.0 (21/05/2015)</span><span class="sxs-lookup"><span data-stu-id="893d7-136">2.2.0 (05/21/2015)</span></span>
* <span data-ttu-id="893d7-137">L'ID del dispositivo di Mobile Engagement per dispositivi < iOS 6 è ora basato su un GUID generato in fase di installazione.</span><span class="sxs-lookup"><span data-stu-id="893d7-137">The Mobile Engagement device id for devices < iOS 6 is now based on a GUID generated at installation time.</span></span>

## <a name="210-04242015"></a><span data-ttu-id="893d7-138">2.1.0 (24/04/2015)</span><span class="sxs-lookup"><span data-stu-id="893d7-138">2.1.0 (04/24/2015)</span></span>
* <span data-ttu-id="893d7-139">È stata aggiunta la compatibilità per Swift.</span><span class="sxs-lookup"><span data-stu-id="893d7-139">Added Swift compatibility.</span></span>
* <span data-ttu-id="893d7-140">Quando si fa clic su una notifica, l'URL dell'azione viene ora eseguito subito dopo l'apertura dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="893d7-140">When clicking on a notification, the action URL is now executed right after the application is opened.</span></span>
* <span data-ttu-id="893d7-141">È stato aggiunto il file di intestazione mancante nel pacchetto dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="893d7-141">Added missing header file in SDK package.</span></span>
* <span data-ttu-id="893d7-142">È stato risolto un problema relativo alla disabilitazione del reporter di arresto anomalo di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="893d7-142">Fixed an issue when the Mobile Engagement crash reporter was disabled.</span></span>

## <a name="200-02172015"></a><span data-ttu-id="893d7-143">2.0.0 (17/02/2015)</span><span class="sxs-lookup"><span data-stu-id="893d7-143">2.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="893d7-144">Versione iniziale di Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="893d7-144">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="893d7-145">La configurazione di appId/sdkKey viene sostituita da una configurazione della stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="893d7-145">appId/sdkKey configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="893d7-146">L'API non invia e non riceve più messaggi XMPP da entità XMPP arbitrarie.</span><span class="sxs-lookup"><span data-stu-id="893d7-146">Removed API to send and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="893d7-147">L'API non riceve e non invia più messaggi tra i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="893d7-147">Removed API to send and receive messages between devices.</span></span>
* <span data-ttu-id="893d7-148">Sono stati introdotti miglioramenti per la sicurezza.</span><span class="sxs-lookup"><span data-stu-id="893d7-148">Security improvements.</span></span>
* <span data-ttu-id="893d7-149">È stato eliminato il rilevamento di SmartAd.</span><span class="sxs-lookup"><span data-stu-id="893d7-149">SmartAd tracking removed.</span></span>
