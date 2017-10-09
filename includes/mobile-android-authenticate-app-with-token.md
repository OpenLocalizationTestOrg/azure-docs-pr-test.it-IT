
<span data-ttu-id="ecaad-101">Hello esempio precedente è stato uno standard sign-in, che richiede hello client toocontact entrambi hello identity provider e hello servizio back-end Azure ogni volta che viene avviata l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ecaad-101">hello previous example showed a standard sign-in, which requires hello client toocontact both hello identity provider and hello back-end Azure service every time hello app starts.</span></span> <span data-ttu-id="ecaad-102">Questo metodo è inefficiente e se molti clienti tentano toostart app contemporaneamente, è possibile avere problemi di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="ecaad-102">This method is inefficient, and you can have usage-related issues if many customers try toostart your app simultaneously.</span></span> <span data-ttu-id="ecaad-103">Un approccio migliore consiste toocache hello autorizzazione token restituito da hello servizio di Azure e provare toouse questo prima di utilizzare un provider basato su Accedi.</span><span class="sxs-lookup"><span data-stu-id="ecaad-103">A better approach is toocache hello authorization token returned by hello Azure service, and try toouse this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="ecaad-104">È possibile memorizzare nella cache token hello emesso dal back-end di hello indipendentemente dal fatto se si utilizza l'autenticazione client gestita o servizio servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="ecaad-104">You can cache hello token issued by hello back-end Azure service regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="ecaad-105">In questa esercitazione viene usata l'autenticazione gestita dal servizio.</span><span class="sxs-lookup"><span data-stu-id="ecaad-105">This tutorial uses service-managed authentication.</span></span>
>
>

1. <span data-ttu-id="ecaad-106">Aprire il file ToDoActivity.java hello e aggiungere hello seguendo le istruzioni di importazione:</span><span class="sxs-lookup"><span data-stu-id="ecaad-106">Open hello ToDoActivity.java file and add hello following import statements:</span></span>

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. <span data-ttu-id="ecaad-107">Aggiungere i seguenti membri toohello hello `ToDoActivity` classe.</span><span class="sxs-lookup"><span data-stu-id="ecaad-107">Add hello following members toohello `ToDoActivity` class.</span></span>

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. <span data-ttu-id="ecaad-108">Nel file hello ToDoActivity.java aggiungere hello seguente definizione per hello `cacheUserToken` metodo.</span><span class="sxs-lookup"><span data-stu-id="ecaad-108">In hello ToDoActivity.java file, add hello following definition for hello `cacheUserToken` method.</span></span>

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    <span data-ttu-id="ecaad-109">Questo metodo archivia i token e un ID utente hello in un file di preferenza che è contrassegnato come privato.</span><span class="sxs-lookup"><span data-stu-id="ecaad-109">This method stores hello user ID and token in a preference file that is marked private.</span></span> <span data-ttu-id="ecaad-110">Si deve proteggere accesso toohello cache in modo che le altre app nel dispositivo hello non dispone di accesso toohello token.</span><span class="sxs-lookup"><span data-stu-id="ecaad-110">This should protect access toohello cache so that other apps on hello device do not have access toohello token.</span></span> <span data-ttu-id="ecaad-111">preferenza di Hello è in modalità sandbox per l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ecaad-111">hello preference is sandboxed for hello app.</span></span> <span data-ttu-id="ecaad-112">Tuttavia, se un utente riesce ad dispositivo toohello di accesso, è possibile che si può ottenere accesso cache dei token toohello tramite altri mezzi.</span><span class="sxs-lookup"><span data-stu-id="ecaad-112">However, if someone gains access toohello device, it is possible that they may gain access toohello token cache through other means.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ecaad-113">È possibile proteggere ulteriormente i token hello con la crittografia, se i dati tooyour token di accesso viene considerati altamente sensibili e un utente può ottenere dispositivo toohello di accesso.</span><span class="sxs-lookup"><span data-stu-id="ecaad-113">You can further protect hello token with encryption, if token access tooyour data is considered highly sensitive and someone may gain access toohello device.</span></span> <span data-ttu-id="ecaad-114">Tuttavia, una soluzione completamente protetta esula hello in questa esercitazione e dipende dai requisiti di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="ecaad-114">A completely secure solution is beyond hello scope of this tutorial, however, and depends on your security requirements.</span></span>
   >
   >
4. <span data-ttu-id="ecaad-115">Nel file hello ToDoActivity.java aggiungere hello seguente definizione per hello `loadUserTokenCache` metodo.</span><span class="sxs-lookup"><span data-stu-id="ecaad-115">In hello ToDoActivity.java file, add hello following definition for hello `loadUserTokenCache` method.</span></span>

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
5. <span data-ttu-id="ecaad-116">In hello *ToDoActivity.java* file, sostituire hello `authenticate` metodo con hello al metodo, che usa una cache dei token.</span><span class="sxs-lookup"><span data-stu-id="ecaad-116">In hello *ToDoActivity.java* file, replace hello `authenticate` method with hello following method, which uses a token cache.</span></span> <span data-ttu-id="ecaad-117">Provider di accesso hello se si desidera modificare toouse un account diverso da Google.</span><span class="sxs-lookup"><span data-stu-id="ecaad-117">Change hello login provider if you want toouse an account other than Google.</span></span>

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
6. <span data-ttu-id="ecaad-118">Compilare l'autenticazione di app e prova hello usando un account valido.</span><span class="sxs-lookup"><span data-stu-id="ecaad-118">Build hello app and test authentication using a valid account.</span></span> <span data-ttu-id="ecaad-119">Eseguirla almeno due volte.</span><span class="sxs-lookup"><span data-stu-id="ecaad-119">Run it at least twice.</span></span> <span data-ttu-id="ecaad-120">Durante hello prima esecuzione, si dovrebbe ricevere un messaggio di richiesta toosign in e creare cache dei token hello.</span><span class="sxs-lookup"><span data-stu-id="ecaad-120">During hello first run, you should receive a prompt toosign in and create hello token cache.</span></span> <span data-ttu-id="ecaad-121">Successivamente, ogni esecuzione tenta cache dei token hello tooload per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="ecaad-121">After that, each run attempts tooload hello token cache for authentication.</span></span> <span data-ttu-id="ecaad-122">Non dovrebbe essere necessario toosign in.</span><span class="sxs-lookup"><span data-stu-id="ecaad-122">You should not be required toosign in.</span></span>
