---
title: aaaGet avviato con Azure Mobile Engagement per la distribuzione di Unity Android
description: Informazioni su come toouse Azure Mobile Engagement con Analitica e le notifiche Push per App Unity distribuzione tooiOS dispositivi.
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: d5f0ef79-be00-4cec-97a5-a0b2fdaa380e
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c4d34691daeb7544b11c2d6895b2474af0f902b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a>Introduzione ad Azure Mobile Engagement per la distribuzione di Unity in Android
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

In questo argomento illustra come toouse Azure Mobile Engagement toounderstand sull'utilizzo delle app e toosend push agli utenti di toosegmented notifiche di un'applicazione di Unity durante la distribuzione di dispositivo Android tooan.
Questa esercitazione viene utilizzato hello classico Unity rollback un'esercitazione palla come punto di partenza hello. È opportuno seguire passaggi hello in questo [esercitazione](mobile-engagement-unity-roll-a-ball.md) prima di procedere con l'integrazione di Mobile Engagement è illustrare nell'esercitazione hello seguente hello. 

Questa esercitazione richiede il seguente hello:

* [Editor di Unity](http://unity3d.com/get-unity)
* [Mobile Engagement Unity SDK](https://aka.ms/azmeunitysdk)
* Google Android SDK

> [!NOTE]
> toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).
> 
> 

## <a id="setup-azme"></a>Configurare Mobile Engagement per l'app Android
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>La connessione back-end Mobile Engagement toohello app
### <a name="import-hello-unity-package"></a>Importa pacchetto di Unity hello
1. Scaricare hello [pacchetto Unity Engagement Mobile](https://aka.ms/azmeunitysdk) e salvarlo tooyour di computer locale. 
2. Andare troppo**risorse -> Importa pacchetto -> pacchetto personalizzato** e selezionare hello pacchetto scaricato in hello prima passo. 
   
    ![][70] 
3. Assicurarsi che tutti i file siano selezionati e fare clic sul pulsante **Import** . 
   
    ![][71] 
4. Dopo l'importazione ha esito positivo, verranno visualizzati i file SDK hello importato nel progetto.  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a>Aggiornare hello EngagementConfiguration
1. Aprire la console di hello **EngagementConfiguration** file script da hello cartella e aggiornamento SDK hello **ANDROID\_connessione\_stringa** con stringa di connessione hello ottenuto in precedenza da hello portale di Azure.  
   
    ![][73]
2. Salvare il file hello 
3. Eseguire **File -> Engagement -> Generate Android Manifest** (File -> Engagement -> Genera manifesto di Android). Si tratta di plug-in hello aggiunto da Mobile Engagement SDK hello e facendo clic su di essa verrà aggiornata automaticamente le impostazioni del progetto. 
   
    ![][74]

> [!IMPORTANT]
> Imposta come tooexecute che ogni volta che si aggiorna hello **EngagementConfiguration** file in caso contrario non rifletteranno le modifiche nell'app hello. 
> 
> 

### <a name="configure-hello-app-for-basic-tracking"></a>Configurare app hello per il rilevamento di base
1. Aprire la console di hello **PlayerController** script associato l'oggetto lettore toohello per la modifica. 
2. Aggiungere hello seguente istruzione using:
   
        using Microsoft.Azure.Engagement.Unity;
3. Aggiungere hello seguente toohello `Start()` (metodo)
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a>Distribuire ed eseguire l'applicazione hello
Assicurarsi di disporre di Android SDK installati nel computer prima di tentare di toodeploy tooyour dispositivo app Unity. 

1. Connettere una macchina tooyour dispositivo Android. 
2. Aprire **File -> Build Settings** (File -> Impostazioni compilazione) 
   
    ![][40]
3. Selezionare **Android** e quindi fare clic su **Switch Platform** (Cambia piattaforma)
   
    ![][51]
   
    ![][52]
4. Fare clic su **Player Settings** e fornire un identificatore del bundle valido. 
   
    ![][53]
5. Infine, fare clic su **Build And Run**
   
    ![][54]
6. Potrebbe essere richiesto di un pacchetto Android cartella nome toostore hello tooprovide. 
7. Se tutto va bene, pacchetto hello verrà distribuito tooyour connesso dispositivo e si dovrebbe essere visualizzato il gioco Unity sul telefono. 

## <a id="monitor"></a>Connettere l'app con monitoraggio in tempo reale
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Abilitare le notifiche push e la messaggistica in-app
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-hello-engagementconfiguration"></a>Aggiornare hello EngagementConfiguration
1. Aprire la console di hello **EngagementConfiguration** file script da hello cartella e aggiornamento SDK hello **ANDROID\_GOOGLE\_numero** con hello **progetto Google Numero** è ottenuto in precedenza dal portale per sviluppatori di Google Cloud hello. Si tratta di una stringa di valore per rendere tooenclose che è racchiuso tra virgolette doppie. 
   
    ![][75]
2. Salvare il file hello. 
3. Eseguire **File -> Engagement -> Generate Android Manifest** (File -> Engagement -> Genera manifesto di Android). Si tratta di plug-in hello aggiunto da Mobile Engagement SDK hello e facendo clic su di essa verrà aggiornata automaticamente le impostazioni del progetto. 
   
    ![][74]

### <a name="configure-hello-app-tooreceive-notifications"></a>Configurare le notifiche di hello app tooreceive
1. Aprire la console di hello **PlayerController** script associato l'oggetto lettore toohello per la modifica. 
2. Aggiungere hello seguente toohello `Start()` (metodo)
   
        EngagementReachAgent.Initialize();
3. Ora che hello app viene aggiornata, distribuire ed eseguire l'applicazione hello in un dispositivo per istruzioni hello riportate di seguito. 

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[40]: ./media/mobile-engagement-unity-android-get-started/40.png
[70]: ./media/mobile-engagement-unity-android-get-started/70.png
[71]: ./media/mobile-engagement-unity-android-get-started/71.png
[72]: ./media/mobile-engagement-unity-android-get-started/72.png
[73]: ./media/mobile-engagement-unity-android-get-started/73.png
[74]: ./media/mobile-engagement-unity-android-get-started/74.png
[75]: ./media/mobile-engagement-unity-android-get-started/75.png
[51]: ./media/mobile-engagement-unity-android-get-started/51.png
[52]: ./media/mobile-engagement-unity-android-get-started/52.png
[53]: ./media/mobile-engagement-unity-android-get-started/53.png
[54]: ./media/mobile-engagement-unity-android-get-started/54.png
