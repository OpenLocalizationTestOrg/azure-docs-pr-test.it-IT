## <a name="create-hello-webapi-project"></a><span data-ttu-id="ad721-101">Creare il progetto WebAPI hello</span><span class="sxs-lookup"><span data-stu-id="ad721-101">Create hello WebAPI Project</span></span>
<span data-ttu-id="ad721-102">Verrà creato un nuovo back-end ASP.NET WebAPI in sezioni hello che seguono e disporrà di tre scopi principali:</span><span class="sxs-lookup"><span data-stu-id="ad721-102">A new ASP.NET WebAPI backend will be created in hello sections that follow and it will have three main purposes:</span></span>

1. <span data-ttu-id="ad721-103">**L'autenticazione dei client**: successive richieste di client tooauthenticate e utente di associare hello con richiesta di hello verrà aggiunto un gestore di messaggi.</span><span class="sxs-lookup"><span data-stu-id="ad721-103">**Authenticating Clients**: A message handler will be added later tooauthenticate client requests and associate hello user with hello request.</span></span>
2. <span data-ttu-id="ad721-104">**Registrazioni di notifica client**: in un secondo momento, si aggiungerà un nuove registrazioni di controller toohandle per le notifiche di tooreceive un client dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ad721-104">**Client Notification Registrations**: Later, you will add a controller toohandle new registrations for a client device tooreceive notifications.</span></span> <span data-ttu-id="ad721-105">Hello nome utente autenticato verrà aggiunta automaticamente la registrazione di toohello come un [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span><span class="sxs-lookup"><span data-stu-id="ad721-105">hello authenticated user name will automatically be added toohello registration as a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span></span>
3. <span data-ttu-id="ad721-106">**L'invio di notifiche tooClients**: in un secondo momento, verrà inoltre aggiunto un tooprovide controller un modo per un tootrigger utente toodevices un push sicura e i client associati a tag hello.</span><span class="sxs-lookup"><span data-stu-id="ad721-106">**Sending Notifications tooClients**: Later, you will also add a controller tooprovide a way for a user tootrigger a secure push toodevices and clients associated with hello tag.</span></span> 

<span data-ttu-id="ad721-107">Hello alla procedura seguente mostra come toocreate hello nuovo back-end WebAPI ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="ad721-107">hello following steps show how toocreate hello new ASP.NET WebAPI backend:</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ad721-108">Se si utilizza Visual Studio 2015 o versione precedente, prima di iniziare questa esercitazione, assicurarsi di aver installato una versione più recente di hello di hello Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="ad721-108">If you are using Visual Studio 2015 or earlier, before starting this tutorial, please ensure that you have installed hello latest version of hello NuGet Package Manager.</span></span> <span data-ttu-id="ad721-109">toocheck, avviare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ad721-109">toocheck, start Visual Studio.</span></span> <span data-ttu-id="ad721-110">Da hello **strumenti** menu, fare clic su **estensioni e aggiornamenti**.</span><span class="sxs-lookup"><span data-stu-id="ad721-110">From hello **Tools** menu, click **Extensions and Updates**.</span></span> <span data-ttu-id="ad721-111">Cercare **Gestione pacchetti NuGet** per la versione di Visual Studio e assicurarsi di disporre hello ultima versione.</span><span class="sxs-lookup"><span data-stu-id="ad721-111">Search for **NuGet Package Manager** for your version of Visual Studio, and make sure you have hello latest version.</span></span> <span data-ttu-id="ad721-112">In caso contrario, disinstallare e reinstallare hello Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="ad721-112">If not, please uninstall, then reinstall hello NuGet Package Manager.</span></span>
> 
> ![][B4]
> 
> [!NOTE]
> <span data-ttu-id="ad721-113">Assicurarsi di aver installato Visual Studio hello [Azure SDK](https://azure.microsoft.com/downloads/) per la distribuzione del sito Web.</span><span class="sxs-lookup"><span data-stu-id="ad721-113">Make sure you have installed hello Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) for website deployment.</span></span>
> 
> 

1. <span data-ttu-id="ad721-114">Avviare Visual Studio o Visual Studio Express.</span><span class="sxs-lookup"><span data-stu-id="ad721-114">Start Visual Studio or Visual Studio Express.</span></span> <span data-ttu-id="ad721-115">Fare clic su **Esplora Server** e Accedi tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="ad721-115">Click **Server Explorer** and sign in tooyour Azure account.</span></span> <span data-ttu-id="ad721-116">Visual Studio sarà necessario toocreate hello sito web di risorse nell'account di accesso.</span><span class="sxs-lookup"><span data-stu-id="ad721-116">Visual Studio will need you signed in toocreate hello web site resources on your account.</span></span>
2. <span data-ttu-id="ad721-117">In Visual Studio, fare clic su **File**, quindi fare clic su **New**, quindi **progetto**, espandere **modelli**, **Visual c#**, quindi fare clic su **Web** e **applicazione Web ASP.NET**, nome del tipo hello **AppBackend**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ad721-117">In Visual Studio, click **File**, then click **New**, then **Project**, expand **Templates**, **Visual C#**, then click **Web** and **ASP.NET Web Application**, type hello name **AppBackend**, and then click **OK**.</span></span> 
   
    ![][B1]
3. <span data-ttu-id="ad721-118">In hello **nuovo progetto ASP.NET** finestra di dialogo, fare clic su **API Web**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ad721-118">In hello **New ASP.NET Project** dialog, click **Web API**, then click **OK**.</span></span>
   
    ![][B2]
4. <span data-ttu-id="ad721-119">In hello **configurare App Web di Microsoft Azure** finestra di dialogo, scegliere una sottoscrizione e un **piano di servizio App** è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="ad721-119">In hello **Configure Microsoft Azure Web App** dialog, choose a subscription, and an **App Service plan** you have already created.</span></span> <span data-ttu-id="ad721-120">È anche possibile scegliere **creare un nuovo piano di servizio app** e crearne uno dalla finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="ad721-120">You can also choose **Create a new app service plan** and create one from hello dialog.</span></span> <span data-ttu-id="ad721-121">Per questa esercitazione non è necessario disporre di un database.</span><span class="sxs-lookup"><span data-stu-id="ad721-121">You do not need a database for this tutorial.</span></span> <span data-ttu-id="ad721-122">Dopo aver selezionato il piano di servizio app, fare clic su **OK** progetto hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="ad721-122">Once you have selected your app service plan, click **OK** toocreate hello project.</span></span>
   
    ![][B5]

## <a name="authenticating-clients-toohello-webapi-backend"></a><span data-ttu-id="ad721-123">L'autenticazione client toohello WebAPI Backend</span><span class="sxs-lookup"><span data-stu-id="ad721-123">Authenticating Clients toohello WebAPI Backend</span></span>
<span data-ttu-id="ad721-124">In questa sezione si creerà una nuova classe di gestore di messaggi denominata **AuthenticationTestHandler** per hello nuovo back-end.</span><span class="sxs-lookup"><span data-stu-id="ad721-124">In this section, you will create a new message handler class named **AuthenticationTestHandler** for hello new backend.</span></span> <span data-ttu-id="ad721-125">Questa classe è derivata da [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) e aggiunta come un gestore di messaggi in modo che può elaborare tutte le richieste pervenute nel back-end hello.</span><span class="sxs-lookup"><span data-stu-id="ad721-125">This class is derived from [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) and added as a message handler so it can process all requests coming into hello backend.</span></span> 

1. <span data-ttu-id="ad721-126">In Esplora soluzioni fare doppio clic su hello **AppBackend** del progetto, fare clic su **Aggiungi**, quindi fare clic su **classe**.</span><span class="sxs-lookup"><span data-stu-id="ad721-126">In Solution Explorer, right-click hello **AppBackend** project, click **Add**, then click **Class**.</span></span> <span data-ttu-id="ad721-127">Nome nuova classe hello **AuthenticationTestHandler.cs**, fare clic su **Aggiungi** classe hello toogenerate.</span><span class="sxs-lookup"><span data-stu-id="ad721-127">Name hello new class **AuthenticationTestHandler.cs**, and click **Add** toogenerate hello class.</span></span> <span data-ttu-id="ad721-128">Questa classe verrà utilizzato tooauthenticate gli utenti che usano *l'autenticazione di base* per semplicità.</span><span class="sxs-lookup"><span data-stu-id="ad721-128">This class will be used tooauthenticate users using *Basic Authentication* for simplicity.</span></span> <span data-ttu-id="ad721-129">Tenere presente che l'app può usare qualsiasi schema di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="ad721-129">Note that your app can use any authentication scheme.</span></span>
2. <span data-ttu-id="ad721-130">In AuthenticationTestHandler.cs, aggiungere hello seguente `using` istruzioni:</span><span class="sxs-lookup"><span data-stu-id="ad721-130">In AuthenticationTestHandler.cs, add hello following `using` statements:</span></span>
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. <span data-ttu-id="ad721-131">In AuthenticationTestHandler.cs, sostituendo hello `AuthenticationTestHandler` definizione di classe con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="ad721-131">In AuthenticationTestHandler.cs, replacing hello `AuthenticationTestHandler` class definition with hello following code.</span></span> 
   
    <span data-ttu-id="ad721-132">Questo gestore autorizzerà richiesta hello quando viene soddisfatte hello e tre le condizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ad721-132">This handler will authorize hello request when hello following three conditions are all true:</span></span>
   
   * <span data-ttu-id="ad721-133">richiesta di Hello incluso un *autorizzazione* intestazione.</span><span class="sxs-lookup"><span data-stu-id="ad721-133">hello request included an *Authorization* header.</span></span> 
   * <span data-ttu-id="ad721-134">richiesta di Hello utilizza *base* l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="ad721-134">hello request uses *basic* authentication.</span></span> 
   * <span data-ttu-id="ad721-135">stringa Hello del nome utente e la stringa di password hello sono hello stessa stringa.</span><span class="sxs-lookup"><span data-stu-id="ad721-135">hello user name string and hello password string are hello same string.</span></span>
     
     <span data-ttu-id="ad721-136">In caso contrario, hello richiesta verrà rifiutata.</span><span class="sxs-lookup"><span data-stu-id="ad721-136">Otherwise, hello request will be rejected.</span></span> <span data-ttu-id="ad721-137">Non si tratta di un vero approccio di autenticazione e autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="ad721-137">This is not a true authentication and authorization approach.</span></span> <span data-ttu-id="ad721-138">È un esempio molto semplice per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ad721-138">It is just a very simple example for this tutorial.</span></span>
     
     <span data-ttu-id="ad721-139">Se il messaggio di richiesta di hello è autenticato e autorizzato per hello `AuthenticationTestHandler`, utente di autenticazione di base hello sarà toohello associata la richiesta corrente su hello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span><span class="sxs-lookup"><span data-stu-id="ad721-139">If hello request message is authenticated and authorized by hello `AuthenticationTestHandler`, then hello basic authentication user will be attached toohello current request on hello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span></span> <span data-ttu-id="ad721-140">Informazioni utente in hello HttpContext verranno utilizzate da un altro controller (RegisterController) tooadd successive un [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello richiesta di registrazione della notifica.</span><span class="sxs-lookup"><span data-stu-id="ad721-140">User information in hello HttpContext will be used by another controller (RegisterController) later tooadd a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello notification registration request.</span></span>
     
       <span data-ttu-id="ad721-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span><span class="sxs-lookup"><span data-stu-id="ad721-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span></span>
     
               if (authorizationHeader != null && authorizationHeader
                   .StartsWith("Basic ", StringComparison.InvariantCultureIgnoreCase))
               {
                   string authorizationUserAndPwdBase64 =
                       authorizationHeader.Substring("Basic ".Length);
                   string authorizationUserAndPwd = Encoding.Default
                       .GetString(Convert.FromBase64String(authorizationUserAndPwdBase64));
                   string user = authorizationUserAndPwd.Split(':')[0];
                   string password = authorizationUserAndPwd.Split(':')[1];
     
                   if (verifyUserAndPwd(user, password))
                   {
                       // Attach hello new principal object toohello current HttpContext object
                       HttpContext.Current.User =
                           new GenericPrincipal(new GenericIdentity(user), new string[0]);
                       System.Threading.Thread.CurrentPrincipal =
                           System.Web.HttpContext.Current.User;
                   }
                   else return Unauthorized();
               }
               else return Unauthorized();
     
               return base.SendAsync(request, cancellationToken);
           }
     
           private bool verifyUserAndPwd(string user, string password)
           {
               // This is not a real authentication scheme.
               return user == password;
           }
     
           private Task<HttpResponseMessage> Unauthorized()
           {
               var response = new HttpResponseMessage(HttpStatusCode.Forbidden);
               var tsc = new TaskCompletionSource<HttpResponseMessage>();
               tsc.SetResult(response);
               return tsc.Task;
           }
       <span data-ttu-id="ad721-142">}</span><span class="sxs-lookup"><span data-stu-id="ad721-142">}</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="ad721-143">**Nota sulla sicurezza**: hello `AuthenticationTestHandler` classe non fornisce l'autenticazione true.</span><span class="sxs-lookup"><span data-stu-id="ad721-143">**Security Note**: hello `AuthenticationTestHandler` class does not provide true authentication.</span></span> <span data-ttu-id="ad721-144">È usato toomimic solo l'autenticazione di base e non è protetto.</span><span class="sxs-lookup"><span data-stu-id="ad721-144">It is used only toomimic basic authentication and is not secure.</span></span> <span data-ttu-id="ad721-145">È necessario implementare un meccanismo di autenticazione sicuro nelle applicazioni e nei servizi di produzione.</span><span class="sxs-lookup"><span data-stu-id="ad721-145">You must implement a secure authentication mechanism in your production applications and services.</span></span>                
     > 
     > 
4. <span data-ttu-id="ad721-146">Aggiungere hello seguente codice alla fine hello hello `Register` metodo hello **App_Start/WebApiConfig.cs** gestore di messaggi hello tooregister classe:</span><span class="sxs-lookup"><span data-stu-id="ad721-146">Add hello following code at hello end of hello `Register` method in hello **App_Start/WebApiConfig.cs** class tooregister hello message handler:</span></span>
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. <span data-ttu-id="ad721-147">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="ad721-147">Save your changes.</span></span>

## <a name="registering-for-notifications-using-hello-webapi-backend"></a><span data-ttu-id="ad721-148">La registrazione per le notifiche tramite hello WebAPI Backend</span><span class="sxs-lookup"><span data-stu-id="ad721-148">Registering for Notifications using hello WebAPI Backend</span></span>
<span data-ttu-id="ad721-149">In questa sezione verranno aggiunti che un nuovo toohandle di back-end di WebAPI toohello controller richiede tooregister un utente e dispositivo per le notifiche tramite la libreria client di hello per gli hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="ad721-149">In this section, we will add a new controller toohello WebAPI backend toohandle requests tooregister a user and device for notifications using hello client library for notification hubs.</span></span> <span data-ttu-id="ad721-150">controller Hello verrà aggiunto un tag di utente per l'utente hello che è stato autenticato e collegato toohello HttpContext da hello `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="ad721-150">hello controller will add a user tag for hello user that was authenticated and attached toohello HttpContext by hello `AuthenticationTestHandler`.</span></span> <span data-ttu-id="ad721-151">tag Hello avrà il formato di stringa hello, `"username:<actual username>"`.</span><span class="sxs-lookup"><span data-stu-id="ad721-151">hello tag will have hello string format, `"username:<actual username>"`.</span></span>

1. <span data-ttu-id="ad721-152">In Esplora soluzioni fare doppio clic su hello **AppBackend** del progetto e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ad721-152">In Solution Explorer, right-click hello **AppBackend** project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="ad721-153">Sul lato sinistro di hello, fare clic su **Online**e cercare **Microsoft.Azure.NotificationHubs** in hello **ricerca** casella.</span><span class="sxs-lookup"><span data-stu-id="ad721-153">On hello left-hand side, click **Online**, and search for **Microsoft.Azure.NotificationHubs** in hello **Search** box.</span></span>
3. <span data-ttu-id="ad721-154">Nell'elenco risultati hello, fare clic su **gli hub di notifica di Microsoft Azure**, quindi fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="ad721-154">In hello results list, click **Microsoft Azure Notification Hubs**, and then click **Install**.</span></span> <span data-ttu-id="ad721-155">Completare l'installazione di hello, quindi chiudere una finestra di gestione pacchetti NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="ad721-155">Complete hello installation, then close hello NuGet package manager window.</span></span>
   
    <span data-ttu-id="ad721-156">Aggiunge un toohello riferimento SDK di hub di notifica di Azure utilizzando hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacchetto NuGet di hub Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="ad721-156">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="ad721-157">A questo punto si creerà un nuovo file di classe che rappresenta la connessione hello con le notifiche toosend utilizzati hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="ad721-157">We will now create a new class file that represents hello connection with notification hub used toosend notifications.</span></span> <span data-ttu-id="ad721-158">In Esplora soluzioni hello, fare clic sul hello **modelli** cartella, fare clic su **Aggiungi**, quindi fare clic su **classe**.</span><span class="sxs-lookup"><span data-stu-id="ad721-158">In hello Solution Explorer, right-click hello **Models** folder, click **Add**, then click **Class**.</span></span> <span data-ttu-id="ad721-159">Nome nuova classe hello **Notifications.cs**, quindi fare clic su **Aggiungi** classe hello toogenerate.</span><span class="sxs-lookup"><span data-stu-id="ad721-159">Name hello new class **Notifications.cs**, then click **Add** toogenerate hello class.</span></span> 
   
    ![][B6]
5. <span data-ttu-id="ad721-160">In Notifications.cs, aggiungere hello seguente `using` istruzione all'inizio di hello del file hello:</span><span class="sxs-lookup"><span data-stu-id="ad721-160">In Notifications.cs, add hello following `using` statement at hello top of hello file:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
6. <span data-ttu-id="ad721-161">Sostituire hello `Notifications` definizione con seguenti hello di classe e rendere segnaposto hello due tooreplace che con stringa di connessione hello (con accesso completo) per l'hub di notifica e hello Nome hub (disponibile all'indirizzo [portale classico di Azure ](http://manage.windowsazure.com)):</span><span class="sxs-lookup"><span data-stu-id="ad721-161">Replace hello `Notifications` class definition with hello following and make sure tooreplace hello two placeholders with hello connection string (with full access) for your notification hub, and hello hub name (available at [Azure Classic Portal](http://manage.windowsazure.com)):</span></span>
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. <span data-ttu-id="ad721-162">Verrà quindi creato un nuovo controller denominato **RegisterController**.</span><span class="sxs-lookup"><span data-stu-id="ad721-162">Next we will create a new controller named **RegisterController**.</span></span> <span data-ttu-id="ad721-163">In Esplora soluzioni fare doppio clic su hello **controller** cartella, quindi fare clic su **Aggiungi**, quindi fare clic su **Controller**.</span><span class="sxs-lookup"><span data-stu-id="ad721-163">In Solution Explorer, right-click hello **Controllers** folder, then click **Add**, then click **Controller**.</span></span> <span data-ttu-id="ad721-164">Fare clic su hello **Web API 2 Controller: vuoto** elemento e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ad721-164">Click hello **Web API 2 Controller -- Empty** item, and then click **Add**.</span></span> <span data-ttu-id="ad721-165">Nome nuova classe hello **RegisterController**, quindi fare clic su **Aggiungi** toogenerate nuovamente i controller di hello.</span><span class="sxs-lookup"><span data-stu-id="ad721-165">Name hello new class **RegisterController**, and then click **Add** again toogenerate hello controller.</span></span>
   
    ![][B7]
   
    ![][B8]
8. <span data-ttu-id="ad721-166">In RegisterController.cs, aggiungere hello seguente `using` istruzioni:</span><span class="sxs-lookup"><span data-stu-id="ad721-166">In RegisterController.cs, add hello following `using` statements:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. <span data-ttu-id="ad721-167">Aggiungere hello seguente codice all'interno di hello `RegisterController` definizione di classe.</span><span class="sxs-lookup"><span data-stu-id="ad721-167">Add hello following code inside hello `RegisterController` class definition.</span></span> <span data-ttu-id="ad721-168">Si noti che in questo codice, aggiungere un utente per l'utente hello che tratta attaccato toohello HttpContext.</span><span class="sxs-lookup"><span data-stu-id="ad721-168">Note that in this code, we add a user tag for hello user this is attached toohello HttpContext.</span></span> <span data-ttu-id="ad721-169">utente Hello è stato autenticato e collegato toohello HttpContext dal filtro messaggi hello è stata aggiunta, `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="ad721-169">hello user was authenticated and attached toohello HttpContext by hello message filter we added, `AuthenticationTestHandler`.</span></span> <span data-ttu-id="ad721-170">È inoltre possibile aggiungere controlli facoltativo tooverify che hello utente disponga dei diritti tooregister per hello richiesto tag.</span><span class="sxs-lookup"><span data-stu-id="ad721-170">You can also add optional checks tooverify that hello user has rights tooregister for hello requested tags.</span></span>
   
        private NotificationHubClient hub;
   
        public RegisterController()
        {
            hub = Notifications.Instance.Hub;
        }
   
        public class DeviceRegistration
        {
            public string Platform { get; set; }
            public string Handle { get; set; }
            public string[] Tags { get; set; }
        }
   
        // POST api/register
        // This creates a registration id
        public async Task<string> Post(string handle = null)
        {
            string newRegistrationId = null;
   
            // make sure there are no existing registrations for this push handle (used for iOS and Android)
            if (handle != null)
            {
                var registrations = await hub.GetRegistrationsByChannelAsync(handle, 100);
   
                foreach (RegistrationDescription registration in registrations)
                {
                    if (newRegistrationId == null)
                    {
                        newRegistrationId = registration.RegistrationId;
                    }
                    else
                    {
                        await hub.DeleteRegistrationAsync(registration);
                    }
                }
            }
   
            if (newRegistrationId == null) 
                newRegistrationId = await hub.CreateRegistrationIdAsync();
   
            return newRegistrationId;
        }
   
        // PUT api/register/5
        // This creates or updates a registration (with provided channelURI) at hello specified id
        public async Task<HttpResponseMessage> Put(string id, DeviceRegistration deviceUpdate)
        {
            RegistrationDescription registration = null;
            switch (deviceUpdate.Platform)
            {
                case "mpns":
                    registration = new MpnsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "wns":
                    registration = new WindowsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "apns":
                    registration = new AppleRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "gcm":
                    registration = new GcmRegistrationDescription(deviceUpdate.Handle);
                    break;
                default:
                    throw new HttpResponseException(HttpStatusCode.BadRequest);
            }
   
            registration.RegistrationId = id;
            var username = HttpContext.Current.User.Identity.Name;
   
            // add check if user is allowed tooadd these tags
            registration.Tags = new HashSet<string>(deviceUpdate.Tags);
            registration.Tags.Add("username:" + username);
   
            try
            {
                await hub.CreateOrUpdateRegistrationAsync(registration);
            }
            catch (MessagingException e)
            {
                ReturnGoneIfHubResponseIsGone(e);
            }
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        // DELETE api/register/5
        public async Task<HttpResponseMessage> Delete(string id)
        {
            await hub.DeleteRegistrationAsync(id);
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        private static void ReturnGoneIfHubResponseIsGone(MessagingException e)
        {
            var webex = e.InnerException as WebException;
            if (webex.Status == WebExceptionStatus.ProtocolError)
            {
                var response = (HttpWebResponse)webex.Response;
                if (response.StatusCode == HttpStatusCode.Gone)
                    throw new HttpRequestException(HttpStatusCode.Gone.ToString());
            }
        }
10. <span data-ttu-id="ad721-171">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="ad721-171">Save your changes.</span></span>

## <a name="sending-notifications-from-hello-webapi-backend"></a><span data-ttu-id="ad721-172">L'invio di notifiche da hello WebAPI Backend</span><span class="sxs-lookup"><span data-stu-id="ad721-172">Sending Notifications from hello WebAPI Backend</span></span>
<span data-ttu-id="ad721-173">In questa sezione si aggiunge un nuovo controller che espone un modo per client dispositivi toosend una notifica in base a tag username hello utilizzo libreria Gestione servizio hub di notifica di Azure in hello back-end ASP.NET WebAPI.</span><span class="sxs-lookup"><span data-stu-id="ad721-173">In this section you add a new controller that exposes a way for client devices toosend a notification based on hello username tag using Azure Notification Hubs Service Management Library in hello ASP.NET WebAPI backend.</span></span>

1. <span data-ttu-id="ad721-174">Creare un altro nuovo controller denominato **NotificationsController**.</span><span class="sxs-lookup"><span data-stu-id="ad721-174">Create another new controller named **NotificationsController**.</span></span> <span data-ttu-id="ad721-175">Creazione di hello esattamente come è stato creato hello **RegisterController** nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="ad721-175">Create it hello same way you created hello **RegisterController** in hello previous section.</span></span>
2. <span data-ttu-id="ad721-176">In NotificationsController.cs, aggiungere hello seguente `using` istruzioni:</span><span class="sxs-lookup"><span data-stu-id="ad721-176">In NotificationsController.cs, add hello following `using` statements:</span></span>
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. <span data-ttu-id="ad721-177">Aggiungere hello seguente metodo toohello **NotificationsController** classe.</span><span class="sxs-lookup"><span data-stu-id="ad721-177">Add hello following method toohello **NotificationsController** class.</span></span>
   
    <span data-ttu-id="ad721-178">Questo codice di inviare un tipo di notifica basato su piattaforma Notification Service (PNS) hello `pns` parametro.</span><span class="sxs-lookup"><span data-stu-id="ad721-178">This code send a notification type based on hello Platform Notification Service (PNS) `pns` parameter.</span></span> <span data-ttu-id="ad721-179">Hello valore `to_tag` è usato tooset hello *username* tag messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="ad721-179">hello value of `to_tag` is used tooset hello *username* tag on hello message.</span></span> <span data-ttu-id="ad721-180">Questo tag deve corrispondere a un tag username di una registrazione dell'hub di notifica attiva.</span><span class="sxs-lookup"><span data-stu-id="ad721-180">This tag must match a username tag of an active notification hub registration.</span></span> <span data-ttu-id="ad721-181">messaggio di notifica Hello è estratto dal corpo hello della richiesta POST per hello e formattato per la destinazione di hello PNS.</span><span class="sxs-lookup"><span data-stu-id="ad721-181">hello notification message is pulled from hello body of hello POST request and formatted for hello target PNS.</span></span> 
   
    <span data-ttu-id="ad721-182">A seconda del servizio notifica piattaforma (PNS) che i dispositivi supportati usano le notifiche di tooreceive hello, notifiche diverse sono supportate con formati diversi.</span><span class="sxs-lookup"><span data-stu-id="ad721-182">Depending on hello Platform Notification Service (PNS) that your supported devices use tooreceive notifications, different notifications are supported using different formats.</span></span> <span data-ttu-id="ad721-183">Ad esempio nei dispositivi Windows è possibile usare una [notifica di tipo avviso popup con WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) che non è supportata direttamente da un altro PNS.</span><span class="sxs-lookup"><span data-stu-id="ad721-183">For example on Windows devices, you could use a [toast notification with WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) that isn't directly supported by another PNS.</span></span> <span data-ttu-id="ad721-184">Il back-end è quindi necessario notifica hello tooformat in una notifica supportata per hello PNS dei dispositivi è pianificare toosupport.</span><span class="sxs-lookup"><span data-stu-id="ad721-184">So your backend would need tooformat hello notification into a supported notification for hello PNS of devices you plan toosupport.</span></span> <span data-ttu-id="ad721-185">Utilizza quindi hello trasmissione API hello [NotificationHubClient classe](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span><span class="sxs-lookup"><span data-stu-id="ad721-185">Then use hello appropriate send API on hello [NotificationHubClient class](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span></span>
   
        public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag)
        {
            var user = HttpContext.Current.User.Identity.Name;
            string[] userTag = new string[2];
            userTag[0] = "username:" + to_tag;
            userTag[1] = "from:" + user;
   
            Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;
            HttpStatusCode ret = HttpStatusCode.InternalServerError;
   
            switch (pns.ToLower())
            {
                case "wns":
                    // Windows 8.1 / Windows Phone 8.1
                    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" + 
                                "From " + user + ": " + message + "</text></binding></visual></toast>";
                    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
                    break;
                case "apns":
                    // iOS
                    var alert = "{\"aps\":{\"alert\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(alert, userTag);
                    break;
                case "gcm":
                    // Android
                    var notif = "{ \"data\" : {\"message\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendGcmNativeNotificationAsync(notif, userTag);
                    break;
            }
   
            if (outcome != null)
            {
                if (!((outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Abandoned) ||
                    (outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Unknown)))
                {
                    ret = HttpStatusCode.OK;
                }
            }
   
            return Request.CreateResponse(ret);
        }
4. <span data-ttu-id="ad721-186">Premere **F5** toorun hello applicazione e tooensure hello l'accuratezza del lavoro svolto finora.</span><span class="sxs-lookup"><span data-stu-id="ad721-186">Press **F5** toorun hello application and tooensure hello accuracy of your work so far.</span></span> <span data-ttu-id="ad721-187">applicazione Hello deve avviare un web browser e visualizzare hello ASP.NET home page.</span><span class="sxs-lookup"><span data-stu-id="ad721-187">hello app should launch a web browser and display hello ASP.NET home page.</span></span> 

## <a name="publish-hello-new-webapi-backend"></a><span data-ttu-id="ad721-188">Pubblicare hello nuovo WebAPI Backend</span><span class="sxs-lookup"><span data-stu-id="ad721-188">Publish hello new WebAPI Backend</span></span>
1. <span data-ttu-id="ad721-189">Ora si distribuirà questo tooan app sito Web di Azure in ordine toomake sia accessibile da tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="ad721-189">Now we will deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="ad721-190">Fare clic su hello **AppBackend** del progetto e selezionare **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="ad721-190">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="ad721-191">Selezionare **Servizio app di Microsoft Azure** come destinazione di pubblicazione e quindi fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="ad721-191">Select **Microsoft Azure App Service** as your publish target and click **Publish**.</span></span> <span data-ttu-id="ad721-192">Si aprirà hello Create Service App finestra di dialogo che consente di creare tutti hello necessarie risorse di Azure toorun hello app web ASP.NET in Azure.</span><span class="sxs-lookup"><span data-stu-id="ad721-192">This opens hello Create App Service dialog, which helps you create all hello necessary Azure resources toorun hello ASP.NET web app in Azure.</span></span>

    ![][B15]
3. <span data-ttu-id="ad721-193">In hello **Crea servizio App** finestra di dialogo, selezionare l'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="ad721-193">In hello **Create App Service** dialog, select your Azure account.</span></span> <span data-ttu-id="ad721-194">Fare clic su **Modifica tipo** e selezionare **App Web**.</span><span class="sxs-lookup"><span data-stu-id="ad721-194">Click **Change Type** and select **Web App**.</span></span> <span data-ttu-id="ad721-195">Mantenere hello **nome dell'applicazione Web** hello specificato e seleziona **sottoscrizione**, **gruppo di risorse**, e **piano di servizio App**.</span><span class="sxs-lookup"><span data-stu-id="ad721-195">Keep hello **Web App Name** given and select hello **Subscription**, **Resource Group**, and **App Service Plan**.</span></span>  <span data-ttu-id="ad721-196">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ad721-196">Click **Create**.</span></span>

4. <span data-ttu-id="ad721-197">Prendere nota di hello **URL del sito** proprietà hello **riepilogo** sezione.</span><span class="sxs-lookup"><span data-stu-id="ad721-197">Make a note of hello **Site URL** property in hello **Summary** section.</span></span> <span data-ttu-id="ad721-198">Si farà riferimento toothis URL come il *endpoint di back-end* più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ad721-198">We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="ad721-199">Fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="ad721-199">Click **Publish**.</span></span>

5. <span data-ttu-id="ad721-200">Una volta completata la procedura guidata hello, pubblica tooAzure di app web ASP.NET hello e quindi avvia hello app nel browser predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="ad721-200">Once hello wizard completes, it publishes hello ASP.NET web app tooAzure, and then launches hello app in hello default browser.</span></span>  <span data-ttu-id="ad721-201">L'applicazione sarà visibile in Servizi app di Azure.</span><span class="sxs-lookup"><span data-stu-id="ad721-201">Your application will be viewable in Azure App Services.</span></span>

<span data-ttu-id="ad721-202">URL di Hello utilizza nome dell'applicazione web hello specificato in precedenza, con http://<app_name>.azurewebsites.net formato hello.</span><span class="sxs-lookup"><span data-stu-id="ad721-202">hello URL uses hello web app name that you specified earlier, with hello format http://<app_name>.azurewebsites.net.</span></span>

[B1]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push1.png
[B2]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push2.png
[B3]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push3.png
[B4]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push4.png
[B5]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push5.png
[B6]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push6.png
[B7]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push7.png
[B8]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push8.png
[B14]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push14.png
[B15]: ./media/notification-hubs-aspnet-backend-notifyusers/publish-to-app-service.png
[B16]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users16.PNG
[B18]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users18.PNG
