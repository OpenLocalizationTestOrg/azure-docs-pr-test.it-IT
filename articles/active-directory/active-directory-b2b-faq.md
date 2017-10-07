---
title: collaborazione B2B di Active Directory FAQ aaaAzure | Documenti Microsoft
description: Ottenere risposte toofrequently domande frequenti su collaborazione B2B di Azure Active Directory.
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 4412bbc65274ff01782db81dfcc8818a6362ea7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-faqs"></a>Domande frequenti su Collaborazione B2B di Azure Active Directory

Le domande frequenti (FAQ) sulla collaborazione business-to-business (B2B) di Azure Active Directory (Azure AD) sono aggiornati periodicamente tooinclude nuovi argomenti.

### <a name="is-azure-ad-b2b-collaboration-available-in-hello-azure-classic-portal"></a>È disponibile nel portale di Azure classico hello collaborazione B2B di Azure AD?
No. Le funzionalità di collaborazione Azure AD B2B sono disponibili solo in hello [portale di Azure](https://portal.azure.com) e hello [Pannello di accesso](https://myapps.microsoft.com/). 

### <a name="can-we-customize-our-sign-in-page-so-it-is-more-intuitive-for-our-b2b-collaboration-guest-users"></a>È possibile personalizzare la pagina di accesso in modo che sia più intuitiva per gli utenti guest di Collaborazione B2B?
Assolutamente sì. Vedere il [post del blog su questa funzionalità](https://blogs.technet.microsoft.com/enterprisemobility/2017/04/07/improving-the-branding-logic-of-azure-ad-login-pages/). Per ulteriori informazioni su come toocustomize dell'organizzazione accesso pagina, vedere [aggiungere personalizzazione toosign nel Pannello di accesso della società](active-directory-add-company-branding.md).

### <a name="can-b2b-collaboration-users-access-sharepoint-online-and-onedrive"></a>Gli utenti di Collaborazione B2B possono accedere a SharePoint Online e a OneDrive?
Sì. È tuttavia hello toosearch di possibilità per gli utenti guest esistenti in SharePoint Online tramite selezione utenti hello **Off** per impostazione predefinita. tooturn su hello opzione toosearch per gli utenti guest esistenti, impostare **ShowPeoplePickerSuggestionsForGuestUsers** troppo**su**. È possibile attivare questa impostazione a livello di tenant hello o a livello di raccolta sito hello. È possibile modificare questa impostazione utilizzando i cmdlet Set-SPOTenant e Set-SPOSite hello. Con questi cmdlet, i membri possono cercare tutti gli utenti guest esistenti nella directory hello. Le modifiche apportate nell'ambito del tenant hello non influiscono sui siti di SharePoint Online sono già stato eseguito il provisioning.

### <a name="is-hello-csv-upload-feature-still-supported"></a>È hello CSV caricare funzionalità ancora supportato?
Sì. Per ulteriori informazioni sull'utilizzo delle funzionalità di caricamento di file con estensione csv hello, vedere [in questo esempio di PowerShell](active-directory-b2b-code-samples.md).

### <a name="how-can-i-customize-my-invitation-emails"></a>Come è possibile personalizzare i messaggi di posta elettronica di invito?
È possibile personalizzare quasi tutte le operazioni sul processo di mittente dell'invito hello utilizzando hello [B2B invito API](active-directory-b2b-api.md).

### <a name="can-an-invited-external-user-leave-hello-organization-after-being-invited"></a>È un utente esterno invitato lasciano l'organizzazione di hello dopo invitati?
amministratore dell'organizzazione invitando Hello è possibile eliminare un utente guest di collaborazione B2B dalla propria directory, ma utente guest hello non può lasciare hello si invitano directory dell'organizzazione da soli. 

### <a name="can-guest-users-reset-their-multi-factor-authentication-method"></a>Gli utenti guest possono reimpostare il metodo di autenticazione a più fattori?
Sì. Gli utenti guest possono reimpostare le hello metodo multi-factor authentication che stesso modo che gli utenti regolari eseguire.

### <a name="which-organization-is-responsible-for-multi-factor-authentication-licenses"></a>Quale organizzazione è responsabile delle licenze dell'autenticazione a più fattori?
organizzazione invitando Hello esegue multi-factor authentication. Hello si invitano organizzazione deve assicurarsi che hello organizzazione numero sufficiente di licenze per i propri utenti B2B che utilizzano l'autenticazione a più fattori.

### <a name="what-if-a-partner-organization-already-has-multi-factor-authentication-set-up-can-we-trust-their-multi-factor-authentication-and-not-use-our-own-multi-factor-authentication"></a>Che cosa accade se un'organizzazione partner ha già configurato l'autenticazione a più fattori? È possibile considerare attendibile l'autenticazione a più fattori già presente e non usare la nuova autenticazione a più fattori?
Questa funzionalità è pianificata per una versione futura, in modo che sarà possibile selezionare tooexclude partner specifici dall'autenticazione a più fattori (hello invitando dell'organizzazione).

### <a name="how-can-i-use-delayed-invitations"></a>Come si usano gli inviti posticipati?
Un'organizzazione potrebbe desidera che gli utenti di collaborazione B2B tooadd, eseguirne il provisioning tooapplications in base alle esigenze e quindi inviare gli inviti. È possibile utilizzare hello B2B collaborazione invito API toocustomize hello caricamento del flusso di lavoro.

### <a name="can-i-make-a-guest-user-a-limited-administrator"></a>È possibile fare in modo che un utente guest diventi amministratore con limitazioni?
Certo. Per ulteriori informazioni, vedere [ruolo tooa utenti guest di aggiungere](active-directory-users-assign-role-azure-portal.md).

### <a name="does-azure-ad-b2b-collaboration-allow-b2b-users-tooaccess-hello-azure-portal"></a>Collaborazione B2B di Azure AD consente B2B utenti tooaccess hello portale di Azure?
A meno che un utente è assegnato il ruolo di hello di amministratore globale o limitato, gli utenti di collaborazione B2B non richiedono accesso toohello portale di Azure. Tuttavia, gli utenti di collaborazione B2B hello ruolo di amministratore globale o limitato accedere portale hello. Inoltre, se un utente guest non è assegnato uno di questi ruoli di amministratore accede portale hello, hello utente potrebbe essere in grado di tooaccess determinate parti di hello esperienza. ruolo di utente guest Hello dispone di alcune autorizzazioni nella directory hello.

### <a name="can-i-block-access-toohello-azure-portal-for-guest-users"></a>È possibile bloccare l'accesso toohello portale per gli utenti guest di Azure?
È possibile usarlo. Quando si configura questo criterio, essere admins e toomembers accesso accidentalmente blocco tooavoid attenzione.
di tooblock un utente guest accedere toohello [portale di Azure](https://portal.azure.com), utilizzare un criterio di accesso condizionale in hello API del modello di distribuzione classica Windows Azure:
1. Modificare hello **tutti gli utenti** in modo che contenga solo i membri di gruppo.
  ![modificare la schermata di gruppo hello](media/active-directory-b2b-faq/modify-all-users-group.png)
2. Creare un gruppo dinamico che contenga utenti guest.
  ![schermata di creazione del gruppo](media/active-directory-b2b-faq/group-with-guest-users.png)
3. Configurare un accesso condizionale criteri tooblock guest agli utenti l'accesso portale hello, come illustrato nell'esempio hello video:
  
  > [!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-block-guest-user/Player] 

### <a name="does-azure-ad-b2b-collaboration-support-multi-factor-authentication-and-consumer-email-accounts"></a>La Collaborazione B2B di Azure AD supporta l'autenticazione a più fattori e gli account di posta elettronica degli utenti?
Sì. Sia l'autenticazione a più fattori che gli account di posta elettronica degli utenti sono supportati per la Collaborazione B2B di Azure AD.

### <a name="do-you-plan-toosupport-password-reset-for-azure-ad-b2b-collaboration-users"></a>Se si prevede di toosupport reimpostazione della password per gli utenti di collaborazione B2B di Azure Active Directory.
Sì. Ecco i dettagli importanti hello per la reimpostazione della password self-service (SSPR) per gli utenti B2B che sono stato richiesto da un'organizzazione partner:
 
* SSPR si verifica solo nei tenant di hello identità dell'utente di hello B2B.
* Se tenant identità hello è un account Microsoft, viene utilizzato l'account Microsoft meccanismo SSPR hello.
* Se il tenant di identità hello è un just-in-time (JIT) o del tenant "virale", viene inviato un messaggio di posta elettronica la reimpostazione della password.
* Per altri tenant, processo SSPR standard hello viene seguito per gli utenti B2B. Come membro SSPR per gli utenti B2B, nel contesto di hello della risorsa hello tenancy è bloccata. 

### <a name="is-password-reset-available-for-guest-users-in-a-just-in-time-jit-or-viral-tenant-who-accepted-invitations-with-a-work-or-school-email-address-but-who-didnt-have-a-pre-existing-azure-ad-account"></a>La reimpostazione della password è disponibile per gli utenti guest in un tenant JIT o "virale" che hanno accettato gli inviti con un indirizzo di posta elettronica aziendale o dell'istituto di istruzione senza avere un account Azure AD preesistente?
Sì. È possibile inviare un messaggio di reimpostazione della password tooreset un utente che consente la propria password in tenancy JIT hello.

### <a name="does-microsoft-dynamics-crm-provide-online-support-for-azure-ad-b2b-collaboration"></a>Microsoft Dynamics CRM offre supporto online per Collaborazione B2B di Azure AD?
Microsoft Dynamics CRM, attualmente, non offre supporto online per Collaborazione B2B di Azure AD. Tuttavia, è previsto il toosupport questo in hello future.

### <a name="what-is-hello-lifetime-of-an-initial-password-for-a-newly-created-b2b-collaboration-user"></a>Che cos'è la durata hello di una password iniziale per un utente di collaborazione B2B appena creata?
Azure AD include un set fisso di tipo carattere, la complessità della password e i requisiti di blocco degli account che si applicano ugualmente tooall account utente del cloud AD Azure. Gli account utente cloud sono account non federati con un altro provider di identità, ad esempio: 
* Account Microsoft
* Facebook
* Active Directory Federation Services
* Un altro tenant cloud (per Collaborazione B2B)

Per gli account federativi, criteri password dipendono dai criteri hello applicati nelle impostazioni dell'account Microsoft hello locale tenancy e hello dell'utente.

### <a name="an-organization-might-want-toohave-different-experiences-in-their-applications-for-tenant-users-and-guest-users-is-there-standard-guidance-for-this-is-hello-presence-of-hello-identity-provider-claim-hello-correct-model-toouse"></a>Un'organizzazione potrebbe essere necessario toohave diverse esperienze nelle proprie applicazioni per utenti del tenant e utenti guest. Ci sono linee guida standard per questo? Presenza di hello di hello identity provider attestazione hello modello corretto toouse
 Un utente guest è possibile utilizzare qualsiasi tooauthenticate di provider di identità. Per altre informazioni, vedere [Proprietà di un utente di Collaborazione B2B](active-directory-b2b-user-properties.md). Hello utilizzare **UserType** esperienza utente toodetermine di proprietà. Hello **UserType** attestazione non è attualmente incluso nel token hello. Le applicazioni devono utilizzare directory hello tooquery di hello API Graph per utente hello e tooget hello UserType.

### <a name="where-can-i-find-a-b2b-collaboration-community-tooshare-solutions-and-toosubmit-ideas"></a>Dove posso trovare un tooshare community di collaborazione B2B soluzioni e idee toosubmit?
Microsoft incoraggia costantemente i feedback tooyour, tooimprove collaborazione B2B. Microsoft invita tooshare è l'utente scenari, le procedure consigliate e aspetti collaborazione B2B di Azure Active Directory. Partecipare a discussioni hello in hello [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).
 
Invita si toosubmit idee e votare le funzionalità future a [idee di collaborazione B2B](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B-Ideas/idb-p/AzureAD_B2B_Ideas).

### <a name="can-we-send-an-invitation-that-is-automatically-redeemed-so-that-hello-user-is-just-ready-toogo-or-does-hello-user-always-have-tooclick-through-toohello-redemption-url"></a>Possiamo inviare un invito che viene recuperato automaticamente, in modo che hello utente sono solo "pronto toogo"? O utente hello sempre privo di tooclick tramite URL riscatto toohello?
Inviti inviati da un utente nell'organizzazione che ha anche un membro dell'organizzazione partner hello invitare hello non richiedono riscatto utente B2B hello.

È consigliabile che si invita un utente di hello toojoin di hello partner dell'organizzazione si invitano dell'organizzazione. [Aggiungere il ruolo di mittente dell'invito guest toohello utente nell'organizzazione risorse hello](active-directory-b2b-add-guest-to-role.md). Questo utente è possibile invitare altri utenti nell'organizzazione partner hello utilizzando Accedi hello dell'interfaccia utente, gli script di PowerShell o le API. Quindi, gli utenti collaborazione B2B da tale organizzazione non sono necessari tooredeem gli inviti.

### <a name="how-does-b2b-collaboration-work-when-hello-invited-partner-is-using-federation-tooadd-their-own-on-premises-authentication"></a>Collaborazione B2B funzionamento quando hello invitato partner utilizza federazione tooadd la propria autenticazione locale
Se il partner hello ha un tenant di Azure AD federato toohello infrastruttura di autenticazione locale, single sign-on (SSO) viene automaticamente ottenuta in locale. Se il partner hello non dispone di un tenant di Azure AD, viene creato un account Azure AD per i nuovi utenti. 

### <a name="i-thought-azure-ad-b2b-didnt-accept-gmailcom-and-outlookcom-email-addresses-and-that-b2c-was-used-for-those-kinds-of-accounts"></a>Pensavo che B2B di Azure AD non accettasse gli indirizzi di posta elettronica gmail.com e outlook.com e che B2C venisse usato per tali tipi di account.
Viene rimossa hello B2B e differenze in termini di cui sono supportate le identità la collaborazione business-a-società (B2C). identità Hello utilizzata non è un buon motivo toochoose tra usando B2B o B2C. Per informazioni sulla scelta dell'opzione di collaborazione, vedere [Confrontare Collaborazione B2B e B2C di Azure Active Directory](active-directory-b2b-compare-b2c.md).

### <a name="what-applications-and-services-support-azure-b2b-guest-users"></a>Quali applicazioni e servizi supportano gli utenti guest di Azure B2B?
Tutte le applicazioni integrate con Azure AD supportano gli utenti guest B2B di Azure. 

### <a name="can-we-force-multi-factor-authentication-for-b2b-guest-users-if-our-partners-dont-have-multi-factor-authentication"></a>Se i partner non dispongono dell' autenticazione a più fattori, è possibile imporla per gli utenti guest di B2B?
Sì. Per altre informazioni, vedere [Accesso condizionale per gli utenti di Collaborazione B2B](active-directory-b2b-mfa-instructions.md).

### <a name="in-sharepoint-you-can-define-an-allow-or-deny-list-for-external-users-can-we-do-this-in-azure"></a>In SharePoint è possibile definire un elenco di utenti esterni "consentiti" o "negati". È possibile farlo anche in Azure?
Sì. Collaborazione B2B di Azure AD supporta l'elenco dei tipi consentiti e negati. 

### <a name="what-licenses-do-we-need-toouse-azure-ad-b2b"></a>Operazioni di licenze è necessario toouse B2B di Azure AD?
Per informazioni su ciò che le licenze dell'organizzazione devono toouse B2B di Azure Active Directory, vedere [collaborazione B2B di Azure Active Directory licenze indicazioni](active-directory-b2b-licensing.md).

### <a name="next-steps"></a>Passaggi successivi

Vedere gli altri articoli su Azure AD B2B Collaboration.

* [Che cos'è Azure AD B2B Collaboration?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Procedura di aggiunta di utenti di Collaborazione B2B ad Azure Active Directory da parte degli amministratori](active-directory-b2b-admin-add-users.md)
* [Procedura per aggiungere utenti di Collaborazione B2B da parte di Information Worker](active-directory-b2b-iw-add-users.md)
* [elementi Hello di posta elettronica di invito collaborazione B2B di hello](active-directory-b2b-invitation-email.md)
* [Riscatto dell'invito di Collaborazione B2B](active-directory-b2b-redemption-experience.md)
* [Licenze per la Collaborazione B2B di Azure AD](active-directory-b2b-licensing.md)
* [Risoluzione dei problemi di Collaborazione B2B di Azure AD](active-directory-b2b-troubleshooting.md)
* [API e personalizzazione per Collaborazione B2B di Azure AD](active-directory-b2b-api.md)
* [Autenticazione a più fattori per utenti di Collaborazione B2B](active-directory-b2b-mfa-instructions.md)
* [Aggiungere gli utenti per la Collaborazione B2B senza un invito](active-directory-b2b-add-user-without-invite.md)
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
