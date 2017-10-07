---
title: flusso di concessione aaaUnderstanding hello implicita OAuth2 di Azure AD | Documenti Microsoft
description: "Ulteriori informazioni sull'implementazione del Azure Active Directory flusso di concessione implicita OAuth2 hello e se è adatta all'applicazione."
services: active-directory
documentationcenter: dev-center-name
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 90e42ff9-43b0-4b4f-a222-51df847b2a8d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/15/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 3402e6619709e1a5b1e790ffd79dc62139552d9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-oauth2-implicit-grant-flow-in-azure-active-directory-ad"></a>Hello conoscenza implicita OAuth2 concedere flusso in Azure Active Directory (AD)
la concessione implicita OAuth2 Hello è noto per la concessione di hello con elenco più lungo di hello di problemi di sicurezza nella specifica OAuth2 hello. E ancora, che è l'approccio hello implementata ADAL JS e hello uno che è consigliabile quando si scrivono applicazioni SPA. Quali sono i vantaggi? Si tratta tutti di compromessi: e in realtà, la concessione implicita hello è consigliabile hello è possibile seguire per le applicazioni che utilizzano un'API Web tramite JavaScript da un browser.

## <a name="what-is-hello-oauth2-implicit-grant"></a>Che cos'è la concessione implicita OAuth2 hello?
Hello tipico [concessione del codice di autorizzazione OAuth2](https://tools.ietf.org/html/rfc6749#section-1.3.1) è hello autorizzazione grant che utilizza due endpoint separati. endpoint di autorizzazione Hello viene utilizzato per la fase di interazione utente hello, che comporta un codice di autorizzazione. endpoint token Hello viene quindi utilizzato dal client hello per lo scambio di codice hello per un token di accesso e spesso anche un token di aggiornamento. Le applicazioni Web sono necessari toopresent le proprie credenziali toohello token endpoint dell'applicazione, in modo che hello server di autorizzazione può autenticare hello client.

Hello [concessione implicita OAuth2](https://tools.ietf.org/html/rfc6749#section-1.3.2) è una variante di altri concede l'autorizzazione. Consente un tooobtain client a un token di accesso (id_token, quando si utilizza e [OpenId Connect](http://openid.net/specs/openid-connect-core-1_0.html)) direttamente dall'endpoint di autorizzazione di hello, senza contattare endpoint token hello né l'autenticazione client hello. Questa variante è stato appositamente progettata per applicazioni in esecuzione in un browser Web basate su JavaScript: nella specifica OAuth2 originale di hello, i token vengono restituiti in un frammento URI. Bits token hello che effettua il codice JavaScript toohello disponibile nel client hello, ma garantisce che non verranno inclusi in reindirizzamenti verso server hello. Restituzione di token tramite browser reindirizza direttamente dall'endpoint di autorizzazione hello. Include inoltre il vantaggio di hello di eliminare tutti i requisiti per tra chiamate di origine, sono necessari se hello applicazione JavaScript è obbligatorio toocontact hello endpoint del token.

Un'importante caratteristica di concessione implicita OAuth2 hello è hello tali flussi non restituiscono mai client toohello i token di aggiornamento. Come verrà illustrato nella sezione successiva di hello, che non è necessario e sarebbe infatti un problema di sicurezza.

## <a name="suitable-scenarios-for-hello-oauth2-implicit-grant"></a>Scenari più appropriati per hello implicita OAuth2 concedere
Come hello OAuth2 specifica dichiara, hello concessione implicita è stato elaborato tooenable agente utente applicazioni che è toosay, applicazioni JavaScript in esecuzione all'interno di un browser. definizione di una caratteristica di tali applicazioni Hello è codice JavaScript viene utilizzato per accedere alle risorse di server (in genere un'API Web) e per l'aggiornamento di un'applicazione hello UX conseguenza. Si tratta di applicazioni, ad esempio Gmail o Outlook Web Access: quando si seleziona un messaggio dalla posta in arrivo, l'unico messaggio hello del Pannello di visualizzazione modifiche toodisplay hello nuova selezione, mentre altri hello della pagina hello rimane invariato. Equivale a differenza delle applicazioni Web basate su reindirizzamento tradizionali, in cui ogni interazione dell'utente comporta un postback dell'intera pagina e un rendering a pagina intera hello nuovo della risposta del server.

Applicazioni che accettano estremi hello basata su JavaScript approccio tooits vengono chiamate applicazioni a pagina singola o stabilimenti termali: idea hello è che le applicazioni solo essere usata una pagina iniziale di HTML e JavaScript associata, con tutte le interazioni successive attivate da Le chiamate API Web eseguite tramite JavaScript. Tuttavia, approcci ibrida, in cui un'applicazione hello è in genere basate sui postback ma esegue chiamate JS occasionali, non sono più comuni: discussione hello sull'utilizzo del flusso implicito è pertinente per quelli anche.

Le applicazioni basate sul reindirizzamento in genere proteggono le richieste tramite cookie, tuttavia questo approccio non funziona anche per le applicazioni JavaScript. I cookie funzionano solo con il dominio hello che sono stati generati, mentre le chiamate JavaScript potrebbero essere dirette verso altri domini. In effetti, che sarà spesso case hello: si tratta di applicazioni chiamata API dell'API Graph API di Office, Microsoft Azure-tutti che si trovano all'esterno del dominio hello da gestito in cui un'applicazione hello. Una crescente tendenza per le applicazioni JavaScript non è toohave alcun back-end, basarsi 100% a 3rd party API Web tooimplement le relative funzioni di business.

Attualmente, hello metodo preferito per la protezione tooa chiamate API Web è toouse hello OAuth2 connessione token approccio, in cui un token di accesso OAuth2 associato a ogni chiamata. API Web Hello esamina il token di accesso in ingresso hello e, se si trova in hello ambiti necessari, concede l'accesso toohello ha richiesto l'operazione. flusso implicito Hello fornisce un meccanismo efficace per le applicazioni JavaScript tooobtain i token di accesso per un'API Web, offre che numerosi vantaggi in rispettano toocookies:

* Token possono essere ottenuti in modo affidabile senza necessità di cross-origin chiamate: registrazione obbligatoria di toowhich URI di reindirizzamento hello sono restituire i token garantisce che i token non vengono spostati
* Le applicazioni JavaScript possono ottenere tutti i token di accesso necessari per tutte le API Web di destinazione, senza alcuna restrizione sui domini.
* Le funzionalità di HTML5 come sessione o l'archiviazione locale concedere controllo completo sulla memorizzazione nella cache di token e la gestione della durata, mentre la gestione dei cookie è opaco toohello app
* I token di accesso non sono attacchi sensibili tooCross-site request forgery (CSRF)

flusso di concessione implicita Hello non emette token di aggiornamento, soprattutto per motivi di sicurezza. Poiché l'ambito di un token di aggiornamento non è così ristretto come quello dei token di accesso, offre potenzialità decisamente maggiori, ma crea anche molti più danni se passa all'esterno. Nel flusso implicito hello, i token vengono recapitati in URL hello e pertanto il rischio di hello di intercettazione superiore hello concessione del codice.

Si noti tuttavia che un'applicazione JavaScript ha un altro meccanismo a disposizione per rinnovare il token di accesso senza richiedere più volte le credenziali utente hello. Hello applicazione può utilizzare un iframe nascosto tooperform nuove richieste di token di endpoint di autorizzazione hello di Azure AD: come browser hello dispone ancora di una sessione attiva (lettura: dispone di un cookie di sessione) in dominio hello Azure AD, hello richiesta di autenticazione può essere eseguito senza necessità di interazione dell'utente.

Questo modello consente hello JavaScript applicazione hello tooindependently rinnovare i token di accesso e anche acquisire nuovi per una nuova API (a condizione che hello utente precedentemente accettato le condizioni per loro. Questo evita di carico di lavoro aggiunto hello di acquisizione, la gestione e protezione di un elemento di valore elevato, ad esempio un token di aggiornamento. elemento di Hello che rende possibile, il rinnovo invisibile all'utente di hello cookie di sessione hello Azure AD, viene gestita all'esterno di un'applicazione hello. Un altro vantaggio di questo approccio è che un utente può disconnettersi da Azure AD, tramite un'applicazione hello effettuati l'accesso AD Azure, in esecuzione in una delle schede del browser hello. Ciò comporta l'eliminazione di hello del cookie di sessione hello Azure AD e hello applicazione JavaScript automaticamente perderanno il possibilità hello token toorenew hello effettuata la disconnessione utente.

## <a name="is-hello-implicit-grant-suitable-for-my-app"></a>È la concessione implicita hello adatto per la mia applicazione?
concessione implicita Hello presenta ulteriori rischi maggiori altri concessioni e aree hello occorre toopay attenzione tooare ben documentata. Ad esempio, [tooImpersonate utilizzo improprio del Token di accesso proprietario della risorsa nel flusso implicito] [ OAuth2-Spec-Implicit-Misuse] e [modello di minaccia di OAuth 2.0 e considerazioni sulla sicurezza] [ OAuth2-Threat-Model-And-Security-Implications]). Tuttavia, il profilo di rischio superiore hello è in gran parte a causa di fatto toohello che ha lo scopo tooenable applicazioni che eseguono codice attiva, gestite da un browser tooa risorsa remota. Se si intende un'architettura SPA, non dispone di alcun componente di back-end o intenda tooinvoke un'API Web tramite JavaScript, è consigliabile usare per l'acquisizione del token di flusso implicito hello.

Se l'applicazione è un client nativo, flusso implicito hello non è un'ottima soluzione. assenza di Hello di cookie di sessione hello Azure AD nel contesto di hello del client nativi priva dell'applicazione da mezzo hello di gestione di una sessione di lunga durata. Ovvero l'applicazione ripetutamente richiederà hello utente quando si ottengono i token di accesso per le nuove risorse.

Se si sviluppa un'applicazione Web che include un back-end e l'utilizzo di un'API dal relativo codice di back-end, flusso implicito hello non è una scelta ottimale. Altre concessioni offrono molte più possibilità. Concessione di credenziali client hello OAuth2, ad esempio, fornisce i token tooobtain hello possibilità che riflettono le autorizzazioni di hello assegnato toohello applicazione stessa, come le deleghe toouser anziché. Ciò significa client hello ha hello possibilità toomaintain l'accesso programmatico tooresources anche quando l'utente non è attivamente impegnato in una sessione e così via. Tali concessioni offrono poi anche maggiori garanzie di sicurezza. Ad esempio, i token di accesso di transito mai tramite browser utente hello, non viene salvato nella cronologia del browser hello dei rischi e così via. un'applicazione Hello client può anche eseguire l'autenticazione avanzata quando si richiede un token.

## <a name="next-steps"></a>Passaggi successivi
* Per un elenco completo delle risorse per sviluppatori, tra cui informazioni di riferimento per i protocolli di hello e l'autorizzazione OAuth2 concedere supporto flussi da Azure AD, vedere toohello [Guida per gli sviluppatori di Azure AD][AAD-Developers-Guide]
* Vedere [come un'applicazione con Azure AD toointegrate] [ ACOM-How-To-Integrate] per profondità aggiuntive sul processo di integrazione dell'applicazione hello.

<!--Image references-->

<!--Reference style links in use-->
[AAD-Developers-Guide]: active-directory-developers-guide.md
[ACOM-How-And-Why-Apps-Added-To-AAD]: active-directory-how-applications-are-added.md
[ACOM-How-To-Integrate]: active-directory-how-to-integrate.md
[OAuth2-Spec-Implicit-Misuse]: https://tools.ietf.org/html/rfc6749#section-10.16
[OAuth2-Threat-Model-And-Security-Implications]: https://tools.ietf.org/html/rfc6819
