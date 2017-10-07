---
title: 'Domande frequenti: Azure AD B2C | Microsoft Docs'
description: Domande frequenti su Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: saeeda
manager: krassk
editor: bryanla
ms.assetid: ed33c2ca-76d0-442a-abb1-8b7b7bb92d6a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeeda
ms.openlocfilehash: f7857299bc3cb9d5fbe58e047818ec56741e0740
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-frequently-asked-questions-faq"></a>Azure AD B2C: domande frequenti 
Questa pagina risponde alle domande frequenti su hello B2C Azure Active Directory (Azure AD). Controllarla costantemente per eventuali aggiornamenti.

### <a name="can-i-use-azure-ad-b2c-features-in-my-existing-employee-based-azure-ad-tenant"></a>È possibile usare le funzionalità di Azure AD B2C nel tenant di Azure AD esistente per dipendenti aziendali?
Azure AD e Azure Active Directory B2C vengono offerte di prodotti separata e non possono coesistere nel hello stesso tenant.  Un tenant di Azure AD rappresenta un'organizzazione.  Un tenant di Azure Active Directory B2C rappresenta una raccolta di identità toobe utilizzato con le applicazioni relying party.  Con i criteri personalizzati (in anteprima pubblica), Azure Active Directory B2C possibile attuare la federazione tooAzure AD autenticazione consentendo di dipendenti in un'organizzazione.

### <a name="can-i-use-azure-ad-b2c-tooprovide-social-login-facebook-and-google-into-office-365"></a>È possibile utilizzare Azure AD B2C tooprovide social login (Facebook e Google +) in Office 365?
Azure Active Directory B2C non può essere utilizzato tooauthenticate utenti per Microsoft Office 365.  Azure AD è la soluzione Microsoft per la gestione dei dipendenti accesso tooSaaS App e dispone di funzionalità progettate a tale scopo, ad esempio l'accesso condizionale di licenza.  Azure AD B2C offre una piattaforma di gestione di identità e accessi per la compilazione di applicazioni web e per dispositivi mobili.  Quando Azure Active Directory B2C è configurato toofederate tooan tenant di Azure AD, il tenant di Azure AD hello gestisce tooapplications accesso dipendente che si basano su Azure Active Directory B2C.

### <a name="what-are-local-accounts-in-azure-ad-b2c-how-are-they-different-from-work-or-school-accounts-in-azure-ad"></a>Che cosa sono gli account locali in Azure AD B2C? In che cosa differiscono dagli account aziendali o dell'istituto di istruzione in Azure AD?
In un tenant di Azure AD, gli utenti che appartengono a tenant toohello Accedi con un indirizzo di posta elettronica del modulo hello `<xyz>@<tenant domain>`.  Hello `<tenant domain>` domini hello tenant o di saluto iniziali è uno dei hello verificato `<...>.onmicrosoft.com` dominio. Questo tipo di account è un account aziendale o dell'istituto di istruzione.

In un tenant di Azure Active Directory B2C, la maggior parte delle applicazioni si desideri impostare utente hello toosign in qualsiasi indirizzo di posta elettronica arbitrario (ad esempio, joe@comcast.net, bob@gmail.com, sarah@contoso.com, o jim@live.com). Questo tipo di account è un account locale.  Sono supportati anche nomi utente arbitrari come account locali (ad esempio, joe, bob, sarah o jim). È possibile scegliere uno di questi due tipi di account locale tramite la configurazione di Azure Active Directory B2C in hello portale di Azure.

### <a name="which-social-identity-providers-do-you-support-now-which-ones-do-you-plan-toosupport-in-hello-future"></a>Quali provider di identità di social networking sono attualmente supportati? Quali occorre pianificare toosupport in futuro hello?
Attualmente sono supportati Facebook, Google +, LinkedIn, Amazon, Twitter (anteprima), WeChat (anteprima), Weibo (anteprima) e QQ (anteprima). Verrà aggiunto il supporto per altri provider di identità di social networking noti, in base alle esigenze dei clienti.

In Azure AD B2C è stato aggiunto anche il supporto per i [criteri personalizzati](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-overview-custom).  Questi [criteri personalizzati](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-overview-custom) consentono di propri criteri che con qualsiasi provider di identità che supporta un toocreate developer [OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) o SAML. 

Per un'introduzione ai criteri personalizzati, vedere lo [starter pack sui criteri personalizzati](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack).

### <a name="can-i-configure-scopes-toogather-more-information-about-consumers-from-various-social-identity-providers"></a>È possibile configurare gli ambiti toogather ulteriori informazioni sui clienti, dai diversi provider di identità di social networking?
No, ma questa funzionalità verrà implementata in futuro. ambiti di Hello predefinito utilizzati per il set supportato dei provider di identità di social networking sono:

* Facebook: email
* Google+: email
* Account Microsoft: profilo di posta elettronica openid
* Amazon: profile
* LinkedIn: r_emailaddress e r_basicprofile

### <a name="does-my-application-have-toobe-run-on-azure-for-it-work-with-azure-ad-b2c"></a>L'applicazione dispone di toobe eseguire in Azure per tale lavoro con Azure Active Directory B2C?
No, non è possibile ospitare l'applicazione in qualsiasi punto (in locale o cloud hello). Tutti gli elementi necessari toointeract con Azure Active Directory B2C è hello toosend possibilità e ricevere richieste HTTP su endpoint accessibile pubblicamente.

### <a name="i-have-multiple-azure-ad-b2c-tenants-how-can-i-manage-them-on-hello-azure-portal"></a>Nel caso di più tenant Azure AD B2C, Come è possibile gestire tali nel portale di Azure hello?
Prima di aprire 'Azure Active Directory B2C' nel menu di sinistra hello di hello portale di Azure, è necessario passare nella directory hello desiderato toomanage.  Passare alla directory facendo la tua identità in alto a hello destra hello portale di Azure, quindi scegliere una directory in hello elenco a discesa che viene visualizzata.  Per istruzioni dettagliate con immagini, vedere [passare le impostazioni di Active Directory B2C tooAzure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).

### <a name="how-do-i-customize-verification-emails-hello-content-and-hello-from-field-sent-by-azure-ad-b2c"></a>Come personalizzare i messaggi di posta elettronica verifica (hello contenuto e hello "da:" campo) inviato da Azure AD B2C?
È possibile utilizzare hello [funzionalità di branding aziendale](../active-directory/active-directory-add-company-branding.md) contenuto hello toocustomize di verifica messaggi di posta elettronica. In particolare, è possono personalizzare questi due elementi di posta elettronica hello:

* **Logo banner**: mostrato all'hello in basso a destra.
* **Colore di sfondo**: visualizzata nella parte superiore di hello.

    ![Screenshot di un messaggio di posta elettronica di verifica personalizzato](./media/active-directory-b2c-faqs/company-branded-verification-email.png)

firma di posta elettronica Hello contiene il nome del tenant di hello B2C fornito al momento della creazione tenant hello B2C. È possibile modificare il nome di hello usando queste istruzioni:

1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com/) come hello amministratore della sottoscrizione.
1. Passare tooyour B2C tenant.
1. Fare clic su hello **configura** scheda.
1. Hello modifica **nome** campo hello **proprietà Directory** sezione.
1. Fare clic su **salvare** nella parte inferiore di hello della pagina hello.

Attualmente non c'è nessun hello toochange modo "da:" campo messaggio di posta elettronica hello. Votare [feedback.azure.com](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/15334335-fully-customizable-verification-emails) si è interessati alla personalizzazione corpo hello del messaggio di verifica hello.

### <a name="how-can-i-migrate-my-existing-user-names-passwords-and-profiles-from-my-database-tooazure-ad-b2c"></a>Come è possibile migrare il nome utente, password e i profili da my tooAzure database Active Directory B2C?
È possibile utilizzare hello API Azure AD Graph toowrite lo strumento di migrazione. Vedere hello [esempio relativo all'API Graph](active-directory-b2c-devquickstarts-graph-dotnet.md) per informazioni dettagliate.

### <a name="what-password-policy-is-used-for-local-accounts-in-azure-ad-b2c"></a>Quali sono i criteri password usati per gli account locali in Azure AD B2C?
criteri password di Azure Active Directory B2C per gli account locali Hello si basa sui criteri di hello per Azure AD. Azure AD B2C dell'iscrizione, l'iscrizione o accesso e la password reimpostare la complessità della password "sicuro" di criteri utilizzato hello e senza scadenza le password. Hello lettura [criteri password di Azure AD](https://msdn.microsoft.com/library/azure/jj943764.aspx) per altri dettagli.

### <a name="can-i-use-azure-ad-connect-toomigrate-consumer-identities-that-are-stored-on-my-on-premises-active-directory-tooazure-ad-b2c"></a>È possibile utilizzare le identità utente di Azure AD Connect toomigrate archiviati nel mio tooAzure di Active Directory locale AD B2C?
No, Azure AD Connect non è progettato toowork con Azure Active Directory B2C. È consigliabile utilizzare hello [API Graph](active-directory-b2c-devquickstarts-graph-dotnet.md) per la migrazione dell'utente.

### <a name="can-my-app-open-up-azure-ad-b2c-pages-within-an-iframe"></a>L'applicazione può aprire le pagine di Azure AD B2C all'interno di un iFrame?
No. Per motivi di sicurezza, le pagine di Azure AD B2C non possono essere aperte in un iFrame.  Il servizio comunica con hello browser tooprohibit IFRAME.  Hello community di sicurezza in generale e hello specifica OAUTH2, consigliabile evitare l'utilizzo di IFRAME per esperienze di identità a causa di rischio toohello martinetto fare clic su.

### <a name="does-azure-ad-b2c-work-with-crm-systems-such-as-microsoft-dynamics"></a>Azure AD B2C è compatibile con i sistemi CRM come Microsoft Dynamics?
È disponibile l'integrazione con il portale di Microsoft Dynamics 365.  Vedere [toouse configurazione Dynamics 365 portale Azure Active Directory B2C per l'autenticazione](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/portals/azure-ad-b2c).

### <a name="does-azure-ad-b2c-work-with-sharepoint-on-premises-2016-or-earlier"></a>Azure AD B2C è compatibile con SharePoint 2016 locale o versione precedente?
Azure Active Directory B2C non è destinata hello SharePoint esterni partner scenario di condivisione; vedere [Azure AD B2B](http://blogs.technet.com/b/ad/archive/2015/09/15/learn-all-about-the-azure-ad-b2b-collaboration-preview.aspx) invece.

### <a name="should-i-use-azure-ad-b2c-or-b2b-toomanage-external-identities"></a>Utilizzare le identità esterne di toomanage B2B o di Azure Active Directory B2C
Leggere questo articolo su [le identità esterne](../active-directory/active-directory-b2b-compare-external-identities.md) toolearn informazioni sull'applicazione hello appropriate funzionalità tooyour scenari di identità esterna.

### <a name="what-reporting-and-auditing-features-does-azure-ad-b2c-provide-are-they-hello-same-as-in-azure-ad-premium"></a>Quali funzionalità di reporting e controllo offre Azure AD B2C? Sono che essi stessi hello come Azure AD Premium?
Azure Active Directory B2C No, non supporta hello stesso insieme di report come Azure AD Premium. Esistono tuttavia molte caratteristiche comuni:

* Hello Accedi report forniscono un record di ogni Accedi con dettagli ridotti.
* I report di controllo sono disponibili nel portale di Azure in Azure Active Directory hello > log di controllo di attività > scegliere B2C e applicare filtri in base alle esigenze. Sono incluse sia le attività amministrative che quelle delle applicazioni. 
* Un report di utilizzo, che include il numero di utenti, il numero di accessi e il volume di autenticazioni MFA, è disponibile tramite l'[API per la creazione di report di utilizzo](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-usage-reporting-api).

### <a name="can-i-localize-hello-ui-of-pages-served-by-azure-ad-b2c-what-languages-are-supported"></a>È possibile localizzare i hello dell'interfaccia utente delle pagine gestite da Azure AD B2C? Quali lingue sono supportate?
È possibile usarlo.  Altre informazioni sulla [personalizzazione della lingua](active-directory-b2c-reference-language-customization.md) che è in anteprima pubblica.  Offriamo traduzioni per 36 lingue ed è possibile sostituire qualsiasi toosuit stringa le proprie esigenze.

### <a name="can-i-use-my-own-urls-on-my-sign-up-and-sign-in-pages-that-are-served-by-azure-ad-b2c-for-instance-can-i-change-hello-url-from-loginmicrosoftonlinecom-toologincontosocom"></a>È possibile usare l'URL personale nelle pagine di iscrizione e accesso servite da Azure AD B2C? Ad esempio, è possibile modificare l'URL di hello da login.microsoftonline.com toologin.contoso.com?
No, per il momento. Questa funzionalità verrà implementata in futuro. Verifica del dominio in hello **domini** scheda nel portale di Azure classico hello non raggiungere questo obiettivo.

### <a name="how-do-i-delete-my-azure-ad-b2c-tenant"></a>Come si elimina il tenant di Azure AD B2C?
Seguire questi passaggi toodelete tenant di Azure Active Directory B2C:

1. Seguire questi passaggi troppo[passare le impostazioni di Active Directory B2C tooAzure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) su hello portale di Azure.
1. Passare toohello **applicazioni**, **provider di identità**, e **tutti i criteri** ed eliminare tutte le voci di hello in ognuno di essi.
1. Accedi a questo punto toohello [portale di Azure classico](https://manage.windowsazure.com/) come hello amministratore della sottoscrizione. (Utilizzare hello stesso lavoro o scuola account o hello stesso account di Microsoft utilizzato toosign iscrizione a Azure).
1. Passare toohello estensione di Active Directory a sinistra di hello e fare clic su tenant B2C.
1. Fare clic su hello **utenti** scheda.
1. Selezionare ogni utente a sua volta (utente exclude hello amministratore della sottoscrizione è stato eseguito l'accesso come). Fare clic su **eliminare** nella parte inferiore di hello della pagina hello e fare clic su **Sì** quando richiesto.
1. Fare clic su hello **applicazioni** scheda.
1. Selezionare **applicazioni proprietà dell'azienda** in hello **Mostra** campo elenco a discesa e fare clic su hello segno di spunta.
1. Un'applicazione denominata **b2c-extensions-app**. Fare clic su **eliminare** nella parte inferiore di hello della pagina hello e fare clic su **Sì** quando richiesto.
1. Passare di nuovo l'estensione Active Directory toohello e selezionare il tenant B2C.
1. Fare clic su **eliminare** nella parte inferiore di hello della pagina hello. processo di hello toocomplete, seguire le istruzioni di hello nella schermata di hello.

### <a name="can-i-get-azure-ad-b2c-as-part-of-enterprise-mobility-suite"></a>È possibile ottenere Azure AD B2C come parte di Enterprise Mobility Suite?
No, Azure AD B2C è un servizio di Azure con pagamento in base al consumo e non fa parte di Enterprise Mobility Suite.

### <a name="how-do-i-report-issues-with-azure-ad-b2c"></a>Come è possibile segnalare problemi relativi ad Azure AD B2C?
Vedere [Azure Active Directory B2C: Inviare richieste di supporto](active-directory-b2c-support.md).
