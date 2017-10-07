---
title: aaaWindows universale avanzate Reporting con MobileApps Engagement
description: Come tooIntegrate Azure Mobile Engagement con App universali di Windows
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ea5030bf-73ac-49b7-bc3e-c25fc10e945a
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 20968f238ef7ae9dc0b8bb6dac3fb8bdb9bc3a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-hello-windows-universal-apps-engagement-sdk"></a>Creazione di report avanzate con hello Windows Universal App Engagement SDK
> [!div class="op_single_selector"]
> * [Windows universale](mobile-engagement-windows-store-advanced-reporting.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-reporting.md)
> 
> 

Questo argomento descrive scenari di segnalazione aggiuntivi nell'applicazione di Windows universale. Questi scenari includono opzioni che è possibile selezionare app toohello tooapply creato in hello [Introduzione](mobile-engagement-windows-store-dotnet-get-started.md) esercitazione.

## <a name="prerequisites"></a>Prerequisiti
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

Prima di iniziare questa esercitazione, è necessario prima completare hello [Introduzione](mobile-engagement-windows-store-dotnet-get-started.md) esercitazione, è intenzionalmente semplice e diretto. Questa esercitazione illustra le opzioni aggiuntive disponibili.

## <a name="specifying-engagement-configuration-at-runtime"></a>Specifica della configurazione di Engagement in fase di esecuzione
configurazione di Engagement Hello è centralizzata in hello `Resources\EngagementConfiguration.xml` file del progetto, in cui è stato specificato in hello [Introduzione](mobile-engagement-windows-store-dotnet-get-started.md) argomento.

Ma è possibile inoltre specificare in fase di esecuzione: è possibile chiamare hello al metodo prima dell'inizializzazione dell'agente di Engagement hello:

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a>Metodo consigliato: eseguire l'overload delle classi `Page`
tooactivate hello reporting di tutti i log di hello richiesti da Engagement toocompute utenti, sessioni, attività, arresti anomali del sistema e le statistiche tecniche, apportare tutte le `Page` sottoclassi ereditano hello `EngagementPage` classi.

Di seguito è riportato un esempio per una pagina dell'applicazione. È possibile eseguire hello stessa operazione per tutte le pagine dell'applicazione.

### <a name="c-source-file"></a>File di origine C#
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
> Se la pagina esegue l'override di hello `OnNavigatedTo` metodo toocall assicurarsi di essere `base.OnNavigatedTo(e)`. In caso contrario, attività hello non venga segnalato (hello `EngagementPage` chiamate `StartActivity` all'interno di relativo `OnNavigatedTo` (metodo)).
> 
> 

### <a name="xaml-file"></a>File XAML
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

### <a name="override-hello-default-behaviour"></a>Eseguire l'override di comportamento predefinito di hello
Per impostazione predefinita, il nome di classe hello della pagina hello viene segnalato come nome dell'attività hello con senza aggiuntivi. Se la classe hello utilizza il suffisso "Pagina" hello, Engagement lo rimuove.

comportamento predefinito di hello toooverride per nome hello, aggiungere questo codice:

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

tooreport informazioni aggiuntive con l'attività, aggiungere il seguente codice:

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

Questi metodi vengono chiamati all'interno di hello `OnNavigatedTo` metodo della pagina.

### <a name="alternate-method-call-startactivity-manually"></a>Metodo alternativo: chiamare `StartActivity()` manualmente
Se non è possibile o non si desidera toooverload il `Page` classi, invece, è possibile avviare le attività chiamando `EngagementAgent` diretta dei metodi.

È consigliabile chiamare `StartActivity` all'interno del metodo `OnNavigatedTo` della pagina.

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> Assicurarsi che la sessione venga terminata correttamente.
> 
> SDK di Windows universale Hello chiama automaticamente hello `EndActivity` metodo quando un'applicazione hello viene chiuso. È pertanto **elevata** consigliato hello toocall `StartActivity` metodo ogni volta che cambia attività hello dell'utente di hello e troppo**mai** chiamata hello `EndActivity` metodo. Questo metodo notifica server Engagement hello che l'utente corrente hello ha lasciato l'applicazione hello, che avrà un impatto tutti i log dell'applicazione.
> 
> 

## <a name="advanced-reporting"></a>Segnalazione avanzata
Facoltativamente, è opportuno eventi specifici dell'applicazione tooreport, errori e processi e toodo, pertanto, utilizzare hello altri metodi, vedere hello `EngagementAgent` classe. Hello Engagement API consente l'utilizzo delle funzionalità avanzate di Engagement tutti.

Per ulteriori informazioni, vedere [come toouse hello avanzate tag API in app universali di Windows di Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md).

