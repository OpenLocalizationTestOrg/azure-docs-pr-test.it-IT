---
title: 'Panoramica: Azure AD B2C | Microsoft Docs'
description: Sviluppo di applicazioni di utenti con Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: c465dbde-f800-4f2e-8814-0ff5f5dae610
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/06/2016
ms.author: saeedakhter-msft
ms.openlocfilehash: abfd742e710458de3193dc5051de7818a112376c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-focus-on-your-app-let-us-worry-about-sign-up-and-sign-in"></a>Azure Active Directory B2C permette di concentrarsi sull'app, lasciando ad Azure la gestione di iscrizioni e accessi

Azure Active Directory B2C è una soluzione di gestione delle identità cloud per applicazioni Web e per dispositivi mobili. È un servizio globale a disponibilità elevata che viene ridimensionata toohundreds di milioni di valori Identity. Basato su una piattaforma sicura di livello aziendale, Azure Active Directory B2C contribuisce alla protezione di applicazioni, azienda e clienti.

Con la configurazione minima, Azure AD B2C consente tooauthenticate l'applicazione:

* **Account social**, come Facebook, Google, LinkedIn e altri
* **Account aziendali** tramite protocolli standard aperti, OpenID Connect o SAML
* **Account locali**, con indirizzo e-mail e password o nome utente e password

## <a name="get-started"></a>Attività iniziali

Innanzitutto, ottenere il proprio tenant utilizzando i passaggi descritti nella procedura hello [creare un tenant di Azure Active Directory B2C](active-directory-b2c-get-started.md).

Scegliere quindi lo scenario di sviluppo dell'applicazione:

|  |  |  |  |
| --- | --- | --- | --- |
| <center>![App per dispositivi mobili e desktop](../active-directory/develop/media/active-directory-developers-guide/NativeApp_Icon.png)<br />App per dispositivi mobili e desktop</center> | [Panoramica](active-directory-b2c-reference-oauth-code.md)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br /><br />[iOS](https://github.com/Azure-Samples/active-directory-b2c-ios-swift-native-msal)<br /><br />[Android](https://github.com/Azure-Samples/active-directory-b2c-android-native-msal) | [.NET](https://github.com/Azure-Samples/active-directory-b2c-dotnet-desktop)<br /><br />[Xamarin](https://github.com/Azure-Samples/active-directory-b2c-xamarin-native) |  |
| <center>![App Web](../active-directory/develop/media/active-directory-developers-guide/Web_app.png)<br />App Web</center> | [Panoramica](active-directory-b2c-reference-oidc.md)<br /><br />[ASP.NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)<br /><br />[ASP.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapp) | [Node.JS](active-directory-b2c-devquickstarts-web-node.md) |  |
| <center>![App a singola pagina](../active-directory/develop/media/active-directory-developers-guide/SPA.png)<br />App a singola pagina</center> | [Panoramica](active-directory-b2c-reference-spa.md)<br /><br />[JavaScript](https://github.com/Azure-Samples/active-directory-b2c-javascript-msal-singlepageapp)<br /><br /> |  |  |
| <center>![API Web](../active-directory/develop/media/active-directory-developers-guide/Web_API.png)<br />API Web</center> | [ASP.NET](active-directory-b2c-devquickstarts-api-dotnet.md)<br /><br /> [ASP.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi)<br /><br /> [Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi) | [Chiamare un'API Web .NET](active-directory-b2c-devquickstarts-web-api-dotnet.md) |

## <a name="whats-new"></a>Novità

Controllare di nuovo questa pagina spesso toolearn sulle modifiche future toohello Azure Active Directory B2C. Gli aggiornamenti vengono anche resi disponibili su Twitter con @AzureAD.

* Inoltre troppo "Criteri predefiniti" disponibilità generale (), hello ["Criteri personalizzati"](active-directory-b2c-overview-custom.md) funzionalità è ora disponibile in anteprima pubblica.  Criteri personalizzati sono destinate ai professionisti di identità che è necessario controllare la composizione hello dell'esperienza di identità.
* Hello [Token di accesso](https://azure.microsoft.com/en-us/blog/azure-ad-b2c-access-tokens-now-in-public-preview) funzionalità è ora disponibile in anteprima pubblica.
* È stata annunciata la [disponibilità generale delle directory Azure Active Directory B2C in Europa](https://azure.microsoft.com/en-us/blog/azuread-b2c-ga-eu/).
* Vedere la libreria degli [esempi di codice su GitHub](https://github.com/Azure-Samples?q=b2c), in continuo aumento.

## <a name="how-tooarticles"></a>Come tooarticles

Informazioni su come toouse funzionalità specifiche di Azure Active Directory B2C:

* Configurare gli account [Facebook](active-directory-b2c-setup-fb-app.md), [Google+](active-directory-b2c-setup-goog-app.md), [Microsoft](active-directory-b2c-setup-msa-app.md), [Amazon](active-directory-b2c-setup-amzn-app.md) e [LinkedIn](active-directory-b2c-setup-li-app.md) per l'uso nelle applicazioni destinate agli utenti.
* [Utilizzare gli attributi personalizzati toocollect informazioni su utenti](active-directory-b2c-reference-custom-attr.md).
* [Abilitare Azure Multi-Factor Authentication nelle applicazioni destinate agli utenti](active-directory-b2c-reference-mfa.md).
* [Configurare la reimpostazione password self-service per gli utenti](active-directory-b2c-reference-sspr.md).
* [Personalizzare hello aspetto dell'iscrizione, eseguire l'accesso in e altre pagine per consumatori](active-directory-b2c-reference-ui-customization.md) che vengono gestite da Azure Active Directory B2C.
* [Utilizzare hello API di Graph di Azure Active Directory tooprogrammatically creare, leggere, aggiornare ed eliminare i consumer](active-directory-b2c-devquickstarts-graph-dotnet.md) nel tenant di Azure Active Directory B2C.

## <a name="next-steps"></a>Passaggi successivi

Questi collegamenti sono utili per l'esplorazione servizio hello in modo approfondito:

* Vedere hello [informazioni sui prezzi di Azure Active Directory B2C](https://azure.microsoft.com/pricing/details/active-directory-b2c/).
* Vedere i [codici di esempio](https://azure.microsoft.com/en-us/resources/samples/?service=active-directory&term=b2c) per Azure Active Directory B2C. 
* Ottenere informazioni su Stack Overflow utilizzando hello [azure-ad-b2c](http://stackoverflow.com/questions/tagged/azure-ad-b2c) tag.
* Fornire le proprie opinioni utilizzando [Uservoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c), desideriamo toohear li!
* Hello revisione [Azure Active Directory B2C Protocol Reference](active-directory-b2c-reference-protocols.md).
* Hello revisione [riferimento del Token di Azure Active Directory B2C](active-directory-b2c-reference-tokens.md).
* Hello lettura [domande frequenti di Azure Active Directory B2C](active-directory-b2c-faqs.md).
* [Inviare richieste di supporto per Azure Active Directory B2C](active-directory-b2c-support.md).

## <a name="get-security-updates-for-our-products"></a>Ottenere aggiornamenti della sicurezza per i prodotti

Si consiglia di generazione di eventi di sicurezza, visitare il sito di notifica tooget [questa pagina](https://technet.microsoft.com/security/dd252948) e la sottoscrizione di avvisi consultivo tooSecurity.

