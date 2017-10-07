---
title: aaaAzure Active Directory l'autenticazione e Gestione risorse | Documenti Microsoft
description: Tooauthentication manuale dello sviluppatore con hello API di gestione risorse di Azure e Azure Active Directory per l'integrazione di un'app con altre sottoscrizioni di Azure.
services: azure-resource-manager,active-directory
documentationcenter: na
author: dushyantgill
manager: timlt
editor: tysonn
ms.assetid: 17b2b40d-bf42-4c7d-9a88-9938409c5088
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/27/2016
ms.author: dugill;tomfitz
ms.openlocfilehash: 757e45fdb28488b45de70647746461888bf35a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-resource-manager-authentication-api-tooaccess-subscriptions"></a>Utilizzare le sottoscrizioni tooaccess autenticazione API di gestione risorse
## <a name="introduction"></a>Introduzione
Se si è uno sviluppatore di software che deve toocreate un'app che gestisce le risorse di Azure del cliente, in questo argomento Mostra come tooauthenticate con hello le API di gestione risorse di Azure e ottenere l'accesso tooresources in altre sottoscrizioni.

L'app possa accedere hello API di gestione risorse in due modi:

1. **Accesso utente + app**: per le app che accedono alle risorse per conto di un utente connesso. Questo approccio funziona per le app, ad esempio le app Web e gli strumenti da riga di comando, che trattano solo la "gestione interattiva" delle risorse di Azure.
2. **Accesso solo app**: per le app che eseguono servizi daemon e processi pianificati. identità dell'applicazione Hello viene concesso l'accesso diretto alle risorse di toohello. Questo approccio funziona per le app che servono a lungo termine tooAzure headless accesso (esecuzione automatica).

Questo argomento vengono fornite istruzioni dettagliate toocreate un'applicazione che utilizza entrambi i metodi di autorizzazione. Viene illustrato come tooperform ogni passaggio con l'API REST o c#. un'applicazione ASP.NET MVC Hello completezza è disponibile all'indirizzo [https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense](https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense).

## <a name="what-hello-web-app-does"></a>Le app web hello non
app web Hello:

1. Esegue l'accesso per un utente di Azure.
2. Chiede utente toogrant hello web app accesso tooResource Manager.
3. Ottiene il token di accesso app + utente per l'accesso a Resource Manager.
4. Usa token (dal passaggio 3) toocall Gestione risorse e ruolo tooa principale di servizio dell'applicazione hello assegnare nella sottoscrizione hello, che fornisce una sottoscrizione di toohello di hello app a lungo termine accesso.
5. Ottiene il token di accesso solo app.
6. Usa token (dal passaggio 5) toomanage risorse nella sottoscrizione hello tramite Gestione risorse.

Ecco il flusso di hello end-to-end dell'applicazione web hello.

![Flusso di autenticazione di Resource Manager](./media/resource-manager-api-authentication/Auth-Swim-Lane.png)

Come un utente, fornire l'id di sottoscrizione hello per sottoscrizione hello desiderato toouse:

![Fornire l'ID sottoscrizione](./media/resource-manager-api-authentication/sample-ux-1.png)

Selezionare hello toouse di account per l'accesso.

![Selezionare un account](./media/resource-manager-api-authentication/sample-ux-2.png)

Fornire le credenziali.

![Fornire le credenziali](./media/resource-manager-api-authentication/sample-ux-3.png)

Concedere hello app accesso tooyour le sottoscrizioni di Azure:

![Concedere l'accesso](./media/resource-manager-api-authentication/sample-ux-4.png)

Gestire le sottoscrizioni connesse:

![Connettere la sottoscrizione](./media/resource-manager-api-authentication/sample-ux-7.png)

## <a name="register-application"></a>Registrare l'applicazione
Prima di iniziare a scrivere codice, registrare l'app Web in Azure Active Directory (AD). registrazione app Hello crea un'identità centrale per l'app in Azure AD. Contiene informazioni di base sull'applicazione quali ID Client OAuth, gli URL di risposta e le credenziali che l'applicazione usa tooauthenticate e le API di gestione risorse di Azure di accesso. registrazione app Hello registra inoltre hello vari delegate le autorizzazioni necessarie all'applicazione quando si accede a Microsoft APIs per conto di utente hello.

Poiché l'applicazione accede ad altre sottoscrizioni, è necessario configurarla come un'applicazione multi-tenant. convalida toopass, fornire un dominio associato con Azure Active Directory. domini di hello toosee associati di Azure Active Directory, accedi toohello [portale classico](https://manage.windowsazure.com). Selezionare l'istanza di Azure Active Directory e quindi selezionare **Domini**.

Hello di esempio seguente viene illustrato come tooregister hello app usando Azure PowerShell. È necessario disporre di hello versione più recente (agosto 2016) di Azure PowerShell per toowork questo comando.

    $app = New-AzureRmADApplication -DisplayName "{app name}" -HomePage "https://{your domain}/{app name}" -IdentifierUris "https://{your domain}/{app name}" -Password "{your password}" -AvailableToOtherTenants $true

toolog in come hello applicazione Active Directory, è necessario che la password e l'id dell'applicazione hello. id applicazione hello toosee restituito dal comando precedente hello, utilizzare:

    $app.ApplicationId

Hello di esempio seguente viene illustrato come tooregister hello app usando l'interfaccia CLI di Azure.

    azure ad app create --name {app name} --home-page https://{your domain}/{app name} --identifier-uris https://{your domain}/{app name} --password {your password} --available true

i risultati di Hello includono hello AppId, è necessario per l'autenticazione come applicazione hello.

### <a name="optional-configuration---certificate-credential"></a>Configurazione facoltativa: credenziali del certificato
Azure AD supporta anche le credenziali del certificato per le applicazioni: creare un certificato autofirmato, mantenere la chiave privata di hello e aggiungere una registrazione dell'applicazione hello tooyour chiave pubblica Azure AD. Per l'autenticazione, l'applicazione invia un tooAzure piccoli payload AD firmato con la chiave privata e Azure AD convalida firma hello con la chiave pubblica hello registrato.

Per informazioni sulla creazione di un'app di Active Directory con un certificato, vedere [toocreate usare Azure PowerShell un'entità servizio tooaccess risorse](resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority) o [toocreate CLI di Azure di utilizzare un'entità servizio tooaccess risorse](resource-group-authenticate-service-principal-cli.md#create-service-principal-with-certificate).

## <a name="get-tenant-id-from-subscription-id"></a>Ottenere l'ID tenant dall'ID sottoscrizione
toorequest un token che può essere utilizzati toocall Gestione risorse, l'applicazione deve tooknow hello tenant ID del tenant di Azure AD hello che ospita hello sottoscrizione di Azure. Molto probabilmente gli utenti conoscono i relativi ID sottoscrizione, ma potrebbero non conoscere gli ID tenant per Azure Active Directory. tooget hello id tenant dell'utente, chiedere utente hello per l'id sottoscrizione hello. Quando si invia una richiesta di informazioni sulla sottoscrizione hello, fornire tale id sottoscrizione:

    https://management.azure.com/subscriptions/{subscription-id}?api-version=2015-01-01

richiesta di Hello non riesce perché l'utente hello ha non ancora connessi, ma è possibile recuperare l'id tenant hello dalla risposta hello. Tale eccezione, recuperare l'id tenant hello dal valore di intestazione di risposta hello per **WWW-Authenticate**. Vedrai questa implementazione di hello [GetDirectoryForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L20) metodo.

## <a name="get-user--app-access-token"></a>Ottenere il token di accesso utente + app
L'applicazione reindirizza hello utente tooAzure Active Directory con un OAuth 2.0 autorizzare richiedere - tooauthenticate hello credenziali dell'utente e ottenere un codice di autorizzazione. L'applicazione utilizza tooget codice di autorizzazione hello un token di accesso per Gestione risorse. Hello [ConnectSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/Controllers/HomeController.cs#L42) metodo crea una richiesta di autorizzazione hello.

Questo argomento viene illustrato l'utente di hello tooauthenticate di richieste di hello API REST. Inoltre, è possibile utilizzare l'autenticazione di helper librerie tooperform nel codice. Per altre informazioni su queste librerie, vedere [Azure Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (Libreria di autenticazione di Azure Active Directory). Per informazioni aggiuntive su come integrare la gestione delle identità in un'applicazione, vedere [Guida per gli sviluppatori di Azure Active Directory](../active-directory/active-directory-developers-guide.md).

### <a name="auth-request-oauth-20"></a>Richiesta di autorizzazione (OAuth 2.0)
Eseguire un endpoint di Authorize toohello Azure AD aprire Connect/OAuth 2.0 autorizzare richieste di ID:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize

parametri di stringa di query Hello sono disponibili per la richiesta sono descritti in hello [richiedere un codice di autorizzazione](../active-directory/develop/active-directory-protocols-oauth-code.md#request-an-authorization-code) argomento.

Hello seguente esempio viene illustrato come toorequest autorizzazione OAuth 2.0:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=query&response_type=code&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&domain_hint=live.com

Azure AD autentica l'utente hello e, se necessario, chiede hello utente toogrant autorizzazione toohello app. Restituisce toohello codice di autorizzazione hello URL di risposta dell'applicazione. A seconda di hello richiesto response_mode, Azure AD entrambi invia nuovamente hello dati nella stringa di query o come dati post.

    code=AAABAAAAiL****FDMZBUwZ8eCAA&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="auth-request-open-id-connect"></a>Richiesta di autorizzazione (Open ID Connect)
Anche se non si solo tooaccess Gestione risorse di Azure per conto di utente hello, consentono inoltre di hello utente toosign tooyour applicazione usando il proprio account Azure AD, emettere un Open ID autorizzare richiesta di connessione. Con Connect Open ID, l'applicazione riceve un id_token da Azure AD che l'app è possibile utilizzare toosign utente hello.

parametri di stringa di query Hello sono disponibili per la richiesta sono descritti in hello [richiesta di accesso hello trasmissione](../active-directory/develop/active-directory-protocols-openid-connect-code.md#send-the-sign-in-request) argomento.

Una richiesta Open ID Connect di esempio è:

     https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=form_post&response_type=code+id_token&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&scope=openid+profile&nonce=63567Dc4MDAw&domain_hint=live.com&state=M_12tMyKaM8

Azure AD autentica l'utente hello e, se necessario, chiede hello utente toogrant autorizzazione toohello app. Restituisce toohello codice di autorizzazione hello URL di risposta dell'applicazione. A seconda di hello richiesto response_mode, Azure AD entrambi invia nuovamente hello dati nella stringa di query o come dati post.

Una risposta Open ID Connect di esempio è:

    code=AAABAAAAiL*****I4rDWd7zXsH6WUjlkIEQxIAA&id_token=eyJ0eXAiOiJKV1Q*****T3GrzzSFxg&state=M_12tMyKaM8&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="token-request-oauth20-code-grant-flow"></a>Richiesta di token (flusso di concessione del codice OAuth 2.0)
Ora che l'applicazione ha ricevuto il codice di autorizzazione hello da Azure AD, è possibile token di accesso ora tooget hello per Gestione risorse di Azure.  Registrare un endpoint Token di Azure AD toohello richiesta Token di OAuth 2.0 codice Grant:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

parametri di stringa di query Hello sono disponibili per la richiesta sono descritti in hello [utilizzare il codice di autorizzazione hello](../active-directory/develop/active-directory-protocols-oauth-code.md#use-the-authorization-code-to-request-an-access-token) argomento.

Hello di esempio seguente mostra una richiesta di token di concessione di codice con le credenziali di password:

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

Quando si utilizzano le credenziali del certificato, è possibile creare un JSON Web Token (JWT) e accedere (RSA SHA256) utilizzando hello chiave privata della credenziale di certificato dell'applicazione. Hello tipi di attestazione per il token hello vengono visualizzati [le attestazioni nei token JWT](../active-directory/develop/active-directory-protocols-oauth-code.md#jwt-token-claims). Per riferimento, vedere hello [codice Active Directory Authentication Library (.NET)](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/blob/dev/src/ADAL.PCL.Desktop/CryptographyHelper.cs) toosign i token JWT asserzione Client.

Vedere hello [aprire ID connettersi spec](http://openid.net/specs/openid-connect-core-1_0.html#ClientAuthentication) per ulteriori informazioni sull'autenticazione client.

Hello di esempio seguente mostra una richiesta di token di concessione di codice con le credenziali di certificato:

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbG*****Y9cYo8nEjMyA

Risposta di esempio per il token di concessione del codice:

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039858","not_before":"1432035958","resource":"https://management.core.windows.net/","access_token":"eyJ0eXAiOiJKV1Q****M7Cw6JWtfY2lGc5A","refresh_token":"AAABAAAAiL9Kn2Z****55j-sjnyYgAA","scope":"user_impersonation","id_token":"eyJ0eXAiOiJKV*****-drP1J3P-HnHi9Rr46kGZnukEBH4dsg"}

#### <a name="handle-code-grant-token-response"></a>Gestire la risposta del token di concessione del codice
Una risposta corretta token contiene i token di accesso hello (utente + app) per Gestione risorse di Azure. L'applicazione usa questo accesso token tooaccess Gestione risorse per conto di utente hello. durata Hello dei token di accesso rilasciato da Azure AD è un'ora. È improbabile che l'applicazione web necessita di token di accesso toorenew hello (utente + app). Se è richiesto il token di accesso di toorenew hello, usare i token di aggiornamento hello che l'applicazione riceve in risposta token hello. Registrare un endpoint Token di Azure AD toohello richiedere Token OAuth 2.0:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

Hello toouse parametri con richiesta di aggiornamento hello sono descritti in [aggiornati i token di accesso hello](../active-directory/develop/active-directory-protocols-oauth-code.md#refreshing-the-access-tokens).

Hello esempio seguente viene illustrato come token di aggiornamento toouse hello:

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=refresh_token&refresh_token=AAABAAAAiL9Kn2Z****55j-sjnyYgAA&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

Anche se i token di aggiornamento possono essere utilizzato tooget nuova i token di accesso per Gestione risorse di Azure, non sono adatti per l'accesso offline dall'applicazione. durata token di aggiornamento Hello è limitata e token di aggiornamento sono associati toohello utente. Se l'utente hello lascia l'organizzazione hello, applicazione hello utilizzando il token di aggiornamento hello perde l'accesso. Questo approccio non è adatto per le applicazioni che vengono utilizzati dal team toomanage le risorse di Azure.

## <a name="check-if-user-can-assign-access-toosubscription"></a>Controllare se l'utente può assegnare toosubscription accesso
A questo punto l'applicazione ha un token tooaccess Gestione risorse di Azure per conto di utente hello. passaggio successivo Hello è tooconnect sottoscrizione toohello app. Dopo la connessione, l'app può gestire le sottoscrizioni anche quando l'utente hello non è presenti (accesso offline a lungo termine).

Per ogni sottoscrizione tooconnect, chiamare hello [autorizzazioni relative agli elenchi di gestione risorse](https://docs.microsoft.com/rest/api/authorization/permissions) toodetermine API utente hello se dispone di diritti di gestione di accesso per la sottoscrizione di hello.

Hello [UserCanManagerAccessForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L44) metodo hello app di esempio ASP.NET MVC implementa questa chiamata.

Hello seguente esempio viene illustrato come toorequest le autorizzazioni dell'utente per una sottoscrizione. 83cfe939-2402-4581-b761-4f59b0a041e4 è l'id di hello di hello sottoscrizione.

    GET https://management.azure.com/subscriptions/83cfe939-2402-4581-b761-4f59b0a041e4/providers/microsoft.authorization/permissions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiLC***lwO1mM7Cw6JWtfY2lGc5A

È un esempio di autorizzazioni dell'utente di hello risposta tooget nella sottoscrizione.

    HTTP/1.1 200 OK

    {"value":[{"actions":["*"],"notActions":["Microsoft.Authorization/*/Write","Microsoft.Authorization/*/Delete"]},{"actions":["*/read"],"notActions":[]}]}

le autorizzazioni di Hello API restituisce più autorizzazioni. Ogni autorizzazione è costituita dalle azioni consentite (actions) e dalle azioni non consentite (notactions). Se è presente nell'elenco di azioni di un'autorizzazione consentito hello un'azione e non è presente nell'elenco notactions hello di tale autorizzazione, hello utente è consentito tooperform tale azione. **Microsoft.Authorization/roleassignments/Write** azione hello che rights management che concede l'accesso. L'applicazione è necessario analizzare hello autorizzazioni risultato toolook per trovare una corrispondenza di espressione regolare in questa stringa di azione in azioni di hello e notactions di ciascuna autorizzazione.

## <a name="get-app-only-access-token"></a>Ottenere il token di accesso solo app
A questo punto, si conosce se hello utente può assegnare a toohello accesso sottoscrizione di Azure. passaggi successivi Hello sono:

1. Assegnare hello appropriato RBAC ruolo tooyour identità dell'applicazione per la sottoscrizione hello.
2. Convalidare l'assegnazione di accesso di hello eseguendo una query per l'autorizzazione dell'applicazione hello sottoscrizione hello o l'accesso alla gestione di risorse utilizzando il token solo per app.
3. Connessione hello record nella struttura di dati applicazioni "sottoscrizioni connessi" - id hello della sottoscrizione di hello di persistenza.

Verrà ora esaminato il primo passaggio hello più da vicino. tooassign hello appropriato RBAC ruolo toohello identità dell'applicazione, è necessario determinare:

* id di oggetto Hello dell'identità dell'applicazione Azure Active Directory dell'utente hello
* Identificatore del ruolo RBAC hello che l'applicazione richiede sottoscrizione hello Hello

Quando l'applicazione autentica un utente da un'istanza di Azure AD, crea un oggetto entità servizio per l'applicazione in tale istanza di Azure AD. Azure consente RBAC ruoli toobe assegnato entità tooservice applicazioni di toocorresponding toogrant accesso diretto alle risorse di Azure. Questa azione è esattamente ciò che si desidera toodo. Query hello Azure AD Graph API toodetermine hello identificatore dell'entità servizio hello dell'applicazione dell'utente connesso di hello's Azure AD.

È necessario un token di accesso per Gestione risorse di Azure, è necessario un nuovo hello di toocall token di accesso API Azure AD Graph. Ogni applicazione in Azure AD ha autorizzazione tooquery il proprio oggetto entità servizio, pertanto è sufficiente un token di accesso solo app.

<a id="app-azure-ad-graph" />

### <a name="get-app-only-access-token-for-azure-ad-graph-api"></a>Ottenere il token di accesso solo app per l'API Graph di Azure AD
tooauthenticate l'app e ottenere un token tooAzure AD Graph API, emettere un endpoint token OAuth 2.0 concessione di credenziali Client del flusso richiesta di token tooAzure AD (**https://login.microsoftonline.com/ {directory_domain_name} / OAuth2/Token**).

Hello [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs) metodo dell'applicazione di esempio ASP.net MVC Ottiene un accesso solo app token per l'utilizzo di API Graph hello hello Active Directory Authentication Library per .NET.

parametri di stringa di query Hello sono disponibili per la richiesta sono descritti in hello [richiedere un Token di accesso](../active-directory/develop/active-directory-protocols-oauth-service-to-service.md#request-an-access-token) argomento.

Richiesta di esempio del token di concessione delle credenziali client:

    POST https://login.microsoftonline.com/62e173e9-301e-423e-bcd4-29121ec1aa24/oauth2/token HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 187</pre>
    <pre>grant_type=client_credentials&client_id=a0448380-c346-4f9f-b897-c18733de9394&resource=https%3A%2F%2Fgraph.windows.net%2F &client_secret=olna8C*****Og%3D

Risposta di esempio del token di concessione delle credenziali client:

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039862","not_before":"1432035962","resource":"https://graph.windows.net/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRv****G5gUTV-kKorR-pg"}

### <a name="get-objectid-of-application-service-principal-in-user-azure-ad"></a>Ottenere l'ObjectId dell'entità servizio dell'applicazione nella directory Azure AD dell'utente
A questo punto, usare hello tooquery token di accesso solo per app hello [le entità servizio di Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity) hello toodetermine API Id oggetto dell'entità servizio dell'applicazione hello nella directory hello.

Hello [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs#) metodo hello applicazione di esempio ASP.net MVC implementa questa chiamata.

Hello seguente esempio viene illustrato come toorequest principale di un'applicazione del servizio. a0448380-c346-4f9f-b897-c18733de9394 è l'id client hello di un'applicazione hello.

    GET https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/servicePrincipals?api-version=1.5&$filter=appId%20eq%20'a0448380-c346-4f9f-b897-c18733de9394' HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJK*****-kKorR-pg

Hello esempio seguente viene illustrata una risposta toohello richiesta per il servizio di un'applicazione principale

    HTTP/1.1 200 OK

    {"odata.metadata":"https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/$metadata#directoryObjects/Microsoft.DirectoryServices.ServicePrincipal","value":[{"odata.type":"Microsoft.DirectoryServices.ServicePrincipal","objectType":"ServicePrincipal","objectId":"9b5018d4-6951-42ed-8a92-f11ec283ccec","deletionTimestamp":null,"accountEnabled":true,"appDisplayName":"CloudSense","appId":"a0448380-c346-4f9f-b897-c18733de9394","appOwnerTenantId":"62e173e9-301e-423e-bcd4-29121ec1aa24","appRoleAssignmentRequired":false,"appRoles":[],"displayName":"CloudSense","errorUrl":null,"homepage":"http://www.vipswapper.com/cloudsense","keyCredentials":[],"logoutUrl":null,"oauth2Permissions":[{"adminConsentDescription":"Allow hello application tooaccess CloudSense on behalf of hello signed-in user.","adminConsentDisplayName":"Access CloudSense","id":"b7b7338e-683a-4796-b95e-60c10380de1c","isEnabled":true,"type":"User","userConsentDescription":"Allow hello application tooaccess CloudSense on your behalf.","userConsentDisplayName":"Access CloudSense","value":"user_impersonation"}],"passwordCredentials":[],"preferredTokenSigningKeyThumbprint":null,"publisherName":"vipswapper"quot;,"replyUrls":["http://www.vipswapper.com/cloudsense","http://www.vipswapper.com","http://vipswapper.com","http://vipswapper.azurewebsites.net","http://localhost:62080"],"samlMetadataUrl":null,"servicePrincipalNames":["http://www.vipswapper.com/cloudsense","a0448380-c346-4f9f-b897-c18733de9394"],"tags":["WindowsAzureActiveDirectoryIntegratedApp"]}]}

### <a name="get-azure-rbac-role-identifier"></a>Ottenere l'identificatore del ruolo Controllo degli accessi in base al ruolo di Azure
tooassign hello appropriato RBAC ruolo tooyour entità servizio, è necessario determinare l'identificatore hello del ruolo di Azure RBAC hello.

Hello RBAC ruolo più appropriato per l'applicazione:

* Se l'applicazione esegue solo il monitoraggio sottoscrizione hello, senza apportare alcuna modifica, richiede solo le autorizzazioni di lettura sottoscrizione hello. Assegnare hello **lettore** ruolo.
* Se l'applicazione gestisce la sottoscrizione di Azure hello, creazione/modifica/eliminazione di entità, viene richiesta una delle autorizzazioni di collaboratore hello.
  * toomanage un particolare tipo di risorsa, assegnare ruoli di collaboratore specifici delle risorse hello (collaboratore alla macchina virtuale, collaboratore di rete virtuale, collaboratore di Account di archiviazione e così via)
  * toomanage qualsiasi tipo di risorsa, assegnare hello **collaboratore** ruolo.

assegnazione di ruolo Hello per l'applicazione è visibile toousers, quindi selezionare hello con privilegi minimi richiesti.

Chiamare hello [definizione del ruolo Gestione risorse API](https://docs.microsoft.com/rest/api/authorization/roledefinitions) toolist tutti i ruoli di Azure RBAC e ricerca quindi scorrere hello toofind di hello risultato desiderato di definizione del ruolo in base al nome.

Hello [GetRoleId](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L246) metodo hello app di esempio ASP.net MVC implementa questa chiamata.

esempio Hello richiesta di esempio viene illustrato come identificatore del ruolo Azure RBAC tooget. 09cbd307-aa71-4aca-b346-5f253e6e3ebb è l'id di hello di hello sottoscrizione.

    GET https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV*****fY2lGc5

risposta Hello è nel seguente formato hello:

    HTTP/1.1 200 OK

    {"value":[{"properties":{"roleName":"API Management Service Contributor","type":"BuiltInRole","description":"Lets you manage API Management services, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.ApiManagement/Services/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/312a565d-c81f-4fd8-895a-4e21e48d571c","type":"Microsoft.Authorization/roleDefinitions","name":"312a565d-c81f-4fd8-895a-4e21e48d571c"},{"properties":{"roleName":"Application Insights Component Contributor","type":"BuiltInRole","description":"Lets you manage Application Insights components, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.Insights/components/*","Microsoft.Insights/webtests/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/ae349356-3a1b-4a5e-921d-050484c6347e","type":"Microsoft.Authorization/roleDefinitions","name":"ae349356-3a1b-4a5e-921d-050484c6347e"}]}

Non è necessario toocall questa API in maniera continuativa. Dopo aver stabilito hello GUID conosciuto hello definizione del ruolo, è possibile creare id di definizione di ruolo hello come:

    /subscriptions/{subscription_id}/providers/Microsoft.Authorization/roleDefinitions/{well-known-role-guid}

Di seguito sono hello GUID noto dei ruoli predefiniti comunemente utilizzati:

| Ruolo | Guid |
| --- | --- |
| Lettore |acdd72a7-3385-48ef-bd42-f606fba81ae7 |
| Collaboratore |b24988ac-6180-42a0-ab88-20f7382dd24c |
| Collaboratore macchine virtuali |d73bb868-a0df-4d4d-bd69-98a00b01fccb |
| Collaboratore reti virtuali |b34d265f-36f7-4a0d-a4d4-e158ca92e90f |
| Collaboratore account di archiviazione |86e8f5dc-a6e9-4c67-9d15-de283e8eac25 |
| Collaboratore siti Web |de139f84-1756-47ae-9be6-808fbbe84772 |
| Collaboratore piani Web |2cc479cb-7b4d-49a8-b449-8c00fd0f0a4b |
| Collaboratore SQL Server |6d8ee4ec-f05a-4a1d-8b00-a9b17e38b437 |
| Collaboratore database SQL |9b7fa17d-e63e-47b0-bb0a-15c516ac86ec |

### <a name="assign-rbac-role-tooapplication"></a>Assegnare RBAC ruolo tooapplication
È tutto ciò che occorre tooassign hello appropriato RBAC ruolo tooyour dell'entità servizio utilizzando hello [Gestione risorse di creare l'assegnazione di ruolo](https://docs.microsoft.com/rest/api/authorization/roleassignments) API.

Hello [GrantRoleToServicePrincipalOnSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L170) metodo hello app di esempio ASP.net MVC implementa questa chiamata.

Un esempio richiesta tooassign RBAC ruolo tooapplication:

    PUT https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/microsoft.authorization/roleassignments/4f87261d-2816-465d-8311-70a27558df4c?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiL*****FlwO1mM7Cw6JWtfY2lGc5
    Content-Type: application/json
    Content-Length: 230

    {"properties": {"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2"}}

Nella richiesta di hello, viene utilizzato hello seguenti valori:

| Guid | Descrizione |
| --- | --- |
| 09cbd307-aa71-4aca-b346-5f253e6e3ebb |id di Hello di hello sottoscrizione |
| c3097b31-7309-4c59-b4e3-770f8406bad2 |id di oggetto Hello dell'entità servizio hello di un'applicazione hello |
| acdd72a7-3385-48ef-bd42-f606fba81ae7 |id di Hello del ruolo di lettore hello |
| 4f87261d-2816-465d-8311-70a27558df4c |un nuovo guid creato per la nuova assegnazione di ruolo hello |

risposta Hello è nel seguente formato hello:

    HTTP/1.1 201 Created

    {"properties":{"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2","scope":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb"},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleAssignments/4f87261d-2816-465d-8311-70a27558df4c","type":"Microsoft.Authorization/roleAssignments","name":"4f87261d-2816-465d-8311-70a27558df4c"}

### <a name="get-app-only-access-token-for-azure-resource-manager"></a>Ottenere il token di accesso solo app per Azure Resource Manager
toovalidate app ha accesso hello desiderato nella sottoscrizione hello, eseguire un'attività di test su sottoscrizione hello tramite un token di autorizzazione solo app.

tooget un token di accesso solo app, seguire le istruzioni nella sezione [ottenere token di accesso solo app per l'API di Azure AD Graph](#app-azure-ad-graph), con un valore diverso per il parametro risorsa hello:

    https://management.core.windows.net/

Hello [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) metodo dell'applicazione di esempio ASP.NET MVC Ottiene un accesso solo app token per l'utilizzo di Azure Resource Manager hello hello Active Directory Authentication Library per .net.

#### <a name="get-applications-permissions-on-subscription"></a>Ottenere le autorizzazioni dell'applicazione per la sottoscrizione
accesso in una sottoscrizione di Azure di toocheck che l'applicazione ha hello desiderato, è inoltre possibile chiamare hello [le autorizzazioni di gestione risorse](https://docs.microsoft.com/rest/api/authorization/permissions) API. Questo approccio è simile toohow determinare se l'utente hello dispone dei diritti di gestione dell'accesso per la sottoscrizione di hello. Tuttavia, questa volta, chiamare l'API di autorizzazioni di hello con token di accesso solo per app hello ottenuto nel passaggio precedente hello.

Hello [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) metodo hello app di esempio ASP.NET MVC implementa questa chiamata.

## <a name="manage-connected-subscriptions"></a>Gestire le sottoscrizioni connesse
Quando ruolo RBAC appropriato hello viene assegnata l'entità servizio dell'applicazione tooyour sottoscrizione hello, l'applicazione può mantenere il monitoraggio/gestione tramite i token di accesso solo app per Gestione risorse di Azure.

Se un proprietario della sottoscrizione Rimuove l'assegnazione di ruolo dell'applicazione utilizzando portale classico hello o strumenti da riga di comando, l'applicazione è tooaccess non è più in grado di sottoscrizione. In tal caso, si deve notificare utente hello che connessione hello sottoscrizione hello è stata interrotta da un'applicazione hello esterno e associarvi un'opzione troppo "Ripristina" connessione hello. "Ripristina" sarebbe semplicemente creare nuovamente l'assegnazione di ruolo hello che è stato eliminato non in linea.

Esattamente come un'applicazione hello utente tooconnect sottoscrizioni tooyour è stato abilitato, è necessario consentire le sottoscrizioni di hello utente toodisconnect troppo. Da un punto di vista della gestione di accesso, disconnessione significa rimuovere l'assegnazione di ruolo hello contenente entità servizio dell'applicazione hello nella sottoscrizione hello. Facoltativamente, dello stato in un'applicazione hello per sottoscrizione hello potrebbe essere rimossi troppo.
Solo gli utenti con autorizzazione di accesso gestione per la sottoscrizione hello sono in grado di toodisconnect sottoscrizione di hello.

Hello [RevokeRoleFromServicePrincipalOnSubscription metodo](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L200) di ASP.net MVC hello app di esempio implementa questa chiamata.

Gli utenti ora possono connettere e gestire facilmente le sottoscrizioni di Azure con l'applicazione.
