---
title: tooIntegrate aaaHow con Azure Active Directory | Documenti Microsoft
description: Toobenefits una Guida di e risorse per l'integrazione con Azure Active Directory.
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: d13bba54-96bd-4b81-bee9-c8025ffa1648
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 4542965ae4a7756eda9f57e9e895f8044892f20e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-with-azure-active-directory"></a>Integrazione con Azure Active Directory
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure Active Directory fornisce alle organizzazioni una soluzione di gestione delle identità di classe enterprise per le applicazioni cloud.  Integrazione di Azure AD consente agli utenti un'esperienza di accesso ottimizzata e consente all'applicazione di criteri tooIT è conforme.

## <a name="how-toointegrate"></a>Come tooIntegrate
Esistono diversi modi per toointegrate l'applicazione con Azure AD.  Fare riferimento agli scenari seguenti a seconda dell'applicazione.

### <a name="support-azure-ad-as-a-way-toosign-in-tooyour-application"></a>Supporto di Azure AD come un modo tooSign In tooYour applicazione
**Ridurre i problemi di accesso e i costi di supporto.** Utilizzando Azure AD toosign tooyour applicazione, gli utenti non sarà possibile tooremember di nome e una password più uno.  Gli sviluppatori, verranno una minore toostore password e protezione.  Non è necessario reimpostare la password dimenticata toohandle potrebbe essere significativamente da solo.  Accedi alla base di Azure AD per alcune delle applicazioni cloud più diffusi al mondo hello, inclusi Office 365 e Microsoft Azure.  Con centinaia di milioni agli utenti di milioni di organizzazioni, probabilità sono l'utente è già connesso tooAzure Active Directory.  Altre informazioni sull'[aggiunta del supporto per l'accesso ad Azure AD](active-directory-authentication-scenarios.md).

**Semplificare l'iscrizione all'applicazione.**  Durante l'iscrizione all'applicazione, Azure AD può inviare le informazioni essenziali relative a un utente per precompilare il modulo di iscrizione o eliminarle completamente.  Gli utenti possono iscriversi per l'applicazione usando il proprio account Azure AD tramite un toothose simile esperienza di consenso familiarità trovato nel social media e applicazioni per dispositivi mobili.  Qualsiasi utente può iscriversi e accedere in tooan applicazione integrata con Azure AD senza il coinvolgimento di personale.  Altre informazioni sulla [registrazione dell'applicazione per l'accesso con l'account Azure AD](../../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md) .

### <a name="browse-for-users-manage-user-provisioning-and-control-access-tooyour-application"></a>Cerca utenti, il Provisioning dell'utente di gestire e controllare l'accesso tooYour applicazione
**Cercare gli utenti nella directory hello.**  Usare hello API Graph toohelp utenti ricerca ed esplorazione per altri utenti nell'organizzazione quando invitare altri utenti o concedere l'accesso, anziché richiedere tootype indirizzi di posta elettronica.  Gli utenti possono cercare utilizzando un'interfaccia familiare indirizzo libro stile, tra cui la visualizzazione dettagli hello di gerarchia organizzativa hello.  Altre informazioni su hello [API Graph](active-directory-graph-api.md).

**Riutilizzare i gruppi e le liste di distribuzione di Active Directory che il cliente gestisce già.**  Azure Active Directory contiene gruppi hello che il cliente è già utilizza per la distribuzione di posta elettronica e la gestione dell'accesso.  Tramite l'API Graph hello, riutilizzare questi gruppi anziché richiedere toocreate del cliente e gestire un set separato di gruppi nell'applicazione.  Informazioni sui gruppi possono anche essere inviati tooyour applicazione nel token di accesso.  Altre informazioni su hello [API Graph](active-directory-graph-api.md).

**Utilizzare toocontrol di Azure AD che ha accesso tooyour applicazione.**  Gli amministratori e i proprietari delle applicazioni in Azure AD possono assegnare accesso tooapplications toospecific utenti e gruppi.  Utilizza hello API Graph, è possibile leggere l'elenco e utilizzarlo toocontrol provisioning e deprovisioning delle risorse e accedere all'interno dell'applicazione.

**Usare Azure AD per il controllo degli accessi in base al ruolo.**  Gli amministratori e i proprietari delle applicazioni possono assegnare utenti e gruppi tooroles definiti quando si registra l'applicazione in Azure AD.  Le informazioni sui ruoli viene inviate tooyour applicazione nel token di accesso e possono anche essere letto utilizzando un hello API Graph.  Altre informazioni sull' [uso di Azure AD per l'autorizzazione](http://blogs.technet.com/b/ad/archive/2014/12/18/azure-active-directory-now-with-group-claims-and-application-roles.aspx).

### <a name="get-access-toousers-profile-calendar-email-contacts-files-and-more"></a>Profilo del tooUser di accesso get, calendario, posta elettronica, contatti, file e altro ancora
**Azure AD è il server di autorizzazione hello per Office 365 e altri servizi aziendali Microsoft.**  Se si supportano Azure AD per l'accesso tooyour applicazione o l'utente account tooAzure AD account utente correnti mediante OAuth 2.0 il collegamento al supporto, è possibile richiedere di lettura e dell'utente di accesso in scrittura tooa profilo, calendario, posta elettronica, contatti, file e altre informazioni.  È facilmente possibile calendario del toouser eventi, scrivere e leggere o scrivere file tootheir OneDrive.  Altre informazioni, vedere [accesso hello API di Office 365](https://msdn.microsoft.com/office/office365/howto/platform-development-overview).

### <a name="promote-your-application-in-hello-azure-and-office-365-marketplaces"></a>Alzare di livello dell'applicazione in Azure hello e Office 365 Marketplace
**Alzare di livello il toohello applicazione milioni di organizzazioni che già usano Azure AD.**  Gli utenti che esplorano questi Marketplace usano già uno o più servizi cloud, di conseguenza rappresentano il pubblico di destinazione ideale per l'applicazione.  Ulteriori informazioni sull'innalzamento di livello applicazione in [hello Azure Marketplace](https://azure.microsoft.com/marketplace/partner-program/).

**Quando gli utenti effettuano l'iscrizione all'applicazione, questa verrà visualizzata nel riquadro di accesso di Azure AD e nell'icona di avvio delle app di Office 365.**  Gli utenti saranno in grado di tooquickly e applicazione tooyour facilmente restituito in un secondo momento, migliorare il coinvolgimento degli utenti.  Altre informazioni su hello [Pannello di accesso AD Azure](../active-directory-saas-access-panel-introduction.md).

### <a name="secure-device-to-service-and-service-to-service-communication"></a>Comunicazione da dispositivo a servizio e da servizio a servizio sicura
**L'utilizzo di Azure AD per la gestione di identità dei dispositivi e servizi riduce codice hello necessario toowrite e consente l'accesso toomanage IT.**  Dispositivi e servizi possono ottenere i token da Azure AD tramite OAuth e utilizzare tali API web di tooaccess di token.  L'uso di Azure AD consente di evitare la scrittura di codice di autenticazione complesso.  Poiché l'identità di hello dei dispositivi e servizi hello vengono archiviate in Azure AD, IT possono gestire le chiavi e revoche di certificati in un'unica posizione, anziché toodo questo separatamente nell'applicazione.

## <a name="benefits-of-integration"></a>Vantaggi dell'integrazione
Integrazione con Azure AD viene fornito con i vantaggi che non richiedono codice aggiuntivo toowrite.

### <a name="integration-with-enterprise-identity-management"></a>Integrazione con il sistema di gestione delle identità aziendale
**Conformità dell'applicazione ai criteri IT.**  Le organizzazioni di integrare i sistemi di gestione di identità enterprise con Azure AD, in modo quando un utente lascia l'organizzazione, che verrà automaticamente perdano l'accesso tooyour applicazione senza IT che dover tootake passaggi aggiuntivi.  IT può gestire chi può accedere all'applicazione e determinare quali criteri di accesso necessari - multi-factor Authentication di esempio - riducendo il toocomply di codice necessario toowrite ai criteri aziendali complessi.  Azure Active Directory fornisce agli amministratori di un log di controllo dettagliato di che ha effettuato l'accesso tooyour applicazione così IT può tenere traccia dell'utilizzo.

**Azure AD estende cloud toohello Active Directory in modo che l'applicazione può essere integrato con Active Directory.**  Molte organizzazioni in tutto il mondo hello utilizzano Active Directory come Accedi principale e il sistema di gestione di identità e richiedono toowork loro applicazioni con Active Directory.  L'integrazione con Azure AD integra l'app con Active Directory.

### <a name="advanced-security-features"></a>Funzionalità di sicurezza avanzate
**Autenticazione a più fattori**  Azure AD offre l'autenticazione a più fattori nativa.  Gli amministratori IT tooaccess multi-factor authentication possono richiedere l'applicazione, in modo che non si dispone toocode questo supporto manualmente.  Altre informazioni su [Multi-Factor Authentication](https://azure.microsoft.com/documentation/services/multi-factor-authentication/).

**Rilevamento di attività di accesso con anomalie.**  Azure AD elabora più di un miliardo accessi al giorno, durante l'utilizzo macchina attività sospette toodetect di algoritmi di apprendimento e la notifica agli amministratori IT di possibili problemi.  Grazie al supporto Accedi AD Azure, l'applicazione ottiene il vantaggio di hello di questo tipo di protezione. Altre informazioni sulla [visualizzazione del report di accesso di Azure Active Directory](../active-directory-view-access-usage-reports.md).

**Accesso condizionale.**  Inoltre l'autenticazione a fattore toomulti, gli amministratori possono richiedere che vengano soddisfatte le condizioni specifiche prima che gli utenti possono Accedi tooyour applicazione.  Le condizioni che possono essere impostate includono l'intervallo di indirizzi IP hello di dispositivi client, l'appartenenza in gruppi specificati e lo stato di hello del dispositivo hello utilizzato per l'accesso.  Altre informazioni sull'[accesso condizionale di Azure Active Directory](../active-directory-conditional-access.md).

### <a name="easy-development"></a>Sviluppo semplificato
**Protocolli standard del settore.**  Microsoft è eseguito il commit toosupporting standard del settore.  Azure AD supporta i protocolli di autenticazione SAML 2.0, OpenID Connect 1.0, OAuth 2.0 e WS-Federation 1.2 hello.  Hello API Graph è conforme a OData 4.0.  Se l'applicazione già supporta protocolli di OpenID Connect 1.0 o hello SAML 2.0 per l'accesso federato, l'aggiunta del supporto per Azure AD può essere semplice.  Altre informazioni sui [protocolli di autenticazione supportati da Azure AD](active-directory-authentication-protocols.md).

**Librerie open source.**  Microsoft fornisce librerie open source completamente supportato per lo sviluppo toospeed linguaggi e piattaforme più diffuso.  codice sorgente Hello è concesso in licenza in Apache 2.0, si stanno toofork gratuita e contribuiscono progetti toohello indietro.  Altre informazioni sulle [librerie di autenticazione di Azure AD](active-directory-authentication-libraries.md).

### <a name="worldwide-presence-and-high-availability"></a>Presenza a livello globale e disponibilità elevata
**Azure AD viene distribuito in Data Center di tutto il mondo hello e gestito e monitorato intorno clock hello.**  Azure AD è hello identità di sistema di gestione per Microsoft Azure e Office 365 e viene distribuito in data 28 Center tutto il mondo hello.  Dati della directory sono garantiti toobe replicati tooat almeno tre datacenter.  Servizi di bilanciamento del carico globale garantire che gli utenti accedono copia più vicino di hello di Azure Active Directory che contiene i dati e automaticamente reindirizza le richieste Data Center tooother se viene rilevato un problema.

## <a name="next-steps"></a>Passaggi successivi
[Introduzione alla scrittura di codice](active-directory-developers-guide.md#get-started).

[Accesso degli utenti tramite Azure AD](active-directory-authentication-scenarios.md)

