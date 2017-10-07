---
title: Indice per la gestione delle applicazioni in Azure Active Directory aaaArticle | Microsoft Azure
description: "Informazioni su come toocustomize hello data di scadenza dei certificati di federazione e utilizzo dei certificati che toorenew scadrà a breve."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 5321b8e4-2afa-4dfe-8d53-4add7abb5ec8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: f8a584baa94dc50e279899074f50160978256559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="article-index-for-application-management-in-azure-active-directory"></a>Indice di articoli per la gestione di applicazioni in Azure Active Directory
Questa pagina fornisce un elenco completo di ogni documento scritto su hello varie funzionalità di applicazione in Azure Active Directory (Azure AD).

È un'area di funzionalità principale tooeach breve introduzione, nonché informazioni aggiuntive su quali tooread articoli a seconda di quali informazioni si sta cercando.

## <a name="overview-articles"></a>Articoli generali
articoli Hello seguenti sono valide punti di partenza per gli utenti che desiderano semplicemente una breve descrizione della funzionalità di gestione di applicazioni Azure AD.

| Guida agli articoli |  |
|:---:| --- |
| Un'introduzione toohello applicazione i problemi di gestione di Azure AD è stato risolto |[Gestione di applicazioni con Azure Active Directory](active-directory-enable-sso-scenario.md) |
| Cenni preliminari hello diverse caratteristiche disponibili in Azure AD correlati tooenabling accesso single sign-on, la definizione di chi ha accesso tooapps e come utenti avviano le app |[Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md) |
| Esaminare hello diversi passaggi per l'integrazione di applicazioni in Azure AD |[Integrazione di Azure Active Directory con applicazioni](active-directory-integrating-applications-getting-started.md)<br /><br />[Abilitazione di Single Sign-On tooSaaS App](active-directory-sso-integrate-saas-apps.md)<br /><br />[La gestione di accesso tooApps](active-directory-managing-access-to-apps.md) |
| Spiegazione tecnica del modo in cui le app vengono rappresentate in Azure AD. |[Come e perché le applicazioni vengono aggiunte AD tooAzure](active-directory-how-applications-are-added.md) |

## <a name="troubleshooting-articles"></a>Articoli sulla risoluzione dei problemi
In questa sezione consente di accedere rapidamente toorelevant guide di risoluzione dei problemi. Ulteriori informazioni su ogni area funzionale sono reperibile nel resto di hello di questa pagina.

| Area di funzionalità |  |
|:---:| --- |
| Single Sign-On federato |[Risoluzione dei problemi dell'accesso Single Sign-On basato su SAML](active-directory-saml-debugging.md) |
| Single Sign-On basato su password |[Risoluzione dei problemi di estensione del Pannello di accesso hello per Internet Explorer](active-directory-saas-ie-troubleshooting.md) |
| Proxy dell'applicazione |[Guida alla risoluzione dei problemi del proxy di applicazione](active-directory-application-proxy-troubleshoot.md) |
| Single Sign-On tra AD locale e Azure AD |[Risoluzione dei problemi di sincronizzazione delle password](connect/active-directory-aadconnectsync-implement-password-synchronization.md#troubleshoot-password-synchronization)<br /><br />[Risoluzione dei problemi di writeback delle password](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) |
| Appartenenze dinamiche a gruppi |[Risoluzione dei problemi di appartenenza dinamica ai gruppi](active-directory-accessmanagement-troubleshooting.md) |

## <a name="single-sign-on-sso"></a>Accesso Single Sign-On (SSO)
### <a name="federated-single-sign-on-sign-into-many-apps-using-one-identity"></a>Single Sign-On federato: accesso a più app mediante una sola identità
Accesso Single sign-on consente agli utenti tooaccess un'ampia gamma di applicazioni e servizi con un solo insieme di credenziali. La federazione è un metodo che consente di abilitare l'accesso Single Sign-On. Quando gli utenti tentano toosign federato ad App, che verrà visualizzato ufficiale nella pagina di accesso tootheir reindirizzato organizzazione eseguito il rendering da Azure Active Directory e sono quindi app toohello indietro reindirizzato alla riuscita dell'autenticazione.

| Guida agli articoli |  |
|:---:| --- |
| Toofederation un'introduzione e altri tipi di accesso |[Single Sign-On con Azure AD](active-directory-appssoaccess-whatis.md) |
| Migliaia di app SaaS preintegrate con Azure AD con procedure di configurazione semplificate per l'accesso Single Sign-On. |[Introduzione a una raccolta di applicazioni Azure AD hello](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery)<br /><br />[Elenco completo di app preintegrate che supportano la federazione](http://aka.ms/aadfederatedapps)<br /><br />[Come tooAdd dell'App toohello raccolta di App di Azure AD](active-directory-app-gallery-listing.md) |
| Più di 150 esercitazioni di app in modalità tooconfigure single sign-on per App, ad esempio [Salesforce](active-directory-saas-salesforce-tutorial.md), [ServiceNow](active-directory-saas-servicenow-tutorial.md), [Google Apps](active-directory-saas-google-apps-tutorial.md), [Workday](active-directory-saas-workday-tutorial.md)e molto altro ancora |[Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md) |
| Come toomanually configurare e personalizzare la configurazione di single sign-on |[Come tooConfigure tooApps federata Single Sign-On che non sono presenti hello raccolta applicazioni di Azure Active Directory](active-directory-saas-custom-apps.md)<br /><br />[Come emettere attestazioni tooCustomize in hello Token SAML per le app Pre-Integrated](active-directory-saml-claims-customization.md) |
| Risoluzione dei problemi di Guida per le applicazioni federate che utilizzano il protocollo SAML hello |[Risoluzione dei problemi dell'accesso Single Sign-On basato su SAML](active-directory-saml-debugging.md) |
| Come tooconfigure data di scadenza del certificato dell'applicazione e in che modo toorenew i certificati |[Gestione di certificati per Single Sign-On federato in Azure Active Directory](active-directory-sso-certs.md) |

Single sign-on federato è disponibile per tutte le edizioni di Azure Active Directory per le applicazioni tooten per utente. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) supporta un numero illimitato di applicazioni. Se l'organizzazione ha [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) o [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), è quindi possibile [utilizzare gruppi di applicazioni di toofederated accesso tooassign](#managing-access-to-applications).

### <a name="password-based-single-sign-on-account-sharing-and-sso-for-non-federated-apps"></a>Accesso Single Sign-On basato su password: condivisione di account e accesso Single Sign-On per app non federate
tooenable single sign-on tooapplications che non supportano la federazione, Azure AD offre password le funzionalità di gestione che è possono archiviare in modo sicuro le password tooSaaS App e accedere automaticamente gli utenti a tali app. È possibile distribuire con facilità le credenziali per gli account appena creati e condividere account del team con più persone. Gli utenti non devono necessariamente tooknow hello credenziali toohello gli account assegnati per l'accesso.

| Guida agli articoli |  |
|:---:| --- |
| Un funzionamento SSO basato su password toohow di introduzione e una breve panoramica tecnica |[Single Sign-On basato su password con Azure AD](active-directory-appssoaccess-whatis.md#password-based-single-sign-on) |
| Un riepilogo degli scenari di hello correlati tooaccount condivisione e come questi problemi vengono risolti da Azure AD |[Condivisione di account con Azure AD](active-directory-sharing-accounts.md) |
| Modificare automaticamente la password di hello per alcune applicazioni a intervalli regolari |[Rollover automatizzato delle password (anteprima)](https://blogs.technet.microsoft.com/enterprisemobility/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview/) |
| Distribuzione e risoluzione dei problemi di guide per la versione di Internet Explorer hello di hello estensione Gestione password di Azure AD |[Come tooDeploy hello estensione del Pannello di accesso per Internet Explorer utilizzando criteri di gruppo](active-directory-saas-ie-group-policy.md)<br /><br />[Risoluzione dei problemi di estensione del Pannello di accesso hello per Internet Explorer](active-directory-saas-ie-troubleshooting.md) |

Basato su password single sign-on è disponibile per tutte le edizioni di Azure Active Directory per le applicazioni tooten per utente. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) supporta un numero illimitato di applicazioni. Se l'organizzazione ha [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) o [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), è quindi possibile [utilizzare gruppi tooassign accesso tooapplications](#managing-access-to-applications). Il rollover automatizzato delle password è una funzionalità di [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) .

### <a name="app-proxy-single-sign-on-and-remote-access-tooon-premises-applications"></a>App Proxy: Le applicazioni locali tooon Single sign-on e accesso remoto
Se si dispone di applicazioni nella rete privata che devono toobe accedono gli utenti e dispositivi esterni hello rete, è possibile utilizzare le app toothose di accesso remoto sicuro tooenable Proxy dell'applicazione AD Azure.

| Guida agli articoli |  |
|:---:| --- |
| Panoramica del proxy di applicazione di Azure AD e del suo funzionamento. |[Fornisce l'accesso remoto sicuro applicazioni tooon locali](active-directory-application-proxy-get-started.md) |
| Esercitazioni sulla procedura tooconfigure Proxy dell'applicazione e in che modo toopublish la prima app |[Come tooSet Proxy App di Azure AD](active-directory-application-proxy-enable.md)<br /><br />[Come installare tooSilently hello connettore del Proxy di applicazione](active-directory-application-proxy-silent-installation.md)<br /><br />[Come tooPublish applicazioni mediante il Proxy di applicazione](active-directory-application-proxy-publish.md)<br /><br />[Come tooUse proprio nome di dominio](active-directory-application-proxy-custom-domains.md) |
| Come tooenable single sign-on e condizionale accesso per le applicazioni pubblicate con il Proxy di applicazione |[Accesso Single Sign-On con il proxy di applicazione](active-directory-application-proxy-sso-using-kcd.md)<br /><br />[Accesso condizionale e proxy di applicazione](active-directory-application-proxy-conditional-access.md) |
| Informazioni aggiuntive su come toouse Proxy dell'applicazione per i seguenti scenari hello |[Come le applicazioni Client Native tooSupport](active-directory-application-proxy-native-client.md)<br /><br />[Come tooSupport Claims-Aware Applications](active-directory-application-proxy-claims-aware-apps.md)<br /><br />[Modalità di pubblicazione di applicazioni tooSupport su percorsi e reti Separate:](active-directory-application-proxy-connectors.md) |
| Guida alla risoluzione dei problemi relativi al proxy di applicazione. |[Guida alla risoluzione dei problemi del proxy di applicazione](active-directory-application-proxy-troubleshoot.md) |

Proxy dell'applicazione è disponibile per tutte le edizioni di Azure Active Directory per le applicazioni tooten per utente. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) supporta un numero illimitato di applicazioni. Se l'organizzazione ha [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) o [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), è quindi possibile [utilizzare gruppi tooassign accesso tooapplications](#managing-access-to-applications).

Può anche essere interessante [servizi di dominio Active Directory di Azure](../active-directory-domain-services/active-directory-ds-overview.md), che consente di toomigrate il tooAzure applicazioni locali e al contempo soddisfano ancora identità hello necessita di tali applicazioni.

### <a name="enabling-single-sign-on-between-azure-ad-and-on-premises-ad"></a>Abilitazione dell'accesso Single Sign-On tra Azure AD e l'istanza locale di AD
Se l'organizzazione gestisce un Windows Server Active Directory locale con Azure Active Directory nel cloud hello, quindi è probabile che si preferisca tooenable single sign-on tra questi due sistemi. Azure AD Connect (strumento hello che integra insieme questi due sistemi) offre più opzioni per l'impostazione di single sign-on: stabilire la federazione con ADFS o un altro provider di federazione o abilitare la sincronizzazione delle password.

| Guida agli articoli |  |
|:---:| --- |
| Cenni preliminari su hello single sign-on le opzioni disponibili in Azure AD Connect, nonché informazioni sulla gestione di ambienti ibridi |[Opzioni di accesso utente di Azure AD Connect](active-directory-aadconnect-user-signin.md) |
| Indicazioni generali per la gestione di ambienti con Active Directory locale e Azure Active Directory. |[Considerazioni di progettazione dell'identità ibrida di Azure Active Directory](active-directory-hybrid-identity-design-considerations-overview.md)<br /><br />[Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md) |
| Indicazioni su come utilizzare la sincronizzazione delle Password tooenable SSO |[Implementare la sincronizzazione password con Azure AD Connect](active-directory-aadconnectsync-implement-password-synchronization.md)<br /><br />[Risolvere i problemi di sincronizzazione delle password](https://support.microsoft.com/en-us/kb/2855271) |
| Informazioni sull'uso di writeback delle Password tooenable SSO |[Introduzione alla gestione delle password in Azure AD](active-directory-passwords-getting-started.md)<br /><br />[Risolvere i problemi relativi al writeback delle password](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) |
| Informazioni sull'uso di terze parti identity provider tooenable SSO |[Elenco di tooEnable compatibile terze parti Identity provider che è possibile utilizzare Single Sign-On](https://aka.ms/ssoproviders) |
| Come gli utenti di Windows 10 potranno sfruttare i vantaggi di hello di single sign-on tramite l'aggiunta di Azure AD |[Estensione delle funzionalità Cloud tooWindows 10 dispositivi tramite Azure Active Directory Join](active-directory-azureadjoin-overview.md) |

Azure AD Connect è disponibile per [tutte le edizioni di Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/). Reimpostazione password self-service di Azure AD è disponibile per [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) e [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/). Password con Writeback tooon locale AD è un [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) funzionalità.

### <a name="conditional-access-enforce-additional-security-requirements-for-high-risk-apps"></a>Accesso condizionale: applicare requisiti di sicurezza aggiuntivi per app a rischio elevato
Dopo aver impostato le risorse e le applicazioni single sign-on tooyour, è possibile quindi proteggere ulteriormente le applicazioni sensibili applicando i requisiti di sicurezza specifico in ogni app toothat Accedi. Ad esempio, è possibile utilizzare Azure AD toodemand che tutte le app di particolare tooa access richiedono sempre l'autenticazione a più fattori, indipendentemente dal fatto che app supporta o meno natura tale funzionalità. Un altro esempio comune di accesso condizionale è toorequire che gli utenti in toohello connesso organizzazione attendibile rete in ordine tooaccess un'applicazione particolarmente sensibile.

| Guida agli articoli |  |
|:---:| --- |
| Una funzionalità di accesso condizionale toohello introduzione offerti su Azure AD, Office 365 e Intune |[Gestione dei rischi con l'accesso condizionale](active-directory-conditional-access.md) |
| Modalità di accesso condizionale tooenable per hello seguenti tipi di risorse |[Accesso condizionale per app SaaS](active-directory-conditional-access-azuread-connected-apps.md)<br /><br />[Accesso condizionale per i servizi di Office 365](active-directory-conditional-access-device-policies.md)<br /><br />[Accesso condizionale per applicazioni locali](active-directory-conditional-access.md)<br /><br />[Accesso condizionale per applicazioni locali pubblicate tramite proxy di app di Azure AD](active-directory-application-proxy-conditional-access.md) |

| Come tooregister dispositivi con Azure Active Directory in ordine tooenable criteri di accesso condizionale basato su dispositivi | [Cenni preliminari sulla registrazione del dispositivo Azure Active Directory](active-directory-conditional-access-device-registration-overview.md)<br /><br />[Come tooEnable registrazione automatica dei dispositivi per i dispositivi Windows aggiunti a un dominio](active-directory-conditional-access-automatic-device-registration.md)<br />- [Procedura per dispositivi Windows 8.1](active-directory-conditional-access-automatic-device-registration-setup.md)<br />- [Procedura per dispositivi Windows 7](active-directory-conditional-access-automatic-device-registration-setup.md) |

| Come toouse hello app Authenticator di Microsoft per la verifica | [Microsoft Authenticator](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) |

L'accesso condizionale è una funzionalità di [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) .

## <a name="apps--azure-ad"></a>App e Azure AD
### <a name="cloud-app-discovery-find-which-saas-apps-are-being-used-in-your-organization"></a>Cloud App Discovery: individuare le app SaaS usate nell'organizzazione
Cloud App Discovery consente ai reparti IT informazioni su quali App SaaS vengono utilizzate nell'intera organizzazione hello. È possibile misurare l'utilizzo delle app e popolarità in modo che non è possibile determinare quali App trarranno vantaggio hello più vengano portati sotto il controllo IT e viene integrato con Azure AD.

| Guida agli articoli |  |
|:---:| --- |
| Panoramica generale del funzionamento. |[Ricerca di applicazioni cloud non autorizzate con Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md) |
| Un approfondimento su come funziona, con le risposte tooquestions su privacy |[Considerazioni sulla sicurezza e sulla privacy](active-directory-cloudappdiscovery-security-and-privacy-considerations.md) |
| Domande frequenti |[Domande frequenti per Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx) |
| Esercitazioni per la distribuzione di Cloud App Discovery. |[Guida alla distribuzione di Criteri di gruppo](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)<br /><br />[Guida alla distribuzione di System Center](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)<br /><br />[Installazione nei server proxy con porte personalizzate](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md) |
| Hello modificare il registro per l'agente di Cloud App Discovery toohello aggiornamenti |[Log delle modifiche](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx) |

Cloud App Discovery è una funzionalità di [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) .

### <a name="automatically-provision-and-deprovision-user-accounts-in-saas-apps"></a>Provisioning e deprovisioning automatici degli account utente nelle app SaaS
Automatizzare la creazione di hello, manutenzione e la rimozione delle identità nelle applicazioni SaaS, ad esempio Dropbox, Salesforce, ServiceNow e altro ancora. Corrispondenza e la sincronizzazione delle identità esistenti tra Azure AD e le app SaaS e controllare l'accesso disabilitando automaticamente gli account quando gli utenti lasciano l'organizzazione hello.

| Guida agli articoli |  |
|:---:| --- |
| Informazioni su come funziona e trovare le risposte alle domande toocommon |[Automatizzare il Provisioning dell'utente e Deprovisioning tooSaaS App](active-directory-saas-app-provisioning.md) |
| Configurare il mapping delle informazioni tra Azure AD e l'app SaaS. |[Personalizzazione dei mapping degli attributi](active-directory-saas-customizing-attribute-mappings.md)<br><br>[Scrittura di espressioni per i mapping degli attributi](active-directory-saas-writing-expressions-for-attribute-mappings.md) |
| Come tooenable automatizzare provisioning tooany app che supporta il protocollo SCIM hello |[Configurare il Provisioning utente automatico tooany SCIM-Enabled App](active-directory-scim-provisioning.md) |
| Come tooreport in e risolvere i problemi di provisioning utente |[Creazione di report sul provisioning utenti automatico](active-directory-saas-provisioning-reporting.md)<br><br>[Notifiche relative al provisioning](active-directory-saas-account-provisioning-notifications.md)<br><br>[Risoluzione dei problemi relativi al provisioning utenti](active-directory-application-provisioning-content-map.md) |
| Limitare l'accesso dell'applicazione tooan provisioning in base ai valori di attributo |[Filtri per la definizione dell'ambito](active-directory-saas-scoping-filters.md) |

Il provisioning utenti automatizzato è disponibile per tutte le edizioni di Azure Active Directory per le applicazioni tooten per utente. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) supporta un numero illimitato di applicazioni. Se l'organizzazione ha [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) o [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), è quindi possibile [toomanage gruppi gli utenti a cui ottengano il provisioning di utilizzare](#managing-access-to-applications).

### <a name="building-applications-that-integrate-with-azure-ad"></a>Sviluppo di applicazioni integrate con Azure AD
Se l'organizzazione è lo sviluppo di mantenere le applicazioni line-of-business (LoB) o se si è un sviluppatore di app con i clienti che usano Azure Active Directory, hello seguenti esercitazioni consentono di integrare le applicazioni con Azure AD.

| Guida agli articoli |  |
|:---:| --- |
| Indicazioni per professionisti IT e sviluppatori di applicazioni per l'integrazione di app con Azure AD. |[Guida Hello professionista IT per lo sviluppo di applicazioni per Azure AD](active-directory-applications-guiding-developers-for-lob-applications.md)<br /><br />[Guida per gli sviluppatori di Hello per Azure Active Directory](active-directory-developers-guide.md) |
| Come i fornitori tooapplication possono aggiungere i relativi toohello App raccolta di App di Azure AD |[Elenca l'applicazione nella raccolta di Azure Active Directory dell'applicazione hello](active-directory-app-gallery-listing.md) |
| Modalità di accesso delle applicazioni toodeveloped tramite Azure Active Directory toomanage |[Modalità assegnazione utente per le applicazioni sviluppate tooEnable](active-directory-applications-guiding-developers-requiring-user-assignment.md)<br /><br />[L'assegnazione di utenti tooyour App](active-directory-applications-guiding-developers-assigning-users.md)<br /><br />[Gruppo di assegnazione tooyour App](active-directory-applications-guiding-developers-assigning-groups.md) |

Se si sta sviluppando applicazioni per consumatori, potrebbe essere interessati all'uso [Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) in modo che non si dispone di propri toomanage di sistema di identità toodevelop gli utenti. [Altre informazioni](../active-directory-b2c/active-directory-b2c-overview.md)

## <a name="managing-access-tooapplications"></a>La gestione di accesso tooApplications
### <a name="using-groups-and-self-service-toomanage-who-has-access-toowhich-apps"></a>Utilizzo di gruppi e toomanage self-service che dispone di accesso toowhich App
toohelp per gestire utenti che dovrebbero avere accesso alle risorse di toowhich, Azure Active Directory consente tooset assegnazioni e le autorizzazioni a livello di scalabilità mediante gruppi. IT può scegliere tooenable funzionalità self-service in modo che gli utenti possono semplicemente richiedere l'autorizzazione in qualsiasi momento.

| Guida agli articoli |  |
|:---:| --- |
| Panoramica delle funzionalità di gestione dell'accesso di Azure AD. |[Introduzione tooManaging tooApps accesso](active-directory-managing-access-to-apps.md)<br /><br />[Funzionamento della gestione dell'accesso in Azure AD](active-directory-manage-groups.md)<br /><br />[Come tooUse gruppi tooManage tooSaaS accesso applicazioni](active-directory-accessmanagement-group-saasapps.md) |
| Abilitare le funzionalità self-service per la gestione di app e gruppi. |[Gestione self-service delle applicazioni](active-directory-self-service-application-access.md)<br /><br />[Gestione self-service dei gruppi](active-directory-accessmanagement-self-service-group-management.md) |
| Istruzioni per la configurazione dei gruppi in Azure AD. |[Come tooCreate gruppi di sicurezza](active-directory-accessmanagement-manage-groups.md)<br /><br />[Come tooDesignate proprietari di un gruppo](active-directory-accessmanagement-managing-group-owners.md)<br /><br />[Come tooUse hello "All Users" gruppo](active-directory-accessmanagement-dedicated-groups.md) |
| Utilizzare gruppi dinamici tooautomatically popolare il gruppo utilizzando le regole di appartenenza basata su attributi |[Appartenenza dinamica a gruppi: regole avanzate](active-directory-accessmanagement-groups-with-advanced-rules.md)<br /><br />[Risoluzione dei problemi di appartenenza dinamica ai gruppi](active-directory-accessmanagement-troubleshooting.md) |

La gestione dell'accesso alle applicazioni basata sui gruppi è disponibile per [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) e [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/). La gestione self-service dei gruppi, la gestione self-service delle applicazioni e i gruppi dinamici sono funzionalità di [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) .

### <a name="b2b-collaboration-enable-partner-access-tooapplications"></a>Collaborazione B2B: Abilitare tooapplications accesso partner
Se l'azienda ha collaborato con altre società, è probabile che sia necessario toomanage partner accesso tooyour alle applicazioni aziendali. Azure la collaborazione B2B Active Directory fornisce un modo semplice e sicuro di tooshare le app con i partner.

| Guida agli articoli |  |
|:---:| --- |
| Panoramica delle diverse funzionalità di Azure AD utili per gestire utenti esterni quali partner, clienti e così via. |[Confronto tra le funzionalità per la gestione di identità esterne con Azure AD](active-directory-b2b-compare-external-identities.md) |
| TooB2B un'introduzione di collaborazione e la modalità di avvio tooget |[Integrazione cloud dei partner semplice e sicura con Azure AD](active-directory-b2b-what-is-azure-ad-b2b.md)<br /><br />[Collaborazione B2B di Azure Active Directory](active-directory-b2b-collaboration-overview.md) |
| Un approfondimento in collaborazione B2B di Azure AD e come toouse, |[Collaborazione B2B: funzionamento](active-directory-b2b-how-it-works.md)<br /><br />[Limitazioni correnti della Collaborazione B2B di Azure AD](active-directory-b2b-current-limitations.md)<br /><br />[Procedura dettagliata di uso della Collaborazione B2B di Azure AD](active-directory-b2b-detailed-walkthrough.md) |
| Articoli di riferimento con dettagli tecnici sul funzionamento di Collaborazione B2B di Azure AD. |[Formato file CSV per l'aggiunta di utenti partner](active-directory-b2b-references-csv-file-format.md)<br /><br />[Attributi utente interessati da Collaborazione B2B di Azure AD](active-directory-b2b-references-external-user-object-attribute-changes.md)<br /><br />[Formato del token utente per utenti partner](active-directory-b2b-references-external-user-token-format.md) |

La Collaborazione B2B è attualmente disponibile per [tutte le edizioni di Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).

### <a name="access-panel-a-portal-for-accessing-apps-and-self-service-features"></a>Pannello di accesso: un portale per l'accesso alle app e alle funzionalità self-service
Hello Pannello di accesso di Azure Active Directory è in cui gli utenti finali possono avviare le App e l'accesso hello funzionalità self-service che consentono di toomanage le App e le appartenenze. Toohello Pannello di accesso, altre opzioni per l'accesso alle applicazioni abilitate per SSO sono inoltre inclusi nell'elenco di hello riportato di seguito.

| Guida agli articoli |  |
|:---:| --- |
| Un confronto tra hello diverse opzioni disponibili per la distribuzione di single sign-on App toousers |[Distribuzione di applicazioni integrate AD Azure tooUsers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users) |
| Cenni preliminari hello Pannello di accesso e i relativi MyApps equivalente per dispositivi mobili |[Introduzione tooAccess pannello e MyApps](active-directory-saas-access-panel-introduction.md)<br />- [iOS](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8)<br />- [Android](https://play.google.com/store/apps/details?id=com.microsoft.myapps) |
| La modalità delle app di Azure AD tooaccess hello sito Web di Office 365 |[Utilizzando l'utilità di avvio dell'applicazione di Office 365 hello](https://support.office.com/en-us/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a) |
| La modalità delle app di Azure AD tooaccess hello app Intune Managed Browser per dispositivi mobili |[Intune Managed Browser](https://technet.microsoft.com/en-us/library/dn878029.aspx)<br />- [iOS](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8)<br />- [Android](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser) |
| Come tooaccess Azure AD App usando collegamenti diretti tooinitiate single sign-on |[Recupero di collegamenti diretti Sign-On tooYour App](active-directory-appssoaccess-whatis.md#direct-sign-on-links-for-federated-password-based-or-existing-apps) |

Il pannello di accesso è disponibile per [tutte le edizioni di Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).

### <a name="reports-easily-audit-app-access-changes-and-monitor-sign-ins-tooapps"></a>Report: Facilmente modifiche accesso all'applicazione di controllare e monitorare accessi tooapps
Azure Active Directory fornisce diversi report e avvisi toohelp monitorare tooapplications di accesso dell'organizzazione. È possibile ricevere avvisi per le app tooyour accessi anomali ed è possibile rilevare quando e perché è stato modificato applicazione tooan di accesso degli utenti.

| Guida agli articoli |  |
|:---:| --- |
| Cenni preliminari hello reporting funzionalità in Azure Active Directory |[Introduzione alla creazione di report di Azure AD](active-directory-reporting-getting-started.md) |
| Come toomonitor hello accessi e utilizzo delle app degli utenti |[Visualizzare i report di accesso e uso](active-directory-view-access-usage-reports.md) |
| Tieni traccia delle modifiche apportate toowho può accedere a una particolare applicazione |[Eventi del report di controllo di Azure Active Directory](active-directory-reporting-audit-events.md) |
| Esportare dati hello di tali strumenti tooyour preferito di report tramite hello API Reporting |[Introduzione a hello API Azure AD Reporting](active-directory-reporting-api-getting-started.md) |

i report sono inclusi in diverse edizioni di Azure Active Directory, toosee [fare clic qui](active-directory-view-access-usage-reports.md).

## <a name="see-also"></a>Vedere anche
[Informazioni su Azure Active Directory](active-directory-whatis.md)

[Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/)

[Servizi di dominio Azure Active Directory](https://azure.microsoft.com/services/active-directory-ds/)

[Azure Multi-Factor Authentication](https://azure.microsoft.com/services/multi-factor-authentication/)
