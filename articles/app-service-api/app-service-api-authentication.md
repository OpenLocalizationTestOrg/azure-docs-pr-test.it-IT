---
title: aaaAuthentication e l'autorizzazione per App per le API in Azure App Service | Documenti Microsoft
description: Informazioni sui servizi di autenticazione e autorizzazione di hello forniti dal servizio App di Azure per App per le API.
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: d620b53a-5a6f-41c9-84c7-f7ef5ff02ae7
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: alkarche
ms.openlocfilehash: 6d26754b8b606ec232a74768787922ea80577c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-api-apps-in-azure-app-service"></a>Autenticazione e autorizzazione per app per le API nel servizio app di Azure
## <a name="overview"></a>Panoramica
> [!NOTE]
> In questo argomento sarà migrato tooa consolidato [l'autenticazione del servizio App / autorizzazione](../app-service/app-service-authentication-overview.md) argomento riguardante Web, dispositivi mobili e App per le API.
> 
> 

Il servizio app di Azure offre servizi di autenticazione e autorizzazione predefiniti che implementano [OAuth 2.0](#oauth) e [OpenID Connect](#oauth). In questo articolo vengono illustrati i servizi di hello e le opzioni disponibili per App per le API in Azure App Service.

Hello seguente diagramma vengono illustrate alcune caratteristiche chiave di autenticazione del servizio App:

* Pre-elabora le richieste API in ingresso, quindi usa qualsiasi linguaggio o framework supportato dal servizio app.
* Offre diverse opzioni per l'autenticazione di quanto lavoro è necessario toodo nel codice.
* Funziona per l'autenticazione sia dell'utente finale che dell'account del servizio. 
* Supporta cinque provider di identità: Azure Active Directory, Facebook, Google, Twitter e account Microsoft.
* Il funzionamento stesso hello per le App per le API, applicazioni Web e App per dispositivi mobili.

![](./media/app-service-api-authentication/api-apps-overview.png)

## <a name="language-agnostic"></a>Indipendente dal linguaggio
Elaborazione dell'autenticazione di servizio App si verifica prima che le richieste raggiungano l'app per le API, il che significa che le funzionalità di autenticazione hello funzionano per App scritte in qualsiasi lingua o un framework per le API.  L'API può essere basata su ASP.NET, Java, Node.js o qualsiasi framework che supporta il servizio app.

Servizio App passa in hello token JSON web token (JWT) nell'intestazione di autorizzazione hello di una richiesta HTTP e il codice scritto in qualsiasi lingua o framework possa ottenere hello informazioni che necessarie da hello token. Inoltre, servizio App consente di accedere più facilmente toohello più diffuse attestazioni impostando alcune intestazioni speciali, come illustrato di seguito hello:

* X-MS-CLIENT-PRINCIPAL-NAME
* X-MS-CLIENT-PRINCIPAL-ID
* X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN
* X-MS-TOKEN-FACEBOOK-EXPIRES-ON

In un'API .NET, è possibile utilizzare hello `Authorize` attributo e per un'autorizzazione, è possibile scrivere facilmente codice in base alle attestazioni in quanto le informazioni sulle attestazioni vengono popolate automaticamente nelle classi di .NET.

## <a name="multiple-protection-options"></a>Opzioni di protezione multiple
Il servizio app può impedire alle richieste HTTP anonime di raggiungere l'app per le API, può passare tutte le richieste e convalidare i token per le richieste che li includono oppure può accettare tutte le richieste senza eseguire alcuna azione su di esse:

1. Consentire solo le richieste autenticate tooreach app per le API.
   
    Se una richiesta anonima viene ricevuta da un browser, il servizio App verrà reindirizzata automaticamente tooa pagina di accesso per il provider di autenticazione hello (Azure AD, Google, Twitter, e così via) che si sceglie. 
   
    Con questa opzione, non è necessario toowrite qualsiasi codice di autenticazione affatto nell'app, e codice di autorizzazione viene semplificato poiché attestazioni più importanti hello fornite nelle intestazioni HTTP hello.
2. Consenti tutte le richieste tooreach app per le API, ma convalidare le richieste autenticate e passare le informazioni di autenticazione nelle intestazioni HTTP hello.
   
    Questa opzione offre una maggiore flessibilità nella gestione delle richieste anonime, ma è necessario codice toowrite se si desidera che gli utenti anonimi tooprevent dall'utilizzo dell'API. Poiché le attestazioni più diffusi hello vengono passate nelle intestazioni hello di richieste HTTP, codice di autorizzazione è relativamente semplice.
3. Consenti tutte le richieste tooreach dell'API, eseguita alcuna operazione sulle informazioni di autenticazione nelle richieste hello.
   
    Questa opzione lascia le attività di autenticazione e autorizzazione completamente il codice di applicazione tooyour hello.

In hello [portale di Azure](https://portal.azure.com/), si seleziona l'opzione hello desiderato hello **autenticazione / autorizzazione** blade.

![](./media/app-service-api-authentication/authblade.png)

Per le opzioni 1 e 2, attivare **l'autenticazione del servizio App**e in hello **tootake azione quando la richiesta non è autenticata** elenco a discesa scegliere **Accedi** o **Consenti richiesta (alcuna azione)**.  Se si sceglie **Accedi**, si dispone di un provider di autenticazione toochoose e configurare tale provider.

![](./media/app-service-api-authentication/actiontotake.png)

Per informazioni dettagliate su come l'autenticazione tooconfigure, vedere [come tooconfigure l'accesso di Azure Active Directory di servizio App applicazione toouse](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). articolo Hello applica tooAPI App come App per dispositivi mobili e fornisca un collegamento articoli tooother per hello altri provider di autenticazione.

## <a id="internal"></a> Autenticazione dell'account del servizio
L'autenticazione del servizio App funziona per scenari interni, ad esempio per la chiamata da un'API app tooanother API app. In questo scenario si ottiene un token usando le credenziali per un account del servizio invece delle credenziali dell'utente finale. Un account del servizio è noto anche come *entità servizio* in Azure Active Directory e l'autenticazione che usa un account di questo tipo è nota anche come scenario da servizio a servizio. 

Per gli scenari servizio-a-service, proteggere hello chiamata API app con Azure Active Directory e fornire un token di autorizzazione dell'entità servizio AAD quando si chiama app hello API. Ottenere un token fornendo hello client ID e client secret da hello applicazione AAD. Nessun codice speciale solo Azure è richiesto, ad esempio true toobe utilizzato per la gestione dei token di hello Zumo di servizi mobili. Un esempio di questo scenario usando l'App per le API di ASP.NET è coperto da esercitazione hello [l'autenticazione dell'entità servizio per App per le API](app-service-api-dotnet-service-principal-auth.md).

Se si desidera toohandle uno scenario di servizio-servizio senza utilizzare l'autenticazione del servizio App, è possibile utilizzare l'autenticazione di base o i certificati client. Per informazioni sui certificati client in Azure, vedere [come l'autenticazione reciproca TLS per le app Web tooConfigure](../app-service-web/app-service-web-configure-tls-mutual-auth.md). Per informazioni sull'autenticazione di base in ASP.NET, vedere il blog sui [filtri di autenticazione nell'API Web 2 ASP.NET](http://www.asp.net/web-api/overview/security/authentication-filters).

L'autenticazione account di servizio da un'applicazione di servizio App logica app tooan API è un caso speciale e viene illustrato in [utilizzando l'API personalizzata ospitato nel servizio App con la logica app](../logic-apps/logic-apps-custom-hosted-api.md).

## <a name="mobile-client-authentication"></a>Autenticazione dei client per dispositivi mobili
Per informazioni sull'autenticazione toohandle da client mobili, vedere hello [documentazione sull'autenticazione dell'App per dispositivi mobili](../app-service-mobile/app-service-mobile-ios-get-started-users.md). L'autenticazione del servizio App funziona hello allo stesso modo per App per dispositivi mobili e App per le API.

## <a name="more-information"></a>Altre informazioni
Per ulteriori informazioni sull'autenticazione e autorizzazione in Azure App Service, vedere hello seguenti risorse:

* [Espansione dell'autenticazione/autorizzazione del servizio App](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)
* [Come tooconfigure l'accesso di Azure Active Directory di servizio App applicazione toouse](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md) (include i collegamenti per altri provider di autenticazione nella parte superiore di hello della pagina hello). 

Per ulteriori informazioni su OAuth 2.0, OpenID Connect e JSON Web token (JWT), vedere hello seguenti risorse.

* [Introduzione a OAuth 2.0](http://shop.oreilly.com/product/0636920021810.do "Getting Started with OAuth 2.0") 
* [Introduzione tooOAuth2, OpenID Connect e JSON Web token (JWT) - corsi Pluralsight](http://www.pluralsight.com/courses/oauth2-json-web-tokens-openid-connect-introduction) 
* [Creazione e protezione di un'API RESTful per più client in ASP.NET - corso PluralSight](http://www.pluralsight.com/courses/building-securing-restful-api-aspdotnet)

Per ulteriori informazioni su Azure Active Directory, vedere hello seguenti risorse.

* [Scenari per Azure AD](http://aka.ms/aadscenarios)
* [Guida per sviluppatori Azure AD](http://aka.ms/aaddev)
* [Esempi di Azure AD](http://aka.ms/aadsamples)

## <a name="next-steps"></a>Passaggi successivi
Questo articolo ha illustrato le funzionalità di autenticazione e autorizzazione del servizio app che è possibile usare per le app per le API. esercitazione successiva di Hello nel recupero hello avviato serie Mostra come tooimplement [autenticazione utente in App per le API del servizio App](app-service-api-dotnet-user-principal-auth.md).

