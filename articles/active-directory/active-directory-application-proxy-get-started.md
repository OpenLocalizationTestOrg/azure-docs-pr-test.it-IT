---
title: accesso remoto sicuro aaaHow tooprovide App tooon locali
description: Descrive come toouse Proxy dell'applicazione AD Azure tooprovide accesso remoto sicuro tooyour locale delle app.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d5450da1-9e06-4d08-8146-011c84922ab5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 289e970ed0596fcd06ccf6b2ad92203366fbb494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprovide-secure-remote-access-tooon-premises-applications"></a>Come tooprovide proteggere l'accesso remoto applicazioni tooon locali

I dipendenti oggi desiderati toobe produttivi in qualsiasi luogo e in qualsiasi momento e da qualsiasi dispositivo. Desiderano toowork sui propri dispositivi mobili, siano essi laptop, Tablet o telefoni. E prevedono tooaccess in grado di toobe tutte le applicazioni locali sia le app SaaS nel cloud hello e aziendali. Accesso di applicazioni locali tooon è coinvolto in genere reti private virtuali (VPN) o zone (DMZ). Non solo sono toomake di complessi e difficili queste soluzioni sicure, ma sono costosi tooset backup e gestire.

C'è una soluzione migliore.

Una moderna forza lavoro mobile-primo hello, world cloud prima esigenza di una soluzione di accesso remoto moderna. Il proxy dell'applicazione di Azure AD è una funzionalità di Azure Active Directory che offre l'accesso remoto come servizio. Ciò significa che è facile toodeploy, utilizzare e gestire.

[!INCLUDE [identity](../../includes/azure-ad-licenses.md)]

## <a name="what-is-azure-active-directory-application-proxy"></a>Informazioni sul proxy dell'applicazione di Azure Active Directory
Il proxy dell'applicazione di Azure AD fornisce sia l'accesso Single Sign-On (SSO) sia l'accesso remoto sicuro per le applicazioni Web ospitate in locale, Alcune applicazioni è preferibile toopublish includono i siti di SharePoint, Outlook Web Access o tutte le altre applicazioni web LOB che è. Queste web locale, le applicazioni sono integrate con Azure AD, hello stessa identità e controllo piattaforma utilizzato da Office 365. Gli utenti finali possono accedere i hello applicazioni locali allo stesso modo che accedono a Office 365 e altre applicazioni SaaS integrato con Azure AD. Non necessaria infrastruttura di rete toochange hello o richiedono VPN tooprovide questa soluzione per gli utenti.

## <a name="why-is-application-proxy-a-better-solution"></a>Perché un Proxy dell'applicazione è una soluzione migliore?
Proxy dell'applicazione Azure AD fornisce un tooall soluzione economica, sicura e semplice accesso remoto alle applicazioni locali.

Il proxy di applicazione di Azure AD:

* **Simple**
   * Non necessario toochange o aggiornare toowork le applicazioni con Proxy dell'applicazione. 
   * Offre agli utenti un'esperienza di autenticazione coerente. È possibile utilizzare le app SaaS tooboth di hello MyApps tooget portale accesso single sign-on in cloud hello e App locale. 
* **Proteggere**
   * Quando si pubblicano le applicazioni mediante il Proxy di applicazione AD Azure, è possibile sfruttare i controlli di autorizzazione avanzata hello e analitica di sicurezza in Azure. Si ottiene sicurezza a livello di cloud e funzionalità di sicurezza Azure come l'accesso condizionale e la verifica in due passaggi.
   * Non è tooopen tutte le connessioni in ingresso attraverso il firewall toogive agli utenti l'accesso remoto. 
* **Convenienza**
   * Proxy dell'applicazione opera cloud hello, pertanto è possibile risparmiare tempo e denaro. Soluzioni locali in genere richiedono tooset backup e gestire le reti perimetrali, server edge o altre infrastrutture complesse.  

## <a name="what-kind-of-applications-work-with-application-proxy"></a>Quale tipo di applicazione funziona con il proxy di applicazione?
Con il proxy dell'applicazione di Azure AD è possibile accedere a tipi diversi di applicazioni interne:

* Applicazioni Web che usano l'[autenticazione integrata di Windows](active-directory-application-proxy-sso-using-kcd.md) per l'autenticazione  
* Applicazioni Web che usano l'accesso basato su form o su [intestazione](application-proxy-ping-access.md)  
* Web API che si desidera tooexpose toorich applicazioni in dispositivi diversi  
* Applicazioni ospitate dietro [Gateway Desktop remoto](application-proxy-publish-remote-desktop.md)  
* Rich client App integrate con hello Active Directory Authentication Library (ADAL)

## <a name="how-does-application-proxy-work"></a>Come funziona il proxy di applicazione?
Esistono due componenti che è necessario tooconfigure toomake lavoro Proxy dell'applicazione: un connettore e un endpoint esterno. 

connettore Hello è un agente semplice che si trova in un Server di Windows all'interno della rete. connettore Hello facilita il flusso del traffico hello da hello servizio Proxy di applicazione di hello cloud tooyour applicazione in locale. Utilizza solo le connessioni in uscita, in modo da non avere tooopen porte in ingresso o inserire qualsiasi elemento nella rete Perimetrale hello. connettori Hello sono senza stati e le informazioni dal cloud hello in base alle esigenze. Per altre informazioni sui connettori, ad esempio come bilanciano il carico ed effettuano l'autenticazione, vedere [Comprendere i connettori del proxy applicazione Azure AD](application-proxy-understand-connectors.md). 

endpoint esterni Hello è come gli utenti raggiungono le applicazioni all'esterno della rete. È possibile proseguire direttamente tooan URL esterno è determinare o accedono tramite il portale di MyApps hello applicazione hello. Quando gli utenti tooone questi endpoint, è l'autenticazione di Azure AD e quindi vengono indirizzate attraverso un'applicazione hello connettore toohello locale.

 ![Diagramma del proxy dell'applicazione di AzureAD](./media/active-directory-application-proxy-get-started/azureappproxxy.png)

1. utente Hello accede a un'applicazione hello tramite il servizio Proxy di applicazione hello ed è tooauthenticate nella pagina di accesso di Azure AD toohello diretto.
2. Dopo una corretta accesso, un token generato e inviato dispositivo client toohello.
3. client Hello invia hello toohello token servizio Proxy di applicazione, che recupera hello nome principale utente (UPN) e nome dell'entità di protezione (SPN) dal token hello, indirizza quindi il connettore del Proxy di applicazione hello richiesta toohello.
4. Se è stato configurato l'accesso single sign-on, il connettore hello esegue alcuna autenticazione aggiuntiva necessaria per conto di utente hello.
5. connettore di Hello invia un'applicazione hello richiesta toohello locale.  
6. risposta Hello viene inviato tramite Proxy applicazione del servizio e connettore toohello.

### <a name="single-sign-on"></a>Single sign-on
Proxy dell'applicazione Azure AD fornisce tooapplications single sign-on (SSO) che utilizzano l'autenticazione integrata di Windows (IWA) o le applicazioni in grado di riconoscere attestazioni. Se l'applicazione utilizza l'autenticazione integrata di Windows, il Proxy di applicazione rappresenta l'utente di hello mediante la delega vincolata Kerberos tooprovide SSO. Se si dispone di un'applicazione in grado di riconoscere attestazioni che considera attendibile Azure Active Directory, SSO funziona perché l'utente hello è già stato autenticato da Azure AD.

Per ulteriori informazioni su Kerberos, vedere [si desidera tooknow sulla delega vincolata Kerberos (KCD)](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd).

### <a name="managing-apps"></a>Gestione delle app
Uno l'app viene pubblicato con Proxy dell'applicazione, è possibile gestirlo come qualsiasi altra app aziendali in hello portale di Azure. Si può utilizzare funzioni di sicurezza di Azure Active Directory come verifica in due passaggi e di accesso condizionale, controllare le autorizzazioni utente e personalizzare hello personalizzazione per l'app. 

## <a name="get-started"></a>Attività iniziali

Prima di configurare Proxy di applicazione, assicurarsi di avere una [edizione di Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/) supportata e una directory di Azure AD di cui si è un amministratore globale.

Introduzione a Proxy di applicazione in due passaggi:

1. [Abilitare il Proxy di applicazione e configurare connettore di hello](active-directory-application-proxy-enable.md).    
2. [Pubblicare applicazioni](active-directory-application-proxy-publish.md) -utilizzare hello tooget guidata semplice e rapido applicazioni on-premise pubblicate ed è accessibile in remoto.

## <a name="whats-next"></a>Passaggi successivi
Dopo aver pubblicato la prima app, si può fare molto di più con il proxy di applicazione:

* [Abilitare l'accesso Single Sign-On](active-directory-application-proxy-sso-using-kcd.md)
* [Pubblicare applicazioni mediante il proprio nome di dominio](active-directory-application-proxy-custom-domains.md)
* [Comprendere i connettori del proxy applicazione di Azure AD](application-proxy-understand-connectors.md)
* [Usare server proxy locali esistenti](application-proxy-working-with-proxy-servers.md) 
* [Impostare una home page personalizzata](application-proxy-office365-app-launcher.md)

Per informazioni più recenti hello e gli aggiornamenti, consultare hello [blog del Proxy dell'applicazione](http://blogs.technet.com/b/applicationproxyblog/)

