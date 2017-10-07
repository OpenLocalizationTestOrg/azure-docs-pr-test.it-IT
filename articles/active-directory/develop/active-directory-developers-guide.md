---
title: aaaAzure Active Directory per gli sviluppatori | Documenti Microsoft
description: Questo articolo offre una panoramica dell'accesso agli account Microsoft aziendali e dell'istituto di istruzione tramite Azure Active Directory.
services: active-directory
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5c872c89-ef04-4f4c-98de-bc0c7460c7c2
ms.service: active-directory
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4dbbea6c1e0b8a70c0c36ddd1caec5658130a003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-for-developers"></a>Azure Active Directory per sviluppatori
Azure Active Directory è un servizio di identità cloud che consente agli sviluppatori toosecurely Accedi qualsiasi utente con un account aziendale o dell'istituto di istruzione supportato da Microsoft.  documentazione Hello di seguito viene illustrato come tooadd Azure AD supporta l'applicazione tooyour utilizzando protocolli di autenticazione standard di settore, OAuth e OpenID Connect.

| | |
| --- | --- |
|[Nozioni di base sull'autenticazione](active-directory-authentication-scenarios.md) | Un tooauthentication introduzione con Azure AD |
|[Tipi di applicazioni](active-directory-authentication-scenarios.md#application-types-and-scenarios) | Una panoramica degli scenari di autenticazione hello è supportato da Azure AD |                                
                                                                              
## <a name="get-started"></a>Attività iniziali
Personalizzare la configurazione guidata illustrata utilizzando il nostro toosign di librerie di autenticazione degli utenti di Azure Active Directory.

|  |  |  |  |
| --- | --- | --- | --- |
| <center>![App per dispositivi mobili e desktop](./media/active-directory-developers-guide/NativeApp_Icon.png)<br />App per dispositivi mobili e desktop</center> | [Panoramica](active-directory-authentication-scenarios.md#native-application-to-web-api)<br /><br />[iOS](active-directory-devquickstarts-ios.md)<br /><br />[Android](active-directory-devquickstarts-android.md) | [.NET](active-directory-devquickstarts-dotnet.md)<br /><br />[Windows](active-directory-devquickstarts-windowsstore.md)<br /><br />[Xamarin](active-directory-devquickstarts-xamarin.md) | [Cordova](active-directory-devquickstarts-cordova.md)<br /><br />[OAuth 2.0](active-directory-protocols-oauth-code.md) |
| <center>![App Web](./media/active-directory-developers-guide/Web_app.png)<br />App Web</center> | [Panoramica](active-directory-authentication-scenarios.md#web-browser-to-web-application)<br /><br />[ASP.NET](active-directory-devquickstarts-webapp-dotnet.md)<br /><br />[Java](active-directory-devquickstarts-webapp-java.md) | [NodeJS](active-directory-devquickstarts-openidconnect-nodejs.md)<br /><br />[OpenID Connect 1.0](active-directory-protocols-openid-connect-code.md) |  |
| <center>![App a singola pagina](./media/active-directory-developers-guide/SPA.png)<br />App a singola pagina</center> | [Panoramica](active-directory-authentication-scenarios.md#single-page-application-spa)<br /><br />[AngularJS](active-directory-devquickstarts-angular.md)<br /><br />[JavaScript](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi) |  |  |
| <center>![API Web](./media/active-directory-developers-guide/Web_API.png)<br />API Web</center> | [Panoramica](active-directory-authentication-scenarios.md#web-application-to-web-api)<br /><br />[ASP.NET](active-directory-devquickstarts-webapi-dotnet.md)<br /><br />[NodeJS](active-directory-devquickstarts-webapi-nodejs.md) | &nbsp; |
| <center>![Da servizio a servizio](./media/active-directory-developers-guide/Service_App.png)<br />Da servizio a servizio</center> | [Panoramica](active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api)<br /><br />[.NET](active-directory-code-samples.md#server-or-daemon-application-to-web-api)<br /><br />[Credenziali client OAuth 2.0](active-directory-protocols-oauth-service-to-service.md) |  |

## <a name="guides"></a>Guide
Questi articoli che indicano la modalità di attività comuni di tooperform con Azure Active Directory.

|                                                                           |  |
|---------------------------------------------------------------------------| --- |
|[Registrazione delle app](active-directory-integrating-applications.md)           | Come tooregister un'app in Azure AD |
|[App multi-tenant](active-directory-devhowto-multi-tenant-overview.md)    | Funzionamento di account di Microsoft toosign |
|[OAuth e OpenID Connect](active-directory-protocols-openid-connect-code.md)| Come toosign-in utenti e chiamare le API web mediante i protocolli di autenticazione moderna |
|[Altre guide](active-directory-developers-guide-index.md#guides)        |     |

## <a name="reference"></a>Riferimento
Questi articoli offrono informazioni dettagliate su API, messaggi di protocollo e termini usati in Azure Active Directory.

|                                                                                   | |
| ----------------------------------------------------------------------------------| --- |
| [Librerie di autenticazione (ADAL)](active-directory-authentication-libraries.md)   | Una panoramica delle librerie di hello & SDK fornite da Azure AD |
| [Esempi di codice](active-directory-code-samples.md)                                  | Elenco di tutti gli esempi di codice di Azure AD |
| [Glossario](active-directory-dev-glossary.md)                                      | Terminologia e definizioni dei termini usati nella documentazione |
| [Altro materiale di riferimento](active-directory-developers-guide-index.md#reference)|     |

## <a name="help--support"></a>Guida e supporto
Si tratta di hello migliore posizioni tooget assistenza per lo sviluppo di Azure Active Directory.

|  |  
|---|
|[Tag `azure-active-directory` e `adal` di Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)      |
|[Commenti e suggerimenti su Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)|
| [Provare Microsoft Dev Chat (gratuito per un periodo di tempo limitato)](http://aka.ms/devchat) |

<br />

> [!NOTE]
> Se è necessario toosign aggiuntivo account personale di Microsoft, è opportuno tooconsider utilizzando hello [endpoint v 2.0 di Azure AD](active-directory-appmodel-v2-overview.md).  endpoint di Azure AD Hello v 2.0 è unificazione hello di account personale di Microsoft & account di lavoro di Microsoft (da Azure AD) in un sistema di autenticazione single.
