---
title: "Glossario di protezione di Active Directory identità aaaAzure | Documenti Microsoft"
description: Glossario di Azure Active Directory Identity Protection
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestione applicazioni, sicurezza, rischio, livello di rischio, vulnerabilità, criteri di sicurezza, glossario"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 833119a5-33d6-4482-adda-fa35218c72c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ff2e96d20e2a3f1df24b78e66be5a0c6807e60a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-glossary"></a>Glossario di Azure Active Directory Identity Protection
### <a name="at-risk-user"></a>A rischio (utente)
Utente con uno o più eventi di rischio attivi. 

### <a name="atypical-sign-in-location"></a>Posizione di accesso atipica
Un accesso aggiuntivo da una posizione geografica non è comune per utente specifico di hello, simili agli utenti o tenant hello.

### <a name="azure-ad-identity-protection"></a>Azure AD Identity Protection
Modulo di sicurezza di Azure Active Directory che fornisce una visualizzazione consolidata degli eventi di rischio e delle potenziali vulnerabilità che interessano le identità di un'organizzazione.

### <a name="conditional-access"></a>Accesso condizionale
Un criterio per la protezione di accesso tooresources. Regole di accesso condizionale vengono archiviate in Azure Active Directory hello e vengono valutate da Azure AD prima di concedere l'accesso toohello risorse.  Queste regole possono includere la limitazione dell'accesso in base alla posizione dell'utente, all'integrità del dispositivo o al metodo di autenticazione dell'utente.

### <a name="credentials"></a>Credenziali
Informazioni che includono l'identificazione e la prova dell'identificazione di risorse di rete e toolocal di accesso utilizzato toogain. Tra le credenziali sono inclusi nomi utente e password, smart card e certificati.

### <a name="event"></a>Evento
Record di un'attività in Azure Active Directory.

### <a name="false-positive-risk-event"></a>Falso positivo (evento di rischio)
Stato evento di rischio impostato manualmente da un utente di protezione dell'identità, che indica che l'evento rischio hello è stato esaminato ed è stata contrassegnata erroneamente come un evento di rischio.

### <a name="identity"></a>Identità
Persona o entità che deve essere verificata tramite autenticazione, in base a criteri quali password o certificato.

### <a name="identity-risk-event"></a>Evento di rischio di identità
Evento di AAD che è stato contrassegnato come anomalo da Identity Protection e che può indicare che un'identità è stata compromessa.

### <a name="ignored-risk-event"></a>Ignorato (evento di rischio)
Stato evento di rischio impostato manualmente da un utente di protezione dell'identità, che indica che l'evento rischio hello viene chiuso senza eseguire un'azione correttiva.

### <a name="impossible-travel-from-atypical-locations"></a>Trasferimento impossibile con posizioni atipiche
Un evento di rischio attivato quando due accessi per hello dello stesso utente vengono rilevati, in cui almeno uno di essi è da un'accesso posizione atipica e ora in cui il tempo di hello tra accessi hello è inferiore al minimo hello richiederebbe toophysically si spostano tra queste percorsi.  

### <a name="investigation"></a>Analisi
Hello processo di revisione hello attività, i registri e altre informazioni rilevanti relative tooa rischio evento toodecide se sono necessarie operazioni di correzione o riduzione, conoscere se e come identità hello compromesso e comprendere come hello. è stato usato l'identità compromesso.

### <a name="leaked-credentials"></a>Credenziali perse
Un evento di rischio attivato quando vengono trovate credenziali dell'utente corrente (nome utente e password) pubblicato nel sito web scuro hello dai nostri ricercatori.

### <a name="mitigation"></a>Mitigazione
Toolimit un'azione o eliminare il possibilità hello di un utente malintenzionato tooexploit un'identità compromessa o un dispositivo senza stato di ripristino hello identità o un dispositivo tooa-safe. Una mitigazione non consente di risolvere gli eventi di rischio precedenti associati identità hello o un dispositivo.

### <a name="multi-factor-authentication"></a>Autenticazione a più fattori
Un metodo di autenticazione che richiede due o più metodi di autenticazione, che possono includere un elemento hello utente dispone di, tale certificato; un utente di hello conosce, ad esempio nomi utente, password o passphrase; attributi fisici, ad esempio un'identificazione digitale; e gli attributi personali, ad esempio una firma personale.

### <a name="offline-detection"></a>Rilevamento offline
rilevamento di anomalie e valutazione dei rischi hello di un evento, ad esempio il tentativo di accesso dopo aver fatto hello, per un evento che è già trascorsa Hello.

### <a name="policy-condition"></a>Condizione dei criteri
Una parte di un criterio di sicurezza che definisce le entità hello (gruppi, utenti, le app, le piattaforme per dispositivi, stati del dispositivo, gli intervalli IP, tipi di client) incluso nei criteri hello o esclusa da esso.

### <a name="policy-rule"></a>Regola dei criteri
parte Hello di un criterio di sicurezza che descrive le circostanze hello che attivano criteri hello e azioni di hello quando viene attivato il criterio di hello.

### <a name="prevention"></a>Prevenzione
Un'azione tooprevent danni toohello organizzazione tramite l'uso improprio di un dispositivo o l'identità sospetto o conoscere toobe compromesso. Un'azione di prevenzione non protette dispositivo hello o l'identità e non consente di risolvere gli eventi di rischio precedenti.

### <a name="privileged-user"></a>Con privilegi (utente)
Un utente che in fase di hello di un evento di rischio, ha tooone le autorizzazioni di amministratore permanente o temporanea o di altre risorse in Azure Active Directory, ad esempio un amministratore globale, amministratore fatturazione, amministratore del servizio, amministratore dell'utente e Password Amministratore. 

### <a name="real-time"></a>Tempo reale
Vedere Rilevamento in tempo reale.

### <a name="real-time-detection"></a>Rilevamento in tempo reale
il rilevamento di anomalie Hello e la valutazione del rischio di hello di un evento, ad esempio il tentativo di accesso prima dell'evento hello è consentiti tooproceed.

### <a name="remediated-risk-event"></a>Con correzione (evento di rischio)
Stato evento di rischio impostato automaticamente la protezione dell'identità, che indica che l'evento rischio hello è stato corretto utilizzando l'azione di correzione standard di hello per questo tipo di evento di rischio. Ad esempio, quando si reimposta la password utente hello, molti eventi di rischio che indicano che la password precedente hello compromesso vengono risolti automaticamente.

### <a name="remediation"></a>Correzione
Un'azione toosecure un'identità o un dispositivo che erano in precedenza o sospettato toobe compromesso. Un'azione correttiva Ripristina hello identità o un dispositivo tooa sicuro lo stato e risolve i precedenti eventi di rischio associati all'identità hello o un dispositivo.

### <a name="resolved-risk-event"></a>Risolto (evento di rischio)
Lo stato di un evento rischio impostato manualmente da un utente di protezione dell'identità, che indica che utente hello ha eseguito un'azione di correzione appropriata all'esterno di protezione dell'identità, e che l'evento rischio hello deve essere considerato chiuso.

### <a name="risk-event-status"></a>Stato dell'evento di rischio
Una proprietà di un evento di rischio, che indica se l'evento hello è attivo e chiuso, motivo hello per chiuderla.

### <a name="risk-event-type"></a>Tipo di evento di rischio
Una categoria per hello rischia di evento, che indica il tipo di hello di anomalie che ha causato toobe evento hello considerate rischiose.

### <a name="risk-level-risk-event"></a>Livello di rischio (evento di rischio)
Un'indicazione della gravità hello utenti hello rischio evento toohelp la protezione dell'identità (alta, Media o bassa) di assegnare priorità alle azioni hello hanno organizzazione di tootheir tooreduce hello rischio. 

### <a name="risk-level-sign-in"></a>Livello di rischio (accesso)
Indicazione (alta, Media o bassa) della probabilità hello per uno specifico segno-, in un altro utente sta tentando toouse hello identità utente.

### <a name="risk-level-user-compromise"></a>Livello di rischio (compromissione dell'utente)
Indicazione della probabilità hello che un'identità sia stato compromesso (alta, Media o bassa).

### <a name="risk-level-vulnerability"></a>Livello di rischio (vulnerabilità)
Un'indicazione della gravità hello di utenti di protezione dell'identità toohelp vulnerabilità hello (alta, Media o bassa) di assegnare priorità alle azioni hello hanno organizzazione di tootheir tooreduce hello rischio.

### <a name="secure-identity"></a>Protezione (identità)
Intraprendere l'azione di correzione, ad esempio una modifica della password o macchina ricreazione toorestore uno stato non compromesso tooan identità potenzialmente compromessi.

### <a name="security-policy"></a>Criteri di sicurezza
Raccolta di regole e condizioni per i criteri. I criteri possono essere applicati tooentities, ad esempio utenti, gruppi, App, dispositivi, piattaforme per dispositivi, stati del dispositivo, gli intervalli IP e i tipi di client Auth2.0. Quando un criterio è abilitato, viene valutata ogni volta che un'entità inclusa nei criteri hello viene rilasciata un token per una risorsa.

### <a name="sign-in-v"></a>Accedere (v)
tooauthenticate tooan identità in Azure Active Directory.

### <a name="sign-in-n"></a>Accesso (s)
processo Hello o un'azione di autenticazione di un'identità in Azure Active Directory ed evento hello che acquisisce l'operazione.

### <a name="sign-in-from-anonymous-ip-address"></a>Accesso da indirizzo IP anonimo
Evento di rischio attivato dopo che un accesso da un indirizzo IP è stato identificato come indirizzo IP proxy anonimo.

### <a name="sign-in-from-infected-device"></a>Accesso da dispositivo infetto
Un evento di rischio attivato quando un'Accedi provengono da un indirizzo IP noto toobe utilizzato da uno o più dispositivi compromessi, che sta attivamente toocommunicate con un server bot.

### <a name="sign-in-from-ip-address-with-suspicious-activity"></a>Accesso da indirizzo IP con attività sospetta
Evento di rischio attivato dopo un accesso riuscito da un indirizzo IP con un numero elevato di tentativi di accesso non riusciti tra più account utente in un breve periodo di tempo.

### <a name="sign-in-from-unfamiliar-location"></a>Accesso da posizione non nota
Evento di rischio attivato quando un utente esegue l'accesso da una nuova posizione (indirizzo IP, latitudine/longitudine e numero ASN).

### <a name="sign-in-risk"></a>Rischio di accesso
Vedere Livello di rischio (accesso)

### <a name="sign-in-risk-policy"></a>Criteri di rischio di accesso
Criteri di accesso condizionale che valuta hello rischio tooa specifico Accedi e applica le misure di attenuazione in base alle regole e condizioni predefinite.

### <a name="user-compromise-risk"></a>Rischio di compromissione dell'utente
Vedere Livello di rischio (compromissione dell'utente)

### <a name="user-risk"></a>Rischio utente
Vedere Livello di rischio (compromissione dell'utente)

### <a name="user-risk-policy"></a>Criteri di rischio utente
Criteri di accesso condizionale che considera Accedi hello e applica le misure di attenuazione in base alle regole e condizioni predefinite.

### <a name="users-flagged-for-risk"></a>Utenti contrassegnati per il rischio
Utenti con eventi di rischio attivi o corretti

### <a name="vulnerability"></a>Vulnerabilità
Una configurazione o una condizione in Azure Active Directory in modo hello directory sensibili tooexploits o minacce.

## <a name="see-also"></a>Vedere anche
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)

