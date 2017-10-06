---
title: aaaGet avviato l'integrazione di Azure AD con le app | Documenti Microsoft
description: "Questo articolo è una guida introduttiva per l'integrazione di Azure Active Directory (AD) con applicazioni locali e applicazioni cloud."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: db6d210d-c970-49e9-bd20-36d984bcd1c3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: 5a7a851e8418083fee72ab58477a9cab75d0d4bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-active-directory-with-applications-getting-started-guide"></a>Guida introduttiva all'integrazione di Azure Active Directory con le applicazioni
## <a name="overview"></a>Panoramica
In questo argomento è toogive previsto è una Guida di orientamento per l'integrazione di applicazioni con Azure Active Directory (AD). Allo scopo di individuare quali parti di questa Guida introduttiva sono tooyou pertinenti, ognuno dei hello nelle sezioni seguenti vengono contenere un breve riepilogo di un argomento più dettagliato.  Seguire i collegamenti di hello per un approfondimento su ciascun argomento.

## <a name="before-you-begin-take-inventory"></a>Considerazioni preliminari
Prima di passare in toointegrating applicazioni con Azure AD, è importante tooknow in cui si ha e dove si desidera toogo.  Hello domande seguenti sono previsti toohelp si pensa di progetto di integrazione dell'applicazione Azure AD.

### <a name="application-inventory"></a>Inventario delle applicazioni
* Dove si trovano tutte le applicazioni? Quali sono i proprietari?
* Che tipo di autenticazione richiedono le applicazioni?
* Che deve accedere ad applicazioni di toowhich?
* Specificare se toodeploy una nuova applicazione.
  * L'applicazione verrà compilata internamente e distribuita in un'istanza di calcolo di Azure?
  * Si userà uno disponibile nella raccolta di applicazioni Azure hello?

### <a name="user-and-group-inventory"></a>Inventario di utenti e gruppi
* Dove si trovano gli account utente?
  * Active Directory locale
  * Azure AD
  * In un database dell'applicazione separato di proprietà dell'utente
  * In applicazioni non approvate
  * Tutti i precedente hello
* Quali autorizzazioni e assegnazioni di ruoli hanno attualmente i singoli utenti? È necessario tooreview l'accesso o si certi che le assegnazioni di ruolo e l'accesso utente sono ora appropriate?
* Sono già stati definiti gruppi in Active Directory locale?
  * In che modo sono organizzati i gruppi?
  * Chi sono i membri del gruppo hello?
  * Le assegnazioni di autorizzazioni o il ruolo gruppi hello attualmente dispone?
* È necessario tooclean dei database utente/gruppo prima di integrazione?  Questa è una domanda molto importante. La qualità del risultato dipende dalla qualità dei dati di partenza.

### <a name="access-management-inventory"></a>Inventario della gestione degli accessi
* Come si gestiscono attualmente i tooapplications di accesso utente? Che necessita di toochange?  Sono stati considerati altre modalità di accesso toomanage, ad esempio con [RBAC](role-based-access-control-configure.md) ad esempio?
* Chi deve toowhat accesso?

Forse tooall risposte hello di queste domande non è in anticipo, ma che non costituisce un problema.  Questa guida è utile per rispondere ad alcune domande e prendere decisioni informate.

## <a name="prerequisites"></a>Prerequisiti
* Una sottoscrizione di Azure e una directory di Azure Active Directory.  Se non si ha ancora una sottoscrizione di Azure, è possibile ottenere una versione di prova gratuita di Azure per 30 giorni. [provarlo,](https://azure.microsoft.com/trial/get-started-active-directory/)

## <a name="application-integration-with-azure-ad"></a>Integrazione delle applicazioni con Azure AD
### <a name="finding-unsanctioned-cloud-applications-with-cloud-app-discovery"></a>Ricerca di applicazioni cloud non autorizzate con Cloud App Discovery
Come indicato in precedenza, è possibile che alcune applicazioni non siano state gestite dall'organizzazione fino a oggi.  Come parte del processo di inventario hello, è possibile toofind non approvata le applicazioni cloud. Vedere [Ricerca di applicazioni cloud non autorizzate con Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).

### <a name="authentication-types"></a>Tipi di autenticazione
È possibile che ogni applicazione abbia requisiti di autenticazione diversi. Con Azure AD la firma dei certificati può essere usata con applicazioni che usano i protocolli di connessione SAML 2.0, WS-Federation oppure OpenID, oltre a Password Single Sign-On. Per altre informazioni sui tipi di autenticazione per le applicazioni che possono essere usati con Azure AD, vedere [Gestione di certificati per Single Sign-On federato in Azure Active Directory](active-directory-sso-certs.md) e [Accesso Single Sign-On basato su password](active-directory-appssoaccess-whatis.md).

### <a name="enabling-sso-with-azure-ad-app-proxy"></a>Abilitazione di SSO con il proxy dell'app di Azure AD
Proxy di applicazione di Microsoft Azure AD, è possibile fornire accesso tooapplications si trova all'interno della rete privata in modo sicuro, ovunque e su qualsiasi dispositivo. Dopo aver installato un connettore del proxy di applicazione all'interno dell'ambiente, è possibile configurarlo facilmente con Azure AD.

### <a name="integrating-applications-with-azure-ad"></a>Integrazione di applicazioni con Azure AD
Hello articoli seguenti illustrano modi diversi di hello applicazioni si integrano con Azure AD e forniscono alcune indicazioni.

* [Determinare quali toouse di Active Directory](active-directory-administer.md)
* [Utilizzo di applicazioni in una raccolta di applicazioni Azure hello](active-directory-appssoaccess-whatis.md)
* [Elenco delle esercitazioni sull'integrazione di applicazioni SaaS](active-directory-saas-tutorial-list.md)

## <a name="managing-access-tooapplications"></a>La gestione di accesso tooapplications
Hello articoli seguenti descrivono modi per gestire l'accesso tooapplications dopo che sono state integrate con Azure Active Directory utilizzando i connettori di Azure AD e Azure AD.

* [La gestione di accesso tooapps mediante Azure AD](active-directory-managing-access-to-apps.md)
* [Automazione con i connettori di Azure AD](active-directory-saas-app-provisioning.md)
* [Assegnazione di utenti applicazione tooan](active-directory-applications-guiding-developers-assigning-users.md)
* [Assegnazione di gruppi di applicazioni tooan](active-directory-applications-guiding-developers-assigning-groups.md)
* [Condivisione di account](active-directory-sharing-accounts.md)

## <a name="integrating-custom-applications"></a>Integrazione di applicazioni personalizzate
Se si sta creando una nuova applicazione e si desidera che gli sviluppatori tooassist all'utilizzo di energia hello Azure AD, vedere [orientamenti sviluppatori](active-directory-applications-guiding-developers-for-lob-applications.md).

Se si desidera tooadd il toohello applicazione personalizzata, la raccolta di applicazioni Azure, vedere ["Bring la propria app" con la configurazione SAML del Self-Service di Azure AD](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).

## <a name="see-also"></a>Vedere anche
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)

