---
title: aaaAzure interfaccia utente di Engagement Mobile - raggiungere criterio
description: Informazioni su come toouse destinazione criteri toosend push campagne tooa selezionare sottoinsieme di utenti con Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: a4ed03a0-55b1-4dd8-b0bd-c475005afb66
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d956add1b7edc1d49451596019c5a4dec098d724
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-targeting-criteria-toosend-push-campaigns-tooa-select-subset-of-your-users"></a>In che modo toouse destinazione criteri toosend push campagne tooa seleziona sottoinsieme di utenti
I destinatari di destinazione in base a criteri specifici con pulsante "Nuovo criterio" hello è uno dei hello più potenti concetti in Azure Mobile Engagement che consente di che inviare rilevanti push delle notifiche che i clienti hello risponderà tooinstead di questi comportamenti tutti gli utenti. È possibile limitare i destinatari in base ai criteri standard e simulare push toodetermine quante persone hanno riceverà una notifica di hello.

**Vedere anche:**

* [Documentazione dell'interfaccia utente - Reach - Nuova campagna di push][Link 27]

## <a name="audience-criteria-can-include"></a>I criteri dei destinatari possono includere:
* * * Technicals: * * è possibile destinare hello in base alle stesse informazioni tecniche è possibile visualizzare hello Analitica e sezioni di monitoraggio. **Vedere anche:**[Documentazione dell'interfaccia utente - Analytics][Link 15], [Documentazione dell'interfaccia utente - Monitor][Link 16]
* **Percorso:** posizione geografica utilizzabili dalle applicazioni che utilizzano "segnalazione della posizione in tempo reale" Geo-Fencing come un tootarget criteri un gruppo di destinatari da hello posizione GPS. Chiamata di "Lazy Area percorso report" inoltre essere tootarget usato un gruppo di destinatari dal percorso di un telefono cellulare hello ("segnalazione della posizione in tempo reale" e "Lazy segnalazione della posizione" deve essere attivato da hello SDK). **Vedere anche:** [Documentazione SDK - iOS - Integrazione][Link 5], [Documentazione SDK - Android - Integrazione][Link 5]
* **Feedback di copertura:** è possibile definire i destinatari sulla base del loro feedback sulle precedenti notifiche di copertura usando il feedback di copertura derivante da annunci, sondaggi e push di dati. In questo modo destinazione toobetter i destinatari quando due o tre raggiunto campagne rispetto a quelle Impossibile hello prima volta. E può essere utilizzato anche toofilter gli utenti che hanno già ricevuto una notifica con contenuto simile, impostando un tooNOT campagna inviato toousers che hanno già ricevuto una campagna specifica precedente. È anche possibile escludere gli utenti inclusi in una campagna specifica ancora attiva in modo che non ricevano nuove notifiche push. **Vedere anche:** [Documentazione dell'interfaccia utente - Reach - Push del contenuto][Link 29]
* **Rilevamento installazione:** è possibile rilevare le informazioni in base alla posizione in cui gli utenti hanno installato l'app. **Vedere anche:** [Documentazione dell'interfaccia utente - Impostazioni][Link 20]
* **Profilo utente:** possibile destinazione in base alle informazioni utente standard e non si può destinazione in base alle informazioni di hello app personalizzata che è stato creato. Ciò include gli utenti attualmente connessi e gli utenti che hanno risposto a domande specifiche, richiesta in app hello stessa anziché semplicemente come hanno risposto campagne tooprevious tooset. Tutte le informazioni sull'app definite per l'app stessa vengono visualizzate nell'elenco.
* Segmenti: è possibile definire i destinatari sulla base dei segmenti creati a seconda del comportamento utente definito da più criteri. Tutti i segmenti definiti per l'app vengono visualizzati nell'elenco. **Vedere anche:**[Documentazione dell'interfaccia utente - Segmenti][Link 18]
* **App Info:** personalizzato App Info tag possono essere creati da un comportamento utente tootrack "Impostazioni". **Vedere anche:** [Documentazione dell'interfaccia utente - Impostazioni][Link 20]

## <a name="example"></a>Esempio:
Se si desidera toopush un annuncio toohello solo sottoinsieme di utenti che hanno eseguito una in-app acquistare azione.

1. Vai a pagina di impostazioni applicazione tooyour, selezionare il menu di "info App" hello e selezionare "Nuova app info"
2. Registrare nuove informazioni booleane sull'app definite "inAppPurchase"
3. Rendere l'applicazione impostare informazioni sull'app troppo "true" quando l'utente di hello esegue correttamente un acquisto in-app (tramite hello sendAppInfo ("inAppPurchase",...) funzione)
4. Se non si desidera toodo questo dall'applicazione, è possibile farlo dal back-end utilizzando l'API dispositivo hello)
5. Quindi, è sufficiente toocreate annuncio, con un criterio di limitazione toousers il gruppo di destinatari con "inAppPurchase" set troppo "true")

> [!NOTE]
> Destinazione in base ai criteri diversi da tag info app richiede informazioni toogather Azure Mobile Engagement dai dispositivi degli utenti prima di push hello viene inviato e pertanto può provocare un ritardo. Anche le opzioni di configurazione push complesse (ad esempio l'aggiornamento dei badge) possono determinare ritardi dei push. Utilizzo di una campagna "un unico passaggio" da hello API Push è hello assoluto metodo più veloce push in Azure Mobile Engagement. Utilizzare solo il tag di info app come criteri di push per una campagna di copertura (sia dall'API Reach hello o hello dell'interfaccia utente) è metodo più veloce Avanti hello poiché tag info app vengono archiviate sul lato server hello. Utilizzando altri criteri di destinazione per una campagna push è hello più flessibile, ma più lente push (metodo), poiché Azure Mobile Engagement ha dispositivi hello tooquery campagna hello toosend di ordine.

![Reach-Criterion1][29] 

## <a name="criterion-options-apply-to"></a>Le opzioni dei criteri si applicano a:
* **Informazioni tecniche**     
* Nome firmware: nome del firmware
* Versione firmware: versione del firmware
* Modello dispositivo: modello del dispositivo
* Produttore dispositivo: produttore del dispositivo
* Versione applicazione: versione dell'applicazione
* Nome operatore: nome dell'operatore, non definito
* Paese operatore: paese dell'operatore, non definito
* Tipo di rete: tipo di rete
* Impostazioni locali: impostazioni locali
* Dimensioni schermo: dimensioni dello schermo
* **Posizione**      
* Ultima area nota: paese, regione, località
* Geo-fencing in tempo reale: elenco di punti di interesse (nome, azioni), POI circolare (nome, latitudine, longitudine, raggio in metri)
* **Feedback di copertura**     
* Feedback annuncio: annuncio, feedback
* Feedback sondaggio: sondaggio, feedback
* Feedback risposta al sondaggio: feedback di risposta al sondaggio, domanda, opzione
* Feedback push di dati: push di dati, feedback
* **Rilevamento installazione**     
* Archivio: archivio, non definito
* Origine: origine, non definita
* **Profilo utente**     
* Sesso: maschio o femmina, non definito
* Data di nascita: operatore, data, non definita
* Consenso: true o false, non definito
* **Informazioni sulle app**      
* Stringa: stringa, non definita
* Data: operatore, data, non definita
* Numero intero: operatore, numero, non definito
* Booleano: true o false, non definito
* **Segmento**    
* Nome di segmenti (dall'elenco a discesa), esclusione (utenti di destinazione che non fanno parte del segmento).

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

