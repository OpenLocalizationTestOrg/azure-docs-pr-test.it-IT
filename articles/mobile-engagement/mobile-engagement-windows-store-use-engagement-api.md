---
title: aaaHow tooUse hello Engagement API in universali di Windows
description: Come tooUse hello Engagement API in universali di Windows
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: bb501fca-9cfe-4495-81df-b5efd6e0137b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0256b839c28e4ef6c530106408d744038fa711ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-universal"></a>Come tooUse hello Engagement API in universali di Windows
Questo documento è un componente aggiuntivo toohello [come tooIntegrate Engagement in Universal Windows](mobile-engagement-windows-store-integrate-engagement.md): fornisce informazioni approfondite su come toouse hello API Engagement tooreport le statistiche dell'applicazione.

Tenere presente che se si vuole solo Engagement tooreport sessioni dell'applicazione, le attività, arresti anomali del sistema e informazioni tecniche, quindi hello semplice toomake tutti i `Page` sottoclassi ereditano hello `EngagementPage` classe.

Se si desidera toodo altre, ad esempio se è necessario tooreport eventi specifici di applicazione, gli errori e i processi o se hai tooreport attività dell'applicazione in modo diverso rispetto a uno implementato in hello hello `EngagementPage` classi, è necessario toouse hello Engagement API.

Hello Engagement API viene fornita da hello `EngagementAgent` classe. È possibile accedere tramite i metodi toothose `EngagementAgent.Instance`.

Anche se il modulo hello dell'agente non è stato inizializzato, ogni API toohello chiamata è rinviata e verrà eseguito nuovamente quando l'agente di hello è disponibile.

## <a name="engagement-concepts"></a>Concetti relativi a Mobile Engagement
parti seguenti Hello perfezionare hello comune [concetti Engagement Mobile](mobile-engagement-concepts.md) per piattaforma universale di Windows hello.

### <a name="session-and-activity"></a>`Session` e `Activity`
Un *attività* è generalmente associato a una pagina di un'applicazione hello, che è hello toosay *attività* inizia quando la pagina hello viene visualizzata e si arresta quando viene chiusa la pagina hello: hello caso quando hello Engagement SDK è integrato con hello `EngagementPage` classe.

Ma *attività* può essere controllato anche manualmente utilizzando l'API di Engagement hello. In questo modo toosplit una determinata pagina in diversi sottotipi parti tooget ulteriori dettagli sull'utilizzo di hello della pagina (ad esempio la frequenza con cui tooknow e per quanto tempo le finestre di dialogo vengono utilizzati all'interno di questa pagina).

## <a name="reporting-activities"></a>Segnalazione di attività
### <a name="user-starts-a-new-activity"></a>L'utente inizia una nuova attività
#### <a name="reference"></a>riferimento
            void StartActivity(string name, Dictionary<object, object> extras = null)

È necessario toocall `StartActivity()` ogni attività utente hello in fase di modifica. Hello prima chiamata toothis funzione avvia una nuova sessione utente.

> [!IMPORTANT]
> Hello SDK chiama automaticamente il metodo EndActivity hello quando un'applicazione hello viene chiuso. Di conseguenza, è consigliabile metodo StartActivity di hello toocall ogni volta che cambia attività hello dell'utente di hello e chiamata tooNEVER hello metodo EndActivity, dopo la chiamata di questo metodo forza toobe sessione corrente di hello è terminata.
> 
> 

#### <a name="example"></a>Esempio
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a>L'utente termina l'attività corrente
#### <a name="reference"></a>riferimento
            void EndActivity()

Questo Termina attività hello e sessione hello. Chiamare questo metodo solo se si è perfettamente consapevoli delle conseguenze.

#### <a name="example"></a>Esempio
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a>Segnalazione di processi
### <a name="start-a-job"></a>Avviare un processo
#### <a name="reference"></a>riferimento
            void StartJob(string name, Dictionary<object, object> extras = null)

È possibile utilizzare hello processo tootrack alcune attività in un periodo di tempo.

#### <a name="example"></a>Esempio
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a>Terminare un processo
#### <a name="reference"></a>riferimento
            void EndJob(string name)

Non appena è terminata un'attività rilevata da un processo, è necessario chiamare metodo EndJob hello per questo processo, fornendo il nome di processo hello.

#### <a name="example"></a>Esempio
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a>Segnalazione di eventi
Esistono tre tipi di eventi:

* Eventi autonomi
* Eventi di sessione
* Eventi di processo

### <a name="standalone-events"></a>Eventi autonomi
#### <a name="reference"></a>riferimento
            void SendEvent(string name, Dictionary<object, object> extras = null)

Possono verificarsi eventi di autonomo all'esterno di contesto hello di una sessione.

#### <a name="example"></a>Esempio
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a>Eventi di sessione
#### <a name="reference"></a>riferimento
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

Gli eventi di sessione sono azioni hello tooreport utilizzati in genere eseguite da un utente durante la sessione.

#### <a name="example"></a>Esempio
**Senza dati:**

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

**Con dati:**

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a>Eventi di processo
#### <a name="reference"></a>riferimento
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

Eventi relativi al processo sono azioni hello tooreport utilizzati in genere eseguite da un utente durante un processo.

#### <a name="example"></a>Esempio
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a>Segnalazione di errori
Esistono tre tipi di errore:

* Errori autonomi
* Errori di sessione
* Errori di processo

### <a name="standalone-errors"></a>Errori autonomi
#### <a name="reference"></a>riferimento
            void SendError(string name, Dictionary<object, object> extras = null)

Di fuori di contesto hello di una sessione possono verificarsi errori di toosession contrarie, errori autonomo.

#### <a name="example"></a>Esempio
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a>Errori di sessione
#### <a name="reference"></a>riferimento
            void SendSessionError(string name, Dictionary<object, object> extras = null)

Sessione gli errori in genere utilizzato tooreport hello conseguenze utente hello durante la sessione.

#### <a name="example"></a>Esempio
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a>Errori di processo
#### <a name="reference"></a>riferimento
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

Gli errori possono essere correlato tooa esecuzione processo anziché essere correlate toohello sessione utente.

#### <a name="example"></a>Esempio
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a>Segnalazione di arresti anomali
l'agente Hello fornisce due metodi toodeal con gli arresti anomali.

### <a name="send-an-exception"></a>Inviare un'eccezione
#### <a name="reference"></a>riferimento
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a>Esempio
È possibile inviare un'eccezione in qualsiasi momento chiamando:

            EngagementAgent.Instance.SendCrash(aCatchedException);

È inoltre possibile utilizzare una sessione di engagement hello tooterminate parametro facoltativo in hello stesso tempo rispetto all'invio di arresto anomalo di hello. toodo in tal caso, chiamare:

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

Se a tale scopo, processi e sessione hello verranno chiusa immediatamente dopo l'invio di arresto anomalo di hello.

### <a name="send-an-unhandled-exception"></a>Inviare un'eccezione non gestita
#### <a name="reference"></a>riferimento
            void SendCrash(Exception e)

Engagement fornisce inoltre un metodo toosend non gestite le eccezioni nel caso di **DISABILITATO** Engagement automatico **arresto anomalo del sistema** reporting. Ciò è particolarmente utile se utilizzato all'interno di gestore dell'evento UnhandledException applicazione hello.

Questo metodo verrà **sempre** terminare una sessione engagement hello e processi dopo la chiamata.

#### <a name="example"></a>Esempio
È possibile utilizzare tooimplement il proprio gestore UnhandledExceptionEventArgs. Ad esempio, aggiungere hello `Current_UnhandledException` metodo hello `App.xaml.cs` file:

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

In App.xaml.cs in "Public App(){}" aggiungere:

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a>Id dispositivo
            String EngagementAgent.Instance.GetDeviceId()

È possibile ottenere l'id dispositivo di engagement hello chiamando questo metodo.

## <a name="extras-parameters"></a>Parametri aggiuntivi
Dati arbitrari possono essere collegati tooan evento, un errore, un'attività o un processo. Tali dati possono essere strutturati utilizzando un dizionario. Chiavi e valori possono essere di qualsiasi tipo.

Se si desidera tooinsert un proprio tipo di funzionalità aggiuntive è tooadd un contratto dati per questo tipo, vengono serializzati i dati extra.

### <a name="example"></a>Esempio
Si crea una nuova classe "Person".

            using System.Runtime.Serialization;

            namespace Microsoft.Azure.Engagement
            {
              [DataContract]
              public class Person
              {
                public Person(string name, int age)
                {
                  Age = age;
                  Name = name;
                }

                // Properties

                [DataMember]
                public int Age
                {
                  get;
                  set;
                }

                [DataMember]
                public string Name
                {
                  get;
                  set; 
                }
              }
            }

Quindi, si aggiungerà un `Person` tooan istanza aggiuntiva.

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> Se si inseriscono altri tipi di oggetti, assicurarsi che il relativo metodo ToString () è implementato tooreturn una stringa leggibile.
> 
> 

### <a name="limits"></a>Limiti
#### <a name="keys"></a>Chiavi
Ogni chiave nell'oggetto hello deve corrispondere hello espressione regolare seguente:

`^[a-zA-Z][a-zA-Z_0-9]*$`

Questo significa che le chiavi devono iniziare con almeno una lettera, seguita da lettere, cifre o caratteri di sottolineatura (\_).

#### <a name="size"></a>Dimensione
Funzionalità aggiuntive sono troppo limitate**1024** caratteri per ogni chiamata.

## <a name="reporting-application-information"></a>Segnalazione di informazioni sull'applicazione
### <a name="reference"></a>riferimento
            void SendAppInfo(Dictionary<object, object> appInfos)

Manualmente, è possibile segnalare informazioni (o qualsiasi altra informazione di specifici dell'applicazione) usando hello SendAppInfo() funzione di rilevamento.

Si noti che questi dati possono essere inviati in modo incrementale: solo hello valore più recente per una determinata chiave verrà conservati per un determinato dispositivo. Ad esempio funzionalità aggiuntive di evento, utilizzare un dizionario\<oggetto,\> tooattach dati.

### <a name="example"></a>Esempio
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a>Limiti
#### <a name="keys"></a>Chiavi
Ogni chiave nell'oggetto hello deve corrispondere hello espressione regolare seguente:

`^[a-zA-Z][a-zA-Z_0-9]*$`

Questo significa che le chiavi devono iniziare con almeno una lettera, seguita da lettere, cifre o caratteri di sottolineatura (\_).

#### <a name="size"></a>Dimensione
Informazioni sull'applicazione è troppo limitati**1024** caratteri per ogni chiamata.

In hello esempio precedente, hello JSON inviato server toohello è 44 caratteri:

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a>Registrazione
### <a name="enable-logging"></a>Abilitare la registrazione
è possibile i log dei test tooproduce configurato nella console IDE hello Hello SDK.
Questi log non sono abilitati per impostazione predefinita. toocustomize, questa proprietà hello aggiornamento `EngagementAgent.Instance.TestLogEnabled` tooone del valore di hello disponibile hello `EngagementTestLogLevel` enumerazione, ad esempio:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

