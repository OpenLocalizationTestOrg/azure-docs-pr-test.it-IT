---
title: aaaHow toouse gli hub di notifica con Java
description: Informazioni su come toouse gli hub di notifica di Azure da un linguaggio back-end.
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 4c3f966d-0158-4a48-b949-9fa3666cb7e4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: java
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: afcf305b1acd9ee28ee4889040ece59d9399d29d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-java"></a>Come toouse gli hub di notifica da Java
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

In questo argomento descrive le funzionalità principali di hello di ufficiale hello nuovo completamente supportata SDK per Java Hub di notifica di Azure. Si tratta di un progetto open source ed è possibile visualizzare l'intero codice SDK hello in [SDK per Java]. 

In generale, è possibile accedere tutte le funzionalità di hub di notifica da un server back-end utilizzabile come Java, PHP, Python o Ruby utilizzando l'interfaccia REST di Hub di notifica di hello come descritto nell'argomento MSDN hello [API REST degli hub di notifica](http://msdn.microsoft.com/library/dn223264.aspx). L'SDK per Java fornisce un semplice wrapper per le interfacce REST in Java. 

Hello SDK supporta attualmente:

* CRUD in Hub di notifica 
* CRUD in Registrazioni
* Gestione dell'installazione
* Importazione/esportazione di registrazioni
* Invii regolari
* Invii pianificati
* Operazioni asincrone tramite Java NIO
* Piattaforme supportate: APNS (iOS), GCM (Android), WNS (app di Windows Store), MPNS(Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android senza servizi Google) 

## <a name="sdk-usage"></a>Uso dell'SDK
### <a name="compile-and-build"></a>Compilazione e creazione
Usare [Maven]

toobuild:

    mvn package

## <a name="code"></a>Codice
### <a name="notification-hub-cruds"></a>CRUD di Hub di notifica
**Creare un oggetto NamespaceManager:**

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

**Creare un hub di notifica:**

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 OPPURE

    hub = new NotificationHub("connection string", "hubname");

**Ottenere un hub di notifica:**

    hub = namespaceManager.getNotificationHub("hubname");

**Aggiornare un hub di notifica:**

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

**Eliminare un hub di notifica:**

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a>CRUD di registrazione
**Creare un client di Hub di notifica:**

    hub = new NotificationHub("connection string", "hubname");

**Creare una registrazione per Windows:**

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

**Creare una registrazione per iOS:**

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

Analogamente, è possibile creare registrazioni per Android (GCM), Windows Phone (MPNS) e Kindle Fire (ADM).

**Creare registrazioni modello:**

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

**Creare registrazioni usando il modello create registrationid + upsert**

Rimuove i duplicati a causa delle risposte tooany perdita se l'archiviazione degli ID di registrazione nel dispositivo hello:

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

**Aggiornare registrazioni:**

    hub.updateRegistration(reg);

**Eliminare registrazioni:**

    hub.deleteRegistration(regid);

**Effettuare query di registrazioni:**

* **Ottenere una singola registrazione:**
  
    hub.getRegistration(regid);
* **Ottenere tutte le registrazioni nell'hub:**
  
    hub.getRegistrations();
* **Ottenere registrazioni con tag:**
  
    hub.getRegistrationsByTag("myTag");
* **Ottenere registrazioni per canale:**
  
    hub.getRegistrationsByChannel("devicetoken");

Tutte le query di raccolta supportano i token $top e di continuazione.

### <a name="installation-api-usage"></a>Uso dell'API di installazione
L'API di installazione rappresenta un meccanismo alternativo per la gestione delle registrazioni. Anziché gestire più registrazioni che non è semplice e può essere eseguita facilmente in modo errato o uso inefficiente, è ora possibile toouse oggetto una singola installazione. L'installazione contiene tutti gli elementi necessari: il canale push (token del dispositivo), tag, modelli, riquadri secondari (per WNS e APN). Non più necessario toocall hello servizio tooget Id - semplicemente generare GUID o qualsiasi altro identificatore, mantenerli nel dispositivo e inviano back-end tooyour insieme canale push (token del dispositivo). Nel back-end hello deve eseguire solo una singola chiamata:, quindi CreateOrUpdateInstallation, è completamente idempotente, è disponibile tooretry se necessario.

Un esempio per Amazon Kindle Fire è simile al seguente:

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

Se si desidera tooupdate è: 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

Per scenari avanzati si dispone di funzionalità di aggiornamento parziale che consente di toomodify solo determinate proprietà degli oggetti installazione hello. L'aggiornamento parziale è essenzialmente un subset di operazioni Patch JSON che è possibile eseguire in un oggetto di installazione.

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

Eliminare l'installazione:

    hub.deleteInstallation(installation.getInstallationId());

Le operazioni CreateOrUpdate, Patch e Delete saranno coerenti con l'operazione Get. L'operazione richiesta appena diventa toohello coda di sistema durante la chiamata di hello e verrà eseguito in background. Si noti che Get non è progettato per uno scenario di runtime principale, ma solo per il debug e risoluzione dei problemi è strettamente limitato dal servizio hello.

Flusso di trasmissione per le installazioni è hello come per le registrazioni. È stato introdotto solo toohello di notifica tootarget un'opzione particolare installazione - utilizza solo tag "InstallationId: {desired-id}". Nel caso riportato sopra l'aspetto dovrebbe essere simile al seguente:

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

Per uno dei diversi modelli:

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a>Pianificare le notifiche (disponibile per il livello STANDARD)
Hello stesso trasmissione regolare ma con un parametro aggiuntivo - scheduledTime che indica quando deve essere recapitata la notifica. Il servizio accetta qualsiasi data e ora da 5 minuti a sette giorni a partire dalla data e ora correnti.

**Pianificare una notifica nativa di Windows:**

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a>Importazione/esportazione (disponibile per il livello STANDARD)
Talvolta è necessario tooperform massa contro le registrazioni. È in genere per l'integrazione con un altro sistema o solo una correzione massive toosay aggiornamento hello tag. Non è fortemente consigliabile toouse flusso Get o l'aggiornamento se stiamo parlando migliaia di registrazioni. Funzionalità di importazione/esportazione è uno scenario di hello toocover progettato. Forniscono sostanzialmente un contenitore di blob toosome di accesso con l'account di archiviazione come origine di dati in arrivo e il percorso per l'output.

**Inviare il processo di esportazione:**

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


**Inviare il processo di importazione:**

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

**Attendere fino al completamento del processo:**

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

**Ottenere tutti i processi:**

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

**URI con firma:** è hello URL di alcuni file blob o contenitore blob più set di parametri, quali le autorizzazioni e l'ora di scadenza e firma di tutte queste operazioni eseguite tramite la chiave di firma di accesso condiviso dell'account. L'SDK per Java di Archiviazione di Azure dispone di funzionalità avanzate, compresa la creazione di tale tipo di URI. Come alternativa semplice è possibile dare un'occhiata ImportExportE2E classe di test (dal percorso di github hello) che è molto di base e compact implementazione dell'algoritmo di firma.

### <a name="send-notifications"></a>Inviare notifiche
oggetto notifica Hello è semplicemente un corpo con intestazioni, alcuni metodi di utilità della Guida nella creazione di oggetti di notifiche hello nativo e modello.

* **Windows Store e Windows Phone 8.1 (non Silverlight)**
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* **iOS**
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* **Android**
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* **Windows Phone 8.0 e 8.1 Silverlight**
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* **Kindle Fire**
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* **Inviare tooTags**
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* **Inviare tootag espressione**       
  
        hub.sendNotification(n, "foo && ! bar");
* **Inviare una notifica modello**
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

Quando si esegue il codice Java, dovrebbe essere visualizzata una notifica sul dispositivo di destinazione.

## <a name="next-steps"></a>Passaggi successivi
In questo argomento illustrato come toocreate un linguaggio semplice REST client per gli hub di notifica. A questo punto è possibile:

* Scaricare hello completo [SDK per Java], che contiene tutto il codice SDK hello. 
* Provare a usare hello esempi:
  * [Introduzione ad Hub di notifica]
  * [Inviare le ultime notizie]
  * [Inviare le ultime notizie localizzate]
  * [Inviare notifiche agli utenti di tooauthenticated]
  * [Inviare notifiche di multipiattaforma tooauthenticated utenti]

[SDK per Java]: https://github.com/Azure/azure-notificationhubs-java-backend
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[Introduzione ad Hub di notifica]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/
[Inviare le ultime notizie]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/
[Inviare le ultime notizie localizzate]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/
[Inviare notifiche agli utenti di tooauthenticated]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/
[Inviare notifiche di multipiattaforma tooauthenticated utenti]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/
[Maven]: http://maven.apache.org/

