---
title: reporting di Active Directory aaaAzure | Documenti Microsoft
description: Offre una panoramica generale della creazione di report in Azure Active Directory.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6141a333-38db-478a-927e-526f1e7614f4
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c91813acbdc4b0bfcd164169b0b575accac227d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting"></a>Creazione di report in Azure Active Directory

La creazione di report in Azure Active Directory permette di ottenere informazioni approfondite sullo stato dell'ambiente.  
dati Hello fornito consentono di:

- Determinare l'utilizzo di app e servizi da parte degli utenti
- Rilevare potenziali rischi che pregiudicano hello integrità dell'ambiente
- Risolvere problemi che influiscono negativamente sulla produttività degli utenti  

architettura di reporting Hello si basa su due concetti di base:

- Report sulla sicurezza
- Report sull’attività

![Creazione di report](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a>Report sulla sicurezza

report sulla sicurezza Hello in Azure Active Directory della Guida è tooprotect identità dell'organizzazione.  
Azure Active Directory prevede due tipi di report sulla sicurezza:

- **Utenti contrassegno i rischi** - hello [utenti contrassegno per report di sicurezza di rischio](active-directory-reporting-security-user-at-risk.md), una panoramica degli account utente che sia stato compromesso.

- **Accessi rischiosi** : con hello [rapporto sulla sicurezza rischiosa Accedi](active-directory-reporting-security-risky-sign-ins.md), si ottiene un indicatore per tentativi di accesso che siano stati eseguiti da un utente che non hello legittimo proprietario di un account utente. 

**Licenza Azure AD è necessario tooaccess un report di sicurezza?**  
Tutte le edizioni di Azure Active Directory offrono report sugli utenti contrassegnati per il rischio e sugli accessi a rischio.  
Tuttavia, il livello di hello di granularità dei report varia tra le edizioni di hello: 

- In hello **le edizioni di Azure Active Directory Free e Basic**, già un elenco degli utenti contrassegnati per rischio e accessi rischiosi. 

- Hello **Azure Active Directory Premium 1** edition estende questo modello, consentendo anche tooexamine alcune hello sottostante gli eventi di rischio che sono stati rilevati per ogni report. 

- Hello **Azure Active Directory Premium 2** edition fornisce all'hello più informazioni dettagliate su hello sottostante gli eventi di rischio e consente inoltre di criteri di sicurezza tooconfigure rispondono automaticamente tooconfigured livelli di rischio.


## <a name="activity-reports"></a>Report sull’attività

Azure Active Directory prevede due tipi di report sull'attività:

- **Log di controllo** : hello [report attività i log di controllo](active-directory-reporting-activity-audit-logs.md) fornisce cronologia toohello di accesso di ogni attività eseguita nel tenant.

- **Accessi** : con hello [report attività accessi](active-directory-reporting-activity-sign-ins.md), è possibile determinare chi ha eseguito l'attività hello segnalate dal report di log di controllo hello.



Hello **i report di log di controllo** fornisce per conformità con i record di attività di sistema.
Tra le altre operazioni, hello forniti dati consentono gli scenari comuni di tooaddress, ad esempio:

- Un utente al tenant ottenuto gruppo admin tooan di accesso. si vuole sapere chi ha concesso tale accesso. 

- Si desidera tooknow hello lista di utenti di accedere a un'app specifica dopo I caricate hello app e di recente da tooknow se viene eseguito correttamente

- Voglio tooknow il numero di password Reimposta viene eseguite nel mio tenant


**Licenza Azure AD è necessario tooaccess hello audit log report?**  
report di log di controllo Hello è disponibile per le funzionalità per i quali si dispone di licenze. Se si dispone di una licenza per una funzionalità specifica, è inoltre accesso toohello informazioni del log per il controllo.

Per ulteriori informazioni, vedere **il confronto delle funzionalità disponibili in genere delle edizioni Free, Basic e Premium di hello** in [Azure Active Directory e le funzionalità](https://www.microsoft.com/cloud-platform/azure-active-directory-features).   



Hello **report attività accessi** tootoofind Abilita risponde tooquestions, ad esempio:

- Che cos'è hello sign-in schema di un utente?
- Quanti utenti hanno effettuato l'accesso nell'arco di una settimana?
- Qual è stato hello di tali accessi?


**Licenza Azure AD eseguire tale operazione è necessario tooaccess hello report attività accessi?**  
tooaccess hello report attività accessi, il tenant deve avere una licenza di Azure AD Premium è associata.


## <a name="programmatic-access"></a>Accesso a livello di codice

Nell'interfaccia utente toohello aggiunta reporting di Azure Active Directory offre inoltre funzioni di [l'accesso programmatico](active-directory-reporting-api-getting-started-azure-portal.md) toohello dati di report. dati di Hello di questi report possono essere molto utile tooyour applicazioni, ad esempio i sistemi SIEM, controllo e strumenti di business intelligence. Hello Azure AD reporting che API forniscono dati toohello accesso a livello di codice tramite un set di API basata su REST. È possibile chiamare le API da numerosi linguaggi di programmazione e strumenti. 


## <a name="next-steps"></a>Passaggi successivi

Se si desidera approfondire hello tooknow vari tipi di report in Azure Active Directory, vedere:

- [Report sugli utenti contrassegnati per il rischio](active-directory-reporting-security-user-at-risk.md)
- [Report sugli accessi a rischio](active-directory-reporting-security-risky-sign-ins.md)
- [Report dei log di controllo](active-directory-reporting-activity-audit-logs.md)
- [Report dei log di accesso](active-directory-reporting-activity-sign-ins.md)

Se si desidera tooknow ulteriori informazioni sull'accesso hello hello utilizzando hello API di segnalazione dei dati di report, vedere: 

- [Introduzione a hello reporting API Azure Active Directory](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png