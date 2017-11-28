### <span data-ttu-id="87a42-101"><a name="server-auth"></a>Procedura: Eseguire l'autenticazione con un provider (flusso server)</span><span class="sxs-lookup"><span data-stu-id="87a42-101"><a name="server-auth"></a>How to: Authenticate with a provider (Server Flow)</span></span>
<span data-ttu-id="87a42-102">Per consentire alle app per dispositivi mobili di gestire il processo di autenticazione nella propria app, è necessario effettuare la registrazione dell'app con il provider di identità.</span><span class="sxs-lookup"><span data-stu-id="87a42-102">To have Mobile Apps manage the authentication process in your app, you must register your app with your identity provider.</span></span> <span data-ttu-id="87a42-103">Nel proprio servizio app di Azure è quindi necessario configurare l'ID e il segreto dell'applicazione forniti dal provider.</span><span class="sxs-lookup"><span data-stu-id="87a42-103">Then in your Azure App Service, you need to configure the application ID and secret provided by your provider.</span></span>
<span data-ttu-id="87a42-104">Per altre informazioni, vedere l'esercitazione [Aggiungere l'autenticazione all'app di Servizi mobili](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="87a42-104">For more information, see the tutorial [Add authentication to your app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span></span>

<span data-ttu-id="87a42-105">Dopo aver effettuato la registrazione del provider di identità, chiamare il metodo `.login()` con il nome del provider.</span><span class="sxs-lookup"><span data-stu-id="87a42-105">Once you have registered your identity provider, call the `.login()` method with the name of your provider.</span></span> <span data-ttu-id="87a42-106">Per accedere ad esempio con Facebook, utilizzare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="87a42-106">For example, to login with Facebook use the following code:</span></span>

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

<span data-ttu-id="87a42-107">I valori validi per il provider sono "aad", "facebook", "google", "microsoftaccount" e "twitter".</span><span class="sxs-lookup"><span data-stu-id="87a42-107">The valid values for the provider are 'aad', 'facebook', 'google', 'microsoftaccount', and 'twitter'.</span></span>

> [!NOTE]
> <span data-ttu-id="87a42-108">L'autenticazione di Google attualmente non funziona tramite Flusso server.</span><span class="sxs-lookup"><span data-stu-id="87a42-108">Google Authentication does not currently work via Server Flow.</span></span>  <span data-ttu-id="87a42-109">Per eseguire l'autenticazione con Google, è necessario usare un [metodo di flusso client](#client-auth).</span><span class="sxs-lookup"><span data-stu-id="87a42-109">To authenticate with Google, you must use a [client-flow method](#client-auth).</span></span>

<span data-ttu-id="87a42-110">In questo caso, il Servizio app di Azure gestisce il flusso di autenticazione OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="87a42-110">In this case, Azure App Service manages the OAuth 2.0 authentication flow.</span></span>  <span data-ttu-id="87a42-111">Viene visualizzata la pagina di accesso al provider selezionato e viene generato un token di autenticazione del Servizio app dopo aver eseguito correttamente l'accesso con il provider di identità.</span><span class="sxs-lookup"><span data-stu-id="87a42-111">It displays the login page of the selected provider and generates an App Service authentication token after successful login with the identity provider.</span></span> <span data-ttu-id="87a42-112">La funzione login, una volta completata, restituisce un oggetto JSON che espone l'ID utente e il token di autenticazione del servizio app rispettivamente nei campi userId e authenticationToken.</span><span class="sxs-lookup"><span data-stu-id="87a42-112">The login function, when complete, returns a JSON object that exposes both the user ID and App Service authentication token in the userId and authenticationToken fields, respectively.</span></span> <span data-ttu-id="87a42-113">È possibile memorizzare questo token nella cache e riutilizzarlo fino alla scadenza.</span><span class="sxs-lookup"><span data-stu-id="87a42-113">This token can be cached and reused until it expires.</span></span>

###<span data-ttu-id="87a42-114"><a name="client-auth"></a>Procedura: Eseguire l'autenticazione con un provider (flusso client)</span><span class="sxs-lookup"><span data-stu-id="87a42-114"><a name="client-auth"></a>How to: Authenticate with a provider (Client Flow)</span></span>

<span data-ttu-id="87a42-115">L'app può anche contattare il provider di identità in modo indipendente e quindi fornire il token restituito al servizio app per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="87a42-115">Your app can also independently contact the identity provider and then provide the returned token to your App Service for authentication.</span></span> <span data-ttu-id="87a42-116">Mediante il flusso client è possibile consentire agli utenti di effettuare l'accesso un'unica volta o recuperare dal provider di identità dati utente aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="87a42-116">This client flow enables you to provide a single sign-in experience for users or to retrieve additional user data from the identity provider.</span></span>

#### <a name="social-authentication-basic-example"></a><span data-ttu-id="87a42-117">Esempio di base di autenticazione tramite social network</span><span class="sxs-lookup"><span data-stu-id="87a42-117">Social Authentication basic example</span></span>

<span data-ttu-id="87a42-118">Questo esempio utilizza il client SDK di Facebook per l'autenticazione:</span><span class="sxs-lookup"><span data-stu-id="87a42-118">This example uses Facebook client SDK for authentication:</span></span>

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
<span data-ttu-id="87a42-119">In questo esempio si presuppone che il token fornito dall'SDK del rispettivo provider sia archiviato nella variabile token.</span><span class="sxs-lookup"><span data-stu-id="87a42-119">This example assumes that the token provided by the respective provider SDK is stored in the token variable.</span></span>

#### <a name="microsoft-account-example"></a><span data-ttu-id="87a42-120">Esempio di account Microsoft</span><span class="sxs-lookup"><span data-stu-id="87a42-120">Microsoft Account example</span></span>

<span data-ttu-id="87a42-121">Nell'esempio seguente viene utilizzato Live SDK, che supporta Single-Sign-On per le app di Windows Store tramite un account Microsoft:</span><span class="sxs-lookup"><span data-stu-id="87a42-121">The following example uses the Live SDK, which supports single-sign-on for Windows Store apps by using Microsoft Account:</span></span>

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

<span data-ttu-id="87a42-122">Questo esempio ottiene un token da Live Connect, che viene fornito al servizio app chiamando la funzione login.</span><span class="sxs-lookup"><span data-stu-id="87a42-122">This example gets a token from Live Connect, which is supplied to your App Service by calling the login function.</span></span>

###<span data-ttu-id="87a42-123"><a name="auth-getinfo"></a>Procedura: Ottenere informazioni relative all'utente autenticato</span><span class="sxs-lookup"><span data-stu-id="87a42-123"><a name="auth-getinfo"></a>How to: Obtain information about the authenticated user</span></span>

<span data-ttu-id="87a42-124">Le informazioni di autenticazione possono essere recuperate dall'endpoint `/.auth/me` usando una chiamata HTTP con una libreria AJAX qualsiasi.</span><span class="sxs-lookup"><span data-stu-id="87a42-124">The authentication information can be retrieved from the `/.auth/me` endpoint using an HTTP call with any AJAX library.</span></span>  <span data-ttu-id="87a42-125">Assicurarsi di impostare l'intestazione `X-ZUMO-AUTH` sul token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="87a42-125">Ensure you set the `X-ZUMO-AUTH` header to your authentication token.</span></span>  <span data-ttu-id="87a42-126">Il token di autenticazione è memorizzato in `client.currentUser.mobileServiceAuthenticationToken`.</span><span class="sxs-lookup"><span data-stu-id="87a42-126">The authentication token is stored in `client.currentUser.mobileServiceAuthenticationToken`.</span></span>  <span data-ttu-id="87a42-127">Ad esempio, per usare l'API fetch:</span><span class="sxs-lookup"><span data-stu-id="87a42-127">For example, to use the fetch API:</span></span>

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // The user object contains the claims for the authenticated user
    });
```

<span data-ttu-id="87a42-128">L'operazione di recupero è disponibile come [pacchetto npm](https://www.npmjs.com/package/whatwg-fetch) oppure può essere scaricato tramite il browser da [CDNJS](https://cdnjs.com/libraries/fetch).</span><span class="sxs-lookup"><span data-stu-id="87a42-128">Fetch is available as [an npm package](https://www.npmjs.com/package/whatwg-fetch) or for browser download from [CDNJS](https://cdnjs.com/libraries/fetch).</span></span> <span data-ttu-id="87a42-129">È anche possibile usare jQuery o un'altra API AJAX per recuperare le informazioni.</span><span class="sxs-lookup"><span data-stu-id="87a42-129">You could also use jQuery or another AJAX API to fetch the information.</span></span>  <span data-ttu-id="87a42-130">I dati saranno ricevuti come oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="87a42-130">Data is received as a JSON object.</span></span>
