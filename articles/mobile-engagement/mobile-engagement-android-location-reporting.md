---
title: aaaLocation Reporting per Azure Mobile Engagement SDK Android
description: Viene descritto come percorso tooconfigure reporting per Azure Mobile Engagement SDK Android
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6cab5ed1-b767-46ac-9f0b-48a4e249d88c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: c2cb097df2a77bee2d56ffe9509dc116548db408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a>Segnalazione della posizione per Android SDK per Azure Mobile Engagement
> [!div class="op_single_selector"]
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

Questo argomento viene descritto come percorso toodo reporting per l'applicazione di Android.

## <a name="prerequisites"></a>Prerequisiti
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a>Segnalazione della posizione
Se si desidera toobe percorsi segnalato, è necessario tooadd poche righe di configurazione (tra hello `<application>` e `</application>` tag).

### <a name="lazy-area-location-reporting"></a>Segnalazione differita della posizione
Segnalazione differita della posizione consente reporting hello paese, area e località associate ai dispositivi. Questo tipo di segnalazione della posizione usa solo le posizioni di rete, sulla base dell'ID di cella o della connessione Wi-Fi. area Hello del dispositivo viene segnalato al massimo una volta per ogni sessione. Hello GPS non viene mai utilizzato e, pertanto questo tipo di percorso report ha impatto significativo a batteria hello.

Le aree segnalate sono utilizzati toocompute statistiche geografica sugli utenti, sessioni, eventi e gli errori. Possono essere usate anche come criteri nelle campagne Reach.

Si attiva il percorso di area lazy reporting con la configurazione di hello indicato in precedenza in questa procedura:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

È inoltre necessario toospecify un'autorizzazione di percorso. Questo codice usa l'autorizzazione ``COARSE`` :

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

Se l'app lo richiede, è possibile usare invece di ``ACCESS_FINE_LOCATION`` .

### <a name="real-time-location-reporting"></a>Segnalazione della posizione in tempo reale
La segnalazione della posizione in tempo reale consente reporting hello latitudine e la longitudine associate ai dispositivi. Questo tipo di segnalazione della posizione usa solo le posizioni di rete, sulla base dell'ID di cella o della connessione Wi-Fi. reporting Hello è attivo solo durante l'esecuzione di un'applicazione hello in primo piano (ad esempio, durante una sessione).

I percorsi in tempo reale sono *non* utilizzato toocompute statistiche. Il loro scopo solo è utilizzare hello tooallow di geo-fencing in tempo reale \<Reach-pubblico-geofencing\> criterio di campagne di copertura.

creazione di report, la posizione in tempo reale tooenable aggiungere una riga di codice toowhere impostare stringa di connessione Engagement hello in attività di avvio hello. ottenere un risultato Hello hello seguente:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need toospecify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a>Segnalazione basata su GPS
Per impostazione predefinita, la segnalazione della posizione in tempo reale usa solo posizioni di rete. tooenable hello GPS basato su percorsi, che sono molto più precisa, utilizzare oggetti di configurazione hello:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

È inoltre necessario hello tooadd seguente autorizzazione se mancante:

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a>Segnalazione in background
Per impostazione predefinita, la segnalazione della posizione in tempo reale è attiva solo durante l'esecuzione di un'applicazione hello in primo piano (ad esempio, durante una sessione). hello tooenable reporting anche in background, utilizzare l'oggetto di configurazione:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> Quando un'applicazione hello viene eseguito in background, vengono segnalati solo i percorsi di rete, anche se è abilitata hello GPS.
> 
> 

Se l'utente hello riavvio del dispositivo, report di posizione background hello viene arrestato. toomake riavviato automaticamente in fase di avvio, aggiungere questo codice.

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

È inoltre necessario hello tooadd seguente autorizzazione se mancante:

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a>Autorizzazioni Android M
A partire da Android M, alcune autorizzazioni vengono gestite in fase di esecuzione e richiedono l'approvazione dell'utente.

Se la destinazione è il livello di API Android 23, le autorizzazioni di runtime hello sono disattivate per impostazione predefinita per le nuove installazioni di app. In caso contrario vengono attivate per impostazione predefinita.

È possibile abilitare o disabilitare le autorizzazioni dal menu di impostazioni dispositivo hello. La disattivazione di autorizzazioni dal menu di sistema hello termina i processi in background hello dell'applicazione hello, che è un comportamento del sistema e non influisce sulla possibilità tooreceive push in background.

Nel contesto di hello della posizione di Mobile Engagement reporting, le autorizzazioni di hello che richiedono l'approvazione in fase di esecuzione sono:

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

Richiedere autorizzazioni all'utente di hello utilizzando una finestra di dialogo di sistema standard. Indicare se l'utente hello Approva, ``EngagementAgent`` tootake che cambiano in considerazione in tempo reale. In caso contrario modifica hello è elaborato successivo ora hello utente avvia hello un'applicazione hello.

Ecco un toouse di esempio di codice in un'attività, delle autorizzazioni per l'applicazione toorequest e portare avanti hello se positivo troppo``EngagementAgent``:

    @Override
    public void onCreate(Bundle savedInstanceState)
    {
      /* Other code... */

      /* Request permissions */
      requestPermissions();
    }

    @TargetApi(Build.VERSION_CODES.M)
    private void requestPermissions()
    {
      /* Avoid crashing if not on Android M */
      if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M)
      {
        /*
         * Request location permission, but this doesn't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }
