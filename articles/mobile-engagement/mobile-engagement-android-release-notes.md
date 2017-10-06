---
title: aaaAzure integrazione SDK Android di Mobile Engagement
description: Ultimi aggiornamenti e procedure relativi ad Azure Mobile Engagement SDK per Android
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 585341f9-3f39-459a-af42-864e400a0128
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 16b098198674c49567d720d0c01d984cb763ed8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes"></a>Note sulla versione

## <a name="431-07172017"></a>4.3.1 (07/17/2017)
* Correzione di un arresto anomalo che poteva verificarsi raramente quando si chiama `EngagementAgentUtils.isInDedicatedEngagementProcess`, che viene utilizzato anche dal hello `EngagementApplication` classe.

## <a name="430-06272017"></a>4.3.0 (06/27/2017)
* Supporto Android 8 (versioni precedenti del SDK non funziona in 8 Android hello).
* Nessuna dipendenza nella raccolta di supporto.
* Rimuovere la classe `EngagementFragmentActivity`.
* Scadenza troppo[limiti di esecuzione in Background](https://developer.android.com/preview/features/background.html) in Android 8, i log in background potrebbero subire un ritardo fino a quando non hello utente interagisce con dispositivi hello, ciò avrà un impatto sulla campagna Push **consegnati** e **Notifica di sistema visualizzata** statistiche viene ritardate se è stato sospeso dispositivo hello (notifica hello verranno comunque visualizzata, verrà dell'anello e vibrare in tempo reale senza problemi).
* Scadenza troppo[Background percorso limiti](https://developer.android.com/preview/features/background-location-limits.html), posizione in tempo reale hello in background non verranno aggiornati frequentemente in Android 8.

## <a name="424-03302017"></a>4.2.4 (03/30/2017)
* Correzione della notifica in-app colori del testo in toobe 7 Android hello stesso come le versioni precedenti di Android.

## <a name="423-08102016"></a>4.2.3 (08/10/2016)
* Rimozione del blocco Wi-Fi.
* Correzione di un deadlock quando si chiama getDeviceId prima di init (bug introdotto nella versione 4.2.0).

## <a name="422-05172016"></a>4.2.2 (05/17/2016)
* Miglioramenti della stabilità.

## <a name="421-05102016"></a>4.2.1 (05/10/2016)
* Sicurezza: disabilitare l'accesso al file locale di visualizzazione Web.
* Sicurezza: rimozione della classe `EngagementPreferenceActivity` che estende la classe `PreferenceActivity` obsoleta e non sicura.
* Sicurezza: reach attività sono documentati toouse `exported="false"`, questo flag può essere utilizzato anche nelle versioni precedenti di SDK.

## <a name="420-03112016"></a>4.2.0 (11/03/2016)
* Hello SDK ora è concesso in licenza in MIT.
* Consentire la specifica di un identificatore del dispositivo personalizzato in fase di inizializzazione dell'SDK.

## <a name="415-02012016"></a>4.1.5 (01/02/2016)
* Miglioramenti della stabilità.

## <a name="414-01262016"></a>4.1.4 (26/01/2016)
* Miglioramenti della stabilità.

## <a name="413-1292015"></a>4.1.3 (9/12/2015)
* Miglioramenti della stabilità.

## <a name="412-11252015"></a>4.1.2 (11/25/2015)
* Miglioramenti della stabilità.

## <a name="411-11042015"></a>4.1.1 (11/04/2015)
* Miglioramenti della stabilità.

## <a name="410-08252015"></a>4.1.0 (08/25/2015)
* Gestione di un nuovo modello di autorizzazione per Android M.
* Ora è possibile configurare le funzionalità di posizione in fase di esecuzione anziché usare `AndroidManifest.xml`.
* Correzione di un bug delle autorizzazioni: se si utilizza `ACCESS_FINE_LOCATION`, `ACCESS_COARSE_LOCATION` non è più necessario.
* Miglioramenti della stabilità.

## <a name="400-07062015"></a>4.0.0 (06/07/2015)
* Protocollo interno modifica toomake analitica e push più affidabile.
* Push nativo (GCM/ADM) è ora anche utilizzato per notifiche in-app è necessario configurare le credenziali push nativo hello per qualsiasi tipo di campagna push.
* Correzione della notifica generale: elementi visualizzati solo 10 secondi dopo il push.
* Correggere un bug nella visualizzazione web: facendo clic su un collegamento è stato inoltre l'esecuzione di hello URL di azione predefinito.
* Correzione di un arresto anomalo raro correlati toolocal gestione dell'archiviazione.
* Correzione della gestione delle stringhe di configurazione dinamiche.
* Aggiornamento del contratto di licenza.

## <a name="300-02172015"></a>3.0.0 (17/02/2015)
* Versione iniziale di Azure Mobile Engagement
* La configurazione di appId è stata sostituita con la configurazione della stringa di connessione.
* Rimosso toosend API e ricevere messaggi XMPP arbitrari da entità XMPP arbitraria.
* Rimosso toosend API e ricevere messaggi tra i dispositivi.
* Sono stati introdotti miglioramenti per la sicurezza.
* È stata rimossa la verifica per Google Play e SmartAd.

