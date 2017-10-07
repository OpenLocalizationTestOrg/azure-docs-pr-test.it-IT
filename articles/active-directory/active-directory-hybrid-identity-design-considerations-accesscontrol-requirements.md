---
title: "Considerazioni sulla progettazione di aaaAzure Active Directory ibrido identità - determinare i requisiti di controllo di accesso | Documenti Microsoft"
description: "Include informazioni su hello punti chiave di identità e l'identificazione di requisiti di accesso per le risorse per gli utenti in un ambiente ibrido."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e3b3b984-0d15-4654-93be-a396324b9f5e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: f0c22629f732a4c13ee7a24456651bec7637c387
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="determine-access-control-requirements-for-your-hybrid-identity-solution"></a>Determinare i requisiti di controllo di accesso per una soluzione di identità ibrida
Durante la progettazione di un'organizzazione la soluzione con identità ibrida tooreview questa opportunità può anche usare i requisiti per le risorse di hello che stanno pianificando toomake di accesso disponibile per gli utenti. accesso ai dati Hello tra tutti i quattro punti chiave di identità, che sono:

* Amministrazione
* Autenticazione
* Authorization
* Controllo

sezioni di Hello che segue illustra l'autenticazione e autorizzazione in ulteriori dettagli, amministrazione e il controllo fanno parte del ciclo di vita identità ibrida hello. Per altre informazioni su queste funzionalità, leggere l'articolo sulle modalità per [determinare le attività di gestione delle identità ibride](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) .

> [!NOTE]
> Lettura [hello quattro punti chiave di identità, gestione delle identità hello età dell'IT ibrido](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) per ulteriori informazioni su ognuno di tali colonne.
> 
> 

## <a name="authentication-and-authorization"></a>Autenticazione e autorizzazione
Esistono diversi scenari di autenticazione e autorizzazione, questi scenari avrà requisiti specifici che devono essere soddisfatti da una soluzione con identità ibrida hello che società hello è tooadopt continua. Scenari che implicano tooBusiness Business (B2B) comunicazione aggiungere una richiesta aggiuntiva per gli amministratori IT poiché sarà necessario tooensure in metodo di autenticazione e autorizzazione di hello utilizzato dall'organizzazione hello grado di comunicare con i partner commerciali. Durante la progettazione di processo per i requisiti di autenticazione e autorizzazione di hello, verificare che hello domande seguenti sono disponibili:

* L'azienda intende autenticare e autorizzare solo gli utenti presenti nel proprio sistema di gestione delle identità?
  * È già stato definito un piano per gli scenari B2B?
  * In caso affermativo, è già possibile sapere quali protocolli (SAML, OAuth, Kerberos, token o i certificati) verranno essere tooconnect utilizzate entrambe le aziende?
* Soluzione con identità ibrida hello che si sta tooadopt supporta i protocolli?

Un altro tooconsider punto importante è in cui verranno collocati i repository di autenticazione hello che verranno utilizzati da utenti e partner e hello modello amministrativo toobe utilizzato. Prendere in considerazione hello le due opzioni principali seguenti:

* Centralizzata: in hello questo modello le credenziali dell'utente, criteri e l'amministrazione può essere centralizzata locale o nel cloud hello.
* Ibrida: in hello questo modello le credenziali dell'utente, criteri e amministrazione sarà centralizzata in locale e una replica nel cloud hello.

Il modello di cui l'organizzazione adotteranno variano secondo i requisiti aziendali tootheir, si desidera hello tooanswer seguente domande tooidentify sistema di gestione di identità hello in cui risiederà e hello toouse modalità amministrativa:

* L'azienda dispone già di un sistema locale per la gestione delle identità?
  * In caso affermativo, si prevede tookeep è?
  * Sono presenti eventuali requisiti di conformità o del regolamento che l'organizzazione deve seguire che stabilisce in cui deve risiedere sistema di gestione di identità hello?
* L'organizzazione utilizza single sign-on per App che si trova in locale o nel cloud hello?
  * In caso affermativo, l'adozione di un modello di identità ibrido hello influisce questo processo?

## <a name="access-control"></a>Controllo dell’accesso
Anche se l'autenticazione e autorizzazione sono dati principali elementi tooenable accesso toocorporate tramite la convalida dell'utente, è anche importante toocontrol hello livello di accesso che questi utenti avranno e livello hello di amministratori di accesso avrà su hello risorse che gestiscono. La soluzione con identità ibrida deve essere in grado di tooprovide accesso granulare tooresources, la delega e controllo di accesso di base al ruolo. Verificare che hello seguente domanda sono disponibili per il controllo di accesso:

* L'azienda ha più di un utente con privilegi elevati toomanage il sistema di identità?
  * Se Sì, ogni utente necessario hello stesso livello di accesso?
* Sarebbe necessario toodelegate accesso toousers toomanage specifiche risorse aziendali?
  * In caso affermativo, con quale frequenza si verifica questa situazione?
* La società dovrebbe toointegrate funzionalità di controllo di accesso tra sedi locali e cloud risorse?
* La società dovrebbe toolimit tooresources di accesso in base alle condizioni toosome?
* La società avrebbe qualsiasi applicazione che deve accedere alle risorse di toosome controllo personalizzato?
  * In caso affermativo, in cui le applicazioni si trovano (locale o nel cloud hello)?
  * In caso affermativo, in cui sono quelle le risorse di destinazione si trova (locale o nel cloud hello)?

> [!NOTE]
> Annotare i tootake che ogni risposta e comprendere motivazioni hello delle risposte hello. [Definire la strategia di protezione dati](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) esaminerà le opzioni di hello disponibili e i vantaggi e svantaggi di ogni opzione.  Rispondendo a queste domande sarà più facile scegliere l'opzione migliore in base alle specifiche esigenze aziendali.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
[Determinare i requisiti di risposta agli eventi imprevisti](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="see-also"></a>Vedere anche
[Panoramica delle considerazioni di progettazione](active-directory-hybrid-identity-design-considerations-overview.md)

