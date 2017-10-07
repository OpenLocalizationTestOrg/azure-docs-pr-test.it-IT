---
title: iniziare con le app di Azure Mobile Engagement per Windows Phone Silverlight aaaGet
description: Informazioni su come toouse Azure Mobile Engagement con analitica e notifiche push per le app di Windows Phone Silverlight.
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: aa34692f-87f7-47c6-a20c-a1972750bc25
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b39a838ab03217b2dc845cbf59d7bf8b094dac1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a>Introduzione ad Azure Mobile Engagement per app per Windows Phone Silverlight
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

In questo argomento illustra come toouse Azure Mobile Engagement toounderstand l'utilizzo delle app e trasmissione push agli utenti di toosegmented notifiche di un'applicazione Windows Phone Silverlight.
Questa esercitazione illustra hello broadcast uno scenario semplice utilizzando Mobile Engagement. Si creerà un'app per Windows Phone Silverlight vuota che raccoglie dati di base e riceve notifiche push tramite il Servizio notifica push Microsoft (MPNS).

> [!NOTE]
> servizio di Azure Mobile Engagement di Hello verrà ritirata 2018 marzo ed è attualmente tooexisting disponibili solo i clienti. Per altre informazioni, vedere [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

> [!NOTE]
> I progetti Windows Phone 8.1 e versioni precedenti non sono supportati in Visual Studio 2017.  Per altre informazioni, vedere [Selezione della piattaforma e compatibilità di Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

> [!NOTE]
> Se la destinazione è Windows Phone 8.1 (non Silverlight), fare riferimento toohello [esercitazione universali di Windows](mobile-engagement-windows-store-dotnet-get-started.md).
> 
> 

Questa esercitazione richiede il seguente hello:

* Visual Studio 2013
* [MicrosoftAzure.MobileEngagement]

> [!NOTE]
> toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).
> 
> 

## <a id="setup-azme"></a>Configurare Mobile Engagement per l'app per Windows Phone
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>La connessione back-end Mobile Engagement toohello app
Questa esercitazione viene illustrato una "integrazione di base", che viene hello minima set di dati obbligatorio toocollect e invia una notifica push. la documentazione completa integrazione Hello è reperibile in hello [integrazione Mobile Engagement SDK di Windows Phone](mobile-engagement-windows-phone-sdk-overview.md)

Verrà creata un'applicazione di base con l'integrazione di Visual Studio toodemonstrate hello.

### <a name="create-a-new-windows-phone-silverlight-project"></a>Creare un nuovo progetto Windows Phone Silverlight
Hello passaggi seguenti si presuppongono hello utilizzo di Visual Studio 2015 se hello passaggi sono simili nelle versioni precedenti di Visual Studio. 

1. Avviare Visual Studio e in hello **Home** selezionare **nuovo progetto**.
2. Nel menu a comparsa hello, selezionare **Windows 8** -> **Windows Phone** -> **applicazione vuota (Windows Phone Silverlight)**. Compilare app hello **nome** e **Nome soluzione**, quindi fare clic su **OK**.
   
    ![][1]
3. È possibile scegliere di tootarget **Windows Phone 8.0** o **Windows Phone 8.1**.

Ora è stata creata una nuova app di Windows Phone Silverlight in cui integrare hello Azure Mobile Engagement SDK.

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a>La connessione back-end Mobile Engagement toohello app
1. Installare hello [MicrosoftAzure.MobileEngagement] pacchetto nuget nel progetto.
2. Aprire `WMAppManifest.xml` , nella cartella proprietà di hello e accertarsi che siano dichiarate seguente hello (aggiungerli se non sono) in hello `<Capabilities />` tag:
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. Incollare una stringa di connessione hello copiato in precedenza per l'applicazione di Mobile Engagement ora e incollarlo in hello `Resources\EngagementConfiguration.xml` file tra hello `<connectionString>` e `</connectionString>` tag:
   
    ![][3]
4. In hello `App.xaml.cs` file:
   
    a. Aggiungere hello `using` istruzione:
   
            using Microsoft.Azure.Engagement;
   
    b. Inizializzare Ciao SDK hello `Application_Launching` metodo:
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    c. Inserire il seguente hello in hello `Application_Activated`:
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <a id="monitor"></a>Abilitare il monitoraggio in tempo reale
In ordine toostart l'invio dei dati e garantire che gli utenti di hello sono attivi, è necessario inviare almeno un back-end Mobile Engagement delle toohello schermata (attività).

1. In hello MainPage.xaml.cs, aggiungere hello `using` istruzione:
   
        using Microsoft.Azure.Engagement;
2. Sostituire la classe base hello di **MainPage**, che si trova prima **PhoneApplicationPage**, con **EngagementPage**.
   
        class MainPage : EngagementPage 
3. Nel file `MainPage.xml`:
   
    a. Aggiungere le dichiarazioni di spazi dei nomi tooyour:
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    b. Sostituire `phone:PhoneApplicationPage` nei nomi di tag XML hello con `engagement:EngagementPage`.

## <a id="monitor"></a>Connettere l'app con monitoraggio in tempo reale
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Abilitare le notifiche push e la messaggistica in-app
Engagement mobile permette toointeract e raggiungere gli utenti con le notifiche Push e la messaggistica in-app nel contesto di hello delle campagne. Questo modulo viene chiamato REACH nel portale Mobile Engagement hello.
Hello nelle sezioni seguenti impostarle backup tooreceive l'app.

### <a name="enable-your-app-tooreceive-mpns-push-notifications"></a>Abilitare il tooreceive app le notifiche Push MPNS
Aggiungere nuove funzionalità tooyour `WMAppManifest.xml` file:

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-hello-reach-sdk"></a>Inizializzare hello REACH SDK
1. In `App.xaml.cs`, chiamare `EngagementReach.Instance.Init();` in hello **Application_Launching** funzione, subito dopo l'inizializzazione dell'agente di hello:
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. In `App.xaml.cs`, chiamare `EngagementReach.Instance.OnActivated(e);` in hello **Application_Activated** funzione, subito dopo l'inizializzazione dell'agente di hello:
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

Le impostazioni sono state completate. Ora è necessario verificare di avere eseguito correttamente l'integrazione di base.

## <a id="send"></a>Invia un'app tooyour notifica
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

Dovrebbe essere una notifica sul dispositivo che verrà visualizzati come una notifica in-app se app hello è aperto in caso contrario come notifica di tipo avviso popup hello seguente: 

![][6]

<!-- URLs. -->
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: ./media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: ./media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: ./media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: ./media/mobile-engagement-windows-phone-get-started/push-screenshot.png
