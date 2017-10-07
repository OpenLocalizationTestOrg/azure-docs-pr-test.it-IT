---
title: riferimento tecnico di Active Directory l'accesso condizionale aaaAzure | Documenti Microsoft
description: "Con il controllo di accesso condizionale, Azure Active Directory verifica specifiche condizioni hello selezionate per l'autenticazione utente hello e prima di consentire l'accesso toohello applicazione. Quando queste condizioni sono soddisfatte, l'utente di hello è autenticato e accesso toohello applicazione consentita."
services: active-directory.
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 56a5bade-7dcc-4dcf-8092-a7d4bf5df3c1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ee201405d1d17f130607a95bf455b60cd222dd0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a>Documentazione tecnica sull'accesso condizionale di Azure Active Directory

## <a name="services-enabled-with-conditional-access"></a>Servizi abilitati con l'accesso condizionale

Le regole di accesso condizionale sono supportate in diversi tipi di applicazioni di Azure AD, inclusi i seguenti:


* Applicazioni registrate con hello Proxy dell'applicazione Azure
* App remote di Azure
* Applicazioni line-of-business e multi-tenant sviluppate registrate con Azure AD
* Dynamics CRM
* Alle applicazioni federate dalla raccolta di applicazione hello Azure AD
* Microsoft Office 365 Yammer
* Microsoft Office 365 Exchange Online
* Microsoft Office 365 SharePoint Online (include OneDrive for Business)
* Microsoft Power BI 
* Applicazioni SSO password dalla raccolta applicazione hello Azure AD
* Visual Studio Team Services
* Microsoft Teams









## <a name="enable-access-rules"></a>Abilitare le regole di accesso
Ogni regola può essere abilitata o disabilitata sulla base delle singole applicazioni. Quando le regole sono **ON** verrà abilitate e applicate per gli utenti l'accesso a un'applicazione hello. Quando si trovano **OFF** non verrà utilizzate e non agli utenti di hello impatto firmerà nell'esperienza.

## <a name="applying-rules-toospecific-users"></a>Utenti di applicare regole toospecific
Le regole possono essere applicati toospecific a insiemi di utenti in base a gruppo di sicurezza impostando **applica a**. **Applica a** può essere impostato troppo**tutti gli utenti** o **gruppi**. Quando impostato troppo**tutti gli utenti** regole hello applicherà tooany utente con l'applicazione toohello di accesso. Hello **gruppi** opzione consente di sicurezza specifici e toobe di gruppi di distribuzione selezionato, verranno applicate le regole solo per questi gruppi.

Quando si distribuisce una regola, è comune toofirst applica un set limitato di utenti, che sono membri di gruppi di distribuzione pilota. Una volta regola hello completo può essere applicato troppo**tutti gli utenti**. In questo modo regola hello toobe applicata per tutti gli utenti dell'organizzazione hello.

Selezionare i gruppi possono anche essere esentati dai criteri di utilizzo hello **tranne** opzione. I membri di questi gruppi saranno esentati, anche se appartengono a un gruppo incluso.

## <a name="at-work-networks"></a>Reti di tipo "ufficio"
Le regole di accesso condizionale che utilizzano una rete "al lavoro", si basano su intervalli di indirizzi IP attendibili che sono stati configurati in Azure AD, o l'utilizzo di hello "all'interno della rete aziendale" attestazione da ADFS. Queste regole includono:

* Richiedi autenticazione a più fattori quando non al lavoro
* Blocca l'accesso quando non al lavoro

Opzioni per specificare le reti di tipo "ufficio"

1. Configurare intervalli di indirizzi IP attendibili in hello [pagina di configurazione di multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-whats-next.md). Criteri di accesso condizionale utilizzerà gli intervalli hello configurato in ogni richiesta e token di rilascio tooevaluate le regole di autenticazione. 
2. Configura l'utilizzo di hello all'interno della rete aziendale attestazione, questa opzione può essere utilizzata con le directory federativa, tramite ADFS. toolearn ulteriori informazioni su hello all'interno della rete aziendale attestazioni, vedere [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).


## <a name="rules-based-on-application-sensitivity"></a>Regole basate sulla sensibilità dell'applicazione
Le regole sono configurate per ogni applicazione consentendo toobe di servizi di valore elevato hello protetta senza conseguenze per servizi di accesso tooother. Regole di accesso condizionale possono essere configurate in hello **configura** scheda dell'applicazione hello. 

Le regole attualmente disponibili sono le seguenti:

* **Richiedi autenticazione a più fattori**
  
  * Tutti gli utenti che questo criterio viene applicato toowill essere tooauthenticate richiesto tramite l'autenticazione a più fattori almeno una volta.
* **Richiedi autenticazione a più fattori quando non al lavoro**
  
  * Se viene applicato il criterio, tutti gli utenti sarà richiesto toohave eseguita almeno una volta autenticazione a più fattori se accedono servizio hello da una postazione remota non lavorative. Se si sposta da un percorso di lavoro tooremote, saranno tooperform richiesto l'autenticazione a più fattori quando si accede hello servizio.
* **Blocca l'accesso quando non al lavoro** 
  
  * Quando gli utenti di passare da postazione remota tooa di lavoro, verrà bloccati se il criterio di "Bloccare l'accesso quando non al lavoro" hello è toothem applicato.  Nella posizione in sede, saranno nuovamente autorizzati ad accedere.

## <a name="related-topics"></a>Argomenti correlati
* [Protezione dell'accesso tooOffice 365 e altre App connessa tooAzure Active Directory](active-directory-conditional-access.md)
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)

