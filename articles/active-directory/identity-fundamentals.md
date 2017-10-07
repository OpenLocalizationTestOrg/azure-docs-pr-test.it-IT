---
title: "aaaFundamentals della gestione delle identità di Azure | Documenti Microsoft"
description: 
keywords: 
author: jeffgilb
manager: femila
ms.reviewr: jsnow
ms.author: jeffgilb
ms.date: 7/5/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: a9710b8e543cdbb2f78ea9e3f83b183e1983b31d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="fundamentals-of-azure-identity-management"></a>Concetti fondamentali sulla gestione delle identità di Azure
Maggiore di risorse digitali aziendali in tempo reale all'esterno di hello rete aziendale, nel cloud hello e nei dispositivi, una grande basato su cloud identità e accessi soluzione di gestione è sempre una necessità. Identità basate su cloud sono ora controllo toomaintain modo migliore di hello over e visibilità, come e quando gli utenti accedere alle applicazioni aziendali e dati.

Microsoft è stato protezione identità basate su cloud per oltre un decennio e ora, con [Azure Active Directory (AD)](https://docs.microsoft.com/azure/active-directory/active-directory-editions), questi stessi sistemi di protezione sono tooyou disponibili. Azure AD permette agli amministratori dell'organizzazione di assicurare facilmente la responsabilità di utenti e amministratori, migliorando notevolmente la sicurezza e la governance.

Azure AD Premium è una basato su cloud identità e accessi soluzione di gestione con le funzionalità di protezione dati avanzata che consente un'identità di protezione per tutte le app, la protezione dell'identità (migliorata hello [grafico di sicurezza di Microsoft Business intelligence](https://www.microsoft.com/en-us/security/intelligence)) e gestione di identità con privilegi. Un altro monitoraggio o reporting strumento Azure AD Premium è possibile proteggere le identità dell'utente in tempo reale e abilitare si toocreate adattiva, basati sui rischi di accesso criteri tooprotect i dati dell'organizzazione.

Questo breve video offre una rapida panoramica delle funzionalità di protezione e gestione delle identità di Azure AD:
<iframe width="560" height="315" src="https://www.youtube.com/embed/9LGIJ2-FKIM" frameborder="0" allowfullscreen></iframe>

Microsoft non solo fornisce un'identità che consente di accedere ovunque, ma anche un set di strumenti tooautomate, proteggere e gestire IT all'interno dell'organizzazione. Anche dopo l'introduzione di hello del cloud computing, è comunque richiesta toomanage e controllare le attività IT come helpdesk chiama tooreset le password utente, utente gruppo di gestione e le richieste dell'applicazione. Complicare ulteriormente le cose, i dipendenti sono ora riportare toowork loro dispositivi personali e utilizzo delle applicazioni SaaS immediatamente disponibili. Mantenere il controllo sulle applicazioni nei data center aziendali e nelle piattaforme cloud pubbliche diventa sempre più difficile.

[!INCLUDE [identity](../../includes/azure-ad-licenses.md)]

## <a name="connect-on-premises-active-directory-with-azure-ad-and-office-365"></a>Connettere Active Directory locale con Azure AD e Office 365
Le organizzazioni che hanno apportato grandi investimenti in Active Directory locale possono estendere tali cloud toohello investimenti integrando le directory locali con Azure AD in [la gestione delle identità ibrida](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview). In questo modo è possibile aumentare la produttività degli utenti grazie a un'identità comune per l'accesso alle risorse, indipendentemente dalla località. Gli utenti e organizzazioni possono quindi utilizzare single sign-on (SSO) tooaccess entrambe le risorse locali e nel cloud servizi come Office 365.

[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) è hello solo strumento è necessario integrazione hello tooget eseguita. Azure AD Connect offre funzionalità toosupport la sincronizzazione delle identità è necessario e sostituisce le versioni precedenti di strumenti di integrazione di identità, ad esempio DirSync e Azure AD Sync. Con Azure AD Connect, la sincronizzazione e la gestione delle identità tra istanze locali e Azure AD è resa possibile da:

- Sincronizzazione: questo componente è responsabile della creazione di utenti, gruppi e altri oggetti. È inoltre responsabile di garantire che le informazioni di identità per gli utenti locali e i gruppi corrispondenti cloud hello. Write-back password può essere anche tookeep abilitato nelle directory locali sincronizzati quando un utente aggiorna la propria password in Azure AD.
- AD FS - federazione è una funzionalità facoltativa fornita da Azure AD Connect che possono essere utilizzati tooconfigure un ambiente ibrido usando una locale infrastruttura ADFS. Federazione può essere utilizzata da organizzazioni tooaddress eseguire distribuzioni complesse, ad esempio single sign-on, l'applicazione di criteri di Active Directory, accesso e delle smart card o di terze parti, autenticazione a più fattori.
- Monitoraggio integrità - [Azure AD Connect Health](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health) possibile forniscono un monitoraggio efficace e fornire una posizione centrale in hello tooview portale Azure questa attività.

## <a name="increase-productivity-and-reduce-helpdesk-costs-with-self-service-and-single-sign-on-experiences"></a>Aumentare la produttività e ridurre i costi di supporto tecnico con esperienze self-service e Single Sign-On

I dipendenti sono più produttivi quando dispongono di un singolo tooremember nome utente e password e un'esperienza coerente da ogni dispositivo. Consentono inoltre di risparmiare tempo quando eseguono attività self-service, ad esempio [reimpostare una password dimenticata](https://docs.microsoft.com/azure/active-directory/active-directory-passwords) o la richiesta di accesso tooan applicazione senza attendere che l'assistenza del supporto tecnico di hello.

Azure AD [estende in locale di Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) in cloud hello, abilitazione degli utenti toouse proprio account aziendale primario per i dispositivi appartenenti a un dominio, alle risorse aziendali sia tutti web hello e le applicazioni SaaS necessario toouse tooget il proprio lavoro. Inoltre toonot con tooremember più set di nomi utente e password, l'accesso alle applicazioni degli utenti possono anche essere automaticamente il provisioning (o deprovisioning) basate sull'appartenenza ai gruppi dell'organizzazione e il relativo stato di un dipendente. Ed è possibile controllare che l'accesso per le app di raccolta o per la propria App locali sviluppate e pubblicate tramite hello [Proxy dell'applicazione AD Azure](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

## <a name="manage-and-control-access-toocorporate-resources"></a>Gestire e controllare l'accesso alle risorse di toocorporate
Identità e accessi Gestione soluzioni Guida di Microsoft IT proteggere tooapplications di accesso e le risorse tra data center aziendale hello e nel cloud hello, abilitare ulteriori livelli di convalida, ad esempio [multi-factor authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next) e [criteri di accesso condizionale](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). Il monitoraggio delle attività sospette tramite funzioni avanzate di report di sicurezza, controllo e avvisi consente di attenuare i potenziali problemi di sicurezza.

Criteri di accesso condizionale in Azure AD Premium offrono hello gruppi enterprise Admins, hello regole di accesso basata su criteri toocreate possibilità per qualsiasi applicazione connesso AD Azure (app SaaS, le applicazioni personalizzate in esecuzione in applicazioni web locale o cloud di hello). Azure AD restituisce questi criteri in tempo reale e applicarle tramite ogni volta che un utente tenta di tooaccess un'applicazione. Criteri di protezione di identità di Azure consentono di intraprendere l'azione tooautomatically se viene individuata un'attività sospetta. Queste azioni possono includere accesso toousers ad alto rischio, imporre l'autenticazione a più fattori, di blocco e reimpostazione password utente se sembra che le credenziali sono stati compromessi.


## <a name="azure-active-directory-privileged-identity-management"></a>Azure Active Directory Privileged Identity Management

[Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-getting-started), incluso in Azure Active Directory Premium P2 hello offerta consente toodiscover, limitare e monitorare gli account amministrativi e i relativi tooresources di accesso in Azure Active Directory e altro Servizi online Microsoft. Consente inoltre di amministrare su richiesta accesso amministrativo per hello esatto periodo che è necessario.

Privileged Identity Management può applicare i diritti di amministratore su richiesta in modo che gli amministratori possono richiedere multi-factor autenticato, temporaneo l'elevazione dei propri privilegi per preconfigurato periodi di tempo prima che gli account restituiscono tooa normale stato utente.

## <a name="benefits-of-azure-identity"></a>Vantaggi della gestione delle identità di Azure

La gestione delle identità di Azure permette di:

-   Creare e gestire un'identità unica per ogni utente in tutta l'azienda, mantenendo utenti, gruppi e dispositivi sincronizzati con [Azure Active Directory Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

-   Fornire l'accesso single sign-on tooyour applicazioni tra migliaia di applicazioni SaaS preintegrate o fornire l'accesso remoto sicuro applicazioni SaaS tooon locale utilizzando hello [Proxy dell'applicazione AD Azure](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

-   Abilitare la sicurezza dell'accesso alle applicazioni grazie all'[autenticazione a più fattori](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next) basata su regole per applicazioni locali e cloud.

-   Migliorare la produttività degli utenti con [di reimpostazione della password self-service](https://docs.microsoft.com/azure/active-directory/active-directory-passwords)e il gruppo e applicazione hello utilizzando richieste di accesso [MyApps portale](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-user-help).

-   Sfruttare i vantaggi di hello [ad alta disponibilità e affidabilità](https://docs.microsoft.com/azure/architecture/resiliency/high-availability-azure-applications) di un livello mondiale, aziendale, basato su cloud identità e accessi soluzione di gestione.

## <a name="next-steps"></a>Passaggi successivi
[Altre informazioni sulle soluzioni per la gestione delle identità di Azure](https://docs.microsoft.com/azure/active-directory/understand-azure-identity-solutions)