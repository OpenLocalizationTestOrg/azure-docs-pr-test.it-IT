
Hello esempio precedente è stato uno standard sign-in, che richiede hello client toocontact entrambi hello identity provider e hello servizio back-end Azure ogni volta che viene avviata l'applicazione hello. Questo metodo è inefficiente e se molti clienti tentano toostart app contemporaneamente, è possibile avere problemi di utilizzo. Un approccio migliore consiste toocache hello autorizzazione token restituito da hello servizio di Azure e provare toouse questo prima di utilizzare un provider basato su Accedi.

> [!NOTE]
> È possibile memorizzare nella cache token hello emesso dal back-end di hello indipendentemente dal fatto se si utilizza l'autenticazione client gestita o servizio servizio di Azure. In questa esercitazione viene usata l'autenticazione gestita dal servizio.
>
>

1. Aprire il file ToDoActivity.java hello e aggiungere hello seguendo le istruzioni di importazione:

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. Aggiungere i seguenti membri toohello hello `ToDoActivity` classe.

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. Nel file hello ToDoActivity.java aggiungere hello seguente definizione per hello `cacheUserToken` metodo.

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    Questo metodo archivia i token e un ID utente hello in un file di preferenza che è contrassegnato come privato. Si deve proteggere accesso toohello cache in modo che le altre app nel dispositivo hello non dispone di accesso toohello token. preferenza di Hello è in modalità sandbox per l'applicazione hello. Tuttavia, se un utente riesce ad dispositivo toohello di accesso, è possibile che si può ottenere accesso cache dei token toohello tramite altri mezzi.

   > [!NOTE]
   > È possibile proteggere ulteriormente i token hello con la crittografia, se i dati tooyour token di accesso viene considerati altamente sensibili e un utente può ottenere dispositivo toohello di accesso. Tuttavia, una soluzione completamente protetta esula hello in questa esercitazione e dipende dai requisiti di sicurezza.
   >
   >
4. Nel file hello ToDoActivity.java aggiungere hello seguente definizione per hello `loadUserTokenCache` metodo.

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
5. In hello *ToDoActivity.java* file, sostituire hello `authenticate` metodo con hello al metodo, che usa una cache dei token. Provider di accesso hello se si desidera modificare toouse un account diverso da Google.

        private void authenticate() {
            // We first try tooload a token cache if one exists.
            if (loadUserTokenCache(mClient))
            {
                createTable();
            }
            // If we failed tooload a token cache, login and create a token cache
            else
            {
                // Login using hello Google provider.    
                ListenableFuture<MobileServiceUser> mLogin = mClient.login(MobileServiceAuthenticationProvider.Google);

                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        createAndShowDialog("You must log in. Login Required", "Error");
                    }           
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        createAndShowDialog(String.format(
                                "You are now logged in - %1$2s",
                                user.getUserId()), "Success");
                        cacheUserToken(mClient.getCurrentUser());
                        createTable();    
                    }
                });
            }
        }
6. Compilare l'autenticazione di app e prova hello usando un account valido. Eseguirla almeno due volte. Durante hello prima esecuzione, si dovrebbe ricevere un messaggio di richiesta toosign in e creare cache dei token hello. Successivamente, ogni esecuzione tenta cache dei token hello tooload per l'autenticazione. Non dovrebbe essere necessario toosign in.
