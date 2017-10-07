---
title: 'Azure Active B2C di Directory: Hello di utilizzare API Graph | Documenti Microsoft'
description: "Come toocall hello API Graph per un tenant B2C tramite un processo di hello tooautomate identità dell'applicazione."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f9904516-d9f7-43b1-ae4f-e4d9eb1c67a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: parakhj
ms.openlocfilehash: a17cdc4adf57dbf22592d99ef8ecde41652763fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-use-hello-graph-api"></a>Azure Active Directory B2C: Utilizzare hello API Graph
Tenant di Azure Active Directory (Azure AD) B2C tendono toobe molto grandi. Ciò significa che molte attività comuni di gestione tenant necessario toobe eseguita a livello di codice. ad esempio la gestione degli utenti. Potrebbe essere necessario toomigrate un tenant B2C tooa di archivio utente esistente. È possibile desidera toohost registrazione dell'utente nella propria pagina e creare gli account utente nella directory di Azure Active Directory B2C background hello. Questi tipi di attività richiedono hello possibilità toocreate, lettura, aggiornamento ed eliminare account utente. Queste attività eseguibili tramite l'API di Azure AD Graph hello.

Per i tenant B2C, esistono due modalità principali della comunicazione con l'API Graph hello.

* Per le attività interattive, Esegui una volta, deve agire come un account di amministratore nel tenant B2C hello quando si eseguono attività hello. Questa modalità richiede toosign un amministratore con le credenziali prima che gli amministratori possono eseguire qualsiasi toohello chiamate API Graph.
* Per attività automatizzata, continua, utilizzare un tipo di account di servizio fornito con attività di gestione tooperform hello dei privilegi necessari. In Azure AD, è possibile farlo registrando un'applicazione e l'autenticazione tooAzure Active Directory. Questa operazione viene eseguita utilizzando un **ID applicazione** che utilizza hello [concessione di credenziali client OAuth 2.0](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api). In questo caso, un'applicazione hello funge da se stesso, non come un utente, hello toocall API Graph.

In questo articolo verrà trattato come tooperform hello caso d'uso automatizzata. toodemonstrate, verrà creato un .NET 4.5 `B2CGraphClient` che esegue utente creare, leggere, aggiornare e l'eliminazione (CRUD). client Hello avrà un'interfaccia di Windows della riga di comando (CLI) che consente di tooinvoke diversi metodi. Tuttavia, hello codice toobehave in modo automatico non interattivo.

## <a name="get-an-azure-ad-b2c-tenant"></a>Ottenere un tenant di Azure AD B2C
Prima di poter creare applicazioni o utenti, o interagire con Azure AD a, è necessario un account di amministratore globale nel tenant di hello e di un tenant di Azure Active Directory B2C. Se non è già disponibile un tenant vedere l' [introduzione ad Azure AD B2C](active-directory-b2c-get-started.md).

## <a name="register-your-application-in-your-tenant"></a>Registrare l'applicazione nel tenant
Dopo aver creato un tenant B2C, è necessario tooregister l'applicazione tramite hello [portale Azure](https://portal.azure.com).

> [!IMPORTANT]
> API di Graph toouse hello con il tenant B2C, sarà necessario tooregister un'applicazione dedicata utilizzando hello generico *registrazioni di App* pannello nel portale di Azure, hello **non** Azure Active Directory B2C  *Applicazioni* blade. Non è possibile riutilizzare hello già esistenti B2C applicazioni registrate in Azure Active Directory B2C hello *applicazioni* blade.

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Scegliere il tenant di Azure Active Directory B2C, selezionare l'account in hello angolo superiore destro della pagina hello.
3. Nel riquadro di navigazione a sinistra di hello, scegliere **più servizi**, fare clic su **registrazioni di App**, fare clic su **Aggiungi**.
4. Seguire le istruzioni di hello e creare una nuova applicazione. 
    1. Selezionare **App Web / API** come tipo di applicazione hello.    
    2. Fornire **qualsiasi URI di reindirizzamento** (ad esempio https://B2CGraphAPI) in quanto non è rilevante per questo esempio.  
5. Hello applicazione verranno ora visualizzati nell'elenco di hello delle applicazioni, fare clic su di esso hello tooobtain **ID applicazione** (noto anche come ID Client). Copiarlo in quanto sarà necessario in una sezione successiva.
6. Nel pannello impostazioni hello, fare clic su **chiavi** e aggiungere una nuova chiave (noto anche come segreto client). Copiare anche questa per usarla in una sezione successiva.

## <a name="configure-create-read-and-update-permissions-for-your-application"></a>Configurare le autorizzazioni creare, leggere e aggiornare per l'applicazione
È possibile procedere tooconfigure tooget l'applicazione che Hello tutti necessarie autorizzazioni toocreate, leggere, aggiornare ed eliminare gli utenti.

1. Continuare a hello pannello registrazioni di App del portale di Azure, selezionare l'applicazione.
2. Nel pannello impostazioni hello, fare clic su **delle autorizzazioni necessarie**.
3. Nel Pannello di hello delle autorizzazioni necessarie, fare clic su **Windows Azure Active Directory**.
4. Nel Pannello di hello Abilita l'accesso, selezionare hello **lettura e scrittura dati directory** autorizzazioni **autorizzazioni applicazione** e fare clic su **salvare**.
5. Infine, nel Pannello di hello delle autorizzazioni necessarie, fare clic su hello **concedere autorizzazioni** pulsante.

Ora è un'applicazione con autorizzazioni toocreate, lettura e aggiornamento gli utenti dal tenant B2C.

## <a name="configure-delete-permissions-for-your-application"></a>Configurare le autorizzazioni di eliminazione per l'applicazione
Attualmente, hello *lettura e scrittura dati directory* autorizzazione **non** includono hello possibilità toodo le eliminazioni ad esempio l'eliminazione di utenti. Se si desidera toogive toodelete utenti applicazione hello possibilità, è necessario toodo questi passaggi aggiuntivi che comportano PowerShell, in caso contrario, è possibile ignorare toohello nella sezione successiva.

Innanzitutto, scaricare e installare hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152). Quindi scaricare e installare hello [modulo di Azure Active Directory a 64 bit per Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).

Dopo aver installato il modulo di PowerShell hello, aprire PowerShell e connettersi tooyour B2C tenant. Dopo aver eseguito `Get-Credential`, verrà richiesto di un nome utente e password, immettere il nome utente hello e una password dell'account di amministratore tenant di B2C.

> [!IMPORTANT]
> È necessario l'account di amministratore di tenant toouse un B2C è **locale** toohello B2C tenant. Questi account hanno un aspetto simile a questo: myusername@myb2ctenant.onmicrosoft.com.

```powershell
Connect-MsolService
```

Ora si userà hello **ID applicazione** nello script hello sotto tooassign hello applicazione hello account amministratore ruolo utente che ne consentono agli utenti di toodelete. Questi ruoli sono identificatori noti, pertanto è sufficiente toodo è di input del **ID applicazione** in script hello riportato di seguito.

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

A questo punto l'applicazione ha anche le autorizzazioni toodelete utenti dal tenant B2C.

## <a name="download-configure-and-build-hello-sample-code"></a>Scaricare, configurare e compilare il codice di esempio hello
Innanzitutto, scaricare il codice di esempio hello e l'esecuzione. Esaminare quindi il codice.  È possibile [scaricare codice di esempio hello come file con estensione zip](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip). È anche possibile clonarlo nella directory desiderata:

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

Aprire hello `B2CGraphClient\B2CGraphClient.sln` soluzione di Visual Studio in Visual Studio. In hello `B2CGraphClient` progetto, il file aperto hello `App.config`. Sostituire le impostazioni dell'app tre hello con valori personalizzati:

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{hello ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{hello Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

Successivamente, fare clic su hello `B2CGraphClient` : esempio hello soluzione e ricompilare. Se l'operazione riesce, sarà disponibile un file eseguibile `B2C.exe` in `B2CGraphClient\bin\Debug`.

## <a name="build-user-crud-operations-by-using-hello-graph-api"></a>Compilare le operazioni CRUD utente tramite l'API Graph hello
hello toouse B2CGraphClient, aprire un `cmd` Windows comando Chiedi conferma prima di modificare la directory toohello `Debug` directory. Eseguire quindi hello `B2C Help` comando.

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

Verrà visualizzata una breve descrizione di ogni comando. Ogni volta che si richiama uno di questi comandi, `B2CGraphClient` rende toohello una richiesta API di Azure AD Graph.

### <a name="get-an-access-token"></a>Ottenere un token di accesso
Qualsiasi toohello richiesta API Graph richiede un token di accesso per l'autenticazione. `B2CGraphClient`Usa hello open source Active Directory Authentication Library (ADAL) toohelp acquisire i token di accesso. ADAL semplifica l'acquisizione del token fornendo un'API semplice e avendo cura di alcuni dettagli importanti, come la memorizzazione nella cache dei token di accesso. Token ADAL tooget toouse, non è tuttavia. È anche possibile ottenere i token creando richieste HTTP.

> [!NOTE]
> In questo esempio di codice Usa ADAL v2 in ordine toocommunicate con hello API Graph.  Nei token di accesso tooget ordine, che può essere usato con hello API Azure AD Graph, è necessario usare ADAL versione 2 o 3.
> 
> 

Quando `B2CGraphClient` viene eseguita, crea un'istanza di hello `B2CGraphClient` classe. costruttore Hello per questa classe imposta lo scaffolding di un'autenticazione ADAL:

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // hello client_id, client_secret, and tenant are provided in Program.cs, which pulls hello values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // hello AuthenticationContext is ADAL's primary class, in which you indicate hello tenant toouse.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // hello ClientCredential is where you pass in your client_id and client_secret, which are
    // provided tooAzure AD in order tooreceive an access_token by using hello app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

Si userà hello `B2C Get-User` comando come esempio. Quando `B2C Get-User` viene richiamato senza alcun input aggiuntivi, hello CLI chiamate hello `B2CGraphClient.GetAllUsers(...)` metodo. Questo metodo chiama `B2CGraphClient.SendGraphGetRequest(...)`, che invia un toohello di richiesta HTTP GET API Graph. Prima di `B2CGraphClient.SendGraphGetRequest(...)` invia hello richiesta GET, innanzitutto Ottiene un token di accesso tramite ADAL:

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL tooacquire a token by using hello app's identity (hello credential)
    // hello first parameter is hello resource we want an access_token for; in this case, hello Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

È possibile ottenere un accesso token per hello API Graph dal chiamante hello ADAL `AuthenticationContext.AcquireToken(...)` metodo. ADAL restituisce quindi un `access_token` che rappresenta l'identità dell'applicazione hello.

### <a name="read-users"></a>Leggere gli utenti
Quando si desidera tooget un elenco di utenti o ottiene un utente specifico da hello API Graph, è possibile inviare un HTTP `GET` richiesta toohello `/users` endpoint. Una richiesta per tutti gli utenti di hello in un tenant è simile al seguente:

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

toosee questa richiesta, eseguire:

 ```
 > B2C Get-User
 ```

Esistono due aspetti importanti toonote:

* Hello token di accesso acquisito tramite la libreria ADAL viene aggiunto toohello `Authorization` intestazione usando hello `Bearer` schema.
* Per i tenant B2C, è necessario utilizzare il parametro di query hello `api-version=1.6`.

Entrambi questi dettagli vengono gestiti in hello `B2CGraphClient.SendGraphGetRequest(...)` metodo:

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure toouse hello 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append hello access token for hello Graph API toohello Authorization header of hello request by using hello Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a>Creare account utente consumer
Quando si creano l'account utente nel tenant di B2C, è possibile inviare un HTTP `POST` richiesta toohello `/users` endpoint:

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required toocreate consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier hello user uses toosign in toohello account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set too'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying toohello end user
    "mailNickname": "joec",                        // an email alias for hello user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set toofalse
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

La maggior parte di queste proprietà in questa richiesta è necessario toocreate degli utenti. toolearn più, fare clic su [qui](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser). Si noti che hello `//` commenti sono stati inclusi a scopo illustrativo. Non includerli in una richiesta effettiva.

richiesta di hello toosee, eseguire uno dei seguenti comandi hello:

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

Hello `Create-User` comando accetta un file con estensione JSON come parametro di input. Il file include una rappresentazione JSON di un oggetto utente. Sono disponibili due file con estensione JSON di esempio nel codice di esempio hello: `usertemplate-email.json` e `usertemplate-username.json`. È possibile modificare questi file toosuit le proprie esigenze. Inoltre toohello richiesto campi sopra indicati, sono inclusi numerosi campi facoltativi che è possibile utilizzare questi file. Sono disponibili informazioni dettagliate su campi facoltativi hello in hello [riferimento all'entità di Azure AD Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).

È possibile visualizzare la richiesta POST hello viene costruito in `B2CGraphClient.SendGraphPostRequest(...)`.

* Collega un toohello token di accesso `Authorization` intestazione della richiesta di hello.
* Imposta `api-version=1.6`.
* Include l'oggetto utente di hello JSON nel corpo di hello di hello richiesta.

> [!NOTE]
> Se hello account che si desidera toomigrate da un archivio utente esistente è la complessità della password inferiore rispetto a hello [forza una password complessa applicata da Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), è possibile disabilitare il requisito di una password complessa hello utilizzando hello `DisableStrongPassword`valore hello `passwordPolicies` proprietà. Ad esempio, è possibile modificare hello creare una richiesta utente fornita in precedenza, come indicato di seguito: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.
> 
> 

### <a name="update-consumer-user-accounts"></a>Aggiornare gli account utente consumer
Quando si aggiornano gli oggetti utente, il processo di hello è simile toohello uno che si utilizzano gli oggetti utente toocreate. Ma questo processo Usa hello HTTP `PATCH` metodo:

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only hello user's displayName
}
```

Provare a un utente tooupdate aggiornando i file JSON con i nuovi dati. È quindi possibile utilizzare `B2CGraphClient` toorun uno di questi comandi:

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

Controllare hello `B2CGraphClient.SendGraphPatchRequest(...)` metodo per informazioni dettagliate su come toosend questa richiesta.

### <a name="search-users"></a>Cercare gli utenti
È possibile cercare gli utenti nel tenant di B2C in due modi: Uno, usando l'ID oggetto dell'utente hello o due, utilizzare l'identificatore di accesso dell'utente hello (ad esempio, hello `signInNames` proprietà).

Eseguire uno dei seguenti comandi toosearch per un utente specifico hello:

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

Ecco alcuni esempi:

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a>Eliminare gli utenti
il processo di Hello per l'eliminazione di un utente è semplice. Hello utilizzare HTTP `DELETE` (metodo) e creare URL hello con hello correggere l'ID di oggetto:

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

toosee ad esempio, immettere questo comando e visualizzazione hello richiesta di eliminazione che viene stampato toohello console:

```
> B2C Delete-User <object-id-of-user>
```

Controllare hello `B2CGraphClient.SendGraphDeleteRequest(...)` metodo per informazioni dettagliate su come toosend questa richiesta.

È possibile eseguire molte altre operazioni con Azure AD Graph API hello in Gestione toouser aggiunta. Le [informazioni di riferimento sull'API Graph di Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) illustrano i dettagli di ogni azione, insieme a richieste di esempio.

## <a name="use-custom-attributes"></a>Usare gli attributi personalizzati
La maggior parte delle applicazioni consumer necessario toostore alcuni tipi di informazioni sul profilo utente personalizzato. A tale scopo, è un attributo personalizzato nel tenant di B2C toodefine. È quindi possibile trattare hello tale attributo allo stesso modo, si considera di qualsiasi altra proprietà in un oggetto utente. È possibile aggiornare l'attributo hello, attributo hello di eliminazione, query dall'attributo hello, inviare attributo hello come attestazione nel token di accesso e altro ancora.

toodefine un attributo personalizzato nel tenant di B2C, vedere hello [riferimento di attributo personalizzato B2C](active-directory-b2c-reference-custom-attr.md).

È possibile visualizzare gli attributi personalizzati di hello definiti nel tenant di B2C utilizzando `B2CGraphClient`:

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

output di Hello di queste funzioni rivela dettagli hello di ogni attributo personalizzato, ad esempio:

```JSON
{
      "odata.type": "Microsoft.DirectoryServices.ExtensionProperty",
      "objectType": "ExtensionProperty",
      "objectId": "cec6391b-204d-42fe-8f7c-89c2b1964fca",
      "deletionTimestamp": null,
      "appDisplayName": "",
      "name": "extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number",
      "dataType": "Integer",
      "isSyncedFromOnPremises": false,
      "targetObjects": [
        "User"
      ]
}
```

È possibile utilizzare hello nome completo, ad esempio `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, come una proprietà per gli oggetti utente.  Aggiornare il file con estensione JSON con una nuova proprietà hello e un valore per proprietà hello e quindi eseguire:

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

Se si usa `B2CGraphClient`, si ha a disposizione un'applicazione di servizio che può gestire gli utenti del tenant di B2C a livello di codice. `B2CGraphClient`Usa il proprio toohello tooauthenticate di identità applicazione API Azure AD Graph. Acquisisce anche i token usando un segreto client. Quando si incorpora questa funzionalità nell'applicazione, tenere presenti alcuni punti chiave per le applicazioni B2C:

* È necessario toogrant hello applicazione hello delle autorizzazioni appropriate nel tenant di hello.
* Per il momento, è necessario i token di accesso tooget toouse ADAL (non MSAL). È anche possibile inviare direttamente messaggi di protocollo, senza usare una raccolta.
* Quando si chiama l'API Graph hello, utilizzare `api-version=1.6`.
* Quando si creano e aggiornano utenti consumer, sono necessarie alcune proprietà, come illustrato in precedenza.

Se si hanno domande o richieste di azioni che si desidera tooperform tramite API Graph hello in tenant B2C lascia un commento in questo articolo o segnalare un problema nel repository di esempio hello GitHub codice.

