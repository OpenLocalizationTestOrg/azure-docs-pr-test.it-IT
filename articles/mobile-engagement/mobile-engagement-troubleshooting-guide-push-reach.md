---
title: aaaAzure Mobile Engagement Troubleshooting Guide - Push/copertura
description: Risoluzione dei problemi relativi all'interazione dell'utente e alle notifiche in Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3f1886b7-1fdd-47f4-b6b0-d79f158d5ef3
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4ee0b34b9b753a98ccf24863acb28a5dc76bfb95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-push-and-reach-issues"></a>Guida alla risoluzione di problemi relativi a notifiche push e Reach
di seguito Hello sono possibili problemi che possono verificarsi con la modalità di invio delle informazioni tooyour gli utenti di Azure Mobile Engagement.

## <a name="push-failures"></a>Errori push
### <a name="issue"></a>Problema
* Le notifiche push non funzionano (in-app, all'esterno dell'app o entrambe).

### <a name="causes"></a>Cause
* Molte volte un errore di push è un'indicazione che Azure Mobile Engagement Reach o un'altra funzionalità avanzata di Azure Mobile Engagement non correttamente è integrata o che è un aggiornamento obbligatorio hello SDK toofix un problema noto con una nuova piattaforma del sistema operativo o il dispositivo.
* In caso di un problema nell'App o di test solo un push In App e solo un toodetermine push delle App.
* Test di hello dell'interfaccia utente e hello API come una risoluzione dei problemi di passaggio toosee quali informazioni aggiuntive sull'errore sono disponibili entrambe le posizioni.
* All'esterno dell'App push non funzionerà a meno che non sia Azure Mobile Engagement e raggiungere sono integrati in hello SDK.
* Le notifiche push non funzionano se i certificati non sono validi o se usano la versione di produzione piuttosto che di sviluppo in modo corretto (solo per iOS). (**Nota:** "all'esterno dell'app" notifiche push non possono essere consegnate tooiOS, se si dispone di entrambi development hello (DEV) e versioni di produzione (produzione) di un'applicazione installata hello stesso dispositivo perché il token di sicurezza hello associato con il certificato può essere invalidato da Apple. tooresolve questo problema, disinstallare hello sviluppo e produzione versioni dell'applicazione e installare nuovamente hello solo una versione del dispositivo.)
* All'esterno dell'App conteggi push vengono gestiti in modo diverso nelle diverse piattaforme (iOS Mostra meno informazioni di Android se push nativo sono disabilitate in un dispositivo, hello API può fornire più informazioni rispetto hello dell'interfaccia utente in statistiche push).
* Le notifiche push all'esterno dell'app possono essere bloccate dai clienti a livello di sistema operativo (iOS e Android).
* All'esterno dell'App push verrà visualizzato come disabilitato nell'interfaccia utente di Azure Mobile Engagement hello se non è integrate correttamente, ma potrebbe non riuscire automaticamente da hello API.
* Nell'App push non funzionerà a meno che non sia Azure Mobile Engagement e raggiungere sono integrati in hello SDK.
* Push GCM e ADM non funzionerà a meno che non sono integrati Azure Mobile Engagement e server specifici hello in hello SDK (solo Android).
* In App e App push deve essere testati separatamente toodetermine se è un problema di Push o Reach.
* In App push necessario app hello toobe aprire ricevuto.
* Nell'App push sono spesso toobe installazione filtrati in base a un tag di info app opt-in o opt-out.
* Se si utilizza una categoria personalizzata nelle notifiche di copertura toodisplay nell'applicazione, è necessario toofollow hello corretto del ciclo di vita della notifica di hello, altrimenti notifica hello potrebbe non essere cancellata quando utente hello ignorarla.
* Se si avvia una campagna con nessuna data di fine e un dispositivo riceve hello nella notifica dell'app, ma non viene visualizzato ancora, hello utente ancora riceverà hello notifica hello alla successiva che connessione in app hello, anche se si interrompe manualmente la campagna hello.
* Per problemi relativi alle API Push hello, confermare che si vuole toouse hello API Push anziché hello API Reach (dall'API Reach hello viene utilizzato più frequentemente) e che non si confusione hello "payload" e i parametri "notifica".
* Test della campagna push con entrambi un dispositivo connesso tramite Wi-Fi e 3G connessione di rete di hello tooeliminate come possibile origine di problemi.

## <a name="push-testing"></a>Test di elementi push
### <a name="issue"></a>Problema
* Push possono essere inviati tooa dispositivo specifico in base a un ID di periferica.

### <a name="causes"></a>Cause
* Dispositivi di test siano impostati in modo diverso per ogni piattaforma, ma che ha causato un evento nell'app in un dispositivo di test e cercando l'ID dispositivo nel portale di hello dovrebbe funzionare toofind l'ID dispositivo per tutte le piattaforme.
* I dispositivi di test funzionano diversamente con IDFA e IDFV (solo per iOS).

## <a name="push-customization"></a>Personalizzazione di elementi push
### <a name="issue"></a>Problema
* Un elemento push avanzato non funziona (badge, suoneria, vibrazione, immagine e così via).
* Collegamenti da push funzionanti (all'esterno dell'app, app, sito Web tooa, percorso tooa nell'app).
* Mostra le statistiche di push che un push non è stato inviato tooas molte persone come previsto (un numero eccessivo o insufficiente).
* Elementi push duplicati e ricevuti due volte.
* Impossibile registrare il dispositivo di test affinché riceva elementi push di Azure Mobile Engagement (con la propria app di produzione o sviluppo).

### <a name="causes"></a>Cause
* posizione specifica di tooa toolink in app richiede "categorie" (solo Android).
* Completa il collegamento di schemi tooredirect utenti tooan un percorso alternativo dopo la selezione di una notifica push necessario toobe creati in e gestito direttamente dall'applicazione e hello dispositivo del sistema operativo non da Mobile Engagement. (**Nota:** all'esterno dell'app notifiche non è possibile collegare direttamente tooin posizioni app iOS differenza di quanto accade con Android.)
* Server di immagine esterni devono toobe in grado di toouse HTTP "GET" e "HEAD" per immagine grande inserisce toowork (solo Android).
* Nel codice, è possibile disattivare l'agente di Azure Mobile Engagement hello quando tastiera hello viene aperto e il codice attivare nuovamente l'agente di Azure Mobile Engagement hello dopo tastiera hello è stato chiuso in modo che hello tastiera non influisce sull'aspetto hello il notifica (solo iOS).
* Alcuni elementi non funzionano in simulazioni di test, ma solo durante le campagne effettive (badge, suoneria, vibrazione, immagine e così via).
* Nessun lato server vengono registrati i dati quando si utilizza il pulsante hello troppo "test" effettua il push. I dati vengono registrati solo per le campagne reali sugli elementi di push.
* toohelp isolare il problema, risolvere i problemi: test, simulare e una campagna reale, poiché ogni funzionano in modo leggermente diverso.
* Hello periodo di tempo che di "app" e campagne "in qualsiasi momento" sono pianificati toorun può influire numeri recapito poiché una campagna verrà recapitata soltanto toousers presenti "app" durante l'esecuzione della campagna hello (e gli utenti che dispongono di impostazioni dispositivo impostare tooreceive notifiche "all'esterno dell'app").
* differenze di Hello tra come handle di Android e iOS le notifiche di app rende difficile toodirectly confrontare le statistiche sui push tra la versione di Android e iOS hello dell'applicazione. Android fornisce più informazioni di notifica a livello di sistema operativo rispetto a iOS. Android segnala quando una notifica nativa viene ricevuta, selezionata o eliminata nel centro notifiche hello, ma iOS non segnala le informazioni a meno che non si fa clic su notifica hello. 
* Hello principale motivo per cui i numeri "push" sono diversi rispetto a quelle diverso rispetto a "recapitati" numeri per raggiungono le campagne che "in app" e "all'esterno dell'app" le notifiche vengono calcolate in modo diverso. "In"app notifiche vengono gestite da Engagement Mobile, ma "all'esterno dell'app" notifiche vengono gestite dall'area di notifica hello in hello del sistema operativo del dispositivo.

## <a name="push-targeting"></a>Selezione della destinazione di elementi push
### <a name="issue"></a>Problema
* La funzionalità di selezione destinazione incorporata non funziona nel modo previsto.
* La selezione della destinazione per il tag relativo alle informazioni dell'app non funziona nel modo previsto.
* La selezione della destinazione relativa alla georilevazione non funziona come previsto.
* Le opzioni della lingua non funzionano come previsto.

### <a name="causes"></a>Cause
* Assicurarsi che sia stato caricato tag info app tramite l'interfaccia utente di Azure Mobile Engagement hello o l'API.
* Limitazione hello velocità o push quota push a livello di applicazione hello o destinatari hello limitazione a livello di hello campagna possono evitare che un utente riceve un push specifici anche se soddisfano i criteri di destinazione altri. 
* L'impostazione di una "lingua" rappresenta un'operazione differente rispetto alla selezione della destinazione in base al paese o alle impostazioni locali. Si tratta di un'operazione differente anche rispetto alla selezione della destinazione in base alla georilevazione usando la posizione GPS o del telefono.
* il messaggio Hello in "lingua predefinita" hello viene inviato tooany i clienti non sono configurate tooone di specificare la lingua alternativa hello di dispositivo.

## <a name="push-scheduling"></a>Pianificazione di elementi push
### <a name="issue"></a>Problema
* La pianificazione degli elementi push non funziona nel modo previsto (inviati in anticipo o in ritardo).

### <a name="causes"></a>Cause
* Fusi orari possono problemi con la pianificazione, soprattutto quando si utilizza fuso orario hello degli utenti finali.
* Le funzionalità push avanzate possono ritardare l'invio di elementi push.
* Destinazione in base alle impostazioni (anziché App Info tag) possono ritardare phone inserisce poiché Azure Mobile Engagement può includere dati in tempo reale di hello phone toorequest prima di inviare un push.
* Le campagne create senza una data di fine archiviano hello push localmente nel dispositivo hello e visualizzarlo hello successiva apertura app hello anche se la campagna hello manualmente viene terminata.
* Avvio di più di una campagna in hello contemporaneamente può richiedere un tooscan di tempo più lungo della base di utenti (ripetere tooonly inizio una campagna in un momento con un massimo di quattro, inoltre come destinazione solo tooyour utenti attivi in modo che gli utenti precedenti non hanno toobe analizzati).
* Se l'opzione hello "Ignora destinatari push verrà inviato toousers tramite API hello" nella sezione "Campagna" hello di una campagna di copertura, campagna hello non invierà automaticamente, sarà necessario toosend manualmente tramite l'API Reach hello.
* Se si utilizza una categoria personalizzata nelle notifiche di copertura toodisplay nell'applicazione, è necessario toofollow hello corretto del ciclo di vita di una notifica, altrimenti notifica hello potrebbe non essere cancellata quando utente hello ignorarla.

