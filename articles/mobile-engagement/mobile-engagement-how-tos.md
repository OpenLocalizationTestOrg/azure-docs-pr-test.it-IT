---
title: aaaAzure interfaccia utente di Engagement Mobile - raggiungere procedura
description: Panoramica dell'interfaccia utente di Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 30af87e6-c816-4cce-8609-6cbd3e83de14
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4b6dafd09d894214d4c386f5c6f157a77671606f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-started-using-and-managing-pushes-tooreach-out-tooyour-end-users"></a>Come tooget all'utilizzo e gestione inserisce tooreach gli utenti finali tooyour
Una volta hello SDK è completamente integrato nell'app, è possibile iniziare utilizzando hello hello Reach sezione utenti hello UI tooPush notifiche toohello dell'app.  

## <a name="do-your-first-push-notification-campaign"></a>Creare la prima campagna di notifica push
* Verificare che la copertura è integrato nell'app con hello SDK. 
* Selezionare l'applicazione.

![First1][1]

* Visitare la sezione "Copertura" e fare clic su "nuovo annuncio" toohello

![First2][2]

* Creare una nuova campagna e assegnarle un nome.
  
![First3][3]

* Selezionare la modalità cui deve essere recapitata notifica hello, come In-app solo

![First4][4]

* Creare il messaggio hello da toopush

![First5][5]

* È possibile scrivere un titolo per la notifica di hello (facoltativo).
* Scrivere il contenuto del messaggio push.
* È possibile caricare un'immagine. Tenere presente che le dimensioni di hello del file hello non possono superare corrispondono a 32.768 byte.
* È inoltre hello possibilità tooselect di ulteriori opzioni, ma lo stato attivo hello di questa esercitazione, si potrà notare che in un secondo momento.
* Selezionare solo il tipo di contenuto hello come notifica

![First6][6]

* Creare la campagna push che verrà visualizzata nell'elenco di campagne.

![First7][7]

## <a name="test-your-push-notification-campaign"></a>Testare la campagna di notifica push
![Test1][8]

* Registrare il dispositivo.
* Fare clic sulla casella di controllo di hello del dispositivo hello desiderato toopush.
* Fare clic su hello "Test" toosend hello push toohello dispositivo.

![Test2][9]

* Attivare la campagna hello

![Test3][10]

* Dopo avere creato la campagna è sufficiente tooactivate per hello notifica toobe inserito tooyour utenti.

## <a name="send-personalized-pushes"></a>Inviare push personalizzati
* Questo esempio viene creato un push in cui un codice di sconto personalizzato viene inserito notifica push di hello.

![Personalize1][11]

Personalizzazione works sostituendo un marcatore da un tag di informazioni di app, pertanto, è necessario toomake hello utente che disponga hello corretto app-info definito per primo. In hello in questo esempio, gli utenti di destinazione avrà un tag di info app denominato rebate_code definito.
Contenuto di notifica push di hello include hello marcatore ${rebate_code} che indica che è sostituito dal contenuto effettivo di hello del tag di hello app info toobe visualizzati sopra.

> [!WARNING]
> Se il tag di hello app info non è definito per l'utente hello, utente hello non riceverà push hello.

* Risultato

![Personalize2][12]

### <a name="you-can-further-personalize-hello-text-your-notification"></a>È possibile personalizzare ulteriormente testo hello la notifica
![Personalize3][13]

* Inclusi titolo hello della notifica di hello,
* E il contenuto del messaggio hello hello.
* Scegliere il tipo di hello di annuncio (visualizzazione di testo o Web)

![Personalize4][14]

### <a name="hello-body-of-an-announcement-may-also-be-personalized-with"></a>corpo Hello di un annuncio può inoltre essere personalizzato con:
* URL di azione Hello, se si vuole hello toocustomize pagina di destinazione
* titolo Hello,
* corpo Hello del messaggio hello.

## <a name="differentiate-your-push-notification-in-or-out-of-app"></a>Differenziare la notifica push (all'interno o all'esterno dell'app)
* Scegliere il tipo di hello di notifica si verrà push, selezionare l'applicazione, passare toohello "Copertura" sezione, selezionare o creare una campagna push e passare toohello "Notifica" sezione.
* Fare clic su "modalità di consegna" hello desiderato.
* Fare clic sulla casella di controllo "Limitare l'attività" hello notifica si verifica su specifiche attività (schermate) hello.

![Differentiate1][15]

### <a name="out-of-app-only-delivery-mode"></a>Modalità di recapito "Solo all'esterno dell'app"
![Differentiate2][16]

"All'esterno dell'App solo" modalità di recapito notifica push quando un'applicazione hello viene chiuso. Si tratta di notifica push standard hello.
Quando si seleziona "da solo app", è necessario avere già fornito certificati hello dalla piattaforma hello che l'applicazione si basa sul (APN o GCM).

### <a name="see-also"></a>Vedere anche
* [Apple Push Notification Service - Certificati](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9), [Google Cloud Messaging - Certificato](http://developer.android.com/google/gcm/index.html) 

### <a name="in-app-only-delivery-mode"></a>Modalità di recapito "Solo in-app"
![Differentiate3][17]

Modalità di consegna "In-App solo" notifica push durante l'esecuzione di un'applicazione hello.
Per questa notifica, non è necessario toogo tramite hello APNS e sistema GCM.
È possibile utilizzare tooreach di sistema di recapito nell'applicazione hello agli utenti finali.
Completamente, è possibile personalizzare la notifica hello e decidere in quali attività (schermata) verrà visualizzata la notifica hello.

### <a name="anytime-delivery-mode"></a>Modalità di recapito "Sempre"
È possibile scegliere una modalità di consegna "In qualsiasi momento", si assicura tooreach hello se l'utente finale dell'applicazione è in esecuzione o non.
Quando si seleziona "In qualsiasi momento", è necessario avere già fornito certificati hello dalla piattaforma hello che l'applicazione è basandosi su (APN o GCM). 

## <a name="schedule-a-push-campaign"></a>Pianificare una campagna push
### <a name="plan-toostart-a-campaign"></a>Pianificare una campagna tooStart
![Shedule1][18]

È hello 21 di marzo e si dispone di un annuncio toomake e le per hello 22 di marzo a mezzanotte. Non è toostay davanti hello interfaccia toodo di push. È possibile pianificare in anticipo hello esatta minuto le notifiche verranno inviate.

* Deselezionare hello "None" casella di controllo e selezionare un'ora di inizio 
* Scegliere hello data e ora di hello che toostart hello push campagna.

### <a name="plan-tooend-a-campaign"></a>Pianificare una campagna tooend
![Shedule2][19]

Si desidera toostop la campagna su hello 25 di marzo 3 PM 00 ma si conosce, non sarà presente toodo è.
Non è toostay davanti toopush interfaccia hello! È possibile pianificare in anticipo hello esatta minuto che la campagna verrà interrotta.

* Fare clic su hello "None" casella di controllo o selezionare un'ora di fine
* Scegliere hello data e ora di hello che toofinish hello push campagna.

### <a name="end-a-campaign-manually"></a>Terminare manualmente una campagna
![Shedule3][20]

Per impostazione predefinita, hello "None" vengono selezionate le caselle di controllo.
Ciò significa che campagna hello verrà avviata appena si attivarlo in hello raggiungere sezione e fine durante l'esecuzione si arresterà in hello raggiungerà sezione.

> [!NOTE]
> Le campagne create senza una data di fine archiviano hello push localmente nel dispositivo hello e visualizzarlo hello successiva apertura app hello anche se la campagna hello manualmente viene terminata.

## <a name="enhance-a-push-notification-with-a-text-view"></a>Migliorare una notifica push con una visualizzazione testo
### <a name="what-is-a-text-view"></a>Cos'è una visualizzazione testo?
![TextView1][21]

Una visualizzazione testo è un popup con contenuto testuale. Questo popup viene visualizzato quando l'utente finale di hello ha fatto clic su notifica push di hello.
Una visualizzazione di testo consente toopresent più contenuto tooyour per l'utente finale. Si tratta di hello opportunità toopresent tooaction una chiamata, ad esempio del passaggio tooa pagina dell'app, il reindirizzamento tooa archivio, aprire una pagina web, l'invio messaggio di posta elettronica, avviare una ricerca geografica localizzate e così via...

### <a name="example-text-view"></a>Esempio: visualizzazione testo
* Creare una campagna di notifica Push nella sezione "Raggiungere" hello e assegnare un nome di una campagna

![TextView2][22]

* Scrivere un messaggio hello che verrà visualizzato per la notifica di hello.
* Selezionare tipo di contenuto di annuncio di "testo" hello

![TextView3][23]

> [!NOTE]
> Quando si effettua il push di una visualizzazione testo, prima viene sempre visualizzata una notifica. 

* Definire il testo hello (dopo la selezione di contenuto di annuncio hello testo, verrà visualizzato sottosezione hello, consentendo toodefine hello testo toobe visualizzato.)

![TextView4][24]

* Scrivere hello titolo che verrà visualizzato all'inizio di hello del messaggio hello.
* Scrivere il contenuto principale hello della visualizzazione di testo hello.
* Scrivere il contenuto di hello che verrà visualizzato sul pulsante di azione hello (un pulsante di azione consente toomake applicazione hello un'azione specifica, ad esempio l'apertura di una pagina dell'applicazione hello, reindirizzamento tooan App store o qualsiasi tipo di origini, che è possibile fornire).
* Contenuto di hello scrittura che verrà visualizzato nel pulsante di uscita hello (facendo clic sul pulsante di uscita hello, visualizzazione del testo hello scomparirà.)
* Creare una campagna di notifica push e verrà visualizzato nell'elenco di hello campagna.

![TextView5][25]

* Attivare i push notifica della campagna toosend hello testo visualizzare tooyour gli utenti.

![TextView6][26]

* Risultato

![TextView7][27]

* Hello utente riceve una notifica di hello e fare clic su di esso.
* visualizzazione del testo Hello viene visualizzato come un toointeract utente hello consentendo a comparsa con esso.

## <a name="enhance-a-push-notification-with-a-web-view"></a>Migliorare una notifica push con una visualizzazione Web
### <a name="what-is-a-web-view"></a>Cos'è una visualizzazione Web?
![WebView1][28]

Una visualizzazione Web è un popup con contenuto Web. Questo popup viene visualizzato quando l'utente finale di hello ha fatto clic su notifica push di hello.
Una visualizzazione web consente toohave ulteriori interazione dell'utente finale di hello.
Si tratta di hello opportunità toopresent tooaction una chiamata ad esempio il reindirizzamento tooApp archivio, aprire una pagina web, l'invio messaggio di posta elettronica, avviare una ricerca geografica localizzate e così via...

### <a name="example-web-view"></a>Esempio: visualizzazione Web
* Creare la campagna Push nella sezione "Raggiungere" hello e assegnare un nome di una campagna.

![WebView2][29]

* Scrivere un messaggio hello che verrà visualizzato per la notifica di hello.
* Selezionare il tipo di contenuto annuncio hello come "web".

![WebView3][30]

### <a name="about-announcement-types"></a>Informazioni sui tipi di annuncio:
* Solo notifica: una semplice notifica standard. Vale a dire che se un utente fa clic su di esso, non verranno visualizzato visualizzazioni aggiuntive, ma solo l'azione di hello associata tooit si verificherà.
* Annuncio di testo: si tratta di una notifica che coinvolge hello utente toohave un'occhiata a una visualizzazione di testo.
* Annuncio Web: si tratta di una notifica che coinvolge hello utente toohave un'occhiata a una visualizzazione web.
  Selezionare hello contenuto "Annuncio Web".

> [!NOTE]
> quando si effettua il push di una visualizzazione Web, prima viene sempre visualizzata una notifica.

* Definire il contenuto web hello (dopo avere selezionato il contenuto web annuncio hello, verrà visualizzata la sottosezione hello, consentendo toodefine hello web Visualizza il contenuto visualizzato toobe.)

![WebView4][31]

* Scrivere hello titolo che verrà visualizzato all'inizio di hello del messaggio hello (facoltativo).
* Scrivere qui il codice HTML.
* Fare clic su origine hello edition tooswitch pulsante di modalità di modifica e verificarne l'aspetto simile.
* Scrivere il contenuto di hello che verrà visualizzato sul pulsante di azione hello (un pulsante di azione consente toomake applicazione hello un'azione specifica, ad esempio l'apertura di una pagina dell'applicazione hello, reindirizzamento tooa archivio o qualsiasi tipo di origini, che è possibile fornire).
* Contenuto di hello scrittura che verrà visualizzato nel pulsante di uscita hello (facendo clic sul pulsante di uscita hello, visualizzazione web hello scompare).
* Risultato

![WebView5][32]

* utente Hello ricevere una notifica di hello e fare clic su di esso.
* visualizzazione del testo Hello viene visualizzato come un toointeract utente hello consentendo a comparsa con esso.

<!--Image references-->
[1]: ./media/mobile-engagement-how-tos/First1.png
[2]: ./media/mobile-engagement-how-tos/First2.png
[3]: ./media/mobile-engagement-how-tos/First3.png
[4]: ./media/mobile-engagement-how-tos/First4.png
[5]: ./media/mobile-engagement-how-tos/First5.png
[6]: ./media/mobile-engagement-how-tos/First6.png
[7]: ./media/mobile-engagement-how-tos/First7.png
[8]: ./media/mobile-engagement-how-tos/Test1.png
[9]: ./media/mobile-engagement-how-tos/Test2.png
[10]: ./media/mobile-engagement-how-tos/Test3.png
[11]: ./media/mobile-engagement-how-tos/Personalize1.png
[12]: ./media/mobile-engagement-how-tos/Personalize2.png
[13]: ./media/mobile-engagement-how-tos/Personalize3.png
[14]: ./media/mobile-engagement-how-tos/Personalize4.png
[15]: ./media/mobile-engagement-how-tos/Differentiate1.png
[16]: ./media/mobile-engagement-how-tos/Differentiate2.png
[17]: ./media/mobile-engagement-how-tos/Differentiate3.png
[18]: ./media/mobile-engagement-how-tos/Schedule1.png
[19]: ./media/mobile-engagement-how-tos/Schedule2.png
[20]: ./media/mobile-engagement-how-tos/Schedule3.png
[21]: ./media/mobile-engagement-how-tos/TextView1.png
[22]: ./media/mobile-engagement-how-tos/TextView2.png
[23]: ./media/mobile-engagement-how-tos/TextView3.png
[24]: ./media/mobile-engagement-how-tos/TextView4.png
[25]: ./media/mobile-engagement-how-tos/TextView5.png
[26]: ./media/mobile-engagement-how-tos/TextView6.png
[27]: ./media/mobile-engagement-how-tos/TextView7.png
[28]: ./media/mobile-engagement-how-tos/WebView1.png
[29]: ./media/mobile-engagement-how-tos/WebView2.png
[30]: ./media/mobile-engagement-how-tos/WebView3.png
[31]: ./media/mobile-engagement-how-tos/WebView4.png
[32]: ./media/mobile-engagement-how-tos/WebView5.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

