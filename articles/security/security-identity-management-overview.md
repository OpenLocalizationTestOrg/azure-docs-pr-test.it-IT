---
title: "sicurezza aaaAzure funzionalità che consentono di con la gestione delle identità | Documenti Microsoft"
description: " In questo articolo viene fornita una panoramica delle funzionalità di sicurezza di Azure hello principali che ti consentono di gestione delle identità. Identità e accessi Gestione soluzioni Guida di Microsoft IT proteggere tooapplications di accesso e le risorse tra data center aziendale hello e nel cloud hello, abilitando livelli aggiuntivi di convalida, ad esempio multi-factor authentication e condizionale criteri di accesso. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 5aa0a7ac-8f18-4ede-92a1-ae0dfe585e28
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: terrylan
ms.openlocfilehash: f08e4f6cf2e48e455a16858b7fee08b53d5aa585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-identity-management-security-overview"></a>Informazioni generali sulla sicurezza della gestione delle identità di Azure
Identità e accessi Gestione soluzioni Guida di Microsoft IT proteggere tooapplications di accesso e le risorse tra data center aziendale hello e nel cloud hello, abilitando livelli aggiuntivi di convalida, ad esempio multi-factor authentication e condizionale criteri di accesso. Il monitoraggio delle attività sospette tramite funzioni avanzate di report di sicurezza, controllo e avvisi consente di attenuare i potenziali problemi di sicurezza. [Azure Active Directory Premium](../active-directory/active-directory-editions.md) fornisce single sign-on toothousands le app cloud (SaaS) e l'accesso tooweb App eseguite in locale.

Vantaggi di sicurezza di Azure Active Directory (AD) includono il possibilità hello di:

* Creare e gestire una singola identità per ogni utente in un'azienda ibrida, mantenendo sincronizzati utenti, gruppi e dispositivi
* Fornire l'accesso single sign-on tooyour applicazioni tra migliaia di applicazioni SaaS preintegrate
* Abilitare la sicurezza dell'accesso alle applicazioni grazie a Multi-Factor Authentication basata su regole per applicazioni locali e cloud
* Applicazioni mediante il Proxy di applicazione AD Azure web di accesso remoto sicuro di provisioning tooon locale

obiettivo di Hello di questo articolo è tooprovide una panoramica delle funzionalità di sicurezza di Azure core hello che ti consentono di gestione delle identità. È possibile utilizzare collegamenti tooarticles che forniscono i dettagli di ogni funzionalità in modo per ulteriori informazioni.  

Hello viene descritta la seguente funzionalità di gestione delle identità di Azure core hello:

* Single sign-on
* Proxy inverso
* Autenticazione a più fattori
* Monitoraggio della sicurezza, avvisi e report basati su Machine Learning
* Gestione delle identità e dell'accesso degli utenti
* Registrazione del dispositivo
* Privileged Identity Management
* Identity Protection
* Gestione delle identità ibrida

## <a name="single-sign-on"></a>Single sign-on
Single sign-on (SSO) si intende tooaccess in grado di tutte le applicazioni di hello e risorse che toodo business, è necessario l'accesso una sola volta utilizzando un unico account utente. Una volta effettuato l'accesso, è possibile accedere a tutte hello applicazioni è necessario senza essere tooauthenticate necessari (ad esempio, digitare una password) un secondo momento.

Molte organizzazioni si basano sul software come un servizio (SaaS), ad esempio Office 365, Box e Salesforce, per la produttività dell'utente finale. In passato, tooindividually necessario personale IT di creare e aggiornare gli account utente in ciascuna applicazione SaaS e gli utenti dovevano tooremember una password per ogni applicazione SaaS.

Azure AD estende gli ambienti Active Directory locale al cloud hello, consentendo agli utenti toouse loro primario accesso account aziendale toonot solo i dispositivi appartenenti a un dominio tootheir e alle risorse aziendali, ma anche tutti hello web e applicazioni SaaS per il proprio lavoro.

Non solo gli utenti, non toomanage più set di nomi utente e password, accesso all'applicazione può essere automaticamente sottoposto a provisioning o deprovisioning in base ai gruppi organizzativi e lo stato di un dipendente. Azure AD un'introduzione alla protezione e i controlli di governance di accesso che consentono di toocentrally gestiscono l'accesso degli utenti tra le applicazioni SaaS.

Altre informazioni:

* [Informazioni generali su Single Sign-On](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../active-directory/active-directory-appssoaccess-whatis.md)
* [Integrare i servizi Single Sign-On di Azure Active Directory nelle app SaaS](../active-directory/active-directory-sso-integrate-saas-apps.md)

## <a name="reverse-proxy"></a>Proxy inverso
Proxy dell'applicazione Azure Active Directory consente di pubblicare applicazioni locali, ad esempio [SharePoint](https://support.office.com/article/What-is-SharePoint-97b915e6-651b-43b2-827d-fb25777f446f?ui=en-US&rs=en-US&ad=US) siti [Outlook Web App](https://technet.microsoft.com/library/jj657718.aspx), e [IIS](http://www.iis.net/)-basato su applicazioni all'interno della rete privata e fornisce l'accesso sicuro toousers all'esterno della rete. Proxy dell'applicazione fornisce l'accesso remoto e single sign-on (SSO) per molti tipi di locale delle applicazioni web con hello migliaia di applicazioni SaaS che supporta Azure AD. I dipendenti possono accedere in App tooyour home sui propri dispositivi mobili ed eseguire l'autenticazione tramite questo proxy basato su cloud.

Altre informazioni:

* [Abilitazione del proxy di applicazione di Azure AD](../active-directory/active-directory-application-proxy-enable.md)
* [Pubblicare applicazioni mediante il proxy di applicazione AD Azure](../active-directory/active-directory-application-proxy-publish.md)
* [Accesso Single Sign-On con il proxy di applicazione](../active-directory/active-directory-application-proxy-sso-using-kcd.md)
* [Utilizzo di access condizionale](../active-directory/active-directory-application-proxy-conditional-access.md)

## <a name="multi-factor-authentication"></a>Autenticazione a più fattori
Azure multi-factor authentication (MFA) è un metodo di autenticazione che richiede l'uso di hello di più di un metodo di verifica e aggiunge un secondo livello critico di sicurezza toouser accessi e le transazioni. MFA contribuisce a salvaguardare toodata di accesso e le applicazioni rispettando richiesta dell'utente per un semplice processo. Offre autenticazione avanzata tramite diverse opzioni di verifica, ad esempio una telefonata, un SMS, una notifica dell'app per dispositivi mobili o un codice di verifica e token OAuth di terze parti.

Altre informazioni:

* [Autenticazione a più fattori](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [Informazioni su Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)
* [Come funziona Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="security-monitoring-alerts-and-machine-learning-based-reports"></a>Monitoraggio della sicurezza, avvisi e report basati su Machine Learning
Monitoraggio della sicurezza, avvisi e report basati su Machine Learning che identificano i modelli di accesso non coerenti per contribuire alla protezione dell'azienda. È possibile utilizzare l'accesso di Azure Active Directory e utilizzo report toogain visibilità hello integrità e sicurezza della directory dell'organizzazione. Con queste informazioni, un amministratore di directory possa meglio stabilire l'origine di possibili rischi per la sicurezza in modo da poter adeguatamente pianificare toomitigate tali rischi.

Nel portale di Azure classico hello, i report sono suddivisi in hello seguenti modi:

* Report anomalie: includono eventi che è stato rilevato toobe anomali di accesso. L'obiettivo è toomake si è consapevoli di tale attività e consentono di toobe in grado di toomake aggettivo indicano se un evento è sospetto.
* Report applicazioni integrate: offrono informazioni dettagliate sull'uso delle applicazioni cloud nell'organizzazione. Azure Active Directory offre l'integrazione con migliaia di applicazioni cloud.
* Report errori: indicano errori che possono verificarsi durante il provisioning di applicazioni tooexternal account.
* Report specifici dell'utente: visualizzano i dati del dispositivo/dell'attività di accesso per un utente specifico.
* Log attività: include un record di tutti gli eventi controllati entro hello ultime 24 ore, ultimi 7 giorni, o ultimi 30 giorni e modifiche dell'attività di gruppo e attività di registrazione e di reimpostazione della password.

Altre informazioni:

* [Visualizzare i report di accesso e utilizzo](../active-directory/active-directory-view-access-usage-reports.md)
* [Introduzione ad Azure Active Directory Reporting](../active-directory/active-directory-reporting-getting-started.md)
* [Guida alla creazione di report in Azure Active Directory](../active-directory/active-directory-reporting-guide.md)

## <a name="consumer-identity-and-access-management"></a>Gestione delle identità e dell'accesso degli utenti
Azure Active B2C di Directory è un servizio di gestione di identità globale, a disponibilità elevata per le applicazioni per consumatori che viene ridimensionata toohundreds di milioni di valori Identity. Il servizio può essere integrato tra piattaforme mobili e Web. Il consumer può accedere tooall le applicazioni attraverso esperienze di personalizzabile tramite gli account di social networking esistenti o creando nuove credenziali.

In hello precedente, gli sviluppatori di applicazioni che volevano toosign backup e accesso degli utenti nelle proprie applicazioni sarebbero siano scritti con il proprio codice. E si sarebbe usato locale database o i sistemi toostore nomi utente e password. Azure B2C Directory attiva offre organizzazione una migliore gestione identità consumer di toointegrate modo nelle applicazioni con supporto hello di una piattaforma sicura, basato su standard e un ampio set di criteri estendibili.

Con Azure Active Directory B2C, gli utenti possono registrarsi alle applicazioni usando gli account di social networking esistenti (Facebook, Google, Amazon, LinkedIn) o creando nuove credenziali (indirizzo di posta elettronica e password o nome utente e password).

Altre informazioni:

* [Informazioni su Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/)
* [Anteprima di Azure Active Directory B2C: iscrizione e accesso degli utenti alle applicazioni](../active-directory-b2c/active-directory-b2c-overview.md)
* [Anteprima di Azure Active Directory B2C: Tipi di applicazioni](../active-directory-b2c/active-directory-b2c-apps.md)

## <a name="device-registration"></a>Registrazione del dispositivo
Registrazione dispositivo di Azure AD è hello base basata su dispositivi [accesso condizionale](../active-directory/active-directory-conditional-access-device-registration-overview.md) scenari. Quando un dispositivo viene registrato, registrazione dispositivo Azure Active Directory fornisce dispositivo hello con un'identità che è usato tooauthenticate hello quando hello utente accede. dispositivo Hello autenticato e gli attributi di hello del dispositivo hello, possono quindi essere tooenforce utilizzato Criteri di accesso condizionale per le applicazioni ospitate nel cloud hello e locale.

Se combinato con una soluzione di gestione (MDM) di dispositivi mobili, ad esempio Intune, sugli attributi del dispositivo hello in Azure Active Directory vengono aggiornati con informazioni aggiuntive sul dispositivo di hello. Ciò consente di regole di accesso condizionale toocreate che impongono l'accesso da dispositivi toomeet agli standard di sicurezza e conformità.

Altre informazioni:

* [Introduzione a Registrazione dispositivo Azure Active Directory](../active-directory/active-directory-conditional-access-device-registration-overview.md)
* [Registrazione automatica dei dispositivi con Azure Active Directory per i dispositivi Windows aggiunti a un dominio](../active-directory/active-directory-conditional-access-automatic-device-registration.md)
* [Come configurare la registrazione automatica dei dispositivi Windows con Azure Active Directory aggiunti a un dominio](../active-directory/active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="privileged-identity-management"></a>Privileged Identity Management
Gestione di identità con privilegi di Azure Active Directory (AD) consente di gestire, controllare e monitorare le identità privilegiate e tooresources di accesso di Azure AD, nonché altri Microsoft online services quali Office 365 o Microsoft Intune.

In alcuni casi gli utenti devono toocarry operazioni privilegiate in risorse di Azure o Office 365 o altre applicazioni SaaS. Questo spesso significa che le organizzazioni possono toogive di accesso con privilegi permanenti usarle in Azure AD. Questo rappresenta un rischio di sicurezza crescente per le risorse ospitate nel cloud poiché le organizzazioni non sono in grado di monitorare completamente le operazioni eseguite dagli utenti con i privilegi amministrativi. Inoltre, se un account utente con accesso privilegiato è compromesso, tale singola violazione può compromettere la sicurezza dell'intero cloud. Azure AD Privileged Identity Management consente tooresolve questo rischio.

Azure AD Privileged Identity Management consente di effettuare le operazioni seguenti:

* Individuare gli utenti amministratori di Azure AD
* Abilitare le connessioni, "just in time" accesso amministrativo tooMicrosoft Online Services quali Office 365 e Intune
* Ottenere report sulla cronologia degli accessi degli amministratori e sulle modifiche alle assegnazioni degli amministratori
* Ottenere avvisi relativi al ruolo con privilegi di accesso tooa

Altre informazioni:

* [Gestione identità con privilegi di Azure AD](../active-directory/active-directory-privileged-identity-management-configure.md)
* [Ruoli in Azure AD Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-roles.md)
* [Azure AD Privileged Identity Management: Come tooadd o rimuovere un ruolo utente](../active-directory/active-directory-privileged-identity-management-how-to-add-role-to-user.md)

## <a name="identity-protection"></a>Identity Protection
Azure AD Identity Protection è un servizio di sicurezza che offre un quadro consolidato degli eventi di rischio e delle potenziali vulnerabilità che interessano le identità dell'organizzazione. Identity Protection si avvale delle funzionalità esistenti di rilevamento anomalie di Azure Active Directory, disponibili tramite i report Anomalie dell'attività di Azure AD, e introduce nuovi tipi di eventi di rischio che consentono di rilevare anomalie in tempo reale.

Altre informazioni:

* [Azure Active Directory Identity Protection](../active-directory/active-directory-identityprotection.md)
* [Channel 9: Azure AD and Identity Show: Identity Protection Preview](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="hybrid-identity-management"></a>Gestione delle identità ibrida
Approccio tooidentity intervalli locali Microsoft e cloud hello, creazione di una singola identità utente per l'autenticazione e autorizzazione tooall risorse, indipendentemente dalla posizione.

Altre informazioni:

* [White paper sull'identità ibrida](http://download.microsoft.com/download/D/B/A/DBA9E313-B833-48EE-998A-240AA799A8AB/Hybrid_Identity_White_Paper.pdf)
* [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)
* [Blog del team di Active Directory](https://blogs.technet.microsoft.com/ad/)
