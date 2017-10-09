---
title: aaaAzure integrazione SDK Android di Mobile Engagement
description: Ultimi aggiornamenti e procedure relativi ad Azure Mobile Engagement SDK per Android
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a5487793-1a12-4f6c-a1cf-587c5a671e6b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4f79936ea0fa6102023dec2b4682032a4a81fa9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-android"></a>Come tooIntegrate Engagement in Android
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

Questa procedura descrive Engagement tooactivate di modo più semplice di hello Analitica e funzioni in un'applicazione Android di monitoraggio.

> [!IMPORTANT]
> L'API di Android SDK deve essere almeno di livello 10 o superiore (Android 2.3.3 o versioni successive).
> 
> 

Hello seguendo i passaggi è che sufficienti tooactivates hello dei log è necessario un report toocompute tutte le statistiche relative agli utenti, sessioni, attività, arresti anomali del sistema e Technicals. Hello dei log è necessario un report toocompute altre statistiche quali processi, errori ed eventi devono essere eseguiti manualmente tramite API di Engagement hello (vedere [come toouse hello avanzate Mobile Engagement tag API in Android](mobile-engagement-android-use-engagement-api.md) poiché questi le statistiche sono dipende dall'applicazione.

## <a name="embed-hello-engagement-sdk-and-service-into-your-android-project"></a>Incorporare il progetto Android hello Engagement SDK e servizio
Download hello Android SDK da [qui](https://aka.ms/vq9mfn) ottenere `mobile-engagement-VERSION.jar` e inserirli in hello `libs` cartella del progetto Android (se non esiste ancora, creare cartelle di librerie hello).

> [!IMPORTANT]
> Se si compila il pacchetto dell'applicazione con ProGuard, è necessario tookeep alcune classi. È possibile utilizzare hello seguente frammento di configurazione:
> 
> -keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
> 
> <methods>; }
> 
> 

Specificare la stringa di connessione Engagement, hello chiamata seguente metodo in attività di avvio hello:

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

stringa di connessione Hello per l'applicazione viene visualizzato nel portale di Azure.

* Se presente, aggiungere queste autorizzazioni Android hello (prima hello `<application>` tag):
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* Aggiungere hello successiva sezione (tra hello `<application>` e `</application>` tag):
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* Modifica `<Your application name>` dal nome dell'applicazione hello.

> [!TIP]
> Hello `android:label` attributo consente un nome hello toochoose di hello servizio Engagement come verrà visualizzato agli utenti finali toohello nella schermata di "Servizi in esecuzione" hello del telefono. È consigliabile tooset questo attributo troppo`"<Your application name>Service"` (ad esempio `"AcmeFunGameService"`).
> 
> 

Se si specifica hello `android:process` attributo assicura che il servizio di Engagement hello verrà eseguito nel proprio processo (Engagement in esecuzione nella stessa procedura adottata applicazione renderà il thread principale o dell'interfaccia utente potenzialmente tempi hello).

> [!NOTE]
> Inserire nel codice `Application.onCreate()` e per tutti i processi dell'applicazione, incluso hello Engagement servizio verranno eseguiti altri i callback dell'applicazione. Potrebbe avere effetti indesiderati (ad esempio, le allocazioni di memoria non necessari e i thread nel processo di Engagement hello, ricevitori broadcast duplicati o servizi).
> 
> 

Se esegue l'override `Application.onCreate()`, hello tooadd consigliato seguente all'inizio di hello del frammento di codice è il `Application.onCreate()` funzione:

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

È possibile eseguire hello stessa operazione per `Application.onTerminate()`, `Application.onLowMemory()` e `Application.onConfigurationChanged(...)`.

È anche possibile estendere `EngagementApplication` anziché estensione `Application`: hello callback `Application.onCreate()` hello controllo processo e chiama `Application.onApplicationProcessCreate()` solo se il processo corrente hello è non hello uno hello Engagement servizio di hosting, hello stesse regole valide per Hello altre richiamate.

## <a name="basic-reporting"></a>Segnalazione di base
### <a name="recommended-method-overload-your-activity-classes"></a>Metodo consigliato: eseguire l'overload delle classi `Activity`
Report hello tooactivate order di tutti i log di hello richiesto da Engagement toocompute utenti, sessioni, attività, arresti anomali del sistema e le statistiche tecniche, è sufficiente toomake tutti i `*Activity` sottoclassi ereditano hello corrispondente `Engagement*Activity` classi (ad esempio, se l'attività legacy estende `ListActivity`, assicurarsi che estende `EngagementListActivity`).

**Senza Engagement:**

            package com.company.myapp;

            import android.app.Activity;
            import android.os.Bundle;

            public class MyApp extends Activity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

**Con Engagement:**

            package com.company.myapp;

            import com.microsoft.azure.engagement.activity.EngagementActivity;
            import android.os.Bundle;

            public class MyApp extends EngagementActivity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

> [!IMPORTANT]
> Quando si utilizza `EngagementListActivity` o `EngagementExpandableListActivity`, assicurarsi che tutte le chiamate troppo`requestWindowFeature(...);` diventa troppo prima chiamata hello`super.onCreate(...);`, in caso contrario si verificherà un arresto anomalo.
> 
> 

È possibile trovare queste classi in hello `src` cartella e possono copiare nel progetto. classi di Hello sono anche in hello **JavaDoc**.

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a>Metodo alternativo: chiamare manualmente `startActivity()` e `endActivity()`
Se non è possibile o non si desidera toooverload il `Activity` classi, è invece possibile iniziare e terminare le attività chiamando `EngagementAgent`del diretta dei metodi.

> [!IMPORTANT]
> Hello, Android SDK non chiama mai hello `endActivity()` (metodo), anche quando viene chiusa l'applicazione hello (in Android, chiudere le applicazioni sono in realtà non). È pertanto *elevata* consigliato hello toocall `startActivity()` metodo hello `onResume` callback di *tutti* le attività e hello `endActivity()` metodo hello `onPause()` callback di *tutti* delle attività. Si tratta di hello solo modo toobe assicurarsi che le sessioni non andrà perso. Se una sessione viene perso, hello servizio Engagement mai disconnessa dal back-end Engagement hello (dal momento che il servizio di hello rimane connesso, purché una sessione è in sospeso).
> 
> 

Di seguito è fornito un esempio:

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

Questo toohello molto simili di esempio `EngagementActivity` classe e le sue varianti, il cui codice sorgente viene fornito in hello `src` cartella.

## <a name="test"></a>Test
Esegue l'app per dispositivi mobili in un emulatore o un dispositivo e verificando che registra una sessione nella scheda Monitoraggio hello ora. verificare l'integrazione.

Nelle sezioni successive di Hello sono facoltative.

## <a name="location-reporting"></a>Segnalazione della posizione
Se si desidera toobe percorsi segnalato, è necessario tooadd poche righe di configurazione (tra hello `<application>` e `</application>` tag).

### <a name="lazy-area-location-reporting"></a>Segnalazione differita della posizione
Segnalazione differita della posizione consente paese hello tooreport, area e località associata toodevices. Questo tipo di segnalazione della posizione usa solo le posizioni di rete, sulla base dell'ID di cella o della connessione Wi-Fi. area Hello del dispositivo viene segnalato al massimo una volta per ogni sessione. Hello GPS non viene mai utilizzato e, pertanto questo tipo di report di percorso include solo poche (non toosay alcun) impatto sulla batteria hello.

Le aree segnalate sono utilizzati toocompute statistiche geografica sugli utenti, sessioni, eventi e gli errori. Possono essere usate anche come criteri nelle campagne Reach.

percorso area lazy tooenable reporting, è possibile farlo tramite configurazione hello indicato in precedenza in questa procedura:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

È inoltre necessario hello tooadd seguente autorizzazione se mancante:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

Oppure è possibile continuare a utilizzare ``ACCESS_FINE_LOCATION`` se è già utilizzato nell'applicazione.

### <a name="real-time-location-reporting"></a>Segnalazione della posizione in tempo reale
La segnalazione della posizione in tempo reale consente tooreport hello latitudine e la longitudine associata toodevices. Per impostazione predefinita, questo tipo di segnalazione della posizione Usa solo i percorsi di rete (basati su ID di cella o Wi-Fi) e reporting hello è attivo solo durante l'esecuzione di un'applicazione hello in primo piano (ad esempio durante una sessione).

I percorsi in tempo reale sono *non* utilizzato toocompute statistiche. Il loro scopo solo è utilizzare hello tooallow di geo-fencing in tempo reale \<Reach-pubblico-geofencing\> criterio di campagne di copertura.

posizione in tempo reale tooenable reporting, è possibile farlo tramite configurazione hello indicato in precedenza in questa procedura:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

È inoltre necessario hello tooadd seguente autorizzazione se mancante:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

Oppure è possibile continuare a utilizzare ``ACCESS_FINE_LOCATION`` se è già utilizzato nell'applicazione.

#### <a name="gps-based-reporting"></a>Segnalazione basata su GPS
Per impostazione predefinita, la segnalazione della posizione in tempo reale usa solo posizioni di rete. Utilizzare hello tooenable di GPS basato su percorsi, che sono molto più precise, usare l'oggetto configurazione hello:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

È inoltre necessario hello tooadd seguente autorizzazione se mancante:

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a>Segnalazione in background
Per impostazione predefinita, la segnalazione della posizione in tempo reale è attiva solo durante l'esecuzione di un'applicazione hello in primo piano (ad esempio durante una sessione). reporting hello tooenable anche in background, usare hello configurazione oggetto:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> Quando un'applicazione hello viene eseguito in background, vengono segnalati solo i percorsi di rete di base, anche se è abilitata hello GPS.
> 
> 

report sulla posizione background Hello verrà arrestata se utente hello viene riavviato il dispositivo, è possibile aggiungere questo toomake riavviato automaticamente in fase di avvio:

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

È inoltre necessario hello tooadd seguente autorizzazione se mancante:

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a>Autorizzazioni Android M
A partire da Android M, alcune autorizzazioni vengono gestite in fase di esecuzione e richiedono l'approvazione dell'utente.

le autorizzazioni di runtime Hello verranno disattivate per impostazione predefinita per le nuove installazioni di app se la destinazione è il livello di API Android 23. In caso contrario verranno attivate per impostazione predefinita.

utente Hello può abilitare o disabilitare le autorizzazioni dal menu di impostazioni dispositivo hello. La disattivazione di autorizzazioni dal menu di sistema di processi in background di un'applicazione hello termina, questo è un comportamento del sistema e non influisce sulla possibilità tooreceive push in background.

Nel contesto di hello di Mobile Engagement, le autorizzazioni di hello che richiedono l'approvazione in fase di esecuzione sono:

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* `WRITE_EXTERNAL_STORAGE` (solo quando la destinazione è il livello 23 dell’API Android)

archiviazione esterna Hello viene utilizzato solo per funzionalità quadro generale di copertura. Se si trova chiedere agli utenti di questo toobe autorizzazione arresto improvviso, è possibile rimuoverlo se è stato utilizzato solo per Engagement Mobile, ma al costo di hello di disabilitare la funzionalità quadro generale.

Per le funzionalità di percorso hello, è necessario richiedere autorizzazioni toouser utilizzando una finestra di dialogo di sistema standard. Se l'utente hello Approva, è necessario tootell ``EngagementAgent`` tootake che modificano in considerazione in tempo reale (modifica hello in caso contrario verrà elaborato successivo ora hello utente avvia hello un'applicazione hello).

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
         * Request location permission, but this won't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want tookeep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a>Segnalazione avanzata
Facoltativamente, se si desidera tooreport eventi specifici di applicazione, gli errori e i processi, è necessario toouse hello API Engagement tramite i metodi di hello di hello `EngagementAgent` classe. Un oggetto di questa classe può essere recuperati dal chiamante hello `EngagementAgent.getInstance()` metodo statico.

Consente tutte le funzionalità avanzate di Engagement toouse Hello Engagement API e dettagliato in hello come tooUse l'API di Engagement in Android (nonché in documentazione tecnica di hello di hello `EngagementAgent` classe).

## <a name="advanced-configuration-in-androidmanifestxml"></a>Configurazione avanzata (in AndroidManifest.xml)
### <a name="wake-locks"></a>Wakelocking
Se si desidera assicurarsi che le statistiche vengono inviate in tempo reale quando si utilizza Wi-Fi o se viene disattivata il schermata Ciao toobe, aggiungere hello autorizzazione facoltativi seguenti:

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a>Segnalazione di arresto anomalo 
Se si desidera toodisable segnalazioni di arresti anomali, aggiungere questo (tra hello `<application>` e `</application>` tag):

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a>Soglia del burst
Per impostazione predefinita, i report del servizio di Engagement hello registra in tempo reale. Se l'applicazione segnala molto spesso i registri, è preferibile toobuffer hello registri e tooreport usarle in una sola volta in volta regolare base (è chiamata hello "modalità burst"). In tal caso, aggiungere questo toodo (tra hello `<application>` e `</application>` tag):

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

Hello modalità burst leggermente aumentare batteria hello vita ma ha un impatto sulle hello Engagement Monitor: durata di tutte le sessioni e i processi sarà arrotondato toohello burst soglia (in questo modo, le sessioni e i processi è inferiore a soglia burst hello potrebbe non essere visibile). È consigliabile toouse una soglia di potenziamento non più di 30000 (30 s).

### <a name="session-timeout"></a>Timeout della sessione
Per impostazione predefinita, una sessione è terminata 10s dopo la fine di hello della propria attività ultima (che in genere si verifica da premendo hello Home o eseguire il backup di chiave, tramite telefono di hello impostazione inattivo o passare a un'altra applicazione). Si tratta di tooavoid una divisione di sessione, ogni utente hello in fase di uscire e tornare rapidamente applicazione toohello (che può verificarsi quando ha prelevati da un'immagine, verificare una notifica e così via.). È opportuno toomodify questo parametro. In tal caso, aggiungere questo toodo (tra hello `<application>` e `</application>` tag):

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a>Disabilitare la segnalazione di log
### <a name="using-a-method-call"></a>Uso di una chiamata del metodo
Se si desidera toostop Engagement l'invio di log, è possibile chiamare:

            EngagementAgent.getInstance(context).setEnabled(false);

Questa chiamata è persistente: usa un file di preferenze condivise.

Se Engagement è attivo quando si chiama questa funzione, può richiedere un minuto per hello servizio toostop. Tuttavia, non verrà avviato servizio hello hello tutti successivo avvio di un'applicazione hello.

È possibile abilitare nuovamente reporting chiamando hello stessa funzione con log `true`.

### <a name="integration-in-your-own-preferenceactivity"></a>Integrazione nella propria classe `PreferenceActivity`
Invece di chiamare questa funzione, è anche possibile integrare questa impostazione direttamente nella classe `PreferenceActivity` esistente.

È possibile configurare le preferenze di file (con modalità desiderata di hello) toouse di Engagement in hello `AndroidManifest.xml` file con `application meta-data`:

* Hello `engagement:agent:settings:name` chiave è utilizzata toodefine hello nome del file di preferenze condivise hello.
* Hello `engagement:agent:settings:mode` chiave è la modalità di hello toodefine utilizzate del file di preferenze condivise hello, è necessario utilizzare hello modalità stesso come il `PreferenceActivity`. modalità Hello deve essere passata come un numero: se si utilizza una combinazione di flag costante nel codice, controllare il valore totale di hello.

Engagement sempre utilizzare hello `engagement:key` booleano chiave all'interno di file di preferenze hello per la gestione di questa impostazione.

Hello in seguito ad esempio `AndroidManifest.xml` Mostra hello valori predefiniti:

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

È quindi possibile aggiungere un `CheckBoxPreference` nel layout delle preferenze come segue quello hello:

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
