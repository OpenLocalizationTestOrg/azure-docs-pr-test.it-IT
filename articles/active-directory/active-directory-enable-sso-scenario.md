---
title: le applicazioni con Azure Active Directory aaaManaging | Documenti Microsoft
description: Questo articolo hello vantaggi l'integrazione di Azure Active Directory locale, cloud e applicazioni SaaS.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 95b96f10-2d5c-4b78-8af8-d3657a24140f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: 0016f8b433e101d8a150bc6d9be3931851578241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-applications-with-azure-active-directory"></a>Gestione di applicazioni con Azure Active Directory
Oltre al flusso di lavoro effettiva hello o il contenuto, le aziende hanno due requisiti di base per tutte le applicazioni:

1. tooincrease produttività, le applicazioni devono utilizzare toodiscover semplice e l'accesso
2. tooenable protezione e governance, organizzazione hello necessita di controllo e controllo su chi può ed effettivamente accede a ogni applicazione

Nel mondo hello delle applicazioni cloud meglio ciò può essere ottenuto utilizzando l'identità toocontrol "*che è consentito toodo cosa*".

Detto con la terminologia IT:

* *Chi* è noto come *identità* -hello gestione di utenti e gruppi
* *Cosa* è noto come *gestione accessi* : hello gestione dell'accesso alle risorse di tooprotected

Entrambi i componenti insieme sono note come *Identity and Access Management (IAM)*, definito da hello [Gartner](http://www.gartner.com/it-glossary/identity-and-access-management-iam) gruppo come "*hello disciplina di sicurezza che consente a destra di hello utenti tooaccess hello destra risorse hello destro volte per motivi di hello*".

OK, qual è il problema di hello? Se le identità e gli accessi *non sono gestiti* in un'unica posizione con una soluzione integrata:

* Gli amministratori di identità hanno tooindividually creare e aggiornare gli account utente in tutte le applicazioni separatamente, un'attività ridondante e richiedere tempo.
* Gli utenti hanno toomemorize più credenziali tooaccess hello le applicazioni che necessarie toowork con. Di conseguenza, gli utenti tendono toowrite verso il basso le password o usare altre soluzioni di gestione di password che introduce altri rischi di protezione dati.
* Le attività ridondanti e tempo riducono hello di utenti e amministratori stanno lavorando attività di business che aumentano a conclusione dell'azienda.

Quali sono i fattori che ostacolano l'adozione di soluzioni di gestione delle identità e degli accessi da parte delle aziende?

* Le soluzioni più tecniche sono basate su piattaforme software che devono toobe distribuito e adattato da ogni organizzazione per le proprie applicazioni.
* L'adozione di applicazioni cloud è spesso così rapida che le organizzazioni IT faticano a stare al passo con l'integrazione con le soluzioni di gestione delle identità e degli accessi esistenti.
* Sicurezza e gli strumenti di monitoraggio richiedono la personalizzazione e integrazione tooachieve completa E2E scenari aggiuntivi.

## <a name="azure-active-directory-integrated-with-applications"></a>Integrazione di Azure Active Directory con le applicazioni
Azure Active Directory è una soluzione IDaaS (Identity as a Service) Microsoft completa che offre i vantaggi seguenti:

* Abilitazione della gestione delle identità e degli accessi come servizio cloud. 
* Gestione centrale dell'accesso, accesso Single Sign-On (SSO) e creazione di report. 
* Supporta la gestione di accesso integrato per [migliaia di applicazioni](https://azure.microsoft.com/marketplace/active-directory/) nella raccolta di applicazione hello, tra cui Salesforce, Google Apps, Box, Concur e più. 

Con Azure Active Directory, tutte le applicazioni pubblicate per i partner e clienti (business o consumer) hanno hello stesse funzionalità di gestione di identità e accessi.<br> In questo modo si toosignificantly ridurre i costi operativi.

Cosa accade se è necessario tooimplement un'applicazione che non è ancora elencata nella raccolta di applicazioni hello? Mentre questo è un po' più tempo rispetto alla configurazione di SSO per le applicazioni dalla raccolta applicazione hello, Azure AD fornisce una procedura guidata che agevola la configurazione di hello.

il valore di Hello di Azure Active Directory è di là "solo" applicazioni cloud. È anche possibile usarlo con applicazioni locali, fornendo accesso remoto sicuro, Con l'accesso remoto sicuro, è possibile eliminare necessità di hello hello per le reti VPN o altre implementazioni di gestione accesso remoto tradizionale.

Fornisce gestione di accesso centrale e single sign-on (SSO) per tutte le applicazioni, Azure AD fornisce soluzioni hello problemi di protezione e la produttività di dati principale toohello.

* Gli utenti possono accedere a più applicazioni con un segno per concedere più tempo tooincome generazione o aziendale le attività di operazioni eseguite.
* Gli amministratori di identità possono gestire l'accesso tooapplications in un'unica posizione.

Hello vantaggio per l'utente hello e per la società è ovvio. Diamo un'occhiata vantaggi hello per un'organizzazione di hello e l'amministratore delle identità.

## <a name="integrated-application-benefits"></a>Vantaggi dell'applicazione integrata
Hello processo SSO prevede due passaggi:

* Autenticazione, il processo di hello di convalidare l'identità dell'utente hello.
* L'autorizzazione, hello decisione tooenable o bloccare l'accesso tooa risorse con i criteri di accesso.

Quando si utilizzano applicazioni toomanage Azure AD e abilitare SSO:

* L'autenticazione viene eseguita (ad esempio AD) locale o account di Azure AD dell'utente hello.
* Autorizzazione esegue hello Azure AD assegnazione e la protezione criterio garantire l'esperienza dell'utente finale coerente e consentendo tooadd assegnazione, percorsi e le condizioni di autenticazione a più fattori in qualsiasi applicazione, indipendentemente dalla relativa capacità interne.

È importante toounderstand che hello autorizzazione hello modo viene applicato nell'applicazione di destinazione hello varia a seconda di come un'applicazione hello è stata integrata con Azure AD.

* **Applicazioni preintegrate dal provider di servizi** : come Office 365 e Azure, si tratta di applicazioni basate su Azure AD e che dipendono da Azure AD per tutte le funzionalità di gestione delle identità e degli accessi. Applicazioni di accesso toothese viene abilitato tramite il rilascio di token e di informazioni di directory.
* **Applicazioni preintegrate da Microsoft e applicazioni personalizzate** : si tratta di applicazioni cloud indipendenti che si basano su una directory dell'applicazione interna e che possono operare indipendentemente da Azure AD. Applicazioni toothese di accesso è abilitata per il rilascio di un account di applicazione specifico credenziale mappata tooan applicazione. A seconda delle funzionalità dell'applicazione hello, credenziali hello possono essere un token di federazione o nome utente e una password per un account che in precedenza è stato eseguito il provisioning in un'applicazione hello.
* **Applicazioni locali** applicazioni pubblicate mediante il proxy di applicazione hello Azure AD principalmente consentendo alle applicazioni locali tooon di accesso. Queste applicazioni si basano su una directory locale centralizzata, ad esempio Windows Server Active Directory. Applicazioni di accesso toothese è abilitato per attivare l'utente finale hello proxy toodeliver hello applicazione toohello contenuto rispettando hello locale sign-on requisito.

Ad esempio, se un utente crea un join tra l'organizzazione, è necessario toocreate un account per utente hello in Azure AD per operazioni hello primario sign-on. Se l'utente richiede l'applicazione tooa gestito di accesso, ad esempio Salesforce, è anche necessario toocreate un account per l'utente in Salesforce e collegarla lavoro SSO toomake di toohello account Azure. Quando l'utente di hello lascia l'organizzazione, è consigliabile toodelete hello account Azure AD e tutti gli account controparte hello archivi IAM delle applicazioni di hello utente hello aveva accesso.

## <a name="access-detection"></a>Rilevamento degli accessi
Nelle aziende moderne i reparti IT spesso non sono a conoscenza di tutte le applicazioni cloud hello in uso. In combinazione con Cloud App Discovery, Azure AD fornisce una soluzione toodetect queste applicazioni.

## <a name="account-management"></a>Account Management
In genere, la gestione di account hello è un processo manuale eseguito da varie applicazioni IT o supportare personali nell'organizzazione hello. Azure AD offre una soluzione di gestione degli account completamente automatizzata per tutte le applicazioni integrate dai provider di servizi e per quelle preintegrate da Microsoft che supportano il provisioning utenti automatizzato o il formato SAML JIT.

## <a name="automated-user-provisioning"></a>Provisioning utenti automatizzato
Alcune applicazioni offrono interfacce di automazione per la creazione e la rimozione (o disattivazione) di account. Se un provider offre un'interfaccia di questo tipo, questa verrà usata da Azure AD. Questo consente di ridurre i costi operativi perché viene eseguita automaticamente le attività amministrative e migliora la protezione di hello del proprio ambiente, poiché riduce il possibilità hello di accesso non autorizzato.

## <a name="access-management"></a>gestione degli accessi
Con Azure AD è possibile gestire l'accesso tooapplications utilizzando singoli o la regola driven assegnazioni. È inoltre possibile delegare l'accesso Gestione toohello chi deve esserne informato in hello organizzazione garantisce hello migliori e una supervisione riduzione onere hello supporto tecnico.

## <a name="on-premises-applications"></a>Applicazioni locali
Hello compilato nel proxy dell'applicazione consente toopublish agli utenti di tooyour applicazioni on-premise risultante sia coerente in accedono esperienza con i vantaggi di applicazione e hello cloud moderne dal monitoraggio di Azure Active Directory, dei rapporti e funzionalità di sicurezza .

## <a name="reporting-and-monitoring"></a>Monitoraggio e creazione di report
Azure AD fornisce funzionalità che consentono di tooknow chi ha accesso tooapplications e quando effettivamente utilizzati li di monitoraggio e reporting preintegrate.

## <a name="related-capabilities"></a>Funzionalità correlate
Azure AD consente di proteggere le applicazioni tramite criteri di accesso granulari e autenticazione a più fattori (MFA) preintegrata. informazioni su Azure MFA, vedere toolearn [Azure MFA](https://azure.microsoft.com/services/multi-factor-authentication/).

## <a name="getting-started"></a>introduttiva
tooget avviato l'integrazione di applicazioni con Azure AD, dare un'occhiata hello [l'integrazione di Azure Active Directory con le applicazioni di Guida introduttiva](active-directory-integrating-applications-getting-started.md).

## <a name="see-also"></a>Vedere anche
[Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)

