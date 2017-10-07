---
title: aaaAzure AD v2 ASP.NET Web Server Getting Started - Test | Documenti Microsoft
description: Implementazione di accessi Microsoft in una soluzione ASP.NET con un'applicazione tradizionale basata su Web browser tramite lo standard OpenID Connect
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 99c7525b9146605142180962fc2a61b3c953c064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Testare il codice

Premere `F5` toorun il progetto in Visual Studio. Hello browser verrà aperto e indirizzare è troppo*http://localhost: {porta}* dove verrà visualizzato hello *accedere con Microsoft* pulsante. Fare clic, toosign in.

Quando si è pronti tootest, utilizzare una o dell'istituto di istruzione (Azure Active Directory), account aziendale o personale (live.com, outlook.com) toosign in. 

![Finestra del browser con accesso con Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Finestra del browser con accesso con Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a>Risultati previsti
Dopo l'accesso, utente hello è reindirizzato toohello home page del sito web che è l'URL HTTPS specificato nelle informazioni di registrazione dell'applicazione nel portale di registrazione dell'applicazione Microsoft hello hello. In questa pagina vengono ora *Hello {User}* e un collegamento toosign-out e le attestazioni dell'utente di hello toosee collegamento – che è un controller di Authorize toohello collegamento creato in precedenza.

### <a name="see-users-claims"></a>Visualizzare le attestazioni dell'utente
Selezionare le attestazioni dell'utente di hello collegamento ipertestuale toosee hello. Ciò porta controller toohello e visualizzazione solo toousers disponibili che vengono autenticate.

#### <a name="expected-results"></a>Risultati previsti
 Verrà visualizzata una tabella contenente le proprietà di base hello dell'utente connesso hello:

| Proprietà | Valore | Descrizione|
|---|---|---|
| Nome | {Nome e cognome utente} | utente Hello e del cognome
|Username | <span>user@domain.com</span>| nome utente Hello utilizzato tooidentify hello registrato
| Oggetto| {Soggetto}|Una stringa di toouniquely identificare accesso utente hello Web hello|
| ID tenant| {GUID}| Oggetto *guid* toouniquely rappresentano l'organizzazione di Azure Active Directory dell'utente di hello.|

Verrà visualizzata anche una tabella contenente tutte le attestazioni utente incluse nella richiesta di autenticazione. Per un elenco e una spiegazione di tutte le attestazioni in un token ID, vedere questo [articolo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "Elenco delle attestazioni nei token ID").


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a>Testare l'accesso a un metodo con attributo *[Authorize]* (facoltativo)
In questo passaggio, si verrà controller di test durante l'accesso ai hello autenticato come utente anonimo:<br/>
Selezionare utente hello toosign-out di collegamento hello e processo di disconnessione hello completo.<br/>
A questo punto, nel browser, digitare http://localhost: {porta} / autenticato tooaccess il controller che è protetta con hello `[Authorize]` attributo

#### <a name="expected-results"></a>Risultati previsti
Si dovrebbe ricevere la visualizzazione di hello toosee tooauthenticate di richiesta di hello.

## <a name="additional-information"></a>Informazioni aggiuntive

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a>Proteggere l'intero sito Web
tooprotect l'intero sito web, aggiungere hello `AuthorizeAttribute` troppo`GlobalFilters` in `Global.asax` `Application_Start` metodo:

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> **Come gli utenti toorestrict da sola organizzazione toosign nell'applicazione tooyour**

> Per impostazione predefinita, gli account personali (tra cui outlook.com, live.com e altri), nonché account aziendale e dell'istituto di istruzione da qualsiasi società o organizzazione che è integrato con Azure Active Directory può Accedi tooyour applicazione. 

> Se si desidera che l'applicazione tooaccept accessi da sola organizzazione di Azure Active Directory, sostituire hello `Tenant` parametro *Web. config* da `Common` toohello nome del tenant dell'organizzazione hello-esempio *contoso.onmicrosoft.com*. Successivamente, modificare hello `ValidateIssuer` argomento in del *classe di avvio di OWIN* troppo`true`.

> gli utenti tooallow da solo un elenco di aziende specifiche, impostare `ValidateIssuer` tootrue e utilizzare hello `ValidIssuers` toospecify parametro un elenco delle organizzazioni.

> Un'altra opzione è un metodo personalizzato tooimplement autorità emittenti di hello toovalidate utilizzando il parametro IssuerValidator. Per altre informazioni su `TokenValidationParameters`, vedere [questo](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "Articolo di MSDN su TokenValidationParameters") articolo di MSDN.

