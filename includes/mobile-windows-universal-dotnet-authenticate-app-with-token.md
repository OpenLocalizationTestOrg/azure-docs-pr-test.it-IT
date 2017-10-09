
1. <span data-ttu-id="3da71-101">Nel file di progetto di hello MainPage.xaml.cs, aggiungere il seguente hello **utilizzando** istruzioni:</span><span class="sxs-lookup"><span data-stu-id="3da71-101">In hello MainPage.xaml.cs project file, add hello following **using** statements:</span></span>
   
        using System.Linq;        
        using Windows.Security.Credentials;
2. <span data-ttu-id="3da71-102">Sostituire hello **AuthenticateAsync** metodo con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="3da71-102">Replace hello **AuthenticateAsync** method with hello following code:</span></span>
   
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
   
    <span data-ttu-id="3da71-103">In questa versione di **AuthenticateAsync**, app hello tenta toouse credenziali archiviate in hello **PasswordVault** tooaccess hello del servizio.</span><span class="sxs-lookup"><span data-stu-id="3da71-103">In this version of **AuthenticateAsync**, hello app tries toouse credentials stored in hello **PasswordVault** tooaccess hello service.</span></span> <span data-ttu-id="3da71-104">Un accesso normale viene eseguito anche quando non sono disponibili credenziali archiviate.</span><span class="sxs-lookup"><span data-stu-id="3da71-104">A regular sign-in is also performed when there is no stored credential.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3da71-105">Un token memorizzato nella cache potrebbe essere scaduto e la scadenza del token può verificarsi anche dopo l'autenticazione quando l'applicazione hello è in uso.</span><span class="sxs-lookup"><span data-stu-id="3da71-105">A cached token may be expired, and token expiration can also occur after authentication when hello app is in use.</span></span> <span data-ttu-id="3da71-106">toolearn toodetermine se un token è scaduto, vedere [cercare i token di autenticazione scaduto](http://aka.ms/jww5vp).</span><span class="sxs-lookup"><span data-stu-id="3da71-106">toolearn how toodetermine if a token is expired, see [Check for expired authentication tokens](http://aka.ms/jww5vp).</span></span> <span data-ttu-id="3da71-107">Per gli errori di autorizzazione una soluzione toohandling tooexpiring correlate, vedere hello post [la memorizzazione nella cache e la gestione di token scaduto nei servizi mobili di Azure gestiti SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx).</span><span class="sxs-lookup"><span data-stu-id="3da71-107">For a solution toohandling authorization errors related tooexpiring tokens, see hello post [Caching and handling expired tokens in Azure Mobile Services managed SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx).</span></span> 
   > 
   > 
3. <span data-ttu-id="3da71-108">Riavviare app hello due volte.</span><span class="sxs-lookup"><span data-stu-id="3da71-108">Restart hello app twice.</span></span>
   
    <span data-ttu-id="3da71-109">Si noti che all'avvio prima di hello, accedi con il provider di hello sono obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="3da71-109">Notice that on hello first start-up, sign-in with hello provider is again required.</span></span> <span data-ttu-id="3da71-110">Tuttavia, al riavvio del secondo hello vengono utilizzate le credenziali memorizzate nella cache di hello e Accedi viene ignorato.</span><span class="sxs-lookup"><span data-stu-id="3da71-110">However, on hello second restart hello cached credentials are used and sign-in is bypassed.</span></span> 

