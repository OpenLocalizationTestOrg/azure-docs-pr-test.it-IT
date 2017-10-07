---
title: "codici di errore di attività di aaaSign report nel portale di Azure Active Directory hello | Documenti Microsoft"
description: "Informazioni di riferimento sui codici di errore del report delle attività di accesso."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: a0ca5b706bfeb0c7ce669712468a083a394712b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-report-error-codes-in-hello-azure-active-directory-portal"></a>Codici di errore report attività di accesso nel portale di Azure Active Directory hello

Con informazioni hello fornite dai report di accessi utente hello, trovare risposte tooquestions, ad esempio:

- Chi ha eseguito l'accesso tramite Azure Active Directory?
- A quali app è stato eseguito l'accesso?
- Quali accessi hanno avuto esito negativo e perché?

Questo errore hello elenchi di argomento codici e hello descrizioni correlate. 

## <a name="how-can-i-display-failed-sign-ins"></a>Come è possibile visualizzare gli accessi non riusciti? 

La prima voce tooall punto Accedi attività dati  **[accessi](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/SignIns)**  in hello **attività** sezione **Azure Active**.


![Attività di accesso](./media/active-directory-reporting-activity-sign-ins-errors/61.png "Attività di accesso")


Il report sugli accessi permette di visualizzare gli accessi non riusciti selezionando **Errore** come **Stato accesso**.


![Attività di accesso](./media/active-directory-reporting-activity-sign-ins-errors/06.png "Attività di accesso")

Fare clic su un elemento nell'elenco visualizzato hello, apre hello **dettagli attività: accessi** blade. Questa visualizzazione fornisce tutti i dettagli di hello che tiene traccia di Azure Active Directory su accessi, tra cui hello **codice di errore di accesso** e **motivo dell'errore**.

![Attività di accesso](./media/active-directory-reporting-activity-sign-ins-errors/05.png "Attività di accesso")


In un toousing alternativo hello dati accessi di hello tooaccess portale Azure, è anche possibile utilizzare hello [reporting API](active-directory-reporting-api-getting-started-azure-portal.md).


Hello seguente sezione vengono fornite una panoramica completa di tutti i possibili errori hello e relative descrizioni. 

## <a name="error-codes"></a>Codici di errore

| Errore| Descrizione |
| --- | --- |
| 50001| entità servizio Hello denominato X non è stato trovato nel tenant di hello denominato Y. Questa situazione può verificarsi se un'applicazione hello non è stata installata dall'amministratore di hello del tenant hello. O entità risorsa non è stato trovato nella directory hello o non è valido|
| 50008| Asserzione SAML sono mancanti o non configurato correttamente nel token hello.|
| 50011| indirizzo di risposta Hello è mancante, non configurato correttamente o non corrispondono agli indirizzi di risposta configurati per l'applicazione hello.|
| 50053| Account è bloccato perché l'utente ha tentato toosign in troppe volte con un ID utente non corretto o la password.|
| 50054| Per l'autenticazione è stata usata la password precedente.|
| 50055| È stata immessa una password non valida o scaduta.|
| 50057| L'account utente è disabilitato.|
| 50058| Nessuna informazione sull'identità dell'utente è stata trovata tra fornite credenziali o un utente non è stato trovato nel tenant o una richiesta di accesso invisibile all'utente è stata inviata ma nessun utente è connesso o servizio era in modalità utente non è possibile tooauthenticate hello.|
| 50074| È richiesta l'autenticazione avanzata (secondo fattore).|
| 50079| Utente deve tooenroll per l'autenticazione a due fattori|
| 50126| Sono stati usati un nome utente o una password non validi oppure un nome utente o una password locali non validi.|
| 50131| Usato in diversi errori di accesso condizionale. Dispositivo di Windows non valido ad esempio stato richiesta è bloccata a causa di attività toosuspicious, i criteri di accesso e criteri di sicurezza decisioni.|
| 50133| Sessione non è valida a causa di tooexpiration o modifica della password di recente.|
| 50144| La password di Active Directory dell'utente è scaduta.|
| 65001| X applicazione non dispone di autorizzazione tooaccess applicazione Y o hello autorizzazione è stata revocata. O hello utente o un amministratore ha non acconsentito applicazione hello toouse con ID X. Send una richiesta di autorizzazione interattiva per questo utente e risorse. O utente hello o un amministratore non ha acconsentito un'applicazione hello toouse con ID X. Send un tooact amministratore tenant di autorizzazione richiesta tooyour per conto di hello App: Y per la risorsa: Z.|
| 65005| un'applicazione Hello richiesti elenco accesso alle risorse non contiene applicazioni individuabile risorse hello o un'applicazione hello client ha richiesto l'accesso tooresource che non è stato specificato nel relativo elenco accesso alle risorse necessarie o servizio grafico restituito non valido richiesta o risorsa non trovata.|
| 70001| un'applicazione Hello denominata X non è stata trovata nel tenant di hello denominato Y. Ciò può verificarsi se un'applicazione hello non è stata installata da hello amministratore di tenant hello o tooby consentito qualsiasi utente nel tenant di hello. Potrebbe essere stato inviato il tenant di autenticazione richiesta toohello errato.|
| 80001| Non sono disponibili agenti di autenticazione.|
| 80002| Timeout della richiesta di convalida della password dell'agente di autenticazione.|
| 80003| Risposta non valida ricevuta dall'agente di autenticazione.|
| 80004| È stato usato un nome dell'entità utente (UPN) non corretto nella richiesta di accesso.|
| 80005| Agente di autenticazione: si è verificato un errore.|
| 80007| L'autenticazione dell'agente non è possibile tooconnect tooActive Directory.|
| 80010| Password per l'autenticazione dell'agente non è possibile toodecrypt.|
| 81001| Il ticket Kerberos dell'utente è troppo grande.|
| 81002| Ticket Kerberos non è possibile toovalidate dell'utente.|
| 81003| Ticket Kerberos non è possibile toovalidate dell'utente.|
| 81004| Tentativo di autenticazione Kerberos non riuscito.|
| 81008| Ticket Kerberos non è possibile toovalidate dell'utente.|
| 81009| Ticket Kerberos non è possibile toovalidate dell'utente.|
| 81010| SSO trasparente non riuscita perché il ticket Kerberos dell'utente hello è scaduto o non è valido.|
| 81011| Oggetto utente non è possibile toofind in base alle informazioni nel ticket Kerberos dell'utente hello.|
| 81012| utente Hello tentativo toosign in tooAzure Active Directory è diverso dall'utente hello effettuato l'accesso al dispositivo hello.|
| 81013| Oggetto utente non è possibile toofind in base alle informazioni nel ticket Kerberos dell'utente hello.|
| 90014| Quando un campo previsto non è presente in una credenziale di hello, usato in vari casi.|
| 90093| Grafico restituito con codice di errore non consentito per la richiesta di hello.|



## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni, vedere hello [Accedi rapporti sull'attività nel portale di Azure Active Directory hello](active-directory-reporting-activity-sign-ins.md).

