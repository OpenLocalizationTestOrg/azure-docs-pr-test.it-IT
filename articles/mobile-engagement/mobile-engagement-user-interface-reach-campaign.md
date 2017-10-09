---
title: aaaAzure interfaccia utente di Engagement Mobile - raggiungere campagna
description: Laern come toocreate e gestire le campagne di notifica push tramite Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2fe124a2-a86f-4136-81ba-a9d298ec798a
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 825e550ace63a34d1a90b10fa976a61eb15a6d04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-push-notification-campaigns"></a>Come toocreate e gestire le campagne di notifica push
È possibile utilizzare hello Reach sezione dell'interfaccia utente di hello toocreate una nuova campagna Push con una formula complessa, fornendo tutte le informazioni di hello è necessario toosend una notifica push. Hello opzioni di una campagna Push variano leggermente a seconda dei tipi di hello quattro campagna: annunci, viene eseguito il polling, inserisce dati e riquadri (solo Windows Phone).

### <a name="option-applies-to"></a>L'opzione si applica a:
* Lingue: tutti (annunci, sondaggi, push di dati e riquadri)
* Campagna: tutti (annunci, sondaggi, push di dati e riquadri)
* Notifica: annunci e sondaggi
* Contenuto: univoco per ogni tipo di campagna
* Destinatari: tutti (annunci, sondaggi, push di dati e riquadri)
* Intervallo di tempo: annunci, sondaggi e riquadri
* Test: tutti (annunci, sondaggi, push di dati e riquadri)

![Reach-Campaign1][20]

## <a name="languages"></a>Lingue
È possibile utilizzare l'elenco a discesa lingue hello menu toosend una versione diversa del toodevices Push impostate toouse diverse lingue. Per impostazione predefinita, tutti i dispositivi riceveranno hello stesso Push indipendentemente dal linguaggio in cui sono impostati toouse. Gli utenti con dispositivi set tooa diversa lingua hello lingua predefinita della riceveranno hello Push. Molte delle opzioni di campagna push hello consentono di contenuto alternativo toospecify per ognuna delle altre lingue hello selezionate. 

![Reach-Campaign2][21]

### <a name="language-differences-apply-to"></a>Le differenze di lingua si applicano a:
* Lingue: Linguaggi univoci possono essere selezionati nella lingua predefinita di addizione toohello
* Campagna: uguale per tutte le lingue
* Notifica: Univoco per ogni lingua inoltre toohello lingua predefinita
* Il contenuto: Univoco per ogni lingua inoltre toohello lingua predefinita
* Destinatari: possono essere filtrati in base a un criterio di lingua distinto
* Intervallo di tempo: uguale per tutte le lingue
* Test: Può essere inviato tooeach lingua alla volta

### <a name="supported-languages"></a>Lingue supportate:
* Arabo (ar) 
* Bulgaro (bg) 
* Catalano (ca) 
* Cinese (zh) 
* Croato (h) 
* Ceco (cs) 
* Danese (da) 
* Olandese (nl) 
* Inglese (en) 
* Finlandese (fi) 
* Francese (fr) 
* Tedesco (de) 
* Greco (el) 
* Ebraico (he) 
* Hindi (hi) 
* Ungherese (hu) 
* Indonesiano (id) 
* Italiano (it) 
* Giapponese (ja) 
* Coreano (ko) 
* Lettone (lv) 
* Lituano (lt) 
* Malese (macrolanguage) (ms) 
* Norvegese Bokmål (nb) 
* Polacco (pl) 
* Portoghese (pt) 
* Romeno (ro) 
* Russo (ru) 
* Serbo (sr) 
* Slovacco (sk) 
* Sloveno (sl) 
* Spagnolo (es) 
* Svedese (sv) 
* Tagalog (tl) 
* Tailandese (th) 
* Turco (tr) 
* Ucraino (Regno Unito) 
* Vietnamita (vi) 

## <a name="campaign"></a>Campagna
È possibile utilizzare hello campagna sezione tooset hello nome e la categoria della campagna anche come se si prevede di sezione di destinatari hello tooignore di una campagna Push e invece di inviare questa campagna tramite l'API Reach hello (e alcuni elementi con livello basso hello API Push). Le categorie possono essere usate con notifiche. nell'applicazione toocontrol un modello di notifica personalizzata in base alle impostazioni predefinite. È possibile ottenere un elenco di "Categorie" esistente tramite l'API Reach hello.

> [!WARNING]
> Se l'opzione hello "Ignora destinatari push verrà inviato toousers tramite API hello" nella sezione "Campagna" hello di una campagna di copertura, campagna hello non invierà automaticamente, sarà necessario toosend manualmente tramite l'API Reach hello.

![Reach-Campaign3][22]

### <a name="option-applies-to"></a>L'opzione si applica a:
* Nome: tutti
* Categoria: annunci e sondaggi
* Ignora i destinatari push verrà inviato toousers tramite API hello: tutti

## <a name="notification"></a>Notifica
È possibile utilizzare le impostazioni di base hello notifica sezione tooset per il push, tra cui: hello titolo di hello Push, il messaggio hello, un'immagine all'interno dell'applicazione, o se è non rilevanti. Molte impostazioni di notifica sono toohello specifico della piattaforma del dispositivo. È possibile scegliere se il push verrà inviato "in-app", "all'esterno dell'app" o in entrambi i modi. (Tenere presente che gli utenti possono "opt-in" o "rifiutare esplicitamente" "fuori app" inserisce nel sistema operativo hello livello nei propri dispositivi e Azure Mobile Engagement non essere in grado di toooverride questa impostazione. Ricordare anche che gestisce l'API Reach hello "nell'app" e "out-of-app" effettua il push. Hello API Push può essere utilizzati toohandle "out dell'app" inserisce troppo). Push possono essere personalizzati con immagini o contenuto HTML, inclusi i collegamenti diretti per il collegamento all'esterno del percorso App o tooanother nell'App (SDK Android 2.1.0 o successive categorie preventivo richieste). È possibile modificare il badge di iOS o di un'icona hello e inviare il contenuto di testo o web (un popup con html, URL collegamento tooanother percorso del contenuto all'interno o all'esterno di hello app). È anche possibile fai squillare i dispositivi Android o vibrare con hello Push. (Tenere presente che sarà necessario hello corrette autorizzazioni SDK in Android tooring file manifesto o vibrare un dispositivo). Non esiste alcuno standard del settore per le dimensioni dell'immagine grande di Android perché le dimensioni dello schermo variano con ogni dispositivo. Tuttavia, le immagini da 400x100 sono adatte a quasi a tutte le dimensioni degli schermi.

### <a name="delivery-types"></a>Tipi di recapito:
* All'esterno dell'app solo: notifica hello verrà recapitata quando l'utente hello non utilizza un'applicazione hello.
* Hello fuori notifica solo app richiede un certificato di Apple o Google (certificato APNS o GCM).
* Nell'applicazione solo: notifica hello viene visualizzata solo quando un'applicazione hello è in esecuzione.
* notifica di Hello utilizza hello Capptain recapito sistema tooreach hello utente. È possibile personalizzare completamente hello layout/visualizzazione il push.
* In qualsiasi momento: Questa opzione assicura che si invia una notifica che o meno, è in esecuzione l'applicazione hello.

![Reach-Campaign4][23]

### <a name="option-applies-to"></a>L'opzione si applica a:
* Notifica: annunci e sondaggi

## <a name="content"></a>Content
È possibile utilizzare contenuto hello di hello sezione contenuto toomodify di annunci, viene eseguito il polling, effettua il push dei dati e riquadri (solo Windows Phone). impostazione del contenuto delle campagne Push Hello è toohello specifico tipo di campagna. 

### <a name="see-also"></a>Vedere anche
* [Documentazione dell'interfaccia utente - Reach - Push del contenuto][Link 29]

![Reach-Campaign5][24]

## <a name="audience"></a>Audience
La campagna o i limiti di una campagna in base ai criteri personalizzati, è possibile utilizzare hello destinatari sezione toodefine un elenco di elementi toolimit standard. set di opzioni tooLimit standard Hello i destinatari consentono agli utenti di nuovo o quello precedente tooeither toopush o solo gli utenti di push nativo. È inoltre possibile impostare un numero di hello toolimit di quota di utenti che ricevono push hello. È possibile modificare manualmente l'espressione hello per la modalità la campagna tooinclude filtrati uno o più utenti tootarget criterio. È possibile digitare manualmente un'espressione di destinatari. Un'espressione di questo tipo deve definire esplicitamente relazione hello tra criteri. Un criterio viene descritto da un identificatore che deve iniziare con una lettera maiuscola e non può contenere spazi. relazione Hello tra criteri hello può essere descritte con 'and', 'or', 'not' gli operatori, nonché '(',')'. Esempio: "Criterion1 or (Criterion1 and not Criterion2)".

> [!NOTE]
> Con numerosi utenti inclusi in campagne, sul lato server hello come destinazione di analisi può richiedere molto tempo, soprattutto se si tenta di toostart più campagne in hello stesso tempo.

* Se possibile, iniziare una sola campagna alla volta.
* In hello massimo inizio solo quattro campagne alla volta.
* Push solo tooyour utenti attivi (casella di controllo "coinvolgere solo gli utenti che possono essere raggiunto tramite Push nativo" e "Coinvolgere solo gli utenti attivi") in modo che solo gli utenti che è ancora installata App hello e utilizzano saranno necessario toobe analizzati.
  Dopo aver definito i destinatari, è possibile utilizzare hello simulare pulsante toofind il numero di utenti che riceveranno questo Push. Questo calcola hello numero di utenti noti potenzialmente destinato al gruppo di destinatari (si tratta di una stima basata su un campione casuale di utenti). Tenere presente che gli utenti che hanno disinstallato l'applicazione hello fanno parte del gruppo di destinatari, ma non possono essere raggiunto.

### <a name="see-also"></a>Vedere anche
* [Documentazione dell'interfaccia utente - Reach - Nuovi criteri di push][Link 28]

![Reach-Campaign6][25]

### <a name="edit-expression"></a>Modifica espressione
![Reach-Campaign7][26]

### <a name="limit-your-audience-option-applies-to"></a>L'opzione Limitare i destinatari si applica a:
* Effettua push solo di un sottoinsieme di utenti: tutti (annunci, sondaggi, push di dati e riquadri)
* Effettua push solo dei vecchi utenti: tutti (annunci, sondaggi, push di dati e riquadri)
* Effettua push solo dei nuovi utenti: tutti (annunci, sondaggi, push di dati e riquadri)
* Effettua push solo degli utenti inattivi: annunci, sondaggi e riquadri
* Effettua push solo degli utenti attivi: tutti (annunci, sondaggi, push di dati e riquadri)
* Effettua push solo degli utenti raggiungibili con Push nativo: annunci e sondaggi

## <a name="time-frame"></a>Intervallo di tempo
È possibile utilizzare hello tempo sezione tooset quando hello push verrà inviato o è possibile lasciare immediatamente campagna hello toostart vuoto di hello intervallo di tempo. Tenere presente che con fuso orario hello degli utenti finali può iniziare campagna hello un giorno prima di quanto si prevede che per gli utenti finali in Asia e invia batch di piccole dimensioni di push contemporaneamente fino a quando tutti i fusi orari hello world corrispondenza hello intervallo di tempo impostato per la campagna. Con fuso orario hello degli utenti finali possono inoltre causare ritardi nelle campagne poiché dispone ora di hello toorequest da un telefono hello prima di iniziare il push di hello.

> [!NOTE]
> quando le campagne non hanno data di fine, i push possono essere memorizzati nella cache locale ed essere ancora visualizzati dopo aver completato manualmente la campagna. tooavoid questo comportamento, specifica un'ora di fine per le campagne.

### <a name="see-also"></a>Vedere anche
* [Reach - Procedure - Pianificazione][Link 3] 

![Reach-Campaign8][27]

### <a name="settings-apply-to"></a>Le impostazioni di applicano a:
* Intervallo di tempo: annunci, sondaggi e riquadri

## <a name="test"></a>Test
È possibile utilizzare il dispositivo di un test di push tooyour hello Test sezione toosend prima del salvataggio della campagna hello. Se è stato configurato tutte le lingue per la campagna personalizzate, è possibile testare push hello in ciascuna lingua. È possibile configurare un dispositivo di test da "Account personale".

> [!NOTE]
> Inserisce alcun lato server vengono registrati i dati quando si utilizza il pulsante hello troppo "non test", i dati vengono registrati solo per le campagne push reale.

### <a name="see-also"></a>Vedere anche
* [Documentazione dell'interfaccia utente - Account personale][Link 14]

![Reach-Campaign9][28]

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

