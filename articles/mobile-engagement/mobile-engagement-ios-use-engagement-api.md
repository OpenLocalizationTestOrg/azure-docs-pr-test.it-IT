---
title: aaaHow tooUse hello Engagement API in iOS
description: "IOS più recente SDK - come tooUse hello Engagement API in iOS"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1fb4509e-3804-46c1-949f-1cf727f91f9f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 7fb9b95ad319cf3b1e2de81b5d6aee5b30266069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-ios"></a>Come tooUse hello Engagement API in iOS
Questo documento è un componente aggiuntivo toohello come tooIntegrate Engagement in iOS: fornisce informazioni approfondite su come toouse hello API Engagement tooreport le statistiche dell'applicazione.

Tenere presente che se si desidera solo Engagement tooreport sessioni dell'applicazione, le attività, arresti anomali del sistema e informazioni tecniche, hello più semplice consiste nel toomake tutti personalizzato `UIViewController` oggetti ereditano hello corrispondente `EngagementViewController` classe .

Se si desidera toodo altre, ad esempio se è necessario tooreport eventi specifici di applicazione, gli errori e i processi o se hai tooreport attività dell'applicazione in modo diverso rispetto a uno implementato in hello hello `EngagementViewController` classi, è necessario toouse hello Engagement API.

Hello Engagement API viene fornita da hello `EngagementAgent` classe. Un'istanza di questa classe può essere recuperata dal chiamante hello `[EngagementAgent shared]` metodo statico (si noti che hello `EngagementAgent` oggetto restituito è un singleton).

Prima di qualsiasi chiamate API, hello `EngagementAgent` necessario inizializzare l'oggetto chiamando il metodo hello`[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`

## <a name="engagement-concepts"></a>Concetti relativi a Mobile Engagement
parti seguenti Hello perfezionare hello comune [concetti Engagement Mobile](mobile-engagement-concepts.md) per la piattaforma iOS hello.

### <a name="session-and-activity"></a>`Session` e `Activity`
Un *attività* è generalmente associato a una schermata dell'applicazione hello, che è hello toosay *attività* inizia quando la schermata Ciao viene visualizzato e si arresta alla chiusura della schermata hello: si tratta di hello caso in cui Hello Engagement SDK è integrato con hello `EngagementViewController` classi.

Ma *attività* può essere controllato anche manualmente utilizzando l'API di Engagement hello. In questo modo una schermata determinata toosplit in diversi tooget di parti di sub hello di ulteriori dettagli sull'utilizzo di questa schermata (ad esempio la frequenza con cui tooknown e per quanto tempo, all'interno di questa schermata, vengono utilizzate le finestre di dialogo).

## <a name="reporting-activities"></a>Segnalazione di attività
### <a name="user-starts-a-new-activity"></a>L'utente inizia una nuova attività
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

È necessario toocall `startActivity()` ogni attività utente hello in fase di modifica. Hello prima chiamata toothis funzione avvia una nuova sessione utente.

### <a name="user-ends-his-current-activity"></a>L'utente termina l'attività corrente
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> È necessario **mai** chiamare questa funzione personalmente, tranne se si desidera toosplit un utilizzo dell'applicazione in diverse sessioni: una chiamata di funzione toothis interromperebbe hello la sessione corrente immediatamente, pertanto, una chiamata successiva troppo`startActivity()`avvia una nuova sessione. Questa funzione viene chiamata automaticamente da hello SDK alla chiusura dell'applicazione.
> 
> 

## <a name="reporting-events"></a>Segnalazione di eventi
### <a name="session-events"></a>Eventi di sessione
Gli eventi di sessione sono azioni hello tooreport utilizzati in genere eseguite da un utente durante la sessione.

**Esempio senza dati aggiuntivi:**

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:nil];
            ...
       }
       [...]
    }

**Esempio con dati aggiuntivi:**

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        NSMutableDictionary* extras = [NSMutableDictionary dictionary];
        [extras setObject:[NSNumber numberWithInt:toInterfaceOrientation] forKey:@"to_orientation_id"];
        [extras setObject:[NSNumber numberWithDouble:duration] forKey:@"duration"];
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:extras];
            ...
       }
       [...]
    }

### <a name="standalone-events"></a>Eventi autonomi
Eventi di toosession contrarie, autonoma eventi possono essere usati all'esterno di contesto hello di una sessione.

**Esempio:**

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a>Segnalazione di errori
### <a name="session-errors"></a>Errori di sessione
Sessione gli errori in genere utilizzato tooreport hello conseguenze utente hello durante la sessione.

**Esempio:**

    /** hello user has entered invalid data in a form */
    @implementation MyViewController {
      [...]
      -(void)onMyFormSubmitted:(MyForm*)form {
        [...]
        /* hello user has entered an invalid email address */
        [[EngagementAgent shared] sendSessionError:@"sign_up_email" extras:nil]
        [...]
      }
      [...]
    }

### <a name="standalone-errors"></a>Errori autonomi
Errori toosession contrarie, autonomo possono essere utilizzati all'esterno di contesto hello di una sessione.

**Esempio:**

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a>Segnalazione di processi
**Esempio:**

Si supponga che si desidera tooreport hello durata del processo di accesso:

    [...]
    -(void)signIn
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      [... sign in ...]

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    }
    [...]

### <a name="report-errors-during-a-job"></a>Segnalazione di errori durante un processo
Gli errori possono essere correlato tooa esecuzione processo anziché essere correlate toohello sessione utente.

**Esempio:**

Si supponga di che voler tooreport un errore durante il processo di accesso:

    [...]
    -(void)signin
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      BOOL success = NO;
      while (!success) {
        /* Try toosign in */
        NSError* error = nil;
        [self trySigin:&error];
        success = error == nil;

        /* If an error occured report it */
        if(!success)
        {
          [[EngagementAgent shared] sendJobError:@"sign_in_error"
                         jobName:@"sign_in"
                          extras:[NSDictionary dictionaryWithObject:[error localizedDescription] forKey:@"error"]];

          /* Retry after a moment */
          [NSThread sleepForTimeInterval:20];
        }
      }

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    };
    [...]

### <a name="events-during-a-job"></a>Eventi durante un processo
Gli eventi possono essere correlato tooa esecuzione processo anziché essere correlate toohello sessione utente.

**Esempio:**

Si supponga che abbiamo un social network ed è possibile usare un processo tooreport hello totale tempo durante cui hello utente è connesso toohello server. utente Hello può ricevere messaggi dai suoi amici, si tratta di un evento di processo.

    [...]
    - (void) signin
    {
      [...Sign in code...]
      [[EngagementAgent shared] startJob:@"connection" extras:nil];
    }
    [...]
    - (void) signout
    {
      [...Sign out code...]
      [[EngagementAgent shared] endJob:@"connection"];
    }
    [...]
    - (void) onMessageReceived
    {
      [...Notify user...]
      [[EngagementAgent shared] sendJobEvent:@"connection" jobName:@"message_received" extras:nil];
    }
    [...]

## <a name="extra-parameters"></a>Parametri aggiuntivi
Dati arbitrari possono essere collegati tooevents, errori, le attività e processi.

Questi dati possono essere strutturati e utilizzano la classe NSDictionary di iOS.

Tenere presente che i dati aggiuntivi possono includere `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` o altre istanze di `NSDictionary`.

> [!NOTE]
> parametro aggiuntivo Hello viene serializzato in JSON. Se si desidera toopass oggetti diversi rispetto a quelli descritti sopra hello, è necessario implementare hello metodo nella classe seguente:
> 
> -(NSString*)JSONRepresentation;
> 
> metodo Hello deve restituire la rappresentazione JSON dell'oggetto.
> 
> 

### <a name="example"></a>Esempio
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a>Limiti
#### <a name="keys"></a>Chiavi
Ogni chiave hello `NSDictionary` deve corrispondere hello espressione regolare seguente:

`^[a-zA-Z][a-zA-Z_0-9]*`

Questo significa che le chiavi devono iniziare con almeno una lettera, seguita da lettere, cifre o caratteri di sottolineatura (\_).

#### <a name="size"></a>Dimensione
Funzionalità aggiuntive sono troppo limitate**1024** caratteri per ogni chiamata (una volta codificato in JSON dall'agente di Engagement hello).

In hello esempio precedente, hello JSON inviato server toohello è 58 caratteri:

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a>Segnalazione di informazioni sull'applicazione
È possibile segnalare manualmente traccia informazioni o qualsiasi altra informazione di specifici dell'applicazione mediante hello `sendAppInfo:` (funzione).

Si noti che queste informazioni possono essere inviate in modo incrementale: solo hello valore più recente per una determinata chiave verrà conservati per un determinato dispositivo.

Ad esempio funzionalità aggiuntive di evento, hello `NSDictionary` classe è usato tooabstract informazioni dell'applicazione, tenere presente che le matrici o dizionari secondari verranno considerati come stringhe flat (con la serializzazione JSON).

**Esempio:**

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a>Limiti
#### <a name="keys"></a>Chiavi
Ogni chiave hello `NSDictionary` deve corrispondere hello espressione regolare seguente:

`^[a-zA-Z][a-zA-Z_0-9]*`

Questo significa che le chiavi devono iniziare con almeno una lettera, seguita da lettere, cifre o caratteri di sottolineatura (\_).

#### <a name="size"></a>Dimensione
Informazioni sull'applicazione sono troppo limitati**1024** caratteri per ogni chiamata (una volta codificato in JSON dall'agente di Engagement hello).

In hello esempio precedente, hello JSON inviato server toohello è 44 caratteri:

    {"birthdate":"1983-12-07","gender":"female"}
