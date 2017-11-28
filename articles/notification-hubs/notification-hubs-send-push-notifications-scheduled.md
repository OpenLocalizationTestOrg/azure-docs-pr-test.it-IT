---
title: aaaHow toosend pianificata notifiche | Documenti Microsoft
description: Questo argomento descrive l'uso di notifiche pianificate con Hub di notifica.
services: notification-hubs
documentationcenter: .net
keywords: notifiche push, notifica push, pianificazione notifiche push
author: ysxu
manager: erikre
editor: 
ms.assetid: 6b718c75-75dd-4c99-aee3-db1288235c1a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 9b3ba715dad6f5d824a615e83f2863b0db47b533
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-send-scheduled-notifications"></a><span data-ttu-id="c7c19-104">Procedura: Inviare le notifiche pianificate</span><span class="sxs-lookup"><span data-stu-id="c7c19-104">How To: Send scheduled notifications</span></span>
## <a name="overview"></a><span data-ttu-id="c7c19-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c7c19-105">Overview</span></span>
<span data-ttu-id="c7c19-106">Se si dispone di uno scenario in cui si desidera una notifica a un certo punto in hello toosend futuri, ma non è un modo semplice di toowake notifiche di hello toosend il codice di back-end di.</span><span class="sxs-lookup"><span data-stu-id="c7c19-106">If you have a scenario in which you want toosend a notification at some point in hello future, but do not have an easy way toowake up your back-end code toosend hello notification.</span></span> <span data-ttu-id="c7c19-107">Livello standard hub di notifica supporta una funzionalità che consente di notifiche tooschedule dei giorni too7 hello future.</span><span class="sxs-lookup"><span data-stu-id="c7c19-107">Standard tier Notification Hubs supports a feature that enables you tooschedule notifications up too7 days in hello future.</span></span>

<span data-ttu-id="c7c19-108">Quando si invia una notifica, è sufficiente usare hello [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) classe hello SDK hub di notifica, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="c7c19-108">When sending a notification, simply use hello [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) class in hello Notification Hubs SDK as shown in hello following example:</span></span>

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

<span data-ttu-id="c7c19-109">È anche possibile annullare una notifica pianificata in precedenza usando il relativo notificationId:</span><span class="sxs-lookup"><span data-stu-id="c7c19-109">Also, you can cancel a previously scheduled notification using its notificationId:</span></span>

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

<span data-ttu-id="c7c19-110">Non sono previsti limiti al numero di hello di notifiche pianificate che è possibile inviare.</span><span class="sxs-lookup"><span data-stu-id="c7c19-110">There are no limits on hello number of scheduled notifications you can send.</span></span>

