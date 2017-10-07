---
title: gli account sviluppatore aaaAuthorize mediante OAuth 2.0 in Gestione API di Azure | Documenti Microsoft
description: Informazioni su come gli utenti tooauthorize mediante OAuth 2.0 in Gestione API.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 78c48247-64f0-4708-b2d0-98b61a821283
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 934901dd6df399470a3257bf7a3a9b9fb5f40d5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-oauth-20-in-azure-api-management"></a>La modalità sviluppatore tooauthorize degli account con OAuth 2.0 in Gestione API di Azure
Supportano molte API [OAuth 2.0](http://oauth.net/2/) toosecure hello API e garantire che solo gli utenti validi hanno accesso, e possono accedere solo alle risorse toowhich hanno diritto. Nella Console per sviluppatori di interattiva della gestione degli ordini toouse Azure API con tali API servizio hello consente tooconfigure toowork di istanza del servizio con il OAuth 2.0 abilitato API.

## <a name="prerequisites"></a>Prerequisiti
Questa guida viene spiegato come tooconfigure toouse di istanza del servizio Gestione API autorizzazione OAuth 2.0 per sviluppatori di account, ma non verrà visualizzato come provider tooconfigure un OAuth 2.0. configurazione di Hello per ogni provider è diverso, sebbene hello passaggi sono simili e hello necessarie le informazioni utilizzate nella configurazione di OAuth 2.0 in all'istanza del servizio Gestione API sono di OAuth 2.0 hello stesso. Questo argomento mostra degli esempi di utilizzo di Azure Active Directory come provider OAuth 2.0.

> [!NOTE]
> Per ulteriori informazioni sulla configurazione di OAuth 2.0 tramite Azure Active Directory, vedere hello [WebApp-GraphAPI-DotNet] [ WebApp-GraphAPI-DotNet] esempio.
> 
> 

## <a name="step1"> </a>Configurare un server autorizzazione OAuth 2.0 in Gestione API
tooget avviato, fare clic su **portale di pubblicazione** in hello portale di Azure per il servizio Gestione API.

![Portale di pubblicazione][api-management-management-console]

> [!NOTE]
> Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.
> 
> 

Fare clic su **sicurezza** da hello **gestione API** menu a sinistra fare clic su di hello **OAuth 2.0**, quindi fare clic su **Aggiungi server di autorizzazione**.

![OAuth 2.0][api-management-oauth2]

Dopo aver fatto clic **Aggiungi server di autorizzazione**, hello nuova autorizzazione server form viene visualizzato.

![Nuovo server][api-management-oauth2-server-1]

Immettere un nome e una descrizione facoltativa in hello **nome** e **descrizione** campi. 

> [!NOTE]
> Questi campi sono server di autorizzazione OAuth 2.0 hello tooidentify utilizzati nell'istanza di servizio Gestione API corrente hello e i relativi valori non vengono forniti dal server hello OAuth 2.0.
> 
> 

Immettere hello **URL pagina di registrazione Client**. Questa pagina è in cui gli utenti possono creare e gestire gli account e varia a seconda hello OAuth 2.0 provider utilizzato. Hello **URL pagina di registrazione Client** punti toohello pagina che gli utenti possono utilizzare toocreate e configurare i propri account per i provider di OAuth 2.0 che supportano la gestione degli account utente. Alcune organizzazioni non configurare o utilizzare questa funzionalità, anche se il provider di hello OAuth 2.0 supporta. Se il provider OAuth 2.0 non dispone di gestione di utenti di account configurati, immettere un URL segnaposto, ad esempio hello URL dell'azienda o un URL, ad esempio `https://placeholder.contoso.com`.

sezione successiva di Hello del modulo hello contiene hello **tipi di concessione del codice di autorizzazione**, **autorizzazione URL dell'endpoint**, e **il metodo di richiesta di autorizzazione** impostazioni.

![Nuovo server][api-management-oauth2-server-2]

Specificare hello **tipi di concessione del codice di autorizzazione** dal controllo dei tipi di hello desiderato. **Authorization code** è specificato per impostazione predefinita.

Immettere hello **URL di endpoint di autorizzazione**. Per Azure Active Directory, questo URL sarà simile toohello seguente URL, in cui `<client_id>` viene sostituito con l'id client hello che identifica il server di applicazioni toohello OAuth 2.0.

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

Hello **il metodo di richiesta di autorizzazione** specifica la modalità di invio richiesta di autorizzazione hello server toohello OAuth 2.0. Il valore selezionato per impostazione predefinita è **GET** .

Nella sezione successiva Hello è dove hello **URL dell'endpoint del Token**, **metodi di autenticazione Client**, **token di accesso, l'invio di metodo**, e **ambitopredefinito** specificati.

![Nuovo server][api-management-oauth2-server-3]

Per un server di Azure Active Directory OAuth 2.0, hello **URL dell'endpoint del Token** avrà hello seguente formato, in cui `<APPID>` ha il formato di hello di `yourapp.onmicrosoft.com`.

`https://login.microsoftonline.com/<APPID>/oauth2/token`

Hello l'impostazione predefinita per **metodi di autenticazione Client** è **base**, e **token di accesso, l'invio di metodo** è **intestazione Authorization**. Questi valori configurati in questa sezione del modulo di hello, insieme a hello **ambito predefinito**.

Hello **credenziali Client** sezione contiene hello **ID Client** e **segreto Client**, che vengono ottenuti durante il processo di creazione e configurazione hello del OAuth 2.0 Server. Una volta hello **ID Client** e **segreto Client** vengono specificati, hello **redirect_uri** per hello **codice di autorizzazione** viene generato. Questo URI è l'URL di risposta hello tooconfigure utilizzati nella configurazione del server OAuth 2.0.

![Nuovo server][api-management-oauth2-server-4]

Se **tipi di concessione del codice di autorizzazione** è troppo**password del proprietario della risorsa**, hello **credenziali del proprietario risorsa** sezione è toospecify usate quelle credenziali; in caso contrario è possibile lasciare vuoto.

![Nuovo server][api-management-oauth2-server-5]

Una volta completato il modulo di hello, fare clic su **salvare** configurazione del server autorizzazione toosave hello API Gestione OAuth 2.0. Dopo aver salvato la configurazione del server hello, è possibile configurare le API toouse questa configurazione, come illustrato nella sezione successiva hello.

## <a name="step2"></a>Configurare un toouse API l'autorizzazione utente OAuth 2.0
Fare clic su **API** da hello **gestione API** hello menu a sinistra, fare clic sul nome hello dell'API di hello desiderato, fare clic su **sicurezza**, quindi selezionare la casella hello per **OAuth 2.0**.

![Autorizzazione utente][api-management-user-authorization]

Seleziona hello desiderato **server autorizzazione** dall'elenco a discesa hello, fare clic su **salvare**.

![Autorizzazione utente][api-management-user-authorization-save]

## <a name="step3"></a>Testare l'autorizzazione utente hello OAuth 2.0 in hello portale per sviluppatori
Dopo aver configurato il server di autorizzazione OAuth 2.0 e configurato toouse l'API del server, è possibile eseguirne il test selezionando toohello portale per sviluppatori e chiama un'API.  Fare clic su **portale per sviluppatori** nel menu in alto destra hello.

![Portale per sviluppatori][api-management-developer-portal-menu]

Fare clic su **API** nel menu in alto hello e scegliere **API Echo**.

![API Echo][api-management-apis-echo-api]

> [!NOTE]
> Se si dispone di un solo API configurata o account tooyour visibile, quindi fare clic su API consente di passare direttamente toohello operazioni dell'API.
> 
> 

Seleziona hello **ottenere risorse** operazione, fare clic su **aprire la Console di**, quindi selezionare **codice di autorizzazione** dall'elenco a discesa hello.

![Open console][api-management-open-console]

Quando **codice di autorizzazione** è selezionata, viene visualizzata una finestra popup con hello sign-in forma di provider hello OAuth 2.0. In questo esempio modulo di accesso hello viene fornito da Azure Active Directory.

> [!NOTE]
> Se si dispone di popup disabilitato, sarà richiesto tooenable dai browser hello. Dopo aver abilitato la loro, selezionare **codice di autorizzazione** hello e nuovo verrà visualizzato il modulo di accesso.
> 
> 

![pagina di accesso][api-management-oauth2-signin]

Dopo aver effettuato l'accesso, hello **le intestazioni di richiesta** vengono popolati con un `Authorization : Bearer` intestazione che autorizza la richiesta di hello.

![Token di intestazione della richiesta][api-management-request-header-token]

A questo punto è possibile configurare i valori hello desiderato per i parametri rimanenti hello e inviare la richiesta di hello. 

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sull'utilizzo di OAuth 2.0 e gestione API, vedere hello seguente video e accompagnamento [articolo](api-management-howto-protect-backend-with-aad.md).

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-oauth2/api-management-management-console.png
[api-management-oauth2]: ./media/api-management-howto-oauth2/api-management-oauth2.png
[api-management-user-authorization]: ./media/api-management-howto-oauth2/api-management-user-authorization.png
[api-management-user-authorization-save]: ./media/api-management-howto-oauth2/api-management-user-authorization-save.png
[api-management-oauth2-signin]: ./media/api-management-howto-oauth2/api-management-oauth2-signin.png
[api-management-request-header-token]: ./media/api-management-howto-oauth2/api-management-request-header-token.png
[api-management-developer-portal-menu]: ./media/api-management-howto-oauth2/api-management-developer-portal-menu.png
[api-management-open-console]: ./media/api-management-howto-oauth2/api-management-open-console.png
[api-management-oauth2-server-1]: ./media/api-management-howto-oauth2/api-management-oauth2-server-1.png
[api-management-oauth2-server-2]: ./media/api-management-howto-oauth2/api-management-oauth2-server-2.png
[api-management-oauth2-server-3]: ./media/api-management-howto-oauth2/api-management-oauth2-server-3.png
[api-management-oauth2-server-4]: ./media/api-management-howto-oauth2/api-management-oauth2-server-4.png
[api-management-oauth2-server-5]: ./media/api-management-howto-oauth2/api-management-oauth2-server-5.png
[api-management-apis-echo-api]: ./media/api-management-howto-oauth2/api-management-apis-echo-api.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

