---
title: Contenuto dell'SDK per app di Windows universali
description: Informazioni sul contenuto di Azure Mobile Engagement SDK per app di Windows universali
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
ms.openlocfilehash: b28d525ab16487b963772e23fdecd11f94dcabd1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-sdk-content"></a><span data-ttu-id="a8976-103">Contenuto dell'SDK per app di Windows universali</span><span class="sxs-lookup"><span data-stu-id="a8976-103">Windows Universal Apps SDK content</span></span>
<span data-ttu-id="a8976-104">Questo documento elenca e descrive il contenuto distribuito dall'SDK nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a8976-104">This document lists and describes the content deployed by the SDK in your application.</span></span>

## <a name="the-resources-folder"></a><span data-ttu-id="a8976-105">Cartella `/Resources`</span><span class="sxs-lookup"><span data-stu-id="a8976-105">The `/Resources` folder</span></span>
<span data-ttu-id="a8976-106">Questa cartella contiene tutte le risorse richieste da Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a8976-106">This folder contains all the resources that Mobile Engagement needs.</span></span> <span data-ttu-id="a8976-107">È inoltre possibile personalizzarle in modo da adattarle all'app.</span><span class="sxs-lookup"><span data-stu-id="a8976-107">You can also customize them to fit your app.</span></span>

* <span data-ttu-id="a8976-108">`EngagementConfiguration.xml` : il file di configurazione di Mobile Engagement, in cui è possibile personalizzare le impostazioni di Mobile Engagement (stringa di connessione di Mobile Engagement, segnalazione di arresto anomalo e così via).</span><span class="sxs-lookup"><span data-stu-id="a8976-108">`EngagementConfiguration.xml` : The Mobile Engagement's configuration file, this is where you can customize Mobile Engagement settings (Mobile Engagement connection string, report crash...).</span></span>

### <a name="html-folder"></a><span data-ttu-id="a8976-109">Cartella /html</span><span class="sxs-lookup"><span data-stu-id="a8976-109">/html folder</span></span>
* <span data-ttu-id="a8976-110">`EngagementNotification.html` : la progettazione HTML per la visualizzazione Web di `Notification` in banner in-app.</span><span class="sxs-lookup"><span data-stu-id="a8976-110">`EngagementNotification.html` : The `Notification` web view html design for in-app banners.</span></span>
* <span data-ttu-id="a8976-111">`EngagementAnnouncement.html` : la progettazione HTML per la visualizzazione Web di `Announcement` in visualizzazioni intermedie.</span><span class="sxs-lookup"><span data-stu-id="a8976-111">`EngagementAnnouncement.html` : The `Announcement` web view html design for in-app interstitial views.</span></span>

### <a name="images-folder"></a><span data-ttu-id="a8976-112">Cartella /images</span><span class="sxs-lookup"><span data-stu-id="a8976-112">/images folder</span></span>
* <span data-ttu-id="a8976-113">`EngagementIconNotification.png`: l'icona del marchio visualizzata a sinistra di una notifica. Sostituirla con un'icona personalizzata.</span><span class="sxs-lookup"><span data-stu-id="a8976-113">`EngagementIconNotification.png` : The brand icon displayed at the left of a notification, replace this one by your brand icon.</span></span>
* <span data-ttu-id="a8976-114">`EngagementIconOk.png`: l'icona `Ok` delle pagine di contenuto Reach per il pulsante di azione o convalida.</span><span class="sxs-lookup"><span data-stu-id="a8976-114">`EngagementIconOk.png` : The `Ok` icon of the reach content pages for the action or validation button.</span></span>
* <span data-ttu-id="a8976-115">`EngagementIconNOK.png`: l'icona `NOK` usata quando il pulsante di convalida delle pagine di contenuto Reach è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="a8976-115">`EngagementIconNOK.png` : The `NOK` icon used when the validation button of the reach content pages is disabled.</span></span>
* <span data-ttu-id="a8976-116">`EngagementIconClose.png`: l'icona `Close` per il pulsante che consente di ignorare il contenuto e le notifiche Reach.</span><span class="sxs-lookup"><span data-stu-id="a8976-116">`EngagementIconClose.png` : The `Close` icon of the reach notifications and contents for the dismiss button.</span></span>

### <a name="overlay-folder"></a><span data-ttu-id="a8976-117">Cartella /overlay</span><span class="sxs-lookup"><span data-stu-id="a8976-117">/overlay folder</span></span>
* <span data-ttu-id="a8976-118">`EngagementPageOverlay.cs` : la pagina di sovrimpressione che determina l'aggiunta dell'interfaccia utente in-app Reach di Engagement al figlio.</span><span class="sxs-lookup"><span data-stu-id="a8976-118">`EngagementPageOverlay.cs` : The overlay page responsible for adding the Engagement reach in-app UI to its child.</span></span>

