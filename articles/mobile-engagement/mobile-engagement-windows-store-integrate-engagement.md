---
title: Integrazione di Universal App Engagement SDK aaaWindows
description: Come tooIntegrate Azure Mobile Engagement con App universali di Windows
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 71236b68-5ebd-44aa-8c82-c7ca8098ea05
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 18543798099c233dbe55cc387ba0216e369c8596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a>Integrazione di Engagement SDK per app universali di Windows
> [!div class="op_single_selector"]
> * [Windows universale](mobile-engagement-windows-store-integrate-engagement.md) 
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [iOS](mobile-engagement-ios-integrate-engagement.md) 
> * [Android](mobile-engagement-android-integrate-engagement.md) 
> 
> 

Questa procedura descrive Engagement tooactivate di modo più semplice di hello Analitica e il monitoraggio funzioni nell'applicazione Windows universale.

Hello seguendo i passaggi è che sufficienti tooactivate hello dei log è necessario un report toocompute tutte le statistiche relative agli utenti, sessioni, attività, arresti anomali del sistema e Technicals. Hello dei log è necessario un report toocompute altre statistiche quali processi, errori ed eventi devono essere eseguiti manualmente tramite API di Engagement hello (vedere [come toouse hello avanzate tag API in app universali di Windows di Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md) poiché Queste statistiche sono dipende dall'applicazione.

## <a name="supported-versions"></a>Versioni supportate
Hello Mobile Engagement SDK per App universali di Windows può essere integrato solo in Windows Runtime e nelle applicazioni di Universal Windows Platform destinazione:

* Windows 8
* Windows 8.1
* Windows Phone 8.1
* Windows 10 (versioni per desktop e portatili)

> [!NOTE]
> Se si sono destinati a Windows Phone Silverlight, vedere toohello [procedura di integrazione di Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).
> 
> 

## <a name="install-hello-mobile-engagement-universal-apps-sdk"></a>Installare hello Mobile Engagement SDK di App universale
### <a name="all-platforms"></a>Tutte le piattaforme
Hello Engagement SDK per Windows Universal App per dispositivi mobili è disponibile come pacchetto Nuget chiamato *MicrosoftAzure.MobileEngagement*. È possibile installarlo dal hello Gestione pacchetti Nuget di Visual Studio.

### <a name="windows-8x-and-windows-phone-81"></a>Windows 8.x e Windows Phone 8.1
NuGet consente di distribuire automaticamente le risorse SDK hello in hello `Resources` cartella hello radice del progetto di applicazione.

### <a name="windows-10-universal-windows-platform-applications"></a>Applicazioni UWP di Windows 10
NuGet non distribuisce automaticamente le risorse SDK hello nell'applicazione UWP ancora. È possibile toodo manualmente fino a ottenere la distribuzione di risorse viene reintrodotto in NuGet:

1. Aprire Esplora file.
2. Passare toohello seguente posizione (**x.x. x** versione hello di coinvolgimento che si sta installando): *% USERPROFILE %\\.nuget\packages\MicrosoftAzure.MobileEngagement\\*  *x.x. x**\\content\win81*
3. Trascinamento della selezione hello **risorse** cartella hello file Esplora toohello radice del progetto in Visual Studio.
4. In Visual Studio selezionare il progetto e attivare hello **Mostra tutti i file** icona sopra hello **Esplora**.
5. Alcuni file non sono inclusi nel progetto hello. tooimport li contemporaneamente, fare clic sul hello **risorse** cartella **Escludi dal progetto** quindi un altro a destra fare clic su hello **risorse** cartella **inclusione nel progetto** toore-includono l'intera cartella hello. Tutti i file da hello **risorse** cartella sono ora inclusi nel progetto.

## <a name="add-hello-capabilities"></a>Aggiungere le funzionalità di hello
Hello Engagement SDK richiede alcune funzionalità di Windows SDK di hello in ordine toowork correttamente.

Aprire il `Package.appxmanifest` file e assicurarsi che vengono dichiarati tale hello seguenti funzionalità:

* `Internet (Client)`

## <a name="initialize-hello-engagement-sdk"></a>Inizializzare hello Engagement SDK
### <a name="engagement-configuration"></a>Configurazione di Engagement
configurazione di Engagement Hello è centralizzata in hello `Resources\EngagementConfiguration.xml` file del progetto.

Modificare questo toospecify file:

* La stringa di connessione dell'applicazione tra i tag `<connectionString>` and `<\connectionString>`.

Se si desidera che in fase di esecuzione, invece, si può chiamare seguente hello toospecify metodo prima dell'inizializzazione dell'agente di Engagement hello:

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

stringa di connessione Hello per l'applicazione viene visualizzato nel portale di Azure classico hello.

### <a name="engagement-initialization"></a>Inizializzazione di Engagement
Quando si crea un nuovo progetto, viene generato un file `App.xaml.cs` . Questa classe eredita da `Application` e contiene molti metodi importanti. Verrà inoltre utilizzato tooinitialize hello Engagement SDK.

Modificare hello `App.xaml.cs`:

* Aggiungere tooyour `using` istruzioni:
  
      using Microsoft.Azure.Engagement;
* Definire un'inizializzazione di Engagement hello tooshare metodo una volta per tutte le chiamate:
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* Chiamare `InitEngagement` in hello `OnLaunched` metodo:
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* Quando l'applicazione viene avviata con uno schema personalizzato, un altro tipo di riga di comando dell'applicazione o hello hello quindi `OnActivated` metodo viene chiamato. Quando viene attivato l'app, è inoltre necessario tooinitiate hello Engagement SDK. toodo in tal caso, eseguire l'override `OnActivated` metodo:
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> Non è fortemente consigliabile è tooadd hello Engagement inizializzazione in un'altra posizione dell'applicazione.
> 
> 

## <a name="basic-reporting"></a>Segnalazione di base
### <a name="recommended-method-overload-your-page-classes"></a>Metodo consigliato: eseguire l'overload delle classi `Page`
Report hello tooactivate order di tutti i log di hello richiesto da Engagement toocompute utenti, sessioni, attività, arresti anomali del sistema e le statistiche tecniche, puoi semplicemente far tutti i `Page` sottoclassi ereditano hello `EngagementPage` classi.

Di seguito è riportato un esempio di come toodo per una pagina dell'applicazione. È possibile eseguire hello stessa operazione per tutte le pagine dell'applicazione.

#### <a name="c-source-file"></a>File di origine C#
Modificare il file `.xaml.cs` della pagina:

* Aggiungere tooyour `using` istruzioni:
  
      using Microsoft.Azure.Engagement;
* Sostituire `Page` con `EngagementPage`:

**Senza Engagement:**

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

**Con Engagement:**

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> Se la pagina esegue l'override di hello `OnNavigatedTo` metodo toocall assicurarsi di essere `base.OnNavigatedTo(e)`. In caso contrario, attività hello non verranno segnalati (hello `EngagementPage` chiamate `StartActivity` all'interno di relativo `OnNavigatedTo` (metodo)).
> 
> 

#### <a name="xaml-file"></a>File XAML
Modificare il file `.xaml` della pagina:

* Aggiungere le dichiarazioni di spazi dei nomi tooyour:
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* Sostituire `Page` con `engagement:EngagementPage`:

**Senza Engagement:**

        <Page>
            <!-- layout -->
            ...
        </Page>

**Con Engagement:**

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-hello-default-behaviour"></a>Eseguire l'override di comportamento predefinito di hello
Per impostazione predefinita, il nome di classe hello della pagina hello viene segnalato come nome dell'attività hello con senza aggiuntivi. Se la classe hello utilizza il suffisso "Pagina" hello, Engagement verrà inoltre rimosso.

Se si desidera il comportamento predefinito di hello toooverride per nome hello, è sufficiente aggiungere questo codice tooyour:

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

Se si desidera tooreport alcune informazioni aggiuntive con l'attività, è possibile aggiungere questo codice tooyour:

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

Questi metodi vengono chiamati all'interno di hello `OnNavigatedTo` metodo della pagina.

### <a name="alternate-method-call-startactivity-manually"></a>Metodo alternativo: chiamare `StartActivity()` manualmente
Se non è possibile o non si desidera toooverload il `Page` classi, invece, è possibile avviare le attività chiamando `EngagementAgent` diretta dei metodi.

È consigliabile toocall `StartActivity` all'interno del `OnNavigatedTo` metodo della pagina.

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> Assicurarsi che la sessione venga terminata correttamente.
> 
> SDK di Windows universale Hello chiama automaticamente hello `EndActivity` metodo quando un'applicazione hello viene chiuso. È pertanto **elevata** consigliato hello toocall `StartActivity` metodo ogni volta che cambia attività hello dell'utente di hello e troppo**mai** chiamata hello `EndActivity` (metodo), questo metodo invia tooEngagement server che l'utente corrente dispone di un'applicazione hello lasciare, ciò influisce su tutti i log dell'applicazione.
> 
> 

## <a name="advanced-reporting"></a>Segnalazione avanzata
Facoltativamente, è opportuno tooreport eventi specifici di applicazione, gli errori e processi e toodo, pertanto, utilizzare hello altri metodi, vedere hello `EngagementAgent` classe. Hello Engagement API consente toouse tutte le funzionalità avanzate di Engagement.

Per ulteriori informazioni, vedere [come toouse hello avanzate tag API in app universali di Windows di Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md).

## <a name="advanced-configuration"></a>Configurazione avanzata
### <a name="disable-automatic-crash-reporting"></a>Disabilitare la segnalazione automatica degli arresti anomali
È possibile disabilitare hello automatica degli arresti anomali delle funzionalità di impegno report. Quindi, quando si verifica un'eccezione non gestita, Engagement non effettuerà alcuna azione.

> [!WARNING]
> Se si prevede di toodisable questa funzionalità, tenere presente che quando si verifica un arresto anomalo del sistema non gestita nell'app, Engagement non invierà arresto anomalo di hello **AND** non comporta la chiusura della sessione hello e processi.
> 
> 

toodisable automatico segnalazioni di arresti anomali, personalizzare solo la configurazione a seconda della modalità di hello è stata dichiarata:

#### <a name="from-engagementconfigurationxml-file"></a>Dal file `EngagementConfiguration.xml`
Impostare i report dell'arresto anomalo troppo`false` tra `<reportCrash>` e `</reportCrash>` tag.

#### <a name="from-engagementconfiguration-object-at-run-time"></a>Dall'oggetto `EngagementConfiguration` in fase di esecuzione
Impostare toofalse di arresto anomalo di report utilizzando l'oggetto EngagementConfiguration.

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a>Modalità burst
Per impostazione predefinita, i report del servizio di Engagement hello registra in tempo reale. Se l'applicazione segnala molto spesso i registri, è preferibile toobuffer hello registri e tooreport usarle in una sola volta in volta regolare base (è chiamata hello "modalità burst").

toodo in tal caso, chiamare il metodo hello:

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

argomento Hello è un valore in **millisecondi**. In qualsiasi momento, se si desidera registrare in tempo reale di tooreactivate hello, chiamare solo metodo hello senza alcun parametro, o con valore 0 hello.

Hello modalità burst leggermente aumentare batteria hello vita ma ha un impatto sulle hello Engagement Monitor: durata di tutte le sessioni e i processi sarà arrotondato toohello burst soglia (in questo modo, le sessioni e i processi è inferiore a soglia burst hello potrebbe non essere visibile). È consigliabile toouse una soglia di potenziamento non più di 30000 (30 s). È necessario tenere presente che registri salvati sono elementi too300 limitato toobe. Se l'invio richiede troppo tempo, è possibile che alcuni log vadano persi.

> [!WARNING]
> soglia di potenziamento Hello non può essere configurata tooa periodo minore 1s. Se si tenta pertanto toodo, hello SDK sarà visualizzare una traccia con l'errore hello e verrà automaticamente reimpostato valore predefinito di toohello, ad esempio, 0. In questo modo verrà attivata hello SDK tooreport hello log in tempo reale.
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

