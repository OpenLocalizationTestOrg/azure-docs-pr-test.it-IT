---
title: "aaaWhat è il pannello di accesso di hello in Azure Active Directory? | Microsoft Docs"
description: Informazioni su come varianti toouse di hello accedono tooaccess pannello (browser web, app Android, app iPhone e iPad) App SaaS.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: c0252d01-7e6e-4f79-a70e-600479577dfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 800be6a69f13978c5b88e2fe28a416d4b763656c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-access-panel"></a>Che cos'è il pannello di accesso di hello?

Pannello di accesso Hello è un portale basato sul web. Consente a un utente con un lavoro o account scuola in Azure Active Directory tooview avvio basato su cloud applicazioni e un amministratore di Azure AD ha concesso l'accesso a. È inoltre possibile utilizzare gruppi self-service e le funzionalità di gestione di app tramite il pannello di accesso di hello.

Pannello di accesso Hello è separato dal portale di Azure hello e non è non toohave una sottoscrizione di Azure.

![Pannello di accesso][1]

Pannello di accesso Hello consente tooedit alcune delle impostazioni del profilo, inclusi hello possibilità di:

- Modifica della password hello associata a un account aziendale o dell'istituto di istruzione

- Modificare le impostazioni di ripristino password

- Modifica di contatti e preferenze impostazioni correlate toomulti-factor authentication (per gli account che sono stati toouse richiesto da un amministratore)

- Visualizzare i dettagli dell'account, ad esempio l'ID utente, l'indirizzo di posta elettronica alternativo, i numeri del cellulare e dell'ufficio e i dispositivi

- Visualizzazione e avvio basato su cloud applicazioni hello amministratore di Azure AD ha concesso l'accesso a. Per ulteriori informazioni sul pannello di accesso hello dal punto di vista degli utenti hello, vedere il pannello di accesso hello. 

- Gestire i gruppi in modalità self-service. In particolare, messaggio per l'amministratore può creare e gestire gruppi di sicurezza e l'appartenenza al gruppo di sicurezza richiesta in Azure AD. Per altre informazioni, vedere [Gestione dei gruppi in modalità self-service per gli utenti in Azure AD](active-directory-accessmanagement-self-service-group-management.md) e [Gestione dei gruppi](active-directory-manage-groups.md).




## <a name="accessing-hello-access-panel"></a>Accesso al pannello di accesso hello

È possibile accedere a pannello di accesso hello visitando hello URL seguente in un web browser:`http://myapps.microsoft.com`

Se si dispone di branding personalizzato configurato per la pagina di accesso, è possibile caricare questa personalizzazione aggiungendo fine toohello di dominio dell'organizzazione di hello URL:`http://myapps.microsoft.com/<your domain>.com`

In questo caso, è possibile usare qualsiasi nome di dominio attivo o verificato che sia stato configurato nel portale di Azure.

![Nome di dominio di Wingtip Toys][2]  

È necessario toodistribute hello URL tooall gli utenti accederanno in tooapplications integrate con Azure AD.

## <a name="authentication"></a>Autenticazione

Pannello di accesso tooreach hello, è necessario essere autenticati in Azure AD tramite un account aziendale o dell'istituto di istruzione. È possibile tooAzure autenticato AD direttamente. In alternativa, se un'organizzazione ha configurato la federazione con Active Directory Federation Services (AD FS) o altre tecnologie, è possibile essere autenticati con Windows Server Active Directory.

Se si dispone di una sottoscrizione per Azure o Office 365 e si utilizza hello portale di Azure o un'applicazione di Office 365, è possibile visualizzare l'elenco di hello delle applicazioni senza firma in nuovamente. Se non si sono autenticati si toosign richiesta in utilizzando hello username e password per l'account in Azure AD. Se l'organizzazione ha configurato la federazione, digitare il nome utente hello è sufficiente.

Quando l'autenticazione, è possibile interagire con applicazioni hello che l'amministratore è integrato con directory hello. toolearn toointegrate applicazioni con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="web-browser-requirements"></a>Requisiti del Web browser

Come minimo, il pannello di accesso di hello richiede un browser che supporta JavaScript e CSS sono state abilitate. Per hello toobe di utente connesso tooapplications tramite basato su password single sign-on (SSO), estensione del Pannello di accesso hello deve essere installato nel browser. estensione Hello viene scaricata automaticamente quando si seleziona un'applicazione che è configurata per SSO basato su password.

estensione del Pannello di accesso Hello è attualmente disponibile per i browser Internet Explorer 8 e versioni successive, Edge, Chrome e Firefox.

## <a name="mobile-app-support"></a>Supporto per app per dispositivi mobili

il team di Azure Active Directory Hello pubblica hello app mobile app. Quando si installa l'applicazione hello, è possibile accedere in applicazioni basate su toopassword SSO sui dispositivi iOS e Android.

> [!NOTE]
> È possibile accedere tooapplications che supportano la federazione con Azure AD (ad esempio Salesforce, Google Apps, Dropbox, Box, Concur, Workday, Office 365 e più di 70 altre) in qualsiasi browser web, su qualsiasi dispositivo, senza la necessità di un'app per dispositivi mobili o plug-in. Tutti gli altri [pannello esperienze di accesso](https://myapps.microsoft.com/) anche non richiedono hello my toobe app per dispositivi mobili App utilizzato in un dispositivo mobile.
>
>

### <a name="my-apps-for-android"></a>App personali per Android

App personali per Android è supportata su qualsiasi dispositivo Android che esegue Android 4.1 e versioni successive.  
È disponibile in hello [Google Play store](https://play.google.com/store/apps/details?id=com.microsoft.myapps).

![App personali per Android][3]   

### <a name="my-apps-for-iphone-and-ipad"></a>App personali per iPhone e iPad

App personali per iOS è supportata su qualsiasi iPhone o iPad che esegue iOS 7 e versioni successive.  
È disponibile in hello [Apple App Store](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).

![App personali per iOS][4]    



## <a name="managed-browser-for-my-apps"></a>Managed browser per App personali

App personali inoltre è integrato in hello Intune Managed Browser. Hello Intune Managed Browser per dispositivi iOS e Android svolge un ruolo fondamentale nell'assicurare che i dati nei dispositivi mobili rimangano protetti. Consente di visualizzare ed esplorare in tutta sicurezza pagine Web che potrebbero contenere informazioni aziendali e garantisce un'esperienza di esplorazione Web sicura.  
Sono disponibili le app toomy di accesso rapido nella home page di Managed Browser e i segnalibri, offrendo meno fa clic su tooreach qualsiasi applicazione che si desidera tooaccess.

È disponibile in hello [Apple App Store](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) e [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).

![Managed Browser per App personali][5]    





## <a name="tips-for-testing-hello-user-experience"></a>Suggerimenti per un'esperienza utente hello test

Se si è un amministratore di Azure e si è connessi con un account nella directory di hello toohello portale di Azure, si accede automaticamente nel Pannello di accesso toohello come l'account corrente. In questo caso, è possibile visualizzare tutte le applicazioni che sono state assegnate tooyou.

**tootest come un *diversi* account utente:**

1. Fare clic sul menu utente hello nell'angolo superiore destro di hello di hello portale di Azure o il pannello di accesso di hello e quindi selezionare **Sign Out**. 
2. Passare toohello [Pannello di accesso](http://myapps.microsoft.com).
3. Nella pagina di accesso hello, tipo hello username e password per account di hello nella directory desiderata tootest.


## <a name="starting-applications"></a>Avvio delle applicazioni

Diversi tipi di applicazioni visualizzabili nel Pannello di accesso hello.

### <a name="office-365-applications"></a>Applicazioni di Office 365

Se l'organizzazione Usa applicazioni di Office 365 e sono concessi in licenza per tali applicazioni di Office 365 hello vengono visualizzati nel Pannello di accesso.

Quando si fa clic su un riquadro dell'applicazione per un'applicazione di Office 365, verrà reindirizzato toohello dell'applicazione e automaticamente connesso.

### <a name="microsoft-and-third-party-applications-configured-with-federation-based-sso"></a>Applicazioni Microsoft e di terze parti configurate con il servizio Single Sign-On basato su federazione

L'amministratore può aggiungere applicazioni nella sezione Active Directory del portale di Azure hello hello con modalità SSO hello impostata troppo**Azure Single Sign-On AD**. Se l'amministratore ha esplicitamente concesso che accedere alle applicazioni di toohello, è possibile visualizzare solo tali applicazioni.

Quando si fa clic su un riquadro per una di queste applicazioni, vengono reindirizzate e firmato automaticamente nell'applicazione toohello.

### <a name="password-based-sso-without-identity-provisioning"></a>Single Sign-On basato su password senza provisioning delle identità

L'amministratore può aggiungere applicazioni nella sezione Active Directory del portale di Azure hello hello con modalità SSO hello impostata troppo**basato su Password Single Sign-On**. Tutti gli utenti nella directory hello possono visualizzare tutte le applicazioni che sono state configurate in questa modalità.

Hello prima volta, si fa clic su un riquadro per una di queste applicazioni, è richiesta tooinstall hello Password SSO plug-in per Internet Explorer o Chrome. installazione di Hello potrebbe richiedere si toorestart web browser. Quando si restituisce toohello Pannello di accesso e fare clic su riquadro dell'applicazione hello nuovamente, viene richiesto un nome utente e password per l'applicazione hello. Dopo avere immesso un nome utente e password, queste credenziali vengono archiviate in modo sicuro e collegati tooyour account in Azure AD.

Hello successivo si fa clic su riquadro dell'applicazione hello, si accede automaticamente nell'applicazione toohello.  
È non hanno tooenter nuovamente le credenziali e o installare hello Password SSO plug-in.

Se le credenziali sono cambiate nell'applicazione di terze parti hello destinazione, è necessario aggiornare anche le credenziali vengono archiviate in Azure AD. 

**credenziali tooupdate:**

1. Selezionare l'icona di hello nel riquadro dell'applicazione hello.
2. Selezionare **aggiornare le credenziali** tooreenter hello username e password per l'applicazione di hello.


### <a name="password-based-sso-with-identity-provisioning"></a>Single Sign-On basato su password con provisioning delle identità

L'amministratore può aggiungere le applicazioni in hello **Active Directory** sezione del portale di Azure con la modalità SSO hello hello impostata troppo**basato su Password Single Sign-On**, insieme a provisioning delle identità.

Hello prima volta, si fa clic su un riquadro dell'applicazione per una di queste applicazioni, è richiesta tooinstall hello **Password SSO plug-in per Internet Explorer o Chrome**. installazione di Hello potrebbe richiedere si toorestart web browser.  
Quando si restituisce toohello Pannello di accesso e fare clic su riquadro dell'applicazione hello nuovamente, si accede automaticamente nell'applicazione toohello.

Alcune applicazioni potrebbero richiedere toochange è la password in hello primo accesso di. Se le credenziali sono cambiate nell'applicazione di terze parti hello destinazione, è necessario aggiornare anche le credenziali di hello archiviate in Azure AD. 

**credenziali tooupdate:**

1. Selezionare l'icona di hello nel riquadro dell'applicazione hello.
2. Selezionare **aggiornare le credenziali** tooreenter hello username e password per l'applicazione di hello.


### <a name="application-with-existing-sso-solutions"></a>Applicazione con soluzioni Single Sign-On esistenti

tooconfigure SSO per un'applicazione, hello portale di Azure offre una terza opzione chiamata **Single Sign-On esistente**. Questa opzione consente il toocreate amministratore un'applicazione tooan di collegamento e lo inserisce nel Pannello di accesso hello per utenti selezionati.

Ad esempio, se un'applicazione è configurata tooauthenticate utenti tramite AD FS 2.0, l'amministratore può utilizzare hello **Single Sign-On esistente** opzione toocreate tooit un collegamento nel Pannello di accesso hello. Quando si accede collegamento hello, vengono autenticati tramite AD FS 2.0 o qualsiasi applicazione di hello soluzione SSO esistente fornisce.


## <a name="next-steps"></a>Passaggi successivi

- toosee un elenco di tutti gli argomenti che sono correlati tooapplication management, vedere hello [indice articolo per la gestione delle applicazioni in Azure Active Directory](active-directory-apps-index.md).
 
- toolearn toointegrate un'app SaaS in Azure AD, vedere hello [elenco di esercitazioni sull'App SaaS toointegrate](active-directory-saas-tutorial-list.md).
 
- toolearn informazioni su gestione delle App con Azure AD, vedere hello [introduzione toosingle sign-on e la gestione di app l'accesso con Azure Active Directory](active-directory-appssoaccess-whatis.md).
 
- toolearn ulteriori informazioni su il provisioning dell'utente, vedere [automatizzare provisioning e deprovisioning applicazioni tooSaaS](active-directory-saas-app-provisioning.md).

<!--Image references-->
[1]: ./media/active-directory-saas-access-panel-introduction/01.png
[2]: ./media/active-directory-saas-access-panel-introduction/02.png
[3]: ./media/active-directory-saas-access-panel-introduction/03.png
[4]: ./media/active-directory-saas-access-panel-introduction/04.png
[5]: ./media/active-directory-saas-access-panel-introduction/05.png
