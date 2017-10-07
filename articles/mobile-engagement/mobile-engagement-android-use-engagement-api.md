---
title: aaaHow tooUse hello Engagement API in Android
description: "Android SDK più recente - come tooUse hello Engagement API in Android"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 09b62659-82ae-4a55-8784-fca0b6b22eaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: article
ms.date: 07/25/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e0b2d484616c0c7874e77c5283d94c3063949ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-android"></a>Come tooUse hello Engagement API in Android
Questo documento è un componente aggiuntivo toohello [opzioni avanzate di segnalazione per Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md). Fornisce informazioni approfondite su come toouse hello API Engagement tooreport le statistiche dell'applicazione.

Tenere presente che se si vuole solo Engagement tooreport sessioni dell'applicazione, le attività, arresti anomali del sistema e informazioni tecniche, quindi hello semplice toomake tutti i `Activity` sottoclassi ereditano hello corrispondente `EngagementActivity` classe.

Se si desidera toodo altre, ad esempio se è necessario tooreport eventi specifici di applicazione, gli errori e i processi o se hai tooreport attività dell'applicazione in modo diverso rispetto a uno implementato in hello hello `EngagementActivity` classi, è necessario toouse hello Engagement API.

Hello Engagement API viene fornita da hello `EngagementAgent` classe. Un'istanza di questa classe può essere recuperata dal chiamante hello `EngagementAgent.getInstance(Context)` metodo statico (si noti che hello `EngagementAgent` oggetto restituito è un singleton).

## <a name="engagement-concepts"></a>Concetti relativi a Mobile Engagement
parti seguenti Hello perfezionare hello comune [concetti Engagement Mobile](mobile-engagement-concepts.md), per la piattaforma Android hello.

### <a name="session-and-activity"></a>`Session` e `Activity`
Se più di pochi secondi di inattività tra due hello rimane *attività*, quindi la sequenza di *attività* è divisa in due distinti *sessioni*. Questi alcuni secondi vengono chiamati hello "timeout della sessione".

Un *attività* è generalmente associato a una schermata dell'applicazione hello, che è hello toosay *attività* inizia quando la schermata Ciao viene visualizzato e si arresta alla chiusura della schermata hello: si tratta di hello caso in cui Hello Engagement SDK è integrato con hello `EngagementActivity` classi.

Ma *attività* può essere controllato anche manualmente utilizzando l'API di Engagement hello. In questo modo una schermata determinata toosplit in diversi tooget di parti di sub hello di ulteriori dettagli sull'utilizzo di questa schermata (ad esempio la frequenza con cui tooknown e per quanto tempo, all'interno di questa schermata, vengono utilizzate le finestre di dialogo).

## <a name="reporting-activities"></a>Segnalazione di attività
> [!IMPORTANT]
> Non è necessario tooreport le attività, come descritto in questa sezione se si utilizza hello `EngagementActivity` classe e le sue varianti, come illustrato in hello tooIntegrate Engagement documento Android.
> 
> 

### <a name="user-starts-a-new-activity"></a>L'utente inizia una nuova attività
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing hello current activity is required for Reach toodisplay in-app notifications, passing null will postpone such announcements and polls.

È necessario toocall `startActivity()` ogni attività utente hello in fase di modifica. Hello prima chiamata toothis funzione avvia una nuova sessione utente.

Hello migliore toocall sul posto questa funzione è in ogni attività `onResume` callback.

### <a name="user-ends-his-current-activity"></a>L'utente termina l'attività corrente
            EngagementAgent.getInstance(this).endActivity();

È necessario toocall `endActivity()` almeno una volta al termine della sua attività ultimo utente hello. Informa hello scadrà Engagement SDK che utente hello è attualmente inattivo e che la sessione di utente hello necessario toobe chiuso una volta hello timeout della sessione (se si chiama `startActivity()` prima della scadenza del timeout della sessione hello, sessione hello viene semplicemente ripreso).

Hello migliore toocall sul posto questa funzione è in ogni attività `onPause` callback.

## <a name="reporting-events"></a>Segnalazione di eventi
### <a name="session-events"></a>Eventi di sessione
Gli eventi di sessione sono azioni hello tooreport utilizzati in genere eseguite da un utente durante la sessione.

**Esempio senza dati aggiuntivi:**

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

**Esempio con dati aggiuntivi:**

            public MyActivity extends EngagementActivity {
              [...]
              @Override
              public boolean onMenuItemSelected(int featureId, MenuItem item) {
                Bundle extras = new Bundle();
                extras.putInt("id", item.getItemId());
                getEngagementAgent().sendSessionEvent("menu_selected", extras);
              }
              [...]
            }

### <a name="standalone-events"></a>Eventi autonomi
Di fuori di contesto hello di una sessione possono verificarsi eventi di toosession contrarie, gli eventi autonomo.

**Esempio:**

Si supponga di che voler tooreport eventi che si verificano quando viene attivato un ricevitore di trasmissione:

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a>Segnalazione di errori
### <a name="session-errors"></a>Errori di sessione
Sessione gli errori in genere utilizzato tooreport hello conseguenze utente hello durante la sessione.

**Esempio:**

            /** hello user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* hello user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a>Errori autonomi
Di fuori di contesto hello di una sessione possono verificarsi errori di toosession contrarie, errori autonomo.

**Esempio:**

Hello esempio seguente viene illustrato come tooreport errore ogni volta che la memoria hello diventa insufficiente phone hello durante il processo di applicazione è in fase di esecuzione.

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a>Segnalazione di processi
### <a name="example"></a>Esempio
Si supponga che si desidera tooreport hello durata del processo di accesso:

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a>Segnalazione di errori durante un processo
Gli errori possono essere correlato tooa esecuzione processo anziché essere correlate toohello sessione utente.

**Esempio:**

Si supponga che si desidera tooreport un errore durante la si accesso processo:

[...] public void signIn(Context context, ...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try toosign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report hello error tooEngagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a>Segnalazione di eventi durante un processo
Gli eventi possono essere correlato tooa esecuzione processo anziché essere correlate toohello sessione utente.

**Esempio:**

Si supponga che abbiamo un social network ed è possibile usare un processo tooreport hello totale tempo durante cui hello utente è connesso toohello server. utente Hello può rimanere connessi in background anche quando si utilizza un'altra applicazione o quando è inattivo phone hello, pertanto non c'è alcuna sessione.

utente Hello può ricevere messaggi dai suoi amici, si tratta di un evento di processo.

            [...]
            public void signin(Context context, ...) {
              [...Sign in code...]
              EngagementAgent.getInstance(context).startJob("connection", null);
            }
            [...]
            public void signout(Context context) {
              [...Sign out code...]
              EngagementAgent.getInstance(context).endJob("connection");
            }
            [...]
            public void onMessageReceived(Context context) {
              [...Notify in status bar...]
              EngagementAgent.getInstance(context).sendJobEvent("message_received", "connection", null);
            }
            [...]

## <a name="extra-parameters"></a>Parametri aggiuntivi
Dati arbitrari possono essere collegati tooevents, errori, le attività e processi.

Questi dati possono essere strutturati, usando la classe Bundle di Android (in realtà, funziona come i parametri aggiuntivi negli intenti di Android). Notare che una classe Bundle può contenere matrici o altre istanze Bundle.

> [!IMPORTANT]
> Se si inserisce in parametri parcelable o serializable, assicurarsi che i relativi `toString()` metodo è implementato tooreturn una stringa leggibile. Le classi serializzabili che contengono campi non temporanei non serializzabili provocano l'arresto anomalo di Android quando si chiama `bundle.putSerializable("key",value);`
> 
> [!WARNING]
> Le matrici di tipo sparse non sono supportate nei parametri aggiuntivi, ovvero non vengono serializzate come matrice. Prima di usarle nei parametri aggiuntivi, è consigliabile convertirle in matrici standard.
> 
> 

### <a name="example"></a>Esempio
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a>Limiti
#### <a name="keys"></a>Chiavi
Ogni chiave hello `Bundle` deve corrispondere hello espressione regolare seguente:

`^[a-zA-Z][a-zA-Z_0-9]*`

Questo significa che le chiavi devono iniziare con almeno una lettera, seguita da lettere, cifre o caratteri di sottolineatura (\_).

#### <a name="size"></a>Dimensione
Funzionalità aggiuntive sono troppo limitate**1024** caratteri per ogni chiamata (una volta codificato in JSON dal servizio di Engagement hello).

In hello esempio precedente, hello JSON inviato server toohello è 58 caratteri:

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a>Segnalazione di informazioni sull'applicazione
È possibile segnalare manualmente traccia informazioni o qualsiasi altra informazione di specifici dell'applicazione mediante hello `sendAppInfo()` (funzione).

Si noti che queste informazioni possono essere inviate in modo incrementale: solo hello valore più recente per una determinata chiave verrà conservati per un determinato dispositivo.

Come funzionalità aggiuntive di evento, hello classe Bundle è usato tooabstract informazioni dell'applicazione, si noti che le matrici o Sub Raggruppa verranno considerati come stringhe flat (con la serializzazione JSON).

### <a name="example"></a>Esempio
Ecco un sesso utente toosend esempio di codice e la data di nascita:

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a>Limiti
#### <a name="keys"></a>Chiavi
Ogni chiave hello `Bundle` deve corrispondere hello espressione regolare seguente:

`^[a-zA-Z][a-zA-Z_0-9]*`

Questo significa che le chiavi devono iniziare con almeno una lettera, seguita da lettere, cifre o caratteri di sottolineatura (\_).

#### <a name="size"></a>Dimensione
Informazioni sull'applicazione sono troppo limitati**1024** caratteri per ogni chiamata (una volta codificato in JSON dal servizio di Engagement hello).

In hello esempio precedente, hello JSON inviato server toohello è 44 caratteri:

            {"expiration":"2016-12-07","status":"premium"}
