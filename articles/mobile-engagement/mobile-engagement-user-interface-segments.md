---
title: aaaAzure interfaccia utente di Engagement Mobile - segmenti
description: Informazioni su come toocreate e gestiscono segmenti di modelli di utilizzo tooidentify gli utenti con Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6a4f2205-4a3c-406e-a04f-5e6f2a36653f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bb214c45d05ebfbf243978658a7e331d4a7c6e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-segments-of-users-tooidentify-usage-patterns"></a>Come toocreate e gestiscono segmenti di modelli di utilizzo tooidentify utenti
Questo articolo descrive hello **segmenti** scheda di hello **Mobile Engagement** portale. Utilizzare hello **Mobile Engagement** toomonitor portale e gestire le App per dispositivi mobili.

sezione di segmenti Hello di hello dell'interfaccia utente consente toowork nella segmentazione agli utenti in base a un comportamento diverso hello e analitica che è possibile ottenere da un'applicazione hello e possono accedere anche tramite API di segmenti hello. Segmenti vengono innanzitutto calcolati 24 ore dopo che sono stati creati e vengono ricalcolate ogni 24 ore in base alle informazioni analitica più recente di hello. Una volta che viene calcolato un segmento, viene visualizzato un grafico "Cronologia tooday giorno" ogni giorno.

> [!NOTE]
> Numero di sezioni di hello **Mobile Engagement** interfaccia utente del portale contengono hello **Mostra Guida** pulsante. Premere tooget questo pulsante più informazioni contestuali su una sezione.
> 
> 

## <a name="create-segments"></a>Creare segmenti
È possibile creare un segmento di base dei criteri too10 di un periodo specifico di giorni too60 hello passato dalla sezione analitica hello. Ad esempio, è possibile creare un segmento in base alle persone hello che dispongono di visualizzare alcune pagine o cercare contenuto specifico all'interno dell'app all'interno di hello ultimi 10 giorni. Queste informazioni sono disponibili nella sezione analitica hello. In tal caso, è possibile usarlo toocreate un segmento e quindi impostare un tootarget di notifica push questo subset di utenti tooget li toocome toohello indietro applicazione. 

> [!NOTE]
> una volta calcolato, un segmento non può essere modificato; può essere solo duplicato (copiato) o distrutto (eliminato). È possibile duplicare un segmento all'interno di hello stessa applicazione (con hello AppID stesso), e possono anche essere clonato in altre applicazioni (con un ID applicazione diverso). 

 ![segments1][35] 

## <a name="examples-segments"></a>Esempi di segmento
 ![segments2][36]

Segmenti consentono agli utenti finali hello toosegment dell'applicazione.
La segmentazione degli utenti è un'importante strategia di marketing. Azure Mobile Engagement consente dati cronologici tooget e creare segmenti di personalizzati. Questo potente strumento consente toolearn sull'esperienza dei clienti dell'applicazione. È possibile analizzare facilmente i segmenti e utilizzarli come destinazioni di push.
Un caso di utilizzo comune è che si desidera toosend tooencourage una notifica push il toorate gli utenti finali dell'applicazione nell'archivio di hello. Anziché inviare una notifica tooall agli utenti finali, è possibile creare un segmento che è necessario specificare solo gli utenti che hanno utilizzato l'applicazione ogni giorno per ultimo mese hello e hanno avuto esperienza di un utente. Quando si invia un numero inferiore di notifiche push mirate, è possibile ottenere un ritorno sugli investimenti migliore.

 ![segments3][37]

### <a name="segments-you-can-create-based-on-hello-major-azure-mobile-engagement-elements"></a>Segmenti che è possibile creare in base agli elementi di Azure Mobile Engagement principali hello:
* Evento: creare un segmento di tale evento specifico di destinazioni con uno di un'applicazione hello che si sono verificati più di due volte a settimana. 
* Sessione: creazione di un segmento di utenti che hanno utilizzato più di 5 volte la settimana scorsa un'applicazione hello.
* Attività: creare un segmento di utenti che hanno utilizzato una pagina o un contenuto più o meno di 10 volte nell'ultimo mese.
* Processo: creare un segmento di utenti che hanno completato un processo più di due volte al giorno.
* Arresto anomalo: creazione di un segmento di tutti gli utenti di hello che hanno subito un arresto anomalo di più di 10 volte la settimana scorsa. (il push per questo segmento dovrebbe includere un messaggio di scuse ed eventualmente un buono).
* Errore: creare un segmento di tutti gli utenti di hello che hanno un errore più di 100 volte ultimi 3 giorni.
* App Info: creazione di un segmento che ha come destinazione un App Info personalizzato che si sono verificati durante hello ultimi 25 giorni.
  
  ![segments4][38]

toouse segmento in modo ottimale, è necessario aver eseguito un'integrazione personalizzata di hello SDK nell'applicazione con un piano di assegnazione di tag di tag "App Info".
Quindi, passare toohello home page di interfaccia di hello, selezionare un'applicazione hello desiderato e fare clic sulla sezione "Segmenti" hello.

1. Selezionare una sezione "Segmenti" hello.
2. Fare clic su "Nuovo segmento" hello pulsante toocreate un nuovo segmento.

## <a name="real-life-example-create-a-simple-segment-based-on-session-information"></a>Esempio di vita reale: creare un segmento semplice in base alle informazioni di "Sessione"
Creare un segmento di tutti gli utenti finali hello che hanno utilizzato almeno 50 volte l'app in hello ultima settimana. Da qui, trovare solo gli utenti finali hello impiegato almeno 30 secondi nell'app per ogni sessione. Verranno visualizzati tutti hello agli utenti finali un'esperienza positiva nell'app. Quindi, segmento hello creato potrebbe essere utilizzato toopush un tooask gli utenti finali di notifica toothese li toorate l'app in hello archiviare.

 ![segments5][39]

1. Assegnare un nome di segmento in ordine toofind rapidamente nell'elenco di "Segmento" hello.
2. Fare clic sul hello pulsante "Crea".
   
   ![segments6][40]

Selezionare Sessione.

 ![segments7][41]

1. Selezionare il periodo di hello di "Ultima settimana".
2. Fare clic su Avanti.
   
   ![segments8][42]
3. Seleziona hello operatore rilevanti tra elenco hello: =; ≥, ≤.
4. Immettere hello numero desiderato.
5. Selezionare hello occorrenza desiderato. 
6. Fare clic su Avanti.
   In questo esempio viene impostato in modo che over hello ultima settimana, corrispondenza utenti che hanno almeno 50 sessioni.
   
   ![segments9][43]

Per hello segmentazione della sessione, è possibile scegliere di lunghezza hello per ogni sessione come criterio.

1. Selezionare hello operatore dall'elenco di hello.
2. Fornire hello lunghezza per ogni sessione.
3. Fare clic su Avanti.
   In questo esempio, afferma che su tutti hello sessioni che sono state segmentate nella sezione di occorrenza hello, selezionare solo gli utenti di hello impiegato più di 30 secondi per ogni sessione.
   
   ![segments10][44]

Nome del criterio di ordine tooretrieve in hello completare a imbuto e fare clic su Fine.

 ![segments11][45]

Al termine dell'impostazione del criterio, esso apparirà nel grafico a imbuto segmento hello.
Poiché un segmento è basato su dati di analisi, i segmenti vengono calcolati una volta al giorno.
In questo esempio, 47,7% degli utenti finali totale hello corrispondente criterio hello. Dovrebbero essere utenti hello hanno un'esperienza ottimale e sarà possibile tooprovide probabilmente una classificazione superiore, se si esegue il push in una notifica chiedere loro toorate hello app nell'archivio di hello.

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
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

