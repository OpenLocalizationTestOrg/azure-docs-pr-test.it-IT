---
title: aaaGet avviato con Azure Mobile Engagement per la distribuzione di Unity iOS
description: Informazioni su come toouse Azure Mobile Engagement con Analitica e le notifiche Push per App Unity distribuzione tooiOS dispositivi.
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7ddfbac3-8d13-4ebe-b061-c865f357297f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f4247b0a9240cbe2bf1a6618388919d3554c07fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a>Introduzione ad Azure Mobile Engagement per la distribuzione di Unity in iOS
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

In questo argomento illustra come toouse Azure Mobile Engagement toounderstand sull'utilizzo delle app e toosend push agli utenti di toosegmented notifiche di un'applicazione di Unity quando si distribuisce il dispositivo iOS tooan.
Questa esercitazione viene utilizzato hello classico Unity rollback un'esercitazione palla come punto di partenza hello. È opportuno seguire passaggi hello in questo [esercitazione](mobile-engagement-unity-roll-a-ball.md) prima di procedere con l'integrazione di Mobile Engagement è illustrare nell'esercitazione hello seguente hello. 

Questa esercitazione richiede il seguente hello:

* [Editor di Unity](http://unity3d.com/get-unity)
* [Mobile Engagement Unity SDK](https://aka.ms/azmeunitysdk)
* Editor di Xcode

> [!NOTE]
> toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).
> 
> 

## <a id="setup-azme"></a>Configurare Mobile Engagement per l'app iOS
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
1. Aprire la console di hello **EngagementConfiguration** file script da hello cartella e aggiornamento SDK hello **IOS\_connessione\_stringa** con stringa di connessione hello ottenuti in precedenza dal portale di Azure hello.  
   
    ![][73]
2. Salvare il file hello. 

### <a name="configure-hello-app-for-basic-tracking"></a>Configurare app hello per il rilevamento di base
1. Aprire la console di hello **PlayerController** script associato l'oggetto lettore toohello per la modifica. 
2. Aggiungere hello seguente istruzione using:
   
        using Microsoft.Azure.Engagement.Unity;
3. Aggiungere hello seguente toohello `Start()` (metodo)
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a>Distribuire ed eseguire l'applicazione hello
1. Connettere una macchina di tooyour dispositivo iOS. 
2. Aprire **File -> Build Settings** (File -> Impostazioni compilazione) 
   
    ![][40]
3. Selezionare **iOS** e quindi fare clic su **Switch Platform** (Cambia piattaforma)
   
    ![][41]
   
    ![][42]
4. Fare clic su **Player Settings** e fornire un identificatore del bundle valido. 
   
    ![][53]
5. Infine, fare clic su **Build And Run**
   
    ![][54]
6. Potrebbe essere richiesto tooprovide un pacchetto di cartella nome toostore hello iOS. 
   
    ![][43]
7. Se tutto va correttamente, verrà compilato il progetto hello e deve aprire sull'applicazione di XCode. 
8. Verificare che tale hello **identificatore Bundle** sia corretto nel progetto hello.  
   
    ![][75]
9. Eseguire app hello in XCode in modo tale che il pacchetto di hello dispositivo connesso tooyour distribuito nel telefono, si dovrebbe vedere del gioco Unity! 

## <a id="monitor"></a>Connettere l'app con monitoraggio in tempo reale
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Abilitare le notifiche push e la messaggistica in-app
Engagement mobile permette di REACH e toointeract con gli utenti con le notifiche push e nel contesto di hello delle campagne di messaggistica in-app. Questo modulo viene chiamato REACH nel portale Mobile Engagement hello.
Non si dispone toodo ulteriori attività di configurazione nelle notifiche di tooreceive app ed è già il programma di installazione per tale.

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[40]: ./media/mobile-engagement-unity-ios-get-started/40.png
[41]: ./media/mobile-engagement-unity-ios-get-started/41.png
[42]: ./media/mobile-engagement-unity-ios-get-started/42.png
[43]: ./media/mobile-engagement-unity-ios-get-started/43.png
[53]: ./media/mobile-engagement-unity-ios-get-started/53.png
[54]: ./media/mobile-engagement-unity-ios-get-started/54.png
[70]: ./media/mobile-engagement-unity-ios-get-started/70.png
[71]: ./media/mobile-engagement-unity-ios-get-started/71.png
[72]: ./media/mobile-engagement-unity-ios-get-started/72.png
[73]: ./media/mobile-engagement-unity-ios-get-started/73.png
[74]: ./media/mobile-engagement-unity-ios-get-started/74.png
[75]: ./media/mobile-engagement-unity-ios-get-started/75.png
