### <span data-ttu-id="f8895-101"><a name="server-auth"></a>Procedura: Eseguire l'autenticazione con un provider (flusso server)</span><span class="sxs-lookup"><span data-stu-id="f8895-101"><a name="server-auth"></a>How to: Authenticate with a provider (Server Flow)</span></span>
<span data-ttu-id="f8895-102">App per dispositivi mobili toohave gestire il processo di autenticazione hello nell'app, è necessario registrare l'app con il provider di identità.</span><span class="sxs-lookup"><span data-stu-id="f8895-102">toohave Mobile Apps manage hello authentication process in your app, you must register your app with your identity provider.</span></span> <span data-ttu-id="f8895-103">Quindi il servizio App di Azure, è necessario tooconfigure hello ID dell'applicazione e il segreto fornite dal provider.</span><span class="sxs-lookup"><span data-stu-id="f8895-103">Then in your Azure App Service, you need tooconfigure hello application ID and secret provided by your provider.</span></span>
<span data-ttu-id="f8895-104">Per ulteriori informazioni, vedere l'esercitazione hello [Aggiungi autenticazione tooyour app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="f8895-104">For more information, see hello tutorial [Add authentication tooyour app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span></span>

<span data-ttu-id="f8895-105">Dopo aver registrato il provider di identità, chiamare hello `.login()` metodo con nome hello del provider.</span><span class="sxs-lookup"><span data-stu-id="f8895-105">Once you have registered your identity provider, call hello `.login()` method with hello name of your provider.</span></span> <span data-ttu-id="f8895-106">Ad esempio, toologin con Facebook utilizzare hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="f8895-106">For example, toologin with Facebook use hello following code:</span></span>

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

<span data-ttu-id="f8895-107">i valori validi per il provider di hello Hello sono 'aad', 'facebook', 'google', 'microsoftaccount' e 'twitter'.</span><span class="sxs-lookup"><span data-stu-id="f8895-107">hello valid values for hello provider are 'aad', 'facebook', 'google', 'microsoftaccount', and 'twitter'.</span></span>

> [!NOTE]
> <span data-ttu-id="f8895-108">L'autenticazione di Google attualmente non funziona tramite Flusso server.</span><span class="sxs-lookup"><span data-stu-id="f8895-108">Google Authentication does not currently work via Server Flow.</span></span>  <span data-ttu-id="f8895-109">tooauthenticate con Google, è necessario utilizzare un [metodo flusso client](#client-auth).</span><span class="sxs-lookup"><span data-stu-id="f8895-109">tooauthenticate with Google, you must use a [client-flow method](#client-auth).</span></span>

<span data-ttu-id="f8895-110">In questo caso, il servizio App di Azure gestisce il flusso di autenticazione OAuth 2.0 hello.</span><span class="sxs-lookup"><span data-stu-id="f8895-110">In this case, Azure App Service manages hello OAuth 2.0 authentication flow.</span></span>  <span data-ttu-id="f8895-111">Visualizza la pagina di accesso hello del provider selezionato hello e genera un token di autenticazione del servizio App dopo aver eseguito correttamente l'accesso con provider di identità hello.</span><span class="sxs-lookup"><span data-stu-id="f8895-111">It displays hello login page of hello selected provider and generates an App Service authentication token after successful login with hello identity provider.</span></span> <span data-ttu-id="f8895-112">funzione di accesso Hello, al termine, restituisce un oggetto JSON che espone sia l'ID utente hello e App servizio token di autenticazione nei campi di ID utente e authenticationToken hello, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="f8895-112">hello login function, when complete, returns a JSON object that exposes both hello user ID and App Service authentication token in hello userId and authenticationToken fields, respectively.</span></span> <span data-ttu-id="f8895-113">È possibile memorizzare questo token nella cache e riutilizzarlo fino alla scadenza.</span><span class="sxs-lookup"><span data-stu-id="f8895-113">This token can be cached and reused until it expires.</span></span>

###<span data-ttu-id="f8895-114"><a name="client-auth"></a>Procedura: Eseguire l'autenticazione con un provider (flusso client)</span><span class="sxs-lookup"><span data-stu-id="f8895-114"><a name="client-auth"></a>How to: Authenticate with a provider (Client Flow)</span></span>

<span data-ttu-id="f8895-115">L'app può anche in modo indipendente, contattare il provider di identità hello e fornire hello restituiti token tooyour servizio App per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="f8895-115">Your app can also independently contact hello identity provider and then provide hello returned token tooyour App Service for authentication.</span></span> <span data-ttu-id="f8895-116">Questo flusso client consente un'esperienza di accesso singola per gli utenti o i dati utente aggiuntivi tooretrieve dal provider di identità hello tooprovide.</span><span class="sxs-lookup"><span data-stu-id="f8895-116">This client flow enables you tooprovide a single sign-in experience for users or tooretrieve additional user data from hello identity provider.</span></span>

#### <a name="social-authentication-basic-example"></a><span data-ttu-id="f8895-117">Esempio di base di autenticazione tramite social network</span><span class="sxs-lookup"><span data-stu-id="f8895-117">Social Authentication basic example</span></span>

<span data-ttu-id="f8895-118">Questo esempio utilizza il client SDK di Facebook per l'autenticazione:</span><span class="sxs-lookup"><span data-stu-id="f8895-118">This example uses Facebook client SDK for authentication:</span></span>

```
client.login(
     "facebook",
     {"access_token": token})
.done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});

```
<span data-ttu-id="f8895-119">Questo esempio si presuppone che token hello fornito dal provider rispettivi hello SDK viene archiviato nella variabile token hello.</span><span class="sxs-lookup"><span data-stu-id="f8895-119">This example assumes that hello token provided by hello respective provider SDK is stored in hello token variable.</span></span>

#### <a name="microsoft-account-example"></a><span data-ttu-id="f8895-120">Esempio di account Microsoft</span><span class="sxs-lookup"><span data-stu-id="f8895-120">Microsoft Account example</span></span>

<span data-ttu-id="f8895-121">Hello seguente viene illustrato come utilizzare hello Live SDK, che supporta single sign-on per applicazioni Windows Store con Account Microsoft:</span><span class="sxs-lookup"><span data-stu-id="f8895-121">hello following example uses hello Live SDK, which supports single-sign-on for Windows Store apps by using Microsoft Account:</span></span>

```
WL.login({ scope: "wl.basic"}).then(function (result) {
      client.login(
            "microsoftaccount",
            {"authenticationToken": result.session.authentication_token})
      .done(function(results){
            alert("You are now logged in as: " + results.userId);
      },
      function(error){
            alert("Error: " + err);
      });
});

```

<span data-ttu-id="f8895-122">In questo esempio Ottiene un token da Live Connect, ovvero tooyour fornito servizio App chiamando la funzione di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="f8895-122">This example gets a token from Live Connect, which is supplied tooyour App Service by calling hello login function.</span></span>

###<span data-ttu-id="f8895-123"><a name="auth-getinfo"></a>Procedura: ottenere informazioni sull'utente autenticato hello</span><span class="sxs-lookup"><span data-stu-id="f8895-123"><a name="auth-getinfo"></a>How to: Obtain information about hello authenticated user</span></span>

<span data-ttu-id="f8895-124">informazioni di autenticazione Hello possono essere recuperate da hello `/.auth/me` endpoint utilizzando HTTP chiamare con qualsiasi libreria AJAX.</span><span class="sxs-lookup"><span data-stu-id="f8895-124">hello authentication information can be retrieved from hello `/.auth/me` endpoint using an HTTP call with any AJAX library.</span></span>  <span data-ttu-id="f8895-125">Assicurarsi di impostare hello `X-ZUMO-AUTH` token di autenticazione tooyour intestazione.</span><span class="sxs-lookup"><span data-stu-id="f8895-125">Ensure you set hello `X-ZUMO-AUTH` header tooyour authentication token.</span></span>  <span data-ttu-id="f8895-126">Hello token di autenticazione viene archiviato `client.currentUser.mobileServiceAuthenticationToken`.</span><span class="sxs-lookup"><span data-stu-id="f8895-126">hello authentication token is stored in `client.currentUser.mobileServiceAuthenticationToken`.</span></span>  <span data-ttu-id="f8895-127">Ad esempio, toouse hello recupero API:</span><span class="sxs-lookup"><span data-stu-id="f8895-127">For example, toouse hello fetch API:</span></span>

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // hello user object contains hello claims for hello authenticated user
    });
```

<span data-ttu-id="f8895-128">L'operazione di recupero è disponibile come [pacchetto npm](https://www.npmjs.com/package/whatwg-fetch) oppure può essere scaricato tramite il browser da [CDNJS](https://cdnjs.com/libraries/fetch).</span><span class="sxs-lookup"><span data-stu-id="f8895-128">Fetch is available as [an npm package](https://www.npmjs.com/package/whatwg-fetch) or for browser download from [CDNJS](https://cdnjs.com/libraries/fetch).</span></span> <span data-ttu-id="f8895-129">È anche possibile usare jQuery o informazioni di un'altra API AJAX toofetch hello.</span><span class="sxs-lookup"><span data-stu-id="f8895-129">You could also use jQuery or another AJAX API toofetch hello information.</span></span>  <span data-ttu-id="f8895-130">I dati saranno ricevuti come oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="f8895-130">Data is received as a JSON object.</span></span>
