---
title: aaaAuthentication e l'autorizzazione in Azure App Service | Documenti Microsoft
description: "Riferimento concettuale e panoramica di hello autenticazione / autorizzazione funzionalità di servizio App di Azure"
services: app-service
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: b7151b57-09e5-4c77-a10c-375a262f17e5
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 08/29/2016
ms.author: mahender
ms.openlocfilehash: dc2074b16cce47b72b78ea7afeda89dbc4832166
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-in-azure-app-service"></a>Autenticazione e autorizzazione nel servizio app di Azure
## <a name="what-is-app-service-authentication--authorization"></a>Informazioni sull’autenticazione / autorizzazione di servizio app
L'autenticazione del servizio App / autorizzazione è una funzionalità che offre un modo per toosign l'applicazione degli utenti in modo che non si dispone di codice toochange sul back-end app hello. Fornisce un modo semplice di tooprotect dell'applicazione e il lavoro con i dati per ogni utente.

Il servizio app usa identità federate, in cui un provider di identità di terze parti archivia gli account e autentica gli utenti. un'applicazione Hello si basa su informazioni di identità del provider di hello in modo che hello app non dispone di toostore tali informazioni a se stesso. Servizio App supporta cinque provider di identità predefinito hello: Twitter, Facebook, Google, Account Microsoft e Azure Active Directory. L'app consente un numero qualsiasi di questi tooprovide di provider di identità gli utenti con le opzioni per la modalità accesso. supporto incorporato di hello tooexpand, è possibile integrare un altro provider di identità o [la propria soluzione di identità personalizzato][custom-auth].

Se si desidera tooget adesso, vedere una delle seguenti esercitazioni hello:

* [Aggiungere app per iOS tooyour autenticazione] [ iOS] (o [Android], [Windows], [xamarin], [ Xamarin], [xamarin. Forms], o [Cordova])
* [Autenticazione utente per le app per le API nel servizio app di Azure][apia-user]
* [Introduzione a Servizio app di Azure: parte 2][web-getstarted]

## <a name="how-authentication-works-in-app-service"></a>Funzionamento dell'autenticazione nel servizio app
In ordine tooauthenticate utilizzando uno dei provider di identità hello, è necessario innanzitutto tooconfigure hello identity provider tooknow sull'applicazione. provider di identità Hello specificherà i segreti forniti tooApp servizio e ID. Relazione di trust hello è stata completata in modo che il servizio App può convalidare asserzioni utente, ad esempio i token di autenticazione, dal provider di identità hello.

toosign, un utente utilizzando uno di questi provider, l'utente di hello deve essere reindirizzato tooan endpoint che esegue l'accesso agli utenti per tale provider. Se i clienti usano un web browser, è possibile avere servizio App di indirizzare automaticamente l'endpoint di toohello tutti gli utenti non autenticati che esegue l'accesso agli utenti. In caso contrario, sarà necessario toodirect clienti troppo`{your App Service base URL}/.auth/login/<provider>`, dove `<provider>` è uno dei seguenti valori hello: aad, facebook, google, microsoft o twitter. Gli scenari relativi alle API e ai dispositivi mobili sono illustrati nelle sezioni successive di questo articolo.

Gli utenti che interagiscono con l'applicazione tramite un Web browser avranno un cookie impostato in modo da rimanere autenticati mentre esplorano l'applicazione. Per altri tipi di client, ad esempio dispositivi mobili, un token web JSON (JWT), che deve essere presentata hello `X-ZUMO-AUTH` intestazione, verrà generato toohello client. SDK per applicazioni client di App per dispositivi mobili Hello questo gestirà automaticamente. In alternativa, un token di identità di Azure Active Directory o un token di accesso può essere direttamente incluso in hello `Authorization` intestazione come un [token di connessione](https://tools.ietf.org/html/rfc6750).

Servizio App convaliderà qualsiasi token che l'applicazione genera tooauthenticate utenti o i cookie. toorestrict che possa accedere all'applicazione, vedere hello [autorizzazione](#authorization) sezione più avanti in questo articolo.

### <a name="mobile-authentication-with-a-provider-sdk"></a>Autenticazione per dispositivi mobili con un SDK del provider
Dopo aver configurato tutti gli elementi nel back-end hello, è possibile modificare i client mobili toosign con il servizio App. Di seguito, sono disponibili due approcci:

* Utilizzare un SDK che un provider di identità specificato pubblica tooestablish identità e quindi ottenere accesso tooApp servizio.
* Utilizzare una singola riga di codice in modo che client di App per dispositivi mobili hello SDK possono accedere gli utenti.

> [!TIP]
> La maggior parte delle applicazioni devono utilizzare un provider SDK tooget un'esperienza più coerente quando l'utente accede, toouse supporto dell'aggiornamento e tooget specifica del provider di hello altri vantaggi.
> 
> 

Quando si utilizza un provider di SDK, gli utenti possono accedere tooan esperienza che più la stretta integrazione con sistema operativo hello app hello è in esecuzione. Inoltre, offre un token del provider e alcune informazioni utente sul client hello, che rende molto più semplice grafico tooconsume API e personalizzare l'esperienza utente hello. In alcuni casi su blog e forum, verrà visualizzato questo hello tooas denominata "flusso client" oppure "flusso diretto client" firma codice sul client hello in utenti e il codice client hello con token di accesso tooa provider.

Dopo aver ottenuto un token del provider, è necessario toobe inviati tooApp servizio per la convalida. Dopo che il servizio App convalida token hello, servizio App crea un nuovo token di servizio App che viene restituito toohello client. client di App per dispositivi mobili Hello SDK è toomanage metodi helper questo scambio e back-end dell'applicazione toohello hello token tooall le richieste di collegamento automatico. Gli sviluppatori possono inoltre includere un token di riferimento toohello provider, se richiesto.

### <a name="mobile-authentication-without-a-provider-sdk"></a>Autenticazione per dispositivi mobili senza un SDK del provider
Se non si desidera tooset di un provider SDK, è possibile consentire funzionalità di hello App per dispositivi mobili di Azure App Service toosign in per l'utente. client di App per dispositivi mobili Hello SDK verrà aperto un provider di toohello visualizzazione web di propria scelta e l'accesso utente hello. In alcuni casi su blog e forum, verrà visualizzato questo hello tooas denominata "flusso server" o "indirizzate al server di flusso" perché server hello gestisce il processo hello che esegue l'accesso agli utenti e client hello SDK non riceve mai il token provider hello.

Codice toostart che questo flusso è incluso nell'esercitazione di autenticazione hello per ogni piattaforma. Alla fine hello flusso hello, hello client SDK dispone di un token di servizio App e token hello viene automaticamente collegato tooall richieste toohello applicazione back-end.

### <a name="service-to-service-authentication"></a>Autenticazione da servizio a servizio
Anche se è possibile concedere agli utenti accesso tooyour applicazione, è possibile inoltre considerare attendibile un'altra applicazione toocall proprio API. È ad esempio possibile che un'app Web chiami un'API in un'altra app Web. In questo scenario, si utilizzano credenziali per un account del servizio anziché le credenziali di utente tooget un token. Un account del servizio è noto anche come *entità servizio* in Azure Active Directory, mentre l'autenticazione che usa un account di questo tipo è nota anche come scenario da servizio a servizio.

> [!IMPORTANT]
> Dato che le app per dispositivi mobili vengono eseguite su dispositivi del cliente, tali applicazioni *non* sono considerate applicazioni attendibili e non devono usare un flusso dell'entità servizio. È invece necessario usare un flusso utente descritto sopra.
> 
> 

Per gli scenari da servizio a servizio, il servizio app può proteggere l'applicazione con Azure Active Directory. applicazione chiamante Hello deve semplicemente tooprovide un token di autorizzazione dell'entità servizio di Azure Active Directory che viene ottenuto fornendo hello client ID e client secret da Azure Active Directory. Viene illustrato un esempio di questo scenario che usa l'App per le API di ASP.NET dall'esercitazione hello [l'autenticazione dell'entità servizio per App per le API][apia-service].

Se si desidera toouse toohandle l'autenticazione di servizio App uno scenario di servizio, è possibile utilizzare l'autenticazione di base o i certificati client. Per informazioni sui certificati client in Azure, vedere [come l'autenticazione reciproca TLS per le app Web tooConfigure](../app-service-web/app-service-web-configure-tls-mutual-auth.md). Per informazioni sull'autenticazione di base in ASP.NET, vedere il blog sui [filtri di autenticazione nell'API Web 2 ASP.NET](http://www.asp.net/web-api/overview/security/authentication-filters).

L'autenticazione account di servizio da un'applicazione di servizio App logica app tooan API è un caso speciale dettagliato in [utilizzando l'API personalizzata ospitato nel servizio App con la logica app](../logic-apps/logic-apps-custom-hosted-api.md).

## <a name="authorization"></a>Funzionamento dell'autorizzazione nel servizio app
È il controllo completo su richieste hello che possa accedere all'applicazione. L'autenticazione del servizio App / autorizzazione può essere configurata con i seguenti comportamenti hello:

* Consentire solo le richieste autenticate tooreach all'applicazione.
  
    Se un browser riceve una richiesta anonima, servizio App verrà reindirizzata tooa pagina per i provider di identità hello che si sceglie in modo che gli utenti possono accedere. Se la richiesta hello proviene da un dispositivo mobile, hello restituito risposta HTTP *401 non autorizzato* risposta.
  
    Con questa opzione, non è necessario toowrite qualsiasi codice di autenticazione affatto nell'app. Se è necessaria l'autorizzazione più preciso, le informazioni sull'utente hello sono codice tooyour disponibili.
* Consentire tutte le richieste tooreach all'applicazione, ma convalidare le richieste autenticate e passare le informazioni di autenticazione nelle intestazioni HTTP hello.
  
    Questa opzione rinvia il codice di applicazione tooyour decisioni di autorizzazione. Fornisce una maggiore flessibilità nella gestione delle richieste anonime, ma si dispone di codice toowrite.
* Consentire all'applicazione di tutte le richieste tooreach ed eseguita alcuna operazione sulle informazioni di autenticazione nelle richieste hello.
  
    In questo caso, hello autenticazione / autorizzazione funzionalità è disattivata. attività di Hello di autenticazione e autorizzazione sono completamente il codice di applicazione tooyour.

comportamenti di Hello precedente sono controllati da hello **tootake azione quando la richiesta non è autenticata** opzione hello portale di Azure. Se si sceglie * * Log con *nome provider* * *, tutte le richieste hanno toobe autenticato. **Consenti richiesta (alcuna azione)** rinvia codice di tooyour decisione di autorizzazione hello, ma fornisce comunque informazioni di autenticazione. Se si desidera toohave di gestire tutto il codice, è possibile disabilitare l'autenticazione hello / la funzionalità di autorizzazione.

## <a name="working-with-user-identities-in-your-application"></a>Utilizzo delle identità utente nell'applicazione
Servizio App passa un'applicazione di tooyour informazioni utente utilizzando le intestazioni speciali. Le richieste esterne non consentono queste intestazioni e saranno presenti solo se impostate dall'autenticazione/autorizzazione del servizio app. Ecco alcune intestazioni di esempio:

* X-MS-CLIENT-PRINCIPAL-NAME
* X-MS-CLIENT-PRINCIPAL-ID
* X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN
* X-MS-TOKEN-FACEBOOK-EXPIRES-ON

Il codice scritto in qualsiasi lingua o framework è possibile ottenere informazioni di hello necessari da queste intestazioni. Per le applicazioni ASP.NET 4.6, hello **ClaimsPrincipal** viene impostato automaticamente con i valori appropriati di hello.

L'applicazione può anche ottenere ulteriori dettagli sull'utente tramite una richiesta HTTP GET in hello `/.auth/me` endpoint dell'applicazione. Un token valido che è incluso con richiesta di hello verrà restituito un payload JSON con i dettagli sul provider hello in uso, hello token del provider sottostante e altre informazioni utente. il server di App per dispositivi mobili SDK Hello forniscono metodi helper toowork con i dati. Per ulteriori informazioni, vedere [come toouse hello Azure Mobile App Node.js SDK](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-getidentity), e [funziona con server di back-end .NET hello SDK per App mobili di Azure](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#user-info).

## <a name="documentation-and-additional-resources"></a>Documentazione e risorse aggiuntive
### <a name="identity-providers"></a>Provider di identità
Hello seguenti esercitazioni Mostra come provider di autenticazione diversi toouse tooconfigure servizio App:

* [Come tooconfigure l'accesso di Azure Active Directory toouse app][AAD]
* [Come tooconfigure l'account di accesso Facebook toouse app][Facebook]
* [Come tooconfigure l'account di accesso Google toouse app][Google]
* [Come tooconfigure l'account di accesso di app toouse Account Microsoft][MSA]
* [Come tooconfigure l'account di accesso Twitter toouse app][Twitter]

Se si desidera toouse un sistema di identità diverso da hello quelle fornite in questo caso, è inoltre possibile utilizzare hello [anteprima supporto dell'autenticazione personalizzata hello Mobile app .NET Server SDK][custom-auth], che può essere usato nelle App web, App per dispositivi mobili, o App per le API.

### <a name="web-applications"></a>Applicazioni Web
Hello seguenti esercitazioni Mostra come applicazione web tooadd tooa di autenticazione:

* [Introduzione a Servizio app di Azure: parte 2][web-getstarted]

### <a name="mobile-applications"></a>Applicazioni per dispositivi mobili
Hello seguenti esercitazioni Mostra come client mobili tooadd autenticazione tooyour utilizzando hello indirizzate al server di flusso:

* [Aggiungere app per iOS tooyour autenticazione][iOS]
* [Aggiungere app Android di autenticazione tooyour][Android]
* [Aggiungere app di Windows Authentication tooyour][Windows]
* [Aggiungere app xamarin di autenticazione tooyour][xamarin]
* [Aggiungere app xamarin di autenticazione tooyour][ Xamarin]
* [Aggiungere app xamarin. Forms per authentication tooyour][xamarin. Forms]
* [Aggiungere app Cordova di autenticazione tooyour][Cordova]

Utilizzare hello seguenti risorse, se si desidera toouse hello diretta dal client del flusso di Azure Active Directory:

* [Utilizzare hello Active Directory Authentication Library per iOS][ADAL-iOS]
* [Usare hello Active Directory Authentication Library per Android][ADAL-Android]
* [Utilizzare hello Active Directory Authentication Library per Windows e Xamarin][ADAL-dotnet]

Utilizzare hello seguenti risorse, se si desidera toouse hello diretta dal client del flusso di Facebook per:

* [Utilizzare hello SDK Facebook per iOS](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#facebook-sdk)

Utilizzare hello seguenti risorse, se si desidera toouse hello diretta dal client del flusso per Twitter:

* [Usare Twitter Fabric for iOS](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#twitter-fabric)

Utilizzare hello seguenti risorse, se si desidera toouse hello diretta dal client del flusso per Google:

* [Utilizzare hello Google Accedi SDK per iOS](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#google-sdk)

### <a name="api-applications"></a>Applicazioni per le API
Hello seguenti esercitazioni Mostra come tooprotect App API:

* [Autenticazione utente per le app per le API nel servizio app di Azure][apia-user]
* [Autenticazione dell'entità servizio per app per le API nel servizio app di Azure][apia-service]

[apia-user]: ../app-service-api/app-service-api-dotnet-user-principal-auth.md
[apia-service]: ../app-service-api/app-service-api-dotnet-service-principal-auth.md

[web-getstarted]: ../app-service-web/app-service-web-get-started-2.md#authenticate-your-users

[iOS]: ../app-service-mobile/app-service-mobile-ios-get-started-users.md
[Android]: ../app-service-mobile/app-service-mobile-android-get-started-users.md
[xamarin]: ../app-service-mobile/app-service-mobile-xamarin-ios-get-started-users.md
[ Xamarin]: ../app-service-mobile/app-service-mobile-xamarin-android-get-started-users.md
[xamarin. Forms]: ../app-service-mobile/app-service-mobile-xamarin-forms-get-started-users.md
[Windows]: ../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-users.md
[Cordova]: ../app-service-mobile/app-service-mobile-cordova-get-started-users.md

[AAD]: ../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md
[Facebook]: ../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md
[Google]: ../app-service-mobile/app-service-mobile-how-to-configure-google-authentication.md
[MSA]: ../app-service-mobile/app-service-mobile-how-to-configure-microsoft-authentication.md
[Twitter]: ../app-service-mobile/app-service-mobile-how-to-configure-twitter-authentication.md

[custom-auth]: ../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth

[ADAL-Android]: ../app-service-mobile/app-service-mobile-android-how-to-use-client-library.md#adal
[ADAL-iOS]: ../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#adal
[ADAL-dotnet]: ../app-service-mobile/app-service-mobile-dotnet-how-to-use-client-library.md#adal
