
L'esempio precedente illustra un accesso standard che richiede al client di contattare sia il provider di identità sia il servizio back-end di Azure ogni volta che l'app viene avviata. Questo metodo risulta inefficiente e può creare problemi relativi all'uso se più clienti tentano di avviare l'app contemporaneamente. Un miglior approccio consiste nel memorizzare nella cache il token di autorizzazione restituito dal servizio Azure e provare a usarlo prima di un accesso basato su provider.

> [!NOTE]
> È possibile memorizzare nella cache il token rilasciato dal servizio back-end di Azure indipendentemente dal fatto che si usi l'autenticazione gestita dal client o dal servizio. In questa esercitazione viene usata l'autenticazione gestita dal servizio.
>
>

1. Aprire il file ToDoActivity.java e quindi aggiungere le istruzioni import seguenti:

    ```java
    import android.content.Context;
    import android.content.SharedPreferences;
    import android.content.SharedPreferences.Editor;
    ```

2. Aggiungere i membri seguenti alla classe `ToDoActivity` :

    ```java
    public static final String SHAREDPREFFILE = "temp";
    public static final String USERIDPREF = "uid";
    public static final String TOKENPREF = "tkn";
    ```

3. Nel file ToDoActivity.java aggiungere la definizione seguente per il metodo `cacheUserToken`.

    ```java
    private void cacheUserToken(MobileServiceUser user)
    {
        SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
        Editor editor = prefs.edit();
        editor.putString(USERIDPREF, user.getUserId());
        editor.putString(TOKENPREF, user.getAuthenticationToken());
        editor.commit();
    }
    ```

    Questo metodo consente di memorizzare l'ID utente e il token in un file delle preferenze contrassegnato come privato. In questo modo è possibile proteggere l'accesso alla cache, affinché le altre app sul dispositivo non possano accedere al token. La preferenza è in modalità sandbox per l'applicazione. Tuttavia, se qualcuno riesce ad accedere al dispositivo, è possibile che riesca accedere anche alla cache dei token con altri mezzi.

   > [!NOTE]
   > È possibile proteggere ulteriormente il token con la crittografia se l'accesso token ai dati è considerato altamente sensibile e qualcuno potrebbe accedere al dispositivo. Tuttavia, una soluzione del tutto sicura esula dall'ambito di questa esercitazione e dipende dai rispettivi requisiti di sicurezza.
   >
   >

4. Nel file ToDoActivity.java aggiungere la definizione seguente per il metodo `loadUserTokenCache`.

    ```java
    private boolean loadUserTokenCache(MobileServiceClient client)
    {
        SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
        String userId = prefs.getString(USERIDPREF, null);
        if (userId == null)
            return false;
        String token = prefs.getString(TOKENPREF, null);
        if (token == null)
            return false;

        MobileServiceUser user = new MobileServiceUser(userId);
        user.setAuthenticationToken(token);
        client.setCurrentUser(user);

        return true;
    }
    ```

5. Nel file *ToDoActivity.java* sostituire i metodi `authenticate` e `onActivityResult` con i seguenti, che usano una cache dei token. Modificare il provider di accesso se si vuole usare un account diverso da Google.

    ```java
    private void authenticate() {
        // We first try to load a token cache if one exists.
        if (loadUserTokenCache(mClient))
        {
            createTable();
        }
        // If we failed to load a token cache, login and create a token cache
        else
        {
            // Login using the Google provider.
            mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
        }
    }

    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        // When request completes
        if (resultCode == RESULT_OK) {
            // Check the request code matches the one we send in the login request
            if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
                MobileServiceActivityResult result = mClient.onActivityResult(data);
                if (result.isLoggedIn()) {
                    // login succeeded
                    createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                    cacheUserToken(mClient.getCurrentUser());
                    createTable();
                } else {
                    // login failed, check the error message
                    String errorMessage = result.getErrorMessage();
                    createAndShowDialog(errorMessage, "Error");
                }
            }
        }
    }
    ```

6. Creare l'app e testare l'autenticazione con un account valido. Eseguirla almeno due volte. Durante la prima esecuzione, si riceverà un prompt di accesso per creare la cache dei token. Successivamente, ogni esecuzione tenta di caricare la cache dei token per l'autenticazione. Non viene richiesto di effettuare l'accesso.
