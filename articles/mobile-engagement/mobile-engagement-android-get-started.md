---
title: aaaGet avviato con Android le app di Azure Mobile Engagement
description: Informazioni su come toouse Azure Mobile Engagement con analitica e notifiche push per le app Android.
services: mobile-engagement
documentationcenter: android
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3c286c6d-cfef-4e3e-9b2c-715429fe82db
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e8c92607691104750cdf1c4f7639a041d8a7bcd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a>Introduzione a Azure Mobile Engagement per app Android
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

In questo argomento illustra come toouse Azure Mobile Engagement toounderstand sull'utilizzo delle app e come toosend push agli utenti di toosegmented notifiche di un'applicazione Android.
Questa esercitazione illustra hello broadcast uno scenario semplice utilizzando Mobile Engagement. Si creerà un'app per Android vuota che raccoglie dati di base e riceve notifiche push tramite il servizio Google Cloud Messaging (GCM).

## <a name="prerequisites"></a>Prerequisiti
Completato questa esercitazione richiede hello [Android Developer Tools](https://developer.android.com/sdk/index.html), che include l'ambiente di sviluppo integrato di Android Studio hello e la piattaforma Android più recente di hello.

È inoltre necessario hello [Mobile Engagement SDK Android](https://aka.ms/vq9mfn).

> [!IMPORTANT]
> toocomplete questa esercitazione, è necessario un account di Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a>Configurare Mobile Engagement per l'app Android
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-toohello-mobile-engagement-backend"></a>La connessione back-end Mobile Engagement toohello app
Questa esercitazione viene illustrato una "integrazione di base", che viene hello minima set di dati obbligatorio toocollect e invia una notifica push. Creare un'app di base con l'integrazione di Android Studio toodemonstrate hello.

la documentazione completa integrazione Hello è reperibile in hello [integrazione Mobile Engagement SDK Android](mobile-engagement-android-sdk-overview.md).

### <a name="create-an-android-project"></a>Creare un progetto Android
1. Avviare **Android Studio**e nel menu a comparsa hello, selezionare **avviare un nuovo progetto Android Studio**.

    ![][1]
2. Specificare il nome dell'app e il dominio aziendale. Prendere nota delle informazioni specificate perché saranno necessarie successivamente. Fare clic su **Avanti**.

    ![][2]
3. Selezione del livello di API e del fattore di forma hello destinazione e fare clic su **Avanti**.

   > [!NOTE]
   > Mobile Engagement richiede almeno un livello API 10 (Android 2.3.3).
   >
   >

    ![][3]
4. Selezionare **attività vuota** qui, viene visualizzata la schermata solo hello per questa app e fare clic su **Avanti**.

    ![][4]
5. Infine, lasciare le impostazioni predefinite hello e fare clic su **fine**.

    ![][5]

Android Studio verranno create app demo hello in cui integrare Mobile Engagement.

### <a name="include-hello-sdk-library-in-your-project"></a>Includere la libreria di SDK hello nel progetto
1. Scaricare hello [Mobile Engagement SDK Android](https://aka.ms/vq9mfn).
2. Estrarre la cartella di tooa hello archivio file nel computer.
3. Identificare libreria JAR hello per la versione corrente di questo SDK hello e copiarlo negli Appunti toohello.

      ![][6]
4. Passare toohello **progetto** sezione (1) e incollare JAR hello nella cartella di librerie hello (2).

      ![][7]
5. libreria di hello tooload, progetto hello di sincronizzazione.

      ![][8]

### <a name="connect-your-app-toomobile-engagement-backend-with-hello-connection-string"></a>La connessione back-end Engagement tooMobile app con hello stringa di connessione
1. Copiare hello seguenti righe di codice nella creazione di attività hello (deve essere eseguita solo in un'unica posizione dell'applicazione, in genere attività principale di hello). Per questa app di esempio, aprire hello MainActivity in src -> main -> cartella java e aggiungere hello seguenti:

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. Risolvere i riferimenti di hello premendo Alt + Invio oppure aggiunta hello seguendo le istruzioni di importazione:

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. Tornare indietro toohello portale classico di Azure dell'app **le informazioni di connessione** hello pagina e copia **stringa di connessione**.

      ![][9]
4. Incollarlo hello `setConnectionString` parametro, sostituendo l'intera stringa hello mostrato nel seguente codice hello:

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a>Aggiungere le autorizzazioni e una dichiarazione del servizio
1. Aggiungere questi toohello autorizzazioni manifest del progetto, immediatamente prima o dopo hello `<application>` tag:

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. toodeclare hello servizio agente, aggiungere il codice tra hello `<application>` e `</application>` tag:

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. Nel codice hello incollata, sostituire `"<Your application name>"` etichetta hello, che viene visualizzato nella hello **impostazioni** menu in cui è possibile visualizzare i servizi in esecuzione sul dispositivo hello. È possibile aggiungere, ad esempio la parola hello "Servizio" in tale etichetta.

### <a name="send-a-screen-toomobile-engagement"></a>Inviare un tooMobile schermata Engagement
toostart l'invio dei dati e assicurarsi che gli utenti di hello sono attivi, è necessario inviare almeno un back-end Mobile Engagement delle toohello schermata (attività).

Andare troppo**Mainactivity** e aggiungere hello seguente classe di base hello tooreplace di **MainActivity** troppo**EngagementActivity**:

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> Se non è la classe base *attività*, consultare [avanzate Reporting Android](mobile-engagement-android-advanced-reporting.md) come tooinherit da classi diverse.
>
>

Commento hello linea per questo scenario di esempio semplice di seguito:

    // setSupportActionBar(toolbar);

Se si desidera hello tookeep `ActionBar` nell'app, vedere [avanzate Reporting Android](mobile-engagement-android-advanced-reporting.md).

## <a name="connect-app-with-real-time-monitoring"></a>Connettere l'app con monitoraggio in tempo reale
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a>Abilitare le notifiche push e la messaggistica in-app
Durante una campagna, Mobile Engagement consente di interagire con gli utenti e coinvolgerli tramite notifiche push e messaggistica in-app. Questo modulo viene chiamato REACH nel portale Mobile Engagement hello.
Hello successiva sezione Imposta backup tooreceive l'app.

### <a name="copy-sdk-resources-in-your-project"></a>Copiare le risorse dell'SDK nel progetto
1. Spostarsi indietro tooyour SDK download del contenuto e copiare hello **res** cartella.

    ![][10]
2. Tornare indietro tooAndroid Studio, seleziona hello **principale** directory dei file del progetto, quindi incollarlo tooadd hello di risorse tooyour project.

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a>Passaggi successivi
Andare troppo[Android SDK](mobile-engagement-android-sdk-overview.md) tooget dettagliate conoscenza hello integrazione SDK.

<!-- Images. -->
[1]: ./media/mobile-engagement-android-get-started/android-studio-new-project.png
[2]: ./media/mobile-engagement-android-get-started/android-studio-project-props.png
[3]: ./media/mobile-engagement-android-get-started/android-studio-project-props2.png
[4]: ./media/mobile-engagement-android-get-started/android-studio-add-activity.png
[5]: ./media/mobile-engagement-android-get-started/android-studio-activity-name.png
[6]: ./media/mobile-engagement-android-get-started/sdk-content.png
[7]: ./media/mobile-engagement-android-get-started/paste-jar.png
[8]: ./media/mobile-engagement-android-get-started/sync-project.png
[9]: ./media/mobile-engagement-android-get-started/app-connection-info-page.png
[10]: ./media/mobile-engagement-android-get-started/copy-resources.png
[11]: ./media/mobile-engagement-android-get-started/paste-resources.png
