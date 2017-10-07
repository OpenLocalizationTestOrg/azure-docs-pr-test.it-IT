---
title: "aaaWhat è l'accesso all'applicazione e servizio single sign-on con Azure Active Directory? | Microsoft Docs"
description: "Usare Azure Active Directory tooenable single sign-on tooall di hello SaaS e applicazioni web che è necessario per le aziende."
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 75d1a3fd-b3c5-4495-a5c8-c4c24145ff00
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curyand
ms.openlocfilehash: 429522cbd570ab27359c4630c5a6d7b25b692ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-application-access-and-single-sign-on-with-azure-active-directory"></a>Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory
Accesso Single sign-on si intende tooaccess in grado di tutte le applicazioni di hello e risorse che toodo business, è necessario l'accesso una sola volta utilizzando un unico account utente. Una volta effettuato l'accesso, è possibile accedere a tutte hello applicazioni è necessario senza essere tooauthenticate necessari (ad esempio, digitare una password) un secondo momento.

Molte organizzazioni si basano sul software come un servizio (SaaS), ad esempio Office 365, Box e Salesforce, per la produttività dell'utente finale. In passato, il personale IT deve tooindividually creare e aggiornare gli account utente in ciascuna applicazione SaaS e gli utenti hanno tooremember una password per ogni applicazione SaaS.

Azure Active Directory estende Active Directory locale in cloud hello, consentendo agli utenti toouse loro primario accesso account aziendale toonot solo i dispositivi appartenenti a un dominio tootheir e alle risorse aziendali, ma anche tutti i web hello e applicazioni SaaS per il proprio lavoro.

In modo non solo gli utenti non dispone toomanage più set di nomi utente e password, le applicazioni di accesso può essere eseguito il provisioning o deprovisioning automaticamente in base i membri del gruppo dell'organizzazione e lo stato come un dipendenti. Azure Active Directory presenta la sicurezza e i controlli di governance di accesso che consentono di toocentrally gestiscono l'accesso degli utenti tra le applicazioni SaaS.

Azure AD consente toomany di integrazione di applicazioni SaaS note odierna; fornisce gestione identità e accessi e consente agli utenti toosingle sign-on tooapplications direttamente, oppure individuare e avviarle da un portale, ad esempio Office 365 o hello Pannello di accesso di Azure AD.

architettura di Hello di integrazione hello è costituita da hello quattro blocchi predefiniti principali seguenti:

* Accesso Single sign-on consente agli utenti tooaccess alle applicazioni SaaS in base al proprio account aziendale in Azure AD. Accesso Single sign-on è quello che consente l'applicazione di tooan tooauthenticate utenti usando il proprio account aziendale single.
* Il provisioning dell'utente permette il provisioning e il deprovisioning dell’utente nei servizi SaaS di destinazione in base alle modifiche effettuate in Windows Server Active Directory e/o in Azure AD. Un account di provisioning è quello che consente un toouse toobe autorizzato utente un'applicazione, dopo che sono autenticati tramite l'accesso single sign-on.
* La gestione di accesso centralizzate delle applicazioni in hello portale di gestione di Azure consente l'accesso alle applicazioni SaaS di singolo punto di gestione e, con hello possibilità toodelegate applicazione accesso decisione apportato e approvazioni tooanyone organizzazione hello
* Segnalazione e monitoraggio unificati delle attività dell'utente in Azure AD

## <a name="how-does-single-sign-on-with-azure-active-directory-work"></a>Come funziona Single Sign-On con Azure Active Directory (PHP)?
Quando un'utente "accesso" tooan applicazione, passano attraverso un processo di autenticazione in cui sono necessari tooprove che che dicono. Senza single sign-on, questa operazione viene in genere eseguita tramite l'immissione di una password viene archiviata in un'applicazione hello e utente hello tooknow richiesto questa password.

Azure AD supporta tre diverse modalità toosign in tooapplications:

* **Single Sign-On federato** consente applicazioni tooredirect tooAzure Active Directory per l'autenticazione utente anziché richiedere la propria password. Questa è supportata per le applicazioni che il supporto di protocolli, ad esempio SAML 2.0, WS-Federation oppure OpenID Connect e hello modalità più ricca di single sign-on.
* **Single Sign-On basato su password** consente l’archiviazione e la riproduzione delle password delle applicazioni protette utilizzando un'estensione del browser Web o un’app mobile. Questo si avvale di hello esistente processo di accesso fornito da un'applicazione hello, ma consente una password di amministratore toomanage hello e non richiede hello utente tooknow hello password.
* **Single Sign-On esistente** consente AD Azure tooleverage qualsiasi single sign-on esistente che è stato configurato un'applicazione hello, ma consente di queste applicazioni toobe collegati toohello Office 365 o portali del Pannello di accesso AD Azure e consente inoltre creazione di report in Azure AD quando hello vengono avviate sono aggiuntive.

Dopo avere autenticato con un'applicazione, occorre anche un account di cui è stato eseguito il provisioning dell'applicazione hello che indica un'applicazione hello toohave in cui sono le autorizzazioni e livello di accesso sono all'interno di un'applicazione hello. Hello provisioning di questo record di account possono verificarsi automaticamente o può verificarsi manualmente dall'amministratore prima che l'utente hello viene fornito l'accesso single sign-on.

 Ulteriori informazioni su queste modalità Single Sign-On e sul provisioning sono riportate di seguito.

### <a name="federated-single-sign-on"></a>Single Sign-On federato
Single Sign-On federato consente agli utenti di hello sign-on consente in toobe l'organizzazione firmato automaticamente nell'applicazione SaaS di terze parti tooa da Azure AD con informazioni sull'account utente di hello da Azure AD.

In questo scenario, quando sono già stati registrati in Azure AD e si desidera tooaccess risorse controllate da un'applicazione SaaS di terze parti, grazie alla federazione hello per toobe un utente autenticato nuovamente.

Azure AD può supportare single sign-on federato con applicazioni che supportano hello SAML 2.0, WS-Federation oppure OpenID connect protocolli.

Vedere anche: [Gestione dei certificati per Single Sign-On federato](active-directory-sso-certs.md)

### <a name="password-based-single-sign-on"></a>Single Sign-On basato su password
Configurazione basata su password single sign-on consente agli utenti di hello in toobe l'organizzazione firmato automaticamente nell'applicazione SaaS di terze parti tooa da Azure AD con informazioni sull'account utente di hello provenienti dall'applicazione SaaS di terze parti hello. Quando si abilita questa funzionalità, Azure AD raccoglie e archivia in modo sicuro informazioni sull'account utente di hello e la password correlata hello.

Azure AD supporta Single Sign-On basato su password per qualunque applicazione basata su cloud con pagina di accesso basata su HTML. Usando un plug-in del browser personalizzato, consente di automatizzare processo recuperando in modo sicuro le credenziali dell'applicazione, ad esempio hello username e password di hello dalla directory hello di accesso dell'utente hello AAD e immettendo queste credenziali pagina di accesso dell'applicazione hello per conto dell'utente hello. Esistono due casi di utilizzo:

1. **Gestione delle credenziali di amministratore** : gli amministratori possono creare e gestire le credenziali dell'applicazione e assegnare tali credenziali toousers o i gruppi che devono accedere toohello applicazione. In questi casi, degli utenti finali di hello non necessita di tooknow hello credenziali, ma ottiene comunque l'applicazione di accesso single sign-on toohello facendo semplicemente clic su di esso nel proprio pannello di accesso o tramite un collegamento fornito. In questo modo entrambi, la gestione del ciclo di vita delle credenziali hello dal messaggio per l'amministratore, nonché praticità per gli utenti finali in base al quale non è necessario tooremember o gestire password specifiche dell'app. Hello credenziali non sono visibili dall'utente finale di hello durante l'accesso automatico hello processo. Tuttavia, sono individuabili tecnicamente dall'utente di hello tramite debug web strumenti e gli utenti e gli amministratori devono seguire hello stessi criteri di sicurezza come se hello credenziali vengono presentate direttamente dall'utente hello. Le credenziali fornite dall’amministratore sono molto utili quando si fornisce un accesso all'account condiviso tra più utenti, ad esempio i social media o applicazioni di condivisione dei documenti.
2. **Gestione delle credenziali di utente** : gli amministratori possono assegnare gli utenti tooend applicazioni o i gruppi e consentire tooenter gli utenti finali di hello le proprie credenziali direttamente dopo l'accesso a un'applicazione hello hello per la prima volta nel proprio pannello di accesso. Questo scenario è pratico per gli utenti finali, che non devono toocontinually immettere password specifiche dell'applicazione hello ogni volta che accedono a un'applicazione hello. In questo caso d'uso utilizzabile anche come un passo a passo tooadministrative Pietra di gestione delle credenziali hello, in base al quale amministratore hello impostare nuove credenziali per un'applicazione hello in una data futura senza modificare l'esperienza di accesso hello app dell'utente finale di hello.

In entrambi i casi, le credenziali vengono archiviate in formato crittografato nella directory di hello e vengono passate solo tramite HTTPS durante il processo Accedi di hello automatizzata. Utilizzando Single Sign-On basato su password, Azure AD offre una soluzione di gestione dell’accesso all’identità pratica per le applicazioni che non sono in grado di supportare i protocolli di federazione.

SSO basato su password si basa su un browser estensione toosecurely recuperare hello applicazione e utente informazioni specifiche da Azure AD e applicarlo toohello servizio. La maggior parte delle applicazioni SaaS di terze parti supportate da Azure AD supportano questa funzionalità.

Per SSO basato su password, browser dell'utente finale di hello può essere:

* Internet Explorer 8, 9, 10 e 11 -- su Windows 7 o versione successiva (vedere anche [Guida alla distribuzione dell'estensione di Internet Explorer](active-directory-saas-ie-group-policy.md))
* Chrome in Windows 7 o versione successiva e MacOS X o versione successiva
* Firefox 26.0 o versione successiva in Windows XP SP2 o versione successiva e in Mac OS X 10.6 o versione successiva

**Nota:** estensione SSO basato su password hello diventerà disponibile per Edge in Windows 10, quando le estensioni browser diventano supportate per Edge.

### <a name="existing-single-sign-on"></a>Single Sign-On esistente
Quando si configura single sign-on per un'applicazione, il portale di gestione di Azure hello offre una terza opzione di "Single Sign-On esistente". Questa opzione consente a un'applicazione di tooan di collegamento hello amministratore toocreate semplicemente e inserirlo nel Pannello di accesso hello per utenti selezionati.

Ad esempio, se è presente un'applicazione che viene configurato tooauthenticate utenti usando Active Directory Federation Services 2.0, un amministratore può utilizzare hello "Single Sign-On esistente" opzione toocreate tooit un collegamento nel Pannello di accesso hello. Quando gli utenti accedono al collegamento hello, saranno autenticati con Active Directory Federation Services 2.0 o qualsiasi esistente soluzione single sign-on è fornita dall'applicazione hello.

### <a name="user-provisioning"></a>Provisioning utente
Per selezionare le applicazioni, Azure AD Abilita provisioning utenti automatizzato e deprovisioning degli account nelle applicazioni SaaS di terze parti da di hello portale di gestione di Azure, utilizzando le informazioni di identità di Windows Server Active Directory o Azure AD. Quando un utente verrà concesse le autorizzazioni in Azure AD per una di queste applicazioni, può essere creato automaticamente un account (provisioning) nell'applicazione SaaS di destinazione hello.

Quando un utente viene eliminato o le relative informazioni cambiano in Azure AD, tali modifiche si riflettono anche nell'applicazione SaaS hello. In questo modo, la configurazione di gestione del ciclo di vita automatica delle identità consente agli amministratori toocontrol e fornire automatizzati provisioning e deprovisioning dalle applicazioni SaaS. In Azure AD questa automazione della gestione del ciclo di vita dell’identità è abilitata dal provisioning dell'utente.

vedere, più toolearn [tooSaaS automatizzata Provisioning e Deprovisioning applicazioni](active-directory-saas-app-provisioning.md)

## <a name="get-started-with-hello-azure-ad-application-gallery"></a>Introduzione a una raccolta di applicazioni Azure AD hello
Tooget pronto iniziare? toodeploy single sign-on tra Azure AD e le applicazioni SaaS che l'organizzazione utilizza, seguire queste linee guida.

### <a name="using-hello-azure-ad-application-gallery"></a>Utilizzando una raccolta di applicazioni Azure AD hello
Hello [raccolta di Azure Active Directory dell'applicazione](https://azure.microsoft.com/marketplace/active-directory/all/) fornisce un elenco di applicazioni che sono note toosupport una forma di single sign-on con Azure Active Directory.

![][1]

Di seguito sono riportati alcuni suggerimenti per la ricerca delle applicazioni in base alle funzionalità che supportano:

* Azure AD supporta automatico il provisioning e deprovisioning per tutte le app "In primo piano" hello [raccolta di Azure Active Directory dell'applicazione](https://azure.microsoft.com/marketplace/active-directory/all/).
* Un elenco di applicazioni federate che supportano in particolare il Single Sign-On federato tramite un protocollo, ad esempio SAML, WS-Federation oppure OpenID Connect, è disponibile [qui](http://social.technet.microsoft.com/wiki/contents/articles/20235.azure-active-directory-application-gallery-federated-saas-apps.aspx).

Dopo aver trovato l'applicazione, è possibile iniziare da seguire hello fornite istruzioni dettagliate presentate nella raccolta di app hello e in tooenable portale di gestione di Azure hello accesso single sign-on.

### <a name="application-not-in-hello-gallery"></a>Applicazione non nella raccolta di hello?
Se l'applicazione non viene trovato nella raccolta di applicazioni di hello Azure AD, sono disponibili queste opzioni:

* **Aggiungere un'app non elencata in uso** -categoria di utilizzo hello personalizzata nella raccolta di app hello all'interno di hello tooconnect portale di gestione di Azure un'applicazione non pubblicata usata dall'organizzazione. È possibile aggiungere qualunque applicazione che supporta SAML 2.0 come applicazione federata o qualunque applicazione che dispone di una pagina di accesso basata su HTML come applicazione Single Sign-On con password. Per altre informazioni, vedere il blog sull' [aggiunta di un'applicazione personalizzata](active-directory-saas-custom-apps.md).
* **Aggiungere la propria app che stai sviluppando** : se è stato sviluppato un'applicazione hello manualmente, seguire le linee guida hello in hello Azure developer documentazione tooimplement federata single sign-on AD o provisioning mediante hello API graph di Azure AD. Per ulteriori informazioni, vedere le risorse:
  
  * [Scenari di autenticazione per Azure AD](active-directory-authentication-scenarios.md)
  * [https://github.com/AzureADSamples/WebApp-MultiTenant-OpenIdConnect-DotNet](https://github.com/AzureADSamples/WebApp-MultiTenant-OpenIdConnect-DotNet)
  * [https://github.com/AzureADSamples/WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet](https://github.com/AzureADSamples/WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet)
  * [https://github.com/AzureADSamples/NativeClient-WebAPI-MultiTenant-WindowsStore](https://github.com/AzureADSamples/NativeClient-WebAPI-MultiTenant-WindowsStore)
* **Richiedere un'integrazione app** -richiesta di supporto per un'applicazione hello è necessario utilizzare hello [forum sul feedback su Azure AD](https://feedback.azure.com/forums/169401-azure-active-directory/).

### <a name="using-hello-azure-management-portal"></a>Tramite il portale di gestione di Azure hello
È possibile utilizzare l'estensione Active Directory hello in hello portale di gestione di Azure tooconfigure hello applicazione single sign-on. Come primo passaggio, è necessario tooselect una directory dalla sezione Active Directory nel portale di hello hello:

![][2]

toomanage delle applicazioni SaaS di terze parti, è possibile passare nella scheda applicazioni hello della directory selezionata hello. Questa vista consente agli amministratori di:

* Aggiunta di nuove applicazioni dalla raccolta di Azure AD hello, nonché lo sviluppo di App
* Eliminare applicazioni integrate
* Gestire le applicazioni di hello che già integrate

Le attività amministrative tipiche per un'applicazione SaaS di terze parti sono:

* Abilitazione di single sign-on con Azure AD, utilizzando SSO basato su password oppure, se disponibile per la destinazione hello SaaS e SSO federato
* Facoltativamente, abilitare il provisioning e deprovisioning per l'utente (gestione del ciclo dell’identità)
* Per le applicazioni in cui è abilitato il provisioning dell'utente, selezionando gli utenti che dispongono di accesso dell'applicazione toothat

Per le app di raccolta che supportano single sign-on federato, configurazione in genere richiede tooprovide impostazioni di configurazione aggiuntive, ad esempio certificati e metadati toocreate una relazione di trust federativa tra app di terze parti hello e Azure AD. Hello configurazione guidata vengono illustrati i dettagli di hello e offre un accesso semplice toohello dati specifici dell'applicazione SaaS e istruzioni.

Per le app di raccolta che supportano il provisioning utente automatico, è necessario è toogive Azure AD autorizzazioni toomanage degli account nell'applicazione SaaS hello. Come minimo, è necessario tooprovide devono utilizzare le credenziali di Azure AD durante l'autenticazione toohello applicazione di destinazione. Se le impostazioni di configurazione aggiuntive necessario toobe fornito dipende dai requisiti di hello di un'applicazione hello.

## <a name="deploying-azure-ad-integrated-applications-toousers"></a>Distribuzione di Azure AD integrato toousers applicazioni
Azure Active Directory fornisce diversi modi personalizzabili toodeploy applicazioni tooend-gli utenti dell'organizzazione:

* Pannello di accesso di Azure AD
* Applicazione di avvio di Office 365
* App diretto toofederated sign-on
* Toofederated di collegamenti diretti, basato su password, o le app di esistenti

I metodi che si sceglie toodeploy nell'organizzazione è a propria discrezione.

### <a name="azure-ad-access-panel"></a>Pannello di accesso di Azure AD
Hello Pannello di accesso a https://myapps.microsoft.com è un portale basato sul web che consente agli utenti finali con un account aziendale in Azure Active Directory tooview e avviare applicazioni basate su cloud toowhich sono stati concessi diritti di accesso hello Azure AD amministratore. Se si è un utente finale con [Azure Active Directory Premium](https://azure.microsoft.com/pricing/details/active-directory/), possono usare anche le funzionalità di gestione di gruppi self-service tramite hello Pannello di accesso.

![][3]

Hello Pannello di accesso è separato dal portale di gestione Azure hello e non richiede agli utenti toohave un abbonamento Azure o Office 365.

Per ulteriori informazioni nel Pannello di accesso hello Azure AD, vedere hello [Pannello di accesso di introduzione toohello](active-directory-saas-access-panel-introduction.md).

### <a name="office-365-application-launcher"></a>Applicazione di avvio di Office 365
Per le organizzazioni che hanno distribuito Office 365, applicazioni assegnate toousers tramite Azure AD verranno visualizzato anche nel portale di Office 365 hello all'indirizzo https://portal.office.com/myapps. Questo rende semplice e pratico per gli utenti in un'organizzazione toolaunch le proprie App senza la necessità di un portale secondo toouse e hello consiglia app avvio soluzione per le organizzazioni che usano Office 365.

![][4]

Per ulteriori informazioni sull'avvio applicazione hello Office 365, vedere [visualizzare l'app avvio app di Office 365 hello](https://msdn.microsoft.com/office/office365/howto/connect-your-app-to-o365-app-launcher).

### <a name="direct-sign-on-toofederated-apps"></a>App diretto toofederated sign-on
Più applicazioni federate che supportano OpenID, WS-Federation o SAML 2.0 connettono anche supporto hello possibilità per gli utenti toostart in un'applicazione hello e quindi ottengano effettuato l'accesso tramite Azure AD per il reindirizzamento automatico o facendo clic su un collegamento di toosign in. Questo è noto come provider di servizi-sign-on avviato dall'e più alle applicazioni federate nella raccolta di applicazione hello Azure AD supportano questa (vedere la documentazione di hello collegata dalla procedura guidata di configurazione di single sign-on hello dell'app nel portale di gestione di Azure hello per Dettagli).

![][5]

### <a name="direct-sign-on-links-for-federated-password-based-or-existing-apps"></a>Collegamenti diretti di accesso per le applicazioni federate, basate su password o esistenti
Inoltre, Azure AD supporta single sign-on collegamenti diretti tooindividual applicazioni che supportano basato su password single sign-on, single sign-on esistente e qualsiasi forma di single sign-on federato.

Questi collegamenti sono opportunamente gli URL che inviano un utente tramite hello Azure AD sign in-process per un'applicazione specifica senza utente hello avviarle dal Pannello di accesso hello Azure AD o Office 365. Questi URL Single Sign-On è reperibile nella scheda Dashboard hello di qualsiasi applicazione nella sezione Active Directory del portale di gestione di Azure hello hello preintegrate, come illustrato nella schermata di hello riportata di seguito.

![][6]

Questi collegamenti possono essere copiati e incollati in qualsiasi posizione desiderata applicazione toohello selezionato di collegamento tooprovide sign-in. Questo potrebbe essere all’interno di un messaggio di posta elettronica o in qualsiasi portale personalizzato basato sul Web configurato per l'accesso alle applicazioni dell’utente. Di seguito è riportato un esempio di URL Single Sign-On diretto di Azure AD per Twitter:

`https://myapps.microsoft.com/signin/Twitter/230848d52c8745d4b05a60d29a40fced`

Un URL specifico tooorganization simile per il pannello di accesso di hello, è possibile personalizzare ulteriormente questo URL mediante l'aggiunta di uno dei domini di attivo o verificato hello per le directory dopo il dominio di indirizzo myapps.microsoft.com hello. In questo modo, che eventuali personalizzazioni organizzative viene caricato immediatamente nella pagina di accesso hello senza utente hello necessità tooenter innanzitutto l'ID utente:

`https://myapps.microsoft.com/contosobuild.com/signin/Twitter/230848d52c8745d4b05a60d29a40fced`

Quando un utente autorizzato fa clic su uno di questi collegamenti specifici dell'applicazione, vengono innanzitutto visualizzati relativi aziendale nella pagina di accesso (presupponendo che non sono già firmati) e dopo l'accesso tootheir reindirizzato app senza arrestare prima il pannello di accesso hello. Se l'utente hello manca prerequisiti tooaccess hello applicazione, ad esempio di estensione del browser di hello basato su password di accesso singolo, collegamento hello richiederà estensione mancante hello tooinstall utente hello. URL del collegamento Hello anche rimane costante se hello configurazione single sign-on per un'applicazione hello viene modificato.

Questi collegamenti utilizzano hello stessi meccanismi di controllo di accesso come hello accedere pannello e Office 365, e solo gli utenti o gruppi che sono stati assegnati toohello applicazione nel portale di gestione di Azure hello saranno in grado di autenticare toosuccessfully. Tuttavia, tutti gli utenti non autorizzati verranno visualizzato un messaggio che indica che non dispongono di accesso e viene assegnati un collegamento tooload hello accesso pannello tooview applicazioni disponibili per i quali hanno accesso.

## <a name="related-articles"></a>Articoli correlati
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Ricerca di applicazioni cloud non autorizzate con Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md)
* [Introduzione tooManaging tooApps accesso](active-directory-managing-access-to-apps.md)
* [Confronto tra le funzionalità per la gestione di identità esterne con Azure AD](active-directory-b2b-compare-external-identities.md)

<!--Image references-->
[1]: ./media/active-directory-appssoaccess-whatis/onlineappgallery.png
[2]: ./media/active-directory-appssoaccess-whatis/azuremgmtportal.png
[3]: ./media/active-directory-appssoaccess-whatis/accesspanel.png
[4]: ./media/active-directory-appssoaccess-whatis/officeapphub.png
[5]: ./media/active-directory-appssoaccess-whatis/workdaymobile.png
[6]: ./media/active-directory-appssoaccess-whatis/deeplink.png
