---
title: domande frequenti di Active Directory aaaAzure | Documenti Microsoft
description: "Azure Active Directory le risposte alle domande relative alla modalità di accesso tooaccess Azure e Azure Active Directory, la gestione delle password e dell'applicazione."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: b8207760-9714-4871-93d5-f9893de31c8f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/16/2017
ms.author: markvi
ms.openlocfilehash: 63c30c4aeda4551bf02c6b968f98cded5a3b2c16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-faq"></a>Domande frequenti su Azure Active Directory
Azure Active Directory (Azure AD) è una soluzione IDaaS (Identity as a Service) completa che si estende a tutti gli aspetti relativi a identità, gestione degli accessi e sicurezza.

Per altre informazioni, vedere [Informazioni su Azure Active Directory](active-directory-whatis.md).


## <a name="access-azure-and-azure-active-directory"></a>Accedere ad Azure e Azure Active Directory
**D: Perché ricevo "non trovata alcuna sottoscrizione" quando si tenta di tooaccess AD Azure nel portale di Azure classico hello?**

**R:** tooaccess hello portale di Azure classico, ogni utente deve avere le autorizzazioni con una sottoscrizione di Azure. Se si dispone di una sottoscrizione a pagamento di Office 365 o Azure AD, andare troppo[http://aka.ms/accessAAD](http://aka.ms/accessAAD) per un passaggio di attivazione unica. In caso contrario, sarà necessario tooactivate gratuito [account Azure](https://azure.microsoft.com/pricing/free-trial/) o una sottoscrizione a pagamento.

Per altre informazioni, vedere:

* [Associare le sottoscrizioni di Azure ad Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)
* [Gestire directory hello per la sottoscrizione di Office 365 in Azure](active-directory-manage-o365-subscription.md)

- - -
**D: qual è la relazione hello tra AD Azure, Office 365 e Azure?**

**R:** Azure AD fornisce funzionalità comuni di identità e accessi tooall i servizi web. Se si utilizza Office 365, Microsoft Azure, Intune, o altri utenti, si sta già usando Azure AD toohelp attivare la gestione sign-on e l'accesso per tutti questi servizi.

Tutti gli utenti vengono impostati i servizi web toouse sono definiti come account utente in una o più istanze di Azure AD. È possibile configurare questi account per funzionalità di Azure AD gratuite come l'accesso alle applicazioni cloud.

I servizi a pagamento di Azure AD, ad esempio Enterprise Mobility + Security, sono complementari ad altri servizi Web come Office 365 e Microsoft Azure, con soluzioni di gestione e di sicurezza complete di scala aziendale.
- - -
**D: perché è possibile accedere toohello portale di Azure ma non hello portale di Azure classico?**

**R:** hello portale di Azure non richiede una sottoscrizione valida e portale classico hello richiede una sottoscrizione valida.  Se non si dispone di una sottoscrizione, è possibile accedere nel portale classico toohello.
- - -
**D: quali sono le differenze di hello tra l'amministratore della sottoscrizione e l'amministratore di Directory?**

**R:** per impostazione predefinita, è assegnato il ruolo di amministratore della sottoscrizione hello quando effettua l'iscrizione per Azure. Un amministratore della sottoscrizione è possibile utilizzare un account Microsoft o un lavoro o scuola account dalla directory hello che hello sottoscrizione di Azure è associato.  Questo ruolo è servizi autorizzati toomanage hello portale di Azure.

Se altri necessario toosign in e accedere ai servizi da utilizzando hello stessa sottoscrizione, è possibile aggiungerli come coamministratori. Questo ruolo hello dispone di privilegi di accesso come servizio salve, ma non è possibile modificare l'associazione di hello delle directory tooAzure sottoscrizioni.  Per ulteriori informazioni su amministratori della sottoscrizione, vedere [come tooadd o modificare i ruoli di amministratore di Azure](../billing-add-change-azure-subscription-administrator.md) e [delle sottoscrizioni Azure sono associate con Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).


Azure AD include un set diverso di amministrazione ruoli toomanage hello directory e le funzionalità relative alle identità.  Questi amministratori saranno le funzionalità di accesso toovarious nel portale di Azure hello o hello portale di Azure classico. ruolo dell'amministratore di Hello determina le operazioni consentite, come creare o modificare gli utenti, assegnare ruoli amministrativi tooothers, reimpostare le password utente, gestire le licenze utente o gestire i domini.  Per altre informazioni sugli amministratori della directory di AD e i loro ruoli, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles.md).

I servizi a pagamento di Azure AD, ad esempio Enterprise Mobility + Security, sono complementari ad altri servizi Web come Office 365 e Microsoft Azure, con soluzioni di gestione e di sicurezza complete di scala aziendale.

- - -
**D: è disponibile un report che indica la scadenza delle licenze utente di Azure AD?**

**R:** No.  Non è attualmente disponibile.

- - -

## <a name="get-started-with-hybrid-azure-ad"></a>Introduzione alla gestione ibrida di Azure AD


**D: Come si abbandona un tenant quando si viene aggiunti come collaboratore?**

**R:** quando vengono aggiunti tenant dell'organizzazione tooanother come un collaboratore, è possibile utilizzare hello "tenant selezione" in tooswitch destra superiore hello tra tenant.  Attualmente, non vi è alcun hello di tooleave modo si invitano organizzazione e Microsoft sta lavorando tale funzionalità.  Fino a quando questa funzionalità è disponibile, è possibile chiedere hello si invitano tooremove organizzazione dal tenant.
- - -
**D: come è possibile collegare il tooAzure di directory Active Directory locale?**

**R:** è possibile connettersi il tooAzure di directory Active Directory locale con Azure AD Connect.

Per altre informazioni, vedere [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).

- - -
**D: Come si configura l'accesso Single Sign-On tra la directory locale e le applicazioni cloud?**

**R:** è solo necessario tooset di single sign-on (SSO) tra la directory locale e Azure AD. Purché si accedere alle applicazioni cloud tramite Azure AD, servizio hello unità automaticamente gli utenti toocorrectly l'autenticazione con le credenziali locali.

L'implementazione dell'accesso Single Sign-On dall'ambiente locale può essere ottenuta facilmente con soluzioni di federazione come Active Directory Federation Services (AD FS) o con la configurazione della sincronizzazione dell'hash delle password. È possibile distribuire facilmente entrambe le opzioni utilizzando Configurazione guidata di hello Azure AD Connect.

Per altre informazioni, vedere [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).

- - -
**D: Azure AD offre un portale self-service per gli utenti dell'organizzazione?**

**R:** Sì, Azure AD fornisce hello [Pannello di accesso AD Azure](http://myapps.microsoft.com) per l'accesso alle applicazioni e utente self-service. Nel caso di un cliente di Office 365, sono disponibili numerosi hello stesse funzionalità nel portale di Office 365 hello.

Per ulteriori informazioni, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

- - -
**D: Azure AD semplifica la gestione dell'infrastruttura locale?**

**R:** Sì. edizione di Azure AD Premium Hello fornisce con Azure AD Connect Health. Azure AD Connect Health consente di monitorare e approfondire la propria identità locale hello e l'infrastruttura servizi di sincronizzazione.  

Per ulteriori informazioni, vedere [monitorare l'identità dell'infrastruttura e sincronizzazione servizi locali nel cloud hello](active-directory-aadconnect-health.md).  

- - -
## <a name="password-management"></a>Gestione delle password
**D: È possibile usare il writeback delle password di Azure AD senza la sincronizzazione password? (In questo scenario, è possibile toouse Azure AD la reimpostazione della password self-service (SSPR) con password writeback e non archiviare password nel cloud hello?)**

**R:** non è necessario toosynchronize l'Active Directory password tooAzure AD tooenable writeback. In un ambiente federato, Azure AD single sign-on (SSO) si basa su hello locale directory tooauthenticate hello di utenti. Questo scenario non richiede hello locale password toobe registrato in Azure AD.

- - -
**D: come tempo occorre per toobe una password riscritti tooActive Directory in locale?**

**R:** Il writeback delle password viene eseguito in tempo reale.

Per altre informazioni, vedere [Introduzione alla gestione delle password](active-directory-passwords-getting-started.md).

- - -
**D: È possibile usare il writeback delle password con password gestite da un amministratore?**

**R:** Sì, se si dispone di writeback delle password abilitato, le operazioni di password hello eseguite da un amministratore vengono scritte tooyour nell'ambiente locale.  

Per ulteriori domande toopassword, vedere [domande frequenti sulla gestione delle Password](active-directory-passwords-faq.md).
- - -
**D: che cosa può fare se non si ricorda password Office 365 o Azure Active Directory esistente durante il tentativo di toochange password?**

**R:** In situazioni di questo tipo è possibile procedere in due modi.  Usare la reimpostazione password self-service (SSPR), se disponibile.  La disponibilità della funzione SSPR dipende dalla sua configurazione.  Per ulteriori informazioni, vedere [come password hello reimpostare lavoro portale](active-directory-passwords-best-practices.md).

Per gli utenti di Office 365, l'amministratore può reimpostare password hello utilizzando i passaggi descritti nella procedura hello [reimpostare le password utente](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).

Per gli account di Azure AD, gli amministratori possono reimpostare le password utilizzando uno dei seguenti hello:

- [Reimpostare gli account nel portale di Azure hello](active-directory-users-reset-password-azure-portal.md)
- [Reimpostare gli account nel portale classico hello](active-directory-create-users-reset-password.md)
- [Tramite PowerShell](/powershell/module/msonline/set-msoluserpassword?view=azureadps-1.0)


- - -
## <a name="security"></a>Sicurezza
**D: Gli account vengono bloccati dopo un numero specifico di tentativi non riusciti o la strategia usata è più sofisticata?**</br>
Viene usato un account di toolock strategia più sofisticate.  Si basa sulla hello IP della richiesta di hello e password hello immesse. durata Hello del blocco di hello aumenta anche in base alle probabilità hello è costituito da un attacco.  

**D: determinati password (comune) rifiutate con hello messaggi 'questa password è stata utilizzata toomany volte', questo riferimento toopasswords utilizzato in active directory corrente hello?**</br>
Si riferisce toopasswords globale comuni, ad esempio tutte le varianti di "Password" e "123456".

**D: Una richiesta di accesso proveniente da origini sospette (botnet, endpoint tor) sarà bloccata in un tenant B2C o è necessario un tenant della Basic Edition o della Premium Edition?**</br>
Esiste un gateway che filtra le richieste e fornisce un livello di protezione da botnet e che viene applicato per tutti i tenant B2C.

## <a name="application-access"></a>Accesso all'applicazione
**D: Dove si può trovare un elenco di applicazioni preintegrate con Azure AD e delle rispettive funzionalità?**

**D:** Azure AD include più di 2.600 applicazioni preintegrate di Microsoft, application service provider o partner. Tutte le applicazioni preintegrate supportano l'accesso Single Sign-On, SSO consente di utilizzare le credenziali aziendali di tooaccess le app. Alcune applicazioni hello supportano anche automatizzati provisioning e deprovisioning.

Per un elenco completo di applicazioni preintegrate hello, vedere hello [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).

- - -
**D: cosa accade se hello applicazione che è necessario non è in marketplace di Azure AD hello?**

**R:** Azure AD Premium consente di aggiungere e configurare qualsiasi applicazione. In base alle funzionalità dell'applicazione e alle preferenze dell'utente, è possibile configurare l'accesso Single Sign-On e il provisioning automatico.  

Per altre informazioni, vedere:

* [Configurazione di single sign-on tooapplications non presenti nella raccolta di hello Azure Active Directory dell'applicazione](active-directory-saas-custom-apps.md)
* [Utilizzando SCIM tooenable il provisioning automatico degli utenti e gruppi da Azure Active Directory tooapplications](active-directory-scim-provisioning.md)

- - -
**D: come utenti Accedi tooapplications grazie ad Azure AD?**

**R:** Azure AD sono disponibili diversi metodi per gli utenti tooview e accedere alle applicazioni, ad esempio:

* Pannello di accesso Hello Azure AD
* avvio applicazione Hello Office 365
* App toofederated accesso diretto
* Toofederated di collegamenti diretti, basato su password, o le app di esistenti

Per ulteriori informazioni, vedere [integrato di distribuzione di Azure AD applicazioni toousers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).

- - -
**D: quali sono i modi hello Azure AD consente l'autenticazione e single sign-on tooapplications?**

**R:** Azure AD supporta molti protocolli standardizzati per l'autenticazione e l'autorizzazione, ad esempio SAML 2.0, OpenID Connect, OAuth 2.0 e WS-Federation. Azure AD supporta anche funzionalità relative all'insieme di credenziali delle password e all'accesso automatico per le app che supportano solo l'autenticazione basata su form.  

Per altre informazioni, vedere:

* [Scenari di autenticazione per Azure AD](active-directory-authentication-scenarios.md)
* [Protocolli di autenticazione di Active Directory](https://msdn.microsoft.com/library/azure/dn151124.aspx)
* [Come funziona Single Sign-On con Azure Active Directory (PHP)?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)

- - -
**D: È possibile aggiungere applicazioni in esecuzione in locale?**

**R:** Proxy dell'applicazione Azure AD offre un accesso facile e sicuro applicazioni web locali tooon in cui si scelgono. È possibile accedere a queste applicazioni in hello allo stesso modo di accedere il software come un servizio (SaaS) app di Azure AD. Non è necessario per una VPN o toochange l'infrastruttura di rete.  

Per ulteriori informazioni, vedere [come tooprovide proteggere l'accesso remoto applicazioni locali tooon](active-directory-application-proxy-get-started.md).

- - -
**D: Come si richiede l'autenticazione Multi-Factor Authentication per gli utenti che accedono a un'applicazione specifica?**

**R:** L'accesso condizionale di Azure AD consente di assegnare criteri di accesso univoci per ogni applicazione. Nei criteri, è possibile richiedere sempre l'autenticazione a più fattori, oppure quando gli utenti non sono connessi toohello rete locale.  

Per ulteriori informazioni, vedere [protezione dell'accesso tooOffice 365 e altre App connessa tooAzure Active Directory](active-directory-conditional-access.md).

- - -
**D: Che cos'è il provisioning utenti automatizzato per le app SaaS?**

**R:** creazione hello tooautomate usano Azure AD, la manutenzione e la rimozione delle identità utente in molte applicazioni SaaS di cloud più diffusi.

Per ulteriori informazioni, vedere [automatizzare provisioning e deprovisioning tooSaaS applicazioni con Azure Active Directory](active-directory-saas-app-provisioning.md).

- - -
**D: È possibile configurare una connessione LDAP sicura con Azure AD?**

**R:** No. Azure AD non supporta il protocollo LDAP hello.
