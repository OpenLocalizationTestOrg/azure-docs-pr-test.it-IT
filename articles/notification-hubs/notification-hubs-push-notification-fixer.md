---
title: aaaAzure gli hub di notifica - linee guida di diagnosi
description: Linee guida su come toodiagnose comuni problemi con gli hub di notifica di Azure.
services: notification-hubs
documentationcenter: Mobile
author: ysxu
manager: erikre
editor: 
ms.assetid: b5c89a2a-63b8-46d2-bbed-924f5a4cce61
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: NA
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: e374278f2bfdfad36ba091e8846059cd184c17ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs---diagnosis-guidelines"></a>Hub di notifica di Azure - Linee guida sulla diagnostica
## <a name="overview"></a>Panoramica
Una delle domande più comuni di hello dei clienti di hub di notifica di Azure è una modalità di visualizzazione toofigure out perché non vedono una notifica inviata dal loro back-end dell'applicazione nel dispositivo client hello - dove e perché sono state eliminate le notifiche e come toofix questo. In questo articolo verranno esaminate hello vari motivi, perché le notifiche possono ottenere eliminate o non comporta il nei dispositivi hello. Esamineremo anche nei modi in cui è possibile analizzare e scoprire causa radice di hello. 

È in primo luogo, toounderstand critici come hub di notifica di Azure inserisce i dispositivi toohello notifiche.
![][0]

In un flusso di notifica di trasmissione tipico, il messaggio hello viene inviato da hello **back-end dell'applicazione** troppo**Hub di notifica di Azure (NH)** che a sua volta esegue alcune operazioni di elaborazione in tutte le registrazioni hello tenendo hello account configurato tag & toodetermine espressioni tag "destinazioni", ovvero tutte le registrazioni di hello che necessitano di notifica push di hello tooreceive. Queste registrazioni possono coprire alcune o tutte le piattaforme supportate: iOS, Google, Windows, Windows Phone, Kindle e Baidu per Android in Cina. Una volta stabilite le destinazioni hello, NH quindi effettua il push delle notifiche, suddiviso in più batch di registrazioni, toohello dispositivo specifico della piattaforma **Push Notification Service (PNS)** -ad esempio APN di Apple, GCM per via di Google. NH autentica con hello che PNS corrispondente in base alle credenziali di hello che è impostato in hello portale classico di Azure nella pagina Hub di notifica configurare hello. Hello PNS inoltra quindi hello notifiche toohello rispettivo **dispositivi client**. Si tratta di piattaforma hello le notifiche push toodeliver modo e si noti che parte finale di hello di recapito delle notifiche avviene tra la piattaforma di hello PNS e dispositivo hello consigliati. Si hanno pertanto quattro componenti principali: *client*, *back-end dell'applicazione*, *Hub di notifica di Azure (NH)* e *servizio di notifica push (PNS)*. Uno di questi componenti può essere la causa dell'eliminazione delle notifiche. Informazioni più dettagliate su questa architettura sono disponibili in [Panoramica dell'Hub di notifica].

Toodeliver errore possono verificarsi notifiche hello iniziale durante il test o gestione temporanea fase che potrebbe indicare un problema di configurazione o il problema può verificarsi nell'ambiente di produzione in cui tutte o alcune hello notifiche possono essere rilasciate che indica un'applicazione più approfondita o problema di modello di messaggistica. Nella sezione hello seguito verranno esaminati vari scenari di notifiche eliminato compreso tipo rari toohello comune, che alcuni dei quali è possibile ovvio e di altri non eccessiva. 

## <a name="azure-notifications-hub-mis-configuration"></a>Configurazione errata di Hub di notifica di Azure
Hub di notifica di Azure deve tooauthenticate stesso contesto hello di toohello di hello per gli sviluppatori applicazione toobe toosuccessfully in grado di inviare notifiche rispettivi PNS. Questo è reso possibile da sviluppatore hello la creazione di un account sviluppatore con la piattaforma di rispettivi hello (Google, Apple e così via Windows) e quindi la registrazione applicazione dove ottenere le credenziali che devono toobe configurate nel portale di hello in notifica Sezione di configurazione dell'hub. Se nessuna notifica apportano tramite, innanzitutto deve essere tooensure che le credenziali corrette hello siano configurate in hello Hub di notifica corrispondenza con un'applicazione hello creato sotto il proprio account sviluppatore specifico della piattaforma. Si noterà la [esercitazioni introduttive] toogo utile su questo processo in modo graduale. Ecco alcuni errori di configurazione comuni:

1. **Generale**
   
    a) verificare che il nome di hub di notifica (senza errori di digitazione) hello stesso che:
   
   * In cui si sta registrando da client hello, 
   * In cui si inviano notifiche dal back-end hello,  
   * In cui è stato configurato le credenziali PNS hello e 
   * Le cui credenziali di firma di accesso condiviso è stato configurato in hello back-end client e hello. 
     
     b) verificare che che si utilizzano stringhe di configurazione SAS corrette hello hello client e il back-end dell'applicazione hello. Come regola generale, è necessario utilizzare hello **DefaultListenSharedAccessSignature** sul client hello e **DefaultFullSharedAccessSignature** nel back-end dell'applicazione hello (che fornisce autorizzazioni toobe toosend in grado di notifica toohello NH)
2. **Configurazione del servizio di notifica push di Apple (APNS)**
   
    È necessario gestire due hub diversi, uno per la produzione e un altro a scopo di test. Ciò significa caricamento certificato hello che verrà toouse hub separato tooa di ambiente sandbox e certificato hello che verrà toouse nell'hub separato tooa di produzione. Non tentare di tipi diversi di tooupload di certificati toohello stesso hub perché potrebbe causare errori di notifica riga hello verso il basso. Se è necessario in una posizione in cui è stato caricato inavvertitamente diversi tipi di certificato toohello stesso hub, è consigliabile hub hello toodelete e avviare di nuovo. Se per qualche motivo, non si è in grado di toodelete hub di hello in hello molto meno, è necessario eliminare tutte le registrazioni esistenti hello dall'hub hello. 
3. **Configurazione di Google Cloud Messaging (GCM)** 
   
    a) Assicurarsi di abilitare "Google Cloud Messaging per Android" nel progetto cloud. 
   
    ![][2]
   
    b) verificare che si creano una chiave"Server", anche se ottenere le credenziali di hello quali NH useranno tooauthenticate con GCM. 
   
    ![][3]
   
    c) assicurarsi di assicurarsi di aver configurato nel client hello da un'entità interamente numerico che è possibile ottenere dal dashboard hello "ID progetto":
   
    ![][1]

## <a name="application-issues"></a>Problemi relativi all'applicazione
1) **Tag/Espressioni tag**

Se si utilizza tag o toosegment espressioni tag al pubblico, è sempre possibile che quando si inviano notifiche di hello, non vi è alcuna destinazione individuati in base alle espressioni tag/tag hello specificate nella chiamata a send. È consigliabile tooreview il tooensure registrazioni che sono presenti tag quali corrispondenza quando si invia una notifica e quindi verifica la conferma di notifica hello solo da client hello con le registrazioni. Ad esempio, Se tutte le registrazioni con NH sono state eseguite con pronunciare tag "Politica" e si invia una notifica con tag "Sport", non verrà inviato tooany dispositivo. Un caso complesso con espressioni tag è quello in cui la registrazione è stata eseguita solo con "Tag A" OPPURE "Tag B", ma durante l'invio delle notifiche si usa "Tag A & & Tag B" come destinazione. Hello diagnosticare autonomamente sezione suggerimenti di seguito, esistono modi in cui è possibile esaminare le registrazioni con tag in hello. 

2) **Problemi relativi ai modelli**

Se si usano i modelli di assicurarsi che vengano eseguite le istruzioni di hello descritte in [istruzioni modello]. 

3) **Registrazioni non valide**

Supponendo che sono state usate hello che hub di notifica è stato configurato correttamente e le espressioni tag/tag correttamente risultante nella casella Trova hello di destinazioni valide notifiche hello toowhich necessario toobe inviato, NH genera più batch l'elaborazione in parallelo, ogni batch l'invio di messaggi tooa set di registrazioni. 

> [!NOTE]
> Poiché è hello l'elaborazione in parallelo, Microsoft non garantisce l'ordine hello in cui hello verranno recapitate notifiche. 
> 
> 

A questo punto, Hub di notifica di Azure è ottimizzato per un modello di recapito "at-most-once" per i messaggi, Ciò significa che si tenta una deduplicazione in modo che non vengono consegnate le notifiche più di una volta tooa dispositivo. tooensure è esaminare registrazioni hello e assicurarsi che solo un messaggio viene inviato per l'identificatore del dispositivo prima dell'invio effettivamente hello messaggio toohello PNS. Ogni batch viene inviato toohello PNS, che a sua volta accetta e convalida le registrazioni hello, è possibile che hello PNS rileva un errore con uno o più registrazioni hello in un batch, restituisce un tooAzure errore NH e arresta l'elaborazione in tal modo eliminazione che batch completamente. Questo vale soprattutto per gli APNS che usano un protocollo di flusso TCP. Sebbene ci stiamo ottimizzati per in più una volta recapito, in questo caso è rimuovere hello registrazione errore il database e tentativi di recapito delle notifiche per il resto di hello di dispositivi hello in batch.

È possibile ottenere informazioni sull'errore per il tentativo di mancato recapito hello in una registrazione utilizzando le API REST di hub di notifica di Azure hello: [per ogni messaggio di telemetria: ottenere dati di telemetria messaggio di notifica](https://msdn.microsoft.com/library/azure/mt608135.aspx) e [PNS Feedback](https://msdn.microsoft.com/library/azure/mt705560.aspx). Vedere hello [SendRESTExample](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/SendRestExample) ad esempio di codice.

## <a name="pns-issues"></a>Problemi relativi a PNS
Una volta che ha ricevuto il messaggio di notifica hello hello rispettivi PNS è responsabilità toodeliver hello notifica toohello periferica. Hub di notifica di Azure rientra in questo caso l'immagine hello e non ha alcun controllo quando o se verrà recapitati dispositivo toohello toobe notifica hello. Poiché i servizi di notifica della piattaforma hello sono molto affidabili, le notifiche tendono dispositivi hello tooreach in pochi secondi da hello PNS. Se hello PNS tuttavia limita gli hub di notifica di Azure applica una strategia di backoff esponenziale e se hello PNS rimane non raggiungibile per 30 minuti è quindi presente un criterio in tooexpire inserire ed eliminare i messaggi in modo permanente. 

Se un sistema PNS toodeliver una notifica di prova ma hello dispositivo è offline, notifica hello è archiviata da hello PNS per un periodo di tempo limitato e consegnata toohello dispositivo quando diventa disponibile. Viene archiviata solo una notifica recente per una determinata app. Se più notifiche vengono inviate quando il dispositivo di hello è offline, ogni nuova notifica causa preavviso hello toobe eliminati. Questo comportamento di mantenere solo la notifica più recente hello è tooas cui coalescing notifiche in APNS e la compressione di GCM (che usa una chiave di compressione). Se il dispositivo hello rimane offline per un lungo periodo, vengono eliminate tutte le notifiche che è state archiviate per tale. Fonte: [Linee guida sul servizio APN] & [Linee guida su GCM]

Con l'hub di notifica di Azure - è possibile passare una chiave coalescing tramite un'intestazione HTTP utilizzando hello generico `SendNotification` API (ad esempio SDK per .NET- `SendNotificationAsync`) che accetta anche le intestazioni HTTP che vengono passate come è toohello rispettivi PNS. 

## <a name="self-diagnose-tips"></a>Suggerimenti per l'utente relativi alla diagnostica
Qui verranno presi in esame hello vari toodiagnose vie e radice provochi problemi Hub di notifica:

### <a name="verify-credentials"></a>Verificare le credenziali
1. **Portale per sviluppatori PNS**
   
    La verifica in hello rispettivi PNS developer portal (APN, GCM, WNS e così via) tramite il nostro [esercitazioni introduttive].
2. **Portale di Azure classico**
   
    Andare toohello Configura scheda tooreview e corrispondere alle credenziali hello con quelli ottenuti dal portale per sviluppatori di hello PNS. 
   
    ![][4]

### <a name="verify-registrations"></a>Verificare le registrazioni
1. **Visual Studio**
   
    Se si utilizza Visual Studio per lo sviluppo è possibile connettersi tooMicrosoft Azure e visualizzare e gestire una serie di servizi Azure, incluso l'Hub di notifiche da "Esplora Server". Questo risulta particolarmente utile per l'ambiente sviluppo/test. 
   
    ![][9]
   
    È possibile visualizzare e gestire tutte le registrazioni hello nell'hub che sono perfettamente suddivisi in categorie per piattaforma, nativa o modello di registrazione, tag, identificatore PNS, data di scadenza hello e di id di registrazione. È anche possibile modificare una registrazione volo hello - che risulta utile ad esempio se si desidera tooedit eventuali tag. 
   
    ![][8]
   
   > [!NOTE]
   > Le registrazioni tooedit funzionalità di Visual Studio devono essere utilizzate solo durante sviluppo/test con un numero limitato di registrazioni. Se vi si verifica un toofix necessario prendere in considerazione le registrazioni in blocco, con funzionalità di registrazione di esportazione/importazione hello descritta in questo articolo - [registrazioni di esportazione/importazione](https://msdn.microsoft.com/library/dn790624.aspx)
   > 
   > 
2. **Service Bus Explorer**
   
    Molti clienti usano Service Bus Explorer (descritto in [Service Bus Explorer] ) per visualizzare e gestire l'hub di notifica. Si tratta di un progetto open source disponibile su code.microsoft.com - [codice di Service Bus Explorer]

### <a name="verify-message-notifications"></a>Verificare le notifiche di messaggi
1. **Portale di Azure classico**
   
    È possibile passare client tooyour toohello "Debug" scheda toosend test notifiche senza la necessità di qualsiasi servizio back-end di e in esecuzione. 
   
    ![][7]
2. **Visual Studio**
   
    È anche possibile inviare notifiche di prova da volevano realizzare hello di Visual Studio:
   
    ![][10]
   
    È possibile leggere altre on hello Azure di Visual Studio notifica Hub Esplora funzionalità 
   
   * [Informazioni generali su Esplora server di Visual Studio]
   * [Post di blog su Esplora server di Visual Studio - 1]
   * [Post di blog su Esplora server di Visual Studio - 2]

### <a name="debug-failed-notifications-review-notification-outcome"></a>Eseguire il debug di notifiche non riuscite/esaminare l'esito della notifica
**Proprietà EnableTestSend**

Quando si invia una notifica tramite hub di notifica, inizialmente solo Ottiene messo in coda per toodo NH elaborazione toofigure out tutte le relative destinazioni e quindi infine NH invia toohello PNS. Ciò significa che quando si utilizza l'API REST o uno qualsiasi dei client hello SDK, hello restituzione ha esito positivo della trasmissione chiamata unico mezzo che hello messaggio è stato correttamente messo in coda con Hub di notifica. Non fornisce informazioni su cosa è successo quando NH ricevuto infine toosend hello messaggio tooPNS. Se la notifica non è in arrivo nel dispositivo client hello, esiste la possibilità che quando NH tentato toodeliver hello messaggio tooPNS, si è verificato un errore, ad esempio, dimensioni del payload hello stato superato il massimo dal PNS hello hello o hello credenziali configurate in NH sono non valido e così via tooget un approfondite errori PNS hello, è stata introdotta una proprietà denominata [EnableTestSend funzionalità]. Questa proprietà viene abilitata automaticamente quando si invia i messaggi generati dal portale di hello o client di Visual Studio di test e consente pertanto toosee dettagliate informazioni di debug. È possibile utilizzare questo valore tramite l'API richiede ad esempio hello hello .NET SDK in cui è disponibile e sarà aggiunto tooall client SDK alla fine. toouse con chiamata REST hello, aggiungere un parametro di stringa di query denominato "test" alla fine hello la chiamata di trasmissione, ad esempio 

    https://mynamespace.servicebus.windows.net/mynotificationhub/messages?api-version=2013-10&test

*Esempio (.NET SDK)*

Si supponga di che utilizzare .NET SDK toosend una notifica di tipo avviso popup nativo:

    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName);
    var result = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(result.State);

`result.State`verrà semplicemente stato `Enqueued` alla fine di hello dell'esecuzione di hello senza qualsiasi comprensione di ciò che si sono verificati tooyour push. È ora possibile usare hello `EnableTestSend` proprietà booleana durante l'inizializzazione di hello `NotificationHubClient` e può ottenere lo stato dettagliato sugli errori PNS hello durante l'invio di notifiche di hello. chiamata di trasmissione Hello qui richiederà ulteriore tempo tooreturn perché solo restituisce dopo NH ha recapitato risultato di hello notifica tooPNS toodetermine hello. 

    bool enableTestSend = true;
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName, enableTestSend);

    var outcome = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(outcome.State);

    foreach (RegistrationResult result in outcome.Results)
    {
        Console.WriteLine(result.ApplicationPlatform + "\n" + result.RegistrationId + "\n" + result.Outcome);
    }

*Output di esempio*

    DetailedStateAvailable
    windows
    7619785862101227384-7840974832647865618-3
    hello Token obtained from hello Token Provider is wrong

Questo messaggio indica credenziali non valide sono configurate nell'hub di notifica hello o un problema con le registrazioni hello hub hello e hello consigliato corso verrà toodelete la registrazione e consentire a client hello ricrearlo prima di inviare hello Messaggio. 

> [!NOTE]
> Si noti che l'utilizzo hello di questa proprietà è molto limitato e pertanto è necessario utilizzare solo tale nell'ambiente di sviluppo/test con un set limitato di registrazioni. È solo inviare notifiche di debug too10 dispositivi. È necessario anche un limite di elaborazione debug invia toobe 10 al minuto. 
> 
> 

### <a name="review-telemetry"></a>Esaminare i dati di telemetria
1. **Usare il portale di Azure classico**
   
    portale Hello consente tooget una rapida panoramica di tutte le attività hello su Hub di notifica. 
   
    a) dalla scheda "dashboard" hello è possibile visualizzare una visualizzazione aggregata di registrazioni hello, notifiche, nonché gli errori per ogni piattaforma. 
   
    ![][5]
   
    b) è anche possibile aggiungere molti altri parametri specifici di piattaforma da hello "Monitoraggio" scheda tootake un'analisi approfondita relativa, in particolare a eventuali errori specifici PNS restituito quando NH tenta toosend hello notifica toohello PNS. 
   
    ![][6]
   
    c) deve iniziare con revisione hello **i messaggi in arrivo**, **operazioni di registrazione**, **notifiche operazioni riuscite** e quindi passare hello tooreview di tooper piattaforma scheda Errori specifici PNS. 
   
    d) nel caso di notifica hello hub configurato correttamente con le impostazioni di autenticazione hello quindi si verrà visualizzato l'errore di autenticazione PNS. Si tratta delle credenziali PNS hello toocheck buona indicazione. 

2) **Accesso a livello di codice**

Per informazioni dettagliate: 

* [Accesso alla telemetria a livello di codice]
* [Esempio di accesso alla telemetria tramite API] 

> [!NOTE]
> Molte funzionalità correlate alla telemetria, come l'**esportazione/importazione di registrazioni** e l'**accesso alla telemetria tramite API**, sono disponibili solo con il livello Standard. Se si tenta di toouse queste funzionalità se si è nel piano gratuito o Basic quindi si otterranno effetto toothis messaggio di eccezione durante l'utilizzo di hello SDK e un HTTP 403 (accesso negato) quando vengono utilizzati direttamente dal hello API REST. Assicurarsi che sia stato spostato verticale tooStandard livello tramite il portale classico di Azure.  
> 
> 

<!-- IMAGES -->
[0]: ./media/notification-hubs-diagnosing/Architecture.png
[1]: ./media/notification-hubs-diagnosing/GCMConfigure.png
[2]: ./media/notification-hubs-diagnosing/GCMEnable.png
[3]: ./media/notification-hubs-diagnosing/GCMServerKey.png
[4]: ./media/notification-hubs-diagnosing/PortalConfigure.png
[5]: ./media/notification-hubs-diagnosing/PortalDashboard.png
[6]: ./media/notification-hubs-diagnosing/PortalMonitoring.png
[7]: ./media/notification-hubs-diagnosing/PortalTestNotification.png
[8]: ./media/notification-hubs-diagnosing/VSRegistrations.png
[9]: ./media/notification-hubs-diagnosing/VSServerExplorer.png
[10]: ./media/notification-hubs-diagnosing/VSTestNotification.png

<!-- LINKS -->
[Panoramica dell'Hub di notifica]: notification-hubs-push-notification-overview.md
[esercitazioni introduttive]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[istruzioni modello]: https://msdn.microsoft.com/library/dn530748.aspx 
[Linee guida sul servizio APN]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW4
[Linee guida su GCM]: http://developer.android.com/google/gcm/adv.html
[Export/Import Registrations]: http://msdn.microsoft.com/library/dn790624.aspx
[Service Bus Explorer]: http://msdn.microsoft.com/library/dn530751.aspx
[codice di Service Bus Explorer]: https://code.msdn.microsoft.com/windowsazure/Service-Bus-Explorer-f2abca5a
[Informazioni generali su Esplora server di Visual Studio]: http://msdn.microsoft.com/library/windows/apps/xaml/dn792122.aspx 
[Post di blog su Esplora server di Visual Studio - 1]: http://azure.microsoft.com/blog/2014/04/09/deep-dive-visual-studio-2013-update-2-rc-and-azure-sdk-2-3/#NotificationHubs 
[Post di blog su Esplora server di Visual Studio - 2]: http://azure.microsoft.com/blog/2014/08/04/announcing-release-of-visual-studio-2013-update-3-and-azure-sdk-2-4/ 
[EnableTestSend funzionalità]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx
[Accesso alla telemetria a livello di codice]: http://msdn.microsoft.com/library/azure/dn458823.aspx
[Esempio di accesso alla telemetria tramite API]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel

