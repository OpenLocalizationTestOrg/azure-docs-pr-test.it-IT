---
title: Active Directory Authentication Library aaaAzure | Documenti Microsoft
description: Hello Azure AD Authentication Library (ADAL) consente a sviluppatori di applicazioni client tooeasily autenticare gli utenti toocloud o Active Directory (AD) locale e ottenere quindi i token di accesso per proteggere le chiamate API.
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: mbaldwin
ms.assetid: 2e4fc79a-0285-40be-8c77-65edee408a22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 20fae18807ef03463ab1bc218e5f3548b5bd5717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-authentication-libraries"></a>Azure Active Directory Authentication Library
Hello Azure Active Directory Authentication Library (ADAL) Abilita client applicazione sviluppatori tooeasily autenticare gli utenti toocloud o Active Directory (AD) locale e ottenere i token di accesso per proteggere le chiamate API. ADAL semplifica l'autenticazione per gli sviluppatori grazie a funzionalità come:
 - Supporto per le chiamate asincrone
 - Cache dei token configurabili in cui archiviare i token di accesso e i token di aggiornamento
 - Aggiornamento del token automatico quando un token di accesso scade ed è disponibile un token di aggiornamento
 - Altro
 
Se si gestisce la maggior parte delle complessità hello, ADAL consente agli sviluppatori di concentrarsi sulla logica di business e proteggere facilmente le risorse, senza essere esperti di sicurezza.

Azure AD Authentication Library è disponibile per una vasta gamma di piattaforme.

### <a name="client-libraries"></a>Librerie client

| Piattaforma | Libreria | Download | Codice sorgente | Esempio | Riferimento
| --- | --- | --- | --- | --- | --- |
| .NET Client, Windows Store, UWP, Xamarin iOS e Android |MSAL per .NET (anteprima) |[NuGet](https://www.nuget.org/packages/Microsoft.Identity.Client/1.1.0-preview) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [App desktop](~/articles/active-directory/develop/guidedsetups/active-directory-windesktop.md) |[Riferimento](https://docs.microsoft.com/dotnet/api/?view=identityclient-1.1.0-preview) | 
| JavaScript |MSAL per JavaScript (anteprima) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [App a pagina singola](~/articles/active-directory/develop/GuidedSetups/active-directory-javascriptspa.md) | [Riferimento](https://htmlpreview.github.io/?https://raw.githubusercontent.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/docs/classes/_useragentapplication_.msal.useragentapplication.html) | 
| iOS |MSAL per iOS (anteprima) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | [App iOS](~/articles/active-directory/develop/GuidedSetups/active-directory-ios.md) | [Riferimento](https://azuread.github.io/docs/objc/) |
| Android |MSAL per Android (anteprima) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) | [App Android](~/articles/active-directory/develop/GuidedSetups/active-directory-android.md) | [Riferimento](http://javadoc.io/doc/com.microsoft.identity.client/msal/0.1.1) |
| .NET Client, Windows Store, UWP, Xamarin iOS e Android |ADAL .NET v3 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet) | [App desktop](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-dotnet) |[Riferimento](https://docs.microsoft.com/dotnet/api/?view=identitymodelclientsad-3.13.9) | 
| .NET Client, Windows Store, Windows Phone 8.1 |ADAL .NET v2 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/2.28.4) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/releases/tag/v2.28.4) | [App desktop](https://github.com/AzureADQuickStarts/NativeClient-DotNet/releases/tag/v2.X) | | 
| JavaScript |ADAL.js |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-js) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-js) |[App a pagina singola](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi) | |
| iOS, macOS |ADAL |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-objc/releases) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-objc) |[App iOS](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-ios) | [Riferimento](https://cocoapods.org/pods/ADAL)|
| Android |ADAL |[Hello Repository centrale](http://search.maven.org/remotecontent?filepath=com/microsoft/aad/adal/) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android) |[App Android](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-android) | [JavaDocs](http://javadoc.io/doc/com.microsoft.aad/adal/)|
| Node.js |ADAL |[npm](https://www.npmjs.com/package/adal-node) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs) | | |
| Java |ADAL4J |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) |[App Web Java](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapp-java) | |
| Python |ADAL |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-python) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-python) | | |
### <a name="server-libraries"></a>Librerie server 

| Piattaforma | Libreria | Download | Codice sorgente | Esempio | Riferimenti
| --- | --- | --- | --- | --- | --- |
| .NET |OWIN per AzureAD|[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.ActiveDirectory/) |[CodePlex](http://katanaproject.codeplex.com) |[Applicazione MVC](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapp-dotnet) | |
| .NET |OWIN per OpenIDConnect |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect) |[CodePlex](http://katanaproject.codeplex.com) |[App Web](https://github.com/AzureADSamples/WebApp-OpenIDConnect-DotNet) | |
| Node.js |Passport Azure AD |[npm](https://www.npmjs.com/package/passport-azure-ad) |[GitHub](https://github.com/AzureAD/passport-azure-ad) | [API Web](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapi-nodejs)| |
| .NET |OWIN per WS-Federation |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.WsFederation) |[CodePlex](http://katanaproject.codeplex.com) |[App Web MVC](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) | |
| .NET |Estensioni del protocollo di identità per .NET 4.5 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Protocol.Extensions) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| .NET |Gestore token JWT per .NET 4.5 |[NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |



## <a name="scenarios"></a>Scenari

Di seguito sono illustrati i tre scenari comuni in cui è possibile usare Azure AD Authentication Library per l'autenticazione di un client che accede a una risorsa remota:  

### <a name="authenticating-users-of-a-native-client-application-running-on-a-device"></a>Autenticazione di utenti di un'applicazione client nativa in esecuzione su un dispositivo 

In questo scenario, uno sviluppatore ha un'applicazione client WPF, che deve tooaccess una risorsa remota protetta da Azure AD, ad esempio un'API web. Egli ha una sottoscrizione Azure, sa come tooinvoke hello API web downstream e conosce hello Azure tenant AD hello Usa API web. Di conseguenza, è possibile utilizzare autenticazione ADAL toofacilitate con Azure AD, delegando completamente tooADAL esperienza di autenticazione hello o gestendo esplicitamente le credenziali dell'utente. ADAL rende utente hello tooauthenticate semplice, ottenere un token di accesso e un token di aggiornamento da Azure AD e quindi utilizzare hello accesso token toomake richieste toohello web API.

Per un esempio di codice che illustra questo scenario utilizzando l'autenticazione tooAzure Active Directory, vedere [tooWeb applicazione WPF Client nativa API](https://github.com/azureadsamples/nativeclient-dotnet).

### <a name="authenticating-a-confidential-client-application-running-on-a-web-server"></a>Autenticazione di un'applicazione client riservata in esecuzione in un server Web

In questo scenario, uno sviluppatore ha un'applicazione in esecuzione su un server che deve tooaccess una risorsa remota protetta da Azure AD, ad esempio un'API web. Egli ha una sottoscrizione Azure, sa come tooinvoke hello servizio downstream e conosce Usa API web hello tenant di Azure AD hello. Di conseguenza, è possibile utilizzare l'autenticazione di toofacilitate ADAL con Azure AD gestendo esplicitamente le credenziali dell'applicazione hello. ADAL rende facile tooretrieve un token da Azure AD utilizzando credenziali client dell'applicazione hello e quindi utilizzare tale web toohello le richieste di token toomake API. ADAL anche gli handle di gestire la durata hello di hello token di accesso memorizzandolo nella cache e rinnovandolo, quando necessario. Per un esempio di codice che illustra questo scenario, vedere [tooWeb di applicazione console Daemon API](https://github.com/AzureADSamples/Daemon-DotNet).

### <a name="authenticating-a-confidential-client-application-running-on-a-server-on-behalf-of-a-user"></a>Autenticazione di un'applicazione client riservata in esecuzione in un server, per conto di un utente 

In questo scenario, uno sviluppatore ha un'applicazione in esecuzione su un server che deve tooaccess una risorsa remota protetta da Azure AD, ad esempio un'API web. richiesta di Hello deve inoltre toobe effettuate per conto di un utente AD Azure. Egli ha una sottoscrizione Azure, sa come tooinvoke hello API web downstream e conosce hello servizio hello tenant di Azure AD Usa. Una volta utente hello applicazione web toohello autenticato, un'applicazione hello può ottenere un codice di autorizzazione per l'utente hello da Azure AD. un'applicazione web Hello utilizzabile poi tooobtain ADAL un token di accesso e un token di aggiornamento per conto dell'utente utilizzando hello del client e del codice delle credenziali di autorizzazione associate a un'applicazione hello da Azure AD. Al termine dell'applicazione web hello in possesso del token di accesso hello, può chiamare API web hello fino alla scadenza del token hello. Quando hello token scade, un'applicazione web hello è possibile utilizzare tooget ADAL un nuovo token di accesso tramite i token di aggiornamento hello ricevuto in precedenza. Per un esempio di codice che illustra questo scenario, vedere [tooWeb tooWeb API Native client API](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof).

## <a name="see-also"></a>Vedere anche

- [Hello Guida per gli sviluppatori di Azure Active Directory](active-directory-developers-guide.md)
- [Scenari di autenticazione per Azure Active Directory](active-directory-authentication-scenarios.md)
- [Esempi di codice per Azure Active Directory](active-directory-code-samples.md)
