---
title: Interfaccia utente di Engagement Mobile - Reach aaaAzure
description: Informazioni su come tooreach toohello utenti dell'applicazione con Azure Mobile Engagement le notifiche push
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: d96e2590-08dd-4481-a352-2c18f26a1643
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 40d5162ddeccec82c2c9f5b0d72b4cb10c9ddc38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreach-out-toohello-users-of-your-application-with-push-notifications"></a>Come tooreach toohello utenti dell'applicazione con le notifiche push
Questo articolo descrive hello **raggiungere** scheda di hello **Mobile Engagement** portale. Utilizzare hello **Mobile Engagement** toomonitor portale e gestire le App per dispositivi mobili. Si noti che toostart tramite il portale di hello è innanzitutto necessario toocreate un **Azure Mobile Engagement** account. Per ulteriori informazioni, vedere [Creare un account Azure Mobile Engagement](mobile-engagement-create.md).

Hello raggiungere sezione dell'interfaccia utente è hello lo strumento Gestione campagna Push hello in cui è possibile creare/modificare/attiva/fine/monitoraggio e ottenere le statistiche sulle campagne di notifica Push e sulle funzionalità che è possibile accedere tramite l'API Reach hello (e alcuni elementi di hello bassa livello API Push). Tenere presente che se si utilizza hello API o hello dell'interfaccia utente, sarà necessario toointegrate Azure Mobile Engagement sia portata nell'applicazione per ogni piattaforma con hello SDK prima di poter usare raggiungere campagne.

> [!NOTE]
> Numero di sezioni di hello **Mobile Engagement** interfaccia utente del portale contengono hello **Mostra Guida** pulsante. Premere tooget questo pulsante più informazioni contestuali su una sezione.
> 
> 

## <a name="four-types-of-push-notifications"></a>Quattro tipi di notifiche push
1. Annunci - Consenti toosend pubblicità messaggi toousers che reindirizza tooanother posizione all'interno di applicazione o toosend le pagine Web tooa o archiviare all'esterno dell'app. 
2. Esegue il polling - consentono ponendo domande toogather informazioni dagli utenti finali.
3. Push di dati - consentono toosend un file di dati binary o base64. informazioni di Hello contenute in un push di dati inviati tooyour applicazione toomodify esperienza corrente degli utenti nell'applicazione. L'applicazione deve toobe tooprocess in grado di hello dati di un push di dati.

## <a name="campaign-details"></a>Dettagli della campagna
È possibile eliminare, modificare o clonare o attivare campagne che non sono stati ancora attivate passando sopra i nomi o è possibile fare clic su tooopen li. È possibile duplicare le campagne che sono già state attivate passando sopra i nomi o è possibile fare clic su tooopen li. Tuttavia, non è possibile modificare una campagna dopo che è stata attivata.

![Reach1][18]

## <a name="reach-feedback"></a>Feedback di Reach
Fare clic su **statistiche** dettagli hello toosee di una campagna di copertura. Hello **semplice** Vista fornisce una rappresentazione visiva sotto forma di hello di un grafico a barre su cosa è successo dopo che è stata attivata una campagna di colonna. Hello **avanzate** visualizzazione fornisce dettagli più granulari sulla campagna push hello. Questi dettagli non sarà disponibili se si invia una campagna di test, ovvero un dispositivo di test inviato tooa push. Le informazioni devono essere interpretate nel modo seguente:

1. **Inserito** -specifica il numero di hello di messaggi con push toohello dispositivi. Questo numero dipenderà dai destinatari hello specificato durante la creazione della campagna push hello. Se non si specifica un gruppo di destinatari, i dispositivi registrato hello tooall verrà inviato il push. Come tutti gli altri servizi, push è non notifiche di push hello direttamente i dispositivi toohello ma invece inviarli toohello rispettivi piattaforma servizi di notifica Push specifici (PNS - APNS/GCM/WNS) in modo che è possibile recapitare le notifiche di hello toohello dispositivi. 
2. **Recapitati** -specifica il numero di hello di messaggi che vengono recapitati dal dispositivo di toohello PNS hello e riconosciuto come ricevuto da Mobile Engagement SDK. 
   
   *Motivi per cui il numero dei messaggi Recapitati può essere inferiore al numero dei massaggi Inviati:*
   
   1. Se l'utente hello è disinstallato l'applicazione hello dal dispositivo hello ma hello PNS non riconosce in fase di hello che inviamo hello push toohello PNS messaggio hello verrà eliminato.
   2. Se il dispositivo di hello è applicazione hello ma dispositivi hello stessi sono stati offline per lunghi periodi di tempo, quindi hello PNS avrà esito negativo dispositivo toohello messaggio hello di toodeliver. 
   3. Se il messaggio hello ottenere recapitato toohello dispositivo ma Ciao hello app Mobile Engagement SDK non riconosce il contenuto di hello del messaggio hello, Elimina il messaggio. Questo problema può verificarsi se personalizzazione hello della notifica hello in app hello genera un'eccezione che viene rilevato nel messaggio di hello hello SDK e drop. Ciò può verificarsi anche se app hello dispositivo hello è utilizzando una versione di hello Mobile Engagement SDK che non è in grado di toounderstand hello versione messaggio hello del push inviate da piattaforma hello ma si tratta solo quando l'applicazione hello è stato aggiornato dopo la notifica hello è stata inviata da piattaforma hello del servizio. Hello **avanzate** scheda indicherà il numero di messaggi sono stato eliminato. 
   4. Nei dispositivi iOS, i messaggi a volte non venga recapitati se dei dispositivi hello nella batteria in esaurimento o se l'app hello utilizza notevole quantità di energia durante l'elaborazione remote notifiche. Si tratta di un limite di dispositivi iOS hello.   
3. **Visualizzato** -specifica il numero di hello di messaggi che vengono correttamente visualizzati toohello utente di app nel dispositivo hello sotto forma di hello di una notifica push/out-di-app di sistema nel centro notifiche hello o una notifica in-app all'interno di hello mobili app.  Hello **avanzate** scheda indicherà quante sono le notifiche di sistema e quanti notifiche nell'applicazione. 
   
   *Conteggio dei motivi per visualizzare sia minore di count consegnati (in attesa toobe visualizzato)*
   
   1. Se ha una data di fine su di esso, è possibile che notifica hello è stata recapitata, ma quando il tempo di hello proviene tooopen campagna notifica hello e la Visualizza utente app toohello, è stato già scaduto in modo che non è stato visualizzato.   
   2. Se una notifica in-app è la notifica di hello notifica hello è visualizzata solo se l'utente app hello apre l'applicazione hello. Nei casi in cui utente app hello non è stato aperto l'applicazione hello, hello SDK segnalerà che notifica hello è stata recapitata, ma non ancora visualizzata finché non viene aperto l'applicazione hello. 
   3. Se notifica hello è una notifica in-app e configurato toobe visualizzato in una determinata attività o la stessa schermata anche notifica hello verrà segnalata come recapitati ma non ancora consegnate fino a quando l'utente di hello apre app hello in una schermata specifica. 
4. **Le interazioni utente** -specifica il numero di hello di messaggi di cui l'utente app hello ha interagito con e includerà i messaggi hello che sono azioni o chiusi. 
   
   * *Hello app è possibile eseguire azioni una notifica in uno dei seguenti modi hello:*
     
     1. Se hello notifica è una notifica di sistema/out-di-app o inviata una notifica in-app come sola notifica l'utente di app hello fa clic sulla notifica hello.
     2. Se notifica hello è una notifica in-app con un testo o di una visualizzazione web o viene eseguito il polling hello quindi utente app fa clic su hello pulsante di azione di notifica hello.
     3. Se la notifica hello è quindi una notifica in-app con una visualizzazione web hello app utente fa clic su un URL hello web solo nella visualizzazione [Android]
   * *utente applicazione Hello può chiudere una notifica in uno dei seguenti modi hello:*
     
     1. Fare clic sul pulsante Chiudi hello notifica hello direttamente. 
     2. Passaggio di stoccaggio o l'eliminazione di notifica hello. 
     3. Le notifiche in-app con il contenuto di testo/web e viene eseguito il polling sono utente app toohello in genere visualizzati in un processo in due passaggi. Viene visualizzato prima una notifica e quando si fa clic su di essa, viene visualizzato il contenuto di testo/web/polling successivi hello. utente applicazione Hello può chiudere una notifica in uno di questi passaggi e i dettagli di hello nella vista avanzata hello acquisisce questo. 
5. **Azioni** -specifica il numero di hello di messaggi che sono stati azioni in modo esplicito dall'utente di app hello. Si tratta di numero più interessante hello in questo modo viene indicato il numero di utenti app sono stato interessato dal messaggio hello inserite nella notifica hello. 

> [!NOTE]
> IOS & piattaforme Windows, se hello utente dispone di app hello aperta e campagna hello è stata una campagna "In qualsiasi momento" è possibile che le notifiche di app e in app visualizzarle nella hello contemporaneamente. Ciò potrebbe causare un conteggio visualizzate superiore hello consegnati. Se l'utente hello interagisce o notifica hello azioni, quindi anche hello interazioni utente/Actioned conteggio potrebbe essere maggiore di recapito. 
> 
> 

![Reach2][19]

## <a name="see-also"></a>Vedere anche
* [Concetti][Link 6]
* [Guida alla risoluzione dei problemi - Assistenza][Link 24]

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

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
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

