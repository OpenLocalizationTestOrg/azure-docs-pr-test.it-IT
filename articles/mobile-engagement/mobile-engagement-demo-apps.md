---
title: app demo di Mobile Engagement aaaAzure | Documenti Microsoft
description: Viene descritto dove toodownload, come toouse e hello vantaggi dell'utilizzo di Azure Mobile Engagement demo app
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: f624d5aa-254b-4ad0-96a3-f00e6c3a2c97
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2016
ms.author: piyushjo
ms.openlocfilehash: 9ff0df0d21e1bad6aff573db49304a55593df1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-demo-app"></a>App demo di Azure Mobile Engagement
Abbiamo pubblicata un'app demo di Azure Mobile Engagement per **iOS**, **Android**, e **Windows** toohelp piattaforme è toofind utili e altre informazioni sui dispositivi mobili Engagement.

app Hello consente di:

* Trovare con facilità collegamenti utili le risorse di Engagement tooMobile come video, documentazione, forum di supporto, hello e in cui le richieste toogo tooraise funzionalità.
* Notifiche di esempio di esperienza supportati da idee tooget Mobile Engagement per applicazioni mobili.
* Utilizzare un toostudy di implementazione di riferimento come tooimplement Mobile Engagement nell'applicazione. È possibile apprendere come:
  
  * Raccogliere dati di analisi.
  * Implementare scenari di notifica avanzati di tipi come *Schermo intero intermedio* o *Popup*.
  * Implementare indagini e sondaggi.
  * Implementare scenari di push di dati e push non interattivi.   

## <a name="app-installation"></a>Installazione di app
Questa app è disponibile in hello archivi di app seguenti:

* **App universale di Windows - Demo**:
  
  * Scaricare l'applicazione hello in hello [App di Windows store](https://www.microsoft.com/en-us/store/apps/azure-mobile-engagement/9nblggh4qmh2).
  * app Hello è stato sviluppato come app universali di Windows 10. è disponibile nel codice sorgente Hello [GitHub](https://github.com/Azure/azure-mobile-engagement-app-windows).
* **App demo per iOS**:
  
  * Scaricare l'applicazione hello in hello [Apple store](https://itunes.apple.com/us/app/azure%20mobile%20engagement/id1105090090).
  * si è sviluppato Hello app in iOS Swift. è disponibile nel codice sorgente Hello [GitHub](https://github.com/Azure/azure-mobile-engagement-app-ios).
* **App demo per Android**:
  
  * Scaricare l'applicazione hello in hello [Google Play store](https://play.google.com/store/apps/details?id=com.microsoft.azure.engagement).
  * è disponibile nel codice sorgente Hello [GitHub](https://github.com/Azure/azure-mobile-engagement-app-android).

![App universale di Windows - Demo][1]

![App demo per iOS][2]
![App demo per Android][3]

## <a name="usage"></a>Utilizzo
È possibile usare questa app in hello seguenti modi:

**Scaricare hello app nel dispositivo da collegamenti di archivio di applicazione hello (forniti in precedenza):**

> [!IMPORTANT]
> Non è necessario un account di Azure o necessario tooconnect hello app tooa back-end. Hello app funziona in modo indipendente.
> 
> 

* Dopo aver hello app sul dispositivo, è possibile passare attraverso collegamenti hello in hello dal menu a sinistra toofind hello risorse utili sull'Engagement Mobile.
* Sono stati aggiunti hello [feed RSS del servizio](https://aka.ms/azmerssfeed) a questa applicazione in modo che vengono sempre aggiornate sugli ultimi aggiornamenti di prodotto hello.
* È anche possibile passare tramite hello esempio notifica scenari tooexperience hello il tipo di notifiche che sono supportati da Mobile Engagement per ogni piattaforma. Queste notifiche possono essere esperti in locale, vale a dire, è possibile fare clic pulsanti hello tooshow schermate hello hello esperienza notifiche, ovvero le notifiche di hello toosending identico dalla piattaforma Mobile Engagement hello.

![Menu dell’app per Windows][4]

![Menu dell'app per iOS][5]
![Menu dell'app per Android][6]

**Scaricare il codice sorgente di hello da hello collegamenti GitHub (forniti in precedenza):**

* Dopo aver scaricato il codice sorgente hello, aprirlo in ambiente di sviluppo rispettivi hello - XCode per iOS, Android Studio per Android e Windows per Visual Studio.
* È quindi necessario seguire il nostro [passaggi base per l'integrazione SDK](mobile-engagement-windows-store-dotnet-get-started.md) in modo che si è in grado di tooconnect tooits questa app proprietari di istanza di back-end Mobile Engagement.
  * È necessario tooconfigure una stringa di connessione in app hello.
  * Piattaforma di notifica push di tooconfigure hello è inoltre necessario per l'app.
* Si noterà che app hello stesso è instrumentato con Engagement Mobile. Pertanto, quando si apre l'applicazione hello dopo la connessione è toohello back-end, sarà toosee in grado di sessione di utente hello, attività, eventi e così via, in hello **monitoraggio** scheda.
* Sarà inoltre in grado di toosend notifiche toothis app dalla propria istanza di Mobile Engagement, anziché utilizzare le notifiche locale.
  
  * Qui è possibile aggiungere il dispositivo come un dispositivo di test utilizzando hello **Get hello ID dispositivo** voce di menu in app hello. In questo modo viene fornito un ID dispositivo da registrare come dispositivo di test con l'istanza del back-end della piattaforma.
    
    ![ID dispositivo in Windows][7]
    
    ![ID del dispositivo in iOS][8]
    ![ID del dispositivo in Android][9]

## <a name="key-features-of-hello-demo-app"></a>Funzionalità principali di app demo hello
* Come accennato in precedenza, con questa app, sono disponibili tutte le risorse principali di hello per Mobile Engagement in mano. È possibile passare attraverso collegamenti hello nel menu di sinistra hello.
* Si possono provare le notifiche out-of-app per ogni piattaforma. Queste notifiche possono essere fornite come **sola notifica**, in cui facendo clic sulla notifica hello semplicemente visualizzata una schermata nativa dell'applicazione hello (utilizzando **il collegamento completo**), o come un **Web annuncio**, in cui è possibile recapitare contenuto HTML aggiuntivo da hello end Mobile Engagement nuovamente visualizzato quando si fa clic su notifica hello toobe.
  
    ![Notifiche out-of-app][29]
* In iOS, è necessario tooclose hello app toosee hello out dell'app o sistema di notifiche push. È possibile esaminare qui l'implementazione hello per l'aggiunta di **pulsanti di azione**, come quelle che vengono aggiunti toothis notifica di fuori dell'app per hello *Feedback* e *condivisione* (in modo che utente Hello può richiedere il diritto di azione dalla notifica hello stesso).
  
    ![Notifiche out-of-app in iOS][11] ![Visualizzazione di notifiche out-of-app in iOS][14]
* Opzioni hello supportate in Android, aggiungere testo su più righe (**testo Big**) o un'immagine di notifica (**quadro generale**) notifica toohello, insieme a hello **pulsantidiazione** (come supportato da iOS).
  
    ![Notifiche out-of-app in Android][12] ![Visualizzazione di notifiche out-of-app in Android][15]
* In Windows 10, è possibile visualizzare l'aspetto delle notifiche di hello in hello PC. Questa notifica viene visualizzato anche in Windows 10 hello **centro notifiche**. Nessun supporto per l'aggiunta di **pulsanti di azione** nel momento hello hello Windows SDK.
  
    ![Notifiche out-of-app in Windows][10] ![Visualizzazione out-of-app in Windows][13]
* Si possono provare le notifiche “in-app” per ogni piattaforma. Si tratta di un'operazione in due fasi in cui viene prima visualizzata una finestra di **notifica** . Quando viene selezionata, viene visualizzata una schermata piena **annuncio**, come visualizzato nella seguente schermata hello. il contenuto di Hello questo annuncio proviene dall'istanza del back-end Mobile Engagement. Hello SDK include modelli di hello per le notifiche e gli annunci. È anche possibile facilmente personalizzare, come illustrato in questa app demo con aggiunta di hello del logo e la colorazione.  
  
    ![Notifiche in-app in Windows][16]
  
    ![Notifiche in-app in iOS][17]  ![Notifiche in-app in Android][18]
  
    **iOS**, **Android**
* È inoltre possibile utilizzare hello **categoria** funzionalità di Mobile Engagement toocustomize questa esperienza predefinita. In app demo hello è stati illustrati due modi toochange hello esperienza comune di notifiche di hello. Si noti che funzionalità di categoria hello non è ancora supportato in Windows SDK hello.
  
    **Schermo intero intermedio:**
  
    ![Notifica in-app - Categoria schermo intermedio][30]
  
    ![Categoria schermo intermedio in iOS][21]     ![Categoria schermo intermedio in Android][22]
  
    **Notifica popup:**
  
    ![Notifica in-app - Categoria popup][31]
  
    ![Notifica popup in iOS][19]    ![Notifica popup in Android][20]

**iOS**, **Android**

* Mobile Engagement supporta anche un tipo specifico di notifica in-app chiamato **Sondaggi**, In questo modo toosend gli utenti di app tooyour segmentata sondaggi rapidi. È possibile aggiungere domande e le opzioni per ogni domanda come hello seguente schermata. Questa verrà quindi viene visualizzata come un utente di app toohello notifica in-app.   
  
    ![Notifiche di sondaggi][32]
  
    ![Sondaggi in Windows][26]
  
    ![Sondaggi in iOS][27]   ![Sondaggi in Android][28]

**iOS**, **Android**

* Mobile Engagement supporta anche l'invio automatico di notifiche **Push di dati**. Con queste notifiche, è possibile inviare dati dal servizio (ad esempio hello i dati JSON nel seguente esempio hello), che è possibile gestire nell'app e intraprendere le azioni. Un esempio è la modalità stiamo cambiando il prezzo di hello di un elemento in modo selettivo mediante le notifiche push di dati.
  
    ![Notifica push di dati][33]
  
    ![Notifica push di dati in Windows][23]
  
    ![Notifica push di dati in iOS][24]  ![Notifica push di dati in Android][25]

**iOS**, **Android**

> [!NOTE]
> È possibile visualizzare istruzioni dettagliate per qualsiasi di queste notifiche facendo **fare clic qui per istruzioni su come toosend queste notifiche dalla piattaforma Mobile Engagement** in qualsiasi schermata di notifica di esempio.
> 
> 

[1]: ./media/mobile-engagement-demo-apps/home-windows.png
[2]: ./media/mobile-engagement-demo-apps/home-ios.png
[3]: ./media/mobile-engagement-demo-apps/home-android.png
[4]: ./media/mobile-engagement-demo-apps/menu-windows.png
[5]: ./media/mobile-engagement-demo-apps/menu-ios.png
[6]: ./media/mobile-engagement-demo-apps/menu-android.png
[7]: ./media/mobile-engagement-demo-apps/device-id-windows.png
[8]: ./media/mobile-engagement-demo-apps/device-id-ios.png
[9]: ./media/mobile-engagement-demo-apps/device-id-android.png
[10]: ./media/mobile-engagement-demo-apps/out-of-app-windows.png
[11]: ./media/mobile-engagement-demo-apps/out-of-app-ios.png
[12]: ./media/mobile-engagement-demo-apps/out-of-app-android.png
[13]: ./media/mobile-engagement-demo-apps/out-of-app-display-windows.png
[14]: ./media/mobile-engagement-demo-apps/out-of-app-display-ios.png
[15]: ./media/mobile-engagement-demo-apps/out-of-app-display-android.png
[16]: ./media/mobile-engagement-demo-apps/in-app-windows.png
[17]: ./media/mobile-engagement-demo-apps/in-app-ios.png
[18]: ./media/mobile-engagement-demo-apps/in-app-android.png
[19]: ./media/mobile-engagement-demo-apps/pop-up-ios.png
[20]: ./media/mobile-engagement-demo-apps/pop-up-android.png
[21]: ./media/mobile-engagement-demo-apps/interstitial-ios.png
[22]: ./media/mobile-engagement-demo-apps/interstitial-android.png
[23]: ./media/mobile-engagement-demo-apps/data-push-windows.png
[24]: ./media/mobile-engagement-demo-apps/data-push-ios.png
[25]: ./media/mobile-engagement-demo-apps/data-push-android.png
[26]: ./media/mobile-engagement-demo-apps/survey-windows.png
[27]: ./media/mobile-engagement-demo-apps/survey-ios.png
[28]: ./media/mobile-engagement-demo-apps/survey-android.png
[29]: ./media/mobile-engagement-demo-apps/out-of-app.png
[30]: ./media/mobile-engagement-demo-apps/in-app-interstitial.png
[31]: ./media/mobile-engagement-demo-apps/in-app-pop-up.png
[32]: ./media/mobile-engagement-demo-apps/notification-poll.png
[33]: ./media/mobile-engagement-demo-apps/notification-data-push.png
