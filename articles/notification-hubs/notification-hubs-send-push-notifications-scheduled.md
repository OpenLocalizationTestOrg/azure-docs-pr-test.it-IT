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
# <a name="how-to-send-scheduled-notifications"></a>Procedura: Inviare le notifiche pianificate
## <a name="overview"></a>Panoramica
Se si dispone di uno scenario in cui si desidera una notifica a un certo punto in hello toosend futuri, ma non è un modo semplice di toowake notifiche di hello toosend il codice di back-end di. Livello standard hub di notifica supporta una funzionalità che consente di notifiche tooschedule dei giorni too7 hello future.

Quando si invia una notifica, è sufficiente usare hello [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) classe hello SDK hub di notifica, come illustrato nell'esempio seguente hello:

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

È anche possibile annullare una notifica pianificata in precedenza usando il relativo notificationId:

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

Non sono previsti limiti al numero di hello di notifiche pianificate che è possibile inviare.

