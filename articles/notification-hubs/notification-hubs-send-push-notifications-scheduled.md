---
title: Informazioni su come inviare notifiche pianificate | Microsoft Docs
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
ms.openlocfilehash: efac6e1ecc00359f1622d380333140bc055c83e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-send-scheduled-notifications"></a><span data-ttu-id="25474-104">Procedura: Inviare le notifiche pianificate</span><span class="sxs-lookup"><span data-stu-id="25474-104">How To: Send scheduled notifications</span></span>
## <a name="overview"></a><span data-ttu-id="25474-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="25474-105">Overview</span></span>
<span data-ttu-id="25474-106">Si consideri uno scenario in cui si desidera inviare una notifica in un certo momento in futuro, ma non si dispone di una soluzione semplice per riattivare il codice di back-end per l'invio della notifica.</span><span class="sxs-lookup"><span data-stu-id="25474-106">If you have a scenario in which you want to send a notification at some point in the future, but do not have an easy way to wake up your back-end code to send the notification.</span></span> <span data-ttu-id="25474-107">Il livello Standard Hub di notifica supporta una funzionalità che consente di pianificare le notifiche fino a 7 giorni prima dell'invio.</span><span class="sxs-lookup"><span data-stu-id="25474-107">Standard tier Notification Hubs supports a feature that enables you to schedule notifications up to 7 days in the future.</span></span>

<span data-ttu-id="25474-108">Per l'invio di una notifica è sufficiente usare la classe [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) classe nell'SDK di Hub di notifica, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="25474-108">When sending a notification, simply use the [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) class in the Notification Hubs SDK as shown in the following example:</span></span>

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

<span data-ttu-id="25474-109">È anche possibile annullare una notifica pianificata in precedenza usando il relativo notificationId:</span><span class="sxs-lookup"><span data-stu-id="25474-109">Also, you can cancel a previously scheduled notification using its notificationId:</span></span>

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

<span data-ttu-id="25474-110">Non sono previsti limiti al numero di notifiche pianificate che è possibile inviare.</span><span class="sxs-lookup"><span data-stu-id="25474-110">There are no limits on the number of scheduled notifications you can send.</span></span>

