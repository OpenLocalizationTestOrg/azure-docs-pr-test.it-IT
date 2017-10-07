---
title: le notifiche aaaConfigure e modelli in Gestione API di Azure di posta elettronica | Documenti Microsoft
description: Informazioni su come le notifiche tooconfigure e modelli in Gestione API di Azure di posta elettronica.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: ee25f26d-4752-433b-af9c-3817db38aed5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: dc23289c25a1641992b73cb955099b3f207b6968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-notifications-and-email-templates-in-azure-api-management"></a>Come le notifiche tooconfigure e modelli in Gestione API di Azure di posta elettronica
Gestione API consente hello tooconfigure notifiche per eventi specifici e i modelli di messaggio di posta elettronica hello tooconfigure che vengono utilizzati toocommunicate con hello amministratori e sviluppatori di un'istanza di gestione API. Questo argomento viene illustrato come le notifiche di tooconfigure per hello eventi disponibili e viene fornita una panoramica della configurazione di modelli di messaggio di posta elettronica hello utilizzati per questi eventi.

## <a name="publisher-notifications"></a>Configurare le notifiche dell'editore
Fare clic su notifiche tooconfigure, **portale di pubblicazione** in hello portale di Azure per il servizio Gestione API. Consente di procedere toohello portale di pubblicazione di gestione API.

![Portale di pubblicazione][api-management-management-console]

> [!NOTE] 
> Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.

Fare clic su **notifiche** da hello **gestione API** menu hello notifiche disponibili hello tooview a sinistra.

![Notifiche dell'editore][api-management-publisher-notifications]

Hello seguente elenco di eventi può essere configurato per le notifiche.

* **Le richieste di sottoscrizione (che richiedono l'approvazione)** : hello destinatari di posta elettronica specificato e gli utenti riceveranno le notifiche di posta elettronica sulle richieste di sottoscrizione per i prodotti di API che richiedono l'approvazione.
* **Le nuove sottoscrizioni** : hello destinatari di posta elettronica specificato e gli utenti riceveranno le notifiche di posta elettronica su nuove sottoscrizioni di API del prodotto.
* **Le richieste dell'applicazione raccolta** : hello destinatari di posta elettronica specificato e gli utenti riceveranno le notifiche di posta elettronica quando la raccolta di applicazioni toohello inviato nuove applicazioni.
* **Ccn** : hello destinatari di posta elettronica specificato e gli utenti riceveranno tramite posta elettronica in copia per conoscenza nascosta toodevelopers di tutti i messaggi di posta elettronica inviati.
* **Nuovo problema o un commento** : hello destinatari di posta elettronica specificato e gli utenti riceveranno le notifiche di posta elettronica quando un nuovo problema o commento viene presentato il portale per sviluppatori hello.
* **Messaggio Chiudi account** : hello destinatari di posta elettronica specificato e gli utenti riceveranno le notifiche di posta elettronica quando viene chiuso un account.
* **Limite di quota di sottoscrizione vicine** : hello seguenti destinatari di posta elettronica e gli utenti riceveranno le notifiche di posta elettronica quando l'utilizzo della sottoscrizione Ottiene toousage Chiudi quota.

Per ogni evento, è possibile specificare i destinatari di posta elettronica con casella di testo indirizzo di posta elettronica hello oppure è possibile selezionare gli utenti da un elenco.

gli indirizzi e-mail di toospecify hello toobe una notifica, immetterle nella casella di testo Indirizzo posta elettronica hello. Se ci sono più indirizzi di posta elettronica, separarli usando delle virgole.

![Destinatari delle notifiche][api-management-email-addresses]

toospecify hello utenti toobe una notifica, fare clic su **aggiungere destinatario**hello casella accanto a hello utenti toobe una notifica di controllo e fare clic su **OK**.

> [!NOTE] 
> Solo gli amministratori vengono visualizzati nell'elenco di hello.


Dopo aver configurato i destinatari delle notifiche hello, fare clic su **salvare** hello tooapply aggiornata i destinatari delle notifiche.

> [!NOTE] 
> Se si esce dalla hello **le notifiche di server di pubblicazione** portale di pubblicazione hello scheda genera avvisi se vi sono presenti modifiche non salvate.


## <a name="email-templates"> </a>Configurare modelli di posta elettronica
Gestione API fornisce modelli di posta elettronica per hello messaggi di posta elettronica vengono inviati in corso di hello di amministrazione e utilizzo di servizio hello. viene fornito i seguenti modelli di posta elettronica Hello.

* Invio alla raccolta di applicazioni approvato
* Lettera di commiato sviluppatore
* Notifica raggiungimento limite quota sviluppatore
* Invito utente
* Nuovo commento aggiunto tooan problema
* Nuovo problema ricevuto
* Nuova sottoscrizione attivata
* Conferma rinnovo sottoscrizione
* Richiesta sottoscrizione rifiutata
* Richiesta sottoscrizione ricevuta

Questi modelli possono essere modificati a piacimento.

tooview e configurare i modelli di messaggio di posta elettronica hello per l'istanza di gestione API, fare clic su **notifiche** da hello **gestione API** menu hello a sinistra e seleziona hello **modelli di posta elettronica**  scheda.

![Modelli di posta elettronica][api-management-email-templates]

tooview o modificare un modello specifico, selezionarlo hello **modelli** elenco a discesa.

![Elenco modelli di posta elettronica][api-management-email-templates-list]

Ogni modello di posta elettronica ha un oggetto in testo normale e una definizione di corpo in formato HTML. Ogni elemento può essere personalizzato a piacimento.

![Editor dei modelli di posta elettronica][api-management-email-template]

Hello **parametri** elenco contiene un elenco di parametri, che, quando inserite nell'oggetto hello o il corpo, è sostituito hello designato valore quando viene inviato tramite posta elettronica hello. tooinsert un parametro, inserire cursore hello in cui si desidera toogo parametro hello, quindi fare clic su hello freccia toohello sinistra del nome di parametro hello.

Fare clic su **anteprima** o **invio di un test** toosee come messaggio di posta elettronica hello verrà Cerca o inviare un messaggio di test.

> [!NOTE] 
> parametri di Hello non vengono sostituiti con i valori effettivi durante l'anteprima o l'invio di un test.

modello di posta elettronica toohello modifiche hello toosave, fare clic su **salvare**, oppure fare clic su modifiche hello toocancel **Annulla**.
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
