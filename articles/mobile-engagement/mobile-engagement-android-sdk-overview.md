---
title: aaaAndroid integrazione del SDK per Azure Mobile Engagement
description: Viene descritto come toointegrate Azure Mobile Engagement SDK nelle App Android
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a91ed04f-f3ce-4692-a6dd-b56a28d7dee8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo;ricksal
ms.openlocfilehash: 0c63bfaf673abbda7ea498390f8282c43e2fb8df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a>Integrazione di Android SDK per Azure Mobile Engagement
> [!div class="op_single_selector"]
> * [Windows universale](mobile-engagement-windows-store-sdk-overview.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-sdk-overview.md)
> * [iOS](mobile-engagement-ios-sdk-overview.md)
> * [Android](mobile-engagement-android-sdk-overview.md)
> 
> 

Questo documento descrive tutti hello integration e opzioni di configurazione disponibili per Azure Mobile Engagement SDK Android.

## <a name="prerequisites"></a>Prerequisiti
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a>Funzionalità avanzate
### <a name="reporting-features"></a>Funzionalità di segnalazione
È possibile aggiungere queste funzionalità:

1. [Opzioni di segnalazione avanzata](mobile-engagement-android-advanced-reporting.md)
2. [Opzioni di segnalazione della posizione](mobile-engagement-android-location-reporting.md)
3. [Opzioni di configurazione avanzate](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a>Notifiche:
[Come toointegrate Reach (notifiche) nell'app Android](mobile-engagement-android-integrate-engagement-reach.md)

1. Google Cloud Messaging (GCM): [come tooIntegrate GCM con Engagement Mobile](mobile-engagement-android-gcm-integrate.md)
2. Amazon Device Messaging (ADM): [come tooIntegrate ADM con Engagement Mobile](mobile-engagement-android-adm-integrate.md)

### <a name="tag-plan-implementation"></a>Implementazione del piano di tag:
[Come toouse hello avanzate tag API nell'app Android di Mobile Engagement](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a>Note sulla versione

### <a name="431-07172017"></a>4.3.1 (07/17/2017)
* Correzione di un arresto anomalo che poteva verificarsi raramente quando si chiama `EngagementAgentUtils.isInDedicatedEngagementProcess`, che viene utilizzato anche dal hello `EngagementApplication` classe.

### <a name="430-06272017"></a>4.3.0 (06/27/2017)
* Supporto Android 8 (versioni precedenti del SDK non funziona in 8 Android hello).
* Nessuna dipendenza nella raccolta di supporto.
* Rimuovere la classe `EngagementFragmentActivity`.
* Scadenza troppo[limiti di esecuzione in Background](https://developer.android.com/preview/features/background.html) in Android 8, i log in background potrebbero subire un ritardo fino a quando non hello utente interagisce con dispositivi hello, ciò avrà un impatto sulla campagna Push **consegnati** e **Notifica di sistema visualizzata** statistiche viene ritardate se è stato sospeso dispositivo hello (notifica hello verranno comunque visualizzata, verrà dell'anello e vibrare in tempo reale senza problemi).
* Scadenza troppo[Background percorso limiti](https://developer.android.com/preview/features/background-location-limits.html), posizione in tempo reale hello in background non verranno aggiornati frequentemente in Android 8.

Per tutte le versioni, vedere hello [completare note sulla versione](mobile-engagement-android-release-notes.md).

## <a name="upgrade-procedures"></a>Procedure di aggiornamento
Se è già stata integrata una versione precedente di Windows SDK nell'applicazione, vedere le [procedure di aggiornamento](mobile-engagement-android-upgrade-procedure.md).

