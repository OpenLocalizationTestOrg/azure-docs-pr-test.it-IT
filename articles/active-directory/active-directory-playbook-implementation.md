---
title: Implementazione di Active Directory PoC Playbook aaaAzure | Documenti Microsoft
description: "Esplorare e implementare rapidamente gli scenari di Gestione delle identità e degli accessi"
services: active-directory
keywords: azure active directory, playbook, modello di verifica, PoC
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 4d61f1432d5f1c15cd88fda4824cf1c1de64c712
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-implementation"></a>Playbook di PoC di Azure Active Directory: implementazione

## <a name="foundation---syncing-ad-tooazure-ad"></a>Foundation - sincronizzazione tooAzure AD Active Directory 

Un'identità ibrida è foundation hello per la maggior parte dei clienti aziendali hello che dispongono già di una directory locale. obiettivo Hello è toointentionally ridurre il tempo come di seguito come valore di hello tooshow possibili scenari di identità e accessi effettivo hello. 

| Scenario | Blocchi predefiniti| 
| --- | --- |  
| [Estensione di cloud toohello identità locale](#extending-your-on-premises-identity-to-the-cloud) | [Sincronizzazione directory: sincronizzazione dell'hash delle password](active-directory-playbook-building-blocks.md#directory-synchronization---password-hash-sync-phs---new-installation) <br/>**Nota**: se si dispone già di DirSync/ADSync o di versioni precedenti di Azure AD Connect, questo passaggio è facoltativo. Alcuni scenari in questa guida potrebbero richiedere la versione più recente di Azure AD Connect.  <br/>[Personalizzazione](active-directory-playbook-building-blocks.md#branding) | 
| [Assegnare licenze di Azure AD usando i gruppi](#assigning-azure-ad-licenses-using-groups) | [Licenze basate sui gruppi](active-directory-playbook-building-blocks.md#group-based-licensing) |


### <a name="extending-your-on-premises-identity-toohello-cloud"></a>Estensione di cloud toohello identità locale 

1. Bob è l'amministratore di Active Directory hello Contoso. Davide Ottiene l'identità di tooenable requisito hello come un servizio per un set di utenti. Dopo l'esecuzione della procedura guidata di Azure AD Connect, hello identità hello degli utenti di destinazione disponibili nel cloud hello. 
2. Bob chiede Susie, uno degli utenti di destinazione, hello tooaccess hello Pannello di accesso di Azure Active Directory e verificare che sia possibile autenticare Mary. Susie vedrà una pagina di accesso personalizzata e un pannello di accesso vuoto pronto per l'abilitazione dell'accesso futuro alle applicazioni.

### <a name="assigning-azure-ad-licenses-using-groups"></a>Assegnare le licenze di Azure AD usando i gruppi 

1. Bob è hello amministratore globale di Azure Active Directory e si desidera tooallocate AD Azure licenze tooa set specifico di utenti come parte della distribuzione iniziale di hello di Azure Active Directory.
2. Bob crea un gruppo per hello utenti pilota. 
3. Bob assegna gruppo toohello di hello licenze
4. Susie, uno dei sistemi informativi hello, viene aggiunto il gruppo di sicurezza toohello come parte del proprio funzioni del processo
5. Dopo un po' di tempo Susie dispone di licenza di accesso toohello Azure AD premium. In questo modo sarà più scenari di prova hello in un secondo momento.

## <a name="theme---lots-of-apps-one-identity"></a>Tema: molte app, una sola identità

| Scenario | Blocchi predefiniti| 
| --- | --- |  
| [Integrare applicazioni SaaS: SSO federato](#integrate-saas-applications---federated-sso) | [SaaS: configurazione SSO federato](active-directory-playbook-building-blocks.md#saas-federated-sso-configuration) <br/>[Gruppi: proprietà delegata](active-directory-playbook-building-blocks.md#groups---delegated-ownership) |
| [Integrare applicazioni SaaS: SSO con password](#integrate-saas-applications---password-sso) | [SaaS: configurazione SSO con password](active-directory-playbook-building-blocks.md#saas-password-sso-configuration) |
| [SSO ed eventi del ciclo di vita delle identità](#sso-and-identity-lifecycle-events) | [SaaS e ciclo di vita delle identità](active-directory-playbook-building-blocks.md#saas-and-identity-lifecycle) |
| [Proteggere gli account di accesso tooShared](#secure-access-to-shared-accounts) | [SaaS: configurazione di account condivisi](active-directory-playbook-building-blocks.md#saas-shared-accounts-configuration) |
| [Proteggere le applicazioni di accesso remoto tooOn locale](#secure-remote-access-to-on-premises-applications) | [Configurazione del proxy delle app](active-directory-playbook-building-blocks.md#app-proxy-configuration) |
| [La sincronizzazione LDAP identità tooAzure AD](#synchronize-ldap-identities-to-azure-ad) |  [Configurazione del connettore LDAP generico](active-directory-playbook-building-blocks.md#generic-ldap-connector-configuration) |

### <a name="integrate-saas-applications---federated-sso"></a>Integrare applicazioni SaaS: SSO federato 

1. Bob è hello amministratore globale di Azure AD e riceve una richiesta dal reparto di Marketing hello, accesso tooenable tootheir istanza ServiceNow. Bob trova esercitazione dettagliata hello nella documentazione di Azure AD e segue e delegati hello assegnazione di utenti toohello app tooKevin, head hello del team di Marketing. 
2. Kevin esegue l'accesso come proprietario di hello dei diritti di ServiceNow e assegna Susie toohello app. Kevin nota anche che il profilo di Susie è stato creato automaticamente in ServiceNow.
3. Susie è un information worker reparto Marketing hello. Ha accesso tooazure Active Directory e individua tutte le applicazioni SaaS verrà assegnata tooin myapps portale. Da qui, lei facilmente ottiene accesso tooServiceNow.
4. il reparto di Marketing Hello vuole tooaudit che ha avuto accesso ServiceNow. Bob scarica un report delle attività e lo condivide con Kevin tramite posta elettronica.  

### <a name="sso-and-identity-lifecycle-events"></a>SSO ed eventi del ciclo di vita delle identità

1. Susie accetta un'assenza e dai criteri aziendali hello locale account di Active Directory è disabilitato temporaneo. Susie ora non è possibile accedere AD tooAzure e pertanto non è possibile accedere a ServiceNow. 
2. Susie consente uno spostamento laterale da tooSales di Marketing. Kevin rimuove il suo accesso da ServiceNow. Susie accede myapps ad azure hello e vede non hello riquadro ServiceNow. Dopo 10 minuti Kevin conferma che l'account di Susie è stato disabilitato dalla console di gestione di ServiceNow.

### <a name="integrate-saas-applications---password-sso"></a>Integrare applicazioni SaaS: SSO con password

1. Bob Configura accesso tooAtlassian HipChat. HipChat ha tooSusie di Password SSO integration e concedere l'accesso
2. Susie registra nel portale myapps toohello e visualizza un hello toodownload collegamento estensione browser IE AD Azure, che lei Scarica
3. Facendo clic, vengono richieste le credenziali nome utente e password per HipChat. Si tratta di un'unica operazione e dopo il completamento di questo utente ha accesso tooHipChat
4. Pochi giorni dopo Susie apre il portale App personali e fa clic di nuovo su HipChat. Questa volta ottiene l'accesso in modo trasparente
5. Kevin, proprietario dell'applicazione hello HipChat, desidera tooaudit che ha eseguito l'accesso di un'applicazione hello. Bob scarica un report di controllo e lo condivide con Kevin tramite posta elettronica. 

### <a name="secure-access-tooshared-accounts"></a>Proteggere gli account di accesso tooShared 

1. Bob è l'handle di Twitter toosecure assegnati compiti hello condiviso per i membri del team vendite hello. Giorgio aggiunge Twitter come un'applicazione SSO e viene assegnato il gruppo di sicurezza toohello di hello Team vendite. Sono stati specificati account toohello condiviso delle credenziali di hello e quindi lo fornisce nel sistema hello. 
2. Le credenziali di Twitter di condivisione non è più attendibile a causa di persone toomultiple esserne a conoscenza. Bob Abilita il rollover automatico della password di Twitter hello.
3. Susie, un membro del team di vendita hello, Registra nel portale myapps toohello e visualizza un hello toodownload collegamento estensione browser IE AD Azure. Esegue l'installazione.
4. Facendo clic sull'utente get accedono direttamente tooTwitter. Lei non conosce la password di hello.
5. Vostro giocatore fa anche parte del team di vendita hello. Ha hello stesse funzioni come Susie nei passaggi 3 e 4
6. reparto vendite Hello vuole tooaudit che ha avuto accesso a Twitter. Bob scarica un report delle attività e lo condivide con Kevin tramite posta elettronica. 

### <a name="secure-remote-access-tooon-premises-applications"></a>Proteggere le applicazioni di accesso remoto tooOn locale

1. Bob, hello Azure amministratore globale di Active Directory, è stato ricevuto numerose richieste tooenable dipendenti tooaccess più utile risorse locali, ad esempio applicazione spese hello, mentre si lavora in modalità remota. Segue hello [documentazione del Proxy di applicazione](active-directory-application-proxy-enable.md) tooinstall un connettore e pubblicare le spese di un'applicazione Proxy dell'applicazione. 
2. Bob condividere l'URL esterno spese applicazione hello con Susie, uno dei dipendenti di hello che richiede l'accesso remoto. Anna accede collegamento hello e dopo l'autenticazione in AAD, è in grado di tooaccess hello spese app e continuare toobe produttivi anche con accesso remoto. 
3. Bob continua quindi applicazioni locali aggiuntive toopublish utilizzando hello stesso processo e fornendo accesso toousers in base alle esigenze. Aggiunge l'accesso condizionale e multi-factor authentication per hello applicazioni più sensibili che pubblica, tooensure aggiuntiva di sicurezza.

### <a name="synchronize-ldap-identities-tooazure-ad"></a>La sincronizzazione LDAP identità tooAzure AD

1. L'azienda di Bob ha un'infrastruttura delle identità complessa. La maggior parte degli utenti hello vengono mantenuta all'interno di Windows Server Active Directory servizi di dominio (ADDS). Alcuni utenti vengono gestiti dal sistema HR all'interno di Active Directory Lightweight Directory Services (ADLDS).
2. Bob viene chiesto di abilitare le app tooSaaS di accesso per tutti gli utenti (anche questi non presenti in ADDS).
3. Bob Configura dati connettore LDAP generico toopull ADLDS in Azure AD Connect.
4. Bob crea regole di sincronizzazione per consentire agli utenti LDAP vengono popolati in Metaverse e tooAzure AD
5. Susie, come utente LDAP, accede alla propria app SaaS usando l'identità sincronizzata



> [!IMPORTANT] 
> Si tratta di una configurazione avanzata che richiede una certa conoscenza di FIM o MIM. Se usata in produzione, è consigliabile leggere le domande su questa configurazione in [supporto tecnico Premier](https://support.microsoft.com/premier).



## <a name="theme---increase-your-security"></a>Tema: aumentare la sicurezza 

| Scenario | Blocchi predefiniti| 
| --- | --- |  
| [Proteggere l'accesso all'account amministratore](#secure-administrator-account-access) | [Azure MFA con le chiamate telefoniche](active-directory-playbook-building-blocks.md#azure-multi-factor-authentication-with-phone-calls) |
| [Proteggere l'accesso per le applicazioni](#secure-access-to-applications) | [Accesso condizionale per applicazioni SaaS](active-directory-playbook-building-blocks.md#mfa-conditional-access-for-saas-applications) |
| [Abilitare l'amministrazione JIT](#enable-just-in-time-jit-administration) | [Privileged Identity Management](active-directory-playbook-building-blocks.md#privileged-identity-management-pim) |
| [Proteggere le identità in base al rischio](#protect-identities-based-on-risk) | [Rilevare eventi di rischio](active-directory-playbook-building-blocks.md#discovering-risk-events) <br/>[Distribuire criteri di rischio di accesso](active-directory-playbook-building-blocks.md#deploying-sign-in-risk-policies) |
| [Eseguire l'autenticazione senza password con l'autenticazione basata su certificati](#authenticate-without-passwords-using-certificate-based-authentication) | [Configurare l'autenticazione basata su certificati](active-directory-playbook-building-blocks.md#configuring-certificate-based-authentication)

### <a name="secure-administrator-account-access"></a>Proteggere l'accesso all'account amministratore

1. Bob è hello amministratore globale di Azure Active Directory. Egli ha identificato Stuart come coamministratore del servizio hello. 
2. Bob Configura account di Stuart tooalways richiedono condizioni di sicurezza di autenticazione a più fattori tooimprove hello
3. Stuart accede toohello portale di Azure e notifiche che deve tooregister il login di hello toocontinue numero telefono
4. Gli accessi successivi da Stuart sono ora protetti con multi-Factor Authentication e ora, viene tooverify una telefonata propria identità.

### <a name="secure-access-tooapplications"></a>Accesso sicuro tooapplications

1. Kevin è i proprietari aziendali hello di ServiceNow. società Hello desidera ora toologin tali utenti con autenticazione a più fattori quando accedono alla rete aziendale di hello esterno.
2. Bob, l'amministratore globale di Azure AD, aggiunge un accesso condizionale criteri toohello ServiceNow applicazione tooenable autenticazione a più fattori per l'accesso esterno
3. Susie, l'information worker esegue l'accesso il portale di App e fa clic sul riquadro ServiceNow hello. A Susie viene visualizzata una richiesta di autenticazione MFA.

### <a name="enable-just-in-time-jit-administration"></a>Abilitare l'amministrazione JIT

1. Bob e Stuart sono amministratori globali di Azure AD. Vogliono ruoli di gestione toohello accesso JIT tooenable e anche i record tookeep utilizzo hello di hello con privilegi ruoli.
2. Bob consente PIM nel tenant di Azure AD hello e diventa l'amministratore della sicurezza hello. Modifica se stesso e l'appartenenza al ruolo di amministratore globale di Stuart da tooeligible permanente.
3. Bob e Stuart ora richiedono l'attivazione proprio ruolo tramite hello portale di Azure prima di effettuare una modifica AD tooAzure configurazione. 

### <a name="protect-identities-based-on-risk"></a>Proteggere le identità in base al rischio 

1. Susie, una Information Worker, tenta di eseguire l'accesso da un browser Tor. 
2. Bob controlla i dashboard di hello Azure AD identity protection e visualizza l'account di accesso di Susie da un indirizzo IP anonimo. team di sicurezza Hello vuole toochallenge tali accede agli utenti con autenticazione a più fattori
3. Bob Abilita criteri di Azure AD Identity Protection toochallenge autenticazione a più fattori per gli eventi medio o alto rischio
4. Dopo un po' di tempo Susie accede di nuovo dal browser Tor. Questa fase, verrà visualizzato hello richiesta di autenticazione a più fattori

### <a name="authenticate-without-passwords-using-certificate-based-authentication"></a>Eseguire l'autenticazione senza password con l'autenticazione basata su certificati

1. Bob è l'amministratore globale per l'istituto finanziario, che impedisce l'uso di password come fattore di autenticazione per le proprie applicazioni.
2. Bob abilita e applica l'autenticazione mediante certificato in ADFS e Azure AD
3. Susie durante l'accesso alle applicazioni è richiesto tooauthenticate tramite certificato

## <a name="theme---scale-with-self-service"></a>Tema: scalabilità self-service

| Scenario | Blocchi predefiniti| 
| --- | --- |  
| [Reimpostazione password self-service](#self-service-password-reset) | [Reimpostazione password self-service](active-directory-playbook-building-blocks.md#self-service-password-reset) |
| [Self-Service l'accesso tooApplications](#self-service-access-to-applications) | [Self-Service l'accesso tooApplications](active-directory-playbook-building-blocks.md#self-service-access-to-application-management) |

### <a name="self-service-password-reset"></a>Reimpostazione della password self-service 

1. Bob è hello Azure AD globale admin e consente la gestione delle Password Self Service tooa sottoinsieme di utenti, inclusi Susie. 
2. Susie registra nel portale toomyapps e tooregister un messaggio, vedere le informazioni di sicurezza per gli eventi di reimpostazione della password future.
3. Dopo pochi giorni Susie dimentica la password e la reimposta tramite il portale di Azure AD

### <a name="self-service-access-tooapplications"></a>Self-Service l'accesso tooApplications 

1. Kevin è i proprietari aziendali hello di ServiceNow. Desidera che gli utenti troppo "iscriversi a", su richiesta, anziché aggiungerli tutti contemporaneamente
2. Bob, l'amministratore globale di Azure AD, modifica hello ServiceNow applicazione tooenable richieste self-service
3. Susie, l'information worker esegue l'accesso il portale di App e fa clic su pulsante "Aggiungi altre applicazioni" hello e vedere ServiceNow come uno dei hello consigliato di applicazioni. Che quindi passa portale App toomy indietro e vedere applicazione ServiceNow hello.

[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]