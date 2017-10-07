---
title: aaaWindows contenuto Universal App SDK
description: Contiene informazioni sul contenuto hello di hello Windows Universal App SDK per Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8fa1b701-1c2b-4aec-940c-06c974ef5405
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a8013d2433c0be62d737c8bc6e8360ed79bbe532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-content"></a><span data-ttu-id="6e058-103">Contenuto dell'SDK per app di Windows universali</span><span class="sxs-lookup"><span data-stu-id="6e058-103">Windows Universal Apps SDK content</span></span>
<span data-ttu-id="6e058-104">Questo documento elenca e descrive il contenuto di hello hello SDK nell'applicazione distribuito.</span><span class="sxs-lookup"><span data-stu-id="6e058-104">This document lists and describes hello content deployed by hello SDK in your application.</span></span>

## <a name="hello-resources-folder"></a><span data-ttu-id="6e058-105">Hello `/Resources` cartella</span><span class="sxs-lookup"><span data-stu-id="6e058-105">hello `/Resources` folder</span></span>
<span data-ttu-id="6e058-106">Questa cartella contiene tutte le risorse di hello che necessita di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="6e058-106">This folder contains all hello resources that Mobile Engagement needs.</span></span> <span data-ttu-id="6e058-107">È inoltre possibile personalizzare tali toofit l'app.</span><span class="sxs-lookup"><span data-stu-id="6e058-107">You can also customize them toofit your app.</span></span>

* <span data-ttu-id="6e058-108">`EngagementConfiguration.xml`: il file di configurazione di Mobile Engagement hello, si tratta in cui è possibile personalizzare le impostazioni di Mobile Engagement (stringa di connessione di Mobile Engagement, arresto anomalo di report...).</span><span class="sxs-lookup"><span data-stu-id="6e058-108">`EngagementConfiguration.xml` : hello Mobile Engagement's configuration file, this is where you can customize Mobile Engagement settings (Mobile Engagement connection string, report crash...).</span></span>

### <a name="html-folder"></a><span data-ttu-id="6e058-109">Cartella /html</span><span class="sxs-lookup"><span data-stu-id="6e058-109">/html folder</span></span>
* <span data-ttu-id="6e058-110">`EngagementNotification.html`: hello `Notification` visualizzazione di progettazione html per le intestazioni nell'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="6e058-110">`EngagementNotification.html` : hello `Notification` web view html design for in-app banners.</span></span>
* <span data-ttu-id="6e058-111">`EngagementAnnouncement.html`: hello `Announcement` visualizzazione di progettazione html per le viste intermedi nell'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="6e058-111">`EngagementAnnouncement.html` : hello `Announcement` web view html design for in-app interstitial views.</span></span>

### <a name="images-folder"></a><span data-ttu-id="6e058-112">Cartella /images</span><span class="sxs-lookup"><span data-stu-id="6e058-112">/images folder</span></span>
* <span data-ttu-id="6e058-113">`EngagementIconNotification.png`: icona di marchio hello in hello sinistra di una notifica, sostituire quello attuale per l'icona del marchio.</span><span class="sxs-lookup"><span data-stu-id="6e058-113">`EngagementIconNotification.png` : hello brand icon displayed at hello left of a notification, replace this one by your brand icon.</span></span>
* <span data-ttu-id="6e058-114">`EngagementIconOk.png`: hello `Ok` icona hello reach pagine di contenuto per i pulsanti di azione o convalida hello.</span><span class="sxs-lookup"><span data-stu-id="6e058-114">`EngagementIconOk.png` : hello `Ok` icon of hello reach content pages for hello action or validation button.</span></span>
* <span data-ttu-id="6e058-115">`EngagementIconNOK.png`: hello `NOK` icona utilizzata quando il pulsante convalida hello hello reach pagine di contenuto è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="6e058-115">`EngagementIconNOK.png` : hello `NOK` icon used when hello validation button of hello reach content pages is disabled.</span></span>
* <span data-ttu-id="6e058-116">`EngagementIconClose.png`: hello `Close` icona di hello raggiungere le notifiche e contenuto per hello chiudere pulsante.</span><span class="sxs-lookup"><span data-stu-id="6e058-116">`EngagementIconClose.png` : hello `Close` icon of hello reach notifications and contents for hello dismiss button.</span></span>

### <a name="overlay-folder"></a><span data-ttu-id="6e058-117">Cartella /overlay</span><span class="sxs-lookup"><span data-stu-id="6e058-117">/overlay folder</span></span>
* <span data-ttu-id="6e058-118">`EngagementPageOverlay.cs`: hello sovrapposizione pagina responsabile dell'aggiunta hello copertura di Engagement figlio tooits di interfaccia utente nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6e058-118">`EngagementPageOverlay.cs` : hello overlay page responsible for adding hello Engagement reach in-app UI tooits child.</span></span>

