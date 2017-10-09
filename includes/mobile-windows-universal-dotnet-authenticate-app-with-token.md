
1. Nel file di progetto di hello MainPage.xaml.cs, aggiungere il seguente hello **utilizzando** istruzioni:
   
        using System.Linq;        
        using Windows.Security.Credentials;
2. Sostituire hello **AuthenticateAsync** metodo con hello seguente codice:
   
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
   
            // This sample uses hello Facebook provider.
            var provider = MobileServiceAuthenticationProvider.Facebook;
   
            // Use hello PasswordVault toosecurely store and access credentials.
            PasswordVault vault = new PasswordVault();
            PasswordCredential credential = null;
   
            try
            {
                // Try tooget an existing credential from hello vault.
                credential = vault.FindAllByResource(provider.ToString()).FirstOrDefault();
            }
            catch (Exception)
            {
                // When there is no matching resource an error occurs, which we ignore.
            }
   
            if (credential != null)
            {
                // Create a user from hello stored credentials.
                user = new MobileServiceUser(credential.UserName);
                credential.RetrievePassword();
                user.MobileServiceAuthenticationToken = credential.Password;
   
                // Set hello user from hello stored credentials.
                App.MobileService.CurrentUser = user;
   
                // Consider adding a check toodetermine if hello token is 
                // expired, as shown in this post: http://aka.ms/jww5vp.
   
                success = true;
                message = string.Format("Cached credentials for user - {0}", user.UserId);
            }
            else
            {
                try
                {
                    // Login with hello identity provider.
                    user = await App.MobileService
                        .LoginAsync(provider);
   
                    // Create and store hello user credentials.
                    credential = new PasswordCredential(provider.ToString(),
                        user.UserId, user.MobileServiceAuthenticationToken);
                    vault.Add(credential);
   
                    success = true;
                    message = string.Format("You are now logged in - {0}", user.UserId);
                }
                catch (MobileServiceInvalidOperationException)
                {
                    message = "You must log in. Login Required";
                }
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
   
            return success;
        }
   
    In questa versione di **AuthenticateAsync**, app hello tenta toouse credenziali archiviate in hello **PasswordVault** tooaccess hello del servizio. Un accesso normale viene eseguito anche quando non sono disponibili credenziali archiviate.
   
   > [!NOTE]
   > Un token memorizzato nella cache potrebbe essere scaduto e la scadenza del token può verificarsi anche dopo l'autenticazione quando l'applicazione hello è in uso. toolearn toodetermine se un token è scaduto, vedere [cercare i token di autenticazione scaduto](http://aka.ms/jww5vp). Per gli errori di autorizzazione una soluzione toohandling tooexpiring correlate, vedere hello post [la memorizzazione nella cache e la gestione di token scaduto nei servizi mobili di Azure gestiti SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx). 
   > 
   > 
3. Riavviare app hello due volte.
   
    Si noti che all'avvio prima di hello, accedi con il provider di hello sono obbligatorio. Tuttavia, al riavvio del secondo hello vengono utilizzate le credenziali memorizzate nella cache di hello e Accedi viene ignorato. 

