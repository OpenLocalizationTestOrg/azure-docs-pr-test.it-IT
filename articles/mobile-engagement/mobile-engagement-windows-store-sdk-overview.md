---
title: aaaAzure Mobile Engagement Universal integrazione con Windows SDK | Documenti Microsoft
description: Integrazione di Windows Universal per SDK per Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ded187d-5c07-4377-a41c-ce205dd38b50
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: 2f88e58adb349a2a4eb43b0f182f99b3e8b8cfd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-sdk-integration-for-azure-mobile-engagement"></a>Integrazione di Windows Universal SDK per Azure Mobile Engagement
Questo documento descrive tutti hello integration e opzioni di configurazione disponibili per Azure Mobile Engagement SDK Universal Windows hello.

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione, è necessario completare l' [esercitazione di 15 minuti](mobile-engagement-windows-store-dotnet-get-started.md).

## <a name="advanced-features"></a>Funzionalità avanzate
### <a name="reporting-features"></a>Funzionalità di segnalazione
È possibile aggiungere queste funzionalità:

1. [Opzioni di segnalazione avanzata](mobile-engagement-windows-store-advanced-reporting.md)
2. [Opzioni di configurazione avanzate](mobile-engagement-windows-store-advanced-configuration.md)

### <a name="notifications"></a>Notifiche
[Come toointegrate Reach (notifiche) nell'app universali di Windows](mobile-engagement-windows-store-integrate-engagement-reach.md)

### <a name="tag-plan-implementation"></a>Implementazione del piano di tag:
[Come toouse hello avanzate Mobile Engagement tag API in app universali di Windows](mobile-engagement-windows-store-use-engagement-api.md)

## <a name="release-notes"></a>Note sulla versione
### <a name="341-11032016"></a>3.4.1 (11/03/2016)

* Miglioramenti della stabilità.

Per le versioni precedenti, vedere hello [completare note sulla versione](mobile-engagement-windows-store-release-notes.md)

## <a name="upgrade-procedures"></a>Procedure di aggiornamento
Se è già stata integrata una versione precedente di Engagement all'interno dell'applicazione, è necessario hello tooconsider seguenti punti quando si aggiorna hello SDK.

Se si perde diverse versioni di hello SDK, è possibile toofollow diverse procedure. Vedere hello completo [le procedure di aggiornamento](mobile-engagement-windows-store-upgrade-procedure.md). Ad esempio se si esegue la migrazione da 0.10.1 too0.11.0 è toofirst seguire hello "da 0.9.0 too0.10.1" routine quindi hello "da 0.10.1 too0.11.0" stored procedure.

### <a name="from-330-too340"></a>Da 3.3.0 too3.4.0
#### <a name="test-logs"></a>Log di test
Registri della console prodotti da hello SDK ora possono essere attivato/disattivato/filtrato. toocustomize, proprietà hello aggiornamento `EngagementAgent.Instance.TestLogEnabled` tooone valori hello disponibili da hello `EngagementTestLogLevel` enumerazione, ad esempio:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

#### <a name="resources"></a>Risorse
sovrapposizione di copertura Hello è stata migliorata. È parte di risorse del pacchetto NuGet SDK hello.

Durante l'aggiornamento toohello nuova versione di hello SDK, è possibile scegliere che se si desidera tookeep i file esistenti da hello sovrapposizione cartella delle risorse o non:

* Se sovrapposizione precedente hello è alle proprie esigenze, o si sta integrando hello `WebView` elementi manualmente, quindi è possibile decidere tookeep l'uscita da file, continuerà a funzionare.
* sovrapposizione nuovo tooupdate toohello, sostituire hello intero `overlay` cartella dalle risorse con hello uno nuovo dal pacchetto SDK hello (app UWP: dopo l'aggiornamento di hello, è possibile ottenere la nuova cartella sovrapposizione di hello da % USERPROFILE %\\.nuget\packages\ MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).

> [!WARNING]
> Utilizzando una sovrapposizione di nuovo hello sovrascrive tutte le personalizzazioni apportate in una versione precedente di hello.
> 
> 

### <a name="upgrade-from-older-versions"></a>Eseguire l'aggiornamento da versioni precedenti
Vedere [Upgrade Procedures](mobile-engagement-windows-store-upgrade-procedure.md)

