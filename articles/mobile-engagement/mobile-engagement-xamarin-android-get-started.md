---
title: aaaGet avviato con Azure Mobile Engagement per xamarin
description: Informazioni su come toouse Azure Mobile Engagement con Analitica e le notifiche Push per le app xamarin.
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: fb68cf98-08a2-41b5-8e59-757469de3fe7
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/16/2016
ms.author: piyushjo
ms.openlocfilehash: 9d584fea8e8153d511258cf9b6f87f31dac6aeca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a>Introduzione ad Azure Mobile Engagement per app Xamarin.Android
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

In questo argomento illustra come toouse Azure Mobile Engagement toounderstand sull'utilizzo delle app e come toosend push agli utenti di toosegmented notifiche di un'applicazione di xamarin.
Questa esercitazione illustra hello broadcast uno scenario semplice utilizzando Mobile Engagement. Verrà creata un'app Xamarin.Android vuota che raccoglie dati di base e riceve notifiche push tramite il servizio Google Cloud Messaging (GCM).

> [!NOTE]
> servizio di Azure Mobile Engagement di Hello verrà ritirata 2018 marzo ed è attualmente tooexisting disponibili solo i clienti. Per altre informazioni, vedere [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Questa esercitazione richiede il seguente hello:

* [Xamarin Studio](http://xamarin.com/studio). È anche possibile usare Visual Studio con Xamarin ma questa esercitazione usa Xamarin Studio. Per istruzioni di installazione, vedere [Configurazione e installazione per Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).
* [Mobile Engagement Xamarin SDK](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).
> 
> 

## <a id="setup-azme"></a>Configurare Mobile Engagement per l'app Android
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>La connessione back-end Mobile Engagement toohello app
Questa esercitazione viene illustrato una "integrazione di base", che viene hello minima set di dati obbligatorio toocollect e invia una notifica push. 

Verrà creata un'applicazione di base con l'integrazione di hello toodemonstrate Xamarin Studio.

### <a name="create-a-new-xamarinandroid-project"></a>Creare un nuovo progetto Xamarin.Android
1. Avviare **Xamarin Studio** andare troppo**File** -> **New** -> **soluzione** 
   
    ![][1]
2. Selezionare **App Android** assicurarsi lingua hello selezionata è **c#** e fare clic su **Avanti**.
   
    ![][2]
3. Compilare hello **nome App** hello e **identificatore organizzazione**. Verificare che toocheckmark **Google Play Services** e quindi fare clic su **Avanti**. 
   
    ![][3]
4. Hello aggiornamento **nome progetto**, **Nome soluzione** e **percorso** se necessario, fare clic su **crea**.
   
    ![][4]

Xamarin Studio consente di creare app di hello in cui integrare Mobile Engagement. 

### <a name="connect-your-app-toomobile-engagement-backend"></a>La connessione back-end Engagement tooMobile app
1. Fare clic con il pulsante destro hello **pacchetti** cartella windows soluzione hello e selezionare **Aggiungi pacchetti...**
   
    ![][5]
2. Ricerca di hello **Xamarin SDK di Microsoft Azure Mobile Engagement** e aggiungerlo tooyour soluzione.  
   
    ![][6]
3. Aprire **Mainactivity** e aggiungere hello seguenti istruzioni using:
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. In hello `OnCreate` metodo, aggiungere hello seguente connessione di hello tooinitialize con back-end Mobile Engagement. Verificare che tooadd il **ConnectionString**. 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a>Aggiungere le autorizzazioni e una dichiarazione del servizio
1. Aprire la console di hello **Manifest.xml** file nella cartella proprietà hello. Selezionare la scheda origine in modo da aggiornare direttamente l'origine XML hello.
2. Aggiungere questi toohello autorizzazioni manifest (che è possibile trovare in hello **proprietà** cartella) del progetto, immediatamente prima o dopo hello `<application>` tag:
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. Aggiungere il seguente hello tra hello `<application>` e `</application>` tag servizio agente di hello toodeclare:
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. Nel codice hello appena incollati, sostituire `"<Your application name>"` nell'etichetta hello. Viene visualizzato in hello **impostazioni** menu in cui gli utenti possono visualizzare i servizi in esecuzione sul dispositivo hello. È possibile aggiungere, ad esempio la parola hello "Servizio" in tale etichetta.

### <a name="send-a-screen-toomobile-engagement"></a>Inviare un tooMobile schermata Engagement
In ordine toostart l'invio dei dati e garantire agli utenti di hello sono attivi, è necessario inviare almeno un back-end Mobile Engagement delle toohello dello schermo. Per eseguire questa operazione-verificare che hello `MainActivity` eredita da `EngagementActivity` anziché `Activity`.

    public class MainActivity : EngagementActivity

In alternativa, se non è possibile ereditare da `EngagementActivity` è necessario aggiungere i metodi `.StartActivity` e `.EndActivity` rispettivamente in `OnResume` e `OnPause`.  

        protected override void OnResume()
            {
                EngagementAgent.StartActivity(EngagementAgentUtils.BuildEngagementActivityName(Java.Lang.Class.FromType(this.GetType())), null);
                base.OnResume();             
            }

            protected override void OnPause()
            {
                EngagementAgent.EndActivity();
                base.OnPause();            
            }

## <a id="monitor"></a>Connettere l'app con monitoraggio in tempo reale
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Abilitare le notifiche push e la messaggistica in-app
Engagement mobile permette toointeract con e raggiungere gli utenti con le notifiche push e nel contesto di hello delle campagne di messaggistica in-app. Questo modulo viene chiamato REACH nel portale Mobile Engagement hello.
Hello le sezioni seguenti viene impostato il tooreceive app li.

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[1]: ./media/mobile-engagement-xamarin-android-get-started/1.png
[2]: ./media/mobile-engagement-xamarin-android-get-started/2.png
[3]: ./media/mobile-engagement-xamarin-android-get-started/3.png
[4]: ./media/mobile-engagement-xamarin-android-get-started/4.png
[5]: ./media/mobile-engagement-xamarin-android-get-started/5.png
[6]: ./media/mobile-engagement-xamarin-android-get-started/6.png
