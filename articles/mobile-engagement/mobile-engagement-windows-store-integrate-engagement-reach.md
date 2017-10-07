---
title: Integrazione di SDK a raggiungere Universal App aaaWindows
description: Come tooIntegrate Azure Mobile Engagement raggiunge con App universali di Windows
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a31ca1d6-856f-4aec-898a-07969ae5f7ec
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: af311c65940014083333853875a00173b8d6783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a>Integrazione di Reach SDK per app universali di Windows
Attenersi alla procedura di integrazione hello descritta in hello [integrazione di Windows universale Engagement SDK](mobile-engagement-windows-store-integrate-engagement.md) prima di seguire questa Guida.

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-universal-project"></a>Incorporare hello Engagement Reach SDK nel progetto Windows universale
Non è un valore tooadd. `EngagementReach` sono già presenti nel progetto.

> [!TIP]
> È possibile personalizzare le immagini si trova in hello `Resources` cartella del progetto, in particolare hello marchio icona (tale impostazione predefinita toohello Engagement). Per le app universali è inoltre possibile spostare hello `Resources` cartella tooshare del progetto condiviso il contenuto tra le app, ma si disporrà di hello tookeep `Resources\EngagementConfiguration.xml` di file nel percorso predefinito è dipendente dalla piattaforma.
> 
> 

## <a name="enable-hello-windows-notification-service"></a>Abilitare il servizio di notifica di Windows hello
### <a name="windows-8x-and-windows-phone-81-only"></a>Solo Windows 8.x e Windows Phone 8.1
In hello toouse ordine **servizio di notifica Windows** (definito WNS) nei `Package.appxmanifest` file nel `Application UI` fare clic su `All Image Assets` nella casella a sinistra bot hello. In hello destra della casella hello `Notifications`, modificare `toast capable` da `(not set)` troppo`(Yes)`.

### <a name="all-platforms"></a>Tutte le piattaforme
È necessario toosynchronize dell'app tooyour Microsoft account e toohello engagement della piattaforma. Per questo è necessario un account toocreate o accedere [Centro sviluppatori windows](https://dev.windows.com). Dopo la creazione di una nuova applicazione e trovare hello SID e una chiave privata. Nel server front-end engagement hello, passare l'impostazione di app in `native push` e incollare le credenziali. Dopo questa operazione, fare clic sul progetto, selezionare `store` e `Associate App with hello Store...`. È sufficiente un'applicazione hello tooselect hanno creata prima toosynchronize.

## <a name="initialize-hello-engagement-reach-sdk"></a>Inizializzare hello Engagement Reach SDK
Modificare hello `App.xaml.cs`:

* Inserire `EngagementReach.Instance.Init` subito dopo `EngagementAgent.Instance.Init` nel metodo `InitEngagement`:
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  Hello `EngagementReach.Instance.Init` viene eseguito in un thread dedicato. Non è toodo è manualmente.

> [!NOTE]
> Se si usano le notifiche push in un' posizione nell'applicazione, è troppo[condividono il canale di push](#push-channel-sharing) con copertura di Engagement.
> 
> 

## <a name="integration"></a>Integrazione
Engagement fornisce il banner in-app copertura di due modi tooadd hello e visualizzazioni intermedi per sondaggi nell'applicazione e gli annunci: hello sovrapporre di integrazione e l'integrazione di hello web viste manuale. È consigliabile non combinare entrambe approccio hello stessa pagina.

scelta di Hello tra integrazione due hello può essere riepilogata in questo modo:

* È possibile scegliere di integrazione di sovrapposizione hello se le pagine eredita già da hello agente `EngagementPage`, è sufficiente sostituire `EngagementPage` da `EngagementPageOverlay` e `xmlns:engagement="using:Microsoft.Azure.Engagement"` da `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` nelle pagine.
* È possibile scegliere integrazione manuale di hello web viste se si desidera tooprecisely sul posto hello raggiungere dell'interfaccia utente all'interno di pagine o se non si desidera tooadd pagine di livello tooyour ereditarietà un'altra. 

### <a name="overlay-integration"></a>Integrazione di una sovrimpressione
sovrapposizione di Engagement Hello aggiunge in modo dinamico gli elementi dell'interfaccia utente di hello utilizzati campagne Reach toodisplay nella pagina. Se hello sovrapposizione non soddisfa il layout è consigliabile visualizzazioni web hello integrazione manuale invece.

Modifica file con estensione XAML `EngagementPage` riferimento troppo`EngagementPageOverlay`

* Aggiungere le dichiarazioni di spazi dei nomi tooyour:
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* Sostituire `engagement:EngagementPage` con `engagement:EngagementPageOverlay`:

**Con EngagementPage:**

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

**Con EngagementPageOverlay:**

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

Quindi, nel file con estensione cs contrassegnare la pagina in `EngagementPageOverlay` anziché `EngagementPage` e importare `Microsoft.Azure.Engagement.Overlay`.

            using Microsoft.Azure.Engagement.Overlay;

* Sostituire `EngagementPage` con `EngagementPageOverlay`:

**Con EngagementPage:**

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

**Con EngagementPageOverlay:**

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


Aggiunge Hello sovrapposizione Engagement un `Grid` elemento nella parte superiore della pagina è composto di layout e hello due `WebView` elementi uno per hello banner e hello altra visualizzazione hello intermedi.

È possibile personalizzare elementi di sovrapposizione hello direttamente in hello `EngagementPageOverlay.cs` file.

### <a name="web-views-manual-integration"></a>Integrazione manuale delle visualizzazioni Web
Copertura verrà eseguita la ricerca delle pagine per hello due `WebView` elementi responsabili della visualizzazione messaggio hello e visualizzazione intermedi hello. Hello solo cosa toodo è tooadd questi due `WebView` elementi in un punto qualsiasi delle pagine, di seguito è riportato un esempio:

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


In questo hello esempio `WebView` elementi sono toofit estesa relativo contenitore che automaticamente ridimensionato nuovamente tali in caso di modifica delle dimensioni dello schermo rotazione o la finestra.

> [!WARNING]
> È importante tookeep hello stessa denominazione `engagement_notification_content` e `engagement_announcement_content` per hello `WebView` elementi. Reach li identifica dal nome. 
> 
> 

## <a name="handle-datapush-optional"></a>Gestire il push di dati (facoltativo)
Se si desidera il push di dati applicazione toobe tooreceive in grado di raggiungere, è necessario tooimplement due eventi di classe EngagementReach hello:

In App.xaml.cs nel costruttore App() hello aggiungere:

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

Quindi, impostare il contenuto di hello di hello `EngagementReach.Instance.Handler` campo con l'oggetto personalizzato nel `App.xaml.cs` classe all'interno di hello `App()` metodo.

**Codice di esempio:**

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> Per impostazione predefinita, Engagement usa una specifica implementazione di `EngagementReachHandler`.
> Non è toocreate personalizzata, e se in tal caso, non è necessario toooverride ogni metodo. comportamento predefinito di Hello è oggetto di base di tooselect hello Engagement.
> 
> 

### <a name="web-view"></a>Visualizzazione Web
Per impostazione predefinita, Reach utilizzerà hello incorporato di risorse di notifiche di hello DLL toodisplay hello e pagine.

una procedura completa di tooprovide il possibilità di personalizzazione si utilizza solo la visualizzazione web. Se si desidera toocustomize layout, eseguire l'override direttamente i file di risorse hello `EngagementAnnouncement.html` e `EngagementNotification.html`. Engagement deve tutto il codice in `<body></body>` toorun correttamente. ma è possibile aggiungere tag esterni a `engagement_webview_area`.

Tuttavia, è possibile decidere toouse le risorse.

È possibile eseguire l'override `EngagementReachHandler` i metodi toouse di Engagement tootell la sottoclasse i layout, ma utilizzare meccanismo engagement di attenzione tooembedded hello:

**Codice di esempio:**

            // In your subclass of EngagementReachHandler

            public override string GetAnnouncementHTML()
            {
              return base.GetAnnouncementHTML();
            }
            public override string GetAnnouncementName()
            {
              return base.GetAnnouncementName();
            }
            public override string GetNotfificationHTML()
            {
              return base.GetNotfificationHTML();
            }
            public override string GetNotfificationName()
            {
              return base.GetNotfificationName();
            }


Per impostazione predefinita, AnnouncementHTML è `ms-appx-web:///Resources/EngagementAnnouncement.html`. Rappresenta i file html hello che progettazione hello contenuto di un messaggio push (annuncio di testo, anoucement Web e di annuncio di polling). AnnouncementName è `engagement_announcement_content`. È il nome di hello della progettazione di webview hello nella pagina xaml.

NotificationHTML è `ms-appx-web:///Resources/EngagementNotification.html`. Rappresenta i file html hello che progettare hello notifica di un messaggio di push. NotificationName è `engagement_notification_content`. È il nome di hello della progettazione di webview hello nella pagina xaml.

### <a name="customization"></a>Personalizzazione
È possibile personalizzare la visualizzazione Web di notifiche e annunci nel modo desiderato se si mantiene l'oggetto Engagement. Fare attenzione che oggetto webview descritto tre volte - hello prima volta in xaml, secondo periodo di tempo in file con estensione cs nel metodo "setwebview()" hello e infine ora nel file html hello.

* In xaml è descrivere il componente corrente layout grafico webview hello.
* Nel file con estensione cs è possibile definire "setwebview()" in cui si imposta la dimensione hello di hello webview due (notifica, annuncio). È molto utile durante il ridimensionamento di un'applicazione hello.
* Nel file html di Engagement hello è descrivere hello webview contenuto, progettazione e hello posizioni di elementi tra loro.

### <a name="launch-message"></a>Messaggio di avvio
Quando un utente fa clic su una notifica di sistema (un tipo di avviso popup), Engagement avvia un'applicazione hello, carico hello contenuto di hello il push dei messaggi e visualizzare la pagina hello campagna corrispondente hello.

Si verifica un ritardo tra l'avvio di hello del display di applicazione e hello hello della pagina hello (a seconda della velocità di hello della rete).

utente di toohello tooindicate che si sta caricando, è necessario fornire un informazioni visive, ad esempio una barra di stato o un indicatore di stato. Engagement non è in grado di gestire questa situazione, ma fornisce alcuni gestori.

aggiungere i callback di hello tooimplement, in App.xaml.cs "Pubblica App() {}":

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

È possibile impostare il callback di hello nel metodo "Public App() {}" con il `App.xaml.cs` file, preferibilmente prima hello `EngagementReach.Instance.Init()` chiamare.

> [!TIP]
> Ogni gestore viene chiamato dal Thread UI hello. Non si dispone tooworry quando si utilizza un MessageBox o qualcosa correlate all'interfaccia utente.
> 
> 

## <a id="push-channel-sharing"></a> Condivisione del canale push
Se si utilizza le notifiche push per uno scopo diverso nell'applicazione è necessario canale di push hello toouse funzionalità di hello Engagement SDK per la condivisione. Si tratta di push tooavoid mancante.

* È possibile fornire la propria inizializzazione di copertura di Engagement toohello push del canale. Hello SDK utilizzeranno anziché richiedere uno nuovo.

Aggiornare l'inizializzazione di copertura di Engagement hello con il canale di push in hello `InitEngagement` metodo hello `App.xaml.cs` file:

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* In alternativa, se si desidera tooconsume hello push canale dopo l'inizializzazione di copertura hello è possibile impostare un callback sul canale di copertura di Engagement tooget hello push dopo averla creata da hello SDK.

Impostare il callback nel punto in cui **dopo** hello Reach inizializzazione:

    /* Set action on hello SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* hello forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a>Suggerimento per lo schema
È possibile utilizzare uno schema personalizzato. È possibile inviare un tipo diverso di URI da engagement front-end toobe utilizzato nell'applicazione engagement. Lo schema predefinito come `http, ftp, ...` è gestito da Windows. Una finestra chiederà se nel dispositivo sono installate applicazioni predefinite. È possibile anche creare uno schema personalizzato per l'applicazione.

Hello semplice tooset uno schema personalizzato nell'applicazione è tooopen il `Package.appxmanifest` andare in `Declarations` pannello. Selezionare `Protocol` in hello dichiarazioni disponibili scorrere casella e aggiungerlo. Modifica hello `Name` campo con il protocollo di nuovo il nome desiderato.

Ora toouse questo protocollo, modificare il `App.xaml.cs` con hello `OnActivated` (metodo) e non dimenticare di engagement tooinitialize qui anche:

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action toodo when app is launch

              #region Custom scheme use
              if (args.Kind == ActivationKind.Protocol)
              {
                ProtocolActivatedEventArgs myProtocol = (ProtocolActivatedEventArgs)args;

                if (myProtocol.Uri.Scheme.Equals("protocolName"))
                {
                  string path = myProtocol.Uri.AbsolutePath;
                }
              }
              #endregion

