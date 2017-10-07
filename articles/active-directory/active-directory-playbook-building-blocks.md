---
title: Active Directory di prova di blocchi predefiniti di concetto playbook aaaAzure | Documenti Microsoft
description: "Esplorare e implementare rapidamente gli scenari di Gestione delle identità e degli accessi"
services: active-directory
keywords: azure active directory, studio, modello di verifica, PoC
documentationcenter: 
author: dstefanMSFT
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: dstefan
ms.openlocfilehash: e54148330a123baf27d7e0f73469ff2a24c0efcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-building-blocks"></a>Playbook dei modelli di verifica di Azure Active Directory: blocchi predefiniti

## <a name="catalog-of-roles"></a>Catalogo dei ruoli

| Ruolo | Descrizione | Responsabilità del modello di verifica |
| --- | --- | --- |
| **Team di sviluppo e architettura identità** | Il team è in genere hello uno che progetta la soluzione hello, implementa i prototipi, unità approvazioni e infine le consegne toooperations | Forniscono ambienti hello e sono hello quelli valutando hello scenari diversi dal punto di vista di hello gestibilità |
| **Team di gestione dell'identità locale** | Gestisce hello identità diverse origini in locale: foreste di Active Directory, la directory LDAP, sistemi HR e provider di identità federativa. | Fornire tooon locale di accedere alle risorse necessarie per hello scenari di prova.<br/>Deve essere coinvolto nella misura minore possibile|
| **Proprietari tecnici delle applicazioni** | Proprietari di tecnici di hello cloud diverse App e servizi integrabili con Azure AD | Disponibilità di informazioni dettagliate sulle applicazioni SaaS (potenzialmente istanze per il test) |
| **Amministrazione globale di Azure AD** | Gestisce la configurazione di hello Azure AD | Fornire le credenziali del servizio di sincronizzazione hello tooconfigure. In genere hello stesso team come l'architettura di identità durante la prova ma separare durante la fase operativa hello|
| **Team responsabile del database** | Proprietari dell'infrastruttura di Database hello | Fornire ambiente tooSQL di accesso (ad FS o Azure AD Connect) per operazioni di preparazione dello scenario specifico.<br/>Deve essere coinvolto nella misura minore possibile |
| **Team responsabile della rete** | Proprietari dell'infrastruttura di rete hello | Fornire l'accesso richiesto a livello di rete hello sincronizzazione hello server tooproperly accesso hello all'origine dati e dei servizi cloud (regole del firewall, porte aperte, le regole IPSec e così via). |
| **Team responsabile della sicurezza** | Definisce una strategia di sicurezza hello, analizza i report di sicurezza da diverse origini e conforme sui risultati. | Disponibilità di scenari di valutazione della sicurezza della destinazione |

## <a name="common-prerequisites-for-all-building-blocks"></a>Prerequisiti comuni per tutti i blocchi predefiniti

Di seguito sono riportati alcuni prerequisiti necessari per qualsiasi modello di verifica usato con Azure AD Premium.

| Prerequisito. | Risorse |
| --- | --- |
| Tenant di Azure AD definito con una sottoscrizione di Azure valida | [Come tenant di Azure Active Directory tooget](active-directory-howto-tenant.md)<br/>**Nota:** se si dispone già di un ambiente con licenze di Azure AD Premium, è possibile ottenere una sottoscrizione di cap zero passando toohttps://aka.ms/accessaad <br/>Per altre informazioni, vedere: https://blogs.technet.microsoft.com/enterprisemobility/2016/02/26/azure-ad-mailbag-azure-subscriptions-and-azure-ad-2/ e https://technet.microsoft.com/library/dn832618.aspx |
| Domini definiti e verificati | [Aggiungere un tooAzure di nome di dominio personalizzato Active Directory](active-directory-domains-add-azure-portal.md)<br/>**Nota:** vengono illustrati alcuni carichi di lavoro, ad esempio Power BI potrebbe avere un tenant di azure AD in hello il provisioning. toocheck se un determinato dominio tenant tooa associato, passare toohttps://login.microsoftonline.com/ {domain}/v2.0/.well-known/openid-configuration. Se si ottiene una risposta corretta, quindi dominio hello è già assegnato tooa tenant e assumere potrebbe essere necessaria. In questo caso, contattare Microsoft per le istruzioni. Ulteriori informazioni sulle opzioni di acquisizione della proprietà hello in: [cos'è Self-Service Signup per Azure?](active-directory-self-service-signup.md) |
| Versione di valutazione di Azure AD Premium o EMS abilitata | [Azure Active Directory Premium gratis per un mese](https://azure.microsoft.com/trial/get-started-active-directory/) |
| È stato assegnato licenze di Azure AD Premium o EMS agli utenti di tooPoC | [Concessione di licenze a se stessi e agli utenti in Azure Active Directory](active-directory-licensing-get-started-azure-portal.md) |
| Credenziali di amministratore globale di Azure AD | [Assegnazione dei ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md) |
| Facoltativo ma vivamente consigliato: ambiente di laboratorio parallelo come fallback | [Prerequisiti di Azure AD Connect](./connect/active-directory-aadconnect-prerequisites.md) |

## <a name="directory-synchronization---password-hash-sync-phs---new-installation"></a>Sincronizzazione directory: sincronizzazione dell'hash delle password (PHS), nuova installazione

TooComplete tempo approssimativo: un'ora per meno di 1.000 utenti di prova

### <a name="pre-requisites"></a>Prerequisiti

| Prerequisito. | Risorse |
| --- | --- |
| Server tooRun Azure AD Connect | [Prerequisiti di Azure AD Connect](./connect/active-directory-aadconnect-prerequisites.md) |
| Gli utenti di prova, in hello stesso dominio e una parte di un gruppo di sicurezza e l'unità Organizzativa | [Installazione personalizzata di Azure AD Connect](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) |
| Azure AD Connect funzionalità necessarie per hello POC vengono identificati | [Connettere Active Directory ad Azure Active Directory - Configurare le funzionalità di sincronizzazione](./connect/active-directory-aadconnect.md#configure-sync-features) |
| Disponibilità delle credenziali necessarie per gli ambienti locale e cloud  | [Azure AD Connect: Account e autorizzazioni](./connect/active-directory-aadconnect-accounts-permissions.md) |

### <a name="steps"></a>Passi

| Passaggio | Risorse |
| --- | --- |
| Scaricare hello la versione più recente di Azure AD Connect | [Scaricare Microsoft Azure Active Directory Connect](https://www.microsoft.com/download/details.aspx?id=47594) |
| Installare Azure AD Connect con percorso più semplice hello: Express <br/>1. Toohello destinazione OU toominimize hello ciclo di sincronizzazione ora filtro<br/>2. Scegliere il set di destinazioni di utenti nel gruppo locale hello.<br/>3. Distribuzione delle caratteristiche di hello necessari da hello altri temi POC | [Azure AD Connect: Installazione personalizzata: Filtro unità organizzativa e dominio](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) <br/>[Azure AD Connect: Installazione personalizzata: Filtro di sincronizzazione basato sui gruppi](./connect/active-directory-aadconnect-get-started-custom.md#sync-filtering-based-on-groups)<br/>[Azure AD Connect: Integrazione delle identità locali con Azure Active Directory: Configurare le funzionalità di sincronizzazione](./connect/active-directory-aadconnect.md#configure-sync-features) |
| Aprire hello Azure AD Connect dell'interfaccia utente e visualizzare i profili hello in esecuzione completata (importazione, sincronizzazione ed esportazione) | [Servizio di sincronizzazione Azure AD Connect: Utilità di pianificazione](./connect/active-directory-aadconnectsync-feature-scheduler.md) |
| Aprire hello [il portale di gestione di Azure AD](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/), scegliere Pannello di toohello "All Users", aggiungere la colonna "Origine di autorità" e vedere visualizzati agli utenti di hello contrassegnato correttamente come proveniente da "Windows Server Active Directory" | [Portale di gestione di Azure AD](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) |

### <a name="considerations"></a>Considerazioni

1. Esaminare le considerazioni sulla sicurezza hello di sincronizzazione degli hash delle password [qui](./connect/active-directory-aadconnectsync-implement-password-synchronization.md).  Se sincronizzazione degli hash delle password per gli utenti di produzione pilota definitivamente non è un'opzione, quindi considerare hello alternative seguenti:
   * Creare gli utenti di test in dominio di produzione hello. Assicurarsi di non sincronizzare altri account
   * Spostamento tooan UAT ambiente
2.  Se si desidera toopursue federazione, vale la pena toounderstand hello costi associati una soluzione federativa Provider di identità locale di là hello POC e misure che contro hello vantaggi si stanno cercando:
    * È presente nel percorso critico hello è toodesign per la disponibilità elevata
    * Si tratta di un servizio locale è necessario toocapacity piano
    * Si tratta di un servizio locale è necessario toomonitor, mantenere/patch

Altre informazioni: [Informazione sulla gestione delle identità di Office 365 e Azure Active Directory - Identità federative](https://support.office.com/article/Understanding-Office-365-identity-and-Azure-Active-Directory-06a189e7-5ec6-4af2-94bf-a22ea225a7a9#bk_federated)

## <a name="branding"></a>Personalizzazione

TooComplete tempo approssimativo: 15 minuti

### <a name="pre-requisites"></a>Prerequisiti

| Prerequisito. | Risorse |
| --- | --- |
| Risorse (immagini, i logo e così via); Per la visualizzazione migliore rendere asset hello che hanno dimensioni consigliata hello. | [Aggiungere informazioni personalizzate distintive tooyour nella pagina di accesso in hello Azure Active Directory della società](active-directory-branding-custom-signon-azure-portal.md) |
| Facoltativo: Se l'ambiente hello dispone di un server ADFS, accedere a tema web toocustomize di toohello server | [Personalizzazione dell'accesso per utenti AD FS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/ad-fs-user-sign-in-customization) |
| Esperienza di accesso dell'utente finale tooperform computer client |  |
| Facoltativo: I dispositivi mobili toovalidate esperienza |  |

### <a name="steps"></a>Passi

| Passaggio | Risorse |
| --- | --- |
| Vai AD tooAzure portale di gestione | [Portale di gestione di Azure AD - Informazioni personalizzate distintive dell'azienda](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/LoginTenantBranding) |
| Caricare gli asset hello della pagina di accesso hello (logo eroe, logo piccolo, etichette e così via). Facoltativamente, se si dispone di AD FS, allineare hello stesso asset con pagine di accesso ADFS | [Aggiungere personalizzazione tooyour sign-on e pagine del Pannello di accesso aziendale: elementi personalizzabili](active-directory-add-company-branding.md) |
| Attendere un paio di minuti per l'effetto toofully modifica hello |  |
| Accedi con hello POC utente credenziali toohttps://myapps.microsoft.com |  |
| Verificare l'aspetto hello nel browser | [Aggiungere informazioni personalizzate distintive tooyour sign-on e pagine del Pannello di accesso della società](active-directory-add-company-branding.md) |
| Facoltativamente, verificare l'aspetto hello in altri dispositivi |  |

### <a name="considerations"></a>Considerazioni

Se rimane hello precedente aspetto dopo la personalizzazione di hello svuotamento della cache di hello browser client e ripetere l'operazione di hello.

## <a name="group-based-licensing"></a>Licenze basate sui gruppi

TooComplete tempo approssimativo: 10 minuti

### <a name="pre-requisites"></a>Prerequisiti

| Prerequisito. | Risorse |
| --- | --- |
| Tutti gli utenti dei moduli di verifica fanno parte di un gruppo di sicurezza (cloud o locale) | [Creare un gruppo e aggiungere membri in Azure Active Directory](active-directory-groups-create-azure-portal.md) |

### <a name="steps"></a>Passi

| Passaggio | Risorse |
| --- | --- |
| Pannello toolicenses andare nel portale di gestione di Azure AD | [Portale di gestione di Azure AD: Licenze](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products) |
| Assegnare gruppo di sicurezza di hello licenze toohello con gli utenti di prova. | [Assegnare licenze tooa gruppo di utenti in Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md) |

### <a name="considerations"></a>Considerazioni

In caso di eventuali problemi, andare troppo[scenari, limitazioni e problemi noti relativi all'utilizzo di gruppi toomanage licenze in Azure Active Directory](active-directory-licensing-group-advanced.md)

## <a name="saas-federated-sso-configuration"></a>SaaS: configurazione SSO federato

TooComplete tempo approssimativo: 60 minuti

### <a name="pre-requisites"></a>Prerequisiti

| Prerequisito. | Risorse |
| --- | --- |
| Ambiente di hello disponibile per l'applicazione SaaS di test. In questa guida viene usato ServiceNow come esempio.<br/>È consigliabile toouse un test istanza toominimize le forze di attrito sull'esplorazione di mapping e la qualità dei dati esistente. | Passare toohttps://developer.servicenow.com/app.do#! / home processo hello toostart di un'istanza di test |
| Console di gestione ServiceNow toohello accesso amministratore | [Esercitazione: Integrazione di Azure Active Directory con ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Set di utenti tooassign hello applicazione di destinazione. È consigliabile un gruppo di sicurezza contenente gli utenti di prova hello. <br/>Se la creazione del gruppo di hello non è fattibile, quindi assegnare utenti hello toodirectly toohello applicazione hello PoC | [Assegnare un'applicazione aziendale tooan utente o gruppo in Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |

### <a name="steps"></a>Passi

| Passaggio | Risorse |
| --- | --- |
| Condividere gli attori tooall esercitazione hello dal Microsoft Documentation  | [Esercitazione: Integrazione di Azure Active Directory con ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Impostare una riunione di lavoro e seguire i passaggi dell'esercitazione hello con ogni attore. | [Esercitazione: Integrazione di Azure Active Directory con ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Assegnare hello app toohello gruppo identificato nella hello prerequisiti. Se hello POC dispone di accesso condizionale nell'ambito di hello, è possibile rivedere che in un secondo momento e aggiungere l'autenticazione a più fattori e così via. <br/>Tenere presente che questo verrà utilizzata nel processo di provisioning (se configurata) hello |  [Assegnare un'applicazione aziendale tooan utente o gruppo in Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) <br/>[Creare un gruppo e aggiungere membri in Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| Utilizzare AD Azure management Portal tooadd ServiceNow applicazione dalla raccolta| [Portale di gestione di Azure AD: applicazioni aziendali](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/Overview) <br/>[Novità della gestione delle applicazioni aziendali in Azure Active Directory](active-directory-enterprise-apps-whats-new-azure-portal.md) |
| Nel pannello "Single sign-on" dell'app ServiceNow abilitare "SAML-based Sign-on" (Accesso basato su SAML) |  |
| Compilare i campi "URL di accesso" e "Identificatore" con l'URL di ServiceNow<br/>Casella di controllo hello troppo "attivare nuovo certificato"<br/>e salvare le impostazioni |  |
| Aprire Pannello di "Configurazione di ServiceNow" nella parte inferiore di hello di hello pannello tooview personalizzata le istruzioni necessarie per tooconfigure ServiceNow |  |
| Seguire le istruzioni tooconfigure ServiceNow |  |
| Nel pannello "Provisioning" dell'applicazione ServiceNow abilitare il provisioning automatico | [La gestione per applicazioni aziendali nel nuovo portale di Azure hello di provisioning dell'account utente](active-directory-enterprise-apps-manage-provisioning.md) |
| Attendere alcuni minuti il completamento del provisioning.  In hello frattempo, è possibile controllare hello provisioning report |  |
| Accedere come un utente di prova dotato di accesso toohttps://myapps.microsoft.com/ | [Che cos'è hello Pannello di accesso?](active-directory-saas-access-panel-introduction.md) |
| Fare clic sul riquadro hello per un'applicazione hello appena creato. Confermare l'accesso |  |
| Facoltativamente, è possibile controllare i report di utilizzo dell'applicazione hello. Si noti latenza, pertanto è necessario toowait traffico hello toosee ora nei report hello. | [Report attività di accesso nel portale di Azure Active Directory hello: utilizzo delle applicazioni gestite](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Criteri di conservazione dei report di Azure Active Directory](active-directory-reporting-retention.md) |

### <a name="considerations"></a>Considerazioni

1. Sopra [esercitazione](active-directory-saas-servicenow-tutorial.md) fa riferimento AD Azure tooold esperienza di gestione. Ma il modulo di verifica si basa sull'esperienza di [Avvio rapido](active-directory-enterprise-apps-whats-new-azure-portal.md#quick-start-get-going-with-your-new-application-right-away).
2. Se un'applicazione hello destinazione non è presente nella raccolta di hello, è possibile utilizzare "Bring la propria app". Altre informazioni: [Novità della gestione delle applicazioni aziendali in Azure Active Directory: Aggiungere applicazioni personalizzate da un'unica posizione](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

## <a name="saas-password-sso-configuration"></a>SaaS: configurazione SSO con password

TooComplete tempo approssimativo: 15 minuti

### <a name="pre-requisites"></a>Prerequisiti

| Prerequisito. | Risorse |
| --- | --- |
| Ambiente di test per le applicazioni SaaS. Esempi di SSO con password sono HipChat e Twitter. Per qualsiasi altra applicazione, è necessario hello URL esatto della pagina hello con modulo di accesso html. | [Twitter in Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/aad.twitter)<br/>[HipChat in Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/aad.hipchat) |
| Account per le applicazioni di hello di test. | [Iscrizione a Twitter](https://twitter.com/signup?lang=en)<br/>[Iscrizione gratuita: HipChat](https://www.hipchat.com/sign_up) |
| Set di utenti tooassign hello applicazione di destinazione. È consigliabile una sicurezza gruppo contenuto hello users. | [Assegnare un'applicazione aziendale tooan utente o gruppo in Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Amministratore locale accesso tooa computer toodeploy hello estensione del Pannello di accesso per Internet Explorer, Chrome o Firefox | [Estensione Pannello di accesso per IE](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Estensione Pannello di accesso per Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Estensione Pannello di accesso per Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |

### <a name="steps"></a>Passi

| Passaggio | Risorse |
| --- | --- |
| Installare l'estensione browser hello | [Estensione Pannello di accesso per IE](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Estensione Pannello di accesso per Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Estensione Pannello di accesso per Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |
| Configurare l'applicazione dalla raccolta | [Novità di gestione delle applicazioni dell'organizzazione in Azure Active Directory: raccolta di applicazioni nuove e migliorate di hello](active-directory-enterprise-apps-whats-new-azure-portal.md#improvements-to-the-azure-active-directory-application-gallery) |
| Configurare l'accesso SSO con password | [Gestione di single sign-on per le app aziendali nel nuovo portale di Azure hello: basato su Password sign-on](active-directory-enterprise-apps-manage-sso.md#password-based-sign-on) |
| Assegnare hello app toohello gruppo identificato nella hello prerequisiti | [Assegnare un'applicazione aziendale tooan utente o gruppo in Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Accedere come un utente di prova dotato di accesso toohttps://myapps.microsoft.com/ |  |
| Fare clic sul riquadro hello per un'applicazione hello appena creato. | [Che cos'è hello Pannello di accesso?: SSO basato su Password senza provisioning delle identità](active-directory-saas-access-panel-introduction.md#password-based-sso-without-identity-provisioning) |
| Fornire le credenziali dell'applicazione hello | [Che cos'è hello Pannello di accesso?: SSO basato su Password senza provisioning delle identità](active-directory-saas-access-panel-introduction.md#password-based-sso-without-identity-provisioning) |
| Chiudere il browser hello e account di accesso di ripetizione hello. Questa volta, tuttavia è necessario che l'utente hello visualizzata accesso trasparente toohello applicazione. |  |
| Facoltativamente, è possibile controllare i report di utilizzo dell'applicazione hello. Si noti latenza, pertanto è necessario toowait traffico hello toosee ora nei report hello. | [Report attività di accesso nel portale di Azure Active Directory hello: utilizzo delle applicazioni gestite](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Criteri di conservazione dei report di Azure Active Directory](active-directory-reporting-retention.md) |

### <a name="considerations"></a>Considerazioni

Se un'applicazione hello destinazione non è presente nella raccolta di hello, è possibile utilizzare "Bring la propria app". Altre informazioni: [Novità della gestione delle applicazioni aziendali in Azure Active Directory: Aggiungere applicazioni personalizzate da un'unica posizione](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

 Tenere hello presente i requisiti seguenti:
   * L'applicazione deve avere un URL di accesso noto
   * Hello nella pagina di accesso deve contenere un form HTML con uno o più campi text che le estensioni del browser hello possibile popolano automaticamente. In hello minimo, deve contenere il nome utente e password.

## <a name="saas-shared-accounts-configuration"></a>SaaS: configurazione di account condivisi

TooComplete tempo approssimativo: 30 minuti

### <a name="pre-requisites"></a>Prerequisiti

| Prerequisito. | Risorse |
| --- | --- |
| Hello elenco di applicazioni di destinazione e gli URL di accesso esatto anticipatamente hello. Ad esempio, è possibile usare Twitter. | [Twitter in Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/aad.twitter)<br/>[Iscrizione a Twitter](https://twitter.com/signup?lang=en) |
| Credenziali condivise per questa applicazione SaaS. | [Condivisione di account con Azure AD](active-directory-sharing-accounts.md)<br/>[Post sul rollover automatizzato delle password in Azure AD per Facebook, Twitter e LinkedIn ora in anteprima nel blog su sicurezza e mobilità aziendale] (https://blogs.technet.microsoft.com/enterprisemobility/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview/ ) |
| Le credenziali per almeno due membri del team che avranno accesso hello stesso account. Devono fare parte di un gruppo di sicurezza. | [Assegnare un'applicazione aziendale tooan utente o gruppo in Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Amministratore locale accesso tooa computer toodeploy hello estensione del Pannello di accesso per Internet Explorer, Chrome o Firefox | [Estensione Pannello di accesso per IE](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Estensione Pannello di accesso per Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Estensione Pannello di accesso per Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |

### <a name="steps"></a>Passi

| Passaggio | Risorse |
| --- | --- |
| Installare l'estensione browser hello | [Estensione Pannello di accesso per IE](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Estensione Pannello di accesso per Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Estensione Pannello di accesso per Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |
| Configurare l'applicazione dalla raccolta | [Novità di gestione delle applicazioni dell'organizzazione in Azure Active Directory: raccolta di applicazioni nuove e migliorate di hello](active-directory-enterprise-apps-whats-new-azure-portal.md#improvements-to-the-azure-active-directory-application-gallery) |
| Configurare l'accesso SSO con password | [Gestione di single sign-on per le app aziendali nel nuovo portale di Azure hello: basato su Password sign-on](active-directory-enterprise-apps-manage-sso.md#password-based-sign-on) |
| Assegnare hello app toohello gruppo identificato nella hello prerequisiti durante l'assegnazione di credenziali | [Assegnare un'applicazione aziendale tooan utente o gruppo in Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Accedere come utenti diversi che app l'accesso come hello **stesso condivisa account.**  |  |
| Facoltativamente, è possibile controllare i report di utilizzo dell'applicazione hello. Si noti latenza, pertanto è necessario toowait traffico hello toosee ora nei report hello. | [Report attività di accesso nel portale di Azure Active Directory hello: utilizzo delle applicazioni gestite](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Criteri di conservazione dei report di Azure Active Directory](active-directory-reporting-retention.md) |


### <a name="considerations"></a>Considerazioni

Se un'applicazione hello destinazione non è presente nella raccolta di hello, è possibile utilizzare "Bring la propria app". Altre informazioni: [Novità della gestione delle applicazioni aziendali in Azure Active Directory: Aggiungere applicazioni personalizzate da un'unica posizione](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

 Tenere hello presente i requisiti seguenti:
   * L'applicazione deve avere un URL di accesso noto
   * Hello nella pagina di accesso deve contenere un form HTML con uno o più campi text che le estensioni del browser hello possibile popolano automaticamente. In hello minimo, deve contenere il nome utente e password.

## <a name="app-proxy-configuration"></a>Configurazione del proxy delle app

TooComplete tempo approssimativo: 20 minuti

### <a name="pre-requisites"></a>Prerequisiti

| Prerequisito. | Risorse |
| --- | --- |
| Una sottoscrizione di Microsoft Azure AD Basic o Premium e una directory di Azure AD di cui si è un amministratore globale | [Edizioni di Azure Active Directory](active-directory-editions.md) |
| Un'applicazione web ospitata locale che si desidera tooconfigure per l'accesso remoto |  |
| Un server che esegue Windows Server 2012 R2 o Windows 8.1 o versione successiva, in cui è possibile installare hello connettore Proxy dell'applicazione | [Comprendere i connettori del proxy applicazione di Azure AD](application-proxy-understand-connectors.md) |
| Se nel percorso di hello è presente un firewall, assicurarsi che sia aperta in modo che hello che connettore può rendere HTTPS (TCP) richiede toohello Proxy dell'applicazione | [Abilitare il Proxy di applicazione nel portale di Azure hello: prerequisiti del Proxy di applicazione](active-directory-application-proxy-enable.md#application-proxy-prerequisites) |
| Se l'organizzazione utilizza proxy toohello tooconnect server internet, hanno un aspetto hello blog post funzionante con server proxy locale esistenti per informazioni dettagliate sulla tooconfigure li | [Usare server proxy locali esistenti](application-proxy-working-with-proxy-servers.md) |


### <a name="steps"></a>Passi

| Passaggio | Risorse |
| --- | --- |
| Installare un connettore sul server hello | [Abilitare il Proxy di applicazione nel portale di Azure hello: installare e registrare hello connettore](active-directory-application-proxy-enable.md#install-and-register-a-connector) |
| Pubblicare un'applicazione hello locale in Azure AD come applicazione Proxy dell'applicazione | [Pubblicare applicazioni mediante il proxy di applicazione AD Azure](application-proxy-publish-azure-portal.md) |
| Assegnare gli utenti test | [Pubblicare applicazioni mediante il proxy dell'applicazione AD Azure: Aggiungere un utente di test](application-proxy-publish-azure-portal.md#add-a-test-user) |
| Facoltativamente, configurare un'esperienza Single Sign-On per gli utenti | [Fornire accesso Single Sign-On mediante il proxy dell'applicazione Azure AD](application-proxy-sso-azure-portal.md) |
| App di test tramite la firma nel portale tooMyApps come utente assegnato | https://myapps.microsoft.com |

### <a name="considerations"></a>Considerazioni

1. Mentre si consiglia di inserire il connettore hello nella rete aziendale, esistono casi in cui verrà visualizzato collocandola in cloud hello ottenere prestazioni migliori. Altre informazioni: [Considerazioni relative alla topologia di rete quando si usa il proxy di applicazione di Azure Active Directory](application-proxy-network-topology-considerations.md)
2. Per informazioni dettagliate sulla sicurezza e su come garantire una soluzione di accesso remoto particolarmente protetta gestendo solo le connessioni in uscita, vedere: [Considerazioni relative alla sicurezza quando si accede alle app in remoto usando il proxy applicazione di Azure AD](application-proxy-security-considerations.md)

## <a name="generic-ldap-connector-configuration"></a>Configurazione del connettore LDAP generico

TooComplete tempo approssimativo: 60 minuti

> [!IMPORTANT]
> Si tratta di una configurazione avanzata che richiede una certa conoscenza di FIM o MIM. Se usata in produzione, è consigliabile leggere le domande su questa configurazione in [supporto tecnico Premier](https://support.microsoft.com/premier).

### <a name="pre-requisites"></a>Prerequisiti

| Prerequisito. | Risorse |
| --- | --- |
| Azure AD Connect installato e configurato | Blocco predefinito: [Sincronizzazione directory: Sincronizzazione dell'hash delle password](#directory-synchronization--password-hash-sync-phs--new-installation) |
| Istanza ADLDS conforme ai requisiti | [Riferimento tecnico connettore LDAP generico: Panoramica di hello connettore LDAP generico](./connect/active-directory-aadconnectsync-connector-genericldap.md#overview-of-the-generic-ldap-connector) |
| Elenco dei carichi di lavoro usati dagli utenti e attributi associati a questi carichi di lavoro | [Sincronizzazione di Azure AD Connect: attributi sincronizzati tooAzure Active Directory](./connect/active-directory-aadconnectsync-attributes-synchronized.md) |


### <a name="steps"></a>Passi

| Passaggio | Risorse |
| --- | --- |
| Aggiungere un connettore Generic LDAP | [Documentazione tecnica sul connettore Generic LDAP: Creare un nuovo connettore](./connect/active-directory-aadconnectsync-connector-genericldap.md#create-a-new-connector) |
| Creare profili di esecuzione per il connettore creato (importazione completa, importazione delta, sincronizzazione completa, sincronizzazione delta, esportazione) | [Create a Management Agent Run Profile](https://technet.microsoft.com/library/jj590219(v=ws.10).aspx) (Creare un profilo di esecuzione dell'agente di gestione)<br/> [Utilizzo dei connettori con hello Azure AD Connect sincronizzazione Service Manager](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md)|
| Eseguire il profilo di importazione completa e verificare se sono presenti oggetti nello spazio connettore | [Search for a Connector Space Object](https://technet.microsoft.com/library/jj590287(v=ws.10).aspx) (Ricerca di un oggetto nello spazio connettore)<br/>[Utilizzo dei connettori con hello sincronizzazione Service Manager di Azure AD Connect: spazio connettore di ricerca](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md#search-connector-space) |
| Creare regole di sincronizzazione in modo che gli oggetti nel metaverse abbiano gli attributi necessari per i carichi di lavoro | [Sincronizzazione di Azure AD Connect: procedure consigliate per la modifica della configurazione predefinita di hello: modifica di regole tooSynchronization](./connect/active-directory-aadconnectsync-best-practices-changing-default-configuration.md#changes-to-synchronization-rules)<br/>[Servizio di sincronizzazione Azure AD Connect: informazioni sul provisioning dichiarativo](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning.md)<br/>[Servizio di sincronizzazione Azure AD Connect: Informazioni sulle espressioni di provisioning dichiarativo](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |
| Avviare un ciclo di sincronizzazione completa | [Sincronizzazione di Azure AD Connect: utilità di pianificazione: avvio dell'utilità di pianificazione di hello](./connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler) |
| In caso di problemi, eseguire le procedure per la risoluzione | [Risolvere i problemi relativi a un oggetto che è non in sincronizzazione tooAzure AD](./connect/active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) |
| Verificare, che LDAP utente può accedere e accedere a un'applicazione hello | https://myapps.microsoft.com |

### <a name="considerations"></a>Considerazioni

> [!IMPORTANT]
> Si tratta di una configurazione avanzata che richiede una certa conoscenza di FIM o MIM. Se usata in produzione, è consigliabile leggere le domande su questa configurazione in [supporto tecnico Premier](https://support.microsoft.com/premier).

## <a name="groups---delegated-ownership"></a>Gruppi: proprietà delegata

TooComplete tempo approssimativo: 10 minuti

### <a name="pre-requisites"></a>Prerequisiti

| Prerequisito. | Risorse |
| --- | --- |
| Applicazione SaaS (SSO federato o con password) già configurata | Blocco predefinito: [SaaS: configurazione SSO federato](#saas-federated-sso-configuration) |
| Viene identificato il gruppo cloud che viene assegnato l'accesso toohello applicazione # 1 | Blocco predefinito: [SaaS: configurazione SSO federato](#saas-federated-sso-configuration) <br/>[Creare un gruppo e aggiungere membri in Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| Sono disponibili le credenziali per il proprietario del gruppo hello | [Gestire accesso tooresources con gruppi di Azure Active Directory](active-directory-manage-groups.md) |
| Le credenziali per le informazioni hello worker che accedono alle App hello è stato individuato. | [Che cos'è hello Pannello di accesso?](active-directory-saas-access-panel-introduction.md) |


### <a name="steps"></a>Passi

| Passaggio | Risorse |
| --- | --- |
| Identifica il gruppo che è stato concesso l'accesso toohello applicazione hello e configurare il proprietario di hello di un determinato gruppo| [Gestire le impostazioni di hello per un gruppo in Azure Active Directory](active-directory-groups-settings-azure-portal.md) |
| Effettuare l'accesso come proprietario del gruppo di hello, vedere l'appartenenza al gruppo hello nella scheda gruppi del Pannello di accesso | [Pagina di gestione dei gruppi di Azure Active Directory](https://account.activedirectory.windowsazure.com/r/#/groups) |
| Aggiungere informativi hello desiderato tootest |  |
| Accedi information worker di hello, confermare il riquadro hello è disponibile | [Che cos'è hello Pannello di accesso?](active-directory-saas-access-panel-introduction.md) |

### <a name="considerations"></a>Considerazioni

Se un'applicazione hello è abilitato il provisioning, si potrebbe essere necessario toowait alcuni minuti per hello provisioning toocomplete prima di accedere a un'applicazione hello information worker di hello.

## <a name="saas-and-identity-lifecycle"></a>SaaS e ciclo di vita delle identità

### <a name="pre-requisites"></a>Prerequisiti

| Prerequisito. | Risorse |
| --- | --- |
| Applicazione SaaS (SSO federato o con password) già configurata | Blocco predefinito: [SaaS: configurazione SSO federato](#saas-federated-sso-configuration) |
| Viene identificato il gruppo cloud che viene assegnato l'accesso toohello applicazione # 1 | Blocco predefinito: [SaaS: configurazione SSO federato](#saas-federated-sso-configuration) <br/>[Creare un gruppo e aggiungere membri in Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| Le credenziali per le informazioni hello worker che accedono alle App hello è stato individuato. | [Che cos'è hello Pannello di accesso?](active-directory-saas-access-panel-introduction.md) |


### <a name="steps"></a>Passi

| Passaggio | Risorse |
| --- | --- |
| Rimuovi utente hello da hello gruppo hello app assegnato troppo| [Gestire l'appartenenza al gruppo per gli utenti nel tenant di Azure Active Directory](active-directory-groups-members-azure-portal.md) |
| Attendere alcuni minuti il completamento del deprovisioning | [Automatizzare il provisioning e il deprovisioning utenti in applicazioni SaaS con Azure Active Directory: Come funziona il provisioning automatizzato?](active-directory-saas-app-provisioning.md#how-does-automated-provisioning-work) |
| In una sessione separata del browser, accedere come portale delle App toomy lavoro informazioni hello e confermare tale riquadro è manca | http://myapps.microsoft.com |


### <a name="considerations"></a>Considerazioni

Estrapolare hello PoC scenario tooleavers e/o assenza scenari. Se l'utente hello Ottiene disabilitato Active Directory locale o rimosso, non è più un modo toolog in toohello applicazione SaaS.

## <a name="self-service-access-tooapplication-management"></a>Self tooApplication accesso al servizio Gestione

TooComplete tempo approssimativo: 10 minuti

### <a name="pre-requisites"></a>Prerequisiti

| Prerequisito. | Risorse |
| --- | --- |
| Identificare gli utenti di prova che verranno richiesto di accedere ad applicazioni toohello, come parte del gruppo di sicurezza hello | Blocco predefinito: [SaaS: configurazione SSO federato](#saas-federated-sso-configuration) |
| Applicazione di destinazione distribuita | Blocco predefinito: [SaaS: configurazione SSO federato](#saas-federated-sso-configuration) |

### <a name="steps"></a>Passi

| Passaggio | Risorse |
| --- | --- |
| Andare a pannello di applicazioni tooEnterprise nel portale di gestione di Azure AD | [Portale di gestione di Azure AD: Applicazioni aziendali](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/AllApps/menuId/) |
| Configurare l'applicazione dai prerequisiti con self-service | [Novità della gestione delle applicazioni aziendali in Azure Active Directory: Configurare l'accesso alle applicazioni self-service](active-directory-enterprise-apps-whats-new-azure-portal.md#configure-self-service-application-access) |
| Accedere come portale delle App toomy lavoro informazioni hello | http://myapps.microsoft.com |
| Si noti "+ Aggiungi app" pulsante op della pagina hello. Utilizzarlo tooget accesso toohello app |  |

### <a name="considerations"></a>Considerazioni

applicazioni di Hello scelte potrebbe essere presente il provisioning di requisiti, in modo da passare immediatamente toohello app può causare alcuni errori. Se un'applicazione hello scelta supporta il provisioning con azure ad e viene configurato, è possibile utilizzare come un opportunità tooshow hello intero flusso di lavoro tooend di fine. Vedere hello fondamentale per [configurazione di SSO federato SaaS](#saas-federated-sso-configuration) per ulteriori informazioni

## <a name="self-service-password-reset"></a>Reimpostazione della password self-service

TooComplete tempo approssimativo: 15 minuti

### <a name="pre-requisites"></a>Prerequisiti

| Prerequisito. | Risorse |
| --- | --- |
| Abilitare la gestione delle password self-service nel tenant. | [Reimpostazione delle password in Azure Active Directory per gli amministratori IT](active-directory-passwords.md) |
| Abilitare le password toomanage writeback password locale. Si noti che questa operazione richiede versioni specifiche di Azure AD Connect | [Prerequisiti per il writeback delle password](active-directory-passwords-writeback.md) |
| Identificare gli utenti di prova hello che utilizzano questa funzionalità, assicurarsi che siano membri di un gruppo di sicurezza. gli utenti di Hello devono essere capacità di hello showcase toofully non amministratori | [Personalizzare: Gestione delle Password AD Azure: reset toopassword limita l'accesso](active-directory-passwords-writeback.md) |


### <a name="steps"></a>Passi

| Passaggio | Risorse |
| --- | --- |
| Passare AD tooAzure portale di gestione: la reimpostazione della Password | [Portale di gestione di Azure AD: Reimpostazione delle password](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset) |
| Determinare i criteri di reimpostazione password hello. Per motivi di prova, è possibile utilizzare telefonata e domande e risposte. È consigliabile tooenable registrazione toobe necessari nella tooaccess Pannello di accesso |  |
| Disconnettersi e accedere di nuovo come Information Worker |  |
| Fornire i dati di reimpostazione della Password Self-Service hello come configurato per il passaggio 2 | http://aka.ms/ssprsetup |
| Browser hello Chiudi |  |
| Avvio del processo di accesso hello hello information worker utilizzata nel passaggio 4 |  |
| Reimpostare la password di hello | [Aggiornare la password: Reimpostare la password](active-directory-passwords-update-your-own-password.md) |
| Provare ad accedere con la nuova password tooAzure Active Directory, nonché le risorse locali tooon |  |

### <a name="considerations"></a>Considerazioni

1. Se l'aggiornamento hello Azure AD Connect verrà toocause le forze di attrito, è consigliabile utilizzarlo con gli account cloud o renderlo una demo in un ambiente separato
2. gli amministratori di Hello dispongono di un criterio diverso utilizzando e salve password dell'account tooreset hello potrebbe alterino hello PoC confusione. Assicurarsi di utilizzare le operazioni di reimpostazione un utente normale account tootest hello


## <a name="azure-multi-factor-authentication-with-phone-calls"></a>Azure Multi-Factor Authentication con chiamate telefoniche

TooComplete tempo approssimativo: 10 minuti

### <a name="pre-requisites"></a>Prerequisiti

| Prerequisito. | Risorse |
| --- | --- |
| Identificare gli utenti del modello di verifica che useranno MFA  |  |
| Telefono con buona ricezione per la richiesta di connessione MFA  | [Informazioni su Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) |

### <a name="steps"></a>Passi

| Passaggio | Risorse |
| --- | --- |
| Passare troppo blade "Utenti e gruppi" nel portale di gestione di Azure AD | [Portale di gestione di Azure AD: Utenti e gruppi](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Overview/menuId/) |
| Scegliere il pannello "Tutti gli utenti" |  |
| Nella parte superiore di hello barra pulsante "Multi-Factor Authentication" Scegli | URL diretto per il portale di Azure MFA: https://aka.ms/mfaportal |
| Nelle impostazioni di "User" hello, selezionare gli utenti di prova hello e attivarli per l'autenticazione a più fattori | [Stati utente in Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-user-states.md) |
| Account di accesso come utente di prova hello e procedura per il processo di prova hello  |  |

### <a name="considerations"></a>Considerazioni

1. Hello PoC passaggi in questo blocco di compilazione in modo esplicito l'impostazione di autenticazione a più fattori per un utente in tutti gli account di accesso. Sono disponibili altri strumenti, ad esempio l'accesso condizionale e la protezione dell'identità, che usano MFA in scenari più specifici. Si tratterà di un elemento tooconsider durante lo spostamento da tooproduction di prova.
2. passaggi di prova Hello in questo blocco di compilazione in modo esplicito utilizza chiamate telefoniche come metodo di autenticazione a più fattori per expedience hello. Quando si passa da tooproduction di prova, è consigliabile utilizzare le applicazioni, ad esempio hello [Microsoft Authenticator](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) come il secondo fattore quando possibile.
Altre informazioni: documento [DRAFT NIST Special Publication 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html)

## <a name="mfa-conditional-access-for-saas-applications"></a>Accesso condizionale MFA per applicazioni SaaS

TooComplete tempo approssimativo: 10 minuti

### <a name="pre-requisites"></a>Prerequisiti

| Prerequisito. | Risorse |
| --- | --- |
| Identificare i criteri hello tootarget agli utenti di prova. Questi utenti devono essere in un criterio di accesso condizionale di sicurezza gruppo tooscope hello | [SaaS: configurazione SSO federato](#saas-federated-sso-configuration) |
| L'applicazione SaaS è già stata configurata |  |
| Gli utenti di prova sono già stati assegnati toohello applicazione |  |
| Utente di prova toohello le credenziali sono disponibili |  |
| L'utente del modello di verifica è registrato per MFA. Uso di un telefono con buona ricezione | http://aka.ms/ssprsetup |
| Dispositivo di rete interna hello. Indirizzo IP configurato nell'intervallo di indirizzi interno hello | Individuare l'indirizzo IP: https://www.bing.com/search?q=what%27s+my+ip |
| Dispositivo di rete esterna di hello (può essere un telefono con la rete mobile del vettore hello) |  |

### <a name="steps"></a>Passi

| Passaggio | Risorse |
| --- | --- |
| Vai AD tooAzure portale di gestione: pannello di accesso condizionale | [Portale di gestione di Azure AD: Accesso condizionale](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies) |
| Creare i criteri di accesso condizionale:<br/>- Individuare gli utenti del modello di verifica in "Utenti e gruppi"<br/>- Individuare l'applicazione del modello di verifica in "App cloud"<br/>- Individuare tutte le posizioni tranne quelle attendibili in "Condizioni" -> "Località" **Nota:** gli indirizzi IP attendibili sono configurati nel [portale di MFA](https://account.activedirectory.windowsazure.com/UserManagement/MfaSettings.aspx)<br/>- Richiedere l'autenticazione a più fattori nel pannello "Concedi" | [Introduzione all'accesso condizionale in Azure Active Directory: Procedura di configurazione dei criteri](active-directory-conditional-access-azure-portal-get-started.md#policy-configuration-steps) |
| Accedere all'applicazione dall'interno della rete aziendale | [Iniziare con l'accesso condizionale in Azure Active Directory: hello criteri di test](active-directory-conditional-access-azure-portal-get-started.md#testing-the-policy) |
| Accedere all'applicazione dalla rete pubblica | [Iniziare con l'accesso condizionale in Azure Active Directory: hello criteri di test](active-directory-conditional-access-azure-portal-get-started.md#testing-the-policy) |

### <a name="considerations"></a>Considerazioni

Se si utilizza la federazione, è possibile utilizzare hello toocommunicate di hello locali il Provider di identità (IdP) interno/esterno dello stato di rete aziendale con le attestazioni. È possibile utilizzare questa tecnica senza elenco di hello toomanage di indirizzi IP che potrebbe essere tooassess complesse e gestire in organizzazioni di grandi dimensioni. In dal programma di installazione, è necessario account per hello "roaming" scenario (un accesso utente dalla rete interna hello e commutatori connessi percorsi, ad esempio un bar) e assicurarsi di che comprendere le implicazioni di hello. Altre informazioni: [Protezione delle risorse cloud con Azure Multi-Factor Authentication e AD FS: Indirizzi IP attendibili per utenti federati](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md#trusted-ips-for-federated-users)

## <a name="privileged-identity-management-pim"></a>Privileged Identity Management (PIM)

TooComplete tempo approssimativo: 15 minuti

### <a name="pre-requisites"></a>Prerequisiti

| Prerequisito. | Risorse |
| --- | --- |
| Identificare salve globale che farà parte di hello POC per PIM | [Iniziare a usare Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md) |
| Identificare salve globale che diventerà hello amministratore della sicurezza | [Iniziare a usare Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)<br/> [Ruolo amministrativo differente in Azure AD PIM](active-directory-privileged-identity-management-roles.md) |
| Facoltativo: Verificare se gli amministratori globali hello posta elettronica accedere tooexercise notifiche di posta elettronica in PIM | [Che cos'è Azure AD Privileged Identity Management?: configurare le impostazioni di attivazione di hello ruolo](active-directory-privileged-identity-management-configure.md#configure-the-role-activation-settings)


### <a name="steps"></a>Passi

| Passaggio | Risorse |
| --- | --- |
| Toohttps://portal.azure.com account di accesso come amministratore globale (GA) e il pannello PIM hello bootstrap. Hello amministratore globale che esegue questo passaggio viene effettuato il seeding come amministratore della sicurezza hello.  In questo esempio sarà l'attore GA1 | [Utilizzando la procedura guidata protezione hello in Azure AD Privileged Identity Management](active-directory-privileged-identity-management-security-wizard.md) |
| Identificare salve globale e spostarli da tooeligible permanente. Deve essere un amministratore separato da hello quello utilizzato nel passaggio 1 per maggiore chiarezza. In questo esempio sarà l'attore GA2 | [Azure AD Privileged Identity Management: Come tooadd o rimuovere un ruolo utente](active-directory-privileged-identity-management-how-to-add-role-to-user.md)<br/>[Che cos'è Azure AD Privileged Identity Management?: configurare le impostazioni di attivazione di hello ruolo](active-directory-privileged-identity-management-configure.md#configure-the-role-activation-settings)  |
| A questo punto, accedere come GA2 toohttps://portal.azure.com e provare a modificare "Impostazioni utente". Come si può vedere, alcune opzioni sono disattivate. | |
| In una nuova scheda in hello stessa sessione come passaggio 3, passare a questo punto toohttps://portal.azure.com e aggiungere hello PIM pannello toohello dashboard. | [Come tooactivate o disattivare i ruoli in Azure AD Privileged Identity Management: aggiungere un'applicazione hello Privileged Identity Management](active-directory-privileged-identity-management-how-to-activate-role.md#add-the-privileged-identity-management-application) |
| Ruolo di amministratore globale di richiesta di attivazione toohello | [Come tooactivate o disattivare i ruoli in Azure AD Privileged Identity Management: attivare un ruolo](active-directory-privileged-identity-management-how-to-activate-role.md#activate-a-role) |
| Si noti che se GA2 non si è mai registrato per l'autenticazione a più fattori, sarà necessaria la registrazione per Azure MFA |  |
| Tornare indietro toohello scheda originale nel passaggio 3 e fare clic sul pulsante Aggiorna hello nel browser hello. Si noti che ora si hanno accesso toochange "Le impostazioni utente" | |
| Facoltativamente, se gli amministratori globali dispongono di posta elettronica attivata, è possibile controllare GA1 e della GA2 cartella Posta in arrivo e vedere notifica hello del ruolo di hello in corso l'attivazione |  |
| 8 controllare la cronologia di controllo hello e osservare hello report tooconfirm hello l'elevazione dei privilegi di GA2 viene visualizzato. | [Che cos'è Azure AD Privileged Identity Management?: Verificare l'attività del ruolo](active-directory-privileged-identity-management-configure.md#review-role-activity) |

### <a name="considerations"></a>Considerazioni

Questa funzionalità fa parte di Azure AD Premium P2 e/o EMS E5

## <a name="discovering-risk-events"></a>Rilevare eventi di rischio

TooComplete tempo approssimativo: 20 minuti

### <a name="pre-requisites"></a>Prerequisiti

| Prerequisito. | Risorse |
| --- | --- |
| Dispositivo con Tor Browser scaricato e installato | [Download di Tor Browser](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Account di accesso di accesso tooPOC utente toodo hello | [Studio di Azure Active Directory Identity Protection](active-directory-identityprotection-playbook.md) |

### <a name="steps"></a>Passi

| Passaggio | Risorse |
| --- | --- |
| Aprire Tor Browser | [Download di Tor Browser](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Accedi toohttps://myapps.microsoft.com con hello account utente di prova | [Studio sulla protezione delle identità di Azure Active Directory: Simulazione sugli eventi di rischio](active-directory-identityprotection-playbook.md#simulating-risk-events) |
| Attendere 5-7 minuti |  |
| Accedere come un amministratore globale di toohttps://portal.azure.com e aprire il pannello di protezione dell'identità hello | https://aka.ms/aadipgetstarted |
| Pannello eventi di rischio hello aperto. Dovrebbe apparire una voce sotto "Accessi da indirizzi IP anonimi"  | [Studio sulla protezione delle identità di Azure Active Directory: Simulazione sugli eventi di rischio](active-directory-identityprotection-playbook.md#simulating-risk-events) |

### <a name="considerations"></a>Considerazioni

Questa funzionalità fa parte di Azure AD Premium P2 e/o EMS E5

## <a name="deploying-sign-in-risk-policies"></a>Distribuire criteri di rischio di accesso

TooComplete tempo approssimativo: 10 minuti

### <a name="pre-requisites"></a>Prerequisiti

| Prerequisito. | Risorse |
| --- | --- |
| Dispositivo con Tor Browser scaricato e installato | [Download di Tor Browser](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Accesso come un prova toodo hello accesso come utente test |  |
| L'utente del modello di verifica è registrato per MFA. Verificare che toouse un telefono con buona ricezione | Blocco predefinito: [Azure Multi-Factor Authentication con chiamate telefoniche](#azure-multi-factor-authentication-with-phone-calls) |


### <a name="steps"></a>Passi

| Passaggio | Risorse |
| --- | --- |
| Accedere come un amministratore globale di toohttps://portal.azure.com e aprire il pannello di protezione dell'identità hello | https://aka.ms/aadipgetstarted |
| Abilitare un criterio di rischio di accesso come segue:<br/>- Assegnato a: utente del modello di verifica<br/>- Condizioni: rischio di accesso medio o alto (l'accesso da una posizione anonima viene considerato come livello di rischio medio)<br/>- Controlli: richiesto MFA | [Studio di Azure Active Directory Identity Protection: Rischio di accesso](active-directory-identityprotection-playbook.md#sign-in-risk) |
| Aprire Tor Browser | [Download di Tor Browser](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Accedi toohttps://myapps.microsoft.com con hello account utente di prova |  |
| Hello avviso richiesta di autenticazione a più fattori | [Esperienze di accesso con Azure AD Identity Protection: Ripristino di un accesso rischioso](active-directory-identityprotection-flows.md#risky-sign-in-recovery)

### <a name="considerations"></a>Considerazioni

Questa funzionalità fa parte di Azure AD Premium P2 e/o EMS E5. informazioni sugli eventi di rischio, visitare toolearn: [gli eventi di rischio di Azure Active Directory](active-directory-reporting-risk-events.md)

## <a name="configuring-certificate-based-authentication"></a>Configurare l'autenticazione basata su certificati

Toocomplete tempo approssimativo: 20 minuti

### <a name="pre-requisites"></a>Prerequisiti

| Prerequisito. | Risorse |
| --- | --- |
| Dispositivo con certificato utente di cui è stato eseguito il provisioning (Windows, iOS o Android) dall'infrastruttura a chiave pubblica aziendale | [Distribuire i certificati utente](https://msdn.microsoft.com/library/cc770857.aspx) |
| Dominio di Azure AD federato con AD FS | [Azure AD Connect e federazione](./connect/active-directory-aadconnectfed-whatis.md)<br/>[Informazioni generali sui Servizi certificati di Active Directory](https://technet.microsoft.com/library/hh831740.aspx)|
| Per i dispositivi iOS l'app Microsoft Authenticator deve essere installata | [Introduzione a app Microsoft Authenticator hello](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) |

### <a name="steps"></a>Passi

| Passaggio | Risorse |
| --- | --- |
| Abilitare l'autenticazione del certificato in AD FS | [Configurare i criteri di autenticazione: l'autenticazione principale con tooconfigure a livello globale in Windows Server 2012 R2](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-authentication-policies#to-configure-primary-authentication-globally-in-windows-server-2012-r2) |
| Facoltativo: abilitare l'autenticazione del certificato in Azure AD per i client di Exchange Active Sync | [Introduzione all'autenticazione basata su certificati di Azure Active Directory](active-directory-certificate-based-authentication-get-started.md) |
| Passare tooAccess pannello e l'autenticazione tramite certificato utente | https://myapps.microsoft.com |

### <a name="considerations"></a>Considerazioni

informazioni su aspetti della distribuzione, visitare toolearn: [ADFS: l'autenticazione del certificato con Azure AD & Office 365](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/)



> [!NOTE]
> Il possesso del certificato utente deve essere protetto, gestendo i dispositivi o con PIN in caso di smart card.



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]
