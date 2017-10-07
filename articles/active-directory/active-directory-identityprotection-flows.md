---
title: esperienze di aaaSign con Azure AD Identity Protection | Documenti Microsoft
description: "Fornisce una panoramica di esperienza utente hello quando la protezione dell'identità è risolti o aggiornato un utente o quando è necessario effettuare l'autenticazione di multi-factor un criterio."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestione applicazioni, sicurezza, rischio, livello di rischio, vulnerabilità, criteri di sicurezza"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: de5bf637-75a7-4104-b6d8-03686372a319
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: fbdca5b86ed93d0a2f2b6df1dd0150da9c0c85c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a>Esperienze di accesso con Azure AD Identity Protection
Con Azure Active Directory Identity Protection è possibile:

* Richiedi tooregister utenti multi-factor Authentication
* gestire gli accessi rischiosi e gli utenti compromessi

risposta Hello dei problemi di hello sistema toothese ha impatto sull'esperienza di accesso dell'utente, poiché solo direttamente firma-in, fornendo un nome utente e una password non essere possibile più. Ulteriori passaggi sono necessari tooget un utente in modo sicuro allo stato di business.

Questo argomento presenta una panoramica dell'esperienza di accesso dell'utente per tutti i casi possibili.

**Autenticazione a più fattori**

* Registrazione per l'autenticazione a più fattori

**Accesso a rischio**

* Ripristino di un accesso rischioso
* Accesso rischioso bloccato
* Registrazione per l'autenticazione a più fattori durante un accesso rischioso

**Utente a rischio**

* Ripristino di account compromessi
* Account compromesso bloccato

## <a name="multi-factor-authentication-registration"></a>Registrazione per l'autenticazione a più fattori
Hello un'esperienza utente ottimale sia per, hello flusso di ripristino di un account compromesso hello rischioso flusso di accesso, quando l'utente hello autonomo è possibile ripristinare. Se gli utenti sono registrati per l'autenticazione a più fattori, si dispone già di un numero di telefono associato all'account che possono essere utilizzati toopass problematiche di sicurezza. Alcun modo coinvolta tecnico o l'amministratore della Guida non è necessario toorecover da eventuali compromissioni account. Pertanto, è consigliabile tooget agli utenti registrati per l'autenticazione a più fattori. 

Gli amministratori possono:

* impostare un criterio che richiede tooset agli utenti di account per la verifica aggiuntiva di sicurezza. 
* Consenti registrazione multi-factor authentication per i giorni di too30 ignorata nel caso in cui si desidera che gli utenti toogive prima di registrare un periodo di tolleranza.

**registrazione con l'autenticazione a più fattori Hello prevede tre passaggi:**

1. Nel primo passaggio hello, utente hello Ottiene una notifica sull'account di hello requisito tooset hello per multi-factor authentication. 
   
    ![Correzione](./media/active-directory-identityprotection-flows/140.png "Correzione")
2. autenticazione a più fattori tooset backup, è necessario system hello toolet sapere come si desidera toobe contattato.
   
    ![Correzione](./media/active-directory-identityprotection-flows/141.png "Correzione")
3. sistema Hello invia una richiesta tooyou ed è necessario toorespond.
   
    ![Correzione](./media/active-directory-identityprotection-flows/142.png "Correzione")

## <a name="risky-sign-in-recovery"></a>Ripristino di un accesso rischioso
Quando un amministratore ha configurato un criterio per i rischi di accesso, gli utenti di hello interessato vengono informati quando tentano di toosign-in. 

**flusso Hello rischiosa Accedi prevede due passaggi:** 

1. utente di Hello viene informato che qualcosa di sospetto è stato rilevato sulla loro l'accesso in, ad esempio la firma un nuovo percorso, un dispositivo o app. 
   
    ![Correzione](./media/active-directory-identityprotection-flows/120.png "Correzione")
2. utente Hello è obbligatorio tooprove la propria identità risolvendo un problema di sicurezza. Se l'utente hello è registrato per l'autenticazione a più fattori devono tooround-trip un numero di telefono tootheir codice di sicurezza. Poiché si tratta di un solo di un accesso rischioso e non un account compromesso, utente hello avrà password hello toochange in questo flusso. 
   
    ![Correzione](./media/active-directory-identityprotection-flows/121.png "Correzione")

## <a name="risky-sign-in-blocked"></a>Accesso rischioso bloccato
Gli amministratori possono anche scegliere tooset un rischio di accesso criteri tooblock di utenti al momento dell'accesso in base al livello di rischio hello. tooget sbloccato, gli utenti finali deve contattare un amministratore o al supporto tecnico o tentano l'accesso da una posizione familiare o dispositivo. Il ripristino automatico tramite l'autenticazione a più fattori non è possibile in questo caso.

![Correzione](./media/active-directory-identityprotection-flows/200.png "Correzione")

## <a name="compromised-account-recovery"></a>Ripristino di account compromessi
Quando è stato configurato un criterio di sicurezza utente dei rischi, gli utenti che soddisfano utente hello corre il rischio livello specificato nei criteri di hello (e pertanto vengono considerati compromessi) devono transitare attraverso hello utente compromissione ripristino flusso prima che essi possono Accedi. 

**flusso di ripristino di Hello utente compromissione include tre passaggi:**

1. Hello utente viene informato che la sicurezza dell'account è a rischio a causa di attività sospette o perdita di credenziali.
   
    ![Correzione](./media/active-directory-identityprotection-flows/101.png "Correzione")
2. utente Hello è obbligatorio tooprove la propria identità risolvendo un problema di sicurezza. Se l'utente hello è registrato per l'autenticazione a più fattori è possibile self-ripristinare vengano compromessi. Sarà necessario tooround-trip un numero di telefono tootheir codice di sicurezza. 
   
   ![Correzione](./media/active-directory-identityprotection-flows/110.png "Correzione")
3. Infine, hello utente è forzato toochange la password poiché qualcun altro abbia avuto accesso tootheir account. 
   Sono incluse per riferimento le screenshot di questa esperienza.
   
   ![Correzione](./media/active-directory-identityprotection-flows/111.png "Correzione")

## <a name="compromised-account-blocked"></a>Account compromesso bloccato
un utente che è stato bloccato da un criterio di sicurezza utente dei rischi sbloccato tooget, hello, l'utente deve contattare un amministratore o il supporto tecnico. Il ripristino automatico tramite l'autenticazione a più fattori non è possibile in questo caso.

![Correzione](./media/active-directory-identityprotection-flows/104.png "Correzione")

## <a name="reset-password"></a>Reimpostazione delle password
Se l’accesso degli utenti compromessi è bloccato, un amministratore può generare una password temporanea per consentire l’accesso. Hello gli utenti avranno toochange la propria password durante un successivo accesso in.

![Correzione](./media/active-directory-identityprotection-flows/160.png "Correzione")

## <a name="see-also"></a>Vedere anche
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md) 

