---
title: aaaAzure interfaccia utente di Engagement Mobile - Analitica
description: Informazioni su come tooanalyze dati cronologici relativi all'applicazione con Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6b2533ac-b8ec-4e35-872c-d563895bdc0c
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4a9df11226fed6710cfb1337ae84ece7596d482f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooanalyze-historical-data-about-your-application"></a>Come tooanalyze dati cronologici relativi all'applicazione
Questo articolo descrive hello **analisi** scheda di hello **Mobile Engagement** portale. Utilizzare hello **Mobile Engagement** toomonitor portale e gestire le App per dispositivi mobili. Si noti che toostart tramite il portale di hello è innanzitutto necessario toocreate un **Azure Mobile Engagement** account.

Hello sezione Analitica di hello dell'interfaccia utente fornisce informazioni aggregate relative all'applicazione basata su dati storici che viene aggiornati ogni 24 ore. Hello informazioni vengono visualizzate in dashboard diversi composto mappe, griglie e grafici a barre/riga/torta. dati Hello possono essere scaricati anche come file con estensione csv. La maggior parte delle stesse informazioni è disponibile in tempo reale in hello sezione monitoraggio di hello dell'interfaccia utente e sono accessibili anche da hello API Analitica.

> [!NOTE]
> Numero di sezioni di hello **Mobile Engagement** interfaccia utente del portale contengono hello **Mostra Guida** pulsante. Premere tooget questo pulsante più informazioni contestuali su una sezione.

## <a name="standard-and-custom-analytics"></a>Analisi standard e personalizzate
Azure Mobile Engagement fornisce un set di base, standard informazioni analitiche relative alle applicazioni che possono essere rappresentate come integrare l'applicazione hello SDK. Azure Mobile Engagement anche informazioni hello possibilità toogather analitica personalizzate aggiuntive che si desidera sul comportamento degli utenti finali. È possibile eseguire questa operazione creando una pianificazione di "tag (informazioni dell'app)" personalizzata creata da **Impostazioni**. In questo modo, Azure Mobile Engagement può raccogliere questi dati aggiuntivi per conto dell'utente.

## <a name="analytics"></a>Analytics
* Dashboard: visualizza informazioni generali sugli utenti nuovi e attivi e sulle loro tendenze.
* Utenti: gli utenti sono identificati tramite l'identificatore del dispositivo. Questo valore è univoco per ogni dispositivo (a un nuovo utente corrisponde un nuovo dispositivo). Un utente viene considerato come nuovo in un determinato intervallo di tempo, se ha eseguito la prima sessione durante questo intervallo di tempo. Un utente viene considerato assorbito se ha eseguito almeno una sessione durante hello ultimi 7 giorni. Gli utenti attivi sono quelli che hanno effettuato almeno una sessione durante un determinato periodo. È possibile ordinarli per mese, settimana, giorno oppure ora. Tutti i grafici di hello simile, ma consentono di toofilter da diverse funzionalità, ad esempio versione di hello dell'applicazione e quindi toosort da un periodo di tempo. informazioni standard raccolte integrando hello SDK Hello includono segue hello: gli utenti attivi, nuovo utente, numero di sessioni, lunghezza di ogni sessione, informazioni tecniche sul paese hello, variabili locali, il percorso, il vettore di lingua, dispositivi, firmware, rete (Wi-Fi), le versioni di app hello e SDK, usato dai clienti. Queste informazioni possono essere visualizzate in tempo reale dalla sezione monitoraggio hello.

> [!NOTE]
> Hello periodo di tempo è basato sulla data hello dalle impostazioni del dispositivo degli utenti hello, pertanto un utente il cui telefono è data hello impostato in modo errato può visualizzati nella hello errato periodo di tempo.

* Assorbimento: un utente viene considerato come assorbito in un determinato intervallo di tempo se ha eseguito la prima sessione durante questo intervallo. È possibile modificare gli intervalli di tempo hello durante i quali vengono conteggiati gli utenti assorbiti (e nuovi utenti) toohours, giorni, settimane o mesi. analitica di conservazione utente Hello si basa su coorti. Una coorte nel programma è stato impostato hello di tutti gli utenti di nuovo hello rilevato per un periodo specifico (ad esempio, set hello di utenti che eseguono la prima sessione durante questo periodo). Vengono utilizzate coorti di 1 giorno, 2 giorni, 4 giorni, 7 giorni o 1 mese. Dato un coorte nel programma, ogni giorno a 1, 2 giorni, 4 giorni, 7 giorni o mesi, 1 Azure Mobile Engagement calcola hello set di tutti gli utenti che appartengono coorte toohello e sono ancora attiva (ad esempio, set hello di utenti che hanno eseguito in almeno una sessione nel periodo di tempo hello). Questo set di utenti viene definito come versione coorte. (Azure Mobile Engagement consente di visualizzare il numero di utenti utilizzano ancora l'app, ma solo negozio di specifico della piattaforma hello può indicare il numero di utenti disinstallato l'iTunes app - GooglePlay, ad esempio,, Windows Store, ecc.).
* Sessioni: Un utilizzo di un'applicazione hello da un utente. Le sessioni vengono generate dalla sequenza di hello delle attività eseguite dagli utenti (un'attività è in genere associati a toohello di utilizzo di una schermata dell'applicazione hello, ma ciò può variare a seconda di hello modo hello SDK è stato integrato nell'applicazione hello). Un utente può eseguire solo un'attività alla volta: come utente di hello inizia la prima attività e si arresta quando avrà terminato la propria attività ultimo avvio di una sessione. Se l'utente non esegue attività per alcuni secondi, la sequenza viene suddivisa in due sessioni distinte.
* Attività: hello periodo di tempo utente e di nomi hello di ogni schermata nell'applicazione impiegano in ogni schermata. Le attività sono un'opzione di analisi personalizzata corrispondenti tag "app info" toohello impostati per la propria app:
* Percorso utente: indica il percorso di navigazione degli utenti tra le attività (schermate) dell'applicazione. È possibile spostare in hello dispositivo di scorrimento tooadjust hello livello di dettagli. I nodi blu rappresentano le attività dell'applicazione. Le dimensioni sono proporzionali toohello tempo trascorso dagli utenti in essa contenuti. I nodi bianchi rappresentano l'inizio e la fine della sessione. I nodi rossi rappresentano gli arresti anomali. I collegamenti rappresentano i passaggi tra attività dell'applicazione (o tra attività e arresti anomali). Fare clic su una descrizione comando contenente altre informazioni sui dati su un nodo o un collegamento di toodisplay: hello tempo impiegato per una particolare schermata, hello conteggio delle transizioni e hello percentuale di transizioni dall'attività di destinazione toohello hello origine attività. (Un---60%---> B indica che gli utenti sull'attività A si tooactivity B il 60% del tempo di hello.) È possibile riorganizzare il grafico hello tooclarify desiderato. ogni volta che si apporta una modifica, la posizione viene salvata. È possibile visualizzare o nascondere hello arresti anomali del sistema toolighten hello grafico.
* Eventi: Azioni specifiche eseguite da un utente in un'applicazione hello. distribuzione di Hello degli eventi viene visualizzata come conteggio hello degli eventi per ogni utente per ogni sessione. Un evento che rappresenta un'azione immediata, ad esempio un clic su un pulsante o hello ricezione di una notifica. (hello significato degli eventi dipende come hello SDK è stato integrato nell'applicazione hello). Un evento può verificarsi durante una sessione o un processo oppure come evento autonomo.
* Processi: Tooevents simili ma vanno concentrarsi sulla lunghezza hello di azione hello. Ad esempio, i processi di stato indicano informazioni tecniche su quanto tempo servirebbe tooload contenuto o un servizio tooweb chiamata. È anche possibile Mostra il tempo impiegato toofill un utente di un modulo, creare un account o effettuare un acquisto. Un processo rappresenta hello durata di un'attività, per esempio, la durata di hello di un'attività di download hello ora un banner viene visualizzato sullo schermo di hello. (hello significato dei processi dipende come hello SDK è stato integrato nell'applicazione hello). I processi sono in genere associati con attività in background che vengono eseguite di fuori ambito hello di una sessione (ad esempio, senza eseguire alcuna attività utente).
* Technicals: Le informazioni tecniche sui dispositivi hello di utenti hello dell'app che è possibile tenere traccia, ad esempio le dimensioni delle impostazioni locali, vettore, rete, dispositivi, Firmware e schermata dei dispositivi degli utenti hello hello e hello versione dell'App e hello versione SDK utilizzata nell'app.
* Errori: Informazioni sugli errori tecnici all'interno di un'applicazione hello che non provocano hello toocrash dell'applicazione. Un errore rappresenta un problema immediato, ad esempio, un errore di rete o una modifica non valida. (hello significato degli eventi dipende come hello SDK è stato integrato nell'applicazione hello). Un errore può verificarsi durante una sessione o un processo oppure come evento autonomo.
* Arresti anomali del sistema: Informazioni sugli errori che causano toocrash l'applicazione. Un arresto anomalo è una condizione imprevista in cui un'applicazione hello non esegue le funzioni previste e deve essere interrotto. Un arresto anomalo del sistema è in genere a causa di tooa bug in un'applicazione hello.

![Analytics2][11]

## <a name="accessing-hello-retention-overview"></a>L'accesso a hello Panoramica di memorizzazione
![Analytics3][12]

Cenni preliminari sulla memorizzazione di Hello è suddivisa in intermedio hello in diverse schede, ogni Panoramica hello di visualizzazione per un determinato periodo di memorizzazione. periodo di memorizzazione di 2 giorni Hello è illustrato nell'esempio di hello. Hello altri 4 giorni schede Mostra hello e periodi di conservazione di 7 giorni.

## <a name="understanding-hello-retention-overview-cards"></a>Informazioni sulle schede Panoramica memorizzazione hello
![Analytics4][13]

### <a name="each-card-is-composed-of-3-main-parts"></a>Ogni scheda comprende tre parti principali:
1. 1: coorte hello e periodo di hello considerati
2. 2-4: hello conservazione per hello periodo corrente
3. 5: un grafico Sparkline della cronologia di hello

### <a name="here-is-detailed-information-about-each-element"></a>Di seguito, sono riportate le informazioni dettagliate su ogni elemento:
1. Coorte e periodo: il titolo fornisce il tipo di hello di coorte nel programma. Di seguito "periodo di 2 giorni" significa che verrà esaminato il comportamento di hello degli utenti oltre 2 giorni, gli utenti che si trova in un periodo di 2 giorni e se si connettono in hello seguenti blocchi di 2 giorni. esempio Hello precedente considera attività hello degli utenti tra hello 21 e 22 di novembre.
2. In questo modo il tasso di conservazione hello su hello 21 e 22 di novembre per gli utenti di hello in arrivo 19 e 20 di novembre. Qui abbiamo 1 utente attivo tra hello 21 e il 22, su hello 3 che sono stati nuovi utenti tra hello 19 e 20.
3. Questo fornisce indicatori visivi hello stesse informazioni di sopra di rappresentare graficamente. (terzo hello di hello cerchio è da numero 33% hello.) colori Hello vengono fornite informazioni aggiuntive: verde indica questo numero sta crescendo dal calcolo precedente hello. Il giallo indica una situazione stabile, mentre il rosso rappresenta una riduzione.
4. Indica i valori hello utilizzati per il calcolo hello.
5. Si tratta di un grafico Sparkline della cronologia di hello del periodo di memorizzazione hello. Consente i valori hello toosee in hello oltre toohave una visione di come è stato migliorato.

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
