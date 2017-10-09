### <a name="server-auth"></a>Procedura: Eseguire l'autenticazione con un provider (flusso server)
App per dispositivi mobili toohave gestire il processo di autenticazione hello nell'app, è necessario registrare l'app con il provider di identità. Quindi il servizio App di Azure, è necessario tooconfigure hello ID dell'applicazione e il segreto fornite dal provider.
Per ulteriori informazioni, vedere l'esercitazione hello [Aggiungi autenticazione tooyour app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).

Dopo aver registrato il provider di identità, chiamare hello `.login()` metodo con nome hello del provider. Ad esempio, toologin con Facebook utilizzare hello seguente codice:

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

i valori validi per il provider di hello Hello sono 'aad', 'facebook', 'google', 'microsoftaccount' e 'twitter'.

> [!NOTE]
> L'autenticazione di Google attualmente non funziona tramite Flusso server.  tooauthenticate con Google, è necessario utilizzare un [metodo flusso client](#client-auth).

In questo caso, il servizio App di Azure gestisce il flusso di autenticazione OAuth 2.0 hello.  Visualizza la pagina di accesso hello del provider selezionato hello e genera un token di autenticazione del servizio App dopo aver eseguito correttamente l'accesso con provider di identità hello. funzione di accesso Hello, al termine, restituisce un oggetto JSON che espone sia l'ID utente hello e App servizio token di autenticazione nei campi di ID utente e authenticationToken hello, rispettivamente. È possibile memorizzare questo token nella cache e riutilizzarlo fino alla scadenza.

###<a name="client-auth"></a>Procedura: Eseguire l'autenticazione con un provider (flusso client)

L'app può anche in modo indipendente, contattare il provider di identità hello e fornire hello restituiti token tooyour servizio App per l'autenticazione. Questo flusso client consente un'esperienza di accesso singola per gli utenti o i dati utente aggiuntivi tooretrieve dal provider di identità hello tooprovide.

#### <a name="social-authentication-basic-example"></a>Esempio di base di autenticazione tramite social network

Questo esempio utilizza il client SDK di Facebook per l'autenticazione:

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
Questo esempio si presuppone che token hello fornito dal provider rispettivi hello SDK viene archiviato nella variabile token hello.

#### <a name="microsoft-account-example"></a>Esempio di account Microsoft

Hello seguente viene illustrato come utilizzare hello Live SDK, che supporta single sign-on per applicazioni Windows Store con Account Microsoft:

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

In questo esempio Ottiene un token da Live Connect, ovvero tooyour fornito servizio App chiamando la funzione di accesso hello.

###<a name="auth-getinfo"></a>Procedura: ottenere informazioni sull'utente autenticato hello

informazioni di autenticazione Hello possono essere recuperate da hello `/.auth/me` endpoint utilizzando HTTP chiamare con qualsiasi libreria AJAX.  Assicurarsi di impostare hello `X-ZUMO-AUTH` token di autenticazione tooyour intestazione.  Hello token di autenticazione viene archiviato `client.currentUser.mobileServiceAuthenticationToken`.  Ad esempio, toouse hello recupero API:

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

L'operazione di recupero è disponibile come [pacchetto npm](https://www.npmjs.com/package/whatwg-fetch) oppure può essere scaricato tramite il browser da [CDNJS](https://cdnjs.com/libraries/fetch). È anche possibile usare jQuery o informazioni di un'altra API AJAX toofetch hello.  I dati saranno ricevuti come oggetto JSON.
