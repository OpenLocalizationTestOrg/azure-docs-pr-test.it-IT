---
title: "Considerazioni sulla progettazione di aaaAzure Active Directory ibrido identità - determinare i requisiti di autenticazione a più fattori"
description: "Con il controllo di accesso condizionale, Azure Active Directory verifica specifiche condizioni hello selezionate per l'autenticazione utente hello e prima di consentire l'accesso toohello applicazione. Quando queste condizioni sono soddisfatte, l'utente di hello è autenticato e accesso toohello applicazione consentita."
documentationcenter: 
services: active-directory
author: femila
manager: billmath
editor: 
ms.assetid: 9c59fda9-47d0-4c7e-b3e7-3575c29beabe
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 49fa7b43772fb3a2d6664747477c60a34cddde2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a>Determinare i requisiti dell'autenticazione a più fattori per la soluzione di identità ibrida
In questo mondo di mobilità, con utenti che accedono ai dati e applicazioni nel cloud hello e da qualsiasi dispositivo, è diventato fondamentale proteggere queste informazioni.  Ogni giorno viene data notizia di una nuova violazione della sicurezza.  Tuttavia, non c'è garanzia contro tali violazioni della sicurezza, autenticazione a più fattori, offre un ulteriore livello di sicurezza toohelp evitare tali violazioni.
Avviare la valutazione dei requisiti delle organizzazioni hello multi-factor Authentication. Che cos'è toosecure durante il tentativo di hello dell'organizzazione.  Questa valutazione è requisiti tecnici di hello toodefine importanti per la configurazione e consentire agli utenti di organizzazioni hello multi-factor Authentication.

> [!NOTE]
> Se non si ha familiarità con l'autenticazione a più fattori e funzionalità, è consigliabile leggere l'articolo hello [che cos'è Azure multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) precedente toocontinue leggere questa sezione.
> 
> 

Verificare i seguenti hello tooanswer che:

* L'azienda sta tentando toosecure Microsoft App? 
* Come sono state pubblicate queste app?
* La società fornisce accesso remoto tooallow dipendenti tooaccess locale App?

In caso affermativo, il tipo di accesso remoto? È inoltre necessario tooevaluate in cui gli utenti di hello che accedono a tali applicazioni verranno memorizzati. Questa valutazione è un'altra strategia di autenticazione a più fattori corretta hello di toodefine passaggio importante. Verificare che hello tooanswer seguenti domande:

* Dove si trovano toobe utenti hello?
* Potrebbero trovarsi ovunque?
* L'azienda vuole tooestablish restrizioni in base della posizione dell'utente toohello?

Dopo aver appreso questi requisiti, è importante tooalso valutare i requisiti dell'utente hello multi-factor Authentication. Questa valutazione è importante perché definirà i requisiti di hello per l'implementazione di multi-factor authentication. Verificare che hello tooanswer seguenti domande:

* Si ha familiarità con l'autenticazione a più fattori utenti hello?
* Alcuni utilizzi sarà l'autenticazione aggiuntiva tooprovide necessarie?  
  * In caso affermativo, tutti hello tempo, quando provenienti da reti esterne o accesso alle applicazioni specifiche o in altre condizioni?
* Gli utenti di hello dovranno come toosetup e implementare l'autenticazione a più fattori?
* Quali sono gli scenari principali di hello che la società decide tooenable multi-factor authentication per gli utenti?

Dopo aver rispondere alle domande precedenti hello, si sarà in grado di toounderstand se esistono già implementata l'autenticazione a più fattori locale. Questa valutazione è requisiti tecnici di hello toodefine importanti per la configurazione e consentire agli utenti di organizzazioni hello multi-factor Authentication. Verificare che hello tooanswer seguenti domande:

* L'azienda necessita di account con privilegi tooprotect con autenticazione a più fattori?
* L'azienda necessita tooenable autenticazione a più fattori per alcune applicazioni per motivi di conformità?
* L'azienda necessita tooenable autenticazione a più fattori per tutti gli utenti idonei di queste applicazioni o solo gli amministratori?
* È necessario sono sempre abilitati con autenticazione a più fattori o solo quando sono connessi utenti hello all'esterno della rete aziendale?

## <a name="next-steps"></a>Passaggi successivi
[Definire una strategia di adozione della soluzione ibrida di gestione delle identità](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a>Vedere anche
[Panoramica delle considerazioni di progettazione](active-directory-hybrid-identity-design-considerations-overview.md)

