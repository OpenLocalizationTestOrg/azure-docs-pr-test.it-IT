---
title: Integrazione di Phone Silverlight raggiungere SDK aaaWindows
description: Come tooIntegrate Azure Mobile Engagement raggiunge con App di Windows Phone Silverlight
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d3516a6b-db9f-4cdb-a475-4148edf81af1
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 09c8767216e11963c5c600755ab8d4d11cd92034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a>Integrazione dell'SDK di Reach per Windows Phone Silverlight
Attenersi alla procedura di integrazione hello descritta in hello [integrazione SDK di Windows Phone Silverlight Engagement](mobile-engagement-windows-phone-integrate-engagement.md) prima di seguire questa Guida.

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a>Incorporare hello Engagement Reach SDK nel progetto Windows Phone Silverlight
Non è un valore tooadd. `EngagementReach` sono già presenti nel progetto.

> [!TIP]
> È possibile personalizzare le immagini si trova in hello `Resources` cartella del progetto, in particolare hello marchio icona (tale impostazione predefinita toohello Engagement).
> 
> 

## <a name="add-hello-capabilities"></a>Aggiungere le funzionalità di hello
Hello Engagement Reach SDK richiede alcune funzionalità aggiuntive.

Aprire il `WMAppManifest.xml` file e assicurarsi che vengono dichiarati tale hello seguenti funzionalità:

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

Hello prima di tutto è utilizzato da visualizzazione hello MPNS servizio tooallow hello della notifica di tipo avviso popup. Hello secondo è tooembed usato un'attività di browser in hello SDK.

Modifica hello `WMAppManifest.xml` file e aggiungere all'interno di hello `<Capabilities />` tag:

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-hello-microsoft-push-notification-service"></a>Abilitare hello servizio notifica Push Microsoft
In hello toouse ordine **servizio notifica Push Microsoft** (definito MPNS) il `WMAppManifest.xml` file deve avere un `<App />` tag con un `Publisher` attributo impostato toohello nome del progetto.

## <a name="initialize-hello-engagement-reach-sdk"></a>Inizializzare hello Engagement Reach SDK
### <a name="engagement-configuration"></a>Configurazione di Engagement
configurazione di Engagement Hello è centralizzata in hello `Resources\EngagementConfiguration.xml` file del progetto.

Modificare questa configurazione di copertura toospecify file:

* *Parametro facoltativo*, indicare se è attivato il push nativo hello (MPNS) o non è compreso tra `<enableNativePush>` e `</enableNativePush>` tag, (`true` per impostazione predefinita).
* *Parametro facoltativo*, indicare il nome del canale di push hello tra hello `<channelName>` e `</channelName>` tag, forniscono hello stesso che l'applicazione può utilizzare o lasciare vuoto il campo attualmente.

Se si desidera che in fase di esecuzione, invece, si può chiamare seguente hello toospecify metodo prima dell'inizializzazione dell'agente di Engagement hello:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether hello native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide hello same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> È possibile specificare il nome di hello di hello MPNS push canale dell'applicazione. Per impostazione predefinita, Engagement crea un nome in base a appId hello. Non si dispone di alcuna necessità toospecify hello nome manualmente, tranne se si prevede di canale di push toouse hello di fuori di Engagement.
> 
> 

### <a name="engagement-initialization"></a>Inizializzazione di Engagement
Modificare hello `App.xaml.cs`:

* Aggiungere tooyour `using` istruzioni:
  
      using Microsoft.Azure.Engagement;
* Inserire `EngagementReach.Instance.Init` subito dopo `EngagementAgent.Instance.Init` in `Application_Launching`:
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* Inserisci `EngagementReach.Instance.OnActivated` in hello `Application_Activated` metodo:
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> Hello `EngagementReach.Instance.Init` viene eseguito in un thread dedicato. Non è toodo è manualmente.
> 
> 

## <a name="app-store-submission-considerations"></a>Considerazioni sull'invio di notifiche di App Store
Microsoft impone alcune regole quando si usano le notifiche push hello:

Da Microsoft hello [criteri di applicazione] documentazione, sezione 2.9:

1) È necessario richiedere le notifiche push hello utente tooaccept tooreceive. Nelle impostazioni, quindi aggiungere le notifiche push hello toodisable un modo.

oggetto EngagementReach Hello fornisce due metodi toomanage hello opt-in/opt-out, `EnableNativePush()` e `DisableNativePush()`. Potrebbe, ad esempio, creare un'opzione nelle impostazioni di hello con un elemento toggle di toodisable o abilitare MPNS.

È inoltre possibile decidere toodeactivate MPNS tramite la configurazione di Engagement hello\<windows-phone-sdk-reach-configurazione\>.

> 2.9.1) applicazione hello innanzitutto deve descrivere hello notifiche toobe fornito e **ottenere l'autorizzazione dell'utente hello (acconsentire esplicitamente)**, e **deve fornire un meccanismo tramite cui hello utente può rifiutare esplicitamente la ricezione le notifiche push**. Tutte le notifiche fornite tramite servizio notifica Push Microsoft hello devono essere coerenti con l'utente di toohello descrizione fornita hello e devono conformarsi a tutte applicabile [criteri di applicazione] [ Content Policies]e [requisiti aggiuntivi per i tipi di applicazione specifico].
> 
> 

2) Non fare un uso eccessivo delle notifiche push. Engagement gestisce le notifiche in modo automatico.

> 2.9.2) applicazione hello e l'utilizzo del servizio notifica Push Microsoft hello deve essere non eccessivamente utilizzare capacità di rete o della larghezza di banda di servizio notifica Push Microsoft hello, o in caso contrario eccessivamente sovraccarica un Windows Phone o altro dispositivo di Microsoft o un servizio con un numero eccessivo push delle notifiche, come stabilito da Microsoft a propria discrezione e non deve compromettere o interferire con le reti di Microsoft Server o qualsiasi server di terze parti o reti connesse toohello servizio notifica Push Microsoft.
> 
> 

3) Non basarsi sulle informazioni di criticals toosend MPNS. Engagement Usa MPNS, in modo da questa regola si applica anche per le campagne hello create all'interno di hello Engagement front-end.

> 2.9.3) hello servizio notifica Push Microsoft potrebbe non essere notifiche toosend utilizzati che vengono mission-critical o in caso contrario potrebbe incidere sulle questioni della priorità, inclusi, a condizione o dispositivo medico di limitazione le notifiche critiche tooa correlati. MICROSOFT espressamente declina qualsiasi garanzia che hello uso di hello MICROSOFT PUSH NOTIFICATION servizio o recapito di MICROSOFT PUSH notifica servizio notifiche verrà essere senza interruzioni, errore disponibile, o in caso contrario garantito tooOCCUR ON A in tempo reale base.
> 
> 

**È possibile garantire che l'applicazione passerà il processo di convalida hello se non si rispettano questi suggerimenti.**

## <a name="handle-data-push-optional"></a>Gestire il push di dati (facoltativo)
Se si desidera il push di dati applicazione toobe tooreceive in grado di raggiungere, è necessario tooimplement due eventi di classe EngagementReach hello:

    EngagementReach.Instance.DataPushStringReceived += (body) =>
    {
       Debug.WriteLine("String data push message received: " + body);
       return true;
    };

    EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
    {
       Debug.WriteLine("Base64 data push message received: " + encodedBody);
       // Do something useful with decodedBody like updating an image view
       return true;
    };

È possibile visualizzare il callback di hello di ogni metodo restituisce un valore booleano. Engagement invia un feedback tooits back-end dopo l'invio di push di dati hello. Se il callback di hello restituisce false, hello `exit` feedback verrà inviato. In caso contrario, il feedback sarà `action`. Se il callback non è impostato per gli eventi di hello, hello `drop` commenti e suggerimenti verranno restituiti tooEngagement.

> [!WARNING]
> Engagement non è in grado di tooreceive feedback multipli per il push di dati. Se si intende tooset diversi gestori di un evento, tenere presente che il feedback hello corrisponderà toohello ultimo quello inviato. In questo caso, è consigliabile tooalways restituisce hello stesso tooavoid valore determinato confusione commenti e suggerimenti su hello front-end.
> 
> 

## <a name="customize-ui-optional"></a>Personalizzare l'interfaccia utente (facoltativo)
### <a name="first-step"></a>Primo passaggio
Abbiamo consentono di raggiungere hello toocustomize dell'interfaccia utente.

toodo, è necessario toocreate una sottoclasse di hello `EngagementReachHandler` classe.

**Codice di esempio:**

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

Quindi, impostare il contenuto di hello di hello `EngagementReach.Instance.Handler` campo con l'oggetto personalizzato nel `App.xaml.cs` classe all'interno di hello `Application_Launching` metodo.

**Codice di esempio:**

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> Per impostazione predefinita, Engagement usa una specifica implementazione di `EngagementReachHandler`. Non è toocreate personalizzata, e se in tal caso, non è necessario toooverride ogni metodo. comportamento predefinito di Hello è oggetto di base di tooselect hello Engagement.
> 
> 

### <a name="layouts"></a>Layout
Per impostazione predefinita, Reach utilizzerà hello incorporato di risorse di notifiche di hello DLL toodisplay hello e pagine.

Tuttavia, è possibile decidere toouse tooreflect proprie risorse il marchio in questi componenti.

È possibile eseguire l'override `EngagementReachHandler` metodi toouse di Engagement tootell la sottoclasse i layout:

**Codice di esempio:**

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetPollUri()
    {
       // return hello path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> Hello `CreateNotification` metodo può restituire null. non verrà visualizzata la notifica Hello e campagna di copertura hello verrà eliminata.
> 
> 

toosimplify l'implementazione del layout, è inoltre possibile usare nostro xaml che può essere utilizzato come base per il codice. Si trovano nell'archivio di Engagement SDK hello (o src/reach /).

> [!WARNING]
> origini di Hello fornito da Microsoft sono hello utilizziamo esatte stesse. Pertanto, se si desidera toomodify li direttamente, non dimenticare dello spazio dei nomi di toochange hello e hello nome.
> 
> 

### <a name="notification-position"></a>Posizione di notifica
Per impostazione predefinita, viene visualizzata una notifica di nell'applicazione in hello sul lato inferiore sinistro di un'applicazione hello. È possibile modificare questo comportamento eseguendo l'override di hello `GetNotificationPosition` metodo hello `EngagementReachHandler` oggetto.

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of hello EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

Attualmente, è possibile scegliere tra hello `BOTTOM` (impostazione predefinita) e `TOP` posizioni.

### <a name="launch-message"></a>Messaggio di avvio
Quando un utente fa clic su una notifica di sistema (un tipo di avviso popup), avvia Engagement hello app, carico hello contenuto di hello il push dei messaggi e visualizzare la pagina hello per hello corrispondente della campagna.

Si verifica un ritardo tra l'avvio di hello del display di applicazione e hello hello della pagina hello (a seconda della velocità di hello della rete).

utente di toohello tooindicate che si sta caricando, è necessario fornire un informazioni visive, ad esempio una barra di stato o un indicatore di stato. Engagement non è in grado di gestire questa situazione, ma fornisce alcuni gestori.

tooimplement hello callback, eseguire:

    /* hello application has launched and hello content is loading.
     * You should display an indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

    /* hello application has finished loading hello content and hello page
     * is about toobe displayed.
     * You should hide hello indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

    /* hello content has been loaded, but an error has occurred.
     * You can provide an information toohello user.
     * You should hide hello indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

È possibile impostare il callback di hello nel `Application_Launching` metodo i `App.xaml.cs` file, preferibilmente prima hello `EngagementReach.Instance.Init()` chiamare.

> [!TIP]
> Ogni gestore viene chiamato dal Thread UI hello. Non si dispone tooworry quando si utilizza un MessageBox o qualcosa correlate all'interfaccia utente.
> 
> 

[criteri di applicazione]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
[requisiti aggiuntivi per i tipi di applicazione specifico]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx

