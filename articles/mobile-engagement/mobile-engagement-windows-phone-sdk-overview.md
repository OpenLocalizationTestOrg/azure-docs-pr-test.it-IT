---
title: Panoramica di Mobile Engagement Windows Phone Silverlight SDK aaaAzure | Documenti Microsoft
description: Panoramica di hello Windows Phone Silverlight SDK per Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0e3d2420-0509-4952-8891-392e3dad9aaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: ff2febed2202127e0538373ebbabe674993ce39d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-overview-for-azure-mobile-engagement"></a>Panoramica di Azure Mobile Engagement SDK per Windows Phone Silverlight
Iniziare da qui i dettagli di hello tooget sulla toointegrate Azure Mobile Engagement in un'App di Windows Phone Silverlight. Se si desidera toogive è un blocco try, assicurarsi innanzitutto completare il nostro [esercitazione di 15 minuti](mobile-engagement-windows-phone-get-started.md).

Fare clic su hello toosee [contenuto SDK](mobile-engagement-windows-phone-sdk-content.md)

## <a name="integration-procedures"></a>Procedure di integrazione
1. Iniziare da qui: [come toointegrate Mobile Engagement nell'app Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
2. Per le notifiche: [come toointegrate Reach (notifiche) nell'app Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement-reach.md)
3. Implementazione del piano di tag: [come toouse hello avanzate tag API nelle applicazioni Windows Phone Silverlight di Mobile Engagement](mobile-engagement-windows-phone-use-engagement-api.md)

## <a name="release-notes"></a>Note sulla versione
###<a name="331-11032016"></a>3.3.1 (11/03/2016)
Parte di hello *MicrosoftAzure.MobileEngagement* pacchetto Nuget **v3.4.1**

* Miglioramenti della stabilità.

Per la versione precedente, vedere hello [completare note sulla versione](mobile-engagement-windows-phone-release-notes.md)

## <a name="upgrade-procedures"></a>Procedure di aggiornamento
Se è già stata integrata una versione precedente di Windows SDK nell'applicazione, è necessario hello tooconsider seguenti punti quando si aggiorna hello SDK.

È possibile toofollow varie procedure se sono saltate diverse versioni di hello SDK. Vedere hello completo [le procedure di aggiornamento](mobile-engagement-windows-phone-upgrade-procedure.md). Ad esempio se si esegue la migrazione da 0.10.1 too0.11.0 è toofirst seguire hello "da 0.9.0 too0.10.1" routine quindi hello "da 0.10.1 too0.11.0" stored procedure.

### <a name="from-200-too330"></a>Da 2.0.0 too3.3.0
#### <a name="test-logs"></a>Log di test
Registri della console prodotti da hello SDK ora possono essere attivato/disattivato/filtrato. toocustomize, questa proprietà hello aggiornamento `EngagementAgent.Instance.TestLogEnabled` tooone del valore di hello disponibile hello `EngagementTestLogLevel` enumerazione, ad esempio:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="upgrade-from-older-versions"></a>Eseguire l'aggiornamento da versioni precedenti
Vedere [Upgrade Procedures](mobile-engagement-windows-phone-upgrade-procedure.md)

