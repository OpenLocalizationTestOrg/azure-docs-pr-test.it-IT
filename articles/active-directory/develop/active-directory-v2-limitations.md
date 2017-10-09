---
title: Active Directory aaaAzure v 2.0 endpoint limitazioni e restrizioni | Documenti Microsoft
description: Un elenco di limitazioni e restrizioni per l'endpoint v 2.0 hello Azure AD.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: a99289c0-e6ce-410c-94f6-c279387b4f66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: bcbb7239f1d117002d16ac23dca8f1feb13a9161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="should-i-use-hello-v20-endpoint"></a>È consigliabile utilizzare endpoint v 2.0 hello?
Quando si compilano applicazioni che si integrano con Azure Active Directory, è necessario toodecide se i protocolli di autenticazione e l'endpoint v 2.0 hello alle proprie esigenze. L'endpoint originale di Azure Active Directory è ancora completamente supportato e, per alcuni aspetti, include più funzionalità della versione 2.0. Tuttavia, hello v 2.0 endpoint [presenta vantaggi significativi](active-directory-v2-compare.md) per gli sviluppatori.

Di seguito sono riportati alcuni consigli per gli sviluppatori, opportunamente semplificati:

* Se nell'applicazione, è necessario supportare gli account Microsoft personali, è possibile utilizzare endpoint v 2.0 hello. Ma prima di procedere, assicurarsi di aver compreso le limitazioni di hello, illustrati in questo articolo.
* Se l'applicazione deve solo toosupport lavoro di Microsoft e gli account dell'istituto di istruzione, non usare endpoint v 2.0 hello. In alternativa, fare riferimento tooour [Guida per sviluppatori di Azure AD](active-directory-developers-guide.md).

Nel corso del tempo, endpoint v 2.0 hello aumenteranno restrizioni hello tooeliminate elencate di seguito, in modo che è necessario solo endpoint di toouse hello v 2.0. In hello frattempo, in questo articolo è toohelp previsto è determinare se l'endpoint di hello v 2.0 è adatta alle proprie esigenze. Continueremo tooupdate questo articolo tooreflect hello corrente dello stato dell'endpoint di hello v 2.0. Controllo di eseguire il backup tooreevaluate esigenze rispetto alle funzionalità v 2.0.

Se si dispone di un'app di Azure AD esistente che non usa l'endpoint di hello v 2.0, non sussiste alcuna necessità toostart da zero. In futuro hello, si fornirà un modo per si toouse delle applicazioni di Azure AD con endpoint v 2.0 hello.

## <a name="restrictions-on-app-types"></a>Restrizioni relative ai tipi di app
Attualmente, hello seguenti tipi di App non sono supportati dall'endpoint di hello v 2.0. Per una descrizione dei tipi di app supportate, vedere [tipi di App per l'endpoint v 2.0 di Azure Active Directory hello](active-directory-v2-flows.md).

### <a name="standalone-web-apis"></a>API Web autonome
È possibile utilizzare endpoint v 2.0 hello troppo[compilare un'API Web protetta con OAuth 2.0](active-directory-v2-flows.md#web-apis). Tuttavia, tale API Web può ricevere token solo da un'applicazione che ha hello stesso ID applicazione. Non è possibile accedere a un'API Web da un client con un ID applicazione diverso client Hello non essere in grado di toorequest oppure ottenere autorizzazioni tooyour API Web.

v 2.0 endpoint Web API negli esempi di hello toosee toobuild un'API Web che accetta i token da un client che ha hello stesso ID applicazione, vedere il nostro [Introduzione](active-directory-appmodel-v2-overview.md#getting-started) sezione.

## <a name="restrictions-on-app-registrations"></a>Restrizioni relative alle registrazioni di app
Attualmente, per ciascuna app che si desidera toointegrate con endpoint di hello v 2.0, è necessario creare una registrazione di app in hello nuovo [portale di registrazione dell'applicazione Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList). Azure AD esistente o App account Microsoft non sono compatibili con endpoint v 2.0 hello. Le applicazioni che sono registrate in un portale diverso dal portale di registrazione applicazione hello non sono compatibili con endpoint v 2.0 hello. In hello future, è possibile pianificare tooprovide toouse un modo un'applicazione esistente come app v 2.0. Tuttavia, non è attualmente presente alcun percorso di migrazione per un toowork app esistenti con endpoint v 2.0 hello.

Inoltre, le registrazioni di app create in hello [portale di registrazione applicazione](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) hanno hello seguenti avvertenze:

* Sono consentiti solo due segreti dell'app per ogni ID applicazione.
* La registrazione di un'app eseguita da un utente con un account Microsoft personale può essere visualizzata e gestita solo da un singolo account sviluppatore. Non può essere condiviso tra più sviluppatori.  Se si desidera tooshare la registrazione dell'app tra più sviluppatori, è possibile creare un'applicazione hello effettuando l'accesso al portale di registrazione hello con un account di Azure AD.
* Esistono numerose restrizioni sul formato hello di reindirizzamento hello URI che è consentito. Per ulteriori informazioni sull'URI di reindirizzamento, vedere la sezione successiva di hello.

## <a name="restrictions-on-redirect-uris"></a>Restrizioni relative agli URI di reindirizzamento
Le applicazioni che vengono registrate nel portale di registrazione applicazione hello non sono attualmente limitate tooa limitato set di valori URI di reindirizzamento. URI per le applicazioni web e servizi deve iniziare con schema hello reindirizzamento Hello `https`, e tutti i valori URI di reindirizzamento devono condividere un singolo dominio DNS. Non è possibile ad esempio registrare un'app Web con uno di questi URI di reindirizzamento:

`https://login-east.contoso.com`  
`https://login-west.contoso.com`

sistema di registrazione Hello Confronta hello intero DNS nome di hello esistente reindirizzamento URI toohello DNS di reindirizzamento hello URI che si sta aggiungendo. nome DNS di Hello richiesta tooadd hello avrà esito negativo se viene soddisfatta una delle seguenti condizioni hello:  

* intero nome DNS Hello dell'URI di reindirizzamento nuovo hello non corrisponde il nome DNS hello dell'URI di reindirizzamento esistente hello.
* intero nome DNS Hello dell'URI di reindirizzamento nuovo hello non è un sottodominio di URI di reindirizzamento esistente hello.

Ad esempio, se l'applicazione hello è l'URI di reindirizzamento:

`https://login.contoso.com`

È possibile aggiungere tooit, simile al seguente:

`https://login.contoso.com/new`

In questo caso, il nome DNS hello corrisponde esattamente. In alternativa, è possibile eseguire un'aggiunta analoga alla seguente:

`https://new.login.contoso.com`

In questo caso, si fa riferimento il sottodominio DNS tooa di login.contoso.com. Se si desidera toohave un'applicazione che dispone di account di accesso east.contoso.com e west.contoso.com account di accesso come URI di reindirizzamento, è necessario aggiungere che gli URI di reindirizzamento nell'ordine indicato:

`https://contoso.com`  
`https://login-east.contoso.com`  
`https://login-west.contoso.com`  

È possibile aggiungere due perché sono i sottodomini di hello innanzitutto l'URI di reindirizzamento, quest'ultimo hello contoso.com. Questa limitazione verrà rimossa in una versione futura.

vedere tooregister un'app nel portale di registrazione applicazione hello toolearn [come un'app con endpoint v 2.0 hello tooregister](active-directory-v2-app-registration.md).

## <a name="restrictions-on-services-and-apis"></a>Restrizioni relative a servizi e API
Attualmente, endpoint di hello v 2.0 supporta l'accesso per qualsiasi app che viene registrato nel portale di registrazione applicazione hello e che sia compresa nell'elenco di hello di [supportati flussi di autenticazione](active-directory-v2-flows.md). Tali app possono tuttavia acquisire il token di accesso di OAuth 2.0 per un set molto limitato di risorse. token solo per accedere a problemi di endpoint Hello v 2.0:

* app Hello che ha richiesto il token hello. Un'applicazione può acquisire un token di accesso per se stesso, se hello logica app è costituita da diversi diversi componenti o livelli. toosee questo scenario in azione, consultare il nostro [Introduzione](active-directory-appmodel-v2-overview.md#getting-started) esercitazioni.
* Hello posta elettronica di Outlook, calendario e contatti REST API, ognuno dei quali si trovano in https://outlook.office.com. toolearn toowrite un'applicazione che accede a queste API, vedere hello [Office Introduzione](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2) esercitazioni.
* API Microsoft Graph. Altre informazioni, vedere [Microsoft Graph](https://graph.microsoft.io) e dati hello tooyou disponibili.

Attualmente non sono supportati altri servizi. Altre Microsoft Online Services verrà aggiunto in futuro, hello inoltre toosupport per le API Web personalizzate e servizi.

## <a name="restrictions-on-libraries-and-sdks"></a>Restrizioni relative alle librerie e agli SDK
Attualmente, supporto della libreria per endpoint v 2.0 hello è limitato. Se si desideri che toouse hello v 2.0 endpoint in un'applicazione di produzione, sono disponibili queste opzioni:

* Se si compila un'applicazione web, è possibile utilizzare in modo sicuro Microsoft in genere disponibile sul lato server middleware tooperform Accedi e token di convalida. Middleware OWIN aprire ID connettersi hello includono per ASP.NET e hello Node.js Passport plug-in. Per esempi di codice che usano il middleware di Microsoft, vedere la sezione [Introduzione](active-directory-appmodel-v2-overview.md#getting-started).
* Se si compila un'applicazione desktop o portatile, è possibile usare una delle Microsoft Authentication Library (MSAL) di anteprima.  Queste librerie sono in anteprima supportata di produzione, pertanto è sicuro toouse usarle in applicazioni di produzione. È possibile leggere informazioni sui termini hello di hello visualizzare in anteprima e hello le librerie disponibili nel nostro [riferimento alle librerie di autenticazione](active-directory-v2-libraries.md).
* Per le piattaforme non coperto da librerie di Microsoft, è possibile integrare con endpoint v 2.0 hello direttamente inviando e ricevendo messaggi del protocollo nel codice dell'applicazione. protocolli di OpenID Connect e OAuth 2.0 Hello [sono documentate in modo esplicito](active-directory-v2-protocols.md) toohelp eseguire un'integrazione di questo tipo.
* Infine, è possibile utilizzare connettersi ID aprire open source e OAuth librerie toointegrate con endpoint v 2.0 hello. protocollo v 2.0 Hello devono essere compatibile con molte librerie di protocollo open source senza modifiche essenziali. disponibilità Hello di questi tipi di librerie dipende dalla lingua e la piattaforma. Hello [aprire ID connettersi](http://openid.net/connect/) e [OAuth 2.0](http://oauth.net/2/) siti Web di gestire un elenco di implementazioni più diffusi. Per ulteriori informazioni, vedere [librerie v 2.0 e l'autenticazione di Azure Active Directory](active-directory-v2-libraries.md)e hello elenco di librerie client open source ed esempi che sono stati testati con endpoint v 2.0 hello.

## <a name="restrictions-on-protocols"></a>Restrizioni relative ai protocolli
endpoint di Hello v 2.0 non supporta SAML o WS-Federation; supporta solo aprire ID connettersi e OAuth 2.0.  Non tutte le caratteristiche e funzionalità dei protocolli OAuth sono state integrate di endpoint di hello v 2.0. Queste funzionalità del protocollo e la funzionalità non sono attualmente *non disponibile* nell'endpoint di hello v 2.0:

* ID i token emessi da endpoint v 2.0 hello non contengono un `email` attestazione utente hello, anche se si acquisisce autorizzazioni hello utente tooview alla posta elettronica.
* endpoint di OpenID Connect UserInfo Hello non è implementata nell'endpoint di hello v 2.0. Tuttavia, tutti i dati di profilo utente che potenzialmente si potrebbero ricevere l'endpoint è disponibile da Microsoft Graph hello `/me` endpoint.
* Hello v 2.0 endpoint non supporta emittente ruolo o gruppo di attestazioni nei token ID.
* Hello [concessione di credenziali Password risorsa proprietario OAuth 2.0](https://tools.ietf.org/html/rfc6749#section-4.3) non è supportato dall'endpoint di hello v 2.0.

Ricordare hello v 2.0 endpoint non supporta alcuna forma di hello SAML o i protocolli WS-Federation.

toobetter comprendere l'ambito di hello di funzionalità del protocollo supportata nell'endpoint di hello v 2.0, leggere la [riferimento protocollo OpenID Connect e OAuth 2.0](active-directory-v2-protocols.md).

## <a name="restrictions-for-work-and-school-accounts"></a>Restrizioni relative agli account aziendali o dell'istituto di istruzione
Se è stato utilizzato Active Directory Authentication Library (ADAL) nelle applicazioni Windows, è possibile sfruttare l'autenticazione integrata di Windows, che usa una concessione di asserzione Security Assertion Markup Language (SAML) hello eseguita. Tale concessione consente agli utenti dei tenant di Azure AD federati di eseguire automaticamente l'autenticazione all'istanza di Active Directory locale senza immettere le credenziali. Attualmente, concessione di asserzione SAML hello non è supportato sull'endpoint di hello v 2.0.
