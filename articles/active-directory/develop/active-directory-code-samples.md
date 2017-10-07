---
title: Esempi di codice di Active Directory aaaAzure | Documenti Microsoft
description: Indice di esempi di codice di Azure Active Directory, organizzati in base allo scenario.
services: active-directory
documentationcenter: dev-center-name
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: a242a5ff-7300-40c2-ba83-fb6035707433
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: mbaldwin
ms.custom: aaddev
ms.openlocfilehash: 921ce08766cc6e29a6db2c4f38d216e6de11730f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-code-samples"></a>Esempi di codice di Azure Active Directory
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

È possibile utilizzare Microsoft Azure Active Directory (Azure AD) tooadd autenticazione e autorizzazione tooyour applicazioni web e le API web. Questa sezione contiene collegamenti si toosamples che illustrano le modalità e i frammenti di codice che è possibile utilizzare nelle applicazioni. Nella pagina di esempio di codice hello, sono disponibili modalità lettura-me gli argomenti della Guida con i requisiti, installazione e configurazione. E codice hello è commentato toohelp è comprendere le sezioni critiche di hello.

scenario di base hello toounderstand per ogni tipo di campionamento, vedere scenari di autenticazione per Azure AD.

Contribuiscono esempi tooour su GitHub: [esempi di Microsoft Azure Active Directory e la documentazione](https://github.com/Azure-Samples?page=3&query=active-directory).

## <a name="web-browser-tooweb-application"></a>Web Browser tooWeb applicazione
Questi esempi viene illustrato come un'applicazione web che indirizza toowrite hello toosign browser dell'utente tooAzure AD esse.

| Linguaggio/Piattaforma | Esempio | Descrizione |
| --- | --- | --- |
| C#/.NET |[WebApp-OpenIDConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) |Utilizzare gli utenti di tooauthenticate OpenID Connect (middleware OpenID Connect OWIN ASP.Net) da un tenant di Azure AD. |
| C#/.NET |[WebApp-MultiTenant-OpenIdConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-multitenant-openidconnect) |Applicazione web MVC .NET multi-tenant che usa OpenID Connect (middleware OpenID Connect OWIN ASP.Net) tooauthenticate utenti da più tenant di Azure AD. |
| C#/.NET |[WebApp-WSFederation-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-wsfederation) |Utilizzare gli utenti tooauthenticate WS-Federation (middleware OWIN WS-Federation ASP.Net) da un tenant di Azure AD. |

## <a name="single-page-application-spa"></a>Applicazione a singola pagina (SPA)
Questo esempio viene illustrato come toowrite un'applicazione a singola pagina protetta con Azure AD.  

| Linguaggio/Piattaforma | Esempio | Descrizione |
| --- | --- | --- |
| JavaScript, C#/.NET |[SinglePageApp-DotNet](https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp) |Usare ADAL per JavaScript e Azure AD app a singola pagina toosecure un basata su AngularJS implementata con un back-end di API web ASP.NET. |

## <a name="native-application-tooweb-api"></a>TooWeb applicazione nativa API
Questi esempi di codice viene illustrato come toobuild le applicazioni client native che chiamano API web che sono protetti da Azure AD. Vengono usati [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) e [OAuth 2.0 in Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx).

| Linguaggio/Piattaforma | Esempio | Descrizione |
| --- | --- | --- |
| JavaScript |[NativeClient-MultiTarget-Cordova](https://github.com/Azure-Samples/active-directory-cordova-multitarget) |Utilizzare i plug-in ADAL hello per Apache Cordova toobuild un'app di Apache Cordova che chiama un'API web e Usa Azure AD per l'autenticazione. |
| C#/.NET |[NativeClient-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop) |Applicazione WPF .NET che chiama un'API Web protetta mediante Azure AD. |
| C#/.NET |[NativeClient-WindowsStore](https://github.com/Azure-Samples/active-directory-dotnet-windows-store) |Applicazione di Windows Store che chiama un'API Web protetta mediante Azure AD. |
| C#/.NET |[NativeClient-WebAPI-MultiTenant-WindowsStore](https://github.com/Azure-Samples/active-directory-dotnet-webapi-multitenant-windows-store) |Applicazione di Windows Store che chiama un'API Web multi-tenant protetta mediante Azure AD. |
| C#/.NET |[WebAPI-OnBehalfOf-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof) |Un'applicazione client nativa che chiama un'API web, che ottiene un token tooact per conto di utente originale hello e quindi utilizza hello token toocall un'altra API web. |
| C#/.NET |[NativeClient-WindowsPhone8.1](https://github.com/Azure-Samples/active-directory-dotnet-windowsphone-8.1) |Applicazione di Windows Store per Windows Phone 8.1 che chiama un'API Web protetta mediante Azure AD. |
| ObjC |[NativeClient-iOS](https://github.com/Azure-Samples/active-directory-ios) |Applicazione iOS che chiama un'API Web che richiede Azure AD per l'autenticazione. |
| C#/.NET |[WebAPI-ManuallyValidateJwt-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapi-manual-jwt-validation) |Un'applicazione client nativa che include la logica tooprocess un token JWT in un'API web, anziché utilizzare il middleware OWIN. |
| C#/Xamarin |[NativeClient-Xamarin-Android](https://github.com/Azure-Samples/active-directory-xamarin-android) |Un Xamarin associazione toohello native Azure AD Authentication Library (ADAL) per hello libreria Android. |
| C#/Xamarin |[NativeClient-Xamarin-iOS](https://github.com/Azure-Samples/active-directory-xamarin-ios) |Un toohello associazione Xamarin native Azure AD Authentication Library (ADAL) per iOS. |
| C#/Xamarin |[NativeClient-MultiTarget-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-multitarget) |Progetto Xamarin destinato a cinque piattaforme che chiama un'API Web protetta mediante Azure AD. |
| C#/.NET |[NativeClient-Headless-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-headless) |Applicazione nativa che esegue l'autenticazione non interattiva e chiama un'API Web protetta mediante Azure AD. |

## <a name="web-application-tooweb-api"></a>TooWeb di applicazione Web API
Questi esempi di codice mostra come usare [OAuth 2.0 in Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx) toobuild le applicazioni web che chiamano API web che sono protetti da Azure AD.

| Linguaggio/Piattaforma | Esempio | Descrizione |
| --- | --- | --- |
| C#/.NET |[WebApp-WebAPI-OpenIDConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-openidconnect) |Chiamare un'API web con hello connesso autorizzazioni dell'utente. |
| C#/.NET |[WebApp-WebAPI-OAuth2-AppIdentity-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-appidentity) |Chiamare un'API web con le autorizzazioni dell'applicazione hello. |
| C#/.NET |[WebApp-WebAPI-OAuth2-UserIdentity-Dotnet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity) |Aggiungere l'autorizzazione con [OAuth 2.0 in Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooan un'applicazione web esistente in modo può chiamare un'API web. |
| JavaScript |[WebAPI-Nodejs](https://github.com/Azure-Samples/active-directory-node-webapi) |Viene configurato un servizio API REST integrato con Azure AD per la protezione delle API. Viene incluso un server Node.js con un'API Web. |
| C#/.NET |[WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-multitenant-openidconnect) |Applicazione che usa OpenID Connect (middleware OpenID Connect OWIN ASP.Net) tooauthenticate agli utenti di un tenant di Azure AD di web MVC multi-tenant. Usa un hello tooinvoke codice di autorizzazione API Graph. |

## <a name="server-or-daemon-application-tooweb-api"></a>Applicazione server o Daemon tooWeb API
Questi esempi di codice viene illustrato come toobuild daemon o un'applicazione server che ottiene risorse da un'API web utilizzando [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) e [OAuth 2.0 in Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx).

| Linguaggio/Piattaforma | Esempio | Descrizione |
| --- | --- | --- |
| C#/.NET |[Daemon-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-daemon) |Applicazione console che chiama un'API Web. credenziale client hello è una password. |
| C#/.NET |[Daemon-CertificateCredential-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential) |Applicazione console che chiama un'API Web. credenziale client hello è un certificato. |

## <a name="calling-azure-ad-graph-api"></a>Chiamata dell'API Graph di Azure AD
In questi esempi di codice mostra come toobuild applicazioni che chiamano hello API Azure AD Graph tooread e scrittura dati directory.

| Linguaggio/Piattaforma | Esempio | Descrizione |
| --- | --- | --- |
| Java |[WebApp-GraphAPI-Java](https://github.com/Azure-Samples/active-directory-java-graphapi-web) |Un'applicazione web che utilizza l'API Graph di hello tooaccess dati della directory Azure AD. |
| PHP |[WebApp-GraphAPI-PHP](https://github.com/Azure-Samples/active-directory-php-graphapi-web) |Un'applicazione web che utilizza l'API Graph di hello tooaccess dati della directory Azure AD. |
| C#/.NET |[WebApp-GraphAPI-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-web) |Un'applicazione web che utilizza l'API Graph di hello tooaccess dati della directory Azure AD. |
| C#/.NET |[ConsoleApp-GraphAPI-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-console) |Questa applicazione console viene comuni in lettura e scrittura chiamate toohello API Graph e illustra come utente tooexecute assegnazione delle licenze e aggiornare i collegamenti e foto di anteprima di un utente. |
| C#/.NET |[ConsoleApp-GraphAPI-DiffQuery-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-diffquery) |Un'applicazione console che utilizza query differenziale hello in hello API Graph tooget periodica modifica toouser oggetti in un tenant di Azure AD. |
| C#/.NET |[WebApp-GraphAPI-DirectoryExtensions-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-directoryextensions-web) |Un'applicazione MVC utilizza l'API Graph query toogenerate un organigramma della società semplice. |
| PHP |[WebApp-GraphAPI-DirectoryExtensions-PHP](https://github.com/Azure-Samples/active-directory-php-graphapi-directoryextensions-web) |Un'applicazione PHP che chiama hello API Graph tooregister un'estensione e quindi leggerne, aggiornarla ed Elimina valori nell'attributo estensione hello. |

## <a name="authorization"></a>Authorization
Questi mostra esempi di codice come toouse Azure AD per l'autorizzazione.

| Linguaggio/Piattaforma | Esempio | Descrizione |
| --- | --- | --- |
| C#/.NET |[WebApp-GroupClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-groupclaims) |Viene eseguito il controllo degli accessi in base al ruolo usando le attestazioni basate su gruppo di Azure Active Directory in un'applicazione integrata con Azure AD. |
| C#/.NET |[WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) |Viene eseguito il controllo degli accessi in base al ruolo usando i ruoli applicazione di Azure Active Directory in un'applicazione integrata con Azure AD. |

## <a name="legacy-walkthroughs"></a>Procedure dettagliate legacy
Queste procedure possono risultare interessanti per l'utente pur essendo basate su tecnologie meno recenti.

| Linguaggio/Piattaforma | Esempio | Descrizione |
| --- | --- | --- |
| C#/.NET |[Autorizzazione basata sui ruoli e basata su ACL in un'applicazione di Microsoft Azure AD](http://go.microsoft.com/fwlink/?LinkId=331694) |Viene eseguita l'autorizzazione basata sui ruoli (Controllo degli accessi in base al ruolo) e sull'elenco di controllo di accesso (ACL) in un'applicazione integrata con Azure AD. |
| C#/.NET |[AAL - servizio di Windows Store app tooREST - autenticazione](http://go.microsoft.com/fwlink/?LinkId=330605) |Utilizzare [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) (in precedenza AAL) per app di Windows Store di Windows Store Beta tooadd utente authentication funzionalità tooa. |
| C#/.NET |[ADAL - service di App Native tooREST - autenticazione con AAD mediante finestra di dialogo del Browser](http://go.microsoft.com/fwlink/?LinkId=259814) |Utilizzare [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) del client di WPF tooa tooadd utente autenticazione funzionalità. |
| C#/.NET |[ADAL - service di App Native tooREST - autenticazione con ACS mediante finestra di dialogo del Browser](http://code.msdn.microsoft.com/AAL-Native-App-to-REST-de57f2cc) |Utilizzare [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) e [Access Control Service 2.0 (ACS)](http://msdn.microsoft.com/library/azure/hh147631.aspx) del client di WPF tooa tooadd utente autenticazione funzionalità. |
| C#/.NET |[ADAL - Server tooServer autenticazione](http://go.microsoft.com/fwlink/?LinkId=259816) |Utilizzare [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) toosecure chiamate al servizio da un tooan di processo sul lato server servizio REST dell'API Web MVC4. |
| C#/.NET |[Aggiunta di tooYour Sign-On Web dell'applicazione tramite Azure Active Directory](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) |Configurare .NET application tooperform web single sign-on con la directory aziendale di Azure AD. |
| C#/.NET |[Sviluppo di applicazioni Web multi-tenant con Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-multitenant-openidconnect) |Usare Azure AD tooadd toohello single sign-on e la funzionalità di accesso directory di un toowork di applicazioni .NET in più organizzazioni. |
| Java |[App di esempio Java per l'API Graph di Azure AD](http://go.microsoft.com/fwlink/?LinkId=263969) |Utilizzare i dati di directory hello API Graph tooaccess da Azure AD. |
| PHP |[App di esempio PHP per l'API Graph di Azure AD](http://code.msdn.microsoft.com/PHP-Sample-App-For-Windows-228c6ddb) |Utilizzare i dati di directory hello API Graph tooaccess da Azure AD. |
| C#/.NET |[App di esempio per l'API Graph di Azure AD](http://go.microsoft.com/fwlink/?LinkID=262648) |Utilizzare i dati di directory hello API Graph tooaccess da Azure AD. |
| C#/.NET |[App di esempio per la query differenziale di Azure AD Graph](http://go.microsoft.com/fwlink/?LinkId=275398) |Utilizzare la query differenziale hello negli oggetti hello API Graph tooget modifiche periodiche toouser in un tenant di Azure AD. |
| C#/.NET |[App di esempio per integrare un'applicazione cloud multi-tenant per Azure AD](http://go.microsoft.com/fwlink/?LinkId=275397) |Viene integrata un'applicazione multi-tenant in Azure AD. |
| C#/.NET |[Protezione di un'applicazione di Windows Store e di un servizio Web REST mediante Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-windows-store) |Creare una risorsa API web semplice e un'applicazione client di Windows Store mediante Azure AD e hello [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md). |
| C#/.NET |[Utilizzando tooQuery API Graph hello Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-web) |Configurare un hello toouse applicazione di Microsoft .NET dati tooaccess API Graph di Azure AD da una directory tenant di Azure AD. |

## <a name="see-also"></a>Vedere anche
##### <a name="other-resources"></a>Altre risorse
[Guida per gli sviluppatori di Azure Active Directory](active-directory-developers-guide.md)

[Concetti e riferimenti relativi all'API Graph di Azure AD](https://msdn.microsoft.com/library/azure/hh974476.aspx)

[Libreria helper dell'API Graph di Azure AD](https://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient)
