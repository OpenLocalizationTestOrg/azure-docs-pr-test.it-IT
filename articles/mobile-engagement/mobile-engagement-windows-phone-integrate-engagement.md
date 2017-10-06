---
title: Integrazione di Phone Silverlight Engagement SDK aaaWindows
description: Come tooIntegrate Azure Mobile Engagement con le app di Windows Phone Silverlight
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 447fea8d-f4e3-4ad4-8ec0-8e3cf1ad3ab0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f65683a62e5256cea469a3a73d99ade4331cb6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a>Integrazione di Mobile Engagement SDK per Windows Phone Silverlight
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md) 
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [iOS](mobile-engagement-ios-integrate-engagement.md) 
> * [Android](mobile-engagement-android-integrate-engagement.md) 
> 
> 

Questa procedura descrive hello più semplice modo tooactivate Azure Mobile Engagement Analitica e funzioni nell'applicazione Windows Phone Silverlight di monitoraggio.

Hello seguendo i passaggi è che sufficienti tooactivate hello dei log è necessario un report toocompute tutte le statistiche relative agli utenti, sessioni, attività, arresti anomali del sistema e Technicals. Hello dei log è necessario un report toocompute altre statistiche quali processi, errori ed eventi devono essere eseguiti manualmente tramite API di Engagement hello (vedere [come toouse hello avanzate Mobile Engagement tag API nelle applicazioni Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md) di seguito) poiché queste statistiche sono dipendenti dall'applicazione.

## <a name="supported-versions"></a>Versioni supportate
Hello Mobile Engagement SDK per Silverlight per Windows può essere integrato solo in applicazioni destinate a:

* Windows Phone 8.0
* Windows Phone 8.1 Silverlight

> [!NOTE]
> Se si sono destinati a Windows Phone 8.1 (non Silverlight), fare riferimento toohello [procedura di integrazione di Windows universale](mobile-engagement-windows-store-integrate-engagement.md).
> 
> 

## <a name="install-hello-mobile-engagement-silverlight-sdk"></a>Installare hello Mobile Engagement Silverlight SDK
Hello Mobile Engagement SDK per Silverlight per Windows è disponibile come pacchetto Nuget chiamato *MicrosoftAzure.MobileEngagement*. È possibile installarlo dal hello Gestione pacchetti Nuget di Visual Studio. 

## <a name="add-hello-capabilities"></a>Aggiungere le funzionalità di hello
Hello Engagement SDK richiede alcune funzionalità di Windows Phone Silverlight SDK di hello in ordine toowork correttamente.

Aprire il `WMAppManifest.xml` file e assicurarsi che tale hello seguenti funzionalità vengono dichiarati in hello `Capabilities` pannello:

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-hello-engagement-sdk"></a>Inizializzare hello Engagement SDK
### <a name="engagement-configuration"></a>Configurazione di Engagement
configurazione di Engagement Hello è centralizzata in hello `Resources\EngagementConfiguration.xml` file del progetto.

Modificare questo toospecify file:

* La stringa di connessione dell'applicazione tra i tag `<connectionString>` and `<\connectionString>`.

Se si desidera che in fase di esecuzione, invece, si può chiamare seguente hello toospecify metodo prima dell'inizializzazione dell'agente di Engagement hello:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

stringa di connessione Hello per l'applicazione viene visualizzato nel portale di Azure classico hello.

### <a name="engagement-initialization"></a>Inizializzazione di Engagement
Quando si crea un nuovo progetto, viene generato un file `App.xaml.cs` . Questa classe eredita da `Application` e contiene molti metodi importanti. Verrà inoltre utilizzato tooinitialize hello Engagement SDK.

Modificare hello `App.xaml.cs`:

* Aggiungere tooyour `using` istruzioni:
  
      using Microsoft.Azure.Engagement;
* Inserisci `EngagementAgent.Instance.Init` in hello `Application_Launching` metodo:
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* Inserisci `EngagementAgent.Instance.OnActivated` in hello `Application_Activated` metodo:
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> Non è fortemente consigliabile è tooadd hello Engagement inizializzazione in un'altra posizione dell'applicazione. Tuttavia, tenere presente che hello `EngagementAgent.Instance.Init` metodo viene eseguito in un thread dedicato e non su hello thread dell'interfaccia utente.
> 
> 

## <a name="basic-reporting"></a>Segnalazione di base
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a>Metodo consigliato: eseguire l'overload delle classi `PhoneApplicationPage`
Report hello tooactivate order di tutti i log di hello richiesto da Engagement toocompute utenti, sessioni, attività, arresti anomali del sistema e le statistiche tecniche, puoi semplicemente far tutti i `PhoneApplicationPage` sottoclassi ereditano hello `EngagementPage` classi.

Di seguito è riportato un esempio di come toodo per una pagina dell'applicazione. È possibile eseguire hello stessa operazione per tutte le pagine dell'applicazione.

#### <a name="c-source-file"></a>File di origine C#
Modificare il file `.xaml.cs` della pagina:

* Aggiungere tooyour `using` istruzioni:
  
      using Microsoft.Azure.Engagement;
* Sostituire `PhoneApplicationPage` con `EngagementPage`:

**Senza Engagement:**

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

**Con Engagement:**

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> Se la pagina eredita da hello `OnNavigatedTo` (metodo), essere hello toolet attenzione `base.OnNavigatedTo(e)` chiamare. In caso contrario, non verranno segnalati attività hello. In effetti, hello `EngagementPage` chiama `StartActivity` all'interno di hello `OnNavigatedTo` metodo.
> 
> 

#### <a name="xaml-file"></a>File XAML
Modificare il file `.xaml` della pagina:

* Aggiungere le dichiarazioni di spazi dei nomi tooyour:
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* Sostituire `phone:PhoneApplicationPage` con `engagement:EngagementPage`:

**Senza Engagement:**

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

**Con Engagement:**

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-hello-default-behavior"></a>Ignorare il comportamento predefinito di hello
Per impostazione predefinita, il nome di classe hello della pagina hello viene segnalato come nome dell'attività hello con senza aggiuntivi. Se la classe hello utilizza il suffisso "Pagina" hello, Engagement verrà inoltre rimosso.

Se si desidera il comportamento predefinito di hello toooverride per nome hello, è sufficiente aggiungere questo codice tooyour:

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

Se si desiderano tooreport alcune informazioni aggiuntive con l'attività, è possibile aggiungere questo codice tooyour:

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

Questi metodi vengono chiamati all'interno di hello `OnNavigatedTo` metodo della pagina.

### <a name="alternate-method-call-startactivity-manually"></a>Metodo alternativo: chiamare `StartActivity()` manualmente
Se non è possibile o non si desidera toooverload il `PhoneApplicationPage` classi, invece, è possibile avviare le attività chiamando `EngagementAgent` diretta dei metodi.

È consigliabile chiamare `StartActivity` all'interno del metodo `OnNavigatedTo` di PhoneApplicationPage.

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> Assicurarsi che la sessione venga terminata correttamente.
> 
> Hello SDK chiama automaticamente hello `EndActivity` metodo quando un'applicazione hello viene chiuso. È pertanto **elevata** consigliato hello toocall `StartActivity` metodo ogni volta che cambia attività hello dell'utente di hello e troppo**mai** chiamata hello `EndActivity` metodo. Questo metodo invia un server di Engagement toohello di messaggio che l'utente corrente hello ha lasciato l'applicazione hello e ciò influisce su tutti i log applicazioni.
> 
> 

## <a name="advanced-reporting"></a>Segnalazione avanzata
Facoltativamente, è opportuno tooreport eventi specifici di applicazione, gli errori e processi e toodo, pertanto, utilizzare hello altri metodi, vedere hello `EngagementAgent` classe. Hello Engagement API consente toouse tutte le funzionalità avanzate di Engagement.

Per ulteriori informazioni, vedere [come toouse hello avanzate Mobile Engagement tag API nelle applicazioni Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md).

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

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a>Modalità burst
Per impostazione predefinita, i report del servizio di Engagement hello registra in tempo reale. Se l'applicazione segnala molto spesso i registri, è preferibile toobuffer hello registri e tooreport usarle in una sola volta in volta regolare base (è chiamata hello "modalità burst").

toodo in tal caso, chiamare il metodo hello:

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

argomento Hello è un valore in **millisecondi**. In qualsiasi momento, se si desidera registrare in tempo reale di tooreactivate hello, chiamare solo metodo hello senza alcun parametro, o con valore 0 hello.

Hello modalità burst leggermente aumentare batteria hello vita ma ha un impatto sulle hello Engagement Monitor: durata di tutte le sessioni e i processi sarà arrotondato toohello burst soglia (in questo modo, le sessioni e i processi è inferiore a soglia burst hello potrebbe non essere visibile). È consigliabile toouse una soglia di potenziamento non più di 30000 (30 s). È necessario tenere presente che registri salvati sono elementi too300 limitato toobe. Se l'invio richiede troppo tempo, è possibile che alcuni log vadano persi.

> [!WARNING]
> Hello soglia burst non può essere configurata tooa periodo inferiore rispetto a un secondo. Se si tenta pertanto toodo, hello SDK sarà visualizzare una traccia con l'errore hello e verrà automaticamente reimpostato toohello valore predefinito, ovvero zero secondi. In questo modo verrà attivata hello SDK tooreport hello log in tempo reale.
> 
> 

