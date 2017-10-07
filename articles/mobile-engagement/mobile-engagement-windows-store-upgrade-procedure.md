---
title: le procedure di aggiornamento SDK di Universal App aaaWindows
description: Procedure di aggiornamento di Windows Universal Apps SDK per Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 4c898175-2cd6-43db-b350-bb408332f24d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 95aba5d55cd65d4190aad35737f872414b5ed443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a>Procedure di aggiornamento di Windows Universal Apps SDK
Se è già stata integrata una versione precedente di Engagement all'interno dell'applicazione, è necessario hello tooconsider seguenti punti quando si aggiorna hello SDK.

È possibile toofollow varie procedure se sono saltate diverse versioni di hello SDK. Ad esempio se si esegue la migrazione da 0.10.1 too0.11.0 è toofirst seguire hello "da 0.9.0 too0.10.1" routine quindi hello "da 0.10.1 too0.11.0" stored procedure.

## <a name="from-330-too340"></a>Da 3.3.0 too3.4.0
### <a name="test-logs"></a>Log di test
Registri della console prodotti da hello SDK ora possono essere attivato/disattivato/filtrato. toocustomize, questa proprietà hello aggiornamento `EngagementAgent.Instance.TestLogEnabled` tooone del valore di hello disponibile hello `EngagementTestLogLevel` enumerazione, ad esempio:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a>Risorse
sovrapposizione di copertura Hello è stata migliorata. È parte di risorse del pacchetto NuGet SDK hello.

Durante l'aggiornamento toohello nuova versione di hello SDK è possibile scegliere che se si desidera tookeep i file esistenti da hello sovrapposizione cartella delle risorse o non:

* Se sovrapposizione precedente hello è alle proprie esigenze o se si sta integrando hello `WebView` elementi manualmente, quindi è possibile decidere tookeep i file esistenti, continuerà a funzionare. 
* Se si desidera tooupdate toohello nuovo sovrapposizione, sostituire semplicemente hello intero `overlay` cartella dalle risorse con hello uno nuovo dal pacchetto SDK hello (app UWP: dopo l'aggiornamento di hello, è possibile ottenere la nuova cartella sovrapposizione di hello da % USERPROFILE %\\. nuget\ packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).

> [!WARNING]
> Utilizzando sovrapposizione nuovo hello sovrascriverà le personalizzazioni apportate in una versione precedente di hello.
> 
> 

## <a name="from-320-too330"></a>Da 3.2.0 too3.3.0
### <a name="resources"></a>Risorse
Questo passaggio riguarda solo le risorse personalizzate. Se sono state personalizzate le risorse di hello fornite da hello SDK (html, immagini, sovrapposizione), è necessario toobackup li prima l'aggiornamento e riapplicare la personalizzazione in aggiornato risorse.

## <a name="from-310-too320"></a>Da 3.1.0 too3.2.0
### <a name="resources"></a>Risorse
Questo passaggio riguarda solo le risorse personalizzate. Se sono state personalizzate le risorse di hello fornite da hello SDK (html, immagini, sovrapposizione), è necessario toobackup li prima l'aggiornamento e riapplicare la personalizzazione in aggiornato risorse.

### <a name="webview-integration"></a>l'integrazione di visualizzazione Web
In questa versione, sono stati introdotti alcuni miglioramenti toomatch diversi form factor. Assicurarsi che l'integrazione di webview hello corrisponda esempio hello:

Nella pagina XAML ():

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

E nel file con estensione cs associato:

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated toowithin a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

              #region tooimplement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update hello webview when hello app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update hello webview when hello app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure toodetach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are hello current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements toohello correct size.
              /// </summary>
              /// <param name="width">hello width of your current display.</param>
              /// <param name="height">hello height of your current display.</param>
              private void SetWebView(double width, double height)
              {
                #pragma warning disable 4014
                CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal,
                        () =>
                        {
                          this.engagement_notification_content.Width = width;
                          this.engagement_announcement_content.Width = width;
                          this.engagement_announcement_content.Height = height;
                        });
              }

              /// <summary>
              /// Handler that takes hello Windows.Current.SizeChanged and indicates that webviews have toobe resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes hello ApplicationView.VisibleBoundsChanged and indicates that webviews have toobe resized
              /// </summary>
              /// <param name="sender">hello related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-too300"></a>Da 2.0.0 too3.0.0
### <a name="resources"></a>Risorse
Questo passaggio riguarda solo le risorse personalizzate. Se sono state personalizzate le risorse di hello fornite da hello SDK (html, immagini, sovrapposizione), è necessario toobackup li prima l'aggiornamento e riapplicare la personalizzazione in aggiornato risorse.

## <a name="from-111-too200"></a>Da 1.1.1 too2.0.0
Hello seguenti viene descritto come toomigrate un'integrazione SDK da hello Capptain servizio offerto da Capptain SAS in un'app con Azure Mobile Engagement. 

> [!IMPORTANT]
> Capptain e Mobile Engagement non sono hello stessi servizi e procedura di hello indicata di seguito solo evidenziata come toomigrate hello app client. Migrazione hello SDK nell'applicazione hello verrà non la migrazione dei dati dai server di hello Capptain server toohello Mobile Engagement
> 
> 

Se si esegue la migrazione da una versione precedente, consultare prima hello Capptain sito web toomigrate too1.1.1 quindi applicare hello procedura

### <a name="nuget-package"></a>Pacchetto NuGet
Sostituire **Capptain.WindowsPhone** con il pacchetto NuGet **MicrosoftAzure.MobileEngagement**.

### <a name="applying-mobile-engagement"></a>Applicazione di Mobile Engagement
Hello SDK viene utilizzato il termine hello `Engagement`. È necessario tooupdate toomatch il progetto questa modifica.

È necessario toouninstall il pacchetto nuget Capptain corrente. Si consideri che verranno rimosse tutte le modifiche nella cartella Risorse di Capptain. Se si desidera tookeep tali file, creare una copia di essi.

Successivamente, installare il pacchetto di hello nuovo impegno di Microsoft Azure nuget nel progetto. È possibile trovarlo direttamente su [sito Web di NuGet] o nell'indice qui. Sostituisce questa azione, tutti i file di risorse utilizzate da Engagement e hello nuova DLL Engagement tooyour aggiunge i riferimenti al progetto.

Hai tooclean riferimenti del progetto eliminando i riferimenti DLL Capptain. Se non si apporta questa, versione di hello di Capptain è in conflitto e si verificheranno gli errori.

Se è stato personalizzato Capptain risorse, copiare il contenuto del file precedente e incollarli in nuovi file di Engagement hello. Si noti che i file xaml sia cs toobe aggiornato.

Dopo avere completato questi passaggi è sufficiente tooreplace precedente Capptain i riferimenti basati sui nuovi riferimenti di Engagement hello.

1. Tutti gli spazi dei nomi di Capptain avere toobe aggiornato.
   
    Prima della migrazione:
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    Dopo la migrazione:
   
        using Microsoft.Azure.Engagement;
2. Tutte le classi Capptain che contengono "Capptain" devono contenere "Engagement".
   
    Prima della migrazione:
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    Dopo la migrazione:
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. Per i file xaml cambiano anche attributi e spazio dei nomi di Capptain.
   
    Prima della migrazione:
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    Dopo la migrazione:
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. Modifiche alle pagine di sovrimpressione
   
   > [!IMPORTANT]
   > Anche la sovrimpressione cambia. Il nuovo spazio dei nomi è `Microsoft.Azure.Engagement.Overlay`. Ha toobe utilizzato nei file xaml e cs. Inoltre `CapptainGrid` toobe denominato `EngagementGrid`, `capptain_notification_content` e `capptain_announcement_content` sono denominati `engagement_notification_content` e `engagement_announcement_content`.
   > 
   > 
   
    Per la sovrimpressione:
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    Diventa:
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. Per hello altre risorse quali immagini Capptain e file HTML, si noti che sono anche stati rinominati toouse "Engagement".

### <a name="project-declaration"></a>Dichiarazione di progetto
In Package.appxmanifest `File Type Associations` è stato aggiornato da:

* capptain\_raggiungere\_tooengagement contenuto\_raggiungere\_contenuto
* capptain\_log\_file tooengagement\_log\_file

### <a name="application-id--sdk-key"></a>ID applicazione / chiave SDK
Engagement utilizza una stringa di connessione. Non si dispone toospecify un ID applicazione e una chiave SDK con Engagement Mobile, è sufficiente toospecify una stringa di connessione. È possibile configurarla nel file EngagementConfiguration.

configurazione di Engagement Hello può essere impostate nel `Resources\EngagementConfiguration.xml` file del progetto.

Modificare questo toospecify file:

* La stringa di connessione dell'applicazione tra i tag `<connectionString>` and `<\connectionString>`.

Se si desidera che in fase di esecuzione, invece, si può chiamare seguente hello toospecify metodo prima dell'inizializzazione dell'agente di Engagement hello:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

stringa di connessione Hello per l'applicazione viene visualizzato nel portale di Azure classico hello.

### <a name="items-name-change"></a>Modifica del nome di elementi
Tutti gli elementi denominati *capptain* sono stati rinominati in *engagement*. Analogamente, per *Capptain* troppo*Engagement*.

Esempi di elementi di Capptain di uso comune:

* CapptainConfiguration è diventato EngagementConfiguration
* CapptainAgent è diventato EngagementAgent
* CapptainReach è diventato EngagementReach
* CapptainHttpConfig è diventato EngagementHttpConfig
* GetCapptainPageName è diventato GetEngagementPageName

Si noti la ridenominazione influisce anche sui metodi sottoposti a override.

