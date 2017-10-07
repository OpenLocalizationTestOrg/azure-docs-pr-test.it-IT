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
# <a name="windows-universal-apps-sdk-content"></a>Contenuto dell'SDK per app di Windows universali
Questo documento elenca e descrive il contenuto di hello hello SDK nell'applicazione distribuito.

## <a name="hello-resources-folder"></a>Hello `/Resources` cartella
Questa cartella contiene tutte le risorse di hello che necessita di Mobile Engagement. È inoltre possibile personalizzare tali toofit l'app.

* `EngagementConfiguration.xml`: il file di configurazione di Mobile Engagement hello, si tratta in cui è possibile personalizzare le impostazioni di Mobile Engagement (stringa di connessione di Mobile Engagement, arresto anomalo di report...).

### <a name="html-folder"></a>Cartella /html
* `EngagementNotification.html`: hello `Notification` visualizzazione di progettazione html per le intestazioni nell'applicazione web.
* `EngagementAnnouncement.html`: hello `Announcement` visualizzazione di progettazione html per le viste intermedi nell'applicazione web.

### <a name="images-folder"></a>Cartella /images
* `EngagementIconNotification.png`: icona di marchio hello in hello sinistra di una notifica, sostituire quello attuale per l'icona del marchio.
* `EngagementIconOk.png`: hello `Ok` icona hello reach pagine di contenuto per i pulsanti di azione o convalida hello.
* `EngagementIconNOK.png`: hello `NOK` icona utilizzata quando il pulsante convalida hello hello reach pagine di contenuto è disabilitato.
* `EngagementIconClose.png`: hello `Close` icona di hello raggiungere le notifiche e contenuto per hello chiudere pulsante.

### <a name="overlay-folder"></a>Cartella /overlay
* `EngagementPageOverlay.cs`: hello sovrapposizione pagina responsabile dell'aggiunta hello copertura di Engagement figlio tooits di interfaccia utente nell'applicazione.

