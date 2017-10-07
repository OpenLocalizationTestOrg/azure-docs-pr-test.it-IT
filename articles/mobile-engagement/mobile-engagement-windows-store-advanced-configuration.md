---
title: Configurazione per Windows Universal App Engagement SDK aaaAdvanced
description: Opzioni di configurazione avanzata per Azure Mobile Engagement per app universali di Windows
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6d85dd5d-ac07-43ba-bbe4-e91c3a17690b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 23bd05012bc25d438d8d4985a112280bed0292b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a>Configurazione avanzata per Engagement SDK per app universali di Windows
> [!div class="op_single_selector"]
> * [Windows universale](mobile-engagement-windows-store-advanced-configuration.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-configuration.md)
> 
> 

Questa procedura viene descritto come tooconfigure varie opzioni di configurazione per le app Android di Azure Mobile Engagement.

## <a name="prerequisites"></a>Prerequisiti
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a>Configurazione avanzata
### <a name="disable-automatic-crash-reporting"></a>Disabilitare la segnalazione automatica degli arresti anomali
È possibile disabilitare hello automatica degli arresti anomali delle funzionalità di impegno report. Quando si verifica un'eccezione non gestita, Engagement non eseguirà alcuna azione.

> [!WARNING]
> Se si disabilita questa funzionalità, quindi quando si verifica un arresto anomalo del sistema non gestita dell'app, Engagement non invia l'arresto anomalo di hello **AND** non comporta la chiusura della sessione hello e processi.
> 
> 

toodisable automatico segnalazioni di arresti anomali, personalizzare la configurazione a seconda della modalità di hello è stata dichiarata:

#### <a name="from-engagementconfigurationxml-file"></a>Dal file `EngagementConfiguration.xml`
Impostare i report dell'arresto anomalo troppo`false` tra `<reportCrash>` e `</reportCrash>` tag.

#### <a name="from-engagementconfiguration-object-at-run-time"></a>Dall'oggetto `EngagementConfiguration` in fase di esecuzione
Impostare toofalse di arresto anomalo di report utilizzando l'oggetto EngagementConfiguration.

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a>Disabilitare la segnalazione in tempo reale
Per impostazione predefinita, i report del servizio di Engagement hello registra in tempo reale. Se l'applicazione indica spesso i registri, è preferibile toobuffer hello registri e tooreport usarle in una sola volta in una base di tempo regolari. la cosiddetta "modalità burst".

toodo in tal caso, chiamare il metodo hello:

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

argomento Hello è un valore in **millisecondi**. Ogni volta che si desidera la registrazione in tempo reale di tooreactivate hello, chiamare il metodo hello senza alcun parametro, o con valore 0 hello.

Modalità burst leggermente aumenta la durata della batteria hello ma ha un impatto sulle hello Engagement Monitor: durata di tutte le sessioni e i processi vengono arrotondati toohello burst soglia (in questo modo, le sessioni e i processi è inferiore a soglia burst hello potrebbe non essere visibile). È consigliabile usare una soglia di burst non maggiore di 30000, ovvero 30 secondi. Registri salvati sono elementi too300 limitato. Se l'invio richiede troppo tempo, è possibile che alcuni log vadano persi.

> [!WARNING]
> soglia burst Hello non può essere configurato tooa periodo minore secondo. Se in tal caso, hello SDK Mostra una traccia con l'errore hello e reimposta automaticamente toohello valore predefinito zero secondi. Questo trigger prova SDK tooreport prova l'accesso in tempo reale.
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
